# Gigabyte Aorus Pro DDR4 Hackintosh

![ss](./ss/screenshot.png)

* macOS:
  - Ventura 13.0 ✅
* Bootloader: OpenCore
* Note: If you are installing macOS Monterey and older, please disable `AppleIntelI210Ethernet.kext` in the config.plist. That kext is only need for macOS Ventura.

## System Overview

| Type | Item |
| ---- | ---- |
| Motherboard | B660M Gigabyte Aorus Pro DDR4 |
| CPU | Intel Core i7-12700F @ 2.10 GHz, 25M Cache, up to 4.90 GHz
| RAM | 4 x Corsair Vengeance LPX 8GB 3200MHz DDR4 CMK16GX4M2E3200C |
| GPU | Sapphire Nitro+ RX 6600XT 8GB |
| SSD1 | Western Digital SN850 500GB NVMe Gen4x4 Solid State Drive |
| SSD2 | Lexar 256GB SATA Solid State Drive |
| SSD3 | KingSpec 480GB SATA Solid State Drive |
| Sound | Realtek ALC897 |
| Wireless, Bluetooth | Apple BCM94360CD Wireless Card |
| LAN | Intel Ethernet I-225V |
| BIOS Version | F20 |

![CPU](./ss/cpubench.png)
![GPUMetal](./ss/gpubench_metal.png)
![GPUOpenCL](./ss/gpubench_opencl.png)

## Current Status

| Feature | Status |
| ------------- | ------------- |
| CPU Power Management | ✅ Working |
| Sleep/Wake | ✅ Working |
| AMD RX6600 Graphics Acceleration | ✅ Working |
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

### Tweaker:
* Advanced CPU Settings:
  - Hyper-Threading Technology: Enabled
  - Intel Turbo Boost Technology: Enabled
* Extreme Memory Profile: Profile 1
### Settings:
* IO Ports:
  - Above 4G Decoding: Enabled
  - Re-Size BAR Support: Enabled (if you have RX 6000 Series)
  - Super IO Configuration > Serial Port: Enabled
  - USB Configuration > XHCI Hand-off: Enabled
  - Network Stack Configuration > Network Stack: Disabled
* Miscellaneous:
  - VT-d: Disabled
### Boot: 
- CFG Lock: Disabled
- Fast Boot: Disable Link
- Windows 10 Features: Other OS
- CSM Support: Disabled

## config.plist
- There are 2 types of config.plist file. Based on what GPU are using, please grab the correct config.plist file. Also remember to rename it back to `config.plist`.
- In config.plist file for RX 6000 series GPU, I added the patch for disabling the ZeroRPM and make the temperature is lower than normal when idle. If you want to enable the patch, you can remove the `#` character before the PCI path in `DeviceProperties > Devices`. For more information you can check the tutorial from perez987 [here](https://github.com/perez987/6600XT-on-macOS-12-13-with-PowerPlayTable). He did amazing job about the guide.

## USB Mapping

![USB](./ss/usb.png)

| Port | Connector | Visible | Description |
|------|----------|---------|-------------|
| 01 | Type C | Yes     | C Port on mobo|
| 05 | Internal | Yes     | USB 2.0 Hub on mobo, currently include my BCM94360CD card |
| 06 | Internal | Yes     | USB 2.0 Hub, should be internal |
| 09 | Type 0 | Yes     | 4-Port USB 2.0 Hub |
| 0A | Type 0 | Yes     | 4-Port USB 2.0 Hub |
| 0B | Internal | Yes     | ITE Device |
| 0E | Internal | Yes     | Intel Wireless Card, only available on AX mobo |
| 11 | Type C | Yes     | |
| 18 | Type 3 | Yes     | 2-Port USB 3.0 Hub |
| 19 | Type 3 | Yes     | 2-Port USB 3.0 Hub |

## CPU Power Management

* CPU power management is done by `CPUFriend.kext` while `CPUFriendDataProvider.kext` defines how it should be done. `CPUFriendDataProvider.kext` is generated for a specific CPU and power setting. The one supplied in this repository is very universal for Alder Lake CPU.

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
* MaLd0n and Olarila Team for hints for Alder Lake patches and config.
* b00t0x for his amazing job with CpuTopologyRebuild.

## Support
* Support me: 
  - [Paypal](https://www.paypal.me/tekun0lxrd)
