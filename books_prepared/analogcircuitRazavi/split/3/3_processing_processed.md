# 3. Diode Models and Circuits

Having studied the physics of diodes in Chapter 2, we now rise to the next level of abstraction and deal with diodes as circuit elements, ultimately arriving at interesting and real-life applications. This chapter also prepares us for understanding transistors as circuit elements in subsequent chapters. We proceed as follows:

## 3.1 IDEAL DIODE

### 3.1.1 Initial Thoughts

In order to appreciate the need for diodes, let us briefly study the design of a cellphone charger. The charger converts the line ac voltage at $110 \mathrm{~V}^{1}$ and $60 \mathrm{~Hz}^{2}$ to a dc voltage of 3.5 V. As shown in Fig. 3.1(a), this is accomplished by first stepping down the ac voltage by means of a transformer to about 4 V and subsequently converting the ac voltage to a dc quantity. ${ }^{3}$ The same principle applies to adaptors that power other electronic devices.

How does the black box in Fig. 3.1(a) perform this conversion? As depicted in Fig. 3.1(b), the output of the transformer exhibits a zero dc content because the negative and positive half cycles enclose equal areas, leading to a zero average. Now suppose this waveform is applied to a mysterious device that passes the positive half cycles but blocks the negative ones. The result displays a positive average and some ac components, which can be removed by a low-pass filter (Section 3.5.1).

[^12]image_name:(a) Charger circuit
description:
[
name: Vline, type: VoltageSource, value: 110√2V, 60Hz, ports: {Np: N1, Nn: GND}
name: Transformer, type: Transformer, ports: {In1: N1, In2: GND, Out1: N2, Out2: GND}
name: V1, type: VoltageSource, value: 4√2V, 60Hz, ports: {Np: N2, Nn: GND}
name: Block Box, type: Other, ports: {N1: N2, N2: Vout}
name: Vout, type: VoltageSource, value: 3.5V, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a charger circuit that converts AC voltage to a DC output. It uses a transformer to step down the voltage and a block box to rectify the waveform by eliminating negative half cycles, resulting in a DC output with a positive average voltage.
image_name:(b) elimination of negative half cycles
description:The graph in Fig. 3.1(b) is a time-domain waveform illustrating the process of eliminating negative half cycles from an AC signal. The X-axis represents time (t), and the Y-axis represents voltage (V). The waveform on the left side of the graph shows an AC signal with equal positive and negative areas, indicating a zero DC content. This waveform is sinusoidal with peaks at regular intervals, representing a typical AC signal with a frequency of 60 Hz.

The right side of the graph demonstrates the effect of a device that allows only the positive half cycles to pass through while blocking the negative ones. As a result, the waveform consists solely of the positive half cycles, leading to a signal with a positive average voltage. This transformation creates a waveform with positive areas only, effectively converting the AC signal into a pulsating DC signal.

The graph visually emphasizes the conversion process, highlighting how the negative half cycles are removed, resulting in a waveform that can be further processed, such as by using a low-pass filter to smooth out the remaining AC components and achieve a more stable DC output.

(b)

Figure 3.1 (a) Charger circuit, (b) elimination of negative half cycles.

Did you know?

The rectification effect was discovered by Carl Braun around 1875. He observed that a metal wire pressed against a sulphide carried more current in one direction than the other. In subsequent decades, researchers tried other structures, arriving at "cat's whisker" rectifiers, which served as detectors for the reception of wireless signals in early radios and radars. These were eventually supplanted by pn junctions.

The waveform conversion in Fig. 3.1(b) points to the need for a device that discriminates between positive and negative voltages, passing only one and blocking the other. A simple resistor cannot serve in this role because it is linear. That is, Ohm's law, $V=I R$, implies that if the voltage across a resistor goes from positive to negative, so does the current through it. We must therefore seek a device that behaves as a short for positive voltages and as an open for negative voltages.

Figure 3.2 summarizes the result of our thought process thus far. The mysterious device generates an output equal to the input for positive half cycles and equal to zero for negative half cycles. Note that the device is nonlinear because it does not satisfy $y=\alpha x$; if $x \rightarrow-x, y \nrightarrow-y$.
image_name:Figure 3.2
description:The graph in Figure 3.2 illustrates the behavior of an ideal diode in response to an input signal, represented as a time-domain waveform. The horizontal axis is labeled \( t \), indicating time, while the vertical axis shows two waveforms: \( x(t) \) as the input and \( y(t) \) as the output.

The input waveform \( x(t) \) is a sinusoidal signal that oscillates above and below the horizontal axis, representing alternating positive and negative half-cycles. The output waveform \( y(t) \) is derived from \( x(t)\) and exhibits a rectified behavior. For the positive half-cycles of \( x(t) \), \( y(t) \) mirrors \( x(t) \), indicating that the diode allows current to pass. For the negative half-cycles of \( x(t) \), \( y(t) \) remains at zero, showing that the diode blocks current flow.

This behavior is characteristic of an ideal diode, which conducts current only in one direction. The graph visually demonstrates the rectification process, where only the positive portions of the input signal are transmitted to the output, effectively clipping the negative portions. This results in a waveform that is non-linear, as it does not follow a proportional relationship with the input.

Figure 3.2 Conceptual operation of a diode.

### 3.1.2 Ideal Diode

The mysterious device mentioned above is called an "ideal diode." Shown in Fig. 3.3(a), the diode is a two-terminal device, with the triangular head denoting the allowable direction of current flow and the vertical bar representing the blocking behavior for currents in the opposite direction. The corresponding terminals are called the "anode" and the "cathode," respectively.
image_name:(a)
description:
[
name: D1, type: Diode, ports: {Na: Anode, Nc: Cathode}
]
extrainfo:The diagram illustrates the symbol and operation of an ideal diode. It shows the diode in forward and reverse bias conditions. In forward bias, the diode conducts current, while in reverse bias, it blocks current. The water pipe analogy is used to explain the diode's operation, where the diode acts like a valve that allows flow in one direction and blocks it in the opposite direction.
image_name:(b)
description:
[
name: D1, type: Diode, ports: {Na: +, Nc: -}
]
extrainfo:The circuit diagram (b) represents the equivalent circuit of a diode under forward and reverse bias conditions. In forward bias, the diode allows current flow, represented by a closed switch. In reverse bias, the diode blocks current flow, represented by an open switch.
image_name:(c)
description:The image labeled as Figure 3.3(c) illustrates a water pipe analogy for a diode, explaining its function in terms of fluid flow. This analogy helps to conceptualize how a diode operates in forward and reverse bias conditions.

1. **Identification of Components and Structure:**
- The diagram shows a cylindrical pipe with a valve mechanism inside. The pipe represents the pathway for current flow, while the valve mimics the diode's ability to control this flow.
- The pipe is labeled with components such as "Hinge," "Stopper," and "Valve," which are parts of the valve mechanism.

2. **Connections and Interactions:**
- In the **Forward Bias** condition, the valve is open, allowing fluid (analogous to current) to flow freely through the pipe. This represents the diode being forward-biased, where it conducts current.
- In the **Reverse Bias** condition, the valve is closed, preventing fluid flow. This illustrates the diode being reverse-biased, where it blocks current.
- Arrows indicate the direction of fluid flow, corresponding to the direction of current flow in an electrical circuit.

3. **Labels, Annotations, and Key Features:**
- The diagram includes labels such as "Forward Bias" and "Reverse Bias" to differentiate the two operating states of the diode.
- The components like "Pipe," "Hinge," "Stopper," and "Valve" are annotated to clarify the parts of the analogy.

Overall, this water pipe analogy effectively demonstrates the basic operational principles of a diode, using the familiar concept of fluid flow to explain electrical behavior.

Figure 3.3 (a) Diode symbol, (b) equivalent circuit, (c) water pipe analogy.

Forward and Reverse Bias To serve as the mysterious device in the charger example of Fig. 3.3(a), the diode must turn "on" if $V_{\text {anode }}>V_{\text {cathode }}$ and "off" if $V_{\text {anode }}<V_{\text {cathode }}$ [Fig. 3.3(b)]. Defining $V_{\text {anode }}-V_{\text {cathode }}=V_{D}$, we say the diode is "forward-biased" if $V_{D}$ tends to exceed zero and "reverse-biased" if $V_{D}<0.4$

A water pipe analogy proves useful here. Consider the pipe shown in Fig. 3.3(c), where a valve (a plate) is hinged on the top and faces a stopper on the bottom. If water pressure is applied from the left, the valve rises, allowing a current. On the other hand, if water pressure is applied from the right, the stopper keeps the valve shut.

As with other two-terminal devices, diodes can be placed in series (or in parallel). Determine which one of the configurations in Fig. 3.4 can conduct current.
image_name:(a)
description:
[
name: D1, type: Diode, ports: {Na: A, Nc: B}
name: D2, type: Diode, ports: {Na: B, Nc: C}
]
extrainfo:The diodes D1 and D2 are connected in series with their anodes facing the same direction, allowing current to flow from node A to node C through node B.

(a)
image_name:(a)
description:
[
name: D1, type: Diode, ports: {Na: A, Nc: B}
name: D2, type: Diode, ports: {Na: B, Nc: C}
]
extrainfo:The diodes D1 and D2 are connected in series with their anodes facing the same direction, allowing current to flow from node A to node C through node B.

(b)
image_name:(a)
description:
[
name: D1, type: Diode, ports: {Na: A, Nc: B}
name: D2, type: Diode, ports: {Na: B, Nc: C}
]
extrainfo:The diodes D1 and D2 are connected in series with their anodes facing the same direction, allowing current to flow from node A to node C through node B.

(c)

Figure 3.4 Series combinations of diodes.

[^13]Solution In Fig. 3.4(a), the anodes of $D_{1}$ and $D_{2}$ point to the same direction, allowing the flow of current from $A$ to $B$ to $C$ but not in the reverse direction. In Fig. 3.4(b), $D_{1}$ stops current flow from $B$ to $A$, and $D_{2}$, from $B$ to $C$. Thus, no current can flow in either direction. By the same token, the topology of Fig. 3.4(c) behaves as an open for any voltage. Of course, none of these circuits appears particularly useful at this point, but they help us become comfortable with diodes.

Exercise Determine all possible series combinations of three diodes and study their conduction properties.

I/V Characteristics In studying electronic devices, it is often helpful to accompany equations with graphical visualizations. A common type of plot is that of the current/voltage (I/V) characteristic, i.e., the current that flows through the device as a function of the voltage across it.

Since an ideal diode behaves as a short or an open, we first construct the I/V characteristics for two special cases of Ohm's law:

$$
\begin{array}{r}
R=0 \Rightarrow I=\frac{V}{R}=\infty \\
R=\infty \Rightarrow I=\frac{V}{R}=0 \tag{3.2}
\end{array}
$$

The results are illustrated in Fig. 3.5(a). For an ideal diode, we combine the positive-voltage region of the first with the negative-voltage region of the second, arriving at the $\mathrm{I}_{D} / \mathrm{V}_{D}$ characteristic in Fig. 3.5(b). Here, $V_{D}=V_{\text {anode }}-V_{\text {cathode }}$, and $I_{D}$ is defined as the current flowing into the anode and out of the cathode.
image_name:(a)
description:The diagram labeled "(a)" shows the I/V characteristics for two extreme cases of resistance: zero resistance (R=0) and infinite resistance (R=∞).

**Type of Graph and Function:**
- This is a current-voltage (I/V) characteristic graph.

**Axes Labels and Units:**
- The horizontal axis represents voltage (V).
- The vertical axis represents current (I).
- The axes are marked with arrows indicating positive directions.

**Overall Behavior and Trends:**
- For R=0: The graph shows a vertical line at V=0, indicating that the current (I) is theoretically infinite for any applied voltage, which is consistent with Ohm’s Law (I=V/R) when R is zero.
- For R=∞: The graph shows a horizontal line along the V-axis, indicating that the current (I) is zero regardless of the voltage applied. This represents an open circuit condition where no current flows.

**Key Features and Technical Details:**
- The vertical line for R=0 suggests a short circuit scenario where any finite voltage results in an infinite current.
- The horizontal line for R=∞ represents a perfect insulator or open circuit where no current can flow.

**Annotations and Specific Data Points:**
- The graph is annotated with labels R=0 and R=∞ to indicate the conditions being illustrated.

(a)
image_name:Figure 3.5 (b)
description:The graph in Figure 3.5(b) illustrates the current-voltage (I-V) characteristics of an ideal diode. It is a two-dimensional plot with the horizontal axis labeled as \( V_D \) representing the diode voltage, and the vertical axis labeled as \( I_D \) representing the diode current. Both axes are marked in a linear scale.

**Type of Graph and Function:**
The graph is a characteristic curve of an ideal diode, showing the relationship between the diode current and voltage.

**Axes Labels and Units:**
- **Horizontal Axis (\( V_D \)):** Represents the voltage across the diode.
- **Vertical Axis (\( I_D \)):** Represents the current through the diode.

**Overall Behavior and Trends:**
- **Reverse Bias (Left Side):** The graph shows no current flow in the reverse bias region (\( V_D < 0 \)), indicating that the ideal diode does not conduct any current when reverse-biased.
- **Forward Bias (Right Side):** For \( V_D > 0 \), the graph suggests that the diode turns on and conducts current immediately as the voltage becomes slightly positive. The current is shown as infinite, represented by a vertical line, indicating that the ideal diode has zero forward resistance and conducts maximum current instantly.

**Key Features and Technical Details:**
- **Reverse Bias Region:** No current flow is indicated, suggesting the diode acts as an open circuit.
- **Forward Bias Region:** The diode conducts infinite current, represented by a vertical line, which is characteristic of an ideal diode with zero forward voltage drop.

**Annotations and Specific Data Points:**
- The graph is annotated with 'Reverse Bias' on the left side and 'Forward Bias' on the right side to indicate the operational regions of the diode.
- The transition from non-conducting to conducting occurs at \( V_D = 0 \), although the graph does not depict any specific numerical values for current or voltage beyond this transition point.

(b)

Figure 3.5 I/V characteristics of (a) zero and infinite resistors, (b) ideal diode.

Example
3.2

We said that an ideal diode turns on for positive anode-cathode voltages. But the characteristic in Fig. 3.5(b) does not appear to show any $I_{D}$ values for $V_{D}>0$. How do we interpret this plot?

Solution This characteristic indicates that as $V_{D}$ exceeds zero by a very small amount, then the diode turns on and conducts infinite current if the circuit surrounding the diode can provide such a current. Thus, in circuits containing only finite currents, a forward-biased ideal diode sustains a zero voltage-similar to a short circuit.

Exercise

How is the characteristic modified if we place a $1-\Omega$ resistor in series with the diode?
image_name:(a)
description:
[
name: VA, type: VoltageSource, value: VA, ports: {Np: VA, Nn: GND}
name: D1, type: Diode, ports: {Na: VA, Nc: GND}
name: D2, type: Diode, ports: {Na: GND, Nc: VA}
]
extrainfo:The circuit consists of two antiparallel diodes (D1 and D2) connected in parallel with a voltage source (VA). The characteristic I/V curve shows that the circuit acts as a short for all voltages, allowing infinite current (IA) to flow in either direction depending on the polarity of VA.
image_name:(b)
description:The graph in Figure 3.6(b) is an I-V characteristic plot for a circuit with antiparallel diodes.

1. **Type of Graph and Function:**
- The graph is an I-V (current-voltage) characteristic plot.

2. **Axes Labels and Units:**
- The horizontal axis represents the voltage across the diodes, labeled as \( V_A \).
- The vertical axis represents the current through the circuit, labeled as \( I_A \).
- Both axes use a linear scale.

3. **Overall Behavior and Trends:**
- The graph shows a vertical line at \( V_A = 0 \), indicating that for any small positive or negative voltage, the current \( I_A \) is infinite. This behavior is characteristic of an ideal short circuit.

4. **Key Features and Technical Details:**
- The plot indicates that the antiparallel diode configuration allows infinite current flow regardless of the polarity of \( V_A \) due to one diode always being forward-biased.
- There are no peaks, valleys, or inflection points as the line is vertical.

5. **Annotations and Specific Data Points:**
- There are no specific annotations or markers, but the graph's vertical line highlights the infinite current flow for any \( V_A \) value, reflecting the ideal short circuit behavior of the antiparallel diodes.

This characteristic explains why the antiparallel diode configuration acts as a short circuit, making it seem like a useless circuit in its ideal form, but potentially more interesting with real diodes.

Figure 3.6 (a) Antiparallel diodes, (b) resulting I/V characteristic.

Solution If $V_{A}>0, D_{1}$ is on and $D_{2}$ is off, yielding $I_{A}=\infty$. If $V_{A}<0, D_{1}$ is off, but $D_{2}$ is on, again leading to $I_{A}=\infty$. The result is illustrated in Fig. 3.6(b). The antiparallel combination therefore acts as a short for all voltages. Seemingly a useless circuit, this topology becomes much more interesting with actual diodes (Section 3.5.3).

Exercise Repeat the above example if a 1-V battery is placed in series with the parallel combination of the diodes.
image_name:(a)
description:
[
name: VA, type: VoltageSource, value: VA, ports: {Np: VA, Nn: GND}
name: D1, type: Diode, ports: {Na: VA, Nc: VH}
name: R1, type: Resistor, value: R1, ports: {N1: VH, N2: GND}
]
extrainfo:The circuit consists of a voltage source VA, a diode D1, and a resistor R1 in series. When VA is positive, the diode is forward-biased, and the current IA flows through the diode and resistor. The circuit demonstrates basic diode-resistor behavior under forward and reverse bias conditions.
image_name:(b)
description:
[
name: VA, type: VoltageSource, value: VA, ports: {Np: Vp, Nn: GND}
name: D1, type: Diode, ports: {Na: Vp, Nc: Vk}
name: R1, type: Resistor, value: R1, ports: {N1: Vk, N2: Vn}
]
extrainfo:The circuit diagram (b) represents a diode D1 in series with a resistor R1. The voltage source VA is connected to the anode of the diode and the ground. The cathode of the diode is connected to one terminal of the resistor, and the other terminal of the resistor is connected to node Vn.
image_name:(c)
description:
[
name: VA, type: VoltageSource, value: VA, ports: {Np: VA, Nn: GND}
name: D1, type: Diode, ports: {Na: VA, Nc: VH}
name: R1, type: Resistor, value: R1, ports: {N1: VH, N2: GND}
]
extrainfo:The circuit diagram (c) represents a diode-resistor combination under reverse bias, where the diode is off, and the circuit behaves as an open circuit with no current flow.
image_name:(d)
description:The graph labeled (d) is an I/V characteristic curve, representing the relationship between the current \( I_A \) and the voltage \( V_A \) across a diode-resistor series combination.

1. **Type of Graph and Function:**
- The graph is a linear plot of current versus voltage, typically used to illustrate the behavior of electronic components like diodes and resistors.

2. **Axes Labels and Units:**
- The horizontal axis represents the voltage \( V_A \), while the vertical axis represents the current \( I_A \). The scale is linear for both axes.

3. **Overall Behavior and Trends:**
- The graph shows a piecewise linear behavior. For \( V_A > 0 \), the line has a positive slope, indicating that the diode is forward-biased and conducts current. The slope of the line is \( \frac{1}{R_1} \), where \( R_1 \) is the resistance in series with the diode.
- For \( V_A < 0 \), the current \( I_A \) remains zero, indicating that the diode is reverse-biased and does not conduct.

4. **Key Features and Technical Details:**
- The graph has a clear transition point at \( V_A = 0 \), where the behavior changes from non-conducting (reverse bias) to conducting (forward bias).
- The slope \( \frac{1}{R_1} \) signifies the inverse of the resistance, showing the linear relationship between \( V_A \) and \( I_A \) in the forward-biased region.

5. **Annotations and Specific Data Points:**
- The graph includes a dotted line indicating the slope \( \frac{1}{R_1} \) for the forward-biased region, emphasizing the linear relationship in this part of the graph.
image_name:(e)
description:
[
name: VA, type: VoltageSource, value: VA, ports: {Np: VA, Nn: GND}
name: D1, type: Diode, ports: {Na: VA, Nc: VH}
name: R1, type: Resistor, value: R1, ports: {N1: VH, N2: GND}
]
extrainfo:The circuit consists of a voltage source VA connected in series with a diode D1 and a resistor R1. The diode is forward-biased when VA is positive, allowing current IA to flow through the circuit. The resistor R1 is connected between node VH and ground.

Figure 3.7 (a) Diode-resistor series combination, (b) equivalent circuit under forward bias, (c) equivalent circuit under reverse bias, (d) I/V characteristic, (e) equivalent circuit if $D_{1}$ is on.

Solution We surmise that, if $V_{A}>0$, the diode is on [Fig. 3.7(b)] and $I_{A}=V_{A} / R_{1}$ because $V_{D 1}=0$ for an ideal diode. On the other hand, if $V_{A}<0, D_{1}$ is probably off [Fig. 3.7(c)] and $I_{D}=0$. Figure 3.7(d) plots the resulting I/V characteristic.

The above observations are based on guesswork. Let us study the circuit more rigorously. We begin with $V_{A}<0$, postulating that the diode is off. To confirm the validity of this guess, let us assume $D_{1}$ is on and see if we reach a conflicting result. If $D_{1}$ is on, the circuit is reduced to that in Fig. 3.7(e), and if $V_{A}$ is negative, so is $I_{A}$; i.e., the actual current flows from right to left. But this implies that $D_{1}$ carries a current from its cathode to its anode, violating the definition of the diode. Thus, for $V_{A}<0, D_{1}$ remains off and $I_{A}=0$.

As $V_{A}$ rises above zero, it tends to forward bias the diode. Does $D_{1}$ turn on for any $V_{A}>0$ or does $R_{1}$ shift the turn-on point? We again invoke proof by contradiction. Suppose for some $V_{A}>0, D_{1}$ is still off, behaving as an open circuit and yielding $I_{A}=0$. The voltage drop across $R_{1}$ is therefore equal to zero, suggesting that $V_{D 1}=V_{A}$ and hence $I_{D 1}=\infty$ and contradicting the original assumption. In other words, $D_{1}$ turns on for any $V_{A}>0$.

Exercise Repeat the above analysis if the terminals of the diode are swapped.

The above example leads to two important points. First, the series combination of $D_{1}$ and $R_{1}$ acts as an open for negative voltages and as a resistor of value $R_{1}$ for positive voltages. Second, in the analysis of circuits, we can assume an arbitrary state (on or off) for each diode and proceed with the computation of voltages and currents; if the assumptions are incorrect, the final result contradicts the original assumptions. Of course, it is helpful to first examine the circuit carefully and make an intuitive guess.

Example Why are we interested in I/V characteristics rather than V/I characteristics?

Solution In the analysis of circuits, we often prefer to consider the voltage to be the "cause" and the current, the "effect." This is because in typical circuits, voltage polarities can be predicted more readily and intuitively than current polarities. Also, devices such as transistors fundamentally produce current in response to voltage.

Exercise Plot the V/I characteristic of an ideal diode.

Solution If $V_{A}=+3 \mathrm{~V}$, and $V_{B}=0$, then we surmise that $D_{1}$ is forward-biased and $D_{2}$, reversebiased. Thus, $V_{\text {out }}=V_{A}=+3 \mathrm{~V}$. If uncertain, we can assume both $D_{1}$ and $D_{2}$ are
forward-biased, immediately facing a conflict: $D_{1}$ enforces a voltage of +3 V at the output whereas $D_{2}$ shorts $V_{\text {out }}$ to $V_{B}=0$. This assumption is therefore incorrect.
image_name:Figure 3.8 OR gate realized by diodes
description:
[
name: D1, type: Diode, ports: {Na: VA, Nc: Vout}
name: D2, type: Diode, ports: {Na: VB, Nc: Vout}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is an OR gate realized with diodes. It outputs the higher of the two input voltages VA or VB to Vout. RL is connected between Vout and ground, providing a path for current when either diode is forward-biased.

Figure 3.8 OR gate realized by diodes.

The symmetry of the circuit with respect to $V_{A}$ and $V_{B}$ suggests that $V_{\text {out }}=V_{B}=+3 \mathrm{~V}$ if $V_{A}=0$ and $V_{B}=+3 \mathrm{~V}$. The circuit operates as a logical OR gate and was in fact used in early digital computers.

Exercise Construct a three-input OR gate.

Is an ideal diode on or off if $V_{D}=0$ ?

Solution An ideal diode experiencing a zero voltage must carry a zero current (why?). However, this does not mean it acts as an open circuit. After all, a piece of wire experiencing a zero voltage behaves similarly. Thus, the state of an ideal diode with $V_{D}=0$ is somewhat arbitrary and ambiguous. In practice, we consider slightly positive or negative voltages to determine the response of a diode circuit.

Exercise Repeat the above example if a $1-\Omega$ resistor is placed in series with the diode.

Input/Output Characteristics Electronic circuits process an input and generate a corresponding output. It is therefore instructive to construct the input/output characteristics of a circuit by varying the input across an allowable range and plotting the resulting output.

As an example, consider the circuit depicted in Fig. 3.9(a), where the output is defined as the voltage across $D_{1}$. If $V_{i n}<0, D_{1}$ is reverse biased, reducing the circuit to that in Fig. 3.9(b). Since no current flows through $R_{1}$, we have $V_{\text {out }}=V_{\text {in }}$. If $V_{\text {in }}>0$, then $D_{1}$ is forward biased, shorting the output and forcing $V_{\text {out }}=0$ [Fig. 3.9(c)]. Figure 3.9(d) illustrates the overall input/output characteristic.

### 3.1.3 Application Examples

Recall from Fig. 3.2 that we arrived at the concept of the ideal diode as a means of converting $x(t)$ to $y(t)$. Let us now design a circuit that performs this function. We may naturally construct the circuit as shown in Fig. 3.10(a). Unfortunately, however, the cathode of the diode is "floating," the output current is always equal to zero, and the state of the diode is ambiguous. We therefore modify the circuit as depicted in Fig. 3.10(b) and analyze
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: Vout}
name: D1, type: Diode, ports: {Na: Vout, Nc: GND}
]
extrainfo:The circuit in Figure 3.10(a) is a simple diode rectifier circuit. It consists of a voltage source Vin, a resistor R1, and a diode D1. The diode is used to allow current to flow in one direction, rectifying the input signal. The output is taken across the diode.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: Vout}
name: SW, type: Switch, ports: {N1: Vout, N2: GND}
]
extrainfo:This circuit diagram (b) represents a rectifier circuit with a switch (SW) replacing the diode from diagram (a). The circuit is designed to handle both positive and negative input voltages, with the switch controlling the output based on the input polarity. The output is taken across the switch and ground, with a resistor R1 connected in series with the voltage source Vin.
image_name:(c)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: Vout}
name: SW, type: Switch, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit in Fig. 3.10(c) represents a rectifier circuit with a switch used for positive input voltages. The switch is closed when Vin > 0, allowing current to flow through R1 to Vout.
image_name:(d)
description:The graph labeled (d) is an input/output characteristic graph for a diode rectifier circuit.

1. **Type of Graph and Function:**
- This is a characteristic curve graph, showing the relationship between the input voltage \( V_{in} \) and the output voltage \( V_{out} \).

2. **Axes Labels and Units:**
- The horizontal axis represents the input voltage \( V_{in} \), while the vertical axis represents the output voltage \( V_{out} \). Units are typically in volts, though specific units are not marked.

3. **Overall Behavior and Trends:**
- The graph shows a piecewise linear relationship. For negative values of \( V_{in} \), \( V_{out} \) is zero, indicating that the diode blocks negative input voltages. For positive values of \( V_{in} \), \( V_{out} \) increases linearly with \( V_{in} \), indicating that the diode conducts and allows the input voltage to pass through.

4. **Key Features and Technical Details:**
- The graph has a distinct "knee" at the origin (0,0), where the behavior changes from blocking to conducting.
- The slope of the line for positive \( V_{in} \) is 1, indicating a 1:1 ratio of \( V_{in} \) to \( V_{out} \) in the conducting region.

5. **Annotations and Specific Data Points:**
- The graph includes a dashed line at the origin marking the transition from non-conducting to conducting states.
- There are no specific numerical values or additional annotations provided on the graph.

Figure 3.9 (a) Resistor-diode circuit, (b) equivalent circuit for negative input, (c) equivalent circuit for positive input, (d) input/output characteristic.
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: D1, type: Diode, ports: {Na: Vin, Nc: Vout}
]
extrainfo:The circuit in Figure 3.9 (a) is a simple diode rectifier circuit. It consists of a voltage source Vin, a diode D1, and the output is taken across the diode. The diode allows current to flow only when the input voltage is positive, effectively rectifying the input signal.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: D1, type: Diode, ports: {Na: Vin, Nc: Vout}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a simple rectifier circuit. The diode D1 allows current to pass only when Vin is positive, rectifying the input signal. Resistor R1 is connected to the ground, providing a path for the current when the diode is forward-biased.
image_name:(c)
description:The graph labeled as Figure 3.10(c) represents the input and output waveforms of a diode operating as a rectifier. This is a time-domain waveform graph.

1. **Axes Labels and Units:**
- The horizontal axis is labeled as time, denoted as \( t \), with specific points marked as \( 0 \), \( \frac{T}{2} \), \( T \), \( \frac{3T}{2} \), and \( 2T \), indicating periodic intervals of the waveform.
- The vertical axis represents voltage, showing the input \( V_{in} \) and output \( V_{out} \) voltages.

2. **Overall Behavior and Trends:**
- The input waveform \( V_{in} \) is a sinusoidal wave, which oscillates above and below the time axis, representing alternating positive and negative half cycles.
- The output waveform \( V_{out} \) displays rectified half cycles, where only the positive half cycles of the input waveform are present, indicating that the diode conducts only during these periods.
- The negative half cycles of the input are clipped, resulting in zero output during these intervals.

3. **Key Features and Technical Details:**
- The rectification process results in the output waveform having a series of positive half cycles, each corresponding to the positive half of the input sinusoidal wave.
- The waveform is periodic with a period \( T \), matching the input waveform's frequency.

4. **Annotations and Specific Data Points:**
- The graph does not provide specific numerical values but shows the transition from input to output, highlighting the rectification process by the diode.
- The term 'Rectified Half Cycles' is annotated on the graph to indicate the nature of the output waveform.

This graph effectively illustrates the basic operation of a diode rectifier, demonstrating how it converts an AC input signal into a unidirectional output signal by allowing current to pass only during the positive half cycles.
image_name:(d)
description:The graph labeled (d) is an input/output characteristic curve for a diode operating as a rectifier. This graph is a plot of the output voltage \( V_{out} \) against the input voltage \( V_{in} \).

1. **Type of Graph and Function:**
- This is a linear graph representing the relationship between input and output voltages in a rectifying diode circuit.

2. **Axes Labels and Units:**
- The horizontal axis represents the input voltage \( V_{in} \), and the vertical axis represents the output voltage \( V_{out} \). Units are not specified but are typically in volts.

3. **Overall Behavior and Trends:**
- The graph shows a linear relationship in the conducting region, where \( V_{out} \) increases proportionally with \( V_{in} \). This indicates a 1:1 ratio of \( V_{in} \) to \( V_{out} \) when the diode is forward-biased.
- For negative input voltages, \( V_{out} \) remains at zero, indicating the diode is not conducting and effectively blocking the negative half of the cycle.

