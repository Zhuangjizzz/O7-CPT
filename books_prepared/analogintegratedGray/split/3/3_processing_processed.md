# 3. Single-Transistor and MultipleTransistor Amplifiers

The technology used to fabricate integrated circuits presents a unique set of component-cost constraints to the circuit designer. The most cost-effective circuit approach to accomplish a given function may be quite different when the realization of the circuit is to be in monolithic form as opposed to discrete transistors and passive elements. ${ }^{1}$ As an illustration, consider the two realizations of a three-stage audio amplifier shown in Figs. 3.1 and 3.2. The first reflects a cost-effective solution in the context of discrete-component circuits, since passive components such as resistors and capacitors are less expensive than the active components, the transistors. Hence, the circuit contains a minimum number of transistors, and the interstage coupling is accomplished with capacitors. However, for the case of monolithic construction, a key determining factor in cost is the die area used. Capacitors of the values used in most discrete-component circuits are not feasible and would have to be external to the chip, increasing the pin count of the package, which increases cost. Therefore, a high premium is placed on eliminating large capacitors, and a dc-coupled circuit realization is very desirable. A second constraint is that the cheapest component that can be fabricated in the integrated circuit is the one that occupies the least area, usually a transistor. Thus a circuit realization that contains the minimum possible total resistance while using more active components may be optimum. ${ }^{2,3}$ Furthermore, an important application of analog circuits is to provide interfaces between the real world and digital circuits. In building digital integrated circuits, CMOS technologies have become dominant because of their high densities and low power dissipations. To reduce the cost and increase the portability of mixed-analog-and-digital systems, both increased levels of integration and reduced power dissipations are required. As a result, we are interested in building analog interface circuits in CMOS technologies. The circuit of Fig. 3.2 reflects these constraints. It uses a CMOS technology and many more transistors than in Fig. 3.1, has less total resistance, and has no coupling capacitors. A differential pair is used to allow direct coupling between stages, while transistor current sources provide biasing without large amounts of resistance. In practice, feedback would be required around the amplifier shown in Fig. 3.2 but is not shown for simplicity. Feedback is described in Chapter 8.

The next three chapters analyze various circuit configurations encountered in linear integrated circuits. In discrete-component circuits, the number of transistors is usually minimized. The best way to analyze such circuits is usually to regard each individual transistor as a stage and to analyze the circuit as a collection of single-transistor stages. A typical monolithic circuit, however, contains a large number of transistors that perform many functions, both passive and active. Thus monolithic circuits are often regarded as a collection of subcircuits that perform specific functions, where the subcircuits may contain many transistors. In this chapter, we first consider the dc and low-frequency properties of the simplest subcircuits: common-emitter, common-base, and common-collector single-transistor amplifiers and their counterparts using
image_name:Figure 3.1 Typical discrete-component realization of an audio amplifier.
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: b1, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: VCC, N2: b1}
name: R4, type: Resistor, value: R4, ports: {N1: VCC, N2: c1}
name: R5, type: Resistor, value: R5, ports: {N1: b2, N2: GND}
name: R7, type: Resistor, value: R7, ports: {N1: e2, N2: GND}
name: R8, type: Resistor, value: R8, ports: {N1: VCC, N2: c2}
name: R9, type: Resistor, value: R9, ports: {N1: b3, N2: GND}
name: R10, type: Resistor, value: R10, ports: {N1: VCC, N2: b3}
name: R11, type: Resistor, value: R11, ports: {N1: b3, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: c1, Nn: b2}
name: C2, type: Capacitor, value: C2, ports: {Np: c2, Nn: b3}
name: CE1, type: Capacitor, value: CE1, ports: {Np: e1, Nn: GND}
name: CE2, type: Capacitor, value: CE2, ports: {Np: e2, Nn: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: b3, Nn: Vo}
name: Ci, type: Capacitor, value: Ci, ports: {Np: Vi, Nn: b1}
name: Q1, type: NPN, ports: {C: c1, B: b1, E: e1}
name: Q2, type: NPN, ports: {C: c2, B: b2, E: e2}
name: Q3, type: NPN, ports: {C: VCC, B: b3, E: Vo}
]
extrainfo:This is a discrete-component audio amplifier circuit using three NPN transistors (Q1, Q2, Q3) in a cascaded configuration. The circuit amplifies an input signal Vi and outputs an amplified signal Vo. Each transistor stage is biased with resistors and capacitors to stabilize and enhance performance. The circuit operates with a VCC power supply and uses capacitors for coupling and bypassing.

Figure 3.1 Typical discrete-component realization of an audio amplifier.
image_name:Figure 3.2
description:
[
name: R1, type: Resistor, ports: {N1: VDD, N2: Vi}
name: M1, type: NMOS, ports: {S: 5152d8, D: d2dag5, G: Vi}
name: M2, type: NMOS, ports: {S: GND, D: d2dag5, G: d5d996}
name: M3, type: PMOS, ports: {S: VDD, D: x2, G: d2dag5}
name: M4, type: PMOS, ports: {S: VDD, D: d2dag5, G: x2}
name: M5, type: PMOS, ports: {S: VDD, D: d5d996, G: d2dag5}
name: M6, type: NMOS, ports: {S: x1, D: Vo, G: d5d996}
name: M7, type: NMOS, ports: {S: VSS, D: g798, G: x1}
name: M8, type: NMOS, ports: {S: VSS, D: 5152d8, G: g798}
name: M9, type: NMOS, ports: {S: VSS, D: x1, G: x1}
name: M10, type: NMOS, ports: {S: VSS, D: x1, G: Vo}
]
extrainfo:This circuit is a CMOS integrated audio amplifier with multiple NMOS and PMOS transistors. It uses differential pairs and current mirrors to amplify the input signal Vi to produce an output signal Vo. The circuit operates with VDD and VSS power supplies and includes biasing and coupling elements to stabilize the amplification process.

Figure 3.2 Typical CMOS integrated-circuit realization of an audio amplifier.

MOS transistors. We then consider some multi-transistor subcircuits that are useful as amplifying stages. The most widely used of these multi-transistor circuits are the differential pairs, which are analyzed extensively in this chapter.

## 3.1 Device Model Selection for Approximate Analysis of Analog Circuits

Much of this book is concerned with the salient performance characteristics of a variety of subcircuits commonly used in analog circuits and of complete functional blocks made up of these subcircuits. The aspects of the performance that are of interest include the dc currents and voltages within the circuit, the effect of mismatches in device characteristics on these voltages and currents, the small-signal, low-frequency input and output resistance, and the voltage gain of the circuit. In later chapters, the high-frequency, small-signal behavior of
circuits is considered. The subcircuit or circuit under investigation is often one of considerable complexity, and the most important single principle that must be followed to achieve success in the hand analysis of such circuits is selecting the simplest possible model for the devices within the circuit that will result in the required accuracy. For example, in the case of dc analysis, hand analysis of a complex circuit is greatly simplified by neglecting certain aspects of transistor behavior, such as the output resistance, which may result in a 10 to 20 percent error in the dc currents calculated. The principal objective of hand analysis, however, is to obtain an intuitive understanding of factors affecting circuit behavior so that an iterative design procedure resulting in improved performance can be carried out. The performance of the circuit can at any point in this cycle be determined precisely by computer simulation, but this approach does not yield the intuitive understanding necessary for design.

Unfortunately, no specific rules can be formulated regarding the selection of the simplest device model for analysis. For example, in the dc analysis of bipolar biasing circuits, assuming constant base-emitter voltages and neglecting transistor output resistances often provides adequate accuracy. However, certain bias circuits depend on the nonlinear relation between the collector current and base-emitter voltage to control the bias current, and the assumption of a constant $V_{B E}$ will result in gross errors in the analyses of these circuits. When analyzing the active-load stages in Chapter 4, the output resistance must be considered to obtain meaningful results. Therefore, a key step in every analysis is to inspect the circuit to determine what aspects of the behavior of the transistors strongly affect the performance of the circuit, and then simplify the model(s) to include only those aspects. This step in the procedure is emphasized in this and the following chapters.

## 3.2 Two-Port Modeling of Amplifiers

The most basic parameter of an amplifier is its gain. Since amplifiers may be connected to a wide variety of sources and loads, predicting the dependence of the gain on the source and load resistance is also important. One way to observe this dependence is to include these resistances in the amplifier analysis. However, this approach requires a completely new amplifier analysis each time the source or load resistance is changed. To simplify this procedure, amplifiers are often modeled as two-port equivalent networks. As shown in Fig. 3.3, two-port networks have four terminals and four port variables (a voltage and a current at each port). A pair of terminals is a port if the current that flows into one terminal is equal to the current that flows out of the other terminal. To model an amplifier, one port represents the amplifier input characteristics and the other represents the output. One variable at each port can be set independently. The other variable at each port is dependent on the two-port network and the independent variables. This dependence is expressed by two equations. We will focus here on the admittance-parameter equations, where the terminal currents are viewed as dependent variables controlled by the independent terminal voltages because we usually model transistors with voltage-controlled current sources. If the network is linear and
image_name:Figure 3.3 Two-port-network block diagram
description:The diagram labeled "Figure 3.3 Two-port-network block diagram" represents a two-port network system. This system consists of a single block labeled "Two-port network" which serves as the central component. The diagram illustrates the flow of electrical signals through this network using four main ports, two on each side of the block.

1. **Main Components:**
- **Two-port network block:** This is the core component of the system, responsible for processing the input signals according to the admittance-parameter equations.

2. **Flow of Information or Control:**
- The system has two input ports on the left side, labeled with voltage \( v_1 \) and current \( i_1 \), and two output ports on the right side, labeled with voltage \( v_2 \) and current \( i_2 \).
- The admittance-parameter equations describe the relationship between the input voltages and output currents, indicating that the currents \( i_1 \) and \( i_2 \) are dependent on the voltages \( v_1 \) and \( v_2 \).
- The direction of signal flow is indicated by arrows: the input current \( i_1 \) and voltage \( v_1 \) flow into the network, while the output current \( i_2 \) and voltage \( v_2 \) flow out.

3. **Labels, Annotations, and Key Indicators:**
- The ports are labeled with their respective voltages and currents (\( v_1, i_1 \) on the input side and \( v_2, i_2 \) on the output side), which help in identifying the input and output relationships.
- The diagram does not show any internal components or feedback loops, focusing instead on the external relationships defined by the admittance-parameter equations.

4. **Overall System Function:**
- The primary function of this two-port network is to model the behavior of linear systems, such as transistors, where the output currents are controlled by the input voltages. This is useful in analyzing small-signal models in electrical engineering, where understanding the interaction between voltages and currents is crucial for designing and optimizing circuits.
Figure 3.3 Two-port-network block diagram.

image_name:Figure 3.4
description:
[
name: y11, type: Resistor, value: y11, ports: {N1: v1, N2: GND}
name: y12, type: CurrentControlledCurrentSource, value: y12v2, ports: {Np: v1, Nn: GND}
name: y21, type: CurrentControlledCurrentSource, value: y21v1, ports: {Np: v2, Nn: GND}
name: y22, type: Resistor, value: y22, ports: {N1: v2, N2: GND}
]
extrainfo:The circuit represents an admittance-parameter two-port network, modeling the behavior of linear systems such as transistors. It uses small-signal analysis to relate input voltages to output currents.

contains no independent sources, the admittance-parameter equations are:

$$
\begin{align*}
i_{1} & =y_{11} v_{1}+y_{12} v_{2}  \tag{3.1}\\
i_{2} & =y_{21} v_{1}+y_{22} v_{2} \tag{3.2}
\end{align*}
$$

The voltages and currents in these equations are deliberately written as small-signal quantities because transistors behave in an approximately linear way only for small signals around a fixed operating point. An equivalent circuit for these equations is shown in Fig. 3.4. The parameters can be found and interpreted as follows:

$$
\begin{align*}
& y_{11}=\left.\frac{i_{1}}{v_{1}}\right|_{v_{2}=0}=\text { Input admittance with the output short-circuited }  \tag{3.3}\\
& y_{12}=\left.\frac{i_{1}}{v_{2}}\right|_{v_{1}=0}=\text { Reverse transconductance with the input short-circuited }  \tag{3.4}\\
& y_{21}=\left.\frac{i_{2}}{v_{1}}\right|_{v_{2}=0}=\text { Forward transconductance with the output short-circuited }  \tag{3.5}\\
& y_{22}=\left.\frac{i_{2}}{v_{2}}\right|_{v_{1}=0}=\text { Output admittance with the input short-circuited } \tag{3.6}
\end{align*}
$$

The $y_{12}$ parameter represents feedback in the amplifier. When the signal propagates back from the output to the input as well as forward from the input to the output, the amplifier is said to be bilateral. In many practical cases, especially at low frequencies, this feedback is negligible and $y_{12}$ is assumed to be zero. Then the amplifier is unilateral and characterized by the other three parameters. Since the model includes only one transconductance when $y_{12}=0, y_{21}$ is usually referred to simply as the short-circuit transconductance, which will be represented by $G_{m}$ in this book. When an amplifier is unilateral, the calculation of $y_{11}$ is simplified from that given in (3.3) because the connections at the output port do not affect the input admittance when $y_{12}=0$.

Instead of calculating $y_{11}$ and $y_{22}$, we will often calculate the reciprocals of these parameters, or the input and output impedances $Z_{i}=1 / y_{11}$ and $Z_{o}=1 / y_{22}$, as shown in the unilateral two-port model of Fig. 3.5a. Also, instead of calculating the short-circuit transconductance $G_{m}=y_{21}$, we will sometimes calculate the open-circuit voltage gain $a_{v}$. This substitution is justified by conversion of the Norton-equivalent output model shown in Fig. 3.5a to the Thévenin-equivalent output model shown in Fig. 3.5b. In general, finding any two of the three parameters including $G_{m}, Z_{o}$, and $a_{v}$ specifies the third parameter because

$$
\begin{equation*}
a_{v}=\left.\frac{v_{2}}{v_{1}}\right|_{i_{2}=0}=-G_{m} Z_{o} \tag{3.7}
\end{equation*}
$$

Once two of these parameters and the input impedance are known, calculation of the effects of loading at the input and output ports is possible. At low frequencies, the input and output impedances are usually dominated by resistances. Therefore, we will characterize the lowfrequency behavior of many amplifiers in this book by finding the input and output resistances, $R_{i}$ and $R_{o}$, as well as $G_{m}$ or $a_{v}$.
image_name:(a)
description:
[
name: Zi, type: Resistor, value: Zi, ports: {N1: V1, N2: GND}
name: Zo, type: Resistor, value: Zo, ports: {N1: V2, N2: GND}
name: Gmv1, type: VoltageControlledCurrentSource, value: Gmv1, ports: {Np: V2, Nn: GND}
]
extrainfo:The circuit diagram (a) represents a unilateral two-port network with a Norton output model. It includes an input impedance Zi connected between V1 and GND, and an output impedance Zo connected between V2 and GND. The current source Gmv1 is controlled by the voltage v1 and is connected between V2 and GND.
image_name:(b)
description:
[
name: Zi, type: Resistor, value: Zi, ports: {N1: V1, N2: GND}
name: a_v1, type: VoltageControlledVoltageSource, value: a_v1, ports: {Np: X, Nn: GND}
name: Zo, type: Resistor, value: Zo, ports: {N1: X, N2: V2}
]
extrainfo:The circuit diagram (b) represents a unilateral two-port equivalent circuit with a Thévenin output model. It includes an input impedance Zi and an output impedance Zo, with a voltage-controlled voltage source a_v1 connected between the input and output sections.
Figure 3.5 Unilateral two-port equivalent circuits with (a) Norton output model

(b) Thévenin output model.
image_name:Figure 3.6
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: Ri, type: Resistor, value: Ri, ports: {N1: X, N2: GND}
name: Gmv1, type: VoltageControlledCurrentSource, value: Gmv1, ports: {Np: V2, Nn: GND}
name: Ro, type: Resistor, value: Ro, ports: {N1: V2, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: V2, N2: GND}
]
extrainfo:The circuit diagram represents a unilateral two-port equivalent circuit with a Thévenin output model. It includes an input impedance Zi and an output impedance Zo, with a voltage-controlled current source Gmv1 connected between the input and output sections. The diagram shows the flow of currents i1 and i2 through the circuit.

Figure 3.6 Example of loading at the input and output of an amplifier modeled by a two-port equivalent circuit.

#### EXAMPLE

A two-port model of a unilateral amplifier is shown in Fig. 3.6. Assume $R_{i}=1 \mathrm{k} \Omega, R_{o}=1 \mathrm{M} \Omega$, and $G_{m}=1 \mathrm{~mA} / \mathrm{V}$. Let $R_{S}$ and $R_{L}$ represent the source resistance of the input generator and load resistance, respectively. Find the low-frequency gain $v_{\mathrm{out}} / v_{\mathrm{in}}$, assuming that the input is an ideal voltage source and the output is unloaded. Repeat, assuming that $R_{S}=1 \mathrm{k} \Omega$ and $R_{L}=1 \mathrm{M} \Omega$.

The open-circuit voltage gain of the two-port amplifier model by itself from $v_{1}$ to $v_{\text {out }}$ is

$$
\left.\frac{v_{\text {out }}}{v_{1}}\right|_{R_{L} \rightarrow \infty}=\left.\frac{v_{2}}{v_{1}}\right|_{i_{2}=0}=-G_{m} R_{o}=-(1 \mathrm{~mA} / \mathrm{V})(1000 \mathrm{k} \Omega)=-1000
$$

Since the source and input resistances form a voltage divider, and since the output resistance appears in parallel with the load resistance, the overall gain from $v_{\text {in }}$ to $v_{\text {out }}$ is

$$
\frac{v_{\text {out }}}{v_{\text {in }}}=\frac{v_{1}}{v_{\text {in }}} \frac{v_{\text {out }}}{v_{1}}=-\frac{R_{i}}{R_{i}+R_{S}} G_{m}\left(R_{o} \| R_{L}\right)
$$

With an ideal voltage source at the input and no load at the output, $R_{S}=0, R_{L} \rightarrow \infty$, and $v_{\text {out }} / v_{\text {in }}=-1000$. With $R_{S}=1 \mathrm{k} \Omega$ and $R_{L}=1 \mathrm{M} \Omega$, the gain is reduced by a factor of four to $v_{\text {out }} / v_{\text {in }}=-0.5(1 \mathrm{~mA} / \mathrm{V})(500 \mathrm{k} \Omega)=-250$.

## 3.3 Basic Single-Transistor Amplifier Stages

Bipolar and MOS transistors are capable of providing useful amplification in three different configurations. In the common-emitter or common-source configuration, the signal is applied to the base or gate of the transistor and the amplified output is taken from the collector or drain.

In the common-collector or common-drain configuration, the signal is applied to the base or gate and the output signal is taken from the emitter or source. This configuration is often referred to as the emitter follower for bipolar circuits and the source follower for MOS circuits. In the common-base or common-gate configuration, the signal is applied to the emitter or the source, and the output signal is taken from the collector or the drain. Each of these configurations provides a unique combination of input resistance, output resistance, voltage gain, and current gain. In many instances, the analysis of complex multistage amplifiers can be reduced to the analysis of a number of single-transistor stages of these types.

We showed in Chapter 1 that the small-signal equivalent circuits for the bipolar and MOS transistors are very similar, with the two devices differing mainly in the values of some of their small-signal parameters. In particular, MOS transistors have essentially infinite input resistance from the gate to the source, in contrast with the finite $r_{\pi}$ of bipolar transistors. On the other hand, bipolar transistors have a $g_{m}$ that is usually an order of magnitude larger than that of MOS transistors biased with the same current. These differences often make one or the other device desirable for use in different situations. For example, amplifiers with very high input impedance are more easily realized with MOS transistors than with bipolar transistors. However, the higher $g_{m}$ of bipolar transistors makes the realization of high-gain amplifiers with bipolar transistors easier than with MOS transistors. In other applications, the exponential large-signal characteristics of bipolar transistors and the square-law characteristics of MOS transistors may each be used to advantage.

As described in Chapter 2, integrated-circuit processes of many varieties now exist. Examples include processes with bipolar or MOS transistors as the only active devices and combined bipolar and CMOS devices in BiCMOS processes. Because the more complex processes involve more masking steps and are thus somewhat more costly to produce, integrated-circuit designers generally use the simplest process available that allows the desired circuit specifications to be achieved. Therefore, designers must appreciate the similarities and differences between bipolar and MOS transistors so that appropriate choices of technology can be made.

### 3.3.1 Common-Emitter Configuration

The resistively loaded common-emitter (CE) amplifier configuration is shown in Fig. 3.7. The resistor $R_{C}$ represents the collector load resistance. The short horizontal line labeled $V_{C C}$ at the top of $R_{C}$ implies that a voltage source of value $V_{C C}$ is connected between that point and ground. This symbol will be used throughout the book. We first calculate the dc transfer characteristic of the amplifier as the input voltage is increased in the positive direction from
image_name:Figure 3.7 Resistively loaded common-emitter amplifier
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Vo}
name: Q1, type: NPN, ports: {C: Vo, B: Vi, E: GND}
]
extrainfo:The circuit is a common-emitter amplifier with the transistor Q1 configured in the forward-active region. The input voltage Vi drives the base of Q1, and the output is taken from the collector. The resistor RC serves as the collector load.
Figure 3.7 Resistively loaded common-emitter amplifier.

image_name:Figure 3.8 Large-signal equivalent circuit
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: R_C, type: Resistor, value: R_C, ports: {N1: VCC, N2: Vo}
name: D1, type: Diode, ports: {Na: Vi, Nc: GND}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name:Ic, type: CurrentSource, value: IS exp(Vbe/VT), ports: {Np: Vo, Nn: GND}
]
extrainfo:The circuit is a large-signal equivalent of a common-emitter amplifier. It includes a diode with a saturation current of IS/βF, representing the base-emitter junction of the transistor. The input voltage Vi drives the base, and the output is taken from the collector. The collector current Ic is given by the exponential relationship Ic = IS exp(Vbe/VT) = βF Ib.
Figure 3.8 Large-signal equivalent circuit valid when the transistor is in the forward-active region. The saturation current of the equivalent base-emitter diode is $I_{S} / \beta_{F}$.
zero. We assume that the base of the transistor is driven by a voltage source of value $V_{i}$. When $V_{i}$ is zero, the transistor operates in the cutoff state and no collector current flows other than the leakage current $I_{C O}$. As the input voltage is increased, the transistor enters the forward-active region, and the collector current is given by

$$
\begin{equation*}
I_{c}=I_{S} \exp \frac{V_{i}}{V_{T}} \tag{3.8}
\end{equation*}
$$

The equivalent circuit for the amplifier when the transistor operates in the forward-active region was derived in Chapter 1 and is repeated in Fig. 3.8. Because of the exponential relationship between $I_{c}$ and $V_{b e}$, the value of the collector current is very small until the input voltage reaches approximately 0.5 V . As long as the transistor operates in the forward-active region, the base current is equal to the collector current divided by $\beta_{F}$, or

$$
\begin{equation*}
I_{b}=\frac{I_{c}}{\beta_{F}}=\frac{I_{S}}{\beta_{F}} \exp \frac{V_{i}}{V_{T}} \tag{3.9}
\end{equation*}
$$

The output voltage is equal to the supply voltage, $V_{C C}$, minus the voltage drop across the collector resistor:

$$
\begin{equation*}
V_{o}=V_{C C}-I_{C} R_{C}=V_{C C}-R_{C} I_{S} \exp \frac{V_{i}}{V_{T}} \tag{3.10}
\end{equation*}
$$

When the output voltage approaches zero, the collector-base junction of the transistor becomes forward biased and the device enters saturation. Once the transistor becomes saturated, the output voltage and collector current take on nearly constant values:

$$
\begin{align*}
V_{o} & =V_{C E(\mathrm{sat})}  \tag{3.11}\\
I_{c} & =\frac{V_{C C}-V_{C E(\mathrm{sat})}}{R_{C}} \tag{3.12}
\end{align*}
$$

The base current, however, continues to increase with further increases in $V_{i}$. Therefore, the forward current gain $I_{c} / I_{b}$ decreases from $\beta_{F}$ as the transistor leaves the forward-active region of operation and moves into saturation. In practice, the current available from the signal source is limited. When the signal source can no longer increase the base current, $V_{i}$ is maximum. The output voltage and the base current are plotted as a function of the input voltage in Fig. 3.9. Note that when the device operates in the forward-active region, small changes in the input voltage can give rise to large changes in the output voltage. The circuit thus provides voltage gain. We now proceed to calculate the voltage gain in the forward-active region.
image_name:Figure 3.9
description:Figure 3.9 consists of two separate graphs that plot the output voltage ($V_o$) and base current ($I_b$) as functions of the input voltage ($V_i$) for a common-emitter circuit.

1. **Output Voltage vs. Input Voltage Graph (Top Graph):**
- **Axes Labels and Units:**
- The x-axis represents the input voltage ($V_i$) in volts (V).
- The y-axis represents the output voltage ($V_o$) in volts (V).
- **Overall Behavior and Trends:**
- The graph shows a sharp transition from a high output voltage ($V_{CC}$) to a low output voltage ($V_{CE(sat)}$) as the input voltage increases.
- The curve starts at a high level ($V_{CC}$) and remains constant until around $V_i = 0.5$ V.
- At this point, the graph sharply decreases, indicating the transition from the saturation region to the forward-active region.
- The output voltage stabilizes at $V_{CE(sat)}$ as $V_i$ increases beyond approximately 1 V, indicating the saturation region.
- **Key Features:**
- The transition between regions is marked by a steep slope, indicating the voltage gain provided by the circuit in the forward-active region.

2. **Base Current vs. Input Voltage Graph (Bottom Graph):**
- **Axes Labels and Units:**
- The x-axis represents the input voltage ($V_i$) in volts (V).
- The y-axis represents the base current ($I_b$) in amperes (A).
- **Overall Behavior and Trends:**
- The base current remains low for input voltages less than approximately 0.5 V, indicating the saturation region.
- As $V_i$ increases past 0.5 V, the base current begins to rise sharply, marking the transition to the forward-active region.
- The curve continues to rise steeply, showing that small increases in $V_i$ lead to significant increases in $I_b$.
- **Key Features:**
- The sharp increase in base current corresponds to the forward-active region, where the transistor provides amplification.
- The graph illustrates the relationship between $V_i$ and $I_b$, highlighting the sensitivity of the base current to changes in input voltage in the forward-active region.

Overall, Figure 3.9 illustrates the behavior of a common-emitter amplifier, showing how the output voltage and base current vary with input voltage, emphasizing the regions of operation and the amplification characteristics of the circuit.

Figure 3.9 Output voltage and base current as a function of $V_{i}$ for the common-emitter circuit.

While incremental performance parameters such as the voltage gain can be calculated from derivatives of the large-signal analysis, the calculations are simplified by using the small-signal hybrid- $\pi$ model for the transistor developed in Chapter 1. The small-signal equivalent circuit for the common-emitter amplifier is shown in Fig. 3.10. Here we have neglected $r_{b}$, assuming that it is much smaller than $r_{\pi}$. We have also neglected $r_{\mu}$. This equivalent circuit does not include the resistance of the load connected to the amplifier output. The collector resistor $R_{C}$ is included because it is usually present in some form as a biasing element. Our objective is to characterize the amplifier alone so that the voltage gain can then be calculated under arbitrary conditions of loading at the input and output. Since the common-emitter amplifier is unilateral when $r_{\mu}$ is neglected, we will calculate the small-signal input resistance, transconductance, and output resistance of the circuit as explained in Section 3.2.

The input resistance is the Thévenin-equivalent resistance seen looking into the input. For the CE amplifier,

$$
\begin{equation*}
R_{i}=\frac{v_{i}}{i_{i}}=r_{\pi}=\frac{\beta_{0}}{g_{m}} \tag{3.13}
\end{equation*}
$$

image_name:Figure 3.10 Small-signal equivalent circuit for the CE amplifier
description:
[
name: rπ, type: Resistor, value: rπ, ports: {N1: Vi, N2: GND}
name: gmV1, type: CurrentControlledCurrentSource, ports: {Np: Vo, Nn: GND}
name: ro, type: Resistor, value: ro, ports: {N1: Vo, N2: Vx}
name: RC, type: Resistor, value: RC, ports: {N1: Vx, N2: GND}
]
extrainfo:The circuit is a small-signal equivalent model of a common-emitter amplifier. It includes a resistor rπ at the input, a current-controlled current source gmV1, and resistors ro and RC at the output. The input voltage is vi, and the output voltage is vo.

Figure 3.10 Small-signal equivalent circuit for the CE amplifier.

The transconductance $G_{m}$ is the change in the short-circuit output current per unit change of input voltage and is given by

$$
\begin{equation*}
G_{m}=\left.\frac{i_{o}}{v_{i}}\right|_{v_{o}=0}=g_{m} \tag{3.14}
\end{equation*}
$$

Equation 3.14 shows that the transconductance of the CE amplifier is equal to the transconductance of the transistor. The output resistance is the Thevenin-equivalent resistance seen looking into the output with the input shorted, or

$$
\begin{equation*}
R_{o}=\left.\frac{v_{o}}{i_{o}}\right|_{v_{i}=0}=R_{C} \| r_{o} \tag{3.15}
\end{equation*}
$$

The open-circuit, or unloaded, voltage gain is

$$
\begin{equation*}
a_{v}=\left.\frac{v_{o}}{v_{i}}\right|_{i_{o}=0}=-g_{m}\left(r_{o} \| R_{C}\right) \tag{3.16}
\end{equation*}
$$

If the collector load resistor $R_{C}$ is made very large, then $a_{v}$ becomes

$$
\begin{equation*}
\lim _{R_{C} \rightarrow \infty} a_{v}=-g_{m} r_{o}=-\frac{I_{C}}{V_{T}} \frac{V_{A}}{I_{C}}=-\frac{V_{A}}{V_{T}}=-\frac{1}{\eta} \tag{3.17}
\end{equation*}
$$

where $I_{C}$ is the dc collector current at the operating point, $V_{T}$ is the thermal voltage, $V_{A}$ is the Early voltage, and $\eta$ is given in (1.114). This gain represents the maximum low-frequency voltage gain obtainable from the transistor. It is independent of the collector bias current for bipolar transistors, and the magnitude is approximately 5000 for typical $n p n$ devices.

Another parameter of interest is the short-circuit current gain $a_{i}$. This parameter is the ratio of $i_{o}$ to $i_{i}$ when the output is shorted. For the CE amplifier,

$$
\begin{equation*}
a_{i}=\left.\frac{i_{o}}{i_{i}}\right|_{v_{o}=0}=\frac{G_{m} v_{i}}{\frac{v_{i}}{R_{i}}}=g_{m} r_{\pi}=\beta_{0} \tag{3.18}
\end{equation*}
$$

#### EXAMPLE

(a) Find the input resistance, output resistance, voltage gain, and current gain of the commonemitter amplifier in Fig. 3.11a. Assume that $I_{C}=100 \mu \mathrm{~A}, \beta_{0}=100, r_{b}=0$, and $r_{o} \rightarrow \infty$.

$$
\begin{aligned}
& R_{i}=r_{\pi}=\frac{\beta_{0}}{g_{m}} \simeq \frac{100(26 \mathrm{mV})}{100 \mu \mathrm{~A}}=26 \mathrm{k} \Omega \\
& R_{o}=R_{C}=5 \mathrm{k} \Omega \\
& a_{v}=-g_{m} R_{C} \simeq-\left(\frac{100 \mu \mathrm{~A}}{26 \mathrm{mV}}\right)(5 \mathrm{k} \Omega) \simeq-19.2 \\
& a_{i}=\beta_{0}=100
\end{aligned}
$$

(b) Calculate the voltage gain of the circuit of Fig. 3.11b. Assume that $V_{\text {BIAS }}$ is adjusted so that the dc collector current is maintained at $100 \mu \mathrm{~A}$.

$$
\begin{aligned}
v_{1} & =v_{s}\left(\frac{R_{i}}{R_{S}+R_{i}}\right) \\
v_{o} & =-G_{m} v_{1}\left(R_{o} \| R_{L}\right)=-G_{m}\left(\frac{R_{i}}{R_{S}+R_{i}}\right)\left(R_{o} \| R_{L}\right) v_{s} \\
\frac{v_{o}}{v_{s}} & =-\left(\frac{1}{260 \Omega}\right)\left(\frac{26 \mathrm{k} \Omega}{26 \mathrm{k} \Omega+20 \mathrm{k} \Omega}\right)\left[\frac{(10 \mathrm{k} \Omega)(5 \mathrm{k} \Omega)}{10 \mathrm{k} \Omega+5 \mathrm{k} \Omega}\right] \simeq-7.25
\end{aligned}
$$

image_name:Figure 3.11 (a)
description:
[
name: Q1, type: NPN, ports: {C: c1, B: b1, E: GND}
name: R_C, type: Resistor, value: 5kΩ, ports: {N1: VCC, N2: c1}
name: RS, type: Resistor, value: 20kΩ, ports: {N1: X, N2: b1}
name: RL, type: Resistor, value: 10kΩ, ports: {N1: C1, N2: GND}
name: Vbias, type: VoltageSource, ports: {Np: VBIAS, Nn: GND}
]
extrainfo:The circuit is a common-emitter amplifier with an NPN transistor Q1. The voltage gain is calculated using the given resistances and transconductance. The input voltage source is Vs, and the bias voltage is Vbias. The collector current Ic is 100 µA.
image_name:Figure 3.11 (b)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: RS, type: Resistor, value: 20 kΩ, ports: {N1: Vs, N2: V1}
name: rπ, type: Resistor, value: 26 kΩ, ports: {N1: V1, N2: GND}
name: GmV1, type: CurrentSource, value: (1/260) A/V, ports: {Np: GND, Nn: Vo}
name: RC, type: Resistor, value: 5 kΩ, ports: {N1: Vo, N2: GND}
name: RL, type: Resistor, value: 10 kΩ, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a common-emitter amplifier with a voltage gain of approximately -7.25. It includes an NPN transistor Q1, with a collector resistor RC and a load resistor RL. The input voltage source Vs is connected through a series resistor RS. The transconductance is modeled as a current source GmV1.
Figure 3.11 (a) Example amplifier circuit. (b) Circuit for calculation of voltage gain with typical source and load resistance values.

### 3.3.2 Common-Source Configuration

The resistively loaded common-source (CS) amplifier configuration is shown in Fig. 3.12a using an $n$-channel MOS transistor. The corresponding small-signal equivalent circuit is shown in Fig. 3.12b. As in the case of the bipolar transistor, the MOS transistor is cutoff for $V_{i}=0$ and thus $I_{d}=0$ and $V_{o}=V_{D D}$. As $V_{i}$ is increased beyond the threshold voltage $V_{t}$, nonzero drain current flows and the transistor operates in the active region (which is often called saturation for MOS transistors) when $V_{o}>V_{G S}-V_{t}$. The large-signal model of Fig. 1.30 can then be
image_name:(a)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vo}
name: M0, type: NMOS, ports: {S: GND, D: Vo, G: Vi}
]
extrainfo:This is a resistively loaded common-source amplifier circuit. The NMOS transistor M0 is used to amplify the input voltage Vi, with RD as the load resistor. The output voltage Vo is taken across the drain of the NMOS transistor.
Figure 3.12 (a) Resistively loaded, common-source amplifier. (b) Small-signal equivalent circuit for the common-source amplifier.

image_name:(b)
description:
[
name: g_m v_i, type: VoltageControlledCurrentSource, value: g_m v_i, ports: {Np: GND, Nn: v1}
name: r_o, type: Resistor, value: r_o, ports: {N1: v2, N2: GND}
name: R_D, type: Resistor, value: R_D, ports: {N1: v3, N2: GND}
]
extrainfo:This circuit is a small-signal equivalent of a resistively loaded common-source amplifier. It includes a voltage-controlled current source (g_m v_i) representing the transconductance of the NMOS transistor, and resistors r_o and R_D representing the output resistance and load resistance, respectively. The input voltage is vi and the output voltage is vo.

(b)
used together with (1.157) to derive

$$
\begin{align*}
V_{o} & =V_{D D}-I_{d} R_{D}  \tag{3.19}\\
& =V_{D D}-\frac{\mu_{n} C_{o x}}{2} \frac{W}{L} R_{D}\left(V_{i}-V_{t}\right)^{2} \tag{3.20}
\end{align*}
$$

