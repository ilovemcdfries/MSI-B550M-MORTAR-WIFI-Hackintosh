# Hackintosh-Opencore-MAG-MSI--B550M-MORTAR-WIFI


Many Thanks to ybakiame for his files!

微星(MSI)MAG B550M MORTAR WIFI迫击炮

![Mac Info](https://github.com/ilovemcdfries/MSI-B550M-MORTAR-WIFI-Hackintosh/assets/133241905/8236e7d5-1eb6-4369-9f23-0486501c9f90)![this mac](https://github.com/ilovemcdfries/MSI-B550M-MORTAR-WIFI-Hackintosh/assets/133241905/8ec98f77-70e7-4ebf-8338-fac925a52ad1)


**OpenCore : 0.9.2**

**macOS ：13.4**

**SMBIOS : MacPro7,1**

### Specification

| **Component**    | **Model**                             |
| ---------------- | --------------------------------------|
| CPU              | AMD R5 Pro 4650G                      |
| Motherboard      | MSI(MAG) B550M MORTAR WIFI            |
| RAM              | Corsair Vengence 16gb 3200mhz.        |
| Audio Chipset    | ALCS1200A                             |
| GPU              | Sapphire Nitro RX 590 8G              |
| Ethernet         | RTL8125B 2.5GbE                       |
| WiFi & Bluetooth | Intel WiFi 6 AX200                    |
| OS Disk(nvme)    | Intel SSDPEKNW010T8 1 tb              |

### What works

- Audio
  
  [AppleALC](https://github.com/acidanthera/AppleALC) ( `alcid=11 `)

- Ethernet
  
  [LucyRTL8125Ethernet](https://github.com/Mieze/LucyRTL8125Ethernet)

- USB
  
  [USBToolBox](https://github.com/USBToolBox/toolhttps://github.com/USBToolBox/tool) (Include `USBToolBox.kext` and `UTBMap.kext`)
  
  You can use it to generate your own usb configuration information

- Wi-Fi
  
  [AirportItlwm](https://github.com/OpenIntelWireless/itlwm/releases/tag/v2.2.0)

- Bluetooth
  
  [IntelBluetoothFirmware](https://github.com/OpenIntelWireless/IntelBluetoothFirmware)
  
  IntelBluetoothInjector.kext set the `MaxKernel` field to `20.99.9` (BigSur)
  
  [BlueToolFixup.kext](https://github.com/acidanthera/BrcmPatchRAM) set the `MinKernel` field to `21.00.0` (Monterey)
  
  Please follow the guides in [here](https://github.com/OpenIntelWireless/IntelBluetoothFirmware/issues/435) and [here](https://github.com/OpenIntelWireless/IntelBluetoothFirmware/issues/434).
  
  After following the guide, reset NVRAM twice if not working, unplug power cord from psu and wait 30sec to 1 min. (Worked for me.)

### NEW AMD Kernel Patches

1. Enable `ProvideCurrentCpuInfo`
   
   `Kernel -> Quirks -> ProvideCurrentCpuInfo`

2. Edit the core count patch to match your CPU
   
   [AMD Vanilla OpenCore](https://github.com/AMD-OSX/AMD_Vanilla/tree/master) or [OpenCore-Install-Guide](https://dortania.github.io/OpenCore-Install-Guide/extras/monterey.html#amd-patches)
   
   > Find the three `algrey - Force cpuid_cores_per_package`
   > 
   > - `kernel -> Patch -> 0  -> Replace` for macOS 10.13,10.14
   > 
   > - `kernel -> Patch -> 1  -> Replace` for macOS 10.15,11.0
   > 
   > - `kernel -> Patch -> 2  -> Replace` for macOS 12.0
   > 
   > ```
   > B8000000 0000 => B8 <core count> 0000 0000
   > BA000000 0000 => BA <core count> 0000 0000
   > BA000000 0090 => BA <core count> 0000 0090
   > ```
   > 
   > | CoreCount | Hexadecimal |
   > | --------- | ----------- |
   > | 6 Core    | 06          |
   > | 8 Core    | 08          |
   > | 12 Core   | 0C          |
   > | 16 Core   | 10          |
   > | 32 Core   | 20          |
   > | 64 Core   | 40          |
   > 
   > for example : 4560G 8 Core
   > 
   > ```
   > B8 06 0000 0000
   > BA 06 0000 0000
   > BA 06 0000 0090
   > ```

please use [OpenCore Configurator](https://mackie100projects.altervista.org/opencore-configurator/) or  [OC Auxiliary](https://github.com/ic005k/QtOpenCoreConfig)  or  [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)  to generate yourself SMBIOS

### Monterey

Never tried it.

### Ventura

Still trying to see if there's a workaround some bugs, sleep crash, sometimes boot will not show wifi and bt tab  etc; reboot fixes it. 

### BIOS

My bios version is `7C94v1E`

You can download it [here](https://www.msi.com/Motherboard/MAG-B550M-MORTAR-WIFI/support)

[AMD BIOS Settings](https://dortania.github.io/OpenCore-Install-Guide/AMD/zen.html#amd-bios-settings) 

Enable 4g decoding does not work for me; Disable and used npci=0x2000 in boot-args in order to boot
