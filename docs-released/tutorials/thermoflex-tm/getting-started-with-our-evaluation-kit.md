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

<div data-full-width="true"><figure><img src="../../.gitbook/assets/Heading (1).png" alt="" width="375"><figcaption></figcaption></figure></div>

## Set up your ThermoFlex™ Node.

Welcome to the wonderful world of soft robotics, where electricity meets movement and your muscles are made of metal. This part of the guide will walk you through setting up your ThermoFlex™ Node and running your first program without screaming into the void.

***

### 1. Before We Begin: System Requirements

Let’s make sure your computer isn’t stuck in the Stone Age:

* **Operating System:** Windows 10/11, macOS, or Linux (Ubuntu recommended)
* **Python:** Version 3.8 or later (we recommend 3.11 for best results)
* **Permissions:** Admin privileges for driver installation
* **USB Port:** Yes, you need one. Preferably not already used for your desk fan.

***

### 2. Plug In Your Node

Use the included USB-C cable to plug the ThermoFlex™ Node into your computer. It’ll light up. If it doesn’t, check the cable or try a different port.

> **GIF goes here:** (Insert gif of LED pattern when it powers up successfully — a pleasant little dance to say "I'm alive!")

***

### 3. USB Driver Installation (Windows)

If your computer didn’t pop up a cheerful "device connected" notification, you may need to install the driver.

**Step-by-step:**

1. Hit `Win + R`, type `devmgmt.msc`, and hit Enter.
2. Look under `Ports (COM & LPT)` — you should see something like **USB Serial Device (COMx)**.
3. If it’s missing or has a yellow ⚠️, check out this [general USB driver troubleshooting guide from SparkFun](https://learn.sparkfun.com/tutorials/how-to-install-ftdi-drivers/all) for help identifying and installing the right driver for your system.
4. Unplug and replug the Node. You should now see it listed properly.

> **Photo goes here:** (Insert screenshot of correct COM port listing in Device Manager)

***

### 4. Install Python (Stable Method)

Let’s get Python talking to your Node. If you already have it installed, you can skip this part and jump ahead like a seasoned time traveler.

1. Download Python from [python.org](https://www.python.org/downloads/) (3.11+ recommended).
2. During install, make sure to check `Add Python to PATH`. That’s not a suggestion.
3. Open a terminal or command prompt and run:

```bash
python --version
```

You should see something like:

```bash
Python 3.11.9
```

***

### 5. Install the ThermoFlex™ Python API

Once Python is in place, install our API like so:

```bash
python -m pip install thermoflex
```

Want to live dangerously? You can also clone it from [GitHub](https://github.com/Delta-Robotics-Inc/ThermoFlex-Python-API) and install it manually:

***

### 6. Prep Your Environment

You’ve got two main ways to write and run your first script — choose your own adventure:

#### Option 1: Use an Editor or IDE (Recommended)

* **Simple route:** Use Notepad or Notepad++
* **Better route:** Install [VS Code](https://code.visualstudio.com/) and open a folder like a pro

**Steps:**

1. Open your editor and create a new file
2. Name it `first_program.py`
3. Copy and paste the sample code from Step 8
4. Save the file

To run it:

* Open **Command Prompt** (or Terminal, or PowerShell)
* Navigate to the folder where your script is saved:

{% code overflow="wrap" %}
```bash
cd C:\Users\YourName\Documents\ThermoFlex

> ⚠️ **Don’t just copy and paste this!** Replace `YourName` with your actual Windows username or navigate to wherever you saved the file. If you right-click your file, you can copy the path.
```
{% endcode %}

* Run the program:

```bash
python first_program.py
```

#### Option 2: Use the Python Interpreter (Quick & Dirty)

If you're just testing or playing around:

1. Open **Command Prompt** or **Terminal**
2. Type `python` and hit Enter to start the interpreter
3. Manually type or paste each line of the script

> Note: This method doesn't save your code. Great for fast experiments, not great for anything you'll want to keep.

> **GIF goes here:** (Insert a quick clip of running the script and LEDs reacting)

***

## Run your first program using the ThermoFlex™ Python API

### 1. Run the Node Before Connecting a Muscle

Before plugging in a ThermoFlex Muscle, run the code once to verify things are working.

> ⚠️ **Warning:** The example script in Step 8 does _not_ include temperature control. If you leave the muscle powered for too long, it can overheat — especially at higher setpoints. That’s why we strongly recommend testing the program without a muscle first. Once you're confident it runs correctly, connect the muscle and go **low and slow** until you dial in the right settings.
>
> 🚨 We've tested muscles under a 25 lb load, and they can reach operating temperature in **about two seconds** from room temp. That's fast — and hot. Until you’re confident in your setup, don’t exceed that load or duration. If you're unsure, send us a message with what you're trying to do and we’ll help you out.
>
> 💡 **Fun fact:** Both the applied load and the starting temperature of the muscle will affect how quickly it heats up. So if your room is hot or your robot is jacked, it may respond faster than expected!

If all’s good, Port 0’s LED will glow.

> **GIF/photo goes here:** (Insert photo of Port 0 LED lighting up — bonus points for dramatic lighting)

Only _after_ the light show should you connect a muscle to Port 0.

***

### 2. First Program: Move a Muscle

Here’s our muscle equivalent of “Hello World.” Save this as `first_program.py`:

```python
import thermoflex as tf  # Import the ThermoFlex API
import time  # Standard time module for delays

# Discover and connect to the first Node over USB
node_net = tf.discover([105])[0]  # 105 is the default USB connection code
node_net.refreshDevices()  # Refresh to find connected devices

# Wait briefly to ensure discovery is complete
time.sleep(1)

# Get the actual Node object from the discovered list
node = node_net.node_list[0]

# Define a muscle object and assign it to Port 0 (aka M1)
muscle = tf.Muscle(idnum=0)  # idnum = 0 maps to Port 0 (labeled M1 on the board)
node.setMuscle(0, muscle)  # Physically connects the virtual muscle to the board

# Move the Muscle
print("Activating Muscle!")
muscle.setMode("percent")  # Set control mode to % power (0 to 1 range)
muscle.setSetpoint("percent", 0.5)  # Command 50% power
muscle.setEnable(True)  # Enable the muscle (starts heating)
tf.delay(5)  # Wait 5 seconds — muscle should contract

# Reduce power to avoid overheating
muscle.setSetpoint("percent", 0.1)  # Drop to 10% to cool slightly

tf.delay(15)  # Wait 15 seconds — adjust based on your setup and safety

# Stop the Muscle
print("Stopping Muscle!")
node.disableAll()  # Turns off all outputs

time.sleep(1)
tf.endAll()  # Cleanly end session (important for USB stability)
```

Or grab it here: [simple example on GitHub](https://github.com/Delta-Robotics-Inc/ThermoFlex-Python-API/blob/main/getting-started/muscle-simple.py)

***

### 3. Next Steps & Troubleshooting

* **Check the API docs:** [ThermoFlex API Docs](https://docs.deltaroboticsinc.com/software/thermoflex-tm-python-api)
* **GitHub Issues:** [Report bugs or ask questions](https://github.com/Delta-Robotics-Inc/ThermoFlex-Python-API/issues)
* **Still stuck?** Email us. We’ll help you out and maybe even include a meme.

***

Now go forth and actuate. Whether you’re building a bionic arm, a robot tentacle, or just trying to impress your cat — you’re officially part of the future.

Welcome to Delta Robotics.

***

**P.S.** Don’t forget to share your builds with us. We like seeing weird, wonderful, moving things.

<figure><img src="../../.gitbook/assets/1.png" alt=""><figcaption></figcaption></figure>

***