4. **Key Features and Technical Details:**
- The graph has a distinct transition point at the origin, marked by a dashed line, which indicates the change from non-conducting to conducting states.
- There are no specific numerical values or additional annotations provided on the graph.

5. **Annotations and Specific Data Points:**
- The dashed line at the origin highlights the threshold where the diode begins to conduct, transitioning from zero output to a linear increase in \( V_{out} \) with increasing \( V_{in} \).

Figure 3.10 (a) A diode operating as a rectifier, (b) complete rectifier, (c) input and output waveforms, (d) input/output characteristic.
its response to a sinusoidal input [Fig. 3.10(c)]. Since $R_{1}$ has a tendency to maintain the cathode of $D_{1}$ near zero, as $V_{\text {in }}$ rises, $D_{1}$ is forward biased, shorting the output to the input. This state holds for the positive half cycle. When $V_{i n}$ falls below zero, $D_{1}$ turns off and $R_{1}$ ensures that $V_{\text {out }}=0$ because $I_{D} R_{1}=0 .{ }^{5}$ The circuit of Fig. 3.10(b) is called a "rectifier."

It is instructive to plot the input/output characteristic of the circuit as well. Noting that if $V_{\text {in }}<0, D_{1}$ is off and $V_{\text {out }}=0$, and if $V_{\text {in }}>0, D_{1}$ is on and $V_{\text {out }}=V_{\text {in }}$, we obtain the behavior shown in Fig. 3.10(d). The rectifier is a nonlinear circuit because if $V_{\text {in }} \rightarrow-V_{\text {in }}$ then $V_{\text {out }} \nrightarrow-V_{\text {out }}$.

Is it a coincidence that the characteristics in Figs. 3.7(d) and 3.10(d) look similar?

Solution No, we recognize that the output voltage in Fig. 3.10(b) is simply equal to $I_{A} R_{1}$ in Fig. 3.7(a). Thus, the two plots differ by only a scaling factor equal to $R_{1}$.

Exercise $\quad$ Construct the characteristic if the terminals of $D_{1}$ are swapped.

We now determine the time average (dc value) of the output waveform in Fig. 3.10(c) to arrive at another interesting application. Suppose $V_{i n}=V_{p} \sin \omega t$, where $\omega=2 \pi / T$ denotes the frequency in radians per second and $T$ the period. Then, in the first cycle after $t=0$, we have

$$
\begin{align*}
V_{\text {out }} & =V_{p} \sin \omega t \text { for } 0 \leq t \leq \frac{T}{2}  \tag{3.3}\\
& =0 \quad \text { for } \frac{T}{2} \leq t \leq T \tag{3.4}
\end{align*}
$$

To compute the average, we obtain the area under $V_{\text {out }}$ and normalize the result to the period:

$$
\begin{align*}
V_{\text {out }, \text { avg }} & =\frac{1}{T} \int_{0}^{T} V_{\text {out }}(t) d t  \tag{3.5}\\
& =\frac{1}{T} \int_{0}^{T / 2} V_{p} \sin \omega t d t  \tag{3.6}\\
& =\frac{1}{T} \cdot \frac{V_{p}}{\omega}[-\cos \omega t]_{0}^{T / 2}  \tag{3.7}\\
& =\frac{V_{p}}{\pi} \tag{3.8}
\end{align*}
$$

Thus, the average is proportional to $V_{p}$, an expected result because a larger input amplitude yields a greater area under the rectified half cycles.

The above observation reveals that the average value of a rectified output can serve as a measure of the "strength" (amplitude) of the input. That is, a rectifier can operate as a "signal strength indicator." For example, since cellphones receive varying levels of signal depending on the user's location and environment, they require an indicator to determine how much the signal must be amplified.

Example A cellphone receives a $1.8-\mathrm{GHz}$ signal with a peak amplitude ranging from $2 \mu \mathrm{~V}$ to <br> 3.9 10 mV . If the signal is applied to a rectifier, what is the corresponding range of the output average?

Solution The rectified output exhibits an average value ranging from $2 \mu \mathrm{~V} /(\pi)=0.637 \mu \mathrm{~V}$ to $10 \mathrm{mV} /(\pi)=3.18 \mathrm{mV}$.

Do the above results change if a $1-\Omega$ resistor is placed in series with the diode?

In our effort toward understanding the role of diodes, we examine another circuit that will eventually (in Section 3.5.3) lead to some important applications. First, consider the topology in Fig. 3.11(a), where a 1-V battery is placed in series with an ideal diode. How does this circuit behave? If $V_{1}<0$, the cathode voltage is higher than the anode voltage, placing $D_{1}$ in reverse bias. Even if $V_{1}$ is slightly greater than zero, e.g., equal to 0.9 V , the anode is not positive enough to forward bias $D_{1}$. Thus, $V_{1}$ must approach +1 V for $D_{1}$
image_name:(a)
description:The graph associated with Fig. 3.11(a) illustrates the current-voltage (I-V) characteristics of a circuit consisting of a 1-V battery in series with an ideal diode.

1. **Type of Graph and Function**: This is an I-V characteristic graph, which shows the relationship between the voltage across the diode-battery combination and the current flowing through it.

2. **Axes Labels and Units**:
- The horizontal axis represents the input voltage \( V_1 \) in volts (V).
- The vertical axis represents the current \( I_1 \) in amperes (A).

3. **Overall Behavior and Trends**:
- The graph shows no current flow (\( I_1 = 0 \)) for \( V_1 < 1 \) V, indicating that the diode is reverse-biased or not sufficiently forward-biased.
- At \( V_1 = 1 \) V, the current \( I_1 \) sharply increases, indicating that the diode becomes forward-biased and allows current to flow.

4. **Key Features and Technical Details**:
- The diode remains off (no current) until the input voltage \( V_1 \) reaches +1 V. This is the threshold voltage where the diode starts conducting.
- The sharp increase in current at \( V_1 = 1 \) V suggests ideal diode behavior, where the diode turns on abruptly.

5. **Annotations and Specific Data Points**:
- The graph is marked with a significant point at \( V_1 = +1 \) V, where the current begins to flow. This is a critical transition point for the diode's operation in the circuit.

(a)
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: Vout}
name: D1, type: Diode, ports: {Na: Vout, Nc: GND}
]
extrainfo:The circuit diagram represents a diode-resistor network with an input voltage source. The diode conducts when Vin exceeds 1 V, clamping the output voltage. The accompanying graphs show the input and output waveforms, and the I-V characteristic illustrates the diode's threshold behavior at 1 V.
image_name:(b)
description:The graph in Figure 3.11(b) represents the I/V characteristic of a resistor-diode circuit. This circuit includes a diode (D1) connected in series with a resistor (R1) and a voltage source (Vin). The graph has two main components: a time-domain waveform and a Vout versus Vin plot.

1. **Time-Domain Waveform**:
- The top part of the graph shows the input voltage (Vin) as a sinusoidal waveform over time (t). The waveform oscillates above and below zero, indicating an AC signal.
- The bottom part displays the output voltage (Vout) waveform, which is similar in shape and phase to the input waveform, but with the negative half-cycles clipped. This indicates that the diode is conducting only during the positive half-cycles, acting as a half-wave rectifier.

2. **Vout vs. Vin Plot**:
- The plot on the right shows the relationship between the output voltage (Vout) and the input voltage (Vin).
- The x-axis represents Vin, and the y-axis represents Vout. The graph indicates that Vout remains zero when Vin is below the diode's threshold voltage (1 V), as the diode is off.
- Once Vin exceeds 1 V, Vout increases linearly with Vin, indicating the diode is conducting, and the circuit behaves like a linear resistor for positive voltages.

3. **Key Features and Annotations**:
- The critical transition point is at Vin = 1 V, where the diode starts conducting, marked by a change in the slope of the Vout vs. Vin plot.
- The dashed line at 1 V on the Vout vs. Vin plot highlights the threshold voltage, a significant point for the diode's operation.

Overall, this graph illustrates the behavior of a diode in a resistor-diode circuit, showing its rectifying effect and threshold voltage characteristics.
image_name:(c)
description:The diagram consists of three main components: a circuit schematic, time-domain waveforms, and an I/V characteristic plot.

1. **Circuit Schematic**:
- The circuit includes a diode \( D_1 \) in series with a resistor \( R_1 \), connected to an input voltage source \( V_{in} \). The output voltage \( V_{out} \) is measured across the diode. The diode is oriented to conduct when the input voltage is positive.

2. **Time-Domain Waveforms**:
- The waveforms depict \( V_{in} \) and \( V_{out} \) as functions of time \( t \). The input voltage \( V_{in} \) is a sinusoidal waveform, alternating above and below the zero voltage line.
- The output voltage \( V_{out} \) shows a clipped waveform, where the negative half-cycles are suppressed due to the diode's rectifying action, demonstrating half-wave rectification.

3. **I/V Characteristic Plot**:
- This plot shows the relationship between \( V_{out} \) (y-axis) and \( V_{in} \) (x-axis). The plot is a piecewise linear graph with a sharp transition at \( V_{in} = 1 \) V, indicating the diode's threshold voltage.
- For \( V_{in} < 1 \) V, \( V_{out} \) remains at zero, showing the diode is off. Once \( V_{in} \) exceeds 1 V, \( V_{out} \) increases linearly with \( V_{in} \), indicating the diode is conducting.

Overall, the diagram illustrates the behavior of a diode in a rectifying circuit, showing how it allows current flow only when the input voltage exceeds a certain threshold, effectively clipping the negative portion of the input waveform.

(b)
image_name:(b)
description:The function graph in diagram (b) illustrates the behavior of a diode-resistor circuit with an added series battery. The graph type is a voltage transfer characteristic plot, which shows the relationship between the input voltage \( V_{in} \) and the output voltage \( V_{out} \).

**Axes Labels and Units:**
- The horizontal axis represents the input voltage \( V_{in} \) in volts.
- The vertical axis represents the output voltage \( V_{out} \) in volts.

**Overall Behavior and Trends:**
- For \( V_{in} < 0 \), the diode \( D_1 \) is off, and the output voltage \( V_{out} \) follows the input voltage \( V_{out} = V_{in} \). This is depicted by the linear segment along the line \( V_{out} = V_{in} \).
- For \( V_{in} > 0 \), the diode \( D_1 \) conducts, behaving like a short circuit, and the output voltage \( V_{out} \) is clamped to 0 volts regardless of \( V_{in} \). This is shown by the horizontal line at \( V_{out} = 0 \).

**Key Features and Technical Details:**
- The graph shows a clear transition at \( V_{in} = 0 \), where the behavior of \( V_{out} \) changes from following \( V_{in} \) to being clamped at 0 volts.
- The presence of a series battery shifts the characteristic curve by 1 V to the right, indicating that the diode requires a forward bias of 1 V to conduct.

**Annotations and Specific Data Points:**
- The graph includes a dashed line at \( +1 \) V, representing the threshold voltage needed for the diode to turn on.
- The graph is annotated with reference lines at \( +1 \) V on both axes to indicate the shift caused by the series battery.

(c)

Figure 3.11 (a) Diode-battery circuit, (b) resistor-diode circuit, (c) addition of series battery to (b).
to turn on. Shown in Fig. 3.11(a), the I/V characteristic of the diode-battery combination resembles that of a diode, but shifted to the right by 1 V .

Now, let us examine the circuit in Fig. 3.11(b). Here, for $V_{\text {in }}<0, D_{1}$ remains off, yielding $V_{\text {out }}=V_{\text {in }}$. For $V_{\text {in }}>0, D_{1}$ acts a short, and $V_{\text {out }}=0$. The circuit therefore does not allow the output to exceed zero, as illustrated in the output waveform and the input/output characteristic. But suppose we seek a circuit that must not allow the output to exceed +1 V (rather than zero). How should the circuit of Fig. 3.11(b) be modified? In this case, $D_{1}$ must turn on only when $V_{\text {out }}$ approaches +1 V , implying that a $1-\mathrm{V}$ battery must be inserted in series with the diode. Depicted in Fig.3.11(c), the modification indeed guarantees $V_{\text {out }} \leq+1 \mathrm{~V}$ for any input level. We say the circuit "clips" or "limits" at +1 V . "Limiters" prove useful in many applications and are described in Section 3.5.3.

Example 3.10

Solution

Sketch the time average of $V_{\text {out }}$ in Fig. 3.11(c) for a sinusoidal input as the battery voltage, $V_{B}$, varies from $-\infty$ to $+\infty$.

If $V_{B}$ is very negative, $D_{1}$ is always on because $V_{i n} \geq-V_{p}$. In this case, the output average is equal to $V_{B}$ [Fig. 3.12(a)]. For $-V_{p}<V_{B}<0, D_{1}$ turns off at some point in the negative half cycle and remains off in the positive half cycle, yielding an average greater than $-V_{p}$ but less than $V_{B}$. For $V_{B}=0$, the average reaches $-V_{p} /(\pi)$. Finally, for $V_{B} \geq V_{p}$, no limiting occurs and the average is equal to zero. Figure 3.12(b) sketches this behavior.
image_name:Figure 3.12(a)
description:The graph in Figure 3.12(a) consists of four subplots, each representing different scenarios of the output voltage \( V_{out} \) based on varying conditions of \( V_B \) relative to \( V_p \), the peak voltage. These subplots illustrate how the input voltage \( V_{in} \) is transformed by the circuit.

1. **Top Left Subplot (\( V_B < -V_p \))**:
- **Type of Graph**: Time-domain waveform.
- **Axes**: The horizontal axis represents time \( t \), and the vertical axis represents voltage.
- **Behavior**: The input voltage \( V_{in} \) is shown as a sinusoidal wave. The output voltage \( V_{out} \) is constant and equal to \( V_B \), represented by a flat line at the \( V_B \) level, indicating that the diode is always on.

2. **Top Right Subplot (\( -V_p < V_B < 0 \))**:
- **Type of Graph**: Time-domain waveform.
- **Axes**: The horizontal axis represents time \( t \), and the vertical axis represents voltage.
- **Behavior**: The input voltage \( V_{in} \) is sinusoidal. The output voltage \( V_{out} \) follows the input during the negative half-cycle but is clipped to \( V_B \) during the positive half-cycle. This indicates that the diode turns off at some point in the negative half-cycle.

3. **Bottom Left Subplot (\( V_B = 0 \))**:
- **Type of Graph**: Time-domain waveform.
- **Axes**: The horizontal axis represents time \( t \), and the vertical axis represents voltage.
- **Behavior**: The input voltage \( V_{in} \) is sinusoidal. The output voltage \( V_{out} \) is a rectified waveform, where only the negative half-cycles are visible. The average output is \(-V_p/\pi\).

4. **Bottom Right Subplot (\( V_B > V_p \))**:
- **Type of Graph**: Time-domain waveform.
- **Axes**: The horizontal axis represents time \( t \), and the vertical axis represents voltage.
- **Behavior**: The input voltage \( V_{in} \) is sinusoidal. The output voltage \( V_{out} \) mirrors the input voltage, indicating no clipping or limiting occurs, and the average output is zero.

Overall, these subplots demonstrate how the output voltage \( V_{out} \) changes based on the bias voltage \( V_B \), affecting whether the diode conducts or not during different parts of the input cycle.
image_name:Figure 3.12(b)
description:Figure 3.12(b) is a set of four time-domain waveforms illustrating different scenarios of diode behavior based on the bias voltage \( V_B \) relative to the peak voltage \( V_p \). Each graph has the horizontal axis labeled as time \( t \) and shows both the input voltage \( V_{in} \) and the output voltage \( V_{out} \).

1. **Top Left Graph (\( V_B < -V_p \)):**
- The input voltage \( V_{in} \) is a sinusoidal waveform oscillating above and below zero.
- The output voltage \( V_{out} \) is constant at \( V_B \), as indicated by a flat line, since the diode is always on due to \( V_{in} \) being greater than \(-V_p\).

2. **Top Right Graph (\(-V_p < V_B < 0\)):**
- The input voltage \( V_{in} \) is again sinusoidal.
- The output voltage \( V_{out} \) follows \( V_{in} \) until it drops below \( V_B \), at which point it remains at \( V_B \) until \( V_{in} \) rises above \( V_B \) again. This results in a waveform that is clipped at \( V_B \) in the negative half-cycle.

3. **Bottom Left Graph (\( V_B = 0 \)):**
- The input voltage \( V_{in} \) is sinusoidal.
- The output voltage \( V_{out} \) is clipped at zero during the negative half-cycle, producing a half-wave rectified waveform.

4. **Bottom Right Graph (\( V_B > V_p \)):**
- The input voltage \( V_{in} \) is sinusoidal.
- The output voltage \( V_{out} \) follows \( V_{in} \) entirely, as \( V_B \) is high enough that no clipping occurs. The waveform is identical to \( V_{in} \), indicating that the diode does not affect the signal.

These graphs demonstrate how varying \( V_B \) affects the output waveform by altering the diode's conduction state, illustrating the clipping and rectification effects in different scenarios.
image_name:V_B = 0
description:The graph titled "V_B = 0" is a time-domain waveform illustrating the behavior of an output voltage \( V_{out} \) in response to an input voltage \( V_{in} \) under different conditions of \( V_B \).

1. **Type of Graph and Function:**
- This is a time-domain waveform graph showing the relationship between input and output voltages over time.

2. **Axes Labels and Units:**
- The horizontal axis represents time \( t \).
- The vertical axis represents voltage, with specific markings for \( V_{in} \), \( V_{B} \), and \( V_{p} \).
- No specific units are given, but it is implied that the voltages are in volts.

3. **Overall Behavior and Trends:**
- The graph consists of four different scenarios, each showing how \( V_{out} \) behaves under varying conditions of \( V_B \).
- For \( V_B < -V_p \): The output voltage \( V_{out} \) remains constant at \( V_B \), indicating that \( V_{out} = V_B \).
- For \( -V_p < V_B < 0 \): \( V_{out} \) follows \( V_{in} \) in the negative half-cycle but is clipped at \( V_B \), creating a flat region at \( V_B \) during the positive half-cycle.
- For \( V_B = 0 \): \( V_{out} \) is a rectified waveform, following the negative half-cycles of \( V_{in} \) and remaining at zero during positive half-cycles.
- For \( V_B > V_p \): \( V_{out} \) follows \( V_{in} \) completely, as no clipping occurs.

4. **Key Features and Technical Details:**
- The graph highlights the clipping effect of \( V_B \) on the input waveform, showing how \( V_{out} \) changes based on the level of \( V_B \) relative to \( V_p \).
- The behavior transitions from constant output to partial clipping, full rectification, and finally, no clipping, illustrating the diode's function in the circuit.

5. **Annotations and Specific Data Points:**
- Each scenario is clearly labeled with the condition of \( V_B \) relative to \( V_p \).
- The graph provides a visual representation of how the diode circuit modulates the waveform based on the biasing voltage \( V_B \).
image_name:V_B > V_p
description:The graph consists of four time-domain waveforms illustrating the behavior of an output voltage \( V_{out} \) relative to an input voltage \( V_{in} \) under different conditions of \( V_B \) and \( V_p \). Each waveform is plotted with time \( t \) on the horizontal axis and voltage on the vertical axis.

1. **Top Left Quadrant \( V_B < -V_p \):**
- **Axes:** Time \( t \) (horizontal), Voltage (vertical).
- **Input \( V_{in} \):** A sinusoidal waveform fluctuating between positive and negative peaks.
- **Output \( V_{out} \):** A constant line at \( V_B \), indicating that the output voltage is clamped to \( V_B \) because \( V_{in} \) never exceeds \( V_B \).

2. **Top Right Quadrant \( -V_p < V_B < 0 \):**
- **Axes:** Time \( t \) (horizontal), Voltage (vertical).
- **Input \( V_{in} \):** A sinusoidal waveform.
- **Output \( V_{out} \):** The waveform follows \( V_{in} \) until it reaches \( V_B \) in the negative cycle, where it flattens, and follows \( V_{in} \) in the positive cycle.

3. **Bottom Left Quadrant \( V_B = 0 \):**
- **Axes:** Time \( t \) (horizontal), Voltage (vertical).
- **Input \( V_{in} \):** A sinusoidal waveform.
- **Output \( V_{out} \):** The waveform is clipped at zero during the negative cycle, creating half-wave rectification.

4. **Bottom Right Quadrant \( +V_p < V_B \):**
- **Axes:** Time \( t \) (horizontal), Voltage (vertical).
- **Input \( V_{in} \):** A sinusoidal waveform.
- **Output \( V_{out} \):** The waveform is unaltered, following \( V_{in} \) entirely, as \( V_B \) does not limit the signal.

Overall, the diagrams illustrate how different values of \( V_B \) affect the limiting behavior of \( V_{out} \) relative to \( V_{in} \), showcasing various clipping and rectification effects.

(a)
image_name:Figure 3.12
description:The graph in Figure 3.12 is a plot depicting the relationship between the output voltage \( V_{out} \) and the input voltage \( V_B \). The axes are labeled with \( V_{out} \) on the vertical axis and \( V_B \) on the horizontal axis. The graph is plotted in a standard Cartesian coordinate system.

Axes Labels and Units:
- **Vertical Axis:** \( V_{out} \), representing the output voltage.
- **Horizontal Axis:** \( V_B \), representing the input voltage.

Overall Behavior and Trends:
- The graph shows a nonlinear relationship between \( V_{out} \) and \( V_B \).
- As \( V_B \) increases from negative to positive values, \( V_{out} \) starts from a negative value and gradually increases.

Key Features and Technical Details:
- The curve begins at a point labeled \(-V_p\) on the vertical axis, indicating the starting point of \( V_{out} \).
- There is a marked point at \(-\frac{V_p}{\pi}\) on the horizontal axis, showing a significant point in the curve's progression.
- The curve appears to asymptotically approach a linear region as \( V_B \) becomes positive.
- The curve crosses the origin, suggesting that \( V_{out} \) becomes zero when \( V_B \) is zero.

Annotations and Specific Data Points:
- The graph is annotated with a specific slope or change in behavior at the point \(-\frac{V_p}{\pi}\).
- The curve passes through the origin, which is a critical point where \( V_{out} = 0 \) when \( V_B = 0 \).

This graph illustrates how the output voltage \( V_{out} \) changes in response to varying input voltage \( V_B \), with specific reference points and nonlinear behavior indicating a complex relationship between the two variables.

(b)

Figure 3.12

Exercise Repeat the above example if the terminals of the diode are swapped.
Example
3.11 Is the circuit of Fig. 3.11(b) a rectifier?

Solution Yes, indeed. The circuit passes only negative cycles to the output, producing a negative average.

Exercise How should the circuit of Fig.3.11(b) be modified to pass only positive cycles to the output?

## 3.3 ADDITIONAL EXAMPLES*

Example In the circuit of Fig. 3.15, $D_{1}$ and $D_{2}$ have different cross section areas but are otherwise 3.13 identical. Determine the current flowing through each diode.

Figure 3.15 Diode circuit.
image_name:Figure 3.15 Diode circuit
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: Vi, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vi, N2: X1}
name: D1, type: Diode, ports: {Na: X1, Nc: GND}
name: D2, type: Diode, ports: {Na: X1, Nc: GND}
]
extrainfo:The circuit consists of a voltage source V1 connected to a resistor R1, which is in series with two parallel diodes D1 and D2. The node X1 connects R1 to the anodes of both diodes, with the cathodes of the diodes connected to ground.

Solution In this case, we must resort to the exponential equation because the ideal and constantvoltage models do not include the device area. We have

$$
\begin{equation*}
I_{i n}=I_{D 1}+I_{D 2} \tag{3.12}
\end{equation*}
$$

We also equate the voltages across $D_{1}$ and $D_{2}$ :

$$
\begin{equation*}
V_{T} \ln \frac{I_{D 1}}{I_{S 1}}=V_{T} \ln \frac{I_{D 2}}{I_{S 2}} \tag{3.13}
\end{equation*}
$$

that is,

$$
\begin{equation*}
\frac{I_{D 1}}{I_{S 1}}=\frac{I_{D 2}}{I_{S 2}} \tag{3.14}
\end{equation*}
$$

Solving (3.13) and (3.15) together yields

$$
\begin{align*}
& I_{D 1}=\frac{I_{i n}}{1+\frac{I_{S 2}}{I_{S 1}}}  \tag{3.15}\\
& I_{D 2}=\frac{I_{i n}}{1+\frac{I_{S 1}}{I_{S 2}}} \tag{3.16}
\end{align*}
$$

As expected, $I_{D 1}=I_{D 2}=I_{i n} / 2$ if $I_{S 1}=I_{S 2}$.

Exercise For the circuit of Fig. 3.15, calculate $V_{D}$ is terms of $I_{i n}, I_{S 1}$, and $I_{S 2}$.
*This section can be skipped in a first reading.

Using the constant-voltage model, plot the input/output characteristics of the circuit depicted in Fig. 3.16(a). Note that a diode about to turn on carries zero current but sustains $V_{D, \text { on }}$.
image_name:Figure 3.16 (a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: Vout}
name: R2, type: Resistor, value: R2, ports: {N1: Vout, N2: GND}
name: D1, type: Diode, ports: {Na: Vout, Nc: GND}
]
extrainfo:The circuit is a basic diode-resistor network with input at Vin and output at Vout. R1 is connected between Vin and Vout, R2 is connected between Vout and GND, and D1 is a diode with anode at Vout and cathode at GND.

(a)
image_name:(a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: Vout}
name: R2, type: Resistor, value: R2, ports: {N1: Vout, N2: GND}
name: D1, type: Diode, ports: {Na: Vout, Nc: GND}
]
extrainfo:The circuit is a basic diode-resistor network with input at Vin and output at Vout. R1 is connected between Vin and Vout, R2 is connected between Vout and GND, and D1 is a diode with anode at Vout and cathode at GND.

(b)
image_name:(c)
description:The graph in Figure 3.16(c) is an input/output characteristic plot of a diode-resistor network. It is a two-dimensional graph with the horizontal axis labeled as $V_{in}$, representing the input voltage, and the vertical axis labeled as $V_{out}$, representing the output voltage. Both axes are likely in volts, though the units are not explicitly stated.

Type of Graph:
This is a characteristic curve, typically used in electronics to illustrate how output voltage varies with input voltage in a specific circuit configuration.

Axes Labels and Units:
- **Horizontal Axis ($V_{in}$):** Represents the input voltage to the circuit.
- **Vertical Axis ($V_{out}$):** Represents the output voltage from the circuit.

Overall Behavior and Trends:
- **Initial Linear Region:** For small values of $V_{in}$, the output voltage $V_{out}$ increases linearly with $V_{in}$, following the slope determined by the ratio $\frac{R_2}{R_1 + R_2}$. This indicates that the diode $D_1$ is off, and the circuit behaves like a simple voltage divider.
- **Threshold Point:** At the point where $V_{in}$ equals $(1 + \frac{R_1}{R_2})V_{D,on}$, the diode $D_1$ turns on. This is marked by a change in the slope of the graph.
- **Saturation Region:** Beyond this threshold, $V_{out}$ becomes constant at $V_{D,on}$, indicating that the diode is fully conducting and clamps the output voltage.

Key Features and Technical Details:
- **Threshold Voltage:** The point at which the diode turns on is marked on the graph as $(1 + \frac{R_1}{R_2})V_{D,on}$. This is a critical value for determining when the diode begins to conduct.
- **Output Voltage in Saturation:** The output voltage $V_{out}$ is clamped to $V_{D,on}$ once the diode is on.
- **Initial Slope:** The initial slope of the graph is determined by the voltage divider rule, given by $\frac{R_2}{R_1 + R_2}$.

Annotations and Specific Data Points:
- **$V_{D,on}$:** This is the diode's forward-bias voltage, where the diode starts conducting significantly.
- **Dashed Lines:** These are used to indicate the transition points and constant voltage levels, enhancing the clarity of the graph’s key transitions.

(c)

Figure 3.16 (a) Diode circuit, (b) equivalent circuit when $D_{1}$ is off, (c) input/output characteristic.

In this case, the voltage across the diode happens to be equal to the output voltage. We note that if $V_{\text {in }}=-\infty, D_{1}$ is reverse biased and the circuit reduces to that in Fig. 3.16(b). Consequently,

$$
\begin{equation*}
v_{\text {out }}=\frac{R_{2}}{R_{1}+R_{2}} V_{i n} \tag{3.17}
\end{equation*}
$$

At what point does $D_{1}$ turn on? The diode voltage must reach $V_{D, o n}$, requiring an input voltage given by:

$$
\begin{equation*}
\frac{R_{2}}{R_{1}+R_{2}} V_{i n}=V_{D, o n} \tag{3.18}
\end{equation*}
$$

and hence

$$
\begin{equation*}
V_{i n}=\left(1+\frac{R_{1}}{R_{2}}\right) V_{D, o n} \tag{3.19}
\end{equation*}
$$

The reader may question the validity of this result: if the diode is indeed on, it draws current and the diode voltage is no longer equal to $\left[R_{2} /\left(R_{1}+R_{2}\right)\right] V_{i n}$. So why did we express the diode voltage as such in Eq. (3.18)? To determine the break point, we assume $V_{\text {in }}$ gradually increases so that it places the diode at the edge of the turn-on, e.g., it creates
$V_{\text {out }} \approx 799 \mathrm{mV}$. The diode therefore still draws no current, but the voltage across it and hence the input voltage are almost sufficient to turn it on.

For $V_{\text {in }}>\left(1+R_{1} / R_{2}\right) V_{D, \text { on }}, D_{1}$ remains forward-biased, yielding $V_{\text {out }}=V_{D, \text { on }}$. Figure 3.16(c) plots the overall characteristic.

Exercise Repeat the above example but assume the terminals of $D_{1}$ are swapped, i.e., the anode is tied to ground and the cathode the output node.

Exercise For the above example, plot the current through $R_{1}$ as a function of $V_{\text {in }}$.

Example
3.15

Plot the input/output characteristic for the circuit shown in Fig. 3.17(a). Assume a constant-voltage model for the diode.
image_name:Figure 3.17 (a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: X, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vin, N2: X}
name: D1, type: Diode, ports: {Na: Vin, Nc: X}
]
extrainfo:The circuit consists of a diode D1, two resistors R1 and R2, and a voltage source Vin. The diode is forward-biased when Vin is greater than the diode's threshold voltage, allowing current to flow through R2 and D1. R1 is connected between node X and ground, influencing the output voltage Vout at node X.

(a)
image_name:(a) Diode circuit
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vin, N2: Vout}
]
extrainfo:The circuit consists of a voltage source Vin, and two resistors R1 and R2. R2 connects Vin to Vout, and R1 connects Vout to ground, forming a voltage divider.

(c)
image_name:(b)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: X, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: X, N2: Vout}
name: D1, type: Diode, ports: {Na: X, Nc: Vin}
]
extrainfo:The circuit consists of a diode D1, and two resistors R1 and R2. R1 connects node X to ground, R2 connects node X to Vout, and D1 connects node X to Vin. The circuit is analyzed with Vin at negative infinity.

(b)
image_name:(d)
description:The graph is an input/output characteristic plot for a diode circuit, illustrating the relationship between the input voltage \( V_{in} \) and the output voltage \( V_{out} \). The plot is linear with two distinct regions, indicating different operating conditions of the diode.

**Axes Labels and Units:**
- The horizontal axis represents the input voltage \( V_{in} \).
- The vertical axis represents the output voltage \( V_{out} \).

