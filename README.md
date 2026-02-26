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
**Username**: grader  
**Password**: 135grader

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
After Apache compression was enabled using 'mod_deflate', the content files are compressed before being sent to the browser. Verification was done in DevTools and in the Network tab where responses show 'Content-Encoding: gzip' and reduced sizes


## Server Header Obfuscation
Enabled mod_headers and set ServerTokens Prod and ServerSignature Off. A local virtual host was created on 127.0.0.1:8080 and the public HTTPS virtual host proxies these requests to this internal listener. The outgoing response header is explicitly set using mod_headers resulting in the final resposne header: 'Server: CSE135 Server'.


## Access Logs & Analytics
- Apache logs located at: /var/log/apache2/access.log
- Generated GoAccess report using: goaccess access.log --log-format=COMBINED

---

## Homework 2 – CGI & Analytics

### Live Site
https://cse135patrick.site

Navigate to:
- **Homework 2 index**: https://cse135patrick.site/hw2/

All required CGI demos are linked from this page.

---

### Homework 2 – CGI Programs

For Homework 2, I implemented the required CGI demos in **three languages**:
- Python
- PHP
- Node.js

Each language includes the following five programs:
1. `hello-html-language`
2. `hello-json-language`
3. `environment-language`
4. `echo-language`
5. `state-language`

All CGI scripts are located on the server under:
- `/usr/lib/cgi-bin/`

The HTML pages (homepage, HW2 index, echo form tester, fingerprint demo) are located under:
- `/var/www/html/cse135hw/`


The **Echo Form Tester** is a standalone HTML page used to test all echo endpoints across languages and supports:
- GET / POST / PUT / DELETE
- x-www-form-urlencoded and application/json
- JavaScript-enabled and no-JavaScript fallback modes

---

### Third-Party Analytics

#### Approach 3: Free Choice – Microsoft Clarity
For the free-choice analytics tool, I evaluated several options and chose **Microsoft Clarity**.

**Why Clarity:**
Clarity was chosen because it is free, simple to integrate, and provides session replays and heatmaps without requiring backend changes.

It was verified by observing recorded user sessions in the Clarity dashboard. While Clarity offers strong visual insight into user behavior, it focuses more on the screen replay
so it works best alongside tools like Google Analytics.

Screenshot included:
- `free-choice.png`

### Homework 3 – Data Collection and Storage

## Server IP:
159.223.192.78

- Target Site:  
  https://test.cse135patrick.site

- Collector Endpoint:  
  https://collector.cse135patrick.site/log.php

- Reporting REST API:  
  https://reporting.cse135patrick.site/api/events/

## Database
PostgreSQL database
Database name: cse135
Table: events

### Notes

- Sessioning implemented using `sessionStorage` per tab (`sid`).
- Events are tied together using the `sid` field.
- Performance, static, and activity events are collected.
- Data is written to both JSONL and PostgreSQL.
- REST endpoint returns data directly from PostgreSQL.










