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




# Day 29: Server-Side Request Forgery (SSRF)

**Date:** August 31, 2026

---

## What Is SSRF?

Hackers trick a server into making requests to places it shouldn't.

---

## What Hackers Can Do

- Access internal services (databases, admin panels)
- Bypass firewalls
- Read local files (`file:///etc/passwd`)
- Port scan internal networks
- Access cloud metadata (`169.254.169.254`)

---

## Real Example: Capital One (2019)

- SSRF vulnerability allowed access to AWS metadata service
- IAM credentials were stolen
- 100 million records exposed

---

## How to Defend

- Allowlist trusted domains
- Block internal IP ranges
- Validate all user input
- Use a proxy to filter dangerous requests

---

## My Golden Rule

> *"If your server makes requests based on user input, assume it's vulnerable until proven otherwise."*

---

**Day 29 Complete**

# Day 30: Insecure Design — OWASP #4

**Date:** September 1, 2026

---

## My Read on This

I get why this is a separate category now. It’s not about one missing piece—it’s about the whole picture being built wrong.

Some bugs you can fix with a patch. But if the design itself is flawed, you're just putting band-aids on a broken bone.

---

## The Twitter API Leak

This one stuck with me. They didn't plan for a scenario where someone would go poking around the authentication system. But hackers did.

250 million dollar fine. That's what insecure design costs.

---

## The Crypto Take

Now I’m thinking about DeFi protocols. If a protocol’s smart contract is designed without proper access controls, you can't just fix it with a patch—you have to rewrite the whole thing.

That's why audits matter so much.

---

## My Golden Rule

> *"If the design is bad, the code will always be insecure no matter how many patches you add."*

---

**Day 30 Complete**



# Day 31: IDOR Practical — Burp Suite

**Date:** September 2, 2026

---

## What I Did

- Accessed the PortSwigger IDOR lab
- Logged in as `wiener`
- Used Burp Suite to intercept the request
- Changed `id=wiener` to `id=carlos`
- The server returned Carlos's data

---

## What I Learned

- IDOR is when the server trusts user-supplied IDs
- It's a type of Broken Access Control (OWASP #1)
- Burp Suite makes it easy to find

---

## Key Takeaway

> *"Never trust user input — even for IDs."*

---

**Day 31 Complete**




# Day 32: Cryptographic Failures — OWASP #2

**Date:** September 3, 2026

---

## What I Learned

Cryptographic failures happen when encryption is weak, missing, or misconfigured.

---

## Real Example: Equifax (2017)

- Unencrypted customer data
- 147 million records exposed
- $700 million settlement

---

## Common Failures

- HTTP instead of HTTPS
- Weak hashing (MD5, SHA1)
- Hardcoded keys
- No encryption at rest

---

## How to Defend

- HTTPS everywhere
- Strong hashing (bcrypt, Argon2)
- Store keys in vaults
- Encrypt data at rest

---

## My Golden Rule

> *"If it's sensitive, encrypt it. If you're not sure, encrypt it anyway."*

---

**Day 32 Complete**



# TitanSEC — Day 33: Software Supply Chain Failures

**Date:** September 4, 2026  
**Topic:** OWASP Top 10:2025 — A03 Software Supply Chain Failures  
**Mode:** Theory + Adversarial Analysis  
**Lab:** None — VPS unavailable

---

## What I Learned

- Software supply chain = the ecosystem/process used to build, distribute and update software
- Direct dependency = explicitly used by the project
- Transitive dependency = brought in indirectly by another dependency
- Dependency confusion = manipulating package resolution to select a malicious package
- Typosquatting = deceptive misspelled/look-alike package names
- Vulnerable dependency = legitimate software with a security weakness
- Malicious dependency = intentionally malicious or compromised software
- CI/CD is security-sensitive because it builds, releases, and deploys software
- SBOM = Software Bill of Materials — an inventory of components
- Hash = cryptographic fingerprint, not encryption
- Digital signature = private key mechanism verified with a public key
- Software provenance = where an artifact came from and how it was produced
- Developer workstations can be supply-chain boundaries
- Separation of duties prevents one identity from having unrestricted control
- Supply-chain evidence includes Git history, CI/CD logs, SBOMs, and cloud audit logs

## Key Takeaway

The application is not the only attack surface. The systems, dependencies and processes used to build and deliver software can also become the attack path.

## Lab Status

No lab completed because the Windows VPS was temporarily unavailable. Theory and adversarial analysis were completed instead. All attack scenarios are theoretical and restricted to authorized security research/training.

# Day 34 — OWASP Top 10:2025 A08: Software or Data Integrity Failures

## What I Learned
Integrity means ensuring software, code, and data remain accurate, trusted, and protected from unauthorized modification.

Key distinction:
- Confidentiality = who can SEE the data?
- Integrity = who can CHANGE the data?
- Availability = can the system/data be USED?

