# EXTRA CREDIT: Fingerprinting Demo (HW2)

## What I built
A small demo that assigns a user ID via cookies, and also computes a browser fingerprint using FingerprintJS. The page sends both to a Node CGI endpoint which stores a simple mapping from fingerprint -> last seen cookie ID.

Demo URL: https://cse135patrick.site/hw2/fingerprint.html

## How it works
- On load, the page creates/reads a cookie `cse135_uid`.
- The page generates a FingerprintJS `visitorId`.
- The page POSTs `{ uid, visitorId, ts }` to `/cgi-bin/fingerprint-node.js`.
- The server stores the mapping in a JSON file under `/tmp` and returns a small HTML result.

## How to test
1. Visit the demo page normally (mapping is created).
2. Clear cookies for the site and refresh.
3. The cookie-based ID changes, but the fingerprint often stays the same, so the server can re-associate activity.

## Notes
- Fingerprinting requires JavaScript. With JS disabled, only cookie/session tracking works.
- Fingerprints can change due to browser updates, privacy settings, extensions, or different devices.
- This demo is for coursework only and is not intended for production tracking without consent.
