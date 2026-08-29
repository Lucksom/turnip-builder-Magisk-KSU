# 🚀 Turnip Mesa Vulkan Drivers – Flashable Modules for Magisk & KernelSU

![License](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)

This repository provides **automatically built, system-wide flashable Magisk / KernelSU / APatch modules** for the highly optimized Mesa Turnip Vulkan drivers compiled by [Balemuni](https://github.com/Balemuni/Balemunis-Aurora).

By default, Balemuni's driver releases are designed to be loaded manually inside emulators (like Yuzu, Vita3K, or Winlator). **This repository automates the process of converting those emulator-only drivers into system-wide graphics overlays.** Flashing these modules updates your Android operating system's default Adreno Vulkan drivers without permanently modifying your device's read-only system partitions.

---

## 📦 Available Variants

Our GitHub Actions script automatically pulls the latest releases from upstream and generates two distinct modules:

### 1. 🌐 Turnip Apex – Universal Edition V2
* **Hardware Support:** Compatible with all Adreno GPUs across the 6xx, 7xx, and 8xx architectures (including Snapdragon 8 Gen 3 and Snapdragon 8 Elite Gen 4/5).
* **Target Audience:** Anyone using an Android 13+ device with an Adreno GPU (except Snapdragon 8 Gen 2 flagships). This provides the safest baseline instruction set for maximum compatibility.

### 2. ⚡ Turnip Apex – Ultimate Edition V2 (SD8 Gen 2)
* **Hardware Support:** Exclusively optimized for **Snapdragon 8 Gen 2 (Adreno 740)** devices.
* **Target Audience:** Users with high-end gaming hardware (AYN Thor, Odin 2, RedMagic 8, Galaxy S23). This build contains aggressive instruction-level tuning specifically for Cortex-X3 prime cores.

### 🌟 Key Upstream Enhancements
Both module variants include Balemuni's upstream optimizations:
* **Global Code Motion (GCM):** Reduces register pressure and improves framerate consistency in the IR3 compiler.
* **Expanded Shader Cache (4 GB):** Prevents premature shader eviction and reduces compilation stutter in large titles.
* **Zelda Artifact Fixes:** Resolves black blocks and terrain artifacts in Tears of the Kingdom and Breath of the Wild via GMEM tuning.
* **Advanced Cache Cleanup:** Our automated packaging includes a custom `uninstall.sh` script that automatically purges stale `*shader*`, `*gpucache*`, and `*graphitecache*` files when the module is removed, preventing bootloops caused by conflicting caches.

---

## ⚙️ Installation Instructions

**Prerequisites:** You must have a rooted Android device (Android 13 or newer) with an Adreno GPU, running [Magisk](https://github.com/topjohnwu/Magisk), [KernelSU](https://kernelosu.org/), or [APatch](https://apatch.dev/).

1. Go to the [Releases page](../../releases/latest) of this repository.
2. Download the `.zip` file that matches your hardware (`Universal` or `Ultimate-SD8G2`).
3. Open your root manager app (Magisk, KernelSU, or APatch).
4. Navigate to the **Modules** tab.
5. Select **Install from storage** and choose the downloaded `.zip` file.
6. Once flashing is complete, **Reboot** your device.

---

## 🔍 How to Verify Driver Installation

You can confirm that the Mesa Turnip driver has successfully overwritten the stock Qualcomm driver using the following methods in **Termux** (after typing `su`) or an **ADB Root Shell**:

### 1. Static Binary Signature Test
Check if the active module contains Mesa Turnip driver signatures:

```bash
strings /data/adb/modules/turnip-balemuni-*/system/vendor/lib64/hw/vulkan.adreno.so | grep -i "mesa" | head -n 3
```

**Expected Response:**
```text
mesa_cache.idx
-GL_MESA_pack_invert -GL_MESA_framebuffer_flip_y -GL_MESA_window_pos
mesa_no_error
```
*(If this output appears, the Mesa driver library is confirmed to be installed and actively mounted).*

### 2. Live Runtime Logcat Test
Clear previous system logs and monitor live graphics initialization:

```bash
logcat -c && logcat | grep -iE "turnip|freedreno|tu_"
```

**Instructions:**
1. Run the command above in Termux or ADB.
2. Launch any 3D game or emulator (e.g., Genshin Impact, PPSSPP, Sudachi, or Winlator).
3. Check the terminal window. You will see live logs confirming Turnip is initializing your GPU:

```text
I freedreno: Device created: Adreno (TM) ...
I turnip: Enabling VK_EXT_...
I turnip: Using KGSL DRM backend
```

---

## 🛟 Troubleshooting & Safety

* **Bootloops / Black Screen:** If an experimental build causes UI crashes on your OEM ROM, **do not factory reset**. 
* **Safe Mode Rescue:** Turn your phone completely off. Power it on, and hold **Volume Down** as soon as the boot logo appears until the phone finishes booting. Android will enter **Safe Mode**, automatically disabling all root modules so you can open your root manager and remove the Turnip module cleanly.

---

## 🙏 Credits & Acknowledgments

* **[Balemuni](https://github.com/Balemuni/Balemunis-Aurora):** For maintaining the custom Turnip 26.3.0-devel builds, hardware patches, and the Apex Universal/Ultimate driver releases.
* **[The Mesa 3D Graphics Library](https://gitlab.freedesktop.org/mesa/mesa):** The Freedreno / Turnip open-source developers who reverse-engineered the Qualcomm Adreno architecture.
* **[topjohnwu](https://github.com/topjohnwu/Magisk):** For the Magisk systemless module framework.

---

## ⚖️ License & Disclaimer

**Disclaimer:** This is an unofficial community automation tool. We are not responsible for bootloops or device issues. Please understand what you are flashing before proceeding. 

The build scripts in this repository are licensed under the MIT License. The packaged Mesa Turnip drivers retain their original upstream MIT licensing.
