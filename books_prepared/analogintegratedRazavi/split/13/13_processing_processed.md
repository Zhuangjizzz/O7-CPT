# CHAPTER 13 Introduction to Switched-Capacitor Circuits

Our study of amplifiers in previous chapters has dealt only with cases in which the input signal is continuously available and applied to the circuit and the output signal is continuously observed. Called "continuous-time" circuits, such amplifiers find wide application in audio, video, and high-speed analog systems. In many situations, however, we may sense the input only at periodic instants of time, ignoring its value at other times. The circuit then processes each "sample," producing a valid output at the end of each period. Such circuits are called "discrete-time" or "sampled-data" systems.

In this chapter, we study a common class of discrete-time systems called "switched-capacitor (SC) circuits." Our objective is to provide the foundation for more advanced topics such as filters, comparators, ADCs, and DACs. Most of our study deals with switched-capacitor amplifiers, but the concepts can be applied to other discrete-time circuits as well. Beginning with a general view of SC circuits, we describe sampling switches and their speed and precision issues. Next, we analyze switched-capacitor amplifiers, considering unity-gain, noninverting, and multiply-by-two topologies. Finally, we examine a switchedcapacitor integrator.

## 13.1 ■ General Considerations

In order to understand the motivation for sampled-data circuits, let us first consider the simple continuoustime amplifier shown in Fig. 13.1(a), where $V_{\text {out }} / V_{\text {in }}$ is ideally equal to $-R_{2} / R_{1}$. Used extensively with bipolar op amps, this circuit presents a difficult issue if implemented in CMOS technology. Recall that, to achieve a high voltage gain, the open-loop output resistance of CMOS op amps is maximized, typically approaching hundreds of kilohms. We therefore suspect that $R_{2}$ heavily drops the open-loop gain, degrading the precision of the circuit. In fact, with the aid of the simple equivalent circuit shown in
image_name:(a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: InP(Ao)}
name: R2, type: Resistor, value: R2, ports: {N1: InP(Ao), N2: Vout}
name: Av, type: OpAmp, value: Av, ports: {InP: InP(Ao), InN: GND, OutP: Vout}
name: Rout, type: Resistor, value: Rout, ports: {N1: Vout, N2: GND}
]
extrainfo:This is a continuous-time feedback amplifier circuit. The circuit is designed to provide a high voltage gain, but the presence of R2 affects the open-loop gain, especially in CMOS technology.
image_name:(b)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: Vx}
name: R2, type: Resistor, value: R2, ports: {N1: Vx, N2: Vout}
name: -AvVx, type: CurrentControlCurrentSource, value: -AvVx, ports: {InP: -AvVx, InN: GND}
name: Rout, type: Resistor, value: Rout, ports: {N1: -AvVx, N2: Vout}
]
extrainfo:The circuit diagram (b) is an equivalent circuit of a continuous-time feedback amplifier. It models the behavior of the amplifier with resistors R1, R2, and Rout, and an operational amplifier with gain Av. The node Vx is the intermediate node connecting R1 and R2, and the output voltage is taken across Rout.

Figure 13.1 (a) Continuous-time feedback amplifier; (b) equivalent circuit of (a).

Fig. 13.1(b), we can write

$$
\begin{equation*}
-A_{v}\left(\frac{V_{\text {out }}-V_{\text {in }}}{R_{1}+R_{2}} R_{1}+V_{\text {in }}\right)-R_{\text {out }} \frac{V_{\text {out }}-V_{\text {in }}}{R_{1}+R_{2}}=V_{\text {out }} \tag{13.1}
\end{equation*}
$$

and hence

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=-\frac{R_{2}}{R_{1}} \cdot \frac{A_{v}-\frac{R_{\text {out }}}{R_{2}}}{1+\frac{R_{\text {out }}}{R_{1}}+A_{v}+\frac{R_{2}}{R_{1}}} \tag{13.2}
\end{equation*}
$$

Equation (13.2) implies that, compared to the case where $R_{\text {out }}=0$, the closed-loop gain suffers from inaccuracies in both the numerator and the denominator. Also, the input resistance of the amplifier, approximately equal to $R_{1}$, loads the preceding stage while introducing thermal noise.

#### Example 13.1

Using the feedback techniques described in Chapter 8, calculate the closed-loop gain of the circuit of Fig. 13.1(a) and compare the result with Eq. (13.2).

#### Solution

With the aid of the approach described in Example 8.16, the reader can prove that

$$
\begin{align*}
\frac{V_{\text {out }}}{V_{\text {in }}} & =\frac{-R^{2} A_{v}}{R_{2}^{2}+R_{1} R_{\text {out }}+R_{2} R_{\text {out }}+\left(1+A_{v}\right) R_{1} R_{2}}  \tag{13.3}\\
& =-\frac{R_{2}}{R_{1}} \cdot \frac{A_{v}}{\frac{R_{2}}{R_{1}}+\frac{R_{\text {out }}}{R_{2}}+\frac{R_{\text {out }}}{R_{1}}+1+A_{v}} \tag{13.4}
\end{align*}
$$

The two results are approximately equal if $R_{\text {out }} / R_{2} \ll A_{v}$, a condition required to ensure that the transmission through $R_{2}$ is negligible.

In the circuit of Fig. 13.1(a), the closed-loop gain is set by the ratio of $R_{2}$ and $R_{1}$. In order to avoid reducing the open-loop gain of the op amp, we postulate that the resistors can be replaced by capacitors [Fig. 13.2(a)]. Ideally, the gain of the circuit is equal to the impedance of $C_{2}$ divided by the impedance of $C_{1}$ and multiplied by -1 , i.e., equal to $-C_{1} / C_{2}$.
image_name:Figure 13.2 (a)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: X}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Vout}
name: Av, type: OpAmp, value: Av, ports: {InP: GND, InN: X}
]
extrainfo:The circuit is a continuous-time feedback amplifier using capacitors. The closed-loop gain is set by the ratio of C2 and C1, ideally equal to -C1/C2.
image_name:Figure 13.2 (b)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: X}
name: C2, type: Capacitor, value: C2, ports: {Np: Vout, Nn: X}
name: Av, type: OpAmp, value: Av, ports: {InP: GND, InN: X, Out: Vout}
name: RF, type: Resistor, value: RF, ports: {N1: Vout, N2: X}
]
extrainfo:The circuit is a continuous-time feedback amplifier using capacitors with an added feedback resistor RF to define the bias point at node X.

Figure 13.2 (a) Continuous-time feedback amplifier using capacitors; (b) use of resistor to define bias point.
image_name:Figure 13.3
description:The graph in Figure 13.3 is a time-domain waveform illustrating the step response of an amplifier circuit. The x-axis represents time (t), while the y-axis indicates voltage, with two distinct levels labeled as \( V_{in} \) and \( V_{out} \).

Type of Graph and Function:
This is a step response graph, which is used to analyze how an amplifier responds to a sudden change in input voltage over time.

Axes Labels and Units:
- **X-axis (Horizontal):** Represents time (t). The units are not specified, but it typically would be in seconds or milliseconds.
- **Y-axis (Vertical):** Represents voltage. The specific units are not provided, but it is generally in volts.

Overall Behavior and Trends:
- The graph shows a sharp step input \( V_{in} \), which remains constant over time after the initial step.
- The output voltage \( V_{out} \) starts at a lower level and gradually rises, following an exponential curve, towards a steady state. This indicates the amplifier's response to the input step.

Key Features and Technical Details:
- **Initial Response:** The \( V_{out} \) initially increases sharply, indicating a rapid response to the input step.
- **Exponential Rise:** The output voltage follows an exponential growth pattern as it approaches the steady state.
- **Steady State:** Eventually, \( V_{out} \) stabilizes, indicating the completion of the transient response phase.

Annotations and Specific Data Points:
- The graph does not include specific numerical values or annotations for time constants or voltage levels.
- The step input \( V_{in} \) is depicted as a constant voltage level after the initial step, and \( V_{out} \) is shown rising to match this level over time.

This graph effectively demonstrates the transient behavior of the amplifier circuit when subjected to a step input, highlighting the time it takes for the output to stabilize at a new voltage level.

Figure 13.3 Step response of the amplifier of Fig. 13.2(b).

But, how is the bias voltage at node $X$ set? ${ }^{1}$ We may add a large feedback resistor as in Fig. 13.2(b), providing dc feedback while negligibly affecting the ac behavior of the amplifier in the frequency band of interest. Such an arrangement is indeed practical if the circuit senses only high-frequency signals. But suppose, for example, the circuit is to amplify a voltage step. Illustrated in Fig. 13.3, the response contains a step change due to the initial amplification by the circuit consisting of $C_{1}, C_{2}$, and the op amp, followed by a "tail" resulting from the loss of charge on $C_{2}$ through $R_{F}$. From another point of view, the circuit may not be suited to amplify wideband signals because it exhibits a high-pass transfer function. In fact, the transfer function is given by

$$
\begin{align*}
\frac{V_{\text {out }}}{V_{\text {in }}}(s) & \approx-\frac{R_{F} \frac{1}{C_{2} s}}{R_{F}+\frac{1}{C_{2} s}} \div \frac{1}{C_{1} s}  \tag{13.5}\\
& =-\frac{R_{F} C_{1} s}{R_{F} C_{2} s+1} \tag{13.6}
\end{align*}
$$

indicating that $V_{\text {out }} / V_{\text {in }} \approx-C_{1} / C_{2}$ only if $\omega \gg\left(R_{F} C_{2}\right)^{-1}$.
The above difficulty can be remedied by increasing $R_{F} C_{2}$, but in many applications the required values of the two components become prohibitively large. We must therefore seek other methods of establishing the bias while utilizing capacitive feedback networks.

It is possible to replace $R_{F}$ in Fig. 13.2(b) with a switch. Illustrated in Fig. 13.4, the idea is to turn $S_{2}$ on so as to place the op amp in unity-gain feedback and force $V_{X}$ to $V_{B}$, an appropriately chosen input common-mode level for the op amp. After the switch turns off, node $X$ retains this voltage, allowing proper operation. Of course, when $S_{2}$ is on, the circuit does not amplify $V_{i n}$.
image_name:Figure 13.4
description:
[
name: S2, type: Switch, ports: {N1: X, N2: Vout}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: X}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Vout}
name: Av, type: OpAmp, value: Av, ports: {InP: VB, InN: X, Out: Vout}
]
extrainfo:The circuit uses a switch S2 to establish unity-gain feedback, defining the DC input level. When S2 is closed, the op-amp forces node X to VB, setting the input common-mode level.

Figure 13.4 Use of feedback switch to define dc input level.

Let us now consider the switched-capacitor circuit depicted in Fig. 13.5, where three switches control the operation: $S_{1}$ and $S_{3}$ connect the left plate of $C_{1}$ to $V_{i n}$ and ground, respectively, and $S_{2}$ provides unity-gain feedback. We first assume that the open-loop gain of the op amp is very large and study the circuit in two phases. First, $S_{1}$ and $S_{2}$ are on and $S_{3}$ is off, yielding the equivalent circuit of Fig. 13.6(a). For a high-gain op amp, $V_{B}=V_{\text {out }} \approx 0$, and hence the voltage across $C_{1}$ is approximately equal to $V_{\text {in }}$.

[^92]image_name:Figure 13.5 Switched-capacitor amplifier
description:
[
name: S1, type: Switch, ports: {N1: Vin, N2: A}
name: S2, type: Switch, ports: {N1: X, N2: Vout}
name: S3, type: Switch, ports: {N1: A, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: A, Nn: X}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Vout}
name: OpAmp, type: OpAmp, ports: {InP: GND, InN: X, OutP: Vout}
]
extrainfo:The circuit is a switched-capacitor amplifier with two modes: sampling and amplification. In sampling mode, S1 and S2 are on, and S3 is off, allowing C1 to sample the input voltage. In amplification mode, S1 and S2 are off, and S3 is on, grounding node A and amplifying the input signal with a gain of -C1/C2.

Figure 13.5 Switched-capacitor amplifier.
image_name:(a)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: A, Nn: X}
name: Av, type: OpAmp, value: Av, ports: {InP: GND, InN: X, OutP: X(Vout)}
]
extrainfo:The circuit is a switched-capacitor amplifier in sampling mode. In this mode, C1 samples the input voltage Vin, and the op-amp is configured to amplify the input signal. The output voltage is determined by the gain -C1/C2. The waveform shows the input voltage Vin, node voltage VA, and output voltage Vout, highlighting the transition at time t0 when the mode changes.
image_name:(b)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: A(GND), Nn: X}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Vout}
name: Av, type: OpAmp, value: Av, ports: {InP: GND, InN: X, OutP: Vout}
]
extrainfo:The circuit is a switched-capacitor amplifier with two modes: sampling and amplification. In sampling mode, S1 and S2 are on, and S3 is off, allowing C1 to sample the input voltage. In amplification mode, S1 and S2 are off, and S3 is on, grounding node A and amplifying the input signal with a gain of -C1/C2. The output voltage changes from zero to Vin0 * C1 / C2 when the mode switches.
image_name:(c)
description:The graph in Figure 13.6(c) illustrates the input and output waveforms for a switched-capacitor amplifier operating in two distinct modes: sampling and amplification. The graph is a time-domain waveform plot that shows how voltage changes over time.

**Axes Labels and Units:**
- The x-axis represents time (t), with a specific reference point marked as \( t_0 \).
- The y-axis represents voltage, with three separate plots for \( V_{in} \), \( V_A \), and \( V_{out} \).

**Overall Behavior and Trends:**
- **\( V_{in} \):** This waveform is a sinusoidal signal, indicating a periodic input voltage. It remains consistent throughout both modes.
- **\( V_A \):** Initially follows the input \( V_{in} \) during the sampling mode, showing a similar sinusoidal pattern. At \( t = t_0 \), when the circuit transitions to amplification mode, \( V_A \) drops to zero as node A is grounded.
- **\( V_{out} \):** Starts at zero and remains constant during the sampling phase. At \( t = t_0 \), the output voltage begins to rise, transitioning from zero to a steady state at \( V_{in0} \frac{C_1}{C_2} \), indicating the amplification process.

**Key Features and Technical Details:**
- The transition at \( t = t_0 \) is critical, marking the shift from sampling to amplification. This is where \( S_1 \) and \( S_2 \) turn off, and \( S_3 \) turns on.
- The gain of the amplifier is represented by the ratio \( -\frac{C_1}{C_2} \), as reflected in the final output voltage level.

**Annotations and Specific Data Points:**
- \( V_{in0} \) is marked on the \( V_A \) waveform, indicating the initial input voltage level before the transition.
- \( V_{in0} \frac{C_1}{C_2} \) is marked as the final steady-state output voltage level, demonstrating the effect of amplification.

Overall, the graph effectively shows the behavior of the switched-capacitor amplifier, illustrating the shift in voltage levels as the circuit transitions between its two modes of operation.

Figure 13.6 Circuit of Fig. 13.5 in (a) sampling mode, (b) amplification mode (c) input and output waveforms in the two modes.

We say that $C_{1}$ samples the input. Next, at $t=t_{0}, S_{1}$ and $S_{2}$ turn off and $S_{3}$ turns on, pulling node $A$ to ground. Since the gain is equal to $-C_{1} / C_{2}$ and since $V_{A}$ changes from $V_{i n 0}$ to 0 , the output voltage must change from zero to $V_{i n 0} C_{1} / C_{2}$.

The output voltage change can also be calculated by examining the transfer of charge. Note that the charge stored on $C_{1}$ just before $t_{0}$ is equal to $V_{i n 0} C_{1}$. After $t=t_{0}$, the negative feedback through $C_{2}$ drives the op amp input differential voltage, and hence the voltage across $C_{1}$, to zero (Fig. 13.7). The charge stored on $C_{1}$ at $t=t_{0}$ must then be transferred to $C_{2}$, producing an output voltage equal to $V_{i n 0} C_{1} / C_{2}$. Thus, the circuit amplifies $V_{i n 0}$ by a factor of $C_{1} / C_{2}$.
image_name:Figure 13.7 Transfer of charge from C1 to C2
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: GND, Nn: InN(Av)}
name: C2, type: Capacitor, value: C2, ports: {Np: InN(A1), Nn: Vout}
name: Av, type: OpAmp, value: Av, ports: {InP: GND, InN: InN(Av), Out: Vout}
]
extrainfo:The circuit transfers charge from C1 to C2, amplifying the input voltage Vin by a factor of C1/C2. Initially, C1 is charged with Vin0, and after t=t0, the charge is transferred to C2, setting Vout to Vin0*C1/C2. The circuit operates in two phases: sampling and amplification.

Figure 13.7 Transfer of charge from $C_{1}$ to $C_{2}$.

Several attributes of the circuit of Fig. 13.5 distinguish it from continuous-time implementations. First, the circuit devotes some time to "sampling" the input, setting the output to zero and providing no amplification during this period. Second, after sampling, for $t>t_{0}$, the circuit ignores the input voltage $V_{i n}$, amplifying the sampled voltage. Third, the circuit configuration changes considerably from one phase to another, as seen in Fig. 13.6(a) and (b), raising concern about its stability. Note that $S_{2}$ must turn on periodically to compensate for the leakage currents that slowly discharge $X$. These currents arise from $S_{2}$ itself and the gate leakage of the op amp.

What is the advantage of the amplifier of Fig. 13.5 over that in Fig. 13.1? In addition to sampling capability, we note from the waveforms depicted in Fig. 13.6 that after $V_{\text {out }}$ settles to $V_{\text {in }} \cdot C_{1} / C_{2}$, the current through $C_{2}$ approaches zero. That is, the feedback capacitor does not reduce the open-loop gain of the amplifier if the output voltage is given enough time to settle. In Fig. 13.1, on the other hand, $R_{2}$ loads the amplifier continuously.

The switched-capacitor amplifier of Fig. 13.5 lends itself to implementation in CMOS technology much more easily than in other technologies. This is because discrete-time operations require switches to perform sampling as well as a high input impedance to sense the stored quantities with no corruption. For example, if the op amp of Fig. 13.5 incorporates bipolar transistors at its input, the base current drawn from the inverting input in the amplification phase [Fig. 13.6(b)] creates an error in the output voltage. The existence of simple switches and a high input impedance have made CMOS technology the dominant choice for sampled-data applications.

The foregoing discussion leads to the conceptual view illustrated in Fig. 13.8 for switched-capacitor amplifiers. In the simplest case, the operation takes place in two phases: sampling and amplification. Thus, in addition to the analog input, $V_{i n}$, the circuit requires a clock to define each phase.

Our study of SC amplifiers proceeds according to these two phases. First, we analyze various sampling techniques. Second, we consider SC amplifier topologies.
image_name:Figure 13.8 General view of switched-capacitor amplifier
description:The block diagram represents a general view of a switched-capacitor amplifier, which operates in two distinct phases: sampling and amplification. The diagram consists of two main blocks connected in series, with additional control provided by a clock signal (CK).

1. **Main Components:**
- **Sampling Block:** This block includes a switch and a capacitor. The switch is controlled by the clock signal (CK) and is used to sample the input voltage, \( V_{in} \). When the clock signal is high, the switch closes, allowing the capacitor to charge to the input voltage level.
- **Amplifier Block:** This block consists of an operational amplifier with a feedback capacitor. The sampled voltage from the sampling block is fed into this amplifier block, where it is amplified.

