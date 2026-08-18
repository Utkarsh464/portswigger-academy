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

---

## Recon

The lab is a product search page. When you search for something, the query gets tracked using JavaScript on the page — your search string is written into the DOM using `document.write`.

I searched for `test123` and inspected the page source. The string appeared inside an `<img>` tag's `src` attribute, meaning the application takes my input from the URL and drops it directly into an HTML attribute without any encoding.

![Search tracking string placed inside img attribute](images/01-search-tracking-string-in-page.png)

---

## Finding the Vulnerability

The vulnerable code path looks something like this:

```javascript
var search = document.location.search;
document.write(
  '<img src="/resources/images/tracking.gif?search=' + search + '">',
);
```

Since `location.search` is fully attacker-controlled and `document.write` outputs raw HTML, I can break out of the `img` attribute and inject my own tags. The key difference from reflected XSS: this happens entirely client-side. The server never sees the payload — the browser processes it.

---

## Exploitation Steps

1. Opened the lab
2. Searched for `test123` and inspected the page source to see where my input landed
3. Saw my string inside `<img src="...search=test123">`
4. Constructed a payload that closes the attribute and injects an SVG: `"><svg onload=alert(1)>`
5. Entered the payload in the search box
6. Lab solved

---

## Payload

```
"><svg onload=alert(1)>
```

This closes the `src` attribute with `"`, closes the `img` tag with `>`, then injects an `<svg>` element with an `onload` handler that fires `alert(1)`.
