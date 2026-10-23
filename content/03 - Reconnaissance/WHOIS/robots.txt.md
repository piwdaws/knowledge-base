## Definition
- A text file located at: /robots.txt It contains directives telling web crawlers which areas they should or should not crawl.

---
## Example of the page 
```html
User-agent: * 
Disallow: /admin/ 
Disallow: /private/ 
Allow: /public/ 
User-agent: Googlebot 
Crawl-delay: 10 
Sitemap: https://www.example.com/sitemap.xml
```

- All user agent are disallow from accessing admin page
- But now we know admin page is exist so we can explore it
- 