2. **Flow of Information or Control:**
- The input voltage \( V_{in} \) is first directed to the sampling block. Here, the switch, controlled by the clock signal, determines when the input is sampled.
- Once the input is sampled, the stored charge on the capacitor is transferred to the amplifier block.
- The operational amplifier then processes this input, and the amplified output voltage \( V_{out} \) is generated.
- The clock signal (CK) orchestrates the timing of these phases, switching between sampling and amplification.

3. **Labels, Annotations, and Key Indicators:**
- **\( V_{in} \):** Input voltage signal.
- **\( V_{out} \):** Output voltage signal.
- **CK:** Clock signal that controls the switching between the sampling and amplification phases.
- A timing diagram is included below the blocks, showing the clock signal's high phase corresponding to the sampling phase and the low phase corresponding to the amplification phase.

4. **Overall System Function:**
- The primary function of this system is to sample an analog input voltage and subsequently amplify it. The switched-capacitor topology allows precise sampling and amplification controlled by the clock signal. This design is particularly useful in sampled-data applications, where the timing of the sample and hold operation is critical for accurate signal processing.
image_name:CK
description:The graph labeled "CK" is a time-domain waveform illustrating the operation of a switched-capacitor amplifier circuit. The x-axis represents time, denoted as 't', and is likely measured in seconds or a submultiple like milliseconds or microseconds, although specific units are not labeled. The y-axis represents the clock signal, 'CK', which is a digital waveform with two distinct levels corresponding to the sampling and amplification phases.

Overall Behavior and Trends:
The waveform is a rectangular pulse, indicating a digital clock signal used to control the switched-capacitor amplifier. The waveform consists of two primary phases:
1. **Sample Phase:** The clock signal 'CK' is high, indicating the period during which the input voltage, 'V_in', is sampled. This phase is represented by the elevated portion of the waveform.
2. **Amplify Phase:** The clock signal 'CK' returns to low, marking the transition to the amplification phase where the previously sampled voltage is processed by the amplifier.

Key Features and Technical Details:
- **Transition Points:** The waveform shows clear transitions from low to high and back to low, indicating the precise timing of sampling and amplification phases.
- **Pulse Width:** The width of the high pulse represents the duration of the sampling phase, which is crucial for determining how long the input signal is observed.
- **Repetition:** Although not explicitly shown, such waveforms typically repeat periodically to continuously sample and amplify input signals.

Annotations and Specific Data Points:
- The graph includes annotations indicating the "Sample" and "Amplify" phases directly beneath the waveform, providing clarity on the function of each phase.
- No specific numerical values or gridlines are provided, but the waveform's rectangular shape and annotations suffice to understand the timing sequence of the switched-capacitor amplifier operation.

Figure 13.8 General view of switched-capacitor amplifier.

## 13.2 ■ Sampling Switches

### 13.2.1 MOSFETS as Switches

A simple sampling circuit consists of a switch and a capacitor [Fig. 13.9(a)]. A MOS transistor can serve as a switch [Fig. 13.9(b)] because it can be on while carrying a zero current.

To understand how the circuit of Fig. 13.9(b) samples the input, first consider the simple cases depicted in Fig. 13.10, where the gate command, $C K$, goes high at $t=t_{0}$. In Fig. 13.10(a), we assume that $V_{i n}=0$ and the capacitor has an initial voltage equal to $V_{D D}$. Thus, at $t=t_{0}, M_{1}$ senses a gate-source voltage equal to $V_{D D}$ while its drain voltage is also equal to $V_{D D}$. The transistor therefore operates in saturation, drawing a current of $I_{D 1}=\left(\mu_{n} C_{o x} / 2\right)(W / L)\left(V_{D D}-V_{T H}\right)^{2}$ from the capacitor. As $V_{\text {out }}$ falls, at some
image_name:Figure 13.9 (a)
description:
[
name: C_H, type: Capacitor, value: C_H, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a sampling circuit. In Figure 13.9(a), a simple switch is used to connect Vin to Vout through a capacitor CH. In Figure 13.9(b), the switch is implemented using an NMOS transistor M1, where the gate is controlled by a clock signal CK.
image_name:Figure 13.9 (b)
description:
[
name: C_H, type: Capacitor, value: CH, ports: {Np: Vout, Nn: GND}
name: M1, type: NMOS, ports: {S: Vout, D: Vin, G: CK}
]
extrainfo:Figure 13.9(b) shows a sampling circuit using an NMOS transistor M1 as a switch. The capacitor CH is connected between the output node Vout and ground. The gate of M1 is controlled by the clock signal CK, allowing it to sample Vin when CK is high.

Figure 13.9 (a) Simple sampling circuit; (b) implementation of the switch by a MOS device.
image_name:(a)
description:The graph labeled "(a)" in the image depicts a time-domain waveform related to the sampling circuit described. It shows the behavior of the output voltage \( V_{out} \) over time \( t \) when the input voltage \( V_{in} \) is 0.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph illustrating the discharge process of a capacitor in a sampling circuit.

2. **Axes Labels and Units:**
- The horizontal axis represents time \( t \), though no specific units are provided, it is typically measured in seconds or milliseconds in such contexts.
- The vertical axis represents the output voltage \( V_{out} \), with a starting value of \( V_{DD} \), the supply voltage.

3. **Overall Behavior and Trends:**
- Initially, at time \( t_0 \), the output voltage \( V_{out} \) is at the supply voltage level \( V_{DD} \).
- As time progresses, \( V_{out} \) decreases exponentially towards zero.
- This behavior indicates the discharge of the capacitor \( C_H \) through the NMOS transistor \( M_1 \) when the clock signal \( CK \) is high.

4. **Key Features and Technical Details:**
- The graph shows an exponential decay, typical of an RC discharge circuit.
- The point where \( V_{out} \) begins to decrease is marked as \( t_0 \), indicating the moment the clock signal activates the NMOS switch.
- The rate of decay is determined by the time constant of the circuit, which depends on the resistance and capacitance values.

5. **Annotations and Specific Data Points:**
- The graph starts at \( V_{DD} \) and approaches zero as time increases.
- There are no specific numerical values or annotations provided for the time constant or the exact rate of decay, but the general trend is clear from the graph's shape.
image_name:(b)
description:The graph in Figure 13.9(b) is a time-domain waveform that illustrates the behavior of the output voltage \( V_{out} \) over time in a sampling circuit using an NMOS transistor as a switch. The specific scenario depicted is when the input voltage \( V_{in} \) is set to +1V.

Axes Labels and Units:
- **Horizontal Axis (x-axis):** Represents time \( t \), though the specific units are not labeled, it is typically in seconds or milliseconds for such circuits.
- **Vertical Axis (y-axis):** Represents the output voltage \( V_{out} \), with key values marked at 0V and +1V.

Overall Behavior and Trends:
- The waveform starts at 0V at time \( t_0 \), indicating that the output capacitor \( C_H \) is initially discharged.
- As time progresses, \( V_{out} \) increases, following an exponential rise towards the input voltage level of +1V. This behavior is characteristic of the charging process of a capacitor through a resistor-like path, as the NMOS transistor in this configuration behaves like a resistor when \( V_{out} \) is much less than \( 2(V_{DD} - V_{TH}) \).

Key Features and Technical Details:
- The waveform exhibits an exponential rise from 0V to +1V, indicating the charging of the capacitor \( C_H \) through the NMOS switch.
- The initial point \( t_0 \) marks the moment when the clock signal \( CK \) transitions from high to low, enabling the NMOS switch and allowing the capacitor to charge.
- The rate of rise is determined by the equivalent resistance \( R_{on} \) of the NMOS transistor and the capacitance \( C_H \).

Annotations and Specific Data Points:
- The graph is annotated with the key voltage level of +1V, which is the final value that \( V_{out} \) approaches as time progresses.
- The transition point \( t_0 \) is marked, indicating the time when the clock signal changes state, allowing the sampling action to commence.

Figure 13.10 Response of a sampling circuit to different input levels and initial conditions.
point $V_{o u t}=V_{D D}-V_{T H}$, driving $M_{1}$ into the triode region. The device nevertheless continues to discharge $C_{H}$ until $V_{\text {out }}$ approaches zero. We note that for $V_{\text {out }} \ll 2\left(V_{D D}-V_{T H}\right)$, the transistor can be viewed as a resistor equal to $R_{o n}=\left[\mu_{n} C_{o x}(W / L)\left(V_{D D}-V_{T H}\right)\right]^{-1}$.

Now consider the case in Fig. 13.10(b), where $V_{\text {in }}=+1 \mathrm{~V}, V_{\text {out }}\left(t=t_{0}\right)=0 \mathrm{~V}$, and $V_{D D}=3 \mathrm{~V}$. Here, the terminal of $M_{1}$ connected to $C_{H}$ acts as the source, and the transistor turns on with $V_{G S}=+3$ V , but $V_{D S}=+1 \mathrm{~V}$. Thus, $M_{1}$ operates in the triode region, charging $C_{H}$ until $V_{\text {out }}$ approaches +1 V . For $V_{\text {out }} \approx+1 \mathrm{~V}, M_{1}$ exhibits an on-resistance of $R_{o n}=\left[\mu_{n} C_{o x}(W / L)\left(V_{D D}-V_{\text {in }}-V_{T H}\right)\right]^{-1}$.

The above observations reveal two important points. First, a MOS switch can conduct current in either direction simply by exchanging the role of its source and drain terminals. Second, as shown in Fig. 13.11, when the switch is on, $V_{\text {out }}$ follows $V_{\text {in }}$, and when the switch is off, $V_{o u t}$ remains constant. Thus, the circuit "tracks" the signal when $C K$ is high and "freezes" the instantaneous value of $V_{i n}$ across $C_{H}$ when C K goes low.

#### Example 13.2

In the circuit of Fig. 13.10(a), calculate $V_{\text {out }}$ as a function of time. Assume that $\lambda=0$.

#### Solution

Before $V_{\text {out }}$ drops below $V_{D D}-V_{T H}, M_{1}$ is saturated and we have

$$
\begin{align*}
V_{\text {out }}(t) & =V_{D D}-\frac{I_{D 1} t}{C_{H}}  \tag{13.7}\\
& =V_{D D}-\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{D D}-V_{T H}\right)^{2} \frac{t}{C_{H}} \tag{13.8}
\end{align*}
$$

image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: Vout, D: Vin, G: High}
name: C_H, type: Capacitor, value: C_H, ports: {Np: Vout, Nn: GND}
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'Vin', 'N2': 'Vout'
'name': 'C_H', 'type': 'Capacitor', 'value': 'C_H', 'ports': {'N1': 'Vout', 'N2': 'Vout'
]
extrainfo:The circuit is a track and hold sampling circuit. The NMOS transistor M1 is used as a switch controlled by the input voltage Vin. When the switch is closed, the capacitor CH charges to the input voltage. The resistor R is used to control the charging time constant.

image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: Vout, D: Vin, G: High}
name: C_H, type: Capacitor, value: C_H, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a track and hold sampling circuit with an NMOS transistor, a resistor, and a capacitor. The NMOS transistor is controlled by a 'Low' signal, and the output voltage is sampled across the capacitor CH.

Figure 13.11 Track and hold capabilities of a sampling circuit.
After

$$
\begin{equation*}
t_{1}=\frac{2 V_{T H} C_{H}}{\mu_{n} C_{o x} \frac{W}{L}\left(V_{D D}-V_{T H}\right)^{2}} \tag{13.9}
\end{equation*}
$$

$M_{1}$ enters the triode region, yielding a time-dependent current. We therefore write

$$
\begin{align*}
C_{H} \frac{d V_{\text {out }}}{d t} & =-I_{D 1}  \tag{13.10}\\
& =-\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left[2\left(V_{D D}-V_{T H}\right) V_{\text {out }}-V_{\text {out }}^{2}\right] \quad t>t_{1} \tag{13.11}
\end{align*}
$$

Rearranging (13.11), we have

$$
\begin{equation*}
\frac{d V_{\text {out }}}{\left[2\left(V_{D D}-V_{T H}\right)-V_{\text {out }}\right] V_{\text {out }}}=-\frac{1}{2} \mu_{n} \frac{C_{\text {ox }}}{C_{H}} \frac{W}{L} d t \tag{13.12}
\end{equation*}
$$

which, upon separation into partial fractions, is written as

$$
\begin{equation*}
\left[\frac{1}{V_{\text {out }}}+\frac{1}{2\left(V_{D D}-V_{T H}\right)-V_{\text {out }}}\right] \frac{d V_{\text {out }}}{V_{D D}-V_{T H}}=-\mu_{n} \frac{C_{o x}}{C_{H}} \frac{W}{L} d t \tag{13.13}
\end{equation*}
$$

Thus,

$$
\begin{equation*}
\ln V_{\text {out }}-\ln \left[2\left(V_{D D}-V_{T H}\right)-V_{\text {out }}\right]=-\left(V_{D D}-V_{T H}\right) \mu_{n} \frac{C_{o x}}{C_{H}} \frac{W}{L}\left(t-t_{1}\right) \tag{13.14}
\end{equation*}
$$

that is

$$
\begin{equation*}
\ln \frac{V_{\text {out }}}{2\left(V_{D D}-V_{T H}\right)-V_{\text {out }}}=-\left(V_{D D}-V_{T H}\right) \mu_{n} \frac{C_{\text {ox }}}{C_{H}} \frac{W}{L}\left(t-t_{1}\right) \tag{13.15}
\end{equation*}
$$

Taking the exponential of both sides and solving for $V_{\text {out }}$, we obtain

$$
\begin{equation*}
V_{o u t}=\frac{2\left(V_{D D}-V_{T H}\right) \exp \left[-\left(V_{D D}-V_{T H}\right) \mu_{n} \frac{C_{o x}}{C_{H}} \cdot \frac{W}{L}\left(t-t_{1}\right)\right]}{1+\exp \left[-\left(V_{D D}-V_{T H}\right) \mu_{n} \frac{C_{o x}}{C_{H}} \cdot \frac{W}{L}\left(t-t_{1}\right)\right]} \tag{13.16}
\end{equation*}
$$

