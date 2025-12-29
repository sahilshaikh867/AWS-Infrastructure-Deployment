# 🕵️ Evil Twin Wi‑Fi Attack Lab (Educational)

A controlled **security lab** to understand how Evil Twin Wi‑Fi attacks work, how attackers clone access points and how to defend against them.

> ⚠️ For learning only, inside an isolated lab. Not for attacking real networks.

---

## 🎯 Goal

- Learn **how Evil Twin attacks work** in practice.  
- Understand what misconfigurations and user behaviors make them successful.  
- Practice defensive thinking: what to change to reduce risk.

---

## 🧪 Lab Environment

- **Attacker**: Kali Linux VM + compatible Wi‑Fi adapter (monitor mode)  
- **Victim**: Test device or VM using lab Wi‑Fi only  
- **AP**: Test router / simulated AP (not a real production network)  

---

## 📚 Concept Recap

An _Evil Twin_ is a rogue wireless access point that:

- Uses the **same SSID** as a legitimate network  
- Broadcasts a stronger signal or kicks clients off the real AP  
- Lures victims to connect to the attacker’s AP  
- Intercepts traffic or steals credentials (often via fake login pages)  

---

## 🔁 Lab Flow (High‑Level)

1. **Reconnaissance**
   - Use tools like `airodump-ng` to scan for nearby SSIDs.
   - Identify the target lab SSID (e.g. `Campus-WiFi-LAB`), channel, security type.

2. **Set Up Evil Twin AP**
   - Configure a fake AP with the same SSID & channel (hostapd/airbase‑ng).
   - Enable DHCP/DNS to redirect clients to the attacker machine.

3. **Create Captive Portal / Phishing Page**
   - Simple HTML page mimicking a Wi‑Fi login portal.
   - Form posts credentials to the attacker’s HTTP server/logs.

4. **Force or Simulate Victim Connection**
   - In the lab, disconnect victim from real AP.
   - Connect it to the Evil Twin AP (manually or via deauth in lab only).

5. **Credential Capture & Analysis**
   - Victim enters credentials into fake portal.
   - Attacker captures the credentials in logs.
   - Analyze:
     - What data was exposed
     - How user could have noticed

6. **Defense Discussion**
   - Review mitigation strategies:
     - WPA2‑Enterprise / WPA3
     - HTTPS & certificate awareness
     - VPN on untrusted networks
     - Wireless intrusion detection where possible

---

## 🧱 Example Tooling

- Kali Linux
- `airmon-ng`, `airodump-ng` for scanning
- `airbase-ng` / `hostapd` for fake AP
- Simple web server (Python/Node/PHP) for portal
- Browser on victim machine

---

## 🧠 What Was Learned

- Practical understanding of **wireless attack surface**.  
- Why **open / weakly secured Wi‑Fi** is dangerous.  
- Importance of **user education** and **network hardening**.  
- How to discuss these attacks from a **defender’s point of view**.

---

## 🔐 Ethics & Safety

- Run only in a **closed lab**, never on shared or public networks.  
- Do **not** capture real user credentials or sensitive data.  
- Use this project to explain and **prevent** attacks, not perform them.
