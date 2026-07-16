# File Path Traversal — Simple Case

| Field | Value |
|---|---|
| **Difficulty** | Apprentice |
| **Category** | Path Traversal |
| **Lab URL** | `https://portswigger.net/web-security/file-path-traversal/lab-simple` |

---

## Lab Objective

Read the contents of `/etc/passwd` from the server's filesystem.

---

## Skills Learned

- Identifying unsanitized file paths in URL parameters
- Using `../` to escape the web root
- Reading arbitrary server files when no filtering is in place

---

## Recon

The lab is a shop website. Product images load through a URL parameter.

Look at how the page loads images:

```
GET /image?filename=23.jpg
```

That `filename` parameter is interesting. If the server is reading files based on this input, maybe I can point it somewhere else.

---

## Finding the Vulnerability

I checked what happens when I change the filename value. The server returned images from what looked like a fixed directory. The question was: does it sanitize `../` sequences?

Tested with:

```
GET /image?filename=../23.jpg
```

If it blocks traversal, I'd get an error. If it doesn't, I might be able to walk up the directory tree.

No error on `../` — that was the green light.

---

## Exploitation Steps

1. Opened the lab in Burp's browser.
2. Found the image request in Proxy history.
3. Sent it to Repeater.
4. Replaced `23.jpg` with `../../../etc/passwd`.
5. Sent the request.
6. The response body contained `/etc/passwd` contents.

---

## Payload

```
../../../etc/passwd
```

This walks up three directories from the web root to reach the system root, then reads `/etc/passwd`.

How many `../` you need depends on where the web server stores images. Three levels usually works for standard Linux setups (`/var/www/html/images/` → `/`). If not, just add more.

---

## Why It Works

The application takes user input and passes it directly to a file-reading function like `file_get_contents()` in PHP or `File.ReadAllBytes()` in C#. No validation. No sanitization. The `../` sequences resolve on the filesystem, so the server reads whatever file I point it at.

The server never checks that the resolved path stays inside the intended directory.

---

## Root Cause

The developer trusted user input. They assumed the `filename` parameter would only ever contain legitimate image filenames. No input validation, no path normalization, no whitelist of allowed files.

---

## Impact

An attacker can read any file on the server:

- `/etc/passwd` — user accounts
- `/etc/shadow` — password hashes (if permissions allow)
- Source code files — to find more vulnerabilities
- Configuration files — database credentials, API keys
- Private keys — `/home/user/.ssh/id_rsa`

In some cases, path traversal can lead to RCE if the attacker can write files (like uploading a webshell) and then include them via traversal.

---

## Mitigation

- Use a whitelist of allowed filenames instead of accepting arbitrary input
- If dynamic filenames are required, validate that the resolved path is inside the intended directory
- `basename()` the input to strip directory components
- Use a database ID map (e.g., `image?id=5` → server looks up filename internally)
- Avoid passing user input to filesystem functions entirely

---

## Key Takeaways

- Always test URL parameters that reference files
- `../` traversal is the first thing to try
- If one level doesn't work, try more
- Check error messages for path disclosure — they tell you how deep you need to go

---

## References

- [PortSwigger: File path traversal](https://portswigger.net/web-security/file-path-traversal)
- [OWASP: Path Traversal](https://owasp.org/www-community/attacks/Path_Traversal)