The output voltage is equal to the drain-source voltage and decreases as the input increases. When $V_{o}<V_{G S}-V_{t}$, the transistor enters the triode region, where its output resistance becomes low and the small-signal voltage gain drops dramatically. In the triode region, the output voltage can be calculated by using (1.152) in (3.19). These results are illustrated in the plot of Fig. 3.13. The slope of this transfer characteristic at any operating point is the small-signal
image_name:Figure 3.13
description:The graph in Figure 3.13 is a plot of output voltage \( V_o \) versus input voltage \( V_i \) for a common-source MOSFET amplifier circuit. The x-axis represents the input voltage \( V_i \) in volts (V), while the y-axis represents the output voltage \( V_o \) in volts (V). The graph is divided into three distinct regions: the cutoff region, the active region, and the triode region.

1. **Cutoff Region:**
- This region is on the left side of the graph, where the input voltage \( V_i \) is less than the threshold voltage \( V_t \). In this region, the output voltage \( V_o \) is constant and equal to the supply voltage \( V_{DD} \). The transistor is off, and no current flows through it.

2. **Active Region:**
- As the input voltage \( V_i \) increases past \( V_t \), the transistor enters the active region. Here, the output voltage \( V_o \) decreases as the input voltage increases. This region is characterized by a negative slope, indicating that the small-signal voltage gain is negative. The MOSFET operates in saturation, providing amplification.

3. **Triode Region:**
- When the input voltage \( V_i \) increases further, the transistor enters the triode region. In this region, the output voltage \( V_o \) falls rapidly, and the slope of the curve becomes steeper. The output resistance is low, and the voltage gain drops significantly.

The graph also includes annotations for key points: the threshold voltage \( V_t \) is marked on the x-axis, and the line \( V_{DS} = V_{GS} - V_t \) is shown, indicating the transition between regions. The graph provides a clear visualization of how the output voltage changes with varying input voltage, illustrating the behavior of the MOSFET in different operating regions.

Figure 3.13 Output voltage versus input voltage for the common-source circuit.
voltage gain at that point. The MOS transistor has much lower voltage gain in the active region than does the bipolar transistor; therefore, the active region for the MOS CS amplifier extends over a much larger range of $V_{i}$ than in the bipolar common-emitter amplifier.

Since the source and body of the MOS transistor both operate at ac ground, $v_{b s}=0$ in Fig. 1.36; therefore, the $g_{m b}$ generator is omitted in Fig. 3.12b. As a result, this circuit is topologically identical to the small-signal equivalent circuit for the common-emitter amplifier shown in Fig. 3.10. The CS amplifier is unilateral because it contains no feedback. Therefore, the low-frequency behavior of this circuit can be characterized using the transconductance, input resistance, and output resistance as described in Section 3.2.

The transconductance $G_{m}$ is

$$
\begin{equation*}
G_{m}=\left.\frac{i_{o}}{v_{i}}\right|_{v_{o}=0}=g_{m} \tag{3.21}
\end{equation*}
$$

Equation 3.21 shows that the transconductance of the CS amplifier is equal to the transconductance of the transistor, as in a common-emitter amplifier. Since the input of the CS amplifier is connected to the gate of an MOS transistor, the dc input current and its low-frequency, smallsignal variation $i_{i}$ are both assumed to equal zero. Under this assumption, the input resistance $R_{i}$ is

$$
\begin{equation*}
R_{i}=\frac{v_{i}}{i_{i}} \rightarrow \infty \tag{3.22}
\end{equation*}
$$

Another way to see this result is to let $\beta_{0} \rightarrow \infty$ in (3.13) because MOS transistors behave like bipolar transistors with infinite $\beta_{0}$. The output resistance is the Thévenin-equivalent resistance seen looking into the output with the input shorted, or

$$
\begin{equation*}
R_{o}=\left.\frac{v_{o}}{i_{o}}\right|_{v_{i}=0}=R_{D} \| r_{o} \tag{3.23}
\end{equation*}
$$

The open-circuit, or unloaded, voltage gain is

$$
\begin{equation*}
a_{v}=\left.\frac{v_{o}}{v_{i}}\right|_{i_{o}=0}=-g_{m}\left(r_{o} \| R_{D}\right) \tag{3.24}
\end{equation*}
$$

If the drain load resistor $R_{D}$ is replaced by a current source, $R_{D} \rightarrow \infty$ and $a_{v}$ becomes

$$
\begin{equation*}
\lim _{R_{D} \rightarrow \infty} a_{v}=-g_{m} r_{o} \tag{3.25}
\end{equation*}
$$

Equation 3.25 gives the maximum possible voltage gain of a one-stage CS amplifier. This result is identical to the first part of (3.17) for a common-emitter amplifier. In the case of the CS amplifier, however, $g_{m}$ is proportional to $\sqrt{I_{D}}$ from (1.180) whereas $r_{o}$ is inversely proportional to $I_{D}$ from (1.194). Thus, we find in (3.25) that the maximum voltage gain per stage is proportional to $1 / \sqrt{I_{D}}$. In contrast, the maximum voltage gain in the common-emitter amplifier is independent of current. A plot of the maximum voltage gain versus $I_{D}$ for a typical MOS transistor is shown in Fig. 3.14. At very low currents, the gain approaches a constant value comparable to that of a bipolar transistor. This region is sometimes called subthreshold, where the transistor operates in weak inversion and the square-law characteristic in (1.157) is no longer valid. As explained in Section 1.8, the drain current becomes an exponential function of the gate-source voltage in this region, resembling the collector-current dependence on the base-emitter voltage in a bipolar transistor.
image_name:Figure 3.14
description:The graph in Figure 3.14 illustrates the variation of maximum MOSFET voltage gain with respect to the bias current (I_D) in amperes. The x-axis represents the drain current (I_D) on a logarithmic scale, ranging from 10^{-8} A to 10^{-3} A. The y-axis represents the maximum voltage gain on a logarithmic scale, ranging from 10^1 to 10^3.

Type of Graph and Function
This is a logarithmic plot showing the relationship between MOSFET voltage gain and bias current. It delineates two distinct operating regions of a MOSFET: the subthreshold region and the square-law region.

Axes Labels and Units
- **X-axis:** Drain current (I_D) in amperes (A), logarithmic scale.
- **Y-axis:** Maximum MOSFET voltage gain, logarithmic scale.

Overall Behavior and Trends
- **Subthreshold Region:** At very low currents (approximately 10^{-8} A to 10^{-6} A), the voltage gain remains relatively constant, indicating that the MOSFET operates in the subthreshold region. Here, the gain value is high, around 10^3, similar to that of a bipolar transistor, as the gain approaches a constant value.
- **Square-law Region:** As the current increases beyond approximately 10^{-6} A, the gain begins to decrease linearly on the logarithmic scale, indicating the transition to the square-law region. This region is characterized by a decrease in gain as the current increases.

Key Features and Technical Details
- The graph shows a clear distinction between the subthreshold and square-law regions, with the gain transitioning from a high constant value to a decreasing trend.
- The transition between the regions is smooth, without abrupt changes, highlighting the continuous nature of MOSFET operation across these regions.

Annotations and Specific Data Points
- The graph is annotated to clearly indicate the subthreshold and square-law regions, providing insight into the operational behavior of MOSFETs at different bias currents.
- No specific numerical values are marked for key data points, but the logarithmic scale provides a clear understanding of the gain's magnitude and its dependence on the current.

Figure 3.14 Typical variation of maximum MOSFET voltage gain with bias current.

Using (1.194), the limiting gain given by (3.25) can also be expressed as

$$
\begin{equation*}
\lim _{R_{D} \rightarrow \infty} a_{v}=-g_{m} r_{o}=-\frac{g_{m}}{I_{D}} I_{D} r_{o}=-\frac{g_{m}}{I_{D}} V_{A} \tag{3.26}
\end{equation*}
$$

In the square-law region in Fig. 3.14, substituting (1.181) into (3.26) gives

$$
\begin{equation*}
\lim _{R_{D} \rightarrow \infty} a_{v}=-\frac{V_{A}}{\left(V_{G S}-V_{t}\right) / 2}=-\frac{2 V_{A}}{V_{o v}} \tag{3.27}
\end{equation*}
$$

where $V_{o v}=V_{G S}-V_{t}$ is the gate overdrive. Since the gate overdrive is typically an order of magnitude larger than the thermal voltage $V_{T}$, the magnitude of the maximum gain predicted by (3.27) is usually much smaller than that predicted by (3.17) for the bipolar case. Substituting (1.163) into (3.27) gives

$$
\begin{equation*}
\lim _{R_{D} \rightarrow \infty} a_{v}=-\frac{2 L_{\mathrm{eff}}}{V_{G S}-V_{t}}\left(\frac{d X_{d}}{d V_{D S}}\right)^{-1} \tag{3.28}
\end{equation*}
$$

#### EXAMPLE

Find the voltage gain of the common-source amplifier of Fig $3.12 a$ with $V_{D D}=5 \mathrm{~V}$, $R_{D}=5 \mathrm{k} \Omega, k^{\prime}=\mu_{n} C_{o x}=100 \mu \mathrm{~A} / \mathrm{V}^{2}, W=50 \mu \mathrm{~m}, L=1 \mu \mathrm{~m}, V_{t}=0.8 \mathrm{~V}, L_{d}=0, X_{d}=0$, and $\lambda=0$. Assume that the bias value of $V_{i}$ is 1 V .

To determine whether the transistor operates in the active region, we first find the dc output voltage $V_{O}=V_{D S}$. If the transistor operates in the active region, (1.157) gives

$$
I_{D}=\frac{k^{\prime}}{2} \frac{W}{L}\left(V_{G S}-V_{t}\right)^{2}=\frac{100}{2} \times 10^{-6} \times \frac{50}{1}(1-0.8)^{2}=100 \mu \mathrm{~A}
$$

Then

$$
V_{O}=V_{D S}=V_{D D}-I_{D} R_{D}=5 \mathrm{~V}-(0.1 \mathrm{~mA})(5 \mathrm{k} \Omega)=4.5 \mathrm{~V}
$$

Since $V_{D S}=4.5 \mathrm{~V}>V_{G S}-V_{t}=0.2 \mathrm{~V}$, the transistor does operate in the active region, as assumed. Then from (1.180),

$$
g_{m}=k^{\prime} \frac{W}{L}\left(V_{G S}-V_{t}\right)=100 \times 10^{-6} \times \frac{50}{1}(1-0.8)=1000 \frac{\mu \mathrm{~A}}{\mathrm{~V}}
$$

Then since $\lambda=0, V_{A} \rightarrow \infty$ and (3.24) gives

$$
a_{v}=-g_{m} R_{D}=-(1.0 \mathrm{~mA} / \mathrm{V})(5 \mathrm{k} \Omega)=-5
$$

Note that the open-circuit voltage gain here is much less than in the bipolar example in Section 3.3.1 even though the dc bias currents are equal.

### 3.3.3 Common-Base Configuration

In the common-base (CB) configuration, ${ }^{4}$ the input signal is applied to the emitter of the transistor, and the output is taken from the collector. The base is tied to ac ground. The commonbase connection is shown in Fig. 3.15. While the connection is not as widely used as the common-emitter amplifier, it has properties that make it useful in certain circumstances. In this section, we calculate the small-signal properties of the common-base stage.

The hybrid- $\pi$ model provides an accurate representation of the small-signal behavior of the transistor independent of the circuit configuration. For the common-base stage, however, the hybrid- $\pi$ model is somewhat cumbersome because the dependent current source is connected between the input and output terminals. ${ }^{4}$ The analysis of common-base stages can be simplified if the model is modified as shown in Fig. 3.16. The small-signal hybrid- $\pi$ model is shown in Fig. 3.16a. First note that the dependent current source flows from the collector terminal to the emitter terminal. The circuit behavior is unchanged if we replace this single current source with two current sources of the same value, one going from the collector to the base and the other going from the base to the emitter, as shown in Fig. 3.16b. Since the currents fed into and removed from the base are equal, the equations that describe the operation of these circuits are identical. We next note that the controlled current source connecting the base and emitter is controlled by the voltage across its own terminals. Therefore, by the application of Ohm's law to this branch, this dependent current source can be replaced by a resistor of value $1 / g_{m}$. This resistance appears in parallel with $r_{\pi}$, and the parallel combination of the two is called the emitter resistance $r_{e}$.

$$
\begin{equation*}
r_{e}=\frac{1}{g_{m}+\frac{1}{r_{\pi}}}=\frac{1}{g_{m}\left(1+\frac{1}{\beta_{0}}\right)}=\frac{\alpha_{0}}{g_{m}} \tag{3.29}
\end{equation*}
$$

The new equivalent circuit is called the $T$ model and is shown in Fig. 3.16c. It has terminal properties exactly equivalent to those of the hybrid- $\pi$ model but is often more convenient to use for common-base calculations. For dc and low input frequencies, the capacitors $C_{\pi}$ and $C_{\mu}$ appear as high-impedance elements and can be neglected. Assume at first that $r_{b}=0$ and $r_{o} \rightarrow \infty$ so that the circuit is unilateral. When $r_{\mu}$ is also neglected, the model reduces to the simple form shown in Fig. 3.16d. Using the T model under these conditions, the small-signal
image_name:Figure 3.15 Typical common-base amplifier
description:
[
name: Q1, type: NPN, ports: {C: Vo, B: Vi, E: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Vo}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
]
extrainfo:This is a common-base amplifier circuit using an NPN transistor Q1. The input voltage Vi is applied to the base, and the output voltage Vo is taken from the collector. The resistor RC is connected between the collector and the positive supply voltage VCC.
Figure 3.15 Typical common-base amplifier.

image_name:Figure 3.16(a) Hybrid-π model
description:
[
name: r_b, type: Resistor, value: r_b, ports: {N1: B, N2: "B"}
name: r_π, type: Resistor, value: r_π, ports: {N1: "B", N2: E}
name: C_π, type: Capacitor, value: C_π, ports: {Np: "B", Nn: E}
name: C_μ, type: Capacitor, value: C_μ, ports: {Np: "B", Nn: C}
name: r_μ, type: Resistor, value: r_μ, ports: {N1: "B", N2: C}
name: g_m v_1, type: CurrentSource, value: g_m v_1', ports: {Np: C, Nn: E}
name: r_o, type: Resistor, value: r_o, ports: {N1: C, N2: E}
]
extrainfo:This circuit is a representation of the hybrid-pi model for a transistor. It includes resistors, capacitors, and a controlled current source to model the behavior of the transistor. The input is at the base node B, and the output is at the collector node C.
image_name:(b)The collector current source gmv1 is changed to two current sources in series, and the point between them attached to the base. This change does not affect the current flowing in the base.
description:
[
name: r_b, type: Resistor, value: r_b, ports: {N1: B, N2: "B"}
name: r_π, type: Resistor, value: r_π, ports: {N1: "B", N2: E}
name: C_π, type: Capacitor, value: C_π, ports: {Np: "B", Nn: E}
name: g_mv_1, type: CurrentControlledCurrentSource, ports: {Np: C, Nn: E}
name: C_μ, type: Capacitor, value: C_μ, ports: {Np: "B", Nn: C}
name: r_μ, type: Resistor, value: r_μ, ports: {N1: "B'", N2: C}
name: r_o, type: Resistor, value: r_o, ports: {N1: C, N2: E}
]
extrainfo:This circuit is a representation of the hybrid-pi model for a transistor. It includes resistors, capacitors, and a controlled current source to model the behavior of the transistor. The input is at the base node B, and the output is at the collector node C.
image_name:(c) The current source between base and emitter is converted to a resistor of value $1 / g_{m}$.
description:
[
name: rb, type: Resistor, value: rb, ports: {N1: b, N2: "b"}
name: re, type: Resistor, value: re, ports: {N1: "b", N2: e}
name: rμ, type: Resistor, value: rμ, ports: {N1: "b", N2: c}
name: ro, type: Resistor, value: ro, ports: {N1: c, N2: e}
name: Cμ, type: Capacitor, value: Cμ, ports: {Np: "b", Nn: c}
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: "b", Nn: e}
name: gmv1, type: VoltageControlledCurrentSource, ports: {Np: c, Nn: "b"}
]
extrainfo:This circuit is a hybrid-π model of a transistor, representing the small-signal model with resistors, capacitors, and a voltage-controlled current source. The base node is labeled as 'b', the collector as 'c', and the emitter as 'e'. The model includes resistances rb, re, rμ, and ro, and capacitances Cμ and Cπ, with a controlled current source gmv1 connected between nodes c and b'.
image_name:(d)
description:This diagram represents the transformation of a hybrid-π model of an NPN transistor to a T model for low frequencies. The transformation involves replacing the current source between the base and emitter with a resistor of value 1/gm. The collector current source gmv1 is represented in the T model.
Figure 3.16 Generation of emitter-current-controlled T model from the hybrid- $\pi$. (a) Hybrid- $\pi$ model. (b) The collector current source $g_{m} v_{1}$ is changed to two current sources in series, and the point between them attached to the base. This change does not affect the current flowing in the base. (c) The current source between base and emitter is converted to a resistor of value $1 / g_{m}$. (d) T model for low frequencies, neglecting $r_{o}, r_{\mu}$, and the charge-storage elements.

image_name:Figure 3.17
description:
[
name: re, type: Resistor, value: re, ports: {N1: vi, N2: GND}
name: gmve, type: VoltageControlledCurrentSource, value: gmve, ports: {Np: vo, Nn: GND}
name: RC, type: Resistor, value: RC, ports: {N1: vo, N2: GND}
]
extrainfo:The circuit is a small-signal equivalent of a common-base stage with negligible ro, rb, and rmu. It includes an input resistance re, a voltage-controlled current source gmve, and an output resistance RC.

Figure 3.17 Small-signal equivalent circuit of the common-base stage; $r_{o}$, $r_{b}$, and $r_{\mu}$ are assumed negligible.
equivalent circuit of the common-base stage is shown in Fig. 3.17. By inspection of Fig. 3.17, the short-circuit transconductance is

$$
\begin{equation*}
G_{m}=g_{m} \tag{3.30}
\end{equation*}
$$

The input resistance is just the resistance $r_{e}$ :

$$
\begin{equation*}
R_{i}=r_{e} \tag{3.31}
\end{equation*}
$$

The output resistance is given by

$$
\begin{equation*}
R_{o}=R_{C} \tag{3.32}
\end{equation*}
$$

Using these parameters, the open-circuit voltage gain and the short-circuit current gain are

$$
\begin{align*}
& a_{v}=G_{m} R_{o}=g_{m} R_{C}  \tag{3.33}\\
& a_{i}=G_{m} R_{i}=g_{m} r_{e}=\alpha_{0} \tag{3.34}
\end{align*}
$$

Comparing (3.31) and (3.13) shows that the input resistance of the common-base configuration is a factor of $\left(\beta_{0}+1\right)$ less than in the common-emitter configuration. Also, comparing (3.34) and (3.18) shows that the current gain of the common-base configuration is reduced by a factor of $\left(\beta_{0}+1\right)$ compared to that of the common-emitter configuration.

Until now, we have assumed that $r_{b}$ is negligible. In practice, however, the base resistance has a significant effect on the transconductance and the input resistance when the common-base stage is operated at sufficiently high current levels. To recalculate these parameters with $r_{b}>0$, assume the transistor operates in the forward-active region and consider the small-signal model shown in Fig. 3.18. Here, the transconductance is

$$
\begin{equation*}
G_{m}=\left.\frac{i_{o}}{v_{i}}\right|_{v_{o}=0}=g_{m}\left(\frac{v_{e}}{v_{i}}\right) \tag{3.35}
\end{equation*}
$$

To find the relationship between $v_{e}$ and $v_{i}$, Kirchoff's current law (KCL) and Kirchoff's voltage law (KVL) can be applied at the internal base node (node (1) and around the input loop, respectively. From KCL at node (1),

$$
\begin{equation*}
g_{m} v_{e}+\frac{v_{b}}{r_{b}}-\frac{v_{e}}{r_{e}}=0 \tag{3.36}
\end{equation*}
$$

image_name:Figure 3.18 Small-signal model of the common-base stage with r_{b}>0
description:
[
name: re, type: Resistor, value: re, ports: {N1: Vi, N2: Vb}
name: rb, type: Resistor, value: rb, ports: {N1: Vb, N2: GND}
name: RC, type: Resistor, value: RC, ports: {N1: Vo, N2: GND}
name: gmve, type: VoltageControlledCurrentSource, ports: {Np: Vo, Nn: Vb}
]
extrainfo:The circuit is a small-signal model of a common-base stage with r_b > 0. It includes resistors re, rb, RC, and a voltage-controlled current source gmve. The input voltage is Vi and the output voltage is Vo.

Figure 3.18 Small-signal model of the common-base stage with $r_{b}>0$.

From KVL around the input loop,

$$
\begin{equation*}
v_{i}=v_{e}+v_{b} \tag{3.37}
\end{equation*}
$$

Solving (3.37) for $v_{b}$, substituting into (3.36), and rearranging gives

$$
\begin{equation*}
\frac{v_{i}}{v_{e}}=1+\frac{g_{m}}{\beta_{0}} r_{b}=1+\frac{r_{b}}{r_{\pi}} \tag{3.38}
\end{equation*}
$$

Substituting (3.38) into (3.35) gives

$$
\begin{equation*}
G_{m}=\frac{g_{m}}{1+\frac{r_{b}}{r_{\pi}}} \tag{3.39}
\end{equation*}
$$

Similarly, the input resistance in Fig. 3.18 is

$$
\begin{equation*}
R_{i}=\frac{v_{i}}{i_{i}}=\frac{v_{i}}{v_{e} / r_{e}}=r_{e}\left(\frac{v_{i}}{v_{e}}\right) \tag{3.40}
\end{equation*}
$$

Substituting (3.38) into (3.40) gives

$$
\begin{equation*}
R_{i}=r_{e}\left(1+\frac{r_{b}}{r_{\pi}}\right)=\frac{\alpha_{0}}{g_{m}}\left(1+\frac{r_{b}}{r_{\pi}}\right) \tag{3.41}
\end{equation*}
$$

Thus if the dc collector current is large enough that $r_{\pi}$ is comparable with $r_{b}$, then the effects of base resistance must be included. For example, if $r_{b}=100 \Omega$ and $\beta_{0}=100$, then a collector current of 26 mA makes $r_{b}$ and $r_{\pi}$ equal.

The main motivation for using common-base stages is twofold. First, the collector-base capacitance does not cause high-frequency feedback from output to input as in the commonemitter amplifier. As described in Chapter 7, this change can be important in the design of high-frequency amplifiers. Second, as described in Chapter 4, the common-base amplifier can achieve much larger output resistance than the common-emitter stage in the limiting case where $R_{C} \rightarrow \infty$. As a result, the common-base configuration can be used as a current source whose current is nearly independent of the voltage across it.

### 3.3.4 Common-Gate Configuration

In the common-gate configuration, the input signal is applied to the source of the transistor, and the output is taken from the drain while the gate is connected to ac ground. This configuration is shown in Fig. 3.19, and its behavior is similar to that of a common-base stage.

As in the analysis of common-base amplifiers in Section 3.3.3, the analysis of commongate amplifiers can be simplified if the model is changed from a hybrid- $\pi$ configuration to a T model, as shown in Fig. 3.20. In Fig. 3.20a, the low-frequency hybrid- $\pi$ model is shown. Note that both transconductance generators are now active. If the substrate or body connection is assumed to operate at ac ground, then $v_{b s}=v_{g s}$ because the gate also operates at ac ground.
image_name:Figure 3.19 Common-gate configuration
description:
[
name: M1, type: NMOS, ports: {S: Vi, D: Vo, G: GND}
name: RD, type: Resistor, value: RD, ports: {N1: Vo, N2: VDD}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a common-gate amplifier configuration using an NMOS transistor. The input is applied to the source of the NMOS, and the output is taken from the drain. The gate is connected to ground, making it a common-gate configuration. RD is the load resistor connected to VDD.

image_name:(a)
description:
[
name: ro, type: Resistor, value: ro, ports: {N1: S, N2: D}
name: gmVgs, type: CurrentSource, value: gmVgs, ports: {Np: S, Nn: D}
name: gmbVbs, type: CurrentSource, value: gmbVbs, ports: {Np: S, Nn: D}
]
extrainfo:The circuit diagram (a) represents a low-frequency hybrid-π model of an NMOS transistor. It shows two dependent current sources, gmVgs and gmbVbs, connected in parallel with a resistor ro between the source (S) and drain (D). This configuration is used for small-signal analysis of MOSFETs.
image_name:(b)
description:
[
name: r_o, type: Resistor, value: r_o, ports: {N1: S, N2: D}
name: (g_m + g_mb) v_sg, type: CurrentSource, value: (g_m + g_mb) v_sg, ports: {Np: S, Nn: D}
]
extrainfo:The circuit diagram (b) represents a simplified model where two dependent current sources have been combined into a single current source with value (g_m + g_mb) v_sg. This configuration is part of a conversion process from a hybrid-π model to a T model for low-frequency analysis.
image_name:(c)
description:
[
name: ro, type: Resistor, value: ro, ports: {N1: S, N2: D}
name: (gm+gmb)Vsg, type: CurrentSource, value: (gm+gmb)Vsg, ports: {Np: S, Nn: GND}
name: (gm+gmb)Vsg, type: CurrentSource, value: (gm+gmb)Vsg, ports: {Np: D, Nn: GND}
]
extrainfo:The circuit diagram (c) represents a simplified model of a transistor using a combination of resistors and current sources. It includes a resistor 'ro' between the source (S) and drain (D), and two dependent current sources labeled '(gm+gmb)Vsg'. One current source is connected from the source to ground, and the other from the drain to ground. This configuration is part of a common-gate amplifier model.
image_name:(d)
description:
[
name: ro, type: Resistor, value: ro, ports: {N1: S, N2: D}
name: (gm+gmb)vsg, type: CurrentSource, value: (gm+gmb)vsg, ports: {Np: G(GND), Nn: D}
name: 1/(gm+gmb), type: Resistor, value: 1/(gm+gmb), ports: {N1: S, N2: GND}
]
extrainfo:The circuit diagram (d) represents a simplified T model of a transistor. It consists of resistors and current sources that model the behavior of the transistor in terms of its transconductance and output resistance. The source is connected to a resistor and a current source, while the drain is connected to another current source. The gate is grounded.

Figure 3.20 Conversion from hybrid- $\pi$ to T model. (a) Low-frequency hybrid- $\pi$ model. (b) The two dependent sources are combined. (c) The combined source is converted into two sources. (d) The current source between the source and gate is converted into a resistor.

Therefore, in Fig. 3.20b, the two dependent current sources are combined. In Fig. 3.20c, the combined current source from the source to the drain is replaced by two current sources: one from the source to the gate and the other from the gate to the drain. Since equal currents are pushed into and pulled out of the gate, the equations that describe the operation of the circuits in Figs. 3.20b and 3.20 c are identical. Finally, because the current source from the source to the gate is controlled by the voltage across itself, it can be replaced by a resistor of value $1 /\left(g_{m}+g_{m b}\right)$, as in Fig. 3.20d.

If $r_{o}$ is finite, the circuit of Fig. 3.20d is bilateral because of feedback provided through $r_{o}$. At first, we will assume that $r_{o} \rightarrow \infty$ so that the circuit is unilateral. Using the T model under these conditions, the small-signal equivalent circuit of the common-gate stage is shown in Fig. 3.21. By inspection of Fig. 3.21,

$$
\begin{gather*}
G_{m}=g_{m}+g_{m b}  \tag{3.42}\\
R_{i}=\frac{1}{g_{m}+g_{m b}}  \tag{3.43}\\
R_{o}=R_{D} \tag{3.44}
\end{gather*}
$$

image_name:Figure 3.21
description:
[
name: 1/gm+gmb, type: Resistor, value: 1/gm+gmb, ports: {N1: vi, N2: GND}
name: (gm+gmb)vsg, type: CurrentSource, value: (gm+gmb)vsg, ports: {Np: Vo, Nn: GND}
name: RD, type: Resistor, value: RD, ports: {N1: Vo, N2: vo}
]
extrainfo:The circuit represents a small-signal equivalent of a common-gate stage with a current source and resistors. It assumes ro is negligible, making the circuit unilateral. The input is at node vi, and the output is at node vo.

Figure 3.21 Small-signal equivalent circuit of the common-gate stage; $r_{o}$ is assumed negligible.

Using these parameters, the open-circuit voltage gain and the short-circuit current gain are

$$
\begin{align*}
& a_{v}=G_{m} R_{o}=\left(g_{m}+g_{m b}\right) R_{D}  \tag{3.45}\\
& a_{i}=G_{m} R_{i}=1 \tag{3.46}
\end{align*}
$$

### 3.3.5 Common-Base and Common-Gate Configurations with Finite $r_{o}$

In calculating the expressions for $G_{m}, R_{i}$, and $R_{o}$ of the common-base and common-gate amplifiers, we have neglected the effects of $r_{o}$. Since $r_{o}$ is connected from each amplifier output back to its input, finite $r_{o}$ causes each circuit to be bilateral, making the input resistance depend on the connection at the amplifier output. Let $R=R_{C}$ in Fig. 3.17 or $R=R_{D}$ in Fig. 3.21, depending on which circuit is under consideration. When $R$ becomes large enough that it is comparable with $r_{o}, r_{o}$ must be included in the small-signal model to accurately predict not only the input resistance, but also the output resistance. On the other hand, since the transconductance is calculated with the output shorted, the relationship between $r_{o}$ and $R$ has no effect on this calculation, and the effect of finite $r_{o}$ on transconductance can be ignored if $r_{o} \gg 1 / G_{m}$.

3.3.5.1 Common-Base and Common-Gate Input Resistance

Figure 3.22a shows a small-signal T model of a common-base or common-gate stage including finite $r_{o}$, where $R_{i(\text { ideal })}$ is given by (3.31) for a common-base amplifier or by (3.43) for a common-gate amplifier. Also, $R$ represents $R_{C}$ in Fig. 3.17 or $R_{D}$ in Fig. 3.21. Connections to the load and the input source are shown in Fig. 3.22a to include their contributions to the input and output resistance, respectively. In Fig. $3.22 a$, the input resistance is $R_{i}=v_{1} / i_{i}$. To find the input resistance, a simplified equivalent circuit such as in Fig. $3.22 b$ is often used. Here, a test voltage source $v_{t}$ is used to drive the amplifier input, and the resulting test current $i_{t}$ is calculated. KCL at the output node in Fig. $3.22 b$ gives

$$
\begin{equation*}
\frac{v_{o}}{R \| R_{L}}+\frac{v_{o}-v_{t}}{r_{o}}=G_{m} v_{t} \tag{3.47}
\end{equation*}
$$

KCL at the input in Fig. $3.22 b$ gives

$$
\begin{equation*}
i_{t}=\frac{v_{t}}{R_{i(\text { ideal })}}+\frac{v_{t}-v_{o}}{r_{o}} \tag{3.48}
\end{equation*}
$$

Solving (3.47) for $v_{o}$ and substituting into (3.48) gives

$$
\begin{equation*}
\frac{i_{t}}{v_{t}}=\frac{1}{R_{i(\text { ideal })}}+\frac{1}{r_{o}}\left(1-\frac{G_{m}+\frac{1}{r_{o}}}{\frac{1}{R \| R_{L}}+\frac{1}{r_{o}}}\right) \tag{3.49}
\end{equation*}
$$

image_name:Figure 3.22 (a)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: VS, N2: X1}
name: VS, type: VoltageSource, value: VS, ports: {Np: VS, Nn: GND}
name: Ri, type: Resistor, value: Ri, ports: {N1: X1, N2: GND}
name: ro, type: Resistor, value: ro, ports: {N1: X1, N2: X2}
name: GmV1, type: VoltageControlledCurrentSource, value: GmV1, ports: {Np: X2, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: X2, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: X2, N2: GND}
]
extrainfo:The circuit is a model of a common-base and common-gate amplifier with finite output resistance ro. It includes an input generator model, an amplifier model, and a load model. The amplifier model consists of an ideal input resistance Ri, a finite output resistance ro, and a voltage-controlled current source GmV1. The load model includes the load resistance RL.
(a)

image_name:(b)
description:
[
name: Vt, type: VoltageSource, ports: {Np: Vt, Nn: GND}
name: Ri, type: Resistor, value: Ri, ports: {N1: Vt, N2: X1}
name: Ro, type: Resistor, value: Ro, ports: {N1: X1, N2: X2}
name: Gmv1, type: VoltageControlledCurrentSource, value: Gmv1, ports: {Np: X2, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: X2, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: X2, N2: GND}
]
extrainfo:The circuit is a model of a common-base and common-gate amplifier with finite output resistance ro. It includes an input generator model, an amplifier model, and a load model. The amplifier model consists of an ideal input resistance Ri, a finite output resistance ro, and a voltage-controlled current source GmV1. The load model includes the load resistance RL.
image_name:(c)
description:
[
name: Vt, type: VoltageSource, value: Vt, ports: {Np: X2, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: X1}
name: Ri, type: Resistor, value: Ri, ports: {N1: X1, N2: GND}
name: ro, type: Resistor, value: ro, ports: {N1: X1, N2: X2}
name: Gmv1, type: VoltageControlledCurrentSource, value: Gmv1, ports: {Np: X2, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: X2, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: X2, N2: GND}
]
extrainfo:The circuit is a model of a common-base and common-gate amplifier with finite output resistance ro. It includes an input generator model, an amplifier model, and a load model. The amplifier model consists of an ideal input resistance Ri, a finite output resistance ro, and a voltage-controlled current source GmV1. The load model includes the load resistance RL.
Figure 3.22 (a) Model of common-base and common-gate amplifiers with finite $r_{o}$, showing connections to the input source and load. (b) Equivalent circuit for calculation of $R_{i}$. (c) Equivalent circuit for calculation of $R_{o}$.

Rearranging (3.49) gives

$$
\begin{equation*}
R_{i}=\frac{v_{t}}{i_{t}}=\frac{r_{o}+R \| R_{L}}{1-G_{m}\left(R \| R_{L}\right)+\frac{r_{o}+R \| R_{L}}{R_{i(\mathrm{ideal})}}} \tag{3.50}
\end{equation*}
$$

Common-Base Input Resistance. For the common-base amplifier, $G_{m}=g_{m}$ from (3.30), and $R_{i \text { (ideal) }}=r_{e}=\alpha_{0} / g_{m}$ from (3.31). Substituting (3.30) and (3.31) into (3.50) with $R=R_{C}$ and rearranging gives

$$
\begin{equation*}
R_{i}=\frac{v_{t}}{i_{t}}=\frac{r_{o}+R_{C} \| R_{L}}{1+\frac{g_{m}\left(R_{C} \| R_{L}\right)}{\beta_{0}}+\frac{g_{m} r_{o}}{\alpha_{0}}}=\frac{r_{o}+R_{C} \| R_{L}}{1+\frac{g_{m}}{\beta_{0}}\left(R_{C} \| R_{L}+\left(\beta_{0}+1\right) r_{o}\right)} \tag{3.51}
\end{equation*}
$$

From (3.51), when $\left(\beta_{0}+1\right) r_{o} \gg R_{C} \| R_{L}$,

$$
\begin{equation*}
R_{i} \simeq \frac{r_{o}+R_{C} \| R_{L}}{1+\frac{g_{m} r_{o}}{\alpha_{0}}} \tag{3.52}
\end{equation*}
$$

From (3.52), when $g_{m} r_{o} \gg \alpha_{0}$,

$$
\begin{equation*}
R_{i} \simeq \frac{\alpha_{0}}{g_{m}}+\frac{\alpha_{0}\left(R_{C} \| R_{L}\right)}{g_{m} r_{o}}=r_{e}+\frac{\alpha_{0}\left(R_{C} \| R_{L}\right)}{g_{m} r_{o}} \tag{3.53}
\end{equation*}
$$

The first term on the right side of (3.53) is the same as in (3.31), where the common-base amplifier was unilateral because infinite $r_{o}$ was assumed. The second term shows that the input resistance now depends on the connection to the output (because finite $r_{o}$ provides feedback and makes the amplifier bilateral). The second term is about equal to the resistance at the amplifier output divided by the $G_{m} r_{o}$ product. When $r_{o} \gg\left(R_{C} \| R_{L}\right)$, the effect of the second term can be neglected.

