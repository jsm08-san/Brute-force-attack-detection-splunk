# Brute Force Attack Detection and SOC Monitoring using Splunk SIEM

## Overview

This project demonstrates the simulation and detection of SSH brute-force attacks in a controlled virtual lab environment. A brute-force attack was launched from Kali Linux using Hydra against an Ubuntu SSH server. Authentication logs generated during the attack were collected and analyzed using Splunk Enterprise. SPL (Search Processing Language) queries, dashboards, and visualizations were created to monitor failed login attempts and improve threat visibility.

This project provides hands-on experience with Security Information and Event Management (SIEM), authentication log analysis, security monitoring, and SOC investigation workflows.

---

## Objectives

* Simulate SSH brute-force attacks using Hydra.
* Configure an Ubuntu server with OpenSSH.
* Collect Linux authentication logs.
* Ingest authentication logs into Splunk Enterprise.
* Analyze failed and successful login attempts using SPL.
* Build a security dashboard for SSH authentication monitoring.
* Improve understanding of SOC monitoring and incident detection.

---

## Lab Architecture

```
                +----------------------+
                |      Kali Linux      |
                |      (Attacker)      |
                +----------+-----------+
                           |
                     SSH Brute Force
                      (Hydra Tool)
                           |
                           v
                +----------------------+
                |      Ubuntu VM       |
                |    OpenSSH Server    |
                +----------+-----------+
                           |
                     Authentication Logs
                     (/var/log/auth.log)
                           |
                           v
                +----------------------+
                |  Splunk Enterprise   |
                |      SIEM Server     |
                +----------+-----------+
                           |
          +----------------+----------------+
          |                                 |
     SPL Queries                     Dashboards
          |                                 |
          +---------------+-----------------+
                          |
                      Security Alerts
```

---

## Technologies Used

* Splunk Enterprise
* Kali Linux
* Ubuntu Linux
* Hydra
* OpenSSH Server
* VirtualBox
* SPL (Search Processing Language)

---

## Project Workflow

1. Created two virtual machines using VirtualBox.
2. Installed Ubuntu as the target machine.
3. Installed Kali Linux as the attacker machine.
4. Configured both VMs using a Bridged Network Adapter.
5. Installed and configured OpenSSH Server on Ubuntu.
6. Created a test user account for SSH authentication.
7. Installed and configured Splunk Enterprise.
8. Added Linux authentication logs (`/var/log/auth.log`) to Splunk.
9. Generated brute-force attacks using Hydra from Kali.
10. Monitored authentication logs in Splunk.
11. Created SPL queries to identify suspicious login attempts.
12. Built dashboards for authentication monitoring.
13. Configured alerts for repeated failed login attempts.

---

## SPL Queries

### Failed SSH Login Attempts

```spl
index=* "Failed password"
```

### Successful SSH Login Attempts

```spl
index=* "Accepted password"
```

### Failed Login Attempts Over Time

```spl
index=* "Failed password"
| timechart count
```

### Top Targeted Usernames

```spl
index=* "Failed password"
| rex "for (invalid user )?(?<username>\S+)"
| stats count by username
```

### Top Attacker IP Addresses

```spl
index=* "Failed password"
| rex "from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| stats count by src_ip
```

### Success vs Failure

```spl
index=* ("Accepted password" OR "Failed password")
| eval Status=if(searchmatch("Accepted password"),"Success","Failure")
| stats count by Status
```

---

## Dashboard Components

* Failed SSH Login Attempts
* Successful SSH Login Attempts
* Failed Login Trend
* Top Targeted Usernames
* Top Source IP Addresses
* Authentication Success vs Failure

---

## Project Outcomes

* Successfully simulated SSH brute-force attacks.
* Monitored Linux authentication events using Splunk Enterprise.
* Identified repeated failed authentication attempts.
* Developed dashboards for authentication monitoring.
* Created SPL queries for security investigations.
* Improved practical understanding of SIEM workflows and SOC monitoring.

---

## Skills Demonstrated

* Security Operations Center (SOC)
* SIEM Monitoring
* Linux Log Analysis
* Splunk Enterprise
* SPL Query Development
* Authentication Monitoring
* SSH Security
* Brute Force Attack Detection
* Threat Investigation
* Security Dashboard Development

---

## Screenshots

The repository includes screenshots of:

* Lab Setup
* SSH Server Configuration
* Hydra Brute Force Attack
* Splunk Search Results
* Authentication Log Analysis
* Security Dashboard
* Alert Configuration

---

## Future Enhancements

* Integrate Fail2Ban for automated response.
* Configure email alerts for repeated login failures.
* Monitor additional Linux system logs.
* Implement real-time threat detection.
* Integrate with other SIEM data sources.

---

## Author

**Santhoshi Manaswini J**

Final Year B.Sc. Cyber Security Student

GitHub: *(Add your GitHub profile link here)*

LinkedIn: *(Add your LinkedIn profile link here)*

---

## License

This project is licensed under the MIT License.
