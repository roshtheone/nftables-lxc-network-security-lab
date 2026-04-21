# 🛡️ Linux Firewall and Container Security Lab
A hands-on cybersecurity lab focused on building a **stateful Linux firewall** with `nftables`, enforcing a **default-deny inbound policy**, and securely forwarding traffic from a VM host to an internal **LXC container**.
This project documents both the **design phase** and the **implementation phase**, showing how a Linux virtual machine can act as a secure public entry point while hosting services safely inside a containerized environment.

----
## ✨ Project Highlights
- 🔒 Stateful firewall built with `nftables`
- 🚫 Default-deny inbound traffic policy
- 🌐 Secure exposure of only **SSH, HTTP, and HTTPS**
- 🔁 DNAT port forwarding from VM host to internal `www` container
- 📦 LXC container addressing and network verification
- 🧪 Service validation and blocked-port testing
- 📝 Clear documentation with screenshots from planning to implementation

  ----
  ## 🧰 Technologies Used

- 🐧 Linux
- 🛡️ `nftables`
- 📦 LXC / LXD
- 🌍 Networking tools: `ip`, `ss`, `sysctl`, `curl`, `nc`
- 🔧 System tools: `systemctl`

---

## 🎯 Security Goals

- Block all inbound traffic by default
- Allow only:
  - `22` → SSH
  - `80` → HTTP
  - `443` → HTTPS
- Forward traffic securely to the internal `www` container
- Keep the host VM as the public access point
- Reduce exposure by keeping services inside the container

---
## 🗺️ Architecture Overview

```text
Internet / User
      ↓
VM Host (10.0.2.15)
      ↓
nftables Firewall + DNAT
      ↓
www Container (172.16.31.50)
