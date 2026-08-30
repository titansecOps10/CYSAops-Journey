# CYSAops-Journey
Documenting my cyber security roadmap 


# CYSAops Journey

Documenting my cybersecurity roadmap — from environment setup to full mastery.

## Day 1 — Aug 1, 2026: Environment Setup

Today I set up my core dev environment for the cybersecurity roadmap:

- Downloaded and installed **Visual Studio Code**
- Downloaded and installed **Git for Windows** (v2.55.0)
- Verified Git install with `git --version`
- Configured Git identity:
  - `git config --global user.name "TitanSEC"`
  - `git config --global user.email "titansec.001@gmail.com"`
- Verified config with `git config --global --list`
- Created this GitHub repository to document the full learning journey

## Next Goal

- Learn Linux fundamentals
- Complete TryHackMe Pre-Security
- Build my first security project



## Day 2 — Aug 2, 2026: First Hacking Room

Finished my first hands-on room on TryHackMe today — "Offensive Security Intro" from the Pre Security path. Ran everything through my Windows VPS since TryHackMe needs a full browser environment.

The room walks you through attacking a fake bank site called FakeBank. First step was running a directory scan with dirb:

dirb http://fakebank.thm

It came back with two hidden pages that weren't linked anywhere on the actual site — /images and /bank-transfer. The second one turned out to be an admin panel with zero login required. Just... open to anyone who found the URL.

Used it to deposit money into account 8881 and watched the balance flip from -$1,232.32 to positive. That's the whole point of the exercise — showing that this isn't a theoretical bug, you can actually walk in and change real account data because nobody put a lock on the door.

Video Demo.
 https://youtube.com/shorts/4mD1zOtmzCk?si=HUmZbkelpOiljM3w

Finished all 4 tasks, picked up 32 points.

Honestly the biggest thing I took from this: I expected "hacking" to mean writing exploit code or something technical like that. This was just... noticing an unlocked door and walking through it. A lot of real vulnerabilities are probably this simple, not some Hollywood movie scene.

Next up: Linux Fundamentals Part 1, now that it's unlocked.

## Day 3 — Aug 4, 2026: Linux Fundamentals Part 1

Completed Linux Fundamentals Part 1 on TryHackMe — first real dive into the Linux command line as planned for this week's roadmap focus.

### What I practiced
- Identity & location: `whoami`, `pwd`
- Listing and reading files: `ls`, `cat`
- Navigating folders: `cd`
- Searching file contents: `grep THM access.log` — found a flag buried in a log file
- Shell operators: `>` to overwrite a file's contents, `>>` to append without erasing

### Result
- ✅ Room completed
- 🏆 9/9 tasks completed
- 🎯 88 points earned

### Key takeaway
`grep` was the standout for me — being able to search a huge log file for a single pattern instantly is exactly the kind of skill that matters in real security work (finding one flagged line in thousands of log entries). Also finally understand the practical difference between `>` and `>>`, which I'll need for scripting later.

### Next Steps
- Linux Fundamentals Part 2
- Continue building toward Phase 2 (ethical hacking labs)

## Day 4 — Aug 5, 2026: First Python Script

Started Phase 4 of the roadmap today — Python. Set up a proper dev environment on the VPS and wrote my first working script from scratch.

