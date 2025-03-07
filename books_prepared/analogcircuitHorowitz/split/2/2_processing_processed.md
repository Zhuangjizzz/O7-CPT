# CHAPTER2 Bipolar Transistors

## 2.1 Introduction

The transistor is our most important example of an "active" component, a device that can amplify, producing an output signal with more power in it than the input signal. The additional power comes from an external source of power (the power supply, to be exact). Note that voltage amplification isn't what matters, since, for example, a step-up transformer, a "passive" component just like a resistor or capacitor, has voltage gain but no power gain. ${ }^{1}$ Devices with power gain are distinguishable by their ability to make oscillators, by feeding some output signal back into the input.

It is interesting to note that the property of power amplification seemed very important to the inventors of the transistor. Almost the first thing they did to convince themselves that they had really invented something was to power a loudspeaker from a transistor, observing that the output signal sounded louder than the input signal.

The transistor is the essential ingredient of every electronic circuit, from the simplest amplifier or oscillator to the most elaborate digital computer. Integrated circuits (ICs), which have largely replaced circuits constructed from discrete transistors, are themselves merely arrays of transistors and other components built from a single chip of semiconductor material.

A good understanding of transistors is very important, even if most of your circuits are made from ICs, because you need to understand the input and output properties of the IC in order to connect it to the rest of your circuit and to the outside world. In addition, the transistor is the single most powerful resource for interfacing, whether between ICs and other circuitry or between one subcircuit and another. Finally, there are frequent (some might say too frequent) situations in which the right IC just doesn't exist, and you have to rely on discrete transistor circuitry to do the job. As you will see, transistors have an excitement all their own. Learning how they work can be great fun.

[^47]There are two major species of transistors: in this chapter we will learn about bipolar junction transistors (BJTs), which historically came first with their Nobel Prize-winning invention in 1947 at Bell Laboratories. The next chapter deals with "field-effect" transistors (FETs), the now-dominant species in digital electronics. To give the coarsest comparison, BJTs excel in accuracy and low noise, whereas FETs excel in low power, high impedance, and high-current switching; there is, of course, much more to this complex subject.

Our treatment of bipolar transistors is going to be quite different from that of many other books. It is common practice to use the $h$-parameter model and equivalent circuit. In our opinion that is unnecessarily complicated and unintuitive. Not only does circuit behavior tend to be revealed to you as something that drops out of elaborate equations, rather than deriving from a clear understanding in your own mind as to how the circuit functions; you also have the tendency to lose sight of which parameters of transistor behavior you can count on and, more important, which ones can vary over large ranges.

In this chapter we will instead build up a very simple introductory transistor model and immediately work out some circuits with it. Its limitations will soon become apparent; then we will expand the model to include the respected Ebers-Moll conventions. With the EbersMoll equations and a simple three-terminal model, you will have a good understanding of transistors; you won't need to do a lot of calculations, and your designs will be first rate. In particular, they will be largely independent of the poorly controlled transistor parameters such as current gain.

Some important engineering notation should be mentioned. Voltage at a transistor terminal (relative to ground) is indicated by a single subscript (C, B, or E): $V_{\mathrm{C}}$ is the collector voltage, for instance. Voltage between two terminals is indicated by a double subscript: $V_{\mathrm{BE}}$ is the base-toemitter voltage drop, for instance. If the same letter is repeated, that means a power-supply voltage: $V_{\mathrm{CC}}$ is the (positive) power-supply voltage associated with the collector,
and $V_{\mathrm{EE}}$ is the (negative) supply voltage associated with the emitter. ${ }^{2}$

#### Why transistor circuits are difficult

For those learning electronics for the first time, this chapter will be difficult. Here's why: all the circuits in the last chapter dealt with two-terminal devices, whether linear (resistors, capacitors, inductors) or nonlinear (diodes). So there was only one voltage (the voltage between the terminals) and only one current (the current flowing through the device) to think about. Transistors, by contrast, are threeterminal devices, which means there are two voltages and two currents to juggle. ${ }^{3}$

### 2.1.1 First transistor model: current amplifier

Let's begin. A bipolar transistor is a three-terminal device (Figure 2.1), in which a small current applied to the base controls a much larger current flowing between the collector and emitter. It is available in two flavors ( $n p n$ and pnp), with properties that meet the following rules for $n p n$ transistors (for pnp simply reverse all polarities):

1. Polarity The collector must be more positive than the emitter.
2. Junctions The base-emitter and base-collector circuits behave like diodes (Figure 2.2) in which a small current applied to the base controls a much larger current flowing between the collector and emitter. Normally the base-emitter diode is conducting, whereas the basecollector diode is reverse-biased, i.e., the applied voltage is in the opposite direction to easy current flow.
3. Maximum ratings Any given transistor has maximum values of $I_{\mathrm{C}}, I_{\mathrm{B}}$, and $V_{\mathrm{CE}}$ that cannot be exceeded without costing the exceeder the price of a new transistor (for typical values, see the listing in Table 2.1 on page 74 , Table 2.2 on page 106, and Table 8.1 on pages 501-502 There are also other limits, such as power dissipation ( $I_{\mathrm{C}} V_{\mathrm{CE}}$ ), temperature, and $V_{\mathrm{BE}}$, that you must keep in mind.
4. Current amplifier When rules $1-3$ are obeyed, $I_{C}$ is roughly proportional to $I_{B}$ and can be written as

$$
\begin{equation*}
I_{\mathrm{C}}=h_{\mathrm{FE}} I_{\mathrm{B}}=\beta I_{\mathrm{B}}, \tag{2.1}
\end{equation*}
$$

${ }^{2}$ In practice, circuit designers use $V_{\mathrm{CC}}$ to designate the positive supply and $V_{\mathrm{EE}}$ the negative supply, even though logically they should be interchanged for pnp transistors (where all polarities are reversed).
${ }^{3}$ You might think that there would be three voltages and three currents; but it's slightly less complicated than that, because there are only two independent voltages and two independent currents, thanks to Kirchhoff's voltage and current laws.
where $\beta$, the current gain (sometimes called ${ }^{4} h_{\mathrm{FE}}$ ), is typically about 100 . Both $I_{\mathrm{B}}$ and $I_{\mathrm{C}}$ flow to the emitter. Note: the collector current is not due to forward conduction of the base-collector diode; that diode is reversebiased. Just think of it as "transistor action."
image_name:Figure 2.1
description:The image labeled "Figure 2.1" depicts various transistor symbols and small transistor package drawings. It includes both schematic symbols and physical package representations for transistors.

1. **Identification of Components and Structure:**
- **Schematic Symbols:**
- The image shows two transistor symbols: an NPN transistor and a PNP transistor. The NPN transistor symbol is highlighted with a red rectangle, indicating the direction of current flow with an arrow pointing out from the emitter. The PNP transistor symbol is highlighted with a blue rectangle, with an arrow pointing into the emitter.
- **Transistor Packages:**
- Several common transistor packages are illustrated, including TO-5, TO-18, TO-92, TO-220, and SOT-23. Each package is shown with its pins labeled, indicating the collector (C), base (B), and emitter (E).

2. **Connections and Interactions:**
- The schematic symbols indicate how the base, collector, and emitter are connected within the transistor. In the NPN symbol, the base is the control terminal, and a small current into the base allows a larger current to flow from collector to emitter. The opposite is true for the PNP symbol, where a small current out of the base controls the larger current from emitter to collector.

3. **Labels, Annotations, and Key Features:**
- The labels "collector," "base," and "emitter" are clearly marked on the schematic symbols.
- The transistor package drawings are annotated with the pin designations (E, B, C) for each package type, providing guidance on how the physical components correspond to the schematic symbols.
- The package types (TO-5, TO-18, TO-92, TO-220, SOT-23) are labeled below each drawing, indicating the form factor and pin configuration for each type of transistor package.

Figure 2.1. Transistor symbols and small transistor package drawings (not to scale). A selection of common transistor packages are shown in Figure 2.3.

image_name:npn
description:
[
name: Q1, type: NPN, ports: {C: C, B: B, E: E}
]
extrainfo:The diagram illustrates the basic operation of NPN and PNP transistors, showing the direction of current flow. In the NPN transistor, a small base current (IB) controls a larger collector current (IC).
image_name:pnp
description:
[
name: pnp, type: PNP, ports: {C: C, B: B, E: E}
]
extrainfo:The diagram shows the current flow directions for both base current (IB) and collector current (IC) for a PNP transistor. The base current flows out of the base, and the collector current flows into the collector.

Figure 2.2. An ohmmeter's view of a transistor's terminals.

Rule 4 gives the transistor its usefulness: a small current flowing into the base controls a much larger current flowing into the collector.

An important warning: the current gain $\beta$ is not a "good" transistor parameter; for instance, its value can vary from 50 to 250 for different specimens of a given transistor type. It also depends on the collector current, collector-toemitter voltage, and temperature. A circuit that depends on a particular value for beta is a bad circuit.

Note particularly the effect of rule 2 . This means you can't go sticking an arbitrary voltage across the baseemitter terminals, because an enormous current will flow if the base is more positive than the emitter by more than about 0.6 to 0.8 V (forward diode drop). This rule also implies that an operating transistor has $V_{\mathrm{B}} \approx V_{\mathrm{E}}+0.6 \mathrm{~V}$ $\left(V_{\mathrm{B}}=V_{\mathrm{E}}+V_{\mathrm{BE}}\right)$. Again, polarities are normally given for $n p n$ transistors; reverse them for $p n p$.

Let us emphasize again that you should not try to think of the collector current as diode conduction. It isn't,

[^48]image_name:Figure 2.3
description:The image displays a collection of various electronic component packages, commonly used in electronic circuits. These components are organized in three rows based on their mounting style and size.

1. **Top Row (Power Packages):**
- **TO-220 (with and without heatsink):** These are three-pin power transistors, often used in power regulation and amplification. The heatsink version has an additional metal flange for heat dissipation.
- **TO-39 and TO-5:** These are metal-can packages with three leads, used for transistors and some ICs, providing good thermal conductivity.
- **TO-3:** A larger metal-can package with two mounting holes and multiple leads, typically used for high-power transistors.

2. **Middle Row (Surface Mount Packages):**
- **SM-8 (dual) and SO-8 (dual):** Small outline integrated circuits with multiple pins, used in compact circuit designs.
- **SOT-23 and SOT-223:** Small outline transistors, used for surface mounting on PCBs.
- **Ceramic SOE:** A ceramic package, providing better thermal and electrical insulation.

3. **Bottom Row (Various Packages):**
- **DIP-16 (quad) and DIP-4:** Dual in-line packages with multiple pins, used for ICs and other components.
- **TO-92 and TO-18:** Small plastic and metal packages for transistors, with three leads.
- **TO-18 (dual):** A variant with additional leads for dual transistor configurations.

**Connections and Interactions:**
- The components are not physically connected in the image, as they are shown as individual units. However, in practical applications, these components would be soldered onto a PCB or connected via wiring to form circuits.

**Labels, Annotations, and Key Features:**
- Each component is labeled with its package type, such as TO-220, TO-92, etc., which helps identify the component's application and compatibility with circuit designs.
- The image includes a scale reference (1 cm) for size comparison, which is crucial for understanding the physical dimensions of these components.

Figure 2.3. Most of the common packages are shown here, for which we give the traditional designations. Top row (power), left to right: TO-220 (with and without heatsink), TO-39, TO-5, TO-3. Middle row (surface mount): SM-8 (dual), SO-8 (dual), SOT-23, ceramic SOE, SOT-223. Bottom row: DIP-16 (quad), DIP-4, TO-92, TO-18, TO-18 (dual).
because the collector-base diode normally has voltages applied across it in the reverse direction. Furthermore, collector current varies very little with collector voltage (it behaves like a not-too-great current source), unlike forward diode conduction, in which the current rises very rapidly with applied voltage.

Table 2.1 on the following page includes a selection of commonly used bipolar transistors, with the corresponding curves of current gain ${ }^{5}$ in Figure 2.4, and a selection of transistors intended for power applications is listed in Table 2.2 on page 106. A more complete listing can be found in Table 8.1 on pages 501-502 and Figure 8.39 in Chapter 8.

## 2.2 Some basic transistor circuits

### 2.2.1 Transistor switch

Look at the circuit in Figure 2.5. This application, in which a small control current enables a much larger current to

[^49]flow in another circuit, is called a transistor switch. From the preceding rules it is easy to understand. When the mechanical switch is open, there is no base current. So, from rule 4, there is no collector current. The lamp is off.

When the switch is closed, the base rises to 0.6 V (baseemitter diode is in forward conduction). The drop across the base resistor is 9.4 V , so the base current is 9.4 mA . Blind application of Rule 4 gives $I_{C}=940 \mathrm{~mA}$ (for a typical beta of 100). That is wrong. Why? Because rule 4 holds only if Rule 1 is obeyed: at a collector current of 100 mA the lamp has 10 V across it. To get a higher current you would have to pull the collector below ground. A transistor can't do this, and the result is what's called saturation the collector goes as close to ground as it can (typical saturation voltages are about $0.05-0.2 \mathrm{~V}$, see Chapter $2 x$.) and stays there. In this case, the lamp goes on, with its rated 10 V across it.

Overdriving the base (we used 9.4 mA when 1.0 mA would have barely sufficed) makes the circuit conservative; in this particular case it is a good idea, since a lamp draws more current when cold (the resistance of a lamp when cold is 5 to 10 times lower than its resistance at operating current). Also, transistor beta drops at low collector-to-base voltages, so some extra base current is necessary to bring

Table 2.1 Representative Bipolar Transistors
Part \#

| npn |  | pnp |  | $\begin{gathered} V_{\mathrm{CEO}} \\ (\mathrm{~V}) \end{gathered}$ | $\begin{gathered} I_{C}(\max ) \\ (\mathrm{mA}) \end{gathered}$ | $\begin{gathered} h_{\mathrm{FE}} @ \mathrm{~mA} \\ \text { (typ) } \end{gathered}$ |  | gain curve ${ }^{d}$ | $\begin{aligned} & \mathrm{C}_{\mathrm{cb}}^{\mathrm{a}} \\ & (\mathrm{pF}) \end{aligned}$ | $\begin{gathered} f_{\mathrm{T}}^{\mathrm{a}} \\ (\mathrm{MHz}) \\ \hline \end{gathered}$ | Comments |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| TO-92 | SOT-23 | TO-92 | SOT-23 |  |  |  |  |  |  |  |  |
| 2N3904 | MMBT3904 | 2N3906 | MMBT3906 | 40 | 150 | 200 | 10 | 6 | 2.5 | 300 | jellybean |
| 2N4401 | MMBT4401 | 2N4403 | MMBT4403 | 40 | 500 | 150 | 150 | 7 | 7 | 300 | '2222 and '2907 dies |
| BC337 | BC817 | BC327 | BC807 | 45 | 750 | 350 | 40 | 5 | 10 | 150 | jellybean |
| 2N5089 | MMBT5089 | 2N5087 | MMBT5087 | 25 | 50 | 500 | 1 | 3 | 1.8 | 350 | high beta |
| BC547C | BC847C | BC557C | BC857C | 45 | 100 | 500 | 10 | 4 | 5 | 150 | jellybean ${ }^{\text {b }}$ |
| MPSA14 | MMBTA14 | MPSA64 | MMBTA64 | 30 | 300 | 10000 | 50 | - | 7 | 125 | Darlington |
| ZTX618 | FMMT618 | ZTX718 | FMMT718 | 20 | 2500 | 320 | $3 A$ | 3a | - | 120 | high $/ \mathrm{c}$, small pkg |
| PN2369 | MMBT2369 | 2N5771 | MMBT5771 | 15 | 150 | 100 | 10 | 10 | 3 | 500 | fast switch, gold doped |
| 2N5551 | MMBT5551 | 2N5401 | MMBT5401 | 150 | 100 | 100 | 10 | 5a | 2.5 | 100 | SOT-223 available |
| MPSA42 | MMBTA42 | MPSA92 | MMBTA92 | 300 | 30 | 75 | 10 | 9 | 1.5 | 50 | HV small signal |
| MPS5179 | BFS17 | MPSH81 | MMBTH81 | 15 | 25 | 90 | 20 | 8 | 0.9 | 900 | RF amplifier |
| - | BFR93 ${ }^{C}$ | - | BFT93 ${ }^{\text {C }}$ | 12 | 50 | 50 | 15 | 10 | 0.5 | 4000 | RF amp |
| TIP142 | - | TIP147 | - | 100 | 10A | >1000 | 5A | - | high | low | TO-220, Darlington |

Notes: (a) see Chapter $2 x$ for graphs of $C_{\mathrm{cb}}$ and $f_{\mathrm{T}}$. (b) lower beta versions have an -A or -B suffix; low-noise versions are BC850 (npn) and BC860 (pnp). (c) also BFR25A and BFT25A. (d) see Figure 2.4.
image_name:Figure 2.4
description:Figure 2.4 presents a set of curves depicting the typical DC current gain, denoted as \( h_{FE} \), for various transistors. The graph is a semi-logarithmic plot, where the x-axis represents the Collector Current, \( I_C \), measured in Amperes (A), and spans from 10 microamperes (\( 10\mu A \)) to 1 ampere (A). The y-axis represents the DC Current Gain, \( h_{FE} \), which is dimensionless, and ranges from 20 to 1000.

Each curve on the graph corresponds to a different transistor type, with labels indicating the specific transistor model such as 2N5962, LM394, BC547, among others. The curves show how the current gain varies with the collector current for each transistor model.

The general trend observed is that each transistor exhibits a peak in current gain at a certain collector current level, after which the gain decreases. For instance, the 2N5962 shows a peak gain at lower collector currents compared to others like the ZTX618, which peaks at higher currents. The curves indicate that different transistors are optimized for different ranges of collector current.

Key features of the graph include the presence of various maxima, where each curve achieves its highest \( h_{FE} \) value. These peaks are critical for understanding the optimal operating conditions for each transistor type. The graph provides a visual representation of how production spreads might affect the typical values, with potential variations of +100% to -50% from these curves.

Overall, this graph is a useful tool for comparing the performance of different transistors in terms of their current gain across a range of collector currents, helping in selecting the appropriate transistor for specific applications.

Figure 2.4. Curves of typical transistor current gain, $\beta$, for a selection of transistors from Table 2.1. These curves are taken from manufacturers' literature. You can expect production spreads of $+100 \%,-50 \%$ from the "typical" values graphed. See also Figure 8.39 for measured beta plots for 44 types of "low-noise" transistors.
a transistor into full saturation. Incidentally, in a real circuit you would probably put a resistor from base to ground (perhaps 10k in this case) to make sure the base is at ground with the switch open. It wouldn't affect the ON operation, because it would sink only 0.06 mA from the base circuit.
image_name:Figure 2.5
description:
[
name: SW1, type: Switch, ports: {N1: VDD, N2: X2}
name: RS, type: Resistor, value: 1.0k, ports: {N1: X1, N2: X2}
name: Q1, type: NPN, ports: {C: C1, B: X1, E: GND}
name: Lamp, type: Other, ports: {N1: VDD, N2: C1}
]
extrainfo:The circuit is a simple transistor switch circuit. The mechanical switch controls the base current of the NPN transistor Q1, turning on the 10V, 0.1A lamp when closed.

Figure 2.5. Transistor switch example.

There are certain cautions to be observed when designing transistor switches:

1. Choose the base resistor conservatively to get plenty of excess base current, especially when driving lamps, because of the reduced beta at low $V_{\mathrm{CE}}$. This is also a good idea for high-speed switching, because of capacitive effects and reduced beta at very high frequencies (many megahertz). ${ }^{6}$
2. If the load swings below ground for some reason (e.g., it is driven from ac, or it is inductive), use a diode in series with the collector (or a diode in the reverse direction to ground) to prevent collector-base conduction on negative swings.
3. For inductive loads, protect the transistor with a diode

[^50]across the load, as shown in Figure 2.6. ${ }^{7}$ Without the diode the inductor will swing the collector to a large positive voltage when the switch is opened, most likely exceeding the collector-emitter breakdown voltage, as the inductor tries to maintain its "on" current from $V_{\mathrm{CC}}$ to the collector (see the discussion of inductors in $\S 1.6 .7$ ).
image_name:Figure 2.6
description:
[
name: D1, type: Diode, ports: {Na: c1a1, Nc: VCC}
name: L1, type: Inductor, value: L1, ports: {N1: c1a1, N2: VCC}
name: Q1, type: NPN, ports: {C: c1a1, B: Vin, E: GND}
]
extrainfo:The circuit is a basic transistor switch with an NPN transistor (Q1) controlling an inductive load (L1). A diode (D1) is used for inductive kickback protection across the inductor. The base of the transistor is driven by an input signal (Vin), and the emitter is connected to ground. The collector is connected to the inductor, which is connected to VCC through the diode.

Figure 2.6. Always use a suppression diode when switching an inductive load.

You might ask why we are bothering with a transistor, and all its complexity, when we could just use that mechanical switch alone to control the lamp or other load. There are several good reasons: (a) a transistor switch can be driven electrically from some other circuit, for example a computer output bit; (b) transistor switches enable you to switch very rapidly, typically in a small fraction of a microsecond; (c) you can switch many different circuits with a single control signal; (d) mechanical switches suffer from wear, and their contacts "bounce" when the switch is activated, often making and breaking the circuit a few dozen times in the first few milliseconds after activation; and (e) with transistor switches you can take advantage of remote cold switching, in which only dc control voltages snake around through cables to reach front-panel switches, rather than the electronically inferior approach of having the signals themselves traveling through cables and switches (if you run lots of signals through cables, you're likely to get capacitive pickup as well as some signal degradation).

#### A. "Transistor man"

The cartoon in Figure 2.7 may help you understand some limits of transistor behavior. The little man's perpetual task in life is to try to keep $I_{\mathrm{C}}=\beta I_{B}$; however, he is only allowed to turn the knob on the variable resistor. Thus he can go from a short circuit (saturation) to an open circuit (transistor in the OFF state), or anything in between, but he isn't allowed to use batteries, current sources, etc.

[^51]image_name:Figure 2.7
description:The image titled "Figure 2.7" is a conceptual cartoon depicting a person, referred to as the "Transistor man," standing inside a circle that represents a transistor. This illustration is designed to explain the behavior and limitations of a transistor in a simplified and relatable manner.

1. Identification of Components and Structure:
- **Transistor Man:** The central figure is a cartoon man who is tasked with maintaining a specific relationship between two currents, $I_C$ (collector current) and $I_B$ (base current).
- **Variable Resistor:** The man is shown adjusting a knob connected to a variable resistor. This represents his ability to control the resistance and thus influence the current flow.
- **Meters:** There are two meters depicted, one connected to the base (B) and the other to the collector (C). These meters visually indicate the current levels at these points.
- **Diode Symbol:** A diode symbol is shown at the base (B) connection, indicating the direction of current flow.

2. Connections and Interactions:
- **Base (B) to Emitter (E):** The base current ($I_B$) enters through the base terminal, monitored by a meter.
- **Collector (C) to Emitter (E):** The collector current ($I_C$) exits through the collector terminal, also monitored by a meter.
- **Feedback Loop:** The man's role is to adjust the variable resistor to keep the collector current ($I_C$) proportional to the base current ($I_B$) by a factor of $h_{FE}$ or $\beta$. This illustrates a feedback mechanism where the man continuously adjusts to maintain the desired current ratio.

3. Labels, Annotations, and Key Features:
- **Equation:** Above the man's head is the equation $I_C = h_{FE} I_B$, indicating the relationship he is trying to maintain.
- **Base (B), Collector (C), Emitter (E):** These are labeled to show the standard transistor terminals.
- **Speech Bubble/Thought Cloud:** The equation is depicted in a thought cloud, symbolizing the man's focus on maintaining this relationship.

This cartoon serves as an educational tool to explain how a transistor works by showing the continuous adjustment needed to maintain the desired current relationship, highlighting the dynamic nature of transistor operation.

Figure 2.7. "Transistor man" observes the base current, and adjusts the output rheostat in an attempt to maintain the output current $\beta$ times larger; $h_{\mathrm{FE}}$ and $\beta$ are used interchangeably.

One warning is in order here: don't think that the collector of a transistor looks like a resistor. It doesn't. Rather, it looks approximately like a poor-quality constant-current sink (the value of current depending on the signal applied to the base), primarily because of this little man's efforts.

Another thing to keep in mind is that, at any given time, a transistor may be (a) cut off (no collector current), (b) in the active region (some collector current, and collector voltage more than a few tenths of a volt above the emitter), or (c) in saturation (collector within a few tenths of a volt of the emitter). See the discussion of transistor saturation in Chapter $2 x$ for more details.

### 2.2.2 Switching circuit examples

The transistor switch is an example of a nonlinear circuit: the output is not proportional to the input; ${ }^{8}$ instead it goes to one of two possible states (cut off, or saturated). Such two-state circuits are extremely common ${ }^{9}$ and form the basis of digital electronics. But to the authors the subject of

[^52]linear circuits (such as amplifiers, current sources, and integrators) offers the most interesting challenges and the potential for great circuit creativity. We will move on to linear circuits in a moment, but this is a good time to enjoy a few circuit examples with transistors acting as switches we like to give a feeling for the richness of electronics by showing real-world examples as soon as possible.

#### A. LED driver

Light-emitting diode indicators - LEDs - have replaced the incandescent lamps of yesteryear for all electronic indicator and readout applications; they're cheap, they come in lots of colors, and they last just about forever. Electrically they are similar to the ordinary silicon signal diodes we met in Chapter 1, but with a larger forward voltage drop (generally in the range of $1.5-3.5 \mathrm{~V}$, rather than approximately ${ }^{10}$ 0.6 V ); that is, as you slowly increase the voltage across an LED's terminals, you find that they start conducting current at, say, 1.5 V , and the current increases rapidly as you apply somewhat more voltage (Figure 2.8). They light up, too! Typical "high-efficiency" indicator LEDs look pretty good at a few milliamps, and they'll knock your eye out at 10-20 mA.
image_name:Figure 2.8
description:The graph in Figure 2.8 is a current versus voltage (I-V) plot, depicting the behavior of various diodes, including LEDs and a 1N914 silicon diode.

1. **Type of Graph and Function:**
- This is a linear I-V graph showing how current (in milliamperes) varies with applied voltage (in volts) across different diodes.

2. **Axes Labels and Units:**
- The x-axis represents Voltage in volts (V), ranging from 0 to 4 volts.
- The y-axis represents Current in milliamperes (mA), ranging from 0 to 30 mA.

3. **Overall Behavior and Trends:**
- The graph shows a steep increase in current with a small increase in voltage for all diodes once a certain threshold voltage is reached. This indicates the forward voltage drop characteristic of diodes.
- The 1N914 silicon diode begins conducting at a lower forward voltage compared to the LEDs, starting around 0.6 volts.
- LEDs have larger forward voltage drops, with different colors of LEDs conducting at different voltages, typically starting from around 1.5 to 3.5 volts.

4. **Key Features and Technical Details:**
- The graph includes curves for several types of LEDs, labeled as IR, red, amber, green (GaP), bright green (GaN), and blue/white. Each of these LEDs shows a different threshold voltage where conduction begins.
- The curves for LEDs are steeper than that of the silicon diode, indicating a rapid increase in current with voltage once the threshold is crossed.

5. **Annotations and Specific Data Points:**
- The graph is annotated with labels for each type of diode, indicating their respective positions and conduction thresholds.
- The 1N914 silicon diode shows conduction starting just below 1 volt, while LEDs start conducting between approximately 1.5 volts (IR) and 3 volts (blue, white).
- The current increases rapidly beyond the threshold voltage, reaching up to 30 mA as depicted on the graph.

Figure 2.8. Like silicon diodes, LEDs have rapidly increasing current versus applied voltage, but with larger forward voltage drops.

We'll show a variety of techniques for driving LEDs in Chapter 12; but we can drive them already, with what we know. The first thing to realize is that we can't just switch a voltage across them, as in Figure 2.5, because of their steep $I$ versus $V$ behavior; for example, applying 5 V across an

[^53]LED is guaranteed to blow it out. We need instead to treat it gently, coaxing it to draw the right current.

Let's assume that we want the LED to light in response to a digital signal line when it goes to a HIGH value of +3.3 V (from its normal resting voltage near ground). Let's assume also that the digital line can provide up to 1 mA of current, if needed. The procedure goes like this: first, choose an LED operating current that will provide adequate brightness, say 5 mA (you might want to try a few samples, to make sure you like the color, brightness, and viewing angle). Then use an $n p n$ transistor as a switch (Figure 2.9), choosing the collector resistor to provide the chosen LED current, realizing that the voltage drop across the resistor is the supply voltage minus the LED forward drop at its operating current. Finally, choose the base resistor to ensure saturation, assuming a conservatively low transistor beta ( $\beta \geq 25$ is pretty safe for a typical small-signal transistor like the popular 2N3904).
image_name:Figure 2.9
description:
[
name: LED, type: Diode, ports: {Na: 3.3V, Nc: K1}
name: R1, type: Resistor, value: 330, ports: {N1: K1, N2: C1}
name: R2, type: Resistor, value: 10k, ports: {N1: Vin, N2: b1}
name: Q1, type: NPN, ports: {C: C1, B: b1, E: GND}
]
extrainfo:The circuit is a simple LED driver using an NPN transistor (2N3904) as a switch. The LED is powered by a +3.3V supply, with a current-limiting resistor (330 ohms) in series. The base of the transistor is driven by a Vin signal through a 10k ohm resistor, ensuring the transistor is saturated when turned on, allowing current to flow from the +3.3V supply through the LED and the transistor to ground.

Figure 2.9. Driving an LED from a "logic-level" input signal, using an $n p n$ saturated switch and series current-limiting resistor.

Note that the transistor is acting as a saturated switch, with the collector resistor setting the operating current. As we'll see shortly, you can devise circuits that provide an accurate current output, largely independent of what the load does. Such a "current source" can also be used to drive LEDs. But our circuit is simple, and effective. There are other variations: we'll see in the next chapter that a MOSFET-type ${ }^{11}$ transistor is often a better choice. And in Chapters $10-12$ we'll see ways to drive LEDs and other optoelectronic devices directly from digital integrated circuits, without external discrete transistors.

Exercise 2.1. What is the LED current, approximately, in the circuit of Figure 2.9? What minimum beta is required for $Q_{1}$ ?

#### B. Variations on a theme

For these switch examples, one side of the load is connected to a positive supply voltage, and the other side is

[^54]switched to ground by the $n p n$ transistor switch. What if you want instead to ground one side of the load and switch the "high side" to a positive voltage?

It's easy enough - but you've got to use the other polarity of transistor (pnp), with its emitter at the positive rail, and its collector tied to the load's high side, as in Figure 2.10 A . The transistor is cut off when the base is held at the emitter voltage (here +15 V ), and switched into saturation by bringing the base toward the collector (i.e., toward ground). When the input is brought to ground, there's about 4 mA of base current through the $3.3 \mathrm{k} \Omega$ base resistor, sufficient for switching loads up to about $200 \mathrm{~mA}(\beta>50$ ).

An awkwardness of this circuit is the need to hold the input at +15 V to turn off the switch; it would be much better to use a lower control voltage, for example, +3 V and ground, commonly available in digital logic that we'll be seeing in Chapters $10-15$. Figure 2.10B shows how to do that: npn switch $Q_{2}$ accepts the "logic-level" input of 0 V or +3 V , pulling its collector load to ground accordingly. When $Q_{2}$ is cut off, $R_{3}$ holds $Q_{3}$ off; when $Q_{2}$ is saturated (by a +3 V input), $R_{2}$ sinks base current from $Q_{3}$ to bring it into saturation.

The "divider" formed by $R_{2} R_{3}$ may be confusing: $R_{3}$ 's job is to keep $Q_{3}$ off when $Q_{2}$ is off; and when $Q_{2}$ pulls its collector low, most of its collector current comes from $Q_{3}$ 's base (because only $\sim 0.6 \mathrm{~mA}$ of the 4.4 mA collector current comes from $R_{3}$ - make sure you understand why). That is, $R_{3}$ does not have much effect on $Q_{3}$ 's saturation. Another way to say it is that the divider would sit at about +11.6 V (rather than +14.4 V ), were it not for $Q_{3}$ 's baseemitter diode, which consequently gets most of $Q_{2}$ 's collector current. In any case, the value of $R_{3}$ is not critical and could be made larger; the tradeoff is slower turn-off of $Q_{3}$, owing to capacitive effects. ${ }^{12}$
image_name:A
description:
[
name: Q1, type: PNP, ports: {C: e1, B: b1, E: VDD}
name: R2, type: Resistor, value: 3.3k, ports: {N1: b1, N2: Vin}
]
extrainfo:The circuit diagram A shows a PNP transistor Q1 configured as a switch. The base of Q1 is connected to a resistor R2 and the input voltage Vin. The emitter is connected to VDD, and the collector is connected to a load and ground. This setup allows Q1 to control the high side of the load connected to ground.
image_name:B
description:
[
name: Q2, type: NPN, ports: {C: c2, B: b2, E: GND}
name: Q3, type: PNP, ports: {C: e2, B: b3, E: VDD}
name: R1, type: Resistor, value: 10k, ports: {N1: Vin, N2: b2}
name: R2, type: Resistor, value: 3.3k, ports: {N1: c2, N2: b3}
name: R3, type: Resistor, value: 1k, ports: {N1: b3, N2: VDD}
]
extrainfo:The circuit is a pulse generator. Q2 is an NPN transistor that switches the load connected to ground. Q3 is a PNP transistor, which is used to control the saturation of Q2. R1, R2, and R3 are used to control the biasing of the transistors. The circuit operates with a +15V supply.

Figure 2.10. Switching the high side of a load returned to ground.

[^55]
#### C. Pulse generator -I

By including a simple $R C$, you can make a circuit that gives a pulse output from a step input; the time constant $\tau=R C$ determines the pulse width. Figure 2.11 shows one way. $Q_{2}$ is normally held in saturation by $R_{3}$, so its output is close to ground; note that $R_{3}$ is chosen small enough to ensure $Q_{2}$ 's saturation. With the circuit's input at ground, $Q_{1}$ is cut off, with its collector at +5 V . The capacitor $C_{1}$ is therefore charged, with +5 V on its left terminal and approximately +0.6 V on its right terminal; i.e., it has about 4.4 V across it. The circuit is waiting for something to happen.
image_name:Figure 2.11
description:
[
name: R1, type: Resistor, value: 10k, ports: {N1: Vin, N2: b1}
name: R2, type: Resistor, value: 1k, ports: {N1: VCC, N2: c1}
name: R3, type: Resistor, value: 10k, ports: {N1: VCC, N2: b2}
name: R4, type: Resistor, value: 1k, ports: {N1: Vout, N2: VCC}
name: C1, type: Capacitor, value: 10nF, ports: {Np: c1, Nn: b2}
name: Q1, type: NPN, ports: {C: c1, B: b1, E: GND}
name: Q2, type: NPN, ports: {C: Vout, B: b2, E: GND}
]
extrainfo:The circuit generates a short pulse from a step input waveform. Q1 and Q2 are NPN transistors used to control the pulse generation. A positive input step at Vin saturates Q1, causing a voltage change across C1 that affects Q2, leading to an output pulse at Vout.
image_name:Generating a short pulse from a step input waveform
description:The graph is a time-domain waveform illustrating the behavior of a circuit designed to generate a short pulse from a step input. It consists of three separate plots aligned vertically, each depicting different aspects of the circuit's response over time.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform plot.

2. **Axes Labels and Units:**
- The x-axis represents time, although specific units are not labeled, it is implied to be in seconds or milliseconds based on typical circuit analysis.
- The y-axis for each plot represents voltage in volts.
- The plots are linear in scale.

3. **Overall Behavior and Trends:**
- **Input ("in") Plot:** Shows a step input waveform that transitions from 0 V to +5 V, indicating a positive step input.
- **Base of Q2 ("base Q2") Plot:** Initially at +0.6 V, the voltage at the base of Q2 momentarily drops to around -4.4 V when the input step occurs, before gradually returning to +0.6 V.
- **Output ("out") Plot:** Reflects the output pulse. It starts at 0 V, jumps to +5 V in response to the input step, and then returns to 0 V after a brief period, indicating the generation of a short pulse.

4. **Key Features and Technical Details:**
- The input step from 0 V to +5 V triggers the sequence.
- The base Q2 voltage drop to -4.4 V is crucial for cutting off Q2, leading to the output pulse.
- The output pulse is characterized by a sharp rise to +5 V and a subsequent fall back to 0 V, indicating a short pulse duration.

5. **Annotations and Specific Data Points:**
- The base Q2 plot shows a dashed line returning to +0.6 V, indicating the expected steady state after the transient response.
- The output plot aligns with the input step, showing a clear correlation between the input and the generated pulse.

This graph effectively illustrates the transient response of the circuit, highlighting how a step input can be used to generate a controlled short pulse at the output.

Figure 2.11. Generating a short pulse from a step input waveform.
A +5 V positive input step brings $Q_{1}$ into saturation (note the values of $R_{1}$ and $R_{2}$ ), forcing its collector to ground; because of the voltage across $C_{1}$, this brings the base of $Q_{2}$ momentarily negative, to about $-4.4 \mathrm{~V}{ }^{13} Q_{2}$ is then cutoff, no current flows through $R_{4}$, and so its output jumps to +5 V ; this is the beginning of the output pulse. Now for the $R C$ : $C_{1}$ can't hold $Q_{2}$ 's base below ground forever, because current is flowing down through $R_{3}$, trying to pull it up. So the right-hand side of the capacitor charges toward +5 V , with a time constant $\tau=R_{3} C_{1}$, here equal to $100 \mu \mathrm{~s}$. The output pulse width is set by this time constant

[^56]and is proportional to $\tau$. To figure out the pulse width accurately you have to look in detail at the circuit operation. In this case it's easy enough to see that the output transistor $Q_{2}$ will turn on again, terminating the output pulse, when the rising voltage on the base of transistor $Q_{2}$ reaches the $\approx 0.6 \mathrm{~V} V_{\mathrm{BE}}$ drop required for turn-on. Try this problem to test your understanding.

Exercise 2.2. Show that the output pulse width for the circuit of Figure 2.11 is approximately $T_{\text {pulse }}=0.76 R_{3} C_{1}=76 \mu \mathrm{~s}$. A good starting point is to notice that $C_{1}$ is charging exponentially from -4.4 V toward +5 V , with the time constant as above.

#### D. Pulse generator - II

Let's play with this circuit a bit. It works fine as described, but note that it requires that the input remain high throughout the duration of the output pulse, at least. It would be nice to eliminate that restriction, and the circuit in Figure 2.12 shows how. To the original circuit we've added a third transistor switch $Q_{3}$, whose job is to hold the collector of $Q_{1}$ at ground once the output pulse begins, regardless of what the input signal does. Now any positive input pulse - whether longer or shorter than the desired output pulse width - produces the same output pulse width; look at the waveforms in the figure. Note that we've chosen $R_{5}$ relatively large to minimize output loading while still ensuring full saturation of $Q_{3}$.

Exercise 2.3. Elaborate on this last statement: what is the output voltage during the pulse, slightly reduced owing to the loading effect of $R_{5}$ ? What is the minimum required beta of $Q_{3}$ to guarantee its saturation during the output pulse?

#### E. Pulse generator - III

For our final act, let's fix a deficiency of these circuits, namely a tendency for the output pulse to turn off somewhat slowly. That happens because $Q_{2}$ 's base voltage, with its leisurely $100 \mu \mathrm{~s} R C$ time constant, rises smoothly (and relatively slowly) through the turn-on voltage threshold of $\approx 0.6 \mathrm{~V}$. Note, by the way, that this problem does not occur at the turn-on of the output pulse, because at that transition $Q_{2}$ 's base voltage drops abruptly down to approximately -4.4 V , owing to the sharp input step waveform, which is further sharpened by the switching action of $Q_{1}$.

The cure here is to add at the output a clever circuit known as a Schmitt trigger, shown in its transistor implementation ${ }^{14}$ in Figure 2.13A. It works like this: imagine a time within the positive output pulse of the previous circuits, so the input to this new Schmitt circuit is high (near

[^57]image_name:Figure 2.12A
description:
[
name: R1, type: Resistor, value: 10k, ports: {N1: Vin, N2: b1}
name: R2, type: Resistor, value: 1k, ports: {N1: VCC, N2: C1C3}
name: R3, type: Resistor, value: 10k, ports: {N1: VCC, N2: b2}
name: R4, type: Resistor, value: 1k, ports: {N1: VCC, N2: Vout}
name: R5, type: Resistor, value: 20k, ports: {N1: b3, N2: Vout}
name: C1, type: Capacitor, value: 10nF, ports: {Np: b2, Nn: C1C3}
name: Q1, type: NPN, ports: {C: C1C3, B: b1, E: GND}
name: Q2, type: NPN, ports: {C: Vout, B: b2, E: GND}
name: Q3, type: NPN, ports: {C: C1C3, B: b3, E: GND}
]
extrainfo:This circuit is a Schmitt trigger implemented using transistors. It provides hysteresis to the input signal, ensuring a clean and stable output transition. The input signal is applied to the base of Q1, which is part of a feedback loop with Q3 to stabilize the collector voltage. The output is taken from the collector of Q2.
image_name:Figure 2.12
description:The graph in Figure 2.12 illustrates a series of time-domain waveforms associated with a transistor circuit. The graph is divided into four separate plots, each representing a different point in the circuit.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform, showing voltage levels over time at various points in the transistor circuit.

2. **Axes Labels and Units:**
- The horizontal axis represents time, although specific time units are not labeled.
- The vertical axis represents voltage in volts, with markings at -5, 0, and +5 volts.

3. **Overall Behavior and Trends:**
- **Input (in):** This waveform shows a step pulse starting at 0 V, rising to +5 V, and then returning to 0 V. The pulse is short, indicating a quick transition.
- **Base of Q2:** This waveform starts at 0 V, drops sharply to approximately -4.4 V, and then gradually returns toward a positive value, nearing +0.6 V. This indicates the behavior of Q2's base voltage in response to the input pulse.
- **Output (out):** The output waveform mirrors the input pulse but with some delay. It starts at 0 V, rises to +5 V, and then returns to 0 V, indicating the circuit's pulse-shaping function.
- **Collector of Q1, Q3:** This waveform starts at 0 V, dips slightly, and then rises to +5 V, showing the collector voltage behavior of transistors Q1 and Q3.

4. **Key Features and Technical Details:**
- The sharp drop in the base voltage of Q2 is critical, as it indicates a significant transition in the circuit operation, likely due to the switching action of Q1.
- The gradual return to +0.6 V at Q2's base suggests a recovery phase in the circuit.
- The output waveform's behavior suggests that the circuit is designed to generate a clean pulse from a step input, a typical application for pulse-shaping circuits.

5. **Annotations and Specific Data Points:**
- The base voltage of Q2 is annotated to show the approximate drop to -4.4 V and the recovery toward +0.6 V.
- The input and output waveforms are aligned, indicating a direct relationship between the input step and the output pulse.

Overall, the graph depicts the functioning of a transistor-based pulse generator or shaper, highlighting the behavior of voltages at critical points in the circuit during the input pulse transition.

Figure 2.12. Generating a short pulse from a step or pulse input.
$+5 \mathrm{~V})$. That holds $Q_{4}$ in saturation, and so $Q_{5}$ is cut off, with the output at +5 V . The emitter current of $Q_{4}$ is about 5 mA , so the emitter voltage is approximately +100 mV ; the base is a $V_{\mathrm{BE}}$ higher, approximately +700 mV .

Now imagine the trailing edge of the input pulse waveform, whose voltage smoothly drops toward ground. As it drops below 700 mV , $Q_{4}$ begins to turn off, so its collector voltage rises. If this were a simple transistor switch (i.e., if $Q_{5}$ were absent) the collector would rise to +5 V ; here, however, the collector resistor $R_{7}$ instead supplies current to $Q_{5}$, putting it in saturation. So $Q_{5}$ 's collector drops nearly to ground.

At this simple level of analysis the circuit appears to be pretty useless, because its output is the same as its input! Let's look a little closer, though: as the input voltage drops through the 700 mV threshold and $Q_{5}$ turns on, the total emitter current rises to $\approx 10 \mathrm{~mA}$ ( 5 mA from $Q_{5}$ 's collector current, and another $\approx 5 \mathrm{~mA}$ from its base current, both of which flow out the emitter). The drop across the emitter resistor is now 200 mV , which means that the input threshold has increased to about +800 mV . So the input voltage, which had just dropped below 700 mV , now finds itself well below the new threshold, causing the
image_name:A
description:
[
name: Q4, type: NPN, ports: {C: c4b5, B: b4, E: e4e5}
name: Q5, type: NPN, ports: {C: Vout, B: c4b5, E: e4e5}
name: R6, type: Resistor, value: 25k, ports: {N1: Vin, N2: b4}
name: R7, type: Resistor, value: 1k, ports: {N1: c4b5, N2: +5V}
name: R8, type: Resistor, value: 1k, ports: {N1: Vout, N2: +5V}
name: R9, type: Resistor, value: 20Ω, ports: {N1: e4e5, N2: GND}
]
extrainfo:The circuit is a Schmitt trigger, which provides hysteresis to the input signal, resulting in abrupt transitions in the output. The threshold changes due to the feedback mechanism, with the input threshold increasing when Q5 turns on.
image_name:Figure 2.13B
description:Figure 2.13B is a graph illustrating the behavior of a Schmitt trigger circuit, specifically showing the hysteresis effect. The graph is a voltage transfer characteristic curve, plotting output voltage (Vout) against input voltage (Vin).

1. **Type of Graph and Function:**
- The graph is a voltage transfer characteristic curve for a Schmitt trigger, illustrating the hysteresis effect.

2. **Axes Labels and Units:**
- The x-axis represents the input voltage (Vin) in volts, ranging approximately from 0 to 0.9 volts.
- The y-axis represents the output voltage (Vout) in volts, ranging from 0 to +5 volts.

3. **Overall Behavior and Trends:**
- The graph shows a typical hysteresis loop with two distinct thresholds: a lower threshold around 0.7 volts and an upper threshold around 0.8 volts.
- As Vin increases past the upper threshold (~0.8V), the output voltage (Vout) abruptly transitions from 0 volts to 5 volts.
- Conversely, as Vin decreases past the lower threshold (~0.7V), Vout transitions back from 5 volts to 0 volts.
- This behavior demonstrates the regenerative switching action of the Schmitt trigger, where the output switches states abruptly once the thresholds are crossed.

4. **Key Features and Technical Details:**
- The hysteresis effect is evident; the output voltage does not change immediately with small changes in input voltage, creating a loop in the graph.
- The difference between the high and low threshold voltages is approximately 0.1 volts, which is the hysteresis width.
- The graph clearly shows the stability of output states between the thresholds, emphasizing the noise immunity provided by the Schmitt trigger.

5. **Annotations and Specific Data Points:**
- The graph includes annotations indicating the direction of change in Vout as Vin crosses each threshold.
- The formula \( \Delta V \approx \frac{R_9}{R_8} V_{CC} \) is noted, suggesting the relationship between resistors and the voltage change, although specific resistor values are not provided in the graph itself.

This description captures the essential characteristics of the Schmitt trigger's operation as depicted in the graph, highlighting its ability to produce clean, abrupt transitions in output voltage despite slow changes in input voltage.

B.

Figure 2.13. A "Schmitt trigger" produces an output with abrupt transitions, regardless of the speed of the input waveform.
output to switch abruptly. This "regenerative" action is how the Schmitt trigger turns a slowly moving waveform into an abrupt transition.

A similar action occurs as the input rises through this higher threshold; see Figure 2.13B, which illustrates how the output voltage changes as the input voltage passes through the two thresholds, an effect known as hysteresis. The Schmitt trigger produces rapid output transitions as the input passes through either threshold. We'll see Schmitt triggers again in Chapters 4 and 10.

There are many enjoyable applications of transistor switches, including "signal" applications like this (combined with more complex digital logic circuits), as well as "power switching" circuits in which transistors operating at high currents, high voltages, or both, are used to control hefty loads, perform power conversion, and so on. Transistor switches can also be used as substitutes for mechanical switches when we are dealing with continuous ("linear" or "analog") waveforms. We'll see examples of these in the next chapter, when we deal with FETs, which are ideally suited to such switching tasks, and again in Chapter 12, where we deal with the control of signals and external loads from logic-level signals.

We now move on to consider the first of several linear transistor circuits.

### 2.2.3 Emitter follower

Figure 2.14 shows an example of an emitter follower. It is called that because the output terminal is the emitter, which follows the input (the base), less one diode drop:

$$
V_{E} \approx V_{B}-0.6 \text { volts. }
$$

The output is a replica of the input, but 0.6 to 0.7 V less positive. For this circuit, $V_{\text {in }}$ must stay at +0.6 V or more, or else the output will sit at ground. By returning the emit-
ter resistor to a negative supply voltage, you can permit negative voltage swings as well. Note that there is no collector resistor in an emitter follower.
image_name:Figure 2.14. Emitter follower
description:
[
name: Q1, type: NPN, ports: {C: +10V, B: Vin, E: Vout}
name: R, type: Resistor, value: R, ports: {N1: Vout, N2: GND}
name: +10V, type: VoltageSource, value: +10V, ports: {Np: +10V, Nn: GND}
]
extrainfo:The circuit is an emitter follower configuration. It has high input impedance and low output impedance, providing a voltage gain of approximately 1. The output voltage is a slightly lower replica of the input voltage, offset by the base-emitter voltage drop (~0.6-0.7V).

Figure 2.14. Emitter follower.

At first glance this circuit may appear quite thoroughly useless, until you realize that the input impedance is much larger than the output impedance, as will be demonstrated shortly. This means that the circuit requires less power from the signal source to drive a given load than would be the case if the signal source were to drive the load directly. Or a signal of some internal impedance (in the Thévenin sense) can now drive a load of comparable or even lower impedance without loss of amplitude (from the usual voltage-divider effect). In other words, an emitter follower has current gain, even though it has no voltage gain. It has power gain. Voltage gain isn't everything!

### A. Impedances of sources and loads

This last point is very important and is worth some more discussion before we calculate in detail the beneficial effects of emitter followers. In electronic circuits, you're always hooking the output of something to the input of something else, as suggested in Figure 2.15. The signal source might be the output of an amplifier stage (with Thévenin equivalent series impedance $\mathbf{Z}_{\text {out }}$ ), driving the next stage or perhaps a load (of some input impedance $\mathbf{Z}_{\text {in }}$ ). In general, the loading effect of the following stage causes a reduction of signal, as we discussed earlier in $\S 1.2 .5 \mathrm{~A}$. For this reason it is usually best to keep $Z_{\text {out }} \ll Z_{\text {in }}$ (a factor of 10 is a comfortable rule of thumb).

In some situations it is OK to forgo this general goal of making the source stiff compared with the load. In particular, if the load is always connected (e.g., within a circuit) and if it presents a known and constant $\mathbf{Z}_{\text {in }}$, it is not too serious if it "loads" the source. However, it is always nicer if signal levels don't change when a load is connected. Also, if $\mathbf{Z}_{\text {in }}$ varies with signal level, then having a stiff source
( $Z_{\text {out }} \ll Z_{\text {in }}$ ) ensures linearity, where otherwise the leveldependent voltage divider would cause distortion. ${ }^{15}$

Finally, as we remarked in $\S 1.2 .5 \mathrm{~A}$, there are two situations in which $Z_{\text {out }} \ll Z_{\text {in }}$ is actually the wrong thing to do: in radiofrequency circuits we usually match impedances $\left(\mathbf{Z}_{\text {out }}=\mathbf{Z}_{\text {in }}\right)$, for reasons we'll describe in Appendix H. A second exception applies if the signal being coupled is a current rather than a voltage. In that case the situation is reversed, and we strive to make $Z_{\text {in }} \ll Z_{\text {out }}$ ( $Z_{\text {out }}=\infty$, for a current source).
image_name:Figure 2.15
description:The circuit illustrates a basic two-stage amplifier configuration. The first amplifier is connected to the second amplifier through a resistor Rout. Rin is the input impedance of the second amplifier. The ground is shared across the circuit.

Figure 2.15. Illustrating circuit "loading" as a voltage divider.

### B. Input and output impedances of emitter followers

As we've stated, the emitter follower is useful for changing impedances of signals or loads. To put it starkly, that's really the whole point of an emitter follower.

Let's calculate the input and output impedances of the emitter follower. In the preceding circuit we consider $R$ to be the load (in practice it sometimes is the load; otherwise the load is in parallel with $R$, but with $R$ dominating the parallel resistance anyway). Make a voltage change $\Delta V_{\mathrm{B}}$ at the base; the corresponding change at the emitter is $\Delta V_{\mathrm{E}}=$ $\Delta V_{\mathrm{B}}$. Then the change in emitter current is

$$
\Delta I_{\mathrm{E}}=\Delta V_{\mathrm{B}} / R,
$$

so

$$
\Delta I_{\mathrm{B}}=\frac{1}{\beta+1} \Delta I_{\mathrm{E}}=\frac{\Delta V_{\mathrm{B}}}{R(\beta+1)}
$$

(using $I_{\mathrm{E}}=I_{\mathrm{C}}+I_{\mathrm{B}}$ ). The input resistance is $\Delta V_{\mathrm{B}} / \Delta I_{\mathrm{B}}$. Therefore

$$
\begin{equation*}
r_{\text {in }}=(\beta+1) R \tag{2.2}
\end{equation*}
$$

The transistor small-signal (or "incremental") current gain

[^58]( $\beta$, or $h_{\mathrm{fe}}$ ) is typically about 100 , so a low-impedance load looks like a much higher impedance at the base; it is easier to drive.

In the preceding calculation we used the changes in the voltages and currents, rather than the steady (dc) values of those voltages (or currents), to arrive at our input resistance $r_{\text {in }}$. Such a "small-signal" analysis is used when the variations represent a possible signal, as in an audio amplifier, riding on a steady dc "bias" (see §2.2.7). Although we indicated changes in voltage and current explicitly (with " $\Delta V$," etc.), the usual practice is to use lowercase symbols for small-signal variations (thus $\Delta V \leftrightarrow v$ ); with this convention the above equation for $\Delta I_{\mathrm{E}}$, for example, would read $i_{\mathrm{E}}=v_{\mathrm{B}} / R$.

The distinction between dc current gain $\left(h_{\mathrm{FE}}\right)$ and smallsignal current gain ( $h_{\mathrm{fe}}$ ) isn't always made clear, and the term beta is used for both. That's alright, since $h_{\mathrm{fe}} \approx h_{\mathrm{FE}}$ (except at very high frequencies), and you never assume you know them accurately, anyway.

Although we used resistances in the preceding derivation, we could generalize to complex impedances by allowing $\Delta V_{\mathrm{B}}, \Delta I_{\mathrm{B}}$, etc., to become complex numbers. We would find that the same transformation rule applies for impedances:

$$
\begin{equation*}
\mathbf{Z}_{\mathrm{in}}=(\beta+1) \mathbf{Z}_{\text {load }} \tag{2.3}
\end{equation*}
$$

We could do a similar calculation to find that the output impedance $\mathbf{Z}_{\text {out }}$ of an emitter follower (the impedance looking into the emitter) driven from a source of internal impedance $\mathbf{Z}_{\text {source }}$ is given by

$$
\begin{equation*}
\mathbf{Z}_{\mathrm{out}}=\frac{\mathbf{Z}_{\text {source }}}{\beta+1} \tag{2.4}
\end{equation*}
$$

Strictly speaking, the output impedance of the circuit should also include the parallel resistance of $R$, but in practice $\mathbf{Z}_{\text {out }}$ (the impedance looking into the emitter) dominates.

Exercise 2.4. Show that the preceding relationship is correct. Hint: hold the source voltage fixed and find the change in output current for a given forced change in output voltage. Remember that the source voltage is connected to the base through a series resistor.

Because of these nice properties, emitter followers find application in many situations, e.g., making lowimpedance signal sources within a circuit (or at outputs), making stiff voltage references from higher-impedance references (formed from voltage dividers, say), and generally isolating signal sources from the loading effects of subsequent stages.
image_name:A
description:
[
name: R1, type: Resistor, value: 240Ω, ports: {N1: Vin, N2: b1}
name: R2, type: Resistor, value: 2.5Ω, ports: {N1: k1, N2: c1}
name: D1, type: Diode, ports: {Na: +5V, Nc: k1}
name: Q1, type: NPN, ports: {C: c1, B: b1, E: GND}
]
extrainfo:The circuit diagram 'A' shows an emitter follower configuration with Q1 driving a very bright white LED. The circuit is powered by a +5V supply and uses a resistor R1 to limit base current to Q1. The LED D1 has a forward voltage drop of 3.6V and operates at 0.5A. The emitter of Q1 is connected to ground, providing a low impedance output. The configuration allows a low-current control signal to switch a high-current load through the LED.
image_name:B
description:
[
name: D1, type: Diode, ports: {Na: +5V, Nc: k1}
name: R2, type: Resistor, value: 2.5Ω, ports: {N1: k1, N2: c3}
name: Q2, type: NPN, ports: {C: +5v, B: vin, E: e2}
name: R3, type: Resistor, value: 10k, ports: {N1: e2, N2: GND}
name: R4, type: Resistor, value: 100Ω, ports: {N1: e2, N2: b3}
name: Q3, type: NPN, ports: {C: c3, B: b3, E: GND}
]
extrainfo:Circuit B uses two NPN transistors (Q2 and Q3) to drive a load with a diode (D1) and resistors (R3 and R4) for biasing. The circuit operates with a +5V supply and is grounded at GND. The input is at Vin, and the output drives the diode.

Figure 2.16. Putting an emitter follower in front of a switch makes it easy for a low-current control signal to switch a high-current load.

Exercise 2.5. Use a follower with the base driven from a voltage divider to provide a stiff source of +5 volts from an available regulated +15 V supply. Load current $(\max )=25 \mathrm{~mA}$. Choose your resistor values so that the output voltage doesn't drop more than 5\% under full load.

### C. Follower drives switch

Figure 2.16 shows a nice example of an emitter follower rescuing an awkward circuit. We're trying to switch a really bright white LED (the kind you use for "area lighting"), which drops about 3.6 V at its desired 500 mA of forward current. And we've got a $0-3 \mathrm{~V}$ digital logic signal available to control the switch. The first circuit uses a single npn saturated switch, with a base resistor sized to produce 10 mA of base current, and a $2.5 \Omega$ current-limiting resistor in series with the LED.

This circuit is OK, sort of. But it draws an uncomfortably large current from the control input; and it requires $Q_{1}$ to have plenty of current gain at the full load current of 0.5 A . In the second circuit (Figure 2.16B) an emitter follower has come to the rescue, greatly reducing the input current (because of its current gain), and at the same time relaxing the minimum beta requirement of the switch $\left(Q_{3}\right)$. To be fair, we should point out that a low-threshold MOSFET provides an even simpler solution here; we'll tell you how, in Chapters 3 and 12.

### D. Important points about followers

Current flow in one direction only. Notice (\$2.1.1, rule 4) that in an emitter follower the npn transistor can only source (as opposed to sink) current. For instance, in the loaded circuit shown in Figure 2.17 the output can swing to within a transistor saturation voltage drop of $V_{\mathrm{CC}}$ (about +9.9 V ), but it cannot go more negative than -5 volts. That is because on the extreme negative swing, the transistor can do no better than to turn off completely, which it does at -4.4 volts input ( -5 V out-
image_name:Figure 2.17
description:
[
'name': 'Q1', 'type': 'NPN', 'ports': {'C': 'VDD', 'B': 'Vin', 'E': 'Vout'
'name': 'R1', 'type': 'Resistor', 'value': '1.0k', 'ports': {'N1': 'Vout', 'N2': '-10V'
'name': 'Rload', 'type': 'Resistor', 'value': '1.0k', 'ports': {'N1': 'Vout', 'N2': 'GND'
]
extrainfo:This circuit is an NPN emitter follower configuration. It can source current through the transistor but has limited ability to sink current through the emitter resistor. The output voltage can swing close to the positive supply voltage but is limited on the negative side by the transistor turning off.

Figure 2.17. An npn emitter follower can source plenty of current through the transistor, but can sink limited current only through its emitter resistor.
put, set by the divider formed by the load and emitter resistors). Further negative swing at the input results in back-biasing of the base-emitter junction, but no further change in output. The output, for a 10 volt amplitude sinewave input, looks as shown in Figure 2.18.
image_name:Figure 2.18
description:The graph in Figure 2.18 is a time-domain waveform illustrating the behavior of an npn emitter follower circuit. The x-axis represents time, while the y-axis represents voltage, with a range from -10 volts to +10 volts. Both axes are marked with linear scales.

The graph shows two waveforms: an input sine wave and an output waveform. The input sine wave has a peak amplitude of 10 volts, oscillating symmetrically about the zero voltage line. The output waveform, however, shows a distinct asymmetry.

In the positive half-cycle, the output waveform closely follows the input waveform but is offset by 0.6 volts below the input. This offset is likely due to the voltage drop across the base-emitter junction of the transistor.

In the negative half-cycle, the output waveform is clipped at -5 volts, indicating the limit of the current sinking capability of the emitter follower. This clipping occurs because the transistor goes out of the active region, and the emitter resistor limits the current.

The graph effectively demonstrates the asymmetrical current drive capability of the npn emitter follower, where it can source current effectively on the positive side but is limited in sinking current on the negative side. The annotations on the graph point out the 0.6V offset and the -5V clipping level, highlighting these critical features of the circuit's performance.

Figure 2.18. Illustrating the asymmetrical current drive capability of the $n p n$ emitter follower.

Another way to view the problem is to say that the emitter follower has a low value of small-signal output impedance, whereas its large-signal output impedance is much higher (as large as $R_{\mathrm{E}}$ ). The output impedance changes over from its small-signal value to its largesignal value at the point where the transistor goes out of the active region (in this case at an output voltage of -5 V ). To put this point another way, a low value of small-signal output impedance doesn't necessarily mean that the circuit can generate large signal swings into a low resistance load. A low small-signal output impedance doesn't imply a large output current capability.

Possible solutions to this problem involve either decreasing the value of the emitter resistor (with greater power dissipation in resistor and transistor), using a pnp transistor (if all signals are negative only), or using a "push-pull" configuration, in which two complementary transistors (one npn, one pnp) are used (§2.4.1). This sort of problem can also come up when the load that an emitter follower is driving contains voltage or current sources of its own, and thus can force a current in the "wrong" direction. This happens most often with
regulated power supplies (the output is usually an emitter follower) driving a circuit that has other power supplies.
Base-emitter breakdown. Always remember that the base-emitter reverse breakdown voltage for silicon transistors is small, quite often as little as 6 volts. Input swings large enough to take the transistor out of conduction can easily result in breakdown (causing permanent degradation of current gain $\beta$ ) unless a protective diode is added (Figure 2.19).
image_name:Figure 2.19
description:
[
name: Q1, type: NPN, ports: {C: c1, B: bk1, E: e1}
name: D1, type: Diode, ports: {Na: bk1, Nc: e1}
]
extrainfo:The circuit diagram shows an NPN transistor (Q1) with a diode (D1) connected to prevent base-emitter reverse voltage breakdown. The base of the transistor is connected to node bk1, the collector to c1, and the emitter to e1. The diode is connected with its anode at bk1 and cathode at e1, providing protection against reverse breakdown.

Figure 2.19. A diode prevents base-emitter reverse voltage breakdown.

Gain is slightly less than unity. The voltage gain of an emitter follower is actually slightly less than 1.0 , because the base-emitter voltage drop is not really constant, but depends slightly on collector current. You will see how to handle that later in the chapter, when we have the Ebers-Moll equation.

### 2.2.4 Emitter followers as voltage regulators

The simplest regulated supply of voltage is simply a zener (Figure 2.20). Some current must flow through the zener, so you choose

$$
\frac{V_{\mathrm{in}}(\min )-V_{\text {out }}}{R}>I_{\mathrm{out}}(\max ) .
$$

Because $V_{\text {in }}$ isn't regulated, you use the lowest value of $V_{\text {in }}$ that might occur. Designing for satisfactory operation under the worst combination (here minimum $V_{\text {in }}$ and maximum $I_{\text {out }}$ ) is known as "worst-case" design. In practice, you would also worry about component tolerances, linevoltage limits, etc., designing to accommodate the worst possible combination that would ever occur.
image_name:Figure 2.20. Simple zener voltage regulator
description:
[
name: R, type: Resistor, value: R, ports: {N1: Vin, N2: Vout}
name: D1, type: Diode, ports: {Na: GND, Nc: Vout}
]
extrainfo:The circuit is a simple zener voltage regulator. It uses a resistor (R) and a zener diode (D1) to regulate the output voltage (Vout) to be equal to the zener voltage (Vzener). The input voltage (Vin) is unregulated and may have some ripple.

Figure 2.20. Simple zener voltage regulator.

The zener must be able to dissipate

$$
P_{\text {zener }}=\left(\frac{V_{\mathrm{in}}-V_{\mathrm{out}}}{R}-I_{\mathrm{out}}\right) V_{\text {zener }}
$$

Again, for worst-case design, you would use $V_{\text {in }}(\max )$ and $I_{\text {out }}$ (min).

Exercise 2.6. Design a +10 V̇ regulated supply for load currents from 0 to 100 mA ; the input voltage is +20 to +25 V . Allow at least 10 mA zener current under all (worst-case) conditions. What power rating must the zener have?

This simple zener-regulated supply is sometimes used for noncritical circuits or circuits using little supply current. However, it has limited usefulness, for several reasons:

- $V_{\text {out }}$ isn't adjustable or settable to a precise value.
- Zener diodes give only moderate ripple rejection and regulation against changes of input or load, owing to their finite dynamic impedance.
- For widely varying load currents a high-power zener is often necessary to handle the dissipation at low load current. ${ }^{16}$

By using an emitter follower to isolate the zener, you get the improved circuit shown in Figure 2.21. Now the situation is much better. Zener current can be made relatively independent of load current, since the transistor base current is small, and far lower zener power dissipation is possible (reduced by as much as a factor of $\beta$ ). The collector resistor $R_{\mathrm{C}}$ can be added to protect the transistor from momentary output short circuits by limiting the current, even though it is not essential to the emitter follower function. Choose $R_{\mathrm{C}}$ so that the voltage drop across it is less than the drop across $R$ for the highest normal load current (i.e., so that the transistor does not saturate at maximum load).
image_name:Figure 2.21
description:
[
name: R, type: Resistor, value: R, ports: {N1: Vin, N2: Vb}
name: RC, type: Resistor, value: RC, ports: {N1: Vin, N2: C}
name: D1, type: Diode, ports: {Na: GND, Nc: vb}
name: Q1, type: NPN, ports: {C: C, B: Vb, E: Vout}
]
extrainfo:The circuit is a zener regulator with an emitter follower configuration. It uses a zener diode for voltage regulation and an NPN transistor to increase output current capability. The resistor RC is used to protect the transistor by limiting the maximum output current.

Figure 2.21. Zener regulator with follower, for increased output current. $R_{\mathrm{C}}$ protects the transistor by limiting maximum output current.

[^59]Exercise 2.7. Design a +10 V supply with the same specifications as in Exercise 2.6. Use a zener and emitter follower. Calculate worst-case dissipation in transistor and zener. What is the percentage change in zener current from the no-load condition to full load? Compare with your previous circuit.

A nice variation of this circuit aims to eliminate the effect of ripple current (through $R$ ) on the zener voltage by supplying the zener current from a current source, which is the subject of §2.2.6. An alternative method uses a lowpass filter in the zener bias circuit (Figure 2.22). $R$ is chosen such that the series pair provides sufficient zener current. Then $C$ is chosen large enough so that $R C \gg 1 / f_{\text {ripple }} \cdot{ }^{17}$.

Later you will see better voltage regulators, ones in which you can vary the output easily and continuously by using feedback. They are also better voltage sources, with output impedances measured in milliohms, temperature coefficients of a few parts per million per degree centigrade, and other desirable features.
image_name:Figure 2.22
description:
[
name: R, type: Resistor, value: R, ports: {N1: b1k1, N2: X1}
name: RC, type: Resistor, value: RC, ports: {N1: Vin, N2: C1}
name: C, type: Capacitor, value: C, ports: {Np: X1, Nn: GND}
name: D1, type: Diode, ports: {Na: GND, Nc: b1k1}
name: Q1, type: NPN, ports: {C: c1, B: b1k1, E: Vout}
]
extrainfo:The circuit is a zener regulator designed to reduce ripple with a zener diode and an NPN transistor configured as an emitter follower. The resistor R and capacitor C form an RC filter. The diode D1 provides voltage regulation, and the transistor Q1 buffers the output.

Figure 2.22. Reducing ripple in the zener regulator.
image_name:Figure 2.23
description:
[
name: R1, type: Resistor, ports: {N1: VCC, N2: b1}
name: R2, type: Resistor, ports: {N1: b2, N2: GND}
name: R3, type: Resistor, ports: {N1: Vout, N2: GND}
name: Cib, type: Capacitor, ports: {Np: b1, Nn: b2}
name: Cib2, type: Capacitor, ports: {Np: b1, Nn: Vout}
name: Q1, type: NPN, ports: {C: b1, B: Vin, E: b2}
name: Q2, type: NPN, ports: {C: VCC, B: Vout, E: Vout}
]
extrainfo:The circuit diagram illustrates an emitter follower configuration using two NPN transistors, Q1 and Q2. The circuit is designed to provide a buffered output at Vout. R1 and R2 are biasing resistors for Q1, while R3 is the load resistor for Q2. Capacitors Cib and Cib2 are used for coupling and bypassing.

Figure 2.23. Biasing an emitter follower from a previous stage.

### 2.2.5 Emitter follower biasing

When an emitter follower is driven from a preceding stage in a circuit, it is usually OK to connect its base directly to the previous stage's output, as shown in Figure 2.23.

[^60]Because the signal on $Q_{1}$ 's collector is always within the range of the power supplies, $Q_{2}$ 's base will be between $V_{\mathrm{CC}}$ and ground, and therefore $Q_{2}$ is in the active region (neither cut off nor saturated), with its base-emitter diode in conduction and its collector at least a few tenths of a volt more positive than its emitter. Sometimes, though, the input to a follower may not be so conveniently situated with respect to the supply voltages. A typical example is a capacitively coupled (or ac-coupled) signal from some external source (e.g., an audio signal input to a stereo amplifier). In that case the signal's average voltage is zero, and direct coupling to an emitter follower will give an output like that in Figure 2.24.
image_name:Figure 2.24
description:The graph in Figure 2.24 displays a time-domain waveform comparison between an input signal and the corresponding output from a transistor amplifier powered by a single positive supply. The x-axis represents time, while the y-axis represents voltage, with no specific units or scales indicated.

Overall Behavior and Trends:
The graph shows two distinct waveforms. The input waveform is depicted with a thicker line, while the output waveform is shown with a thinner line. Both waveforms exhibit periodic behavior with peaks and valleys, indicating oscillations over time.

Key Features and Technical Details:
- **Input Waveform:** The input signal crosses the zero-voltage line multiple times, illustrating its AC nature. It has noticeable peaks and troughs, with the waveform extending both above and below the zero line, indicating positive and negative voltage swings.
- **Output Waveform:** The output waveform closely follows the input waveform's shape but is clipped at the zero line, showing that the amplifier cannot produce negative voltage swings. This clipping results in a distortion of the output signal compared to the input.

Annotations and Specific Data Points:
- The graph is annotated with labels indicating which line represents the input and which represents the output.
- The horizontal line at zero volts serves as a reference, highlighting the inability of the output to swing negatively.

This graph effectively illustrates the limitation of a transistor amplifier using a single positive supply, where the output cannot mirror the negative portions of an AC input signal, leading to a distorted output waveform.

Figure 2.24. A transistor amplifier powered from a single positive supply cannot generate negative voltage swings at the transistor output terminal.

It is necessary to bias the follower (in fact, any transistor amplifier) so that collector current flows during the entire signal swing. In this case a voltage divider is the simplest way (Figure 2.25). $R_{1}$ and $R_{2}$ are chosen to put the base halfway between ground and $V_{\mathrm{CC}}$ when there is no input signal, i.e., $R_{1}$ and $R_{2}$ are approximately equal. The process of selecting the operating voltages in a circuit, in the absence of applied signals, is known as setting the quiescent point. In this case, as in most cases, the quiescent point is chosen to allow maximum symmetrical signal swing of the output waveform without clipping (flattening of the top or bottom of the waveform). What values should $R_{1}$ and $R_{2}$ have? Applying our general principle ( $\S 1.2 .5 \mathrm{~A}$, $\S 2.2 .3 \mathrm{~A}$ ), we make the impedance of the dc bias source (the impedance looking into the voltage divider) small compared with the load it drives (the dc impedance looking into the base of the follower). In this case,

$$
R_{1} \| R_{2} \ll \beta R_{\mathrm{E}}
$$

This is approximately equivalent to saying that the current flowing in the voltage divider should be large compared with the current drawn by the base.
image_name:Figure 2.25
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: VCC, N2: b}
name: R2, type: Resistor, value: R2, ports: {N1: b, N2: GND}
name: RE, type: Resistor, value: RE, ports: {N1: e, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: b}
name: C2, type: Capacitor, value: C2, ports: {Np: e, Nn: Vout}
name: Q1, type: NPN, ports: {C: VCC, B: b, E: e}
]
extrainfo:This circuit is an AC-coupled emitter follower designed for audio signals ranging from 20 Hz to 20 kHz. The power supply voltage is 15 V, and the quiescent current is 1 mA. The emitter voltage is set to 7.5 V for maximum symmetrical swing.

Figure 2.25. An ac-coupled emitter follower. Note base bias voltage divider.

#### A. Emitter follower design example

As an actual design example, let's make an emitter follower for audio signals $(20 \mathrm{~Hz}$ to 20 kHz$) . V_{\mathrm{CC}}$ is +15 V , and quiescent current is to be 1 mA .

Step 1. Choose $V_{E}$. For the largest possible symmetrical swing without clipping, $V_{\mathrm{E}}=0.5 V_{\mathrm{CC}}$, or +7.5 volts.

Step 2. Choose $R_{\mathrm{E}}$. For a quiescent current of 1 mA , $R_{\mathrm{E}}=7.5 \mathrm{k}$.

Step 3. Choose $R_{1}$ and $R_{2} . V_{\mathrm{B}}$ is $V_{\mathrm{E}}+0.6 \mathrm{~V}$, or 8.1 V . This determines the ratio of $R_{1}$ to $R_{2}$ as $1: 1.17$. The preceding loading criterion requires that the parallel resistance of $R_{1}$ and $R_{2}$ be about 75 k or less (one-tenth of $7.5 \mathrm{k} \times \beta$ ). Suitable standard values are $R_{1}=130 \mathrm{k}, R_{2}=150 \mathrm{k}$.

Step 4. Choose $C_{1}$. The capacitor $C_{1}$ forms a highpass filter with the impedance it sees as a load, namely the impedance looking into the base in parallel with the impedance looking into the base voltage divider. If we assume that the load this circuit will drive is large compared with the emitter resistor, then the impedance looking into the base is $\beta R_{\mathrm{E}}$, about 750 k . The divider looks like 70 k . So the capacitor sees a load of about 63 k , and it should have a value of at least $0.15 \mu \mathrm{~F}$ so that the 3 dB point will be below the lowest frequency of interest, 20 Hz .

Step 5. Choose $C_{2}$. The capacitor $C_{2}$ forms a highpass filter in combination with the load impedance, which is unknown. However, it is safe to assume that the load impedance won't be smaller than $R_{\mathrm{E}}$, which gives a value for $C_{2}$ of at least $1.0 \mu \mathrm{~F}$ to put the 3 dB point below 20 Hz . Because there are now two cascaded highpass filter sections, the capacitor values should be increased somewhat to prevent excessive attenuation (reduction of signal amplitude, in this case 6 dB ) at the lowest frequency of interest. $C_{1}=0.47 \mu \mathrm{~F}$ and $C_{2}=3.3 \mu \mathrm{~F}$ might be good choices. ${ }^{18}$

[^61]From our simple transistor model, the output impedance at the emitter is just $\mathbf{Z}_{\text {out }}=R_{\mathrm{E}} \|\left[\left(\mathbf{Z}_{\text {in }}\left\|R_{1}\right\| R_{2}\right) / \beta\right]$, where $\mathbf{Z}_{\text {in }}$ is the (Thévenin) output resistance of the signal that drives this circuit. So, taking $\beta \approx 100$, a signal source with $10 \mathrm{k} \Omega$ output resistance would result in an output impedance (at the emitter) of about $87 \Omega$. As we'll see later in the chapter (§2.3), there's an effect (the intrinsic emitter impedance, $r_{\mathrm{e}}$ ) that adds an additional resistance of $0.025 / I_{\mathrm{E}}$ effectively in series with the emitter; so the output impedance here (with $10 \mathrm{k} \Omega$ source) would be about $110 \Omega$.

#### B. Followers with split supplies

Because signals often are "near ground," it is convenient to use symmetrical positive and negative supplies. This simplifies biasing and eliminates coupling capacitors (Figure 2.26).
Warning: you must always provide a dc path for base bias current, even if it goes only to ground. In this circuit it is assumed that the signal source has a dc path to ground. If not (e.g., if the signal is capacitively coupled), you must provide a resistor to ground (Figure 2.27). $R_{\mathrm{B}}$ could be about one-tenth of $\beta R_{\mathrm{E}}$, as before.

Exercise 2.8. Design an emitter follower with $\pm 15 \mathrm{~V}$ supplies to operate over the audio range ( 20 Hz to 20 kHz ). Use 5 mA quiescent current and capacitive input coupling.
image_name:Figure 2.26. A dc-coupled emitter follower with split supply.
description:
[
name: Q1, type: NPN, ports: {C: +VCC, B: Vin, E: Vout}
name: RE, type: Resistor, value: RE, ports: {N1: Vout, N2: -VEE}
]
extrainfo:The circuit is a DC-coupled emitter follower with split supply, using an NPN transistor (Q1) and a resistor (RE) to provide biasing and stabilization. It operates over a split supply with +VCC and -VEE.

Figure 2.26. A dc-coupled emitter follower with split supply.
image_name:Figure 2.26
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RB, type: Resistor, value: RB, ports: {N1: Vin, N2: GND}
name: Q1, type: NPN, ports: {C: +VCC, B: Vin, E: Vout}
name: RE, type: Resistor, value: RE, ports: {N1: Vout, N2: -VEE}
]
extrainfo:The circuit is a DC-coupled emitter follower with split supply, using an NPN transistor (Q1) and a resistor (RE) to provide biasing and stabilization. It operates over a split supply with +VCC and -VEE.

Figure 2.27. Always provide a dc bias path.

#### C. Bad biasing

You sometimes see sadness-inducing circuits like the disaster shown in Figure 2.28. The designer chose $R_{\mathrm{B}}$ by assuming a particular value for beta (100), estimating the base current, and then hoping for a 7 V drop across $R_{\mathrm{B}}$. This is a bad design; beta is not a good parameter and will vary considerably. By using voltage biasing with a stiff voltage divider, as in the detailed example presented earlier, the quiescent point is insensitive to variations in transistor beta. For instance, in the previous design example the emitter voltage will increase by only $0.35 \mathrm{~V}(5 \%)$ for a transistor with $\beta=200$ instead of the nominal $\beta=100$. And, as with this emitter follower example, it is just as easy to fall into this trap and design bad transistor circuits in the other transistor configurations (notably the common-emitter amplifier, which we will treat later in this chapter).
image_name:Figure 2.28
description:
[
name: RB, type: Resistor, value: 750k, ports: {N1: LOAD, N2: b}
name: RE, type: Resistor, value: 7.5k, ports: {N1: Vout, N2: GND}
name: C, type: Capacitor, value: C, ports: {Np: Vin, Nn: b}
name: Q1, type: NPN, ports: {C: +15V, B: b, E: Vout}
]
extrainfo:The circuit is an emitter follower configuration with an NPN transistor Q1. It is designed to buffer the input voltage Vin to the output Vout, with a load connected to the collector. The base of the transistor is biased through resistor RB. The emitter resistor RE helps stabilize the output voltage.

Figure 2.28. Don't do this!

#### D. Cancelling the offset -I

Wouldn't it be nice if an emitter follower did not cause an offset of the output signal by the $V_{\mathrm{BE}} \approx 0.6 \mathrm{~V}$ base-emitter drop? Figure 2.29 shows how to cancel the dc offset, by cascading a pnp follower (which has a positive $V_{\mathrm{BE}}$ offset) with an $n p n$ follower (which has a comparable negative $V_{\mathrm{BE}}$ offset). Here we've configured the circuit with $\pm 10 \mathrm{~V}$ symmetrical split supplies; and we've used equal-value emitter resistors so that the two transistors have a comparable quiescent current for an input signal near 0 V .

This is a nice trick, useful to know about and often helpful. But the cancellation isn't perfect, for reasons we'll see later in the chapter ( $V_{\mathrm{BE}}$ depends somewhat on collector current, and on transistor size, §2.3), and again in Chapter 5. But, as we'll see in Chapter 4, it is in fact rather easy to make a follower, using operational amplifiers, with nearly perfect zero offset ( $10 \mu \mathrm{~V}$ or less); and as a bonus you get input impedances in the gigaohms (or more), input currents in the nanoamps (or less), and output impedances
image_name:Figure 2.29
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: 10k, ports: {N1: LOAD1, N2: Vin}
name: Q1, type: PNP, ports: {C: Vin, B: in, E: LOAD2}
name: Q2, type: NPN, ports: {C: LOAD1, B: in, E: Vout}
name: R2, type: Resistor, value: 10k, ports: {N1: Vout, N2: LOAD2}
name: Vout, type: VoltageSource, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit consists of a PNP and an NPN transistor configured as followers to achieve approximate cancellation of V_BE offsets. It includes two 10k resistors and operates between +10V and -10V power supplies.

Figure 2.29. Cascading a pnp and an npn follower produces approximate cancellation of the $V_{\mathrm{BE}}$ offsets.
measured in fractions of an ohm. Take a look ahead at Chapter 4.

### 2.2.6 Current source

Current sources, although often neglected, are as important and as useful as voltage sources. They often provide an excellent way to bias transistors, and they are unequaled as "active loads" for super-gain amplifier stages and as emitter sources for differential amplifiers. Integrators, sawtooth generators, and ramp generators need current sources. They provide wide-voltage-range pullups within amplifier and regulator circuits. And, finally, there are applications in the outside world that require constant current sources, e.g., electrophoresis or electrochemistry.

#### A. Resistor plus voltage source

The simplest approximation to a current source is shown in Figure 2.30. As long as $R_{\text {load }} \ll R$ (in other words, $V_{\text {load }} \ll$ $V$ ), the current is nearly constant and is approximately

$$
I \approx V / R
$$

The load doesn't have to be resistive. A capacitor will charge at a constant rate, as long as $V_{\text {cap }} \ll V$; this is just the first part of the exponential charging curve of an $R C$.
image_name:Figure 2.30
description:
[
name: +V, type: VoltageSource, ports: {Np: +V, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: +V, N2: Vload}
name: Rload, type: Resistor, value: Rload, ports: {N1: Vload, N2: GND}
]
extrainfo:The circuit approximates a current source using a resistor and a voltage source. The current is nearly constant as long as Rload is much smaller than R.

Figure 2.30. Current-source approximation.
There are several drawbacks to a simple resistor current source. To make a good approximation to a current source, you must use large voltages, with lots of power dissipation in the resistor. In addition, the current isn't easily
programmable, i.e., controllable over a large range by means of a voltage somewhere else in the circuit.

Exercise 2.9. If you want a current source constant to $1 \%$ over a load voltage range of 0 to +10 volts, how large a voltage source must you use in series with a single resistor?

Exercise 2.10. Suppose you want a 10 mA current in the preceding problem. How much power is dissipated in the series resistor? How much gets to the load?

#### B. Transistor current source

Happily, it is possible to make a very good current source with a transistor (Figure 2.31). It works like this: applying $V_{\mathrm{B}}$ to the base, with $V_{\mathrm{B}}>0.6 \mathrm{~V}$, ensures that the emitter is always conducting:

$$
V_{\mathrm{E}}=V_{\mathrm{B}}-0.6 \text { volts. }
$$

So

$$
I_{\mathrm{E}}=V_{\mathrm{E}} / R_{\mathrm{E}}=\left(V_{\mathrm{B}}-0.6 \text { volts }\right) / R_{\mathrm{E}}
$$

But, since $I_{\mathrm{E}} \approx I_{\mathrm{C}}$ for large beta,

$$
\begin{equation*}
I_{\mathrm{C}} \approx\left(V_{\mathrm{B}}-0.6 \text { volts }\right) / R_{\mathrm{E}}, \tag{2.5}
\end{equation*}
$$

independent of $V_{C}$, as long as the transistor is not saturated ( $V_{\mathrm{C}} \gtrsim V_{\mathrm{E}}+0.2$ volts).
image_name:Figure 2.31
description:
[
name: Q1, type: NPN, ports: {C: C1, B: VB, E: e1}
name: RE, type: Resistor, value: RE, ports: {N1: e1, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: VCC, Nn: C1}
]
extrainfo:The circuit is a transistor current source with a bias voltage VB. The NPN transistor Q1 controls the current through the load, which is connected to the collector. The emitter is connected to the ground through resistor RE, setting the emitter current IE, which is approximately equal to the collector current IC for large beta. The capacitor C1 is connected across the load and VCC.

Figure 2.31. Transistor current source: basic concept.

#### C. Current-source biasing

The base voltage can be provided in a number of ways. A voltage divider is OK , as long as it is stiff enough. As before, the criterion is that its impedance should be much less than the dc impedance looking into the base ( $\beta R_{\mathrm{E}}$ ). Or you can use a zener diode (or a two-terminal IC reference like the LM385), biased from $V_{\mathrm{CC}}$, or even a few forward-
biased diodes ${ }^{19}$ in series from base to the corresponding emitter supply. Figure 2.32 shows some examples. In the last example (Figure 2.32C), a pnp transistor sources current to a load returned to ground. The other examples (using $n p n$ transistors) should properly be called current sinks, but the usual practice is to refer to them all loosely as "current sources." ${ }^{20}$ In the first circuit, the voltage-divider impedance of $\sim 1.3 \mathrm{k}$ is stiff compared with the impedance looking into the base of about 100 k (for $\beta=100$ ), so any changes in beta with collector voltage will not much affect the output current by causing the base voltage to change. In the other two circuits the biasing resistors are chosen to provide several milliamps to bring the diodes into conduction.

#### D. Compliance

A current source can provide constant current to the load only over some finite range of load voltage. To do otherwise would be equivalent to providing infinite power. The output voltage range over which a current source behaves well is called its output compliance. For the preceding transistor current sources, the compliance is set by the requirement that the transistors stay in the active region. Thus in the first circuit the voltage at the collector can go down until the transistor is almost in saturation, perhaps +1.1 V at the collector. The second circuit, with its higher emitter voltage, can sink current down to a collector voltage of about +5.1 V .

In all cases the collector voltage can range from a value near saturation all the way up to the supply voltage. For example, the last circuit can source current to the load for any voltage between zero and about +8.6 V across the load. In fact, the load might even contain batteries or power supplies of its own, which could carry the collector beyond the supply voltage (Figure 2.32A,B) or below ground (Figure 2.32 C ). That's OK, but you must watch out for transistor breakdown ( $V_{\mathrm{CE}}$ must not exceed $B V_{\mathrm{CEO}}$, the specified collector-emitter breakdown voltage) and also for excessive power dissipation (set by $I_{\mathrm{C}} V_{\mathrm{CE}}$ ). As you will see in $\S \S 3.5 .1 \mathrm{~B}, 3.6 .4 \mathrm{C}$, and 9.4 .2 , there is an additional safe-operating-area constraint on power transistors.
Exercise 2.11. You have +5 and +15 V regulated supplies available in a circuit. Design a 5 mA npn current sink using the +5 V to bias the base. What is the output compliance?

[^62]image_name:A
description:
[
name: Q1, type: NPN, ports: {C: LOAD1, B: b1, E: e1}
name: R1, type: Resistor, value: 8.2k, ports: {N1: LOAD1, N2: b1}
name: R2, type: Resistor, value: 1.6k, ports: {N1: b1, N2: GND}
name: R3, type: Resistor, value: 1.0k, ports: {N1: b1, N2: e1}
name: Q1, type: NPN, ports: {C: LOAD1, B: blk1, E: e1}
name: R4, type: Resistor, value: 10k, ports: {N1: LOAD1, N2: blk}
name: D1, type: Diode, ports: {Na: blk, Nc: GND}
name: R5, type: Resistor, value: 10k, ports: {N1: blk1, N2: e1}
name: Q1, type: PNP, ports: {C: c1, B: blk3, E: e1}
name: R6, type: Resistor, value: 560Ω, ports: {N1: c1, N2: e1}
name: R7, type: Resistor, value: 4.7k, ports: {N1: blk3, N2: GND}
name: D1, type: Diode, ports: {Na: LOAD1, Nc: k1a2}
name: D2, type: Diode, ports: {Na: k1a2, Nc: k2a3}
name: D3, type: Diode, ports: {Na: k2a3, Nc: blk3}
]
extrainfo:The circuit diagram illustrates three different transistor current-source circuits, each employing an NPN transistor for current sinking. Circuit A utilizes a simple resistor divider biasing method, Circuit B incorporates a Zener diode for a fixed bias voltage, and Circuit C uses a series of diodes for biasing. Each circuit is designed to maintain a specific current through the load with varying biasing techniques.
image_name:B
description:
[
name: Q1, type: NPN, ports: {C: LOAD1, B: b1k1, E: e1}
name: D1, type: Diode, ports: {Na: b1k, Nc: GND}
name: 10k, type: Resistor, value: 10k, ports: {N1: LOAD1, N2: b1k}
name: 10k, type: Resistor, value: 10k, ports: {N1: e1, N2: GND}
]
extrainfo:Circuit B is a current sink using an NPN transistor Q1. The base of Q1 is biased at 5.6V using a zener diode D1. The load is connected to +15V, and the emitter of Q1 is connected to ground through a 10k resistor. The circuit sinks 0.5mA of current through the load.
image_name:C
description:
[
name: Q1, type: NPN, ports: {C: LOAD1, B: bk3, E: e1}
name: D1, type: Diode, ports: {Na: LOAD1, Nc: bk3}
name: D2, type: Diode, ports: {Na: k1a2, Nc: k2c3}
name: D3, type: Diode, ports: {Na: k2c3, Nc: bk3}
name: R6, type: Resistor, value: 560, ports: {N1: LOAD1, N2: e1}
name: R7, type: Resistor, value: 4.7k, ports: {N1: bk3, N2: GND}
]
extrainfo:This circuit is a current sink using an NPN transistor (Q1) with diodes (D1, D2, D3) to set the bias voltage. The load is connected between the collector of Q1 and the supply voltage (+10V). The circuit sinks a current of 2mA through the load.

Figure 2.32. Transistor current-source circuits, illustrating three methods of base biasing; npn transistors sink current, whereas pnp transistors source current. The circuit in C illustrates a load returned to ground. See also Figure 3.26.

A current source doesn't have to have a fixed voltage at the base. By varying $V_{\mathrm{B}}$ you get a voltage-programmable current source. The input signal swing $v_{\text {in }}$ (recall that lowercase symbols mean variations) must stay small enough so that the emitter voltage never drops to zero, if the output current is to reflect input-voltage variations smoothly. The result will be a current source with variations in output current proportional to the variations in input voltage, $i_{\text {out }}=v_{\text {in }} / R_{\mathrm{E}}$. This is the basis of the amplifier we'll see next (§2.2.7).

#### E. Cancelling the offset - II

It's a minor drawback of these current source circuits that you have to apply a base voltage that is offset by $V_{\mathrm{BE}} \approx$ 0.6 V from the voltage that you want to appear across the emitter resistor; and it is of course the latter that sets the output current. It's the same offset issue as with an emitter follower; and you can use the same trick (§2.2.5D) to bring about approximate cancellation of the offset in situations in which that is a problem.
image_name:Figure 2.33
description:
[
name: R1, type: Resistor, value: 10k, ports: {N1: Vin, N2: e1b2}
name: R2, type: Resistor, value: 1k, ports: {N1: e2, N2: GND}
name: Q1, type: NPN, ports: {C: e1b2, B: Vin, E: GND}
name: Q2, type: PNP, ports: {C: LOAD, B: e1b2, E: e2}
]
extrainfo:The circuit is a current source with compensation for the V_BE drop, using a PNP transistor Q2 to set the output current based on the voltage across the emitter resistor R2. The NPN transistor Q1 acts as an input follower to match the base voltage of Q2.

Figure 2.33. Compensating the $V_{\mathrm{BE}}$ drop in a current source.
Look at Figure 2.33. It has our standard current-source output stage $Q_{2}$, with the current set by the voltage across the emitter resistor: $I_{L}=V_{\mathrm{E}} / R_{2}$. So $Q_{2}$ 's base needs to be
a $V_{\mathrm{BE}}$ higher (the offset), but that's just what the pnp input follower does anyway. So, voilà, the voltage at $Q_{2}$ 's emitter winds up being approximately equal to $V_{\text {in }}$ that you apply; and so the output current is simply $I_{\mathrm{L}}=V_{\text {in }} / R_{2}$, with no ifs, ands, buts, or $V_{\mathrm{BE}}$ offsets. Cute!

We hasten to point out, though, that this is not a particularly accurate cancellation, because the two transistors will in general have different collector currents, and therefore somewhat different base-emitter drops (§2.3). But it's a first-order hack, and a lot better than nothing. And, once again, the magic of operational amplifiers (Chapter 4) will provide a way to make current sources in which the output current is accurately programmed by an input voltage, without that pesky $V_{\mathrm{BE}}$ offset.

#### F. Deficiencies of current sources

These transistor current-source circuits perform well, particularly when compared with a simple resistor biased from a fixed voltage (Figure 2.30). When you look closely, though, you find that they do depart from the ideal at some level of scrutiny - that is, the load current does show some (relatively small) variation with voltage. Another way to say the same thing is that the current source has a finite $\left(R_{\mathrm{Th}}<\infty\right)$ Thévenin equivalent resistance.

We discuss the causes of these deficiencies, and some very clever circuit fixes, later in the chapter, and also in Chapter 2x.

### 2.2.7 Common-emitter amplifier

Consider a current source with a resistor as load (Figure 2.34). The collector voltage is

$$
V_{\mathrm{C}}=V_{\mathrm{CC}}-I_{\mathrm{C}} R_{\mathrm{C}}
$$

We could capacitively couple a signal to the base to cause the collector voltage to vary. Consider the example in
image_name:Figure 2.34
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: b1, N2: VCC}
name: R2, type: Resistor, value: R2, ports: {N1: b1, N2: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: c1}
name: RE, type: Resistor, value: RE, ports: {N1: e1, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: c1, Nn: Vout}
name: Q1, type: NPN, ports: {C: c1, B: b1, E: e1}
]
extrainfo:This is a common-emitter amplifier circuit. The transistor Q1 is used to amplify the input signal. R1 and R2 form a voltage divider to bias the base of the transistor. RC is the collector resistor, and RE is the emitter resistor. C1 is a coupling capacitor that allows AC signals to pass while blocking DC.

Figure 2.34. Current source driving a resistor as load: an amplifier!

Figure 2.35 . Blocking capacitor $C$ is chosen so that all frequencies of interest are passed by the highpass filter it forms in combination with the parallel resistance of the base biasing resistors ${ }^{21}$; that is,

$$
C \geq \frac{1}{2 \pi f\left(R_{1} \| R_{2}\right)}
$$

The quiescent collector current is 1.0 mA because of the applied base bias and the 1.0 k emitter resistor. That current puts the collector at +10 volts $(+20 \mathrm{~V}$, minus 1.0 mA through 10k). Now imagine an applied wiggle in base voltage $v_{\mathrm{B}}$. The emitter follows with $v_{\mathrm{E}}=v_{\mathrm{B}}$, which causes a wiggle in emitter current

$$
i_{\mathrm{E}}=v_{\mathrm{E}} / R_{\mathrm{E}}=v_{\mathrm{B}} / R_{\mathrm{E}}
$$

and nearly the same change in collector current ( $\beta$ is large). So the initial wiggle in base voltage finally causes a collector voltage wiggle

$$
v_{\mathrm{C}}=-i_{\mathrm{C}} R_{\mathrm{C}}=-v_{\mathrm{B}}\left(R_{\mathrm{C}} / R_{\mathrm{E}}\right)
$$

Aha! It's a voltage amplifier, with a voltage amplification (or "gain") given by

$$
\begin{equation*}
\text { gain }=v_{\text {out }} / v_{\mathrm{in}}=-R_{\mathrm{C}} / R_{\mathrm{E}} \tag{2.6}
\end{equation*}
$$

In this case the gain is $-10,000 / 1000$, or -10 . The minus sign means that a positive wiggle at the input gets turned into a negative wiggle (10 times as large) at the output. This is called a common-emitter amplifier with emitter degeneration.

#### A. Input and output impedances of the common-emitter amplifier

We can easily determine the input and output impedances of the amplifier. The input signal sees, in parallel, 110k, 10 k , and the impedance looking into the base. The latter is

[^63]image_name:Figure 2.35
description:
[
name: R1, type: Resistor, value: 110k, ports: {N1: LOAD, N2: b1}
name: R2, type: Resistor, value: 10k, ports: {N1: b1, N2: GND}
name: RC, type: Resistor, value: 10k, ports: {N1: Vout, N2: +20V}
name: RE, type: Resistor, value: 1.0k, ports: {N1: e1, N2: GND}
name: C, type: Capacitor, value: 0.1μF, ports: {Np: Vin, Nn: b1}
name: Q1, type: NPN, ports: {C: Vout, B: b1, E: e1}
]
extrainfo:The circuit is a common-emitter amplifier with emitter degeneration. The input is at Vin, and the output is at Vout. The amplifier provides a gain of -10. The input impedance is approximately 8k ohms, and the output impedance is determined by RC. The circuit operates with a supply voltage of +20V.

Figure 2.35. An ac common-emitter amplifier with emitter degeneration. Note that the output terminal is the collector rather than the emitter.
about 100 k ( $\beta$ times $R_{\mathrm{E}}$ ), so the input impedance (dominated by the 10 k ) is about 8 k . The input coupling capacitor thus forms a highpass filter, with the 3 dB point at 200 Hz . The signal driving the amplifier sees $0.1 \mu \mathrm{~F}$ in series with 8 k , which to signals of normal frequencies (well above the 3 dB point) just looks like 8 k .

The output impedance is 10 k in parallel with the impedance looking into the collector. What is that? Well, remember that if you snip off the collector resistor, you're simply looking into a current source. The collector impedance is very large (measured in megohms), and so the output impedance is just the value of the collector resistor, 10k. It is worth remembering that the impedance looking into a transistor's collector is high, whereas the impedance looking into the emitter is low (as in the emitter follower). Although the output impedance of a commonemitter amplifier will be dominated by the collector load resistor, the output impedance of an emitter follower will not be dominated by the emitter load resistor, but rather by the impedance looking into the emitter.

### 2.2.8 Unity-gain phase splitter

Sometimes it is useful to generate a signal and its inverse, i.e., two signals $180^{\circ}$ out of phase. That's easy to do - just use an emitter-degenerated amplifier with a gain of -1 (Figure 2.36). The quiescent collector voltage is set to $0.75 V_{\mathrm{CC}}$, rather than the usual $0.5 V_{\mathrm{CC}}$, in order to achieve the same result - maximum symmetrical output swing without clipping at either output. The collector can swing from $0.5 V_{\mathrm{CC}}$ to $V_{\mathrm{CC}}$, whereas the emitter can swing from ground to $0.5 V_{\mathrm{CC}}$.

Note that the phase-splitter outputs must be loaded with equal (or very high) impedances at the two outputs to maintain gain symmetry.
image_name:Figure 2.36. Unity-gain phase splitter
description:
[
name: C, type: Capacitor, value: C, ports: {Np: Vin, Nn: b1}
name: Q1, type: NPN, ports: {C: φ2, B: b1, E: φ1}
name: LOAD, type: Resistor, value: LOAD, ports: {N1: LOAD, N2: φ2}
name: 150k, type: Resistor, value: 150k, ports: {N1: Vin, N2: b1}
name: 62k, type: Resistor, value: 62k, ports: {N1: b1, N2: GND}
name: 4.99k 1%, type: Resistor, value: 4.99k 1%, ports: {N1: φ2, N2: +20V}
name: 4.99k 1%, type: Resistor, value: 4.99k 1%, ports: {N1: φ1, N2: GND}
]
extrainfo:The circuit is a unity-gain phase splitter designed to provide maximum symmetrical output swing without clipping. The quiescent collector voltage is set to 0.75 V_CC to achieve this. The phase-splitter outputs must be loaded with equal or very high impedances to maintain gain symmetry.

Figure 2.36. Unity-gain phase splitter.
image_name:Figure 2.37. Constant-amplitude phase shifter
description:
[
name: C, type: Capacitor, value: C, ports: {Np: φ2, Nn: Vo}
name: R, type: Resistor, value: R, ports: {N1: Vo, N2: φ1}
]
extrainfo:The circuit is a constant-amplitude phase shifter. It provides an output sinewave of adjustable phase (from zero to 180 degrees) with constant amplitude. The phase shift is determined by the formula θ = 2 tan⁻¹(ωRC).

Figure 2.37. Constant-amplitude phase shifter.

#### A. Phase shifter

A nice use of the phase splitter is shown in Figure 2.37. This circuit gives (for a sinewave input) an output sinewave of adjustable phase (from zero to $180^{\circ}$ ) and with constant amplitude. It can be best understood with a phasor diagram of voltages (§1.7.12); with the input signal represented by a unit vector along the real axis, the signals look as shown in Figure 2.38.

Signal vectors $\mathbf{v}_{\mathrm{R}}$ and $\mathbf{v}_{\mathrm{C}}$ must be at right angles, and they must add to form a vector of constant length along the real axis. There is a theorem from geometry that says that the locus of such points is a circle. So the resultant vector (the output voltage) always has unit length, i.e., the same amplitude as the input, and its phase can vary from nearly zero to nearly $180^{\circ}$ relative to the input wave as $R$ is varied from nearly zero to a value much larger than $X_{\mathrm{C}}$ at the operating frequency. However, note that the phase shift depends on the frequency of the input signal for a given setting of the potentiometer $R$. It is worth noting that a simple $R C$ highpass (or lowpass) network could also be used as an adjustable phase shifter. However, its output amplitude would vary over an enormous range as the phase shift was adjusted.

An additional concern here is the ability of the phasesplitter circuit to drive the $R C$ phase shifter as a load. Ideally, the load should present an impedance that is large
compared with the collector and emitter resistors. As a result, this circuit is of limited utility where a wide range of phase shifts is required. You will see improved phasesplitter techniques in Chapter 4, where we use op-amps as impedance buffers, and in Chapter 7, where a cascade of several phase-shifter sections generates a set of "quadrature" signals that extends the phase-shifting range to a full $0^{\circ}$ to $360^{\circ}$.
image_name:Figure 2.38
description:Figure 2.38 is a phasor diagram illustrating the phase relationship in a phase shifter circuit. The diagram represents the vector sum of voltages across different components in the circuit.

1. **Type of Graph and Function:**
- This is a phasor diagram, which is used to represent the magnitude and phase relationship between sinusoidal functions in AC circuits.

2. **Axes Labels and Units:**
- The axes are not explicitly labeled with units, as phasor diagrams typically use a generic reference for voltage (V) without specific units on the axes. The horizontal axis represents the real part of the voltage, and the vertical axis represents the imaginary part.

3. **Overall Behavior and Trends:**
- The diagram shows a circular arrangement, indicating a phase shift. The vectors are drawn from the origin, representing different voltages in the circuit. The angle \( \theta \) is the phase shift introduced by the circuit.
- \( v_C \) is the voltage across the capacitor, \( v_R \) is the voltage across the resistor, and \( v_{out} \) is the output voltage, which is the vector sum of \( v_C \) and \( v_R \).

4. **Key Features and Technical Details:**
- The angle \( \theta \) between \( v_R \) and \( v_{out} \) is shown, which is calculated as \( \theta = 2 \arctan(\omega RC) \), where \( \omega \) is the angular frequency, \( R \) is the resistance, and \( C \) is the capacitance.
- The vectors form a right triangle, with the hypotenuse being \( v_{out} \), illustrating the phase shift between input and output voltages.

5. **Annotations and Specific Data Points:**
- The diagram includes annotations for \( v_C \), \( v_R \), \( v_{out} \), and the angle \( \theta \), providing a clear visual representation of the phase relationships in the circuit.

Figure 2.38. Phasor diagram for phase shifter, for which $\theta=$ $2 \arctan (\omega R C)$.
image_name:Figure 2.39
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: b1, E: e1}
name: 110k, type: Resistor, value: 110k, ports: {N1: LOAD, N2: b1}
name: 10k, type: Resistor, value: 10k, ports: {N1: b1, N2: GND}
name: 0.1uF, type: Capacitor, value: 0.1uF, ports: {Np: Vin, Nn: b1}
name: 1.0k, type: Resistor, value: 1.0k, ports: {N1: e1, N2: GND}
name: 10k, type: Resistor, value: 10k, ports: {N1: Vout, N2: +20V}
]
extrainfo:The circuit is a common-emitter amplifier with a transconductance stage driving a resistive load. It includes biasing for the transistor Q1 with a 1.6V at the base and 1.0V at the emitter. The output is taken across a 10k resistor connected to +20V.

Figure 2.39. The common-emitter amplifier is a transconductance stage driving a (resistive) load.

### 2.2.9 Transconductance

In the preceding section we figured out the operation of the emitter-degenerated amplifier by (a) imagining an applied base voltage swing and seeing that the emitter voltage had the same swing, then (b) calculating the emitter current swing; then, ignoring the small base current contribution, we got the collector current swing and thus (c) the collector voltage swing. The voltage gain was then simply the ratio of collector (output) voltage swing to base (input) voltage swing.

There's another way to think about this kind of amplifier. Imagine breaking it apart, as in Figure 2.39. The first
part is a voltage-controlled current source, with quiescent current of 1.0 mA and gain of $-1 \mathrm{~mA} / \mathrm{V}$. Gain means the ratio of output to input; in this case the gain has units of current/voltage, or 1/resistance. The inverse of resistance is called conductance. ${ }^{22}$ An amplifier whose gain has units of conductance is called a transconductance amplifier; the ratio of changes $\Delta I_{\text {out }} / \Delta V_{\text {in }}$ (usually written with smallsignal changes indicated in lowercase: $i_{\text {out }} / v_{\text {in }}$ ) is called the transconductance, $g_{m}$ :

$$
\begin{equation*}
g_{m}=\frac{\Delta I_{\text {out }}}{\Delta V_{\text {in }}}=\frac{i_{\text {out }}}{v_{\text {in }}} . \tag{2.7}
\end{equation*}
$$

Think of the first part of the circuit as a transconductance amplifier, i.e., a voltage-to-current amplifier with transconductance $g_{m}$ (gain) of $-1 \mathrm{~mA} / \mathrm{V}(1000 \mu \mathrm{~S}$, or 1 mS , which is just $1 / R_{\mathrm{E}}$ ). The second part of the circuit is the load resistor, an "amplifier" that converts current to voltage. This resistor could be called a transresistance converter, and its gain $\left(r_{m}\right)$ has units of voltage/current, or resistance. In this case its quiescent voltage is $V_{\mathrm{CC}}$, and its gain (transresistance) is $10 \mathrm{~V} / \mathrm{mA}$ ( $10 \mathrm{k} \Omega$ ), which is just $R_{\mathrm{C}}$. Connecting the two parts together gives you a voltage amplifier. You get the overall gain by multiplying the two gains. In this case the voltage gain $G_{V}=g_{m} R_{\mathrm{C}}=-R_{\mathrm{C}} / R_{\mathrm{E}}$, or -10 , a unitless number equal to the ratio (output voltage change)/(input voltage change).

This is a useful way to think about an amplifier, because you can analyze performance of the sections independently. For example, you can analyze the transconductance part of the amplifier by evaluating $g_{m}$ for different circuit configurations or even different devices, such as field-effect transistors FETs. Then you can analyze the transresistance (or load) part by considering gain versus voltage swing tradeoffs. If you are interested in the overall voltage gain, it is given by $G_{\mathrm{V}}=g_{m} r_{m}$, where $r_{m}$ is the transresistance of the load. Ultimately the substitution of an active load (current source), with its extremely high transresistance, can yield single-stage voltage gains of 10,000 or more. The cascode configuration, which we will discuss later, is another example easily understood with this approach.

In Chapter 4, which deals with operational amplifiers, you will see further examples of amplifiers with voltages or currents as inputs or outputs: voltage amplifiers (voltage to voltage), current amplifiers (current to current), and transresistance amplifiers (current to voltage).

[^64]
#### A. Turning up the gain: limitations of the simple model

The voltage gain of the emitter-degenerated amplifier is $-R_{\mathrm{C}} / R_{\mathrm{E}}$, according to our model. What happens as $R_{\mathrm{E}}$ is reduced toward zero? The equation predicts that the gain will rise without limit. But if we made actual measurements of the preceding circuit, keeping the quiescent current constant at 1 mA , we would find that the gain would level off at about 400 when $R_{\mathrm{E}}$ is zero, i.e., with the emitter grounded. We would also find that the amplifier would become significantly nonlinear (the output would not be a faithful replica of the input), the input impedance would become small and nonlinear, and the biasing would become critical and unstable with temperature. Clearly our transistor model is incomplete and needs to be modified to handle this circuit situation, as well as others we will talk about presently. Our fixed-up model, which we will call the transconductance model, will be accurate enough for the remainder of the book.

#### B. Recap: the "four topologies"

Before jumping into the complexity just ahead, let's remind ourselves of the four transistor circuits we've seen, namely the switch, emitter follower, current source, and commonemitter amplifier. We've drawn these very schematically in Figure 2.40, omitting details like biasing, and even the polarity of transistor (i.e., $n p n$ or $p n p$ ). For completeness we've included also a fifth circuit, the common-base amplifier, which we'll meet soon enough (§2.4.5B).

## 2.3 Ebers-Moll model applied to basic transistor circuits

We've enjoyed seeing some nice feats that can be accomplished with the simplest BJT model - switch, follower, current source, amplifier - but we've run up against some serious limitations (hey, would you believe, infinite gain?!). Now it's time to go a level deeper, to address these limitations. The material that follows will suffice for our purposes. And - good news - for many BJT applications the simple model you've already seen is completely adequate.

### 2.3.1 Improved transistor model: transconductance amplifier

The important change is in rule 4 (\$2.1.1), where we said earlier that $I_{\mathrm{C}}=\beta I_{\mathrm{B}}$. We thought of the transistor as a current amplifier whose input circuit behaved like a diode. That's roughly correct, and for some applications it's good enough. But to understand differential amplifiers,
image_name:emitter follower
description:
[
name: Emitter Follower, type: NPN, ports: {C: Vout, B: Vin, E: GND}
]
extrainfo:The circuit diagram represents an emitter follower configuration using an NPN transistor. The base is connected to the input, the collector is connected to the output, and the emitter is grounded. This configuration is commonly used for impedance matching and buffering applications.
image_name:switch
description:
[
name: Switch, type: NPN, ports: {C: OUT, B: IN, E: GND}
name: Load, type: Resistor, ports: {N1: OUT, N2: VDD}
]
extrainfo:The circuit named 'switch' includes an NPN transistor acting as a switch and a load resistor connected to the collector. The emitter is grounded, and the base is connected to the input node. The load is connected between the collector and VDD.
image_name:current source
description:
[
name: Current Source, type: NPN, ports: {C: OUT, B: IN, E: GND}
]
extrainfo:The circuit diagram represents a basic NPN current source configuration. The collector is connected to the output node, the base is connected to the input node, and the emitter is grounded. This configuration is used to provide a constant current to a load connected at the output.
image_name:common-emitter amplifier
description:
[
name: Common-Emitter Amplifier, type: NPN, ports: {C: VDD, B: Vin, E: GND}
]
extrainfo:The common-emitter amplifier is a basic transistor circuit with the collector connected to VDD, the base to the input (Vin), and the emitter to ground (GND). It is used to amplify voltage.
image_name:common-base amplifier
description:
[
name: Common-Base Amplifier, type: NPN, ports: {C: OUT, B: IN, E: GND}
]
extrainfo:The circuit diagram represents a common-base amplifier using an NPN transistor. The collector is connected to the output, the base is connected to the input, and the emitter is grounded.

Figure 2.40. Five basic transistor circuits. Fixed voltages (power supplies or ground) are indicated by connections to horizontal line segments. For the switch, the load may be a resistor, to produce a full-swing voltage output; for the common-emitter amplifier, the emitter resistor may be bypassed or omitted altogether.
logarithmic converters, temperature compensation, and other important applications, you must think of the transistor as a transconductance device - collector current is determined by base-to-emitter voltage.

Here's the modified rule 4.
4. Transconductance amplifier When rules 1-3 (§2.1.1) are obeyed, $I_{\mathrm{C}}$ is related to $V_{\mathrm{BE}}$ by ${ }^{23}$

$$
\begin{equation*}
I_{\mathrm{C}}=I_{\mathrm{S}}(T)\left(e^{V_{\mathrm{BE}} / V_{\mathrm{T}}}-1\right) \tag{2.8}
\end{equation*}
$$

or, equivalently,

$$
\begin{equation*}
V_{\mathrm{BE}}=\frac{k T}{q} \log _{e}\left(\frac{I_{\mathrm{C}}}{I_{\mathrm{S}}(T)}+1\right), \tag{2.9}
\end{equation*}
$$

where

$$
\begin{equation*}
V_{\mathrm{T}}=k T / q=25.3 \mathrm{mV} \tag{2.10}
\end{equation*}
$$

at room temperature $\left(68^{\circ} \mathrm{F}, 20^{\circ} \mathrm{C}\right), q$ is the electron charge ( $1.60 \times 10^{-19}$ coulombs), $k$ is Boltzmann's constant $\left(1.38 \times 10^{-23}\right.$ joules/K, sometimes written $\left.k_{\mathrm{B}}\right), T$ is the absolute temperature in degrees Kelvin $\left(\mathrm{K}={ }^{\circ} \mathrm{C}+273.16\right)$, and $I_{\mathrm{S}}(T)$ is the saturation current of the particular transistor (which depends strongly on temperature, $T$, as we'll see shortly). Then the base current, which also depends on $V_{\mathrm{BE}}$, can be approximated by

$$
I_{\mathrm{B}}=I_{\mathrm{C}} / \beta,
$$

where the "constant" $\beta$ is typically in the range 20 to 1000, but depends on transistor type, $I_{\mathrm{C}}, V_{\mathrm{CE}}$, and temperature. $I_{S}(T)$ approximates the reverse leakage current (roughly $10^{-15} \mathrm{~A}$ for a small-signal transistor like the 2 N 3904 ). In the active region $I_{\mathrm{C}} \gg I_{S}$, and therefore

[^65]the -1 term can be neglected in comparison with the exponential:
\$\$

$$
\begin{equation*}
I_{\mathrm{C}} \approx I_{\mathrm{S}}(T) e^{V_{\mathrm{BE}} / V_{\mathrm{T}}} \tag{2.11}
\end{equation*}
$$

\$\$

The equation for $I_{\mathrm{C}}$ is known as the Ebers-Moll equation. ${ }^{24}$ It also describes approximately the current versus voltage for a diode, if $V_{\mathrm{T}}$ is multiplied by a correction factor $m$ between 1 and 2. For transistors it is important to realize that the collector current is accurately determined by the base-emitter voltage, rather than by the base current (the base current is then roughly determined by $\beta$ ), and that this exponential law is accurate over an enormous range of currents, typically from nanoamps to milliamps. Figure 2.41 makes the point graphically. ${ }^{25}$ If you measure the base current at various collector currents, you will get a graph of $\beta$ versus $I_{C}$ like that in Figure 2.42. Transistor beta versus collector current is discussed further in Chapter $2 x$.

Although the Ebers-Moll equation tells us that the base-emitter voltage "programs" the collector current, this property is not easy to use in practice (biasing a transistor by applying a base voltage) because of the large temperature coefficient of base-emitter voltage. You will see later how the Ebers-Moll equation provides insight and solutions to this problem.

### 2.3.2 Consequences of the Ebers-Moll model: rules of thumb for transistor design

From the Ebers-Moll equation (2.8) we get these simple (but handy) "ratio rules" for collector current: $I_{\mathrm{C} 2} / I_{\mathrm{C} 1}=\exp \left(\Delta V_{\mathrm{BE}} / V_{\mathrm{T}}\right)$ and $\Delta V_{\mathrm{BE}}=V_{\mathrm{T}} \log _{e}\left(I_{\mathrm{C} 2} / I_{\mathrm{C} 1}\right) . \mathrm{We}$

[^66]image_name:Figure 2.41
description:**Type of Graph and Function:** The graph is a logarithmic plot depicting the relationship between the base-to-emitter voltage \( V_{BE} \) and the collector current \( I_C \) and base current \( I_B \) in a transistor.

**Axes Labels and Units:**
- The x-axis represents the base-to-emitter voltage \( V_{BE} \) in volts, ranging from 0.1 to 0.8 volts.
- The y-axis represents the collector current \( I_C \) in amperes, displayed on a logarithmic scale, ranging from \( 10^{-10} \) to \( 10^{-3} \) amperes.

**Overall Behavior and Trends:**
- The graph shows two distinct linear trends on a logarithmic scale. The collector current \( I_C \) increases exponentially with \( V_{BE} \), reflecting the exponential relationship described by the Ebers-Moll equation.
- The base current \( I_B \) also increases with \( V_{BE} \) but at a lower rate than \( I_C \), indicating its dependence on \( I_C \) and the transistor's current gain \( h_{FE} \).

**Key Features and Technical Details:**
- The plot includes a line labeled \( I_C \), which shows a steeper slope compared to the line labeled \( I_B \), indicating a higher rate of increase for the collector current with respect to \( V_{BE} \).
- The equation \( V_{BE} = \frac{kT}{q} \ln \left( \frac{I_C}{I_S} + 1 \right) \) is annotated on the graph, representing the theoretical relationship between \( V_{BE} \) and \( I_C \).
- The line representing \( I_B \) is labeled as "recombination current," and it follows the equation \( I_B = \frac{I_C}{h_{FE}} \), where \( h_{FE} \) is the transistor's current gain.

**Annotations and Specific Data Points:**
- The graph includes annotations for the equation and the relationship between \( I_B \) and \( I_C \), providing insights into the behavior of transistor currents as functions of \( V_{BE} \).
- The logarithmic scale on the y-axis emphasizes the exponential nature of the current increase with voltage.

Figure 2.41. Transistor base and collector currents as functions of base-to-emitter voltage $V_{\mathrm{BE}}$.
image_name:Figure 2.42
description:The graph labeled as "Figure 2.42" illustrates the relationship between transistor current gain (denoted as \( \beta \)) and collector current (\( I_C \)) using a logarithmic scale on both axes. The x-axis represents the collector current \( I_C \) in amperes, ranging from \( 10^{-8} \) to \( 10^{-2} \) amps, while the y-axis represents the current gain \( \beta \), ranging from 100 to 1000.

**Type of Graph and Function:**
This is a logarithmic plot showing the variation of a transistor's current gain with respect to its collector current.

**Axes Labels and Units:**
- **X-axis:** \( I_C \) (amps, log scale)
- **Y-axis:** \( \beta \) (log scale)

**Overall Behavior and Trends:**
The graph shows a bell-shaped curve indicating that the current gain \( \beta \) initially increases with an increase in \( I_C \), reaches a peak, and then begins to decrease as \( I_C \) continues to increase. This suggests that there is an optimal range of collector current where the transistor's current gain is maximized.

**Key Features and Technical Details:**
- The peak of the curve occurs approximately around \( I_C = 10^{-5} \) to \( 10^{-4} \) amps where \( \beta \) reaches its maximum value.
- The curve is symmetric around its peak, indicating a balanced increase and decrease of \( \beta \) with changes in \( I_C \).

**Annotations and Specific Data Points:**
- The logarithmic scale on both axes emphasizes the exponential relationship between \( \beta \) and \( I_C \).
- No specific numerical values or data points are annotated on the graph, but the general trend is clear from the curve's shape.

Figure 2.42. Typical transistor current gain $(\beta)$ versus collector current.
also get the following important quantities we will be using often in circuit design.

#### A. The steepness of the diode curve.

How much do we need to increase $V_{\mathrm{BE}}$ to increase $I_{\mathrm{C}}$ by a factor of 10 ? From the Ebers-Moll equation, that's just $V_{\mathrm{T}} \log _{e} 10$, or 58.2 mV at room temperature. We like to remember this as base-emitter voltage increases approximately 60 mV per decade of collector current. (Two other formulations: collector current doubles for each 18 mV increase in base-emitter voltage; collector current increases $4 \%$ per millivolt increase in base-emitter voltage.) Equivalently, $I_{\mathrm{C}}=I_{C 0} e^{\Delta V / 25}$, where $\Delta V$ is in millivolts. ${ }^{26}$

[^67]
#### B. The small-signal impedance looking into the emitter, $r_{\mathrm{e}}$, for the base held at a fixed voltage.

Taking the derivative of $V_{\mathrm{BE}}$ with respect to $I_{\mathrm{C}}$, you get

$$
\begin{equation*}
r_{\mathrm{e}}=V_{T} / I_{\mathrm{C}}=25 / I_{\mathrm{C}} \text { ohms, } \tag{2.12}
\end{equation*}
$$

where $I_{\mathrm{C}}$ is in milliamps. ${ }^{27}$ The numerical value $25 / I_{\mathrm{C}}$ is for room temperature. This intrinsic emitter resistance, $r_{\mathrm{e}}$, acts as if it is in series with the emitter in all transistor circuits. It limits the gain of a grounded-emitter amplifier, causes an emitter follower to have a voltage gain of slightly less than unity, and prevents the output impedance of an emitter follower from reaching zero. Note that the transconductance ${ }^{28}$ of a grounded emitter amplifier is just

$$
\begin{equation*}
g_{m}=I_{\mathrm{C}} / V_{\mathrm{T}}=1 / r_{\mathrm{e}}\left(=40 I_{\mathrm{C}} \text { at room temp }\right) \tag{2.13}
\end{equation*}
$$

#### C. The temperature dependence of $V_{\mathrm{BE}}$.

A glance at the Ebers-Moll equation suggests that $V_{\mathrm{BE}}$ (at constant $I_{\mathrm{C}}$ ) has a positive temperature coefficient because of the multiplying factor of $T$ in $V_{\mathrm{T}}$. However, the strong temperature dependence of $I_{\mathrm{S}}(T)$ more than compensates for that term, such that $V_{\mathrm{BE}}$ (at constant $I_{\mathrm{C}}$ ) decreases about $2.1 \mathrm{mV} /{ }^{\circ} \mathrm{C}$. It is roughly proportional to $1 / T_{\mathrm{abs}}$, where $T_{\mathrm{abs}}$ is the absolute temperature. Sometimes it's useful to cast this instead in terms of the temperature dependence of $I_{\mathrm{C}}$ (at constant $V_{\mathrm{BE}}$ ): I Increases about $9 \% /{ }^{\circ} \mathrm{C}$; it doubles for an $8^{\circ} \mathrm{C}$ rise.

There is one additional quantity we will need on occasion, although it is not derivable from the Ebers-Moll equation. It is known as the Early effect, ${ }^{29}$ and it sets important limits on current-source and amplifier performance.

#### D. Early effect.

$V_{\mathrm{BE}}$ (at constant $I_{\mathrm{C}}$ ) varies slightly with changing $V_{\mathrm{CE}}$. This effect is caused by the variation of effective base width as $V_{\mathrm{CE}}$ changes, and it is given, approximately, by

$$
\begin{equation*}
\Delta V_{\mathrm{BE}}=-\eta \Delta V_{\mathrm{CE}} \tag{2.14}
\end{equation*}
$$

where $\eta \approx 10^{-4}-10^{-5}$. (As an example, the npn 2N5088 has $\eta=1.3 \times 10^{-4}$, thus a 1.3 mV change of $V_{\mathrm{BE}}$ to maintain constant collector current when $V_{\mathrm{CE}}$ changes by 10 V .)
opportunity to make a "silicon thermometer." We'll see more of this in Chapter 2x, and again in Chapter 9.
27 We like to remember the fact that $r_{\mathrm{e}}=25 \Omega$ at a collector current of 1 mA . Then we just scale inversely for other currents: thus $r_{\mathrm{e}}=2.5 \Omega$ at $I_{\mathrm{C}}=10 \mathrm{~mA}$, etc.
${ }^{28}$ At the next level of sophistication we'll see that, since the quantity $r_{\mathrm{e}}$ is proportional to absolute temperature, a grounded emitter amplifier whose collector current is PTAT has transconductance (and gain) independent of temperature. More in Chapter $2 x$.
29 J. M. Early, "Effects of space-charge layer widening in junction transistors," Proc. IRE 40, 1401 (1952). James Early died in 2004.

This is often described instead as a linear increase of collector current with increasing collector voltage when $V_{\mathrm{BE}}$ is held constant; you see it expressed as

$$
\begin{equation*}
I_{\mathrm{C}}=I_{\mathrm{C} 0}\left(1+\frac{V_{\mathrm{CE}}}{V_{\mathrm{A}}}\right) \tag{2.15}
\end{equation*}
$$

where $V_{\mathrm{A}}$ (typically $50-500 \mathrm{~V}$ ) is known as the Early voltage. ${ }^{30}$ This is shown graphically in Figure 2.59 in $\S 2.3 .7 \mathrm{~A}$. A low Early voltage indicates a low collector output resistance; pnp transistors tend to have low $V_{\mathrm{A}}$, see measured values in Table 8.1. We treat the Early effect in more detail in Chapter $2 x .{ }^{31}$

These are the essential quantities we need. With them we will be able to handle most problems of transistor circuit design, and we will have little need to refer to the Ebers-Moll equation itself. ${ }^{32}$

### 2.3.3 The emitter follower revisited

Before looking again at the common-emitter amplifier with the benefit of our new transistor model, let's take a quick look at the humble emitter follower. The EbersMoll model predicts that an emitter follower should have nonzero output impedance, even when driven by a voltage source, because of finite $r_{\mathrm{e}}$ (item B in the above list). The same effect also produces a voltage gain slightly less than unity, because $r_{\mathrm{e}}$ forms a voltage divider with the load resistor.

These effects are easy to calculate. With fixed base voltage, the impedance looking back into the emitter is just $R_{\text {out }}=d V_{\mathrm{BE}} / d I_{\mathrm{E}}$; but $I_{\mathrm{E}} \approx I_{\mathrm{C}}$, so $R_{\text {out }} \approx r_{\mathrm{e}}$, the intrinsic emitter resistance [recall $r_{\mathrm{e}}=25 / I_{\mathrm{C}}(\mathrm{mA})$ ]. For example, in Figure 2.43A, the load sees a driving impedance of $r_{\mathrm{e}}=25 \Omega$, because $I_{\mathrm{C}}=1 \mathrm{~mA}$. (This is paralleled by the emitter resistor $R_{\mathrm{E}}$, if used; but in practice $R_{\mathrm{E}}$ will always be much larger than $r_{\mathrm{e}}$.) Figure 2.43B shows a more typical situation, with finite source resistance $R_{\mathrm{S}}$ (for simplicity we've omitted the obligatory biasing components -

[^68]base divider and blocking capacitor - which are shown in Figure 2.43C). In this case the emitter follower's output impedance is just $r_{\mathrm{e}}$ in series with $R_{\mathrm{S}} /(\beta+1)$ (again paralleled by an unimportant $R_{\mathrm{E}}$, if present). For example, if $R_{\mathrm{s}}=1 \mathrm{k}$ and $I_{\mathrm{C}}=1 \mathrm{~mA}, R_{\text {out }}=35 \Omega$ (assuming $\beta=100$ ). It is easy to show that the intrinsic emitter $r_{\mathrm{e}}$ also figures into an emitter follower's input impedance, just as if it were in series with the load (actually, parallel combination of load resistor and emitter resistor). In other words, for the emitter follower circuit the effect of the Ebers-Moll model is simply to add a series emitter resistance $r_{\mathrm{e}}$ to our earlier results. ${ }^{33}$

The voltage gain of an emitter follower is slightly less than unity, owing to the voltage divider produced by $r_{\mathrm{e}}$ and the load. It is simple to calculate, because the output is at the junction of $r_{\mathrm{e}}$ and $R_{\text {load }}: G_{\mathrm{V}}=v_{\text {out }} / v_{\text {in }}=R_{\mathrm{L}} /\left(r_{\mathrm{e}}+R_{\mathrm{L}}\right)$. Thus, for example, a follower running at 1 mA quiescent current, with 1 k load, has a voltage gain of 0.976 . Engineers sometimes like to write the gain in terms of the transconductance, to put it in a form that holds for FETs also (see §3.2.3A); in that case (using $g_{m}=1 / r_{\mathrm{e}}$ ) you get $G_{\mathrm{V}}=R_{\mathrm{L}} g_{m} /\left(1+R_{\mathrm{L}} g_{m}\right)$.

### 2.3.4 The common-emitter amplifier revisited

Previously we got wrong answers for the voltage gain of the common-emitter amplifier with emitter resistor (sometimes called emitter degeneration) when we set the emitter resistor equal to zero; recall that our wrong answer was $G_{\mathrm{V}}=-R_{\mathrm{C}} / R_{\mathrm{E}}=\infty!$

The problem is that the transistor has $25 / I_{\mathrm{C}}(\mathrm{mA})$ ohms of built-in (intrinsic) emitter resistance $r_{\mathrm{e}}$ that must be added to the actual external emitter resistor. This resistance is significant only when small emitter resistors (or none at all) are used. ${ }^{34}$ So, for instance, the amplifier we considered previously will have a voltage gain of $-10 \mathrm{k} / r_{\mathrm{e}}$, or -400 , when the external emitter resistor is zero. The input impedance is not zero, as we would have predicted earlier $\left(\beta R_{\mathrm{E}}\right.$ ); it is approximately $\beta r_{\mathrm{e}}$, or in this case ( 1 mA quiescent current) about $2.5 \mathrm{k} .{ }^{35}$

[^69]image_name:A
description:
[
name: Q1, type: NPN, ports: {C: LOAD, B: VB, E: e1}
name: load, type: Resistor, ports: {N1: e1, N2: GND}
]
extrainfo:The circuit diagram A is a simple NPN transistor configuration with a fixed bias voltage VB. The transistor Q1 is connected with its collector at the LOAD node, base at VB, and emitter at e1. A resistor labeled 'load' is connected between e1 and ground. The circuit has a 1mA current flowing from the LOAD node through the transistor.
image_name:B
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: b1}
name: Q1, type: NPN, ports: {C: LOAD, B: b1, E: e1}
name: load, type: Resistor, ports: {N1: e1, N2: GND}
]
extrainfo:The circuit is a common-emitter amplifier with an NPN transistor Q1. The input signal is applied to the base of the transistor (b1) through a resistor RS. The output is taken from the collector (LOAD). The emitter is grounded through a resistor. The gain and output impedance are given by G = Rload / (Rload + re) and Zout = re + Zin/β respectively.
image_name:C
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: b1, E: e1}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X1}
name: R1, type: Resistor, value: R1, ports: {N1: VCC, N2: b1}
name: R2, type: Resistor, value: R2, ports: {N1: b1, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: X1, Nn: b1}
]
extrainfo:The circuit is a common-emitter amplifier with a biasing network consisting of R1 and R2, and a blocking capacitor C1 to couple the input signal. The output is taken from the emitter of Q1. The load is connected to the emitter, making it an emitter follower configuration.

Figure 2.43. Output impedance of emitter followers (see text).

The terms "grounded emitter" and "common emitter" are sometimes used interchangeably, and they can be confusing. We will use the phrase "grounded-emitter amplifier" to mean a common-emitter amplifier with $R_{\mathrm{E}}=0$ (or equivalent bypassing). A common-emitter amplifier stage may have an emitter resistor; what matters is that the emitter circuit is common to the input circuit and the output circuit.

[^70]
#### A. Shortcomings of the single-stage grounded emitter amplifier

The extra voltage gain you get by using $R_{\mathrm{E}}=0$ comes at the expense of other properties of the amplifier. In fact, the grounded-emitter amplifier, in spite of its popularity in textbooks, should be avoided except in circuits with overall negative feedback. In order to see why, consider Figure 2.44 .
image_name:Figure 2.44
description:
[
name: Q1, type: NPN, ports: {C: signal out, B: signal in, E: GND}
name: RC, type: Resistor, value: 10k, ports: {N1: LOAD, N2: signal out}
name: LOAD, type: VoltageSource, value: +20V, ports: {Np: LOAD, Nn: GND}
]
extrainfo:This is a common-emitter amplifier without emitter degeneration, providing high voltage gain at the cost of increased nonlinearity.

Figure 2.44. Common-emitter amplifier without emitter degeneration.

1. Nonlinearity. The voltage gain is $G=-g_{m} R_{\mathrm{C}}=$ $-R_{\mathrm{C}} / r_{\mathrm{e}}=-R_{\mathrm{C}} I_{\mathrm{C}}(\mathrm{mA}) / 25$, so for a quiescent current of 1 mA , the gain is -400 . But $I_{\mathrm{C}}$ varies as the output signal varies. For this example, the gain will vary from -800 $\left(V_{\text {out }}=0, I_{\mathrm{C}}=2 \mathrm{~mA}\right)$ down to zero ( $\left.V_{\text {out }}=V_{\mathrm{CC}}, I_{\mathrm{C}}=0\right)$. For a triangle-wave input, the output will look as in Figure 2.45. The amplifier has lots of distortion, or poor linearity. The grounded-emitter amplifier without feedback is useful only for small-signal swings about the quiescent point. By contrast, the emitter-degenerated amplifier has a gain almost entirely independent of collector current, as long as $R_{\mathrm{E}} \gg r_{\mathrm{e}}$, and can be used for undistorted amplification even with large-signal swings.

It's easy to estimate the distortion, both with and without an external emitter resistor. With a grounded emitter, the incremental (small-signal) gain is $G_{\mathrm{V}}=-R_{\mathrm{C}} / r_{\mathrm{e}}=$ $-I_{\mathrm{C}} R_{\mathrm{C}} / V_{\mathrm{T}}=-V_{\text {drop }} / V_{\mathrm{T}}$, where $V_{\text {drop }}$ is the instantaneous voltage drop across the collector resistor. Because the gain is proportional to the drop across the collector resistor, the nonlinearity (fractional change of gain with swing) equals the ratio of instantaneous swing to average quiescent drop across the collector resistor: $\Delta G / G \approx \Delta V_{\text {out }} / V_{\text {drop }}$, where $V_{\text {drop }}$ is the average, or quiescent, voltage drop across the collector resistor $R_{\mathrm{C}}$. Because this represents the extreme variation of gain (i.e., at the peaks of the swing), the overall waveform "distortion" (usually stated as the amplitude of the residual waveform after subtraction of the strictly linear component) will be smaller by roughly a factor of 3 . Note that the distortion depends on only the ratio of swing to quiescent drop, and not directly on the operating current, etc.

As an example, in a grounded emitter amplifier powered from +10 V , biased to half the supply (i.e., $V_{\text {drop }}=5 \mathrm{~V}$ ), we measured a distortion of $0.7 \%$ at 0.1 V output sinewave amplitude and $6.6 \%$ at 1 V amplitude; these values are in good agreement with the predicted values. Compare this with the situation with an added external emitter resistor $R_{\mathrm{E}}$, in which the voltage gain becomes $G_{\mathrm{V}}=-R_{\mathrm{C}} /\left(r_{\mathrm{e}}+R_{\mathrm{E}}\right)=$ $-I_{\mathrm{C}} R_{\mathrm{C}} /\left(V_{\mathrm{T}}+I_{\mathrm{C}} R_{\mathrm{E}}\right)$. Only the first term in the denominator contributes distortion, so the distortion is reduced by the ratio of $r_{\mathrm{e}}$ to the total effective emitter resistance: the nonlinearity becomes $\Delta G / G \approx\left(\Delta V_{\text {out }} / V_{\text {drop }}\right)\left[r_{\mathrm{e}} /\left(r_{\mathrm{e}}+R_{\mathrm{E}}\right)\right]=$ $\left(\Delta V_{\text {out }} / V_{\text {drop }}\right)\left[V_{\mathrm{T}} /\left(V_{\mathrm{T}}+I_{\mathrm{E}} R_{\mathrm{E}}\right)\right]$; the second term is the factor by which the distortion is reduced. When we added an emitter resistor, chosen to drop 0.25 V at the quiescent current - which by this estimate should reduce the nonlinearity by a factor of $10-$ the measured distortion of the previous amplifier dropped to $0.08 \%$ and $0.74 \%$ for 0.1 V and 1 V output amplitudes, respectively. Once again, these measurement agree well with our prediction.

Exercise 2.12. Calculate the predicted distortion for these two amplifiers at the two output levels that were measured.

As we remarked, the nonlinearity of a common-emitter amplifier, when driven by a triangle wave, takes the form of the asymmetric "barn roof" distortion sketched in Figure 2.45. ${ }^{36}$ For comparison we took a real-life 'scope (oscilloscope) trace of a grounded emitter amplifier (Figure 2.46); we used a 2 N 3904 with a 5 k collector resistor to a +10 V supply, biased (carefully!) to half the supply. With a ruler we estimated the incremental gain at output voltages of +5 V (halfway to $V_{+}$) and at +7.5 V , as shown, where the collector current is 1 mA and 0.5 mA , respectively. The gain values are in pretty good agreement with the predictions $\left(G=R_{\mathrm{C}} / r_{\mathrm{e}}=I_{\mathrm{C}}(\mathrm{mA}) R_{\mathrm{C}} / 25 \Omega\right)$ of $G=-200$ and $G=-100$, respectively. By comparison, Figure 2.47 shows what happened when we added a $225 \Omega$ emitter resistor: the gain is reduced by a factor of 10 at the quiescent point $\left(G=R_{\mathrm{C}} /\left(R_{\mathrm{E}}+r_{\mathrm{e}}\right) \approx R_{\mathrm{C}} / 250 \Omega\right)$, but with much improved linearity (because changes in $r_{\mathrm{e}}$ contribute little to the overall resistance in the denominator, which is now dominated by the fixed $225 \Omega$ external emitter resistor).

For sinusoidal input, the output contains all harmonics of the fundamental wave. Later in the chapter we'll see how to make differential amplifiers with a pair of transistors; for these the residual distortion is symmetric, and contains only the odd harmonics. And in Chapter $2 x$ we'll see some very clever methods for cancelling distortion in differential

[^71]image_name:Figure 2.45
description:The graph in Figure 2.45 is a time-domain waveform representing the output voltage \( V_{out} \) of a grounded-emitter amplifier over time. The horizontal axis is labeled 'time,' and the vertical axis is labeled \( V_{out} \), indicating that the graph displays how the output voltage varies with time. The scale on the vertical axis is linear, with a reference line marked at \( V_{CC} \), the supply voltage.

The waveform shows a nonlinear behavior characterized by a series of peaks and valleys, indicating the presence of distortion in the output signal. Each cycle of the waveform consists of a rise and fall in voltage, with the peaks not reaching \( V_{CC} \), suggesting clipping or saturation effects at the output.

The graph is annotated with terms 'low gain' and 'high gain,' indicating varying gain levels throughout the waveform. The slope of the waveform is said to be proportional to \( V_{CC} - V \), suggesting that the gain of the amplifier is dependent on the difference between the supply voltage and some reference voltage \( V \).

Overall, the waveform demonstrates how a grounded-emitter amplifier can introduce nonlinear distortion, with the gain being higher at certain points and lower at others, resulting in a waveform that deviates from a pure sinusoidal shape. This distortion is typical in amplifiers operating near their limits, where the output is no longer a perfect replica of the input signal."}opfujsonjson{

Figure 2.45. Nonlinear output waveform from grounded-emitter amplifier.
image_name:Figure 2.45
description:The graph in Figure 2.45 illustrates the output waveform from a grounded-emitter amplifier, showcasing nonlinear distortion. It is a time-domain waveform with two traces: the input and the output signals.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform.

2. **Axes Labels and Units:**
- The horizontal axis represents time, with a scale of 0.2 ms/division.
- The vertical axis represents voltage, with two scales: the input signal is shown at 25 mV/div (AC-coupled), and the output signal at 1.25 V/div (DC-coupled).

3. **Overall Behavior and Trends:**
- The input waveform is a triangle wave, indicating a linear increase and decrease in voltage over time.
- The output waveform is distorted, deviating from the triangle shape of the input, which is typical for amplifiers operating near their limits.
- The output waveform exhibits peaks and valleys that are more rounded compared to the sharp transitions in the input triangle wave, reflecting the nonlinear gain of the amplifier.

4. **Key Features and Technical Details:**
- The gain of the amplifier varies along the waveform. Tangent lines are drawn on the output waveform to estimate gain at certain points.
- The gain is annotated as G = -19.0 and G = -9.5 at different sections of the waveform, indicating varying amplification levels.
- The distortion is more pronounced at the peaks of the waveform where the gain decreases.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for gain estimates at specific points on the output waveform.
- The output is referenced to ground as indicated by the 'output gnd ref' label.

Overall, this graph demonstrates the nonlinear behavior of a grounded-emitter amplifier, where the output waveform is not a perfect replica of the input due to varying gain levels, leading to distortion.

Figure 2.46. Real life! The grounded-emitter amplifier of Figure 2.44 , with $R_{\mathrm{C}}=5 \mathrm{k}, V_{+}=+10 \mathrm{~V}$, and a 1 kHz triangle wave input. Top and bottom of the screen are +10 V and ground for the dccoupled output trace (note sensitive scale for the ac-coupled input signal). Gain estimates (tangent lines) are at $V_{\text {out }}$ values of $0.5 V_{+}$ and $0.75 V_{+}$. Horizontal: $0.2 \mathrm{~ms} /$ div.
amplifiers, along with the use of SPICE simulation software for rapid analysis and circuit iteration. Finally, to set things in perspective, we should add that any amplifier's residual distortion can be reduced dramatically by use of negative feedback. We'll introduce feedback later in this chapter (\$2.5), after you've gained familiarity with common transistor circuits. Feedback will finally take center stage when we get to operational amplifiers in Chapter 4.
2. Input impedance. The input impedance is roughly $\mathbf{Z}_{\text {in }}=\beta r_{\mathrm{e}}=25 \beta / I_{\mathrm{C}}(\mathrm{mA})$ ohms. Once again, $I_{\mathrm{C}}$ varies over the signal swing, giving a varying input impedance. Unless the signal source driving the base has low impedance, you will wind up with nonlinearity because of the nonlinear (variable) voltage divider formed from the signal source and the amplifier's input impedance. By contrast, the input impedance of an emitter-degenerated amplifier is nearly constant, and high.
3. Biasing. The grounded emitter amplifier is difficult to
image_name:Figure 2.47
description:The graph in Figure 2.47 is a time-domain waveform illustrating the input and output voltages of an amplifier circuit. The horizontal axis represents time, with a scale of 0.2 milliseconds per division. The vertical axes represent voltage, with the input voltage labeled as 0.2 volts per division (ac) and the output voltage labeled as 1.25 volts per division (dc).

The graph shows a series of triangular waveforms. The input waveform is a symmetrical triangle wave with a smaller amplitude, while the output waveform has a larger amplitude and is inverted, indicating a negative gain. The gain of the amplifier is annotated as \( G = -19.6 \), which is consistent with the observed inversion and amplification of the input signal.

The waveform has a periodic pattern, with each cycle consisting of a linear rise and fall, characteristic of a triangular wave. The input and output signals are aligned in such a way that the peaks of the input correspond to the troughs of the output, highlighting the phase inversion.

Key features include the linear segments of the waveforms, which indicate a consistent rate of change, and the inversion of the output signal relative to the input. The graph effectively demonstrates the effect of adding a 225-ohm emitter resistor to the amplifier, resulting in improved linearity at the expense of gain, as described in the accompanying text.

Figure 2.47. Adding a $225 \Omega$ emitter resistor improves the linearity dramatically at the expense of gain (which drops by a factor of 10 at the quiescent point). Horizontal: $0.2 \mathrm{~ms} /$ div.
bias. It might be tempting just to apply a voltage (from a voltage divider) that gives the right quiescent current according to the Ebers-Moll equation. That won't work, because of the temperature dependence of $V_{\mathrm{BE}}$ (at fixed $I_{\mathrm{C}}$ ), which varies about $2.1 \mathrm{mV} /{ }^{\circ} \mathrm{C}$ [it actually decreases with increasing $T$ because of the variation of $I_{\mathrm{S}}(T)$ with temperature; as a result, $V_{\mathrm{BE}}$ is roughly proportional to $1 / T$, the absolute temperature]. This means that the collector current (for fixed $V_{\mathrm{BE}}$ ) will increase by a factor of 10 for a $30^{\circ} \mathrm{C}$ rise in temperature (which corresponds to a 60 mV change in $V_{\mathrm{BE}}$ ), or about $9 \% /{ }^{\circ} \mathrm{C}$. Such unstable biasing is useless, because even rather small changes in temperature will cause the amplifier to saturate. For example, a grounded emitter stage biased with the collector at half the supply voltage will go into saturation if the temperature rises by $8^{\circ} \mathrm{C}$.
Exercise 2.13. Verify that an $8^{\circ} \mathrm{C}$ rise in ambient temperature will cause a base-voltage-biased grounded emitter stage to saturate, assuming that it was initially biased for $V_{\mathrm{C}}=0.5 V_{\mathrm{CC}}$.

Some solutions to the biasing problem are discussed in the following sections. By contrast, the emitterdegenerated amplifier achieves stable biasing by applying a voltage to the base, most of which appears across the emitter resistor, thus determining the quiescent current.

#### B. Emitter resistor as feedback

Adding an external series resistor to the intrinsic emitter resistance $r_{\mathrm{e}}$ (emitter degeneration) improves many properties of the common-emitter amplifier, but at the expense of gain. You will see the same thing happening in Chapters 4 and 5, when we discuss negative feedback, an important technique for improving amplifier characteristics by feeding back some of the output signal to reduce the effective input signal. The similarity here is no coincidence -
the emitter-degenerated amplifier itself uses a form of negative feedback. Think of the transistor as a transconductance device, determining collector current (and therefore output voltage) according to the voltage applied between the base and emitter; but the input to the amplifier is the voltage from base to ground. So the voltage from base to emitter is the input voltage, minus a sample of the output (namely $I_{\mathrm{E}} R_{\mathrm{E}}$ ). That's negative feedback, and that's why emitter degeneration improves most properties of the amplifier (here improved linearity and stability and increased input impedance. ${ }^{37}$ ) Later in the chapter, in $\S 2.5$, we'll make these statements quantitative when we first look at feedback. And there are great things to look forward to, with the full flowering of feedback in Chapters 4 and 5!

### 2.3.5 Biasing the common-emitter amplifier

If you must have the highest possible gain (or if the amplifier stage is inside a feedback loop), it is possible to arrange successful biasing of a common-emitter amplifier. There are three solutions that can be applied, separately or in combination: bypassed emitter resistor, matched biasing transistor, and dc feedback.
image_name:Figure 2.48
description:
[
name: 82k, type: Resistor, value: 82k, ports: {N1: LOAD, N2: b1}
name: 0.1μF, type: Capacitor, value: 0.1μF, ports: {Np: Vin, Nn: b1}
name: 10k, type: Resistor, value: 10k, ports: {N1: b1, N2: GND}
name: Q1, type: NPN, ports: {C: Vout, B: b1, E: e1}
name: RC, type: Resistor, value: 7.5k, ports: {N1: VCC, N2: Vout}
name: RE, type: Resistor, value: 1.0k, ports: {N1: e1, N2: GND}
name: 10μF, type: Capacitor, value: 10μF, ports: {Np: e1, Nn: GND}
name: VCC, type: VoltageSource, value: +15V, ports: {Np: VCC, Nn: GND}
]
extrainfo:The circuit is a common-emitter amplifier with a bypassed emitter resistor. It uses feedback for biasing stability and is biased at VCC/2. The gain is given by GV = -20VCC and the output impedance is Zout = RC.

Figure 2.48. A bypassed emitter resistor can be used to improve the bias stability of a grounded-emitter amplifier.

#### A. Bypassed emitter resistor

You can use a bypassed emitter resistor, biasing as for the degenerated amplifier, as shown in Figure 2.48. In this case $R_{\mathrm{E}}$ has been chosen about $0.1 R_{\mathrm{C}}$, for ease of biasing; if $R_{\mathrm{E}}$ is too small, the emitter voltage will be much smaller than the base-emitter drop, leading to temperature instability of the quiescent point as $V_{\mathrm{BE}}$ varies with temperature. The emitter bypass capacitor is chosen to make its impedance small compared with $r_{\mathrm{e}}$ (not $R_{\mathrm{E}}-$ why?) at the

[^72]lowest frequency of interest. In this case its impedance is $25 \Omega$ at 650 Hz . At signal frequencies the input coupling capacitor sees an impedance of 10 k in parallel with the base impedance, in this case $\beta \times 25 \Omega$, or roughly 2.5 k . At dc , the impedance looking into the base is much larger ( $\beta$ times the emitter resistor, or about 100k).
image_name:Figure 2.49
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: LOAD, N2: b1}
name: R2, type: Resistor, value: R2, ports: {N1: b1, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: b1}
name: Q1, type: NPN, ports: {C: +20V, B: b1, E: e1}
name: 10k, type: Resistor, value: 10k, ports: {N1: +20V, N2: Vout}
name: 175Ω, type: Resistor, value: 175Ω, ports: {N1: e1, N2: GND}
]
extrainfo:The circuit is a single-stage amplifier with a gain of 50. It uses an NPN transistor (Q1) with a collector resistor of 10k ohms and an emitter resistor of 175 ohms. The circuit is powered by a +20V supply and is designed for signals from 20 Hz to 20 kHz. The base voltage is 0.775V and the emitter voltage is 0.175V.

Figure 2.49. Gain-of-50 stage presents blas stability problem.
A variation on this circuit consists of using two emitter resistors in series, one of them bypassed. For instance, suppose you want an amplifier with a voltage gain of 50, quiescent current of 1 mA , and $V_{\mathrm{CC}}$ of +20 volts, for signals from 20 Hz to 20 kHz . If you try to use the emitterdegenerated circuit, you will have the circuit shown in Figure 2.49. The collector resistor is chosen to put the quiescent collector voltage at $0.5 V_{\mathrm{CC}}$. Then the emitter resistor is chosen for the required gain, including the effects of the $r_{\mathrm{e}}$ of $25 / I_{\mathrm{C}}(\mathrm{mA})$. The problem is that the emitter voltage of only 0.175 V will vary significantly as the $\sim 0.6 \mathrm{~V}$ of base-emitter drop varies with temperature $\left(-2.1 \mathrm{mV} /{ }^{\circ} \mathrm{C}\right.$, approximately), since the base is held at constant voltage by $R_{1}$ and $R_{2}$; for instance, you can verify that an increase of $20^{\circ} \mathrm{C}$ will cause the collector current to increase by nearly $25 \%$.

Exercise 2.14. Show that this statement is correct.
The solution here is to add some bypassed emitter resistance for stable biasing, with no change in gain at signal frequencies (Figure 2.50). As before, the collector resistor is chosen to put the collector at 10 volts $\left(0.5 V_{\mathrm{CC}}\right)$. Then the unbypassed emitter resistor is chosen to give a gain of 50, including the intrinsic emitter resistance $r_{\mathrm{e}}=$ $25 / I_{\mathrm{C}}(\mathrm{mA})$. Enough bypassed emitter resistance is added to make stable biasing possible (one-tenth of the collector resistance is a good guideline). The base voltage is chosen to give 1 mA of emitter current, with impedance about one-tenth the dc impedance looking into the base (in this case about 100 k$)$. The emitter bypass capacitor is chosen to have low impedance compared with $180+25 \Omega$ at the lowest signal frequencies. Finally, the input coupling ca-
pacitor is chosen to have low impedance compared with the signal-frequency input impedance of the amplifier, which is equal to the voltage-divider impedance in parallel with $\beta \times(180+25) \Omega$ (the $820 \Omega$ is bypassed and looks like a short at signal frequencies).
image_name:Figure 2.50
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: b1}
name: Q1, type: NPN, ports: {C: LOAD, B: b1, E: e1}
name: R1, type: Resistor, value: 110k, ports: {N1: LOAD, N2: b1}
name: R2, type: Resistor, value: 10k, ports: {N1: b1, N2: GND}
name: R3, type: Resistor, value: 10k, ports: {N1: +20V, N2: Vout}
name: R4, type: Resistor, value: 180Ω, ports: {N1: b1, N2: e1}
name: R5, type: Resistor, value: 820Ω, ports: {N1: e1, N2: GND}
name: C2, type: Capacitor, value: 68μF, ports: {Np: e1, Nn: GND}
]
extrainfo:This circuit is a common-emitter amplifier designed for bias stability, linearity, and large voltage gain. The emitter bypass capacitor (C2) is used to reduce impedance at low frequencies, and input coupling capacitor (C1) manages the input signal frequency impedance. The amplifier's gain can be varied by adjusting the 180Ω resistor (R4) without changing the bias.

Figure 2.50. A common-emitter amplifier combining bias stability, linearity, and large voltage gain.

An alternative circuit splits the signal and dc paths (Figure 2.51 ). This lets you vary the gain (by changing the $180 \Omega$ resistor) without bias change.
image_name:Figure 2.51
description:
[
name: Q1, type: NPN, ports: {C: LOAD, B: Vin, E: e1}
name: 1.0k, type: Resistor, value: 1.0k, ports: {N1: e1, N2: GND}
name: 180Ω, type: Resistor, value: 180Ω, ports: {N1: e1, N2: GND}
name: X1, type: Capacitor, value: 68μF, ports: {Np: e1, Nn: GND}
]
extrainfo:This is a common-emitter amplifier circuit. The transistor Q1 is used for amplification. The resistor 1.0k is used for biasing, and the 180Ω resistor can be adjusted to vary the gain. The capacitor X1 is used to reduce impedance at low frequencies.

Figure 2.51. Equivalent emitter circuit for Figure 2.50.

#### B. Matched biasing transistor

You can use a matched transistor to generate the correct base voltage for the required collector current; this ensures automatic temperature compensation (Figure 2.52). ${ }^{38} Q_{1}$ 's collector is drawing 1 mA , since it is guaranteed to be near ground (about one $V_{\mathrm{BE}}$ drop above ground, to be exact); if $Q_{1}$ and $Q_{2}$ are a matched pair (available as a single device, with the two transistors on one piece of silicon), then $Q_{2}$ will also be biased to draw 1 mA , putting its collector at

[^73]+10 volts and allowing a full $\pm 10 \mathrm{~V}$ symmetrical swing on its collector. Changes in temperature are of no importance as long as both transistors are at the same temperature. This is a good reason for using a "monolithic" dual transistor.
image_name:A
description:
[
name: Q1, type: NPN, ports: {C: b1, B: b1, E: GND}
name: Q2, type: NPN, ports: {C: Vout, B: b2, E: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: b1, Nn: b2}
name: C, type: Capacitor, value: C, ports: {Np: b2, Nn: Vin}
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Vout, type: VoltageSource, value: Vout, ports: {Np: Vout, Nn: GND}
name: 10k, type: Resistor, value: 10k, ports: {N1: b1, N2: C1}
name: 20k, type: Resistor, value: 20k, ports: {N1: +20V, N2: b1}
name: 180Ω, type: Resistor, value: 180Ω, ports: {N1: e1, N2: GND}
]
extrainfo:The circuit diagram shows a biasing scheme with compensated V_BE drop for both grounded emitter and degenerated emitter stages. It includes monolithic dual transistors Q1 and Q2, which are matched pairs. The circuit allows a full ±10 V symmetrical swing on the collector of Q2.
image_name:B
description:
[
name: Q1, type: NPN, ports: {C: b2, B: b1, E: e1}
name: Q2, type: NPN, ports: {C: Vout, B: b2, E: e2}
name: R1, type: Resistor, value: 20k, ports: {N1: LOAD, N2: b2}
name: R2, type: Resistor, value: 10k, ports: {N1: b1, N2: C1}
name: R3, type: Resistor, value: 10k, ports: {N1: b2, N2: Vout}
name: R4, type: Resistor, value: 180Ω, ports: {N1: e1, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: C1, Nn: b2}
name: C, type: Capacitor, value: C, ports: {Np: b2, Nn: Vin}
]
extrainfo:The circuit diagram B represents a biasing scheme with compensated V_BE drop for a degenerated emitter stage. It uses feedback to stabilize the quiescent point and allows for a symmetrical voltage swing at the collector of Q2.

Figure 2.52. Biasing scheme with compensated $V_{\mathrm{BE}}$ drop, for both grounded emitter (A) and degenerated emitter (B) stages. With the values shown, $V_{\mathrm{C}}$ would be approximately 10.5 V ; reducing the 20 k resistor to 19.1 k (a standard value) would take into account the effects of $V_{\mathrm{BE}}$ and finite $\beta$ and put $V_{\mathrm{C}}$ at 10 V .

#### C. Feedback at dc

You can use dc feedback to stabilize the quiescent point. Figure 2.53A shows one method. By taking the bias voltage from the collector, rather than from $V_{\mathrm{CC}}$, you get some measure of bias stability. The base sits one diode drop above ground - and because its bias comes from a 10:1 divider, the collector must be at 11 diode drops above ground, or about 7 volts. Any tendency for the transistor to saturate (e.g., if it happens to have unusually high beta) is stabilized, since the dropping collector voltage will reduce the base bias. This scheme is acceptable if great stability is not required. The quiescent point is liable to drift a volt or so as the ambient (surrounding) temperature changes, because the base-emitter voltage has a significant temperature coefficient (Ebers-Moll, again). Better stability is possible if
several stages of amplification are included within the feedback loop. You will see examples later in connection with feedback.

A better understanding of feedback is really necessary to understand this circuit. For instance, feedback acts to reduce the input and output impedances. The input signal sees $R_{1}$ 's resistance effectively reduced by the voltage gain of the stage. In this case it is equivalent to a resistor of about $200 \Omega$ to ground (not pleasant at all!). Later in this chapter (and again in Chapter 4) we treat feedback in enough detail so that you will be able to figure the voltage gain and terminal impedance of this circuit.

Figures 2.53B-D illustrate some variations on the basic dc-feedback bias scheme: circuit B adds some emitter degeneration to improve linearity and predictability of gain; circuit C adds to that an input follower to increase the input impedance (with appropriately increased $R_{1} R_{2}$ divider values and changed ratio to accommodate the additional $V_{\mathrm{BE}}$ drop); and circuit D combines the methods of Figure 2.51 with circuit B to achieve greater bias stability.

Note that the base bias resistor values in these circuits could be increased to raise the input impedance, but you should then take into account the non-negligible base current. Suitable values might be $R_{1}=220 \mathrm{k}$ and $R_{2}=33 \mathrm{k}$. An alternative approach might be to bypass the feedback resistance in order to eliminate feedback (and therefore lowered input impedance) at signal frequencies (Figure 2.54). ${ }^{39}$

#### D. Comments on biasing and gain

One important point about grounded emitter amplifier stages: you might think that the voltage gain can be raised by increasing the quiescent current, since the intrinsic emitter resistance $r_{\mathrm{e}}$ drops with rising current. Although $r_{\mathrm{e}}$ does decrease with increasing collector current, the smaller collector resistor you need to obtain the same quiescent collector voltage just cancels the advantage. In fact, you can show that the small-signal voltage gain of a grounded-emitter amplifier biased to $0.5 V_{\mathrm{CC}}$ is given by $G=20 V_{\mathrm{CC}}$ (in volts), independent of quiescent current.

Exercise 2.15. Show that the preceding statement is true.
If you need more voltage gain in one stage, one approach is to use a current source as an active load. Because its impedance is very high, single-stage voltage gains of

[^74]image_name:A.
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: e, E: GND}
name: R1, type: Resistor, value: 68k, ports: {N1: Vin, N2: e}
name: R2, type: Resistor, value: 6.8k, ports: {N1: e, N2: GND}
name: RE, type: Resistor, value: 50Ω, ports: {N1: e, N2: GND}
name: RC, type: Resistor, ports: {N1: Vout, N2: VCC}
name: C1, type: Capacitor, ports: {Np: e, Nn: Vin}
]
extrainfo:The circuit is a grounded-emitter amplifier with an NPN transistor (Q1) and is biased to achieve a quiescent collector voltage of approximately 0.5 VCC. The voltage gain is independent of the quiescent current. The circuit uses a resistor (RC) as the collector load and is connected to VCC. The input is AC-coupled through capacitor C1. The emitter resistor RE provides stabilization.
image_name:B.
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: b1, E: e1}
name: R1, type: Resistor, value: 68k, ports: {N1: Vin, N2: b1}
name: R2, type: Resistor, value: 6.8k, ports: {N1: b1, N2: GND}
name: RE, type: Resistor, value: 50, ports: {N1: e1, N2: GND}
name: RC, type: Resistor, ports: {N1: VCC, N2: Vout}
name: C1, type: Capacitor, ports: {Np: b1, Nn: Vin}
]
extrainfo:The circuit diagram B is a grounded-emitter amplifier with a voltage gain determined by the collector load resistor RC. The biasing is set to provide a quiescent point at 0.5 VCC. The emitter resistor RE provides stability against variations in temperature and transistor parameters.
image_name:C.
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: b1, E: e1}
name: Q2, type: NPN, ports: {C: Vout, B: e1.b2, E: e2}
name: R1, type: Resistor, value: 68k, ports: {N1: Vin, N2: b1}
name: R2, type: Resistor, value: 6.8k, ports: {N1: b1, N2: GND}
name: R3, type: Resistor, value: 6.8k, ports: {N1: e1.b2, N2: GND}
name: RE, type: Resistor, value: 50Ω, ports: {N1: e2, N2: GND}
name: RC, type: Resistor, ports: {N1: VCC, N2: Vout}
name: C1, type: Capacitor, ports: {Np: Vin, Nn: b1}
name: C2, type: Capacitor, ports: {Np: e1, Nn: X1}
]
extrainfo:The circuit is a multi-stage amplifier with two NPN transistors Q1 and Q2. The output is labeled as Vout, and the circuit is biased with a VCC supply. Resistors R1 and R2 form a voltage divider for the base of Q1, while R3 provides biasing for Q2. Capacitors C1 and C2 are used for coupling and bypassing.
image_name:D.
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: b1, E: e1}
name: R1, type: Resistor, value: 68k, ports: {N1: Vin, N2: b1}
name: R2, type: Resistor, value: 6.8k, ports: {N1: b1, N2: GND}
name: RC, type: Resistor, ports: {N1: Vout, N2: VCC}
name: RE1, type: Resistor, value: 1k, ports: {N1: e1, N2: GND}
name: RE2, type: Resistor, value: 50Ω, ports: {N1: e1, N2: GND}
name: C1, type: Capacitor, ports: {Np: b1, Nn: Vin}
name: C2, type: Capacitor, ports: {Np: e1, Nn: X1}
]
extrainfo:The circuit is a single-stage amplifier with an active load, using a current source for high impedance. The voltage gain is increased by using a current source as a load, and the amplifier is part of a DC feedback loop.

1000 or more are possible. ${ }^{40}$ Such an arrangement cannot be used with the biasing schemes we have discussed, but must be part of an overall dc feedback loop, a subject we will discuss in Chapter 4. You should be sure such an amplifier looks into a high-impedance load; otherwise the gain obtained by high collector load impedance will be lost. Something like an emitter follower, an FET, or an op-amp presents a good load.
image_name:Figure 2.54
description:
[
name: C1, type: Capacitor, value: 10μF, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: 33k, ports: {N1: X1, N2: C1}
name: R2, type: Resistor, value: 33k, ports: {N1: X1, N2: b1}
name: R3, type: Resistor, value: 6.8k, ports: {N1: b1, N2: GND}
name: Q1, type: NPN, ports: {C: C1, B: b1, E: e1}
]
extrainfo:This circuit is a common-emitter amplifier with a feedback loop. It uses an NPN transistor (Q1) with a collector resistor (R1) and a biasing network formed by R2 and R3. The capacitor C1 is used for coupling the input signal, and the circuit is grounded at the emitter of Q1.

Figure 2.54. Eliminating impedance-lowering feedback at signal frequencies.

In RF amplifiers intended for use only over a narrow frequency range, it is common to use a parallel $L C$ circuit as a collector load. In that case a very high voltage gain is possible since the $L C$ circuit has high impedance (like a current source) at the signal frequency, with low impedance at dc. Because the $L C$ is "tuned," out-of-band interfering signals (and distortion) are effectively rejected. Additional bonuses are the possibility of peak-to-peak (pp) output swings of $2 V_{\mathrm{CC}}$, and the use of transformer coupling from the inductor.

[^75]Exercise 2.16. Design a tuned common-emitter amplifier stage to operate at 100 kHz . Use a bypassed emitter resistor, and set the quiescent current at 1.0 mA . Assume $V_{\mathrm{CC}}=+15 \mathrm{~V}$ and $L=$ 1.0 mH , and put a 6.2 k resistor across the $L C$ to set $Q=10$ (to get a $10 \%$ bandpass; see $\S 1.714$ ). Use capacitive input coupling.
image_name:Figure 2.55
description:
[
name: Q1, type: PNP, ports: {C: X1, B: X1, E: X1}
name: Q2, type: PNP, ports: {C: VCC, B: X1, E: C2}
name: C2, type: Capacitor, value: C2, ports: {Np: C2, Nn: GND}
]
extrainfo:The circuit is a classic bipolar-transistor matched-pair current mirror. It mirrors a current I = Ip through the load connected to ground. The voltage supply is VCC, and VBE is indicated across the base-emitter junction of Q1.

Figure 2.55. Classic bipolar-transistor matched-pair current mirror. Note the common convention of referring to the positive supply as $V_{\mathrm{CC}}$, even when pnp transistors are used.

### 2.3.6 An aside: the perfect transistor

Looking at BJT transistor properties like the non-zero (and temperature-dependent) $V_{\mathrm{BE}}$, the finite (and currentdependent) emitter impedance $r_{\mathrm{e}}$ and transconductance $g_{m}$, the collector current that varies with collector voltage (Early effect) etc., one is tempted to ask which transistor is better? Is there a "best" transistor, or perhaps even a perfect transistor? If you go through our transistor tables, e.g., Tables 2.1 and 2.2, and especially Table 8.1 for small-signal transistors, you'll see there is no best transistor candidate. That's because all physical bipolar transistors are subject to the same device physics, and their parameters tend to scale with die size and current, etc.

However, it turns out that there is a candidate for a "perfect transistor," if you don't limit yourself to a single $n p n$ or $p n p$ structure; see Figure 2.56. This device has nearly ideal properties: $V_{\mathrm{BE}}=0 \mathrm{~V}(!)$, along with very high $g_{m}$ (thus low $r_{\mathrm{e}}$ ), and very high beta. And just to top it off, current can flow in either direction - it's ambidextrous, or "bipolarity" (saying it's bipolarity is better than saying it's a bipolar bipolar transistor). Like a regular BJT, it's a transconductance device: when driven with a positive $V_{\mathrm{BE}}$ input signal, it sources an output current that is $g_{m}$ times greater, and vice versa (with a negative $V_{\mathrm{BE}}$ it sinks a current). Unlike a BJT, though, it's noninverting. All signals are referenced to ground. Very nice.
image_name:A
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: Vin, E: GND}
name: Cin, type: Capacitor, value: Cin, ports: {Np: Vin, Nn: GND}
name: Cout, type: Capacitor, value: Cout, ports: {Np: Vout, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: LOAD1}
name: RE, type: Resistor, value: RE, ports: {N1: E, N2: GND}
name: b1, type: Resistor, value: b1, ports: {N1: Vin, N2: GND}
name: e1, type: Resistor, value: e1, ports: {N1: E, N2: GND}
]
extrainfo:The circuit is a common-emitter BJT amplifier with emitter degeneration and load resistors. It is designed to amplify the input signal Vin with the output taken at Vout. The circuit includes capacitors Cin and Cout for AC coupling.
image_name:B
description:
[
name: Q1, type: NPN, ports: {C: C, B: B, E: E}
name: RL, type: Resistor, value: RL, ports: {N1: C, N2: GND}
name: RE, type: Resistor, value: RE, ports: {N1: E, N2: GND}
]
extrainfo:The circuit B is a common-emitter amplifier stage with emitter degeneration. It uses an NPN transistor Q1 with a load resistor RL connected to the collector and an emitter resistor RE connected to the emitter. The base is the input node, and the collector is the output node.
image_name:C
description:
[
name: OpAmp, type: OpAmp, ports: {InP: B, InN: E, OutP: C, OutN: , Vdd: V+, -Vdd: V-}
]
extrainfo:The circuit diagram C represents an Operational Transconductance Amplifier (OTA) symbol for a 'perfect' transistor. It is a noninverting amplifier with all signals referenced to ground.

Figure 2.56. A. An ordinary common-emitter BJT amplifier stage, with an emitter-degeneration resistor $R_{\mathrm{E}}$ and a load resistor $R_{\mathrm{L}}$. B. In a common-emitter amplifier built with the "perfect" transistor, all signals are referenced to ground, to which the load $R_{\mathrm{L}}$ is also returned (the power supplies are not shown). C. The OTA symbol for the perfect transistor, implemented as an Operational Transconductance Amplifier device. The truncated apex symbol means the device has a current output.

How does the perfect transistor work? Figure 2.57 shows a four-transistor circuit known as a diamond transistor stage. This circuit is a variation of the cascaded pnpnpn emitter follower in Figure 2.29: a complementary npnpnp input follower is wired in parallel, and biased with current sources; the emitter outputs ( $2 V_{\mathrm{BE}}$ apart) drive a matched push-pull output follower, which therefore runs at the same quiescent current. The common node is the effective emitter, $E$. Finally, a pair of current mirrors brings the two individual collector currents to a common output, the effective collector, $C$, where the output current is zero if the input voltage (between terminals $B$ and $E$ ) is zero. As with an ordinary BJT, any current into (or out of) the emitter has to appear at the collector. The part does require two power supply connections. We'll have more to say about this interesting component in Chapters $2 x$ and $4 x$.

Texas Instruments calls their perfect transistor (its part
image_name:A
description:
[
name: Q1, type: NPN, ports: {C: V+, B: B, E: be}
name: Q2, type: NPN, ports: {C: C1, B: be, E: E}
name: Q3, type: PNP, ports: {C: be, B: B, E: V+}
name: Q4, type: PNP, ports: {C: E, B: be, E: C1}
name: I1, type: CurrentSource, value: I1, ports: {Np: V+, Nn: be}
name: I2, type: CurrentSource, value: I2, ports: {Np: C1, Nn: V-}
name: OpAmp1, type: OpAmp, ports: {InP: B, InN: GND, Out: be}
name: Buffer, type: Buffer, ports: {In: C1, Out: E}
]
extrainfo:The circuit diagram illustrates a 'perfect transistor' using a diamond transistor configuration. It includes two current mirrors and an output buffer. The diamond transistor is composed of complementary matched offset-cancelled emitter followers, providing high linearity and wide bandwidth.
image_name:B
description:
[
name: V+, type: VoltageSource, ports: {Np: V+, Nn: GND}
name: V-, type: VoltageSource, ports: {Np: GND, Nn: V-}
name: Q1, type: NPN, ports: {C: V+, B: B, E: be}
name: Q2, type: NPN, ports: {C: C, B: be, E: E}
name: Q3, type: PNP, ports: {C: be, B: B, E: V-}
name: Q4, type: PNP, ports: {C: E, B: e, E: V-}
name: I1, type: CurrentSource, ports: {Np: V+, Nn: be}
name: I2, type: CurrentSource, ports: {Np: be, Nn: C}
name: Buffer, type: Buffer, ports: {In: C, Out: E}
name: OpAmp, type: OpAmp, ports: {InP: B, InN: GND, Out: be}
]
extrainfo:The circuit diagram 'B' represents a diamond transistor configuration with two NPN and two PNP transistors. It includes current mirrors and a buffer for output. The OpAmp is used to control the transistor operation, providing a voltage-controlled current source functionality.

Figure 2.57. A. The OPA860 perfect transistor includes a diamond transistor (the triangle) and a pair of current mirrors. A second diamond transistor acts as an output buffer. B. The diamond transistor consists of a complementary pair of matched offset-cancelled emitter followers.
number is OPA860 $0^{41}$ ) an Operational Transconductance Amplifier (OTA). Other names they use are "VoltageControlled Current source," "Transconductor," "Macro Transistor," and "positive second-generation current conveyor" (CCII+). We fear it has a branding identity crisis, so, with characteristic understatement, we're calling it a "perfect transistor."

How close to perfection do these parts come? The OPA860 and OPA861 perfect transistors have these specs: $V_{\text {os }}=3 \mathrm{mV}$ typ ( 12 mV max), $g_{m}=95 \mathrm{mS}, r_{\mathrm{e}}=10.5 \Omega$, $Z_{\text {out }}=54 \mathrm{k} \Omega\left\|2 \mathrm{pF}, Z_{\text {in }}=455 \mathrm{k} \Omega\right\| 2 \mathrm{pF}, I_{\text {out }(\max )}= \pm 15 \mathrm{~mA}$. Its maximum gain is 5100 . Hardly perfect, but, hey, not half bad. You can create many nice circuits with these puppies (e.g., active filter, wideband current summing circuit, or integrator for nanosecond-scale pulses); see the OPA860 datasheet for details.

[^76]
[^0]:    ${ }^{1}$ A mid-century computer (the IBM 650) cost \$300,000, weighed 2.7 tons, and contained 126 lamps on its control panel; in an amusing reversal, a contemporary energy-efficient lamp contains a computer of greater capability within its base, and costs about $\$ 10$.

[^1]:    2 These are the definitions, but hardly the way circuit designers think of voltage. With time, you'll develop a good intuitive sense of what voltage really is, in an electronic circuit. Roughly (very roughly) speaking, voltages are what you apply to cause currents to flow.

[^2]:    ${ }^{3}$ It has been said that engineers in other disciplines are envious of electrical engineers, because we have such a splendid visualization tool.

[^3]:    ${ }^{4}$ In the domain of high frequencies or low impedances, that isn't strictly true, and we will have more to say about this later, and in Chapter $1 x$. For now, it's a good approximation.

[^4]:    ${ }^{5}$ Unless you're a power engineer working with giant 13 kV transformers and the like - those guys are allowed to say amperage.
${ }^{6}$... also, Dude, "ohmage" is not the preferred nomenclature: resistance, please.

[^5]:    ${ }^{7}$ The sizes of chip resistors and other components intended for surface mounting are specified by a four-digit size code, in which each pair of digits specifies a dimension in units of $0.010^{\prime \prime}(0.25 \mathrm{~mm}$ ). For example, an 0805 size resistor is $2 \mathrm{~mm} \times 1.25 \mathrm{~mm}$, or $80 \mathrm{mils} \times 50$ mils ( 1 mil is $0.001^{\prime \prime}$ ); the height must be separately specified. To add confusion to this simple scheme, the four-digit size code may instead be metric (sometimes without saying so!), in units of 0.1 mm : thus an " 0805 " (English) is also a "2012" (metric).

[^6]:    ${ }^{8}$ Conservatively rated at $1 / 8$ watt in its RN55 military grade ("MILspec"), but rated at $1 / 4$ watt in its CMF-55 industrial grade.

[^7]:    ${ }^{9}$ A popular "international" alternative notation replaces the decimal point with the unit multiplier, thus 4 k 7 or 1 M 0 . A $2.2 \Omega$ resistor becomes 2R2. There is an analogous scheme for capacitors and inductors.

[^8]:    ${ }^{10}$ With an error, in this case, of just $0.01 \%$.

[^9]:    12 We provide a proof, for those who are interested, in Appendix D.

[^10]:    ${ }^{13}$ This is the opposite of an ideal voltage-measuring meter, which should present infinite resistance across its input terminals.
14 A special class of current meters known as electrometers operate with very small voltage burdens (as little at 0.1 mV ) by using the technique of feedback, something we'll learn about in Chapters 2 and 4.

[^11]:    15 There are two important exceptions to this general principle: (1) a current source has a high (ideally infinite) internal resistance and should drive a load of relatively low load resistance; (2) when dealing with ra-

[^12]:    dio frequencies and transmission lines, you must "match impedances" (i.e., set $R_{\text {load }}=R_{\text {internal }}$ ) in order to prevent reflection and loss of power. See Appendix H on transmission lines.
${ }^{16}$ The urge to anthropomorphize runs deep in the engineering and scientific community, despite warnings like "don't anthropomorphize computers ... they don't like it."

[^13]:    18 Occasionally you'll encounter devices (e.g., mechanical movingpointer meters) that respond to the average magnitude of an ac signal.

[^14]:    ${ }^{19}$ One of the authors, when asked by his nontechnical spouse how much we spent on that big plasma screen, replied " $36 \mathrm{~dB} \$$."

[^15]:    ${ }^{20}$ Readers of the scientific journal Nature (London) were greeted, in 2008, with an article titled "The missing memristor found" (D. B. Strukov et al., 453, 80, 2008), purporting to have found a heretofore missing "fourth fundamental [passive circuit] element." We are skeptical. However the controversy is ultimately resolved, it should be noted that the memristor is a nonlinear element; there are only three linear passive 2-terminal circuit elements.

[^16]:    21 And it doesn't hurt to have a high dielectric constant, as well: air has $\varepsilon=1$, but plastic films have $\varepsilon=2.1$ (polypropylene) or 3.1 (polyester). And certain ceramics are popular among capacitor makers: $\varepsilon=45$ ("C0G" type) or 3000 ("X7R" type).

[^17]:    22 Ironically, these essential bypass capacitors are so taken for granted that they are usually omitted from schematic diagrams (a practice we follow in this book). Don't make the mistake of omitting them also from your actual circuits!

[^18]:    23 To make matters confusing to the uninitiated, the units are often omitted on capacitor values specified in schematic diagrams. You have to figure it out from the context.

[^19]:    ${ }^{24}$ Complementary metal-oxide semiconductor, the dominant form of digital logic, as we'll see from Chapter 10 onward.

[^20]:    ${ }^{25}$ Devotees of the cinema will be reminded of Dr. Strangelove's outburst:
"The whole point of a doomsday machine is lost ... if you keep it secret!"

[^21]:    ${ }^{26}$ We're used to thinking of signals as time-varying voltages; but we'll see how we can convert such signals to proportional time-varying currents, by using "voltage-to-current converters" (with the fancier name "transconductance amplifiers").

[^22]:    27 Just as with the differentiator, we'll have another way of framing this criterion in §1.7.10.

[^23]:    ${ }^{29}$ The diode drop can be eliminated with active switching (or synchronous switching, a technique in which the diodes are replaced by transistor switches, actuated in synchronism with the input ac waveform (see §9.5.3B).

[^24]:    ${ }^{30}$ While teaching electronics we've noticed that students love to memorize these equations! An informal poll of the authors showed that two out of two engineers don't memorize them. Please don't waste brain cells that way - instead, learn how to derive them.

[^25]:    ${ }^{31}$ Called the conduction angle.

[^26]:    ${ }^{32}$ A popular variant is the regulated switching power converter. Although its operation is quite different in detail, it uses the same feedback principle to maintain a constant output voltage. See Chapter 9 for much more on both techniques.

[^27]:    ${ }^{33}$ As explained in §9.5.1, you should choose a capacitor rated for
"across-the-line" service.

[^28]:    ${ }^{34}$ A mechanical analogy may be helpful here. Imagine dropping packages onto a conveyor belt that is moving at speed $v$; the packages are accelerated to that speed by friction, with $50 \%$ efficiency, finally reaching the belt speed $v$, at which speed they ride into the sunset. That's resistive charging. Now we try something completely different, namely, we rig up a conveyor belt with little catchers attached by springs to the belt; and alongside it we have a second belt, running at twice the speed $(2 v)$. Now when we drop a package onto the first conveyor it compresses a spring, then rebounds at $2 v$; and it makes a soft landing onto the second conveyor. No energy is lost (ideal springs), and the package rides off into the sunset at $2 v$. That's reactive charging.
${ }^{35}$ Resonant charging is used for the high-voltage supply in flashlamps and stroboscopes, with the advantages of (a) full charge between flashes (spaced no closer than $t_{\mathrm{f}}$ ), and (b) no current immediately after discharge (see waveforms), thus permitting the flashlamp to "quench" after each flash.

[^29]:    ${ }^{36}$ But, in a nutshell, the magnitude of $\mathbf{Z}$ gives the ratio of amplitudes of voltage to current, and the polar angle of $\mathbf{Z}$ gives the phase angle between current and voltage.

[^30]:    ${ }^{37}$ Later we'll see inductors, which also have a $90^{\circ}$ phase shift (though of the opposite sign), and so are likewise characterized by a reactance $X_{\mathrm{L}}$.

[^31]:    ${ }^{38}$ Of course, it fails to predict anything about phase shifts in this circuit. As we'll see later, the output signal's phase lags the input by $90^{\circ}$ at high frequencies, going smoothly from $0^{\circ}$ at low frequencies, with a $45^{\circ}$ lag at $\omega_{0}$ (see Figure 1.104 in §1.7.9).

[^32]:    39 With two important exceptions, namely, transmission lines and current sources.

[^33]:    ${ }^{40}$ We take the easy path here by specifying the current, rather than the voltage; we are rewarded with a simple derivative (rather than a simple integral!).

[^34]:    ${ }^{41}$ Note the convention that the reactance $X_{\mathrm{C}}$ is a real number (the $90^{\circ}$ phase shift is implicit in the term "reactance"), but the corresponding impedance is purely imaginary: $\mathbf{Z}=R-j X$.

[^35]:    ${ }^{42}$ It's always a good idea to check limiting values: here we see that $P \rightarrow V^{2} / R$ for large $C$; and for small $C$ the magnitude of the current $|I| \rightarrow V_{0} / X_{\mathrm{C}}$, or $V_{0} \omega C$, thus $P \rightarrow I^{2} R=V_{0}^{2} \omega^{2} C^{2} R$, in agreement at both limits.

[^36]:    ${ }^{43}$ Or, for nonlinear circuits, it indicates that the current waveform is not proportional to the voltage waveform. More on this in §9.7.1.

[^37]:    ${ }^{46}$ Or, equivalently, $Q=R / X_{\mathrm{C}}=R / X_{\mathrm{L}}$, where $X_{\mathrm{L}}=X_{\mathrm{C}}$ are the reactances at $\omega_{0}$.
${ }^{47}$ We'll see in Chapter $1 x$ that real components depart from the ideal, often expressed in terms of an effective series resistance, ESR.

[^38]:    ${ }^{48}$ Or, equivalently, $Q=X_{\mathrm{L}} / R=X_{\mathrm{C}} / R$, where $X_{\mathrm{L}}=X_{\mathrm{C}}$ are the reactances at $\omega_{0}$.

[^39]:    49 There are more complicated ways of framing this, but you don't really want to know just yet...

[^40]:    ${ }^{50}$ These use gold contact plating.

[^41]:    ${ }^{51}$ In an amusing historical footnote, the stepping relay used for a century as the cornerstone of telephone exchanges (the "Strowger selector") was invented by a Topeka undertaker, Almon Strowger, evidently because he suspected that telephone calls intended for his business were being routed (by the switchboard operators in his town) to a funeral home competitor.

[^42]:    52 A search for "connector" on the DigiKey website returns 116 categories, with approximately 43,000 individual varieties in stock.

[^43]:    ${ }^{53}$ Advocates of each would probably reply "This is our most modestly priced receptacle."

[^44]:    54 The invention of the gallium nitride blue LED was the breakthrough product of a lone and unappreciated employee of Nichia Chemical Industries, Shuji Nakamura.
${ }^{55}$ And of course, for both residential and commercial area lighting, LEDs have now largely relegated to the dustbin of history the century-old hot-filament incandescent lamp.

[^45]:    ${ }^{56}$ An interesting form of variable inductor of yesteryear was the variometer, a rotatable coil positioned within a fixed outer coil and connected in series with it. As the inner coil was rotated, the total inductance went from maximum (four times the inductance of either coil alone) all the way down to zero. These things were consumer items, listed for example in the 1925 Sears Roebuck catalog.

[^46]:    ${ }^{57}$ Physics 123 ("Laboratory Electronics") at Harvard University: "Half course (fall term; repeated spring term). A lab-intensive introduction to electronic circuit design. Develops circuit intuition and debugging skills through daily hands-on lab exercises, each preceded by class discussion, with minimal use of mathematics and physics. Moves quickly from passive circuits, to discrete transistors, then concentrates on operational amplifiers, used to make a variety of circuits including integrators, oscillators, regulators, and filters. The digital half of the course treats analog-digital interfacing, emphasizing the use of microcontrollers and programmable logic devices (PLDs)." See http://webdocs.registrar.fas.harvard.edu/ courses/Physics.html.

[^47]:    ${ }^{1}$ It is even possible to achieve modest voltage gain in a circuit comprising only resistors and capacitors. To explore this idea, surprising even to seasoned engineers, look at Appendix J on SPICE.

[^48]:    ${ }^{4}$ As the " $h$-parameter" transistor model has fallen out of popularity, you tend often to see $\beta$ (instead of $h_{\mathrm{FE}}$ ) as the symbol for current gain.

[^49]:    ${ }^{5}$ In addition to listing typical betas ( $h_{\mathrm{FE}}$ ) and maximum allowed collector-to-emitter voltages ( $V_{\text {CEO }}$ ), Table 2.1 includes the cutoff frequency ( $f_{\mathrm{T}}$, at which the beta has decreased to 1 ) and the feedback capacitance $\left(C_{\mathrm{cb}}\right)$. These are important when dealing with fast signals or high frequencies; we'll see them in $\S 2.4 .5$ and Chapter $2 x$.

[^50]:    ${ }^{6}$ A small "speed-up" capacitor - typically just a few picofarads - is often connected across the base resistor to improve high-speed performance.

[^51]:    ${ }^{7}$ Or, for faster turn-off, with a resistor, an $R C$ network, or zener clamp; see §1.6.7.

[^52]:    ${ }^{8}$ A mathematician would define linearity by saying that the response to the sum of two inputs is the sum of the individual responses; this necessarily implies proportionality.
${ }^{9}$ If you took a census, asking the transistors of the world what they are doing, at least $95 \%$ would tell you they are switches.

[^53]:    ${ }^{10}$ The larger drop is due to the use of different semiconductor materials such as GaAsP, GaAlAs, and GaN, with their larger bandgaps.

[^54]:    11 metal-oxide semiconductor field-effect transistor.

[^55]:    ${ }^{12}$ But don't make it too small: $Q_{3}$ would not switch at all if $R_{3}$ were reduced to $100 \Omega$ (why?). We were surprised to see this basic error in an instrument, the rest of which displayed circuit design of the highest sophistication.

[^56]:    ${ }^{13}$ A caution here: this circuit should not be run from a supply voltage greater than +7 V , because the negative pulse can drive $Q_{2}$ 's base into reverse breakdown. This is a common oversight, even among experienced circuit designers.

[^57]:    14 We'll see other ways of making a Schmitt trigger, using op-amps or comparators, in Chapter 4.

[^58]:    ${ }^{15}$ We use the boldface symbol $\mathbf{Z}$ when the complex nature of impedance is important. In common usage the term "impedance" can refer loosely to the magnitude of impedance, or even to a purely real impedance (e.g., transmission-line impedance); for such instances we use the ordinary math-italic symbol $Z$.

[^59]:    ${ }^{16}$ This is a property shared by all shunt regulators, of which the zener is the simplest example.

[^60]:    ${ }^{17}$ In a variation of this circuit, the upper resistor is replaced with a diode.

[^61]:    18 These values may seem curiously "unround." But they are chosen from the widely available EIA "E6" decade values (see Appendix C); and in fact "round-number" values of $0.5 \mu \mathrm{~F}$ and $3.0 \mu \mathrm{~F}$ are harder to find.

[^62]:    ${ }_{19}$ A red LED, with its forward voltage drop of $\approx 1.6 \mathrm{~V}$, is a convenient substitute for a string of three diodes.
20 "Sink" and "source" simply refer to the direction of current flow: if a circuit supplies (positive) current to a point, it is a source, and vice versa.

[^63]:    ${ }^{21}$ The impedance looking into the base itself will usually be much larger because of the way the base resistors are chosen, and it can generally be ignored.

[^64]:    ${ }^{22}$ The inverse of reactance is susceptance (and the inverse of impedance is admittance), and has a special unit, the siemens ("S," not to be confused with lowercase "s," which means seconds), which used to be called the mho (ohm spelled backward, symbol " $(\mathrm{J}$ ").

[^65]:    ${ }^{23}$ We indicate the important temperature dependence of $I_{S}$ by explicitly showing it in functional form - " $I_{\mathrm{S}}(T)$ ".

[^66]:    24 J. J. Ebers \& J. L. Moll, "Large-signal behavior of junction transistors," Proc. IRE 42, 1761 (1954).
${ }^{25}$ This is sometimes called a Gummel plot.

[^67]:    ${ }^{26}$ The " 25 " in this and the following discussion is more precisely 25.3 mV , the value of $k_{\mathrm{B}} T / q$ at room temperature. It's proportional to absolute temperature - engineers like to say "PTAT," pronounced pee'tat. This has interesting (and useful) consequences, for example the

[^68]:    ${ }^{30}$ The connection between Early voltage and $\eta$ is $\eta=V_{\mathrm{T}} /\left(V_{\mathrm{A}}+V_{\mathrm{CE}}\right) \approx$ $V_{\mathrm{T}} / V_{\mathrm{A}}$; see Chapter $2 x$.
${ }^{31}$ Previewing some of the results there, the Early effect (a) determines a transistor's collector output resistance $r_{\mathrm{o}}=V_{\mathrm{A}} / I_{\mathrm{C}}$; (b) sets a limit on single-stage voltage gain; and (c) limits the output resistance of a current source. Other things being equal, pnp transistors tend to have low Early voltages, as do transistors with high beta; high-voltage transistors usually have high Early voltages, along with low beta. These trends can be seen in the measured Early voltages listed in Table 8.1.
${ }^{32}$ The computer circuit-analysis program SPICE includes accurate transistor simulation with the Ebers-Moll formulas and Gummel-Poon charge models. It's a lot of fun to "wire up" circuits on your computer screen and set them running with SPICE. For more detail see the application of SPICE to BJT amplifier distortion in Chapter $2 x$.

[^69]:    ${ }^{33}$ There's more, if you look deeper: at high frequencies (above $f_{\mathrm{T}} / \beta$ ) the effective current gain drops inversely with frequency; so you get a linearly rising output impedance from an emitter follower that is driven with low $R_{\mathrm{s}}$. That is, it looks like an inductance, and a capacitive load can cause ringing or even oscillation; these effects are treated in Chapter $2 x$.
${ }^{34}$ Or, equivalently, when the emitter resistor is bypassed with a capacitor whose impedance at signal frequencies is comparable with, or less than, $r_{\mathrm{e}}$.
35 These estimates of gain and input impedance are reasonably good, as long as we stay away from operation at very high frequencies or

[^70]:    from circuits in which the collector load resistor is replaced with a current source "active load" $\left(R_{\mathrm{C}} \rightarrow \infty\right)$. The ultimate voltage gain of a grounded-emitter amplifier, in the latter situation, is limited by the Early effect; this is discussed in more detail Chapter $2 x$.

[^71]:    ${ }^{36}$ Because the gain (i.e., the slope of $V_{\text {out }}$ versus $V_{\text {in }}$ ) is proportional to the distance from the $V_{\mathrm{CC}}$ line, the shape of the curve is in fact an exponential.

[^72]:    37 And, as we'll learn, the output impedance would be reduced - a desirable feature in a voltage amplifier - if the feedback were taken directly from the collector.

[^73]:    ${ }^{38}$ R. Widlar, "Some circuit design techniques for linear integrated circuits," IEEE Trans. Circuit Theory CT-12, 586 (1965). See also US Patent 3,364,434.

[^74]:    ${ }^{39}$ But caution: the cascaded $R C$ sections ( 33 k into $10 \mu \mathrm{~F}, 33 \mathrm{k}$ into the input capacitor) can cause peaking or instability, unless care is taken (for example by avoiding similar $R C$ products).

[^75]:    ${ }^{40}$ Ultimately limited by the transistor's finite collector output resistance (a consequence of the Early effect); see the Early effect discussion in Chapter $2 x$.

[^76]:    ${ }^{41}$ TI's OP861 version omits the output buffer and is available in a small SOT-23 package. That's one of our favorite surface-mount package styles, available for many of the other transistors mentioned in our tables. Knowledgeable readers will recognize the circuitry from inside a current-feedback, or CFB opamp. Some of these devices (for example the AD844) make the internal node available.

### 2.3.7 Current mirrors

The technique of matched base-emitter biasing can be used to make what is called a current mirror, an interesting current-source circuit that simply reverses the sign of a "programming" current. (Figure 2.55). You program the mirror by sinking a current from $Q_{1}$ 's collector. That causes a $V_{\mathrm{BE}}$ for $Q_{1}$ appropriate to that current at the circuit temperature and for that transistor type. $Q_{2}$, matched to $Q_{1}{ }^{42}$ is thereby programmed to source the same current to the load. The small base currents are unimportant. ${ }^{43}$

One nice feature of this circuit is voltage compliance of the output transistor current source to within a few tenths of a volt of $V_{\mathrm{CC}}$, as there is no emitter resistor drop to contend with. Also, in many applications it is handy to be able to program a current with a current. An easy way to generate the control current $I_{P}$ is with a resistor (Figure 2.58). Because the bases are a diode drop below $V_{\mathrm{CC}}$, the 14.4 k resistor produces a control current, and therefore an output current, of 1 mA . Current mirrors can be used in transistor circuits whenever a current source is needed. They're very popular in integrated circuits, where (a) matched transistors abound and (b) the designer tries to make circuits that will work over a large range of supply voltages. There are even resistorless IC op-amps in which the operating current of the whole amplifier is set by one external resistor, with all the quiescent currents of the individual amplifier stages inside being determined by current mirrors.
image_name:Figure 2.58
description:
[
name: Q1, type: PNP, ports: {C: VCC, B: X1, E: GND}
name: Q2, type: PNP, ports: {C: VCC, B: X1, E: load}
name: X1, type: Resistor, value: 14.4k, ports: {N1: X1, N2: GND}
name: I, type: CurrentSource, ports: {Np: load, Nn: GND}
]
extrainfo:The circuit is a current mirror with PNP transistors Q1 and Q2. The resistor X1 sets the reference current IP. The current mirror provides a constant current I to the load.

Figure 2.58. Programming current-mirror current.

#### A. Current-mirror limitations due to the Early effect

One problem with the simple current mirror is that the output current varies a bit with changes in output voltage, i.e.,

[^0]the output impedance is not infinite. This is because of the slight variation of $V_{\mathrm{BE}}$ with collector voltage at a given current in $Q_{2}$ (which is due to the Early effect); said a different way, the curve of collector current versus collectoremitter voltage at a fixed base-emitter voltage is not flat (Figure 2.59). In practice, the current might vary $25 \%$ or so over the output compliance range - much poorer performance than that of the current source with an emitter resistor discussed earlier.
image_name:Figure 2.59
description:The graph in Figure 2.59 illustrates the Early effect in a transistor, showing how the collector current ($I_C$) varies with the collector-emitter voltage ($V_{CE}$) for different base-emitter voltages ($V_{BE}$). This is a family of curves typically used in transistor characteristics analysis.

1. **Type of Graph and Function:**
- The graph is a characteristic curve for a bipolar junction transistor (BJT), showing the relationship between collector current and collector-emitter voltage at constant base-emitter voltages.

2. **Axes Labels and Units:**
- The horizontal axis represents the collector-emitter voltage ($V_{CE}$) and is likely in volts.
- The vertical axis represents the collector current ($I_C$), probably measured in amperes or milliamperes.
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The curves show an upward trend, indicating that as $V_{CE}$ increases, $I_C$ also increases.
- Each curve corresponds to a different $V_{BE}$ value (0.60, 0.62, and 0.64 volts), with higher $V_{BE}$ values resulting in higher $I_C$ for the same $V_{CE}$.
- The curves are not flat, demonstrating the Early effect, where $I_C$ increases with $V_{CE}$ even at constant $V_{BE}$.

4. **Key Features and Technical Details:**
- The curves start from a point on the $V_{CE}$ axis and initially rise steeply before gradually leveling off at higher $V_{CE}$ values.
- Dashed lines extrapolate back to intersect the negative $V_{CE}$ axis at a point labeled as $-V_A$, representing the Early voltage.
- The Early voltage ($V_A$) is an indication of the output conductance of the transistor, with larger $V_A$ values implying better current source behavior.

5. **Annotations and Specific Data Points:**
- The curves are annotated with their respective $V_{BE}$ values (0.60, 0.62, 0.64 volts), indicating the conditions under which each curve was plotted.
- The intersection of the extrapolated dashed lines with the negative $V_{CE}$ axis provides a visual reference for understanding the Early effect and its impact on transistor performance.

Figure 2.59. Early effect: collector current varies with $V_{\mathrm{CE}}$. (Interestingly, you get a very similar curve, with comparable $V_{\mathrm{A}}$, if you apply instead a family of constant base currents.)
image_name:Figure 2.60
description:
[
name: Q1, type: PNP, ports: {C: Vcc, B: X1, E: e1}
name: Q2, type: PNP, ports: {C: Vcc, B: X1, E: e2}
name: R1, type: Resistor, value: 1.0k, ports: {N1: Vcc, N2: e1}
name: R2, type: Resistor, value: 1.0k, ports: {N1: Vcc, N2: e2}
name: R3, type: Resistor, value: 18k, ports: {N1: X1, N2: GND}
name: I1, type: CurrentSource, value: 1mA, ports: {Np: e2, Nn: GND}
]
extrainfo:The circuit is an improved current mirror with emitter resistors. It uses two matched PNP transistors (Q1 and Q2) with emitter resistors (R1 and R2) to improve the current source stability. The emitter resistors help minimize the effect of V_BE variations with V_CE on the output current.

Figure 2.60. Improved current mirror with emitter resistors.

One solution, if a better current source is needed (it often isn't), is the circuit shown in Figure 2.60. The emitter resistors are chosen to have at least a few tenths of a volt drop; this makes the circuit a far better current source, since the small variations of $V_{\mathrm{BE}}$ with $V_{\mathrm{CE}}$ are now negligible in determining the output current. Again, matched transistors should be used. Note that this circuit loses its effectiveness if operation over a wide range of programming current is intended (figure out why). ${ }^{44}$

[^1]image_name:Figure 2.61
description:
[
name: Q1, type: PNP, ports: {C: X1, B: C1b3, E: e1}
name: Q2, type: PNP, ports: {C: +VCC, B: X1, E: e2}
name: Q3, type: PNP, ports: {C: X1, B: C1b3, E: e3}
name: R1, type: Resistor, value: R1, ports: {N1: C1b3, N2: GND}
name: RE, type: Resistor, value: RE, ports: {N1: +VCC, N2: e1}
name: RE, type: Resistor, value: RE, ports: {N1: +VCC, N2: e2}
name: C1b3, type: Capacitor, value: C1b3, ports: {Np: C1b3, Nn: GND}
name: C3, type: Capacitor, value: C3, ports: {Np: e3, Nn: GND}
name: I_load, type: CurrentSource, value: I_load, ports: {Np: e3, Nn: GND}
]
extrainfo:The circuit is a Wilson current mirror with improved stability and reduced output current error due to the inclusion of cascode transistor Q3 and emitter resistors RE. The circuit is designed for good stability with load variations and reduced error caused by V_BE mismatch.

Figure 2.61. Wilson current mirror. Good stability with load variations is achieved through cascode transistor $Q_{3}$, which reduces voltage variations across $Q_{1}$. Adding a pair of emitter resistors $R_{\mathrm{E}}$, as shown, reduces output current error caused by $V_{\mathrm{BE}}$ mismatch, when chosen such that $I_{\mathrm{P}} R_{\mathrm{E}}$ is of order 100 mV or more.

#### B. Wilson mirror

Another current mirror with improved consistency of current is shown in the clever circuit of Figure 2.61. $Q_{1}$ and $Q_{2}$ are in the usual mirror configuration, but $Q_{3}$ now keeps $Q_{1}$ 's collector fixed at two diode drops below $V_{\mathrm{CC}}$. That circumvents the Early effect in $Q_{1}$, whose collector is now the programming terminal, with $Q_{2}$ now sourcing the output current. The result is that both current-determining transistors ( $Q_{1}$ and $Q_{2}$ ) have fixed collector-emitter drops; you can think of $Q_{3}$ as simply passing the output current through to a variable-voltage load (a similar trick is used in the cascode connection, which you will see later in the chapter). Transistor $Q_{3}$, by the way, does not have to be matched to $Q_{1}$ and $Q_{2}$; but if it has the same beta, then you get an exact cancellation of the (small) base current error that afflicts the simple mirror of Figure 2.55 (or the betaenhanced mirror in Chapter 2x).

Exercise 2.17. Show that this statement is true.

There are additional nice tricks you can do with current mirrors, such as generating multiple independent outputs, or an output that is a fixed multiple of the programming current. One trick (invented by the legendary Widlar) is to unbalance the $R_{\mathrm{E}}$ 's in Figure 2.61; as a rough estimate, the output current ratio is approximately the ratio of resistor values (because the base-emitter drops are roughly equal). But to get it right you need to take into account the difference of $V_{\mathrm{BE}}$ 's (because the transistors are running at different currents), for which the graph in Figure 2.62 is helpful. This graph is also useful for estimating the current unbalance in a current mirror built with discrete (i.e.,
not matched) transistors. We treat current mirrors further in Chapter $2 x(\$ 82 x .3$ and 2x.11).
image_name:Figure 2.62
description:**Type of Graph and Function:**
The graph is a logarithmic plot showing the relationship between the base-emitter voltage difference (ΔV_BE) and the collector current ratio (I_C2/I_C1) for matched transistors. This is a characteristic plot used in the analysis of bipolar junction transistors (BJTs).

**Axes Labels and Units:**
- The x-axis represents the Current Ratio (I_C2/I_C1), with a logarithmic scale ranging from 0.01 to 2.
- The y-axis represents the Base-Emitter Voltage Difference (ΔV_BE) in millivolts (mV), with a linear scale ranging from -120 mV to 20 mV.

**Overall Behavior and Trends:**
The graph shows a linear relationship between the logarithm of the current ratio and the base-emitter voltage difference. As the current ratio increases, the voltage difference also increases. The slope of the lines indicates the rate of change of ΔV_BE with respect to the current ratio.

**Key Features and Technical Details:**
- The graph includes three lines representing different temperatures: 0°C, 25°C, and 50°C. These lines show how temperature affects the base-emitter voltage difference for a given current ratio.
- The equation ΔV_BE = (kT/q) log_e(I_C2/I_C1) is annotated on the graph, where k is the Boltzmann constant, T is the temperature in Kelvin, and q is the charge of an electron. This equation describes the relationship between the current ratio and the voltage difference.
- The graph highlights that the change in ΔV_BE is approximately 60 mV per decade of current ratio change or 0.25 mV per percentage change.

**Annotations and Specific Data Points:**
- The graph includes gridlines to help identify specific data points along the current ratio and voltage difference axes.
- Temperature annotations (0°C, 25°C, 50°C) are marked along the lines, indicating the impact of temperature on the voltage difference for a given current ratio.

Figure 2.62. Collector current ratios for matched transistors, as determined by the difference in applied base-emitter voltages. See Table 8.1b for low-noise matched BJTs.

### 2.3.8 Differential amplifiers

The differential amplifier is a very common configuration used to amplify the difference voltage between two input signals. In the ideal case the output is entirely independent of the individual signal levels - only the difference matters.

Differential amplifiers are important in applications in which weak signals are contaminated by "pickup" and other miscellaneous noise. Examples include digital and RF signals transferred over twisted-pair cables, audio signals (the term "balanced" means differential, usually $600 \Omega$ impedance, in the audio business), local-area-network signals (such as 100BASE-TX and 1000BASE-T Ethernet), electrocardiogram voltages, magnetic disk head amplifiers, and numerous other applications. A differential amplifier at the receiving end restores the original signal if the interfering "common-mode" signals (see below) are not too large. Differential amplifiers are universally used in operational amplifiers, an essential building block that is the subject of Chapter 4. They're very important in dc amplifier design (amplifiers that amplify clear down to dc, i.e., have no coupling capacitors) because their symmetrical design is inherently compensated against thermal drifts.

Some nomenclature: when both inputs change levels together, that's a common-mode input change. A differential change is called normal mode, or sometimes differential mode. A good differential amplifier has a high commonmode rejection ratio (CMRR), the ratio of response for a normal-mode signal to the response for a common-mode signal of the same amplitude. CMRR is usually specified in decibels. The common-mode input range is the voltage level over which the inputs may vary. The differential amplifier is sometimes called a "long-tailed pair."

Figure 2.63 shows the basic circuit. The output is taken off one collector with respect to ground; that is called a single-ended output and is the most common configuration. You can think of this amplifier as a device that amplifies a difference signal and converts it to a single-ended signal so that ordinary subcircuits (followers, current sources, etc.) can make use of the output. (If, instead, a differential output is desired, it is taken between the collectors.)
image_name:Figure 2.63. Classic transistor differential amplifier.
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: Vin1, E: e1}
name: Q2, type: NPN, ports: {C: Vout, B: Vin2, E: e2}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Q1_C}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Q2_C}
name: RE, type: Resistor, value: RE, ports: {N1: e1, N2: A}
name: RE, type: Resistor, value: RE, ports: {N1: e2, N2: A}
name: R1, type: Resistor, value: R1, ports: {N1: A, N2: VEE}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: VEE, type: VoltageSource, value: VEE, ports: {Np: GND, Nn: VEE}
]
extrainfo:The circuit is a classic transistor differential amplifier with a single-ended output. It consists of two NPN transistors (Q1 and Q2) with shared emitter resistors (RE) and collector resistors (RC). The input signals are applied to the bases of the transistors, and the output is taken from the collector of Q2.

Figure 2.63. Classic transistor differential amplifier.
What is the gain? That's easy enough to calculate: imagine a symmetrical input signal wiggle, in which input 1 rises by $v_{\text {in }}$ (a small-signal variation) and input 2 drops by the same amount. As long as both transistors stay in the active region, point $A$ remains fixed. You then determine the gain as with the single transistor amplifier, remembering that the input change is actually twice the wiggle on either base: $G_{\text {diff }}=R_{\mathrm{C}} / 2\left(r_{\mathrm{e}}+R_{\mathrm{E}}\right)$. Typically $R_{\mathrm{E}}$ is small, $100 \Omega$ or less, or it may be omitted entirely. Differential voltage gains of a few hundred are possible.

You can determine the common-mode gain by putting identical signals $v_{\text {in }}$ on both inputs. If you think about it correctly ${ }^{45}$ (remembering that $R_{1}$ carries both emitter currents), you'll find $G_{\mathrm{CM}}=-R_{\mathrm{C}} /\left(2 R_{1}+R_{\mathrm{E}}\right)$. Here we've ig-

[^2]nored the small $r_{\mathrm{e}}$, because $R_{1}$ is typically large, at least a few thousand ohms. We really could have ignored $R_{\mathrm{E}}$ as well. The CMRR is thus roughly $R_{1} /\left(r_{\mathrm{e}}+R_{\mathrm{E}}\right)$. Let's look at a typical example (Figure 2.64) to get some familiarity with differential amplifiers.

Collector resistor $R_{\mathrm{C}}$ is chosen for a quiescent current of $100 \mu \mathrm{~A}$. As usual, we put the collector at $0.5 V_{\mathrm{CC}}$ for large dynamic range. $Q_{1}$ 's collector resistor can be omitted, since no output is taken there. ${ }^{46} R_{1}$ is chosen to give total emitter current of $200 \mu \mathrm{~A}$, split equally between the two sides when the (differential) input is zero. From the formulas just derived, this amplifier has a differential gain of 10 and a common-mode gain of 0.55 . Omitting the 1.0 k resistors raises the differential gain to 50 , but drops the (differential) input impedance from about 250 k to about 50 k (you can substitute Darlington transistors ${ }^{47}$ in the input stage to raise the impedance into the megohm range, if necessary).
image_name:Figure 2.64
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: Vin1, E: e1}
name: Q2, type: NPN, ports: {C: Vout, B: Vin2, E: e2}
name: C1, type: Capacitor, value: C1, ports: {Np: VCC, Nn: Vin1}
name: RC, type: Resistor, value: 25k, ports: {N1: VCC, N2: Vout}
name: RE1, type: Resistor, value: 1.0k, ports: {N1: e1, N2: X1}
name: RE2, type: Resistor, value: 1.0k, ports: {N1: e2, N2: X1}
name: R1, type: Resistor, value: 22k, ports: {N1: X1, N2: -5V}
name: 200μA, type: CurrentSource, value: 200μA, ports: {Np: X1, Nn: -5V}
]
extrainfo:The circuit is a differential amplifier with a differential gain of 10 and a common-mode gain of 0.55. Omitting the 1.0k resistors increases the differential gain to 50 but decreases the input impedance from about 250k to about 50k. Darlington transistors can be used to raise the impedance into the megohm range. The maximum differential gain with RE=0 is 20 times the voltage across the collector resistor.

Figure 2.64. Calculating differential amplifier performance.
Remember that the maximum gain of a single-ended grounded emitter amplifier biased to $0.5 V_{\mathrm{CC}}$ is $20 V_{\mathrm{CC}}$ (in volts). In the case of a differential amplifier the maximum differential gain $\left(R_{\mathrm{E}}=0\right)$ is half that figure, or (for arbitrary quiescent point) 20 times the voltage (in volts) across the collector resistor. The corresponding maximum CMRR (again with $R_{\mathrm{E}}=0$ ) is equal to 20 times the voltage (in volts) across $R_{1}$. As with the single-ended common-emitter amplifier, the emitter resistors $R_{\mathrm{E}}$ reduce distortion, at the

[^3]expense of gain. See the extensive discussion of BJT amplifier distortion in Chapter $2 x$.

Exercise 2.18. Verify that these expressions are correct. Then design a differential amplifier to run from $\pm 5 \mathrm{~V}$ supply rails, with $G_{\text {diff }}=25$ and $R_{\text {out }}=10 \mathrm{k}$. As usual, put the collector's quiescent point at half of $V_{\mathrm{CC}}$.

#### A. Biasing with a current source

The common-mode gain of the differential amplifier can be reduced enormously by the substitution of a current source for $R_{1}$. Then $R_{1}$ effectively becomes very large and the common-mode gain is nearly zero. If you prefer, just imagine a common-mode input swing; the emitter current source maintains a constant total emitter current, shared equally by the two collector circuits, by symmetry. The output is therefore unchanged. Figure 2.65 shows an example. The CMRR of this circuit, using an LM394 monolithic transistor pair for $Q_{1}$ and $Q_{2}$, will be around 100,000:1 $(100 \mathrm{~dB})$ at dc. The common-mode input range for this circuit goes from -3.5 V to +3 V ; it is limited at the low end by the compliance of the emitter current source and at the high end by the collector's quiescent voltage. ${ }^{48}$
image_name:Figure 2.65
description:
[
name: Q1, type: NPN, ports: {C: Vcc, B: b1, E: P}
name: Q2, type: NPN, ports: {C: Vcc, B: b2, E: P}
name: Q3, type: NPN, ports: {C: LOAD, B: b3k, E: a1}
name: D1, type: Diode, ports: {Na: a1, Nc: GND}
name: R1, type: Resistor, value: 10k, ports: {N1: b3k, N2: GND}
name: R2, type: Resistor, value: 3.24k, ports: {N1: a1, N2: GND}
name: R3, type: Resistor, value: 25k, ports: {N1: Vcc, N2: Vout}
name: I1, type: CurrentSource, value: 200µA, ports: {Np: P, Nn: -5V}
name: V1, type: VoltageSource, value: 1.24V, ports: {Np: b3k, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with improved CMRR using a current source. It uses a monolithic transistor pair for Q1 and Q2, providing high CMRR at DC. The common-mode input range is from -3.5V to +3V, limited by the emitter current source and collector quiescent voltage.

Figure 2.65. Improving CMRR of the differential amplifier with a current source.

Be sure to remember that this amplifier, like all transistor amplifiers, must have a dc bias path to the bases. If the input is capacitively coupled, for instance, you must have

[^4]base resistors to ground. An additional caution for differential amplifiers, particularly those without inter-emitter resistors: bipolar transistors can tolerate only 6 volts of baseemitter reverse bias before breakdown; thus, applying a differential input voltage larger than this will destroy the input stage (if there is no inter-emitter resistor). An inter-emitter resistor limits the breakdown current and prevents destruction, but the transistors may be degraded nonetheless (in beta, noise, etc.). In either case the input impedance drops drastically during reverse conduction.

An interesting aside: the emitter current sink shown in Figure 2.65 has some variation with temperature, because $V_{\mathrm{BE}}$ decreases with increasing temperature (to the tune of approximately $-2.1 \mathrm{mV} /{ }^{\circ} \mathrm{C}$, §2.3.2), causing the current to increase. More explicitly, if we call the 1.24 V zenerlike reference " $V_{\text {ref }}$ " then the drop across the emitter resistor equals $V_{\mathrm{ref}}-V_{\mathrm{BE}}$; the current is proportional, thus increasing with temperature. As it happens, this is in fact beneficial: it can be shown from basic transistor theory that the quantity $V_{g 0}-V_{\mathrm{BE}}$ is approximately proportional to absolute temperature (PTAT), where $V_{g 0}$ is the silicon bandgap voltage (extrapolated to absolute zero), approximately 1.23 V . So, by choosing our $V_{\text {ref }}$ voltage equal to the bandgap voltage, we have an emitter current that increases PTAT; and this cancels the temperature dependence of differential-pair voltage gain $\left(g_{m} \propto 1 / T_{\mathrm{ab}}, \S 2.3 .2\right.$ ). We'll explore this sort of cleverness a bit more in §9.10.2. And in Chapter 9 there's extensive discussion of the differential amplifier and the closely related "instrumentation amplifier."

#### B. Use in single-ended dc amplifiers

A differential amplifier makes an excellent dc amplifier, even for single-ended inputs. You just ground one of the inputs and connect the signal to the other (Figure 2.66). You might think that the "unused" transistor could be eliminated. Not so! The differential configuration is inherently compensated for temperature drifts, and even when one input is at ground that transistor is still doing something: a temperature change causes both $V_{\mathrm{BE}}$ 's to change the same amount, with no change in balance or output. That is, changes in $V_{\mathrm{BE}}$ are not amplified by $G_{\text {diff }}$ (only by $G_{\mathrm{CM}}$, which can be made essentially zero). Furthermore, the cancellation of $V_{\mathrm{BE}}$ 's means that there are no 0.6 V drops at the input to worry about. The quality of a dc amplifier constructed this way is limited only by mismatching of input $V_{\mathrm{BE}}$ 's or their temperature coefficients. Commercial monolithic transistor pairs and commercial differential amplifier ICs are available with extremely good matching (e.g., the MAT12 npn monolithic matched pair has a typical drift of
$V_{\mathrm{BE}}$ between the two transistors of $0.15 \mu \mathrm{~V} /{ }^{\circ} \mathrm{C}$ ). See Table 8.1 b on page 502 for a listing of matched BJTs.
image_name:Figure 2.66
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: Vin, E: e1}
name: Q2, type: NPN, ports: {C: Vout, B: GND, E: e2}
name: RC, type: Resistor, value: RC, ports: {N1: Vout, N2: VCC}
name: RE1, type: Resistor, value: RE, ports: {N1: e1, N2: P}
name: RE2, type: Resistor, value: RE, ports: {N1: e2, N2: P}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: VEE, type: VoltageSource, value: VEE, ports: {Np: GND, Nn: P}
]
extrainfo:This circuit is a differential amplifier used as a precision single-ended DC amplifier. It uses two NPN transistors (Q1 and Q2) with a shared emitter resistor configuration and is powered by dual voltage sources (+VCC and -VEE). The input is noninverting, applied to the base of Q1, while Q2 has its base grounded. The output is taken from the collector of Q2.

Figure 2.66. A differential amplifier can be used as a precision single-ended dc amplifier.

Either input could have been grounded in the preceding circuit example. The choice depends on whether or not the amplifier is supposed to invert the signal. (The configuration shown is preferable at high frequencies, however, because of the Miller effect; see §2.4.5.) The connection shown is noninverting, and so the inverting input has been grounded. This terminology carries over to op-amps, which are versatile high-gain differential amplifiers.

#### C. Current-mirror active load

As with the simple grounded-emitter amplifier, it is sometimes desirable to have a single-stage differential amplifier with very high gain. An elegant solution is a currentmirror active load (Figure 2.67). $Q_{1} Q_{2}$ is the differential pair with emitter current source. $Q_{3}$ and $Q_{4}$, a current mirror, form the collector load. The high effective collector load impedance provided by the mirror yields voltage gains of 5000 or more, assuming no load at the amplifier's output. ${ }^{49}$ Such an amplifier is very common as the input stage in a larger circuit, and is usually used only within a feedback loop, or as a comparator (discussed in the next section). Be sure to keep the load impedance of such an amplifier very high, or the gain will drop enormously.

#### D. Differential amplifiers as phase splitters

The collectors of a symmetrical differential amplifier generate equal signal swings of opposite phase. By taking outputs from both collectors, you've got a phase splitter. Of course, you could also use a differential amplifier with both

[^5]image_name:Figure 2.67
description:
[
name: Q1, type: NMOS, ports: {S: P, D: X1, G: Vin1}
name: Q2, type: NMOS, ports: {S: P, D: Vout, G: Vin2}
name: Q3, type: PMOS, ports: {S: VCC, D: X1, G: X1}
name: Q4, type: PMOS, ports: {S: VCC, D: Vout, G: X1}
name: VEE, type: VoltageSource, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with active current mirror load. It has two NMOS transistors (Q1, Q2) at the bottom and two PMOS transistors (Q3, Q4) at the top, with a voltage source VEE connected to node P.

Figure 2.67. Differential amplifier with active current mirror load.
differential inputs and differential outputs. This differential output signal could then be used to drive an additional differential amplifier stage, with greatly improved overall common-mode rejection.

#### E. Differential amplifiers as comparators

Because of its high gain and stable characteristics, the differential amplifier is the main building block of the comparator (which we saw in §1.4.2E), a circuit that tells which of two inputs is larger. They are used for all sorts of applications: switching on lights and heaters, generating square waves from triangles, detecting when a level in a circuit exceeds some particular threshold, class-D amplifiers and pulse-code modulation, switching power supplies, etc. The basic idea is to connect a differential amplifier so that it turns a transistor switch on or off, depending on the relative levels of the input signals. The linear region of amplification is ignored, with one or the other of the two input transistors cut off at any time. A typical hookup is illustrated in $\S 2.6 .2$ by a temperature-controlling circuit that uses a resistive temperature sensor (thermistor).

## 2.4 Some amplifier building blocks

We've now seen most of the basic - and important transistor circuit configurations: switch, follower, current source (and mirror), and common-emitter amplifier (both single-ended and differential). For the remainder of the chapter we look at some circuit elaborations and their consequences: push-pull, Darlington and Sziklai, bootstrapping, Miller effect, and the cascode configuration. We'll finish with an introduction to the wonderful (and essential) technique of negative feedback. Chapter $2 x$ deals with follow-on transistor circuits and techniques at a greater level of sophistication.

Table 2.2 Bipolar Power Transistors ${ }^{a}$

|  |  |  | $V_{\text {CEO }}$ <br> max | $\underset{\max _{\mathrm{b}}}{\mathrm{I}^{b}}$ | Pdiss $m^{b}{ }^{b, h}$ | $R_{\theta \mathrm{JC}}^{\mathrm{C}}$ |  | FE | Ic | $f_{\mathrm{T}}$ min | multiple |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| NPN | PNP | Case | (V) | (A) | (W) | ( ${ }^{\circ} \mathrm{C} / \mathrm{W}$ ) | min | typ | (A) | (MHz) | manf? |
| standard BJT |  |  |  |  |  |  |  |  |  |  |  |
| BD139 | BD140 | TO-126 | 80 | 1.5 | 12.5 | 10 | $40^{\text {e }}$ | 100 | 0.15 | 50 | $\cdot$ |
| 2N3055 | 2N2955 | TO-3 | 60 | 15 | 115 | 1.5 | 20 | -- | 4 | 2.5 | $\cdot$ |
| 2N6292 | 2N6107 | TO-220 | 70 | 7 | 40 | 3.1 | 30 | -- | 2 | 4 | - |
| TIP31C | TIP32C | TO-220 | 100 | 3 | 40 | 3.1 | 25 | 100 | 1 | 3 | $\cdot$ |
| TIP33C | TIP34C | TO-218 ${ }^{\text {d }}$ | 100 | 10 | 80 | 1.6 | 40 | 100 | 1 | 3 | $\cdot$ |
| TIP35C | TIP36C | TO-218 ${ }^{\text {d }}$ | 100 | 25 | 125 | 1.0 | 25 | 150 | 1.5 | 3 | $\cdot$ |
| MJ15015 | MJ15016 | TO-3 | 120 | 15 | 180 | 1.0 | 20 | 35 | 4 | $0.8^{9}$ | - |
| MJE15030 | MJE15031 | TO-220 | 150 | 8 | 50 | 2.5 | 40 | 80 | 3 | 30 | $\cdot$,z |
| MJE15032 | MJE15033 | TO-220 | 250 | 8 | 50 | 2.5 | 50 | 100 | 1 | 30 | $\cdot$ |
| 2SC5200 | 2SA1943 | TO-264 | 230 | 17 | 150 | 0.8 | 55 | 80 | 1 | 30 | $\cdot$ |
| 2SC5242 ${ }^{\text {k }}$ | 2SA1962 ${ }^{k}$ | TO-3P | 250 | s | S | S | s | s | s | s | $\cdot$ |
| MJE340 | MJE350 | TO-126 | 300 | 0.5 | 20 | 6 | 30 | -- | 0.05 | -- | $\cdot$ |
| TIP47 | MJE5730 | TO-220 | 250 | 1 | 40 | 3.1 | 30 | -- | 0.3 | 10 | $\cdot$ |
| TIP50 ${ }^{\text {U }}$ | MJE5731A ${ }^{\text {u }}$ | TO-220 | 400 | s | s | s | S | -- | s | s | $\cdot$ |
| MJE13007 | MJE5852 | TO-220 | $400^{f}$ | 8 | 80 | 1.6 | $8^{9}$ | 209 | 2 | $14^{t}$ | - |
| Darlington |  |  |  |  |  |  |  |  |  |  |  |
| MJD112 | MJD117 | DPak | 100 | 2 | 20 | 6.3 | 1000 | 2000 | 2 | 25 | $\cdot$ |
| TIP122 | TIP127 | TO-220 | 100 | 5 | 65 | 1.9 | 1000 | -- | 3 | -- | $\cdot$ |
| TIP142 | TIP147 | TO-218 | 100 | 10 | 125 | 1.0 | 1000 | -- | 5 | -- | $\cdot$ |
| MJ11015 | MJ11016 | TO-3 | 120 | 30 | 200 | 0.9 | 1000 | -- | 20 | 4 | $\cdot$ |
| MJ11032 | MJ11033 | TO-3 | 120 | 50 | 300 | 0.6 | 1000 | -- | 25 | -- | $\cdot$ |
| MJH11019 | MJH11020 | TO-218 | 200 v | 15 | 150 | 0.8 | 400 | -- | 10 | 3 | $\cdot$ |

Notes: (a) sorted more or less by voltage, current and families; see also additional tables in Chapter $2 x$. (b) with case at 25C. (c) $P_{\text {diss }}($ reality $)=\left(T_{J}[\right.$ your-max-value $\left.]-T a m b\right) /\left(R_{\theta J C}+R_{\theta C S}+R_{\theta S A}\right)$; this is a much lower number than the "spec," especially if you're careful with $T_{J}$ max, say $100^{\circ} \mathrm{C}$. (d) similar to TO-247. (e) higher gain grades are available. (f) much higher VCES "blocking" capability (compared with Vceo), e.g. 700V for MJE13007. (g) higher for the PNP device. (h) Pdiss $(m a x)=\left(150^{\circ} \mathrm{C}-25^{\circ} \mathrm{C}\right) / R_{\theta J C}$; this is a classic datasheet specsmanship value. (k) larger pkg version of above. (s) same as above. (t) typical. (u) higher voltage version of above. (v) there are also 150 V and 250V versions. (z) if these are hard to get, try the '028 and '029 versions (120V rather than 150V).

### 2.4.1 Push-pull output stages

As we mentioned earlier in the chapter, an npn emitter follower cannot sink current and a pnp follower cannot source current. The result is that a single-ended follower operating between split supplies can drive a ground-returned load only if a high quiescent current is used. ${ }^{50}$ The quiescent current must be at least as large as the maximum output current during peaks of the waveform, resulting in high quiescent power dissipation. For example, Figure 2.68 shows a follower circuit to drive an $8 \Omega$ loudspeaker load with up to 10 watts of audio.

An explanation of the driver stage: the pnp follower $Q_{1}$ is included to reduce drive requirements and to cancel $Q_{2}$ 's $V_{\mathrm{BE}}$ offset ( 0 V input gives approximately 0 V output).

[^6]$Q_{1}$ could, of course, be omitted for simplicity. The hefty current source in $Q_{1}$ 's emitter load is used to ensure that there is sufficient base drive to $Q_{2}$ at the top of the signal swing. A resistor as emitter load would be inferior because it would have to be a rather low value ( $50 \Omega$ or less) in order to guarantee at least 50 mA of base drive to $Q_{2}$ at the peak of the swing, when load current would be maximum and the drop across the resistor would be minimum; the resultant quiescent current in $Q_{1}$ would be excessive.

The output of this example circuit can swing to nearly $\pm 15$ volts (peak) in both directions, giving the desired output power ( 9 V rms across $8 \Omega$ ). However, the output transistor dissipates 55 watts with no signal (hence the heatsink symbol), and the emitter resistor dissipates another 110 watts. Quiescent power dissipation many times greater than the maximum output power is characteristic of this kind of class-A circuit (transistor always in conduction);
image_name:Figure 2.68
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: 8Ω, type: Resistor, value: 8Ω, ports: {N1: Vout, N2: GND}
name: 100mA, type: CurrentSource, value: 100mA, ports: {Np: VDD, Nn: ebz}
name: Q1, type: PNP, ports: {C: ebz, B: Vin, E: VDD}
name: Q2, type: NPN, ports: {C: VDD, B: ebz, E: Vout}
]
extrainfo:The circuit is a single-ended emitter follower amplifier with a PNP transistor (Q1) and an NPN transistor (Q2). It is designed to drive an 8Ω loudspeaker. The circuit operates with a quiescent power dissipation of 165 W, characteristic of class-A operation, and can output nearly ±15 V peak, providing 9 V rms across the loudspeaker.

Figure 2.68. A 10 W loudspeaker amplifier, built with a singleended emitter follower, dissipates 165 W of quiescent power!
this obviously leaves a lot to be desired in applications in which any significant amount of power is involved.
image_name:Figure 2.69
description:
[
name: Q1, type: NPN, ports: {C: +15V, B: Vin, E: Vout}
name: Q2, type: PNP, ports: {C: Vout, B: Vin, E: -15V}
name: +15V, type: VoltageSource, value: +15V, ports: {Np: +15V, Nn: GND}
name: -15V, type: VoltageSource, value: -15V, ports: {Np: GND, Nn: -15V}
]
extrainfo:This is a push-pull amplifier circuit using NPN and PNP transistors to drive a loudspeaker. Q1 conducts on positive swings, and Q2 conducts on negative swings. The circuit is designed to minimize power dissipation at zero input voltage.

Figure 2.69. Push-pull emitter follower.
Figure 2.69 shows a push-pull follower doing the same job. $Q_{1}$ conducts on positive swings, $Q_{2}$ on negative swings. With zero input voltage, there is no collector current and no power dissipation. At 10 watts of output power there is less than 10 watts of dissipation in each transistor. ${ }^{51}$

#### A. Crossover distortion in push-pull stages

There is a problem with the preceding circuit as drawn. The output trails the input by a $V_{\mathrm{BE}}$ drop; on positive swings the output is about 0.6 V less positive than the input, and the reverse for negative swings. For an input sine wave, the output would look as shown in Figure 2.70. In the language of the audio business, this is called crossover distortion. The best cure (feedback offers another method, although by itself it is not entirely satisfactory; see §4.3.1E) is to bias the push-pull stage into slight conduction, as in Figure 2.71.

The bias resistors $R$ bring the diodes into forward conduction, holding $Q_{1}$ 's base a diode drop above the input

[^7]image_name:Figure 2.70
description:The graph in Figure 2.70 is a time-domain waveform that illustrates crossover distortion in a push-pull amplifier. The x-axis represents time, and the y-axis represents voltage. Both axes are on a linear scale, with no specific units or markers provided.

The graph displays two waveforms: 'signal in' and 'signal out'. The 'signal in' waveform is a smooth sinusoidal curve representing the input sine wave. The 'signal out' waveform, however, deviates from this smooth curve, particularly noticeable at the zero-crossing points where the waveform transitions from positive to negative and vice versa.

The key feature of this graph is the presence of crossover distortion, highlighted by an annotated circle. This distortion occurs around the zero-crossing region where the output signal momentarily flattens instead of following the smooth curve of the input signal. This flattening indicates a brief period where neither of the output transistors in the push-pull amplifier is conducting, resulting in a distortion in the output waveform.

Overall, the graph effectively demonstrates the concept of crossover distortion by contrasting the ideal input signal with the distorted output signal, emphasizing the need for proper biasing to eliminate this distortion.

Figure 2.70. Crossover distortion in the push-pull follower.
image_name:Figure 2.71
description:
[
name: Q1, type: NPN, ports: {C: +VCC, B: b1a1, E: Vout}
name: Q2, type: PNP, ports: {C: Vout, B: b2k2, E: -VEE}
name: D1, type: Diode, ports: {Na: b1a1, Nc: Vin}
name: D2, type: Diode, ports: {Na: Vin, Nc: b2k2}
name: R1, type: Resistor, value: R, ports: {N1: +VCC, N2: b1a1}
name: R2, type: Resistor, value: R, ports: {N1: b2k2, N2: -VEE}
name: R3, type: Resistor, value: 100Ω, ports: {N1: Vin, N2: Vout}
]
extrainfo:This circuit is a push-pull amplifier with biasing to eliminate crossover distortion. The diodes D1 and D2 provide the necessary biasing to ensure that one of the transistors Q1 or Q2 is always conducting, minimizing distortion. Resistors R1 and R2 set the bias current, and the 100Ω resistor provides load balancing.

Figure 2.71. Biasing the push-pull follower to eliminate crossover distortion.
signal and $Q_{2}$ 's base a diode drop below the input signal. Now, as the input signal crosses through zero, conduction passes from $Q_{2}$ to $Q_{1}$; one of the output transistors is always on. The value $R$ of the base resistors is chosen to provide enough base current for the output transistors at the peak output swing. For instance, with $\pm 20 \mathrm{~V}$ supplies and an $8 \Omega$ load running up to 10 watts sinewave power, the peak base voltage is about 13.5 volts and the peak load current is about 1.6 amps . Assuming a transistor beta of 50 (power transistors generally have lower current gain than small-signal transistors), the 32 mA of necessary base current will require base resistors of about $220 \Omega(6.5 \mathrm{~V}$ from $V_{\mathrm{CC}}$ to base at peak swing).

In this circuit we've added a resistor from input to output (this could have been done in Figure 2.69 as well). This serves to eliminate the "dead zone" as conduction passes from one transistor to the other (particularly in the first circuit), which is desirable especially when this circuit is included within a larger feedback circuit. However, it does not substitute for the better procedure of linearizing by biasing, as in Figure 2.71, to achieve transistor conduction over the full output waveform. We have more to say about this in Chapter $2 x$.
B. Thermal stability in class-B push-pull amplifiers The preceding amplifier has one unfortunate feature: it is not thermally stable. As the output transistors warm up (and they will get hot, because they are dissipating power when signal is applied), their $V_{\mathrm{BE}}$ drops, causing quiescent current to flow. The added heat this produces causes the situation to get worse, with the strong possibility of what is called thermal runaway (whether it runs away or not depends on a number of factors, including how large a "heatsink" is used, how well the diode's temperature tracks the transistor's temperature, etc.). Even without runaway, better control over the circuit is needed, usually with the sort of arrangement shown in Figure 2.72.
image_name:Figure 2.72
description:
[
name: R1, type: Resistor, value: 470Ω, ports: {N1: VCC, N2: b2}
name: R2, type: Resistor, value: 50Ω, ports: {N1: b2, N2: a1}
name: R3, type: Resistor, value: 1Ω, ports: {N1: b2, N2: Vout}
name: R4, type: Resistor, value: 1Ω, ports: {N1: Vout, N2: e3}
name: Q1, type: NPN, ports: {C: b2, B: b1, E: e1}
name: Q2, type: NPN, ports: {C: VCC, B: b2, E: Vout}
name: Q3, type: PNP, ports: {C: Vout, B: b3k2, E: e3}
name: D1, type: Diode, ports: {Na: a1, Nc: b3k1}
name: V2, type: VoltageSource, ports: {Np: b3k1, Nn: b3k2}
]
extrainfo:The circuit is a push-pull follower designed to improve thermal stability by using small emitter resistors. It includes NPN and PNP transistors, diodes for biasing, and resistors for current control. The input is from the collector of the previous stage, and the output is labeled as Vout.

Figure 2.72. Adding (small) emitter resistors improve thermal stability in the push-pull follower.

For variety, the input is shown coming from the collector of the previous stage; $R_{1}$ now serves the dual purpose of being $Q_{1}$ 's collector resistor, and also providing current to bias the diodes and bias-setting resistor in the push-pull base circuit. Here $R_{3}$ and $R_{4}$, typically a few ohms or less, provide a "cushion" for the critical quiescent current biasing: the voltage between the bases of the output transistors must now be a bit greater than two diode drops, and you provide the extra with adjustable biasing resistor $R_{2}$ (often replaced with a third series diode, or, better, with the more elegant biasing circuit of Figure 2.78 on page 111). With a few tenths of a volt across $R_{3}$ and $R_{4}$, the temperature variation of $V_{\mathrm{BE}}$ doesn't cause the current to rise very rapidly (the larger the drop across $R_{3}$ and $R_{4}$, the less sensitive it is), and the circuit will be stable. Stability is improved by mounting the diodes ${ }^{52}$

[^8]in physical contact with the output transistors (or their heatsinks).

You can estimate the thermal stability of such a circuit by remembering that the base-emitter drop decreases by about 2.1 mV for each $1^{\circ} \mathrm{C}$ rise, and that the collector current increases by a factor of 10 for every 60 mV increase in base-emitter voltage (or $4 \%$ per mV ). For example, if $R_{2}$ were replaced with a diode, you would have three diode drops between the bases of $Q_{2}$ and $Q_{3}$, leaving about one diode drop across the series combination of $R_{3}$ and $R_{4}$. (The latter would then be chosen to give an appropriate quiescent current, perhaps 100 mA for an audio power amplifier.) The worst case for thermal stability occurs if the biasing diodes are not thermally coupled to the output transistors.

Let us assume the worst and calculate the increase in output-stage quiescent current corresponding to a $30^{\circ} \mathrm{C}$ temperature rise in output transistor temperature. That's not a lot for a power amplifier, by the way. For that temperature rise, the $V_{\mathrm{BE}}$ of each output transistor will decrease by about 63 mV at constant current, raising the voltage across $R_{3}$ and $R_{4}$ by about $50 \%$ (i.e., the quiescent current will rise by about $50 \%$ ). The corresponding figure for the preceding amplifier circuit without emitter resistors (Figure 2.71) will be a factor of 10 rise in quiescent current (recall that $I_{C}$ increases a decade per 60 mV increase in $V_{\mathrm{BE}}$ ), i.e., $1000 \%$. The improved thermal stability of this biasing arrangement (even without having the diodes thermally coupled to the output transistors) is evident. And you'll do significantly better when the diodes (or diode-connected transistors, or, best of all, $V_{\mathrm{BE}}$-referenced biasing as shown in Figure 2.78) ride along on the heatsink.

This circuit has the additional advantage that, by adjusting the quiescent current, you have some control over the amount of residual crossover distortion. A push-pull amplifier biased in this way to obtain substantial quiescent current at the crossover point is sometimes referred to as a "class-AB" amplifier, meaning that both transistors conduct simultaneously during a significant portion of the cycle. In practice, you choose a quiescent current that is a good compromise between low distortion and excessive quiescent dissipation. Feedback, introduced later in this chapter (and exploited shamelessly, and with joy, in Chapter 4), is almost always used to reduce distortion still further.

We will see a further evolution of this circuit in §2.4.2, where we supplement it with the intriguingly named techniques of $V_{\mathrm{BE}}$-referenced biasing, collector bootstrapping, and $\beta$-boosting complementary Darlington output stage.

#### C. "Class-D" amplifiers

An interesting solution to this whole business of power dissipation (and distortion) in class-AB linear power amplifiers is to abandon the idea of a linear stage entirely and use instead a switching scheme: imagine that the push-pull follower transistors $Q_{2}$ and $Q_{3}$ in Figure 2.72 are replaced with a pair of transistor switches, with one ON and the other ofF at any time, so that the output is switched completely to $+V_{\mathrm{CC}}$ or to $-V_{\mathrm{CC}}$ at any instant. Imagine also that these switches are operated at a high frequency (say at least 10 times the highest audio frequency) and that their relative timing is controlled (by techniques we'll see later, in Chapters $10-13$ ) such that the average output voltage is equal to the desired analog output. Finally, we add an $L C$ lowpass filter to kill the high switching signal, leaving the desired (lower-frequency) analog output intact.

This is a Class-D, or switching amplifier. It has the advantage of very high efficiency, because the switching transistors are either off (no current) or in saturation (near-zero voltage); that is, the power dissipated in the switching transistors (the product $V_{\mathrm{CE}} \times I_{\mathrm{C}}$ ) is always small. There's also no worry about thermal runaway. The downsides are the problems of emission of high-frequency noise, switching feedthrough to the output, and the difficulty of achieving excellent linearity.

Class-D amplifiers are nearly universal in inexpensive audio equipment, and they are increasingly finding their way into high-end audio equipment. Figure 2.73 shows measured waveforms of an inexpensive (and tiny!) class-D amplifier IC driving a $5 \Omega$ load with a sinewave at the high end of the audio range ( 20 kHz ). This particular IC uses a 250 kHz switching frequency, and can drive 20 watts each into a pair of stereo speakers; pretty much everything you need (except for the output $L C$ filters) is on the chip, which costs about $\$ 3$ in small quantities. Pretty neat.

### 2.4.2 Darlington connection

If you hook two transistors together as in Figure 2.74, the result - called a Darlington connection ${ }^{53}$ (or Darlington pair) - behaves like a single transistor with beta equal to the product of the two transistor betas. ${ }^{54}$ This can be very handy where high currents are involved (e.g., voltage regulators or power amplifier output stages), or for input stages

[^9]image_name:Figure 2.73
description:The graph in Figure 2.73 depicts the waveforms associated with a Class-D amplifier. It shows three distinct waveforms: the analog input, the PWM (pulse-width modulated) output before filtering, and the analog output after filtering. The horizontal axis represents time with a scale of 10 microseconds per division.

1. **Analog Input (Top Waveform):** The analog input waveform is a sine wave with a frequency of 20 kHz, as indicated by the context. The vertical scale is 1 volt per division. The waveform is smooth and periodic, indicating a consistent sine wave input.

2. **PWM Output (Middle Waveform):** This waveform represents the pulse-width modulated signal that controls the duty cycle of the amplifier. The vertical scale is 5 volts per division. The waveform consists of a series of rapid, rectangular pulses, where the width of each pulse varies according to the amplitude of the input sine wave. This PWM signal is characterized by high-frequency switching and is used to drive the amplifier’s output stage.

3. **Analog Output (Bottom Waveform):** After passing through an LC lowpass filter, the PWM signal is smoothed out to recreate the original input sine wave. The vertical scale for this waveform is also 5 volts per division. The output waveform closely resembles the original analog input, demonstrating the effectiveness of the filtering process in suppressing high-frequency components and reproducing the desired audio signal.

Overall, the graph illustrates the process of converting an analog input to a PWM signal for amplification and then back to an analog output, highlighting the efficiency and functionality of a Class-D amplifier system.

Figure 2.73. Class-D amplifier waveforms: a 20 kHz input sinewave controls the "duty cycle" (fraction of time the output is HIGH) of a push-pull switched output. These waveforms are from a TPA3123 stereo amplifier chip running from +15 V , and show the prefiltered PWM (pulse-width modulated) output, and the final smoothed output after the LC lowpass output filter. Horizontal: $10 \mu \mathrm{~s} / \mathrm{div}$.
of amplifiers where very high input impedance is necessary.
image_name:Figure 2.74
description:
[
name: Q1, type: NPN, ports: {C: C, B: B, E: e1b2}
name: Q2, type: NPN, ports: {C: C, B: e1b2, E: E}
]
extrainfo:The circuit is a Darlington pair configuration, which increases current gain with the product of individual gains (β = β1β2). The base-emitter drop is twice normal, and the saturation voltage is at least one diode drop.

Figure 2.74. Darlington transistor configuration.
For a Darlington transistor the base-emitter drop is twice normal and the saturation voltage is at least one diode drop (since $Q_{1}$ 's emitter must be a diode drop above $Q_{2}$ 's emitter). Also, the combination tends to act like a rather slow transistor because $Q_{1}$ cannot turn off $Q_{2}$ quickly. This problem is usually taken care of by including a resistor from base to emitter of $Q_{2}$ (Figure 2.75). Resistor $R$ also prevents leakage current through $Q_{1}$ from biasing $Q_{2}$ into conduction; ${ }^{55}$ its value is chosen so that $Q_{1}$ 's leakage current (nanoamps for small-signal transistors, as much as hundreds of microamps for power transistors) produces less than a diode drop across $R$, and so that $R$ doesn't sink a large proportion of $Q_{2}$ 's base current when it has a diode drop across it. Typically $R$ might be a few hundred ohms in

[^10]a power transistor Darlington, or a few thousand ohms for a small-signal Darlington.

Darlington transistors are available as single packages, usually with the base-emitter resistor included. A typical example is the $n p n$ power Darlington MJH6284 (and pnp cousin MJH6287), with a current gain of 1000 (typical) at a collector current of 10 amps . Another popular power Darlington is the inexpensive $n p n$ TIP142 (and pnp cousin TIP147): these cost $\$ 1$ in small quantities and have typical $\beta=4000$ at $I_{\mathrm{C}}=5 \mathrm{~A}$. And for small-signal applications we like the widely available MPSA14 or MMBTA14 (in TO-92 and SOT23 packages, respectively), with a minimum beta of 10,000 at 10 mA and 20,000 at 100 mA . These 30 volt parts have no internal base-emitter resistor (so you can use them at very low currents); they cost less than $\$ 0.10$ in small quantities. Figure 2.76 shows beta versus collector current for these parts; note the pleasantly high values of beta, but with substantial dependence both on temperature and on collector current.
image_name:Figure 2.75
description:
[
name: Q1, type: NPN, ports: {C: C, B: B, E: eb2}
name: Q2, type: NPN, ports: {C: C, B: eb2, E: E}
name: R, type: Resistor, value: R, ports: {N1: eb2, N2: E}
]
extrainfo:This circuit diagram shows a Darlington pair configuration with two NPN transistors (Q1 and Q2) to improve current gain. The overall beta (β) of the configuration is the product of the individual betas of Q1 and Q2 (β = β1β2). A resistor R is connected between the emitter of Q1 and the base of Q2.

Figure 2.75. Improving turn-off speed in a Darlington pair. (The beta formula is valid as long as $R$ does not rob significant base current from $Q_{2}$.)
image_name:Figure 2.76
description:The graph in Figure 2.76 is a plot of DC current gain (beta, \(h_{FE}\)) versus collector current (\(I_C\)) for the MPSA14 NPN Darlington transistor. It is a typical performance graph adapted from the datasheet, illustrating how the current gain varies with different collector currents and junction temperatures.

1. **Type of Graph and Function:**
- This is a performance graph depicting the relationship between DC current gain and collector current.

2. **Axes Labels and Units:**
- The x-axis represents the collector current (\(I_C\)) in milliamperes (mA), ranging from 5 mA to 500 mA.
- The y-axis represents the DC current gain (beta, \(h_{FE}\)), on a logarithmic scale, ranging from 2k to 200k.

3. **Overall Behavior and Trends:**
- The graph shows three curves, each corresponding to a different junction temperature: \(T_J = 125^\circ C\), \(25^\circ C\), and \(-55^\circ C\).
- For each temperature, the DC current gain increases with collector current, reaching a peak and then slightly decreasing at higher collector currents.
- The current gain is higher at elevated temperatures (\(125^\circ C\)) and lower at reduced temperatures (\(-55^\circ C\)).

4. **Key Features and Technical Details:**
- The peak current gain values occur at different collector currents depending on the temperature. The gain is highest at \(T_J = 125^\circ C\) and lowest at \(-55^\circ C\).
- The graph demonstrates how thermal conditions affect the efficiency and performance of the Darlington pair.

5. **Annotations and Specific Data Points:**
- The graph includes annotations indicating the junction temperatures for each curve.
- Significant gridlines are present at key gain values (5k, 10k, 50k, 100k) to aid in reading the graph's values.

Figure 2.76. Typical beta versus collector current for the popular MPSA14 npn Darlington (adapted from the datasheet).
image_name:Figure 2.77
description:
[
name: Q1, type: NPN, ports: {C: C, B: B, E: E}
name: Q2, type: PNP, ports: {C: C, B: E, E: E}
name: Q3, type: NPN, ports: {C: C, B: B, E: E}
name: RB, type: Resistor, value: RB, ports: {N1: B, N2: C}
name: Cb2, type: Capacitor, value: Cb2, ports: {Np: B, Nn: C}
]
extrainfo:The circuit diagram illustrates a Sziklai pair configuration, also known as a complementary Darlington pair, which increases the current gain. The effective beta (β) of the configuration is the product of the individual transistors' beta values (β = β1β2). This configuration behaves like a single NPN transistor with a high current gain.

Figure 2.77. Sziklai connection ("complementary Darlington").

#### A. Sziklai connection

A similar beta-boosting configuration is the Sziklai connection, ${ }^{56}$ sometimes referred to as a complementary Darlington (Figure 2.77). This combination behaves like an npn transistor, again with large beta. It has only a single base-emitter drop, but (like the Darlington) it also cannot saturate to less than a diode drop. A resistor from base to emitter of $Q_{2}$ is advisable, for the same reasons as with the Darlington (leakage current; speed; stability of $V_{\mathrm{BE}}$ ). This connection is common in push-pull power output stages in which the designer may wish to use one polarity of highcurrent output transistor only. However, even when used as complementary polarity pairs, it is generally to be preferred over the Darlington for amplifiers and other linear applications; that is because it has the advantage of a single $V_{\mathrm{BE}}$ drop (versus two), and that voltage drop is stabilized by the base-emitter resistor of the output transistor. For example, if $R_{\mathrm{B}}$ is chosen such that its current (with a nominal $V_{\mathrm{BE}}$ drop across it) is $25 \%$ of the output transistor's base current at peak output, then the driver transistor sees a collector current that ranges over only a factor of 5; so its $V_{\mathrm{BE}}$ (which is the Sziklai's $V_{\mathrm{BE}}$ ) varies only $40 \mathrm{mV}\left(V_{\mathrm{T}} \ln 5\right)$ over the full output current swing. The Sziklai configuration is discussed in more detail in Chapter 2x (see §2x.10); and you'll find nice examples of circuits that rely on the

[^11]Sziklai's unique properties in that chapter's section "BJT amplifier distortion: a SPICE exploration."

Figure 2.78 shows a nice example of a push-pull Sziklai output stage. This has an important advantage compared with the Darlington alternative, namely that the biasing of the $Q_{3} Q_{5}$ pair into class-AB conduction (to minimize crossover distortion) has just two base-emitter drops, rather than four; and, more importantly, $Q_{3}$ and $Q_{5}$ are running cool compared with the output transistors ( $Q_{4}$ and $Q_{6}$ ), so they can be relied upon to have a stable baseemitter drop. This allows higher quiescent currents than with the conventional Darlington, where you have to leave a larger safety margin; bottom line, lower distortion. ${ }^{57}$

In this circuit $Q_{2}$ functions as an "adjustable $V_{\mathrm{BE}}$ multiplier" for biasing, here settable from 1 to $3.5 V_{\mathrm{BE}}$ 's; it is bypassed at signal frequencies. Another circuit trick is the "bootstrapping" of $Q_{1}$ 's collector resistor by $C_{1}$ (see §2.4.3), raising its effective resistance at signal frequencies and increasing the amplifier's loop gain to produce lower distortion.

#### B. Superbeta transistor

The Darlington connection and its near relatives should not be confused with the so-called superbeta transistor, a device with very high current gain achieved through the manufacturing process. A typical superbeta transistor is the 2N5962, with a guaranteed minimum current gain of 450 at collector currents from $10 \mu \mathrm{~A}$ to 10 mA (see, for example, Table 8.1a on page 501. Superbeta matched pairs are available for use in low-level amplifiers that require matched characteristics, for example the differential amplifier of §2.3.8. Legendary examples are the LM394 and MAT-01 series; these provide high-gain $n p n$ transistor pairs whose $V_{\mathrm{BE}}$ 's are matched to a fraction of a millivolt (as little as $50 \mu \mathrm{~V}$ in the best versions) and whose betas are matched to about $1 \%$. The MAT-03 is a $p n p$ matched pair (see Table 8.1 b on page 502). Some commercial op-amps use superbeta differential input stages to achieve input (i.e., base bias) currents as low as 50 picoamps this way; examples are the LT1008 and LT1012.

### 2.4.3 Bootstrapping

When biasing an emitter follower, for instance, you choose the base voltage-divider resistors so that the divider presents a stiff voltage source to the base, i.e., their par-

[^12]image_name:Figure 2.78
description:
[
name: R1, type: Resistor, value: 3.6k, ports: {N1: +75V, N2: X1}
name: R2, type: Resistor, value: 3.6k, ports: {N1: X1, N2: C2b3}
name: R3, type: Resistor, value: 100, ports: {N1: +75V, N2: C3b4}
name: R4, type: Resistor, value: 0.5Ω, ports: {N1: C3e4, N2: X2}
name: R5, type: Resistor, value: 0.5Ω, ports: {N1: e5C6, N2: X2}
name: R6, type: Resistor, value: 100, ports: {N1: X3, N2: C5b6}
name: C1, type: Capacitor, value: 47μF, 50V, ports: {Np: X1, Nn: X2}
name: C2, type: Capacitor, value: 10μF, ports: {Np: C2b3, Nn: X3}
name: Q1, type: NPN, ports: {C: X3, B: X3, E: b2}
name: Q2, type: NPN, ports: {C: C2b3, B: b2, E: X3}
name: Q3, type: NPN, ports: {C: C3b4, B: C2b3, E: e3C4}
name: Q4, type: PNP, ports: {C: e3C4, B: C3b4, E: +75V}
name: Q5, type: PNP, ports: {C: e5C6, B: C5b6, E: X3}
name: Q6, type: NPN, ports: {C: X2, B: e5C6, E: -75V}
]
extrainfo:This circuit is a push-pull power stage with Sziklai-pair output transistors, capable of output swings to ±70V and output currents of ±2A peak. It includes a bias network to lower input impedance and uses a 10mA bias current through Q2.

Figure 2.78. Push-pull power stage with Sziklai-pair output transistors, capable of output swings to $\pm 70 \mathrm{~V}$ and output currents of $\pm 2 \mathrm{~A}$ peak.
image_name:Figure 2.79
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: 0.1μF, type: Capacitor, value: 0.1μF, ports: {Np: Vin, Nn: b1}
name: 20k_1, type: Resistor, value: 20k, ports: {N1: Vcc, N2: b1}
name: 20k_2, type: Resistor, value: 20k, ports: {N1: b1, N2: GND}
name: Q1, type: NPN, ports: {C: Vcc, B: b1, E: Vout}
name: 1.0k, type: Resistor, value: 1.0k, ports: {N1: Vout, N2: GND}
]
extrainfo:This circuit is a bias network that lowers input impedance, dominated by the voltage divider. The input resistance is about 9.1kΩ, mainly due to the 10kΩ voltage divider impedance.

Figure 2.79. Bias network lowers input impedance.
allel impedance is much less than the impedance looking into the base. For this reason the resulting circuit has an input impedance dominated by the voltage divider - the driving signal sees a much lower impedance than would otherwise be necessary. Figure 2.79 shows an example. The input resistance of about 9.1 k is mostly due to the voltagedivider impedance of 10 k . It is always desirable to keep input impedances high, and anyway it's a shame to load the input with the divider, which, after all, is only there to bias the transistor.
"Bootstrapping" is the colorful name given to a technique that circumvents this problem (Figure 2.80). The
transistor is biased by the divider $R_{1} R_{2}$ through series resistor $R_{3}$. Capacitor $C_{2}$ is chosen to have low impedance at signal frequencies compared with the bias resistors. As always, bias is stable if the dc impedance seen from the base (in this case 9.7 k ) is much less than the dc impedance looking into the base (in this case approximately 100k). But now the signal-frequency input impedance is no longer the same as the dc impedance. Look at it this way: an input wiggle $v_{\text {in }}$ results in an emitter wiggle $v_{\mathrm{E}} \approx v_{\mathrm{in}}$. So the change in current through bias resistor $R_{3}$ is $i=$ $\left(v_{\text {in }}-v_{\mathrm{E}}\right) / R_{3} \approx 0$, i.e., $Z_{\text {in }}$ (of the bias string) $=v_{\text {in }} / i_{\text {in }} \approx$ infinity. We've made the loading (shunt) impedance of the bias network very large at signal frequencies.
image_name:Figure 2.80
description:
[
name: C1, type: Capacitor, value: 0.1uF, ports: {Np: Vin, Nn: b1}
name: R1, type: Resistor, value: 10k, ports: {N1: b1, N2: Vcc}
name: R2, type: Resistor, value: 10k, ports: {N1: X1, N2: GND}
name: R3, type: Resistor, value: 4.7k, ports: {N1: b1, N2: X1}
name: R4, type: Resistor, value: 1.0k, ports: {N1: Vout, N2: GND}
name: C2, type: Capacitor, value: 10uF, ports: {Np: X1, Nn: Vout}
name: Q1, type: NPN, ports: {C: Vcc, B: b1, E: Vout}
]
extrainfo:The circuit is an emitter follower with bootstrapped bias to raise input impedance.

Figure 2.80. Raising the input impedance of an emitter follower at signal frequencies by bootstrapping the base bias divider.

Another way of seeing this is to notice that $R_{3}$ always has the same voltage across it at signal frequencies (since both ends of the resistor have the same voltage changes), i.e., it's a current source. But a current source has infinite impedance. In reality the effective impedance is less than infinity because the gain of a follower is slightly less than unity. That is so because the base-emitter drop depends on collector current, which changes with the signal level. You could have predicted the same result from the voltagedividing effect of the impedance looking into the emitter $\left[r_{\mathrm{e}}=25 / I_{\mathrm{C}}(\mathrm{mA})\right.$ ohms $]$ combined with the emitter resistor. If the follower has voltage gain $A$ (slightly less than unity), the effective value of $R_{3}$ at signal frequencies is

$$
R_{3} /(1-A)
$$

The voltage gain of a follower can be written $A=R_{\mathrm{L}} /\left(R_{\mathrm{L}}+r_{\mathrm{e}}\right)$, where $R_{\mathrm{L}}$ is the total load seen at the emitter (here $R_{1}\left\|R_{2}\right\| R_{4}$ ), so the effective value of bias resistor $R_{3}$ at signal frequencies can be written as $R_{3} \rightarrow$ $R_{3}\left(1+R_{\mathrm{L}} / r_{\mathrm{e}}\right)$. In practice the value of $R_{3}$ is effectively increased by a hundred or so, and the input impedance is then dominated by the transistor's base impedance. The emitterdegenerated amplifier can be bootstrapped in the same way,
since the signal on the emitter follows the base. The bias divider circuit is driven by the low-impedance emitter output at signal frequencies, which is what isolates the input signal from this usual task, and makes possible the beneficial increase of input impedance.

#### A. Bootstrapping collector load resistors

The bootstrap principle can be used to increase the effective value of a transistor's collector load resistor, if that stage drives a follower. That can increase the voltage gain of the stage substantially - recall that $G_{\mathrm{V}}=-g_{m} R_{\mathrm{C}}$, with $g_{m}=1 /\left(R_{\mathrm{E}}+r_{\mathrm{e}}\right)$. This technique is used in Figure 2.78, where we bootstrapped $Q_{1}$ 's collector load resistor $\left(R_{2}\right)$, forming an approximate current-source load. This serves two useful functions: (a) it raises the voltage gain of $Q_{1}$, and (b) it provides base drive current to $Q_{3} Q_{4}$ that does not drop off toward the top of the swing (as would a resistive load, just when you need it most).

### 2.4.4 Current sharing in paralleled BJTs

It's not unusual in power electronics design to find that the power transistor you've chosen is not able to handle the required power dissipation, and needs to share the job with additional transistors. This is a fine idea, but you need a way to ensure that each transistor handles an equal portion of the power dissipation. In $\S 9.13 .5$ we illustrate the use of transistors in series. This can simplify the problem, because we know they'll all be running at the same current. But it's often more attractive to divide up the current by connecting the transistors in parallel, as in Figure 2.81A.

There are two problems with this approach. First, we know the bipolar transistor is a transconductance device, with its collector current determined in a precise way by its base-to-emitter voltage $V_{\mathrm{BE}}$, as given by the Ebers-Moll equations 2.8 and 2.9. As we saw in $\S 2.3 .2$, the temperature coefficient of $V_{\mathrm{BE}}$ (at constant collector current) is about $-2.1 \mathrm{mV} /{ }^{\circ} \mathrm{C}$; or, equivalently, $I_{\mathrm{C}}$ increases with temperature for a fixed $V_{\mathrm{BE}} .{ }^{58}$ This is unfortunate, because if the junction of one of the transistors becomes hotter than the rest, it takes more of the total current, thereby heating up even more. It's in danger of the dreaded thermal runaway.

The second problem is that transistors of the same part number are not identical. They come off the shelf with

[^13]differing values of $V_{\mathrm{BE}}$ for a given $I_{\mathrm{C}}$. This is true even for parts made at the same time on the same fabrication line, and from the same silicon wafer. To see how large a variation you are likely to get, we measured 100 adjacent ZTX851 transistors on a reel, with an observed spread of about 17 mV , shown in Figure 8.44. This really represents a "best case," because you cannot be certain that a batch of incoming transistors derive from a single lot, much less a single wafer. When you first build something, the $V_{\mathrm{BE}}$ 's of "identical" transistors may be within $20-50 \mathrm{mV}$ of each other, but that matching is lost when one of them has to be replaced someday. It's always safer to assume a possible 100 mV or so spread of base-emitter voltages. Recalling that $\Delta V_{\mathrm{BE}}=60 \mathrm{mV}$ corresponds to a factor of ten current ratio, it's clear that you cannot get away with a direct parallel connection like Figure 2.81A.

The usual solution to this problem is the use of small resistors in the emitters, as shown in Figure 2.81B. These are called emitter-ballasting resistors, and their value is chosen to drop at least a few tenths of a volt at the higher end of the anticipated operating current range. That voltage drop must be adequate to swamp the $V_{\mathrm{BE}}$ spread of the individual transistors, and is ordinarily chosen somewhere in the range of $300-500 \mathrm{mV}$.
image_name:Figure 2.81A
description:
[
name: Q1, type: NPN, ports: {C: VDD, B: Vin, E: GND}
name: Q2, type: NPN, ports: {C: VDD, B: Vin, E: GND}
name: Q3, type: NPN, ports: {C: VDD, B: Vin, E: GND}
]
extrainfo:Figure 2.81A shows three NPN transistors (Q1, Q2, Q3) connected in parallel without emitter ballasting resistors, which can lead to current imbalance issues.
image_name:Figure 2.81B
description:
[
name: Q1, type: NPN, ports: {C: LOAD1, B: LOAD2, E: N1}
name: Q2, type: NPN, ports: {C: LOAD1, B: LOAD2, E: N2}
name: Q3, type: NPN, ports: {C: LOAD1, B: LOAD2, E: N3}
name: R_E, type: Resistor, value: R_E, ports: {N1: N1, N2: LOAD2}
name: R_E, type: Resistor, value: R_E, ports: {N1: N2, N2: LOAD2}
name: R_E, type: Resistor, value: R_E, ports: {N1: N3, N2: LOAD2}
]
extrainfo:Figure 2.81B demonstrates the use of emitter-ballasting resistors (R_E) to equalize the currents of parallel transistors Q1, Q2, and Q3. These resistors help in maintaining balanced emitter currents among the transistors.

Figure 2.81. To equalize the currents of parallel transistors, use emitter ballasting resistors $R_{\mathrm{E}}$, as in circuit B .

At high currents the resistors may suffer from an inconveniently-high power dissipation, so you may want to use the current-sharing trick shown in Figure 2.82. Here the current-sensing transistors $Q_{4}-Q_{6}$ adjust the base drive to the "paralleled" power transistors $Q_{1}-Q_{3}$ to maintain equal emitter currents (you can think of $Q_{4}-Q_{6}$ as a high-gain differential amplifier with three inputs). This "active ballast" technique works well with power Darlington BJTs, and it works particularly well with MOSFETs (see Figure 3.117), thanks to their negligible input (gate) current, thus making

MOSFETs a good choice for circuits with lots of power dissipation. ${ }^{59}$
image_name:Figure 2.82
description:
[
name: Q1, type: NPN, ports: {C: C, B: B, E: bc4}
name: Q2, type: NPN, ports: {C: C, B: B, E: bc5}
name: Q3, type: NPN, ports: {C: C, B: B, E: bc6}
name: Q4, type: NPN, ports: {C: bc4, B: B, E: eb4}
name: Q5, type: NPN, ports: {C: bc5, B: B, E: eb5}
name: Q6, type: NPN, ports: {C: bc6, B: B, E: eb6}
name: R1, type: Resistor, value: 220, ports: {N1: B, N2: bc4}
name: R1, type: Resistor, value: 220, ports: {N1: B, N2: bc5}
name: R1, type: Resistor, value: 220, ports: {N1: B, N2: bc6}
name: RE, type: Resistor, value: RE, ports: {N1: eb4, N2: E}
name: RE, type: Resistor, value: RE, ports: {N1: eb5, N2: E}
name: RE, type: Resistor, value: RE, ports: {N1: eb6, N2: E}
name: RE, type: Resistor, value: 0.05Ω, ports: {N1: E, N2: X1}
name: Current Source, type: CurrentSource, value: 30mA, ports: {Np: X1, Nn: GND}
]
extrainfo:The circuit implements active ballasting for parallel power transistors Q1-Q3 using feedback from current sensing transistors Q4-Q6 to ensure equal emitter currents. Each power transistor is paired with a sensing transistor to adjust its base drive, maintaining balance in the circuit. This configuration is effective for managing power dissipation, especially with MOSFETs.

Figure 2.82. Active ballasting of parallel transistors $Q_{1}-Q_{3}$ via feedback from current sensing transistors $Q_{4}-Q_{6}$ lets you configure a parallel power transistors with very low drops across the emitter resistors.

### 2.4.5 Capacitance and Miller effect

In our discussion so far we have used what amounts to a dc, or low-frequency, model of the transistor. Our simple current amplifier model and the more sophisticated EbersMoll transconductance model both deal with voltages, currents, and resistances seen at the various terminals. With these models alone we have managed to go quite far, and in fact these simple models contain nearly everything you will ever need to know to design transistor circuits. However, one important aspect that has serious impact on highspeed and high-frequency circuits has been neglected: the existence of capacitance in the external circuit and in the transistor junctions themselves. Indeed, at high frequencies the effects of capacitance often dominate circuit behavior; at 100 MHz a typical junction capacitance of 5 pF has an impedance of just $320 \Omega$ !

In this brief subsection we introduce the problem, illustrate some of its circuit incarnations, and suggest some methods of circumventing its effects. It would be a mistake to leave this chapter without realizing the nature of this problem. In the course of this brief discussion we will encounter the infamous Miller effect, and the use of configurations such as the cascode to overcome it.

[^14]
#### A. Junction and circuit capacitance

Capacitance limits the speed at which the voltages within a circuit can swing ("slew rate"), owing to finite driving impedance or current. When a capacitance is driven by a finite source resistance, you see $R C$ exponential charging behavior, whereas a capacitance driven by a current source leads to slew-rate-limited waveforms (ramps). As general guidance, reducing the source impedances and load capacitances and increasing the drive currents within a circuit will speed things up. However, there are some subtleties connected with feedback capacitance and input capacitance. Let's take a brief look.
image_name:Figure 2.83
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: b1, E: e1}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: b1}
name: RL, type: Resistor, value: RL, ports: {N1: Vcc, N2: Vout}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: b1}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
name: Ccb, type: Capacitor, value: Ccb, ports: {Np: b1, Nn: Vout}
name: Cbe, type: Capacitor, value: Cbe, ports: {Np: b1, Nn: e1}
]
extrainfo:The circuit is a transistor amplifier with junction and load capacitances. It includes an NPN transistor (Q1) with resistors RS and RL, and capacitors C1, CL, Ccb, and Cbe. The input is at Vin and the output is at Vout. The circuit demonstrates the effects of junction capacitance on amplifier performance.

Figure 2.83. Junction and load capacitances in a transistor amplifier.

The circuit in Figure 2.83 illustrates most of the problems of junction capacitance. The output capacitance forms a time constant with the output resistance $R_{\mathrm{L}}$ ( $R_{\mathrm{L}}$ includes both the collector and load resistances, and $C_{\mathrm{L}}$ includes both junction and load capacitances), giving a rolloff starting at some frequency $f=1 / 2 \pi R_{\mathrm{L}} C_{\mathrm{L}}$.

The same is true for the input capacitance, $C_{\mathrm{be}}$, in combination with the source impedance $R_{\mathrm{S}}$. Of greater significance, at high frequencies the input capacitance robs base current, effectively decreasing the transistor's beta. In fact, transistor datasheets specify a cutoff frequency, $f_{\mathrm{T}}$, at which the beta has decreased to unity - not much of an amplifier anymore! We discuss this further in Chapter $2 x$.

#### B. Miller effect

The feedback impedance $C_{\mathrm{cb}}$ is another matter. The amplifier has some overall voltage gain $G_{\mathrm{V}}$, so a small voltage wiggle at the input results in a wiggle $G_{\mathrm{V}}$ times larger (and inverted) at the collector. This means that the signal source sees a current through $C_{\mathrm{cb}}$ that is $G_{\mathrm{V}}+1$ times as large as if $C_{\mathrm{cb}}$ were connected from base to ground; i.e., for the pur-
pose of input rolloff frequency calculations, the feedback capacitance behaves like a capacitor of value $C_{\mathrm{cb}}\left(G_{\mathrm{V}}+\right.$ 1) from input to ground. This effective increase of $C_{\mathrm{cb}}$ is known as the Miller effect. It often dominates the rolloff characteristics of amplifiers, because a typical feedback capacitance of 4 pF can look like several hundred picofarads to ground.

There are several methods available for beating the Miller effect: (a) you can decrease the source impedance driving a grounded-emitter stage by using an emitter follower. Figure 2.84 shows three other possibilities; (b) the differential amplifier circuit with no collector resistor in $Q_{1}$ (Figure 2.84A) has no Miller effect; you can think of it as an emitter follower driving a grounded-base amplifier (see below); (c) the famous cascode configuration (Figure 2.84B) elegantly defeats the Miller effect. Here $Q_{1}$ is a grounded-emitter amplifier with $R_{\mathrm{L}}$ as its collector resistor: $Q_{2}$ is interposed in the collector path to prevent $Q_{1}$ 's collector from swinging (thereby eliminating the Miller effect) while passing the collector current through to the load resistor unchanged. The input labeled $V_{+}$is a fixed-bias voltage, usually set a few volts above $Q_{1}$ 's emitter voltage to pin $Q_{1}$ 's collector and keep it in the active region. This circuit fragment is incomplete, because biasing is not shown; you could either include a bypassed emitter resistor and base divider for biasing $Q_{1}$ (as we did earlier in the chapter) or include it within an overall loop with feedback at dc. $V_{+}$might be provided from a divider or zener, with bypassing to keep it stiff at signal frequencies. (d) Finally, the grounded-base amplifier can be used by itself, as shown in Figure 2.84C. It has no Miller effect because the base is driven by zero source impedance (ground), and the amplifier is noninverting from input to output.

Exercise 2.19. Explain in detail why there is no Miller effect in either transistor in the preceding differential amplifier and cascode circuits.

Capacitive effects can be somewhat more complicated than this brief introduction might indicate. In particular: (a) the rolloffs that are due to feedback and output capacitances are not entirely independent; in the terminology of the trade there is pole splitting; (b) the transistor's input capacitance still has an effect, even with a stiff input signal source. In particular, current that flows through $C_{\text {be }}$ is not amplified by the transistor. This base current "robbing" by the input capacitance causes the transistor's small-signal current gain $h_{\mathrm{fe}}$ to drop at high frequencies, eventually reaching unity at a frequency known as $f_{\mathrm{T}}$. (c) To complicate matters, the junction capacitances depend on voltage: a dominant portion of $C_{\mathrm{be}}$ changes proportionally with
image_name:A
description:
[
name: Q1, type: NPN, ports: {C: p, B: b1, E: p}
name: Q2, type: NPN, ports: {C: Vout, B: p, E: GND}
]
extrainfo:The circuit diagram A is a differential amplifier with an inverting input grounded to avoid the Miller effect. It uses two NPN transistors, Q1 and Q2. The base of Q1 is connected to the input node b1, and its collector and emitter are connected to node p. The collector of Q2 is connected to the output node Vout, and its emitter is grounded. The diagram also includes resistors Rs, RE, and RL, as well as a voltage source Vs connected to node X1.
image_name:B
description:
[
name: Q1, type: NPN, ports: {C: GND, B: Vin2, E: CE2}
name: Q2, type: NPN, ports: {C: Vout, B: Vin1, E: CE2}
name: RL, type: Resistor, value: RL, ports: {N1: VCC, N2: Vout}
name: Vs, type: VoltageSource, value: Vs, ports: {Np: V+, Nn: GND}
name: RE, type: Resistor, value: RE, ports: {N1: Vin, N2: e1}
name: Rs, type: Resistor, value: Rs, ports: {N1: Vin2, N2: GND}
name: CE2, type: Capacitor, value: CE2, ports: {Np: CE2, Nn: GND}
]
extrainfo:This is a cascode amplifier configuration (B) to avoid the Miller effect. It uses two NPN transistors Q1 and Q2 with a resistor RL connected to the VCC and Vout. The input is provided at Vin1 and Vin2, with a voltage source Vs providing bias through V+.
image_name:C
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: e1, E: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: +5V}
name: RE, type: Resistor, value: RE, ports: {N1: Vin, N2: e1}
]
extrainfo:The circuit C is a grounded base amplifier configuration. It uses an NPN transistor Q1 with the emitter grounded and the base connected to an input voltage Vin through resistor RE. The collector is connected to the output Vout, which is also connected to a load resistor RL and a +5V supply.

Figure 2.84. Three circuit configurations that avoid the Miller effect. A. Differential amplifier with inverting input grounded. B. Cascode connection. C. Grounded base amplifier.
operating current, so $f_{\mathrm{T}}$ is given instead. ${ }^{60}$ (d) When a transistor is operated as a switch, effects associated with charge stored in the base region of a saturated transistor cause an additional loss of speed.

The Miller effect looms large in high-speed and wideband circuits, and we'll be seeing it again and again in subsequent chapters.

### 2.4.6 Field-effect transistors

In this chapter we have dealt exclusively with BJTs, characterized by the Ebers-Moll equation. BJTs were the original transistors, and they are widely used in analog circuit design. However, it would be a mistake to continue without a few words of explanation about the other kind of transistor, the FET, which we will take up in detail in Chapter 3.

The FET behaves in many ways like an ordinary bipolar transistor. It is a three-terminal amplifying device, available in both polarities, with a terminal (the gate) that controls the current flow between the other two terminals (source and drain). It has a unique property, though: the gate draws no dc current, except for leakage. This means that extremely high input impedances are possible, limited only by capacitance and leakage effects. With FETs you don't have to worry about providing substantial base current, as was necessary with the BJT circuit design of this chapter. Input currents measured in picoamperes are commonplace. Yet the FET is a rugged and capable device, with voltage and current ratings comparable to those of bipolar transistors.

Most of the available devices fabricated with BJTs

[^15](matched pairs, differential and operational amplifiers, comparators, high-current switches and amplifiers, and RF amplifiers) are also available with FET construction, often with superior performance. Furthermore, digital logic, microprocessors, memory, and all manner of complex and wonderful large-scale digital chips are built almost exclusively with FETs. Finally, the area of micropower design is dominated by FET circuits. It is not exaggeration to say that, demographically, almost all transistors are FETs. ${ }^{61}$

FETs are so important in electronic design that we devote the next chapter to them before treating operational amplifiers and feedback in Chapter 4. We urge the reader to be patient with us as we lay the groundwork in these first three difficult chapters; that patience will be rewarded many times over in the succeeding chapters, as we explore the enjoyable topics of circuit design with operational amplifiers and digital integrated circuits.

## 2.5 Negative feedback

We've hinted earlier in the chapter that feedback offers a cure to some vexing problems: biasing the groundedemitter amplifier (\$2.3.4 and 2.3.5), biasing the differential amplifier with current-mirror active load (§2.3.8C), and minimizing crossover distortion in push-pull followers (§2.4.1A). It's even better than that - negative feedback

[^16]is a wonderful technique that can cure all manner of ills: distortion and nonlinearities, frequency dependence of amplifier gain, departure from ideal performance of voltage sources, current sources, or pretty much anything else.

We'll be enjoying the benefits of negative feedback fully in Chapter 4, where we introduce the universal analog component called an operational amplifier ("op-amp"), a creature that thrives on negative feedback. But this is a good place to introduce feedback, both because it is widely used in discrete transistor circuits and also because it is present already in our common emitter amplifier, whose improved linearity (compared with that of the grounded-emitter amplifier) is due to negative feedback.

### 2.5.1 Introduction to feedback

Feedback has become such a well-known concept that the word has entered the general vocabulary. In control systems, feedback consists of comparing the actual output of the system with the desired output and making a correction accordingly. The "system" can be almost anything: for instance, the process of driving a car down the road, in which the output (the position and velocity of the car) is sensed by the driver, who compares it with expectations and makes corrections to the input (steering wheel, throttle, brake). In amplifier circuits the output should be a multiple of the input, so in a feedback amplifier the input is compared with an attenuated version of the output.

As used in amplifiers, negative feedback is implemented simply by coupling the output back in such a way as to cancel some of the input. You might think that this would only have the effect of reducing the amplifier's gain and would be a pretty stupid thing to do. Harold S. Black, who attempted to patent negative feedback in 1928, was greeted with the same response. In his words, "Our patent application was treated in the same manner as one for a perpetual-motion machine." ${ }^{62}$ True, it does lower the gain, but in exchange it also improves other characteristics, most notably freedom from distortion and nonlinearity, flatness of response (or conformity to some desired frequency response), and predictability. In fact, as more negative feedback is used, the resultant amplifier characteristics become less dependent on the characteristics of the open-loop (nofeedback) amplifier and finally depend on the properties only of the feedback network itself. Operational amplifiers

[^17](the very high-gain differential amplifier building blocks of Chapter 4) are typically used in this high-loop-gain limit, with open-loop voltage gain (no feedback) of a million or so.

A feedback network can be frequency dependent, to produce an equalization amplifier (with specific gain-versus-frequency characteristics), or it can be amplitude dependent, producing a nonlinear amplifier (an example is a logarithmic amplifier, built with feedback that exploits the logarithmic $V_{\mathrm{BE}}$ versus $I_{\mathrm{C}}$ of a diode or transistor). It can be arranged to produce a current source (near-infinite output impedance) or a voltage source (near-zero output impedance), and it can be connected to generate very high or very low input impedance. Speaking in general terms, the property that is sampled to produce feedback is the property that is improved. Thus, if you feed back a signal proportional to the output current, you will generate a good current source. ${ }^{63}$

Let's look at how feedback works, and how it affects what an amplifier does. We will find simple expressions for the input impedance, output impedance, and gain of an amplifier with negative feedback.

### 2.5.2 Gain equation

Look at Figure 2.85. To get started we've drawn the familiar common-emitter amplifier with emitter degeneration. Thinking of the transistor in the Ebers-Moll sense, the small-signal voltage from base to emitter ( $\Delta V_{\mathrm{BE}}$ ) programs the collector current. But $\Delta V_{\mathrm{BE}}$ is less than the input voltage $V_{\mathrm{in}}$, because of the drop across $R_{\mathrm{E}}$. If the output is unloaded, it's easy to get the equation in the figure. In other words, the common-emitter amplifier with emitter degeneration is a grounded-emitter amplifier with negative feedback, as we hinted earlier.

This circuit has some subtleties, which we'd like to sidestep for now by looking instead at the more straightforward configuration shown in Figure 2.85B. Here we've drawn a differential amplifier (with differential gain $A$ ), with a fraction of its output signal subtracted from the circuit input $v_{\text {in }}$. That fraction, of course, is given simply by

[^18]image_name:A
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: Vin, E: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Vout}
name: RE, type: Resistor, value: RE, ports: {N1: e, N2: GND}
name: A, type: OpAmp, value: A, ports: {InP: Vin, InN: Vdiff, OutP: Vout, OutN: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: InN(A)}
name: R2, type: Resistor, value: R2, ports: {N1: InN(A), N2: GND}
]
extrainfo:The diagram shows two configurations: A common-emitter amplifier with emitter degeneration (A) and a differential amplifier configured as a noninverting amplifier (B). In configuration A, negative feedback is used to stabilize the gain. In configuration B, the differential gain is defined as A, and negative feedback is applied through a voltage divider formed by R1 and R2.
image_name:B
description:
[
name: A, type: OpAmp, value: A, ports: {InP: Vin, InN: Vdiff, OutP: Vout}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: 1nA(A)}
name: R2, type: Resistor, value: R2, ports: {N1: 1nA(A), N2: GND}
]
extrainfo:This is a differential amplifier configured as a noninverting voltage amplifier with negative feedback. The feedback network is composed of resistors R1 and R2, which determine the fraction of the output voltage fed back to the input. The differential gain is represented as A. The circuit follows the equation Vdiff = Vin - (R2/(R1 + R2)) * Vout.
image_name:C
description:The block diagram labeled 'C' illustrates a conventional feedback system commonly used in amplifiers. It consists of the following main components:

1. **Summing Junction**: This is the point where the input signal \( V_{in} \) is combined with the feedback signal. The summing junction subtracts a fraction of the output signal \( V_{out} \) from the input signal, resulting in a differential input \( V_{diff} \).

2. **Amplifier (Block A)**: This block represents the main amplifier with a gain \( A \). It amplifies the differential input signal \( V_{diff} \) to produce the output signal \( V_{out} \). The amplifier is configured as a non-inverting amplifier, meaning it maintains the phase of the input signal.

3. **Feedback Network (Block B)**: This block takes a portion of the output signal \( V_{out} \), scales it by a factor \( B \), and feeds it back to the summing junction. This creates a negative feedback loop, which stabilizes the gain and bandwidth of the amplifier.

Flow of Information:
- The input signal \( V_{in} \) enters the summing junction.
- The feedback network provides a scaled version of \( V_{out} \) back to the summing junction.
- The summing junction subtracts the feedback signal from the input signal to produce \( V_{diff} \).
- \( V_{diff} \) is then amplified by the amplifier block \( A \) to produce the output \( V_{out} \).
Labels and Annotations:
- \( V_{in} \), \( V_{out} \), and \( V_{diff} \) are labeled to indicate their roles as input, output, and differential signals respectively.
- The gain of the amplifier is indicated as \( A \), and the feedback factor is represented by block \( B \).
Overall System Function:
The primary function of this system is to act as a non-inverting amplifier with negative feedback. The feedback loop helps to control the gain and improve the stability and linearity of the amplifier. By subtracting a portion of the output from the input, the system reduces distortion and increases bandwidth, making it ideal for precise amplification tasks.

C.
$$
V_{\text {diff }}=V_{\text {in }}-B V_{\text {out }}
$$

Figure 2.85. Negative feedback subtracts a fraction of the output from the input: A. Common-emitter amplifier. B. Differential amplifier configured as a noninverting voltage amplifier. C. Conventional block diagram.
the voltage divider equation, as shown. This is a very common configuration, widely used with op-amps (Chapter 4), and known simply as a "noninverting amplifier."

When talking about negative feedback, it's conventional to draw a diagram like Figure 2.85 C , in which the feedback fraction is simply labeled $B$. This is useful because it allows more generality than a voltage divider (feedback can include frequency-dependent components like capacitors, and nonlinear components like diodes), and it keeps the equations simple. For a voltage divider, of course, $B$ would simply be equal to $R_{2} /\left(R_{1}+R_{2}\right)$.

Let's figure out the gain. The amplifier has open-loop voltage gain $A$, and the feedback network subtracts a fraction $B$ of the output voltage from the input. (Later we will generalize things so that inputs and outputs can be currents
or voltages.) The input to the gain block is then $V_{\text {in }}-B V_{\text {out }}$. But the output is just the input times $A$ :

$$
A\left(V_{\text {in }}-B V_{\text {out }}\right)=V_{\text {out }} .
$$

In other words,

$$
V_{\text {out }}=\frac{A}{1+A B} V_{\text {in }}
$$

and so the closed-loop voltage gain, $V_{\text {out }} / V_{\mathrm{in}}$, is just

$$
\begin{equation*}
G=\frac{A}{1+A B} \tag{2.16}
\end{equation*}
$$

Some terminology: the standard designations for these quantities are as follows: $G=$ closed-loop gain, $A=$ openloop gain, $A B=$ loop gain, $1+A B=$ return difference, or desensitivity. The feedback network is sometimes called the beta network (no relation to transistor beta, $h_{\mathrm{fe}}$ ). ${ }^{64}$

### 2.5.3 Effects of feedback on amplifier circuits

Let's look at the important effects of feedback. The most significant are predictability of gain (and reduction of distortion), changed input impedance, and changed output impedance.

#### A. Predictability of gain

The voltage gain is $G=A /(1+A B)$. In the limit of infinite ${ }^{65}$ open-loop gain $A, G=1 / B$. For finite gain $A$, feedback acts to reduce the effects of variations of $A$ (with frequency, temperature, amplitude, etc.). For instance, suppose $A$ depends on frequency as in Figure 2.86. This will surely satisfy anyone's definition of a poor amplifier (the gain varies over a factor of 10 with frequency). Now imagine we introduce feedback, with $B=0.1$ (a simple voltage divider will do). The closed-loop voltage gain now varies from 1000/[1 $+(1000 \times 0.1)]$, or 9.90 , to $10,000 /[1$ $+(10,000 \times 0.1)]$, or 9.99 , a variation of just $1 \%$ over the same range of frequency! To put it in audio terms, the original amplifier is flat to $\pm 10 \mathrm{~dB}$, whereas the feedback amplifier is flat to $\pm 0.04 \mathrm{~dB}$. We can now recover the original gain of 1000 with nearly this linearity simply by cascading three such stages.

It was for just this reason (namely, the need for extremely flat-response telephone repeater amplifiers) that

[^19]image_name:Figure 2.86
description:The graph depicted is a plot of the open-loop gain \( A \) of an amplifier as a function of frequency \( f \). The x-axis represents the frequency \( f \), while the y-axis represents the open-loop gain \( A \), with values ranging from 0 to 10,000. The y-axis is labeled in a linear scale with significant markers at 0, 1000, 5000, and 10,000.

The graph shows a bell-shaped curve indicating that the open-loop gain varies widely with frequency. Initially, as the frequency increases from the left, the gain \( A \) also increases, reaching a peak value slightly above 10,000. This peak represents the maximum gain of the amplifier at a specific frequency. After reaching this peak, the gain decreases as the frequency continues to increase, demonstrating a symmetrical decline.

This behavior suggests that the amplifier has a specific frequency range where it operates with maximum efficiency, and the gain reduces outside this range. The curve does not indicate any resonance peaks or sharp drops, suggesting a smooth variation in gain with frequency. This type of response is typical in amplifiers where the gain is dependent on frequency, and it highlights the need for feedback mechanisms to stabilize the gain across a broader frequency range.

Figure 2.86. Amplifier with open-loop gain $A$ that varies widely with frequency $f$.
negative feedback in electronics was invented. As the inventor, Harold Black, described it in his first open publication on the invention [Elec. Eng., 53, 114, (1934)], "by building an amplifier whose gain is made deliberately, say 40 decibels higher than necessary ( 10,000 -fold excess on energy basis) and then feeding the output back to the input in such a way as to throw away the excess gain, it has been found possible to effect extraordinary improvement in constancy of amplification and freedom from nonlinearity." Black's patent is spectacular, with dozens of elegant figures; we reproduce one of them here (Figure 2.87), which makes the point eloquently.
image_name:FIG.59
description:The graph depicted in FIG.59 is a Bode plot illustrating the gain-frequency characteristic as a function of degenerative feedback. The x-axis represents frequency in cycles per second (Hertz), using a logarithmic scale ranging from \(10^2\) to \(10^5\) Hz. The y-axis represents gain in decibels (dB), ranging from 20 dB to 100 dB.

**Overall Behavior and Trends:**
- The graph shows three distinct curves labeled "No Feedback," "Feedback 1," and "Feedback 2," illustrating how feedback affects gain across different frequencies.
- The "No Feedback" curve starts at approximately 40 dB at low frequencies, peaking around 90 dB near \(10^4\) Hz, and then decreases back to about 60 dB at the high-frequency end.
- "Feedback 1" follows a similar pattern but with reduced gain, starting around 40 dB, peaking slightly above 60 dB, and decreasing to about 40 dB.
- "Feedback 2" shows even more attenuation, maintaining a relatively flat gain of about 30 dB across the frequency spectrum.

**Key Features and Technical Details:**
- The peak gain for the "No Feedback" curve occurs around \(10^4\) Hz, indicating a resonant frequency where the system naturally amplifies the most.
- The "Operating Range" is marked on the "No Feedback" curve, highlighting the range of frequencies where the system operates with optimal gain.
- The application of feedback reduces the peak gain and flattens the response, demonstrating the stabilizing effect of feedback on the system.

**Annotations and Specific Data Points:**
- The graph clearly annotates the different feedback conditions, providing a visual comparison of how each feedback level affects the gain.
- The significant reduction in gain with increasing feedback illustrates the principle of degenerative feedback, which is used to stabilize and linearize amplifier systems.

This graph effectively communicates the impact of feedback on gain, showcasing the trade-off between gain and stability in amplifier design.

Figure 2.87. Harold Black explains it in his historic 1937 patent, with the unassuming title "Wave translation system."

It is easy to show, by taking the partial derivative of $G$ with respect to $A$ (i.e., $\partial G / \partial A$ ), that relative variations in the open-loop gain are reduced by the desensitivity:

$$
\begin{equation*}
\frac{\Delta G}{G}=\frac{1}{1+A B} \frac{\Delta A}{A} . \tag{2.17}
\end{equation*}
$$

Thus, for good performance the loop gain $A B$ should be much larger than 1 . That's equivalent to saying that the open-loop gain should be much larger than the closed-loop gain.

A very important consequence of this is that nonlinearities, which are simply gain variations that depend on signal level, are reduced in exactly the same way.

#### B. Input impedance

Feedback can be arranged to subtract a voltage or a current from the input (these are sometimes called series feedback and shunt feedback, respectively). The noninverting amplifier configuration we've been considering, for instance, subtracts a sample of the output voltage from the differential voltage appearing at the input, whereas the feedback scheme in Figure 2.89B subtracts a current from the input. The effects on input impedance are opposite in the two cases: voltage feedback multiplies the open-loop input impedance by $1+A B$, whereas current feedback reduces it by the same factor. In the limit of infinite loop gain the input impedance (at the amplifier's input terminal) goes to infinity or zero, respectively. This is easy to understand, since voltage feedback tends to subtract signal from the input, resulting in a smaller change (by the factor $A B$ ) across the amplifier's input resistance; it's a form of bootstrapping. Current feedback reduces the input signal by bucking it with an equal current.
image_name:Figure 2.88
description:
[
name: Ri, type: Resistor, value: Ri, ports: {N1: Vip, N2: X1}
name: A, type: OpAmp, value: A, ports: {InP: Vip, InN: X1, Out: Vout}
name: B, type: Buffer, ports: {In: Vout, Out: X1}
]
extrainfo:The circuit is a differential amplifier with series voltage feedback. The input voltage Vin is reduced by the feedback factor BVout, creating a differential voltage Vdiff across the input of the op-amp. The feedback is applied through a buffer B, which isolates the feedback path.

Figure 2.88. Series-feedback Gnput impedance.

#### Series (voltage) feedback

Let's see explicitly how the effective input impedance is changed by feedback. We illustrate the case of voltage feedback only, since the derivations are similar for the two cases. We begin with a differential amplifier model with (finite) input resistance as shown in Figure 2.88. An input $V_{\text {in }}$ is reduced by $B V_{\text {out }}$, putting a voltage $V_{\text {diff }}=V_{\text {in }}-B V_{\text {out }}$ across the inputs of the amplifier. The input current is therefore

$$
I_{\text {in }}=\frac{V_{\text {in }}-B V_{\text {out }}}{R_{i}}=\frac{V_{\text {in }}\left(1-B \frac{A}{1+A B}\right)}{R_{i}}=\frac{V_{\text {in }}}{(1+A B) R_{i}},
$$

giving an effective input impedance

$$
Z_{\text {in }}=V_{\text {in }} / I_{\text {in }}=(1+A B) R_{i} .
$$

In other words, the input impedance is boosted by a factor of the loop gain plus one. If you were to use the circuit of Figure 2.85B to close the feedback loop around a differential amplifier whose native input impedance is $100 \mathrm{k} \Omega$ and whose differential gain is $10^{4}$, choosing the resistor ratio (99:1) for a target gain of 100 (in the limit of infinite amplifier gain), the input impedance seen by the signal source would be approximately $10 \mathrm{M} \Omega$, and the closed-loop gain would be 99.66

#### Shunt (current) feedback

Look at Figure 2.89A. The impedance seen looking into the input of a voltage amplifier with current feedback is reduced by the feedback current, which opposes voltage changes at the input. ${ }^{67}$ By considering the current change produced by a voltage change at the input, you find that the input signal sees a parallel combination of (a) the amplifier's native input impedance $R_{\mathrm{i}}$ and (b) the feedback resistor $R_{\mathrm{f}}$ divided by $1+A$. That is,

$$
Z_{\mathrm{in}}=R_{\mathrm{i}} \| \frac{R_{\mathrm{f}}}{1+A}
$$

(see if you can prove this). In cases of very high loop gain (e.g, an op-amp), the input impedance is reduced to a fraction of an ohm, which might seem bad. But in fact this configuration is used to convert an input current into an output voltage (a "transresistance amplifier"), for which a low input impedance is a good characteristic. We'll see examples in Chapters 4 and $4 x$.

By the addition of an input resistor (Figure 2.89B) the circuit becomes an "inverting amplifier," with input resistance as shown. You can think of this (particularly in the high-loop-gain limit) as a resistor feeding a current-tovoltage amplifier. In that limit $R_{\text {in }}$ approximately equals $R_{1}$ (and the closed-loop gain approximately equals $-R_{2} / R_{1}$ ).

It is a straightforward exercise to derive an expression for the closed-loop voltage gain of the inverting amplifier with finite loop gain. The answer is

$$
G=-A(1-B) /(1+A B)
$$

where $B$ is defined as before, $B=R_{1} /\left(R_{1}+R_{2}\right)$. In the limit of large open-loop gain $A, G=1-1 / B$ (i.e., $\left.G=-R_{2} / R_{1}\right)$.

[^20]image_name:A
description:
[
name: Rf, type: Resistor, value: Rf, ports: {N1: input, N2: output}
name: Ri, type: Resistor, value: Ri, ports: {N1: input, N2: GND}
name: Ro, type: Resistor, value: Ro, ports: {N1: output, N2: GND}
name: Av, type: OpAmp, value: Av, ports: {InP: GND, InN: input, OutP: output, OutN: GND}
]
extrainfo:The circuit diagram A represents a transresistance amplifier with the input impedance Z_in = Ri || Rf/(1+A) and the output impedance Z_out = Ro/(1+A). The circuit uses feedback to control these impedances.
image_name:B
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: input, N2: v}
name: Ri, type: Resistor, value: Ri, ports: {N1: v, N2: GND}
name: Av, type: OpAmp, value: Av, ports: {InP: GND, InN: v, OutP: Vout, OutN: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vout, N2: v}
name: Ro, type: Resistor, value: Ro, ports: {N1: Vout, N2: output}
]
extrainfo:The circuit diagram B represents an inverting amplifier with resistors R1 and R2 setting the gain, and Ro representing the output impedance. The input impedance is given by Zin = R1 + Ri || (R2 / (1 + A)) and the output impedance is given by Zout = Ro / (1 + AB), where B = R1 / (R1 + R2).

Figure 2.89. Input and output impedances for (A) transresistance amplifier and ( B ) inverting amplifier.

Exercise 2.20. Derive the foregoing expressions for input impedance and gain of the inverting amplifier.
image_name:Figure 2.90
description:
[
name: Ri, type: Resistor, value: Ri, ports: {N1: Vin, N2: InN}
name: AVd, type: OpAmp, value: AVd, ports: {InP: GND, InN: InN, Out: V}
name: Ro, type: Resistor, value: Ro, ports: {N1: V, N2: Out}
name: B, type: Other, ports: {N1: Out, N2: Vin}
]
extrainfo:The circuit is an inverting amplifier with feedback. The input impedance is determined by Ri and the feedback factor B. The output impedance is reduced by the feedback factor (1+AB).

Figure 2.90. Output impedance.

#### C. Output impedance

Again, feedback can extract a sample of the output voltage or the output current. In the first case the open-loop output impedance will be reduced by the factor $1+A B$, whereas in the second case it will be increased by the same factor. We illustrate this effect for the case of voltage sampling.

We begin with the model shown in Figure 2.90. This time we have shown the output impedance explicitly. The calculation is simplified by a trick: short the input and apply a voltage $V$ to the output; by calculating the output current $I$, we get the output impedance $R_{\mathrm{o}}^{\prime}=V / I$. Voltage $V$ at the output puts a voltage $-B V$ across the amplifier's input, producing a voltage $-A B V$ in the amplifier's internal generator. The output current is therefore

$$
I=\frac{V-(-A B V)}{R_{\mathrm{o}}}=\frac{V(1+A B)}{R_{\mathrm{o}}}
$$

giving an effective output impedance ${ }^{68}$ of

$$
Z_{\text {out }}=V / I=R_{\mathrm{o}} /(1+A B) .
$$

#### D. Sensing output current

Feedback can be connected instead to sample the output current. Then the expression for output impedance becomes

$$
Z_{\text {out }}=R_{\mathrm{o}}(1+A B)
$$

In fact, it is possible to have multiple feedback paths, sampling both voltage and current. In the general case the output impedance is given by Blackman's impedance relation ${ }^{69}$

$$
Z_{\mathrm{out}}=R_{\mathrm{o}} \frac{1+(A B)_{\mathrm{SC}}}{1+(A B)_{\mathrm{OC}}}
$$

where $(A B)_{\mathrm{SC}}$ is the loop gain with the output shorted to ground and $(A B)_{\mathrm{OC}}$ is the loop gain with no load attached. Thus feedback can be used to generate a desired output impedance. This equation reduces to the previous results for the usual situation in which feedback is derived from either the output voltage or the output current. See additional discussion in Chapter $2 x$.

### 2.5.4 Two important details

Feedback is a rich subject, which we've simplified shamelessly in this brief introduction. Here are two details that should not be overlooked, however, even at this somewhat superficial level of understanding.

[^21]
#### A. Loading by the feedback network

In feedback computations, you usually assume that the beta network doesn't load the amplifier's output. If it does, that must be taken into account in computing the open-loop gain. Likewise, if the connection of the beta network at the amplifier's input affects the open-loop gain (feedback removed, but network still connected), you must use the modified open-loop gain. Finally, the preceding expressions assume that the beta network is unidirectional, i.e., it does not couple any signal from the input to the output.

#### B. Phase shifts, stability, and "compensation"

The open-loop amplifier gain $A$ is central in the expressions we've found for closed-loop gain and the corresponding input and output impedances. By default one might reasonably assume that $A$ is a real number - that is, that the output is in phase with the input. In real life things are more complex, ${ }^{70}$ because of the effects of circuit capacitances (and Miller effect, §2.4.5), and also the limited bandwidth ( $f_{\mathrm{T}}$ ) of the active components themselves. The result is that the open-loop amplifier will exhibit lagging phase shifts that increase with frequency. This has several consequences for the closed-loop amplifier.

#### Stability

If the open-loop amplifier's lagging phase shift reaches $180^{\circ}$, then negative feedback becomes positive feedback, with the possibility of oscillation. This is not what you want! (The actual criterion for oscillation is that the phase shift be $180^{\circ}$ at a frequency at which the loop gain $A B$ equals 1.) This is a serious concern, particularly in amplifiers with plenty of gain (such as op-amps). The problem is only exacerbated if the feedback network contributes additional lagging phase shift (as it often will). The subject of frequency compensation in feedback amplifiers deals directly with this essential issue; you can read about it in §4.9.

#### Gain and phase shift

The expressions we found for closed-loop gain and for the input and output impedances contain the open-loop gain A. For example, the voltage amplifier with series feedback (Figures 2.85B\&C, 2.88, and 2.90) has closed-loop gain $G_{\text {CL }}=A /(1+A B)$, where $A=G_{\text {OL }}$, the amplifier's openloop gain. Let's imagine that the open-loop gain $A$ is 100, and that we've chosen $B=0.1$ for a target closed-loop gain of $G_{\mathrm{CL}} \approx 10$. Now, if the open-loop amplifier had no phase shifts, then $G_{\text {CL }} \approx 9.09$, also without phase shift. If instead the amplifier has a $90^{\circ}$ lagging phase shift, then $A$ is pure

[^22]image_name:Figure 2.91
description:
[
name: Q1, type: NPN, ports: {C: Cb3, B: Vin, E: P1}
name: Q2, type: NPN, ports: {C: VCC, B: P1, E: b2}
name: Q3, type: PNP, ports: {C: X1, B: Cb3, E: VCC}
name: Q4, type: NPN, ports: {C: VCC, B: X1, E: X}
name: Q5, type: PNP, ports: {C: X, B: X3, E: VEE}
name: R1, type: Resistor, value: 100k, ports: {N1: Vin, N2: GND}
name: R2, type: Resistor, value: 620Ω, ports: {N1: Cb3, N2: VCC}
name: R3, type: Resistor, value: 6.8k, ports: {N1: P1, N2: GND}
name: R4, type: Resistor, value: 100k, ports: {N1: b2, N2: X3}
name: R5, type: Resistor, value: 3.3k, ports: {N1: X3, N2: X}
name: R6, type: Resistor, value: 1.5k, ports: {N1: X3, N2: VEE}
name: R7, type: Resistor, value: 5Ω, ports: {N1: X, N2: Vout}
name: R8, type: Resistor, value: 5Ω, ports: {N1: Vout, N2: X}
name: C1, type: Capacitor, value: 2.2μF, ports: {Np: Vin, Nn: b1}
name: C2, type: Capacitor, value: 47μF, ports: {Np: GND, Nn: X3}
name: Cb3, type: Capacitor, value: Cb3, ports: {Np: Cb3, Nn: Cb3}
name: D1, type: Diode, ports: {Na: X1, Nc: X2}
name: D2, type: Diode, ports: {Na: X2, Nc: X3}
name: D3, type: Diode, ports: {Na: X3, Nc: X}
]
extrainfo:The circuit is a transistor power amplifier with negative feedback, utilizing a combination of NPN and PNP transistors, resistors, capacitors, and diodes. It is powered by a dual supply (+15V and -15V). The amplifier is designed to manage phase shifts and maintain closed-loop gain stability.

Figure 2.91. Transistor power amplifier with negative feedback.
imaginary $(A=-100 j)$, and the closed-loop gain becomes $G_{\mathrm{CL}}=9.90-0.99 j$. That's a magnitude $\left|G_{\mathrm{CL}}\right|=9.95$, with a lagging phase shift of approximately $6^{\circ}$. In other words, the effect of a pretty significant (halfway to oscillation!) open-loop phase shift turns out, in fact, to be favorable: the closed-loop gain is only $0.5 \%$ less than the target, compared with $9 \%$ for the case of the same amplifier without phase shift. The price you pay is some residual phase shift and, of course, an approach to instability.

As artificial as this example may seem, it in fact reflects a reality of op-amps, which usually have an $\sim 90^{\circ}$ lagging phase shift over almost their entire bandwidth (typically from $\sim 10 \mathrm{~Hz}$ to 1 MHz or more). Because of their much higher open-loop gain, the amplifier with feedback exhibits very little phase shift, and an accurate gain set almost entirely by the feedback network. Much more on this in Chapter 4, and in $\S 4.9$.

Exercise 2.21. Verify that the above expressions for $G_{\text {CL }}$ are correct.

### 2.5.5 Two examples of transistor amplifiers with feedback

Let's look at two transistor amplifier designs to see how the performance is affected by negative feedback. There's a bit of complexity in this analysis . . . don't be discouraged! ${ }^{71}$

[^23]Figure 2.91 shows a complete transistor amplifier with negative feedback. Let's see how it goes.

#### A. Circuit description

It may look complicated, but it is extremely straightforward in design and is relatively easy to analyze. $Q_{1}$ and $Q_{2}$ form a differential pair, with common-emitter amplifier $Q_{3}$ amplifying its output. $R_{6}$ is $Q_{3}$ 's collector load resistor, and push-pull pair $Q_{4}$ and $Q_{5}$ form the output emitter follower. The output voltage is sampled by the feedback network consisting of voltage divider $R_{4}$ and $R_{5}$, with $C_{2}$ included to reduce the gain to unity at dc for stable biasing. $R_{3}$ sets the quiescent current in the differential pair, and since overall feedback guarantees that the quiescent output voltage is at ground, $Q_{3}$ 's quiescent current is easily seen to be 10 mA ( $V_{\mathrm{EE}}$ across $R_{6}$, approximately). As we discussed earlier (§2.4.1B), the diodes bias the push-pull pair into conduction, leaving one diode drop across the series pair $R_{7}$ and $R_{8}$, i.e., 60 mA quiescent current. That's classAB operation, good for minimizing crossover distortion, at the cost of 1 watt standby dissipation in each output transistor.

From the point of view of our earlier circuits, the only unusual feature is $Q_{1}$ 's quiescent collector voltage, one diode drop below $V_{\mathrm{CC}}$. That is where it must sit in order to hold $Q_{3}$ in conduction, and the feedback path ensures that it will. (For instance, if $Q_{1}$ were to pull its collector closer to ground, $Q_{3}$ would conduct heavily, raising the output
voltage, which in turn would force $Q_{2}$ to conduct more heavily, reducing $Q_{1}$ 's collector current and hence restoring the status quo.) $R_{2}$ was chosen to give a diode drop at $Q_{1}$ 's quiescent current in order to keep the collector currents in the differential pair approximately equal at the quiescent point. In this transistor circuit the input bias current is not negligible $(4 \mu \mathrm{~A})$, resulting in a 0.4 V drop across the 100 k input resistors. In transistor amplifier circuits like this, in which the input currents are considerably larger than in op-amps, it is particularly important to make sure that the dc resistances seen from the inputs are equal, as shown (a Darlington input stage would probably be better here).

#### B. Analysis

Let's analyze this circuit in detail, determining the gain, input and output impedances, and distortion. To illustrate the utility of feedback, we will find these parameters for both the open-loop and closed-loop situations (recognizing that biasing would be hopeless in the open-loop case). To get a feeling for the linearizing effect of the feedback, the gain will be calculated at +10 volts and -10 volts output, as well as at the quiescent point $(0 \mathrm{~V})$.

#### Open loop

Input impedance We cut the feedback at point $X$ and ground the right-hand side of $R_{4}$. The input signal sees 100k in parallel with the impedance looking into the base. The latter is $h_{\mathrm{fe}}$ times twice the intrinsic emitter resistance plus the impedance seen at $Q_{2}$ 's emitter caused by the finite impedance of the feedback network at $Q_{2}$ 's base. For $h_{\mathrm{fe}} \approx 250, Z_{\mathrm{in}} \approx 250 \times[(2 \times 25)+(3.3 \mathrm{k} / 250)]$; i.e., $Z_{\text {in }} \approx 16 \mathrm{k}$.

Output impedance Since the impedance looking back into $Q_{3}$ 's collector is high, the output transistors are driven by a 1.5 k source $\left(R_{6}\right)$. The output impedance is about $15 \Omega$ ( $\beta \approx 100$ ) plus the $5 \Omega$ emitter resistance, or $20 \Omega$. The intrinsic emitter resistance of $0.4 \Omega$ is negligible.

Gain The differential input stage sees a load of $R_{2}$ paralleled by $Q_{3}$ 's base resistance. Since $Q_{3}$ is running 10 mA quiescent current, its intrinsic emitter resistance is $2.5 \Omega$, giving a base impedance of about $250 \Omega$ (again, $\beta \approx 100$ ). The differential pair thus has a gain of

$$
\frac{250 \| 620}{2 \times 25 \Omega} \text { or } 3.5
$$

The second stage, $Q_{3}$, has a voltage gain of $1.5 \mathrm{k} \Omega / 2.5 \Omega$, or 600. The overall voltage gain at the quiescent point is $3.5 \times 600$, or 2100 . Since $Q_{3}$ 's gain depends on its collector current, there is substantial change of gain with signal
swing, i.e., nonlinearity. The gain is tabulated in the following section for three values of output voltage.

Closed loop
Input impedance This circuit uses series feedback, so the input impedance is raised by $(1+$ loop gain $)$. The feedback network is a voltage divider with $B=1 / 30$ at signal frequencies, so the loop gain $A B$ is 70 . The input impedance is therefore $70 \times 16 \mathrm{k}$, still paralleled by the 100 k bias resistor, i.e., about 92 k . The bias resistor now dominates the input impedance.

Output impedance Since the output voltage is sampled, the output impedance is reduced by $(1+$ loop gain $)$. The output impedance is therefore $0.3 \Omega$. Note that this is a small-signal impedance and does not mean that a $1 \Omega$ load could be driven to nearly full swing, for instance. The $5 \Omega$ emitter resistors in the output stage limit the large signal swing. For instance, a $4 \Omega$ load could be driven only to 10 Vpp , approximately.

Gain The gain is $A /(1+A B)$. At the quiescent point that equals 30.84, using the exact value for $B$. To illustrate the gain stability achieved with negative feedback, the overall voltage gain of the circuit with and without feedback is tabulated at three values of output level at the end of this paragraph. It should be obvious that negative feedback has brought about considerable improvement in the amplifier's characteristics, although in fairness it should be pointed out that the amplifier could have been designed for better open-loop performance, e.g., by using a current source for $Q_{3}$ 's collector load and degenerating its emitter, by using a current source for the differential-pair emitter circuit, etc. Even so, feedback would still make a large improvement.

|  | Open loop |  |  |  | Closed loop |  |  |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| $V_{\text {out }}$ | -10 | 0 | +10 | -10 | 0 | +10 |  |
| $\mathbf{Z}_{\text {in }}$ | 16 k | 16 k | 16 k | 92 k | 92 k | 92 k |  |
| $\mathbf{Z}_{\text {out }}$ | $20 \Omega$ | $20 \Omega$ | $20 \Omega$ | $0.3 \Omega$ | $0.3 \Omega$ | $0.3 \Omega$ |  |
| Gain | 1360 | 2100 | 2400 | 30.60 | 30.84 | 30.90 |  |

#### C. Series-feedback pair

Figure 2.92 shows another transistor amplifier with feedback. Thinking of $Q_{1}$ as an amplifier of its base-emitter voltage drop (thinking in the Ebers-Moll sense), the feedback samples the output voltage and subtracts a fraction of it from the input signal. This circuit is a bit tricky because $Q_{2}$ 's collector resistor doubles as the feedback network. Applying the techniques we used earlier, one can show that $G($ open loop $) \approx 200$, loop gain $\approx 20, Z_{\text {out }}($ open
image_name:Figure 2.92
description:
[
name: R1, type: Resistor, value: 68k, ports: {N1: Vcc, N2: Vin}
name: R2, type: Resistor, value: 10k, ports: {N1: Vin, N2: GND}
name: R3, type: Resistor, value: 620, ports: {N1: Cb, N2: Vcc}
name: R4, type: Resistor, value: 1.0k, ports: {N1: e1, N2: GND}
name: R5, type: Resistor, value: 10k, ports: {N1: Vout, N2: e1}
name: Q1, type: NPN, ports: {C: Cb, B: Vin, E: e1}
name: Q2, type: PNP, ports: {C: Vout, B: Cb, E: Vcc}
name: Vcc, type: VoltageSource, value: +20V, ports: {Np: Vcc, Nn: GND}
]
extrainfo:The circuit is a series-feedback amplifier using two transistors, Q1 (NPN) and Q2 (PNP). The feedback is implemented through the resistor R5, providing a fraction of the output voltage back to the input. The circuit is biased to operate with a gain of approximately 9.5 in closed loop.

loop $) \approx 10 \mathrm{k}, Z_{\text {out }}($ closed loop $) \approx 500 \Omega$, and $G($ closed loop) $\approx 9.5$.

Exercise 2.22. Go for it!

## 2.6 Some typical transistor circuits

To illustrate some of the ideas of this chapter, let's look at a few examples of circuits with transistors. The range of circuits we can cover at this point is necessarily limited, because real-world circuits usually incorporate op-amps (the subject of Chapter 4) and other useful ICs - but we'll see plenty of transistors used alongside ICs in those later chapters.

### 2.6.1 Regulated power supply

Figure 2.93 shows a very common configuration. $R_{1}$ normally holds $Q_{1}$ on; when the output reaches 10 volts, $Q_{2}$ goes into conduction (base at 5 V ), preventing further rise of output voltage by shunting base current from $Q_{1}$ 's base. The supply can be made adjustable by replacing $R_{2}$ and $R_{3}$ with a potentiometer. In this voltage regulator (or "regulated dc supply") circuit, negative feedback acts to stabilize the output voltage: $Q_{2}$ "looks at" the output and does something about it if the output isn't at the right voltage.

A few details: (a) Adding a biasing resistor $R_{4}$ ensures a relatively constant zener current, so that the zener voltage does not change significantly with load current. It is tempting to provide that bias current from the input, but it is far better to use the regulated output. A warning is in order: whenever you use an output voltage to make something happen within a circuit, make sure that the circuit will start up correctly; here, however, there is no problem (why not?). (b) The capacitor $C_{1}$ would probably be needed in
this circuit to ensure stability (i.e., to prevent oscillation), particularly if the output were capacitively bypassed (as it should be), for reasons we will see later in connection with feedback loop stability (§4.9).

We'll see much more of this subject in Chapter 9.
image_name:Figure 2.93. Feedback voltage regulator
description:
[
name: Q1, type: NPN, ports: {C: b1c2, B: b1c2, E: Vout}
name: Q2, type: NPN, ports: {C: b1c2, B: b2, E: GND}
name: D1, type: Diode, ports: {Na: e1k1, Nc: GND}
name: R1, type: Resistor, value: 1.0k, ports: {N1: VDD, N2: b1c2}
name: R2, type: Resistor, value: 1.0k, ports: {N1: Vout, N2: b2}
name: R3, type: Resistor, value: 1.0k, ports: {N1: b2, N2: GND}
name: R4, type: Resistor, value: 5k, ports: {N1: b2, N2: e1k1}
name: C1, type: Capacitor, value: 100pF, ports: {Np: b1c2, Nn: b2}
]
extrainfo:The circuit is a feedback voltage regulator with a TIP31 and 2N3904 transistors. The diode D1 is a 4.3V Zener diode for voltage regulation. Capacitor C1 is used to ensure stability by preventing oscillation. The circuit operates from an unregulated input voltage of +12V to +25V and regulates the output to +10V with a current range of 0 to 100mA.

Figure 2.93. Feedback voltage regulator.

### 2.6.2 Temperature controller

The schematic diagram in Figure 2.94 shows a temperature controller based on a thermistor sensing element, a device that changes resistance with temperature. Differential Darlington $Q_{1}-Q_{4}$ compares the voltage of the adjustable reference divider $R_{4}-R_{6}$ with the divider formed from the thermistor and $R_{2}$. (By comparing ratios from the same supply, the comparison becomes insensitive to supply variations; this particular configuration is called a Wheatstone bridge.) Current mirror $Q_{5} Q_{6}$ provides an active load to raise the gain, and mirror $Q_{7} Q_{8}$ provides emitter current. $Q_{9}$ compares the differential amplifier output with a fixed voltage, saturating Darlington $Q_{10} Q_{11}$ (which supplies power to the heater) if the thermistor is too cold. $R_{9}$ is a current-sensing resistor that turns on protection transistor $Q_{12}$ if the output current exceeds about 6 amps ; that steals base drive from $Q_{10} Q_{11}$, preventing damage. And $R_{12}$ adds a small amount of positive feedback, to cause the heater to snap on and off abruptly; this is the same trick (a "Schmitt trigger") as in Figure 2.13.

### 2.6.3 Simple logic with transistors and diodes

Figure 2.95 shows a circuit that performs a task we illustrated in $\S 1.9 .1 \mathrm{~F}$ : sounding a buzzer if either car door is open and the driver is seated. In this circuit the transistors all operate as switches (either OFF or saturated). Diodes $D_{1}$ and $D_{2}$ form what is called an OR gate, turning off $Q_{1}$ if either door is open (switch closed). However, the collector of
image_name:Figure 2.94
description:
[
name: Q1, type: NPN, ports: {C: X2, B: b1k3, E: GND}
name: Q2, type: NPN, ports: {C: b2, B: X2, E: GND}
name: Q3, type: NPN, ports: {C: buzzer, B: X2, E: GND}
name: R1, type: Resistor, value: 1k, ports: {N1: VCC, N2: X1}
name: R2, type: Resistor, value: 1k, ports: {N1: X2, N2: VCC}
name: R3, type: Resistor, value: 1k, ports: {N1: b2, N2: VCC}
name: R4, type: Resistor, value: 10k, ports: {N1: b1k3, N2: GND}
name: D1, type: Diode, ports: {Na: S1, Nc: X1}
name: D2, type: Diode, ports: {Na: S2, Nc: X1}
name: D3, type: Diode, ports: {Na: X1, Nc: b1k3}
name: D4, type: Diode, ports: {Na: buzzer, Nc: GND}
name: C3, type: Capacitor, ports: {Np: VCC, Nn: buzzer}
]
extrainfo:This circuit is a seat-belt buzzer system that uses transistors and diodes to form logic gates. It activates the buzzer if either car door is open and the driver is seated. Diodes D1 and D2 form an OR gate, while D3 ensures Q1 is off when either door is closed. Q3 is used to drive the buzzer when Q1 is off and the seat switch S3 is closed. Diode D4 protects against inductive transients from the buzzer.
image_name:Figure 2.95
description:
[
name: Q1, type: NPN, ports: {C: X2, B: b1k3, E: GND}
name: Q2, type: NPN, ports: {C: b2, B: X2, E: GND}
name: Q3, type: NPN, ports: {C: buzzer, B: b2, E: GND}
name: R1, type: Resistor, value: 1.0k, ports: {N1: VCC, N2: X1}
name: R2, type: Resistor, value: 1.0k, ports: {N1: X2, N2: b2}
name: R3, type: Resistor, value: 1.0k, ports: {N1: buzzer, N2: b2}
name: R4, type: Resistor, value: 10k, ports: {N1: b1k3, N2: GND}
name: D1, type: Diode, ports: {Na: X1, Nc: GND}
name: D2, type: Diode, ports: {Na: X1, Nc: GND}
name: D3, type: Diode, ports: {Na: X1, Nc: b1k3}
name: D4, type: Diode, ports: {Na: buzzer, Nc: GND}
name: S1, type: Switch, ports: {N1: left door, N2: GND}
name: S2, type: Switch, ports: {N1: right door, N2: GND}
name: S3, type: Switch, ports: {N1: seat, N2: GND}
name: C3, type: Capacitor, value: C3, ports: {Np: buzzer, Nn: GND}
]
extrainfo:This circuit is a seat-belt buzzer circuit using transistors and diodes to form logic gates. It sounds a buzzer if either car door is open and the driver is seated. Diodes D1 and D2 form an OR gate, turning off Q1 if either door is open. Q3 turns on the buzzer when the driver is seated.

Figure 2.95. Both diodes and transistors are used to make digital logic "gates" in this seat-belt buzzer circuit.
$Q_{1}$ stays near ground, preventing the buzzer from sounding unless switch $S_{3}$ is also closed (driver seated); in that case $R_{2}$ turns on $Q_{3}$, putting 12 volts across the buzzer. $D_{3}$ provides a diode drop so that $Q_{1}$ is OFF with $S_{1}$ or $S_{2}$ closed, and $D_{4}$ protects $Q_{3}$ from the buzzer's inductive turn-off transient. In Chapters $10-15$ we discuss logic circuitry in detail.

#### Additional Exercises for Chapter 2

Exercise 2.23. Design a transistor switch circuit that allows you to switch two loads to ground by means of saturated npn transistors. Closing switch $A$ should cause both loads to be powered, whereas closing switch $B$ should power only one load. Hint: use diodes.

Exercise 2.24. Consider the current source in Figure 2.96. (a) What is $I_{\text {load }}$ ? What is the output compliance? Assume $V_{\mathrm{BE}}$ is 0.6 V . (b) If $\beta$ varies from 50 to 100 for collector voltages within the output compliance range, how much will the output current vary? (There are two effects here.) (c) If $V_{\mathrm{BE}}$ varies according to $\Delta V_{\mathrm{BE}}=-0.0001 \Delta V_{\mathrm{CE}}$ (Early effect), how much will the load current vary over the compliance range? (d) What is the temperature coefficient of output current assuming that $\beta$ does not vary with temperature? What is the temperature coefficient of output current assuming that $\beta$ increases from its nominal value of 100 by $0.4 \% /{ }^{\circ} \mathrm{C}$ ?
image_name:Figure 2.96. Current source exercise.
description:
[
name: 8.2k, type: Resistor, value: 8.2k, ports: {N1: VCC, N2: b1}
name: 1.6k, type: Resistor, value: 1.6k, ports: {N1: b1, N2: GND}
name: 1.5k, type: Resistor, value: 1.5k, ports: {N1: e1, N2: GND}
name: Load, type: Other, ports: {N1: c1, N2: VCC}
name: Q1, type: NPN, ports: {C: c1, B: b1, E: e1}
]
extrainfo:The circuit is a current source with an NPN transistor. The load is connected between the collector and VCC. Resistors 8.2k and 1.6k form a voltage divider for biasing the base of the transistor. The 1.5k resistor is connected to the emitter and ground.

Figure 2.96. Current source exercise.

Exercise 2.25. Design a common-emitter npn amplifier with a voltage gain of $15, V_{\mathrm{CC}}$ of +15 V , and $I_{\mathrm{C}}$ of 0.5 mA . Bias the collector at $0.5 V_{\mathrm{CC}}$, and put the low-frequency 3 dB point at 100 Hz .
Exercise 2.26. Bootstrap the circuit in the preceding problem to raise the input impedance. Choose the rolloff of the bootstrap appropriately.

Exercise 2.27. Design a dc-coupled differential amplifier with a voltage gain of 50 (to a single-ended output) for input signals near ground, supply voltages of $\pm 15$ volts, and quiescent currents of 0.1 mA in each transistor. Use a current source in the emitter and an emitter follower output stage.

Exercise 2.28. In this problem you will ultimately design an amplifier whose gain is controlled by an externally applied voltage (in Chapter 3 you will see how to do the same thing with FETs). (a) Begin by designing a long-tailed pair differential amplifier with emitter current source and no emitter resistors (undegenerated). Use $\pm 15 \mathrm{~V}$ supplies. Set $I_{\mathrm{C}}$ (each transistor) at $100 \mu \mathrm{~A}$, and use $R_{\mathrm{C}}=10 \mathrm{k}$. Calculate the voltage gain from a single-ended input (other input grounded) to a single-ended output. (b) Now modify the circuit so that an externally applied voltage controls the emitter current source. Give an approximate formula for the gain as a function of controlling voltage. (In a real circuit you might arrange a second set of voltage-controlled current sources
to cancel the quiescent-point shift that gain changes produce in this circuit, or a differential-input second stage could be added to your circuit.)
image_name:Figure 2.97. Bad biasing.
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: b1, E: GND}
name: R, type: Resistor, value: 100Ω, ports: {N1: b1, N2: GND}
name: C, type: Capacitor, value: C, ports: {Np: Vin, Nn: b1}
name: Vcc, type: VoltageSource, value: +20V, ports: {Np: Vcc, Nn: GND}
name: 1k, type: Resistor, value: 1k, ports: {N1: Vcc, N2: b1}
name: 10k, type: Resistor, value: 10k, ports: {N1: Vout, N2: Vcc}
]
extrainfo:The circuit is a simple amplifier with bad biasing. It uses an NPN transistor (Q1) with a collector connected to the output (Vout), a base connected through a capacitor (C) to the input (Vin), and an emitter connected to ground. The circuit is powered by a +20V supply (Vcc). A 1k resistor connects Vcc to the base, and a 10k resistor connects Vout to Vcc. A 100Ω resistor is used for biasing at the base.

Figure 2.97. Bad biasing.
image_name:Figure 2.98
description:
[
name: Q1, type: NPN, ports: {C: Vin1, B: Vin1, E: VE}
name: Q2, type: NPN, ports: {C: +VCC, B: Vin1, E: Vin1}
name: Q3, type: NPN, ports: {C: X1, B: Vin1, E: Vin1}
name: Q4, type: PNP, ports: {C: Vin1, B: Vin1, E: VE+2V}
name: Q5, type: NPN, ports: {C: Vin2, B: VE, E: Vin2}
name: R1, type: Resistor, value: R1, ports: {N1: +VCC, N2: Vin1}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin1, Nn: to further stages}
]
extrainfo:The circuit is a precision operational amplifier with a base-current cancellation scheme. It includes multiple NPN and PNP transistors for biasing and amplification, with connections to both positive and negative voltage supplies.

Figure 2.98. Base-current cancellation scheme used in precision operational amplifiers. Bias-current cancellation is discussed in detail in Chapter $4 x$.

Exercise 2.29. Disregarding the lessons of this chapter, a disgruntled student builds the amplifier shown in Figure 2.97. He adjusts $R$ until the quiescent point is $0.5 V_{\mathrm{CC}}$. (a) What is $Z_{\text {in }}$ (at high frequencies where $Z_{\mathrm{C}} \approx 0$ )? (b) What is the small-signal voltage gain? (c) What rise in ambient temperature (roughly) will cause the transistor to saturate?

Exercise 2.30. Several commercially available precision op-amps (e.g., the venerable OP-07) use the circuit in Figure 2.98 to cancel input bias current (only half of the symmetrical-input differential amplifier is shown in detail; the other half works the same way). Explain how the circuit works. Note: $Q_{1}$ and $Q_{2}$ are a betamatched pair. Hint: it's all done with mirrors.

#### Review of Chapter 2

An A-to-W review of Chapter 2. This review doesn't follow the exact topic order in the chapter: here we first cover transistor theory, then circle back to discuss some applications. In the chapter circuits have been interspersed with theory to provide motivation and illustrate how to use the theory.

#### IA. Pin-Labeling Conventions.

The introduction (§2.1) describes some transistor and circuit-labeling conventions. For example, $V_{\mathrm{B}}$ (with a single subscript) indicates the voltage at the base terminal, and similarly $I_{\mathrm{B}}$ indicates current flowing into the base terminal. $V_{\mathrm{BE}}$ (two subscripts) indicates base-to-emitter voltage. Symbols like $V_{\mathrm{CC}}$ and $V_{\mathrm{EE}}$ (repeated subscripts) indicate the positive and negative supply voltages.

#### IB. Transistor Types and Polarities.

Transistors are three-terminal devices capable of amplifying signals. They come in two broad classes, bipolar junction transistors (BJTs, the subject of this chapter), and field-effect transistors (FETs, the subject of Chapter 3). BJTs have a control terminal called the base, and a pair of output terminals, called the collector and the emitter (the corresponding terminals in a FET are gate, drain, and source). A signal applied to the base controls the current flowing from collector to emitter. There are two BJT polarities available, $n p n$ and $p n p$; for $n p n$ devices the collector is more positive than the emitter, and the opposite is true for pnp. Figure 2.2 illustrates this and identifies intrinsic diodes that are part of the transistor structure, see IID and IIF below. The figure also illustrates that the collector current and the (much smaller) base current combine to form the emitter current.

Operating modes Transistors can operate as switches turned ON or OFF - or they can be used as linear devices, for example as amplifiers, with an output current proportional to an input signal. Put another way, a transistor can be in one of three states: cutoff (non-zero $V_{\mathrm{CE}}$ but zero $I_{\mathrm{C}}$ ), saturated (non-zero $I_{\mathrm{C}}$ but near-zero $V_{\mathrm{CE}}$ ), or in the linear region (non-zero $V_{\mathrm{CE}}$ and $I_{\mathrm{C}}$ ). If you prefer prose (and using "voltage" as shorthand for collector-to-emitter voltage $V_{\mathrm{CE}}$, and "current" as shorthand for collector current $I_{\mathrm{C}}$ ), the cutoff state has voltage but no current, the saturated state has current but near-zero voltage, and the linear region has both voltage and current.

#### IC. Transistor Man and Current Gain.

In the simplest analysis, §2.1.1, the transistor is simply a current amplifier, with a current gain called beta (symbol $\beta$, or sometimes $h_{\mathrm{FE}}$ ). A current into the base causes
a current $\beta$ times larger to flow from collector to emitter, $I_{\mathrm{C}}=\beta I_{\mathrm{B}}$, if the external circuit allows it. When currents are flowing, the base-emitter diode is conducting, so the base is $\sim 0.65 \mathrm{~V}$ more positive (for $n p n$ ) than the emitter. The transistor doesn't create the collector current out of thin air; it simply throttles current from an available supply voltage. This important point is emphasized by our "transistor man" creation (Figure 2.7), a little homunculus whose job is to continuously examine the base current and attempt to adjust the collector's current to be a factor of $\beta$ (or $h_{\mathrm{FE}}$ ) times larger. For a typical BJT the beta might be around 150, but beta is only loosely specified, and a particular transistor type may have a $3: 1$ spread (or more) in specified beta at some collector current (and further 3:1 spreads of $\beta$ versus $I_{\mathrm{C}}$ and $\beta$ versus temperature, see for example Figure 2.76).

#### ID. Switches and Saturation.

When operated as a switch, §2.2.1, a current must be injected into the base to keep the transistor "ON." This current must be substantially more than $I_{\mathrm{B}}=I_{\mathrm{C}} / \beta$. In practice a value of $1 / 10$ th of the maximum expected collector current is common, but you could use less, depending on the manufacturer's recommendations. Under this condition the transistor is in saturation, with $25-200 \mathrm{mV}$ across the terminals. At such low collector-to-emitter voltages the base-to-collector diode in Figure 2.2 is conducting, and it robs some of the base-current drive. This creates an equilibrium at the saturation voltage. We'll return in $9[\mathrm{~K}$ to look at some circuit examples. See also the discussion of transistor saturation in Chapter $2 x$.

#### ๆE. The BJT is a Transconductance Device.

As we point out in §2.1.1, "A circuit that depends on a particular value for beta is a bad circuit." That's because $\beta$ can vary by factors of 2 to 3 from the manufacturer's nominal datasheet value. A more reliable design approach is to use other highly-predictable BJT parameters that take into account that it is a transconductance device. In keeping with the definition of transconductance (an output current proportional to an input voltage), a BJT's collector current, $I_{\mathrm{C}}$, is controlled by its base-to-emitter voltage, $V_{\mathrm{BE}}$, see $\S 2.3$. (We can then rely on $I_{\mathrm{B}}=I_{\mathrm{C}} / \beta$ to estimate the base current, the other way around from the simple approach in $\mathbb{I C}$.) The transconductance view of BJTs is helpful in many circumstances (estimating gain, distortion, tempco), and it is essential in understanding and designing circuits such as differential amplifiers and current mirrors. However, in many situations you can circumvent the beta-uncertainty problem with circuit design tricks such as dc feedback or emitter degeneration, without explicitly invoking Ebers-Moll
(IIF). Note also that, just as it would be a bad idea to bias a BJT by applying a base current calculated from $I_{\mathrm{C}} / \beta$ (from an assumed $\beta$ ), it would be even worse to attempt to bias a BJT by applying a calculated $V_{\mathrm{BE}}$ (from an assumed $I_{\mathrm{s}}$, see $\mathbb{I}$ F); more on this in $\mathbb{I} \mathrm{Q}$, below. We might paraphrase this by saying "a circuit that depends on a particular value for $I_{\mathrm{s}}$, or for operation at a precise ambient temperature, is a bad circuit."

#### IF. Ebers-Moll.

Figure 2.41 shows a typical Gummel plot, with $V_{\mathrm{BE}}$ dictating $I_{\mathrm{C}}$, and thus an approximate $I_{\mathrm{B}}$. Equations (2.8) and (2.9) show the exponential (or logarithmic) nature of this relationship. A simple form of the equation, $I_{\mathrm{C}}=I_{\mathrm{s}} \exp \left(V_{\mathrm{BE}} / V_{\mathrm{T}}\right)$ and its inverse, $V_{\mathrm{BE}}=V_{\mathrm{T}} \log _{e}\left(I_{\mathrm{C}} / I_{\mathrm{s}}\right)$, where the constant $V_{\mathrm{T}}=25 \mathrm{mV}$ at $25^{\circ} \mathrm{C}$, reveals that collector current is determined by $V_{\mathrm{BE}}$ and a parameter $I_{\mathrm{s}}$, the latter related to the transistor die size and its current density. $I_{\mathrm{S}}$ is a very small current, typically some $10^{11}$ times smaller than $I_{C}$. The Ebers-Moll formula accurately holds for the entire range of silicon BJT types, for example those listed in Table 8.1. The integrated-circuit (IC) industry relies on Ebers-Moll for the design of their highly-successful BJT linear circuits.

#### IG. Collector Current versus Base Voltage: Rules of Thumb.

See §2.3.2. It's useful to remember a few rules of thumb, which we can derive from Ebers-Moll: $I_{\mathrm{C}}$ increases by a factor of ten for $\mathrm{a} \approx 60 \mathrm{mV}$ increase in $V_{\mathrm{BE}}$; it doubles for an $\approx 18 \mathrm{mV} V_{\mathrm{BE}}$ increase, and it increases $4 \%$ for a 1 mV $V_{\mathrm{BE}}$ increase.

IH. Small Signals, Transconductance and $r_{\mathrm{e}}$.
See §2.3.2B. It's convenient to assume operation at fixed $I_{\mathrm{C}}$, and look for the effect of small changes ("small signals"). First, thinking about the rules of thumb above, we can calculate (eq'n 2.13,) the transconductance, $g_{m}=\partial I_{\mathrm{C}} / \partial V_{\mathrm{BE}}=I_{\mathrm{C}} / V_{\mathrm{T}}$. This evaluates to $g_{m}=40 \mathrm{mS}$ at 1 mA , with $g_{m}$ proportional to current. To put it another way, we can assign an effective internal resistance $r_{\mathrm{e}}$ in series with the emitter, $r_{\mathrm{e}}=1 / g_{m}=V_{\mathrm{T}} / I_{\mathrm{C}}$, see eq'n 2.12. (The small $r$ indicates small signal.) A useful fact to memorize: $r_{\mathrm{e}}$ is about $25 \Omega$ at a collector current of 1 mA , and it scales inversely with current.

#### III. Dependence on Temperature.

See §2.3.2C. In $\llbracket \mathrm{F}$ we said $V_{\mathrm{T}}=25 \mathrm{mV}$ at $25^{\circ} \mathrm{C}$, which suggests it's not exactly a constant, but changes with temperature. Because $V_{\mathrm{T}}=k T / q$ (\$2.3.1), you might guess that $V_{\mathrm{BE}}$ is proportional to absolute temperature, thus a temper-
ature coefficient of about $+2 \mathrm{mV} /{ }^{\circ} \mathrm{C}$ (because $V_{\mathrm{BE}} \approx 600 \mathrm{mV}$ at $T=300 \mathrm{~K}$ ). But the scaling parameter $I_{\mathrm{s}}$ has a large opposite tempco, producing an overall tempco of about $-2.1 \mathrm{mV} /{ }^{\circ} \mathrm{C}$. Memorize this fact also! Because $V_{\mathrm{T}}$ is proportional to absolute temperature, the tempco of transconductance at fixed collector current is inversely proportional to absolute temperature (recall $g_{m}=I_{\mathrm{C}} / V_{\mathrm{T}}$ ), and thus drops by about $0.34 \% /^{\circ} \mathrm{C}$ at $25^{\circ} \mathrm{C}$.

#### IJ. Early Effect.

See §2.3.2D. In our simple understanding so far, base voltages (or currents) "program" a BJT's collector current, independent of collector voltage. But in reality $I_{C}$ increases slightly with increasing $V_{\text {CE }}$. This is called the Early effect, see eq'n 2.14 and Figure 2.59, which can be characterized by an Early voltage $V_{\mathrm{A}}$, a parameter independent of operating current; see eq'n 2.15. If the Early voltage is low (a common drawback of $p n p$ transistors) the effect can be quite large. For example, a pnp 2N5087 with $V_{\mathrm{A}}=55 \mathrm{~V}$ has $\eta=4 \times 10^{-4}$, and would experience a 4 mV shift of $V_{\mathrm{BE}}$ with a 10 V change of $V_{\mathrm{CE}}$; if instead the base voltage were held constant, a 10 V increase of collector voltage would cause a $17 \%$ increase of collector current. We hasten to point out there are circuit configurations, such as degeneration, or the cascode, that alleviate the Early effect. For more detail see the discussion in Chapter $2 x$.

#### Circuit Examples

With this summary of basic BJT theory, we now circle back and review some circuit examples from Chapter 2. One way to review the circuits is to flip through the chapter looking at the pictures (and reading the captions), and refer to the associated text wherever you are uncertain of the underlying principles.

#### ףK. Transistor Switches.

BJT switches are discussed in §2.2.1, and circuit examples appear in Figures 2.9 (driving an LED), 2.10 (highside switching, including level shifting), and 2.16 (with an emitter-follower driver). Simply put, you arrange to drive a current into the base to put the transistor into solid saturation for the anticipated collector load current (i.e., $I_{\mathrm{B}} \gg$ $\left.I_{\mathrm{C}} / \beta\right)$, bringing its collector within tens of millivolts of the emitter. More like this appears in Chapter 12 (Logic Interfacing). Looking forward, the use of MOSFET switches often provide a superior switching solution (§§3.4.4 and 3.5); their control terminal (the gate) conveniently requires no static gate current, though you may have to provide significant transient currents to charge its gate capacitance during rapid switching.

#### IL. Transistor Pulsers.

Basic timer and pulse generator circuits are shown in Figures 2.11 (pulse from a step) and 2.12 (pulse from a pulse). These are simple, but not terribly accurate or stable; better to use a dedicated timer or pulse generator IC, see §7.2.

#### 11M. Schmitt Trigger.

A Schmitt trigger is a threshold level-detecting circuit (Figure 2.13) with hysteresis to prevent multiple transitions when noisy input signals go though the threshold(s). Although you can make a Schmitt trigger circuit with discrete transistors, good design practice favors the use of dedicated comparator ICs, see $\S \S 4.3 .2$ and 12.3.

#### IN. Emitter Follower.

The emitter follower is a linear amplifier with an ideal voltage gain of unity, see $\S 2.2 .3$. The beta of the transistor increases the follower's input impedance and reduces its output impedance, see $\S 2.2 .3 \mathrm{~B}$ and eq'n 2.2. There's more detail in §2.3.3 and Figure 2.43, where the effect of the intrinsic emitter resistance $r_{\mathrm{e}}$ is taken into account. In simplified form $R_{\text {out }}=r_{\mathrm{e}}+R_{\mathrm{S}} / \beta$, where $R_{\mathrm{S}}$ is the signal source resistance seen at the base. The dc output voltage is offset from the dc input by $V_{\mathrm{BE}}$, about 0.6 V to 0.7 V , unless a cancelling circuit is used, see §2.2.3D and Figure 2.29. Emitter followers are also used as voltage regulators, see $\S 2.2 .4$ and Figures 2.21 and 2.22. A precision alternative is the op-amp follower, see $\S 4.2 .3$ in Chapter 4.

#### IO. Current Source (or Current Sink).

In contrast to the familiar voltage source (which delivers a constant voltage regardless of load current, think of a battery), a current source delivers a constant current regardless of the load's voltage drop, see §2.2.6 and Figure 2.31; there's no everyday "battery equivalent." Transconductance devices like BJTs, with their relatively constant collector output currents, are natural candidates for making current sources. For the simplest current source, the base is biased with a voltage, say $V_{\mathrm{b}}$, with respect to a reference point (often ground), and the emitter is connected through a resistor to the same reference. For an $n p n$ transistor with ground reference the output (sinking) current will be $I_{\mathrm{C}}=\left(V_{\mathrm{b}}-V_{\mathrm{BE}}\right) / R_{\mathrm{E}}$, see Figure 2.32 . For better stability and predictability the $V_{\mathrm{BE}}$ term can be cancelled, see Figure 2.33. The operating voltage range of a current source is called its compliance range, set on the low end by collector saturation, and on the high end by the transistor's breakdown voltage or by power-dissipation issues. Current sources are frequently created using current-mirror circuits, see TIP below. Precise and stable current sources can
be made with op-amps (§4.2.5); there are also dedicated current-source integrated circuits (§9.3.14).

#### IP. Current Mirrors.

A current mirror (§2.3.7) is a three-terminal current-source circuit that generates an output current proportional to an input "programming" current. In a typical configuration (Figures 2.55 and 2.58) the mirror attaches to a dc rail (or to ground), reflecting the programming current, the latter perhaps set by a resistor. The circuit often omits any emitter resistors, thus achieving compliance to within a fraction of a volt of the rail. Ordinarily you wouldn't attempt to apply exactly the right $V_{\mathrm{BE}}$ to generate a prescribed $I_{\mathrm{C}}$ (à la Ebers-Moll); but that's exactly what you're doing here. The trick is that one transistor $\left(Q_{1}\right)$ of the matched pair inverts Ebers-Moll, creating from the programming current $I_{\mathrm{P}}$ exactly the right $V_{\mathrm{BE}}$ to re-create the same current in the output transistor $Q_{2}$. Cute!

These circuits assume matched transistors, such as you would find inside an IC (recall from $\mathbb{I} \mathrm{G}$ that even a 1 mV difference of $V_{\mathrm{BE}}$ produces a $4 \%$ change of current). Figure 2.62 graphs base-emitter voltage difference versus collector current ratio, $\Delta V_{\mathrm{BE}}=V_{\mathrm{T}} \log _{e}\left(I_{\mathrm{C} 2} / I_{\mathrm{C} 1}\right)$. You can exploit this effect to generate a "ratio mirror," as discussed in Chapter 2x.

As nice as it looks, the basic current mirror of Figure 2.55 suffers from Early-effect change of output current when the output voltage changes. The effect is particularly serious with pnp transistors: in the example of a 2N5087 in $\mathbb{I J} \mathrm{J}$ above, the 4 mV change of $V_{\mathrm{BE}}$ (for a 10 V output change) would cause a $17 \%$ current error. One solution (Figure 2.60) is to add emitter degeneration resistors, at the expense both of compliance near the reference rail and of dynamic range. A more elegant solution is the Wilson mirror (Figure 2.61), which defeats Early effect by exploiting the ever-useful cascode configuration (Figure 2.84B). Cascode transistor $Q_{3}$ passes output transistor $Q_{2}$ 's collector current to the load, while $Q_{2}$ operates with a fixed $V_{\mathrm{CE}}$ of one diode drop (its own $V_{\mathrm{BE}}$ ). The Wilson mirror's ingenious configuration also cancels base-current errors (an ordinary mirror with BJTs having $\beta=100$ has a current error of $2 \%$ ). Degeneration resistors can be added, as shown in circuit B, for additional suppression of Early effect, but they would be omitted in a "pure Wilson mirror." Linear ICs are full of Wilson mirrors. See Chapter $2 x$ for a discussion of bipolarity current mirrors.

#### ПQ. Common-Emitter Amplifiers.

See $\S$ §.2.7 and 2.3.4, and Figures 2.35, 2.48 and 2.50. The simplest form of BJT amplifier has a grounded emitter, a load resistor $R_{\mathrm{L}}$ from the collector to a supply $V_{+}$, and
a dc bias plus a small signal voltage applied to the base. The gain is $G_{\mathrm{V}}=-R_{\mathrm{L}} / r_{\mathrm{e}}$. If the base bias is carefully set so that the collector current pulls the collector halfway to ground, then $I_{\mathrm{C}}=V_{\mathrm{S}} / 2 R_{\mathrm{L}}, r_{\mathrm{e}}=V_{\mathrm{T}} / I_{\mathrm{C}}=2 R_{\mathrm{L}} V_{\mathrm{T}} / V_{\mathrm{S}}$, and so the voltage gain (recall $V_{\mathrm{T}} \approx 25 \mathrm{mV}$ ) is $G_{\mathrm{V}}=-20 V_{\mathrm{s}}$, where $V_{\mathrm{s}}$ is in units of volts. For $V_{\mathrm{s}}=20 \mathrm{~V}$, for example, the voltage gain is -400 .

That's a lot of gain! Unless the signals are small, however, there's a serious problem: the gain is inverse in $r_{\mathrm{e}}$, thus proportional to $I_{\mathrm{C}}$. But the latter changes as the output voltage swings up and down, producing first-order changes in gain, with resulting severe distortion (Figure 2.46). This can be alleviated (at the expense of gain) by adding emitter degeneration in the form of an emitter resistor $R_{\mathrm{E}}$. The gain is then $G_{\mathrm{V}}=-R_{\mathrm{L}} /\left(R_{\mathrm{E}}+r_{\mathrm{e}}\right)$, with greatly reduced effect of varying $r_{\mathrm{e}}$; see Figure 2.47, where emitter degeneration was added to reduce the gain by a factor of ten ( $\left.R_{\mathrm{E}}=9 r_{\mathrm{e}}\right)$. This is also a form of negative feedback, see $\S 2.3 .4 \mathrm{~B}$ and IIW below. You can think of this circuit as a classic current source ( $\Psi \mathrm{O}$ ) driving a resistor as load; the voltage gain is the current source's transconductance multiplied by the load resistance, $G_{\mathrm{V}}=g_{m} R_{\mathrm{L}}$, where $g_{m}=-1 / r_{\mathrm{e}}$.

We've sidestepped the important issue of setting the base bias voltage to produce the desired quiescent collector current. But we don't know the appropriate voltage $V_{\mathrm{BE}}$, and a small change has a big effect, see $\Psi_{[ }$above (e.g., a 60 mV uncertainty in $V_{\mathrm{BE}}$, which is about what you might encounter from different batches of a given transistor, produces a $10 \times$ error in $I_{C}!$ ). There are many circuit solutions, see §2.3.5, but the simplest involves adding emitter degeneration at dc, bypassed as necessary to produce higher gain at signal frequencies (Figure 2.50 and 2.51). Another approach is to use a matching transistor to set the bias, analogous to the current mirror (Figure 2.52); this method is inherent in the widely-used differential amplifier (Figure 2.65). A third approach is to exploit feedback to set the bias (Figures 2.53 and 2.54 ), a method that figures centrally in op-amp circuits (Chapter 4).

#### IR. Differential Amplifiers.

The differential amplifier (\$2.3.8) is a symmetrical configuration of two matched transistors, used to amplify the difference of two input signals. It may include emitter degeneration (Figure 2.64), but need not (Figure 2.65). For best performance the emitter pulldown resistor is replaced by a current source, and (for highest gain) the resistive collector load is replaced by a current mirror (Figure 2.67). Differential amplifiers should reject strongly any common-mode input signal, achieving a good common-mode rejection ratio (CMRR, the ratio $G_{\mathrm{diff}} / G_{\mathrm{CM}}$ ). Differential amplifiers can be used to amplify single-ended input signals (ground
the other input), where the inherent cancellation of $V_{\mathrm{BE}}$ offsets allows accurate dc performance (\$2.3.8B). Ordinarily you use only one output from a differential amplifier; that is, it is used to to convert a balanced input to a single-ended output. But you can use both outputs (a "fully-differential amplifier," §5.17) to drive a balanced load, or to create a pair of signals $180^{\circ}$ out of phase (a phase splitter). See also the sections on the emitter-input differential amplifier and on BJT amplifier distortion in Chapter 2x, and §5.13-§5.16 (precision differential and instrumentation amplifiers).

#### IS. Comparators.

A differential amplifier with lots of gain $G_{\text {diff }}$ is driven into differential saturation with a small differential input (§2.3.8E). For example, just a few millivolts of input difference is adequate to saturate the output if $G_{\text {diff }}=1000$ (easily accomplished with a current-mirror collector load). When operated in this way, the differential amplifier is a voltage comparator, a circuit used widely to sense thresholds or compare signal levels; it's the basis of analog-todigital conversion, and figures importantly in Chapter 12 (see $\S 12.3$ and Tables 12.1 and 12.2).

#### IT. Push-Pull Amplifiers.

A single transistor conducts in one direction only (e.g., an npn transistor can only sink current from its collector, and source current from its emitter). That makes it awkward to drive a heavy load with alternating polarity (e.g., a loudspeaker, servomotor, etc.), although it can be done, wastefully, with a single-ended stage ("class-A") with high quiescent current, see Figure 2.68. The push-pull configuration uses a pair of transistors connected to opposite supply rails (§2.4.1), an arrangement that can supply large output currents of either polarity with little or no quiescent current. Figure 2.69 shows a push-pull follower with complementary polarities, and with zero quiescent current ("class-B"); this produces some crossover distortion, which can be eliminated by biasing the pair into quiescent conduction ("class-AB," Figure 2.71),. The output transistors can be beta-boosting configurations like the Darlington or Sziklai (IIU), see for example Figure 2.78. The pushpull configuration is widely used in logic circuits (see Figure 10.25), gate driver ICs (see Figure 3.97), and in combination with op-amps to deliver greater output currents (see Figure 4.26).

#### qU. The Darlington and Sziklai Connections.

These simple combinations of two transistors create a 3terminal equivalent transistor with $\beta=\beta_{1} \beta_{2}$. The Darlington (Figures 2.74 and 2.75) cascades two transistors of the
same polarity and has a base-emitter drop of $2 V_{\mathrm{BE}}$; the Sziklai (Figure 2.77) pairs opposite polarities, and has a single base-emitter drop (which is only weakly dependent on output current, thanks to $R_{\mathrm{B}}$ ). For either configuration a resistor $R_{\mathrm{B}}$ should be connected across the output transistor's base-emitter terminals. For more about this subject see see the discussion in Chapter $2 x$.

#### IV. Miller Effect.

Like all electronic components, transistors have interterminal capacitances, designated (by terminal pairs) $C_{\mathrm{be}}$, $C_{\mathrm{ce}}$, and $C_{\mathrm{c}} .^{72}$ While $C_{\mathrm{be}}$ and $C_{\mathrm{ce}}$ slow the input and output waveforms by creating lowpass filters with the source and load resistances, the effect of the feedback capacitance $C_{\mathrm{cb}}$ is more insidious: it creates an additional input capacitance to ground equal to $C_{\mathrm{cb}}$ multiplied by the stage's inverting voltage gain, thus its effective input capacitance becomes $C_{\mathrm{eff}}=\left(G_{\mathrm{V}}+1\right) C_{\mathrm{cb}}$. This is the infamous Miller effect (\$2.4.5B), whose impact can be devastating in high-speed and wideband amplifiers. Some circuit solutions include

[^24]the grounded-base amplifier, the differential amplifier, and the cascode configuration (see the discussion of cascode in Chapter 2x).

#### IW. Negative Feedback.

If there were a Nobel prize for grand-concepts-in-circuitdesign, it would surely go to Harold Black for his elegant elucidation of negative feedback. In its simplest form, it consists of subtracting, from the input signal, a fraction $B$ of an amplifier's output signal $V_{\text {out }}$ (Figure 2.85). If the amplifier's open-loop gain is $A$, then the closed-loop gain becomes (eq'n 2.16) $G_{\mathrm{cl}}=A /(1+A B)$. The quantity $A B$, which generally is large compared with unity, is called the loop gain, and it (more precisely the quantity $1+A B$ ) is the multiplier by which negative feedback improves the amplifier's performance: improved linearity and constancy of gain, and (in this series feedback circuit configuration) raised input impedance and lowered output impedance; see §2.5.3.

Feedback is the essence of linear design, and it is woven deeply into the DNA of op-amp circuits (the subject of Chapter 4), and power circuits (Chapter 9). With negative feedback you can make amplifiers with $0.0001 \%$ distortion, voltage sources with $0.001 \Omega$ output impedance, and many other wonders too magnificent here to relate. Stay tuned. Better yet, read on!
