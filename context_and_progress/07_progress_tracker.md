# Progress Tracker

Active reference for where I am against the roadmap. Update this file at the end of each working session — Claude reads it at the start of each session to orient.

---

## At a glance

- **Current phase:** Phase 1 (Foundations)
- **Started:** 2026-04-23
- **Last updated:** 2026-04-23
- **Current focus:** Week 1 setup + first PortSwigger labs
- **Next milestone:** Kali VM running, 5+ PortSwigger labs done, by end of Week 2
- **Blockers / open questions:** none

---

## Recent log (newest first)

### 2026-04-23

- Hugo blog live at https://just5034.github.io with PaperMod theme, deployed via GitHub Actions
- HackTheBox, PortSwigger Web Security Academy, HackerOne accounts created
- HackerOne profile filled in (bio, photo, languages, intro, links)
- About page on blog written
- Read MDN HTTP overview + HTTP Messages reference (covered through HTTP/2 binary framing and HTTP/3 conceptually)
- Read PortSwigger "What is SQL injection?" page and watched the intro video
- **Solved PortSwigger SQLi Lab 1** (SQLi in WHERE clause, retrieve hidden data) — solved twice, once with `'--` (constraint removal via comment) and once with `'+OR+1=1--` (constraint replacement with always-true predicate). Did it without Burp Suite by manipulating the URL directly.

---

## Phase 1: Foundations (now → end of May 2026)

### Setup / scaffolding

- [x] Hugo blog live at https://just5034.github.io
- [x] GitHub Actions auto-deploy working
- [x] About page written
- [x] HackTheBox account
- [x] PortSwigger Web Security Academy account
- [x] HackerOne profile (bio, photo, intro, social links, 2FA)
- [ ] LinkedIn updated to reflect security pivot (defer until OSCP scheduled)
- [ ] Kali VM set up (VirtualBox + prebuilt image, snapshot taken)
- [ ] Burp Suite Community installed (only when first lab requires it)
- [ ] Move repo folder out of OneDrive (low priority housekeeping)

### Networking

Goal: make TCP/IP, DNS, HTTP, TLS, and routing feel intuitive, not memorized.