### What I did
- Opened VS Code on the VPS, created a new project folder (`Python-Practice`)
- Installed the Python extension for VS Code
- Discovered Python itself wasn't installed on the VPS — installed it via `uv` (a fast Python installer/package manager)
- Wrote my first script:
  ```python
  name = input("What's your name? ")
  print("Hello, " + name + "! Welcome to Day 1 of Python.")


## Day 5 — Aug 6, 2026: Linux File Permissions (Theory + Verification)

Today's roadmap slot was Cloud Security (AWS), but hit a wall — TryHackMe locked both the AWS rooms and Linux Fundamentals Part 2/3 behind a paywall I can't afford right now. Pivoted to something free and just as valuable: really understanding Linux file permissions, the rwx system, and how chmod's numeric notation actually works.

### What I learned

**The permission model**
Every file/folder has three permission types (read, write, execute) applied to three categories (Owner, Group, Others). Displayed as a 10-character string like `-rwxr-xr--`:
- First character: file type (`-` = file, `d` = directory, `l` = symlink)
- Next 3: Owner permissions
- Next 3: Group permissions
- Last 3: Others permissions

**The numeric system (octal notation)**
Each permission has a fixed value: r=4, w=2, x=1. Add them per category to get a single digit (0-7), giving the three-digit number used in `chmod` commands. E.g. `rwxr-xr--` = 754.

### Verification — ran it on my own VPS

Used Git Bash and ran `ls -l` on a real directory. Decoded actual output from my own system, including:
- Regular files at `644` (rw-r--r--) — sensible default, owner edits, others read-only
- Directories at `755` (rwxr-xr-x) — owner full control, others can enter/read but not modify
- Symlinks showing `777` (rwxrwxrwx) — learned this is normal for symlinks specifically, since real security sits on the target file, not the link itself

### Self-test
Converted 7 permission strings to numeric notation from memory, no reference material. Got all 7 correct:
- rwx→7, r-x→5, -wx→3, r--→4, --x→1, rw-→6, ---→0

### Key takeaway
This ties directly back to real security work — a file showing `777` where sensitive data lives (like a config or password file) is a red flag attackers actively scan for. Understanding what "normal" looks like is what makes misconfigurations spottable.

### Next Steps
- Revisit AWS/cloud security once funds allow for TryHackMe premium, or find a free alternative (AWS Skill Builder, OverTheWire)
- Continue Python scripting


## Day 6 — Aug 7, 2026: Built a Password Strength Checker

First real project from the roadmap's Phase 4 list. Built a Python script from scratch, piece by piece, that checks a password against four real security criteria and gives a verdict.

### What I built
- Takes a password as input
- Checks four conditions:
  - Length ≥ 8 characters
  - Contains an uppercase letter
  - Contains a number
  - Contains a symbol
- Scores the password (0-4) based on how many checks pass
- Uses `if/elif/else` to give a final verdict: STRONG, MEDIUM, or WEAK

### Key code concepts learned
- `any()` with a loop condition — checking if *any* character in a string meets a condition
- Boolean variables (`True`/`False`) and how Python treats them as 1/0 when summed
- `if/elif/else` — first real branching logic, and why indentation isn't just style in Python, it's required syntax that defines what code belongs to which condition

### Verified with two tests
- `Vic@2000` → passed all 4 checks → correctly returned STRONG
- `abc` → failed all 4 checks → correctly returned WEAK
- Predicted the second result correctly before running it

### Key takeaway
This is the first time I built something with actual decision-making logic, not just input/output. Understanding *why* the indentation matters (it's not cosmetic, it defines code blocks) was the biggest concept shift today.

### Next Steps
- Push `password_checker.py` to GitHub (`python-practice` repo)
- Continue building toward the roadmap's remaining Python projects (log analyzer, file encryption tool, port scanner)


# Day 6 — Networking Fundamentals & Packet Analysis
Date: August 8, 2026
Author: Victory (TitanSEC)
Environment: Contabo Cloud VPS (Windows Server), accessed via RDP

## Objective
Build a working knowledge of core networking diagnostic tools and packet-level traffic analysis using Wireshark, then investigate a real connection on a live system.

## Tools Used
- Windows PowerShell (ipconfig, ping, nslookup, tracert, netstat)
- Wireshark 4.6.7 (with Npcap capture driver)

## Part 1 — Command-Line Investigation
Ran baseline diagnostics on the VPS to understand its network configuration.

- ipconfig — Local network config. VPS internal IPv4: 169.58.18.221, gateway 169.58.0.1
- ping 169.58.0.1 — Reachability to gateway. 100% packet loss — expected, most cloud gateways block ICMP by default
- nslookup google.com — DNS resolution. Resolved cleanly via Contabo's DNS server (195.179.224.53), returning multiple IPv4/IPv6 addresses
- tracert google.com — Path to destination. 14 hops, routed through Colt Technology Services' Frankfurt infrastructure before reaching Google's network
- netstat -ano — Active/listening connections. Found routine listening services (RDP 3389, WinRM 5985/5986) and outbound scanner probes against exposed ports from dozens of unrelated foreign IPs

Observation: Port 5986 (WinRM/HTTPS) showed connection attempts from a wide, geographically scattered set of IPs in TIME_WAIT state — consistent with background internet-wide port scanning rather than a targeted attack. Worth revisiting to confirm WinRM external exposure is actually needed.

## Part 2 — Wireshark Packet Capture
Installed Wireshark + Npcap on the VPS and ran a live capture on the Ethernet interface.

### DNS Query/Response Pair (bbc.com)
Isolated with filter: dns

- Query (packet 7146): 169.58.18.221 → 195.179.224.53, UDP src port 61599 → dst port 53. Standard query, type A, for bbc.com.
- Response (packet 7147): 195.179.224.53 → 169.58.18.221, UDP src port 53 → dst port 61599. Returned multiple A records in the 151.101.x.81 range — Fastly CDN IPs, confirming BBC serves its site through Fastly.

This confirmed the standard DNS request/response pattern: client asks a nameserver over UDP/53, nameserver replies with IP(s) for the queried domain.

### RDP/TLS Session Investigation
Isolated with filter: tcp.port == 3389 && ip.addr == 105.112.212.77

- Nearly all traffic captured on this filter was TLSv1.2 between the VPS (169.58.18.221) and the remote RDP client (105.112.212.77) over port 3389.
- Inspected packet 7124 in detail: ACK number in the hundreds of thousands (Ack=536122), indicating this was deep into an already-established session, not a new connection.
- Finding: No SYN / SYN-ACK / ACK handshake was present anywhere in the capture. The capture window started after the RDP session was already active, so the connection-opening handshake predates the capture and was not recoverable from this dataset.

## Key Takeaways
1. RDP encrypts session data at the transport layer via TLS — packet metadata (source/destination IP, port, timing, volume) is visible, but actual content (keystrokes, screen data) is not, by design.
2. A capture is only as complete as its time window — starting a capture mid-session means foundational events (like the TCP handshake) may already be missing. Always start captures before the connection of interest begins, where possible.
3. DNS traffic is easy to identify and interpret even without deep protocol knowledge: UDP port 53, clear query/response labeling in Wireshark, and readable domain names in both the packet detail pane and raw hex/ASCII dump.
4. Background port-scanning noise against common admin ports (3389, 5985, 5986) is constant on any internet-facing host — not evidence of targeted compromise, but a good reminder to minimize exposed services.

## Next Steps
- Re-run capture starting before initiating a new RDP session, to capture the full TCP three-way handshake.
- Review Windows Firewall / Contabo network firewall rules to restrict WinRM (5985/5986) to only trusted source IPs if not actively needed.
- Continue toward TryHackMe rooms covering packet analysis and traffic fundamentals to build on this baseline.

## Day 7 — Aug 8, 2026: Week 1 Assignment — File Permission Auditor

First weekly assignment, combining this week's two skills — Linux file permissions and Python fundamentals — into one working tool. Built a Python script that scans a folder and flags files with dangerous "world-writable" permissions, the same kind of misconfiguration real security auditors check for.

### What I built
A script that:
- Takes a folder path as input
- Lists every file in that folder using `os.listdir()`
- Reads each file's raw permission data with `os.stat().st_mode`
- Converts it to readable octal format (e.g. `666`) using `oct()`
- Loops through every file and flags any where "Others" has write access — a real security red flag

### Errors made and how I fixed them

**1. "Folder name is not valid" in VS Code**
Tried creating the project folder directly through VS Code's file dialog and it kept rejecting even simple names like `test1`. Turned out to be a quirk with VS Code's own dialog — creating the folder in Windows File Explorer instead worked immediately, then opened that same folder in VS Code normally.

**2. NameError: 'readable_permissions' is not defined**
While editing, accidentally deleted the line that calculated `readable_permissions` but left the print line that referenced it — Python couldn't find a variable that no longer existed. Fixed by re-adding the missing line back above the print statement.

**3. Duplicate output (raw number printed twice)**
Ended up with an old leftover print line still referencing the raw permission number, running alongside the new one showing the readable format. Left it in for now rather than fully rebuild the loop — it doesn't break functionality, just prints an extra line. Noted as cleanup for later.

**4. Indentation confusion**
Struggled with how many levels of indentation different lines needed, especially once the `if` statement was nested inside the `for` loop (2 levels deep). Eventually got it by thinking in terms of "one more Tab than the line it belongs inside."

### Verified working
Ran the script on its own folder — correctly detected `permission_auditor.py` had permission `666` and flagged it as WORLD-WRITABLE, since the last digit (6) means Others can write to it.

### Key takeaway
This was a genuinely frustrating session — small mistakes (a missing line, extra indentation, a buggy dialog box) compounded into real confusion more than once. But every error had a clear, findable cause, and working through each one slowly is what got the tool actually working by the end. First time combining two separate skills (Linux permissions + Python logic) into one real tool instead of practicing them separately.

### Repo
[weekly-assignments/week-1-file-permission-auditor](https://github.com/titansecOps10/weekly-assignments)

### Next Steps
- Clean up the duplicate print line
- Add a summary count at the end (e.g. "3 files flagged out of 12 scanned")
- Continue alternating Linux/Python/projects per the weekly roadmap


# Day 9: Zero Trust Architecture (ZTA)

**Date:** August 10, 2026

---

## What I Learned

### Old Model vs Zero Trust

| Traditional | Zero Trust |
|-------------|------------|
| Trust inside network | Trust NOTHING |
| One-time check | Continuous verification |
| Flat network | Micro-segmented |

---

### 5 Core Principles

1. **Verify Explicitly** - Check identity, device, location, time, behavior
2. **Least Privilege** - Give ONLY what's needed, NOTHING more
3. **Assume Breach** - Act like you're already hacked
4. **Micro-segmentation** - Divide network into tiny islands
5. **Continuous Monitoring** - Trust is never permanent

---

### Real-World Example: Bank Access Control

| Role | Access |
|------|--------|
| Customer | ONLY their own account (biometric required) |
| Teller | View balances, withdraw/deposit |
| Branch Manager | Approve loans, override tellers |
| Accountant | Read-only transactions (can audit, can't withdraw) |
| IT Admin | Server maintenance ONLY |

---

### Key Takeaways

✅ **Least Privilege** - No one gets more access than they should

✅ **Impossible Travel** - Login from China at 8AM then Atlanta at 5PM = BLOCK

✅ **Blast Radius** - Even if Accountant gets hacked, only logs exposed. No funds stolen.

✅ **Biometrics** - Fingerprint ensures customers access ONLY their own account

---

### My Definition

> *"Trust NOTHING, verify EVERYTHING, give MINIMUM access."*

---

## Tomorrow's Topic

*TBD*

---

**End of Day 9**


# Ransomware Deep Dive

**Date:** August 12, 2026

---

## What is Ransomware?

Malware that locks your files and demands money to unlock them.

---

## How It Works

1. You click a bad link or open a bad email
2. Malware encrypts your files
3. Pop-up appears: "Pay $500 in Bitcoin"
4. You pay or lose files forever

---

## Real Example: Colonial Pipeline (2021)

- Hacker used a stolen password (no MFA)
- Shut down US fuel supply for 6 days
- Company paid $4.4 million
- Total damage: $100+ million

---

## My Answers to Scenarios

### Scenario 1: Suspicious Email
**My Answer:** Don't open it.
**✅ Correct.** Verify with sender first.

### Scenario 2: Ransomware Attack
**My Answer:** Try to restore backups. Contact FBI. Hack the hacker if possible.
**✅ Correct.** Some hackers get caught by getting hacked back.

### Scenario 3: Found USB Drive
**My Answer:** Hand it to IT immediately.
**✅ Correct.** Never plug in unknown USBs.

---

## How to Defend

### For Me (Personal)
- Backup files regularly
- Don't open suspicious emails
- Keep software updated
- Use antivirus

### For Companies
- Use MFA everywhere
- Give employees only necessary access
- Train staff to spot attacks
- Have backups ready

---

## Key Takeaway

> Backups save you. Criminals can't hold your files hostage if you have copies.

---

**Day 11 Complete - August 12, 2026**


# Day 12: MITRE ATT&CK Framework

**Date:** August 13, 2026

---

## What I Learned

MITRE ATT&CK is a database of hacker techniques. It shows exactly how attackers operate.

---

## The Attack Chain

1. Reconnaissance (Gather info)
2. Resource Development (Setup tools)
3. Initial Access (Get in)
4. Execution (Run malware)
5. Persistence (Stay inside)
6. Privilege Escalation (Get higher access)
7. Defense Evasion (Avoid detection)
8. Credential Access (Steal passwords)
9. Discovery (Explore network)
10. Lateral Movement (Move to other systems)
11. Collection (Gather data)
12. Exfiltration (Steal data)
13. Impact (Final damage)

---

## Real Example

Colonial Pipeline:
- Initial Access → Stolen VPN password
- Impact → Ransomware encryption

---

## Key Takeaway

> *"Know your enemy. MITRE ATT&CK shows you exactly how hackers operate."*

---

**Day 12 Complete**



# Day 13: Cloud Security Basics

**Date:** August 14, 2026

---

## What is Cloud Security?

Protecting your data, apps, and infrastructure in the cloud.

---

## Shared Responsibility Model

| Cloud Provider | You (Customer) |
|----------------|----------------|
| Physical security | Your data |
| Network security | Your passwords |
| Hardware security | Your configurations |
| Base OS patching | Your apps |

---

## Common Cloud Mistakes

- Public storage (anyone can view)
- Weak passwords
- No MFA
- Too much access
- Unpatched systems

---

## Real Example: Capital One (2019)

- Misconfigured firewall
- 100 million records exposed
- $80 million fine

**Lesson:** One misconfiguration = catastrophe.

---

## Cloud Security Tips

- Use MFA
- Least privilege access
- Encrypt data
- Monitor logs
- Regular audits

---

## Key Takeaway

> *"The cloud is secure by default, but insecure by configuration."*

---

**Day 13 Complete - August 14, 2026**


# Day 14: Digital Forensics

**Date:** August 15, 2026

---

## What is Digital Forensics?

Investigating digital crime by finding and analyzing evidence.

---

## 5 Steps of Forensics

1. **Identification** - Find devices with evidence
2. **Preservation** - Secure evidence (NEVER work on original)
3. **Analysis** - Examine data (logs, files, history)
4. **Documentation** - Write everything down
5. **Presentation** - Explain findings in court

---

## Types of Forensics

- Computer (hard drives, files)
- Network (traffic, logs)
- Mobile (phones, texts)
- Cloud (AWS, Azure)
- Memory (RAM)

---

## Chain of Custody

Every piece of evidence must be tracked:
- Who collected it?
- When?
- Where?
- Who had it next?

If broken → Evidence is useless in court.

---

## Real Case: Silk Road

**How FBI caught Ross Ulbricht:**
- Traced server to Iceland
- Watched him log in at a café
- Grabbed his laptop while he was there

**He got caught because:**
- Reused usernames
- Posted real email
- Sloppy OpSec

**Lesson:** Even masterminds make rookie mistakes.

---

## My Hot Take

> *"If the FBI didn't physically see the laptop, they wouldn't have caught him. Rookies."*

---

## Tools Used

- FTK (Forensic Toolkit)
- EnCase
- Autopsy (free)
- Wireshark (network)
- Volatility (memory)

---

## Key Takeaway

> *"Digital evidence is fragile. One mistake destroys it forever."*

---

**Day 14 Complete - August 15, 2026**




# Day 15: OSINT (Open Source Intelligence)

**Date:** August 16, 2026

---

## What is OSINT?

Gathering information from publicly available sources.

No hacking. No breaking in. Just using what's already out there.

---

## Where OSINT Comes From

| Source | Examples |
|--------|----------|
| Social Media | Facebook, Twitter, LinkedIn, Instagram |
| Search Engines | Google, Bing, DuckDuckGo |
| Public Records | Court records, property records |
| Government Data | Census, voting records |
| Company Websites | Employee names, emails |
| Data Breaches | Leaked passwords, emails |

---

## What OSINT Can Reveal

- Real name
- Address
- Phone number
- Email
- Family members
- Employer
- Habits
- Passwords (via breaches)
- Connections

---

## Real Example: The Masked Hacker

**Mistake:** Used real email on a forum

**How caught:**
1. Email → LinkedIn → Real name
2. Real name → Facebook → Friends, location
3. Location → Public records → Address
4. Address → FBI showed up

**Lesson:** One slip = caught.

---

## OSINT Tools

| Tool | Purpose |
|------|---------|
| Google Dorking | Advanced search |
| Shodan | Find internet-connected devices |
| Maltego | Visualize relationships |
| theHarvester | Find emails and subdomains |
| Recon-ng | OSINT automation |
| Sherlock | Find usernames across platforms |
| HaveIBeenPwned | Check if email is in a breach |

---

## How to Protect Yourself

- Limit social media
- Use fake names
- Don't post location
- Use different emails
- Opt out of data brokers
- Use strong passwords
- Enable MFA

---

## My OSINT Challenge Answer

**Scenario:** Journalist investigating a corrupt politician

**3 things I'd search first:**
1. Name (Google, LinkedIn)
2. Email (theHarvester, HaveIBeenPwned)
3. Social Media accounts (Sherlock)

---

## Key Takeaway

> *"You don't need to be a hacker to find information. You just need to know where to look."*

---

**Day 15 Complete - August 16, 2026**



# Day 16: OSINT & Google Dorks

**Date:** August 17, 2026

---

## What I Learned

Google Dorks are advanced searches that find exposed information.

---

## Dorks I Tried

1. `intitle:"index of" "wp-content"` → ✅ WORKED
2. `inurl:login "admin" site:.com` → ✅ WORKED
3. `filetype:log "username" -github` → ❌ BLOCKED
4. `filetype:env "DB_PASSWORD" -github` → ❌ BLOCKED
5. `site:.gov filetype:pdf "confidential"` → ❌ BLOCKED

---

## Results

- No email breaches (HaveIBeenPwned)
- Found exposed login pages and directories
- Learned that VPN helps avoid Google blocks

---

## Key Takeaway

> *"Google Dorks are powerful — but you need patience and sometimes a VPN."*

---

**Day 16 Complete**


# Day 17: Password Security & Cracking

**Date:** August 18, 2026

---

## What I Learned

- Hackers crack passwords using brute force, dictionary attacks, and rainbow tables
- Length > 12 characters with mixed characters is strongest
- Password managers are essential

---

## Password Strength Test Results

| Password | Crack Time |
|----------|------------|
| password123 | Instant |
| B1ue$ky#2026 | Minutes/hours |
| correcthorsebatterystaple | Years |

---

## Key Takeaway

> *"A strong password is the first line of defense. Make it long, unique, and random."*

---

**Day 17 Complete**


# Day 18: Phishing 2.0 — Advanced Social Engineering

**Date:** August 19, 2026

---

## What I Learned

Phishing has evolved from obvious scams to personalized, AI-driven attacks.

---

## Modern Techniques

- Spear Phishing (targeted)
- Whaling (executives)
- Clone Phishing (copy real emails)
- Vishing (voice calls)
- Smishing (SMS)
- Deepfake Phishing (video/audio)

---

## Why It Works

- Urgency
- Fear
- Authority
- Trust
- Curiosity
- Greed

---

## Real Example: MGM Resorts (2023)

- Hacker called helpdesk
- Pretended to be employee
- Helpdesk reset password
- $100+ million loss

---

## Defenses

- Verify through another channel
- Check email headers
- Hover over links
- Don't trust urgency
- Use MFA
- Security training

---

## Key Takeaway

> *"Phishing 2.0 is personal, believable, and dangerous. Always verify before you trust."*

---

**Day 18 Complete**



# Day 19: Wi-Fi Security

**Date:** August 20, 2026

---

## What I Learned

Public Wi-Fi is insecure. Hackers use:
- Man-in-the-Middle (intercept traffic)
- Evil Twin (fake Wi-Fi networks)
- Packet Sniffing (capture unencrypted data)

---

## How to Protect Myself

- Use a VPN
- Always use HTTPS (look for padlock)
- Turn off file sharing
- Use mobile hotspot instead of public Wi-Fi
- Log out of sensitive accounts

---

## Key Takeaway

> *"Public Wi-Fi is a public conversation. If you don't want strangers hearing it, encrypt it."*

---

**Day 19 Complete**


# Day 20: Malware Types

**Date:** August 21, 2026

---

## 7 Types of Malware

1. Virus — Attaches to files, spreads when executed
2. Worm — Self-replicates without user action
3. Trojan — Disguises as legit software, steals data
4. Ransomware — Encrypts files, demands payment
5. Spyware — Secretly monitors activity
6. Adware — Displays unwanted ads
7. Rootkit — Hides deep in system, gives admin access

---

## How Malware Spreads

- Email attachments
- Malicious websites
- USB drives
- Software cracks
- Phishing links
- Exploits

---

## How to Defend

- Antivirus
- Keep software updated
- Don't open suspicious emails
- Use MFA
- Backup data
- Avoid cracked software

---

## Key Takeaway

> *"Malware is everywhere. Stay vigilant, update your systems, and think before you click."*

---

**Day 20 Complete**

# Day 21: Incident Response (IR)

**Date:** August 23, 2026

---

## What I Learned

Incident Response is the plan for when things go wrong.

---

## The 6 Phases

1. **Preparation** — Train, plan, backup
2. **Identification** — Detect and confirm the attack
3. **Containment** — Isolate the threat
4. **Eradication** — Remove the malware
5. **Recovery** — Restore systems
6. **Lessons Learned** — Improve for next time

---

## Real Example: Uber (2022)

- No MFA → Employee got phished
- Hacker accessed internal systems
- Uber improved MFA after

---

## Key Takeaway

> *"Incident Response is like a fire drill. If you don't practice, you'll panic when it's real."*

---

**Day 21 Complete**

# Linux Permissions Cheat Sheet

**Date:** August 24, 2026

---

## Permission Types

- r = read
- w = write
- x = execute

---

## Permission Levels

- u = user (owner)
- g = group
- o = others

---

## Chmod Number System

| Number | Permission |
|--------|------------|
| 7 | rwx |
| 6 | rw- |
| 5 | r-x |
| 4 | r-- |
| 0 | --- |

---

## Common Commands

- `ls -l` — View permissions
- `chmod 755 file` — rwxr-xr-x
- `chmod 644 file` — rw-r--r--
- `chmod u+x file` — Add execute for user
- `whoami` — Current user
- `id` — User and group info

---

## Why This Matters in Cybersecurity

Misconfigured permissions can allow hackers to:

- Execute malicious scripts
- Read sensitive files
- Escalate privileges

---

**Day 22 Complete**


# Day 23: Web Application Security — OWASP Top 10

**Date:** August 25, 2026

---

## OWASP Top 10 (2021)

1. Broken Access Control
2. Cryptographic Failures
3. Injection (SQL, NoSQL, OS)
4. Insecure Design
5. Security Misconfiguration
6. Vulnerable Components
7. Identification Failures
8. Software/Data Integrity
9. Security Logging Failures
10. Server-Side Request Forgery

---

## SQL Injection (SQLi)

- Hackers inject malicious SQL queries
- Can steal databases, bypass logins
- Example: `' OR '1'='1`

---

## Cross-Site Scripting (XSS)

- Hackers inject malicious JavaScript
- Can steal cookies, hijack sessions
- Example: `<script>alert('XSS')</script>`

---

## Key Takeaway

> *"Web security is the #1 skill for bug bounty and employment. Learn it. Practice it. Master it."*

---

**Day 23 Complete**


# Day 24: Cross-Site Scripting (XSS)

**Date:** August 26, 2026

---

## What is XSS?

Hackers inject malicious JavaScript into websites.

---

## 3 Types of XSS

1. Reflected XSS — Script in URL
2. Stored XSS — Script saved on website
3. DOM-based XSS — Script runs in browser

---

## What Hackers Can Do

- Steal cookies
- Log keystrokes
- Phish users
- Deface websites
- Redirect to malicious sites

---

## Real Example: MySpace (2005)

- 1 million users infected in 24 hours
- Platform had to shut down

---

## How to Defend

- Input validation
- Output encoding
- Content Security Policy (CSP)
- Use secure frameworks

---

## Key Takeaway

> *"XSS is everywhere. Always validate and encode user input."*

---

**Day 24 Complete**



# Day 25: Broken Authentication

**Date:** August 27, 2026

---

## What is Broken Authentication?

Weak login systems that allow hackers to bypass passwords.

---

## Common Attacks

- Brute Force
- Credential Stuffing
- Session Hijacking
- Weak Password Reset
- No MFA

---

## Real Example: Uber (2022)

- Hacker used leaked password
- No MFA on employee account
- $100+ million damage

---

## Defenses

- MFA
- Rate Limiting
- Strong Passwords
- Session Expiry
- Secure Password Reset

---

## Key Takeaway

> *"Passwords are not enough. MFA is mandatory."*

also built a password simulator via replit

https://1feb1801-773a-4293-aa60-4932fb2156cf-00-3tzlqlykx8hyx.worf.replit.dev/

Using unlimited attempts options and rate limits 
---

**Day 25 Complete**


# Day 26: Security Misconfigurations

**Date:** August 28, 2026

---

## What Are They?

Systems set up carelessly — leaving doors open for hackers.

---

## Common Misconfigurations

- Default Credentials (admin/admin)
- Open Ports (22, 3306)
- Public Cloud Storage (S3 buckets)
- Verbose Error Messages
- Unpatched Software
- Directory Listing

---

## Real Example: Capital One (2019)

- Misconfigured S3 bucket → public
- 100 million records exposed
- $80 million fine

---

## Defenses

- Change default passwords
- Close unnecessary ports
- Private cloud storage
- Hide error details
- Patch regularly
- Automated scanning

---

## Key Takeaway

> *"Most breaches happen because of lazy defaults. Change them."*

---

**Day 26 Complete**

# Day 27: Vulnerable & Outdated Components

**Date:** August 29, 2026

---

## My Read on This

Honestly, this is one of those "it's so simple it's stupid" vulnerabilities. Like, why do we need a whole category for this? But then I remember Log4j, and I see why it's here.

Hackers don't invent new ways to break in—they just look for stuff you forgot to patch. It's like trying to rob a house and finding the back door open cos the owner forgot to close it.

---

## The Log4j Meltdown

I remember reading about this one. A logging library. A LIBRARY. And it took down half the internet. People don't realize how deep these dependencies go.

- **Core issue:** Remote Code Execution
- **Affected:** Basically everything running Java
- **Fix:** Update one file. But the problem was *finding* where it was buried.

That's the real challenge—knowing what you have before you can secure it.

---

## My Crypto Take

I'm looking at crypto exchanges and DeFi protocols now. They use so many third-party services. If one of those services has an outdated dependency, the entire pool of funds is at risk.

**Takeaway:** Do your own research. Is the protocol you're using still actively maintained? If the code base looks dead, stay away.

---

## Quick Activity (I did this today)

I checked the Wordpress version on a random blog I visit. They were running an old version. I'm not interested in hacking them—I sent them a message to update their stuff. Security is a shared responsibility.

---

## My Golden Rule

> *"If you're not updating it, you're accepting the risk."*

---

**Day 27 Complete**


# Day 28: Security Logging & Monitoring Failures

**Date:** August 30, 2026

---

## My Take on This

I think this is underrated. Everyone's obsessed with stopping the attack, but nobody talks about what happens when the attack succeeds (and let's be real—it will).

If you don't have logs, you don't have a crime scene. You're just guessing.

---

## Why It Hit Me

I was thinking about the Colonial Pipeline hack. The hackers got in because of a weak password. But the company didn't even notice the unusual login until the ransomware screen popped up.

That's a logging failure.

---

## The Crypto Angle

For me, I'm looking at exchanges and DeFi protocols now. If a protocol doesn't log admin actions or withdrawal requests, you won't know if it's compromised until the TVL drops to zero.

**Red flag:** A project that doesn't have a public security audit or a transparent bug bounty program.

---

## What I Did Today

I wrote a simple Python script in Replit to simulate a log file. It flagged three failed logins in a row as a potential brute force.

It was a basic simulation—but it showed me what a real SOC analyst sees every day.

---

## My Philosophy

> *"You can't stop every attack. But you can always spot it if you're watching."*

---

**Day 28 Complete**