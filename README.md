# Analog_WLED_RGB_Controller
Analog WLED RGB Controller for 12V Stripes

# ESP32-S3 Analog RGB WLED Controller
An open-source hardware controller designed for **12V Analog RGB LED Strips** powered by the **ESP32-S3-WROOM-1** module and integrated with [WLED](https://github.com/Aircoookie/WLED).
This board features logic-level driven N-channel MOSFET switching, dual buck regulation for high-efficiency power management, an onboard digital I2S MEMS microphone for Sound-Reactive effects, and USB-C connectivity with ESD protection.
---
## Features
* **MCU Core:** ESP32-S3-WROOM-1 (USB native support, Wi-Fi, BLE).
* **LED Control:** 3x Low-side MOSFET channels (`IRLZ44N`) driven directly via ESP32 PWM pins.
* **Power Management:**
  * **12V Input:** Reverse polarity diode protection (`SMBJ43A`) & replaceable fuse (`F1`).
  * **12V → 5V Buck Converter:** LMR51430YDDCR step-down regulator.
  * **5V → 3.3V Regulator:** Secondary LMR51430YDDCR step-down regulator for stable MCU & microphone power.
* **Audio Reactive Capabilities:** Onboard `MSM261S4030HDR` I2S Digital MEMS Microphone for real-time sound synchronization.
* **Connectivity:** USB-C connector (USB 2.0 interface) with USBLC6-2SC6 ESD protection for data/power.
---
## Hardware Specifications & Pinout
### ESP32-S3 GPIO Mapping

| Function | Pin Name | ESP32-S3 GPIO | Description |
| :--- | :--- | :--- | :--- |
| **Red Channel** | `Red` | **IO38** | Low-side PWM output for Red channel |
| **Green Channel** | `Green` | **IO39** | Low-side PWM output for Green channel |
| **Blue Channel** | `Blue` | **IO40** | Low-side PWM output for Blue channel |
| **I2S Mic WS** | `WS` | **IO12** | Word Select (LRCLK) |
| **I2S Mic SCK** | `SCK` | **IO13** | Continuous Serial Clock (BCLK) |
| **I2S Mic SD** | `SD` | **IO14** | Serial Data Out |

---
## Connector Details
### 1. Power Input (`J3`)
* **Pin 1:** +12V DC Input
* **Pin 2:** GND
### 2. RGB Strip Output (`J4`)
* **Pin 1:** +12V VCC (Shared Positive Terminal)
* **Pin 2:** Blue Channel (`Q1` Drain)
* **Pin 3:** Green Channel (`Q2` Drain)
* **Pin 4:** Red Channel (`Q3` Drain)
---
## WLED Configuration Guide
### 1. Initial Setup
1. Flashing WLED: Use the [WLED Web Installer](https://install.wled.me/) to flash standard or Sound-Reactive ESP32-S3 firmware.
2. Connect to the initial `WLED-AP` access point and configure your local Wi-Fi credentials.
### 2. LED Settings
1. Open the WLED web UI and go to **Config** > **LED Preferences**.
2. Set **LED total** to `1`.
3. Under **Hardware setup**, select **Analog RGB** as the LED type.
4. Assign the GPIO pins as follows:
   * **Red:** `38`
   * **Green:** `39`
   * **Blue:** `40`
5. Save settings and restart.
### 3. Sound-Reactive Audio Settings (Optional)
If using Audio-Reactive firmware:
1. Go to **Config** > **Usermods** (or **Audio Settings** depending on version).
2. Set **Digital Microphone Type:** `I2S Generic`
3. Configure I2S Pins:
   * **I2S SD:** `14`
   * **I2S WS:** `12`
   * **I2S SCK:** `13`
---
## Hardware Architecture
