# VPN Setup Guide – Forge Server 🛡️

This document details the configuration of a VPN to enable secure, remote access to the Forge Server environment. A VPN ensures that all lab access is encrypted, controlled, and ready for IAM simulation or remote support activities.

---

## 🔧 Purpose

- Enable secure remote access for IAM roleplay and AD provisioning tests
- Simulate enterprise access control scenarios
- Provide encrypted tunnels for AI service testing (Meetily, Ollama)
- Future-proof for integration into SIEM logs and event tracking

---

## 🧱 Recommended VPN Tools

### ✅ WireGuard (Preferred)
- Lightweight and modern
- Simple configuration
- Strong encryption (Curve25519, ChaCha20)

### 🛡️ Alternative: OpenVPN
- More traditional
- Larger community support
- Supports MFA plugins and advanced routing

---

## 🔨 Basic Setup Overview – WireGuard (Local Only)

> Note: This section assumes installation on Linux or Windows

### 1. Install WireGuard:
- Linux: `sudo apt install wireguard`
- Windows: Download installer from https://www.wireguard.com/install

### 2. Generate Keys:
Run this in your terminal or PowerShell:
- `wg genkey | tee privatekey | wg pubkey > publickey`

### 3. Configure Interface:
Create a file named `wg0.conf` with the following:
[Interface]
PrivateKey = <your_private_key>
Address = 10.0.0.1/24
ListenPort = 51820

[Peer]
PublicKey = <client_public_key>
AllowedIPs = 10.0.0.2/32


### 4. Start VPN:
- `sudo wg-quick up wg0`

---

## 🔐 Security Recommendations

- Use firewall rules to block public access to the VPN port
- Enable IP forwarding only when testing routing
- Log all VPN connections for potential SIEM ingestion
- Consider adding two-factor VPN access in future upgrade

---

## 🛠️ Future Enhancements

- Integrate VPN logs into a local SIEM like Wazuh or Graylog
- Simulate IAM support tasks via VPN sessions
- Launch Forge Server remote sessions using SSH over VPN only
- Test endpoint hardening with VPN-required access scenarios

---

## 🔍 Reference Materials

- WireGuard Documentation: https://www.wireguard.com
- OpenVPN Community: https://openvpn.net/community-resources/
- Guide: WireGuard on Ubuntu: https://www.cyberciti.biz/faq/ubuntu-22-04-lts-set-up-wireguard-vpn/

---

## 📍 Status

VPN is in design or deployment phase. Details will be updated as configurations are implemented.

