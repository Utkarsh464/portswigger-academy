# DOM XSS in innerHTML sink using source location.search

| Field          | Value                                                                                    |
| -------------- | ---------------------------------------------------------------------------------------- |
| **Difficulty** | Apprentice                                                                               |
| **Category**   | Cross-Site Scripting (XSS)                                                               |
| **Lab URL**    | `https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-innerhtml-sink` |

---

## Lab Objective

Perform a cross-site scripting attack that calls the `alert` function.

---

## Skills Learned

- Recognizing `innerHTML` as a dangerous DOM XSS sink
- Tracing data from `location.search` to a client-side sink
- Understanding why `<script>` and `<svg onload>` don't fire through `innerHTML`
- Triggering JavaScript with an `<img>` `onerror` handler

---

## Recon

The lab is a blog with a search feature. When you search for something, the term is reflected back on the results page — but not by the server. It's done entirely in client-side JavaScript.

I searched for `test123` and opened DevTools. Searching the DOM for `test123` showed my input placed inside a `<span>` (the `searchMessage` element). That told me the search term was being written into the page by JavaScript rather than returned in the HTTP response — a classic DOM XSS setup.

---

## Finding the Vulnerability

Searching the page's JavaScript with DevTools (`Control+Shift+F`) revealed the vulnerable code:

```javascript
function doSearchQuery(query) {
  document.getElementById("searchMessage").innerHTML = query;
}

var query = new URLSearchParams(window.location.search).get("search");
if (query) {
  doSearchQuery(query);
}
```

The `search` parameter comes from `location.search` (fully attacker-controlled via the URL) and is passed straight into `innerHTML` with no encoding or sanitization. Because `innerHTML` parses its argument as HTML, any tags I supply become real DOM nodes.

This is DOM-based XSS: the server never sees the payload, so server-side output encoding can't stop it. The browser builds the malicious DOM itself from the URL.

---

## Exploitation Steps

1. Opened the lab
2. Searched for `test123` and inspected the DOM to confirm my input landed inside the `searchMessage` element
3. Found the `innerHTML` sink and the `location.search` source in the page's JavaScript
4. Entered `<img src=1 onerror=alert(1)>` in the search box
5. Clicked "Search"
6. The broken `src` threw an error, `onerror` fired, `alert(1)` popped, and the lab was solved

---

## Payload

```
<img src=1 onerror=alert(1)>
```

The `src=1` is not a valid image, so the browser raises an error while loading it. The `onerror` event handler then executes `alert(1)`.

---

## Why It Works

`innerHTML` is a sink — whatever string is assigned to it is parsed as HTML by the browser. Here the app assigns my URL-controlled `search` value directly to `innerHTML`, so my tags become live DOM nodes.

One important detail: `innerHTML` does **not** execute `<script>` tags, and `svg onload` events don't fire in modern browsers when inserted via `innerHTML`. That's why a plain `<script>alert(1)</script>` fails. The fix is to use an element that runs JavaScript through an event handler triggered by an error condition — `<img src=1 onerror=alert(1)>` does exactly that: the invalid `src` forces the `onerror` handler to run.

Because the injection happens entirely client-side, server-side filters and encoding are irrelevant.

---

## Root Cause

Using `innerHTML` with attacker-controlled input taken from `location.search`, with no encoding or sanitization. The developer wanted to echo the search term back to the user but fed untrusted URL data straight into a dynamic-HTML sink.

---

## Impact

An attacker can run arbitrary JavaScript in the victim's browser:

- **Session hijacking** — steal cookies and tokens
- **Phishing** — inject fake login forms
- **Keylogging** — capture keystrokes
- **Redirect** — send the victim to a malicious site

The attack only needs the victim to open a crafted URL, which makes it easy to weaponize (email, message, shortened link).

---

## Mitigation

- Avoid `innerHTML` with untrusted input; use `textContent` to insert user data as text
- If dynamic HTML is required, sanitize with a vetted library (e.g. DOMPurify) before assignment
- Keep data out of sinks: read user input with `textContent` / `setAttribute` rather than string assignment
- Deploy a Content Security Policy (CSP) that blocks inline event handlers like `onerror`

---

## Key Takeaways

- `innerHTML` is a DOM XSS sink just like `document.write` — treat `location.*` → `innerHTML` as dangerous
- `<script>` and `<svg onload>` won't fire through `innerHTML`; reach for `<img onerror>` instead
- The vulnerability is in client-side code, so server-side hardening alone won't fix it
- Always trace sources (`location.search`, `location.hash`) to sinks (`innerHTML`, `document.write`, `eval`) in DevTools

---

## Related Labs

- [03 - DOM XSS in document.write sink using source location.search](../03%20-%20DOM%20XSS%20in%20document.write%20sink%20using%20source%20location.search/README.md) — same source, different sink (`document.write`)
- [04 - DOM XSS in document.write sink using source location.search inside a select element](../04%20-%20DOM%20XSS%20in%20document.write%20sink%20using%20source%20location.search%20inside%20a%20select%20element/README.md) — `document.write` inside a `<select>` element
- [01 - Reflected XSS into HTML context with nothing encoded](../01%20-%20Reflected%20XSS%20into%20HTML%20context%20with%20nothing%20encoded/README.md) — same unencoded context but server-side reflection

---

## References

- [PortSwigger: DOM-based XSS](https://portswigger.net/web-security/cross-site-scripting/dom-based)
- [PortSwigger: Cross-site scripting (XSS)](https://portswigger.net/web-security/cross-site-scripting)
- [OWASP: DOM based XSS](https://owasp.org/www-community/attacks/xss/#dom-based-xss)
