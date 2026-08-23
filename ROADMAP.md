# ROADMAP — PortSwigger Web Security Academy

Checking off labs as I go.

---

## SQL Injection (18 labs)

- [x] SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
- [x] SQL injection vulnerability allowing login bypass
- [x] SQL injection attack, querying the database type and version on Oracle
- [x] SQL injection attack, querying the database type and version on MySQL and Microsoft
- [x] SQL injection attack, listing the database contents on non-Oracle databases
- [x] SQL injection attack, listing the database contents on Oracle
- [x] SQL injection UNION attack, determining the number of columns returned by the query
- [x] SQL injection UNION attack, finding a column containing text
- [x] SQL injection UNION attack, retrieving data from other tables
- [x] SQL injection UNION attack, retrieving multiple values in a single column
- [x] Blind SQL injection with conditional responses
- [x] Blind SQL injection with conditional errors
- [x] Visible error-based SQL injection
- [x] Blind SQL injection with time delays
- [ ] Blind SQL injection with time delays and information retrieval
- [ ] Blind SQL injection with out-of-band interaction
- [ ] Blind SQL injection with out-of-band data exfiltration
- [x] SQL injection with filter bypass via XML encoding

## Cross-Site Scripting (XSS) (30 labs)

- [x] Reflected XSS into HTML context with nothing encoded
- [x] Stored XSS into HTML context with nothing encoded
- [ ] DOM XSS in `document.write` sink using source `location.search`
- [x] DOM XSS in `innerHTML` sink using source `location.search`
- [ ] DOM XSS in jQuery anchor `href` attribute sink using `location.search` source
- [ ] DOM XSS in jQuery selector sink using a hashchange event
- [ ] Reflected XSS into attribute with angle brackets HTML-encoded
- [ ] Stored XSS into anchor `href` attribute with double quotes HTML-encoded
- [ ] Reflected XSS into a JavaScript string with angle brackets HTML encoded
- [x] DOM XSS in `document.write` sink using source `location.search` inside a select element
- [ ] DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded
- [ ] Reflected DOM XSS
- [ ] Stored DOM XSS
- [ ] Reflected XSS into HTML context with most tags and attributes blocked
- [ ] Reflected XSS into HTML context with all tags blocked except custom ones
- [ ] Reflected XSS with some SVG markup allowed
- [ ] Reflected XSS in canonical link tag
- [ ] Reflected XSS into a JavaScript string with single quote and backslash escaped
- [ ] Reflected XSS into a JavaScript string with angle brackets and double quotes HTML-encoded and single quotes escaped
- [ ] Stored XSS into `onclick` event with angle brackets and double quotes HTML-encoded and single quotes and backslash escaped
- [ ] Reflected XSS into a template literal with angle brackets, single, double quotes, backslash and backticks Unicode-escaped
- [ ] Exploiting cross-site scripting to steal cookies
- [ ] Exploiting cross-site scripting to capture passwords
- [ ] Exploiting XSS to bypass CSRF defenses
- [ ] Reflected XSS with AngularJS sandbox escape without strings
- [ ] Reflected XSS with AngularJS sandbox escape and CSP
- [ ] Reflected XSS with event handlers and `href` attributes blocked
- [ ] Reflected XSS in a JavaScript URL with some characters blocked
- [ ] Reflected XSS protected by very strict CSP, with dangling markup attack
- [ ] Reflected XSS protected by CSP, with CSP bypass

## Cross-Site Request Forgery (CSRF) (12 labs)

- [ ] CSRF vulnerability with no defenses
- [ ] CSRF where token validation depends on request method
- [ ] CSRF where token validation depends on token being present
- [ ] CSRF where token is not tied to user session
- [ ] CSRF where token is tied to non-session cookie
- [ ] CSRF where token is duplicated in cookie
- [ ] SameSite Lax bypass via method override
- [ ] SameSite Strict bypass via client-side redirect
- [ ] SameSite Strict bypass via sibling domain
- [ ] SameSite Lax bypass via cookie refresh
- [ ] CSRF where Referer validation depends on header being present
- [ ] CSRF with broken Referer validation

## Clickjacking (5 labs)