**Overall Behavior and Trends:**
- For very negative \( V_{in} \), the output follows a line with a slope of 1, indicating a linear relationship where \( V_{out} = V_{in} \).
- As \( V_{in} \) increases, the line transitions at a point marked by the intersection of the two linear regions.
- Beyond this transition, the slope of the line changes to \( \frac{R_1}{R_1 + R_2} \), representing a different linear relationship.

**Key Features and Technical Details:**
- The transition point on the vertical axis is labeled as \((1 + \frac{R_1}{R_2}) V_{D,on}\), indicating the voltage at which the diode starts conducting.
- The slope of the line in the second region is less than 1, reflecting the voltage division between the resistors \( R_1 \) and \( R_2 \).

**Annotations and Specific Data Points:**
- The graph includes annotations for the slopes and transition points, providing a clear understanding of how the diode and resistors influence the circuit behavior.
- The slope values and transition voltage are critical for analyzing the diode's operation in the circuit.

(d)

Figure 3.17 (a) Diode circuit, (b) illustration for very negative inputs, (c) equivalent circuit when $D_{1}$ is off, (d) input/output characteristic.

Solution We begin with $V_{\text {in }}=-\infty$, and redraw the circuit as depicted in Fig. 3.17(b), placing the more negative voltages on the bottom and the more positive voltages on the top. This diagram suggests that the diode operates in forward bias, establishing a voltage at node $X$ equal to $V_{i n}+V_{D, o n}$. Note that in this regime, $V_{X}$ is independent of $R_{2}$ because $D_{1}$ acts as a battery. Thus, so long as $D_{1}$ is on, we have

$$
\begin{equation*}
V_{\text {out }}=V_{\text {in }}+V_{D, \text { on }} \tag{3.20}
\end{equation*}
$$

We also compute the current flowing through $R_{2}$ and $R_{1}$ :

$$
\begin{align*}
I_{R 2} & =\frac{V_{D, o n}}{R_{2}}  \tag{3.21}\\
I_{R 1} & =\frac{0-V_{X}}{R_{1}}  \tag{3.22}\\
& =\frac{-\left(V_{i n}+V_{D, o n}\right)}{R_{1}} \tag{3.23}
\end{align*}
$$

Thus, as $V_{i n}$ increases from $-\infty, I_{R 2}$ remains constant but $\left|I_{R 1}\right|$ decreases; i.e., at some point $I_{R 2}=I_{R 1}$.

At what point does $D_{1}$ turn off? Interestingly, in this case it is simpler to seek the condition that results in a zero current through the diode rather than insufficient voltage across it. The observation that at some point, $I_{R 2}=I_{R 1}$ proves useful here as this condition also implies that $D_{1}$ carries no current ( KCL at node $X$ ). In other words, $D_{1}$ turns off if $V_{i n}$ is chosen to yield $I_{R 2}=I_{R 1}$. From (3.21) and (3.23),

$$
\begin{equation*}
\frac{V_{D, \text { on }}}{R_{2}}=-\frac{V_{i n}+V_{D, o n}}{R_{1}} \tag{3.24}
\end{equation*}
$$

and hence

$$
\begin{equation*}
V_{i n}=-\left(1+\frac{R_{1}}{R_{2}}\right) V_{D, o n} . \tag{3.25}
\end{equation*}
$$

As $V_{i n}$ exceeds this value, the circuit reduces to that shown in Fig. 3.17(c) and

$$
\begin{equation*}
V_{\text {out }}=\frac{R_{1}}{R_{1}+R_{2}} V_{\text {in }} . \tag{3.26}
\end{equation*}
$$

The overall characteristic is shown in Fig. 3.17(d).
The reader may find it interesting to recognize that the circuits of Figs. 3.16(a) and 3.17(a) are identical: in the former, the output is sensed across the diode whereas in the latter it is sensed across the series resistor.

Exercise Repeat the above example if the terminals of the diode are swapped.

As mentioned in Example 3.4, in more complex circuits, it may be difficult to correctly predict the region of operation of each diode by inspection. In such cases, we may simply make a guess, proceed with the analysis, and eventually determine if the final result agrees or conflicts with the original guess. Of course, we still apply intuition to minimize the guesswork. The following example illustrates this approach.

Plot the input/output characteristic of the circuit shown in Fig. 3.18(a) using the constantvoltage diode model.

Solution We begin with $V_{i n}=-\infty$, predicting intuitively that $D_{1}$ is on. We also (blindly) assume that $D_{2}$ is on, thus reducing the circuit to that in Fig. 3.18(b). The path through $V_{D, \text { on }}$ and
image_name:(a)
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: D1, type: Diode, ports: {Na: Vin, Nc: X}
name: D2, type: Diode, ports: {Na: Vin, Nc: Y}
name: R1, type: Resistor, value: R1, ports: {N1: X, N2: Vout}
name: V_B, type: VoltageSource, value: 2V, ports: {Np: Y, Nn: GND}
]
extrainfo:The circuit is a diode-based rectifier with two diodes (D1 and D2) and a voltage source V_B. It includes a resistor R1 connected to Vout and a ground connection. The circuit is designed to modify the input voltage Vin based on the diode states and the bias voltage V_B.
image_name:(b)
description:
[
name: D1, type: Diode, ports: {Na: Vin, Nc: X}
name: D2, type: Diode, ports: {Na: X, Nc: Y}
name: R1, type: Resistor, value: R1, ports: {N1: X, N2: Vout}
name: R2, type: Resistor, value: R2, ports: {N1: Vout, N2: GND}
name: V_B, type: VoltageSource, value: 2V, ports: {Np: Y, Nn: GND}
]
extrainfo:The circuit in diagram (b) is a simplified version of the diode circuit for very negative inputs. It includes two diodes (D1 and D2), two resistors (R1 and R2), and a voltage source (V_B). The circuit is used to analyze the input/output characteristics of the diode configuration.
image_name:(c)
description:
[
name: D1, type: Diode, ports: {Na: Vin, Nc: X}
name: D2, type: Diode, ports: {Na: Vin, Nc: Y}
name: R1, type: Resistor, value: R1, ports: {N1: X, N2: Vout}
name: V_B, type: VoltageSource, value: 2V, ports: {Np: Y, Nn: GND}
name: V_D,on, type: VoltageSource, value: V_D,on, ports: {Np: Vin, Nn: Y}
]
extrainfo:The circuit diagram (c) is a simplified version for analyzing the behavior of the circuit under very negative input conditions. It includes two diodes (D1 and D2), a resistor (R1), and two voltage sources (V_B and V_D,on). The circuit is used to study the input/output characteristics by assuming certain conditions for the diodes and voltage sources.
image_name:(d)
description:
[
name: D1, type: Diode, ports: {Na: Vin, Nc: X}
name: R1, type: Resistor, value: R1, ports: {N1: X, N2: Vout}
]
extrainfo:The circuit diagram (d) shows a simplified version with diode D1 and resistor R1. Diode D2 and voltage source VB are not active in this configuration. The circuit is connected to Vin and outputs at Vout, with R1 connected to ground.
image_name:(e)
description:
[
name: D1, type: Diode, ports: {Na: Vin, Nc: X}
name: D2, type: Diode, ports: {Na: Vin, Nc: Y}
name: R1, type: Resistor, value: R1, ports: {N1: X, N2: Vout}
name: VB, type: VoltageSource, value: 2V, ports: {Np: Y, Nn: X}
]
extrainfo:The circuit in diagram (e) shows a configuration where two diodes (D1 and D2) are connected to the input voltage Vin. D1 is connected in series with resistor R1 leading to Vout, while D2 is in parallel with a voltage source VB (2V) connected between nodes Y and X. The output voltage Vout is taken across R1.
image_name:(f)
description:The graph labeled "(f)" represents the input/output characteristic of a diode circuit. It is a plot with the horizontal axis labeled as $V_{in}$ and the vertical axis labeled as $V_{out}$. The graph demonstrates the relationship between the input voltage ($V_{in}$) and the output voltage ($V_{out}$) for a specific diode configuration.

**Type of Graph and Function:**
- This is a linear plot showing the input/output characteristic of a diode circuit.

**Axes Labels and Units:**
- The horizontal axis represents the input voltage, $V_{in}$.
- The vertical axis represents the output voltage, $V_{out}$.

**Overall Behavior and Trends:**
- The graph shows a linear region where the output voltage follows the input voltage with a certain offset.
- Initially, the graph starts at a point where $V_{out} = -V_{D,on}$ when $V_{in}$ is very negative.
- As $V_{in}$ increases, $D_1$ turns off, and the graph shows a change in slope or offset.

**Key Features and Technical Details:**
- The graph features a notable point where $D_1$ turns off, marked by a change in behavior.
- The initial offset is due to the diode's forward voltage drop, denoted as $-V_{D,on}$.

**Annotations and Specific Data Points:**
- The point where $D_1$ turns off is annotated on the graph, indicating a transition in the circuit's behavior.
- The graph is linear except for this transition point, which is a critical feature of the diode's operation in the circuit.
image_name:(g)
description:
[
name: D1, type: Diode, ports: {Na: Vin, Nc: X}
name: D2, type: Diode, ports: {Na: Vin, Nc: Y}
name: R1, type: Resistor, value: R1, ports: {N1: X, N2: Vout}
name: V_B, type: VoltageSource, value: 2V, ports: {Np: Y, Nn: GND}
name: V_D,on, type: VoltageSource, value: V_D,on, ports: {Np: Vin, Nn: Y}
]
extrainfo:The circuit is a diode-based input/output characteristic circuit with a constant-voltage diode model, including two diodes (D1 and D2) and a voltage source V_B connected in parallel. The resistor R1 is connected from node X to Vout. The input voltage Vin is applied to the anodes of both diodes. The circuit illustrates the behavior of the diodes and resistor for different input conditions.
image_name:(h)
description:1. **Type of Graph and Function:**
The graph is an input/output characteristic plot for a diode circuit, showing the relationship between input voltage \( V_{in} \) and output voltage \( V_{out} \).

2. **Axes Labels and Units:**
- The horizontal axis represents the input voltage \( V_{in} \).
- The vertical axis represents the output voltage \( V_{out} \).
- Units for both axes are typically in volts (V).

3. **Overall Behavior and Trends:**
- The graph shows a piecewise linear behavior.
- For very negative \( V_{in} \), the output voltage \( V_{out} \) is constant at \(-V_{D,on}\), indicating the diode \( D_1 \) is on and conducting.
- As \( V_{in} \) increases and reaches \(-V_{D,on}\), \( D_1 \) turns off, and the output voltage starts to follow the input voltage.
- The graph has a sharp transition at \( V_{in} = -V_{D,on} \).

4. **Key Features and Technical Details:**
- The point \( V_{in} = -V_{D,on} \) is a significant transition where the behavior of the circuit changes.
- For \( V_{in} > -V_{D,on} \), the output voltage \( V_{out} \) increases linearly with \( V_{in} \).
- The slope of the line in this region is 1, indicating a direct linear relationship between \( V_{in} \) and \( V_{out} \).

5. **Annotations and Specific Data Points:**
- The graph is annotated with arrows and labels indicating the behavior of \( D_1 \) turning off and the linear increase in \( V_{out} \) as \( V_{in} \) increases past \(-V_{D,on} \).
- The line extends into the positive region of the \( V_{in} \) axis, maintaining a slope of 1.

Figure 3.18 (a) Diode circuit, (b) possible equivalent circuit for very negative inputs,
(c) simplified circuit, (d) equivalent circuit, (e) equivalent circuit for $V_{i n}=-V_{D, o n}$,
(f) section of input/output characteristic, (g) equivalent circuit, (f) complete input/ output characteristic.
$V_{B}$ creates a difference of $V_{D, \text { on }}+V_{B}$ between $V_{\text {in }}$ and $V_{\text {out }}$, i.e., $V_{\text {out }}=V_{\text {in }}-\left(V_{D, \text { on }}+V_{B}\right)$. This voltage difference also appears across the branch consisting of $R_{1}$ and $V_{D, o n}$, yielding

$$
\begin{equation*}
R_{1} I_{R 1}+V_{D, o n}=-\left(V_{B}+V_{D, o n}\right), \tag{3.27}
\end{equation*}
$$

and hence

$$
\begin{equation*}
I_{R 1}=\frac{-V_{B}-2 V_{D, o n}}{R_{1}} \tag{3.28}
\end{equation*}
$$

That is, $I_{R 1}$ is independent of $V_{i n}$. We must now analyze these results to determine whether they agree with our assumptions regarding the state of $D_{1}$ and $D_{2}$.

Consider the current flowing through $R_{2}$ :

$$
\begin{align*}
I_{R 2} & =-\frac{V_{\text {out }}}{R_{2}}  \tag{3.29}\\
& =-\frac{V_{\text {in }}-\left(V_{D, \text { on }}-V_{B}\right)}{R_{2}} \tag{3.30}
\end{align*}
$$

which approaches $+\infty$ for $V_{\text {in }}=-\infty$. The large value of $I_{R 2}$ and the constant value of $I_{R 1}$ indicate that the branch consisting of $V_{B}$ and $D_{2}$ carries a large current with the direction shown. That is, $D_{2}$ must conduct current from its cathode to its anode, which is not possible.

In summary, we have observed that the forward bias assumption for $D_{2}$ translates to a current in a prohibited direction. Thus, $D_{2}$ operates in reverse bias for $V_{i n}=-\infty$. Redrawing the circuit as in Fig. 3.18(c) and noting that $V_{X}=V_{i n}+V_{D, o n}$, we have

$$
\begin{equation*}
V_{\text {out }}=\left(V_{\text {in }}+V_{D, \text { on }}\right) \frac{R_{2}}{R_{1}+R_{2}} \tag{3.31}
\end{equation*}
$$

We now raise $V_{\text {in }}$ and determine the first break point, i.e., the point at which $D_{1}$ turns off or $D_{2}$ turns on. Which one occurs first? Let us assume $D_{1}$ turns off first and obtain the corresponding value of $V_{\text {in }}$. Since $D_{2}$ is assumed off, we draw the circuit as shown in Fig. 3.18(d). Assuming that $D_{1}$ is still slightly on, we recognize that at $V_{\text {in }} \approx-V_{D, o n}$, $V_{X}=V_{\text {in }}+V_{D, \text { on }}$ approaches zero, yielding a zero current through $R_{1}, R_{2}$, and hence $D_{1}$. The diode therefore turns off at $V_{i n}=-V_{D, o n}$.

We must now verify the assumption that $D_{2}$ remains off. Since at this break point, $V_{X}=V_{\text {out }}=0$, the voltage at node $Y$ is equal to $+V_{B}$ whereas the cathode of $D_{2}$ is at $-V_{D, \text { on }}$ [Fig. 3.18(e)]. In other words, $D_{2}$ is indeed off. Fig. 3.18(f) plots the input/output characteristic to the extent computed thus far, revealing that $V_{\text {out }}=0$ after the first break point because the current flowing through $R_{1}$ and $R_{2}$ is equal to zero.

At what point does $D_{2}$ turn on? The input voltage must exceed $V_{Y}$ by $V_{D, o n}$. Before $D_{2}$ turns on, $V_{\text {out }}=0$, and $V_{Y}=V_{B}$; i.e., $V_{\text {in }}$ must reach $V_{B}+V_{D, \text { on }}$, after which the circuit is configured as shown in Fig. 3.18(g). Consequently,

$$
\begin{equation*}
V_{\text {out }}=V_{\text {in }}-V_{D, \text { on }}-V_{B} \tag{3.32}
\end{equation*}
$$

Figure 3.18(h) plots the overall result, summarizing the regions of operation.
Exercise In the above example, assume $D_{2}$ turns on before $D_{1}$ turns off and show that the results conflict with the assumption.

## 3.4 LARGE-SIGNAL AND SMALL-SIGNAL OPERATION

Our treatment of diodes thus far has allowed arbitrarily large voltage and current changes, thereby requiring a "general" model such as the exponential I/V characteristic. We call this regime "large-signal operation" and the exponential characteristic the "large-signal model" to emphasize that the model can accommodate arbitrary signal levels. However, as seen in previous examples, this model often complicates the analysis, making it difficult to develop an intuitive understanding of the circuit's operation. Furthermore, as the
number of nonlinear devices in the circuit increases, "manual" analysis eventually becomes impractical.

The ideal and constant-voltage diode models resolve the issues to some extent, but the sharp nonlinearity at the turn-on point still proves problematic. The following example illustrates the general difficulty.
3.17

Having lost his 2.4-V cellphone charger, an electrical engineering student tries several stores but does not find adaptors with outputs less than 3 V . He then decides to put his knowledge of electronics to work and constructs the circuit shown in Fig. 3.19, where three identical diodes in forward bias produce a total voltage of $V_{\text {out }}=3 V_{D} \approx 2.4 \mathrm{~V}$ and resistor $R_{1}$ sustains the remaining 600 mV . Neglect the current drawn by the cellphone. ${ }^{6}$ (a) Determine the reverse saturation current, $I_{S 1}$ so that $V_{\text {out }}=2.4 \mathrm{~V}$. (b) Compute $V_{\text {out }}$ if the adaptor voltage is in fact 3.1 V .
image_name:Fig. 3.19
description:
[
name: Vad, type: VoltageSource, value: 3V, ports: {Np: Vad, Nn: GND}
name: Ix, type: CurrentSource, ports: {Np: Vad, Nn: X1}
name: R1, type: Resistor, value: 100Ω, ports: {N1: Vad, N2: Vout}
name: D1, type: Diode, ports: {Na: Vout, Nc: X1}
name: D2, type: Diode, ports: {Na: X1, Nc: X2}
name: D3, type: Diode, ports: {Na: X2, Nc: GND}
]
extrainfo:The circuit consists of a voltage source (Vad = 3V), a current source (Ix), a resistor (R1 = 100Ω), and three diodes (D1, D2, D3) in series. The diodes are forward-biased, and the total output voltage (Vout) is approximately 2.4V. The resistor R1 sustains the remaining 600mV. The circuit is used to feed a cellphone, with the current through the diodes being equal to the current through the resistor.

Solution
(a) With $V_{\text {out }}=2.4 \mathrm{~V}$, the current flowing through $R_{1}$ is equal to

$$
\begin{align*}
I_{X} & =\frac{V_{\text {ad }}-V_{\text {out }}}{R_{1}}  \tag{3.33}\\
& =6 \mathrm{~mA} . \tag{3.34}
\end{align*}
$$

We note that each diode carries $I_{X}$ and hence

$$
\begin{equation*}
I_{X}=I_{S} \exp \frac{V_{D}}{V_{T}} \tag{3.35}
\end{equation*}
$$

It follows that

$$
\begin{equation*}
6 \mathrm{~mA}=I_{S} \exp \frac{800 \mathrm{mV}}{26 \mathrm{mV}} \tag{3.36}
\end{equation*}
$$

and

$$
\begin{equation*}
I_{S}=2.602 \times 10^{-16} \mathrm{~A} \tag{3.37}
\end{equation*}
$$

(b) If $V_{\text {ad }}$ increases to 3.1 V , we expect that $V_{\text {out }}$ increases only slightly. To understand why, first suppose $V_{\text {out }}$ remains constant and equal to 2.4 V . Then, the additional 0.1 V must drop across $R_{1}$, raising $I_{X}$ to 7 mA . Since the voltage across each diode has a
${ }^{6}$ Made for the sake of simplicity here, this assumption may not be valid.

[^0]:    ${ }^{1}$ Recall that the wavelength is equal to the (light) velocity divided by the frequency.
${ }^{2}$ Cellphones in fact use other types of modulation to translate the voice band to higher frequencies.
${ }^{3}$ Also called a "mixer" in high-frequency

[^1]:    *This section serves as a review and can be skipped in classroom teaching.

[^2]:    ${ }^{5}$ Distortion arises if the output is not a linear function of input.

[^3]:    ${ }^{1}$ As design managers often say, "If you do not push the devices and circuits to their limit but your competitor does, then you lose to your competitor."
${ }^{2}$ Silicon is obtained from sand after a great deal of processing.

[^4]:    ${ }^{3}$ The unit eV (electron volt) represents the energy necessary to move one electron across a potential difference of 1 V . Note that $1 \mathrm{eV}=1.6 \times 10^{-19} \mathrm{~J}$.

[^5]:    ${ }^{4}$ Recall that the potential (voltage) difference, $V$, is equal to the negative integral of the electric field, $E$, with respect to distance: $V_{a b}=-\int_{b}^{a} E d x$.
${ }^{5}$ The convention for direction of current assumes flow of positive charge from a positive voltage to a negative voltage. Thus, if electrons flow from point $A$ to point $B$, the current is considered to have a direction from $B$ to $A$.
${ }^{6}$ This phenomenon is analogous to the "terminal velocity" that a sky diver with a parachute (hopefully, open) experiences.

[^6]:    *This section can be skipped in a first reading.

[^7]:    ${ }^{7}$ The factor $L_{d}$ is necessary to convert the exponent to a dimensionless quantity.

[^8]:    ${ }^{8}$ The direction of the electric field is determined by placing a small positive test charge in the region and watching how it moves: away from positive charge and toward negative charge.

[^9]:    ${ }^{10}$ The dielectric constant of materials is usually written in the form $\epsilon_{r} \epsilon_{0}$, where $\epsilon_{r}$ is the "relative" dielectric constant and a dimensionless factor (e.g., 11.7), and $\epsilon_{0}$ the dielectric constant of vacuum $\left(8.85 \times 10^{-14} \mathrm{~F} / \mathrm{cm}\right)$.

[^10]:    ${ }^{11}$ The width of the depletion region actually decreases in forward bias, but we neglect this effect here.

[^11]:    *This section can be skipped in a first reading.

[^12]:    ${ }^{1}$ This value refers to the root-mean-square (rms) voltage. The peak value is therefore equal to $110 \sqrt{2}$.
${ }^{2}$ The line ac voltage in most countries is at 220 V and 50 Hz .
${ }^{3}$ The actual operation of adaptors is somewhat different.

[^13]:    ${ }^{4}$ In our drawings, we sometimes place more positive nodes higher to provide a visual picture of the circuit's operation. The diodes in Fig. 3.3(b) are drawn according to this convention.

[^14]:    ${ }^{5}$ Note that without $R_{1}$, the output voltage is not defined because a floating node can assume any potential.

logarithmic dependence upon the current, the change from 6 mA to 7 mA indeed yields a small change in $V_{\text {out }}{ }^{7}$

To examine the circuit quantitatively, we begin with $I_{X}=7 \mathrm{~mA}$ and iterate:

$$
\begin{align*}
V_{\text {out }} & =3 V_{D}  \tag{3.38}\\
& =3 V_{T} \ln \frac{I_{X}}{I_{S}}  \tag{3.39}\\
& =2.412 \mathrm{~V} \tag{3.40}
\end{align*}
$$

This value of $V_{\text {out }}$ gives a new value for $I_{X}$ :

$$
\begin{align*}
I_{X} & =\frac{V_{\text {ad }}-V_{\text {out }}}{R_{1}}  \tag{3.41}\\
& =6.88 \mathrm{~mA} \tag{3.42}
\end{align*}
$$

which translates to a new $V_{\text {out }}$ :

$$
\begin{align*}
V_{\text {out }} & =3 V_{D}  \tag{3.43}\\
& =2.411 \mathrm{~V} . \tag{3.44}
\end{align*}
$$

Noting the very small difference between (3.40) and (3.44), we conclude that $V_{\text {out }}=2.411 \mathrm{~V}$ with good accuracy. The constant-voltage diode model would not be useful in this case.

Exercise Repeat the above example if an output voltage of 2.35 is desired.

The situation ${ }^{6}$ described above is an example of small "perturbations" in circuits. The change in $V_{a d}$ from 3 V to 3.1 V results in a small change in the circuit's voltages and currents, motivating us to seek a simpler analysis method that can replace the nonlinear equations and the inevitable iterative procedure. Of course, since the above example does not present an overwhelmingly difficult problem, the reader may wonder if a simpler approach is really necessary. But, as seen in subsequent chapters, circuits containing complex devices such as transistors may indeed become impossible to analyze if the nonlinear equations are retained.

These thoughts lead us to the extremely important concept of "small-signal operation," whereby the circuit experiences only small changes in voltages and currents and can therefore be simplified through the use of "small-signal models" for nonlinear devices. The simplicity arises because such models are linear, allowing standard circuit analysis and obviating the need for iteration. The definition of "small" will become clear later.

To develop our understanding of small-signal operation, let us consider diode $D_{1}$ in Fig. 3.20(a), which sustains a voltage $V_{D 1}$ and carries a current $I_{D 1}$ [point $A$ in Fig. 3.20(b)]. Now suppose a perturbation in the circuit changes the diode voltage by a small amount

[^0]image_name:(a)
description:
[
name: D1, type: Diode, ports: {Na: A, Nc: K}
]
extrainfo:The diagram shows a diode D1 with an anode at node A and a cathode at node K. It illustrates the diode's operation at a point A with voltage VD1 and current ID1, and the effect of a small voltage change ΔVD on the current, resulting in a new operating point B with current ID2.
image_name:(b)
description:The graph labeled (b) in Figure 3.20 presents the current-voltage (I-V) characteristic of a diode. This is a nonlinear graph depicting the relationship between the diode current \( I_D \) on the vertical axis and the diode voltage \( V_D \) on the horizontal axis.

1. **Type of Graph and Function**:
- The graph is a nonlinear I-V characteristic curve typical for a diode.

2. **Axes Labels and Units**:
- The horizontal axis represents the diode voltage \( V_D \).
- The vertical axis represents the diode current \( I_D \).
- The units for \( V_D \) and \( I_D \) are typically volts and amperes, respectively, although specific units are not indicated on the graph.

3. **Overall Behavior and Trends**:
- The graph shows an exponential increase in current \( I_D \) as the voltage \( V_D \) increases. This is characteristic of the forward-bias region of a diode.
- The curve starts near the origin and rises steeply as voltage increases, indicating the diode's exponential response to voltage changes.

4. **Key Features and Technical Details**:
- Point \( A \) is marked on the curve, representing an operating point with specific voltage \( V_{D1} \) and current \( I_{D1} \).
- There is no linear region shown; the entire curve is nonlinear, highlighting the diode's exponential behavior.

5. **Annotations and Specific Data Points**:
- The operating point \( A \) is annotated on the graph, showing the intersection of a horizontal line from \( I_{D1} \) and a vertical line from \( V_{D1} \).
- There are no additional annotations or specific numerical values provided for other points on the curve.
image_name:(c)
description:The graph in Figure 3.20(c) is a plot of diode current \( I_D \) versus diode voltage \( V_D \). It specifically illustrates the effect of a small change in voltage \( \Delta V_D \) on the diode current, showing the transition from point A to point B.

1. **Type of Graph and Function:**
- This is a current-voltage (I-V) characteristic curve for a diode, showing the exponential relationship between the diode current and voltage.

2. **Axes Labels and Units:**
- The horizontal axis represents the diode voltage \( V_D \), typically in volts.
- The vertical axis represents the diode current \( I_D \), typically in amperes.
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The curve is exponential, indicating the typical behavior of a diode where current increases exponentially with an increase in voltage.
- At point A, the diode is at its initial operating point \( (V_{D1}, I_{D1}) \).
- The curve shows an increase in current from \( I_{D1} \) to \( I_{D2} \) as the voltage changes from \( V_{D1} \) to \( V_{D2} \), illustrating the concept of small-signal operation.

4. **Key Features and Technical Details:**
- Point A represents the initial operating point of the diode, with coordinates \( (V_{D1}, I_{D1}) \).
- Point B represents the new operating point after a small increase in voltage, with coordinates \( (V_{D2}, I_{D2}) \).
- The change in voltage \( \Delta V_D \) is marked along the horizontal axis between \( V_{D1} \) and \( V_{D2} \).
- The change in current \( \Delta I_D \) is marked along the vertical axis between \( I_{D1} \) and \( I_{D2} \).

5. **Annotations and Specific Data Points:**
- The graph includes annotations for points A and B, with dashed lines indicating the corresponding current and voltage levels.
- The change in voltage \( \Delta V_D \) and the resulting change in current \( \Delta I_D \) are highlighted, demonstrating the diode's response to small perturbations in voltage.

Figure 3.20 (a) General circuit containing a diode, (b) operating point of $D_{1}$, (c) change in $I_{D}$ as a result of change in $V_{D}$.
$\Delta V_{D}$ [point $B$ in Fig. 3.20(c)]. How do we predict the change in the diode current, $\Delta I_{D}$ ? We can begin with the nonlinear characteristic:

$$
\begin{align*}
I_{D 2} & =I_{S} \exp \frac{V_{D 1}+\Delta V}{V_{T}}  \tag{3.45}\\
& =I_{S} \exp \frac{V_{D 1}}{V_{T}} \exp \frac{\Delta V}{V_{T}} \tag{3.46}
\end{align*}
$$

If $\Delta V \ll V_{T}$, then $\exp \left(\Delta V / V_{T}\right) \approx 1+\Delta V / V_{T}$ and

$$
\begin{align*}
I_{D 2} & =I_{S} \exp \frac{V_{D 1}}{V_{T}}+\frac{\Delta V}{V_{T}} I_{S} \exp \frac{V_{D 1}}{V_{T}}  \tag{3.47}\\
& =I_{D 1}+\frac{\Delta V}{V_{T}} I_{D 1} \tag{3.48}
\end{align*}
$$

That is,

$$
\begin{equation*}
\Delta I_{D}=\frac{\Delta V}{V_{T}} I_{D 1} \tag{3.49}
\end{equation*}
$$

The key observation here is that $\Delta I_{D}$ is a linear function of $\Delta V$, with a proportionality factor equal to $I_{D 1} / V_{T}$. (Note that larger values of $I_{D 1}$ lead to a greater $\Delta I_{D}$ for a given $\Delta V_{D}$. The significance of this trend becomes clear later.)

The above result should not come as a surprise: if the change in $V_{D}$ is small, the section of the characteristic in Fig. 3.20(c) between points $A$ and $B$ can be approximated by a straight line (Fig. 3.21), with a slope equal to the local slope of the characteristic.
image_name:Figure 3.21
description:The graph in Figure 3.21 illustrates a section of a diode's current-voltage (I-V) characteristic curve. This is an exponential graph depicting the relationship between the diode current (I_D) on the vertical axis and the diode voltage (V_D) on the horizontal axis. Both axes are typically in linear scale, with the current axis labeled as I_D and the voltage axis labeled as V_D.

1. **Type of Graph and Function:**
- This is a characteristic curve graph showing the exponential relationship typical of a diode's I-V characteristics.

2. **Axes Labels and Units:**
- The vertical axis represents the diode current (I_D), while the horizontal axis represents the diode voltage (V_D).
- Units are not explicitly shown but are conventionally amperes for current and volts for voltage.

3. **Overall Behavior and Trends:**
- The curve shows an exponential increase in current as the voltage increases, typical of diode behavior.
- There is a small section between points A and B that is approximated by a straight line, indicating a linear approximation for small changes in voltage.

4. **Key Features and Technical Details:**
- Points A and B are marked on the curve, with A corresponding to (V_D1, I_D1) and B to (V_D2, I_D2).
- The linear approximation between A and B is highlighted, showing a slope that represents the small-signal conductance.
- The change in current (ΔI_D) and voltage (ΔV_D) between these points is shown, illustrating the linear approximation.

