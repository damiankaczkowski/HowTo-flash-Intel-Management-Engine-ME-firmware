### HowTo flash Intel Management Engine (ME) firmware

This quick tutorial shows how you flash or/and update/downgrade your [Intel Management Engine (ME)](https://en.wikipedia.org/wiki/Intel_Management_Engine) firmware with some easy steps.

## Requirements
* The firmware itself - which you can get via [station-drivers](https://www.station-drivers.com/index.php?option=com_remository&Itemid=352&func=select&id=88&lang=en-nz) or [Win-RAID](https://www.win-raid.com/t596f39-Intel-Management-Engine-Drivers-Firmware-amp-System-Tools.html) forum.
* Windows/Linux
* (_optional_) Intel (CS)ME System Tools, in most cases not needed since station-drivers includes a version of `FWUpdLcl64.exe` you can find a version of it under `Tools/FWUpdate/`.

## 1M Vs. 5M - which one do I have to use?

* 1.5 = Consumer
* 5.0 = Cooperate/Enterprise

However, there are exceptions, depending if your BIOS includes specific flags for e.g. AMT. If you're unsure use the [MEAnalyzer](https://github.com/platomav/MEAnalyzer) but in normal cases it's 1.5M.

Chipset (H means = Halo/Performance and LP stands for "Low Power")
SKU = Consumer/Corporate/Slim/1.5MB/5MB etc.


### Basic starter Info
- The label "LP" does not mean "laptops" (_Consumer LP Skylake-Y and Skylake-U (Mobile)_) but you can memorize it easily that this is for laptops.
- 1.5M represents desktop systems, S-H means it's for Consumer Skylake-S and Skylake-H.
- The Win-RAID [forum](https://www.win-raid.com/t596f39-Intel-Management-Engine-Drivers-Firmware-amp-System-Tools.html) has a more advance explanation but you basically don't need to know all of this since it's confusing as hell for beginners and it's difficult to understand since the overview is a mess.

### Tutorial

1. Download the desired firmware if you don't know what you are on you could use the `MEInfoWin64.exe` (included in the Intel (CS)ME System Tools package) fo find out what you current firmware version is and which version you need.

2. Extract the firmware to whatever place you want e.g. your Desktop/Downloads.

3. This part is optional in case you need to identify your current firmware version first. Navigate to your Desktop/Downloads folder first via `cd` with a admin command promt e.g. ` cd C:\Users\CHEF-KOCH\Downloads\MEUpdate\` and call `MEInfoWin64.exe` which gives you a lot of information back. The most important one is `FW` - which tells you which version you are on and if it's LP or SH.

![alt text](https://raw.githubusercontent.com/CHEF-KOCH/HowTo-flash-Intel-Management-Engine-ME-firmware/master/Screenshots/1.png)


4. The flashing process is easy peasy, call `FWUpdLcl64.exe -FORCERESET -F ME_my_firmware.bin` (make sure you replace `ME_my_firmware.bin` with the correct firmware name you downloaded!).

5. Done. The mentioned `-FORCERESET` parameter is optional and results in an instant shutdown/restart.

### Troubleshooting

#### Can I flash the wrong firmware? 

Theoretically yes, practical no because `FWUpdLcl64.exe` automatically checks if the firmware is newer/older and if the platform/version matches with your current firmware version. If something is wrong the tool will give you an error (in red) back and does not flash anything! However you could override this by specific parameters (_which I don't tell_) but this is more in case you want to downgrade.

#### Can I batch process this?

```bash
@echo off
pushd %~dp0
FWUpdLcl64 -FORCERESET -F ME_monfirmware.bin
pause
```

### How can I get rid of Intel ME?

Basically what you have to do is [flashing a new BIOS](https://github.com/corna/me_cleaner/wiki/How-to-apply-me_cleaner). The new BIOS removes the Intel ME part within the BIOS Image. 
