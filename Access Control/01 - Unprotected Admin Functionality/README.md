# Unprotected Admin Functionality

| Field | Value |
|---|---|
| **Difficulty** | Apprentice |
| **Category** | Access Control |
| **Lab URL** | `https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality` |

---

## Lab Objective

Access the admin panel and delete user `carlos`.

---

## Skills Learned

- Checking for common admin paths
- Identifying missing access controls on admin interfaces
- The importance of directory discovery

---

## Recon

I loaded the lab in Burp's browser and looked around. Standard shop frontend. Nothing special.

Checked `/robots.txt` just in case. It revealed:

```
Disallow: /administrator-panel
```

That's the admin path, exposed in robots.txt. Rookie mistake.

---

## Finding the Vulnerability

The admin panel exists at `/administrator-panel` but there's no authentication check. Anyone who knows the URL can access it.

I found it two ways:

1. `robots.txt` straight up told me
2. I could have brute-forced common paths too

---

## Exploitation Steps

1. Opened the lab in Burp's browser.
2. Navigated to `/administrator-panel`.
3. The admin panel loaded with a list of users and a "Delete" button next to `carlos`.
4. Clicked "Delete".
5. Lab solved.

---

## Payload

No payload needed. Just a URL:

```
GET /administrator-panel
```

Then:

```
GET /administrator-panel/delete?username=carlos
```

---

## Why It Works

The server doesn't check the user's role or authentication status when serving the admin panel. The admin functionality is hidden behind an obscure path, but there's no actual access control enforcing who can use it.

Robots.txt isn't a security control — it's a hint for search engines. Developers sometimes hide paths there and think that's enough.

---

## Root Cause

The developer relied on security by obscurity. They put the admin panel at a non-obvious path but never implemented authentication or authorization checks on it.

---

## Impact

Any unauthenticated user can:

- Access administrative functions
- Delete users
- Modify site content
- Access sensitive data behind the admin panel

---

## Mitigation

- Every admin endpoint must check the user's session and role before processing requests
- Don't rely on obscurity or robots.txt for security
- Implement proper authentication middleware on sensitive routes

---

## Key Takeaways

- Always check `robots.txt` during recon
- Directory brute-forcing can find hidden admin panels
- Obscurity is not a security measure
- Check access controls even when you find endpoints — sometimes they exist but are misconfigured

---

## References

- [PortSwigger: Access control](https://portswigger.net/web-security/access-control)
- [OWASP: Testing for Admin Interfaces](https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/05-Authorization_Testing/03-Testing_for_Privilege_Escalation)
