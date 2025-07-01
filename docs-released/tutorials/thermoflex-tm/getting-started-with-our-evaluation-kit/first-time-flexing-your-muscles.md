---
description: This page walks you through running your first script.
---

# First time flexing your muscles

## Run Your First Program Using the ThermoFlex™ Python API

_Flex it. Don’t fry it._

<h2 align="center">🚨🚨🚨 READ THIS FIRST 🚨🚨🚨</h2>

### 🔥 Disclaimer: Use at Your Own Risk

This is experimental tech. It uses **high-discharge batteries to heat metal wires**, and if misused, it can get dangerously hot, melt stuff, or start a fire.

By purchasing and using this product, you understand and agree that:

* This is **an experimental device** intended for research and prototyping.
* You must operate it **in a well-ventilated area**, away from flammable or meltable objects.
* You are responsible for using this product safely and intelligently.
* **Delta Robotics Inc. is not liable for any damage, injury, or fire** resulting from its use.

We’ve taken every reasonable measure to make our products safe — and we’re working hard to make them even safer — but this system must be used **at your own risk**.

<h2 align="center"><mark style="color:red;"><strong>You have been warned!</strong></mark></h2>

***

### 🚨 Run the Node Before Connecting a Muscle

This step is **not optional**. Skipping it could destroy your ThermoFlex™ Muscle before it even flexes.

Before plugging anything into the output port:

* **Run the script once with no muscle connected.**\
  This confirms that your Node is alive and responding before it starts pushing current. If your code glitches and the muscle is connected, it can **overheat and fail in seconds**.

#### Why This Matters:

* The basic example script has **no temperature sensing or current limits**.
* If your setup delivers too much power for too long, the muscle will **melt its sleeve, deform, or snap entirely**.
* Nitinol doesn’t forgive. Once it’s cooked, it’s done.

***

### ⚡ High-Discharge LiPo = High Risk

If you're using an **11.1 V LiPo with a high C-rating**, the Node can unleash huge surges of current. It doesn’t limit output — it gives the muscle whatever the battery allows. That power can cook your actuator instantly.

#### We Recommend:

* Use a **3S 5200 mAh 80C LiPo with XT60** — our house standard.
* If you're new, go with a **lower C-rating** to reduce risk.
* Add an **inline fuse** or a **current-limiting circuit**.
* Upcoming firmware and hardware updates will add **onboard thermal sensing** and **safer defaults**, but until then, proceed with caution.

***

### 1. Understand the Script You’re About to Run

This is our “Hello, World!” for muscles; it runs a simple 5-second heating cycle to make the actuator flex, then drops power to avoid damage.

Here’s what you should know:

* The script uses **percent-based control**, _not_ temperature or current regulation.
* It’s calibrated for **11.1 V input**. If you’re using a different voltage, results will vary.
* **Too much time = cooked muscle.** The example assumes \~5 seconds is safe for typical setups, but **you need to calibrate it for your own hardware**.

***

### 2. How to Calibrate the Flex Safely

If you’re running the script for the first time _with a muscle_, do this:

1. **Set a high timeout** — something like `tf.delay(100)` to give yourself plenty of buffer (but don't let it actually run that long).
2. **Lower the power** — set `"percent"` to `0.3` or less. You can raise it later.
3. **Watch the LED** on the Node. It blinks when the muscle is enabled.
4. **Start a stopwatch** at the same moment the LED turns on.
5. **Manually disable the muscle** using the Node Controller button when the actuator finishes contracting.
6. **Record the time** it took to reach full contraction. Use that number in your script for safe automation.
7. Wait **30–40 seconds between runs** to allow the muscle to cool, or use compressed air for faster testing.

***

### 3. Your First Flex Script

Save this as `first_program.py` and run it using Python:

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
tf.delay(5)  # Run for 5 seconds at 50% — muscle should contract

# Reduce power to avoid overheating
muscle.setSetpoint("percent", 0.1)  # Drop to 10%

tf.delay(10)  # Run for 10 seconds at 10%  — adjust based on your setup and safety

# Stop the Muscle
print("Stopping Muscle!")
node.disableAll()  # Turns off all outputs

time.sleep(1)
tf.endAll()  # Cleanly end session (important for USB stability)
```

Or grab it here: [simple example on GitHub](https://github.com/Delta-Robotics-Inc/ThermoFlex-Python-API/blob/main/getting-started/muscle-simple.py)

***

### 4. Next Steps & Troubleshooting

* [Read the ThermoFlex API Docs](https://github.com/DeltaRoboticsInc/ThermoFlex#api-documentation)
* [Report bugs or ask questions on GitHub](https://github.com/DeltaRoboticsInc/ThermoFlex/issues)
* Still stuck? Email us. We’ll help — and probably send a meme too.

***

Now go forth and actuate. Whether you’re building a robot arm, a cyborg salamander, or a muscle-powered marshmallow launcher, you’re officially part of the future.

**Welcome to Delta Robotics.**

_P.S. Share your builds — we love weird, wiggly, wonderful machines._

***

<figure><img src="../../../.gitbook/assets/1.png" alt=""><figcaption></figcaption></figure>
