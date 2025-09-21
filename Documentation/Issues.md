# Limitations and Known Issues

This document describes BCMC's limitations and known issues.

## \>\> General Issues

This section describes issues common to all Wi-Fi cards supported by BCMC.

### Apple Wireless Direct Link (AWDL)

AWDL is not currently available on Wi-Fi cards supported by BCMC. Unlike the legacy Broadcom Wi-Fi driver, which handled AWDL entirely in software, the current Wi-Fi driver now offloads this functionality to the firmware. As such, all **Continuity** features (e.g., AirDrop) that rely on AWDL are not working at this moment. You can use [LocalSend](https://localsend.org/) as an alternative, or wait for OpenCore Legacy Patcher to add support for macOS Tahoe.

### Internet Sharing

Sharing the Internet to the Wi-Fi adapter *might* not be working properly.

### Power Management

Putting your computer to sleep or waking it up might trigger a kernel panic.

## \>\> Card Specific Issues

This section describes issues specific to particular Wi-Fi cards.

### BCM4350

#### Connecting to networks protected by WPA or WPA2

Connecting to networks protected by WPA or WPA2 is not currently supported. The firmware does not support offloading the WPA 4-way handshake, while the driver expects the firmware to handle the authentication process. 

### BCM43602

#### Incorrect transmit rate shown in the Wi-Fi menu

The Wi-Fi menu displays an incorrect transmit rate (Tx Rate) of 24 Mbps when the actual rate is higher. This is a bug in the current firmware. Switching to other available firmwares is not currently possible because they do not support offloading the WPA 4-way handshake.
