# Setup Mac Os Sierra 10.12.6 on Mini-ITX Intel PC

- This guide is [based on this build](https://www.tonymacx86.com/threads/success-10-12-4-asus-z170-pro-gaming-i5-6500-970gtx.201607/).
- Also [based on this one](https://www.tonymacx86.com/threads/storks-myhero-build-asus-rog-maximus-viii-hero-i7-6700k-gtx-980.197284/).

Thanks to the authors of these and all the other guides!

Although this guide was written for a specific setup, it can vary from basic specs (cpu, gpu, ram etc). This guide certainly works on the following specs:

- Bios Version 3406
- Asus Z170i Pro Gaming Motherboard (Mini-ITX) (100 series Intel)
- Intel i7 6700K, 4Ghz, LGA1151 (6th Gen Skylake)
- Memory DDR4-2400 G.Skill Ripjaws
- Hard Drive SSD Samsung 850 EVO
- EVGA Nvidia GTX 1050Ti Mini
- Corsair 450SF 450 Watt PSU
- Realtek ALC1150 Supreme FX
- LAN Intel WG-I219V
- WLAN AzureWave AW-CB210NF-P
- Onboard Graphics Intel® HD Graphics
- M.2 Socket 3, with M key, type 2242/2260/2280 storage devices support (both SATA & PCIE mode)
- ASMedia® USB 3.1 controller : 
- 2 x USB 3.1 Gen 2 port(s) (Type-A)
- Intel® Z170 chipset : 
- 6 x USB 3.1 Gen 1 port(s) (4 at back panel, blue, 2 at mid-board)
- Intel® Z170 chipset : 
- 4 x USB 2.0/1.1 port(s) (2 at back panel, black, 2 at mid-board)

Notes on issues with other components:

- M.2 (Micros SSD slot) SSD HDD is not seen by Mac OS 10.12.6
- Onboard Intel Graphics adapter boots to black screen

This guide is based on the excellent guide from [tonymacx68.com](https://www.tonymacx86.com/threads/success-10-12-4-asus-z170-pro-gaming-i5-6500-970gtx.201607/).

## What you will need

The following is required before even attemting to install your Mac OS build:

- 2x 16GB Flash Drives, try to get faster ones (and ones you can store away for re-installation).
- Copy of bootable [Mac OS Sierra](https://www.hackintosh.zone/file/1008-hackintosh-sierra/) iso to build pre-build installation on.
- Latest version of [Unibeast](https://www.tonymacx86.com/resources/categories/tonymacx86-downloads.3/) which is used to create a final bootable Mac OS on. 
- Latest version of [Multibeast](https://www.tonymacx86.com/resources/categories/tonymacx86-downloads.3/) which is used to configure a final post installation bootable Mac OS operating system.

## Mac OS pre-built setup

The pre-built setup is used to create a final installation usb disk for final installation. If you have an existing Mac built this step can be skipped altogether.

**Using Linux (Ubuntu):**

Use the downloaded [Hackintosh Sierra dmg](https://www.hackintosh.zone/file/1008-hackintosh-sierra/) file and extract it with `sudo apt-get install dmg2img`:

	dmg2img -v -i Hackintosh-Sierra-Zone.dmg -o Hackintosh-Sierra-Zone-Uncompress.dmg

Now we are ready to copy the image to a flash drive using `dd`:

	dd if=Hackintosh-Sierra-Zone-Uncompress.dmg of=/dev/sdc bs=1M
	
Note that /dev/sdc should be the location of your flash drive.

More in [detailed instructions](http://redirect.niresh.co/hackintoshsierra.html)...

## Making the UniBeast USB Thumb Drive

Use the tonymacx86 guide [UniBeast: Install macOS Sierra on Any Supported Intel-based PC](https://www.tonymacx86.com/threads/unibeast-install-macos-sierra-on-any-supported-intel-based-pc.200564/). Note: your USB Thumb drive needs to have 7.63 GB of free space to build the UniBeast installation thumb drive. Otherwise, you'll need a 16GB USB thumb drive which is a better size so you can copy the following items to the thumb drive for use in the post installation phase:

- [MultiBeast v9](http://www.tonymacx86.com/downloads) for Sierra which you can probably put on a 8GB USB thumb drive, but a 16GB drive is best
- (EFI Mounter V3)[http://www.tonymacx86.com/downloads.php?do=cat&id=10]
- [KextBeast](http://www.tonymacx86.com/downloads) which you'll use to install the Codec Commander kext
- For proper processor power management, get the SSDT for your processor from [ammulder's Guide](http://www.tonymacx86.com/threads/guide-el-capitan-on-the-skylake-h170n-wifi.178197/#SSDT) and rename it SSDT.aml; I chose the SSDT for my [i7-6700K](http://www.tonymacx86.com/attachments/ssdt-i7-6700k-aml.161866/). Note: ammulder's SSDTs are for non overclocking speeds; for overclocking, you'll need to create a SSDT for your processor using PikeRalpha's ssdtPRGen.sh script located here.
- Rehabman's [Codec Commander kext](https://bitbucket.org/RehabMan/os-x-eapd-codec-commander/downloads) for making the audio (after wakeup from sleep) work which we'll install using KextBeast
- [Clover Configurator](https://www.tonymacx86.com/resources/categories/community-software.10/) for fine tuning
- (Optional) the nVidia Web drivers for the Maxwell chipset cards (750, 750 Ti, 950 Ti, etc). See tonymacx86's sticky thread in the [Graphics forum section](http://www.tonymacx86.com/forums/graphics.13/) or the [tonymacx86 driver list](https://www.tonymacx86.com/nvidia-drivers/).

## Bios Setup

Follow [Step 3](https://www.tonymacx86.com/threads/unibeast-install-macos-sierra-on-any-supported-intel-based-pc.200564/#uefi_settings) in the tonymacx86 guide.

- Update to latest bios version. Mine was updated to 3406.

The following bios settings apply to this motherboard:

- Load Optimized Defaults
- If your CPU supports VT-d -> disable (Not the same as VT-x which is for Virtual Machines and can be left enabled)
- If your system has CFG-Lock -> disable
- Secure Boot Mode =-> disable
- Set OS Type -> Other OS 
- If your system has IO SerialPort -> disable (if you can find it) (N/A)
- If your system has XHCI Handoff -> enabled (N/A)

**Extreme Tweeker**

	AI Overclocker Tuner > X.M.P.
	Extreme Tweeking > Enable​
	
**Advanced Items**

	System Agent (SA) Configuration > VT-d > Disable
	PCH Configuration > IOAPIC 24-119 > Disabled
	USB Configuration > Legacy USB Support > Auto
	USB Configuration > XHCI Hand Off > Enabled
	APM Configuration > Power on by PCI - E/PCI > Disabled​
	
**Boot Menu**

	Fast Boot > Disabled
	Boot Logo Display > Disabled
	Secure Boot > OS Type > Other OS
	Boot Option 1 > USB installer thumb drive (the UEFI choice if there are two entries)​
	Exit > Save Changes​

You are now ready to boot from this flash drive and install a pre-built Mac OS system so we can build our final Unibeast system.

## Installed and booted up

The next step is to create a Unibeast installation medium and going through the [installation steps](https://www.tonymacx86.com/threads/unibeast-install-macos-sierra-on-any-supported-intel-based-pc.200564/).

## Multibeast

For the configuration of the motherboard we are using we will be installing the following kexts by running Multibeast (9.2.0):

All kexts will be installed to `/Library/Extensions` using a file commander/terminal other than finder to get there, if you get a kernel panic you can remove it from this directory;

- Quick Start -> UEFI Boot Mode
- Divers -> Audio -> ALC1150
- Drivers > Audio > 100/200 Series Audio
- Drivers -> Misc -> FakeSMC (Already ticked)
- (Optional) Drivers > Misc > FakeSMC Plugins
- (Optional) Drivers > Misc > FakeSMC HWMonitor Application
- Drivers - Disks -> None
- Drivers -> Network -> IntelMausiEthernet
- Drivers -> USB -> Increase Max Port Limit 200 Series
- Bootloaders -> Clover v2.4k r4063 UEFI Boot Mode + Emulated NVRAM <--- Required if BIOS version is greater than 2202
- Customize -> Graphics Configuration -> Nvidia Web Drivers Boot Flag.
- System Definitions -> iMac 14,2 (Best compatibility, rest will mot likely give you issues independent of what CPU you have).
-  Save <--- Save your MultiBeast configuration file somewhere convenient
- Click on the Install button in the MultiBeast window bottom right hand corner and wait for MultiBeast to finish.
- Important. MultiBeast v9.2.0's FakeSMC Plugins' FakeSMC_GPUSensors.kext has not been updated to support Pascal graphics cards. To prevent Kernel Panics and Reboot
	- Open the installation drive's /Library/Extensions/ folder;
	- Find and trash the FakeSMC_GPUSensors.kext;
	- Delete the Trash.​
- (Optional) If you have a current Nvidia graphics card, copy the Nvidia driver from the thumb drive onto your Desktop, unzip it and install the driver now, but don't reboot when the installer is done, just leave it along as we'll come back to it.
- Drag & drop the Codec Commander zip file from the thumb drive onto your Desktop and un-zip the file. Drag the CodecCommand.kext from the Release folder to the Desktop. Drag the zip & the two folders to the Trash.
- Drag & drop the KextBeast on your Desktop, unzip it and run it; chose to put the kexts in the /Library/Extensions folder. Drag and drop the CodecCommand.kext to a safe place.
- Now you need to install your processor's SSDT.aml, with Clover Configurator mount EFI or use EFI Mounter if you know the drive path.
	- Navigate to EFI > EFI > CLOVER > ACPI > patched folder;
	- Drag & drop the SSDT.aml from the thumb drive ino the ...ACPI > patched folder.​
- Now reboot.
	- IMPORTANT: Due to a quirk with Apple's cache (see the Note in MultiBeast [v9.2.0 Announcement](https://www.tonymacx86.com/threads/multibeast-9-2-update.229691/)), you'll need to rerun MultiBeast v9.2.0 selecting only the following:
	- Drivers > Audio > Realtek ALC1150
	- Drivers > Audio > 100/200 Series Audio
	- Build > Install
	- Reboot after installation is complete​

Finally, since we're using the iMac14,2 system definition, we have to make one more change since Sierra broke wake-up from long (4+hours) sleep. Special thanks to pastrychief for discovering this "fix"; see his Build Description and Post #63 in his Build Description thread for more details. So, in the Terminal, execute the following command:

`bdmesg|grep -y aml`

## Basic configuration with Clover Configurator

Download and install latest [Clover Configurator](http://mackie100projects.altervista.org/download-clover-configurator/) and run it. Now open it and mount EFI partions so we can find `EFI/CLOVER/config.plist` (this is a config file that contains all the information regarding your system) and open this file with Clover Configurator.

First thing we need to do is properly setup your system and SMBIOS by following [this guide](https://www.tonymacx86.com/threads/an-idiots-guide-to-imessage.196827/).

Save config.plist. Backup. Reboot.

After this you should have a proper SMBIOS.

- Sound wont work after reboot yet.
- Nvidia wont work after reboot yet. 

## Nvidia Web Drivers

Now download the nvidia web drivers from the internet and install. The latest version I used was WebDriver-378.05.05.25f01. See [here](https://www.tonymacx86.com/threads/solving-nvidia-driver-install-loading-problems.161256/#Problem6).
 
Dont expect nvidia drivers to work just yet. Reboot, in the Nvidia Control (Nvidia Taskbar Icon) select Nvidia Webdriver, reboot and see it works, if it does work and it did not switch back to the OS X Default driver, you can skip next step, otherwise follow it too.

## Nvidia setup with Clover Configurator.

If it switched back to the OS X Default driver, [follow this guide](https://www.tonymacx86.com/threads/solving-nvidia-driver-install-loading-problems.161256/#Problem6). Instead we will use Clover Configurator.

Reboot. If it works and the task ndivia icon click says you are using Nvidia great, you are done with this step else continue...

Again mount EFI so we can `EFI/CLOVER/config.plist` (this is a config file that contains all the information regarding your system) and open this file with Clover Configurator. 

- Boot -> nvda_drv=1
- Install Drivers -> EmuVariableUefi

From the taskbar click on the nvidia icon select Nvidia and reboot. Should be working now.

## Sound

Test your sound if it is not working do this:

For working audio, boot at least once from your new drive (not the USB), mount your EFI partition, and then run the script from here: [audio_cloverALC-120.command.zip](https://github.com/toleda/audio_CloverALC/blob/master/audio_cloverALC-120.command.zip).
After reboot, audio works fine for me.

## Making NVMe drive work

Check this tutorial out, here is the output of a [generated example](https://www.tonymacx86.com/threads/guide-hackrnvmefamily-co-existence-with-ionvmefamily-using-class-code-spoof.210316/).

	Jasons-iMac:patch-nvme.git jason$ ./patch_nvme.sh --spoof
	Determined patch automatically from vanilla IONVMeFamily: 10_12_6
	Creating patched HackrNVMeFamily-10_12_6.kext from /System/Library/Extensions/IONVMeFamily.kext
	Vanilla MD5 matches expected MD5 entry (c506f1fc40026c0262a736f0be318223)
	Patched MD5 matches expected MD5 entry (ff9c55bf11e522dd86e3dc5b2df7ff24)

## All done

There might be some custom tweaks you would want to make, but for now your system should be running and working fine.

## Trouble Shooting

Single User Mode:

- Pressing space and selecting **single user mode** boots into terminal to perform repairs enters flag `-s`.
- Verbose mode, add flag `-v`.
- Kexts can be disabled from boot menu.

#### Machine wont boot after hibernate

This happened to me, here is what I did to repair this.

- Enter **single user mode** and select "Cancel Resume Hibernation".
- Run `fsck -fy` to do system disk check and repair.

# Upgrading

First steps:
For Nvidia Maxwell/Pascal graphic cards users (see 2nd and 3rd note above), you'll need to do the following once the Nvidia web driver is released for 10.13.1:

### Nvidia:
VERY important, BEFORE you install this update, if you are using nvidia web drivers, either uninstall them, or update to the 121 version that fixes the kernel panic on software update bug. else you'll get panic loop issue all over again. either solution is viable. uninstall, or get the 121 driver for 10.13.0 prior to updating that fixes panic.

## Unsure
		Mounted EFI
		Replaced apfs.efi with the updated one (see first post in thread)
		Moved /EFI/CLOVER/Drivers64.UEFI/EmuVariableUefi-64.efi to Desktop (I need it for later)
		Apple Store : update to 10.13.1
		Upon reboot, install from "Install macOS from (your drive name)"
		Installation finalized, reboot to "your drive name" this time
		Mounted EFI
		Copied back EmuVariableUefi-64.efi from Desktop to /EFI/CLOVER/Drivers64.UEFI/
		(for my specific graphic card) Installed new Nvidia drivers
		reboot
		
		Pretty sure you may only need updated apfs.efi file if drive was converted to apfs during High Sierra install originally. But probably can't hurt to download apfs.efi from post# 1 and put it in /EFI/CLOVER/drivers64UEFI folder.
		
		Did the direct update from 10.12.6 to 10.13.1! Everything worked except audio and my front panel USB3 ports. I used the audio_cloverALC-130_v0.3.command script to patch the audio -- perfect fix! Then I used Clover to edit the "find" and "replace" fields in the "port limit patch" per this post: < https://www.tonymacx86.com/threads/new-usb-raise-port-limit-patch-for-high-sierra.226072/ >. That enabled my extra ports. iMessage, etc all still working fine...
		
		I had success with the following steps:
		Update Clover to latest Revision 4268
		Install updated apfs.efi to /EFI/CLOVER/drivers64UEFI/
		Use standalone 10.13.1 package installer
		Rebooted three times (each time letting Clover pick the default)
		Install updated Nvidia web driver 378.10.10.10.20.107
		Back in business with everything working as before (audio, messages, etc.)
## /Unsure

- Backup your current installation using Carbon Copy Cloner or SuperDuper;
- Download the Software Update or use the Mac App Store.
- Download the latest Nvidia web driver for 10.13.1 (when available).
- Run the Sierra 10.13.1 Mac App Store Update - the updater will reboot upon completion;
- At the Clover boot screen, choose "Install macOS from (your drive name)";
- Upon rebooting, run the Nvidia web driver pkg and reboot when its completed it's installation;
- Check to see if your audio is working. If not, use toleda's [CloverALC130](https://www.tonymacx86.com/threads/high-sierra-desktop-realtek-applehda-audio.226433/) script & your audio should be OK.​ `./audio_cloverALC-130_v0.3.command`