A08:2025 focuses on situations where software or data is treated as trusted without properly verifying its integrity. This includes CI/CD pipelines, software updates, libraries/plugins, artifacts, serialized data, and critical application data.

## Important Concepts
- A hash such as SHA-256 can detect whether something changed, but a hash alone does not prove who created it.
- Digital signatures can help verify both integrity and the expected source of software/data.
- A compromised CI/CD pipeline can modify an otherwise legitimate build and produce a malicious artifact.
- Automatic updates can become dangerous when update packages are not properly verified.
- Untrusted libraries, plugins, repositories, or artifacts can introduce malicious code.
- Insecure deserialization occurs when untrusted serialized data is accepted and reconstructed without sufficient validation/integrity protection.
- Data integrity can be compromised when attackers modify things such as account balances, transactions, permissions, or records.

## Attack Chain
Developer → Build → Artifact → Registry → Production

Integrity can be attacked at multiple points in this chain.

## Investigation Evidence
Useful evidence includes:
- File hashes
- Digital signatures
- Git history
- CI/CD logs
- Build artifacts
- Registry logs
- Deployment records
- Database audit logs
- API/access logs

Key investigation questions:
1. What should exist?
2. What exists now?
3. What changed?
4. When did it change?
5. Who or what changed it?
6. How did the modified item reach production?

## My Knowledge Check Corrections
- Integrity is NOT keeping information secret; that is confidentiality.
- Brute forcing primarily targets authentication, not integrity.
- Sharing data with third parties without authorization is primarily a confidentiality/privacy issue.
- Digital signatures are not about revealing device information; they provide cryptographic verification of integrity and signer authenticity.
- Automatic updates must verify that the update came from the expected source and was not modified.
- A compromised build pipeline can alter software even when the original source code is clean.

## Attack Angle
When analyzing an integrity failure, ask:
WHO can modify it?
WHAT can be modified?
WHERE is the trust boundary?
HOW is integrity verified?
WHAT evidence proves the modification?

## Source
OWASP Top 10:2025 — A08: Software or Data Integrity Failures


# Day 35 — OWASP Top 10:2025 A10: Mishandling of Exceptional Conditions

## What I Learned
A10 is about how an application behaves when something unexpected happens.

An exceptional condition can include:
- Authentication/authorization failures
- Invalid or unexpected input
- Database/network failures
- Transaction failures
- Resource exhaustion
- Unexpected application states

The security issue is not simply that an error happened. The important question is how the application handles the error.

## Fail Open vs Fail Closed

Fail Open:
A security check fails but the system still allows access.

Example:
Authorization cannot be verified → application grants access.

Fail Closed:
A security check fails and access is denied.

Security principle:
If authorization cannot be verified, deny access.

## Error Information Leakage
Detailed errors can expose useful information to attackers, such as:
- Database technology/version
- Internal hostnames/IPs
- File paths
- SQL queries
- Stack traces
- Application/framework information

A safer approach is to show the user a generic error while keeping detailed technical information in internal logs.

Example:

User:
"Something went wrong. Please try again."

Security/Development logs:
Detailed error, timestamp, affected service, request/transaction ID and relevant diagnostic information.

## Transaction Failures
If an operation completes only partially, the application can leave inconsistent data.

Example:
Debit account → succeeds
Credit receiver → fails

A secure implementation may need a rollback so the incomplete transaction does not leave corrupted or inconsistent state.

## Resource Exhaustion
Poor exception handling can leave resources such as memory, connections, files, or locks unreleased.

Repeatedly triggering the condition can eventually exhaust resources and cause a denial of service.

## Attack Perspective
When I encounter an application error, I should ask:

1. Does it fail open or fail closed?
2. Does it reveal sensitive technical information?
3. Does it leave corrupted or partial state?
4. Are resources properly released?
5. Can the error be repeatedly triggered?
6. Does the application recover safely?
7. What evidence is recorded for defenders?

## My Knowledge Check Corrections

I initially understood an exceptional condition mainly as an authentication situation where a new device/location is allowed through without proper verification.

Correction:
An exceptional condition is much broader. It is any unexpected situation the application must handle.

I correctly understood that:
- Fail-open authentication/authorization can allow unauthorized access.
- Authorization should fail closed when verification is unavailable.
- Detailed technical errors can help attackers with reconnaissance.
- Developers/security teams still need detailed internal logs.
- Rollback can undo an incomplete/failed transaction.

I needed to improve my understanding of:
- Partial transaction failures
- Resource exhaustion caused by poor exception handling
- Exceptional conditions occurring outside authentication

## Personal Mental Model

Unexpected Condition
        ↓
Error Handling
        ↓
Application State
        ↓
Recovery

At every stage I should ask whether the failure creates a security problem.

## Attack Angle

