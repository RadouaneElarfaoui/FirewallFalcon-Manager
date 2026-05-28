<div align="center">
  <img src="https://img.shields.io/badge/FirewallFalcon-Manager-blue?style=for-the-badge&logo=shield" alt="FirewallFalcon" />
  <h1>🦅 FirewallFalcon Manager v4.0.0</h1>
  <p><b>The ultimate, lightning-fast, and beautiful terminal UI manager for VPN tunneling, protocol deployments, and advanced user administration on Linux servers.</b></p>
  
  <a href="https://github.com/firewallfalcons/FirewallFalcon-Manager/releases">
    <img src="https://img.shields.io/github/v/release/firewallfalcons/FirewallFalcon-Manager?style=flat-square&color=success" alt="Latest Release">
  </a>
  <img src="https://img.shields.io/badge/platform-linux-lightgrey?style=flat-square" alt="Platform">
  <img src="https://img.shields.io/badge/bash-%3E%3D4.0-yellow?style=flat-square&logo=gnu-bash" alt="Bash">
  <a href="https://t.me/firewallfalcons">
    <img src="https://img.shields.io/badge/Telegram-Channel-blue?style=flat-square&logo=telegram" alt="Telegram">
  </a>
</div>

---

## ✨ Why FirewallFalcon Manager?

FirewallFalcon Manager is built with an **obsessive focus on speed, fluidity, and aesthetics**. We took the traditional chunky script and refined it into a gorgeous, highly responsive, and relentlessly efficient terminal experience.

Whether you're managing 5 users or 500, deploying complex protocols, or locking down your server traffic—you can do it all in seconds, with zero frustration.

---

## 🚀 Installation

It takes less than a minute to deploy the complete FirewallFalcon Manager on your fresh VPS. Choose the installation method that works best for you:

### Primary Method (Recommended)
```bash
curl -L -o install.sh "https://raw.githubusercontent.com/firewallfalcons/FirewallFalcon-Manager/main/install.sh" && chmod +x install.sh && sudo ./install.sh && rm install.sh
```

### Alternate Short Method
```bash
bash <(curl -fsSL https://thefirewoods.org)
```

*(Once installed, simply type `menu` in your terminal to launch the interface!)*

---

## 🌟 Elite Features

### 👤 Hyper-Optimized User Management
* **Batch Operations Engine:** Delete, Lock, Unlock, or Renew multiple users simultaneously. You can type `1 3 5` or ranges like `1-4` to execute massive operations in the blink of an eye.
* **Smart UI Selection:** Automatically detects your user count. If you have fewer than 15 active users, it dynamically skips the search prompt to save you keystrokes.
* **Agile Creation:** Bulk string generation with instant preset defaults (`Enter` for 30 Days, unlimited Bandwidth, 1 Device Connection).
* **Temporary Trial Accounts:** Instantly spin up self-destructing trial accounts spanning 1, 2, 6, 12, or 24 hours (powered autonomously by the `at` daemon).

### 🛠️ One-Click VPN & Protocol Deployers
Easily spin up entire tunneling infrastructures onto your server without touching a single complex config file.
* **BadVPN (UDP Gateway):** Optimize gaming and tunneling packets.
* **UDP Custom:** Manage customizable UDP bypasses.
* **SSL Tunnels:** HAProxy payload routing on port 444.
* **Nginx Reverse Proxy:** Full HTTP/HTTPS webserver installer, featuring **Auto-Certbot integration** for free SSL certificates.
* **DNSTT (SlowDNS):** Bypass heavy firewalls through port 53 DNS records.
* **Falcon Proxy:** Setup and customize version-controlled Websocket/Socks proxies.
* **ZiVPN (UDP):** Accelerated custom UDP handling.
* **X-UI Web Panel:** Automated installer for the infamous GUI management portal.

### 📊 Advanced Quotas & Network Safety
* **Strict Bandwidth Limiting:** Assign gigabyte allowances (e.g., 50GB) upon creation. Background services will safely and automatically lock users who exceed their usage.
* **Active Connection Limits:** Ensure nobody shares their account by enforcing strict concurrent session limits. 
* **Live Traffic Monitor:** Check high-speed Bash network tracking (or install `vnstat` for persistent metrics).
* **Anti-Torrent Guard:** Deploy stateful iptables payload inspection to permanently drop `BitTorrent` data, protecting your host from abuse complaints.

### 🎨 Beautiful SSH Customization
* **Dynamic Login Banners:** FirewallFalcon overrides the default SSH `sshd_config` to inject an intelligent script. 
* When your users connect via an HTTP injector or SSH tunnel app, they are greeted by a beautiful customized text box detailing their exact:
  * Expiry Date
  * Quota Remaining
  * Real-Time Active Connections

### 💾 Backup & Restore Stability
* Automatically collect your payload records, user databases, TLS certificates, and bandwidth usage statistics into single portable `.tar.gz` archives. Restore entire businesses onto a new server with one menu click.

---

## Oracle Cloud Always Free Adaptation

This repository is a fork of FirewallFalcon-Manager, specifically optimized and adapted to run seamlessly on Oracle Cloud Always Free Virtual Machines (VMs).

### Crucial Checklist for Oracle Cloud Console (Dashboard)

Oracle Cloud VMs block all incoming traffic by default through Virtual Cloud Network (VCN) Security Lists. To make your tunnels work, you must add Ingress Rules in your Oracle Cloud Console:

1. Go to **Networking** > **Virtual Cloud Networks** > Select your VCN > **Security Lists** > Select your Default Security List.
2. Add **Ingress Rules** with the following settings:
   - **Source CIDR**: `0.0.0.0/0`
   - **IP Protocol**: `TCP`
   - **Destination Port Range**: Add rules for the following ports:
     - `22` (SSH Access)
     - `80` (Standard HTTP & HAProxy Edge Stack)
     - `443` (Standard HTTPS & HAProxy Edge Stack)
     - `8080` (Falcon Proxy Websocket)
     - `8880` (Nginx Cleartext - required for Cloudflare proxying)
     - `8443` (Nginx TLS - required for Cloudflare proxying)
     - `8000` (Alternative HTTP Web port)

### Crucial Checklist on the VPS (System)

1. **Nginx Public Binding**: By default in this fork, the internal Nginx configuration binds to wildcard address `0.0.0.0` (instead of the upstream default `127.0.0.1`). This ensures Cloudflare CDN proxies connecting on ports `8880` or `8443` are routed directly to Nginx.
2. **Service Status Verification**: Ensure that Nginx, HAProxy, and Falcon Proxy are all active and enabled:
   ```bash
   sudo systemctl status nginx haproxy falconproxy
   ```
3. **Firewall Access**: The local OS firewalls (like iptables or ufw) are automatically configured by the installation script to accept these ports.
4. **Interactive Administration**: Just type `menu` in your terminal at any time to manage users, renew accounts, or view live bandwidth metrics.

---

## 💬 Community & Support

* **Telegram Channel:** [t.me/firewallfalcons](https://t.me/firewallfalcons) - Join for updates and support!
* **Donations:** If you find this project useful and want to support its development, you can contribute via:
    * **PayPal:** [paypal.me/00xmahmoud](https://paypal.me/00xmahmoud)
    * **Binance ID:** `885652061`
    * **USDT (TRC20):** `TM2AfVAWQJiuriGC6KoTmsAJuUTTBd2f1R`

---

<div align="center">
  <b>Built by FirewallFalcons</b><br>
  <i>"Fast configuration, Secure tunneling, Beautiful interfaces."</i>
</div>