5. **Annotations and Specific Data Points:**
- The graph includes dashed lines to indicate the levels of I_D1 and I_D2, as well as V_D1 and V_D2.
- The inset zooms in on the linear section between A and B, emphasizing the linear approximation of the characteristic curve.

Figure 3.21 Approximation of characteristic by a straight line.

In other words,

$$
\begin{align*}
\frac{\Delta I_{D}}{\Delta V_{D}} & =\left.\frac{d I_{D}}{d V_{D}}\right|_{V D=V D 1}  \tag{3.50}\\
& =\frac{I_{S}}{V_{T}} \exp \frac{V_{D 1}}{V_{T}}  \tag{3.51}\\
& =\frac{I_{D 1}}{V_{T}} \tag{3.52}
\end{align*}
$$

which yields the same result as that in Eq. (3.49). ${ }^{8}$
Let us summarize our results thus far. If the voltage across a diode changes by a small amount (much less than $V_{T}$ ), then the change in the current is given by Eq. (3.49). Equivalently, for small-signal analysis, we can assume the operation is at a point such as $A$ in Fig. 3.21 and, due to a small perturbation, it moves on a straight line to point $B$ with a slope equal to the local slope of the characteristic (i.e., $d I_{D} / d V_{D}$ calculated at $V_{D}=V_{D 1}$ or $I_{D}=I_{D 1}$ ). Point $A$ is called the "bias" point, the "quiescent" point, or the "operating" point.

Example A diode is biased at a current of 1 mA . (a) Determine the current change if $V_{D}$ changes by 1 mV . (b) Determine the voltage change if $I_{D}$ changes by $10 \%$.

Solution (a) We have

$$
\begin{align*}
\Delta I_{D} & =\frac{I_{D}}{V_{T}} \Delta V_{D}  \tag{3.53}\\
& =38.4 \mu \mathrm{~A} . \tag{3.54}
\end{align*}
$$

(b) Using the same equation yields

$$
\begin{align*}
\Delta V_{D} & =\frac{V_{T}}{I_{D}} \Delta I_{D}  \tag{3.55}\\
& =\left(\frac{26 \mathrm{mV}}{1 \mathrm{~mA}}\right) \times(0.1 \mathrm{~mA})  \tag{3.56}\\
& =2.6 \mathrm{mV} \tag{3.57}
\end{align*}
$$

Exercise In response to a current change of 1 mA , a diode exhibits a voltage change of 3 mV . Calculate the bias current of the diode.

Equation (3.58) in the above example reveals an interesting aspect of small-signal operation: as far as (small) changes in the diode current and voltage are concerned, the device behaves as a linear resistor. In analogy with Ohm's Law, we define the "small-signal

[^1]resistance" of the diode as:
\$\$

$$
\begin{equation*}
r_{d}=\frac{V_{T}}{I_{D}} \tag{3.58}
\end{equation*}
$$

\$\$

This quantity is also called the "incremental" resistance to emphasize its validity for small changes. In the above example, $r_{d}=26 \Omega$.

Figure 3.22(a) summarizes the results of our derivations for a forward-biased diode. For bias calculations, the diode is replaced with an ideal voltage source of value $V_{D, o n}$, and for small changes, with a resistance equal to $r_{d}$. For example, the circuit of Fig. 3.22(b) is transformed to that in Fig. 3.22(c) if only small changes in $V_{1}$ and $V_{\text {out }}$ are of interest. Note that $v_{1}$ and $v_{\text {out }}$ in Fig. 3.22(c) represent changes in voltage and are called smallsignal quantities. In general, we denote small-signal voltages and currents by lower-case letters.
image_name:(a)
description:
[
name: VD,on, type: VoltageSource, value: VD,on, ports: {Np: Vout, Nn: GND}
name: rd, type: Resistor, value: rd, ports: {N1: Vout, N2: GND}
name: R1, type: Resistor, value: R1, ports: {N1: V1, N2: Vout}
name: D1, type: Diode, ports: {Na: Vout, Nc: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
]
extrainfo:The diagram illustrates a bias model and small-signal model for a diode. The diode in the circuit is replaced by a voltage source VD,on and a resistor rd for small-signal analysis. The circuit is used to analyze small changes in input and output voltages.
image_name:(b)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: V1, N2: Vout}
name: D1, type: Diode, ports: {Na: Vout, Nc: GND}
]
extrainfo:The circuit in (b) is a simple diode rectifier with a resistor R1 connected to a voltage source V1, and a diode D1 connected to the output node Vout. The diode is in forward-bias configuration, allowing current to flow from Vout to GND when the diode is conducting.
image_name:(c)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: V1, N2: Vout}
name: rd, type: Resistor, value: rd, ports: {N1: Vout, N2: GND}
]
extrainfo:This is a small-signal model of a diode circuit where the diode is replaced by its small-signal resistance rd. The circuit is powered by a voltage source V1 and includes a resistor R1. The output voltage is measured across the resistor rd.

Figure 3.22 Summary of diode models for bias and signal calculations, (b) circuit example, (c) small-signal model.

### Example

A sinusoidal signal having a peak amplitude of $V_{p}$ and a dc value of $V_{0}$ can be expressed
3.19 as $V(t)=V_{0}+V_{p} \cos \omega t$. If this signal is applied across a diode and $V_{p} \ll V_{T}$, determine the resulting diode current.

Solution The signal waveform is illustrated in Fig. 3.23(a). As shown in Fig. 3.23(b), we rotate this diagram by $90^{\circ}$ so that its vertical axis is aligned with the voltage axis of the diode characteristic. With a signal swing much less than $V_{T}$, we can view $V_{0}$ and the corresponding current, $I_{0}$, as the bias point of the diode and $V_{p}$ as a small perturbation. It follows that

$$
\begin{equation*}
I_{0}=I_{S} \exp \frac{V_{0}}{V_{T}} \tag{3.59}
\end{equation*}
$$

and

$$
\begin{equation*}
r_{d}=\frac{V_{T}}{I_{0}} \tag{3.60}
\end{equation*}
$$

Thus, the peak current is simply equal to

$$
\begin{align*}
I_{p} & =V_{p} / r_{d}  \tag{3.61}\\
& =\frac{I_{0}}{V_{T}} V_{p} \tag{3.62}
\end{align*}
$$

image_name:(a)
description:The graph is a time-domain waveform depicting a sinusoidal voltage signal with a DC offset. The x-axis represents time \( t \), although no specific units or scale are provided. The y-axis represents the voltage \( V(t) \), again without specified units or scale.

The waveform is a sinusoidal function oscillating around a constant DC level \( V_0 \). The sinusoid has a peak amplitude of \( V_p \) above and below the DC level, indicating that the voltage varies between \( V_0 + V_p \) and \( V_0 - V_p \). The waveform is symmetric around the DC level, showing a regular periodic pattern typical of a sinusoidal signal.

Key features include:
- A horizontal dashed line indicating the DC level \( V_0 \).
- Vertical arrows pointing to the peak amplitude \( V_p \) above and below the DC level, highlighting the maximum deviation of the sinusoidal waveform from the DC level.
- The sinusoidal waveform suggests a consistent frequency, though the exact frequency is not specified.

No specific numerical values or annotations are provided on the graph, focusing instead on the general shape and behavior of the waveform.
image_name:(b)
description:The graph in Figure 3.23 (b) is a time-domain waveform illustrating the response of a diode to a sinusoidal input. The horizontal axis represents time \( t \), while the vertical axis represents voltage \( V(t) \). The graph shows a sinusoidal waveform superimposed on a constant DC level \( V_0 \).

1. **Type of Graph and Function:**
- The graph is a time-domain waveform showing how the voltage across a diode varies over time in response to a sinusoidal input.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \( t \) for time, though the units are not specified.
- The vertical axis is labeled \( V(t) \) for voltage, again with unspecified units.
- The graph includes a dotted line indicating the DC level \( V_0 \).

3. **Overall Behavior and Trends:**
- The waveform exhibits a sinusoidal shape oscillating around the DC level \( V_0 \).
- The amplitude of the oscillation is denoted as \( V_p \), representing the peak voltage of the sinusoid above and below the DC level.

4. **Key Features and Technical Details:**
- The waveform has periodic peaks and troughs, indicating the sinusoidal nature of the input.
- The peak-to-peak voltage is twice the amplitude \( V_p \), as it swings from \( V_0 + V_p \) to \( V_0 - V_p \).

5. **Annotations and Specific Data Points:**
- The graph includes annotations for the DC level \( V_0 \) and the peak amplitude \( V_p \), highlighting the sinusoidal variation around the DC bias point.

In summary, the graph illustrates the diode's response to a sinusoidal input, characterized by oscillations around a DC bias level, with the peak amplitude of the oscillations labeled as \( V_p \).

(a)
image_name:Figure 3.23 (a)
description:The graph in Figure 3.23 (a) consists of two main parts illustrating the behavior of a diode under a sinusoidal input.

1. **Type of Graph and Function:**
- The graph on the left is a plot of diode current \( I_D \) versus diode voltage \( V_D \), showing the diode's characteristic curve.
- The graph on the right is a time-domain waveform of the diode current \( I_D \) as a function of time \( t \).

2. **Axes Labels and Units:**
- The left graph has the vertical axis labeled \( I_D \) (diode current) and the horizontal axis labeled \( V_D \) (diode voltage).
- The right graph has the vertical axis labeled \( I_D \) and the horizontal axis labeled \( t \) (time).
- Units are not explicitly mentioned, but current is typically in amperes and voltage in volts.

3. **Overall Behavior and Trends:**
- The left graph shows the exponential increase of diode current \( I_D \) with increasing diode voltage \( V_D \), characteristic of a diode's forward-bias region.
- The right graph depicts sinusoidal oscillations of the diode current \( I_D \) around a DC level \( I_0 \) over time.

4. **Key Features and Technical Details:**
- In the left graph, the exponential curve starts near the origin and rises sharply as \( V_D \) increases, indicating the diode's turn-on behavior.
- The right graph shows oscillations with a peak-to-peak amplitude of twice \( I_p \), centered around a DC level \( I_0 \).
- The sinusoidal input is annotated with \( V_0 \) and the peak amplitude \( V_p \), illustrating the input variation.

5. **Annotations and Specific Data Points:**
- The left graph includes dashed lines indicating the DC level \( I_0 \).
- The right graph includes annotations for the peak amplitude \( I_p \) of the oscillations.

In summary, Figure 3.23 (a) illustrates the diode's current-voltage characteristic and its response to a sinusoidal input, showing how the diode current oscillates around a DC level in response to the input voltage.
image_name:Figure 3.23 (b)
description:The graph in Figure 3.23(b) illustrates the response of a diode to a sinusoidal input. It consists of two main parts: the left side shows the diode characteristic curve, while the right side displays the time-domain response of the diode current.

1. **Type of Graph and Function:**
- The left graph is a diode characteristic curve plotting diode current \( I_D \) against diode voltage \( V_D \), while the right graph is a time-domain waveform showing the diode current \( I_D \) over time \( t \).

2. **Axes Labels and Units:**
- **Left Graph:**
- X-axis: Diode voltage \( V_D \) (units not specified, typically volts)
- Y-axis: Diode current \( I_D \) (units not specified, typically amperes)
- **Right Graph:**
- X-axis: Time \( t \) (units not specified, typically seconds)
- Y-axis: Diode current \( I_D \) (units not specified, typically amperes)

3. **Overall Behavior and Trends:**
- **Left Graph:**
- The diode characteristic curve shows an exponential increase in diode current \( I_D \) as the diode voltage \( V_D \) increases.
- The curve starts from the origin and rises steeply, indicating the typical exponential behavior of a diode in forward bias.
- **Right Graph:**
- The time-domain response shows a sinusoidal variation of the diode current \( I_D \) around a DC level \( I_0 \).
- The waveform oscillates with a peak amplitude \( I_p \), indicating the influence of the sinusoidal input.

4. **Key Features and Technical Details:**
- **Left Graph:**
- The DC level \( I_0 \) is marked, showing the bias point of the diode.
- **Right Graph:**
- The sinusoidal waveform is centered around the DC level \( I_0 \) with peaks at \( I_0 + I_p \) and troughs at \( I_0 - I_p \).
- The peak amplitude \( I_p \) is annotated, indicating the extent of the sinusoidal variation.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for the DC level \( I_0 \) and the peak amplitude \( I_p \), highlighting the sinusoidal variation around the DC bias point.

(b)

Figure 3.23 (a) Sinusoidal input along with a dc level, (b) response of a diode to the sinusoid.
yielding

$$
\begin{align*}
I_{D}(t) & =I_{0}+I_{p} \cos \omega t  \tag{3.63}\\
& =I_{S} \exp \frac{V_{0}}{V_{T}}+\frac{I_{0}}{V_{T}} V_{p} \cos \omega t \tag{3.64}
\end{align*}
$$

Exercise The diode in the above example produces a peak current of 0.1 mA in response to $V_{0}=800 \mathrm{mV}$ and $V_{p}=1.5 \mathrm{mV}$. Calculate $I_{S}$.

The above example demonstrates the utility of small-signal analysis. If $V_{p}$ were large, we would need to solve the following equation:

$$
\begin{equation*}
I_{D}(t)=I_{S} \exp \frac{V_{0}+V_{p} \cos \omega t}{V_{T}} \tag{3.65}
\end{equation*}
$$

a task much more difficult than the above linear calculations. ${ }^{9}$

In the derivation leading to Eq. (3.49), we assumed a small change in $V_{D}$ and obtained
3.20 the resulting change in $I_{D}$. Beginning with $V_{D}=V_{T} \ln \left(I_{D} / I_{S}\right)$, investigate the reverse case, i.e., $I_{D}$ changes by a small amount and we wish to compute the change in $V_{D}$.

[^2]Solution Denoting the change in $V_{D}$ by $\Delta V_{D}$, we have

$$
\begin{align*}
V_{D 1}+\Delta V_{D} & =V_{T} \ln \frac{I_{D 1}+\Delta I_{D}}{I_{S}}  \tag{3.66}\\
& =V_{T} \ln \left[\frac{I_{D 1}}{I_{S}}\left(1+\frac{\Delta I_{D}}{I_{D 1}}\right)\right]  \tag{3.67}\\
& =V_{T} \ln \frac{I_{D 1}}{I_{S}}+V_{T} \ln \left(1+\frac{\Delta I_{D}}{I_{D 1}}\right) \tag{3.68}
\end{align*}
$$

For small-signal operation, we assume $\Delta I_{D} \ll I_{D 1}$ and note that $\ln (1+\epsilon) \approx \epsilon$ if $\epsilon \ll 1$. Thus,

$$
\begin{equation*}
\Delta V_{D}=V_{T} \cdot \frac{\Delta I_{D}}{I_{D 1}} \tag{3.69}
\end{equation*}
$$

which is the same as Eq. (3.49). Figure 3.24 illustrates the two cases, distinguishing between the cause and the effect.
image_name:(a)
description:
[
name: ΔVD, type: VoltageSource, ports: {Np: ΔVD, Nn: GND}
name: D1, type: Diode, ports: {Na: ΔVD, Nc: GND}
name: ΔID, type: CurrentSource, ports: {Np: ΔVD, Nn: GND}
]
extrainfo:The circuit diagram (a) represents a small-signal model of a diode with a voltage source ΔVD and a current source ΔID connected in parallel with diode D1. The ground node is marked as GND. The equations provided describe the relationships between the changes in diode current and voltage.
image_name:(b)
description:
[
name: D1, type: Diode, ports: {Na: ΔVD, Nc: GND}
name: ΔVD, type: VoltageSource, ports: {Np: ΔVD, Nn: GND}
name: ΔID, type: CurrentSource, ports: {Np: ΔVD, Nn: GND}
]
extrainfo:The circuit diagram (b) represents a small-signal model of a diode with a voltage source (ΔVD) and a current source (ΔID) connected in parallel with the diode D1. The relationship between the change in current (ΔID) and voltage (ΔVD) is given by ΔVD = ΔID * rd = ΔID * (VT / ID1).

Figure 3.24 Change in diode current (voltage) due to a change in voltage (current).

Exercise Repeat the above example by taking the derivative of the diode voltage equation with respect to $I_{D}$.

With our understanding of small-signal operation, we now revisit Example 3.17.

Example Repeat part (b) of Example 3.17 with the aid of a small-signal model for the diodes.
3.21

Solution Since each diode carries $I_{D 1}=6 \mathrm{~mA}$ with an adaptor voltage of 3 V and $V_{D 1}=800 \mathrm{mV}$, we can construct the small-signal model shown in Fig. 3.25, where $v_{a d}=100 \mathrm{mV}$ and $r_{d}=(26 \mathrm{mV}) /(6 \mathrm{~mA})=4.33 \Omega$. (As mentioned earlier, the voltages shown in this model denote small changes.) We can thus write:

$$
\begin{align*}
v_{\text {out }} & =\frac{3 r_{d}}{R_{1}+3 r_{d}} v_{a d}  \tag{3.70}\\
& =11.5 \mathrm{mV} . \tag{3.71}
\end{align*}
$$

Figure 3.25 Small-signal model of adaptor.

That is, a 100-mV change in $V_{\text {ad }}$ yields an $11.5-\mathrm{mV}$ change in $V_{\text {out }}$. In Example 3.17, solution of nonlinear diode equations predicted an $11-\mathrm{mV}$ change in $V_{\text {out }}$. The small-signal analysis therefore offers reasonable accuracy while requiring much less computational effort.

Exercise Repeat Examples (3.17) and (3.21) if the value of $R_{1}$ in Fig. 3.19 is changed to $200 \Omega$.

Considering the power of today's computer software tools, the reader may wonder if the small-signal model is really necessary. Indeed, we utilize sophisticated simulation tools in the design of integrated circuits today, but the intuition gained by hand analysis of a circuit proves invaluable in understanding fundamental limitations and various trade-offs that eventually lead to a compromise in the design. A good circuit designer analyzes and understands the circuit before giving it to the computer for a more accurate analysis. A bad circuit designer, on the other hand, allows the computer to think for him/her.

In Examples 3.17 and 3.21, the current drawn by the cellphone is neglected. Now suppose, 3.22 as shown in Fig. 3.26, the load pulls a current of $0.5 \mathrm{~mA}^{10}$ and determine $V_{\text {out }}$.
image_name:Figure 3.26
description:
[
name: Vad, type: VoltageSource, value: Vad, ports: {Np: Vad, Nn: GND}
name: R1, type: Resistor, value: 100Ω, ports: {N1: Vad, N2: X1}
name: D1, type: Diode, ports: {Na: X1, Nc: X2}
name: D2, type: Diode, ports: {Na: X2, Nc: Vout}
name: D3, type: Diode, ports: {Na: Vout, Nc: GND}
]
extrainfo:The circuit is an adaptor feeding a cellphone, drawing 0.5 mA current. The diodes are arranged in series to regulate the output voltage Vout.

[^3]Solution Since the current flowing through the diodes decreases by 0.5 mA and since this change is much less than the bias current $(6 \mathrm{~mA})$, we write the change in the output voltage as:

$$
\begin{align*}
\Delta V_{\text {out }} & =\Delta I_{D} \cdot\left(3 r_{d}\right)  \tag{3.72}\\
& =0.5 \mathrm{~mA}(3 \times 4.33 \Omega)  \tag{3.73}\\
& =6.5 \mathrm{mV} \tag{3.74}
\end{align*}
$$

Exercise $\quad$ Repeat the above example if $R_{1}$ is reduced to $80 \Omega$.

Did you know?

What would our life be like without diodes? Forget about cell phones, laptops, and digital cameras. We would not even have radios, TVs, GPS, radars, satellites, power plants, or long-distance telephone communication. And, of course, no Google or Facebook. In essence, we would return to the simple lifestyle of the early 1900s-which might not be that bad after all ...

In summary, the analysis of circuits containing diodes (and other nonlinear devices such as transistors) proceeds in three steps: (1) determine-perhaps with the aid of the constant-voltage model-the initial values of voltages and currents (before an input change is applied); (2) develop the small-signal model for each diode (i.e., calculate $r_{d}$ ); (3) replace each diode with its small-signal model and compute the effect of the input change.

## 3.5 APPLICATIONS OF DIODES

The remainder of this chapter deals with circuit applications of diodes. A brief outline is shown below.

| Half-Wave and <br> Full-Wave rectifiers | Limiting <br> Circuits |
| :---: | :---: |
| Voltage <br> Doublers | Level Shifters <br> and Switches |

Figure 3.27 Applications of diodes.

### 3.5.1 Half-Wave and Full-Wave Rectifiers

Half-Wave Rectifier Let us return to the rectifier circuit of Fig. 3.10(b) and study it more closely. In particular, we no longer assume $D_{1}$ is ideal, but use a constant-voltage model. As illustrated in Fig. 3.28, $V_{\text {out }}$ remains equal to zero until $V_{\text {in }}$ exceeds $V_{D, \text { on }}$, at which point $D_{1}$ turns on and $V_{\text {out }}=V_{\text {in }}-V_{D, \text { on }}$. For $V_{\text {in }}<V_{D, \text { on }}, D_{1}$ is off ${ }^{11}$ and $V_{\text {out }}=0$. Thus, the circuit still operates as a rectifier but produces a slightly lower dc level.
image_name:Figure 3.28 Simple rectifier
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: D1, type: Diode, ports: {Na: Vin, Nc: Vout}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a simple rectifier using a diode D1 and a resistor R1. It allows current to pass only when the input voltage Vin exceeds the diode's threshold voltage VD,on, producing a rectified output voltage Vout.
image_name:
description:The graph on the right side of the image represents a time-domain waveform for a simple rectifier circuit. The horizontal axis is labeled as time \( t \), while the vertical axis represents voltage. The graph shows two waveforms: \( V_{\text{in}} \) and \( V_{\text{out}} \). \( V_{\text{in}} \) is a sinusoidal input voltage, depicted as a continuous wave oscillating above and below zero. \( V_{\text{out}} \) is the output voltage, which is zero until the input voltage exceeds the threshold voltage \( V_{D, \text{on}} \). At this point, the diode \( D_1 \) turns on, and the output voltage follows the input voltage minus the diode's forward voltage \( V_{D, \text{on}} \). \( V_{\text{out}} \) is shown as a clipped waveform, only allowing the positive half-cycles of \( V_{\text{in}} \) to pass through when \( V_{\text{in}} > V_{D, \text{on}} \). The graph illustrates the rectifying behavior of the circuit, which blocks the negative half-cycles and allows the positive ones, reduced by \( V_{D, \text{on}} \), to appear at the output.

Figure 3.28 Simple rectifier.
${ }^{11}$ If $V_{i n}<0, D_{1}$ carries a small leakage current, but the effect is negligible.

Prove that the circuit shown in Fig. 3.29(a) is also a rectifier.
image_name:Figure 3.28 Simple rectifier
description:
[

]
extrainfo:The image is not related to the circuit diagram or devices mentioned in the context. It appears to be a simple image containing the number '3.23' with no additional circuit information.
image_name:Figure 3.29 Rectification of positive cycles
description:The graph in Figure 3.29 illustrates the rectification of positive cycles in a circuit using a diode. This is a time-domain waveform graph, where the x-axis represents time (usually in seconds or milliseconds) and the y-axis represents voltage (in volts).

Axes Labels and Units
- **X-axis:** Time (units not specified, typically milliseconds or seconds)
- **Y-axis:** Voltage (Volts)

Overall Behavior and Trends
The graph displays the input and output voltage waveforms of a rectifying circuit. The input waveform is a sinusoidal signal, exhibiting both positive and negative half-cycles. However, the output waveform only shows the positive half-cycles, indicating that the negative half-cycles have been blocked by the rectifier.

Key Features and Technical Details
- **Positive Half-Cycles:** The positive half-cycles of the input waveform are allowed to pass through the rectifier, but they are slightly reduced in amplitude by the diode's forward voltage drop (denoted as \( V_{D, \text{on}} \)).
- **Negative Half-Cycles:** The negative half-cycles are blocked and do not appear in the output waveform, demonstrating the rectifying behavior of the circuit.
- **Amplitude Reduction:** The output waveform's amplitude is slightly less than the input due to the diode's forward voltage drop.

Annotations and Specific Data Points
- **Diode Forward Voltage Drop:** The graph may indicate the forward voltage drop of the diode, \( V_{D, \text{on}} \), which is the threshold above which the diode conducts the positive half-cycles.

This graph effectively demonstrates the basic operation of a rectifier circuit, which allows only the positive portion of an AC signal to pass through while blocking the negative portion.
image_name:(a)
description:
[

]
extrainfo:The image contains a label '3.23', which may refer to a figure or section number in a document. No circuit diagram or devices are present in the image.

image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: D1, type: Diode, ports: {Na: Vin, Nc: Vout}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit diagram represents a basic rectifier circuit using a diode and a resistor. It allows only the positive portion of an AC signal to pass through, blocking the negative portion.

(a)
image_name:Figure 3.29
description:The graph in Figure 3.29 is a time-domain waveform illustrating the behavior of a rectifier circuit. The x-axis represents time (t), while the y-axis represents voltage. There are two waveforms depicted: \( V_{in} \) and \( V_{out} \).

1. **Type of Graph and Function**:
- This is a time-domain waveform graph showing the input and output voltages of a rectifier circuit.

2. **Axes Labels and Units**:
- The x-axis is labeled as time \( t \), with no specific units provided, suggesting a general representation of time.
- The y-axis represents voltage, with the input voltage \( V_{in} \) and output voltage \( V_{out} \) marked.

3. **Overall Behavior and Trends**:
- The input voltage \( V_{in} \) is a sinusoidal waveform, showing both positive and negative cycles.
- The output voltage \( V_{out} \) is depicted as a waveform that only allows the negative cycles to pass, blocking the positive cycles entirely, which is characteristic of a rectifier that blocks positive cycles.

4. **Key Features and Technical Details**:
- The input waveform \( V_{in} \) is a smooth, continuous sine wave.
- The output waveform \( V_{out} \) is zero during the positive cycles of \( V_{in} \) and follows the negative cycles, indicating the diode's behavior of allowing only negative voltages to pass.

5. **Annotations and Specific Data Points**:
- The graph shows the transition points where \( V_{out} \) switches from zero to following \( V_{in} \) during the negative cycles.
- There are no specific numerical values or annotations on the graph, indicating a general representation of the rectification process.

(b)

Figure 3.29 Rectification of positive cycles.
Solution In this case, $D_{1}$ remains on for negative values of $V_{i n}$, specifically, for $V_{i n} \leq-V_{D, o n}$. As $V_{\text {in }}$ exceeds $-V_{D, \text { on }}, D_{1}$ turns off, allowing $R_{2}$ to maintain $V_{\text {out }}=0$. Depicted in Fig. 3.29, the resulting output reveals that this circuit is also a rectifier, but it blocks the positive cycles.

Exercise Plot the output if $D_{1}$ is an ideal diode.

Called a "half-wave rectifier," the circuit of Fig. 3.28 does not produce a useful output. Unlike a battery, the rectifier generates an output that varies considerably with time and cannot supply power to electronic devices. We must therefore attempt to create a constant output.

Fortunately, a simple modification solves the problem. As depicted in Fig. 3.30(a), the resistor is replaced with a capacitor. The operation of this circuit is quite different from that of the above rectifier. Assuming a constant-voltage model for $D_{1}$ in forward bias, we begin with a zero initial condition across $C_{1}$ and study the behavior of the circuit [Fig. 3.30(b)]. As $V_{\text {in }}$ rises from zero, $D_{1}$ is off until $V_{i n}>V_{D, o n}$, at which point $D_{1}$ begins to act as a battery and $V_{\text {out }}=V_{\text {in }}-V_{D, \text { on }}$. Thus, $V_{\text {out }}$ reaches a peak value of $V_{p}-V_{D, \text { on }}$. What happens as $V_{\text {in }}$
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: D1, type: Diode, ports: {Na: Vin, Nc: Vout}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit in Figure 3.30 (a) is a diode-capacitor rectifier circuit. It rectifies the input voltage Vin to produce a DC output voltage Vout. The diode D1 conducts when Vin exceeds the diode's threshold voltage, charging the capacitor C1. When Vin falls, the diode turns off, and the capacitor holds the charge, maintaining the output voltage.
image_name:(b)
description:The graph in Figure 3.30(b) depicts the input and output waveforms of a diode-capacitor rectifier circuit. The x-axis represents time \( t \), while the y-axis represents voltage. The graph is in the time domain, showing the behavior of the input voltage \( V_{\text{in}} \) and the output voltage \( V_{\text{out}} \) over time.

**Axes Labels and Units:**
- **X-axis:** Time \( t \) (units not specified, typically seconds or milliseconds)
- **Y-axis:** Voltage (units not specified, typically volts)

**Overall Behavior and Trends:**
- The input voltage \( V_{\text{in}} \) is a sinusoidal waveform, reaching a peak value \( V_p \).
- The output voltage \( V_{\text{out}} \) follows the input voltage until \( V_{\text{in}} \) exceeds the diode’s forward voltage drop \( V_{D, \text{on}} \). Beyond this point, \( V_{\text{out}} = V_{\text{in}} - V_{D, \text{on}} \).
- As \( V_{\text{in}} \) decreases after reaching its peak, \( V_{\text{out}} \) remains constant at \( V_p - V_{D, \text{on}} \) due to the capacitor \( C_1 \) holding the charge.

**Key Features and Technical Details:**
- At time \( t_1 \), \( V_{\text{in}} \) reaches its peak \( V_p \), and \( V_{\text{out}} = V_p - V_{D, \text{on}} \).
- The diode turns off after \( t_1 \) as \( V_{\text{in}} \) begins to fall, keeping \( V_{\text{out}} \) constant due to the capacitor.
- The output remains constant until \( t_3 \) when \( V_{\text{in}} \) rises again, repeating the cycle.
- The maximum reverse voltage across the diode is indicated on the graph.

**Annotations and Specific Data Points:**
- The graph includes annotations for \( V_p \), \( V_p - V_{D, \text{on}} \), and \( V_{D, \text{on}} \).
- Specific time points \( t_1, t_2, t_3, t_4, \) and \( t_5 \) are marked, showing the critical points of the waveform behavior.

Figure 3.30 (a) Diode-capacitor circuit, (b) input and output waveforms.
passes its peak value? At $t=t_{1}$, we have $V_{\text {in }}=V_{p}$ and $V_{\text {out }}=V_{p}-V_{D, o n}$. As $V_{\text {in }}$ begins to fall, $V_{\text {out }}$ must remain constant. This is because if $V_{\text {out }}$ were to fall, then $C_{1}$ would need to be discharged by a current flowing from its top plate through the cathode of $D_{1}$, which is impossible. ${ }^{12}$ The diode therefore turns off after $t_{1}$. At $t=t_{2}, V_{\text {in }}=V_{p}-V_{D, \text { on }}=V_{\text {out }}$, i.e., the diode sustains a zero voltage difference. At $t>t_{2}, V_{\text {in }}<V_{\text {out }}$ and the diode experiences a negative voltage.

Continuing our analysis, we note that at $t=t_{3}, V_{\text {in }}=-V_{p}$, applying a maximum reverse bias of $V_{\text {out }}-V_{\text {in }}=2 V_{p}-V_{D, \text { on }}$ across the diode. For this reason, diodes used in rectifiers must withstand a reverse voltage of approximately $2 V_{p}$ with no breakdown.

