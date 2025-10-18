# LS Command Detected in Requested URL Investigation Walkthrough

## 1. Incident Overview
I received a high-severity alert indicating a potential command injection attempt. The alert was triggered because the requested URL contained the term "ls," which can indicate an attempt to execute a Linux system command. My objective was to investigate the activity, determine whether it was a legitimate request or a malicious attempt, and document all findings.

## 2. Tools & Technologies Used
- [**VirusTotal**](https://www.virustotal.com/gui/home/upload)
- [**Whois Lookup**](https://whois.domaintools.com)
- [**AbuseIPDB**](https://www.abuseipdb.com)

## 3. Reviewing the Alert
**Alert Type:** LS Command Detected in Requested URL  
**Severity:** High  
**Event Time:** February 27, 2022, 12:36 AM  
**Source Address:** 172.16.17.46 (Host: EliotPRD)  
**Destination IP Address:** 188.114.96.15  
**Alert Trigger Reason:** URL Contains "ls"  
**Device Action:** Allowed  

**Summary:**  
The host *EliotPRD* initiated an HTTP request to the external IP 188.114.96.15. The URL included the substring “ls,” triggering the detection rule. The request was allowed by the device, meaning no automatic blocking occurred at the network layer. Initial review suggested that the user associated with the activity was *eliot*, last logged in at 12:00 AM on the same date.

## 4. The Investigation
I began by reviewing the raw HTTP traffic associated with the alert. The detection was triggered because the URL string contained “ls,” a common command used for directory listing in Unix systems. Upon deeper inspection, I found that the “ls” sequence was part of the word “skills” within the URL, not an executed command.

Next, I checked additional HTTP logs from the same host and user around the time of the alert. No signs of command injection, abnormal parameters, or encoded payloads were present. All observed traffic was directed toward legitimate domains and contained no malicious indicators.

<img width="1333" height="663" alt="vivaldi_aiCEcFXIXk" src="https://github.com/user-attachments/assets/63b5a3c7-ce51-4134-9d44-69c4ddb7c3e7" width="85%"/>
<br>
<img width="659" height="631" alt="vivaldi_q7MUmN5YOT" src="https://github.com/user-attachments/assets/4bab7240-fb3f-404d-935e-5da21d108610" width="85%"/>
<br>
<img width="775" height="533" alt="vivaldi_DzQojKKPae" src="https://github.com/user-attachments/assets/9bff24ed-a137-498e-828a-0a28f8127310" width="85%"/>

To validate further, I cross-referenced the destination IP with internal and external threat intelligence feeds. The IP 188.114.96.15 was not associated with any known malicious infrastructure. Given these findings, I concluded that the alert was triggered by a benign keyword match and not actual command execution.

## 5. Findings Summary
- URL contained the substring “ls” within a non-malicious word (“skills”).  
- No evidence of command injection or exploit attempt.  
- Destination IP not linked to known malicious actors.  
- HTTP activity appeared normal and business-related.  
- Device action was “Allowed,” and no follow-up alerts were generated.

**Final Determination:**  
This alert was a **False Positive**. The “ls” detection was triggered by a substring match rather than a command execution attempt. No indicators of compromise or malicious activity were found. No further action required.


---

<!-- To insert an image -->
<!-- ![Description](image-path.png) -->

<!-- To create a table -->
<!-- | Column 1 | Column 2 | Column 3 |
|----------|----------|----------|
| Value 1 | Value 2 | Value 3 | -->

<!-- To create a code block -->
<!-- ```bash
command or script here
``` -->

<!-- To create a link -->
<!-- [Link Text](https://example.com) -->
