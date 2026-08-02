# ROADMAP — PortSwigger Web Security Academy

Checking off labs as I go.

---

## SQL Injection (18 labs)

- [x] SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
- [x] SQL injection vulnerability allowing login bypass
- [ ] SQL injection attack, querying the database type and version on Oracle
- [ ] SQL injection attack, querying the database type and version on MySQL and Microsoft
- [ ] SQL injection attack, listing the database contents on non-Oracle databases
- [ ] SQL injection attack, listing the database contents on Oracle
- [ ] SQL injection UNION attack, determining the number of columns returned by the query
- [ ] SQL injection UNION attack, finding a column containing text
- [ ] SQL injection UNION attack, retrieving data from other tables
- [ ] SQL injection UNION attack, retrieving multiple values in a single column
- [ ] Blind SQL injection with conditional responses
- [ ] Blind SQL injection with conditional errors
- [ ] Blind SQL injection with time delays
- [ ] Blind SQL injection with out-of-band interaction
- [ ] Blind SQL injection with out-of-band data exfiltration
- [ ] SQL injection with filter bypass via XML encoding

## Cross-Site Scripting (36 labs)

- [ ] Reflected XSS into HTML context with nothing encoded
- [ ] Stored XSS into HTML context with nothing encoded
- [ ] DOM XSS in `document.write` sink using source `location.search`
- [ ] DOM XSS in `innerHTML` sink using source `location.search`
- [ ] DOM XSS in jQuery anchor `href` attribute sink using `location.search` source
- [ ] DOM XSS in jQuery selector sink using a hashchange event
- [ ] Reflected XSS into attribute with angle brackets HTML-encoded
- [ ] Stored XSS into `onclick` event with angle brackets and double quotes HTML-encoded and single quotes and backslash escaped
- [ ] Reflected XSS into a JavaScript string with angle brackets HTML encoded
- [ ] DOM XSS in `document.write` sink using source `location.search` inside a select element
- [ ] DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded
- [ ] Reflected DOM XSS
- [ ] Stored DOM XSS
- [ ] Reflected XSS with HTML-encoded with JavaScript string
- [ ] XSS in a JavaScript string with angle brackets HTML encoded (and remaining)
- [ ] Exploiting cross-site scripting to steal cookies
- [ ] Exploiting cross-site scripting to capture passwords
- [ ] Exploiting cross-site scripting to perform CSRF
- [ ] Reflected XSS with some SVG markup allowed
- [ ] Reflected XSS in canonical link tag
- [ ] Reflected XSS in a JavaScript URL with some characters blocked
- [ ] Reflected XSS with AngularJS sandbox escape without strings
- [ ] Reflected XSS with AngularJS sandbox escape and CSP
- [ ] Reflected XSS with event handlers and `href` attributes blocked
- [ ] Reflected XSS with all tags except custom ones blocked
- [ ] Reflected XSS in event handler and `href` attributes blocked
- [ ] Reflected XSS with some SVG tags allowed
- [ ] Reflected XSS in a JavaScript URL with some characters blocked
- [ ] Stored XSS into `onclick` event with angle brackets and double quotes HTML-encoded and single quotes and backslash escaped
- [ ] Reflected XSS with AngularJS sandbox escape without strings
- [ ] Reflected XSS with AngularJS sandbox escape and CSP
- [ ] XSS via `XMLHttpRequest`
- [ ] XSS via `innerHTML` mutation
- [ ] DOM XSS combined with reflected and stored data
- [ ] XSS in hidden input fields

## CSRF (3 labs)

- [ ] CSRF vulnerability with no defenses
- [ ] CSRF where token validation depends on request method
- [ ] CSRF where token validation depends on token being present

## Clickjacking (4 labs)

- [ ] Basic clickjacking with CSRF token protection
- [ ] Clickjacking with form input data prefilled from a URL parameter
- [ ] Clickjacking with a frame buster script
- [ ] Exploiting clickjacking vulnerability to trigger DOM-based XSS

## DOM-Based Vulnerabilities (2 labs)

- [ ] DOM XSS using web messages
- [ ] DOM XSS using web messages and a JavaScript URL

## Cross-Origin Resource Sharing (CORS) (3 labs)

- [ ] CORS vulnerability with basic origin reflection
- [ ] CORS vulnerability with trusted null origin
- [ ] CORS vulnerability with trusted insecure protocols

## WebSockets (2 labs)

- [ ] Manipulating WebSocket messages to exploit vulnerabilities
- [ ] Cross-site WebSocket hijacking

## Web Cache Poisoning (4 labs)

- [ ] Web cache poisoning with an unkeyed header
- [ ] Web cache poisoning with an unkeyed cookie
- [ ] Web cache poisoning with multiple headers
- [ ] Web cache poisoning via an unkeyed query parameter

## Deserialization (6 labs)