Does $V_{\text {out }}$ change after $t=t_{1}$ ? Let us consider $t=t_{4}$ as a potentially interesting point. Here, $V_{\text {in }}$ just exceeds $V_{\text {out }}$ but still cannot turn $D_{1}$ on. At $t=t_{5}$, $V_{\text {in }}=V_{p}=V_{\text {out }}+V_{D, \text { on }}$, and $D_{1}$ is on, but $V_{\text {out }}$ exhibits no tendency to change because the situation is identical to that at $t=t_{1}$. In other words, $V_{\text {out }}$ remains equal to $V_{p}-V_{D, \text { on }}$ indefinitely.

Example Assuming an ideal diode model, (a) Repeat the above analysis. (b) Plot the voltage across $D_{1}, V_{D 1}$, as a function of time.

Solution (a) With a zero initial condition across $C_{1}, D_{1}$ turns on as $V_{\text {in }}$ exceeds zero and $V_{\text {out }}=V_{\text {in }}$. After $t=t_{1}, V_{\text {in }}$ falls below $V_{\text {out }}$, turning $D_{1}$ off. Figure 3.31(a) shows the input and output waveforms.
image_name:Figure 3.31(a)
description:**Type of Graph and Function:**
The graph is a time-domain waveform showing the behavior of input and output voltages over time for a circuit with an ideal diode.

**Axes Labels and Units:**
- The horizontal axis represents time \( t \), though no specific units are provided, it's typically in seconds or milliseconds.
- The vertical axis represents voltage, with the input voltage \( V_{in} \) and output voltage \( V_{out} \) labeled.

**Overall Behavior and Trends:**
- The input voltage \( V_{in} \) is shown as a dashed sinusoidal waveform, indicating a periodic signal with both positive and negative cycles.
- The output voltage \( V_{out} \) is shown as a solid line that initially follows the input voltage until a certain point \( t_1 \), after which it remains constant.

**Key Features and Technical Details:**
- At time \( t_1 \), the input voltage \( V_{in} \) begins to drop below the output voltage \( V_{out} \), causing the diode to turn off and the output to remain constant.
- The output voltage \( V_{out} \) appears to maintain a constant value equal to the peak of the input voltage before \( t_1 \).

**Annotations and Specific Data Points:**
- The graph marks the time \( t_1 \) where the transition occurs between the input following the output and the output maintaining a constant value.
- The behavior of the diode is implied by the change in the relationship between \( V_{in} \) and \( V_{out} \) at \( t_1 \).

(a)
image_name:(b)
description:The graph represents the voltage across a diode, denoted as \( V_{D1} \), plotted against time \( t \). This is a time-domain waveform showing the behavior of the diode voltage in relation to the input voltage.

**Axes Labels and Units:**
- The horizontal axis represents time \( t \), with no specific units or scale provided.
- The vertical axis represents the diode voltage \( V_{D1} \).

**Overall Behavior and Trends:**
- The waveform resembles a sinusoidal pattern that is shifted downward. It oscillates around a baseline that is below zero.
- The waveform starts at a maximum negative value and rises to a peak before descending again, repeating this cycle.

**Key Features and Technical Details:**
- The waveform has a distinct baseline at \(-2V_p\), indicating that the average value of \( V_{D1} \) is shifted by \(-V_p\) from zero.
- The time \( t_1 \) is marked on the graph, indicating a significant point in time where a transition occurs.
- The waveform is periodic, suggesting a regular oscillation pattern.

**Annotations and Specific Data Points:**
- The graph is annotated with \(-2V_p\) as a reference line, highlighting the shifted average value of the waveform.
- \( t_1 \) is annotated, marking a critical point in the time axis where the behavior of the waveform might change or where the transition in the circuit's operation is noted.

(b)

Figure 3.31 (a) Input and output waveforms of the circuit in Fig. 3.30 with an ideal diode, (b) voltage across the diode.

[^4](b) The voltage across the diode is $V_{D 1}=V_{\text {in }}-V_{\text {out }}$. Using the plots in Fig. 3.31(a), we readily arrive at the waveform in Fig. 3.31(b). Interestingly, $V_{D 1}$ is similar to $V_{i n}$ but with the average value shifted from zero to $-V_{p}$. We will exploit this result in the design of voltage doublers (Section 3.5.4).

Exercise Repeat the above example if the terminals of the diode are swapped.

The circuit of Fig. 3.30(a) achieves the properties required of an "ac-dc converter," generating a constant output equal to the peak value of the input sinusoid. ${ }^{13}$ But how is the value of $C_{1}$ chosen? To answer this question, we consider a more realistic application where this circuit must provide a current to a load.

Example A laptop computer consumes an average power of 25 W with a supply voltage of 3.3 V .
3.25 Determine the average current drawn from the batteries or the adaptor.

Solution $\quad$ Since $P=V \cdot I$, we have $I \approx 7.58 \mathrm{~A}$. If the laptop is modeled by a resistor, $R_{L}$, then $R_{L}=V / I=0.436 \Omega$.

Exercise What power dissipation does a 1- $\Omega$ load represent for such a supply voltage?

As suggested by the above example, the load can be represented by a simple resistor in some cases [Fig. 3.32(a)]. We must therefore repeat our analysis with $R_{L}$ present. From the waveforms in Fig. 3.32(b), we recognize that $V_{\text {out }}$ behaves as before until $t=t_{1}$, still exhibiting a value of $V_{\text {in }}-V_{D, o n}=V_{p}-V_{D, o n}$ if the diode voltage is assumed relatively constant. However, as $V_{\text {in }}$ begins to fall after $t=t_{1}$, so does $V_{\text {out }}$ because $R_{L}$ provides a discharge path for $C_{1}$. Of course, since changes in $V_{\text {out }}$ are undesirable, $C_{1}$ must be so large that the current drawn by $R_{L}$ does not reduce $V_{\text {out }}$ significantly. With such a choice of $C_{1}$, $V_{\text {out }}$ falls slowly and $D_{1}$ remains reverse biased.
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: D1, type: Diode, ports: {Na: Vin, Nc: Vout}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a rectifier driving a resistive load. It uses a diode to allow current flow in one direction, charging the capacitor C1, which smooths the output voltage. The resistor RL provides a discharge path for C1, affecting the output voltage when Vin decreases.
image_name:(b)
description:The graph labeled as (b) is a time-domain waveform illustrating the behavior of both input voltage (Vin) and output voltage (Vout) over time in a rectifier circuit driving a resistive load.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform plot showing voltage changes over time.

2. **Axes Labels and Units:**
- The horizontal axis represents time (t), though units are not explicitly provided, it is typically in seconds or milliseconds in such contexts.
- The vertical axis represents voltage, typically in volts (V).

3. **Overall Behavior and Trends:**
- The input voltage (Vin) is shown as a sinusoidal waveform, indicating it is alternating in nature.
- The output voltage (Vout) follows the input voltage initially but maintains a more constant value after peaking, before gradually decreasing.
- The waveform shows that Vout initially rises with Vin, reaching a peak and then slowly declining as Vin goes negative.

4. **Key Features and Technical Details:**
- At time t1, both Vin and Vout reach their maximum values, with Vout slightly lower due to the forward voltage drop across the diode (V_D,on).
- As Vin decreases, Vout also decreases but at a slower rate, due to the discharge of the capacitor C1 through the resistive load RL.
- At time t2, Vin and Vout become equal, and shortly after at t3, Vin exceeds Vout by the diode's forward voltage, turning the diode on again.
- This process repeats, maintaining Vout close to Vin minus the diode drop when the diode is forward-biased.

5. **Annotations and Specific Data Points:**
- The graph marks significant points such as t1, t2, and t3, which are crucial for understanding the timing of diode conduction and the voltage relationship changes.
- The peak voltage (Vp) and voltage drop (VR) are annotated to show the maximum output voltage and the reduction due to the diode drop, respectively.

Figure 3.32 (a) Rectifier driving a resistive load, (b) input and output waveforms.

[^5]The output voltage continues to decrease while $V_{i n}$ goes through a negative excursion and returns to positive values. At some point, $t=t_{2}, V_{\text {in }}$ and $V_{\text {out }}$ become equal and slightly later, at $t=t_{3}, V_{\text {in }}$ exceeds $V_{\text {out }}$ by $V_{D, o n}$, thereby turning $D_{1}$ on and forcing $V_{\text {out }}=V_{\text {in }}-V_{D, \text { on }}$. Hereafter, the circuit behaves as in the first cycle. The resulting variation in $V_{\text {out }}$ is called the "ripple." Also, $C_{1}$ is called the "smoothing" or "filter" capacitor.

Sketch the output waveform of Fig. 3.32 as $C_{1}$ varies from very large values to very small values.

Solution If $C_{1}$ is very large, the current drawn by $R_{L}$ when $D_{1}$ is off creates only a small change in $V_{\text {out }}$. Conversely, if $C_{1}$ is very small, the circuit approaches that in Fig. 3.28, exhibiting large variations in $V_{\text {out }}$. Figure 3.33 illustrates several cases.
image_name:Figure 3.33
description:The graph in Figure 3.33 is a time-domain waveform illustrating the output voltage, \( V_{out} \), of a rectifier circuit for different values of the smoothing capacitor, \( C_1 \). The x-axis represents time \( t \), while the y-axis represents voltage. The input voltage \( V_{in} \) is shown as a reference waveform, which is a sinusoidal wave.

**Overall Behavior and Trends:**
- **Very Small \( C_1 \):** The output waveform closely follows the input sinusoidal waveform, indicating large variations in \( V_{out} \) and high ripple amplitude. This is because the small capacitor cannot store enough charge to smooth out the variations effectively.
- **Small \( C_1 \):** The output waveform shows reduced ripple compared to the very small \( C_1 \) case. The peaks are smoother, but there is still noticeable variation in \( V_{out} \).
- **Large \( C_1 \):** The output waveform is significantly smoothed out, with minimal ripple. The waveform maintains a more constant DC level with only slight variations, indicating that the large capacitor effectively smooths the output voltage.

**Key Features and Technical Details:**
- The graph shows how increasing the capacitance of \( C_1 \) reduces the ripple in the output voltage, leading to a smoother DC output.
- The peak-to-peak amplitude of the ripple decreases as \( C_1 \) increases, demonstrating the capacitor's role in filtering.

**Annotations and Specific Data Points:**
- The graph is annotated with labels indicating the different scenarios for \( C_1 \): 'Very Small \( C_1 \)', 'Small \( C_1 \)', and 'Large \( C_1 \)'.
- The input voltage \( V_{in} \) is shown as a reference, illustrating the effect of the smoothing capacitor on the output waveform.

Figure 3.33 Output waveform of rectifier for different values of smoothing capacitor.

Exercise $\quad$ Repeat the above example for different values of $R_{L}$ with $C_{1}$ constant.

Ripple Amplitude* In typical applications, the (peak-to-peak) amplitude of the ripple, $V_{R}$, in Fig. 3.32(b) must remain below 5 to $10 \%$ of the input peak voltage. If the maximum current drawn by the load is known, the value of $C_{1}$ is chosen large enough to yield an acceptable ripple. To this end, we must compute $V_{R}$ analytically (Fig. 3.34). Since $V_{\text {out }}=V_{p}-V_{D, \text { on }}$ at $t=t_{1}$, the discharge of $C_{1}$ through $R_{L}$ can be expressed as:

$$
\begin{equation*}
V_{\text {out }}(t)=\left(V_{p}-V_{D, \text { on }}\right) \exp \frac{-t}{R_{L} C_{1}} \quad 0 \leq t \leq t_{3} \tag{3.75}
\end{equation*}
$$

where we have chosen $t_{1}=0$ for simplicity. To ensure a small ripple, $R_{L} C_{1}$ must be much greater than $t_{3}-t_{1}$; thus, noting that $\exp (-\epsilon) \approx 1-\epsilon$ for $\epsilon \ll 1$,

$$
\begin{align*}
V_{\text {out }}(t) \approx & \left(V_{p}-V_{D, \text { on }}\right)\left(1-\frac{t}{R_{L} C_{1}}\right)  \tag{3.76}\\
& \approx\left(V_{p}-V_{D, \text { on }}\right)-\frac{V_{p}-V_{D, \text { on }}}{R_{L}} \cdot \frac{t}{C_{1}} \tag{3.77}
\end{align*}
$$

[^6]image_name:Figure 3.34 Ripple at output of a rectifier
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: D1, type: Diode, ports: {Na: Vin, Nc: Vout}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a rectifier with a diode (D1) and a smoothing capacitor (C1) connected to a load resistor (RL). It converts AC input voltage (Vin) to a DC output voltage (Vout) with reduced ripple.

(a)
image_name:Figure 3.34 Ripple at output of a rectifier
description:The graph in Figure 3.34 illustrates the ripple voltage at the output of a rectifier circuit. It is a time-domain waveform that shows how the output voltage (Vout) varies over time (t), following the rectification of an AC input voltage (Vin).

1. **Type of Graph and Function:**
- This is a time-domain waveform graph depicting the behavior of a rectified voltage output from a diode-capacitor rectifier circuit.

2. **Axes Labels and Units:**
- The horizontal axis represents time (t), though specific units are not provided, it is typically in seconds or milliseconds for such circuits.
- The vertical axis represents voltage, with significant levels marked as \( V_p \) (peak voltage), \( V_{p} - V_{D,on} \) (peak voltage minus diode forward voltage), and \( V_R \) (voltage ripple).

3. **Overall Behavior and Trends:**
- The graph shows a waveform that starts at a peak voltage \( V_p \) and then decreases linearly, representing the discharge of the capacitor over time.
- The waveform exhibits a ripple characteristic after each peak, indicating the voltage drop as the capacitor discharges through the load resistor.
- The waveform then rises again as the input AC voltage reaches its next peak, with the cycle repeating.

4. **Key Features and Technical Details:**
- Peaks occur at \( V_p \), where the diode conducts and the capacitor charges up to the peak input voltage minus the diode's forward voltage drop.
- The falling edge of the waveform represents the discharge of the capacitor through the load resistor \( R_L \), with a relatively constant slope indicating a near-constant discharge current.
- The ripple voltage \( V_R \) is the difference between the peak voltage and the lowest point of the waveform before the next charging cycle begins.

5. **Annotations and Specific Data Points:**
- Specific time points \( t_1, t_2, t_3, \) and \( t_4 \) are marked, representing key phases in the charging and discharging cycle of the capacitor.
- The graph is annotated with the circuit diagram below, showing the diode, capacitor, and resistor configuration, highlighting the rectification process and smoothing effect of the capacitor.
image_name:(a)
description:
[
name: SW, type: Switch, ports: {N1: LOAD, N2: Xb}
name: C, type: Capacitor, value: C, ports: {Np: X1, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: X1, N2: GND}
]
extrainfo:The circuit diagram represents a rectifier with a smoothing capacitor and a load resistor. The switch (SW) controls the input from the load (LOAD) to the circuit, passing through a capacitor (C) and a resistor (R) connected in parallel, both grounded. The graph above the circuit shows the ripple voltage at the output (Vout) and the effect of the smoothing capacitor in reducing the ripple.

(b)

Figure 3.34 Ripple at output of a rectifier.

The first term on the right-hand side represents the initial condition across $C_{1}$ and the second term, a falling ramp-as if a constant current equal to $\left(V_{p}-V_{D, o n}\right) / R_{L}$ discharges $C_{1}{ }^{14}$ This result should not come as a surprise because the nearly constant voltage across $R_{L}$ results in a relatively constant current equal to $\left(V_{p}-V_{D, \text { on }}\right) / R_{L}$.

The peak-to-peak amplitude of the ripple is equal to the amount of discharge at $t=t_{3}$. Since $t_{4}-t_{3}$ is equal to the input period, $T_{i n}$, we write $t_{3}-t_{1}=T_{\text {in }}-\Delta T$, where $\Delta T\left(=t_{4}-t_{3}\right)$ denotes the time during which $D_{1}$ is on. Thus,

$$
\begin{equation*}
V_{R}=\frac{V_{p}-V_{D . m}}{R_{L}} \frac{T_{n-n}-\Delta T}{C_{1}} \tag{3.78}
\end{equation*}
$$

Recognizing that if $C_{1}$ discharges by a small amount, then the diode turns on for only a brief period, we can assume $\Delta T \ll T_{i n}$ and hence

$$
\begin{align*}
V_{R} & \approx \frac{V_{p}-V_{D . m}}{R_{L}} \cdot \frac{T_{i}}{C_{1}}  \tag{3.79}\\
& \approx \frac{V_{p}-V_{D, \text { em }}}{R_{L} C_{1} f_{m}} \tag{3.80}
\end{align*}
$$

where $f_{\text {in }}=T_{\text {in }}^{-1}$.

Example 3.97

A transformer converts the $110-\mathrm{V}, 60-\mathrm{Hz}$ line voltage to a peak-to-peak swing of 9 V . A half-wave rectifier follows the transformer to supply the power to the laptop computer of Example 3.25. Determine the minimum value of the filter capacitor that maintains the ripple below 0.1 V . Assume $V_{D . . . m}=0.8 \mathrm{~V}$.

Solution We have $V_{p}=4.5 \mathrm{~V}, R_{L}=0.436 \Omega$, and $T_{\text {in }}=16.7 \mathrm{~ms}$. Thus,

$$
\begin{align*}
C_{1} & =\frac{V_{p}-V_{D, a n}}{V_{R}} \cdot \frac{T_{\text {k }}}{R_{L}}  \tag{3.81}\\
& =1.417 \mathrm{~F} . \tag{3.82}
\end{align*}
$$

[^7]This is a very large value. The designer must trade the ripple amplitude with the size, weight, and cost of the capacitor. In fact, limitations on size, weight, and cost of the adaptor may dictate a much greater ripple, e.g., 0.5 V , thereby demanding that the circuit following the rectifier tolerate such a large, periodic variation.

Exercise Repeat the above example for $220-\mathrm{V}, 50-\mathrm{Hz}$ line voltage, assuming the transformer still produces a peak-to-peak swing of 9 V . Which mains frequency gives a more desirable choice of $C_{1}$ ?

In many cases, the current drawn by the load is known. Repeating the above analysis with the load represented by a constant current source or simply viewing $\left(V_{p}-V_{D, o n}\right) / R_{L}$ in Eq. (3.80) as the load current, $I_{L}$, we can write

$$
\begin{equation*}
V_{R}=\frac{I_{L}}{C_{1} f_{i n}} \tag{3.83}
\end{equation*}
$$

Diode Peak Current* We noted in Fig. 3.30(b) that the diode must exhibit a reverse breakdown voltage of at least $2 \mathrm{~V}_{p}$. Another important parameter of the diode is the maximum forward bias current that it must tolerate. For a given junction doping profile and geometry, if the current exceeds a certain limit, the power dissipated in the diode $\left(=V_{D} I_{D}\right)$ may raise the junction temperature so much as to damage the device.
image_name:Figure 3.35 Rectifier circuit for calculation of I_D
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: D1, type: Diode, ports: {Na: Vin, Nc: Vout}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a rectifier circuit used to calculate the diode current (I_D). It consists of a diode (D1), a capacitor (C1), a resistor (RL), and a voltage source (Vin). The diode allows current to pass when forward-biased, and the capacitor smooths the output voltage. The resistor represents the load.
image_name:
description:The graph provided illustrates the behavior of a rectifier circuit, specifically focusing on the input and output voltage waveforms over time.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform, depicting the input and output voltages of a rectifier circuit.

2. **Axes Labels and Units:**
- The horizontal axis represents time (t), though specific units are not provided.
- The vertical axis represents voltage, with key values indicated as \( V_p \) (peak voltage) and \( V_R \) (reference voltage).

3. **Overall Behavior and Trends:**
- The input voltage \( V_{in} \) is a sinusoidal waveform, shown in gray, with peaks reaching \( V_p \).
- The output voltage \( V_{out} \), shown in black, follows the input but is clipped and shifted, maintaining a more constant level after the peak of \( V_{in} \).
- The waveform indicates the charging and discharging behavior typical of a rectifier circuit with a smoothing capacitor \( C_1 \).

4. **Key Features and Technical Details:**
- The output waveform \( V_{out} \) does not drop below a certain level \( V_p - V_R \), indicating the effect of the capacitor smoothing the output.
- At time \( t_1 \), the diode \( D_1 \) turns on, allowing the capacitor to charge, which is shown by the increase in \( V_{out} \) following the peak of \( V_{in} \).
- The graph highlights the peak voltage \( V_p \) and the reference voltage \( V_R \) as critical levels for understanding the operation of the rectifier.

5. **Annotations and Specific Data Points:**
- The graph includes a horizontal dashed line at \( V_p \) and \( V_p - V_R \), marking significant voltage levels.
- The point \( t_1 \) is annotated, indicating the moment when the diode conducts, and the capacitor begins charging.

This graph effectively demonstrates the rectifier's operation, showing how the diode and capacitor work together to produce a smoothed DC output from an AC input.

Figure 3.35 Rectifier circuit for calculation of $I_{D}$.
We recognize from Fig. 3.35, that the diode current in forward bias consists of two components: (1) the transient current drawn by $C_{1}, C_{1} d V_{\text {out }} / d t$, and (2) the current supplied to $R_{L}$, approximately equal to $\left(V_{p}-V_{D, o n}\right) / R_{L}$. The peak diode current therefore occurs when the first component reaches a maximum, i.e., at the point $D_{1}$ turns on because the slope of the output waveform is maximum. Assuming $V_{D, o n} \ll V_{p}$ for simplicity, we note that the point at which $D_{1}$ turns on is given by $V_{i n}\left(t_{1}\right)=V_{p}-V_{R}$. Thus, for $V_{\text {in }}(t)=V_{p} \sin \omega_{\text {in }} t$,

$$
\begin{equation*}
V_{p} \sin \omega_{i n} t_{1}=V_{p}-V_{R} \tag{3.84}
\end{equation*}
$$

and hence

$$
\begin{equation*}
\sin \omega_{i n} t_{1}=1-\frac{V_{R}}{V_{p}} \tag{3.85}
\end{equation*}
$$

*This section can be skipped in a first reading.

With $V_{D, \text { on }}$ neglected, we also have $V_{\text {out }}(t) \approx V_{\text {in }}(t)$, obtaining the diode current as

$$
\begin{align*}
I_{D 1}(t) & =C_{1} \frac{d V_{\text {out }}}{d t}+\frac{V_{p}}{R_{L}}  \tag{3.86}\\
& =C_{1} \omega_{\text {in }} V_{p} \cos \omega_{\text {in }} t+\frac{V_{p}}{R_{L}} \tag{3.87}
\end{align*}
$$

This current reaches a peak at $t=t_{1}$ :

$$
\begin{equation*}
I_{p}=C_{1} \omega_{i n} V_{p} \cos \omega_{i n} t_{1}+\frac{V_{p}}{R_{L}} \tag{3.88}
\end{equation*}
$$

which, from (3.85), reduces to

$$
\begin{align*}
I_{p} & =C_{1} \omega_{i n} V_{p} \sqrt{1-\left(1-\frac{V_{R}}{V_{p}}\right)^{2}}+\frac{V_{p}}{R_{L}}  \tag{3.89}\\
& =C_{1} \omega_{i n} V_{p} \sqrt{\frac{2 V_{R}}{V_{p}}-\frac{V_{R}^{2}}{V_{p}^{2}}}+\frac{V_{p}}{R_{L}} \tag{3.90}
\end{align*}
$$

Since $V_{R} \ll V_{p}$, we neglect the second term under the square root:

$$
\begin{align*}
I_{p} & \approx C_{1} \omega_{i n} V_{p} \sqrt{\frac{2 V_{R}}{V_{p}}}+\frac{V_{p}}{R_{L}}  \tag{3.91}\\
& \approx \frac{V_{p}}{R_{L}}\left(R_{L} C_{1} \omega_{i n} \sqrt{\frac{2 V_{R}}{V_{p}}}+1\right) \tag{3.92}
\end{align*}
$$

Example Determine the peak diode current in Example 3.27 assuming $V_{D, \text { on }} \approx 0$ and $C_{1}=1.417 \mathrm{~F}$.

Solution We have $V_{p}=4.5 \mathrm{~V}, R_{L}=0.436 \Omega, \omega_{i n}=2 \pi(60 \mathrm{~Hz})$, and $V_{R}=0.1 \mathrm{~V}$. Thus,

$$
\begin{equation*}
I_{p}=517 \mathrm{~A} \tag{3.93}
\end{equation*}
$$

This value is extremely large. Note that the current drawn by $C_{1}$ is much greater than that flowing through $R_{L}$.

Exercise Repeat the above example if $C_{1}=1000 \mu \mathrm{~F}$.

Full-Wave Rectifier The half-wave rectifier studied above blocks the negative half cycles of the input, allowing the filter capacitor to be discharged by the load for almost the entire period. The circuit therefore suffers from a large ripple in the presence of a heavy load (a high current).

It is possible to reduce the ripple voltage by a factor of two through a simple modification. Illustrated in Fig. 3.36(a), the idea is to pass both positive and negative half cycles to the output, but with the negative half cycles inverted (i.e., multiplied by -1 ). We first implement a circuit that performs this function [called a "full-wave
image_name:(a)
description:The graph labeled (a) in Figure 3.36 depicts the input and output waveforms of a full-wave rectifier. It is a time-domain waveform graph.

1. **Type of Graph and Function:**
- The graph illustrates time-domain waveforms, showing how the input and output voltages vary over time.

2. **Axes Labels and Units:**
- The horizontal axis represents time \( t \), though no specific units are given. It is assumed to be in seconds or milliseconds, typical for such graphs.
- The vertical axes represent the input voltage \( x(t) \) and the output voltage \( y(t) \).

3. **Overall Behavior and Trends:**
- The input waveform \( x(t) \) is a sinusoidal wave, alternating between positive and negative peaks symmetrically around the horizontal axis.
- The output waveform \( y(t) \) is a series of positive half-sine waves. Each negative half-cycle of the input is inverted to become positive, resulting in a waveform that is entirely above the horizontal axis.

4. **Key Features and Technical Details:**
- The input waveform has both positive and negative peaks, indicating an AC signal.
- The output waveform has peaks at the same frequency as the input but with all cycles being positive, characteristic of a full-wave rectification process.
- The peaks of the output waveform align with the peaks of the input waveform, but the negative halves are inverted, doubling the frequency of peaks in the output compared to the input.

5. **Annotations and Specific Data Points:**
- There are no specific numerical values or gridlines provided, but the dashed lines indicate the transformation of the negative input cycles to positive output cycles.

This graph effectively demonstrates the function of a full-wave rectifier, converting an AC input into a pulsating DC output with reduced ripple voltage compared to a half-wave rectifier.
image_name:(b)
description:The graph in Figure 3.36(b) represents the input/output characteristic of a full-wave rectifier. This graph is composed of two parts: a plot on the left showing the relationship between input voltage \( V_{in} \) and output voltage \( V_{out} \), and a time-domain waveform on the right showing \( V_{out} \) over time \( t \).

1. **Type of Graph and Function:**
- The graph on the left is a piecewise linear function showing the input/output characteristic of a full-wave rectifier.
- The graph on the right is a time-domain waveform illustrating the output voltage over time.

2. **Axes Labels and Units:**
- Left Graph:
- Horizontal axis: \( V_{in} \) (Input Voltage)
- Vertical axis: \( V_{out} \) (Output Voltage)
- Right Graph:
- Horizontal axis: \( t \) (Time)
- Vertical axis: \( V_{out} \) (Output Voltage)

3. **Overall Behavior and Trends:**
- **Left Graph:**
- The input/output characteristic is V-shaped, indicating that the output voltage mirrors the absolute value of the input voltage. This behavior is typical of a full-wave rectifier, which inverts negative input voltages to positive outputs.
- **Right Graph:**
- The waveform shows a series of positive half-cycles, repeating periodically. This reflects the full-wave rectification process where both halves of the input AC signal are converted to positive output cycles.

4. **Key Features and Technical Details:**
- **Left Graph:**
- The graph has a sharp transition at the origin, indicating ideal diode behavior with no threshold voltage.
- **Right Graph:**
- The waveform has peaks at regular intervals, with no negative portions, showing that the rectifier outputs only positive voltages.

5. **Annotations and Specific Data Points:**
- There are no specific numerical annotations or markers, but the overall shape and transitions are indicative of the rectification process.

Figure 3.36 (a) Input and output waveforms and (b) input/output characteristic of a full-wave rectifier.
rectifier" (FWR)] and next prove that it indeed exhibits a smaller ripple. We begin with the assumption that the diodes are ideal to simplify the task of circuit synthesis. Figure 3.36(b) depicts the desired input/output characteristic of the full-wave rectifier.

Consider the two half-wave rectifiers shown in Fig. 3.37(a), where one blocks negative half cycles and the other, positive half cycles. Can we combine these circuits to realize a full-wave rectifier? We may attempt the circuit in Fig. 3.37(b), but, unfortunately, the output contains both positive and negative half cycles, i.e., no rectification is performed because the negative half cycles are not inverted. Thus, the problem is reduced to that illustrated in Fig. 3.37(c): we must first design a half-wave rectifier that inverts. Shown in Fig. 3.37(d) is such a topology, which can also be redrawn as in Fig. 3.37(e) for simplicity. Note the polarity of $V_{\text {out }}$ in the two diagrams. Here, if $V_{\text {in }}<0$, both $D_{2}$ and $D_{1}$ are on and $V_{\text {out }}=-V_{\text {in }}$. Conversely, if $V_{\text {in }}>0$, both diodes are off, yielding a zero current through $R_{L}$ and hence $V_{\text {out }}=0$. In analogy with this circuit, we also compose that in Fig. 3.37(f), which simply blocks the negative input half cycles; i.e., $V_{\text {out }}=0$ for $V_{\text {in }}<0$ and $V_{\text {out }}=V_{\text {in }}$ for $V_{i n}>0$.
image_name:(a)
description:
[
name: A1, type: VoltageSource, value: A1, ports: {Np: X1, Nn: GND}
name: D1, type: Diode, ports: {Na: X1, Nc: X5}
name: K1, type: Switch, ports: {N1: X5, N2: X6}
name: RL, type: Resistor, value: RL, ports: {N1: X6, N2: GND}
name: K2, type: Switch, ports: {N1: X7, N2: X8}
name: D2, type: Diode, ports: {Na: X8, Nc: X2}
name: A2, type: VoltageSource, value: A2, ports: {Np: X2, Nn: GND}
]
extrainfo:The circuit in Figure (a) is a rectifier circuit with two voltage sources (A1 and A2), two diodes (D1 and D2), two switches (K1 and K2), and a resistor (RL). It is designed to rectify and invert the input signal.
image_name:(b)
description:
[
name: D2, type: Diode, ports: {Na: X2, Nc: X4}
name: D1, type: Diode, ports: {Na: X4, Nc: X1}
name: RL, type: Resistor, value: RL, ports: {N1: X4, N2: GND}
]
extrainfo:Figure 3.37(b) demonstrates a configuration where diodes D1 and D2 are arranged in series opposition between nodes X2 and X1, with a resistor RL connected from node X4 to ground. This setup is used for rectification and inversion of an AC signal.
image_name:(c)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: X2, Nn: X1}
name: RL, type: Resistor, value: RL, ports: {N1: X3, N2: GND}
]
extrainfo:The circuit diagram (c) is a representation of a system with an unknown component between nodes X2 and X3. It is connected to a voltage source Vin between nodes X2 and X1, and a load resistor RL between nodes X3 and GND. The circuit appears to be part of a rectification or filtering system.
image_name:(d)
description:
[
name: D2, type: Diode, ports: {Na: X2, Nc: X4}
name: D1, type: Diode, ports: {Na: X1, Nc: X3}
name: RL, type: Resistor, value: RL, ports: {N1: X4, N2: X3}
]
extrainfo:This circuit diagram (d) represents a full-wave rectifier using diodes D1 and D2. The input voltage is applied across nodes X2 and X1, and the output is taken across nodes X4 and X3. The resistor RL is used as a load across the output.
image_name:(e)
description:
[
name: D2, type: Diode, ports: {Na: X2, Nc: X4}
name: RL, type: Resistor, value: RL, ports: {N1: X4, N2: X3}
name: D1, type: Diode, ports: {Na: X1, Nc: X3}
]
extrainfo:The circuit (e) is a rectifier that allows current flow during the positive half-cycle of the input voltage, resulting in a positive output voltage (Vout) across RL. Diodes D1 and D2 are arranged to conduct for positive input voltages, blocking negative input voltages.
image_name:(f)
description:
[
name: D3, type: Diode, ports: {Na: X2, Nc: X4}
name: D4, type: Diode, ports: {Na: X1, Nc: X3}
name: RL, type: Resistor, value: RL, ports: {N1: X4, N2: X3}
]
extrainfo:The circuit diagram (f) represents a full-wave rectifier with diodes D3 and D4. The diodes are arranged to conduct during opposite half cycles of the input AC signal. Diode D3 conducts during the positive half cycle, while D4 conducts during the negative half cycle. The resistor RL is the load, across which the rectified output voltage Vout is obtained.

