# CSE 135 Homework

This repository hosts the website for CSE 135 homework. It includes a homepage, personal pages, and links to weekly homework assignments. The website is hosted on a DigitalOcean droplet and automatically deploys from GitHub using GitHub Actions.

## Features

- **Homepage**: Includes an overview and links to assignments.
- **Personal Pages**: Each team member has their own page with information about themselves.
- **Deployment**: The website is deployed automatically to DigitalOcean via GitHub Actions whenever changes are pushed to the repository.

## Setup Instructions

### 1. Clone the repository
```bash
git clone https://github.com/TheAsianFish/cse135hw.git
cd cse135hw
```


## Login Instructions

### Domain: https://cse135patrick.site

### Grader Password
```bash
135grader
```

## Site Contents
- Personal Page:   https://cse135patrick.site/members/patrickchung.html
- Favicon:   `/favicon.png`
- Robots:   `/robots.txt`
- PHP verification page:    https://cse135patrick.site/hw1/hello.php
- GoAccess analytics report:    https://cse135patrick.site/hw1/report.html


## GitHub Auto-Deploy Setup
- Repository: https://github.com/TheAsianFish/cse135hw
- Deployent via **GitHub Actions**
- Every push on 'main' copies files to /var/www/html/cse135hw
- Apache is restarted automatically after deployment


## Compression
```bash
After Apache compression was enabled using 'mod_deflate', the content files are compressed before being sent to the browser. Verification was done in DevTools and in the Network tab where responses show 'Content-Encoding: gzip' and reduced sizes
```

## Server Header Obfuscation
```bash
Enabled mod_headers and set ServerTokens Prod and ServerSignature Off. A local virtual host was created on 127.0.0.1:8080 and the public HTTPS virtual host proxies these requests to this internal listener. The outgoing response header is explicitly set using mod_headers resulting in the final resposne header: 'Server: CSE135 Server'.
```

## Access Logs & Analytics
- Apache logs located at: /var/log/apache2/access.log
- Generated GoAccess report using: goaccess access.log --log-format=COMBINED