An attacker does not always need to "break" the application directly.

They can intentionally create unexpected situations and observe how the application reacts.

The error response itself can become an attack surface.

## Key Takeaway

The main lesson from A10:

"Don't only test what happens when everything works. Test what happens when things go wrong."

A secure system should fail safely, protect its state, avoid unnecessary information leakage, release resources properly, and leave useful evidence for defenders.

## Source
OWASP Top 10:2025 — A10: Mishandling of Exceptional Conditions



# Day 36 — OWASP Top 10:2025 A01: Broken Access Control

## What I Learned
Authentication = Who are you?
Authorization = What are you allowed to access/do?

Broken Access Control happens when a user can access data or perform actions they should not be authorized to perform.

## Example
User A:
`/profile/100`

Changes the ID to:
`/profile/101`

If User A can now access User B's information, this may be an access-control vulnerability.

## Common Attack Areas
- Accessing another user's data
- Accessing admin functionality as a normal user
- Changing IDs in URLs or API requests
- Bypassing authorization checks
- Performing actions after privileges have been removed

## Security Mindset
For every protected resource, ask:

WHO is making the request?
WHAT are they allowed to do?
WHAT happens if they change the request?
IS authorization actually enforced?

## Key Takeaway
Authentication proves identity.

Authorization controls permissions.

Broken Access Control occurs when those permissions can be bypassed or are incorrectly enforced.


# Day 37 — OWASP A01: Broken Access Control
## Practical: IDOR / BOLA Demonstration

### Objective
Demonstrate how missing object-level authorization allows one authenticated user to access another user's resource.

### Practical
Built a deliberately vulnerable API lab on Replit with fictional users and orders.

Tested object ID:
`201`

### Result

Vulnerable endpoint:
`GET /api/orders/:id`

Result:
`200 OK`

Returned:
- Order ID: 201
- Owner: Bob
- Item: Secure Coding Workshop
- Amount: $42.00

The application returned Bob's order because the vulnerable endpoint did not perform an ownership check.

### Secure Endpoint

`GET /api/secure/orders/:id`

Result:
`403 Forbidden`

The secure version correctly enforced ownership authorization.

### What I Demonstrated

Authentication alone is not enough.

The application must also verify:

`Is this authenticated user authorized to access THIS object?`

Changing an object ID from one user's resource to another can expose unauthorized data when that check is missing.

### Vulnerability
**BOLA — Broken Object Level Authorization**

Also commonly demonstrated as:
**IDOR — Insecure Direct Object Reference**

### Evidence
Replit lab screenshots show:
- Vulnerable endpoint → `200 OK` → Bob's order exposed
- Secure endpoint → `403 Forbidden` → access correctly denied

### Security Fix
Perform an ownership/authorization check on every object-level request before returning or modifying the resource.

### Lab
Replit demo:
https://2732b00c-2a01-4e68-a34b-a0abd23aee44-00-1nl0puzt2pjur.worf.replit.dev/


# Day 38 — OWASP A01: Broken Access Control — BFLA

## Topic
Broken Function Level Authorization (BFLA)

## What I learned
BFLA occurs when an application/API allows a user to access or execute a function that their role or permissions should not allow.

Authentication answers:
"Who are you?"

Authorization answers:
"What are you allowed to do?"

A user can be properly authenticated but still be unauthorized to execute privileged functions.

Example:

Normal user → GET /api/profile       → ALLOWED
Normal user → GET /api/admin/logs    → SHOULD BE DENIED
Normal user → DELETE /api/users/2    → SHOULD BE DENIED

## BOLA vs BFLA

BOLA:
Tests access to a specific object/resource that the user should not access.

Example:
User A changes:
GET /api/orders/101
to:
GET /api/orders/201

BFLA:
Tests whether a user can execute a function/action reserved for another privilege level.

Example:
A normal user directly calls:
DELETE /api/users/2
or:
GET /api/admin/logs

## Lab Status

Planned a controlled Node.js/Express BFLA lab with:

- Alice = normal user
- Admin = administrator
- Normal profile endpoint
- Admin logs endpoint
- User deletion function

The vulnerable design intentionally included authentication without the required role/permission checks.

The lab could not be executed today because I reached my Replit usage limit.

No exploitation evidence was claimed because the vulnerable operation was not actually run.

## Expected Vulnerability

If Alice, authenticated only as a normal user, can successfully execute an administrative function and receives a successful response such as HTTP 200, that would demonstrate broken function-level authorization.

A properly protected privileged function should reject Alice's request, typically with HTTP 403 Forbidden when she is authenticated but lacks the required permission.

## Security Lesson

Hiding an admin button in the frontend is not authorization.

The server/API must enforce the permission.

Function-level access should be explicitly restricted to users with the required permissions and least privilege should be applied.

## Attack Angle

Trust boundary:
Normal user → privileged function

