## 📌 Overview
This project documents a standalone security experiment focused on deploying and configuring an Intrusion Detection/Prevention System (IDS/IPS) within a virtualized network. I utilized **pfSense** as a core firewall and integrated **Snort** to monitor, detect, and automatically block malicious network activity.

## 🛠️ Lab Architecture
The lab was built as an isolated virtual network to safely simulate and mitigate real-world attack vectors.

* **Firewall/Router:** pfSense running on a **FreeBSD Virtual Machine**.
* **IDS/IPS Engine:** Snort (configured as a pfSense package).
* **Network Topology:** * **WAN:** Connected to the host network for internet access.
    * **LAN:** Private internal network hosting the target assets.
* **Target Asset:** Metasploitable 2 (Linux-based vulnerable VM).



---

## 🚀 Implementation & Configuration

### 1. Interface Initialization
* **Snort Deployment:** Installed the Snort package within pfSense and bound the sensor to the **LAN interface**.
* **Traffic Visibility:** Monitoring the LAN interface ensures the IDS can inspect "east-west" traffic (internal VM-to-VM) and any inbound requests that bypass initial firewall rules.

### 2. Detection Logic & Threat Intel
I configured specific signatures to detect two common stages of an attack: Reconnaissance and Command & Control (C2).
* **SSH Detection:** Monitoring for brute-force attempts or unauthorized remote access.
* **ICMP (Ping) Monitoring:** Configured specifically to identify potential **Remote Access Trojans (RATs)** and **C2 heartbeats**. 
    * *Security Insight:* Adversaries often use ICMP for "heartbeat" checks or covert exfiltration because it is frequently overlooked by standard port-based firewall rules.

### 3. Transitioning to Active Prevention (IPS)
I enabled the **"Block on Alert"** feature to transform the setup into a functional Intrusion Prevention System.
* **Automated Mitigation:** When a packet triggers a Snort rule, the source IP is dynamically added to the pfSense **Block Table**, immediately severing the connection.
* **Administrative Pass Lists:** To prevent accidental lockouts during research, I configured a **Pass List** for my host machine, allowing me to ping and manage the lab without being blocked by the IDS.

---

## 📈 Lessons Learned & Technical Discoveries
* **Rule Persistence:** I discovered that Snort must be **manually restarted** within the pfSense interface whenever rules or Pass Lists are modified to ensure changes are committed to the engine.
* **Alert Integrity:** I intentionally avoided using **Suppress Lists**. While they reduce log noise, they hide critical event data. For this experiment, I prioritized 100% visibility into every triggered alert over a cleaner dashboard.
* **The "Default Deny" Realization:** My initial approach focused on creating "Deny" rules for every specific bad packet I encountered. I realized this logic was flawed and inefficient. I have since adopted a **"Default Deny" architecture**, where I explicitly allow only verified traffic and let a single final rule drop everything else.

---

## 🧰 Tools & Environment
* **OS:** FreeBSD (via pfSense), Linux (Metasploitable 2).
* **Security:** Snort (Signature-based detection).
* **Testing:** PuTTY (SSH verification), ICMP (Traffic testing).
* **Virtualization:** VirtualBox.
