---
description: >-
  This part of the guide will walk you through setting up your ThermoFlex™ Node
  and running your first program without screaming into the void.
---

# Update library & firmware

## Set up your ThermoFlex™ Node.

***

### 1. Before We Begin: System Requirements

Let’s make sure your computer isn’t stuck in the Stone Age:

* **Operating System:** Windows 10/11, macOS, or Linux (Ubuntu recommended)
* **Python:** Version 3.8 or later (we recommend 3.13 for best results)
* **Permissions:** Admin privileges for driver installation
* **USB Port:** Yes, you need one. Preferably not already used for your desk fan.

***

### 2. Plug In Your Node

Use the included USB-C cable to plug the ThermoFlex™ Node into your computer. It’ll light up. If it doesn’t, check the cable or try a different port.

> **GIF goes here:** (Insert gif of LED pattern when it powers up successfully, a pleasant little dance to say "I'm alive!")

***

### 3. USB Driver Installation (Windows)

If your computer didn’t pop up a cheerful "device connected" notification, you may need to install the driver.

**Step-by-step:**

1. Hit `Win + R`, type `devmgmt.msc`, and hit Enter.
2. Look under `Ports (COM & LPT)`  You should see something like **USB Serial Device (COMx)**.
3. If it’s missing or has a yellow ⚠️, check out this [general USB driver troubleshooting guide from SparkFun](https://learn.sparkfun.com/tutorials/how-to-install-ftdi-drivers/all) for help identifying and installing the right driver for your system.
4. Unplug and replug the Node. You should now see it listed properly.

> **Photo goes here:** (Insert screenshot of correct COM port listing in Device Manager)

***

### 4. Install Python (Stable Method)

Let’s get Python talking to your Node. If you already have it installed, you can skip this part and jump ahead like a seasoned time traveler.

1. Download Python from [python.org](https://www.python.org/downloads/) (3.13+ recommended).
2. During install, make sure to check `Add Python to PATH`. That’s not a suggestion.
3. Open a terminal or command prompt and run:

```bash
python --version
```

You should see something like:

```bash
Python 3.13.3
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

You’ve got two main ways to write and run your first script, choose your own adventure:

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