Question:
"Does the server actually verify my privilege before executing this function?"

Potential attack paths:
- Directly requesting admin endpoints
- Force browsing hidden functions
- Changing HTTP methods
- Testing privileged endpoints with lower-privilege credentials
- Looking for inconsistent authorization between endpoints

## Lab Evidence

Status: NOT EXECUTED TODAY

Reason:
Replit usage limit reached.

Next step:
Resume the controlled BFLA lab when the environment is available, then capture:
1. Normal-user request
2. Vulnerable response
3. Authorization failure
4. Secure response after the fix
5. Retest evidence

## Reference

OWASP API Security Top 10:2023
API5: Broken Function Level Authorization

OWASP Web Security Testing Guide:
WSTG-APIT-04


# Day 38 — OWASP A01 Broken Access Control — BFLA

## Topic
Broken Function Level Authorization (BFLA)

## What I learned

BFLA occurs when an application/API allows a user to execute a function or operation that their role or permissions should not allow.

Authentication answers:
"Who are you?"

Authorization answers:
"What are you allowed to do?"

A user can be properly authenticated while still being unauthorized to execute privileged functions.

Example:

Normal user → GET /api/profile       → ALLOWED
Normal user → GET /api/admin/logs    → SHOULD BE DENIED
Normal user → DELETE /api/users/2    → SHOULD BE DENIED

## BOLA vs BFLA

BOLA:
"Which object can I access?"

Example:
Changing:

GET /api/orders/101

to:

GET /api/orders/201

to access another user's object.

BFLA:
"Which function/action can I perform?"

Example:
A normal user directly calls:

GET /api/admin/logs

or:

DELETE /api/users/2

when those functions are restricted to administrators.

Important distinction:
BOLA focuses on unauthorized access to a specific object.
BFLA focuses on unauthorized execution of a function or operation.

## Knowledge Check

1. A normal user receiving a successful response from an admin-only endpoint is an authorization failure.

2. Hiding an admin button in the frontend is not authorization because the user can still construct the request directly.

3. A DELETE operation involving a specific object can involve BOLA, but when the security question is whether the user is allowed to execute the privileged DELETE function, the focus is BFLA.

4. A server-side role check such as:

if (req.user.role !== "admin") {
    return 403;
}

is enforcing authorization.

5. Different authorization results for different HTTP methods can indicate inconsistent function-level authorization.

Example:

GET /api/admin/reports     → 403
POST /api/admin/reports    → 403
DELETE /api/admin/reports  → 200

This suggests that authorization may be enforced inconsistently between methods/endpoints.

## Attack Angle

Instead of only asking:

"Is /admin protected?"

Ask:

"What function is this endpoint exposing, and where does the server verify that my identity is allowed to execute it?"

Potential tests include:

- Directly requesting privileged endpoints
- Force browsing hidden functions
- Testing lower-privileged credentials against admin functions
- Trying alternative HTTP methods
- Looking for inconsistent authorization between endpoints
- Comparing behavior between user and admin accounts

## Lab Status

The planned Node.js/Express BFLA lab could not be executed because my Replit usage limit was reached.

No exploitation evidence was claimed.

The lab will be resumed when the environment becomes available.

Planned evidence:

1. Normal-user request
2. Privileged function request
3. Vulnerable response
4. Authorization fix
5. 403 response after fix
6. Retest evidence

## Security Lesson

Frontend restrictions are not security boundaries.

Authorization must be enforced server-side.

Privileged functions should use explicit permission checks, least privilege, and consistent access-control enforcement.

## Current Status

Theory: COMPLETE
Knowledge check: COMPLETE
Adversarial reasoning: COMPLETE
Practical lab: PENDING

Next:
Execute the controlled BFLA lab → exploit → observe → fix → retest → document.



# Day 39 — Broken Object Property Level Authorization

## Topic
OWASP A01 — Broken Access Control
Focus: Broken Object Property Level Authorization (BOPLA)

## What I learned

Property-level authorization asks two separate questions:

1. Can the user READ a particular property?
2. Can the user MODIFY a particular property?

A user may be authorized to modify their email address but not privileged properties such as:
- role
- account balance
- permissions
- discount
- access level

The vulnerability occurs when the server accepts properties that the authenticated user should not be allowed to control.

## Mass Assignment

Mass assignment occurs when an application automatically maps client-supplied parameters to an internal object without properly restricting which properties the user is allowed to modify.

Example:

Normal request:
{
  "email": "user@example.com"
}

Potentially dangerous request:
{
  "email": "user@example.com",
  "role": "admin"
}

The problem is not that the user can see the "role" property.

The problem is that the server may allow the user to CONTROL a privileged property they should not be authorized to modify.

## Read vs Write

READ:
"Am I allowed to see this property?"

WRITE:
"Am I allowed to change this property?"

