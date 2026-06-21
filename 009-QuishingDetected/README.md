# SOC251 - Quishing Detected (QR Code Phishing)

**Platform:** LetsDefend  
**Date:** Jun 21, 2026  
**Severity:** Medium  
**Type:** Exchange  
**Verdict:** True Positive ✅

---

## Alert Details

| Field | Value |
|---|---|
| EventID | 214 |
| Event Time | Jan 01, 2024, 12:37 PM |
| Sender | security@microsecmfa.com |
| Recipient | Claire@letsdefend.io |
| Subject | New Year's Mandatory Security Update: MFA |
| Device Action | Allowed |

---

## What I Did

Checked the sender IP on VirusTotal - 8/91 detections, confirmed malicious.

Checked browser history for the recipient (Claire) - no sign she clicked 
any link or scanned the QR code.

Checked Email Security logs - email was delivered but found no evidence 
it was opened or interacted with.

Searched logs for the attacker IP across other accounts - only Claire 
was targeted, no other devices affected.

---

## Mistake I Made

First time I answered "No" to containment, thinking since Claire didn't 
click anything, there was nothing to isolate.

**Correct answer was "Yes - isolate the host."** Even without confirmed 
interaction, containment can be a precautionary step to prevent any 
risk if the user did interact with it but logs missed something, or 
to stop further phishing attempts to the same account. Claire could do interaction with her mobile phone.

---

## Verdict
**True Positive** - Quishing attempt, blocked before user interaction.

---

## Analyst Note
Ignore emails sent from this IP.
