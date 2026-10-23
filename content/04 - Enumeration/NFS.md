Network File System (NFS) is a network file system and has the same purpose as SMB. Its purpose is to access file systems over a network as if they were local. However, it uses an entirely different protocol.

---
## Show Available NFS Share
```bash
showmount -e 10.129.14.128
```

---
## Mounting NFS Share
```bash
# Create a directory
mkdir empty

# mount the nfs with the newly created directory
sudo mount -t nfs 10.129.14.128:/ ./empty/ -o nolock

# Change directory
cd empty

# See the whole directory with tree
tree .
```

---
## Unmounting
```bash
# Exit the mounted NFS
cd ..

# Unmount
sudo umount ./empty
```
