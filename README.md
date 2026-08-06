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