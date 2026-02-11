# ThinkPad-T560-Sequoia (OpenCore)

![macOS Sequoia](https://img.shields.io/badge/macOS-Sequoia-success?style=flat-square&logo=apple)
![OpenCore](https://img.shields.io/badge/OpenCore-1.0.6-blue?style=flat-square)
![Status](https://img.shields.io/badge/Status-Stable-green?style=flat-square)

Complete OpenCore EFI configuration for the **Lenovo ThinkPad T560**, making it the first known stable build for **macOS Sequoia** on this machine. This configuration bypasses Skylake limitations and fixes critical sleep/wake and connectivity issues.

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

* **SD Card Reader:** Intentionally disabled. Enabling `RealtekCardReader.kext` will cause the system to crash/restart after sleep.
* **AMFI:** Security is partially lowered (`amfi_get_out_of_my_way=1`) to allow Intel Wireless drivers to function on Sequoia.

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

Serials are blanked for security. Use [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) to generate data for **MacBookPro16,2**.

### 2. HeliPort

For WiFi, install the [HeliPort app](https://github.com/OpenIntelWireless/HeliPort) and set it to **Launch at Login**.

---

## ⚖️ License & Disclaimer

This project is licensed under the **MIT License**. This EFI is provided "as is". I am not responsible for any damage or data loss. Use it at your own risk.

## 👏 Credits

* **Apple**: For macOS.
* **Acidanthera**: For OpenCore, Lilu, WhateverGreen, and AppleALC.
* **OpenIntelWireless**: For `itlwm` and Intel Bluetooth drivers.
* **Dortania**: For the master guides.

---