Common-Gate Input Resistance. For the common-gate amplifier, $G_{m}=\left(g_{m}+g_{m b}\right)$ from (3.42) and $R_{i(\text { ideal })}=1 /\left(g_{m}+g_{m b}\right)$ from (3.43). Substituting (3.42) and (3.43) into (3.50) with $R=R_{D}$ and rearranging gives

$$
\begin{equation*}
R_{i}=\frac{v_{t}}{i_{t}}=\frac{r_{o}+R_{D} \| R_{L}}{1+\left(g_{m}+g_{m b}\right) r_{o}} \tag{3.54}
\end{equation*}
$$

When $\left(g_{m}+g_{m b}\right) r_{o} \gg 1$,

$$
\begin{equation*}
R_{i} \simeq \frac{1}{g_{m}+g_{m b}}+\frac{R_{D} \| R_{L}}{\left(g_{m}+g_{m b}\right) r_{o}} \tag{3.55}
\end{equation*}
$$

The first term on the right side of (3.55) is the same as in (3.43), where the common-gate amplifier was unilateral because infinite $r_{o}$ was assumed. The second term is about equal to the resistance at the amplifier output divided by the $G_{m} r_{o}$ product and shows the effect of finite $r_{o}$, which makes the circuit bilateral. When $r_{o} \gg\left(R_{D} \| R_{L}\right)$, the effect of the second term can be neglected. Neglecting the second term usually causes only a small error when $R_{D}$ here or $R_{C}$ in the common-base case is built as a physical resistor even if the amplifier is unloaded $\left(R_{L} \rightarrow \infty\right)$. However, when $R_{D}$ or $R_{C}$ is replaced by a transistor current source, the effect of the second term can be significant. Chapter 4 describes techniques used to construct transistor current sources that can have very high equivalent resistance.

3.3.5.2 Common-Base and Common-Gate Output Resistance

The output resistance in Fig. 3.22a is $R_{o}=v_{o} / i_{o}$ with $v_{s}=0$. For this calculation, consider the equivalent circuit shown in Fig. 3.22c, where $v_{s}=0$. A test voltage $v_{t}$ is used to drive the amplifier output, and the resulting test current $i_{t}$ can be calculated. Since $R$ appears in parallel with the amplifier output, the calculation will be done in two steps. First, the output resistance with $R \rightarrow \infty$ is calculated. Second, this result is placed in parallel with $R$ to give the overall output resistance. From KCL at the input node in Fig. 3.22c,

$$
\begin{equation*}
\frac{v_{1}}{R_{S}}+\frac{v_{1}}{R_{i \text { (ideal })}}+\frac{v_{1}-v_{t}}{r_{o}}=0 \tag{3.56}
\end{equation*}
$$

With $R \rightarrow \infty, \mathrm{KCL}$ at the output node gives

$$
\begin{equation*}
i_{t}=-G_{m} v_{1}+\frac{v_{t}-v_{1}}{r_{o}} \tag{3.57}
\end{equation*}
$$

Solving (3.56) for $v_{1}$ and substituting into (3.57) gives

$$
\begin{equation*}
\frac{i_{t}}{v_{t}}=\frac{1}{r_{o}}-\frac{1}{r_{o}}\left(\frac{G_{m}+\frac{1}{r_{o}}}{\frac{1}{R_{S}}+\frac{1}{R_{i(\text { ideal })}}+\frac{1}{r_{o}}}\right) \tag{3.58}
\end{equation*}
$$

Rearranging (3.58) gives

$$
\begin{equation*}
\frac{v_{t}}{i_{t}}=\frac{r_{o}\left(\frac{1}{R_{S}}+\frac{1}{R_{i(\text { ideal })}}+\frac{1}{r_{o}}\right)}{\frac{1}{R_{S}}+\frac{1}{R_{i(\text { ideal })}}-G_{m}} \tag{3.59}
\end{equation*}
$$

With finite $R$, the output resistance is

$$
\begin{equation*}
R_{o}=R\left\|\left(\frac{v_{t}}{i_{t}}\right)=R\right\|\left[\frac{r_{o}\left(\frac{1}{R_{S}}+\frac{1}{R_{i(\mathrm{ideal})}}+\frac{1}{r_{o}}\right)}{\frac{1}{R_{S}}+\frac{1}{R_{i(\text { ideal })}}-G_{m}}\right] \tag{3.60}
\end{equation*}
$$

Common-Base Output Resistance. For the common-base amplifier, $G_{m}=g_{m}$ from (3.30) and $R_{i(\text { ideal })}=r_{e}=\alpha_{0} / g_{m}$ from (3.31). Substituting (3.30) and (3.31) into (3.60) and rearranging gives

$$
\begin{equation*}
R_{o}=R \|\left[\frac{r_{o}+R_{S}\left(1+\frac{g_{m} r_{o}}{\alpha_{0}}\right)}{1+\frac{R_{S}}{r_{\pi}}}\right] \tag{3.61}
\end{equation*}
$$

The term in brackets on the right side of (3.61) shows that the output resistance of the commonbase amplifier depends on the resistance of the input source $R_{S}$ when $r_{o}$ is finite. For example, if the input comes from an ideal voltage source, $R_{S}=0$ and

$$
\begin{equation*}
R_{o}=R \| r_{o} \tag{3.62}
\end{equation*}
$$

On the other hand, if the input comes from an ideal current source, $R_{S} \rightarrow \infty$ and

$$
\begin{equation*}
R_{o}=R \|\left[\left(\frac{1+g_{m} r_{o}}{\alpha_{0}}\right) r_{\pi}\right] \tag{3.63}
\end{equation*}
$$

From (3.61), when $R_{S} \ll r_{\pi}$,

$$
\begin{equation*}
R_{o} \simeq R \|\left[r_{o}+R_{S}\left(\frac{1+g_{m} r_{o}}{\alpha_{0}}\right)\right] \tag{3.64}
\end{equation*}
$$

From (3.64), when $g_{m} r_{o} \gg \alpha_{0}$ and $g_{m} R_{S} \gg \alpha_{0}$,

$$
\begin{equation*}
R_{o} \simeq R \|\left(\frac{g_{m} r_{o}}{\alpha_{0}} R_{S}\right) \tag{3.65}
\end{equation*}
$$

The term in parentheses in (3.65) is about equal to the input source resistance multiplied by the $G_{m} r_{o}$ product. Therefore, (3.65) and (3.53) together show that the common-base amplifier can be thought of as a resistance scaler, where the resistance is scaled up from the emitter to the collector and down from the collector to the emitter by a factor approximately equal to the $G_{m} r_{o}$ product in each case.

Common-Gate Output Resistance. For the common-gate amplifier, $G_{m}=\left(g_{m}+g_{m b}\right)$ from (3.42) and $R_{i(\text { ideal })}=1 /\left(g_{m}+g_{m b}\right)$ from (3.43). Substituting (3.42) and (3.43) into (3.60) and rearranging gives

$$
\begin{equation*}
R_{o}=R \|\left[r_{o}+R_{S}\left(1+\left(g_{m}+g_{m b}\right) r_{o}\right)\right] \tag{3.66}
\end{equation*}
$$

From (3.66), when $\left(g_{m}+g_{m b}\right) r_{o} \gg 1$ and $\left(g_{m}+g_{m b}\right) R_{S} \gg 1$,

$$
\begin{equation*}
R_{o} \simeq R \|\left(\left(g_{m}+g_{m b}\right) r_{o} R_{S}\right) \tag{3.67}
\end{equation*}
$$

The term in parentheses in (3.67) is equal to the input source resistance multiplied by the $G_{m} r_{o}$ product. Therefore, (3.67) and (3.55) together show that the common-gate amplifier is also a resistance scaler, where the resistance is scaled up from the source to the drain and down from the drain to the source by a factor approximately equal to the $G_{m} r_{o}$ product in each case.

### 3.3.6 Common-Collector Configuration (Emitter Follower)

The common-collector connection is shown in Fig. 3.23a. The distinguishing feature of this configuration is that the signal is applied to the base and the output is taken from the emitter. ${ }^{4}$ From a large-signal standpoint, the output voltage is equal to the input voltage minus the base-emitter voltage. Since the base-emitter voltage is a logarithmic function of the collector current, the base-emitter voltage is almost constant even when the collector current varies. If the base-emitter voltage were exactly constant, the output voltage of the common-collector amplifier would be equal to the input voltage minus a constant offset, and the small-signal gain of the circuit would be unity. For this reason, the circuit is also known as an emitter follower because the emitter voltage follows the base voltage. In practice, the base-emitter voltage is not exactly constant if the collector current varies. For example, (1.82) shows that the base-emitter voltage must increase by about 18 mV to double the collector current and by about 60 mV to increase the collector current by a factor of 10 at room temperature. Furthermore, even if the collector current were exactly constant, the base-emitter voltage depends to some extent on the collector-emitter voltage if the Early voltage is finite. These effects are most easily studied using small-signal analysis.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: b1, E: v0}
name: RS, type: Resistor, value: RS, ports: {N1: vs, N2: x}
name: RL, type: Resistor, value: RL, ports: {N1: v0, N2: GND}
name: Ri, type: Resistor, value: Ri, ports: {N1: b1, N2: GND}
name: R0, type: Resistor, value: R0, ports: {N1: v0, N2: vo}
name: ro, type: Resistor, value: ro, ports: {N1: v0, N2: GND}
name: vs, type: VoltageSource, value: vs, ports: {Np: vs, Nn: GND}
name: Vbias, type: VoltageSource, value: Vbias, ports: {Np: b1, Nn: GND}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: VEE, type: VoltageSource, value: VEE, ports: {Np: GND, Nn: v0}
name: gmv1=βoii, type: CurrentControlledCurrentSource, ports: {Np: v0, Nn: GND}
]
extrainfo:The circuit is a common-collector configuration with a small-signal equivalent circuit. It includes a voltage divider biasing and emitter follower configuration. The input voltage is applied at 'vs', and the output is taken at 'vo'. The circuit is designed to study the effects of varying collector current and base-emitter voltage.
image_name:(b)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: Vs, N2: Vi}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
name: Ri, type: Resistor, value: Ri, ports: {N1: Vi, N2: V1}
name: Rπ, type: Resistor, value: Rπ, ports: {N1: V1, N2: Vo}
name: ro, type: Resistor, value: ro, ports: {N1: GND, N2: Vo}
name: Ro, type: Resistor, value: Ro, ports: {N1: Vo, N2: Vo+}
name: Q1, type: NPN, ports: {C: VCC, B: Vi, E: Vo}
name: Vbias, type: VoltageSource, value: Vbias, ports: {Np: Vbias, Nn: GND}
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: gmv1=βoIi, type: VoltageControlledCurrentSource, ports: {Np: V1, Nn: Vo}
]
extrainfo:The circuit represents a small-signal equivalent model of an emitter-follower configuration with a common-collector connection. The input voltage Vs is applied through Rs, and the output is taken across Ro and RL. The transistor Q1 is modeled using the hybrid-pi model with parameters Rπ and ro. The controlled current source gmv1=βoIi models the transconductance of the transistor.

Figure 3.23 (a) Common-collector configuration. (b) Small-signal equivalent circuit of the emitterfollower circuit including $R_{L}$ and $R_{S}$.

The appropriate small-signal transistor model is the hybrid- $\pi$, and the small-signal equivalent circuit is shown in Fig. 3.23b. When the input voltage $v_{s}$ increases, the base-emitter voltage of the transistor increases, which increases the output current $i_{o}$. However, increasing $i_{o}$ increases the output voltage $v_{o}$, which decreases the base-emitter voltage by negative feedback. Negative feedback is covered thoroughly in Chapter 8 . The key point here is that the common-collector configuration is not unilateral. As a result, the input resistance depends on the load resistor $R_{L}$ and the output resistance depends on the source resistance $R_{S}$. Therefore, the characterization of the emitter follower by the corresponding equivalent two-port network is not particularly useful for intuitive understanding. Instead, we will analyze the entire emitterfollower circuit of Fig. 3.23 b , including both the source resistance $R_{S}$ and the load resistor $R_{L}$. From KCL at the output node, we find

$$
\begin{equation*}
\frac{v_{s}-v_{o}}{R_{S}+r_{\pi}}+\beta_{0}\left(\frac{v_{s}-v_{o}}{R_{S}+r_{\pi}}\right)-\frac{v_{o}}{R_{L}}-\frac{v_{o}}{r_{o}}=0 \tag{3.68}
\end{equation*}
$$

from which we find

$$
\begin{equation*}
\frac{v_{o}}{v_{s}}=\frac{1}{1+\frac{R_{S}+r_{\pi}}{\left(\beta_{0}+1\right)\left(R_{L} \| r_{o}\right)}} \tag{3.69}
\end{equation*}
$$

If the base resistance $r_{b}$ is significant, it can simply be added to $R_{S}$ in these expressions. The voltage gain is always less than unity and will be close to unity if $\beta_{0}\left(R_{L} \| r_{o}\right) \gg\left(R_{S}+r_{\pi}\right)$. In most practical circuits, this condition holds. Note that because we have included the source resistance in this calculation, the value of $v_{o} / v_{s}$ is not analogous to $a_{v}$ calculated for the CE and CB stages. When $r_{\pi} \gg R_{S}, \beta_{0} \gg 1$, and $r_{o} \gg R_{L}$, (3.69) can be approximated as

$$
\begin{equation*}
\frac{v_{o}}{v_{s}} \simeq \frac{g_{m} R_{L}}{1+g_{m} R_{L}} \tag{3.70}
\end{equation*}
$$

We calculate the input resistance $R_{i}$ by removing the input source, driving the input with a test current source $i_{t}$, and calculating the resulting voltage $v_{t}$ across the input terminals. The circuit used to do this calculation is shown in Fig. 3.24a. From KCL at the output node,

$$
\begin{equation*}
\frac{v_{o}}{R_{L}}+\frac{v_{o}}{r_{o}}=i_{t}+\beta_{0} i_{t} \tag{3.71}
\end{equation*}
$$

Then the voltage $v_{t}$ is

$$
\begin{equation*}
v_{t}=i_{t} r_{\pi}+v_{o}=i_{t} r_{\pi}+\frac{i_{t}+\beta_{0} i_{t}}{\frac{1}{R_{L}}+\frac{1}{r_{o}}} \tag{3.72}
\end{equation*}
$$

and thus

$$
\begin{equation*}
R_{i}=\frac{v_{t}}{i_{t}}=r_{\pi}+\left(\beta_{0}+1\right)\left(R_{L} \| r_{o}\right) \tag{3.73}
\end{equation*}
$$

A general property of emitter followers is that the resistance looking into the base is equal to $r_{\pi}$ plus $\left(\beta_{0}+1\right)$ times the incremental resistance connected from the emitter to small-signal ground. The factor of $\beta_{0}+1$ in (3.73) stems from the current gain of the common-collector configuration from the base to the emitter, which increases the voltage drop on the resistance connected from the emitter to small-signal ground and its contribution to the test voltage $v_{t}$ in (3.72).

We now calculate the output resistance $R_{o}$ by removing the load resistance $R_{L}$ and finding the Thevenin-equivalent resistance looking into the output terminals. We can do this by either inserting a test current and calculating the resulting voltage or applying a test voltage and
image_name:(a)
description:
[
name: it, type: CurrentSource, value: it, ports: {Np: Ut, Nn: GND}
name: vt, type: VoltageSource, value: vt, ports: {Np: Ut, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vo, N2: Ut}
name: βib, type: CurrentControlCurrentSource, value: βib, ports: {Np: GND, Nn: Vo}
name: ro, type: Resistor, value: ro, ports: {N1: v0, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:This is a circuit for calculating the input resistance of an emitter follower. It includes a voltage source Ut, a current source it, and a test voltage vt. The resistors rπ and ro are connected to node Ut, with rπ also connected to Vo. The current source βib is connected between Ut and Vo. The load resistor RL is connected between Vo and GND.
image_name:(b)
description:
[
name: it, type: CurrentSource, value: it, ports: {Np: GND, Nn: Vt}
name: vt, type: VoltageSource, value: vt, ports: {Np: Vt, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vt, N2: Ut}
name: gmV1, type: CurrentControlCurrentSource, value: gmV1, ports: {Np: Vt, Nn: GND}
name: ro, type: Resistor, value: ro, ports: {N1: Ut, N2: GND}
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: X}
]
extrainfo:The circuit is used to calculate the output resistance of an emitter follower by applying a test voltage vt.

image_name:(c)
description:
[
name: RS, type: Resistor, value: 1 kΩ, ports: {N1: Vs, N2: b1}
name: Q1, type: NPN, ports: {C: VCC, B: b1, E: Vo}
name: RL, type: Resistor, value: 1 kΩ, ports: {N1: Vo, N2: VEE}
name: Vs, type: VoltageSource, ports: {Np: Vs, Nn: GND}
]
extrainfo:This circuit is an emitter follower configuration used to calculate the input resistance. It includes a voltage source, a resistor RS, an NPN transistor Q1, and a load resistor RL. The emitter voltage Vo is the output voltage.

Figure 3.24 (a) Circuit for calculation of the input resistance of the emitter follower. (b) Circuit for calculation of the output resistance of the emitter follower. (c) Example emitter follower.
calculating the current. In this case, the calculation is simpler if a test voltage $v_{t}$ is applied as shown in Fig. 3.24b. The voltage $v_{1}$ is given by

$$
\begin{equation*}
v_{1}=-v_{t}\left(\frac{r_{\pi}}{r_{\pi}+R_{S}}\right) \tag{3.74}
\end{equation*}
$$

The total output current $i_{t}$ is thus

$$
\begin{equation*}
i_{t}=\frac{v_{t}}{r_{\pi}+R_{S}}+\frac{v_{t}}{r_{o}}+g_{m} v_{t}\left(\frac{r_{\pi}}{r_{\pi}+R_{S}}\right) \tag{3.75}
\end{equation*}
$$

Therefore,

$$
\begin{equation*}
R_{o}=\frac{v_{t}}{i_{t}}=\left(\frac{r_{\pi}+R_{S}}{\beta_{0}+1}\right) \| r_{o} \tag{3.76}
\end{equation*}
$$

If $\beta_{0} \gg 1$ and $r_{o} \gg\left(1 / g_{m}\right)+R_{S} /\left(\beta_{0}+1\right)$,

$$
\begin{equation*}
R_{o} \simeq \frac{1}{g_{m}}+\frac{R_{S}}{\beta_{0}+1} \tag{3.77}
\end{equation*}
$$

Equation 3.77 shows that the resistance at the output is about equal to the resistance in the base lead, divided by $\left(\beta_{0}+1\right)$, plus $1 / g_{m}$. In ( 3.77$), R_{S}$ is divided by $\beta_{0}+1$ because the base current flows in $R_{S}$, and the base current is $\beta_{0}+1$ times smaller than the emitter current.

Therefore, the emitter follower has high input resistance, low output resistance, and nearunity voltage gain. It is most widely used as an impedance transformer to reduce loading of a preceding signal source by the input impedance of a following stage. It also finds application as a unity-voltage-gain level shift because the dc output voltage is shifted from the dc input voltage by $V_{B E(\mathrm{on})}$.

#### EXAMPLE

Calculate the input resistance, output resistance, and voltage gain of the emitter follower of Fig. 3.24c. Assume that $\beta_{0}=100, r_{b}=0, r_{o} \rightarrow \infty$, and $I_{C}=100 \mu \mathrm{~A}$.

$$
\begin{aligned}
& R_{i}=r_{\pi}+R_{L}\left(1+\beta_{0}\right)=26 \mathrm{k} \Omega+(1 \mathrm{k} \Omega)(101)=127 \mathrm{k} \Omega \\
& \frac{v_{o}}{v_{s}}=\frac{1}{1+\frac{r_{\pi}+R_{S}}{\left(\beta_{0}+1\right) R_{L}}}=\frac{1}{1+\frac{26 \mathrm{k} \Omega+1 \mathrm{k} \Omega}{(101)(1 \mathrm{k} \Omega)}} \simeq 0.79 \\
& R_{o}=\frac{R_{S}+r_{\pi}}{1+\beta_{0}}=\frac{1 \mathrm{k} \Omega+26 \mathrm{k} \Omega}{101} \simeq 270 \Omega
\end{aligned}
$$

### 3.3.7 Common-Drain Configuration (Source Follower)

The common-drain configuration is shown in Fig. 3.25a. The input signal is applied to the gate and the output is taken from the source. From a large-signal standpoint, the output voltage is equal to the input voltage minus the gate-source voltage. The gate-source voltage consists of two parts: the threshold and the overdrive. If both parts are constant, the resulting output
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: Vo, D: VDD, G: Vi}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a common-drain configuration, also known as a source follower. The input is applied to the gate of the NMOS (M1), and the output is taken from the source. The output voltage follows the input voltage with a slight offset.

Figure 3.25 (a) Common-drain configuration. (b) Small-signal equivalent circuit of the common-drain configuration.
image_name:(a)
description:
[
name: g_m v_gs, type: CurrentSource, value: g_m v_gs, ports: {Np: vo(vs), Nn: GND}
name: g_mb v_bs, type: CurrentSource, value: g_mb v_bs, ports: {Np: vo(vs), Nn: GND}
name: R_L, type: Resistor, value: R_L, ports: {N1: vi, N2: vo(vs)}
name: r_o, type: Resistor, value: r_o, ports: {N1: vo(vs), N2: vo(vs)}
]
extrainfo:The circuit is a small-signal equivalent of a common-drain configuration (source follower). The input is applied at vi, and the output is taken from vo(vs). The small-signal gain is unity, and the output voltage follows the input voltage with a slight offset. The body effect influences the threshold voltage.
image_name:(b)
description:
[
name: g_m v_gs, type: VoltageControlledCurrentSource, value: g_m v_gs, ports: {Np: vo, Nn: GND}
name: g_mb V_bs, type: VoltageControlledCurrentSource, value: g_mb V_bs, ports: {Np: vo, Nn: GND}
name: R_L, type: Resistor, value: R_L, ports: {N1: vo, N2: GND}
name: r_o, type: Resistor, value: r_o, ports: {N1: vo, N2: vout}
name: Vi, type: VoltageSource, value: Vi, ports: {Np: vi, Nn: GND}
]
extrainfo:The circuit is a small-signal equivalent of a common-drain configuration (source follower). The input voltage is applied at the gate, and the output is taken from the source, following the input voltage with a slight offset. The small-signal gain is approximately unity.

voltage is simply offset from the input, and the small-signal gain would be unity. Therefore, the source follows the gate, and the circuit is also known as a source follower. In practice, the body effect changes the threshold voltage, and the overdrive depends on the drain current, which changes as the output voltage changes unless $R_{L} \rightarrow \infty$. Furthermore, even if the current were exactly constant, the overdrive depends to some extent on the drain-source voltage unless the Early voltage is infinite. We will use small-signal analysis to study these effects.

The small-signal equivalent circuit is shown in Fig. 3.25b. Since the body terminal is not shown in Fig. 3.25a, we assume that the body is connected to the lowest supply voltage (ground here) to keep the source-body $p n$ junction reverse biased. As a result, $v_{b s}$ changes when the output changes because the source is connected to the output, and the $g_{m b}$ generator is active in general.

From KVL around the input loop,

$$
\begin{equation*}
v_{i}=v_{g s}+v_{o} \tag{3.78}
\end{equation*}
$$

With the output open circuited, $i_{o}=0$, and KCL at the output node gives

$$
\begin{equation*}
g_{m} v_{g s}-g_{m b} v_{o}-\frac{v_{o}}{R_{L}}-\frac{v_{o}}{r_{o}}=0 \tag{3.79}
\end{equation*}
$$

Solving (3.78) for $v_{g s}$, substituting into (3.79), and rearranging gives

$$
\begin{equation*}
\left.\frac{v_{o}}{v_{i}}\right|_{i_{o}=0}=\frac{g_{m}}{g_{m}+g_{m b}+\frac{1}{R_{L}}+\frac{1}{r_{o}}}=\frac{g_{m} r_{o}}{1+\left(g_{m}+g_{m b}\right) r_{o}+\frac{r_{o}}{R_{L}}} \tag{3.80}
\end{equation*}
$$

If $R_{L} \rightarrow \infty$, (3.80) simplifies to

$$
\begin{equation*}
\left.\lim _{R_{L} \rightarrow \infty} \frac{v_{o}}{v_{i}}\right|_{i_{o}=0}=\frac{g_{m} r_{o}}{1+\left(g_{m}+g_{m b}\right) r_{o}} \tag{3.81}
\end{equation*}
$$

Equation 3.81 gives the open-circuit voltage gain of the source follower with the load resistor replaced by an ideal current source. If $r_{o}$ is finite, this gain is less than unity even if the body effect is eliminated by connecting the source to the body to deactivate the $g_{m b}$ generator. In this case, variation in the output voltage changes the drain-source voltage and the current through $r_{o}$. From a large-signal standpoint, solving (1.165) for $V_{G S}-V_{t}$ shows that the overdrive also depends on the drain-source voltage unless the channel-length modulation parameter $\lambda$ is zero. This dependence causes the small-signal gain to be less than unity.

A significant difference between bipolar and MOS followers is apparent from (3.80). If $R_{L} \rightarrow \infty$ and $r_{o} \rightarrow \infty$,

$$
\begin{equation*}
\lim _{\substack{R_{L} \rightarrow \infty \\ r_{o} \rightarrow \infty}} \frac{v_{o}}{v_{i}}=\frac{g_{m}}{g_{m}+g_{m b}}=\frac{1}{1+\chi} \tag{3.82}
\end{equation*}
$$

Equation 3.82 shows that the source-follower gain is less than unity under these conditions and that the gain depends on $\chi=g_{m b} / g_{m}$, which is typically in the range of 0.1 to 0.3 . In contrast, the gain of an emitter follower would be unity under these conditions. As a result, the sourcefollower gain is not as well specified as that of an emitter follower when body effect is a factor. Furthermore, (1.200) shows that $\chi$ depends on the source-body voltage which is equal to $V_{o}$ when the body is connected to ground. Therefore, the gain calculated in (3.82) depends on the output voltage, causing distortion to arise for large-signal changes in the output as shown in Section 5.3.2. To overcome these limitations in practice, the type of source follower ( $n$-channel or $p$-channel) can be chosen so that it can be fabricated in an isolated well. Then the well can be connected to the source of the transistor, setting $V_{S B}=0$ and $v_{s b}=0$. Unfortunately, the parasitic capacitance from the well to the substrate increases the capacitance attached to the
source with this connection, reducing the bandwidth of the source follower. The frequency response of source followers is covered in Chapter 7.

The output resistance of the source follower can be calculated from Fig. $3.25 b$ by setting $v_{i}=0$ and driving the output with a voltage source $v_{o}$. Then $v_{g s}=-v_{o}$ and $i_{o}$ is

$$
\begin{equation*}
i_{o}=\frac{v_{o}}{r_{o}}+\frac{v_{o}}{R_{L}}+g_{m} v_{o}+g_{m b} v_{o} \tag{3.83}
\end{equation*}
$$

Rearranging (3.83) gives

$$
\begin{equation*}
R_{o}=\frac{v_{o}}{i_{o}}=\frac{1}{g_{m}+g_{m b}+\frac{1}{r_{o}}+\frac{1}{R_{L}}} \tag{3.84}
\end{equation*}
$$

Equation 3.84 shows that the body effect reduces the output resistance, which is desirable because the source follower produces a voltage output. This beneficial effect stems from the nonzero small-signal current conducted by the $g_{m b}$ generator in Fig. 3.25b, which increases the output current for a given change in the output voltage. As $r_{o} \rightarrow \infty$ and $R_{L} \rightarrow \infty$, this output resistance approaches $1 /\left(g_{m}+g_{m b}\right)$. The common-gate input resistance given in (3.54) approaches the same limiting value.

As with emitter followers, source followers are used as voltage buffers and level shifters. When used as a level shifter, they are more flexible than emitter followers because the dc value of $V_{G S}$ can be altered by changing the $W / L$ ratio.

### 3.3.8 Common-Emitter Amplifier with Emitter Degeneration

In the common-emitter amplifier considered earlier, the signal is applied to the base, the output is taken from the collector, and the emitter is attached to ac ground. In practice, however, the common-emitter circuit is often used with a nonzero resistance in series with the emitter as shown in Fig. 3.26a. The resistance has several effects, including reducing the transconductance, increasing the output resistance, and increasing the input resistance. These changes stem from negative feedback introduced by the emitter resistor $R_{E}$. When $V_{i}$ increases, the base-emitter voltage increases, which increases the collector current. As a result, the voltage dropped across the emitter resistor increases, reducing the base-emitter voltage compared to the case where $R_{E}=0$. Therefore, the presence of nonzero $R_{E}$ reduces the base-emitter voltage through a negative-feedback process termed emitter degeneration. This circuit is examined from a feedback standpoint in Chapter 8.

In this section, we calculate the input resistance, output resistance, and transconductance of the emitter-degenerated, common-emitter amplifier. To find the input resistance and transconductance, consider the small-signal equivalent circuit shown in Fig. 3.26b, and focus on $v_{i}, i_{b}$, and $i_{o}$. From KCL at the emitter,

$$
\begin{equation*}
\frac{v_{e}}{R_{E}}+\frac{v_{e}+i_{o} R_{C}}{r_{o}}=\left(\beta_{0}+1\right) i_{b} \tag{3.85}
\end{equation*}
$$

From KCL at the collector,

$$
\begin{equation*}
i_{o}+\frac{v_{e}+i_{o} R_{C}}{r_{o}}=\beta_{0} i_{b} \tag{3.86}
\end{equation*}
$$

From KVL around the input loop,

$$
\begin{equation*}
i_{b}=\frac{v_{i}-v_{e}}{r_{\pi}} \tag{3.87}
\end{equation*}
$$

image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: Vo, B: Vi, E: e1}
name: RC, type: Resistor, value: RC, ports: {N1: Vo, N2: VCC}
name: RE, type: Resistor, value: RE, ports: {N1: e1, N2: GND}
]
extrainfo:The circuit is a common-emitter amplifier with emitter degeneration. The transistor Q1 is configured with a resistor at the emitter (RE) and a load resistor at the collector (RC). The input is applied at Vi and the output is taken from Vo. The circuit uses a VCC supply voltage.
image_name:(b)
description:
[
name: RC, type: Resistor, value: RC, ports: {N1: Vo, N2: GND}
name: RE, type: Resistor, value: RE, ports: {N1: X, N2: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vi, N2: X}
name: ro, type: Resistor, value: ro, ports: {N1: Vo, N2: Vt}
name: Gm, type: CurrentControlledCurrentSource, value: Gmv1, ports: {Np: X, Nn: Vo}
]
extrainfo:The circuit diagram (b) represents a small-signal model for calculating output resistance in an emitter-degenerated common-emitter amplifier. It includes an NPN transistor, resistors for emitter and collector, and current-controlled current sources to model transistor behavior.
image_name:(c)
description:Circuit for calculation of output resistance.
image_name:(d)
description:The circuit is a small-signal, two-port equivalent of an emitter-degenerated common-emitter amplifier. It includes resistors representing input and output resistances and a current source representing the transconductance.

Figure 3.26 (a) Common-emitter amplifier with emitter degeneration. (b) Small-signal equivalent circuit for emitter-degenerated, common-emitter amplifier. (c) Circuit for calculation of output resistance. (d) Small-signal, two-port equivalent of emitter-degenerated CE amplifier.

Solving (3.85) for $i_{o}$, substituting into (3.86) and rearranging gives

$$
\begin{equation*}
v_{e}=i_{b}\left(\frac{1+\left(\beta_{0}+1\right) \frac{r_{o}}{R_{C}}}{\frac{1}{R_{C}}+\frac{1}{R_{E}}+\frac{r_{o}}{R_{C} R_{E}}}\right) \tag{3.88}
\end{equation*}
$$

Substituting (3.88) into (3.87) and rearranging gives

$$
\begin{equation*}
R_{i}=\frac{v_{i}}{i_{b}}=r_{\pi}+\left(\beta_{0}+1\right) R_{E}\left(\frac{r_{o}+\frac{R_{C}}{\beta_{0}+1}}{r_{o}+R_{C}+R_{E}}\right) \tag{3.89}
\end{equation*}
$$

If $r_{o} \gg R_{C}$ and $r_{o} \gg R_{E}$, the last term in parentheses in (3.89) is approximately equal to unity and

$$
\begin{equation*}
R_{i} \simeq r_{\pi}+\left(\beta_{0}+1\right) R_{E} \tag{3.90}
\end{equation*}
$$

Because the last term in parentheses in (3.89) is less than one, comparing (3.89) and (3.90) shows that finite $r_{o}$ reduces the input resistance of the common-emitter amplifier with emitter degeneration. This reduction stems from nonzero current that flows in $r_{o}$ when $r_{o}$ is finite. If $v_{i}$ increases, $v_{e}$ follows $v_{i}$ because the base-emitter voltage is approximately constant, but the collector voltage ( $-i_{o} R_{C}$ ) decreases by an amount determined by the small-signal gain from the base to the collector. Therefore, the current that flows in $r_{o}$ from the emitter to the collector increases, increasing the base current and reducing the input resistance. In practice, (3.90) is usually used to calculate the input resistance. The error in the approximation is usually small unless the resistances represented by $R_{C}$ or $R_{E}$ are large, such as when implemented with transistors in active-load configurations. Active loads are considered in Chapter 4.

Now we will calculate the transconductance of the stage. First, set $R_{C}=0$ in Fig. 3.26b because $G_{m}=i_{o} / v_{i}$ with the output shorted. Substituting (3.87) into (3.85) with $R_{C}=0$ and rearranging gives

$$
\begin{equation*}
v_{e}=v_{i}\left(\frac{\frac{\left(\beta_{0}+1\right)}{r_{\pi}}}{\frac{1}{R_{E}}+\frac{1}{r_{o}}+\frac{\beta_{0}+1}{r_{\pi}}}\right) \tag{3.91}
\end{equation*}
$$

Substituting (3.87) and (3.91) into (3.86) with $R_{C}=0$ and rearranging gives

$$
\begin{equation*}
G_{m}=\frac{i_{o}}{v_{i}}=g_{m}\left[\frac{1-\frac{R_{E}}{\beta_{0} r_{o}}}{1+g_{m} R_{E}\left(1+\frac{1}{\beta_{0}}+\frac{1}{g_{m} r_{o}}\right)}\right] \tag{3.92}
\end{equation*}
$$

In most practical cases, $\beta_{0} \gg 1, r_{o} \gg R_{E}$, and $g_{m} r_{o} \gg 1$. Then

$$
\begin{equation*}
G_{m} \simeq \frac{g_{m}}{1+g_{m} R_{E}} \tag{3.93}
\end{equation*}
$$

Equation 3.93 is usually used to calculate the transconductance of a common-emitter amplifier with emitter degeneration.

The output resistance is calculated using the equivalent circuit of Fig. 3.26c. For the time being, assume that $R_{C}$ is very large and can be neglected. The test current $i_{t}$ flows in the parallel combination of $r_{\pi}$ and $R_{E}$, so that

$$
\begin{equation*}
v_{1}=-i_{t}\left(r_{\pi} \| R_{E}\right) \tag{3.94}
\end{equation*}
$$

The current through $r_{o}$ is

$$
\begin{equation*}
i_{1}=i_{t}-g_{m} v_{1}=i_{t}+i_{t} g_{m}\left(r_{\pi} \| R_{E}\right) \tag{3.95}
\end{equation*}
$$

As a result, the voltage $v_{t}$ is

$$
\begin{equation*}
v_{t}=-v_{1}+i_{1} r_{o}=i_{t}\left(r_{\pi} \| R_{E}\right)+i_{t} r_{o}\left[1+g_{m}\left(r_{\pi} \| R_{E}\right)\right] \tag{3.96}
\end{equation*}
$$

Thus

$$
\begin{equation*}
R_{o}=\frac{v_{t}}{i_{t}}=\left(r_{\pi} \| R_{E}\right)+r_{o}\left[1+g_{m}\left(r_{\pi} \| R_{E}\right)\right] \tag{3.97}
\end{equation*}
$$

In this equation, the first term is much smaller than the second. If the first term is neglected, we obtain,

$$
\begin{equation*}
R_{o} \simeq r_{o}\left(1+g_{m} \frac{r_{\pi} R_{E}}{r_{\pi}+R_{E}}\right)=r_{o}\left(1+\frac{g_{m} R_{E}}{1+\frac{R_{E}}{r_{\pi}}}\right)=r_{o}\left(1+\frac{g_{m} R_{E}}{1+\frac{g_{m} R_{E}}{\beta_{0}}}\right) \tag{3.98}
\end{equation*}
$$

