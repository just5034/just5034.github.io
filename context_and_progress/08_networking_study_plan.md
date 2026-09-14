# 08 — Networking for Red Teaming: Study Plan & Tutor Protocol

Active Phase 1 track as of 2026-09-14. This is the detailed plan; `07_progress_tracker.md` holds the high-level state and points here. **Claude: read the "Tutor Protocol" section at the bottom before guiding me through this track.**

---

## Purpose & scope calibration

I'm learning networking **as a foundation for red teaming / offensive security**, not to become a network engineer. That distinction sets the depth everywhere:

- **I need:** deep *conceptual* fluency in how traffic actually flows end-to-end, addressing and subnetting, the core protocols (DNS, TCP/UDP, IP, ARP, TLS), NAT, routing-at-a-concept-level, and how firewalls/egress filtering shape what's possible. Enough to map a target network, scope an engagement, pivot, MITM a LAN, evade a filter, and reason about every tool I run.
- **I do NOT need:** to configure enterprise routers, grind congestion-control proofs, memorize OSPF/BGP path-selection internals, or do CRC math. Those are engineer-depth. Know they exist, move on.

**Definition of done** (exit criteria — when this is met, return to the Authentication track):

1. Narrate the layered model + encapsulation cold, using a captured packet.
2. Subnet fluently (CIDR, ranges, host counts) without a calculator.
3. Trace a request end-to-end: DHCP → DNS → ARP → routing → NAT → TCP handshake → TLS → HTTP, and say what happens at each step.
4. Map ~10 core protocols each to a concrete offensive technique (see the red-team map below).
5. Basic competence with `nmap`, `tcpdump`/Wireshark, `dig`, `netcat`, `arp`, `traceroute`.

**Time budget:** ~15–25 hrs of reading + hands-on over ~3–4 weeks at 15–20 hrs/week (shared with other Phase 1 work). This is a bounded foundation pass, **not** an open-ended networking major. Networking keeps reinforcing passively through later labs; don't let this block Authentication indefinitely.

---

## The reading spine

**Kurose & Ross, *Computer Networking: A Top-Down Approach*** (8th ed; 7th is fine — chapters map closely). It's a paid textbook — likely reachable via Columbia library access, or the 7th-ed PDF through the library.

- Free, legit companion **Wireshark labs** (chapter-aligned) live at `gaia.cs.umass.edu/kurose_ross` — use these as the hands-on for the reading.
- If a fully-free reading spine is ever wanted instead: **Peterson & Davie, *Computer Networks: A Systems Approach*** is open-access at systemsapproach.org (bottom-up rather than top-down; the arc below still applies).

"Top-down" means the book descends the stack: overview → application → transport → network → link. Read in book order (Ch 1→8); it front-loads the protocols you already touch, which is good for motivation.

---

## Chapter plan (depth-flagged, red-team-oriented)

Depth flags: **CORE** = read carefully · **SKIM** = get the gist, don't grind · **SKIP** = optional/defer.

### [ ] Ch 1 — Computer Networks & the Internet · **CORE**
- **Concepts:** the layered model + **encapsulation** (the single most important idea), network edge vs core, packet vs circuit switching, delay/loss/throughput, a first taste of security.
- **Red-team so-what:** layering is the map for *where* every attack and tool operates (L2 ARP spoof vs L3 routing vs L4 scanning vs L7 web).
- **Hands-on:** install Wireshark on the PC; capture one packet; expand it and identify each layer's header (Ethernet → IP → TCP → TLS). `tracert` a site to see the core and per-hop delay.