Figure 3.37 (a) Rectification of each half cycle, (b) no rectification, (c) rectification and inversion, (d) realization of (c), (e) path for negative half cycles, (f) path for positive half cycles.
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: X2, Nn: X1}
name: RL, type: Resistor, value: RL, ports: {N1: X3, N2: X4}
name: D1, type: Diode, ports: {Na: X3, Nc: X2}
name: D2, type: Diode, ports: {Na: X2, Nc: X4}
name: D3, type: Diode, ports: {Na: X1, Nc: X3}
name: D4, type: Diode, ports: {Na: X4, Nc: X1}
]
extrainfo:The circuit in Figure 3.38(a) is a full-wave rectifier. It uses four diodes (D1, D2, D3, D4) arranged in a bridge configuration to convert an AC input voltage (Vin) into a DC output voltage across the load resistor (RL). The diodes conduct in pairs during each half cycle of the AC input, allowing current to flow through the load in the same direction during both half cycles, thus achieving full-wave rectification.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: X2, Nn: X1}
name: RL, type: Resistor, value: RL, ports: {N1: X6, N2: X3}
name: D1, type: Diode, ports: {Na: X4, Nc: X3}
name: D2, type: Diode, ports: {Na: X2, Nc: X6}
name: D3, type: Diode, ports: {Na: X6, Nc: X4}
name: D4, type: Diode, ports: {Na: X3, Nc: X5}
]
extrainfo:This is a full-wave rectifier circuit. It uses four diodes (D1, D2, D3, D4) arranged in a bridge configuration to convert an AC input voltage into a DC output voltage across the load resistor RL. During the positive half-cycle of the AC input, diodes D2 and D3 conduct, while during the negative half-cycle, diodes D1 and D4 conduct.
image_name:(c)
description:
[
name: RL, type: Resistor, value: RL, ports: {N1: k2, N2: k1}
name: D1, type: Diode, ports: {Na: k1, Nc: A1}
name: D2, type: Diode, ports: {Na: k2, Nc: A2}
name: D3, type: Diode, ports: {Na: A3, Nc: k2}
name: D4, type: Diode, ports: {Na: A4, Nc: A1}
]
extrainfo:The circuit (c) is a rectifier circuit that inverts the input signal. Diode D2 conducts during positive half cycles, while D1 conducts during negative half cycles. The load resistor RL is connected across nodes k2 and k1.
image_name:(d)
description:
[
name: RL, type: Resistor, ports: {N1: A4, N2: k3}
name: D1, type: Diode, ports: {Na: k4, Nc: k3}
name: D2, type: Diode, ports: {Na: A3, Nc: k3}
name: D3, type: Diode, ports: {Na: A3, Nc: A4}
name: D4, type: Diode, ports: {Na: A4, Nc: k4}
]
extrainfo:The circuit is a rectifier that processes positive half cycles through D3 and D4, and negative half cycles through D1 and D2. The load resistor RL is connected across nodes A4 and k3, providing the rectified output voltage Vout.

Figure 3.38 (a) Full-wave rectifier, (b) simplified diagram, (c) current path for negative input, (d) current path for positive input.

With the foregoing developments, we can now combine the topologies of Figs. 3.37(d) and (f) to form a full-wave rectifier. Depicted in Fig. 3.38(a), the resulting circuit passes the negative half cycles through $D_{1}$ and $D_{2}$ with a sign reversal [as in Fig. 3.37(d)] and the positive half cycles through $D_{3}$ and $D_{4}$ with no sign reversal [as in Fig. 3.37(f)]. This configuration is usually drawn as in Fig. 3.38(b)and called a "bridge rectifier."

Let us summarize our thoughts with the aid of the circuit shown in Fig. 3.38(b). If $V_{\text {in }}<0, D_{2}$ and $D_{1}$ are on and $D_{3}$ and $D_{4}$ are off, reducing the circuit to that shown in Fig. 3.38(c) and yielding $V_{\text {out }}=-V_{\text {in }}$. On the other hand, if $V_{\text {in }}>0$, the bridge is simplified as shown in Fig. 3.38(d), and $V_{\text {out }}=V_{\text {in }}$.

How do these results change if the diodes are not ideal? Figures 3.38(c) and (d) reveal that the circuit introduces two forward-biased diodes in series with $R_{L}$, yielding $V_{\text {out }}=-V_{\text {in }}-2 V_{D, \text { on }}$ for $V_{\text {in }}<0$. By contrast, the half-wave rectifier in Fig. 3.28produces $V_{\text {out }}=V_{\text {in }}-V_{D, \text { on }}$. The drop of $2 V_{D, \text { on }}$ may pose difficulty if $V_{p}$ is relatively small and the output voltage must be close to $V_{p}$.

Assuming a constant-voltage model for the diodes, plot the input/output characteristic of a full-wave rectifier.

Solution The output remains equal to zero for $\left|V_{i n}\right|<2 V_{D, \text { on }}$ and "tracks" the input for $\left|V_{i n}\right|>V_{D, \text { on }}$ with a slope of unity. Figure 3.39 plots the result.

Exercise What is the slope of the characteristic for $\left|V_{i n}\right|>2 V_{D, o n}$ ?

We now redraw the bridge once more and add the smoothing capacitor to arrive at the complete design [Fig. 3.40(a)]. Since the capacitor discharge occurs for about half of
image_name:Figure 3.39
description:The graph in Figure 3.39 represents the input/output characteristic of a full-wave rectifier with nonideal diodes. It consists of two parts: a Vout vs. Vin plot and a Vout vs. time plot.

1. **Vout vs. Vin Plot**:
- **Axes**: The horizontal axis is labeled as Vin, representing the input voltage, while the vertical axis is labeled as Vout, representing the output voltage.
- **Units**: The units are typically in volts, though not explicitly mentioned.
- **Behavior**: The graph shows a piecewise linear characteristic. For input voltages \(|Vin| < 2VD,on\), the output voltage remains at zero. Once the input voltage exceeds \(2VD,on\) in magnitude, the output starts to track the input with a slope of unity. This means that for \(Vin > 2VD,on\), Vout = Vin - 2VD,on, and similarly for \(Vin < -2VD,on\).
- **Key Features**: The critical points are at \(-2VD,on\) and \(+2VD,on\), where the output transitions from zero to following the input.

2. **Vout vs. Time Plot**:
- **Axes**: The horizontal axis is labeled as time \(t\), and the vertical axis is labeled as Vout.
- **Behavior**: The plot shows the typical output waveform of a full-wave rectifier, which consists of a series of arches or humps. This indicates that the output voltage is always positive and follows the absolute value of the input waveform.
- **Key Features**: The waveform is periodic, reflecting the input frequency, and shows the rectification process where both halves of the AC input are converted to positive output.

Overall, the graph illustrates the rectification process, showing how the full-wave rectifier outputs a voltage that follows the input for values beyond the diode threshold, while converting AC input into a pulsating DC output over time.

Figure 3.39 Input/output characteristic of full-wave rectifier with nonideal diodes.
the input cycle, the ripple is approximately equal to half of that in Eq. (3.80):

$$
\begin{equation*}
V_{R} \approx \frac{1}{2} \cdot \frac{V_{p}-2 V_{D, o n}}{R_{L} C_{1} f_{i n}} \tag{3.94}
\end{equation*}
$$

where the numerator reflects the drop of $2 V_{D, \text { on }}$ due to the bridge.
In addition to a lower ripple, the full-wave rectifier offers another important advantage: the maximum reverse bias voltage across each diode is approximately equal to $V_{p}$ rather than $2 V_{p}$. As illustrated in Fig. 3.40(b), when $V_{i n}$ is near $V_{p}$ and $D_{3}$ is on, the voltage across $D_{2}, V_{A B}$, is simply equal to $V_{D, \text { on }}+V_{\text {out }}=V_{p}-V_{D, \text { on }}$. A similar argument applies to the other diodes.
image_name:(b) equivalent circuit
description:
[
name: D1, type: Diode, ports: {Na: X2, Nc: Vout}
name: D2, type: Diode, ports: {Na: GND, Nc: X2}
name: D3, type: Diode, ports: {Na: Vout, Nc: X1}
name: D4, type: Diode, ports: {Na: X1, Nc: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a full-wave rectifier using a bridge configuration with diodes D1 to D4. It converts AC input to DC output, smoothing the output with a resistor RL and capacitor C1. The waveform shows reduced ripple in the output voltage.
image_name:(a) Ripple in full-wave rectifier
description:The graph titled "Ripple in full-wave rectifier" is a time-domain waveform representation of the input and output voltages of a full-wave rectifier circuit.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph showing the behavior of voltages over time.

2. **Axes Labels and Units:**
- The horizontal axis represents time (t), although specific units are not provided.
- The vertical axis represents voltage, with the input voltage ($V_{in}$) and output voltage ($V_{out}$) shown. No units are specified, but it is typically in volts.

3. **Overall Behavior and Trends:**
- The input voltage ($V_{in}$) is depicted as a sinusoidal waveform, illustrating an alternating current (AC) signal.
- The output voltage ($V_{out}$) is shown as a series of positive half-cycles, indicating the rectification process. The waveform is smoother compared to a half-wave rectifier, but it still contains some ripple.

4. **Key Features and Technical Details:**
- The $V_{in}$ waveform is a standard sine wave, crossing the time axis at zero, reaching a peak, and then descending.
- The $V_{out}$ waveform consists of successive positive half-cycles, demonstrating the full-wave rectification which converts both halves of the AC input into positive output.
- The ripple is visible as small oscillations on the $V_{out}$ waveform, which are minimized compared to a half-wave rectifier.

5. **Annotations and Specific Data Points:**
- The graph illustrates how the full-wave rectifier reduces ripple compared to the input signal, but specific numerical values or annotations are not provided in the image.

(a)
image_name:(b)
description:
[
name: D1, type: Diode, ports: {Na: Vout, Nc: X1}
name: D2, type: Diode, ports: {Na: A, Nc: B}
name: D3, type: Diode, ports: {Na: A, Nc: Vout}
name: D4, type: Diode, ports: {Na: B, Nc: X1}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: GND}
]
extrainfo:This is a full-wave bridge rectifier circuit with a smoothing capacitor (C1) and load resistor (RL). The diodes (D1, D2, D3, D4) form a bridge configuration that converts AC input voltage (Vin) into a DC output voltage (Vout). The ripple in the output is reduced by the capacitor. The circuit depicts a common ground node (GND) for the output.

Figure 3.40 (a) Ripple in full-wave rectifier, (b) equivalent circuit.

Another point of contrast between half-wave and full-wave rectifiers is that the former has a common terminal between the input and output ports (node $G$ in Fig. 3.28), whereas the latter does not. In Problem 3.40, we study the effect of shorting the input and output grounds of a full-wave rectifier and conclude that it disrupts the operation of the circuit.

Example Plot the currents carried by each diode in a bridge rectifier as a function of
3.30 time for a sinusoidal input. Assume no smoothing capacitor is connected to the output.

Solution From Figs. 3.38(c) and (d), we have $V_{\text {out }}=-V_{\text {in }}+2 V_{D, \text { on }}$ for $V_{\text {in }}<-2 V_{D, \text { on }}$ and $V_{\text {out }}=V_{\text {in }}-2 V_{D, \text { on }}$ for $V_{\text {in }}>+2 V_{D, \text { on }}$. In each half cycle, two of the diodes carry a current equal to $V_{\text {out }} / R_{L}$ and the other two remain off. Thus, the diode currents appear as shown in Fig. 3.41.
image_name:Figure 3.41 Currents carried by diodes in a full-wave rectifier.
description:The graph in Figure 3.41 represents the currents carried by diodes in a full-wave rectifier circuit. It consists of two main waveforms:

1. **Top Waveform (Input Voltage, $V_{in}$):**
- **Type of Graph:** Time-domain waveform.
- **Axes Labels:**
- Horizontal axis: Time ($t$).
- Vertical axis: Input voltage ($V_{in}$).
- **Overall Behavior and Trends:**
- The waveform is sinusoidal, representing the alternating input voltage.
- It has a positive peak followed by a negative peak, indicating a full cycle of AC voltage.
- **Key Features:**
- No specific numerical values are provided, but it is implied that the peaks correspond to the maximum and minimum voltages of the AC signal.

2. **Middle Waveform ($I_{D1} = I_{D2}$):**
- **Type of Graph:** Time-domain waveform representing diode currents.
- **Axes Labels:**
- Horizontal axis: Time ($t$).
- Vertical axis: Current through diodes $D1$ and $D2$ ($I_{D1} = I_{D2}$).
- **Overall Behavior and Trends:**
- The waveform shows a half-sinusoidal shape corresponding to the positive half-cycle of the input voltage.
- The current is zero during the negative half-cycle.
- **Key Features:**
- The peak current is labeled as $(V_p - 2V_{D,on}) / R_L$, indicating the maximum current through the diodes $D1$ and $D2$ during the positive half-cycle.

3. **Bottom Waveform ($I_{D3} = I_{D4}$):**
- **Type of Graph:** Time-domain waveform representing diode currents.
- **Axes Labels:**
- Horizontal axis: Time ($t$).
- Vertical axis: Current through diodes $D3$ and $D4$ ($I_{D3} = I_{D4}$).
- **Overall Behavior and Trends:**
- The waveform shows a half-sinusoidal shape corresponding to the negative half-cycle of the input voltage.
- The current is zero during the positive half-cycle.
- **Key Features:**
- The peak current is labeled as $(V_p - 2V_{D,on}) / R_L$, indicating the maximum current through the diodes $D3$ and $D4$ during the negative half-cycle.

**Annotations and Specific Data Points:**
- The waveforms are annotated with the expression for peak currents, showing the effect of the diode's on-state voltage drop ($2V_{D,on}$) on the current levels.
- The time axis is consistent across all waveforms, indicating synchronous behavior of the input voltage and the diode currents.

Figure 3.41 Currents carried by diodes in a full-wave rectifier.

Exercise Sketch the power consumed in each diode as a function of time.

The results of our study are summarized in Fig. 3.42. While using two more diodes, fullwave rectifiers exhibit a lower ripple and require only half the diode breakdown voltage, well justifying their use in adaptors and chargers. ${ }^{15}$

[^8]image_name:Figure 3.41
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: D1, type: Diode, ports: {Na: Vin, Nc: K1}
name: C1, type: Capacitor, value: C1, ports: {Np: K1, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: K1, N2: GND}
]
extrainfo:The circuit is a full-wave rectifier with a capacitor filter. The input voltage is rectified by D1, smoothed by C1, and the load is represented by RL. The output voltage Vout is approximately Vp - VD,on, where VD,on is the diode's forward voltage drop. The reverse bias voltage is approximately 2Vp, indicating the peak inverse voltage the diode must withstand.
image_name:Figure 3.42
description:The diagram in Figure 3.42 illustrates a full-wave rectifier circuit and its corresponding input and output waveforms.

1. **Type of Graph and Function**:
- The graph is a time-domain waveform showing the relationship between input voltage \(V_{in}\) and output voltage \(V_{out}\) over time.

2. **Axes Labels and Units**:
- The horizontal axis represents time \(t\), though no specific units are provided.
- The vertical axis represents voltage, with \(V_{in}\) and \(V_{out}\) as the key variables.

3. **Overall Behavior and Trends**:
- The input voltage \(V_{in}\) is shown as a sinusoidal waveform.
- The output voltage \(V_{out}\) follows a rectified waveform, where the negative portions of the input waveform are flipped to the positive side, typical of full-wave rectification.
- The output waveform has a slightly lower amplitude than the input waveform, indicating voltage drop across the diode.

4. **Key Features and Technical Details**:
- The circuit diagram includes a diode \(D_1\), a capacitor \(C_1\), and a load resistor \(R_L\), which are standard components in rectification circuits.
- The output voltage is approximately \(V_p - V_{D,on}\), where \(V_p\) is the peak input voltage and \(V_{D,on}\) is the diode's forward voltage drop.
- The reverse bias voltage is approximately \(2V_p\), indicating the voltage stress on the diode during reverse bias conditions.

5. **Annotations and Specific Data Points**:
- The graph does not provide specific numerical values but indicates the relationship between input and output voltages qualitatively.
- The labels and annotations highlight the key components and voltage levels in the circuit, providing insight into the rectification process.

(a)
image_name:Figure 3.42
description:
[
name: D1, type: Diode, ports: {Na: X2, Nc: X1}
name: D2, type: Diode, ports: {Na: X2, Nc: GND}
name: D3, type: Diode, ports: {Na: X3, Nc: X2}
name: D4, type: Diode, ports: {Na: GND, Nc: X1}
name: RL, type: Resistor, value: RL, ports: {N1: X3, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: X3, Nn: GND}
]
extrainfo:The circuit is a full-wave rectifier using a bridge configuration of diodes D1, D2, D3, and D4. It rectifies the input AC voltage Vin to a DC output voltage across RL and C1, with an output voltage approximately equal to Vp - 2VD,on.

image_name:Reverse Bias ≈ Vp
description:The graph is a time-domain waveform illustrating the behavior of input and output voltages in a full-wave rectifier circuit. The horizontal axis represents time (t), while the vertical axis represents voltage (V), with no specific units or scaling mentioned.

**Type of Graph and Function:**
This is a time-domain waveform graph, showing the input and output voltages of a rectifier circuit over time.

**Axes Labels and Units:**
- **Horizontal Axis (t):** Represents time.
- **Vertical Axis (V):** Represents voltage, with two waveforms labeled as \( V_{in} \) and \( V_{out} \).

**Overall Behavior and Trends:**
- The input voltage \( V_{in} \) is depicted as a sinusoidal waveform, representing the AC input to the rectifier.
- The output voltage \( V_{out} \) is shown as a rectified waveform, which follows the peaks of the input waveform but does not dip below zero, indicating the conversion of AC to DC.

**Key Features and Technical Details:**
- The output voltage \( V_{out} \) does not follow the negative half-cycles of the input waveform, which is characteristic of full-wave rectification.
- The peaks of the output waveform are slightly lower than the peaks of the input waveform, likely due to the voltage drop across the diodes in the rectifier.
- The label "Reverse Bias \( \approx V_p \)" suggests that the reverse bias voltage is approximately equal to the peak voltage, indicating the voltage stress on the diodes in reverse bias.

**Annotations and Specific Data Points:**
- The graph is annotated with \( V_{in} \) and \( V_{out} \) to differentiate the input and output waveforms.
- No specific numerical values are provided for voltages or time intervals.

(b)

Figure 3.42 Summary of rectifier circuits.

Example
3.31

Design a full-wave rectifier to deliver an average power of 2 W to a cellphone with a voltage of 3.6 V and a ripple of 0.2 V .

Solution We begin with the required input swing. Since the output voltage is approximately equal to $V_{p}-2 V_{D, o n}$, we have

$$
\begin{align*}
V_{i n, p} & =3.6 \mathrm{~V}+2 V_{D, o n}  \tag{3.95}\\
& \approx 5.2 \mathrm{~V} . \tag{3.96}
\end{align*}
$$

Thus, the transformer preceding the rectifier must step the line voltage $\left(110 \mathrm{~V}_{r m s}\right.$ or $220 \mathrm{~V}_{\mathrm{rms}}$ ) down to a peak value of 5.2 V .

Next, we determine the minimum value of the smoothing capacitor that ensures $V_{R} \leq 0.2 \mathrm{~V}$. Rewriting Eq. (3.83) for a full-wave rectifier gives

$$
\begin{align*}
V_{R} & =\frac{I_{L}}{2 C_{1} f_{\text {in }}}  \tag{3.97}\\
& =\frac{2 \mathrm{~W}}{3.6 \mathrm{~V}} \cdot \frac{1}{2 C_{1} f_{\text {in }}} . \tag{3.98}
\end{align*}
$$

For $V_{R}=0.2 \mathrm{~V}$ and $f_{\text {in }}=60 \mathrm{~Hz}$,

$$
\begin{equation*}
C_{1}=23,000 \mu \mathrm{~F} \tag{3.99}
\end{equation*}
$$

The diodes must withstand a reverse bias voltage of 5.2 V .

Exercise If cost and size limitations impose a maximum value of $1000 \mu \mathrm{~F}$ on the smoothing capacitor, what is the maximum allowable power drain in the above example?

A radio frequency signal received and amplified by a cellphone exhibits a peak swing of
3.32 10 mV . We wish to generate a dc voltage representing the signal amplitude [Eq. (3.8)]. Is it possible to use the half-wave or full-wave rectifiers studied above?

Solution No, it is not. Owing to its small amplitude, the signal cannot turn actual diodes on and off, resulting in a zero output. For such signal levels, "precision rectification" is necessary, a subject studied in Chapter 8.

Exercise What if a constant voltage of 0.8 V is added to the desired signal?

### 3.5.2 Voltage Regulation*

The adaptor circuit studied above generally proves inadequate. Due to the significant variation of the line voltage, the peak amplitude produced by the transformer and hence the dc output vary considerably, possibly exceeding the maximum level that can be tolerated by the load (e.g., a cellphone). Furthermore, the ripple may become seriously objectionable in many applications. For example, if the adaptor supplies power to a stereo, the $120-\mathrm{Hz}$ ripple can be heard from the speakers. Moreover, the finite output impedance of the transformer leads to changes in $V_{\text {out }}$ if the current drawn by the load varies. For these reasons, the circuit of Fig. 3.40(a) is often followed by a "voltage regulator" so as to provide a constant output.

We have already encountered a voltage regulator without calling it such: the circuit studied in Example 3.17 provides a voltage of 2.4 V , incurring only an $11-\mathrm{mV}$ change in the output for a $100-\mathrm{mV}$ variation in the input. We may therefore arrive at the circuit shown in Fig. 3.43 as a more versatile adaptor having a nominal output of $3 V_{D, \text { on }} \approx 2.4 \mathrm{~V}$. Unfortunately, as studied in Example 3.22, the output voltage varies with the load current.
image_name:Figure 3.43
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: L1, type: Inductor, value: L1, ports: {N1: Vin, N2: X1}
name: L2, type: Inductor, value: L2, ports: {N1: X1, N2: X2}
name: Diode Bridge, type: Other, ports: {N1: X1, N2: X2, N3: X4, N4: X3}
name: R1, type: Resistor, value: R1, ports: {N1: X4, N2: X5}
name: C1, type: Capacitor, value: C1, ports: {Np: X4, Nn: X3}
name: D1, type: Diode, ports: {Na: X5, Nc: X6}
name: D2, type: Diode, ports: {Na: X6, Nc: X7}
name: D3, type: Diode, ports: {Na: X7, Nc: X3}
]
extrainfo:The circuit is a voltage regulator block diagram featuring a diode bridge rectifier, followed by a filter and voltage regulation stage using Zener diodes. It is designed to maintain a stable output voltage despite variations in input voltage or load conditions.

Figure 3.43 Voltage regulator block diagram.
*This section can be skipped in a first reading.
image_name:(a)
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: Vout}
name: D1, type: Diode, ports: {Na: Vout, Nc: GND}
]
extrainfo:The circuit diagram (a) is a voltage regulator using a Zener diode. It stabilizes the output voltage (Vout) by shunting current to ground through the Zener diode (D1) when the voltage exceeds a certain level. The resistor R1 limits the current through the diode. The input voltage is Vin, and the output voltage is Vout.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: Vout}
name: rd, type: Resistor, value: rd, ports: {N1: Vout, N2: GND}
]
extrainfo:This is a small-signal equivalent circuit of a Zener diode regulator. The diagram shows a resistor R1 connected between the input voltage Vin and the output voltage Vout, and a resistor rd connected between Vout and ground (GND). The circuit is used to model the behavior of the Zener diode in a voltage regulation application.

Figure 3.44 (a) Regulator using a Zener diode, (b) small-signal equivalent of (a).

Did you know?

The diodes used in power supplies may not seem to have a large carbon footprint, but if we add up the power consumption of all of the diodes in the world, we see a frightening picture.

As an example, consider Google's server farms. It is estimated that Google has about half a million servers. If one server draws 200 W from a 12-V supply, then each rectifier diode carries an average current of $200 \mathrm{~W} / 12 \mathrm{~V} / 2 \approx 8.5 \mathrm{~A}$. (We assume two diodes alternately turn on, each carrying half of the server's average current.) With a forward bias of about 0.7 V , two diodes consume 12 W, suggesting that the rectifier diodes in Google's servers dissipate a total power of roughly 6 MW. This is equivalent to the power generated by about 10 nuclear power plants! Indeed, a great deal of effort is presently expended on "green electronics," trying to reduce the power consumption of every circuit, including the power supply itself. (Our example is actually quite pessimistic as computers use "switching" power supplies to improve the efficiency.)

Figure 3.44(a) shows another regulator circuit employing a Zener diode. Operating in the reverse breakdown region, $D_{1}$ exhibits a small-signal resistance, $r_{D}$, in the range of 1 to $10 \Omega$, thus providing a relatively constant output despite input variations if $r_{D} \ll R_{1}$. This can be seen from the small-signal model of Fig. 3.44(b):

$$
\begin{equation*}
v_{\text {out }}=\frac{r_{D}}{r_{D}+R_{1}} v_{\text {in }} \tag{3.100}
\end{equation*}
$$

For example, if $r_{D}=5 \Omega$ and $R_{1}=1 \mathrm{k} \Omega$, then changes in $V_{\text {in }}$ are attenuated by approximately a factor of 200 as they appear in $V_{\text {out }}$. The Zener regulator nonetheless has the same drawback as the circuit of Fig. 3.43, namely, poor stability if the load current varies significantly.

Our brief study of regulators thus far reveals two important aspects of their design: the stability of the output with respect to input variations, and the stability of the output with respect to load current variations. The former is quantified by "line regulation," defined as $\Delta V_{\text {out }} / \Delta V_{\text {in }}$, and the latter by "load regulation," defined as $\Delta V_{\text {out }} / \Delta I_{L}$.
image_name:Fig. 3.45(a)
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: Vout}
name: D1, type: Diode, ports: {Na: Vout, Nc: Vout}
name: D2, type: Diode, ports: {Na: Vout, Nc: GND}
]
extrainfo:The circuit is a voltage regulator using two diodes. D1 is forward-biased with a voltage drop V_D,on, and D2 is reverse-biased with a breakdown voltage V_Dz. The output voltage Vout is stabilized by the diodes.

(a)
image_name:(b)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: Vout}
name: rd1, type: Resistor, value: rd1, ports: {N1: Vout, N2: X1}
name: rd2, type: Resistor, value: rd2, ports: {N1: X1, N2: GND}
]
extrainfo:The circuit is a small-signal equivalent of a voltage regulator using two diodes. It stabilizes the output voltage Vout by using resistors rd1 and rd2.

(b)
image_name:(b)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: Vout}
name: rd1, type: Resistor, value: rd1, ports: {N1: Vout, N2: X1}
name: rd2, type: Resistor, value: rd2, ports: {N1: X1, N2: GND}
]
extrainfo:The circuit is a small-signal equivalent of a voltage regulator using two diodes. It stabilizes the output voltage Vout by using resistors rd1 and rd2.

(c)

Figure 3.45 Circuit using two diodes, (b) small-signal equivalent, (c) load regulation.

Solution We first determine the bias current of $D_{1}$ and hence its small-signal resistance:

$$
\begin{align*}
I_{D 1} & =\frac{V_{i n}-V_{D, \text { on }}-V_{D 2}}{R_{1}}  \tag{3.101}\\
& =15 \mathrm{~mA} . \tag{3.102}
\end{align*}
$$

Thus,

$$
\begin{align*}
r_{D 1} & =\frac{V_{T}}{I_{D 1}}  \tag{3.103}\\
& =1.73 \Omega . \tag{3.104}
\end{align*}
$$

From the small-signal model of Fig. 3.44(b), we compute the line regulation as

$$
\begin{align*}
\frac{v_{\text {out }}}{v_{\text {in }}} & =\frac{r_{D 1}+r_{D 2}}{r_{D 1}+r_{D 2}+R_{1}}  \tag{3.105}\\
& =0.063 \tag{3.106}
\end{align*}
$$

For load regulation, we assume the input is constant and study the effect of load current variations. Using the small-signal circuit shown in Fig. 3.45(c) (where $v_{i n}=0$ to represent a constant input), we have

$$
\begin{equation*}
\frac{v_{\text {out }}}{\left(r_{D 1}+r_{D 2}\right) \| R_{1}}=-i_{L} \tag{3.107}
\end{equation*}
$$

That is,

$$
\begin{align*}
\left|\frac{v_{\text {out }}}{i_{L}}\right| & =\left(r_{D 1}+r_{D 2}\right) \| R_{1}  \tag{3.108}\\
& =6.31 \Omega . \tag{3.109}
\end{align*}
$$

This value indicates that a $1-\mathrm{mA}$ change in the load current results in a $6.31-\mathrm{mV}$ change in the output voltage.

Exercise Repeat the above example for $R_{1}=50 \Omega$ and compare the results.

Figure 3.46 summarizes the results of our study in this section.
image_name:Figure 3.46 Summary of regulators
description:
[
name: D1, type: Diode, ports: {Na: Vin, Nc: k1}
name: C1, type: Capacitor, value: C1, ports: {Np: k1, Nn: GND}
name: Load, type: Other, ports: {N1: k1, N2: GND}
name: D1, type: Diode, ports: {Na: VinP, Nc: X1}
name: C, type: Capacitor, value: C, ports: {Np: X1, Nn: GND}
name: Load, type: Other, ports: {N1: X1, N2: GND}
name: D1, type: Diode, ports: {Na: X1, Nc: GND}
name: R, type: Resistor, value: R, ports: {N1: X1, N2: X2}
name: C, type: Capacitor, value: C, ports: {Np: X2, Nn: GND}
name: Load, type: Other, ports: {N1: X2, N2: GND}
]
extrainfo:The diagram shows three types of voltage regulator circuits with diodes, capacitors, and loads. Each circuit is designed to regulate the input voltage Vin to the load. The first circuit uses a diode D1 and a capacitor C1. The second uses a diode and capacitor C. The third circuit adds a resistor R in series with a diode and capacitor for additional voltage regulation.

