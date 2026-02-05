# Metasploitable 2: Exploring r-services

## 📌 Overview
This project documents the reconnaissance and exploitation of legacy "r-services" on a **Metasploitable 2** target within a virtualized home lab. The goal was to identify open ports and leverage misconfigured default settings to gain an initial foothold on the system.

## 🛠️ Lab Architecture
* **Attacker Machine:** Kali Linux
* **Target Machine:** Metasploitable 2
* **Network Environment:** Isolated Virtual Lab

---

## 🚀 Execution & Findings

### 1. Service Discovery
* **Action:** Ran `nmap -sV [TARGET_IP]` to determine open ports.
* **Discovery:** Noticed that ports **512**, **513**, and **514** were all open.

### 2. Protocol Analysis
* **Observation:** These are **rsh ports**, which have mostly been switched to **SSH (Port 22)** in modern environments.
* **Security Flaw:** The Metasploitable 2 machine did not have its default passwords updated, making it vulnerable to unauthorized access.

### 3. Exploitation
* **Method:** Because the machine used default credentials, it can be logged into using the following command:
  `rlogin -l msfadmin -p 513 [TARGET_IP]`

---

## ⚡ Impact
* **System Control:** Successfully gaining access provided control over the Metasploitable 2 machine.
* **Foothold established:** With this access, I can perform many malicious activities as I have a foothold.

## 📈 Lessons Learned & Technical Discoveries
* **Legacy Protocol Risks:** This experiment highlights the danger of leaving legacy services active, as they lack the security features of modern standards like SSH.
* **Default Credential Hazards:** The ease of this exploit was entirely due to the failure to update default passwords, a common but critical security oversight.
