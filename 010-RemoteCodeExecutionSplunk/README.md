# SOC239 - Remote Code Execution Detected in Splunk Enterprise

**Platform:** LetsDefend  
**Date:** Jun 21, 2026  
**Severity:** High  
**Type:** Unauthorized Access  
**Verdict:** True Positive ✅

---

## Alert Details

| Field | Value |
|---|---|
| EventID | 201 |
| Event Time | Nov 21, 2023, 12:24 PM |
| Source IP | 180.101.88.240 |
| Destination IP | 172.16.20.13 |
| Hostname | Splunk Enterprise |
| Trigger File | shell.xsl |
| Device Action | Allowed |

---

## What I Did

Checked source IP on VirusTotal - confirmed malicious.

Looked at the request URL - file upload named "shell.xsl" going to 
Splunk's indexing/preview endpoint. This is XML Injection (XSLT file 
used to trigger code execution), not Command Injection.

Checked mailbox for any planned penetration test notice - nothing found, 
not a planned test.

Checked Command History on the Splunk host via Endpoint Security. 
Found normal admin activity early in the day, then at 12:23-12:24 
(right when the alert triggered) suspicious commands appeared:
- `cat shell.sh` - attacker checking uploaded file
- `whoami`, `id`, `groups` - checking permissions
- `useradd -m analsyt` + `passwd analsyt` - backdoor account created

---

## Verdict
**True Positive** - RCE attack succeeded. Attacker uploaded malicious 
XSLT file, gained code execution, and created a backdoor user account.

---

## Analyst Note
RCE attack confirmed on Splunk Enterprise via malicious XSLT file 
upload (shell.xsl). Source IP 180.101.88.240 confirmed malicious on 
VirusTotal. Attack succeeded - found post-exploitation activity in 
Command History including backdoor account "analsyt" created after 
exploit. Host isolated. Escalated to Tier 2.

---

## Lessons Learned
Same pattern as the SQL Injection case - check Command History around 
the exact alert timestamp, not just for any suspicious commands. The 
attacker's actions right after the exploit (recon commands + creating 
a new user) is the clearest sign that RCE actually worked.
