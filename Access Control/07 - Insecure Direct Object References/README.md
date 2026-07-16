# Insecure Direct Object References

| Field | Value |
|---|---|
| **Difficulty** | Apprentice |
| **Category** | Access Control |
| **Lab URL** | `https://portswigger.net/web-security/access-control/lab-insecure-direct-object-references` |

---

## Lab Objective

Access another user's invoice document by exploiting an insecure direct object reference.

---

## Skills Learned

- Identifying direct object references in file downloads
- Manipulating numeric IDs to access unauthorized resources
- Real-world IDOR in document retrieval

---

## Recon

Logged in as `wiener:peter`. The account page had a link to download an invoice:

```
/invoice?id=1.txt
```

Clicking it downloaded `invoice_1.txt` containing my order details.

The `id` parameter is a simple number. Predictable. Sequential.

---

## Finding the Vulnerability

The server uses the `id` parameter to look up which invoice file to return. There's no check that the invoice belongs to the currently authenticated user.

I changed `id=1` to `id=2` and got someone else's invoice.

---

## Exploitation Steps

1. Logged in as `wiener:peter`.
2. Found the invoice download link.
3. Sent the request to Burp Repeater.
4. Changed `id=1` to `id=2`.
5. Sent the request.
6. Received another user's invoice with their credit card details.
7. Submitted the card number to solve the lab.

---

## Payload

```
GET /invoice?id=2
```

Just incrementing the numeric ID.

---

## Why It Works

The invoice ID is directly tied to a filesystem path or database query. The server fetches whatever file corresponds to the `id` parameter without checking if the current user owns that invoice.

The IDs are sequential integers, making them trivially guessable. Even if they were random, the real issue is the lack of authorization.

---

## Root Cause

No authorization check on the invoice download endpoint. The `id` parameter is user-controllable, and the server trusts it to determine which document to serve.

---

## Impact

Any authenticated user can:

- Access any other user's invoices
- View credit card numbers and personal details
- Harvest sensitive financial information

---

## Mitigation

- Verify that the authenticated user owns the requested invoice before serving it
- Use a server-side mapping (user → invoice IDs) instead of accepting arbitrary IDs
- Consider using non-sequential, unpredictable identifiers in addition to authorization checks
- Never include sensitive financial data in downloadable documents without additional protection

---

## Key Takeaways

- File downloads with sequential IDs are a classic IDOR target
- Always check if you can access other users' documents by changing IDs
- This vulnerability is incredibly common in real applications
- Authorization must be checked on every endpoint, not just pages

---

## References

- [PortSwigger: IDOR](https://portswigger.net/web-security/access-control/idor)
- [OWASP: Insecure Direct Object Reference Prevention](https://cheatsheetseries.owasp.org/cheatsheets/Insecure_Direct_Object_Reference_Prevention_Cheat_Sheet.html)
