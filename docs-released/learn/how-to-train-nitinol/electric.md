---
description: Extremely quick high-precision shape setting process (Experimental)
---

# Electric

On this page, we focus on using **Delta Robotics’** [**ThermoFlex™ Node**](https://www.deltaroboticsinc.com/product-page/thermoflex-kit) to perform shape-setting of Nitinol wires through controlled electrical heating. The ThermoFlex Node is a smart current controller designed for Nitinol “muscle” wires, and it can be a powerful tool for training your wire with precision. Instead of using external heaters like torches or ovens, the Node passes an electric current through the wire to heat it (Joule heating). We’ll cover the benefits of this approach – such as precise, localized heating and easy monitoring – and guide you on how to safely execute shape-setting with the Node. We’ll also show an example (in pseudocode) of using the Node’s API to automate the process. By harnessing the ThermoFlex Node, you can achieve repeatable training results with high accuracy.

**(This guide contains the guidelines for this process and if you would like to try this out for yourself, please** [**reach out to Mark**](mailto:mark@deltaroboticsinc.com) **for actual code and recommendations)**

> **Note:** _Preconfigured shape-set profiles are coming soon._ Delta Robotics is developing built-in “shape training” routines for the ThermoFlex Node. These will be available via firmware updates or the API, providing one-command execution of common training cycles (with recommended currents, durations, and ramping). Once available, you’ll be able to select a profile (for example, “Standard 550°C 20min shape-set for 0.5 mm wire”) and the Node will automatically run that sequence. This will simplify the process even further and ensure users apply proven parameters. Keep an eye on the ThermoFlex Node documentation for these updates.

***

### Quick Disclaimer

Working with Nitinol involves high-temperature processes and equipment that carry inherent risks. Delta Robotics provides these guidelines for educational and informational purposes only. It is your responsibility to exercise caution, follow all provided safety instructions, and take appropriate safety measures.

Always:

* Wear appropriate protective gear, including heat-resistant gloves, safety glasses, and protective clothing.
* Ensure proper ventilation when heating materials.
* Maintain ready access to fire safety equipment, including fire extinguishers.
* Handle all heated materials and equipment cautiously, using appropriate tools.

Delta Robotics shall **NOT** be held responsible for any injury, damage, or loss incurred through improper or unsafe handling of materials, equipment, or processes described in our guides.

Please prioritize safety at all times and perform these procedures at your own risk.

***

### Why Use Electrical Shape-Setting?

Electrical (resistance) heating for Nitinol training has several advantages:

* **Precise, Localized Heating:** The wire becomes its heating element. You can heat exactly the section of wire you need to shape-set without wasting energy on the surrounding air or fixtures. This localization means you can reach target temperature _fast_. High current can bring the wire to 500–550 °C within seconds, and turning off the current allows it to cool quickly. This rapid heating and cooling can prevent unintended over-aging of the material​ \[1]; in other words, the wire spends less time at high temperature than it would in a slow furnace ramp, preserving properties.
* **Controlled by Current and Feedback:** The ThermoFlex Node can regulate the current, and with appropriate feedback by measuring the wire’s electrical resistance, it’s possible to reach and hold a desired temperature very accurately​. The ThermoFlex Node controller also includes two standard JST connector ports for monitoring external sensors to provide even more control. The **resistance of Nitinol increases with temperature** \[1], so by monitoring the voltage and current, the Node can infer the wire’s temperature. In practice, this means you can implement a closed-loop system: “Apply current until the wire is \~550 °C, hold it there for 20 minutes, then shut off.” This level of control yields **consistent and repeatable results** for shape-setting \[1].
* **Minimal Equipment:** Aside from the ThermoFlex Node (and a power source for it), you don’t need large ovens or special furnaces. A Node, a computer, a DC power source, and your wire fixture setup will suffice. This makes it accessible for a small lab or even field use. It’s an **inexpensive setup** compared to industrial furnaces​ \[1].
* **Data Monitoring and Logging:** Because the process is electrical, you can easily log data like current, voltage, estimated temperature, etc., via the Node’s API. This lets you analyze the shape-setting cycle after the fact or ensure everything went according to plan in real time. For example, you might log the resistance over time and see that it plateaued – confirmation the wire reached steady state at the set temperature.
* **Safety and Cleanliness:** No open flames are involved, and the heat is concentrated in the wire. That reduces the risk of accidental fires or widespread hot surfaces. (However, note that the wire _will_ get extremely hot, so safety is still paramount – more on that below.) Also, you avoid combustion byproducts; the process is relatively clean except for any oxide that forms on the wire.

In summary, using the ThermoFlex Node for shape-setting combines the **speed of a torch** with the **control of a furnace**, and it’s particularly well-suited for the ThermoFlex system since it was designed to drive these wires.

### Setup and Procedure

Before running a shape-set cycle with the ThermoFlex Node, ensure you have the following prepared:

* **Wired Fixture:** Similar to the other methods, you need to **constrain the Nitinol wire in the desired shape**. Because we’ll be running current through the wire, the fixture **must not create a short circuit**. This usually means using a non-conductive fixture or ensuring the wire’s ends are electrically isolated except at the Node’s connection. Common approach: use ceramic or high-temp plastic pins to guide the wire shape or a fiberglass/ceramic board with anchors. If you use a metal fixture (like clamping between metal plates), you have to isolate the wire from the fixture at least at one end, otherwise, the current might bypass the segment of the wire (going through the fixture) or just short out.\
  Make sure the fixture can handle the heat (use materials like ceramic, stainless steel, or Nichrome hooks, etc.). The wire will still reach \~550 °C, so treat this like a high-temperature setup.
* **Connect the ThermoFlex Node:** Attach the ends of the Nitinol wire to the Node’s output terminals. Typically, the ThermoFlex Node will have clamp or screw terminals where you can secure the wire. Ensure a **solid electrical connection** – loose connections can lead to sparking or inconsistent current flow. Also, ensure the connecting leads from the Node to the wire can handle the current and heat (use the leads provided with the Node or appropriate gauge wires, and keep them away from direct contact with the hot section of the Nitinol).
* **Configure the Node (Current and Duration):** Using the Node’s Python API, set up the shape-setting parameters. The key settings will be:
  * **Current Level or Target Temperature:** The ThermoFlex Node controller enables you to set a target resistance for the controller to hold. For our experiments, we used a source meter to determine the precise resistance of our coils (150 mOhms for a ThermoFlex coil 2mm wire diameter). We then ran our program while increasing the level until we achieved good results from the actuator. Until we have a better model for selecting a resistance level based on your actuator characteristics (wire diameter and length), we recommend repeating this process similarly. If you would like to read literature to understand a good baseline for your wire, see our [further research section](../further-research.md) for recommened places to start.
  * **Duration (Hold Time):** Set the time for which the current will run. As with other methods, something like 20 minutes is a good baseline for thorough shape-setting​ \[1]. You should implement this timed run in a python script, disabling the Node muscle port after the experiment finishes.
  * **Ramp or Pulse (Optional):** Advanced use – some prefer not to just slam full current instantly. You could ramp the current up over a few seconds to reduce thermal shock, especially for thicker wires, although Nitinol generally can handle rapid heating. You might ramp to setpoint over, say, 30 seconds.
  * **Monitoring Setup:** If using feedback, ensure it’s enabled (for example, resistance-based control mode). Also, set the data logging interval if you want to capture data (information on how to enable logging is in progress so reach out on how to do that).
* **Execute the Shape-Set Cycle:** Start the heating process. The Node will drive current through the wire, heating it. If all is well, the wire will quickly rise in temperature. **Do not leave it unattended** – even though it’s automated, always supervise in case of any issues (like a connection coming loose or an unexpected temperature overshoot). **If you see the wire glowing bright or other concerning signs, stop the process using the left button on the Node (halts power output) or for drastic circumstances with the reset button/pull the power**. Under normal operation with correct settings, the wire should reach a steady glow (dull red) when the lights are off. The Node (with feedback in resistive mode) will adjust the current to maintain the target. If no feedback, the wire will find an equilibrium where heat loss = heat input; that equilibrium should be at your target if the current was chosen correctly.
* **Hold and Monitor:** Let the wire stay at the temperature for the configured duration. Use the Node’s readings to monitor. For example, if the Node API provides real-time resistance, watch that it stays roughly constant, indicating steady-state. If you see a drift, that might mean the wire’s resistance is changing (possibly annealing effects) – slight increase in resistance is normal as it fully austenitizes. The Node might compensate by lowering current slightly to hold temp.
* **Cool Down:** When the time is up, stop the current. The wire will begin cooling immediately. You can choose to **quench** it or just let it cool in the air (we hit it with a pressurized air hose). With the Node setup, a water quench is a bit tricky because the wire is wired up to the device. **Do not water quench while still connected to the Node** – first, disconnect power or open the circuit. You don’t want to dunk the Node or live wires in water! The better approach in this case, if quenching is desired, is to quickly disconnect one end of the wire from the Node (using insulated tools) and then drop the wire (with fixture) into water. Alternatively, since electrical heating cools the wire quickly once the current is off (the wire is thin and loses heat fast to air), you might get away with just an air cool. If you do air-cool, you can accelerate it by blowing with pressurized air.
* **Disconnect and Inspect:** Once the wire has cooled to a safe handling temperature, fully disconnect the wire from the Node leads. Inspect the wire – it should now hold the trained shape and experience a visible color change (our material did). Check your fixture and wire for any signs of overheating (e.g., melted supports if any or char if you had tape/markers). If everything looks good, proceed to remove the wire from the fixture as described in the basic guide. The shape should be set.

### Example: Using the ThermoFlex Node API

Below is an **example** that demonstrates how one might use the ThermoFlex Node’s API to run a shape-setting routine. (This code may or may not need to be updated to the newest version of the ThermoFlex API).

````python
```python
'''
This program utilizes the resistance control mode with the ThermoFlex Python API.
Tested with thermoflex library v1.0.1 and Node Controller firmware v1.0.1

Summary
This script sets up a connection with a ThermoFlex Node Controller, logs data during a predefined experiment,
parses the data, and visualizes it in real-time using Matplotlib. The experiment is controlled via the ThermoFlex API,
and the data is continuously updated and displayed in a set of subplots.

@author: Mark Dannemiller
'''

import thermoflex as tf
import time
import matplotlib.pyplot as plt
from timeit import default_timer

# Data storage arrays
time_data = []
m1_en_data = []
vbatt_data = []
vld_data = []
amps_data = []
resist_data = []
pwm_data = []

def get_data(node, muscle):
    """Get and parse data from the node and muscle objects"""
    try:
        # Get node status
        node_status = node.getStatus()
        if node_status:
            # Parse node status data
            vbatt = node.node_status['volt_supply']
            if vbatt is not None:
                vbatt_data.append(vbatt)
                time_data.append(int(time.time() * 1000))  # Current time in ms

        # Get muscle status
        muscle_status = muscle.SMA_status
        if muscle_status:
            vld = muscle_status['load_voltdrop'][-1] if muscle_status['load_voltdrop'] else 0
            amps = muscle_status['load_amps'][-1] if muscle_status['load_amps'] else 0
            ohms = muscle_status['r_sns_ohms'][-1] if muscle_status['r_sns_ohms'] else 0
            pwm = muscle_status['pwm_out'][-1] if muscle_status['pwm_out'] else 0

            vld_data.append(vld)
            amps_data.append(amps)
            resist_data.append(ohms)
            pwm_data.append(pwm)
            m1_en_data.append(muscle.enable_status)

    except Exception as e:
        print(f"Error getting data: {e}")

def plot_data(ax, title, x_label, y_label, x_arr, y_arr, y_range, history):
    """Plot data with specified parameters"""
    ax.clear()
    start_index = len(x_arr) - history
    if start_index < 0 or history < 0:
        start_index = 0
        start_range = 0
    else:
        start_range = x_arr[start_index]
        
    for i in range(start_index, len(x_arr) - 1):
        if x_arr[i] < x_arr[i + 1]:
            # Normalize pwm_data to be between 0 and 1
            normalized_value = pwm_data[i] / 255.0
            # Get color from the 'cool' colormap
            color = plt.cm.cool(0.5)
            ax.plot(x_arr[i:i + 2], y_arr[i:i + 2], color)

    ax.set_xlim(start_range, x_arr[-1] + 1000)
    ax.set_ylim(0, y_range)
    ax.set_title(title)
    ax.set_xlabel(x_label)
    ax.set_ylabel(y_label)

def update_plot(history):
    """Update all plots with current data"""
    if len(time_data) > 0:
        plot_data(ax1, 'VBatt Data', 'Log Time (ms)', 'Voltage (V)', time_data, vbatt_data, 24, history)
        plot_data(ax2, 'V_LD Data', 'Log Time (ms)', 'Voltage (V)', time_data, vld_data, 30, history)
        plot_data(ax3, 'Amps Data', 'Log Time (ms)', 'Current (A)', time_data, amps_data, 100, history)
        plot_data(ax4, 'M2 Resist Data', 'Log Time (ms)', 'Resistance (mΩ)', time_data, resist_data, 1000, history)

        fig.tight_layout()
        plt.pause(0.001)

def delay(wait_time, node, muscle):
    """Delay while collecting data"""
    start = default_timer()
    while default_timer() - start < wait_time:
        get_data(node, muscle)
        tf.update()

# Initialize the plot
plt.style.use("fivethirtyeight")
fig, ((ax1, ax2), (ax3, ax4)) = plt.subplots(2, 2, figsize=(10, 8))

# Experiment parameters
wait1 = 1200.0  # Main heating time
wait2 = 5.0    # Cooling time
setpoint = 170  # Resistance setpoint in mΩ (calibrated for 550°C)

# Discover and setup the ThermoFlex network
node_net = tf.discover([105])[0]  # Discover networks over USB and get the first one
node_net.refreshDevices()  # Discover all Node devices on the selected network
tf.delay(1)  # Wait for the devices to be discovered

node = node_net.node_list[0]  # Get the first connected Node
muscle = tf.Muscle(idnum=0)  # Create muscle object for M1
node.setMuscle(0, muscle)  # Assign the muscle to the Node at port 0

# Configure the muscle for resistance control
muscle.setMode("ohms")
muscle.setSetpoint(setpoint=setpoint)

# Start the experiment
node.disableAll()  # Ensure all muscles are disabled initially
tf.delay(0.5)  # Wait for commands to be processed

# Enable logging and start the muscle
node.setLogmode(2)  # Set to dump mode for detailed logging
muscle.setEnable(True)

# Run the main heating phase
delay(wait1, node, muscle)

# Disable the muscle and monitor cooling
node.disableAll()
delay(wait2, node, muscle)

# Print final data
print("Time data:", time_data)
print("Enable status:", m1_en_data)
print("Battery voltage:", vbatt_data)
print("Current:", amps_data)
print("Load voltage:", vld_data)
print("Resistance:", resist_data)
print("PWM:", pwm_data)

# Show final plot
update_plot(-1)

# Clean up
tf.endAll()

```
````

In the above code, we:

* Connect to the ThermoFlex Node.
* Set it to a manual or appropriate mode for direct control.
* Specify a target temperature resistance (550 °C)=170mOhms and a hold time (20 minutes).
* Start the heating process.
* Enter a loop to periodically retrieve data (temperature, current, voltage) for monitoring/logging. We compute resistance as well, which is a useful metric: for instance, if the resistance stabilizes, it implies temperature is steady; if it starts rising slowly, it could mean the wire is heating more or undergoing structural changes.
* After the hold time, the Node stops heating automatically
* We stop and disconnect, concluding the process.

### Safety Guidance for Electrical Shape-Setting

While using the Node removes flames, it introduces electrical considerations:

* **Never Exceed Device Limits:** Check the ThermoFlex Node’s spec for maximum current and voltage. Do not set a current beyond what the Node or the wire can handle. (For example, if the Node can supply up to 30 A continuously, stay at or below that. Similarly, thin wires can fuse like a fuse-wire if over-currented.) A good practice is to start low and incrementally increase current while monitoring the wire’s temperature.
* **Avoid Short Circuits:** Double-check that the only path for current is **through the entire length of the wire** you want to heat. If you accidentally allow a shorter path (say the wire touching a metal fixture connecting the two ends), the current will bypass most of the wire, possibly overheating the small section that is conducting or damaging the Node’s output drivers. Use insulating spacers and keep the fixture design in mind.
* **Monitor at All Times:** Just as you wouldn’t leave a torch unattended, don’t leave the Node running unattended. The wire could potentially overheat if, say, the feedback mechanism fails or if an incorrect parameter is set. Keep an eye on it or have an emergency cutoff in software (for instance, if measured temperature exceeds a threshold, immediately stop).
* **Cooling Period:** After the run, let everything cool before touching it. The wire will be extremely hot, and so might be the Node’s terminals that are connected to it (since heat can conduct back a bit). Power down the Node if possible when done, as an added safety.
* **Ventilation:** There’s no combustion, but if the wire has any sort of coating or the fixture has paint, those could burn off. Ensure the area is ventilated. Additionally, high temperatures can oxidize the wire surface, releasing a little smoke. It’s generally much less than a flame-based heating, but still be in a ventilated space.
* **Electrical Safety:** The Node uses DC power (battery or DC supply). Ensure that the power source you use is safe (properly rated, no exposed live wires). If using a high-power battery, be aware of the high current draw and ensure the battery and Node are properly cooled (large currents can heat cables and connectors, too).

By adhering to these guidelines, electrical shape-setting can be conducted safely and effectively.

### Benefits Recap and Looking Forward

Using the ThermoFlex Node for shape-setting offers a high degree of control. You can fine-tune the shape-setting process to achieve **consistent outcomes**. Research has demonstrated that Joule heating methods can produce very reliable shape-setting results, often with less trial-and-error compared to furnace methods​

The ability to log data also means you can build up a knowledge base: for example, noting the exact resistance at target temperature for your wire helps future runs.

**Advantages Summary:**

* Achieve target temperature quickly, avoiding prolonged high-temp exposure (which can preserve better material properties).
* Easy to repeat the exact same thermal cycle via software – just run the same code again for another wire.
* Integrate shape-setting into an automated workflow. For instance, an engineering team could have a script that shape-sets a batch of muscle wires and then automatically performs some test cycles on them – all using the Node and connected sensors.
* If you only have one or a few wires to train, this method saves a lot of time compared to heating up a full furnace.

**Limitations:** One should note that electrical shape-setting works best for relatively **straightforward shapes** (like springs, straight actuators, etc. – typical for ThermoFlex muscles). If you have a very complex 3D shape that isn’t just a single continuous wire or if the wire is part of a larger assembly, you might still need the oven approach. But for most cases involving Delta Robotics ThermoFlex wires, the Node method is ideal.

***

### Final Thoughts

By leveraging the ThermoFlex Node, users can bring **engineering-grade precision** to what was once a labor-intensive task. Whether you’re a hobbyist benefiting from the Node’s ease of use or a researcher needing consistent training for experiments, electrical shape-setting is a powerful technique. Always pair technology with understanding: even with automated control, remember the fundamentals of Nitinol training (from the Basic and Advanced guides) – they’ll help you interpret data and fine-tune as needed.

With this documentation, ThermoFlex users at any level should feel empowered to train their Nitinol wires safely and effectively, unlocking the incredible capabilities of shape memory alloy technology in their projects.

***

### Referances

\[1] - [Rapid, Reliable Shape Setting of Superelastic Nitinol for Prototyping Robots](https://pmc.ncbi.nlm.nih.gov/articles/PMC5026417/)

