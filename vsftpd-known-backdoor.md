# Metasploitable 2: Exploring the vsftpd 2.3.4 Backdoor

## 📌 Project Overview
This project documents the identification and exploitation of the notorious backdoor in **vsftpd version 2.3.4** (CVE-2011-2523) on a Metasploitable 2 target. The experiment demonstrates how a specific character sequence can trigger a hidden listener, providing unauthorized command-line access.

## 🛠️ Lab Architecture
* **Attacker Machine:** Kali Linux
* **Target Machine:** Metasploitable 2 (Vulnerable VM)
* **Network Environment:** Isolated Virtual Lab

---

## 🚀 Execution & Findings

### 1. Reconnaissance & Service Identification
I conducted a version scan on the target machine to identify the FTP service and its specific version.
* **Command:** `nmap -sV -p- [TARGET_IP]`
* **Discovery:** Port 21 was running **vsftpd 2.3.4**, which is known to contain a backdoor.

### 2. Triggering the Backdoor
Using **netcat**, I opened a TCP connection to the target on Port 21.
* **Exploit Mechanism:** I was able to enter any username as long as `:)` was concatenated at the end (e.g., `user :)`) and provided any random password.
* **Command:** `nc [TARGET_IP] 21`

### 3. Exploitation & System Access
Upon a secondary scan after triggering the backdoor, **Port 6200** was found to be open.
* **Connection:** I established a TCP connection to Port 6200, which provided direct access to the target machine's command line.
* **Impact:** From this shell, I had full control and could even shut down the target system.

---

## ⚡ Forensic Analysis & Mitigation
* **Log Evidence:** Reviewing the `vsftpd.log` file on the target machine clearly shows the attacker machine's IP address gaining initial access.
* **Security Recommendation:** The presence of an unrecognized IP in the FTP logs should prompt immediate investigation and a network block on that address.
* **Remediation:** Vulnerable versions of vsftpd should be immediately upgraded to a secure version, and legacy services should be audited for similar known backdoors.