These must be considered separately.

## Practical Lab

PortSwigger Web Security Academy:
"Exploiting a mass assignment vulnerability"

Lab target:
Lightweight "l33t" Leather Jacket

Planned investigation:
- Inspect API requests.
- Compare GET and POST responses.
- Identify hidden parameters.
- Test whether the hidden property is accepted.
- Determine whether the server processes the property.
- Exploit the property-level authorization weakness.
- Document evidence and the security impact.

## Current Status

LAB NOT COMPLETED.

PortSwigger lab was opened successfully, and the Leather Jacket was added to the basket.

Burp Suite is not currently installed.
VPS access is temporarily unavailable because the VPS subscription has not yet been renewed.

Therefore, no exploit evidence or successful lab completion is claimed.

## Key Takeaway

Authentication does not automatically mean a user is authorized to control every property associated with their account.

The server must explicitly enforce which properties each user is allowed to read or modify.

## Next Step

When VPS access is restored:
1. Install Burp Suite Community Edition.
2. Capture the PortSwigger lab traffic.
3. Investigate the /api/checkout requests.
4. Identify the hidden property.
5. Test it in Repeater.
6. Complete the lab.
7. Record the HTTP evidence and final result.

## Attack Angle

Ask:

"What properties does the client control that the server should control?"

This is the core question for property-level authorization and mass assignment.


# Day 39 — Broken Object Property Level Authorization

## Topic
OWASP A01 — Broken Access Control
Focus: Broken Object Property Level Authorization (BOPLA)

## Core Concept

Property-level authorization asks:

1. What properties can a user READ?
2. What properties can a user MODIFY?

Being authorized to modify one property does not mean the user is authorized to modify every property.

Example:

Allowed:
email → change ✅

Not allowed:
role → change ❌
balance → change ❌
permissions → change ❌

If the server allows a normal user to modify a privileged property, this can become a property-level authorization vulnerability.

## Mass Assignment

Mass assignment occurs when an application automatically maps
client-supplied parameters to internal object properties without
properly restricting which properties the user is allowed to control.

Example:

Normal request:

{
  "email": "user@example.com"
}

Potentially dangerous request:

{
  "email": "user@example.com",
  "role": "admin"
}

The problem is not simply that the property exists.

The problem is that the server allows the client to control a
property that should be protected.

## Read vs Write

READ:
"Am I allowed to see this property?"

WRITE:
"Am I allowed to change this property?"

These are separate authorization decisions.

## Today's Practical Lab

Platform:
PortSwigger Web Security Academy

Lab:
"Exploiting a mass assignment vulnerability"

Target:
Lightweight "l33t" Leather Jacket

Objective:
Identify a hidden API property and determine whether the server
allows the client to control it.

## Current Status

Lab opened successfully.

Leather Jacket added to the basket.

Lab is NOT completed yet.

Burp Suite is not currently available because VPS access has not
yet been renewed.

No exploit or successful completion is claimed.

## Key Takeaway

Authentication answers:

"Who are you?"

Authorization answers:

"What are you allowed to do?"

Property-level authorization asks:

"Which specific properties are you allowed to read or change?"

## Attack Angle

When examining an API, ask:

"What properties does the client control that should actually be
controlled by the server?"

## Next Practical Step

When Burp/VPS access is available:

1. Capture the checkout requests.
2. Compare GET and POST responses.
3. Identify the hidden property.
4. Test whether the server accepts it.
5. Observe the response.
6. Complete the lab.
7. Document the evidence and remediation.

## Progress

Day 39 — THEORY COMPLETE
Practical lab — PENDING

BOLA → Object
BFLA → Function
BOPLA → Property

Day 40, Unprotected Admin Functionality. assignment done in weekly assignments section


# Day 41 — Sessions, JWT & Authentication

## Focus
Authentication, sessions, cookies, JWT, and MFA bypass concepts.

## Curriculum Alignment
Week 14 — Sessions, JWT & Authentication
- Theory: Sessions, cookies, JWT, OAuth/OIDC fundamentals
- Hands-on: Build vulnerable authentication system
- Adversarial challenge: Controlled token/session abuse
- Expected evidence: Token lifecycle evidence
- GitHub: Auth Lab
- Difficulty: 4/5
- Skills: Authentication

Source: TITANSEC 12-Month Security Engineering Apprenticeship
[Curriculum source: Week 14]

## Theory Learned

### Authentication
Authentication answers:

"Who are you?"

Examples:
- Username + password
- MFA
- Passkeys
- Certificates
- OAuth/OIDC authentication

### Authorization
Authorization answers:

"What are you allowed to do?"

Authentication and authorization are separate security controls.

### Session
A session represents an authenticated user's state across multiple HTTP requests.

A typical flow:

