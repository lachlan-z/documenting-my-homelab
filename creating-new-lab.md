# Homelab Build & Architecture Documentation

## 📌 Project Overview
This project documents the physical assembly, hardware procurement, and network configuration of a custom virtualization environment. The goal was to build a robust, segmented lab using **Proxmox VE** and enterprise-grade networking hardware to support "Router-on-a-Stick" topologies and multi-VLAN traffic management.

## 🛠️ Hardware Specifications
* **Core Server:** Intel i7-7700
* **NIC:** Intel i340-T4 quad-port Gigabit Ethernet
* **Switching:** Cisco 2960S Managed Switch
* **Storage (Boot):** 128GB Intel SSD (Proxmox OS)
* **Storage (VMs):** 1TB HDD (ISO & Disk Images)

---

## 🚀 Phase I: Hardware Procurement & Physical Integration

### 1. Physical Assembly
* Installed the Intel i340-T4 NIC into the PCIe slot for high-performance network segmentation.
* **Cable Architecture:**
    * **Management:** Intel NIC Port 4 (`enp1s0f3`) dedicated to Proxmox management traffic.
    * **Trunked Traffic:** Intel NIC Port 3 (`enp1s0f2`) dedicated to laboratory trunked traffic.
* **Physical Uplink:** Established a link between Proxmox and the Cisco 2960S (Port `Gi1/0/1`) to facilitate the "Router-on-a-Stick" topology.

---

## 💻 Phase II: Software Implementation & Network Configuration

### 1. Proxmox Installation & Initialization
* **Boot Media:** Created a bootable drive using BalenaEtcher on macOS.
* **BIOS Configuration:** Enabled **Intel VT-x/VT-d** to support hardware-accelerated virtualization.
* **Storage Prep:** Performed a secure wipe of the 1TB HDD to initialize it for high-capacity VM deployment.

### 2. Network Hardware Migration
* Migrated the management uplink from the integrated motherboard port (`e1000e`) to the Intel i340-T4 (`igb`).
* **Reasoning:** This mitigation was performed to improve driver stability and ensure strict traffic isolation.
* **Configuration:** Updated `/etc/network/interfaces` to map the management bridge (`vmbr0`) to the new physical interface (`enp1s0f3`).

### 3. VLAN Trunking & 802.1Q Implementation
* **Linux Bridge:** Created a **VLAN-aware** Linux Bridge (`vmbr1`) on physical interface `enp1s0f2`.
* **Switch Configuration:** Configured the Cisco 2960S port (`Gi1/0/1`) as an **802.1Q trunk**.
* **VLAN Assignments:** Configured the trunk to allow simultaneous passage of **VLANs 1, 10, and 20** between the host and the network fabric.

---

## 📈 Key Technical Outcomes
* **Hardware-Accelerated Virtualization:** Fully enabled via BIOS settings for optimal VM performance.
* **Network Isolation:** Achieved physical and logical separation of management and lab traffic.
* **Scalable Topology:** The "Router-on-a-Stick" configuration allows for easy addition of new VLANs and subnetworks without adding physical hardware.