Figure 3.46 Summary of regulators.

### 3.5.3 Limiting Circuits

Consider the signal received by a cellphone as the user comes closer to a base station (Fig. 3.47). As the distance decreases from kilometers to hundreds of meters, the signal level may become large enough to "saturate" the circuits as it travels through the receiver chain. It is therefore desirable to "limit" the signal amplitude at a suitable point in the receiver.
image_name:(a)
description:The diagram labeled "(a)" illustrates a simple communication system involving a base station and a receiver.

1. **Main Components:**
- **Base Station:** This is represented by a tower with a transmitting antenna. It is responsible for sending out signals.
- **Receiver:** This consists of an antenna and an amplifier. The antenna captures the incoming signals from the base station, and the amplifier boosts the signal strength for further processing.

2. **Flow of Information or Control:**
- **Signal Transmission:** The base station emits radio frequency signals, depicted as waves moving towards the receiver.
- **Signal Reception and Amplification:** The receiver's antenna captures these signals. The captured signals are then fed into an amplifier, which increases their amplitude to make them suitable for further processing or analysis.

3. **Labels, Annotations, and Key Indicators:**
- The diagram uses arrows to show the direction of signal flow from the base station to the receiver.
- The receiver is labeled to clearly indicate its function in the system.

4. **Overall System Function:**
- The primary function of this system is to demonstrate the process of receiving signals from a distant base station. The receiver captures and amplifies these signals, ensuring they are strong enough for subsequent use. This setup is typical in wireless communication systems where maintaining signal integrity over long distances is crucial.
image_name:(b)
description:The diagram labeled "(b)" illustrates a communication system involving a base station and a receiver. Here is a detailed description of the system block diagram:

1. **Main Components:**
- **Base Station:** This is depicted as a tower with an antenna at the top. It serves as the origin point for the transmission of signals.
- **Receiver:** Located next to the base station, the receiver is represented with an antenna and a triangular block, indicating an amplifier or signal processing unit.

2. **Flow of Information or Control:**
- **Signal Transmission:** The base station emits signals, shown as wavy lines, towards the receiver.
- **Signal Reception and Processing:** The receiver captures the incoming signals with its antenna and processes them through the triangular block, which likely represents amplification or initial filtering.
- **Output Signal:** The processed signal is shown as a jagged line, indicating a possibly amplified or modified output signal.

3. **Labels, Annotations, and Key Indicators:**
- The diagram labels the components as "Base Station" and "Receiver," which clarifies their roles.
- The signal path is visually represented by arrows indicating the direction of signal flow from the base station to the receiver.

4. **Overall System Function:**
- The primary function of this system is to demonstrate the reception of signals by a receiver located near a base station. As the base station emits signals, the receiver captures and processes these signals, likely adjusting the amplitude to prevent saturation as the signal strength increases due to proximity. This setup is essential for maintaining communication integrity as the distance between the base station and receiver changes.

Figure 3.47 Signals received (a) far from or (b) near a base station.

How should a limiting circuit behave? For small input levels, the circuit must simply pass the input to the output, e.g., $V_{\text {out }}=V_{\text {in }}$, and as the input level exceeds a "threshold" or "limit," the output must remain constant. This behavior must hold for both positive and negative inputs, translating to the input/output characteristic shown in Fig. 3.48(a). As illustrated in Fig. 3.48(b), a signal applied to the input emerges at the output with its peak values "clipped" at $\pm V_{L}$.

We now implement a circuit that exhibits the above behavior. The nonlinear input/ output characteristic suggests that one or more diodes must turn on or off as $V_{i n}$ approaches $\pm V_{L}$. In fact, we have already seen simple examples in Figs. 3.11(b)and (c), where the positive half cycles of the input are clipped at 0 V and +1 V , respectively. We reexamine the former assuming a more realistic diode, e.g., the constant-voltage model. As illustrated in Fig. 3.49(a), $V_{\text {out }}$ is equal to $V_{\text {in }}$ for $V_{\text {in }}<V_{D, \text { on }}$ and equal to $V_{D, \text { on }}$ thereafter.

To serve as a more general limiting circuit, the above topology must satisfy two other conditions. First, the limiting level, $V_{L}$, must be an arbitrary voltage and not necessarily equal to $V_{D, o n}$. Inspired by the circuit of Fig. 3.11 (c), we postulate that a constant voltage source in series with $D_{1}$ shifts the limiting point, accomplishing this objective. Depicted in Fig. 3.49(b), the resulting circuit limits at $V_{L}=V_{B 1}+V_{D, \text { on }}$. Note that $V_{B 1}$ can be positive or negative to shift $V_{L}$ to higher or lower values, respectively.

Second, the negative values of $V_{i n}$ must also experience limiting. Beginning with the circuit of Fig. 3.49(a), we recognize that if the anode and cathode of $D_{1}$ are swapped, then the circuit limits at $V_{i n}=-V_{D, \text { on }}$ [Fig. 3.50(a)]. Thus, as shown in Fig. 3.50(b), two "antiparallel" diodes can create a characteristic that limits at $\pm V_{D, o n}$. Finally, inserting constant voltage sources in series with the diodes shifts the limiting points to arbitrary levels (Fig. 3.51).
image_name:(a)
description:The graph labeled (a) depicts the input/output characteristic of a limiting circuit. This is a piecewise linear graph, where the x-axis represents the input voltage $V_{in}$, and the y-axis represents the output voltage $V_{out}$. Both axes are likely in volts, although specific units are not annotated.

**Type of Graph and Function:**
- This is a static characteristic curve of a limiter circuit, showing how the output voltage changes with respect to the input voltage.

**Axes Labels and Units:**
- **X-axis:** Input voltage ($V_{in}$)
- **Y-axis:** Output voltage ($V_{out}$)

**Overall Behavior and Trends:**
- The graph has three distinct regions:
1. **Linear Region:** For input voltages between $-V_L$ and $+V_L$, the output voltage is linearly proportional to the input voltage, following a 45-degree line through the origin.
2. **Clipping Regions:** For input voltages less than $-V_L$, the output voltage is constant at $-V_L$. For input voltages greater than $+V_L$, the output voltage is constant at $+V_L$.

**Key Features and Technical Details:**
- **Limiting Levels:** The output voltage is limited to $-V_L$ and $+V_L$, indicating the presence of a limiting mechanism in the circuit.
- **Transition Points:** The transition between linear and limiting behavior occurs at $V_{in} = -V_L$ and $V_{in} = +V_L$.

**Annotations and Specific Data Points:**
- The graph is annotated with $\pm V_L$, marking the limiting levels on both the x-axis and y-axis, emphasizing the points where the limiter starts to clip the input signal.

This graph provides a clear visualization of how the limiter circuit restricts the output voltage to a defined range, regardless of further increases or decreases in the input voltage beyond the specified threshold levels.
image_name:(b)
description:The graph labeled as (b) in Figure 3.48 illustrates the response of a limiting circuit to a sinusoidal input. It consists of two plots:

1. **Input/Output Characteristic Plot:**
- **Axes:**
- The horizontal axis represents the input voltage \(V_{in}\).
- The vertical axis represents the output voltage \(V_{out}\).
- **Behavior:**
- The graph shows a linear region where the output voltage follows the input voltage linearly between two threshold levels, \(+V_L\) and \(-V_L\).
- Beyond these thresholds, the output voltage is limited to \(+V_L\) and \(-V_L\), creating a flat region in the graph.
- **Key Features:**
- The graph has two distinct flat regions, indicating the limiting behavior of the circuit.
- The transition between the linear and flat regions occurs at \(+V_L\) and \(-V_L\).

2. **Time-Domain Response Plot:**
- **Axes:**
- The horizontal axis represents time \(t\).
- The vertical axis represents the output voltage \(V_{out}\).
- **Behavior:**
- The plot shows a sinusoidal waveform that is clipped at the levels \(+V_L\) and \(-V_L\).
- The input sinusoid (dashed line) exceeds these levels, but the output (solid line) is limited, resulting in a flat-topped waveform.
- **Key Features:**
- The waveform is symmetrical about the horizontal axis.
- The clipping occurs at the same voltage levels \(+V_L\) and \(-V_L\) as indicated in the input/output characteristic plot.

Overall, this graph depicts how a limiting circuit modifies a sinusoidal input by restricting the output voltage to a specified range, effectively clipping the peaks of the waveform at \(+V_L\) and \(-V_L\).

Figure 3.48 (a) Input/output characteristic of a limiting circuit, (b) response to a sinusoid.
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: Vout}
name: D1, type: Diode, ports: {Na: Vout, Nc: GND}
]
extrainfo:This is a simple diode limiter circuit. It clips the input voltage at the diode's forward voltage, VD,on, limiting the output voltage to this level. The graphs illustrate the input/output characteristic and the response to a sinusoidal input.
image_name:(b)
description:The graph in Figure 3.48(b) depicts the output response of a limiting circuit to a sinusoidal input. This is a time-domain waveform graph where the horizontal axis represents time \(t\) and the vertical axis represents output voltage \(V_{out}\). The waveform is symmetrical about the horizontal axis, indicating that the input sinusoidal waveform is being modified by the limiting circuit.

The key feature of this graph is the clipping of the sinusoidal waveform at a specific voltage level, denoted as \(V_{D,on}\). The peaks of the sinusoidal waveform are clipped at this level, resulting in a flat-top waveform at the positive peak. This demonstrates the effect of the limiter, which restricts the output voltage to a defined range, effectively cutting off the peaks of the waveform at \(V_{D,on}\).

The dashed line represents the original unaltered sinusoidal waveform, showing what the waveform would look like without the limiting effect. The solid line shows the actual output after clipping, where the positive peaks are limited to \(V_{D,on}\), while the negative half of the waveform remains unaffected, indicating a unidirectional clipping characteristic of the limiting circuit shown in the context.

This type of waveform modification is typical in circuits designed to prevent voltage from exceeding a certain threshold, protecting components from overvoltage conditions or altering the signal for specific applications.
image_name:(c)
description:The diagram labeled "(c)" depicts a typical diode limiting circuit and its effect on an input sinusoidal waveform. Here's a detailed description of the graph:

1. **Type of Graph and Function:**
- The graph includes both a circuit schematic and two plots: an input/output characteristic plot and a time-domain waveform.

2. **Axes Labels and Units:**
- The input/output characteristic plot has the horizontal axis labeled as \( V_{in} \) (input voltage) and the vertical axis labeled as \( V_{out} \) (output voltage). The units are in volts.
- The time-domain waveform plot has the horizontal axis labeled as \( t \) (time) and the vertical axis as \( V_{out} \) (output voltage), also in volts.

3. **Overall Behavior and Trends:**
- **Input/Output Characteristic Plot:**
- The plot shows a linear region where the diode is off, and the output voltage follows the input voltage until the diode turns on at \( V_{D,on} \). Beyond this point, the output voltage is clamped at \( V_{D,on} \).
- **Time-Domain Waveform:**
- The sinusoidal input is clipped at the positive peak, where the output voltage is limited to \( V_{D,on} \). The negative half of the waveform is unaffected, indicating a single-sided clipping effect.

4. **Key Features and Technical Details:**
- The diode begins conducting at a forward voltage \( V_{D,on} \), clipping the output waveform at this level.
- The circuit consists of a resistor \( R_1 \) and a diode \( D_1 \) that shunts excess voltage to ground when the input exceeds \( V_{D,on} \).

5. **Annotations and Specific Data Points:**
- The input/output characteristic plot includes a dashed line indicating the onset of diode conduction at \( V_{D,on} \).
- The time-domain waveform shows the clipped portion of the sinusoid with a dashed line representing the original unclipped waveform for comparison.

This graph effectively illustrates how a diode limiter modifies an input sinusoidal signal by clipping its positive peaks at a specific voltage level \( V_{D,on} \), demonstrating the behavior of a single-sided limiter circuit.

(a)
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: Vout}
name: D1, type: Diode, ports: {Na: Vout, Nc: GND}
name: VB1, type: VoltageSource, value: VB1, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a limiter with level shift, where the diode clips the positive peaks of the input sinusoidal signal at a specific voltage level determined by VD,on and VB1. The waveform shows the clipped signal compared to the original sinusoid.
image_name:(b)
description:The diagram labeled "(b)" consists of two main components: a circuit schematic and two graphical plots.

1. **Circuit Schematic:**
- The circuit includes a diode (D1) and a resistor (R1) connected in series with an input voltage source (Vin). Additionally, there's a battery (VB1) connected in parallel with the diode, providing a level shift to the output voltage (Vout).
- The diode is oriented to conduct when the input voltage exceeds a certain threshold, specifically when the input voltage is greater than the sum of the diode's forward voltage drop (VD,on) and the battery voltage (VB1).

2. **Graphical Plots:**
- **Vout vs. Vin Plot:**
- The plot on the right shows the relationship between the output voltage (Vout) and the input voltage (Vin).
- The x-axis represents the input voltage (Vin), while the y-axis represents the output voltage (Vout).
- The graph is linear with a slope of 1 until the input voltage reaches the threshold level of VD,on + VB1.
- Beyond this point, the output voltage is clipped and remains constant at VD,on + VB1, indicating the limiting action of the circuit.
- A dashed line marks the threshold level, showing where the diode begins to conduct.

- **Time-Domain Waveform:**
- The plot below the Vout vs. Vin graph is a time-domain waveform of the output voltage (Vout).
- The x-axis represents time (t), and the y-axis represents the output voltage (Vout).
- The waveform is a clipped sinusoid, where the positive peaks are flattened at the level of VD,on + VB1 due to the limiting action.
- A dashed line shows the original unclipped sinusoidal waveform for comparison, highlighting the extent of clipping.

Overall, the diagram illustrates how the circuit functions as a limiter with a level shift, clipping the positive peaks of an input sinusoidal signal at a specific voltage level determined by the diode and battery combination.

(b)

Figure 3.49 (a) Simple limiter, (b) limiter with level shift.
image_name:Figure 3.49 (a)
description:**Figure 3.49 (a) - Simple Limiter**

1. **Type of Graph and Function:**
- The diagram represents a simple electronic limiter circuit and its output waveform. The graph is a time-domain waveform showing how the output voltage (V_out) behaves over time (t) when an input voltage (V_in) is applied.

2. **Axes Labels and Units:**
- The x-axis represents time (t).
- The y-axis represents the output voltage (V_out).
- Voltage levels are indicated relative to the diode's forward voltage drop (V_D,on).

3. **Overall Behavior and Trends:**
- The circuit clips the input sinusoidal waveform, flattening the positive peaks at the level of V_D,on. The negative cycle is unaffected.
- The waveform shows a sinusoidal input with positive peaks clipped, indicating the limiting action of the diode.

4. **Key Features and Technical Details:**
- The clipping level is determined by the diode's forward voltage drop (V_D,on).
- The positive peaks of the waveform are limited to V_D,on, while the negative portion of the waveform remains unchanged.
- The dashed line in the waveform graph represents the original unclipped sinusoidal input for comparison.

5. **Annotations and Specific Data Points:**
- The waveform graph clearly shows the clipping level at V_D,on, with a horizontal line marking this level.
- The dashed line helps visualize the extent of clipping compared to the original waveform.
image_name:Figure 3.49 (b)
description:Figure 3.49(b) illustrates a limiter circuit with level shift, designed to clip both positive and negative peaks of an input sinusoidal waveform. The circuit diagram on the left shows a configuration with two diodes, D1 and D2, connected in parallel with opposite orientations, and a resistor R1 in series with the input voltage source \( V_{in} \). This setup allows for symmetrical clipping of the waveform.

To the right of the circuit diagram, there are two graphs:

1. **Voltage-Time Graph (Middle):**
- **Type:** Time-domain waveform.
- **Axes:**
- Horizontal axis represents time \( t \).
- Vertical axis represents output voltage \( V_{out} \).
- **Behavior:** The graph shows the input sinusoidal waveform being clipped at both positive and negative peaks. The clipping occurs at voltage levels defined by the diode's forward voltage drop \( V_{D,on} \). The waveform is flat-topped at these levels, indicating the limiting action.
- **Key Features:**
- The positive peaks are clipped at \( +V_{D,on} \).
- The negative peaks are clipped at \( -V_{D,on} \).
- The unclipped sinusoidal waveform is indicated by a dashed line for comparison.

2. **Voltage-Input Graph (Right):**
- **Type:** Voltage transfer characteristic curve.
- **Axes:**
- Horizontal axis represents input voltage \( V_{in} \).
- Vertical axis represents output voltage \( V_{out} \).
- **Behavior:** This graph shows the relationship between \( V_{in} \) and \( V_{out} \). The output voltage remains constant at \( +V_{D,on} \) and \( -V_{D,on} \) for input voltages beyond these thresholds, illustrating the limiting effect.
- **Key Features:**
- Linear region between \( -V_{D,on} \) and \( +V_{D,on} \).
- Flat regions beyond these points indicating the clipped output.

Overall, the diagram effectively demonstrates how the limiter circuit modifies the input signal by clipping both half cycles, maintaining the output within a specified voltage range determined by the diodes' forward voltage characteristics.

Figure 3.50 (a) Negative-cycle limiter, (b) limiter for both half cycles.
image_name:Figure 3.52(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: Vout}
name: D1, type: Diode, ports: {Na: Vout, Nc: GND}
name: D2, type: Diode, ports: {Na: GND, Nc: Vout}
name: V_B1, type: VoltageSource, value: V_B1, ports: {Np: Vout, Nn: GND}
name: V_B2, type: VoltageSource, value: V_B2, ports: {Np: GND, Nn: Vout}
]
extrainfo:The circuit is a limiter designed to clip both the positive and negative cycles of the input signal. The diodes and voltage sources set the clipping levels at ±(VD,on + VB1) and ±(VD,on + VB2) respectively. The graph shows the input-output relationship and the clipped waveform.
image_name:Figure 3.51
description:The graph in Figure 3.51 illustrates the characteristic of a general limiter circuit. This graph is a plot of the output voltage (V_out) versus the input voltage (V_in), showcasing how the limiter modifies the input signal.

1. **Type of Graph and Function:**
- The graph is a characteristic curve of a limiter circuit, demonstrating the relationship between input and output voltages.

2. **Axes Labels and Units:**
- The horizontal axis represents the input voltage (V_in).
- The vertical axis represents the output voltage (V_out).
- Both axes are likely measured in volts (V), though specific units are not explicitly labeled.

3. **Overall Behavior and Trends:**
- The graph shows a linear region where the output voltage follows the input voltage. This occurs between the breakpoints defined by the diode forward voltage and bias voltages.
- Beyond these points, the graph flattens, indicating that the output voltage is clipped and does not increase with the input voltage. This clipping occurs at both positive and negative voltages.

4. **Key Features and Technical Details:**
- The linear region of the graph is between \(V_{D,on} + V_{B1}\) and \(-V_{D,on} - V_{B2}\), where \(V_{D,on}\) is the diode's forward voltage and \(V_{B1}, V_{B2}\) are the bias voltages.
- The output voltage is limited to these bounds, ensuring that it does not exceed these values.

5. **Annotations and Specific Data Points:**
- The graph is annotated with the breakpoints \(V_{D,on} + V_{B1}\) and \(-V_{D,on} - V_{B2}\), showing where the linear region transitions to the flat, clipped regions.
- The accompanying waveform on the right illustrates the effect on a sinusoidal input signal, showing how the peaks of the waveform are clipped to maintain the output within the specified voltage range.
image_name:Figure 3.50(b)
description:The diagram labeled as Figure 3.50(b) depicts a limiter circuit designed to clip both positive and negative half cycles of an input signal. The circuit consists of a resistor \( R_1 \) and two diodes \( D_1 \) and \( D_2 \), each with a voltage source in series, \( V_{B1} \) and \( V_{B2} \), respectively. The diodes are oriented in opposite directions to limit the voltage in both directions.

**Type of Graph and Function:**
The graph in the middle of the diagram shows the voltage transfer characteristic of the limiter circuit. It is a piecewise linear graph that illustrates how the output voltage \( V_{out} \) relates to the input voltage \( V_{in} \).

**Axes Labels and Units:**
- The horizontal axis represents the input voltage \( V_{in} \).
- The vertical axis represents the output voltage \( V_{out} \).
- The axes are in linear scale with no specific units labeled, but they are typically in volts.

**Overall Behavior and Trends:**
The graph shows a linear region where the output voltage equals the input voltage, bounded by the values \( V_{D,on} + V_{B1} \) and \( -V_{D,on} - V_{B2} \). Beyond these points, the graph flattens, indicating the output voltage is clipped and remains constant despite further increases in the input voltage.

**Key Features and Technical Details:**
- The linear region is centered around the origin, suggesting symmetric clipping for both positive and negative cycles.
- The clipping levels are determined by the diode forward voltage \( V_{D,on} \) and the series voltage sources \( V_{B1} \) and \( V_{B2} \).
- The graph shows the breakpoints at \( V_{D,on} + V_{B1} \) and \( -V_{D,on} - V_{B2} \), where the graph transitions from linear to flat.

**Annotations and Specific Data Points:**
- The graph is annotated with the values \( V_{D,on} + V_{B1} \) and \( -V_{D,on} - V_{B2} \), indicating the voltage levels at which clipping occurs.
- The right side of the diagram includes a time-domain representation of the output waveform, highlighting the clipping effect on a sinusoidal input. The waveform is shown with flat tops and bottoms, corresponding to the clipped regions on the transfer characteristic graph.

Figure 3.51 General limiter and its characteristic.

Example A signal must be limited at $\pm 100 \mathrm{mV}$. Assuming $V_{D, o n}=800 \mathrm{mV}$, design the required limiting circuit.

Solution
Figure 3.52(a) illustrates how the voltage sources must shift the break points. Since the positive limiting point must shift to the left, the voltage source in series with $D_{1}$ must be negative and equal to 700 mV . Similarly, the source in series with $D_{2}$ must be positive and equal to 700 mV . Figure 3.52(b) shows the result.
image_name:Figure 3.52 (b)
description:The graph in Figure 3.52 (b) is an input/output characteristic graph for a limiting circuit. The x-axis represents the input voltage \( V_{in} \) while the y-axis represents the output voltage \( V_{out} \). Both axes are marked in millivolts (mV).

**Type of Graph and Function:**
This is a piecewise linear graph showing how the limiting circuit affects the output voltage based on the input voltage.

**Axes Labels and Units:**
- **X-axis:** Input voltage \( V_{in} \) in millivolts (mV)
- **Y-axis:** Output voltage \( V_{out} \) in millivolts (mV)

**Overall Behavior and Trends:**
The graph illustrates a linear region in the center where the output voltage is directly proportional to the input voltage. This region is bounded by two flat, horizontal lines representing the limiting behavior of the circuit.

- For input voltages between approximately \(+100 mV\) and \(-100 mV\), the output voltage follows a linear relationship with the input voltage.
- Beyond these points, the output voltage is clipped or limited:
- When \( V_{in} \) exceeds \(+100 mV\), \( V_{out} \) is capped at \(+100 mV\).
- When \( V_{in} \) goes below \(-100 mV\), \( V_{out} \) is capped at \(-100 mV\).

**Key Features and Technical Details:**
- The graph shows a slope of 1 in the linear region, indicating a direct one-to-one relationship between \( V_{in} \) and \( V_{out} \) within the specified limits.
- The break points occur at \(+V_{D,on}\) and \(-V_{D,on}\), where \( V_{D,on} = 800 mV \). These are shifted by the voltage sources to achieve the desired limiting points at \(+100 mV\) and \(-100 mV\).

**Annotations and Specific Data Points:**
- The graph is annotated with \(+V_{D,on}\) and \(-V_{D,on}\) to indicate the points where the diodes turn on, although these are shifted due to the additional voltage sources.
- The limiting levels at \(+100 mV\) and \(-100 mV\) are clearly marked with horizontal lines, showing the maximum and minimum output voltages achievable by the circuit.

(a)
image_name:(a)
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: Vout}
name: D1, type: Diode, ports: {Na: Vout, Nc: X1}
name: D2, type: Diode, ports: {Na: Vout, Nc: X2}
]
extrainfo:The circuit is a limiting circuit with diodes D1 and D2 used to clip the voltage. The diodes are connected in parallel with voltage sources of 700 mV to ground, providing a reference for limiting the voltage at the output node Vout.

(b)

Figure 3.52 (a) Example of a limiting circuit, (b) input/output characteristic.
Exercise Repeat the above example if the positive values of the signal must be limited at +200 mV and the negative values at -1.1 V .

Before concluding this section, we make two observations. First, the circuits studied above actually display a nonzero slope in the limiting region (Fig. 3.53). This is because, as $V_{i n}$ increases, so does the current through the diode that is forward biased and hence the diode voltage. ${ }^{16}$ Nonetheless, the $60-\mathrm{mV} /$ decade rule expressed by Eq. (2.109) implies that this effect is typically negligible. Second, we have thus far assumed $V_{\text {out }}=V_{\text {in }}$ for $-V_{L}<V_{\text {in }}<+V_{L}$, but it is possible to realize a non-unity slope in the region: $V_{\text {out }}=\alpha V_{\text {in }}$.
${ }^{16}$ Recall that $V_{D}=V_{T} \ln \left(I_{D} / I_{S}\right)$.
image_name:Figure 3.53 Effect of nonideal diodes on limiting characteristic
description:The graph in Figure 3.53 is a plot depicting the effect of nonideal diodes on the limiting characteristic of a circuit. It is a two-dimensional graph with the horizontal axis labeled as \( V_{in} \) and the vertical axis labeled as \( V_{out} \). Both axes are likely measured in volts, although no specific units are provided.

Type of Graph and Function:
This is a characteristic curve graph showing the relationship between input voltage \( V_{in} \) and output voltage \( V_{out} \) in a diode circuit, highlighting the non-ideal behavior of diodes.

Axes Labels and Units:
- **Horizontal Axis (\( V_{in} \))**: Represents the input voltage.
- **Vertical Axis (\( V_{out} \))**: Represents the output voltage.

Overall Behavior and Trends:
The graph shows a sigmoidal shape, indicating that the output voltage \( V_{out} \) is not a simple linear function of the input voltage \( V_{in} \). Instead, there are distinct regions:
- **Linear Region**: Around the origin, \( V_{out} \) increases linearly with \( V_{in} \), suggesting a proportional relationship between input and output.
- **Saturation Regions**: At both extremes of the \( V_{in} \) range, the graph flattens, indicating that \( V_{out} \) reaches a limiting value and changes little with further increases or decreases in \( V_{in} \).

Key Features and Technical Details:
- **Inflection Points**: The transition from the linear region to the saturation regions is smooth, with inflection points marking the change in curvature.
- **Nonlinear Behavior**: The curvature at the transition points illustrates the non-ideal behavior of the diodes, which deviate from the ideal diode equation.

Annotations and Specific Data Points:
No specific numerical values or annotations are provided on the graph, but the general trend suggests a typical diode limiting behavior where the output voltage is clamped at certain levels due to the forward and reverse bias characteristics of the diodes.

Figure 3.53 Effect of nonideal diodes on limiting characteristic.

### 3.5.4 Voltage Doublers*

Electronic systems typically employ a "global" supply voltage, e.g., 3 V , requiring that the discrete and integrated circuits operate with such a value. However, the design of some circuits in the system is greatly simplified if they run from a higher supply voltage, e.g., 6 V . "Voltage doublers" may serve this purpose. ${ }^{17}$

Before studying doublers, it is helpful to review some basic properties of capacitors. First, to charge one plate of a capacitor to $+Q$, the other plate must be charged to $-Q$. Thus, in the circuit of Fig. 3.54(a), the voltage across $C_{1}$ cannot change even if $V_{i n}$ changes because the right plate of $C_{1}$ cannot receive or release charge $(Q=C V)$. Since $V_{C 1}$ remains constant, an input change $\Delta V_{\text {in }}$ appears directly at the output. This is an important observation.
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: Vout}
]
extrainfo:The circuit shows how a voltage change at one plate of a capacitor appears directly at the output when the other plate cannot receive or release charge. This is a basic property of capacitors used in voltage doubling circuits.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: Vout}
name: C2, type: Capacitor, value: C2, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit in diagram (b) is a capacitive voltage divider with input at Vin and output at Vout. The voltage across C1 is Vin - Vout, and the voltage across C2 is Vout. The ground is connected to the negative terminal of Vin and the negative terminal of C2.

Figure 3.54 (a) Voltage change at one plate of a capacitor, (b) voltage division.

Second, a capacitive voltage divider such as that in Fig. 3.54(b) operates as follows. If $V_{i n}$ becomes more positive, the left plate of $C_{1}$ receives positive charge from $V_{i n}$, thus requiring that the right plate absorb negative charge of the same magnitude from the top plate of $C_{2}$. Having lost negative charge, the top plate of $C_{2}$ equivalently holds more positive charge, and hence the bottom plate absorbs negative charge from ground. Note that all four plates receive or release equal amounts of charge because $C_{1}$ and $C_{2}$ are in series. To determine the change in $V_{\text {out }}, \Delta V_{\text {out }}$, resulting from $\Delta V_{\text {in }}$, we write the change in the charge on $C_{2}$ as $\Delta Q_{2}=C_{2} \cdot \Delta V_{\text {out }}$, which also holds for $C_{1}: \Delta Q_{2}=\Delta Q_{1}$. Thus, the voltage change across $C_{1}$ is equal to $C_{2} \cdot \Delta V_{\text {out }} / C_{1}$. Adding these two voltage changes and equating the result to $\Delta V_{i n}$, we have

$$
\begin{equation*}
\Delta V_{\text {in }}=\frac{C_{2}}{C_{1}} \Delta V_{\text {out }}+\Delta V_{\text {out }} \tag{3.110}
\end{equation*}
$$

[^9]That is,

$$
\begin{equation*}
\Delta V_{\text {out }}=\frac{C_{1}}{C_{1}+C_{2}} \Delta V_{\text {in }} \tag{3.111}
\end{equation*}
$$

This result is similar to the voltage division expression for resistive dividers, except that $C_{1}$ (rather than $C_{2}$ ) appears in the numerator. Interestingly, the circuit of Fig. 3.54(a) is a special case of the capacitive divider with $C_{2}=0$ and hence $\Delta V_{\text {out }}=\Delta V_{\text {in }}$.

As our first step toward realizing a voltage doubler, recall the result illustrated in Fig. 3.31: the voltage across the diode in the peak detector exhibits an average value of $-V_{p}$ and, more importantly, a peak value of $-2 V_{p}$ (with respect to zero). For further investigation, we redraw the circuit as shown in Fig. 3.55, where the diode and the capacitors are exchanged and the voltage across $D_{1}$ is labeled $V_{\text {out }}$. While $V_{\text {out }}$ in this circuit behaves exactly the same as $V_{D 1}$ in Fig. 3.30(a), we derive the output waveform from a different perspective so as to gain more insight.
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: Vout}
name: D1, type: Diode, ports: {Na: Vout, Nc: GND}
]
extrainfo:The circuit is a peak detector with an ideal diode and a capacitor. The input voltage Vin charges the capacitor C1 through the diode D1, and Vout is the voltage across the diode. The waveform shows Vout peaking at -2Vp with respect to zero.
image_name:(b)
description:The graph in Figure 3.55(b) is a time-domain waveform depicting the behavior of the output voltage, \( V_{\text{out}} \), over time in a capacitor-diode circuit. The horizontal axis represents time \( t \), while the vertical axis represents voltage. The graph uses a linear scale for both axes.

