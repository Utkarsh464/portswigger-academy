# Unprotected Admin Functionality With Unpredictable URL

| Field | Value |
|---|---|
| **Difficulty** | Apprentice |
| **Category** | Access Control |
| **Lab URL** | `https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality-with-unpredictable-url` |

---

## Lab Objective

Access the admin panel at a randomized URL and delete user `carlos`.

---

## Skills Learned

- Finding hidden URLs in JavaScript source
- Exposing admin paths leaked in client-side code
- Same vulnerability, different hiding method

---

## Recon

Same shop as before, but this time `robots.txt` doesn't help. No obvious admin paths.

I opened the page source (Ctrl+U). Looked through the HTML. Then I checked the JavaScript files.

Found this in the main page's JS:

```javascript
var adminPanel = document.getElementById('admin-panel');
if (adminPanel) {
    adminPanel.href = '/admin-j6s2d8a4';
}
```

The admin path is generated randomly per lab instance and stored in a JavaScript variable.

---

## Finding the Vulnerability

The admin panel URL changes every time the lab resets, but it's always embedded in the JavaScript on the homepage. The server doesn't check who accesses it — the randomization is the only protection.

---

## Exploitation Steps

1. Loaded the lab homepage.
2. Viewed the page source.
3. Searched for `admin` in the source code.
4. Found the JavaScript that sets the admin panel link.
5. Noted the path: `/admin-j6s2d8a4`.
6. Navigated there.
7. Deleted user `carlos`.

---

## Payload

No payload. Found URL in page source:

```
GET /admin-j6s2d8a4
```

Then the delete link from the admin panel.

---

## Why It Works

Randomizing the URL is better than a fixed path, but it's still not access control. The admin path has to be accessible to administrators, and if it's exposed in client-side code, anyone can find it.

The core issue is the same as Lab 01: the admin panel doesn't verify the user's role. The URL being random just adds a tiny speed bump.

---

## Root Cause

The developer added URL randomization thinking it would protect the admin panel. They forgot (or didn't know) that the URL needs to be shared with legitimate admins, and putting it in JavaScript means anyone can find it.

No session validation on the admin panel endpoints.

---

## Impact

Same as Lab 01. Any attacker who inspects the page source can find the admin URL and perform privileged actions.

---

## Mitigation

- Random URLs are better than nothing but not sufficient
- Every admin endpoint must enforce authentication and authorization
- Don't put sensitive URLs in client-side code
- Use proper session management with role-based access control

---

## Key Takeaways

- Always view page source and JS files
- Search for keywords like `admin`, `panel`, `dashboard`, `hidden`, `config`
- JavaScript files leak all kinds of things
- Random URLs are not a replacement for access control

---

## Screenshots

> I'd capture:
>
> 1. The JavaScript code showing the admin URL
> 2. The admin panel after navigating to the discovered path
> 3. The delete request in Burp

---

## References

- [PortSwigger: Access control](https://portswigger.net/web-security/access-control)
- [OWASP: Client-side URL manipulation](https://owasp.org/www-community/attacks/Client-side_URL_manipulation)