image_name:Figure 13.12 Maximum output level in an NMOS sampler
description:
[
name: M1, type: NMOS, ports: {S: Vout, D: VDD, G: CK}
name: CH, type: Capacitor, value: CH, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is an NMOS sampler with an input voltage Vin set to VDD. The NMOS transistor M1 is controlled by a clock signal CK. The output voltage Vout changes over time as shown in the graph, reaching a maximum of VDD - VTH.
image_name:Vout vs time
description:The graph titled "Vout vs time" is a time-domain waveform representing the output voltage \( V_{\text{out}} \) of an NMOS sampler circuit over time.

**Axes Labels and Units:**
- The horizontal axis represents time \( t \), but no specific units are provided. It is implied to be in seconds or a subunit thereof.
- The vertical axis represents the output voltage \( V_{\text{out}} \) in volts.

**Overall Behavior and Trends:**
- The graph illustrates an exponential rise in the output voltage \( V_{\text{out}} \) as time progresses.
- Initially, \( V_{\text{out}} \) starts at 0 volts and increases toward \( V_{DD} - V_{TH} \) as \( t \) increases.
- The shape of the curve is characteristic of a charging capacitor in an RC circuit, where the voltage asymptotically approaches its maximum value.

**Key Features and Technical Details:**
- The curve starts at the origin (0,0), indicating that \( V_{\text{out}} \) is zero at \( t=0 \).
- As time progresses, the curve rises sharply initially and then gradually flattens out as it approaches the voltage level \( V_{DD} - V_{TH} \), indicating saturation.
- The curve does not reach \( V_{DD} \) entirely, due to the threshold voltage \( V_{TH} \) of the transistor.

**Annotations and Specific Data Points:**
- A step input \( V_{\text{in}} = V_{DD} \) is applied at the beginning of the time axis, which is reflected in the waveform.
- The graph does not provide specific numerical values for \( V_{DD} \) or \( V_{TH} \), but the trend and behavior are clearly illustrated.

This graph provides insight into the transient response of the NMOS sampler circuit when a step voltage \( V_{DD} \) is applied, showing how \( V_{\text{out}} \) evolves over time until it stabilizes at \( V_{DD} - V_{TH} \).

Figure 13.12 Maximum output level in an NMOS sampler.
In the circuit of Fig. 13.10(b), we assumed that $V_{i n}=+1 \mathrm{~V}$ (Fig. 13.12). Now suppose $V_{i n}=V_{D D}$. How does $V_{\text {out }}$ vary with time? Since the gate and drain of $M_{1}$ are at the same potential, the transistor is saturated, and we have

$$
\begin{align*}
C_{H} \frac{d V_{\text {out }}}{d t} & =I_{D 1}  \tag{13.17}\\
& =\frac{1}{2} \mu_{n} C_{\text {ox }} \frac{W}{L}\left(V_{D D}-V_{\text {out }}-V_{T H}\right)^{2} \tag{13.18}
\end{align*}
$$

where channel-length modulation is neglected. It follows that

$$
\begin{equation*}
\frac{d V_{\text {out }}}{\left(V_{D D}-V_{\text {out }}-V_{T H}\right)^{2}}=\frac{1}{2} \mu_{n} \frac{C_{\text {ox }}}{C_{H}} \frac{W}{L} d t \tag{13.19}
\end{equation*}
$$

and hence

$$
\begin{equation*}
\left.\frac{1}{V_{D D}-V_{\text {out }}-V_{T H}}\right|_{0} ^{\text {Vout }}=\left.\frac{1}{2} \mu_{n} \frac{C_{o x}}{C_{H}} \frac{W}{L} t\right|_{0} ^{t} \tag{13.20}
\end{equation*}
$$

where body effect is neglected and $V_{\text {out }}(t=0)$ is assumed zero. Thus,

$$
\begin{equation*}
V_{\text {out }}=V_{D D}-V_{T H}-\frac{1}{\frac{1}{2} \mu_{n} \frac{C_{o x}}{C_{H}} \frac{W}{L} t+\frac{1}{V_{D D}-V_{T H}}} \tag{13.21}
\end{equation*}
$$

Equation (13.21) implies that as $t \rightarrow \infty, V_{\text {out }} \rightarrow V_{D D}-V_{T H}$. This is because as $V_{\text {out }}$ approaches $V_{D D}-V_{T H}$, the overdrive voltage of $M_{1}$ vanishes, reducing the current available for charging $C_{H}$ to negligible values. Of course, even for $V_{o u t}=V_{D D}-V_{T H}$, the transistor conducts some subthreshold current and, given enough time, eventually brings $V_{\text {out }}$ to $V_{D D}$. Nonetheless, as mentioned in Chapter 3, for typical operation speeds, it is reasonable to assume that $V_{\text {out }}$ does not exceed $V_{D D}-V_{T H}$.

The foregoing analysis demonstrates a serious limitation of MOS switches: if the input signal level is close to $V_{D D}$, then the output provided by an NMOS switch cannot track the input. From another point of view, the on-resistance of the switch increases considerably as the input and output voltages approach $V_{D D}-V_{T H}$. We may then ask-What is the maximum input level that the switch can pass to the output faithfully? In Fig. 13.12, for $V_{\text {out }} \approx V_{i n}$, the transistor must operate in the deep triode region, and hence the upper bound of $V_{i n}$ equals $V_{D D}-V_{T H}$. As explained later, in practice, $V_{i n}$ must be quite lower than this value.

#### Example 13.3

In the circuit of Fig. 13.13, calculate the minimum and maximum on-resistance of $M_{1}$. Assume that $\mu_{n} C_{o x}=$ $50 \mu \mathrm{~A} / \mathrm{V}^{2}, W / L=10 / 1, V_{T H}=0.7 \mathrm{~V}, V_{D D}=3 \mathrm{~V}$, and $\gamma=0$.
image_name:f_{in} = 10 MHz
description:The graph depicted is a time-domain waveform representing the input and output voltages of a circuit involving a transistor $M_1$ and a capacitor $C_H$. The input signal, labeled $f_{in} = 10 \text{ MHz}$, is shown on the left side of the diagram. It is a sinusoidal waveform with a frequency of 10 MHz and an amplitude of 0.5 V. The horizontal axis represents time $t$, and the vertical axis represents voltage in volts.

The output signal, $V_{out}$, is displayed on the right side of the diagram. It mirrors the input waveform, indicating that $V_{out}$ tracks $V_{in}$ closely. This correspondence suggests that the transistor $M_1$ is operating in a region where it allows the output to follow the input with minimal phase shift or amplitude distortion.

The circuit schematic in the center shows a transistor $M_1$ connected to a 3 V supply and a 1 pF capacitor $C_H$. The gate of the transistor is driven by the input voltage, and the source is connected to the output node $V_{out}$. The configuration suggests that $M_1$ is acting as a pass transistor, allowing the input signal to pass through to the output while the capacitor $C_H$ likely serves to stabilize or filter the output signal.

Overall, the graph indicates that the design achieves a high-fidelity transmission of the input signal to the output, appropriate for the given frequency and amplitude, and confirms the transistor's operation in the desired region, as described in the context.
image_name:Figure 13.13
description:
[
name: M1, type: NMOS, ports: {S: Vout, D: Vin, G: 3V}
name: CH, type: Capacitor, value: 1 pF, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit consists of an NMOS transistor M1 and a capacitor CH. The NMOS operates in the triode region to allow Vout to track Vin with a negligible phase shift. The input frequency is 10 MHz, and the input and output signals have a peak of +0.5 V.
image_name:
description:The diagram consists of a circuit schematic and two time-domain waveforms. The circuit features a MOSFET labeled as M1, with its gate connected to a +3 V supply, and its source connected to the output voltage, V_out. A capacitor, C_H, with a capacitance of 1 pF, is connected to V_out and grounded.

On either side of the circuit, there are two identical sinusoidal waveforms representing input and output voltages over time. Both waveforms have an amplitude of +0.5 V and a frequency of 10 MHz, as indicated by the label 'f_in = 10 MHz'. The waveforms are plotted against time (t) on the horizontal axis. The vertical axis represents voltage, although it is not explicitly labeled.

The waveforms suggest that the input and output signals are sinusoidal with no visible phase shift, indicating that V_out closely tracks V_in. This behavior is consistent with the operation of M1 in the triode region, where the on-resistance is low, allowing the output to follow the input with minimal distortion or delay.

#### Solution

We note that in the steady state, $M_{1}$ remains in the triode region because the gate voltage is higher than both $V_{i n}$ and $V_{\text {out }}$ by a value greater than $V_{T H}$. If $f_{\text {in }}=10 \mathrm{MHz}$, we predict that $V_{\text {out }}$ tracks $V_{\text {in }}$ with a negligible phase shift due to the on-resistance of $M_{1}$ and $C_{H}$. Assuming that $V_{\text {out }} \approx V_{i n}$, we need not distinguish between the source and drain terminals, obtaining

$$
\begin{equation*}
R_{o n 1}=\frac{1}{\mu_{n} C_{o x} \frac{W}{L}\left(V_{D D}-V_{i n}-V_{T H}\right)} \tag{13.22}
\end{equation*}
$$

Thus, $R_{\text {on } 1, \max } \approx 1.11 \mathrm{k} \Omega$ and $R_{\text {on } 1, \min } \approx 870 \Omega$. By contrast, if the maximum input level is raised to 1.5 V , then $R_{\text {on } 1, \max }=2.5 \mathrm{k} \Omega$.

MOS devices operating in the deep triode region are sometimes called "zero-offset" switches to emphasize that they exhibit no dc shift between the input and output voltages of the simple sampling circuit of Fig. 13.9(b). ${ }^{2}$ This is evident from the examples of Fig. 13.10, where the output eventually becomes equal to the input. Nonexistent in bipolar technology, the zero-offset property proves crucial in precise sampling of analog signals.

We have thus far considered only NMOS switches. The reader can verify that the foregoing principles apply to PMOS switches as well. In particular, as shown in Fig. 13.14, a PMOS transistor fails to operate as a switch if its gate is grounded and its drain terminal senses an input voltage of $\left|V_{T H P}\right|$ or less. In other words, the on-resistance of the device rises rapidly as the input and output levels drop to $\left|V_{T H P}\right|$ above ground.
image_name:Figure 13.14 Sampling circuit using PMOS switch
description:
[
name: M1, type: PMOS, ports: {S: Vout, D: Vin, G: CK}
name: CH, type: Capacitor, value: CH, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a sampling circuit using a PMOS switch. The PMOS transistor M1 is controlled by the clock signal CK. When CK is low, M1 is on, allowing the capacitor CH to charge to VDD. The output voltage Vout decreases over time as the capacitor discharges. The diagram also shows the timing diagram for CK and Vout, illustrating the switching behavior and the effect on Vout.
image_name:Figure 13.14 Sampling circuit using PMOS switch.
description:The graph in Figure 13.14 is a time-domain waveform illustrating the definition of speed in a sampling circuit. It consists of two waveforms plotted against time (t), with the x-axis labeled as time (t) and no specific units provided. The y-axis represents voltage levels, with two distinct traces: one for the clock (CK) signal and one for the output voltage (V_out).

1. **Clock Signal (CK):**
- The CK signal is shown as a step waveform. It starts at a high voltage level, labeled as V_DD, and then abruptly transitions to a low voltage level (ground, 0). This transition represents the activation of the sampling process.

2. **Output Voltage (V_out):**
- The V_out waveform begins at the same high voltage level, V_DD, and exhibits an exponential decay towards a lower voltage level. This decay continues until it approaches a threshold voltage level, labeled as |V_THP|, indicating the point where the PMOS switch fails to effectively conduct.

3. **Overall Behavior and Trends:**
- The graph illustrates the time it takes for the output voltage to transition from the initial high level (V_DD) to the threshold level (|V_THP|). This transition time is a measure of the speed of the sampling circuit.
- The exponential nature of the decay in V_out suggests the presence of capacitive discharge, likely influenced by the parasitic capacitance in the circuit.

4. **Key Features and Technical Details:**
- The critical transition in the CK signal is marked by a sharp drop from V_DD to 0, indicating the moment when the sampling begins.
- The V_out decay curve is smooth and exponential, highlighting the gradual discharge process.
- The threshold level |V_THP| is crucial as it marks the limit below which the PMOS switch's resistance becomes too high for effective operation.

5. **Annotations and Specific Data Points:**
- The graph does not provide specific numerical values for time or voltage, but the labels V_DD and |V_THP| serve as reference points for understanding the voltage levels involved in the circuit's operation.

### 13.2.2 Speed Considerations

What determines the speed of the sampling circuits of Fig. 13.9? We must first define the speed here. Illustrated in Fig. 13.15, a simple measure of speed is the time required for the output voltage to go

image_name:Figure 13.15 Definition of speed in a sampling circuit
description:
[
name: M1, type: NMOS, ports: {S: Vout, D: Vin, G: CK}
name: CH, type: Capacitor, value: CH, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a sampling circuit using an NMOS switch (M1) controlled by the clock (CK). The capacitor (CH) stores the sampled voltage. The graph illustrates the speed of the sampling circuit, showing how the output voltage (Vout) approaches the input voltage (Vin0) over time, settling within a specified error band (ΔV) after a time period (tS).
image_name:Figure 13.15 Definition of speed in a sampling circuit
description:The graph in Figure 13.15 is a time-domain waveform illustrating the definition of speed in a sampling circuit. The horizontal axis represents time (t), while the vertical axis represents the output voltage (V_out). The graph depicts how the output voltage changes over time after the switch in the circuit is activated.

Axes and Units:
- **Horizontal Axis (Time, t):** No specific units are provided, but it is understood to represent time progression.
- **Vertical Axis (Voltage, V_out):** Represents the output voltage level, with reference points labeled as V_DD and V_in0.

Overall Behavior and Trends:
- The waveform starts at zero when the time is zero, indicating that the output voltage V_out initially is at ground level.
- After the switch is turned on, V_out begins to rise towards the input voltage level, V_in0.
- The curve shows an exponential rise, starting steep and gradually leveling off as it approaches V_in0.
- The output voltage does not reach V_in0 instantaneously but takes time to settle within a specified error band, ΔV.

Key Features and Technical Details:
- The rise of V_out is marked with a settling time, t_S, which is the time it takes for V_out to reach within a certain percentage (e.g., 0.1%) of the final value V_in0.
- ΔV represents the error band around the final value V_in0, indicating the range within which V_out is considered settled.
- The waveform does not reach V_in0 exactly but approaches it asymptotically.

Annotations and Specific Data Points:
- V_DD is marked on the vertical axis as a reference for the maximum voltage level.
- V_in0 is indicated as the target level for V_out.
- The settling time t_S is marked on the time axis, showing the point where V_out is within ΔV of V_in0.

This graph effectively illustrates the concept of speed in a sampling circuit by showing how quickly the output voltage can settle to the input voltage level after the switch is activated, within an acceptable error margin.

Figure 13.15 Definition of speed in a sampling circuit.
from zero to the maximum input level after the switch turns on. Since $V_{\text {out }}$ would take infinite time to become equal to $V_{i n 0}$, we consider the output settled when it is within a certain "error band," $\Delta V$, around the final value. For example, we say that the output settles to $0.1 \%$ accuracy after $t_{S}$ seconds, meaning that in Fig. 13.15, $\Delta V / V_{i n 0}=0.1 \%$. Thus, the speed specification must be accompanied by an accuracy specification as well. Note that after $t=t_{S}$, we can consider the source and drain voltages to be approximately equal.

From the circuit of Fig. 13.15, we surmise that the sampling speed is given by two factors: the onresistance of the switch and the value of the sampling capacitor. Thus, to achieve a higher speed, a large aspect ratio and a small capacitor must be used. However, as illustrated in Fig. 13.13, the on-resistance also depends on the input level, yielding a greater time constant for more positive inputs (in the case of NMOS switches). From Eq. (13.22), we plot the on-resistance of the switch as a function of the input level [Fig. 13.16(a)], noting the sharp rise as $V_{i n}$ approaches $V_{D D}-V_{T H}$. For example, if we restrict the variation of $R_{o n}$ to a range of 4 to 1 , then the maximum input level is given by

$$
\begin{equation*}
\frac{1}{\mu_{n} C_{o x} \frac{W}{L}\left(V_{D D}-V_{i n, \max }-V_{T H}\right)}=\frac{4}{\mu_{n} C_{o x} \frac{W}{L}\left(V_{D D}-V_{T H}\right)} \tag{13.23}
\end{equation*}
$$

That is

$$
\begin{equation*}
V_{i n, \max }=\frac{3}{4}\left(V_{D D}-V_{T H}\right) \tag{13.24}
\end{equation*}
$$

This value falls around $V_{D D} / 2$, translating to severe swing limitations. Note that the device threshold voltage directly limits the voltage swings. ${ }^{3}$
image_name:(a)
description:The graph labeled "(a)" is a plot of the on-resistance \( R_{on,N} \) of an NMOS device as a function of the input voltage \( V_{in} \). The graph is a line plot with the following details:

1. **Axes Labels and Units:**
- The horizontal axis represents the input voltage \( V_{in} \), with no specific units marked, assuming volts (V).
- The vertical axis represents the on-resistance \( R_{on,N} \), with no specific units marked, assuming ohms (Ω).

2. **Overall Behavior and Trends:**
- The graph shows an increasing trend in the on-resistance \( R_{on,N} \) as the input voltage \( V_{in} \) increases.
- The curve starts at a relatively low resistance value when \( V_{in} \) is close to zero and rises steeply as \( V_{in} \) approaches \( V_{DD} - V_{TH} \).

3. **Key Features and Technical Details:**
- There is a significant increase in the on-resistance as the input voltage approaches the threshold \( V_{DD} - V_{TH} \), indicating a steep rise in resistance.
- The graph is asymptotic near \( V_{DD} - V_{TH} \), suggesting a sharp increase in resistance beyond this point.
- A dashed vertical line is marked at \( V_{DD} - V_{TH} \), highlighting this critical threshold voltage.

4. **Annotations and Specific Data Points:**
- The graph includes a dashed vertical line at \( V_{DD} - V_{TH} \) on the \( V_{in} \) axis, indicating a key threshold value where the behavior of the NMOS on-resistance changes significantly.
- There are no specific numerical values or additional annotations provided on the graph.
image_name:(b)
description:The graph labeled (b) is a plot of the on-resistance \( R_{on,P} \) of a PMOS device as a function of the input voltage \( V_{in} \).

1. **Type of Graph and Function:**
- This is a line graph showing the relationship between the on-resistance of a PMOS transistor and its input voltage.

2. **Axes Labels and Units:**
- The horizontal axis represents the input voltage \( V_{in} \), with the scale starting from 0. The units are in volts, although not explicitly marked.
- The vertical axis represents the on-resistance \( R_{on,P} \) of the PMOS device. The units are in ohms, though not explicitly marked.

3. **Overall Behavior and Trends:**
- The graph shows a decreasing trend of the on-resistance as the input voltage increases.
- Initially, when \( V_{in} \) is around 0, the on-resistance is high.
- As \( V_{in} \) increases, \( R_{on,P} \) decreases rapidly.
- The curve appears to approach an asymptote, indicating that the resistance levels off at higher input voltages.

4. **Key Features and Technical Details:**
- A significant point on the graph is marked at \( |V_{THP}| \), which is the threshold voltage for the PMOS device.
- The on-resistance decreases significantly after the input voltage surpasses \( |V_{THP}| \).

5. **Annotations and Specific Data Points:**
- The dashed vertical line at \( |V_{THP}| \) indicates the threshold voltage, a critical point where the behavior of the device changes notably.
- No specific numerical values are provided for \( R_{on,P} \) or \( V_{in} \), other than the threshold voltage marker.

Figure 13.16 On-resistance of (a) NMOS and (b) PMOS devices as a function of input voltage.

In order to accommodate greater voltage swings in a sampling circuit, we first observe that a PMOS switch exhibits an on-resistance that decreases as the input voltage becomes more positive [Fig. 13.16(b)]. It is then plausible to employ "complementary" switches so as to allow rail-to-tail swings. Shown in Fig. 13.17(a), such a combination requires complementary clocks, producing an equivalent resistance:

$$
\begin{aligned}
R_{o n, e q} & =R_{o n, N} \| R_{o n, P} \\
& =\frac{1}{\mu_{n} C_{o x}(W / L)_{N}\left(V_{D D}-V_{i n}-V_{T H N}\right)} \| \frac{1}{\mu_{p} C_{o x}(W / L)_{P}\left(V_{i n}-\left|V_{T H P}\right|\right)}
\end{aligned}
$$

It follows that

$$
\begin{aligned}
& R_{o n, e q}= \\
& \frac{1}{\mu_{n} C_{o x}(W / L)_{N}\left(V_{D D}-V_{T H N}\right)-\left[\mu_{n} C_{o x}(W / L)_{N}-\mu_{p} C_{o x}(W / L)_{P}\right] V_{i n}-\mu_{p} C_{o x}(W / L)_{P}\left|V_{T H P}\right|}
\end{aligned}
$$

image_name:Figure 13.17 (a)
description:
[
name: M1, type: NMOS, ports: {S: Vin, D: Vout, G: CK}
name: M2, type: PMOS, ports: {S: Vout, D: Vin, G: CK_bar}
name: CH, type: Capacitor, value: CH, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit diagram represents a complementary switch with NMOS and PMOS transistors controlled by a clock signal 'CK'. The output is taken across the capacitor CH connected to Vout and ground.

image_name:Figure 13.17 (b)
description:The graph in Figure 13.17(b) is a plot of the on-resistance of a complementary switch as a function of the input voltage \( V_{in} \). The x-axis represents the input voltage \( V_{in} \) and is marked with two significant points: \( |V_{THP}| \) and \( V_{DD} - V_{TH} \). The y-axis represents the on-resistance, although it is not labeled with specific units.

The graph displays three curves:

1. **\( R_{on,P} \)**: This curve represents the on-resistance of the PMOS transistor. It starts at a higher resistance when \( V_{in} \) is less than \( |V_{THP}| \) and decreases as \( V_{in} \) increases, approaching zero as \( V_{in} \) nears \( V_{DD} - V_{TH} \).

2. **\( R_{on,N} \)**: This curve shows the on-resistance of the NMOS transistor. It begins at a lower resistance when \( V_{in} \) is greater than \( V_{DD} - V_{TH} \) and increases as \( V_{in} \) decreases, moving towards \( |V_{THP}| \).

3. **\( R_{on,eq} \)**: This is the equivalent on-resistance of the complementary switch, which is a combination of the NMOS and PMOS resistances. The curve for \( R_{on,eq} \) is relatively flat compared to the individual resistances, indicating less variation across the range of \( V_{in} \).

The overall behavior shows that while \( R_{on,P} \) and \( R_{on,N} \) vary significantly with \( V_{in} \), their combination \( R_{on,eq} \) remains more stable, demonstrating the advantage of using a complementary switch configuration to minimize resistance variation with input voltage.

Figure 13.17 (a) Complementary switch; (b) on-resistance of the complementary switch.
Interestingly, if $\mu_{n} C_{o x}(W / L)_{N}=\mu_{p} C_{o x}(W / L)_{P}$, then $R_{o n, e q}$ is independent of the input level. ${ }^{4}$ Figure 13.17(b) plots the behavior of $R_{o n, e q}$ in the general case, revealing much less variation than that corresponding to each switch alone. We quantify the effect of switch nonlinearity in Chapter 14.

For high-speed input signals, it is critical that the NMOS and PMOS switches in Fig. 13.17(a) turn off simultaneously so as to avoid ambiguity in the sampled value. If, for example, the NMOS device turns off $\Delta t$ seconds earlier than the PMOS device, then the output voltage tends to track the input for the remaining $\Delta t$ seconds, but with a large, input-dependent time constant (Fig. 13.18). This effect gives rise to distortion in the sampled value. For moderate precision, the simple circuit shown in Fig. 13.19 provides complementary clocks by duplicating the delay of inverter $I_{1}$ through the pass gate $G_{2}$.

### 13.2.3 Precision Considerations

Our foregoing study of MOS switches indicates that a larger $W / L$ or a smaller sampling capacitor results in a higher speed. In this section, we show that these methods of increasing the speed degrade the precision with which the signal is sampled.

Three mechanisms in MOS transistor operation introduce error at the instant the switch turns off. We study each effect individually.

image_name:Figure 13.18
description:The graph in Figure 13.18 consists of two main parts, illustrating the distortion generated if complementary switches do not turn off simultaneously.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform, showing the behavior of complementary clock signals and their effect on input and output voltages.

2. **Axes Labels and Units:**
- The horizontal axis represents time (denoted as 't'), though no specific units are provided.
- The vertical axis is not explicitly labeled but represents voltage levels for the clock signals and input/output voltages.

3. **Overall Behavior and Trends:**
- The first part of the graph shows two complementary clock signals, CK and \(\overline{CK}\), crossing each other with a small time difference \(\Delta t\). This indicates that the switches do not turn off at the exact same time, leading to a timing mismatch.
- The second part of the graph shows the input voltage \(V_{in}\) as a sinusoidal waveform and the output voltage \(V_{out}\) following a similar pattern but with noticeable distortion. The output voltage deviates from an ideal value, which is indicated by a dashed line.

4. **Key Features and Technical Details:**
- The key feature here is the timing mismatch \(\Delta t\) between the complementary clock signals, which is crucial in understanding the distortion at the output.
- The distortion in \(V_{out}\) is depicted as a deviation from the ideal value, highlighting the impact of non-simultaneous switch-off on signal integrity.

5. **Annotations and Specific Data Points:**
- \(\Delta t\) is annotated on the clock signal graph, emphasizing the timing difference.
- The ideal value of \(V_{out}\) is marked as a dashed line, showing the expected behavior without distortion.
image_name:Figure 13.18
description: consists of two main parts: the top part illustrates complementary clock signals, and the bottom part depicts a comparison between input and output waveforms.

1. **Type of Graph and Function:**
- The top graph is a timing diagram showing the relationship between two complementary clock signals, labeled as CK and \( \overline{CK} \).
- The bottom graph is a time-domain waveform comparison, showing input (\( V_{in} \)) and output (\( V_{out} \)) voltages over time.

2. **Axes Labels and Units:**
- The horizontal axis in both graphs represents time (t), though specific units are not provided.
- The vertical axis in the top graph represents the logic levels of the clock signals CK and \( \overline{CK} \).
- The vertical axis in the bottom graph represents voltage levels for \( V_{in} \) and \( V_{out} \), though specific voltage units are not provided.

3. **Overall Behavior and Trends:**
- In the top graph, CK and \( \overline{CK} \) are complementary signals with a crossover point, indicating a non-zero delay (\( \Delta t \)) between their transitions.
- In the bottom graph, \( V_{in} \) is a sinusoidal waveform, while \( V_{out} \) follows a similar shape but is slightly distorted, with a noticeable deviation from the ideal value at certain points.

4. **Key Features and Technical Details:**
- The top graph highlights the delay \( \Delta t \) between the falling edge of CK and the rising edge of \( \overline{CK} \), which is a critical parameter in timing analysis.
- The bottom graph shows that \( V_{out} \) does not perfectly follow \( V_{in} \), indicating some form of distortion or error introduced in the signal processing.
- The ideal value for \( V_{out} \) is marked with a dashed line, showing where the output should ideally align with the input.

5. **Annotations and Specific Data Points:**
- The top graph includes an annotation for \( \Delta t \), emphasizing the timing mismatch between the complementary clocks.
- The bottom graph includes an annotation for the "Ideal Value" of \( V_{out} \), highlighting the discrepancy between the actual and expected output.

Figure 13.18 Distortion generated if complementary switches do not turn off simultaneously.

image_name:Figure 13.19
description:The circuit is designed to generate complementary clock signals CK and CK_bar from the input clock CKin using an NMOS transistor and an inverter.

Figure 13.19 Simple circuit generating complementary clocks.

Channel Charge Injection Consider the sampling circuit of Fig. 13.20, and recall that for a MOSFET to be on, a channel must exist at the oxide-silicon interface. Assuming that $V_{\text {in }} \approx V_{\text {out }}$, we use our derivations in Chapter 2 to express the total charge in the inversion layer as

$$
\begin{equation*}
Q_{c h}=W L C_{o x}\left(V_{D D}-V_{i n}-V_{T H}\right) \tag{13.25}
\end{equation*}
$$

where $L$ denotes the effective channel length. When the switch turns off, $Q_{c h}$ exits through the source and drain terminals, a phenomenon called "channel charge injection."
image_name:Figure 13.20 Charge injection when a switch turns off.
description:
[
name: M1, type: NMOS, ports: {S: Vout, D: Vin, G: CK}
name: CH, type: Capacitor, value: CH, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit illustrates charge injection in a switch when it turns off, affecting the voltage across the capacitor CH. The NMOS transistor M1 is controlled by the clock signal CK, allowing charge to flow from Vin to Vout when on. When M1 turns off, charge injection occurs, potentially causing an error voltage on CH.

The charge injected to the left side of Fig. 13.20 is absorbed by the input source, creating no error. On the other hand, the charge injected to the right side is deposited on $C_{H}$, introducing an error in the voltage stored on the capacitor. For example, if half of $Q_{c h}$ is injected onto $C_{H}$, the resulting error equals

$$
\begin{equation*}
\Delta V=\frac{W L C_{o x}\left(V_{D D}-V_{i n}-V_{T H}\right)}{2 C_{H}} \tag{13.26}
\end{equation*}
$$

Illustrated in Fig. 13.21, the error for an NMOS switch appears as a negative "pedestal" at the output. Note that the error is directly proportional to $W L C_{o x}$ and inversely proportional to $C_{H}$.
image_name:Figure 13.21 Effect of charge injection.
description:The graph in Figure 13.21 illustrates the effect of charge injection in a circuit using an NMOS switch. The diagram is composed of three main parts:

1. **Input Waveform (Left Side):**
- The left side of the figure shows an input sinusoidal waveform labeled as $V_{in}$. This waveform represents the input voltage to the circuit. The sinusoidal shape indicates a periodic oscillation, typical of alternating current (AC) signals.

2. **Circuit Diagram (Center):**
- At the center of the figure, there is a schematic of a simple circuit involving an NMOS transistor labeled as $M_1$. The gate of the transistor is controlled by a clock signal labeled "CK," represented by a square waveform. This suggests that the transistor is being switched on and off periodically.
- The source of the transistor is connected to the input voltage $V_{in}$, and the drain is connected to the output $V_{out}$.
- A capacitor labeled $C_{H}$ is connected between the output $V_{out}$ and ground (GND), which stores charge when the transistor is conducting.

3. **Output Waveform (Right Side):**
- The right side of the figure shows the output waveform $V_{out}$, which is a sinusoidal wave similar to the input but with a noticeable negative "pedestal" or dip, labeled as $\Delta V$. This indicates the error introduced by charge injection when the transistor switches.
- The dip in the waveform corresponds to the moment when the transistor turns off, and part of the channel charge is injected onto the capacitor $C_{H}$, leading to a temporary voltage drop.

Overall, the figure demonstrates how charge injection from the NMOS switch affects the output voltage, creating a negative voltage error (pedestal) at the output. This error is proportional to the dimensions of the transistor ($WL$) and the oxide capacitance ($C_{ox}$), and inversely proportional to the holding capacitance ($C_{H}$), as described by the equation provided in the context.

An important question that arises now is-Why did we assume in arriving at (13.26) that exactly half of the channel charge is injected onto $C_{H}$ ? In reality, the fraction of charge that exits through the source and drain terminals is a relatively complex function of various parameters, such as the impedance seen at each terminal to ground and the transition time of the clock [1, 2]. Investigations of this effect have not yielded any rule of thumb that can predict the charge splitting in terms of such parameters. Furthermore, in many cases, these parameters, e.g., the clock transition time, are poorly controlled. Also, most circuit simulation programs model charge injection quite inaccurately. As a worst-case estimate, we can assume that the entire channel charge is injected onto the sampling capacitor.

How does charge injection affect the precision? Assuming that all of the charge is deposited on the capacitor, we express the sampled output voltage as

$$
\begin{equation*}
V_{\text {out }} \approx V_{\text {in }}-\frac{W L C_{o x}\left(V_{D D}-V_{\text {in }}-V_{T H}\right)}{C_{H}} \tag{13.27}
\end{equation*}
$$

where the phase shift between the input and the output is neglected. Thus,

$$
\begin{equation*}
V_{o u t}=V_{i n}\left(1+\frac{W L C_{o x}}{C_{H}}\right)-\frac{W L C_{o x}}{C_{H}}\left(V_{D D}-V_{T H}\right) \tag{13.28}
\end{equation*}
$$

suggesting that the output deviates from the ideal value through two effects: a nonunity gain equal to $1+W L C_{o x} / C_{H},{ }^{5}$ and a constant offset voltage $-W L C_{o x}\left(V_{D D}-V_{T H}\right) / C_{H}$ (Fig. 13.22). In other words, since we have assumed that channel charge is a linear function of the input voltage, the circuit exhibits only gain error and dc offset.
image_name:Figure 13.22 Input/output characteristic of sampling circuit in the presence of charge injection
description:Figure 13.22 shows the input/output characteristic of a sampling circuit when charge injection is present. The graph is a linear plot with two primary lines: one labeled "Ideal" and the other labeled "With Charge Injection." The x-axis represents the input voltage $V_{in}$, while the y-axis represents the sampled output voltage $V_{out}$. Both axes are likely in volts, although specific units are not provided.

The "Ideal" line is a dashed line that passes through the origin, illustrating a direct proportional relationship between $V_{in}$ and $V_{out}$ with no offset or gain error. This line represents the expected behavior of the circuit without any charge injection.

The solid line labeled "With Charge Injection" deviates from the ideal line, indicating a gain error and a DC offset. The line is shifted downward, starting from a negative offset on the y-axis, labeled "Offset," and has a slope greater than the ideal line, indicating a non-unity gain. This represents the effect of charge injection, which introduces both a constant offset voltage and a gain error in the output.

Overall, the graph highlights the impact of charge injection on the circuit's performance, showing how the actual output deviates from the ideal linear relationship due to these effects.

Figure 13.22 Input/output characteristic of sampling circuit in the presence of charge injection.

In the foregoing discussion, we tacitly assumed that $V_{T H}$ is constant. However, for NMOS switches (in an $n$-well technology), body effect must be taken into account. ${ }^{6}$ Since $V_{T H}=V_{T H 0}+\gamma\left(\sqrt{2 \phi_{B}+V_{S B}}-\sqrt{2 \phi_{B}}\right)$,

[^96]and $V_{B S} \approx-V_{i n}$, we have
\$\$

$$
\begin{align*}
V_{o u t}= & V_{i n}-\frac{W L C_{o x}}{C_{H}}\left(V_{D D}-V_{i n}-V_{T H 0}-\gamma \sqrt{2 \phi_{B}+V_{i n}}+\gamma \sqrt{2 \phi_{B}}\right)  \tag{13.29}\\
= & V_{i n}\left(1+\frac{W L C_{o x}}{C_{H}}\right)+\gamma \frac{W L C_{o x}}{C_{H}} \sqrt{2 \phi_{B}+V_{i n}} \\
& -\frac{W L C_{o x}}{C_{H}}\left(V_{D D}-V_{T H 0}+\gamma \sqrt{2 \phi_{B}}\right) \tag{13.30}
\end{align*}
$$

\$\$

It follows that the nonlinear dependence of $V_{T H}$ upon $V_{i n}$ introduces nonlinearity in the input/output characteristic.

In summary, charge injection contributes three types of errors in MOS sampling circuits: gain error, dc offsets, and nonlinearity. In many applications, the first two can be tolerated or corrected whereas the last cannot.

It is instructive to consider the speed-precision trade-off resulting from charge injection. Representing the speed by a simple time constant $\tau$ and the precision by the error $\Delta V$ due to charge injection, we define a figure of merit as $F=(\tau \Delta V)^{-1}$. Writing

$$
\begin{align*}
\tau & =R_{o n} C_{H}  \tag{13.31}\\
& =\frac{1}{\mu_{n} C_{o x}(W / L)\left(V_{D D}-V_{i n}-V_{T H}\right)} C_{H} \tag{13.32}
\end{align*}
$$

and

$$
\begin{equation*}
\Delta V=\frac{W L C_{o x}}{C_{H}}\left(V_{D D}-V_{i n}-V_{T H}\right) \tag{13.33}
\end{equation*}
$$

we have

$$
\begin{equation*}
F=\frac{\mu_{n}}{L^{2}} \tag{13.34}
\end{equation*}
$$

Thus, to the first order, the trade-off is independent of the switch width and the sampling capacitor.
Clock Feedthrough In addition to channel charge injection, a MOS switch couples the clock transitions to the sampling capacitor through its gate-drain or gate-source overlap capacitance. Depicted in Fig. 13.23, the effect introduces an error in the sampled output voltage. Assuming the overlap capacitance is constant, we express the error as

$$
\begin{equation*}
\Delta V=V_{C K} \frac{W C_{o v}}{W C_{o v}+C_{H}} \tag{13.35}
\end{equation*}
$$

image_name:Figure 13.23 Clock feedthrough in a sampling circuit
description:
[
name: M1, type: NMOS, ports: {S: Vout, D: Vin, G: VCK}
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: VCK, Nn: Vin}
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: VCK, Nn: Vout}
name: CH, type: Capacitor, value: CH, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit demonstrates clock feedthrough in a sampling circuit, where the NMOS transistor M1 introduces an error in the sampled output voltage due to overlap capacitance.

Figure 13.23 Clock feedthrough in a sampling circuit.
where $C_{o v}$ is the overlap capacitance per unit width. The error $\Delta V$ is independent of the input level, manifesting itself as a constant offset in the input/output characteristic. As with charge injection, clock feedthrough leads to a trade-off between speed and precision as well.
$\boldsymbol{k T} / \mathbf{C}$ Noise Recall from Example 7.3 that a resistor charging a capacitor gives rise to a total rms noise voltage of $\sqrt{k T / C}$. As shown in Fig. 13.24, a similar effect occurs in sampling circuits. The on-resistance of the switch introduces thermal noise at the output and, when the switch turns off, this noise is stored on the capacitor along with the instantaneous value of the input voltage. It can be proved that the rms voltage of the sampled noise in this case is still approximately equal to $\sqrt{k T / C}[3,4]$.
image_name:Figure 13.24 Thermal noise in a sampling circuit
description:
[
name: Ron, type: Resistor, value: Ron, ports: {N1: Vin, N2: Vout}
name: CH, type: Capacitor, value: CH, ports: {Np: Vout, Nn: GND}
'name': 'Ropen', 'type': 'Resistor', 'value': 'Ropen', 'ports': {'N1': 'Vin+Vn', 'N2': 'Vout'
'name': 'CH', 'type': 'Capacitor', 'value': 'CH', 'ports': {'Np': 'Vin+Vn', 'Nn': 'GND'
]
extrainfo:The circuit diagram shows a sampling circuit with thermal noise. The resistor Ron charges the capacitor CH, and when the switch is open, the resistor Ropen is introduced, leading to a noise voltage Vn added to the input voltage Vin at the output.

Figure 13.24 Thermal noise in a sampling circuit.
The problem of $k T / C$ noise limits the performance in many high-precision applications. In order to achieve low noise, the sampling capacitor must be sufficiently large, thus loading other circuits and degrading the speed.

### 13.2.4 Charge Injection Cancellation

The dependence of charge injection upon the input level and the trade-off expressed by (13.34) make it necessary to seek methods of canceling the effect of charge injection so as to achieve a higher $F$. We consider a few such techniques here.

To arrive at the first technique, we postulate that the charge injected by the main transistor can be removed by means of a second transistor. As shown in Fig. 13.25, a "dummy" switch, $M_{2}$, driven by $\overline{C K}$ is added to the circuit such that after $M_{1}$ turns off and $M_{2}$ turns on, the channel charge deposited by the former on $C_{H}$ is absorbed by the latter to create a channel. Note that both the source and drain of $M_{2}$ are connected to the output node.
image_name:Figure 13.25
description:
[
name: M1, type: NMOS, ports: {S: Vout, D: Vin, G: CK}
name: M2, type: NMOS, ports: {S: Vout, D: Vout, G: CK_bar}
name: CH, type: Capacitor, value: CH, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit uses a dummy NMOS transistor M2 to absorb the charge injected by the main NMOS transistor M1 to reduce charge injection and clock feedthrough effects. The charge injected by M1, Δq1, is countered by the charge absorbed by M2, Δq2.

Figure 13.25 Addition of dummy device to reduce charge injection and clock feedthrough.

How do we ensure that the charge injected by $M_{1}, \Delta q_{1}$, is equal to that absorbed by $M_{2}, \Delta q_{2}$ ? Suppose half of the channel charge of $M_{1}$ is injected onto $C_{H}$, i.e.,

$$
\begin{equation*}
\Delta q_{1}=\frac{W_{1} L_{1} C_{o x}}{2}\left(V_{C K}-V_{i n}-V_{T H 1}\right) \tag{13.36}
\end{equation*}
$$

Since $\Delta q_{2}=W_{2} L_{2} C_{o x}\left(V_{C K}-V_{i n}-V_{T H 2}\right)$, if we choose $W_{2}=0.5 W_{1}$ and $L_{2}=L_{1}$, then $\Delta q_{2}=\Delta q_{1}$. Unfortunately, the assumption of equal splitting of charge between source and drain is generally invalid, making this approach less attractive.

Interestingly, with the choice $W_{2}=0.5 W_{1}$ and $L_{2}=L_{1}$, the effect of clock feedthrough is suppressed. As depicted in Fig. 13.26, the total charge in $V_{\text {out }}$ is zero because

$$
\begin{equation*}
-V_{C K} \frac{W_{1} C_{o v}}{W_{1} C_{o v}+C_{H}+2 W_{2} C_{o v}}+V_{C K} \frac{2 W_{2} C_{o v}}{W_{1} C_{o v}+C_{H}+2 W_{2} C_{o v}}=0 \tag{13.37}
\end{equation*}
$$

image_name:Figure 13.26
description:
[
name: M1, type: NMOS, ports: {S: Vout, D: Vin, G: CK}
name: M2, type: NMOS, ports: {S: Vout, D: Vout, G: Ck_bar}
name: Cgs1, type: Capacitor, value: Cgs1, ports: {Np: CK, Nn: Vout}
name: Cgd2, type: Capacitor, value: Cgd2, ports: {Np: Ck_bar, Nn: Vout}
name: Cgs2, type: Capacitor, value: Cgs2, ports: {Np: Ck_bar, Nn: Vout}
name: CH, type: Capacitor, value: CH, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit implements a charge injection cancellation approach using NMOS transistors M1 and M2, and capacitors to suppress clock feedthrough. The configuration ensures that the total charge at Vout is zero for the given conditions.
image_name:Figure 13.26
description:
[
name: W1Cov, type: Capacitor, value: W1Cov, ports: {Np: Ck, Nn: Vout}
name: 2W2Cov, type: Capacitor, value: 2W2Cov, ports: {Np: Ck_bar, Nn: Vout}
name: CH, type: Capacitor, value: CH, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit in Figure 13.26 is designed to suppress clock feedthrough using a dummy switch configuration. It uses NMOS transistors M1 and M2 along with capacitors to achieve charge cancellation. The effect of clock feedthrough is minimized by balancing the charge injection from the transistors. The right side of the diagram illustrates the equivalent circuit with capacitors W1Cov and 2W2Cov, which further aids in charge cancellation.

Figure 13.26 Clock feedthrough suppression by dummy switch.
Another approach to lowering the effect of charge injection incorporates both PMOS and NMOS devices such that the opposite charge packets injected by the two cancel each other (Fig. 13.27). For $\Delta q_{1}$ to cancel $\Delta q_{2}$, we must have $W_{1} L_{1} C_{o x}\left(V_{C K}-V_{i n}-V_{T H N}\right)=W_{2} L_{2} C_{o x}\left(V_{i n}-\left|V_{T H P}\right|\right)$. Thus, the cancellation occurs for only one input level. Even for clock feedthrough, the circuit does not provide complete cancellation because the gate-drain overlap capacitance of NFETs is not equal to that of PFETs.
image_name:Figure 13.27
description:
[
name: M1, type: NMOS, ports: {S: Vin, D: Vout, G: CK}
name: M2, type: PMOS, ports: {S: Vout, D: Vin, G: CK_bar}
name: CH, type: Capacitor, value: CH, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit uses complementary switches (M1 and M2) to reduce charge injection. M1 injects electrons and M2 injects holes, aiming to cancel each other's charge injection effects. The capacitor CH is connected between the output node Vout and ground.

Figure 13.27 Use of complementary switches to reduce charge injection.

Our knowledge of the advantages of differential circuits suggests that the problem of charge injection may be relieved through differential operation. As shown in Fig. 13.28, we surmise that charge injection appears as a common-mode disturbance. But, writing $\Delta q_{1}=W L C_{o x}\left(V_{C K}-V_{i n 1}-V_{T H 1}\right)$ and $\Delta q_{2}=$ $W L C_{o x}\left(V_{C K}-V_{i n 2}-V_{T H 2}\right)$, we recognize that $\Delta q_{1}=\Delta q_{2}$ only if $V_{i n 1}=V_{i n 2}$. In other words, the overall error is not suppressed for differential signals. Nevertheless, this technique both removes the

image_name:Figure 13.28 Differential sampling circuit
description:
[
name: M1, type: NMOS, ports: {S: Vout1, D: Vin1, G: CK}
name: M2, type: NMOS, ports: {S: Vout2, D: CK, G: Vin2}
name: CH1, type: Capacitor, value: CH, ports: {Np: Vout1, Nn: GND}
name: CH2, type: Capacitor, value: CH, ports: {Np: Vout2, Nn: GND}
]
extrainfo:The circuit is a differential sampling circuit using NMOS transistors M1 and M2, controlled by the clock signal CK. Each transistor's drain is connected to the clock, and sources are connected to separate output nodes Vout1 and Vout2. Capacitors CH are used to sample and hold the output voltages.

Figure 13.28 Differential sampling circuit.
constant offset and lowers the nonlinear component. This can be understood by writing

$$
\begin{align*}
\Delta q_{1}-\Delta q_{2} & =W L C_{o x}\left[\left(V_{i n 2}-V_{i n 1}\right)+\left(V_{T H 2}-V_{T H 1}\right)\right]  \tag{13.38}\\
& =W L C_{o x}\left[V_{i n 2}-V_{i n 1}+\gamma\left(\sqrt{2 \phi_{F}+V_{i n 2}}-\sqrt{2 \phi_{F}+V_{i n 1}}\right)\right] \tag{13.39}
\end{align*}
$$

Since for $V_{i n 1}=V_{i n 2}, \Delta q_{1}-\Delta q_{2}=0$, the characteristic exhibits no offset. Also, the nonlinearity of body effect now appears in both square-root terms of (13.39), leading to only odd-order distortion (Chapter 14).

The problem of charge injection continues to limit the speed-precision envelope in sampled-data systems. Many cancellation techniques have been introduced, but each leads to other trade-offs. One such technique, called "bottom-plate sampling," is widely used in switched-capacitor circuits and is described later in this chapter.

## 13.3 ■ Switched-Capacitor Amplifiers

As mentioned in Sec. 13.1 and exemplified by the circuit of Fig. 13.5, CMOS feedback amplifiers are more easily implemented with a capacitive feedback network than with a resistive one. Having examined sampling techniques, we are now ready to study a number of switched-capacitor amplifiers. Our objective is to understand the underlying principles as well as the speed-precision trade-offs encountered in the design of each circuit.

Before studying SC amplifiers, it is helpful to look briefly at the physical implementation of capacitors in CMOS technology. A simple capacitor structure is shown in Fig. 13.29(a), where the "top plate" and the "bottom plate" are realized by metal layers. An important concern in using this structure is the parasitic capacitance between each plate and the substrate. In particular, the bottom plate suffers from capacitance, $C_{p}$, to the underlying substrate-a value typically 5 to $10 \%$ of the main capacitance. For this reason, we usually model the capacitor as in Fig. 13.29(b). Monolithic capacitors are described in more detail in Chapters 18 and 19 .
image_name:(a)
description:The image consists of two parts: (a) and (b).

**(a) Monolithic Capacitor Structure:**
- **Components and Structure:** The diagram shows a cross-sectional view of a monolithic capacitor. It consists of a "Top Plate" labeled as 'A' and a "Bottom Plate" labeled as 'B'. These plates are realized using metal layers, specifically "Metal 9" for the top plate and "Metal 8" for the bottom plate. Between these two metal layers is a "Dielectric" material.
- **Connections and Interactions:** The bottom plate is connected to the substrate, and there is a parasitic capacitance, denoted as \(C_{p}\), between the bottom plate and the substrate. This parasitic capacitance is a significant concern as it can affect the performance of the capacitor.
- **Labels, Annotations, and Key Features:** The diagram highlights the materials used (metal layers and dielectric) and indicates the presence of parasitic capacitance \(C_{p}\).

**(b) Circuit Model Including Parasitic Capacitance:**
- **Components and Structure:** This part of the image represents the equivalent circuit model of the monolithic capacitor shown in (a). It includes the main capacitance \(C_{AB}\) between points X and Y and the parasitic capacitance \(C_{p}\) to the substrate.
- **Connections and Interactions:** The circuit model shows \(C_{AB}\) as the primary capacitance between the top and bottom plates. The parasitic capacitance \(C_{p}\) is connected from point X to the ground, representing the capacitance to the substrate.
- **Labels, Annotations, and Key Features:** The circuit diagram is labeled with the capacitances \(C_{AB}\) and \(C_{p}\), and points X and Y are marked to indicate the terminals of the main capacitance.
image_name:(b)
description:
[
name: C_P, type: Capacitor, value: C_P, ports: {Np: X, Nn: GND}
name: C_AB, type: Capacitor, value: C_AB, ports: {Np: X, Nn: Y}
]
extrainfo:The circuit model shows a monolithic capacitor with parasitic capacitance C_P to the substrate, and the main capacitance C_AB between nodes X and Y.

Figure 13.29 (a) Monolithic capacitor structure; (b) circuit model of (a) including parasitic capacitance to the substrate.

### 13.3.1 Unity-Gain Sampler/Buffer

While a unity-gain amplifier can be realized with no resistors or capacitors in the feedback network [Fig. 13.30(a)], for discrete-time applications, it still requires a sampling circuit. We may therefore conceive the circuit shown in Fig. 13.30(b) as a sampler/buffer. However, the input-dependent charge injected by $S_{1}$ onto $C_{H}$ limits the accuracy here.

Now consider the topology depicted in Fig. 13.31(a), where three switches control the sampling and amplification modes. In the sampling mode, $S_{1}$ and $S_{2}$ are on and $S_{3}$ is off, yielding the topology shown in Fig. 13.31(b). Thus, $V_{\text {out }}=V_{X} \approx 0$, and the voltage across $C_{H}$ tracks $V_{\text {in }}$. At $t=t_{0}$, when $V_{\text {in }}=V_{0}$,
image_name:Figure 13.30 (a) Unity-gain buffer
description:
[
name: Av, type: OpAmp, value: Av, ports: {InP: Vin, InN: Vout, OutP: Vout}
]
extrainfo:The circuit is a unity-gain buffer using an operational amplifier. The input voltage Vin is connected to the non-inverting input of the op-amp, and the output Vout is fed back to the inverting input, creating a unity gain configuration.

image_name:(b) sampling circuit followed by unity-gain buffer.
description:
[
name: S1, type: Switch, ports: {N1: Vin, N2: InP(Av)}
name: CH, type: Capacitor, value: CH, ports: {Np: InP(Av), Nn: GND}
name: Av, type: OpAmp, value: Av, ports: {InP: InP(Av), InN: Vout, OutP: Vout}
name: S1, type: Switch, ports: {N1: Vin, N2: Y}
name: S2, type: Switch, ports: {N1: X, N2: Vout}
name: S3, type: Switch, ports: {N1: Y, N2: Vout}
name: CH, type: Capacitor, value: CH, ports: {Np: Y, Nn: X}
name: Av, type: OpAmp, value: Av, ports: {InP: GND, InN: X, OutP: Vout}
]
extrainfo:The circuit is a unity-gain buffer with a sampling function. Switches S1, S2, and S3 control the mode of operation. The capacitor CH is used for sampling the input voltage. The operational amplifier Av is configured as a unity-gain buffer, providing an output Vout equal to the input voltage Vin when S1 is closed and S2 is open. When S2 is closed and S3 is open, the capacitor holds the sampled voltage.
image_name:(b)
description:
[
name: CH, type: Capacitor, value: CH, ports: {Np: Vin, Nn: X}
name: Av, type: OpAmp, value: Av, ports: {InP: GND, InN: X, OutP: X(Vout)}
]
extrainfo:The circuit is a sampling circuit followed by a unity-gain buffer. The capacitor CH samples the input voltage Vin when switch S1 is closed. The op-amp Av is configured as a unity-gain buffer, providing a stable output Vout that follows the sampled voltage.
image_name:(c)
description:
[
name: CH, type: Capacitor, value: CH, ports: {Np: Vout, Nn: X}
name: Av, type: OpAmp, value: Av, ports: {InP: X, InN: GND, OutP: Vout}
]
extrainfo:The circuit in (c) is in amplification mode. The capacitor CH is flipped around the op-amp, and the feedback loop is closed through the switch S3, allowing the op-amp to amplify the voltage across the capacitor.

Figure 13.31 (a) Unity-gain sampler; (b) circuit of (a) in sampling mode; (c) circuit of (a) in amplification mode.
$S_{1}$ and $S_{2}$ turn off and $S_{3}$ turns on, flipping the capacitor around the op amp and entering the circuit into the amplification mode [Fig. 13.31(c)]. Since the op amp's high gain requires that node $X$ still be a virtual ground and since the charge on the capacitor must be conserved, $V_{\text {out }}$ rises to a value approximately equal to $V_{0}$. This voltage is therefore "frozen," and it can be processed by subsequent stages.

With proper timing, the circuit of Fig. 13.31(a) can substantially alleviate the problem of channel charge injection. As Fig. 13.32 illustrates in "slow motion," during the transition from the sampling mode to the amplification mode, $S_{2}$ turns off slightly before $S_{1}$ does. We carefully examine the effect of the charge injected by $S_{2}$ and $S_{1}$. When $S_{2}$ turns off, it injects a charge packet $\Delta q_{2}$ onto $C_{H}$, producing an error equal to $\Delta q_{2} / C_{H}$. However, this charge is independent of the input level because node $X$ is a virtual ground. For example, if $S_{2}$ is realized by an NMOS device whose gate voltage equals $V_{C K}$, then $\Delta q_{2}=W L C_{o x}\left(V_{C K}-V_{T H}-V_{X}\right)$.
image_name:(a)
description:
[
name: S1, type: Switch, ports: {N1: Vin, N2: Y}
name: S2, type: Switch, ports: {N1: Vout, N2: X}
name: CH, type: Capacitor, value: CH, ports: {Np: Y, Nn: X}
name: Av, type: OpAmp, value: Av, ports: {InP: GND, InN: X, OutP: Vout}
]
extrainfo:The circuit is a unity-gain sampler with charge injection analysis. S1 is connected between Vin and node Y, S2 connects Vout and node X, and CH is connected between nodes Y and X. The op-amp is configured with its inverting input connected to node X and non-inverting input to ground, providing an output at Vout.
image_name:(b)
description:
[
name: S1, type: Switch, ports: {N1: Vin, N2: Y}
name: S2, type: Switch, ports: {N1: X, N2: Vout}
name: CH, type: Capacitor, value: CH, ports: {Np: Y, Nn: X}
name: Av, type: OpAmp, value: Av, ports: {InP: GND, InN: X, OutP: Vout}
]
extrainfo:The circuit is a unity-gain sampler with switches S1 and S2 controlling the sampling and holding phases. The charge injection from S2 introduces an offset error, which can be corrected by differential operation.
image_name:(c)
description:
[
name: S3, type: Switch, ports: {N1: Vout, N2: Y}
name: CH, type: Capacitor, value: CH, ports: {Np: Y, Nn: X}
name: Av, type: OpAmp, value: Av, ports: {InP: GND, InN: X, Out: Vout}
]
extrainfo:The circuit is a unity-gain sampler with a feedback loop involving the switch S3 and the op-amp Av. The capacitor CH is used to hold the sampled voltage. The op-amp is configured in a negative feedback loop to maintain the output voltage equal to the input voltage at node X.

Figure 13.32 Operation of the unity-gain sampler in slow motion.

The constant magnitude of $\Delta q_{2}$ means that the channel charge of $S_{2}$ introduces only an offset (rather than gain error or nonlinearity) in the input/output characteristic. As described below, this offset can easily be removed by differential operation. But, how about the charge injected by $S_{1}$ onto $C_{H}$ ? Let us set $V_{i n}$ to zero and suppose that $S_{1}$ injects a charge packet $\Delta q_{1}$ onto node $P$ (after $S_{2}$ has turned off) [Fig. 13.33(a)]. If the capacitance connected from $X$ to ground (including the input capacitance of the op amp) is zero, $V_{P}$ and $V_{X}$ jump to infinity. To simplify the analysis, we assume a capacitance equal to $C_{X}$ from $X$ to ground [Fig. 13.33(b)], and we will see shortly that its value does not affect the results. In
image_name:(a)
description:
[
name: S1, type: Switch, ports: {N1: Vin, N2: P}
name: CH, type: Capacitor, value: CH, ports: {Np: P, Nn: X}
name: Av, type: OpAmp, value: Av, ports: {InP: GND, InN: X, OutP: Vout}
name: CX, type: Capacitor, value: CX, ports: {Np: X, Nn: GND}
]
extrainfo:The circuit diagram (a) shows an op-amp configuration with a switch S1, capacitors CH and CX, and an op-amp Av. The switch S1 injects a charge packet Δq1 onto node P when closed. Capacitor CH is connected between nodes P and X, while capacitor CX is connected from node X to ground. The op-amp Av has its non-inverting input grounded and inverting input connected to node X, with the output at Vout.
image_name:(b)
description:
[
name: S1, type: Switch, ports: {N1: Vin, N2: P}
name: CH, type: Capacitor, value: CH, ports: {Np: P, Nn: X}
name: CX, type: Capacitor, value: CX, ports: {Np: X, Nn: GND}
name: Av, type: OpAmp, value: Av, ports: {InP: GND, InN: X, Out: Vout}
]
extrainfo:The circuit diagram (b) shows a configuration where a switch S1 injects charge \( \Delta q_1 \) onto node P. Capacitors CH and CX are connected in series with an op-amp Av. CX is connected to ground, stabilizing node X.
image_name:(c)
description:
[
name: CH, type: Capacitor, value: CH, ports: {Np: X, Nn: Vout}
name: CX, type: Capacitor, value: CX, ports: {Np: X, Nn: GND}
name: Av1, type: OpAmp, value: Av1, ports: {InP: GND, InN: X, OutP: Vout}
]
extrainfo:The circuit is a charge amplifier configuration with feedback capacitor CH and input capacitor CX. The switch S1 injects charge onto node P, which is then transferred to node X. The op-amp Av1 amplifies the voltage across CX, providing the output Vout.

Figure 13.33 Effect of charge injected by $S_{1}$ with (a) zero and (b) finite op amp input capacitance; (c) transition of circuit to amplification mode.

Fig. 13.33(b), each of the series capacitors $C_{H}$ and $C_{X}$ carries a charge equal to $\Delta q_{1}$. Now, as shown in Fig. 13.33(c), we place $C_{H}$ around the op amp, seeking to obtain the resulting output voltage.

To calculate the output voltage, we must make an important observation: the total charge at node $X$ cannot change after $S_{2}$ turns off because no path exists for electrons to flow into or out of this node. Thus, if before $S_{1}$ turns off, the total charge on the right plate of $C_{H}$ and the top plate of $C_{X}$ is zero, it must still add up to zero after $S_{1}$ injects charge because no resistive path is connected to $X$. The same holds true after $C_{H}$ is placed around the op amp.

Now consider the circuit of Fig. 13.33(c), assuming that the total charge at node $X$ is zero. We can write $C_{X} V_{X}-\left(V_{\text {out }}-V_{X}\right) C_{H}=0$, and $V_{X}=-V_{\text {out }} / A_{v 1}$. Thus, $-\left(C_{X}+C_{H}\right) V_{\text {out }} / A_{v 1}-V_{\text {out }} C_{H}=0$, i.e., $V_{\text {out }}=0$. Note that this result is independent of $\Delta q_{1}$, capacitor values, or the gain of the op amp, thereby revealing that the charge injection by $S_{1}$ introduces no error if $S_{2}$ turns off first.

In summary, in Fig. 13.31(a), after $S_{2}$ turns off, node $X$ "floats," maintaining a constant total charge regardless of the transitions at other nodes of the circuit. As a result, after the feedback configuration is formed, the output voltage is not influenced by the charge injection due to $S_{1}$. From another point of view, node $X$ is a virtual ground at the moment $S_{2}$ turns off, freezing the instantaneous input level across $C_{H}$ and yielding a charge equal to $V_{0} C_{H}$ on the left plate of $C_{H}$. After settling with feedback, node $X$ is again a virtual ground, forcing $C_{H}$ to still carry $V_{0} C_{H}$ and hence the output voltage to be approximately equal to $V_{0}$.

The effect of the charge injected by $S_{1}$ can be studied from yet another perspective. Suppose that in Fig. 13.33(c), the output voltage is finite and positive. Then, since $V_{X}=V_{\text {out }} /\left(-A_{v 1}\right), V_{X}$ must be finite and negative, requiring negative charge on the top plate of $C_{X}$. For the total charge at $X$ to be zero, the charge on the left plate of $C_{H}$ must be positive and that on its right plate negative, giving $V_{\text {out }} \leq 0$. Thus, the only valid solution is $V_{\text {out }}=0$.

The third switch in Fig. 13.31(a), $S_{3}$, also merits attention. In order to turn on, $S_{3}$ must establish an inversion layer at its oxide interface. Does the required channel charge come from $C_{H}$ or from the op amp? We note from the foregoing analysis that after the feedback circuit has settled, the charge on $C_{H}$ equals $V_{0} C_{H}$, unaffected by $S_{3}$. The channel charge of this switch is therefore entirely supplied by the op amp, introducing no error.

Our study of Fig. 13.31(a) thus far suggests that, with proper timing, the charge injected by $S_{1}$ and $S_{3}$ is unimportant and the channel charge of $S_{2}$ results in a constant offset voltage. Figure 13.34 depicts a simple realization of the clock edges to ensure that $S_{1}$ turns off after $S_{2}$ does.

The input-independent nature of the charge injected by the reset switch allows complete cancellation by differential operation. Illustrated in Fig. 13.35, such an approach employs a differential op amp along with two sampling capacitors so that the charge injected by $S_{2}$ and $S_{2}^{\prime}$ appears as a common-mode disturbance at nodes $X$ and $Y$. This is in contrast to the behavior of the differential circuit shown in Fig. 13.28, where the input-dependent charge injection still leads to nonlinearity. In reality, $S_{2}$ and $S_{2}^{\prime}$ exhibit a finite charge injection mismatch, an issue resolved by adding another switch, $S_{e q}$, that turns off slightly after $S_{2}$ and $S_{2}^{\prime}$ (and before $S_{1}$ and $S_{1}^{\prime}$ ), thereby equalizing the charge at nodes $X$ and $Y$.
image_name:Figure 13.34 Generation of proper clock edges for unity-gain sampler
description:The circuit is a unity-gain sampler with proper clock edge generation using three inverters. The switches S1, S2, and S3 control the sampling operation, with CH holding the charge. The OpAmp buffers the output to Vout.

Figure 13.34 Generation of proper clock edges for unity-gain sampler.
image_name:Figure 13.35 Differential realization of unity-gain sampler
description:
[
name: S1, type: Switch, ports: {N1: Vip, N2: X1}
name: "S1", type: Switch, ports: {N1: Vin, N2: Y1}
name: S2, type: Switch, ports: {N1: X, N2: Vout}
name: "S2", type: Switch, ports: {N1: Y, N2: Vout}
name: S3, type: Switch, ports: {N1: X1, N2: Voutn}
name: "S3", type: Switch, ports: {N1: Y1, N2: Voutp}
name: CH, type: Capacitor, value: CH, ports: {Np: X1, Nn: X}
name: CH, type: Capacitor, value: CH, ports: {Np: Y1, Nn: Y}
name: Seq, type: Switch, ports: {Np: X, Nn: Y}
name: Av, type: OpAmp, value: Av, ports: {InP: X, InN: Y, OutP: Voutp, OutN: Voutn'}
]
extrainfo:The circuit is a differential realization of a unity-gain sampler. It uses switches S1, S1', S2, S2', S3, and S3' to control the sampling operation. Capacitors CH and Seq are used for holding charge, and the OpAmp Av buffers the output to Vout. The circuit is designed for precision sampling and buffering of input signals.

Figure 13.35 Differential realization of unity-gain sampler.

Precision Considerations The circuit of Fig. 13.31(a) operates as a unity-gain buffer in the amplification mode, producing an output voltage approximately equal to the voltage stored across the capacitor. How close to unity is the gain here? As a general case, we assume that the op amp exhibits a finite input capacitance $C_{i n}$ and calculate the output voltage when the circuit goes from the sampling mode to the amplification mode (Fig. 13.36). Owing to the finite gain of the op amp, $V_{X} \neq 0$ in the amplification mode, giving a charge equal to $C_{i n} V_{X}$ on $C_{i n}$. The conservation of charge at $X$ requires that $C_{i n} V_{X}$ come from $C_{H}$, raising the charge on $C_{H}$ to $C_{H} V_{0}+C_{i n} V_{X} .{ }^{7}$ It follows that the voltage across $C_{H}$ equals $\left(C_{H} V_{0}+C_{\text {in }} V_{X}\right) / C_{H}$. We therefore write $V_{\text {out }}-\left(C_{H} V_{0}+C_{\text {in }} V_{X}\right) / C_{H}=V_{X}$ and $V_{X}=-V_{\text {out }} / A_{v 1}$. Thus,

$$
\begin{align*}
V_{\text {out }} & =\frac{V_{0}}{1+\frac{1}{A_{v 1}}\left(\frac{C_{\text {in }}}{C_{H}}+1\right)}  \tag{13.40}\\
& \approx V_{0}\left[1-\frac{1}{A_{v 1}}\left(\frac{C_{i n}}{C_{H}}+1\right)\right] \tag{13.41}
\end{align*}
$$

image_name:Figure 13.36 Equivalent circuit for accuracy calculations
description:
[
name: C_H, type: Capacitor, value: C_H, ports: {Np: Vin, Nn: X}
name: C_in, type: Capacitor, value: C_in, ports: {Np: X, Nn: GND}
name: A_v1, type: OpAmp, value: A_v1, ports: {InP: GND, InN: X, Out: X(Vout)}
]
extrainfo:The circuit is an equivalent circuit for accuracy calculations, involving capacitors C_H and C_in, and an operational amplifier A_v1. It is used to analyze the gain error and accuracy of the system.

Figure 13.36 Equivalent circuit for accuracy calculations.

[^97]As expected, if $C_{i n} / C_{H} \ll 1$, then $V_{\text {out }} \approx V_{0} /\left(1+A_{v 1}^{-1}\right)$. In general, however, the circuit suffers from a gain error of approximately $-\left(C_{i n} / C_{H}+1\right) / A_{v 1}$, suggesting that the input capacitance must be minimized even if speed is not critical. Recall from Chapter 9 that to increase $A_{v 1}$, we may choose a large width for the input transistors of the op amp, but at the cost of higher input capacitance. An optimum device size must therefore yield minimum gain error rather than maximum $A_{v 1}$.

#### Example 13.4

In the circuit of Fig. 13.36, $C_{i n}=0.5 \mathrm{pF}$ and $C_{H}=2 \mathrm{pF}$. What is the minimum op amp gain that guarantees a gain error of $0.1 \%$ ?

#### Solution

Since $C_{\text {in }} / C_{H}=0.25$, we have $A_{v 1, \text { min }}=1000 \times 1.25=1250$.

Speed Considerations Let us first examine the circuit in the sampling mode [Fig. 13.37(a)]. What is the time constant in this phase? The total resistance in series with $C_{H}$ is given by $R_{o n 1}$ and the resistance between $X$ and ground, $R_{X}$. Using the simple op amp model shown in Fig. 13.37(b), where $R_{0}$ denotes the open-loop output impedance of the op amp, we have

$$
\begin{equation*}
\left(I_{X}-G_{m} V_{X}\right) R_{0}+I_{X} R_{o n 2}=V_{X} \tag{13.42}
\end{equation*}
$$

that is

$$
\begin{equation*}
R_{X}=\frac{R_{0}+R_{\text {on } 2}}{1+G_{m} R_{0}} \tag{13.43}
\end{equation*}
$$

Since typically $R_{o n 2} \ll R_{0}$ and $G_{m} R_{0} \gg 1$, we have $R_{X} \approx 1 / G_{m}$. For example, in a telescopic op amp employing differential to single-ended conversion, $G_{m}$ equals the transconductance of each input transistor.
image_name:(a)
description:The circuit in Fig. 13.37(a) is a unity-gain sampler in sampling mode. It includes switches S1 and S2, a capacitor CH, and an operational amplifier AV. The equivalent circuit in Fig. 13.37(b) shows the relationship between the elements with voltage Vx and current Ix, including resistors Ron2 and R0, and a current-controlled current source GmVx.
image_name:(b)
description:The circuit diagram (b) represents an equivalent circuit for the unity-gain sampler in amplification mode. It includes a voltage source VX, a resistor Ron2, a current-controlled current source GmVx, and a resistor R0.

Figure $\mathbf{1 3 . 3 7}$ (a) Unity-gain sampler in sampling mode; (b) equivalent circuit of (a).
The time constant in the sampling mode is thus equal to

$$
\begin{equation*}
\tau_{s a m}=\left(R_{o n 1}+\frac{1}{G_{m}}\right) C_{H} \tag{13.44}
\end{equation*}
$$

The magnitude of $\tau_{\text {sam }}$ must be sufficiently small to allow settling in the test case of Fig. 13.15 to the required precision.

Now let us consider the circuit as it enters the amplification mode. Shown in Fig. 13.38 along with both the op amp input capacitance and the load capacitance, the circuit must begin with $V_{\text {out }} \approx 0$ and eventually produce $V_{\text {out }} \approx V_{0}$. If $C_{\text {in }}$ is relatively small, we can assume that the voltages across $C_{L}$ and
image_name:Figure 13.38
description:
[
name: CH, type: Capacitor, value: CH, ports: {Np: X, Nn: Vout}
name: Cin, type: Capacitor, value: Cin, ports: {Np: X, Nn: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
name: Av, type: OpAmp, value: Av, ports: {InP: GND, InN: X, Out: Vout}
]
extrainfo:The circuit is a unity-gain sampler in amplification mode. It uses an operational amplifier with capacitive feedback to achieve the desired output voltage.

image_name:Figure 13.38 Time response of unity-gain sampler in amplification mode
description:The graph titled "Figure 13.38 Time response of unity-gain sampler in amplification mode" is a time-domain waveform. It depicts the time response of a unity-gain sampler in amplification mode, focusing on the voltages $V_{X}$ and $V_{out}$.

**Axes Labels and Units:**
- The horizontal axis represents time, denoted as $t$, with an unspecified unit of measurement.
- The vertical axis represents voltage, with two key voltages indicated: $V_X$ and $V_{out}$. The voltage $V_X$ starts at 0 and $-V_0$, while $V_{out}$ starts at 0 and approaches $V_0$.

**Overall Behavior and Trends:**
- At time $t_0$, $V_X$ starts at 0 and jumps to $-V_0$, indicating an initial large input difference sensed by the operational amplifier.
- $V_{out}$ begins at 0 and gradually increases towards $V_0$, suggesting an exponential rise as the circuit transitions into amplification mode.
- Both $V_X$ and $V_{out}$ exhibit smooth, continuous curves without oscillations, indicating a stable transition.

**Key Features and Technical Details:**
- The graph shows a rapid transition at $t_0$, where $V_X$ instantaneously drops to $-V_0$.
- $V_{out}$ shows an exponential increase, typical of a charging capacitor in an RC circuit, as it asymptotically approaches $V_0$.

**Annotations and Specific Data Points:**
- The graph is marked with $t_0$ at the point of initial change, emphasizing the moment the op amp begins to amplify the input.
- The initial and final values of $V_X$ and $V_{out}$ are annotated as $-V_0$ and $V_0$, respectively, providing clear reference points for the voltage levels involved.

Figure 13.38 Time response of unity-gain sampler in amplification mode.
$C_{H}$ do not change instantaneously, concluding that if $V_{\text {out }} \approx 0$ and $V_{C H} \approx V_{0}$, then $V_{X}=-V_{0}$ at the beginning of the amplification mode. In other words, the input difference sensed by the op amp initially jumps to a large value, possibly causing the op amp to slew. But, let us first assume that the op amp can be modeled by a linear model and determine the output response.

To simplify the analysis, we represent the charge on $C_{H}$ by an explicit series voltage source, $V_{S}$, that goes from zero to $V_{0}$ at $t=t_{0}$ while $C_{H}$ carries no charge itself (Fig. 13.39). The objective is to obtain the transfer function $V_{\text {out }}(s) / V_{S}(s)$ and hence the step response. We have

$$
\begin{equation*}
V_{\text {out }}\left(\frac{1}{R_{0}}+C_{L} s\right)+G_{m} V_{X}=\left(V_{S}+V_{X}-V_{\text {out }}\right) C_{H} s \tag{13.45}
\end{equation*}
$$

image_name:Figure 13.39
description:
[
name: VS, type: VoltageSource, value: VS, ports: {Np: Vx+Vs, Nn: X}
name: CH, type: Capacitor, value: CH, ports: {Np: Vx+Vs, Nn: Vout}
name: Cin, type: Capacitor, value: Cin, ports: {Np: X, Nn: GND}
name: GmVx, type: VoltageControlledCurrentSource, value: GmVx, ports: {Np: Vout, Nn: GND}
name: R0, type: Resistor, value: R0, ports: {N1: Vout, N2: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a unity-gain amplifier in amplification mode, involving a voltage source, capacitors, a voltage-controlled current source, and a resistor. It is designed to analyze the transfer function Vout(s)/Vs(s) and the step response.

Figure 13.39 Equivalent circuit of unity-gain circuit in amplification mode.

Also, since the current through $C_{i n}$ equals $V_{X} C_{i n} s$,

$$
\begin{equation*}
V_{X} \frac{C_{i n} s}{C_{H} s}+V_{X}+V_{S}=V_{\text {out }} \tag{13.46}
\end{equation*}
$$

Calculating $V_{X}$ from (13.46) and substituting in (13.45), we arrive at the transfer function:

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{S}}(s)=R_{0} \frac{\left(G_{m}+C_{\text {in }} s\right) C_{H}}{R_{0}\left(C_{L} C_{\text {in }}+C_{\text {in }} C_{H}+C_{H} C_{L}\right) s+G_{m} R_{0} C_{H}+C_{H}+C_{\text {in }}} \tag{13.47}
\end{equation*}
$$

Note that for $s=0,(13.47)$ reduces to a form similar to (13.40). Since typically $G_{m} R_{0} C_{H} \gg C_{H}+C_{i n}$, we can simplify (13.47) as

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{S}}(s)=\frac{\left(G_{m}+C_{\text {in }} s\right) C_{H}}{\left(C_{L} C_{\text {in }}+C_{\text {in }} C_{H}+C_{H} C_{L}\right) s+G_{m} C_{H}} \tag{13.48}
\end{equation*}
$$

Thus, the response is characterized by a time constant equal to

$$
\begin{align*}
\tau_{a m p} & =\frac{C_{L} C_{i n}+C_{i n} C_{H}+C_{H} C_{L}}{G_{m} C_{H}}  \tag{13.49}\\
& =\frac{1}{G_{m}}\left[C_{i n}+\left(1+\frac{C_{i n}}{C_{H}}\right) C_{L}\right] \tag{13.50}
\end{align*}
$$

which is independent of the op amp output resistance. This is because a higher $R_{0}$ leads to a greater loop gain, eventually yielding a constant closed-loop speed. Another interesting interpretation of this result is described later (Fig. 13.52).

#### Example 13.5

Consider the special cases $C_{L}=0$ and $C_{i n}=0$ and explain the results intuitively.

#### Solution

If $C_{L}=0$, then $\tau=C_{i n} / G_{m}$. This occurs because the equivalent resistance seen by $C_{i n}$ is simply equal to $1 / G_{m}$ if $C_{L}=0$ [Fig. 13.40(a)].
image_name:(a)
description:
[
name: Cin, type: Capacitor, value: Cin, ports: {Np: InN(Ao), Nn: GND}
name: Ao, type: OpAmp, value: Ao, ports: {InP: GND, InN: InN(Ao), OutP: Out(Ao)}
name: CH, type: Capacitor, value: CH, ports: {Np: Out(Ao), Nn: InN(Ao)}
]
extrainfo:The circuit diagram (a) represents a configuration with a capacitor Cin connected to the inverting input of an operational amplifier Ao. A voltage-controlled current source with transconductance 1/Gm is also connected to this input. The capacitor CH is connected between the output and the inverting input of the op-amp. The non-inverting input of the op-amp is grounded.
image_name:(b)
description:
[
name: CH, type: Capacitor, value: CH, ports: {Np: Out(Ao), Nn: InN(Ao)}
name: Ao, type: OpAmp, value: Ao, ports: {InP: GND, InN: InN(Ao), OutP: Out(Ao)}
name: CL, type: Capacitor, value: CL, ports: {Np: Out(Ao), Nn: GND}
]
extrainfo:The circuit in diagram (b) represents a feedback loop with an operational amplifier Ao, where the output is fed back to the inverting input through capacitor CH. The load capacitance CL is connected to the output, and the current source 1/Gm provides feedback to maintain stability.

Figure 13.40
If $C_{i n}=0$, we have $\tau=C_{L} / G_{m}$ because $C_{L}$ now sees a driving resistance equal to $1 / G_{m}$ [Fig. 13.40(b)].

We now study the slewing behavior of the circuit, considering a telescopic op amp as an example. Upon entering the amplification mode, the circuit may experience a large step at the inverting input (Fig. 13.38). As shown in Fig. 13.41, the tail current of the op amp's input differential pair is then steered to one side, and its mirror current charges the capacitance seen at the output. Since $M_{2}$ is off during slewing, $C_{i n}$ is negligible and the slew rate is approximately equal to $I_{S S} / C_{L}$. The slewing continues until $V_{X}$ is sufficiently close to the gate voltage of $M_{1}$, after which point the settling progresses with the time constant given in (13.50).

Our foregoing studies reveal that the input capacitance of the op amp degrades both the speed and the precision of the unity-gain sampler/buffer. For this reason, the bottom plate of $C_{H}$ in Fig. 13.31 is usually driven by the input signal or the output of the op amp, and the top plate is connected to node $X$
image_name:Figure 13.41 Unity-gain sampler during slewing
description:
[
name: M7, type: PMOS, ports: {S: VDD, D: X1, G: X1}
name: M8, type: PMOS, ports: {S: VDD, D: s6d8, G: X1}
name: M5, type: PMOS, ports: {S: X1, D: Y, G: Y}
name: M6, type: PMOS, ports: {S: s6d8, D: Vout, G: Y}
name: M3, type: NMOS, ports: {S: d1s3, D: Y, G: Vb1}
name: M4, type: NMOS, ports: {S: d2s4, D: Vout, G: Vb1}
name: M1, type: NMOS, ports: {S: P, D: d1s3, G: Vb}
name: M2, type: NMOS, ports: {S: P, D: d2s4, G: X}
name: CH, type: Capacitor, value: CH, ports: {Np: Vout, Nn: X}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: VDD, Nn: P}
]
extrainfo:The circuit is a unity-gain sampler during slewing, involving PMOS and NMOS transistors, capacitors, and a current source. It is designed to minimize parasitic capacitance and avoid substrate noise injection through bottom-plate sampling.

Figure 13.41 Unity-gain sampler during slewing.
image_name:Figure 13.42 Connection of capacitor to the unity-gain sampler.
description:
[
name: S1, type: Switch, ports: {N1: Vin, N2: Y}
name: S2, type: Switch, ports: {N1: X, N2: Vout}
name: S3, type: Switch, ports: {N1: Y, N2: Vout}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: X, Out: Vout}
]
extrainfo:The circuit is a unity-gain sampler during slewing, involving switches and an operational amplifier. It is designed to minimize parasitic capacitance and avoid substrate noise injection through bottom-plate sampling. The capacitor is connected between nodes Y and X.

Figure 13.42 Connection of capacitor to the unity-gain sampler.
(Fig. 13.42), minimizing the parasitic capacitance seen from node $X$ to ground. This technique is called "bottom-plate sampling." Driving the bottom plate by the input or the output also avoids the injection of substrate noise to node $X$ (Chapter 19).

It is instructive to compare the performance of the sampling circuits shown in Figs. 13.30(b) and 13.31(a). In Fig. 13.30(b), the sampling time constant is smaller because it depends on only the onresistance of the switch. More important, in Fig. 13.30(b), the amplification after the switch turns off is almost instantaneous, whereas in Fig. 13.31, it requires a finite settling time. However, the critical advantage of the unity-gain sampler is the input-independent charge injection.

### 13.3.2 Noninverting Amplifier

In this section, we revisit the amplifier of Fig. 13.5, studying its speed and precision properties. Repeated in Fig. 13.43(a), the amplifier operates as follows. In the sampling mode, $S_{1}$ and $S_{2}$ are on and $S_{3}$ is off, creating a virtual ground at $X$ and allowing the voltage across $C_{1}$ to track the input voltage [Fig. 13.43(b)]. At the end of the sampling mode, $S_{2}$ turns off first, injecting a constant charge, $\Delta q_{2}$, onto node $X$. Subsequently, $S_{1}$ turns off and $S_{3}$ turns on [Fig. 13.43(c)]. Since $V_{P}$ goes from $V_{i n 0}$ to 0 , the output voltage changes from 0 to approximately $V_{i n 0}\left(C_{1} / C_{2}\right)$, providing a voltage gain equal to $C_{1} / C_{2}$. We call the circuit a "noninverting amplifier" because the final output has the same polarity as $V_{i n 0}$ and the gain can be greater than unity.
image_name:(a)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Y, Nn: X}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Vout}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: X, OutP: Vout}
name: S1, type: Switch, ports: {N1: Vin, N2: X}
name: S2, type: Switch, ports: {N1: X, N2: Vout}
name: S3, type: Switch, ports: {N1: Y, N2: GND}
]
extrainfo:The circuit is a noninverting amplifier using an operational amplifier and capacitors C1 and C2. It operates in two modes: sampling and amplification. In sampling mode, S2 is off, and charge is stored on C1. In amplification mode, S2 turns on, and the voltage at Vout is amplified by a factor of C1/C2.
image_name:(b)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: P, Nn: X}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: X, Out: Vout}
]
extrainfo:The circuit diagram (b) is a noninverting amplifier in sampling mode. The input voltage Vin is applied through switch S1 to capacitor C1, which is connected to the inverting input of the op-amp A0. The output voltage Vout is taken across capacitor C2. Switch S2 connects node X to Vout, and switch S3 grounds node P when closed. The op-amp provides feedback from the output to the input, stabilizing the gain.
image_name:(c)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: P, Nn: X}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Vout}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: X, OutP: Vout}
]
extrainfo:The circuit is a noninverting amplifier with a voltage gain of C1/C2. In the amplification mode, the circuit transitions with S1 turning off and S3 turning on, causing the output voltage to change from 0 to approximately Vin0(C1/C2). The amplifier avoids input-dependent charge injection by turning S2 off before S1.
image_name:(c)
description:The diagram illustrates a noninverting amplifier circuit in three stages: (a) the basic configuration, (b) the circuit in sampling mode, and (c) the transition to amplification mode with a graphical representation of the output voltage over time.