- [x] HTTP fundamentals (MDN HTTP overview, HTTP Messages, including HTTP/2 and /3)
- [ ] Beej's Guide to Network Programming, chapters 1–5 (free online)
- [ ] Beej's Guide remaining chapters
- [ ] TLS handshake mental model (read Cloudflare's "How TLS works" or equivalent)
- [ ] DNS resolution path (recursive vs iterative, record types)
- [ ] TCP vs UDP, three-way handshake, connection states
- [ ] Routing basics (subnets, NAT, common topologies)
- [ ] Wireshark installed
- [ ] Wireshark capture #1: home network traffic, identify HTTP, DNS, TLS handshake
- [ ] Wireshark capture #2: capture a deliberate SQLi payload and find it in the request
- [ ] Kurose & Ross *Computer Networking: A Top-Down Approach* (textbook backup if depth needed; optional)

### Linux / Systems

Self-rated comfort: **decent** (gets around, occasional googling). Goal: comfortable with processes, permissions, syscalls, file descriptors, and ELF basics by end of Phase 1.

- [ ] *The Linux Command Line* by William Shotts — skim for shell fluency gaps (free online)
- [ ] The Cyber Mentor's "Linux 101" YouTube series
- [ ] Set up a Linux server from scratch, harden it, audit it (exercise from curriculum)
- [ ] Process model: ps, top, /proc, signals
- [ ] File permissions deep dive: chmod bits, setuid/setgid/sticky, ACLs
- [ ] Syscalls and strace (run strace on a simple program, understand what it shows)
- [ ] ELF binary basics: sections, segments, readelf, objdump
- [ ] *Linux Kernel Development* by Robert Love (optional, deeper systems understanding)

### C / Low-level

Goal: read exploit code comfortably. Not "write production C."

- [ ] Self-assessment: read a simple exploit writeup and judge gaps honestly
- [ ] K&R *The C Programming Language* — reference, dip into as needed
- [ ] Beej's Guide to C Programming — more approachable alternative
- [ ] Pointers, memory layout, stack vs heap (whatever's rusty)

### Web Security (PortSwigger tracks)

Curriculum order: SQLi → Authentication → Access Control → XSS → SSRF → XXE → Deserialization → everything else.

Phase 1 deliverable: 10+ labs total. Phase 2 deliverable: cumulative depth across most tracks.

- [x] **SQLi Lab 1** — SQLi in WHERE clause, retrieve hidden data (solved 2026-04-23)
- [ ] SQLi Lab 2 — login bypass (next up)
- [ ] SQLi remaining Apprentice labs
- [ ] SQLi Practitioner labs (will need Burp by here)
- [ ] Authentication track
- [ ] Access control track
- [ ] XSS track
- [ ] SSRF track
- [ ] XXE track
- [ ] Insecure deserialization track
- [ ] Everything else (CSRF, command injection, file upload, JWT, SSTI, etc.)

### Mindset / strategic reading

Throughout Phase 1, a few chapters per week.

- [ ] Ross Anderson, *Security Engineering* (3rd ed., free online) — primary mindset book
- [ ] Clifford Stoll, *The Cuckoo's Egg* — narrative threat hunting
- [ ] Kim Zetter, *Countdown to Zero Day* — Stuxnet, nation-state ops

### Hands-on platforms (introductions)

HTB and TryHackMe come into play seriously in Phase 2; in Phase 1 the goal is just first contact.

- [ ] HackTheBox: Starting Point track (guided on-ramp)
- [ ] 3–5 HTB starter boxes completed (Phase 1 deliverable)
- [ ] TryHackMe: free intro path for tool exposure
- [ ] PicoCTF networking challenges (reinforce Wireshark/protocol knowledge)

### Web security supplemental reading (Phase 1 / 2 ongoing)

- [ ] Stuttard & Pinto, *The Web Application Hacker's Handbook* (dated but canonical)
- [ ] Michal Zalewski, *The Tangled Web* (browser internals)
- [ ] Peter Yaworski, *Real-World Bug Hunting* (writeup collection)

### Phase 1 deliverables checklist

- [x] Personal security blog live
- [ ] Kali VM set up and comfortable
- [ ] HTB account with 3–5 starter boxes completed
- [ ] 10+ PortSwigger labs completed (1 done so far)

---

## Phase 2: OSCP Sprint + Portfolio (June → August 2026)

Light tracking now; expand when phase begins.

### Big rocks

- [ ] PEN-200 course + lab + exam bundle purchased (~$1,600)
- [ ] PEN-200 course exercises completed
- [ ] ~80% of PEN-200 labs completed
- [ ] TJ Null's HTB OSCP-like list (target ~40 machines)
- [ ] 2–3 practice exams under real timing
- [ ] Practice report writing during prep, not just at the end
- [ ] **OSCP exam attempted by end of August**
- [ ] OSCP passed (budget for retake at $249 if needed)
- [ ] 25+ HTB machines completed total
- [ ] 10+ retired HTB machine writeups published on blog
- [ ] Spare desktop → Proxmox AD lab for OSCP prep, build in early June after move
- [ ] BIOS check on spare desktop: confirm Intel VT-x or AMD-V is enabled

### Supplementary
- [ ] IppSec YouTube channel — regular viewing
- [ ] 0xdf's writeups — regular reading
- [ ] HackTheBox Academy / CPTS path (alternate or supplement)
- [ ] pwn.college (ASU) for binary exploitation, if time
- [ ] HackerOne CTF (h1-ctf) for bug-bounty-style challenges
- [ ] crackmes.one for reverse engineering practice

### Community / events
- [ ] DEF CON 34 (Las Vegas, August 2026) — book early
- [ ] BSides LA 2026 (check dates, usually summer)
- [ ] BSides Las Vegas (right before DEF CON)
- [ ] DC949 (OC DEF CON group) — monthly attendance starting June
- [ ] OWASP LA — monthly attendance
- [ ] LA2600 — casual, attend once to evaluate
- [ ] ShellCon (Long Beach area) — annual
- [ ] **5–10 SoCal in-person connections** (deliverable)

### Optional / situational certs (Phase 2)

Mostly avoid; revisit only if specific need arises.

- [ ] CompTIA Security+ — only if HR filter at target companies demands it (~$400, 2–3 weeks)
- [ ] Burp Suite Certified Practitioner — free exam, after PortSwigger Academy depth
- [ ] eJPT — skip unless OffSec budget is a hard blocker
- [ ] CEH — **avoid**, widely mocked

---

## Phase 3: Differentiation + Applications (September → November 2026)

### Differentiation project (pick ONE by start of Phase 3)

Options from `04_portfolio_and_projects.md`:
- [ ] Option A: LLM application pen testing methodology
- [ ] Option B: Agent system red team tool (open source)
- [ ] Option C: Vulnerability assessment of an open-source agent framework
- [ ] Option D: AI red team playbook (process-heavy, less code)

Status: not yet selected. Decision point: late August after OSCP outcome known.

### AI + security reading for Phase 3 (begin reading by July as background)

- [ ] OWASP Top 10 for LLM Applications
- [ ] MITRE ATLAS (adversarial ML threat framework)
- [ ] NIST AI Risk Management Framework
- [ ] Anthropic red teaming public papers
- [ ] Simon Willison's prompt injection blog (ongoing tracker)
- [ ] Protect AI / HiddenLayer / Robust Intelligence practitioner blogs
- [ ] TL;DR Sec newsletter (Clint Gibler) — subscribe early, read weekly
- [ ] Risky Business podcast — start listening early

### Bug bounty
- [ ] HackerOne profile populated ✓ (already done in Phase 1)
- [ ] First public program selected (beginner-friendly)
- [ ] First valid Low-severity finding (target: end of Phase 3)

### Applications
- [ ] Resume rewritten with security framing
- [ ] LinkedIn headline + about updated
- [ ] First batch of applications submitted (October)
- [ ] 50+ applications by end of Phase 3
- [ ] 2–3 initial screens or phone calls booked

### Lecturing constraint
- [ ] St. Francis adjunct lecturing capped at 10–15 hrs/week
- [ ] 15 hrs/week minimum protected for cyber

---

## Phase 4: Interviews and Landing (December 2026 → February 2027)

- [ ] Interview prep loops (live exploitation, code review, scenario)
- [ ] Mock interviews
- [ ] Pitch refined: "systems thinker with deep AI expertise who went deep on offensive security"
- [ ] First offer received
- [ ] Salary negotiation executed (target $80–110k SoCal, higher for AI red team)

---

## Backup branch: Detection Engineering

Pivot trigger: by July 2026, if OSCP study feels like grinding rather than engaging.

- [ ] Home SIEM lab (Security Onion or Splunk/Elastic)
- [ ] Atomic Red Team for attack traffic generation
- [ ] Sigma rule writing
- [ ] Bejtlich, *The Practice of Network Security Monitoring*
- [ ] BlueTeamLabs platform
- [ ] SANS free resources

---

## Portfolio components (from `04_portfolio_and_projects.md`)

- [x] Personal blog live
- [ ] 15–20 blog posts by end of Phase 3
- [ ] GitHub: 3–5 pinned repos demonstrating security skill
- [ ] HTB profile public, Pro Hacker rank by end of Phase 2
- [x] HackerOne profile created
- [ ] HackerOne: 1–2 valid public disclosures
- [ ] LinkedIn updated for security
- [ ] X/Twitter security presence (optional)

---

## Quick reference: what NOT to do

From the project files, things to actively avoid (so they stay top of mind):

- Cert-stacking before shipping public work
- Tool obsession (comparison-shopping over skill-building)
- Drifting into AI-security takes when I should be learning cyber fundamentals
- Asking variations of "is this the right path" repeatedly
- Over-scoping the differentiation project at 3x viable scope
- Building "yet another CTF writeup blog" with nothing distinctive
- AI-generated slop content for SEO
- Buying a custom domain before there's content to put on it
- Publishing PortSwigger lab solutions on the public blog (low signal, gameable)