If $g_{m} R_{E} \ll \beta_{0}$, then

$$
\begin{equation*}
R_{o} \simeq r_{o}\left(1+g_{m} R_{E}\right) \tag{3.99}
\end{equation*}
$$

Thus the output resistance is increased by a factor $\left(1+g_{m} R_{E}\right)$. This fact makes the use of emitter degeneration desirable in transistor current sources. If the collector load resistor $R_{C}$ is not large enough to neglect, it must be included in parallel with the expressions in (3.97)(3.99). A small-signal equivalent circuit, neglecting $R_{C}$, is shown in Fig. 3.26d. On the other hand, if $g_{m} R_{E} \gg \beta_{0}$, (3.98) shows that

$$
\begin{equation*}
R_{o} \simeq r_{o}\left(1+\beta_{0}\right) \tag{3.100}
\end{equation*}
$$

The output resistance is finite even when $R_{E} \rightarrow \infty$ because nonzero test current flows in $r_{\pi}$ when $\beta_{0}$ is finite.

### 3.3.9 Common-Source Amplifier with Source Degeneration

Source degeneration in MOS transistor amplifiers is not as widely used as emitter degeneration in bipolar circuits for at least two reasons. First, the transconductance of MOS transistors is normally much lower than that of bipolar transistors so that further reduction in transconductance is usually undesirable. Second, although degeneration increases the input resistance in the bipolar case, $R_{i} \rightarrow \infty$ even without degeneration in the MOS case. However, examining the effects of source degeneration is important in part because it is widely used to increase the output resistance of MOS current sources. Also, because small-geometry MOS transistors can be modeled as ideal square-law devices with added source resistors as shown in Section 1.7.1, we will consider the effects of source degeneration below.

A common-source amplifier with source degeneration is shown in Fig. 3.27. Its smallsignal equivalent circuit is shown in Fig. 3.28. Because the input is connected to the gate of the MOS transistor, $R_{i} \rightarrow \infty$. To calculate the transconductance, set $R_{D}=0$ because $G_{m}=i_{o} / v_{i}$ with the output shorted. Also, since a connection to the body is not shown in Fig. 3.27, we assume that the body is connected to the lowest power-supply voltage, which is ground. Therefore, the dc body voltage is constant and $v_{b}=0$. From KCL at the source with $R_{D}=0$,

$$
\begin{equation*}
\frac{v_{s}}{R_{S}}+\frac{v_{s}}{r_{o}}=g_{m}\left(v_{i}-v_{s}\right)+g_{m b}\left(0-v_{s}\right) \tag{3.101}
\end{equation*}
$$

image_name:Figure 3.27
description:
[
name: M1, type: NMOS, ports: {S: s1, D: vo, G: vi}
name: RD, type: Resistor, value: RD, ports: {N1: vo, N2: VDD}
name: RS, type: Resistor, value: RS, ports: {N1: s1, N2: GND}
]
extrainfo:The circuit is a common-source amplifier with source degeneration using an NMOS transistor M1. The source is connected to ground through a resistor RS, and the drain is connected to VDD through a resistor RD. The input voltage is applied at the gate of M1.
image_name:Figure 3.28
description:
[
name: RD, type: Resistor, value: RD, ports: {N1: Vo, N2: GND}
name: RS, type: Resistor, value: RS, ports: {N1: S, N2: GND}
name: gmvgs, type: VoltageControlledCurrentSource, ports: {Np: Vo, Nn: S}
name: gmbvbs, type: VoltageControlledCurrentSource, ports: {Np: Vo, Nn: S}
name: ro, type: Resistor, value: ro, ports: {N1: Vo, N2: GND}
]
extrainfo:This is a small-signal equivalent circuit of a source-degenerated, common-source amplifier. The NMOS transistor M1 is degenerated by a source resistor RS, and the drain is connected to a load resistor RD. The circuit includes two voltage-controlled current sources representing the transconductance gm and the body effect gmb. The output voltage Vo is taken across RD.

Figure 3.28 Small-signal equivalent of the sourcedegenerated, commonsource amplifier.

From KCL at the drain with $R_{D}=0$,

$$
\begin{equation*}
i_{o}+\frac{v_{s}}{r_{o}}=g_{m}\left(v_{i}-v_{s}\right)+g_{m b}\left(0-v_{s}\right) \tag{3.102}
\end{equation*}
$$

Solving (3.101) for $v_{s}$, substituting into (3.102), and rearranging gives

$$
\begin{equation*}
G_{m}=\frac{i_{o}}{v_{i}}=\frac{g_{m}}{1+\left(g_{m}+g_{m b}\right) R_{S}+\frac{R_{S}}{r_{o}}} \tag{3.103}
\end{equation*}
$$

If $r_{o} \gg R_{S}$,

$$
\begin{equation*}
G_{m} \simeq \frac{g_{m}}{1+\left(g_{m}+g_{m b}\right) R_{S}} \tag{3.104}
\end{equation*}
$$

For large $R_{S},(3.104)$ shows that the value of $G_{m}$ approaches $1 /\left[(1+\chi) R_{S}\right]$. Even in this limiting case, the transconductance of the common-source amplifier with degeneration is dependent on an active-device parameter $\chi$. Since $\chi$ is typically in the range of 0.1 to 0.3 , the body effect causes the transconductance in this case to deviate from $1 / R_{S}$ by about 10 to 20 percent. In contrast, (3.92) indicates that the value of $G_{m}$ for a common-emitter amplifier with degeneration approaches $\beta_{0} /\left[\left(\beta_{0}+1\right) R_{E}\right]$ for large $R_{E}$, assuming that $r_{o} \gg R_{E}$ and $g_{m} r_{o} \gg 1$. If $\beta_{0}>100$, the transconductance of this bipolar amplifier is within 1 percent of $1 / R_{E}$. Therefore, the transconductance of a common-source amplifier with degeneration is usually much more dependent on active-device parameters than in its bipolar counterpart.

The output resistance of the circuit can be calculated from the equivalent circuit of Fig. 3.29, where $R_{D}$ is neglected. Since the entire test current flows in $R_{S}$,

$$
\begin{equation*}
v_{s}=i_{t} R_{S} \tag{3.105}
\end{equation*}
$$

Then

$$
\begin{equation*}
v_{t}=v_{s}+i_{1} r_{o}=v_{s}+r_{o}\left[i_{t}-g_{m}\left(0-v_{s}\right)-g_{m b}\left(0-v_{s}\right)\right] \tag{3.106}
\end{equation*}
$$

image_name:Figure 3.29 Circuit for calculation of output resistance
description:
[
name: Vgs, type: VoltageSource, value: Vgs, ports: {Np: GND, Nn: Vs}
name: Rs, type: Resistor, value: Rs, ports: {N1: Vs, N2: GND}
name: gmVgs, type: CurrentSource, value: gmVgs, ports: {Np: Vc, Nn: Vs}
name: gmbVbs, type: CurrentSource, value: gmbVbs, ports: {Np: Vc, Nn: Vs}
name: ro, type: Resistor, value: ro, ports: {N1: Vc, N2: Vt}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: Vt, Nn: GND}
]
extrainfo:The circuit is designed to calculate the output resistance and includes a voltage source Vgs, a resistor Rs, two current sources gmVgs and gmbVbs, a resistor ro, and a voltage source Vt. The configuration shows how the test current it flows through the circuit to determine the output voltage vt.

Figure 3.29 Circuit for calculation of output resistance.

Substituting (3.105) into (3.106) and rearranging gives

$$
\begin{equation*}
R_{o}=\frac{v_{t}}{i_{t}}=R_{S}+r_{o}\left[1+\left(g_{m}+g_{m b}\right) R_{S}\right] \tag{3.107}
\end{equation*}
$$

This equation shows that as $R_{S}$ is made arbitrarily large, the value of $R_{o}$ continues to increase. In contrast, (3.100) shows that $R_{O}$ in the common-emitter amplifier with degeneration approaches a maximum value of about $\left(\beta_{0}+1\right) r_{o}$ as $R_{E} \rightarrow \infty$.

## 3.4 Multiple-Transistor Amplifier Stages

Most integrated-circuit amplifiers consist of a number of stages, each of which provides voltage gain, current gain, and/or impedance-level transformation from input to output. Such circuits can be analyzed by considering each transistor to be a stage and analyzing the circuit as a collection of individual transistors. However, certain combinations of transistors occur so frequently that these combinations are usually characterized as subcircuits and regarded as a single stage. The usefulness of these topologies varies considerably with the technology being used. For example, the Darlington two-transistor connection is widely used in bipolar integrated circuits to improve the effective current gain and input resistance of a single bipolar transistor. Since the current gain and input resistance are infinite with MOS transistors however, this connection finds little use in pure MOS integrated circuits. On the other hand, the cascode connection achieves a very high output resistance and is useful in both bipolar and MOS technologies.

### 3.4.1 The CC-CE, CC-CC and Darlington Configurations

The common-collector-common-emitter (CC-CE), common-collector-common-collector (CC-CC), and Darlington ${ }^{5}$ configurations are all closely related. They incorporate an additional transistor to boost the current gain and input resistance of the basic bipolar transistor. The common-collector-common-emitter configuration is shown in Fig. 3.30a. The biasing current source $I_{\text {BIAS }}$ is present to establish the quiescent dc operating current in the emitterfollower transistor $Q_{1}$; this current source may be absent in some cases or may be replaced by a resistor. The common-collector-common-collector configuration is illustrated in Fig. 3.30b. In both of these configurations, the effect of transistor $Q_{1}$ is to increase the current gain through the stage and to increase the input resistance. For the purpose of the low-frequency, small-signal analysis of circuits, the two transistors $Q_{1}$ and $Q_{2}$ can be thought of as a single composite transistor, as illustrated in Fig. 3.31. The small-signal equivalent circuit for this composite device is shown in Fig. 3.32, assuming that the effects of the $r_{o}$ of $Q_{1}$ are negligible. We will now calculate effective values for the $r_{\pi}, g_{m}, \beta_{0}$, and $r_{o}$ of the composite device, and we will designate these composite parameters with a superscript $c$. We will also denote the
image_name:Figure 3.31
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: In, E: e1b2}
name: Q2, type: NPN, ports: {C: Out, B: e1b2, E: GND}
name: IBIAS, type: CurrentSource, value: IBIAS, ports: {Np: e1b2, Nn: GND}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
]
extrainfo:The circuit represents a composite transistor configuration using two NPN transistors (Q1 and Q2) with a current source IBIAS providing biasing. The input is at the base of Q1, and the output is at the collector of Q2. VCC is the supply voltage, and both transistors are connected to the ground.

(a)
image_name:Figure 3.30 (a)
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: In, E: e1b2}
name: Q2, type: NPN, ports: {C: VCL, B: e1b2, E: Out}
name: IBIAS, type: CurrentSource, value: IBIAS, ports: {Np: e1b2, Nn: GND}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
]
extrainfo:The circuit is a common-collector-common-emitter cascade configuration with two NPN transistors. The input is at the base of Q1 and the output is at the collector of Q2. A current source IBIAS provides biasing, and VCC is the supply voltage.

(b)

Figure 3.30 (a) Common-collector-common-emitter cascade. (b) Common-collector- commoncollector cascade.
image_name:Figure 3.31
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: Bc, E: e1b2}
name: Q2, type: NPN, ports: {C: Cc, B: e1b2, E: Ec}
name: IBIAS, type: CurrentSource, ports: {Np: e1b2, Nn: GND}
]
extrainfo:The circuit is a common-collector-common-emitter cascade configuration with two NPN transistors. The input is at the base of Q1 and the output is at the collector of Q2. A current source IBIAS provides biasing, and VCC is the supply voltage.

Figure 3.31 The composite transistor representation of the CC-CE and CC-CC connections.
image_name:Figure 3.32
description:
[
name: r_π1, type: Resistor, value: r_π1, ports: {N1: BC, N2: e1b2}
name: g_m1V_1, type: CurrentControlledCurrentSource, ports: {Np: GND, Nn: e1b2}
name: r_π2, type: Resistor, value: r_π2, ports: {N1: e1b2, N2: EC}
name: g_m2V_2, type: CurrentControlledCurrentSource, ports: {Np: CC, Nn: EC}
name: r_o2, type: Resistor, value: r_o2, ports: {N1: CC, N2: EC}
]
extrainfo:The circuit is a small-signal equivalent of a common-collector-common-emitter cascade configuration with two NPN transistors. The input is at the base of Q1 and the output is at the collector of Q2. A current source IBIAS provides biasing, and VCC is the supply voltage.

Figure 3.32 Small-signal equivalent circuit for the CC-CE and CC-CC connected transistors.
terminal voltages and currents of the composite device with a superscript $c$. We assume that $\beta_{0}$ is constant.

The effective value of $r_{\pi}, r_{\pi}^{c}$, is the resistance seen looking into the composite base $B^{c}$ with the composite emitter $E^{c}$ grounded. Referring to Fig. 3.32, we see that the resistance looking into the base of $Q_{2}$ with $E^{c}$ grounded is simply $r_{\pi 2}$. Thus (3.73) for the input resistance of the emitter follower can be used. Substituting $r_{\pi 2}$ for $R_{L}$ and allowing $r_{o} \rightarrow \infty$ gives

$$
\begin{equation*}
r_{\pi}^{c}=r_{\pi 1}+\left(\beta_{0}+1\right) r_{\pi 2} \tag{3.108}
\end{equation*}
$$

The effective transconductance of the configuration $g_{m}^{c}$ is the change in the collector current of $Q_{2}, i_{c}^{c}$, for a unit change in $v_{b e}^{c}$ with $C^{c}$ and $E^{c}$ grounded. To calculate this transconductance, we first find the change in $v_{2}$ that occurs for a unit change in $v_{b e}^{c}$. Equation 3.69 can be used
directly, giving

$$
\begin{equation*}
\frac{v_{2}}{v_{b e}^{c}}=\frac{1}{1+\left(\frac{r_{\pi 1}}{\left(\beta_{0}+1\right) r_{\pi 2}}\right)} \tag{3.109}
\end{equation*}
$$

Also

$$
\begin{equation*}
i_{c}^{c}=g_{m}^{c} v_{b e}^{c}=g_{m 2} v_{2}=\frac{g_{m 2} v_{b e}^{c}}{1+\left(\frac{r_{\pi 1}}{\left(\beta_{0}+1\right) r_{\pi 2}}\right)} \tag{3.110}
\end{equation*}
$$

Thus

$$
\begin{equation*}
g_{m}^{c}=\frac{i_{c}^{c}}{v_{b e}^{c}}=\frac{g_{m 2}}{1+\left(\frac{r_{\pi 1}}{\left(\beta_{0}+1\right) r_{\pi 2}}\right)} \tag{3.111}
\end{equation*}
$$

For the special case in which the biasing current source $I_{\text {BIAS }}$ is zero, the emitter current of $Q_{1}$ is equal to the base current of $Q_{2}$. Thus the ratio of $r_{\pi 1}$ to $r_{\pi 2}$ is $\left(\beta_{0}+1\right)$, and (3.111) reduces to

$$
\begin{equation*}
g_{m}^{c}=\frac{g_{m 2}}{2} \tag{3.112}
\end{equation*}
$$

The effective current gain $\beta^{c}$ is the ratio

$$
\begin{equation*}
\beta^{c}=\frac{i_{c}^{c}}{i_{b}^{c}}=\frac{i_{c 2}}{i_{b 1}} \tag{3.113}
\end{equation*}
$$

The emitter current of $Q_{1}$ is given by

$$
\begin{equation*}
i_{e 1}=\left(\beta_{0}+1\right) i_{b 1} \tag{3.114}
\end{equation*}
$$

Since $i_{e 1}=i_{b 2}$,

$$
\begin{equation*}
i_{c 2}=i_{c}^{c}=\beta_{0} i_{b 2}=\beta_{0}\left(\beta_{0}+1\right) i_{b 1}=\beta_{0}\left(\beta_{0}+1\right) i_{b}^{c} \tag{3.115}
\end{equation*}
$$

Therefore,

$$
\begin{equation*}
\beta^{c}=\beta_{0}\left(\beta_{0}+1\right) \tag{3.116}
\end{equation*}
$$

Equation 3.116 shows that the current gain of the composite transistor is approximately equal to $\beta_{0}^{2}$. Also, by inspection of Fig. 3.32, assuming $r_{\mu}$ is negligible, we have

$$
\begin{equation*}
r_{o}^{c}=r_{o 2} \tag{3.117}
\end{equation*}
$$

The small-signal, two-port network equivalent for the CC-CE connection is shown in Fig. 3.33, where the collector resistor $R_{C}$ has not been included. This small-signal equivalent can be used to represent the small-signal operation of the composite device, simplifying the analysis of circuits containing this structure.

The Darlington configuration, illustrated in Fig. 3.34, is a composite two-transistor device in which the collectors are tied together and the emitter of the first device drives the base of the second. A biasing element of some sort is used to control the emitter current of $Q_{1}$. The result is a three-terminal composite transistor that can be used in place of a single transistor in common-emitter, common-base, and common-collector configurations. When used as an emitter follower, the device is identical to the CC-CC connection already described. When used as a common-emitter amplifier, the device is very similar to the CC-CE connection, except that the collector of $Q_{1}$ is connected to the output instead of to the power supply. One effect of this change is to reduce the effective output resistance of the device
image_name:Figure 3.33 Two-port representation, CC-CE connection
description:
[
name: Rc_i, type: Resistor, value: Rc_i, ports: {N1: Vin, N2: GND}
name: Gc_m, type: CurrentControlledCurrentSource, value: Gc_m, ports: {Np: Vout, Nn: GND}
name: Rc_o, type: Resistor, value: Rc_o, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a two-port representation of a CC-CE connection. It includes a resistor Rc_i connected between Vin and GND, a current-controlled current source Gc_m controlled by V1 with output between Vout and GND, and a resistor Rc_o connected between Vout and GND. The equations for Rc_i, Gc_m, and Rc_o are provided, indicating their dependence on transistor parameters.
image_name:Figure 3.34 The Darlington configuration
description:
[
name: Rc_i, type: Resistor, value: Rc_i, ports: {N1: Vin, N2: GND}
name: Gc_m, type: VoltageControlledCurrentSource, value: Gc_m, ports: {Np: Vout, Nn: GND}
name: Rc_o, type: Resistor, value: Rc_o, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit represents a Darlington configuration with input at Vin and output at Vout. It includes a voltage-controlled current source Gc_m and resistors Rc_i and Rc_o. The configuration equations for Rc_i, Gc_m, and Rc_o are provided in the diagram.

Figure 3.33 Two-port representation, CC-CE connection.
image_name:Figure 3.34 The Darlington configuration
description:
[
name: Q1, type: NPN, ports: {C: CC, B: BC, E: elb2}
name: Q2, type: NPN, ports: {C: CC, B: elb2, E: EC}
name: IBIAS, type: CurrentSource, value: IBIAS, ports: {Np: elb2, Nn: EC}
]
extrainfo:The circuit is a Darlington configuration with two NPN transistors Q1 and Q2. The input is at BC and the output is at EC. IBIAS provides the biasing current for the transistors. The Darlington pair increases current gain.

Figure 3.34 The Darlington configuration.
because of feedback through the $r_{o}$ of $Q_{1}$. Also, this change increases the input capacitance because of the connection of the collector-base capacitance of $Q_{1}$ from the input to the output. Because of these drawbacks, the CC-CE connection is normally preferable in integrated smallsignal amplifiers. The term Darlington is often used to refer to both the CC-CE and CC-CC connections.

As mentioned previously, Darlington-type connections are used to boost the effective current gain of bipolar transistors and have no significant application in pure-MOS circuits. In BiCMOS technologies, however, a potentially useful connection is shown in Fig. 3.35, where an MOS transistor is used for $Q_{1}$. This configuration not only realizes the infinite input resistance and current gain of the MOS transistor, but also the large transconductance of the bipolar transistor.
image_name:Figure 3.35 Compound Darlington connection
description:
[
name: M1, type: NMOS, ports: {S: e2, D: s1g2, G: g1}
name: Q2, type: NPN, ports: {C: d1c2, B: s1g2, E: e2}
name: IBIAS, type: CurrentSource, value: IBIAS, ports: {Np: e2, Nn: s1g2}
]
extrainfo:This is a compound Darlington connection in BiCMOS technology, utilizing an NMOS transistor (M1) and an NPN transistor (Q2) to achieve high input resistance, current gain, and transconductance.

Figure 3.35 Compound Darlington connection available in BiCMOS technology.

#### EXAMPLE

Find the effective $r_{\pi}^{c}, \beta^{c}$, and $g_{m}^{c}$ for the composite transistor shown in Fig. 3.31. For both devices, assume that $\beta_{0}=100, r_{b}=0$, and $r_{o} \rightarrow \infty$. For $Q_{2}$, assume that $I_{C}=100 \mu \mathrm{~A}$ and that $I_{\text {BIAS }}=10 \mu \mathrm{~A}$.

The base current of $Q_{2}$ is $100 \mu \mathrm{~A} / 100=1 \mu \mathrm{~A}$. Thus the emitter current of $Q_{1}$ is $11 \mu \mathrm{~A}$. Then

$$
\begin{aligned}
r_{\pi 1} & =\frac{\beta_{0}}{g_{m}}=\frac{100}{11 \mu \mathrm{~A} / 26 \mathrm{mV}}=236 \mathrm{k} \Omega \\
g_{m 1} & =(2.36 \mathrm{k} \Omega)^{-1} \\
r_{\pi 2} & =26 \mathrm{k} \Omega \\
g_{m 2} & =(260 \Omega)^{-1} \\
r_{\pi}^{c} & =236 \mathrm{k} \Omega+(101)(26 \mathrm{k} \Omega)=2.8 \mathrm{M} \Omega \\
\beta^{c} & =(101)(100)=10,100 \\
g_{m}^{c} & =g_{m 2}(0.916)=(283 \Omega)^{-1}
\end{aligned}
$$

Thus the composite transistor has much higher input resistance and current gain than a single transistor.

### 3.4.2 The Cascode Configuration

The cascode configuration was first invented for vacuum-tube circuits. ${ }^{6,7}$ With vacuum tubes, the terminal that emits electrons is the cathode, the terminal that controls current flow is the grid, and the terminal that collects electrons is the anode. The cascode is a cascade of commoncathode and common-grid stages joined at the anode of the first stage and the cathode of the second stage. The cascode configuration is important mostly because it increases output resistance and reduces unwanted capacitive feedback in amplifiers, allowing operation at higher frequencies than would otherwise be possible. The high output resistance attainable is particularly useful in desensitizing bias references from variations in power-supply voltage and in achieving large amounts of voltage gain. These applications are described further in Chapter 4. The topic of frequency response is covered in Chapter 7. Here, we will focus on the low-frequency, small-signal properties of the cascode configuration.

3.4.2.1 The Bipolar Cascode

In bipolar form, the cascode is a common-emitter-common-base (CE-CB) amplifier, as shown in Fig. 3.36. We will assume here that $r_{b}$ in both devices is zero. Although the base resistances have a negligible effect on the low-frequency performance, the effects of nonzero $r_{b}$ are important in the high-frequency performance of this combination. These effects are considered in Chapter 7.

The small-signal equivalent for the bipolar cascode circuit is shown in Fig. 3.37. Since we are considering the low-frequency performance, we neglect the capacitances in the model of each transistor. We will determine the input resistance, output resistance, and transconductance of the cascode circuit. By inspection of Fig. 3.37, the input resistance is simply

$$
\begin{equation*}
R_{i}=r_{\pi 1} \tag{3.118}
\end{equation*}
$$

image_name:Figure 3.36
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: VBIAS, type: VoltageSource, value: VBIAS, ports: {Np: VBIAS, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: Ro, type: Resistor, value: Ro, ports: {N1: C2, N2: C2}
name: R, type: Resistor, value: R, ports: {N1: VDD, N2: Vout}
name: C2, type: Capacitor, value: C2, ports: {Np: C2, Nn: VDD}
name: Q1, type: NPN, ports: {C: CR2, B: Vi, E: GND}
name: Q2, type: NPN, ports: {C: C2, B: CR2, E: VBIAS}
]
extrainfo:The circuit is a cascode amplifier using bipolar transistors. It features two NPN transistors (Q1 and Q2) in a cascode configuration to improve performance metrics such as gain and bandwidth. The input is connected to Vi, and the output is taken across the resistor R. The bias voltage VBIAS is used to set the operating point of Q2. The circuit is powered by VDD.
image_name:Figure 3.37
description:
[
name: Q1, type: NPN, ports: {C: C1, B: Vi, E: GND}
name: Q2, type: NPN, ports: {C: C2, B: C1, E: C1}
name: VBIAS, type: VoltageSource, value: VBIAS, ports: {Np: C1, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: Ro, type: Resistor, value: Ro, ports: {N1: C2, N2: C2}
name: R, type: Resistor, value: R, ports: {N1: C2, N2: Vout}
name: C2, type: Capacitor, value: C2, ports: {Np: C2, Nn: VDD}
]
extrainfo:The circuit is a small-signal equivalent of a bipolar-transistor cascode amplifier. It is used to analyze input resistance, output resistance, and transconductance. The circuit simplifies the analysis by neglecting capacitances and assumes unity current gain from emitter to collector in Q2.

Figure 3.37 Small-signal equivalent circuit for the bipolar-transistor cascode connection.

Since the current gain from the emitter to the collector of $Q_{2}$ is nearly unity, the transconductance of the circuit from input to output is

$$
\begin{equation*}
G_{m} \simeq g_{m 1} \tag{3.119}
\end{equation*}
$$

The output resistance can be calculated by shorting the input $v_{i}$ to ground and applying a test signal at the output. Then $v_{1}=0$ in Fig. 3.37 and the $g_{m 1} v_{1}$ generator is inactive. The circuit is then identical to that of Fig. $3.26 c$ for a bipolar transistor with emitter degeneration. Therefore, using (3.98) with $R_{E}=r_{o 1}$ shows that the output resistance is

$$
\begin{equation*}
R_{o} \simeq r_{o 2}\left(1+\frac{g_{m 2} r_{o 1}}{1+\frac{g_{m 2} r_{o 1}}{\beta_{0}}}\right) \tag{3.120}
\end{equation*}
$$

If $g_{m 2} r_{o 1} \gg \beta_{0}$ and $\beta_{0} \gg 1$,

$$
\begin{equation*}
R_{o} \simeq \beta_{0} r_{o 2} \tag{3.121}
\end{equation*}
$$

Therefore, the CE-CB connection displays an output resistance that is larger by a factor of about $\beta_{0}$ than the CE stage alone. If this circuit is operated with a hypothetical collector load that has infinite incremental resistance, the voltage gain is

$$
\begin{equation*}
A_{v}=\frac{v_{o}}{v_{i}}=-G_{m} R_{o} \simeq-g_{m 1} r_{o 2} \beta_{0}=-\frac{\beta_{0}}{\eta} \tag{3.122}
\end{equation*}
$$

Thus the magnitude of the maximum available voltage gain is higher by a factor $\beta_{0}$ than for the case of a single transistor. For a typical npn transistor, the ratio of $\beta_{0} / \eta$ is approximately $2 \times 10^{5}$. In this analysis, we have neglected $r_{\mu}$. As described in Chapter 1 , the value of $r_{\mu}$ for integrated-circuit npn transistors is usually much larger than $\beta_{0} r_{o}$, and then $r_{\mu}$ has little effect on $R_{o}$. For lateral pnp transistors, however, $r_{\mu}$ is comparable with $\beta_{0} r_{o}$ and decreases $R_{o}$ somewhat.
image_name:Figure 3.38 Cascode amplifier using MOSFETs
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1e2, G: Vi}
name: M2, type: NMOS, ports: {S: d1e2, D: d2, G: VBIAS}
name: R, type: Resistor, value: R, ports: {N1: d2, N2: VDD}
name: V_BIAS, type: VoltageSource, value: V_BIAS, ports: {Np: VBIAS, Nn: GND}
name: V_DD, type: VoltageSource, value: V_DD, ports: {Np: VDD, Nn: GND}
name: V_i, type: VoltageSource, value: V_i, ports: {Np: Vi, Nn: GND}
]
extrainfo:The circuit is a cascode amplifier using MOSFETs. It consists of two NMOS transistors in a common-source-common-gate configuration. The input signal is applied to the gate of M1, and the output is taken from the drain of M2. The circuit is biased by V_BIAS and powered by V_DD.

Figure 3.38 Cascode amplifier using MOSFETs.
image_name:Figure 3.39 Small-signal equivalent circuit for the MOS-transistor cascode connection
description:
[
name: gm1vi, type: VoltageControlledCurrentSource, ports: {Np: d1e2, Nn: GND}
name: ro1, type: Resistor, value: ro1, ports: {N1: d1e2, N2: GND}
name: gm2vgs2, type: VoltageControlledCurrentSource, ports: {Np: d2, Nn: d1e2}
name: gmb2vbs2, type: VoltageControlledCurrentSource, ports: {Np: d2, Nn: d1e2}
name: ro2, type: Resistor, value: ro2, ports: {N1: d2, N2: d1e2}
name: R, type: Resistor, value: R, ports: {N1: d2, N2: GND}
name: V_i, type: VoltageSource, value: V_i, ports: {Np: Vi, Nn: GND}
]
extrainfo:The circuit is a small-signal equivalent of a MOS-transistor cascode connection. It includes two voltage-controlled current sources representing the transconductance of the MOSFETs, resistors modeling the output resistance, and a voltage source for input.

Figure 3.39 Small-signal equivalent circuit for the MOS-transistor cascode connection.

3.4.2.2 The MOS Cascode

In MOS form, the cascode is a common-source-common-gate (CS-CG) amplifier, as shown in Fig. 3.38. The small-signal equivalent circuit is shown in Fig. 3.39. Since the input is connected to the gate of $M_{1}$, the input resistance is

$$
\begin{equation*}
R_{i} \rightarrow \infty \tag{3.123}
\end{equation*}
$$

To find the transconductance, set $R=0$ to short the output and calculate the current $i_{o}$. From KCL at the output,

$$
\begin{equation*}
i_{o}+g_{m 2} v_{d s 1}+g_{m b 2} v_{d s 1}+\frac{v_{d s 1}}{r_{o 2}}=0 \tag{3.124}
\end{equation*}
$$

From KCL at the source of $M_{2}$,

$$
\begin{equation*}
g_{m 1} v_{i}+g_{m 2} v_{d s 1}+g_{m b 2} v_{d s 1}+\frac{v_{d s 1}}{r_{o 1}}+\frac{v_{d s 1}}{r_{o 2}}=0 \tag{3.125}
\end{equation*}
$$

Solving (3.125) for $v_{d s 1}$, substituting into (3.124), and rearranging gives

$$
\begin{equation*}
G_{m}=\left.\frac{i_{o}}{v_{i}}\right|_{v_{o}=0}=g_{m 1}\left(1-\frac{1}{1+\left(g_{m 2}+g_{m b 2}\right) r_{o 1}+\frac{r_{o 1}}{r_{o 2}}}\right) \simeq g_{m 1} \tag{3.126}
\end{equation*}
$$

Equation 3.126 shows that the transconductance of the simple cascode is less than $g_{m 1}$. If $\left(g_{m 2}+g_{m b 2}\right) r_{o 1} \gg 1$, however, the difference is small, and the main point here is that the cascode configuration has little effect on the transconductance. This result stems from the observation that $R_{i 2}$, the resistance looking in the source of $M_{2}$, is much less than $r_{o 1}$. From (3.54) and (3.55) with $R=R_{D} \| R_{L}$,

$$
\begin{equation*}
R_{i 2}=\frac{r_{o 2}+R}{1+\left(g_{m 2}+g_{m b 2}\right) r_{o 2}} \simeq \frac{1}{g_{m 2}+g_{m b 2}}+\frac{R}{\left(g_{m 2}+g_{m b 2}\right) r_{o 2}} \tag{3.127}
\end{equation*}
$$

In finding the transconductance, we set $R=0$ so that $v_{o}=0$. Then $R_{i 2} \simeq 1 /\left(g_{m}+g_{m b}\right)$, and most of the $g_{m 1} v_{i}$ current flows in the source of $M_{2}$ because $R_{i 2} \ll r_{o 1}$. Finally, the current gain from the source to the drain of $M_{2}$ is unity. Therefore, most of the $g_{m 1} v_{i}$ current flows in the output, and $G_{m} \simeq g_{m 1}$, as shown in (3.126).

To find the output resistance, set $v_{i}=0$, which deactivates the $g_{m 1}$ generator in Fig. 3.39 and reduces the model for common-source transistor $M_{1}$ to simply $r_{o 1}$. Therefore, the output resistance of the cascode can be found by substituting $R_{S}=r_{o 1}$ in (3.66), which was derived for a common-gate amplifier. To focus on the output resistance of the cascode itself, let $R \rightarrow \infty$. The result is

$$
\begin{equation*}
R_{o}=r_{o 1}+r_{o 2}+\left(g_{m 2}+g_{m b 2}\right) r_{o 1} r_{o 2} \simeq\left(g_{m 2}+g_{m b 2}\right) r_{o 1} r_{o 2} \tag{3.128}
\end{equation*}
$$

Equation 3.128 shows that the MOS cascode increases the output resistance by a factor of about $\left(g_{m}+g_{m b}\right) r_{o}$ compared to a common-source amplifier.

The increase in the output resistance can be predicted in another way that provides insight into the operation of the cascode. Let $i_{o}$ represent the current that flows in the output node in Fig. 3.39 when the output is driven by voltage $v_{o}$. Since $v_{d s 1}=i_{o} r_{o 1}$ when $v_{i}=0$, the output resistance is

$$
\begin{equation*}
R_{o}=\left.\frac{v_{o}}{i_{o}}\right|_{v_{i}=0}=\left.\frac{v_{o}}{\left(v_{d s 1} / r_{o 1}\right)}\right|_{v_{i}=0}=\left.r_{o 1}\left(\frac{v_{d s 1}}{v_{o}}\right)^{-1}\right|_{v_{i}=0} \tag{3.129}
\end{equation*}
$$

To find the ratio $v_{d s 1} / v_{o}$, consider the modified small-signal circuits shown in Fig. 3.40. In Fig. 3.40a, $R \rightarrow \infty$ so we can concentrate on the output resistance of the cascode circuit itself. Also, the $g_{m 1} v_{i}$ generator is eliminated because $v_{i}=0$, and the two generators $g_{m 2} v_{d s 1}$ and $g_{m b 2} v_{d s 1}$ have been combined into one equivalent generator $\left(g_{m 2}+g_{m b 2}\right) v_{d s 1}$. In Fig. 3.40b,
image_name:(a)
description:
[
name: ro1, type: Resistor, value: ro1, ports: {N1: X, N2: GND}
name: ro2, type: Resistor, value: ro2, ports: {N1: Vo, N2: X}
name: (gm2+gmb2)vds1, type: VoltageControlledCurrentSource, ports: {Np: Vo, Nn: X}
name: vo, type: VoltageSource, value: vo, ports: {Np: Vo, Nn: GND}
]
extrainfo:The circuit represents a cascode amplifier model focusing on the output resistance. The dependent current source is represented as (gm2+gmb2)vds1, and the resistors ro1 and ro2 are connected to the output node Vo. The voltage source vo is connected between Vo and ground.
image_name:(b)
description:
[
name: (gm2 + gmb2)vds1, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: vo}
name: (gm2 + gmb2)vds1, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: X}
name: ro1, type: Resistor, value: ro1, ports: {N1: X, N2: GND}
name: ro2, type: Resistor, value: ro2, ports: {N1: vo, N2: X}
name: vo, type: VoltageSource, value: vo, ports: {Np: vo, Nn: GND}
]
extrainfo:The circuit diagram represents a modified cascode configuration with two voltage-controlled current sources and resistors ro1 and ro2. The output voltage source vo is connected between the node vo and ground.
image_name:(c)
description:
[
name: (gm2 + gmb2)vds1, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: vo}
name: ro1, type: Resistor, value: ro1, ports: {N1: x, N2: GND}
name: ro2, type: Resistor, value: ro2, ports: {N1: vo, N2: x}
name: vo, type: VoltageSource, value: vo, ports: {Np: vo, Nn: GND}
]
extrainfo:This circuit is part of a cascode model to find the voltage ratio vds1/vo, featuring a voltage-controlled current source and resistors ro1 and ro2. The current source is connected between GND and node vo, and the resistors form a path from node x to vo.

