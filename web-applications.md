# Information gathering
1. `/robots.txt` - Are there any disallowed paths that look interesting? 
2. `/sitemap.xml` - Check sitemap to map out all public areas of the website/application.
4. `favicon.ico` - Can give away what framework was used to build the application. Download the favicon, `md5sum` it and see if it's listed here 👉 https://wiki.owasp.org/index.php/OWASP_favicon_database
5. `HTTP Headers` - Might give away useful details about the application, such as programming language, webserver, CDNs
6. `View Source` - Manually view HTML, CSS & JS files for clues
7. `Automated tools` - Tools like https://builtwith.com/ and https://www.wappalyzer.com/ can help with automating parts of the information gathering process.
10. `google dorking` - Google dorking the website for common mistakes might be an option? 
