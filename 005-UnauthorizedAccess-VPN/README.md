# SOC257 - VPN Connection Detected from Unauthorized Country

**Platform:** LetsDefend  
**Date:** Jun 15, 2026  
**Severity:** Low  
**Type:** Unauthorized Access  
**Verdict:** True Positive ✅

---

## Alert Details

| Field | Value |
|---|---|
| EventID | 225 |
| Event Time | Feb 13, 2024, 02:04 AM |
| Rule | SOC257 - VPN Connection Detected from Unauthorized Country |
| Type | Unauthorized Access |

---

## Investigation Steps

### Step 1 - IP Reputation Check
Checked source IP on VirusTotal and AbuseIPDB.  
**Result:** IP belongs to VNPT Corp (AS45899) - Vietnamese ISP. 
IP flagged as malicious.

### Step 2 - Network Direction
Source IP: external (Vietnam)  
Destination: company VPN gateway  
**Result:** External → Company Network

### Step 3 - Define Threat Actor
Analyzed IP origin and behavior pattern.  
**Result:** External threat actor connecting from Vietnam - 
unauthorized country for company VPN access.

### Step 4 - Is Sensitive Data at Risk?
Checked what resources the user accessed after VPN connection.  
**Result:** Sensitive data potentially at risk - 
access to internal systems confirmed.

### Step 5 - Has Critical System Been Affected?
Investigated which systems were reachable via this VPN session.  
**Result:** Critical systems potentially affected - 
full scope requires L2 investigation.

### Step 6 - Device Isolation
Assessed whether endpoint isolation was necessary.  
**Result:** VPN session terminated and source IP blocked. 
Device isolation not required - threat was at network level.

---

## Artifacts

| Type | Value | Notes |
|---|---|---|
| IP Address | Source IP (Vietnam) | VNPT Corp AS45899, malicious |
| Country | Vietnam | Unauthorized country for VPN access |

---

## Analyst Note
Unauthorized VPN access from high-risk location. VPN connection 
detected from Vietnam (VNPT Corp) at 02:04 AM. No authorized 
remote work or planned test confirmed. Session terminated, 
IP blocked, user password reset recommended.

---

## Verdict
**True Positive** - Unauthorized VPN connection from Vietnam 
confirmed. Potential access to sensitive data and critical systems.

---

## Lessons Learned
First attempt on this alert resulted in incorrect answers on 
device isolation, sensitive data and critical system questions.

**Key lesson:** VPN unauthorized access does NOT automatically 
require device isolation. The threat is at network level - 
correct response is to terminate VPN session and block source IP.

For sensitive data and critical systems questions - always check 
what the user actually accessed during the session before answering. 
Do not assume - verify in logs first.

**Important timing indicator:** Connection at 02:04 AM from 
unusual country is a strong indicator of unauthorized access 
rather than legitimate remote work.

