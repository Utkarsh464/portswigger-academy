# User ID Controlled By Request Parameter With Password Disclosure

| Field | Value |
|---|---|
| **Difficulty** | Apprentice |
| **Category** | Access Control |
| **Lab URL** | `https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter-with-password-disclosure` |

---

## Lab Objective

Access Carlos's account using his credentials, then delete his account from the admin panel.

---

## Skills Learned

- Extracting credentials from account pages
- Chaining vulnerabilities (IDOR + admin access)
- Finding hidden fields in HTML responses

---

## Recon

Logged in as `wiener:peter`. Account page at:

```
/myaccount?id=wiener
```

Checked the HTML source. Found a password field:

```html
<input type="password" name="password" value="peter" disabled>
```

The password is in a disabled input field in the HTML. Disabled means the user can't edit it, but it's still there in the source code.

---

## Finding the Vulnerability

Two issues:

1. The server returns the password in the HTML for any user if you change the `id` parameter
2. The password is in cleartext

I changed `id=wiener` to `id=carlos` and found his password in the HTML source.

---

## Exploitation Steps

1. Logged in as `wiener:peter`.
2. Sent a request to `/myaccount?id=carlos`.
3. Viewed the response in Burp.
4. Found Carlos's password in the HTML: `<input type="password" value="..." disabled>`.
5. Logged out of `wiener`.
6. Logged in as `carlos` with the extracted password.
7. Navigated to the admin panel (which was unprotected in this lab).
8. Deleted `carlos`'s account.
9. Lab solved.

---

## Payload

No payload. Just parameter manipulation:

```
GET /myaccount?id=carlos
```

Then login with the extracted credentials.

---

## Why It Works

The account page loads the user's data based on the `id` parameter without checking ownership. The password is rendered in the HTML as a disabled input field. Disabled fields aren't submitted with forms, but they're still fully visible in the page source.

The password is stored in plaintext (or reversibly encrypted), which is a separate but related issue.

---

## Root Cause

1. No authorization check on the account details endpoint
2. Password stored in plaintext and rendered in HTML
3. Using a disabled input field instead of not exposing the password at all

---

## Impact

An attacker can:

- Steal any user's password
- Take over accounts
- Use the compromised account to access admin functionality (if admin panel is also unprotected)

---

## Mitigation

- Never return passwords in HTML, even in disabled fields
- Hash passwords — never store or transmit them in plaintext
- Verify authorization before serving account data
- Use server-side sessions to track the current user instead of trusting URL parameters

---

## Key Takeaways

- Disabled form fields are not hidden — they're in the HTML source
- Always view page source, not just the rendered page
- One vulnerability can chain into another (IDOR → credential theft → admin access)
- Storing passwords in a way that allows them to be rendered as plaintext is a red flag

---

## References

- [PortSwigger: Access control](https://portswigger.net/web-security/access-control)
- [OWASP: Password in HTML Source Code](https://owasp.org/www-community/vulnerabilities/Password_in_HTML_Source_Code)
