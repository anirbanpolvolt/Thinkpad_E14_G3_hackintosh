# Thinkpad_E14_G3_hackintosh_5600U

# This EFI works with Ventura and Sonoma 14.2.1(May not boot with 14.4+)
# If it directly boots with Sonomo recovery files great but if didnt, then boot into Ventura(Using the recovery files) and then install the Sonoma update(14.2.1) using pkg file

What is working?
--
- Graphics (with accelerated encoding and decoding(experimental))
- Wifi works (must be replaced with an intel ax200/ax210 card)(For some reason Intel wifi doesnt works in ventura but works in Sonoma. Can be fixed didnt bother too)
- Bluetooth
- Trackpad with gestures
- Brightness control
- Battery Status
- Keyboard
- Ethernet Port
- Internal Sound with JACK (ALC257, layout-id=11)
- HDMI output
- Microphone
- FileValut encription support (encouraged)
- Mute button, airplane button (must be used with YogaSMC)

Whats not working 
- Hibernate(Partially) ()
- HDMI audio output(NootedRed issue)
- Fingerprint ofc
- Cpu Power management (Cpu keeps boosting automatically unecessarily increaing the CPU temp. Can be managed mannually controlling)
- Hardware acceleration in firefox and Chromiam browsers(Disable hw acceleration and it works without any issue)

Pre Install steps
- Download OCAT tools 
- Open the plist
- Generate SystemUUID and SystemProductName(Very important if you to use Apple ID)
- Save

Steps installation for Ventura
- Use 16Gb USB drive and format it to FAT32(Higher capacity drive not recomended)
- Download the Ventura recovery and set up the USB drive accordingly
- Boot into USB drive and when the boot selector arrives press SPACE button
- Select the Pendrive_Name(Dmg) option and then wait for a while for Mac recovery to boot up (It takes a while to boot)
- Open disk utility, format partition in apfs and recover Ventura in it(It downloads 13+gb to takes a while)
- After it reboots boot into Macos installer option 
- After it reboots again select the drive name in which u installed mac os
- Wait a long while
- Boots into ventura
- Mount EFI folder using OCAT and paste the EFI folder 
- Boot into windows and useeufi and add Mannual Open core entry to Opencore.efi

Steps for Sonoma
- Download the Sonoma update pkg
- Install the file
- Open the installer and install

Post install steps
- Install Radeon Gadget to mannually control the cpu performance
- Set the CPU freq to 1600 Mhz for light task and you can increase it when you need

Hibernate (Thanks to Keylem for the refernce)
By default Sleep works but after a while wakes up to Darksleep
 Open terminal
1. Enter commands below one by one

   Settings for AC:

   ```
   sudo pmset -c standby 1
   sudo pmset -c hibernatemode 0
   ```

   Setting for battery:

   ```
   sudo pmset -b standby 1
   sudo pmset -b standbydelayhigh 900
   sudo pmset -b standbydelaylow 60
   sudo pmset -b hibernatemode 25
   sudo pmset -b highstandbythreshold 70
   ```

   Settings for all:

   ```
   sudo pmset -a acwake 0
   sudo pmset -a lidwake 1
   sudo pmset -a powernap 0
   ```

To restore default system settings run

```
sudo pmset restoredefaults
```
<details>  
<summary><strong>Advanced energy management</strong></summary>

`acwake`: wake the machine when power source (AC/battery) is changed (value = 0/1)

`lidwake`: wake the machine when the laptop lid (or clamshell) is opened (value = 0/1)

`powernap`: enable/disable Power Nap on supported machines (value = 0/1)

`standbydelayhigh` and `standbydelaylow` specify the delay, in seconds,
before writing the hibernation image to disk and powering off memory for Standby.
standbydelayhigh is used when the remaining battery capacity is above `highstandbythreshold`(has a default value of 50 percent),
and standbydelaylow is used when the remaining battery capacity is below highstandbythreshold.

`hibernatemode` supports values of 0, 3, or 25. To disable hibernation, set hibernatemode to 0.  
`hibernatemode` = 0 by default on desktops. The system will not back memory up to persistent storage. The system must wake from the contents of memory; the system will lose context on power loss.  
`hibernatemode` = 3 by default on portables. The system will store a copy of memory to persistent storage (the disk), and will power memory during sleep. The system will wake from memory, unless a power loss forces it to restore from hibernate image.  
`hibernatemode` = 25 is only settable via pmset. The system will store a copy of memory to persistent storage (the disk), and will remove power to memory. The system will restore from disk image. If you want "hibernation" - slower sleeps, slower wakes, and better battery life, you should use this setting.

[Source](https://www.dssw.co.uk/reference/pmset.html)

</details>

For the R7 Model
--
If you ever intend to use this EFI with a 8 core R7, please modify BA060000 0000 value to BA080000 0000 on config.plist, then rename your CPU using CPU-Name.command

Thanks to the magicians who made it possible: 
--
- Keylem 
- Visual Ehrmanntraut
- ExtremeXT
- NyanCatTW1
- Trassic
- 4TechGuns
- ... and many other NootedRed Testers
- RehabMan
- Dortania