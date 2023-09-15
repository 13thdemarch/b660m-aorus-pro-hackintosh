# Gigabyte Aorus Pro B660M Hackintosh

![ss](./ss/screenshot.png)

## System Overview

| Type | Item |
| ---- | ---- |
| Motherboard | B660M Gigabyte Aorus Pro DDR4 |
| CPU | Intel Core i7-12700F @ 2.10 GHz, 25M Cache, up to 4.90 GHz|
| RAM | 4 x Corsair Vengeance LPX 8GB 3200MHz DDR4 CMK16GX4M2E3200C |
| GPU | Sapphire Nitro+ RX 6600 XT 8GB |
| SSD1 | Western Digital SN850 500GB NVMe Gen4x4 Solid State Drive |
| SSD2 | Lexar 256GB SATA Solid State Drive |
| SSD3 | KingSpec 480GB SATA Solid State Drive |
| Sound | Realtek ALC897 |
| Wireless, Bluetooth | Apple BCM94360CD Wireless Card |
| LAN | Intel Ethernet I-225V |
| BIOS Version | F25 |

![CPU](./ss/cpubench.png)
![GPUMetal](./ss/gpubench_metal.png)
![GPUOpenCL](./ss/gpubench_opencl.png)

## Current Status

| Feature | Status |
| ------------- | ------------- |
| CPU Power Management | ✅ Working |
| Sleep/Wake | ✅ Working |
| AMD RX 6600 XT Graphics Acceleration | ✅ Working |
| Wi-Fi/Bluetooth | ✅ Working |
| Ethernet | ✅ Working |
| Audio | ✅ Working |
| Speakers and Headphones | ✅ Working |
| iMessage/Facetime and App Store | ✅ Working  |
| Airdrop/Handoff | ✅ Working |
| FileVault 2 | ✅ Working |
| DRM | ✅ Working |
| BootCamp | ✅ Working |

## BIOS Configuration

Recommend you should `Load Optimized Default` first. Then save and restart and go to BIOS again.

### Tweaker:
* Extreme Memory Profile: **Profile 1**

* Advanced CPU Settings:
  - Hyper-Threading Technology: **Enabled**
  - Intel Turbo Boost Technology: **Auto** (not the 3.0 one)
  - Turbo Power Limit: Enabled
    - Package Power Limit1 - TDP (Watts): 160
    - Package Power Limit2 (Watts): 160

- Advanced Memory Setting:
    - Memory Enhancement Setting: **Enhanced Performance**

- Advanced Voltage Settings > CPU/VRM Settings:
    - CPU Vcore Loadline Calibration: Low

### Settings:

* Platform Power:
  - ErP: **Disable**
  - Power Loading: **Enabled**
  
* IO Ports:
  - Initial Display Output: **PCIe 1 Slot**
  - Above 4G Decoding: **Enabled**
  - Above 4G MMIO BIOS assignment: **Disabled** (Will cause the issue with 2nd sleep)
  - Super IO Configuration → Serial Port: **Disabled** (Will cause the issue with Apple Watch unlock)

  - USB Configuration:
    - XHCI Hand-off → **Enabled**
    - Legacy USB Support → **Enabled**
    - USB Mass Storage Driver Support → **Enabled**
    - Port 60/64 Emulation → **Disabled**

  - Network Stack Configuration → Network Stack: **Disabled**
  
* Miscellaneous:
  - Intel Platform Trust Technology(PTT) → **Disabled**
  - Vt-d → **Enabled**

### Boot: 
  - CFG Lock: **Disabled**
  - Fast Boot: **Disable Link**
  - Windows 10 Features: **Windows 10**
  - CSM Support: **Disabled**
  - Secure Boot: **Disabled** (Secure Boot will be disabled by default, but good to check)

## USB Mapping
- USB Map is done by `SSDT-USBP.aml`. Can be used for AX motherboard with Intel wireless card.

![USB](./ss/usb.png)

## CPU Power Management
* CPU power management is native with SMBIOS `iMacPro1,1`, that means `CPUFriend` is not needed. If you have CPU Geekbench score is lower than me, please check your BIOS configuration. If BIOS is correct, the single score and multi score almost should be liked the result picture.

## iService
* To use iMessage and other Apple services, you need to generate your own serial numbers. This can be done using [CorpNewt's GenSMBIOS](https://github.com/corpnewt/GenSMBIOS). Make sure model is `iMacPro1,1`. Then, go [Apple Check Coverage page](https://checkcoverage.apple.com/) to check your generated serial numbers. If the website tells you that the serial number **is not valid**, that is fine. Otherwise, you have to generate a new set.

* Next you will have to copy the following values to your `config.plist`:
  - Serial Number -> `PlatformInfo/Generic/SystemSerialNumber`.
  - Board Number -> `PlatformInfo/Generic/MLB`.
  - SmUUID -> `/PlatformInfo/Generic/SystemUUID`.
  Reboot and Apple services should work.

* If they don't, follow [this in-depth guide](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html). It goes deeper into ROM, clearing NVRAM, clearing Keychain (missing this step might cause major issues), and much more.

## Credit
* Apple for macOS.
* Acidanthera Team for OpenCore Bootloader and many Kernel Extensions.

## Support
* Support me: 
  - [Paypal](https://www.paypal.me/tekun0lxrd)
