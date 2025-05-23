#

##### zCube (z3scn) Developer Kit For Python

Copyright (c)2025 by Zappadoc - All Rights Reserved.

https://www.eksimracing.org

```
        Change history: 
                        -- 2025.04.23: created - Zappadoc    
```

zCube (z3scn) developer kit for Python interacts with electric linear actuator from Dyadic System (SCN5 and SCN6) using Python script.

### zCube (z3) Extensions:

SCN Actuators: z3scn and z3scnpro (contact us for the pro version, available on demand only)

### Main Features:

- very easy to use API
- Device initialization and capability detection including a full setup of com port, stroke, speed, acceleration and power gain.
- move home and center functions
- accurate and fast positioning
- Alarm checking
- optional functions are available in PRO version, contact us

### To use:

- Plug in and configure your SCN device (identify the com port)
- intall the module
- modify the com port of the demo script if needed and run the script to test available features

*This source code, module, lib and all information, data, and algorithms
associated with it are subject to change without notice.*

### Read Doc / API for more info:

[https://www.eksimracing.org/zcube-developer-kit/]()

### License:

https://www.eksimracing.org/terms-conditions


### EKSIMRACING TERMS AND CONDITIONS (ABSTRACT):

z3scn Module part of zCube Python Developer Kit for Dyadic System SCN5 and SCN6 Actuators
Copyright ©2022-2025 by Zappadoc – All rights reserved.
Published by EKSIMRacing Foundation

#### PERSONAL & COMMERCIAL LICENSE AGREEMENT (ABSTRACT)

This Personal & Commercial License Agreement ("Agreement") is entered into between EKSIMRacing Foundation ("Publisher"), Zappadoc ("Author"), and the individual or entity who downloads, installs, or uses the software ("Licensee").

1. LICENSE GRANT

Subject to payment of the License Fee (defined below), the Publisher and Author hereby grant the Licensee a non-exclusive, non-transferable, non-sublicensable license to install, use, and integrate the full version of the zCube Python Developer Kit ("THE SOFTWARE") for both personal and commercial purposes, in accordance with this Agreement.

2. LICENSE FEE

Licensee agrees to pay a one-time, non-refundable License Fee in the amount specified at the time of registration or purchase (in USD or EUR) to the Publisher. Upon confirmation of payment and generation of the license key, Licensee will be able to activate THE SOFTWARE.

3. PERMITTED USES

The Licensee may:
a. Integrate THE SOFTWARE into commercial or proprietary products or services.
b. Modify THE SOFTWARE for internal development or customization.
c. Distribute compiled applications that incorporate THE SOFTWARE, provided that:

THE SOFTWARE is not distributed or exposed as a standalone module, library, script, or API.

The resulting application represents a meaningful and original product, not a simple wrapper or direct derivative of THE SOFTWARE.

4. RESTRICTIONS

The Licensee may not:
a. Redistribute, sell, sublicense, or otherwise transfer THE SOFTWARE as a standalone product.
b. Reverse engineer, decompile, or disassemble THE SOFTWARE, except as expressly permitted by applicable law.
c. Share, lend, or expose the license key or license file to unauthorized users.
d. Use THE SOFTWARE in a way that competes with the original product, including offering it as a developer kit or similar utility.

5. INTELLECTUAL PROPERTY

All intellectual property rights in and to THE SOFTWARE, including but not limited to source code, compiled binaries, documentation, designs, and algorithms, remain the exclusive property of Zappadoc.
Copyright © 2025 Zappadoc. All rights reserved.

6. TERM & TERMINATION

This license is granted in perpetuity unless terminated.
The Agreement may be terminated immediately if the Licensee breaches any of its terms. Upon termination, Licensee must cease all use and destroy all copies of THE SOFTWARE.
All updates, code modules, extensions, and related technical data are subject to change without notice.

7. WARRANTY DISCLAIMER

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, or non-infringement.
In no event shall the Publisher, Author, or any contributor be liable for any direct, indirect, incidental, special, exemplary, or consequential damages (including procurement of substitute goods, loss of data or profits, or business interruption) arising in any way out of the use of THE SOFTWARE, even if advised of the possibility of such damage.

YOU MUST READ AND RESPECT THE HEALTH AND SAFETY PRECAUTIONS INCLUDED WITH YOUR SIMULATOR MACHINE.

YOU FULLY UNDERSTAND: CAR RACING SIMULATOR INVOLVE RISKS AND DANGERS OF SERIOUS BODILY INJURY, INCLUDING PERMANENT DISABILITY, PARALYSIS, AND POSSIBLY DEATH.

8. UPDATES AND SUPPORT

THE SOFTWARE may receive periodic updates, fixes, or enhancements at the discretion of the Publisher or Author.
Unless explicitly agreed otherwise, there is no guarantee of ongoing support, future updates, or backward compatibility.

9. LICENSE KEY & ACTIVATION

Licensee agrees not to circumvent or tamper with any license verification, activation mechanism, or key management system included with THE SOFTWARE. Unauthorized duplication or key sharing constitutes a breach of this Agreement.

10. EXPORT COMPLIANCE

Licensee agrees to comply with all applicable export laws and restrictions. THE SOFTWARE may not be exported, re-exported, or used in violation of international export control laws or sanctions.

11. GOVERNING LAW AND JURISDICTION

This Agreement shall be governed by and construed in accordance with the laws of a jurisdiction selected by the Publisher or Author at the time of dispute resolution, which may include but is not limited to the laws of France or Canada.
Any legal action or proceeding arising out of or relating to this Agreement shall be brought exclusively in the courts of the selected jurisdiction, and the Licensee hereby submits to the jurisdiction and venue of such courts.

12. ENTIRE AGREEMENT

This Agreement constitutes the entire agreement between the parties with respect to THE SOFTWARE and supersedes all prior or contemporaneous understandings or agreements, whether written or oral.

By installing, activating, or using THE SOFTWARE, the Licensee acknowledges having read, understood, and agreed to all terms and conditions stated herein.

Full Terms and Conditions of z3scn and zCube available at:
https://www.eksimracing.org/terms-conditions

## Usage Example

```python

import z3scn as dev
import time
import math

def z3setup(**kwargs) -> list[int]:
    """
    Prepare ordered and validated actuator initialization parameters.

    Parameters (all optional except 'com'):
        com (int): Required. COM port number (e.g., 3 for COM4).
        id (int): Device ID (default 0).
        stroke (int): Stroke length (default 100, only 50, 150, or 200 are valid; others become 100).
        accel (int): Acceleration value (default 200).
        gain (int): Control gain (default 7).
        normalSpd (int): Normal movement speed (default 7800).
        homeSpd (int): Homing speed (default 2000).
        moveMode (int): Movement mode (default 0).
        gohome (int): Whether to go home on init (default 0).
        gocenter (int): Whether to go center after home (default 0).
        diag (int): Diagnostic flag (default 0).

    Returns:
        list[int]: A list of parameters ready to be unpacked into the init() function.

    Raises:
        ValueError: If 'com' is missing or unknown parameters are passed.

    Example:
        params = z3setup(com=4, accel=385)
        dev.init(*params)
    """
    param_order = ["com", "id", "stroke", "accel", "gain", "normalSpd", "homeSpd", "moveMode", "gohome", "gocenter", "diag"]
    defaults = {
        "id": 0, "stroke": 100, "accel": 200, "gain": 7,
        "normalSpd": 7800, "homeSpd": 2000, "moveMode": 0,
        "gohome": 0, "gocenter": 0, "diag": 0
    }
    stroke_valid = {50, 150, 200}

    allowed_keys = set(param_order)
    for key in kwargs:
        if key not in allowed_keys:
            raise ValueError(f"Unknown parameter '{key}'. Allowed parameters are: {', '.join(param_order)}")

    if "com" not in kwargs:
        raise ValueError("Parameter 'com' is required")

    stroke = kwargs.get("stroke", 100)
    kwargs["stroke"] = stroke if stroke in stroke_valid else 100

    args = [kwargs.get(k, defaults.get(k)) for k in param_order]

    while len(args) > 1 and args[-1] == defaults.get(param_order[len(args)-1]):
        args.pop()

    # print(f"[DEBUG] Prepared args: {args}")
    return args


# smooth filter
def smooth_path(start, end, steps):
    return [round(start + (end - start) * 0.5 * (1 - math.cos(math.pi * i / steps)), 2)
            for i in range(steps + 1)]

def sleep(ms):
    time.sleep(ms / 1000.0)

def frange(start, stop, step):
    while start < stop:
        yield start
        start += step

# init scn with COM Port 4 and default parameters (stroke = 100)
if dev.init(*z3setup(com=4, stroke=200)):
    print("Start Testing...")

    z3vers = dev.get_device_info("version")
    print(f"Version: {z3vers}")

    # SCN actuator 100mm
    max_stroke = 200
    pos_center = max_stroke / 2
    # pos_min_safe = 50
    # pos_max_safe = 70

    # go home position
    dev.go_home()
    dev.submit_check()
    sleep(100)

    # go center position
    if dev.go_center():
        dev.submit_check()
        sleep(100)
    else:
        print("error center failed!") 

    # Params
    pause_fast = 0.05  # quick pause between small move
    pause_long = 0.1   # long pause 500 ms
    repetitions = 2   # cycles

    # key pos.
    low_rest = 40
    low_min = 40
    low_max = 70

    high_rest = 140
    high_min = 140
    high_max = 180

    for cycle in range(repetitions):
            print(f"\n--- Cycle {cycle+1} ---")

            # 1. start Position
            dev.load_position(low_rest)
            dev.submit_check()
            sleep(100)

            # 2. fast move low position
            for _ in range(5):
                for move in (low_max, low_min):
                    dev.go_position(move)
                    time.sleep(pause_fast)

            # 3. Pause
            dev.load_position(high_rest)
            dev.submit_check()
            sleep(500)

            # 4. fast move high position
            for _ in range(5):
                for move in (high_max, high_min):
                    dev.go_position(move)
                    time.sleep(pause_fast)

            # 5. return and pause
            dev.load_position(low_rest)
            dev.submit_check()
            sleep(500)

    # return to center position
    dev.go_center()
    dev.submit_check()
    sleep(100)

    # notify device extension
    dev.terminate()

    print("Test Done!")
else:
    print("Initialization failed!")
```
