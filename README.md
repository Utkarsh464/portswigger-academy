# PortSwigger Web Security Academy — Writeups

![Burp Suite](https://img.shields.io/badge/Burp_Suite-FF6633?style=for-the-badge&logo=burpsuite&logoColor=white)
![Kali Linux](https://img.shields.io/badge/Kali_Linux-557C94?style=for-the-badge&logo=kali-linux&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)

Personal, step-by-step writeups from my [PortSwigger Web Security
Academy](https://portswigger.net/web-security) labs. Each one walks through how
to find a vulnerability, how to exploit it, and — most importantly — how to fix
it.

---

## Progress

| Category | Labs Solved | Status |
|---|---|---|
| Access Control | 12 / 13 | In progress |
| Path Traversal | 2 / 6 | In progress |
| Cross-Site Scripting (XSS) | 2 / 30 | In progress |
| SSRF | 2 / 7 | In progress |
| SQL Injection | 2 / 18 | In progress |

```
███░░░░░░░░░░░░░░░░░  20 / ~250  (8%)
```

---

## Writeups

```
portswigger-academy/
├── Access Control/                         12 / 13
│   ├── 01 - Unprotected Admin Functionality/
│   ├── 02 - Unprotected Admin Functionality With Unpredictable URL/
│   ├── 03 - User Role Controlled By Request Parameter/
│   ├── 04 - User ID Controlled By Request Parameter/
│   ├── 05 - User ID Controlled By Request Parameter With Data Leakage In Redirect/
│   ├── 06 - User ID Controlled By Request Parameter With Password Disclosure/
│   ├── 07 - Insecure Direct Object References/
│   ├── 08 - User Role Can Be Modified In User Profile/
│   ├── 09 - User ID Controlled By Request Parameter With Unpredictable User IDs/
│   ├── 10 - URL-Based Access Control Can Be Circumvented/
│   ├── 11 - Method-Based Access Control Can Be Circumvented/
│   └── 12 - Multi-Step Process With No Access Control On One Step/
├── Path Traversal/                           # 2 / 6
│   ├── 01 - File Path Traversal - Simple Case/
│   └── 02 - File Path Traversal - Traversal Sequences Blocked with Absolute Path Bypass/
├── Cross-Site Scripting (XSS)/               # 2 / 30
│   ├── 01 - Reflected XSS into HTML context with nothing encoded/
│   └── 02 - Stored XSS into HTML context with nothing encoded/
├── SSRF/                                     # 2 / 7
│   ├── 01 - Basic SSRF against the local server/
│   └── 02 - Basic SSRF against another back-end system/
└── SQL Injection/                            # 2 / 18
    ├── 01 - SQL injection vulnerability in WHERE clause allowing retrieval of hidden data/
    └── 02 - SQL injection vulnerability allowing login bypass/
```

Writeups with a `images/` folder include screenshots taken while solving the
lab. See `ROADMAP.md` for the full tracked list and remaining labs.

---

## How Each Writeup Is Structured

Every lab writeup follows the same format:

- **Title** — Lab name and difficulty
- **Category** — Which category it falls under
- **Lab Objective** — What PortSwigger asks you to do
- **Skills Learned** — What I took away from it
- **Recon** — What I checked before exploiting
- **Finding the Vulnerability** — How I identified the weak point
- **Exploitation Steps** — Step-by-step walkthrough
- **Payload(s)** — The actual payloads used
- **Why It Works** — Technical explanation
- **Root Cause** — Why the developer made it vulnerable
- **Impact** — What an attacker could really do with this
- **Mitigation** — How to fix it
- **Key Takeaways** — Notes for future testing
- **References** — Links to docs and further reading

---

## What's Next

Working through the remaining labs in order. Next up:

- More Access Control labs (horizontal privilege escalation)
- More SQL Injection labs
- More Path Traversal labs
- Cross-Site Scripting (XSS)
- CSRF
- XXE

---

## Disclaimer

> These writeups are for educational purposes only. I solved these labs on
> PortSwigger's hosted platform. Do not test vulnerabilities on systems you
> don't own or have permission to test.

---

## Badges

![GitHub last commit](https://img.shields.io/github/last-commit/Utkarsh464/portswigger-academy)
![GitHub repo size](https://img.shields.io/github/repo-size/Utkarsh464/portswigger-academy)
![GitHub](https://img.shields.io/github/license/Utkarsh464/portswigger-academy)

Let me know if you spot a mistake. I'm learning too.