1. User submits credentials.
2. Server verifies credentials.
3. Server creates an authenticated session.
4. Browser receives a session identifier, commonly through a cookie.
5. Browser sends the session identifier with subsequent requests.
6. Server uses it to determine the authenticated user.

### Cookies
Cookies can store session identifiers in the browser.

Important security attributes include:

- Secure — cookie should only be sent over HTTPS.
- HttpOnly — JavaScript cannot directly access the cookie.
- SameSite — controls cross-site cookie sending behavior.

### JWT
JSON Web Token (JWT) is a token format commonly used to carry claims.

Typical structure:

HEADER.PAYLOAD.SIGNATURE

The payload may contain claims such as:
- user identity
- issuer
- expiration
- roles/scopes

JWT payload data is encoded, not automatically encrypted.

Security depends on correct validation of:
- signature
- algorithm
- issuer
- audience
- expiration
- required claims

## Practical Lab Attempt

Platform:
PortSwigger Web Security Academy

Lab:
2FA Simple Bypass

Credentials supplied by the authorized training lab:
- wiener:peter
- carlos:montoya

### Completed

Successfully authenticated as `wiener` through the normal 2FA flow.

Observed:
- Login
- 2FA verification
- My Account page

### Attack Attempt

Logged in as Carlos and reached the 2FA stage.

The intended test was to attempt direct navigation to:

`/my-account`

without completing the second authentication factor.

### Result

The lab instance repeatedly returned:

`Server Error: Gateway Timeout (0)`

The expected Carlos account page did not load.

Therefore:

- 2FA bypass: NOT VERIFIED
- Lab solved: NO
- Exploit success: NOT CLAIMED
- Evidence: Gateway Timeout only
- Lab status: PENDING REVISIT

## Security Lesson

A 2FA bypass can occur when an application establishes an authenticated state after the first authentication step but fails to properly enforce completion of the second factor before granting access to protected resources.

The important security boundary is therefore:

Password authentication
        ↓
Second-factor verification
        ↓
Authenticated session
        ↓
Protected resources

The application must not allow the user to skip the second-factor verification and reach protected resources.

## Attack Surface

Future testing should examine:

- Session creation before MFA completion
- Session state transitions
- Direct access to authenticated endpoints
- MFA verification enforcement
- Session invalidation
- Session fixation
- Session expiration
- Cookie security
- JWT validation
- Token lifetime
- Authentication/authorization boundary

## Evidence Status

Normal authentication flow: COMPLETE

2FA bypass attempt: ATTEMPTED

Successful bypass evidence: NOT AVAILABLE

Lab infrastructure response: GATEWAY TIMEOUT

## Revisit Plan

Sunday:
1. Reopen the 2FA Simple Bypass lab.
2. Repeat the test against a fresh lab instance.
3. Capture the complete request/response flow.
4. Confirm whether `/my-account` is accessible before 2FA completion.
5. Document the actual result.
6. Continue into session/JWT testing if the environment works.

## Key Terms

Authentication — Verifying a user's identity.

Authorization — Determining what an authenticated user is permitted to access or perform.

MFA — Multi-Factor Authentication; authentication using multiple independent factors.

2FA — Two-Factor Authentication; a form of MFA using two authentication factors.

Session — Server/application state representing an authenticated user's interaction.

Session ID — Identifier used to associate requests with a user's session.

Cookie — Browser-stored data that can be used to maintain session state.

JWT — JSON Web Token; a compact token format containing claims.

Claim — A piece of information/assertion contained in a token.

OAuth — Authorization framework commonly used for delegated access.

OIDC — OpenID Connect; an authentication layer built on OAuth 2.0.

## Day 41 Status

THEORY: COMPLETE
PRACTICAL: ATTEMPTED
EXPLOIT: NOT VERIFIED
LAB: PENDING
DOCUMENTATION: COMPLETE

No false exploit claim made.



# Day 42 — Session Security & Authentication State

## Focus

Understanding the lifecycle of authenticated sessions and identifying security boundaries between login, MFA, session management, authorization, and logout.

## Curriculum Alignment

Week 14 — Sessions, JWT & Authentication

Curriculum requirements:
- Sessions
- Cookies
- JWT
- OAuth/OIDC fundamentals
- Controlled token/session abuse
- Token lifecycle evidence

Source:
TITANSEC 12-Month Security Engineering Apprenticeship — Week 14

## Core Concept

Authentication is not a single event.

A secure application moves through multiple security states:

LOGIN
  ↓
PASSWORD VERIFICATION
  ↓
MFA
  ↓
SESSION CREATION
  ↓
SESSION VALIDATION
  ↓
AUTHORIZATION
  ↓
RESOURCE ACCESS
  ↓
PASSWORD / MFA CHANGES
  ↓
LOGOUT
  ↓
SESSION INVALIDATION
  ↓
SESSION EXPIRATION

Each transition represents a potential security boundary.

## Authentication

