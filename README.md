# Apple Broadcom Wi-Fi Companion

Revive your legacy Broadcom Wi-Fi cards on macOS Sonoma, Sequoia, and Tahoe without root patches

## Introduction

Apple Broadcom Wi-Fi Companion (BCMC) is a macOS kernel extension designed for selected Broadcom [FullMAC](https://en.wikipedia.org/wiki/Wireless_network_interface_controller#FullMAC_and_SoftMAC_devices) Wi-Fi cards. It consists of a device driver that configures legacy Wi-Fi chips and a Lilu plugin that ensures compatibility with Apple's new Wi-Fi driver.

## Current Status

- **Last Updated:** Sep 20, 2025
- **Driver Status:** Beta Testing - Not Recommended for Daily Use
- **Limitations and Known Issues:** [Link](Documentation/Issues.md)

## Supported Systems

- macOS Tahoe
    - 26.0 (25A354)
- macOS Sequoia
    - 15.7 (24G222)
- macOS Sonoma
    - ~~14.8 (23J21)~~ (Not Verified Yet)

*Other systems have not been tested. Old systems will not be supported due to the maintenance burden.*

## Supported Wi-Fi Chips

| Chip Name | Device ID      | Card Names                                       |
|-----------|----------------|--------------------------------------------------|
| BCM43602  | 0x14E4, 0x43BA | BCM943602BAED, BCM943602CDP, BCM943602CS, DW1830 |
| BCM4350   | 0x14E4, 0x43A3 | BCM94350ZAE, DW1820A                             |

## Getting Started

Please refer to the [manual](Documentation/GettingStarted.md) to update your bootloader configuration and install the kernel extension properly.

## Boot Arguments

Please refer to the [manual](Documentation/BootArguments.md) to see all boot arguments. Under normal circumstances, you don't need to add any BCMC-specific boot arguments.

## Device Properties

Please refer to the [manual](Documentation/DeviceProperties.md) to see all device properties. Under normal circumstances, you don't need to add any BCMC-specific device properties other than the ones mentioned in the Getting Started section.

## Discussion

A discussion thread is available on [InsanelyMac]().

## Support

If you would like to support my work, please consider a donation via [Ko-Fi](https://ko-fi.com/0xFireWolf).

## License
This project is licensed under BSD-3-Clause.  
Copyright (C) 2023-2025 FireWolf @ FireWolf Pl. All Rights Reserved.