- [ ] Basic clickjacking with CSRF token protection
- [ ] Clickjacking with form data prefilled from a URL parameter
- [ ] Clickjacking with a frame buster script
- [ ] Exploiting a clickjacking vulnerability to trigger DOM-based XSS
- [ ] Multistep clickjacking

## DOM-Based Vulnerabilities (7 labs)

- [ ] DOM XSS using web messages
- [ ] DOM XSS using web messages and a JavaScript URL
- [ ] DOM XSS using web messages and JSON.parse
- [ ] DOM-based open redirection
- [ ] DOM-based cookie manipulation
- [ ] Exploiting DOM clobbering to enable XSS
- [ ] Clobbering DOM attributes to bypass HTML filters

## Cross-Origin Resource Sharing (CORS) (3 labs)

- [ ] CORS vulnerability with basic origin reflection
- [ ] CORS vulnerability with trusted null origin
- [ ] CORS vulnerability with trusted insecure protocols

## XML External Entity (XXE) Injection (9 labs)

- [ ] Exploiting XXE using external entities to retrieve files
- [ ] Exploiting XXE to perform SSRF attacks
- [ ] Blind XXE with out-of-band interaction
- [ ] Blind XXE with out-of-band interaction via XML parameter entities
- [ ] Exploiting blind XXE to exfiltrate data using a malicious external DTD
- [ ] Exploiting blind XXE to retrieve data via error messages
- [ ] Exploiting XInclude to retrieve files
- [ ] Exploiting XXE via image file upload
- [ ] Exploiting XXE to retrieve data by repurposing a local DTD

## Server-Side Request Forgery (SSRF) (7 labs)

- [x] Basic SSRF against the local server
- [x] Basic SSRF against another back-end system
- [ ] Blind SSRF with out-of-band detection
- [ ] SSRF with blacklist-based input filter
- [ ] SSRF with filter bypass via open redirection vulnerability
- [ ] Blind SSRF with Shellshock exploitation
- [ ] SSRF with whitelist-based input filter

## HTTP Request Smuggling (22 labs)

- [ ] HTTP request smuggling, confirming a CL.TE vulnerability via differential responses
- [ ] HTTP request smuggling confirming a TE.CL vulnerability via differential responses
- [ ] Exploiting HTTP request smuggling to bypass front-end security controls, CL.TE vulnerability
- [ ] Exploiting HTTP request smuggling to bypass front-end security controls, TE.CL vulnerability
- [ ] Exploiting HTTP request smuggling to reveal front-end request rewriting
- [ ] Exploiting HTTP request smuggling to capture other users' requests
- [ ] Exploiting HTTP request smuggling to deliver reflected XSS
- [ ] Response queue poisoning via H2.TE request smuggling
- [ ] H2.CL request smuggling
- [ ] HTTP/2 request smuggling via CRLF injection
- [ ] HTTP/2 request splitting via CRLF injection
- [ ] 0.CL request smuggling
- [ ] CL.0 request smuggling
- [ ] HTTP request smuggling, basic CL.TE vulnerability
- [ ] HTTP request smuggling, basic TE.CL vulnerability
- [ ] HTTP request smuggling, obfuscating the TE header
- [ ] Exploiting HTTP request smuggling to perform web cache poisoning
- [ ] Exploiting HTTP request smuggling to perform web cache deception
- [ ] Bypassing access controls via HTTP/2 request tunnelling
- [ ] Web cache poisoning via HTTP/2 request tunnelling
- [ ] Client-side desync
- [ ] Server-side pause-based request smuggling

## OS Command Injection (5 labs)

- [ ] OS command injection, simple case
- [ ] Blind OS command injection with time delays
- [ ] Blind OS command injection with output redirection
- [ ] Blind OS command injection with out-of-band interaction
- [ ] Blind OS command injection with out-of-band data exfiltration

## Server-Side Template Injection (SSTI) (7 labs)

- [ ] Basic server-side template injection
- [ ] Basic server-side template injection (code context)
- [ ] Server-side template injection using documentation
- [ ] Server-side template injection in an unknown language with a documented exploit
- [ ] Server-side template injection with information disclosure via user-supplied objects
- [ ] Server-side template injection in a sandboxed environment
- [ ] Server-side template injection with a custom exploit

## Path Traversal (6 labs)