1. **Type of Graph and Function:**
- The graph in part (c) is a time-domain waveform showing the output voltage of the amplifier as it transitions from sampling to amplification mode.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as time \( t \). The units are not specified but typically would be in seconds or milliseconds.
- The vertical axis represents the output voltage \( V_{out} \), which is a function of the input voltage \( V_{in0} \).

3. **Overall Behavior and Trends:**
- The graph in part (c) shows a curve starting from zero and rising to a final value of \( \frac{C_1}{C_2} V_{in0} \). This indicates an exponential or step response characteristic as the circuit transitions to amplification mode.
- The output voltage increases from 0 to \( \frac{C_1}{C_2} V_{in0} \), suggesting a gain equal to \( \frac{C_1}{C_2} \).

4. **Key Features and Technical Details:**
- The circuit in (a) consists of an operational amplifier \( A_0 \) with capacitors \( C_1 \) and \( C_2 \), and switches \( S_1 \), \( S_2 \), and \( S_3 \).
- In (b), the switch \( S_2 \) is open, and \( S_1 \) is closed, allowing the circuit to sample the input voltage \( V_{in} \).
- In (c), \( S_2 \) turns off first, injecting a constant charge onto node \( X \), then \( S_1 \) turns off, and \( S_3 \) turns on, transitioning the circuit to amplification mode.
- The gain of the amplifier is determined by the ratio of \( C_1 \) to \( C_2 \), and the output voltage reaches \( \frac{C_1}{C_2} V_{in0} \) as shown in the graph.

