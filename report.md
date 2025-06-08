# 🛡️ Detailed Analysis Report

## 1. Overview

This report documents the implementation of a Host-Based Intrusion Detection System (HIDS) using OSSEC in a controlled lab environment. The setup uses two virtual machines: one as the **server** (Ubuntu) and another as the **agent** (Kali Linux). The project simulates typical intrusion detection tasks such as agent management, system log monitoring, and alert generation.

---

## 2. OSSEC Installation and Configuration

- **Server**: Ubuntu VM.
- **Agent**: Kali Linux VM.
- **OSSEC Version**: 3.7.0

**Installation Steps**:
- Downloaded and extracted OSSEC HIDS 3.7.0.
- Installed OSSEC HIDS on both the Ubuntu server and the Kali agent.
- Configured the Ubuntu server as the OSSEC manager.
- Added the Kali agent on the server and extracted the agent key.
- Configured the agent to connect to the server.

**Configuration Highlights**:
- Email notifications were disabled during installation.
- Integrity check daemon (`syscheckd`) enabled to monitor filesystem changes.
- Syslog monitoring was configured on both server and agent.

---

## 3. Attack Simulation and Analysis

- **Simulated Attack**:
  - From the Kali agent, ran `nmap` scans targeting the Ubuntu server.
  - Simulated unauthorized SSH login attempts using `sudo tail` commands and privilege escalation.
- **Observed Behavior**:
  - OSSEC HIDS server generated alerts corresponding to suspicious activities.
  - Alerts included:
    - Brute-force login attempts.
    - Unauthorized root login detection.
    - System file changes (rootcheck).

---

## 4. Indicators of Compromise (IoCs)

| Indicator             | Description                       |
|-----------------------|-----------------------------------|
| Source IP: 192.168.64.x | Attacker’s IP                   |
| Destination IP: 192.168.64.x | Target’s IP (Ubuntu)      |
| Port: 22/tcp          | SSH service port targeted        |
| OSSEC Alerts          | Generated based on suspicious events |

---

## 5. Screenshots

Below are screenshots saved in the `/screenshots/` folder illustrating each analysis step:

| Screenshot | Description |
|------------|-------------|
| `screenshots/1.jpeg`  | OSSEC HIDS installation on Ubuntu server. |
| `screenshots/2.jpeg`  | OSSEC HIDS installation on Kali agent. |
| `screenshots/3.jpeg`  | Creating an agent on Ubuntu server. |
| `screenshots/4.jpeg`  | Retrieving Ubuntu’s IP address and agent key. |
| `screenshots/5.jpeg`  | Creating another agent and getting the agent key. |
| `screenshots/6.jpeg`  | Checking agent status on Ubuntu after running on Kali. |
| `screenshots/7.jpeg`  | Attempted attack from Kali on Ubuntu using `sudo tail`. |
| `screenshots/8.jpeg`  | Monitoring the attack on Kali. |
| `screenshots/9.jpeg`  | Running the Nmap attack on Kali targeting Ubuntu. |
| `screenshots/10.jpeg` | Checking generated alerts on Ubuntu terminal (OSSEC logs). |
| `screenshots/11.jpeg` | Final alert logs on Ubuntu showing detection of the Kali attack. |

---

## 6. Recommendations

- Regularly update OSSEC signatures and rule sets.
- Configure email notifications to receive real-time alerts.
- Harden SSH configuration and limit access to trusted IPs.
- Monitor system logs (`/var/log/auth.log`, `/var/ossec/logs/alerts/alerts.log`) for suspicious events.
- Implement fail2ban or similar tools to mitigate brute-force attacks.

---

## 7. Conclusion

This project demonstrates how to deploy OSSEC HIDS for host-based intrusion detection. Screenshots and logs highlight attacker behaviors and show how OSSEC HIDS effectively detects malicious activities.

---

## 8. Author

**Aman Sharma**  
Cybersecurity & Network Analysis Enthusiast  