Figure 3.40 Construction of a cascode model to find $v_{d s 1} / v_{o}$. (a) The dependent sources are combined. (b) The combined source is converted into two sources. (c) The current source between the source of $M_{2}$ and ground is converted into a resistor.
the $\left(g_{m 2}+g_{m b 2}\right) v_{d s 1}$ generator from the source to the drain of $M_{2}$ has been replaced by two equal-valued generators: one from ground to the drain of $M_{2}$ and the other from the source of $M_{2}$ to ground. This replacement is similar to the substitution made in Fig. 3.20 to convert the hybrid- $\pi$ model to a T model for a common-gate amplifier. Because the equations that describe the operation of the circuits in Fig. 3.40a and Fig. 3.40b are identical, the circuit in Fig. 3.40b is equivalent to that in Fig. 3.40a. Finally, in Fig. 3.40c, the current source from the source of $M_{2}$ to ground, which is controlled by the voltage across itself, is replaced by an equivalent resistor of value $1 /\left(g_{m 2}+g_{m b 2}\right)$. The current $\left(g_{m 2}+g_{m b 2}\right) v_{d s 1}$ in Fig. $3.40 c$ flows into the test source $v_{o}$. The two resistors in Fig. 3.40c form a voltage divider, giving

$$
\begin{equation*}
\frac{v_{d s 1}}{v_{o}}=\frac{\left(\frac{1}{g_{m 2}+g_{m b 2}}\right) \| r_{o 1}}{\left[\left(\frac{1}{g_{m 2}+g_{m b 2}}\right) \| r_{o 1}\right]+r_{o 2}} \simeq \frac{1}{\left(g_{m 2}+g_{m b 2}\right) r_{o 2}} \tag{3.130}
\end{equation*}
$$

Substituting (3.130) into (3.129) and rearranging gives the same result as in (3.128). In (3.130), the term $1 /\left(g_{m 2}+g_{m b 2}\right)$ represents the resistance looking into the source of the common-gate transistor $M_{2}$ when the output in Fig. 3.39 is voltage driven. The key point here is that the output resistance of the cascode can be increased by reducing the input resistance of the common-gate transistor under these conditions because this change reduces both $v_{d s 1}$ and $i_{o}$.

Unlike in the bipolar case, the maximum value of the output resistance in the MOS cascode does not saturate at a level determined by $\beta_{0}$; therefore, further increases in the output resistance can be obtained by using more than one level of cascoding. This approach is used in practice. Ultimately, the maximum output resistance is limited by impact ionization as described in Section 1.9 or by leakage current in the reverse-biased junction diode at the output. Also, the number of levels of cascoding is limited by the power-supply voltage and signal-swing requirements. Each additional level of cascoding places one more transistor in series with the input transistor between the power supply and ground. To operate all the transistors in the active region, the drain-source voltage of each transistor must be greater than its overdrive $V_{G S}-V_{t}$. Since the cascode transistors operate in series with the input transistor, additional levels of cascoding use some of the available power-supply voltage, reducing the amount by which the output can vary before pushing one or more transistors into the triode region. This topic is considered further in Chapter 4.

In BiCMOS technologies, cascodes are sometimes used with the MOS transistor $M_{2}$ in Fig. 3.38 replaced by a bipolar transistor, such as $Q_{2}$ in Fig. 3.36. This configuration has the infinite input resistance given by $M_{1}$. Also, the resistance looking into the emitter of the commonbase stage $Q_{2}$ when the output is grounded is $R_{i 2} \simeq 1 / g_{m 2}$ in this configuration. Since the transconductance for a given bias current of bipolar transistors is usually much greater than for MOS transistors, the BiCMOS configuration is often used to reduce the load resistance presented to $M_{1}$ and to improve the high-frequency properties of the cascode amplifier. The frequency response of a cascode amplifier is described in Chapter 7.

#### EXAMPLE

Calculate the transconductance and output resistance of the cascode circuit of Fig. 3.38. Assume that both transistors operate in the active region with $g_{m}=1 \mathrm{~mA} / \mathrm{V}, \chi=0.1$, and $r_{o}=20 \mathrm{k} \Omega$.

From (3.126),

$$
G_{m}=\left(1 \frac{\mathrm{~mA}}{\mathrm{~V}}\right)\left(1-\frac{1}{1+(1.1)(20)+1}\right)=960 \frac{\mu \mathrm{~A}}{\mathrm{~V}}
$$

From (3.128),

$$
R_{o}=20 \mathrm{k} \Omega+20 \mathrm{k} \Omega+(1.1)(20) 20 \mathrm{k} \Omega=480 \mathrm{k} \Omega
$$

The approximations in (3.126) and (3.128) give $G_{m} \simeq 1 \mathrm{~mA} / \mathrm{V}$ and $R_{o} \simeq 440 \mathrm{k} \Omega$. These approximations deviate from the exact results by about 4 percent and 8 percent, respectively, and are usually close enough for hand calculations.

### 3.4.3 The Active Cascode

As mentioned in the previous section, increasing the number of levels of cascoding increases the output resistance of MOS amplifiers. In practice, however, the power-supply voltage and signal-swing requirements limit the number of levels of cascoding that can be applied. One way to increase the output resistance of the MOS cascode circuit without increasing the number of levels of cascoding is to use the active-cascode circuit, as shown in Fig. 3.41. 8,9

This circuit uses an amplifier in a negative feedback loop to control the voltage from the gate of $M_{2}$ to ground. If the amplifier gain $a$ is infinite, the negative feedback loop adjusts the gate of $M_{2}$ until the voltage difference between the two amplifier inputs is zero. In other words, the drain-source voltage of $M_{1}$ is driven to equal $V_{\text {BIAS }}$. If the drain-source voltage of $M_{1}$ is constant, the change in the drain current in response to changes in the output voltage $V_{o}$ is zero, and the output resistance is infinite. In practice, the amplifier gain $a$ is finite, which means that the drain-source voltage of $M_{1}$ is not exactly constant and the output resistance is finite. The effect of negative feedback on output resistance is considered quantitatively in Chapter 8. In this section, we will derive the small-signal properties of the active-cascode circuit by comparing its small-signal model to that of the simple cascode described in the previous section.

Qualitatively, when the output voltage increases, the drain current of $M_{2}$ increases, which increases the drain current and drain-source voltage of $M_{1}$. This voltage increase is amplified by $-a$, causing the voltage from the gate of $M_{2}$ to ground to fall. The falling gate voltage of $M_{2}$ acts to reduce the change in its drain current, increasing the output resistance compared to a simple cascode, where the voltage from the gate of $M_{2}$ to ground is held constant.

Figure 3.42 shows the low-frequency, small-signal equivalent circuit. The body-effect transconductance generator for $M_{1}$ is inactive because $v_{b s 1}=0$. The gate-source voltage of $M_{2}$ is

$$
\begin{equation*}
v_{g s 2}=v_{g 2}-v_{s 2}=v_{g 2}-v_{d s 1}=-(a) v_{d s 1}-v_{d s 1}=-(a+1) v_{d s 1} \tag{3.131}
\end{equation*}
$$

image_name:Figure 3.41 Active cascode amplifier using MOSFETs
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1s2, G: Vi}
name: M2, type: NMOS, ports: {S: d1s2, D: Vo, G: g2}
name: R, type: Resistor, value: R, ports: {N1: VDD, N2: Vo}
name: V_BIAS, type: VoltageSource, value: V_BIAS, ports: {Np: V_BIAS, Nn: GND}
name: OpAmp, type: OpAmp, value: a, ports: {InP: V_BIAS, InN: d1s2, OutP: g2}
]
extrainfo:The circuit is an active cascode amplifier using MOSFETs. The op-amp provides feedback to the gate of M2, enhancing the output resistance. The input signal Vi is applied to the gate of M1, and the output is taken from Vo.

Figure 3.41 Active cascode amplifier using MOSFETs.
image_name:Figure 3.42 Small-signal equivalent circuit for the active-cascode connection with MOS transistors
description:
[
name: vi, type: VoltageSource, value: vi, ports: {Np: vi, Nn: GND}
name: gm2vgs2, type: VoltageControlledCurrentSource, value: gm2vgs2, ports: {Np: d2, Nn: d1s2}
name: 8mb2vbs2, type: VoltageControlledCurrentSource, value: 8mb2vbs2, ports: {Np: d2, Nn: d1s2}
name: gm1vi, type: VoltageControlledCurrentSource, value: gm1vi, ports: {Np: d1s2, Nn: GND}
name: ro2, type: Resistor, value: ro2, ports: {N1: d2, N2: d1s2}
name: ro1, type: Resistor, value: ro1, ports: {N1: d1s2, N2: GND}
name: R, type: Resistor, value: R, ports: {N1: d2, N2: vo}
]
extrainfo:The circuit diagram is a small-signal equivalent circuit for an active-cascode connection with MOS transistors. It includes voltage-controlled current sources representing the transconductance of MOSFETs, and resistors representing output resistances. The input voltage is applied at node 'vi', and the output is taken across resistor 'R' at node 'vo'.

Figure 3.42 Small-signal equivalent circuit for the active-cascode connection with MOS transistors.

In contrast, $v_{g s 2}=-v_{d s 1}$ in a simple cascode because the voltage from the gate of $M_{2}$ to ground is constant in Fig. 3.38. Therefore, if $a>0$, the factor $(a+1)$ in (3.131) amplifies the gate-source voltage of $M_{2}$ compared to the case of a simple cascode. This amplification is central to the characteristics of the active-cascode circuit. Since the small-signal diagrams of the simple and active-cascode circuits are identical except for the value of $v_{g s 2}$, and since $v_{g s 2}$ is only used to control the current flowing in the $g_{m 2}$ generator, the active-cascode circuit can be analyzed using the equations for the simple cascode with $g_{m 2}$ replaced by $(a+1) g_{m 2}$. In other words, the active cascode behaves as if it were a simple cascode with an enhanced value of $g_{m 2}$.

To find the transconductance of the active cascode, $g_{m 2}(a+1)$ replaces $g_{m 2}$ in (3.126), giving

$$
\begin{equation*}
G_{m}=g_{m 1}\left(1-\frac{1}{1+\left[g_{m 2}(a+1)+g_{m b 2}\right] r_{o 1}+\frac{r_{o 1}}{r_{o 2}}}\right) \tag{3.132}
\end{equation*}
$$

Again, $G_{m} \simeq g_{m 1}$ under most conditions; therefore, the active-cascode structure is generally not used to modify the transconductance.

The active cascode reduces $R_{i 2}$, the resistance looking into the source of $M_{2}$, compared to the simple cascode, which reduces the $v_{d s 1} / v_{o}$ ratio given in (3.130) and increases the output resistance. Substituting (3.130) into (3.129) with $g_{m 2}(a+1)$ replacing $g_{m 2}$ gives

$$
\begin{equation*}
R_{o}=r_{o 1}+r_{o 2}+\left[g_{m 2}(a+1)+g_{m b 2}\right] r_{o 1} r_{o 2} \simeq\left[g_{m 2}(a+1)+g_{m b 2}\right] r_{o 1} r_{o 2} \tag{3.133}
\end{equation*}
$$

This result can also be derived by substituting $g_{m 2}(a+1)$ for $g_{m 2}$ in (3.128). Equation 3.133 shows that the active-cascode configuration increases the output resistance by a factor of about $\left[g_{m}(a+1)+g_{m b}\right] r_{o}$ compared to a common-source amplifier.

A key limitation of the active-cascode circuit is that the output impedance is increased only at frequencies where the amplifier that drives the gate of $M_{2}$ provides some gain. In practice, the gain of this amplifier falls with increasing frequency, reducing the potential benefits of the active-cascode circuits in high-frequency applications. A potential problem with the activecascode configuration is that the negative feedback loop through $M_{2}$ may not be stable in all cases.

### 3.4.4 The Super Source Follower

Equation 3.84 shows that the output resistance of a source follower is approximately $1 /\left(g_{m}+\right.$ $g_{m b}$ ). Because MOS transistors usually have much lower transconductance than their bipolar counterparts, this output resistance may be too high for some applications, especially when a resistive load must be driven. One way to reduce the output resistance is to increase the transconductance by increasing the $W / L$ ratio of the source follower and its dc bias current. However, this approach requires a proportionate increase in the area and power dissipation to reduce $R_{o}$. To minimize the area and power dissipation required to reach a given output resistance, the super source follower configuration shown in Fig. 3.43 is sometimes used. This circuit uses negative feedback through $M_{2}$ to reduce the output resistance. Negative feedback is studied quantitatively in Chapter 8. From a qualitative standpoint, when the input voltage is constant and the output voltage increases, the magnitude of the drain current of $M_{1}$ also increases, in turn increasing the gate-source voltage of $M_{2}$. As a result, the drain current of $M_{2}$ increases, reducing the output resistance by increasing the total current that flows into the output node under these conditions.

From a dc standpoint, the bias current in $M_{2}$ is the difference between $I_{1}$ and $I_{2}$; therefore, $I_{1}>I_{2}$ is required for proper operation. This information can be used to find the small-signal parameters of both transistors. The small-signal equivalent circuit is shown in Fig. 3.44. The body-effect transconductance generator for $M_{2}$ is inactive because $v_{b s 2}=0$. Also, the polarities of the voltage-controlled current sources for $n$ - and $p$-channel devices are identical. Finally, the output resistances of current sources $I_{1}$ and $I_{2}$ are represented by $r_{1}$ and $r_{2}$, respectively.
image_name:Figure 3.43 Super-source-follower configuration
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: Vo, G: Vi}
name: M2, type: NMOS, ports: {S: GND, D: Vo, G: d1g2}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: Vo}
name: I2, type: CurrentSource, value: I2, ports: {Np: d1g2, Nn: GND}
name: r1, type: Resistor, value: r1, ports: {N1: v2, N2: GND}
name: r2, type: Resistor, value: r2, ports: {N1: v2, N2: GND}
name: ro1, type: Resistor, value: ro1, ports: {N1: Vo, N2: x}
name: ro2, type: Resistor, value: ro2, ports: {N1: Vo, N2: vo}
]
extrainfo:The circuit is a super-source-follower configuration with PMOS M1 and NMOS M2. It uses current sources I1 and I2. The resistors r1 and r2 are connected to the node v2. The output is taken from node Vo.
image_name:Figure 3.44 Small-signal equivalent circuit of the super-source follower
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: Vo, G: Vi}
name: M2, type: NMOS, ports: {S: GND, D: Vo, G: d1g2}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: Vo}
name: I2, type: CurrentSource, value: I2, ports: {Np: d1g2, Nn: GND}
name: r1, type: Resistor, value: r1, ports: {N1: V2, N2: GND}
name: r2, type: Resistor, value: r2, ports: {N1: V2, N2: GND}
name: ro1, type: Resistor, value: ro1, ports: {N1: Vo, N2: X}
name: ro2, type: Resistor, value: ro2, ports: {N1: Vo, N2: Vo}
]
extrainfo:The circuit represents a small-signal equivalent of a super-source follower. It includes PMOS and NMOS transistors, with current sources and resistors. The body-effect transconductance generator for M2 is inactive, and the output resistances of current sources I1 and I2 are represented by r1 and r2. The circuit is used to analyze the output resistance by setting Vi=0 and calculating the current io at the output node when driven by a voltage Vo.

Figure 3.44 Small-signal equivalent circuit of the super-source follower.

If the current sources are ideal, $r_{1} \rightarrow \infty$ and $r_{2} \rightarrow \infty$. In practice, these resistances are large but finite. Techniques to build high-resistance current sources are considered in Chapter 4.

To find the output resistance, set $v_{i}=0$ and calculate the current $i_{o}$ that flows in the output node when the output is driven by a voltage $v_{o}$. From KCL at the output under these conditions,

$$
\begin{equation*}
i_{o}=\frac{v_{o}}{r_{1}}+\frac{v_{o}}{r_{o 2}}+g_{m 2} v_{2}+\frac{v_{2}}{r_{2}} \tag{3.134}
\end{equation*}
$$

From KCL at the drain of $M_{1}$ with $v_{i}=0$,

$$
\begin{equation*}
\frac{v_{2}}{r_{2}}-g_{m 1} v_{o}-g_{m b 1} v_{o}+\frac{v_{2}-v_{o}}{r_{o 1}}=0 \tag{3.135}
\end{equation*}
$$

Solving (3.135) for $v_{2}$, substituting into (3.134), and rearranging gives

$$
\begin{equation*}
R_{o}=\left.\frac{v_{o}}{i_{o}}\right|_{v_{i}=0}=r_{1}\left\|r_{o 2}\right\|\left(\frac{r_{o 1}+r_{2}}{\left[1+\left(g_{m 1}+g_{m b 1}\right) r_{o 1}\right]\left(1+g_{m 2} r_{2}\right)}\right) \tag{3.136}
\end{equation*}
$$

Assume $I_{1}$ and $I_{2}$ are ideal current sources so that $r_{1} \rightarrow \infty$ and $r_{2} \rightarrow \infty$. If $r_{o 2} \rightarrow \infty$, and if $\left(g_{m 1}+g_{m b 1}\right) r_{o 1} \gg 1$,

$$
\begin{equation*}
R_{o} \simeq \frac{1}{g_{m 1}+g_{m b 1}}\left(\frac{1}{g_{m 2} r_{o 1}}\right) \tag{3.137}
\end{equation*}
$$

Comparing (3.84) and (3.137) shows that the negative feedback through $M_{2}$ reduces the output resistance by a factor of about $g_{m 2} r_{o 1}$.

Now we will calculate the open-circuit voltage gain of the super-source follower. With the output open circuited, KCL at the output node gives

$$
\begin{equation*}
\frac{v_{o}}{r_{1}}+\frac{v_{o}}{r_{o 2}}+g_{m 2} v_{2}+\frac{v_{2}}{r_{2}}=0 \tag{3.138}
\end{equation*}
$$

From KCL at the drain of $M_{1}$,

$$
\begin{equation*}
\frac{v_{2}}{r_{2}}+g_{m 1}\left(v_{i}-v_{o}\right)-g_{m b 1} v_{o}+\frac{v_{2}-v_{o}}{r_{o 1}}=0 \tag{3.139}
\end{equation*}
$$

Solving (3.138) for $v_{2}$, substituting into (3.139), and rearranging gives

$$
\begin{equation*}
\left.\frac{v_{o}}{v_{i}}\right|_{i_{o}=0}=\frac{g_{m 1} r_{o 1}}{1+\left(g_{m 1}+g_{m b 1}\right) r_{o 1}+\frac{\left(r_{2}+r_{o 1}\right)}{\left(r_{1} \| r_{o 2}\right)\left(1+g_{m 2} r_{2}\right)}} \tag{3.140}
\end{equation*}
$$

With ideal current sources,

$$
\begin{equation*}
\left.\lim _{\substack{r_{1} \rightarrow \infty \\ r_{2} \rightarrow \infty}} \frac{v_{o}}{v_{i}}\right|_{i_{o}=0}=\frac{g_{m 1} r_{o 1}}{1+\left(g_{m 1}+g_{m b 1}\right) r_{o 1}+\frac{1}{g_{m 2} r_{o 2}}} \tag{3.141}
\end{equation*}
$$

Comparing (3.141) and (3.81) shows that the deviation of this gain from unity is greater than with a simple source follower. If $g_{m 2} r_{o 2} \gg 1$, however, the difference is small and the main conclusion is that the super-source-follower configuration has little effect on the open-circuit voltage gain.

As mentioned earlier, the super-source follower is sometimes used in MOS technologies to reduce the source-follower output resistance. It is also used in bipolar technologies in output stages to reduce the current conducted in a weak lateral pnp transistor. This application is
described in Chapter 5. The main potential problem with the super-source-follower configuration is that the negative feedback loop through $M_{2}$ may not be stable in all cases, especially when driving a capacitive load. The stability of feedback amplifiers is considered in Chapter 9.

## 3.5 Differential Pairs

The differential pair is another example of a circuit that was first invented for use with vacuum tubes. ${ }^{10}$ The original circuit uses two vacuum tubes whose cathodes are connected together. Modern differential pairs use bipolar or MOS transistors coupled at their emitters or sources, respectively, and are perhaps the most widely used two-transistor subcircuits in monolithic analog circuits. The usefulness of the differential pair stems from two key properties. First, cascades of differential pairs can be directly connected to one another without interstage coupling capacitors. Second, the differential pair is primarily sensitive to the difference between two input voltages, allowing a high degree of rejection of signals common to both inputs. ${ }^{11,12}$ In this section, we consider the properties of emitter-coupled pairs of bipolar transistors and source-coupled pairs of MOS transistors in detail.

### 3.5.1 The dc Transfer Characteristic of an Emitter-Coupled Pair

The simplest form of an emitter-coupled pair is shown in Fig. 3.45. The biasing circuit in the lead connected to the emitters of $Q_{1}$ and $Q_{2}$ can be a transistor current source, which is called a tail current source, or a simple resistor. If a simple resistor $R_{\text {TAIL }}$ is used alone, $I_{\text {TAIL }}=0$ in Fig. 3.45. Otherwise, $I_{\text {TAIL }}$ and $R_{\text {TAIL }}$ together form a Norton-equivalent model of the tail current source.

The large-signal behavior of the emitter-coupled pair is important in part because it illustrates the limited range of input voltages over which the circuit behaves almost linearly. Also, the large-signal behavior shows that the amplitude of analog signals in bipolar circuits can be limited without pushing the transistors into saturation, where the response time would be increased because of excess charge storage in the base region. For simplicity in the analysis, we assume that the output resistance of the tail current source $R_{\text {TAIL }} \rightarrow \infty$, that the output resistance of each transistor $r_{o} \rightarrow \infty$, and that the base resistance of each transistor $r_{b}=0$. These
image_name:Figure 3.45 Emitter-coupled pair circuit diagram
description:
[
name: Q1, type: NPN, ports: {C: V_o1, B: V_i1, E: X}
name: Q2, type: NPN, ports: {C: V_o2, B: V_i2, E: X}
name: RC, type: Resistor, value: RC, ports: {N1: V_CC, N2: V_o1}
name: RC, type: Resistor, value: RC, ports: {N1: V_CC, N2: V_o2}
name: ITAIL, type: CurrentSource, value: ITAIL, ports: {Np: X, Nn: V_EE}
name: RTAIL, type: Resistor, value: RTAIL, ports: {N1: X, N2: V_EE}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: V_CC, Nn: GND}
name: VEE, type: VoltageSource, value: VEE, ports: {Np: GND, Nn: V_EE}
name: Vi1, type: VoltageSource, value: Vi1, ports: {Np: V_i1, Nn: GND}
name: Vi2, type: VoltageSource, value: Vi2, ports: {Np: V_i2, Nn: GND}
]
extrainfo:The circuit is an emitter-coupled pair with two NPN transistors Q1 and Q2. It uses a current source ITAIL and a resistor RTAIL to establish the tail current. The collector resistors RC are connected to VCC, and the emitters of Q1 and Q2 are connected together at node X. The input voltages Vi1 and Vi2 control the differential pair operation.

Figure 3.45 Emitter-coupled pair circuit diagram.
assumptions do not strongly affect the low-frequency, large-signal behavior of the circuit. From KVL around the input loop,

$$
\begin{equation*}
V_{i 1}-V_{b e 1}+V_{b e 2}-V_{i 2}=0 \tag{3.142}
\end{equation*}
$$

Assume the collector resistors are small enough that the transistors do not operate in saturation if $V_{i 1} \leq V_{C C}$ and $V_{i 2} \leq V_{C C}$. If $V_{b e 1} \gg V_{T}$ and $V_{b e 2} \gg V_{T}$, the Ebers-Moll equations show that

$$
\begin{align*}
& V_{b e 1}=V_{T} \ln \frac{I_{c 1}}{I_{S 1}}  \tag{3.143}\\
& V_{b e 2}=V_{T} \ln \frac{I_{c 2}}{I_{S 2}} \tag{3.144}
\end{align*}
$$

Assume the transistors are identical so that $I_{S 1}=I_{S 2}$. Then combining (3.142), (3.143), and (3.144), we find

$$
\begin{equation*}
\frac{I_{c 1}}{I_{c 2}}=\exp \left(\frac{V_{i 1}-V_{i 2}}{V_{T}}\right)=\exp \left(\frac{V_{i d}}{V_{T}}\right) \tag{3.145}
\end{equation*}
$$

where $V_{i d}=V_{i 1}-V_{i 2}$. Since we have assumed that the transistors are identical, $\alpha_{F 1}=$ $\alpha_{F 2}=\alpha_{F}$. Then KCL at the emitters of the transistors shows

$$
\begin{equation*}
-\left(I_{e 1}+I_{e 2}\right)=I_{\mathrm{TAIL}}=\frac{I_{c 1}+I_{c 2}}{\alpha_{F}} \tag{3.146}
\end{equation*}
$$

Combining (3.145) and (3.146), we find that

$$
\begin{align*}
& I_{c 1}=\frac{\alpha_{F} I_{\mathrm{TAIL}}}{1+\exp \left(-\frac{V_{i d}}{V_{T}}\right)}  \tag{3.147}\\
& I_{c 2}=\frac{\alpha_{F} I_{\mathrm{TAIL}}}{1+\exp \left(\frac{V_{i d}}{V_{T}}\right)} \tag{3.148}
\end{align*}
$$

These two currents are shown as a function of $V_{i d}$ in Fig. 3.46. When the magnitude of $V_{i d}$ is greater than about $3 V_{T}$, which is approximately 78 mV at room temperature, the collector currents are almost independent of $V_{i d}$ because one of the transistors turns off and the other conducts all the current that flows. Furthermore, the circuit behaves in an approximately
image_name:Figure 3.46 Emitter-coupled pair collector currents as a function of differential input voltage
description:The graph in Figure 3.46 is a plot of the collector currents \(I_{c1}\) and \(I_{c2}\) of an emitter-coupled pair as a function of the differential input voltage \(V_{id}\). The graph is a typical representation of how these currents behave over a range of input voltages, specifically for a differential pair of transistors.

Axes Labels and Units:
- **X-axis:** Represents the differential input voltage \(V_{id}\), marked at intervals of \(-4V_T, -3V_T, -2V_T, -V_T, 0, V_T, 2V_T, 3V_T, 4V_T\). \(V_T\) is the thermal voltage, approximately 26 mV at room temperature.
- **Y-axis:** Represents the collector currents \(I_{c1}\) and \(I_{c2}\) as a function of \(V_{id}\). The units are not explicitly given but are typically in amperes.

Overall Behavior and Trends:
- The graph shows two curves, \(I_{c1}\) and \(I_{c2}\), which are symmetric and intersect at \(V_{id} = 0\).
- As \(V_{id}\) increases from \(-4V_T\) to \(4V_T\), \(I_{c1}\) increases from \(0\) to \(\alpha_F I_{\text{TAIL}}\), while \(I_{c2}\) decreases from \(\alpha_F I_{\text{TAIL}}\) to \(0\).
- The opposite trend is observed as \(V_{id}\) decreases from \(0\) to \(-4V_T\), where \(I_{c1}\) decreases and \(I_{c2}\) increases.

Key Features and Technical Details:
- At \(V_{id} = 0\), both currents are equal to \(0.5 \alpha_F I_{\text{TAIL}}\), indicating balanced operation.
- When \(|V_{id}| > 3V_T\), one of the transistors turns off, and the other conducts almost all the current, making the currents nearly independent of \(V_{id}\).
- The plot shows a linear region around \(V_{id} = 0\), where the circuit behaves approximately linearly.

Annotations and Specific Data Points:
- The graph is annotated with the values \(0.5 \alpha_F I_{\text{TAIL}}\) at \(V_{id} = 0\) and \(\alpha_F I_{\text{TAIL}}\) as the maximum current for \(I_{c1}\) and \(I_{c2}\). This indicates the saturation level of the collector currents in the differential pair configuration.

Figure 3.46 Emitter-coupled pair collector currents as a function of differential input voltage.
image_name:Figure 3.47
description:The graph in Figure 3.47 depicts the differential output voltage \( V_{od} \) as a function of the differential input voltage \( V_{id} \) for an emitter-coupled pair. This is a typical S-shaped curve representing the behavior of the differential output voltage.

Axes Labels and Units:
- **Horizontal Axis (X-axis):** Represents the differential input voltage \( V_{id} \), marked in units of \( V_T \) (thermal voltage). The axis spans from \(-4V_T\) to \(4V_T\).
- **Vertical Axis (Y-axis):** Represents the differential output voltage \( V_{od} \), with significant markers at \( \alpha_F I_{\text{TAIL}} R_C \) and \(-\alpha_F I_{\text{TAIL}} R_C \).

Overall Behavior and Trends:
- The graph exhibits a nonlinear S-shaped curve.
- For small values of \( V_{id} \) (within the range of approximately \(-V_T\) to \(V_T\)), the curve is nearly linear, indicating a linear region where the circuit behaves approximately linearly.
- As \( V_{id} \) increases or decreases beyond this linear region, the curve saturates, approaching constant values \( \alpha_F I_{\text{TAIL}} R_C \) and \(-\alpha_F I_{\text{TAIL}} R_C \).

Key Features and Technical Details:
- **Linear Region:** Around \( V_{id} = 0 \), the curve is approximately linear, which is crucial for small-signal analysis.
- **Saturation Levels:** The maximum and minimum output voltages are \( \alpha_F I_{\text{TAIL}} R_C \) and \(-\alpha_F I_{\text{TAIL}} R_C \), respectively, indicating the saturation levels of the output.
- **Symmetry:** The curve is symmetric around the origin, reflecting the balanced nature of the differential pair.

Annotations and Specific Data Points:
- The graph is annotated with horizontal dashed lines at \( \alpha_F I_{\text{TAIL}} R_C \) and \(-\alpha_F I_{\text{TAIL}} R_C \), marking the saturation levels of the output voltage.
- The transition from linear to saturation is smooth, highlighting the gradual change in behavior as \( V_{id} \) moves away from zero.

Figure 3.47 Emitter-coupled pair, differential output voltage as a function of differential input voltage.
linear fashion only when the magnitude of $V_{i d}$ is less than about $V_{T}$. We can now compute the output voltages as

$$
\begin{align*}
& V_{o 1}=V_{C C}-I_{c 1} R_{C}  \tag{3.149}\\
& V_{o 2}=V_{C C}-I_{c 2} R_{C} \tag{3.150}
\end{align*}
$$

The output signal of interest is often the difference between $V_{o 1}$ and $V_{o 2}$, which we define as $V_{o d}$. Then

$$
\begin{equation*}
V_{o d}=V_{o 1}-V_{o 2}=\alpha_{F} I_{\mathrm{TAIL}} R_{C} \tanh \left(\frac{-V_{i d}}{2 V_{T}}\right) \tag{3.151}
\end{equation*}
$$

This function is plotted in Fig. 3.47. Here a significant advantage of differential amplifiers is apparent: When $V_{i d}$ is zero, $V_{o d}$ is zero if $Q_{1}$ and $Q_{2}$ are identical and if identical resistors are connected to the collectors of $Q_{1}$ and $Q_{2}$. This property allows direct coupling of cascaded stages without offsets.

### 3.5.2 The dc Transfer Characteristic with Emitter Degeneration

To increase the range of $V_{i d}$ over which the emitter-coupled pair behaves approximately as a linear amplifier, emitter-degeneration resistors are frequently included in series with the emitters of the transistors, as shown in Fig. 3.48. The analysis of this circuit proceeds in the same manner as without degeneration, except that the voltage drop across these resistors must be included in the KVL equation corresponding to (3.142). A transcendental equation results from this analysis and a closed-form solution like that of (3.151) does not exist, but the effect of the resistors may be understood intuitively from the examples plotted in Fig. 3.49. For large values of emitter-degeneration resistors, the linear range of operation is extended by an amount approximately equal to $I_{\text {TAIL }} R_{E}$. This result stems from the observation that all of $I_{\text {TAIL }}$ flows in one of the degeneration resistors when one transistor turns off. Therefore, the voltage drop is $I_{\mathrm{TAIL}} R_{E}$ on one resistor and zero on the other, and the value of $V_{i d}$ required to turn one transistor off is changed by the difference of the voltage drops on these resistors. Furthermore, since the voltage gain is the slope of the transfer characteristic, the voltage gain is reduced by approximately the same factor that the input range is increased. In operation, the emitter resistors introduce local negative feedback in the differential pair. This topic is considered in Chapter 8.
image_name:Figure 3.48 Circuit diagram of emitter-coupled pair with emitter degeneration
description:
[
name: Q1, type: NPN, ports: {C: Vodn, B: Vid/2, E: e1}
name: Q2, type: NPN, ports: {C: Vodp, B: -Vid/2, E: e2}
name: RC, type: Resistor, value: RC, ports: {N1: Vodn, N2: VCC}
name: RC, type: Resistor, value: RC, ports: {N1: Vodp, N2: VCC}
name: RE, type: Resistor, value: RE, ports: {N1: e1, N2: p}
name: RE, type: Resistor, value: RE, ports: {N1: e2, N2: p}
name: ITAIL, type: CurrentSource, value: ITAIL, ports: {Np: p, Nn: VEE}
]
extrainfo:The circuit is an emitter-coupled pair with emitter degeneration, used for differential amplification. It introduces local negative feedback through the emitter resistors RE, which stabilizes the gain and increases linearity.

Figure 3.48 Circuit diagram of emitter-coupled pair with emitter degeneration.
image_name:Figure 3.49 Output voltage as a function of input voltage, emitter-coupled pair with emitter degeneration.
description:The graph in Figure 3.49 is a plot of the output differential voltage \( V_{od} \) as a function of the input differential voltage \( V_{id} \) for an emitter-coupled pair with emitter degeneration. The graph is a DC transfer characteristic curve, illustrating how the output voltage changes in response to varying input voltage.

**Axes Labels and Units:**
- The horizontal axis represents the input differential voltage \( V_{id} \), with marked values at \(-20V_T\), \(-10V_T\), \(0\), \(10V_T\), and \(20V_T\).
- The vertical axis represents the output differential voltage \( V_{od} \), with dashed lines indicating the saturation levels at \( \alpha F I_{TAIL} R_C \) and \( -\alpha F I_{TAIL} R_C \).

**Overall Behavior and Trends:**
- The graph shows three curves corresponding to different values of \( I_{TAIL} R_E \): 0, \(10V_T\), and \(20V_T\).
- For \( I_{TAIL} R_E = 0 \), the curve is more linear and has a steeper slope around \( V_{id} = 0 \), indicating higher gain.
- As \( I_{TAIL} R_E \) increases, the curves become more rounded, showing reduced gain and increased linearity due to the negative feedback introduced by the emitter degeneration.
- All curves saturate at the same levels, \( \alpha F I_{TAIL} R_C \) and \( -\alpha F I_{TAIL} R_C \).

**Key Features and Technical Details:**
- The central region of the curves (around \( V_{id} = 0 \)) shows a linear relationship, which becomes less steep with increasing \( I_{TAIL} R_E \), indicating the effect of emitter degeneration in stabilizing the gain.
- The saturation levels are symmetric about the origin, reflecting the balanced nature of the differential pair.

**Annotations and Specific Data Points:**
- The graph includes annotations for the values of \( I_{TAIL} R_E \), clearly indicating how the emitter degeneration affects the transfer characteristic.
- The curves are labeled with arrows showing the direction of increasing \( I_{TAIL} R_E \).

Figure 3.49 Output voltage as a function of input voltage, emitter-coupled pair with emitter degeneration.

### 3.5.3 The dc Transfer Characteristic of a Source-Coupled Pair

Consider the $n$-channel MOS-transistor source-coupled pair shown in Fig. 3.50. The following analysis applies equally well to a corresponding $p$-channel source-coupled pair with appropriate sign changes. In monolithic form, a transistor current source, called a tail current source, is usually connected to the sources of $M_{1}$ and $M_{2}$. In that case, $I_{\text {TAIL }}$ and $R_{\text {TAIL }}$ together form a Norton-equivalent model of the tail current source.