5. **Annotations and Specific Data Points:**
- The graph in (c) is annotated with the final output voltage value \( \frac{C_1}{C_2} V_{in0} \), indicating the gain achieved by the circuit.
- The transition is smooth, indicating a stable amplification process.

This diagram effectively demonstrates the operation of a noninverting amplifier, highlighting the importance of switch timing and capacitor ratios in achieving the desired voltage gain.

Figure 13.43 (a) Noninverting amplifier; (b) circuit of (a) in sampling mode; (c) transition of circuit to amplification mode.

As with the unity-gain circuit of Fig. 13.31(a), the noninverting amplifier avoids input-dependent charge injection by proper timing, namely, turning $S_{2}$ off before $S_{1}$ (Fig. 13.44). After $S_{2}$ is off, the total charge at node $X$ remains constant, making the circuit insensitive to charge injection of $S_{1}$ or charge "absorption" of $S_{3}$. Let us first study the effect of $S_{1}$ carefully. As illustrated in Fig. 13.45, the charge injected by $S_{1}, \Delta q_{1}$, changes the voltage at node $P$ by approximately $\Delta V_{P}=\Delta q_{1} / C_{1}$, and hence the output voltage by $-\Delta q_{1} C_{1} / C_{2}$. However, after $S_{3}$ turns on, $V_{P}$ drops to zero. Thus, the overall change in $V_{P}$ is equal to $0-V_{i n 0}=-V_{i n 0}$, producing an overall change in the output equal to $-V_{\text {in0 }}\left(-C_{1} / C_{2}\right)=V_{\text {in } 0} C_{1} / C_{2}$.
image_name:Figure 13.44
description:
[
name: S1, type: Switch, ports: {N1: Vin, N2: P}
name: S2, type: Switch, ports: {N1: X, N2: Vout}
name: C1, type: Capacitor, value: C1, ports: {Np: P, Nn: X}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Vout}
name: Ao, type: OpAmp, value: Ao, ports: {InP: GND, InN: X, OutP: Vout, OutN: GND}
]
extrainfo:This is a non-inverting amplifier circuit with charge injection effects. The switches S1 and S2 control the charge flow and the capacitors C1 and C2 determine the amplification factor. The op-amp is used to stabilize the output voltage.

