# 🔐 SSH Brute Force Detection Using Splunk SIEM

## 🚀 Overview

Cyberattacks often begin with unauthorized login attempts. This project demonstrates how a Security Information and Event Management (SIEM) platform can detect and monitor SSH brute-force attacks in real time.

Using **Splunk Enterprise**, authentication logs from an **Ubuntu Server** are collected, analyzed, and visualized. A **Kali Linux** machine simulates brute-force attacks, allowing the system to identify suspicious login behavior and trigger security alerts.

---

## 🎯 Objectives

* Collect SSH authentication logs from Ubuntu Server.
* Detect repeated failed login attempts.
* Identify attacking IP addresses.
* Generate real-time security alerts.
* Visualize attack activity through dashboards.
* Demonstrate a basic Security Operations Center (SOC) workflow.

---

## 🏗️ Architecture

```text
Kali Linux (Attacker)
        │
        │ SSH Brute Force Attack
        ▼
Ubuntu Server (Target)
        │
        │ /var/log/auth.log
        ▼
Splunk Universal Forwarder
        │
        ▼
Splunk Enterprise (SIEM)
        │
        ├── Detection Rules
        ├── Alerts
        └── Dashboards
```

---

## 🛠️ Technologies Used

| Technology                 | Purpose           |
| -------------------------- | ----------------- |
| Splunk Enterprise          | SIEM Platform     |
| Splunk Universal Forwarder | Log Collection    |
| Ubuntu Server              | Target System     |
| OpenSSH Server             | SSH Service       |
| Kali Linux                 | Attack Simulation |
| Hydra                      | Brute Force Tool  |

---

## 🔍 Detection Logic

The following Splunk query identifies source IPs generating multiple failed SSH login attempts:

```spl
index=* "Failed password"
| rex "from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| stats count by src_ip
| where count >= 5
```

### Detection Workflow

1. SSH login failures are generated.
2. Ubuntu records events in `auth.log`.
3. Universal Forwarder sends logs to Splunk.
4. Splunk extracts source IP information.
5. Detection rule identifies suspicious activity.
6. Alert is triggered.
7. Dashboard visualizes the attack.

---

## 📊 Dashboard Features

### 📈 Failed Login Count

Displays the total number of failed SSH login attempts.

### 🌍 Top Attacker IPs

Identifies the most active attacking hosts.

---

## ⚔️ Attack Simulation

A controlled SSH brute-force attack is launched from Kali Linux using Hydra.

Example:

```bash
hydra -l test -P lists.txt ssh://TARGET_IP
```

The generated authentication failures are then detected and analyzed by Splunk.

---

## 📷 Screenshots

* SIEM SETTING UP:
<img width="1917" height="956" alt="recieving config added port 9997" src="https://github.com/user-attachments/assets/ad0e6019-660d-431b-b10d-9957ce8daca6" />


<img width="1362" height="718" alt="listed forward-servers" src="https://github.com/user-attachments/assets/a3285e9b-8b84-441a-8d2d-1295414ea5bf" />


<img width="1360" height="716" alt="Monitor files" src="https://github.com/user-attachments/assets/06964fbd-f6c6-4c16-9f9c-77e59d53e277" />




* Kali Linux attack simulation
<img width="1364" height="722" alt="attack done on kali found pass" src="https://github.com/user-attachments/assets/7d219709-e768-4da2-a9f2-4fd4f7c9a4f8" />



* Security dashboard
<img width="1907" height="947" alt="dashboard after attack" src="https://github.com/user-attachments/assets/52beeab1-2984-4930-ac92-dc533115b636" />



---

## 🧠 Skills Demonstrated

* SIEM Operations
* Log Analysis
* Threat Detection
* Security Monitoring
* Incident Detection
* Linux Administration
* Splunk Dashboard Development
* Alert Engineering

---

## 📌 Future Enhancements

* Automated IP Blocking
* Email Notifications
* MITRE ATT&CK Mapping
* Threat Intelligence Integration
* SOAR Automation
* Multi-Server Monitoring

---

## 🎓 Educational Purpose

This project was developed as a cybersecurity learning exercise to understand how modern SOC teams detect and investigate brute-force attacks using SIEM technology.

---

## ⭐ Key Takeaway

This project demonstrates the complete security monitoring lifecycle:

**Collect → Analyze → Detect → Alert → Visualize**

which forms the foundation of modern Security Operations Centers (SOCs).
