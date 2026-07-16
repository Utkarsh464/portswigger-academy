# PortSwigger Web Security Academy — My Writeups

![Burp Suite](https://img.shields.io/badge/Burp_Suite-FF6633?style=for-the-badge&logo=burpsuite&logoColor=white)
![Kali Linux](https://img.shields.io/badge/Kali_Linux-557C94?style=for-the-badge&logo=kali-linux&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)

Personal writeups from my PortSwigger Web Security Academy labs.

I work through these to understand real-world vulnerabilities — how to find them, how to exploit them, and most importantly, how to fix them.

---

## Why I'm Doing This

Web security is a huge field. The PortSwigger labs give you a structured way to learn the most important categories step by step. Each lab forces you to think like an attacker, understand how the application works under the hood, and find creative ways to break it.

This repo documents what I learn. If someone else finds it useful, that's a bonus.

---

## Topics Covered

| Category | Labs Solved | Status |
|---|---|---|
| Path Traversal | 2 / 8 | In progress |
| Access Control | 7 / 13 | In progress |

More categories coming as I work through them.

---

## Progress

```
█████████░░░░░░░░░░░  9 / ~250  (4%)
```

---

## Repository Structure

```
portswigger-academy/
├── README.md
├── LICENSE
├── ROADMAP.md
├── Path Traversal/
│   ├── 01 - File Path Traversal - Simple Case/
│   │   └── README.md
│   └── 02 - File Path Traversal - Traversal Sequences Blocked with Absolute Path Bypass/
│       ├── images/
│       │   ├── 01-original-request.png
│       │   └── 02-successful-exploit.png
│       └── README.md
└── Access Control/
    ├── 01 - Unprotected Admin Functionality/
    │   └── README.md
    ├── 02 - Unprotected Admin Functionality With Unpredictable URL/
    │   └── README.md
    ├── 03 - User Role Controlled By Request Parameter/
    │   └── README.md
    ├── 04 - User ID Controlled By Request Parameter/
    │   └── README.md
    ├── 05 - User ID Controlled By Request Parameter With Data Leakage In Redirect/
    │   └── README.md
    ├── 06 - User ID Controlled By Request Parameter With Password Disclosure/
    │   └── README.md
    └── 07 - Insecure Direct Object References/
        └── README.md
```

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

## Disclaimer

> These writeups are for educational purposes only. I solved these labs on PortSwigger's hosted platform. Do not test vulnerabilities on systems you don't own or have permission to test.

---

## Badges

![GitHub last commit](https://img.shields.io/github/last-commit/Utkarsh464/portswigger-academy)
![GitHub repo size](https://img.shields.io/github/repo-size/Utkarsh464/portswigger-academy)
![GitHub](https://img.shields.io/github/license/Utkarsh464/portswigger-academy)

---

## What's Next

I'm working through the remaining labs in order. Next up:

- More Path Traversal labs
- Access Control labs (horizontal privilege escalation)
- SQL Injection
- Cross-Site Scripting (XSS)
- CSRF
- SSRF
- XXE
- And everything else

---

Let me know if you spot a mistake. I'm learning too.
