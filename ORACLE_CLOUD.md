# Oracle Cloud Always Free VM - Setup & Configuration Guide

This guide provides crucial steps and checklists to successfully run your FirewallFalcon tunnels on an Oracle Cloud Always Free Virtual Machine (VM).

---

## 1. Oracle Cloud Console (Dashboard) Configuration

Oracle Cloud VMs are protected by an external Virtual Cloud Network (VCN) firewall. By default, all incoming traffic except SSH (Port 22) is blocked. You must manually add Ingress Rules to allow traffic to reach your VPS.

### Step-by-Step Security List Configuration:
1. Log in to your **Oracle Cloud Console**.
2. Go to **Networking** > **Virtual Cloud Networks**.
3. Click on your VCN name.
4. On the left side, click **Security Lists**, then select your **Default Security List**.
5. Click **Add Ingress Rules**.
6. Create an Ingress Rule with the following settings:
   - **Source Type**: `CIDR`
   - **Source CIDR**: `0.0.0.0/0` (Allows traffic from any IP)
   - **IP Protocol**: `TCP`
   - **Destination Port Range**: Add a rule for the following ports:
     - `22` (Raw SSH Access)
     - `80` (Standard HTTP & HAProxy Edge Stack)
     - `443` (Standard HTTPS & HAProxy Edge Stack)
     - `8080` (Falcon Proxy Websocket Backend)
     - `8880` (Nginx Cleartext - Required for Cloudflare proxying)
     - `8443` (Nginx TLS - Required for Cloudflare proxying)
     - `8000` (Alternative HTTP port)

---

## 2. VPS System Checklist & Verifications

This fork has been customized to make tunneling behind Cloudflare extremely easy and stable out-of-the-box.

### Key Details on the VPS:
1. **Public Nginx Binding**: 
   The Nginx internal proxy is configured to bind to wildcard address `0.0.0.0` (on ports `8880` and `8443`) instead of the loopback `127.0.0.1`. This allows Cloudflare CDN proxies (like `canary-guest-cf.pscp.tv:8880`) to communicate directly with your Nginx server.
   
2. **Checking Services Status**:
   Ensure that Nginx, HAProxy, and Falcon Proxy are all active and running on your server:
   ```bash
   sudo systemctl status nginx haproxy falconproxy
   ```
   
3. **Firewall Verification**:
   The local OS firewalls (iptables/ufw) are configured automatically by the installer script to accept the required ports. You do not need to perform any manual local firewall rules.
   
4. **Interactive Dashboard**:
   Simply run the `menu` command in your terminal to manage accounts, renew users, create trial accounts, or view live traffic statistics.
