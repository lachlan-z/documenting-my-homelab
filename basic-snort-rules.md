# Snort IDS Exploration: Custom Traffic Alerting & Intrusion Testing

## 📌 Project Overview
This project documents the setup and configuration of **Snort**, an open-source Network Intrusion Detection System (NIDS), within a virtualized home lab. The objective was to monitor internal network traffic and trigger alerts for specific protocols and anomalies—specifically ICMP traffic and packet size variations—originating from a Kali Linux attack machine.

## 🛠️ Lab Architecture
The environment utilizes a "Sensor and Target" model within an isolated virtual network to simulate real-world intrusion scenarios.

* **IDS Sensor:** Ubuntu Server (Snort)
* **Attack Machine:** Kali Linux
* **Target Machine:** Metasploitable 2
* **Network Interface:** `enp0s8` (Internal Bridge)



---

## 🚀 Implementation Steps

### 1. Custom Rule Definition
I configured custom rules in the `local.rules` file to detect ICMP (Ping) traffic directed at the target machine.

* **Configuration Path:** `/etc/snort/rules/local.rules`
* **Rule Syntax:**
    ```snort
    alert icmp any any -> [TARGET_IP] any (msg:"ICMP Traffic Detected"; sid:1000001; rev:1;)
    ```

### 2. Intrusion Testing & Troubleshooting
Using a **Kali Linux** VM, I generated traffic to test the sensor's responsiveness. 

* **Packet Size Exploration:** During testing, I attempted to manually define rules for specific packet sizes to identify non-standard traffic.
* **Key Discovery:** Through this process, I realized that Snort already includes comprehensive preprocessors and built-in rules for packet size handling. This highlighted the importance of auditing existing rule libraries to avoid redundancy and optimize performance.

### 3. Launching the IDS
Snort was executed in IDS mode, monitoring the internal interface and outputting alerts directly to the console for real-time verification.

**Command:**
```bash
sudo snort -q -l /var/log/snort -i enp0s8 -A console -c /etc/snort/snort.conf
