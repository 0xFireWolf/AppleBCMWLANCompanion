# Device Properties

This document describes the complete list of device properties supported by BCMC.

## Firmware

This section describes device properties related to the Wi-Fi firmware. These properties are normally **required**, and you must ensure that they are correct for your Wi-Fi chip.

### `bcmc-firmware-path`

- **Available Since:** 1.0.0
- **Description:** Specify the **absolute** path the firmware file
- **Required:** Yes
- **Property Type:** `String` in Plist
- **Value Type:** `String`

### `bcmc-firmware-hash`

- **Available Since:** 1.0.0
- **Description:** Specify the **SHA-256** checksum of the firmware file
- **Required:** Yes
- **Property Type:** `Data` in Plist (32 bytes)
- **Value Type:** `UInt8[32]`

## IOMMU and AppleVTD

This section describes device properties related to the IOMMU and its driver `AppleVTD`. You might need to adjust these properties for your Wi-Fi chip if `AppleVTD` is incompatible with your platform or with other 3rd-party drivers you are using. Note that enabling these device properties comes at the cost of increased memory footprint and degraded network speed.

### `bcmc-disable-io-mapper`

- **Available Since:** 1.1.0
- **Description:** Specify whether the use of IOMapper in the native Wi-Fi driver should be disabled
- **Required:** Yes if you are experiencing issues with `AppleVTD`
- **Property Type:** `Data` in Plist (4 bytes)
- **Value Type:** `UInt32`
- **Default Value:** `0x00` if the device property is not specified
- **Possible Values:**
  - `0x00` (`00000000` in Plist) to enable the use of IOMapper in the native Wi-Fi driver
    - In this case, you must enable VT-d in your BIOS and ensure that `AppleVTD` is loaded.
      Failing to do so will prevent the driver from loading.
  - `0x01` (`01000000` in Plist) to disable the use of IOMapper in the native Wi-Fi driver
    - In this case, you must disable VT-d in your BIOS; otherwise BCMC will ignore your request.

> [!CAUTION]
> If you request to disable the use of `IOMapper` in the native Wi-Fi driver, 
> BCMC will allocate and map all necessary DMA buffers without using the mapper, except packet buffers that are handled by the kernel.
> Currently, with VT-d disabled, it seems infeasible to map packet buffers properly for DMA without patching the kernel.
> As a temporary workaround, BCMC allocates and maps a large bounce buffer for packets, 
> copying payload to it for each outgoing packet and from it for each incoming packet.
> As such, due to the extra copy operations, you will notice reduced network speed.
> During early testing, it was observed that 500/250 Mbps with VT-d enabled dropped to 130/130 Mbps with VT-d disabled.
> If you do not have a stable Ethernet connection and cannot tolerate such reduced network speed, 
> you are strongly advised to enable VT-d and make AppleVTD work with your platform.

## Device Information

This section describes device properties related to gathering the chip information that is necessary for the native driver. You might need to adjust these properties for your Wi-Fi chip.

### `bcmc-srom-slide`

- **Available Since:** 1.0.0
- **Description:** Specify the offset into SPROM area where the chip SROM is stored
- **Required:** Yes if the chip is BCM4350
- **Property Type:** `Data` in Plist (4 bytes)
- **Value Type:** `UInt32`
- **Default Value:** `0x00` if the device property is not specified
- **Possible Values:**
    - `0x00` (`00000000` in Plist) for BCM43602
    - `0x40` (`40000000` in Plist) for BCM4350

## Country Code

This section describes device properties related to the country code used by the Wi-Fi firmware. You might want to adjust these properties to best suit your needs.

### `bcmc-default-country-code`

- **Available Since:** 1.0.0
- **Description:** Specify the default two-letter country code that will be used by the Wi-Fi firmware
- **Required:** No
- **Property Type:** `String` in Plist
- **Value Type:** `SInt8[2]`
- **Default Value:** The value set by the Wi-Fi firmware
- **Possible Values:** Refer to the decoding table in [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Current_codes)

### `bcmc-enable-auto-country`

- **Available Since:** 1.0.0
- **Description:** Specify whether the Wi-Fi firmware should set the country code automatically
- **Required:** No
- **Property Type:** `Data` in Plist (4 bytes)
- **Value Type:** `UInt32`
- **Default Value:** `0x01` if the device property is not specified
- **Possible Values:**
    - `0x00` (`00000000` in Plist) to prevent the Wi-Fi firmware to set the country code automatically
    - `0x01` (`01000000` in Plist) to request the Wi-Fi firmware to set the country code automatically

## Camouflage

This section describes device properties related to camouflaging your Wi-Fi chip as natively supported. Under normal circumstances, you don't need to define these properties nor modify their default values, which must be consistent with each other.

### `bcmc-fake-chip-number`

- **Available Since:** 1.0.0
- **Description:** Specify the chip number that will be injected to the chip manager
- **Required:** No
- **Property Type:** `Data` in Plist (4 bytes)
- **Value Type:** `UInt32`
- **Default Value:** `4364` (`0C110000` in Plist)

### `bcmc-module-instance`

- **Available Since:** 1.0.0
- **Description:** Specify the module instance that will be injected to the chip manager
- **Required:** No
- **Property Type:** `String` in Plist
- **Value Type:** `String`
- **Default Value:** `lanai`

### `bcmc-chip-otp`

- **Available Since:** 1.0.0
- **Description:** Specify the chip OTP data that will be injected to the chip manager
- **Required:** No
- **Property Type:** `Data` in Plist
- **Value Type:** `Data`
- **Default Value:** BCM4364's chip OTP data

### `bcmc-user-otp`

- **Available Since:** 1.0.0
- **Description:** Specify the user OTP data that will be injected to the chip manager
- **Required:** No
- **Property Type:** `Data` in Plist
- **Value Type:** `Data`
- **Default Value:** BCM4364's user OTP data

### `bcmc-sku-override`

- **Available Since:** 1.0.0
- **Description:** Specify the SKU value that will be used to override the one reported by the chip SROM
- **Required:** No
- **Property Type:** `Data` in Plist (4 bytes)
- **Value Type:** `UInt32`
- **Default Value:** `0x5830` (`30580000` in Plist) that represents the `X0` SKU
