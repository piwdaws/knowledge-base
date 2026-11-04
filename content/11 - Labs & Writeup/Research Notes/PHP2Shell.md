## Overview
PHP2shell is a pair of hight impact CVE (**CVE-2026-109618** and **CVE-2026-109619**). Concerning memory flaws in PHP version 5.4 - 8.5 that allow remote code execution (RCE) and gain remote control of targeted website host.

The vulnerability have been existed way back in 2012 but its only been discover with the help of AI in August 2026 and its existence was pubicly announced on 20 October 2026. 

## Discovery 
The vulnerability were discovered by Ryan Austin, a researcher at the California-based security firm Calif as part of OpenAi "Patch The Planet" project in August 2026, and a security company, Wiz. 

---
## What is happening
PHP is a programming language that run large portion of website in the world. When something goes badly wrong happen, inside PHP got a 'panic button' which it presses immediately when something goes wrong. The problem is, it doesnt clean up itself and abandoned whatever it was doing in the middle of it and leaving it unfinished. 

Normally that is harmless, but researcher found out that attacker can trigger that panic at exactly the right moment, then take advantage of the mess left behind to trick the server into running attacker own command. 

---
## Two vulnerabilities  
### CVE-2026-109618 - Out-Of-Memory Handling
- PHP fails to clean up correctly when request processing runs out of memory or exits abnormally. Later cleanup can encounter incomplete or inconsistent internal data.

### CVE-2026-109619 - Stale pointers / use-after-free
- PHP retains a reference to memory that has been freed, then later code can use that invalid reference

Two different failure conditions in PHP's request-processing and cleanup logic. And should not be treated as one identical bug. 

You dont need credential for this just a web request is enough

---
## Understanding the technical in-depth
PHP core engine is called **Zend**. When PHP need to abort due to fatal condition. Like running out of memory, hitting a timeout, a dropped connection or so on. It calls an internal function named `zend_bailout()`. This function performed what called a `longjmp`. It basically just jump out of anything it was running. Skipping a normal cleanup step that would have done on its way.

---

## CVE-2026-109618 - Out-Of-Memory Handling
**Understanding Out-Of-memory**
This bug caused the memory clean up stop halfway and causing the data to be inconsistent and cause a memory corruption. 

The way it work, the attacker deliberately send a crafted multipart upload or web request to trigger the `zend_bailout()`. The payload would forced PHP to run out of memory and PHP will try to clean up the memory. The next stage of the payload would trigger the `zend_bailout()` to stop the cleanup halfway, leaving it uninitialized and partially built in memory. Later code in the same request read that entry as if its valid and executing the attacker command

Red Hat describes this vulnerability as a failure to roll back incomplete state after a memory allocation failure, followed by cleanup operating on uninitialized memory.

---

## CVE-2026-109619 — PHP uses stale pointers
**How it lead to stale pointers**
The same `zend_bailout()` can interrupt PHP's session upload-progress tracking feature (session.upload_progress). One reported chain involves the internal function `zend_hash_update()`, which — via PHP's normal memory-cleanup routine, `zval_ptr_dtor()` — frees a block of memory that a stales pointer still points to. 

A later, separate web request can cause that freed memory to be reused for attacker-supplied data. When PHP's engine calls `zend_call_function()` the PHP uses any time it calls a function internally and it ends up calling through that corrupted pointer, which the attacker has shaped to point at their own fake instructions, resulting in arbitrary command execution on the server.


---
## The official fix made by PHP foundation

A commit `01a40e89fb`, "Avoid state corruption via bailout". It changes how PHP's memory manager handles running out of memory. Instead of immediately panicking with `zend_bailout()`, PHP now has a "fallible allocation" mode (femalloc / safe_ferealloc, gated by a check called ZEND_HAS_OOM()) that simply returns "no memory available" as a normal result the calling code can check for and handle gracefully, rather than aborting mid-operation.

This is a flaw in the PHP language runtime itself and not in any specific application's code. That means a website can be vulnerable purely because of the PHP version it runs, even if the application code on top of it has no bugs of its own. Any PHP app regardless of framework (WordPress, Laravel, Symfony, plain PHP, etc.) is affected if it's running an unpatched PHP version.

---
## A well documented POC for PHP2Shell

**"Steal My Bitcoin" challenge was a Capture The Flag (CTF) security contest** launched in late October 2026 by cybersecurity researcher James Pavur. The challenge put a $2,000 Bitcoin bounty on a live server to test the real-world exploitability of the controversial **PHP2Shell vulnerability**

The challenge concluded when a UK-based penetration tester known online as **"Killer" (or "killa") successfully breached the server and claimed the prize**

[StealMyBitcoin-POC](https://github.com/KillaBoi/StealMyBitcoin-PoC)

The POC is well written on itself but here a simplified version on how it works

The script itself is a 4 stages memory corruption exploit toward PHP server. 

**Stage 1** - OOM crush
- The script sends a multipart request with **deeply nested field names**. Blowing past the 128 MiB limit. The worker crashes mid-parse, leaving **stale session data** sitting in heap memory. 

**Stage 2** - Heap Address Leak
- Multiple HTTP requests race to be handled by **that same crashed worker** before it’s cleaned up. One of them triggers PHP to serialize its session into the `PHPSESSID` cookie since the heap is stale and partially overwritten, it serializes **256 bytes of raw heap memory** instead of a normal session ID.

- `heap_candidate()` scans these  bytes for **pointers that agree on the same Zend heap chunk base**. This defeats **ASLR** for the heap.

**Stage 3** - Code Pointer Leak
- Same trick but this time the stale memory contains `zval_ptr_dtor` , a **function pointer inside the PHP binary itself**.

- `code_candidate()` validates it by checking the low 21 bits match the expected value. Since ASLR doesn’t move page offsets, this fingerprint confirms the right pointer was leaked. Now the code image base is known, which also defeats **code ASLR**.

**Stage 4** - Forge a HashTable
- The payload then calculates the exact heap address where a controlled value will land by using the leaked chunk base + a calibrated offset

- Builds a **forged `zend_array` (HashTable)** at that address. A fake PHP internal data structure

- That HashTable is set to `zif_system` (PHP’s internal `system()` function)

- The fake structure also embeds a `zend_string` containing the shell **command to execute**

When PHP’s cleanup code runs on the forged HashTable, it calls the `zif_system` and executing arbitrary OS commands as the PHP process.

---
## Defeating the ASLR is the key
**ASLR (Address Space Layout Randomization)** randomizes where the OS loads things into memory every time a process starts.

ASLR protects **static binaries** from having predictable memory layouts. 

So if you can make the process _tell you_ where things are (via the stale heap leak), ASLR is neutralized entirely.

---
## Source
[Wikipedia PHP2shell](https://en.wikipedia.org/wiki/PHP2Shell)
[ox-security](https://www.ox.security/blog/cve-2026-109618-cve-2026-109619-two-vulnerabilities-allow-unauthenticated-rce-in-php/)
[Medium](https://levelup.gitconnected.com/php2shell-two-critical-php-flaws-are-being-exploited-heres-how-to-patch-today-add61aa15d10)
[Picus-security](https://www.picussecurity.com/resource/php2shell-the-two-critical-php-rce-flaws-cve-2026-109618-cve-2026-109619-explained)
[PHP2Shell explained in 10 minutes (A technical analysis)](https://www.youtube.com/watch?v=K8EXJIDk-K4)




