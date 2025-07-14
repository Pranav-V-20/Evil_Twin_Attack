# ESP8266 Evil Twin + Deauthentication Attack

A powerful proof-of-concept tool that **deauthenticates clients** from a legitimate WiFi access point and immediately launches an **Evil Twin** access point with the same SSID — using just an **ESP8266 NodeMCU**.

> ⚠️ **DISCLAIMER:** This tool is strictly for **educational and authorized penetration testing** purposes only. Do not use it on networks you do not own or have permission to test.

---

## 📌 Project Overview

This project demonstrates a full-chain WiFi attack:

1. **Deauth Attack**: Disconnects users from the target AP using 802.11 deauthentication frames.
2. **Evil Twin**: Creates a fake AP with the same SSID.
3. **Phishing Portal**: Captures credentials via a login page hosted on the ESP8266.

---

## 🚀 Features

- 📡 Sends continuous **deauth packets** to disrupt legitimate connections.
- 🔁 Broadcasts a **fake AP** with the same SSID as the original.
- 🎯 Redirects victims to a **login phishing page** via captive portal.
- 💾 Logs captured credentials to serial or SPIFFS (optional).
- 🧠 Fully automated chain: **Deauth → Fake AP → Phishing**

---

## 🧰 Hardware & Software Requirements

| Item               | Details                                 |
|--------------------|------------------------------------------|
| ESP8266 NodeMCU     | WiFi-capable microcontroller             |
| Arduino IDE         | For flashing firmware                   |
| WiFi devices        | Smartphone or PC to test                |
| USB cable           | For programming                         |
| Libraries           | `ESP8266WiFi`, `ESPAsyncWebServer`, `DNSServer` |

---

## ⚙️ How It Works

sequenceDiagram
    participant Attacker as ESP8266
    participant Victim as Phone/Laptop
    participant RealAP as Real WiFi

    Attacker->>RealAP: Send deauth packets
    Victim-->>RealAP: Disconnected
    Attacker->>Victim: Fake AP with same SSID
    Victim->>Attacker: Auto-connects to stronger signal
    Attacker->>Victim: Captive login page
    Victim->>Attacker: Enters credentials
    Attacker->>EEPROM: Stores credentials

---

## 📁 Folder Structure

```
Evil_Twin_Attack/
├── EvilTwin_ESP8266.ino
├── README.md
```

---

## 🔧 Setup Instructions

### 1. Flash Firmware

```bash
git clone https://github.com/yourusername/esp8266-evil-twin-deauth.git
```

Open `evil_twin.ino` in **Arduino IDE**, then:

* Select **NodeMCU 1.0 (ESP-12E Module)**
* Install libraries:

  * `ESP8266WiFi`
  * `ESPAsyncWebServer`
  * `DNSServer`
* Upload sketch to ESP8266

---

## 🧪 Test the Attack

1. ESP8266 starts sending **deauth packets** to clients of `targetSSID`.
2. Victims are forcibly disconnected.
3. A **fake AP** with the same SSID appears immediately.
4. Victims connect automatically to the fake AP.
5. Captive portal **phishing page** pops up asking for credentials.
6. Credentials are stored or printed over serial.

---

## 📋 Sample Captured Credentials

```
[+] SSID: Black Devil
[+] Password: deauther
```

---

## ⚠️ Legal Notice

This tool is designed for **educational use** only. Unauthorized use against networks you do not own or manage is a **crime** in many jurisdictions. Use this only in **lab or CTF environments** with proper consent.
