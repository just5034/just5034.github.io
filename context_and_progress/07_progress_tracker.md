# Progress Tracker

Active reference for where I am against the roadmap. Update this file at the end of each working session — Claude reads it at the start of each session to orient.

---

## At a glance

- **Current phase:** Phase 1 (Foundations)
- **Started:** 2026-04-23
- **Last updated:** 2026-04-28
- **Current focus:** Burp Suite first-run config + browser proxy + cert install on Kali, then re-walk SQLi Lab 1 in Repeater. Then blind SQLi labs.
- **Next milestone:** Kali VM running on the PC, Burp configured, blind SQLi labs underway — by end of Week 2
- **Blockers / open questions:** none

---

## Hardware Notes

State of the machines for cyber lab work, so this doesn't get re-litigated session to session.

### Personal PC (Windows 11 Home, x86_64, 32 GB RAM, ~400 GB free) — **primary Phase 1 lab machine**

- **Remote access:** runs Tailscale + RustDesk service. Reachable from Surface anywhere with internet. See "Remote access stack" subsection below.
- **Status:** not yet configured for cyber work as of 2026-04-28. No diagnostics run. Original Windows install state.
- **Architecture:** x86_64 (presumed — desktop PC; verify with `(Get-CimInstance Win32_ComputerSystem).SystemType` before committing).
- **Expected hypervisor situation:** likely the same VBS firmware lock as the Surface (same Windows 11 Home edition), but **unverified**. Run the Surface's diagnostic playbook first (`Get-CimInstance Win32_DeviceGuard`) before applying registry edits blindly.
- **Plan:** install VirtualBox 7 + Extension Pack, download the same Kali x86_64 prebuilt VirtualBox image (already on the Surface — just re-download or copy across), import, accept NEM mode if VBS is locked, snapshot. Mirror the Surface's registry edits if HVCI is enabled.
- **VM specs to use:** 8 GB RAM (8192 MB), 4 vCPUs, 80 GB dynamic disk (default in prebuilt image), 128 MB video memory, NAT networking, bidirectional clipboard + drag-and-drop after Guest Additions.

### Surface Pro (Windows 11 Home **ARM**, 16 GB RAM, ~127 GB free) — **non-VM workstation only**

- **Remote access:** has Tailscale + RustDesk client + SSH client. Can drive PC desktop (via RustDesk over Tailscale) and SSH into Kali (over Tailscale) from anywhere with internet. See "Remote access stack" subsection below.
- **Critical:** this is a Windows-on-ARM device (Snapdragon-based). VirtualBox 7.2 on Windows ARM cannot run x86_64 guests — only ARM guests. The Kali x86 prebuilt image errors out with `VBOX_E_PLATFORM_ARCH_NOT_SUPPORTED` (verified 2026-04-28).
- **Decision:** do not pursue ARM Kali. The cyber tooling ecosystem (HTB targets, OSCP exam, most exploits) is x86. Running ARM Kali means perpetually translating from x86 tutorials. Yak-shaving trap; avoid.
- **What the Surface is good for:**
  - Browser-only PortSwigger labs (Apprentice SQLi without Burp — already proven workflow)
  - Reading (Beej, Anderson, MDN, blog posts)
  - Writing (Hugo blog drafts, writeups, project file updates, note-taking)
  - Anything the cyber work doesn't need a Linux VM for
- **Hardware/registry state from earlier session (2026-04-28):** HVCI / Memory Integrity disabled via registry; Windows Hello DeviceGuard scenario disabled (PIN login still works); VBS still running because System Guard Secure Launch is firmware-locked. These edits do no harm; leave them. Does not affect any non-VM workflow.
- **VirtualBox + Extension Pack:** installed but useless for x86 VMs on this hardware. Leave installed or uninstall — preference call.

### Spare desktop (32 GB RAM, 1 TB+ SSD) — **Phase 2 priority hardware**

- Currently in transit logistics; arrives in California after May move.
- Will run **Proxmox bare-metal** for OSCP AD lab work. Bare-metal Type 1 hypervisor sidesteps all the Windows VBS nonsense entirely — no host OS competing for VT-x.
- BIOS pre-flight when it arrives:
  - Confirm Intel VT-x / AMD-V enabled
  - Confirm IOMMU / VT-d enabled (needed for PCI passthrough if used)
  - Look for any "VBS lock" / "Secure Launch" / firmware-level virtualization protections and ensure they're either off or compatible with Proxmox