- [x] File path traversal, simple case
- [x] File path traversal, traversal sequences blocked with absolute path bypass
- [ ] File path traversal, traversal sequences stripped non-recursively
- [ ] File path traversal, traversal sequences stripped with superfluous URL-decode
- [ ] File path traversal, validation of start of path
- [ ] File path traversal, validation of file extension with null byte bypass

## Access Control (13 labs)

- [x] Unprotected admin functionality
- [x] Unprotected admin functionality with unpredictable URL
- [x] User role controlled by request parameter
- [x] User role can be modified in user profile
- [x] User ID controlled by request parameter
- [x] User ID controlled by request parameter, with unpredictable user IDs
- [x] User ID controlled by request parameter with data leakage in redirect
- [x] User ID controlled by request parameter with password disclosure
- [x] Insecure direct object references
- [x] URL-based access control can be circumvented
- [x] Method-based access control can be circumvented
- [x] Multi-step process with no access control on one step
- [x] Referer-based access control

## Authentication (14 labs)

- [ ] Username enumeration via different responses
- [ ] 2FA simple bypass
- [ ] Password reset broken logic
- [ ] Username enumeration via subtly different responses
- [ ] Username enumeration via response timing
- [ ] Broken brute-force protection, IP block
- [ ] Username enumeration via account lock
- [ ] 2FA broken logic
- [ ] Brute-forcing a stay-logged-in cookie
- [ ] Offline password cracking
- [ ] Password reset poisoning via middleware
- [ ] Password brute-force via password change
- [ ] Broken brute-force protection, multiple credentials per request
- [ ] 2FA bypass using a brute-force attack

## WebSockets (3 labs)

- [ ] Manipulating WebSocket messages to exploit vulnerabilities
- [ ] Cross-site WebSocket hijacking
- [ ] Manipulating the WebSocket handshake to exploit vulnerabilities

## Web Cache Poisoning (13 labs)

- [ ] Web cache poisoning with an unkeyed header
- [ ] Web cache poisoning with an unkeyed cookie
- [ ] Web cache poisoning with multiple headers
- [ ] Targeted web cache poisoning using an unknown header
- [ ] Web cache poisoning via an unkeyed query string
- [ ] Web cache poisoning via an unkeyed query parameter
- [ ] Parameter cloaking
- [ ] Web cache poisoning via a fat GET request
- [ ] URL normalization
- [ ] Web cache poisoning to exploit a DOM vulnerability via a cache with strict cacheability criteria
- [ ] Combining web cache poisoning vulnerabilities
- [ ] Cache key injection
- [ ] Internal cache poisoning

## Insecure Deserialization (10 labs)

- [ ] Modifying serialized objects
- [ ] Modifying serialized data types
- [ ] Using application functionality to exploit insecure deserialization
- [ ] Arbitrary object injection in PHP
- [ ] Exploiting Java deserialization with Apache Commons
- [ ] Exploiting PHP deserialization with a pre-built gadget chain
- [ ] Exploiting Ruby deserialization using a documented gadget chain
- [ ] Developing a custom gadget chain for Java deserialization
- [ ] Developing a custom gadget chain for PHP deserialization
- [ ] Using PHAR deserialization to deploy a custom gadget chain

## Information Disclosure (5 labs)

- [ ] Information disclosure in error messages
- [ ] Information disclosure on a debug page
- [ ] Source code disclosure via backup files
- [ ] Authentication bypass via information disclosure
- [ ] Information disclosure in version control history

## Business Logic Vulnerabilities (12 labs)

- [ ] Excessive trust in client-side controls
- [ ] High-level logic vulnerability
- [ ] Inconsistent security controls
- [ ] Flawed enforcement of business rules
- [ ] Low-level logic flaw
- [ ] Inconsistent handling of exceptional input
- [ ] Weak isolation on dual-use endpoint
- [ ] Insufficient workflow validation
- [ ] Authentication bypass via flawed state machine
- [ ] Infinite money logic flaw
- [ ] Authentication bypass via encryption oracle
- [ ] Bypassing access controls via email address parsing discrepancies

## HTTP Host Header Attacks (7 labs)

- [ ] Basic password reset poisoning
- [ ] Host header authentication bypass
- [ ] Web cache poisoning via ambiguous requests
- [ ] Routing-based SSRF
- [ ] SSRF via flawed request parsing
- [ ] Host validation bypass via connection state attack
- [ ] Password reset poisoning via dangling markup

