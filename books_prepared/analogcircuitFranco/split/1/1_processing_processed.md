# 1. Diodes and the pn Junction
Chapter Outline
1.1 The Ideal Diode 3
1.2 Basic Diode Applications 10
1.3 Operational Amplifiers and Diode Applications 21
1.4 Semiconductors 25
1.5 The pn Junction in Equilibrium 34
1.6 Effect of External Bias on the SCL Parameters 39
1.7 The pn Diode Equation 43
1.8 The Reverse-Biased pn Junction 50
1.9 Forward-Biased Diode Characteristics 53
1.10 Dc Analysis of pn Diode Circuits 58
1.11 Ac Analysis of pn Diode Circuits 67
1.12 Breakdown-Region Operation 76
1.13 Dc Power Supplies 84
Appendix 1A: SPICE Models for Diodes 90
References 93
Problems 93
The diode is the most basic electronic device. In fact, its invention, over a century ago, is credited with ushering in the era of electronics. Like the resistor, the diode comes with two terminals; however, unlike the bidirectional resistor, the diode carries current only in one direction. For a qualitative understanding of how this can happen, think of the early diodes, which were of the vacuum-tube type. A vacuum diode had an incandescent filament called a cathode, acting as a copious source of free electrons, and a plate called an anode, to control current flow. Applying a positive voltage to the anode relative to the cathode would attract the negatively charged electrons and thus sustain electron flow from cathode to anode. Conversely, applying a negative voltage to the anode would repel the electrons and thus inhibit electron flow. By a hydraulic analogy, the diode can be visualized as a one-way valve.
The vacuum-tube diode was invented by John A. Fleming in 1904. Just two years later, in 1906, Greenleaf W. Pickard invented an alternative diode type by forming a point contact to a slab of silicon, thus creating the first solid-state electronic device. However, it took half a century for the semiconductor industry to become a commercial reality, so the first half of the twentieth century was dominated by vacuum-tube electronics.
Nowadays diodes are made of semiconductor materials, with dramatic advantages over their vacuum-tube counterparts in terms of miniaturization, reliability, power consumption and cost. Specifically, the most common diode today is the silicon $p n$ junction, though other types of materials and junctions are also in use. The $p n$ junction plays a central role in microelectronics in that not only does it provide the diode function at the basis of the above applications, but it is also at the basis of the bipolar junction transistor (BJT), the junction field-effect transistor (JFET), and other semiconductor devices such as the silicon-controlled rectifier (SCR). The $p n$ junction is also present in the metal-oxide-semiconductor field-effect transistor (MOSFET), the device most widely used in today's microelectronics products. Furthermore, in its reverse-biased form, the pn junction is used to isolate from each other different devices coexisting on the same semiconductor chip.
The student who comes from prerequisite courses in linear circuits will immediately find that diodes, like the transistors to follow, are highly nonlinear devices. Mercifully, a number of techniques have been developed for the analysis of nonlinear devices that draw quite heavily from those covered by linear-circuits courses. Far from being a waste of time, the analytical tools learned in circuits courses will also be put to heavy use in the study of electronics. Specifically, Ohm's Law, Kirchhoff's Laws (KVL and KCL), the Voltage/Current Divider Rules, Thévenin's/Norton's Theorems, and the Superposition Principle will continue to be our precious analytical tools as we venture into the exciting realm of electronic devices and systems.
CHAPTER HIGHLIGHTS
The chapter begins with the ideal diode, a concept designed to develop a basic feel for diode behavior as well as introduce the student to nonlinear circuit analysis techniques, the backbone of all subsequent electronics. The applications covered are diode rectifiers, diode logic gates, voltage clamps, piecewise-linear function generators, peak detectors, dc restorers, and voltage multipliers.
Next, we review the basic operational amplifier principles of prerequisite circuits courses because diodes (and later, transistors) offer a fertile application ground for op amps. The first diode-op-amp application to be considered is full-wave rectification, but others will follow as we proceed.
As mentioned, today diodes are made of semiconductors, so the next objective is the study of basic $p n$ junction theory. After a review of the semiconductor basics normally covered in prerequisite physics courses, the chapter develops an intuitive discussion of the $p n$ junction, highlighting those practical aspects (rules of thumb) that form the working knowledge of the electronics engineer in the modern industrial milieu. Whether the student will pursue a career as an IC designer, or a product, process, or reliability engineer, or as a test or applications engineer, the pn junction will
always resurface in a variety of situations, so it is only appropriate that we address it in some depth. All the student needs to remember from basic physics is Gauss's Theorem as well as the relationship between electric field and potential,
$$
\frac{d E}{d x}=\frac{\rho(x)}{\varepsilon_{s i}} \quad E=-\frac{d v(x)}{d x}
$$
The outcome of $p n$ junction theory is the concept of a real-life diode, a device that in spite of its departure from the ideal diode is still analyzed via suitable linearizing techniques. This introduces the student to the large-signal model as well as the small-signal model for the diode, models that will be expanded further in the following chapters when we study transistors.
The last part of the chapter applies the above models to the study of a number of widely used practical circuits such as rectifiers, voltage references, basic nonlinear op amp circuits, and dc power supplies. The Appendix discusses the parameters intervening in the diode model used by SPICE.
Most likely the chapter covers more material than feasible in a typical junior course. But, the instructor can easily skip selected topics, such as the sections on semiconductor theory, especially if these topics are covered in alternative courses. I have written this chapter with the aim to have all (or almost all) pertinent diode material in one place.
## 1.1 THE IDEAL DIODE
The diode is a two-terminal device designed to conduct current in one direction only. Unlike the resistor, which conducts in either direction, the diode carries current only from the terminal called anode $(A)$ to the terminal called cathode $(C)$. Its circuit symbol, shown in Fig. 1.1a, uses an arrowhead to signify this directionality. The voltage across the diode is defined as positive at the anode and negative at the cathode, thus conforming to the passive sign convention of other popular devices such as resistors.
image_name:(a)
description:The diagram shows the ideal diode symbol and its characteristic curve. The 'ON' region indicates forward bias where current flows from anode (A) to cathode (C). The 'CO' region indicates reverse bias where no current flows.
image_name:(b)
description:The graph in Figure 1.1 (b) is an ideal diode \(i\)-\(v\) characteristic graph. This graph illustrates the relationship between the current \(i\) and the voltage \(v\) across a diode in two distinct regions: the ON region and the cut-off (CO) region.
1. **Type of Graph and Function:**
- This is a characteristic curve graph for an ideal diode, commonly used in electronics to show how current and voltage relate in a diode.
2. **Axes Labels and Units:**
- The horizontal axis represents voltage \(v\) and is marked with zero at the origin. Positive voltage is to the right, and negative voltage is to the left.
- The vertical axis represents current \(i\) and is marked with zero at the origin. Positive current is upwards, and negative current is downwards.
3. **Overall Behavior and Trends:**
- In the ON region, when the diode is forward-biased (positive voltage), the current increases sharply with a very small increase in voltage, indicating that the diode conducts.
- In the CO region, when the diode is reverse-biased (negative voltage), the current is zero, indicating that the diode does not conduct.
4. **Key Features and Technical Details:**
- The ON region is marked on the graph where the current is positive, and the voltage is positive. This indicates that the diode is conducting.
- The cut-off region is marked where the current remains zero despite the negative voltage, indicating the diode is not conducting.
- The graph uses arrows to represent the direction of current flow in both regions. In the ON region, the arrow points upwards, signifying positive current flow. In the CO region, the arrow points to zero current.
5. **Annotations and Specific Data Points:**
- The graph includes labels "ON" and "CO" at the corresponding regions to indicate the diode's operational state.
- The diode symbols with anode \(A\) and cathode \(C\) terminals are shown next to the graph, demonstrating the direction of current flow and voltage polarity in both regions.
FIGURE 1.1 (a) Circuit symbol and sign convention for the diode. (b) Ideal-diode $i$-v characteristic and diode models in the on (ON) region and in the cut-off (CO) region of operation.
image_name:(a)
description:The circuit diagram '(a)' shows a simple series circuit with a voltage source, a diode, and a load. The diode is forward-biased, allowing current 'i' to flow from the source through the diode to the load. The valve analogy illustrates the forward operation of the diode, where it acts as a closed valve allowing flow from the pump to the tank.
image_name:(b)
description:The system block diagram labeled "(b)" illustrates the reverse operation of a diode using a valve analogy. This diagram is divided into two main sections: an electrical circuit and a mechanical analogy.
**Main Components:**
1. **Electrical Circuit:**
- **Diode:** Shown with the standard symbol, indicating the direction of current flow. In this diagram, the diode is reverse-biased, meaning it does not conduct current.
- **Source:** Represented by a voltage source symbol, providing electrical power.
- **Load:** Indicated as a block in the circuit, representing the component that would consume power if current were flowing.
2. **Mechanical Analogy:**
- **Tank and Pump:** The tank represents the load, and the pump represents the source of power. The valve analogy is used to show the direction of flow.
**Flow of Information or Control:**
- In the electrical circuit, the current flow is attempted in the reverse direction through the diode, but the diode blocks this flow, resulting in zero current (as indicated by the label "0").
- In the mechanical analogy, the valve is closed, preventing the flow from the tank to the pump, which corresponds to the diode's blocking action in the reverse-biased condition.
**Labels, Annotations, and Key Indicators:**
- The arrow on the diode symbol in the circuit indicates the direction of conventional current flow, which in this case is blocked.
- The label "0" next to the current arrow in the circuit emphasizes that no current flows when the diode is reverse-biased.
**Overall System Function:**
The primary function of this diagram is to illustrate the behavior of a diode in reverse operation. In this state, the diode acts as an open circuit, preventing any current flow. The valve analogy helps to conceptualize this by showing the closed valve that stops fluid flow from the tank to the pump, mirroring the diode's function in the electrical circuit. This demonstrates the diode's role as a one-way device, allowing current to flow only in the forward direction when not reverse-biased.
FIGURE 1.2 Valve analogy of a diode: (a) forward operation and (b) reverse operation.
When invited to draw current in the direction of its arrowhead ( $i>0$ ), also called the forward ( F ) direction, a diode will eagerly conduct the given current by acting as a short circuit $(v=0)$. In this case the diode is said to be forward biased, or also to be on (ON). However, if we try to force current in the opposite direction, also called the reverse $(\mathrm{R})$ direction, the diode will stubbornly oppose current flow by acting as an open circuit $(i=0)$. The diode is now said to be reverse biased, or also to be cut off $(\mathrm{CO})$. When cut off the diode will sustain whatever voltage $(v<0)$ is imposed by the surrounding circuitry.
Figure $1.1 b$ shows the $i-v$ characteristic of the diode, which we express mathematically as
$$
\begin{align*}
v=0 & \text { for } i>0  \tag{1.1a}\\
i=0 & \text { for } v<0 \tag{1.1b}
\end{align*}
$$
Also shown next to the curves are the diode models (a short circuit and an open circuit) corresponding to the two modes of operation. A device with the characteristic shown is referred to as an ideal diode. As we shall see, practical diodes will only approximate these idealized curves.
A diode can be likened to a water valve according to the analogy of Fig. 1.2. The valve hinges at the top and has a stopper at the bottom. Forcing electric current to a load via a diode is like pumping water to a tank via a pipe equipped with a valve. If pump pressure is applied in the forward direction, the valve will open and allow water to flow as in Fig. 1.2a. However, if pressure is applied in the reverse direction as in Fig. 1.2b, the valve will close and inhibit water flow. To develop a feel for diode operation, let us consider our first circuit example.
EXAMPLE 1.1 (a) In the circuit of Fig. 1.3 let $R_{1}=1 \mathrm{k} \Omega$ and $R_{2}=2 \mathrm{k} \Omega$. If $v_{S}=3 \mathrm{~V}$, find $i_{S}$ so that $D$ draws 1 mA . Show the final circuit.
(b) If $i_{S}=3 \mathrm{~mA}$, find $v_{S}$ so that $D$ drops 2 V . Show the circuit.
(c) If $i_{S}=2 \mathrm{~mA}$ and $v_{S}=6 \mathrm{~V}$, find $R_{1}$ and $R_{2}$ so that $D$ operates at the origin of the $i-v$ plane, where $v=0$ and $i=0$.
image_name:Figure 1.3
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: X2, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: X1, N2: Vs}
name: D, type: Diode, ports: {Na: X2, Nc: X1}
name: is, type: CurrentSource, value: is, ports: {Np: X2, Nn: GND}
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
]
extrainfo:The circuit consists of a current source is, a diode D, and two resistors R1 and R2. The current source is connected to node X2, which is also connected to the anode of diode D and one terminal of resistor R1. The cathode of the diode is connected to node X1, which is also connected to one terminal of resistor R2. The other terminal of R2 is connected to the positive terminal of the voltage source Vs. The negative terminal of the voltage source and one terminal of R1 are connected to the ground.
FIGURE 1.3 Circuit of Example 1.1.
#### Solution
(a) In conduction $D$ acts as a short-circuit, so $v_{A}=v_{C}$. By Ohm's law and KVL, $v_{A}=v_{C}=(2 \mathrm{k} \Omega) \times(1 \mathrm{~mA})+(3 \mathrm{~V})=5 \mathrm{~V}$, causing the $1-\mathrm{k} \Omega$ resistance to draw $(5 \mathrm{~V}) /(1 \mathrm{k} \Omega)=5 \mathrm{~mA}$, flowing downward. KCL gives $i_{S}=(1 \mathrm{~mA})+$ $(5 \mathrm{~mA})=6 \mathrm{~mA}$, so the situation is as in Fig. 1.4a.
image_name:(a)
description:
[
name: Current Source 1, type: CurrentSource, value: 6 mA, ports: {Np: X, Nn: GND}
name: R1, type: Resistor, value: 1 kΩ, ports: {N1: X, N2: GND}
name: R2, type: Resistor, value: 2 kΩ, ports: {N1: A, N2: V}
name: Voltage Source 1, type: VoltageSource, value: 3 V, ports: {Np: V, Nn: GND}
]
extrainfo:In this circuit, a 6 mA current source feeds node X. R1 connects node X to ground. A 1 mA current source is connected between nodes A and C, with R2 connecting node A to V. A 3 V voltage source is connected between node V and ground. Node C is at the same potential as node A due to the diode short-circuit assumption.
image_name:(b)
description:
[
name: Current Source 2, type: CurrentSource, value: 3 mA, ports: {Np: X, Nn: GND}
name: R3, type: Resistor, value: 1 kΩ, ports: {N1: X, N2: GND}
name: R4, type: Resistor, value: 2 kΩ, ports: {N1: C, N2: V}
name: Voltage Source 2, type: VoltageSource, value: 5 V, ports: {Np: V, Nn: GND}
]
extrainfo:The circuit diagram (b) involves a current source of 3 mA connected to node X, which is also connected to a 1 kΩ resistor to ground. Another 2 kΩ resistor is connected between nodes A and V, with a 5 V voltage source connected between nodes V and C. Node C is 2 V higher than node A.
FIGURE 1.4 Circuit solutions to Example 1.1.
(b) In cutoff $D$ acts as an open circuit, so the $2-\mathrm{k} \Omega$ resistance drops 0 V . By Ohm's law, $v_{A}=3 \times 1=3 \mathrm{~V}$. By KVL, the voltage at the cathode is $v_{C}=v_{A}+2=3+2=5 \mathrm{~V}$, so $v_{S}=v_{C}=5 \mathrm{~V}$ as shown in Fig. 1.4b.
(c) $i=0 \Rightarrow v_{C}=v_{S}=6 \mathrm{~V} ; v=0 \Rightarrow v_{A}=v_{C}=6 \mathrm{~V}$ and $R_{1}=v_{A} / i_{S}=6 / 2=$ $3 \mathrm{k} \Omega$. As long as $D$ is cut off, the value of $R_{2}$ is irrelevant. $R_{2}$ has an impact only when $D$ is on.
#### Finding the Operating Mode of a Diode
Even though it consists of two straight segments, the diode characteristic is nonlinear. (In fact, it is said to be piecewise linear.) Yet, as demonstrated by Example 1.1, we can still apply the analytical techniques learned in linear-circuits courses because at any given time the diode operates only in one of its two possible modes (either ON or CO), where it admits a model (open or short circuit) that is indeed linear. Thus, to carry out our analysis, we only need to determine which of the two modes the diode happens to be operating in at a given time.
image_name:(a)
description:
[
name: Voc, type: VoltageSource, value: Voc, ports: {Np: X2, Nn: X1}
name: Req, type: Resistor, value: Req, ports: {N1: X2, N2: X3}
name: Diode, type: Diode, ports: {Na: X3, Nc: X1}
]
extrainfo:The circuit contains a voltage source Voc, a resistor Req, and a diode. The diode is connected with its anode at node X3 and cathode at node X1. The load lines for different Voc polarities are shown in figures (b) and (c).
image_name:(b)
description:The graph labeled "(b)" is a load line diagram used in the context of diode circuit analysis. This type of graph is a plot of current (i) versus voltage (v), often used to determine the operating point of a diode within a circuit.
1. **Type of Graph and Function:**
- The graph is a load line diagram, commonly used in electronics to analyze circuits containing nonlinear components like diodes.
2. **Axes Labels and Units:**
- The horizontal axis (x-axis) represents voltage (v), typically measured in volts.
- The vertical axis (y-axis) represents current (i), usually measured in amperes.
- The scales on both axes are linear, as is typical for load line diagrams.
3. **Overall Behavior and Trends:**
- The load line is a straight line with a negative slope, indicating a linear relationship between current and voltage as determined by the circuit's Thévenin equivalent resistance \( R_{eq} \).
- The slope of the load line is \(-1/R_{eq}\), showing the inverse relationship between current and voltage.
- The load line intersects the voltage axis at \( v_{OC} \), the open-circuit voltage, and the current axis at a point determined by \( v_{OC}/R_{eq} \).
4. **Key Features and Technical Details:**
- The load line is annotated with a point labeled \( Q_F \), which represents the forward operating point of the diode when \( v_{OC} > 0 \).
- The intersection of the load line with the diode's characteristic curve determines the actual operating point of the diode.
- The slope \(-1/R_{eq}\) is significant as it reflects the resistance of the circuit seen by the diode.
5. **Annotations and Specific Data Points:**
- The diagram includes an annotation for the load line for \( v_{OC} > 0 \), indicating the condition under which the forward operating point \( Q_F \) is relevant.
- The point \( Q_F \) is where the diode's characteristic curve intersects with the load line, defining the diode's current and voltage under the given conditions.
This graph is essential for visualizing how the diode will behave in the circuit, allowing for the determination of its operating point based on the surrounding linear circuit components.
image_name:(c)
description:The graph labeled (c) is a load line analysis diagram for a diode circuit. It is used to determine the operating point of the diode when the open-circuit voltage \( v_{OC} \) is less than zero.
1. **Type of Graph and Function:**
- This is a load line graph, commonly used in diode and transistor circuits to find the operating point by intersecting the load line with the device's characteristic curve.
2. **Axes Labels and Units:**
- The horizontal axis represents the voltage \( v \) across the diode.
- The vertical axis represents the current \( i \) through the diode.
- Both axes are linear, with the origin marked at (0,0).
3. **Overall Behavior and Trends:**
- The load line is a straight line with a negative slope, indicating a linear relationship between \( v \) and \( i \) when considering the external circuit's resistance \( R_{eq} \).
- The slope of the line is \(-1/R_{eq}\), showing that as the voltage across the diode decreases, the current increases linearly.
4. **Key Features and Technical Details:**
- The line intersects the horizontal axis at \( v_{OC} \), which is negative in this case, indicating the open-circuit voltage.
- The point \( Q_R \) on the load line represents the quiescent or operating point of the diode for \( v_{OC} < 0 \).
5. **Annotations and Specific Data Points:**
- The load line is annotated with "Load line for \( v_{OC} < 0 \)" to specify the condition under which this line applies.
- The slope \(-1/R_{eq}\) is indicated with a right-angle marker, emphasizing the resistance's role in determining the line's slope.
This graph helps in analyzing the diode's behavior when embedded in a linear circuit with a negative open-circuit voltage, allowing for the determination of current and voltage across the diode at the operating point \( Q_R \).
There are many situations in which the diode is embedded in a linear circuit, indicating that we can simplify our analysis significantly if we replace the surrounding circuitry with its Thévenin equivalent. After doing so we end up with the basic situation of Fig. 1.5a, where $v_{O C}$ is the open-circuit voltage that the external circuit would sustain between the nodes corresponding to the anode and the cathode, but with the diode removed. (Note that the polarity of $v_{O C}$ is defined positive at the point of connection to the anode!) Moreover, $R_{e q}$ is the external circuit's equivalent resistance as seen by the diode. Shown in Fig. $1.5 b$ and $1.5 c$ is the $i-v$ characteristic of the diode as well as that of the surrounding circuit, the latter being referred to as the load line. As we know from basic circuit theory, the load line is a straight line intercepting the $v$-axis at $v=v_{O C}$, and having a slope of $-1 / R_{e q}$. The circuit's operating point lies at the intersection of the diode curve and the load line, where the diode and the surrounding circuit share the same voltage and current. It is apparent that
- If $v_{O C}>0$, the operating point $\left(Q_{F}\right)$ lies on the ON segment, where the diode is forward biased and thus acts as a short circuit to yield
$$
\begin{equation*}
v=0 \quad i=\frac{v_{O C}}{R_{e q}}(>0) \tag{1.2a}
\end{equation*}
$$
- Conversely, if $v_{O C}<0$, the operating point $\left(Q_{R}\right)$ lies on the CO segment, where the diode is reverse biased and thus acts as an open circuit to yield
$$
\begin{equation*}
i=0 \quad v=v_{O C}(<0) \tag{1.2b}
\end{equation*}
$$
Let us illustrate via an actual example.
EXAMPLE 1.2 (a) Find $v$ and $i$ in the circuit of Fig. $1.6 a$ if $v_{S}=12 \mathrm{~V}, R_{1}=10 \mathrm{k} \Omega, R_{2}=30 \mathrm{k} \Omega$, and $R_{3}=R_{4}=15 \mathrm{k} \Omega$.
(b) Repeat, but with $R_{2}$ lowered from $30 \mathrm{k} \Omega$ to $2.0 \mathrm{k} \Omega$.
(c) What happens if we reverse the diode's direction in part (a)? In part (b)?
image_name:(a)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vs, N2: X1}
name: R2, type: Resistor, value: R2, ports: {N1: X1, N2: GND}
name: R3, type: Resistor, value: R3, ports: {N1: Vs, N2: X2}
name: R4, type: Resistor, value: R4, ports: {N1: X2, N2: GND}
name: Diode, type: Diode, ports: {Na: X1, Nc: X2}
]
extrainfo:The circuit consists of a voltage source Vs, four resistors (R1, R2, R3, R4), and a diode. The diode is oriented with its anode connected to node X1 and cathode to node X2. The resistors form two voltage dividers, one with R1 and R2, and the other with R3 and R4. The circuit is grounded.
image_name:(b)
description:
[
name: VS, type: VoltageSource, value: VS, ports: {Np: VS, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: VS, N2: X1}
name: R2, type: Resistor, value: R2, ports: {N1: X1, N2: GND}
name: R3, type: Resistor, value: R3, ports: {N1: VS, N2: X2}
name: R4, type: Resistor, value: R4, ports: {N1: X2, N2: GND}
name: VOC, type: VoltageSource, value: VOC, ports: {Np: X1, Nn: X2}
]
extrainfo:The circuit diagram (b) represents a subcircuit for finding the Thévenin equivalent voltage (VOC) across nodes X1 and X2, with resistors R1, R2, R3, and R4 forming a network around the voltage source VS.
image_name:(c)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: GND, N2: X1}
name: R2, type: Resistor, value: R2, ports: {N1: X1, N2: GND}
name: R3, type: Resistor, value: R3, ports: {N1: GND, N2: X2}
name: R4, type: Resistor, value: R4, ports: {N1: X2, N2: GND}
]
extrainfo:The circuit diagram (c) shows a simplified network with resistors R1, R2, R3, and R4 connected to form two parallel branches between nodes X1 and X2. The equivalent resistor Req is placed between these nodes.
FIGURE 1.6 (a) Circuit of Example 1.2. (b), (c) Subcircuits to find the Thévenin's equivalent of the network surrounding the diode. Note that the diode has been removed.
#### Solution
(a) Removing the diode yields the subcircuit of Fig. $1.6 b$, where the voltage divider rule gives
$$
v_{O C}=\left(\frac{R_{2}}{R_{1}+R_{2}}-\frac{R_{4}}{R_{3}+R_{4}}\right) v_{S}
$$
Substituting the given component values gives $v_{O C}=9-6=3 \mathrm{~V}$. Since $v_{O C}>0$, the diode will be on, acting as a short circuit with $v=0$. To find $i$, we need $R_{e q}$. To this end, we suppress the voltage source to obtain the subcircuit of Fig. 1.6c. By inspection,
$$
R_{e q}=\left(R_{1} / / R_{2}\right)+\left(R_{3} / / R_{4}\right)
$$
Substituting the given component values gives $R_{e q}=15 \mathrm{k} \Omega$. Consequently, by Eq. $(1.2 a), i=3 / 15=0.2 \mathrm{~mA}$. The situation is shown in Fig. $1.7 a$, where the student is encouraged to find all other voltages and currents in the circuit as a check.
image_name:Fig. 1.7a
description:
[
name: V1, type: VoltageSource, value: 12 V, ports: {Np: V1, Nn: GND}
name: R1, type: Resistor, value: 10 kΩ, ports: {N1: V1, N2: V2}
name: R2, type: Resistor, value: 30 kΩ, ports: {N1: V2, N2: GND}
name: R3, type: Resistor, value: 15 kΩ, ports: {N1: V1, N2: V3}
name: R4, type: Resistor, value: 15 kΩ, ports: {N1: V3, N2: GND}
]
extrainfo:The circuit in Fig. 1.7a includes a voltage source, a current source, and resistors forming a network. The total equivalent resistance is calculated as 15 kΩ, and the current through the current source is 0.2 mA.
image_name:Fig. 1.7b
description:
[
name: V1, type: VoltageSource, value: 12V, ports: {Np: V1, Nn: GND}
name: R1, type: Resistor, value: 10kΩ, ports: {N1: V1, N2: A}
name: R2, type: Resistor, value: 2kΩ, ports: {N1: A, N2: GND}
name: R3, type: Resistor, value: 15kΩ, ports: {N1: V1, N2: C}
name: R4, type: Resistor, value: 15kΩ, ports: {N1: C, N2: GND}
]
extrainfo:The circuit is a voltage divider with a diode acting as an open circuit since the voltage across it is negative. The voltage at node A is 2V, and at node C is 6V.
FIGURE 1.7 Circuit of Example 1.2a, where the diode is on, and Example 1.1b, where the diode is off.
(b) With $R_{2}$ lowered to $2.0 \mathrm{k} \Omega$ we get $v_{O C}=2-6=-4 \mathrm{~V}$. Since we now have $v_{O C}<0$, the diode is off, acting as an open circuit with $i=0$. The situation is depicted in Fig. 1.7b.
(c) Reversing the diode direction so that the anode is now at the right and the cathode is at the left will cause the diode to be off in part (a) and on in part ( $b$ ). Thus, in part ( $a$ ) the diode current is zero, and the diode voltage is -3 V . In part (b) we get $R_{e q}=(10 / / 2)+(15 / / 15)=55 / 6 \mathrm{k} \Omega, v=0 \mathrm{~V}$, and $i=4 /(55 / 6)=24 / 55 \mathrm{~mA}$, now flowing toward the left.
#### Cut-and-Try Approach
If the diode is part of a nonlinear circuit, as in the case of multiple-diode circuits, it is generally not possible to perform a Thévenin's reduction of the surrounding circuitry. However, knowing that the diode must be either on or off, we can use intuition to make an educated assumption, and then check that our results are consistent with our assumption, changing the assumption if needed, until we obtain consistent results. A two-diode circuit provides a classic example of the cut-and-try approach.
EXAMPLE 1.3 (a) The circuit of Fig. $1.8 a$ is powered by a dual $\pm 6-\mathrm{V}$ dc power supply system, which we show in concise form (that is, without drawing the actual dc voltage sources) in order to reduce cluttering in the circuit diagram. Find the current $I_{D}$ and voltage $V_{D}$ for each diode.
(b) Repeat, but with the resistances interchanged with each other.
image_name:(a)
description:
[
name: R1, type: Resistor, value: 1kΩ, ports: {N1: X1, N2: +6V}
name: R2, type: Resistor, value: 3kΩ, ports: {N1: X2, N2: -6V}
name: D1, type: Diode, ports: {Na: X1, Nc: GND}
name: D2, type: Diode, ports: {Na: X1, Nc: X2}
name: +6V, type: VoltageSource, value: +6V, ports: {Np: +6V, Nn: GND}
name: -6V, type: VoltageSource, value: -6V, ports: {Np: GND, Nn: -6V}
]
extrainfo:The circuit is a dual diode configuration with a dual ±6V power supply. Diode D1 is connected to ground, while D2 is connected to a 3kΩ resistor leading to the -6V source. The 1kΩ resistor connects the +6V source to the node X1, which is common to both diodes. This configuration allows for different conduction states of the diodes based on the applied voltage.
image_name:(b)
description:
[
name: V1, type: VoltageSource, value: +6 V, ports: {Np: +6 V, Nn: X1}
name: R1, type: Resistor, value: 1 kΩ, ports: {N1: +6 V, N2: X1}
name: D1, type: Diode, ports: {Na: X1, Nc: GND}
name: R2, type: Resistor, value: 3 kΩ, ports: {N1: X1, N2: -6 V}
name: D2, type: Diode, ports: {Na: X1, Nc: X2}
name: V2, type: VoltageSource, value: -6 V, ports: {Np: X2, Nn: -6 V}
]
extrainfo:The circuit consists of two diodes (D1, D2), two resistors (1 kΩ, 3 kΩ), and two voltage sources (+6 V, -6 V). The current through D1 is 4 mA and through D2 is 2 mA, with a total of 6 mA flowing through the 1 kΩ resistor.
FIGURE 1.8 (a) Circuit of Example 13.a. (b) The circuit after it has been solved.
#### Solution
(a) Knowing that each diode has to be either in conduction (ON) or cut off $(\mathrm{CO})$, we have four possibilities: $\left(D_{1}, D_{2}\right)=(\mathrm{CO}, \mathrm{CO}),(\mathrm{CO}, \mathrm{ON}),(\mathrm{ON}, \mathrm{CO})$, (ON, ON). However, considering that the $+6-\mathrm{V}$ source tends to source current to both anodes, and that the $-6-\mathrm{V}$ source tends to sink current from $D_{2}$ 's cathode, it seems reasonable to assume that both diodes be on, or $\left(D_{1}, D_{2}\right)=$ (ON, ON). Thus, replacing each diode with a short circuit, we end up with the situation of Fig. 1.5b, where the diode voltages are
$$
V_{D_{1}}=V_{D_{2}}=0 \mathrm{~V}
$$
Moreover, applying first Ohm's law and then KCL we have
$$
I_{D_{2}}=I_{3 \mathrm{k} \Omega}=\frac{0-(-6)}{3}=2 \mathrm{~mA} \quad I_{D_{1}}=I_{1 \mathrm{k} \Omega}-I_{D_{2}}=\frac{6-0}{1}-2=4 \mathrm{~mA}
$$
Both diodes carry current in the forward direction, so our results are consistent with our initial assumption, and we are done.
image_name:(a)
description:
[
name: D1, type: Diode, ports: {Na: X1, Nc: GND}
name: D2, type: Diode, ports: {Na: X1, Nc: X2}
name: R1, type: Resistor, value: 3kΩ, ports: {N1: +6V, N2: X1}
name: R2, type: Resistor, value: 1kΩ, ports: {N1: X2, N2: -6V}
name: V1, type: VoltageSource, value: +6V, ports: {Np: +6V, Nn: GND}
name: V2, type: VoltageSource, value: -6V, ports: {Np: GND, Nn: -6V}
]
extrainfo:The circuit consists of two diodes D1 and D2, two resistors R1 (3kΩ) and R2 (1kΩ), and two voltage sources V1 (+6V) and V2 (-6V). Diode D1 is connected to ground, and diode D2 is connected between two nodes X1 and X2. The circuit demonstrates a basic diode-resistor network with voltage sources.
image_name:(b)
description:
[
name: D1, type: Diode, ports: {Na: X1, Nc: GND}
name: D2, type: Diode, ports: {Na: X1, Nc: X2}
name: R1, type: Resistor, value: 3kΩ, ports: {N1: V1, N2: X1}
name: R2, type: Resistor, value: 1kΩ, ports: {N1: X2, N2: V2}
name: V1, type: VoltageSource, value: +6V, ports: {Np: V1, Nn: GND}
name: V2, type: VoltageSource, value: -6V, ports: {Np: X2, Nn: GND}
]
extrainfo:The circuit diagram represents a scenario where both diodes D1 and D2 are initially assumed to be ON. The current through R1 is 2 mA and through R2 is 6 mA, leading to a 4 mA current through D1 in the forward direction.
image_name:(c)
description:
[
name: D1, type: Diode, ports: {Na: X1, Nc: GND}
name: D2, type: Diode, ports: {Na: X1, Nc: X2}
name: R1, type: Resistor, value: 3kΩ, ports: {N1: +6V, N2: X1}
name: R2, type: Resistor, value: 1kΩ, ports: {N1: X2, N2: -6V}
name: V1, type: VoltageSource, value: +6V, ports: {Np: +6V, Nn: GND}
name: V2, type: VoltageSource, value: -6V, ports: {Np: GND, Nn: -6V}
]
extrainfo:The circuit represents a diode-resistor network with two voltage sources, showing the current distribution and voltage drop across the components. D1 is not conducting any current, while D2 is conducting 3 mA.
FIGURE 1.9 (a) Circuit of Example 1.3b. (b) First attempt (wrong), and (c) second attempt (successful).
(b) Swapping the resistances results in the circuit of Fig. 1.9a. We may again assume the state $\left(D_{1}, D_{2}\right)=(\mathrm{ON}, \mathrm{ON})$ and refer to the circuit of Fig. $1.9 b$ for our calculations. By Ohm's law, $I_{3 \mathrm{k} \Omega}=6 / 3=2 \mathrm{~mA}$ and $I_{1 \mathrm{k} \Omega}=[0-(-6)] / 1=6 \mathrm{~mA}$. Then, to satisfy KCL, $D_{1}$ would have to supply 4 mA flowing upward, that is, in the reverse direction. But this is impossible, indicating that the assumption $\left(D_{1}, D_{2}\right)=(\mathrm{ON}, \mathrm{ON})$ was wrong. Yet, we note that $D_{2}$ must be ON because the negative supply draws current from its cathode. The only plausible assumption is thus $\left(D_{1}, D_{2}\right)=(\mathrm{CO}, \mathrm{ON})$, as shown in Fig. 1.9c. We now have
$$
I_{D_{1}}=0 \quad I_{D_{2}}=\frac{6-(-6)}{3+1}=3 \mathrm{~mA}
$$
By KVL, the voltage at the node common to the anodes is $6-(3 \times 3)=-3 \mathrm{~V}$, indicating that $D_{1}$ is indeed reverse biased, as assumed at the onset of our second try. So, $V_{D_{1}}=-3 \mathrm{~V}$, and $V_{D_{2}}=0$.
#### Exercise 1.1
Find $I_{D}$ and $V_{D}$ for each diode in the circuit of Fig. $1.9 a$ if (a) the direction of $D_{1}$ is reversed while $D_{2}$ is as shown; (b) the direction of $D_{2}$ is reversed while $D_{1}$ is as shown; $(c)$ the direction of each diode in Fig. 1.9a is reversed.
Ans. (a) $I_{D_{1}}=4 \mathrm{~mA}, V_{D_{1}}=0, I_{D_{2}}=6 \mathrm{~mA}, V_{D_{2}}=0$; (b) $I_{D_{1}}=2 \mathrm{~mA}, V_{D_{1}}=0$, $I_{D_{2}}=0, V_{D_{2}}=-6 \mathrm{~V}$; (c) $I_{D_{1}}=I_{D_{2}}=0, V_{D_{1}}=-6 \mathrm{~V}, V_{D_{2}}=-12 \mathrm{~V}$.
### Concluding Observations
Even though the diode is the simplest electronic element, it offers a glimpse into important features that are common to other more complex electronic devices, such as transistors to be studied later.
- The diode is a classic example of a nonlinear circuit element.
- Strictly speaking, the analysis techniques learned in linear-circuits courses cannot be applied to nonlinear elements. However, every attempt should be made to
approximate the $i-v$ characteristics with piecewise linear segments, for then we can create separate linear models for the device, one for each region of operation.
- Once we know which region the device finds itself operating in at a given moment, we can apply familiar linear-analysis techniques to investigate its behavior over that particular region.
Quite often a cut-and-try approach may be required in order to determine the actual region of operation. This approach involves the following steps:
- Start out by making an educated assumption about the region of operation of each nonlinear device.
- Replace each device with the linear model pertaining to that region, and proceed with a linear analysis of the resulting circuit.
- Check that the results are consistent with your initial assumption. If they are, we are finished. If they aren't, we need to change our initial assumption until consistent results are obtained.
We shall encounter plenty of examples as we proceed. Lastly, it must be said that computer simulation, such as PSpice, is a powerful tool not only to corroborate any assumptions that we make, but also to provide refinements and details that a piecewise linear approximation of necessity often misses.
## 1.2 BASIC DIODE APPLICATIONS
Having introduced the fundamentals of diode behavior and diode circuit analysis, we are now ready to examine some of the most common diode applications.
### Rectifiers
Figure $1.10 a$ depicts one of the most popular diode applications, namely, signal rectification. During the positive alternations of $v_{I}$ the diode is on and the circuit gives $v_{O}=v_{I}$ (see Fig. 1.10b). During the negative alternations of $v_{I}$ the diode is cut off, and the circuit gives $v_{O}=0 \mathrm{~V}$ (see Fig. 1.10c). Figure 1.11a shows the response $v_{O}$ to a sinusoidal input $v_{I}$. We say that the circuit passes on to the load $R$ only the positive portions of the input waveform, while the negative portions are inhibited. We observe that while $v_{I}$ alternates in polarity and averages out to zero, $v_{O}$ is unipolar and thus exhibits a nonzero average, or a nonzero dc component. For this reason the circuit is referred to as rectifier. Its behavior can be visualized also via the voltage
image_name:(a)
description:
[
name: V_I, type: VoltageSource, value: V_I, ports: {Np: V_I, Nn: GND}
name: D1, type: Diode, ports: {Na: V_I, Nc: X1}
name: R, type: Resistor, value: R, ports: {N1: X1, N2: GND}
]
extrainfo:The circuit is a half-wave rectifier. It allows only the positive portions of the input waveform to pass through, resulting in a unipolar output voltage with a nonzero average.
image_name:(b)
description:
[
name: V_I, type: VoltageSource, ports: {Np: V_I, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: V_O, N2: GND}
]
extrainfo:This is a half-wave rectifier circuit. In this configuration, when the input voltage v_I is greater than 0, the output voltage v_O equals v_I. When v_I is less than 0, the output voltage v_O is 0.
image_name:(c)
description:
[
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: VO, N2: GND}
]
extrainfo:The circuit is a half-wave rectifier where the diode is omitted in case (c), resulting in no current flow and zero output voltage when the input voltage is negative.
FIGURE 1.10 (a) Half-wave rectifier and its equivalent circuits for (b) $v_{l}>0$ and (c) $v_{l}<0$.
image_name:(a)
description:The graph labeled (a) consists of two time-domain waveform plots, representing the input and output voltages of a half-wave rectifier circuit.
1. **Type of Graph and Function:**
- The graph is a time-domain waveform plot.
- It shows the behavior of input and output voltages over time for a half-wave rectifier.
2. **Axes Labels and Units:**
- The horizontal axis represents time, labeled as "Time t."
- The vertical axes represent voltage, labeled as "Input v_I" for the top plot and "Output v_O" for the bottom plot.
- Both voltages are measured in volts, though specific units are not marked.
3. **Overall Behavior and Trends:**
- The top plot shows a sinusoidal waveform representing the input voltage, v_I, which oscillates above and below zero, indicating alternating current (AC).
- The bottom plot shows the output voltage, v_O, which only has positive half-cycles of the input waveform, characteristic of a half-wave rectifier. The negative half-cycles are clipped to zero.
4. **Key Features and Technical Details:**
- The input voltage waveform is a continuous sinusoid, crossing zero at regular intervals.
- The output voltage waveform matches the positive peaks of the input but remains at zero during the negative half-cycles.
- This behavior results from the diode allowing current to pass only when the input voltage is positive, effectively rectifying the AC input.
5. **Annotations and Specific Data Points:**
- There are no specific numerical values or annotations provided in this graph, but the behavior is consistent with the mathematical expression of a half-wave rectifier: v_O = v_I for v_I > 0 and v_O = 0 for v_I < 0.
image_name:(b)
description:The graph in Figure 1.11(b) is a Voltage Transfer Characteristic (VTC) plot for a half-wave rectifier circuit. This plot illustrates the relationship between the output voltage \( v_O \) and the input voltage \( v_I \).
1. **Type of Graph and Function:**
- The graph is a Voltage Transfer Characteristic (VTC) curve.
2. **Axes Labels and Units:**
- The horizontal axis represents the input voltage \( v_I \), marked with positive and negative directions.
- The vertical axis represents the output voltage \( v_O \).
- Units are typically in volts, though not explicitly labeled here.
3. **Overall Behavior and Trends:**
- For positive input voltages \( v_I > 0 \), the output voltage \( v_O \) increases linearly with a slope of +1 V/V, indicating a direct proportionality where \( v_O = v_I \).
- For negative input voltages \( v_I < 0 \), the output voltage \( v_O \) remains at 0, indicating no output.
- The graph demonstrates a piecewise linear behavior.
4. **Key Features and Technical Details:**
- The graph has a clear inflection at \( v_I = 0 \), where the behavior changes from no output for negative inputs to a linear increase for positive inputs.
- The slope of the line for positive input is +1 V/V, representing the gain of the rectifier when the diode conducts.
- This VTC is characteristic of a half-wave rectifier without a diode, as it only allows positive half-cycles to pass through.
5. **Annotations and Specific Data Points:**
- The line for \( v_I > 0 \) is marked with a slope annotation of +1 V/V.
- The origin (0,0) is a critical point where the transition occurs.
This graph effectively visualizes the behavior of the half-wave rectifier circuit, highlighting the rectification process by showing output only for positive input voltages while blocking negative inputs.
FIGURE 1.11 Illustrating half-wave rectification via (a) the input/output waveforms and ( $b$ ) the VTC.
transfer curve (VTC), representing the plot of $v_{O}$ versus $v_{I}$. This curve, expressed mathematically as
$$
\begin{array}{ll}
v_{O}=v_{I} & \text { for } v_{I}>0 \\
v_{O}=0 & \text { for } v_{I}<0 \tag{1.3b}
\end{array}
$$
is shown in Fig. 1.11b. Needless to say, the presence of the diode results in a nonlinear VTC. The student can easily verify that reversing the diode interconnection in Fig. 1.10a results in a rectifier that passes only the negative portions of the input waveform.
Since it passes only half the input wave, the circuit of Fig. 1.10a is called a halfwave rectifier. By contrast, a full-wave rectifier passes both halves of the input wave, one unchanged and the other inverted. Also called absolute-value circuit, it is implemented using the four-diode arrangement of Fig. 1.12a, known as a diode bridge. To understand its operation, consider first the case $v_{I}>0$, then the case $v_{I}<0$.
- For $v_{I}>0$ we expect the input source $v_{I}$ to source current to $D_{1}$ 's anode and to sink current from $D_{4}$ 's cathode, causing both diodes to be on, as depicted in Fig. 1.12b. Under these circumstances we have $v_{O}=v_{I}(>0)$. Moreover, we note that both $D_{2}$ and $D_{3}$ are reverse biased by the amount $v_{0}$, as also shown in Fig. 1.12b. The current loop is thus source $\rightarrow D_{1} \rightarrow R \rightarrow D_{4} \rightarrow$ source.
image_name:(a)
description:
[
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
name: D1, type: Diode, ports: {Na: VI, Nc: X1}
name: D2, type: Diode, ports: {Na: GND, Nc: X1}
name: D3, type: Diode, ports: {Na: X2, Nc: VI}
name: D4, type: Diode, ports: {Na: X2, Nc: GND}
name: R, type: Resistor, value: R, ports: {N1: X1, N2: X2}
]
extrainfo:The circuit is a full-wave rectifier with diodes D1 and D4 conducting when vI > 0, and diodes D2 and D3 conducting when vI < 0. The output voltage vO is taken across the resistor R.
image_name:(a)
description:
[
name: vI, type: VoltageSource, value: vI, ports: {Np: VI, Nn: GND}
name: D1, type: Diode, ports: {Na: VI, Nc: X1}
name: D2, type: Diode, ports: {Na: GND, Nc: X1}
name: D3, type: Diode, ports: {Na: X2, Nc: VI}
name: D4, type: Diode, ports: {Na: X2, Nc: GND}
name: R, type: Resistor, value: R, ports: {N1: X1, N2: X2}
]
extrainfo:The circuit is a full-wave rectifier. Diodes D1 and D4 conduct when vI > 0, and diodes D2 and D3 conduct when vI < 0. The output voltage vO is taken across the resistor R.
(b)
image_name:(c)
description:
[
name: vI, type: VoltageSource, value: vI, ports: {Np: GND, Nn: VI}
name: D1, type: Diode, ports: {Na: GND, Nc: X1}
name: D2, type: Diode, ports: {Na: GND, Nc: X1}
name: D3, type: Diode, ports: {Na: X2, Nc: VI}
name: D4, type: Diode, ports: {Na: X2, Nc: GND}
name: i, type: CurrentSource, ports: {Np: X1, Nn: X2}
name: vO, type: VoltageSource, ports: {Np: X1, Nn: X2}
]
extrainfo:The circuit is a full-wave rectifier operating with vI < 0. Diodes D2 and D3 conduct, allowing current to flow through the resistor R, generating the output voltage vO across R.
(c)
FIGURE 1.12 (a) Full-wave rectifier and its equivalent circuits for (b) $v_{l}>0$ and (c) $v_{l}<0$.
image_name:(a)
description:The graph in Figure 1.13(a) depicts the input and output waveforms of a full-wave rectifier circuit. It consists of two separate plots aligned vertically.
1. **Input Waveform (Top Plot):**
- **Type:** Time-domain waveform.
- **Axes:**
- The horizontal axis represents time \( t \) (units not specified, but typically in seconds or milliseconds).
- The vertical axis represents the input voltage \( v_I \), with a baseline of 0 volts.
- **Behavior:**
- The waveform is sinusoidal, oscillating symmetrically above and below the 0-volt line, indicating an AC input.
- The peaks and troughs are equidistant from the baseline, showing a consistent amplitude.
2. **Output Waveform (Bottom Plot):**
- **Type:** Time-domain waveform.
- **Axes:**
- The horizontal axis represents time \( t \), consistent with the input waveform.
- The vertical axis represents the output voltage \( v_O \), again with a baseline of 0 volts.
- **Behavior:**
- The waveform is rectified, meaning it only oscillates above the 0-volt line, indicating that negative portions of the input waveform have been inverted.
- The output shows a series of peaks corresponding to the absolute value of the input waveform, demonstrating the full-wave rectification process.
3. **Overall Characteristics:**
- The input waveform is a pure sine wave, while the output waveform is a series of positive half-cycles.
- This transformation is typical of a full-wave rectifier, which converts both halves of the AC input into a unidirectional output.
- The frequency of the output waveform is twice that of the input, reflecting the rectification process where each cycle of the input results in two peaks in the output.
image_name:(b)
description:The graph in figure (b) is a Voltage Transfer Characteristic (VTC) plot for a full-wave rectifier circuit. The graph is a piecewise linear plot showing the relationship between the input voltage \(v_I\) on the horizontal axis and the output voltage \(v_O\) on the vertical axis.
1. **Axes Labels and Units:**
- The horizontal axis represents the input voltage \(v_I\) and is marked with a zero point, extending in both the negative and positive directions.
- The vertical axis represents the output voltage \(v_O\), also marked with a zero point.
- The scales are linear, and there are no specific units marked, but it is implied to be volts for both axes.
2. **Overall Behavior and Trends:**
- The plot is symmetric about the origin, forming a 'V' shape.
- For positive values of \(v_I\), the slope of the line is \(+1\) V/V, indicating that the output voltage \(v_O\) equals the input voltage \(v_I\).
- For negative values of \(v_I\), the slope of the line is \(-1\) V/V, indicating that the output voltage \(v_O\) is the negative of the input voltage \(v_I\).
- This behavior reflects the operation of a full-wave rectifier, where negative input voltages are inverted to positive output voltages.
3. **Key Features and Technical Details:**
- The graph intersects at the origin (0,0), which is a key point where both input and output voltages are zero.
- The slopes of \(+1\) V/V and \(-1\) V/V on either side of the origin are significant, highlighting the rectification process.
4. **Annotations and Specific Data Points:**
- The graph is annotated with the slopes \(+1\) V/V and \(-1\) V/V, emphasizing the linear relationship in each region.
Overall, this VTC graph clearly illustrates the function of a full-wave rectifier, showing how input voltages are transformed into output voltages by inverting negative inputs to positive outputs, while maintaining the magnitude of positive inputs.
FIGURE 1.13 Illustrating full-wave rectification via (a) the input/output waveforms and (b) the VTC.
- For $v_{I}<0$ we expect the input source $v_{I}$ to sink current from $D_{3}$ 's cathode and to source current to $D_{2}$ 's anode, causing both diodes to be on, as depicted in Fig. 1.12c. We now have $v_{O}=-v_{I}$, or $v_{O}>0$ because $v_{I}<0$. Moreover, both $D_{1}$ and $D_{4}$ are now reverse biased, as also shown in Fig. 1.12c. The current loop is now source $\rightarrow$ $D_{2} \rightarrow R \rightarrow D_{3} \rightarrow$ source. We observe that the current through $R$ flows toward the right in both cases, confirming the absolute-value function mentioned earlier.
Figure $1.13 a$ shows the response $v_{O}$ to a sinusoidal input $v_{I}$, while Fig. $1.13 b$ shows the VTC, which we express concisely as
$$
\begin{equation*}
v_{O}=\left|v_{I}\right| \tag{1.4}
\end{equation*}
$$
Rectifier circuits find application in power electronics, communications, and instrumentation.
EXAMPLE 1.4 (a) Shown in Fig. 1.14 is a simple-if not overly efficient—circuit for charging a $12-\mathrm{V}$ car battery. Assuming $v_{S}$ is an ac source with a $24-\mathrm{V}$ peak amplitude obtained from the household ac power via a step-down transformer, sketch and label $v_{S}$ as well as the battery current $i$.
(b) Find the fraction of each ac cycle during which the battery receives current.
#### Solution
(a) It is apparent that as long as $\left|v_{S}\right| \leq 12 \mathrm{~V}$, all diodes are cut off and $i=0$. However, as soon as $v_{S}$ rises above $12 \mathrm{~V}, D_{1}$ and $D_{4}$ go on, thus establishing the current loop
$$
\text { source } \rightarrow R \rightarrow D_{1} \rightarrow \text { battery } \rightarrow D_{4} \rightarrow \text { source }
$$
Conversely, when $v_{S}$ drops below $-12 \mathrm{~V}, D_{2}$ and $D_{3}$ go on, thus establishing the current loop
$$
\text { source } \rightarrow D_{2} \rightarrow \text { battery } \rightarrow D_{3} \rightarrow R \rightarrow \text { source }
$$
image_name:(a)
description:
[
name: VS, type: VoltageSource, value: VS, ports: {Np: Vs, Nn: GND}
name: R, type: Resistor, value: 12Ω, ports: {N1: Vs, N2: X1}
name: D1, type: Diode, ports: {Na: X1, Nc: X2}
name: D2, type: Diode, ports: {Na: GND, Nc: X2}
name: D3, type: Diode, ports: {Na: X3, Nc: X1}
name: D4, type: Diode, ports: {Na: X3, Nc: GND}
name: 12V, type: VoltageSource, value: 12V, ports: {Np: X2, Nn: X3}
]
extrainfo:The circuit is a simple battery charger. When the input voltage VS exceeds ±12V, diodes D1 and D4 or D2 and D3 conduct, allowing current to flow and charge the battery. The current is zero when |VS| ≤ 12V and follows i = (VS - 12V)/R when |VS| > 12V.
image_name:(b)
description:### Type of Graph and Function:
The graph in Figure 1.14(b) is a time-domain waveform depicting the voltage and current across a simple battery charger circuit.
Axes Labels and Units:
- **Horizontal Axis:** Time \( t \) in arbitrary units (possibly seconds or milliseconds), with marked points at \( t_1 \), \( t_2 \), \( T/2 \), and \( T \).
- **Vertical Axis:**
- Upper graph: Voltage \( v_S \) in volts (V), ranging from \(-24 \text{ V}\) to \(+24 \text{ V}\).
- Lower graph: Current \( i \) in amperes (A), ranging from 0 to 1 A.
Overall Behavior and Trends:
- **Voltage \( v_S \):**
- The waveform is sinusoidal, oscillating between \(+24 \text{ V}\) and \(-24 \text{ V}\), indicating an AC signal.
- The waveform crosses the zero line periodically, showing a complete cycle from 0 to \( T \).
- **Current \( i \):**
- The current waveform is non-zero only when \( |v_S| > 12 \text{ V} \).
- It forms a half-wave rectified pattern, with peaks reaching 1 A.
- The current is zero when \( |v_S| \leq 12 \text{ V} \), as indicated by the flat line at 0 A during these intervals.
Key Features and Technical Details:
- **Voltage Peaks:** Occur at \( +24 \text{ V} \) and \( -24 \text{ V} \).
- **Current Peaks:** Reach a maximum value of 1 A.
- **Zero Crossings:** Voltage crosses zero at regular intervals, while current crosses zero at points where \( |v_S| \leq 12 \text{ V} \).
- **Time Intervals:**
- \( T_{ON} \) is the duration where the current is non-zero, corresponding to the intervals where \( |v_S| > 12 \text{ V} \).
- \( t_1 \) and \( t_2 \) mark the start and end of the current flow in the first half-cycle.
Annotations and Specific Data Points:
- **Annotations:**
- \( T_{ON} \) is marked to indicate the active period of current flow.
- Specific time points \( t_1 \), \( t_2 \), \( T/2 \), and \( T \) are marked on the time axis.
- **Numerical Values:**
- Peak current value is 1 A.
- Voltage threshold for current flow is \( 12 \text{ V} \).
FIGURE 1.14 (a) Simple battery charger, and (b) voltage and current waveforms.
In either case, we have
$$
i=0 \quad \text { for } \quad\left|v_{S}\right| \leq 12 \mathrm{~V} \quad i=\frac{v_{S}-12 \mathrm{~V}}{R} \quad \text { for } \quad\left|v_{S}\right|>12 \mathrm{~V}
$$
The peak value of the current is $(24-12) / 12=1 \mathrm{~A}$. The waveforms are shown in Fig. 1.14b.
(b) During the first cycle, $i$ starts to flow into the battery at the instant $t_{1}$ such that
$$
24 \sin \frac{2 \pi t_{1}}{T}=12
$$
or $t_{1}=T / 12$, and stops conducting at $t_{2}=T / 2-T / 12$. Consequently, the conduction interval is $T_{\mathrm{ON}}=t_{2}-t_{1}=T / 3$, or $T_{\mathrm{ON}}=(2 / 3)(T / 2)$, where $T / 2$ is the period of the current waveform. In summary, the battery receives current during $2 / 3$ of the time.
### Diode Logic Gates
Figures $1.15 a$ and $1.16 a$ show how diodes can be used to implement elementary functions of the logic type, which are at the basis of digital systems. The inputs $A$ and $B$ and the output $Y$ are binary-valued voltages that can be either low $(L)$, such as 0 V , or high $(H)$, such as the power-supply voltage $V_{S}$ (typically, 5 V$)$. Circuit behavior is best understood by examining the rows of the accompanying tables, one at a time.
image_name:(a)
description:The system block diagram in Figure 1.15 (a) illustrates a diode-based logic gate circuit that implements the OR function. The primary components of this circuit include two diodes, labeled as \(D_A\) and \(D_B\), and a resistor \(R\) connected to ground. The inputs to the circuit are labeled \(A\) and \(B\), and the output is labeled \(Y\).
Main Components:
1. **Diodes (\(D_A\) and \(D_B\))**: These are the key elements that determine the logic operation. Each diode is connected to one of the inputs (\(A\) and \(B\)), allowing current to flow when the input is high.
2. **Resistor (\(R\))**: This is connected between the output \(Y\) and ground. It helps in pulling the output to a low state when both inputs are low.
Flow of Information or Control:
- The inputs \(A\) and \(B\) are binary voltages, either high (\(H\)) or low (\(L\)).
- The diodes \(D_A\) and \(D_B\) are oriented such that if either \(A\) or \(B\) is high, the corresponding diode will conduct, allowing current to flow to the output \(Y\), pulling it high.
- If both inputs \(A\) and \(B\) are low, neither diode conducts, and the resistor \(R\) pulls the output \(Y\) low.
Labels, Annotations, and Key Indicators:
- The diodes are labeled \(D_A\) and \(D_B\), indicating their association with inputs \(A\) and \(B\), respectively.
- The output \(Y\) is the result of the OR operation, where \(Y\) is high if at least one of the inputs is high.
Overall System Function:
The primary function of this system is to perform a logical OR operation on the binary inputs \(A\) and \(B\). The arrangement of the diodes and the resistor ensures that the output \(Y\) is high if either or both inputs are high, and low only when both inputs are low. This is represented by the truth table accompanying the diagram, which confirms that the circuit behaves as an OR gate.
| $A$ | $B$ | $D_{A}$ | $D_{B}$ | $Y$ |
| :---: | :---: | :---: | :---: | :---: |
| $L$ | $L$ | CO | CO | $L$ |
| $L$ | $H$ | CO | ON | $H$ |
| $H$ | $L$ | ON | CO | $H$ |
| $H$ | $H$ | ON | ON | $H$ |
(b)
FIGURE 1.15 (a) Diode circuit implementing the OR function, and (b) its truth table.
image_name:Figure 1.15 (a)
description:
[
name: DA, type: Diode, ports: {Na: Y, Nc: A}
name: DB, type: Diode, ports: {Na: Y, Nc: B}
name: R, type: Resistor, value: R, ports: {N1: Y, N2: VS}
name: VS, type: VoltageSource, value: VS, ports: {Np: VS, Nn: GND}
]
extrainfo:The circuit implements an OR gate using diodes DA and DB, a resistor R, and a voltage source VS. The output Y is high if either input A or B is high.
image_name:Figure 1.16 (a)
description:The system block diagram in Figure 1.16 (a) represents a diode-based circuit that implements the AND logic function. The primary components of this circuit include two diodes, labeled as $D_A$ and $D_B$, a resistor $R$, and a voltage source $V_S$. The circuit is connected to two inputs, $A$ and $B$, and produces an output $Y$.
Main Components:
1. **Diodes ($D_A$ and $D_B$):**
- These are the key elements responsible for implementing the AND logic operation. They allow current to pass only when forward-biased.
2. **Resistor ($R$):**
- Connected between the voltage source $V_S$ and the node where the diodes meet. It helps in limiting the current flow through the circuit.
3. **Voltage Source ($V_S$):**
- Provides the necessary voltage for the circuit operation.
Flow of Information or Control:
- **Input Signals ($A$ and $B$):**
- These signals are applied to the anodes of diodes $D_A$ and $D_B$, respectively.
- If both inputs $A$ and $B$ are high, both diodes become forward-biased, allowing current to flow from $V_S$ through the resistor $R$ to the output $Y$.
- If either input is low, the corresponding diode remains reverse-biased, preventing current flow, resulting in a low output $Y$.
- **Output Signal ($Y$):**
- The output is high only when both input signals are high, aligning with the behavior of an AND gate.
Labels, Annotations, and Key Indicators:
- The diagram includes labels for each component and signal path, clearly identifying the inputs ($A$, $B$) and the output ($Y$).
Overall System Function:
- This diode circuit functions as an AND gate. The arrangement ensures that the output $Y$ is high only when both inputs $A$ and $B$ are high, effectively performing the logical AND operation. The resistor $R$ and voltage source $V_S$ ensure proper current and voltage levels for the operation of the diodes and the circuit as a whole.
(a)
| $A$ | $B$ | $D_{A}$ | $D_{B}$ | $Y$ |
| :---: | :---: | :---: | :---: | :---: |
| $L$ | $L$ | ON | ON | $L$ |
| $L$ | $H$ | ON | CO | $L$ |
| $H$ | $L$ | CO | ON | $L$ |
| $H$ | $H$ | CO | CO | $H$ |
(b)
FIGURE 1.16 (a) Diode circuit implementing the AND function, and (b) its truth table.
- As long as both inputs $A$ and $B$ are low $(0 \mathrm{~V})$ in Fig. $1.15 a$, both diodes are off, so all voltages and currents are zero, and $Y$ is low. However, if we drive at least one input high ( 5 V ), we will be sourcing current to the anode of the corresponding diode, turning it on and thus pulling $Y$ also high, as illustrated in Fig. 1.15b. We summarize by saying that $Y$ is high if $A$ or $B$ or both are high. This logic function, aptly called the OR function, is identified by the logic-gate symbol next to the circuit itself, in Fig. 1.15a. The table of Fig. $1.15 b$ summarizes its behavior and is called the truth table.
- As long as at least one input is low $(0 \mathrm{~V})$ in Fig. 1.16a, the corresponding diode will be on as we are sinking current from its cathode. So, $Y$ is also low. Only if both $A$ and $B$ are high will both diodes be cut off, causing the current through $R$ to drop to zero. With zero current, the voltage drop across $R$ is also zero, and we say that $R$ pulls $Y$ to $V_{S}$, or high, as illustrated in Fig. 1.16b. This state of affairs is summarized by saying that $Y$ is high if $A$ and $B$ are high. This logic function, aptly called the AND function, is identified by the logic-gate symbol next to the circuit itself, in Fig. 1.16 $a$. The table of Fig. $1.16 b$ summarizes its behavior and is called the truth table.
Each gate can readily be expanded to handle more than just two inputs by interconnecting additional diodes, as needed. The above gates, though certainly useful, are not sufficient to build a complete digital system because we also need, among others, the inversion function. This requires a transistor, as we shall study in the next two chapters.
### Voltage Clamps
The unidirectional-switch behavior of the diode can be exploited to establish prescribed limits for certain voltages in a circuit. Such a situation arises, for instance, in connection with the inputs to integrated circuits (ICs), which must be kept within limits as recommended in the data sheets in order to prevent the IC from malfunctioning or, even worse, from undergoing permanent damage. As a rule, the input voltages to an IC should never be allowed to exceed its power-supply voltages.
Figure 1.17 a illustrates the situation for a single-supply IC, such as a CMOS digital circuit or a single-supply op amp. However, the principle can readily be generalized to multiple-supply systems, such as dual-supply op amps. With reference to Fig. $1.17 a$, we readily see that as long as the external input $v_{I}$ lies within the range $0 \leq v_{I} \leq V_{S}$, both diodes are off, so the signal right at the IC's input pin is $v_{I C} \cong v_{I}$
image_name:(a)
description:
[
name: R, type: Resistor, value: R, ports: {N1: vI, N2: vIC}
name: D1, type: Diode, ports: {Na: vIC, Nc: VS}
name: D2, type: Diode, ports: {Na: GND, Nc: vIC}
name: IC, type: OpAmp, value: IC, ports: {InP: vIC, InN: GND, OutP: vO}
name: VS, type: VoltageSource, value: VS, ports: {Np: VS, Nn: GND}
]
extrainfo:The circuit diagram shows a single-supply IC with diode clamps to limit the input voltage range. Diode D1 clamps the input voltage to the supply voltage VS, and D2 clamps it to ground. This ensures that the input voltage to the IC remains within safe limits, protecting the IC from overvoltage.
image_name:(b)
description:The graph in Figure 1.17(b) is a time-domain waveform plot. It depicts the behavior of the input voltage $v_I$ and the clamped voltage $v_{IC}$ over time, demonstrating the effect of diode clamps in a single-supply IC circuit.
1. **Type of Graph and Function:**
- This is a time-domain waveform graph.
2. **Axes Labels and Units:**
- The x-axis represents time $t$ and is typically measured in seconds or milliseconds, though the specific units are not labeled in the diagram.
- The y-axis represents voltage, labeled with values $0$ and $V_S$ (the supply voltage), indicating the voltage levels in volts.
3. **Overall Behavior and Trends:**
- The input voltage $v_I$ is shown as a sinusoidal waveform oscillating above and below the supply voltage $V_S$ and ground (0 volts).
- The clamped voltage $v_{IC}$ follows $v_I$ as long as $v_I$ is between 0 and $V_S$. When $v_I$ exceeds $V_S$, $v_{IC}$ is clamped at $V_S$; similarly, when $v_I$ goes below 0, $v_{IC}$ is clamped at 0 volts.
- This results in a clipped waveform for $v_{IC}$, with flat tops and bottoms corresponding to the clamping action.
4. **Key Features and Technical Details:**
- The waveform for $v_I$ exhibits a typical sinusoidal shape with peaks exceeding $V_S$ and valleys going below 0.
- The waveform for $v_{IC}$ shows clamping at $V_S$ and 0 volts, indicating the action of the diodes $D_1$ and $D_2$.
- The transition points where $v_I$ exceeds $V_S$ or goes below 0 correspond to the activation of the diodes, where $D_1$ and $D_2$ conduct to keep $v_{IC}$ within the supply range.
5. **Annotations and Specific Data Points:**
- The graph includes annotations for $v_I$ and $v_{IC}$, showing the difference between the input and the clamped voltages.
- The horizontal lines at $V_S$ and 0 volts emphasize the clamping levels enforced by the diodes.
This graph effectively illustrates how diode clamps maintain the IC input voltage within the safe operating range, preventing it from exceeding the supply voltage limits.
FIGURE 1.17 (a) Using diode clamps to limit the input voltage range of an IC.
(b) Waveforms.
(assuming the IC draws negligible input current, which is indeed the case with CMOS logic circuits as well as op amps.) However, should $v_{I}$ exceed the supply voltage $V_{S}$, either because of an oversight by the user or because of interference noise superimposed upon $v_{I}$ itself, $D_{1}$ will go on, thus establishing a short between $v_{I C}$ and $V_{S}$. We say that $D_{1}$ clamps $v_{I C}$ at $V_{S}$. By similar reasoning, should $v_{I}$ drop below ground potential, $D_{2}$ will clamp $v_{I C}$ at 0 V . As depicted in Fig. $1.17 b$, the diodes protect the IC against possible input overdrive situations by limiting the input-pin voltage within the range
$$
0 \leq v_{I C} \leq V_{S}
$$
For this reason, a diode clamp is also referred to as a limiter, and since it clips the portions of the input waveform falling outside the allowed range, it is also called a clipper.
The need for protection against input overdrives is so important and so common that many ICs come already equipped with internal diode-clamping networks to relieve the user from this worry. In this respect it is worth mentioning the MOSFET as a device particularly sensitive to input overvoltages when handled by humans. Since its gate terminal is the plate of an extremely tiny capacitor, any electrostatic charge that may have accumulated on the body of the user will be transferred to this capacitor during manual contact, thus leading to potentially high voltages (as per $V=Q / C$ ) that are likely to destroy the capacitor's dielectric. However, in the presence of suitable diode clamps, the body of the handler will discharge through one of the diodes, saving the device from assured destruction.
#### Exercise 1.2
In the circuit of Fig. 1.17 let $R=10 \mathrm{k} \Omega$ and $V_{S}=5 \mathrm{~V}$. Assuming the IC draws no current at its input terminal, find the current through $R$ (magnitude and direction) for the following values of $v_{I}:(a)=1 \mathrm{~V},(b) 8 \mathrm{~V},(c)-2 \mathrm{~V},(d) 4.5 \mathrm{~V}$. (e) If it is found that $R$ draws 0.25 mA flowing toward the right, what do you conclude about $v_{I}$ ? ( $f$ ) What if $R$ draws 0.5 mA flowing toward the left? $(g)$ What if the current through $R$ is zero?
Ans. (a) 0 mA ; (b) $0.3 \mathrm{~mA}(\rightarrow)$; (c) $0.2 \mathrm{~mA}(\leftarrow)$; (d) 0 mA ; (e) $v_{I}=7.5 \mathrm{~V}$; (f) $v_{I}=-5 \mathrm{~V}$; (g) $0 \leq v_{I} \leq 5 \mathrm{~V}$.
### Piecewise-Linear Function Generators
The nonlinear characteristic of the diode can be exploited on purpose to create piecewise-linear approximations to nonlinear functions. A popular application example is the conversion of a triangular wave to a sinewave. Figure $1.18 a$ shows a simple example of a piecewise-linear function generator. We make the following observations:
image_name:(a)
description:
[
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
name: R1, type: Resistor, value: 20kΩ, ports: {N1: VI, N2: Vo}
name: R2, type: Resistor, value: 10kΩ, ports: {N1: 12V, N2: X2}
name: R3, type: Resistor, value: 10kΩ, ports: {N1: X2, N2: X1}
name: R4, type: Resistor, value: 10kΩ, ports: {N1: X1, N2: GND}
name: D1, type: Diode, ports: {Na: Vo, Nc: X2}
name: D2, type: Diode, ports: {Na: X1, Nc: Vo}
]
extrainfo:This circuit is a piecewise-linear function generator that uses diodes to create a nonlinear characteristic. The 12V supply is divided into three equal voltage drops across three 10kΩ resistors, resulting in voltages of 4V and 8V at nodes X1 and X2, respectively. The diodes D1 and D2 control the voltage at Vo based on the input voltage VI.
(a) GND
image_name:FIGURE 1.18 (b)
description:The graph in FIGURE 1.18 (b) is a Voltage Transfer Characteristic (VTC) plot, which shows the relationship between the output voltage (v_O) and the input voltage (v_I) for the circuit described.
1. **Type of Graph and Function:**
- This is a piecewise-linear graph depicting the VTC of a diode-based nonlinear circuit.
2. **Axes Labels and Units:**
- The x-axis represents the input voltage (v_I) in volts (V), ranging from 0 to 12 V.
- The y-axis represents the output voltage (v_O) in volts (V), ranging from 2 to 10 V.
- The graph uses a linear scale for both axes.
3. **Overall Behavior and Trends:**
- The graph is segmented into three linear regions, indicating piecewise-linear behavior.
- For input voltages below 4 V, the output voltage increases linearly with a slope less than one.
- Between 4 V and 8 V, the output voltage remains relatively constant at around 4 V, indicating that both diodes are off in this region.
- For input voltages above 8 V, the output voltage again increases linearly with a slope similar to the initial region.
4. **Key Features and Technical Details:**
- There are two inflection points at approximately 4 V and 8 V on the x-axis, corresponding to the activation and deactivation thresholds of the diodes.
- The constant region between 4 V and 8 V suggests no current flow through the diodes, and thus, no change in output voltage.
- The linear regions before 4 V and after 8 V indicate diode conduction, affecting the voltage drop across the resistors.
5. **Annotations and Specific Data Points:**
- The graph includes gridlines to assist in reading specific values.
- Critical points include the transition at 4 V where the slope changes, and at 8 V where another transition occurs.
This graph effectively illustrates how the diode configuration in the circuit governs the output voltage based on the input voltage, demonstrating the piecewise-linear characteristics of the circuit.
(b)
FIGURE 1.18 (a) Piecewise-linear function generator example, and (b) its VTC.
- With both diodes off, the three $10-\mathrm{kV}$ resistors partition the $12-\mathrm{V}$ supply voltage into three equal voltage drops, thus giving 4 V and 8 V , respectively. This is illustrated in Fig. 1.19a, where we observe that both diodes are off as long as the input is kept within the range $4 \mathrm{~V}<v_{I}<8 \mathrm{~V}$. Since no current flows through the $20-\mathrm{k} \Omega$ resistor, the latter drops 0 V , so the circuit gives
$$
\begin{equation*}
v_{O}=v_{I} \quad \text { for } 4 \mathrm{~V}<v_{I}<8 \mathrm{~V} \tag{1.5a}
\end{equation*}
$$
image_name:(a)
description:
[
name: V_I, type: VoltageSource, value: V_I, ports: {Np: vI, Nn: GND}
name: R1, type: Resistor, value: 20 kΩ, ports: {N1: vI, N2: vO}
name: D_1, type: Diode, ports: {Na: vO, Nc: 8 V}
name: D_2, type: Diode, ports: {Na: 4 V, Nc: vO}
name: R2, type: Resistor, value: 10 kΩ, ports: {N1: 12 V, N2: 8 V}
name: R3, type: Resistor, value: 10 kΩ, ports: {N1: 8 V, N2: 4 V}
name: R4, type: Resistor, value: 10 kΩ, ports: {N1: 4 V, N2: GND}
]
extrainfo:The circuit is a piecewise-linear function generator. For 4V < vI < 8V, both diodes are off and vO = vI. If vI < 4V, D2 turns on, clamping vO to 4V. If vI > 8V, D1 turns on, clamping vO to 8V.
image_name:(b)
description:
[
name: V_I, type: VoltageSource, value: V_I, ports: {Np: vI, Nn: GND}
name: 20 kΩ, type: Resistor, value: 20 kΩ, ports: {N1: vI, N2: vO}
name: D_1, type: Diode, ports: {Na: vO, Nc: 8V}
name: D_2, type: Diode, ports: {Na: 4V, Nc: vO}
name: 10 kΩ, type: Resistor, value: 10 kΩ, ports: {N1: 12V, N2: 8V}
name: 10 kΩ, type: Resistor, value: 10 kΩ, ports: {N1: 8V, N2: 4V}
name: 10 kΩ, type: Resistor, value: 10 kΩ, ports: {N1: 4V, N2: GND}
]
extrainfo:For vI < 4V, D2 is on and D1 is off. The circuit allows current to flow from the 12V supply through the 10 kΩ resistors to ground, with vO at 4V.
image_name:(c)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: VI, Nn: GND}
name: D1, type: Diode, ports: {Na: VO, Nc: 8V}
name: D2, type: Diode, ports: {Na: 4V, Nc: VO}
name: R1, type: Resistor, value: 20kΩ, ports: {N1: VI, N2: VO}
name: R2, type: Resistor, value: 10kΩ, ports: {N1: 12V, N2: 8V}
name: R3, type: Resistor, value: 10kΩ, ports: {N1: 8V, N2: 4V}
name: R4, type: Resistor, value: 10kΩ, ports: {N1: 4V, N2: GND}
]
extrainfo:The circuit diagram (c) represents a voltage divider with diodes D1 and D2 used for wave shaping. When the input voltage VI is greater than 8V, D1 conducts and clamps the output VO. The resistors R2, R3, and R4 form a voltage divider to create reference voltages at 8V and 4V respectively. The circuit allows for wave shaping based on the input voltage range.
FIGURE 1.19 Equivalent circuits of the function generator of Fig. 1.18 for different input conditions.
image_name:FIGURE 1.20
description:The graph in FIGURE 1.20 illustrates the wave shaping effect of a piecewise-linear circuit, as described in the context. This is a time-domain waveform graph showing the relationship between input voltage \( v_I \) and output voltage \( v_O \) over time.
Axes Labels and Units:
- **X-axis (Horizontal):** Represents Time. The specific units of time are not labeled, but it is a continuous time scale.
- **Y-axis (Vertical):** Represents Voltage in Volts, ranging from 0 to 12 volts.
Overall Behavior and Trends:
- The input voltage \( v_I \) is depicted as a triangular waveform oscillating between 0V and 12V. This waveform is shown in a lighter gray color.
- The output voltage \( v_O \), shown in a darker line, follows a modified waveform due to the circuit's wave shaping characteristics. It does not exceed 8V and does not drop below 3V, as it is clamped by the diodes and the voltage divider.
Key Features and Technical Details:
- When \( v_I \) exceeds 8V, the output \( v_O \) is clamped at 8V. This is due to diode D1 conducting and clamping the output.
- When \( v_I \) drops below 4V, the output \( v_O \) follows the equation \( v_O = 0.25v_I + 3 \), as described in the context. This is due to diode D2 conducting.
- The waveform of \( v_O \) has flat peaks at 8V and a linear increase from 3V when \( v_I \) is below 4V.
Annotations and Specific Data Points:
- The graph has specific reference lines at 4V, 8V, and 12V, indicating key voltage levels.
- The behavior of \( v_O \) is clearly annotated with arrows showing its relationship with \( v_I \).
This graph effectively demonstrates the clipping and linear transformation effects imposed by the circuit on the input waveform.
FIGURE 1.20 Illustrating the waveshaping effect of the piecewise-linear circuit of Fig. 1.18a.
- If we lower $v_{I}$ below $4 \mathrm{~V}, D_{2}$ goes on while $D_{1}$ remains off, resulting in the situation of Fig. 1.19b. By KCL we have
$$
\frac{12-v_{O}}{10+10}=\frac{v_{O}-v_{I}}{20}+\frac{v_{O}}{10}
$$
which is readily solved for $v_{O}$ to give
$$
\begin{equation*}
v_{O}=0.25 v_{I}+3 \mathrm{~V} \quad \text { for } v_{I}<4 \mathrm{~V} \tag{1.5b}
\end{equation*}
$$
- If we raise $v_{I}$ above $8 \mathrm{~V}, D_{1}$ goes on while $D_{2}$ remains off, resulting in the situation of Fig. 1.19c. Applying again KCL, we get
$$
\frac{v_{I}-v_{O}}{20}+\frac{12-v_{O}}{10}=\frac{v_{O}}{10+10}
$$
which is readily solved for $v_{O}$ to give
$$
\begin{equation*}
v_{O}=0.25 v_{I}+6 \mathrm{~V} \quad \text { for } v_{I}>8 \mathrm{~V} \tag{1.5c}
\end{equation*}
$$
Figure $1.18 b$ shows the circuit's VTC. Clearly, we have three separate regions of operation. Within each region, the VTC is a straight segment whose analytical expression is obtained by drawing the corresponding equivalent circuit, as per Fig. 1.19, and subjecting it to elementary linear analysis techniques. This is typical of diode circuits.
Figure 1.20 shows the waveshaping effect of the circuit of Fig. 1.18 upon a triangular wave. Here, the aim is to compress the top and the bottom of the triangle to approximate a sine. Clearly, the present example provides a rather crude approximation, but it is not hard to imagine that we can improve it by using additional segments. This is normally accomplished with $p n$ junction diodes. As we shall see, the characteristic of the $p n$ diode has a rounded knee which helps ensure a smoother transition from one segment to the next of the VTC.
### Peak Detectors
Additional interesting applications arise if a diode $D$ is partnered by a capacitor $C$. As our first example we consider the circuit of Fig. 1.21a, known as a peak detector. To understand its operation, refer to the waveforms of Fig. 1.21b, where $C$ is assumed initially discharged. As $v_{I}$ swings positive, current will be sourced to the anode, forcing $D$ to conduct and thus to charge up $C$. Since $D$ acts as a short circuit, $v_{O}$ simply follows $v_{I}$.
image_name:(a)
description:
[
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
name: D, type: Diode, ports: {Na: GND, Nc: VO}
name: C, type: Capacitor, value: C, ports: {Np: VI, Nn: VO}
]
extrainfo:The circuit is a peak detector which uses a diode and capacitor to capture and hold the peak voltage of the input signal. The diode conducts when the input voltage rises, charging the capacitor to the peak voltage. When the input voltage falls, the diode stops conducting and the capacitor holds the peak voltage.
image_name:(b)
description:The graph in Fig. 1.21b is a time-domain waveform illustrating the operation of a peak detector circuit. The x-axis represents time (t), while the y-axis represents voltage. The graph shows two waveforms: the input voltage $v_I$ and the output voltage $v_O$.
1. **Type of Graph and Function:**
- The graph is a time-domain waveform plot, showing how the input and output voltages change over time.
2. **Axes Labels and Units:**
- The x-axis is labeled as 'Time t', which implies the unit is likely seconds or a submultiple such as milliseconds (not explicitly stated).
- The y-axis is labeled with voltage ($v_I$ and $v_O$), but specific units are not provided (assumed to be volts).
3. **Overall Behavior and Trends:**
- The input voltage $v_I$ is a sinusoidal waveform oscillating above and below zero volts.
- The output voltage $v_O$ follows the peaks of $v_I$. Initially, as $v_I$ increases, $v_O$ follows it closely, indicating the diode (D) is conducting.
- Once $v_I$ reaches its peak and starts to decrease, $v_O$ holds the peak value, as the diode turns off and the capacitor (C) retains the charge.
- This behavior repeats with each cycle of $v_I$, where $v_O$ only updates when $v_I$ reaches a new peak greater than the previous one.
4. **Key Features and Technical Details:**
- The diode (D) is annotated with states 'ON' and 'CO' (cut-off), indicating its operation during the waveform cycle.
- The waveform $v_O$ shows a step-like behavior, maintaining the peak voltage until a new higher peak is encountered in $v_I$.
- The graph illustrates the memory effect of the capacitor, which holds the peak voltage.
5. **Annotations and Specific Data Points:**
- Annotations on the graph indicate when the diode is 'ON' and when it is 'CO', showing the transition points.
- The zero voltage line is marked, showing the baseline for the input sinusoidal waveform $v_I$.
This graph effectively demonstrates the peak detection functionality, where the output voltage $v_O$ tracks and holds the maximum value of the input voltage $v_I$ over time.
FIGURE 1.21 (a) Peak detector, and (b) illustrative waveforms.
Once $v_{I}$ peaks out, the anode will start swinging negative relative to the cathode, turning $D$ off and thus leaving $C$ to hold the previously acquired voltage, whose value coincides with that of the previous input peak. This memory action by $C$ will persist until $v_{I}$ rises again to a new, higher peak. When this happens, $D$ will go on again, charging up $C$ to this new peak.
It is apparent that the diode's directionality causes the capacitor voltage to experience only increases, this being the reason why the circuit shown is said to be a positive peak detector. Reversing the diode interconnection in the circuit will cause the capacitor voltage to experience only decreases, thus yielding a negative peak detector. Peak detectors are at the basis of demodulators in the detection of audio signals in amplitude-modulation (AM) radio receivers.
### The Clamped Capacitor or Dc Restorer
In the circuit of Fig. $1.22 a$ the diode provides a clamping function that prevents $v_{O}$ from ever going negative. To understand circuit operation, refer to the waveforms of Fig. $1.22 b$, where the input is a sine wave alternating between $+V_{m}$ and $-V_{m}$, and $C$ is assumed initially discharged. During the initial positive alternation of $v_{I}$ we simply have $v_{O}=v_{I}$ as the voltage across $C$ is zero and the diode is off. However, as $v_{I}$ goes below 0 V for the first time, the input source will sink current from $D$ 's cathode via $C$, thus turning $D$ on and forcing $C$ to charge. As $v_{I}$ reaches its negative peak of $-V_{m}$ at $t=t_{2}$,
image_name:(a)
description:
[
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
name: C, type: Capacitor, value: C, ports: {Np: VI, Nn: VO}
name: D, type: Diode, ports: {Na: VI, Nc: VO}
]
extrainfo:The circuit is a basic clamping circuit where the diode conducts during negative cycles of the input voltage, charging the capacitor to maintain the output voltage at a level shifted by the peak input voltage.
image_name:(b)
description:The graph in Figure 1.22(b) is a time-domain waveform illustrating the behavior of a clamping circuit. The x-axis represents time (t), while the y-axis represents voltage levels, marked in terms of \( V_m \), the peak input voltage. The y-axis has key voltage levels labeled as \(-V_m\), 0, \(V_m\), and \(2V_m\).
Two waveforms are shown:
1. **Input Voltage \( v_I \):** This waveform is depicted in gray and oscillates sinusoidally between \(-V_m\) and \(+V_m\). The input voltage \( v_I \) has a zero average value as it alternates symmetrically around the zero-voltage line.
2. **Output Voltage \( v_O \):** This waveform is shown in black. Initially, during the time interval from 0 to \( t_2 \), the diode is conducting (as indicated by the label \( D = ON \)), and the waveform rises from 0 to \( V_m \). After \( t_2 \), the diode stops conducting, and the capacitor retains the voltage, causing the output waveform \( v_O \) to oscillate between 0 and \( +2V_m \). This results in a voltage shift upwards by \( V_m \), as indicated by the equation \( v_O = v_I + V_m \) for \( t \geq t_2 \).
**Key Features and Trends:**
- The transition point \( t_2 \) marks the end of the diode conduction phase, after which the output voltage waveform maintains its shifted position.
- The waveform \( v_O \) demonstrates periodic behavior, with peaks at \( 2V_m \) and valleys at 0.
- The graph effectively demonstrates the clamping action of the circuit, where the output voltage is consistently higher than the input voltage by a fixed amount (\( V_m \)).
Overall, this graph visually represents the voltage transformation achieved by the clamping circuit, highlighting the shift in the output waveform relative to the input waveform.
(b)
FIGURE 1.22 (a) Clamped capacitor, and (b) illustrative waveforms.
$C$ will have acquired a voltage equal to $V_{m}$, positive at the right plate. After $t=t_{2}$, the diode will never conduct again, and $C$ will retain the voltage acquired last, thus giving
$$
\begin{equation*}
v_{O}=v_{I}+V_{m} \tag{1.6}
\end{equation*}
$$
for $t \geq t_{2}$. While $v_{I}$ alternates between $-V_{m}$ and $+V_{m}$, and thus averages out to zero, $v_{O}$ ends up alternating between 0 and $+2 V_{m}$ because of the voltage offset provided by $C$. Consequently, $v_{O}$ averages out to $+V_{m}$, and because of this nonzero dc component at its output, the circuit is also referred to as a dc restorer.
### Voltage Multipliers and PSpice Simulation
An interesting property of the clamped-capacitor circuit of Fig. $1.22 a$ is that it provides a positive output peak that is twice that of the input. This indicates that if we feed the output of the clamped capacitor circuit to a peak detector, we can synthesize a dc voltage of value $+2 V_{m}$, that is, of twice the amplitude of the input! To better understand the behavior of this composite circuit, we simulate it via PSpice. Aptly called a voltage doubler, the circuit is shown in Fig. 1.23 for the case of a 1-kHz, 10-V sinusoidal input. The circuit utilizes pseudo-ideal diodes, whose PSpice models have been created by editing one of the already existing diode models available in PSpice's library, and then setting the parameters $I_{s}$ and $n$ to the values shown in the table (more on this in Appendix 1A).
The various waveforms are displayed in Fig. 1.24, where we observe that after a transient situation lasting less than ten cycles, the output settles to the dc value
$$
\begin{equation*}
v_{2} \rightarrow 2 V_{m} \tag{1.7}
\end{equation*}
$$
or $v_{2}=20 \mathrm{~V}$ in the present example. The reason it takes several cycles to attain the desired steady-state situation is that $C_{1}$ is being loaded by $C_{2}$. If the circuit were implemented with $C_{1} \gg C_{2}$, steady state would be achieved essentially at the second positive peak of $v_{I}$. However, with equal capacitors, which is how the circuit is usually implemented, the charge accumulated by $C_{1}$ at each positive peak of $v_{I}$ redistributes equally between $C_{1}$ and $C_{2}$, causing a reduction in $v_{1}$ which, though significant at the first peak of $v_{l}$, becomes progressively less relevant with each subsequent peak. One can prove (see Exercise 1.3), that the values attained by $v_{2}$ at each peak of $v_{I}$ are $5 \mathrm{~V}, 12.5 \mathrm{~V}, 16.25 \mathrm{~V}, 18.125 \mathrm{~V}$. . . .
image_name:FIGURE 1.23
description:
[
name: vI, type: VoltageSource, value: 10 Vac, ports: {Np: vI, Nn: 0}
name: C1, type: Capacitor, value: 1 nF, ports: {Np: vI, Nn: v1}
name: D1, type: Diode, ports: {Na: 0, Nc: v1}
name: D2, type: Diode, ports: {Na: v1, Nc: v2}
name: C2, type: Capacitor, value: 1 nF, ports: {Np: v2, Nn: 0}
]
extrainfo:The circuit is a voltage doubler using pseudo-ideal diodes. The diodes have parameters Is = 1 nA and n = 0.001.
FIGURE 1.23 PSpice circuit simulating a voltage doubler based on pseudo-ideal diodes. The parameters of the PSpice diode model are shown inside the box at the right.
image_name:FIGURE 1.24
description:The graph in FIGURE 1.24 illustrates the waveforms for a voltage doubler circuit using pseudo-ideal diodes. The x-axis represents time in milliseconds (ms), ranging from 0 to 10 ms. The y-axis represents voltage in volts (V), with values ranging from -10 V to 20 V. The graph is linear in both axes.
Three waveforms are depicted:
1. **Input Voltage ($v_I$):** This waveform is a sinusoidal wave with a peak amplitude of approximately 10 V and a frequency that completes several cycles within the 10 ms timeframe. It oscillates symmetrically around 0 V, indicating an AC input.
2. **Intermediate Voltage ($v_1$):** This waveform is also sinusoidal but appears to have a slightly reduced amplitude compared to the input voltage. It follows the input voltage closely, indicating the effect of the first diode in the voltage doubler circuit.
3. **Output Voltage ($v_2$):** This waveform shows a step-like increase, starting at about 5 V. It increases incrementally with each peak of the input voltage, ultimately reaching a value close to 20 V. This behavior reflects the voltage doubling effect, where each peak of the input voltage contributes to the increase in $v_2$.
**Overall Behavior and Trends:**
- The input voltage ($v_I$) maintains a consistent sinusoidal pattern throughout the duration.
- The intermediate voltage ($v_1$) mirrors the input but with slightly reduced amplitude, indicating some voltage drop or regulation.
- The output voltage ($v_2$) shows a distinct stepped increase. Each step corresponds to a peak in the input voltage, showcasing the charge conservation principle and voltage doubling effect.
**Key Features:**
- The $v_2$ waveform begins at 5 V and steps up towards 20 V, aligning with the theoretical model where $v_2(k) = 0.5 v_2(k-1) + 10$ V.
- The waveform reaches within 10% of 20 V by the third peak of the input voltage, as indicated by the gradual step increase.
- By analyzing the waveform, one can deduce the efficiency and behavior of the voltage doubler circuit over time.
FIGURE 1.24 Waveforms for the PSpice circuit of Fig. 1.23.
#### Exercise 1.3
Denoting the value of $v_{2}$ following the $k$-th peak of $v_{I}$ as $v_{2}(k)$, use the charge conservation principle to show that $v_{2}(k)$ is related to the value $v_{2}(k-1)$ following the previous peak as
$$
v_{2}(k)=0.5 v_{2}(k-1)+10 \mathrm{~V}
$$
$k=2,3,4 \ldots$, and $v_{2}(1)=5 \mathrm{~V}$. At which peak of $v_{I}$ does $v_{2}$ come within about $10 \%$ of 20 V ? $1 \%$ of 20 V ?
Ans. For $10 \%, k=3$. For $1 \%, k=6$.
The principle at the basis of the voltage doubler can be generalized to achieve higher voltage-multiplication factors. Figure 1.25 shows a voltage quadrupler, whose waveforms are displayed in Fig. 1.26. We see again that after a transient situation lasting a certain number of cycles the output $v_{4}$ eventually settles to the dc value
$$
\begin{equation*}
v_{4} \rightarrow 4 V_{m} \tag{1.8}
\end{equation*}
$$
or $v_{4}=40 \mathrm{~V}$ in the present example. The reader is encouraged to trace through each waveform in detail to develop a feel for the workings of this clever circuit.
Voltage multipliers find application in integrated circuits, where it is desired to synthesize specific voltages to bias different on-chip circuits, starting out with a single supply voltage such as that provided by a rechargeable battery.
image_name:Figure 1.25 Voltage quadrupler
description:
[
name: V1, type: VoltageSource, value: 10 Vac, ports: {Np: V_I, Nn: GND}
name: C1, type: Capacitor, value: 1nF, ports: {Np: V_I, Nn: v1}
name: C2, type: Capacitor, value: 1nF, ports: {Np: V2, Nn: GND}
name: C3, type: Capacitor, value: 1nF, ports: {Np: V3, Nn: v1}
name: C4, type: Capacitor, value: 1nF, ports: {Np: v4, Nn: V2}
name: D1, type: Diode, ports: {Na: GND, Nc: v1}
name: D2, type: Diode, ports: {Na: v1, Nc: V2}
name: D3, type: Diode, ports: {Na: v2, Nc: V3}
name: D4, type: Diode, ports: {Na: v3, Nc: V4'}
]
extrainfo:The circuit is a voltage quadrupler, which multiplies the input AC voltage by four through a series of capacitors and diodes.
FIGURE 1.25 Voltage quadrupler.
image_name:FIGURE 1.26 Waveforms for the voltage quadrupler of Fig. 1.25.
description:The graph in Figure 1.26 is a time-domain waveform depicting the operation of a voltage quadrupler circuit. The x-axis is labeled 'Time t (ms)' and spans from 0 to 25 milliseconds, indicating the progression of time in milliseconds. The y-axis is labeled 'Waveforms (V)' and measures voltage in volts, ranging from -10V to 40V.
The graph shows multiple waveforms, each representing different voltage points in the quadrupler circuit. The key waveforms are labeled as $v_I$, $v_1$, $v_2$, $v_3$, and $v_4$:
- **$v_I$ (Input Voltage):** This waveform oscillates between approximately -10V and 10V, representing the AC input voltage to the circuit. It is a sinusoidal waveform with a constant amplitude.
- **$v_1$, $v_2$, $v_3$, and $v_4$ (Output Voltages):** These waveforms show a stepwise increase in the DC level, superimposed with an AC ripple.
- **$v_1$** oscillates around a DC level of approximately 10V.
- **$v_2$** oscillates around a DC level of approximately 20V.
- **$v_3$** oscillates around a DC level of approximately 30V.
- **$v_4$** oscillates around a DC level of approximately 40V.
The overall behavior shows the effect of the voltage quadrupler circuit, which increases the DC level of the input voltage by a factor of four, as indicated by the labels (2V_m) and (4V_m) on the y-axis. The AC ripple on each waveform diminishes as the DC level increases, showing the filtering effect of the capacitors in the circuit.
The waveforms exhibit periodicity corresponding to the input AC waveform, and the stepwise increase in DC levels demonstrates the cumulative effect of the diodes and capacitors in the quadrupler arrangement. The graph effectively illustrates the voltage multiplication and rectification process inherent in the circuit's design.
FIGURE 1.26 Waveforms for the voltage quadrupler of Fig. 1.25.
## 1.3 OPERATIONAL AMPLIFIERS AND DIODE APPLICATIONS
As we move along we shall find that the range of applications for diodes and, later, for transistors can be expanded significantly if we team up these devices with the operational amplifier, or op amp for short. Recall from prerequisite circuit courses that an op amp is a high-gain voltage amplifier that accepts two inputs, called the inverting input $v_{N}$ and the noninverting input $v_{P}$, and yields an output $v_{O}$ such that
$$
\begin{equation*}
v_{O}=a\left(v_{P}-v_{N}\right) \tag{1.9}
\end{equation*}
$$
where $a$ (in $\mathrm{V} / \mathrm{V}$ ) is the voltage gain (see Fig. 1.27a). In order to function, an op amp needs to be powered. Figure $1.27 a$ shows dual power supplies of $\pm V_{S}$, but a single supply is also common. (To reduce cluttering, it is customary to omit showing the supplies explicitly.) Physically, an op amp cannot swing $v_{O}$ above $+V_{S}$ or below $-V_{S}$. Overdriving it will simply cause $v_{O}$ to saturate at some voltage $V_{O H}$ in the vicinity of $+V_{S}$ or at some voltage $V_{O L}$ in the vicinity of $-V_{S}$, so Eq. (1.9) holds only so long as we confine $v_{O}$ within the range $V_{O L}<v_{O}<V_{O H}$, aptly called the linear output range. Figure $1.27 b$ shows the op amp's voltage transfer curve (VTC).
As we move along we shall find that the higher the voltage gain $a$, the better (as an example, the venerable 741 op amp has $a=200,000 \mathrm{~V} / \mathrm{V}$, also expressed as
image_name:(a)
description:
[
name: a, type: OpAmp, value: a, ports: {InP: vP, InN: vN, OutP: vO, OutN: ', Vdd: +VS, -Vdd: -VS'}
]
extrainfo:The diagram (a) shows an operational amplifier with gain 'a'. The op amp is powered by positive and negative supply voltages +VS and -VS. The output voltage vO is a function of the difference between the input voltages vP and vN, specifically vO = a(vP - vN), within the linear range defined by VOL < vO < VOH.
image_name:(b)
description:The graph in Figure 1.27(b) is a voltage transfer curve (VTC) for an operational amplifier (op amp). This graph is a plot of the output voltage \( v_O \) versus the difference in input voltages \( v_P - v_N \).
1. **Type of Graph and Function:**
- The graph is a voltage transfer characteristic curve, specifically for an operational amplifier.
2. **Axes Labels and Units:**
- The horizontal axis represents the differential input voltage \( v_P - v_N \).
- The vertical axis represents the output voltage \( v_O \).
- Both axes are likely in volts, although specific units are not marked.
3. **Overall Behavior and Trends:**
- The graph shows a linear region where the slope is indicated by \( a \), which represents the gain of the op amp.
- Outside this linear region, the output voltage saturates at \( V_{OH} \) for positive input voltage differences and at \( V_{OL} \) for negative input voltage differences.
- The linear region is very narrow due to the high gain \( a \), demonstrating that only a small input voltage difference is needed to drive the output to saturation.
4. **Key Features and Technical Details:**
- The slope \( a \) in the linear region is the gain of the op amp, which can be extremely high, such as 200,000 V/V for a typical op amp like the 741.
- The saturation levels \( V_{OH} \) and \( V_{OL} \) correspond to the positive and negative supply voltages \( +V_S \) and \( -V_S \), respectively.
- The graph visually emphasizes the op amp’s ability to amplify small input differences to large output voltages within its linear range.
5. **Annotations and Specific Data Points:**
- There are no specific numerical values marked on the graph, but it is understood that \( V_{OH} \) and \( V_{OL} \) are close to the supply voltages \( +V_S \) and \( -V_S \).
- The linear region is centered around the origin \( (0,0) \), indicating that for zero input voltage difference, the output is also zero, assuming ideal conditions.
- The graph highlights the concept of saturation, where the output voltage cannot increase beyond certain limits regardless of further increases in input voltage difference.
image_name:(c)
description:
[
name: A2, type: OpAmp, value: ∞, ports: {InP: vP, InN: vN, Out: vO}
]
extrainfo:The op-amp in diagram (c) is ideal with an infinite gain and zero input voltage difference. It outputs a current iO at the output vO.
FIGURE 1.27 (a) Op amp symbol and labels. (b) The gain $a$ is the slope of the voltage transfer curve (VTC). (c) The input voltage of an ideal op amp approaches 0 V . Moreover, it draws no input currents.
$a=0.2 \mathrm{~V} / \mu \mathrm{V})$. Due to the sheer size of its gain, an op amp needs only a vanishingly small difference $v_{P}-v_{N}$ at the input to sustain a given voltage $v_{O}$ at the output (as an example, to sustain 1 V at the output, a 741 needs only $5 \mu \mathrm{~V}$ at the input!). Rewriting Eq. (1.9) as $\left(v_{P}-v_{N}\right)=v_{O} / a$, we get, in the ideal op amp limit of an infinitely high gain,
$$
\lim _{a \rightarrow \infty}\left(v_{P}-v_{N}\right)=\lim _{a \rightarrow \infty} \frac{v_{O}}{a}=0
$$
Op amps are designed to operate with negative feedback, an arrangement that allows the amplifier to influence its inverting input $v_{N}$ via an external network called the feedback network. With this viewpoint in mind, we express the above relation as
$$
\begin{equation*}
\lim _{a \rightarrow \infty} v_{N}=v_{P} \tag{1.10}
\end{equation*}
$$
which forms the basis of the important rule that engineers use to analyze op amp circuits:
Op Amp Rule: When given the ability to influence its own input $v_{N}$ via negative feedback, an ideal op amp will output whatever voltage $v_{O}$ and current $i_{O}$ it takes to force $v_{N}$ to track $v_{p}$. Moreover, the op amp will do this without drawing any current at either input pin (see Fig. 1.27c).
Let us put to use this rule to review the most popular op amp circuits.
### Basic Op Amp Circuits
The most popular op amp circuits are the noninverting amplifier, the inverting amplifier, the summing amplifier, and the voltage buffer.
- The Noninverting Amplifier: In the circuit of Fig. $1.28 a$ the op amp influences $v_{N}$ via the voltage divider made up of $R_{1}$ and $R_{2}$ to give
$$
v_{N}=\frac{R_{1}}{R_{1}+R_{2}} v_{O}=\frac{v_{O}}{1+R_{2} / R_{1}}
$$
By the op amp rule we have $v_{N}=v_{P}\left(=v_{I}\right)$. Consequently, replacing $v_{N}$ with $v_{I}$ in the above expression and solving for the ratio $v_{O} / v_{I}$ gives
$$
\begin{equation*}
A=\frac{v_{O}}{v_{I}}=1+\frac{R_{2}}{R_{1}} \tag{1.11}
\end{equation*}
$$
image_name:(a)
description:
[
name: V_I, type: VoltageSource, value: VI, ports: {Np: V_I, Nn: GND}
name: OpAmp, type: OpAmp, value: ∞, ports: {InP: V_I_, InN: V_N, OutP: Vo}
name: R1, type: Resistor, value: R1, ports: {N1: V_N_, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vo, N2: V_N}
]
extrainfo:This is a noninverting amplifier circuit with a gain of 1 + R2/R1. The input voltage Vin is applied to the non-inverting input of the op-amp, and the output voltage Vo is fed back to the inverting input through a voltage divider formed by R1 and R2.
image_name:(b)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: Vi, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vi, N2: 0V}
name: R2, type: Resistor, value: R2, ports: {N1: 0V, N2: Vo}
name: OpAmp, type: OpAmp, value: ∞, ports: {InP: GND, InN: 0V, OutP: Vo}
]
extrainfo:This is an inverting amplifier circuit where the voltage gain is determined by the ratio of R2 to R1. The op-amp is ideal with infinite gain. The input voltage is connected to the inverting terminal through R1, and the feedback is provided by R2.
FIGURE 1.28 (a) Noninverting and (b) inverting op amp configurations.
where $A$ represents the gain of the entire circuit (not to be confused with the gain $a(\rightarrow \infty)$ of the basic op amp). Since $v_{O}$ has the same polarity as $v_{I}$ the circuit is referred to as noninverting amplifier.
- The Inverting Amplifier: In the circuit of Fig. $1.28 b$ the op amp influences $v_{N}$ via the feedback resistance $R_{2}$, and since the op amp rule implies $v_{N}=v_{P}=0$, we refer to node $v_{N}$ as a virtual ground. Any current injected by $v_{I}$ via $R_{1}$ is removed by $v_{O}$ via $R_{2}$, or $i_{1}=i_{2}$. Using Ohm's law,
$$
\frac{v_{I}-0}{R_{1}}=\frac{0-v_{O}}{R_{2}}
$$
Solving again for the ratio $v_{O} / v_{I}$ gives
$$
\begin{equation*}
A=\frac{v_{O}}{v_{I}}=-\frac{R_{2}}{R_{1}} \tag{1.12}
\end{equation*}
$$
Since the polarity of $v_{O}$ is opposite to that of $v_{I}$ the circuit is called an inverting amplifier.
- The Summing Amplifier: By the op amp rule, the inverting-input node in Fig. 1.29 is at virtual ground. This node is called a summing junction because it sums the currents coming from the input sources $v_{1}$ and $v_{2}$ and diverts this sum to the output node $v_{O}$ to give
$$
\frac{v_{1}-0}{R_{1}}+\frac{v_{2}-0}{R_{2}}=\frac{0-v_{0}}{R_{3}}
$$
Solving for $v_{o}$,
$$
\begin{equation*}
v_{O}=-\left(\frac{R_{3}}{R_{1}} v_{1}+\frac{R_{3}}{R_{2}} v_{2}\right) \tag{1.13}
\end{equation*}
$$
If $R_{1}=R_{2}$, the circuit gives $v_{O}=-\left(R_{3} / R_{1}\right)\left(v_{1}+v_{2}\right)$ and is aptly called a summing amplifier.
- The Voltage Buffer: Letting $R_{2}=0$ and $R_{1}=\infty$ in the circuit of Fig. $1.28 a$ turns it into a unity-gain amplifier $(A=1 \mathrm{~V} / \mathrm{V})$. Its main application is as a voltage buffer to eliminate inter-stage loading. As an example, consider Fig. 1.30a, where a signal
image_name:FIGURE 1.29
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: v1, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: v1, N2: InN}
name: R2, type: Resistor, value: R2, ports: {N1: v2, N2: InN}
name: V2, type: VoltageSource, value: V2, ports: {Np: v2, Nn: GND}
name: R3, type: Resistor, value: R3, ports: {N1: InN, N2: vO}
name: OpAmp, type: OpAmp, value: OpAmp, ports: {InP: GND, InN: InN, OutP: vO}
]
extrainfo:This is a summing amplifier circuit. The output voltage vO is a weighted sum of the input voltages v1 and v2, inverted by the operational amplifier. The circuit is configured with resistors R1, R2, and R3, and two voltage sources V1 and V2.
image_name:(a)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: v1, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: v1, N2: v2}
name: R2, type: Resistor, value: R2, ports: {N1: v2, N2: GND}
]
extrainfo:This circuit represents a voltage divider. The voltage at node v2 is a fraction of the input voltage v1, determined by the resistances R1 and R2. The diagram illustrates that v2 is less than v1.
(a)
image_name:(b)
description:
[
name: V1, type: VoltageSource, value: v1, ports: {Np: v1, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: v1, N2: InP}
name: OpAmp, type: OpAmp, ports: {InP: InP, InN: Vo, OutP: Vo, OutN: GND, Vdd: +Vs, -Vdd: -Vs}
name: R2, type: Resistor, value: R2, ports: {N1: Vo, N2: GND}
]
extrainfo:This circuit uses a unity-gain voltage buffer (op-amp) to eliminate loading effects. The input voltage v1 is buffered by the op-amp, providing an output voltage v2 equal to v1, regardless of the load connected to v2. The op-amp has infinite input impedance and zero output impedance, preventing any current draw from R1.
FIGURE 1.30 Using a unity-gain voltage buffer to eliminate loading (current polarities shown for $v_{1}>0$ ).
source $v_{1}$ with internal resistance $R_{1}$ is to be fed to a load $R_{2}$. If we connect the source to the load via a plain wire, $R_{2}$ will form a voltage divider with $R_{1}$, giving $v_{2}=$ $v_{1} /\left(1+R_{1} / R_{2}\right)$. Clearly $v_{2}$ is less than $v_{1}$, a situation referred to as loading and stemming from the fact that $R_{2}$ draws current via $R_{1}$, so there is voltage loss across $R_{1}$.
However, if we couple the source to the load via a buffer as in Fig. 1.30b, there will be no voltage drop across $R_{1}$ because the op amp is designed to draw no input currents. Consequently the buffer eliminates loading to give $v_{2}=v_{1}$. Of course $R_{2}$ does draw current, but this is supplied by the op amp, which in turn draws it from the power supply $+V_{S}$ rather than from $v_{1}$. (The illustration refers to the case $v_{1}>0$; for $v_{1}<0$ the load current will flow from $R_{2}$ through the op amp to $-V_{S}$.)
The above configurations show up so often, either on their own or as subcircuits of more complex systems, that we shall apply Eqs. (1.10) through (1.13) quite frequently.
### Our First Diode/Op-Amp Circuit
Having reviewed op amp basics, we are now ready to investigate our first diode/opamp circuit, shown in Fig. 1.31a. Where do we begin? As a rule, start out using simple inspection to see if you can identify already familiar subcircuits, and then build up your understanding from there, one step at a time. In the present case we observe that $D_{2}$ and $R_{3}$ form a half-wave rectifier of the type of Fig. 1.10a, so we can follow the line of reasoning developed there and analyze the cases $v_{I}>0$ and $v_{I}<0$ separately.
image_name:(a)
description:
[
name: VI, type: VoltageSource, value: vI, ports: {Np: VI, Nn: GND}
name: R1, type: Resistor, value: 10kΩ, ports: {N1: X1, N2: Inn(∞)}
name: R2, type: Resistor, value: 10kΩ, ports: {N1: Inn(-∞), N2: VO}
name: R3, type: Resistor, value: 10kΩ, ports: {N1: InP(∞), N2: GND}
name: D1, type: Diode, ports: {Na: X1, Nc: Inn(-∞)}
name: D2, type: Diode, ports: {Na: VI, Nc: InP(∞)}
name: OpAmp, type: OpAmp, ports: {InP: InP(∞), InN: Inn(-∞), OutP: VO}
]
extrainfo:The circuit is a diode/op-amp configuration with a half-wave rectifier formed by D2 and R3. The op-amp is used for signal processing, and the circuit analyzes input conditions where vI is greater than or less than zero separately.
image_name:(b)
description:The graph depicted is a time-domain waveform illustrating the input and output voltages of a diode/op-amp circuit. The x-axis is labeled 'Time t', indicating that the graph plots voltage changes over time. The y-axis is labeled 'Waveforms', representing voltage levels without specific units given.
The waveform for the input voltage, denoted as \( v_I \), is a sinusoidal wave that oscillates above and below the horizontal axis, indicating alternating positive and negative values. This waveform is shown in a lighter color.
The output voltage waveform, denoted as \( v_O \), is depicted in a darker color and only oscillates above the horizontal axis. This indicates that the circuit is performing a half-wave rectification, allowing only the positive half-cycles of the input waveform to pass through while blocking the negative half-cycles.
Key features of this graph include:
- The input waveform \( v_I \) is a standard sinusoidal wave, showing periodicity with equal positive and negative amplitudes.
- The output waveform \( v_O \) follows the positive half of the input wave, demonstrating the rectification process.
- There are zero crossings at the points where the input wave transitions from positive to negative values and vice versa.
Overall, the graph clearly illustrates the function of a half-wave rectifier in processing an alternating input signal to produce a unidirectional output signal.
(b)
FIGURE 1.31 (a) Our first diode/op-amp circuit, and (b) its input and output waveforms.
image_name:Figure 1.32a
description:
[
name: R1, type: Resistor, value: 10kΩ, ports: {N1: X1, N2: vN}
name: R2, type: Resistor, value: 10kΩ, ports: {N1: vN, N2: vO}
name: R3, type: Resistor, value: 10kΩ, ports: {N1: vP, N2: GND}
name: D1, type: Diode, ports: {Na: X1, Nc: vN}
name: D2, type: Diode, ports: {Na: X1, Nc: vP}
name: V1, type: VoltageSource, ports: {Np: X1, Nn: GND}
name: OpAmp, type: OpAmp, ports: {InP: vP, InN: vN, OutP: vO}
]
extrainfo:The circuit is a half-wave rectifier using diodes and an op-amp. For vI > 0, D2 is on, allowing the input voltage to pass through to the output. For vI < 0, D2 is off, and the output is 0.
image_name:Figure 1.32b
description:
[
name: V1, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: 10 kΩ, ports: {N1: Vin, N2: VN}
name: R2, type: Resistor, value: 10 kΩ, ports: {N1: VN, N2: Vout}
name: R3, type: Resistor, value: 10 kΩ, ports: {N1: VP, N2: GND}
name: D1, type: Diode, ports: {Na: VN, Nc: Vin}
name: D2, type: Diode, ports: {Na: Vin, Nc: VP}
name: OpAmp, type: OpAmp, ports: {InP: VP, InN: VN, OutP: Vout}
]
extrainfo:The circuit is a precision rectifier using an op-amp and diodes. It processes an AC input to produce a rectified output, allowing current flow only during specific input voltage conditions.
FIGURE 1.32 Redrawing the circuit of Fig. 1.31a for (a) $v_{l}>0$ and (b) $v_{l}<0$.
- For $v_{I}>0, D_{2}$ is on, making $v_{P}=v_{I}$. But, by the op amp rule we have $v_{N}=v_{P}$, and thus $v_{N}=v_{I}$. This causes $D_{1}$ to be off, as pictured in Fig. 1.32a. In the absence of any current through $R_{2}$ the op amp gives $v_{O}=v_{N}$, so
$$
\begin{equation*}
v_{O}=v_{I} \tag{1.14a}
\end{equation*}
$$
- For $v_{I}<0, D_{2}$ is off, making $v_{P}=0$ and thus, by the op amp rule, $v_{N}=0 . D_{1}$ is now on, as pictured in Fig. 1.32b, and the op amp acts as an inverting amplifier to give
$$
\begin{equation*}
v_{O}=-\frac{R_{2}}{R_{1}} v_{I}=-\frac{10}{10} v_{I}=-v_{I} \tag{1.14b}
\end{equation*}
$$
- We combine the two expressions by writing
$$
\begin{equation*}
v_{O}=\left|v_{I}\right| \tag{1.15}
\end{equation*}
$$
and by stating that the circuit is a full-wave rectifier. The function is similar to that provided by the circuit of Fig. 1.12a and graphed in Fig. 1.13. There is a difference, however: in the circuit of Fig. 1.12a the rectified signal appears across a floating load, whereas in the op amp version of Fig. 1.31a the rectified signal is referenced to ground and as such it can be applied to a grounded load.
#### Exercise 1.4
Find $v_{O}$ in the circuit of Fig. 1.31a if (a) $R_{3}$ is doubled; (b) $R_{2}$ is doubled; (c) $R_{1}$ is doubled; (d) the direction of each diode is reversed; (e) only the direction of $D_{1}$ is reversed.
Ans. (a) $v_{O}=\left|v_{I}\right| ;$ (b) $v_{O}=v_{I}$ for $v_{I}>0 ; v_{O}=-2 v_{I}$ for $v_{I}<0 ;$ (c) $v_{O}=v_{I}$ for $v_{I}>0$, $v_{O}=-0.5 v_{I}$ for $v_{I}<0 ;(d) v_{O}=-\left|v_{I}\right| ;(e) v_{O}=v_{I}$ for $v_{I}>0, v_{O}=0$ for $v_{I}<0$.
## 1.4 SEMICONDUCTORS
The material in widest use by the semiconductor industry today is silicon $(\mathrm{Si})$, an element of Group IV of the periodic table of elements (see the portion shown in Table 1.1). The atoms of Group IV elements possess four electrons in their outer electron shell, also called the valence band. Each atom shares these four electrons with its four nearest neighbor atoms to form covalent bonds. These bonds keep atoms
TABLE 1.1 Portion of the Periodic Table with the most common semiconductor and dopant elements.
| III | IV | V |
| :--- | :--- | :--- |
| 5 | 6 | 7 |
| B | $\mathbf{C}$ | $\mathbf{N}$ |
| Boron | Carbon | Nitrogen |
| 13 | 14 | 15 |
| Al | $\mathbf{S i}$ | $\mathbf{P}$ |
| Aluminum | Silicon | Phosphorus |
| 31 | 32 | 33 |
| Ga | $\mathbf{G e}$ | As |
| Gallium | Germanium | Arsenic |
| 49 | 50 | 51 |
| In | Sn | Sb |
| Indium | Tin | Antimony |
bound to fixed positions of an orderly spatial structure known as crystal lattice. This is depicted in the two-dimensional rendition of Fig. 1.33a. The number of silicon atoms per unit volume (atoms $/ \mathrm{cm}^{3}$ ), also called atomic density, is
$$
\begin{equation*}
N_{s i}=5 \times 10^{22} \text { atoms } / \mathrm{cm}^{3} \tag{1.16}
\end{equation*}
$$
Due to thermal agitation, a covalent bond may break on occasion, freeing an electron which then becomes available for conduction. Consequently, the parent atom is said to be ionized. As we know, the electron charge is $-q$, where
$$
\begin{equation*}
q=1.602 \times 10^{-19} \mathrm{C} \tag{1.17}
\end{equation*}
$$
Once an electron moves away from a covalent site, it leaves behind a vacancy having charge $+q$, as shown in Fig. 1.33b. An electron from another covalent bond may fill this vacancy, leaving in turn behind another vacancy at the covalent site of origin.
image_name:(a)
description:The image consists of two diagrams labeled as (a) and (b).
1. **Identification of Components and Structure:**
- **Diagram (a):** This represents a lattice structure of pure silicon. Each circle labeled "Si" symbolizes a silicon atom. The atoms are arranged in a regular grid pattern, forming a crystal lattice. Each silicon atom is connected to four neighboring silicon atoms through lines, which represent covalent bonds. The smaller circles at the ends of these lines represent the shared electrons in the covalent bonds.
2. **Connections and Interactions:**
- In diagram (a), the silicon atoms are interconnected through covalent bonds, indicating a stable crystal structure without any free charge carriers.
3. **Labels, Annotations, and Key Features:**
- The silicon atoms are labeled "Si" in both diagrams.
4. **Diagram (b):** This shows the creation of an electron-hole pair within the silicon lattice.
- A missing electron from one of the covalent bonds creates a vacancy, referred to as a "hole," which is positively charged. This is indicated by a missing bond in the lattice and an arrow pointing to the vacancy, labeled "Free electron-hole pair."
- The electron that has moved away from its original covalent bond is now available for conduction, thus representing the concept of an electron-hole pair.
5. **Connections and Interactions:**
- The movement of electrons and the creation of holes are depicted, showing the dynamic process of electron-hole pair generation and potential recombination within the silicon crystal.
6. **Labels, Annotations, and Key Features:**
- The annotation "Free electron-hole pair" highlights the location of the vacancy and the electron's movement, illustrating the concept of thermal agitation leading to free charge carriers in the silicon lattice.
image_name:(b)
description:The image consists of two parts labeled (a) and (b), illustrating the atomic structure of silicon and the creation of an electron-hole pair.
1. **Identification of Components and Structure:**
- **(a) Pure Silicon:** The diagram shows a lattice structure of silicon atoms, each labeled with 'Si.' The silicon atoms are arranged in a grid-like pattern, representing the crystalline structure of pure silicon. Each silicon atom is connected to four neighboring atoms, indicating covalent bonds, depicted by lines connecting the atoms.
- **(b) Creation of an Electron-Hole Pair:** This part of the image shows a similar silicon lattice, but with an additional feature. One of the covalent bonds is broken, resulting in a free electron (shown as a small circle) and a positive hole (indicated by a circle with a '+' sign) where the electron was originally located.
2. **Connections and Interactions:**
- In both diagrams, the silicon atoms are interconnected through covalent bonds, illustrating the stable crystalline structure of silicon.
- In (b), the broken bond represents the thermal agitation process that frees an electron, creating an electron-hole pair. The arrow indicates the movement of the electron away from its original position, leaving behind a hole.
3. **Labels, Annotations, and Key Features:**
- The diagrams are labeled as (a) and (b) to differentiate between pure silicon and the electron-hole pair creation.
- In (b), a label 'Free electron-hole pair' is provided with an arrow pointing to the location where the electron has moved, highlighting the formation of the electron-hole pair due to thermal agitation.
FIGURE 1.33 (a) Pure silicon. (b) Creation of an electron-hole pair by thermal agitation.
As this process repeats itself, we are in effect witnessing the motion of positively charged vacancies, or holes, through the crystal.
Just as thermal agitation results in the creation of free electron-hole pairs, an electron and a hole may recombine and thus disappear from the pool of free charges. The recombination rate is proportional to the number of free electron-hole pairs available, which in turn is a strong function of temperature. In thermal equilibrium, the recombination rate equals the generation rate, resulting in an equilibrium electron concentration (or density) $n$ (electrons/cm ${ }^{3}$ ) and hole concentration (or density) $p$ (holes $/ \mathrm{cm}^{3}$ ) such that
$$
\begin{equation*}
n=p=n_{i} \tag{1.18}
\end{equation*}
$$
where $n_{i}$ is called the intrinsic concentration. For silicon, $n_{i}$ is such that
$$
\begin{equation*}
n_{i}^{2}(T)=B T^{3} e^{-V_{c 0} / V_{T}} \mathrm{~cm}^{-6} \tag{1.19}
\end{equation*}
$$
where $T$ is absolute temperature, in $\mathrm{K}, B$ is a suitable constant, $V_{G 0}=1.205 \mathrm{~V}$ is the bandgap voltage for silicon, and
$$
\begin{equation*}
V_{T}=\frac{k T}{q} \tag{1.20}
\end{equation*}
$$
is a temperature-dependent scaling factor, in V, often arising in semiconductor physics and called the thermal voltage. Here $q$ is the electron charge and $k=1.381 \times 10^{-23} \mathrm{~J} / \mathrm{K}$ is Boltzmann's constant. At room temperature ( $T=300 \mathrm{~K}$ ), we have $V_{T}=25.86 \mathrm{mV}$ $\cong 26 \mathrm{mV}$ 。
For silicon, Eq. (1.19) takes on the form
$$
\begin{equation*}
n_{i}^{2}(T)=1.5 \times 10^{33} T^{3} e^{-14,028 / T} \mathrm{~cm}^{-6} \tag{1.21}
\end{equation*}
$$
We observe that $n_{i}$ is a strong function of temperature. At $T=300 \mathrm{~K}$ we have $n_{i}^{2}=2 \times 10^{20} \mathrm{~cm}^{-6}$, or $n_{i}=1.4 \times 10^{10} / \mathrm{cm}^{3}$, indicating that only one in about $36 \times$ $10^{12}$ silicon atoms is ionized. By contrast, in a good conductor each atom contributes one or more electrons to conduction. It is apparent that at room temperature pure silicon is not much of a conductor.
### Doping
The electric properties of an element of Group IV can be altered dramatically by replacing some of its atoms with atoms of elements from the adjacent groups. For instance, replacing an atom of silicon with one of phosphorous $(\mathrm{P})$, which belongs to Group V and thus possesses five electrons in its outer shell, results in the situation of Fig. 1.34a. Four of the five electrons will go into forming covalent bonds, just like those of a silicon atom would; the fifth electron, due to thermal agitation, will wander throughout the crystal, no longer belonging to any particular atom and thus being free and available for conduction. Group V elements are referred to as donors in that each atom contributes, or donates, an electron to the silicon crystal. By contrast, replacing an atom of silicon with one of boron (B), which belongs to
image_name:(a)
description:The image labeled as "(a)" illustrates a silicon crystal lattice with a donor atom. In this diagram, silicon (Si) atoms are arranged in a regular pattern, each represented by circles labeled "Si". These silicon atoms are interconnected, indicating covalent bonds.
In the center of the lattice, one of the silicon atoms is replaced by a phosphorus (P) atom, which is shown as a shaded circle labeled "P". Phosphorus is a Group V element, meaning it has five electrons in its outer shell. When it replaces a silicon atom in the lattice, it forms four covalent bonds with neighboring silicon atoms, similar to a silicon atom. However, the fifth electron from the phosphorus atom becomes a free electron, depicted as a smaller circle outside the lattice with an arrow pointing to it, labeled "Free electron".
This free electron is not bound to any particular atom and can move freely throughout the crystal, contributing to electrical conduction. The presence of this free electron is what characterizes the phosphorus atom as a donor in the silicon lattice, as it donates an electron to the conduction band.
image_name:(b)
description:The image labeled as "(b)" illustrates a silicon crystal lattice that has been doped with an acceptor atom, specifically boron (B), which is a Group III element. In this diagram, the silicon (Si) atoms are depicted as circles, each connected to four adjacent silicon atoms, representing the typical tetrahedral covalent bonding structure of silicon.
1. **Identification of Components and Structure:**
- The silicon atoms are shown in a grid-like arrangement, each bonded to four neighboring silicon atoms, forming a part of the crystal lattice.
- A boron atom (B) is embedded within the silicon lattice, replacing one of the silicon atoms.
2. **Connections and Interactions:**
- The boron atom, having only three valence electrons, forms covalent bonds with three surrounding silicon atoms, leaving one bond incomplete. This incomplete bond creates a "hole," which is depicted in the diagram.
- The "hole" is illustrated as a positive charge, indicating its ability to accept an electron, thus facilitating the conduction process in the doped silicon.
3. **Labels, Annotations, and Key Features:**
- The boron atom is labeled with the letter "B" and is shaded differently to distinguish it from the silicon atoms.
- An arrow points to the "Free hole," highlighting the absence of an electron and the resulting positive charge.
- The diagram emphasizes the concept of "holes" in semiconductor physics, where the absence of an electron in the covalent bond allows for electrical conduction through electron movement into these holes, effectively making the holes act as positive charge carriers.
This representation helps in understanding how doping silicon with acceptor atoms like boron leads to the creation of p-type semiconductors, where the primary charge carriers are holes.
FIGURE 1.34 Silicon with (a) a donor atom, and (b) an acceptor atom.
Group III and thus possesses only three electrons in its outer shell, will lead to the situation of Fig. 1.34b. Here, the lack of a fourth electron results in a hole, and since holes in turn accept electrons when they recombine, Group III elements are referred to as acceptors.
The replacement of silicon atoms with donor or acceptor atoms is called doping. Since doped silicon is no longer pure, donor and acceptor atoms are collectively referred to as impurities. By doping silicon with a sufficient number of impurities, we can turn it into a good conductor-hence the reason for calling it a semiconductor. Doping can be achieved in more than one way. With solid-state diffusion, the doping material is deposited on a selected area of the silicon crystal, which is then placed in a high temperature furnace to force the impurity atoms to penetrate and diffuse into the underlying region of the crystal. With ion implantation, the silicon crystal is bombarded with ions of the desired impurity material, which then remain embedded in the crystal. Doped silicon can also be grown directly as a crystal, starting with a suitable mixture of silicon and impurity atoms of the desired type.
The donor and acceptor concentrations (atoms $/ \mathrm{cm}^{3}$ ), also called doping densities, are denoted as $N_{D}$ and $N_{A}$, respectively. Depending on the particular requirements, doping doses may range from as low as $10^{14}$ atoms $/ \mathrm{cm}^{3}$ to as high as $10^{21}$ atoms $/ \mathrm{cm}^{3}$, that is, practical impurity densities are always much higher than the room-temperature intrinsic electron-hole concentration ( $\left.n_{i}=1.4 \times 10^{10} / \mathrm{cm}^{3}\right)$. Consequently, at room temperature, silicon doped with donor impurities, also called $n$-type silicon, has $n>$ $N_{D}$, while silicon doped with acceptor impurities, also called p-type silicon, has $p>N_{A}$.
Regardless of the type and amount of doping, the electron and hole concentrations satisfy at all times the mass-action law,
$$
\begin{equation*}
n \times p=n_{i}^{2} \tag{1.22}
\end{equation*}
$$
or $n \times p=2 \times 10^{20} \mathrm{~cm}^{-6}$ at room temperature ( $T=300 \mathrm{~K}$ ). Consequently, in n-type silicon we have
$$
\begin{equation*}
n \cong N_{D} \quad p \cong \frac{n_{i}^{2}}{N_{D}} \tag{1.23a}
\end{equation*}
$$
while in p-type silicon we have
$$
\begin{equation*}
p \cong N_{A} \quad n \cong \frac{n_{i}^{2}}{N_{A}} \tag{1.23b}
\end{equation*}
$$
To put numbers in perspective, suppose some $n$-type silicon has been doped with $N_{D}=10^{16} / \mathrm{cm}^{3}$. Then, $n \cong 10^{16} / \mathrm{cm}^{3}$ and $p \cong 2 \times 10^{20} / 10^{16}=2 \times 10^{4} / \mathrm{cm}^{3}$, indicating a material much richer in electrons and much poorer in holes than intrinsic silicon. Since $n \gg p$, electrons in $n$-type silicon are aptly called majority charge carriers, and holes minority charge carriers. Conversely, a $p$-type silicon with $N_{A}=10^{18} / \mathrm{cm}^{3}$ would have $p \cong 10^{18} / \mathrm{cm}^{3}$ and $n \cong 2 \times 10^{2} / \mathrm{cm}^{3}$. Since now $p \gg n$, the majority carriers in $p$-type silicon are holes, and the minority carriers are electrons.
It is understood that the thermal generation of electron-hole pairs continues to take place just as in the intrinsic case. However, with such an abundance of majority carriers, the chance of recombining for minority carriers is now much higher, this being the reason for their much reduced concentration. In fact, the balance between the two charge types is governed by the mass-action law!
We note that the designations $n$-type and $p$-type identify only the type of majority carriers in the given material. They should not mislead the reader into regarding $n$-type material as negatively charged, or $p$-type material as positively charged! Regardless of the doping type, the material remains at all times neutrally charged because for every charge that has been freed there is the charge of the ionized atom left behind, which is of the opposite polarity. Figure. 1.35 depicts $n$ and $p$ for three significant cases.
### Drift and Diffusion Currents
There are two types of conduction mechanisms in semiconductors, often coexisting: drift and diffusion.
- The Drift Current: To discuss the drift mechanism, refer to Fig. 1.36a, top, where a slab of $p$-type material is assumed to be immersed in an electric field of strength $E$ (in $\mathrm{V} / \mathrm{cm}$ ). Such a field can be produced by connecting an external battery across the slab. If the slab is homogeneous, as assumed here, the
image_name:(a)
description:The graph labeled as "(a)" represents the mobile charge concentrations in a slab of pure silicon. It is a plot of charge concentration against position within the slab. The x-axis is labeled as 'x' and represents the position along the slab, ranging from 0 to L. The y-axis represents the concentration of charge carriers, measured in cm⁻³.
In this graph, the concentration of both holes (p) and electrons (n) is equal to the intrinsic carrier concentration, denoted as nᵢ. This is shown as a horizontal line at nᵢ across the entire length of the slab (from 0 to L), indicating uniform distribution. There are no variations or trends across the slab, as it is pure silicon with no doping. The graph is linear with no peaks, valleys, or inflection points, reflecting the intrinsic nature of the material. The scale is linear, and there are no additional annotations or markers on this graph.
image_name:(b)
description:The graph labeled '(b)' represents the mobile-charge concentrations in a slab of n-type silicon. The x-axis is labeled 'x' and represents the position along the slab, ranging from 0 to L. The y-axis is labeled '(cm^-3)' and represents the concentration of charge carriers in the silicon.
In this graph, there are two horizontal lines representing different charge carrier concentrations:
1. **Electron Concentration (n):** This is shown as a solid line at a level labeled 'N_D', which is the donor concentration. The electron concentration is constant across the slab, indicating a uniform distribution of donor atoms.
2. **Hole Concentration (p):** This is represented by a lower solid line at a level labeled 'n_i^2/N_D', where 'n_i' is the intrinsic carrier concentration. This line is much lower than the electron concentration line, reflecting the minority carrier concentration in n-type silicon.
There is also a dashed line labeled 'n_i', which represents the intrinsic carrier concentration. This line is positioned between the electron and hole concentration lines, indicating the natural carrier concentration level if no doping were present.
The graph shows a clear distinction between the majority carriers (electrons) and minority carriers (holes) in n-type silicon, with electrons being the predominant charge carriers due to the donor doping.
image_name:(c)
description:The graph labeled (c) represents the mobile charge concentrations in a slab of p-type silicon. This graph is a plot of charge carrier concentrations against position \( x \), with the horizontal axis labeled \( x \) and extending from 0 to \( L \). The vertical axis represents concentration in \( \text{cm}^{-3} \) and is plotted on a linear scale.
In the p-type silicon, the concentration of holes \( p \) is shown as a constant value \( N_A \) across the slab. This indicates that the acceptor impurity concentration \( N_A \) is uniform throughout the material. The electron concentration \( n \), however, is much lower and is shown as \( n_i^2 / N_A \), where \( n_i \) is the intrinsic carrier concentration. This reflects the minority carrier concentration in p-type material.
A dashed line at \( n_i \) represents the intrinsic carrier concentration level, which lies above the electron concentration and below the hole concentration. The graph clearly shows that in p-type silicon, holes are the majority carriers, and electrons are the minority carriers, with a significant difference between their concentrations. The flat lines for both \( p \) and \( n \) indicate that these concentrations do not vary with position \( x \) across the slab, illustrating a homogeneous distribution of charge carriers.
FIGURE 1.35 Mobile-charge concentrations in a slab of (a) pure silicon, (b) n-type silicon, and (c) p-type silicon. (The vertical scales are logarithmic.)
image_name:(a)
description:The image labeled "(a)" illustrates the concept of current drift in a semiconductor slab, specifically for holes. The diagram is divided into two main sections: the physical representation of the slab at the top and a graph below it.
1. **Identification of Components and Structure:**
- The top section shows a rectangular slab with a cross-sectional area labeled as "A." Inside the slab, there are symbols representing positive charges (holes), depicted as circles with a plus sign inside.
- An electric field, denoted by "E," is applied across the slab, pointing from left to right, indicating the direction of the field.
- The slab is divided into a small section with thickness labeled as "dx."
2. **Connections and Interactions:**
- The holes are shown moving in the direction of the electric field "E," illustrating the drift current. The movement of holes is represented by arrows pointing in the same direction as the electric field.
- The current density due to hole drift is labeled as "J_p(drift)," also pointing in the direction of the field.
3. **Labels, Annotations, and Key Features:**
- Below the slab, a graph plots potential "v(x)" against position "x." The potential decreases linearly from left to right, indicating a uniform electric field across the slab.
- The slope of the potential graph is labeled "dv(x)/dx," representing the rate of change of potential with respect to position, which is constant due to the uniform field.
- The graph shows the potential starting from a positive value and decreasing to zero as it moves across the slab.
Overall, this diagram effectively illustrates the concept of drift current in a homogeneous semiconductor slab, where holes move under the influence of a constant electric field, resulting in a uniform drift current density across the slab.
image_name:v(x)
description:The graph labeled "v(x)" is a linear function graph that represents how the potential varies with position across a slab. The graph is a straight line, indicating a linear relationship between the potential \( v(x) \) and the position \( x \).
Axes Labels and Units:
- **Horizontal Axis (x-axis):** Represents the position \( x \) across the slab. The units are not specified, but it is typically in meters or centimeters in semiconductor contexts.
- **Vertical Axis (y-axis):** Represents the potential \( v(x) \). Again, units are not specified, but it is usually in volts.
Overall Behavior and Trends:
The graph shows a decreasing linear trend, indicating that the potential \( v(x) \) decreases uniformly as the position \( x \) increases. This suggests a constant electric field across the slab, as the derivative \( dv(x)/dx \) is a constant negative value.
Key Features and Technical Details:
- The slope of the line \( dv(x)/dx \) represents the electric field \( E \), which is constant throughout the slab. The negative slope indicates that the electric field is in the direction of decreasing potential.
- The graph starts at a higher potential value at \( x = 0 \) and decreases linearly to zero.
Annotations and Specific Data Points:
- The graph is annotated with \( J_{p(drift)} \), indicating the direction of hole drift current, which is in the same direction as the electric field.
- The graph does not specify numerical values for the potential, slope, or position, focusing instead on the qualitative relationship between \( v(x) \) and \( x \).
image_name:(b)
description:The image labeled "(b)" illustrates the concept of current diffusion for the case of holes in a p-type silicon slab. The diagram is divided into two sections: the top part shows a three-dimensional representation of the slab, and the bottom part presents a graph plotting the concentration of holes against the position.
1. **Identification of Components and Structure:**
- The top section of the diagram shows a rectangular slab labeled with area "A." Inside the slab, circles with positive signs represent holes, the majority carriers in p-type silicon. The arrows indicate the direction of hole movement, which is from left to right across the slab.
- The bottom section of the diagram features a graph with the vertical axis labeled as "p(x)", representing the concentration of holes, and the horizontal axis labeled as "x," representing the position across the slab.
2. **Connections and Interactions:**
- The arrows within the slab indicate the diffusion process, where holes move from regions of higher concentration to regions of lower concentration. This movement results in a current labeled "J_p(diff)," which is directed from left to right.
- The graph below illustrates a linear decrease in hole concentration from left to right, represented by the slope "dp(x)/dx." This slope indicates the gradient driving the diffusion process.
3. **Labels, Annotations, and Key Features:**
- The slab is labeled with area "A," and the movement of holes is indicated with arrows.
- The graph includes the label "J_p(diff)" for the diffusion current and "dp(x)/dx" for the concentration gradient.
- The linear graph highlights the relationship between position and hole concentration, emphasizing the diffusion mechanism in the slab.
image_name:p(x)
description:The graph labeled \( p(x) \) represents the concentration of holes as a function of position \( x \) across a slab of p-type silicon. This is a linear graph illustrating hole diffusion.
1. **Type of Graph and Function:**
- The graph is a linear plot indicating the change in hole concentration \( p(x) \) across the slab.
- It represents the concept of diffusion in semiconductor physics.
2. **Axes Labels and Units:**
- The vertical axis is labeled \( p(x) \), representing the hole concentration.
- The horizontal axis is labeled \( x \), representing the position across the slab.
- The scales are linear, with no specific units mentioned for \( p(x) \) or \( x \).
3. **Overall Behavior and Trends:**
- The graph shows a linear decrease in hole concentration \( p(x) \) as the position \( x \) increases.
- This indicates a uniform gradient in hole concentration, typical of diffusion processes.
4. **Key Features and Technical Details:**
- The slope \( \frac{dp(x)}{dx} \) is negative, indicating a decrease in concentration with distance.
- There are no peaks, valleys, or inflection points; the graph is a straight line.
- The direction of the current due to diffusion, \( J_{p(diff)} \), is indicated as moving in the positive \( x \) direction.
5. **Annotations and Specific Data Points:**
- The graph is annotated with the derivative \( \frac{dp(x)}{dx} \), emphasizing the constant slope.
- The direction of diffusion is marked with an arrow labeled \( J_{p(diff)} \), showing the flow of holes.
FIGURE 1.36 Illustrating (a) current drift and (b) current diffusion for the case of holes.
potential $v(x)$ will vary linearly across the slab, as shown at the bottom. From basic physics we know that field and potential are related as
$$
\begin{equation*}
E=-\frac{d v(x)}{d x} \tag{1.24}
\end{equation*}
$$
Consequently, $E$ will be constant throughout the homogeneous slab.
Now, under the accelerating effect of $E$, holes will drift in the same direction as the field and achieve an average drift velocity $v_{p}$ (in $\mathrm{cm} / \mathrm{s}$ ) which is linearly proportional to the field strength,
$$
\begin{equation*}
v_{p}=\mu_{p} E \tag{1.25a}
\end{equation*}
$$
Aptly called the hole mobility, $\mu_{p}$ (in $\mathrm{cm}^{2} / \mathrm{Vs}$ ) gives a measure of the average drift velocity acquired by holes for a given applied field. As holes drift, they produce the current $i_{p(\text { drift })}=d Q_{p} / d t$, where $d Q_{p}$ is the amount of charge transferred during the interval $d t$. Given that during $d t$ holes travel the distance $d x=v_{p} d t$, the holes making up $d Q_{p}$ are contained within the volume $A d x=A v_{p} d t$, and their number is thus $p A v_{p} d t$, where $p$ is their concentration (holes $/ \mathrm{cm}^{3}$ ), and $A$ is the cross sectional area of the silicon slab (in $\mathrm{cm}^{2}$ ). Multiplying this number by the hole charge $+q$ gives $d Q_{p}=q p A v_{p} d t$, so
$$
i_{p(\mathrm{drift})}=\frac{d Q_{p}}{d t}=q p A v_{p}=q p A \mu_{p} E
$$
As we progress, we will find it more convenient to work with the current per unit area, or current densiy $J$ (in $\mathrm{A} / \mathrm{cm}^{2}$ ), rather than with the ordinary current $i$ (in A). The hole drift current density is simply $J_{p(\text { drift })}=i_{p(\text { drift })} / A$, or
$$
\begin{equation*}
J_{p(\mathrm{drift})}=q p \mu_{p} E \tag{1.25b}
\end{equation*}
$$
Similar considerations hold for a slab of $n$-type material, except that in this case the mobile charges are electrons, whose concentration and mobility are $n$ and $\mu_{n}$. Thus, the average drift velocity of electrons is
$$
\begin{equation*}
v_{n}=\mu_{n} E \tag{1.26a}
\end{equation*}
$$
where $\mu_{n}$ (in $\mathrm{cm}^{2} / \mathrm{Vs}$ ) is the electron mobility, and the electron drift current density is
$$
\begin{equation*}
J_{n(\mathrm{drift})}=q n \mu_{n} E \tag{1.26b}
\end{equation*}
$$
Equation (1.26b) is also at the basis of metals and ordinary conductors such as composition resistors, where the only type of mobile charges available are electrons. Both equations indicate the necessary ingredients for good conduction: high concentration along with high mobility.
- The Diffusion Current: The other mechanism for charge-carrier motion in semiconductors is diffusion-a mechanism not found in ordinary conductors. As we progress, we shall see that in semiconductor devices it is possible to establish and continuously maintain non-uniform profiles for the mobile charge densities. Figure $1.36 b$ shows an example of a linear density profile, such as that found in the base region of a forward-biased bipolar junction transistor. As holes wander randomly because of thermal agitation, they tend to diffuse from regions of higher density to regions of lower density, or toward the right in our example. This is similar to particles of smoke diffusing from the smoking area to the rest of a room. If holes are continuously injected to the left while being removed from the right, a sustained current flow will result. The hole diffusion current density is
$$
\begin{equation*}
J_{p(\mathrm{diff})}=-q D \frac{d p(x)}{d x} \tag{1.27a}
\end{equation*}
$$
where $D_{p}$ is the hole diffusivity (in $\mathrm{cm}^{2} / \mathrm{s}$ ). The negative sign stems from the fact that holes flow in the direction of the negative gradient in $p$. Likewise, the electron diffusion current density is
$$
\begin{equation*}
J_{n(\mathrm{diff})}=q D_{n} \frac{d n(x)}{d x} \tag{1.27b}
\end{equation*}
$$
image_name:
description:The image contains a continuation of a sentence explaining electron diffusivity. It states: "where $D_n$ is the electron diffusivity (in cm$^2$/s), and the sign is now positive due to the negative charge of electrons." This sentence clarifies that the electron diffusivity is measured in cm$^2$/s and emphasizes the positive sign in the electron diffusion current density equation due to the negative charge of electrons.
the negative charge of electrons.
We note strong similarities between the expressions for the drift and diffusion currents. In fact, substituting Eq. (1.24) into Eqs. (1.25b) and (1.26b) gives
$$
J_{p(\mathrm{drift})}=-q p \mu_{p} \frac{d v(x)}{d x} \quad J_{n(\mathrm{drift})}=q n \mu \frac{d v(x)}{d x}
$$
image_name:FIGURE 1.37
description:The graph in FIGURE 1.37 is a plot showing the dependence of electron (μ_n) and hole (μ_p) mobilities on the total doping density (N_A + N_D) at room temperature (300 K). It is a log-log plot with the x-axis labeled as \( N_A + N_D \) in \( \text{cm}^{-3} \), representing the total doping density, and the y-axis labeled as Mobility in \( \text{cm}^2/\text{Vs} \), representing the mobility of charge carriers.
Type of Graph and Function
This is a log-log plot showing the relationship between doping density and charge carrier mobility.
Axes Labels and Units
- **X-axis:** Total doping density \( N_A + N_D \) (\( \text{cm}^{-3} \)), logarithmic scale.
- **Y-axis:** Mobility (\( \text{cm}^2/\text{Vs} \)), linear scale.
Overall Behavior and Trends
- **Electron Mobility (μ_n):** Starts at a high value (around 1500 \( \text{cm}^2/\text{Vs} \)) at low doping densities and decreases steadily as the doping density increases.
- **Hole Mobility (μ_p):** Begins at a lower value (around 500 \( \text{cm}^2/\text{Vs} \)) compared to electrons and also decreases with increasing doping density.
Key Features and Technical Details
- Both mobilities show a decreasing trend as the doping density increases, indicating reduced mobility with higher impurity concentrations.
- The graph shows two empirical formulas for calculating the mobilities:
- \( \mu_n = 68 + \frac{1346}{1 + \left( \frac{N_A + N_D}{9.2 \times 10^{16}} \right)^{0.71}} \)
- \( \mu_p = 45 + \frac{427}{1 + \left( \frac{N_A + N_D}{2.2 \times 10^{17}} \right)^{0.72}} \)
Annotations and Specific Data Points
- The curves for both μ_n and μ_p are labeled on the graph.
- The empirical formulas are provided in a box to the right of the graph for reference.
This graph illustrates how increased impurity concentrations in semiconductors lead to decreased mobility of charge carriers, which is critical for understanding semiconductor behavior and device performance.
image_name:Empirical formulas
description:The image is a graph depicting the mobility of electrons (μₙ) and holes (μₚ) at a temperature of 300 K as a function of the total doping density (N_A + N_D) in cm⁻³. The x-axis represents the total doping density on a logarithmic scale ranging from 10¹⁴ to 10²⁰ cm⁻³, while the y-axis represents mobility in cm²/Vs, ranging from 0 to 1500 cm²/Vs.
Two curves are shown:
1. The curve for electron mobility (μₙ) starts at a higher mobility value and decreases as the doping density increases.
2. The curve for hole mobility (μₚ) starts at a lower mobility value and also decreases with increasing doping density.
To the right of the graph, empirical formulas for calculating the mobilities are provided:
- For electron mobility (μₙ):
\[ μₙ = 68 + \frac{1346}{1 + \left(\frac{N_A + N_D}{9.2 \times 10^{16}}\right)^{0.71}} \] cm²/Vs
- For hole mobility (μₚ):
\[ μₚ = 45 + \frac{427}{1 + \left(\frac{N_A + N_D}{2.2 \times 10^{17}}\right)^{0.72}} \] cm²/Vs
These formulas show how the mobilities are influenced by the total doping density, with both electron and hole mobilities decreasing as the doping density increases.
FIGURE 1.37 Room-temperature dependence of the mobilities on the total doping density, and empirical formulas for their calculation for the case of donor atoms of phosphorous and acceptor atoms of boron.
which are even closer in form to Eqs. (1.27a) and (1.27b). These equations indicate that:
- To sustain a given current we need a gradient (a voltage gradient to sustain drift, a density gradient to sustain diffusion).
- Charge flow is in the direction of a decreasing gradient.
- The diffusivities $D_{p}$ and $D_{n}$ play a similar role to the mobilities $\mu_{p}$ and $\mu_{n}$ in that each offers a measure of how much current stems from a given gradient. Indeed, it turns out that diffusivities and mobilities are related by Einstein's relations
$$
\begin{equation*}
\frac{D_{n}}{\mu_{n}}=\frac{D_{p}}{\mu_{p}}=V_{T} \tag{1.28}
\end{equation*}
$$
where $V_{T} \cong 26 \mathrm{mV}$ is the thermal voltage of Eq. (1.20).
Mobilities and diffusivities are greatest when silicon is pure, but decrease with doping as well as temperature. Figure 1.37 shows the dependence of $\mu_{n}$ and $\mu_{p}$ on the total doping density $\left(N_{A}+N_{D}\right)$, at room temperature. The higher mobility (by a factor of two to three) exhibited by electrons compared to holes is the primary reason why $n$-type materials are generally preferred over $p$-type materials, particularly in the fabrication of devices intended for high-speed operation.
Lastly, it must be pointed out that the linear relationships between velocities and electric field, expressed as $v_{n}=\mu_{n} E$ and $v_{p}=\mu_{p} E$, hold only up to a certain field strength, typically on the order of $5 \mathrm{kV} / \mathrm{cm}$. Past this limit, electron and hole velocities saturate at approximately $10^{7} \mathrm{~cm} / \mathrm{s}$. Aptly called velocity saturation, this phenomenon sets an upper limit on the speed of operation of semiconductor devices such as MOSFETs.
An Example: The Integrated-Circuit Diode
Figure 1.38 illustrates the most basic steps involved in the fabrication of the pn junction diode, a semiconductor device at the basis of most other integrated-circuit (IC) devices. Starting out with a lightly doped $n$-type slab, such as $N_{D}=10^{15} / \mathrm{cm}^{3}$, a localized boron diffusion is made to create a $p$-type region. Clearly, in order to overcome
image_name:(a)
description:The image labeled as "(a)" depicts the initial stage in the fabrication of a pn junction diode. It shows a rectangular block representing a slab of lightly doped n-type silicon, commonly referred to as "n- bulk silicon." This slab serves as the substrate for further processing. The n-type doping is indicated by the presence of donor atoms in a concentration typically around $N_{D}=10^{15} / \mathrm{cm}^{3}$. The diagram is a simple geometric representation without additional components, connections, or annotations other than the label "n- bulk silicon," which identifies the material and its doping type. This stage is foundational, as it sets the base upon which further diffusion and processing steps will be carried out to form the diode structure.
image_name:(b)
description:The image labeled (b) depicts a step in the fabrication process of an integrated-circuit diode. It shows the formation of a p-type region within a lightly doped n-type silicon substrate. The diagram illustrates a rectangular block representing the n-type bulk silicon, labeled as "n- bulk silicon," indicating a lightly doped n-type region. Over this substrate, a localized p-type region is formed through boron diffusion, depicted as a shaded area on the surface of the n-type block. This p-type region is essential for creating the pn junction necessary for diode operation. The interaction between the n-type and p-type regions forms the basis for the diode's rectifying behavior. The diagram does not include detailed annotations of electrical connections or other features, focusing primarily on the diffusion process to establish the p-type region within the n-type substrate.
image_name:(c)
description:The image labeled as (c) in Figure 1.38 illustrates the final step in the fabrication process of an integrated-circuit diode. This diagram shows a three-dimensional representation of a semiconductor structure. The main component visible is a rectangular block labeled as 'n⁻ bulk silicon,' indicating that it is composed of lightly doped n-type silicon. This bulk silicon serves as the substrate for the diode.
1. **Identification of Components and Structure:**
- The primary component is the 'n⁻ bulk silicon,' depicted as a solid rectangular block. This represents the foundational substrate material used in the diode fabrication.
2. **Connections and Interactions:**
- While the image does not explicitly show connections or wiring, it implies that this n-type substrate is part of a larger process where a p-type region would be diffused into this substrate to form a pn junction. The provision for connection to the outside, such as metal contacts, would be made in subsequent steps not shown in this particular image.
3. **Labels, Annotations, and Key Features:**
- The label 'n⁻ bulk silicon' is critical as it identifies the material type and doping level. The n⁻ notation indicates a lower concentration of donor atoms, which is typical for the substrate in semiconductor devices.
Overall, this image represents the substrate material that forms the basis for creating the pn junction diode, with the expectation that further processing will define the diode's electrical characteristics and connections.
(a)
image_name:(b)
description:The image depicts a simplified cross-sectional view of a semiconductor substrate used in the fabrication of an integrated circuit (IC) diode. The substrate is labeled 'n⁻ bulk,' indicating it is made of lightly doped n-type silicon, which serves as the base material for the diode. The term 'n⁻' signifies a lower concentration of donor atoms compared to heavily doped n-type regions. Within this substrate, there is a region labeled 'p diffusion,' representing an area where p-type impurities have been introduced through a diffusion process. This p-type region is essential for forming the pn junction, which is the core of diode functionality. The diagram highlights the initial steps in diode fabrication, where the p-type region is created within the n-type substrate, setting the stage for subsequent processes that will complete the diode structure and enable its electrical connections.
(b)
image_name:(b)
description:The diagram illustrates a cross-sectional view of a semiconductor structure involved in the fabrication of a diode. It highlights the p-type diffusion process within an n-type substrate. The image shows a rectangular block labeled 'Anode' positioned above a p-type region, which is depicted as a lightly shaded area within the substrate. Adjacent to this, a block labeled 'Cathode' is positioned above an n+ region, indicating a heavily doped n-type area. This n+ region is also within the n-type substrate, which is marked as n−, representing a lightly doped n-type material.
1. **Identification of Components and Structure:**
- **P-type Region (p):** This is where p-type impurities have been introduced, forming the anode of the diode.
- **N+ Region (n+):** A heavily doped n-type region that forms the cathode of the diode.
- **N- Substrate (n−):** The base n-type material where the p-type diffusion and n+ regions are created.
2. **Connections and Interactions:**
- The anode and cathode are positioned above their respective semiconductor regions, indicating the flow of current through the p-n junction formed between these regions.
- The p-n junction is the critical part of the diode that allows current to flow in one direction when forward-biased.
3. **Labels, Annotations, and Key Features:**
- The labels 'Anode' and 'Cathode' clearly indicate the terminals of the diode.
- The diagram shows the spatial arrangement of the p-type and n-type regions, essential for understanding the diode's function.
- The n+ region ensures an ohmic contact with the cathode, facilitating efficient current flow.
(c)
FIGURE 1.38 Basic fabrication steps of an IC diode: (a) starting material, (b) p-type diffusion, and (c) provision for its connection to the outside.
the existing $n$-type nature of this region, the acceptor density $N_{A}$ must exceed the existing donor density $N_{D}$ there. Then, in this region we have
$$
p \cong N_{A}-N_{D} \quad n \cong \frac{n_{i}^{2}}{N_{A}-N_{D}}
$$
An additional diffusion is made to create a heavily doped $n$-type region to ensure an ohmic contact between the $n$-type slab and a metal (more on this later in the chapter), and finally metal depositions are made to allow for the interconnection of the device to external circuitry.
The dimensions of the above device are in the range of micro meters $\left(1 \mu \mathrm{~m}=10^{-6} \mathrm{~m}\right)$. Such tiny dimensions allow for the simultaneous fabrication of a very large number of devices on the same wafer. To prevent different devices from interfering with each other, we must keep them electrically isolated from each other. Interestingly enough, a popular way of achieving isolation is through additional reverse-biased pn junctions, a subject that we will illustrate in greater detail when studying the fabrication of transistors. The interested student is encouraged to search the Web for videos and articles illustrating the fascinating subject of integrated circuit fabrication.
Find the electron and hole concentrations $n$ and $p$ as well as the mobilities $\mu_{n}$ and $\mu_{p}$, and the diffusivities $D_{n}$ and $D_{p}$ in the three regions of the structure of Fig. 1.38, assuming the following doping densities:
(a) $n^{-}$-type bulk: $N_{D}=10^{15}$ phosphorous atoms $/ \mathrm{cm}^{3}$
(b) $p$-type diffusion: $N_{A}=10^{17}$ boron atoms $/ \mathrm{cm}^{3}$
(c) $n^{+}$-type diffusion: $N_{D}=10^{20}$ phosphorous atoms $/ \mathrm{cm}^{3}$
#### Solution
(a) We have $n \cong N_{D}=10^{15} / \mathrm{cm}^{3}$ and $p \cong n_{i}^{2} / N_{D}=2 \times 10^{20} / 10^{15}=2 \times 10^{5} / \mathrm{cm}^{3}$. Using the empirical formulas of Fig. 1.37, we find
$$
\begin{aligned}
& \mu_{n}=68+\frac{1346}{1+\left(\frac{10^{15}}{9.2 \times 10^{16}}\right)^{0.71}}=1362 \mathrm{~cm}^{2} / \mathrm{Vs} \\
& \mu_{p}=45+\frac{427}{1+\left(\frac{10^{15}}{2.2 \times 10^{17}}\right)^{0.72}}=463 \mathrm{~cm}^{2} / \mathrm{Vs}
\end{aligned}
$$
Using Eq. (1.28), we find $D_{n}=0.026 \times 1362=35.4 \mathrm{~cm}^{2} / \mathrm{s}$ and $D_{p}=$ $0.026 \times 463=12 \mathrm{~cm}^{2} / \mathrm{s}$.
(b) We now have $p \cong N_{A}-N_{D}=10^{17}-10^{15} \cong 10^{17} / \mathrm{cm}^{3}$ and $n \cong n_{i}^{2} /\left(N_{A}-N_{D}\right) \cong$ $2 \times 10^{3} / \mathrm{cm}^{3}$. Using again the empirical formulas,
$$
\begin{aligned}
& \mu_{n}=68+\frac{1346}{1+\left(\frac{10^{17}+10^{15}}{9.2 \times 10^{16}}\right)^{0.71}}=719 \mathrm{~cm}^{2} / \mathrm{Vs} \\
& \mu_{p}=45+\frac{427}{1+\left(\frac{10^{17}+10^{15}}{2.2 \times 10^{17}}\right)^{0.72}}=317 \mathrm{~cm}^{2} / \mathrm{Vs}
\end{aligned}
$$
Moreover, $D_{n}=0.026 \times 719=18.7 \mathrm{~cm}^{2} / \mathrm{s}$ and $D_{p}=8.3 \mathrm{~cm}^{2} / \mathrm{s}$.
(c) We now have $n \cong 10^{20}+10^{15} \cong 10^{20} / \mathrm{cm}^{3}, p \cong 2 / \mathrm{cm}^{3} ; \mu_{n}=78 \mathrm{~cm}^{2} / \mathrm{Vs}$, $D_{n}=2 \mathrm{~cm}^{2} / \mathrm{s} ; \mu_{p}=50 \mathrm{~cm}^{2} / \mathrm{Vs}$, and $D_{p}=1.3 \mathrm{~cm}^{2} / \mathrm{s}$.
## 1.5 THE pn JUNCTION IN EQUILIBRIUM
When a $p$-type and an $n$-type region are joined together, they are said to form a $p n$ junction. Even though in practice they are fabricated contiguously as exemplified in Fig. 1.38, from a pedagogical viewpoint it is convenient to consider two slabs that have been fabricated separately and are brought into contact with each other subsequently, in the manner depicted in Fig. 1.39, top. To develop a numerical feel for the various quantities involved, we shall work with the following doping concentration example:
$$
\begin{equation*}
N_{A}=10^{18} / \mathrm{cm}^{3} \quad N_{D}=10^{16} / \mathrm{cm}^{3} \tag{1.29}
\end{equation*}
$$
Assume donor atoms of phosphorous and acceptor atoms of boron, so we can use the formulas of Fig. 1.37, when necessary. Using the subscript zero to identify equilibrium concentrations, we exploit Eq. (1.23b) to find the $p$-side hole and electron concentrations
$$
\begin{equation*}
p_{p 0} \cong N_{A}=10^{18} / \mathrm{cm}^{3} \quad n_{p 0} \cong \frac{n_{i}^{2}}{N_{A}}=2 \times 10^{2} / \mathrm{cm}^{3} \tag{1.30a}
\end{equation*}
$$
and we exploit Eq. (1.23a) to find the $n$-side electron and hole concentrations
$$
\begin{equation*}
n_{n 0} \cong N_{D}=10^{16} / \mathrm{cm}^{3} \quad p_{n 0} \cong \frac{n_{i}^{2}}{N_{D}}=2 \times 10^{4} / \mathrm{cm}^{3} \tag{1.30b}
\end{equation*}
$$
Once the two slabs are brought into contact, holes will diffuse from the $p$-side, where they are highly concentrated $\left(10^{18}\right.$ holes $\left./ \mathrm{cm}^{3}\right)$, toward the $n$-side, where they are concentrated only sparingly ( $2 \times 10^{4}$ holes $/ \mathrm{cm}^{3}$. $)$ Likewise, electrons will diffuse in the opposite direction. However, every hole diffusing across the metallurgical junction leaves behind a negatively charged ion, just as every diffusing electron leaves behind a positively charged ion. These ions are bound to their fixed positions in the crystal lattice and do not contribute to current. However, they form a space charge layer (SCL), also called depletion layer because it is essentially depleted of mobile charges
image_name:FIGURE 1.39 Equilibrium conditions in a pn slab.
description:The diagram titled "FIGURE 1.39 Equilibrium conditions in a pn slab" illustrates the equilibrium state in a pn junction. The image is divided into several sections, each depicting different aspects of the junction's behavior and properties.
1. **Identification of Components and Structure:**
- The top part of the diagram shows a cross-sectional view of a pn junction, with the p-type region on the left and the n-type region on the right. The p-type region contains holes (positive charge carriers), while the n-type region contains electrons (negative charge carriers).
- A space-charge layer (SCL) or depletion region is visible at the junction between the p-type and n-type regions. This region is characterized by the presence of negative ions in the p-type region and positive ions in the n-type region.
- An electric field (E) is depicted, opposing the diffusion of charge carriers across the junction.
2. **Connections and Interactions:**
- The diagram illustrates the diffusion of holes and electrons across the junction, leading to the formation of the space-charge layer. This diffusion results in the establishment of an electric field (E) that counterbalances further diffusion, leading to equilibrium.
- The electric field direction is shown with arrows, indicating its opposing effect on the diffusion of charge carriers.
3. **Labels, Annotations, and Key Features:**
- The concentrations of charge carriers (holes and electrons) are labeled as \( p_0 \) and \( n_0 \) for the p-type and n-type regions, respectively, with specific values given (e.g., \( p_{p0} = 10^{18} \) cm\(^{-3}\), \( n_{n0} = 10^{16} \) cm\(^{-3}\)).
- The charge density \( \rho \) is shown in a graph, with \( qN_D \) and \( -qN_A \) representing the charge densities in the n-type and p-type regions, respectively.
- The electric field \( E \) is plotted as a function of position \( x \), showing a peak at the junction and decreasing to zero in both directions.
- The potential \( \phi \) is also plotted, showing a smooth transition from \( \phi_p \) in the p-type region to \( \phi_n \) in the n-type region, with \( \phi_0 \) representing the built-in potential.
- Axis labels such as \( x \), \( n, p \) (cm\(^{-3}\)), \( \rho \) (C/cm\(^{3}\)), \( E \) (V/cm), and \( \phi \) (V) provide additional context for interpreting the graphs.
Overall, the diagram provides a comprehensive visualization of the equilibrium conditions in a pn junction, highlighting the distribution of charge carriers, the formation of the space-charge layer, and the resulting electric field and potential profiles.
image_name:n, p (cm^{-3})
description:The diagram illustrates equilibrium conditions in a pn junction slab, focusing on the distribution of charge carriers, electric field, and potential across the junction. It consists of several graphs stacked vertically, each depicting a different aspect of the junction.
1. **Charge Carrier Concentration (n, p in cm^{-3}):**
- The top graph shows the concentration of holes (p) and electrons (n) across the junction. The x-axis represents the position across the junction, labeled from -x_{p0} to x_{n0}, with the junction at x=0.
- On the p-type side (left), the hole concentration (p) is high, labeled as p_{p0} (10^{18} cm^{-3}), and decreases towards the junction.
- On the n-type side (right), the electron concentration (n) is high, labeled as n_{n0} (10^{16} cm^{-3}), and decreases towards the junction.
- The concentrations cross at the junction, indicating a depletion region where mobile charge carriers are reduced.
2. **Charge Density (ρ in C/cm^{3}):**
- This graph shows the charge density across the junction.
- The p-type side has negative charge density (-qN_A), and the n-type side has positive charge density (qN_D), both represented as step functions centered at x=0.
- The space-charge layer is highlighted, indicating the region where immobile ions create a space charge.
3. **Electric Field (E in V/cm):**
- The electric field graph shows a triangular distribution across the junction.
- It peaks negatively at the junction (-E_{m0}) and decreases to zero at the edges of the depletion region (-x_{p0} and x_{n0}).
- This field opposes the diffusion of charge carriers, maintaining equilibrium.
4. **Electric Potential (φ in V):**
- The potential graph shows a smooth transition from φ_p on the p-type side to φ_n on the n-type side.
- The potential increases from -x_{p0} to x_{n0}, indicating a built-in potential barrier φ_0 across the junction.
- The curve is sigmoid, reflecting the gradual change in potential across the depletion region.
Overall, these graphs collectively illustrate the balance of charge carriers, electric field, and potential that establishes equilibrium in a pn junction. The depletion region is characterized by a lack of mobile carriers, a built-in electric field, and a potential barrier that prevents further diffusion of carriers.
image_name:ρ (C/cm^{3})
description:The graph titled "ρ (C/cm^{3})" is a part of a series of diagrams representing equilibrium conditions in a pn junction. It specifically depicts the charge density ρ as a function of position x across the junction, showing the space-charge layer (SCL) or depletion region.
### Type of Graph and Function:
This is a spatial distribution graph showing charge density across a pn junction. It is a piecewise function graph that represents the distribution of charge density in the depletion region.
Axes Labels and Units:
- **Horizontal Axis (x):** Represents position across the junction, with units in centimeters (cm). The axis is centered at 0, with negative values extending into the p-type region and positive values into the n-type region.
- **Vertical Axis (ρ):** Represents charge density, with units in Coulombs per cubic centimeter (C/cm³).
Overall Behavior and Trends:
The graph shows a step function behavior:
- For the p-type region (negative x), the charge density ρ is constant and negative, indicating the presence of negative ions (acceptor ions).
- For the n-type region (positive x), the charge density ρ is constant and positive, indicating the presence of positive ions (donor ions).
- The charge density is zero at the junction (x = 0) and outside the depletion region.
Key Features and Technical Details:
- **Negative Charge Density (p-type):** The graph shows a constant negative charge density of \(-qN_A\) from \(-x_{p0}\) to 0.
- **Positive Charge Density (n-type):** The graph shows a constant positive charge density of \(qN_D\) from 0 to \(x_{n0}\).
- The charge density transitions sharply at the boundaries of the depletion region, \(-x_{p0}\) and \(x_{n0}\), indicating the edges of the space-charge layer.
Annotations and Specific Data Points:
- The graph is annotated with symbols \(-qN_A\) and \(qN_D\) to indicate the charge densities in the p-type and n-type regions, respectively.
- The boundaries of the depletion region are marked as \(-x_{p0}\) and \(x_{n0}\), where the charge density changes abruptly.
This graph is crucial for understanding how the electric field and potential develop across the pn junction, as it directly relates to the space-charge distribution that establishes the equilibrium condition in the junction.
image_name:E (V/cm)
description:The graph titled "E (V/cm)" is part of a series of diagrams illustrating the equilibrium conditions in a pn junction. This specific graph focuses on the electric field (E) as a function of position (x) across the junction.
### Type of Graph and Function:
- The graph is a spatial distribution plot showing how the electric field varies across the pn junction.
Axes Labels and Units:
- The horizontal axis is labeled "x" and represents the position across the junction, with units not explicitly stated but implied to be in centimeters (cm) based on context.
- The vertical axis is labeled "E" with units of volts per centimeter (V/cm).
Overall Behavior and Trends:
- The graph shows a V-shaped curve centered at the origin (x = 0), indicating the presence of an electric field across the space charge layer.
- The electric field has a negative peak at the center of the junction, denoted as -E_{m0}, and decreases symmetrically towards the edges of the depletion region.
Key Features and Technical Details:
- The graph is symmetric with respect to the origin, reflecting the balance in the electric field across the depletion layer.
- The electric field is zero outside the depletion region, indicating no electric field in the neutral p-type and n-type regions.
- The maximum negative value of the electric field is labeled as -E_{m0} at the center of the junction.
Annotations and Specific Data Points:
- The graph is annotated with key positions: -x_{p0} and x_{n0}, which mark the boundaries of the space charge layer.
- The electric field is zero at these boundary points, consistent with the absence of a field in the neutral regions.
This graph is crucial for understanding how the electric field counteracts the diffusion of charge carriers, leading to equilibrium in the pn junction.
FIGURE 1.39 Equilibrium conditions in a pn slab.
due to their diffusion across the junction. The SCL, in turn, establishes an electric field $E$ in the direction opposing diffusion. As holes and electrons keep diffusing, the SCL keeps building up, until an equilibrium condition is reached whereby the electric field $E$ will exactly counterbalance the tendency of holes and electrons to diffuse further. Thereafter, the net current across the junction will be zero.
### Equilibrium Conditions
We express the equilibrium conditions by writing $J_{p(\text { drifif })}+J_{p(\text { diff }}=0$ and $J_{n(\text { drift })}+$ $J_{n(d i f f)}=0$. Taking the origin of the $x$-axis at the point of contact between the $p$ and $n$ regions, also called the metallurgical junction, we have, by Eqs. (1.25) through (1.27),
$$
\begin{align*}
& q p(x) \mu_{p} E(x)-q D \frac{d p(x)}{d x}=0  \tag{1.31a}\\
& q n(x) \mu_{n} E(x)+q D_{n} \frac{d n(x)}{d x}=0 \tag{1.31b}
\end{align*}
$$
where we are emphasizing that $p, n$, and $E$ are now functions of the position $x$ along the $p n$ slab.
The equilibrium situation is illustrated further in Fig. 1.39, where the origin of the $x$ axis has been taken right at the metallurgical junction. The edges of the SCL are located at $-x_{p 0}$ and $+x_{n 0}$, respectively. The charge density $\rho$ (in $\mathrm{C} / \mathrm{cm}^{3}$ ) due to immobile ions is $+q N_{D}$ in the $n$ side of the SCL, and $-q N_{A}$ in the $p$ side. Denoting the cross-sectional area of the $p$ and $n$ slabs as $A$, we find the total SCL charge in the $n$-side as $Q^{+}=q N_{D} \times A x_{n 0}$, and the total SCL charge in the $p$-side as $Q^{-}=-q N_{A} \times A x_{p 0}$. Charge neutrality requires that $Q^{+}=-Q^{-}$, or $q N_{D} A x_{n 0}=q N_{A} A x_{p 0}$. Simplifying, we get
$$
\begin{equation*}
\frac{x_{p 0}}{x_{n 0}}=\frac{N_{D}}{N_{A}} \tag{1.32}
\end{equation*}
$$
indicating that in an asymmetrically doped $p n$ junction such as ours $\left(N_{A} \gg N_{D}\right)$, the SCL will extend mostly into the more lightly doped side $\left(x_{n 0} \gg x_{p 0}\right)$. This makes sense as it takes more volume in the lightly doped side to come up with the same number of ions as the heavily doped side. We have tried to convey this pictorially in Fig. 1.39, top.
We readily visualize the electric field strength $E$ as a function of $x$ by counting the field lines. Each line starts on a positive ion at the right and ends on a negative ion at the left. The number of lines is maximum at the metallurgical junction $(x=0)$ and decreases linearly as we move away on either side, to finally drop to zero at the edges of the SCL. The regions outside the SCL, where the electric field is zero, are aptly called the neutral regions. Because of asymmetric doping, the profile of $E$ is a scalene triangle, and a negative one as $E$ is in the direction of negative $x$.
We readily find a relationship between the maximum strength $E_{m 0}$ and the SCL edges $x_{p 0}$ and $x_{n 0}$ via Gauss's theorem. In a one-dimensional case such as this, this theorem is expressed as
$$
\begin{equation*}
\frac{d E}{d x}=\frac{\rho(x)}{\varepsilon_{s i}} \tag{1.33}
\end{equation*}
$$
where $\varepsilon_{s i}$ is silicon's permittivity $\left(\varepsilon_{s i}=1.04 \mathrm{pF} / \mathrm{cm}\right)$. In the right portion of the SCL we have $d E / d x=E_{m 0} / x_{n}$ and $\rho / \varepsilon_{s i}=q N_{D} / \varepsilon_{s i}$, so $E_{m 0} / x_{n 0}=q N_{D} / \varepsilon_{s i t}$. Applying similar considerations to the left side of the SCL and solving for $E_{m 0}$ gives
$$
\begin{equation*}
E_{m 0}=\frac{q N_{A} x_{p 0}}{\varepsilon_{s i}}=\frac{q N_{D} x_{n 0}}{\varepsilon_{s i}} \tag{1.34}
\end{equation*}
$$
### The Built-in Potential $\boldsymbol{\phi}_{\mathbf{0}}$
From basic electrostatics we know that an electric field is always accompanied by an electric potential gradient. For a one-dimensional situation such as ours, the relationship between field $E$ and potential $\phi$ is, by Eq. (1.24), $E=-d \phi / d x$. Rewriting as $\phi=-\int E d x$, we visualize $\phi$ as the negative of the area enclosed by the $E$ curve. Since $E$ has a linear profile, $\phi$ will have a quadratic profile, as shown in Fig. 1.39, bottom. We observe that outside the SCL the profile of $\phi$ is flat because $E=0$ there. The potentials there are denoted as $\phi_{p}$ and $\phi_{n}$, respectively. We now wish to find expressions for $\phi_{p}$ and $\phi_{n}$, as well as for the built-in equilibrium potential $\phi_{0}$, defined as
$$
\phi_{0}=\phi_{n}-\phi_{p}
$$
This potential acts as a barrier preventing holes and electrons from diffusing further, and is the result of the charge redistribution taking place automatically at either side of the metallurgical junction when we create it. Solving for $E(x)$ in Eq. (1.31) and using Einstein's relations of Eq. (1.28) gives
$$
E(x) d x=V_{T} \frac{d p(x)}{p(x)}=-V_{T} \frac{d n(x)}{n(x)}
$$
Using again $\phi(x)=-\int E(x) d x$ and integrating from $-x_{p 0}$ to $+x_{n 0}$ gives
$$
\int_{\phi_{p}}^{\phi_{n}} d \phi(x)=-V_{T} \int_{p_{p 0}}^{p_{n 0}} \frac{d p(x)}{p(x)}=V_{T} \int_{n_{n 0}}^{n_{n 0}} \frac{d n(x)}{n(x)}
$$
where the integration limits are, respectively, the values of $\phi, p$, and $n$ at $x=-x_{p 0}$ and $x=+x_{n 0}$. This gives
$$
\begin{equation*}
\phi_{0}=\phi_{n}-\phi_{p}=V_{T} \ln \frac{p_{p 0}}{p_{n 0}}=V_{T} \ln \frac{n_{n 0}}{n_{p 0}} \tag{1.35}
\end{equation*}
$$
Using Eq. (1.10), we can also write
$$
\begin{gather*}
\phi_{0}=V_{T} \ln \frac{N_{A} N_{D}}{n_{i}^{2}}  \tag{1.36a}\\
\phi_{n}=V_{T} \ln \frac{N_{D}}{n_{i}}  \tag{1.36b}\\
\phi_{p}=V_{T} \ln \frac{n_{i}}{N_{A}} \tag{1.36c}
\end{gather*}
$$
Note that since in practical junctions $N_{A}$ and $N_{D}$ are greater than $n_{i}$, we have $\phi_{n}>0$ and $\phi_{p}<0$. Moreover, since $N_{A}$ and $N_{D}$ appear in the argument of the logarithmic function, the $\phi \mathrm{s}$ of Eq. (1.36) are not that sensitive to variations in the doping doses.
(a) Find the room-temperature values of $\phi_{n}, \phi_{p}$, and $\phi_{0}$ for a junction with the
EXAMPLE 1.6 dopings of Eq. (1.29).
(b) Find $\phi_{0}$ if both doping doses are increased by an order of magnitude.
#### Solution
(a) We have $\phi_{n}=(26 \mathrm{mV}) \ln \left[10^{16} /\left(1.4 \times 10^{10}\right)\right]=0.350 \mathrm{~V}, \phi_{p}=-0.470 \mathrm{~V}$, and $\phi_{0}=0.350-(-0.470)=0.820 \mathrm{~V}$.
(b) Now $\phi_{0}=0.940 \mathrm{~V}$, not much of a change because of the logarithmic dependence. It pays to think of $\phi_{0}$ as being close to 1 V , regardless of the particular doping values.
### The Electric Field $E_{m 0}$, the SCL Width $X_{d 0}$, and the SCL Charge $\boldsymbol{Q}_{j 0}$
We now wish to derive an expression for all other pertinent junction parameters in equilibrium. The maximum field strength $E_{m 0}$ is found once again via $\int d \phi(x)=-\int E(x) d x$, where we integrate from $-x_{p 0}$ to $x_{n 0}$. The left-hand side integrates simply to $\phi_{0}$, while the right-hand side represents the negative of the area of the electric-field triangle. Consequently, we have
$$
\begin{equation*}
\phi_{0}=\frac{\left(x_{p 0}+x_{n 0}\right) E_{m 0}}{2} \tag{1.37}
\end{equation*}
$$
But, according to Eq. (1.34),
$$
\begin{equation*}
x_{p 0}=\frac{\varepsilon_{s i}}{q N_{A}} E_{m 0} \quad x_{n 0}=\frac{\varepsilon_{s i}}{q N_{D}} E_{m 0} \tag{1.38}
\end{equation*}
$$
Substituting $x_{p 0}$ and $x_{n 0}$ into Eq. (1.37), expressing $\phi_{0}$ via Eq. (1.36a), and solving for $E_{m 0}$, we finally get
$$
\begin{equation*}
E_{m 0}=\sqrt{\frac{2 q \phi_{0}}{\varepsilon_{s i}} \frac{N_{A} N_{D}}{N_{A}+N_{D}}} \tag{1.39}
\end{equation*}
$$
If we insert Eq. (1.39) back into Eq. (1.38), we obtain the equilibrium edges of the SCL as
$$
\begin{equation*}
x_{p 0}=\sqrt{\frac{2 \varepsilon_{s i} \phi_{0}}{q N_{A}} \frac{N_{D}}{N_{A}+N_{D}}} \quad x_{n 0}=\sqrt{\frac{2 \varepsilon_{s i} \phi_{0}}{q N_{D}} \frac{N_{A}}{N_{A}+N_{D}}} \tag{1.40}
\end{equation*}
$$
The sum of the two is aptly called the equilibrium $S C L$ width, $X_{d 0}=x_{p 0}+x_{n 0}$. By Eq. (1.40),
$$
\begin{equation*}
X_{d 0}=\sqrt{\frac{2 \varepsilon_{s i} \phi_{0}}{q}\left(\frac{1}{N_{A}}+\frac{1}{N_{D}}\right)} \tag{1.41}
\end{equation*}
$$
The equilibrium junction charge is $Q_{j 0}=Q^{+}=q N_{D} A x_{n 0}$, where $A$ is the aforementioned junction's cross-sectional area. Using Eq. (1.40),
$$
\begin{equation*}
Q_{j 0}=A \sqrt{2 \varepsilon_{s i} q \phi_{0} \frac{N_{A} N_{D}}{N_{A}+N_{D}}} \tag{1.42}
\end{equation*}
$$
Assuming a cross-sectional area $A=(100 \mu \mathrm{~m}) \times(100 \mu \mathrm{~m})$ for a $p n$ junction with the doping doses of Eq. (1.29), find $E_{m 0}, X_{d 0}, x_{p 0}, x_{n 0}$, and $Q_{j 0}$.
#### Solution
From Example $1.6, \phi_{0}=0.820 \mathrm{~V}$. Also, since in our case $N_{A} \gg N_{D}$, we can approximate $N_{A} N_{D} /\left(N_{A}+N_{D}\right) \cong N_{D}=10^{16} \mathrm{~cm}^{-3}$. Then, Eq. (1.39) gives
$$
E_{m 0} \cong \sqrt{\frac{2 \times 1.602 \times 10^{-19} \times 0.820 \times 10^{16}}{1.04 \times 10^{-12}}}=5.03 \times 10^{4} \mathrm{~V} / \mathrm{cm}
$$
and Eq. (1.41) gives
$$
X_{d 0} \cong \sqrt{\frac{2 \times 1.04 \times 10^{-12} \times 0.820}{1.602 \times 10^{-19}}\left(\frac{1}{10^{16}}\right)}=3.26 \times 10^{-5} \mathrm{~cm}=0.326 \mu \mathrm{~m}
$$
Similarly, Eq. (1.40) gives $x_{p 0}=0.003 \mu \mathrm{~m}$ and $x_{n 0}=0.323 \mu \mathrm{~m}$, confirming that the SCL extends almost entirely into the more lightly doped side, which in our example is the $n$ side. Finally, since the junction area is $A=\left(100 \times 10^{-4} \mathrm{~cm}\right)^{2}=$ $10^{-4} \mathrm{~cm}^{2}$, Eq. (1.42) gives $Q_{j 0}=5.23 \mathrm{pC}$.
#### Exercise 1.5
Show that
$$
\begin{equation*}
\phi(0)=\phi_{p}+\frac{N_{D}}{N_{A}+N_{D}} \phi_{0} \tag{1.43}
\end{equation*}
$$
Hence, verify that $\phi(0)=0$ only in the case of symmetrically doped junctions $\left(N_{D}=N_{A}\right)$. Otherwise, $\phi(0)>0$ for $N_{D}>N_{A}$, and $\phi(0)<0$ for $N_{D}<N_{A}$ (as in the case of Fig. 1.39).
## 1.6 EFFECT OF EXTERNAL BIAS ON THE SCL PARAMETERS
Let us now investigate the effect of applying a voltage $v$ across our $p n$ junction in the manner of Fig. 1.40, top. (Note that the polarity convention for $v$ is positive at the $p$ side and negative at the $n$ side; for $v>0$ the $p n$ junction is said to be forward biased, and for $v<0$ it is reverse biased.) By KVL, the potential barrier across the spacecharge layer (SCL) becomes $\phi_{0}-v$. With a changed profile for $\phi$, the electric field strength $E$ will also have to change. Since the field lines making up $E$ come from the uncovered ions of the SCL, the SCL's width $X_{d}=x_{n}+x_{p}$ will have to change accordingly. Specifically, we can state that:
- Forward biasing the junction $(v>0)$ lowers the potential barrier as well as the electric field compared to the unbiased case, and thus shrinks $X_{d}$.
- Conversely, reverse biasing the junction $(v<0)$ raises the potential barrier and the electric field, and thus widens $X_{d}$. For a visual comparison, Fig. 1.40 uses gray lines to show the unbiased situation.
image_name:FIGURE 1.40 Effect of forward-biasing a pn junction
description:The image titled "FIGURE 1.40 Effect of forward-biasing a pn junction" illustrates the changes in a pn junction under forward bias conditions. The diagram is divided into several parts to show different characteristics and behaviors of the junction.
1. **Identification of Components and Structure:**
- The top section shows a simplified representation of a pn junction with p-type and n-type semiconductors. The p-type region is on the left, filled with positive charge carriers (holes), while the n-type region on the right contains negative charge carriers (electrons).
- In the center, there is a depletion region marked, where positive and negative charges are separated, creating an electric field (E) across the junction.
- The forward bias voltage (v) is applied across the junction, indicated by a voltage source symbol on top, which reduces the potential barrier.
2. **Connections and Interactions:**
- The diagram shows the electric field lines (curved arrows) within the depletion region, indicating the direction of the electric field.
- The depletion width is marked as \(X_d\), which is the sum of \(x_p\) (depletion width in the p-region) and \(x_n\) (depletion width in the n-region).
- Below the main junction diagram, three graphs are shown:
- The first graph plots charge density \(\rho\) as a function of position \(x\), showing positive charge \(qN_D\) in the n-region and negative charge \(qN_A\) in the p-region.
- The second graph shows the electric field \(E\) as a function of \(x\), with a peak value \(E_m\) at the junction.
- The third graph illustrates the potential \(\phi\) as a function of \(x\), showing how it changes with the applied forward bias \(v\). The potential decreases from \(\phi_0\) to \(\phi_0 - v\).
3. **Labels, Annotations, and Key Features:**
- Important labels include \(x_p\), \(x_n\), \(X_d\), \(\phi_p\), \(\phi_n\), and \(\phi_0 - v\).
- The graphs are labeled with units: charge density in \(C/cm^3\), electric field in \(V/cm\), and potential in volts (V).
- Gray lines in the potential graph represent the unbiased situation, providing a visual comparison to the forward-biased condition.
Overall, the diagram effectively demonstrates the effect of forward biasing on the pn junction, emphasizing changes in charge distribution, electric field, and potential barrier.
image_name:ρ (C/cm³)
description:The graph titled "ρ (C/cm³)" is a charge density distribution graph for a pn junction diode, illustrating the variation of charge density across the depletion region. The x-axis represents the position across the junction, labeled as \(x\), with units in centimeters \(\text{cm}\). The y-axis represents the charge density \(\rho\), with units in coulombs per cubic centimeter \(\text{C/cm}^3\).
Graph Details:
1. **Type of Graph and Function:**
- This is a piecewise function graph showing the charge density distribution in a pn junction.
2. **Axes Labels and Units:**
- **X-axis:** Position \(x\), units are in centimeters (\(\text{cm}\)).
- **Y-axis:** Charge density \(\rho\), units are in \(\text{C/cm}^3\).
3. **Overall Behavior and Trends:**
- The charge density is zero outside the depletion region, indicating no net charge.
- Within the depletion region, from \(-x_p\) to \(x_n\), the charge density is constant.
- On the p-type side (\(-x_p\) to 0), the charge density is negative, represented by \(-qN_A\), indicating the presence of ionized acceptor atoms.
- On the n-type side (0 to \(x_n\)), the charge density is positive, represented by \(qN_D\), indicating the presence of ionized donor atoms.
4. **Key Features and Technical Details:**
- The depletion width \(X_d = x_n + x_p\) is shown, indicating the extent of the region where charges are present.
- The graph shows a clear demarcation between the n-type and p-type regions at \(x = 0\).
- The constant values of charge density \(-qN_A\) and \(qN_D\) are critical in defining the electric field and potential across the junction.
5. **Annotations and Specific Data Points:**
- \(x = 0\) is marked as the junction interface, separating the p-type and n-type regions.
- The regions \(-x_p\) and \(x_n\) are labeled to indicate the extent of negative and positive charge densities, respectively.
This graph is crucial for understanding the distribution of charge in a pn junction, which directly affects the electric field and potential across the junction, as shown in the subsequent graphs of electric field \(E\) and potential \(\phi\). The behavior of this graph under forward and reverse bias conditions is essential for analyzing diode operation.
image_name:E (V/cm)
description:The graph titled "E (V/cm)" is a plot depicting the electric field across a pn junction under the influence of an external bias voltage \( v \). This is a typical electric field distribution graph for a semiconductor pn junction.
1. **Type of Graph and Function:**
- The graph is a plot of electric field strength \( E \) versus position \( x \) across the depletion region of a pn junction.
- It is a piecewise linear graph representing the electric field distribution.
2. **Axes Labels and Units:**
- The horizontal axis represents the position \( x \) across the junction, with units likely in centimeters (cm).
- The vertical axis represents the electric field strength \( E \), measured in volts per centimeter (V/cm).
3. **Overall Behavior and Trends:**
- The graph shows a V-shaped distribution of the electric field.
- The field is zero outside the depletion region and reaches a maximum negative value \( -E_m \) within the depletion region.
- The electric field is symmetric about the origin, indicating equal and opposite contributions from the p-type and n-type regions.
4. **Key Features and Technical Details:**
- The maximum electric field \( -E_m \) occurs at the junction's center (\( x = 0 \)).
- As the external bias \( v \) is applied, the width of the depletion region \( X_d = x_n + x_p \) is adjusted, affecting the electric field distribution.
- The graph uses gray lines to represent the unbiased case, showing the change in the electric field when a forward bias is applied.
5. **Annotations and Specific Data Points:**
- The plot includes markers for \( -x_p \) and \( x_n \), indicating the boundaries of the depletion region.
- Annotations show the changes in the electric field and potential due to the applied bias, with \( \phi_0 - v \) indicating the modified potential barrier.
- The graph visually compares the biased and unbiased cases, emphasizing the reduction in the electric field and potential barrier with forward bias.
FIGURE 1.40 Effect of forward-biasing a pn junction.
To investigate the effect of the external bias $v$ quantitatively, we simply replace $\phi_{0}$ with $\left(\phi_{0}-v\right)$ in Eqs. (1.39) through (1.42). Thus, rewriting Eq. (1.39) with $E_{m}(v)$ in place of $E_{m 0}$ and $\left(\phi_{0}-v\right)$ in place of $\phi_{0}$, we get the maximum electric-field strength as a function of $v$
$$
E_{m}(v)=\sqrt{\frac{2 q\left(\phi_{0}-v\right)}{\varepsilon_{s i}} \frac{N_{A} N_{D}}{N_{A}+N_{D}}}=\sqrt{\frac{2 q \phi_{0}}{\varepsilon_{s i}} \frac{N_{A} N_{D}}{N_{A}+N_{D}}} \sqrt{1-\frac{v}{\phi_{0}}}
$$
This is expressed more concisely as
$$
\begin{equation*}
E_{m}(v)=E_{m 0} \sqrt{1-\frac{v}{\phi_{0}}} \tag{1.44}
\end{equation*}
$$
image_name:(a)
description:The graph (a) is a plot of the SCL width, denoted as \(X_d\), as a function of voltage \(v\). This is a line plot with the following characteristics:
1. **Type of Graph and Function:**
- The graph is a line plot representing the voltage dependence of the space-charge layer (SCL) width \(X_d\).
- It follows the function \(X_d(v) = X_{d0} \sqrt{1 - \frac{v}{\phi_0}}\), where \(X_{d0}\) is the zero-bias value of \(X_d\).
2. **Axes Labels and Units:**
- The horizontal axis represents voltage \(v\), starting from 0 and extending to \(\phi_0\).
- The vertical axis represents the SCL width \(X_d\), with a marked zero-bias point \(X_{d0}\).
3. **Overall Behavior and Trends:**
- The graph shows a decreasing trend as \(v\) increases from 0 to \(\phi_0\).
- The curve starts at \(X_{d0}\) when \(v = 0\) and decreases towards zero as \(v\) approaches \(\phi_0\).
- The shape of the curve is concave, reflecting the square root dependence on \(1 - \frac{v}{\phi_0}\).
4. **Key Features and Technical Details:**
- At \(v = 0\), the width is at its maximum value \(X_{d0}\).
- As \(v\) approaches \(\phi_0\), \(X_d\) approaches zero, indicating the depletion of the space-charge layer.
- The curve never actually reaches zero, as it is asymptotic to the \(v = \phi_0\) line.
5. **Annotations and Specific Data Points:**
- The graph is annotated with \(X_{d0}\) at \(v = 0\) and \(\phi_0\) on the \(v\)-axis.
- No additional specific numerical data points are provided on the graph itself.
image_name:(b)
description:The graph labeled (b) is a plot of junction capacitance, denoted as \( C_j \), as a function of voltage \( v \). The vertical axis represents the junction capacitance \( C_j \), while the horizontal axis represents the voltage \( v \). Both axes appear to be scaled linearly.
The graph shows an increasing trend in capacitance as the voltage approaches \( \phi_0 \) from the left. At \( v = 0 \), the capacitance is at its zero-bias value, \( C_{j0} \). As the voltage \( v \) increases towards \( \phi_0 \), the capacitance \( C_j \) increases sharply, suggesting a form of exponential or hyperbolic growth as it approaches the threshold voltage \( \phi_0 \).
Key features of the graph include:
- The zero-bias capacitance \( C_{j0} \) at \( v = 0 \).
- A marked increase in \( C_j \) as \( v \) approaches \( \phi_0 \), with the curve becoming steeper near \( \phi_0 \), indicating a nonlinear relationship.
- The graph does not extend beyond \( \phi_0 \), suggesting that this is a critical point for the behavior being analyzed.
Overall, the graph illustrates how the junction capacitance increases with voltage, particularly as it nears a critical voltage \( \phi_0 \).
FIGURE 1.41 Voltage dependence of the (a) SCL width and (b) junction capacitance for $m=1 / 2$.
where $E_{m 0}$, aptly called the zero-bias $(v=0)$ value of $E_{m}$, was derived in Eq. (1.39). Proceeding in similar manner for the SCL's width, we find
$$
\begin{equation*}
X_{d}(v)=X_{d 0} \sqrt{1-\frac{v}{\phi_{0}}} \tag{1.45}
\end{equation*}
$$
where $X_{d 0}$ is the zero-bias $(v=0)$ value of $X_{d}$, which was derived in Eq. (1.41). The voltage dependence of $X_{d}$ is depicted in Fig. 1.41a. Finally, the junction charge is
$$
\begin{equation*}
Q_{j}(v)=Q_{j 0} \sqrt{1-\frac{v}{\phi_{0}}} \tag{1.46}
\end{equation*}
$$
where $Q_{j 0}$ is the zero-bias $(v=0)$ value of $Q_{j}$ as given in Eq. (1.42).
### The Junction Capacitance $\boldsymbol{C}_{\boldsymbol{j}}$
Since applying a voltage across a pn junction redistributes its SCL charge, the junction exhibits capacitive behavior. The junction capacitance is $C_{j}=d Q_{j} / d v$. Differentiating Eq. (1.46) and rearranging,
$$
\begin{equation*}
C_{j}(v)=\frac{C_{j 0}}{\left(1-v / \phi_{0}\right)^{m}} \tag{1.47a}
\end{equation*}
$$
where
$$
\begin{equation*}
C_{j 0}=A \sqrt{\frac{\varepsilon_{s i} q}{2 \phi_{0}} \frac{N_{A} N_{D}}{N_{A}+N_{D}}} \tag{1.47b}
\end{equation*}
$$
is the zero-bias $(v=0)$ value of $C_{j}$ and $m$, called the grading coefficient, is $1 / 2$ in the present case, which assumes an abrupt junction. Practical junctions often have a graded doping profile, in which case it can be shown ${ }^{2}$ that a more appropriate value is $m=1 / 3$. The actual value of $m$ can be found experimentally by measuring $C_{j}$ for different values of $v$ and then using data-interpolation to indirectly find $m$. The voltage dependence of $C_{j}$ is depicted in Fig. 1.41b.
image_name:(a)
description:The image consists of two diagrams labeled (a) and (b), each representing different views of a semiconductor junction and its equivalent model.
1. **Identification of Components and Structure:**
- **Diagram (a):** This part of the image illustrates a semiconductor junction composed of two regions: a p-type and an n-type semiconductor. These regions are shown as blocks joined together, with the depletion region marked between them. The area of the junction is labeled as \( A \), and the width of the depletion region is marked as \( X_d \).
- **Diagram (b):** This diagram represents the parallel-plate capacitor equivalent of the semiconductor junction. It shows two plates separated by a dielectric material with permittivity \( \varepsilon_{si} \). The area \( A \) and the separation \( X_d \) are also marked here, indicating the dimensions of the equivalent capacitor.
2. **Connections and Interactions:**
- Both diagrams show a voltage source \( v \) connected across the junction, indicating the application of a reverse bias. This connection is depicted as a loop, suggesting the flow of voltage across the junction.
- In the parallel-plate model, the voltage source is similarly connected across the plates, representing how the junction capacitance \( C_j \) behaves like a capacitor under the influence of an applied voltage.
3. **Labels, Annotations, and Key Features:**
- **Voltage Source (\( v \)):** Indicates the applied reverse bias voltage across the junction.
- **Area (\( A \)):** Represents the cross-sectional area of the junction and its equivalent parallel-plate capacitor.
- **Depletion Width (\( X_d \)):** The thickness of the depletion region in the junction and the separation between the plates in the capacitor model.
- **Permittivity (\( \varepsilon_{si} \)):** In diagram (b), this denotes the permittivity of the dielectric material between the plates, equivalent to the semiconductor material's permittivity in the junction.
Overall, the image provides a visual representation of the semiconductor junction and its equivalent capacitor model, highlighting the relationship between the physical structure of the junction and its electrical properties.
image_name:(b)
description:The image labeled as Figure 1.42 (b) illustrates the equivalent parallel-plate capacitor model of a junction capacitance $C_j$. This model is used to simplify the understanding of how a semiconductor junction behaves electrically.
1. Identification of Components and Structure:
- **Parallel-Plate Capacitor Representation:** The diagram shows a simplified structure of a parallel-plate capacitor, which consists of two conductive plates separated by a dielectric material.
- **Plates:** The plates are represented by the two shaded areas on either side of the dielectric material.
- **Dielectric Material:** The central region between the plates is labeled with $\varepsilon_{si}$, indicating the permittivity of silicon, which acts as the dielectric material.
- **Area (A):** The area of the plates is labeled as $A$.
2. Connections and Interactions:
- **Voltage Source (v):** A voltage source is connected across the plates, indicated by a circle with a plus and minus sign, representing the potential difference applied across the junction.
- **Separation Distance ($X_d$):** The distance between the plates is labeled as $X_d$, which represents the depletion width of the junction.
- **Flow of Electric Field:** The applied voltage creates an electric field across the dielectric, affecting the capacitance of the junction.
3. Labels, Annotations, and Key Features:
- **$\varepsilon_{si}$:** This label indicates the permittivity of the silicon, which is crucial in determining the capacitance value.
- **$A$ and $X_d$:** These labels denote the area of the plates and the separation distance, respectively, which are key parameters in the parallel-plate capacitor formula $C = \varepsilon_{si} \frac{A}{X_d}$.
This representation helps in understanding the junction capacitance by drawing an analogy to a more familiar parallel-plate capacitor, emphasizing the dependency of capacitance on the area, permittivity, and separation distance.
FIGURE 1.42 (a) The junction capacitance $C_{j}$, and $(b)$ its parallel-plate equivalent.
Combining Eqs. (1.41), (1.45), and (1.47) with $m=1 / 2$, we put $C_{J}$ in yet another insightful form
$$
\begin{equation*}
C_{j}(v)=\varepsilon_{s i} \frac{A}{X_{d}(v)} \tag{1.48}
\end{equation*}
$$
This is the same form as that of a parallel-plate capacitor consisting of two plates of area $A$ separated by a dielectric material having permittivity $\varepsilon_{s i}$ and thickness $X_{d}$. This equivalence is illustrated in Fig. 1.42. However, unlike a fixed capacitor, the present one exhibits a voltage-dependent plate separation $X_{d}(v)$, indicating nonlinear capacitance behavior, as already seen in Fig. 1.41b. We also observe that Eq. (1.47a) predicts $C_{j} \rightarrow \infty$ for $v \rightarrow \phi_{0}$. This, of course, cannot happen in practice, indicating that Eq. $(1.47 a)$, whose derivation is based on a number of simplifying assumptions, no longer holds as $v$ approaches $\phi_{0}$.
EXAMPLE 1.8 Find $C_{j 0}$ for the junction of Example 1.7. Then, assuming $m=1 / 2$, calculate $E_{m}, X_{d}$, $Q_{j}$, and $C_{j}$ for $(a) v=+0.65 \mathrm{~V}$, and $(b) v=-5 \mathrm{~V}$.
#### Solution
(a) Using Eq. (1.47b) we readily find $C_{j 0}=3.19 \mathrm{pF}$. Moreover
$$
\sqrt{1-v / \phi_{0}}=\sqrt{1-0.65 / 0.82}=0.455
$$
indicating a decrease in $E_{m}, X_{d}$, and $Q_{j}$, but an increase in $C_{j}$. Indeed, at $v=+0.65 \mathrm{~V}$ we have $E_{m}=5.03 \times 10^{4} \times 0.455=2.29 \times 10^{4} \mathrm{~V} / \mathrm{cm}$, $X_{d}=0.148 \mu \mathrm{~m}, Q_{j}=2.38 \mathrm{pC}$, and $C_{j}=3.19 / 0.455=7.01 \mathrm{pF}$.
(b) Now $E_{m}, X_{d}$, and $Q_{j}$ will increase but $C_{j}$ will decrease by $\sqrt{1-(-5) / 0.82}=$ 2.66, so $E_{m}=13.4 \times 10^{4} \mathrm{~V} / \mathrm{cm}, X_{d}=0.869 \mu \mathrm{~m}, Q_{j}=13.9 \mathrm{pC}$, and $C_{j}=1.20 \mathrm{pF}$.
Remark: It pays to keep in mind the following orders of magnitude for low-power junctions:
$$
\phi_{0} \sim 1 \mathrm{~V} \quad E_{m} \sim 10^{4} \mathrm{~V} / \mathrm{cm} \quad X_{d} \sim 1 \mu \mathrm{~m} \quad Q_{j} \sim 1 \mathrm{pC} \quad C_{j} \sim 1 \mathrm{pF}
$$
## 1.7 THE pn DIODE EQUATION
Forward-biasing a pn junction affects not only the parameters of its space-charge layer (SCL), but also the concentration profiles of its charge carriers in the neutral regions, and quite dramatically so, as we are about to see. The starting point is offered by Eq. (1.35), which we turn around by taking the logarithms throughout and solving for the minority concentrations,
$$
\begin{align*}
& p_{n 0}=p_{p 0} e^{-\phi_{0} / V_{T}}  \tag{1.49a}\\
& n_{p 0}=n_{n 0} e^{-\phi_{0} / V_{T}} \tag{1.49b}
\end{align*}
$$
These equations relate the hole and the electron concentrations at either side of the SCL for the unbiased $(v=0)$ equilibrium situation. If we now forward bias the junction $(v>0), E$ will decrease and thus allow holes to diffuse from the $p$ side, through the SCL, to the $n$ side, and electrons from the $n$ to the $p$ side. We can still use Eq. (1.49) to relate the concentrations right at the edges of the SCL, also called boundary concentrations, provided we replace $\phi_{0}$ with $\phi_{0}-v$. The result is
$$
\begin{align*}
& p_{n}\left(x_{n}\right)=p_{p}\left(-x_{p}\right) e^{-\left(\phi_{0}-v\right) / V_{T}}  \tag{1.50a}\\
& n_{p}\left(-x_{p}\right)=n_{n}\left(x_{n}\right) e^{-\left(\phi_{0}-v\right) / V_{T}} \tag{1.50b}
\end{align*}
$$
The so-called low-level injection assumption stipulates that even after biasing, the minority concentrations at either side of the SCL continue to remain much lower than the majority concentrations there, and thus leave the latter essentially undisturbed compared to the unbiased case. This means that we can let $p_{p}\left(-x_{p}\right)=p_{p 0}$ and $n_{n}\left(x_{n}\right)=$ $n_{n 0}$ in Eq. (1.50). Reusing Eq. (1.49), we can then write
$$
\begin{gather*}
p_{n}\left(x_{n}\right)=p_{n 0} e^{v / V_{T}}  \tag{1.51a}\\
n_{p}\left(-x_{p}\right)=n_{p 0} e^{v / V_{T}} \tag{1.51b}
\end{gather*}
$$
Referred to as the law of the junction, Eq. (1.51) relates the boundary values of the minority concentrations to the applied voltage $v$. Though the derivations were made for the forward-bias case $(v>0)$, this law holds also for the reverse-bias case $(v<0)$.
Assuming the doping doses of Eq. (1.29), find the minority and majority concentrations at either edge of the SCL if the junction is forward biased with $v=0.65 \mathrm{~V}$. Comment on your results.
#### Solution
By Eq. (1.30), $p_{p}\left(-x_{p}\right)=p_{p 0} \cong 10^{18} / \mathrm{cm}^{3}$ and $n_{n}\left(x_{n}\right) \cong n_{n 0} \cong 10^{16} / \mathrm{cm}^{3}$. Moreover, $n_{p 0} \cong 2 \times 10^{2} / \mathrm{cm}^{3}$, and $p_{n 0} \cong 2 \times 10^{4} / \mathrm{cm}^{3}$. Since $\exp (0.650 / 0.026) \cong 7.2 \times 10^{10}$, Eq. (1.51) gives
$$
\begin{aligned}
& p_{n}\left(x_{n}\right) \cong 2 \times 10^{4} \times 7.2 \times 10^{10}=1.44 \times 10^{15} / \mathrm{cm}^{3} \\
& n_{p}\left(-x_{p}\right) \cong 2 \times 10^{2} \times 7.2 \times 10^{10}=1.44 \times 10^{13} / \mathrm{cm}^{3}
\end{aligned}
$$
image_name:FIGURE 1.43
description:The graph in FIGURE 1.43 illustrates the behavior of a pn junction under forward bias, specifically at 0.65 V. It consists of three main plots stacked vertically, each representing different physical quantities across the pn junction.
1. **First Plot (Top):**
- **Type of Graph:** Concentration profile.
- **Axes Labels and Units:**
- **X-axis:** Distance \( x \) across the junction, ranging from \(-W_p\) to \(W_n\).
- **Y-axis:** Carrier concentration \( n, p \) in \( \text{cm}^{-3} \).
- **Overall Behavior and Trends:**
- The graph shows the concentration of minority carriers in the neutral regions of the pn junction.
- On the p-type side, the minority carrier concentration \( n_p(x) \) increases exponentially from \( n_{p0} = 2 \times 10^2 \text{ cm}^{-3} \) to \( n_p(-x_p) = 1.44 \times 10^{13} \text{ cm}^{-3} \).
- On the n-type side, the minority carrier concentration \( p_n(x) \) decreases exponentially from \( p_n(x_n) = 1.44 \times 10^{15} \text{ cm}^{-3} \) back to \( p_{n0} = 2 \times 10^4 \text{ cm}^{-3} \).
- **Key Features:**
- The curves illustrate the diffusion of minority carriers away from the space charge region.
- The concentrations are significantly higher near the junction, indicating a high recombination rate.
2. **Second Plot (Middle):**
- **Type of Graph:** Excess carrier concentration profile.
- **Axes Labels and Units:**
- **X-axis:** Distance \( x \).
- **Y-axis:** Excess carrier concentration \( n', p' \) in \( \text{cm}^{-3} \).
- **Overall Behavior and Trends:**
- Similar exponential trends as the first plot but focusing on excess carriers.
- Excess electrons \( n'_p(x) \) and holes \( p'_n(x) \) peak near the junction and decrease exponentially.
- **Key Features:**
- Shows how forward bias increases the excess minority carriers significantly.
3. **Third Plot (Bottom):**
- **Type of Graph:** Current density profile.
- **Axes Labels and Units:**
- **X-axis:** Distance \( x \).
- **Y-axis:** Current density \( J_n, J_p \) in \( \text{A/cm}^2 \).
- **Overall Behavior and Trends:**
- The current densities \( J_n(x) \) and \( J_p(x) \) are shown to be constant across the neutral regions.
- The plot indicates that the diffusion currents are equal and opposite, maintaining a balance in the junction.
- **Key Features:**
- The current density remains constant, reflecting the steady-state condition under forward bias.
**Annotations and Specific Data Points:**
- The plots are annotated with critical points such as \( n_p(-x_p) \) and \( p_n(x_n) \), showing numerical values for key concentrations.
- The regions \( L_n \) and \( L_p \) indicate the diffusion lengths for electrons and holes, respectively.
- The diagram also includes the physical layout of the pn junction with the applied forward bias voltage of 0.65 V, illustrating the movement of charge carriers across the junction.
FIGURE 1.43 Forward biasing a pn junction creates an excess of minority charges in the neutral regions. These charges diffuse away from the SCL, giving raise to diffusion currents.
These boundary values are shown numerically in Fig. 1.43. We observe that a forward bias of only 0.65 V causes $p_{n}\left(x_{n}\right)$ to shoot up from $2 \times 10^{4} / \mathrm{cm}^{3}$ to $1.44 \times 10^{15} / \mathrm{cm}^{3}$ ! However, this is still less than the majority concentration there $\left(10^{16} / \mathrm{cm}^{3}\right)$, thus confirming low-level injection. Likewise, $n_{p}\left(-x_{p}\right)$ has jumped from $2 \times 10^{2} / \mathrm{cm}^{3}$ to $1.44 \times 10^{13} / \mathrm{cm}^{3}$. This too is quite a number, yet it is much less than the majority concentration there $\left(10^{18} / \mathrm{cm}^{3}\right)$, again indicating low-level injection.
#### Excess Minority Concentrations
It is apparent that forward biasing the $p n$ junction establishes an excess of minority carriers at both edges of the SCL. The excess concentrations are $p_{n}^{\prime}\left(x_{n}\right)=p_{n}\left(x_{n}\right)-p_{n 0}$ at the right edge, and $n_{p}^{\prime}\left(-x_{p}\right)=n_{p}\left(-x_{p}\right)-n_{p 0}$ at the left edge. By Eq. (1.51), these excesses can be expressed as
$$
\begin{gather*}
p_{n}^{\prime}\left(x_{n}\right)=p_{n 0}\left(e^{v / V_{T}}-1\right)  \tag{1.52a}\\
n_{p}^{\prime}\left(-x_{p}\right)=n_{p 0}\left(e^{v / V_{T}}-1\right) \tag{1.52b}
\end{gather*}
$$
Once minority excesses have been established, the carriers will diffuse away from the SCL toward regions of lower excess concentrations (holes from $x_{n}$ toward the right, electrons from $-x_{p}$ toward the left). In both cases, their diffusion takes place in a sea of oppositely-charged majority carriers, indicating a high chance of recombination. In fact, the further away we go from the SCL's edges, the less and less excess minority carriers we are likely to find.
This diffuse-and-recombine process is governed by the diffusion equation, which for excess holes takes on the form ${ }^{2}$
$$
D_{p} \frac{d^{2} p_{n}^{\prime}(x)}{d x^{2}}=\frac{p_{n}^{\prime}(x)}{\tau_{p}}
$$
where $\tau_{p}$ is the mean recombination time, also called the mean lifetime of the excess holes. A similar equation holds for excess electrons, but with $\tau_{n}$ as the mean recombination time. The solution to the diffusion equation is an exponential decay with $x$ for holes, and with $-x$ for electrons, in the manner illustrated in Fig. 1.43, middle. Mathematically, the decay for holes is expressed as
$$
\begin{equation*}
p_{n}^{\prime}(x)=p_{n 0}\left(e^{v / V_{T}}-1\right) e^{-\left(x-x_{n}\right) / L_{p}} \tag{1.53}
\end{equation*}
$$
where the quantity
$$
\begin{equation*}
L_{p}=\sqrt{D_{p} \tau_{p}} \tag{1.54a}
\end{equation*}
$$
is called the hole diffusion length, in cm . It represents the distance from $x_{n}$ at which $p_{n}^{\prime}(x)$ drops to $1 / e(36.8 \%)$ of its boundary value $p_{n}^{\prime}\left(x_{n}\right)$. A similar expression holds for excess electrons in the $p$ side, but with the electron diffusion length
$$
\begin{equation*}
L_{n}=\sqrt{D_{n} \tau_{n}} \tag{1.54b}
\end{equation*}
$$
The lengths $L_{p}$ and $L_{n}$ are typically on the order of $10^{1} \mu \mathrm{~m}$, so we generally have $L_{p} \gg x_{n}$ and $L_{n} \gg x_{p}$.
Note that $p_{n}^{\prime} \rightarrow 0$ at the right end of the $n$-type slab $\left(x=W_{n}\right)$, as the excess holes undergo total recombination with the electrons of the metal electrode there. Likewise, $n_{p}^{\prime} \rightarrow 0$ at the left end of the $p$-type slab $\left(x=-W_{p}\right)$, as excess electrons undergo total removal by the metal electrode there.
By Eq. (1.27a) the diffusion of excess holes toward the right results in the current density $J_{p}(x)=-q D_{p} d p_{n}^{\prime}(x) / d x$. Differentiating Eq. (1.53) and substituting gives
$$
\begin{equation*}
J_{p}(x)=q D_{p} \frac{p_{n 0}}{L_{p}}\left(e^{v / V_{T}}-1\right) e^{-\left(x-x_{n}\right) / L_{p}} \tag{1.55a}
\end{equation*}
$$
A similar expression holds for the current density due to excess electrons diffusing toward the left, except that we need to replace $x$ with $-x$ in the exponent,
$$
\begin{equation*}
J_{n}(x)=q D_{n} \frac{n_{p 0}}{L_{n}}\left(e^{v / V_{T}}-1\right) e^{\left(x+x_{p}\right) / L_{n}} \tag{1.55b}
\end{equation*}
$$
We expect recombination within the (thin) depletion region to be negligible, so $J_{p}$ and $J_{n}$ will essentially be constant there. With reference to Fig. 1.43, bottom, we find the total current density within the SCL as $J_{\text {tot }}=J_{p}\left(x_{n}\right)+J_{n}\left(-x_{p}\right)$. Using Eq. (1.55), we readily get
$$
\begin{equation*}
J_{\text {tot }}=q\left(\frac{D_{p} p_{n 0}}{L_{p}}+\frac{D_{n} n_{p 0}}{L_{n}}\right)\left(e^{v / V_{T}}-1\right) \tag{1.56}
\end{equation*}
$$
Note that Fig. 1.43, bottom, shows only the minority diffusion currents. For a complete picture of conduction we need to show also the majority diffusion currents. Owing to the charge conservation principle, $J_{\text {tot }}$ must be constant throughout the slab. We can thus obtain each majority current component by taking the graphical difference between the total current and the corresponding minority current component, or $J_{p}=J_{\text {tot }}-J_{n}$ to the left of $-x_{p}$, and $J_{n}=J_{\text {tot }}-J_{p}$ to the right of $x_{n}$. The result, shown in Fig. 1.44, shows how fascinating conduction is inside a pn slab.
image_name:FIGURE 1.44 Minority and majority current densities inside a pn slab.
description:The graph depicted in Figure 1.44 illustrates the minority and majority current densities inside a pn slab. This is a current density graph where the x-axis represents the position across the slab, denoted by \( x \), with units not specified but typically in micrometers or centimeters in semiconductor contexts. The y-axis represents current density \( J \) in amperes per square centimeter (A/cm²).
Type of Graph and Function
This is a spatial distribution graph showing the behavior of current densities across a pn junction. It is a linear graph depicting how current densities vary as a function of position across the slab.
Axes Labels and Units
- **X-axis**: Position \( x \) across the slab, with critical points labeled as \(-x_p\) and \(x_n\).
- **Y-axis**: Current density \( J \) in A/cm².
Overall Behavior and Trends
- **Total Current Density \( J_{tot} \)**: This is a constant horizontal line across the slab, indicating that the total current density remains constant due to charge conservation.
- **Majority Carrier Current Density \( J_p \) and \( J_n \)**: These curves show the variation of hole and electron current densities, respectively.
- \( J_p \): Starts high at \(-x_p\), decreasing towards zero as it approaches \( x_n \).
- \( J_n \): Starts at zero at \(-x_p\) and increases towards \( x_n \).
- **Minority Carrier Current Density \( J_n(x) \) and \( J_p(x) \)**: These curves represent minority carriers and show symmetrical behavior to their majority counterparts but with opposite trends.
Key Features and Technical Details
- **Symmetry**: The graph is symmetrical around the center of the slab at \( x = 0 \).
- **Intersection at Zero**: The minority and majority currents intersect at the origin, indicating zero net current at the depletion region boundary.
- **Critical Points**: \(-x_p\) and \(x_n\) mark the boundaries of the depletion region where the behavior of the currents changes.
Annotations and Specific Data Points
- **Reference Lines**: The total current density \( J_{tot} \) is marked as a constant line.
- **Markers**: \( J_p \) and \( J_n \) are labeled to show their respective regions of dominance.
This graph effectively demonstrates the interplay between majority and minority carriers in a pn junction, with the total current remaining constant while individual carrier currents vary spatially across the slab.
FIGURE 1.44 Minority and majority current densities inside a pn slab.
If we were to scan the slab from left to right, our description of conduction would be as follows
- At the far left we see a current of mainly holes diffusing toward the right on their way to recombine with electrons. Some of these holes disappear by recombination in the $p$ side itself, others manage to make it all the way to the SCL, from where they emerge as minority carriers in the $n$ side. As they progress toward the right, they are further annihilated by electrons.
- Moving closer to the SCL while still on the $p$ side, we note that $J_{p}$ has subsided somewhat, but at the expense of an increase in $J_{n}$, so as to ensure the constancy of $J_{\text {tor }}$. The fact that close to the SCL, $J_{p}$ has subsided doesn't necessarily imply a reduction in hole concentration there. In fact, Example 1.9 has revealed that at $x=-x_{p}$ there are $10^{18}$ holes $/ \mathrm{cm}^{3}$ pressing against the SCL, quite a number compared to the $1.44 \times 10^{13}$ electrons/cm ${ }^{3}$ available there. Out of these $10^{18} \mathrm{holes} /$ $\mathrm{cm}^{3}$, only $1.44 \times 10^{15}$ holes $/ \mathrm{cm}^{3}$ manage to emerge from the SCL, at the right.
- Moving now inside the SCL, we see a two-way traffic of holes and electrons, hardly recombining with each other because $X_{d}$ is much shorter than the diffusion lengths $L_{p}$ and $L_{n}$. Because of asymmetric doping as well as differences in the hole and electron diffusivities and diffusion lengths, $J_{p}$ and $J_{n}$ are generally different inside the SCL.
- As we move past the SCL into the $n$ region, we note that excess holes fade away, annihilated by the majority of electrons present there. We instead observe a progressively larger current of electrons moving toward the left, on their way either to annihilate holes while still in the $n$ side, or to be annihilated by holes once they cross the SCL to emerge in the $p$ side.
### The Diode Equation
The overall current $i$ through a $p n$ junction of cross-sectional area $A$ is readily found as $i=A J_{\text {tot }}$. Using Eqs. (1.56), along with Eq. (1.30), we get what is commonly referred to as the diode equation
$$
\begin{equation*}
i=I_{s}\left(e^{v / V_{T}}-1\right) \tag{1.57}
\end{equation*}
$$
where $I_{s}$ is a scaling factor called the saturation current,
$$
\begin{equation*}
I_{s}=A \times n_{i}^{2}(T) \times q\left(\frac{D_{p}}{L_{p} N_{D}}+\frac{D_{n}}{L_{n} N_{A}}\right) \tag{1.58}
\end{equation*}
$$
This factor gives an indication of how much current $i$ we get for a given applied voltage $v$. For low-power junctions, $I_{s}$ is typically on the order of femto-amperes ( $1 \mathrm{fA}=$ $10^{-15} \mathrm{~A}$ ). We observe that $I_{s}$ depends on:
- The cross-sectional area $A$ (the larger $A$, the higher the current-just as with ordinary resistors)
- Temperature $T$, especially via $n_{i}^{2}(T)$
- The doping densities $N_{A}$ and $N_{D}$, the diffusivities $D_{p}$ and $D_{n}$, and the diffusion lengths $L_{p}$ and $L_{n}$.
As we proceed we shall find that most practical junctions are fabricated with one side much more heavily doped than the other. When this is the case, one of the terms within parentheses in Eq. (1.58) becomes negligible, and $I_{s}$ is determined primarily by the term with the smaller doping concentration in its denominator. In our working $p n$ junction example, for which $N_{A} \gg N_{D}$, the dominant term in Eq. (1.58) is the first one, stemming from the injection of holes into the more lightly doped $n$-side. As we know, this is also the side into which most of the SCL extends. For obvious reasons, asymmetrically-doped junctions are also referred to as one-sided junctions. An example will better illustrate.
(a) Estimate $i$ if the $p n$ junction of Example 1.7 is biased at $v=0.65 \mathrm{~V}$. Assume $D_{p}=10 \mathrm{~cm}^{2} / \mathrm{s}, L_{p}=5 \mu \mathrm{~m}, D_{n}=7 \mathrm{~cm}^{2} / \mathrm{s}$, and $L_{n}=10 \mu \mathrm{~m}$. Comment on your results.
(b) Find the area $A$ needed for the junction of part (a) to give $i=0.15 \mathrm{~mA}$ at $v=0.65 \mathrm{~V}$.
#### Solution
(a) Inserting the given data into Eq. (1.58) gives
$$
\begin{aligned}
I_{s} & =10^{-4} \times 2 \times 10^{20} \times 1.602 \times 10^{-19}\left(\frac{10}{5 \times 10^{-4} \times 10^{16}}+\frac{7}{10 \times 10^{-4} \times 10^{18}}\right) \\
& =6.41+0.02=6.43 \mathrm{fA}
\end{aligned}
$$
As expected of a one-sided junction such as the present one, $I_{s}$ is determined primarily by one term, namely, the first term, representing hole injection. Electron injection into the heavily-doped $p$-side has little say in this case. Finally, we use Eq. (1.57) to find
$$
i=6.43 \times 10^{-15}\left(e^{650 / 26}-1\right)=463 \mu \mathrm{~A}
$$
(b) To lower $i$ from 0.463 mA to 0.15 mA , we need to lower $A$ in proportion, that is, from $10^{-4} \mathrm{~cm}^{2}$ to $(0.15 / 0.463) \times 10^{-4} \mathrm{~cm}^{2}$, or to $0.324 \times 10^{-4} \mathrm{~cm}^{2}$. This requires a square area of about $(57 \mu \mathrm{~m}) \times(57 \mu \mathrm{~m})$.
### Short-Base Diodes
In the diode example of Fig. 1.43 the neutral regions are long enough to provide sufficient distance for the minority charges to recombine with the majority charges as they diffuse away from the SCL. Aptly called a long-base diode, this structure occurs when the device is fabricated with dimensions $W_{n} \gg L_{p}$ and $W_{p} \gg L_{n}$. As we progress, we shall see that $p n$ diodes are also fabricated with $W_{n} \ll L_{p}$, or $W_{p} \ll L_{n}$, or both. A popular example is the base-emitter junction of a bipolar junction transistor, this being the reason why such a structure is referred to as a short-base diode.
With $W_{n} \ll L_{p}$, the holes injected into the $n$-side don't have much of a chance to recombine while diffusing toward the right, indicating that $J_{p}$ will essentially be
image_name:FIGURE 1.45 Minority carrier concentrations in a forward-biased short-base diode
description:The graph in Figure 1.45 depicts the minority carrier concentrations in a forward-biased short-base diode. This diode is characterized by the conditions \( W_n \ll L_p \) and \( W_p \ll L_n \). The graph is a spatial representation of carrier concentration across the \( p \)-type and \( n \)-type regions of the diode.
Type of Graph and Function:
This is a spatial concentration profile graph, showing how minority carrier concentrations vary along the diode structure when it is forward-biased.
Axes Labels and Units:
- **Horizontal Axis (x):** Represents the position along the diode, with the origin (0) at the junction between \( p \)-type and \( n \)-type regions. The axis extends from \( -W_p \) (in the \( p \)-type region) to \( W_n \) (in the \( n \)-type region).
- **Vertical Axis (n, p in cm\(^{-3}\)):** Represents the minority carrier concentration, with separate profiles for \( n_p(x) \) in the \( p \)-type region and \( p_n(x) \) in the \( n \)-type region.
Overall Behavior and Trends:
- In the \( p \)-type region, the minority carrier concentration \( n_p(x) \) increases linearly from \( n_{p0} \) at \( -W_p \) to a maximum at the junction (\( -x_p \)).
- In the \( n \)-type region, the minority carrier concentration \( p_n(x) \) decreases linearly from a maximum at the junction (\( x_n \)) to \( p_{n0} \) at \( W_n \).
- The linear profiles indicate a constant slope, which is a characteristic of short-base diodes where minority carriers are injected and diffuse without significant recombination.
Key Features and Technical Details:
- **Minority Carrier Concentrations:** \( n_p(x) \) and \( p_n(x) \) are depicted with linear slopes, indicating efficient carrier injection and diffusion.
- **Junction Behavior:** At the junction (0), the concentrations transition smoothly, reflecting the forward-bias condition.
- **Boundary Conditions:** The concentrations \( n_{p0} \) and \( p_{n0} \) at the boundaries \( -W_p \) and \( W_n \) respectively, represent the equilibrium minority carrier concentrations.
Annotations and Specific Data Points:
- The graph includes annotations for \( n_p(-x_p) \) and \( p_n(x_n) \), marking the peak concentrations at the junction edges.
- The linearity and slopes are critical for understanding the behavior of the diode under forward-bias, emphasizing minimal recombination and efficient carrier transport.
FIGURE 1.45 Minority carrier concentrations in a forward-biased short-base diode fabricated with $W_{n} \ll L_{p}$ and $W_{p} \ll L_{n}$.
constant in the $n$-side. By Eq. $(1.27 a)$, this implies, in turn, a constant slope for $p_{n}(x)$, as depicted in Fig. 1.45. If the condition $W_{p} \ll L_{n}$ holds, similar considerations apply to $J_{n}$ and $n_{p}(x)$ in the $p$-side. To find the $i-v$ characteristic of a short-base diode, we start with $J_{p}=-q D_{p} d p_{n}^{\prime}(x) / d x$, where $p_{n}^{\prime}(x)$ is the excess hole density in the $n$-side. The slope of the triangle in Fig. 1.45 is readily found as
$$
\frac{d p_{n}^{\prime}(x)}{d x}=-\frac{p_{n}\left(x_{n}\right)-p_{n 0}}{W_{n}-x_{n}} \cong-\frac{p_{n 0}\left(e^{v / V_{T}}-1\right)}{W_{n}}
$$
where we have exploited the fact that usually $x_{n} \ll W_{n}$. Similar considerations hold for the $p$-side slope $d n_{p}^{\prime}(x) / d x$. Proceeding as in the derivation of Eq. (1.58), we readily find that a short-base diode still obeys Eq. (1.57), but with the following expression for the saturation current,
$$
\begin{equation*}
I_{s} \cong A n_{i}^{2} q\left(\frac{D_{p}}{W_{n} N_{D}}+\frac{D_{n}}{W_{p} N_{A}}\right) \tag{1.59}
\end{equation*}
$$
This is identical to that of Eq. (1.58), except for the replacements $L_{p} \rightarrow W_{n}$ and $L_{p} \rightarrow W_{n}$. Considering that in a short-base diode the $W \mathrm{~s}$ are much smaller than the $L \mathrm{~s}$, it is apparent that this structure requires a smaller cross-sectional area $A$ to achieve the same value of $I_{s}$. Another advantage is that the amount of excess charge stored in a forward-biased short-base diode is much smaller than that of a long-base device operating at the same current. This results in much faster switching times, as we shall see in Chapter 6.
EXAMPLE 1.11 Repeat Example 1.10, but for the case in which the diode has been fabricated with $W_{p}=0.5 \mu \mathrm{~m}$ and $W_{n}=1 \mu \mathrm{~m}$. Compare and comment.
#### Solution
Since we have a one-sided junction with $N_{A} \gg N_{D}$, we expect the first term within parentheses in Eq. (1.59) to dominate, just like its counterpart of Eq. (1.58). Considering that the value of $W_{n}$ given here is five times as small as the value of $L_{p}$ given in Example 1.10, we anticipate a fivefold increase in $I_{s}$, or $I_{s} \cong 6.41 \times 5 \cong$ 33 fA . With the same applied voltage $v$, the current $i$ will also increase fivefold,
$$
i \cong 33 \times 10^{-15} e^{650 / 26} \cong 2.4 \mathrm{~mA}
$$
To lower $i$ from 2.4 mA to 0.15 mA , we need to lower $A$ in proportion, from $10^{-4} \mathrm{~cm}^{2}$ to $(0.15 / 2.4) \times 10^{-4} \mathrm{~cm}^{2}$, or to $0.063 \times 10^{-4} \mathrm{~cm}^{2}$. This can be achieved with a square area of $(25 \mu \mathrm{~m}) \times(25 \mu \mathrm{~m})$.
## 1.8 THE REVERSE-BIASED pn JUNCTION
Reverse biasing a pn junction further increases the existing potential barrier, thus inhibiting hole and electron diffusion across the metallurgical junction. Given this strong preference to conduct in the forward direction, the $p n$ junction exhibits diode behavior, so from now on we shall use the words pn junction and diode interchangeably.
For sufficiently negative values of the applied voltage $v$ (say, for $v<-4 V_{T} \cong-0.1 \mathrm{~V}$ ), Eq. (1.57) predicts that $i$ will saturate at $-I_{s}$ (hence, the name saturation current). As we know, for low-power diodes, $I_{s}$ is typically in the fA range. However, the actual reverse current found in a pn junction, which we shall denote as $I_{R}$, is orders of magnitude higher than $I_{s}$, typically in the pA to nA range. This stems from the thermal generation of holeelectron pairs within the space-charge layer SCL, which we ignored in the course of our analysis. In fact, even though we have been referring to the SCL as the depletion region, thermal generation of hole-electron pairs does continue to take place there, and once generated, holes and electrons are swept in opposite directions by the strong local electric field $E$, resulting in a combined drift current from the $n$ side, through the SCL, to the $p$ side. Intuitively we expect $I_{R}$ to be proportional to the SCL's volume $A X_{d}$, and since $X_{d}$ increases with the amount of reverse bias, as per Eq. (1.45), $I_{R}$ will also increase with the reverse voltage in square-root fashion. Depending on the quality of fabrication, leakage current may also flow across the surface of the pn junction, further contributing to $I_{R}$.
The overall reverse current $I_{R}$ is a strong function of temperature, a behavior that engineers remember via the following important rule of thumb:
The reverse current $I_{R}$ of a pn junction doubles for about every $10^{\circ} \mathrm{C}$ of temperature increase
Once we know $I_{R}$ at some reference temperature $T_{0}$, we can estimate it at any other temperature $T$ using
$$
\begin{equation*}
I_{R}(T) \cong I_{R}\left(T_{0}\right) \times 2^{\left(T-T_{0}\right) / 10} \tag{1.60}
\end{equation*}
$$
If at $25^{\circ} \mathrm{C}$ a certain diode exhibits $I_{R}=1 \mathrm{pA}$, estimate $I_{R}(a)$ at $125{ }^{\circ} \mathrm{C}$, and (b) at $-25^{\circ} \mathrm{C}$.
#### Solution
(a) By Eq. (1.60), $I_{R}\left(125^{\circ} \mathrm{C}\right) \cong 10^{-12} \times 2^{(125-25) / 10} \cong 1 \mathrm{nA}$. (b) Likewise, $I_{R}\left(-25^{\circ} \mathrm{C}\right)$ $\cong 0.03 \mathrm{pA}$.
### Reverse Breakdown
If we gradually increase the reverse bias of a $p n$ junction, a voltage is reached, called the breakdown voltage ( $B V$ ), at which the reverse current shoots up in magnitude from the negligible value $I_{R}$ discussed above to much higher values. The name stems from the fact that the $i-v$ curve bends sharply, or breaks down. This does not necessarily imply a destructive process-in fact, one always limits the reverse current within safety levels by interposing a suitable resistor in series between the driving voltage source and the reverse-biased junction. Figure 1.46 shows the complete $i-v$ characteristic of a typical $p n$ junction.
The breaking down of the $i-v$ curve evidently indicates the sudden availability of huge quantities of mobile charges to produce the much increased current levels. This sudden availability is the result of either of two separate mechanisms: Zener
image_name:Figure 1.46
description:The graph in Figure 1.46 is a current-voltage ($i-v$) characteristic curve of a typical $pn$ junction diode. It is a two-dimensional plot with the voltage ($v$) on the horizontal axis and current ($i$) on the vertical axis.
1. **Type of Graph and Function:**
- This is an $i-v$ characteristic curve, which is commonly used to describe the behavior of semiconductor devices such as diodes.
2. **Axes Labels and Units:**
- The horizontal axis represents the voltage ($v$) applied across the diode, with positive and negative directions.
- The vertical axis represents the current ($i$) flowing through the diode.
- Both axes are likely measured in volts (V) and amperes (A), respectively, although specific units are not indicated.
3. **Overall Behavior and Trends:**
- In the forward-bias region (right side of the vertical axis), the current increases exponentially with a slight increase in voltage, indicating the diode is conducting.
- In the reverse-bias region (left side of the vertical axis), the current remains nearly constant at a very low level until a certain reverse voltage (breakdown voltage, $BV$) is reached.
- Beyond the breakdown voltage, the current increases sharply, indicating breakdown conditions such as Zener or avalanche breakdown.
4. **Key Features and Technical Details:**
- **Forward Bias Region:** Starts at the origin, where current $I_D$ increases sharply after a threshold voltage $V_D$ is surpassed.
- **Reverse Bias Region:** Shows a small reverse current $I_R$ until reaching the breakdown voltage $BV$ at $-V_Z$.
- **Breakdown Point ($Q_B$):** At this point, the reverse current increases significantly.
- **Slope in Reverse Region:** The slope $1/r_z$ indicates the dynamic resistance in the breakdown region.
- **Forward Conducting Point ($Q_F$):** Represents the point where the diode is fully conducting in the forward direction.
5. **Annotations and Specific Data Points:**
- The graph is annotated with specific points such as $Q_B$ (breakdown point) and $Q_F$ (forward conducting point).
- The breakdown voltage $-V_Z$ and the forward voltage $V_D$ are marked on the voltage axis.
- The reverse current $I_R$ and the forward current $I_D$ are indicated on the current axis.
This graph effectively illustrates the nonlinear behavior of a $pn$ junction diode, highlighting the significant increase in current during breakdown and forward conduction.
FIGURE 1.46 The complete $i-v$ characteristic of a pn junction.
breakdown, and avalanche breakdown. The former occurs in heavily doped junctions, the latter in lightly doped junctions.
- In heavily doped junctions the electric field within the SCL is already fairly strong, and increasing it further with several volts of reverse bias will give it enough strength to strip electrons away from the covalent bonds and thus create electron-hole pairs. The field itself then sweeps these newly freed charges out of the SCL (holes into the $p$ side, electrons into the $n$ side), thus sustaining much higher currents than in the case of thermal generation alone. Called Zener effect, this phenomenon occurs for BV values on the order of 6 V or less.
- In lightly doped junctions the electric field is not strong enough to break covalent bonds directly. However, with the wider SCL widths now available, the field has more space to accelerate any free electrons that happen to be within the SCL. Given sufficient kinetic energy, these electrons will free new electron-hole pairs as they collide with the atoms of the crystal lattice. These secondary electrons can in turn free additional electrons, in an effect aptly called avalanche effect. This effect occurs for BV values on the order of 6 V or higher. In the neighborhood of 6 V the Zener and avalanche effects may coexist.
When designed to operate deliberately in the breakdown region, a diode is commonly referred to as a Zener diode, regardless of whether the actual breakdown mechanism is of the Zener or avalanche type. The coordinates of an operating point $Q_{B}$ in the breakdown region are conveniently relabeled as $-I_{Z}$ and $-V_{Z}$, respectively. The slope of the diode curve in the breakdown region is denoted as $1 / r_{z}$, and sufficiently to the left of the breakdown knee it is approximately constant. Depending on fabrication details, $r_{z}$ is on the order of $10^{1}$ to $10^{3} \Omega$.
The temperature coefficient at a given breakdown-region operating point $Q_{B}\left(I_{Z}, V_{Z}\right)$ is defined as
$$
\operatorname{TC}\left(V_{Z}\right)=\left.\frac{\partial V_{Z}}{\partial T}\right|_{I_{Z}}
$$
We again distinguish two cases:
- In the case of the Zener effect, increasing temperature will increase thermal agitation and thus facilitate covalent breakdown, so we need to turn down the applied voltage $V_{Z}$ a bit if we want to maintain the same current level $I_{Z}$ at a higher temperature. Thus, $\mathrm{TC}\left(V_{Z}\right)<0$ in the Zener case.
- In the avalanche case, thermal agitation will increase the frequency of collisions of free electrons with atoms of the crystal lattice, making it more difficult for electrons to accelerate and acquire sufficient kinetic energy to trigger the avalanche mechanism. Now we need to turn $u p$ the applied voltage $V_{Z}$ a bit if we want to maintain the same current level $I_{Z}$, so $\mathrm{TC}\left(V_{Z}\right)>0$ in the avalanche case. We summarize the two mechanisms as follows:
The Zener effect occurs in heavily doped junctions, $V_{Z}$ is lower than about 6 V , and $\mathrm{TC}\left(V_{Z}\right)<0$
The avalanche effect occurs in lightly doped junctions, $V_{Z}$ is higher than about 6 V , and $\mathrm{TC}\left(V_{Z}\right)>0$
By playing with the impurity concentrations during processing, the manufacturer can control the BV of a junction to a particular value. Two familiar representatives are the base-emitter (BE) and the base-collector (BC) junctions forming the bipolar junction transistor (BJT). The BE junction is heavily doped, and thus breaks down by the Zener effect in the neighborhood of 6 V . This low BV value poses no problem when the BJT is operated in the forward-active (FA) region, where the BE junction is forward biased. However, in the FA region the BC junction is reverse biased. To prevent it from going into breakdown, the collector region is doped lightly, indicating that BC breakdown is of avalanche type.
## 1.9 FORWARD-BIASED DIODE CHARACTERISTICS
For sufficiently high forward voltages (in practice, for $v>4 V_{T} \cong 0.1 \mathrm{~V}$ ), we can ignore unity in Eq. (1.57), and write
$$
\begin{equation*}
i_{D}=I_{S} e^{v_{D} / V_{T}} \tag{1.61}
\end{equation*}
$$
where we are now using subscript $D$ to signify operation well into the forward region. This equation represents a perfectly exponential $i-v$ characteristic. Also called the ideal diode equation, it is satisfied by practical pn junctions quite well over a wide range of currents, typically on the order of six decades, making it one of the most predictable laws of electronics. The exponential law enjoys some fascinating properties, as we are about to see.
Equation (1.61) is readily turned around as
$$
\begin{equation*}
v_{D}=V_{T} \ln \left(\frac{i_{D}}{I_{s}}\right) \tag{1.62}
\end{equation*}
$$
In this form, it allows us to find the voltage drop $v_{D}$ needed to sustain a given current $i_{D}$.
### Properties of the Exponential Characteristic
The slope of the diode curve at a given operating current $I_{D}$ in the forward-bias region is defined as $g_{d}=d i_{D} /\left.d v_{D}\right|_{I_{D}}$, and is called the dynamic conductance of the diode. Differentiating Eq. (1.61), we get
$$
\begin{equation*}
g_{d}=\frac{I_{D}}{V_{T}} \tag{1.63}
\end{equation*}
$$
indicating that slope is linearly proportional to the operating current $I_{D}$. The reciprocal of $g_{d}$ is called the dynamic resistance of the diode, or $r_{d}=1 / g_{d}=V_{T} / I_{D}$. Both $g_{d}$ and $r_{d}$ span quite a range of values, depending on the operating current. Note the following significant values:
$$
r_{d}(1 \mathrm{~mA})=26 \Omega \quad r_{d}(1 \mu \mathrm{~A})=26 \mathrm{k} \Omega \quad r_{d}(1 \mathrm{nA})=26 \mathrm{M} \Omega
$$
The parameters $r_{d}$ and $g_{d}$ form the basis of small-signal diode circuit analysis, to be studied later.
Given a diode carrying a certain current $I_{D}$, we wish to find the voltage change $\Delta V_{D}$ required to change its current from $I_{D}$ to $m I_{D}$, where $m$ is some multiplicative factor. Using Eq. (1.62), we find such a voltage change as $\Delta V_{D}=V_{T} \ln \left(m I_{D} / I_{s}\right)-$ $V_{T} \ln \left(I_{D} / I_{s}\right)=V_{T} \ln \left[\left(m I_{D} / I_{s}\right) /\left(I_{D} / I_{s}\right)\right]$, or
$$
\Delta V_{D}=V_{T} \ln m
$$
Two popular cases are a change in current by an octave ( $m=2^{ \pm 1}$ ), or by a decade $\left(m=10^{ \pm 1}\right)$, which give, respectively, $\Delta V_{D(\text { oct })}=(26 \mathrm{mV}) \times( \pm \ln 2) \cong \pm 18 \mathrm{mV}$, and $\Delta V_{D(\mathrm{dec})}=(26 \mathrm{mV}) \times( \pm \ln 10) \cong \pm 60 \mathrm{mV}$. These findings form the basis of the following important rules of thumb, illustrated pictorially in Fig. 1.47a:
To effect an octave change in $I_{D}$ we need to change $V_{D}$ by 18 mV
To effect a decade change in $I_{D}$ we need to change $V_{D}$ by 60 mV
A convenient feature of the above rules is that they are independent of the particular quiescent point $Q_{F}$ on the diode curve where the changes are made. For instance, consider a diode initially operating at a quiescent current of $10 \mu \mathrm{~A}$. If we wish to double its current to $20 \mu \mathrm{~A}$, we need an increase $\Delta V_{D}=18 \mathrm{mV}$. To effect the tenfold change $10 \mu \mathrm{~A} \rightarrow 100 \mu \mathrm{~A}$ we need an increase $\Delta V_{D}=60 \mathrm{mV}$. Likewise, the change $10 \mu \mathrm{~A} \rightarrow 1 \mu \mathrm{~A}$ requires a decrease $\Delta V_{D}=-60 \mathrm{mV}$. If you wish to change $I_{D}$ from
image_name:(a)
description:The graph labeled (a) is an exponential I-V (current-voltage) characteristic curve of a diode. The x-axis represents the voltage across the diode, denoted as \( v \), and the y-axis represents the current through the diode, denoted as \( i \). Both axes are likely using a linear scale.
Axes Labels and Units:
- **X-axis (Voltage, \( v \))**: Labeled with voltage values such as \( V_D \), \( V_D + 18 \text{ mV} \), and \( V_D + 60 \text{ mV} \).
- **Y-axis (Current, \( i \))**: Labeled with current multiples like \( I_D \), \( 2I_D \), and \( 10I_D \).
Overall Behavior and Trends:
The graph shows the diode's exponential increase in current with an increase in voltage. Initially, the current increases slowly with voltage, but as the voltage continues to rise, the current increases more rapidly, showing the exponential nature of the diode's I-V characteristic.
Key Features and Technical Details:
- **Point \( Q_1 \)**: Represents the initial operating point at \( I_D \) and \( V_D \).
- **Point \( Q_2 \)**: Indicates a current of \( 2I_D \) at a voltage of \( V_D + 18 \text{ mV} \).
- **Point \( Q_{10} \)**: Shows a current of \( 10I_D \) at a voltage of \( V_D + 60 \text{ mV} \).
Annotations and Specific Data Points:
- The graph illustrates how the diode current changes with small increments in voltage, emphasizing the rule of thumb that a 60 mV increase in voltage results in a tenfold increase in current.
- The graph is marked at specific voltage increments to show how the diode's current behavior changes with these voltage steps.
image_name:(b)
description:The graph labeled (b) is an I-V (current-voltage) characteristic curve for a pn junction diode, illustrating the effect of temperature on the diode's behavior. The graph is plotted with the current \( i \) on the vertical axis and the voltage \( v \) on the horizontal axis. Both axes are likely in linear scale, though specific units are not marked, it is implied that the current is in microamperes and the voltage in millivolts.
**Overall Behavior and Trends:**
The graph shows two curves, both exhibiting the typical exponential increase of current with voltage characteristic of a diode. As the voltage increases, the current rises sharply, indicating the diode's forward-bias operation. The two curves represent different temperatures, with the rightmost curve corresponding to a lower temperature and the leftmost curve to a higher temperature.
**Key Features and Technical Details:**
- The shift in the curve due to temperature change is marked as \(-2 \text{ mV/°C}\), indicating that for every degree Celsius increase in temperature, the curve shifts 2 mV to the left. This represents the decrease in the forward voltage required to maintain the same current as the temperature increases.
- The curves do not intersect, showing that at any given voltage, the current is higher at the elevated temperature.
**Annotations and Specific Data Points:**
- The annotation "Increasing \( T \)" indicates the direction of temperature increase.
- The voltage shift \(-2 \text{ mV/°C}\) is specifically marked between the two curves, emphasizing the rate of change with temperature.
This graph effectively illustrates how the forward voltage of a diode decreases with increasing temperature, a critical consideration in diode circuit design and analysis.
FIGURE 1.47 Illustrating some important rules of thumb for pn junctions.
$10 \mu \mathrm{~A}$ to $50 \mu \mathrm{~A}$, pretend first to raise it from $10 \mu \mathrm{~A}$ to $100 \mu \mathrm{~A}\left(\Delta V_{D}=+60 \mathrm{mV}\right)$, and then to lower it from $100 \mu \mathrm{~A}$ to $50 \mu \mathrm{~A}\left(\Delta V_{D}=-18 \mathrm{mV}\right)$, for a net change $V_{D}=60-18=42 \mathrm{mV}$.
### Temperature Dependence
Whether we use Eq. (1.61) or (1.62), it is apparent that the diode characteristic depends on temperature via $V_{T}$ as well as $I_{s}$. A convenient way to characterize the overall thermal dependence is via the temperature coefficient of the forward voltage drop at a given operating current $I_{D}$, defined as
$$
\begin{equation*}
\mathrm{TC}\left(V_{D}\right)=\left.\frac{\partial V_{D}}{\partial T}\right|_{I_{D}} \tag{1.64}
\end{equation*}
$$
Differentiating Eq. (1.62), we obtain
$$
\begin{equation*}
\mathrm{TC}\left(V_{D}\right)=\left.\frac{\partial\left[V_{T} \ln \left(I_{D} / I_{s}\right)\right]}{\partial T}\right|_{I_{D}}=\frac{V_{D}}{T}-V_{T}\left(\frac{d I_{s} / d T}{I_{s}}\right) \tag{1.65}
\end{equation*}
$$
According to Eqs. (1.58) and (1.59), $I_{s} \propto n_{i}^{2}(T) D(T)$, where $n_{i}$ is the intrinsic concentration and $D$ is the diffusivity, both of which are functions of temperature $T$. By Eq. (1.21), $n_{i}^{2}(T) \propto T^{3} e^{-V_{01} / V_{T}}$, where $V_{G 0}=1.205 \mathrm{~V}$ is the bandgap voltage for silicon. By Eqs. (1.20) and (1.28), $D(T)=(k T / q) \mu(T)$, where $\mu(T)$ is the mobility, in turn a function of temperature of the type $\mu(T) \propto T^{m}, m \cong-1.5$. Combining all this we have
$$
\begin{gathered}
I_{s} \propto T^{4+m} e^{-V_{c o}(q / k T)} \\
\frac{d I_{s} / d T}{I_{s}}=\frac{(4+m) T^{4+m-1} e^{-V_{\sigma_{0}}(q / k T)}+T^{4+m} e^{-V_{c o l}(q / k T)} \times V_{G 0}\left(q / k T^{2}\right)}{T^{4+m} e^{-V_{c 0}(q / k T)}}=\frac{4+m}{T}+\frac{V_{G 0}}{T V_{T}}
\end{gathered}
$$
Substituting into Eq. (1.65) and simplifying, we finally get
$$
\begin{equation*}
\operatorname{TC}\left(V_{D}\right)=\frac{V_{D}-(4+m) V_{T}-V_{G 0}}{T} \tag{1.66}
\end{equation*}
$$
Assuming $V_{D}=0.65 \mathrm{~V}$ at $T=300 \mathrm{~K}$, Eq. (1.66) gives $\mathrm{TC}\left(V_{D}\right) \cong-2.1 \mathrm{mV} /{ }^{\circ} \mathrm{C}$. Engineers remember $p n$ junction thermal behavior via the following rule of thumb, pictorially illustrated in Fig. 1.47b:
At room-temperature the forward voltage-drop of a pn diode drifts by about $-2 \mathrm{mV} /{ }^{\circ} \mathrm{C}$
Once we know $V_{D}$ at some reference temperature $T_{0}$, we can estimate it at any other temperature $T$ using
$$
\begin{equation*}
V_{D}(T) \cong V_{D}\left(T_{0}\right)-(2 \mathrm{mV}) \times\left(T-T_{0}\right) \tag{1.67}
\end{equation*}
$$
EXAMPLE 1.13 If at $25^{\circ} \mathrm{C}$ a certain diode exhibits $V_{D}=650 \mathrm{mV}$ at $I_{D}=0.1 \mathrm{~mA}$, estimate $V_{D}$ at:
(a) $T=70^{\circ} \mathrm{C}$ and $I_{D}=0.1 \mathrm{~mA}$.
(b) $T=0^{\circ} \mathrm{C}$ and $I_{D}=0.1 \mathrm{~mA}$.
(c) $T=50^{\circ} \mathrm{C}$ and $I_{D}=0.02 \mathrm{~mA}$.
(d) $T=40^{\circ} \mathrm{C}$ and $I_{D}=4 \mathrm{~mA}$.
#### Solution
Using the rules of thumb learned thus far we get:
(a) $V_{D} \cong 650-2 \times(70-25)=650-90=560 \mathrm{mV}$.
(b) $V_{D} \cong 650-2 \times(0-25)=650+50=700 \mathrm{mV}$.
(c) First, pretend to lower $I_{D}=$ from 0.1 mA to $0.01 \mathrm{~mA}\left(\Delta V_{D}=-60 \mathrm{mV}\right)$, and then double it ( $\Delta V_{D}=+18 \mathrm{mV}$ ) to end up at 0.02 mA with the net value $V_{D} \cong 650-60+18=608 \mathrm{mV}$. Finally, pretend to increase temperature from $25^{\circ} \mathrm{C}$ to $50^{\circ} \mathrm{C}$, for an additional change $\Delta V_{D}=-2 \times(50-25)=-50 \mathrm{mV}$. The final value is thus $V_{D} \cong 608-50=558 \mathrm{mV}$.
(d) Proceeding as in part ( $c$ ) we find $V_{D}=650+60+18+18-2 \times(40-25)=$ 716 mV .
If a forward-biased diode is placed in series with a reverse-biased Zener diode of the opposite temperature coefficient, or $\mathrm{TC}\left(V_{Z}\right)=-\mathrm{TC}\left(V_{D}\right) \cong+2 \mathrm{mV}$, the thermal variations of the two devices will cancel each other out to yield a composite voltage drop $V_{R E F}=V_{Z}+V_{D}$ approaching zero temperature coefficient. This technique is used in the implementation of thermally stable voltage references. The best stability is achieved for $V_{Z} \cong 6.2 \mathrm{~V}$, thus yielding $V_{R E F} \cong 6.2+0.7=6.9 \mathrm{~V}$ with $\mathrm{TC}\left(V_{R E F}\right) \rightarrow 0$.
### Deviations from Ideality
Rewriting Eq. (1.62) as $v_{D}=V_{T}\left(\ln i_{D}-\ln I_{s}\right)$, or
$$
\ln i_{D}=\left(\frac{1}{V_{T}}\right) v_{D}+\ln I_{s}
$$
indicates that if we plot $i_{D}$ versus $v_{D}$ on semi-logarithmic paper ( $v_{D}$ on the linear axis, $i_{D}$ on the logarithmic axis), we get a curve of the type
$$
y=\left(1 / V_{T}\right) x+y(0)
$$
This is a straight line with slope $\left(1 / V_{T}\right)$ and $0-\mathrm{V}$ intercept at $i_{D}=I_{S}$. This feature proves very convenient in the characterization of a diode. Given a set of measured data, we can easily find the best-fit straight line; then, we find its slope to obtain the experimental value of $V_{T}$, and we extrapolate the line in the limit $v_{D} \rightarrow 0$ to find its intercept on the $i_{D}$ axis and thus obtain the experimental value of $I_{s}$.
The semi-log-plot of an actual low-power pn diode characteristic is more likely to appear as in Fig. 1.48. The curve is fairly straight over a wide range of currents, typically from 1 nA to 1 mA , but deviates from ideality both at the high and
image_name:Figure 1.48
description:**Type of Graph and Function:**
The graph is a semi-logarithmic plot representing the characteristic behavior of a low-power pn diode. It displays the relationship between the diode current ($i_D$) and the diode voltage ($v_D$).
**Axes Labels and Units:**
- The x-axis represents the diode voltage $v_D$, plotted on a linear scale.
- The y-axis represents the diode current $i_D$, plotted on a logarithmic scale.
- The graph includes annotations for different emission coefficients $n$ and thermal voltage $1/V_T$.
**Overall Behavior and Trends:**
The graph shows a characteristic curve that is fairly linear over a wide range of currents, typically from 1 nA to 1 mA. The curve deviates from this linearity at both low and high current levels. At low current levels, the curve starts below the linear region, while at high current levels, it bends upwards, indicating deviation from ideal behavior.
**Key Features and Technical Details:**
- The linear region of the graph, where the emission coefficient $n = 1$, indicates ideal diode behavior.
- At low current levels, the emission coefficient $n = 2$, indicating deviation due to loss of mobile charge.
- At high current levels, the emission coefficient $n = 2$ again, due to bulk resistance and high-level injection effects.
- The intercept on the $i_D$ axis at $v_D = 0$ gives the saturation current $I_s$.
- The slope of the linear region is related to the thermal voltage $1/V_T$.
**Annotations and Specific Data Points:**
- The graph is annotated with lines indicating the regions where $n = 1$ and $n = 2$.
- The thermal voltage $1/V_T$ is marked on the linear region of the graph.
- The saturation current $I_s$ is indicated at the intercept of the $i_D$ axis.
FIGURE 1.48 Illustrating the effect of the emission coefficient $n$ at low and at high current levels.
low ends of the range. These deviations stem from various approximations that were made in the course of the derivations leading to the ideal diode equation. Specifically, deviations at the high end of the current range are caused by the presence of bulk resistance in the neutral regions as well as high-level injection effects, while deviation at the low end is caused by loss of mobile charges to recombination within the space-charge layer (SCL). We now wish to examine these approximations in greater detail.
- In our derivations we have assumed zero electric field inside the regions at either side of the SCL, so that the voltage that we apply across the terminals is transmitted entirely to the edges of the SCL itself. However, like any conductor, each of these regions exhibits a nonzero-if small—ohmic resistance called the bulk resistance. Denoting the overall resistance (sum of the $p$-side and $n$-side bulk resistances) as $r_{s}$, we observe that in response to the externally applied voltage $v_{D}$, the actual voltage $v_{J}$ reaching the junction is, by KVL,
$$
\begin{equation*}
v_{J}=v_{D}-r_{S} i_{D} \tag{1.68}
\end{equation*}
$$
When the diode is operated at low current levels, the voltage drop across the bulk material is negligible and $v_{J} \cong v_{D}$. Not so at the upper end of the current range, where this drop may become significant and cause a deviation of the actual $i-v$ characteristic from exponential ideality. On semi-log paper, this appears as a curvature for values of $i_{D}$ on the order of 1 mA or higher.
- If the applied voltage across the junction is increased to the point of making the minority densities at the SCL edges comparable to the majority densities there, the low-level injection assumption no longer holds, and the diode equation now takes on the form
$$
\begin{equation*}
i_{D}=I_{s} e^{v_{D} / n V_{T}} \tag{1.69a}
\end{equation*}
$$
where $n$, called the emission coefficient (not to be confused with the electron concentration $n!$ ) is such that $n \rightarrow 1$ under low-level injection conditions, but $n \rightarrow 2$ when these conditions no longer hold. The inverse equation is now
$$
\begin{equation*}
v_{D}=n V_{T} \ln \left(\frac{i_{D}}{I_{s}}\right) \tag{1.69b}
\end{equation*}
$$
Rewriting as
$$
\ln i_{D}=\left(\frac{1}{n V_{T}}\right) v_{D}+\ln I_{s}
$$
indicates that the slope of the semi-log curve is now $1 /\left(n V_{T}\right)$. Clearly, for $n=2$ the slope is only half of that for $n=1$. We can find the experimental value of the quantity $n V_{T}$ through a mere slope measurement on the semi-log plot.
- Equation (1.69) with $n \rightarrow 2$ holds also at the low end of the current range, but for a completely different reason, namely the loss of mobile charges to recombination (trapping) within the SCL. Evidently, our assumption of constant current densities within the SCL is not exactly valid. It must be said that loss to recombination occurs regardless of the operating point on the $i-v$ curve, but its effect is noticeable only at the low-end, where the forward current is comparable to, or even smaller than that due to loss. On semi-log paper, this appears as a curvature for values of $i_{D}$ on the order of 1 pA or lower.
EXAMPLE 1.14 If a $p n$ junction with $I_{s}=1 \mathrm{fA}$ gives $I_{D}=1 \mathrm{~mA}$ at $V_{D}=725 \mathrm{mV}$, find $r_{S}$.
#### Solution
By Eq. (1.62) the actual junction voltage is $V_{J}=(26 \mathrm{mV}) \ln \left(10^{-3} / 10^{-15}\right)=718.4 \mathrm{mV}$. By Eq. (1.68), $r_{S}=(725-718.4) / 1=6.6 \Omega$.
## 1.10 Dc ANALYSIS OF pn DIODE CIRCUITS
A task that arises all the time in the analysis of diode circuits is finding a diode's quiescent point $Q=Q\left(I_{D}, V_{D}\right)$. As we know, if the diode is embedded in an otherwise linear circuit, this task simplifies considerably if we replace the surrounding circuitry with its Thévenin equivalent and thus end up with the situation of Fig. 1.49a. Here, $V_{O C}$ is the open-circuit voltage that the external circuit would produce between the nodes corresponding to the anode and the cathode, but with the diode removed, and $R_{e q}$ is the external circuit's equivalent resistance, that is, the resistance as seen by the diode.
### Load-Line Analysis
The operating point can be visualized graphically as the intercept of the diode curve and the load line, as already seen in Fig. $1.5 b$ for the case of the ideal diode. The situation is depicted in Fig. $1.49 b$ for the case of a forward-biased pn junction diode. Though graphical analysis helps us develop a visual feel for a circuit's workings, we usually need to find the operating point $Q$ numerically, the issue that we are going to address next.
image_name:(a)
description:
[
name: V_OC, type: VoltageSource, value: V_OC, ports: {Np: VOC, Nn: GND}
name: R_eq, type: Resistor, value: R_eq, ports: {N1: VOC, N2: X1}
name: I_D, type: CurrentControlledCurrentSource, value: I_D, ports: {Np: X1, Nn: GND}
]
extrainfo:The circuit consists of a voltage source V_OC, a resistor R_eq, and a current-controlled current source I_D. The circuit is used to analyze the quiescent point Q of a pn-junction diode in a linear circuit.
image_name:(b)
description:The graph in Figure 1.49(b) is a load-line analysis used to determine the quiescent point (Q-point) of a pn-junction diode in a linear circuit. This is a graphical representation where two curves intersect: the diode's characteristic curve and the load line.
1. **Type of Graph and Function:**
- The graph is a combination of a diode's exponential I-V characteristic curve and a linear load line.
2. **Axes Labels and Units:**
- The horizontal axis (v) represents the voltage across the diode, labeled as \( V_D \), ranging from 0 to \( V_{OC} \).
- The vertical axis (i) represents the current through the diode, labeled as \( I_D \), ranging from 0 to \( \frac{V_{OC}}{R_{eq}} \).
3. **Overall Behavior and Trends:**
- The diode's characteristic curve starts at the origin and follows an exponential growth as voltage \( V_D \) increases, showing the typical forward-bias behavior of a diode.
- The load line is a straight line with a negative slope, intersecting the vertical axis at \( \frac{V_{OC}}{R_{eq}} \) and the horizontal axis at \( V_{OC} \).
4. **Key Features and Technical Details:**
- The intersection point, labeled as \( Q \), is the operating point where the diode's current \( I_D \) and voltage \( V_D \) satisfy both the diode's characteristic equation and the circuit's load equation.
- The load line's slope is determined by \( -\frac{1}{R_{eq}} \), representing the inverse of the equivalent resistance in the circuit.
5. **Annotations and Specific Data Points:**
- The point \( Q \) is marked on the graph, indicating the quiescent point where the diode operates in the circuit.
- The graph visually demonstrates the balance between the diode's forward-bias behavior and the circuit's constraints, allowing for an intuitive understanding of the diode's operation in the given configuration.
FIGURE 1.49 Finding the quiescent point $Q$ of a $p n$-junction diode embedded in a linear circuit.
### Iterative Analysis
With reference to Fig. 1.49a we observe that the diode current is, by Ohm's law,
$$
\begin{equation*}
I_{D}=\frac{V_{O C}-V_{D}}{R_{e q}} \tag{1.70}
\end{equation*}
$$
Also, the diode voltage is, by Eq. (1.69b),
$$
\begin{equation*}
V_{D}=n V_{T} \ln \frac{I_{D}}{I_{s}} \tag{1.71}
\end{equation*}
$$
where $n$ is the emission coefficient, $1 \leq n \leq 2$. In the following we shall assume $n=1$ for simplicity, but the ensuing analysis can readily be generalized to the case $n \neq 1$ by replacing $V_{T}$ with $n V_{T}$. Substituting Eq. (1.70) into (1.71) gives
$$
\begin{equation*}
V_{D}=n V_{T} \ln \frac{V_{O C}-V_{D}}{R_{e q} I_{s}} \tag{1.72}
\end{equation*}
$$
This is a transcendental equation in that it does not provide us with a closed-form expression for the unknown $V_{D}$. However, we can solve it by iterations. To this end, we start out with a reasonable initial estimate for $V_{D}$, we insert it in the right-hand side of Eq. (1.72) to come up with a better estimate, and then we insert this new estimate back in the right-hand side to come up with yet a better estimate, repeating the procedure if necessary, until the result settles within a predetermined resolution.
In the circuit of Fig. 1.49a let $R_{e q}=1 \mathrm{k} \Omega$, and let the diode have $n=1, V_{T}=26 \mathrm{mV}$, and $I_{s}=1 \mathrm{fA}$. Estimate $V_{D}$ down to the mV , as well as $I_{D}$, if (a) $V_{O C}=1.5 \mathrm{~V}$, (b) $V_{O C}=3 \mathrm{~V}$, and (c) $V_{O C}=0.75 \mathrm{~V}$.
#### Solution
(a) In the various $p n$-junction examples encountered so far we have found that $V_{D}$ is typically in the range of $0.6-0.7 \mathrm{~V}$, so let us arbitrarily start out with the initial guess $\mathrm{V}_{D(0)}=0.65 \mathrm{~V}$. Plugging into Eq. (1.72) gives the new estimate
$$
V_{D(1)}=n V_{T} \ln \frac{V_{O C}-V_{D(0)}}{R_{e q} I_{s}}=0.026 \ln \frac{1.5-0.65}{10^{3} \times 10^{-15}}=0.714 \mathrm{~V}
$$
Using this new value as initial guess we find
$$
V_{D(2)}=n V_{T} \ln \frac{V_{O C}-V_{D(1)}}{R_{e q} I_{s}}=0.026 \ln \frac{1.5-0.714}{10^{-12}}=0.712 \mathrm{~V}
$$
Iterating once more we find
$$
V_{D(3)}=n V_{T} \ln \frac{V_{O C}-V_{D(2)}}{R_{e q} I_{s}}=0.026 \ln \frac{1.5-0.712}{10^{-12}}=0.712 \mathrm{~V}
$$
Since the result hasn't changed within the intended resolution of 0.001 V ( $=1 \mathrm{mV}$ ), we conclude that $V_{D}=712 \mathrm{mV}$. Finally, the current is, by Eq. (1.70),
$$
I_{D}=\frac{1.5-0.712}{10^{3}}=0.788 \mathrm{~mA}
$$
(b) This time let us start out with the initial guess $V_{D(0)}=0.7 \mathrm{~V}$. Then,
$$
V_{D(1)}=0.026 \ln \frac{3-0.7}{10^{-12}}=0.740 \mathrm{~V}
$$
One more iteration confirms that this is actually the desired value, or $V_{D}=$ 740 mV within a 1-mV resolution. Then, $I_{D}=(3-0.74) / 1=2.26 \mathrm{~mA}$.
(c) Starting again with $V_{D(0)}=0.65 \mathrm{~V}$, we find
$$
V_{D(1)}=0.026 \ln \frac{0.75-0.65}{10^{-12}}=0.659 \mathrm{~V}
$$
Three more iterations confirm the final value $V_{D}=657 \mathrm{mV}$. Consequently, $I_{D}$ $=(0.75-0.657) / 1=93 \mu \mathrm{~A}$.
Remark 1: In going from (a) to (b) we have doubled $V_{O C}$, and in going from (a) to (c) we have halved $V_{O C}$; however, $I_{D}$ has neither doubled nor halved, as the presence of the diode renders the circuit nonlinear.
Remark 2: We could have found $I_{D}$ also using the diode equation. For instance, in part (a) we could have calculated
$$
I_{D}=I_{S} e^{V_{D} / n V_{T}}=10^{-15} e^{712 / 26}=0.782 \mathrm{~mA}
$$
This disagrees with the value of 0.788 mA found via Eq. (1.70). True, both calculations are afflicted by roundoff errors, but even so, which result is the more dependable of the two? Here's an important point to keep in mind: because of the high sensitivity of the exponential function to even small variations in its exponent, the value of $V_{D}$ in the exponent must be known very accurately for the result to be also accurate. By contrast, the value of the $V_{D}$ in the linear Eq. (1.70) need not be as accurate, and yet it will still yield a dependable $I_{D}$ value. Consequently, 0.788 mA is the more accurate value in our example.
Remark 3: Of course, if we use the exponential form with a more accurate value of $V_{D}$ the resulting $I_{D}$ will also be more accurate. In fact, using just one more significant digit from the third-iteration result, which is $V_{D(3)}=0.7122 \mathrm{~V}$ (rather than the truncated value of 0.712 V ) we get
$$
I_{D}=10^{-15} e^{712.2 / 26}=0.788 \mathrm{~mA}
$$
This matches that found via Eq. (1.70). If, for some reason, you need to use the diode equation in its exponential form, make sure that you know the value of $V_{D}$ to an adequate degree of accuracy!
### Piecewise-Linear Approximation and Large-Signal Diode Models
Load-line analysis provides a graphical means for visualizing a diode's role in a circuit, and iterative analysis provides a numerical means for calculating a diode's operating point. In practice, whether we analyze an existing diode circuit or we design a new one, we need faster, if only approximate, analysis techniques. Moreover, as we apply these techniques, we wish to draw from the wealth of knowledge acquired in prerequisite linear-circuits courses. Both requirements are met by effecting upon the actual pn-junction characteristic of Fig. 1.46 a piecewise-linear approximation as depicted in Fig. 1.50. Specifically, the actual curve, shown in shaded form, is approximated with three straight segments, each corresponding to a different region of operation, namely, the forward (ON), the cutoff (CO), and the breakdown (BD) regions. We make the following observations:
- When a pn junction is forward biased, its characteristic is exponential, that is, a curve that after a brief knee, shoots up quite rapidly, no matter which current range we choose to display. The curves of Figs. 1.47 and $1.49 b$ were doctored a bit to allow for a better visualization of the details under discussion, but the actual curve is indeed as in Fig. 1.46-quite steep. We know from one of the rules of thumb that increasing $V_{D}$ by a mere 60 mV raises $I_{D}$ tenfold, while decreasing it by 60 mV lowers $I_{D}$ tenfold, indicating that within the
image_name:Piecewise-linear approximations and large signal models of the pn junction diode
description:The graph represents piecewise-linear approximations and large signal models of a pn junction diode, showcasing its behavior in three distinct regions of operation: forward (ON), cutoff (CO), and breakdown (BD).
1. **Type of Graph and Function:**
- The graph is a piecewise-linear approximation of the diode's current-voltage (I-V) characteristics.
2. **Axes Labels and Units:**
- The horizontal axis represents voltage (v), while the vertical axis represents current (i).
- Units are not explicitly labeled, but typically voltage is in volts (V) and current in amperes (A).
3. **Overall Behavior and Trends:**
- The graph is divided into three regions:
- **Forward (ON) Region:** The current increases sharply with a small increase in voltage, indicating the diode is conducting. This is represented by a steep curve on the right side of the origin.
- **Cutoff (CO) Region:** Near the origin, the diode is non-conducting, and the current is nearly zero despite changes in voltage.
- **Breakdown (BD) Region:** On the left side, as the reverse voltage increases, the diode enters breakdown, allowing current to increase again.
4. **Key Features and Technical Details:**
- **Forward Region (ON):** The diode starts conducting at a threshold voltage, labeled as \( V_{D(on)} \).
- **Cutoff Region (CO):** The current is negligible, indicating the diode is off.
- **Breakdown Region (BD):** Characterized by a breakdown voltage \( BV \), where the reverse current increases sharply.
- **Annotations:**
- The graph includes symbols representing the diode's equivalent circuits in each region.
- In the BD region, parameters \( V_{Z} \) and \( r_{z} \) are shown, indicating the Zener voltage and dynamic resistance, respectively.
5. **Annotations and Specific Data Points:**
- The graph includes labels such as ON, CO, and BD to indicate regions.
- Specific points like \( V_{D(on)} \) and \( V_{Z0} \) are marked, indicating the onset of conduction and breakdown voltages.
This graph effectively illustrates the diode's operation in different regions, showing how it behaves under various voltage conditions.
image_name:forward (ON)
description:
[
name: IZ, type: CurrentSource, value: IZ, ports: {Np: C, Nn: A}
name: VZ, type: VoltageSource, value: VZ, ports: {Np: C, Nn: A}
name: rz, type: Resistor, value: rz, ports: {N1: C, N2: A}
name: VZ0, type: VoltageSource, value: VZ0, ports: {Np: C, Nn: A}
name: BD, type: Other, ports: {N1: C, N2: A}
name: CO, type: Other, ports: {N1: C, N2: A}
name: ON, type: Switch, ports: {N1: A, N2: C}
name: ID, type: CurrentSource, value: ID, ports: {Np: A, Nn: C}
name: VD(on), type: VoltageSource, value: VD(on), ports: {Np: A, Nn: C}
]
extrainfo:The diagram represents the piecewise-linear approximations and large signal models of a pn junction diode in its three regions of operation: forward (ON), cutoff (CO), and breakdown (BD). It shows the transition between these states with corresponding circuit representations.
image_name:cutoff (CO) and breakdown (BD)
description:
[
name: Z, type: Diode, ports: {Na: C, Nc: A}
name: rz, type: Resistor, value: rz, ports: {N1: C, N2: A}
name: D, type: Diode, ports: {Na: A, Nc: C}
]
extrainfo:The diagram illustrates the piecewise-linear approximations and large signal models of the pn junction diode in its three regions of operation: forward (ON), cutoff (CO), and breakdown (BD). It includes a Zener diode model with a breakdown voltage Vz and a resistor rz in parallel. The graph shows the I-V characteristics with different regions marked.
FIGURE 1.50 Piecewise-linear approximations and large signal models of the pn junction diode in its three regions of operation: forward (ON), cutoff (CO), and breakdown (BD).
range $V_{D} \pm 60 \mathrm{mV}, I_{D}$ undergoes a 100-to-1 change! For practical purpose, when a junction conducts only $1 / 100$ of its normal current, it can be regarded as being cut off (in digital applications, even a 10-to-1 ratio will do). Considering that a low-power silicon junction operating in the mA range typically exhibits a roomtemperature voltage drop of about 0.7 V , we approximate the exponential curve with a vertical segment located at $v=V_{D(\text { on })}=0.7 \mathrm{~V}$. The corresponding diode model is thus a battery of value $V_{D(\text { on })}$, as shown. For obvious reasons, this model is referred to as a constant voltage-drop model. The reader, who may find this approximation unconvincing, will soon realize that it is actually quite effective in providing us with a quick feel for the workings of diode circuits. During a second and more detailed pass, one can always use iterative techniques or computer simulation such as PSpice to refine the analysis and come up with more accurate results.
- From the knee leading to the exponential rise to the knee leading to the breakdown drop, the current is negligibly small, indicating that for practical purposes we can regard the junction as cut off (CO). The corresponding diode model is an open circuit, as shown. Note that the cutoff region extends to the right of the origin, all the way to the onset of the exponential raise. Even though for $v>0$ the junction is, strictly speaking, forward biased, the actual current between 0 V and the knee leading to the exponential raise is simply too small for the junction to be considered convincingly on. So, we take a weakly forward-biased junction as being effectively cut off.
- Well into the breakdown (BD) region, the characteristic is close to linear, so we approximate it with a straight segment, as shown. As seen in Fig. 1.46, the slope of the curve there is denoted as $1 / r_{z}$, and a BD operating point is denoted as $Q_{B}=Q_{B}\left(-I_{Z},-V_{Z}\right)$. To signify operation in the BD region, the circuit symbol for the diode is modified as shown at the lower left of Fig. 1.50. Also, the device is drawn upside down to make $V_{Z}$ positive at the top (cathode), and to make $I_{Z}$ positive when flowing from cathode to anode. This gimmick dispenses us from having to deal with negative voltages and currents. The diode model in the BD region is a battery of value $V_{Z 0}$ with a series resistance $r_{z}$, where $-V_{z 0}$ represents the location of the intercept of the extrapolated linear curve with the $v$ axis.
Again, the beginner may deem the piecewise linear approximation too gross, especially near the knee leading from the CO to the BD regions. However, it turns out that a $p n$ junction is seldom operated in the knee region. Generally speaking, the $p n$-junction finds application either as a rectifying switch, or as a voltage reference.
- When used as a rectifier a diode is designed to alternate between the ON and CO modes without ever entering the BD region. In fact, to be on the safe side, rectifiers are implemented with diodes having a breakdown voltage (BV) well above the maximum reverse voltage, also called peak inverse voltage (PIV), that the device is likely to ever experience in the given circuit.
- When used as a voltage reference a diode is operated deliberately in the BD region, and far enough down the BD curve to prevent the operating point from ever getting too close to the knee. This issue will be addressed in greater detail in Section 1.12.
Repeat Example 1.15, but using the constant voltage-drop diode model. Comment on your findings.
#### Solution
Equation (1.70) now approximates to
$$
\begin{equation*}
I_{D}=\frac{V_{O C}-V_{D(\mathrm{on})}}{R_{e q}} \tag{1.73}
\end{equation*}
$$
or $I_{D}=\left(V_{O C}-0.7\right) / 1$.
(a) We now get $I_{D}=(1.5-0.7) / 1=0.8 \mathrm{~mA}$, which is very close to 0.788 mA found in Example 1.15.
(b) Now $I_{D}=(3-0.7) / 1=2.3 \mathrm{~mA}$, which is even closer to 2.26 mA found in Example 1.15.
(c) If we try $I_{D}=(0.75-0.7) / 1=50 \mu \mathrm{~A}$, we obtain a result in significant disagreement with $93 \mu \mathrm{~A}$ found previously. It is apparent that Eq. (1.73) will give dependable results only if $V_{O C} \gg V_{D(\text { on })}$. If this condition is not met, then the iterative method is the only reasonable alternative for hand calculations.
Remark: Once again we want to stress the difference between $V_{D}$ and $V_{D(\text { on })}$, repeated as follows:
- $V_{D}$ is the actual voltage drop across the diode, and it can be used in critical calculations such as $I_{D}=I_{s} \exp \left(V_{D} / V_{T}\right)$, provided it is known to an adequate degree of accuracy, e.g. within millivolts.
- $V_{D(\text { on })}$ is an assumed $(\sim 0.7 \mathrm{~V})$ and thus only approximate value that we use in less critical calculations such as $I_{D}=\left[V_{O C}-V_{D(\text { on })}\right] / R_{e q}$, provided $V_{O C} \gg V_{D(\mathrm{on})}$.
A potentially catastrophic mistake is to write $I_{D}=I_{s} \exp \left(V_{D(\text { on })} / V_{T}\right)$. Make sure you never do this!
#### Circuit Analysis Using the Piecewise Linear Approximation
Following is a procedure for determining the operating point of a pn diode for the case in which the device is embedded in an otherwise linear circuit:
- First, find the open-circuit voltage $V_{O C}$ produced by the external circuit with the diode removed (recall that the polarity of $V_{O C}$ is defined positive at the node connected to the anode.)
- Next, determine the region of diode operation as follows:
- If $V_{O C}>V_{D(\text { on })}(\cong 0.7 \mathrm{~V}$ for a silicon diode), the diode is operating in the ON region
- If $-V_{Z 0}<V_{O C}<V_{D(\text { on })}$, the diode is cut off (CO)
- If $V_{O C}<-V_{Z 0}$, the diode is operating in the BD region
- Finally, replace the diode with the model pertaining to that particular region, as depicted in Fig. 1.50, and proceed with the analysis of the resulting linear circuit using familiar analysis techniques.
Let us illustrate with practical examples.
### The pn Junction Diode as a Rectifier
To investigate the operation of the $p n$ junction diode as a rectifier we perform a PSpice simulation of a half-wave rectifier using the popular 1N4148 low-power pn diode, whose model is available in PSpice's analog library. With reference to the circuit of Fig. 1.51 $a$ we make the following observations:
- As long as $v_{I}<V_{D(\text { on })}$, the diode is off and the circuit behaves as in Fig. 1.51b, top, giving
$$
\begin{equation*}
v_{O}=0 \quad \text { for } v_{I}<V_{D(\text { on })} \tag{1.74a}
\end{equation*}
$$
- For $v_{I}>V_{D(\text { on })}$ the diode is conductive and acts as a battery $V_{D(\text { on })}=0.7 \mathrm{~V}$, as shown in Fig. 1.51b, bottom. The output now follows the input, but with an offset of -0.7 V , by KVL. Thus,
$$
\begin{equation*}
v_{O}=v_{I}-V_{D(\mathrm{on})} \quad \text { for } v_{I}>V_{D(\mathrm{on})} \tag{1.74b}
\end{equation*}
$$
Circuit behavior is illustrated further via the input and output waveforms of Fig. 1.52a, and the voltage transfer curve (VTC) of Fig. 1.52b. Compared to the ideal diode, for which $V_{D(\text { on })}=0$, a silicon diode requires about 0.7 V to turn on, and once on, it introduces an error in the form of a $-0.7-\mathrm{V}$ offset at the output. This offset may or may not be a problem, depending on the performance requirements of the application at hand. Also, a closer look at both plots reveals that the diode's transition from on to off (or vice versa) is not abrupt, as implied by our piecewise-linear approximation, but gradual, owing to the knee of the exponential curve. This feature is actually quite beneficial in the case of piecewise-linear function generators as it ensures a smoother transition from one segment to the next of the VTC.
Now that we understand how a silicon diode behaves as a half-wave rectifier, we find it easier to reexamine all other ideal-diode circuits investigated in Section 1.2, such as full-wave rectifiers, voltage clamps, piecewise-linear function generators, clamped
image_name:(a)
description:
[
name: V1, type: VoltageSource, value: 10 Vac, ports: {Np: VI, Nn: GND}
name: D1, type: Diode, value: D1N4148, ports: {Na: VI, Nc: VO}
name: R, type: Resistor, value: 1 kΩ, ports: {N1: VO, N2: GND}
]
extrainfo:This is a half-wave rectifier circuit using a 1N4148 diode. The input voltage is 10 Vac, and the output is taken across a 1 kΩ resistor. The diode conducts only when the input voltage exceeds the diode's forward voltage, allowing current to flow and creating a rectified output.
image_name:(b) top
description:
[
name: VI, type: VoltageSource, value: 10 Vac, ports: {Np: VI, Nn: GND}
name: D1, type: Diode, value: 1N4148, ports: {Na: VI, Nc: VO}
name: R, type: Resistor, value: 1 kΩ, ports: {N1: VO, N2: GND}
]
extrainfo:The circuit is a half-wave rectifier using a 1N4148 diode. When the input voltage VI is greater than the diode's forward voltage, current flows through the diode, and the output voltage VO is approximately VI minus the diode's forward voltage drop. When VI is less than the diode's forward voltage, the diode is off, and VO is zero.
image_name:(b) bottom
description:
[
name: V1, type: VoltageSource, value: 10 Vac, ports: {Np: VI, Nn: GND}
name: D1, type: Diode, value: 1N4148, ports: {Na: VI, Nc: VO}
name: R, type: Resistor, value: 1 kΩ, ports: {N1: VO, N2: GND}
]
extrainfo:The circuit is a half-wave rectifier using a 1N4148 diode. When the input voltage (VI) is greater than the diode's forward voltage (VD(on)), the diode conducts and the output voltage (VO) is equal to the input voltage minus the diode's forward voltage. When the input voltage is less than the diode's forward voltage, the diode does not conduct and the output voltage is zero.
FIGURE 1.51 Investigating a half-wave rectifier using the 1N4148 pn diode: (a) PSpice circuit, and (b) its equivalent circuits when the diode is off (top) and on (bottom).
image_name:(a)
description:The graph in Figure 1.52(a) is a time-domain waveform plot showing the input and output voltages of a half-wave rectifier circuit using a 1N4148 pn diode. The x-axis represents time in milliseconds (ms), ranging from 0 to 2 ms, while the y-axis represents voltage in volts (V), ranging from -5 V to 5 V. The graph uses a linear scale for both axes.
The input voltage \(v_I\) is depicted as a sinusoidal waveform oscillating between -5 V and 5 V with a period of 1 ms. The output voltage \(v_O\) is shown as a waveform that mirrors the positive half-cycles of the input voltage but is offset by the diode's forward voltage \(V_{D(on)}\). During the positive half-cycles, the output voltage follows the input voltage closely but is reduced by the forward voltage drop of the diode. During the negative half-cycles, the output voltage is zero, indicating that the diode is not conducting.
Key features include the point at which the diode begins to conduct, marked by \(V_{D(on)}\), and the fact that the output voltage only appears during the positive half-cycles of the input waveform. There are no annotations for specific numerical values of \(V_{D(on)}\) in this figure, but the general behavior is consistent with typical diode rectification characteristics.
image_name:(b)
description:The graph labeled as "(b)" is a Voltage Transfer Characteristic (VTC) plot for a diode in a half-wave rectifier circuit. The graph displays the relationship between the input voltage (v_I) on the x-axis and the output voltage (v_O) on the y-axis. Both axes are marked in volts (V), ranging from -5V to +5V.
The plot features two lines: an 'Ideal' line and an 'Actual' line. The 'Ideal' line represents the expected behavior without considering the diode's forward voltage drop. It starts at the origin (0,0) and follows a 45-degree angle, indicating a direct one-to-one correspondence between input and output voltages.
The 'Actual' line, however, reflects the real behavior of the diode. It remains at 0V for input voltages below the diode's forward voltage (V_D(on)), indicating no conduction. Once the input voltage exceeds V_D(on), the output voltage increases linearly but offset by the forward voltage drop, which is shown as a vertical shift between the 'Ideal' and 'Actual' lines.
This graph effectively demonstrates the diode's threshold behavior, where conduction begins only after surpassing the forward voltage, resulting in an output that trails the input by the forward voltage amount.
FIGURE 1.52 PSpice plots for the circuit of Fig. 1.51a. (a) Input and output waveforms, and (b) VTC.
capacitors, and voltage multipliers, but using real-life junction diodes instead. As an example, Fig. 1.53 depicts the full-wave rectifier. Due to the fact that we now have two diodes in series with the load, the output offset error is $2 V_{D(\text { on })}(\cong 1.4 \mathrm{~V})$.
image_name:Figure 1.53 (a)
description:
[
name: V1, type: VoltageSource, value: 10 Vac, ports: {Np: VI, Nn: GND}
name: D1, type: Diode, value: 1N4148, ports: {Na: V1, Nc: X1}
name: D2, type: Diode, value: 1N4148, ports: {Na: GND, Nc: X1}
name: D3, type: Diode, value: 1N4148, ports: {Na: X2, Nc: VI}
name: D4, type: Diode, value: 1N4148, ports: {Na: X2, Nc: GND}
name: R, type: Resistor, value: 1 kΩ, ports: {N1: X1, N2: X2}
]
extrainfo:The circuit is a full-wave rectifier using four 1N4148 diodes and a resistor. The input is an AC voltage source of 10 Vac, and the output is taken across the resistor. The diodes are arranged in a bridge configuration to rectify the input AC voltage.
(a)
image_name:(b)
description:The graph in Figure 1.53(b) is a time-domain waveform depicting both the input and output voltages of a full-wave rectifier circuit. The x-axis represents time in milliseconds (ms), ranging from 0 to 2 ms, while the y-axis represents voltage in volts (V), ranging from -10 V to 10 V.
Two waveforms are shown:
1. **Input Voltage (v_I):** This waveform is a sinusoidal AC signal with a peak amplitude of 10 V. It oscillates between +10 V and -10 V with a period of approximately 1 ms, indicating a frequency of about 1 kHz.
2. **Output Voltage (v_O):** This waveform is the rectified output of the circuit. It is a full-wave rectified signal, which means it only has positive values. The peak of the output waveform is slightly lower than the input due to the voltage drop across the diodes, which is noted as \(2V_{D(\text{on})}\) (approximately 1.4 V for silicon diodes, since \(V_{D(\text{on})}=0.7\) V for each diode in the bridge).
**Overall Behavior and Trends:**
- The input waveform is a smooth sinusoidal curve, while the output waveform shows rectification, converting the negative half-cycles of the input into positive half-cycles.
- The output waveform's peaks reach approximately 8.6 V, which is the input peak (10 V) minus the diode drop (2 x 0.7 V).
**Key Features and Technical Details:**
- The rectification process is evident as the output waveform does not go below 0 V.
- The output waveform is slightly flattened at the peaks compared to the input, which is typical in rectification due to diode conduction.
- The frequency of the output waveform is twice that of the input, reflecting the full-wave rectification process.
**Annotations and Specific Data Points:**
- The graph includes annotations for \(v_I\) and \(v_O\), clearly marking the input and output waveforms.
- A marker indicates the voltage drop across the diodes as \(2V_{D(\text{on})}\).
(b)
FIGURE 1.53 (a) PSpice circuit to simulate a full-wave rectifier using 1N4148 diodes, and (b) the input and output waveforms.
#### Exercise 1.6
a. In the following, let the diodes be silicon types with $V_{D(\text { on })}=0.7 \mathrm{~V}$. Assuming input logic levels of 0 V and 5 V in the OR gate of Fig. 1.15, find the output logic levels.
b. Repeat, but for the AND gate of Fig. 1.16.
c. Assuming $V_{S}=5 \mathrm{~V}$ in the IC circuit of Fig. 1.17, find the range of values for $v_{I C}$.
Ans. (a) 0 V and 4.3 V. (b) 0.7 V and 5 V . (c) $-0.7 \mathrm{~V} \leq v_{I C} \leq 5.7 \mathrm{~V}$.
### The Superdiode
There are applications, such as precision instrumentation, in which the rectifier's output offset of 0.7 V is unacceptable and needs to be eliminated somehow. The only way to ensure this, in the half-wave rectifier example of Fig. 1.51, is to drive the anode about 0.7 V higher than $v_{I}$ so that the voltage at the cathode will equal $v_{I}$ itself. This task is achieved by placing the diode within the negative feedback path of an operational amplifier (op amp), as depicted in the PSpice circuit of Fig. 1.54a. The relevant waveforms are displayed in Fig. 1.54b.
To analyze the circuit, recall the familiar op amp rule, stating that in negativefeedback operation an op amp will output whatever voltage $v_{O}$ it takes to force $v_{N}$ to track $v_{P}$. Consider the cases $v_{I}>0$ and $v_{I}<0$ separately.
- For $v_{I}>0$ the op amp needs to source current to $R$ in order to make the invertinginput voltage $\left(v_{O}\right)$ follow the non-inverting-input voltage $\left(v_{I}\right)$. This the op amp can readily do via the diode, whose direction conforms to that of the needed current. To turn on the diode, the op amp must swing its output $\left(v_{A}\right)$ a diode drop higher than $v_{O}$. For instance, with $v_{I}=1 \mathrm{~V}$, the op amp achieves $v_{O}=1 \mathrm{~V}$ by outputting $v_{A} \cong 1.7 \mathrm{~V}$. The situation during the positive alternations in $v_{I}$ is depicted in Fig. 1.55a.
- For $v_{I}<0$ the op amp would have to $\sin k$ current from $R$ in order to make $v_{O}$ follow $v_{I}$. But, this is impossible due to the diode's inability to conduct in the reverse direction. So, the diode goes off, in effect disconnecting $R$ from the circuit and thus give $v_{O}=0$. The situation is depicted in Fig. 1.55b. Deprived of the feedback path, the op amp can no longer influence its inverting input, so it ends up operating in the open-loop mode. As an example, consider the case $v_{I}=-1 \mathrm{~V}$, so that the voltage difference at the op amp's input is $v_{P}-v_{N}=(-1-0)=-1 \mathrm{~V}$. The op amp, in its attempt to magnify this negative input difference by the full open-loop gain, will swing its output $v_{A}$ in the negative direction as far as it will go. In fact, in this example the output saturates in the vicinity of -6 V .
- Once $v_{I}$ becomes again positive, the op amp will pull out of saturation and return to ride $v_{A}$ a diode drop higher than $v_{I}$, as already seen in Fig. 1.55a.
image_name:(a)
description:
[
name: V_I, type: VoltageSource, value: 5 Vac, ports: {Np: V_I, Nn: GND}
name: μA741, type: OpAmp, ports: {InP: V_I, InN: V_O, OutP: V_A, OutN: ', Vdd: VCC, -Vdd: VEE}
name: D, type: Diode, value: D1N4148, ports: {Na: V_A, Nc: V_O}
name: R, type: Resistor, value: 1 kΩ, ports: {N1: V_O, N2: GND'}
]
extrainfo:This circuit is a superdiode configuration using an op-amp (μA741) and a diode (D1N4148). The input voltage (V_I) is 5 Vac. The op-amp is powered by VCC (6.5 V) and VEE (-6.5 V). The output voltage (V_O) is across the resistor (R) with a value of 1 kΩ. The diode conducts when the op-amp output (V_A) is positive, allowing V_O to follow V_I.
image_name:(b)
description:The graph labeled "(b)" is a time-domain waveform plot. It shows the behavior of three signals over time: \( v_I \), \( v_A \), and \( v_O \). The x-axis represents time in milliseconds (ms), ranging from 0 to 20 ms. The y-axis represents voltage in volts (V), with values ranging from -5 V to 5 V.
Overall Behavior and Trends:
- **Input Signal \( v_I \):** This waveform is a sinusoidal signal oscillating between +5 V and -5 V. It completes a full cycle every 10 ms, indicating a frequency of 100 Hz.
- **Output Signal \( v_O \):** The output \( v_O \) follows \( v_I \) when \( v_I \) is positive, essentially acting as a half-wave rectifier. When \( v_I \) is negative, \( v_O \) remains at 0 V, indicating that the diode is off and blocking the negative half of the cycle.
- **Amplifier Output \( v_A \):** This waveform shows the op-amp output, which saturates at around -6 V when \( v_I \) is negative. When \( v_I \) becomes positive, \( v_A \) follows \( v_I \) closely, indicating that the op-amp is out of saturation and actively tracking the input.
Key Features and Technical Details:
- **Saturation:** The op-amp output \( v_A \) saturates negatively when \( v_I \) is negative, showing its limit at approximately -6 V.
- **Rectification:** The output \( v_O \) is zero when \( v_I \) is negative, demonstrating the diode's rectifying behavior.
- **Diode Behavior:** The diode conducts when \( v_I \) is positive and blocks when \( v_I \) is negative, allowing \( v_O \) to match \( v_I \) only during the positive half-cycle.
Annotations and Specific Data Points:
- **Zero Crossings:** \( v_I \) crosses zero at approximately 5 ms and 15 ms, aligning with the transitions of \( v_O \) from zero to positive.
- **Peak Values:** \( v_I \) peaks at +5 V and -5 V, while \( v_O \) peaks coincide with the positive peaks of \( v_I \).
- **Saturation Level:** \( v_A \) reaches a saturation level of about -6 V during the negative half-cycle of \( v_I \).
FIGURE 1.54 (a) Superdiode PSpice circuit, and (b) its waveforms
image_name:Figure 1.55 (a)
description:
[
name: V_I, type: VoltageSource, value: V_I, ports: {Np: V_I, Nn: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: V_I, InN: V_O, OutP: V_A, OutN: GND}
name: R, type: Resistor, value: R, ports: {N1: V_O, N2: GND}
]
extrainfo:The circuit operates as a superdiode. When v_I > 0, v_O follows v_I due to the forward bias of the diode. When v_I < 0, v_O is clamped to 0 V. The op-amp output v_A reaches approximately -6 V during the negative half-cycle of v_I.
image_name:Figure 1.55 (b)
description:
[
name: V_I, type: VoltageSource, value: V_I, ports: {Np: V_I, Nn: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: V_I, InN: V_O, OutP: V_A}
name: R, type: Resistor, value: R, ports: {N1: V_O, N2: GND}
]
extrainfo:The circuit represents a superdiode configuration with an op-amp. When the input voltage V_I is negative, the output voltage V_O is zero, and the op-amp output V_A saturates at approximately -6 V.
FIGURE 1.55 Equivalent circuits of the superdiode circuit when the diode is (a) on and (b) off.
## 1.11 Ac ANALYSIS OF pn DIODE CIRCUITS
The piecewise-linear approximation of Fig. 1.50 encompasses the entire $i-v$ characteristic of the $p n$ diode. There is another important form of linearization in use, but involving only a limited portion of the forward-region characteristic. As we know, this characteristic is exponential and thus a highly nonlinear curve. However, if we restrict the diode's operation within a sufficiently small portion of this curve, as highlighted in Fig. 1.56a, then we can approximate this portion with a straight segment and thus apply familiar linear-circuit analysis techniques. This alternative form of linearization, aptly called small-signal approximation and depicted in expanded form in Fig. 1.56b, relies on two premises:
- First, we bias the diode at a suitable operating point $Q_{0}=Q_{0}\left(I_{D}, V_{D}\right)$ up the diode curve, in effect establishing the origin of a new system of $i$-v axes for signal variations about this point.
- Then, we vary the diode's operating point up and down the curve by amounts denoted as $i_{d}$ and $v_{d}$, keeping $i_{d}$ and $v_{d}$ sufficiently small so as to ensure that $i_{d} i s$ linearly proportional to $v_{d}$, just as in the case of ordinary resistance.
To simplify the bookkeeping, engineers have developed a special form of signal notation ${ }^{7}$ that has proved quite convenient not only for diodes, but also for other
image_name:(a)
description:The graph labeled "(a)" illustrates the small-signal operation of a pn diode, focusing on the relationship between the diode current and voltage. This is a two-dimensional plot with the horizontal axis labeled as \( v_D \), representing the diode voltage, and the vertical axis labeled as \( i_D \), representing the diode current. Both axes start at zero and increase positively.
1. **Type of Graph and Function:**
- The graph is a characteristic curve of a pn diode, showing the nonlinear relationship between the diode current (\( i_D \)) and voltage (\( v_D \)).
2. **Axes Labels and Units:**
- **Horizontal Axis (x-axis):** \( v_D \), diode voltage.
- **Vertical Axis (y-axis):** \( i_D \), diode current.
3. **Overall Behavior and Trends:**
- The curve starts at the origin (0,0) and exhibits an exponential increase, typical of a diode's I-V characteristic. This indicates that as the voltage increases, the current increases exponentially after a certain threshold.
4. **Key Features and Technical Details:**
- The point \( Q_0 \) is marked on the curve, representing the quiescent or operating point of the diode. This is where the diode is biased in its normal operating region.
- Around \( Q_0 \), small variations are shown as \( i_d \) (current variation) and \( v_d \) (voltage variation), indicating the linear approximation of the diode's behavior in this region. This linear approximation is valid for small signals around the quiescent point, allowing the diode to be treated like a resistor.
5. **Annotations and Specific Data Points:**
- The graph highlights the small-signal model by showing \( i_d \) and \( v_d \) as small deviations from the quiescent point \( Q_0 \). These deviations are sufficiently small to ensure linearity, making \( i_d \) proportional to \( v_d \).
This graph effectively illustrates how the diode behaves under small-signal conditions, emphasizing the linear relationship that can be used for analysis in this specific region of operation.
image_name:(b)
description:The graph in Figure 1.56 (b) illustrates the small-signal operation of a pn diode by expanding on the diode's I-V characteristic curve. This is a plot showing the relationship between the diode current (i_D) and the diode voltage (v_D), with a focus on small-signal variations around a specific operating point.
1. **Type of Graph and Function:**
- This is a linearized segment of a diode's I-V characteristic curve, specifically illustrating small-signal behavior. It is not a frequency-domain plot but a time-domain representation focusing on small-signal increments.
2. **Axes Labels and Units:**
- The x-axis represents the diode voltage \( v_D \), with units typically in volts.
- The y-axis represents the diode current \( i_D \), with units typically in amperes.
- Both axes are marked linearly, and the diagram expands around a specific operating point \( Q_0 \).
3. **Overall Behavior and Trends:**
- The graph shows a linear approximation of the diode's behavior around the operating point \( Q_0 \), where \( I_D \) and \( V_D \) are the DC operating current and voltage, respectively.
- Small deviations \( i_d \) and \( v_d \) are added to \( I_D \) and \( V_D \) to show how the diode responds to small variations in voltage and current.
- The tangent line at \( Q_0 \) represents the linear approximation, indicating the small-signal resistance \( r_d \).
4. **Key Features and Technical Details:**
- The point \( Q_0 \) is the quiescent operating point, with coordinates \( (V_D, I_D) \).
- The tangent line's slope at \( Q_0 \) is \( 1/r_d \), where \( r_d \) is the small-signal resistance.
- The graph shows the linear response of the diode to small perturbations, with \( Q_1 \) representing a new point after a small increase in both voltage and current.
5. **Annotations and Specific Data Points:**
- The graph is annotated with the operating point \( Q_0 \), the tangent line, and the small-signal increments \( v_d \) and \( i_d \).
- The points \( I_D + i_d \) and \( V_D + v_d \) are marked to show the effect of small-signal changes on the diode's operation.
This graph is essential for understanding the linear approximation of a diode's behavior in small-signal analysis, allowing for simplified calculations in circuit design involving diodes.
FIGURE 1.56 (a) Illustrating the small-signal operation of a pn diode. (b) Expanded view.
image_name:Figure 1.57
description:The graph in Figure 1.57 illustrates the decomposition of a signal into its DC and AC components, specifically for the voltage across a pn diode. This is a time-domain waveform representation, showing how the total voltage \( v_D \) is the sum of a DC component \( V_D \) and an AC component \( v_d \).
1. **Type of Graph and Function:**
- The graph is a time-domain waveform illustrating the decomposition of a voltage signal into DC and AC components.
2. **Axes Labels and Units:**
- The horizontal axis represents time \( t \) with no specific units marked, suggesting a general representation.
- The vertical axis represents voltage. The leftmost graph shows \( v_D \), the middle graph shows \( V_D \), and the rightmost graph shows \( v_d \).
3. **Overall Behavior and Trends:**
- The leftmost graph shows a sinusoidal waveform representing \( v_D \), indicating a periodic voltage over time.
- The middle graph shows a constant line at \( V_D \), indicating a steady DC voltage component.
- The rightmost graph shows a sinusoidal waveform similar to the leftmost graph, representing the AC component \( v_d \).
4. **Key Features and Technical Details:**
- The sinusoidal waveforms in the leftmost and rightmost graphs suggest a consistent amplitude and frequency, typical of AC signals.
- The middle graph’s constant line at \( V_D \) indicates no variation over time, characteristic of a DC component.
5. **Annotations and Specific Data Points:**
- The graph effectively demonstrates the relationship \( v_D = V_D + v_d \), visually breaking down the total voltage into its components.
- There are no specific numerical values or annotations provided, emphasizing the conceptual demonstration of signal decomposition.
FIGURE 1.57 Illustrating the decomposition of a signal into its $d c$ and ac components, or $v_{D}=V_{D}+v_{d}$.
nonlinear devices like transistors, as we shall see. By this notation, the voltage and current of the pn diode are expressed in the form
$$
\begin{gather*}
v_{D}=V_{D}+v_{d}  \tag{1.75a}\\
i_{D}=I_{D}+i_{d} \tag{1.75b}
\end{gather*}
$$
where:
- $v_{D}$ and $i_{D}$ are referred to as the total signals (lower-case symbols with upper-case subscripts)
- $V_{D}$ and $I_{D}$ are their $d c$ components (upper-case symbols with upper-case subscripts)
- $v_{d}$ and $i_{d}$ are their ac components (lower-case symbols with lower-case subscripts)
This form of signal decomposition is illustrated in Fig. 1.57 for the case of the voltage $v_{D}$, but a similar picture holds also the current $i_{D}$.
Figure 1.58 shows two sets of waveforms obtained via PSpice simulation. The diode used is such that with $V_{D}=700 \mathrm{mV}$ it gives exactly $I_{D}=1.0 \mathrm{~mA}$. Moreover, to make it easier for the naked eye to observe any distortion, we have chosen a triangular waveform for the ac voltage component. We make the following observations:
- In Fig. 1.58a the diode is subjected to an ac voltage component (top) having peak values of $\pm 5 \mathrm{mV}$, and it responds with a current waveform (bottom) that is only slightly distorted. In a truly undistorted waveform, the positive and negative portions are mirror images of each other. In the example shown the positive portion is slightly bigger than the negative one because of the curvature of the diode's $i-v$ characteristic. Even so, we can state that distortion is reasonably low.
- In Fig. 1.58 b the ac voltage (top) has been raised to peak values of $\pm 18 \mathrm{mV}$, and the current response (bottom) is now highly distorted. The reason for choosing 18 mV is that we can figure out the peak values of current using one of the rules of thumb. Namely, with $v_{D}=(700+18) \mathrm{mV}, i_{D}$ doubles from 1.0 mA to 2.0 mA , whereas with $v_{D}=(700-18) \mathrm{mV}, i_{D}$ halves from 1.0 mA to 0.5 mA . For the current waveform to be undistorted, the positive peak should equal the negative peak, so it should be $1.0+0.5=1.5 \mathrm{~mA}$, not 2.0 mA . The pronounced distortion stems from the fact that the increased ac voltage drive causes the operating point to span a wider portion of the exponential curve. As seen, the negative portions of the waveforms get compressed, and the positive portions get expanded.
image_name:(a)
description:The graph labeled (a) in Figure 1.58 consists of two main plots: the top plot shows the diode voltage waveform, and the bottom plot shows the diode current waveform. Both plots are time-domain waveforms, with time on the x-axis ranging from 0 to 2 milliseconds (ms).
**Top Plot - Diode Voltage:**
- **Y-Axis:** Diode Voltage in millivolts (mV), ranging from 680 mV to 720 mV.
- **Behavior:** The waveform is a triangular wave with peaks at approximately 710 mV and valleys at around 690 mV. The waveform is periodic with a period of 1 ms, indicating a frequency of 1 kHz.
- **Trend:** The waveform is fairly linear, with symmetrical rise and fall times, suggesting a linear response under the given conditions.
**Bottom Plot - Diode Current:**
- **Y-Axis:** Diode Current in milliamperes (mA), ranging from 0.5 mA to 1.5 mA.
- **Behavior:** The waveform is also triangular with peaks at about 1.0 mA and valleys at around 0.5 mA. Like the voltage waveform, it is periodic with a period of 1 ms.
- **Trend:** The current waveform shows a consistent linear pattern, indicating that the diode operates close to linearity under these conditions.
**Key Features:**
- Both voltage and current waveforms maintain a consistent shape and amplitude over time, implying minimal distortion.
- The linearity in both waveforms suggests that the diode is operating within a range where the small-signal approximation is valid.
image_name:(b)
description:The graph labeled (b) consists of two subplots depicting diode voltage and diode current waveforms over time.
### Type of Graph and Function
- **Graph Type:** Time-domain waveform
- **Function:** Diode voltage and current response to an AC voltage drive
Axes Labels and Units
- **Top Graph (Diode Voltage):**
- **Y-axis:** Diode Voltage (mV), ranging from 680 mV to 720 mV
- **X-axis:** Time (ms), ranging from 0 to 2 ms
- **Bottom Graph (Diode Current):**
- **Y-axis:** Diode Current (mA), ranging from 0.5 mA to 2.0 mA
- **X-axis:** Time (ms), ranging from 0 to 2 ms
Overall Behavior and Trends
- **Diode Voltage (Top Graph):**
- The waveform is triangular, indicating a linear increase and decrease in voltage over each cycle.
- Peaks at approximately 715 mV and valleys at about 685 mV.
- The waveform is periodic with a period of approximately 1 ms.
- **Diode Current (Bottom Graph):**
- The waveform is also triangular, mirroring the voltage waveform.
- Peaks at 2.0 mA and valleys at 0.5 mA.
- The periodicity matches the voltage waveform, with a period of approximately 1 ms.
Key Features and Technical Details
- **Voltage Peaks and Valleys:**
- Maximum voltage is slightly above 710 mV.
- Minimum voltage is slightly below 690 mV.
- **Current Peaks and Valleys:**
- Maximum current reaches 2.0 mA.
- Minimum current drops to 0.5 mA.
- The waveforms demonstrate distortion, as the current waveform's positive peak is higher than the negative, indicating non-linear behavior under this drive condition.
Annotations and Specific Data Points
- The graph effectively illustrates the non-linear response of the diode under a large AC voltage drive. The current waveform's asymmetry highlights the distortion discussed in the context, where the positive peak is exaggerated compared to the negative peak.
This graph demonstrates the impact of increased AC voltage drive on diode behavior, illustrating significant waveform distortion, especially in the current response.
FIGURE 1.58 Voltage waveforms (top) and current waveforms (bottom) for two different ac voltage drives.
It is apparent that under the voltage drive conditions of Fig. 1.58a diode behavior can be regarded fairly close to linear, but that under the conditions of Fig. 1.58 b it can't. Next, we wish to investigate quantitatively the range of validity of the small-signal approximation.
### Small-Signal Operation
As we know, the function of the dc source $V_{D}$ in Fig. 1.59a is to bias the diode at a specific quiescent point $Q_{0}=Q_{0}\left(I_{D}, V_{D}\right)$ up the diode curve. Assuming an emission coefficient of unity $(n=1)$ for simplicity, the corresponding dc current is
$$
I_{D}=I_{S} e^{V_{D} / V_{T}}
$$
If we now turn on the $a c$ source $v_{d}$ as in Fig. 1.59b, the operating point will move up and down the diode curve, yielding the ac current $i_{d}$. In the expanded view of Fig. $1.56 b$
image_name:(a)
description:
[
name: VD, type: VoltageSource, value: VD, ports: {Np: VD, Nn: GND}
name: D1, type: Diode, ports: {Na: VD, Nc: GND}
]
extrainfo:The circuit represents a DC biasing setup for a diode with a voltage source VD providing the necessary bias to set the diode at a specific quiescent point. The current ID flows through the diode.
image_name:(b)
description:
[
name: Vd, type: VoltageSource, value: Vd, ports: {Np: Vd, Nn: GND}
name: Diode, type: Diode, ports: {Na: Vd, Nc: GND}
name: vd, type: VoltageSource, value: vd, ports: {Np: Vd, Nn: GND}
name: Diode, type: Diode, ports: {Na: Vd, Nc: GND}
]
extrainfo:The circuit diagram (b) represents a diode biased by a DC source VD and an AC source vd, allowing the diode's operating point to move along its curve. The diode conducts a combined DC and AC current.
image_name:(c)
description:
[
name: vd, type: VoltageSource, value: vd, ports: {Np: vd, Nn: GND}
name: Diode, type: Diode, ports: {Na: vd, Nc: GND}
]
extrainfo:This is a small-signal model of a diode circuit with an AC voltage source. The AC source 'vd' is connected in series with the diode, and the circuit is grounded at one end.
FIGURE 1.59 Systematic analysis of small-signal diode operation. The actual circuit is shown in the center (b), while (a) shows its large-signal or dc version, and (c) shows its small-signal or ac version.
we have captured a positive alternation of $v_{d}$, during which the diode's instantaneous operating point is $Q_{1}=Q_{1}\left(I_{D}+i_{d}, V_{D}+v_{d}\right)$. The diode equation gives, at $Q_{1}$,
$$
I_{D}+i_{d}=I_{s} e^{\left(V_{D}+v_{d}\right) / V_{T}}=\left(I_{s} e^{V_{D} / V_{T}}\right) e^{v_{d} / V_{T}}=I_{D} e^{v_{d} / V_{T}}
$$
or
$$
\begin{equation*}
i_{d}=I_{D}\left(e^{v_{d} / V_{T}}-1\right) \tag{1.76}
\end{equation*}
$$
Performing a series expansion of the exponential term gives
$$
i_{d}=I_{D}\left[\chi+\frac{v_{d}}{V_{T}}+\frac{1}{2!}\left(\frac{v_{d}}{V_{T}}\right)^{2}+\frac{1}{3!}\left(\frac{v_{d}}{V_{T}}\right)^{3}+\cdots-\chi\right]
$$
or
$$
\begin{equation*}
i_{d}=\frac{I_{D}}{V_{T}} v_{d}\left(1+\frac{v_{d}}{2 V_{T}}+\cdots\right) \tag{1.77}
\end{equation*}
$$
This equation indicates a nonlinear relationship between $i_{d}$ and $v_{d}$. This is not surprising, given the exponential and thus highly nonlinear characteristic of the diode. However, if we stipulate to keep the magnitude of $v_{d}$ sufficiently small, then the quadratic and higher-order terms in $v_{d}$ can be ignored, allowing us to work with a linear and thus simpler relationship. Specifically, if we stipulate to keep
$$
\begin{equation*}
\left|v_{d}\right| \ll 2 V_{T}(\cong 52 \mathrm{mV}) \tag{1.78}
\end{equation*}
$$
then Eq. (1.77) simplifies as $i_{d}=\left(I_{D} / V_{T}\right) v_{d}$. This can be put in the form of Ohm's law,
$$
\begin{equation*}
i_{d}=\frac{v_{d}}{r_{d}} \tag{1.79}
\end{equation*}
$$
where
$$
\begin{equation*}
r_{d}=\frac{V_{T}}{I_{D}} \tag{1.80}
\end{equation*}
$$
is the diode's dynamic resistance. Its reciprocal $1 / r_{d}$ is simply the slope of the diode curve calculated at the quiescent point $Q_{0}$. With reference to Fig. $1.56 b$ we see that if $v_{d}$ is sufficiently small, the portion of the curve from $Q_{0}$ to $Q_{1}$ can be approximated with the straight segment tangent to the diode curve right at $Q_{0}$. For obvious reasons the ac variations $v_{d}$ and $i_{d}$ are referred to as small signals. By contrast, $V_{D}$ and $I_{D}$ are referred to as large signals. Equation (1.79) is referred to as the small-signal approximation, and Eq. (1.78) quantifies the validity of this approximation.
Ignoring higher-order terms in Eq. (1.77), we estimate the error $\varepsilon$ incurred in the small-signal approximation as
$$
\begin{equation*}
\varepsilon \cong \frac{v_{b e}}{2 V_{T}} \cong \frac{v_{b e}}{52 \mathrm{mV}} \tag{1.81}
\end{equation*}
$$
This amounts to about $2 \%$ for every 1-mV of $v_{b e}$. Thus, if we wish to keep $\varepsilon$ below $10 \%$ (an acceptable error in most practical situations), then we need to ensure that
$$
\begin{equation*}
\left|v_{b e}\right| \leq 5 \mathrm{mV} \tag{1.82}
\end{equation*}
$$
This shall be our working condition, as we move along.
(a) If $I_{D}=1 \mathrm{~mA}$, find the peak values of $i_{d}$ in Fig. $1.58 a$, where $v_{d}$ has peak values of $\pm 5 \mathrm{mV}$. Calculate the peaks approximately, via Eq. (1.79), and exactly, via Eq. (1.76). What is the percentage error incurred in the smallsignal approximation?
(b) Repeat, but for the case of Fig. $1.58 b$, where $v_{d}$ has peak values of $\pm 18 \mathrm{mV}$.
#### Solution
(a) By Eq. (1.80), $r_{d}=26 / 1=26 \Omega$. By Eq. (1.79), $i_{d}$ peaks at the values
$$
i_{d(\mathrm{pk})}=\frac{ \pm 5 \times 10^{-3}}{26} \cong \pm 192 \mu \mathrm{~A}
$$
By Eq. (1.76), the exact values of the positive and negative peaks of $i_{d}$ are, respectively,
$$
i_{d(\mathrm{pospk})}=10^{-3}\left(e^{5 / 26}-1\right)=212 \mu \mathrm{~A} \quad i_{d(\mathrm{neg} \mathrm{pk})}=10^{-3}\left(e^{-5 / 26}-1\right)=-175 \mu \mathrm{~A}
$$
We see that the small-signal approximation underestimates the positive peak by $(212-192) / 192$, or $10.3 \%$, and overestimates the negative peak by (192 - 175)/192, or $8.9 \%$. Both errors are consistent with Eq. (1.81) which predicts errors of approximately $\pm 5 / 52= \pm 9.6 \%$.
(b) Now Eq. (1.79) predicts
$$
i_{d(\mathrm{pk})}=\frac{ \pm 18 \times 10^{-3}}{26} \cong \pm 692 \mu \mathrm{~A}
$$
Using Eq. (1.76), or more simply the rule of thumb, we find the exact peak values to be $i_{d(\mathrm{pos} \mathrm{pk})}=1000 \mu \mathrm{~A}$ and $i_{d(\mathrm{neg} \mathrm{pk})}=-500 \mu \mathrm{~A}$. The underestimation error is now $31 \%$ and the overestimation error is $38 \%$, both of which are generally unacceptable. The far more pronounced distortion of Fig. $1.58 b$ confirms this.
Remark: The above results, derived for the case of an emission coefficient $n=1$, are readily generalized if we let $V_{T} \rightarrow n V_{T}$ in Eqs. (1.78), (1.80), and (1.81), and let $5 \mathrm{mV} \rightarrow n 5 \mathrm{mV}$ in Eq. (1.82). For example, for $n=1.5$, Eq. (1.78) becomes $\left|v_{d}\right| \ll 2 \times 1.5 V_{T}\left(\cong 78 \mathrm{mV}\right.$ ), and Eq. (1.82) becomes $\left|v_{d}\right| \leq 7.5 \mathrm{mV}$.
### The Small-Signal Diode Model
Equations (1.79) and (1.80) indicate that, under the condition of Eq. (1.78), a pn diode behaves with respect to the small signals $v_{d}$ and $i_{d}$ as a mere resistor $r_{d}$. The smallsignal model for the diode, also called incremental model, is shown in Fig. 1.60 (right).
image_name:Large-signal model
description:
[
name: VD(on), type: VoltageSource, value: VD(on), ports: {Np: A, Nn: C}
name: ID, type: CurrentSource, value: ID, ports: {Np: A, Nn: C}
name: Diode1, type: Diode, ports: {Na: A, Nc: C}
name: rd, type: Resistor, value: rd, ports: {N1: A, N2: B}
]
extrainfo:The diagram shows the large-signal model on the left and the small-signal model on the right for a pn diode. In the large-signal model, the diode is represented with a voltage source VD(on) and a current source ID. In the small-signal model, the diode behaves as a resistor rd with voltage vd and current id.
image_name:Small-signal model
description:
[
name: VD(on), type: VoltageSource, value: VD(on), ports: {Np: A, Nn: C}
name: ID, type: CurrentSource, value: ID, ports: {Np: A, Nn: C}
name: Diode, type: Diode, ports: {Na: A, Nc: C}
name: rd, type: Resistor, value: rd, ports: {N1: A, N2: B}
]
extrainfo:The diagram illustrates the transition from a large-signal model to a small-signal model for a pn diode. The large-signal model (left) includes a voltage source VD(on) and a current source ID. The small-signal model (right) simplifies the diode to a resistor rd with voltage vd and current id.
FIGURE 1.60 Large-signal model (left) and small-signal model (right) of the pn diode.
For convenience, also shown is the large-signal model (left). The beginner should be careful not to confuse the two! We use the large-signal model to investigate $d c$ biasing, for instance to find the quiescent current $I_{D}$. We use the small-signal model to investigate the diode's response to ac signals of suitably small magnitude.
The decomposition of the diode voltage and current into separate dc and ac components, along with the fact that both the large-signal and the small-signal diode models are linear, allows us to perform the dc and ac analyses separately, as pictured in Fig. 1.59a and 1.59c. We then apply the superposition principle and add the $d c$ and $a c$ results to obtain the total result. An example will better illustrate.
EXAMPLE 1.18 Let the diode of Fig. 1.61 have $I_{s}=1 \mathrm{fA}$ and $n=1$. Find $v_{D}=V_{D}+v_{d}$ if $v_{S}=V_{S}+v_{s}=8 \mathrm{~V}+(1 \mathrm{~V}) \sin \omega t$. Is the condition of Eq. (1.82) satisfied?
image_name:Figure 1.61
description:
[
name: VS, type: VoltageSource, value: 8 + 1 sin ωt V, ports: {Np: VS, Nn: GND}
name: R, type: Resistor, value: 10 kΩ, ports: {N1: VS, N2: VD}
name: VD, type: Diode, ports: {Na: VD, Nc: GND}
]
extrainfo:The circuit consists of a voltage source VS, a resistor R, and a diode VD connected in series. The voltage source provides a DC voltage of 8V with an AC component of 1V sin(ωt). The resistor has a resistance of 10 kΩ. The diode is connected such that its anode is at VD and its cathode is grounded.
FIGURE 1.61 Circuit of Example 1.18.
#### Solution
Perform the dc and ac analyses separately to find, respectively, $V_{D}$ and $v_{d}$. Then, apply the superposition principle to obtain $v_{D}=V_{D}+v_{d}$.
- For $d c$ analysis refer to the dc version of Fig. 1.62a, showing only the $d c$ components $V_{S}$ and $I_{D}$. The ac components ( $v_{s}$ and $v_{d}$ ) have deliberately been set to zero as they don't intervene in dc analysis. Moreover, the diode has been replaced by its large-signal model (the battery $V_{D(\text { on })}$ ). We have
$$
\begin{aligned}
I_{D} & =\frac{V_{S}-V_{D(\mathrm{on})}}{R}=\frac{8-0.7}{10}=0.73 \mathrm{~mA} \\
V_{D} & =V_{T} \ln \frac{I_{D}}{I_{\mathrm{s}}}=26 \ln \frac{0.73 \times 10^{-3}}{10^{-15}}=710 \mathrm{mV}
\end{aligned}
$$
image_name:(a)
description:
[
name: VS, type: VoltageSource, value: 8V, ports: {Np: VS, Nn: GND}
name: R, type: Resistor, value: 10kΩ, ports: {N1: VS, N2: VD(on)}
name: VD(on), type: VoltageSource, value: 0.7V, ports: {Np: VD(on), Nn: GND}
]
extrainfo:The circuit diagram (a) represents a DC analysis with a voltage source VS of 8V, a resistor R of 10kΩ, and a diode represented as a voltage source VD(on) of 0.7V. The current ID flows from VS through R to VD(on) and then to ground.
image_name:(b)
description:
[
name: vs, type: VoltageSource, value: (1V)sinωt, ports: {Np: Vs, Nn: GND}
name: R, type: Resistor, value: 10kΩ, ports: {N1: Vs, N2: Vd}
name: rd, type: Resistor, ports: {N1: Vd, N2: GND}
]
extrainfo:The circuit is an AC equivalent model with a sinusoidal input voltage source vs, a resistor R, and an incremental resistance rd representing the diode's small-signal model.
FIGURE 1.62 (a) Dc and (b) ac equivalents of the circuit of Fig. 1.61.
- For ac analysis refer to the ac version of Fig. 1.62b, showing only the ac components $v_{s}$ and $v_{d}$. The dc components $\left(V_{S}, I_{D}, V_{D}\right.$ ) have deliberately been set to zero in this case. Moreover, the diode has been replaced by its small-signal model (the incremental resistance $r_{d}$ ). We easily find
$$
\begin{aligned}
& r_{d}=\frac{V_{T}}{I_{D}}=\frac{26}{0.73} \cong 36 \Omega \\
& v_{d}=\frac{r_{d}}{R+r_{d}} v_{s}=\frac{36}{10,000+36}(1 \mathrm{~V}) \sin \omega t \cong(3.6 \mathrm{mV}) \sin \omega t
\end{aligned}
$$
Since $3.6 \mathrm{mV}<5 \mathrm{mV} \ll 2 V_{T}(\cong 52 \mathrm{mV}$ ), the error of our approximate ac calculations is less than $10 \%$.
- Finally, applying the superposition principle, we find the total diode voltage as
$$
v_{D}=(710+3.6 \sin \omega t) \mathrm{mV}
$$
#### Exercise 1.7
Repeat Example 1.18 if a $6-\mathrm{k} \Omega$ resistance is connected in parallel with the diode.
Hint: Apply Thévenin Theorem to the circuit external to the diode.
Ans. $v_{D}=(706+4.2 \sin \omega t) \mathrm{mV}$.
### The pn Diode as a Current-Controlled Resistance
The relation $r_{d}=V_{T} / I_{D}$ indicates that in small-signal operation a $p n$ diode acts as a variable resistance whose value can be programmed via the bias current $I_{D}$. If we make $r_{d}$ part of a voltage divider, then we can achieve current-controlled attenuation. Alternatively, making it part of the feedback network of an op amp, we can achieve current-controlled amplification. These concepts find application, among others, in automatic gain control (AGC), where one circuit controls the gain of another circuit.
Figure $1.63 b$ shows a current-controlled attenuator. Current control is provided by the source $I_{D}$, which also causes the diode to develop the voltage drop $V_{D}=$ $V_{T} \ln \left(I_{D} / I_{s}\right)$. To prevent the signal source $v_{i}$ from disturbing the dc bias conditions of the diode, we interpose an ac-coupling capacitor $C$, as shown.
image_name:(a)
description:
[
name: VD, type: VoltageSource, value: VD, ports: {Np: VD, Nn: GND}
name: ID, type: CurrentSource, value: ID, ports: {Np: VD, Nn: GND}
]
extrainfo:The circuit diagram (a) shows a current-controlled attenuator using a diode and a current source. The voltage source VD and current source ID are connected in parallel with the diode. The ground node is shared among these components.
image_name:(b)
description:
[
name: vi, type: VoltageSource, value: vi, ports: {Np: Vi, Nn: GND}
name: C, type: Capacitor, value: C, ports: {Np: Vi, Nn: RC}
name: R, type: Resistor, value: R, ports: {N1: RC, N2: Vo}
name: vo, type: VoltageSource, value: vo, ports: {Np: Vo, Nn: GND}
name: ID, type: CurrentSource, value: ID, ports: {Np: Vo, Nn: GND}
name: D, type: Diode, ports: {Na: Vo, Nc: GND}
]
extrainfo:The circuit is a current-controlled attenuator. The current source ID controls the diode, which affects the voltage drop across it. An AC-coupling capacitor C is used to isolate the DC bias.
image_name:(c)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: Vi, N2: Vo}
name: rd, type: Resistor, value: rd, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit diagram (c) is a simple resistive network with a voltage source Vi, a resistor R, and a diode rd. The output voltage Vo is taken across the diode rd, and the circuit is grounded at one point.
FIGURE 1.63 (b) Current-controlled attenuator and its (a) $d c$ and (c) ac equivalents.
We make the following observations about the capacitor:
- At dc, $C$ draws zero current and thus acts as an open circuit. In fact, in the dc equivalent of Fig. 1.63a, $C$ has been omitted altogether.
- When power is applied to the circuit, $C$ will charge up until its plates attain the open-circuit dc voltages of the corresponding nodes. So, the left plate remains at $0-\mathrm{V} \mathrm{dc}$, the right plate charges to $V_{D}$.
- $C$ is chosen sufficiently large to ensure that its impedance is negligible compared to $R$, in effect acting as an ac short. This requires that $1 /(\omega C) \ll R$, or $C \gg 1 /(\omega R)$, where $\omega$ is the input signal frequency.
To develop the ac equivalent of our circuit we replace $C$ by a short circuit and the diode by the variable resistance $r_{d}$. The result is shown in Fig. $1.63 c$, where $I_{D}$ has been omitted altogether as it is a dc quantity, thus having a zero ac component. Applying the voltage divider rule, we get
$$
v_{o}=\frac{r_{d}}{R+r_{d}} v_{i}=\frac{V_{T} / I_{D}}{R+V_{T} / I_{D}} v_{i}=\frac{1}{1+\left(R / V_{T}\right) I_{D}} v_{i}
$$
indicating that the gain of the circuit is
$$
\begin{equation*}
\frac{v_{o}}{v_{i}}=\frac{1}{1+\left(R / V_{T}\right) I_{D}} \tag{1.83}
\end{equation*}
$$
EXAMPLE 1.19 In the circuit of Fig. 1.63 b let
$$
v_{i}=(5 \mathrm{mV}) \cos 10^{6} t
$$
and let $I_{D}$ be variable over the range
$$
(10 \mu \mathrm{~A}) \leq I_{D} \leq(1 \mathrm{~mA})
$$
(a) Specify suitable values for $R$ and $C$ so that for $I_{D}=100 \mu \mathrm{~A}$ the gain is $0.5 \mathrm{~V} / \mathrm{V}$.
(b) If $I_{s}=2 \mathrm{fA}$, show all node voltages ( dc as well as ac components) in the circuit of part (a).
(c) Plot the gain $v_{o} / v_{i}$ versus $I_{D}$ over the specified range of $I_{D}$ values. What are the values of gain and $V_{D}$ at the extremes of the range?
#### Solution
(a) At $I_{D}=100 \mu \mathrm{~A}$ we have $r_{d}=(26 \mathrm{mV}) /(100 \mu \mathrm{~A})=260 \Omega$. For a gain of $0.5 \mathrm{~V} / \mathrm{V}$, use $R=260 \Omega$. Moreover, use $C \gg 1 /(\omega R)=1 /\left(10^{6} \times 260\right)=$ 3.8 nF . For instance, pick $C=0.1 \mu \mathrm{~F}$.
(b) The voltage drop across the diode is $V_{D}=V_{T} \ln \left(I_{D} / I_{s}\right)=0.026 \ln \left[10^{-4} /(2 \times\right.$ $\left.\left.10^{-15}\right)\right] \cong 640 \mathrm{mV}$, so the node voltages are as shown in Fig. 1.64a.
(c) With the given component values, Eq. (1.83) gives
$$
\frac{v_{o}}{v_{i}}=\frac{1}{1+10^{4} I_{D}}
$$
image_name:Figure 1.64 (a)
description:
[
name: V1, type: VoltageSource, value: 5mV, ports: {Np: Vin, Nn: GND}
name: C, type: Capacitor, value: 0.1uF, ports: {Np: Vin, Nn: Vc}
name: Rc, type: Resistor, value: 260Ω, ports: {N1: Vc, N2: X1}
name: D, type: Diode, ports: {Na: X1, Nc: GND}
name: Is, type: CurrentSource, value: 100uA, ports: {Np: X1, Nn: GND}
]
extrainfo:The circuit is a diode-based configuration with a voltage source and a current source. The capacitor and resistor form an RC filter. The diode is forward-biased by the current source.
image_name:Figure 1.64 (b)
description:The graph in Figure 1.64(b) is a plot of the gain \( v_o/v_i \) versus the programming current \( I_D \). It is a logarithmic plot on the horizontal axis, which represents the programming current \( I_D \) in microamperes (\( \mu A \)), ranging from 10 to 1000 \( \mu A \). The vertical axis represents the gain \( v_o/v_i \) in volts per volt (V/V) and is linearly scaled from 0 to 1.
**Overall Behavior and Trends:**
The graph shows a decreasing trend of gain as the programming current \( I_D \) increases. At lower values of \( I_D \), the gain is close to 1, indicating minimal attenuation. As \( I_D \) increases, the gain decreases, showing significant attenuation at higher currents.
**Key Features and Technical Details:**
- The curve starts near a gain of 1 V/V when \( I_D \) is around 10 \( \mu A \).
- The gain decreases steadily as \( I_D \) increases, reaching approximately 0.5 V/V at around 100 \( \mu A \).
- At \( I_D \) of 1000 \( \mu A \), the gain approaches 0 V/V, indicating very high attenuation.
**Annotations and Specific Data Points:**
- The graph includes gridlines at the 0.5 gain level and at \( I_D \) values of 10, 100, and 1000 \( \mu A \), marking significant points along the curve.
- The curve is smooth, with no abrupt changes or discontinuities.
FIGURE 1.64 (a) Circuit of Example 10.3 at $I_{D}=100 \mu \mathrm{~A}$, and (b) the range of variability of its gain.
whose plot is shown in Fig. 1.64b. At $I_{D}=10 \mu \mathrm{~A}$ this gives $v_{o} / v_{i}=$ $0.91 \mathrm{~V} / \mathrm{V}$. Moreover, by the rule of thumb, $V_{D}=640-60=580 \mathrm{mV}$. Similarly, at $I_{D}=1 \mathrm{~mA}$ we get $v_{o} / v_{i}=0.091 \mathrm{~V} / \mathrm{V}$ and $V_{D}=700 \mathrm{mV}$.
Figure 1.65a shows how a pn diode can be used in connection with an op amp to implement a current-controlled amplifier. As in the case of the controlled attenuator, the source $I_{D}$ programs the value of $r_{d}$, and the capacitor is used to block the dc voltage component $V_{D}$ developed by the diode. The ac equivalent, shown in Fig. 1.65b, reveals the familiar noninverting op amp configuration, whose gain is
$$
\begin{equation*}
\frac{v_{o}}{v_{i}}=1+\frac{R}{r_{d}}=1+\frac{R}{V_{T}} I_{D} \tag{1.84}
\end{equation*}
$$
In this case the impedance provided by $C$ must be negligible compared to $r_{d}$ over the entire range of $r_{d}$ values. This condition is hardest to satisfy when $r_{d}$ is minimized, so we must have $C \gg 1 /\left[\omega r_{d(\min )}\right]$.
image_name:Figure 1.65 (a)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: Vi, InN: InN(A1), OutP: Vo}
name: R, type: Resistor, value: R, ports: {N1: Vo, N2: InN(A1)}
name: C, type: Capacitor, value: C, ports: {Np: InN(A1), Nn: X1}
name: ID, type: CurrentSource, value: ID, ports: {Np: X1, Nn: GND}
name: D, type: Diode, ports: {Na: X1, Nc: GND}
]
extrainfo:The circuit is a current-controlled amplifier with an op-amp in a non-inverting configuration. The gain is influenced by the diode's dynamic resistance.
(a)
image_name:(a)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: Vi, InN: InN(A1), OutP: Vo, OutN: GND}
name: R, type: Resistor, value: R, ports: {N1: Vo, N2: InN(A1)}
name: rd, type: Resistor, value: rd, ports: {N1: InN(A1), N2: GND}
]
extrainfo:The circuit is a current-controlled amplifier with an op-amp in a non-inverting configuration. The gain is influenced by the diode's dynamic resistance. The input voltage is vi = (5 mV) cos(10^4 t), and the current ID is variable between 0.1 mA and 1 mA.
(b)
FIGURE 1.65 (a) Current-controlled amplifier, and (b) its small-signal ac equivalent.
EXAMPLE 1.20 In the circuit of Fig. $1.65 a$ let $v_{i}=(5 \mathrm{mV}) \cos 10^{4} t$, and let $I_{D}$ be variable over the range $(0.1 \mathrm{~mA}) \leq I_{D} \leq(1 \mathrm{~mA})$. Specify suitable values for $R$ and $C$ so that for $I_{D}=$ 1 mA the gain is $100 \mathrm{~V} / \mathrm{V}$. What is the range of variability of the gain of your circuit?
#### Solution
At $I_{D}=1 \mathrm{~mA}$ we have $r_{d}=26 \Omega$. For a gain of $100 \mathrm{~V} / \mathrm{V}$ we need $R$ such that $100=$ $1+R / 26$, or $R=2574 \Omega$. Moreover, we need $C \gg 1 /\left[\omega r_{d(\min )}\right]=1 /\left(10^{4} \times 26\right)=$ $3.8 \mu \mathrm{~F}$. For instance, pick $C=100 \mu \mathrm{~F}$.
At $I_{D}=0.1 \mathrm{~mA}$ we have $r_{d}=260 \Omega$, so the gain is $1+2574 / 260=11.9 \mathrm{~V} / \mathrm{V}$. Thus, as $I_{D}$ is varied from 1 mA to 0.1 mA , the gain varies from $100 \mathrm{~V} / \mathrm{V}$ to $10.9 \mathrm{~V} / \mathrm{V}$.
## 1.12 BREAKDOWN-REGION OPERATION
The very steep diode curve in the breakdown (BD) region suggests that we can use the $p n$ diode as a voltage reference, if only an approximate one. A voltage reference is a circuit that provides a constant output voltage $V_{o}$ in spite of variations in its own supply voltage $V_{I}$ and in the load current $I_{L}$. Such a voltage is used as a reference by other circuits, like data converters, multimeters, and regulated power supplies, or also to power circuits with moderate power requirements, which we shall generally refer to as the load (LD). As we know, the reciprocal of slope of the BD-region characteristic is denoted as $r_{z}$ and is called the dynamic resistance in the BD region. The smaller $r_{z}$, the steeper the characteristic. According to the BD diode model depicted in Fig. 1.50, in the limit $r_{z} \rightarrow 0$ the diode would act as a perfect voltage source $V_{\text {Z0 }}$.
As we know, the breakdown effect is due to two different mechanisms: Zener breakdown for BD voltages of less than about 6 V , and avalanche breakdown for BD voltages of more than about 6 V . Diodes specifically intended for BD-region operation are referred to as Zener diodes, regardless of the BD mechanism, and exhibit $r_{z}$ values on the order of a few ohms to a few tens of ohms. Commercial Zener diodes are available in the same standard values as $10 \%$ resistances, such as $4.3 \mathrm{~V}, 4.7 \mathrm{~V}$, $5.1 \mathrm{~V}, 5.6 \mathrm{~V}, 6.2 \mathrm{~V}, 6.8 \mathrm{~V}, 7.5 \mathrm{~V}, 8.2 \mathrm{~V}, 9.1 \mathrm{~V}, 10 \mathrm{~V} \ldots .$. The manufacturer's data sheets usually report $V_{Z}$ as well as $r_{z}$ at some specific bias current $I_{Z}$ well down the BD curve, away from the knee. With reference to the BD model of Fig. 1.50, we can find the extrapolated value $V_{z 0}$ indirectly as
$$
\begin{equation*}
V_{z 0}=V_{Z}-r_{z} I_{Z} \tag{1.85}
\end{equation*}
$$
EXAMPLE 1.21 A certain Zener diode is specified to have $r_{z}=10 \Omega$, and $V_{Z}=6.2 \mathrm{~V}$ at $I_{Z}=20 \mathrm{~mA}$. Find $V_{z 0}$, as well as the value of $V_{Z}$ at $I_{Z}=10 \mathrm{~mA}$.
#### Solution
By Eq. (1.85), $V_{z 0}=6.2-10 \times 0.02=6.0 \mathrm{~V}$. By Eq. (1.85) still, $V_{z}=V_{z 0}+r_{z} I_{z}=$ $6.0+10 \times 0.01=6.1 \mathrm{~V}$.
image_name:(a)
description:
[
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: VI, N2: X1}
name: D, type: Diode, ports: {Na: GND, Nc: X1}
name: LD, type: Other, ports: {N1: VO, N2: GND}
name: rz, type: Resistor, value: rz, ports: {N1: VO, N2: GND}
]
extrainfo:The circuit diagram (a) is a voltage reference circuit using a Zener diode. The voltage source VI provides input voltage, and the Zener diode D stabilizes the output voltage VO across the load LD. The resistor R limits the current through the diode. The circuit maintains a constant output voltage VO despite variations in the input voltage or load current.
image_name:(b)
description:
[
name: VI, type: VoltageSource, ports: {Np: VI, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: VI, N2: VO}
name: LD, type: VoltageControlledVoltageSource, value: VO, ports: {Np: VO, Nn: GND}
name: rz, type: Resistor, value: rz, ports: {N1: VO, N2: VZ0}
name: VZ0, type: VoltageSource, value: VZ0, ports: {Np: VZ0, Nn: GND}
]
extrainfo:The circuit diagram (b) represents a Zener diode voltage reference model with a voltage source VI, resistor R, and load LD. The Zener diode is modeled with a series resistor rz and a voltage source VZ0. The output voltage VO is used as the reference voltage.
FIGURE 1.66 (a) The Zener diode as a voltage reference. (b) To investigate the reference's behavior, replace the Zener diode with its BD-region model.
#### Solution
(a) From Fig. $1.66 b$ it is apparent that $V_{O}=V_{Z}$, so at $I_{Z}=5 \mathrm{~mA}$ we have $V_{o}=$ $V_{z 0}+r_{z} I_{Z}=6.0+10 \times 0.005=6.05 \mathrm{~V}$. The diode current is minimized when $V_{I}$ is minimized $(15 \mathrm{~V})$ and $I_{L}$ is maximized $(10 \mathrm{~mA})$, so $R$ must be such that
$$
R=\frac{V_{l(\min )}-V_{O}}{I_{Z(\min )}+I_{L(\mathrm{fs})}}=\frac{15-6.05}{5+10} \cong 600 \Omega
$$
The closest standard values are $620 \Omega$ and $560 \Omega$. To be on the safe side, use $560 \Omega$.
(b) Again from Fig. $1.66 b$ we note that $V_{O}$ is maximized when $V_{I}$ is maximized $(25 \mathrm{~V})$ and $I_{L}$ is minimized $(0 \mathrm{~mA})$, so using Eq. (1.86) we find
$$
V_{O(\max )}=\frac{10}{560+10} 25+\frac{560}{560+10} 6.0-0=6.333 \mathrm{~V}
$$
Conversely, $V_{O}$ is minimized when $V_{I}$ is minimized $(15 \mathrm{~V})$ and $I_{L}$ is maximized (10 mA), so
$$
V_{O(\min )}=\frac{10}{560+10} 15+\frac{560}{560+10} 6.0-(560 / / 10) 0.01=6.060 \mathrm{~V}
$$
The overall variation in $V_{O}$ is $6.333-6.060=0.273 \mathrm{~V}$, or $0.273 / 6.2=4.4 \%$. Given the much wider range of variability of $V_{I}$ as well as the full-scale variability of $I_{L}$, this is a remarkable result!
### Line and Load Regulation
The output of a voltage reference should be independent of $V_{I}$ and $I_{L}$, so only the second term in the right-hand side of Eq. (1.86) is a desirable one. The other two terms should be zero, a condition that the present circuit could achieve only in the limit $r_{z} \rightarrow 0$. The quality of a voltage reference is specified in terms of two parameters borrowed from voltage-regulator terminology, namely, (a) the line regulation, representing the mV change in $V_{O}$ for every $1-\mathrm{V}$ change in $V_{l}$, and $(b)$ the load regulation, representing the mV change in $V_{O}$ for every 1-mA change in $I_{L}$. From Eq. (1.86) we find, for the present circuit,
$$
\begin{equation*}
\text { Line regulation }=\frac{\Delta V_{O}}{\Delta V_{I}}=\frac{r_{z}}{R+r_{z}} \tag{1.87a}
\end{equation*}
$$
$$
\begin{equation*}
\text { Load regulation }=\frac{\Delta V_{O}}{\Delta I_{L}}=-\left(R / / r_{z}\right) \tag{1.87b}
\end{equation*}
$$
Find the line and load regulation of the circuit of Example 1.22. Express your results in $\mathrm{mV} / \mathrm{V}$ and $\mathrm{mV} / \mathrm{mA}$, as well as in percentage form.
#### Solution
Line Regulation $=10 / 570=17.5 \mathrm{mV} / \mathrm{V}$. Since 17.5 mV represents $0.27 \%$ of 6.2 V , we can also say that Line Regulation $=0.27 \% / \mathrm{V}$. Likewise, Load Regulation $=-(560 / / 10)=-9.8 \mathrm{mV} / \mathrm{mA}$, or $-0.16 \% / \mathrm{mA}$.
#### Solution
(a) We have $R=\left(V_{I}-V_{D(\text { on })}\right) / I_{D} \cong(5-0.7) / 1.0=4.3 \mathrm{k} \Omega$. Moreover, $V_{O}=$ $(26 \mathrm{mV}) \ln \left(10^{-3} / 10^{-15}\right)=0.718 \mathrm{~V}$. At $I_{D}=1 \mathrm{~mA}$ the diode has $r_{d}=26 / 1=$ $26 \Omega$, so Line Regulation $=r_{d} /\left(R+r_{d}\right)=26 /(4300+26)=6 \mathrm{mV} / \mathrm{V}$, and Load Regulation $=-R / / r_{d} \cong-26 \mathrm{mV} / \mathrm{mA}$.
(b) To achieve the same output voltage with a voltage divider we need a second resistor of value $0.718 / 1.0=0.718 \mathrm{k} \Omega$. We now have Line Regulation $=$ $718 /(4300+718)=143 \mathrm{mV} / \mathrm{V}$, and Load Regulation $=-4300 / / 718 \cong$ $-615 \mathrm{mV} / \mathrm{mA}$. Clearly, a diode reference is much better than a voltage divider.
### Zener Diodes as Voltage Clamps
Its voltage-source behavior in the BD region makes the Zener diode suited to stable voltage-clamp applications. The example of Fig. 1.70 is based on a pair of Zener diodes connected back to back. Since they are in series, they are either both off, or both on (one in the forward region and the other in the BD region). We have three possibilities:
- For $v_{I}$ sufficiently positive to turn on both diodes, $D_{1}$ will operate in the BD region and $D_{2}$ in the forward region, as depicted in Fig. 1.71a. The output is clamped at $V_{O H}=V_{Z 1}+V_{D 2(0 n)}$, where we are ignoring the Zener-diode resistance $r_{z 1}$ compared to $R$. Clearly, this situation occurs for $v_{I}>V_{O H}$.
- For $v_{I}$ sufficiently negative, the situation reverses, with $D_{1}$ now operating in the forward region and $D_{2}$ in the BD region. As depicted in Fig. 1.71b, the output is now clamped at $V_{O L}=-\left(V_{D 1(\mathrm{on})}+V_{Z 2}\right)$. This situation occurs for $v_{I}<V_{O L}$.
image_name:(a)
description:
[
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
name: R, type: Resistor, value: 10kΩ, ports: {N1: VI, N2: VO}
name: D1, type: Diode, ports: {Na: VO, Nc: X1}
name: D2, type: Diode, ports: {Na: X1, Nc: GND}
]
extrainfo:The circuit is a Zener-diode clamp. The output voltage is clamped at VOH = VZ1 + VD2(on) for positive input and VOL = -(VD1(on) + VZ2) for negative input. For intermediate input values, the output follows the input.
(a)
image_name:Fig. 1.70b
description:The graph in Fig. 1.70b illustrates the effect of a Zener-diode clamp on an input waveform. It is a time-domain waveform graph, showing how the output voltage \( v_O \) behaves in response to an input voltage \( v_I \) over time.
**Axes Labels and Units:**
- The horizontal axis represents time \( t \), but specific units or scale are not provided.
- The vertical axis represents voltage, with key voltage levels labeled as \( V_{OH} \) (output high voltage), \( V_{OL} \) (output low voltage), and 0 volts.
**Overall Behavior and Trends:**
- The input waveform \( v_I \) is depicted as a sinusoidal wave in gray, oscillating above and below the zero voltage line.
- The output waveform \( v_O \) is shown in black, with its amplitude clamped at \( V_{OH} \) and \( V_{OL} \).
- For input voltages between \( V_{OL} \) and \( V_{OH} \), the output follows the input waveform linearly, indicating that the diodes do not conduct and act as open circuits.
**Key Features and Technical Details:**
- The graph shows clipping of the input waveform at the top and bottom, where the output \( v_O \) levels off at \( V_{OH} \) and \( V_{OL} \) respectively.
- The clamping effect is evident as the output waveform does not exceed \( V_{OH} \) or go below \( V_{OL} \), regardless of the input amplitude.
**Annotations and Specific Data Points:**
- The input waveform \( v_I \) is annotated with an arrow indicating its sinusoidal nature.
- The output waveform \( v_O \) is also annotated, highlighting the regions where it follows the input and where it is clamped.
- The graph clearly demonstrates the clamping action of the Zener diodes, effectively limiting the output voltage to within the specified bounds of \( V_{OH} \) and \( V_{OL} \).
(b)
FIGURE 1.70 A Zener-diode clamp, and its effect upon the input waveform.
- For $V_{O L}<v_{I}<V_{O H}$ there isn't sufficient voltage drive to turn on the diodes, so they both act as open circuits. The situation is depicted in Fig. 1.71c, where the lack of current causes $R$ to drop 0 V , thus giving $v_{O}=v_{I}$. We say that now $R$, being unencumbered, pulls $v_{O}$ to $v_{I}$.
The clamping effect is depicted in Fig. 1.70b. For instance, if $D_{1}$ is a 4.3-V Zener diode and $D_{2}$ is a 6.8-V Zener diode, $v_{O}$ will be clamped in the positive direction at $V_{O H}=$ $4.3+0.7=5.0 \mathrm{~V}$, and in the negative direction at $V_{O L}=-(0.7+6.8)=-7.5 \mathrm{~V}$.
image_name:(a)
description:
[
name: V_I, type: VoltageSource, value: V_I, ports: {Np: V_I, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: V_I, N2: V_O}
name: V_Z1, type: VoltageSource, value: V_Z1, ports: {Np: V_O, Nn: GND}
name: V_D2(on), type: VoltageSource, value: V_D2(on), ports: {Np: V_O, Nn: GND}
name: V_Z2, type: VoltageSource, value: V_Z2, ports: {Np: V_O, Nn: GND}
name: V_D1(on), type: VoltageSource, value: V_D1(on), ports: {Np: V_O, Nn: GND}
]
extrainfo:The circuit shows three conditions for clamping the output voltage based on the input voltage and Zener diodes. In condition (a), the input voltage is greater than the high clamping voltage, V_OH. In condition (b), the input voltage is less than the low clamping voltage, V_OL. In condition (c), the output voltage equals the input voltage, indicating no clamping effect.
image_name:(b)
description:
[
name: V_I, type: VoltageSource, value: V_I, ports: {Np: V_I, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: V_I, N2: V_O}
name: V_Z1, type: VoltageSource, value: V_Z1, ports: {Np: X, Nn: GND}
name: V_D2(on), type: VoltageSource, value: V_D2(on), ports: {Np: V_O, Nn: X}
name: V_Z2, type: VoltageSource, value: V_Z2, ports: {Np: GND, Nn: X}
name: V_D1(on), type: VoltageSource, value: V_D1(on), ports: {Np: X, Nn: V_O}
]
extrainfo:The circuit in diagram (b) illustrates a clamping circuit with Zener diodes and resistors to control the output voltage levels, V_OH and V_OL, based on the input voltage V_I. The clamping ensures that V_O is limited to certain voltage levels depending on the Zener breakdown voltages and the diode forward voltage drops.
image_name:(c)
description:
[
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: VI, N2: VO}
name: VZ1, type: VoltageSource, value: VZ1, ports: {Np: X, Nn: GND}
name: VD2(on), type: VoltageSource, value: VD2(on), ports: {Np: X, Nn: GND}
name: VZ2, type: VoltageSource, value: VZ2, ports: {Np: X, Nn: GND}
name: VD1(on), type: VoltageSource, value: VD1(on), ports: {Np: X, Nn: GND}
]
extrainfo:The circuit in part (c) shows a condition where the output voltage vO equals the input voltage vI, indicating a direct connection with no clamping action.
FIGURE 1.71 Illustrating the three possible conditions for the circuit of Fig. 1.70a.
There are situations in which it is desirable that clamping be symmetric about 0 V , or $V_{O L}=-V_{O H}$. This requires that the two Zener diodes be matched. Alternatively, we can use only one Zener diode, but along with a diode bridge to make it perform the same clamping action both in the positive and negative directions. The circuit is shown in Fig. 1.72, where we have again three possibilities:
- For $v_{I}$ sufficiently positive to turn on the Zener diode via the diode bridge, current flows down the path
$$
\text { source } \rightarrow R \rightarrow D_{1} \rightarrow D_{Z} \rightarrow D_{4} \rightarrow \text { ground }
$$
The output is clamped at $V_{O H}=V_{D 1(\mathrm{on})}+V_{Z}+V_{D 4(\mathrm{on})}=V_{Z}+2 V_{D(\mathrm{on})}$. Clearly, this situation arises for $v_{I}>\left(V_{Z}+2 V_{D(\text { on })}\right)$.
- For $v_{I}$ sufficiently negative, current flows down the path
$$
\text { ground } \rightarrow D_{2} \rightarrow D_{Z} \rightarrow D_{3} \rightarrow R \rightarrow \text { source }
$$
and this occurs for $v_{I}<-\left(V_{Z}+2 V_{D(\text { on })}\right)$. The output is now clamped at $V_{O L}=$ $-\left(V_{Z}+2 V_{D(\text { on })}\right)=-V_{O H}$.
image_name:FIGURE 1.72 Symmetric voltage clamp
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
name: R, type: Resistor, value: 10kΩ, ports: {N1: V1, N2: X1}
name: D1, type: Diode, ports: {Na: X1, Nc: X2}
name: D2, type: Diode, ports: {Na: GND, Nc: X2}
name: DZ, type: Diode, ports: {Na: X2, Nc: X3}
name: D3, type: Diode, ports: {Na: X3, Nc: VO}
name: D4, type: Diode, ports: {Na: GND, Nc: X3}
]
extrainfo:The circuit is a symmetric voltage clamp using a Zener diode to limit the output voltage swing. For input voltages greater than VZ + 2VD(on), or less than -(VZ + 2VD(on)), the output is clamped. Within this range, the output follows the input.
FIGURE 1.72 Symmetric voltage clamp.
- For $\left|v_{t}\right|<\left(V_{Z}+2 V_{D(\text { on })}\right)$ there isn't sufficient voltage drive to turn on any of the diodes, so they all act as open circuits. The lack of current allows $R$ to pull $v_{O}$ to $v_{I}$, thus giving $v_{O}=v_{I}$.
For instance, using a 5.1-V Zener diode will cause the output to be clamped at $\pm(5.1+1.4)= \pm 6.5 \mathrm{~V}$.
Figure $1.73 a$ illustrates the use of a Zener-diode clamp to limit the output swing of an op amp (in this example an inverting-type amplifier). We identify three possibilities:
- As long as both diodes are off, the Inverting Amplifier Rule indicates that the circuit will give
$$
v_{O}=-\frac{R_{2}}{R_{1}} v_{I}
$$
As shown in Fig. 1.73b, the voltage transfer curve (VTC) is a straight line with the gain $\left(-R_{2} / R_{1}\right)$ as its slope. With both diodes in cutoff, any current through $R_{1}$ flows right through $R_{2}$.
- For $v_{I}$ sufficiently positive both diodes will go on ( $D_{1}$ forward, $D_{2}$ in breakdown), thus establishing a fixed voltage drop between the op amp's inverting
image_name:(a)
description:
[
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: VI, N2: InN(A1)}
name: R2, type: Resistor, value: R2, ports: {N1: InN(A1), N2: VO}
name: D1, type: Diode, ports: {Na: X1, Nc: VO}
name: D2, type: Diode, ports: {Na: VO, Nc: X1}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: VO}
]
extrainfo:The circuit is an inverting amplifier with diodes D1 and D2 used for output clamping. The diodes limit the output swing to prevent it from exceeding certain voltage levels. The voltage transfer curve shows the linear gain region and the clamped regions.
image_name:(b)
description:The graph labeled "(b)" is a Voltage Transfer Curve (VTC) for an inverting amplifier circuit with diodes used to limit the output swing. This graph is a plot of the output voltage \( v_O \) on the y-axis versus the input voltage \( v_I \) on the x-axis. Both axes are likely in volts, with a linear scale.
Type of Graph and Function
- **Type**: Voltage Transfer Curve (VTC)
- **Function**: Shows the relationship between input and output voltages in an inverting amplifier circuit.
Axes Labels and Units
- **X-axis**: Represents the input voltage \( v_I \), likely in volts.
- **Y-axis**: Represents the output voltage \( v_O \), likely in volts.
- **Scale**: Linear scale for both axes.
Overall Behavior and Trends
- The graph shows a straight line with a negative slope in the central region, indicating a linear relationship between \( v_I \) and \( v_O \) as described by the gain \(-R_2/R_1\).
- At the extremes of \( v_I \), the output voltage \( v_O \) becomes clamped, resulting in horizontal lines. This indicates the action of the diodes limiting the output voltage.
Key Features and Technical Details
- **Slope**: The central linear region has a slope of \(-R_2/R_1\), which represents the gain of the inverting amplifier.
- **Clamping Points**:
- Upper clamping point at \( V_{Z1} + V_{D2(on)} \), where the output voltage is limited as the diodes conduct.
- Lower clamping point at \(-(V_{D1(on)} + V_{Z2})\), where the output voltage is similarly limited.
- **Breakpoints**: Transition from the linear region to the clamped regions occurs at specific input voltage values where the diodes begin to conduct.
Annotations and Specific Data Points
- The graph is annotated with the clamping voltages \( V_{Z1} + V_{D2(on)} \) and \(-(V_{D1(on)} + V_{Z2}) \).
- The slope of the linear region is explicitly marked as \(-R_2/R_1\).
FIGURE 1.73 Using Zener diodes to limit the output swing of an op amp.
input, which is at virtual ground, and the output $v_{o}$. Consequently, the output is now clamped at
$$
V_{O L}=-\left(V_{D 1(\text { on })}+V_{Z 2}\right)
$$
For instance, if $D_{2}$ is a 4.3-V Zener diode, the output will be clamped at $V_{O L}=$ $-(0.7+4.3)=-5 \mathrm{~V}$. As we raise $v_{I}$ above the value corresponding to the onset of the clamping action, the current through $R_{2}$ remains fixed at $\left(V_{D 1(\text { on })}+V_{Z 2}\right) / R_{2}$, so any excess current coming in via $R_{1}$ will be diverted to the output terminal via the diodes.
- For $v_{I}$ sufficiently negative the opposite situation occurs ( $D_{1}$ in breakdown, $D_{2}$ forward), and the output is now clamped at
$$
V_{O H}=+\left(V_{Z 1}+V_{D 2(\text { on })}\right)
$$
For instance, if $D_{1}$ is a $6.8-\mathrm{V}$ Zener diode, the output will be clamped at $V_{O H}=+(6.8+0.7)=+7.5 \mathrm{~V}$.
If symmetric clamping is desired, the Zener diodes need to be matched. Alternatively, we replace the back-to-back Zener pair with a single Zener diode and a diode bridge, in the manner discussed in connection with Fig. 1.72.
## 1.13 Dc POWER SUPPLIES
As implied by its name, a dc power supply is a circuit that provides a specified dc voltage to power other circuits. The supply is powered in turn by another power source, which in the following we shall assume to be the household ac power, which in the United States is $120 \mathrm{~V} \mathrm{rms}, 60 \mathrm{~Hz}$. Since the household ac voltage is sinusoidal, we need to convert it to a dc voltage. As a first step we rectify it to eliminate its negative alternations and thus ensure that the voltage is always positive. However, the result is a pulsating voltage, that is, a voltage that periodically returns to zero. We need an energy-storage device to hold the voltage above some specified level during the times when the rectifier's output would drop to zero. Such a device is the capacitor, and the result is shown in Fig. 1.74 for the simpler case of a half-wave rectifier (the full-wave rectifier will be discussed later), and a load that we model with resistor $R$. Not shown in the figure for simplicity is a transformer, which we use to step down the ac voltage from its peak value of $120 \sqrt{2} \mathrm{~V}$ to the value required by the application at hand ( 10 V in the example of Fig. 1.74).
image_name:Figure 1.74
description:
[
name: v1, type: VoltageSource, value: 10V, ports: {Np: Vi, Nn: GND}
name: D, type: Diode, ports: {Na: Vi, Nc: Vo}
name: C, type: Capacitor, value: 150uF, ports: {Np: Vo, Nn: GND}
name: R, type: Resistor, value: 1kΩ, ports: {N1: Vo, N2: Vout}
]
extrainfo:The circuit is a half-wave rectifier with a smoothing capacitor and load resistor. The input AC voltage source has a peak amplitude of 10V and a frequency of 60Hz. The diode D1N4002 rectifies the AC input, and the capacitor smooths the rectified output to provide a DC voltage across the load resistor.
FIGURE 1.74 PSpice circuit to simulate a dc power supply with a load $R$.
image_name:Figure 1.75 Voltage (top) and current (bottom) waveforms for the dc power supply of Fig. 1.74
description:**Type of Graph and Function:**
The graph consists of two time-domain waveforms. The top graph shows voltage over time, while the bottom graph displays current over time.
**Axes Labels and Units:**
- **Top Graph (Voltage):**
- **Y-axis:** Voltage (V)
- **X-axis:** Time (ms)
- The voltage is measured in volts, ranging from -10V to 10V.
- **Bottom Graph (Current):**
- **Y-axis:** Diode current $i_D$ (mA)
- **X-axis:** Time (ms)
- The current is measured in milliamperes, ranging from 0 to 600 mA.
**Overall Behavior and Trends:**
- **Top Graph (Voltage):**
- The input voltage $v_I$ (gray line) is a sinusoidal AC waveform with a peak amplitude of 10V.
- The output voltage $v_O$ (black line) is a rectified waveform showing a smoothed DC voltage with a ripple, peaking at approximately 9.3V due to the diode drop of 0.7V.
- The waveform is periodic with a frequency corresponding to the input AC frequency of 60Hz.
- **Bottom Graph (Current):**
- The diode current $i_D$ shows sharp peaks corresponding to the charging of the capacitor during each positive half-cycle of the AC input.
- The current peaks are initially high, reaching up to 600 mA, and decrease significantly after the initial surge.
**Key Features and Technical Details:**
- **Top Graph (Voltage):**
- The output voltage $v_O$ follows the peaks of the input voltage $v_I$ but does not drop to negative values, indicating rectification.
- The ripple in $v_O$ decreases over time as the capacitor smooths the output.
- **Bottom Graph (Current):**
- The initial current surge is significant as the capacitor charges quickly to the peak voltage.
- Subsequent current peaks are smaller, reflecting the reduced charging current needed to maintain the capacitor's voltage.
**Annotations and Specific Data Points:**
- The top graph is annotated with $v_I$ and $v_O$ to differentiate between input and output voltages.
- The initial current peak reaches approximately 600 mA, with subsequent peaks much smaller, reflecting the behavior of the diode and capacitor in the rectifier circuit.
FIGURE 1.75 Voltage (top) and current (bottom) waveforms for the dc power supply of Fig. 1.74.
The relevant waveforms of the circuit of Fig. 1.74 are shown in Fig. 1.75, with respect to which we make the following observations:
- At power turn-on the diode $D$ and the capacitor $C$ act as a peak detector, and we witness a large initial current surge to charge $C$, initially assumed discharged, to the peak value of the input, short of the diode voltage drop $(10-0.7=9.3 \mathrm{~V}$ in our example.)
- Once $v_{I}$ peaks out, the diode goes off, leaving the capacitor as the sole source of power for the load. As $R$ draws current, $C$ will discharge. However, in a welldesigned dc supply, $C$ is chosen large enough to keep discharge fairly small during the time intervals when the diode is off.
- As the next positive input alternation comes along and $v_{I}$ rises above the present capacitor voltage by a diode voltage drop, the diode becomes again conductive, recharging the capacitor to the peak value of the input, short of the diode voltage drop.
- Henceforth all the waveforms repeat, with the output voltage exhibiting ripple, and the diode current consisting of spikes during the diode conduction intervals.
### Ripple, Conduction Interval, and Peak Diode Current
We now wish to investigate the interdependence of the various parameters intervening in the design of a dc power supply. Dc supplies of the type under discussion here are hardly precise systems, so we make a number of simplifying assumptions to speed up our estimations. As mentioned, in a well-designed dc supply the capacitor
image_name:(a)
description:
[
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
name: D, type: Diode, ports: {Na: VI, Nc: VO}
name: C, type: Capacitor, value: C, ports: {Np: VO, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: VO, N2: GND}
]
extrainfo:The circuit is a basic DC power supply with a diode rectifier, smoothing capacitor, and load resistor. It converts AC input to DC output with ripple, as shown in the waveform diagram. The diode conducts during the positive half-cycles, charging the capacitor, which then discharges through the resistor, providing a smoother DC output.
image_name:(b)
description:The graph in Figure 1.76(b) illustrates the voltage and current waveforms in a DC power supply circuit. It includes two primary plots: the voltage waveform at the top and the diode current waveform at the bottom.
**Type of Graph and Function:**
- The graph is a time-domain waveform showing voltage and current over time.
**Axes Labels and Units:**
- The horizontal axis represents time, denoted as 't'. Specific time intervals are marked, such as \( T_{ON} \) and \( T_{OFF} \), which are the conduction and non-conduction intervals respectively.
- The vertical axis of the top plot represents voltage, with key values labeled as \( V_I \) and \( V_O \) (input and output voltages), and \( V_p \) (peak voltage).
- The vertical axis of the bottom plot represents current, specifically the diode current \( i_D \).
**Overall Behavior and Trends:**
- The voltage waveform shows a periodic pattern with a peak \( V_p \) and a ripple \( V_r \) between the peak and the minimum of the waveform.
- The diode current waveform consists of sharp spikes during the diode conduction intervals (\( T_{ON} \)).
**Key Features and Technical Details:**
- The voltage waveform has a peak \( V_p \) and a ripple \( V_r \), indicating the variation in output voltage.
- The diode current \( i_D \) reaches a maximum value \( i_{D(max)} \) during the conduction interval \( T_{ON} \), after which it drops to zero during \( T_{OFF} \).
- The shaded areas under the current spikes represent the conduction intervals.
**Annotations and Specific Data Points:**
- \( T \) represents the period of the waveform cycle.
- \( T_{ON} \) and \( T_{OFF} \) are the time intervals when the diode is conducting and not conducting, respectively.
- The maximum diode current \( i_{D(max)} \) is annotated on the current waveform.
This graph effectively demonstrates the relationship between the voltage ripple and the diode current spikes in a DC power supply circuit, emphasizing the importance of the conduction intervals in determining the current characteristics.
FIGURE 1.76 (a) Dc power supply, and (b) voltage and current waveforms.
is chosen sufficiently large to ensure a small ripple relative to the peak value $V_{p}$ of the ac input, or
$$
V_{r} \ll V_{p}
$$
where $V_{r}$ denotes the peak-to-peak amplitude of the output ripple. Also, it is convenient to assume the diode to be ideal, or $V_{D(\text { on })} \cong 0$. With these approximations in mind, we redraw the circuit and the repetitive portion of its waveforms as in Fig. 1.76. As seen, capacitor discharge is approximately linear, and thus governed by the rule that engineers express in the form $C \Delta v=I \Delta t$ (cee delta vee equals aye delta tee), where presently $\Delta v$ is the ripple $V_{r}, I$ is the average load current $I_{L}$, and $\Delta t$ is the time interval during which the diode is off, or $T_{\mathrm{OFF}}$. Thus, $C V_{r} \cong I_{L} T_{\mathrm{OFF}}$. Solving for the ripple, we obtain
$$
\begin{equation*}
V_{r} \cong \frac{I_{L} T_{\mathrm{OFF}}}{C} \tag{1.91}
\end{equation*}
$$
With reference to Fig. 1.76b, top, we approximate $I_{L} \cong\left(V_{p}-0.5 V_{r}\right) / R \cong V_{p} / R$ and $T_{\text {OFF }} \cong T=1 / f$, where $f$ is the input frequency. Consequently, Eq. (1.91) becomes
$$
\begin{equation*}
V_{r} \cong \frac{V_{p}}{f R C} \tag{1.92}
\end{equation*}
$$
If we wish to know to a better degree of accuracy the average value of the output, also called the output dc component and aptly denoted as $V_{O}$, then the diode's voltage drop needs to be taken into consideration. By inspection,
$$
\begin{equation*}
V_{O}=V_{p}-V_{D(\mathrm{on})}-0.5 V_{r} \tag{1.93}
\end{equation*}
$$
(a) Estimate the ripple in the circuit of Fig. 1.74.
(b) If $V_{D(\text { on })}=0.7 \mathrm{~V}$, what is the dc component of the output? What value must $V_{p}$ be changed to if we want $V_{O}=10 \mathrm{~V}$ ?
(c) If $V_{p}$ is changed to 50 V and $R$ to $10 \mathrm{k} \Omega$, find $C$ for a ripple of not more than 2 V .
#### Solution
(a) By Eq. (1.92),
$$
V_{r} \cong \frac{10}{60 \times 10^{3} \times 150 \times 10^{-6}}=1.1 \mathrm{~V}
$$
which is in fairly good agreement with Fig. 1.75, top.
(b) By Eq. (1.93), $V_{O}=10-0.7-0.5 \times 1.1=8.75 \mathrm{~V}$, also in fairly good agreement with Fig. 1.75, top. For $V_{o}=10 \mathrm{~V}$, we need to raise $V_{p}$ to $10+0.7+0.5 \times 1.1$, or to $V_{p}=11.25 \mathrm{~V}$.
(c) Using again Eq. (1.91), we need
$$
C \geq \frac{V_{p}}{f R V_{r}}=\frac{50}{60 \times 10^{4} \times 2} \cong 42 \mu \mathrm{~F}
$$
We now wish to develop expressions for the diode conduction interval $T_{\mathrm{ON}}$ and the peak diode current $i_{D(\max )}$. To simplify our estimations, we again assume $V_{D(\text { on })}=0$. With reference to Fig. 1.76b, top, we express the input as $v_{I}(t)=V_{p} \cos (2 \pi f t)$. Impos$\operatorname{ing} v_{O}\left(-T_{\mathrm{ON}}\right)=v_{l}\left(-T_{\mathrm{ON}}\right)=V_{p}-V_{r}$ yields
$$
V_{p} \cos \left[2 \pi f\left(-T_{\mathrm{ON}}\right)\right]=V_{p}-V_{r}
$$
Rearranging and expanding the cosine function, we write
$$
1-\frac{V_{r}}{V_{p}}=\cos \left[2 \pi f\left(-T_{\mathrm{ON}}\right)\right]=\cos \left(2 \pi f T_{\mathrm{ON}}\right)=1-\frac{1}{2}\left(2 \pi f T_{\mathrm{ON}}\right)^{2}+\cdots
$$
It is apparent from the figure that the condition $V_{r} \ll V_{p}$ implies $T_{\mathrm{ON}} \ll T(=1 / f)$, so we can ignore higher-order terms in the series expansion. Solving for $T_{\mathrm{ON}}$ we get
$$
\begin{equation*}
T_{\mathrm{ON}} \cong \frac{1}{2 \pi f} \sqrt{\frac{2 V_{r}}{V_{p}}} \tag{1.94}
\end{equation*}
$$
With reference to Fig. 1.76a, we observe that during diode conduction we have, by KCL
$$
\begin{equation*}
i_{D}=C \frac{d v_{O}}{d t}+i_{L}=C \frac{d\left[V_{p} \cos (2 \pi f t)\right]}{d t}+i_{L} \tag{1.95}
\end{equation*}
$$
The diode current is maximum at the onset of the conduction interval, or $t=-T_{\mathrm{ON}}$. At this instant we have
$$
\left.\frac{d \cos (2 \pi f t)}{d t}\right|_{t=-T_{o \mathrm{o}}}=-2 \pi f \sin \left[2 \pi f\left(-T_{\mathrm{ON}}\right)\right] \cong(2 \pi f)^{2} T_{\mathrm{ON}}=2 \pi f \sqrt{\frac{2 V_{r}}{V_{p}}}
$$
where we have approximated $\sin x \cong x$ and have also used Eq. (1.94). Substituting into Eq. (1.95), along with the approximation $i_{L} \cong I_{L} \cong V_{p} / R$, we finally get
$$
\begin{equation*}
i_{D(\max )} \cong I_{L}\left(1+2 \pi \sqrt{\frac{2 V_{p}}{V_{r}}}\right) \tag{1.96}
\end{equation*}
$$
EXAMPLE 1.26 (a) Estimate the conduction interval in the circuit of Fig. 1.74, and express it as a percentage of the period $T$. Comment on your result.
(b) Find $i_{D(\max )}$ for the same circuit.
(c) Estimate the average diode current $i_{D(\text { avg })}$ during the conduction interval $T_{\mathrm{ON}}$, and again comment.
#### Solution
(a) Using $V_{r}=1.1 \mathrm{~V}$ from Example 1.25, we have, by Eq. (1.94),
$$
T_{\mathrm{ON}}=\frac{1}{2 \pi 60} \sqrt{\frac{2 \times 1.1}{10}}=1.24 \mathrm{~ms}
$$
Since the period is $T=1 / 60=16.7 \mathrm{~ms}$, the diode conducts during $1.24 / 16.7=$ 0.075 , or only $7.5 \%$ of each cycle, thus confirming the validity of the approximation $T_{\text {OFF }} \cong T$.
(b) We have $I_{L} \cong V_{p} / R=10 / 1=10 \mathrm{~mA}$. By Eq. (1.96),
$$
i_{D(\max )}=10\left(1+2 \pi \sqrt{\frac{2 \times 10}{1.1}}\right) \cong 280 \mathrm{~mA}
$$
(c) Given the approximately triangular shape of the current spikes, we estimate $i_{D(\text { avg })} \cong i_{D(\max )} / 2=140 \mathrm{~mA}$. Note that $i_{D(\text { avg })} \gg I_{L}$, an obvious consequence of the fact that the charge delivered by the capacitor to the load during the time interval $T_{\mathrm{OFF}}$ must be replenished by the diode during the much shorter conduction interval $T_{\mathrm{ON}}$.
When designing a dc power supply we must select a diode type with adequate current-handling capability during the brief spikes of conduction. Also, we must ensure that the breakdown voltage is sufficiently higher than the peak inverse voltage (PIV), which is the maximum reverse voltage that the diode ever experiences in a given circuit. In the circuit of Fig. 1.74 this condition occurs when $v_{I}$ reaches its negative peak, at which point the voltage across the diode is, by KVL, $v_{D}=-V_{p}-v_{O} \cong$ $-V_{p}-V_{p}=-2 V_{p}$. Consequently,
$$
\begin{equation*}
\mathrm{PIV} \cong 2 V_{p} \tag{1.97}
\end{equation*}
$$
With the data of Fig. 1.74, PIV $=20 \mathrm{~V}$. To be on the safe side, specify a PIV at least $50 \%$ higher than the calculated value. In our case, let PIV $\geq 1.5 \times 20=30 \mathrm{~V}$.
### Dc Supplies with Full-Wave Rectifiers
It is apparent that if we use a full-wave rectifier instead of a half-wave, the ripple will be approximately reduced in half, everything else remaining the same. Alternatively, we can guarantee the same ripple but with a capacitance half as large, which is quite desirable because large-valued capacitors are bulky. As mentioned, a dc supply that is powered from the household ac power is likely to be preceded by a transformer to scale down the $120-\mathrm{V}$ ac voltage to a more manageable value as required by the application at hand. We can take advantage of this and use a center-tapped transformer, along with a pair of diodes, to achieve full-wave rectification in the manner depicted in Fig. 1.77. A center tapped winding can be viewed as two identical windings connected in series but in antiphase, so that the voltages at its terminals, relative to the common node, are, respectively, $+v_{S}$ and $-v_{S}$. Once we add two diodes as shown, we end up with two separate half-wave rectifiers, but operating on alternate half cycles, in effect resulting in full-wave rectification. Equation (1.91) still holds. However, in Eq. (1.92) we must replace $f$ with $2 f$ to reflect the fact that the period of the full-wave rectified ac voltage is half that of the original voltage and its frequency is thus $2 f$. Consequently, Eqs. (1.92) and (1.96) become
$$
\begin{equation*}
V_{r} \cong \frac{V_{p}}{2 f R C} \tag{1.98}
\end{equation*}
$$
and
$$
\begin{equation*}
i_{D(\max )} \cong I_{L}\left(1+2 \pi \sqrt{\frac{V_{p}}{2 V_{r}}}\right) \tag{1.99}
\end{equation*}
$$
indicating that, everything else remaining the same, both $V_{r}$ and $i_{D(\max )}$ are approximately reduced in half compared to the half-wave case. However, we still have PIV $\cong 2 V_{p}$. The conduction interval of each diode is still governed by Eq. (1.94), if with the new value of $V_{r}$.
A notorious disadvantage of the center-tapped transformer is that its secondary coil requires twice as many turns. The alternative implementation of Fig. 1.78 utilizes a single secondary, but with a diode bridge to achieve full-wave rectification. Its
image_name:FIGURE 1.77 (a)
description:
[
name: vP, type: VoltageSource, value: vP, ports: {Np: vP, Nn: GND}
name: Transformer, type: Transformer, ports: {In1: vP, In2: GND, Out1: vS, Oou2: -vS}
name: D1, type: Diode, ports: {Na: vS, Nc: vO}
name: D2, type: Diode, ports: {Na: -vS, Nc: vO}
name: C, type: Capacitor, value: C, ports: {Np: vO, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: vO, N2: GND}
]
extrainfo:The circuit is a full-wave rectifier using a center-tapped transformer. It converts AC voltage to DC voltage with the help of diodes D1 and D2, a capacitor C for smoothing, and a resistor R as load. The waveform shows the rectified output voltage over time.
image_name:FIGURE 1.77 (b)
description:1. **Type of Graph and Function:**
The graph in FIGURE 1.77 (b) is a time-domain waveform representing the output voltage of a full-wave rectifier using a center-tapped transformer.
2. **Axes Labels and Units:**
- The horizontal axis is labeled as time \( t \), with units likely in seconds or milliseconds, though specific units are not provided.
- The vertical axis represents the output voltage \( v_O \), with units in volts, though specific values are not mentioned.
3. **Overall Behavior and Trends:**
- The waveform shows a periodic pattern, repeating every period \( T \).
- Each cycle consists of two peaks, indicating a full-wave rectification process where both halves of the input AC waveform are used.
- The waveform demonstrates a charging and discharging pattern, typical of a rectified signal with a smoothing capacitor.
4. **Key Features and Technical Details:**
- The waveform has a smooth rise and fall, with sharp peaks at each half-period \( T/2 \), \( T \), and \( 3T/2 \).
- The peaks correspond to the maximum voltage level achieved during each half of the AC cycle.
- The waveform does not return to zero, indicating the presence of a DC offset due to the rectification process.
- The sharp peaks suggest the point at which the capacitor charges to the peak rectified voltage, while the gradual decline shows the capacitor discharging through the load.
5. **Annotations and Specific Data Points:**
- The graph is annotated with \( v_O \) to indicate the output voltage.
- Key points are marked at \( 0 \), \( T/2 \), \( T \), and \( 3T/2 \) along the time axis, highlighting the periodic nature of the waveform.
This waveform effectively illustrates the behavior of a full-wave rectified output, showing both the charging and discharging phases of the smoothing capacitor, which results in a more constant DC output compared to a half-wave rectifier.
FIGURE 1.77 (a) Dc power supply with a full-wave rectifier using a center-tapped transformer, and (b) voltage waveforms.
image_name:FIGURE 1.78
description:
[
name: Vp, type: VoltageSource, value: Vp, ports: {Np: Vp, Nn: GND}
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: D1, type: Diode, ports: {Na: Vs, Nc: X2}
name: D2, type: Diode, ports: {Na: X2, Nc: GND}
name: D3, type: Diode, ports: {Na: Vs, Nc: X1}
name: D4, type: Diode, ports: {Na: X1, Nc: GND}
name: C, type: Capacitor, value: C, ports: {Np: X2, Nn: X1}
name: R, type: Resistor, value: R, ports: {N1: X2, N2: X1}
]
extrainfo:The circuit is a DC power supply using a diode bridge rectifier. It converts AC to DC, smoothing the output with a capacitor to provide a steady DC voltage across the resistor load.
FIGURE 1.78 Dc power supply using a diode bridge rectifier.
waveforms are similar to those of Fig. 1.77b, and Eqs. (1.98) and (1.99) hold also in the present case. However, with two diode drops, Eq. (1.93) changes to
$$
\begin{equation*}
V_{O}=V_{p}-2 V_{D(\mathrm{on})}-0.5 V_{r} \tag{1.100}
\end{equation*}
$$
Moreover, we now have
$$
\begin{equation*}
\mathrm{PIV} \cong V_{p} \tag{1.101}
\end{equation*}
$$
Given the various options available-half wave, full-wave with center-tapped transformer, or full-wave with diode bridge-a designer will evaluate the advantages and disadvantages of each and settle for the one that best meets the cost and complexity constraints of the application at hand.
### Concluding Observation
It is important to realize that the expressions of Eqs. (1.94), (1.96), (1.98), and (1.99) have been derived for the case of sinusoidal inputs, as most dc power supplies are powered from the household ac line. However, there are specialized cases in which the input waveform is not necessarily sinusoidal. It is left as an exercise, in the end-of-chapter problems, to apply the same line of reasoning to non-sinusoidal cases and develop ad-hoc expressions for $T_{\mathrm{ON}}, i_{D(\max )}$, and $i_{D(\text { avg })}$. Also, for simplicity, the load is usually simulated with a mere resistance. A more realistic load model is a Norton equivalent, consisting of a fixed load-current in parallel with a resistance.
## APPENDIX 1A
### SPICE Models for Diodes
SPICE (an acronym for Simulation Program with Integrated Circuit Emphasis) is a powerful computer-simulation tool designed to help verify complex circuits that would be prohibitive to analyze via hand calculations. Nowadays there are a plethora of SPICE versions available (a Web search will reveal the existence of online clubs devoted to particular versions, where members exchange useful tips). Rather than committing to a particular version, I have tried to keep the SPICE examples general and simple enough so students can try them out using their preferred SPICE version. All examples were created using the Student Versions of Cadence's PSpice. This version, available free of charge, is a powerful pedagogical tool especially for the beginner, as you can glean from the various PSpice examples scattered throughout the current and subsequent chapters.
However powerful, SPICE is no substitute for true understanding-the kind attainable through diligent reasoning and patient paper-and-pencil calculations. Even when circuit complexity mandates the use of SPICE, one must still be able to examine the results provided by the computer and spot-check them by a combination of hand calculations and intuitive insight. Consequently, SPICE is only an analytical aid-if a most powerful one.
It is assumed that the student is already familiar with SPICE basics from prerequisite courses such as circuits courses and labs (how to create a circuit schematic using parts from SPICE's internal libraries, how to direct SPICE to perform a specific type of analysis among the various possible, and how to display traces using Probe, the oscilloscope-like feature provided by PSpice). The focus of this Appendix is SPICE models for diodes.
When we use a semiconductor device in a SPICE circuit schematic, we need to specify the characteristics of that device. The characteristics are expressed in terms of a list of parameters that SPICE then uses to create an internal model of the device. Shown in Table 1A. 1 are the parameters intervening in the creation of the model for $p n$ diodes. PSpice comes with a library of models for some of the most popular semiconductor devices. Moreover, the user can create additional models by suitably editing one of the already available models.
As an example, consider the PSpice circuit of Fig. 1.51a, utilizing the popular $1 N 4148$ pn diode. By PSpice convention, diode names must start with the letter D, so the part number has been designated as D1N4148. To create the circuit we use the Place $\rightarrow$ Part commands to lay out the various components, and the Place $\rightarrow$ Wire commands to interconnect them. When it comes to placing the diode, we import it from PSpice's library by going down its list of entries and left-clicking on the D1N4148 part. To visualize its model, first left-click on the diode to select it, then right-click to activate a pull-down menu of possible actions. Left-click on Edit PSpice Model, and the following list will appear:
```
.model D1N4148 D(Is=2.682n N=1.836 Rs=.5664 Ikf=44.17m Xti=3
+ Eg=1.11 Cjo=4p M=.3333 Vj=.5 Fc=.5 Isr=1.565n Nr=2
+ Bv=100 Ibv=100u Tt=11.54n)
```
TABLE 1A.1 Partial parameter list of the PSpice diode model.
| Symbol | Name | Parameter description | Units | Default | Example |
| :--- | :--- | :--- | :--- | :--- | :--- |
| $I_{s}$ | Is | Saturation current | A | 10 fA | 2 fA |
| $n$ | N | Emission coefficient |  | 1 | 1.5 |
| $r_{S}$ | Rs | Bulk resistance | $\Omega$ | 0 | 2 |
| $C_{j 0}$ | Cjo | Zero-bias junction capacitance | F | 0 | 1.0 pF |
| $m$ | M | Grading coefficient |  | 0.5 | 0.33 |
| $\phi_{0}$ | Vj | Built-in potential | V | 1 V | 0.8 V |
| $\tau_{T}$ | Tt | Transit time | S | 0 | 0.2 ns |
| $V_{Z}$ | Bv | Voltage at onset of breakdown | V | $\infty$ | 100 V |
| $I_{Z}$ | Ibv | Current at onset of breakdown | A | 0.1 nA | $100 \mu \mathrm{~A}$ |
The parameter values shown are designed to match as closely as possible those given in the manufacturer's data sheets. We easily see that this particular diode type has $I_{s}=2.682 \mathrm{nA}, n=1.836, r_{s}=0.5664 \Omega, C_{j 0}=4 \mathrm{pF}, m=0.3333, \phi_{0}=$ 0.5 V , and $\tau_{T}=11.54 \mathrm{~ns}$. We also note that the onset of the breakdown region (knee of the $i-v$ curve in reverse bias) is specified to be 100 V at $100 \mu \mathrm{~A}\left(V_{Z}=\right.$ 100 V at $I_{Z}=100 \mu \mathrm{~A}$ ). The complete list contains additional parameters representing higher-order effects that are beyond our present scope. Also, note the usage of a space to separate individual parameters, and the usage of the + symbol to denote continuity when the list is too long to fit in a single line. For more details, see Ref. [11].
If you wish to create your own diode model to experiment with, you can do so simply by overwriting (editing) the parameter values of an existing diode model, such as the D1N4148 considered above. However, to avoid losing the original D1N4148 model, a new name must be given to the newly formed model. This is what was done to create a model for the pseudo-ideal diode of Figs. 2.14 and 2.16. The diode model was renamed as Dideal, and the parameter list was edited as follows:
.model Dideal D(Is=1n N=0.001)
Even though we know that a practical $p n$ junction has $1 \leq n \leq 2$, here we have specified an artificially small value of $n$ to ensure that the exponential $i-v$ curve shoots up for very small values of $v$, thus approximating an ideal diode. (To get an idea, use the logarithmic diode law to verify that to sustain $i=1 \mathrm{~mA}$ this diode requires only $v=0.36 \mathrm{mV}-$ almost 0 V , and certainly much less than the typical voltage drop of 0.7 V !) This is all we need to simulate an almost ideal diode, so all other parameters have been omitted from the list. All omitted parameters are automatically assigned default values according to Table 1A.1.
PSpice's library contains also a model for the 1N750 4.7-V Zener diode:
image_name:1N750 4.7-V Zener diode model
description:The image displays the SPICE model parameters for a 1N750 4.7-V Zener diode. The model is defined with the following parameters:
- **Model Name:** D1N750
- **Diode Type:** D
- **Parameters:**
- **Is (Saturation Current):** 880.5E-18 A
- **Rs (Series Resistance):** 0.25 Ω
- **Ikf (Forward Knee Current):** 0 A
- **N (Emission Coefficient):** 1
- **Xti (Temperature Coefficient of Is):** 3
- **Eg (Energy Gap):** 1.11 eV
- **Cjo (Zero-bias Junction Capacitance):** 175 pF
- **M (Grading Coefficient):** 0.5516
- **Vj (Built-in Potential):** 0.75 V
- **Fc (Forward Bias Depletion Capacitance Coefficient):** 0.5
- **Isr (Recombination Current Parameter):** 1.859 nA
- **Nr (Emission Coefficient for Isr):** 2
- **Bv (Breakdown Voltage):** 4.7 V
- **Ibv (Current at Breakdown Voltage):** 20.245 mA
- **Nbv (Emission Coefficient for Ibv):** 1.6989
- **Ibvl (Low-level Current at Breakdown Voltage):** 1.9556 mA
- **Nbvl (Emission Coefficient for Ibvl):** 14.976
- **Tbvl (Temperature Coefficient for Ibvl):** -21.277 μA
The last line, which starts with an asterisk, is a comment summarizing key characteristics of the diode:
- **Vz (Zener Voltage):** 4.7 V at 20 mA
- **Rz (Dynamic Resistance):**
- 300 Ω at 1 mA
- 12.5 Ω at 5 mA
- 2.6 Ω at 20 mA
This detailed specification outlines the electrical characteristics of the 1N750 Zener diode, useful for circuit simulation and analysis.
The last line, starting with an asterisk, is by convention a comment line summarizing salient characteristics. It states that this diode is rated to provide $V_{Z}=4.7 \mathrm{~V}$ at $I_{Z}=20 \mathrm{~mA}$. Moreover, the reciprocal of the slope of the $i-v$ curve in the breakdown region, denoted as $r_{z}$ in the text, is specified at different points as $r_{z}=300 \Omega$ at $I_{Z}=1 \mathrm{~mA}, r_{z}=12.5 \Omega$ at $I_{Z}=5 \mathrm{~mA}$, and $r_{z}=2.6 \Omega$ at $I_{Z}=20 \mathrm{~mA}$. Clearly, the further down the curve past the knee, the steeper the slope.
The user can readily edit the above model to create a Zener diode with a different rating. For instance, changing $\mathrm{Bv}=4.7$ to $\mathrm{Bv}=6.2$ will turn the model into that of a 6.2-V Zener.
FIGURE P1.14
Hint: consider first the case $v_{I} \geq 0$, and show that $D_{3}$ and $D_{4}$ are off, and that if $v_{I}$ is gradually increased from 0 V , a point is reached at which $D_{1}$ goes on, and then another at which $D_{2}$ goes on. Then, exploit the fact that circuit behavior for $v_{I}<0$ is symmetric of that for $v_{I}>0$.
(b) What happens if $D_{2}$ and $D_{4}$ are removed?
1.15 Sketch and label the VTC of the circuit of Problem 1.14 over the range $-6 \mathrm{~V} \leq v_{I} \leq 6 \mathrm{~V}$ if:
(a) the directions of $D_{2}$ and the $D_{4}$ are reversed, so that their anodes are now at the top and the cathodes at the bottom;
(b) $D_{2}$ and $D_{4}$ are removed from the circuit;
(c) $D_{2}, D_{4}$, and $R_{4}$ are removed from the circuit.
1.16 Redraw the circuit of Fig. P1.14, but with an additional $20-\mathrm{k} \Omega$ resistance between the node labeled $v_{o}$ and ground.
(a) Specify suitable values for $V_{S}$ and $R_{1}$ through $R_{4}$ to implement a symmetric VTC that goes through the origin and has a slope of $1 / 2 \mathrm{~V} / \mathrm{V}$ for $\left|v_{l}\right| \leq 6 \mathrm{~V}$, a slope of $1 / 3 \mathrm{~V} / \mathrm{V}$ for $6 \mathrm{~V} \leq\left|v_{l}\right| \leq 12 \mathrm{~V}$, and a slope of $0 \mathrm{~V} / \mathrm{V}$ for $\left|v_{l}\right| \geq 12 \mathrm{~V}$.
Hint: exploit the symmetry of the VTC, draw it for the case for $v_{I} \geq 0$, and show the subcircuit corresponding to each of its three segments.
(b) What happens to the VTC if $D_{2}$ and $D_{4}$ are removed?
(c) What happens to the VTC if the value of $V_{S}$ is doubled?
1.17 In a clamped capacitor circuit of the type of Fig. 1.22a let $v_{I}$ be a 1-kHz triangular wave having peak values of +10 V and -5 V , and let $C=1 \mu \mathrm{~F}$.
(a) Sketch and label, versus time, $v_{l}, v_{o}$, and the diode current $i_{D}$. Assume $C$ is initially discharged, and let $t=0$ be the instant when $v_{I}$ starts rising from 0 V .
(b) Repeat, but with the direction of the diode reversed, so that the anode is now at the top and the cathode at the bottom.
(c) What happens if the frequency is doubled? Halved?
1.18 Let $C=1 \mu \mathrm{~F}$ be initially discharged in the circuit of Fig. P1.18. Sketch and label $v_{o}(t)$ if $v_{l}(t)$ is the square-wave shown. Do it first with $R=\infty$, then with $R=5 \mathrm{k} \Omega$. Compare the two cases, comment.
image_name:Fig. P1.18
description:
[
name: vI, type: VoltageSource, value: vI, ports: {Np: vI, Nn: GND}
name: C, type: Capacitor, value: C, ports: {Np: vI, Nn: node1}
name: D, type: Diode, ports: {Na: GND, Nc: node1}
name: R, type: Resistor, value: R, ports: {N1: GND, N2: vO}
]
extrainfo:The circuit is a basic RC diode clamper with a square wave input. The diode clamps the output voltage to ground when the input is negative. The capacitor charges and discharges to shape the output waveform. The resistor R provides a load for the output voltage vO.
image_name:v_I(t)
description:The graph depicted is a time-domain waveform representing the input voltage $v_I(t)$ in a circuit. It is a square wave with the following characteristics:
1. **Axes Labels and Units:**
- The horizontal axis represents time, labeled as $t$ and measured in milliseconds (ms).
- The vertical axis represents voltage, labeled as $v_I$ and measured in volts (V).
2. **Overall Behavior and Trends:**
- The waveform is a periodic square wave with a period of 2 milliseconds.
- It alternates between two voltage levels: +10 V and -10 V.
- The waveform remains at +10 V from 0 to 1 ms and from 2 to 3 ms.
- It switches to -10 V from 1 to 2 ms and from 3 to 4 ms.
3. **Key Features and Technical Details:**
- The waveform has sharp transitions at the 1 ms, 2 ms, and 3 ms marks, indicating instantaneous changes in voltage levels.
- The amplitude of the square wave is 10 V, with a peak-to-peak voltage of 20 V.
- The duty cycle is 50%, as the waveform spends equal time at +10 V and -10 V within each period.
4. **Annotations and Specific Data Points:**
- The graph does not have any specific annotations or markers other than the axis labels and the periodic nature of the waveform.
This square wave is used as the input voltage in the circuit shown above, which includes a capacitor $C$, a diode $D$, and a resistor $R$. The behavior of the output voltage $v_o(t)$ will depend on these components and their configurations.
FIGURE P1.18
1.19 (a) Redraw the circuit of Fig. P1.18, but with $R$ replaced by a $1-\mathrm{mA}$ current source flowing downward. Assuming $C$ is initially discharged, sketch and label $v_{o}(t)$ if $v_{I}(t)$ is the square-wave shown, and $C=1 \mu \mathrm{~F}$.
(b) Repeat, but with the 1-mA source now flowing upward. Compare the two cases, comment.
