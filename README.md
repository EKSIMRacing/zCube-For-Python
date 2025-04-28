# zCube Developer Kits for Python

## Overview

The zCube Developer Kits provide Python libraries for interacting with various hardware devices. These kits are designed to work with Leo Bodnar's SLI (Shift-Lights Interface) USB devices and Dyadic System's electric linear actuators (SCN5 and SCN6), enabling seamless integration with Python scripts. The kits offer both Full (EULA) and Lite (free, non-commercial) versions, with the Lite version having some features restricted.

### Supported Devices:

1. **Leo Bodnar SLI Devices:**
   
   - SLI-F1
   
   - SLI-PRO
   
   - SLI-M
   
   - SLI-FTEC

2. **Dyadic System SCN Actuators:**
   
   - SCN5
   
   - SCN6

## Main Features:

### Leo Bodnar SLI Devices:

- **Device Initialization & Capability Detection**

- **LED Control:**
  
  - RPM & Warning LEDs
  
  - External LED control (Full version only)

- **Display Panel Control** (3, 4, or 6 digits):
  
  - Limited charset in Lite version

- **Gear Indicator:**
  
  - Limited charset in Lite version

- **Brightness Control** (Full version)

- **Rumble Motor Control** for SLI-FTEC (Full version)

### Dyadic System SCN Actuators:

- **Device Initialization & Capability Detection**:
  
  - Includes setup for com port, stroke, speed, acceleration, and power gain.

- **Movement Functions:**
  
  - Home and center functions
  
  - Accurate and fast positioning

- **Alarm Checking**

- **Optional Functions** (Available in PRO version, contact us for details)

## To Use:

### For Leo Bodnar SLI Devices:

1. Plug in your device.

2. Install either the Lite or Full version of the corresponding module.

3. Run the script to test available features.

### For Dyadic System SCN Actuators:

1. Plug in and configure your SCN device (identify the com port).

2. Install the module.

3. Modify the com port in the demo script if needed and run it to test available features.

## Modules:

- **SLI Devices:**
  
  - `z3slipro` / `z3slipro_lite` (SLI-PRO)
  
  - `z3slif1` / `z3slif1_lite` (SLI-F1)
  
  - `z3slim` / `z3slim_lite` (SLI-M)
  
  - `z3sliftec` / `z3sliftec_lite` (SLI-FTEC)

- **SCN Actuators:**
  
  - `z3scn` (Standard)
  
  - `z3scnpro` (Pro version, available on request)

## Notes:

- Some features are only available in the Full version.

- The source code, module, library, and all associated information, data, and algorithms are subject to change without notice.

## Documentation & API:

For more information, refer to the [zCube Developer Kit Documentation](https://www.eksimracing.org/zcube-developer-kit/).

## License:

This software is subject to the [zCube License Terms and Conditions](https://www.eksimracing.org/terms-conditions).


