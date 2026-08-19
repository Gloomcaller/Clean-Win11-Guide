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

## Step 4: Skipping the Internet Check (The OOBE Bypass)

Windows 11 forces you to connect to Wi-Fi and sign in with a Microsoft account during setup. We bypass this to create a local, offline account instead.

1. When you reach the **Let's connect you to a network** screen, press **Shift + F10** on your keyboard.
   - On some laptops, you may need to press **Shift + Fn + F10**.
2. A black Command Prompt window will appear. Type `start ms-cxh:localonly` and press **Enter**.
3. The local account creation screen will appear immediately. Fill in your username and password.
   - You can leave the password blank if you want the PC to boot straight to the desktop without typing a password.
4. Click **Next** and complete the setup.

> [!TIP]
> If `start ms-cxh:localonly` does not work for some reason, try the classic method instead:
> - In the Command Prompt (Shift + F10), type `OOBE\BYPASSNRO` and press Enter.
> - Your PC will restart. When it comes back, click **I don't have internet** > **Continue with limited setup**.
> - If that also fails, type `taskmgr` in Command Prompt, find "Network Connection Flow" in Task Manager, and click **End Task**.

---

Once you have created your account, Windows will prepare your desktop. This may take a few minutes. Proceed to Step 5.

## Step 5: First Boot and Critical Drivers

Once Windows prepares your desktop, you will be logged in and ready to go. First, connect to the internet and install all necessary drivers.

### Connect to the Internet

1. Click the network icon in the bottom-right corner of the taskbar.
2. Connect to your Wi-Fi network or plug in an Ethernet cable.

> [!TIP]
> If you don't see your Wi-Fi network, Windows may be missing the drivers for your Wi-Fi card. Download the Wi-Fi drivers from your motherboard or laptop manufacturer's website using your phone, transfer them via USB cable, and install them on your PC.

### Install Windows Updates

1. Open **Settings** (press **Windows + I** or right-click the Start Menu and select Settings).
2. Go to **Windows Update** and click **Check for updates**.
3. Install all available updates. Restart if prompted.
4. **Repeat this 2-3 times** until no more updates appear. Some updates are installed in stages.

### Install GPU and Chipset Drivers

Windows Update usually installs basic display drivers, but for the best performance and stability, you should install the latest drivers directly from your hardware manufacturer.

- **NVIDIA GPUs:** Download from https://www.nvidia.com/en-us/drivers/
- **AMD GPUs:** Download from https://www.amd.com/en/support
- **Intel GPUs and Chipset:** Download from https://www.intel.com/content/www/us/en/support/detect.html

Download and install the appropriate driver for your hardware, then restart your PC.

---

Once your drivers are installed and your PC has restarted, proceed to Step 6.

## Step 6: Activating Windows 11

If you haven't already activated Windows, you can use Microsoft Activation Scripts (MAS) to permanently activate your system for free.

---

Option A: PowerShell Method (Recommended)

1. Open PowerShell as Administrator (right-click Start Menu > Terminal (Admin)).
2. Copy and paste this command and press **Enter**:
   `irm https://massgrave.dev/get | iex`
3. The MAS menu will appear. Type the number corresponding to one of the **Green** options (e.g., HWID for permanent Windows activation) and press Enter.
4. Follow the on-screen instructions.

---

Option B: Offline Method

Use this method if you prefer downloading a file or cannot use the PowerShell method.

1. Download the script from the official MAS repository:
   - Direct script: [MAS_AIO.cmd](https://github.com/massgravel/Microsoft-Activation-Scripts/raw/master/MAS_AIO.cmd)
   - Or download [MAS_AIO.zip](https://github.com/massgravel/Microsoft-Activation-Scripts/raw/master/MAS_AIO.zip) if the direct script is blocked by your browser.
2. Run the `MAS_AIO.cmd` file.
3. In the menu that appears, type the number corresponding to one of the **Green** options (e.g., HWID for permanent Windows activation).

> [!CAUTION]
> The `irm` command downloads a script from a URL and `iex` executes it. Always double-check the URL before running the command and verify the source is trustworthy. Be cautious of third parties spreading malware disguised as MAS by altering the URL.

---

Once activation is complete, proceed to Step 7.
