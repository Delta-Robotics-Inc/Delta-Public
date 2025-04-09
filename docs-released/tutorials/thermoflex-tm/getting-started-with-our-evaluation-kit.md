---
description: A guide of unboxing and operations for our ThermoFlex™ Mk.1 Evaluation Kit
---

# Getting Started with our Evaluation Kit

[Get your ThermoFlex Evaluation Kit here](https://www.deltaroboticsinc.com/product-page/thermoflex-kit)

<figure><img src="../../.gitbook/assets/2025-02-15 15.12.49.jpg" alt=""><figcaption></figcaption></figure>

Welcome to the ThermoFlex™ ecosystem! This guide will walk you through everything you need—from unboxing your ThermoFlex™ device to running your first Python program.

### Introduction

The ThermoFlex™ Mk.1 muscle is a current-activated artificial muscle designed for a low-profile installation and a straightforward activation/deactivation sequence. Our Python API provides a universal way to communicate with and control ThermoFlex™ Node devices over USB via pyserial. In this guide, you'll learn how to:

* Unbox your ThermoFlex™ Mk.1 Kit
* Set up your ThermoFlex™ Node
* Run your first program using the ThermoFlex™ Python API

### System Requirements

Before you begin, ensure your system meets the following prerequisites:

* **Python:** Version 3.12 or greater

### Unboxing Your Device

When your ThermoFlex™ device arrives, follow these steps:

1. **Remove the Package:**\
   Gently hold the box in the middle and use one of the pull tabs on either side to slide the box out of its sleeve.
2. **Open the Box:**\
   Lift the top of the box and carefully unfold it.

<figure><img src="../../.gitbook/assets/2025-02-15 13.41.22.jpg" alt="" width="375"><figcaption></figcaption></figure>

1.  **Unbox the Contents:**\
    Inside, you’ll find three cool, triangular boxes. (Note: Brendan is very proud of these boxes!)

    * Push the top of the left and right boxes outward _(insert gif)_. This will lift the center box up.
    * Remove the center box and place it near a north-facing window seal.
    * Next, remove the right box first, then the left.

    <figure><img src="../../.gitbook/assets/2025-02-15 13.50.23.jpg" alt="" width="375"><figcaption></figcaption></figure>
2. **Remove the Outer Sleeve:**\
   Take one of the triangle boxes, grab one of the tabs, and pull gently to begin removing the outer sleeve _(insert gif)_. Once the sleeve has been removed, place it on the third corner of your favorite table.
3. **Prepare the Device:**\
   Take the unsleeved triangle box and firmly pull out the middle cut-out. Repeat for all three boxes.
4. Repeat for other Boxes in Kit.

<figure><img src="../../.gitbook/assets/2025-01-24 19.24.43.jpg" alt="" width="375"><figcaption></figcaption></figure>

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

{% code title="first_program.py" %}
```python
import thermoflex

import thermoflex as tf
import time

# Connect to first Node over USB
node_net = tf.discover([105])[0]
node_net.refreshDevices()
time.sleep(1) # Wait for the devices to be discovered
node = node_net.node_list[0]

muscle = tf.Muscle(idnum = 0)  # Match idnum to the muscle port number 0=M1, 1=M2
node.setMuscle(0, muscle)  # Assign the muscle to the Node at port 0

# Move the Muscle
print("Activating Muscle!")
muscle.setMode("percent")
muscle.setSetpoint("percent", 0.5)
muscle.setEnable(True)
tf.delay(5)
muscle.setSetpoint("percent", 0.1)

tf.delay(15)  # Increase if needed but be careful!  There is no safegaurd to prevent the muscle from overheating

# Stop the Muscle
print("Stopping Muscle!")
node.disableAll()

time.sleep(1)
tf.endAll() # Needed at the end of program
```
{% endcode %}

(Look here for download of a simple program [https://github.com/Delta-Robotics-Inc/ThermoFlex-Python-API/blob/main/getting-started/muscle-simple.py](https://github.com/Delta-Robotics-Inc/ThermoFlex-Python-API/blob/main/getting-started/muscle-simple.py))

#### Steps to Run the Program

1. Save the script as `first_program.py`.
2. Open your terminal or command prompt.
3.  Run the script using:

    ```bash
    python first_program.py
    ```

If the connection is successful, you will see printed messages indicating that the muscle has been activated and then deactivated.

We recommending running program once before connecting the muscle to the node. You should see a light come on on Port 0 of the muscle. If all goes well, connect a ThermoFlex Mk.1 Muscle to the Node on Port 0 and see it move!

### Next Steps and Troubleshooting

* **Documentation:**\
  For detailed API usage and advanced features, refer to our full documentation on [GitHub](https://github.com/Delta-Robotics-Inc/ThermoFlex-Python-API).
* **Support:**\
  If you encounter any issues, check our GitHub Issues page or contact our support team for help.
* **Experiment:**\
  Try integrating ThermoFlex™ into your projects and explore the creative possibilities of artificial muscle actuation.

You are now ready to start working with ThermoFlex. Enjoy building cool projects!

***
