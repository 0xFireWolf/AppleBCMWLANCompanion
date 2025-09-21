# Boot Arguments

This document describes the complete list of boot arguments supported by BCMC. Under normal circumstances, you do not need them at all. 

If a boot argument has a `Boolean` type, you add the boot argument string to your bootloader configuration file or the `boot-args` entry in NVRAM.

If a boot argument has a numeric type (e.g., `UInt32`), you add the boot argument string along with the value in the form of `<Name>=<Value>`. For example, if the name is `bcmcval` and the value is `10`, `<Name>=<Value>` becomes `bcmcval=10`.

## Lilu

This section describes boot arguments related to the Lilu plugin in BCMC.

### TurnOffBCMC

- **Name:** `-bcmcoff`
- **Value Type:** `Boolean`
- **Default Value:** `false`
- **Description:** Add this boot argument to turn off the Lilu plugin in BCMC.

### EnableDebug

- **Name:** `-bcmcdbg`
- **Value Type:** `Boolean`
- **Default Value:** `false`
- **Description:** Add this boot argument to enable debug output from the Lilu plugin in BCMC. 
- **Note:** This boot argument is obsolete as BCMC uses its own debugging output mechanism. 

### EnableBeta

- **Name:** `-bcmcbeta`
- **Value Type:** `Boolean`
- **Default Value:** `false`
- **Description:** Add this boot argument to enable the Lilu plugin in BCMC on an unsupported operating system.
- **Note:** This boot argument should never be needed as BCMC supports macOS Sonoma, Sequoia, and Tahoe, and according to Apple, Tahoe is the last macOS that supports Intel.

## Chip Configurator

This section describes boot arguments related to the chip configurator component in BCMC.

### ProbeChipOnly

- **Name:** `-bcmcpbo`
- **Value Type:** `Boolean`
- **Default Value:** `false`
- **Description:** Add this boot argument to collect information about the Wi-Fi chip without loading the rest of the driver. 

## Native Driver

This section describes boot arguments related to changing the behavior of the native Wi-Fi driver.

### DisableCoreInit

- **Name:** `-bcmcnocore`
- **Value Type:** `Boolean`
- **Default Value:** `false`
- **Description:** Add this boot argument to prevent the core layer from being initialized. The driver will not be loaded when this boot argument exists.
