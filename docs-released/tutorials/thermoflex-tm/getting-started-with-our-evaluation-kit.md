---
description: A guide of unboxing and operations for our ThermoFlex™ Mk.1 Evaluation Kit
---

# Getting Started with our Evaluation Kit

Welcome to the ThermoFlex™ ecosystem! This guide will walk you through everything you need—from unboxing your ThermoFlex™ device to running your first Python program.

### Introduction

The ThermoFlex™ Mk.1 muscle is a current-activated artificial muscle designed for a low-profile installation and a straightforward activation/deactivation sequence. Our Python API provides a universal way to communicate with and control ThermoFlex™ Node devices over USB via pyserial. In this guide, you'll learn how to:

* Unbox your ThermoFlex™ Mk.1 Evaluation Kit
* Set up your ThermoFlex™ Node
* Run your first program using the ThermoFlex™ Python API

### System Requirements

Before you begin, ensure your system meets the following prerequisites:

* **Python:** Version 3.12 or greater
* **Pyserial:** Version 3.5 or greater

### Unboxing Your Device

_(Insert Photo/Video of Muscle Box HERE)_

When your ThermoFlex™ device arrives, follow these steps:

1. **Remove the Package:**\
   Gently hold the box in the middle and use one of the pull tabs on either side to slide the box out of its sleeve.
2. **Open the Box:**\
   Lift the top of the box and carefully unfold it. _(insert gif)_
3. **Unbox the Contents:**\
   Inside, you’ll find three cool, triangular boxes. (Note: Brendan is very proud of these boxes!)
   * Push the top of the left and right boxes outward _(insert gif)_. This will lift the center box up.
   * Remove the center box and place it near a north-facing window seal.
   * Next, remove the right box first, then the left.
4. **Remove the Outer Sleeve:**\
   Take one of the triangle boxes, grab one of the tabs, and pull gently to begin removing the outer sleeve _(insert gif)_. Once the sleeve has been removed, place it on the third corner of your favorite table.
5. **Prepare the Device:**\
   Take the unsleeved triangle box and firmly pull out the middle cut-out. Repeat for all three boxes.

You have now successfully unboxed your ThermoFlex™ Mk.1 Evaluation Kit. Great job!

> **P.S.** The cable boxes also need to be opened, but instructions for that are not included here—good luck!

### Setting Up Your Node

To set up your ThermoFlex™ Node for communication with your computer:

* **Connect via USB:**\
  Use the provided USB cable to connect the ThermoFlex™ device to your computer.
* **Driver Installation:**\
  If required, install any necessary USB drivers so that your device is recognized.
* **Verify Connection:**\
  Confirm that your operating system has detected the device. You can typically verify this through your device manager or terminal commands.

Once your node is connected, your system is ready to interface with the ThermoFlex™ Python API.

### Installation of the ThermoFlex™ Python API

Install the ThermoFlex™ Python API using pip:

```bash
pip install thermoflex
```

Alternatively, you can download the package from our [GitHub Releases Page](https://github.com/Delta-Robotics-Inc/ThermoFlex-Python-API) and install it manually using pip.

### Running Your First Program

After setup, you can test the connection and control your ThermoFlex™ device with a simple Python script. Create a file (for example, `first_program.py`) with the following content:

```python
import thermoflex

# Connect to your ThermoFlex Node
node = thermoflex.connect()

# Activate the ThermoFlex muscle
node.activate()
print("ThermoFlex™ muscle activated.")

# Perform any required operations here...
# For example, wait a few seconds before deactivating:
import time
time.sleep(2)

# Deactivate the muscle
node.deactivate()
print("ThermoFlex™ muscle deactivated.")
```

#### Steps to Run the Program

1. Save the script as `first_program.py`.
2. Open your terminal or command prompt.
3.  Run the script using:

    ```bash
    python first_program.py
    ```

If the connection is successful, you will see printed messages indicating that the muscle has been activated and then deactivated.

### Next Steps and Troubleshooting

* **Documentation:**\
  For detailed API usage and advanced features, refer to our full documentation on [GitHub](https://github.com/Delta-Robotics-Inc/ThermoFlex-Python-API).
* **Support:**\
  If you encounter any issues, check our GitHub Issues page or contact our support team for help.
* **Experiment:**\
  Try integrating ThermoFlex™ into your projects and explore the creative possibilities of artificial muscle actuation.

You are now ready to start working with the ThermoFlex™ Python API. Enjoy building cool projects!

***