## OAuth Authentication (6 labs)

- [ ] Authentication bypass via OAuth implicit flow
- [ ] SSRF via OpenID dynamic client registration
- [ ] Forced OAuth profile linking
- [ ] OAuth account hijacking via redirect_uri
- [ ] Stealing OAuth access tokens via an open redirect
- [ ] Stealing OAuth access tokens via a proxy page

## File Upload Vulnerabilities (7 labs)

- [ ] Remote code execution via web shell upload
- [ ] Web shell upload via Content-Type restriction bypass
- [ ] Web shell upload via path traversal
- [ ] Web shell upload via extension blacklist bypass
- [ ] Web shell upload via obfuscated file extension
- [ ] Remote code execution via polyglot web shell upload
- [ ] Web shell upload via race condition

## JWT (8 labs)

- [ ] JWT authentication bypass via unverified signature
- [ ] JWT authentication bypass via flawed signature verification
- [ ] JWT authentication bypass via weak signing key
- [ ] JWT authentication bypass via jwk header injection
- [ ] JWT authentication bypass via jku header injection
- [ ] JWT authentication bypass via kid header path traversal
- [ ] JWT authentication bypass via algorithm confusion
- [ ] JWT authentication bypass via algorithm confusion with no exposed key

## Essential Skills (2 labs)

- [ ] Discovering vulnerabilities quickly with targeted scanning
- [ ] Scanning non-standard data structures

## Prototype Pollution (10 labs)

- [ ] Client-side prototype pollution via browser APIs
- [ ] DOM XSS via client-side prototype pollution
- [ ] DOM XSS via an alternative prototype pollution vector
- [ ] Client-side prototype pollution via flawed sanitization
- [ ] Client-side prototype pollution in third-party libraries
- [ ] Privilege escalation via server-side prototype pollution
- [ ] Detecting server-side prototype pollution without polluted property reflection
- [ ] Bypassing flawed input filters for server-side prototype pollution
- [ ] Remote code execution via server-side prototype pollution
- [ ] Exfiltrating sensitive data via server-side prototype pollution

## GraphQL API Vulnerabilities (5 labs)

- [ ] Accessing private GraphQL posts
- [ ] Accidental exposure of private GraphQL fields
- [ ] Finding a hidden GraphQL endpoint
- [ ] Bypassing GraphQL brute force protections
- [ ] Performing CSRF exploits over GraphQL

## Race Conditions (6 labs)

- [ ] Limit overrun race conditions
- [ ] Bypassing rate limits via race conditions
- [ ] Multi-endpoint race conditions
- [ ] Single-endpoint race conditions
- [ ] Exploiting time-sensitive vulnerabilities
- [ ] Partial construction race conditions

## NoSQL Injection (4 labs)

- [ ] Detecting NoSQL injection
- [ ] Exploiting NoSQL operator injection to bypass authentication
- [ ] Exploiting NoSQL injection to extract data
- [ ] Exploiting NoSQL operator injection to extract unknown fields

## API Testing (5 labs)

- [ ] Exploiting an API endpoint using documentation
- [ ] Exploiting server-side parameter pollution in a query string
- [ ] Finding and exploiting an unused API endpoint
- [ ] Exploiting a mass assignment vulnerability
- [ ] Exploiting server-side parameter pollution in a REST URL

## Web LLM Attacks (8 labs)

- [ ] Exploiting LLM APIs with excessive agency
- [ ] Exploiting vulnerabilities in LLM APIs
- [ ] Indirect prompt injection
- [ ] Exploiting insecure output handling in LLM APIs
- [ ] Exploiting AI agents to perform destructive actions
- [ ] Exploiting AI agents to exfiltrate sensitive information
- [ ] Exploiting AI agents to trigger secondary vulnerabilities
- [ ] Bypassing AI scanner defenses to exfiltrate sensitive information

## Web Cache Deception (5 labs)

- [ ] Exploiting path mapping for web cache deception
- [ ] Exploiting path delimiters for web cache deception
- [ ] Exploiting origin server normalization for web cache deception
- [ ] Exploiting cache server normalization for web cache deception
- [ ] Exploiting exact-match cache rules for web cache deception

---

Last updated: August 2026
