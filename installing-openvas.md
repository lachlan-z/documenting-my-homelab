# Installing OpenVAS

## 📌 Project Overview
This project documents the installation and troubleshooting of **OpenVAS** (GVM) on a Kali Linux machine. The objective was to set up a professional vulnerability scanner, though the process highlighted critical hardware and configuration requirements for the service.

## 🛠️ Environment
* **OS:** Kali Linux (Up-to-date)
* **Tool:** OpenVAS

---

## 🚀 Implementation & Troubleshooting

### 1. Initial Setup & Dependency Alignment
* **Updates:** Ensured the Kali machine was fully up to date before installation.
* **Database Alignment:** During the setup, I realized the **Postgres** version on my machine differed from the one required by the OpenVAS setup. I manually aligned these versions to continue the installation.

### 2. Performance Bottlenecks
* **Dashboard Access:** Accessed the OpenVAS dashboard via the browser on `localhost` port `9392`.
* **Sync Issues:** Ran into a serious bottleneck during the data syncing process.
* **Resource Monitoring:** Used `top -bc -u postgres` to investigate the delay.
* **Discovery:** Identified a **73.2 wa** (iowait), meaning the CPU was waiting for I/O operations.

---

## 📈 Lessons Learned & Technical Discoveries
* **Resource Allocation:** I noticed I didn't allocate enough **RAM** to the machine, which caused "thrashing" and severe performance degradation.
* **Disk Space & Storage:** After learning the disk space requirements for OpenVAS, I decided not to continue with the setup until I upgrade the storage on my machine.
* **Technical Insight:** The high `iowait` confirmed that the system was being choked by slow disk operations and insufficient memory, making a successful sync impossible under the current hardware constraints.
