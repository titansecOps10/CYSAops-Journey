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