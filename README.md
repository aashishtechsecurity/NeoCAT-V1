<div align="center">

# 🐱 NeoCAT V1

### ESP32-S3 Security Research Toolkit — Powered by PCBCupid Glyph S3

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-ESP32--S3-blue.svg)](#hardware)
[![Arduino](https://img.shields.io/badge/Arduino-Compatible-teal.svg)](#flashing)
[![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-brightgreen.svg)](https://github.com/cyberkallan/NeoCAT-V1/pulls)

**A premium, mobile-app-like security research toolkit for ESP32-S3 boards with built-in web dashboard, WiFi analysis, BLE scanning, Captive Portal Cloning, Chat Rooms, and RGB LED control.**

---

`WiFi Scanner` · `BLE Scanner` · `Clone AP` · `Beacon Flood` · `Chat Room` · `RGB LED Control` · `PWA Dashboard`

</div>

---

## ✨ Features

### 📱 Premium Web Dashboard
- **PWA Support** — Install as a native app on your phone (Add to Home Screen)
- **Sliding Navigation** — Green indicator pill smoothly glides between tabs
- **Zero Dependencies** — Everything served from flash, no CDN required
- **Mobile-First** — Designed for phone screens, responsive up to tablet
- **Sleek Mecha-Cat UI** — Cyberpunk-inspired dark theme with smooth gradients

### 📡 WiFi Pentesting
- WiFi network scanning with signal strength, channel, and encryption info
- **Clone AP** — Create an Evil Twin of any network with a built-in Captive Portal (Prank, Hacker, or Rickroll templates)
- Beacon flood with custom SSIDs
- Rickroll beacon flood (pre-loaded funny SSIDs)
- Probe request flood
- Real-time packet counter with live bar chart

### 💬 Chat Room System
- Built-in captive portal chat room (accessible at `192.168.4.1/chat`)
- Real-time WebSocket messaging
- Secure admin dashboard to manage users, kick participants, and clear chat logs

### 📶 BLE Module
- BLE device scanning with name, MAC, and RSSI
- BLE advertisement spam (Apple, Samsung, Windows, All)
- Real-time packet tracking

### 💻 Command Line Terminal
- Live terminal console with timestamped logs
- Direct control over WiFi, BLE, and LED subsystems via commands (e.g. `wifi.scan`, `ble.spam apple`, `led.color FF0000`)
- Built-in `help` command for documentation

### 💡 LED Controller
- Multiple LED modes: Idle, Scanning, Attacking, Off, Custom
- Full RGB color picker with hex display
- Real-time mode switching via web dashboard

---

## 🔧 Hardware

### Supported Boards
| Board | Chip | Flash | Status |
|-------|------|-------|--------|
| PCBCupid Glyph S3 | ESP32-S3 | 8MB | ✅ Tested |
<<<<<<< HEAD
| ESP32 Dev Module | ESP32-D0WD-V3 | 4MB | ✅ Tested |
=======
>>>>>>> 786213442cf4ac133b7cc0c7150bcd7fdab4e2a8
| ESP32-S3-DevKitC-1 | ESP32-S3 | 8MB | ✅ Compatible |
| ESP32-S3-WROOM-1 | ESP32-S3 | 8MB | ✅ Compatible |
| Any ESP32-S3 board | ESP32-S3 | 4MB+ | ⚠️ Should work |

### Pin Requirements
<<<<<<< HEAD
- **RGB LED**: WS2812B / NeoPixel on **GPIO23** (modified from GPIO7 to prevent SPI flash pin conflicts on classic ESP32)
- **Built-in LED**: **GPIO2** (standard ESP32 LED pin)
- **Battery ADC**: **GPIO35** (input-only ADC1 pin)
=======
- **RGB LED**: WS2812B / NeoPixel on GPIO7 (Configurable)
- **USB**: CDC mode for serial communication
>>>>>>> 786213442cf4ac133b7cc0c7150bcd7fdab4e2a8

---

## 📦 Software Requirements

- [Arduino IDE 2.x](https://www.arduino.cc/en/software)
- **ESP32 Board Package** v3.x+ (via Arduino Board Manager)
  - Board Manager URL: `https://espressif.github.io/arduino-esp32/package_esp32_index.json`
- **Required Libraries** (install via Library Manager):
  - `ESPAsyncWebServer` by lacamera
  - `AsyncTCP` by dvarrel
  - `ArduinoJson` by Benoit Blanchon (v7+)
  - `NimBLE-Arduino` by h2zero
  - `Adafruit NeoPixel` by Adafruit

---

## 🚀 Flashing

### Method 1: Arduino IDE (Recommended for Beginners)

1. **Install Arduino IDE** from [arduino.cc](https://www.arduino.cc/en/software)
2. **Add ESP32 Board Package**:
   - Go to `File → Preferences`
   - Add to "Additional Board Manager URLs": `https://espressif.github.io/arduino-esp32/package_esp32_index.json`
   - Go to `Tools → Board → Board Manager`, search "esp32", install **v3.x+**
3. **Install Libraries**:
   - Go to `Sketch → Include Library → Manage Libraries`
   - Search and install the libraries listed in the software requirements section
4. **Configure Board**:
   - Board: `ESP32S3 Dev Module`
   - USB CDC On Boot: `Enabled`
   - Flash Size: `8MB (64Mb)`
   - Partition Scheme: `8M with spiffs` (or custom partitions.csv)
   - PSRAM: `Disabled` (Unless your board has PSRAM)
5. **Upload**:
   - Open `NeoCAT_v1/NeoCAT_v1.ino`
   - Connect board, select port, and hit Upload

---

## 🎮 Usage Guide

### 1. Connect
1. Power on the ESP32-S3. The LED will pulse blue.
2. Connect to the WiFi network: **NeoCAT V1** (No password)
3. Open your browser and go to `http://192.168.4.1`

### 2. Dashboard Tabs
- **Terminal**: Type commands to manually control the board. Check `help` for a full list.
- **WiFi**: Scan networks, select targets, start Evil Twin Clone APs, or run Beacon/Probe floods.
- **BLE**: Scan for nearby Bluetooth devices or launch Apple/Samsung/Windows connection spam.
- **Chat**: Enable the Captive Portal Chat room. Users connecting to the network will be redirected to a localized, offline messaging app.
- **LED**: Manually set colors or let the system indicate current status.

---

## ⚠️ Disclaimer

This project is for educational and security research purposes only. **Only use these tools on networks and devices you own or have explicit permission to test.**

The author is not responsible for any misuse or damage caused by this tool.

---

<div align="center">
  <b>Developed by Arjun TM (<a href="https://github.com/cyberkallan">@cyberkallan</a>)</b><br>
  <b>4MB Dev Kit Port by <a href="https://instagram.com/Aashishtechsecurity">@Aashishtechsecurity</a></b>
</div>
