# Chapter4 Building Blocks for Analog Integrated Circuits

Chapter Outline
4.1 Design Considerations in Monolithic Circuits ..... 334
4.2 BJT Characteristics and Models Revisited ..... 342
4.3 MOSFET Characteristics and Models Revisited ..... 357
4.4 Darlington, Cascode, and Cascade Configurations ..... 371
4.5 Differential Pairs ..... 386
4.6 Common-Mode Rejection Ratio in Differential Pairs ..... 396
4.7 Input Offset Voltage/Current in Differential Pairs ..... 404
4.8 Current Mirrors ..... 409
4.9 Differential Pairs with Active Loads ..... 421
4.10 Bipolar Output Stages ..... 432
4.11 CMOS Output Stages ..... 440
Appendix 4A: Editing SPICE Netlists ..... 445
References ..... 446
Problems ..... 446

As mentioned in Chapter 2, following its invention in 1947, the bipolar junction transistor (BJT) was first put to use as a replacement for the much bulkier, power hungry and far less reliable vacuum tube. In fact, the first transistor circuits were virtual replicas of vacuum-tube circuit prototypes, if with suitable scaling of the power supplies and surrounding components. Broadly speaking, they belong to the class of circuits that we have investigated so far and that are generally referred to as discrete circuits.

Toward the end of the 1950s it was realized that the dramatic miniaturization and reduction in power consumption brought about by the transistor could be exploited further by fabricating entire circuits (transistors, diodes, resistors, and small capacitors, along with their interconnections) in monolithic form, that is, on the same piece of semiconductor material, or chip. Also called an integrated circuit (IC), it was first implemented in 1958 by Jack Kilby at Texas Instruments, and, independently, in 1959
by Robert Noyce at Fairchild Semiconductor. The 1960s saw a feverish activity that resulted in the development of the first monolithic operational amplifier by Fairchild Semiconductor (mA Series) along with the digital IC families known as transistortransistor logic (TTL) by Texas Instruments (7400 Series) and emitter-coupled logic (ECL) by Motorola (10K Series).

Meanwhile, in the early 1960s the field-effect transistor of the metal-oxidesemiconductor type (MOSFET) became a commercial reality. Compared to the BJT, the MOSFET offered the advantages of smaller size and lower power consumption. This alternative technology led to the development of the first battery-powered electronic calculators and wristwatches, as well as a low-power alternative to the prevailing TTL bipolar logic family, namely, the CMOS digital family of the 4000 Series, by RCA. These products were followed by the first microprocessor, by Intel, in 1971. Since then, IC electronics has progressed exponentially and has penetrated virtually every aspect of modern life. This impressive growth has been governed by Moore's law, roughly stating that thanks to continued advances in IC fabrication, the number of devices that can be integrated on a given chip area doubles every approximately 18 months. Originally formulated in 1965, this law still holds to this day, though it has been pointed out that technology is bound to approach physical limits that will eventually lead to the demise of this law.

The BJT, after having been the dominant semiconductor device for nearly three decades, has been overtaken by the MOSFET, especially in high-density ICs, owing to the MOSFET's aforementioned advantages of smaller size and lower power consumption. Nonetheless, the BJT continues to be the device of choice in highperformance general-purpose analog ICs. It is also preferred in specialized discrete designs, thanks to the availability of a wide selection of devices. It is also possible to fabricate BJTs and MOSFETs simultaneously on the same chip, if at an increase in the number of fabrication steps and cost. The resulting technology, aptly known as BiCMOS technology, exploits the advantages of both transistor types to provide even more innovative design solutions. Contemporary ICs tend to combine digital as well as analog functions on the same chip, this being the reason for the name mixed-signal or also mixed-mode ICs. As a rule, one would try to implement as many functions as possible in digital form, and use analog circuitry only when interfacing to the external physical world, which is analog by nature.

CHAPTER HIGHLIGHTS

The chapter begins with a comparison between discreet and monolithic design. This is followed by a review of BJT and FET characteristics emphasizing second-order effects that were deliberately omitted in the earlier introductory chapters, but that are relevant to monolithic circuit realizations. Also reviewed are the basic single-transistor configurations of Chapters 2 and 3, but from a monolithic perspective, where the functions of dc biasing and output loading are no longer provided by resistors, but by other transistors operating as current sources or sinks.

Next, the chapter investigates a variety of multiple-transistor circuit configurations that have become standard building blocks for analog ICs. These include the Darlington and cascode configurations, differential pairs, current mirrors, dc current
sources and sinks, active-loaded gain stages, and push-pull output stages. Particular attention is devoted to the differential pair because it forms the core of most analog ICs. First, we investigate the pair for the idealized case of perfectly matched components, then we examine the effect of fabrication mismatches upon input offset errors and the common-mode rejection ratio. Whenever possible, BJT and FET realizations are covered in parallel both to void duplications and to compare the two technologies in their similarities and differences.

This chapter exposes the student to a variety of clever design solutions that contribute to making analog electronics a most fascinating discipline. But the best is yet to come, in the next chapter, when these building blocks will be combined together in the design of some representative analog ICs.

It is reassuring to know that no matter how sophisticated a given circuit, the tools we use to comprehend it are still those mastered in a basic electric circuits course, namely, Ohm's law, Kirchhoff's laws (KVL and KCL), Thévenin's/Norton's reductions, and the test-signal technique to find terminal resistances in the presence of dependent sources.

The chapter makes abundant use of PSpice both as a software oscilloscope to display transfer curves and waveforms, and as a verification tool for dc and ac hand calculations.

## 4.1 DESIGN CONSIDERATIONS IN MONOLITHIC CIRCUITS

The widespread usage of monolithic circuits, also called integrated circuits (ICs), stems from our ability to fabricate large numbers of interconnected devices on the same semiconductor chip while keeping power consumption suitably low. Compared to their discrete predecessors, ICs present unique constraints as well as advantages for the designer. The most relevant ones are as follows:

- Capacitors are highly undesirable in IC technology as they tend to take up inordinate amounts of chip area. While small capacitors (on the order of a few picofarads or less) are still acceptable, large-valued ones such as those used for ac coupling and ac bypassing in the discrete CE and CS amplifier examples of Chapters 2 and 3 must definitely be ruled out. Consequently, inter-stage coupling must be of the dc type, and suitable techniques must be devised to avoid ac bypass capacitors. All considered, these constraints turn out to be a blessing because once they are met, a monolithic circuit will function all the way down to dc. By contrast, the discrete designs of Chapters 2 and 3 will function properly only above a certain frequency, as at low frequencies capacitors will start acting as open circuits, no longer providing the intended functions of coupling and bypass.
- Resistors too tend to take up precious chip area, though not as severely as capacitors, so they too must be avoided whenever possible. When implemented with the same materials that are utilized to form the regions of a transistor, monolithic resistances also suffer from gross tolerances and can be quite sensitive to temperature. On the other hand, transistors are the most natural devices in IC technology, both in terms of size and ease of fabrication, so in monolithic implementations, resistive functions such as dc biasing must be rephrased in terms of transistors.
- Devices fabricated simultaneously on the same chip tend to exhibit highly matched characteristics. True, these characteristics are sensitive to temperature and also drift with time, but if two or more devices are fabricated in close proximity to each other so that they share the same environment, their characteristics will track over a range of environmental variations. Matching and tracking are exploited on purpose in IC design to implement clever functions that would be far more difficult to achieve in discrete form. Two popular examples are current mirrors and differential pairs, to be investigated in great detail as we proceed.

### An Illustrative Example

To illustrate similarities as well as differences between discrete and monolithic design, let us reconsider the familiar CE configuration of Fig. 4.1, which in the days of discrete designs preceding ICs was the workhorse of voltage amplification. As long as each capacitor acts as an ac short compared to the equivalent resistance presented by the surrounding circuitry, the small-signal gain takes on the form

$$
\begin{equation*}
a=\frac{v_{o}}{v_{i}}=-g_{m}\left(r_{o} / / R_{C}\right) \tag{4.1a}
\end{equation*}
$$

To convert this design to a form suited to monolithic fabrication we need to get rid of the capacitors and replace the resistors with suitably biased transistors whenever possible. Following are the relevant steps:

- The function of $C_{1}$ in Fig. 4.1 is to resolve the dc difference between the input source (typically with a dc component of 0 V ) and the base (typically biased at $1 / 3 V_{C C}$ ) while providing an ac short between source and base ( $\left.v_{b} \rightarrow v_{i}\right)$. The best way to get rid of $C_{1}$ is to couple the input source to the base directly, as in Fig. 4.2a. Dc coupling also eliminates the need for the biasing resistors $R_{1}$ and $R_{2}$.
- The function of $R_{E}$ in Fig. 4.1 is to establish the bias current $I_{E}$, whereas that of $C_{2}$ is to ensure an ac ground at the emitter $\left(v_{e} \rightarrow 0\right)$. Both functions can be met, at least in principle, by biasing the emitter negatively via a suitable voltage source $V_{B E 1}=V_{T} \ln \left(I_{C 1} / I_{s 1}\right)$, as also shown in Fig. 4.2a.
image_name:FIGURE 4.1
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: VCC, N2: X1}
name: R2, type: Resistor, value: R2, ports: {N1: X1, N2: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Vo}
name: RE, type: Resistor, value: RE, ports: {N1: X2, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: VI, Nn: X1}
name: C2, type: Capacitor, value: C2, ports: {Np: X2, Nn: GND}
name: Q1, type: NPN, ports: {C: Vo, B: X1, E: X2}
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
]
extrainfo:This is a discrete voltage amplifier circuit with DC coupling. The bias current IE is established by RE, and C2 ensures an AC ground at the emitter. The circuit uses an NPN transistor Q1 for amplification.

FIGURE 4.1 A discrete voltage amplifier.
image_name:FIGURE 4.2(a)
description:
[
name: Q1, type: NPN, ports: {C: VO, B: VI, E: VE1}
name: Q4, type: PNP, ports: {C: VCC, B: X1, E: VO}
name: V_I, type: VoltageSource, value: V_I, ports: {Np: VI, Nn: GND}
name: V_EB4, type: VoltageSource, value: V_EB4, ports: {Np: VCC, Nn: x1}
name: V_BE1, type: VoltageSource, value: V_BE1, ports: {Np: GND, Nn: VE1}
]
extrainfo:This circuit is a discrete voltage amplifier using two transistors, Q1 and Q4. Q1 is an NPN transistor used for amplification, and Q4 is a PNP transistor connected to VCC. The circuit is DC coupled, with VI as the input voltage source and VO as the output. V_EB4 and V_BE1 are additional voltage sources used for biasing.
image_name:v_o vs V_o
description:### Type of Graph and Function
The graph is a time-domain waveform representing the output voltage \( v_o \) of a discrete voltage amplifier circuit.

Axes Labels and Units
- **X-Axis:** Time (not explicitly labeled, but implied by the waveform nature)
- **Y-Axis:** Output Voltage \( v_o \) in volts

Overall Behavior and Trends
The waveform shows an oscillatory behavior indicating an AC signal superimposed on a DC level. The graph suggests that the output voltage \( v_o \) fluctuates around a central DC level \( V_O \), with peaks and troughs indicating the maximum \( v_o(\text{max}) \) and minimum \( v_o(\text{min}) \) amplitudes of the AC signal.

Key Features and Technical Details
- **Central DC Level:** \( V_O \) is the steady DC component around which the AC signal oscillates.
- **Amplitude:** The AC component varies between \( v_o(\text{max}) \) and \( v_o(\text{min}) \).
- **Waveform Shape:** The waveform is sinusoidal, typical for AC signals in amplification circuits.

Annotations and Specific Data Points
- The graph includes annotations for \( v_o(\text{max}) \), \( V_O \), and \( v_o(\text{min}) \), highlighting the peak, central, and trough points of the waveform.
- The waveform is labeled to show the AC component \( v_o = V_O + v_o \), indicating the superposition of AC on a DC level.
image_name:FIGURE 4.2(b)
image_name:(b)
description:
[
name: rop, type: Resistor, value: rop, ports: {N1: GND, N2: vo}
name: Q1, type: NPN, ports: {C: vo, B: vi, E: GND}
]
extrainfo:The circuit is an AC amplifier with an NPN transistor Q1. The input voltage vi is applied to the base of Q1, and the output voltage vo is taken from the collector. The resistor rop is used for biasing and setting the gain.
image_name:Waveform Shape
description:The graph labeled "Waveform Shape" is a time-domain waveform representation of an AC signal. The graph is sinusoidal, which is typical for AC signals involved in amplification circuits. The x-axis represents time, although it is not explicitly labeled with units, and the y-axis represents voltage, indicating the output voltage \( v_o \).

Axes Labels and Units
- **X-Axis:** Represents time (units not specified)
- **Y-Axis:** Represents voltage \( v_o \) (units not specified)

Overall Behavior and Trends
The waveform depicted is sinusoidal, showing periodic oscillations. It alternates between a maximum voltage \( v_o(\text{max}) \) and a minimum voltage \( v_o(\text{min}) \). The sinusoidal waveform suggests a consistent periodicity, characteristic of AC signals.

Key Features and Technical Details
- **Peaks and Troughs:** The waveform reaches its peak at \( v_o(\text{max}) \) and its trough at \( v_o(\text{min}) \).
- **Central Line:** The waveform oscillates around a central DC level, labeled as \( V_O \), indicating the DC offset around which the AC component \( v_o \) oscillates.
- **AC Component:** The annotation \( v_o = V_O + v_o \) highlights the superposition of the AC component on the DC level.

Annotations and Specific Data Points
The graph includes annotations for the peak \( v_o(\text{max}) \), the central DC level \( V_O \), and the trough \( v_o(\text{min}) \). These annotations help in understanding the amplitude and offset of the waveform. The sinusoidal shape is typical for circuits involving alternating current, especially in the context of amplification as indicated by the surrounding circuit diagram.

GND
(b)

FIGURE 4.2 (a) Conceptual circuit showing how to turn the discrete amplifier of Fig. 4.1 into a form suitable to monolithic fabrication. (b) Ac equivalent of the circuit of (a).

- The function of $R_{C}$ in Fig. 4.1 is to bias the collector, typically at $V_{O} \cong 2 / 3 V_{C C}$, while also setting the gain, as per Eq. $4.1 a$. The best way to get rid of $R_{C}$ is to replace it with a pnp BJT operating as a current source, as also shown in Fig. 4.2a. Once this is done, the ac equivalent becomes as in Fig. 4.2b, where $r_{o p}$ is the ac resistance seen looking into $Q_{4}$ 's collector, now playing the role of $R_{C}$ in the expression for the gain. Consequently, Eq. (4.1a) becomes

$$
\begin{equation*}
a=\frac{v_{o}}{v_{i}}=-g_{m n}\left(r_{o n} / / r_{o p}\right) \tag{4.1b}
\end{equation*}
$$

where we are using subscripts $n$ and $p$ to distinguish between the parameters of the $n p n$ and $p n p$ BJTs. Given that $R_{C}$ (a passive element) has been replaced by a transistor (an active element), $Q_{4}$ is aptly referred to as an active load.

We observe that for Eq. (4.1b) to hold, both BJTs must operate in the forwardactive region or at most at the edge of saturation (EOS). $Q_{1}$ will be in the active region so long as $v_{O} \geq v_{O(\text { min })}$, where $v_{O(\text { min })}=V_{E 1}+V_{C E 1(\mathrm{EOS})}$. But, $V_{E 1}=-V_{B E 1}$, so

$$
\begin{equation*}
v_{O(\min )}=V_{C E 1(\mathrm{EOS})}-V_{B E 1} \tag{4.2a}
\end{equation*}
$$

Similarly, $Q_{4}$ will be in the active region so long as $v_{O} \leq v_{O(\max )}$, where

$$
\begin{equation*}
v_{O(\max )}=V_{C C}-V_{E C 4(\mathrm{EOS})} \tag{4.2b}
\end{equation*}
$$

The voltages $v_{O(\min )}$ and $v_{O(\max )}$ define the lower and upper limits of the linear output voltage range, commonly known as the output voltage swing (OVS). It is apparent that Eq. (4.1b) will hold only so long as we confine $v_{o}$ within this range, that is, for $v_{O(\min )} \leq v_{O} \leq v_{O(\text { max })}$.
(a) In the circuit of Fig. $4.2 a$ let $Q_{1}$ have $I_{s}=10 \mathrm{fA}, V_{A}=100 \mathrm{~V}$, and $V_{C E(\operatorname{EOS})}=$

#### EXAMPLE 4.1

0.2 V , and let $Q_{4}$ have $I_{s}=5 \mathrm{fA}, V_{A}=75 \mathrm{~V}$, and $V_{E C(\mathrm{EOS})}=0.2 \mathrm{~V}$. If $V_{C C}=10 \mathrm{~V}$, specify suitable values for $V_{B E}$ and $V_{E B}$ so that with $v_{I}=0$ the BJTs draw 1 mA and $V_{O}$ lies in the middle of the OVS.
(b) Find the ac gain $a$ as well as $v_{o}(t)$ if $v_{I}(t)=V_{I}+v_{i}(t)=0 \mathrm{~V}+(2.5 \mathrm{mV}) \cos \omega t$. Does $v_{o}(t)$ fall within the linear output range at all times?

#### Solution

(a) By Eq. (4.2) we have

$$
v_{O(\min )} \cong 0.2-0.7=-0.5 \mathrm{~V} \quad v_{O(\max )} \cong 10-0.2=9.8 \mathrm{~V}
$$

To bias the output in the middle of the OVS we need

$$
V_{O}=\frac{1}{2}\left[v_{O(\max )}+v_{O(\min )}\right]=\frac{1}{2}(9.8-0.5)=4.65 \mathrm{~V}
$$

For $Q_{1}$ we have, by Eq. (2.21),

$$
I_{C 1}=I_{s} e^{V_{B E 1} / V_{T}}\left(1+\frac{V_{C E 1}}{V_{A 1}}\right)
$$

or

$$
10^{-3}=10 \times 10^{-15} \times e^{V_{B E} /(26 \mathrm{mV})}\left(1+\frac{4.65-(-0.7)}{100}\right)
$$

Solving, we get $V_{B E 1}=657.2 \mathrm{mV}$. Adapting the above expression to $Q_{4}$ 's collector current yields

$$
10^{-3}=5 \times 10^{-15} \times e^{V_{E A /} /(26 \mathrm{mV})}\left(1+\frac{10-4.65}{75}\right)
$$

which gives $V_{E B 4}=674.8 \mathrm{mV}$.
(b) We have $g_{m n}=1 /(26 \Omega), r_{o n}=100 \mathrm{k} \Omega$, and $r_{o p}=75 \mathrm{k} \Omega$, so Eq. (4.1b) gives

$$
a=-\frac{100 / / 75}{0.026}=-1,648 \mathrm{~V} / \mathrm{V}
$$

Finally, since $(2.5 \mathrm{mV}) \times 1648=4.12 \mathrm{~V}$, we have

$$
v_{o}(t)=V_{O}+v_{o}(t)=4.65 \mathrm{~V}+(4.12 \mathrm{~V}) \cos \left(\omega t-180^{\circ}\right)
$$

Note that $v_{O}$ alternates between $4.65+4.12=8.77 \mathrm{~V}$ and $4.65-4.12=0.53 \mathrm{~V}$, indicating that the condition $v_{O(\min )}<v_{O}<v_{O(\max )}$ is satisfied at all times.

We observe that the gain achievable with an active load can be much higher than with a discrete load, thanks to the fact that usually $r_{o p} \gg R_{C}$. High gains are especially welcome in negative-feedback systems such as op amp circuits, where the higher the gain the more pronounced the benefits of negative feedback tend to be (this will become clear when we study negative feedback in Chapter 7.)

As we move along we shall see that we can increase gain further by suitably raising the effective resistance seen looking into $Q_{4}$ 's collector, for instance, by introducing emitter degeneration for $Q_{4}$. If this resistance is made much higher than $r_{o n}$, then the ac gain of Eq. (4.1b) simplifies as $a=a_{\text {intrinsic }}$, where

$$
\begin{equation*}
a_{\text {intrinsic }}=-g_{m} r_{o}=-\frac{V_{A}}{V_{T}} \tag{4.3}
\end{equation*}
$$

Here, $V_{A}$ is the Early voltage of the amplifying BJT ( $Q_{1}$ in the present case), $V_{T}$ is the thermal voltage ( 26 mV at $T=300 \mathrm{~K}$ ), and $a_{\text {intrinsic }}$ is the maximum gain achievable with a single BJT, a gain aptly called the intrinsic gain. In Example 4.1 we have $a_{\text {intrinsic }}=-100 / 0.026=-3846 \mathrm{~V} / \mathrm{V}$. Compare this with the case of a typical passive load of the types investigated in Chapter 2, say $R_{C}=10 \mathrm{k} \Omega$, which would give $a=-(100 / / 10) / 0.026=-350 \mathrm{~V} / \mathrm{V}$, a whole order of magnitude lower than the intrinsic gain!

At this point we wonder how to implement the sources $V_{B E 1}$ and $V_{E B 4}$ of Fig. 4.2a. Example 4.1 indicates that their values must be accurate within millivolts. We also know that these values drift with temperature by about $-2 \mathrm{mV} /{ }^{\circ} \mathrm{C}$, so we need biasing schemes capable of assuring stable collector currents against a range of fabrication and environmental variations. In IC technology these schemes are made possible by the aforementioned availability of matching and tracking, as it will be demonstrated next.

### Emitter-Coupled Pairs

The scheme shown in Fig. 4.3a utilizes a current sink $\left(2 I_{E}\right)$ to provide dc biasing, and a second BJT ( $Q_{2}$ ) to provide a low ac-resistance path between $Q_{1}$ 's emitter and ground. (Viewed this way, $Q_{2}$ in effect replaces the ac bypass capacitance $C_{2}$ of Fig. 4.1.) If $Q_{1}$ and $Q_{2}$ are matched, then for $v_{i}=0$ the sink current $2 I_{E E}$ will split equally between the two BJTs as they experience the same $V_{B E}$ drop. Moreover, the two currents $I_{E}$ will track each other over a range of thermal variations in $V_{B E}$.

The ac resistance between $Q_{1}$ 's emitter and ground is the resistance seen looking into $Q_{2}$ 's emitter, or $r_{e 2}=\alpha_{02} / g_{m 2} \cong 1 / g_{m 2}\left(=1 / g_{m 1}\right)$. This resistance, though not zero, is small ( $26 \Omega$ at 1 mA ) and introduces emitter degeneration for $Q_{1}$, as depicted in the ac equivalent of Fig. 4.3b. The degenerated transconductance is

$$
\begin{equation*}
G_{m}=\frac{g_{m 1}}{1+g_{m 1} r_{e 2}} \cong \frac{g_{m 1}}{1+g_{m 1} / g_{m 2}}=\frac{g_{m}}{2} \tag{4.4}
\end{equation*}
$$

where the $n$ and $p$ subscripts have been dropped as the BJTs have identical $g_{m}$ s. Because of degeneration the voltage gain will also be reduced, but this price is well worth the elimination of $C_{2}$. In fact, even with degeneration, gain continues to remain fairly high, and it does so all the way down to dc!
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: X2, B: GND, E: -V_BE}
name: Q2, type: NPN, ports: {C: GND, B: GND, E: -V_BE}
name: Q4, type: PNP, ports: {C: X2, B: X1, E: VCC}
name: V_CC, type: VoltageSource, value: V_CC, ports: {Np: V_CC, Nn: GND}
name: V_EE, type: VoltageSource, value: V_EE, ports: {Np: GND, Nn: V_EE}
name: V_EB, type: VoltageSource, value: V_EB, ports: {Np: VCC, Nn: X2}
]
extrainfo:The circuit is a biasing scheme for an amplifier with a current mirror configuration for biasing Q4. The current through Q4 (PNP) is mirrored to match the current through Q1 (NPN). The circuit eliminates the need for a coupling capacitor C2 while maintaining high gain down to DC.

(a)
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: Vo, B: Vi, E: X1}
name: rop, type: Resistor, value: rop, ports: {N1: Vo, N2: GND}
name: re2, type: Resistor, value: re2, ports: {N1: X1, N2: GND}
name: vi, type: VoltageSource, value: vi, ports: {Np: Vi, Nn: GND}
]
extrainfo:This circuit represents a biasing scheme for an amplifier using a current mirror configuration. The NPN transistor Q1 is biased to maintain the current through it, and the design eliminates the need for a coupling capacitor while maintaining high gain down to DC. The resistor rop is connected from the collector of Q1 to GND, and the resistor re2 is connected from the emitter of Q1 to GND. The input voltage vi is applied to the base of Q1.

(b)

FIGURE 4.3 (a) Biasing scheme for the amplifier $Q_{1}$, and
(b) ac equivalent for the entire circuit.

### Current Mirrors

Next, we wish to investigate a suitable IC scheme to bias $Q_{4}$. Since the current $I_{C 4}$ sourced by $Q_{4}$ must at all times equal the current $I_{C 1}$ sunk by $Q_{1}$, it is apparent that $V_{E B}$ must be adjusted continuously against any thermal variations. The scheme of Fig. 4.4 does this automatically via $Q_{2}$ and the diode-connected transistor $Q_{3}$ as follows: as we know, $I_{C 2}$ matches $I_{C 1}$; moreover, in response to $I_{C 2}, Q_{3}$ develops a voltage drop $V_{E B}$ that is in turn transmitted to $Q_{4}$. Being matched and subject to the same $V_{E B}$ drive,
image_name:Figure 4.4
description:
[
name: Q1, type: NPN, ports: {C: X2, B: GND, E: -VBE}
name: Q2, type: NPN, ports: {C: X1, B: GND, E: -VBE}
name: Q3, type: PNP, ports: {C: X1, B: X1, E: VCC}
name: Q4, type: PNP, ports: {C: X2, B: X1, E: VCC}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: VEE, type: VoltageSource, value: VEE, ports: {Np: GND, Nn: VEE}
name: 2IE, type: CurrentSource, value: 2IE, ports: {Np: -VBE, Nn: GND}
]
extrainfo:The circuit is a biasing scheme for the active load Q4. It uses a current mirror configuration where Q4 mirrors Q3, ensuring that IC4 tracks IC1 regardless of thermal variations. The circuit is designed to maintain the collector current IC4 equal to IC1 by using Q2 and a diode-connected Q3 to adjust VEB automatically.

FIGURE 4.4 Biasing scheme for the active load $Q_{4}$.
$Q_{4}$ will draw as much collector current as $Q_{3}$, this being the reason why $Q_{4}$ is said to mirror $Q_{3}$. Ignoring base currents, we summarize by stating that $I_{C 4}$ mirrors $I_{C 3}$, which is the same as $I_{C 2}$, which in turn tracks $I_{C 1}$. Consequently, $I_{C 4}$ will track $I_{C 1}$ regardless of any thermal drift of $V_{E B}$ or $V_{B E}$ ! The current mirror, already introduced in its most basic form in Chapters 2 and 3, finds wide application both in bipolar and CMOS ICs and will be investigated in great depth in Section 4.8.

### Monolithic Voltage Amplifiers

Aptly referred to as an emitter-coupled pair (EC pair), the $Q_{1}-Q_{2}$ pair of Fig. 4.4 exhibits an interesting and useful symmetry: just like $Q_{2}$ provides a low-resistance to $Q_{1}$ 's emitter, $Q_{1}$ provides the same function for $Q_{2}$. This reciprocity suggests that we can apply the input to either of the two bases, or even drive the two bases simultaneously with separate signals, thus increasing the circuit's flexibility. In fact we shall see that the two base signals influence the output in equal but opposite amounts, indicating that the output depends on the difference between the inputs, this being the reason why the EC pair is also referred to as a differential pair. Differential pairs form the input stages of a wide variety of monolithic circuits, such as operational amplifiers and voltage comparators, and they will be investigated in great depth in Section 4.5.

Figure $4.5 a$ shows a popular monolithic counterpart of the discrete design of Fig. 4.1. Its basic ingredients are as follows:

- The EC pair $Q_{1}-Q_{2}$ provides signal amplification, and it does so in differential form.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: vo, B: Vi1, E: P}
name: Q2, type: NPN, ports: {C: x2, B: Vi2, E: P}
name: Q3, type: PNP, ports: {C: VCC, B: x2, E: x2}
name: Q4, type: PNP, ports: {C: VCC, B: x2, E: Vo}
name: Q5, type: NPN, ports: {C: x1, B: x1, E: VEE}
name: Q6, type: NPN, ports: {C: p, B: x1, E: VEE}
name: R, type: Resistor, value: R, ports: {N1: x1, N2: GND}
name: Vi1, type: VoltageSource, value: Vi1, ports: {Np: Vi1, Nn: GND}
name: Vi2, type: VoltageSource, value: Vi2, ports: {Np: Vi2, Nn: GND}
]
extrainfo:The circuit is a high-gain monolithic amplifier using bipolar transistors. The EC pair Q1-Q2 provides differential signal amplification, while the current mirror Q3-Q4 acts as an active load, ensuring high gain and converting the input differential signal to a single-ended output. Q5-Q6 provide DC biasing for the circuit.
image_name:(b)
description:
[
name: Vi1, type: VoltageSource, value: Vi1, ports: {Np: vi1, Nn: GND}
name: Vi2, type: VoltageSource, value: Vi2, ports: {Np: vi2, Nn: GND}
name: M1, type: NMOS, ports: {S: P, D: vo, G: vi1}
name: M2, type: NMOS, ports: {S: P, D: x1, G: vi2}
name: M3, type: PMOS, ports: {S: VDD, D: x1, G: x1}
name: M4, type: PMOS, ports: {S: VDD, D: x1, G: x1}
name: M5, type: NMOS, ports: {S: VSS, D: x2, G: x2}
name: M6, type: NMOS, ports: {S: VSS, D: P, G: x2}
name: M7, type: NMOS, ports: {S: X2, D: GND, G: GND}
]
extrainfo:The circuit is a CMOS differential amplifier with a current mirror load. The NMOS transistors M1 and M2 form the differential pair, while PMOS transistors M3 and M4 act as the current mirror load, converting the differential input into a single-ended output at node x1. NMOS transistors M5 and M6 are part of the current mirror providing biasing, and M7 is used for additional biasing.

FIGURE 4.5 High-gain monolithic amplifiers: (a) bipolar and (b) CMOS.

- The current mirror $Q_{3}-Q_{4}$ forms an active load for the EC pair, assuring high gain and also converting the input signal difference to a single-ended output. As we move along we shall see that the gain is

$$
\begin{equation*}
a=\frac{v_{o}}{v_{i 1}-v_{i 2}}=-g_{m n}\left(r_{o n} / / r_{o p}\right) \tag{4.5}
\end{equation*}
$$

- Another current mirror $\left(Q_{5}-Q_{6}\right)$ is used to provide the dc bias for the EC pair. Here, $R$ establishes the current into the diode-connected BJT $Q_{5}$, and $Q_{6}$ then mirrors this current (now re-labeled as $I_{E E}$ ) to the EC pair, but at a higher outputresistance level ( $r_{o 6}$ in the present case).

Compared to the discrete predecessor of Fig. 4.1, the monolithic version of Fig. $4.5 a$ might seem far more complex and expensive to fabricate. However, considering that it uses no capacitors and just one resistor, and that transistors are the preferred devices in IC technology, the monolithic version is highly desirable indeed. It is also more flexible as it responds to the difference between a pair of input signals, not to mention its ability to provide much higher voltage gains.

By the time MOS technology became commercially viable, the canons of IC design were already well established in bipolar technology, so it was a straightforward matter to transfer them directly to the new technology. Shown in Fig. 4.5b is the CMOS counterpart of the bipolar version of Fig. 4.5a. In this example even the current-setting resistor $R$ has been replaced by a transistor, namely, the diode-connected MOSFET $M_{7}$, whose $W / L$ ratio is chosen so as to achieve the desired bias current $I_{S S}$. As we move along, we shall see that Eq. (4.5) applies to the CMOS amplifier version as well, the only difference being in the lower transconductances of FETs. (The circuits of Fig. 4.5 will be investigated in great depth in Section 4.9.)

Figure 4.6 shows a PSpice circuit to display the VTC of the bipolar amplifier of Fig. 4.5a. The steepness of the curve confirms the high gain of the circuit. Also shown are the saturation limits of the linear region of operation.

### What to Expect

The discussion leading to the amplifiers of Fig. 4.5 provides a nutshell overview of the most relevant considerations in monolithic design:

- Avoid the use of on-chip resistors and capacitors. If capacitors are required, they should be on the order of a few picofarads or less.
- Resistances will continue to appear in our circuits and calculations, but for the most part they will be the resistances of small-signal transistor models, such as $r_{o p}$ and $r_{e 2}$ of Fig. 4.3b.
- Exploit the availability of matched and tracking characteristics to devise creative design solutions, such as current mirrors and differential pairs.
- Even though IC design follows a different set of rules than discrete design, the study of ICs still relies very heavily on the foundations provided by Chapters 1 through 3.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: X1, B: VID, E: P}
name: Q2, type: NPN, ports: {C: Vo, B: GND, E: P}
name: Q3, type: PNP, ports: {C: X1, B: x1, E: VCC}
name: Q4, type: PNP, ports: {C: Vo, B: X1, E: VCC}
name: V_ID, type: VoltageSource, value: V_ID, ports: {Np: VID, Nn: GND}
name: I_EE, type: CurrentSource, value: 1 mA, ports: {Np: P, Nn: VEE}
]
extrainfo:This circuit is a differential amplifier with a current mirror load. It includes two NPN transistors (Q1 and Q2) and two PNP transistors (Q3 and Q4). The input voltage is applied at VID, and the output is taken from Vo. The circuit is biased with a current source I_EE of 1 mA.
image_name:(b)
description:The graph in Figure 4.6(b) is a Voltage Transfer Characteristic (VTC) plot for a monolithic amplifier. It displays the relationship between the input differential voltage \( v_{ID} \) and the output voltage \( v_o \).

1. **Type of Graph and Function:**
- The graph is a VTC plot.
- It shows the output voltage \( v_o \) as a function of the input differential voltage \( v_{ID} \).

2. **Axes Labels and Units:**
- The x-axis represents the input voltage \( v_{ID} \) in millivolts (mV).
- The y-axis represents the output voltage \( v_o \) in volts (V).
- Both axes use a linear scale.

3. **Overall Behavior and Trends:**
- The graph exhibits a sigmoidal shape typical of amplifier transfer characteristics.
- For input voltages \( v_{ID} \) less than approximately -5 mV, the output voltage \( v_o \) remains near 0 V, indicating the amplifier is in cutoff.
- As \( v_{ID} \) increases from -5 mV to 5 mV, the output voltage \( v_o \) transitions sharply from 0 V to approximately 10 V, showing the active region of the amplifier.
- For \( v_{ID} \) greater than approximately 5 mV, the output voltage \( v_o \) saturates at around 10 V.

4. **Key Features and Technical Details:**
- The transition region, where the amplifier is active, is centered around \( v_{ID} = 0 \) mV.
- The slope of the curve in the transition region represents the gain of the amplifier.
- The output voltage saturates at the power supply limits, around 0 V and 10 V.

5. **Annotations and Specific Data Points:**
- There are no specific annotations or markers on the graph.
- The graph clearly illustrates the cutoff, active, and saturation regions of the amplifier's operation.

FIGURE 4.6 (a) PSpice circuit to plot (b) the VTC of the monolithic amplifier of Fig. 4.5a. The following parameters are assumed: Qn: $I_{s}=2 \mathrm{fA}, \beta_{F}=200, V_{A}=100 \mathrm{~V}$. Qp: $I_{s}=1 \mathrm{fA}, \beta_{F}=50$, $V_{A}=50 \mathrm{~V}$.

- We shall make frequent use of PSpice simulation to corroborate the result of hand analysis as well as to investigate higher-order nuances that often escape paper-and-pencil calculations.

In order to proceed, we need to investigate in more systematic detail the currentmirror and differential-pair concepts introduced above, as well as a variety of other canonical blocks that are at the basis of contemporary monolithic design. However, before embarking on these tasks, we need to reexamine the characteristics and models for active devices (both BJTs and MOSFETs) in finer detail.

## 4.2 BJT CHARACTERISTICS AND MODELS REVISITED

The BJT characteristics and models of Chapter 2 were deliberately kept as simple as possible to allow the beginner to focus on the essentials of discrete circuit design and develop a basic feel for circuit operation. As we embark upon the study of monolithic circuits, we need to suitably refine our BJT models to include second-order effects that tend to play more prominent roles in these types of circuits.

### Base Width Modulation Revisited

In our study of npn BJT operation we found that increasing $v_{C E}$ expands the width of the base-collector depletion region, thus shrinking the effective base width $W_{B}$. This phenomenon, known as the Early effect, yields a steeper profile of excess electrons within the base, ultimately raising the collector current $i_{C}$ because it is proportional to
image_name:Q
description:
[
name: Q, type: NPN, ports: {C: C, B: B, E: E}
]
extrainfo:The circuit diagram represents a small-signal model of an NPN BJT including the Early effect. The model includes resistors r_pi and r_mu, and a voltage-controlled current source g_m*v_be to represent the transconductance.
image_name:
description:
[
'name': 'r_π', 'type': 'Resistor', 'value': 'r_π', 'ports': {'N1': 'B', 'N2': 'E'
'name': 'r_μ', 'type': 'Resistor', 'value': 'r_μ', 'ports': {'N1': 'B', 'N2': 'C'
'name': 'g_m v_be', 'type': 'VoltageControlledCurrentSource', 'ports': {'Np': 'C', 'Nn': 'E'
'name': 'r_o', 'type': 'Resistor', 'value': 'r_o', 'ports': {'N1': 'C', 'N2': 'E'
]
extrainfo:The circuit diagram represents a small-signal model of an NPN BJT, including the Early effect modeled by the resistor r_o and the voltage-controlled current source g_m v_be. The resistors r_π and r_μ model the base-emitter and base-collector resistances, respectively.
image_name:FIGURE 4.7
description:
[
name: Q, type: NPN, ports: {C: C, B: B, E: E}
]
extrainfo:The circuit represents a small-signal model of an NPN BJT including base-width modulation effects. The model includes resistors r_π and r_μ, a voltage-controlled current source g_mV_be, and a resistor r_o to account for the Early effect.

FIGURE 4.7 Small-signal BJT model including $r_{\mu}$.
this profile's slope. There is yet another more subtle effect of base-width modulation, for a reduction in $W_{B}$ reduces also the recombination component $i_{B B}$ of the total base current $i_{B}$. We recall that $i_{B}=i_{B E}+i_{B B}$, where $i_{B E}$ is the diffusion component from base to emitter, and $i_{B B}$ is the recombination component within the base. According to Eq. (2.14), $i_{B B}$ is proportional to the excess charge in the base region, in turn proportional to the volume $A_{E} \times W_{B}$, so a reduction in $W_{B}$ will also reduce $i_{B B}$, and hence, $i_{B}$. In summary, if we increase $v_{C E}$ while keeping $v_{B E}$ constant, we witness (a) an increase in the current $i_{C}$ drawn from the $v_{C E}$ source, and (b) a decrease in the current $i_{B}$ drawn from the $v_{B E}$ source. In small-signal operation we model the former by means of the familiar resistance $r_{o}$ between collector and emitter, and the latter by means of an additional resistance $r_{\mu}$ between collector and base. The resulting more refined model is depicted in Fig. 4.7.

Assuming $v_{B E}$ is held constant, we find $r_{\mu}$ as

$$
\frac{1}{r_{\mu}}=\frac{d i_{B B}}{d v_{C E}}=\frac{d i_{C}}{d v_{C E}} \frac{d i_{B B}}{d i_{C}}=\frac{1}{r_{o}} \frac{d i_{B B}}{d i_{C}}
$$

or

$$
\begin{equation*}
r_{\mu}=\frac{i_{c}}{i_{b b}} r_{o} \tag{4.6}
\end{equation*}
$$

where $i_{c}$ and $i_{b b}$ are small-signal variations of $i_{C}$ and $i_{B B}$. If $i_{B}$ consisted entirely of $i_{B B}$, then we would have $i_{c} / i_{b b}=i_{c} / i_{b}=\beta_{0}$, and Eq. (4.6) would give $r_{\mu}=r_{\mu(\min )}$, where

$$
\begin{equation*}
r_{\mu(\min )}=\beta_{0} r_{o} \tag{4.7}
\end{equation*}
$$

However, $i_{B B}$ is only a fraction of $i_{B}$, so if we write $i_{b b}=(1 / m) i_{b}, m \geq 1$, then Eq. (4.6) becomes

$$
\begin{equation*}
r_{\mu}=m \beta_{0} r_{o} \tag{4.8}
\end{equation*}
$$

In monolithic npn BJTs, $i_{B E}$ usually dominates and $i_{B B}$ is on the order of only $10 \%$ of $i_{B}(m=10)$, so it is common practice to assume $r_{\mu} \cong 10 \beta_{0} r_{o}$. Because of its sheer size, $r_{\mu}$ is usually ignored except for a few special cases, as we shall see. In lateral pnp BJTs (see Fig 2.3) the recombination component is far more significant, so in this case $r_{\mu}$ is closer to the lower limit of Eq. (4.7).

### Bulk Resistances in the BJT

The materials making up the emitter, base, and collector regions exhibit nonzero resistances that need to be taken into account in high-accuracy BJT modeling. To include these higher-order effects, the small-signal model is augmented as in Fig. 4.8. To understand the origin of these bias-independent resistances, also called bulk resistances, refer to the BJT structure of Figs. 2.1 and 2.2:

- The emitter region is short and heavily doped, so its bulk resistance $r_{e x}$ (not to be confused with $\left.r_{e}=\alpha_{0} / g_{m}\right)$ is rather small and fixed. In monolithic BJTs $r_{e x}$ is on the order of just a few Ohms.
- The base region is doped more lightly than the emitter and it also forms a longer conductive path, especially transversally, so $r_{b}$ is one to two orders of magnitude higher than $r_{e x}$. In monolithic BJTs $r_{b}$ typically ranges from 50 to $500 \Omega$. Note that the voltage controlling the dependent source is the internal voltage $v_{\pi}$, not the terminal voltage $v_{b e}$ ! For $r_{e x} \cong 0$, the two are related as $v_{\pi}=v_{b e} \times r_{\pi} /\left(r_{b}+r_{\pi}\right)$.
- The collector region is doped even more lightly in order to assure an adequately high value of $B V_{C E O}$, and it forms an even longer conductive path. This would result in an unacceptably high bulk resistance. In the planar process this drawback is reduced drastically by fabricating a highly conductive buried layer, as shown in Fig. 2.2. This heavily doped layer provides a low-resistance path for electrons once they have crossed from the $p$ base into the $n^{-}$collector region and thence to the buried layer itself. By this artifice, the overall resistance $r_{c}$ is kept in the range of 20 to $500 \Omega$. (Nowadays the $n^{+}$collector diffusion is extended all the way to the buried layer so as to minimize $r_{c}$.)

The model of Fig. 4.8 is referred to as a low-frequency model. When studying the frequency response of BJT circuits, in Chapter 6, we will need to augment this model with appropriate parasitic capacitances. At low operating frequencies these capacitances act as open circuits and will thus be ignored. Not so at high frequencies, where they become significant and tend to alter circuit behavior dramatically. To keep hand calculations manageable we will ignore $r_{b}, r_{e x}, r_{c}$, and $r_{\mu}$ whenever possible. Only when their presence has an appreciable impact shall we take them into proper consideration.
image_name:FIGURE 4.8 Complete small-signal model of the BJT at low frequencies
description:
[
name: rb, type: Resistor, value: rb, ports: {N1: B, N2: X3}
name: rπ, type: Resistor, value: rπ, ports: {N1: X3, N2: X2}
name: rμ, type: Resistor, value: rμ, ports: {N1: X3, N2: X1}
name: rex, type: Resistor, value: rex, ports: {N1: X2, N2: E}
name: rc, type: Resistor, value: rc, ports: {N1: X1, N2: C}
name: ro, type: Resistor, value: ro, ports: {N1: X1, N2: X2}
name: gmvπ, type: VoltageControlledCurrentSource, value: gmvπ, ports: {Np: X1, Nn: X2}
]
extrainfo:The circuit is a small-signal model of a BJT at low frequencies, illustrating the various resistances and the controlled current source representing the transistor's transconductance.

FIGURE 4.8 Complete small-signal model of the BJT at low frequencies.

### The Small-Signal Resistances Seen Looking into the Terminals of a BJT

While investigating the resistance-transformation abilities of the BJT in connection with Fig. 2.42, we stipulated an ac grounded collector in order to keep our derivations simple. The results obtained there provide good approximations for discrete designs, where the net equivalent resistance external to the collector is not very large. However, in monolithic circuits the collector is often terminated on an active load whose equivalent resistance can be quite high, rendering the results of Chapter 2 no longer adequate. We need to reexamine the resistance transformation ability of the BJT but using the more general ac circuit of Fig. 4.9. The main novelty now is the coupling established by $r_{o}$ between $R_{C}$ and the internal circuitry of the BJT model. As usual, we utilize lower-case subscripts to distinguish the small-signal resistances $R_{b}, R_{e}$, and $R_{c}$ from the external resistances $R_{B}$, $R_{E}$, and $R_{C}$.

- The Resistance $\boldsymbol{R}_{b}$ Seen Looking into the Base. The circuit to find this resistance is shown in Fig. 4.10a. Ignoring $r_{\mu}$ because of its sheer size, we use Ohm's law to write

$$
i_{b}=\frac{v_{b}-v_{e}}{r_{\pi}}
$$

We need another equation to eliminate $v_{e}$, so we apply KCL at node $v_{e}$ and write

$$
\frac{v_{b}-v_{e}}{r_{\pi}}+\beta_{0} i_{b}+\frac{v_{c}-v_{e}}{r_{o}}=\frac{v_{e}}{R_{E}}
$$

Now, we need yet another equation to eliminate $v_{c}$, so we again apply KCL at $v_{c}$ and write

$$
\frac{0-v_{c}}{R_{C}}=\beta_{0} i_{b}+\frac{v_{c}-v_{e}}{r_{o}}
$$

image_name:Figure 4.9
description:
[
name: Q1, type: NPN, ports: {C: c, B: b, E: e}
name: RC, type: Resistor, value: RC, ports: {N1: c, N2: GND}
name: RB, type: Resistor, value: RB, ports: {N1: b, N2: GND}
name: RE, type: Resistor, value: RE, ports: {N1: e, N2: GND}
]
extrainfo:The circuit is a small-signal model of a BJT with resistors connected to the collector, base, and emitter. It shows the calculation of resistances looking into the BJT's terminals.
image_name:Equations for R_b, R_e, R_c
description:The image consists of a schematic diagram on the left and a set of equations on the right.

**Schematic Diagram:**
- The diagram shows a bipolar junction transistor (BJT) labeled as Q1, with its three terminals: base (b), collector (c), and emitter (e).
- The base is connected to a resistor labeled \( R_B \) and \( R_b \) leading to ground (GND).
- The collector is connected to a resistor labeled \( R_C \) also leading to GND.
- The emitter is connected to a resistor labeled \( R_E \) leading to GND.

**Equations:**
- The equations provide expressions for the resistances \( R_b \), \( R_e \), and \( R_c \) seen looking into the BJT's terminals.
- **\( R_b \):**
\[
R_b = r_{\pi} + (\beta_0 + 1)(R_E // r_o) \times \frac{1 + R_C/[(\beta_0 + 1)r_o]}{1 + R_C/(R_E + r_o)}
\]
- **\( R_e \):**
\[
R_e = \left(\frac{R_B + r_{\pi}//r_o}{\beta_0 + 1}\right) \times \frac{1 + R_C/r_o}{1 + R_C/[(\beta_0 + 1)r_o + R_B + r_{\pi}]}
\]
- **\( R_c \):**
\[
R_c \approx r_o \left[1 + \frac{g_m(r_{\pi}//R_E)}{1 + R_B/(r_{\pi} + R_E)}\right] // \left[\frac{r_{\mu}}{1 + (R_B/R_b)/(R_E + 1/g_m)}\right]
\]

These equations describe the small-signal resistances at the BJT's terminals, taking into account various parameters such as \( r_{\pi} \), \( \beta_0 \), \( R_E \), \( r_o \), and \( g_m \). The schematic and equations are used in the analysis of transistor circuits to determine input and output resistances.

FIGURE 4.9 The small-signal resistances seen looking into the BJT's terminals.
image_name:(a)
description:
[
name: Vb, type: VoltageSource, value: Vb, ports: {Np: GND, Nn: B}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vb, N2: ve}
name: rμ, type: Resistor, value: rμ, ports: {N1: vb, N2: Vc}
name: ro, type: Resistor, value: ro, ports: {N1: Vc, N2: Ve}
name: RC, type: Resistor, value: RC, ports: {N1: Vc, N2: GND}
name: RE, type: Resistor, value: RE, ports: {N1: Ve, N2: GND}
name: βib, type: VoltageControlledCurrentSource, value: βib, ports: {Np: Vc, Nn: Ve'}
]
extrainfo:The circuit diagram (a) is a small-signal model of a BJT with various resistances and a voltage-controlled current source. It analyzes the resistances seen at the BJT terminals, considering parameters such as rπ, rμ, ro, and RE.
image_name:(b)
description:
[
'name': 'r_pi', 'type': 'Resistor', 'value': 'r_pi', 'ports': {'N1': 'X1', 'N2': 'E'}
'name': 'r_mu', 'type': 'Resistor', 'value': 'r_mu', 'ports': {'N1': 'x1', 'N2': 'Vc'}
'name': 'Rc', 'type': 'Resistor', 'value': 'Rc', 'ports': {'N1': 'Vc', 'N2': 'GND'}
'name': 'Ro', 'type': 'Resistor', 'value': 'ro', 'ports': {'N1': 'Vc', 'N2': 'E'}
'name': 'Rb', 'type': 'Resistor', 'value': 'Rb', 'ports': {'N1': 'X1', 'N2': 'GND'}
'name': 'V_e', 'type': 'VoltageSource', 'value': 've', 'ports': {'Np': 'E', 'Nn': 'GND'}
'name': 'CurrentControlledCurrentSource', 'type': 'CurrentControlledCurrentSource', 'value': 'β0ib', 'ports': {'Np': 'Vc', 'Nn': 'E'}
]
extrainfo:Test circuit (b) is used to find the emitter resistance R_e. It includes a voltage source V_e and a current-controlled current source dependent on β0ib.

FIGURE 4.10 Test circuits to find (a) $R_{b}$ and (b) $R_{e}$.

Eliminating $v_{e}$ and $v_{c}$, collecting, and taking the ratio $R_{b}=v_{b} / i_{b}$ gives, after some algebra,

$$
\begin{equation*}
R_{b}=r_{\pi}+\left(\beta_{0}+1\right)\left(R_{E} / / r_{o}\right) \times \frac{1+R_{C} /\left[\left(\beta_{0}+1\right) r_{o}\right]}{1+R_{C} /\left(R_{E}+r_{o}\right)} \tag{4.9}
\end{equation*}
$$

It is apparent that as long as $R_{C} \ll\left(\beta_{0}+1\right) r_{o}$ and $R_{C} \ll\left(R_{E}+r_{o}\right)$, Eq. (4.9) reduces to the familiar form $R_{b}=r_{\pi}+\left(\beta_{0}+1\right)\left(R_{E} / / r_{o}\right)$. In the discrete designs of Chapter 2, $R_{C}$ was always small enough to meet these conditions. However, this is not necessarily the case in monolithic designs, where the collector may be terminated on an active load and therefore $R_{C}$ can be quite large. In fact, you can verify that in the limit $R_{C} \rightarrow \infty$, Eq. (4.9) gives $R_{b} \rightarrow r_{\pi}+R_{E}$ ! To justify this surprising result, note that letting $R_{C}=\infty$ in Fig. 4.10a will force the current $\beta_{0} i_{b}$ to circulate entirely in $r_{o}$, making the two elements act as a self-contained subcircuit. Consequently, the source $v_{i}$ sees just $r_{\pi}$ in series with $R_{E}$ !

EXAMPLE 4.2 Let the BJT of Fig. 4.9 have $\beta_{0}=100, r_{\pi}=2.6 \mathrm{k} \Omega$, and $r_{o}=100 \mathrm{k} \Omega$. If $R_{E}$ $=1.0 \mathrm{k} \Omega$, find $R_{b}$ in the limits $R_{C} \rightarrow 0$ and $R_{C} \rightarrow \infty$. For what value of $R_{C}$ does $R_{b}$ drop to $90 \%$ of the value corresponding to $R_{C} \rightarrow 0$ ?

#### Solution

By Eq. (4.9),

$$
\begin{aligned}
& \lim _{R_{c} \rightarrow 0} R_{b}=r_{\pi}+\left(\beta_{0}+1\right)\left(R_{E} / / r_{o}\right)=2.6+101(1 / / 100) \cong 103 \mathrm{k} \Omega \\
& \lim _{R_{c} \rightarrow \infty} R_{b}=r_{\pi}+R_{E}=2.6+1=3.6 \mathrm{k} \Omega
\end{aligned}
$$

Imposing

$$
0.9 \times 103=2.6+(1 / / 100) \frac{1+R_{C} /(101 \times 100)}{1+R_{C} /(1+100)}
$$

and solving gives $R_{C}=11.5 \mathrm{k} \Omega$.

- The Resistance $\boldsymbol{R}_{e}$ Seen Looking into the Emitter. Summing currents into the emitter node of Fig. 4.10b gives

$$
\left(\beta_{0}+1\right) i_{b}+i_{e}+\frac{v_{c}-v_{e}}{r_{o}}=0
$$

We need two additional equations to eliminate $i_{b}$ and $v_{c}$. Again ignoring $r_{\mu}$, we use Ohm's law to write

$$
i_{b}=\frac{0-v_{e}}{R_{B}+r_{\pi}}
$$

Moreover, KCL at the collector node gives

$$
\frac{0-v_{c}}{R_{C}}=\beta_{0} i_{b}+\frac{v_{c}-v_{e}}{r_{o}}
$$

Eliminating, collecting and solving for the ratio $R_{e}=v_{e} / i_{e}$ gives, after some algebra,

$$
\begin{equation*}
R_{e}=\left(\frac{R_{B}+r_{\pi}}{\beta_{0}+1} / / r_{o}\right) \times \frac{1+R_{C} / r_{o}}{1+R_{C} /\left[\left(\beta_{0}+1\right) r_{o}+R_{B}+r_{\pi}\right]} \tag{4.10}
\end{equation*}
$$

As long as $R_{C} \ll r_{o}$ this equation reduces to the familiar form of discrete designs, namely, $R_{e} \cong\left[\left(R_{B}+r_{\pi}\right) /\left(\beta_{0}+1\right)\right] / / r_{o}$, which is small because of the term $\left(\beta_{0}+1\right)$ in the denominator. However, if the collector is terminated on a current source, $R_{C}$ can be sufficiently large to raise $R_{e}$ dramatically. In fact, one can easily verify that in the limit $R_{C} \rightarrow \infty$ Eq. (4.10) gives $R_{e} \rightarrow R_{B}+r_{\pi}$ ! Again, with the collector ac open circuited, the current $\beta_{0} i_{b}$ will circulate exclusively in $r_{o}$, making the two elements act as a self-contained subcircuit. Consequently, the source $v_{e}$ sees just $r_{\pi}$ in series with $R_{B}$.

- The Resistance $\boldsymbol{R}_{\boldsymbol{c}}$ Seen Looking into the Collector. With sufficient emitter degeneration the resistance seen looking into the collector can be quite large, so ignoring $r_{\mu}$ may no longer be acceptable. Unfortunately, the inclusion of $r_{\mu}$ in the calculations complicates the algebra significantly and without providing much insight. A quicker, if approximate, approach is to investigate the effects of $r_{o}$ and $r_{\mu}$ separately and then combine them together. For the test circuit of Fig. 4.11a we ignore $r_{\mu}$ and recycle familiar results to write $i_{c 1}=v_{c} / R_{c 1}$, where

$$
\begin{equation*}
R_{c 1} \cong r_{o}\left[1+\frac{g_{m}\left(r_{n} / / R_{E}\right)}{1+R_{B} /\left(r_{\pi}+R_{E}\right)}\right] \tag{4.11}
\end{equation*}
$$

In the circuit of Fig. $4.11 b$ we ignore $r_{o}$ and apply KCL,

$$
i_{c 2}=\frac{v_{c}-v_{b}}{r_{\mu}}+\frac{g_{m}}{1+g_{m} R_{E}} v_{b}
$$

By the voltage divider formula,

$$
v_{b}=\frac{R_{B} / / R_{b}}{\left(R_{B} / / R_{b}\right)+r_{\mu}} v_{c} \cong \frac{R_{B} / / R_{b}}{r_{\mu}} v_{c}
$$

image_name:(a)
description:
[
name: RB, type: Resistor, value: RB, ports: {N1: Vb, N2: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vb, N2: Ve}
name: rμ, type: Resistor, value: rμ, ports: {N1: Vb, N2: Vc}
name: ro, type: Resistor, value: ro, ports: {N1: Vc, N2: Ve}
name: RE, type: Resistor, value: RE, ports: {N1: Ve, N2: GND}
name: gmvbe, type: VoltageControlledCurrentSource, value: gmvbe, ports: {Np: Vc, Nn: Ve}
name: vc, type: VoltageSource, value: vc, ports: {Np: Vc, Nn: GND}
]
extrainfo:The circuit is a test circuit to find contributions to Rc due to ro and rμ. It includes resistors, a capacitor, a voltage-controlled current source, and a voltage source. The circuit demonstrates the application of KCL and voltage divider principles.
image_name:(b)
description:
[
name: RB, type: Resistor, value: RB, ports: {N1: GND, N2: vb}
name: rπ, type: Resistor, value: rπ, ports: {N1: vb, N2: ve}
name: rμ, type: Resistor, value: rμ, ports: {N1: vb, N2: vc}
name: gmvbe, type: VoltageControlledCurrentSource, ports: {Np: vc, Nn: ve}
name: RE, type: Resistor, value: RE, ports: {N1: ve, N2: GND}
name: vc, type: VoltageSource, value: vc, ports: {Np: vc, Nn: GND}
name: ro, type: Resistor, value: ro, ports: {N1: vc, N2: ve}
]
extrainfo:The circuit is a test circuit used to find the contribution to Rc due to rμ. It includes resistors RB, rπ, rμ, and RE, a voltage-controlled current source gmvbe, and a voltage source vc. The circuit analyzes the current ic2 flowing through the circuit.

FIGURE 4.11 Test circuits to find the contributions to $R_{c}$ due to (a) $r_{o}$ and (b) $r_{\mu}$.
where we have used the fact that in circuits of practical interest $r_{\mu} \gg R_{B} / / R_{b}, R_{b}=$ $r_{\pi}+\left(\beta_{0}+1\right) R_{E}$. Clearly $v_{b}$ is much smaller than $v_{c}$, so we can simplify further, as

$$
i_{c 2}=\frac{v_{c}}{r_{\mu}}+\frac{g_{m}}{1+g_{m} R_{E}} \frac{R_{B} / / R_{b}}{r_{\mu}} v_{c} \cong \frac{1}{r_{\mu}}\left(1+\frac{R_{B} / / R_{b}}{R_{E}+1 / g_{m}}\right) v_{c}=\frac{v_{c}}{R_{c 2}}
$$

where

$$
\begin{equation*}
R_{c 2}=\frac{r_{\mu}}{1+\left(R_{B} / / R_{b}\right) /\left(R_{E}+1 / g_{m}\right)} \tag{4.12}
\end{equation*}
$$

With $r_{o}$ and $r_{\mu}$ present simultaneously, the overall current drawn from the $v_{c}$ source is $i_{c} \cong i_{c 1}+i_{c 2}=v_{c} / R_{c 1}+v_{c} / R_{c 2}$. Letting $R_{c}=v_{c} / i_{c}$, we find

$$
\begin{equation*}
R_{c} \cong R_{c 1} / / R_{c 2} \cong r_{o}\left[1+\frac{g_{m}\left(r_{\pi} / / R_{E}\right)}{1+R_{B} /\left(r_{\pi}+R_{E}\right)}\right] / /\left[\frac{r_{\mu}}{1+\left(R_{B} / / R_{b}\right) /\left(R_{E}+1 / g_{m}\right)}\right] \tag{4.13}
\end{equation*}
$$

We observe that the presence of $R_{B}$ reduces both $R_{c 1}$ and $R_{c 2}$. In applications where it is desired to maximize $R_{c}$, it would be best to keep $R_{B}$ as small as the design will allow.

EXAMPLE 4.3 Let the BJT of Fig. 4.9 have $\beta_{0}=100, r_{\pi}=2.6 \mathrm{k} \Omega, r_{o}=100 \mathrm{k} \Omega$, and $r_{\mu}=2 \beta_{0} r_{o}$. If $R_{B}=10 \mathrm{k} \Omega$ and $R_{E}=1.0 \mathrm{k} \Omega$, estimate $R_{c}$. What happens if $R_{B}=0$ ? Compare with PSpice.

#### Solution

We have $g_{m}=100 / 2600=1 /(26 \Omega)$ and $r_{\mu}=2 \times 100 \times 100=20 \mathrm{M} \Omega$. Equations (4.11) through (4.13) give

$$
\begin{aligned}
& R_{c 1} \cong 100\left(1+\frac{(2.6 / / 1) / 0.026}{1+10 /(2.6+1)}\right)=835 \mathrm{k} \Omega \\
& R_{c 2}=\frac{20}{1+(10 / / 103.6) /(1+0.026)} \cong 2 \mathrm{M} \Omega \\
& R_{c} \cong 835 / / 2,000=591 \mathrm{k} \Omega
\end{aligned}
$$

With $R_{B}=0$ we get $R_{c 1}=2.88 \mathrm{M} \Omega, R_{c 2}=r_{\mu}=20 \mathrm{M} \Omega$, and $R_{c}=2.88 / / 20,000=$ $2.52 \mathrm{M} \Omega$, in excellent agreement with PSpice, which gives $R_{c}=594 \mathrm{k} \Omega$ for $R_{B}=10 \mathrm{k} \Omega$, and $R_{c}=2.52 \mathrm{M} \Omega$ for $R_{B}=0$.

As mentioned, a monolithic transistor amplifier is likely to be biased and/or loaded by another transistor configured as a current source or sink, so it is instructive to reexamine the basic CE, CC, and CB configurations from the perspective of monolithic design. To focus on the distinguishing aspects of this type of design, we first investigate a circuit in the absence of loading and for the case of ideal current sources/ sinks (to keep things simple we also assume $r_{\mu}=\infty$ ). Then, we adapt our results to the case of non-ideal sources/sinks, in the presence of output loading, and with $r_{\mu} \neq \infty$.

### The CE Configuration with an Idealized Active Load

Recall that the common-emitter (CE) configuration (with or without emitter degeneration) is best suited to voltage amplification. The monolithic rendition of Fig. 4.12 uses the current source $I_{L O A D}$ as an active load, and the voltage source $V_{B I A S}$ to bias the BJT. We assume that $V_{B I A S}$ has been adjusted so as to bias the collector well within the linear region of operation. We readily find the input and output resistances by adapting Eqs. (4.9) and (4.13) in the limits $R_{B} \rightarrow 0, R_{C} \rightarrow \infty$, and $r_{\mu} \rightarrow \infty$. The results are

$$
\begin{equation*}
R_{i}=r_{\pi}+R_{E} \tag{4.14}
\end{equation*}
$$

$$
\begin{equation*}
R_{o}=r_{o}\left[1+g_{m}\left(r_{\pi} / / R_{E}\right)\right] \tag{4.15}
\end{equation*}
$$

Comparing to the case $R_{C} \rightarrow 0$, for which the familiar expression $R_{i}=r_{\pi}+$ $\left(\beta_{0}+1\right)\left(R_{E} / / r_{o}\right)$ holds, one may find Eq. (4.14) surprising. However, we readily justify it by turning to the ac equivalent of Fig. 4.13, where we observe that in the limit $R_{C} \rightarrow \infty$ the collector acts as an open circuit, at least on an ac basis. This means that the $g_{m} v_{\pi}$ current must circulate entirely in $r_{o}$, so these two elements act as a self-contained subcircuit. In this case the source $v_{i}$ sees just $r_{\pi}$ in series with $R_{E}$ ! Here is one significant difference between monolithic (high $R_{C}$ ) and discrete (low $R_{C}$ ) design!
image_name:FIGURE 4.12 Voltage amplifier with an ideal active load
description:
[
name: Q1, type: NPN, ports: {C: Vo, B: Vi, E: Ve}
name: RE, type: Resistor, value: RE, ports: {N1: Ve, N2: GND}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: VBias}
name: VBias, type: VoltageSource, value: VBias, ports: {Np: VBias, Nn: GND}
name: ILOAD, type: CurrentSource, value: ILOAD, ports: {Np: VCC, Nn: Vo}
]
extrainfo:The circuit is a voltage amplifier with an ideal active load. It uses an NPN transistor Q1 for amplification, with VCC as the supply voltage and ILOAD as the load current source. The input voltage Vi is superimposed on a bias voltage VBias, and the output is taken across Ro.

| CE-ED |
| :--- |
| $R_{i}=r_{\pi}+R_{E}$ |
| $a_{o c}=-g_{m} r_{o} \frac{1-R_{E} /\left(\beta_{o} r_{o}\right)}{1+R_{E} / r_{\pi}}$ |
| $R_{o}=r_{o}\left[1+g_{m}\left(r_{\pi} / / R_{E}\right)\right]$ |

| $\mathbf{C E}\left(\boldsymbol{R}_{E}=\mathbf{0}\right)$ |
| :--- |
| $R_{i}=r_{\pi}$ |
| $a_{o c}=a_{\text {intrinic }}=-g_{m} r_{o}$ |
| $R_{o}=r_{o}$ |

FIGURE 4.12 Voltage amplifier with an ideal active load, and its small-signal characteristics for $r_{\mu}=\infty$.
image_name:FIGURE 4.13
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vi, N2: Ve}
name: gmvπ, type: VoltageControlledCurrentSource, ports: {Np: Vo, Nn: Ve}
name: RE, type: Resistor, value: RE, ports: {N1: Ve, N2: GND}
name: ro, type: Resistor, value: ro, ports: {N1: Vo, N2: Ve}
name: RC, type: Resistor, value: RC, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a voltage amplifier with an ideal active load, showing small-signal characteristics. The input voltage is applied at Vi, and the output is taken from Vout. The circuit includes a voltage-controlled current source representing the transconductance gain.

FIGURE 4.13 Ac equivalent of the voltage amplifier of Fig. 4.12.

To find the voltage gain, consider again Fig. 4.13 in the limit $R_{C} \rightarrow \infty$. By KVL and Ohm's Law,

$$
v_{o}=v_{i}-v_{\pi}-r_{o} g_{m} v_{\pi}=v_{i}-\left(1+g_{m} r_{o}\right) v_{\pi}
$$

By the voltage divider formula,

$$
v_{\pi}=\frac{r_{\pi}}{r_{\pi}+R_{E}} v_{i}
$$

Substituting $v_{\pi}$, collecting, and solving for the ratio $v_{o} / v_{i}$ we get, after some algebra,

$$
\begin{equation*}
a_{o c}=\lim _{R_{c} \rightarrow \infty} \frac{v_{o}}{v_{i}}=-g_{m} r_{o} \frac{1-R_{E} /\left(\beta_{0} r_{o}\right)}{1+R_{E} / r_{\pi}} \tag{4.16a}
\end{equation*}
$$

where $a_{o c}$ is the open-circuit voltage gain, also called the unloaded voltage gain. A practical circuit has $R_{E} /\left(\beta_{0} r_{o}\right) \ll 1$, so this gain simplifies to

$$
\begin{equation*}
a_{o c} \cong \frac{-g_{m} r_{o}}{1+R_{E} / r_{\pi}} \tag{4.16b}
\end{equation*}
$$

The above expressions were derived in the presence of emitter degeneration, but we readily adapt them to the nondegenerated case by letting $R_{E}=0$. This gives $R_{i}=r_{\pi}, R_{o}=r_{o}$, and $a_{o c}=a_{\text {intrinsic }}$, where

$$
\begin{equation*}
a_{\text {intrinsic }}=-g_{m} r_{o}=-\frac{V_{A}}{V_{T}} \tag{4.17}
\end{equation*}
$$

is called the BJT's intrinsic gain. This is the maximum voltage gain achievable with a CE amplifier.

In actual application the amplifier is likely to drive some finite load resistance, and the $I_{\text {LOAD }}$ current source is likely to exhibit some finite parallel resistance. Moreover, $r_{\mu} \neq \infty$. Lumping all these resistances together and denoting the result as $R_{C}$, we find the loaded gain via the voltage divider formula,

$$
\begin{equation*}
\frac{v_{o}}{v_{i}} \cong-a_{o c} \times \frac{R_{C}}{R_{o}+R_{C}} \tag{4.18}
\end{equation*}
$$

Note that the presence of $R_{C}$ will also alter the input resistance $R_{i}$, as per Eq. (4.9).

#### EXercise 4.1

Show that for $R_{C} \ll r_{o}$, Eqs. (4.9) and (4.18) can be put in the more familiar forms of discrete design

$$
\begin{equation*}
R_{i} \cong r_{\pi}+\left(\beta_{0}+1\right) R_{E} \quad \frac{v_{o}}{v_{i}} \cong-\frac{R_{C}}{r_{e}+R_{E}} \tag{4.19}
\end{equation*}
$$

Let the BJT of Fig. 4.12 have $g_{m}=1 / 25 \mathrm{~A} / \mathrm{V}, r_{\pi}=4.0 \mathrm{k} \Omega$, and $r_{o}=50 \mathrm{k} \Omega$. EXAMPLE 4.4 Assuming $r_{\mu}=\infty$, find $R_{i}, R_{o}$, and $v_{o} / v_{i}$ if:
(a) $R_{E}=0$ and $R_{C}=\infty$.
(b) $R_{E}=1.0 \mathrm{k} \Omega$ and $R_{C}=\infty$.
(c) $R_{E}=1.0 \mathrm{k} \Omega$ and $R_{C}$ is adjusted so that $R_{C}=R_{o}$.
(d) $R_{E}=1.0 \mathrm{k} \Omega$ and $R_{C}=10 \mathrm{k} \Omega$. Comment on your results at each step.
(e) Repeat parts (a) and (b) assuming $r_{\mu}=5 \beta_{0} r_{o}$.

#### Solution

(a) With $R_{E}=0$ and $R_{C}=\infty$ the BJT amplifies by its intrinsic gain, and we have

$$
\begin{aligned}
& R_{i}=r_{\pi}=4.0 \mathrm{k} \Omega \\
& R_{o}=r_{o}=50 \mathrm{k} \Omega \\
& a_{\text {intrinsic }}=-g_{m} r_{o}=-50 / 0.025=-2000 \mathrm{~V} / \mathrm{V}
\end{aligned}
$$

(b) With emitter degeneration we expect an increase in $R_{i}$ and $R_{o}$ and a drop in $a$,

$$
\begin{aligned}
& R_{i}=r_{\pi}+R_{E}=4+1=5 \mathrm{k} \Omega \\
& R_{o}=r_{o}\left[1+g_{m}\left(r_{n} / R_{E}\right)\right]=50[1+(4 / / 1) / 0.025]=1.65 \mathrm{M} \Omega \\
& \frac{v_{o}}{v_{i}} \cong \frac{-g_{m} r_{o}}{1+R_{E} / r_{\pi}}=\frac{-2000}{1+1 / 4}=-1600 \mathrm{~V} / \mathrm{V}
\end{aligned}
$$

(c) We still have $R_{o}=1.65 \mathrm{M} \Omega$. However, loading the collector with $R_{C}=R_{o}=$ $1.65 \mathrm{M} \Omega$ will reduce gain to one-half the unloaded value, by Eq. (4.18). Thus

$$
\frac{v_{o}}{v_{i}}=-1600 \frac{1.65}{1.65+1.65}=-800 \mathrm{~V} / \mathrm{V}
$$

Moreover, $R_{i}$ will increase because of the coupling action by $r_{o}$. Using Eq. (4.9) with $\beta_{0}=g_{m} r_{\pi}=160$,

$$
R_{i}=4+161(1 / / 50) \times \frac{1+1650 /(161 \times 50)}{1+1650 /(1+50)}=9.7 \mathrm{k} \Omega
$$

(d) Using again Eqs (4.18) and (4.9), but with $R_{C}=10 \mathrm{k} \Omega$, we now get

$$
\frac{v_{o}}{v_{i}}=-9.63 \mathrm{~V} / \mathrm{V} \quad R_{i}=136 \mathrm{k} \Omega
$$

With $R_{C}$ this low, we could have used the familiar expressions of Eq. (4.19) to estimate

$$
\frac{v_{o}}{v_{i}} \cong-\frac{10}{0.025+1}=-9.76 \mathrm{~V} / \mathrm{V} \quad R_{i} \cong 4+161 \times 1=165 \mathrm{k} \Omega
$$

which are in fair agreement with the above. It is apparent that reducing $R_{C}$ lowers $a$ while raising $R_{i}$. The difference between monolithic and discrete design is evidenced further in Exercise 4.3, p. 357.
(e) We have $r_{\mu}=5 \times 160 \times 50=40 \mathrm{M} \Omega$. To assess the impact of $r_{\mu}$ we adapt Eq. (4.18). Thus, in (a) gain drops to $-2000 \times 40 /(0.05+40)=-1997 \mathrm{~V} / \mathrm{V}$ and in $(b)$ gain drops to $-1600 \times 40 /(1.65+40)=-1537 \mathrm{~V} / \mathrm{V}$. In both cases the change is fairly small, indicating that we can ignore $r_{\mu}$, at least in this example.

#### EXercise 4.2

Use Eq. (4.16a) to predict the gain of the circuit of Fig. 4.12 if (a) $R_{E}=\beta_{0} r_{o}$, and (b) $R_{E}=\infty$. Hence, justify your results via physical reasoning.

### The CC Configuration with an Idealized Active Load

Recall that the common-collector (CC) configuration is best suited to voltage buffering. The IC rendition of Fig. 4.14 admits the ac equivalent of Fig. 4.15, which we wish to investigate in the limit $R_{E} \rightarrow \infty$. In the absence of $r_{\mu}$ the resistance seen looking into the base would be $r_{\pi}+\left(\beta_{0}+1\right) r_{o} \cong \beta_{0} r_{o}$. This is large and comparable to $r_{\mu}$ ( $=m \beta_{0} r_{o}$ ), so taking the latter into account, we write, for $R_{E} \rightarrow \infty$,

$$
\begin{equation*}
R_{i} \cong\left(\beta_{0} r_{o}\right) / /\left(m \beta_{0} r_{o}\right)=\frac{m}{m+1} \beta_{0} r_{o} \tag{4.20}
\end{equation*}
$$

Moreover, adapting familiar expressions in the limit $R_{E} \rightarrow \infty$, we get

$$
\begin{equation*}
R_{o}=r_{e} / / r_{o} \cong r_{e} \tag{4.21}
\end{equation*}
$$

and

$$
\begin{equation*}
a_{o c}=\lim _{R_{k} \rightarrow \infty} \frac{v_{o}}{v_{i}}=\frac{1}{1+\frac{r_{\pi}}{\left(\beta_{0}+1\right) r_{o}}}=\frac{1}{1+r_{e} / r_{o}} \cong \frac{1}{1+1 /\left(g_{m} r_{o}\right)} \tag{4.22}
\end{equation*}
$$

image_name:FIGURE 4.14 Voltage follower with ideal current sink bias, and its small-signal characteristics.
description:
[
name: vi, type: VoltageSource, value: vi, ports: {Np: Vi, Nn: GND}
name: Q1, type: NPN, ports: {C: VCC, B: Vi, E: Vo}
name: IBIAS, type: CurrentSource, value: IBIAS, ports: {Np: Vo, Nn: VEE}
]
extrainfo:The circuit is a voltage follower with ideal current sink bias. It uses an NPN transistor (Q1) to buffer the input voltage (Vi) to the output (Vo). The current source (IBIAS) provides the biasing current for the transistor.

$$
\begin{aligned}
& R_{i} \cong \frac{m}{m+1} \beta_{o} r_{o} \\
& \hline a_{o c} \cong \frac{1}{1+1 /\left(g_{m} r_{o}\right)} \\
& R_{o} \cong r_{e}
\end{aligned}
$$

FIGURE 4.14 Voltage follower with ideal current sink bias, and its small-signal characteristics.
image_name:FIGURE 4.15
description:
[
name: vi, type: VoltageSource, value: vi, ports: {Np: Vi, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vi, N2: Vo}
name: rμ, type: Resistor, value: rμ, ports: {N1: Vi, N2: GND}
name: RE, type: Resistor, value: RE, ports: {N1: Vo, N2: GND}
name: ro, type: Resistor, value: ro, ports: {N1: Vo, N2: GND}
name: gmvπ, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: Vo}
]
extrainfo:The circuit is a voltage follower with ideal current sink bias, using an NPN transistor to buffer the input voltage Vi to the output Vo. The current source IBIAS provides the biasing current for the transistor.

FIGURE 4.15 Ac equivalent of the voltage follower of Fig. 4.14.
where $a_{o c}$ is the unloaded or open-circuit voltage gain. This gain, slightly less than unity, is the maximum gain achievable with the CC configuration, and it can also be expressed in the bias-independent form

$$
\begin{equation*}
a_{o c} \cong \frac{1}{1+V_{T} / V_{A}} \tag{4.23}
\end{equation*}
$$

In actual application the circuit is likely to drive some finite load, and the $I_{B I A S}$ current sink is likely to exhibit some finite parallel resistance. Lumping these resistances together and denoting the result as $R_{E}$, we observe that $R_{E}$ appears in parallel with $r_{o}$ in Fig. 4.15, so we recycle Eq. (4.22) but with $r_{o} / / R_{E}$ in place of $r_{o}$ to get the loaded gain

$$
\begin{equation*}
\frac{v_{o}}{v_{i}} \cong \frac{1}{1+1 /\left[g_{m}\left(r_{o} / / R_{E}\right)\right]} \tag{4.24}
\end{equation*}
$$

You can readily verify that the above expression can also be manipulated into a voltage-divider form as

$$
\begin{equation*}
v_{o} \cong \frac{\left(r_{o} / / R_{E}\right)}{\left(1 / g_{m}\right)+\left(r_{o} / / R_{E}\right)} v_{i} \tag{4.25}
\end{equation*}
$$

The reason for doing this is that we can visualize the voltage buffer according to Fig. 4.16. This insightful form will be used extensively as we move along.
image_name:Figure 4.16
description:
[
name: Q1, type: NPN, ports: {C: GND, B: vi, E: vo}
name: RE, type: Resistor, value: RE, ports: {N1: vo, N2: GND}
name: OpAmp1, type: OpAmp, value: 1 V/V, ports: {InP: vi, InN: GND, OutP: Vo1}
name: 1/gm, type: Resistor, value: 1/gm, ports: {N1: Vo1, N2: Vo}
name: ro, type: Resistor, value: ro, ports: {N1: Vo, N2: Vo}
name: RE, type: Resistor, value: RE, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit diagram represents a BJT voltage follower acting as a unity-gain buffer. The output resistance is modeled as 1/gm, forming a voltage divider with ro and RE.

FIGURE 4.16 A BJT voltage follower acts as a unity-gain buffer with output resistance $1 / g_{m}$, in turn forming a voltage divider with the rest of the resistances associated with the emitter $\left(r_{0} / / R_{E}\right.$ in the present case).
(Truth be told, the output resistance of the unity-gain stage should be $r_{e}$ instead of $1 / g_{m}$; but, since $r_{e}=\alpha_{0} / g_{m}$, where $\alpha_{0}=\beta_{0} /\left(\beta_{0}+1\right) \cong 1$, we let $1 / g_{m}$ stand, if nothing else because of the similarity with FETs to be investigated in the next section.)

EXAMPLE 4.5 Let the voltage follower of Fig. 4.14 have $g_{m}=1 /(10 \Omega), r_{\pi}=2.0 \mathrm{k} \Omega, r_{o}=25 \mathrm{k} \Omega$, and $m=5$.
(a) Find $R_{i}$ and $v_{o} / v_{i}$ if net resistance external to the emitter is $R_{E}=\infty$.
(b) Repeat, if the circuit drives a $3.0-\mathrm{k} \Omega$ load and the biasing sink has a $50-\mathrm{k} \Omega$ parallel resistance.
(c) Repeat part (b) if the $v_{i}$ source has a series resistance $R_{B}=30 \mathrm{k} \Omega$.

#### Solution

(a) The BJT has $\beta_{0}=g_{m} r_{\pi}=(1 / 10) 2000=200$. For $R_{E}=\infty$ we have, by Eqs. (4.20) and (4.22),

$$
\begin{aligned}
& R_{i} \cong \frac{5}{5+1} 200 \times 25 \cong 4.2 \mathrm{M} \Omega \\
& a_{o c}=\frac{1}{1+1 /(25 / 0.01)}=\frac{1}{1+1 / 2500}=0.9996 \mathrm{~V} / \mathrm{V}
\end{aligned}
$$

(b) We now have $R_{E}=50 / / 3=2.83 \mathrm{k} \Omega$ and $r_{o} / / R_{E}=25 / / 2.83=2.54 \mathrm{k} \Omega$. By inspection,

$$
\begin{aligned}
R_{i} & =r_{\mu} / /\left[r_{\pi}+\left(\beta_{0}+1\right)\left(r_{o} / / R_{E}\right)\right]=(5 \times 200 \times 25) / /(2+201 \times 2.54) \\
& =(25,000 / / 512)=502 \mathrm{k} \Omega
\end{aligned}
$$

indicating that $r_{\mu}$ now has a negligible effect and we could have ignored it. Finally, Eq. (4.24) gives

$$
\frac{v_{o}}{v_{i}}=\frac{1}{1+1 /(2.54 / 0.010)}=\frac{1}{1+1 / 254} \cong 0.996 \mathrm{~V} / \mathrm{V}
$$

(c) Here is an example where the viewpoint of Fig. 4.16 comes in handy. We can still apply the voltage-divider formula, but after reflecting $R_{B}$ to the emitter, where it will appear in series with the $1 / g_{m}$ resistance. The reflected value is $R_{B} /\left(\beta_{0}+1\right)=30 / 201=149 \Omega$, so Eq. (4.25) gives

$$
\frac{v_{o}}{v_{i}}=\frac{2.54}{0.149+0.010+2.54}=0.941 \mathrm{~V} / \mathrm{V}
$$

### The CB Configuration with an Idealized Active Load

Thanks to its high output resistance, the CB configuration finds application not only as a current buffer, but also as a voltage amplifier with high unloaded gain. Consider the monolithic rendition of Fig. 4.17, which uses the source $I_{L O A D}$ as an active load, and the source $V_{B I A S}$ to bias the BJT (as usual, we assume that $V_{B I A S}$ has been adjusted so as to bias the collector well within the linear region of operation). We wish to find the unloaded or open-circuit voltage gain $a_{o c}$ as well as $R_{i}$ and $R_{o}$. To this end, refer
image_name:FIGURE 4.17
description:
[
name: Q1, type: NPN, ports: {C: Vo, B: VBIAS, E: Vi}
name: ILOAD, type: CurrentSource, value: ILOAD, ports: {Np: VCC, Nn: Vo}
name: VBIAS, type: VoltageSource, value: VBIAS, ports: {Np: VBIAS, Nn: GND}
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
]
extrainfo:The circuit is a common-base (CB) configuration used as a high-gain voltage amplifier. The NPN transistor Q1 is biased using VBIAS. The circuit aims to achieve a high unloaded voltage gain with the given equations Ri = rπ, aoc = Vo/Vi = 1 + gmr_o, and Ro = r_o.

FIGURE 4.17 The CB configuration as a high-gain voltage amplifier, and its ac characteristics for $r_{\mu}=\infty$.
to the ac equivalent of Fig. 4.18 in the limit $R_{C} \rightarrow \infty$ (for the time being assume also $r_{\mu}=\infty$ ). Noting that $v_{\pi}=-v_{i}$, we relabel and reorient the dependent source to effect the circuit transformation shown. It is apparent that the $g_{m} v_{\pi}$ current circulates entirely in $r_{o}$, so we apply KVL and Ohm's law to write $v_{o}=v_{i}+r_{o} g_{m} v_{i}=\left(1+g_{m} r_{o}\right) v_{i}$. Taking the ratio $v_{o} / v_{i}$ we get

$$
\begin{equation*}
a_{o c}=\lim _{R_{c} \rightarrow \infty} \frac{v_{o}}{v_{i}}=1+g_{m} r_{o} \tag{4.26}
\end{equation*}
$$

It is interesting to observe that the product $g_{m} r_{o}$ appears in the expressions for $a_{o c}$ for each of the three basic BJT configurations, as per Eqs. (4.17), (4.22), and (4.26). As we know, $g_{m} r_{o}\left(=V_{A} / V_{T}\right)$ is a fairly large number that depends only on physical properties of the BJT, regardless of the biasing conditions. We can easily say that this number represents a figure of merit of a BJT in monolithic design.
image_name:FIGURE 4.18
description:
[
name: r_π, type: Resistor, value: r_π, ports: {N1: GND, N2: Vi}
name: r_μ, type: Resistor, value: r_μ, ports: {N1: Vo, N2: GND}
name: g_m v_π, type: VoltageControlledCurrentSource, value: g_m v_π, ports: {Np: Vo, Nn: Vi}
name: r_o, type: Resistor, value: r_o, ports: {N1: Vo, N2: Vi}
name: R_C, type: Resistor, value: R_C, ports: {N1: Vo, N2: GND}
name: v_i, type: VoltageSource, value: v_i, ports: {Np: Vi, Nn: GND}
]
extrainfo:The circuit is an AC equivalent of a CB voltage amplifier. It includes resistors, a voltage-controlled current source, and a voltage source. The configuration shows the transformation of input resistance in a common-base amplifier setup.

image_name:FIGURE 4.19
description:
[
name: RC, type: Resistor, value: RC, ports: {N1: C, N2: GND}
name: RE, type: Resistor, value: RE, ports: {N1: E, N2: GND}
name: Q1, type: NPN, ports: {C: C, B: GND, E: E}
]
extrainfo:The circuit is an AC equivalent of a common-base (CB) voltage amplifier, illustrating resistance transformation properties. The collector is open-circuited for AC signals, and the input resistance is defined by the equation \( R_{i} \approx \frac{r_{o} + R_{C}}{r_{o} + R_{C}(\beta_{0} + 1)} \). The output resistance is given by \( R_{o} \approx r_{o}[1 + g_{m}(r_{\pi}//R_{E})]//r_{\mu} \).
image_name:Equation Box
description:The image is a schematic diagram of a common-base (CB) voltage amplifier circuit, accompanied by a boxed set of equations that describe the resistance transformation properties of the circuit.

### Circuit Diagram:
- **Transistor (Q1):** The circuit features a bipolar junction transistor (BJT) with its collector (C), base, and emitter (e) labeled. The transistor is configured in a common-base setup.
- **Resistors:**
- **R_C:** Connected between the collector and the ground.
- **R_i:** Connected between the emitter and the ground.
- **R_E:** Shown in the emitter path.
- **R_o:** Connected from the collector to another node.
- **Ground Connections:** Various parts of the circuit are grounded, including the base and the bottom of R_E.

### Equations:
The boxed section on the right contains two equations:
1. **Input Resistance (R_i):**
\[ R_i \approx r_e \frac{r_o + R_C}{r_o + R_C(\beta_0 + 1)} \]
This equation describes the input resistance in terms of the small-signal parameters and the circuit resistances.

2. **Output Resistance (R_o):**
\[ R_o \approx r_o \left[ 1 + g_m \left( \frac{r_\pi}{R_E} \right) \right] \parallel r_\mu \]
This equation describes the output resistance, incorporating the transconductance (g_m), and other small-signal parameters.

### Contextual Information:
- The diagram and equations illustrate the resistance-transformation properties of the common-base configuration, highlighting how the input and output resistances are influenced by the circuit components and transistor parameters.

FIGURE 4.19 Illustrating the resistance-transformation properties of the CB configuration.
With the collector acting as an open ac circuit, the resistance seen by the input source is simply

$$
\begin{equation*}
R_{i}=r_{\pi} \tag{4.27}
\end{equation*}
$$

Comparing to the case $R_{C} \rightarrow 0$, for which the familiar expression $R_{i}=r_{e} / / r_{o} \cong r_{e}$ holds, one may find Eq. (4.27) surprising. Again, because of the ac open-circuited collector, the current supplied by the $v_{i}$ source flows entirely in $r_{\pi}$. This is another significant difference between monolithic (high $R_{C}$ ) and discrete (low $R_{C}$ ) design! Finally, to find the output resistance, we let $v_{i} \rightarrow 0$ and write, by inspection

$$
\begin{equation*}
R_{o}=r_{o} \tag{4.28}
\end{equation*}
$$

In actual application the amplifier is likely to drive some finite load resistance, and the $I_{L O A D}$ source is likely to exhibit some finite parallel resistance. Moreover, $r_{\mu} \neq \infty$. Lumping all these resistances together and denoting the result as $R_{C}$, we find the loaded gain via the voltage divider formula,

$$
\begin{equation*}
\frac{v_{o}}{v_{i}} \cong a_{o c} \times \frac{R_{C}}{r_{o}+R_{C}} \tag{4.29}
\end{equation*}
$$

The CB configuration is widely used in monolithic design both because of its potentially high unloaded voltage gain and because of its resistance-transformation abilities. (We will soon see an example in the cascode configuration.) Adapting Eqs. (4.10) and (4.13) with $R_{B}=0$, we readily find the expressions tabulated in Fig. 4.19, which you are urged to keep in mind as we shall refer to them often.

EXAMPLE 4.6 Let the BJT of Fig. 4.17 have $g_{m}=1 /(50 \Omega), \beta_{0}=150$, and $r_{o}=120 \mathrm{k} \Omega$.
(a) Assuming $r_{\mu}=\infty$, find $R_{i}, R_{o}$, and $v_{o} / v_{i}$ in the limit $R_{C} \rightarrow \infty$.
(b) Repeat, if the circuit drives an external load of $1 \mathrm{M} \Omega$.
(c) Investigate the effect of taking into account $r_{\mu}=m \beta_{0} r_{o}, m=5$.

#### Solution

(a) By Eqs. (4.26) through (4.28) we have

$$
R_{i}=150 \times 50=7.5 \mathrm{k} \Omega \quad R_{o}=120 \mathrm{k} \Omega \quad a_{o c}=1+\frac{120}{0.05}=2401 \mathrm{~V} / \mathrm{V}
$$

(b) $R_{o}$ remains the same. However, the input resistance and gain drop. Using the expression for $R_{i}$ tabulated in Fig. 4.19, along with Eq. (4.29), we find

$$
R_{i} \cong 50 \frac{0.12+1}{0.12+1 / 151} \cong 442 \Omega \quad \frac{v_{o}}{v_{i}}=2401 \frac{1}{0.12+1} \cong 2144 \mathrm{~V} / \mathrm{V}
$$

(c) We have $r_{\mu}=5 \times 150 \times 120=90 \mathrm{M} \Omega$, so the parameters of part (a) change to

$$
R_{i} \cong 50 \frac{0.12+90}{0.12+90 / 151} \cong 6.29 \mathrm{k} \Omega \quad \frac{v_{o}}{v_{i}}=2401 \frac{90}{0.12+90} \cong 2398 \mathrm{~V} / \mathrm{V}
$$

Similarly, we recalculate the parameters of part (b), but using (90//1) $\mathrm{M} \Omega$ instead of $1 \mathrm{M} \Omega$. The difference is on the order of $1 \%$, indicating that $r_{\mu}$ plays a negligible role in this example.

#### EXercise 4.3

The voltage gain $a=v_{c} / v_{e}$ of the CB configuration may lie anywhere over the range $g_{m} R_{C} \leq a \leq 1+g_{m} r_{o}$, depending on how $R_{C}$ compares with $r_{o}$. The lower extreme is reached in the limit $R_{C} \ll r_{o}$, typical of discrete designs, whereas the upper extreme is reached in the limit $R_{C} \gg r_{o}$, typical of monolithic designs. Let us arbitrarily define the discrete design range as the range $R_{C} \leq R_{C(\max )}$ over which $a$ departs from its lower extreme by no more than $10 \%$, and the monolithic design range as the range $R_{C} \geq R_{C(\min )}$ over which a departs from its upper extreme by no more than $10 \%$.
a. Estimate $R_{C(\max )}$ and $R_{C(\min )}$ for a BJT with $\beta_{0}=100$ and $V_{A}=100 \mathrm{~V}$ at $I_{C}=1 \mathrm{~mA}$.
b. What are the values of $R_{e}$ at the lower and upper extremes?
c. What are the values of $R_{e}$ at $R_{C}=R_{C(\max )}$ and at $R_{C}=R_{C(\min )}$ ?

Ans: (a) $R_{C(\max )} \cong 11 \mathrm{k} \Omega, R_{C(\min )} \cong 900 \mathrm{k} \Omega$. (b) $26 \Omega, 2.6 \mathrm{k} \Omega$. (c) $28.8 \Omega, 239 \Omega$

## 4.3 MOSFET CHARACTERISTICS AND MODELS REVISITED

The MOSFET models and analytical methodologies of Chapter 3 were deliberately kept as simple as possible so we could focus on the very basics. As we embark upon the study of monolithic circuits, we need to suitably refine models and techniques to include higher-order effects that tend to play a more prominent role in monolithic design.

### The Role of $\boldsymbol{\lambda}$ in Dc Calculations

Recall from Chapter 3 that the dc current of a saturated $n$ MOSFET is

$$
\begin{equation*}
I_{D}=\frac{1}{2} k^{\prime} \frac{W}{L} V_{O V}^{2}\left(1+\lambda V_{D S}\right) \tag{4.30}
\end{equation*}
$$

where $\lambda$ is the channel-length modulation parameter, a device parameter typically on the order of 0.01 to $0.1 \mathrm{~V}^{-1}$. As we know, this type of modulation stems from the portion of the drain-body SCL extending into the channel. Its width $\left(x_{p}\right.$ for the $n$ MOSFET, $x_{n}$ for the $p$ MOSFET) depends on doping levels as well as on junction bias, as per Eqs. (1.40) and (1.45). As we know, the shorter the channel the more pronounced the effect of channel-length modulation in Eq. (4.30). IC designers relate $\lambda$ to $L$ as

$$
\begin{equation*}
\lambda=\frac{\lambda^{\prime}}{L} \tag{4.31}
\end{equation*}
$$

where $\lambda^{\prime}$ (in $\mu \mathrm{m} / \mathrm{V}$ ) is a process parameter, and $L$ (in $\mu \mathrm{m}$ ) is the channel length. Typically, $\lambda^{\prime}$ ranges from 0.02 to $0.2 \mu \mathrm{~m} / \mathrm{V}$. An IC designer will specify $L$ to achieve a given $\lambda$, and $W$ to achieve a given $k, k=k^{\prime}(W / L)$. Note that this flexibility is not available in bipolar IC design!

As long as $\lambda V_{D S} \ll 1$ we ignore the term $\lambda V_{D S}$ in Eq. (4.30) to simplify dc calculations. However, in monolithic circuits this may no longer be acceptable. An example will give a better idea.

EXAMPLE 4.7 Let the diode-connected FET of Fig. 4.20 have $V_{t}=1.0 \mathrm{~V}, k^{\prime}=100 \mu \mathrm{~A} / \mathrm{V}^{2}$, and $\lambda^{\prime}=0.2 \mu \mathrm{~m} / \mathrm{V}$.
(a) Find $W$ and $L$ to achieve $\lambda=0.1 \mathrm{~V}^{-1}$ and $k=0.5 \mathrm{~mA} / \mathrm{V}^{2}$.
(b) If $I=1.0 \mathrm{~mA}$, find $V$ assuming $\lambda=0$ to simplify dc calculations.
(c) Refine your calculation of part (b), but with $\lambda=0.1 \mathrm{~V}^{-1}$.
(d) How would you adjust $I$ to retain the value of $V$ found in part (b)?
(e) How would you alter the $W / L$ ratio to retain the values of $I$ and $V$ of part (b) without changing $\lambda$ ?
image_name:FIGURE 4.20 Circuit of Example 4.7
description:
[
name: I, type: CurrentSource, value: I, ports: {Np: GND, Nn: V}
name: M1, type: NMOS, ports: {S: GND, D: V, G: V}
]
extrainfo:The circuit consists of a current source (I) and a voltage source (V) connected to an NMOS transistor (M1). The NMOS transistor's source is connected to ground, and both the drain and gate are connected to the same node (D).

FIGURE 4.20 Circuit of Example 4.7.

#### Solution

(a) We need $L=\lambda^{\prime} / \lambda=0.2 / 0.1=2 \mu m$, and $W / L=k / k^{\prime}=0.5 / 0.1=5$. So, $W=5 L=10 \mu \mathrm{~m}$.
(b) We have $V_{O V}=\sqrt{2 I_{D} / k}=\sqrt{2 \times 1 / 0.5}=2 \mathrm{~V}$, and $V=V_{t}+V_{O V}=1.0+$ $2.0=3.0 \mathrm{~V}$.
(c) We now have

$$
1 \mathrm{~mA}=\frac{0.5 \mathrm{~mA}}{2}(V-1.0)^{2} \times(1+0.1 \times V)
$$

Taking the square root of both sides and solving for the linear term in $V$ we get

$$
V=1.0+\frac{2}{\sqrt{1+0.1 \times V}}
$$

Starting out with the estimate $V=3.0 \mathrm{~V}$ and iterating, we find $V=2.77 \mathrm{~V}$ ( $<3.0 \mathrm{~V}$ because of $\lambda$ ).
(d) $I=(1 \mathrm{~mA}) \times(1+0.1 \times 3.0)=1.3 \mathrm{~mA}(>1 \mathrm{~mA}$ because of $\lambda)$.
(e) To lower $I$ from 1.3 mA to 1.0 mA while retaining $V=3.0 \mathrm{~V}$ we need to reduce the $W / L$ ratio in proportion. So, $(W / L)_{\text {new }}=(W / L)_{\text {old }} \times(1.0 / 1.3)=$ $5 \times 0.77=3.85$. To retain the same $\lambda$, keep $L_{\text {new }}=L_{\text {old }} \cdot S$, we need $W_{\text {new }}=$ $W_{\text {old }} \times 0.77=7.7 \mu \mathrm{~m}$.

### The Body Transconductance

In Chapter 3 we assumed MOSFETs with the body and source terminals tied together. This freed us from having to worry about the body effect so we could focus on the very basics of MOSFET behavior. In monolithic circuits different FETs share the same tub or body. The body common to all $n$ MOSFETs is tied to the most negative voltage (MNV) in the circuit in order to avoid the inadvertent turn-on of the diode formed by the $p$-type body and the $n$-type source. Likewise, the body common to all $p$ MOSFETs is tied to the most positive voltage (MPV). In the case of a saturated $n$ MOSFET whose source is allowed to attain a different potential than the body, the drain current takes on the more general form

$$
\begin{equation*}
i_{D}=\frac{k}{2}\left[v_{G S}-v_{t}\left(v_{S B}\right)\right]^{2}\left(1+\lambda v_{D S}\right) \tag{4.32}
\end{equation*}
$$

showing explicitly that the threshold voltage $v_{t}$ is a function of the source-to-body voltage $v_{S B}(\geq 0)$. This dependence takes on the form of Eq. (3.8), repeated here for convenience

$$
\begin{equation*}
v_{t}\left(v_{S B}\right)=V_{t 0}+\gamma\left[\sqrt{v_{S B}+2\left|\phi_{p}\right|}-\sqrt{2\left|\phi_{p}\right|}\right] \tag{4.33}
\end{equation*}
$$

where

$$
\begin{equation*}
\gamma=\frac{\sqrt{2 q N_{A} \varepsilon_{s i}}}{C_{o x}} \tag{4.34}
\end{equation*}
$$

For a $p$ MOSFET Eq. (4.33) takes on the form $v_{t}\left(v_{B S}\right)=V_{t 0}-\gamma\left[\sqrt{v_{B S}+2 \phi_{n}}-\sqrt{2 \phi_{n}}\right]$, where $\gamma$ is still found via Eq. (4.34), but with $N_{A}$ replaced by $N_{D}$. It is apparent that FETs operating with $v_{B}=v_{S}$ will also have $v_{t}=V_{t 0}$. However, FETs with $v_{S} \neq v_{B}$ will have $v_{t} \neq V_{t 0}$, a phenomenon referred to as the body effect. Since $v_{S B}$ (or $v_{S B}$ for a $p$ MOSFET) affects $i_{D}$, the body acts as a second gate, though with a lesser impact upon $i_{D}$ than the gate proper because of the presence of the square root function in Eq. (4.33). For this reason the body is also referred to as the back gate.
image_name:FIGURE 4.21 Small-signal MOSFET model
description:
[
name: M1, type: NMOS, ports: {S: S, D: D, G: G}
name: gmVgs, type: VoltageControlledCurrentSource, ports: {Np: D, Nn: -Vbs}
name: gmbVbs, type: VoltageControlledCurrentSource, ports: {Np: D, Nn: -Vbs}
name: ro, type: Resistor, value: ro, ports: {N1: D, N2: -Vbs}
]
extrainfo:The circuit diagram represents a small-signal model of a MOSFET with the body effect included. The dependent sources gmVgs and gmbVbs model the transconductance and body effect, respectively. The resistor ro represents the output resistance.

FIGURE 4.21 Small-signal MOSFET model with the source $g_{m b} v_{b s}$ stemming from the body effect.

Just like we use the dependent source $g_{m} \nu_{g s}$ to model the effect of a small-signal change in the gate voltage relative to that of the source, we use an additional dependent source $g_{m b} v_{b s}$ to model the effect of a small-signal change in the back-gate voltage relative to that of the source. This results in the small-signal model of Fig. 4.21, where $g_{m b}$, aptly called the body transconductance, is defined as

$$
\begin{equation*}
g_{m b}=\left.\frac{\partial i_{D}}{\partial v_{B S}}\right|_{V_{G S} V_{D S}} \tag{4.35}
\end{equation*}
$$

with $v_{G S}$ and $v_{D S}$ held constant. (Conversely, the ordinary transconductance is defined as $g_{m}=\partial i_{D} / \partial v_{G S}$ with $v_{B S}$ and $v_{D S}$ held constant.) Differentiation of Eq. (4.32) with respect to $v_{B S}\left(=-v_{S B}\right)$ gives

$$
\begin{aligned}
g_{m b} & =\frac{\partial i_{D}}{\partial\left(-v_{S B}\right)}=-\frac{\partial i_{D}}{\partial v_{S B}}=-k\left[v_{G S}-v_{t}\left(v_{S B}\right)\right]\left(1+\lambda v_{D S}\right)\left(-\frac{\partial v_{t}}{\partial v_{S B}}\right) \\
& =g_{m}\left(1+\lambda v_{D S}\right) \frac{\gamma}{2 \sqrt{v_{S B}+2\left|\phi_{p}\right|}}
\end{aligned}
$$

where we have used the fact that $k\left[v_{G S}-v_{t}\left(v_{S B}\right)\right]=g_{m}$. For $\lambda v_{D S} \ll 1$ we can write

$$
\begin{equation*}
g_{m b}=\chi g_{m} \tag{4.36}
\end{equation*}
$$

where

$$
\begin{equation*}
\chi=\frac{\gamma}{2 \sqrt{v_{S B}+2\left|\phi_{p}\right|}} \tag{4.37}
\end{equation*}
$$

The proportionality constant $\chi$ depends on process parameters as well as on $v_{S B}$ (or $v_{B S}$ for the $p$ MOSFET case), and is typically on the order of 0.1 to 0.3 . Note that since the MNV (or MPV for the $p$ MOSFET) is usually of the dc type, the body is shown at ac ground in Fig. 4.21.

Let the FET of Fig. 4.22 have $V_{t 0}=1.0 \mathrm{~V}, k=0.5 \mathrm{~mA} / \mathrm{V}^{2}, \lambda=1 /(40 \mathrm{~V}),\left|2 \phi_{p}\right|=$ 0.6 V , and $\gamma=0.445 \mathrm{~V}^{1 / 2}$. If $V_{D D}=9.0 \mathrm{~V}$, specify suitable resistances to bias the FET at $I_{D}=1 \mathrm{~mA}$ according to the $1 / 3-1 / 3-1 / 3$ Rule (to simplify dc calculations, assume $\lambda=0$ ). Hence, calculate the small-signal parameters.
image_name:Figure 4.22 Circuit of Example 4.8
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: Vb}
name: R2, type: Resistor, value: R2, ports: {N1: Vb, N2: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: x1}
name: RS, type: Resistor, value: RS, ports: {N1: x2, N2: GND}
name: M1, type: NMOS, ports: {S: x2, D: x1, G: Vb}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a common-source NMOS amplifier with resistive load. It uses a voltage divider biasing network formed by R1 and R2 to set the gate voltage of the NMOS transistor M1. RD is the drain resistor, and RS is the source resistor. VDD is the supply voltage.

FIGURE 4.22 Circuit of Example 4.8

#### Solution

We have $V_{S}=(1 / 3) 9=3 \mathrm{~V}$, so $R_{D}=R_{S}=3 / 1=3 \mathrm{k} \Omega$. Clearly, $V_{S B}=3 \mathrm{~V}$, so Eqs. (4.33) and (4.37) give

$$
V_{t}=1.0+0.445[\sqrt{3+0.6}-\sqrt{0.6}]=1.5 \mathrm{~V} \quad \chi=\frac{0.445}{2 \sqrt{3+0.6}}=0.117
$$

Also, $V_{O V}=\left(2 I_{D} / k\right)^{1 / 2}=(2 \times 1 / 0.5)^{1 / 2}=2 \mathrm{~V}$, so $V_{G}=V_{S}+V_{t}+V_{O V}=3+1.5+$ $2=6.5 \mathrm{~V}$. We need a resistance pair such that $R_{1} / R_{2}=2.5 / 6.5=1 / 2.6$. Use $R_{1}=$ $1.0 \mathrm{M} \Omega$ and $R_{2}=2.6 \mathrm{M} \Omega$. Finally, the FET's small-signal parameters are

$$
\begin{aligned}
g_{m} & =(2 \times 0.5 \times 1)^{1 / 2}=1.0 \mathrm{~mA} / \mathrm{V} \\
g_{m b} & =0.117 \times 1=0.117 \mathrm{~mA} / \mathrm{V} \\
r_{o} & =40 / 1=40 \mathrm{k} \Omega
\end{aligned}
$$

### A Generalized Ac Circuit

We now wish to investigate how the presence of the $g_{m b} v_{b s}$ source affects the various parameters in the generalized ac circuit of Fig. 4.23. We anticipate that except for the CS configuration, for which $v_{b s}=0$, all other configurations will be sensitive to the body effect.

- The Transconductance $\boldsymbol{G}_{\boldsymbol{m}}=\boldsymbol{i}_{d} / \boldsymbol{v}_{g}$. With reference to the small-signal equivalent of Fig. $4.24 a$ we observe that $v_{b s}=-v_{s}$, so we can reverse the direction of the $g_{m b} v_{b s}$ source and relabel it as $g_{m b} v_{s}$. This is depicted in Fig. 4.24b. Applying KCL at the drain node we get

$$
i_{d}+g_{m b} v_{s}=g_{m}\left(v_{g}-v_{s}\right)+\frac{v_{d}-v_{s}}{r_{o}}
$$

image_name:Figure 4.23
description:
[
name: M1, type: NMOS, ports: {V: Vs, D: vd, G: Vg}
name: RD, type: Resistor, value: RD, ports: {N1: vd, N2: GND}
name: RS, type: Resistor, value: RS, ports: {N1: vs, N2: GND}
name: Vg, type: VoltageSource, value: Vg, ports: {Np: Vg, Nn: GND}
]
extrainfo:The circuit is a common-source amplifier using an NMOS transistor with source degeneration. The amplifier has a gain defined by the transconductance Gm = id/vg. The resistors RD and RS are used for drain and source resistances, respectively. The input voltage vg is applied through the gate resistor Rg.
image_name:Summary of small-signal gains and terminal resistances for a MOSFET
description:The image consists of two main components: a schematic diagram of a MOSFET circuit and a table summarizing small-signal gains and terminal resistances.

**Schematic Diagram:**
- The circuit features a MOSFET with its gate, source, and drain terminals labeled.
- The gate terminal is connected to a voltage source labeled \( V_g \), which is in series with a resistor \( R_g \).
- The source terminal is connected to ground through a resistor \( R_s \).
- The drain terminal is connected to a load resistor \( R_D \) and also to ground.
- The input signal \( v_g \) is applied at the gate, and the output voltage \( v_d \) is observed at the drain.
- Current \( i_d \) flows from the drain through \( R_D \) to ground.

**Table of Small-Signal Gains and Terminal Resistances:**
- **Transconductance \( G_m \):**
\[ G_m = \frac{i_d}{v_g} = \frac{g_m}{1 + (g_m + g_{mb})R_s + (R_D + R_s)/r_o} \]
- **Voltage Gain \( \frac{v_d}{v_g} \):**
\[ \frac{v_d}{v_g} = \frac{-g_m R_D}{1 + (g_m + g_{mb})R_s + (R_D + R_s)/r_o} \]
- **Source Voltage Gain \( \frac{v_s}{v_g} \):**
\[ \frac{v_s}{v_g} = \frac{g_m R_s}{1 + (g_m + g_{mb})R_s + (R_D + R_s)/r_o} \]
- **Gate Resistance \( R_g \):**
\[ R_g = \infty \]
- **Source Resistance \( R_s \):**
\[ R_s = \left( \frac{1}{g_m + g_{mb}} \parallel \frac{1}{r_o} \right) + \frac{R_D}{1 + (g_m + g_{mb})r_o} \]
- **Drain Resistance \( R_d \):**
\[ R_d = r_o + \left[ 1 + (g_m + g_{mb})r_o \right] R_s \]

This image provides a comprehensive summary of the small-signal model parameters for a MOSFET, illustrating how the various resistances and gains are calculated based on the device characteristics and external components.

FIGURE 4.23 Summary of small-signal gains and terminal resistances for a MOSFET.

Since $i_{d}$ enters the drain and exits the source, we have, by Ohm's law, $v_{s}=R_{S} i_{d}$ and $v_{d}=-R_{D} i_{d}$. Substituting in the above expression and collecting we get the circuit's transconductance

$$
\begin{equation*}
G_{m}=\frac{i_{d}}{v_{g}}=\frac{g_{m}}{1+\left(g_{m}+g_{m b}\right) R_{S}+\left(R_{D}+R_{S}\right) / r_{o}} \tag{4.38}
\end{equation*}
$$

This is similar to the expression tabulated in Fig. 3.50, except for the denominator term increase from $g_{m} R_{S}$ to $\left(g_{m}+g_{m b}\right) R_{S}$. By Eq. (4.36) this represents a percentage increase of $100 \chi$.
image_name:(a)
description:
[
name: Vg, type: VoltageSource, value: Vg, ports: {Np: Vg, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: vs, N2: GND}
name: RD, type: Resistor, value: RD, ports: {N1: x1, N2: GND}
name: ro, type: Resistor, value: ro, ports: {N1: x1, N2: vs}
name: gmVgs, type: VoltageControlledCurrentSource, ports: {Np: x1, Nn: vs}
name: gmbVbs, type: VoltageControlledCurrentSource, ports: {Np: x1, Nn: vs}
]
extrainfo:The circuit is a small-signal equivalent model with voltage and current sources representing transconductance and body effect. It includes resistors RS and RD connected to ground, a resistor ro between nodes vd and vs, and two voltage-controlled current sources representing gm and gmb effects.
image_name:(b)
description:
[
name: Vg, type: VoltageSource, value: Vg, ports: {Np: Vg, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: vs, N2: GND}
name: RD, type: Resistor, value: RD, ports: {N1: vd, N2: GND}
name: gmvgs, type: VoltageControlledCurrentSource, value: gmvgs, ports: {Np: vs, Nn: vd}
name: gmbvbs, type: VoltageControlledCurrentSource, value: gmbvbs, ports: {Np: vs, Nn: vd}
name: ro, type: Resistor, value: ro, ports: {N1: vd, N2: Vs}
]
extrainfo:The circuit diagram (b) represents a small-signal equivalent circuit with a voltage source Vg, resistors RS and RD, and controlled current sources gmvgs and gmbvbs. The circuit is grounded at multiple points and includes nodes for vs and vd.

FIGURE 4.24 (a) Small-signal equivalent of the generalized ac circuit of Fig. 4.22. (b) The circuit of (a) after suitable transformation.

- The Voltage Gains $\boldsymbol{v}_{s} / \boldsymbol{v}_{g}$ and $\boldsymbol{v}_{d} / \boldsymbol{v}_{g}$. We also have $v_{s}=R_{S} i_{d}=R_{s} G_{m} v_{g}$ and $v_{d}=$ $-R_{D} i_{d}=-R_{D} G_{m} v_{g}$, so the small-signal voltage gains from $v_{g}$ to $v_{s}$ and from $v_{g}$ to $v_{d}$ are, respectively

$$
\begin{align*}
& \frac{v_{d}}{v_{g}}=\frac{-g_{m} R_{D}}{1+\left(g_{m}+g_{m b}\right) R_{S}+\left(R_{D}+R_{S}\right) / r_{o}}  \tag{4.39a}\\
& \frac{v_{s}}{v_{g}}=\frac{g_{m} R_{S}}{1+\left(g_{m}+g_{m b}\right) R_{S}+\left(R_{D}+R_{S}\right) / r_{o}} \tag{4.39b}
\end{align*}
$$

Note again the denominator term increase from $g_{m} R_{S}$ to $\left(g_{m}+g_{m b}\right) R_{S}$.

- The Resistance $\boldsymbol{R}_{s}$ Seen Looking into the Source. To find this resistance we let $v_{g} \rightarrow 0$ and we subject the source terminal to a test voltage $v_{s}$. But, with $v_{g}=0$ we get $v_{g s}=v_{g}-v_{s}=0-v_{s}=-v_{s}$, so now we can reverse and relabel also the $g_{m} v_{g s}$ source, as in Fig. 4.25a. By KCL we have

$$
i_{s}=g_{m} v_{s}+g_{m b} v_{s}+\frac{v_{s}-v_{d}}{r_{o}}=\left(g_{m}+g_{m b}\right) v_{s}+\frac{v_{s}-R_{D} i_{s}}{r_{o}}
$$

Collecting and taking the ratio $R_{s}=v_{s} / i_{s}$ gives, after some algebra,

$$
\begin{equation*}
R_{s}=\left(\frac{1}{g_{m}+g_{m b}} / / r_{o}\right)+\frac{R_{D}}{1+\left(g_{m}+g_{m b}\right) r_{o}} \tag{4.40a}
\end{equation*}
$$

Typically $1 /\left(g_{m}+g_{m b}\right) \ll r_{o}$, so the above expression simplifies to

$$
\begin{equation*}
R_{s} \cong \frac{1}{g_{m}+g_{m b}}+\frac{R_{D}}{1+\left(g_{m}+g_{m b}\right) r_{o}} \tag{4.40b}
\end{equation*}
$$

The first term is similar to that of discrete designs, except for the change from $g_{m}$ to $g_{m}+g_{m b}$. The second term represents the effect of the external drain resistance $R_{D}$ reflected to the source. This term is usually ignored in discrete designs, but not necessarily in monolithic designs, where the drain may be terminated on a current source and therefore $R_{D}$ may be quite large.
image_name:(a)
description:
[
name: g_m v_s, type: VoltageControlledCurrentSource, value: g_m v_s, ports: {Np: v_s, Nn: v_d}
name: g_{mb
mb
Np: v_s, Nn: v_s
name: R_D, type: Resistor, value: R_D, ports: {N1: v_d, N2: GND}
name: r_o, type: Resistor, value: r_o, ports: {N1: v_d, N2: v_s}
name: v_s, type: VoltageSource, value: v_s, ports: {Np: v_s, Nn: GND}
]
extrainfo:The circuit is used to analyze the small-signal resistance seen looking into the source. It includes a voltage-controlled current source representing transconductance and body effect, a resistor for drain resistance, and another for output resistance.
image_name:(b)
description:
[
name: gmvs, type: VoltageControlledCurrentSource, value: gmvs, ports: {Np: vs, Nn: vd}
name: gmbvs, type: VoltageControlledCurrentSource, value: gmbvs, ports: {Np: vs, Nn: vd}
name: ro, type: Resistor, value: ro, ports: {N1: vd, N2: vs}
name: RS, type: Resistor, value: RS, ports: {N1: vs, N2: GND}
name: vd, type: VoltageSource, value: vd, ports: {Np: vd, Nn: GND}
]
extrainfo:The circuit is a test setup to measure the small-signal resistance seen looking into the drain (Rd). It includes voltage-controlled current sources representing transconductance and body effect, and a resistor representing the output resistance of the transistor. The input voltage source vd is applied to the drain.

FIGURE 4.25 Test circuits to find (a) the small-signal resistance $R_{s}$ seen looking into the source and (b) the small-signal resistance $R_{d}$ seen looking into the drain.

- The Resistance $\boldsymbol{R}_{d}$ Seen Looking into the Drain. To find this resistance we let $v_{g} \rightarrow 0$ and we subject the drain to a test voltage $v_{d}$. But, with $v_{g}=0$ we again get $v_{g s}=-v_{s}$, so we again reverse and relabel both dependent sources as in Fig. 4.25b. By KCL,

$$
i_{d}+g_{m} v_{s}+g_{m b} v_{s}=\frac{v_{d}-v_{s}}{r_{o}}
$$

Substituting $v_{s}=R_{S} i_{d}$, collecting, and taking the ratio $R_{d}=v_{d} / i_{d}$, we get

$$
\begin{equation*}
R_{d}=r_{o}+\left[1+\left(g_{m}+g_{m b}\right) r_{o}\right] R_{S} \tag{4.41}
\end{equation*}
$$

The first component is just the FET's internal resistance $r_{o}$, while the second component represents the effect of the external source resistance $R_{S}$ reflected to the drain. It is interesting to contrast the effects of the MOSFET upon its external resistances: while $R_{D}$ reflected to the source gets divided by the amount $1+\left(g_{m}+\right.$ $\left.g_{m b}\right) r_{o}, R_{S}$ reflected to the drain gets multiplied by the same amount. We shall have more to say about these symmetric actions when studying cascode configurations.

As mentioned, a monolithic MOSFET amplifier is likely to be biased or to be loaded by another FET operating as a current source or sink, so it is instructive to reexamine the basic FET configurations from the IC design viewpoint. We first investigate the limiting case of ideal current sources/sinks, then we adapt our results to the case of non-ideal sources/sinks, and in the presence of an output load.

### The CS Configuration with an Idealized Active Load

Recall that the common-source (CS) configuration (with or without source degeneration) is best suited to voltage amplification. The monolithic rendition of Fig. 4.26 uses the current source $I_{L O A D}$ as an active load, and the voltage source $V_{B A A S}$ to bias the FET. We assume that $V_{B A S}$ has been adjusted so as to ensure that the drain is biased at a voltage well within the linear region of operation. The amplifier's characteristics are readily obtained by adapting the expressions of Fig. 4.23 in the limit $R_{D} \rightarrow \infty$. The results are tabulated in Fig. 4.26 both for the CS-SD case $\left(R_{S} \neq 0\right)$, and the plain CS case $\left(R_{S}=0\right)$.
image_name:Voltage amplifier with a current-source load
description:
[
name: M1, type: NMOS, ports: {S: Vs, D: Vo, G: Vbias+Vi}
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: Vs}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vbias+Vi, Nn: Vbias}
name: VBias, type: VoltageSource, value: VBias, ports: {Np: Vbias, Nn: GND}
name: ILoad, type: CurrentSource, value: ILoad, ports: {Np: VDD, Nn: Vo}
]
extrainfo:The circuit is a voltage amplifier with a current-source load. It uses an NMOS transistor (M1) with a bias voltage (Vbias) and input voltage (Vi) to control the gate. The output is taken across the resistor R0. The amplifier is characterized by its intrinsic gain and output resistance, as indicated in the accompanying table.
image_name:summary of its small-signal characteristics
description:The image consists of two main sections: a circuit diagram on the left and a table summarizing small-signal characteristics on the right.

**Circuit Diagram:**
- The circuit features a field-effect transistor (FET) labeled as M1.
- The source of M1 is connected to ground through a resistor labeled \( R_S \).
- The gate of M1 is connected to a voltage source \( V_{\text{BIAS}} + v_i \), where \( v_i \) is the input signal.
- The drain of M1 is connected to a current source \( I_{\text{LOAD}} \) and a voltage source \( V_{DD} \). The output voltage \( v_o \) is measured across a load \( R_O \) connected to the drain.

**Table of Small-Signal Characteristics:**
- The table is divided into two columns representing different configurations: CS-SD (Common Source with Source Degeneration) and CS (Common Source with \( R_S = 0 \)).

**CS-SD Configuration:**
- \( R_i = \infty \)
- \( a_{\text{intrinsic}} = -g_m r_o \)
- \( R_o = r_o + \left[ 1 + (g_m + g_{mb})r_o \right] R_S \)

**CS (\( R_S = 0 \)) Configuration:**
- \( R_i = \infty \)
- \( a_{\text{intrinsic}} = -g_m r_o \)
- \( R_o = r_o \)

This image illustrates the configuration and characteristics of a voltage amplifier with a current-source load, highlighting how the presence or absence of source degeneration (\( R_S \)) affects the output resistance \( R_o \).

FIGURE 4.26 Voltage amplifier with a current-source load and summary of its small-signal characteristics.

The voltage gain achieved in the limit $R_{D} \rightarrow \infty$ is $v_{o} / v_{i}=-g_{m} r_{o}$. Aptly called the unloaded or also the open-circuit voltage gain, this is the maximum voltage gain attainable with the CS configuration and for this reason it is also called the intrinsic gain $a_{\text {intrinsic }}$. It is interesting that this gain is unaffected by the presence of $R_{S}$. This is so because with an ideal current-source load the drain is an ac open circuit giving $i_{d}=0 . \mathrm{So}, i_{s}=0$ and $v_{s}=R_{S} i_{s}=0$, indicating that neither $R_{S}$ nor $g_{m b}$ intervene in the expression for the gain in this case. (However, they do intervene in the expression for $R_{o}$ in the CS-SD case.)

In actual application a CS amplifier is likely to drive some finite load resistance, and the $I_{L O A D}$ source is likely to exhibit some finite parallel resistance. Lumping these resistances together and denoting their combination as $R_{D}$, we adapt Eq. (4.39) to find the loaded gain as

$$
\begin{equation*}
\frac{v_{o}}{v_{i}}=\frac{-g_{m} R_{D}}{1+\left(g_{m}+g_{m b}\right) R_{S}+\left(R_{D}+R_{S}\right) / r_{o}} \tag{4.42}
\end{equation*}
$$

Suppose the FET of Fig. 4.26 has $g_{m}=1 \mathrm{~mA} / \mathrm{V}^{2}, r_{o}=50 \mathrm{k} \Omega$, and $\chi=0.15$. Find $R_{o}$ and $v_{o} / v_{i} \mathrm{if:}$
(a) $R_{S}=0$ and $R_{D}=\infty$.
(b) $R_{S}=0$ and $R_{D}=100 \mathrm{k} \Omega$.
(c) $R_{S}=2.0 \mathrm{k} \Omega$ and $R_{D}=\infty$.
(d) $R_{S}=2.0 \mathrm{k} \Omega$ and $R_{D}=100 \mathrm{k} \Omega$. Comment on your results at each step.

#### Solution

(a) With $R_{S}=0$ and $R_{D}=\infty$ the FET amplifies by its intrinsic gain and we have

$$
R_{o}=r_{o}=50 \mathrm{k} \Omega \quad a_{\text {intrinsic }}=-g_{m} r_{o}=-1 \times 50=-50 \mathrm{~V} / \mathrm{V}
$$

(b) With $R_{S}=0$ we still have $R_{o}=50 \mathrm{k} \Omega$. With $R_{D}=100 \mathrm{k} \Omega$, the loaded gain is, by Eq. (4.42),

$$
\frac{v_{o}}{v_{i}}=\frac{-1 \times 100}{1+100 / 50}=-33.3 \mathrm{~V} / \mathrm{V}
$$

(c) With source degeneration we expect $R_{o}$ to increase. However, so long as $R_{D}=\infty$, gain is unaffected by $R_{S}$.

$$
\begin{aligned}
& R_{o}=r_{o}+\left[1+\left(g_{m}+g_{m b}\right) r_{o}\right] R_{S}=50+[1+(1+0.15 \times 1) 50] 2=167 \mathrm{k} \Omega \\
& \frac{v_{o}}{v_{i}}=-50 \mathrm{~V} / \mathrm{V}
\end{aligned}
$$

(d) The resistance seen by $R_{D}$ is still $167 \mathrm{k} \Omega$. However, by Eq. (4.42), gain drops to

$$
\frac{v_{o}}{v_{i}}=\frac{-1 \times 100}{1+1 \times 1.15 \times 2+(100+2) / 50}=18.7 \mathrm{~V} / \mathrm{V}
$$

Combining familiar expressions for $g_{m}$ and $r_{o}$ we can put the intrinsic gain in the alternative form

$$
\begin{equation*}
a_{\text {intrinsic }}=-\frac{1}{\lambda} \sqrt{\frac{2 k}{I_{D}}} \tag{4.43}
\end{equation*}
$$

Unlike the BJT's intrinsic gain of Eq. (4.17), which is bias-independent, that of the FET is inversely proportional to $\sqrt{I_{D}}$, indicating that lowering $I_{D}$ increases $a_{\text {intrinsic }}$. This is certainly desirable in low-power IC design. However, two observations are in order. First, Eq. (4.43) is a result of the quadratic characteristic of the MOSFET. At sufficiently low operating currents the FET enters the sub-threshold region where its characteristic changes from quadratic to exponential. Consequently, at low currents the intrinsic gain of the MOSFET becomes bias-independent, just like in the case of the BJT. Second, low operating currents reduce a circuit's ability to drive capacitive loads, resulting in slower operation and thus reduced frequency bandwidth (more on this in Chapter 6).

#### EXAMPLE 4.10

(a) If a MOSFET gives $a_{\text {intrinsic }}=-50 \mathrm{~V} / \mathrm{V}$ at $I_{D}=1 \mathrm{~mA}$, find $a_{\text {intrinsic }}$ at $I_{D}=$ $100 \mu \mathrm{~A}$. What value of $I_{D}$ is needed for $a_{\text {intrinsic }}=-100 \mathrm{~V} / \mathrm{V}$ ?
(b) If it is found that this FET enters the sub-threshold region in the vicinity of $I_{D}=10 \mu \mathrm{~A}$, estimate its maximum intrinsic gain.

#### Solution

(a) Lowering $I_{D}$ by a factor of 10 will change $a_{\text {intrinsic }}$ from $-50 \mathrm{~V} / \mathrm{V}$ to $-50 \sqrt{10}=$ $-158 \mathrm{~V} / \mathrm{V}$. In order to double $a_{\text {intrinsic }}$ from $-50 \mathrm{~V} / \mathrm{V}$ to $-100 \mathrm{~V} / \mathrm{V}$ we must lower $I_{D}$ by a factor of four, so $I_{D}=1 / 4=250 \mu \mathrm{~A}$.
(b) For $I_{D} \leq 10 \mu \mathrm{~A}$ gain will settle at $a_{\text {intrinsic(max) }}=-50 \sqrt{1000 / 10}=-500 \mathrm{~V} / \mathrm{V}$.

Writing $g_{m} r_{o}=\left(2 I_{D} / V_{O V}\right) /\left(\lambda I_{D}\right)=2 /\left(\lambda V_{O V}\right)$ we get yet another insightful form for the intrinsic gain

$$
\begin{equation*}
a_{\text {intrinsic }}=-\frac{2 L}{\lambda^{\prime} V_{O V}} \tag{4.44}
\end{equation*}
$$

where $V_{O V}$ is the overdrive voltage, $L$ the channel length, and $\lambda^{\prime}$ is the process parameter characterizing channel-length modulation, as per Eq. (4.31). This form indicates that the longer the channel for a given $V_{O V}$, the higher the intrinsic gain. This flexibility is quite convenient for the MOS IC designer!

EXAMPLE 4.11 Assuming a process with $k^{\prime}=75 \mu \mathrm{~A} / \mathrm{V}^{2}$ and $\lambda^{\prime}=0.1 \mu \mathrm{~m} / \mathrm{V}$, specify $W$ and $L$ so that at $I_{D}=100 \mu \mathrm{~A}$ and $V_{D S}=2 \mathrm{~V}$ a MOSFET provides $a_{\text {intrinsic }}=-50 \mathrm{~V} / \mathrm{V}$ with $V_{O V}=0.5 \mathrm{~V}$.

#### Solution

By Eqs. (4.44) and (4.31) we have

$$
\begin{aligned}
& L=-\lambda^{\prime} \times V_{O V} \times a_{\text {intrinsic }} / 2=-0.1 \times 0.5 \times(-50) / 2=2.5 \mu \mathrm{~m} \\
& 100=\frac{1}{2} 75 \frac{\mathrm{~W}}{2.5} 0.5^{2}\left(1+\frac{0.1}{2.5} \times 2\right) .
\end{aligned}
$$

Solving we get $W=24.7 \mu \mathrm{~m}$.

### The CD Configuration with an Idealized Active Load

Recall that the common-drain (CD) configuration is best suited to voltage buffering. In monolithic realizations a FET buffer is usually biased via a current sink, so let us investigate the voltage transfer curve (VTC) of such a realization. Figure 4.27 shows a PSpice circuit to serve this purpose, along with its voltage transfer curve (VTC). The latter is shown both for the already familiar case of body and source tied together $(\gamma=0)$, and the henceforth more common case of the body tied to the most negative voltage (MNV) in the circuit, so that $(\gamma \neq 0)$. We observe that both curves are shifted downward by $v_{G S}$, namely, $v_{O}=v_{I}-v_{G S}=v_{I}-\left(V_{t}+V_{O V}\right)$. In the case $\gamma=0$ we have $V_{t}=V_{t 0}=$ constant, but in the case $\gamma \neq 0$, the body effect makes $V_{t}$ itself a function of $v_{O}$ and, hence, of $v_{I}$. We also note that the $p n$ junction formed by the body and source clamps $v_{O}$ a diode drop below $V_{S S}$ (or at about -5.6 V in the present example). Also, $v_{O}$ saturates at $V_{D D}\left(=5 \mathrm{~V}\right.$ in the present example) for $v_{I}$ high enough to drive the FET into the ohmic region.

We now wish to find the unloaded voltage gain and output resistance, as depicted in Fig. 4.28. We do this by adapting the expressions tabulated in Fig. 4.23 in the
image_name:(a)
description:
[
name: M, type: NMOS, ports: {S: Vo, D: VDD, G: I}
name: V_I, type: VoltageSource, value: V_I, ports: {Np: I, Nn: GND}
name: I_BIAS, type: CurrentSource, value: 250 µA, ports: {Np: O, Nn: VSS}
]
extrainfo:The circuit is a monolithic MOS buffer with a voltage transfer characteristic (VTC) shown in the graph. It uses an NMOS transistor with a bias current source and a voltage input source. The output voltage saturates at VDD for high input voltages.
image_name:(b)
description:The graph in Figure 4.27(b) is a Voltage Transfer Characteristic (VTC) plot, illustrating the relationship between the input voltage \( v_I \) and the output voltage \( v_O \) for a MOS buffer circuit.

1. **Type of Graph and Function:**
- This is a Voltage Transfer Characteristic (VTC) graph, which is a type of plot used to depict the input-output relationship of a circuit.

2. **Axes Labels and Units:**
- The horizontal axis represents the input voltage \( v_I \) in volts (V), ranging from -7 V to 7 V.
- The vertical axis represents the output voltage \( v_O \) in volts (V), also ranging from -7 V to 7 V.
- Both axes are linearly scaled.

3. **Overall Behavior and Trends:**
- The graph shows two curves corresponding to different values of the body effect parameter \( \gamma \): \( \gamma = 0 \) and \( \gamma = 0.75 \, \text{V}^{1/2} \).
- For \( \gamma = 0 \), the curve is above the one for \( \gamma = 0.75 \, \text{V}^{1/2} \), indicating that the body effect influences the output voltage.
- Both curves show an approximately linear region where the slope is positive, indicating a proportional increase in \( v_O \) with \( v_I \).
- There are saturation regions at both ends where the output voltage levels off, indicating the limits of the buffer’s output capability.

4. **Key Features and Technical Details:**
- The curves start saturating at the extreme values of \( v_I \). For \( v_I \) around -7 V, \( v_O \) approaches -7 V, and for \( v_I \) around 7 V, \( v_O \) approaches 5 V.
- The linear region is more pronounced in the middle range of \( v_I \), where the MOSFET operates in the active region.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for \( \gamma = 0 \) and \( \gamma = 0.75 \, \text{V}^{1/2} \), showing the impact of the body effect on the VTC.
- There are no specific numerical data points marked on the graph, but the saturation and linear regions are clearly visible.

FIGURE 4.27 (a) PSpice circuit of a monolithic MOS buffer, and (b) its VTC. The MOSFET parameters are $k^{\prime}=100 \mu \mathrm{~A} / \mathrm{V}^{2}, W=10 \mu \mathrm{~m}, L=1 \mu \mathrm{~m}, V_{t 0}=0.5 \mathrm{~V}$, $\gamma=0.7 \mathrm{~V}^{1 / 2},\left|2 \phi_{\rho}\right|=0.6 \mathrm{~V}$, and $\lambda=0.05 \mathrm{~V}^{-1}$.
image_name:FIGURE 4.28 Voltage buffer with current-sink bias
description:
[
name: Vi, type: VoltageSource, ports: {Np: Vi, Nn: GND}
name: M1, type: NMOS, ports: {S: vo, D: VDD, G: Vi}
name: IBIAS, type: CurrentSource, ports: {Np: Vo, Nn: VSS}
]
extrainfo:The circuit is a voltage buffer with a current-sink bias. It includes an NMOS transistor biased by a current source. The input voltage Vi is applied to the gate of the NMOS, and the output voltage Vo is taken from the drain. The circuit is biased between VDD and VSS.
image_name:summary of its small-signal characteristics
description:The image consists of two main parts: a circuit diagram and a table summarizing small-signal characteristics.

**Circuit Diagram:**
- The circuit is a voltage buffer with a current-sink bias.
- It includes a MOSFET transistor, depicted with a gate, source, and drain.
- The input voltage \(v_i\) is applied through a resistor \(R_i\) to the gate of the MOSFET.
- The source is connected to the negative supply voltage \(V_{SS}\), and the drain is connected to the positive supply voltage \(V_{DD}\).
- A current source \(I_{BIAS}\) is connected between the source and drain.
- The output voltage \(v_o\) is taken across a load resistor \(R_o\) connected to the drain.

**Table of Small-Signal Characteristics:**
- The table contains expressions for three parameters:
- \(R_i = \infty\): This suggests that the input resistance is infinite, typical for a voltage buffer.
- \(a_{oc} \approx \frac{1}{1 + \chi}\): This represents the open-circuit voltage gain, indicating that the gain is reduced by a factor involving \(\chi\).
- \(R_o \approx \frac{1}{g_m + g_{mb}}\): This indicates the output resistance, which is inversely proportional to the sum of the transconductance \(g_m\) and the body transconductance \(g_{mb}\).

FIGURE 4.28 Voltage buffer with current-sink bias, and summary of its small-signal characteristics.
limits $R_{D} \rightarrow 0$ and $R_{S} \rightarrow \infty$. With a bit of algebra, we can put these expressions in the insightful forms

$$
\begin{equation*}
a_{o c}=\lim _{R_{s} \rightarrow \infty} \frac{v_{o}}{v_{i}}=\frac{1}{1+\chi+1 /\left(g_{m} r_{o}\right)} \quad R_{o}=\left(\frac{1}{g_{m}+g_{m b}}\right) / / / r_{o} \tag{4.45}
\end{equation*}
$$

with $\chi$ as given in Eq. (4.37). In view of the fact that $\left(g_{m}+g_{m b}\right) r_{o}>g_{m} r_{o} \gg 1$, we can simplify as

$$
\begin{equation*}
a_{o c} \cong \frac{1}{1+\chi} \quad R_{o} \cong \frac{1}{g_{m}+g_{m b}} \tag{4.46}
\end{equation*}
$$

Clearly, the effect of $g_{m b}$ is to lower both $a_{o c}$ and $R_{o}$ by about $1+\chi$ compared to the case $\gamma=0$. For instance, a voltage buffer implemented with the FET of Example 4.9 would give $a_{o c} \cong 1 /(1+0.15)=0.87 \mathrm{~V} / \mathrm{V}$ and $R_{o} \cong 1 /(1+0.15)=0.87 \mathrm{k} \Omega$.

In actual application the buffer is likely to drive some finite load resistance, and the $I_{B A S}$ current sink is likely to exhibit some finite parallel resistance. Lumping these two resistances together as a net resistance $R_{S}$, we observe that $R_{S}$ appears in parallel with $r_{o}$, so we adapt Eq. (4.45) to find the loaded gain as

$$
\begin{equation*}
\frac{v_{o}}{v_{i}}=\frac{1}{1+\chi+1 /\left[g_{m}\left(R_{S} / / r_{o}\right)\right]} \tag{4.47}
\end{equation*}
$$

We can gain additional insight by manipulating this expression into the following voltage-divider form

$$
\begin{equation*}
v_{o}=\frac{\left(1 / g_{m b}\right) / / R_{S} / / r_{o}}{1 / g_{m}+\left[\left(1 / g_{m b}\right) / / R_{S} / / r_{o}\right]} v_{i} \tag{4.48}
\end{equation*}
$$

which allows us to visualize the voltage buffer more intuitively as in Fig. 4.29. Note the similarity to the bipolar counterpart of Fig. 4.16, aside from the $1 / g_{m b}$ resistance, which is absent in the bipolar version.
image_name:FIGURE 4.29
description:
[
name: M1, type: NMOS, ports: {S: GND, D: vo, G: vi}
name: RS, type: Resistor, value: RS, ports: {N1: vo, N2: GND}
name: 1/gm, type: Resistor, value: 1/gm, ports: {N1: Out(1), N2: Vo}
name: 1/gmb, type: Resistor, value: 1/gmb, ports: {N1: Vo, N2: GND}
name: ro, type: Resistor, value: ro, ports: {N1: Vo, N2: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vo, N2: vo}
name: OpAmp, type: OpAmp, value: 1 V/V, ports: {InP: vi, InN: GND, OutP: Out(1)}
]
extrainfo:The circuit represents a FET voltage buffer with an NMOS transistor M1, resistors representing transconductance and output resistance, and an operational amplifier providing unity gain. The circuit is designed to act as a voltage divider with the output voltage vo.

FIGURE 4.29 A FET voltage buffer acts as a unity-gain buffer with output resistance $1 / g_{m}$, in turn forming a voltage divider with the rest of the resistances associated with the source terminal, or $\left(1 / g_{m b}\right) / / r_{o} / / R_{S}$.
(a) Let the FET of Fig. 4.28 have $V_{t 0}=0.5 \mathrm{~V}, k=2 \mathrm{~mA} / \mathrm{V}^{2}, \lambda=0.025 \mathrm{~V}^{-1}$, $\left|2 \phi_{p}\right|=0.6 \mathrm{~V}$, and $\gamma=0.4 \mathrm{~V}^{1 / 2}$. (a) If $V_{D D}=-V_{S S}=5.0 \mathrm{~V}$ and $I_{B A A S}=1 \mathrm{~mA}$, find the output voltage $V_{O}$ corresponding to the input voltage $V_{I}=0$.
(b) Estimate $a_{o c}$ and $R_{o}$.
(c) Find the gain if the circuit drives a $10-\mathrm{k} \Omega$ load.

#### Solution

(a) To sustain $I_{D}=1 \mathrm{~mA}$ the FET needs $V_{O V}=\sqrt{2 \times 1 / 2}=1 \mathrm{~V}$. As a firstestimate, let $V_{O(0)}=-\left(V_{t 0}+V_{O V}\right)=-(0.5+1)=-1.5 \mathrm{~V}$, so $V_{S B(0)}=-1.5-(-5)=3.5 \mathrm{~V}$. Then, $V_{t(1)}=0.5+0.4(\sqrt{3.5+0.6}-\sqrt{0.6})=1.0 \mathrm{~V}$, by Eq. (4.33). So a better estimate is $V_{O(1)}=-\left(V_{t(1)}+V_{O V}\right)=-(1+1)=-2 \mathrm{~V}$. This corresponds to $V_{S B(1)}=3 \mathrm{~V}$, so we iterate to find $V_{t(2)}=0.95 \mathrm{~V}$ and get yet a better estimate as $V_{O(2)}=-1.95 \mathrm{~V}$. One more iteration with $V_{S B(2)}=3.05 \mathrm{~V}$ yields a negligible change, so we conclude that with $V_{I}=0$ the circuit gives

$$
V_{o} \cong-1.95 \mathrm{~V}
$$

(b) We have $g_{m}=\sqrt{2 \times 2 \times 1}=2 \mathrm{~mA} / \mathrm{V}$ and $r_{o}=1 /\left(\lambda I_{D}\right)=1 /(0.025 \times 1)=$ $40 \mathrm{k} \Omega$. Also, Eq. (4.37) gives $\chi=0.4 /(2 \sqrt{3.05}+0.6)=0.105$. Consequently, use Eq. (4.46) to get

$$
a_{o c} \cong \frac{1}{1+0.105}=0.905 \mathrm{~V} / \mathrm{V} \quad R_{o} \cong \frac{1}{2(1+0.105)}=0.452 \mathrm{k} \Omega
$$

(Using the exact expressions of Eq. (4.45) we find $a_{o c}=0.895 \mathrm{~V} / \mathrm{V}$ and $R_{o}=0.447 \mathrm{k} \Omega$, hardly worth the extra computational effort.)
(c) We have $1 / g_{m}=1 / 2=0.5 \mathrm{k} \Omega$ and $1 / g_{m b}=1 /(0.105 \times 2)=4.76 \mathrm{k} \Omega$. Using Eq. (4.48) we get

$$
\frac{v_{o}}{v_{i}}=\frac{4.76 / / 10 / / 40}{0.5+4.76 / / 10 / / 40}=0.835 \mathrm{~V} / \mathrm{V}
$$

### The Active-Loaded CG Configuration as a Voltage Amplifier

The inherently high output resistance of the common-gate (CG) configuration makes it suited not only to current buffering, as we already know, but also to high-gain voltage amplification. To investigate this alternative aspect, refer to the monolithic
image_name:FIGURE 4.30
description:
[
name: I_LOAD, type: CurrentSource, value: I_LOAD, ports: {Np: VDD, Nn: Vo}
name: R_D, type: Resistor, value: R_D, ports: {N1: Vo, N2: GND}
name: NMOS1, type: NMOS, ports: {S: Vi, D: Vo, G: GND}
name: R_S, type: Resistor, value: R_S, ports: {N1: Vi, N2: GND}
name: I_BIAS, type: CurrentSource, value: I_BIAS, ports: {Np: Vi, Nn: VSS}
name: isig, type: CurrentSource, value: isig, ports: {Np: GND, Nn: Vi}
]
extrainfo:The circuit is a common-gate (CG) configuration used as a high-gain voltage amplifier. It utilizes an active load (I_LOAD) and a bias current source (I_BIAS). The input voltage is applied at Vi, and the output voltage is taken from Vo. The resistors R_D, R_O, R_i, and R_S help set the gain and input/output impedances. The equations provided describe input resistance (R_i), open-circuit voltage gain (a_oc), and output resistance (R_o).
image_name:ac characteristrics
description:The image illustrates a common-gate (CG) configuration used as a high-gain voltage amplifier. The circuit diagram is detailed, showing the arrangement of components and connections. At the top, the power supply voltage \( V_{DD} \) is connected to a current source labeled \( I_{LOAD} \), which acts as an active load. The output voltage \( V_o \) is taken across a resistor \( R_D \), which is connected to ground (GND).

The main component of the circuit is a transistor, depicted in the center of the diagram. The transistor's source is connected to a bias current source \( I_{BIAS} \), which provides the necessary source bias. The signal input \( v_i \) is applied to the source through a resistor \( R_S \). The transistor's gate is grounded, and its drain is connected to the output \( V_o \).

To the right of the circuit diagram, a box summarizes the AC characteristics of the configuration. Three equations are presented:

1. \( R_i \approx \frac{1}{g_m + g_{mb}} + \frac{R_D}{a_{oc}} \), which describes the input resistance.
2. \( a_{oc} = \lim_{R_D \to \infty} \frac{v_o}{v_i} = 1 + (g_m + g_{mb})r_o \), which defines the open-circuit voltage gain.
3. \( R_o = r_o + a_{oc} R_S \), which gives the output resistance.

These equations highlight the relationships between the various parameters, such as transconductance \( g_m \), body transconductance \( g_{mb} \), and output resistance \( r_o \), in determining the performance of the CG amplifier configuration.

FIGURE 4.30 The CG configuration as a high-gain voltage amplifier, and summary of its ac characteristrics.
rendition of Fig. 4.30, where the $I_{B I A S}$ current sink provides source bias, and the $I_{L O A D}$ current source acts as an active load. Also shown are the net resistance $R_{D}$ external to the drain, combining the parallel resistance of the $I_{L O A D}$ source as well as that of a possible output load, and the net resistance $R_{S}$ external to the source, combining the parallel resistances of the $i_{s i g}$ source and the $I_{B A S S}$ sink.

We wish to find the unloaded voltage gain from $v_{i}$ to $v_{o}$, that is, the gain $v_{o} / v_{i}$ in the limit $R_{D} \rightarrow \infty$, for this reason also called the open-circuit voltage gain. To this end, refer to the ac equivalent of Fig. 4.31. Since $v_{b s}=v_{g s}=-v_{i}$, we invert the direction of the dependent sources, and since they are in parallel, we lump them together
image_name:FIGURE 4.31
description:
[
name: gmvgs, type: VoltageControlledCurrentSource, ports: {Np: vo, Nn: vi}
name: gmbvbs, type: VoltageControlledCurrentSource, ports: {Np: vo, Nn: vi}
name: ro, type: Resistor, value: ro, ports: {N1: vo, N2: vi}
name: vi, type: VoltageSource, value: vi, ports: {Np: vi, Nn: GND}
name: (gm+gmb)vi, type: VoltageControlledCurrentSource, ports: {Np: vo, Nn: vi}
]
extrainfo:The circuit diagram shows an AC equivalent model to find the open-circuit voltage gain of a common gate (CG) configuration. The dependent sources are combined into a single source with a value of (gm + gmb)vi. The output voltage vo is measured across the resistor ro.

FIGURE 4.31 Ac equivalent to find the open-circuit voltage gain of the CG configuration.
as a single dependent source of value $\left(g_{m}+g_{m b}\right) v_{i}$, as shown. By KVL and Ohm's Law, $v_{o}=v_{i}+r_{o}\left(g_{m}+g_{m b}\right) v_{i}$, so

$$
\begin{equation*}
a_{o c}=\lim _{R_{D} \rightarrow \infty} \frac{v_{o}}{v_{i}}=1+\left(g_{m}+g_{m b}\right) r_{o} \tag{4.49}
\end{equation*}
$$

To find the resistance $R_{i}$ seen looking into the source and the resistance $R_{o}$ seen looking into the drain, we simply recycle the results tabulated in Fig. 4.23 and write

$$
\begin{equation*}
R_{i} \cong \frac{1}{g_{m}+g_{m b}}+\frac{R_{D}}{a_{o c}} \quad R_{o}=r_{o}+a_{o c} R_{S} \tag{4.50}
\end{equation*}
$$

As already seen, the drain resistance $R_{D}$ reflected to the source gets divided by $a_{o c}$, whereas the source resistance $R_{S}$ reflected to the drain gets multiplied by $a_{o c}$. These symmetric resistance-transformation properties are worth remembering, as they will appear frequently as we move along.

## 4.4 DARLINGTON, CASCODE, AND CASCADE CONFIGURATIONS

Up to now we have focused on single-transistor configurations, namely, the CE/CS voltage amplifier, the CC/CD voltage buffer, and the CB/CG current buffer. Each configuration implements its intended function but only as an approximation to the ideal. For instance, to avoid loading both at its input and output ports, a voltage amplifier/buffer should have $R_{i} \rightarrow \infty$ and $R_{o} \rightarrow 0$, while a current amplifier/buffer should have $R_{i} \rightarrow 0$ and $R_{o} \rightarrow \infty$. The CE amplifier, while capable of relatively high gain, has $R_{i}=r_{\pi}$, which is often not high enough. On the other hand, the CC configuration is renowned for its high input resistance, but at the price of a voltage gain a bit less than unity. It makes sense to combine the two configurations so that as a team they exploit the advantages of one to reduce the shortcomings of the other. The resulting CC-CE pair, along with its CC-CC sibling, belongs to a class of two-transistor circuits broadly referred to as the Darlington configuration and characterized by high input resistance.

On another subject, the design of high-gain amplifiers such as operational amplifiers and voltage comparators requires that high gains be achieved with as few amplifier stages as possible. The CE/CS configurations offer $a_{\text {instrinsic }}=-g_{m} r_{o}$, which may not be sufficiently high for this purpose, especially in the CS case. On the other hand, the $\mathrm{CB} / \mathrm{CG}$ current buffers are renowned for providing high output resistance, so if we combine a CE/CS amplifier with a current buffer we can raise the unloaded voltage gain way above the intrinsic gain of a single transistor. The resulting CE-CB and CS-CG pairs are known as the cascode configuration, a term coined in the days of vacuum tubes.

On yet another note, the advent of monolithic circuits with matched devices has ushered in other transistor pairings, such as the CC-CB and CD-CG configurations. Also known as emitter-coupled (EC) and source-coupled (SC) pairs, or collectively as differential pairs, they are used as the input stage of popular ICs such as the operational amplifier and the voltage comparator. These pairs play such an important role that they merit detailed attention separately. In the present section we focus on Darlington-type and cascode-type transistor pairs.

### The Darlington Configuration

Named after Sidney Darlington who patented it in1952, this configuration is based on the idea of feeding the emitter of one BJT to the base of another to achieve an overall current gain approaching the product of the individual current gains. Figure $4.32 a$ shows the npn realization of the Darlington concept, whereas Fig. $4.32 b$ shows its complementary version using pnp transistors. The function of the current source $I$ is to establish the operating point of $Q_{1}$ and also to help remove the base charge of $Q_{2}$ during turnoff (more on this in Chapter 6). This source is usually implemented with a plain resistor, or it may even be absent.

When it is absent, $Q_{1}$ is biased by $Q_{2}$ 's base current. This current may be too low for $Q_{1}$ to provide a reasonably high beta, hence the need to bias $Q_{1}$ more convincingly. We shall now demonstrate that a Darlington pair can be regarded as a single composite transistor. Though the discussion will focus on the npn pair, the results are readily adapted to the pnp pair, provided we reverse all voltage polarities and current directions.

In response to the applied current $I_{B}$, the configuration of Fig. $4.33 a$ develops the composite base-emitter voltage drop

$$
\begin{equation*}
V_{B E}=V_{B E 1}+V_{B E 2} \tag{4.51}
\end{equation*}
$$

where we are using subscripts 1 and 2 to denote parameters pertaining to $Q_{1}$ and $Q_{2}$, and no numerical subscripts for the composite transistor. To signify the need for two B-E voltage drops to turn it on, the composite device is sometimes drawn with two emitter arrows, as shown in Fig. 4.32. Assuming both transistors are operating in the forward-active region, the collector current of the composite device in Fig. 4.33a is

$$
\begin{aligned}
I_{C} & =I_{C 1}+I_{C 2}=\beta_{1} I_{B}+\beta_{2}\left(I_{E 1}-I\right)=\beta_{1} I_{B}+\beta_{2}\left[\left(\beta_{1}+1\right) I_{B}-I\right] \\
& =\left(\beta_{1}+\beta_{1} \beta_{2}+\beta_{2}\right) I_{B}-\beta_{2} I
\end{aligned}
$$

If we rewrite as

$$
I_{C}=\beta I_{B}-\beta_{2} I
$$

image_name:FIGURE 4.32 (a)
description:
[
name: Q1, type: NPN, ports: {C: C, B: B, E: P}
name: Q2, type: NPN, ports: {C: C, B: P, E: E}
name: I, type: CurrentSource, value: I, ports: {Np: P, Nn: E'}
]
extrainfo:The circuit is a Darlington pair configuration using NPN transistors Q1 and Q2. It is designed to provide high current gain. The current source I is connected between the base and emitter of the composite transistor.
image_name:FIGURE 4.32 (b)
description:
[
name: Q1, type: NPN, ports: {C: C, B: B, E: P}
name: Q2, type: NPN, ports: {C: C, B: P, E: E}
name: I, type: CurrentSource, ports: {Np: E, Nn: P}
]
extrainfo:The circuit in FIGURE 4.32 (b) represents a Darlington pair configuration using NPN transistors. It features two NPN transistors (Q1 and Q2) and a current source (I). The configuration is designed to provide high current gain by cascading the transistors. The collector of Q1 is connected to the base of Q2, and the emitters are connected together, forming the output. The collector of Q2 is the input for the overall composite device. This setup is commonly used to amplify weak signals in various electronic applications.

FIGURE 4.32 The Darlington configuration: (a) npn and (b) pnp.
image_name:Figure 4.32 (a)
description:
[
name: Q1, type: NPN, ports: {C: C, B: B, E: P}
name: Q2, type: NPN, ports: {C: C, B: P, E: E}
name: IB, type: CurrentSource, value: IB, ports: {Np: GND, Nn: B}
name: I, type: CurrentSource, value: I, ports: {Np: P, Nn: E}
]
extrainfo:The circuit is a Darlington configuration using two NPN transistors (Q1 and Q2) for high current gain. The collector of Q1 is connected to the base of Q2, and their emitters are connected together. This configuration is often used to amplify weak signals.
image_name:Figure 4.32 (b)
description:
[
name: Q1, type: NPN, ports: {C: C, B: B, E: X}
name: Q2, type: NPN, ports: {C: C, B: X, E: E}
name: Vbe, type: VoltageSource, value: Vbe, ports: {Np: B, Nn: GND}
]
extrainfo:This circuit is a Darlington pair configuration using two NPN transistors (Q1 and Q2) to provide high current gain. The collector of Q1 is connected to the base of Q2, and their emitters are connected together to form the output. The collector of Q2 serves as the input for the composite device, allowing it to amplify weak signals effectively.

FIGURE 4.33 Circuits to investigate the (a) dc and (b) ac characteristics of the npn Darlington configuration.
it is apparent that

$$
\begin{equation*}
\beta=\beta_{1}+\beta_{1} \beta_{2}+\beta_{2} \cong \beta_{1} \beta_{2} \tag{4.52}
\end{equation*}
$$

that is, the current gain of the composite device is approximately the product of the individual gains. We can look at the Darlington configuration from two alternative viewpoints (assume $I=0$ for simplicity). If we focus on $Q_{2}$, we can view $Q_{1}$ as providing a means to lower the required input current by a factor of $\beta_{1}$. For instance, to sustain $I_{C 2}=1 \mathrm{~mA}$ with $\beta_{1}=\beta_{2}=100$, we need $I_{B 2} \cong 10 \mu \mathrm{~A}$, but only $I_{B 1} \cong 0.1 \mu \mathrm{~A}$. Alternatively, if we focus on $Q_{1}$, we can view $Q_{2}$ as providing a means to boost the output current capability by a factor of $\beta_{2}$. For instance, with $I_{E 1}=10 \mathrm{~mA}$ and $\beta_{2}=50$, the Darlington configuration yields $I_{E 2} \cong 5 \mathrm{~A}$. In the former capacity, the Darlington configuration is often used in the design of low input bias current amplifiers. In the latter capacity, it is used in the design of the output stage of power amplifiers.

Turning next to the ac equivalent of Fig. $4.33 b$, we note that $Q_{1}$ acts as an emitter follower with $r_{\pi^{2}}$ as its emitter load, so the resistance seen looking into the base of the composite device is

$$
\begin{equation*}
R_{b}=r_{\pi 1}+\left(\beta_{1}+1\right) r_{\pi 2} \tag{4.53}
\end{equation*}
$$

We likewise observe that the base of $Q_{2}$ is terminated on the resistance $r_{e 1}$ seen looking into $Q_{1}$ 's emitter, so the resistance seen looking into the emitter of the composite device is, by inspection,

$$
\begin{equation*}
R_{e}=r_{e 2}+\frac{r_{e 1}}{\beta_{2}+1} \tag{4.54}
\end{equation*}
$$

Alternatively, this result could have been obtained as $R_{e}=R_{b} /(\beta+1)$, with $R_{b}$ and $\beta$ given by Eqs. (4.53) and (4.52). The transconductance of the composite device is found as $G_{m}=\alpha / R_{e} \cong 1 / R_{e}$. The result is

$$
\begin{equation*}
G_{m}=\frac{i_{c}}{v_{b e}}=\frac{g_{m 2}}{1+\frac{g_{m 2} / g_{m 1}}{\beta_{2}+1}} \tag{4.55}
\end{equation*}
$$

Finally, we seek an expression for the resistance $R_{c}$ seen looking into the composite collector. Due to the feedback path established by $r_{o 1}$ between the common collector node and $Q_{2}$ 's base node, we cannot use plain inspection. Rather, we need to replace the two transistors with their respective small-signal models, and then apply the test method to the common collector terminal. The result (see Problem 4.23) is

$$
\begin{equation*}
R_{c} \cong r_{o 2} / l\left(r_{o 1} \frac{1+\beta_{2} g_{m 1} / g_{m 2}}{1+\beta_{2}}\right) \tag{4.56}
\end{equation*}
$$

To get a better feel for the various parameters, it is instructive to consider the special case $I=0, \beta_{1}=\beta_{2}$, and $V_{A 1}=V_{A 2}$, for then the above expressions simplify as

$$
\begin{equation*}
\beta=\beta_{1}^{2} \quad R_{b}=2 r_{\pi 1} \quad G_{m}=\frac{g_{m 2}}{2} \quad R_{e}=2 r_{e 2} \quad R_{c}=\frac{2}{3} r_{o 2} \tag{4.57}
\end{equation*}
$$

EXAMPLE 4.13 Assuming a Darlington configuration with $\beta_{1}=\beta_{2}=100$ and $V_{A 1}=V_{A 2}=100 \mathrm{~V}$, find its small-signal parameters if $I_{C 2}=1 \mathrm{~mA}$ and $I=90 \mu \mathrm{~A}$.

#### Solution

We have $I_{C 1} \cong I_{E 1}=I_{B 2}+I=I_{C 2} / \beta_{2}+I \cong 1000 / 100+90=100 \mu \mathrm{~A}$. Consequently, $g_{m 2}=1 /(26 \Omega), r_{\pi 2}=2.6 \mathrm{k} \Omega, r_{o 2}=100 \mathrm{k} \Omega, g_{m 1}=1 /(260 \Omega), r_{\pi 1}=$ $26 \mathrm{k} \Omega$, and $r_{o 1}=1 \mathrm{M} \Omega$. Using Eqs. (4.52) through (4.56),

$$
\begin{aligned}
& \beta \cong 100 \times 100=10,000 \quad G_{m}=\frac{1 / 26}{1+(260 / 26) / 101}=\frac{1}{28.6 \Omega} \\
& R_{b} \cong 26+101 \times 2.6 \cong 290 \mathrm{k} \Omega \quad R_{e} \cong 26+\frac{260}{100+1}=28.3 \Omega \\
& R_{c} \cong 100 / /\left(1000 \frac{1+100 \times 26 / 260}{101}\right)=100 / / 109=52 \mathrm{k} \Omega
\end{aligned}
$$

Recall that pnp BJTs fabricated in the standard planar process exhibit poorer characteristics than their npn counterparts, so pnp BJTs should be avoided whenever possible. Shown in Fig. 4.34a is a popular alternative to the complementary pair of Fig. 4.32b. Named for G. C. Sziklai who patented it in the 1950s, this configuration acts like a composite $p n p$ BJT, except that it uses an $n p n$ device for $Q_{2}$, which usually provides a much higher current gain than a pnp type. Also referred to as quasi-complementary Darlington configuration, it enjoys the additional advantage of requiring only a single junction
image_name:(a)
description:
[
name: Q1, type: PNP, ports: {C: P, B: B, E: E}
name: Q2, type: PNP, ports: {C: E, B: P, E: C}
name: I, type: CurrentSource, value: I, ports: {Np: P, Nn: C}
]
extrainfo:The circuit diagram (a) represents a quasi-complementary Darlington configuration known as the Sziklai pair, which uses two PNP transistors and a current source. The configuration acts like a composite PNP BJT with a single junction voltage drop.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: P, D: C, G: G}
name: Q2, type: NPN, ports: {C: C, B: P, E: C}
name: I, type: CurrentSource, value: I, ports: {Np: P, Nn: E}
]
extrainfo:The circuit diagram (b) is a BiMOS Darlington configuration using an NMOS transistor (M1) and an NPN transistor (Q2). It provides high input impedance and current gain.

FIGURE 4.34 Alternative Darlington realizations: (a) quasi-complementary and (b) BiMOS.
voltage drop between its composite emitter and base, or $V_{E B}=V_{E B 1}$. The small-signal characteristics of the Sziklai pair are investigated further in Problem 4.24.

BiCMOS technology exploits the advantages of both BJTs and MOSFETs to further improve circuit performance. The Darlington rendition of Fig. $4.34 b$ uses a MOSFET to provide $R_{i}=\infty$ and a BJT to provide a higher current-drive capability as well as a higher transconductance.

### The CC-CE and CC-CC Configurations

IC design often utilizes slight variants of the Darlington configuration to meet special needs. Two examples are shown in Fig. 4.35. The CC-CE version of Fig. 4.35a avoids the reduction in $r_{o}$ due to $r_{o 1}$ 's feedback action by separating the collectors, as shown. Even more important, $Q_{1}$ provides a low-impedance drive to $Q_{2}$ to alleviate the impact of the Miller effect and thus maximize the frequency bandwidth, a subject we'll address in great detail in Chapter 6 when studying frequency/transient responses.
image_name:(a) CC-CE configuration
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: In, E: P}
name: Q2, type: NPN, ports: {C: Out, B: P, E: GND}
name: I, type: CurrentSource, ports: {Np: P, Nn: GND}
]
extrainfo:This is a CC-CE Darlington configuration with Q1 providing low-impedance drive to Q2, improving bandwidth by mitigating the Miller effect.
image_name:(b) CC-CC configuration
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: In, E: P}
name: Q2, type: NPN, ports: {C: VCC, B: P, E: Out}
name: I, type: CurrentSource, ports: {Np: P, Nn: GND}
]
extrainfo:This is a CC-CC configuration using two NPN transistors with a current source. The input is connected to the base of Q1, and the output is taken from the collector of Q2. The circuit is powered by VCC, and the current source provides biasing.
FIGURE 4.35 The (a) CC-CE and (b) CC-CC configurations.

### The Bipolar Cascode Configuration

This configuration is based on the artifice of feeding a CE voltage amplifier to a CB current buffer to raise the output resistance and, in so doing, to significantly increase the unloaded or open-circuit voltage gain $a_{o c}$ compared to the intrinsic gain of the CE stage. Also referred to as CE-CB amplifier, the cascode configuration offers another advantage, namely, a much wider gain-bandwidth product than the conventional CE amplifier-a topic that will be investigated in Chapter 6 (in the present section we limit ourselves to the low-frequency gain and the input/output resistances).

The circuit of Fig. $4.36 a$ uses the current source $I_{\text {LOAD }}$ as an active load, and the voltage sources $V_{B E 1}$ and $V_{B 2}$ to bias the BJTs. We assume that $V_{B E 1}$ has been adjusted so as to ensure that $Q_{2}$ 's collector is biased well within the linear region of operation, and that $V_{B 2}$ is high enough to prevent $Q_{1}$ from saturating ( $V_{B 2} \cong 1 \mathrm{~V}$ will do in this example). We now wish to find the small-signal characteristics of this circuit. To this end, refer to its ac equivalent of Fig. $4.36 b$ where we have, by inspection,

$$
\begin{equation*}
R_{i}=r_{\pi 1} \tag{4.58}
\end{equation*}
$$

To find $R_{o}$ we observe that $Q_{2}$ is subject to a good deal of emitter degeneration, with $Q_{1}$ 's collector resistance $r_{o 1}$ acting as $Q_{2}$ 's degeneration resistance. We thus write

$$
\begin{equation*}
R_{o}=r_{o 2}\left[1+g_{m 2}\left(r_{\pi 2} / / r_{o 1}\right)\right] \tag{4.59a}
\end{equation*}
$$

image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: v_c1, B: V_BE1 + V_i, E: GND}
name: Q2, type: NPN, ports: {C: Vo, B: V_B2, E: v_c1}
name: V_CC, type: VoltageSource, value: V_CC, ports: {Np: V_CC, Nn: GND}
name: I_LOAD, type: CurrentSource, value: I_LOAD, ports: {Np: V_CC, Nn: v_o}
name: V_B2, type: VoltageSource, value: V_B2, ports: {Np: V_B2, Nn: GND}
name: V_i, type: VoltageSource, value: V_i, ports: {Np: V_BE1 + V_i, Nn: V_BE1}
name: V_BE1, type: VoltageSource, value: V_BE1, ports: {Np: V_BE1, Nn: GND}
]
extrainfo:This is a CE-CB bipolar cascode configuration. Q1 and Q2 are NPN transistors. Q1's collector is connected to the emitter of Q2, forming the cascode structure. V_CC provides the supply voltage, and I_LOAD is the current source for the load. V_B2 and V_i are biasing voltages for Q2 and Q1 respectively. R_i is the input resistor, and R_o is the output resistor.

image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: vc1, B: vi, E: GND}
name: Vi, type: VoltageSource, value: Vi, ports: {Np: vi, Nn: GND}
name: r_pi2, type: Resistor, value: r_pi2, ports: {N1: vc1, N2: GND}
name: g_m2*v_pi2, type: VoltageControlledCurrentSource, value: g_m2*v_pi2, ports: {Np: v_o, Nn: vc1}
name: r_o2, type: Resistor, value: r_o2, ports: {N1: v_o, N2: vc1}
]
extrainfo:This circuit is a CE-CB (common-emitter, common-base) bipolar cascode configuration designed for high-frequency applications. It includes emitter degeneration and provides a high gain-bandwidth product with improved input and output isolation.

(b)

FIGURE 4.36 (a) The CE-CB, or bipolar cascode configuration, and (b) its ac equivalent.

For $r_{\pi 2} \ll r_{o 1}$ we can approximate $g_{m 2}\left(r_{\pi 2} / / r_{o 1}\right) \cong g_{m 2} r_{\pi 2}=\beta_{02}$, so the above expression simplifies as

$$
\begin{equation*}
R_{o} \cong\left(\beta_{02}+1\right) r_{o 2} \tag{4.59b}
\end{equation*}
$$

indicating that cascoding raises the output resistance by about $\beta_{02}+1$. To find the voltage gain, recall that in the absence of any external ac load the current $g_{m 2} \nu_{m 2}$ circulates entirely in the resistance $r_{o 2}$. Consequently, $Q_{1}$ acts as a CE amplifier with $r_{\pi 2}$ as its collector resistance, providing the voltage gain

$$
a_{1}=\frac{v_{c 1}}{v_{i}}=-g_{m 1}\left(r_{\pi 2} / / r_{o 1}\right)=-g_{m} \frac{r_{\pi} r_{o}}{r_{\pi}+r_{o}}=-\beta_{0} \frac{r_{o}}{r_{\pi}+r_{o}}
$$

where the numerical subscripts have been dropped to reflect the fact that matched and equally-biased BJTs exhibit identical small-signal parameters. We also know from Eq. (4.26) that the unloaded voltage gain of the CB stage $Q_{2}$ is

$$
a_{2}=\frac{v_{o}}{v_{c 1}}=1+g_{m 2} r_{o 2}
$$

Consequently, the overall unloaded voltage gain is $a_{o c}=v_{o} / v_{i}=\left(v_{o} / v_{c 1}\right) \times\left(v_{c 1} / v_{i}\right)=$ $a_{2} \times a_{1}=a_{1} \times a_{2}$, or

$$
\begin{equation*}
a_{o c}=-\beta_{0} \frac{r_{o}}{r_{\pi}+r_{o}}\left(1+g_{m} r_{o}\right) \tag{4.60a}
\end{equation*}
$$

where the numerical subscripts have again been omitted. For $r_{\pi} \ll r_{o}$ and $g_{m} r_{o} \gg 1$ we can approximate

$$
\begin{equation*}
a_{o c} \cong-\beta_{0} g_{m} r_{o} \tag{4.60b}
\end{equation*}
$$

Since $-g_{m} r_{o}$ represents a BJT's intrinsic gain, it is apparent that the artifice of cascoding raises this gain by almost $\beta_{0}$ ! This is not surprising once we realize that $Q_{1}$ 's collector current flows through $r_{\pi 2}$ to become $Q_{2}$ 's base current. Hence, the amplification factor $\beta_{0}$.

We observe that $R_{o}$ of Eq. (4.59b) is comparable to $r_{\mu}$, which has been deliberately omitted for the sake of simplicity. A more accurate expression is thus $R_{o} \cong\left(\beta_{02} r_{o 2}\right) / / r_{\mu}$. Using Eq. (4.8), we write

$$
\begin{equation*}
R_{o} \cong \frac{m}{m+1} \beta_{0} r_{o} \quad a_{o c} \cong-\beta_{0} g_{m} R_{o}=-\frac{m}{m+1} \beta_{0} g_{m} r_{o} \tag{4.61}
\end{equation*}
$$

Note that in order to fully realize the high-gain potential of the bipolar cascode we must avoid loading its output appreciably. We could buffer the cascode's output with a high input-resistance stage such as a Darlington-type voltage follower, or, in the case of BiMOS technology, with a MOSFET follower.

EXAMPLE 4.14 (a) Assuming a cascode configuration with $I_{L A D}=1 \mathrm{~mA}, \beta_{1}=\beta_{2}=100$, $V_{A 1}=V_{A 2}=100 \mathrm{~V}$, and $m=5$, find quick estimates for $R_{i}, R_{o}$, and $v_{o} / v_{i}$.
(b) Repeat if the circuit drives a 1-M $\Omega$ external load, and comment.

#### Solution

(a) Applying Eqs. (4.58) and (4.61) we get

$$
\begin{aligned}
& R_{i}=2.6 \mathrm{k} \Omega \quad R_{o} \cong \frac{5}{5+1} 100 \times 10^{5}=8.33 \mathrm{M} \Omega \\
& a_{o c}=-g_{m} R_{o}=-\frac{8.33 \times 10^{6}}{26} \cong-320 \times 10^{3} \mathrm{~V} / \mathrm{V}
\end{aligned}
$$

This is quite a gain!
(b) With an external load $R_{L}=1 \mathrm{M} \Omega$ the gain drops to

$$
\frac{v_{o}}{v_{i}}=a_{o c} \frac{R_{L}}{R_{o}+R_{L}} \cong-320 \times 10^{3} \frac{1}{8.33+1}=-34.3 \times 10^{3} \mathrm{~V} / \mathrm{V}
$$

Note almost an order of magnitude drop due to heavy output loading, even though a 1-M $\Omega$ load might seem large by common standards. Clearly, in order to fully realize the high-gain capabilities of the cascode, we must ensure that output loading is negligible.

EXAMPLE 4.15 To gain deeper insight it is instructive to follow the signal as it progresses from the input to the output node. In so doing, we will also get a chance to refine the quick estimate provided by Eq. (4.61).
(a) With reference to the cascode of Example 4.14a, find the individual gains $a_{1}$ and $a_{2}$ as well as the gain $a_{o c}$. Verify with PSpice and compare with Example 4.14a.
(b) Assuming a maximum output swing of $\left|v_{o(\max )}\right|=2.5 \mathrm{~V}$, find the corresponding input swing $\left|v_{i(\max )}\right|$. Do both BJTs meet the small-signal constraint $\left|v_{b e}\right| \leq 5 \mathrm{mV}$ ?

#### Solution

(a) For the CE stage $Q_{1}$ we have $a_{1}=-g_{m 1} R_{C 1}$, where $R_{C 1}$ is the total collector resistance of $Q_{1}$. By inspection, $R_{C 1} \cong r_{\mu 1} / / r_{o 1} / / R_{e 2}$, where $R_{e 2}$ is the resistance seen looking into the emitter of $Q_{2}$. Adapting the expression tabulated in Fig. 4.19 we get

$$
R_{e 2} \cong r_{e 2} \frac{r_{o 2}+r_{\mu 2}}{r_{o 2}+r_{\mu 2} /\left(\beta_{02}+1\right)}=\frac{100}{101} 26 \frac{0.1+50}{0.1+50 / 101}=2.17 \mathrm{k} \Omega
$$

so

$$
a_{1}=-g_{m 1} R_{C 1}=-\frac{50,000 / / 100 / / 2.17}{0.026}=-81.7 \mathrm{~V} / \mathrm{V}
$$

in excellent agreement with PSpice's prediction $a_{1}=-81.6 \mathrm{~V} / \mathrm{V}$. A quick estimate would have given $a_{1} \cong-\beta_{01}=-100 \mathrm{~V} / \mathrm{V}$ and $R_{e 2}=r_{\pi 2}=2.6 \mathrm{k} \Omega$.

Both estimates are higher than the actual values because they ignore the presence of $r_{o 2}$ and $r_{\mu 2}$. The gain of the CB stage $Q_{2}$ is

$$
a_{2}=1+g_{m 2} r_{o 2}=1+\frac{100}{0.026}=3846 \mathrm{~V} / \mathrm{V}
$$

so $a_{o c}=-81.7 \times 3846=-314 \times 10^{3} \mathrm{~V} / \mathrm{V}$, in excellent agreement with PSpice's $a_{o c}=-313 \times 10^{3} \mathrm{~V} / \mathrm{V}$.
(b) We have $\left|v_{i(\max )}\right|=\left|v_{o(\max )}\right| /\left|a_{o c}\right|=2.5 /(314,000) \cong 8 \mu \mathrm{~V}$. Moreover, $\left|v_{b e 2}\right|=$ $\left|v_{o(\max )}\right| / a_{2}=2.5 / 3846=0.65 \mathrm{mV}$, indicating that both BJTs amply meet the small-signal constraint.

### The MOS Cascode Configuration

The cascode concept, originally developed for vacuum tubes and subsequently adapted to BJTs, is widely used in MOS technology as well. Here, we feed a CS amplifier to a CG current buffer to raise the output resistance and, in so doing, we raise also the unloaded voltage gain. This is especially desirable in the case of FETs, which are notorious for their lower $g_{m} \mathrm{~s}$ compared to BJTs. Also referred to as the CS-CG amplifier, the cascode configuration is also an inherently faster circuit than an ordinary CS amplifier (this subject will be investigated in Chapter 6; in this section we limit ourselves to the low-frequency gain and the input/output resistances).

The circuit of Fig. 4.37a uses the current source $I_{\text {LOAD }}$ as active load, and the voltage sources $V_{G S 1}$ and $V_{G 2}$ to bias the FETs. We assume that $V_{G S 1}$ has been adjusted so
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vd1, G: Vi}
name: M2, type: NMOS, ports: {S: Vd1, D: Vo, G: VG2}
name: I_LOAD, type: CurrentSource, value: I_LOAD, ports: {Np: VDD, Nn: Vo}
name: V_GS1, type: VoltageSource, value: V_GS1, ports: {Np: V_GS1, Nn: GND}
name: V_G2, type: VoltageSource, value: V_G2, ports: {Np: V_GS2, Nn: GND}
name: V_DD, type: VoltageSource, value: V_DD, ports: {Np: VDD, Nn: GND}
name: v_i, type: VoltageSource, value: v_i, ports: {Np: Vi, Nn: VGS1}
]
extrainfo:This is a cascode amplifier circuit using NMOS transistors with a current source as active load. The circuit is designed to have high gain and wide bandwidth, with M1 and M2 configured in a common-source and common-gate topology respectively. The input is applied at the gate of M1, and the output is taken from the drain of M2. The circuit biases are provided by V_GS1 and V_G2, ensuring proper operation of the transistors.
image_name:(b)
description:
[
'name': 'Vi', 'type': 'VoltageSource', 'ports': {'Np': 'Vi', 'Nn': 'GND'
'name': 'ro1', 'type': 'Resistor', 'value': 'ro1', 'ports': {'N1': 'Vd1', 'N2': 'GND'
'name': 'ro2', 'type': 'Resistor', 'value': 'ro2', 'ports': {'N1': 'Vo', 'N2': 'GND'
]
extrainfo:The circuit is a small-signal equivalent of a cascode amplifier with NMOS transistors M1 and M2. It features a current source ILOAD as an active load and is biased with voltage sources VG2 and Vi. The output is taken across Ro, and the circuit is designed for high-frequency response with low input resistance.

FIGURE 4.37 (a) The CS-CG, or MOSFET cascode configuration, and (b) its smallsignal equivalent circuit.
as to ensure that $M_{2}$ 's drain is biased well within the linear region of operation, and that $V_{G 2}$ is high enough to bias $M_{1}$ at or above its edge of saturation. We now wish to find the small-signal characteristics of the overall circuit. To this end, refer to the ac equivalent of Fig. 4.37b. By inspection, the input resistance is

$$
\begin{equation*}
R_{i}=\infty \tag{4.62}
\end{equation*}
$$

To find the output resistance, let $v_{i} \rightarrow 0$, thereby deactivating the $g_{m 1} v_{g s 1}$ source and leaving only $r_{o 1}$ in place. This resistance causes a great deal of source degeneration for $M_{2}$, so we adapt Eq. (4.41) to write

$$
\begin{equation*}
R_{o}=r_{o 2}+\left[1+\left(g_{m 2}+g_{m b 2}\right) r_{o 2}\right] r_{o 1} \cong\left(g_{m 2}+g_{m b 2}\right) r_{o 1} r_{o 2} \tag{4.63}
\end{equation*}
$$

indicating that cascoding two FETs raises the output resistance dramatically. We expect the unloaded gain to increase accordingly. Referring again to Fig. 4.37b, we observe that in the absence of any external ac load, $M_{2}$ 's drain is an ac open circuit, so the entire ac equivalent of $M_{2}$ forms a self-contained subcircuit. The source $g_{m 1} v_{g s 1}$ sinks current out of $r_{o 1}$ to give, by Ohm's law, $v_{d 1}=-g_{m 1} v_{i} r_{o 1}$, so the gain of the CS stage $M_{1}$ is

$$
a_{1}=\frac{v_{d 1}}{v_{i}}=-g_{m 1} r_{o 1}
$$

As we know, this is $M_{1}$ 's intrinsic gain. By Eq. (4.49) the unloaded voltage gain of the CG stage $M_{2}$ is

$$
a_{2}=1+\left(g_{m 2}+g_{m b 2}\right) r_{o 2}
$$

Consequently, the overall voltage gain is $a_{o c}=v_{o} / v_{i}=\left(v_{o} / v_{d 1}\right) \times\left(v_{d 1} / v_{i}\right)=a_{2} \times a_{1}=$ $a_{1} \times a_{2}$, or

$$
\begin{equation*}
a_{o c}=-g_{m 1} r_{o 1}\left[1+\left(g_{m 2}+g_{m b 2}\right) r_{o 2}\right] \cong-g_{m 1} r_{o 1}\left(g_{m 2}+g_{m b 2}\right) r_{o 2} \tag{4.64}
\end{equation*}
$$

It is apparent that the artifice of cascoding increases $M_{1}$ 's intrinsic gain $-g_{m 1} r_{o 1}$ by a factor of about $\left(g_{m 2}+g_{m b 2}\right) r_{o 2}$, which is the gain contribution by $M_{2}$. This feature is widely exploited to make up for the low $g_{m}$ s of FETs! For instance, cascoding FETs with $\left|a_{\text {intrinsic }}\right|$ as low as $10 \mathrm{~V} / \mathrm{V}$ will yield $\left|a_{o c}\right| \cong 10^{2} \mathrm{~V} / \mathrm{V}$.

In order to fully realize the high-gain potential of the FET cascode we must avoid loading its output appreciably. This constraint is easily met in MOS technology, as the output of the cascode is likely to drive the gate of another FET, which presents an infinite input resistance, at least at low frequencies. This is a definite advantage compared to BJT cascodes: somehow, the high input-resistance of a FET makes up for the FET's notoriously low $g_{m}$ !

### The Telescopic Cascode Configuration

We have just seen that cascoding raises both the output resistance and the unloaded gain of the CS stage by the intrinsic gain of the CG stage. If desired, we can raise $a_{o c}$ and $R_{o}$ further by adding another level of cascoding, in the manner exemplified in Fig. 4.38 for the case of double cascoding. The stacking of transistors is reminiscent
image_name:FIGURE 4.38 The telescopic cascode configuration
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X2, G: VGS1+Vi}
name: M2, type: NMOS, ports: {S: X2, D: X1, G: VG2}
name: M3, type: NMOS, ports: {S: X1, D: Vo, G: VG3}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: ILOAD, type: CurrentSource, value: ILOAD, ports: {Np: VDD, Nn: Vo}
name: VG3, type: VoltageSource, value: VG3, ports: {Np: VG3, Nn: GND}
name: VG2, type: VoltageSource, value: VG2, ports: {Np: VG2, Nn: GND}
name: VGS1, type: VoltageSource, value: VGS1, ports: {Np: VGS1, Nn: GND}
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: VGS1}
]
extrainfo:This is a telescopic cascode configuration with three NMOS transistors stacked to increase the output resistance and gain. The circuit uses bias voltages VG3, VG2, and VGS1 to control the gates of M3, M2, and M1 respectively. The input voltage Vi is applied through Ri, and the output is taken across Ro at Vo.

FIGURE 4.38 The telescopic cascode
configuration (double cascode shown).
of a telescope extension, so this arrangement is aptly referred to as telescopic cascode. For instance, a three-transistor cascode using FETs with intrinsic gains as low as $10 \mathrm{~V} / \mathrm{V}$ each will yield $\left|a_{o c}\right| \cong 10^{3} \mathrm{~V} / \mathrm{V}$ ! This is a definite advantage of MOSFETs compared to BJTs, as a bipolar cascode, after one level of cascoding, already approaches its maximum possible gain of about $\beta_{0} a_{\text {instrinsic }}$.

The advantages of telescopic cascoding come at a price: a reduction in the output voltage swing (OVS). Assuming $M_{1}$ and $M_{2}$ are biased at the edge of saturation (EOS), the output must swing above

$$
\begin{equation*}
v_{O(\min )}=V_{O V 1}+V_{O V 2}+V_{O V 3} \tag{4.65}
\end{equation*}
$$

where $V_{O V 1}$ through $V_{O V 3}$ are the overdrive voltages of the stacked FETs. This limit may be unacceptably high in low power-supply systems. Fortunately, this drawback can be avoided by using the folded cascode technique discussed next.

### The Folded Cascode Configuration

A notorious drawback of the cascode configurations of Figs. 4.36 and 4.37 is limited voltage headroom at the output. With proper choice of the bias voltages $V_{B 2}$ and $V_{G 2}$, the best we can achieve is $v_{O(\text { min })}=2 V_{C E(\mathrm{EOS})}$ in the bipolar case, and $v_{O(\min )}=2 V_{D S(\mathrm{EOS})}=$ $2 V_{O V}$ in the MOS case. In both cases $v_{O(\min )}>0 \mathrm{~V}$. Yet, many applications call for $v_{o}$ 's ability to swing both above and below 0 V . We can meet this requirement by using a complementary transistor as the CB/CG stage, in the manner of Fig. 4.39. Aptly called folded cascode, this arrangement requires an additional current source $I_{B I A S}$ (typically $I_{B A S}=2 I_{L O A D}$ ) to bias the transistor pair, but this is a price well worth paying for expanded output headroom. In both cases $v_{O(\text { min })}$ is now established by the
image_name:(a)
description:
[
name: Qn, type: NPN, ports: {C: Vcn, B: Vi, E: GND}
name: Qp, type: PNP, ports: {C: Vo, B: Vbp, E: Vcn}
name: IBIAS, type: CurrentSource, ports: {Np: VCC, Nn: Vcn}
name: ILOAD, type: CurrentSource, ports: {Np: Vo, Nn: VEE}
name: VBEn, type: VoltageSource, value: VBEn, ports: {Np: VBEn, Nn: GND}
name: VBp, type: VoltageSource, value: VBp, ports: {Np: VBp, Nn: GND}
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: VBEn}
]
extrainfo:The circuit diagram depicts a folded cascode amplifier topology. It includes both bipolar (a) and CMOS (b) implementations. The bipolar version uses NPN and PNP transistors, while the CMOS version uses NMOS and PMOS transistors. Both versions include current sources for biasing and load, and resistors for input and output connections. The design allows for output voltage swing above and below 0 V, enhancing output headroom.
image_name:(b)
description:
[
name: Mn, type: NMOS, ports: {S: GND, D: Vdn, G: VGSn+Vi}
name: Mp, type: PMOS, ports: {S: Vdn, D: Vo, G: VGP}
name: IBIAS, type: CurrentSource, value: IBIAS, ports: {Np: VDD, Nn: Vdn}
name: ILOAD, type: CurrentSource, value: ILOAD, ports: {Np: Vo, Nn: VSS}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: VSS, type: VoltageSource, value: VSS, ports: {Np: GND, Nn: VSS}
name: VGSn, type: VoltageSource, value: VGSn, ports: {Np: VGSn, Nn: GND}
name: VGP, type: VoltageSource, value: VGP, ports: {Np: VGP, Nn: GND}
name: Vi, type: VoltageSource, value: Vi, ports: {Np: VGSn+Vi, Nn: VGSn}
]
extrainfo:This is a folded cascode amplifier circuit using CMOS technology. The circuit is designed to allow the output voltage to swing above and below 0V by using a complementary NMOS and PMOS pair. The additional current source IBIAS biases the transistor pair, providing expanded output headroom. The output voltage range is determined by the supply voltages VDD and VSS, along with the voltage drop across ILOAD.

FIGURE 4.39 Folded cascode: (a) bipolar, and (b) CMOS.
negative supply, along with the minimum permissible voltage drop $V\left(I_{L O A D}\right)_{\min }$ across the $I_{\text {LOAD }}$ current sink. We thus have for the BJT and CMOS circuits, respectively,

$$
\begin{equation*}
v_{O(\min )}=V_{E E}+V\left(I_{L O A D}\right)_{\min } \quad v_{O(\min )}=V_{S S}+V\left(I_{L O A D}\right)_{\min } \tag{4.66a}
\end{equation*}
$$

The upper bound on the output swing is established by the bias voltage $V_{B p}$ and $V_{G p}$, along with the minimum permissible voltage $V_{B I A S(\min )}$ across the $I_{B I A S}$ source. Selecting $V_{B p}$ and $V_{G p}$ so that this source is operated right at its minimum voltage drop, we have for the BJT and CMOS circuits, respectively,

$$
\begin{equation*}
v_{O(\max )}=V_{C C}-V\left(I_{B I A S}\right)_{\min }-V_{E C P(\mathrm{sat})} \quad v_{O(\max )}=V_{D D}-V\left(I_{B I A S}\right)_{\min }-V_{O V_{D}} \tag{4.66b}
\end{equation*}
$$

For instance, assuming $\pm 5-\mathrm{V}$ power supplies, along with $V\left(I_{B I A S}\right)_{\min }=V\left(I_{L O A D}\right)_{\min }=$ $V_{E C D(\text { sat })}=0.2 \mathrm{~V}$ in the BJT case, and $V\left(I_{B A A S}\right)_{\min }=V\left(I_{L O A D}\right)_{\text {min }}=V_{O V p}=0.5 \mathrm{~V}$ in the MOS case, the output voltage swings are

$$
-4.8 \mathrm{~V} \leq v_{O(\mathrm{BJT})} \leq 4.6 \mathrm{~V} \quad-4.5 \mathrm{~V} \leq v_{O(\mathrm{MOS})} \leq 4.0 \mathrm{~V}
$$

These compare quite favorably with the swings of the conventional cascodes of Figs. 4.36 and 4.37, which, for the same parameter values, are $0.4 \mathrm{~V} \leq v_{\text {(BJT) }} \leq 4.8 \mathrm{~V}$ and $1.0 \mathrm{~V} \leq v_{O(\mathrm{MOS})} \leq 4.5 \mathrm{~V}$.

### Cascoded Current Sources/Sinks

In Sections 4.2 and 4.3 we have made extensive use of current sources/sinks to provide dc bias $\left(I_{B A S}\right)$ as well as active loading $\left(I_{L O A D}\right)$. Current sources/sinks are themselves implemented with transistors. A good starting point is the collector or drain terminal, owing to the relative flatness of the active-region $i_{C^{-}} v_{C E}$ and $i_{D}-v_{D S}$ characteristics, whose slope is $1 / r_{o}$. There are many situations in which the curves are not
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: Vo, B: VB1, E: x}
name: Q2, type: NPN, ports: {C: x, B: VBE2, E: GND}
name: Load, type: Other, ports: {N1: VCC, N2: Vo}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: VB1, type: VoltageSource, value: VB1, ports: {Np: VB1, Nn: GND}
name: VBE2, type: VoltageSource, value: VBE2, ports: {Np: VBE2, Nn: GND'}
]
extrainfo:The circuit diagram (a) is a bipolar cascode configuration used to achieve high output resistance. It consists of two NPN transistors, Q1 and Q2, with a load connected to VCC. The resistors R0 and ro2 are used for biasing and setting the output resistance. Voltage sources VB1 and VBE2 provide the necessary biasing voltages. The current IO flows from VCC through the load to the ground.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: Vo, D: x, G: VG1}
name: M2, type: NMOS, ports: {S: GND, D: x, G: VGS2}
name: Load, type: Other, ports: {N1: VCC, N2: Vo}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: VG1, type: VoltageSource, value: VG1, ports: {Np: VG1, Nn: GND}
name: VGS2, type: VoltageSource, value: VGS2, ports: {Np: VGS2, Nn: GND}
]
extrainfo:The circuit diagram (b) shows a MOS cascode configuration to achieve high output resistance. It consists of two NMOS transistors (M1 and M2) with their sources connected to GND and drains connected to node x. The gates are controlled by VG1 and VGS2, respectively. The load is connected to the VCC and vO nodes, with a resistor Ro between vO and x, and ro2 between x and GND.

FIGURE 4.40 Using the (a) bipolar cascode and (b) MOS cascode to achieve high output resistance.
flat enough, so we must devise ways to raise the effective value of $r_{o}$. Already familiar examples are emitter and source degeneration, where we use a suitable resistance $R_{E}$ or $R_{S}$ in series with the emitter or source to provide a biasing function as well as raise the effective resistance seen looking into the collector or drain. However, it has already been pointed out that physical resistances are undesirable in monolithic circuits. Another serious drawback is that if a high degree of degeneration is needed, the degeneration resistance would have to be large, and its voltage drop could drastically reduce the available voltage headroom at the output of the source/sink.

An ingenious artifice is to replace the emitter/source degeneration resistance with a second transistor $Q_{2} / M_{2}$, and to let its resistance $r_{o 2}$ play the role of the degeneration resistance for the transistor $Q_{1} / M_{1}$. The result is the two-transistor circuits of Fig. 4.40 $a$ and $b$. These are the already familiar cascode circuits, except that we are now taking an alternative viewpoint: while in Figs. 4.36 and 4.37 we focused on the bottom transistor and added the top transistor to raise the bottom transistor's intrinsic gain, in Fig. 4.40 we focus on the top transistor and add the bottom transistor to raise the top transistor's output resistance.

Regardless of the viewpoint, the formulas developed earlier still stand, so we adapt them to the present case to write

$$
\begin{equation*}
R_{o(\mathrm{BJT})}=r_{o 1}\left[1+g_{m 1}\left(r_{\pi 1} / / r_{o 2}\right)\right] \tag{4.67}
\end{equation*}
$$

and

$$
\begin{equation*}
R_{o(\mathrm{MOS})}=r_{o 1}+\left[1+\left(g_{m 1}+g_{m b 1}\right) r_{o 1}\right] r_{o 2} \tag{4.68}
\end{equation*}
$$

As we know, for $r_{o 2} \gg r_{\pi 1}$ Eq. (4.67) simplifies as $R_{o} \cong\left(1+\beta_{01}\right) r_{o 1}$. Similarly, for $\left(g_{m 1}+g_{m b 1}\right) r_{o 1} \gg 1$ Eq. (4.68) simplifies as $R_{o} \cong(1+\chi) g_{m 1} r_{o 1} r_{o 2}$.

EXAMPLE 4.16 (a) Let the FETs of Fig. $4.40 b$ have $V_{t 0}=0.5 \mathrm{~V}, k=1.25 \mathrm{~mA} / \mathrm{V}^{2}, \lambda=0.08 \mathrm{~V}^{-1}$, $\left|2 \phi_{p}\right|=0.6 \mathrm{~V}$, and $\gamma=0.45 \mathrm{~V}^{1 / 2}$. Find the values of $V_{G 1}$ and $V_{G S 2}$ that will bias $M_{2}$ at the edge of saturation with $I_{D}=100 \mu \mathrm{~A}$.
(b) Find $R_{o}$ as well as $v_{O(\min )}$ for which $M_{1}$ is still saturated. What is the percentage change in $I_{O}$ for each 1-V change in $v_{O}$ above $v_{O(\min )}$ ?

#### Solution

(a) We have

$$
\begin{aligned}
& V_{O V 1}=V_{O V 2}=\sqrt{2 I_{D} / k}=\sqrt{2 \times 0.1 / 1.25}=0.4 \mathrm{~V} \\
& \text { so } V_{G S 2}=V_{t 0}+V_{O V 2}=0.5+0.4=0.9 \mathrm{~V} \text {. We also have } \\
& V_{t 1}=V_{t 0}+\gamma\left(\sqrt{V_{S B 1}+\left|2 \phi_{p}\right|}-\sqrt{\left|2 \phi_{p}\right|}\right) \\
& =0.5+0.45(\sqrt{0.4+0.6}-\sqrt{0.6})=0.6 \mathrm{~V} \\
& \text { so } V_{G 1}=V_{G S 1}+V_{D S 2}=V_{O V 1}+V_{t 1}+V_{O V 2}=0.4+0.6+0.4=1.4 \mathrm{~V} \text {. }
\end{aligned}
$$

(b) We have

$$
\begin{aligned}
g_{m 1} & =k_{1} V_{o V 1}=1.25 \times 0.4=0.5 \mathrm{~mA} / \mathrm{V} \\
r_{o 1} & =r_{o 2}=\frac{1}{\lambda I_{D}}=\frac{1}{0.08 \times 0.1}=125 \mathrm{k} \Omega \\
\chi & =\frac{\gamma}{2 \sqrt{V_{S B 1}+2\left|\phi_{p}\right|}}=\frac{0.45}{2 \sqrt{0.4+0.6}}=0.225 \\
R_{o} & =r_{o}+\left[1+(1+\chi) g_{m 1} r_{o}\right] r_{o}=125+[1+1.225 \times 0.5 \times 125] 125 \\
& =9.82 \mathrm{M} \Omega
\end{aligned}
$$

Also, $v_{O(\min )}=V_{O V 2}+V_{O V 1}=0.8 \mathrm{~V}$. For a 1-V change in $v_{O}$ within the linear region of operation we get $\Delta I_{O}=\Delta v_{o} / R_{o}=(1 \mathrm{~V}) /(9.82 \mathrm{M} \Omega)=102 \mathrm{nA}$, representing a change of only $\left(102 \times 10^{-9}\right) /\left(100 \times 10^{-6}\right) \cong 0.1 \%$.

### Cascaded Stages

When its gain specifications cannot be met with a single transistor, a circuit is implemented as a cascade of two or more individual stages. Already familiar examples are Darlington amplifiers, which use two stages to raise the input resistance as well as the current gain, and cascode amplifiers, which use CE-CB or CS-CG pairs to raise the output resistance as well as the unloaded voltage gain. (Incidentally, the word cascode, which denotes a particular example of a cascade, has not made it into mainstream dictionaries. So, chances are that a spell-checker will annoyingly change typed instances of cascode to cascade.)

When analyzing a cascade of two or more individual stages, an engineer often needs to come up with a quick estimate for the overall signal-to-load gain, with interstage loading automatically taken into account. To accomplish this, we label each
interstage node separately, and we find the loaded gain from one node to the next using the familiar rules of thumb:

The loaded gain of a CE/CS voltage amplifier stage is the (negative of the) ratio of the total resistance associated with the collector/drain to the total resistance associated with emitter/source.

A voltage follower acts as a unity-gain buffer with output resistance $1 / g_{m}$, in turn forming a voltage divider with the rest of the resistances associated with the emitter/source.

Then, we find the gain of the entire cascade as the product of the individual gains. Study the following example carefully, as we will have plenty of occasions to retrace this procedure as we move along.

Shown in Fig. 4.41 is the ac equivalent of a three-stage amplifier consisting of CE stage $Q_{1}$, followed by CE-ED stage $Q_{2}$, followed in turn by CC stage $Q_{3}$. Assuming for simplicity that all three BJTs have $g_{m}=1 /(25 \Omega), r_{\pi}=5 \mathrm{k} \Omega$, and $r_{o}=50 \mathrm{k} \Omega$, estimate the overall gain $v_{o} / v_{i}$.
image_name:Figure 4.41
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: vi, Nn: GND}
name: Rs, type: Resistor, value: 1kΩ, ports: {N1: vi, N2: v1}
name: RC1, type: Resistor, value: 10kΩ, ports: {N1: v2, N2: GND}
name: RC2, type: Resistor, value: 10kΩ, ports: {N1: v3, N2: GND}
name: RE2, type: Resistor, value: 0.2kΩ, ports: {N1: v4, N2: GND}
name: RL, type: Resistor, value: 10kΩ, ports: {N1: vo, N2: GND}
name: Q1, type: NPN, ports: {C: v2, B: v1, E: GND}
name: Q2, type: PNP, ports: {C: v3, B: v2, E: v4}
name: Q3, type: NPN, ports: {C: GND, B: v3, E: Vo}
]
extrainfo:The circuit is a three-stage amplifier consisting of a common-emitter (CE) stage, a common-emitter with emitter degeneration (CE-ED) stage, and a common-collector (CC) stage. The BJTs have parameters gm = 1/25Ω, rπ = 5kΩ, and ro = 50kΩ. The overall gain is to be estimated from vo/vi.

FIGURE 4.41 Circuit of Example 4.17.

#### Solution

Even though the node voltages of interest to us are $v_{i}$ and $v_{o}$, we label also the intermediate nodes $v_{1}, v_{2}$, and $v_{3}$, as they will appear in our intermediate calculations. We make the following considerations:

- In progressing from node $v_{i}$ to node $v_{1}$ the signal encounters a voltage divider formed by $R_{s}$ and the resistance $R_{1}$ presented by node $v_{1}$. By inspection, $R_{1}=$ $r_{\pi 1}$, so

$$
\frac{v_{1}}{v_{i}}=\frac{R_{1}}{R_{s}+R_{1}}=\frac{r_{\pi 1}}{R_{s}+r_{\pi 1}}=\frac{5}{1+5}=0.833 \mathrm{~V} / \mathrm{V}
$$

- In progressing from node $v_{1}$ to node $v_{2}$ the signal undergoes amplification by the CE stage $Q_{1}$, whose total emitter resistance is $r_{e 1}\left(=\alpha_{01} / g_{m 1} \cong 1 / g_{m 1}\right)$, and whose total collector resistance $R_{2}$ consists of three components: $R_{C 1}, r_{o 1}$, and the ac resistance $R_{b 2}$ seen looking into $Q_{2}$ 's base. By inspection, $R_{b 2}=r_{\pi 2}+$ $\left(\beta_{2}+1\right) R_{E 2}=5+[(5 / 0.025)+1] \times 0.2=45.2 \mathrm{k} \Omega$, so we write

$$
\frac{v_{2}}{v_{1}}=-\frac{R_{C 1} / / r_{o l} / / R_{b 2}}{r_{e 1}} \cong-\frac{10 / / 50 / / 45.2}{0.025}=-281 \mathrm{~V} / \mathrm{V}
$$

- In progressing from $v_{2}$ to $v_{3}$ the signal undergoes amplification by the CE-ED stage $Q_{2}$. The total emitter resistance is $\alpha_{02} / g_{m 2}+R_{E 2} \cong 25+200=$ $225 \Omega$. The total collector resistance $R_{3}$ consists of three components: $R_{C 2}$, the ac resistance $R_{c 2}$ seen looking into $Q_{2}$ 's collector, and the ac resistance $R_{b 3}$ seen looking into $Q_{3}$ 's base. By inspection, $R_{c 2}=r_{o 2}\left[1+g_{m 2}\left(r_{\pi 2} / / R_{E 2}\right)\right]=$ $50[1+(5 / / 0.2) / 0.025]=435 \mathrm{k} \Omega$, and $R_{b 3}=r_{\pi 3}+\left(\beta_{3}+1\right) R_{E 3}=5+201 \times 10=$ $2.015 \mathrm{M} \Omega$. Consequently,

$$
\frac{v_{3}}{v_{2}}=-\frac{R_{C 2} / / R_{c 2} / / R_{b 3}}{r_{e 2}+R_{E 2}} \cong-\frac{10 / / 435 / / 2015}{0.025+0.200}=-43.2 \mathrm{~V} / \mathrm{V}
$$

- In progressing from $v_{3}$ to $v_{o}$ the signal is buffered by the CC stage $Q_{3}$, acting as a unity-gain amplifier with output resistance $1 / g_{m 3}=25 \Omega$. This resistance forms a voltage divider with the combination $R_{L} / / r_{o 3}=10 / / 50=8.33 \mathrm{k} \Omega$, so

$$
\frac{v_{o}}{v_{3}}=1 \times \frac{R_{L} / / r_{o 3}}{r_{e 3}+\left(R_{L} / / r_{o 3}\right)} \cong \frac{8.33}{0.025+8.33}=0.997 \mathrm{~V} / \mathrm{V}
$$

We finally have

$$
\begin{aligned}
\frac{v_{o}}{v_{i}} & =\frac{v_{1}}{v_{i}} \times \frac{v_{2}}{v_{1}} \times \frac{v_{3}}{v_{2}} \times \frac{v_{o}}{v_{3}}=0.833 \times(-281) \times(-43.2) \times 0.997 \\
& =10.1 \times 10^{3} \mathrm{~V} / \mathrm{V}
\end{aligned}
$$

## 4.5 DIFFERENTIAL PAIRS

We now turn our attention to another important transistor pair, namely, the differential pair. Already introduced informally in Section 4.1, this is probably the most widely used subcircuit in analog ICs. Even though the concept was initially developed for vacuum tubes and subsequently adapted to discrete BJTs, it was the advent of monolithic circuits that made it possible to realize its full potential. This is because performance is critically dependent upon matching between the two transistors, and the monolithic process offers matched devices also capable of tracking each other with temperature and time. Compared to single-transistor amplifiers, differential amplifiers are much more immune to a type of interference noise known as commonmode noise, and lend themselves to dc coupling, thus avoiding the bulky capacitors of discrete designs. In fact, the differential amplifier functions over a frequency range
extending all the way down to dc. All this comes at the price of increased circuit complexity, but it is not a problem in monolithic circuits, where additional transistors are easily available at insignificant extra cost.

The monolithic differential pair was first realized in bipolar form, taking on the name of emitter-coupled (EC) pair. Once MOS technology became commercially viable, the concept was adapted to MOSFETs as the source-coupled (SC) pair. Let us investigate both implementations in proper detail.

### The Emitter-Coupled Pair

The simplest form of the emitter-coupled (EC) pair is shown in Fig. 4.42. Emitter bias for the pair is provided by a current source, here modeled by the Norton equivalent consisting of $I_{E E}$ and $R_{E E}$. (In a well-designed circuit, $R_{E E}$ is large and is often ignored, especially in the course of dc analysis.) Since one side is the exact mirror image of the other, the circuit is also said to be balanced, and this symmetry is exploited to facilitate circuit analysis, as we shall see. To develop a basic feel for the circuit, let us investigate its large-signal behavior (to keep things simple, in this section we assume $V_{A}=\infty$ ).

Applying KVL around the input loop gives

$$
v_{I 1}-v_{B E 1}+v_{B E 2}-v_{I 2}=0
$$

that is, $v_{B E 1}-v_{B E 2}=v_{I 1}-v_{I 2}$. Assuming forward-active operation for the BJTs, we use the familiar exponential relationships and write $i_{C 1}=I_{s 1} \exp \left(v_{B E 1} / V_{T}\right)$ and $i_{C 2}=I_{s 2} \exp \left(v_{B E 2} / V_{T}\right)$. Consequently,

$$
\frac{i_{C 1}}{i_{C 2}}=\frac{I_{s 1}}{I_{s 2}} \exp \left(\frac{v_{B E 1}-v_{B E 2}}{V_{T}}\right)=\frac{I_{s 1}}{I_{s 2}} \exp \left(\frac{v_{n 1}-v_{t 2}}{V_{T}}\right)
$$

image_name:FIGURE 4.42 The emitter-coupled (EC) pair
description:
[
name: Q1, type: NPN, ports: {C: vO1, B: vI1, E: P}
name: Q2, type: NPN, ports: {C: vO2, B: vI2, E: P}
name: VI1, type: VoltageSource, value: VI1, ports: {Np: vI1, Nn: GND}
name: VI2, type: VoltageSource, value: VI2, ports: {Np: vI2, Nn: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: vO1}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: vO2}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: P, Nn: VEE}
name: REE, type: Resistor, value: REE, ports: {N1: P, N2: VEE}
]
extrainfo:The circuit is an emitter-coupled pair (EC pair) with two matched NPN transistors Q1 and Q2. The emitters are connected together and biased with a current source IEE. The collectors are connected to VCC through identical resistors RC. Input voltages V11 and V12 are applied to the bases of Q1 and Q2, respectively.

FIGURE 4.42 The emitter-coupled (EC) pair.

Matched transistors have $I_{s 1}=I_{s 2}$, so the above relation simplifies as

$$
\begin{equation*}
\frac{i_{C 1}}{i_{C 2}}=\exp \left(\frac{v_{I D}}{V_{T}}\right) \tag{4.69}
\end{equation*}
$$

where

$$
\begin{equation*}
v_{I D}=v_{I 1}-v_{I 2} \tag{4.70}
\end{equation*}
$$

is the difference between the input voltages. By KCL, the emitter currents are such that $i_{E 1}+i_{E 2}=I_{E E}$, where we are ignoring $R_{E E}$, which in a well-designed circuit is very large. This allows us to write

$$
\begin{equation*}
i_{C 1}+i_{C 2}=\alpha_{F} I_{E E} \tag{4.71}
\end{equation*}
$$

Combining Eqs. (4.69) and (4.71) we readily get

$$
\begin{equation*}
i_{C 1}=\frac{\alpha_{F} I_{E E}}{1+\exp \left(-v_{i D} / V_{T}\right)} \quad i_{C 2}=\frac{\alpha_{F} I_{E E}}{1+\exp \left(v_{i D} / V_{T}\right)} \tag{4.72}
\end{equation*}
$$

We also have, by KVL and Ohm's law,

$$
v_{O 1}=V_{C C}-R_{C} i_{C 1} \quad v_{O 2}=V_{C C}-R_{C} i_{C 2}
$$

Substituting the expressions of Eq. (4.72) and simplifying we obtain an expression for the voltage difference at the output,

$$
\begin{equation*}
v_{O D}=v_{O 1}-v_{O 2}=\alpha_{F} I_{E E} R_{C} \tanh \left(-\frac{v_{I D}}{2 V_{T}}\right) \tag{4.73}
\end{equation*}
$$

We can readily plot Eqs. (4.72) and (4.73) using PSpice. In the circuit of Fig. 4.43 we have set $v_{I 2}=0$, so $v_{I D}=v_{I 1}$ in this case. After directing PSpice to sweep
image_name:Figure 4.43
description:
[
name: Q1, type: NPN, ports: {C: Vo1, B: VID, E: P}
name: Q2, type: NPN, ports: {C: Vo2, B: GND, E: P}
name: RC1, type: Resistor, value: 10kΩ, ports: {N1: Vo1, N2: VCC}
name: RC2, type: Resistor, value: 10kΩ, ports: {N1: Vo2, N2: VCC}
name: VID, type: VoltageSource, value: VID, ports: {Np: VID, Nn: GND}
name: VCC, type: VoltageSource, value: 12V, ports: {Np: VCC, Nn: GND}
name: VEE, type: VoltageSource, value: -12V, ports: {Np: GND, Nn: P}
name: IEE, type: CurrentSource, value: 1mA, ports: {Np: P, Nn: GND'}
]
extrainfo:The circuit is a differential amplifier using BJTs. Q1 and Q2 form the differential pair with resistors RC1 and RC2 as the collector loads. The differential input voltage is applied across VID, and the output is taken differentially across vO1 and vO2. The circuit is powered by VCC and VEE, with a constant current source IEE providing biasing.

FIGURE 4.43 PSpice circuit to plot the transfer curves of an EC pair using BJTs with $\beta_{F}=100$ and $l_{s}=2 \mathrm{fA}$.
image_name:(a)
description:The graph labeled (a) is a plot of the collector currents, \(i_{C1}\) and \(i_{C2}\), versus the differential input voltage \(v_{ID}\) for a differential amplifier circuit using bipolar junction transistors (BJTs). This is a linear plot with the input voltage \(v_{ID}\) on the x-axis, ranging from \(-4V_T\) to \(4V_T\), where \(V_T\) is the thermal voltage, approximately 25 mV at room temperature. The y-axis represents the collector currents \(i_{C1}\) and \(i_{C2}\) in milliamperes (mA), ranging from 0 to 1 mA.\n\n### Overall Behavior and Trends:\n- **Symmetrical Behavior:** The graph shows symmetrical behavior about the point \(v_{ID} = 0\).\n- **Current Splitting:** At \(v_{ID} = 0\), the current \(I_{EE}\) is equally split between the two transistors, resulting in \(i_{C1} = i_{C2} = 0.5\) mA.\n- **Opposite Trends:** As \(v_{ID}\) increases towards \(4V_T\), \(i_{C1}\) increases from 0.5 mA to 1 mA, while \(i_{C2}\) decreases from 0.5 mA to 0 mA. Conversely, as \(v_{ID}\) decreases towards \(-4V_T\), \(i_{C1}\) decreases to 0 mA and \(i_{C2}\) increases to 1 mA.\n\n### Key Features and Technical Details:\n- **Intersection Point:** The currents \(i_{C1}\) and \(i_{C2}\) intersect at \(v_{ID} = 0\), indicating equal current distribution.\n- **Linear Changes:** The changes in collector currents are linear with respect to \(v_{ID}\) within the plotted range.\n- **Maximum and Minimum Values:** \(i_{C1}\) reaches a maximum of 1 mA when \(v_{ID} = 4V_T\) and a minimum of 0 mA when \(v_{ID} = -4V_T\). Similarly, \(i_{C2}\) has a maximum of 1 mA when \(v_{ID} = -4V_T\) and a minimum of 0 mA when \(v_{ID} = 4V_T\).\n\n### Annotations and Specific Data Points:\n- **Gridlines and Markers:** The plot includes gridlines at \(-2V_T\), 0, and \(2V_T\) for both axes, aiding in the visualization of the trends.\n- **Symmetrical Cross:** The graph forms a symmetrical cross pattern, highlighting the inverse relationship between \(i_{C1}\) and \(i_{C2}\) as \(v_{ID}\) varies.
image_name:(b)
description:The graph labeled '(b)' is a plot of the output voltage difference \( v_{OD} \) as a function of the differential input voltage \( v_{ID} \) for a differential amplifier using BJTs. This is a voltage transfer characteristic plot.

1. **Axes Labels and Units:**
- The horizontal axis represents the input voltage \( v_{ID} \), ranging from \(-4V_T\) to \(4V_T\), where \( V_T \) is the thermal voltage (approximately 25 mV at room temperature).
- The vertical axis represents the output voltage difference \( v_{OD} \) in volts, ranging from -10 V to 10 V.

2. **Overall Behavior and Trends:**
- The graph shows a nonlinear relationship between \( v_{ID} \) and \( v_{OD} \). It is a typical S-shaped curve characteristic of a differential amplifier.
- At \( v_{ID} = 0 \), the output voltage \( v_{OD} \) is zero, indicating that the currents through the transistors are balanced.
- As \( v_{ID} \) increases positively, \( v_{OD} \) decreases, and as \( v_{ID} \) decreases negatively, \( v_{OD} \) increases.

3. **Key Features and Technical Details:**
- The plot is symmetric about the origin, reflecting the balanced nature of the differential amplifier.
- The slope of the curve around \( v_{ID} = 0 \) is steep, indicating high gain in this region.
- The curve flattens as \( v_{ID} \) moves towards \( \pm 4V_T \), showing saturation behavior where further increases in \( v_{ID} \) have less effect on \( v_{OD} \).

4. **Annotations and Specific Data Points:**
- The graph includes a small annotation labeled 'a', which likely marks the linear region of operation where the amplifier provides maximum gain. This is typically around the origin where \( v_{ID} = 0 \).
- The significant points where the curve starts to flatten indicate the limits of the linear amplification region.

FIGURE 4.44 Plots of (a) the collector currents $i_{C 1}$ and $i_{C 2}$, and (b) plot of the difference $v_{O D}$ between the collector voltages of the PSpice circuit of Fig. 4.43
$v_{I D}$ from $-4 V_{T}\left(\cong-100 \mathrm{mV}\right.$ ) to $4 V_{T}(\cong+100 \mathrm{mV}$ ), we obtain the traces of Fig. 4.44.
We make the following observations:

- For $v_{I D}=0, I_{E E}$ splits equally between $Q_{1}$ and $Q_{2}$, giving $i_{C 1}=i_{C 2}=\alpha_{F} I_{E E} / 2 \cong$ 0.5 mA . With equal currents, $R_{C 1}$ and $R_{C 2}$ drop equal voltages, giving $v_{O 1}=v_{O 2}=$ $12-10 \times 0.5=7 \mathrm{~V}$. Consequently, $v_{O D}=v_{O 1}-v_{O 2}=0$, and we say that with $v_{I D}=0$ the EC pair is in dc balance.
- Raising $v_{I D}$ above 0 V makes $Q_{1}$ more conductive at the expense of $Q_{2}$ becoming less conductive ( $i_{C 1}$ increases while $i_{C 2}$ decreases). This current imbalance causes $v_{O 1}$ to drop while $v_{O 2}$ rises, causing a two-fold decrease in $v_{O D}$.
- As $v_{I D}$ reaches about $4 V_{T}(\cong 100 \mu \mathrm{~V})$, we can say that virtually all of $I_{E E}$ comes from $Q_{1}$ while $Q_{2}$ is essentially off. Consequently, $v_{O 1} \cong 12-10 \times 1=2 \mathrm{~V}$, $v_{O 2} \cong 12 \mathrm{~V}$, and $v_{O D} \cong 2-12=-10 \mathrm{~V}$. Increasing $v_{I D}$ further will simply cause $v_{O D}$ to saturate at -10 V .
- Lowering $v_{I D}$ below 0 V makes $Q_{2}$ more conductive and $Q_{1}$ less conductive. The roles of $Q_{1}$ and $Q_{2}$ are now interchanged, and the curves are therefore symmetric with respect to the origin. Lowering $v_{I D}$ below about -100 mV causes $v_{O D}$ to saturate at +10 V .
We are particularly interested in the voltage transfer curve (VTC) of Fig. 4.44b. Since BJTs are nonlinear devices, it is not surprising that this curve is also nonlinear. However, if we restrict operation in the vicinity of the origin, the VTC can be approximated with its tangent there, so we can write

$$
\begin{equation*}
v_{o d}=a v_{i d} \tag{4.74}
\end{equation*}
$$

where $v_{o d}$ and $v_{i d}$ are small variations of $v_{O D}$ and $v_{I D}$ about 0 V , and $a$ is the slope of the VTC at the origin, as indicated in the figure. Differentiating Eq. (4.73) and calculating the derivative at the origin gives

$$
\begin{equation*}
a=-\frac{\alpha_{F} I_{E E} R_{C}}{2 V_{T}}=-g_{m} R_{C} \tag{4.75}
\end{equation*}
$$

where

$$
\begin{equation*}
g_{m}=\frac{\alpha_{F} I_{E E}}{2 V_{T}} \cong \frac{I_{E E}}{2 V_{T}} \tag{4.76}
\end{equation*}
$$

is the transconductance of the BJTs at dc balance, where $I_{C 1}=I_{C 2} \cong 0.5 I_{E E}$. The slope of the VTC represents the small-signal voltage gain $a$. With the component values of Fig. 4.43, $a \cong-(1 / 0.052) \times 10=-192$ V/V. Note that unlike the circuits of Chapter 2, the EC pair achieves this gain without requiring any capacitors, and it does so all the way down to arbitrarily low signal frequencies, including dc!

Since the EC pair responds to the difference between its input voltages, it is also called a differential amplifier. Though the pair of Fig. 4.42 is based on npn BJTs, a differential amplifier can also be implemented using pnp devices, provided voltage and current polarities are suitably reversed (see Problem 4.40). As we move along, we will work with both $n p n$ and $p n p$ pairs.

### The Source-Coupled Pair

Figure 4.45 shows the MOS counterpart of the bipolar differential amplifier of Fig. 4.42. Its analysis proceeds pretty much as in the BJT case, except that the exponential characteristics of BJTs are now replaced by the quadratic characteristics of MOSFETs. (To keep things simple, in this section we assume $\lambda=0$ and $\gamma=0$.) Applying KVL around the input loop gives

$$
v_{l 1}-v_{G S 1}+v_{G S 2}-v_{12}=0
$$

image_name:Figure 4.45 The source-coupled (SC) pair
description:
[
name: M1, type: NMOS, ports: {S: P, D: vo1, G: vI1}
name: M2, type: NMOS, ports: {S: P, D: vo2, G: vI2}
name: RD1, type: Resistor, value: RD, ports: {N1: VDD, N2: vo1}
name: RD2, type: Resistor, value: RD, ports: {N1: VDD, N2: vo2}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: VSS, type: VoltageSource, value: VSS, ports: {Np: VSS, Nn: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: vI1, Nn: GND}
name: V2, type: VoltageSource, value: V2, ports: {Np: vI2, Nn: GND}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: GND}
name: RSS, type: Resistor, value: RSS, ports: {N1: VSS, N2: P}
]
extrainfo:The circuit is a source-coupled pair using NMOS transistors M1 and M2. It is powered by VDD and VSS, with differential inputs V1 and V2. The current source ISS provides biasing, and RD resistors are used as loads for each transistor.

FIGURE 4.45 The source-coupled (SC) pair.
that is, $v_{G S 1}-v_{G S 2}=v_{I 1}-v_{I 2}$. Assuming saturated FETs, we use the familiar quadratic relationships to write

$$
v_{G S 1}=V_{t 1}+\sqrt{2 i_{D 1} / k_{1}} \quad v_{G S 2}=V_{t 2}+\sqrt{2 i_{D 2} / k_{2}}
$$

Matched FETs have $V_{t 1}=V_{t 2}=V_{t}$ and $k_{1}=k_{2}=k$, so the above relationships yield

$$
\begin{equation*}
v_{I D}=v_{I 1}-v_{I 2}=v_{G S 1}-v_{G S 2}=\frac{\sqrt{i_{D 1}}-\sqrt{i_{D 2}}}{\sqrt{k / 2}} \tag{4.77}
\end{equation*}
$$

By KCL, the transistor currents satisfy the condition

$$
\begin{equation*}
i_{D 1}+i_{D 2}=I_{S S} \tag{4.78}
\end{equation*}
$$

where we are ignoring $R_{S S}$, which in a well-designed circuit is very large. We have two equations in the two unknowns $i_{D 1}$ and $i_{D 2}$. Letting $i_{D 2}=I_{S S}-i_{D 1}$ in Eq. (4.77), squaring both sides, and rearranging, we get

$$
\sqrt{i_{D 1}\left(I_{S S}-i_{D 1}\right)}=\frac{1}{2}\left(I_{S S}-\frac{k}{2} v_{I D}^{2}\right)
$$

Squaring once again and rearranging,

$$
i_{D 1}^{2}-I_{S S} i_{D 1}+\frac{1}{4}\left(I_{S S}-\frac{k}{2} v_{I D}^{2}\right)^{2}=0
$$

Solving this quadratic equation and retaining only the physically acceptable solution we get

$$
\begin{equation*}
i_{D 1}=\frac{I_{S S}}{2}\left[1+\frac{v_{I D}}{\sqrt{I_{S S} / k}} \sqrt{1-\frac{v_{I D}^{2}}{4 I_{S S} / k}}\right] \tag{4.79a}
\end{equation*}
$$

Using again $i_{D 2}=I_{S S}-i_{D 1}$, we likewise find

$$
\begin{equation*}
i_{D 2}=\frac{I_{S S}}{2}\left[1-\frac{v_{I D}}{\sqrt{I_{S S} / k}} \sqrt{1-\frac{v_{I D}^{2}}{4 I_{S S} / k}}\right] \tag{4.79b}
\end{equation*}
$$

We also have, by KVL and Ohm's law,

$$
v_{O 1}=V_{D D}-R_{D} i_{D 1} \quad v_{O 2}=V_{D D}-R_{D} i_{D 2}
$$

Using the expressions of Eq. (4.79) we get, after suitable simplifications, an expression for the voltage difference at the output,

$$
\begin{equation*}
v_{O D}=v_{O 1}-v_{O 2}=-R_{D} \sqrt{k I_{S S}} v_{I D} \sqrt{1-\frac{v_{I D}^{2}}{4 I_{S S} / k}} \tag{4.80}
\end{equation*}
$$

We can readily plot Eqs. (4.79) and (4.80) using PSpice. In the circuit of Fig. 4.46 we have set $v_{l 2}=0$, so $v_{I D}=v_{I 1}$ in this case. After directing PSpice to sweep $v_{I D}$ from
image_name:FIGURE 4.46
description:
[
name: M1, type: NMOS, ports: {S: P, D: vO1, G: VID}
name: M2, type: NMOS, ports: {S: P, D: vO2, G: GND}
name: RD1, type: Resistor, value: 10kΩ, ports: {N1: vO1, N2: VDD}
name: RD2, type: Resistor, value: 10kΩ, ports: {N1: vO2, N2: VDD}
name: VID, type: VoltageSource, value: VID, ports: {Np: VID, Nn: GND}
name: ISS, type: CurrentSource, value: 1mA, ports: {Np: P, Nn: VSS}
name: VDD, type: VoltageSource, value: 12V, ports: {Np: VDD, Nn: GND}
name: VSS, type: VoltageSource, value: -12V, ports: {Np: GND, Nn: VSS}
]
extrainfo:The circuit is a differential amplifier using NMOS transistors M1 and M2. It operates with a dual supply of +12V and -12V. The input voltage VID is applied to the gate of M1, while M2 is grounded. The differential output voltage VOD is measured between vO1 and vO2. The current source ISS provides a constant current of 1mA to the source nodes of M1 and M2.

FIGURE 4.46 PSpice circuit to plot the transfer curves of an SC pair using FETs with $k=1.0 \mathrm{~mA} / \mathrm{V}^{2}$ and $V_{t}=1.0 \mathrm{~V}$.
-2 V to +2 V , we obtain the traces of Fig. 4.47, in connection with which we make the following observations:

- For $v_{I D}=0, I_{S S}$ splits equally between $M_{1}$ and $M_{2}$, giving $i_{D 1}=i_{D 2}=I_{S S} / 2=$ 0.5 mA . With equal currents, $R_{D 1}$ and $R_{D 2}$ drop equal voltages, giving $v_{O 1}=$ $v_{O 2}=12-10 \times 0.5=7 \mathrm{~V}$. Consequently, we have $v_{O D}=v_{O 1}-v_{O 2}=0$, and we say that the SC pair is in dc balance. The overdrive voltage $V_{O V}$ required of each FET to sustain $I_{S S} / 2$ is such that $I_{S S} / 2=(k / 2) V_{O V}^{2}$, or

$$
\begin{equation*}
V_{O V}=\sqrt{\frac{I_{S S}}{k}} \tag{4.81}
\end{equation*}
$$

In our example, $V_{O V}=\sqrt{1 / 1}=1 \mathrm{~V}$.
image_name:(a)
description:The graph is a plot of the drain currents $i_{D1}$ and $i_{D2}$ against the input voltage $v_{ID}$. This is a typical characteristic curve of a differential pair in a balanced state.

1. **Type of Graph and Function:**
- This is a characteristic curve plot showing the relationship between drain currents and input voltage for a differential pair of transistors.

2. **Axes Labels and Units:**
- The horizontal axis represents the input voltage $v_{ID}$, with units presumably in volts (V), although not explicitly labeled.
- The vertical axis represents the drain currents $i_{D1}$ and $i_{D2}$, measured in milliamperes (mA).
- The scale on both axes appears to be linear.

3. **Overall Behavior and Trends:**
- The graph shows two curves, $i_{D1}$ and $i_{D2}$, which are mirror images of each other about the vertical axis.
- At $v_{ID} = 0$, both currents are equal at 0.5 mA, indicating a balanced state.
- As $v_{ID}$ increases towards $\sqrt{2}V_{OV}$, $i_{D1}$ increases towards 1.0 mA while $i_{D2}$ decreases towards 0 mA.
- Conversely, as $v_{ID}$ decreases towards $-\sqrt{2}V_{OV}$, $i_{D2}$ increases towards 1.0 mA while $i_{D1}$ decreases towards 0 mA.

4. **Key Features and Technical Details:**
- The point where $v_{ID} = 0$ is a critical point where the currents are balanced.
- The curves are symmetric, indicating that the system responds equally to positive and negative input voltages.
- The transition from 0.5 mA to 1.0 mA (and vice versa) occurs smoothly, suggesting a continuous and predictable change in conductivity of the transistors.

5. **Annotations and Specific Data Points:**
- The graph is annotated with $i_{D1}$ and $i_{D2}$ to indicate the respective curves.
- The input voltage values $\sqrt{2}V_{OV}$ and $-\sqrt{2}V_{OV}$ are marked on the horizontal axis, representing the limits of the input voltage range considered in this plot.
image_name:(b)
description:The graph is a plot of the difference in drain voltages, labeled as $v_{OD}$, for a given circuit. This is a time-domain waveform that illustrates how the drain voltages vary with respect to an input voltage, $v_{ID}$.

**Axes Labels and Units:**
- The x-axis represents the input voltage, $v_{ID}$, with units of volts. The scale is linear, with significant markers at $-\sqrt{2}V_{OV}$, 0, and $\sqrt{2}V_{OV}$.
- The y-axis represents the drain currents, $i_{D1}$ and $i_{D2}$, with units of milliamps (mA). The scale is linear, ranging from 0 to 1 mA.

**Overall Behavior and Trends:**
- The graph features two curves that intersect at the center point, where $v_{ID} = 0$.
- The curve labeled $i_{D1}$ increases from 0 mA to 1 mA as the input voltage $v_{ID}$ increases from $-\sqrt{2}V_{OV}$ to $\sqrt{2}V_{OV}$.
- Conversely, the curve labeled $i_{D2}$ decreases from 1 mA to 0 mA over the same range of input voltage.
- The curves exhibit a symmetrical, sigmoid-like behavior around the origin, indicating a balance point where the currents are equal.

**Key Features and Technical Details:**
- At $v_{ID} = 0$, both $i_{D1}$ and $i_{D2}$ are equal to 0.5 mA, indicating a balanced state.
- The curves are symmetrical about the y-axis, indicating that changes in $v_{ID}$ in either direction from zero result in opposite changes in $i_{D1}$ and $i_{D2}$.
- The transition between the minimum and maximum values of the currents is smooth, with no abrupt changes or discontinuities.

**Annotations and Specific Data Points:**
- The graph is marked at critical points $-\sqrt{2}V_{OV}$ and $\sqrt{2}V_{OV}$, where $i_{D1}$ and $i_{D2}$ reach their respective maximum and minimum values.
- The intersection point at $v_{ID} = 0$ is a significant feature, representing the equilibrium or balance point for the circuit's operation.

(a)
image_name:(b)
description:The graph displayed is a plot of the output voltage difference, denoted as $v_{OD}$, against the input voltage $v_{ID}$. This graph is a linear plot, with both axes labeled appropriately: the horizontal axis represents the input voltage $v_{ID}$ and is measured in volts (V), while the vertical axis represents the output voltage $v_{OD}$, also in volts (V).

**Axes and Units:**
- **Horizontal Axis:** Input voltage $v_{ID}$ in volts (V).
- **Vertical Axis:** Output voltage $v_{OD}$ in volts (V).

**Overall Behavior and Trends:**
- The graph shows a smooth, continuous curve that transitions from a positive to a negative output voltage as the input voltage increases from $-\sqrt{2}V_{OV}$ to $\sqrt{2}V_{OV}$.
- At $v_{ID} = 0$, the output voltage $v_{OD}$ crosses the zero point, indicating a significant equilibrium or balance point in the circuit's operation.
- The transition between the maximum and minimum values of the output voltage is smooth, with no abrupt changes or discontinuities.

**Key Features and Technical Details:**
- The graph is marked at critical points $-\sqrt{2}V_{OV}$ and $\sqrt{2}V_{OV}$, where the output voltage $v_{OD}$ reaches its maximum and minimum values, respectively.
- The plot shows a linear decrease in $v_{OD}$ as $v_{ID}$ increases, indicating that as $v_{ID}$ is raised above 0 V, $M_1$ becomes more conductive while $M_2$ becomes less conductive. This results in a decrease in $v_{O1}$ and an increase in $v_{O2}$, causing a decrease in $v_{OD}$.

**Annotations and Specific Data Points:**
- The graph is annotated with a point labeled 'a', which appears to highlight a specific data point or region of interest where the slope of the curve is particularly relevant.
- The intersection at $v_{ID} = 0$ is highlighted as a critical point for the circuit's operation, representing a balanced state between the two transistors $M_1$ and $M_2$.

This graph effectively illustrates the relationship between the input and output voltages in the circuit, emphasizing the continuous and smooth nature of the transition between states.

(b)

FIGURE 4.47 Plots of (a) the drain currents $i_{D 1}$ and $i_{D 2}$, and (b) plot of the difference $v_{O D}$ in the drain voltages for the PSpice circuit of Fig. 4.46.

- Raising $v_{I D}$ above 0 V makes $M_{1}$ more conductive at the expense of $M_{2}$ becoming less conductive ( $i_{D 1}$ increases while $i_{D 2}$ decreases). This imbalance causes $v_{O 1}$ to drop while $v_{O 2}$ rises, causing a two-fold decrease in $v_{O D}$.
- As we raise $v_{I D}$ further, we reach a point at which all of $I_{S S}$ will come from $M_{1}$ and none from $M_{2}$. For this to occur, $M_{1}$ 's overdrive must be $\sqrt{2}$ times as large as in Eq. (4.81), owing to the quadratic dependence of current on overdrive. At this point we have $v_{G S 2}=V_{t}$ and $v_{G S 1}=V_{t}+\sqrt{2} V_{O V}$, that is, $v_{I D}=\sqrt{2} V_{O V}$, with $V_{O V}$ as given in Eq. (4.81). Beyond this point, the voltages saturate at $v_{O 1} \cong$ $12-10 \times 1=2 \mathrm{~V}, v_{O 2} \cong 12 \mathrm{~V}$, and $v_{O D} \cong 2-12=-10 \mathrm{~V}$.
- Lowering $v_{I D}$ below 0 V makes $M_{2}$ more conductive and $M_{1}$ less conductive. The roles of $M_{1}$ and $M_{2}$ are now interchanged, thereby yielding curves that are symmetric about the origin. Saturation now occurs for $v_{I D} \leq-\sqrt{2} V_{O V}$, where $v_{O D}=+10 \mathrm{~V}$.
We are especially interested in the voltage transfer curve (VTC) of Fig. 4.47b. Since FETs are nonlinear devices, it is not surprising that this curve is also nonlinear. However, if we restrict operation in the vicinity of the origin, the VTC can be approximated with its tangent there, so we can write

$$
\begin{equation*}
v_{o d}=a v_{i d} \tag{4.82}
\end{equation*}
$$

where $v_{o d}$ and $v_{i d}$ represent small variations of $v_{O D}$ and $v_{I D}$ about 0 V , and $a$ is the slope of the VTC at the origin, as indicated in the figure. Differentiating Eq. (4.80) and calculating it at the origin gives

$$
\begin{equation*}
a=-R_{D} \sqrt{k I_{S S}}=-g_{m} R_{D} \tag{4.83}
\end{equation*}
$$

where

$$
\begin{equation*}
g_{m}=\sqrt{k I_{S S}} \tag{4.84a}
\end{equation*}
$$

is the transconductance of the FETs at dc balance, where $I_{D 1}=I_{D 2}=0.5 I_{S S}$. The slope of the VTC represents the small-signal voltage gain $a$. With the component values of Fig. 4.46 we have $a \cong-10 \times \sqrt{1 / 1}=-10 \mathrm{~V} / \mathrm{V}$. Unlike the circuits of Chapter 3, the SC pair achieves this gain without requiring any capacitors and it functions all the way down to arbitrarily low signal frequencies, including dc!

Since the SC pair responds to the difference between its input voltages, it is also called a differential amplifier. Though the pair of Fig. 4.45 is based on $n$-channel FETs, a differential amplifier can also be implemented using $p$-channel devices, provided voltage and current polarities are suitably reversed (see Problem 4.48). As we move along, we will work with both types of pairs.

Rewriting Eq. (4.84a) as

$$
\begin{equation*}
g_{m}=\frac{I_{S S}}{V_{O V}} \tag{4.84b}
\end{equation*}
$$

allows for the direct comparison with the BJT expression of Eq. (4.76): if an SC pair and an EC pair are biased equally, the ratio of the transconductances is $g_{m(\mathrm{SC})} / g_{m(\mathrm{EC})}=2 V_{T} / V_{O V}$. Typically, $g_{m(\mathrm{SC})} / g_{m(\mathrm{EC})} \ll 1$ because usually $V_{O V} \gg 2 V_{T}$.

### Intuitive Ac Analysis of Differential Pairs

Even though VTC analysis has already provided us with expressions for the smallsignal gains, in daily practice one needs to come up with quick ac parameter estimates by performing ac analysis directly on the circuit itself. The ability to investigate a circuit from different perspectives is highly desirable because it reinforces our understanding, not to mention that we can use one method to find results and another to check them.

Let us turn first to the EC pair of Fig. 4.48a, representing the ac equivalent of the circuit of Fig. 4.42. In small-signal operation the BJTs of Fig. 4.42 draw identical dc currents,

$$
\begin{equation*}
I_{C 1}=I_{C 2}=I_{C}=\frac{\alpha_{F} I_{E E}}{2} \cong \frac{I_{E E}}{2} \tag{4.85}
\end{equation*}
$$

so their transconductances are also identical,

$$
\begin{equation*}
g_{m 1}=g_{m 2}=g_{m}=\frac{I_{C}}{V_{T}} \cong \frac{I_{E E}}{2 V_{T}} \tag{4.86}
\end{equation*}
$$

Focusing on the lower part of the circuit, we can regard $Q_{1}$ as a unity-gain emitter follower with output resistance $R_{e 1}$ in turn loaded by the resistance $R_{e 2}$ provided by $Q_{2}$. Since $R_{e 1}=R_{e 2}$ at dc balance, the voltage divider rule indicates that the ac voltage at the shared emitter terminal is $v_{i} / 2$, as shown. The ac current into $Q_{1}$ 's collector is thus $i_{c}=g_{m 1} v_{b e 1}=$ $g_{m 1}\left(v_{b 1}-v_{e 1}\right)=g_{m 1}\left(v_{i}-v_{i} / 2\right)=g_{m} v_{i} / 2$. This current emerges out of $Q_{1}$ 's emitter as $i_{e}\left(=i_{c} / \alpha_{0}\right)$, it flows into $Q_{2}$ 's emitter, and emerges once again out of $Q_{2}$ 's collector as $\alpha_{0} i_{e}$, that is, it emerges again as $i_{c}$ (the fact that $v_{b e 1}=v_{i} / 2$ and $v_{b e 2}=-v_{i} / 2$ confirms equal magnitudes but opposite polarities for the two $i_{c}$ currents). By KVL and Ohm's Law we have $v_{o}=v_{o 1}-v_{o 2}=-R_{C} i_{c}-\left(R_{C} i_{c}\right)=-2 R_{C} i_{c}=-2 R_{C} g_{m} v_{i} / 2=-g_{m} R_{C} v_{i}$, so

$$
\begin{equation*}
a=\frac{v_{o}}{v_{i}}=-g_{m} R_{C} \tag{4.87}
\end{equation*}
$$

image_name:(a)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: vi, Nn: GND}
name: Q1, type: NPN, ports: {C: vo1, B: vi, E: vi/2}
name: Q2, type: NPN, ports: {C: vo2, B: vi/2, E: GND}
name: RC, type: Resistor, value: RC, ports: {N1: GND, N2: vo1}
name: RC, type: Resistor, value: RC, ports: {N1: GND, N2: vo2}
]
extrainfo:The circuit diagram (a) represents a differential amplifier using NPN transistors Q1 and Q2. The input voltage vi is applied to the base of Q1, and the emitters of Q1 and Q2 are connected through resistors Re1 and Re2. The collectors are connected to the output nodes vo1 and vo2 through resistors RC. The circuit amplifies the difference between the input signals.
image_name:(b)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: M1, type: NMOS, ports: {S: vi/2, D: vo1, G: Vi}
name: M2, type: NMOS, ports: {S: GND, D: vo2, G: Vi/2}
name: RD, type: Resistor, value: RD, ports: {N1: GND, N2: vo1}
name: RD, type: Resistor, value: RD, ports: {N1: GND, N2: vo2}
]
extrainfo:Diagram (b) represents a small-signal equivalent circuit of an SC pair. It consists of two NMOS transistors (M1 and M2) with a differential input Vi. The resistors RD provide the load resistance for the transistors. The circuit is configured to produce differential output voltages vo1 and vo2.

FIGURE 4.48 Small-signal equivalents of (a) the EC pair, and (b) the SC pair.
where $a$ is the already familiar differential gain of the EC pair. Expressing it in the alternative form

$$
\begin{equation*}
a=-\frac{R_{C} I_{E E} / 2}{V_{T}} \tag{4.88}
\end{equation*}
$$

allows us to estimate the gain of the EC pair by taking the ratio of the voltage $R_{C} \times$ $\left(I_{E E} / 2\right)$ dropped at dc balance by the collector resistors to the thermal voltage $V_{T}$. Recall from Chapter 2 that the small-signal approximation holds so long as $\left|v_{b e}\right| \ll 2 V_{T}$. Considering that presently we have $v_{b e 1}=-v_{b e 2}=v_{i} / 2$, the small-signal condition is now

$$
\begin{equation*}
\left|v_{i}\right| \ll 4 V_{T} \tag{4.89}
\end{equation*}
$$

Thus, for the small-signal approximation to hold with an error of no more than about $10 \%$, we approximately need $\left|v_{i}\right| \leq 10 \mathrm{mV}$.

Turning next to the SC pair of Fig. 4.48b, representing the ac equivalent of the circuit of Fig. 4.45, we note its formal similarity to its bipolar counterpart of Fig. 4.48a, and conclude that we can recycle a good deal of previous derivations. Thus, at dc balance the FETs draw identical dc currents,

$$
\begin{equation*}
I_{D 1}=I_{D 2}=I_{D}=\frac{I_{S S}}{2} \tag{4.90}
\end{equation*}
$$

so their transconductances are also identical,

$$
\begin{equation*}
g_{m 1}=g_{m 2}=g_{m}=\sqrt{k I_{S S}} \tag{4.91}
\end{equation*}
$$

We can view $M_{1}$ as a unity-gain source follower with output resistance $R_{s 1}$, in turn loaded by the resistance $R_{s 2}$ provided by $M_{2}$ 's source. Since $R_{s 1}=R_{s 2}$ at dc balance, the voltage divider rule indicates that the ac voltage at the shared source terminal is $v_{i} / 2$, as shown. The ac current into $M_{1}$ 's drain is thus $i_{d}=g_{m 1} v_{g s 1}=g_{m 1}\left(v_{g 1}-v_{s 1}\right)=$ $g_{m} v_{i} / 2$. This current exits $M_{1}$ 's source, enters $M_{2}$ 's source, and finally exits $M_{2}$ 's drain (this is confirmed by the fact that with $v_{g s 1}=v_{i} / 2$ and $v_{s s 2}=-v_{i} / 2$ the two $i_{d}$ currents have equal magnitudes but opposite polarities). Finally, $v_{o}=v_{o 1}-v_{o 2}=-R_{D} i_{d}-$ $\left(R_{D} i_{d}\right)=-2 R_{D} g_{m} v_{i} / 2=R_{D} g_{m} v_{i}$, so

$$
\begin{equation*}
a=\frac{v_{o}}{v_{i}}=-g_{m} R_{D} \tag{4.92}
\end{equation*}
$$

This is the already familiar differential gain of the SC pair. Expressing it in the alternative form

$$
\begin{equation*}
a=-\frac{R_{D} I_{S S} / 2}{0.5 V_{o V}} \tag{4.93}
\end{equation*}
$$

allows us to estimate the gain achievable with this circuit as the ratio of the voltage $R_{D} \times\left(I_{S S} / 2\right)$ dropped by the drain resistors at dc balance to half the overdrive voltage. Recall from Chapter 3 that the small-signal approximation holds provided we keep
$\left|v_{g s}\right| \ll 2 V_{O V}$. Considering that presently we have $v_{g s 1}=-v_{g s 2}=v_{i} / 2$, the small-signal condition is now

$$
\begin{equation*}
\left|v_{i}\right| \ll 4 V_{O V} \tag{4.94}
\end{equation*}
$$

Looking at Fig. 4.47b, where $V_{O V}=1 \mathrm{~V}$, we see that a reasonable choice is to restrict the input within the range $\left|v_{i}\right| \leq 0.5 V_{O V}$ (or 0.5 V in our example).

## 4.6 COMMON-MODE REJECTION RATIO IN DIFFERENTIAL PAIRS

As implied by its name, a differential amplifier responds only to the difference $v_{i d}=v_{i 1}-v_{i 2}$, regardless of the individual values of $v_{i 1}$ and $v_{i 2}$. For instance, when subjected to any one of the following input pairs

$$
\left(v_{i 1}, v_{i 2}\right)=(0.005 \mathrm{~V}, 0.000 \mathrm{~V}),(1.005 \mathrm{~V}, 1.000 \mathrm{~V}),(-2.000 \mathrm{~V},-2.005 \mathrm{~V})
$$

a differential amplifier with a gain of, say, $-100 \mathrm{~V} / \mathrm{V}$ will respond only to their difference ( $v_{i d}=5 \mathrm{mV}$ in each of the three cases) to give $v_{o}=-100 \times 5=-500 \mathrm{mV}$, even though the individual inputs are in the vicinity of 0 V in the first case, 1 V in the second case, and -2 V in the third case. For a more systematic analysis, it is convenient to define the differential-mode input as

$$
\begin{equation*}
v_{i d}=v_{i 1}-v_{i 2} \tag{4.95a}
\end{equation*}
$$

and the average, or common-mode input as

$$
\begin{equation*}
v_{i c}=\frac{v_{i 1}+v_{i 2}}{2} \tag{4.95b}
\end{equation*}
$$

Turning these equations around allows us to express the original signals in the insightful forms

$$
\begin{equation*}
v_{i 1}=v_{i c}+\frac{v_{i d}}{2} \quad v_{i 2}=v_{i c}-\frac{v_{i d}}{2} \tag{4.96}
\end{equation*}
$$

The process is illustrated pictorially in Fig. 4.49. Based in this decomposition, we can now state succinctly that a true differential amplifier responds only to $v_{i d}$, regardless of $v_{i c}$.

In practice, because of unavoidable imbalances in the two circuit halves that are processing $v_{i 1}$ and $v_{i 2}$, a real-life amplifier will be somewhat sensitive also to $v_{i c}$. The small-signal output takes on the more general form

$$
\begin{equation*}
v_{o}=a_{d m} v_{i d}+a_{c m} v_{i c} \tag{4.97}
\end{equation*}
$$

image_name:(a)
description:
[
name: vi1, type: VoltageSource, value: vi1, ports: {Np: vi1, Nn: GND}
name: vi2, type: VoltageSource, value: vi2, ports: {Np: vi2, Nn: GND}
name: Diff amp, type: OpAmp, value: Diff amp, ports: {InP: vi1, InN: vi2, Out: vo}
]
extrainfo:The circuit diagram (a) represents a differential amplifier with two input voltage sources (vi1 and vi2) and a single output (vo). The differential amplifier is designed to amplify the difference between vi1 and vi2.
image_name:(b)
description:
[
name: vic, type: VoltageSource, value: vic, ports: {Np: vic, Nn: GND}
name: vid/2 (positive), type: VoltageSource, value: vid/2, ports: {Np: vi1, Nn: vic}
name: vid/2 (negative), type: VoltageSource, value: vid/2, ports: {Np: vic, Nn: vi2}
name: Diff amp, type: OpAmp, value: Diff amp, ports: {InP: vi1, InN: vi2, Out: vo}
]
extrainfo:The circuit in diagram (b) is a differential amplifier with inputs expressed in terms of their common-mode and differential-mode components. The voltage sources 'vid/2 (positive)' and 'vid/2 (negative)' are used to create the differential input signals from the common-mode input 'vic'.

FIGURE 4.49 Expressing (a) the input signals $v_{i 1}$ and $v_{i 2}$ of a differential amplifier in terms of (b) their common-mode and differential-mode components $v_{i c}$ and $v_{i d}$.
where $a_{d m}$ and $a_{c m}$ are the differential-mode and common-mode gains. Ideally, $a_{c m}$ should be zero, but in practice it will differ from zero, though presumably by very little. To tell how close a practical differential amplifier is to ideal, we use a figure of merit known as the common-mode rejection ratio (CMRR),

$$
\begin{equation*}
\mathrm{CMRR}=\left|\frac{a_{d m}}{a_{c m}}\right| \tag{4.98}
\end{equation*}
$$

In a high-quality differential amplifier this ratio can be rather high, such as $10^{5}$, so CMRR is usually expressed in decibels ( $20 \log 10^{5}=100 \mathrm{~dB}$ ).

Being referenced to ground, both $v_{i 1}$ and $v_{i 2}$ in Fig. 4.49 are said to be single-ended signals. As a signal propagates down a wire or a printed-circuit trace, it tends to pick up all sorts of interference noise from nearby circuits via capacitive and inductive coupling, as well as via the imperfect common ground wire or trace. Consequently, by the time it reaches its destination, the signal may have experienced significant corruption, making recovery of the useful information a formidable task. A clever trick is to work with double-ended signals, where the useful signal is now the voltage difference $v_{i d}$ between a pair of dedicated wires, rather than between a single wire and ground. If these dedicated wires are run in parallel and close to each other, interference with respect to ground will affect them equally, thus appearing as a common-mode component $v_{i c}$. Then, processing a double-ended signal with a high-CMRR difference amplifier will magnify $v_{i d}$ while rejecting $v_{i c}$, thus assuring a high degree of signal integrity.

### CMRR and Input Resistances of the EC Pair

We wish to find the CMRR of the EC pair of Fig. 4.42. With reference to Fig. 4.49b and Eq. (4.97), we proceed in two steps. First, we let $v_{i c}=0$ and find $a_{d m}=v_{o} / v_{i d}$. Then, we let $v_{i d}=0$ and find $a_{c m}=v_{o} / v_{i c}$. Finally, we plug our results into Eq. (4.98).

With $v_{i c}=0$, the circuit of Fig. 4.42 reduces to the ac equivalent of Fig. 4.50a. Looking at the lower portion of the circuit, we can regard $Q_{1}$ and $Q_{2}$ as emitter followers with $Q_{1}$ trying to pull the common emitter voltage $v_{e}$ up, and $Q_{2}$ trying to pull $v_{e}$ down by the same amount. Consequently, $v_{e}$ will remain at ac ground. Also, $v_{o d}$ splits symmetrically between the two halves of the circuit, with $v_{o d} / 2$ appearing
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: vod/2, B: Vid/2, E: vee}
name: Q2, type: NPN, ports: {C: -vod/2, B: -Vid/2, E: vee}
name: RC, type: Resistor, value: RC, ports: {N1: vod/2, N2: GND}
name: RC, type: Resistor, value: RC, ports: {N1: -vod/2, N2: GND}
name: REE, type: Resistor, value: REE, ports: {N1: vee, N2: GND}
name: Vid/2, type: VoltageSource, value: Vid/2, ports: {Np: Vid/2, Nn: GND}
name: Vid/2, type: VoltageSource, value: Vid/2, ports: {Np: -Vid/2, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with two NPN transistors (Q1 and Q2) configured as emitter followers. Each transistor is driven by a differential input voltage (Vid/2 and -Vid/2). The resistors RC are connected between the collector of each transistor and the ground, while REE connects the emitters to ground. The differential output voltage (vod) is taken across the collectors of Q1 and Q2.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: vod/2, B: Vid/2, E: GND}
name: RC, type: Resistor, value: RC, ports: {N1: vod/2, N2: GND}
name: Vid/2, type: VoltageSource, value: Vid/2, ports: {Np: Vid/2, Nn: GND}
]
extrainfo:The circuit is a differential-mode half circuit focusing on the left half of the original differential pair. The common emitter node is at AC ground, rendering the REE resistor ineffective in this configuration.

FIGURE 4.50 (a) Ac circuit to find the differential-mode parameters of the EC pair, and (b) differential-mode half circuit.
at $Q_{1}$ 's collector, and $-v_{o d} / 2$ at $Q_{2}$ 's collector. We can thus focus on just one of the two halves, say, the left half, as shown in Fig. 4.50b. (Note that because the common emitter node is at ac ground, $R_{E E}$ plays no role in this case). This is the familiar CE configuration, for which $v_{o d} / 2=-g_{m}\left(R_{C} / r_{o}\right)\left(v_{i d} / 2\right)$, so

$$
\begin{equation*}
a_{d m}=\frac{v_{o d}}{v_{i d}}=-g_{m}\left(R_{C} / / r_{o}\right) \tag{4.99}
\end{equation*}
$$

This is an already familiar result, but the ability to confirm it via the half-circuit analysis technique offers further insight into balanced operation.

Next, we let $v_{i d}=0$, reducing the circuit of Fig. 4.42 to that of Fig. 4.51a, where the reason for splitting $R_{E E}$ into a pair of $2 R_{E E} \mathrm{~s}$ in parallel will be obvious in a moment. Since the two identical halves are driven by the same voltage $v_{i c}$, the collector voltages will be identical, so we label them with the same symbol $v_{o c}$. Moreover, no current will flow through the wire connecting the two emitters, so we can remove this wire altogether without altering circuit operation, and focus on just one half of the circuit, say, the left half, as shown in Fig. 4.51b. This is the familiar CE-ED configuration for which we readily find

$$
\begin{equation*}
a_{c m}=\frac{v_{o c}}{v_{i c}}=-\frac{g_{m} R_{C}}{1+2 g_{m} R_{E E}} \tag{4.100}
\end{equation*}
$$

(In this case $r_{o}$ has been ignored altogether as emitter degeneration raises its effective value dramatically.)

Depending on the intended use of the differential pair outputs, we have two possibilities:

- The output is taken single-endedly from either one of the two collectors. In this case the CMRR is the ratio of one-half the gain of Eq. (4.99) to that of Eq. (4.100). If we ignore $r_{o}$, this ratio simplifies as
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: voc, B: Vic, E: X1}
name: Q2, type: NPN, ports: {C: voc, B: Vic, E: X1}
name: RC, type: Resistor, value: RC, ports: {N1: voc, N2: GND}
name: RC, type: Resistor, value: RC, ports: {N1: voc, N2: GND}
name: 2REE, type: Resistor, value: 2REE, ports: {N1: X1, N2: GND}
name: 2REE, type: Resistor, value: 2REE, ports: {N1: X1, N2: GND}
name: Vic, type: VoltageSource, value: Vic, ports: {Np: Vic, Nn: GND}
]
extrainfo:The circuit (a) is a differential pair with emitter degeneration using two NPN transistors Q1 and Q2. The output is taken single-endedly from the collector of each transistor. The resistors RC and 2REE provide load and emitter degeneration, respectively. The common-mode rejection ratio (CMRR) is a key parameter for this circuit.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: voc, B: Vic, E: X1}
name: RC, type: Resistor, value: RC, ports: {N1: voc, N2: GND}
name: 2REE, type: Resistor, value: 2REE, ports: {N1: X1, N2: GND}
name: Vic, type: VoltageSource, value: Vic, ports: {Np: Vic, Nn: GND}
]
extrainfo:The circuit is a common-mode half circuit of a differential pair with emitter degeneration, used to analyze common-mode rejection ratio (CMRR). It consists of an NPN transistor Q1, a collector resistor RC, and an emitter degeneration resistor 2REE. The voltage source Vic provides the input signal.

FIGURE 4.51 (a) Ac circuit to find the common-mode parameters of the EC pair, and (b) common-mode half circuit.

$$
\begin{equation*}
\mathrm{CMRR} \cong \frac{1}{2}+g_{m} R_{E E} \cong g_{m} R_{E E} \tag{4.101}
\end{equation*}
$$

- The output is taken differentially, that is, between the two collectors. Since their voltage difference is zero regardless of $v_{i c}$, then $a_{c m}=\left(v_{o 1}-v_{o 2}\right) / v_{i c}=0$ in this case, so Eq. (4.98) gives

$$
\begin{equation*}
\mathrm{CMRR}=\infty \tag{4.102}
\end{equation*}
$$

This last result predicates two perfectly balanced circuit halves. In practice, unavoidable mismatches between the two halves will result in a non-infinite CMRR, as we shall see shortly.

An EC pair is fully characterized once we know also its differential-mode and common-mode input resistances $R_{i d}$ and $R_{i c}$. With reference to Fig. $4.50 b$, we have, by inspection, $R_{i d} / 2=r_{\pi}$, so the overall resistance between the inputs of the EC pair is the sum of the two halves, or

$$
\begin{equation*}
R_{i d}=2 r_{\pi} \tag{4.103}
\end{equation*}
$$

On the other hand, the resistance between either input and ground is, from Fig. 4.51b,

$$
\begin{equation*}
R_{i c}=r_{\pi}+2\left(\beta_{0}+1\right) R_{E E} \tag{4.104}
\end{equation*}
$$

This may be truly large, in which case it may be advisable to take $r_{\mu}$ into account.
(a) In the bipolar pair of Fig. 4.42 let $V_{C C}=-V_{E E}=5 \mathrm{~V}, I_{E E}=0.2 \mathrm{~mA}$, $R_{C}=30 \mathrm{k} \Omega$, and $R_{E E}=500 \mathrm{k} \Omega$. If $\beta_{0}=200, V_{A}=75 \mathrm{~V}$, and $r_{\mu}=1000 r_{o}$, find $a_{d m}, a_{c m}$, CMRR (in dB), $R_{i d}$, and $R_{i c}$.
(b) Suppose the inputs are tied together and driven by a common-mode voltage $v_{I C}$. Assuming $V_{B E(\mathrm{on})}=0.6 \mathrm{~V}$ and $V_{C E(\mathrm{EOS})}=0.2 \mathrm{~V}$, find the maximum value of $v_{I C}$ for which the BJTs are still operating in the forward-active region.

#### Solution

(a) We have $I_{C} \cong I_{E E} / 2=0.2 / 2=0.1 \mathrm{~mA}, g_{m}=0.1 / 26=1 /(260 \Omega), r_{\pi}=$ $200 \times 260=52 \mathrm{k} \Omega, r_{o}=75 / 0.1=750 \mathrm{k} \Omega$, and $r_{\mu}=750 \mathrm{M} \Omega$. Then, $a_{d m}=-(30 / / 750) / 0.260=-111 \mathrm{~V} / \mathrm{V}, a_{c m}=-(30 / 0.26) /(1+2 \times 500 / 0.26)=$ -0.03 V/V, single-ended CMRR $=500 / 0.260=1923=65.7 \mathrm{~dB}$, differential CMRR $=\infty, R_{i d}=2 \times 52=104 \mathrm{k} \Omega$, and $R_{i c} \cong(0.52+2 \times 201 \times$ $0.5) / / 750=201 / / 750=159 \mathrm{M} \Omega$ ( $r_{\mu}$ has negligible impact).
(b) At dc balance we have $V_{C}=5-30 \times 0.1=2 \mathrm{~V}$. To bring the BJTs to the edge of saturation we need to raise their common emitter voltage to $V_{E}=$ $V_{C}-V_{C E(\mathrm{EOS})}=2-0.2=1.8 \mathrm{~V}$. Consequently, $v_{I C(\max )}=V_{E}+V_{B E(\mathrm{on})}=$ $1.8+0.6 \mathrm{~V}=2.4 \mathrm{~V}$.

### CMRR of the SC Pair

The half-circuit analysis technique applied to bipolar pairs holds for MOS pairs just as well. These circuits are shown in Fig. 4.52, and their similarity to their bipolar counterparts indicates that we can reuse a good deal of already familiar insight and equations. Thus, the half circuit of Fig. $4.52 a$ gives

$$
\begin{equation*}
a_{d m}=\frac{v_{o d}}{v_{i d}}=-g_{m}\left(R_{D} / / r_{o}\right) \tag{4.105}
\end{equation*}
$$

Likewise, the half circuit of Fig. $4.52 b$ gives, by Eq. (4.39a),

$$
\begin{equation*}
a_{c m}=\frac{v_{o c}}{v_{i c}}=-\frac{g_{m} R_{D}}{1+2\left(g_{m}+g_{m b}\right) R_{S S}+\left(R_{D}+2 R_{S S}\right) / r_{o}} \tag{4.106}
\end{equation*}
$$

image_name:(a)
description:
[
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: VOD/2}
name: M1, type: NMOS, ports: {S: GND, D: VOD/2, G: VID/2}
name: Vid/2, type: VoltageSource, value: Vid/2, ports: {Np: VID/2, Nn: GND}
]
extrainfo:This circuit is a half-circuit used to find the differential-mode gain of an SC pair. It includes a resistor RD connected to the drain of an NMOS transistor M1, with a voltage source Vid/2 applied to the gate of M1. The output voltage is taken across the resistor RD.

(a)
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: x, D: voc, G: Vic}
name: RD, type: Resistor, value: RD, ports: {N1: x, N2: GND}
name: 2RSS, type: Resistor, value: 2RSS, ports: {N1: x, N2: GND}
name: vic, type: VoltageSource, value: vic, ports: {Np: Vic, Nn: GND}
]
extrainfo:This circuit is a half-circuit used to find the common-mode gain of an SC pair. It includes a resistor RD connected to the drain of an NMOS transistor M1, with a voltage source vic applied to the gate of M1. The output voltage is taken across the resistor RD.

FIGURE 4.52 Half circuits to find the (a) differentialmode gain and (b) common-mode gain of an SC pair.

where $g_{m b}$ is the body transconductance. For single-ended utilization, the CMRR is the ratio of one-half the gain of Eq. (4.105) to that of Eq. (4.106). If $r_{o}$ is sufficiently large, we can approximate

$$
\begin{equation*}
\mathrm{CMRR} \cong \frac{1}{2}+\left(g_{m}+g_{m b}\right) R_{S S} \cong\left(g_{m}+g_{m b}\right) R_{S S} \tag{4.107}
\end{equation*}
$$

For differential output utilization we have

$$
\begin{equation*}
\mathrm{CMRR}=\infty \tag{4.108}
\end{equation*}
$$

An advantage of FETs compared to BJTs is that

$$
\begin{equation*}
R_{i d}=R_{i c}=\infty, \tag{4.109}
\end{equation*}
$$

(a) In the MOS pair of Fig. 4.45 let $V_{D D}=-V_{E E}=2.5 \mathrm{~V}, I_{S S}=0.2 \mathrm{~mA}$, $R_{D}=10 \mathrm{k} \Omega$, and $R_{S S}=1 \mathrm{M} \Omega$. If the FETs have $k=1.25 \mathrm{~mA} / \mathrm{V}^{2}, V_{t}=0.4 \mathrm{~V}$, $\chi=0.2$, and $\lambda=1 /(10 \mathrm{~V})$, find $a_{d m}, a_{c m}$, and CMRR.
(b) If the inputs are tied together and driven by a common-mode voltage $v_{I C}$, what is the maximum value of $v_{I C}$ for which the FETs will still operate in saturation?

#### Solution

(a) We have $I_{D} \cong I_{S S} / 2=0.2 / 2=0.1 \mathrm{~mA}, g_{m}=\left(2 k I_{D}\right)^{1 / 2}=(2 \times 1.25 \times 0.1)^{1 / 2}=$ $0.5 \mathrm{~mA} / \mathrm{V}, r_{o}=1 /\left(\lambda I_{D}\right)=10 / 0.1=100 \mathrm{k} \Omega ; a_{d m}=-0.5 \times(10 / / 100)=-4.55 \mathrm{~V} / \mathrm{V}$, $a_{c m}=-0.5 \times 10 /[1+2(1.2 \times 0.5 \times 1000)+(10+2000) / 100]=$ $-4.1 \times 10^{-3} \mathrm{~V} / \mathrm{V}$; single-ended CMRR $=0.5 \times 1.2 \times 1000=600=55.6 \mathrm{~dB}$, differential CMRR $=\infty$.
(b) At dc balance we have $V_{D}=2.5-10 \times 0.1=1.5 \mathrm{~V}$. To bring the FETs to the edge of saturation we need to raise $v_{I C}$ till $V_{D S}=V_{O V}$, or $V_{S}=V_{D}-V_{O V}$. The corresponding input, denoted as $v_{I C(\max )}$, is such that $v_{I C(\max )}=V_{S}+$ $\left(V_{t}+V_{O V}\right)=V_{D}-V_{O V}+V_{t}+V_{O V}=V_{D}+V_{t}=1.5 \mathrm{~V}+0.4=1.9 \mathrm{~V}$.

### Effect of Mismatches on the CMRR

With perfectly matched halves, the collector resistors drop identical voltages in Fig. 4.53a, so the collector signals cancel each other out exactly to give $a_{c m}=$ $\left(v_{o 1}-v_{o 2}\right) / v_{i c}=0 / v_{i c}=0$, and therefore CMRR $=\infty$, by Eq. (4.98). (Similar considerations hold in the MOS circuit of Fig. $4.53 b$, so the following analysis applies both to the EC and SC pairs.) In practice, the two halves of a differential pair are likely to be mismatched, even if only slightly, so it is of interest to investigate the impact on the CMRR. The two main factors to be considered are (a) mismatched
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: vo1, B: Vic, E: P}
name: Q2, type: NPN, ports: {C: vo2, B: Vic, E: P}
name: RC1, type: Resistor, value: RC1, ports: {N1: vo1, N2: GND}
name: RC2, type: Resistor, value: RC2, ports: {N1: vo2, N2: GND}
name: REE, type: Resistor, value: REE, ports: {N1: P, N2: GND}
name: vic, type: VoltageSource, value: vic, ports: {Np: Vic, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with mismatched collector resistances (RC1 and RC2) and transconductances (gm1 and gm2) affecting the CMRR. The diagram is labeled (a) and focuses on analyzing the effect of these mismatches.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: e1e2, D: vo1, G: Vic}
name: M2, type: NMOS, ports: {S: e1e2, D: vo2, G: Vic}
name: RD1, type: Resistor, value: RD1, ports: {N1: vo1, N2: GND}
name: RD2, type: Resistor, value: RD2, ports: {N1: vo2, N2: GND}
name: RSS, type: Resistor, value: RSS, ports: {N1: e1e2, N2: GND}
name: vic, type: VoltageSource, value: vic, ports: {Np: Vic, Nn: GND}
]
extrainfo:The circuit diagram shows a differential pair using NMOS transistors M1 and M2 with resistive loads RD1 and RD2. The voltage source vic provides the input common-mode voltage Vic. The resistors RSS provide source degeneration for the MOS transistors. The circuit is used to investigate the effect of mismatches in RD and gm on the common-mode rejection ratio (CMRR).

FIGURE 4.53 Ac circuits to investigate the effect of $R$ and $g_{m}$ mismatches upon the CMRR.
collector resistances $R_{C 1}$ and $R_{C 2}$, and (b) mismatched BJT transconductances $g_{m 1}$ and $g_{m 2}$. We assume that these mismatches are small enough that we can still approximate

$$
\begin{equation*}
a_{d m}=\frac{v_{o d}}{v_{i d}} \cong-g_{m} R_{C} \tag{4.110}
\end{equation*}
$$

with $g_{m}$ and $R_{C}$ representing the average values of the transconductances and resistances,

$$
g_{m}=\frac{g_{m 1}+g_{m 2}}{2} \quad R_{C}=\frac{R_{C 1}+R_{C 2}}{2}
$$

Moreover, with sufficiently small mismatches in Fig. 4.53a, we can still approximate

$$
\begin{equation*}
a_{c m}=\frac{v_{o 1}-v_{o 2}}{v_{i c}} \cong-\frac{g_{m 1} R_{C 1}-g_{m 2} R_{C 2}}{1+2 g_{m} R_{E E}} \tag{4.111}
\end{equation*}
$$

If we introduce the differences

$$
\Delta g_{m}=g_{m 1}-g_{m 2} \quad \Delta R_{C}=R_{C 1}-R_{C 2}
$$

then it is readily seen that the individual transconductances and resistances can be expressed as

$$
\begin{array}{rlr}
g_{m 1} & =g_{m}+\frac{\Delta g_{m}}{2} & g_{m 2}=g_{m}-\frac{\Delta g_{m}}{2} \\
R_{C 1} & =R_{C}+\frac{\Delta R_{C}}{2} & R_{C 2}=R_{C}-\frac{\Delta R_{C}}{2}
\end{array}
$$

Substituting into Eq. (4.111) gives

$$
a_{c m} \cong-\frac{\left(g_{m}+\frac{\Delta g_{m}}{2}\right)\left(R_{C}+\frac{\Delta R_{C}}{2}\right)-\left(g_{m}-\frac{\Delta g_{m}}{2}\right)\left(R_{C}-\frac{\Delta R_{C}}{2}\right)}{1+2 g_{m} R_{E E}}
$$

Expanding and ignoring higher-order terms ( $\Delta$-term products or squares), we get, after simplifying,

$$
\begin{equation*}
a_{c m} \cong-\frac{g_{m} \Delta R_{C}+\Delta g_{m} R_{C}}{1+2 g_{m} R_{E E}} \tag{4.112}
\end{equation*}
$$

Finally, substituting Eqs. (4.112) and (4.110) into Eq. (4.98) gives

$$
\begin{equation*}
\mathrm{CMRR} \cong \frac{1+2 g_{m} R_{E E}}{\Delta R_{C} / R_{C}+\Delta g_{m} / g_{m}} \tag{4.113}
\end{equation*}
$$

The above equations refer to the worst-case scenario in which the mismatches conspire to reinforce each other. However, the two causes of mismatch are usually uncorrelated, so a more realistic estimate for the CMRR of the EC pair is found as ${ }^{1}$

$$
\begin{equation*}
\mathrm{CMRR}_{(\mathrm{BJT})} \cong \frac{1+2 g_{m} R_{E E}}{\sqrt{\left(\Delta R_{C} / R_{C}\right)^{2}+\left(\Delta g_{m} / g_{m}\right)^{2}}} \tag{4.114a}
\end{equation*}
$$

We can readily adapt this expression to the SC pair of Fig. $4.53 b$ by writing

$$
\begin{equation*}
\mathrm{CMRR}_{(\mathrm{MOS})} \cong \frac{1+2\left(g_{m}+g_{m b}\right) R_{S S}}{\sqrt{\left(\Delta R_{D} / R_{D}\right)^{2}+\left(\Delta g_{m} / g_{m}\right)^{2}}} \tag{4.114b}
\end{equation*}
$$

It is apparent that for given amounts of mismatch, the CMRR is approximately proportional to the equivalent resistance $R_{E E}$ or $R_{S S}$ presented by the biasing current sink. To ensure high CMRR values, this source is typically a high output-resistance source, such as a cascode source or other source types to be investigated in Section 4.8.
(a) Suppose the $g_{m}$ 's in an SC pair are in the range of $100 \pm 10 \mu \mathrm{~A} / \mathrm{V}$, and the drain resistances have tolerances of $\pm 5 \%$. If $\chi=0.15$ and $R_{S S}=500 \mathrm{k} \Omega$, estimate the worst-case scenario CMRR. What if the tolerances are uncorrelated?
(b) Find the value of $R_{S S}$ needed to ensure CMRR $\geq 60 \mathrm{~dB}$.

#### Solution

(a) By inspection, $\Delta R_{D} / R_{D}=0.1$. We also have $g_{m}+g_{m b}=(1+\chi) g_{m}=$ $115 \mu \mathrm{~A} / \mathrm{V}, \Delta g_{m}=20 \mu \mathrm{~A} / \mathrm{V}$, and $\Delta g_{m} / g_{m}=20 / 100=0.2$. In the worst-case scenario,

$$
\mathrm{CMRR} \cong \frac{1+2(115) 10^{-6} \times 500 \times 10^{3}}{0.1+0.2}=\frac{116}{0.3}=387=51.7 \mathrm{~dB}
$$

If the mismatches are uncorrelated, then use Eq. (4.114b) and write

$$
\mathrm{CMRR} \cong \frac{116}{\sqrt{0.1^{2}+0.2^{2}}}=\frac{116}{0.224}=519=54.3 \mathrm{~dB}
$$

(b) To raise CMRR to 60 dB , or 1,000 , we need to increase $R_{S S}$ in proportion, that is, $R_{S S}=(500 \mathrm{k} \Omega) \times(1000 / 519)=964 \mathrm{k} \Omega$.

## 4.7 INPUT OFFSET VOLTAGE/CURRENT IN DIFFERENTIAL PAIRS

If we ground both inputs of a differential pair, as depicted in Fig. 4.54 for a bipolar pair, we expect $V_{O}=0$. However, because of fabrication process variations, the two halves of the circuit are likely to be somewhat mismatched, resulting in an output error $E_{O} \neq 0$. We can visualize the effect of mismatches as a shift in the VTC of Fig. $4.44 b$ either to the right or to the left, depending on the direction of the mismatch. If we want to drive the output to zero we need to apply a corrective input voltage that will offset the VTC in the opposite direction until it goes through the origin. This corrective voltage is the input offset voltage $V_{o S}$ depicted in Fig. 4.54b. By inspection, we find $V_{O S}$ by reflecting the negative of $E_{O}$ to the input, or

$$
\begin{equation*}
V_{o S}=\frac{E_{O}}{-a_{d m}} \tag{4.115}
\end{equation*}
$$

where $a_{d m}$ is the differential-mode gain of the pair under consideration.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: Eo+, B: GND, E: P}
name: Q2, type: NPN, ports: {C: Eo-, B: GND, E: P}
name: RC1, type: Resistor, value: RC1, ports: {N1: VCC, N2: EO+}
name: RC2, type: Resistor, value: RC2, ports: {N1: VCC, N2: EO-}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: P, Nn: VEE}
]
extrainfo:The circuit is a differential amplifier with two NPN transistors. The output error voltage EO is present when the inputs are grounded. The input offset voltage VOS is used to nullify EO.
image_name:(b)
description:
[
name: RC1, type: Resistor, value: RC1, ports: {N1: VCC, N2: Q1_C}
name: RC2, type: Resistor, value: RC2, ports: {N1: VCC, N2: Q2_C}
name: Q1, type: NPN, ports: {C: Q1_C, B: VOS, E: P}
name: Q2, type: NPN, ports: {C: Q2_C, B: GND, E: P}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: P, Nn: VEE}
name: VEE, type: VoltageSource, value: VEE, ports: {Np: VEE, Nn: GND}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: VOS, type: VoltageSource, value: VOS, ports: {Np: VOS, Nn: GND}
]
extrainfo:The circuit diagram (b) represents a differential amplifier with input offset voltage VOS applied to nullify the output error EO. The NPN transistors Q1 and Q2 form the differential pair, with mismatched collector resistances RC1 and RC2 potentially contributing to the input offset voltage.

FIGURE 4.54 (a) A practical EC pair with grounded inputs generally gives an output error $E_{O} \neq 0$. (b) $V_{O S}$ is defined as the input voltage required to null $E_{0}$.

### Input Offset Voltage of the EC Pair

Two main factors contribute to the $V_{O S}$ of an EC pair: (a) mismatched collector resistances $R_{C 1}$ and $R_{C 2}$, and (b) mismatched saturation currents $I_{s 1}$ and $I_{s 2}$ of the BJTs. By Eq. (2.11), mismatches between $I_{s 1}$ and $I_{s 2}$ stem, in turn, from mismatches between the emitter areas $A_{E 1}$ and $A_{E 2}$ and between the base widths $W_{B 1}$ and $W_{B 2}$, as well as differences in the base-region doping densities and in the individual temperatures of the two devices. Moreover, because of the Early effect, $W_{B 1}$ and $W_{B 2}$ depend on the voltages $V_{C E 1}$ and $V_{C E 2}$, so even two BJTs fabricated perfectly identical will exhibit saturation-current mismatches if operated at different $V_{C E}$ values.

- To investigate the effect of mismatched $R_{C 1}$ and $R_{C 2}$, assume the BJTs are perfectly matched so that in the circuit of Fig. $4.54 a$ we have $I_{C 1}=I_{C 2} \cong I_{E E} / 2$. The contribution to $E_{O}$ is

$$
E_{O 1}=V_{C C}-R_{C 1} I_{C 1}-\left(V_{C C}-R_{C 2} I_{C 2}\right)=-\Delta R_{C} \frac{I_{E E}}{2}
$$

where $\Delta R_{C}=R_{C 1}-R_{C 2}$. Dividing by $-a_{d m} \cong g_{m} R_{C}$, with $R_{C}$ representing the mean value of the two resistances, or $R_{C}=\left(R_{C 1}+R_{C 2}\right) / 2$, and $g_{m}=\left(I_{E E} / 2\right) / V_{T}$, we get

$$
\begin{equation*}
V_{O S 1} \cong-V_{T} \frac{\Delta R_{C}}{R_{C}} \tag{4.116}
\end{equation*}
$$

- To investigate the effect of mismatched $I_{s 1}$ and $I_{s 2}$, assume the resistances are now perfectly matched. Since the BJTs of Fig. $4.54 a$ experience the same drive $V_{B E}$, the current $I_{E E}$ must split between $Q_{1}$ and $Q_{2}$ in proportion to $I_{s 1}$ and $I_{s 2}$,

$$
I_{C 1} \cong \frac{I_{E E}}{2}\left(1+\frac{\Delta I_{s}}{2 I_{s}}\right) \quad I_{C 2} \cong \frac{I_{E E}}{2}\left(1-\frac{\Delta I_{s}}{2 I_{s}}\right)
$$

where $\Delta I_{s}=I_{s 1}-I_{s 2}$ and $I_{s}=\left(I_{s 1}+I_{s 2}\right) / 2$, as usual. The contribution to $E_{O}$ is now

$$
E_{O 2}=V_{C C}-R_{C} I_{C 1}-\left(V_{C C}-R_{C} I_{C 2}\right)=-R_{C} \frac{I_{E E}}{2} \frac{\Delta I_{s}}{I_{s}}
$$

Again dividing by $-a_{d m}$ we get

$$
\begin{equation*}
V_{O S 2} \cong-V_{T} \frac{\Delta I_{s}}{I_{s}} \tag{4.117}
\end{equation*}
$$

Note that the negative signs in Eqs. (4.116) and (4.117) are not relevant because a mismatch can occur in either direction, depending on the random variation of the fabrication process. It is thus customary to drop the sign and to express $V_{O S}$ always as a positive number. In general the two causes of offset voltage are uncorrelated, so the total offset voltage is usually estimated as ${ }^{1}$

$$
\begin{equation*}
V_{o s} \cong V_{T} \sqrt{\left(\frac{\Delta R_{C}}{R_{C}}\right)^{2}+\left(\frac{\Delta I_{s}}{I_{s}}\right)^{2}} \tag{4.118}
\end{equation*}
$$

Suppose the EC pair of Example 4.18 is implemented with resistances afflicted by $\pm 5 \%$ tolerances and with BJTs whose saturation currents are afflicted by $\pm 10 \%$ tolerances. Estimate $V_{O S}$ and $E_{O}$.

#### Solution

We have $\Delta R_{C} / R_{C}=0.1$ and $\Delta I_{s} / I_{s}=0.2$. Applying Eq. (4.118) gives

$$
V_{O S} \cong(26 \mathrm{mV}) \sqrt{(0.1)^{2}+(0.2)^{2}}=5.8 \mathrm{mV}
$$

Note that $V_{O S}$ may be positive or negative, depending on the direction of the mismatch. $E_{O}=\left|a_{d m}\right| V_{O S}=111 \times 5.8=644 \mathrm{mV}$.

### Input Bias Current and Offset Current of the EC Pair

When an EC pair is driven by sources having nonzero series resistances it is of interest to know the currents into the bases of the BJTs because these currents flow through the source resistances, causing voltage drops that may upset the dc balance of the pair appreciably. With perfectly matched devices, the base currents are $I_{B 1}=I_{B 2}=I_{B}$, where

$$
\begin{equation*}
I_{B}=\frac{I_{E E}}{2\left(\beta_{F}+1\right)} \tag{4.119}
\end{equation*}
$$

However, any mismatches in the $\beta_{F} \mathrm{~s}$ of the two BJTs will cause mismatches in the base currents. If we define the input bias current $I_{B}$ and the input offset current $I_{O S}$ of an EC pair as

$$
\begin{equation*}
I_{B}=\frac{I_{B 1}+I_{B 2}}{2} \quad I_{O S}=I_{B 1}-I_{B 2} \tag{4.120}
\end{equation*}
$$

then a beta mismatch $\Delta \beta_{F}$ will result in $I_{O S} \neq 0$. The two are related as

$$
\begin{equation*}
I_{O S} \cong-I_{B} \frac{\Delta \beta_{F}}{\beta_{F}} \tag{4.121}
\end{equation*}
$$

where $\beta_{F}=\left(\beta_{F 1}+\beta_{F 2}\right) / 2$, as usual. For instance, with a $10 \%$ beta mismatch, $I_{O S}$ is $10 \%$ of $I_{B}$.

### Input Offset Voltage of the SC Pair

Three main factors contribute to $V_{O S}$ in the case of an SC pair: (a) mismatched drain resistances $R_{D 1}$ and $R_{D 2},(b)$ mismatched device transconductance parameters $k_{1}$ and $k_{2}$, and (c) mismatched threshold voltages $V_{t 1}$ and $V_{t 2}$. By Eqs. (3.13) and (3.14), mismatches between $k_{1}$ and $k_{2}$ stem, in turn, from mismatches between the ratios $W_{1} / L_{1}$ and $W_{2} / L_{2}$ as well as variations in the oxide thickness $t_{o x}$ and temperature gradients from one device to the other. By Eqs. (3.7) through (3.9), mismatches between $V_{t 1}$ and $V_{t 2}$ are the result of differences in the implant densities, oxide thickness, and temperature of the two devices. Finally, because of the channel-length modulation effect, $L_{1}$ and $L_{2}$ depend on
the voltages $V_{D S 1}$ and $V_{D S 2}$, so even two FETs fabricated perfectly identical will exhibit transconductance-parameter mismatches if operated at different $V_{D S}$ values.

- To investigate the effect of mismatched $R_{D 1}$ and $R_{D 2}$, proceed as in the bipolar case and write

$$
E_{O 1} \cong-\Delta R_{D} \frac{I_{S S}}{2}
$$

where $\Delta R_{D}=R_{D 1}-R_{D 2}$. Dividing by $-a_{d m} \cong g_{m} R_{D}$, with $R_{D}$ representing the mean value of the two resistances, or $R_{D}=\left(R_{D 1}+R_{D 2}\right) / 2$, and with $g_{m}=$ $2\left(I_{S S} / 2\right) / V_{O V}=I_{S S} / V_{O V}$, we get

$$
\begin{equation*}
V_{O S 1} \cong-\frac{V_{O V}}{2} \frac{\Delta R_{D}}{R_{D}} \tag{4.122}
\end{equation*}
$$

where $V_{O V}$ is the dc-balance overdrive voltage of Eq. (4.81).

- To investigate the effect of mismatched $k_{1}$ and $k_{2}$ assume the resistances as now perfectly matched and the FETs have identical threshold voltages. Since the FETs of Fig. 4.55a are subject to the same overdrive voltage $V_{O V}$, the current $I_{S S}$ must split between $M_{1}$ and $M_{2}$ in proportion to $k_{1}$ and $k_{2}$,

$$
I_{D 1}=\frac{I_{S S}}{2}\left(1+\frac{\Delta k}{2 k}\right) \quad I_{D 2}=\frac{I_{S S}}{2}\left(1-\frac{\Delta k}{2 k}\right)
$$

where $\Delta k=k_{1}-k_{2}$ and $k=\left(k_{1}+k_{2}\right) / 2$. Consequently,

$$
E_{O 2}=V_{D D}-R_{D} I_{D 1}-\left(V_{D D}-R_{D} I_{D 2}\right)=-R_{D} \frac{I_{S S}}{2} \frac{\Delta k}{k}
$$

image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: Eo+, G: GND}
name: M2, type: NMOS, ports: {S: P, D: Eo-, G: GND}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: Eo+}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: Eo-}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: GND}
name: VSS, type: VoltageSource, value: VSS, ports: {Np: P, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with a current source ISS providing bias. M1 and M2 are NMOS transistors forming a differential pair. RD1 and RD2 are load resistors connected to VDD. VSS is the negative supply voltage.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: P, D: RD1, G: VOS}
name: M2, type: NMOS, ports: {S: P, D: RD2, G: P}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: RD1}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: RD2}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: VSS}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: VSS, type: VoltageSource, value: VSS, ports: {Np: GND, Nn: VSS}
name: VOS, type: VoltageSource, value: VOS, ports: {Np: VOS, Nn: GND}
]
extrainfo:The circuit is a differential pair with NMOS transistors M1 and M2. VOS is used to null the output error EO. ISS provides a constant current source to the circuit. RD1 and RD2 are load resistors connected to VDD.

FIGURE 4.55 (a) A practical SC pair with grounded inputs generally gives an output error $E_{O} \neq 0$. (b) $V_{\text {os }}$ is defined as the input voltage required to null $E_{0}$.

Again dividing by $-a_{d m} \cong g_{m} R_{D}$, we get

$$
\begin{equation*}
V_{O S 2} \cong-\frac{V_{O V}}{2} \frac{\Delta k}{k} \tag{4.123}
\end{equation*}
$$

- To investigate the effect of mismatched $V_{t 1}$ and $V_{t 2}$, assume all other parameters are matched. Then, to achieve the dc balance of Fig. $4.55 b$, we must ensure that the FETs experience identical overdrive voltages. This occurs for

$$
\begin{equation*}
V_{O S 3}=\Delta V_{t}=V_{t 1}-V_{t 2} \tag{4.124}
\end{equation*}
$$

Note the similarity of the MOS Eqs. (4.122) and (4.123) to the BJT Eqs. (4.116) and (4.117), except that we now have $V_{O V} / 2$ in place of $V_{T}$. Since $V_{T}=26 \mathrm{mV}$ whereas $V_{O V} / 2$ is typically at least an order of magnitude higher, it is apparent that SC pairs tend to exhibit larger offsets than BJT pairs.

As in the bipolar case, the signs of the various offset components are not relevant. Moreover, the three causes of offset voltage are not correlated, so the total offset voltage is usually estimated as ${ }^{1}$

$$
\begin{equation*}
V_{O S} \cong \frac{V_{O V}}{2} \sqrt{\left(\frac{\Delta R_{D}}{R_{D}}\right)^{2}+\left(\frac{\Delta k}{k}\right)^{2}+\left(\frac{\Delta V_{t}}{0.5 V_{O V}}\right)^{2}} \tag{4.125}
\end{equation*}
$$

Finally, since the gate current of a MOSFET is zero at dc, the input bias current and input offset current are non-issues in SC pairs. When the input terminals are made externally accessible, they are equipped with internal diode clamps to prevent electric discharge that might damage the dielectric of the FETs. In normal operation these diodes are reverse biased, so the gate-terminal currents are those of reverse-biased pn junctions. At room temperature these currents are very small (in the nA or even pA range), but as we know, they double for about every $10^{\circ} \mathrm{C}$ of temperature increase.

EXAMPLE 4.22 Suppose an SC pair is afflicted by an $R_{D}$ mismatch of $\pm 1 \%$, a $k$ mismatch of $\pm 3 \%$, and a $V_{t}$ mismatch of $\pm 5 \mathrm{mV}$. If $V_{O V}=0.5 \mathrm{~V}$, estimate the worst-case value as well as the likely value of $V_{O S}$. Which is the major contributor to $V_{O S}$ ?

#### Solution

Summing the various terms directly gives the worst-case scenario estimate,

$$
V_{O S} \cong \frac{500 \mathrm{mV}}{2}\left(\frac{2}{100}+\frac{6}{100}+\frac{10}{250}\right)=5+15+10=30 \mathrm{mV}
$$

Using Eq. (4.125), we find the likely estimate

$$
V_{O S} \cong \sqrt{5^{2}+15^{2}+10^{2}}=18.7 \mathrm{mV}
$$

In this example the main culprit is the $k$ mismatch.

### Input Offset Voltage Drift

Like virtually all device and circuit parameters, $V_{O S}$ drifts with temperature, and in low-level signal processing, such as in instrumentation and measurement, it is necessary to know both $V_{O S}$ and its thermal drift.

In the case of EC pairs, Eq. (4.118) indicates that $V_{O S}$ is proportional to the thermal voltage $V_{T}$, which in turn is proportional to temperature $T$. Consequently,

$$
\begin{equation*}
\frac{d V_{O S}}{d T}=\frac{V_{O S}}{T} \tag{4.126}
\end{equation*}
$$

At room temperature ( $T=300 \mathrm{~K}$ ), $V_{o S}$ drifts by $1 \times 10^{-3} / 300=3.3 \mu \mathrm{~V} /{ }^{\circ} \mathrm{C}$ for every mV of offset. So, for an EC pair with $V_{O S}=1.5 \mathrm{mV}, V_{O S}$ drifts by $5 \mu \mathrm{~V} /{ }^{\circ} \mathrm{C}$.

The offset drift of SC pairs is more complex ${ }^{1,3}$ than in the bipolar case. Suffice it to say here that CMOS IC designers continuously strive to reduce both $V_{O S}$ and its drift using clever compensation techniques such as autozero techniques and floatinggate programming.

## 4.8 CURRENT MIRRORS

Along with differential pairs, current mirrors are the workhorses of analog ICs. A common current mirror application is the generation of stable and predictable dc currents to bias other circuits. When used in this capacity, a current mirror is also referred to as a current reference. Mirrors are also used to steer current signals. As such they find application as active loads in a variety of analog signal processing ICs such as operational amplifiers (op amps), current-feedback amplifiers (CFAs), and operational transconductance amplifiers (OTAs). Current mirroring is made possible by the high degree of matching and thermal tracking of transistors fabricated in close proximity of each other on the same chip.

The function of a current mirror is to accept a current $i_{I}$ at a low (ideally zero) input-resistance terminal, and deliver a current $i_{O}\left(=i_{I}\right)$ at a high (ideally infinite) output-resistance terminal. The current mirror is similar to the current buffer, except that both currents flow into (or out of) the circuit. For this reason, a current mirror is also said to provide current reversal. We have already been exposed to current mirrors in the introductory chapters on BJTs and MOSFETs, as well as in Section 4.1. We now wish to examine them in systematic detail.

### Basic Bipolar Current Mirrors

Shown in Fig. 4.56a is the basic bipolar current mirror. As the input source $i_{I}$ is turned on, the diode-connected transistor $Q_{1}$ develops a voltage drop $v_{B E}$ related to $i_{I}$ by the well-known logarithmic law. But $Q_{2}$ is subjected to the same drive $v_{B E}$ as $Q_{1}$, so $Q_{2}$ will just mirror the current of $Q_{1}$. We wish to find a precise relationship between $i_{o}$ and $i_{l}$, as well as the small-signal input and output resistances $R_{i}$ and $R_{o}$. We also wish to display the $i-v$ characteristic of the output port.
image_name:(a) Basic BJT current mirror
description:
[
name: Q1, type: NPN, ports: {C: VBE+, B: VBE+, E: GND}
name: Q2, type: NPN, ports: {C: Vo, B: VBE+, E: GND}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: iI, type: CurrentSource, value: iI, ports: {Np: VCC, Nn: Vi}
]
extrainfo:The circuit is a basic BJT current mirror. Both transistors Q1 and Q2 are NPN and share the same base-emitter voltage VBE+. The current source iI provides the input current which is mirrored by the transistors to provide the output current iO through the load. The resistors Ri and Ro are connected to the input and output nodes respectively.
image_name:(b) output-port i-v characteristic
description:### Type of Graph and Function:
The graph represents the **output-port i-v characteristic** of a basic BJT current mirror circuit. This type of graph is typically used to illustrate how the output current ($i_o$) varies with the output voltage ($v_o$) in a transistor circuit.

Axes Labels and Units:
- **X-axis (Horizontal):** Represents the output voltage $v_o$, typically in volts (V).
- **Y-axis (Vertical):** Represents the output current $i_o$, typically in amperes (A).
- The scale appears to be linear, as is common for i-v characteristic curves.

Overall Behavior and Trends:
- The graph likely shows a region where the output current $i_o$ remains relatively constant over a range of output voltages $v_o$. This is characteristic of the active region of a current mirror, where the output current mirrors the input current.
- At lower voltages, there might be a steep increase in current, indicating the saturation region.
- As the voltage increases beyond a certain point, the current becomes constant, suggesting the active region.
- At very high voltages, the current may again change behavior, possibly indicating breakdown or another non-ideal effect.

Key Features and Technical Details:
- **Saturation Region:** At low $v_o$, the transistor $Q_2$ may not be fully active, leading to a steep rise in $i_o$.
- **Active Region:** A flat portion of the curve where $i_o$ is constant, showing the effective mirroring action of the current mirror. This is where the circuit is ideally used.
- **Breakdown Region:** At very high $v_o$, the graph might show a change in the slope, indicating non-ideal behavior.

Annotations and Specific Data Points:
- **Reference Lines:** May include lines indicating ideal constant current levels.
- **Critical Points:** The transition from saturation to active region is critical for understanding the operational limits of the current mirror.
- **Numerical Values:** Specific values for $v_o$ where transitions occur might be annotated, although these are not visible in the description provided.

(a)
image_name:(b)
description:The graph depicted is the output-port current-voltage (i-v) characteristic of a basic BJT current mirror. It is a plot with the output current ($i_O$) on the vertical axis and the output voltage ($v_O$) on the horizontal axis. The axes are labeled with $i_O$ and $v_O$, and the units are typically in amperes for current and volts for voltage, although specific units are not indicated on this graph.

The graph shows a distinct non-linear behavior typical of a BJT current mirror. Initially, as $v_O$ increases from zero, $i_O$ remains very low, indicating the saturation region. This is followed by a sharp increase in $i_O$, marking the transition from the saturation region to the active region. This transition occurs around the point labeled $V_{CE(EOS)}$, which is the collector-emitter voltage at the edge of saturation.

After this sharp rise, the graph enters a quasi-linear region where $i_O$ remains relatively constant despite further increases in $v_O$. This plateau indicates the active region where the current mirror operates ideally, maintaining a constant current. The value of this constant current is indicated by the horizontal line at $i_I(1 - 2/\beta_F)$, which represents the ideal current level minus the base current correction factor due to finite beta ($\beta_F$) of the transistors.

The slope of the line in the active region is slightly positive, represented by the term $1/r_o$, indicating a small increase in $i_O$ with $v_O$ due to the output resistance $r_o$ of the transistor. This slope is a measure of the non-ideality of the current mirror, reflecting the finite output resistance.

The graph is annotated with critical voltages $V_{CE(EOS)}$ and $v_{BE}$, the base-emitter voltage, which are key points in understanding the operational limits and behavior of the current mirror. The transition from the saturation to the active region is particularly critical for understanding how the current mirror will behave under different load conditions.

(b)

FIGURE 4.56 (a) Basic BJT current mirror, and (b) output-port i-v characteristic.
For a detailed analysis refer to Fig. $4.57 a$ and assume $V_{A}=\infty$ for simplicity. Since the BJTs are matched and experience the same $v_{B E}$ drop, they must draw identical currents, here denoted as $i_{C}$. Also, together they draw a total base current of $2 i_{C} / \beta_{F}$. Consequently, KCL gives $i_{I}=i_{C}+2 i_{C} / \beta_{F}=i_{C}\left(1+2 / \beta_{F}\right)$. Substituting $i_{C}=i_{o}$ and solving for $i_{o}$ gives

$$
\begin{equation*}
i_{O}=\frac{i_{I}}{1+2 / \beta_{F}} \cong i_{I}\left(1-\frac{2}{\beta_{F}}\right) \tag{4.127}
\end{equation*}
$$

Because of the finite current gain $\beta_{F}, i_{O}$ does not mirror $i_{I}$ exactly, but is afflicted by a small systematic error $\varepsilon=-2 / \beta_{F}$. For instance, with $\beta_{F}=100$, we have $\varepsilon=-2 \%$.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: vBE, B: vBE, E: GND}
name: Q2, type: NPN, ports: {C: vO, B: vBE, E: GND}
name: Load, type: Other, ports: {N1: vcc, N2: vo}
name: i_I, type: CurrentSource, ports: {Np: Vcc, Nn: vi}
]
extrainfo:The circuit in (a) is a basic BJT current mirror configuration using two NPN transistors, Q1 and Q2. The input current i_I is mirrored to the output current i_O, with a systematic error due to finite current gain β_F. The load is connected to the output node vO.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: VI, B: VBE, E: GND}
name: Q2, type: NPN, ports: {C: vO, B: vBE, E: GND}
name: Q3, type: NPN, ports: {C: VCC, B: vI, E: VBE}
name: Load, type: Other, ports: {N1: VCC, N2: VO}
name: iI, type: CurrentSource, ports: {Np: VCC, Nn: vI}
name: VCC, type: VoltageSource, ports: {Np: VCC, Nn: GND}
]
extrainfo:The circuit diagram (b) is a BJT current mirror with a beta helper transistor Q3. The current mirror consists of transistors Q1 and Q2, with Q3 providing additional current to improve accuracy. The input current iI is mirrored to the output current iO, with a systematic error due to the finite current gain beta_F. The load is connected to the output node vO.

FIGURE 4.57 (a) Currents in (a) the basic BJT current mirror, and (b) basic mirror with beta helper.

Note that Eq. (4.127) holds in dc as well as in ac form, so we have made no smallsignal approximations.

The above equation holds only as long as $v_{C E 2}=v_{C E 1}$, a condition that we shall refer to as $d c$ balance for the two BJTs. In the present case, this occurs for $v_{O}=v_{I}=v_{B E}$. If $v_{O}$ is raised above this value, $i_{O}$ will increase due to the Early effect. To account for this, we need to modify Eq. (4.127) as

$$
\begin{equation*}
i_{O} \cong i_{I}\left(1-\frac{2}{\beta_{F}}\right) \times\left(1+\frac{v_{O}-v_{B E}}{V_{A}}\right) \tag{4.128}
\end{equation*}
$$

The $i_{O^{-}} v_{O}$ characteristic is shown in Fig. $4.56 b$, along with the value of $i_{O}$ at dc balance and the corresponding value of $v_{0}$. Note that Eq. (4.128) holds so long as $v_{O} \geq v_{O(\min )}$, where

$$
\begin{equation*}
v_{O(\min )}=V_{C E(\mathrm{EOS})}(\cong 0.2 \mathrm{~V}) \tag{4.129}
\end{equation*}
$$

If $v_{O}$ drops below this limit, $Q_{2}$ will enter the saturation region, where we witness a rapid decrease in $i_{o}$. By inspection we also have $R_{i}=r_{o 1} / / r_{e l} / / r_{\pi 2} \cong r_{e 1} \cong 1 / g_{m 1}$, and $R_{o}=r_{o 2}$. Dropping subscripts 1 and 2 as the BJTs are assumed matched and are also biased identically, we thus have

$$
\begin{equation*}
R_{i} \cong \frac{1}{g_{m}} \quad R_{o}=r_{o} \tag{4.130}
\end{equation*}
$$

As we know, the $i_{O^{-}} v_{O}$ curve has a slope of $1 / r_{o}$, and its extrapolation intercepts the horizontal axis at $v_{O}=-V_{A}$, where $V_{A}$ is the Early voltage.

The above analysis stipulates perfect matching between $Q_{1}$ and $Q_{2}$. At times the transistors are deliberately fabricated with unequal emitter areas in order to provide current amplification or attenuation, depending on the case. For instance, if $Q_{2}$ 's emitter area is made twice as large as $Q_{1}$ 's, then $Q_{2}$ will draw twice as much current as $Q_{1}$, giving $i_{O} \cong 2 i_{r}$. Denoting the saturation currents of the two BJTs as $I_{s 1}$ and $I_{s 2}$, respectively, we can readily generalize Eq. (4.128) as

$$
\begin{equation*}
i_{O} \cong i_{l}\left(\frac{I_{s 2}}{I_{s 1}}\right) \times\left(1-\frac{1+I_{s 2} / I_{s 1}}{\beta_{F}}\right) \times\left(1+\frac{v_{O}-v_{B E}}{V_{A}}\right) \tag{4.131}
\end{equation*}
$$

In order to reduce the error stemming from the fact that $\beta_{F}$ is not infinite, a third transistor $Q_{3}$ is often added as in Fig. 4.57b. Aptly referred to as beta helper, $Q_{3}$ reduces the current component being subtracted from $i_{I}$ by a factor of $\beta_{F}+1$, in effect changing the dc balance value of Eq. (4.127) to

$$
\begin{equation*}
i_{O} \cong i_{l}\left(1-\frac{2}{\beta_{F}^{2}}\right) \tag{4.132}
\end{equation*}
$$

Note that with this modification $v_{I}$ is raised to $2 v_{B E}$, so the dc balance condition is now $v_{O}=2 v_{B E}$. The ac resistance seen by the input source also doubles to $R_{i} \cong 2 / g_{m}$ (see Problem 4.71). Beta helpers find application especially in multiple-output current mirrors.
image_name:(a) Basic MOSFET current mirror
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vgs, G: Vgs}
name: M2, type: NMOS, ports: {S: GND, D: Vo, G: Vgs}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: Load, type: Other, value: Load, ports: {N1: VDD, N2: Vo}
name: Ii, type: CurrentSource, value: Ii, ports: {Np: VDD, Nn: Vi}
]
extrainfo:This is a basic MOSFET current mirror circuit. The current mirror consists of two NMOS transistors, M1 and M2, which are configured to copy the input current Ii to the output node Vo. The input current source Ii drives the gate-source voltage Vgs of M1, which is mirrored to M2 to produce the output current Io. The load and Ro are connected to the output node Vo. The circuit is powered by a voltage source VDD.

(a)
image_name:Figure 4.58 (b)
description:The graph in Figure 4.58 (b) is an output-port current-voltage ($i$ - $v$) characteristic plot for a basic MOSFET current mirror circuit.

1. **Type of Graph and Function:**
- This is a characteristic curve representing the relationship between the output current ($i_O$) and the output voltage ($v_O$) in the current mirror.

2. **Axes Labels and Units:**
- The horizontal axis is labeled $v_O$, representing the output voltage.
- The vertical axis is labeled $i_O$, representing the output current.
- The units for both axes are not explicitly provided, but they typically represent volts (V) for the voltage and amperes (A) for the current.

3. **Overall Behavior and Trends:**
- The graph shows a typical MOSFET characteristic curve where the output current $i_O$ initially increases sharply with $v_O$ and then levels off, reflecting the saturation region of the MOSFET operation.
- After reaching a certain point, the increase in $i_O$ becomes more gradual, indicating the output resistance effect, which is represented by the slope $1/r_o$.

4. **Key Features and Technical Details:**
- The curve starts from the origin (0,0), indicating that both the output current and voltage start from zero.
- A horizontal line is drawn at $i_O = \frac{W_2/L_2}{W_1/L_1} i_I$, which represents the mirrored current ratio based on the transistor dimensions.
- Vertical lines at $v_{OV}$ and $v_{GS}$ mark significant voltage points:
- $v_{OV}$ is the overdrive voltage, where the MOSFET starts to enter saturation.
- $v_{GS}$ is the gate-source voltage, critical for MOSFET operation.

5. **Annotations and Specific Data Points:**
- The slope $1/r_o$ represents the output resistance of the MOSFET in the saturation region, affecting the linearity of the current mirror.
- The graph provides a visual representation of how the current mirror maintains a constant current over a range of output voltages, which is crucial for its function as a current source.

(b)

FIGURE 4.58 (a) Basic MOSFET current mirror, and (b) output-port $i$ - $v$ characteristic.

The above discussion has focused on current mirrors using npn-type BJTs, whose collectors sink current. If the application calls for the current mirror to source current, then the circuit is implemented with pnp-type BJTs, as already discussed in Chapter 2. Since IC pnp BJTs exhibit notoriously low betas, pnp mirrors often use beta helpers to reduce their inherently higher systematic error.

### Basic MOSFET Current Mirror

The MOS counterpart of the BJT mirror is shown in Fig. 4.58a. Thanks to the fact that gate currents are zero, a MOSFET current mirror does not suffer from the systematic error due to $\beta_{F}$. As the input source $i_{I}$ is turned on, the diode-connected transistor $M_{1}$ responds with the voltage drop $v_{G S}=V_{t}+v_{O V}$, where $v_{O V}$ is the overdrive voltage necessary to sustain $i_{r}$. The incoming current and $v_{G S}$ are related as

$$
i_{I}=\frac{k_{1}}{2}\left(v_{G S}-V_{t}\right)^{2}\left(1+\lambda v_{G S}\right)
$$

But, $M_{2}$ is subjected to the same drive $v_{G S}$ as $M_{1}$, so $M_{2}$ will draw the current

$$
i_{O}=\frac{k_{2}}{2}\left(v_{G S}-V_{t}\right)^{2}\left(1+\lambda v_{O}\right)
$$

As we know, the device trasconductance parameter of a MOSFET is $k=k^{\prime}(W / L)$, where $W$ and $L$ are the channel width and length of the particular FET, and $k^{\prime}$ is the process transconductance parameter, common to all same-type FETs on the chip. Taking the ratio $i_{o} / i_{I}$ and simplifying, we get, under the assumption $\lambda v_{G S} \ll 1$,

$$
\begin{equation*}
i_{O} \cong i_{I} \frac{W_{2} / L_{2}}{W_{1} / L_{1}} \times\left[1+\lambda\left(v_{O}-v_{G S}\right)\right] \tag{4.133}
\end{equation*}
$$

The $i_{O_{0}} v_{O}$ characteristic is shown in Fig. $4.58 b$, along with the value of $i_{O}$ at dc balance, a condition now expressed as $v_{O}=v_{I}=v_{G S}$. Note that Eq. (4.133) holds so long as $v_{O} \geq v_{O(\min )}$, where

$$
\begin{equation*}
v_{O(\min )}=v_{O V} \tag{4.134}
\end{equation*}
$$

If $v_{O}$ drops below this limit, $M_{2}$ will enter the triode region where $i_{O}$ eventually drops to zero. By inspection we also have $R_{i}=r_{o 1} / /\left(1 / g_{m 1}\right) \cong 1 / g_{m 1}$ and $R_{o}=r_{o 2}=1 /\left(\lambda i_{o}\right)$. Dropping subscripts 1 and 2 as the FETs are assumed matched and are also biased identically, we thus have

$$
\begin{equation*}
R_{i} \cong \frac{1}{g_{m}} \quad R_{o}=r_{o} \tag{4.135}
\end{equation*}
$$

As we know, the slope of the $i-v$ curve in Fig. $4.58 b$ is $1 / r_{o}$. Moreover, its extrapolation intercepts the horizontal axis at $v_{O}=-1 / \lambda$. If the $W / L$ ratios of the two FETs are equal, then $i_{O}=i_{I}$ at dc balance.

### Cascode Current Mirrors

According to Eqs. (4.130) and (4.135), the output resistance of basic current mirrors is $r_{o}$. There are many situations requiring a much higher output resistance, and the cascoding techniques of Section 4.4 provide a popular way to raise output resistance significantly.

Figure 4.59 a shows a bipolar cascode mirror. The matched BJT pair $Q_{3}{ }^{-} Q_{4}$ provides the mirror action proper, whereas the CB BJT $Q_{2}$ raises the output resistance way above $r_{o}$. The function of diode-connected $Q_{1}$ is to bias $Q_{2}$ 's base a $v_{B E}$ drop above $Q_{4}$ 's
image_name:(a)
description:
[
'name': 'Q1', 'type': 'NPN', 'ports': {'C': '2VBE', 'B': '2VBE', 'E': 'VBE'
'name': 'Q2', 'type': 'NPN', 'ports': {'C': 'Vo', 'B': '2VBE', 'E': 'X'
'name': 'Q3', 'type': 'NPN', 'ports': {'C': 'VBE', 'B': 'VBE', 'E': 'GND'
'name': 'Q4', 'type': 'NPN', 'ports': {'C': 'X', 'B': 'VBE', 'E': 'GND'
'name': 'iI', 'type': 'CurrentSource', 'value': 'iI', 'ports': {'Np': 'VCC', 'Nn': '2VBE'
'name': 'Load', 'type': 'Other', 'ports': {'N1': 'VDD', 'N2': 'Vo'
]
extrainfo:The circuit diagram (a) shows a bipolar cascode current mirror. It consists of NPN transistors Q1, Q2, Q3, and Q4. Q1 is diode-connected to provide biasing for Q2, raising the output resistance. The current source iI provides the input current, and the resistors Ri and Ro are connected to the input and output nodes respectively. The circuit is designed to increase output resistance significantly using cascoding techniques.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: Vt+Vov, D: 2Vt+2Vov, G: 2Vt+2Vov}
name: M2, type: NMOS, ports: {S: X, D: Vo, G: Vt+Vov}
name: M3, type: NMOS, ports: {S: GND, D: 2Vt+2Vov, G: Vt+Vov}
name: M4, type: NMOS, ports: {S: X, D: Vo, G: Vt+Vov}
name: i_I, type: CurrentSource, value: i_I, ports: {Np: Vi, Nn: GND}
name: R_i, type: Resistor, value: R_i, ports: {N1: Vi, N2: 2Vt+2Vov}
name: R_o, type: Resistor, value: R_o, ports: {N1: Vo, N2: Load}
name: Load, type: Other, ports: {N1: Load, N2: GND}
]
extrainfo:This is a MOS cascode current mirror circuit. The circuit on the right (b) uses NMOS transistors to achieve high output resistance. The input voltage is Vi and the output voltage is Vo. The circuit is biased by a current source i_I. The resistors R_i and R_o are used to control the input and output impedance.

FIGURE 4.59 Cascode current mirrors: (a) bipolar and (b) MOS.
base to give $v_{C E 4}=v_{C E 3}=v_{B E}$. Compared to the basic mirror, the input parameters are doubled to $v_{I}=2 v_{B E}$ and $R_{i} \cong 2 / g_{m}$. Also, the lower limit of the linear range of operation is now raised by one $v_{B E}$ drop to $v_{O(\min )}=v_{C E 4}+V_{C E 2(\mathrm{EOS})}=v_{B E}+V_{C E 2(\mathrm{EOS})}$. It is left as an exercise for the student (see Problem 4.72) to prove that $R_{i} \cong 2 / g_{m}, R_{o} \cong\left(\beta_{0} / 2\right) r_{o}$ and

$$
\begin{equation*}
i_{O} \cong i_{l}\left(1-\frac{4}{\beta_{F}}\right) \times\left(1+\frac{v_{O}-2 v_{B E}}{\left(\beta_{0} / 2\right) V_{A}}\right) \tag{4.136}
\end{equation*}
$$

We can visualize the effect of cascoding as shifting the extrapolated intercept of the $i_{O}-v_{O}$ curve with the horizontal axis from $-V_{A}$ to about $-\left(\beta_{0} / 2\right) V_{A}$, thus making the $i_{o}-v_{O}$ curve much flatter.

When the output resistance of a collector terminal is raised significantly above $r_{o}$ as in the present case, the base-collector resistance $r_{\mu}$ may no longer be negligible. As we know, $r_{\mu}$ models the effect of base-width modulation by $v_{C E}$ upon the recombination current in the base, and is expressed as $r_{\mu}=m \beta_{0} r_{o}$, where $1 / m(m \geq 1)$ represents the fraction of the total base current due to recombination. A more accurate expression for the output resistance is thus

$$
\begin{equation*}
R_{o(\mathrm{BJT})} \cong\left(\frac{\beta_{0}}{2} r_{o}\right) / / r_{\mu}=\frac{m}{1+2 m} \beta_{0} r_{o} \tag{4.137}
\end{equation*}
$$

In the worst-case scenario of the base current being predominantly of the recombination type $(m \rightarrow 1)$, we get $R_{o} \rightarrow\left(\beta_{0} / 3\right) r_{o}$. In a practical cascode mirror $R_{o}$ will lie somewhere between $1 / 3$ and $1 / 2$ of $\beta_{0} r_{o}$.

Turning next to the MOS cascode mirror of Fig. $4.59 b$ we observe that it utilizes the matched pair $M_{3}-M_{4}$ to provide the mirror action proper, the CG FET $M_{2}$ to raise the output resistance, and the diode-connected FET $M_{1}$ to bias $M_{2}$ 's gate a diode drop above $M_{4}$ 's gate to give $v_{D S 4}=v_{D S 3}=V_{t}+v_{O V}$. Adapting Eq. (4.63) we now have $R_{o}=r_{o 2}\left[1+\left(g_{m 2}+g_{m b 2}\right) r_{o 4}\right]+r_{o 4}$ or, dropping the subscripts,

$$
\begin{equation*}
R_{o(\mathrm{MOS})}=r_{o}\left[2+\left(g_{m}+g_{m b}\right) r_{o}\right] \tag{4.138}
\end{equation*}
$$

As expected, the artifice of cascoding raises the output resistance by a factor of $\left[2+\left(g_{m}+g_{m b}\right) r_{o}\right]$ or, equivalently, it shifts the $v_{o}$-axis intercept of the $i_{o^{-}} v_{O}$ curve from $-1 / \lambda$ to $(-1 / \lambda) \times\left[2+\left(g_{m}+g_{m b}\right) r_{o}\right]$.

For the circuit to function properly, both $M_{2}$ and $M_{4}$ must operate with $v_{D S} \geq v_{O V}$. Since $v_{D S 4}=V_{t}+v_{O V}$, it turns out that $M_{4}$ actually exceeds the minimum required by an amount equal to $V_{t}$. Imposing $v_{D S 2} \geq v_{O V}$ we find that the linear output range is now $v_{O} \geq v_{O(\min )}$, where $v_{O(\min )}=v_{D S 4}+v_{O V}$, or

$$
\begin{equation*}
v_{O(\min )}=V_{t}+2 v_{O V} \tag{4.139}
\end{equation*}
$$

Compared to Eq. (4.134) for the basic mirror of Fig. 4.58a, the limit of Eq. (4.139) may prove too high in low-voltage applications where even fractions of a volt matter.

While we can make the $2 v_{O V}$ term as small as needed by fabricating the FETs with suitably large $W / L$ ratios, the $V_{t}$ term poses the ultimate limit on $v_{O(\min )}$.

### Wide-Swing MOS Cascode Mirrors

Wide-swing cascode mirrors eliminate the $V_{t}$ term from Eq. (4.139) by downshifting $M_{2}$ 's bias from $v_{G 2}=2 V_{t}+2 v_{O V}$ of Fig. $4.59 b$ to $v_{G 2}=1 V_{t}+2 v_{O V}$ in order to bring $M_{4}$ right to the edge of saturation, where $v_{D S 4}=v_{O V}$. This results in

$$
\begin{equation*}
v_{O(\min )}=2 v_{O V} \tag{4.140}
\end{equation*}
$$

In the modified cascode mirror of Fig. 4.60 a this downshift is provided by the source follower $M_{5}$. ( $M_{5}$ is biased by $M_{6}$, in turn mirroring $M_{3}$.) To yield $v_{S 5}=V_{t}+2 v_{O V}$, $M_{5}$ requires $v_{G 5}=v_{S 5}+v_{G S 5}=\left(V_{t}+2 v_{O V}\right)+\left(V_{t}+v_{O V}\right)=2 V_{t}+3 v_{O V}$. Compared to Fig. $4.59 b$, where $v_{I}=2 V_{t}+2 v_{O V}$, we now need $v_{I}=2 V_{t}+3 v_{O V}$, or $1 v_{O V}$ higher. We achieve this by fabricating $M_{1}$ with a $W / L$ ratio that is $1 / 4$ that of all other FETs so that, by virtue of the relation $v_{O V}=\sqrt{(2 / k) i_{D}}, M_{1}$ will require an overdrive voltage of $2 v_{O V}$ to sustain the same current $i_{D}$ that all other FETs are sustaining with only $1 v_{O V}$.

A drawback of the circuit of Fig. 4.60a is that it requires an additional branch $\left(M_{5}-M_{6}\right)$ to provide level shifting. The two branches are cleverly combined into one in the circuit of Fig. 4.60b, called the Sooch cascode current mirror for its
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: X1, D: VI, G: VI}
name: M2, type: NMOS, ports: {S: Vov, D: Vo, G: Vt+2Vov}
name: M3, type: NMOS, ports: {S: GND, D: X1, G: X1}
name: M4, type: NMOS, ports: {S: GND, D: VO, G: Vt+Vov}
name: M5, type: NMOS, ports: {S: Vt+2Vov, D: VDD, G: 2Vt+3Vov}
name: M6, type: NMOS, ports: {S: GND, D: Vt+2Vov, G: X1}
name: i1, type: CurrentSource, ports: {Np: VDD, Nn: 2Vt+3Vov}
name: Load, type: Other, ports: {N1: VDD, N2: Vo}
]
extrainfo:This is a wide-swing cascode current mirror circuit using NMOS transistors. The circuit utilizes source followers and cascode connections to achieve level shifting and improved performance. M1, M2, M3, and M4 form the main current mirror, while M5 and M6 provide level shifting. The current source i1 supplies the bias current, and the load is connected to the output node VO.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: s1d5, D: vI, G: vI}
name: M2, type: NMOS, ports: {S: s2d4, D: vO, G: s1d5}
name: M3, type: NMOS, ports: {S: GND, D: s6d3, G: g3s5g4}
name: M4, type: NMOS, ports: {S: GND, D: s2d4, G: g3s5g4}
name: M5, type: NMOS, ports: {S: g3s5g4, D: s1d5, G: vI}
name: M6, type: NMOS, ports: {S: s6d3, D: g3s5g4, G: s1d5}
name: iI, type: CurrentSource, ports: {Np: VDD, Nn: VI}
name: Load, type: Other, ports: {N1: VDD, N2: Vo}
]
extrainfo:The circuit diagram (b) is a Sooch cascode current mirror. It uses a clever combination of branches to provide level shifting. The M6-M3 pair synthesizes the voltage needed to bias M4.

FIGURE 4.60 Wide-swing cascode mirrors. (a) Using source follower $M_{5}$ to downshift $M_{2}$ 's bias by $V_{t}$ (note that the $W / L$ ratio of $M_{1}$ is $1 / 4$ that of all other FETs). (b) The Sooch cascode current mirror.
inventor N. S. Sooch. Though the details of its analysis are left as an exercise for the student (see Problem 4.73), suffice it to list here its principal features, which are:

- The $M_{6}-M_{3}$ pair synthesizes the voltage $v_{G 4}=V_{t}+v_{O V}$ needed to bias $M_{4}$.
- The $M_{1}-M_{5}$ pair synthesizes the voltage drop $v_{D S 5}=v_{O V}$ needed to bias $M_{2}$ at $v_{G 2}=V_{t}+2 v_{O V}$, that is, $1 v_{O V}$ higher than $v_{G 4}$. As discussed in Problem 4.73, we achieve this by fabricating $M_{5}$ with a $W / L$ ratio that is $1 / 3$ that of the other FETs.
- $M_{6}$ is designed to drop $v_{D S 6}=V_{t}$ and thus force $M_{3}$ to operate at $v_{D S 3}=v_{O V}=v_{D S 4}$. This eliminates any channel-length modulation differences between $M_{3}$ and $M_{4}$ and thus results in perfectly matched currents (so long as the $W / L$ ratios of $M_{3}$ and $M_{4}$ are matched).
In the above analyses we have neglected the body effect for simplicity. In practice, all FETs with source voltages different from the body voltage will exhibit slightly higher values of $V_{t}$. The IC designer can compensate for threshold shifts by suitably adjusting the $W / L$ ratios when needed.

### Wilson Current Mirror

The Wilson current mirror, shown in Fig. 4.61a, was developed to improve the characteristics of the basic bipolar current mirror. As the input source is turned on, $i_{I}$ will initially flow into $Q_{3}$ 's base, turning on $Q_{3}$ as well as the diode-connected transistor $Q_{2}$. The current through $Q_{2}$ is then mirrored by $Q_{1}$ back to the input node, thus closing a negative-feedback loop. While in the basic mirror of Fig. $4.56 a$ both base currents are subtracted from the input side of the circuit, in the Wilson configuration $i_{B 3}$ is subtracted from the input side and $i_{B 1}$ is subtracted from the output side. As we shall see shortly,
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: VI, B: VBE, E: GND}
name: Q2, type: NPN, ports: {C: VBE, B: VBE, E: GND}
name: Q3, type: NPN, ports: {C: Vo, B: VI, E: VBE}
name: Load, type: Resistor, value: Load, ports: {N1: VCC, N2: VO}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: iI, type: CurrentSource, value: iI, ports: {Np: VCC, Nn: VI}
]
extrainfo:The circuit is a Wilson current mirror configuration designed to improve output current accuracy by using negative feedback. It consists of three NPN transistors (Q1, Q2, Q3) and resistors for input and output current stabilization. The configuration helps in reducing the output current error and increases the output resistance.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: P, B: VBE, E: GND}
name: Q2, type: NPN, ports: {C: VBE, B: VBE, E: GND}
name: Q3, type: NPN, ports: {C: x1, B: P, E: VBE}
name: Load, type: Other, ports: {N1: VCC, N2: x1}
name: iI, type: CurrentSource, value: iI, ports: {Np: VCC, Nn: P}
]
extrainfo:The circuit diagram (b) is a Wilson current mirror configuration. It uses three NPN transistors and provides a negative feedback loop to mirror the input current to the output with reduced error. The feedback increases the output resistance significantly.

FIGURE 4.61 (a) Wilson current mirror, and (b) its various current components.
this form of cancellation reduces the output current error to a level comparable to that of the beta helper, provided the BJTs have matched betas. Moreover, the presence of negative feedback raises the output resistance dramatically.

To find a relationship between $i_{O}$ and $i_{J}$, refer to Fig. 4.61b. Assuming $V_{A}=\infty$ for simplicity and starting out at the bottom, we observe that $Q_{1}$ and $Q_{2}$ are subject to the same drive $v_{B E}$, so they draw identical currents, here denoted as $i_{C}$. Moving upward, we repeatedly apply KCL as well as the forward-region current relationships of BJTs to end up with the relationships

$$
i_{I}=i_{C}\left[1+\left(1+\frac{2}{\beta_{F}}\right) \frac{1}{\beta_{F}+1}\right] \quad i_{O}=\beta_{F} i_{C}\left(1+\frac{2}{\beta_{F}}\right) \frac{1}{\beta_{F}+1}
$$

Eliminating $i_{C}$ we find, after minor algebra,

$$
\begin{equation*}
i_{O}=i_{I} \frac{1}{1+\frac{2}{\beta_{F}\left(\beta_{F}+2\right)}} \cong i_{I} \frac{1}{1+\frac{2}{\beta_{F}^{2}}} \cong i_{l}\left(1-\frac{2}{\beta_{F}^{2}}\right) \tag{4.141}
\end{equation*}
$$

For instance, with $\beta_{F}=100$ the error is $\varepsilon=-0.02 \%$, which is truly negligible. We observe that the voltage at the input node is now $2 v_{B E}$ and that the circuit will work properly so long as $v_{O} \geq v_{O(\min )}$, where

$$
\begin{equation*}
v_{O(\text { min })}=v_{B E}+V_{C E 3(\mathrm{EOS})}(\cong 0.9 \mathrm{~V}) \tag{4.142}
\end{equation*}
$$

To find the output resistance $R_{o}$ we replace the circuit with its small-signal equivalent and use the test-voltage method of Fig. 4.62a. Here, $r_{\pi 1}$ and $r_{o 2}$ have been lumped together with $r_{e 2}$, the dynamic resistance of diode-connected transistor $Q_{2}$. Moreover, since $Q_{1}$ mirrors the current of $Q_{2}$, we model it with a unity-gain controlled source $1 i_{2}$. Since $r_{o 2} \gg r_{\pi 1} \gg r_{e 2}$, we approximate $r_{\pi 1} / / r_{e 2} / / r_{o 2} \cong r_{e 2}=\alpha_{02} / g_{m 2} \cong$ $1 / g_{m}$, as shown in Fig. 4.62b. In fact, it turns out that we can also ignore $r_{o 1}$ in the course of our calculations. To see why, we apply KCL at the upper-left node, along with KVL and Ohm's law and get

$$
i_{b 3}+1 i_{2}+\frac{r_{e 2} i_{2}+r_{\pi 3} i_{b 3}}{r_{o 1}}=0 \Rightarrow i_{b 3}\left(1+\frac{r_{\pi 3}}{r_{o 1}}\right)+i_{2}\left(1+\frac{r_{e 2}}{r_{o 1}}\right)=0
$$

image_name:(a)
description:
[
name: r_pi3, type: Resistor, value: r_pi3, ports: {N1: X1, N2: X2}
name: r_o1, type: Resistor, value: r_o1, ports: {N1: X1, N2: GND}
name: r_o3, type: Resistor, value: r_o3, ports: {N1: V, N2: X2}
name: r_pi1//r_e2//r_o2, type: Resistor, value: r_pi1//r_e2//r_o2, ports: {N1: X2, N2: GND}
name: i_1, type: CurrentSource, value: i_1, ports: {Np: X1, Nn: GND}
name: v, type: VoltageSource, value: v, ports: {Np: V, Nn: GND}
name: beta_03i_b3, type: VoltageControlledCurrentSource, ports: {Np: V, Nn: X2}
]
extrainfo:The circuit is a small-signal model of a Wilson current mirror. It includes resistors and current sources to model transistor behavior. The circuit is simplified by ignoring certain resistances due to their relative magnitudes.
image_name:(b)
description:
[
name: r_pi, type: Resistor, value: r_pi, ports: {N1: X1, N2: X2}
name: r_o, type: Resistor, value: r_o, ports: {N1: V, N2: X1}
name: 1/g_m, type: Resistor, value: 1/g_m, ports: {N1: X1, N2: GND}
name: i/2, type: CurrentSource, value: i/2, ports: {Np: X2, Nn: GND}
name: β_0i/2, type: VoltageControlledCurrentSource, ports: {Np: X1, Nn: V}
name: v, type: VoltageSource, value: v, ports: {Np: V, Nn: GND}
]
extrainfo:This is a simplified small-signal model of a Wilson current mirror. The diagram represents the ac equivalent circuit with a voltage-controlled current source and resistors modeling the transistors' behavior.

FIGURE 4.62 (a) Small-signal model of the Wilson current mirror, and (b) its simplified version.

Given that $r_{e 2} \ll r_{\pi 3} \ll r_{o 1}$, we can ignore $r_{o 1}$ and write $i_{b 3}+i_{2} \cong 0$, or $i_{b 3}=-i_{2}$. This means that the ac current $i_{b 3}$ is actually flowing out of $Q_{3}$ 's base, and that $i_{b 3}$ coincides with the current $1 i_{2}$ drawn by the dependent source modeling $Q_{1}$. The ac equivalent of Fig. $4.62 a$ simplifies as in Fig. $4.62 b$, where we have exploited the fact that $i=1 i_{2}+i_{2}$, or $i_{2}=i / 2$. Applying Kirchoff's laws and Ohm's law gives

$$
i+\beta_{0} \frac{i}{2}=\frac{v-\left(1 / g_{m}\right) i / 2}{r_{o}} \Rightarrow i\left(1+\frac{\beta_{0}}{2}+\frac{1}{2 g_{m} r_{o}}\right)=\frac{v}{r_{o}}
$$

But, $1 /\left(2 g_{m} r_{o}\right) \ll 1$, so we finally get

$$
\begin{equation*}
R_{o}=\frac{v}{i} \cong\left(1+\frac{\beta_{0}}{2}\right) r_{o} \cong \frac{\beta_{0}}{2} r_{o} \tag{4.143a}
\end{equation*}
$$

It is left as an exercise for the student (see Problem 4.71) to prove that $R_{i} \cong 2 / g_{m}$ in Fig. 4.61 $a$. Compared to the basic-mirror characteristic of Fig. 4.56b, the Wilson mirror yields a much flatter curve, but only down to $v_{O}=v_{B E}+V_{C E 3(E O S)}$. Alternatively, we can say that the intercept of the Wilson's $i-v$ curve with the horizontal axis is shifted from $-V_{A}$ to $-\left(\beta_{0} / 2\right) V_{A}$. This great improvement is the result of the negative-feedback action provided by $Q_{1}$, a subject we shall return to in Chapter 7. As in the cascode realization, the output resistance is raised significantly above $r_{o}$, so $r_{\mu}$ may no longer be negligible. As in the cascode case, a better estimate for $R_{o}$ is then

$$
\begin{equation*}
R_{o} \cong\left(\frac{\beta_{0}}{2} r_{o}\right) / / r_{\mu}=\frac{m}{1+2 m} \beta_{0} r_{o} \tag{4.143b}
\end{equation*}
$$

Finally, it must be said that the calculation of the various currents in Fig. $4.62 b$ postulates identical currents for $Q_{1}$ and $Q_{2}$, when in fact the two BJTs are operating at different values of $v_{C E}$, namely, $v_{C E 2}=v_{B E}$ and $v_{C E 1}=2 v_{B E}$. Consequently, $i_{C 1} \cong$ $i_{C 2}\left(1+v_{B E} / V_{A}\right)$. This difference results in a systematic error for $i_{O}$. To account for this error, typically around $1 \%$, we need to refine the initial value of Eq. (4.141) as

$$
\begin{equation*}
i_{O} \cong i_{l}\left(1-\frac{2}{\beta_{F}^{2}}\right) \times\left(1-\frac{v_{B E}}{V_{A}}\right) \cong i_{l}\left(1-\frac{2}{\beta_{F}^{2}}-\frac{v_{B E}}{V_{A}}\right) \tag{4.144}
\end{equation*}
$$

where the higher-order term has been ignored in the calculation of the product. When undesirable, this additional systematic error can be eliminated by fabricating a diode-connected BJT $Q_{4}$ in series with the collector terminal of $Q_{1}$. Then, the $v_{B E}$ drop across this dummy diode will equalize the $v_{C E} \mathrm{~s}$ of $Q_{1}$ and $Q_{2}$ and therefore ensure $i_{C 1}=i_{C 2}$.

EXAMPLE 4.23 (a) If $i_{I}=1.0 \mathrm{~mA}$ in the basic current mirror of Fig. $4.56 a$, what is the initial value of $i_{O}$ ? By how much does $i_{O}$ change if $v_{O}$ is raised by 10 V ? Assume matched BJTs with $\beta_{0}=100$ and $V_{A}=80 \mathrm{~V}$.
(b) Repeat, but for the Wilson mirror of Fig. 4.61 $a$. Compare and comment.

#### Solution

(a) By Eq. (4.127), $i_{o}=1.0(1-2 / 100)=0.98 \mathrm{~mA}$. Also, $R_{o}=r_{o}=80 / 0.98=$ $81.6 \mathrm{k} \Omega$. Consequently, $\Delta i_{o}=\Delta v_{o} / R_{o}=10 / 81.6=0.1225 \mathrm{~mA}$, indicating that $i_{0}$ will increase to $0.98+0.1225=1.1025 \mathrm{~mA}$.
(b) By Eq. (4.144), $i_{o}=1.0\left(1-2 / 100^{2}-0.7 / 80\right)=0.9910 \mathrm{~mA}$. Moreover, $R_{o}=\left(\beta_{0} / 2\right) r_{o}=(100 / 2) 80.7=4.04 \mathrm{M} \Omega$, so $\Delta i_{o}=\Delta v_{o} / R_{o}=10 / 4.04=$ $2.5 \mu \mathrm{~A}$, indicating that $i_{o}$ will increase to $0.9910+0.0025=0.9935 \mathrm{~mA}$. The Wilson source is superior both in terms of the initial error and the current variation with voltage.

### Widlar Current Source/Sink

In low-current dc biasing the need often arises for a current mirror capable of giving $I_{O} \ll I_{I}$. Though this can, in principle, be achieved by fabricating $Q_{2}$ in the basic mirror of Fig. $4.56 a$ with a much smaller emitter area than $Q_{1}$, a more viable alternative is to place a resistance $R$ in series with $Q_{2}$ 's emitter terminal to suitably reduce its $V_{B E}$ drop and hence lower the output current $I_{O}$. The result is the modified circuit of Fig. 4.63a, known as the Widlar current source for its inventor B. Widlar. (More properly, the circuit shown ought to be called Widlar current sink as it utilizes npn BJTs, with the designation Widlar current source reserved for its pnp version.) A side benefit of this circuit is that $R$ introduces emitter degeneration and therefore raises the output resistance to $R_{o} \cong r_{o 2}\left[1+g_{m 2}\left(r_{\pi 2} / / R\right)\right]$.

To investigate circuit behavior, neglect base currents and apply Ohm's law and KVL to write $R I_{O}=V_{B E 1}-V_{B E 2}=V_{T} \ln \left(I_{I} / I_{s}\right)-V_{T} \ln \left(I_{O} / I_{s}\right)$, or

$$
\begin{equation*}
R I_{O}=V_{T} \ln \frac{I_{I}}{I_{O}} \tag{4.145}
\end{equation*}
$$

image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: X1, B: X1, E: GND}
name: Q2, type: NPN, ports: {C: X2, B: X1, E: e1}
name: R, type: Resistor, value: R, ports: {N1: e1, N2: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: VCC, Nn: X1}
name: Load, type: Other, ports: {N1: VDD, N2: X2}
]
extrainfo:The circuit is a Widlar current sink. It is designed to provide a constant output current (I_O) regardless of the load, by using two NPN transistors (Q1 and Q2) and a resistor (R) for emitter degeneration. The current source (I1) provides the input current (I_I) to the circuit, and the load is connected in parallel with the output.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: X2, B: X1, E: GND}
name: Q2, type: NPN, ports: {C: X3, B: X2, E: GND}
name: R, type: Resistor, value: R, ports: {N1: X1, N2: X2}
name: I_I, type: CurrentSource, value: I_I, ports: {Np: VCC, Nn: X1}
name: Load, type: Other, ports: {N1: VCC, N2: X3}
]
extrainfo:The circuit is an implementation of a Widlar current sink. It uses two NPN transistors and a resistor to achieve a current ratio between I_O and I_I. The resistor R is used for emitter degeneration, which increases the output resistance.

FIGURE 4.63 (a) Widlar current sink. (b) An alternative implementation of the same concept.
where $V_{T}$ is the familiar thermal voltage ( $V_{T}=26 \mathrm{mV}$ at room temperature). Two issues arise in connection with the Widlar circuit: find $R$ to achieve a specified $I_{O} / I_{I}$ ratio; or, given $R$, find $I_{O} / I_{I}$.

EXAMPLE 4.24 (a) Find $R$ so that the Widlar circuit of Fig. $4.63 a$ gives $I_{O}=30 \mu \mathrm{~A}$ for $I_{I}=$ 0.5 mA . Assuming $\beta_{0}=100$ and $V_{A}=60 \mathrm{~V}$, find the source's output resistance as seen by the load.
(b) Find $I_{O}$ if $I_{I}=1.0 \mathrm{~mA}$ and $R=5 \mathrm{k} \Omega$.

#### Solution

(a) By Eq. (4.145),

$$
R=\frac{V_{T}}{I_{O}} \ln \frac{I_{I}}{I_{O}}=\frac{26 \times 10^{-3}}{30 \times 10^{-6}} \ln \frac{0.5 \times 10^{-3}}{30 \times 10^{-6}}=2.44 \mathrm{k} \Omega
$$

We have $g_{m}=1 /(0.87 \mathrm{k} \Omega), r_{\pi}=87 \mathrm{k} \Omega$, and $r_{o}=2 \mathrm{M} \Omega$. Due to the degeneration introduced by $R$, we get

$$
R_{o}=r_{o 2}\left[1+g_{m 2}\left(r_{\pi 2} / / R\right)\right]=2[1+(87 / / 2.44) / 0.87]=7.5 \mathrm{M} \Omega
$$

(b) Using again Eq. (4.145) we get

$$
I_{O}=\frac{V_{T}}{R} \ln \frac{I_{I}}{I_{O}}=\frac{26 \times 10^{-3}}{5 \times 10^{3}} \ln \frac{10^{-3}}{I_{O}}=5.2 \times 10^{-6} \ln \frac{10^{-3}}{I_{O}}
$$

This transcendental equation is solved via iterations. We expect $I_{O} \ll I_{l}$, so start out with an educated guess, say, $I_{O(0)}=10 \mu \mathrm{~A}$, and plug it in the right-hand side to obtain the new estimate $I_{O(1)}=24 \mu \mathrm{~A}$. Iterate by plugging this new estimate in the right-hand side and get $I_{O(2)}=19.4 \mu \mathrm{~A}$. After a few more iterations the result settles at $I_{O}=20.3 \mu \mathrm{~A}$.

Shown in Fig. 4.63b is an alternative circuit realization of the same concept, except that it achieves the same result using a much smaller value of $R$ since the current through $R$ is now $I_{I}\left(I_{O}\right)$. (As we know, smaller resistors are preferable as they take up less chip area.) We still have $V_{R}=V_{B E 1}-V_{B E 2}$. However, we now have $V_{R}=R I_{I}$, so Eq. (4.145) becomes

$$
\begin{equation*}
R I_{I}=V_{T} \ln \frac{I_{I}}{I_{O}} \tag{4.146}
\end{equation*}
$$

This expression can be used either to find $R$ for a given set of values of $I_{I}$ and $I_{O}$, or to find $I_{O}$ for a given set of values of $I_{I}$ and $R$ (see Problem 4.77). Rewriting Eq. (4.146) as

$$
I_{O}=I_{I} e^{-R I_{l} / V_{T}}
$$

we observe that for small values of $I_{I}$ the exponential term tends to unity, indicating that $I_{O}$ increases approximately in proportion to $I_{I}$. On the other hand, for large values of $I_{l}$, the exponential term dominates, causing $I_{O}$ to decrease with $I_{I}$. It is apparent that $I_{O}$ must peak at some intermediate value of $I_{I}$ (see Problem 4.78), this being the reason why the circuit of Fig. 4.63 b is also called a peaking current source (strictly speaking, the designation peaking current sink would be more appropriate for the present case of npn BJTs, and peaking current source for the case of pnp BJTs).

## 4.9 DIFFERENTIAL PAIRS WITH ACTIVE LOADS

The most common application of the differential pair is as input stage to operational amplifiers and voltage comparators, where the two most critical requirements are (a) a high differential gain $a_{d m}$ and (b) a high common-mode rejection ratio (CMRR). The circuits of Fig. 4.64 maximize both parameters by taking advantage of current mirrors.

Let us address the common-mode rejection ratio (CMRR) first. Previous analysis has shown that to ensure a high CMRR, the biasing circuitry must present a high resistance to the differential pair (high $R_{E E}$ for EC pairs, high $R_{S S}$ for SC pairs). In both circuits of Fig. 4.64 this constraint is met by using a current mirror that accepts
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: X1, B: VI1, E: P}
name: Q2, type: NPN, ports: {C: Vo, B: VI2, E: P}
name: Q3, type: PNP, ports: {C: X1, B: X1, E: VCC}
name: Q4, type: PNP, ports: {C: Vo, B: X1, E: VCC}
name: Q5, type: NPN, ports: {C: X2, B: X2, E: VEE}
name: Q6, type: NPN, ports: {C: P, B: X2, E: VEE}
name: V_I1, type: VoltageSource, value: V_I1, ports: {Np: VI1, Nn: GND}
name: V_I2, type: VoltageSource, value: V_I2, ports: {Np: VI2, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: GND, N2: X2}
]
extrainfo:The circuit diagram (a) features a differential amplifier using BJTs with active loads and current-source biasing. It employs a high CMRR strategy by utilizing a current mirror for biasing. The transistors Q3 and Q4 form the active load, while Q5 and Q6 act as the current mirror.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: P, D: g3g4d3, G: vI1}
name: M2, type: NMOS, ports: {S: P, D: Vo, G: vI2}
name: M3, type: PMOS, ports: {S: VDD, D: g3g4d3, G: g3g4d3}
name: M4, type: PMOS, ports: {S: VDD, D: Vo, G: g3g4d3}
name: M5, type: NMOS, ports: {S: GND, D: g5g6d5, G: g5g6d5}
name: M6, type: NMOS, ports: {S: GND, D: P, G: g5g6d5}
name: R, type: Resistor, value: R, ports: {N1: GND, N2: g5g6d5}
name: V_I1, type: VoltageSource, value: V_I1, ports: {Np: vI1, Nn: GND}
name: V_I2, type: VoltageSource, value: V_I2, ports: {Np: vI2, Nn: GND'}
]
extrainfo:The circuit diagram (b) is a CMOS differential pair with active loads and current-source biasing. It utilizes NMOS transistors M1 and M2 for the differential pair and PMOS transistors M3 and M4 as active loads. The current mirror formed by M5 and M6 provides biasing, ensuring high output resistance and improving common-mode rejection ratio (CMRR). The resistors and voltage sources are used to establish biasing conditions and input signals.

FIGURE 4.64 Differential pairs with active loads and current-source biasing: (a) BJT, and (b) CMOS.
the reference current established by $R$ and mirrors it to the differential pair at a high output resistance (in this case the resistance $r_{o 6}$ of the mirror transistor). If desired, we can raise this resistance further by using a Wilson current mirror or a cascode current mirror. When used to provide a biasing function as in the present case, a current mirror is called a current reference.

Next, let us address the differential-mode gain $a_{d m}$. Equations (4.88) and (4.93) provide estimates for the gains achievable with resistive-loaded differential pairs, namely,

$$
a_{d m(\mathrm{BJT})} \cong-\frac{R_{C}\left(I_{E E} / 2\right)}{V_{T}} \quad a_{d m(\mathrm{FET})} \cong-\frac{R_{D}\left(I_{S S} / 2\right)}{0.5 V_{O V}}
$$

In both cases gain is proportional to the dc voltage dropped across the load resistance $R_{C} / R_{D}$. If a higher gain is desired for given biasing conditions, $R_{C} / R_{D}$ will have to be increased. This, however, risks driving the transistors in saturation. We resolve this impasse by replacing resistive loads with active loads, as already mentioned in Section 4.1. In Fig. 4.64, $Q_{4} / M_{4}$ acts as the load to $Q_{2} / M_{2}$, so the role of $R_{C} / R_{D}$ in the above gain expressions is now played by the usually much larger output resistance $r_{o 4}$ of $Q_{4} / M_{4}$.

For proper operation, the load $Q_{4} / M_{4}$ must be biased at the same current as $Q_{2} / M_{2}$. The circuit of Fig. $4.64 a$ uses $Q_{1}$ to mimic the dc current $\alpha_{F} I_{E E} / 2\left(\cong I_{E E} / 2\right.$ drawn by its matched companion $Q_{2}$. This current is then fed to $Q_{3}$, which in turn forces its matched companion $Q_{4}$ to mirror it back to $Q_{2}$. So, at dc balance, all four BJTs draw identical currents, namely, $I_{E E} / 2$ ! Similar considerations hold for the CMOS counterpart of Fig. 4.64b, where at dc balance all four FETs draw identical currents of $I_{S S} / 2$.

An additional advantage of active loads is signal conversion from doubleended form $\left(v_{I 1}-v_{12}\right)$ to single-ended form $\left(v_{o}\right)$. This is an indispensable feature in popular ICs such as operational amplifiers and voltage comparators. Finally, it must be pointed out that the signal-processing circuit portions of Fig. 4.64 use no resistors, a definite advantage as integrated resistors tend to take up precious chip area.

### Voltage Transfer Curves

The voltage transfer curve (VTC) of an active-loaded differential pair can readily be plotted via PSpice. Let us first investigate the BJT circuit of Fig. 4.65a, where we observe the following:

- With $v_{I D}=0, I_{E E}$ divides equally between the matched BJTs $Q_{1}-Q_{2}$, so $I_{C 1}=I_{C 2}=$ $\alpha_{F} I_{E E} / 2 \cong I_{E E} / 2$. By KCL, $I_{C 3}=I_{C 1}$, and by mirror action, $I_{C 4}=I_{C 3}$, so all BJTs are biased at $I_{E E} / 2$. Taking the Early effect into consideration, we observe that for the BJTs to carry identical currents, the $d c$ balance conditions $V_{C E 2}=V_{C E 1}$ and $V_{E C 4}=V_{E C 3}$ must hold. These conditions are met simultaneously when

$$
\begin{equation*}
V_{O}=V_{C C}-V_{E B p} \tag{4.147}
\end{equation*}
$$

image_name:Figure 4.65(a)
description:
[
name: Q1, type: NPN, ports: {C: X1, B: Qn, E: P}
name: Q2, type: NPN, ports: {C: Vo, B: GND, E: P}
name: Q3, type: PNP, ports: {C: X1, B: X1, E: VCC}
name: Q4, type: PNP, ports: {C: Vo, B: X1, E: VCC}
name: V_ID, type: VoltageSource, ports: {Np: Qn, Nn: GND}
name: I_EE, type: CurrentSource, value: 1 mA, ports: {Np: P, Nn: VEE}
]
extrainfo:The circuit is an active-loaded emitter-coupled pair with a current mirror load. It is biased with I_EE = 1 mA. The VTC shows the output voltage V_O versus input voltage V_ID, indicating a differential amplifier behavior.
image_name:Figure 4.65(b)
description:The graph in Figure 4.65(b) is a Voltage Transfer Characteristic (VTC) plot, which shows the relationship between the input differential voltage \( v_{ID} \) and the output voltage \( v_O \).

1. **Axes Labels and Units:**
- The horizontal axis represents the input voltage \( v_{ID} \) in millivolts (mV), ranging from -10 mV to 10 mV.
- The vertical axis represents the output voltage \( v_O \) in volts (V), ranging from 0 V to 10 V.

2. **Overall Behavior and Trends:**
- The graph exhibits a nonlinear characteristic with a distinct transition region.
- For input voltages \( v_{ID} \) less than approximately -5 mV, the output voltage \( v_O \) remains close to 0 V, indicating a low output state.
- As \( v_{ID} \) increases past -5 mV, the output voltage begins to rise sharply, transitioning from the low state to the high state.
- The output reaches a high state of approximately 10 V at \( v_{ID} \) around 5 mV.

3. **Key Features and Technical Details:**
- The transition from low to high output voltage occurs over a narrow range of input voltages, indicating a steep slope in the VTC, which is typical for active-loaded differential pairs.
- The midpoint of the transition, where the output voltage is approximately 5 V, occurs around \( v_{ID} = 0 \) mV.
- This steep transition indicates high gain in the differential pair configuration.

4. **Annotations and Specific Data Points:**
- The graph does not have specific markers or annotations, but the key transition points are evident from the curve's shape.
- The symmetry about the midpoint (0 mV) suggests balanced operation of the circuit, as expected from the circuit configuration described in the context.

This VTC plot is characteristic of an active-loaded emitter-coupled pair, demonstrating its function as a differential amplifier with high gain and a defined transition region between low and high output states.

FIGURE 4.65 (a) PSpice circuit of an active-loaded EC pair with $I_{s n}=2 I_{s p}=2 \mathrm{fA}, \beta_{F n}=4 \beta_{F p}=200$, $V_{A n}=2 V_{A p}=100 \mathrm{~V}$, and (b) its VTC.
where $V_{E B p}$ is the emitter-base voltage drop of the pnp BJTs. In the example given, $V_{O} \cong 10-0.7=9.3 \mathrm{~V}$. However, a closer examination of the VTC of Fig. 4.65b reveals that the actual value of $V_{O}$ is lower than the above estimate. This is due to the beta error of the current-mirror load, which gives $I_{C 4}<I_{E E} / 2$ at the value of $V_{O}$ of Eq. (4.147). Consequently, $Q_{2}$ will pull down $V_{O}$ until $I_{C 4}=I_{C 2}$ exactly. From the plot, this occurs at $V_{o} \cong 8.0 \mathrm{~V}$ (more on this in Example 4.27).

- Raising $v_{I D}$ above 0 V makes $Q_{1}$ more conductive at the expense of $Q_{2}$ becoming less conductive. By mirror action, $Q_{4}$ also becomes more conductive, so the pull-up action by $Q_{4}$ will prevail over the pull-down action by $Q_{2}$. We thus witness a rise in $v_{O}$ until $Q_{4}$ reaches the edge of saturation (EOS). Beyond this point $Q_{4}$ saturates, in turn causing the VTC to saturate at $v_{O}=V_{C C}-V_{E C 4(\text { sat })} \cong$ $10-0.1=9.9 \mathrm{~V}$.
- Lowering $v_{I D}$ below 0 V makes $Q_{1}$ less conductive and $Q_{2}$ more conductive, causing the pull-down action by $Q_{2}$ to prevail over the pull-up action by $Q_{4}$. We now witness a drop in $v_{o}$, until $Q_{2}$ reaches the EOS. Below this point, the VTC saturates at $v_{O}=V_{E 2}+V_{C E 2(\mathrm{sat})} \cong-0.7+0.1=-0.6 \mathrm{~V}$.

Next, let us turn to the CMOS circuit of Fig. $4.66 a$, where we observe the following:

- With $v_{I D}=0, I_{S S}$ divides equally between the matched FETs $M_{1}-M_{2}$, giving $I_{D 1}=$ $I_{D 2}=I_{S S} / 2$. By KCL, $I_{D 3}=I_{D 1}$, and by mirror action, $I_{D 4}=I_{D 3}$, so all FETs are biased at $I_{S S} / 2$. Taking channel modulation into consideration, we observe that
image_name:Figure 4.66(a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: x1, G: VID}
name: M2, type: NMOS, ports: {S: P, D: vo, G: Mn}
name: M3, type: PMOS, ports: {S: VDD, D: x1, G: x1}
name: M4, type: PMOS, ports: {S: VDD, D: vo, G: x1}
name: VID, type: VoltageSource, ports: {Np: VID, Nn: GND}
name: ISS, type: CurrentSource, value: 100uA, ports: {Np: P, Nn: VSS}
]
extrainfo:The circuit is a CMOS differential amplifier with active loads. It consists of a differential pair (M1, M2) and current mirrors (M3, M4, Mp, Mn) to provide active loading and biasing. The supply voltages are VDD = 10V and VSS = -10V. The input voltage is VID, and the output voltage is vo. The current source ISS provides a bias current of 100µA.
image_name:Figure 4.66(b)
description:The graph in Figure 4.66 (b) is a Voltage Transfer Characteristic (VTC) curve, which shows the relationship between the input differential voltage \( v_{ID} \) and the output voltage \( v_O \) for a CMOS circuit.

1. **Type of Graph and Function:**
- This is a VTC graph, which is typically used to depict how the output voltage of a circuit responds to changes in the input voltage.

2. **Axes Labels and Units:**
- The x-axis represents the input differential voltage \( v_{ID} \) in millivolts (mV).
- The y-axis represents the output voltage \( v_O \) in volts (V).
- Both axes are on a linear scale.

3. **Overall Behavior and Trends:**
- The graph shows a sigmoid-like curve.
- At very negative values of \( v_{ID} \), the output voltage \( v_O \) is near zero, indicating that the circuit is in the cutoff region.
- As \( v_{ID} \) increases, \( v_O \) starts to rise sharply, indicating the transition region.
- The curve then flattens out as \( v_{ID} \) becomes more positive, showing that the circuit enters the saturation region where \( v_O \) approaches a maximum value close to the supply voltage.

4. **Key Features and Technical Details:**
- The transition from low to high output voltage occurs around \( v_{ID} = 0 \) mV, which is the threshold point.
- The output voltage \( v_O \) saturates at approximately 10 V, aligning with the positive supply voltage \( V_{DD} = 10 \) V.
- The steepest part of the curve, which indicates the highest gain, is centered around the origin.

5. **Annotations and Specific Data Points:**
- Key data points include the zero crossing at \( v_{ID} = 0 \) mV and the saturation level at \( v_O \approx 10 \) V.
- No additional annotations or reference lines are present on the graph.

FIGURE 4.66 (a) PSpice circuit of an active-loaded S pair with $k_{n}=k_{p}=100 \mu \mathrm{~A} / \mathrm{V}^{2}$, $V_{\text {ton }}=-V_{\text {top }}=1.0 \mathrm{~V}, \lambda_{n}=\lambda_{p}=0.02 \mathrm{~V}^{-1}$, and (b) its VTC.
for the FETs to carry identical currents, the dc balance conditions $V_{D S 2}=V_{D S 1}$ and $V_{S D 4}=V_{S D 3}$ must hold. These conditions are met simultaneously for

$$
\begin{equation*}
V_{O}=V_{D D}-V_{S G_{p}} \tag{4.148}
\end{equation*}
$$

where $V_{S G p}$ is the source-gate voltage drop of the $p$ MOSFETs. In the example given, $V_{O V}=1.0 \mathrm{~V}$, so $V_{S G_{p}}=\left|V_{t p}\right|+V_{O V}=1+1=2 \mathrm{~V}$ and $V_{O}=10-2=8 \mathrm{~V}$, in agreement with Fig. 4.66b.

- Raising $v_{I D}$ above 0 V makes $M_{1}$ more conductive at the expense of $M_{2}$ becoming less conductive. By mirror action, $M_{4}$ also becomes more conductive, indicating that the pull-up action by $M_{4}$ will prevail over the pull-down action by $M_{2}$. We thus witness a rise in $v_{O}$ until $M_{4}$ leaves the saturation region to enter the triode region. Beyond this point $M_{4}$ ceases to provide the mirror function and the VTC saturates, as shown.
- Lowering $v_{I D}$ below 0 V makes $M_{1}$ less conductive and $M_{2}$ more conductive, causing the pull-down action by $M_{2}$ to prevail over the pull-up action by $M_{4}$. We now witness a drop in $v_{O}$ until $M_{2}$ leaves the saturation region to enter the triode region. Below this point the VTC saturates, as shown.

### The Differential-Mode Gain

An instructive method for finding the differential-mode gain of an active-loaded differential pair is via its Norton equivalent, consisting of a dependent source $i_{o(\mathrm{sc})}$ and a parallel resistance $R_{o}$.

To find the short-circuit output current $i_{o(\mathrm{sc})}$, refer to the ac equivalents of Fig. 4.67, whose similarity indicates that their analysis can be carried out in parallel. We observe that since the collectors of $Q_{1}$ and $Q_{2}$ are terminated differently, the shared emitter terminal is not, strictly speaking, at ac ground, as shown. The EC pair
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: x2, B: Vid/2, E: X1}
name: Q2, type: NPN, ports: {C: GND, B: -Vid/2, E: x1}
name: Q3, type: PNP, ports: {C: x2, B: x2, E: GND}
name: Q4, type: PNP, ports: {C: GND, B: X2, E: GND}
name: Vid/2, type: VoltageSource, value: Vid/2, ports: {Np: Vid/2, Nn: GND}
name: -Vid/2, type: VoltageSource, value: -Vid/2, ports: {Np: -Vid/2, Nn: GND}
]
extrainfo:The circuit in diagram (a) is a differential amplifier using BJTs. It consists of two NPN transistors (Q1 and Q2) forming a differential pair, and two PNP transistors (Q3 and Q4) acting as current mirrors or loads. The input is a differential signal applied to the bases of Q1 and Q2, while the output is taken from the collectors of Q3 and Q4. The currents i1, i2, i3, and i4 are labeled, indicating the current paths through the transistors.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: X1, D: g3g4d3, G: Vid/2}
name: M2, type: NMOS, ports: {S: X1, D: GND, G: -Vid/2}
name: M3, type: PMOS, ports: {S: GND, D: g3g4d3, G: g3g4d3}
name: M4, type: PMOS, ports: {S: GND, D: GND, G: g3g4d3}
name: Vid/2, type: VoltageSource, value: Vid/2, ports: {Np: Vid/2, Nn: GND}
name: -Vid/2, type: VoltageSource, value: -Vid/2, ports: {Np: -Vid/2, Nn: GND}
]
extrainfo:The circuit diagram (b) represents a differential amplifier with BJT and CMOS transistors. The BJTs (Q1, Q2) form the input differential pair, while Q3 and Q4 are current mirrors. The CMOS part consists of two NMOS (M1, M2) and two PMOS (M3, M4) transistors, forming a differential pair and current mirror. The circuit is used to find the short-circuit output current i_o(sc). The input is a differential voltage (Vid/2 and -Vid/2) applied to the gates of the NMOS and the bases of the BJTs.

FIGURE 4.67 Half-circuits to find the short-circuit output current $i_{0}$ : (a) BJT, and (b) CMOS.
will be slightly imbalanced because of the Early effect and so will be the SC pair due to the channel-length modulation effect. Yet, to expedite our estimations, let us continue to assume ac grounds, as shown. For both pairs we can thus approximate

$$
i_{2}=i_{1} \cong g_{m n} \frac{v_{i d}}{2}
$$

where $g_{m n}$ is the transconductance of the transistors in the differential pair. By KCL we have $i_{3}=i_{1}$, and by current-mirror action we have $i_{4}=i_{3}$. Consequently, we also have $i_{4}=i_{1}$, so $i_{o(\mathrm{sc})}=i_{4}+i_{2}=2 i_{1}$, that is,

$$
\begin{equation*}
i_{o}(\mathrm{sc}) \cong g_{m n} v_{i d} \tag{4.149}
\end{equation*}
$$

In the bipolar case all four BJTs have identical $g_{m} \mathrm{~s}$, so we can drop the subscript $n$ and write in this case $i_{o(\mathrm{sc})}=g_{m} v_{i d}, g_{m}=0.5 I_{E E} / V_{T}$.However, in the MOS case we need to keep the distinction as $g_{m n}\left(=\sqrt{k_{n} I_{S S}}\right)$ and $g_{m p}\left(=\sqrt{k_{p} I_{S S}}\right)$ may differ because $k_{n}$ and $k_{p}$ are not necessarily identical.

Next, let us turn to the task of finding the small-signal output resistance $R_{o}$. To this end, set the input sources to zero, apply a test voltage $v$, find the current $i$ out of the test source, and let $R_{o}=v_{o} / i_{o}$. With reference to Fig. 4.68 we observe that in both circuits the test current $i$ consists of three components:

- The component $i_{4}$ into $Q_{4}$ 's collector or into $M_{4}$ 's drain. By Ohm's law this component is simply

$$
i_{4}=\frac{V}{r_{o 4}}
$$

- The component $i_{2}$ into $Q_{2}$ 's collector or into $M_{2}$ 's drain. Due to the presence of the degeneration resistance $R_{e 1}=r_{e 1}=\alpha_{01} / g_{m 1} \cong 1 / g_{m 1}$, the resistance seen looking into $Q_{2}$ 's collector is $r_{o 2}\left(1+g_{m 2} R_{e 1}\right)=r_{o 2}\left(1+g_{m 2} / g_{m 1}\right)=2 r_{o 2}$. Likewise, because
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: X1, B: GND, E: e1e2}
name: Q2, type: NPN, ports: {C: Vo, B: GND, E: e1e2}
name: Q3, type: PNP, ports: {C: X1, B: X1, E: GND}
name: Q4, type: PNP, ports: {C: Vo, B: X1, E: GND}
name: Vo, type: VoltageSource, value: Vo, ports: {Np: Vo, Nn: GND}
]
extrainfo:The circuit diagram (a) represents a BJT differential amplifier with degeneration resistors Re1 and Ro, and a voltage source Vo. The currents i2 and i4 flow through Q2 and Q4 respectively. The circuit diagram (b) represents a CMOS differential amplifier with degeneration resistors Rs1 and Ro, and a voltage source Vo. The currents i2 and i4 flow through M2 and M4 respectively. Both circuits are designed to find the output resistance R0.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: x, D: g3g4d3, G: GND}
name: M2, type: NMOS, ports: {S: x, D: Vo, G: GND}
name: M3, type: PMOS, ports: {S: GND, D: g3g4d3, G: g3g4d3}
name: M4, type: PMOS, ports: {S: GND, D: Vo, G: g3g4d3}
name: vo, type: VoltageSource, value: vo, ports: {Np: Vo, Nn: GND}
]
extrainfo:The circuit is a CMOS differential amplifier with NMOS transistors M1 and M2 forming the input differential pair, and PMOS transistors M3 and M4 forming the active load. The output resistance is determined by Ro, and the circuit is biased by Rs1. The output voltage is taken across the resistor Ro.

FIGURE 4.68 Test circuits to find the output resistance $R_{0}$ of the (a) BJT and (b) CMOS differential amplifier.
of the degeneration resistance $R_{s 1} \cong 1 /\left(g_{m 1}+g_{m b 1}\right)$, the resistance seen looking into $M_{2}$ 's drain is approximately $r_{o 2}\left[1+\left(g_{m 2}+g_{m b 2}\right) /\left(g_{m 1}+g_{m b 1}\right)\right]=2 r_{o 2}$. Thus

$$
i_{2}=\frac{v}{2 r_{o 2}}
$$

- By KCL, the component $i_{2}$ must leave $Q_{2}$ 's emitter or $M_{2}$ 's source, flow through $Q_{1}$ or $M_{1}$ and into $Q_{3}$ or $M_{3}$, from where it is finally mirrored by $Q_{4}$ or $M_{4}$, as shown.

We now apply KCL to write

$$
i_{o}=i_{4}+i_{2}+i_{2}=\frac{V}{r_{o 4}}+\frac{v}{2 r_{o 2}}+\frac{v}{2 r_{o 2}}=\frac{V}{r_{o 4}}+\frac{V}{r_{o 2}}=\frac{v}{r_{o 4} / / r_{o 2}}
$$

Letting $R_{o}=v_{o} / i_{o}$ we finally get

$$
\begin{equation*}
R_{o}=r_{o p} / / r_{o n} \tag{4.150}
\end{equation*}
$$

where, as usual, we use subscripts $n$ and $p$ to denote the collector/drain resistances of the transistors in the differential pair and in the current mirror, respectively.

As we know, the differential input resistance of the bipolar circuit is $R_{i d}=2 r_{\pi}$, whereas that of its CMOS counterpart is $R_{i d}=\infty$. We visualize our findings via the Norton equivalents depicted in Fig. 4.69. Finally, we use Ohm's law to obtain $v_{o d}=$ $R_{o} i_{o(\mathrm{sc})}$, or $v_{o d}=R_{o} g_{m} v_{i d}$ in the bipolar case, and $v_{o d}=R_{o} g_{m n} v_{i d}$ in the CMNOS case. The unloaded voltage gain is $a_{d m}=v_{o d} / v_{i d}$, so

$$
\begin{equation*}
a_{d m(\mathrm{BJT})}=g_{m}\left(r_{o p} / / r_{o n}\right) \quad a_{d m(\mathrm{MOS})}=g_{m n}\left(r_{o p} / / r_{o n}\right) \tag{4.151}
\end{equation*}
$$

image_name:(a)
description:
[
name: 2rπ, type: Resistor, value: 2rπ, ports: {N1: vi1, N2: vi2}
name: g_m v_id, type: VoltageControlledCurrentSource, value: g_m v_id, ports: {Np: GND, Nn: vod}
name: r_op//r_on, type: Resistor, value: r_op//r_on, ports: {N1: vod, N2: GND}
]
extrainfo:The circuit is a Norton equivalent of an active-loaded differential amplifier using BJTs. It consists of a voltage source representing the input differential voltage, a resistor representing the input resistance, a voltage-controlled current source modeling the transconductance, and an output resistor representing the load resistance.
image_name:(b)
description:
[
name: g_mn v_id, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: vod}
name: r_op // r_on, type: Resistor, value: r_op // r_on, ports: {N1: vod, N2: GND}
]
extrainfo:The circuit diagram (b) represents a Norton equivalent of a CMOS active-loaded differential amplifier. It shows a voltage-controlled current source and a parallel resistor connected to the ground, with the output voltage labeled as v_od.

FIGURE 4.69 Norton equivalents of the active-loaded differential amplifier: (a) BJT, and (b) CMOS.

In Problem 4.84 it is shown that $a_{d m(\text { MOS })}$ can be put in the insightful form

$$
\begin{equation*}
a_{d m(\mathrm{MOS})}=-\frac{2}{V_{O V_{n}}\left(\lambda_{n}+\lambda_{p}\right)} \tag{4.152a}
\end{equation*}
$$

where $V_{O V n}$ is the overdrive voltage of the FETs of the differential pair, and $\lambda_{n}$ and $\lambda_{p}$ are the channel-length modulation parameters of the $n$ FETs and the $p$ FETs, respectively. If all FETs are fabricated with the same channel length $L$, then Eq. (4.31) provides yet another insightful form for the differential gain

$$
\begin{equation*}
a_{d m(\mathrm{MOS})}=-\frac{2 L}{V_{O V_{n}}\left(\lambda_{n}^{\prime}+\lambda_{p}^{\prime}\right)} \tag{4.152b}
\end{equation*}
$$

where $\lambda_{n}^{\prime}$ and $\lambda_{p}^{\prime}$ are the process parameters characterizing channel-length modulation in the two FET types. It is apparent that the longer the channel for a given $V_{O V n}$, the higher the gain.
(a) Estimate the element values of the Norton equivalent of the bipolar circuit of Fig. 4.65a, as well as its voltage gain $a_{d m}$.
(b) Repeat, but for the CMOS circuit of Fig. 4.66a. Compare with part (a) and comment.

#### Solution

(a) We have $g_{m}=0.5 I_{E E} / V_{T}=0.5 / 26=1 /(52 \Omega), r_{o p}=50 / 0.5=100 \mathrm{k} \Omega$, $r_{o n}=100 / 0.5=200 \mathrm{k} \Omega, r_{o p} / / r_{o n}=100 / / 200=67 \mathrm{k} \Omega, 2 r_{\pi}=2 \times 200 \times 52=$ $20.8 \mathrm{k} \Omega$, and $a_{d m}=67 / 0.052=1282 \mathrm{~V} / \mathrm{V}$.
(b) We have $g_{m n}=\sqrt{k I_{S S}}=\sqrt{100 \times 100}=100 \mu \mathrm{~A} / \mathrm{V}, r_{o p}=r_{o n}=1 /(0.02 \times$ $\left.50 \times 10^{-6}\right)=1 \mathrm{M} \Omega, r_{o p} / / r_{o n}=0.5 \mathrm{M} \Omega$, and $a_{d m}=100 \times 0.5=50 \mathrm{~V} / \mathrm{V}$, a much lower gain than in the bipolar case due to lower $g_{m n}$.

#### The Common-Mode Rejection Ratio (CMRR)

As we know, a differential amplifier should ideally respond only to the differentialmode component $v_{i d}=v_{i 1}-v_{i 2}$, regardless of the common-mode component $v_{i c}=$ $\left(v_{i 1}+v_{i 2}\right) / 2$. But a real-life active-loaded amplifier is somewhat sensistive also to $v_{i c}$, so its overall output $v_{o}$ takes on the more general form

$$
v_{o}=v_{o d}+v_{o c}=a_{d m} v_{i d}+a_{c m} v_{i c}
$$

where $v_{o d}$ and $v_{o c}$ are the differential-mode and common-mode output components, and $a_{d m}$ and $a_{c m}$ are the corresponding gains. As we know, a figure of merit is the common-mode rejection ratio (CMRR),

$$
\begin{equation*}
\mathrm{CMRR}=\left|\frac{a_{d m}}{a_{c m}}\right| \tag{4.153}
\end{equation*}
$$

which should be as large as possible (ideally, $a_{c m}$ should be zero, so CMRR $=\infty$ ). We already know $a_{d m}$ from Eq. (4.151), so we only need to find $a_{c m}$, a task that we shall carry out with the help of the equivalent circuits of Fig. 4.70. In accordance with Section 4.6, the differential pairs $Q_{1}-Q_{2}$ and $M_{1}-M_{2}$ have been split into two common-mode halves. Moreover, the diode-connected transistors $Q_{3}$ and $M_{3}$ have been replaced by an equivalent resistance $r_{3}$, and the mirror transistors $Q_{4}$ and $M_{4}$ have been replaced by their small-signal equivalents (note that $r_{\pi 4}$ has been included in $r_{3}$ ). The obvious similarity between the two circuits suggests that we can analyze them simultaneously. (As usual, the following analysis assumes matched differential pairs as well as matched active-load pairs.)

In Fig. 4.70 $a$ we have, by inspection,

$$
\begin{equation*}
i_{1(\mathrm{BJT})}=i_{2(\mathrm{BJT})}=\frac{g_{m}}{1+g_{m} 2 R_{E E}} v_{i c} \tag{4.154a}
\end{equation*}
$$

image_name:(a)
description:
[
name: Vic, type: VoltageSource, value: Vic, ports: {Np: Vic, Nn: GND}
name: Q1, type: NPN, ports: {C: -V3, B: Vic, E: X1}
name: Q2, type: NPN, ports: {C: Voc, B: Vic, E: X2}
name: r3, type: Resistor, value: r3, ports: {N1: GND, N2: -V3}
name: gm4V3, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: Voc}
name: ro4, type: Resistor, value: ro4, ports: {N1: Voc, N2: GND}
name: 2REE, type: Resistor, value: 2REE, ports: {N1: X1, N2: GND}
name: 2REE, type: Resistor, value: 2REE, ports: {N1: X2, N2: GND}
]
extrainfo:The circuit is a BJT differential amplifier with a current mirror active load. It is used to find the common-mode gain acm = Voc / Vic. The resistors r3 and ro4 are part of the active load, and the transistors Q1 and Q2 form the differential pair.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: S1, D: -V3, G: Vic}
name: M2, type: NMOS, ports: {S: S2, D: Voc, G: Vic}
name: r3, type: Resistor, value: r3, ports: {N1: GND, N2: -V3}
name: ro4, type: Resistor, value: ro4, ports: {N1: Voc, N2: GND}
name: 2RSS, type: Resistor, value: 2RSS, ports: {N1: s1, N2: GND}
name: 2RSS, type: Resistor, value: 2RSS, ports: {N1: s2, N2: GND}
name: Vic, type: VoltageSource, value: Vic, ports: {Np: Vic, Nn: GND}
name: gm4V3, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: Voc}
]
extrainfo:The circuit is a CMOS differential amplifier with a common-mode feedback. It utilizes NMOS transistors M1 and M2 with a voltage-controlled current source gm4V3 for feedback. The resistors 2RSS are connected to the sources of M1 and M2, providing the biasing.

FIGURE 4.70 (a) BJT and (b) CMOS ac equivalents to find the common-mode gain $a_{c m}=v_{o c} / v_{i c}$.

Likewise, in Fig. $4.70 b$ we have

$$
\begin{equation*}
i_{1(\mathrm{MOS})}=i_{2(\mathrm{MOS})}=\frac{g_{m n}}{1+\left(g_{m n}+g_{m b n}\right) 2 R_{S S}} v_{i c} \tag{4.154b}
\end{equation*}
$$

Also in Fig. 4.70a we have, by inspection,

$$
\begin{equation*}
r_{3(\mathrm{BJT})}=\frac{1}{g_{m 3}} / / r_{o 3} / / r_{\pi 3} / / r_{\pi 4} \tag{4.155a}
\end{equation*}
$$

and in Fig. $4.70 b$ we have

$$
\begin{equation*}
r_{3(\mathrm{MOS})}=\frac{1}{g_{m 3}} / / r_{o 3} \tag{4.155b}
\end{equation*}
$$

The voltage drop $v_{3}=r_{3} i_{1}$ causes $Q_{4}$ and $M_{4}$ to source the current $g_{m 4} \nu_{3}$ to the output node, where KCL gives, for both circuits,

$$
g_{m 4} v_{3}=\frac{v_{o c}}{r_{o 4}}+i_{2}
$$

that is, $v_{o c}=g_{m 4} r_{o 4} r_{3} i_{1}-r_{o 4} i_{2}$. Exploiting the fact that $i_{2}=i_{1}$ and $g_{m 4}=g_{m 3}$ we get, for both circuits,

$$
\begin{equation*}
v_{o c}=\left(g_{m 3} r_{3}-1\right) r_{o 4} i_{1} \tag{4.156}
\end{equation*}
$$

Note that $r_{3}$ is slightly less than $1 / g_{m 3}$, so the product $g_{m 3} r_{3}$ will be slightly less than unity. Clearly, there is a slight imbalance between the current sourced by $Q_{4} / M_{4}$ and that sunk by $Q_{2} / M_{2}$, giving $v_{o c} \neq 0$. It is precisely this inherent imbalance that makes $a_{c m} \neq 0$ and therefore CMRR $<\infty$. Indeed, substituting Eq. (4.154) into Eq. (4.156) and letting $a_{c m}=v_{o c} / v_{i c}$ gives (see Problem 4.85)

$$
\begin{gather*}
a_{c m(\mathrm{BJT})}=\frac{-g_{m} r_{o p}}{\left(1+0.5 \beta_{0 p}\right)\left(1+2 g_{m} R_{E E}\right)}  \tag{4.157a}\\
a_{c m(\mathrm{MOS})}=\frac{-g_{m n} r_{o p}}{\left(1+g_{m p} r_{o p}\right)\left[1+2\left(g_{m n}+g_{m b n}\right) R_{S S}\right]}
\end{gather*}
$$

where, as usual, the numerical subscripts have been replaced by subscripts $p$ and $n$ when needed. So long as the various $g_{m} \times r$ products are much greater than unity, the above expressions simplify as

$$
\begin{equation*}
a_{c m(\mathrm{BJT})} \cong \frac{-r_{o p}}{\beta_{0 p} R_{E E}} \quad a_{c m(\mathrm{MOS})}=\frac{-1}{2\left(1+\chi_{n}\right) g_{m p} R_{S S}} \tag{4.157c}
\end{equation*}
$$

EXAMPLE 4.26
(a) Assuming $R_{E E}=100 \mathrm{k} \Omega$, find $a_{c m}$ and CMRR for the active-loaded EC pair of Fig. 4.65a.
(b) Repeat, but for the CMOS circuit of Fig. 4.66a. Assume $R_{S S}=0.5 \mathrm{M} \Omega$ and $g_{m b n}=0.1 g_{m n}$.

#### Solution

(a) By Eq. (4.157a) we have

$$
a_{c m(\mathrm{BJT})}=\frac{-100 / 0.052}{(1+0.5 \times 50)(1+2 \times 100 / 0.052)}=-19.2 \mathrm{mV} / \mathrm{V}
$$

Example 4.25a gave $a_{d m}=1282 \mathrm{~V} / \mathrm{V}$, so $\mathrm{CMRR}_{\text {BJT }}=1282 /\left(19.2 \times 10^{-3}\right)=$ 66,681 (=96.5 dB).
(b) In this particular example we have $g_{m n}=g_{m p}(=0.1 \mathrm{~mA} / \mathrm{V})$. Using Eq. (4.157b),

$$
a_{c m(\mathrm{MOS})}=\frac{-0.1 \times 1000}{(1+0.1 \times 1000)[1+2 \times 0.1(1+0.1) 500]}=-8.92 \mathrm{mV} / \mathrm{V}
$$

Example $4.25 b$ gave $a_{d m}=50 \mathrm{~V} / \mathrm{V}$, so $\mathrm{CMRR}_{\text {MOS }}=50 /\left(8.92 \times 10^{-3}\right)=$ 5,605 (=75 dB).

It is instructive to develop direct expressions for the CMRRs. Substituting Eqs. (4.151) and (4.157) into Eq. (4.153) we get (see Problem 4.85) the BJT expression

$$
\begin{equation*}
\mathrm{CMRR}_{\mathrm{BJT}}=\frac{1+0.5 \beta_{0 p}}{1+r_{o p} / r_{o n}}\left(1+2 g_{m} R_{E E}\right) \rightarrow \frac{\beta_{0 p} g_{m} R_{E E}}{1+r_{o p} / r_{o n}} \tag{4.158a}
\end{equation*}
$$

which shows an active-load improvement on the order of $\left(1+0.5 \beta_{0 p}\right) /\left(1+r_{o p} / r_{o n}\right)$ compared to the passive-load case. Likewise, for the MOSFET case we get

$$
\begin{equation*}
\mathrm{CMRR}_{\mathrm{MOS}} \cong \frac{1+g_{m p} r_{o p}}{1+r_{o p} / r_{o n}}\left[1+2\left(g_{m n}+g_{m b n}\right) R_{S S}\right] \rightarrow 2 g_{m p}\left(r_{o n} / / r_{o p}\right) g_{m n}\left(1+\chi_{n}\right) R_{S S} \tag{4.158b}
\end{equation*}
$$

indicating an improvement on the order of $\left(1+g_{m p} r_{o p}\right) /\left(1+r_{o p} / r_{o n}\right)$ compared to the passive-load case.

#### Input Offset Voltage of Active-Loaded Differential Pairs

In an active-loaded differential pair the input offset voltage $V_{O S}$ is the result of mismatches in the transistors of the differential pair as well as in those of the current mirror. Turning first to the BJT circuit of Fig. 4.64a, we adapt Eq. (4.118) and write

$$
\begin{equation*}
V_{O S(\mathrm{BJT})} \cong V_{T} \sqrt{\left(\frac{\Delta I_{s n}}{I_{s n}}\right)^{2}+\left(\frac{\Delta I_{s p}}{I_{s p}}\right)^{2}} \tag{4.159}
\end{equation*}
$$

If the two mismatches are of equal magnitude, the effect of the active-load mismatch is to make the offset typically $\sqrt{2}$ times as large as that due to the EC pair alone. In the bipolar case we have an additional offset term due to the beta error of the pnp mirror. As we know, this error is

$$
\Delta I_{C 4}=-\frac{2}{\beta_{F p}} I_{C 4} \cong-\frac{2}{\beta_{F p}} I_{C}
$$

where $\beta_{F_{p}}$ is the average beta of the pnp BJTs. Dividing this term by $-g_{m}\left(=-I_{C} / V_{T}\right)$ gives

$$
\begin{equation*}
V_{O S(\text { systematic) }} \cong \frac{\Delta I_{C 4}}{-g_{m}}=V_{T} \frac{2}{\beta_{F p}} \tag{4.160}
\end{equation*}
$$

This is the corrective voltage that we need to apply at the input in order to compensate for the beta error of the mirror, even if the npn and pnp pairs are perfectly matched. Unlike the offset terms resulting from random transistor mismatches, the term of Eq. (4.160) occurs always in the same direction and is therefore referred to as a systematic offset term. If necessary, it can be reduced by implementing the active load with a mirror equipped with a beta helper, or with a cascode-type or a Wilson-type mirror.

Using the data of Example 4.25a, discuss the effect of $\beta_{F p}$ in the bipolar circuit of Fig. 4.65a.

#### Solution

With $v_{I D}=0$ we have $I_{C} \cong 500 \mu \mathrm{~A}$ and $V_{E B p} \cong 0.7 \mathrm{~V}$. If the pnp BJTs had infinite betas, the circuit would yield $V_{O} \cong 10-0.7=9.3 \mathrm{~V}$. However, because of noninfinite pnp betas, the mirror exhibits an error $\Delta I_{C 4} \cong-(2 / 50) 500=-20 \mu \mathrm{~A}$. To achieve $I_{C 4}=I_{C 2}$, the output will change automatically by $\Delta V_{O}=R_{o} \Delta I_{C 4}=67 \times$ $10^{3} \times\left(-20 \times 10^{-6}\right) \cong-1.3 \mathrm{~V}$ and settle at $V_{o} \cong 9.3-1.3=8.0 \mathrm{~V}$, in agreement with the VTC of Fig. 4.65b. If we wish to ensure ideal dc balance we must drive $V_{O}$ back to 9.3 V . This is achieved by applying a corrective input voltage $V_{I D}=$ $-\Delta V_{o} / a_{d m}=1.3 / 1282 \cong 1 \mathrm{mV}$. Sure enough, this is the offset term predicted by Eq. (4.160), that is, $V_{O S \text { (systematic) }}=26(2 / 50)=1 \mathrm{mV}$ !

Turning next to the CMOS circuit of Fig. $4.64 b$, we note the absence of any systematic offset because the gate currents are zero. The offset now stems from $k$ and $V_{t}$ mismatches in each transistor pair. It is left as an exercise for the student (see Problem 4.96) to show that

$$
\begin{equation*}
V_{O S(\mathrm{MOS})} \cong \frac{V_{O V n}}{2} \sqrt{\left(\frac{\Delta k_{n}}{k_{n}}\right)^{2}+\left(\frac{\Delta k_{p}}{k_{p}}\right)^{2}+\left(\frac{\Delta V_{t n}}{0.5 V_{O V n}}\right)^{2}+\left(\frac{\Delta V_{t p}}{0.5 V_{O V n}}\right)^{2}} \tag{4.161}
\end{equation*}
$$

image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: P2, B: VI1, E: P1}
name: Q2, type: NPN, ports: {C: P3, B: VI2, E: P1}
name: Q3, type: PNP, ports: {C: X1, B: VBIAS, E: X1}
name: Q4, type: PNP, ports: {C: VO, B: P3, E: VBIAS}
name: Q5, type: NPN, ports: {C: X1, B: X1, E: VO}
name: Q6, type: NPN, ports: {C: X1, B: X1, E: VEE}
name: V_I1, type: VoltageSource, value: V_I1, ports: {Np: VI1, Nn: GND}
name: V_I2, type: VoltageSource, value: V_I2, ports: {Np: VI2, Nn: GND}
name: V_BIAS, type: VoltageSource, value: V_BIAS, ports: {Np: VBIAS, Nn: GND}
name: I, type: CurrentSource, value: I, ports: {Np: P1, Nn: VEE}
name: I, type: CurrentSource, value: I, ports: {Np: VCC, Nn: P2}
name: I, type: CurrentSource, value: I, ports: {Np: VCC, Nn: P3}
]
extrainfo:The circuit diagram (a) is a bipolar folded-cascoded differential pair. It consists of NPN transistors (Q1, Q2) forming the differential pair, and PNP transistors (Q3, Q4) as the active load. The circuit is powered by VCC and VEE, with biasing provided by V_BIAS. The output is taken from node VO. The current sources I provide biasing currents for the differential pair and the active load.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: P3, D: P1, G: VI1}
name: M2, type: NMOS, ports: {S: P3, D: P2, G: VI2}
name: M3, type: PMOS, ports: {S: P1, D: X1, G: VBIAS}
name: M4, type: PMOS, ports: {S: P2, D: Vo, G: VBIAS}
name: M5, type: NMOS, ports: {S: VSS, D: X1, G: X1}
name: M6, type: NMOS, ports: {S: VSS, D: Vo, G: X1}
name: VBIAS, type: VoltageSource, value: VBIAS, ports: {Np: VBIAS, Nn: GND}
name: VI1, type: VoltageSource, value: VI1, ports: {Np: VI1, Nn: GND}
name: VI2, type: VoltageSource, value: VI2, ports: {Np: VI2, Nn: GND}
name: I, type: CurrentSource, value: I, ports: {Np: VDD, Nn: P1}
name: I, type: CurrentSource, value: I, ports: {Np: VDD, Nn: P2}
name: I, type: CurrentSource, value: I, ports: {Np: P3, Nn: VSS}
]
extrainfo:The circuit diagram (b) is a CMOS folded-cascoded differential pair. It features a pair of NMOS transistors (M1 and M2) as the input differential pair and PMOS transistors (M3 and M4) as the active load. The NMOS transistors M5 and M6 are used for current mirroring or amplification. The circuit is biased using a voltage source VBIAS and has a current source I for biasing the differential pair. The outputs are taken from the node labeled VO.

FIGURE 4.71 (a) Bipolar and (b) CMOS folded-cascoded differential pairs.
If the active-load mismatches have equal magnitudes as those of the differential pair, the effect of the active load is to make the offset typically $\sqrt{2}$ times as large as that due to the differential pair alone.

### Folded-Cascoded Differential Pairs

A notorious drawback in both circuits of Fig. 4.64 is limited voltage headroom at the output. The upper limit of the output voltage swing (OVS) is reached when $Q_{4} / M_{4}$ is driven to the edge of saturation (EOS), so the bipolar circuit has $v_{O(\max )}=V_{C C}-$ $V_{E C 4(\mathrm{EOS})}$ and the MOS version has $v_{O(\max )}=V_{D D}-V_{O V 4}$. The lower limit of the OVS is reached when $Q_{2} / M_{2}$ is driven to the EOS, so the bipolar circuit has $v_{O(\text { min })}=v_{12}-$ $V_{B E 2}+V_{C E 2(\mathrm{EOS})}$ and the MOS circuit has $v_{O(\min )}=v_{12}-V_{G S 2}+V_{O V 2}=v_{12}-\left(V_{t 2}+\right.$ $\left.V_{O V 2}\right)+V_{O V 2}=v_{12}-V_{t 2}$.

It is the lower limit that poses problems because it depends on $v_{12}$. In fact, the higher $v_{12}$, the less voltage headroom is available at the output.

The above drawback is ingeniously avoided via the folded-cascode arrangements of Fig. 4.71, where it is apparent that the lower limit is now reached when $Q_{6} / M_{6}$ is driven to the edge of saturation. In fact, the bipolar circuit has now $v_{O(\min )}=V_{E E}+$ $V_{C E(\mathrm{EOS})}$ and the MOS version has $v_{O(\text { min })}=V_{S S}+V_{O V 6}$. In both cases $v_{O(\text { min })}$ is independent of $v_{12}$ and is fairly close to the negative supply (more in Problems 4.97 and 4.98).

## 4.10 BIPOLAR OUTPUT STAGES

The primary function of the output stage of a voltage-output circuit is to provide low output resistance in order to reduce output loading. In general-purpose ICs such as op amps, the output stage must be capable of supplying enough current (and thus
power) to meet the needs of a variety of loads, and it should do so while consuming a minimum of standby power. Finally, these functions should be provided over a suitably wide frequency bandwidth, with a minimum of distortion, and with a wide output voltage swing-ideally, from rail to rail. Among the various outputstage configurations available in bipolar technology, the ones that have gained most prominence are the so-called push-pull output stages.

### The Class B Push-Pull Output Stage

A good candidate for the role of output stage is the common-collector (CC) configuration because it accepts a small base current to deliver an emitter current $\beta+1$ times as large. Moreover, the driving source's resistance, reflected to the emitter, is $\beta+1$ times as small. The npn BJT only sources emitter current and the pnp BJT only sinks emitter current, so we need both device types in order to accommodate both polarities. The npn BJT will handle positive voltage alternations, when current is to be pushed into the load; the pnp BJT will handle negative voltage alternations, when current is to be pulled out of the load. Aptly called push-pull stage, the circuit is shown in its basic form in Fig. 4.72a. With reference to its voltage transfer curve (VTC) of Fig. $4.72 b$ we observe the following:

- As long as $v_{I}$ falls within the range $-V_{E B 2(\text { on })}<v_{I}<V_{B E 1(\text { on })}$, both BJTs are off, giving $v_{O}=0$.
- As we raise $v_{I}$ above $V_{B E 1(\text { on })}, Q_{1}$ goes on while $Q_{2}$ continues to remain off. In forward-active operation, $Q_{1}$ acts as an emitter follower with a voltage gain of slightly less than $1 \mathrm{~V} / \mathrm{V}$.
- Raising $v_{I}$ above the positive supply voltage will eventually bring $Q_{1}$ to the edge of saturation (EOS), thus estasblishing the upper limit of the output voltage swing (OVS) as $v_{O(\max )}=V_{C C}-V_{C E 1(\mathrm{EOS})}$.
- As we lower $v_{I}$ below $-V_{E B 2(0 n)}$, the roles of $Q_{1}$ and $Q_{2}$ are interchanged, yielding a symmetric VTC with respect to the origin, and such that $v_{O(\min )}=V_{E E}+V_{E C \text { (EOS) }}$.
image_name:(a)
description:
[
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
name: Rs, type: Resistor, value: Rs, ports: {N1: VI, N2: v1}
name: Q1, type: NPN, ports: {C: VCC, B: v1, E: vO}
name: Q2, type: PNP, ports: {C: VEE, B: v1, E: Vo}
name: RL, type: Resistor, value: RL, ports: {N1: vO, N2: GND}
]
extrainfo:This is a Class B push-pull amplifier circuit. It uses complementary NPN and PNP transistors (Q1 and Q2) to amplify the input signal VI. The circuit introduces distortion due to the dead band between -VEB2(on) and VBE1(on). The output voltage swing is limited by the saturation of Q1 and Q2.
image_name:(b)
description:The graph in Figure 4.72(b) is a Voltage Transfer Characteristic (VTC) graph for a Class B push-pull circuit. It illustrates the relationship between the input voltage \(v_I\) on the x-axis and the output voltage \(v_O\) on the y-axis. Both axes are labeled with voltage units (volts), and the graph is plotted on a linear scale.

Overall Behavior and Trends:
- The graph shows a piecewise linear characteristic with three distinct regions:
1. **Dead Band Region**: In the central region around the origin, the slope is nearly zero. This is the dead band where neither transistor \(Q_1\) nor \(Q_2\) is conducting significantly. This region is bounded by \(-V_{EB2(on)}\) and \(V_{BE1(on)}\).
2. **Positive Slope Region**: As \(v_I\) increases beyond \(V_{BE1(on)}\), the output \(v_O\) increases linearly with a slope of approximately 1 V/V. In this region, \(Q_1\) is on and \(Q_2\) is off.
3. **Negative Slope Region**: As \(v_I\) decreases below \(-V_{EB2(on)}\), the output \(v_O\) decreases linearly with the same slope. Here, \(Q_1\) is off and \(Q_2\) is on.

Key Features and Technical Details:
- **Dead Band**: The graph indicates a dead band between \(-V_{EB2(on)}\) and \(V_{BE1(on)}\), where the output voltage does not change significantly with changes in input voltage.
- **Maximum and Minimum Output Voltages**: The graph shows horizontal asymptotes at \(v_O(\max)\) and \(v_O(\min)\), representing the maximum and minimum output voltages achievable by the circuit.
- **Operating Regions**: The transitions between the dead band and the linear regions are marked by the activation of either \(Q_1\) or \(Q_2\). The graph is symmetric about the origin, reflecting the push-pull nature of the circuit.

Annotations:
- The graph is annotated with the conditions for \(Q_1\) and \(Q_2\) being on or off, indicating the active transistor in each region.
- The slope of the linear regions is noted as approximately 1 V/V, showing the gain in these regions.

This VTC graph effectively demonstrates the behavior of a Class B push-pull amplifier, highlighting the dead band and linear operating regions, and the role of transistors \(Q_1\) and \(Q_2\) in defining the output voltage based on the input voltage.

FIGURE 4.72 (a) Class B push-pull circuit and (b) its VTC.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: VI, E: VO}
name: Q2, type: PNP, ports: {C: VEE, B: VI, E: Vo}
name: vI, type: VoltageSource, ports: {Np: VI, Nn: GND}
name: RL, type: Resistor, value: 1 kΩ, ports: {N1: VO, N2: GND}
]
extrainfo:The circuit is a Class B push-pull amplifier with transistors Q1 and Q2. It operates between VCC (5V) and VEE (-5V). The input voltage is vI, and the output voltage is across RL. The circuit exhibits crossover distortion due to the dead band where neither transistor conducts.
image_name:(b)
description:The graph labeled (b) is a time-domain waveform that illustrates the input and output voltages of a Class B push-pull amplifier circuit over a period of 2 milliseconds. The x-axis represents time in milliseconds (ms), while the y-axis represents waveforms in volts (V). The graph uses a linear scale for both axes.

In this graph, two waveforms are depicted: the input voltage \( v_I \) and the output voltage \( v_O \). The input waveform \( v_I \) is shown as a light gray sinusoidal wave with a peak amplitude of approximately 2 V, oscillating between +2 V and -2 V. The output waveform \( v_O \) is depicted as a darker wave, also sinusoidal, but with noticeable distortion.

The key behavior observed in the output waveform \( v_O \) is the presence of crossover distortion, characterized by flat regions around the zero-crossing points where the waveform does not follow the sinusoidal shape of the input. This distortion occurs due to the dead band, where neither transistor \( Q_1 \) nor \( Q_2 \) conducts, resulting in a lack of output signal in this region.

The output waveform \( v_O \) closely follows the input waveform \( v_I \) during the positive and negative peaks, but deviates significantly around the zero-crossing points. This behavior is typical for a Class B push-pull amplifier, highlighting its efficiency in amplifying signals but also its susceptibility to crossover distortion when handling sine waves. The circuit is better suited for handling square-wave signals to minimize this distortion effect.

FIGURE 4.73 (a) PSpice Class B push-pull circuit and (b) its input and output waveforms.

We can gain additional insight by simulating the circuit via PSpice. As shown in Fig. 4.73, the circuit introduces considerable distortion due to the presence of the dead band $-V_{E B 2(\text { on })}<v_{I}<V_{B E 1(\text { on })}$, over which neither BJT conducts. Called crossover distortion, it is generally intolerable, so the present circuit is relegated primarily to handling square-wave signals, where crossover distortion is not an issue.

This circuit is said to be of the Class B type because each BJT conducts only during half a cycle (actually, because of the nonzero base-emitter voltage drops, the conduction angle is less than $180^{\circ}$ for each BJT).

### The Class AB Push-Pull Output Stage

If we could arrange for both BJTs to be already conductive for $v_{O}=0$, as opposed to having to wait for $v_{I}$ to raise above $V_{B E 1(\mathrm{on})}$ or to drop below $-V_{E B 2(\text { on })}$, then crossover distortion would be eliminated altogether. This requires establishing between the two bases a voltage drop $V_{B B}=V_{B E 1(\text { on })}+V_{E B 2(\text { on })} \cong 2 \times 0.7=1.4 \mathrm{~V}$. To ensure predictable biasing for the BJTs, $V_{B B}$ must closely track the sum of their base-emitter voltage drops, so we need some form of mirror-like operation. In the classic arrangement of Fig. $4.74 a$ the base bias $V_{B B}$ is provided by the pair of diode-connected BJTs $Q_{3}$ and $Q_{4}$ and the associated current generators $I_{1}$ and $I_{2}$. Referred to as a Class AB stage, the circuit yields the much-improved VTC of Fig. 4.74b. By inspection, we find its small-signal output resistance as

$$
\begin{equation*}
R_{o}=\left(\frac{r_{d 3}}{\beta_{01}+1}+r_{e 1}\right) / /\left(\frac{r_{d 4}}{\beta_{02}+1}+r_{e 2}\right) \tag{4.162}
\end{equation*}
$$

where $r_{d 3}$ and $r_{d 4}$ are the dynamic resistances of the diode-connected BJTs, and $r_{e 1}$ and $r_{e 2}$ are the dynamic resistances seen looking into the emitters of the push-pull BJTs. Usually $R_{o}$ is fairly small.

Circuit behavior is best understood via the PSpice example of Fig. 4.75, which uses the $Q_{5}-Q_{6}$ and $Q_{7}-Q_{8}$ current mirrors, along with the reference source $I_{R E F}$, to bias
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: P2, E: Vo}
name: Q2, type: PNP, ports: {C: VEE, B: P1, E: Vo}
name: Q3, type: NPN, ports: {C: P2, B: P2, E: VI}
name: Q4, type: PNP, ports: {C: P1, B: P1, E: VI}
name: RL, type: Resistor, value: RL, ports: {N1: VO, N2: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: VCC, Nn: P2}
name: I2, type: CurrentSource, value: I2, ports: {Np: P1, Nn: VEE}
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
]
extrainfo:The circuit is a Class AB push-pull amplifier using NPN and PNP transistors. It features current mirrors for biasing and a voltage transfer characteristic (VTC) shown in part (b). The output voltage (VO) is determined by the input voltage (VI) and the biasing from the current sources I1 and I2. The load resistor RL is connected to the output node VO.
image_name:(b)
description:The graph in part (b) of the figure is a Voltage Transfer Characteristic (VTC) plot for a Class AB push-pull amplifier circuit. This type of graph is used to show the relationship between the input voltage (V_I) and the output voltage (V_O) of the circuit.

Axes Labels and Units:
- **X-axis:** Represents the input voltage (V_I) in volts.
- **Y-axis:** Represents the output voltage (V_O) in volts.

Overall Behavior and Trends:
- The graph shows a linear relationship between the input and output voltages over a central region. This linear region has a slope approximately equal to 1 V/V, indicating that the output voltage changes at nearly the same rate as the input voltage.
- At the extremes of the input voltage range, the graph levels off, indicating saturation. The output voltage reaches a maximum (V_O(max)) and minimum (V_O(min)) value, beyond which it does not increase or decrease further despite changes in the input voltage.

Key Features and Technical Details:
- **Slope:** The central linear region has a slope of approximately 1 V/V, which is characteristic of an ideal amplifier with unity gain.
- **Saturation Points:** The graph shows distinct saturation points at both high and low input voltages, where the output voltage remains constant at V_O(max) and V_O(min), respectively.

Annotations and Specific Data Points:
- The graph is annotated to show the slope of the linear region and the saturation levels at V_O(max) and V_O(min). These points are critical for understanding the limits of linear operation for the amplifier.

This VTC graph is useful for analyzing the linearity and saturation behavior of the Class AB push-pull amplifier circuit, providing insights into its operational range and limitations.

FIGURE 4.74 (a) Class AB push-pull circuit and (b) its VTC.
the diode-connected $Q_{3}{ }^{-} Q_{4}$ pair at $I_{C 3}=I_{C 4}=I_{R E F}=0.1 \mathrm{~mA}$. Referring also to the waveforms of Fig. 4.76, we make the following considerations:

- For $v_{O}=0$ the current through $R_{L}$ is zero, so $Q_{1}$ and $Q_{2}$ must carry identical currents, or $i_{C 1}=i_{C 2}$. Assuming the $Q_{1}-Q_{3}$ and $Q_{2}-Q_{4}$ pairs are matched, $Q_{1}$ will mirror $Q_{3}$ and $Q_{2}$ will mirror $Q_{4}$ to give $i_{C 1}=i_{C 2}=0.1 \mathrm{~mA}$. This is called
image_name:FIGURE 4.75 (a)
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: X3, E: VO}
name: Q2, type: PNP, ports: {C: VEE, B: X4, E: VO}
name: Q3, type: NPN, ports: {C: X3, B: X3, E: VI}
name: Q4, type: PNP, ports: {C: X4, B: X4, E: VI}
name: Q5, type: PNP, ports: {C: X3, B: X1, E: VCC}
name: Q6, type: PNP, ports: {C: X1, B: X1, E: X1}
name: Q7, type: NPN, ports: {C: X4, B: X2, E: VEE}
name: Q8, type: NPN, ports: {C: X2, B: X2, E: VEE}
name: IREF, type: CurrentSource, value: 0.1 mA, ports: {Np: X1, Nn: X2}
name: VI, type: VoltageSource, ports: {Np: VI, Nn: GND}
name: RL, type: Resistor, value: 1 kΩ, ports: {N1: VO, N2: GND}
]
extrainfo:The circuit is a Class AB bipolar push-pull stage with a quiescent current of 0.1 mA in the diode-connected Q3-Q4 pair. The circuit is powered by VCC (5 V) and VEE (-5 V). The output voltage (VO) is driven by the input voltage (VI) through a pair of complementary transistors Q1 (NPN) and Q2 (PNP) with a load resistor RL of 1 kΩ. The current source IREF sets the reference current for the circuit.
image_name:FIGURE 4.75 (b)
description:The graph in Figure 4.75 (b) is a Voltage Transfer Characteristic (VTC) curve for a Class AB bipolar push-pull stage.

1. **Type of Graph and Function:**
- This is a VTC graph illustrating the relationship between input voltage and output voltage for the circuit.

2. **Axes Labels and Units:**
- The x-axis represents the input voltage \( v_I \) in volts (V), ranging from -5 V to 5 V.
- The y-axis represents the output voltage \( v_O \) in volts (V), also ranging from -5 V to 5 V.
- The graph is plotted on a linear scale with gridlines for better visualization.

3. **Overall Behavior and Trends:**
- The graph shows a linear region where the output voltage \( v_O \) increases proportionally with the input voltage \( v_I \). This linear region is centered around the origin.
- There are slight non-linearities at the beginning and end of the curve, indicating possible saturation or cutoff effects typical in push-pull amplifiers.

4. **Key Features and Technical Details:**
- The graph passes through the origin (0,0), which indicates that the circuit has no offset voltage at zero input.
- The slope of the linear region represents the gain of the amplifier stage. The graph appears to have a unity gain, as the output voltage closely follows the input voltage.
- The non-linear regions at the extremes suggest the limits of the linear operating range, beyond which the amplifier cannot maintain a linear response.

5. **Annotations and Specific Data Points:**
- There are no specific annotations or markers, but the gridlines provide reference points for analyzing the linearity and gain of the circuit.
- The critical point to note is the linearity in the central region, which is crucial for minimizing distortion in the amplifier's output.

FIGURE 4.75 (a) PSpice circuit of a Class AB bipolar push-pull stage, and (b) its VTC.
image_name:(a)
description:The graph labeled '(a)' represents voltage waveforms over time for a Class AB bipolar push-pull stage circuit. The horizontal axis is labeled 'Time t (ms)' and spans from 0 to 2 milliseconds, while the vertical axis is labeled 'Waveforms (V)' and ranges from -2 to 1 volt.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph showing the input and output voltage waveforms.

2. **Axes Labels and Units:**
- **X-axis:** Time in milliseconds (ms)
- **Y-axis:** Voltage in volts (V)

3. **Overall Behavior and Trends:**
- The graph displays two waveforms, $v_I$ (input voltage) and $v_O$ (output voltage), both sinusoidal in nature.
- Both waveforms oscillate with a period of approximately 1 millisecond.
- The input waveform $v_I$ appears slightly larger in amplitude than the output waveform $v_O$.

4. **Key Features and Technical Details:**
- The waveforms are centered around 0 volts, indicating no DC offset.
- The output waveform $v_O$ follows the input waveform $v_I$ closely, demonstrating the linearity of the amplifier in this region.
- There are no annotations or specific markers on the graph, but gridlines are present for reference.

5. **Annotations and Specific Data Points:**
- The critical aspect to note is the linearity in the central region, minimizing distortion in the amplifier's output.
image_name:(b)
description:The graph labeled as "(b)" is a time-domain waveform plot depicting the collector currents in a Class AB bipolar push-pull amplifier stage. The x-axis represents time in milliseconds (ms), ranging from 0 to 2 ms, while the y-axis represents the collector currents in milliamperes (mA), ranging from 0 to 1 mA.

The plot displays two waveforms, labeled as \(i_{C1}\) and \(i_{C2}\), corresponding to the collector currents of the two transistors in the push-pull configuration. Both waveforms exhibit a periodic behavior with a frequency corresponding to the time scale shown, completing a cycle approximately every 1 ms, indicating a frequency of about 1 kHz.

The waveform \(i_{C1}\) is shown in a lighter shade, while \(i_{C2}\) is in a darker shade. Each waveform reaches its peak at about 1 mA and returns to 0 mA at the zero crossings, indicating that the transistors conduct alternately. This behavior is characteristic of push-pull amplifiers, where one transistor conducts while the other is off, minimizing crossover distortion.

The waveforms are symmetric and sinusoidal, reflecting the linearity of the amplifier within the operating range. The critical feature of this graph is the alternating conduction of \(i_{C1}\) and \(i_{C2}\), which is essential for the efficient operation of the Class AB amplifier, balancing conduction time and minimizing power loss.

FIGURE 4.76 (a) Voltage and (b) current waveforms for the PSpice circuit of Fig. 4.75.
the quiescent current $I_{Q}$ of the $Q_{1}-Q_{2}$ pair. For the sake of efficiency, in a welldesigned circuit $I_{Q}$ is kept at the minimum necessary to avoid distortion. It is apparent that $v_{O}=0$ for $v_{I}=0$. When $i_{L}=0$, the circuit is said to be in standby.

- As we increase $v_{l}, v_{O}$ will also increase due to the emitter-follower action by $Q_{1}$. So, the load current $i_{L}=v_{O} / R_{L}$ will also increase, in turn raising $i_{C 1}$. For instance, as $i_{C 1}$ doubles, $v_{B E 1}$ will increase by 18 mV , by the well-known rule of thumb. But, since $v_{B E 1}+v_{E B 2}=V_{B B} \cong$ constant, the $18-\mathrm{mV}$ increase in $v_{B E 1}$ will cause an $18-\mathrm{mV}$ decrease in $v_{E B 2}$, indicating that $i_{C 2}$ will halve. It is apparent from Fig. $4.76 b$ that as $v_{I}$ is raised further, we eventually get $i_{C 2} \rightarrow 0$ and $i_{C 1} \rightarrow i_{L}$.
- For $v_{I}$ sufficiently large, diode $Q_{3}$ will go off, causing $Q_{5}$ to saturate. Consequently, the VTC itself will saturate. The upper limit of the OVS is reached when $Q_{5}$ is brought to the EOS, so we now have

$$
\begin{equation*}
v_{O(\max )}=V_{C C}-V_{E C S(\mathrm{EOS})}-V_{B E 1(\mathrm{on})} \tag{4.163a}
\end{equation*}
$$

For the circuit under consideration, $v_{O(\max )} \cong 5-0.2-0.7=4.1 \mathrm{~V}$.

- As we lower $v_{I}$ below 0 V , the roles of $Q_{1}$ and $Q_{2}$ are interchanged, thus yielding a symmetric VTC. The lower limits of the OVS is

$$
\begin{equation*}
v_{O(\min )}=V_{E E}+V_{C E 7(\mathrm{EOS})}+V_{E B 2(\mathrm{on})} \tag{4.163b}
\end{equation*}
$$

Presently, $v_{O(\text { min })} \cong-4.1 \mathrm{~V}$.
For a better understanding of the interplay among the various currents, we apply KVL to write $v_{B E 1}+v_{E B 2}=V_{B E 3}+V_{E B 4}$. Using the well-known BJT equation we rewrite as

$$
V_{T} \ln \frac{i_{C 1}}{I_{s 1}}+V_{T} \ln \frac{i_{C 2}}{I_{s 2}}=V_{T} \ln \frac{I_{C 3}}{I_{s 3}}+V_{T} \ln \frac{I_{C 4}}{I_{s 4}}
$$

or

$$
V_{T} \ln \left(\frac{i_{C 1}}{I_{s 1}} \frac{i_{c 2}}{I_{s 2}}\right)=V_{T} \ln \left(\frac{I_{C 3}}{I_{s 3}} \frac{I_{C 4}}{I_{s 4}}\right)
$$

For this equality to hold, the arguments of the logarithms must be identical, so we get

$$
\begin{equation*}
i_{C 1} i_{C 2}=\left(\frac{I_{s 1} I_{s 2}}{I_{s 3} I_{s 4}}\right) I_{C 3} I_{C 4} \tag{4.164}
\end{equation*}
$$

indicating that the product $i_{C 1} i_{C 2}$ remains constant. In the example of Fig. 4.75 we have $i_{C 1} i_{C 2}=I_{C 3} I_{C 4}=(0.1 \mathrm{~mA})^{2}=10^{-8} \mathrm{~A}^{2}$. This means that if one of the two currents increases because of $i_{L}$ by a given number of octaves or decades, the other current must decrease by the same number of octaves or decades. As we know, for $i_{L}=0$ the circuit is in standby with $i_{C 1}=i_{C 2}$ and it draws the quiescent current

$$
\begin{equation*}
I_{Q}=\sqrt{\frac{I_{s 1} I_{s 2}}{I_{s 3} I_{s 4}} I_{C 3} I_{C 4}} \tag{4.165}
\end{equation*}
$$

Since all its BJTs are assumed identical, the present circuit has $I_{Q}=0.1 \mathrm{~mA}$.
(a) For the circuit of Fig. $4.75 a$, find $v_{I}$ for $i_{C 1}=0.4 \mathrm{~mA}$. What is the corresponding value of $v_{o}$ ?
(b) Find $v_{I}$ for $v_{O}=-0.25 \mathrm{~V}$. What are the values of $i_{C 1}$ and $i_{C 2}$ ?
(c) Estimate $v_{O}$ if $v_{I}=1.0 \mathrm{~V}$.

#### Solution

(a) Increasing $i_{C 1}$ from 0.1 mA to 0.4 mA (two octaves) will lower $i_{C 2}$ from 0.1 mA to $0.1 /(2 \times 2)=0.025 \mathrm{~mA}$. By KCL, $i_{L}=i_{C 1}-i_{C 2}=0.4-0.025=$ 0.375 mA . By Ohm's law, $v_{O}=R_{L} i_{L}=1 \times 0.375=0.375 \mathrm{~V}$. By the rule of thumb, a two-octave increase in $i_{C 1}$ requires an increase in $v_{B E 1}$ of $2 \times 18=$ 36 mV . Thus, to raise $v_{O}$ from 0 V to 0.375 V , we must raise $v_{I}$ from 0 V to $0.375+0.036=0.411 \mathrm{~V}$.
(b) We now have $i_{L}=v_{O} / R_{L}=-0.25 / 1=-0.25 \mathrm{~mA}$, that is, a $0.25-\mathrm{mA}$ load current flowing into $Q_{2}$ 's emitter. KCL now gives $i_{C 2}=i_{L}+i_{C 1}=0.25 \times$ $10^{-3}+10^{-8} / i_{C 2}$, which we solve to get $i_{C 2}=0.285 \mathrm{~mA}$. Moreover, $i_{C 1}=$ $10^{-8} /\left(0.285 \times 10^{-3}\right)=0.035 \mathrm{~mA}$. Raising $i_{C 2}$ from 0.1 mA to 0.285 mA requires that $v_{E B 2}$ be increased by $(26 \mathrm{mV}) \ln (0.285 / 0.1) \cong 27 \mathrm{mV}$. Consequently, $v_{I}=-0.25-0.027=-0.277 \mathrm{~V}$.
(c) We anticipate $v_{O}$ to be slightly less than 1.0 V . Start out with the initial estimate $v_{O(0)} \cong 1 \mathrm{~V}$ and then iterate. We have $i_{L(0)} \cong 1 / 1=1 \mathrm{~mA}$ and $i_{C 2} \ll i_{C 1}$, so $i_{C 1(0)} \cong i_{L(0)} \cong 1 \mathrm{~mA}$. To increase $i_{C 1}$ from 0.1 mA to 1 mA (one decade), we must increase $v_{B E 1}$ by 60 mV , by the well-known rule of thumb. So, a better estimate is $v_{O(1)}=1.0-0.06=0.94 \mathrm{~V}$. Then, $i_{L(1)}=0.94 / 1=0.94 \mathrm{~mA}$ and $i_{C 2(1)}=10^{-8} /\left(0.94 \times 10^{-3}\right)=0.016 \mathrm{~mA}$. The reader can do one more iteration to verify that the last results are adequate enough.

Overload Protection

Bipolar push-pull stages are notoriously vulnerable to overload conditions such as the inadvertent shorting of the output terminal to ground. When an overload condition arises, the stage upstream will step up the base drive of the overloaded BJT, causing the latter to draw sufficient current to overheat and possibly destroy itself. We need watchdog circuitry to sense the current in each of the push-pull BJTs, and should this current try to exceed a prescribed safety limit, intervene in such a way as to prevent any further current increase. The output stage will no longer perform its intended function, but at least it will be saved from possible destruction.

Shown in Fig. 4.77 is the overload protection circuitry for $Q_{1}$, but a similar concept can be used to protect $Q_{2}$. This circuitry consists of a small series resistance $R_{S C}$ to sense the emitter current of $Q_{1}$, and a watchdog BJT $Q_{5}$ designed to be off under normal operation, but to go on as soon as the load attempts to draw excessive current from $Q_{1}$. Once on, $Q_{5}$ will divert to the load any excess current from the $I_{1}$ source, letting into $Q_{1}$ 's base only the amount necessary to sustain $Q_{1}$ 's conduction at the safety limit. The current sensing resistance is chosen as

$$
\begin{equation*}
R_{\mathrm{SC}}=\frac{V_{B E 5(\mathrm{on})}}{I_{S C}} \tag{4.166}
\end{equation*}
$$

where $V_{B E 5(\text { on })}$ is the voltage needed to turn on $Q_{5}$ and $I_{S C}$ is the maximum allowed current for $Q_{1}$.
image_name:FIGURE 4.77
description:
[
name: I1, type: CurrentSource, value: I1, ports: {Np: VCC, Nn: P1}
name: I2, type: CurrentSource, value: I2, ports: {Np: P3, Nn: VEE}
name: Q1, type: NPN, ports: {C: VCC, B: P1, E: P2}
name: Q2, type: PNP, ports: {C: VEE, B: P3, E: VO}
name: Q3, type: Diode, ports: {Na: P1, Nc: VI}
name: Q4, type: Diode, ports: {Na: VI, Nc: P3}
name: Q5, type: NPN, ports: {C: P1, B: P2, E: VO}
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
name: RSC, type: Resistor, value: RSC, ports: {N1: P2, N2: V0}
name: RL, type: Resistor, value: RL, ports: {N1: VO, N2: GND}
]
extrainfo:The circuit provides overload protection for Q1. Q5 diverts excess current from I1 to maintain Q1's safety limit. RSC is calculated to ensure Q5 turns on at the desired current limit. The circuit is part of a negative-feedback system regulating the output at Vo = 10V.

FIGURE 4.77 Overload protection for $Q_{1}$.

In the circuit of Fig. 4.77 let $\beta_{F 1}=\beta_{F 5}=250, V_{B E 5(\text { on })}=0.7 \mathrm{~V}, I_{1}=I_{2}=300 \mu \mathrm{~A}$,
EXAMPLE 4.29 and $V_{C C}=15 \mathrm{~V}$. Suppose the circuit is part of a negative-feedback system designed to regulate the output at $V_{o}=10 \mathrm{~V}$.
(a) Specify $R_{S C}$ for $I_{S C}=20 \mathrm{~mA}$.
(b) Show all relevant voltages and currents if a student tries the circuit in the lab with $R_{L}=2.0 \mathrm{k} \Omega$.
(c) Repeat if the student, because of a resistance color-code misreading, loads the circuit with $R_{L}=20 \Omega$ instead of $R_{L}=2.0 \mathrm{k} \Omega$.
(d) What is likely to happen if $Q_{1}$ does not have short-circuit protection? Comment on your findings.

#### Solution

(a) $R_{S C}=0.7 / 0.020=35 \Omega$.
(b) With $R_{L}=2.0 \mathrm{k} \Omega$ we have $I_{L}=V_{o} / R_{L}=10 / 2.0=5 \mathrm{~mA}$. As it flows through $R_{\mathrm{SC}}$, this current creates the voltage drop $V_{B E 5}=R_{S C} I_{L}=0.035 \times 5=0.175 \mathrm{~V}$. This is insufficient to turn on $Q_{5}$, so the latter will remain in a dormant state, like a good watchdog should do. To supply $5 \mathrm{~mA}, Q_{1}$ draws the base current $I_{B 1}=$ $I_{E 1} /\left(\beta_{F 1}+1\right)=5 / 251 \cong 20 \mu \mathrm{~A}$. This current comes from the $I_{1}$ source, so the remaining $280 \mu \mathrm{~A}$ go to the diode $Q_{3}$. The situation is illustrated in Fig. 4.78a.
(c) Installing a voracious load such as $R_{L}=20 \Omega$ will pull $V_{O}$ down toward ground. Sensing this drop in $V_{O}$ via the feedback network, the circuitry upstream will try adjusting $v_{I}$ in such a way as to boost the base drive of $Q_{1}$ in order to raise $V_{o}$. In fact, all of $I_{1}$ will now be diverted toward $Q_{1}$, thereby awakening $Q_{5}$ and leading to the overload situation of Fig. 4.78b. Here, $Q_{1}$ 's current is limited
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: 15V, B: P1, E: X1}
name: Q5, type: NPN, ports: {C: P1, B: X1, E: X2}
name: Q3, type: Diode, ports: {Na: P1, Nc: VI}
name: V1, type: VoltageSource, value: V1, ports: {Np: VI, Nn: GND}
name: 35Ω, type: Resistor, value: 35Ω, ports: {N1: X1, N2: X2}
name: 2kΩ, type: Resistor, value: 2kΩ, ports: {N1: X2, N2: GND}
name: 300μA, type: CurrentSource, value: 300μA, ports: {Np: 15V, Nn: P1}
]
extrainfo:The circuit diagram illustrates a feedback mechanism where Q1 and Q5 are used to regulate the current through the load. Under normal conditions, Q1 controls the current to the load, while Q5 remains off. In overload conditions, Q5 activates, diverting excess current to the load. The feedback network adjusts the base drive of Q1 to maintain the output voltage. The circuit includes a 300μA current source, a 15V supply, and resistors for current limiting and feedback.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: 15V, B: P1, E: X1}
name: Q3, type: Diode, ports: {Na: P1, Nc: VI}
name: Q5, type: NPN, ports: {C: P1, B: X1, E: X2}
name: V1, type: VoltageSource, value: V1, ports: {Np: VI, Nn: GND}
name: 2kΩ, type: Resistor, value: 2kΩ, ports: {N1: X2, N2: GND}
name: 300μA, type: CurrentSource, value: 300μA, ports: {Np: 15V, Nn: P1}
]
extrainfo:The circuit operates under overload conditions with a voracious load of 20Ω causing the output voltage VO to drop. Feedback attempts to adjust the input to boost the base drive of Q1, diverting all current towards Q1 and activating Q5. Q1's current is limited to about ISC = 20 mA, and the remaining current is passed on by Q5 directly to the load.

FIGURE 4.78 Circuit of Example 4.29 operating under (a) normal and (b) overload conditions.
to about $I_{S C}=20 \mathrm{~mA}$. To sustain this current, $Q_{1}$ draws the base current $I_{B 1}=I_{S C} /\left(\beta_{F}+1\right)=20 / 251 \cong 80 \mu \mathrm{~A}$. The remaining current of $300-80=$ $220 \mu \mathrm{~A}$ is passed on by $Q_{5}$ directly to the load. Allowing for about $1 \mu \mathrm{~A}$ of base current for $Q_{5}$, we have $I_{E 5}=220+1=221 \mu \mathrm{~A}, I_{L}=20+0.221=$ 20.221 mA , and $V_{O}=20 \times 20.221 \times 10^{-3} \cong 0.4 \mathrm{~V}$. This is a far cry from the intended value $V_{O}=10 \mathrm{~V}$, but at least $Q_{1}$ is spared destruction.
(d) Without protection, $Q_{1}$ would try to draw $I_{E 1}=\left(\beta_{F}+1\right) I_{1}=251 \times 0.3 \cong$ 75 mA , raising the output only to $V_{O}=0.020 \times 75=1.5 \mathrm{~V}$. The power dissipated by $Q_{1}$ would be $P_{1} \cong V_{C E 1} \times I_{C 1}=(15-1.5) 75>1 \mathrm{~W}$, high enough to cause the monolithic BJT $Q_{1}$ most likely to blow out.

## 4.11 CMOS OUTPUT STAGES

As in the bipolar case, a CMOS output stage should provide low output impedance over a wide frequency bandwidth and with a wide OVS—ideally from rail to railwhile consuming a minimum of standby power. As we are about to see, the design of CMOS output stages presents some marked differences compared to the bipolar case.

### The CD Push-Pull Output Stage

In principle, the bipolar Class AB configuration of Fig. 4.75 could be replicated in MOS form as shown in Fig. 4.79. Here, the common-drain (CD) $M_{1}-M_{2}$ pair forms the push-pull stage proper; the diode-connected $M_{3}-M_{4}$ pair biases the $M_{1}-M_{2}$ pair
image_name:FIGURE 4.79(a)
description:
[
name: M1, type: NMOS, ports: {S: Vo, D: VDD, G: X3}
name: M2, type: NMOS, ports: {S: VSS, D: vo, G: x4}
name: M3, type: NMOS, ports: {S: VI, D: X3, G: X3}
name: M4, type: PMOS, ports: {S: x4, D: VI, G: x4}
name: M5, type: PMOS, ports: {S: VDD, D: x3, G: x1}
name: M6, type: PMOS, ports: {S: VDD, D: x1, G: x1}
name: M7, type: NMOS, ports: {S: VSS, D: x4, G: x2}
name: M8, type: NMOS, ports: {S: VSS, D: x2, G: x2}
name: RL, type: Resistor, value: 1kΩ, ports: {N1: vo, N2: 0}
name: IREF, type: CurrentSource, value: 50µA, ports: {Np: x1, Nn: x2}
name: VI, type: VoltageSource, ports: {Np: vi, Nn: 0}
]
extrainfo:The circuit is a CD push-pull output stage with a Class AB configuration. It uses MOSFETs M1 and M2 for the push-pull stage and M3 and M4 for biasing. Current mirrors formed by M5-M6 and M7-M8 provide biasing currents.
image_name:(b)
description:The graph labeled as "(b)" is a Voltage Transfer Characteristic (VTC) plot for a CD push-pull output stage in a CMOS circuit. This type of graph is used to illustrate how the output voltage of a circuit varies with the input voltage.

1. **Type of Graph and Function:**
- This is a Voltage Transfer Characteristic (VTC) graph.
- It shows the relationship between input voltage and output voltage for the CMOS push-pull stage.

2. **Axes Labels and Units:**
- The x-axis represents the input voltage ($V_{I}$) in volts.
- The y-axis represents the output voltage ($V_{O}$) in volts.
- Both axes use a linear scale.

3. **Overall Behavior and Trends:**
- The graph typically shows a linear region where the output voltage closely follows the input voltage.
- At low input voltages, the output voltage is low, indicating the transistors are not fully on.
- As the input voltage increases past the threshold, the output voltage increases linearly, indicating proper conduction through the transistors.
- At high input voltages, the output voltage saturates near the supply voltage, indicating the transistors are fully on.

4. **Key Features and Technical Details:**
- The graph likely includes a threshold voltage point where the transistors begin to conduct significantly.
- There are saturation regions at both low and high input voltages where the output voltage levels off.
- The slope of the linear region can indicate the gain of the stage.

5. **Annotations and Specific Data Points:**
- Critical points such as the threshold voltage and saturation points may be annotated.
- The maximum output voltage is typically close to the supply voltage $V_{DD}$, and the minimum output voltage is near $V_{SS}$.
- Specific numerical values for these points might be marked to indicate the exact behavior of the circuit.

(a)
image_name:(b)
description:The graph is a Voltage Transfer Characteristic (VTC) plot for a CD push-pull output stage, showing the relationship between input voltage ($v_I$) and output voltage ($v_O$). The x-axis represents the input voltage, $v_I$, in volts, ranging from -5V to 5V. The y-axis represents the output voltage, $v_O$, also in volts, with a similar range of -5V to 5V.

The graph exhibits a piecewise linear behavior. At the beginning, for negative input voltages, the output voltage is relatively constant at a low negative value, indicating a saturation region. As the input voltage increases and crosses the threshold, the output voltage begins to increase linearly, depicting the active region of the circuit. This linear region suggests a proportional gain between the input and output voltages.

As the input voltage continues to increase towards positive values, the output voltage again levels off, indicating another saturation region. The leveling off at both extremes suggests that the circuit is designed to limit the output voltage to within a specific range, close to the supply voltages $V_{SS}$ and $V_{DD}$.

Key features include the transition points where the output voltage changes from saturation to linear behavior, which are critical for understanding the biasing and operation of the circuit. These transitions are not numerically marked but are evident from the change in slope on the graph. The maximum and minimum output voltages align closely with the supply voltages, indicating efficient utilization of the voltage range.

(b)

FIGURE 4.79 (a) PSpice circuit of the CD push-pull output stage, and (b) its VTC. (All FETs have $V_{t}=0.75 \mathrm{~V}$ and $\lambda=0.02 \mathrm{~V}^{-1}$; moreover, $k_{1}=k_{2}=4 \mathrm{~mA} / \mathrm{V}^{2}$, and $k_{3}=k_{4}=k_{5}=k_{6}=k_{7}=k_{8}=1.6 \mathrm{~mA} / \mathrm{V}^{2}$.)
for Class AB operation, and the current mirrors $M_{5}-M_{6}$ and $M_{7}-M_{8}$, along with the reference current $I_{R E F}$, provide the necessary current to bias the diode pair. By inspection, the output resistance is

$$
\begin{equation*}
R_{o}=\frac{1}{\left(g_{m 1}+g_{m 2}\right)} / / r_{o 1} / / r_{o 2} \tag{4.167}
\end{equation*}
$$

which is usually low. Using KVL we readily find the limits of the output voltage swing (OVS) as

$$
\begin{align*}
& v_{O(\max )}=V_{D D}-V_{O V 5}-V_{t 1}-v_{O V 1}  \tag{4.168a}\\
& v_{O(\min )}=V_{S S}+V_{O V 7}+\left|V_{t 2}\right|+v_{O V 2} \tag{4.168b}
\end{align*}
$$

We immediately note a glaring difference compared to the bipolar case. While the voltage drops $V_{E C 5(\mathrm{EOS})}+V_{B E 1(\mathrm{on})}$ and $V_{C E 7(\mathrm{EOS})}+V_{E B 2(\mathrm{on})}$ of Eq. (4.163) are relatively constant $(\sim 0.9 \mathrm{~V})$, their counterpart drops $V_{O V 5}+V_{t 1}+v_{O V 1}$ and $V_{O V 7}+\left|V_{t 2}\right|+v_{O V 2}$ of Eq. (4.168) depend on $i_{L}$ via $v_{O V 1}$ and $v_{O V 2}$. Moreover, $V_{t 1}$ and $V_{t 2}$ are subject to the body effect, further reducing the OVS, at whose extremes $V_{t 1}$ and $V_{t 2}$ get maximized. In the CMOS example of Fig. 4.79 the edges of the OVS are within a couple of volts of either supply rail, whereas in the bipolar example of Fig. 4.75 they are approximately fixed and within less than a volt. The limited OVS of the Class AB CD stage can be a serious drawback in low-voltage power supply systems, where better design alternatives are necessary.

### The CMOS Inverter as Output Stage

The OVS can be improved considerably if the FETs of the push-pull pair are operated in the common-source (CS) mode instead of the CD mode. This is the case of the already familiar CMOS inverter, shown again in Fig. 4.80. The ensuing VTC, obtained using the same transistor parameters and load resistance as in Fig. 4.79,
image_name:(a)
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: Vo, G: Vi}
name: M2, type: NMOS, ports: {S: VSS, D: Vo, G: Vi}
name: RL, type: Resistor, value: 1kΩ, ports: {N1: Vo, N2: GND}
name: VI, type: VoltageSource, ports: {Np: Vi, Nn: GND}
name: VDD, type: VoltageSource, value: 5V, ports: {Np: VDD, Nn: GND}
name: VSS, type: VoltageSource, value: -5V, ports: {Np: GND, Nn: VSS}
]
extrainfo:The circuit is a CMOS inverter output stage with a PMOS and NMOS transistor pair. It is powered by a dual power supply of +5V and -5V, and drives a load resistor of 1kΩ. The circuit can swing the output voltage close to the power-supply rails.
image_name:(b)
description:The graph in Figure 4.80(b) is a Voltage Transfer Characteristic (VTC) curve for a CMOS inverter. This graph is a plot of the output voltage \( v_O \) on the vertical axis versus the input voltage \( v_I \) on the horizontal axis. Both axes are labeled in volts, with the input voltage ranging from -5 V to 5 V and the output voltage ranging from -5 V to 5 V as well.

The graph displays a typical inverter characteristic with a clear transition region. At low input voltages (around -5 V), the output voltage is high (close to 5 V), indicating that the inverter is in the logic high region. As the input voltage increases, the output voltage begins to decrease sharply around the threshold region, which is centered near 0 V. This transition is highly nonlinear, reflecting the switching action of the inverter.

At high input voltages (around 5 V), the output voltage is low (close to -5 V), indicating that the inverter is in the logic low region. The curve shows a steep slope in the transition region, which is characteristic of digital inverters, providing a clear distinction between the logic high and logic low states.

Key features include the steep transition around 0 V, which indicates a rapid change from high to low output, and the saturation regions where the output voltage remains constant despite changes in the input voltage. This behavior is typical for CMOS inverters, where the output swings close to the power supply rails, maximizing the logic level separation.

FIGURE 4.80 (a) PSpice circuit of the CMOS inverter, and (b) its VTC. (Both FETs have $k=4 \mathrm{~mA} / \mathrm{V}^{2}, V_{t}=0.75 \mathrm{~V}$, and $\lambda=0.02 \mathrm{~V}^{-1}$.)
clearly shows the circuit's ability to swing its output fairly close to the power-supply rails. However, as an output stage, the inverter suffers from a number of drawbacks: its VTC is highly nonlinear, its output resistance $R_{o}=r_{o 1} / / r_{o 2}$ is usually too high, and and its quiescent current can be intolerably large. (The circuit provides also polarity inversion, but this is not a serious issue as we can deliberately invert signal polarity somewhere else in the system.) For these reasons, the CMOS inverter is relegated to logic-type output circuits such as voltage comparators, where $v_{O}$ sits mostly at either logic level, undergoing only rapid transitions between one logic level and the other.

### The CS Push-Pull Output Stage with Feedback Amplifiers

The shortcomings of the CMOS-inverter output stage are cleverly avoided by separately predistorting the gate drives in such a way as to ensure a fairly linear VTC with a comparatively wide OVS. This task is accomplished by means of negative feedback, according to the principle depicted in Fig. 4.81 $a$. We make the following considerations:

- The circuit is made up of two complementary subcircuits, each consisting of a low-gain op amp and a CS FET connected for negative-feedback operation (note that since the CS configuration provides signal inversion, the ouput is fed back to the op amp's noninverting input, rather than to the more usual inverting input). In this mode of operation each op amp will provide the corresponding FET with whatever gate drive it takes to force $v_{O}$ to track $v_{I}$. Consequently, as long as at least one of the op amps can exercise its negative-feedback control, we expect a fairly linear VTC.
- The op amps, themselves made up of MOSFETs, are deliberately unbalanced for the purpose of setting the quiescent current of the push-pull pair at a specified
image_name:(a)
description:
[
name: vI, type: VoltageSource, value: vI, ports: {Np: VI, Nn: GND}
name: M1, type: PMOS, ports: {S: VDD, D: VO, G: Out(a1)}
name: M2, type: NMOS, ports: {S: GND, D: VO, G: Out(a2)}
name: a1, type: OpAmp, value: a1, ports: {InP: VI-VOS1, InN: VI, OutP: Out(a1), OutN: ', Vdd: , -Vdd:}
name: a2, type: OpAmp, value: a2, ports: {InP: VO, InN: VI+VOS2, OutP: Out(a2), OutN: , Vdd: , -Vdd:}
name: RL, type: Resistor, value: RL, ports: {N1: VO, N2: GND'}
]
extrainfo:The circuit is a CS push-pull output stage with negative feedback to linearize the VTC and reduce output resistance. It includes two op amps driving a PMOS and NMOS, with offset voltages VOS1 and VOS2 for quiescent current setting.
image_name:(b)
description:
[
'name': 'a1', 'type': 'OpAmp', 'value': 'a1', 'ports': {'InP': 'Vo', 'InN': 'GND', 'OutP': 'Out(a1)'}
'name': 'a2', 'type': 'OpAmp', 'value': 'a2', 'ports': {'InP': 'Vo', 'InN': 'GND', 'OutP': 'Out(a2)'}
'name': 'ro1', 'type': 'Resistor', 'value': 'ro1', 'ports': {'N1': 'Vo', 'N2': 'GND'}
'name': 'ro2', 'type': 'Resistor', 'value': 'ro2', 'ports': {'N1': 'Vo', 'N2': 'GND'}
'name': 'gm1vgs1', 'type': 'VoltageControlCurrentSource', 'value': 'vIgm1vgs1 'ports': {'Np': 'VO', 'Nn': 'GND'}
'name': 'gm2vgs2', 'type': 'VoltageControlCurrentSource', 'value': 'vIgm1vgs1 'ports': {'Np': 'VO', 'Nn': 'GND'}
]
extrainfo:The circuit is a push-pull output stage with op-amps providing gate drive to PMOS and NMOS transistors. The op-amps are deliberately unbalanced to set the quiescent current. Negative feedback is used to linearize the VTC and reduce the output resistance. The AC equivalent circuit is used to find the output resistance Ro.

FIGURE 4.81 (a) CS push-pull output stage, and (b) ac equivalent to find its output resistance $R_{0}$.
value, as we shall see in Example 4.30. This imbalance, created by fabricating the two halves of each amplifier with differing $W / L$ ratios, is modeled via the offset voltages $V_{O S 1}$ and $V_{O S 2}$.

- Negative feedback, besides linearizing the VTC, reduces the output resistance $R_{o}$ dramatically. To substantiate, set all independent sources to zero and apply a test source $v_{o}$ as in Fig. 4.81b. By KCL,

$$
i_{o}=\frac{v_{o}}{r_{o 1}}+\frac{v_{o}}{r_{o 2}}+g_{m 1} a v_{o}+g_{m 2} a v_{o}
$$

Collecting, we get

$$
\begin{equation*}
R_{o}=\frac{v_{o}}{i_{o}}=\frac{1}{a\left(g_{m 1}+g_{m 2}\right)} / / r_{o 1} / / r_{o 2} \tag{4.169}
\end{equation*}
$$

which shows a two-fold beneficial effect of negative feedback upon the output resistance: $(a)$ it brings the $g_{m} \mathrm{~s}$ into the picture $\left(1 / g_{m} \ll r_{o}\right)$, and $(b)$ it multiplies them by the gain $a$ to further lower $R_{o}$.

Let the MOSFETs of Fig. $4.81 a$ be matched devices with $k=4 \mathrm{~mA} / \mathrm{V}^{2}, V_{t}=0.75 \mathrm{~V}$, and $\lambda=0.02 \mathrm{~V}^{-1}$. Moreover, let $V_{D D}=-V_{S S}=5.0 \mathrm{~V}$ and $a=10 \mathrm{~V} / \mathrm{V}$.
(a) Specify $V_{O S 1}$ and $V_{O S 2}$ for a standby current $I_{Q}=125 \mu \mathrm{~A}$.
(b) Find the value of $R_{o}$ in standby.
(c) Find $v_{O}$ if $v_{I}=4.0 \mathrm{~V}$ and $R_{L}=1 \mathrm{k} \Omega$.
(d) Use PSpice to display $v_{O}, i_{L}, i_{D 1}, i_{D 2}, v_{G 1}$ and $v_{G 2}$ versus $v_{I}$ for $-5 \mathrm{~V}<v_{I}<+5 \mathrm{~V}$. Hence, comment on your findings.

#### Solution

(a) In standby $\left(v_{O}=v_{I}=0\right)$ both FETs are saturated, so we impose

$$
125 \mu \mathrm{~A}=\frac{1}{2}\left(4 \mathrm{~mA} / \mathrm{V}^{2}\right) V_{O V(S B Y)}^{2}
$$

to obtain $V_{O V(\mathrm{SBY})}=0.25 \mathrm{~V}$. The required gate voltage for $M_{1}$ in standby is $V_{G 1(\mathrm{SBY})}=V_{D D}-V_{t}-V_{O V(S B Y)}=5-0.75-0.25=4 \mathrm{~V}$. But, $V_{G 1(\mathrm{SBY})}$ is generated by the upper op amp as $V_{G 1(\mathrm{SBY})}=a\left(v_{P}-v_{N}\right)$, so imposing $4=$ $10\left[0-\left(-V_{O S 1}\right)\right]$ gives $V_{O S 1}=0.4 \mathrm{~V}$. With matched FETs we have, by symmetry, $V_{O S 2}=V_{O S 1}=0.4 \mathrm{~V}$.
(b) In standby we have $g_{m 1}=g_{m 2}=2 I_{Q} / V_{O V(\text { SBY })}=2 \times 125 \times 10^{-6} / 0.25=$ $1 /(1 \mathrm{k} \Omega)$ and $r_{o 1}=r_{o 2}=1 /\left(\lambda I_{D}\right)=1 /\left(0.02 \times 125 \times 10^{-6}\right)=400 \mathrm{k} \Omega$, so

$$
R_{o}=\frac{1}{10\left(10^{-3}+10^{-3}\right)} / /\left(400 \times 10^{3}\right) / /\left(400 \times 10^{3}\right) \cong 50 \Omega
$$

which is quite low.
(c) For $v_{I}=4.0 \mathrm{~V}$ we expect $v_{O}$ to approach 4 V , indicating that with a relatively small $v_{S D 1}, M_{1}$ is likely to be in the triode region, where

$$
i_{D 1}=k\left[v_{O V 1} v_{S D 1}-\frac{1}{2} v_{S D 1}^{2}\right]=4\left[\left(5-0.75-v_{G 1}\right)\left(5-v_{O}\right)-\frac{1}{2}\left(5-v_{O}\right)^{2}\right]
$$

We also have, by inspection,
$v_{G 1}=a\left(v_{P}-v_{N}\right)=a\left[v_{O}-\left(v_{I}-V_{O S 1}\right)\right]=10\left(v_{O}-(4-0.4)\right]=10\left(v_{O}-3.6\right)$
Moreover, we expect $M_{2}$ to be in cutoff, so we can write

$$
i_{D 1}=i_{L}=\frac{v_{O}}{R_{L}}=\frac{v_{O}}{1}
$$

Eliminating $v_{G 1}$ and $i_{D 1}$ and solving gives the physically acceptable solution $v_{O}=3.88 \mathrm{~V}$ (fairly close to 4 V , as expected). Back substituting gives $v_{G 1}=2.82 \mathrm{~V}$. Since $v_{S D 1}<v_{O V 1}(1.12 \mathrm{~V}<1.43 \mathrm{~V})$, the FET is indeed in the triode region.
(d) Using the PSpice circuit of Fig. 4.82a we obtain the VTC of Fig. 4.82b, which is fairly linear over a wide OVS. The plots of Fig. 4.83a confirm that for $v_{I}=0$ the op amps provide $v_{G 1}=4 \mathrm{~V}$ and $v_{G 2}=-4 \mathrm{~V}$ in order to ensure the voltage overdrives of 0.25 V needed to bias both FETs at $I_{Q}=125 \mu \mathrm{~A}$. As $v_{I}$ moves away from 0 V , one of the FETs goes off while the other takes on the task of feeding the load. Even more revealing are the plots of Fig. 4.83b, showing how the op amps predistort the gate drives $v_{G 1}$ and $v_{G 2}$ in order to ensure a fairly linear voltage transfer characteristic, especially toward the extremes of the OVS. The predistorting action by negative feedback will be investigated more systematically in Chapter 7.
image_name:Figure 4.82 (a)
description:
[
name: VI, type: VoltageSource, ports: {Np: VI, Nn: GND}
name: VOS1, type: VoltageSource, ports: {Np: VDD, Nn: InN(U1)}
name: VOS2, type: VoltageSource, ports: {Np: InN(U2), Nn: VI}
name: U1, type: OpAmp, value: U1, ports: {InP: VO, InN: InN(U1), OutP: VG1, OutN: ', Vdd: , -Vdd:}
name: U2, type: OpAmp, value: U2, ports: {InP: VO, InN: InN(U2), OutP: VG2, OutN: , Vdd: , -Vdd:}
name: M1, type: PMOS, ports: {S: VDD, D: VO, G: VG1}
name: M2, type: NMOS, ports: {S: VSS, D: VO, G: VG2}
name: RL, type: Resistor, value: 1 kΩ, ports: {N1: VO, N2: GND'}
]
extrainfo:The circuit is a push-pull stage using PMOS and NMOS transistors driven by op-amps to achieve linear voltage transfer. The op-amps predistort the gate voltages to maintain linearity. The circuit is biased at ±5 V supply voltages with an output load resistor of 1 kΩ.
image_name:Figure 4.82 (b)
description:The graph in Figure 4.82 (b) is a Voltage Transfer Characteristic (VTC) plot. It depicts the relationship between the input voltage \( v_I \) on the x-axis and the output voltage \( v_O \) on the y-axis. Both axes are labeled in volts (V), and the scales are linear, ranging from -5 V to 5 V.

Overall Behavior and Trends:
The graph shows a linear relationship between the input and output voltages, forming a straight line with a slope of approximately 1. This indicates that the circuit provides a near unity gain, meaning the output voltage closely follows the input voltage.

Key Features and Technical Details:
- **Linear Region:** The line passes through the origin (0,0), suggesting a direct proportionality without any offset.
- **Symmetry:** The graph is symmetric about the origin, indicating that the circuit behaves similarly for both positive and negative input voltages.
- **Range:** The input and output voltages both range from -5 V to 5 V, showing the operational limits of the circuit.

Annotations and Specific Data Points:
There are no specific annotations or markers on the graph. However, the linearity and symmetry are crucial characteristics, ensuring that the circuit can handle both positive and negative signals effectively without distortion. This behavior is expected from a push-pull stage circuit designed to enhance linearity over a wide range of input voltages.

FIGURE 4.82 (a) PSpice circuit of the CS push-pull stage of Example 4.30, and (b) its VTC. (Both FETs have $k=4 \mathrm{~mA} / \mathrm{V}^{2}, V_{t}=0.75 \mathrm{~V}$, and $\lambda=0.02 \mathrm{~V}^{-1}$; both op amps have $a=10 \mathrm{~V} / \mathrm{V}$ and $V_{\text {oS }}=0.4 \mathrm{~V}$.)
image_name:(a)
description:The graph in Figure 4.83(a) is a current transfer characteristic curve for a CS push-pull stage circuit. This type of graph is used to illustrate how different currents in the circuit vary with respect to an input voltage.

1. **Type of Graph and Function:**
- The graph is a current transfer characteristic curve.

2. **Axes Labels and Units:**
- The x-axis represents the input voltage $v_I$ in volts (V), ranging from -5 V to 5 V.
- The y-axis represents the currents in milliamperes (mA), ranging from -5 mA to 5 mA.

3. **Overall Behavior and Trends:**
- The graph shows three distinct current curves: $i_{D1}$, $i_{D2}$, and $i_L$.
- $i_{D1}$ increases linearly with increasing $v_I$, starting from -5 mA at $v_I = -5$ V to 5 mA at $v_I = 5$ V.
- $i_{D2}$ decreases linearly with increasing $v_I$, starting from 5 mA at $v_I = -5$ V to -5 mA at $v_I = 5$ V.
- $i_L$ remains constant at 0 mA across the entire range of $v_I$.

4. **Key Features and Technical Details:**
- The crossing point of $i_{D1}$ and $i_{D2}$ occurs at the origin (0 V, 0 mA), indicating a balanced push-pull operation.
- The linearity of $i_{D1}$ and $i_{D2}$ suggests a symmetrical response to positive and negative input voltages.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for each current curve ($i_{D1}$, $i_{D2}$, and $i_L$), clearly marking their paths and behaviors.
- No specific numerical markers or additional reference lines are present beyond the standard gridlines.
image_name:(b)
description:The graph in Figure 4.83(b) is a voltage transfer curve (VTC) for a CS push-pull stage circuit. It plots various output voltages against the input voltage \( v_I \), which ranges from -5 V to 5 V.

1. **Type of Graph and Function:**
- This is a voltage transfer curve (VTC), showing the relationship between input and output voltages in a circuit.

2. **Axes Labels and Units:**
- The x-axis represents the input voltage \( v_I \) in volts (V), ranging from -5 V to 5 V.
- The y-axis represents the output voltages in volts (V), also ranging from -5 V to 5 V.
- The scale on both axes is linear.

3. **Overall Behavior and Trends:**
- The graph shows three curves: \( v_O \), \( v_{G1} \), and \( v_{G2} \).
- \( v_O \) follows a linear path through the origin, indicating a direct proportionality between input and output voltages.
- \( v_{G1} \) and \( v_{G2} \) exhibit nonlinear behavior, curving downward and upward respectively as the input voltage moves away from zero.

4. **Key Features and Technical Details:**
- The curve \( v_O \) is linear, indicating that the output voltage increases linearly with the input voltage.
- \( v_{G1} \) shows a decreasing trend as the input voltage increases, suggesting a voltage drop across a component in the circuit.
- \( v_{G2} \) increases as the input voltage increases, indicating a voltage rise.
- These curves reflect the characteristics of the push-pull stage, with \( v_O \) representing the main output and \( v_{G1} \) and \( v_{G2} \) showing the gate voltages of the FETs.

5. **Annotations and Specific Data Points:**
- The graph is marked with the labels \( v_O \), \( v_{G1} \), and \( v_{G2} \) to indicate the respective curves.
- There are no specific numerical annotations for data points, but the behavior of each curve is clear from the graph's general shape.

FIGURE 4.83 (a) Current and (b) voltage transfer curves for the PSpice circuit of Fig. 4.82a.

## APPENDIX 4A

Editing SPICE Netlists

The MOSFET models available in the Eval library of Version 9.2 of PSpice refer to devices with body and source tied together. However, if we want to investigate the body effect, we can readily untie the two terminals and connect the body to the MNV in the case of $n$ MOSFETs or to the MPV in the case of $p$ MOSFETs by suitably editing the circuit's netlist. (A netlist is an internal code to which PSpice automatically converts the circuit entered via the Schematic Capture facility, before performing the actual simulation.)

To illustrate, refer to the PSpice example of Fig. 4.27. Once we have created the circuit schematic via the Place $\rightarrow$ Part and Place $\rightarrow$ Wire commands, we first use PSpice $\rightarrow$ Create Netlist to direct PSpice to generate the netlist, and then we use PSpice $\rightarrow$ View Netlist to visualize it. The result is the following lines of code:

| * source | CKT_of_Fig_4.27 |
| :--- | :--- |
| M_M1 | VDD I O O Mn |
| V_V1 | VDD 0 5Vdc |
| V_V2 | 0 VSS 5Vdc |
| V_VS | I O OVdc |
| I_ID | O VSS DC 250uA |

We are interested in the second line, which refers to the MOSFET $M_{1}$ of Fig. 4.27, renamed by PSpice as M_M1. The remaining entries in this line refer to the circuit's nodes to which the Drain, Gate, Source, and Body (in that order) are connected. These are, respectively, the power supply (VDD), the input node (I), the output node $(\mathrm{O})$, and again the output node (O). The last entry (Mn) refers to the PSpice model for
$M_{1}$, which has been created in accordance with Appendix 3A to reflect the characteristics listed in the caption of Fig. 4.27. This model is

```
.model Mn NMOS(Kp=100u Vto=0.5V Lambda=0.05 Gamma=0.75
+ Phi=0.6)
```

We now edit (overwrite) the netlist by modifying the second line as follows:

```
* source CKT_of_Fig_4.27
M_M1 VDD I O VSS Mn W=10u L=1u
V_V1 VDD 0 5Vdc
V_V2 0 VSS 5Vdc
V_vS I 0 OVdc
I_ID O VSS DC 250uA
```

The body, formely connected to the source ( 0 ), is now connected to the negative power supply (VSS). Moreover, the model name (Mn) is followed by the specifications of the channel width and length ( $\mathrm{W}=10 \mathrm{u} \quad \mathrm{L}=1 \mathrm{u}$ ). This is particularly convenient in multi-transistor circuits, where all FETs share the same process parameters as specified in a common model ( Mn in this case), but each device is assigned its individual W and L values in the netlist line where the device appears.

Once the netlist has been edited, we must save it via the File $\rightarrow$ Save commands. We finally launch the simulation of the circuit pertaining to the modified netlist via the PSpice $\rightarrow$ Run commands, as usual.