### [ ] Ch 2 — Application Layer · **CORE** (DNS), **SKIM** (email, streaming/CDN, P2P)
- **Concepts:** HTTP (you know it — skim, but note cookies/sessions/caching), **DNS deeply** (recursive vs iterative, the resolver hierarchy, record types, caching/TTL), socket programming (skim — you're a programmer).
- **Red-team so-what:** DNS drives subdomain enumeration, OOB exfil (see `notes/portswigger/sqli-oob-dns-reference.md`), DNS spoofing, and DNS-based C2. HTTP is the whole web-exploitation surface.
- **Hands-on:** `dig`/`nslookup` safari across record types (A, AAAA, CNAME, NS, MX, TXT); `dig +trace` to watch recursion; `curl -v` a site; find the DNS + HTTP exchange in Wireshark.

### [ ] Ch 3 — Transport Layer · **CORE** (TCP/UDP/ports/handshake), **SKIM** (reliable-data-transfer derivations, congestion-control math — grasp AIMD conceptually, skip the formulas)
- **Concepts:** UDP vs TCP, ports, the three-way handshake, teardown, sequence/ack numbers, reliability, sockets = (IP, port).
- **Red-team so-what:** the handshake underpins port scanning and firewall/IDS evasion (SYN vs connect vs FIN/idle scans); UDP underpins amplification and DNS/SNMP attacks.
- **Hands-on:** capture and annotate a full TCP handshake + teardown; run your first `nmap` scan (compare `-sT` connect vs `-sS` SYN and relate to the handshake); hold a `netcat` TCP chat and a UDP one.

### [ ] Ch 4 — Network Layer: Data Plane · **CORE** (highest red-team density)
- **Concepts:** IP, IPv4 addressing, **subnetting & CIDR**, NAT, DHCP, IPv6 basics, fragmentation.
- **Red-team so-what:** subnetting = engagement scoping and target-network mapping; NAT = pivoting/tunneling through compromised hosts; DHCP/IP = knowing where you are on a network.
- **Hands-on:** **subnettingpractice.com daily drills** (the one topic that's pure repetition — do it until CIDR is reflexive); `ipconfig`/`ip a` to find your address, mask, gateway, and derive your subnet; `ipconfig /all` for the DHCP lease; compare private vs public IP (whatismyip) to see NAT.

### [ ] Ch 5 — Network Layer: Control Plane · **SKIM** (ICMP is **CORE**)
- **Concepts:** routing at a concept level (link-state vs distance-vector — high level only), OSPF/BGP (know *what* they are + BGP's internet-trust/security relevance; **skim** the algorithms), **ICMP** (ping/traceroute mechanics — core), SDN (**skip** for now).
- **Red-team so-what:** ICMP/traceroute for network recon and mapping; BGP awareness for internet-scale trust; ICMP tunneling as a covert channel.
- **Hands-on:** analyze a `traceroute` hop-by-hop; find ICMP echo request/reply in Wireshark.

### [ ] Ch 6 — Link Layer & LANs · **CORE** (**SKIM** the CRC/error-detection math)
- **Concepts:** MAC addresses, switches, **ARP** (deep — the basis of LAN MITM), Ethernet, VLANs, broadcast domains.
- **Red-team so-what:** ARP spoofing = LAN man-in-the-middle and credential capture; VLAN concepts = segmentation you'll try to hop; switch behavior shapes what you can sniff.
- **Hands-on:** `arp -a`; capture an ARP request/reply in Wireshark; **(later, in the Kali lab)** run an ARP-spoof MITM with `bettercap` as an offensive exercise once the lab network exists.

### [ ] Ch 7 — Wireless & Mobile · **SKIP / DEFER**
- Revisit only if/when a wireless-attack topic or engagement comes up. Note it exists; don't spend Phase 1 time here.

### [ ] Ch 8 — Security in Computer Networks · **CORE** (selective)
- **Concepts:** crypto basics (you have some — skim), **TLS handshake** (core), IPsec/VPN (**skim**, but relate to the WireGuard/Tailscale you already run), **firewalls & IDS** (core — stateful vs stateless, egress filtering).
- **Red-team so-what:** TLS = Burp interception, downgrade attacks, cert-pinning bypass; egress filtering = *why the interactsh domains were blocked* and why OOB channel choice matters; firewall statefulness = evasion.
- **Hands-on:** find the TLS ClientHello + certificate in Wireshark and relate it to a Burp intercept; write and test one egress rule (Windows Firewall on the PC, or `iptables` on Kali) and watch it block a connection.

---

## Red-team "so-what" map (keep the offensive lens front-and-center)

| Networking concept | Offensive technique it unlocks |
|---|---|
| Layering / encapsulation | Knowing which layer each tool/attack operates at |
| DNS | Subdomain enum, OOB exfil, DNS spoofing, DNS C2 |
| HTTP / cookies / sessions | The entire web-exploitation surface (your SQLi track) |
| TCP handshake / ports | Port scanning, SYN/FIN/idle scans, IDS evasion |
| UDP | Amplification, DNS/SNMP attacks |
| IP addressing / subnetting | Engagement scoping, network mapping, lateral movement |
| NAT | Pivoting / tunneling through compromised hosts |
| ARP | LAN MITM, ARP spoofing, credential capture |
| Routing / ICMP | Recon, traceroute mapping, ICMP tunneling |
| TLS | Interception (Burp), downgrade, cert-pinning bypass |
| Firewalls / egress filtering | Choosing exfil/OOB/C2 paths that actually escape |

---

## Practice resources & setup

- **subnettingpractice.com** — CIDR/subnet drills. Daily, short.
- **K&R Wireshark labs** (`gaia.cs.umass.edu/kurose_ross`) — chapter-aligned, free, exactly matched to the reading.
- **TryHackMe** free rooms — the "Pre Security" path and "Network Fundamentals" module for security-flavored hands-on (browser-based; works even on the Surface).
- **Kali VM tools** (on the PC): `nmap`, `tcpdump`, `dig`, `netcat`/`ncat`, `arp`, `traceroute`, and `bettercap` (for the later ARP-MITM exercise).
- **Wireshark** on the PC — the microscope, used *throughout* to see each concept live.

Reading works on the Surface (or anywhere). Packet captures and Kali tools want the PC.

---

## Tutor Protocol — directions for Claude

**When I tell you I'm reading / have finished a chapter or section, or ask for exercises, enter tutor mode and run this loop:**

1. **Active recall first.** Before adding anything, ask me to explain the chapter's 1–2 key concepts back to you. Correct gently and fill gaps. Don't just lecture over me.
2. **Give the red-team "so-what"** for that chapter's concepts (use the map above; go deeper on request). Always tie the concept to an offensive technique — that's the point of this track.
3. **Hand me the hands-on exercise** for that chapter (from the plan, or generate a fresh one), sized ~20–40 min, with any setup/commands. For Kali/tool exercises: give the commands, but make *me* interpret the output — debug with me, don't hand me the conclusion.
4. **Offer check-your-understanding questions** or a short mini-quiz when I want to self-test.
5. **When I've done the reading + exercise,** offer to tick the chapter checkbox here and in `07_progress_tracker.md` and log a one-line progress note.

**Calibration rules:**

- Teach networking at genuine **beginner** depth — I'm new to this domain — but use **CS/ML analogies** freely (I'm strong there): encapsulation ≈ nested wrapper types / function-call stack; subnetting ≈ bit-masking; the TCP connection ≈ a finite state machine; DNS ≈ a distributed cache hierarchy.
- **Enforce the depth flags.** If I start grinding a SKIM/SKIP section (congestion-control proofs, BGP internals, CRC math, wireless), redirect me: "engineer-depth, not red-team-relevant — note it exists, move on."
- **Keep it bounded** to the definition of done. Watch for the setup-yak-shaving / rabbit-hole pattern (see `06_session_prep.md`) and pull me back. Don't let networking expand past the exit criteria before we return to the Authentication track.
- **Bias every example, exercise, and analogy toward offensive security / OSCP / AD.** This is networking *for red teaming*.
- Match my intensity; prose over bullets; no cheerleading.

**Don't:** turn every concept into a wall of text; withhold hands-on debugging help to the point of frustration; or drift into pure network-engineering depth because the textbook covers it.

---

## Progress

- **Current position:** Not started — begin **Ch 1**.
- Chapter checkboxes are in the plan above; tick them as completed. Newest per-chapter notes below (newest first) as we go.
