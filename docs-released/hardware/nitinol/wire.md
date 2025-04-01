---
description: >-
  Everything you need to know about Delta Robotics' Nitinol wire—specs,
  performance, control, and best practices for high-performance actuation.
---

# Wire

## 🔧 Nitinol Wire: What It Is, What It Does, and How Not to Break It

At Delta Robotics, we sell wire that moves. Not like electrical current (though yes, that too) — we’re talking **real, physical motion**. Our Nitinol wire contracts when you heat it, and then cools back into shape. It's kind of like a tiny, silent robot muscle.

This page is here to help you understand what our wires can do, how to use them, and how to not ruin them on Day One.

***

### 🧪 What You’re Working With (Product Overview)

Let’s start with the basics. Here’s what’s in the box:

* **Material**: Nickel-Titanium (aka Nitinol — it’s a shape memory alloy)
* **Form**: Straight annealed
* **How It Works**: Joule heating (just run current through it)
* **Lengths**: 1 ft, 5 ft, 10 ft (custom lengths if you ask nicely)
* **Diameters**: 0.5 mm, 1.0 mm, 2.0 mm
* **Activation Temp**: \~90 °C (hot, but not melt-your-desk hot)

> By default, our wires are **trained straight**. Want them to curl, bend, or do something wild?\
> [**Train your Nitinol here →**](https://docs.deltaroboticsinc.com/learn/how-to-train-nitinol)

***

### 📐 NiTi #5: Wire Specs (But Fun)

NiTi #5 is a high-temp Nitinol alloy that kicks into action around 85–95 °C. The data below is a combo of manufacturer specs, lab tests, and a healthy amount of calculator abuse.

> ⚠️ We’re still validating these numbers across labs and field tests.\
> If you’re a Nitinol nerd and spot something weird — let us know!

| **Property**               | **0.5 mm** | **1.0 mm**            | **2.0 mm**             |
| -------------------------- | ---------- | --------------------- | ---------------------- |
| Resistance (Ω/m)           | \~4.3 Ω    | \~1.1 Ω _(estimated)_ | \~0.27 Ω _(estimated)_ |
| Heating Pull Force (g)     | \~3,560 g  | \~14,240 g _(est.)_   | \~56,960 g _(est.)_    |
| Cooling (Bias) Force (g)   | \~1,424 g  | \~5,696 g _(est.)_    | \~22,784 g _(est.)_    |
| Contraction Current (\~1s) | \~4 A      | \~16 A _(est.)_       | \~64 A _(est.)_        |
| Cooling Time (90 °C, air)  | \~14 s     | \~40 s _(est.)_       | \~100 s _(est.)_       |
| Max Recommended Strain     | **5%**     | **5%**                | **5%**                 |

> 🎯 Use **3–4% strain** if you want your wire to last longer than a weekend.

***

### 🔄 How Long Will It Last?

Here’s the short version: less strain = longer life. Push it too far, and it’ll break up with you.

| **Strain** | **Cycle Life**                  |
| ---------- | ------------------------------- |
| 2%         | 1,000,000+ cycles               |
| 4%         | 100,000+ cycles                 |
| 6%         | 10,000–20,000 cycles            |
| 8%         | 2,000–5,000 cycles              |
| >8%        | 💀 Don’t say we didn’t warn you |

***

### 🧠 Control It Like a Pro

#### ThermoFlex™ Node Controller

All of our wires work with our **ThermoFlex™ Node Controller**, built by people who really love robots (and hate magic smoke).

* Pre-made wire profiles (coming soon)
* USB & Serial control (yes, you can script it)
* Built-in current & resistance sensing
* 60 A output — enough to power even 2 mm wire for an under 1-second contraction time

It runs on **Arduino Minima**, talks over **CAN**, and supports up to **200 devices** from one USB cable.\
Also? It helped us shape-set actuators electrically before we got a fancy furnace. Nerd cred confirmed.

[Read the Nitinol Training Guide →](https://docs.deltaroboticsinc.com/learn/how-to-train-nitinol)

***

#### ❄️ Cooling Tips

Want your wire to move faster? Get it cold, quickly.

* **Air Cooling**\
  \~14 s for 0.5 mm\
  \~40 s for 1.0 mm\
  \~100 s for 2.0 mm\
  &#xNAN;_(That’s in still air — use a fan!)_
* **Liquid Cooling**\
  Up to **100× faster**. Yes, really.\
  We’re building a system just for this. Stay tuned.

***

### 🔩 How to Mount It (Without Tears)

Getting the wire connected is an underrated art form. Here's your cheat sheet:

#### Physical Mounting

| Method            | Works For?        | Notes                              |
| ----------------- | ----------------- | ---------------------------------- |
| Screw-down clamps | All sizes         | Best combo of secure + simple      |
| Wrap-around posts | Light duty setups | Just make sure it’s tensioned well |
| Crimps            | Low-force only    | Fatigue risk at higher loads       |

#### Electrical Connection

| Method          | Works For?         | Notes                                             |
| --------------- | ------------------ | ------------------------------------------------- |
| Screw terminals | Most setups        | Best choice. Easy to adjust, high current capable |
| Alligator clips | Prototypes only    | Handy but not reliable for real-world use         |
| Soldering       | ⚠️ Not recommended | Unless you’re a chemist (see below)               |

***

#### 🧪 Experimental: Soldering Nitinol

**Don’t try this at home — seriously.**

Yes, it’s _technically_ possible. But first you have to:

1. Strip the oxide layer using **hydrofluoric acid** (don’t unless you know how to)
2. Electroplate with **nickel**
3. Then maybe — _maybe_ — your solder will stick (still experimental)

> We only do this in the lab, and we’re trained. This isn’t a weekend project.

***

### ✅ Best Practices (a.k.a. How Not to Mess It Up)

* ✅ Use screw terminals or mechanical anchors
* 🚫 Avoid soldering (unless pre-tabbed)
* ⚖️ Pre-tension slightly — but **don’t stretch it**
* 🔁 Stay under **5% strain** if you want it to last

***

### 📚 Sources & References

For the curious, the nerdy, and the skeptical — here are some external referances:

* Fort Wayne Metals\
  [Shape Memory Nitinol](https://www.fwmetals.com/what-we-do/materials/nitinol/shape-memory-nitinol)\
  [NiTi Actuator Wire Datasheet (PDF)](https://www.fwmetals.com/media/pbmke3zt/0-3-mm-acuator-data-sheet.pdf)

> _1.0 mm and 2.0 mm values are extrapolated from 0.5 mm data using basic math, standard assumptions, and coffee._
