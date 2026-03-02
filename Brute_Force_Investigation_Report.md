# Brute Force Attack Investigation Report

## 1. Incident Summary

A potential brute-force SSH attack was detected on the monitored Linux system using Splunk SIEM. Multiple failed login attempts were observed from the same IP address within a short time period.

---

## 2. Log Source

* Log File: `/var/log/auth.log`
* Sourcetype: `linux_logs`
* Index: `main`
* Host: antony-VMware-Virtual-Platform

---

## 3. Detection Method

The following SPL query was used to identify repeated failed login attempts:

```spl
index=main "Failed password"
| rex "from (?<attacker_ip>\d+\.\d+\.\d+\.\d+)"
| stats count as failed_attempts by attacker_ip
| where failed_attempts > 5
```

This query extracts the attacker IP and counts failed attempts. Any IP with more than 5 failed attempts is flagged as suspicious.

---

## 4. Findings

* Attacker IP: 127.0.0.1
* Failed Attempts: 6+
* Target Service: SSH
* Attack Type: Brute-force login attempt

Multiple authentication failures indicate a brute-force attempt to gain unauthorized access.

---

## 5. Impact Assessment

No successful login was observed. The attack was limited to failed authentication attempts. However, repeated attempts indicate malicious intent.

---

## 6. Recommended Actions

* Implement account lockout policy after multiple failed attempts
* Enable firewall rules to block suspicious IP addresses
* Configure Splunk alert for real-time brute-force detection
* Use fail2ban to prevent automated attacks

---

## 7. Conclusion

The brute-force attempt was successfully detected using Splunk SIEM by monitoring Linux authentication logs. Proper log ingestion, field extraction, and statistical analysis enabled effective identification of suspicious behavior.

This lab demonstrates practical SOC-level detection and investigation workflow.

---
