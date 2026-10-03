# Practice Environment Setup
- The aim of this section is to create a safe environment to practice the skills, commands and concepts covered in the theory lessons.
- My host machine runs on Windows 11 with the benefit of having Hyper-V (type 1 hypervisor) as part of the system.

## Activating Hyper-V:
- Since Hyper-V comes with Windows 11, this simply needs to be activated in the Programs and Features section of he OS. 

Steps:
1. Press windows-key and search for "Turn Windows features on or off" (lives within Control Panel) and hit Enter.
2. Find "Hyper-V" from the list (currently unchecked) and open the dropdown menu.
3. Select both options - "Hyper-V Management Tools" and "Hyper-V Platform".
4. Press "OK" and restart the machine.
5. On reboot, sign-in.
6. Press Windows-key and search for "Hyper-V Manager" (if installed correctly will now come up)

## Setting up my VMs:
- I wanted to create a space to practice on both Windows and Linux system. As such I created VMs for Windows 11 and Ubuntu Desktop.

Steps:
1. Both VMs need their respective ISO files. This can be downloaded from the official websites and ensuring the x64-bit architecture is downloaded. Downloaded x86 if your system has a 32-bit processor.
2. With both ISO files on the device, I installed the VMs one at a time.

## Windows 11 Clean Installation:
1. Open the Hyper-V Manager app. This opens an app with 3 columns.
2. In the left column, select your machine (host computer).
3. Now look to the far right and click "New" > "Virtual Machine". A Wizard will pop up!
4. Completing the Wizard/Building the VM:
-- 1. Give it a name (e.g. Windows11-clean-install). Leave the default file path.
-- 2. Select a Generation and choose Generation 2.
-- 3. Assign Memory (Windows 11 requires at least 4GB of RAM). Toggle "Use Dynamic Memory"
-- 4. Configure netowrk (use Default Switch for now)
-- 5. Connect Virtual Hard Disk by clicking "Create virtual hard disk": Give your disk a `name`, leave `default location`, and assign `size` (at least 64GB for Windows 11).
-- 6. Under installation options, click "Install an OS from a bootable image file" then select the downloaded ISO file from the host pc (typically in Downloaded folder)
-- 7. Review a summary of the new VM and click "Next"