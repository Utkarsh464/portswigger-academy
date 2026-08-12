# PortSwigger Web Security Academy — Writeups

![Burp Suite](https://img.shields.io/badge/Burp_Suite-FF6633?style=for-the-badge&logo=burpsuite&logoColor=white)
![Kali Linux](https://img.shields.io/badge/Kali_Linux-557C94?style=for-the-badge&logo=kali-linux&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)

Personal, step-by-step writeups from my [PortSwigger Web Security
Academy](https://portswigger.net/web-security) labs. Each one walks through how
to find a vulnerability, how to exploit it, and — most importantly — how to fix
it.

---

## Table of Contents

- [Progress](#progress)
- [Writeups](#writeups)
  - [Access Control](#access-control)
  - [Path Traversal](#path-traversal)
  - [Cross-Site Scripting (XSS)](#cross-site-scripting-xss)
  - [SSRF](#ssrf)
  - [SQL Injection](#sql-injection)
- [How Each Writeup Is Structured](#how-each-writeup-is-structured)
- [What's Next](#whats-next)
- [Disclaimer](#disclaimer)
- [Badges](#badges)

---

## Progress

| Category | Labs Solved | Status |
|---|---|---|
| Access Control | 13 / 13 | Completed |
| Path Traversal | 2 / 6 | In progress |
| Cross-Site Scripting (XSS) | 2 / 30 | In progress |
| SSRF | 2 / 7 | In progress |
| SQL Injection | 13 / 18 | In progress |

---

## Writeups

Writeups with a `images/` folder include screenshots taken while solving the
lab. See `ROADMAP.md` for the full tracked list and remaining labs.

### Access Control

*13 / 13 — completed*

| # | Lab | Difficulty | What it covers |
|---|---|---|---|
| 1 | [Unprotected Admin Functionality](Access%20Control/01%20-%20Unprotected%20Admin%20Functionality) | Apprentice | Admin panel exposed with no access control. |
| 2 | [Unprotected Admin Functionality With Unpredictable URL](Access%20Control/02%20-%20Unprotected%20Admin%20Functionality%20With%20Unpredictable%20URL) | Apprentice | Hidden admin path discovered (e.g. via `robots.txt`). |
| 3 | [User Role Controlled By Request Parameter](Access%20Control/03%20-%20User%20Role%20Controlled%20By%20Request%20Parameter) | Apprentice | Role/privilege supplied entirely in a request parameter. |
| 4 | [User ID Controlled By Request Parameter](Access%20Control/04%20-%20User%20ID%20Controlled%20By%20Request%20Parameter) | Apprentice | Horizontal escalation by tampering with the `id` parameter. |
| 5 | [User ID Controlled By Request Parameter With Data Leakage In Redirect](Access%20Control/05%20-%20User%20ID%20Controlled%20By%20Request%20Parameter%20With%20Data%20Leakage%20In%20Redirect) | Apprentice | Data leaked through a redirect after a tampered `id`. |
| 6 | [User ID Controlled By Request Parameter With Password Disclosure](Access%20Control/06%20-%20User%20ID%20Controlled%20By%20Request%20Parameter%20With%20Password%20Disclosure) | Apprentice | Plaintext password disclosed via `id` manipulation. |
| 7 | [Insecure Direct Object References](Access%20Control/07%20-%20Insecure%20Direct%20Object%20References) | Apprentice | URI/ID references expose other users' resources. |
| 8 | [User Role Can Be Modified In User Profile](Access%20Control/08%20-%20User%20Role%20Can%20Be%20Modified%20In%20User%20Profile) | Apprentice | `roleid` changed via the profile update endpoint. |
| 9 | [User ID Controlled By Request Parameter With Unpredictable User IDs](Access%20Control/09%20-%20User%20ID%20Controlled%20By%20Request%20Parameter%20With%20Unpredictable%20User%20IDs) | Apprentice | GUID-based IDs; locate the victim's ID then escalate. |
| 10 | [URL-Based Access Control Can Be Circumvented](Access%20Control/10%20-%20URL-Based%20Access%20Control%20Can%20Be%20Circumvented) | Practitioner | Blocked URL bypass with `X-Original-URL`. |
| 11 | [Method-Based Access Control Can Be Circumvented](Access%20Control/11%20-%20Method-Based%20Access%20Control%20Can%20Be%20Circumvented) | Practitioner | Check only on certain HTTP methods; switch methods to bypass. |
| 12 | [Multi-Step Process With No Access Control On One Step](Access%20Control/12%20-%20Multi-Step%20Process%20With%20No%20Access%20Control%20On%20One%20Step) | Practitioner | Multi-step workflow with an unguarded step. |
| 13 | [Referer-Based Access Control Can Be Circumvented](Access%20Control/13%20-%20Referer-Based%20Access%20Control%20Can%20Be%20Circumvented) | Practitioner | Authorization decided by the `Referer` header. |

### Path Traversal

2 / 6 — in progress

| # | Lab | Difficulty | What it covers |
|---|---|---|---|
| 1 | [File Path Traversal - Simple Case](Path%20Traversal/01%20-%20File%20Path%20Traversal%20-%20Simple%20Case) | Apprentice | Absolute traversal sequences to read `/etc/passwd` and more. |
| 2 | [File Path Traversal - Traversal Sequences Blocked with Absolute Path Bypass](Path%20Traversal/02%20-%20File%20Path%20Traversal%20-%20Traversal%20Sequences%20Blocked%20with%20Absolute%20Path%20Bypass) | Practitioner | Bypass a filter that blocks traversal sequences using absolute paths. |

### Cross-Site Scripting (XSS)

2 / 30 — in progress

| # | Lab | Difficulty | What it covers |
|---|---|---|---|
| 1 | [Reflected XSS into HTML context with nothing encoded](Cross-Site%20Scripting%20%28XSS%29/01%20-%20Reflected%20XSS%20into%20HTML%20context%20with%20nothing%20encoded) | Apprentice | Inject and reflect script via the search input. |
| 2 | [Stored XSS into HTML context with nothing encoded](Cross-Site%20Scripting%20%28XSS%29/02%20-%20Stored%20XSS%20into%20HTML%20context%20with%20nothing%20encoded) | Apprentice | Stored payload triggers when the content is viewed. |

### SSRF

2 / 7 — in progress

| # | Lab | Difficulty | What it covers |
|---|---|---|---|
| 1 | [Basic SSRF against the local server](SSRF/01%20-%20Basic%20SSRF%20against%20the%20local%20server) | Apprentice | Point the stock-check URL at `http://localhost/admin`. |
| 2 | [Basic SSRF against another back-end system](SSRF/02%20-%20Basic%20SSRF%20against%20another%20back-end%20system) | Apprentice | Scan `192.168.0.X` for an internal admin interface. |

### SQL Injection

13 / 18 — in progress

| # | Lab | Difficulty | What it covers |
|---|---|---|---|
| 1 | [SQL injection vulnerability in WHERE clause allowing retrieval of hidden data](SQL%20Injection/01%20-%20SQL%20injection%20vulnerability%20in%20WHERE%20clause%20allowing%20retrieval%20of%20hidden%20data) | Apprentice | `' OR 1=1--` to break the WHERE clause and reveal all records. |
| 2 | [SQL injection vulnerability allowing login bypass](SQL%20Injection/02%20-%20SQL%20injection%20vulnerability%20allowing%20login%20bypass) | Apprentice | Bypass authentication by injecting into the login query. |
| 3 | [SQL injection attack, querying the database type and version on Oracle](SQL%20Injection/03%20-%20SQL%20injection%20attack%2C%20querying%20the%20database%20type%20and%20version%20on%20Oracle) | Practitioner | Oracle version via `UNION SELECT` and `v$version`. |
| 4 | [SQL injection UNION attack, determining the number of columns returned by the query](SQL%20Injection/04%20-%20SQL%20injection%20UNION%20attack%2C%20determining%20the%20number%20of%20columns%20returned%20by%20the%20query) | Practitioner | `ORDER BY` and `NULL` probes to size the query for `UNION`. |
| 5 | [SQL injection attack, querying the database type and version on MySQL and Microsoft](SQL%20Injection/05%20-%20SQL%20injection%20attack%2C%20querying%20the%20database%20type%20and%20version%20on%20MySQL%20and%20Microsoft) | Practitioner | Version via `@@version` / `version()` on MySQL & MSSQL. |
| 6 | [SQL injection attack, listing the database contents on non-Oracle databases](SQL%20Injection/06%20-%20SQL%20injection%20attack%2C%20listing%20the%20database%20contents%20on%20non-Oracle%20databases) | Practitioner | Enumerate schema/data via `information_schema`, dump credentials. |
| 7 | [SQL injection with filter bypass via XML encoding](SQL%20Injection/07%20-%20SQL%20injection%20with%20filter%20bypass%20via%20XML%20encoding) | Practitioner | WAF-encoded `UNION` payload in XML to bypass the filter. |
| 8 | [SQL injection attack, listing the database contents on Oracle](SQL%20Injection/08%20-%20SQL%20injection%20attack%2C%20listing%20the%20database%20contents%20on%20Oracle) | Practitioner | Enumerate Oracle DB via `all_tables`/`all_tab_columns`, dump credentials. |
| 9 | [SQL injection UNION attack, finding a column containing text](SQL%20Injection/09%20-%20SQL%20injection%20UNION%20attack%2C%20finding%20a%20column%20containing%20text) | Practitioner | Probe `UNION` columns with a string to find a text-compatible position. |
| 10 | [SQL injection UNION attack, retrieving data from other tables](SQL%20Injection/10%20-%20SQL%20injection%20UNION%20attack%2C%20retrieving%20data%20from%20other%20tables) | Practitioner | `UNION SELECT username,password FROM users--` to dump credentials. |
| 11 | [SQL injection UNION attack, retrieving multiple values in a single column](SQL%20Injection/11%20-%20SQL%20injection%20UNION%20attack%2C%20retrieving%20multiple%20values%20in%20a%20single%20column) | Practitioner | `\|\|` concatenation to dump `username~password` via one column. |
| 12 | [Blind SQL injection with conditional responses](SQL%20Injection/12%20-%20Blind%20SQL%20injection%20with%20conditional%20responses) | Practitioner | Boolean oracle via `Welcome back`; `SUBSTRING()` per-character extraction. |
| 13 | [Blind SQL injection with conditional errors](SQL%20Injection/13%20-%20Blind%20SQL%20injection%20with%20conditional%20errors) | Practitioner | Oracle `CASE WHEN` + `TO_CHAR(1/0)` error oracle; `SUBSTR()` extraction. |

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
> Portswigger's hosted platform. Do not test vulnerabilities on systems you
> don't own or have permission to test.

---

## Badges

![GitHub last commit](https://img.shields.io/github/last-commit/Utkarsh464/portswigger-academy)
![GitHub repo size](https://img.shields.io/github/repo-size/Utkarsh464/portswigger-academy)
![GitHub](https://img.shields.io/github/license/Utkarsh464/portswigger-academy)

Let me know if you spot a mistake. I'm learning too.