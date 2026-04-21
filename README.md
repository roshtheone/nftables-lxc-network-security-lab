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
```
----
## 📸 Preview

### 🖥️ Host Network Overview
Verified the VM hostname, interfaces, and routing information before applying firewall and forwarding rules.

![Host Network Overview](screenshots/host-network-overview.png)

---

### 📦 LXC Container Address Verification
Confirmed that all running LXC containers had assigned IPv4 addresses, including the `www` container at `172.16.31.50`.

![LXC Container Address Verification](screenshots/lxc-container-address-verification.png)

---

### 🛡️ nftables Firewall Rules
Verified that `nftables` was active and that the firewall enforced a stateful default-deny policy while allowing only ports **22**, **80**, and **443**.

![nftables Firewall Rules](screenshots/nftables-firewall-rules.png)

---

### 🔁 Port Forwarding to the `www` Container
Verified IPv4 forwarding and DNAT rules that route incoming traffic from the VM host to the internal `www` container.

![Port Forwarding to the www Container](screenshots/port-forwarding-www-container.png)

---

### ✅ Container Service Verification
Confirmed that the `www` container was listening on ports **22**, **80**, and **443**, and that the required services were running.

![Container Service Verification](screenshots/container-service.png)

---

### 🧪 Connectivity and Access Validation
Validated successful connectivity to approved services and confirmed that unauthorized ports remained blocked.

![Connectivity and Access Validation](screenshots/connectivity-access-validation.png)

---

## 📄 License and Usage

Copyright (c) 2026 Roshaan Ameer

All rights reserved.

This project is shared for **portfolio, review, and educational viewing purposes only**.  
No permission is granted to use, copy, modify, redistribute, publish, or sell any part of this work without prior written permission from the author.

See the [LICENSE](LICENSE) file for full details.