For this large-signal analysis, we assume that the output resistance of the tail current source is $R_{\text {TAIL }} \rightarrow \infty$. Also, we assume that the output resistance of each transistor $r_{o} \rightarrow \infty$. Although these assumptions do not strongly affect the low-frequency, large-signal behavior of the circuit, they could have a significant impact on the small-signal behavior. Therefore, we will reconsider these assumptions when we analyze the circuit from a small-signal standpoint. From KVL around the input loop,

$$
\begin{equation*}
V_{i 1}-V_{g s 1}+V_{g s 2}-V_{i 2}=0 \tag{3.152}
\end{equation*}
$$

We assume that the drain resistors are small enough that neither transistor operates in the triode region if $V_{i 1} \leq V_{D D}$ and $V_{i 2} \leq V_{D D}$. Furthermore, we assume that the drain current of each
image_name:Figure 3.50 n-channel MOSFET source-coupled pair
description:
[
name: Vi1, type: VoltageSource, value: Vi1, ports: {Np: Vi1, Nn: GND}
name: Vi2, type: VoltageSource, value: Vi2, ports: {Np: Vi2, Nn: GND}
name: M1, type: NMOS, ports: {S: P, D: Vo1, G: Vi1}
name: M2, type: NMOS, ports: {S: P, D: Vo2, G: Vi2}
name: RD, type: Resistor, value: RD, ports: {N1: Vo1, N2: VDD}
name: RD, type: Resistor, value: RD, ports: {N1: Vo2, N2: VDD}
name: RTAIL, type: Resistor, value: RTAIL, ports: {N1: P, N2: -VSS}
name: ITAIL, type: CurrentSource, value: ITAIL, ports: {Np: P, Nn: -VSS}
]
extrainfo:The circuit is a differential amplifier using a source-coupled pair of NMOS transistors (M1 and M2). The drains of M1 and M2 are connected to VDD through resistors RD, and the sources are connected together at node P, which is connected to a current source ITAIL and a resistor RTAIL connected to VSS.

Figure $3.50 n$-channel MOSFET source-coupled pair.
transistor is related to its gate-source voltage by the approximate square-law relationship given in (1.157). If the transistors are identical, applying (1.157) to each transistor and rearranging gives

$$
\begin{equation*}
V_{g s 1}=V_{t}+\sqrt{\frac{2 I_{d 1}}{k^{\prime}(W / L)}} \tag{3.153}
\end{equation*}
$$

and

$$
\begin{equation*}
V_{g s 2}=V_{t}+\sqrt{\frac{2 I_{d 2}}{k^{\prime}(W / L)}} \tag{3.154}
\end{equation*}
$$

Substituting (3.153) and (3.154) into (3.152) and rearranging gives

$$
\begin{equation*}
V_{i d}=V_{i 1}-V_{i 2}=\frac{\sqrt{I_{d 1}}-\sqrt{I_{d 2}}}{\sqrt{\frac{k^{\prime}}{2} \frac{W}{L}}} \tag{3.155}
\end{equation*}
$$

From KCL at the source of $M_{1}$ and $M_{2}$,

$$
\begin{equation*}
I_{d 1}+I_{d 2}=I_{\mathrm{TAIL}} \tag{3.156}
\end{equation*}
$$

Solving (3.156) for $I_{d 2}$, substituting into (3.155), rearranging, and using the quadratic formula gives

$$
\begin{equation*}
I_{d 1}=\frac{I_{\mathrm{TAIL}}}{2} \pm \frac{k^{\prime}}{4} \frac{W}{L} V_{i d} \sqrt{\frac{4 I_{\mathrm{TAIL}}}{k^{\prime}(W / L)}-V_{i d}^{2}} \tag{3.157}
\end{equation*}
$$

Since $I_{d 1}>I_{\text {TAIL }} / 2$ when $V_{i d}>0$, the potential solution where the second term is subtracted from the first in (3.157) cannot occur in practice. Therefore,

$$
\begin{equation*}
I_{d 1}=\frac{I_{\mathrm{TAIL}}}{2}+\frac{k^{\prime}}{4} \frac{W}{L} V_{i d} \sqrt{\frac{4 I_{\mathrm{TAIL}}}{k^{\prime}(W / L)}-V_{i d}^{2}} \tag{3.158}
\end{equation*}
$$

Substituting (3.158) into (3.156) gives

$$
\begin{equation*}
I_{d 2}=\frac{I_{\mathrm{TAIL}}}{2}-\frac{k^{\prime}}{4} \frac{W}{L} V_{i d} \sqrt{\frac{4 I_{\mathrm{TAIL}}}{k^{\prime}(W / L)}-V_{i d}^{2}} \tag{3.159}
\end{equation*}
$$

Equations 3.158 and 3.159 are valid when both transistors operate in the active or saturation region. Since we have assumed that neither transistor operates in the triode region, the limitation here stems from turning off one of the transistors. When $M_{1}$ turns off, $I_{d 1}=0$ and $I_{d 2}=I_{\text {TAIL }}$. On the other hand, $I_{d 1}=I_{\text {TAIL }}$ and $I_{d 2}=0$ when $M_{2}$ turns off. Substituting these values in (3.155) shows that both transistors operate in the active region if

$$
\begin{equation*}
\left|V_{i d}\right| \leq \sqrt{\frac{2 I_{\mathrm{TAIL}}}{k^{\prime}(W / L)}} \tag{3.160}
\end{equation*}
$$

Since $I_{d 1}=I_{d 2}=I_{\text {TAIL }} / 2$ when $V_{i d}=0$, the range in (3.160) can be rewritten as

$$
\begin{equation*}
\left|V_{i d}\right| \leq\left.\sqrt{2}\left(\sqrt{\frac{2 I_{d 1}}{k^{\prime}(W / L)}}\right)\right|_{V_{i d}=0}=\left.\sqrt{2}\left(V_{o v}\right)\right|_{V_{i d}=0} \tag{3.161}
\end{equation*}
$$

Equation 3.161 shows that the range of $V_{i d}$ for which both transistors operate in the active region is proportional to the overdrive calculated when $V_{i d}=0$. This result is illustrated in Fig. 3.51. The overdrive is an important quantity in MOS circuit design, affecting not only the input range of differential pairs, but also other characteristics including the speed, offset, and output swing of MOS amplifiers. Since the overdrive of an MOS transistor depends on its current and $W / L$ ratio, the range of a source-coupled pair can be adjusted to suit a given application by adjusting the value of the tail current and/or the aspect ratio of the input devices. In contrast, the input range of the bipolar emitter-coupled pair is about $\pm 3 V_{T}$, independent of bias current or device size. In fact, the source-coupled pair behaves somewhat like an emittercoupled pair with emitter-degeneration resistors that can be selected to give a desired input voltage range.
image_name:Figure 3.51 dc transfer characteristic of the MOS source-coupled pair
description:The graph in Figure 3.51 illustrates the DC transfer characteristic of a MOS source-coupled pair. It is a plot that shows the relationship between the differential input voltage \(V_{id}\) on the horizontal axis and the drain currents \(I_{d1}\) and \(I_{d2}\) on the vertical axis. The graph is plotted with \(V_{id}\) in volts ranging from -0.5 V to 0.5 V, and the drain currents \(I_{d1}\) and \(I_{d2}\) are shown as a function of \(I_{TAIL}\), the tail current, which is split equally when \(V_{id} = 0\) such that \(I_{d1} = I_{d2} = I_{TAIL}/2\).

The graph has multiple curves corresponding to different values of the overdrive voltage \(V_{ov} = V_{GS} - V_t\), specifically \(V_{ov} = 0.1 V\), \(0.2 V\), and \(0.4 V\). These curves illustrate how the transfer characteristic varies with different overdrive voltages.

### Overall Behavior and Trends:
- As \(V_{id}\) increases from negative to positive values, \(I_{d1}\) increases from \(I_{TAIL}/2\) toward \(I_{TAIL}\), while \(I_{d2}\) decreases from \(I_{TAIL}/2\) toward zero.
- Conversely, as \(V_{id}\) decreases, \(I_{d1}\) decreases toward zero, and \(I_{d2}\) increases toward \(I_{TAIL}\).
- The curves become sharper and more pronounced as \(V_{ov}\) increases, indicating a stronger response of the drain currents to changes in \(V_{id}\).

Key Features:
- The center point where \(V_{id} = 0\) corresponds to \(I_{d1} = I_{d2} = I_{TAIL}/2\), which is a point of symmetry in the graph.
- For each \(V_{ov}\), the curves diverge from this central point, showing how \(I_{d1}\) and \(I_{d2}\) split as \(V_{id}\) moves away from zero.
- The graph highlights the effect of the overdrive voltage on the MOS source-coupled pair's transfer characteristic, demonstrating increased sensitivity with higher \(V_{ov}\) values.

Overall, this graph provides insight into the behavior of a MOS source-coupled pair in terms of its drain currents as a function of differential input voltage and varying overdrive voltages.

Figure 3.51 dc transfer characteristic of the MOS source-coupled pair. The parameter is the overdrive $V_{o v}=V_{G S}-V_{t}$ determined when $V_{i d}=0$.

In many practical cases, the key output of the differential pair is not $I_{d 1}$ or $I_{d 2}$ alone but the difference between these quantities. Subtracting (3.159) from (3.158) gives

$$
\begin{equation*}
\Delta I_{d}=I_{d 1}-I_{d 2}=\frac{k^{\prime}}{2} \frac{W}{L} V_{i d} \sqrt{\frac{4 I_{\mathrm{TAIL}}}{k^{\prime}(W / L)}-V_{i d}^{2}} \tag{3.162}
\end{equation*}
$$

We can now compute the differential output voltage as

$$
\begin{equation*}
V_{o d}=V_{o 1}-V_{o 2}=V_{D D}-I_{d 1} R_{D}-V_{D D}+I_{d 2} R_{D}=-\left(\Delta I_{d}\right) R_{D} \tag{3.163}
\end{equation*}
$$

Since $\Delta I_{d}=0$ when $V_{i d}=0$, (3.163) shows that $V_{o d}=0$ when $V_{i d}=0$ if $M_{1}$ and $M_{2}$ are identical and if identical resistors are connected to the drains of $M_{1}$ and $M_{2}$. This property allows direct coupling of cascaded MOS differential pairs, as in the bipolar case.

### 3.5.4 Introduction to the Small-Signal Analysis of Differential Amplifiers

The features of interest in the performance of differential pairs are often the small-signal properties for dc differential input voltages near zero volts. In the next two sections, we assume that the dc differential input voltage is zero and calculate the small-signal parameters. If the parameters are constant, the small-signal model predicts that the circuit operation is linear. The results of the small-signal analysis are valid for signals that are small enough to cause insignificant nonlinearity.

In previous sections, we have considered amplifiers with two input terminals ( $V_{i}$ and ground) and two output terminals ( $V_{o}$ and ground). Small-signal analysis of such circuits leads to one equation for each circuit, such as

$$
\begin{equation*}
v_{o}=A v_{i} \tag{3.164}
\end{equation*}
$$

Here, $A$ is the small-signal voltage gain under given loading conditions. In contrast, differential pairs have three input terminals ( $V_{i 1}, V_{i 2}$, and ground) and three output terminals ( $V_{o 1}, V_{o 2}$, and ground). Therefore, direct small-signal analysis of differential pairs leads to two equations for each circuit (one for each output), where each output depends on each input:

$$
\begin{align*}
& v_{o 1}=A_{11} v_{i 1}+A_{12} v_{i 2}  \tag{3.165}\\
& v_{o 2}=A_{21} v_{i 1}+A_{22} v_{i 2} \tag{3.166}
\end{align*}
$$

Here, four voltage gains, $A_{11}, A_{12}, A_{21}$, and $A_{22}$, specify the small-signal operation of the circuit under given loading conditions. These gains can be interpreted as

$$
\begin{align*}
& A_{11}=\left.\frac{v_{o 1}}{v_{i 1}}\right|_{v_{i 2}=0}  \tag{3.167}\\
& A_{12}=\left.\frac{v_{o 1}}{v_{i 2}}\right|_{v_{i 1}=0}  \tag{3.168}\\
& A_{21}=\left.\frac{v_{o 2}}{v_{i 1}}\right|_{v_{i 2}=0}  \tag{3.169}\\
& A_{22}=\left.\frac{v_{o 2}}{v_{i 2}}\right|_{v_{i 1}=0} \tag{3.170}
\end{align*}
$$

Although direct small-signal analysis of differential pairs can be used to calculate these four gain values in a straightforward way, the results are difficult to interpret because differential
pairs usually are not used to react to $v_{i 1}$ or $v_{i 2}$ alone. Instead, differential pairs are used most often to sense the difference between the two inputs while trying to ignore the part of the two inputs that is common to each. Desired signals will be forced to appear as differences in differential circuits. In practice, undesired signals will also appear. For example, mixed-signal integrated circuits use both analog and digital signal processing, and the analog signals are vulnerable to corruption from noise generated by the digital circuits and transmitted through the common substrate. The hope in using differential circuits is that undesired signals will appear equally on both inputs and be rejected.

To highlight this behavior, we will define new differential and common-mode variables at the input and output as follows. The differential input, to which differential pairs are sensitive, is

$$
\begin{equation*}
v_{i d}=v_{i 1}-v_{i 2} \tag{3.171}
\end{equation*}
$$

The common-mode or average input, to which differential pairs are insensitive, is

$$
\begin{equation*}
v_{i c}=\frac{v_{i 1}+v_{i 2}}{2} \tag{3.172}
\end{equation*}
$$

These equations can be inverted to give $v_{i 1}$ and $v_{i 2}$ in terms of $v_{i d}$ and $v_{i c}$ :

$$
\begin{align*}
& v_{i 1}=v_{i c}+\frac{v_{i d}}{2}  \tag{3.173}\\
& v_{i 2}=v_{i c}-\frac{v_{i d}}{2} \tag{3.174}
\end{align*}
$$

The physical significance of these new variables can be understood by using (3.173) and (3.174) to redraw the input connections to a differential amplifier as shown in Fig. 3.52. The common-mode input is the input component that appears equally in $v_{i 1}$ and $v_{i 2}$. The differential input is the input component that appears between $v_{i 1}$ and $v_{i 2}$.

New output variables are defined in the same way. The differential output is

$$
\begin{equation*}
v_{o d}=v_{o 1}-v_{o 2} \tag{3.175}
\end{equation*}
$$

The common-mode or average output is

$$
\begin{equation*}
v_{o c}=\frac{v_{o 1}+v_{o 2}}{2} \tag{3.176}
\end{equation*}
$$

Solving these equations for $v_{o 1}$ and $v_{o 2}$, we obtain

$$
\begin{align*}
& v_{o 1}=v_{o c}+\frac{v_{o d}}{2}  \tag{3.177}\\
& v_{o 2}=v_{o c}-\frac{v_{o d}}{2} \tag{3.178}
\end{align*}
$$

image_name:(a)
description:
[
name: vi1, type: VoltageSource, value: vi1, ports: {Np: Vii, Nn: GND}
name: vi2, type: VoltageSource, value: vi2, ports: {Np: Viz, Nn: GND}
name: A, type: OpAmp, value: A, ports: {InP: Vii, InN: Viz, OutP: Out(A)}
]
extrainfo:The circuit diagram (a) represents a differential amplifier with two independent voltage inputs, vi1 and vi2, connected to an operational amplifier A. The output is labeled Out(A). The ground nodes are connected to the negative terminals of both voltage sources.
image_name:(b)
description:
[
name: vic, type: VoltageSource, value: vic, ports: {Np: Vic, Nn: GND}
name: vid/2, type: VoltageSource, value: vid/2, ports: {Np: InP(A), Nn: Vic}
name: -vid/2, type: VoltageSource, value: -vid/2, ports: {Np: Vic, Nn: InN(A)}
name: A, type: OpAmp, value: A, ports: {InP: InP(A), InN: InN(A), OutP: Out(A)}
]
extrainfo:The circuit diagram (b) represents a differential amplifier with inputs expressed in terms of differential (vid/2) and common-mode (vic) components. The circuit uses an op-amp to amplify the differential input.

We have now defined two new input variables and two new output variables. By substituting the expressions for $v_{i 1}, v_{i 2}, v_{o 1}$, and $v_{o 2}$ in terms of the new variables back into (3.165) and (3.166), we find

$$
\begin{gather*}
v_{o d}=\left(\frac{A_{11}-A_{12}-A_{21}+A_{22}}{2}\right) v_{i d}+\left(A_{11}+A_{12}-A_{21}-A_{22}\right) v_{i c}  \tag{3.179}\\
v_{o c}=\left(\frac{A_{11}-A_{12}+A_{21}-A_{22}}{4}\right) v_{i d}+\left(\frac{A_{11}+A_{12}+A_{21}+A_{22}}{2}\right) v_{i c} \tag{3.180}
\end{gather*}
$$

Defining four new gain factors that are equal to the coefficients in these equations, (3.179) and (3.180) can be rewritten as

$$
\begin{align*}
& v_{o d}=A_{d m} v_{i d}+A_{c m-d m} v_{i c}  \tag{3.181}\\
& v_{o c}=A_{d m-c m} v_{i d}+A_{c m} v_{i c} \tag{3.182}
\end{align*}
$$

The differential-mode gain $A_{d m}$ is the change in the differential output per unit change in differential input:

$$
\begin{equation*}
A_{d m}=\left.\frac{v_{o d}}{v_{i d}}\right|_{v_{i c}=0}=\frac{A_{11}-A_{12}-A_{21}+A_{22}}{2} \tag{3.183}
\end{equation*}
$$

The common-mode gain $A_{c m}$ is the change in the common-mode output voltage per unit change in the common-mode input:

$$
\begin{equation*}
A_{c m}=\left.\frac{v_{o c}}{v_{i c}}\right|_{v_{i d}=0}=\frac{A_{11}+A_{12}+A_{21}+A_{22}}{2} \tag{3.184}
\end{equation*}
$$

The differential-mode-to-common-mode gain $A_{d m-c m}$ is the change in the common-mode output voltage per unit change in the differential-mode input:

$$
\begin{equation*}
A_{d m-c m}=\left.\frac{v_{o c}}{v_{i d}}\right|_{v_{i c}=0}=\frac{A_{11}-A_{12}+A_{21}-A_{22}}{4} \tag{3.185}
\end{equation*}
$$

The common-mode-to-differential-mode gain $A_{c m-d m}$ is the change in the differential-mode output voltage per unit change in the common-mode input:

$$
\begin{equation*}
A_{c m-d m}=\left.\frac{v_{o d}}{v_{i c}}\right|_{v_{i d}=0}=A_{11}+A_{12}-A_{21}-A_{22} \tag{3.186}
\end{equation*}
$$

The purpose of a differential amplifier is to sense changes in its differential input while rejecting changes in its common-mode input. The desired output is differential, and its variation should be proportional to the variation in the differential input. Variation in the common-mode output is undesired because it must be rejected by another differential stage to sense the desired differential signal. Therefore, an important design goal in differential amplifiers is to make $A_{d m}$ large compared to the other three gain coefficients in (3.181) and (3.182).

In differential amplifiers with perfect symmetry, each component on the side of one output corresponds to an identical component on the side of the other output. With such perfectly balanced amplifiers, when $v_{i 1}=-v_{i 2}, v_{o 1}=-v_{o 2}$. In other words, when the input is purely differential $\left(v_{i c}=0\right)$, the output of a perfectly balanced differential amplifier is purely differential ( $v_{o c}=0$ ), and thus $A_{d m-c m}=0$. Similarly, pure common-mode inputs (for which $v_{i d}=0$ ) produce pure common-mode outputs and $A_{c m-d m}=0$ in perfectly balanced differential amplifiers. Even with perfect symmetry, however, $A_{c m} \neq 0$ is possible. Therefore, the ratio $A_{d m} / A_{c m}$ is one figure of merit for a differential amplifier, giving the ratio of the desired
differential-mode gain to the undesired common-mode gain. In this book, we will define the magnitude of this ratio as the common-mode-rejection ratio, CMRR:

$$
\begin{equation*}
\mathrm{CMRR} \equiv\left|\frac{A_{d m}}{A_{c m}}\right| \tag{3.187}
\end{equation*}
$$

Furthermore, since differential amplifiers are not perfectly balanced in practice, $A_{d m-c m} \neq 0$ and $A_{c m-d m} \neq 0$. The ratios $A_{d m} / A_{c m-d m}$ and $A_{d m} / A_{d m-c m}$ are two other figures of merit that characterize the performance of differential amplifiers. Of these, the first is particularly important because ratio $A_{d m} / A_{c m-d m}$ determines the extent to which the differential output is produced by the desired differential input instead of by the undesired common-mode input. This ratio is important because once a common-mode input is converted to a differential output, the result is treated as the desired signal by subsequent differential amplifiers. In fact, in multistage differential amplifiers, the common-mode-to-differential-mode gain of the first stage is usually an important factor in the overall CMRR. In Section 3.5.5, we consider perfectly balanced differential amplifiers from a small-signal standpoint; in Section 3.5.6.9, imperfectly balanced differential amplifiers from the same standpoint.

### 3.5.5 Small-Signal Characteristics of Balanced Differential Amplifiers

In this section, we will study perfectly balanced differential amplifiers. Therefore, $A_{c m-d m}=0$ and $A_{d m-c m}=0$ here, and our goal is to calculate $A_{d m}$ and $A_{c m}$. Although calculating $A_{d m}$ and $A_{c m}$ from the entire small-signal equivalent circuit of a differential amplifier is possible, these calculations are greatly simplified by taking advantage of the symmetry that exists in perfectly balanced amplifiers. In general, we first find the response of a given circuit to pure differential and pure common-mode inputs separately. Then the results can be superposed to find the total solution. Since superposition is valid only for linear circuits, the following analysis is strictly valid only from a small-signal standpoint and approximately valid only for signals that cause negligible nonlinearity. In previous sections, we carried out large-signal analyses of differential pairs and assumed that the Norton-equivalent resistance of the tail current source was infinite. Since this resistance has a considerable effect on the small-signal behavior of differential pairs, however, we now assume that this resistance is finite.

Because the analysis here is virtually the same for both bipolar and MOS differential pairs, the two cases will be considered together. Consider the bipolar emitter-coupled pair of Fig. 3.45 and the MOS source-coupled pair of Fig. 3.50 from a small-signal standpoint. Then $V_{i 1}=v_{i 1}$ and $V_{i 2}=v_{i 2}$. These circuits are redrawn in Fig. $3.53 a$ and Fig. $3.53 b$ with the common-mode input voltages set to zero so we can consider the effect of the differential-mode input by itself. The small-signal equivalent circuit for both cases is shown in Fig. 3.54 with $R$ used to replace $R_{C}$ in Fig. $3.53 a$ and $R_{D}$ in $3.53 b$. Note that the small-signal equivalent circuit neglects finite $r_{o}$ in both cases. Also, in the MOS case, nonzero $g_{m b}$ is ignored and $r_{\pi} \rightarrow \infty$ because $\beta_{0} \rightarrow \infty$.

Because the circuit in Fig. 3.54 is perfectly balanced, and because the inputs are driven by equal and opposite voltages, the voltage across $R_{\text {TAIL }}$ does not vary at all. Another way to see this result is to view the two lower parts of the circuit as voltage followers. When one side pulls up, the other side pulls down, resulting in a constant voltage across the tail current source by superposition. Since the voltage across $R_{\text {TAIL }}$ experiences no variation, the behavior of the small-signal circuit is unaffected by the placement of a short circuit across $R_{\text {TAIL }}$, as shown in Fig. 3.55. After placing this short circuit, we see that the two sides of the circuit are not only identical, but also independent because they are joined at a node that operates as a small-signal ground. Therefore, the response to small-signal differential inputs can be determined by analyzing one side of the original circuit with $R_{\text {TAIL }}$ replaced by a short circuit.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: Vodp, B: Vid/2, E: P}
name: Q2, type: NPN, ports: {C: Vodn, B: -Vid/2, E: P}
name: RC, type: Resistor, value: RC, ports: {N1: +VCC, N2: Vodp}
name: RC, type: Resistor, value: RC, ports: {N1: +VCC, N2: Vodn}
name: RTAIL, type: Resistor, value: RTAIL, ports: {N1: P, N2: -VEE}
name: ITAIL, type: CurrentSource, value: ITAIL, ports: {Np: P, Nn: -VEE}
name: +VCC, type: VoltageSource, value: +VCC, ports: {Np: +VCC, Nn: GND}
name: M1, type: NMOS, ports: {S: P, D: +VDD, G: Vid/2}
name: M2, type: NMOS, ports: {S: P, D: +VDD, G: -Vid/2}
name: +VDD, type: VoltageSource, value: +VDD, ports: {Np: +VDD, Nn: GND}
name: RTAIL, type: Resistor, value: RTAIL, ports: {N1: P, N2: -VSS}
name: ITAIL, type: CurrentSource, value: ITAIL, ports: {Np: P, Nn: -VSS}
]
extrainfo:The circuit diagram (a) is an emitter-coupled pair with a differential input, using NPN transistors Q1 and Q2. The differential input is applied across the bases of Q1 and Q2, while the emitters are connected together and to a current source ITAIL through RTAIL. The collectors are connected to the power supply +VCC through resistors RC. The output voltages are taken from the collectors of Q1 and Q2.

The circuit diagram (b) is a source-coupled pair with a differential input, using NMOS transistors M1 and M2. The differential input is applied across the gates of M1 and M2, while the sources are connected together and to a current source ITAIL through RTAIL. The drains are connected to the power supply +VDD through resistors RD. The output voltages are taken from the drains of M1 and M2.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: P, D: Vodp, G: Vid/2}
name: M2, type: NMOS, ports: {S: P, D: Vodn, G: -Vid/2}
name: RD, type: Resistor, value: RD, ports: {N1: Vodp, N2: VDD}
name: RD, type: Resistor, value: RD, ports: {N1: Vodn, N2: VDD}
name: RTAIL, type: Resistor, value: RTAIL, ports: {N1: P, N2: -VSS}
name: ITAIL, type: CurrentSource, value: ITAIL, ports: {Np: P, Nn: -VSS}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: VSS, type: VoltageSource, value: VSS, ports: {Np: GND, Nn: VSS}
name: Vid, type: VoltageSource, value: Vid, ports: {Np: Vid/2, Nn: GND}
name: Vid, type: VoltageSource, value: Vid, ports: {Np: -Vid/2, Nn: GND}
]
extrainfo:The circuit is a source-coupled differential pair with NMOS transistors. It operates with differential input voltages and produces differential output voltages. The current source I_TAIL and resistor R_TAIL provide biasing. The circuit is powered by VDD and VSS.

Figure 3.53 (a) Emitter-coupled pair with pure differential input. (b) Source-coupled pair with pure differential input.
image_name:Figure 3.54
description:
[
name: Vid/2, type: VoltageSource, ports: {Np: Vid/2, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vid/2, N2: P}
name: R, type: Resistor, value: R, ports: {N1: P, N2: Vod/2}
name: gmv1, type: CurrentSource, ports: {Np: P, Nn: GND}
name: gmv2, type: CurrentSource, ports: {Np: P, Nn: GND}
name: RTail, type: Resistor, value: RTail, ports: {N1: P, N2: GND}
]
extrainfo:The circuit is a small-signal equivalent of a differential pair with pure differential-mode input. It includes voltage sources Vid/2 and -Vid/2, resistors rπ and R, and current sources gmv1 and gmv2. The tail resistor RTail provides biasing, and the circuit is grounded at multiple points.

Figure 3.54 Small-signal equivalent circuit for differential pair with pure differential-mode input.
image_name:Figure 3.55 Differential-mode circuit with the tail current source grounded
description:
[
name: Vid/2, type: VoltageSource, value: Vid/2, ports: {Np: Vid/2, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vid/2, N2: v1}
name: R, type: Resistor, value: R, ports: {N1: x1, N2: GND}
name: gmv1, type: CurrentSource, value: gmv1, ports: {Np: x1, Nn: P}
name: R, type: Resistor, value: R, ports: {N1: x2, N2: GND}
name: gmv2, type: CurrentSource, value: gmv2, ports: {Np: x2, Nn: P}
name: RTAIL, type: Resistor, value: RTAIL, ports: {N1: P, N2: GND}
name: -Vid/2, type: VoltageSource, value: -Vid/2, ports: {Np: -Vid/2, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: -Vid/2, N2: v2}
]
extrainfo:The circuit is a differential-mode circuit with symmetrical current sources and resistors, grounded at multiple points. The tail resistor RTAIL provides biasing, and the current ix is zero due to symmetry.

Figure 3.55 Differential-mode circuit with the tail current source grounded. Because of the symmetry of the circuit, $i_{x}=0$.
image_name:Figure 3.56
description:
[
name: vid/2, type: VoltageSource, value: vid/2, ports: {Np: vid/2, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: vid/2, N2: GND}
name: gmv1, type: CurrentSource, value: gmv1, ports: {Np: vid/2, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: vid/2, N2: vod/2}
name: vod/2, type: VoltageSource, value: vod/2, ports: {Np: vod/2, Nn: GND}
]
extrainfo:The circuit is a differential-mode half circuit. It is used for analyzing the low- and high-frequency performance of differential amplifiers. The symmetry of the circuit results in a zero current ix.

This simplified circuit, shown in Fig. 3.56, is called the differential-mode half circuit and is useful for analysis of both the low- and high-frequency performance of all types of differential amplifiers. By inspection of Fig. 3.56, we recognize this circuit as the small-signal equivalent of a common-emitter or common-source amplifier. Therefore,

$$
\begin{equation*}
\frac{v_{o d}}{2}=-g_{m} R \frac{v_{i d}}{2} \tag{3.188}
\end{equation*}
$$

and

$$
\begin{equation*}
A_{d m}=\left.\frac{v_{o d}}{v_{i d}}\right|_{v_{i c}=0}=-g_{m} R \tag{3.189}
\end{equation*}
$$

To include the output resistance of the transistor in the above analysis, $R$ in (3.189) should be replaced by $R \| r_{0}$. Finally, note that neglecting $g_{m b}$ from this analysis for MOS sourcecoupled pairs has no effect on the result because the voltage from the source to the body of the input transistors is the same as the voltage across the tail current source, which is constant with a pure differential input.

The circuits in Fig. 3.45 and Fig. 3.50 are now reconsidered from a small-signal, commonmode standpoint. Setting $V_{i 1}=V_{i 2}=v_{i c}$, the circuits are redrawn in Fig. 3.57a and Fig. 3.57b. The small-signal equivalent circuit is shown in Fig. 3.58, but with the modification that the resistor $R_{\text {TAIL }}$ has been split into two parallel resistors, each of value twice the original. Also $R$ has been used to replace $R_{C}$ in Fig. $3.57 a$ and $R_{D}$ in 3.57b. Again $r_{o}$ is neglected in both cases, and $g_{m b}$ is neglected in the MOS case, where $r_{\pi} \rightarrow \infty$ because $\beta_{0} \rightarrow \infty$.

Because the circuit in Fig. 3.58 is divided into two identical halves, and because each half is driven by the same voltage $v_{i c}$, no current $i_{x}$ flows in the lead connecting the half circuits. The circuit behavior is thus unchanged when this lead is removed as shown in Fig. 3.59. As a result, we see that the two halves of the circuit in Fig. 3.58 are not only identical, but also independent because they are joined by a branch that conducts no small-signal current. Therefore, the response to small-signal, common-mode inputs can be determined by analyzing
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: Voc, B: Vic, E: P}
name: Q2, type: NPN, ports: {C: Voc, B: Vic, E: P}
name: RC, type: Resistor, value: RC, ports: {N1: Vcc, N2: Voc}
name: RC, type: Resistor, value: RC, ports: {N1: Vcc, N2: Voc}
name: RTAIL, type: Resistor, value: RTAIL, ports: {N1: P, N2: -VEE}
name: ITAIL, type: CurrentSource, value: ITAIL, ports: {Np: P, Nn: -VEE}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: Vcc, Nn: GND}
]
extrainfo:The circuit is a differential pair with NPN transistors Q1 and Q2, biased by a current source ITAIL and resistor RTAIL. The output is taken across RC resistors connected to Vcc.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: P, D: Voc, G: Vic}
name: M2, type: NMOS, ports: {S: P, D: Voc, G: Vic}
name: RD, type: Resistor, value: RD, ports: {N1: Voc, N2: VDD}
name: RD, type: Resistor, value: RD, ports: {N1: Voc, N2: VDD}
name: ITAIL, type: CurrentSource, value: ITAIL, ports: {Np: P, Nn: -VSS}
name: RTAIL, type: Resistor, value: RTAIL, ports: {N1: P, N2: -VSS}
]
extrainfo:The circuit is a source-coupled pair with a pure common-mode input. It includes two NMOS transistors (M1 and M2) with their sources connected together at node P, which is connected to a current source ITAIL and resistor RTAIL. The drains of the NMOS transistors are connected to resistors RD leading to VDD. The gates of the transistors receive the common-mode input Vic.

Figure 3.57 (a) Emitter-coupled pair with pure common-mode input. (b) Source-coupled pair with pure common-mode input.
one half of the original circuit with an open circuit replacing the branch that joins the two halves of the original circuit. This simplified circuit, shown in Fig. 3.60, is called the commonmode half circuit. By inspection of Fig. 3.60, we recognize this circuit as a common-emitter or common-source amplifier with degeneration. Then

$$
\begin{equation*}
v_{o c}=-G_{m} R v_{i c} \tag{3.190}
\end{equation*}
$$

image_name:Figure 3.58 Smallsignal equivalent circuit, pure commonmode input.
description:
[
name: vic, type: VoltageSource, value: vic, ports: {Np: vic, Nn: GND}
name: rπ1, type: Resistor, value: rπ, ports: {N1: vic, N2: p1}
name: rπ2, type: Resistor, value: rπ, ports: {N1: vic, N2: p2}
name: R1, type: Resistor, value: R, ports: {N1: GND, N2: x1}
name: R2, type: Resistor, value: R, ports: {N1: GND, N2: x2}
name: 2RTAIL1, type: Resistor, value: 2RTAIL, ports: {N1: p1, N2: GND}
name: 2RTAIL2, type: Resistor, value: 2RTAIL, ports: {N1: p2, N2: GND}
name: gmv1, type: VoltageControlledCurrentSource, value: gmv1, ports: {Np: x1, Nn: p1}
name: gmv2, type: VoltageControlledCurrentSource, value: gmv2, ports: {Np: x2, Nn: p2}
]
extrainfo:The circuit is a small-signal equivalent with pure common-mode input, featuring a symmetrical structure. It includes two identical branches with resistors and voltage-controlled current sources.

Figure 3.58 Smallsignal equivalent circuit, pure commonmode input.

image_name:Figure 3.59 Modified common-mode equivalent circuit.
description:
[
name: Vic, type: VoltageSource, value: Vic, ports: {Np: Vic, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vic, N2: p1}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vic, N2: p2}
name: R, type: Resistor, value: R, ports: {N1: x1, N2: GND}
name: R, type: Resistor, value: R, ports: {N1: x2, N2: GND}
name: 2RTAIL, type: Resistor, value: 2RTAIL, ports: {N1: p1, N2: GND}
name: 2RTAIL, type: Resistor, value: 2RTAIL, ports: {N1: p2, N2: GND}
name: gmV1, type: VoltageControlledCurrentSource, ports: {Np: x1, Nn: p1}
name: gmV2, type: VoltageControlledCurrentSource, ports: {Np: x2, Nn: p2}
]
extrainfo:The circuit is a small-signal symmetrical structure with common-mode input. It features two identical branches, each with a resistor, a voltage-controlled current source, and a resistor connected to ground.

Figure 3.59 Modified common-mode equivalent circuit.

image_name:Figure 3.59 common-mode equivalent circuit
description:
[
name: Vic, type: VoltageSource, value: Vic, ports: {Np: Vic, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vic, N2: P}
name: 2RTail, type: Resistor, value: 2RTail, ports: {N1: P, N2: GND}
name: gmv1, type: CurrentSource, value: gmv1, ports: {Np: P, Nn: Voc}
name: R, type: Resistor, value: R, ports: {N1: Voc, N2: GND}
]
extrainfo:The circuit is a modified common-mode equivalent circuit with a symmetrical structure and common-mode input. It includes a voltage source (Vic), resistors (rπ and 2RTail), a voltage-controlled current source (gmv1), and a resistor (R) connected to ground. The circuit demonstrates common-mode signal processing with degeneration affecting the transconductance.

Figure 3.60 Common-mode half circuit.
and