Figure 13.44 Transition of noninverting amplifier to amplification mode.
image_name:Figure 13.45
description:
[
name: S1, type: Switch, ports: {N1: Vin, N2: P}
name: S3, type: Switch, ports: {N1: P, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: P, Nn: X}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Vout}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: X, OutP: Vout, OutN: GND}
]
extrainfo:This is a non-inverting amplifier circuit with charge injection effects. The switches S1 and S3 control the charge flow and the capacitors C1 and C2 determine the amplification factor. The op-amp is used to stabilize the output voltage. The diagram illustrates the transition of the non-inverting amplifier to amplification mode and the effect of charge injected by S1.
image_name:Figure 13.45
description:The graph in Figure 13.45 consists of two time-domain waveforms depicting the effect of charge injection by switch $S_1$ on a non-inverting amplifier circuit.

1. **Type of Graph and Function**:
- The graph is a time-domain waveform showing voltage changes over time.

2. **Axes Labels and Units**:
- The horizontal axis represents time ($t$).
- The vertical axes represent voltage levels.
- The top graph shows the voltage at point $V_P$ and the bottom graph shows the output voltage $V_{out}$.

3. **Overall Behavior and Trends**:
- **Top Graph ($V_P$ vs. $t$):**
- Initially, $V_P$ is at a fixed voltage $V_{in0}$.
- When switch $S_1$ turns off, there is a small perturbation, indicated by a drop in voltage $\Delta V_P$.
- After the perturbation, the voltage $V_P$ stabilizes at a lower level.
- When switch $S_3$ turns on, $V_P$ drops to zero.
- **Bottom Graph ($V_{out}$ vs. $t$):**
- The output voltage $V_{out}$ starts at zero.
- As time progresses, it rises smoothly and stabilizes at a level proportional to $\frac{C_1}{C_2} V_{in0}$.