- [ ] Modifying serialized objects
- [ ] Modifying serialized data types
- [ ] Using application functionality to exploit insecure deserialization
- [ ] Arbitrary object injection in PHP
- [ ] Exploiting Java deserialization with Apache Commons
- [ ] Exploiting PHP deserialization with a pre-built gadget chain

## HTTP Request Smuggling (8 labs)

- [ ] HTTP request smuggling, confirming a CL.TE vulnerability via differential responses
- [ ] HTTP request smuggling, confirming a TE.CL vulnerability via differential responses
- [ ] HTTP request smuggling, confirming a TE.TE behavior via obfuscated TE header
- [ ] HTTP request smuggling, exploiting CL.TE vulnerability to bypass front-end security controls
- [ ] HTTP request smuggling, exploiting TE.CL vulnerability to bypass front-end security controls
- [ ] HTTP request smuggling, exploiting CL.TE vulnerability to deliver reflected XSS
- [ ] Exploiting HTTP request smuggling to capture other users requests
- [ ] Exploiting HTTP request smuggling to perform web cache poisoning

## OAuth Authentication (4 labs)

- [ ] Authentication bypass via OAuth implicit flow
- [ ] Forced OAuth profile linking
- [ ] OAuth account hijacking via CSRF
- [ ] Stealing OAuth access tokens via an open redirect

## File Upload Vulnerabilities (6 labs)

- [ ] Remote code execution via web shell upload
- [ ] Web shell upload via Content-Type restriction bypass
- [ ] Web shell upload via path traversal
- [ ] Web shell upload via extension blacklist bypass
- [ ] Web shell upload via obfuscated file extension
- [ ] Remote code execution via polyglot web shell upload

## **Path Traversal (8 labs)**

- [x] File path traversal, simple case
- [x] File path traversal, traversal sequences blocked with absolute path bypass
- [ ] File path traversal, traversal sequences stripped non-recursively
- [ ] File path traversal, traversal sequences stripped with superfluous URL-decode
- [ ] File path traversal, validation of start of path
- [ ] File path traversal, validation of file extension with null byte bypass
- [ ] File path traversal, validation of file extension with out-of-band resource load
- [ ] Lab: Multi-step path traversal

## **Access Control (14 labs)**

- [x] Unprotected admin functionality
- [x] Unprotected admin functionality with unpredictable URL
- [x] User role controlled by request parameter
- [x] User ID controlled by request parameter
- [x] User ID controlled by request parameter with data leakage in redirect
- [x] User ID controlled by request parameter with password disclosure
- [x] Insecure direct object references
- [x] User role can be modified in user profile
- [x] User ID controlled by request parameter, with unpredictable user IDs
- [ ] URL-based access control can be circumvented
- [ ] Method-based access control can be circumvented
- [ ] Multi-step process with no access control on one step
- [ ] Referer-based access control
- [ ] Insecure direct object references (horizontal privilege escalation)

## Authentication (11 labs)

- [ ] Username enumeration via different responses
- [ ] 2FA simple bypass
- [ ] Password reset broken logic
- [ ] Username enumeration via subtly different responses
- [ ] Username enumeration via response timing
- [ ] Broken brute-force protection, IP block
- [ ] Username enumeration via account lock
- [ ] 2FA bypass using a brute-force attack
- [ ] Brute-forcing a stay-logged-in cookie
- [ ] Offline password cracking
- [ ] Password reset poisoning via middleware

## Server-Side Request Forgery (SSRF) (6 labs)

- [x] Basic SSRF against the local server
- [x] Basic SSRF against another back-end system
- [ ] SSRF with blacklist-based input filter
- [ ] SSRF with whitelist-based input filter
- [ ] SSRF with filter bypass via open redirection vulnerability
- [ ] Blind SSRF with out-of-band detection

## XXE Injection (5 labs)

- [ ] Exploiting XXE using external entities to retrieve files
- [ ] Exploiting XXE to perform SSRF attacks
- [ ] Blind XXE with out-of-band interaction
- [ ] Blind XXE with out-of-band interaction via XML parameter entities
- [ ] Exploiting XInclude to retrieve files

## NoSQL Injection (4 labs)

- [ ] NoSQL injection, detecting
- [ ] NoSQL injection, bypassing authentication
- [ ] NoSQL injection, extracting data
- [ ] NoSQL injection, blind

## API Testing (5 labs)

- [ ] API endpoints exposed via Swagger
- [ ] Exploiting an API endpoint using documentation
- [ ] Finding and exploiting an unused API endpoint
- [ ] Mass assignment vulnerability
- [ ] Exploiting server-side parameter pollution in a query string
- [ ] Exploiting server-side parameter pollution in a REST URL

## Web LLM (1 lab)

- [ ] Web LLM

## GraphQL API (5 labs)

- [ ] GraphQL API
- [ ] GraphQL introspection
- [ ] GraphQL CSRF
- [ ] GraphQL IDOR
- [ ] GraphQL batching

---


---

Last updated: July 2026
