# 🚀 Turnip Mesa Vulkan Drivers – Flashable Modules for Magisk & KernelSU

![Build Status](https://img.shields.io/github/actions/workflow/status/YOUR-USERNAME/YOUR-REPO/build-turnip.yml?label=Auto-Builder&style=for-the-badge)
![Latest Release](https://img.shields.io/github/v/release/YOUR-USERNAME/YOUR-REPO?label=Latest%20Release&style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)

This repository provides **automatically built, system-wide flashable Magisk / KernelSU / APatch modules** for the highly optimized Mesa Turnip Vulkan drivers compiled by [Balemuni](https://github.com/Balemuni/Balemunis-Aurora).

By default, Balemuni's driver releases are designed to be loaded manually inside emulators (like Yuzu, Vita3K, or Winlator). **This repository automates the process of converting those emulator-only drivers into system-wide graphics overlays.** Flashing these modules updates your Android operating system's default Adreno Vulkan drivers without permanently modifying your device's read-only system partitions.

---

## 📦 Available Variants

Our GitHub Actions script automatically pulls the latest releases from upstream and generates two distinct modules:

### 1. 🌐 Turnip Apex – Universal Edition
* **Hardware Support:** Compatible with all Adreno GPUs across the 6xx, 7xx, and 8xx architectures (including Snapdragon 8 Gen 3 and Snapdragon 8 Elite Gen 4/5).
* **Target Audience:** Anyone using an Android 13+ device with an Adreno GPU (except Snapdragon 8 Gen 2 flagships). This is the safest baseline instruction set for maximum compatibility.

### 2. ⚡ Turnip Apex – Ultimate Edition (SD8 Gen 2)
* **Hardware Support:** Exclusively optimized for **Snapdragon 8 Gen 2 (Adreno 740)** devices.
* **Target Audience:** Users with high-end gaming hardware (AYN Thor, Odin 2, RedMagic 8, Galaxy S23). This build contains aggressive instruction-level tuning specifically for Cortex-X3 prime cores.

*Both variants include major upstream fixes, including 4GB expanded shader caches, Global Code Motion (GCM) in the IR3 compiler, and GMEM fixes for terrain artifacts in major emulation titles.*

---

## ⚙️ Installation Instructions

**Prerequisites:** You must have a rooted Android device (Android 13 or newer) with an Adreno GPU, running [Magisk](https://github.com/topjohnwu/Magisk), [KernelSU](https://kernelosu.org/), or [APatch](https://apatch.dev/).

1. Go to the [Releases page](../../releases/latest) of this repository.
2. Download the `.zip` file that matches your hardware (`Universal` or `Ultimate-SD8G2`).
3. Open your root manager app (Magisk, KernelSU, or APatch).
4. Navigate to the **Modules** tab.
5. Select **Install from storage** and choose the downloaded `.zip` file.
6. Once the flashing is complete, **Reboot** your device.
7. *Optional:* You can verify the driver installation using apps like **Vulkan Caps Viewer** from the Play Store to confirm your system Vulkan version now reports as `Turnip`.

---

## 🛟 Troubleshooting & Safety

* **Bootloops/Black Screen:** Because Android relies on Vulkan to render the system UI, installing bleeding-edge graphics drivers system-wide carries a risk of black screens if the driver is incompatible with your specific OEM firmware (like Samsung OneUI or Xiaomi HyperOS). 
* **How to fix:** If your device bootloops, **do not panic or factory reset.** Simply reboot into Safe Mode (usually holding Volume Down during boot). Magisk/KernelSU will automatically disable all modules, allowing you to boot up normally, open the root app, and uninstall the module.

---

## 🙏 Credits & Acknowledgments

This project is simply an automated packager. All credit for the actual driver code, compiling, and specific optimizations goes to the original developers:

* **[Balemuni](https://github.com/Balemuni/Balemunis-Aurora):** For the custom Turnip 26.3.0-devel base, hardware compatibility patches, and maintaining the Apex Universal/Ultimate driver builds.
* **[The Mesa 3D Graphics Library](https://gitlab.freedesktop.org/mesa/mesa):** Specifically the Freedreno / Turnip open-source developers who have tirelessly reverse-engineered the Qualcomm Adreno architecture.
* **[topjohnwu](https://github.com/topjohnwu/Magisk):** For creating the Magisk systemless module framework.

---

## ⚖️ License & Disclaimer

**Disclaimer:** This is an unofficial, community-maintained automation tool. We are not responsible for bricked devices, bootloops, or voided warranties. Please understand what you are flashing before proceeding. 

The build scripts in this repository are licensed under the MIT License. The packaged Mesa Turnip drivers retain their original upstream MIT licensing.
