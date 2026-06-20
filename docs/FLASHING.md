# 🚀 Flashing Guide — NeoCAT V1

Complete step-by-step guide to flash NeoCAT V1 firmware onto your ESP32-S3 board.

---

## Prerequisites

### Hardware
- ESP32-S3 development board with **8MB flash** (4MB may work with reduced partition)
- USB-C cable (data-capable, not charge-only)
- WS2812B / NeoPixel LED (optional, for RGB effects)

### Software
- **Arduino IDE 2.x** — [Download](https://www.arduino.cc/en/software)
- **ESP32 Board Package** v3.x or later
- Required Arduino Libraries (see below)

---

## Step 1: Install ESP32 Board Package

1. Open Arduino IDE
2. Go to **File → Preferences**
3. In "Additional Board Manager URLs", add:
   ```
   https://espressif.github.io/arduino-esp32/package_esp32_index.json
   ```
4. Go to **Tools → Board → Board Manager**
5. Search for **"esp32"** and install **"esp32 by Espressif Systems"** (v3.x+)

---

## Step 2: Install Required Libraries

Go to **Sketch → Include Library → Manage Libraries** and install:

| Library | Author | Version |
|---------|--------|---------|
| ESPAsyncWebServer | lacamera | Latest |
| AsyncTCP | dvarrel | Latest |
| ArduinoJson | Benoit Blanchon | 7.x+ |
| NimBLE-Arduino | h2zero | Latest |
| Adafruit NeoPixel | Adafruit | Latest |

---

## Step 3: Configure Board Settings

Go to **Tools** menu and set:

| Setting | Value |
|---------|-------|
| **Board** | `ESP32 Dev Module` |
| **Flash Size** | `4MB (32Mb)` |
| **Partition Scheme** | `Custom` (using the project's `partitions.csv`) |
| **Upload Speed** | `921600` |
| **CPU Frequency** | `240MHz (WiFi)` |
| **Port** | Select your COM port |

### How the 4MB Flash Migration Works
To allow the NeoCAT V1 firmware (which originally required an 8MB ESP32-S3 layout) to run on a standard 4MB classic ESP32 without losing functionality, the partition layout was compressed:
* **App Space (`app0`)**: Resized from `6.25MB` to `2.875MB (0x2E0000)`. Because the compiled program binary is typically under 1.5MB, this provides more than enough room for the firmware logic and static pages without compromising features.
* **Filesystem (`spiffs`/LittleFS)**: Resized from `1.6MB` to `1.0625MB (0x110000)`. This retains plenty of space for user configuration, chat logs, and custom scripts.
* **Hardware Pins Safety**: Configured to run on standard ESP32 IOs, ensuring GPIO pins connected to SPI Flash are not occupied.

> **Finding your COM port**: 
> - **Windows**: Device Manager → Ports (COM & LPT) → Look for CP210x or CH340 USB-to-UART Bridge
> - **macOS**: `/dev/cu.usbserial-*`
> - **Linux**: `/dev/ttyUSB0` or `/dev/ttyACM0`

---

## Step 4: Flash the Firmware

1. Open `NeoCAT_v1/NeoCAT_v1.ino` in Arduino IDE
2. Connect your ESP32-S3 via USB
3. Select the correct COM port in **Tools → Port**
4. Click the **Upload** button (→ arrow)
5. Wait for compilation and upload to complete

### Expected Output
```
Sketch uses 1258772 bytes (37%) of program storage space.
Global variables use 50980 bytes (15%) of dynamic memory.
...
Writing at 0x00010000... (100 %)
Hash of data verified.
```

> ⚠️ **"Serial exception" after flashing** — This is **NORMAL** for ESP32-S3 with USB CDC. The board resets its USB connection after flashing, causing pySerial to lose the port momentarily. Your flash was successful if you see "Hash of data verified."

---

## Step 5: First Boot

1. The board will restart automatically after flashing
2. Look for WiFi network **"NeoCAT V1"** on your phone/laptop
3. Connect to it (no password required)
4. A captive portal should auto-open the dashboard
5. If not, open your browser and navigate to **`http://192.168.4.1/`**
6. Accept the legal disclaimer (shown only on first visit)
7. You're in! 🎉

---

## Troubleshooting

### Board not detected on USB
- Try a different USB cable (must be data-capable)
- Try a different USB port
- Install [CP2102 drivers](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers) if needed
- On ESP32-S3: hold **BOOT** button, press **RESET**, then release **BOOT** to enter download mode

### Compilation errors
- Ensure all libraries are installed (Step 2)
- Ensure ESP32 board package is v3.x+ (Step 1)
- Check that board is set to "ESP32S3 Dev Module" (not ESP32 or ESP32-S2)

### WiFi "NeoCAT V1" not appearing
- Wait 5-10 seconds after power-on
- Check serial monitor (115200 baud) for boot messages
- Ensure the flash was successful

### Dashboard not loading
- Ensure you're connected to "NeoCAT V1" WiFi
- Try `http://192.168.4.1/` directly in browser
- Clear browser cache and try again

### Full Erase (Nuclear Option)
If nothing works, do a full erase and reflash:
```bash
# Using esptool (found in Arduino15/packages/esp32/tools/esptool_py/)
esptool.exe --chip esp32 --port COM9 erase_flash

# Then re-flash using Arduino IDE
```

---

## Arduino CLI Commands (Quick Reference)

```bash
# Compile only
arduino-cli compile \
  --fqbn "esp32:esp32:esp32:FlashSize=4M" \
  --build-property "build.partitions=partitions" \
  NeoCAT_v1/

# Compile and upload
arduino-cli compile --upload \
  -p COM9 \
  --fqbn "esp32:esp32:esp32:FlashSize=4M" \
  --build-property "build.partitions=partitions" \
  NeoCAT_v1/

# Upload only (if already compiled)
arduino-cli upload \
  -p COM9 \
  --fqbn "esp32:esp32:esp32:FlashSize=4M" \
  NeoCAT_v1/

# Monitor serial output
arduino-cli monitor -p COM9 --config baudrate=115200
```

---

<div align="center">

**NeoCAT V1** — Powered by **Glyph S3**

</div>
