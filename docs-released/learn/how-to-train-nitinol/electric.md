---
description: Extremely quick high-precision shape setting process (Experimental)
---

# Electric

On this page, we focus on using **Delta Robotics’** [**ThermoFlex™ Node**](https://www.deltaroboticsinc.com/product-page/thermoflex-kit) to perform shape-setting of Nitinol wires through controlled electrical heating. The ThermoFlex Node is a smart current controller designed for Nitinol “muscle” wires, and it can be a powerful tool for training your wire with precision. Instead of using external heaters like torches or ovens, the Node passes an electric current through the wire to heat it (Joule heating). We’ll cover the benefits of this approach – such as precise, localized heating and easy monitoring – and guide you on how to safely execute shape-setting with the Node. We’ll also show an example (in pseudocode) of using the Node’s API to automate the process. By harnessing the ThermoFlex Node, you can achieve repeatable training results with high accuracy.

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
* **Configure the Node (Current and Duration):** Using the Node’s API or control software, set up the shape-setting parameters. The key settings will be:
  * **Current Level or Target Temperature:** You might either directly control via current or use a target temperature if the Node/firmware supports that (with resistance feedback). For example, you might determine that a certain current (say 8 A for a given wire diameter) corresponds to roughly 550 °C. You can then command the Node to regulate around that current or temperature. If an API call exists to set a temperature, it likely internally does the regulation by adjusting the current on the fly. Otherwise, you can do a simple approach: set a constant current that you know will keep the wire at the desired temperature. It’s advisable to err on the lower side and possibly do some trial calibration – for instance, start with a current that you think will reach \~500 °C, run for a short time, and check (some Nodes can give you the resistance reading, which correlates to temperature). Many ThermoFlex users have a chart or formula for current vs. temperature for their wire (because it depends on wire gauge and length).
  * **Duration (Hold Time):** Set the time for which the current will run. As with other methods, something like 20 minutes is a good baseline for thorough shape-setting​ \[1]. The Node might allow a timed run, or you might have to implement a timer in code to stop it. Ensure you also plan how to stop the current after the duration, either manually or via code, to avoid overshooting the intended heating time.
  * **Ramp or Pulse (Optional):** Advanced use – some prefer not to just slam full current instantly. You could ramp the current up over a few seconds to reduce thermal shock, especially for thicker wires, although Nitinol generally can handle rapid heating. The Node might support pulsed heating or ramp profiles. If available, you might ramp to setpoint over, say, 30 seconds.
  * **Monitoring Setup:** If using feedback, ensure it’s enabled (for example, resistance-based control mode). Also, set the data logging interval if you want to capture data.
* **Execute the Shape-Set Cycle:** Start the heating process. The Node will drive current through the wire, heating it. If all is well, the wire will quickly rise in temperature. **Do not leave it unattended** – even though it’s automated, always supervise in case of any issues (like a connection coming loose or an unexpected temperature overshoot). If you see the wire glowing bright or other concerning signs, stop the process. Under normal operation with correct settings, the wire should reach a steady glow (dull red). The Node (with feedback) will adjust the current to maintain the target. If no feedback, the wire will find an equilibrium where heat loss = heat input; that equilibrium should be at your target if the current was chosen correctly.
* **Hold and Monitor:** Let the wire stay at the temperature for the configured duration. Use the Node’s readings to monitor. For example, if the Node API provides real-time resistance or an estimated temperature, watch that it stays roughly constant, indicating steady-state. If you see a drift, that might mean the wire’s resistance is changing (possibly annealing effects) – slight increase in resistance is normal as it fully austenitizes. The Node might compensate by lowering current slightly to hold temp.
* **Cool Down:** When the time is up, stop the current. The wire will begin cooling immediately. You can choose to **quench** it or just let it cool in the air. With the Node setup, a water quench is a bit tricky because the wire is wired up to the device. **Do not quench while still connected to the Node** – first, disconnect power or open the circuit (some Nodes might have a quick release, or you can simply turn it off and wait a few seconds). You don’t want to dunk the Node or live wires in water! The better approach in this case, if quenching is desired, is to quickly disconnect one end of the wire from the Node (using insulated tools) and then drop the wire (with fixture) into water. Alternatively, since electrical heating cools the wire quickly once the current is off (the wire is thin and loses heat fast to air), you might get away with just an air cool. If you do air-cool, you can accelerate it by gently blowing air (room temp air or even a fan, **not** cold compressed air, which can shock-cool too fast, causing thermal stress).
* **Disconnect and Inspect:** Once the wire has cooled to a safe handling temperature, fully disconnect the wire from the Node leads. Inspect the wire – it should now hold the trained shape. Check your fixture and wire for any signs of overheating (e.g., melted supports if any or char if you had tape/markers). If everything looks good, proceed to remove the wire from the fixture as described in the basic guide. The shape should be set.

### Example: Using the ThermoFlex Node API

Below is a **pseudocode example** that demonstrates how one might use the ThermoFlex Node’s API to run a shape-setting routine. This assumes a Python-like pseudocode where a library or interface is available to control the Node. (The actual API calls might differ; consult the ThermoFlex Node documentation for precise syntax.)

```python
pythonCopyEdit# Pseudocode for shape-setting using ThermoFlex Node

from thermoflex_node import ThermoFlexNode  # hypothetical import of a Node API

# Initialize connection to the ThermoFlex Node (e.g., via serial or USB)
node = ThermoFlexNode(port="/dev/ttyUSB0")  # using the correct port or identifier
node.connect()

# Safety check: ensure node is in manual control mode and not running
node.stop_all()  
node.set_mode("manual")  # switch to manual control mode for direct commands

# Configure shape-setting parameters
target_temp = 550  # Target temperature in °C for shape setting
hold_time = 20 * 60  # Hold time in seconds (20 minutes)

# If the Node supports setting a target temperature with feedback:
node.set_target_temperature(target_temp)
node.set_hold_time(hold_time)
node.start_heating()

# Monitor progress (pseudo-monitoring loop)
elapsed = 0
while node.is_heating():
    temp = node.get_current_temperature()      # reading from Node's sensors/estimates
    curr = node.get_output_current()           # current in Amps
    volt = node.get_output_voltage()           # voltage across the wire
    res = volt / curr if curr > 0 else None    # calculate resistance as V/I (Ohm's law)
    print(f"Time: {elapsed}s, Temp: {temp:.1f}°C, Current: {curr:.1f}A, Resistance: {res:.4f}Ω")
    sleep(5)  # log every 5 seconds (for example)
    elapsed += 5

# Once done, ensure heating has stopped
node.stop_heating()
node.disconnect()
print("Shape-setting cycle complete. Wire is now cooling down.")
```

In the above pseudocode, we:

* Connect to the ThermoFlex Node.
* Set it to a manual or appropriate mode for direct control.
* Specify a target temperature (550 °C) and a hold time (20 minutes).
* Start the heating process.
* Enter a loop to periodically retrieve data (temperature, current, voltage) for monitoring/logging. We compute resistance as well, which is a useful metric: for instance, if the resistance stabilizes, it implies temperature is steady; if it starts rising slowly, it could mean the wire is heating more or undergoing structural changes.
* After the hold time, the Node stops heating automatically (in this pseudocode, `node.is_heating()` would become false once the hold\_time has elapsed).
* We stop and disconnect, concluding the process.

**Note:** The exact API will vary. Some Nodes might not directly take a temperature but require you to set a current. In that case, you might do something like `node.set_output_current(8.0)` (Amps) instead of a temperature, and manually control the duration in your code. Or, if you have a lookup for current vs temperature, you could implement a feedback loop in code: e.g., gradually adjust current to hit a resistance value corresponding to 550 °C. The above is a simplified example to illustrate the concept.

### Safety Guidance for Electrical Shape-Setting

While using the Node removes flames, it introduces electrical considerations:

* **Never Exceed Device Limits:** Check the ThermoFlex Node’s spec for maximum current and voltage. Do not set a current beyond what the Node or the wire can handle. (For example, if the Node can supply up to 30 A continuously, stay at or below that. Similarly, thin wires can fuse like a fuse-wire if over-currented.) A good practice is to start low and incrementally increase current while monitoring the wire’s temperature.
* **Avoid Short Circuits:** Double-check that the only path for current is **through the entire length of the wire** you want to heat. If you accidentally allow a shorter path (say the wire touching a metal fixture connecting the two ends), the current will bypass most of the wire, possibly overheating the small section that is conducting or damaging the Node’s output drivers. Use insulating spacers and keep the fixture design in mind.
* **Monitor at All Times:** Just as you wouldn’t leave a torch unattended, don’t leave the Node running unattended. The wire could potentially overheat if, say, the feedback mechanism fails or if an incorrect parameter is set. Keep an eye on it or have an emergency cutoff in software (for instance, if measured temperature exceeds a threshold, immediately stop).
* **Cooling Period:** After the run, let everything cool before touching it. The wire will be extremely hot, and so might be the Node’s terminals that are connected to it (since heat can conduct back a bit). Power down the Node if possible when done, as an added safety.
* **Ventilation:** There’s no combustion, but if the wire has any sort of coating or the fixture has paint, those could burn off. Ensure the area is ventilated. Additionally, high temperatures can oxidize the wire surface, releasing a little smoke. It’s generally much less than a flame-based heating, but still be in a ventilated space.
* **Electrical Safety:** The Node likely uses DC power (battery or DC supply). Ensure that the power source you use is safe (properly rated, no exposed live wires). If using a high-power battery, be aware of the high current draw and ensure the battery and Node are properly cooled (large currents can heat cables and connectors, too).

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

