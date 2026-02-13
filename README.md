# ThinkPad-T560-Sequoia (OpenCore)

![macOS Sequoia](https://img.shields.io/badge/macOS-Sequoia-success?style=flat-square&logo=apple)
![OpenCore](https://img.shields.io/badge/OpenCore-1.0.6-blue?style=flat-square)
![Status](https://img.shields.io/badge/Status-Stable-green?style=flat-square)

Complete OpenCore EFI configuration for the **Lenovo ThinkPad T560**, making it the first known stable build for **macOS Sequoia** on this machine. This configuration bypasses Skylake limitations and fixes critical sleep/wake and connectivity issues.

<img width="1920" height="1080" alt="mac" src="https://github.com/user-attachments/assets/be93bf47-ce30-44a8-b1c6-be1d9604b465" />

---

## 💻 Hardware Specification

| Component | Specification | Status |
| --- | --- | --- |
| **CPU** | Intel Core i7 6600u (Skylake) | ✅ Working (via `-no_compat_check`) |
| **iGPU** | Intel HD Graphics 520 | ✅ Working (Spoofed to Kaby Lake) |
| **dGPU** | NVIDIA GeForce 940MX | ⛔ Disabled (via SSDT) |
| **Audio** | Realtek ALC293 | ✅ Working (Layout ID: 28) |
| **WiFi** | Intel AC 8260 | ✅ Working (`itlwm.kext` + HeliPort) |
| **Bluetooth** | Intel Bluetooth | ✅ Working (Tested with Beats) |
| **Ethernet** | Intel I219-V | ✅ Working |
| **Input** | Synaptics Trackpad & TrackPoint | ✅ Working (with Gestures) |
| **SD Reader** | Realtek RTS522A | ⚠️ Disabled (See Notes) |
| **Camera** | None (Corporate Model) | ⛔ Not present |

---

## ✅ What Works

* **Graphics:** Full acceleration on HD 520 (MacBookPro16,2 spoof).
* **Connectivity:** WiFi via HeliPort and Bluetooth with Sequoia fixes.
* **Sleep/Wake:** 100% stable. Fixed via `SSDT-GPRW` and `SSDT-PTSWAK` with proper ACPI patches.
* **Power Management:** Battery status and CPU power management working natively.
* **USB:** Fully mapped. Bluetooth port set to Internal (255) to prevent sleep wake loops.

## ❌ Known Issues

* **NVIDIA 940MX**: macOS does not support Optimus technology. The discrete GPU is disabled via ACPI (SSDT) to save battery.
* **SD Card Reader**: Intentionally disabled. Enabling `RealtekCardReader.kext` will cause the system to crash/restart after sleep.
* **Special Keys**: Dedicated keys for Calculator, Lock, Web Browser, and File Explorer do not function.
* **DRM**: DRM content (Netflix/Apple TV+ in Safari) might not work (common iGPU limitation). Use Chromium/Firefox.
* **You tell me!**

---

## ⚙️ BIOS Settings

* **Config -> Serial Port:** Disabled
* **Config -> Network -> Wake On LAN:** Disabled
* **Security -> Secure Boot:** Disabled
* **Security -> Security Chip:** Disabled
* **Startup -> CSM Support:** No (UEFI Only)

---

## 📝 Installation & Post-Install

### 1. SMBIOS
Serials are blanked for security reasons. Use [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) to generate data for **MacBookPro16,2**.

### 2. Function Keys (YogaSMC)
The YogaSMC.kext is included in the EFI. To get the on-screen display (OSD) for volume/brightness and full function key support:
Download and install the YogaSMC App (Settings pane) inside macOS.

### 3. HeliPort
For WiFi, install the [HeliPort app](https://github.com/OpenIntelWireless/HeliPort) and set it to **Launch at Login**.

---

## ⚖️ License & Disclaimer

This project is licensed under the **MIT License**. This EFI is provided "as is". I am not responsible for any damage or data loss. Use it at your own risk.

## 👏 Credits

* [Apple](https://apple.com) for macOS.
* [Acidanthera](https://github.com/acidanthera) for OpenCore, Lilu, WhateverGreen, and AppleALC.
* [Dortania](https://dortania.github.io/OpenCore-Install-Guide/) for the extensive guides.
* [OpenIntelWireless](https://github.com/OpenIntelWireless) for Intel WiFi drivers.

---
