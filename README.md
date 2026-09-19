# Analog_WLED_RGB_Controller

# ESP32-S3 Analog RGB WLED Controller

An open-source hardware controller for **12 V analog RGB LED strips**, built around the **ESP32-S3-WROOM-1** and designed for WLED.

The controller uses three low-side N-channel MOSFET switches to independently control the Red, Green, and Blue channels of a 12 V analog RGB strip using PWM. It also includes onboard power regulation, USB-C connectivity, ESD protection, and an I2S digital MEMS microphone for sound-reactive WLED effects.

The hardware is designed around a **3 A RGB strip load target** and a 12 V input supply.

---

## Features

### MCU

- **ESP32-S3-WROOM-1**
- Wi-Fi and Bluetooth LE
- Native USB support
- Hardware PWM for RGB control
- 3.3 V logic

### RGB LED Control

- 3 independent low-side MOSFET channels
- **IRLZ44N** N-channel logic-level MOSFETs
- PWM-controlled Red, Green, and Blue channels
- Designed for **12 V common-anode analog RGB LED strips**
- Target RGB strip load: **up to 3 A**
- Separate MOSFET switching for each RGB channel

The RGB strip's positive terminal is connected directly to the +12 V supply.  
The three color channels are switched on the low side by the MOSFETs.

### Power Management

The board uses a two-stage buck-converter power architecture:

**12 V → 5 V → 3.3 V**

- 12 V DC input
- Replaceable input fuse
- Reverse/transient protection using `SMBJ43A`
- `LMR51430YDDCR` synchronous buck converter for **12 V → 5 V**
- Second `LMR51430YDDCR` buck converter for **5 V → 3.3 V**
- Separate regulated rails for the ESP32-S3 and microphone
- High-efficiency switching regulation

### Audio Reactive

- Onboard `MSM261S4030HDR` digital I2S MEMS microphone
- Direct connection to the ESP32-S3 I2S peripheral
- Intended for WLED Sound Reactive effects
- No external analog microphone amplifier required

### USB-C

- USB-C connector
- USB 2.0 data connection to the ESP32-S3
- `USBLC6-2SC6` ESD protection
- USB power/data interface for programming and configuration

---

# Electrical Architecture

The controller is divided into four main sections:

```text
                 +----------------------+
                 |      12 V INPUT      |
                 +----------+-----------+
                            |
                     Fuse + Protection
                            |
              +-------------+-------------+
              |                           |
              |                           |
          RGB LED Strip              12 V → 5 V
              |                      Buck Converter
              |                           |
              |                          +5 V
              |                           |
        +-----+-----+                 5 V → 3.3 V
        |           |                 Buck Converter
       Red       Green / Blue             |
        |           |                    +3.3 V
     MOSFETs     MOSFETs                  |
        |           |              +------+------+
        +-----+-----+              |             |
              |                 ESP32-S3       I2S Mic
             GNDconverter for **5 V → 3.3 V**
- Separate regulated rails for the ESP32-S3 and microphone
- High-efficiency switching regulation

### Audio Reactive

- Onboard `MSM261S4030HDR` digital I2S MEMS microphone
- Direct connection to the ESP32-S3 I2S peripheral
- Intended
