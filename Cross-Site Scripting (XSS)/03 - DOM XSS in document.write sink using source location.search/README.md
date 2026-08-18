# DOM XSS in document.write sink using source location.search

| Field          | Value                                                                                         |
| -------------- | --------------------------------------------------------------------------------------------- |
| **Difficulty** | Apprentice                                                                                    |
| **Category**   | Cross-Site Scripting (XSS)                                                                    |
| **Lab URL**    | `https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink` |

---

## Lab Objective

Perform a cross-site scripting attack that calls the `alert` function.

---

## Skills Learned

- Understanding DOM-based XSS vs reflected/stored XSS
- Identifying `document.write` as a dangerous sink
- Tracing data flow from `location.search` to the DOM
- Breaking out of HTML attribute context