- Phase 2's heavier multi-VM AD scenarios live here. PC's NEM-mode VirtualBox is fine for Phase 1 single-VM work.

### Remote access stack — Surface ⇄ PC ⇄ Kali

Setup completed 2026-04-28. Surface can drive the PC's desktop and Kali's terminal from anywhere with internet.

- **Tailscale** (free Personal plan, single account) on all three: PC host, Surface, Kali VM. Mesh networking via WireGuard, NAT-traversing, no port forwarding needed. Each device has a stable `100.x.y.z` private IP. `tailscale status` on any device shows the mesh.
- **RustDesk** for full desktop access from Surface to PC. Installed as Windows service on PC with permanent password. Direct IP connection over Tailscale (using PC's `100.x.y.z` + custom firewall-allowed port). The "unencrypted TCP" warning is a non-issue because the entire channel is inside Tailscale's WireGuard tunnel. Use this when GUI tools are needed (Burp, Wireshark, browser-based labs requiring proxy).
- **SSH** for terminal-only Kali access from Surface. Tailscale runs inside the Kali VM, giving Kali its own `100.x.y.z` IP. SSH from Surface direct to Kali via that IP. Use this for any command-line work — much faster and lighter than driving RustDesk just to open a terminal.
- **Constraints for SSH-from-anywhere:** PC must be awake + online (no sleep/hibernate); Kali VM must be running on PC (no pause/save-state); Surface needs any internet connection.
- **Workflow rule of thumb:** RustDesk for GUI, SSH for shells. Default to SSH whenever possible — lower latency, simpler, doesn't require RustDesk on either end.
- **Banked for future polish:** SSH key-pair auth Surface → Kali (skip password prompts), VirtualBox auto-start on PC boot (so Kali is always up when PC is up).

---

## Recent log (newest first)

### 2026-04-29 (6th, sesion)

- Read chapters 1-3 of Anderson's "Security Engineering".

### 2026-04-28 (continued, fifth session)

- Set up remote access stack so Surface can drive PC and Kali from anywhere with internet.
- **Tailscale** (free Personal plan) installed on PC, Surface, and inside the Kali VM. All three meshed under one account. Each device has a stable `100.x.y.z` private IP, NAT-traversed, encrypted via WireGuard.
- **RustDesk** installed on PC (as Windows service, with permanent password) and Surface (as client). Configured for direct IP access on a custom port, allowed through Windows Firewall. Connecting via PC's Tailscale IP gives full desktop access; the "unencrypted TCP" warning is misleading because the channel is wrapped in Tailscale's WireGuard encryption.
- **SSH** enabled inside Kali (`systemctl enable --now ssh`), reachable directly from Surface via Kali's Tailscale IP. Bypasses RustDesk entirely for terminal work — much faster than driving the desktop for command-line tasks.
- Verified end-to-end: from Surface, can SSH into Kali shell over Tailscale.
- Constraint to remember: SSH-from-anywhere only works when (a) PC is awake + online, (b) Kali VM is running on PC, (c) Surface has internet. Sleep/hibernate on PC kills it; pause/save-state on VM kills it.
- Took new Kali snapshot: `clean-install-with-tailscale-ssh` — supersedes `clean-install-updated` as the working rollback point. Old snapshot kept for full-clean rollback if ever needed.
- Banked for future: SSH key-pair auth (Surface → Kali) to skip password prompts. ~5 min when wanted.
- Added SSH-to-PC via key auth (ed25519). Microsoft Account complication resolved by skipping password auth entirely. Key in C:\ProgramData\ssh\administrators_authorized_keys (Windows admin SSH path). Now have three from-Surface paths: RustDesk→PC desktop, SSH→PC shell, SSH→Kali shell. PC SSH enables headless VM start: `VBoxManage startvm "kali-linux-2026.1-virtualbox-amd64" --type headless`.
- **Next session:** Burp first-run, browser proxy + cert, then SQLi Lab 1 in Repeater, then blind SQLi labs.

### 2026-04-28 (continued, fourth session)
- VBS / HVCI fully disabled on PC via registry + bcdedit (no firmware lock here, unlike Surface). VBS confirmed off post-reboot.
- VirtualBox 7 + Extension Pack + Kali x86_64 prebuilt image installed on PC.
- Kali booted natively (VT-x, no NEM mode). apt full-upgrade ran clean. Default kali password changed.
- Clean snapshot taken: `clean-install-updated`.
- Phase 1 Kali deliverable: DONE.
- Next session: Burp first-run, browser proxy + cert, then SQLi Lab 1 in Repeater, then blind SQLi.

### 2026-04-28 (continued, third session of the day)

- Attempted Kali VirtualBox install on Surface. Pre-install diagnostics on the Surface ran cleanly (VBS state matched PC's expected behavior, registry edits applied, Hyper-V features cycled, downloads completed, integrity verified, extraction successful, VirtualBox + Extension Pack installed).
- VM startup failed with `VBOX_E_PLATFORM_ARCH_NOT_SUPPORTED`. **Root cause: Surface is Windows-on-ARM (Snapdragon).** Kali x86_64 images can't run on ARM VirtualBox. Should have caught this earlier — none of the prior diagnostics tested CPU architecture.
- **Decision:** Surface demoted to non-VM workstation (browser labs, reading, writing). PC promoted to primary Phase 1 lab machine. ARM Kali rejected as a yak-shaving trap (cyber tooling ecosystem is x86).
- Net session outcome: ~2.5 hours of setup work that won't deliver Kali on the Surface, but real systems-thinking knowledge gained (VBS, DeviceGuard registry, Hyper-V coexistence, NEM mode, ARM-vs-x86 hypervisor constraints). Blog post material at minimum.
- **Lesson recorded:** "Verify host architecture (`(Get-CimInstance Win32_ComputerSystem).SystemType`) BEFORE downloading any prebuilt VM image. Architecture mismatch fails silently until VM start."
- **Next session:** PC install. Diagnostic playbook first (architecture, VBS state, RAM, disk), then VirtualBox + Kali. Expected smoother given lessons from Surface.


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
- [x] Kali VM set up on PC (VirtualBox 7 + Extension Pack + prebuilt x86_64 image, snapshot taken)
- [x] Burp Suite Community first-run config + browser proxy set up
- [x] Re-walk SQLi Lab 1 in Burp Repeater (validate workflow, build muscle memory)
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

- [x] **SQLi Apprentice labs 1–10** complete (through UNION attacks) — done in browser only, no Burp
- [x] Re-walk SQLi Lab 1 (or another solved lab) in Burp Repeater once Kali is up on PC — validate Burp workflow
- [ ] SQLi Blind injection labs (Burp essentially required from here, so blocked on PC Kali install)
- [ ] SQLi Practitioner labs
- [ ] Authentication track
- [ ] Access control track
- [ ] XSS track
- [ ] SSRF track
- [ ] XXE track
- [ ] Insecure deserialization track
- [ ] Everything else (CSRF, command injection, file upload, JWT, SSTI, etc.)

### Mindset / strategic reading

Throughout Phase 1, a few chapters per week. **All of these can happen on the Surface.**

- [ ] Ross Anderson, *Security Engineering* (3rd ed., free online) — primary mindset book
- [ ] Clifford Stoll, *The Cuckoo's Egg* — narrative threat hunting
- [ ] Kim Zetter, *Countdown to Zero Day* — Stuxnet, nation-state ops

### Hands-on platforms (introductions)

HTB and TryHackMe come into play seriously in Phase 2; in Phase 1 the goal is just first contact. **Will need PC + Kali for HTB VPN.**

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
- [x] 10+ PortSwigger labs completed
- [ ] Kali VM set up and comfortable (deferred to PC; Surface is ARM, blocked)
- [ ] HTB account with 3–5 starter boxes completed

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

### Spare desktop / Proxmox lab — **build in early June after move**

This becomes essential, given the PC is in NEM mode (assuming VBS firmware lock matches Surface) and the Surface is ARM. The spare desktop is the only path to native-VT-x performance for AD lab work.

- [ ] BIOS pre-flight: VT-x / AMD-V enabled; IOMMU / VT-d enabled; check for and disable any firmware VBS / Secure Launch toggles
- [ ] Install Proxmox bare-metal (Type 1, no Windows host competing for the hypervisor)
- [ ] Build AD lab: Domain Controller + 1–2 Windows clients + Kali attacker, all on an internal Proxmox network
- [ ] Snapshot baseline state of each VM before lab work starts (rollback for repeat practice)
- [ ] Verify HTB VPN works from the Kali VM (or from PC's Kali, depending on workflow)

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
- Re-fighting the Windows 11 VBS / hypervisor disable battle on the PC. Mirror the Surface playbook (registry edits, accept NEM mode, move on).
- Pursuing ARM Kali on the Surface. Cyber tooling ecosystem is x86; translating perpetually is a yak-shaving trap.