$$
\begin{equation*}
A_{c m}=\left.\frac{v_{o c}}{v_{i c}}\right|_{v_{i d}=0}=-G_{m} R \tag{3.191}
\end{equation*}
$$

where $G_{m}$ is the transconductance of a common-emitter or common-source amplifier with degeneration and will be considered quantitatively below. Since degeneration reduces the transconductance, and since degeneration occurs only in the common-mode case, (3.189) and (3.191) show that $\left|A_{d m}\right|>\left|A_{c m}\right|$; therefore, the differential pair is more sensitive to differential inputs than to common-mode inputs. In other words, the tail current source provides local negative feedback to common-mode inputs (or local common-mode feedback). Negative feedback is studied in Chapter 8.

Bipolar Emitter-Coupled Pair. For the bipolar case, substituting (3.93) for $G_{m}$ with $R_{E}=$ $2 R_{\text {TAIL }}$ into (3.191) and rearranging gives

$$
\begin{equation*}
A_{c m} \simeq-\frac{g_{m} R}{1+g_{m}\left(2 R_{\mathrm{TAIL}}\right)}=-\frac{g_{m} R}{1+2 g_{m} R_{\mathrm{TAIL}}} \tag{3.192}
\end{equation*}
$$

To include the effect of finite $r_{o}$ in the above analysis, $R$ in (3.192) should be replaced by $R \| R_{o}$, where $R_{o}$ is the output resistance of a common-emitter amplifier with emitter degeneration of $R_{E}=2 R_{\text {TAIL }}$, given in (3.97) or (3.98). This substitution ignores the effect of finite $r_{o}$ on $G_{m}$, which is shown in (3.92) and is usually negligible.

The CMRR is found by substituting (3.189) and (3.192) into (3.187), which gives

$$
\begin{equation*}
\mathrm{CMRR}=1+2 g_{m} R_{\mathrm{TAIL}} \tag{3.193}
\end{equation*}
$$

This expression applies to the particular case of a single-stage, emitter-coupled pair. It shows that increasing the output resistance of the tail current source $R_{\text {TAIL }}$ improves the common-mode-rejection ratio. This topic is considered in Chapter 4.

Since bipolar transistors have finite $\beta_{0}$, and since differential amplifiers are often used as the input stage of instrumentation circuits, the input resistance of emitter-coupled pairs is also an important design consideration. The differential input resistance $R_{i d}$ is defined as the ratio of the small-signal differential input voltage $v_{i d}$ to the small-signal input current $i_{b}$ when a pure differential input voltage is applied. By inspecting Fig. 3.56, we find that

$$
\begin{equation*}
\frac{v_{i d}}{2}=i_{b} r_{\pi} \tag{3.194}
\end{equation*}
$$

Therefore, the differential input resistance of the emitter-coupled pair is

$$
\begin{equation*}
R_{i d}=\left.\frac{v_{i d}}{i_{b}}\right|_{v_{i c}=0}=2 r_{\pi} \tag{3.195}
\end{equation*}
$$

Thus the differential input resistance depends on the $r_{\pi}$ of the transistor, which increases with increasing $\beta_{0}$ and decreasing collector current. High input resistance is therefore obtained when an emitter-coupled pair is operated at low bias current levels. Techniques to achieve small bias currents are considered in Chapter 4.

The common-mode input resistance $R_{i c}$ is defined as the ratio of the small-signal, commonmode input voltage $v_{i c}$ to the small-signal input current $i_{b}$ in one terminal when a pure commonmode input is applied. Since the common-mode half circuit in Fig. 3.60 is the same as that for a common-emitter amplifier with emitter degeneration, substituting $R_{E}=2 R_{\text {TAIL }}$ into (3.90) gives $R_{i c}$ as

$$
\begin{equation*}
R_{i c}=\left.\frac{v_{i c}}{i_{b}}\right|_{v_{i d}=0}=r_{\pi}+\left(\beta_{0}+1\right)\left(2 R_{\mathrm{TAIL}}\right) \tag{3.196}
\end{equation*}
$$

The small-signal input current that flows when both common-mode and differential-mode input voltages are applied can be found by superposition and is given by

$$
\begin{align*}
& i_{b 1}=\frac{v_{i d}}{R_{i d}}+\frac{v_{i c}}{R_{i c}}  \tag{3.197}\\
& i_{b 2}=-\frac{v_{i d}}{R_{i d}}+\frac{v_{i c}}{R_{i c}} \tag{3.198}
\end{align*}
$$

where $i_{b 1}$ and $i_{b 2}$ represent the base currents of $Q_{1}$ and $Q_{2}$, respectively.
The input resistance can be represented by the $\pi$ equivalent circuit of Fig. $3.61 a$ or by the T-equivalent circuit of Fig. 3.61b. For the $\pi$ model, the common-mode input resistance is exactly $R_{i c}$ independent of $R_{x}$. To make the differential-mode input resistance exactly $R_{i d}$, the
image_name:(a)
description:
[
name: R_ic, type: Resistor, value: R_ic, ports: {N1: X1, N2: GND}
name: R_x, type: Resistor, value: R_id, ports: {N1: X1, N2: X2}
name: R_ic_2, type: Resistor, value: R_ic, ports: {N1: X2, N2: GND}
]
extrainfo:This is a low-frequency, small-signal, π-equivalent input circuit for a differential amplifier. The circuit shows the configuration of resistors R_ic and R_x (equivalent to R_id) in the input stage of the amplifier.
image_name:(b)
description:
[
name: R_id/2, type: Resistor, value: R_id/2, ports: {N1: X1, N2: X2}
name: R_ic, type: Resistor, value: R_ic, ports: {N1: X2, N2: GND}
name: R_id/2, type: Resistor, value: R_id/2, ports: {N1: X2, N2: LOAD}
]
extrainfo:This is a T-equivalent input circuit for a differential amplifier. The resistors are arranged to achieve specific input resistances. The common-mode input resistance is determined by R_ic, while the differential-mode input resistance is set by the configuration of R_id/2 resistors.

Figure 3.61 (a) General low-frequency, small-signal, $\pi$-equivalent input circuit for the differential amplifier. (b) T-equivalent input circuit.
value of $R_{x}$ should be more than $R_{i d}$ to account for nonzero current in $R_{i c}$. On the other hand, for the T model, the differential-mode input resistance is exactly $R_{i d}$ independent of $R_{y}$, and the common-mode input resistance is $R_{i c}$ if $R_{y}$ is chosen to be less than $R_{i c} / 2$ as shown. The approximations in Fig. 3.61 are valid if $R_{i c}$ is much larger than $R_{i d}$.

MOS Source-Coupled Pair. For the MOS case, substituting (3.104) for $G_{m}$ with $g_{m b}=0$ and $R_{S}=2 R_{\text {TAIL }}$ into (3.191) and rearranging gives

$$
\begin{equation*}
A_{c m} \simeq-\frac{g_{m} R}{1+g_{m}\left(2 R_{\mathrm{TAIL}}\right)}=-\frac{g_{m} R}{1+2 g_{m} R_{\mathrm{TAIL}}} \tag{3.199}
\end{equation*}
$$

Although (3.199) and the common-mode half circuit in Fig. 3.60 ignore the body-effect transconductance $g_{m b}$, the common-mode gain depends on $g_{m b}$ in practice because the body effect changes the source-body voltage of the transistors in the differential pair. Since nonzero $g_{m b}$ was included in the derivation of the transconductance of the common-source amplifier with degeneration, a simple way to include the body effect here is to allow nonzero $g_{m b}$ when substituting (3.104) into (3.191). The result is

$$
\begin{equation*}
A_{c m} \simeq-\frac{g_{m} R}{1+\left(g_{m}+g_{m b}\right)\left(2 R_{\mathrm{TAIL}}\right)}=-\frac{g_{m} R}{1+2\left(g_{m}+g_{m b}\right) R_{\mathrm{TAIL}}} \tag{3.200}
\end{equation*}
$$

To include the effect of finite $r_{o}$ in the above analysis, $R$ in (3.199) and (3.200) should be replaced by $R \| R_{o}$, where $R_{o}$ is the output resistance of a common-source amplifier with source degeneration of $R_{S}=2 R_{\text {TAIL }}$, given in (3.107). This substitution ignores the effect of finite $r_{o}$ on $G_{m}$, which is shown in (3.103) and is usually negligible.

The CMRR is found by substituting (3.189) and (3.200) into (3.187), which gives

$$
\begin{equation*}
\mathrm{CMRR} \simeq 1+2\left(g_{m}+g_{m b}\right) R_{\mathrm{TAIL}} \tag{3.201}
\end{equation*}
$$

Equation 3.201 is valid for a single-stage, source-coupled pair and shows that increasing $R_{\text {TAIL }}$ increases the CMRR. This topic is studied in Chapter 4.

### 3.5.6 Device Mismatch Effects in Differential Amplifiers

An important aspect of the performance of differential amplifiers is the minimum dc and ac differential voltages that can be detected. The presence of component mismatches within the amplifier itself and drifts of component values with temperature produce dc differential voltages at the output that are indistinguishable from the dc component of the signal being amplified. Also, such mismatches and drifts cause nonzero common-mode-to-differentialmode gain as well as nonzero differential-to-common-mode gain to arise. Nonzero $A_{c m-d m}$ is especially important because it converts common-mode inputs to differential outputs, which
image_name:(a)
description:
[
name: A, type: OpAmp, value: A, ports: {InP: VIDP, InN: VIDN, OutP: VODP, OutN: VODN}
]
extrainfo:The circuit is a differential amplifier with mismatches, which affects the differential and common-mode gains.

image_name:(b)
description:
[
name: V_OS, type: VoltageSource, value: V_OS, ports: {Np: X, Nn: InP(A)}
name: I_OS/2, type: CurrentSource, value: I_OS/2, ports: {Np: InP(A), Nn: InN(A)}
name: A, type: OpAmp, value: A, ports: {InP: InP(A), InN: InN(A), OutP: VODP, OutN: VODN}
]
extrainfo:The circuit is a differential amplifier without mismatches, affecting differential and common-mode gains.

Figure 3.62 Equivalent input offset voltage $\left(V_{O S}\right)$ and current $\left(I_{O S}\right)$ for a differential amplifier. (a) Actual circuit containing mismatches. (b) Equivalent dc circuit with identically matched devices and the offset voltage and current referred to the input.
are treated as the desired signal by subsequent stages. In many analog systems, these types of errors pose the basic limitation on the resolution of the system, and hence consideration of mismatch-induced effects is often central to the design of analog circuits.

#### 3.5.6.1 Input Offset Voltage and Current

For differential amplifiers, the effect of mismatches on dc performance is most conveniently represented by two quantities, the input offset voltage and the input offset current. These quantities represent the input-referred effect of all the component mismatches within the amplifier on its dc performance. ${ }^{11,12}$ As illustrated in Fig. 3.62, the dc behavior of the amplifier containing the mismatches is identical to an ideal amplifier with no mismatches but with the input offset voltage source added in series with the input and the input offset current source in shunt across the input terminals. Both quantities are required to represent the effect of mismatch in general so that the model is valid for any source resistance. For example, if the input terminals are driven by an ideal voltage source with zero resistance, the input offset current does not contribute to the amplifier output, and the offset voltage generator is needed to model the effect of mismatch. On the other hand, if the input terminals are driven by an ideal current source with infinite resistance, the input offset voltage does not contribute to the amplifier output, and the offset current generator is needed to model the effect of mismatch. These quantities are usually a function of both temperature and common-mode input voltage. In the next several sections, we calculate the input offset voltage and current of the emitter-coupled pair and the source-coupled pair.

#### 3.5.6.2 Input Offset Voltage of the Emitter-Coupled Pair

The predominant sources of offset error in the emitter-coupled pair are the mismatches in the base width, base doping level, and collector doping level of the transistors, mismatches in the effective emitter area of the transistors, and mismatches in the collector load resistors. To provide analytical results simple enough for intuitive interpretation, the analysis will be carried out assuming a uniform-base transistor. The results are similar for the nonuniform case, although the analytical procedure is more tedious. In most instances the dc base current is low enough that the dc voltage drop in $r_{b}$ is negligible, so we neglect $r_{b}$.

Consider Fig. 3.45 with dc signals so that $V_{i 1}=V_{I 1}, V_{i 2}=V_{I 2}, V_{o 1}=V_{O 1}$, and $V_{o 2}=$ $V_{O 2}$. Let $V_{I D}=V_{I 1}-V_{I 2}$. Also, assume that the collector resistors may not be identical. Let $R_{C 1}$ and $R_{C 2}$ represent the values of the resistors attached to $Q_{1}$ and $Q_{2}$, respectively. From KVL around the input loop,

$$
\begin{equation*}
V_{I D}-V_{B E 1}+V_{B E 2}=0 \tag{3.202}
\end{equation*}
$$

Therefore,

$$
\begin{equation*}
V_{I D}=V_{T} \ln \frac{I_{C 1}}{I_{S 1}}-V_{T} \ln \frac{I_{C 2}}{I_{S 2}}=V_{T} \ln \frac{I_{C 1}}{I_{C 2}} \frac{I_{S 2}}{I_{S 1}} \tag{3.203}
\end{equation*}
$$

The factors determining the saturation current $I_{S}$ of a bipolar transistor are described in Chapter 1. There it was shown that if the impurity concentration in the base region is uniform, these saturation currents can be written

$$
\begin{align*}
& I_{S 1}=\frac{q n_{i}^{2} \bar{D}_{n}}{N_{A} W_{B 1}\left(V_{C B}\right)} A_{1}=\frac{q n_{i}^{2} \bar{D}_{n}}{Q_{B 1}\left(V_{C B}\right)} A_{1}  \tag{3.204}\\
& I_{S 2}=\frac{q n_{i}^{2} \bar{D}_{n}}{N_{A} W_{B 2}\left(V_{C B}\right)} A_{2}=\frac{q n_{i}^{2} \bar{D}_{n}}{Q_{B 2}\left(V_{C B}\right)} A_{2} \tag{3.205}
\end{align*}
$$

where $W_{B}\left(V_{C B}\right)$ is the base width as a function of $V_{C B}, N_{A}$ is the acceptor density in the base, and $A$ is the emitter area. We denote the product $N_{A} W_{B}\left(V_{C B}\right)$ as $Q_{B}\left(V_{C B}\right)$, the total base impurity doping per unit area.

The input offset voltage $V_{O S}$ is equal to the value of $V_{I D}=V_{I 1}-V_{I 2}$ that must be applied to the input to drive the differential output voltage $V_{O D}=V_{O 1}-V_{O 2}$ to zero. For $V_{O D}$ to be zero, $I_{C 1} R_{C 1}=I_{C 2} R_{C 2}$; therefore,

$$
\begin{equation*}
\frac{I_{C 1}}{I_{C 2}}=\frac{R_{C 2}}{R_{C 1}} \tag{3.206}
\end{equation*}
$$

Substituting (3.204), (3.205), and (3.206) into (3.203) gives

$$
\begin{equation*}
V_{O S}=V_{T} \ln \left[\left(\frac{R_{C 2}}{R_{C 1}}\right)\left(\frac{A_{2}}{A_{1}}\right)\left(\frac{Q_{B 1}\left(V_{C B}\right)}{Q_{B 2}\left(V_{C B}\right)}\right)\right] \tag{3.207}
\end{equation*}
$$

This expression relates the input offset voltage to the device parameters and $R_{C}$ mismatch. Usually, however, the argument of the log function is very close to unity and the equation can be interpreted in a more intuitively satisfying way. In the following section we perform an approximate analysis, valid if the mismatches are small.

#### 3.5.6.3 Offset Voltage of the Emitter-Coupled Pair: Approximate Analysis

In cases of practical interest involving offset voltages and currents, the mismatch between any two nominally matched circuit parameters is usually small compared with the absolute value of that parameter. This observation leads to a procedure by which the individual contributions to offset voltage can be considered separately and summed.

First, define new parameters to describe the mismatch in the components, using the relations

$$
\begin{align*}
\Delta X & =X_{1}-X_{2}  \tag{3.208}\\
X & =\frac{X_{1}+X_{2}}{2} \tag{3.209}
\end{align*}
$$

Thus $\Delta X$ is the difference between two parameters, and $X$ is the average of the two nominally matched parameters. Note that $\Delta X$ can be positive or negative. Next invert (3.208) and (3.209) to give

$$
\begin{align*}
& X_{1}=X+\frac{\Delta X}{2}  \tag{3.210}\\
& X_{2}=X-\frac{\Delta X}{2} \tag{3.211}
\end{align*}
$$

These relations can be applied to the collector resistances, the emitter areas, and the base doping parameters in (3.207) to give

$$
\begin{equation*}
V_{O S}=V_{T} \ln \left[\left(\frac{R_{C}-\frac{\Delta R_{C}}{2}}{R_{C}+\frac{\Delta R_{C}}{2}}\right)\left(\frac{A-\frac{\Delta A}{2}}{A+\frac{\Delta A}{2}}\right)\left(\frac{Q_{B}+\frac{\Delta Q_{B}}{2}}{Q_{B}-\frac{\Delta Q_{B}}{2}}\right)\right] \tag{3.212}
\end{equation*}
$$

With the assumptions that $\Delta R_{C} \ll R_{C}, \Delta A \ll A$, and $\Delta Q_{B} \ll Q_{B}$, (3.212) can be simplified to

$$
\begin{align*}
V_{O S} & \simeq V_{T} \ln \left[\left(1-\frac{\Delta R_{C}}{R_{C}}\right)\left(1-\frac{\Delta A}{A}\right)\left(1+\frac{\Delta Q_{B}}{Q_{B}}\right)\right] \\
& \simeq V_{T}\left[\ln \left(1-\frac{\Delta R_{C}}{R_{C}}\right)+\ln \left(1-\frac{\Delta A}{A}\right)+\ln \left(1+\frac{\Delta Q_{B}}{Q_{B}}\right)\right] \tag{3.213}
\end{align*}
$$

If $x \ll 1$, a Taylor series can be used to show that

$$
\begin{equation*}
\ln (1+x)=x-\frac{x^{2}}{2}+\frac{x^{3}}{3}-\cdots \tag{3.214}
\end{equation*}
$$

Applying (3.214) to each logarithm in (3.213) and ignoring terms higher than first order in the expansions gives

$$
\begin{equation*}
V_{O S} \simeq V_{T}\left(-\frac{\Delta R_{C}}{R_{C}}-\frac{\Delta A}{A}+\frac{\Delta Q_{B}}{Q_{B}}\right) \tag{3.215}
\end{equation*}
$$

Thus, under the assumptions made, we have obtained an approximate expression for the input offset voltage, which is the linear superposition of the effects of the different components. It can be shown that this can always be done for small component mismatches. Note that the signs of the individual terms of (3.215) are not particularly significant, since the mismatch factors can be positive or negative depending on the direction of the random parameter variation. The worst-case offset occurs when the terms have signs such that the individual contributions add.

Equation 3.215 relates the offset voltage to mismatches in the resistors and in the structural parameters $A$ and $Q_{B}$ of the transistors. For the purpose of predicting the offset voltage from device parameters that are directly measurable electrically, we rewrite (3.215) to express the offset in terms of the resistor mismatch and the mismatch in the saturation currents of the transistors:

$$
\begin{equation*}
V_{O S} \simeq V_{T}\left(-\frac{\Delta R_{C}}{R_{C}}-\frac{\Delta I_{S}}{I_{S}}\right) \tag{3.216}
\end{equation*}
$$

where

$$
\begin{equation*}
\frac{\Delta I_{S}}{I_{S}}=\frac{\Delta A}{A}-\frac{\Delta Q_{B}}{Q_{B}} \tag{3.217}
\end{equation*}
$$

is the offset voltage contribution from the transistors themselves, as reflected in the mismatch in saturation current. Mismatch factors $\Delta R_{C} / R_{C}$ and $\Delta I_{S} / I_{S}$ are actually random parameters that take on a different value for each circuit fabricated, and the distribution of the observed values is described by a probability distribution. For large samples the distribution tends toward a normal, or Gaussian, distribution with zero mean. Typically observed standard deviations for the preceding mismatch parameters for small-area diffused devices are

$$
\begin{equation*}
\sigma_{\Delta R / R}=0.01 \quad \sigma_{\Delta I_{S} / I_{S}}=0.05 \tag{3.218}
\end{equation*}
$$

In the Gaussian distribution, 68 percent of the samples have a value within $\pm \sigma$ of the mean value. If we assume that the mean value of the distribution is zero, then 68 percent of the resistor pairs in a large sample will match within 1 percent, and 68 percent of the transistor pairs will have saturation currents that match within 5 percent for the distributions described by (3.218). These values can be heavily influenced by device geometry and processing. If we pick one sample from each distribution so that the parameter mismatch is equal to the corresponding standard deviation, and if the mismatch factors are chosen in the direction so that they add, the resulting offset from (3.216) would be

$$
\begin{equation*}
V_{O S} \simeq(26 \mathrm{mV})(0.01+0.05) \simeq 1.5 \mathrm{mV} \tag{3.219}
\end{equation*}
$$

Large ion-implanted devices with careful layout can achieve $V_{O S} \simeq 0.1 \mathrm{mV}$. A parameter of more interest to the circuit designer than the offset of one sample is the standard deviation of the total offset voltage. Since the offset is the sum of two uncorrelated random parameters, the standard deviation of the sum is equal to the square root of the sum of the squares of the standard deviation of the two mismatch contributions, or

$$
\begin{equation*}
\sigma_{V_{O S}}=V_{T} \sqrt{\left(\sigma_{\Delta R / R}\right)^{2}+\left(\sigma_{\Delta I_{S} / I_{S}}\right)^{2}} \tag{3.220}
\end{equation*}
$$

The properties of the Gaussian distribution are summarized in Appendix A.3.1.

#### 3.5.6.4 Offset Voltage Drift in the Emitter-Coupled Pair

When emitter-coupled pairs are used as low-level dc amplifiers where the offset voltage is critical, provision is sometimes made to manually adjust the input offset voltage to zero with an external potentiometer. When this adjustment is done, the important parameter becomes not the offset voltage itself, but the variation of this offset voltage with temperature, often referred to as drift. For most practical circuits, the sensitivity of the input offset voltage to temperature is not zero, and the wider the excursion of temperature experienced by the circuit, the more error the offset voltage drift will contribute. This parameter is easily calculated for the emitter-coupled pair by differentiating (3.207) as follows

$$
\begin{equation*}
\frac{d V_{O S}}{d T}=\frac{V_{O S}}{T} \tag{3.221}
\end{equation*}
$$

using $V_{T}=k T / q$ and assuming the ratios in (3.207) are independent of temperature. Thus the drift and offset are proportional for the emitter-coupled pair. This relationship is observed experimentally. For example, an emitter-coupled pair with a measured offset voltage of 2 mV would display a drift of $2 \mathrm{mV} / 300^{\circ} \mathrm{K}$ or $6.6 \mu \mathrm{~V} /{ }^{\circ} \mathrm{C}$ under the assumptions we have made.

Equation 3.221 appears to show that the drift also would be nulled by externally adjusting the offset to zero. This observation is only approximately true because of the way in which the nulling is accomplished. ${ }^{13}$ Usually an external potentiometer is placed in parallel with a portion of one of the collector load resistors in the pair. The temperature coefficient of the nulling potentiometer generally does not match that of the diffused resistors, so a resistor-mismatch temperature coefficient is introduced that can make the drift worse than it was without nulling. Voltage drifts in the $1 \mu \mathrm{~V} /{ }^{\circ} \mathrm{C}$ range can be obtained with careful design.

#### 3.5.6.5 Input Offset Current of the Emitter-Coupled Pair

The input offset current $I_{O S}$ is measured with the inputs connected only to current sources and is the difference in the base currents that must be applied to drive the differential output voltage $V_{O D}=V_{O 1}-V_{O 2}$ to zero. Since the base current of each transistor is equal to the corresponding collector current divided by beta, the offset current is

$$
\begin{equation*}
I_{O S}=\frac{I_{C 1}}{\beta_{F 1}}-\frac{I_{C 2}}{\beta_{F 2}} \tag{3.222}
\end{equation*}
$$

when $V_{O D}=0$. As before, we can write

$$
\begin{array}{ll}
I_{C 1}=I_{C}+\frac{\Delta I_{C}}{2} & I_{C 2}=I_{C}-\frac{\Delta I_{C}}{2} \\
\beta_{F 1}=\beta_{F}+\frac{\Delta \beta_{F}}{2} & \beta_{F 2}=\beta_{F}-\frac{\Delta \beta_{F}}{2} \tag{3.224}
\end{array}
$$

Inserting (3.223) and (3.224) into (3.222), the offset current becomes

$$
\begin{equation*}
I_{O S}=\left(\frac{I_{C}+\frac{\Delta I_{C}}{2}}{\beta_{F}+\frac{\Delta \beta_{F}}{2}}-\frac{I_{C}-\frac{\Delta I_{C}}{2}}{\beta_{F}-\frac{\Delta \beta_{F}}{2}}\right) \tag{3.225}
\end{equation*}
$$

Neglecting higher-order terms, this becomes

$$
\begin{equation*}
I_{O S} \simeq \frac{I_{C}}{\beta_{F}}\left(\frac{\Delta I_{C}}{I_{C}}-\frac{\Delta \beta_{F}}{\beta_{F}}\right) \tag{3.226}
\end{equation*}
$$

For $V_{O D}$ to be zero, $I_{C 1} R_{C 1}=I_{C 2} R_{C 2}$; therefore, from (3.206), the mismatch in collector currents is

$$
\begin{equation*}
\frac{\Delta I_{C}}{I_{C}}=-\frac{\Delta R_{C}}{R_{C}} \tag{3.227}
\end{equation*}
$$

Equation 3.227 shows that the fractional mismatch in the collector currents must be equal in magnitude and opposite in polarity from the fractional mismatch in the collector resistors to force $V_{O D}=0$. Substituting (3.227) into (3.226) gives

$$
\begin{equation*}
I_{O S} \simeq-\frac{I_{C}}{\beta_{F}}\left(\frac{\Delta R_{C}}{R_{C}}+\frac{\Delta \beta_{F}}{\beta_{F}}\right) \tag{3.228}
\end{equation*}
$$

A typically observed beta mismatch distribution displays a deviation of about 10 percent. Assuming a beta mismatch of 10 percent and a mismatch in collector resistors of 1 percent, we obtain

$$
\begin{equation*}
I_{O S} \simeq-\frac{I_{C}}{\beta_{F}}\left(\frac{\Delta R_{C}}{R_{C}}+\frac{\Delta \beta_{F}}{\beta_{F}}\right)=-\frac{I_{C}}{\beta_{F}}(0.11)=-0.11\left(I_{B}\right) \tag{3.229}
\end{equation*}
$$

In many applications, the input offset current as well as the input current itself must be minimized. A good example is the input stage of operational amplifiers. Various circuit and technological approaches to reduce these currents are considered in Chapter 6.

#### 3.5.6.6 Input Offset Voltage of the Source-Coupled Pair

As mentioned earlier in the chapter, MOS transistors inherently provide higher input resistance and lower input bias current than bipolar transistors when the MOS gate is used as the input. This observation also applies to differential-pair amplifiers. The input offset current of an MOS differential pair is the difference between the two gate currents and is essentially zero because the gates of the input transistors are connected to silicon dioxide, which is an insulator. However, MOS transistors exhibit lower transconductance than bipolar transistors at the same current, resulting in poorer input offset voltage and common-mode rejection ratio in MOS differential pairs than in the case of bipolar transistors. In this section we calculate the input offset voltage of the source-coupled MOSFET pair.

Consider Fig. 3.50 with dc signals so that $V_{i 1}=V_{I 1}, V_{i 2}=V_{I 2}, V_{o 1}=V_{O 1}$, and $V_{o 2}=$ $V_{O 2}$. Let $V_{I D}=V_{I 1}-V_{I 2}$. Also, assume that the drain resistors may not be identical. Let $R_{D 1}$ and $R_{D 2}$ represent the values of the resistors attached to $M_{1}$ and $M_{2}$, respectively. KVL around the input loop gives

$$
\begin{equation*}
V_{I D}-V_{G S 1}+V_{G S 2}=0 \tag{3.230}
\end{equation*}
$$

Solving (1.157) for the gate-source voltage and substituting into (3.230) gives

$$
\begin{align*}
V_{I D} & =V_{G S 1}-V_{G S 2} \\
& =V_{t 1}+\sqrt{\frac{2 I_{D 1}}{k^{\prime}(W / L)_{1}}}-V_{t 2}-\sqrt{\frac{2 I_{D 2}}{k^{\prime}(W / L)_{2}}} \tag{3.231}
\end{align*}
$$

As in the bipolar case, the input offset voltage $V_{O S}$ is equal to the value of $V_{I D}=V_{I 1}-V_{I 2}$ that must be applied to the input to drive the differential output voltage $V_{O D}=V_{O 1}-V_{O 2}$ to zero. For $V_{O D}$ to be zero, $I_{D 1} R_{D 1}=I_{D 2} R_{D 2}$; therefore,

$$
\begin{equation*}
V_{O S}=V_{t 1}-V_{t 2}+\sqrt{\frac{2 I_{D 1}}{k^{\prime}(W / L)_{1}}}-\sqrt{\frac{2 I_{D 2}}{k^{\prime}(W / L)_{2}}} \tag{3.232}
\end{equation*}
$$

subject to the constraint that $I_{D 1} R_{D 1}=I_{D 2} R_{D 2}$.

#### 3.5.6.7 Offset Voltage of the Source-Coupled Pair: Approximate Analysis

The mismatch between any two nominally matched circuit parameters is usually small compared with the absolute value of that parameter in practice. As a result, (3.232) can be rewritten in a way that allows us to understand the contributions of each mismatch to the overall offset.

Defining difference and average quantities in the usual way, we have

$$
\begin{align*}
\Delta I_{D} & =I_{D 1}-I_{D 2}  \tag{3.233}\\
I_{D} & =\frac{I_{D 1}+I_{D 2}}{2}  \tag{3.234}\\
\Delta(W / L) & =(W / L)_{1}-(W / L)_{2}  \tag{3.235}\\
(W / L) & =\frac{(W / L)_{1}+(W / L)_{2}}{2}  \tag{3.236}\\
\Delta V_{t} & =V_{t 1}-V_{t 2}  \tag{3.237}\\
V_{t} & =\frac{V_{t 1}+V_{t 2}}{2}  \tag{3.238}\\
\Delta R_{L} & =R_{L 1}-R_{L 2}  \tag{3.239}\\
R_{L} & =\frac{R_{L 1}+R_{L 2}}{2} \tag{3.240}
\end{align*}
$$

Rearranging (3.233) and (3.234) as well as (3.235) and (3.236) gives

$$
\begin{align*}
I_{D 1} & =I_{D}+\frac{\Delta I_{D}}{2} & & I_{D 2}=I_{D}-\frac{\Delta I_{D}}{2}  \tag{3.241}\\
(W / L)_{1} & =(W / L)+\frac{\Delta(W / L)}{2} & & (W / L)_{2}=(W / L)-\frac{\Delta(W / L)}{2} \tag{3.242}
\end{align*}
$$

Substituting (3.237), (3.241), and (3.242) into (3.232) gives

$$
\begin{equation*}
V_{O S}=\Delta V_{t}+\sqrt{\frac{2\left(I_{D}+\Delta I_{D} / 2\right)}{k^{\prime}[(W / L)+\Delta(W / L) / 2]}}-\sqrt{\frac{2\left(I_{D}-\Delta I_{D} / 2\right)}{k^{\prime}[(W / L)-\Delta(W / L) / 2]}} \tag{3.243}
\end{equation*}
$$

Rearranging (3.243) gives

$$
\begin{equation*}
V_{O S}=\Delta V_{t}+\left(V_{G S}-V_{t}\right)\left(\sqrt{\frac{1+\Delta I_{D} / 2 I_{D}}{1+\frac{\Delta(W / L)}{2(W / L)}}}-\sqrt{\frac{1-\Delta I_{D} / 2 I_{D}}{1-\frac{\Delta(W / L)}{2(W / L)}}}\right) \tag{3.244}
\end{equation*}
$$

If the mismatch terms are small, the argument of each square root in (3.244) is approximately unity. Using $\sqrt{x} \simeq(1+x) / 2$ when $x \simeq 1$ for the argument of each square root in (3.244), we have

$$
\begin{equation*}
V_{O S} \simeq \Delta V_{t}+\frac{\left(V_{G S}-V_{t}\right)}{2}\left(\frac{1+\Delta I_{D} / 2 I_{D}}{1+\frac{\Delta(W / L)}{2(W / L)}}-\frac{1-\Delta I_{D} / 2 I_{D}}{1-\frac{\Delta(W / L)}{2(W / L)}}\right) \tag{3.245}
\end{equation*}
$$

Carrying out the long divisions in (3.245) and ignoring terms higher than first order gives

$$
\begin{equation*}
V_{O S} \simeq \Delta V_{t}+\frac{\left(V_{G S}-V_{t}\right)}{2}\left(\frac{\Delta I_{D}}{I_{D}}-\frac{\Delta(W / L)}{(W / L)}\right) \tag{3.246}
\end{equation*}
$$

When the differential input voltage is $V_{O S}$, the differential output voltage is zero; therefore, $I_{D 1} R_{L 1}=I_{D 2} R_{L 2}$, and

$$
\begin{equation*}
\frac{\Delta I_{D}}{I_{D}}=-\frac{\Delta R_{L}}{R_{L}} \tag{3.247}
\end{equation*}
$$

In other words, the mismatch in the drain currents must be opposite of the mismatch of the load resistors to set $V_{O D}=0$. Substituting (3.247) into (3.246) gives

$$
\begin{equation*}
V_{O S}=\Delta V_{t}+\frac{\left(V_{G S}-V_{t}\right)}{2}\left(-\frac{\Delta R_{L}}{R_{L}}-\frac{\Delta(W / L)}{(W / L)}\right) \tag{3.248}
\end{equation*}
$$

The first term on the right side of (3.248) stems from threshold mismatch. This mismatch component is present in MOS devices but not in bipolar transistors. This component results in a constant offset component that is bias-current independent. Threshold mismatch is a strong function of process cleanliness and uniformity and can be substantially improved by the use of careful layout. Measurements indicate that large-geometry structures are capable of achieving threshold-mismatch distributions with standard deviations on the order of 2 mV in a modern silicon-gate MOS process. This offset component alone limits the minimum offset in the MOS case and is an order of magnitude larger than the total differential-pair offset in modern ion-implanted bipolar technologies.

The second term on the right side of (3.248) shows that another component of the offset scales with the overdrive $V_{o v}=\left(V_{G S}-V_{t}\right)$ and is related to a mismatch in the load elements or in the device $W / L$ ratio. In the bipolar emitter-coupled pair offset, the corresponding mismatch terms were multiplied by $V_{T}$, typically a smaller number than $V_{o v} / 2$. Thus source-coupled pairs of MOS transistors display higher input offset voltage than bipolar pairs for the same level of geometric mismatch or process gradient even when threshold mismatch is ignored. The key reason for this limitation is that the ratio of the transconductance to the bias current is much lower with MOS transistors than in the bipolar case. The quantities $V_{T}$ in (3.216) and $\left(V_{G S}-V_{t}\right) / 2=V_{o v} / 2$ in (3.248) are both equal to $I_{\mathrm{BIAS}} / g_{m}$ for the devices in question. This quantity is typically in the range 50 mV to 500 mV for MOS transistors instead of 26 mV for bipolar transistors.

#### 3.5.6.8 Offset Voltage Drift in the Source-Coupled Pair

Offset voltage drift in MOSFET source-coupled pairs does not show the high correlation with offset voltage observed in bipolar pairs. The offset consists of several terms that have different temperature coefficients. Both $V_{t}$ and $V_{o v}$ have a strong temperature dependence, affecting $V_{G S}$ in opposite directions. The temperature dependence of $V_{o v}$ stems primarily from the mobility variation, which gives a negative temperature coefficient to the drain current, while the threshold voltage depends on the Fermi potential. As shown in Section 1.5.4, the
latter decreases with temperature and contributes a positive temperature coefficient to the drain current. The drift due to the $\Delta V_{t}$ term in $V_{O S}$ may be quite large if this term itself is large. These two effects can be made to cancel at one value of $I_{D}$, which is a useful phenomenon for temperature-stable biasing of single-ended amplifiers. In differential amplifiers, however, this phenomenon is not greatly useful because differential configurations already give first-order cancellation of $V_{G S}$ temperature variations.

