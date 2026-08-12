# User Role Controlled By Request Parameter

| Field | Value |
|---|---|
| **Difficulty** | Apprentice |
| **Category** | Access Control |
| **Lab URL** | `https://portswigger.net/web-security/access-control/lab-user-role-controlled-by-request-parameter` |

---

## Lab Objective

Access the admin panel and delete user `carlos` by manipulating your role.

---

## Skills Learned

- How applications sometimes store roles in cookies
- Modifying client-side parameters to escalate privileges
- Why you should never trust the client for authorization

---

## Recon

Logged into the lab with the provided credentials (`wiener:peter`). Checked my cookies in Burp.

Found this cookie:

```
Admin=false
```

That's interesting. The application stores my admin status in a cookie that I can modify.

---

## Finding the Vulnerability

The server reads the `Admin` cookie to decide if the user is an administrator. There's no server-side session data checking the actual role — it just trusts whatever the cookie says.

I changed `Admin=false` to `Admin=true` and refreshed the page. The admin panel link appeared.

---

## Exploitation Steps

1. Logged in as `wiener:peter`.
2. Opened Burp, found the cookie `Admin=false`.
3. Changed it to `Admin=true` in the request.
4. Reloaded the page.
5. Admin panel was now accessible.
6. Navigated to the admin panel and deleted `carlos`.

---

## Payload

Modified cookie:

```
Cookie: session=abc123; Admin=true
```

Just flipping `false` to `true`.

---

## Why It Works

The application never validates the `Admin` cookie against server-side data. It reads the cookie and makes authorization decisions based on its value. Since cookies are stored client-side and sent with every request, the attacker has full control over them.

This is a classic case of trusting the client with authorization logic.

---

## Root Cause

The developer used a client-side cookie to determine admin status. They should have stored the role in a server-side session and checked that on every request.

---

## Impact

Any user can escalate to admin by modifying a single cookie value. This gives full access to all admin functionality, including user management, content modification, and data access.

---

## Mitigation

- Never store authorization data in client-accessible storage (cookies, local storage)
- Use server-side sessions to track user roles
- Validate authorization on every request against a trusted backend store (database, session store)
- Sign or encrypt cookies if you must store data client-side

---

## Key Takeaways

- Always inspect cookies during testing
- Look for boolean or role-based cookies
- If you see `admin=0`, `role=user`, `isAdmin=false` — test what happens when you change them
- Client-side controls are not security controls

---

## Related Labs

- [08 - User Role Can Be Modified In User Profile](../08%20-%20User%20Role%20Can%20Be%20Modified%20In%20User%20Profile/README.md) — in both, the user's role is trusted from client-controlled input

---

## References

- [PortSwigger: Access control](https://portswigger.net/web-security/access-control)
- [OWASP: Testing for Cookies attributes](https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/06-Session_Management_Testing/02-Testing_for_Cookies_Attributes)
