

# 🛡 Splunk SOC Lab – Brute Force Detection

## 📌 Project Overview

This project demonstrates how to detect brute-force login attempts using Splunk SIEM by analyzing Linux authentication logs.

The objective is to simulate real-world SOC monitoring and identify suspicious login activity based on repeated failed authentication attempts.

---

## 🎯 Objective

* Monitor Linux authentication logs
* Detect multiple failed login attempts
* Identify suspicious source IP addresses
* Simulate a SOC investigation workflow

---

## 🛠 Tools Used

* Splunk Enterprise
* Ubuntu Linux
* Linux Authentication Logs (`/var/log/auth.log`)

---

## 🔎 Log Source

Linux authentication logs:

```
/var/log/auth.log
```

Failed SSH login attempts are monitored to detect brute-force behavior.

---

## 🚨 Detection Logic

Splunk Query Used:

```
index=linux_logs "Failed password"
| stats count by src_ip
| where count > 5
```

This query identifies IP addresses with more than 5 failed login attempts.

---

## 📊 Investigation Steps

1. Ingested `/var/log/auth.log` into Splunk
2. Filtered failed login events
3. Aggregated events by source IP
4. Identified suspicious IP performing repeated login attempts
5. Documented findings

---

## 📸 Screenshots

( screenshots inside a folder named `screenshots/`)

* Splunk log ingestion
* Detection query
* Query results

---

## 📝 Findings

* Multiple failed login attempts detected
* Suspicious IP identified
* Behavior consistent with brute-force attack pattern

---

## ✅ Conclusion

This lab demonstrates practical SOC monitoring skills using Splunk.
By analyzing authentication logs, repeated login failures can be detected and investigated effectively.

---

## 📚 Skills Demonstrated

* SIEM log ingestion
* Log analysis
* Threat detection
* Basic incident investigation
* Query creation in Splunk

---

📸 Detection Screenshots
Raw Failed Login Events

IP Extraction

Brute Force Detection
