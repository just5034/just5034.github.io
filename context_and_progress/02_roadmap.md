# Zero-to-Hero Roadmap

Timeline: April 2026 → February 2027 (~10 months to first offer)

---

## Phase 1: Foundations (Now → End of May, ~6 weeks)

**Goal**: Close the gap between ML engineer and someone who can think about systems like a security person.

### Priorities
- **Networking fluency**: TCP/IP, DNS, HTTP, TLS, routing — should feel intuitive, not memorized
  - Beej's Guide to Network Programming
  - Wireshark labs — capture your own traffic, dissect it
- **Linux internals**: processes, permissions, syscalls, file descriptors, ELF basics
- **C refresher** (if rusty) — enough to read exploit writeups comfortably
- **Web security primer**: start PortSwigger Web Security Academy (SQLi track first)
- **Mindset book**: Ross Anderson's *Security Engineering* (free online) — read a few chapters/week

### Deliverables by end of Phase 1
- Kali VM set up and comfortable
- HackTheBox account with 3-5 starter boxes completed
- 10+ PortSwigger labs completed
- Personal security blog live (can be bare-bones Jekyll/Hugo on GitHub Pages)

### Time commitment
15-20 hrs/week. No lecturing yet — push harder here.

---

## Phase 2: OSCP Sprint + Portfolio (June → August, ~3 months)

**Goal**: Earn OSCP, build a visible body of offensive security work.

### Priorities
- **OSCP preparation**: buy the lab + exam bundle (~$1,600)
  - Grind the official PEN-200 labs
  - Supplement with TJ Null's OSCP HTB list
- **HackTheBox progression**: target 25-30 machines completed by end of August
- **Writeups**: publish writeups for at least 10 boxes on your blog (after retirement for HTB)
- **Attempt OSCP by end of August** — budget for a potential second attempt

### Community milestones
- **DEF CON 34** (Las Vegas, August) — go. Stay in a cheap hotel, meet people, attend villages
- **BSides LA** — check 2026 dates; usually summer
- **DC949** (Orange County DEF CON group) — attend monthly starting in June
- **OWASP LA** — monthly meetup

### Deliverables by end of Phase 2
- OSCP certified (or scheduled retake)
- 25+ HTB machines completed
- 10+ public writeups
- In-person connections with 5-10 SoCal security practitioners

### Time commitment
25-30 hrs/week possible over summer (no lecturing). **Use this window hard.**

---

## Phase 3: Differentiation + Applications (September → November, ~3 months)

**Goal**: Ship the thing that sets you apart, and start applying.

### Priorities
- **Differentiation project** — pick ONE, ship it well:
  - A pen testing methodology for LLM-integrated applications (with case studies)
  - An open-source tool for prompt injection testing in agent systems
  - A detailed vulnerability assessment of a popular open-source agent framework
  - A red team playbook for AI applications
  - *This is where GRACE/ALICE experience + OSCP skills compound into something nobody else has*
- **Bug bounty presence**: HackerOne profile, 1-2 valid low-severity findings on public programs
- **Begin applications in October**:
  - 50-100 applications is normal
  - Lean heavily on meetup contacts for referrals
  - Target roles below in Document 05

### Parallel constraint
St. Francis lecturing starts. **Cap at 10-15 hrs/week.** Protect 15 hrs/week minimum for cyber.

### Deliverables by end of Phase 3
- Differentiation project published + promoted (blog post, Twitter/LinkedIn, submit to relevant newsletters)
- Active HackerOne profile
- First batch of applications submitted
- 2-3 initial screens or phone calls booked

---

## Phase 4: Interviews and Landing (December → February 2027)

**Goal**: Convert pipeline to offer.

### Priorities
- **Interview prep specifically for security**:
  - Live exploitation exercises (practice on HTB)
  - Code review questions (OWASP Top 10 patterns)
  - Scenario-based questions ("you see this alert, what do you do")
- **Refine pitch**: "systems thinker with deep AI expertise who went deep on offensive security"
- **Continue shipping** writeups and bug bounty work — pipeline doesn't stop during interviews
- **Salary negotiation prep**: know your numbers, have competing offers if possible

### Target outcome
First offer by end of February 2027, $80-110k range for SoCal pen tester / AppSec role. Higher if AI red team or remote role.

---

## Backup Branch: Detection Engineering

**Pivot trigger**: If by July 2026 OSCP study feels like grinding rather than engaging, or if the offensive mindset just isn't clicking.

### Why this works for you
- ML background is a cleaner fit (data pipelines, anomaly detection, feature engineering on telemetry)
- Job market is more forgiving at the junior level
- Salaries are comparable
- Detection engineering has growing AI integration (behavioral analysis, LLM-assisted triage)

### Pivoted priorities
- Home SIEM lab: Security Onion or Splunk/Elastic stack
- Atomic Red Team for generating attack traffic
- Learn Sigma rule writing
- Read Bejtlich's *The Practice of Network Security Monitoring*
- SANS free resources + BlueTeamLabs platform

---

## Compressed Timeline Option

If willing to take a SOC analyst or junior detection role as a bridge:
- Could land a role by late 2026 (Oct-Dec)
- Lower ceiling on first salary ($60-80k SoCal)
- Faster entry, build resume, pivot into offensive/AppSec after 12-18 months

**Decision point**: revisit in August after OSCP result.

---

## Key Milestones Checklist

- [ ] Phase 1 complete: networking + Linux fluency, PortSwigger started, blog live
- [ ] DEF CON 34 attended
- [ ] OSCP passed
- [ ] 25+ HTB writeups published
- [ ] Differentiation project shipped
- [ ] 50+ applications submitted
- [ ] First offer received
