# Week 4 Assignment: Security Log Simulator

**Date:** August 30, 2026  
**Type:** Practical Project (AI-Assisted Development)  
**Tool:** Replit + Python

---

## 📋 Project Overview

I built a **Security Log Simulator** — a command-line tool that mimics real-world security logs and detects threats.

**Why this matters:** SOC analysts spend their days reading logs. This tool simulates that experience and teaches you to spot anomalies.

---

## 🔧 Features I Built

| Feature | What It Does |
|---------|--------------|
| **Real-time log simulation** | Generates timestamped security events |
| **Threat detection** | Flags brute-force attempts (3+ failed logins) |
| **Multiple log levels** | INFO, WARN, ERROR, ALERT |
| **Export to JSON/CSV** | Output logs in machine-readable formats |
| **Search & filter** | Search by keyword or log level |
| **Command-line flags** | Run with different options |

---

## 🧪 Example Commands

```bash
# Basic run
python3 security_log_simulator.py

# Export as JSON
python3 security_log_simulator.py --format json

# Load from a log file
python3 security_log_simulator.py --log-file events.json

# Search for specific events
python3 security_log_simulator.py --search admin

# Filter by log level
python3 security_log_simulator.py --level WARN

https://639c5b82-bb4e-4a58-b71f-77c1f67c9586-00-lknb89pkqiu.worf.replit.dev/


[19:45:32] [INFO] User 'Victory' logged in from IP 192.168.1.5
[19:45:33] [WARN] Failed login attempt for 'admin' from IP 10.0.0.22
[19:45:34] [WARN] Failed login attempt for 'admin' from IP 10.0.0.22
[19:45:35] [WARN] Failed login attempt for 'admin' from IP 10.0.0.22
[19:45:36] [ALERT] Brute force detected! Account 'admin' locked out.

📊 Summary: 3 failed attempts for 'admin'
🚨 ALERT: Brute force pattern detected!