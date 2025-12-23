---
description: >-
  An in-development hydraulic artificial muscle system targeting high-pressure
  operation
icon: droplet
---

# HydraFlex™ (In Development)

{% hint style="info" %}
**Prototype caveat (alpha):** This documentation reflects the current R\&D state. Hardware, materials, and test procedures will evolve quickly. Expect sharp corners. File feedback early and often.\
\
**Availability:** HydraFlex is not shipping and is not for general purchase or integration yet. This page is a development snapshot, not a datasheet.
{% endhint %}

***

### What is a hydraulic artificial muscle?

A classic McKibben-style artificial muscle is:

* A flexible inner bladder
* Wrapped in a braided sleeve
* Terminated with end fittings
* Pressurized to generate an axial pulling force

For HydraFlex, the pressure medium is **hydraulic fluid** instead of air.

That means:

* Higher stiffness (less compressibility)
* Higher force potential for a given diameter
* More plumbing discipline

***

### Why hydraulics are interesting

#### Higher force density

Hydraulics let you run at much higher pressures than typical pneumatic setups, which can translate to higher force in the same form factor.

#### Better controllability (sometimes)

Lower compressibility can make pressure control feel less like herding cats.

#### Portable power, still decoupled

Like pneumatics, you can keep the heavy parts off-joint:

* Pump
* Reservoir
* Accumulator (optional)
* Valves and filtration

Then route lightweight hoses to the muscles.

***

### HydraFlex vs AeroFlex

HydraFlex and AeroFlex muscles are mechanically very similar.

What stays the same:

* Bladder + braid + end fittings architecture
* Contraction physics (geometry-driven)
* Mounting patterns and modular “muscle as a part” philosophy

What changes:

* Operating pressure target is **much higher**
* Material requirements get brutal (bladder + braid + termination)
* The “system” shifts from compressor/regulator to **pump/reservoir/valves**

If you have not read the AeroFlex overview yet, start there.

{% content-ref url="aeroflex-tm-in-development.md" %}
[aeroflex-tm-in-development.md](aeroflex-tm-in-development.md)
{% endcontent-ref %}

***

### Design targets (R\&D)

These are targets for the R\&D program, not promises. If you are looking for guaranteed specs, HydraFlex is not ready to date.

| Parameter          | Target                       | Why it exists                 |
| ------------------ | ---------------------------- | ----------------------------- |
| Operating pressure | **500 psi** (≈ 3.45 MPa)     | High force in compact form    |
| System footprint   | Compact pump + plumbing      | On-board or wearable-friendly |
| Muscle form factor | Modular sizes                | Repeatable, swappable builds  |
| Characterization   | Force/pressure/length curves | Control loops need data       |
| Failure behavior   | Predictable + documented     | No mystery bursts             |

{% hint style="info" %}
500 psi is not “industrial hydraulics.” It is still more than enough to ruin your afternoon.
{% endhint %}

***

### What we are building (behind the curtain)

HydraFlex is not just a muscle. It is a muscle **ecosystem**.

Right now this looks like bench rigs, off-the-shelf plumbing, and a lot of material coupons that live short, exciting lives.

#### 1) High-pressure braided muscles

Core R\&D focus:

* Bladder material that survives pressure, flexing, and cycling
* Braided sleeving that holds geometry without shredding the bladder
* End fittings that do not turn into weak links

#### 2) A compact hydraulic pump pack

We are starting with off-the-shelf components:

* Pumps
* Fittings
* Hoses
* Valves

Then we shrink and standardize once the requirements are real.

#### 3) A sane integration story

The endgame is modular building blocks:

* Standard muscle sizes
* Standard fluid interfaces
* Mounting hardware that is not “whatever was in the drawer”

***

### What we are actively researching and improving

#### Muscle materials at 500 psi

The muscle is the hard part.

We are testing combinations of:

* Bladder materials and wall thicknesses
* Braids (Carbon Fiber vs aramid-class fibers, different picks and weaves)
* Termination methods (clamps, ferrules, overmolds, hybrid approaches)

#### End fittings and terminations

A high-pressure muscle fails at the interface first.

We care about:

* Leak rate under static pressure
* Leak rate under bending and cycling
* Repeatable assembly without “artisan torque”

#### Small, tight hydraulics

A compact pump system needs:

* Pressure relief (mandatory)
* Filtration and fluid cleanliness
* A layout that is serviceable

#### Sensing and control

HydraFlex wants to behave like a real actuator, not “adjust pressure until it looks right.”

Planned focus areas:

* Pressure sensing close to the muscle
* Force sensing in-line or at the joint
* Control modes: pressure, force, and position

***

### Where HydraFlex is headed

You will see this section grow as we move from lab prototypes to something you can actually build with.

Our roadmap is roughly:

1. Prove a repeatable 500 psi muscle build
2. Publish force/pressure/length characterization
3. Package a compact pump/valve module
4. Release reference designs (joints, limbs, and wearables)

***

### Who this is for (today)

HydraFlex is for you if:

* You want high force density without rigid gear trains
* You are building at “body scale” (wearables, limbs, animatronics)
* You have the lab discipline to work with pressurized fluid
* You are collaborating with us on R\&D (or you are intentionally reading ahead)

If your plan involves zip ties as primary safety hardware, start with AeroFlex.

***

### Further reading

Hydraulic McKibben muscles have a deep research history. Here are some solid starting points:

* [Very High Force Hydraulic McKibben Artificial Muscle with a p-Phenylene-2,6-benzobisoxazole (PBO) Cord Sleeve (Advanced Robotics, 2010)](https://doi.org/10.1163/016918609X12586209967366)
* [Development of Power Robot Hand with Shape Adaptability Using Hydraulic McKibben Muscles (IEEE ICRA, 2010)](https://doi.org/10.1109/ROBOT.2010.5509489)
* [Development of Contraction and Extension Artificial Muscles with Different Braid Angles (Journal of Robotics and Mechatronics, 2011)](https://doi.org/10.20965/jrm.2011.p0582)
* [A Proposal of a New Rotational-Compliant Joint with Oil-Hydraulic McKibben Artificial Muscles (Advanced Robotics, 2018)](https://doi.org/10.1080/01691864.2018.1464946)
* [Trends in Hydraulic Actuators and Components in Legged and Tough Robots: A Review (Advanced Robotics, 2018)](https://doi.org/10.1080/01691864.2018.1455606)
* [Safety-Enhanced Control Strategy of a Power Soft Robot Driven by Hydraulic Artificial Muscles (ROBOMECH Journal, 2021, Open Access)](https://doi.org/10.1186/s40648-021-00194-5)
* [Experimental Comparison of Antagonistic Hydraulic Muscle Actuation (Mechatronics, 2022)](https://doi.org/10.1016/j.mechatronics.2022.102737)
* [Experimental Validation of a 7-DOF Power Soft Robot Driven by Hydraulic Artificial Muscles (IEEE RA-L, 2024)](https://doi.org/10.1109/LRA.2024.3394219)
