
# Guide: Kali NetHunter on OnePlus 6T (Android 15)

The official Kali NetHunter installer is currently only compatible up to Android 12. If you try to flash it on Android 15, you will face bootloops or brick yout phone. This guide explains the **"Frankenstein Method"**: swapping the legacy kernel with a modern one to get full packet injection and monitor mode on **LineageOS 22.2**  with compatible external antennas.


## 📦 Prerequisites

* **Phone:** OnePlus 6T with unlocked bootloader 
(Check XDA forums or Google it if you don't know how to do it.)
* **ROM:** LineageOS 22.2 (Android 15) [LineageOS 22.2](https://download.lineageos.org/devices/fajita/builds) 
(If they updated the version to a newer one on LineageOS download page you can still get it [on my SourceForge](https://sourceforge.net/projects/lineageos-22-2-oneplus-6t/).)
* **Flash Images:** `boot.img`, `dtbo.img`, and`vbmeta.img`.
(If they updated the version to a newer one on LineageOS download you can't use those *.img files, don't worry, you can still get it [on my SourceForge](https://sourceforge.net/projects/lineageos-22-2-oneplus-6t/).)
* **Kernel:** [Loukious kernel](https://github.com/Loukious/nethunter_kernel_oneplus_sdm845/releases/tag/nethunter-22.2) (Download the **`Image.gz-dtb`**).
* **NetHunter:** Official AIO Package for OnePlus 6/6T from [Kali.org](https://www.kali.org/get-kali/#kali-mobile). 
(You'll see that when you download the ZIP file, the name contains "los-twelve" at the end, which is why it won't work for us directly.)
* **Magisk:** Download the latest Magisk version .APK on the official repo [Magisk Latest](https://github.com/topjohnwu/Magisk/releases/latest).

---

## 🛠️ Step 1: Flashing the Base (LineageOS 22.2)

Download and perform a clean installation of LineageOS 22.2 by following the official instructions on the [LineageOS Wiki for OnePlus 6T](https://wiki.lineageos.org/devices/fajita/).

---

## 🏗️ Step 2: The "Frankenstein" Kernel Swap

We are going to replace the old kernel inside the installer with the new one from Loukious.

1. **Get the files:** Have the **Official NetHunter AIO ZIP** and the new **`Image.gz-dtb`** ready.
2. **Extract the kernel zip:** Open the AIO ZIP and drag the `kernel-nethunter.zip`.
3. **Swap the file:**
   * Open `kernel-nethunter.zip` (using 7-Zip or WinRAR).
   * Delete the old `Image.gz-dtb` inside.
   * Drag and drop your **new** `Image.gz-dtb` into it.
4. **Flash:** Install the final `kernel-nethunter.zip`  with Recovery:
   * Enter Recovery
   * Apply update
   * Apply from ADB
   * On your PC: ``adb sideload kernel-nethunter.zip`` 
   (If verification fails click **``Yes``**)
   * Wait until it's done.
   * Reboot to system.
5. **Done!** You now have the NetHunter Kernel installed.

> **Note:** We perform the installation this way because using the full, unmodified Kali AIO suite that they provide on the website with all the tools and apps installed on Android 15 will cause bootloops. We will address this on Step 4.

<details>
  <summary>Magisk Root (Image)</summary>
![enter image description here](https://raw.githubusercontent.com/r0grr/Guide-Kali-NetHunter-on-OnePlus-6T-Android-15/refs/heads/main/images/Settings.png)
  
</details>

---

## 💉 Step 3: Rooting with Magisk

After flashing the modified kernel and confirm that the phone boots to LineageOS, you MUST flash Magisk. If you skip this, you will lack root permissions, leaving the NetHunter environment and the Chroot completely useless.

1. **Rename APK to ZIP:** `Magisk-vXX.X.apk` to `Magisk-vXX.X.zip`.
2. **Flash:**
   * Enter Recovery
   * Apply update
   * Apply from ADB
   * On your PC: ``adb sideload Magisk-vXX.X.zip`` 
   (If verification fails click **``Yes``**)
   * Wait until it's done.
   * Reboot to system.
3. **Open Magisk app**
   * Click **Install**
    * Choose **Direct install (Recommended)**
    * Wait until it's done
    * Reboot
4. **Done!** You now have root!

<details>
  <summary>Magisk Root (Image)</summary>
![enter image description here](https://raw.githubusercontent.com/r0grr/Guide-Kali-NetHunter-on-OnePlus-6T-Android-15/refs/heads/main/images/Magisk.png)
  
</details>

---

## 📱 Step 4: NetHunter App Store & Essential Apps

Now that your kernel is ready, you need the software interface to manage the Kali environment.

1. **Install NetHunter Store:** Download and install the Store APK from [store.nethunter.com](https://store.nethunter.com/).
2. **Download Essential Apps:** Open the NetHunter Store and install:

| Application  | Purpose |
|--|--|
| **NetHunter App** | Central control hub for all NetHunter attacks, services, and configuration |
|**NetHunter Terminal**|Command-line interface required to access the Kali (chroot) environment.|
|**NetHunter KeX**|Desktop experience provider; allows running the full Kali GUI on your phone or external monitor.|

4. **Initialize the Chroot:**
   * Open the **NetHunter App**.
   * It will ask for Root permissions (grant them via the pop-up from Magisk).
   * Navigate to **"Kali Chroot Manager"**.
   * Click **Install Kali Chroot** > *Download latest Kali Chroot from official image*
   * Click **Ok** and wait untill it's done, don't kill the app and keep the screen on.
5. If everything went well, click **Start** and check if almost everything turns green and says *Running!* on top.

<details>
  <summary>Chroot OK (Image)</summary>
![enter image description here](https://raw.githubusercontent.com/r0grr/Guide-Kali-NetHunter-on-OnePlus-6T-Android-15/refs/heads/main/images/NetHunter_Chroot.png)
  
</details>

> **Note**:  Check [Kali Nethunter Documentation](https://www.kali.org/docs/nethunter/) if you have any doubts or troubles.