4. **Key Features and Technical Details**:
- The perturbation in $V_P$ due to $S_1$ is temporary and does not affect the final output voltage $V_{out}$.
- The final output voltage is determined by the ratio of capacitors $C_1$ and $C_2$ and the initial input voltage $V_{in0}$.

5. **Annotations and Specific Data Points**:
- The top graph is annotated with the points where $S_1$ turns off and $S_3$ turns on, highlighting the changes in $V_P$.
- The bottom graph shows the final stabilized output voltage $V_{out}$ as $\frac{C_1}{C_2} V_{in0}$.

Figure 13.45 Effect of charge injected by $S_{1}$.
The key point here is that $V_{P}$ goes from one fixed voltage, $V_{0}$, to another, 0 , with an intermediate perturbation due to $S_{1}$. Since the output voltage of interest is measured after node $P$ is connected to ground, the charge injected by $S_{1}$ does not affect the final output. From another perspective, as shown in Fig. 13.46, the charge on the right plate of $C_{1}$ at the instant $S_{2}$ turns off is approximately equal

image_name:Figure 13.46 Charge redistribution in noninverting amplifier
description:
[
name: S1, type: Switch, ports: {N1: Vin, N2: P}
name: S2, type: Switch, ports: {N1: X, N2: Vout}
name: C1, type: Capacitor, value: C1, ports: {Np: P, Nn: X}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Vout}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: X, OutP: Vout, OutN: GND}
]
extrainfo:The circuit is a noninverting amplifier with charge redistribution. When S2 is off, the charge on C1 is redistributed to C2, resulting in an output voltage approximately equal to Vin0*C1/C2.

Figure 13.46 Charge redistribution in noninverting amplifier.

to $-V_{i n 0} C_{1}$. Also, the total charge at node $X$ must remain constant after $S_{2}$ turns off. Thus, when node $P$ is connected to ground and the circuit settles, the voltage across $C_{1}$, and hence its charge, are nearly zero, and the charge $-V_{i n 0} C_{1}$ must reside on the left plate of $C_{2}$. In other words, the output voltage is approximately equal to $V_{i n 0} C_{1} / C_{2}$ regardless of the intermediate excursions at node $P$.

The foregoing discussion indicates that two other phenomena have no effect on the final output. First, from the time $S_{2}$ turns off until the time $S_{1}$ turns off, the input voltage may change significantly (Fig. 13.47) without introducing any error. In other words, the sampling instant is defined by the turn-off of $S_{2}$. Second, when $S_{3}$ turns on, it requires some channel charge, but since the final value of $V_{P}$ is zero, this charge is unimportant. Neither of these effects introduces error because the total charge at node $X$ is conserved and $V_{P}$ is eventually set by a fixed (zero) potential. To emphasize that $V_{P}$ is initially and finally determined by fixed voltages, we say that node $P$ is "driven" or node $P$ switches from a low-impedance node to another low-impedance node. Here the term low-impedance distinguishes node $P$, at which charge is not conserved, from "floating" nodes such as $X$, where charge is conserved.

image_name:Figure 13.47 Effect of input change after S2 turns off
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: S1, type: Switch, ports: {N1: Vin, N2: P}
name: S2, type: Switch, ports: {N1: X, N2: Vout}
name: S3, type: Switch, ports: {N1: P, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: P, Nn: X}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Vout}
name: Ao, type: OpAmp, value: Ao, ports: {InP: GND, InN: X, Out: Vout}
]
extrainfo:The circuit is a switched-capacitor integrator with differential operation to suppress offset due to charge injection. Proper timing ensures node X is only perturbed by S2's charge injection.

Figure 13.47 Effect of input change after $S_{2}$ turns off.
In summary, proper timing in Fig. 13.43(a) ensures that node $X$ is perturbed only by the charge injection of $S_{2}$, making the final value of $V_{\text {out }}$ free from errors due to $S_{1}$ and $S_{3}$. The constant offset due to $S_{2}$ can be suppressed by differential operation (Fig. 13.48).
image_name:Figure 13.48
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: X1, Nn: X}
name: C1, type: Capacitor, value: C1, ports: {Np: Y1, Nn: Y}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Voutn}
name: C2, type: Capacitor, value: C2, ports: {Np: Y, Nn: Voutp}
name: S1, type: Switch, ports: {N1: Vip, N2: X1}
name: "S1", type: Switch, ports: {N1: "Vin", N2: Y1}
name: S2, type: Switch, ports: {N1: Voutn, N2: X}
name: "S2", type: Switch, ports: {N1: Voutp, N2: Y}
name: S3, type: Switch, ports: {N1: Voutn, N2: X1}
name: "S3", type: Switch, ports: {N1: Voutp, N2: Y1}
name: A0, type: OpAmp, value: A0, ports: {InP: Y, InN: X, OutP: Voutp, OutN: Voutn}
]
extrainfo:The circuit is a differential noninverting amplifier with capacitive feedback and switches for controlling the input and output paths. It uses an operational amplifier (A0) to amplify the difference between two input signals (Vin and Vin') and provides differential outputs (Voutp and Voutn). The switches (S1, S1', S2, S2', S3, S3') are used to control signal paths and charge injection management.

Figure 13.48 Differential realization of noninverting amplifier.

#### Example 13.6

In the differential circuit of Fig. 13.48, suppose the equalizing switch is not used and $S_{2}$ and $S_{2}^{\prime}$ exhibit a threshold voltage mismatch of 10 mV . If $C_{1}=1 \mathrm{pF}, C_{2}=0.5 \mathrm{pF}, V_{T H}=0.6 \mathrm{~V}$, and for all switches $W L C_{o x}=50 \mathrm{fF}$,
calculate the dc offset measured at the output assuming that all of the channel charge of $S_{2}$ and $S_{2}^{\prime}$ is injected onto $X$ and $Y$, respectively.

#### Solution

Simplifying the circuit as in Fig. 13.49, we have $V_{\text {out }} \approx \Delta q / C_{2}$, where $\Delta q=W L C_{\text {ox }} \Delta V_{T H}$. Note that $C_{1}$ does not appear in the result because $X$ is a virtual ground, i.e., the voltage across $C_{1}$ changes only negligibly. Thus, the injected charge resides primarily on the left plate of $C_{2}$, giving an output error voltage equal to $\Delta V_{\text {out }}=$ $W L C_{o x} \Delta V_{T H} / C_{2}=1 \mathrm{mV}$.
image_name:Figure 13.49
description:
[
name: S1, type: Switch, ports: {N1: Vip, N2: X1}
name: "S1", type: Switch, ports: {N1: Vin, N2: Y1}
name: S2, type: Switch, ports: {N1: X, N2: Voutp}
name: "S2", type: Switch, ports: {N1: Y, N2: Vout}
name: C1, type: Capacitor, value: C1, ports: {Np: X1, Nn: X}
name: C1, type: Capacitor, value: C1, ports: {Np: Y1, Nn: Y}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Voutn}
name: C2, type: Capacitor, value: C2, ports: {Np: Y, Nn: Voutp}
name: Ao, type: OpAmp, value: Ao, ports: {InP: X, InN: Y, OutP: Voutp, OutN: Voutn}
]
extrainfo:The circuit is a charge amplifier with a differential output using an operational amplifier Ao, two capacitors C1 and C2, and switches for controlling input and output connections. The circuit is designed to amplify the input voltage Vin with a gain determined by the capacitors.

Precision Considerations As mentioned above, the circuit of Fig. 13.43(a) provides a nominal voltage gain of $C_{1} / C_{2}$. We now calculate the actual gain if the op amp exhibits a finite open-loop gain equal to $A_{v 1}$. Depicted in Fig. 13.50 along with the input capacitance of the op amp, the circuit amplifies the input voltage change such that

$$
\begin{equation*}
\left(V_{\text {out }}-V_{X}\right) C_{2} s=V_{X} C_{\text {in }} s+\left(V_{X}-V_{\text {in }}\right) C_{1} s \tag{13.51}
\end{equation*}
$$

Since $V_{\text {out }}=-A_{v 1} V_{X}$, we have

$$
\begin{equation*}
\left|\frac{V_{\text {out }}}{V_{\text {in }}}\right|=\frac{C_{1}}{C_{2}+\frac{C_{2}+C_{1}+C_{\text {in }}}{A_{v 1}}} \tag{13.52}
\end{equation*}
$$

For large $A_{v 1}$,

$$
\begin{equation*}
\left|\frac{V_{\text {out }}}{V_{\text {in }}}\right| \approx \frac{C_{1}}{C_{2}}\left(1-\frac{C_{2}+C_{1}+C_{\text {in }}}{C_{2}} \cdot \frac{1}{A_{v 1}}\right) \tag{13.53}
\end{equation*}
$$

implying that the amplifier suffers from a gain error of $\left(C_{2}+C_{1}+C_{i n}\right) /\left(C_{2} A_{v 1}\right)$. Note that the gain error increases with the nominal gain $C_{1} / C_{2}$.
image_name:Figure 13.50 Equivalent circuit of noninverting amplifier during amplification
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: X}
name: Cin, type: Capacitor, value: Cin, ports: {Np: X, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Vout}
name: Av1, type: OpAmp, value: Av1, ports: {InP: GND, InN: X, Out: Vout}
]
extrainfo:The circuit is a noninverting amplifier with capacitive feedback. It includes capacitors C1, Cin, and C2, and an operational amplifier Av1. The node labeled X is the inverting input of the op-amp, and the output is fed back through C2 to this node, creating a feedback loop. The input voltage is applied across C1.

Figure 13.50 Equivalent circuit of noninverting amplifier during amplification.

Comparing (13.41) with (13.53), we note that with $C_{H}=C_{2}$ and for a nominal gain of unity, the noninverting amplifier exhibits greater gain error than does the unity-gain sampler. This is because the feedback factor equals $C_{2} /\left(C_{1}+C_{i n}+C_{2}\right)$ in the former and $C_{H} /\left(C_{H}+C_{i n}\right)$ in the latter. For example, if $C_{i n}$ is negligible, the unity-gain sampler's gain error is half that of the noninverting amplifier.

Speed Considerations The smaller feedback factor in Fig. 13.50 suggests that the time response of the amplifier may be slower than that of the unity-gain sampler. This is indeed true. Consider the equivalent circuit shown in Fig. 13.51(a). Since the only difference between this circuit and that in Fig. 13.39 is the capacitor $C_{1}$, which is connected from node $X$ to an ideal voltage source, we expect that (13.50) gives the time constant of this amplifier as well if $C_{i n}$ is replaced by $C_{i n}+C_{1}$. But for a more rigorous analysis, we substitute $V_{i n}, C_{1}$, and $C_{i n}$ in Fig. 13.51(a) with a Thevenin equivalent as in Fig. 13.51(b), where $\alpha=C_{1} /\left(C_{1}+C_{i n}\right)$, and $C_{e q}=C_{1}+C_{i n}$ and note that

$$
\begin{equation*}
V_{X}=\left(\alpha V_{\text {in }}-V_{\text {out }}\right) \frac{C_{e q}}{C_{e q}+C_{2}}+V_{\text {out }} \tag{13.54}
\end{equation*}
$$