Authentication answers:

"Who are you?"

Examples:
- Password authentication
- MFA
- Passkeys
- Certificates
- Federated authentication

A failure in credential verification is an authentication failure.

## MFA

Multi-Factor Authentication adds another authentication factor after the initial credential verification.

Expected security model:

Password ✓
    ↓
MFA ✓
    ↓
Fully authenticated session
    ↓
Protected resources

If an application allows protected resources to be accessed before MFA completion, the authentication boundary may be broken.

This connects directly to the Day 41 PortSwigger 2FA Simple Bypass lab attempt.

## Session

A session represents authenticated state between the client and application.

After successful authentication, the server may issue a session identifier.

Conceptual flow:

Browser
  ↓
Session identifier
  ↓
Server
  ↓
Authenticated identity

The password normally does not need to be submitted with every request.

Instead, the application uses the session credential to associate subsequent requests with the authenticated user.

## Cookies

Cookies are commonly used to transport session identifiers between the browser and web application.

Important cookie security attributes include:

- Secure
- HttpOnly
- SameSite

A browser tab does NOT necessarily represent a separate session.

Multiple tabs for the same website can share the browser profile's cookies and therefore share authentication state.

Closing a tab is therefore not equivalent to logging out.

## Session Security Attack Surface

### Session Creation

Questions:

- When is the authenticated session created?
- Is it created before or after MFA?
- Is the session identifier regenerated after authentication?
- Does authentication state correctly reflect MFA completion?

### Session Validation

Questions:

- Does the server validate the session on every protected request?
- Does the session correspond to the correct user?
- Can an expired or invalidated session still access protected resources?

### Session Fixation

A session fixation vulnerability can occur when an attacker can cause a victim to authenticate using a session identifier known to the attacker.

Security principle:

Regenerate session identifiers when authentication or privilege state changes.

### Session Termination

Logout should cause appropriate server-side invalidation of the authenticated session.

Security question:

Does the old session remain usable after logout?

### Session Expiration

Security questions:

- What happens after inactivity?
- What happens after long periods?
- Can stale sessions remain valid indefinitely?
- Are sensitive actions capable of triggering reauthentication?

## Authorization

Authorization answers:

"What is this authenticated user allowed to do?"

Example:

USER
  ↓
GET /my-account → ALLOW

USER
  ↓
GET /admin → DENY

Authorization failures include:
- IDOR/BOLA
- BFLA
- Property-level authorization failures
- Privilege escalation

Authorization must be enforced server-side.

## Browser Session Observation

A browser can maintain authentication state even after a specific tab is closed.

Conceptually:

Chrome profile
    ↓
Cookie/session storage
    ↓
Authenticated website

Multiple tabs may therefore use the same authentication state.

Security implication:

The security of the device and browser profile becomes part of the security of the authenticated accounts.

An unlocked or compromised device can expose authenticated sessions even when the user is not actively interacting with the website.

## Day 41 Connection

Day 41 studied MFA enforcement using the PortSwigger 2FA Simple Bypass lab.

The intended security boundary was:

Password authentication
    ↓
2FA verification
    ↓
Authenticated session
    ↓
Protected account

The lab attempt was not successfully completed because the PortSwigger lab instance repeatedly returned a Gateway Timeout.

No successful exploit is claimed.

## Day 42 Security Questions

For any authentication system, ask:

1. When does authentication begin?
2. When is authentication considered complete?
3. When is the session created?
4. What proves the session belongs to the correct user?
5. Is MFA enforced before protected resources are available?
6. How is the session validated?
7. How is authorization enforced?
8. What happens when the password changes?
9. What happens when MFA changes?
10. What happens when the user logs out?
11. What happens when the session expires?
12. Can old authentication state remain valid?

## Attack Surface Model

LOGIN
→ Authentication failure

MFA
→ MFA bypass

SESSION CREATION
→ Session fixation / incorrect authentication state

SESSION VALIDATION
→ Session hijacking / invalid session acceptance

AUTHORIZATION
→ IDOR / BOLA / BFLA / privilege escalation

RESOURCE ACCESS
→ Unauthorized access

PASSWORD / MFA CHANGE
→ Stale-session or reauthentication weaknesses

LOGOUT
→ Session invalidation failure

EXPIRATION
→ Excessively long-lived sessions

## Practical Status

Theory: COMPLETE

Session lifecycle understanding: COMPLETE

Browser/session relationship: UNDERSTOOD

Practical exploitation: PENDING

PortSwigger authentication labs: REVISIT SUNDAY

## Key Terms

Authentication — Verifying a user's identity.

Authorization — Determining what an authenticated identity is permitted to access or perform.

MFA — Multi-Factor Authentication.

2FA — Two-Factor Authentication, a type of MFA using two authentication factors.

Session — Authenticated state maintained between a client and application.

