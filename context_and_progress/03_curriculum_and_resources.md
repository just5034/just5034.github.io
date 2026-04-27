# Curriculum & Resources

Opinionated list of what to learn, in what order, from where. Not exhaustive — focused on highest-ROI resources.

---

## Foundations

### Networking
- **Beej's Guide to Network Programming** (free online) — practical, code-oriented
- **Kurose & Ross, *Computer Networking: A Top-Down Approach*** — textbook backup if you want depth
- **Wireshark**: install it, capture your home network traffic, learn to filter and dissect packets
- **PicoCTF networking challenges** — hands-on reinforcement

### Linux / Systems
- **The Linux Command Line** by William Shotts (free online) — if shell fluency is weak
- **Linux Kernel Development** by Robert Love — optional, for deeper systems understanding
- **The Cyber Mentor's "Linux 101"** (YouTube) — free, pragmatic
- Exercise: set up a Linux server from scratch, harden it, audit it

### C / Low-level
- **The C Programming Language** (K&R) — still the reference
- **Beej's Guide to C Programming** — more approachable alternative
- Only needed to the level of "can read exploit code comfortably"

---

## Core Cybersecurity Mindset

- **Security Engineering** by Ross Anderson (free online, 3rd edition) — **the** book on thinking about security systems. Read throughout Phase 1.
- **The Cuckoo's Egg** by Clifford Stoll — narrative, sets up threat hunting intuition
- **Countdown to Zero Day** by Kim Zetter — Stuxnet story, great for understanding nation-state ops

---

## Web Security (Offensive)

- **PortSwigger Web Security Academy** (free) — the gold standard. Work through tracks in this order:
  1. SQL injection
  2. Authentication
  3. Access control
  4. XSS
  5. SSRF
  6. XXE
  7. Deserialization
  8. Everything else
- **The Web Application Hacker's Handbook** (Stuttard & Pinto) — dated but canonical
- **The Tangled Web** by Michal Zalewski — how browsers actually work
- **Real-World Bug Hunting** by Peter Yaworski — writeup collection, great pattern learning

---

## Hands-On Platforms

Ranked by ROI for your path:

1. **HackTheBox** — primary. Get a VIP subscription during OSCP prep.
   - Follow **TJ Null's OSCP-like machines list** specifically
2. **PortSwigger Academy** — free, web-focused, essential
3. **TryHackMe** — easier on-ramp than HTB, good for learning specific tools/concepts
4. **pwn.college** (ASU) — binary exploitation, free, excellent curriculum
5. **HackerOne CTF (h1-ctf)** — bug bounty-style challenges
6. **crackmes.one** — reverse engineering practice

---

## OSCP Preparation

### The cert itself
- **PEN-200 course + lab + exam bundle**: ~$1,600 (check current Offensive Security pricing)
- 90 days of lab access is standard; buy more if needed
- Exam: 24 hours practical + 24 hours report writing
- Failure first attempt is normal. Budget emotionally and financially for possible retake (~$249).

### Prep path
1. Complete all PEN-200 course exercises
2. Work through ~80% of the PEN-200 labs
3. Grind TJ Null's HTB list (~40 machines)
4. Do at least 2-3 practice exams under real timing conditions
5. **Practice report writing during prep, not just at the end**

### Key supplementary resources
- **IppSec** YouTube channel — HTB walkthroughs by the best teacher in the space
- **0xdf's writeups** — deep technical blog posts
- **HackTheBox Academy** — official courses, some free, "CPTS" path is alternative to OSCP if OffSec pricing is too much

---

## Optional Certs

- **CompTIA Security+**: cheap, sometimes needed as HR filter. ~$400. Study 2-3 weeks max. Skip if your resume already looks strong.
- **eJPT (eLearnSecurity Junior Penetration Tester)**: cheaper OSCP-alternative, less respected. Skip unless budget is a hard blocker.
- **CISSP**: requires 5 years experience, not relevant now.
- **Burp Suite Certified Practitioner**: free exam, cheap value-add after PortSwigger Academy.
- **OSEP, OSWE, OSED**: advanced OffSec certs, consider *after* first job.

**Avoid**: CEH (widely mocked among practitioners), stacking vendor-specific certs early.

---

## Community & Events (SoCal-focused)

### Regular meetups
- **DC949** — Orange County DEF CON group, monthly
- **OWASP LA** — monthly, web security focus
- **BSides LA** — annual conference, usually summer, affordable (~$50-100)
- **LA2600** — hacker meetup, more casual

### Annual events
- **DEF CON** (Las Vegas, August) — essential, go at least once
- **BSides Las Vegas** (right before DEF CON) — smaller, more technical
- **ShellCon** (Long Beach area) — regional conference

### Online
- **InfoSec Twitter/X** — still the best real-time pulse on the field
- **/r/netsec**, **/r/AskNetsec** — signal-to-noise varies
- **TL;DR Sec newsletter** (Clint Gibler) — weekly, high quality
- **Risky Business podcast** — news, well-curated

---

## AI + Security Reading (for Phase 3 differentiation work)

- **OWASP Top 10 for LLM Applications** — canonical list, read and know cold
- **MITRE ATLAS** — adversarial ML threat framework
- **NIST AI Risk Management Framework**
- **Anthropic's red teaming papers** — public research on LLM security testing
- **"Prompt Injection" papers** — Simon Willison's blog is the best informal tracker
- **Protect AI**, **HiddenLayer**, **Robust Intelligence** blogs — practitioner content

---

## Home Lab Gear

You probably already have more than enough hardware, but:
- A dedicated machine or VM cluster for target practice (beyond HTB)
- VirtualBox or VMware Workstation — free tiers work
- Consider Proxmox on an old machine if you want to get fancy
- A cheap Raspberry Pi + network tap for packet capture experiments
- **Don't over-invest in hardware early** — most learning is on HTB/PortSwigger cloud labs
