# User ID Controlled By Request Parameter

| Field | Value |
|---|---|
| **Difficulty** | Apprentice |
| **Category** | Access Control |
| **Lab URL** | `https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter` |

---

## Lab Objective

Access another user's account details (API key) by manipulating the `id` parameter.

---

## Skills Learned

- Horizontal privilege escalation via user ID parameter
- Accessing other users' data by changing a numeric or string ID
- The difference between vertical and horizontal access control

---

## Recon

Logged in as `wiener:peter`. The account page shows:

```
/accountDetails?id=wiener
```

The `id` parameter matches my username. I wondered what happens if I change it.

---

## Finding the Vulnerability

The application uses the `id` parameter directly from the URL to fetch account details. There's no check that the authenticated user owns the requested ID.

I changed `id=wiener` to `id=carlos` and the page returned Carlos's account details — including their API key.

---

## Exploitation Steps

1. Logged in as `wiener:peter`.
2. Opened Burp and captured the `/accountDetails` request.
3. Changed the `id` parameter from `wiener` to `carlos`.
4. Sent the request.
5. The response contained Carlos's API key.
6. Submitted the API key to solve the lab.

---

## Payload

```
GET /accountDetails?id=carlos
```

Just a different username in the `id` parameter.

---

## Why It Works

The server authenticates the user via session cookie but doesn't verify that the requested resource belongs to that user. The `id` parameter is used directly in a database query or API call without any ownership check.

This is a classic insecure direct object reference (IDOR) pattern, specifically horizontal privilege escalation.

---

## Root Cause

The developer checked "is this user logged in?" but never checked "does this user own the requested resource?" The `id` parameter is user-controllable and the server trusts it.

---

## Impact

Any authenticated user can view any other user's private data:

- API keys
- Personal information
- Email addresses
- Phone numbers
- Payment details (in real applications)

---

## Mitigation

- For every request that accesses a resource by ID, verify the authenticated user has permission to access that resource
- Use a server-side mapping of user → owned resources instead of accepting user IDs from the client
- Consider using UUIDs instead of sequential or predictable IDs (mitigation, not a fix)
- Implement proper authorization checks in the backend, not just authentication

---

## Key Takeaways

- Always check if you can access other users' data by changing IDs
- Don't assume the server validates ownership
- This is one of the most common vulnerabilities in web applications
- The fix is always a server-side authorization check, not "hide the ID"

---

## Related Labs

- [05 - User ID Controlled By Request Parameter With Data Leakage In Redirect](../05%20-%20User%20ID%20Controlled%20By%20Request%20Parameter%20With%20Data%20Leakage%20In%20Redirect/README.md) — same `id`-parameter tampering, data leaked through a redirect
- [06 - User ID Controlled By Request Parameter With Password Disclosure](../06%20-%20User%20ID%20Controlled%20By%20Request%20Parameter%20With%20Password%20Disclosure/README.md) — same `id`-parameter tampering exposing user account data
- [09 - User ID Controlled By Request Parameter With Unpredictable User IDs](../09%20-%20User%20ID%20Controlled%20By%20Request%20Parameter%20With%20Unpredictable%20User%20IDs/README.md) — same `id`-parameter escalation, but IDs are hard to predict

---

## References

- [PortSwigger: Access control (IDOR)](https://portswigger.net/web-security/access-control/idor)
- [OWASP: Insecure Direct Object Reference Prevention](https://cheatsheetseries.owasp.org/cheatsheets/Insecure_Direct_Object_Reference_Prevention_Cheat_Sheet.html)