### 3.5.6.9 Small-Signal Characteristics of Unbalanced Differential Amplifiers ${ }^{11}$

As mentioned in Section 3.5.4, the common-mode-to-differential-mode gain and differential-mode-to-common-mode gain of unbalanced differential amplifiers are nonzero. The direct approach to calculation of these cross-gain terms requires analysis of the entire small-signal diagram. In perfectly balanced differential amplifiers, the cross-gain terms are zero, and the differential-mode and common-mode gains can be found by using two independent half circuits, as shown in Section 3.5.5. With imperfect matching, exact half-circuit analysis is still possible if the half circuits are coupled instead of independent. Furthermore, if the mismatches are small, a modified version of half-circuit analysis gives results that are approximately valid. This modified half-circuit analysis not only greatly simplifies the required calculations, but also gives insight about how to reduce $A_{c m-d m}$ and $A_{d m-c m}$ in practice.

First consider a pair of mismatched resistors $R_{1}$ and $R_{2}$ shown in Fig. 3.63. Assume that the branch currents are $i_{1}$ and $i_{2}$, respectively. From Ohm's law, the differential and common-mode voltages across the resistors can be written as

$$
\begin{equation*}
v_{d}=v_{1}-v_{2}=i_{1} R_{1}-i_{2} R_{2} \tag{3.249}
\end{equation*}
$$

and

$$
\begin{equation*}
v_{c}=\frac{v_{1}+v_{2}}{2}=\frac{i_{1} R_{1}+i_{2} R_{2}}{2} \tag{3.250}
\end{equation*}
$$

Define $i_{d}=i_{1}-i_{2}, i_{c}=\left(i_{1}+i_{2}\right) / 2, \Delta R=R_{1}-R_{2}$, and $R=\left(R_{1}+R_{2}\right) / 2$. Then (3.249) and (3.250) can be rewritten as

$$
\begin{equation*}
v_{d}=\left(i_{c}+\frac{i_{d}}{2}\right)\left(R+\frac{\Delta R}{2}\right)-\left(i_{c}-\frac{i_{d}}{2}\right)\left(R-\frac{\Delta R}{2}\right)=i_{d} R+i_{c}(\Delta R) \tag{3.251}
\end{equation*}
$$

and

$$
\begin{equation*}
v_{c}=\frac{\left(i_{c}+\frac{i_{d}}{2}\right)\left(R+\frac{\Delta R}{2}\right)+\left(i_{c}-\frac{i_{d}}{2}\right)\left(R-\frac{\Delta R}{2}\right)}{2}=i_{c} R+\frac{i_{d}(\Delta R)}{4} \tag{3.252}
\end{equation*}
$$

These equations can be used to draw differential and common-mode half circuits for the pair of mismatched resistors. Since the differential half circuit should give half the differential voltage dropped across the resistors, the two terms on the right-hand side of (3.251) are each divided by two and used to represent one component of a branch voltage of $v_{d} / 2$. The differential half circuit is shown in Fig. 3.64a. The first component of the branch voltage is the voltage
image_name:Figure 3.63
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: X1, N2: X2}
name: R2, type: Resistor, value: R2, ports: {N1: X1, N2: X2}
]
extrainfo:The diagram shows two resistors, R1 and R2, in parallel, each with a voltage drop (v1 and v2) and current (i1 and i2) flowing through them.

Figure 3.63 A pair of mismatched resistors.
image_name:(a)
description:
[
name: R, type: Resistor, value: R, ports: {N1: X, N2: X2}
name: i_c, type: CurrentSource, value: (ΔR/2), ports: {Np: X1, Nn: X}
name: i_d, type: CurrentSource, value: (ΔR/2), ports: {Np: X2, Nn: X1}
]
extrainfo:The circuit diagram (a) shows a differential half circuit with a resistor R and two current sources i_c and i_d. The current source i_c flows from node X1 to node X, while i_d flows from node X2 to node X1. There is a voltage drop vd/2 across the resistor R.
image_name:(b)
description:
[
name: R, type: Resistor, value: R, ports: {N1: X, N2: X2}
name: ic, type: CurrentSource, value: ΔR/2, ports: {Np: X2, Nn: X1}
name: id, type: CurrentSource, value: id/2, ports: {Np: X1, Nn: X}
]
extrainfo:The circuit diagram (b) shows a resistor R connected with two current sources. The current source with value ΔR/2 flows from node X2 to X1, and the current source with value id/2 flows from node X1 to X. The voltage across the resistor R is denoted as vc.

Figure 3.64 (a) Differential and (b) common-mode half circuits for a pair of mismatched resistors.
dropped across $R$ and is half the differential current times the average resistor value. The second component is the voltage across the dependent voltage source controlled by the current flowing in the common-mode half circuit and is proportional to half the mismatch in the resistor values. The common-mode half circuit is constructed from (3.252) and is shown in Fig. 3.64b. Here the total branch voltage $v_{c}$ is the sum of the voltages across a resistor and a dependent voltage source controlled by the current flowing in the differential half circuit. In the limiting case where $\Delta R=0$, the voltage across each dependent source in Fig. 3.64 is zero, and each half circuit collapses to simply a resistor of value $R$. Therefore, the half circuits are independent in this case, as expected. In practice, however, $\Delta R \neq 0$, and Fig. 3.64 shows that the differential voltage depends not only on the differential current, but also on the common-mode current. Similarly, the common-mode voltage depends in part on the differential current. Thus the behavior of a pair of mismatched resistors can be represented exactly by using coupled half circuits.

Next consider a pair of mismatched voltage-controlled current sources as shown in Fig. 3.65. Assume that the control voltages are $v_{1}$ and $v_{2}$, respectively. Then the differential and common-mode currents can be written as

$$
\begin{align*}
i_{d} & =i_{1}-i_{2}=g_{m 1} v_{1}-g_{m 2} v_{2} \\
& =\left(g_{m}+\frac{\Delta g_{m}}{2}\right)\left(v_{c}+\frac{v_{d}}{2}\right)-\left(g_{m}-\frac{\Delta g_{m}}{2}\right)\left(v_{c}-\frac{v_{d}}{2}\right) \\
& =g_{m} v_{d}+\Delta g_{m} v_{c} \tag{3.253}
\end{align*}
$$

and

$$
\begin{align*}
i_{c} & =\frac{i_{1}+i_{2}}{2}=\frac{g_{m 1} v_{1}+g_{m 2} v_{2}}{2} \\
& =\frac{\left(g_{m}+\frac{\Delta g_{m}}{2}\right)\left(v_{c}+\frac{v_{d}}{2}\right)+\left(g_{m}-\frac{\Delta g_{m}}{2}\right)\left(v_{c}-\frac{v_{d}}{2}\right)}{2} \\
& =g_{m} v_{c}+\frac{\Delta g_{m} v_{d}}{4} \tag{3.254}
\end{align*}
$$

where $v_{d}=v_{1}-v_{2}, v_{c}=\left(v_{1}+v_{2}\right) / 2, \Delta g_{m}=g_{m 1}-g_{m 2}$, and $g_{m}=\left(g_{m 1}+g_{m 2}\right) / 2$.
image_name:Figure 3.65
description:
[
name: gm1V1, type: VoltageControlledCurrentSource, value: gm1V1, ports: {Np: X1, Nn: X2}
name: gm2V2, type: VoltageControlledCurrentSource, value: gm2V2, ports: {Np: X1, Nn: X2}
]
extrainfo:The diagram shows two voltage-controlled current sources with mismatched transconductance values, gm1 and gm2, connected between nodes X1 and X2.

Figure 3.65 A pair of mismatched voltage-controlled current sources.
image_name:(a)
description:
[
name: g_m v_d/2, type: CurrentControlledCurrentSource, ports: {Np: X1, Nn: X2}
name: Δg_m/2 v_c, type: CurrentControlledCurrentSource, ports: {Np: X1, Nn: X2}
]
extrainfo:The diagram (a) shows a differential half-circuit with two current-controlled current sources connected between nodes X1 and X2. The sources represent the differential transconductance and its mismatch component.
image_name:(b)
description:
[
name: g_m v_c, type: CurrentControlledCurrentSource, ports: {Np: X1, Nn: X2}
name: Δg_m/2 v_d/2, type: CurrentControlledCurrentSource, ports: {Np: X1, Nn: X2}
]
extrainfo:The circuit diagram (b) shows two current-controlled current sources connected between nodes X1 and X2. The sources are characterized by transconductances g_m and Δg_m/2, with dependencies on v_c and v_d/2 respectively.

Figure 3.66 (a) Differential and (b) common-mode half circuits for a pair of mismatched voltagecontrolled current sources.

The corresponding differential and common-mode half circuits each use two voltagecontrolled current sources, as shown in Fig. 3.66. In each case, one dependent source is proportional to the average transconductance and the other to half the mismatch in the transconductances. With perfect matching, the mismatch terms are zero, and the two half circuits are independent. With imperfect matching, however, the mismatch terms are nonzero. In the differential half circuit, the mismatch current source is controlled by the common-mode control voltage. In the common-mode half circuit, the mismatch current source is controlled by half the differential control voltage. Thus, as for mismatched resistors, the behavior of a pair of mismatched voltage-controlled current sources can be represented exactly by using coupled half circuits.

With these concepts in mind, construction of the differential and common-mode half circuits of unbalanced differential amplifiers is straightforward. In the differential half circuit, mismatched resistors are replaced by the circuit shown in Fig. 3.64a, and mismatched voltagecontrolled current sources are replaced by the circuit in Fig. 3.66a. Similarly, the circuits shown in Fig. 3.64b and Fig. 3.66breplace mismatched resistors and voltage-controlled current sources in the common-mode half circuit. Although mismatches change the differential and common-mode components of signals that appear at various points in the complete unbalanced amplifier, the differential components are still equal and opposite while the common-mode components are identical by definition. Therefore, small-signal short and open circuits induced by the differential and common-mode signals are unaffected by these replacements.

For example, the differential and common-mode half circuits of the unbalanced differential amplifier shown in Fig. 3.67 are shown in Fig. 3.68. KCL at the output of the differential half
image_name:Figure 3.67
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: vo1, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: vo2, N2: GND}
name: rtail, type: Resistor, value: rtail, ports: {N1: p, N2: GND}
name: vi1, type: VoltageSource, value: vi1, ports: {Np: v1, Nn: GND}
name: vi2, type: VoltageSource, value: vi2, ports: {Np: vi2, Nn: GND}
name: gm1V1, type: VoltageControlledCurrentSource, value: gm1V1, ports: {Np: vo1, Nn: p}
name: gm2V2, type: VoltageControlledCurrentSource, value: gm2V2, ports: {Np: vo2, Nn: p}
]
extrainfo:The circuit is an unbalanced differential amplifier with differential and common-mode components. It includes resistors R1 and R2 connected to the outputs vo1 and vo2, respectively, and a tail resistor rtail connected to ground. The voltage sources vii, vi1, and vi2 provide the input signals. The current sources gm1V1 and gm2V2 are controlled by the input voltages v1 and v2.

Figure 3.67 The small-signal diagram of an unbalanced differential amplifier.
image_name:Figure 3.67
description:
[
name: Vid/2, type: VoltageSource, value: Vid/2, ports: {Np: Vid/2, Nn: GND}
name: R, type: Resistor, value: R, ports: {Np: X, Nn: Vod/2}
name: iRc ΔR/2, type: VoltageSource, value: iRc ΔR/2, ports: {Np: X, Nn: GND}
name: gm vid/2, type: CurrentSource, value: gm vid/2, ports: {Np: GND, Nn: Vod/2}
name: Δgm/2 v, type: CurrentSource, value: Δgm/2 v, ports: {Np: GND, Nn: Vod/2}
]
extrainfo:The circuit is an unbalanced differential amplifier with differential and common-mode components. It includes resistors R1 and R2 connected to the outputs vo1 and vo2, respectively, and a tail resistor rtail connected to ground. The voltage sources vii, vi1, and vi2 provide the input signals. The current sources gm1V1 and gm2V2 are controlled by the input voltages v1 and v2.

image_name:Figure 3.68 b
description:The circuit is a common-mode half circuit of a differential amplifier. It includes a voltage source Vic providing input voltage vic, a resistor R connected between nodes X and Voc, and a current source iRd/2 connected from node X to ground. The circuit also features a voltage-controlled current source gmV and another voltage-controlled current source Δgm/2, both controlling current between nodes Voc and P. The circuit demonstrates key operations of a differential amplifier in common-mode with components contributing to the overall output voltage voc.

Figure 3.68 (a) Differential and (b) common-mode half circuits of the differential amplifier shown in Fig. 3.67.
circuit in Fig. 3.68a gives

$$
\begin{equation*}
\frac{i_{R d}}{2}+g_{m} \frac{v_{i d}}{2}+\frac{\Delta g_{m}}{2} v=0 \tag{3.255}
\end{equation*}
$$

KCL at the output of the common-mode half circuit in Fig. $3.68 b$ gives

$$
\begin{equation*}
g_{m} v+\frac{\Delta g_{m}}{2} \frac{v_{i d}}{2}+i_{R c}=0 \tag{3.256}
\end{equation*}
$$

Also, KVL around the input loop in the common-mode half circuit gives

$$
\begin{equation*}
v=v_{i c}-v_{\text {tail }}=v_{i c}+2 i_{R c} r_{\text {tail }} \tag{3.257}
\end{equation*}
$$

Substituting (3.257) into (3.256) and rearranging gives

$$
\begin{equation*}
i_{R c}=-\frac{g_{m} v_{i c}+\frac{\Delta g_{m}}{2} \frac{v_{i d}}{2}}{1+2 g_{m} r_{\text {tail }}} \tag{3.258}
\end{equation*}
$$

Substituting (3.257) and (3.258) into (3.255) and rearranging gives

$$
\begin{equation*}
\frac{i_{R d}}{2}=\frac{v_{i d}}{2}\left(-g_{m}+\frac{\Delta g_{m} r_{\text {tail }} \frac{\Delta g_{m}}{2}}{1+2 g_{m} r_{\text {tail }}}\right)+v_{i c}\left(-\frac{\Delta g_{m}}{2}+\frac{\Delta g_{m} r_{\text {tail }} g_{m}}{1+2 g_{m} r_{\text {tail }}}\right) \tag{3.259}
\end{equation*}
$$

From KVL in the $R$ branch in the differential half circuit in Fig. 3.68a,

$$
\begin{equation*}
\frac{v_{o d}}{2}=i_{R c} \frac{\Delta R}{2}+\frac{i_{R d}}{2} R \tag{3.260}
\end{equation*}
$$

Substituting (3.258) and (3.259) into (3.260) and rearranging gives

$$
\begin{equation*}
v_{o d}=A_{d m} v_{i d}+A_{c m-d m} v_{i c} \tag{3.261}
\end{equation*}
$$

where $A_{d m}$ and $A_{c m-d m}$ are

$$
\begin{align*}
A_{d m} & =\left.\frac{v_{o d}}{v_{i d}}\right|_{v_{i c}=0}=-g_{m} R+\frac{\Delta g_{m} r_{\text {tail }} \frac{\Delta g_{m}}{2} R-\frac{\Delta g_{m}}{2} \frac{\Delta R}{2}}{1+2 g_{m} r_{\text {tail }}}  \tag{3.262}\\
A_{c m-d m}= & \left.\frac{v_{o d}}{v_{i c}}\right|_{v_{i d}=0}=-\left(\frac{g_{m} \Delta R+\Delta g_{m} R}{1+2 g_{m} r_{\text {tail }}}\right) \tag{3.263}
\end{align*}
$$

From KVL in the $R$ branch in the common-mode half circuit in Fig. 3.68b,

$$
\begin{equation*}
v_{o c}=\frac{i_{R d}}{2} \frac{\Delta R}{2}+i_{R c} R \tag{3.264}
\end{equation*}
$$

Substituting (3.258) and (3.259) into (3.264) and rearranging gives

$$
\begin{equation*}
v_{o c}=A_{d m-c m} v_{i d}+A_{c m} v_{i c} \tag{3.265}
\end{equation*}
$$

where $A_{d m-c m}$ and $A_{c m}$ are

$$
\begin{align*}
A_{d m-c m} & =\left.\frac{v_{o c}}{v_{i d}}\right|_{v_{i c}=0} \\
& =-\frac{1}{4}\left[g_{m} \Delta R+\frac{\Delta g_{m} R-g_{m} \Delta R\left(2 g_{m} r_{\text {tail }}\left(\frac{\Delta g_{m}}{2 g_{m}}\right)^{2}\right)}{1+2 g_{m} r_{\text {tail }}}\right]  \tag{3.266}\\
A_{c m} & =\left.\frac{v_{o c}}{v_{i c}}\right|_{v_{i d}=0}=-\left(\frac{g_{m} R+\frac{\Delta g_{m}}{2} \frac{\Delta R}{2}}{1+2 g_{m} r_{\text {tail }}}\right) \tag{3.267}
\end{align*}
$$

The calculations in (3.255) through (3.267) are based on the half circuits in Fig. 3.68 and give exactly the same results as an analysis of the entire differential amplifier shown in Fig. 3.67. Because the half circuits are coupled, however, exact half-circuit analysis requires the simultaneous consideration of both half circuits, which is about as complicated as the direct analysis of the entire original circuit.

In practice, the mismatch terms are usually a small fraction of the corresponding average values. As a result, the dominant contributions to the differential signals that control the mismatch generators in the common-mode half circuit stem from differential inputs. Similarly, the dominant part of the common-mode signals that control the mismatch generators in the differential half circuit arise from common-mode inputs. Therefore, we will assume that the signals controlling the mismatch generators can be found approximately by analyzing each half circuit independently without mismatch. The signals that control the mismatch generators in Fig. 3.68 are $i_{R c}, i_{R d} / 2, v$, and $v_{i d} / 2$. We will find approximations to these quantities, $\hat{i}_{R c}$, $\hat{i}_{R d} / 2, \hat{v}$, and $\hat{v}_{i d} / 2$ using the half circuits shown in Fig. 3.69, where the inputs are the same as in Fig. 3.68 but where the mismatch terms are set equal to zero. By ignoring the second-order
image_name:(a)
description:
[
name: Vid/2, type: VoltageSource, value: Vid/2, ports: {Np: Vid/2, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: X, N2: GND}
name: gmVid/2, type: VoltageControlledCurrentSource, ports: {Np: X, Nn: GND}
]
extrainfo:The circuit diagram (a) represents a differential half-circuit of a differential amplifier. It features a voltage source Vid/2, a resistor R, and a voltage-controlled current source gmVid/2. The circuit is grounded at one end. The diagram simplifies the calculation by setting mismatch terms to zero. The current iRd/2 flows through the resistor R, and the current source gmVid/2 is controlled by the voltage Vid/2.
image_name:(b)
description:
[
name: Vic, type: VoltageSource, value: Vic, ports: {Np: Vic, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: X2, N2: GND}
name: gm*V, type: CurrentControlledCurrentSource, ports: {Np: X2, Nn: X1}
name: 2rtail, type: Resistor, value: 2rtail, ports: {N1: X1, N2: GND}
]
extrainfo:The circuit diagram shows a common-mode half circuit of a differential amplifier with mismatch terms set to zero. It includes voltage sources, resistors, and current-controlled current sources. The circuit is analyzed by approximating control signals with mismatch terms ignored.

Figure 3.69 (a) Differential and (b) common-mode half circuits of the differential amplifier shown in Fig. 3.67 with mismatch terms set equal to zero.
interactions in which the mismatch generators influence the values of the control signals, this process greatly simplifies the required calculations, as shown next.

From inspection of the differential half circuit in Fig. 3.69a,

$$
\begin{equation*}
\frac{\hat{v}_{i d}}{2}=\frac{v_{i d}}{2} \tag{3.268}
\end{equation*}
$$

and

$$
\begin{equation*}
\frac{\hat{i}_{R d}}{2}=-g_{m} \frac{v_{i d}}{2} \tag{3.269}
\end{equation*}
$$

From the common-mode half circuit in Fig. 3.69b,

$$
\begin{equation*}
\hat{v}=v_{i c}-g_{m} \hat{v}\left(2 r_{\text {tail }}\right)=\frac{v_{i c}}{1+2 g_{m} r_{\text {tail }}} \tag{3.270}
\end{equation*}
$$

Therefore,

$$
\begin{equation*}
\hat{i}_{R c}=-\frac{g_{m} v_{i c}}{1+2 g_{m} r_{\text {tail }}} \tag{3.271}
\end{equation*}
$$

Now reconsider the differential half circuit with mismatch shown in Fig. 3.68a. Assume that $i_{R c} \simeq \hat{i}_{R c}$ and $v \simeq \hat{v}$. Then

$$
\begin{equation*}
\frac{v_{o d}}{2} \simeq-\frac{\Delta R}{2}\left(\frac{g_{m} v_{i c}}{1+2 g_{m} r_{\text {tail }}}\right)-g_{m} \frac{v_{i d}}{2} R-\frac{\Delta g_{m}}{2} \frac{v_{i c}}{1+2 g_{m} r_{\text {tail }}} R \tag{3.272}
\end{equation*}
$$

From (3.272),

$$
\begin{equation*}
A_{d m}=\left.\frac{v_{o d}}{v_{i d}}\right|_{v_{i c}=0} \simeq-g_{m} R \tag{3.273}
\end{equation*}
$$

and

$$
\begin{equation*}
A_{c m-d m}=\left.\frac{v_{o d}}{v_{i c}}\right|_{v_{i d}=0} \simeq-\left(\frac{g_{m} \Delta R+\Delta g_{m} R}{1+2 g_{m} r_{\text {tail }}}\right) \tag{3.274}
\end{equation*}
$$

Equation 3.274 shows that the ratio $A_{d m} / A_{c m-d m}$ is approximately proportional to $1+2 g_{m} r_{\text {tail }}$. Also, (3.274) agrees exactly with (3.263) in this case because the $g_{m}$ generator in Fig. $3.68 a$ is controlled by a purely differential signal. In other examples, the common-mode-to-differentialmode gain calculated in this way will be only approximately correct.

Now reconsider the common-mode half circuit with mismatch shown in Fig. 3.68b and assume that $i_{R d} \simeq \hat{i}_{R d}$. From KCL at the tail node,

$$
\begin{equation*}
v_{\text {tail }} \simeq\left(g_{m} v+\frac{\Delta g_{m}}{2} \frac{v_{i d}}{2}\right) 2 r_{\text {tail }} \tag{3.275}
\end{equation*}
$$

Then

$$
\begin{equation*}
v=v_{i c}-v_{\text {tail }} \simeq \frac{v_{i c}-\frac{\Delta g_{m}}{2} \frac{v_{i d}}{2}\left(2 r_{\text {tail }}\right)}{1+2 g_{m} r_{\text {tail }}} \tag{3.276}
\end{equation*}
$$

From KCL at the output node in Fig. 3.68b,

$$
\begin{equation*}
\frac{v_{o c}-\frac{i_{R d}}{2} \frac{\Delta R}{2}}{R}+g_{m} v+\frac{\Delta g_{m}}{2} \frac{v_{i d}}{2}=0 \tag{3.277}
\end{equation*}
$$

Assume that $i_{R d} \simeq \hat{i}_{R d}$. Substituting (3.269) and (3.276) into (3.277) and rearranging gives

$$
\begin{equation*}
v_{o c} \simeq-\frac{1}{4}\left(g_{m} \Delta R+\frac{\Delta g_{m} R}{1+2 g_{m} r_{\text {tail }}}\right) v_{i d}-\frac{g_{m} R}{1+2 g_{m} r_{\text {tail }}} v_{i c} \tag{3.278}
\end{equation*}
$$

From (3.278),

$$
\begin{equation*}
A_{d m-c m}=\left.\frac{v_{o c}}{v_{i d}}\right|_{v_{i c}=0} \simeq-\frac{1}{4}\left(g_{m} \Delta R+\frac{\Delta g_{m} R}{1+2 g_{m} r_{\text {tail }}}\right) \tag{3.279}
\end{equation*}
$$

and

$$
\begin{equation*}
A_{c m}=\left.\frac{v_{o c}}{v_{i c}}\right|_{v_{i d}=0} \simeq-\frac{g_{m} R}{1+2 g_{m} r_{\text {tail }}} \tag{3.280}
\end{equation*}
$$

These equations show that increasing the degeneration to common-mode inputs represented by the quantity $1+2 g_{m} r_{\text {tail }}$ reduces the magnitude of $A_{c m-d m}, A_{d m-c m}$, and $A_{c m}$. As $r_{\text {tail }} \rightarrow \infty$ in this case, $A_{c m-d m} \rightarrow 0$ and $A_{c m} \rightarrow 0$. On the other hand, $A_{d m-c m}$ does not approach zero when $r_{\text {tail }}$ becomes infinite. Instead,

$$
\begin{equation*}
\lim _{r_{\text {tail }} \rightarrow \infty} A_{d m-c m} \simeq-\frac{g_{m} \Delta R}{4} \tag{3.281}
\end{equation*}
$$

With finite and mismatched transistor output resistances, $A_{c m-d m}$ also approaches a nonzero value as $r_{\text {tail }}$ becomes infinite. Therefore, $r_{\text {tail }}$ should be viewed as an important parameter because it reduces the sensitivity of differential pairs to common-mode inputs and helps reduce the effects of mismatch. However, even an ideal tail current source does not overcome all the problems introduced by mismatch. In Chapter 4, we will consider transistor current sources for which $r_{\text {tail }}$ can be quite large.

#### EXAMPLE

Consider the unbalanced differential amplifier in Fig. 3.67. Assume that

$$
\begin{aligned}
& g_{m 1}=1.001 \mathrm{~mA} / \mathrm{V} \quad g_{m 2}=0.999 \mathrm{~mA} / \mathrm{V} \\
& R_{1}=101 \mathrm{k} \Omega \quad R_{2}=99 \mathrm{k} \Omega \quad r_{\text {tail }}=1 \mathrm{M} \Omega
\end{aligned}
$$

Find $A_{d m}, A_{c m}, A_{c m-d m}$, and $A_{d m-c m}$.

Calculating average and mismatch quantities gives

$$
\begin{array}{ll}
g_{m}=\frac{g_{m 1}+g_{m 2}}{2}=1 \frac{\mathrm{~mA}}{\mathrm{~V}} & \Delta g_{m}=g_{m 1}-g_{m 2}=0.002 \frac{\mathrm{~mA}}{\mathrm{~V}} \\
R=\frac{R_{1}+R_{2}}{2}=100 \mathrm{k} \Omega & \Delta R=R_{1}-R_{2}=2 \mathrm{k} \Omega
\end{array}
$$

From (3.269)

$$
\frac{\hat{i}_{R d}}{2}=-1 \frac{\mathrm{~mA}}{\mathrm{~V}} \frac{v_{i d}}{2}=-\frac{v_{i d}}{2 \mathrm{k} \Omega}
$$

From (3.271)

$$
\hat{i}_{R c}=-\frac{1 \frac{\mathrm{~mA}}{\mathrm{~V}} v_{i c}}{1+2(1)(1000)}=-\frac{v_{i c}}{2001 \mathrm{k} \Omega}
$$

From (3.273), (3.274), (3.279), and (3.280),

$$
\begin{aligned}
A_{d m} & \simeq-1(100)=-100 \\
A_{c m-d m} & \simeq-\frac{1(2)+0.002(100)}{1+2(1)(1000)} \simeq-0.0011 \\
A_{d m-c m} & \simeq-\frac{1}{4}\left(1(2)+\frac{0.002(100)}{1+2(1)(1000)}\right) \simeq-0.5 \\
A_{c m} & \simeq-\frac{1(100)}{1+2(1)(1000)} \simeq-0.05
\end{aligned}
$$

## APPENDIX

### A.3.1 ELEMENTARY STATISTICS AND THE GAUSSIAN DISTRIBUTION

From the standpoint of a circuit designer, many circuit parameters are best regarded as random variables whose behavior is described by a probability distribution. This view is particularly important in the case of a parameter such as offset voltage. Even though the offset may be zero with perfectly matched components, random variations in resistors and transistors cause a spread of offset voltage around the mean value, and the size of this spread determines the fraction of circuits that meet a given offset specification.

Several factors cause the parameters of an integrated circuit to show random variations. One of these factors is the randomness of the edge definition when regions are defined to form resistors and active devices. In addition, random variations across the wafer in the diffusion of impurities can be a significant factor. These processes usually give rise to a Gaussian distribution (sometimes called a normal distribution) of the parameters. A Gaussian distribution of a parameter $x$ is specified by a probability density function $p(x)$ given by

$$
\begin{equation*}
p(x)=\frac{1}{\sqrt{2 \pi} \sigma} \exp \left[-\frac{(x-m)^{2}}{2 \sigma^{2}}\right] \tag{3.282}
\end{equation*}
$$

where $\sigma$ is the standard deviation of the distribution and $m$ is the mean or average value of $x$. The significance of this function is that, for one particular circuit chosen at random from a large collection of circuits, the probability of the parameter having values between $x$ and $(x+d x)$ is given by $p(x) d x$, which is the area under the curve $p(x)$ in the range $x$ to $(x+d x)$. For
image_name:Figure 3.70 Probability density function
description:The graph depicted is a Gaussian distribution, also known as a normal distribution, representing the probability density function (PDF) given by \( p(x) = \frac{1}{\sqrt{2\pi}\sigma} \exp\left[-\frac{(x-m)^2}{2\sigma^2}\right] \). It is characterized by its bell-shaped curve.

1. **Type of Graph and Function:**
- This is a probability density function graph for a Gaussian distribution.

2. **Axes Labels and Units:**
- The vertical axis, labeled \( p(x) \), is on a linear scale and represents the probability density, measured in units of \( 1/\sigma \).
- The horizontal axis, labeled \( x \), is also on a linear scale and represents the variable \( x \).

3. **Overall Behavior and Trends:**
- The graph displays a symmetric bell-shaped curve centered around the mean \( m \).
- The distribution is symmetric about \( m \), with the highest point (peak) at \( x = m \).
- The curve approaches zero as \( x \) moves away from the mean, both to the left and right.

4. **Key Features and Technical Details:**
- The peak of the curve occurs at \( x = m \), which is the mean.
- The width of the curve is determined by the standard deviation \( \sigma \), with inflection points occurring at \( m - \sigma \) and \( m + \sigma \).
- The points \( m - 2\sigma \) and \( m + 2\sigma \) are marked, indicating the range within which approximately 95% of the values lie in a normal distribution.

5. **Annotations and Specific Data Points:**
- The annotations include markers at \( m - 2\sigma \), \( m - \sigma \), \( m \), \( m + \sigma \), and \( m + 2\sigma \), highlighting the mean and standard deviation intervals.
- The maximum value of \( p(x) \) is approximately \( 0.5/\sigma \) at \( x = m \).

Figure 3.70 Probability density function $p(x)$ for a Gaussian distribution with mean value $m$ and standard deviation $\sigma . p(x)=\exp \left[-(x-m)^{2} /\left(2 \sigma^{2}\right)\right] /(\sqrt{2 \pi} \sigma)$.
example, the probability that $x$ has a value less than $X$ is obtained by integrating (3.282) to give

$$
\begin{align*}
P(x<X) & =\int_{-\infty}^{X} p(x) d x  \tag{3.283}\\
& =\int_{-\infty}^{X} \frac{1}{\sqrt{2 \pi} \sigma} \exp \left[-\frac{(x-m)^{2}}{2 \sigma^{2}}\right] d x \tag{3.284}
\end{align*}
$$

In a large sample, the fraction of circuits where $x$ is less than $X$ will be given by the probability $P(x<X)$, and thus this quantity has real practical significance. The probability density function $p(x)$ in (3.282) is sketched in Fig. 3.70 and shows a characteristic bell shape. The peak value of the distribution occurs when $x=m$, where $m$ is the mean value of $x$. The standard deviation $\sigma$ is a measure of the spread of the distribution, and large values of $\sigma$ give rise to a broad distribution. The distribution extends over $-\infty<x<\infty$, as shown by (3.282), but most of the area under the curve is found in the range $x=m \pm 3 \sigma$, as will be seen in the following analysis.

The development thus far has shown that the probability of the parameter $x$ having values in a certain range is just equal to the area under the curve of Fig. 3.70 in that range. Since $x$ must lie somewhere in the range $\pm \infty$, the total area under the curve must be unity, and integration of (3.282) will show that this is so. The most common specification of interest to circuit designers is the fraction of a large sample of circuits that lies inside a band around the mean. For example, if a circuit has a gain $x$ that has a Gaussian distribution with mean value 100, what fraction of circuits have gain values in the range 90 to 110? This fraction can be found by evaluating the probability that $x$ takes on values in the range $x=m \pm 10$ where $m=100$. This probability could be found from (3.282) if $\sigma$ is known by integrating as follows:

$$
\begin{equation*}
P(m-10<x<m+10)=\int_{m-10}^{m+10} \frac{1}{\sqrt{2 \pi} \sigma} \exp \left[-\frac{(x-m)^{2}}{2 \sigma^{2}}\right] d x \tag{3.285}
\end{equation*}
$$

This equation gives the area under the Gaussian curve in the range $x=m \pm 10$.

| $k$ | Area under the Gaussian curve <br> in the range $m \pm k \sigma$ |
| :--- | :---: |
| 0.2 | 0.159 |
| 0.4 | 0.311 |
| 0.6 | 0.451 |
| 0.8 | 0.576 |
| 1.0 | 0.683 |
| 1.2 | 0.766 |
| 1.4 | 0.838 |
| 1.6 | 0.890 |
| 1.8 | 0.928 |
| 2.0 | 0.954 |
| 2.2 | 0.972 |
| 2.4 | 0.984 |
| 2.6 | 0.991 |
| 2.8 | 0.995 |
| 3.0 | 0.997 |

Figure 3.71 Values of the integral in (3.286) for various values of $k$. This integral gives the area under the Gaussian curve of Fig. 3.70 in the range $x= \pm k \sigma$ 。

To simplify calculations of the kind described above, values of the integral in (3.285) have been calculated and tabulated. To make the tables general, the range of integration is normalized to $\sigma$ to give

$$
\begin{equation*}
P(m-k \sigma<x<m+k \sigma)=\int_{m-k \sigma}^{m+k \sigma} \frac{1}{\sqrt{2 \pi} \sigma} \exp \left[-\frac{(x-m)^{2}}{2 \sigma^{2}}\right] d x \tag{3.286}
\end{equation*}
$$

Values of this integral for various values of $k$ are tabulated in Fig. 3.71. This table shows that $P=0.683$ for $k=1$ and thus 68.3 percent of a large sample of a Gaussian distribution lies within a range $x=m \pm \sigma$. For $k=3$, the value of $P=0.997$ and thus 99.7 percent of a large sample lies within a range $x=m \pm 3 \sigma$.

Circuit parameters such as offset or gain often can be expressed as a linear combination of other parameters as shown in (3.216) and (3.248) for offset voltage. If all the parameters are independent random variables with Gaussian distributions, the standard deviations and means can be related as follows. Assume that the random variable $x$ can be expressed in terms of random variables $a, b$, and $c$ using

$$
\begin{equation*}
x=a+b-c \tag{3.287}
\end{equation*}
$$

Then it can be shown that

$$
\begin{align*}
m_{x} & =m_{a}+m_{b}-m_{c}  \tag{3.288}\\
\sigma_{x}^{2} & =\sigma_{a}^{2}+\sigma_{b}^{2}+\sigma_{c}^{2} \tag{3.289}
\end{align*}
$$

where $m_{x}$ is the mean value of $x$ and $\sigma_{x}$ is the standard deviation of $x$. Equation 3.289 shows that the square of the standard deviation of $x$ is the sum of the square of the standard deviations of $a, b$, and $c$. This result extends to any number of variables.

These results were treated in the context of the random variations found in circuit parameters. The Gaussian distribution is also useful in the treatment of random noise, as described in Chapter 11.

#### EXAMPLE

The offset voltage of a circuit has a mean value of $m=0$ and a standard deviation of $\sigma=2$ mV . What fraction of circuits will have offsets with magnitudes less than 4 mV ?

A range of offset of $\pm 4 \mathrm{mV}$ corresponds to $\pm 2 \sigma$. From Fig. 3.71, we find that the area under the Gaussian curve in this range is 0.954 , and thus 95.4 percent of circuits will have offsets with magnitudes less than 4 mV .
