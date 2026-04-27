# Portfolio & Projects

Security hires on demonstration. Credentials get past HR; public work gets past technical managers. This document defines what to build and how to present it.

---

## Core Portfolio Components

All five should exist and be linked from your resume/LinkedIn:

### 1. Personal security blog
- Simple static site (Jekyll/Hugo/Astro on GitHub Pages) — don't spend time on aesthetics
- Content mix:
  - HTB/retired machine writeups (technical)
  - Tool/technique deep-dives
  - The differentiation project (see below)
  - Occasional AI+security analysis posts
- Target: 15-20 posts by end of Phase 3
- Own domain is nice but optional

### 2. GitHub
- Pin 3-5 repos that demonstrate security skill:
  - Writeups repo (markdown files organized by platform/box)
  - Any tools you write during OSCP prep or projects
  - The differentiation project
- Clean READMEs, no dead/experimental repos pinned

### 3. HackTheBox profile
- Public profile linked everywhere
- Aim for Pro Hacker rank by end of Phase 2
- 25-30 boxes completed by application time

### 4. HackerOne profile
- Create early, even before submitting anything
- Target: 1-2 valid public disclosures by end of Phase 3
- Even low-severity findings (info disclosure, minor XSS on non-critical apps) count as signal

### 5. LinkedIn / X presence
- LinkedIn: cyber transition framed clearly, portfolio links prominent
- X (optional but valuable): follow infosec people, share your writeups, engage with the community
- Don't cringe-post about "journey"s — just ship and share work

---

## HackTheBox Writeup Cadence

### During Phase 1
- 3-5 beginner boxes, writeups optional (private notes fine)

### During Phase 2 (OSCP sprint)
- 25-30 total boxes
- Publish writeups **only for retired machines** (HTB TOS)
- Target: 10+ published writeups
- Style: technical, show your actual methodology including dead ends, not just the successful path

### Good writeup structure
1. Box overview and difficulty
2. Reconnaissance — what you ran, what you found
3. Enumeration — full service-by-service analysis
4. Foothold — the initial exploit, with code
5. Privilege escalation — how you got root
6. Lessons learned / what tripped you up

The "dead ends" part is what makes writeups good. Anyone can copy the solution; showing *how you thought through it* demonstrates real skill.

---

## The Differentiation Project

This is the single highest-leverage thing you'll do. Pick ONE and ship it well by end of Phase 3.

### Why this matters for you specifically
Nobody else in the junior cybersecurity pool has your AI/ML depth. Your GRACE and ALICE work aren't just resume filler — they're credibility anchors for work at the AI + security intersection. Even if you want pure cyber roles, this project makes you memorable.

### Project option A: LLM Application Pen Testing Methodology
- A structured methodology for assessing security of LLM-integrated applications
- Reference OWASP LLM Top 10, extend with your own categories
- Include 2-3 worked examples on real open-source projects (with responsible disclosure if you find issues)
- Deliverable: blog series + GitHub repo with checklist and tooling

### Project option B: Agent System Red Team Tool
- An open-source tool for testing prompt injection, tool misuse, and privilege escalation in LLM agent systems
- Given your LangChain/LangGraph experience, this is a natural fit
- Could integrate with popular frameworks (LangChain, LlamaIndex, AutoGen)
- Deliverable: GitHub repo with docs, examples, demo video

### Project option C: Vulnerability Assessment of Open-Source Agent Framework
- Pick a popular framework (one you've used)
- Do a structured security assessment: threat model, attack surface analysis, actual testing
- Responsibly disclose any real findings
- Deliverable: long-form technical writeup + any CVEs/advisories

### Project option D: AI Red Team Playbook
- Document methodologies for red-teaming AI applications at a company level
- Less code-heavy, more process-oriented
- Good fit if offensive coding is slower than you'd like
- Deliverable: comprehensive guide document, possibly self-published or as a long blog series

### Evaluation criteria (pick the project that scores highest)
- **Are you actually interested?** — if not, it'll stall
- **Does it use your unique background?** — GRACE, ALICE, LangChain experience
- **Does it produce something sharable?** — not just "I learned things"
- **Can it realistically ship in ~8 weeks?** — scope conservatively

---

## Bug Bounty Strategy

### Goal
Not to make money — to generate signal. One or two valid findings is enough.

### Where to start
- **HackerOne public programs** (not invite-only)
- **Bugcrowd** public programs
- **Start with beginner-friendly programs**: those that explicitly welcome new researchers
- **Government VDPs** (US HackerOne government programs) — no bounty but valid CVEs

### What to hunt
- **Don't try to compete with seasoned hunters on major programs** (Google, Meta, etc.)
- Target smaller programs with fewer researchers
- Focus on vulnerability classes you're strong in (whatever you've practiced most in PortSwigger)
- Information disclosure, minor access control issues, and misconfigurations are underrated

### Expectations
- 10+ hours of hunting before your first valid finding is normal
- Most bugs will be duplicates — don't take it personally
- One valid Low-severity finding by end of Phase 3 = mission accomplished

---

## Positioning the AI/ML Background

Your background isn't a gap to explain; it's the thing that makes you different. In every piece of portfolio work:

- **Don't lead with it** — lead with the security skill
- **Let it surface naturally** — "I was testing LangChain because I've built agent systems with it"
- **Frame as complement, not substitute** — cyber is the skill, AI is the domain expertise
- **Avoid buzzword soup** — "GenAI security" sounds like marketing; "I tested prompt injection in a production agent framework" sounds like work

---

## What NOT to Build

- **Yet another CTF writeup blog with nothing distinctive** — have one, but don't make it your whole identity
- **Tools that duplicate existing popular tools** — nobody needs another nmap wrapper
- **AI-generated slop content** for SEO — actively hurts credibility
- **Massive projects that won't ship** — better to ship one focused thing than half-finish three
