# User ID Controlled By Request Parameter With Data Leakage In Redirect

| Field | Value |
|---|---|
| **Difficulty** | Apprentice |
| **Category** | Access Control |
| **Lab URL** | `https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter-with-data-leakage-in-redirect` |

---

## Lab Objective

Access Carlos's account details and obtain his API key.

---

## Skills Learned

- Data leakage before redirect
- Using Burp to capture responses that the browser never shows
- The difference between front-end and back-end authorization

---

## Recon

Same setup as Lab 04. Logged in as `wiener:peter`. Account page at:

```
/accountDetails?id=wiener
```

I changed `id=wiener` to `id=carlos` in the browser URL bar. The page redirected to `/login` with a message about not being logged in.

That's odd — I am logged in. Something's different here.

---

## Finding the Vulnerability

The server returns a redirect when you try to access another user's account, but the response body still contains the data before the redirect happens.

In the browser, you just see the redirect. In Burp, you see the full response including Carlos's account details, then the redirect instruction.

---

## Exploitation Steps

1. Logged in as `wiener:peter`.
2. Opened Burp and turned intercept on.
3. Sent a request to `/accountDetails?id=carlos`.
4. Forwarded the request.
5. The response was a 302 redirect to `/login`.
6. But the response body contained Carlos's account HTML with the API key.
7. Copied the API key from the response body.
8. Submitted it to solve the lab.

---

## Payload

```
GET /accountDetails?id=carlos
```

Same as Lab 04, but the exploit vector is different.

---

## Why It Works

The server fetches the account data for the requested ID before checking authorization. When it detects that the user shouldn't have access, it sends a redirect. But by that point, the data is already in the response body.

The redirect header tells the browser to navigate away, but Burp shows the full response. The damage is done before the security check runs.

Bad ordering: access data first, check permissions second.

---

## Root Cause

The code path was:

1. Query database for `id=carlos`
2. Build response with data
3. Check if session user owns this ID
4. If not, return redirect

Steps 1-2 should happen after step 3. The data should never be fetched if the user isn't authorized.

---

## Impact

Same as Lab 04 — any authenticated user can access any other user's private data. The redirect gives a false sense of security, but the data is already leaked.

---

## Mitigation

- Check authorization before fetching or processing data
- Return a 401/403 immediately if the user isn't authorized — don't build a response first
- Never include sensitive data in a response that will be redirected

---

## Key Takeaways

- A redirect doesn't mean the data wasn't sent
- Always check response bodies in Burp, even for 302 responses
- The order of operations in code matters for security
- Front-end behavior (redirect) ≠ back-end reality (data sent)

---

## Related Labs

- [04 - User ID Controlled By Request Parameter](../04%20-%20User%20ID%20Controlled%20By%20Request%20Parameter/README.md) — same tampered `id` parameter; the result leaks via the redirect
- [06 - User ID Controlled By Request Parameter With Password Disclosure](../06%20-%20User%20ID%20Controlled%20By%20Request%20Parameter%20With%20Password%20Disclosure/README.md) — same horizontal escalation exposing user data

---

## References

- [PortSwigger: Access control](https://portswigger.net/web-security/access-control)
- [CWE-200: Exposure of Sensitive Information](https://cwe.mitre.org/data/definitions/200.html)
