---
description: A modular pneumatic artificial muscle system.
icon: wind
---

# AeroFlex™ (Coming Soon)

<div data-full-width="false"><figure><img src="../.gitbook/assets/Ryzers Glam Shot.JPEG" alt=""><figcaption><p>Lower body exo-skeleton using a prototype AeroFlex™ pneumatic muscle system.</p></figcaption></figure></div>

Pneumatic artificial muscles (PAMs) are not new. Classic McKibben-style muscles have been around for decades; there are plenty of DIY tutorials floating around, and companies like Festo sell polished versions if you can afford them..

So why are we bothering?

We believe the core tech is good, but the ecosystem around it is not. PAMs are strong, light, and inherently safe around humans, yet most people still reach for a servo or stepper long before they consider a muscle.

AeroFlex™ is our attempt to fix that.

We are trying to build a standardized family of braided pneumatic muscles, hardware, and control tools so you can treat a pneumatic muscle like just another part in your toolkit.

This page is the 101: what PAMs are, why they are useful, and how AeroFlex pushes them further.

***

## What is a pneumatic artificial muscle?

At the simplest level, a classic PAM (and our AeroFlex muscles) is:

* A soft inner tube or bladder
* Wrapped in a braided sleeve
* Hooked up to compressed air

When you pump in air, the inner tube wants to expand in diameter. The braid resists that change in length. The result:

* The diameter increases
* The length decreases
* You get a strong pulling force along the axis

Think "Chinese finger trap, but in reverse."

This basic geometry is sometimes called a McKibben muscle. We are not reinventing that concept. We are standardizing, instrumenting, and packaging it so it is actually practical.

***

## Why PAMs are interesting

### High power-to-weight

For their size and mass, braided pneumatic muscles can pull hard and move fast.

* Lots of force in a compact package
* Great for joints, linkages, and mechanisms where motors and gearboxes can't fit.

If your alternative involves bolting something the size of a car alternator to your robot, PAMs start looking pretty good.

### Inherently compliant

PAMs are soft and squishy by default.

* Safer interaction with humans
* Less damage during collisions
* Fewer shattered gear trains when something hits a hard stop

You get mechanical compliance built into the actuator, instead of trying to fake it with springs, flexures, or control loops.

#### Silent(ish) actuation

Most of the noise in a PAM system comes from the compressor, not the muscle itself.

* Compressors can be loud, but you can park them off-board, put them in another room, or bury them in an enclosure so the noisy part is physically separated from the robot or wearable
* A buffer tank lets you run short bursts of motion with the compressor off, which makes things much quieter in practice
* With good valve selection, reasonable pressures, and a sane plumbing layout, airflow and valve noise stay much lower than a typical motor+gearbox setup

"Robot moves without sounding like a blender" is underrated.

### Simple mechanical construction

You do not need a full machine shop to build a basic PAM:

* Soft tubing or a custom bladder
* Braided sleeve (PET, Nylon, etc.)
* End fittings

This makes them friendly to labs, classrooms, and garage projects.

### Great for "body scale" motion

PAMs shine in applications that look more like biomechanics than CNC machines:

* Exoskeleton joints
* Animatronic limbs and faces
* Soft grippers and tentacles
* Tails, spines, and other creature mechanics
* Assistive and wearable devices

If you want movement that feels more like muscle than motor, PAMs belong on your list.

### Decoupled power source

The heavy stuff can live somewhere else:

* Compressor
* Tanks
* Regulators
* Filtration

You can park those off-board or in a backpack, then run light, flexible air lines to the muscles themselves. That is a big deal for wearables, mobile robots, and animatronics where mass at the joint is painful.

***

## What is wrong with PAMs today?

If PAMs are so great, why is everything still running on motors?

Some pain points in the current ecosystem:

* No standard parts: Everyone ends up having to make their own.
* Awkward contraction ratios: Many DIY builds get mediocre stroke per length.
* Bulky pneumatics: Valves, regulators, and sensors are often sized for industrial pneumatics, not wearables.
* Cost and availability: Good commercial muscles are expensive and not stocked like standard actuators. DIY approaches are cheap but don't have the performance
* Poor integration story: Mounting hardware is improvised. Sensing and control are ad hoc. Every project feels like a custom job.

AeroFlex exists to attack these problems directly.

***

## Enter AeroFlex

AeroFlex is our family of braided pneumatic muscles and supporting hardware that we are standardizing at Delta Robotics.

The core idea:

> Take proven McKibben-style tech, and make it cheap, repeatable, and usable in real projects.

<figure><img src="../.gitbook/assets/IMG_3342.JPEG" alt=""><figcaption><p>Early AeroFlex™ Prototypes</p></figcaption></figure>

### Our design goals

1. Known, repeatable geometry
   * Defined braid angle, inner and outer diameters, nominal lengths, or make custom&#x20;
   * Predictable contraction ratios with a target around 50 percent stroke
   * Tunable variants for force vs stroke tradeoffs
2. Known pressure and force ranges
   * Documented operating and maximum pressures
   * Force curves vs pressure and displacement
   * Characterization data you can drop into a simulator or controller
3. Integrated sensing
   * Pressure sensing at or near the muscle
   * Force sensing via in-line load cells or end-effector measurement
   * Length / contraction sensing via encoders, linear sensors, or indirect models

In other words: we want you to be able to do more than "add air until it feels right."

4. Portable pneumatics
   * Smaller, more efficient valves sized correctly for AeroFlex muscles
   * Compact regulators and manifolds that make sense on a wearable or small robot
   * Path toward backpack or on-board pneumatic modules, not just benchtop rigs
5. Real integration hardware
   * Standard end fittings and mounting patterns
   * Brackets, clevises, and link hardware that can be reused across projects
   * Thoughtful routing and strain relief for air lines and sensor cables

***

## What we are actively researching and improving

### Better contraction ratio

Target: roughly 50 percent contraction, within sane pressures and lifetimes.

We are exploring:

* Low-angle, high-aspect-ratio braids
* Different combinations of inner tube and sleeve stiffness
* Multi-filament bundles where several smaller muscles are grouped to act like a single unit

The goal is to get more stroke per unit length so you do not have to build absurd linkages just to move a joint.

<div align="center" data-full-width="false"><figure><img src="../.gitbook/assets/Muscle Test.gif" alt=""><figcaption><p>Testing Multi-Filiment Designs</p></figcaption></figure></div>

### Smaller, more efficient pneumatics

We want AeroFlex setups that are:

* Wearable, not cart-mounted
* Optimized for the flow and pressure ranges that AeroFlex actually uses

That means:

* Valve selection and characterization specifically for AeroFlex muscles
* Experiments with compact compressors, tanks, and regulators
* Layouts that can realistically live in a backpack, torso shell, or robot base

### Integrated sensing and control

To control AeroFlex muscles like real actuators instead of "vibes and PSI," we are:

* Embedding or closely coupling pressure sensors to each muscle or muscle group
* Benchmarking force output across pressure and strain
* Experimenting with length estimation through sensors and modeling

On the control side:

* Modeling muscle behavior for feedforward control
* Exploring closed-loop pressure control, force control, and position control
* Firmware and software that make AeroFlex act like a clean API, not a tangle of hoses

### Materials, durability, and repeatability

We are testing:

* Different inner tube materials and wall thicknesses
* Various braided sleeves (PET, aramid, etc.) and weave patterns
* End-fitting designs that survive repeated cycling, bending, and abuse

The goal is to publish not just "it works once," but:

* Cycle life expectations
* Failure modes
* Reasonable derating guidelines

### Standardization and documentation

AeroFlex is not just a pile of parts. We are building:

* A small number of standard muscle sizes with documented performance
* Reference designs for exoskeleton joints, animatronics, and robotic limbs
* Integration guides and CAD for mounts, brackets, and manifolds

If you want a "just works" path, there will be off-the-shelf options. If you want to tweak and customize, there will be recipes.

***

## Where AeroFlex is headed

In the AeroFlex family and related docs, you will see us working toward:

* A catalog of standard AeroFlex muscles with known specs
* Control stacks that integrate muscles, valves, and sensors cleanly
* Example applications: exoskeleton joints, robot arms, animatronics, and prosthetic components
* Both pre-made muscles and DIY-friendly kits

Our endgame is simple:

> Make it as normal to drop a pneumatic muscle into your project as it is to drop in a servo.

***

## Who this is for

AeroFlex is for you if:

* You have built or tried McKibben muscles and want something more predictable
* You have looked at Festo muscles and decided your budget would rather not
* You wanted to try PAMs but got scared off by compressors, fittings, and random forum posts

If you have experience, horror stories, or hard-earned lessons with pneumatic muscles, we want those. If you are new and full of "dumb" questions, those are welcome too.

We are all collectively arguing with air pressure here.