Session ID — Identifier associated with an application session.

Cookie — Browser-stored data commonly used to maintain web session state.

Session fixation — Attack involving a session identifier that an attacker can cause a victim to use.

Session invalidation — Making a session credential no longer valid.

Session expiration — Ending a session after a defined lifetime or inactivity period.

JWT — JSON Web Token, a structured token format commonly used to carry claims.

## Evidence

No exploit evidence claimed for Day 42.

Primary evidence:
- Session lifecycle analysis
- Authentication-state model
- Browser/session reasoning
- Security-boundary analysis


# Day 43 — JWT Fundamentals & Trust

## Objective
Understand JWT structure, encoding, signatures, and the security assumptions behind JWT authentication.

## Theory

JWT = JSON Web Token.

A JWT normally has three Base64URL-encoded parts:

HEADER.PAYLOAD.SIGNATURE

Header:
- Defines token metadata and signing algorithm.
- Common fields include `alg` and `typ`.

Payload:
- Contains claims such as user identity, role, expiration, etc.
- The payload is normally encoded, NOT encrypted.
- Anyone who obtains the token can decode the payload.

Signature:
- Provides integrity/authenticity evidence.
- Changing the header or payload normally causes the original signature to become invalid.

Encoding ≠ Encryption:
- Encoding changes representation and is reversible without a secret.
- Encryption provides confidentiality and requires a key.

Valid JWT ≠ Authorized action:
A server can successfully validate a JWT while still denying the requested action.
Example:
valid JWT + role=user + request to /admin → authorization should deny access.

## Practical Activity

Platform: PortSwigger Web Security Academy
Lab: JWT authentication bypass via flawed signature verification

Environment limitation:
Firefox was available, but Burp/VPS was unavailable.

Completed:
- Accessed the PortSwigger JWT material.
- Reviewed JWT structure and trust model.
- Opened the JWT authentication lab.
- Identified the intended authentication flow using `wiener:peter`.
- Reviewed the intended attack path involving JWT manipulation.

Not completed:
- HTTP interception/modification.
- JWT signature manipulation.
- Successful authentication bypass.
- `/admin` access.

No successful exploit is claimed.

## Key Security Lesson

JWT security depends on the server correctly validating the token's integrity AND correctly enforcing authorization.

A JWT should never be trusted merely because it is syntactically valid or decodable.

## Evidence
- PortSwigger JWT documentation
- PortSwigger JWT authentication lab
- Practical lab reconnaissance

## Next Step
When Burp/VPS is available:
capture the authenticated request → inspect JWT → test controlled token manipulation → observe server behavior → document evidence → validate the defense.


# Day 44: API Security — Beyond JWT

Date: September 17, 2026

---

## What I Learned

- APIs are the backbone of modern apps and the #1 attack surface
- JWT is one piece of API security
- OWASP API Top 10 exists separately from the web OWASP Top 10
- BOLA = Broken Object Level Authorization (API version of IDOR)

---

## OWASP API Top 10 (Key Ones)

1. BOLA - Broken Object Level Authorization
2. Broken Authentication
3. Broken Object Property Level Authorization
4. Unrestricted Resource Consumption
5. Broken Function Level Authorization

---

## Practical

- Tested jsonplaceholder.typicode.com API
- Changed IDs in URL to test for BOLA-style flaws

---

## Key Takeaway

> "APIs are where the money moves. Learn to test them."


# Day 45 — JWT Attacks & Signature Verification

## Objective
Understand how flawed JWT signature verification can lead to authentication bypass.

## Theory

JWT security depends on the server correctly validating the token before trusting its claims.

Important distinction:
- Decoding a JWT does not validate it.
- A valid signature does not automatically grant authorization.
- Changing the header or payload normally invalidates the original signature.
- `alg` specifies the cryptographic algorithm used by the JWT.

A dangerous implementation flaw is accepting a JWT without a valid signature. This can allow an attacker to modify claims such as the authenticated username.

## Practical Lab

Platform: PortSwigger Web Security Academy

Lab:
JWT authentication bypass via flawed signature verification

Completed:
- Accessed the lab.
- Authenticated successfully as `wiener:peter`.
- Reached `/my-account`.
- Confirmed the lab environment is functioning.

Limitation:
Firefox Android did not expose the authenticated HTTP request/JWT cookie required for the next stage.

Therefore:
- JWT modification was not performed.
- `/admin` was not accessed.
- The lab was NOT marked as solved.

## Intended Attack Chain

Capture request → extract JWT → modify claims → test signature verification → request `/admin` → validate authorization behavior.

## Key Lesson

The security boundary is not simply:

"Can the application decode this JWT?"

It is:

"Has the application correctly verified the token's integrity, validity, and authorization before trusting its claims?"

## Source
PortSwigger Web Security Academy — JWT attacks and JWT authentication bypass lab.