image_name:Figure 13.51 (a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Cin, type: Capacitor, value: Cin, ports: {Np: X, Nn: GND}
name: C1, type: Capacitor, ports: {Np: Vin, Nn: X}
name: C2, type: Capacitor, ports: {Np: X, Nn: Vout}
name: GmVx, type: VoltageControlledCurrentSource, ports: {Np: Vout, Nn: GND}
name: R0, type: Resistor, value: R0, ports: {N1: Vout, N2: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a noninverting amplifier with a Thevenin equivalent input. It includes a voltage source, capacitors, a voltage-controlled current source, and a resistor. The circuit topology suggests a focus on frequency response and stability.

image_name:Figure 13.51 (b)
description:
[
name: αVin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: Ceq, type: Capacitor, value: Ceq, ports: {Np: Vin, Nn: X}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Vout}
name: GmVx, type: VoltageControlledCurrentSource, ports: {Np: Vout, Nn: GND}
name: R0, type: Resistor, value: R0, ports: {N1: Vout, N2: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a noninverting amplifier with a Thevenin equivalent input. It includes a voltage source, capacitors, a voltage-controlled current source, and a resistor, focusing on frequency response and stability.

Figure 13.51 (a) Equivalent circuit of noninverting amplifier in amplification mode; (b) circuit of (a) with $V_{i n}, C_{1}$, and $C_{\text {in }}$ replaced by a Thevenin equivalent.

Thus,

$$
\begin{equation*}
\left[\left(\alpha V_{\text {in }}-V_{\text {out }}\right) \frac{C_{e q}}{C_{e q}+C_{2}}+V_{\text {out }}\right] G_{m}+V_{\text {out }}\left(\frac{1}{R_{0}}+C_{L} s\right)=\left(\alpha V_{\text {in }}-V_{\text {out }} \frac{C_{e q} C_{2}}{C_{e q}+C_{2}} s\right. \tag{13.55}
\end{equation*}
$$

and hence

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}(s)=\frac{-C_{e q} \frac{C_{1}}{C_{1}+C_{\text {in }}}\left(G_{m}-C_{2} s\right) R_{0}}{C_{2} G_{m} R_{0}+C_{e q}+C_{2}+R_{0}\left[C_{L}\left(C_{e q}+C_{2}\right)+C_{e q} C_{2}\right] s} \tag{13.56}
\end{equation*}
$$

Note that for $s=0,(13.56)$ reduces to (13.52). For a large $G_{m} R_{0}$, we can simplify (13.56) to

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}(s) \approx \frac{-C_{e q} \frac{C_{1}}{C_{1}+C_{\text {in }}}\left(G_{m}-C_{2} s\right) R_{0}}{R_{0}\left(C_{L} C_{e q}+C_{L} C_{2}+C_{e q} C_{2}\right) s+G_{m} R_{0} C_{2}} \tag{13.57}
\end{equation*}
$$

obtaining a time constant of

$$
\begin{equation*}
\tau_{a m p}=\frac{C_{L} C_{e q}+C_{L} C_{2}+C_{e q} C_{2}}{G_{m} C_{2}} \tag{13.58}
\end{equation*}
$$

which is the same as the time constant of Fig. 13.38 if $C_{i n}$ is replaced by $C_{i n}+C_{1}$. Note the direct dependence of $\tau_{\text {amp }}$ upon the nominal gain, $C_{1} / C_{2}$.

This expression can be rewritten as

$$
\begin{equation*}
\tau=\frac{C_{1}+C_{2}+C_{i n}}{C_{2}} \cdot \frac{C_{L}+\frac{C_{2}\left(C_{i n}+C_{1}\right)}{C_{2}+C_{i n}+C_{1}}}{G_{m}} \tag{13.59}
\end{equation*}
$$

yielding interesting insights: the time constant is given by an equivalent capacitance, $C_{L}+C_{2}\left(C_{i n}+\right.$ $\left.C_{1}\right) /\left(C_{2}+C_{i n}+C_{1}\right)$, and an equivalent resistance, $\left(C_{1}+C_{2}+C_{i n}\right) /\left(G_{m} C_{2}\right)$ (Fig. 13.52). We can roughly say that the op amp sees the series combination of $C_{2}$ and $C_{1}+C_{i n}$ in parallel with $C_{L}$, and its $G_{m}$ is reduced by the feedback factor, $C_{2} /\left(C_{1}+C_{2}+C_{\text {in }}\right)$.
image_name:Figure 13.52
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: X}
name: Cin, type: Capacitor, value: Cin, ports: {Np: X, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Vout}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
name: Gm, type: OpAmp, value: Gm, ports: {InP: GND, InN: X, OutP: Vout}
]
extrainfo:The circuit diagram shows an equivalent circuit with capacitors C1, Cin, C2, and CL in a feedback configuration with an operational amplifier Gm. The time constant is determined by an equivalent capacitance and resistance. The diagram illustrates how the op amp sees the series combination of C2 and C1+Cin in parallel with CL, with Gm reduced by the feedback factor.

Figure 13.52 Equivalent circuit showing settling time constant.
It is instructive to examine the amplifier's time constant for the special case $C_{L}=0$. Equation (13.58) yields $\tau_{\text {amp }}=\left(C_{1}+C_{i n}\right) / G_{m}$, a value independent of the feedback capacitor. This is because, while a larger $C_{2}$ introduces heavier loading at the output, it also provides a greater feedback factor.

The reader may wonder why Eq. (13.56) yields a negative gain for the circuit that we have called a "noninverting" amplifier. This equation simply means that if the left plate of $C_{1}$ is stepped down, then the output goes $u p$. This does not contradict the operation of the original circuit (Fig. 13.43), where the change in $V_{P}$ is equal to $-V_{i n}$.

## 13.4 Switched-Capacitor Integrator

Integrators are used in many analog systems. Examples include filters and oversampled analog-to-digital converters. Figure 13.55 depicts a continuous-time integrator, whose output can be expressed as

$$
\begin{equation*}
V_{\text {out }}=-\frac{1}{R C_{F}} \int V_{\text {in }} d t \tag{13.60}
\end{equation*}
$$

if the op amp gain is very large. For sampled-data systems, we must devise a discrete-time counterpart of this circuit.

Before studying SC integrators, let us first point out an interesting property. Consider a resistor connected between two nodes [Fig. 13.56(a)], carrying a current equal to $\left(V_{A}-V_{B}\right) / R$. The role of the resistor is to take a certain amount of charge from node $A$ every second and move it to node $B$. Can we

image_name:Figure 13.55 Continuous-time integrator
description:
[
name: R, type: Resistor, value: R, ports: {N1: Vin, N2: X}
name: CF, type: Capacitor, value: CF, ports: {Np: Vout, Nn: X}
name: A0, type: OpAmp, value: A0, ports: {InP: Gnd, InN: X, Out: Vout}
]
extrainfo:This is a continuous-time integrator circuit using an operational amplifier with feedback through a capacitor CF and input through a resistor R. The input voltage is Vin, and the output voltage is Vout.

image_name:(a)
description:
[
name: R, type: Resistor, value: R, ports: {N1: A, N2: B}
name: VA, type: VoltageSource, value: VA, ports: {Np: A, Nn: GND}
name: VB, type: VoltageSource, value: VB, ports: {Np: B, Nn: GND}
]
extrainfo:This is a simple resistive circuit with two voltage sources, VA and VB, connected to a resistor R. The current I flows from node A to node B through the resistor R.

image_name:(b)
description:
[
name: VA, type: VoltageSource, value: VA, ports: {Np: A, Nn: GND}
name: VB, type: VoltageSource, value: VB, ports: {Np: B, Nn: GND}
name: S1, type: Switch, ports: {N1: A, N2: X}
name: S2, type: Switch, ports: {N1: X, N2: B}
name: CS, type: Capacitor, value: CS, ports: {Np: X, Nn: GND}
]
extrainfo:This circuit consists of two voltage sources VA and VB, a capacitor CS, and two switches S1 and S2. The switches alternately connect the capacitor to nodes A and B, enabling charge transfer between the nodes.

Figure 13.56 (a) Continuous-time and (b) discrete-time resistors.
perform the same function with a capacitor? Suppose that in the circuit of Fig. 13.56(b), capacitor $C_{S}$ is alternately connected to nodes $A$ and $B$ at a clock rate $f_{C K}$. The average current flowing from $A$ to $B$ is then equal to the charge moved in one clock period:

$$
\begin{align*}
\overline{I_{A B}} & =\frac{C_{S}\left(V_{A}-V_{B}\right)}{f_{C K}^{-1}}  \tag{13.61}\\
& =C_{S} f_{C K}\left(V_{A}-V_{B}\right) \tag{13.62}
\end{align*}
$$

We can therefore view the circuit as a "resistor" equal to $\left(C_{S} f_{C K}\right)^{-1}$. Recognized by James Clark Maxwell, this property formed the foundation for many modern switched-capacitor circuits.

Let us now replace resistor $R$ in Fig. 13.55 by its discrete-time equivalent, arriving at the integrator of Fig. 13.57(a). We note that in every clock cycle, $C_{1}$ absorbs a charge equal to $C_{1} V_{i n}$ when $S_{1}$ is on and deposits the charge on $C_{2}$ when $S_{2}$ is on (node $X$ is a virtual ground). For example, if $V_{i n}$ is constant, the output changes by $V_{i n} C_{1} / C_{2}$ every clock cycle [Fig. 13.57(b)]. Approximating the staircase waveform by a ramp, we note that the circuit behaves as an integrator.
image_name:(a)
description:
[
name: S1, type: Switch, ports: {N1: Vin, N2: P}
name: S2, type: Switch, ports: {N1: P, N2: X}
name: C1, type: Capacitor, value: C1, ports: {Np: P, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Vout}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: X, Out: Vout}
]
extrainfo:This circuit is a discrete-time integrator. The capacitor C1 absorbs charge when switch S1 is on and transfers it to C2 when S2 is on. The op-amp A0 ensures that node X is a virtual ground, resulting in the integration of the input voltage Vin over time. The output voltage Vout changes by an amount proportional to Vin*C1/C2 each clock cycle.
image_name:(b)
description:The graph in Figure 13.57(b) is a time-domain waveform representing the output voltage \( V_{out} \) of a discrete-time integrator circuit in response to a constant input voltage \( V_{in} \).

1. **Type of Graph and Function:**
- This is a time-domain waveform showing a staircase function.

2. **Axes Labels and Units:**
- The horizontal axis represents time \( t \), though specific units are not given, it is typically in seconds or milliseconds for integrator circuits.
- The vertical axis represents the output voltage \( V_{out} \) in volts.

3. **Overall Behavior and Trends:**
- The graph shows a staircase-like waveform, where the output voltage decreases in discrete steps over time.
- Each step corresponds to a clock cycle of the integrator circuit.

4. **Key Features and Technical Details:**
- The magnitude of each step is given by \( \frac{C_{1}}{C_{2}} V_{in} \), indicating that the output voltage decreases by this amount every clock cycle.
- The waveform approximates a ramp when viewed over a longer period, reflecting the integrative behavior of the circuit.

5. **Annotations and Specific Data Points:**
- There is an annotation showing the step size \( \frac{C_{1}}{C_{2}} V_{in} \) between each level of the staircase.
- No specific numerical values or additional annotations are provided on the graph, but the described behavior is consistent with the theoretical operation of a discrete-time integrator.

Figure 13.57 (a) Discrete-time integrator; (b) response of circuit to a constant input voltage.
The final value of $V_{\text {out }}$ in Fig. 13.57(a) after every clock cycle can be written as

$$
\begin{equation*}
V_{\text {out }}\left(k T_{C K}\right)=V_{\text {out }}\left[(k-1) T_{C K}\right]-V_{\text {in }}\left[(k-1) T_{C K}\right] \cdot \frac{C_{1}}{C_{2}} \tag{13.63}
\end{equation*}
$$

where the gain of the op amp is assumed large. Note that the small-signal settling time constant as charge is transferred from $C_{1}$ to $C_{2}$ is given by (13.50).

The integrator of Fig. 13.57(a) suffers from two important drawbacks. First, the input-dependent charge injection of $S_{1}$ introduces nonlinearity in the charge stored on $C_{1}$ and hence the output voltage. Second, the nonlinear capacitance at node $P$ resulting from the source/drain junctions of $S_{1}$ and $S_{2}$ leads to a nonlinear charge-to-voltage conversion when $C_{1}$ is switched to $X$. This can be understood with the aid of Fig. 13.58, where the charge stored on the total junction capacitance, $C_{j}$, is not equal to $V_{i n 0} C_{j}$, but rather equal to

$$
\begin{equation*}
q_{c j}=\int_{0}^{V i n 0} C_{j} d V \tag{13.64}
\end{equation*}
$$

Since $C_{j}$ is a function of voltage, $q_{c j}$ exhibits a nonlinear dependence on $V_{i n 0}$, thereby creating a nonlinear component at the output after the charge is transferred to the integration capacitor.
image_name:Figure 13.58
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Vin0(P), Nn: GND}
name: Cj, type: Capacitor, value: Cj, ports: {Np: P, Nn: GND}
name: S2, type: Switch, ports: {N1: P, N2: X}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Vout}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: X, OutP: Vout, OutN: GND}
]
extrainfo:The circuit is a switched-capacitor integrator with nonlinear junction capacitance effects. It includes a junction capacitance Cj that introduces nonlinearity, and an operational amplifier A0 for integration.

Figure 13.58 Effect of junction capacitance nonlinearity in SC integrator.

An integrator topology that resolves both of the foregoing issues is shown in Fig. 13.59(a). We study the circuit's operation in the sampling and integration modes. As shown in Fig. 13.59(b), in the sampling mode, $S_{1}$ and $S_{3}$ are on and $S_{2}$ and $S_{4}$ are off, allowing the voltage across $C_{1}$ to track $V_{i n}$ while the op amp and $C_{2}$ hold the previous value. In the transition to the integration mode, $S_{3}$ turns off first, injecting a constant charge onto $C_{1} ; S_{1}$ turns off next; and subsequently $S_{2}$ and $S_{4}$ turn on [Fig. 13.59(c)]. The charge stored on $C_{1}$ is therefore transferred to $C_{2}$ through the virtual ground node.
image_name:(a)
description:
[
name: S1, type: Switch, ports: {N1: Vin, N2: X1}
name: S2, type: Switch, ports: {N1: X1, N2: GND}
name: S3, type: Switch, ports: {N1: P, N2: GND}
name: S4, type: Switch, ports: {N1: P, N2: X}
name: C1, type: Capacitor, value: C1, ports: {Np: X1, Nn: P}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Vout}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: X, OutP: Vout}
]
extrainfo:The circuit is a parasitic-insensitive integrator. In sampling mode, switches S1 and S3 are on, allowing C1 to track Vin. In integration mode, the charge on C1 is transferred to C2 through the op-amp A0.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: Vout, Nn: InN(A0)}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: InN(A0), OutP: Vout}
]
extrainfo:In sampling mode, capacitors C1 and C2 are used with an op-amp to track and hold the input voltage Vin. Switches S1 and S3 are on, allowing C1 to charge to Vin, while S2 and S4 are off. The op-amp A0 and capacitor C2 hold the previous output voltage Vout.
image_name:(c)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: InN(A0), Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: InN(A0), Nn: Vout}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: InN(A0), OutP: Vout}
]
extrainfo:The circuit is a parasitic-insensitive integrator in integration mode. S1 and S3 are off, while S2 and S4 are on. C1 transfers charge to C2 through the op amp.

Figure 13.59 (a) Parasitic-insensitive integrator; (b) circuit of (a) in sampling mode; (c) circuit of (a) in integration mode.

Since $S_{3}$ turns off first, it introduces only a constant offset, which can be suppressed by differential operation. Moreover, because the left plate of $C_{1}$ is "driven" (Sec. 13.3.2), the charge injection or absorption of $S_{1}$ and $S_{2}$ contributes no error. Also, since node $X$ is a virtual ground, the charge injected or absorbed by $S_{4}$ is constant and independent of $V_{i n}$.

How about the nonlinear junction capacitance of $S_{3}$ and $S_{4}$ ? We observe that the voltage across this capacitance goes from near zero in the sampling mode to virtual ground in the integration mode. Since the voltage across the nonlinear capacitance changes by a very small amount, the resulting nonlinearity is negligible.

## 13.5 ■ Switched-Capacitor Common-Mode Feedback

Our study of common-mode feedback in Chapter 9 suggested that sensing the output CM level by means of resistors lowers the differential voltage gain of the circuit. We also observed that sensing techniques using MOSFETs that operate as source followers or variable resistors suffer from a limited linear range. Switched-capacitor CMFB networks provide an alternative that avoids both of these difficulties (but the circuit must be refreshed periodically).

In switched-capacitor common-mode feedback, the outputs are sensed by capacitors rather than resistors. Figure 13.60 depicts a simple example, where equal capacitors $C_{1}$ and $C_{2}$ reproduce at node $X$ the average of the changes in each output voltage. Thus, if $V_{\text {out } 1}$ and $V_{\text {out } 2}$ experience, say, a positive CM change, then $V_{X}$ and hence $I_{D 5}$ increase, pulling $V_{\text {out } 1}$ and $V_{\text {out } 2}$ down. The output CM level is then equal to $V_{G S 2}$ plus the voltage across $C_{1}$ and $C_{2}$.

image_name:Figure 13.60
description:
[
name: M1, type: NMOS, ports: {S: P, D: Vout1, G: Vin}
name: M2, type: NMOS, ports: {S: P, D: Vout2, G: Vin}
name: M5, type: NMOS, ports: {S: GND, D: P, G: X}
name: M3, type: PMOS, ports: {S: VDD, D: Vout1, G: Vb}
name: M4, type: PMOS, ports: {S: VDD, D: Vout2, G: Vb}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout1, Nn: X}
name: C2, type: Capacitor, value: C2, ports: {Np: Vout2, Nn: X}
]
extrainfo:The circuit is a simple switched-capacitor common-mode feedback circuit. It uses capacitors C1 and C2 to sense the common-mode voltage at nodes Vout1 and Vout2, and adjusts the voltage at node X accordingly. Transistors M3 and M4 are PMOS devices used for feedback control, while M1, M2, and M5 are NMOS devices for signal processing and feedback.

Figure 13.60 Simple SC commonmode feedback.

How is the voltage across $C_{1}$ and $C_{2}$ defined? This is typically carried out when the amplifier is in the sampling (or reset) mode and can be accomplished as shown in Fig. 13.61. Here, during CM level definition, the amplifier differential input is zero and switch $S_{1}$ is on. Transistors $M_{6}$ and $M_{7}$ operate as a linear sense circuit because their gate voltages are nominally equal. Thus, the circuit settles such that the ouput CM level is equal to $V_{G S 6,7}+V_{G S 5}$. At the end of this mode, $S_{1}$ turns off, leaving a voltage equal
image_name:Figure 13.61 Definition of the voltage across C1 and C2
description:This circuit is a differential amplifier with capacitive coupling. In the sampling mode, the differential input is zero, and the output common-mode level is set by transistors M6 and M7. Capacitors C1 and C2 store the voltage across them. The switch S1 is used to reset the circuit.

Figure 13.61 Definition of the voltage across $C_{1}$ and $C_{2}$.
to $V_{G S 6,7}$ across $C_{1}$ and $C_{2}$. In the amplification mode, $M_{6}$ and $M_{7}$ may experience a large nonlinearity, but they do not affect the performance of the main circuit because $S_{1}$ is off.

In applications where the output CM level must be defined more accurately than in the previous example, the topology shown in Fig. 13.62 may be used. Here, in the reset mode, one plate of $C_{1}$ and $C_{2}$ is switched to $V_{C M}$ while the other is connected to the gate of $M_{6}$. Each capacitor therefore sustains a voltage equal to $V_{C M}-V_{G S 6}$. In the amplification mode, $S_{2}$ and $S_{3}$ are on and the other switches are off, yielding an output CM level equal to $V_{C M}-V_{G S 6}+V_{G S 5}$. This value is equal to $V_{C M}$ if $I_{D 3}$ and $I_{D 4}$ are copied properly from $I_{R E F}$ so that $V_{G S 6}=V_{G S 5}$.
image_name:Figure 13.62 Alternative topology for definition of output CM level.
description:This circuit is an alternative topology for defining the output common-mode (CM) level. It includes differential pairs M1 and M2, with tail current provided by M5. Capacitors C1 and C2 are used for charge storage, and switches S1 to S5 control the operation modes. The PMOS transistors M3 and M4 form a current mirror for biasing. The circuit aims to stabilize the output CM level with large output swings, using IREF as a reference current.

Figure 13.62 Alternative topology for definition of output CM level.
With large output swings, the speed of the CMFB loop may in fact influence the settling of the differential output [6]. For this reason, part of the tail current of the differential pairs in Figs. 13.61 and 13.62 can be provided by a constant current source so that $M_{5}$ makes only small adjustments to the circuit.