Overall Behavior and Trends:
- The waveform starts at 0 volts when \( t = 0 \) and follows a sinusoidal pattern influenced by the input voltage \( V_{\text{in}} \).
- As time progresses, \( V_{\text{in}} \) rises towards a peak value, \( V_{p} \), at time \( t_1 \), causing the diode to conduct and clamp \( V_{\text{out}} \) to 0 volts initially.
- Once \( V_{\text{in}} \) reaches its peak, the diode turns off, and \( V_{\text{out}} \) becomes negative, reaching a minimum of \(-V_{p}\) and further down to \(-2V_{p}\) as the input waveform cycles through its negative peak.

Key Features:
- **Zero Crossing:** The waveform crosses zero volts at the start and returns to zero at \( t_1 \).
- **Peak Values:** The waveform peaks at \(-V_{p}\) and \(-2V_{p}\), indicating the negative peaks of the output voltage when the diode is off.
- **Time Period:** The time period of the waveform is not explicitly marked, but the pattern suggests a periodic nature consistent with the input sinusoidal waveform.

Annotations and Specific Data Points:
- The graph includes annotations for key voltage levels: 0 volts, \(-V_{p}\), and \(-2V_{p}\).
- The point where \( V_{\text{in}} \) reaches its peak is marked at \( t_1 \), highlighting the transition from diode conduction to cutoff.

This waveform analysis provides insight into the voltage behavior across the diode, illustrating how the circuit modifies the input signal to produce the observed output voltage pattern.

Figure 3.55 (a) Capacitor-diode circuit and (b) its waveforms.

Assuming an ideal diode and a zero initial condition across $C_{1}$, we note that as $V_{\text {in }}$ exceeds zero, the input tends to place positive charge on the left plate of $C_{1}$ and hence draw negative charge from $D_{1}$. Consequently, $D_{1}$ turns on, forcing $V_{\text {out }}=0 .{ }^{18}$ As the input rises toward $V_{p}$, the voltage across $C_{1}$ remains equal to $V_{i n}$ because its right plate is "pinned" at zero by $D_{1}$. After $t=t_{1}, V_{\text {in }}$ begins to fall and tends to discharge $C_{1}$, i.e., draw positive charge from the left plate and hence from $D_{1}$. The diode therefore turns off, reducing the circuit to that in Fig. 3.54(a). From this time, the output simply tracks the changes in the input while $C_{1}$ sustains a constant voltage equal to $V_{p}$. In particular, as $V_{i n}$ varies from $+V_{p}$ to $-V_{p}$, the output goes from zero to $-2 V_{p}$, and the cycle repeats indefinitely. The output waveform is thus identical to that obtained in Fig. 3.31(b).

[^10]image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: Vout}
name: D1, type: Diode, ports: {Na: Vout, Nc: GND}
]
extrainfo:The circuit is a peak detector or rectifier with a capacitor and diode. The input voltage is applied across the capacitor, and the diode rectifies the output to ground. The waveform shows the output voltage tracking the peaks of the input voltage.
image_name:(b)
description:The graph in Figure 3.56(b) represents the output waveform of a capacitor-diode circuit as described in the context. It is a time-domain waveform plot.

1. **Axes Labels and Units:**
- The horizontal axis represents time, labeled as 't'.
- The vertical axis represents voltage, labeled with reference to the output voltage, 'V_out', and input voltage, 'V_in'.
- There are no specific units marked, but it is implied that voltage is in volts and time is in a standard unit like seconds.

2. **Overall Behavior and Trends:**
- The waveform shows a periodic behavior with alternating positive and negative cycles.
- The input voltage, V_in, is shown as a sinusoidal waveform (blue curve), oscillating between positive and negative peaks.
- The output voltage, V_out, (black curve) starts at zero, rises to a peak of +2V_p, and then drops back to zero, following a similar pattern for the negative cycle.
- This behavior indicates that the output tracks the input during the positive half cycle and resets to zero during the negative half cycle.

3. **Key Features and Technical Details:**
- The waveform shows key points at t_1 and t_2 where the diode turns on and off, affecting the output waveform.
- At t_1, the diode turns off, allowing the capacitor to charge and the output to follow the input.
- At t_2, the diode turns on, forcing the output to reset to zero.
- The peak value of the output voltage reaches +2V_p, indicating a doubling effect during the positive cycle.

4. **Annotations and Specific Data Points:**
- The graph includes annotations for the time points t_1, t_2, and t_4, marking significant changes in the circuit behavior.
- A reference line at +2V_p is drawn to indicate the maximum output voltage achieved during the cycle.

This waveform illustrates the operation of the capacitor-diode circuit, where the output voltage reflects the behavior of the input voltage with specific modifications due to the diode's switching actions.

Figure 3.56 Capacitor-diode circuit and (b) its waveforms.

Solution As $V_{\text {in }}$ rises from zero, attempting to place positive charge on the left plate of $C_{1}$ and hence draw negative charge from $D_{1}$, the diode turns off. As a result, $C_{1}$ directly transfers the input change to the output for the entire positive half cycle. After $t=t_{1}$, the input tends to push negative charge into $C_{1}$, turning $D_{1}$ on and forcing $V_{\text {out }}=0$. Thus, the voltage across $C_{1}$ remains equal to $V_{\text {in }}$ until $t=t_{2}$, at which point the direction of the current through $C_{1}$ and $D_{1}$ must change, turning $D_{1}$ off. Now, $C_{1}$ carries a voltage equal to $V_{p}$ and transfers the input change to the output; i.e., the output tracks the input but with a level shift of $+V_{p}$, reaching a peak value of $+2 V_{p}$.

Exercise Repeat the above example if the right plate of $C_{1}$ is 1 V more positive than its left plate at $t=0$.

We have thus far developed circuits that generate a periodic output with a peak value of $-2 V_{p}$ or $+2 V_{p}$ for an input sinusoid varying between $-V_{p}$ and $+V_{p}$. We surmise that if these circuits are followed by a peak detector [e.g., Fig. 3.30(a)], then a constant output equal to $-2 V_{p}$ or $+2 V_{p}$ may be produced. Figure 3.57 exemplifies this concept, combining the circuit of Fig. 3.56 with the peak detector of Fig. 3.30(a). Of course, since the peak detector "loads" the first stage when $D_{2}$ turns on, we must still analyze this circuit carefully and determine whether it indeed operates as a voltage doubler.
image_name:Figure 3.57
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: X}
name: D1, type: Diode, ports: {Na: X, Nc: GND}
name: D2, type: Diode, ports: {Na: X, Nc: Vout}
name: C2, type: Capacitor, value: C2, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a voltage doubler using ideal diodes and capacitors. It starts with a negative cycle to charge C1 to -Vp. During the positive cycle, D1 is off, and D2 conducts, transferring the charge to C2, effectively doubling the voltage at the output to 2Vp.
image_name:Vout vs Vin
description:The graph in question is a time-domain waveform depicting the relationship between the output voltage \( V_{out} \) and the input voltage \( V_{in} \) in a voltage doubler circuit. The graph is plotted with \( V_{out} \) on the vertical axis and time \( t \) on the horizontal axis.

**Axes Labels and Units:**
- **Vertical Axis:** \( V_{out} \), labeled in terms of voltage, with key points marked at \( V_p \) and \( \frac{V_p}{2} \).
- **Horizontal Axis:** Time \( t \), with specific times marked as \( t_1, t_2, t_3, t_4, \) and \( t_5 \).

**Overall Behavior and Trends:**
- The waveform begins at zero output voltage as \( V_{in} \) is initially zero or negative, turning on diode \( D_1 \) and keeping \( D_2 \) off.
- At \( t = t_1 \), \( V_{out} \) starts to rise sharply as \( V_{in} \) becomes positive, eventually reaching a peak value of \( V_p \) at \( t_2 \).
- From \( t_2 \) to \( t_3 \), the output voltage remains constant at \( V_p \), indicating a plateau in the waveform.
- As \( V_{in} \) decreases after \( t_3 \), \( V_{out} \) drops back to \( \frac{V_p}{2} \) at \( t_4 \), maintaining this level until \( t_5 \).
- The waveform exhibits a periodic behavior, with the cycle repeating as \( V_{in} \) oscillates.

**Key Features and Technical Details:**
- The graph clearly illustrates the charging and discharging phases of the capacitors \( C_1 \) and \( C_2 \) in the circuit.
- The key feature of the circuit as a voltage doubler is highlighted by the doubling of the peak input voltage to \( V_p \) at the output.

**Annotations and Specific Data Points:**
- The waveform is annotated with specific time points \( t_1 \) through \( t_5 \) that correspond to critical points in the operation of the circuit.
- The annotations indicate the operation of the diodes and the voltage levels across the capacitors at these times.

Figure 3.57 Voltage doubler circuit and its waveforms.

We assume ideal diodes, zero initial conditions across $C_{1}$ and $C_{2}$, and $C_{1}=C_{2}$. In this case, the analysis is simplified if we begin with a negative cycle. As $V_{\text {in }}$ falls below zero, $D_{1}$ turns on, pinning node $X$ to zero. ${ }^{19}$ Thus, for $t<t_{1}, D_{2}$ remains off and $V_{\text {out }}=0$. At $t=t_{1}$, the voltage across $C_{1}$ reaches $-V_{p}$. For $t>t_{1}$, the input begins to rise and tends to deposit positive charge on the left plate of $C_{1}$, turning $D_{1}$ off and yielding the circuit shown in Fig. 3.57.

How does $D_{2}$ behave in this regime? Since $V_{i n}$ is now rising, we postulate that $V_{X}$ also tends to increase (from zero), turning $D_{2}$ on. (If $D_{2}$ remains off, then $C_{1}$ simply transfers the change in $V_{i n}$ to node $X$, raising $V_{X}$ and hence turning $D_{2}$ on.) As a result, the circuit reduces to a simple capacitive divider that follows Eq. (3.111):

$$
\begin{equation*}
\Delta V_{\text {out }}=\frac{1}{2} \Delta V_{\text {in }} \tag{3.112}
\end{equation*}
$$

because $C_{1}=C_{2}$. In other words, $V_{X}$ and $V_{\text {out }}$ begin from zero, remain equal, and vary sinusoidally but with an amplitude equal to $V_{p} / 2$. Thus, from $t_{1}$ to $t_{2}$, a change of $2 V_{p}$ in $V_{\text {in }}$ appears as a change equal to $V_{p}$ in $V_{X}$ and $V_{\text {out }}$. Note at $t=t_{2}$, the voltage across $C_{1}$ is zero because both $V_{\text {in }}$ and $V_{\text {out }}$ are equal to $+V_{p}$.

What happens after $t=t_{2}$ ? Since $V_{i n}$ begins to fall and tends to draw charge from $C_{1}$, $D_{2}$ turns off, maintaining $V_{\text {out }}$ at $+V_{p}$. The reader may wonder if something is wrong here;

[^11]our objective was to generate an output equal to $2 V_{p}$ rather than $V_{p}$. But again, patience is a virtue and we must continue the transient analysis. For $t>t_{2}$, both $D_{1}$ and $D_{2}$ are off, and each capacitor holds a constant voltage. Since the voltage across $C_{1}$ is zero, $V_{X}=V_{i n}$, falling to zero at $t=t_{3}$. At this point, $D_{1}$ turns on again, allowing $C_{1}$ to charge to $-V_{p}$ at $t=t_{4}$. As $V_{i n}$ begins to rise again, $D_{1}$ turns off and $D_{2}$ remains off because $V_{X}=0$ and $V_{\text {out }}=+V_{p}$. Now, with the right plate of $C_{1}$ floating, $V_{X}$ tracks the change at the input, reaching $+V_{p}$ as $V_{i n}$ goes from $-V_{p}$ to 0 . Thus, $D_{2}$ turns on at $t=t_{5}$, forming a capacitive divider again. After this time, the output change is equal to half of the input change, i.e., $V_{\text {out }}$ increases from $+V_{p}$ to $+V_{p}+V_{p} / 2$ as $V_{\text {in }}$ goes from 0 to $+V_{p}$. The output has now reached $3 V_{p} / 2$.

As is evident from the foregoing analysis, the output continues to rise by $V_{p}, V_{p} / 2$, $V_{p} / 4$, etc., in each input cycle, approaching a final value of

$$
\begin{align*}
V_{\text {out }} & =V_{p}\left(1+\frac{1}{2}+\frac{1}{4}+\cdots\right)  \tag{3.113}\\
& =\frac{V_{p}}{1-\frac{1}{2}}  \tag{3.114}\\
& =2 V_{p} \tag{3.115}
\end{align*}
$$

The reader is encouraged to continue the analysis for a few more cycles and verify this trend.

Solution Using the diagram in Fig. 3.58(a), noting that $D_{1}$ and $C_{1}$ carry equal currents when $D_{1}$ is forward biased, and writing the current as $I_{D 1}=-C_{1} d V_{i n} / d t$, we construct the plot shown in Fig. 3.58(b). ${ }^{20}$ For $0<t<t_{1}, D_{1}$ conducts and the peak current corresponds to the maximum slope of $V_{i n}$, i.e., immediately after $t=0$. From $t=t_{1}$ to $t=t_{3}$, the diode remains off, repeating the same behavior in subsequent cycles.

Exercise Plot the current through $D_{2}$ in the above example as a function of time.

[^12]image_name:Figure 3.58
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: X1}
name: D1, type: Diode, ports: {Na: X1, Nc: X2}
name: C2, type: Capacitor, value: C2, ports: {Np: X2, Nn: GND}
]
extrainfo:The circuit is a voltage doubler using diodes and capacitors. It charges C1 during the negative half-cycle and transfers charge to C2 during the positive half-cycle, effectively doubling the input voltage.
image_name:V_in
description:The graph labeled "V_in" is a time-domain waveform representing the input voltage in a voltage doubler circuit. The x-axis is labeled as time \( t \), with key time intervals marked as \( t_1, t_2, t_3, t_4, \) and \( t_5 \). The y-axis represents the voltage \( V_{in} \), though specific units are not provided, it is typically in volts.

Overall Behavior and Trends:
- The waveform exhibits a sinusoidal shape, characteristic of alternating current (AC) signals.
- The waveform starts at zero, increases to a positive peak, returns to zero, decreases to a negative peak, and then returns to zero again, completing one full cycle.
- The positive peak occurs between \( t_1 \) and \( t_2 \), while the negative peak occurs between \( t_3 \) and \( t_4 \).
- The waveform is symmetrical about the time axis, indicating a consistent amplitude on both the positive and negative sides.

Key Features and Technical Details:
- The waveform crosses the time axis at \( t_1 \), \( t_3 \), and \( t_5 \), indicating zero crossings.
- The peak positive voltage is reached just before \( t_2 \), and the peak negative voltage is reached just before \( t_4 \).
- The intervals \( t_2 - t_3 \) and \( t_4 - t_5 \) indicate the time duration for the waveform to transition from peak to zero crossing.

Annotations and Specific Data Points:
- The waveform is annotated with specific circuit configurations showing diode and capacitor placements for different phases of the waveform.
- These annotations suggest the operation of the circuit as a voltage doubler, with the diodes and capacitors working in tandem to shift and stabilize the voltage levels.
- The circuit configurations shown alongside the waveform indicate different stages of charging and discharging of the capacitors, which correspond to the different segments of the waveform.
image_name:I_{D1}
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: X1}
name: D1, type: Diode, ports: {Na: X1, Nc: X2}
name: C2, type: Capacitor, value: C2, ports: {Np: X2, Nn: GND}
]
extrainfo:The circuit is a voltage doubler using diodes and capacitors. The input voltage Vin is doubled across C2. The waveform of ID1 indicates the current through diode D1 over time, showing conduction during t1 to t2 and t4 to t5.

Figure 3.58 Diode current in a voltage doubler.

### 3.5.5 Diodes as Level Shifters and Switches*

In the design of electronic circuits, we may need to shift the average level of a signal up or down because the subsequent stage (e.g., an amplifier) may not operate properly with the present dc level.

Sustaining a relatively constant voltage in forward bias, a diode can be viewed as a battery and hence a device capable of shifting the signal level. In our first attempt, we consider the circuit shown in Fig. 3.59(a) as a candidate for shifting the level down by $V_{D, o n}$. However, the diode current remains unknown and dependent on the next stage. To alleviate this issue we modify the circuit as depicted in Fig. 3.59(b), where $I_{1}$ draws a constant current, establishing $V_{D, o n}$ across $D_{1}{ }^{21}$ If the current pulled by the next stage is negligible (or at least constant), $V_{\text {out }}$ is simply lower than $V_{\text {in }}$ by a constant amount, $V_{D, \text { on }}$.
image_name:Figure 3.59 (a)
description:
[
name: D1, type: Diode, ports: {Na: Vin, Nc: Vout}
]
extrainfo:The circuit in Figure 3.59 (a) uses a diode for level shifting. The input voltage Vin is applied to the anode of the diode D1, and the output voltage Vout is taken from the cathode. This configuration shifts the DC level of the input signal down by the diode's forward voltage drop, V_D,on.
image_name:Figure 3.59 (b)
description:
[
name: D1, type: Diode, ports: {Na: Vin, Nc: Vout}
name: I1, type: CurrentSource, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a level shifter that shifts the input voltage down by the diode's forward voltage drop, VD,on. A constant current source, I1, is used to establish this voltage across the diode, D1.
image_name:Figure 3.60
description:The graph in Figure 3.60 illustrates a circuit designed to shift the DC level of a signal upward by \(2 V_{D, on}\). The figure is a schematic diagram showing two diodes in series, used to achieve the desired voltage level shift. The circuit is structured as follows:

1. **Type of Graph and Function:**
- The diagram is a circuit schematic, not a traditional graph with axes. It shows a configuration for level shifting a DC signal using diodes.

2. **Circuit Components:**
- The circuit includes two diodes, labeled \(D_1\) and \(D_2\), connected in series.
- The input voltage \(V_{in}\) is applied to the cathode of the second diode \(D_2\), and the output voltage \(V_{out}\) is taken from the anode of the first diode \(D_1\).
- The diodes are oriented to allow current flow from the input to the output when forward-biased.

3. **Functionality:**
- The purpose of the circuit is to shift the input signal's DC level upwards by twice the diode's forward voltage drop \(2 V_{D, on}\).
- By placing two diodes in series, the total voltage drop across them when forward-biased is \(2 V_{D, on}\), effectively raising the DC level of the input signal by this amount.

4. **Behavior and Trends:**
- The circuit ensures that any AC signal superimposed on the DC level at the input will appear at the output with its DC level shifted upwards by \(2 V_{D, on}\).
- This configuration is useful in applications where a specific DC offset is required for further signal processing.

5. **Technical Details:**
- The diodes must be forward-biased for the level shift to occur, which means \(V_{in}\) must be greater than the combined forward voltage of the diodes.
- This circuit is typically used in analog signal processing to adjust the DC level without affecting the AC characteristics of the signal.

This description provides a comprehensive understanding of the circuit's purpose and operation, allowing for practical implementation or analysis without requiring visual access to the diagram itself.

Figure 3.59 (a) Use of a diode for level shift, (b) practical implementation.

[^13]Design a circuit that shifts up the dc level of a signal by $2 V_{D, o n}$.
3.37

Solution To shift the level $u p$, we apply the input to the cathode. Also, to obtain a shift of $2 V_{D, o n}$, we place two diodes in series. Figure 3.60 shows the result.
image_name:Figure 3.59 (b)
description:
[
name: I1, type: CurrentSource, ports: {Np: VCC, Nn: Vout}
name: X1, type: Diode, ports: {Na: Vout, Nc: Vin}
name: X2, type: Diode, ports: {Na: Vout, Nc: Vin}
name: Vout, type: VoltageSource, ports: {Np: Vout, Nn: Vin}
]
extrainfo:The circuit shifts the DC level of the input signal by 2 times the diode's forward voltage (2VD,on) using two diodes in series. The output voltage is the input voltage shifted up by this amount.
image_name:Figure 3.60
description:The diagram in Figure 3.60 illustrates a circuit and its corresponding waveform graph, demonstrating a positive voltage shift achieved by using two diodes.

**Circuit Description:**
- The circuit consists of two diodes connected in series. The anode of the first diode is connected to the input voltage \( V_{in} \), while the cathode of the second diode is connected to the output voltage \( V_{out} \).
- The diodes are oriented such that the input is applied to the cathode, shifting the DC level upward.
- A current source \( I_1 \) is connected to the node between the diodes and \( V_{out} \), with the other end connected to \( V_{CC} \), which supplies the necessary bias current.

**Waveform Graph Description:**
- The graph on the right displays two waveforms: \( V_{in} \) (dashed line) and \( V_{out} \) (solid line), both plotted against time \( t \).
- The \( V_{in} \) waveform is a sinusoidal signal centered around a baseline.
- The \( V_{out} \) waveform is a similar sinusoidal signal but shifted upwards by a constant voltage of \( 2V_{D,on} \), where \( V_{D,on} \) is the forward voltage drop across each diode.
- This shift is indicated by a vertical arrow between the two waveforms, labeled \( 2V_{D,on} \).
- The time axis is linear, and the voltage axis is not explicitly labeled with units, but it is implied to be volts.

**Overall Behavior:**
- The primary behavior exhibited is the DC level shift of the input signal by the combined forward voltage drop of the two diodes, resulting in the output signal being consistently higher than the input by \( 2V_{D,on} \).
- This level shift is effective for applications requiring a positive DC offset of an AC signal.

Figure 3.60 Positive voltage shift by two diodes.

What happens if $I_{1}$ is extremely small?

The level shift circuit of Fig. 3.59(b) can be transformed to an electronic switch. For example, many applications employ the topology shown in Fig. 3.61(a) to "sample" $V_{\text {in }}$ across $C_{1}$ and "freeze" the value when $S_{1}$ turns off. Let us replace $S_{1}$ with the level shift circuit and allow $I_{1}$ to be turned on and off [Fig. 3.61(b)]. If $I_{1}$ is on, $V_{\text {out }}$ tracks $V_{\text {in }}$ except for a level shift equal to $V_{D, o n}$. When $I_{1}$ turns off, so does $D_{1}$, evidently disconnecting $C_{1}$ from the input and freezing the voltage across $C_{1}$.
image_name:(a)
description:
[
name: SW, type: Switch, ports: {N1: Vin, N2: Vout}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit diagram (a) is a basic switched-capacitor circuit where the switch SW samples the input voltage Vin across the capacitor C1. When the switch is closed, Vout follows Vin. When the switch is open, the voltage across C1 is held constant, effectively 'freezing' the sampled voltage.
image_name:(b)
description:
[
name: SW, type: Switch, ports: {N1: Vin, N2: Vout}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: GND}
name: D1, type: Diode, ports: {Na: Vin, Nc: Vout}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vout, Nn: GND}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: X1, type: Other, ports: {N1: Vin, N2: Vin}
]
extrainfo:The circuit diagram (b) shows a switched-capacitor circuit with a diode D1 used as a switch to sample and hold the input voltage Vin across capacitor C1. The current source I1 is used to control the operation of the diode, allowing Vout to track Vin when I1 is on, and freezing the voltage across C1 when I1 is off. The circuit illustrates a level-shifting operation where the output voltage Vout is offset by the diode's forward voltage drop when conducting.
image_name:(c)
description:The diagram labeled "(c)" in Figure 3.61 illustrates the behavior of the circuit over time with respect to the input voltage ($V_{in}$), clock signal (CK), and output voltage ($V_{out}$). This is a time-domain waveform graph.

1. **Axes Labels and Units:**
- The horizontal axis represents time ($t$).
- The vertical axis represents voltage, although specific units are not labeled, it is implied to be in volts.

2. **Overall Behavior and Trends:**
- The graph shows three waveforms: $V_{in}$, CK, and $V_{out}$.
- $V_{in}$ is depicted as a sinusoidal waveform, indicating a periodic input voltage.
- CK is a square waveform, representing a clock signal that toggles between two levels.
- $V_{out}$ follows $V_{in}$ with a noticeable phase shift and amplitude change, particularly when $D_1$ turns on and off.

3. **Key Features and Technical Details:**
- At time $t_1$, $D_1$ turns off, which is marked on the graph. At this point, $V_{out}$ begins to diverge from $V_{in}$, indicating the "freezing" effect of the circuit where $C_1$ holds the voltage.
- At time $t_2$, $D_1$ turns on, allowing $V_{out}$ to track $V_{in}$ again, but with a level shift.
- The transition between these states is critical to understanding how the circuit samples and holds the input voltage.

4. **Annotations and Specific Data Points:**
- The graph is annotated with the points $t_1$ and $t_2$ to indicate the switching actions of $D_1$.
- The behavior of $V_{out}$ relative to $V_{in}$ and the clock signal is central to the circuit's function as a sample-and-hold circuit with a level shift.
image_name:(d)
description:
[
name: SW, type: Switch, ports: {N1: Vin, N2: Vout}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: GND}
name: D1, type: Diode, ports: {Na: Vin, Nc: Vout}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vout, Nn: GND}
name: D2, type: Diode, ports: {Na: Vin, Nc: Vout}
name: P, type: Diode, ports: {Na: Vin, Nc: GND}
name: X1, type: Diode, ports: {Na: Vin, Nc: Vout}
]
extrainfo:The circuit uses diodes D1, D2, and P to manage the flow of current and voltage levels. The current source I1 is controlled by a clock signal (CK), and the capacitor C1 is used to store the voltage level. The diodes serve as switches to control the voltage across C1 when I1 is turned off.
image_name:(e)
description:
[
name: X1, type: Other, ports: {N1: Vin, N2: Vout}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit diagram (e) shows a simple configuration with a component X1 connected between Vin and Vout, and a capacitor C1 connected from Vout to ground (GND). This setup is likely used for signal processing or filtering purposes.

Figure 3.61 (a) Switched-capacitor circuit, (b) realization of (a) using a diode as a switch, (c) problem of diode conduction, (d) more complete circuit, (e) equivalent circuit when $I_{1}$ and $I_{2}$ are off.

We used the term "evidently" in the last sentence because the circuit's true behavior somewhat differs from the above description. The assumption that $D_{1}$ turns off holds only if $C_{1}$ draws no current from $D_{1}$, i.e., only if $V_{\text {in }}-V_{\text {out }}$ remains less than $V_{D, \text { on }}$. Now consider the case illustrated in Fig. 3.61(c), where $I_{1}$ turns off at $t=t_{1}$, allowing $C_{1}$ to store a value equal to $V_{i n 1}-V_{D, o n}$. As the input waveform completes a negative excursion and exceeds $V_{\text {in } 1}$ at $t=t_{2}$, the diode is forward-biased again, charging $C_{1}$ with the input (in a manner similar to a peak detector). That is, even though $I_{1}$ is off, $D_{1}$ turns on for part of the cycle.

To resolve this issue, the circuit is modified as shown in Fig. 3.61(d), where $D_{2}$ is inserted between $D_{1}$ and $C_{1}$, and $I_{2}$ provides a bias current for $D_{2}$. With both $I_{1}$ and $I_{2}$ on, the diodes operate in forward bias, $V_{X}=V_{\text {in }}-V_{D 1}$, and $V_{\text {out }}=V_{X}+V_{D 2}=V_{\text {in }}$ if $V_{D 1}=V_{D 2}$. Thus, $V_{\text {out }}$ tracks $V_{\text {in }}$ with no level shift. When $I_{1}$ and $I_{2}$ turn off, the circuit reduces to that in Fig. 3.61(e), where the back-to-back diodes fail to conduct for any value of $V_{\text {in }}-V_{\text {out }}$, thereby isolating $C_{1}$ from the input. In other words, the two diodes and the two current sources form an electronic switch.

Example Recall from Chapter 2 that diodes exhibit a junction capacitance in reverse bias. Study 3.38 the effect of this capacitance on the operation of the above circuit.

Solution Figure 3.62 shows the equivalent circuit for the case where the diodes are off, suggesting that the conduction of the input through the junction capacitances disturbs the output. Specifically, invoking the capacitive divider of Fig. 3.54(b) and assuming
image_name:Figure 3.62
description:
[
name: Cj1, type: Capacitor, value: Cj1, ports: {Np: Vin, Nn: X1}
name: Cj2, type: Capacitor, value: Cj2, ports: {Np: X1, Nn: Vout}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: GND}
name: D1, type: Diode, ports: {Na: Vin, Nc: X1}
name: D2, type: Diode, ports: {Na: Vout, Nc: X1}
]
extrainfo:The circuit diagram represents a diode switch with capacitive feedthrough. The diodes D1 and D2 are used to control the switching, while capacitors Cj1 and Cj2 model the junction capacitance. C1 is used to stabilize the output voltage Vout.

Figure 3.62 Feedthrough in the diode switch.
$C_{j 1}=C_{j 2}=C_{j}$, we have

$$
\begin{equation*}
\Delta V_{\text {out }}=\frac{C_{j} / 2}{C_{j} / 2+C_{1}} \Delta V_{\text {in }} \tag{3.116}
\end{equation*}
$$

To ensure this "feedthrough" is small, $C_{1}$ must be sufficiently large.

Exercise Calculate the change in the voltage at the left plate of $C_{j 1}$ (with respect to ground) in terms of $\Delta V_{i n}$.

## 3.6 CHAPTER SUMMARY

- In addition to the exponential and constant-voltage models, an "ideal" model is sometimes used to analyze diode circuits. The ideal model assumes the diode turns on with a very small forward bias voltage.
- For many electronic circuits, the "input/output characteristics" are studied to understand the response to various input levels, e.g., as the input level goes from $-\infty$ to $+\infty$.
- "Large-signal operation" occurs when a circuit or device experiences arbitrarily large voltage or current excursions. The exponential, constant-voltage, or ideal diode models are used in this case.
- If the changes in voltages and currents are sufficiently small, then nonlinear devices and circuits can be approximated by linear couterparts, greatly simplifying the analysis. This is called "small-signal operation."
- The small-signal model of a diode consists of an "incremental resistance" given by $V_{\mathrm{T}} / \mathrm{I}_{\mathrm{D}}$.
- Diodes find application in many circuits, including rectifiers, limiting circuits, voltage doublers, and level shifters.
- Half-wave rectifiers pass the positive (negative) half cycles of the input wavefrom and block the negative (positive) half cycles. If followed by a capacitor, a rectifier can produce a dc level nearly equal to the peak of the input swing.
- A half-wave rectifier with a smoothing capacitor of value $C_{1}$ and load resistor $R_{\mathrm{L}}$ exhibits an output ripple equal to $\left(V_{\mathrm{P}}-V_{\mathrm{D}, \text { on }}\right) /\left(R_{\mathrm{L}} C_{1} f_{\text {in }}\right)$.
- Full-wave rectifiers convert both positive and negative input cycles to the same polarity at the output. If followed by a smoothing capacitor and a load resistor, these rectifiers exhibit an output ripple given by $0.5\left(V_{\mathrm{P}}-2 V_{\mathrm{D}, \text { on }}\right) /$ ( $R_{\mathrm{L}} C_{1} f_{\text {in }}$ ).
- Diodes can operate as limiting devices, i.e., limit the output swing even if the input swing continues to increase.
