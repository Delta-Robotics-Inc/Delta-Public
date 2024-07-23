---
description: Need to know about Nitinol? You're in the right place!
---

# Nitinol FAQ

Here are the [generalized properties](https://en.wikipedia.org/wiki/Nickel\_titanium) of Nitinol alloy:



| Material properties                                                                                            | Value                       |
| -------------------------------------------------------------------------------------------------------------- | --------------------------- |
| [Melting point](https://en.wikipedia.org/wiki/Melting\_point)                                                  | 1,310 °C (2,390 °F)         |
| [Density](https://en.wikipedia.org/wiki/Density)                                                               | 6.45 g/cm3 (0.233 lb/cu in) |
| [Electrical resistivity](https://en.wikipedia.org/wiki/Electrical\_resistivity\_and\_conductivity) (austenite) | 82×10−6 Ω·cm                |
| (martensite)                                                                                                   | 76×10−6 Ω·cm                |
| [Thermal conductivity](https://en.wikipedia.org/wiki/Thermal\_conductivity) (austenite)                        | 0.18 W/cm·K                 |
| (martensite)                                                                                                   | 0.086 W/cm·K                |
| [Coefficient of thermal expansion](https://en.wikipedia.org/wiki/Thermal\_expansion) (austenite)               | 11×10−6/°C                  |
| (martensite)                                                                                                   | 6.6×10−6/°C                 |
| [Magnetic permeability](https://en.wikipedia.org/wiki/Magnetic\_permeability)                                  | < 1.002                     |
| [Magnetic susceptibility](https://en.wikipedia.org/wiki/Magnetic\_susceptibility) (austenite)                  | 3.7×10−6 emu/g              |
| (martensite)                                                                                                   | 2.4×10−6 emu/g              |
| [Elastic modulus](https://en.wikipedia.org/wiki/Elastic\_modulus) (austenite)                                  | 75–83 GPa                   |
| (martensite)                                                                                                   | 28–40 GPa                   |
| [Yield strength](https://en.wikipedia.org/wiki/Yield\_strength) (austenite)                                    | 195–690 MPa                 |
| (martensite)                                                                                                   | 70–140 MPa                  |
| [Poisson's ratio](https://en.wikipedia.org/wiki/Poisson's\_ratio)                                              | 0.33                        |

Shape memory Nitinol has three main phases; Twined Martensite, De-twinned Martensite, and Austenite phases. The Image below shows at what atomic phases the Nitinol is in during heating and cooling cycles. For how this relates to Delta Robotics ThermoFlex actuators:

* During a contraction i.e. shortening of the actuator we are in a De-twinned Martensite phase to Austenite transition (left side of graph)
* During it's cooling cycle where power is off and the muscle is left to dissipate heat it is in a Austenite to Twinned Martensite phase (right side of graph).
* During load where the actuator is under stress and be deformed i.e. being stretch out by a water jug and pulled it is going from Twinned to De-twinned Martensite (bottom of image)

<figure><img src="../.gitbook/assets/NiTi_structure_transformation.jpg" alt="" width="563"><figcaption></figcaption></figure>



NiTiNOL (Nickel-Titanium alloy) exhibits different crystal lattice structures depending on its phase:

<table data-card-size="large" data-view="cards" data-full-width="true"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td>Austenite Phase:</td><td>In the high-temperature phase, NiTiNOL has a B2 cubic structure. This is a body-centered cubic (BCC) lattice where nickel and titanium atoms are positioned at the corners and the center of the unit cell.</td></tr><tr><td>Martensite Phase:</td><td>In the low-temperature phase, NiTiNOL transforms into martensite, which has a more complex structure. The martensite phase can have different forms depending on the specific alloy composition and thermal treatment: Monoclinic B19' Structure: This is the most common form of martensite in NiTiNOL. It has a distorted lattice compared to the austenite phase, allowing for significant deformation and the shape memory effect. Orthorhombic B19 Structure: This form is less common but can also be observed under certain conditions.</td></tr></tbody></table>

<figure><img src="../.gitbook/assets/Nitinol_Austenite_and_martensite.jpg" alt="" width="563"><figcaption><p>Above are images of Nitinols lattice in Austinite and Martensite</p></figcaption></figure>



Due to the Nature of Nitinol is has a hysteretic curve for temperature vs strain/transformation. Below is a image of this curve with Austenite start (As), Austenite finish (Af), Martensite start (Ms), and Martensite finish (Mf) phases listed.

<figure><img src="../.gitbook/assets/Nitinol_transformation_hysterisis.svg" alt=""><figcaption></figcaption></figure>



While the Nitinol we currently use at Delta is a 90 Degree Celsius Activation Temperature Nitinol alloy we can have Nitinol's activation temperature, otherwise known as Martensite start (Ms), change based on the Ratio of Nickel to Titanium. The greater percentage that Nickel takes up in the alloy content the lower the activation temperature is. Below is a graph of this relationship.

<figure><img src="../.gitbook/assets/Nitinol_Ms_vs_Ni_content.jpg" alt="" width="563"><figcaption></figcaption></figure>
