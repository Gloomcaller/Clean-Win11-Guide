# Clean-Win11-Guide

The only Windows 11 installation guide you'll ever need (I hope).
From a blank USB to a debloated, fully optimized PC without a Microsoft account in sight.

> [!WARNING]
> This process deletes ALL data on the drive you install to.
> Back up your photos, documents, game saves, and browser bookmarks before starting.

If you have a PC or a laptop with no data on the drives, you can ignore the warning since there is nothing to delete.

---

Prerequisites

- A working PC to create the USB drive.
- A USB Flash Drive with at least 8GB of storage (16GB is safer). Ideally use a USB 3.0 drive (blue interior) or faster.
- A stable internet connection (for drivers and app downloads post-install).
- About 30-60 minutes for installation (may take longer on older HDDs), plus additional time for downloading Windows 11 (depends on your internet speed).

---

## Step 1: Creating the Bootable USB Drive

You have two options here. I recommend Option B (the official tool) if your PC is relatively modern (less than 5 years old). Use Option A (Rufus) if you have an older PC, a custom build, or want to bypass Microsoft's strict hardware requirements.

---

Option A: Using Rufus (Best for older PCs)

Rufus allows you to bypass TPM 2.0, Secure Boot, and RAM requirements easily.

1. Download the official Windows 11 ISO from [Microsoft's website](https://www.microsoft.com/software-download/windows11).
2. Download [Rufus](https://rufus.ie/) (the portable version is fine, no installation needed).
3. Open Rufus, select your USB drive, and click **SELECT** to choose the Windows 11 ISO you downloaded.
4. CRITICAL: When Rufus asks about **User Experience**, check the boxes for:
   - Remove requirement for TPM 2.0 / Secure Boot.
   - Remove requirement for an online Microsoft account.
   - (Optional) Set local account and username.
5. Click START and wait for the progress bar to finish. Once done, your USB is ready.

Screenshot reference: assets/rufus-settings.png

---

Option B: Using the Official Windows 11 Media Creation Tool (Recommended for modern PCs)

If your PC meets Windows 11's official hardware requirements (TPM 2.0, Secure Boot, supported CPU), this is the simplest and most reliable method. It automatically downloads the latest version and formats your USB correctly.

1. Go to Microsoft's [Windows 11 download page](https://www.microsoft.com/software-download/windows11).
2. Under **Create Windows 11 Installation Media**, click the "Download now" button to get the Media Creation Tool.
3. Run the tool and accept the license terms.
4. Select **Create installation media (USB flash drive, DVD, or ISO file)** and click Next.
5. Choose the language and edition (usually the default is fine) and click Next.
6. Select **USB flash drive** and click Next.
7. Choose your USB drive from the list and click Next.
8. The tool will download Windows 11 and create the bootable USB automatically (This may take some time depending on your internet speed).
9. Click Finish once done.

Screenshot reference: assets/media-creation-tool.png

---

Whichever option you choose, your USB drive is now ready. Proceed to Step 2.

---

## Step 2: Entering BIOS and Changing Boot Order

Before you can install Windows, you need to tell your computer to boot from the USB drive instead of your hard drive. This is done in the BIOS (Basic Input Output System).

1. Restart your PC with the USB drive plugged in.
2. As soon as the screen turns on (even before the Windows logo appears), **spam the BIOS key** repeatedly. Press it over and over until you enter the BIOS menu.

Common BIOS keys by brand:
- **DEL** - Most common (ASUS, MSI, Gigabyte desktop boards)
- **F2** - ASUS laptops, Dell, Acer
- **F10** - HP
- **F12** - Lenovo, Dell, MSI laptops
- **ESC** - Some HP and Lenovo laptops

If you miss it and Windows starts loading, just restart and try again.

3. Once inside the BIOS, navigate using your arrow keys (mouse may not work). Look for a tab called:
   - **Boot**
   - **Boot Order**
   - **Boot Priority**

4. Find your USB drive in the list. It may be listed as:
   - The brand name of your USB (e.g., "SanDisk", "Kingston")
   - "UEFI: [USB name]"
   - "USB-HDD"

5. Move your USB drive to the **#1 (Top)** position in the boot order.
   - Usually you press **+** or **-** keys, or **F5/F6**, or drag with the mouse if supported.

6. Press **Save and Exit** (usually **F10**) and confirm "Yes" or "OK" when prompted.

Your PC will now restart and boot from the USB drive.

> [!TIP]
> If you don't see your USB drive in the boot list, try the following:
> - Disable **Secure Boot** (usually found in the Security or Boot tab).
> - Enable **CSM** or **Legacy Mode** (if available).
> - Try plugging the USB into a different port (preferably a USB 2.0 port - black or white interior - if USB 3.0 ports are not recognized).

Screenshot reference: assets/bios-boot-menu.jpg

---

Once your PC boots from the USB, you will see a blue Windows setup screen. Proceed to Step 3.

---

## Step 3: Installing Windows and Wiping the Old Drive

Your PC will now boot from the USB drive. You'll see a blue Windows setup screen. Follow these steps carefully.

1. Select your language, time format, and keyboard layout (defaults are usually fine). Click **Next**.
2. Click **Install Now**.
3. When asked for a license key, click **I don't have a product key**. You can activate later with your existing license.
4. Select the edition that matches your license (usually Windows 11 Pro or Home). Click **Next**.
5. Check the box to accept the license terms and click **Next**.
6. **CRITICAL STEP:** Select **Custom: Install Windows only (advanced)**. Do NOT select Upgrade.
7. You will now see a list of partitions on your drive(s). This is where the magic happens.

   - You will see entries like:
     - `Drive 0 Partition 1` (System Reserved)
     - `Drive 0 Partition 2`
     - `Drive 0 Partition 3` (Windows)
     - etc.

   - **THE NUCLEAR STEP:** Select **EVERY** partition on your main drive (usually Drive 0) one by one and click **Delete** for each.

   - After deleting all partitions, the drive should now show as a single entry called **Unallocated Space**.

> [!CAUTION]
> Double-check you are deleting the correct drive! If you have multiple physical drives (e.g., a second SSD or HDD), you can identify them by their size (e.g., 240GB, 500GB, 1TB). Unplug extra drives beforehand if you are unsure.

8. Select the now-empty **Unallocated Space** and click **Next**.
9. Windows will now begin copying files and installing. This will take 10-20 minutes. Your PC will restart automatically during this process.

> [!IMPORTANT]
> Do NOT unplug the USB drive during the installation. You can safely remove it only after the PC restarts and you see the "Let's start with region" screen again.

Screenshot reference: assets/delete-partitions.png

---

After the installation finishes and your PC restarts, you will be greeted by the Windows 11 setup wizard. Proceed to Step 4.
