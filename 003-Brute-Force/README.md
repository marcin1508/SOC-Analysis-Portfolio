# SOC176 - RDP Brute Force Detected

**Platform:** LetsDefend  
**Date:** Jun 09, 2026  
**Severity:** Medium  
**Type:** Brute Force  
**Verdict:** True Positive ✅

---

## Alert Details

| Field | Value |
|---|---|
| EventID | 234 |
| Event Time | Mar 07, 2024, 11:44 AM |
| Rule | SOC176 - RDP Brute Force Detected |
| Type | Brute Force |

---

## Investigation Steps

### Step 1 - IP Reputation Check
Checked source IP reputation using VirusTotal and AbuseIPDB.  
**Result:** IP identified as malicious, associated with brute 
force activity.

### Step 2 - Log Management
Analyzed authentication logs for failed and successful login attempts.  
**Result:** Multiple failed RDP login attempts detected from 
single source IP over short time period - classic brute force pattern.

### Step 3 - Determine the Scope
Investigated how many systems were targeted.  
**Result:** Attack focused on single host.

### Step 4 - Traffic Analysis
Analyzed network traffic from source IP.  
**Result:** High volume of RDP connection attempts confirmed 
brute force attack.

### Step 5 - Enrichment and Context
Gathered additional context about the attack.  
**Result:** Attack originated from external IP, no legitimate 
business reason for RDP access from this source.

### Step 6 - Device Isolation
Based on evidence of successful brute force attack, host was isolated.  
**Result:** Device isolated to prevent further unauthorized access.

---

## Actions Taken
- Affected host isolated from network
- Source IP blocked
- Incident escalated for credential reset and forensic investigation

---

## Analyst Note
Successful brute force attack, host isolated.

---

## Verdict
**True Positive** - RDP brute force attack confirmed successful. 
Host isolated immediately to prevent lateral movement.

---

## Lessons Learned
RDP brute force attacks are often automated and target 
common usernames and passwords. Key indicators: high volume 
of failed logins from single IP in short timeframe. 
When brute force is successful (valid credentials found), 
immediate host isolation is required to prevent attacker 
from moving laterally through the network.

## Screenshot
![Alert Summary](003-bruteforce.png)
