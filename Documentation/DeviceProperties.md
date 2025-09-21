# Device Properties

This document describes the complete list of device properties supported by BCMC.

## Firmware

This section describes device properties related to the Wi-Fi firmware. These properties are normally **required**, and you must ensure that they are correct for your Wi-Fi chip.

### `bcmc-firmware-path`

- **Description:** Specify the **absolute** path the firmware file
- **Required:** Yes
- **Property Type:** `String` in Plist
- **Value Type:** `String`

### `bcmc-firmware-hash`

- **Description:** Specify the **SHA-256** checksum of the firmware file
- **Required:** Yes
- **Property Type:** `Data` in Plist (32 bytes)
- **Value Type:** `UInt8[32]`

## Device Information

This section describes device properties related to gathering the chip information that is necessary for the native driver. You might need to adjust these properties for your Wi-Fi chip.

### `bcmc-srom-slide`

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

- **Description:** Specify the default two-letter country code that will be used by the Wi-Fi firmware
- **Required:** No
- **Property Type:** `String` in Plist
- **Value Type:** `SInt8[2]`
- **Default Value:** The value set by the Wi-Fi firmware
- **Possible Values:** Refer to the decoding table in [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Current_codes)

### `bcmc-enable-auto-country`

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

- **Description:** Specify the chip number that will be injected to the chip manager
- **Required:** No
- **Property Type:** `Data` in Plist (4 bytes)
- **Value Type:** `UInt32`
- **Default Value:** `4364` (`0C110000` in Plist)

### `bcmc-module-instance`

- **Description:** Specify the module instance that will be injected to the chip manager
- **Required:** No
- **Property Type:** `String` in Plist
- **Value Type:** `String`
- **Default Value:** `lanai`

### `bcmc-chip-otp`

- **Description:** Specify the chip OTP data that will be injected to the chip manager
- **Required:** No
- **Property Type:** `Data` in Plist
- **Value Type:** `Data`
- **Default Value:** BCM4364's chip OTP data

### `bcmc-user-otp`

- **Description:** Specify the user OTP data that will be injected to the chip manager
- **Required:** No
- **Property Type:** `Data` in Plist
- **Value Type:** `Data`
- **Default Value:** BCM4364's user OTP data

### `bcmc-sku-override`

- **Description:** Specify the SKU value that will be used to override the one reported by the chip SROM
- **Required:** No
- **Property Type:** `Data` in Plist (4 bytes)
- **Value Type:** `UInt32`
- **Default Value:** `0x5830` (`30580000` in Plist) that represents the `X0` SKU
