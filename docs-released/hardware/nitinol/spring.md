---
description: >-
  An human-friendly guide to Delta Robotics’ Nitinol Tension Springs — covering
  specs, control, cooling, and how not to accidentally cook your actuator.
---

# Spring

## **Nitinol Tension Springs: Tiny Coils with Big Pull**

At Delta Robotics, we don't just sell wire — we also sell wire that’s been coiled into little powerhouses. Meet our **Nitinol Tension Springs**, precision-formed from shape memory alloy, ready to yank, lift, and contract with muscle-like motion. They’re like the wire’s gym-rat cousin: more compact, still ripped.

This page walks you through what they are, how they work, and how to keep them springing instead of snapping.

***

### 📦 **What’s in the Coil (Product Overview)**

Here’s what you’re getting:

* **Material:** Shape Memory Alloy (Nitinol)
* **Form:** Precision tension spring, trained to contract when heated
* **Actuation Method:** Joule heating (yep — just run current through it)
* **Length:** 50mm
* **Spring ODs:** 5 mm, 10 mm, 20 mm
* **Wire Diameters:** 0.5 mm, 1.0 mm, 2.0 mm
* **Activation Temp:** \~90 °C (like a hot cup of tea, but way more useful)
* **Mounting:** Each spring comes pre-mounted with 5052 aluminum fixtures on both ends — electrically conductive, mechanically overbuilt, and ready to plug into your project

These aren’t passive mechanical springs — they’re active, electrically actuated devices.

***

### 🧪 **Spring Stats (By Size)**

| **Spec**              | **0.5 mm Spring** | **1.0 mm Spring** | **2.0 mm Spring** |
| --------------------- | ----------------- | ----------------- | ----------------- |
| Wire Diameter         | 0.5 mm            | 1.0 mm            | 2.0 mm            |
| Outer Diameter        | 5 mm              | 10 mm             | 20 mm             |
| Max Force (Estimated) | 2–3 N             | 8–10 N            | 25–30 N           |
| Stroke Length (Est.)  | 15–20 mm          | 30–40 mm          | 40–50 mm          |
| Resistance (Ω)        | 0.79 Ω            | 0.41 Ω            | 0.17 Ω            |
| Contraction Current   | 4 A               | 16 A              | 60 A              |
| Actuation Power       | 12 W              | 105 W             | 600 W             |
| Cooling Time (Air)    | 5–15 s            | 20–30 s           | 60 s              |
| Cooling Time (Fan)    | 2–6 s             | 8–15 s            | 20–30 s           |
| Cooling Time (Water)  | 1 s               | 2–3 s             | 5–7 s             |
| Efficiency            | 2–5%              | 2–5%              | 2–5%              |
| Cycle Life (at 3–5%)  | 100,000–1,000,000 | 100,000–1,000,000 | 100,000–1,000,000 |
| Operating Temp Range  | 0 °C – 120 °C     | 0 °C – 120 °C     | 0 °C – 120 °C     |

⚠️ We’re still validating these values, so don't take them at face value. Spot something weird — let us know!

***

### 🔄 **How Long Will It Bounce Back?**

Spring fatigue is real — but manageable. Stay within the strain limits, and these springs can run laps for months:

| **Strain** | **Cycle Life**           |
| ---------- | ------------------------ |
| 2%         | 1,000,000+ cycles        |
| 4%         | 100,000+ cycles          |
| 6%         | 10,000–20,000 cycles     |
| 8%         | 2,000–5,000 cycles       |
| >8%        | 💀 Umm like maybe a few. |

**Pro tip:** Springs tend to settle in. Run a few warmup cycles to stabilize force output.

***

### 🧠 **How to Control It (Like a Spring Whisperer)**

Just like our wire, these springs love the **ThermoFlex™ Node Controller**:

* 60 A output — enough to boss around 2 mm springs
* USB & CAN control for scripting and sync
* Built-in current sensing for over-temp protection
* Works with custom ramp profiles for smooth motion

***

### ❄️ **Cooling It Down (100% Faster Than Watching Paint Dry - we tested it.)**

Like all shape memory alloys, these springs can only cycle as fast as they can cool:

* **Air Cooling:** 5–60 s depending on spring size
* **Fan Cooling:** Much better — think 2× to 5× faster
* **Water Cooling:** Instant noodle fast — 1–7 s depending on size

We’re working on integrated cooling gear. Until then, BYOF (bring your own fan).

***

### 🔧 **Mounting Tips (From People Who've Broken Stuff)**

These aren’t passive springs — they fight back. Mount them accordingly:

**Physical Mounting**

* Comes with pre-installed 5052 aluminum mounts — no additional brackets, no fuss
* Seriously, just bolt it in and go

**Electrical Connection**

* Aluminum mounts are conductive — clamp them or screw them into your terminals
* Soldering is possible but tricky. The large surface area of the aluminum spring mount makes it hard to get the solder to the right temp.

***

### ✅ **Best Practices**

* ✅ Pre-tension the spring slightly for faster response
* ✅ Use mechanical mounting over adhesives
* ✅ Stay under 5% strain for high cycle life
* 🚫 Don’t overheat — target 90 °C, not lava
* 🚫 Don’t cut your spring unless you know what you’re doing (ask us, we'll tell you)

***

Questions? Bugs? Spring puns? [Email ](mailto:kevin@deltaroboticsinc.com)Kevin — his inbox can take it.
