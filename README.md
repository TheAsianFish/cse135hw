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


### Homework 4 – MVC Reporting Dashboard (Derisk Checkpoint)

## Dashboard Login

URL:  
https://reporting.cse135patrick.site/login.php

Credentials:  
Username: grader  
Password: 135grader

---

## Step 1 – MVC Web Application with Authentication

A reporting dashboard was implemented using PHP with an MVC-style structure.  
Authentication is required before accessing reporting pages. If a user attempts to directly access protected URLs, they are redirected to the login page.

Protected pages:
- https://reporting.cse135patrick.site/reports/index.php
- https://reporting.cse135patrick.site/reports/table.php
- https://reporting.cse135patrick.site/reports/charts.php

### MVC Structure

Model (Data Layer)
- `lib/db.php` – PostgreSQL database connection

View (Presentation Layer)
- `login.php`
- `reports/index.php`
- `reports/table.php`
- `reports/charts.php`
- `lib/layout.php`

Controller (Application Logic)
- `lib/auth.php`
- `login.php`
- `logout.php`

---

## Step 2 – Datastore Connected to Table/Grid

A reporting page displays collected analytics data from PostgreSQL in a raw HTML table.

URL:  
https://reporting.cse135patrick.site/reports/table.php

The table reads from the `events` table and displays fields such as:
- Event ID
- Timestamp
- Event Type
- Session ID
- Page URL

---

## Step 3 – Datastore Connected to Charts

Charts were implemented using Chart.js to visualize aggregated analytics data.

URL:  
https://reporting.cse135patrick.site/reports/charts.php

Charts include:

Event Count by Type
```sql
SELECT type, COUNT(*) AS count
FROM events
GROUP BY type
ORDER BY count DESC;
```

Top Pages by Event Count
```sql
SELECT page, COUNT(*) AS count
FROM events
GROUP BY page
ORDER BY count DESC
LIMIT 10;
```

The charts dynamically update based on the data stored in PostgreSQL.

---

## Summary

The Homework 4 dashboard connects the analytics pipeline built in Homework 3 to a reporting interface.

```
Browser Events
   ↓
collector.js
   ↓
log.php ingestion endpoint
   ↓
PostgreSQL events table
   ↓
Reporting dashboard
   ↓
Tables and charts
```


### Homework 5 – Reporting DashBoard Final Push

# Project Overview

This project implements a secure reporting dashboard built on top of the analytics
collector developed earlier in the course.

The system allows authenticated users to explore analytics data, generate reports,
and export them for sharing or documentation.

The dashboard supports multiple roles with authorization rules controlling which
sections of the reporting system a user can access.

Reports include charts, data tables, and analyst commentary to provide
interpretation of collected analytics data.

The system focuses on:

• authentication security  
• role-based authorization  
• server-side analytics processing  
• data visualization  
• exportable reporting  

---

# Deployment

Live deployment:

```
https://reporting.cse135patrick.site/login.php
https://reporting.cse135patrick.site/reports/index.php
```

Test site generating analytics data:

```
https://test.cse135patrick.site
```

---

# Report Categories

Three main report types are implemented:

### Overview Report

Displays high-level traffic statistics:

• total events  
• session counts  
• unique pages  
• event activity over time  
• most visited pages  

Charts:

• events by day line chart  
• event type distribution chart  

---

### Performance Report

Displays performance metrics captured from the client.

Metrics:

• average load time  
• maximum load time  
• page-level performance  

Charts:

• average load time by page  

---

### Error Report

Displays captured client errors.

Metrics:

• total error count  
• grouped error messages  
• error frequency  

Charts:

• error trend by day  

---

# Saved Reports

Analysts can save curated reports.

Saved reports contain:

• title  
• description  
• analyst interpretation  
• category  
• chart visualizations  
• export functionality  

Viewers can access saved reports but cannot modify them.

---

# Export System

Reports can be exported to PDF.

The export system generates a PDF version of a report page which can be downloaded
and shared.

---

# Authentication and Authorization

Three user roles are implemented:

```
super_admin
analyst
viewer
```

Permissions:

Super Admin
• manage users
• access all reports

Analyst
• view report sections
• create and edit saved reports

Viewer
• view saved reports only

Authorization checks protect all report endpoints.

---

# Data Visualization

Charts are implemented using Chart.js.

Visualization types include:

• line charts
• bar charts
• horizontal bar charts

Tables complement the charts to provide detailed numerical values.

The dashboard includes metric cards to summarize key indicators.

---

# AI Usage

AI tools were used to assist with:

• code formatting
• UI improvements
• chart configuration suggestions
• documentation drafting

All code was reviewed and tested manually before deployment.

AI tools were treated as a coding assistant rather than an autonomous generator.

---

# Future Improvements

For future iterations, the following improvements could be added:

• date range filtering for reports  
• session replay insights  
• performance percentile metrics  
• scheduled automated reports

---

# Lessons Learned

This project reinforced the importance of:

• server-side authorization checks  
• clean dashboard presentation  
• balancing visualization with performance  
• designing analytics systems that remain simple but extensible

The final dashboard demonstrates how analytics data can be collected, analyzed,
and presented through a structured reporting interface.









