# Differential Amplifiers

The elegant concept of "differential" signals and amplifiers was invented in the 1940s and first utilized in vacuum-tube circuits. Since then, differential circuits have found increasingly wider usage in microelectronics and serve as a robust, high-performance design paradigm in many of today's systems. This chapter describes bipolar and MOS differential amplifiers and formulates their large-signal and small-signal properties. The concepts are outlined below.

General Considerations

- Differential Signals
- Differential Pair

Bipolar Differential Pair

- Qualitative Analysis
- Large-Signal Analysis
- Small-Signal Analysis

MOS Differential Pair

- Qualitative Analysis
- Large-Signal Analysis
- Small-Signal Analysis

Other Concepts

- Cascode Pair
- Common-Mode Rejection
- Pair with Active Load

## 10.1 GENERAL CONSIDERATIONS

### 10.1.1 Initial Thoughts

We have already seen that op amps have two inputs, a point of contrast to the amplifiers studied in previous chapters. In order to further understand the need for differential circuits, let us first consider an example.

Example Having learned the design of rectifiers and basic amplifier stages, an electrical engineering student constructs the circuit shown in Fig. 10.1(a) to amplify the signal produced by a microphone. Unfortunately, upon applying the result to a speaker, the student observes that the amplifier output contains a strong "humming" noise, i.e., a steady low-frequency component. Explain what happens.

Recall from Chapter 3 that the current drawn from the rectified output creates a ripple waveform at twice the ac line frequency ( 50 or 60 Hz ) [Fig. 10.1(b)]. Examining the output of the common-emitter stage, we can identify two components: (1) the amplified version of the microphone signal and (2) the ripple waveform present on $V_{C C}$. For the latter, we can write

$$
\begin{equation*}
V_{\text {out }}=V_{C C}-R_{C} I_{C} \tag{10.1}
\end{equation*}
$$

noting that $V_{\text {out }}$ simply "tracks" $V_{C C}$ and hence contains the ripple in its entirety. The "hum" originates from the ripple. Figure 10.1(c) depicts the overall output in the presence of both the signal and the ripple. Illustrated in Fig. 10.1(d), this phenomenon is summarized as the "supply noise goes to the output with a gain of unity." (A MOS implementation would suffer from the same problem.)
image_name:(a)
description:The circuit is a common-emitter amplifier stage powered by a rectifier. It shows how ripple from the power supply can affect the output signal. The ripple frequency for a full-wave rectifier would be 120 Hz, while for a half-wave rectifier it would be 60 Hz. Increasing C1 can reduce the ripple amplitude.
image_name:(b)
description:The graph labeled (b) is a time-domain waveform illustrating the ripple on the supply voltage, denoted as \( V_{CC} \). The x-axis represents time \( t \), though specific units are not provided, and the y-axis represents voltage, specifically \( V_{CC} \). The waveform is characterized by a periodic, sawtooth-like shape, indicating the presence of ripple. This ripple is a result of the rectification process depicted in the circuit diagram (a), likely from a full-wave or half-wave rectifier.

The ripple shows a consistent, repeating pattern, suggesting a steady frequency, which is typically double the input AC frequency for a full-wave rectifier (e.g., 120 Hz if the input is 60 Hz) or the same frequency for a half-wave rectifier. The waveform does not reach a steady DC level but instead oscillates around a mean value, reflecting the incomplete smoothing by the capacitor \( C_1 \) in the circuit.

There are no specific annotations or markers on this graph to indicate particular voltage levels or time intervals. The overall behavior indicates that the ripple amplitude could be reduced by increasing the capacitance of \( C_1 \), as mentioned in the context.
image_name:(c)
description:The graph in Figure 10.1(c) is a time-domain waveform depicting the output voltage, \( V_{\text{out}} \), from a common-emitter (CE) stage circuit. The horizontal axis represents time, \( t \), while the vertical axis represents the output voltage, \( V_{\text{out}} \), though specific units are not provided.

The waveform illustrates the combined effect of a voice signal and the ripple from the power supply. The graph shows a series of irregular oscillations, indicating the presence of both the desired voice signal and unwanted ripple noise. The oscillations appear to be superimposed, with the ripple frequency likely being lower than that of the voice signal, resulting in a noisy output.

Overall, the graph highlights the issue of supply noise, which is transferred to the output without attenuation, as mentioned in the context. The ripple's presence can cause distortion in the voice signal, leading to a "hum" in the output. This visual representation underscores the importance of addressing power supply noise to maintain signal integrity in audio applications.
image_name:(d)
description:The diagram labeled as Figure 10.1(d) illustrates the paths taken by both the ripple and the signal to reach the output. The main components involved include a resistor \( R \), a transistor, and the power supply voltage \( V_{CC} \). The diagram shows how the ripple from the supply voltage \( V_{CC} \) and the input signal both affect the transistor, which is depicted within a red box.

1. **Main Components:**
- **Resistor (R):** This component is connected to the supply voltage \( V_{CC} \) and plays a role in setting the biasing conditions for the transistor.
- **Transistor:** The primary active component that amplifies the input signal. It is connected to ground (GND) and receives both the ripple and the input signal.
- **Power Supply (\( V_{CC} \)):** Provides the necessary voltage for the circuit operation and contains a ripple component.

2. **Flow of Information or Control:**
- The ripple from the power supply \( V_{CC} \) is shown to directly influence the output by passing through the resistor \( R \) and affecting the transistor. This path is indicated by a gray arrow labeled 'Ripple.'
- Simultaneously, the input signal also reaches the transistor, affecting its operation. This path is indicated by another arrow labeled 'Signal.'
- Both the ripple and the signal converge at the transistor, which then drives the output.

3. **Labels, Annotations, and Key Indicators:**
- The diagram is annotated with labels such as 'Ripple' and 'Signal' to clearly indicate the paths taken by each component to the output.
- The transistor is highlighted in a red box, emphasizing its role in processing both the ripple and the signal.

4. **Overall System Function:**
- The primary function of this system is to demonstrate how both the supply voltage ripple and the input signal affect the output. The ripple from the power supply is not attenuated and directly affects the output, resulting in noise or ‘hum’ in the output signal. The diagram effectively shows that the supply noise is transferred to the output with a gain of unity, meaning it is not diminished or amplified, merely passed through as-is.

Figure 10.1 (a) CE stage powered by a rectifier, (b) ripple on supply voltage, (c) effect at output, (d) ripple and signal paths to output.

Exercise What is the hum frequency for a full-wave rectifier or a half-wave rectifier?

How should we suppress the hum in the above example? We can increase $C_{1}$, thus lowering the ripple amplitude, but the required capacitor value may become prohibitively large if many circuits draw current from the rectifier. Alternatively, we can modify the amplifier topology such that the output is insensitive to $V_{C C}$. How is that possible? Equation (10.1) implies that a change in $V_{C C}$ directly appears in $V_{\text {out }}$, fundamentally because both $V_{\text {out }}$ and $V_{C C}$ are measured with respect to ground and differ by $R_{C} I_{C}$. But what if $V_{\text {out }}$ is not "referenced" to ground?! More specifically, what if $V_{\text {out }}$ is measured with respect to another point that itself experiences the supply ripple to the same extent? It is thus possible to eliminate the ripple from the "net" output.

While rather abstract, the above conjecture can be readily implemented. Figure 10.2(a) illustrates the core concept. The CE stage is duplicated on the right, and the output is now measured between nodes $X$ and $Y$ rather than from $X$ to ground. What happens if $V_{C C}$
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RC1, type: Resistor, value: RC1, ports: {N1: VCC, N2: X}
name: RC2, type: Resistor, value: RC2, ports: {N1: VCC, N2: Y}
name: Q1, type: NPN, ports: {C: X, B: P, E: GND}
name: Q2, type: NPN, ports: {C: Y, B: Bias, E: GND}
name: C, type: Capacitor, ports: {N1: Vin, N2: P}
]
extrainfo:The circuit uses two NPN transistors in common-emitter configuration to eliminate ripple by measuring the output between nodes X and Y. Both transistors are biased and connected to resistors RC1 and RC2, which are connected to VCC. The output voltage Vout is the difference between the voltages at nodes X and Y, effectively canceling out any ripple present in VCC.

(a)
image_name:(b)
description:
[
name: RC1, type: Resistor, value: RC1, ports: {N1: VCC, N2: X}
name: RC2, type: Resistor, value: RC2, ports: {N1: VCC, N2: Y}
name: Q1, type: NPN, ports: {C: X, B: Vin, E: GND}
name: Q2, type: NPN, ports: {C: Y, B: Bias, E: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: Y, InN: X, OutP: , OutN:}
]
extrainfo:The circuit uses two NPN transistors in common-emitter configuration to eliminate ripple by measuring the output between nodes X and Y. Both transistors are biased and connected to resistors RC1 and RC2, which are connected to VCC. The output voltage Vout is the difference between the voltages at nodes X and Y, effectively canceling out any ripple present in VCC.

(b)

Figure 10.2 Use of two CE stages to remove effect of ripple.
contains ripple? Both $V_{X}$ and $V_{Y}$ rise and fall by the same amount and hence the difference between $V_{X}$ and $V_{Y}$ remains free from the ripple.

In fact, denoting the ripple by $v_{r}$, we express the small-signal voltages at these nodes as

$$
\begin{align*}
& v_{X}=A_{v} v_{i n}+v_{r}  \tag{10.2}\\
& v_{Y}=v_{r} \tag{10.3}
\end{align*}
$$

That is,

$$
\begin{equation*}
v_{X}-v_{Y}=A_{v} v_{i n} \tag{10.4}
\end{equation*}
$$

Note that $Q_{2}$ carries no signal, simply serving as a constant current source.
The above development serves as the foundation for differential amplifiers: the symmetric CE stages provide two output nodes whose voltage difference remains free from the supply ripple.

### 10.1.2 Differential Signals

Let us return to the circuit of Fig. 10.2(a) and recall that the duplicate stage consisting of $Q_{2}$ and $R_{C 2}$ remains "idle," thereby "wasting" current. We may therefore wonder if this stage can provide signal amplification in addition to establishing a reference point for $V_{\text {out }}$. In our first attempt, we directly apply the input signal to the base of $Q_{2}$ [Fig. 10.3(a)]. Unfortunately, the signal components at $X$ and $Y$ are in phase, canceling each other as they appear in $v_{X}-v_{Y}$ :

$$
\begin{align*}
v_{X} & =A_{v} v_{i n}+v_{r}  \tag{10.5}\\
v_{Y} & =A_{v} v_{i n}+v_{r}  \tag{10.6}\\
& \Rightarrow v_{X}-v_{Y}=0 . \tag{10.7}
\end{align*}
$$

For the signal components to enhance each other at the output, we can invert one of the input phases as shown in Fig. 10.3(b), obtaining

$$
\begin{align*}
& v_{X}=A_{v} v_{i n}+v_{r}  \tag{10.8}\\
& v_{Y}=-A_{v} v_{i n}+v_{r} \tag{10.9}
\end{align*}
$$

and hence

$$
\begin{equation*}
v_{X}-v_{Y}=2 A_{v} v_{i n} \tag{10.10}
\end{equation*}
$$

image_name:(a)
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: C1, type: Capacitor, ports: {N1: Vin, N2: Bias1}
name: Q1, type: NPN, ports: {C: X, B: Bias1, E: GND}
name: Q2, type: NPN, ports: {C: Y, B: Bias2, E: GND}
name: C2, type: Capacitor, ports: {N1: Vin, N2: Bias2}
name: RC1, type: Resistor, value: RC1, ports: {N1: VCC, N2: X}
name: RC2, type: Resistor, value: RC2, ports: {N1: VCC, N2: Y}
]
extrainfo:The circuit in Figure 10.3(a) shows a configuration where a single input signal is applied to two common-emitter (CE) stages. The output nodes X and Y are connected to the collectors of the transistors Q1 and Q2, respectively. This setup is used to enhance the output signal by utilizing two amplifying stages.
image_name:(b)
description:
[
'name': 'VCC', 'type': 'VoltageSource', 'value': 'VCC', 'ports': {'Np': 'VCC', 'Nn': 'GND'
'name': 'RC1', 'type': 'Resistor', 'value': 'RC1', 'ports': {'N1': 'VCC', 'N2': 'X'
'name': 'RC2', 'type': 'Resistor', 'value': 'RC2', 'ports': {'N1': 'VCC', 'N2': 'Y'
'name': 'Q1', 'type': 'NPN', 'ports': {'C': 'X', 'B': '+Vin', 'E': 'GND'
'name': 'Q2', 'type': 'NPN', 'ports': {'C': 'Y', 'B': '-Vin', 'E': 'GND'
]
extrainfo:The circuit in diagram (b) is a differential amplifier using two NPN transistors Q1 and Q2. The input signals are +Vin and -Vin, providing differential input to the bases of Q1 and Q2. The resistors RC1 and RC2 are connected to VCC and serve as collector resistors for Q1 and Q2 respectively, providing load to the transistors. The emitters of both transistors are connected to ground, and the collectors are connected to nodes X and Y, which serve as output nodes for the differential signals. The circuit is designed to provide twice the output swing by exploiting the differential input signals.
image_name:(c)
description:The circuit diagram (c) illustrates the use of a transformer to generate differential phases from a single input signal. This setup is used to convert a microphone signal into two complementary signals, which are then processed by the circuit to enhance the output signal swing.

Figure 10.3 (a) Application of one input signal to two CE stages, (b) use of differential input signals, (c) generation of differential phases from one signal.

Compared to the circuit of Fig. 10.2(a), this topology provides twice the output swing by exploiting the amplification capability of the duplicate stage.

The reader may wonder how $-v_{\text {in }}$ can be generated. Illustrated in Fig. 10.3(c), a simple approach is to utilize a transformer to convert the microphone signal to two components bearing a phase difference of $180^{\circ}$.

Our thought process has led us to the specific waveforms in Fig. 10.3(b): the circuit senses two inputs that vary by equal and opposite amounts and generates two outputs that behave in a similar fashion. These waveforms are examples of "differential" signals and stand in contrast to "single-ended" signals-the type to which we are accustomed from basic circuits and previous chapters of this book. More specifically, a single-ended signal is one measured with respect to the common ground [Fig. 10.4(a)] and "carried by one line," whereas a differential signal is measured between two nodes that have equal and opposite swings [Fig. 10.4(b)] and is thus "carried by two lines."

Figure 10.4(c) summarizes the foregoing development. Here, $V_{1}$ and $V_{2}$ vary by equal and opposite amounts and have the same average (dc) level, $V_{C M}$, with respect to ground:

$$
\begin{align*}
& V_{1}=V_{0} \sin \omega t+V_{C M}  \tag{10.11}\\
& V_{2}=-V_{0} \sin \omega t+V_{C M} \tag{10.12}
\end{align*}
$$

Since each of $V_{1}$ and $V_{2}$ has a peak-to-peak swing of $2 V_{0}$, we say the "differential swing" is $4 V_{0}$. We may also say $V_{1}$ and $V_{2}$ are differential signals to emphasize that they vary by equal and opposite amounts around a fixed level, $V_{C M}$.

The dc voltage that is common to both $V_{1}$ and $V_{2}$ [ $V_{C M}$ in Fig. 10.4(c)] is called the "common-mode (CM) level." That is, in the absence of differential signals, the two nodes remain at a potential equal to $V_{C M}$ with respect to the global ground. For example, in the transformer of Fig. 10.3(c),$+v_{\text {in }}$ and $-v_{\text {in }}$ display a CM level of zero because the center tap of the transformer is grounded.
image_name:(a)
description:
[
name: A1, type: OpAmp, ports: {InP: Vin, InN: GND, OutP: Vout, OutN: GND}
name: Q1, type: NPN, ports: {C: Vout, B: Vin, E: GND}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: Resistor, type: Resistor, ports: {N1: VCC, N2: Vout}
]
extrainfo:The circuit consists of an operational amplifier and an NPN transistor configuration. The OpAmp is configured with a single-ended input and output. The NPN transistor is used as an amplifier, with the collector connected to Vout, the base to Vin, and the emitter grounded. A resistor is connected between VCC and Vout. The circuit is powered by a voltage source VCC.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: C1, B: V, E: GND}
name: Q2, type: NPN, ports: {C: C2, B: Vin, E: GND}
name: R1, type: Resistor, ports: {N1: VCC, N2: C1}
name: R2, type: Resistor, ports: {N1: VCC, N2: C2}
name: V, type: VoltageSource, value: V, ports: {Np: V, Nn: GND}
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
]
extrainfo:The circuit diagram shows a differential amplifier configuration with an operational amplifier and an NPN transistor. The operational amplifier receives a differential input signal (Vin) and provides an output (Vout). The NPN transistor is configured as a common-emitter amplifier with the collector connected to Vout, the base connected to Vin, and the emitter grounded. VCC is the power supply for the transistor.

(a)
image_name:Figure 10.5
description:The circuit diagram shows a differential amplifier configuration with an operational amplifier and two NPN transistors. The operational amplifier receives a differential input signal (Vin) and provides an output (Vout). The NPN transistors are configured as common-emitter amplifiers with the collectors connected to VCC, the bases connected to Vin, and the emitters grounded. VCC is the power supply for the transistors.

(b)
image_name:(c) illustration of common-mode level
description:The graph is a time-domain waveform illustrating the common-mode level (V_CM) over time (t). The x-axis represents time (t), and the y-axis represents the common-mode voltage (V_CM). The graph is linear in both axes, with no specific scale or units indicated.

The waveform shows a sinusoidal pattern with two key voltage levels, V_1 and V_2, which are marked by horizontal dashed lines. The amplitude of the waveform is labeled as 2V_0, indicating the peak-to-peak voltage difference. The sinusoidal wave oscillates between V_1 and V_2, showing a periodic behavior typical of a sine wave.

The graph highlights the concept of common-mode voltage by depicting the sinusoidal wave centered around a mean value, which is the common-mode level. This level is crucial in differential amplifier circuits, where balancing the input signals is essential to minimize common-mode noise.

No specific numerical values are provided for V_1, V_2, or V_0, but the annotations help in understanding the amplitude and periodic nature of the waveform. The graph serves as a visual representation of how common-mode voltage varies over time in such circuits.

(c)

Figure 10.4 (a) Single-ended signals, (b) differential signals, (c) illustration of commonmode level.

Solution The center tap can simply be tied to a voltage equal to +2 V (Fig. 10.5).
image_name:Figure 10.5
description:The circuit includes a diode grounded on both anode and cathode, an inductor connected between ground and Vin1, and a capacitor with a value of 2V connected between Vin1 and ground. The diagram also illustrates the waveform of Vin1 and Vin2 with a common-mode voltage of +2V.
image_name:(c)
description:The graph in Figure 10.5(c) illustrates the common-mode level in a circuit. It is a time-domain waveform graph depicting two input voltages, \( V_{in1} \) and \( V_{in2} \), over time, \( t \). The horizontal axis represents time, while the vertical axis represents voltage. The scale is linear, though specific units for time are not provided.

Both \( V_{in1} \) and \( V_{in2} \) are sinusoidal signals with the same amplitude and frequency, but they are 180 degrees out of phase with each other. This means when \( V_{in1} \) reaches its peak, \( V_{in2} \) reaches its trough, and vice versa.

A dotted line is drawn at the +2 V level, indicating the common-mode voltage level. The waveform amplitudes oscillate around this +2 V reference, highlighting the common-mode nature of the signals. The graph visually represents how the common-mode voltage remains constant at +2 V, even as the differential components of \( V_{in1} \) and \( V_{in2} \) vary sinusoidally over time.

Figure 10.5

Exercise Does the CM level change if the inputs of the amplifier draw a bias current?

| Example <br> 10.3 | Determine the common-mode level at the output of the circuit shown in Fig. 10.3(b). |
| :---: | :---: |
| Solution | In the absence of signals, $V_{X}=V_{Y}=V_{C C}-R_{C} I_{C}$ (with respect to ground), where $R_{C}=R_{C 1}=R_{C 2}$ and $I_{C}$ denotes the bias current of $Q_{1}$ and $Q_{2}$. Thus, $V_{C M}=V_{C C}-R_{C} I_{C}$. Interestingly, the ripple affects $V_{C M}$ but not the differential output. |
| Exercise | If a resistor of value $R_{1}$ is inserted between $V_{C C}$ and the top terminals of $R_{C 1}$ and $R_{C 2}$, what is the output CM level? |

Our observations regarding supply ripple and the use of the "duplicate stage" provide sufficient justification for studying differential signals. But, how about the common-mode level? What is the significance of $V_{C M}=V_{C C}-R_{C} I_{C}$ in the above example? Why is it interesting that the ripple appears in $V_{C M}$ but not in the differential output? We will answer these important questions in the following sections.

### 10.1.3 Differential Pair

Before formally introducing the differential pair, we must recognize that the circuit of Fig. 10.4(b) senses two inputs and can therefore serve as $A_{1}$ in Fig. 10.2(b). This observation leads to the differential pair.

While sensing and producing differential signals, the circuit of Fig. 10.4(b) suffers from some drawbacks. Fortunately, a simple modification yields an elegant, versatile topology. Illustrated in Fig. 10.6(a), the (bipolar) "differential pair" ${ }^{1}$ is similar to the circuit of Fig. 10.4(b), except that the emitters of $Q_{1}$ and $Q_{2}$ are tied to a constant current source rather than to ground. We call $I_{E E}$ the "tail current source." The MOS counterpart is shown in Fig. 10.6(b). In both cases, the sum of the transistor currents is equal to the tail current. Our objective is to analyze the large-signal and small-signal behavior of these circuits and demonstrate their advantages over the "single-ended" stages studied in previous chapters.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: X, B: Vin1, E: P}
name: Q2, type: NPN, ports: {C: Y, B: Vin2, E: P}
name: RC1, type: Resistor, value: RC, ports: {N1: VCC, N2: X}
name: RC2, type: Resistor, value: RC, ports: {N1: VCC, N2: Y}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a bipolar differential pair with a constant current source IEE connected at the emitters of Q1 and Q2. The resistors RC are connected to the collectors of Q1 and Q2, and the input voltages Vin1 and Vin2 are applied to the bases of Q1 and Q2 respectively.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin1}
name: M2, type: NMOS, ports: {S: P, D: Y, G: Vin2}
name: RD, type: Resistor, value: RD, ports: {N1: X, N2: VDD}
name: RD, type: Resistor, value: RD, ports: {N1: Y, N2: VDD}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a MOS differential pair with a constant current source ISS providing the tail current. The differential inputs are Vin1 and Vin2, and the differential outputs are at nodes X and Y. The resistors RD provide load resistance for the differential pair.

Figure 10.6 (a) Bipolar and (b) MOS differential pairs.
For each differential pair, we begin with a qualitative, intuitive analysis and subsequently formulate the large-signal and small-signal behavior. We also assume each circuit is perfectly symmetric, i.e., the transistors are identical and so are the resistors.

## 10.2 BIPOLAR DIFFERENTIAL PAIR

### 10.2.1 Qualitative Analysis

It is instructive to first examine the bias conditions of the circuit. Recall from Section 10.1.2 that in the absence of signals, differential nodes reside at the common-mode level. We therefore draw the pair as shown in Fig. 10.7, with the two inputs tied to $V_{C M}$ to indicate no signal exists at the input. By virtue of symmetry,

$$
\begin{align*}
V_{B E 1} & =V_{B E 2}  \tag{10.13}\\
I_{C 1} & =I_{C 2}=\frac{I_{E E}}{2}, \tag{10.14}
\end{align*}
$$

[^8]image_name:Figure 10.7
description:
[
name: Q1, type: NPN, ports: {C: X, B: VCM, E: e1e2}
name: Q2, type: NPN, ports: {C: Y, B: VCM, E: e1e2}
name: RC1, type: Resistor, value: RC, ports: {N1: VCC, N2: X}
name: RC2, type: Resistor, value: RC, ports: {N1: VCC, N2: Y}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: VCM, type: VoltageSource, value: VCM, ports: {Np: VCM, Nn: GND}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: e1e2, Nn: GND}
]
extrainfo:The circuit is a differential pair with NPN transistors Q1 and Q2. Both transistors share the same emitter node e1e2, which is connected to a current source IEE. The bases of Q1 and Q2 are tied together and connected to a common-mode voltage source VCM. The collectors of Q1 and Q2 are connected to resistors RC1 and RC2, respectively, which are connected to the VCC voltage source. The circuit is symmetrical, and it operates in equilibrium when the input voltages are equal, resulting in equal collector currents and voltages at nodes X and Y.

Figure 10.7 Response of differential pair to input CM change.
where the collector and emitter currents are assumed equal. We say the circuit is in "equilibrium."

Thus, the voltage drop across each load resistor is equal to $R_{C} I_{E E} / 2$ and hence

$$
\begin{equation*}
V_{X}=V_{Y}=V_{C C}-R_{C} \frac{I_{E E}}{2} . \tag{10.15}
\end{equation*}
$$

In other words, if the two input voltages are equal, so are the two outputs. We say a zero differential input produces a zero differential output. The circuit also "rejects" the effect of supply ripple: if $V_{C C}$ experiences a change, the differential output, $V_{X}-V_{Y}$, does not.

Are $Q_{1}$ and $Q_{2}$ in the active region? To avoid saturation, the collector voltages must not fall below the base voltages:

$$
\begin{equation*}
V_{C C}-R_{C} \frac{I_{E E}}{2} \geq V_{C M}, \tag{10.16}
\end{equation*}
$$

revealing that $V_{C M}$ cannot be arbitrarily high.

Did you know?

The amplifiers studied in previous chapters have one input with respect to ground [Fig. (a)] whereas the differential pair has two distinct inputs. An important application of the differential pair is at the input of op amps, where inverting and noninverting input terminals are necessary [Fig. (b)]. Without this second input, many op-amp-based functions would be difficult to realize. For example, the noninverting amplifier and the precision rectifier utilize both inputs.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: Vin1, E: GND}
]
extrainfo:The circuit is a differential pair with two NPN transistors Q1 and Q2. The current source Ie2 provides a tail current, and the emitters of both transistors are connected to ground. The collectors are connected together at the output node Vout.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: load1, B: Vin, E: e1e2}
name: Q2, type: NPN, ports: {C: load2, B: Vin2, E: GND}
name: Ie2, type: CurrentSource, ports: {Np: e1e2, Nn: GND}
]
extrainfo:The circuit diagram shows a differential amplifier with two NPN transistors (Q1 and Q2) and a current source (Ie2). It has two distinct inputs (Vin1 and Vin2) and is used at the input of op amps for inverting and noninverting functions.

(a)

Amplifiers with single-ended and differential inputs.

| $\begin{array}{\|l\|l\|}  & \text { Example } \\ 10.4 \end{array}$ | A bipolar differential pair employs a load resistance of $1 \mathrm{k} \Omega$ and a tail current of 1 mA . How close to $V_{C C}$ can $V_{C M}$ be chosen? |  |
| :---: | :---: | :---: |
| Solution | Equation 10.16 gives $\begin{aligned} V_{C C}-V_{C M} & \geq R_{C} \frac{I_{E E}}{2} \\ & \geq 0.5 \mathrm{~V} . \end{aligned}$ | $\begin{aligned} & (10.17) \\ & (10.18) \end{aligned}$ |
|  | That is, $V_{C M}$ must remain below $V_{C C}$ by at least 0.5 V . |  |

[^9]image_name:Figure 10.8
description:The diagram in Figure 10.8 illustrates the effect of common-mode input voltages \( V_{CM1} \) and \( V_{CM2} \) on the output voltages \( V_X \) and \( V_Y \) of a bipolar differential pair circuit. The graph is a schematic representation, not a plot with numerical axes.

Type of Graph and Function:
This is a schematic diagram rather than a traditional graph. It visually represents voltage levels and relationships in a differential pair circuit.
Axes Labels and Units:
There are no traditional axes with labels or units in this diagram. Instead, it uses horizontal lines and annotations to indicate voltage levels.

Overall Behavior and Trends:
- The diagram shows that the common-mode input voltage \( V_{CM} \) has an upper limit to avoid saturation.
- The upper limit is marked as \( V_{CC} - \frac{R_C I_{EE}}{2} \), where \( V_{CC} \) is the supply voltage, \( R_C \) is the load resistance, and \( I_{EE} \) is the tail current.
- \( V_{CM1} \) and \( V_{CM2} \) are two different common-mode input voltages, both below this upper limit.

Key Features and Technical Details:
- The upper limit of \( V_{CM} \) is shown as a dashed line labeled "Upper Limit of \( V_{CM} \) to Avoid Saturation."
- The vertical distance between \( V_{CC} \) and the upper limit is \( \frac{R_C I_{EE}}{2} \).
- The diagram indicates that \( V_X \) and \( V_Y \) are the output voltages, and they are affected by \( V_{CM1} \) and \( V_{CM2} \).

Annotations and Specific Data Points:
- Arrows from \( V_{CM1} \) and \( V_{CM2} \) point towards \( V_X \) and \( V_Y \), indicating their influence.
- The diagram emphasizes maintaining \( V_{CM} \) below the specified upper limit to prevent saturation of the differential pair's output transistors.

Figure 10.8 Effect of $V_{C M 1}$ and $V_{C M 2}$ at output.

Now, let us vary $V_{C M}$ in Fig. 10.7 by a small amount and determine the circuit's response. Interestingly, Eqs. (10.13)-(10.15) remain unchanged, thereby suggesting that neither the collector current nor the collector voltage of the transistors is affected. We say the circuit does not respond to changes in the input common-mode level, or the circuit "rejects" input CM variations. Figure 10.8 summarizes these results.

The "common-mode rejection" capability of the differential pair distinctly sets it apart from our original circuit in Fig. 10.4(b). In the latter, if the base voltage of $Q_{1}$ and $Q_{2}$ changes, so do their collector currents and voltages (why?). The reader may recognize that it is the tail current source in the differential pair that guarantees constant collector currents and hence rejection of the input CM level.

With our treatment of the common-mode response, we now turn to the more interesting case of differential response. We hold one input constant, vary the other, and examine the currents flowing in the two transistors. While not exactly differential, such input signals provide a simple, intuitive starting point. Recall that $I_{C 1}+I_{C 2}=I_{E E}$.

Consider the circuit shown in Fig. 10.9(a), where the two transistors are drawn with a vertical offset to emphasize that $Q_{1}$ senses a more positive base voltage. Since the difference between the base voltages of $Q_{1}$ and $Q_{2}$ is so large, we postulate that $Q_{1}$ "hogs" all of the tail current, thereby turning $Q_{2}$ off. That is,

$$
\begin{align*}
I_{C 1} & =I_{E E}  \tag{10.19}\\
I_{C 2} & =0, \tag{10.20}
\end{align*}
$$

image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: X, B: Vin1, E: P}
name: Q2, type: NPN, ports: {C: Y, B: Vin2, E: P}
name: RC1, type: Resistor, value: RC, ports: {N1: VCC, N2: X}
name: RC2, type: Resistor, value: RC, ports: {N1: VCC, N2: Y}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential pair with NPN transistors Q1 and Q2. The input voltages Vin1 and Vin2 control the current distribution between Q1 and Q2. In scenario (a), Q1 receives a higher base voltage (+2 V) than Q2 (+1 V), leading Q1 to conduct more current. The output voltage Vout is measured between nodes X and Y, across the resistors RC.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: X, B: Vin1, E: P}
name: Q2, type: NPN, ports: {C: Y, B: Vin2, E: P}
name: RC1, type: Resistor, value: RC, ports: {N1: X, N2: VCC}
name: RC2, type: Resistor, value: RC, ports: {N1: Y, N2: VCC}
name: VCC, type: VoltageSource, value: 2.5V, ports: {Np: VCC, Nn: GND}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: P, Nn: GND}
]
extrainfo:In this configuration, Q2 is turned on due to the higher base voltage at Vin2, drawing all the tail current IEE, while Q1 is off. This results in Vout being close to VCC. The circuit is a differential amplifier with a large negative input difference.

Figure 10.9 Response of bipolar differential pair to (a) large positive input difference and (b) large negative input difference.
and hence

$$
\begin{align*}
& V_{X}=V_{C C}-R_{C} I_{E E}  \tag{10.21}\\
& V_{Y}=V_{C C} \tag{10.22}
\end{align*}
$$

But, how can we prove that $Q_{1}$ indeed absorbs all of $I_{E E}$ ? Let us assume that it is not so; i.e., $I_{C 1}<I_{E E}$ and $I_{C 2} \neq 0$. If $Q_{2}$ carries an appreciable current, then its base-emitter voltage must reach a typical value of, say, 0.8 V . With its base held at +1 V , the device therefore requires an emitter voltage of $V_{P} \approx 0.2 \mathrm{~V}$. However, this means that $Q_{1}$ sustains a baseemitter voltage of $V_{i n 1}-V_{P}=+2 \mathrm{~V}-0.2 \mathrm{~V}=1.8 \mathrm{~V}$ !! Since with $V_{B E}=1.8 \mathrm{~V}$, a typical transistor carries an enormous current, and since $I_{C 1}$ cannot exceed $I_{E E}$, we conclude that the conditions $V_{B E 1}=1.8 \mathrm{~V}$ and $V_{P} \approx 0.2 \mathrm{~V}$ cannot occur. In fact, with a typical baseemitter voltage of $0.8 \mathrm{~V}, Q_{1}$ holds node $P$ at approximately +1.2 V , ensuring that $Q_{2}$ remains off.

Symmetry of the circuit implies that swapping the base voltages of $Q_{1}$ and $Q_{2}$ reverses the situation [Fig. 10.9(b)], giving

$$
\begin{align*}
I_{C 2} & =I_{E E}  \tag{10.23}\\
I_{C 1} & =0 \tag{10.24}
\end{align*}
$$

and hence

$$
\begin{align*}
V_{Y} & =V_{C C}-R_{C} I_{E E}  \tag{10.25}\\
V_{X} & =V_{C C} \tag{10.26}
\end{align*}
$$

The above experiments reveal that, as the difference between the two inputs departs from zero, the differential pair "steers" the tail current from one transistor to the other. In fact, based on Eqs. (10.14), (10.19), and (10.23), we can sketch the collector currents of $Q_{1}$ and $Q_{2}$ as a function of the input difference [Fig. 10.10(a)]. We have not yet formulated these characteristics but we do observe that the collector current of each transistor goes from 0 to $I_{E E}$ if $\left|V_{i n 1}-V_{i n 2}\right|$ becomes sufficiently large.

It is also important to note that $V_{X}$ and $V_{Y}$ vary differentially in response to $V_{i n 1}-V_{\text {in } 2}$. From Eqs. (10.15), (10.21), and (10.25), we can sketch the input/output characteristics of the circuit as shown in Fig. 10.10(b). That is, a nonzero differential input yields a nonzero differential output-a behavior in sharp contrast to the CM response. Since $V_{X}$ and $V_{Y}$
image_name:(a)
description:The graph labeled (a) is a plot of collector currents (I_C1 and I_C2) as a function of the differential input voltage (V_in1 - V_in2) in a bipolar differential pair circuit.

1. **Type of Graph and Function:**
- The graph is a characteristic curve representing how the collector currents change with varying differential input voltage in a differential amplifier.

2. **Axes Labels and Units:**
- The x-axis is labeled as the differential input voltage (V_in1 - V_in2).
- The y-axis represents the collector currents I_C1 and I_C2.
- Units are not explicitly mentioned, but the context implies volts for the x-axis and amperes for the y-axis.

3. **Overall Behavior and Trends:**
- The graph exhibits a symmetrical behavior around the origin (0 on the x-axis).
- As the differential input voltage increases positively, I_C2 increases towards I_EE (the total emitter current), while I_C1 decreases towards zero.
- Conversely, as the differential input voltage becomes negative, I_C1 increases towards I_EE, while I_C2 decreases towards zero.
- At V_in1 - V_in2 = 0, both I_C1 and I_C2 are equal to I_EE/2, indicating balanced current distribution.

4. **Key Features and Technical Details:**
- The maximum and minimum values of the collector currents are I_EE and 0, respectively.
- The curve is smooth, indicating a continuous transition of current from one transistor to the other as the input voltage changes.
- The crossing point at V_in1 - V_in2 = 0 is a critical point where the currents are equally split.

5. **Annotations and Specific Data Points:**
- The graph is annotated with the values I_EE (total emitter current) and I_EE/2 at the crossing point.
- The symmetry and crossing point highlight the differential nature of the circuit, where the input voltage difference directly affects the current distribution between the two transistors.
image_name:(b)
description:The graph in Figure 10.10(b) illustrates the relationship between the differential input voltage \( V_{in1} - V_{in2} \) and the differential output voltages \( V_X \) and \( V_Y \) in a bipolar differential pair circuit.

1. **Type of Graph and Function:**
- The graph is a characteristic curve showing the differential input-output relationship in a bipolar differential pair circuit.

2. **Axes Labels and Units:**
- The horizontal axis represents the differential input voltage \( V_{in1} - V_{in2} \).
- The vertical axis represents the output voltages \( V_X \) and \( V_Y \).
- No specific units are marked, but the context implies they are likely in volts.

3. **Overall Behavior and Trends:**
- The graph shows a symmetrical behavior around the vertical axis at zero differential input.
- As the differential input voltage increases positively, \( V_X \) increases towards \( V_{CC} \) and \( V_Y \) decreases towards \( V_{CC} - R_C I_{EE} \).
- Conversely, as the differential input voltage becomes more negative, \( V_X \) decreases and \( V_Y \) increases, showing a mirror image behavior.

4. **Key Features and Technical Details:**
- At zero differential input (\( V_{in1} - V_{in2} = 0 \)), both \( V_X \) and \( V_Y \) are at the common-mode level \( V_{CC} - R_C I_{EE} / 2 \).
- The graph shows that the output voltages \( V_X \) and \( V_Y \) diverge from this common-mode level as the differential input increases or decreases.

5. **Annotations and Specific Data Points:**
- The graph is annotated with \( V_{CC} \) and \( V_{CC} - R_C I_{EE} \) to indicate the asymptotic behavior of \( V_X \) and \( V_Y \) respectively.
- The intersection point at zero differential input is marked, indicating the common-mode output level.

Figure 10.10 Variation of (a) collector currents and (b) output voltages as a function of input.
are differential, we can define a common-mode level for them. Given by $V_{C C}-R_{C} I_{E E} / 2$, this quantity is called the "output CM level."

| Example | A bipolar differential pair employs a tail current of 0.5 mA and a collector resistance <br> of $1 \mathrm{k} \Omega$. What is the maximum allowable base voltage if the differential input is large <br> enough to completely steer the tail current? Assume $V_{C C}=2.5 \mathrm{~V}$. |
| :---: | :--- |
| Solution | If $I_{E E}$ is completely steered, the transistor carrying the current lowers its collector voltage <br> to $V_{C C}-R_{C} I_{E E}=2 \mathrm{~V}$. Thus, the base voltage must remain below this value so as to avoid <br> saturation. |

Exercise Repeat the above example if the tail current is raised to 1 mA .

In the last step of our qualitative analysis, we "zoom in" around $V_{i n 1}-V_{i n 2}=0$ (the equilibrium condition) and study the circuit's behavior for a small input difference. As illustrated in Fig. 10.11(a), the base voltage of $Q_{1}$ is raised from $V_{C M}$ by $\Delta V$ while that of $Q_{2}$ is lowered from $V_{C M}$ by the same amount. We surmise that $I_{C 1}$ increases slightly and, since $I_{C 1}+I_{C 2}=I_{E E}, I_{C 2}$ decreases by the same amount:

$$
\begin{align*}
& I_{C 1}=\frac{I_{E E}}{2}+\Delta I  \tag{10.27}\\
& I_{C 2}=\frac{I_{E E}}{2}-\Delta I \tag{10.28}
\end{align*}
$$

How is $\Delta I$ related to $\Delta V$ ? If the emitters of $Q_{1}$ and $Q_{2}$ were directly tied to ground, then $\Delta I$ would simply be equal to $g_{m} \Delta V$. In the differential pair, however, node $P$ is free to rise or fall. We must therefore compute the change in $V_{P}$.

Suppose, as shown in Fig. 10.11(b), $V_{P}$ rises by $\Delta V_{P}$. As a result, the net increase in $V_{B E 1}$ is equal to $\Delta V-\Delta V_{P}$ and hence

$$
\begin{equation*}
\Delta I_{C 1}=g_{m}\left(\Delta V-\Delta V_{P}\right) \tag{10.29}
\end{equation*}
$$

Similarly, the net decrease in $V_{B E 2}$ is equal to $\Delta V+\Delta V_{P}$, yielding

$$
\begin{equation*}
\Delta I_{C 2}=-g_{m}\left(\Delta V+\Delta V_{P}\right) \tag{10.30}
\end{equation*}
$$

image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: X, B: VCM_plus, E: P}
name: Q2, type: NPN, ports: {C: Y, B: VCM_minus, E: P}
name: RC1, type: Resistor, value: RC, ports: {N1: VCC, N2: X}
name: RC2, type: Resistor, value: RC, ports: {N1: VCC, N2: Y}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential pair with transistors Q1 and Q2. It senses small differential input changes at nodes X and Y. The current source IEE provides biasing, and resistors RC set the load for the transistors. The input voltage is split into VCM + ΔV and VCM - ΔV at the bases of Q1 and Q2, respectively.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: X, B: VCM+ΔV, E: P}
name: Q2, type: NPN, ports: {C: Y, B: VCM-ΔV, E: P}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential pair with a current source IEE providing tail current. The transistors Q1 and Q2 form the differential pair, with their emitters connected to the current source. The resistors RC are connected to the collectors of Q1 and Q2, and VCC is the supply voltage. The input differential voltage is applied across the bases of Q1 and Q2, with a hypothetical change ΔVP at node P.

Figure 10.11 (a) Differential pair sensing small, differential input changes, (b) hypothetical change at $P$.

But recall from Eqs. (10.27) and (10.28) that $\Delta I_{C 1}$ must be equal to $-\Delta I_{C 2}$, dictating that

$$
\begin{equation*}
g_{m}\left(\Delta V-\Delta V_{P}\right)=g_{m}\left(\Delta V+\Delta V_{P}\right) \tag{10.31}
\end{equation*}
$$

and hence

$$
\begin{equation*}
\Delta V_{P}=0 . \tag{10.32}
\end{equation*}
$$

Interestingly, the tail voltage remains constant if the two inputs vary differentially and by a small amount-an observation critical to the small-signal analysis of the circuit.

The reader may wonder why Eq. (10.32) does not hold if $\Delta V$ is large. Which one of the above equations is violated? For a large differential input, $Q_{1}$ and $Q_{2}$ carry significantly different currents, thus exhibiting unequal transconductances and prohibiting the omission of $g_{m}$ 's from the two sides of Eq. (10.31).

With $\Delta V_{P}=0$ in Fig. 10.11(a), we can rewrite Eqs. (10.29) and (10.30) respectively as

$$
\begin{align*}
& \Delta I_{C 1}=g_{m} \Delta V  \tag{10.33}\\
& \Delta I_{C 2}=-g_{m} \Delta V \tag{10.34}
\end{align*}
$$

and

$$
\begin{align*}
\Delta V_{X} & =-g_{m} \Delta V R_{C}  \tag{10.35}\\
\Delta V_{Y} & =g_{m} \Delta V R_{C} . \tag{10.36}
\end{align*}
$$

The differential output therefore goes from 0 to

$$
\begin{equation*}
\Delta V_{X}-\Delta V_{Y}=-2 g_{m} \Delta V R_{C} \tag{10.37}
\end{equation*}
$$

We define the small-signal differential gain of the circuit as

$$
\begin{align*}
A_{v} & =\frac{\text { Change in Differential Output }}{\text { Change in Differential Input }}  \tag{10.38}\\
& =\frac{-2 g_{m} \Delta V R_{C}}{2 \Delta V}  \tag{10.39}\\
& =-g_{m} R_{C} \tag{10.40}
\end{align*}
$$

(Note that the change in the differential input is equal to $2 \Delta V$.) This expression is similar to that of the common-emitter stage.

Example Design a bipolar differential pair for a gain of 10 and a power budget of 1 mW with a
10.6 supply voltage of 2 V .

Solution With $V_{C C}=2 \mathrm{~V}$, the power budget translates to a tail current of 0.5 mA . Each transistor thus carries a current of 0.25 mA near equilibrium, providing a transconductance of $0.25 \mathrm{~mA} / 26 \mathrm{mV}=(104 \Omega)^{-1}$. It follows that

$$
\begin{align*}
R_{C} & =\frac{\left|A_{v}\right|}{g_{m}}  \tag{10.41}\\
& =1040 \Omega . \tag{10.42}
\end{align*}
$$

Exercise Redesign the circuit for a power budget of 0.5 mW and compare the results.

Example Compare the power dissipation of a bipolar differential pair with that of a CE stage <br> 10.7 if both circuits are designed for equal voltage gains, collector resistances, and supply voltages.

Solution The gain of the differential pair is written from Eq. (10.40) as

$$
\begin{equation*}
\left|A_{V, \mathrm{diff}}\right|=g_{m 1,2} R_{C} \tag{10.43}
\end{equation*}
$$

where $g_{m 1,2}$ denotes the transconductance of each of the two transistors. For a CE stage

$$
\begin{equation*}
\left|A_{V, C E}\right|=g_{m} R_{C} \tag{10.44}
\end{equation*}
$$

Thus,

$$
\begin{equation*}
g_{m 1,2} R_{C}=g_{m} R_{C} \tag{10.45}
\end{equation*}
$$

and hence

$$
\begin{equation*}
\frac{I_{E E}}{2 V_{T}}=\frac{I_{C}}{V_{T}} \tag{10.46}
\end{equation*}
$$

where $I_{E E} / 2$ is the bias current of each transistor in the differential pair, and $I_{C}$ represents the bias current of the CE stage. In other words,

$$
\begin{equation*}
I_{E E}=2 I_{C} \tag{10.47}
\end{equation*}
$$

indicating that the differential pair consumes twice as much power. This is one of the drawbacks of differential circuits.

Exercise
If both circuits are designed for the same power budget, equal collector resistances, and equal supply voltages, compare their voltage gains.

### 10.2.2 Large-Signal Analysis

Having obtained insight into the operation of the bipolar differential pair, we now quantify its large-signal behavior, aiming to formulate the input/output characteristic of the circuit (the sketches in Fig. 10.10). Not having seen any large-signal analysis in the previous chapters, the reader may naturally wonder why we are suddenly interested in this aspect of the differential pair. Our interest arises from (a) the need to understand the circuit's limitations in serving as a linear amplifier, and (b) the application of the differential pair as a (nonlinear) current-steering circuit.

In order to derive the relationship between the differential input and output of the circuit, we first note from Fig. 10.12 that

$$
\begin{align*}
& V_{\text {out } 1}=V_{C C}-R_{C} I_{C 1}  \tag{10.48}\\
& V_{\text {out } 2}=V_{C C}-R_{C} I_{C 2} \tag{10.49}
\end{align*}
$$

and hence

$$
\begin{align*}
V_{\text {out }} & =V_{\text {out } 1}-V_{\text {out } 2}  \tag{10.50}\\
& =-R_{C}\left(I_{C 1}-I_{C 2}\right) \tag{10.51}
\end{align*}
$$

We must therefore compute $I_{C 1}$ and $I_{C 2}$ in terms of the input difference. Assuming $\alpha=1$ and $V_{A}=\infty$, and recalling from Chapter 4 that $V_{B E}=V_{T} \ln \left(I_{C} / I_{S}\right)$, we write a KVL around
image_name:Figure 10.12 Bipolar differential pair for large-signal analysis
description:
[
name: Q1, type: NPN, ports: {C: Vout1, B: Vin1, E: P}
name: Q2, type: NPN, ports: {C: Vout2, B: Vin2, E: P}
name: RC1, type: Resistor, value: RC, ports: {N1: Vout1, N2: VCC}
name: RC2, type: Resistor, value: RC, ports: {N1: Vout2, N2: VCC}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a bipolar differential pair for large-signal analysis, with two NPN transistors (Q1 and Q2) sharing a common emitter node connected to a current source IEE. The collectors of Q1 and Q2 are connected to VCC through resistors RC. The inputs are Vin1 and Vin2, and the outputs are Vout1 and Vout2.

Figure 10.12 Bipolar differential pair for large-signal analysis.
the input network,

$$
\begin{equation*}
V_{i n 1}-V_{B E 1}=V_{P}=V_{i n 2}-V_{B E 2} \tag{10.52}
\end{equation*}
$$

obtaining

$$
\begin{align*}
V_{i n 1}-V_{i n 2} & =V_{B E 1}-V_{B E 2}  \tag{10.53}\\
& =V_{T} \ln \frac{I_{C 1}}{I_{S 1}}-V_{T} \ln \frac{I_{C 2}}{I_{S 2}}  \tag{10.54}\\
& =V_{T} \ln \frac{I_{C 1}}{I_{C 2}} \tag{10.55}
\end{align*}
$$

Also, a KCL at node $P$ gives

$$
\begin{equation*}
I_{C 1}+I_{C 2}=I_{E E} \tag{10.56}
\end{equation*}
$$

Equations (10.55) and (10.56) contain two unknowns. Substituting for $I_{C 1}$ from Eq. (10.55) in Eq. (10.56) yields

$$
\begin{equation*}
I_{C 2} \exp \frac{V_{i n 1}-V_{i n 2}}{V_{T}}+I_{C 2}=I_{E E} \tag{10.57}
\end{equation*}
$$

and, therefore,

$$
\begin{equation*}
I_{C 2}=\frac{I_{E E}}{1+\exp \frac{V_{i n 1}-V_{i n 2}}{V_{T}}} \tag{10.58}
\end{equation*}
$$

The symmetry of the circuit with respect to $V_{i n 1}$ and $V_{i n 2}$ and with respect to $I_{C 1}$ and $I_{C 2}$ suggests that $I_{C 1}$ exhibits the same behavior as Eq. (10.58) but with the roles of $V_{i n 1}$ and $V_{i n 2}$ exchanged:

$$
\begin{align*}
I_{C 1} & =\frac{I_{E E}}{1+\exp \frac{V_{i n 2}-V_{i n 1}}{V_{T}}}  \tag{10.59}\\
& =\frac{I_{E E} \exp \frac{V_{i n 1}-V_{i n 2}}{V_{T}}}{1+\exp \frac{V_{i n 1}-V_{i n 2}}{V_{T}}} \tag{10.60}
\end{align*}
$$

Alternatively, the reader can substitute for $I_{C 2}$ from Eq. (10.58) in Eq. (10.56) to obtain $I_{C 1}$.

[^0]:    ${ }^{6}$ The reader can show that placing $V_{o s}$ in series with the inverting input of the op amp yields the same result.

[^1]:    ${ }^{7}$ Recall that in a linear system, if $x(t) \rightarrow y(t)$, then $2 x(t) \rightarrow 2 y(t)$.

[^2]:    ${ }^{8} \mathrm{Op}$ amps employing MOS transistors at their input exhibit a very high input impedance at low frequencies.

[^3]:    ${ }^{1}$ Coined in the vacuum-tube era, the term "cascode" is believed to be an abbreviation of "cascaded triodes."

[^4]:    ${ }^{3}$ In integrated circuits, all bipolar transistors fabricated on the same wafer exhibit the same Early voltage. This example applies to discrete implementations.

[^5]:    ${ }^{4}$ In reality, other second-order effects limit the output impedance of MOS cascodes.

[^6]:    ${ }^{5}$ While omitted for simplicity in Chapters 4 and 6, the condition $v_{\text {out }}=0$ is also required for the transconductance of transistors. That is, the collector or drain must by shorted to ac ground.

[^7]:    ${ }^{6}$ In deep-submicron CMOS technologies, the gate oxide thickness is reduced to less than $30 \AA$, leading to "tunneling" and hence noticeable gate current. This effect is beyond the scope of this book.

[^8]:    ${ }^{1}$ Also called the "emitter-coupled pair" or the "long-tailed pair."

[^9]:    Exercise What value of $R_{C}$ allows the input CM level to approach $V_{C C}$ if the transistors can tolerate a base-collector forward bias of 400 mV ?

Equations (10.58) and (10.60) play a crucial role in our quantitative understanding of the differential pair's operation. In particular, if $V_{i n 1}-V_{i n 2}$ is very negative, then $\exp \left(V_{i n 1}-V_{i n 2}\right) / V_{T} \rightarrow 0$ and

$$
\begin{align*}
I_{C 1} & \rightarrow 0  \tag{10.61}\\
I_{C 2} & \rightarrow I_{E E} \tag{10.62}
\end{align*}
$$

as predicted by our qualitative analysis [Fig.10.9(b)]. Similarly, if $V_{i n 1}-V_{i n 2}$ is very positive, $\exp \left(V_{i n 1}-V_{i n 2}\right) / V_{T} \rightarrow \infty$ and

$$
\begin{align*}
I_{C 1} \rightarrow I_{E E}  \tag{10.63}\\
I_{C 2} \rightarrow 0 \tag{10.64}
\end{align*}
$$

What is meant by "very" negative or positive? For example, can we say $I_{C 1} \approx 0$ and $I_{C 2} \approx I_{E E}$ if $V_{i n 1}-V_{i n 2}=-10 V_{T}$ ? Since $\exp (-10) \approx 4.54 \times 10^{-5}$,

$$
\begin{align*}
I_{C 1} & \approx \frac{I_{E E} \times 4.54 \times 10^{-5}}{1+4.54 \times 10^{-5}}  \tag{10.65}\\
& \approx 4.54 \times 10^{-5} I_{E E} \tag{10.66}
\end{align*}
$$

and

$$
\begin{align*}
I_{C 2} & \approx \frac{I_{E E}}{1+4.54 \times 10^{-5}}  \tag{10.67}\\
& \approx I_{E E}\left(1-4.54 \times 10^{-5}\right) \tag{10.68}
\end{align*}
$$

In other words, $Q_{1}$ carries only $0.0045 \%$ of the tail current; and $I_{E E}$ can be considered steered completely to $Q_{2}$.

| Example $10.8$ | Determine the differential input voltage that steers $98 \%$ of the tail current to one transistor. |
| :---: | :---: |
| Solution | We require that |
|  | $I_{C 1}=0.02 I_{E E}$ |
|  | $\begin{equation*} \approx I_{E E} \exp \frac{V_{i n 1}-V_{i n 2}}{V_{T}} \tag{10.70} \end{equation*}$ |
|  | and hence |
|  | $V_{i n 1}-V_{i n 2} \approx-3.91 V_{T}$ |
|  | We often say a differential input of $4 V_{T}$ is sufficient to turn one side of the bipolar pair nearly off. Note that this value remains independent of $I_{E E}$ and $I_{S}$. |

Exercise What differential input is necessary to steer $90 \%$ of the tail current?

For the output voltages in Fig. 10.12, we have

$$
\begin{align*}
V_{\text {out } 1} & =V_{C C}-R_{C} I_{C 1}  \tag{10.72}\\
& =V_{C C}-R_{C} \frac{I_{E E} \exp \frac{V_{i n 1}-V_{\text {in } 2}}{V_{T}}}{1+\exp \frac{V_{i n 1}-V_{i n 2}}{V_{T}}} \tag{10.73}
\end{align*}
$$

and

$$
\begin{align*}
V_{\text {out } 2} & =V_{C C}-R_{C} I_{C 2}  \tag{10.74}\\
& =V_{C C}-R_{C} \frac{I_{E E}}{1+\exp \frac{V_{\text {in } 1}-V_{\text {in } 2}}{V_{T}}} \tag{10.75}
\end{align*}
$$

Of particular importance is the output differential voltage:

$$
\begin{align*}
V_{\text {out } 1}-V_{\text {out } 2} & =-R_{C}\left(I_{C 1}-I_{C 2}\right)  \tag{10.76}\\
& =R_{C} I_{E E} \frac{1-\exp \frac{V_{i n 1}-V_{\text {in } 2}}{V_{T}}}{1+\exp \frac{V_{i n 1}-V_{\text {in } 2}}{V_{T}}}  \tag{10.77}\\
& =-R_{C} I_{E E} \tanh \frac{V_{\text {in } 1}-V_{\text {in } 2}}{2 V_{T}} \tag{10.78}
\end{align*}
$$

Figure 10.13 summarizes the results, indicating that the differential output voltage begins from a "saturated" value of $+R_{C} I_{E E}$ for a very negative differential input, gradually becomes a linear function of $V_{i n 1}-V_{i n 2}$ for relatively small values of $\left|V_{i n 1}-V_{i n 2}\right|$, and reaches a saturated level of $-R_{C} I_{E E}$ as $V_{i n 1}-V_{i n 2}$ becomes very positive. From Example 10.8, we recognize that even a differential input of $4 V_{T} \approx 104 \mathrm{mV}$ "switches" the differential pair, thereby concluding that $\left|V_{i n 1}-V_{i n 2}\right|$ must remain well below this value for linear operation.
image_name:I_C1, I_C2 vs V_in1 - V_in2
description:The graph consists of three separate plots, each illustrating a different relationship between currents, voltages, and the differential input voltage $V_{in1} - V_{in2}$ in a bipolar differential pair circuit.

1. **Top Plot: $I_{C1}$ and $I_{C2}$ vs $V_{in1} - V_{in2}$**
- **Type of Graph:** This is a current versus differential voltage plot.
- **Axes Labels and Units:**
- Horizontal axis: $V_{in1} - V_{in2}$ (unitless or volts)
- Vertical axis: Collector currents $I_{C1}$ and $I_{C2}$ (amperes)
- **Overall Behavior and Trends:**
- The graph shows two curves representing the collector currents $I_{C1}$ and $I_{C2}$.
- As $V_{in1} - V_{in2}$ increases from negative to positive, $I_{C1}$ starts from zero and increases towards $I_{EE}$, while $I_{C2}$ decreases from $I_{EE}$ to zero.
- The currents are symmetric about the vertical axis at $V_{in1} - V_{in2} = 0$.
- **Key Features and Technical Details:**
- At $V_{in1} - V_{in2} = 0$, both $I_{C1}$ and $I_{C2}$ are equal to $\frac{I_{EE}}{2}$.

2. **Middle Plot: $V_{out1}$ and $V_{out2}$ vs $V_{in1} - V_{in2}$**
- **Type of Graph:** This is a voltage versus differential voltage plot.
- **Axes Labels and Units:**
- Horizontal axis: $V_{in1} - V_{in2}$ (unitless or volts)
- Vertical axis: Output voltages $V_{out1}$ and $V_{out2}$ (volts)
- **Overall Behavior and Trends:**
- The graph shows two curves representing the output voltages $V_{out1}$ and $V_{out2}$.
- As $V_{in1} - V_{in2}$ increases, $V_{out1}$ decreases from $V_{CC}$ to $V_{CC} - R_C I_{EE}$, while $V_{out2}$ increases from $V_{CC} - R_C I_{EE}$ to $V_{CC}$.
- The voltages are symmetric about the vertical axis at $V_{in1} - V_{in2} = 0$.
- **Key Features and Technical Details:**
- At $V_{in1} - V_{in2} = 0$, both $V_{out1}$ and $V_{out2}$ are equal to $V_{CC} - \frac{R_C I_{EE}}{2}$.

3. **Bottom Plot: $V_{out1} - V_{out2}$ vs $V_{in1} - V_{in2}$**
- **Type of Graph:** This is a differential output voltage versus differential input voltage plot.
- **Axes Labels and Units:**
- Horizontal axis: $V_{in1} - V_{in2}$ (unitless or volts)
- Vertical axis: Differential output voltage $V_{out1} - V_{out2}$ (volts)
- **Overall Behavior and Trends:**
- The graph shows a single curve representing the difference between the two output voltages.
- As $V_{in1} - V_{in2}$ increases, $V_{out1} - V_{out2}$ decreases from $+R_C I_{EE}$ to $-R_C I_{EE}$.
- The curve is linear around $V_{in1} - V_{in2} = 0$ and saturates at the positive and negative extremes.
- **Key Features and Technical Details:**
- At $V_{in1} - V_{in2} = 0$, $V_{out1} - V_{out2}$ is zero, indicating a balanced state.
image_name:V_out1, V_out2 vs V_in1 - V_in2
description:The graph consists of three plots illustrating the behavior of currents and voltages in a bipolar differential pair as a function of the differential input \( V_{in1} - V_{in2} \).

1. **Top Plot: Currents \( I_{C1} \) and \( I_{C2} \)**
- **Axes:**
- **X-axis:** Represents \( V_{in1} - V_{in2} \), the differential input voltage.
- **Y-axis:** Represents the collector currents \( I_{C1} \) and \( I_{C2} \).
- **Behavior:**
- As \( V_{in1} - V_{in2} \) increases from negative to positive, \( I_{C1} \) decreases from \( I_{EE} \) to zero, while \( I_{C2} \) increases from zero to \( I_{EE} \).
- The currents cross at \( I_{EE}/2 \) when \( V_{in1} - V_{in2} = 0 \).

2. **Middle Plot: Voltages \( V_{out1} \) and \( V_{out2} \)**
- **Axes:**
- **X-axis:** Represents \( V_{in1} - V_{in2} \).
- **Y-axis:** Represents the output voltages \( V_{out1} \) and \( V_{out2} \).
- **Behavior:**
- As \( V_{in1} - V_{in2} \) increases, \( V_{out1} \) decreases from \( V_{CC} \) to \( V_{CC} - R_C I_{EE} \), while \( V_{out2} \) increases from \( V_{CC} - R_C I_{EE} \) to \( V_{CC} \).
- The voltages cross at \( V_{CC} - R_C I_{EE}/2 \) when \( V_{in1} - V_{in2} = 0 \).

3. **Bottom Plot: Differential Output Voltage \( V_{out1} - V_{out2} \)**
- **Axes:**
- **X-axis:** Represents \( V_{in1} - V_{in2} \).
- **Y-axis:** Represents the differential output voltage \( V_{out1} - V_{out2} \).
- **Behavior:**
- The differential output voltage decreases linearly from \( +R_C I_{EE} \) to \( -R_C I_{EE} \) as \( V_{in1} - V_{in2} \) increases.
- The curve crosses the zero line when \( V_{in1} - V_{in2} = 0 \).

Overall, the plots demonstrate the linear and saturating behavior of the bipolar differential pair as the differential input voltage varies. The transition from linear to saturation occurs as the differential input becomes large, consistent with the theoretical explanation provided in the context.
image_name:V_out1 - V_out2 vs V_in1 - V_in2
description:The graph titled "V_out1 - V_out2 vs V_in1 - V_in2" consists of three sub-plots that illustrate the behavior of a bipolar differential pair circuit in response to differential input voltages.

1. **Top Sub-Plot: Currents I_C1 and I_C2 vs V_in1 - V_in2**
- **Axes:**
- Horizontal Axis: $V_{in1} - V_{in2}$
- Vertical Axis: Currents $I_{C1}$ and $I_{C2}$
- **Behavior:**
- The plot shows two crossing curves, where $I_{C1}$ increases and $I_{C2}$ decreases as $V_{in1} - V_{in2}$ increases from negative to positive.
- Both currents are equal to $\frac{I_{EE}}{2}$ at $V_{in1} - V_{in2} = 0$.
- As $V_{in1} - V_{in2}$ becomes very positive, $I_{C1}$ approaches $I_{EE}$, and $I_{C2}$ approaches zero.
- Conversely, for very negative $V_{in1} - V_{in2}$, $I_{C1}$ approaches zero, and $I_{C2}$ approaches $I_{EE}$.

2. **Middle Sub-Plot: Voltages V_out1 and V_out2 vs V_in1 - V_in2**
- **Axes:**
- Horizontal Axis: $V_{in1} - V_{in2}$
- Vertical Axis: Output Voltages $V_{out1}$ and $V_{out2}$
- **Behavior:**
- The plot shows two crossing curves, similar to the current plot.
- $V_{out1}$ increases and $V_{out2}$ decreases as $V_{in1} - V_{in2}$ increases from negative to positive.
- At $V_{in1} - V_{in2} = 0$, both voltages are at $V_{CC} - R_C \frac{I_{EE}}{2}$.
- For very positive $V_{in1} - V_{in2}$, $V_{out1}$ approaches $V_{CC}$, and $V_{out2}$ approaches $V_{CC} - R_C I_{EE}$.
- For very negative $V_{in1} - V_{in2}$, $V_{out1}$ approaches $V_{CC} - R_C I_{EE}$, and $V_{out2}$ approaches $V_{CC}$.

3. **Bottom Sub-Plot: Differential Output Voltage V_out1 - V_out2 vs V_in1 - V_in2**
- **Axes:**
- Horizontal Axis: $V_{in1} - V_{in2}$
- Vertical Axis: Differential Output Voltage $V_{out1} - V_{out2}$
- **Behavior:**
- The plot shows a smooth transition from negative to positive values as $V_{in1} - V_{in2}$ increases.
- At $V_{in1} - V_{in2} = 0$, the differential output voltage is zero.
- The differential output voltage saturates at $+R_C I_{EE}$ for very positive $V_{in1} - V_{in2}$ and at $-R_C I_{EE}$ for very negative $V_{in1} - V_{in2}$.

Overall, the graph illustrates the linear region and saturation behavior of the bipolar differential pair, showing how the differential input voltage affects the collector currents and output voltages, with clear linear and saturation regions.

Figure 10.13 Variation of currents and voltages as a function of input.

Sketch the output waveforms of the bipolar differential pair in Fig. 10.14(a) in response to the sinusoidal inputs shown in Figs. 10.14(b) and (c). Assume $Q_{1}$ and $Q_{2}$ remain in the forward active region.

Solution For the sinusoids depicted in Fig. 10.14(b), the circuit operates linearly because the maximum differential input is equal to $\pm 2 \mathrm{mV}$. The outputs are therefore sinusoids having a peak amplitude of $1 \mathrm{mV} \times g_{m} R_{C}$ [Fig.10.14(d)]. On the other hand, the sinusoids in Fig. 10.14(c) force a maximum input difference of $\pm 200 \mathrm{mV}$, turning $Q_{1}$ or $Q_{2}$ off. For example, as $V_{\text {in } 1}$ approaches 50 mV above $V_{C M}$ and $V_{i n 2}$ reaches 50 mV below $V_{C M}$ (at $t=t_{1}$ ), $Q_{1}$ absorbs most of the tail current, thus producing

$$
\begin{align*}
& V_{\text {out } 1} \approx V_{C C}-R_{C} I_{E E}  \tag{10.79}\\
& V_{\text {out } 2} \approx V_{C C} . \tag{10.80}
\end{align*}
$$

Thereafter, the outputs remain saturated until $\left|V_{i n 1}-V_{i n 2}\right|$ falls to less than 100 mV . The result is sketched in Fig. 10.14(e). We say the circuit operates as a "limiter" in this case, playing a role similar to the diode limiters studied in Chapter 3.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: Vout1, B: Vin1, E: P}
name: Q2, type: NPN, ports: {C: Vout2, B: Vin2, E: P}
name: RC1, type: Resistor, value: RC, ports: {N1: Vout1, N2: VCC}
name: RC2, type: Resistor, value: RC, ports: {N1: Vout2, N2: VCC}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: P, Nn: GND}
]
extrainfo:This circuit is a differential amplifier with two NPN transistors (Q1 and Q2), two resistors (RC), and a current source (IEE). The outputs are Vout1 and Vout2, with inputs Vin1 and Vin2. The circuit operates as a limiter, with outputs remaining saturated until the input difference falls below 100 mV.

(a)
image_name:(a)
description:The graph in figure (a) is a time-domain waveform illustrating the behavior of two input voltages, \( V_{in1} \) and \( V_{in2} \), over time \( t \). The horizontal axis represents time, while the vertical axis indicates voltage levels. Both input voltages oscillate sinusoidally around a common-mode voltage \( V_{CM} \), which is depicted as a dashed horizontal line.

The amplitude of the oscillations for both \( V_{in1} \) and \( V_{in2} \) is 1 mV, as indicated by the vertical arrows. \( V_{in1} \) and \( V_{in2} \) are shown to be 180 degrees out of phase with each other, signifying that when one voltage reaches its peak, the other is at its trough.

This waveform is characteristic of a differential input to a differential amplifier, where the difference between the two input signals is amplified while the common-mode voltage remains unchanged. The graph effectively demonstrates the small-signal behavior of the differential amplifier's inputs, aligning with the circuit's operation as a limiter when the input difference is below 100 mV.

(b)
image_name:(b)
description:The graph labeled as (b) is a time-domain waveform illustrating the output voltages of a differential amplifier. The x-axis represents time (t), while the y-axis represents voltage. The graph shows two sinusoidal waveforms labeled \( V_{out1} \) and \( V_{out2} \), which are out of phase with each other. The waveforms are centered around a common-mode voltage \( V_{CM} \).

The amplitude of each waveform is indicated as \( 1 \text{ mV} \times g_m R_C \), where \( g_m \) is the transconductance and \( R_C \) is the load resistance. This suggests that the amplitude of the output voltage is determined by the product of the transconductance and load resistance, scaled by the input signal amplitude of 1 mV.

The waveforms exhibit a characteristic behavior of differential signals, where one signal reaches its peak while the other reaches its trough, maintaining a constant difference between them. This behavior is typical for differential amplifiers, which amplify the difference between two input signals while rejecting any common-mode signals.

The graph effectively demonstrates the small-signal behavior of the differential amplifier's outputs, aligning with the circuit's operation as a limiter when the input difference is below a certain threshold. The periodic nature of the waveforms indicates a continuous oscillation, and the symmetry around \( V_{CM} \) highlights the differential nature of the outputs.

(d)
image_name:(d)
description:The graph labeled "(d)" represents a time-domain waveform of a differential amplifier's input signals. The x-axis is labeled as time \( t \), and the y-axis represents voltage, although it is not explicitly labeled, the context suggests it is in millivolts (mV). The graph shows two sinusoidal waveforms, \( V_{in1} \) and \( V_{in2} \), which are offset from each other in phase.

The central horizontal dashed line is labeled \( V_{CM} \), indicating the common-mode voltage level around which the differential signals oscillate. The amplitude of the waveforms is marked as 100 mV, suggesting that each waveform reaches a peak of 100 mV above and below the \( V_{CM} \) level.

The waveforms are periodic and symmetric about the \( V_{CM} \) line, which is characteristic of differential signals. The time \( t_1 \) is marked on the x-axis, indicating a specific moment in time, possibly where the analysis or measurement begins.

Overall, the graph illustrates the behavior of the differential amplifier under small-signal conditions, showing how the input signals \( V_{in1} \) and \( V_{in2} \) vary over time and their relationship to the common-mode voltage \( V_{CM} \). The periodic nature and symmetry of the waveforms highlight the differential nature of the amplifier's operation.

(c)
image_name:(c)
description:The graph labeled as "(c)" illustrates the behavior of a differential amplifier under small-signal conditions, focusing on the output voltages \( V_{out1} \) and \( V_{out2} \) over time. The x-axis is labeled "\( t \)" and represents time, with a specific moment marked as \( t_1 \). The y-axis represents voltage levels, with key reference voltages indicated: \( V_{CC} \), \( V_{CC} - R_C \frac{I_{EE}}{2} \), and \( V_{CC} - R_C I_{EE} \).

The graph shows two periodic waveforms, \( V_{out1} \) and \( V_{out2} \), that are 180 degrees out of phase, highlighting the differential nature of the amplifier. These waveforms are symmetrical and exhibit a square wave pattern, which is characteristic of the output behavior when the amplifier is driven by a differential input.

The waveform \( V_{out2} \) peaks at the voltage level \( V_{CC} \) and reaches its minimum at \( V_{CC} - R_C I_{EE} \). Conversely, \( V_{out1} \) reaches its peak at \( V_{CC} - R_C I_{EE} \) and its minimum at \( V_{CC} - R_C \frac{I_{EE}}{2} \), showing the complementary relationship between the two outputs.

The periodicity and symmetry of the waveforms suggest that the amplifier is operating in its linear region under small-signal conditions, with the outputs swinging between the specified voltage levels. This behavior is typical of a differential amplifier responding to small differential input signals, maintaining a constant common-mode voltage \( V_{CM} \).

(e)

Figure 10.14

Exercise
What happens to the above results if the tail current is halved?

Did you know?

Differential pairs can operate as limiters if their input difference is large. In this case, they "clip" the top and bottom of the signal waveform. Of course, limiting a signal such as your voice creates distortion and is undesirable. However, limiting proves useful in some applications. A common example is in FM radios, where the RF waveform ideally contains only frequency modulation [Fig. (a)], but in practice incurs some noise [Fig. (b)]. A limiter removes the noise on the amplitude, improving the signal quality.
image_name:(a)
description:The graph labeled as "(a)" represents an ideal FM waveform. This is a time-domain waveform, characterized by a smooth, continuous sinusoidal shape. The x-axis likely represents time, although specific units are not provided, while the y-axis represents amplitude. The waveform exhibits a consistent frequency modulation without any distortion or noise, maintaining a uniform amplitude throughout.

In contrast, the graph labeled "(b)" shows a noisy FM waveform. Here, the sinusoidal shape is distorted by irregularities and fluctuations, indicating the presence of noise affecting the amplitude. This noise disrupts the smooth pattern seen in the ideal waveform.

The graph labeled "(c)" illustrates a clipped noisy FM waveform. This waveform has undergone a limiting process where the peaks and troughs are flattened or "clipped," reducing the amplitude variations caused by noise. While the clipping reduces noise, it also alters the original sinusoidal shape, leading to a more rectangular waveform appearance. This modification helps in improving signal quality by removing amplitude noise, although it may introduce some distortion.
image_name:(b)
description:The graph labeled "(b)" is titled "Noisy FM Waveform". It is a time-domain waveform graph illustrating the effect of noise on a frequency-modulated (FM) signal.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform, showing how the amplitude of the signal varies over time.

2. **Axes Labels and Units:**
- The x-axis likely represents time, although it is not explicitly labeled in the image. The units of time are not specified.
- The y-axis represents amplitude, but again, there are no specific units or scale markings provided.

3. **Overall Behavior and Trends:**
- The waveform displays periodic oscillations characteristic of FM signals but is visibly distorted by noise.
- The peaks and troughs of the waveform are irregular, indicating the presence of noise superimposed on the signal.
- Unlike a clean sinusoidal waveform, this one shows erratic fluctuations in amplitude.

4. **Key Features and Technical Details:**
- The waveform exhibits a jagged appearance, with sharp, uneven peaks and valleys.
- There are no clear inflection points or zero crossings due to the noise distortion.
- The signal does not maintain a constant amplitude, reflecting the noise interference.

5. **Annotations and Specific Data Points:**
- There are no specific numerical annotations or markers on the graph.
- The graph visually contrasts with the ideal FM waveform (a) and the clipped noisy FM waveform (c) shown in the accompanying images, highlighting the effect of noise before and after clipping.
image_name:(c)
description:The graph labeled (c) is a time-domain waveform showing a "Clipped Noisy FM Waveform." This waveform is the result of applying a limiter to a noisy FM signal, as depicted in the preceding graph (b).

**Type of Graph and Function:**
- The graph is a time-domain waveform representation of a frequency-modulated (FM) signal that has undergone clipping.

**Axes Labels and Units:**
- The horizontal axis likely represents time, though no specific units are provided. The vertical axis represents amplitude, again without specific units.

**Overall Behavior and Trends:**
- The waveform exhibits a series of periodic oscillations, similar in frequency to the ideal FM waveform but with a distinct difference in amplitude behavior.
- The tops and bottoms of the waveform are flat, indicating that the signal has been clipped, which removes amplitude variations that represent noise.

**Key Features and Technical Details:**
- The clipping process has removed the peaks and troughs of the noise, resulting in a more uniform amplitude across the waveform.
- The overall shape of the waveform is more rectangular compared to the ideal sinusoidal form, due to the clipping effect.

**Annotations and Specific Data Points:**
- The graph is labeled "Clipped Noisy FM Waveform," indicating the effect of the clipping process on the noisy FM signal.
- No specific numerical values or markers are present on the graph, but the visual representation clearly shows the effect of clipping on the waveform's amplitude.

Effect of clipping on FM waveform.

### 10.2.3 Small-Signal Analysis

Our brief investigation of the differential pair in Fig. 10.11 revealed that, for small differential inputs, the tail node maintains a constant voltage (and hence is called a "virtual ground"). We also obtained a voltage gain equal to $g_{m} R_{C}$. We now study the small-signal behavior of the circuit in greater detail. As explained in previous chapters, the definition of "small signals" is somewhat arbitrary, but the requirement is that the input signals not influence the bias currents of $Q_{1}$ and $Q_{2}$ appreciably. In other words, the two transistors must exhibit approximately equal transconductances-the same condition required for node $P$ to appear as virtual ground. In practice, an input difference of less than 10 mV is considered "small" for most applications.

Assuming perfect symmetry, an ideal tail current source, and $V_{A}=\infty$, we construct the small-signal model of the circuit as shown in Fig. 10.15(a). Here, $v_{i n 1}$ and $v_{i n 2}$ represent small changes in each input and must satisfy $v_{i n 1}=-v_{i n 2}$ for differential operation. Note that the tail current source is replaced with an open circuit. As with the foregoing largesignal analysis, let us write a KVL around the input network and a KCL at node $P$ :

$$
\begin{gather*}
v_{i n 1}-v_{\pi 1}=v_{P}=v_{i n 2}-v_{\pi 2}  \tag{10.81}\\
\frac{v_{\pi 1}}{r_{\pi 1}}+g_{m 1} v_{\pi 1}+\frac{v_{\pi 2}}{r_{\pi 2}}+g_{m 2} v_{\pi 2}=0 \tag{10.82}
\end{gather*}
$$

With $r_{\pi 1}=r_{\pi 2}$ and $g_{m 1}=g_{m 2}$, Eq. (10.82) yields

$$
\begin{equation*}
v_{\pi 1}=-v_{\pi 2} \tag{10.83}
\end{equation*}
$$

and since $v_{i n 1}=-v_{i n 2}$, Eq. (10.81) translates to

$$
\begin{equation*}
2 v_{i n 1}=2 v_{\pi 1} \tag{10.84}
\end{equation*}
$$

image_name:(a)
description:
[
name: vin1, type: VoltageSource, ports: {Np: Vin1, Nn: GND}
name: vin2, type: VoltageSource, ports: {Np: Vin2, Nn: GND}
name: r_π1, type: Resistor, value: r_π1, ports: {N1: Vin1, N2: P}
name: r_π2, type: Resistor, value: r_π2, ports: {N1: Vin2, N2: P}
name: R_C, type: Resistor, value: R_C, ports: {N1: GND, N2: X}
name: g_m1v_π1, type: VoltageControlledCurrentSource, value: g_m1v_π1, ports: {Np: GND, Nn: X}
name: g_m2v_π2, type: VoltageControlledCurrentSource, value: g_m2v_π2, ports: {Np: GND, Nn: Y}
]
extrainfo:Figure 10.15(a) represents a small-signal model of a bipolar pair. The node P is a virtual ground for differential small-signal inputs, simplifying the analysis. The circuit includes two NPN transistors, Q1 and Q2, with their collectors connected to ground and their emitters connected to the respective input voltages. The resistors r_π1 and r_π2 are connected to the bases of Q1 and Q2, respectively. The current sources g_m1v_π1 and g_m2v_π2 are controlled by the voltages across r_π1 and r_π2, respectively.
image_name:(b)
description:
[
name: vin1, type: VoltageSource, value: vin1, ports: {Np: Vin1, Nn: GND}
name: vin2, type: VoltageSource, value: vin2, ports: {Np: Vin2, Nn: GND}
name: rπ1, type: Resistor, value: rπ1, ports: {N1: Vin1, N2: GND}
name: rπ2, type: Resistor, value: rπ2, ports: {N1: Vin2, N2: GND}
name: RC, type: Resistor, value: RC, ports: {N1: GND, N2: P1}
name: RC, type: Resistor, value: RC, ports: {N1: GND, N2: P2}
name: g_m1v_π1, type: VoltageControlledCurrentSource, ports: {Np: P1, Nn: GND}
name: g_m2v_π2, type: VoltageControlledCurrentSource, ports: {Np: P2, Nn: GND}
]
extrainfo:This is a simplified small-signal model of a differential amplifier with two voltage sources vin1 and vin2, resistors rπ1, rπ2, and RC, and voltage-controlled current sources g_m1v_π1 and g_m2v_π2. Node P acts as a virtual ground for differential small-signal inputs.
image_name:(c)
description:
[
name: Vin1, type: VoltageSource, value: Vin1, ports: {Np: Vin1, Nn: GND}
name: Vin2, type: VoltageSource, value: Vin2, ports: {Np: Vin2, Nn: GND}
name: Q1, type: NPN, ports: {C: C1, B: Vin, E: GND}
name: Q2, type: NPN, ports: {C: C2, B: Vin2, E: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: C1}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: C2}
]
extrainfo:The circuit is a differential amplifier with two NPN transistors Q1 and Q2. It uses capacitors C1 and C2 for coupling and resistors RC for load. The circuit is designed for differential input signals Vin1 and Vin2, with a virtual ground at the base node B.

Figure 10.15 (a) Small-signal model of bipolar pair, (b) simplified small-signal model, (c) simplied diagram.

That is,

$$
\begin{align*}
v_{P} & =v_{i n 1}-v_{\pi 1}  \tag{10.85}\\
& =0 . \tag{10.86}
\end{align*}
$$

Thus, the small-signal model confirms the prediction made by Eq. (10.32). In Problem 10.28, we prove that this property holds in the presence of the Early effect as well.

The virtual-ground nature of node $P$ for differential small-signal inputs simplifies the analysis considerably. Since $v_{P}=0$, this node can be shorted to ac ground, reducing the differential pair of Fig. 10.15(a) to two "half circuits" [Fig. 10.15(b)]. With each half resembling a common-emitter stage, we can write

$$
\begin{align*}
v_{\text {out } 1} & =-g_{m} R_{C} v_{\text {in } 1}  \tag{10.87}\\
v_{\text {out } 2} & =-g_{m} R_{C} v_{\text {in } 2} \tag{10.88}
\end{align*}
$$

It follows that the differential voltage gain of the differential pair is equal to

$$
\begin{equation*}
\frac{v_{\text {out } 1}-v_{\text {out } 2}}{v_{\text {in } 1}-v_{\text {in } 2}}=-g_{m} R_{C} \tag{10.89}
\end{equation*}
$$

the same as that expressed by Eq. (10.40). For simplicity, we may draw the two half circuits as in Fig. 10.15(c), with the understanding that the incremental inputs are small and differential. Also, since the two halves are identical, we may draw only one half.

Example Compute the differential gain of the circuit shown in Fig. 10.16(a), where ideal current 10.10 sources are used as loads to maximize the gain.
image_name:Figure 10.16(a)
description:
[
name: Q1, type: NPN, ports: {C: Vout+, B: Vin1, E: P}
name: Q2, type: NPN, ports: {C: Vout-, B: Vin2, E: P}
name: I_EE, type: CurrentSource, ports: {Np: P, Nn: GND}
name: V_CC, type: VoltageSource, ports: {Np: V_CC, Nn: GND}
name: I1, type: CurrentSource, ports: {Np: VCC, Nn: Vout+}
name: I2, type: CurrentSource, ports: {Np: VCC, Nn: Vout-}
]
extrainfo:The circuit is a differential amplifier with two NPN transistors (Q1 and Q2), each having its base connected to separate input voltages (Vin1 and Vin2). The emitters are connected together to a current source (I_EE) which is grounded. The collectors of both transistors are connected to the output node (Vout), which is also connected to V_CC through current sources, maximizing the gain.

(a)
image_name:Figure 10.16
description:
[
name: Q1, type: NPN, ports: {C: Vout1, B: Vin1, E: GND}
name: Q2, type: NPN, ports: {C: Vout2, B: Vin2, E: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vout1, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vout2, N2: GND}
]
extrainfo:The circuit is a differential amplifier with two NPN transistors (Q1 and Q2), each having its base connected to separate input voltages (Vin1 and Vin2). The emitters are connected to GND. The collectors are connected to output nodes Vout1 and Vout2, which are also connected to resistors R1 and R2, respectively, to GND.

(b)

Solution With ideal current sources, the Early effect in $Q_{1}$ and $Q_{2}$ cannot be neglected, and the half circuits must be visualized as depicted in Fig. 10.16(b). Thus,

$$
\begin{align*}
& v_{\text {out } 1}=-g_{m} r_{O} v_{\text {in } 1}  \tag{10.90}\\
& v_{\text {out } 2}=-g_{m} r_{O} v_{\text {in } 2} \tag{10.91}
\end{align*}
$$

and hence

$$
\begin{equation*}
\frac{v_{\text {out } 1}-v_{\text {out } 2}}{v_{\text {in } 1}-v_{\text {in } 2}}=-g_{m} r_{O} \tag{10.92}
\end{equation*}
$$

Exercise Calculate the gain for $V_{A}=5 \mathrm{~V}$.

Example Figure 10.17(a) illustrates an implementation of the topology shown in Fig. 10.16(a).
10.11 Calculate the differential voltage gain.

Solution Noting that each pnp device introduces a resistance of $r_{O P}$ at the output nodes and drawing the half circuit as in Fig. 10.17(b), we have

$$
\begin{equation*}
\frac{v_{\text {out } 1}-v_{\text {out } 2}}{v_{\text {in } 1}-v_{\text {in } 2}}=-g_{m}\left(r_{O N} \| r_{O P}\right) \tag{10.93}
\end{equation*}
$$

where $r_{O N}$ denotes the output impedance of the $n p n$ transistors.
image_name:Figure 10.17 (a)
description:
[
name: Q1, type: NPN, ports: {C: Vout+, B: Vin1, E: P}
name: Q2, type: NPN, ports: {C: Vout-, B: Vin2, E: P}
name: Q3, type: PNP, ports: {C: Vout+, B: Vb, E: VCC}
name: Q4, type: PNP, ports: {C: Vout-, B: Vb, E: VCC}
name: IEE, type: CurrentSource, ports: {Np: P, Nn: GND}
]
extrainfo:Q3 and Q4 are configured as diode-connected devices. The circuit is a differential amplifier with a current source IEE providing bias current. The differential voltage gain is defined as the difference between the outputs divided by the difference between the inputs.

(a)
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: Vin1, E: GND}
name: Q3, type: PNP, ports: {C: Vout, B:   GND, E: GND}
]
extrainfo:Q3 is configured as a diode-connected device. The circuit is a differential amplifier with a focus on single-ended gain.

(b)

Figure 10.17

Exercise Calculate the gain if $Q_{3}$ and $Q_{4}$ are configured as diode-connected devices.

We must emphasize that the differential voltage gain is defined as the difference between the outputs divided by the difference between the inputs. As such, this gain is equal to the single-ended gain of each half circuit.

We now make an observation that proves useful in the analysis of differential circuits. As noted above, the symmetry of the circuit $\left(g_{m 1}=g_{m 2}\right)$ establishes a virtual ground at node $P$ in Fig. 10.12 if the incremental inputs are small and differential. This property holds for any other node that appears on the axis of symmetry. For example, the two resistors shown in Fig. 10.18 create a virtual ground at $X$ if (1) $R_{1}=R_{2}$ and (2) nodes $A$ and $B$ vary by equal and opposite amounts. ${ }^{2}$ Additional examples make this concept clearer. We assume perfect symmetry in each case.
image_name:Figure 10.18
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: A, N2: X}
name: R2, type: Resistor, value: R2, ports: {N1: X, N2: B}
name: ΔV, type: VoltageSource, value: ΔV, ports: {Np: A, Nn: GND}
name: ΔV, type: VoltageSource, value: ΔV, ports: {Np: B, Nn: GND}
]
extrainfo:The circuit establishes a virtual ground at node X when R1 equals R2 and nodes A and B vary by equal and opposite amounts.

Figure 10.18

Example Determine the differential gain of the circuit in Fig. 10.19(a) if $V_{A}<\infty$ and the circuit 10.12 is symmetric.

Solution Drawing one of the half circuits as shown in Fig. 10.19(b), we express the total resistance seen at the collector of $Q_{1}$ as

$$
\begin{equation*}
R_{o u t}=r_{O 1}\left\|r_{O 3}\right\| R_{1} \tag{10.94}
\end{equation*}
$$

[^0]image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: Vout1, B: Vin1, E: P}
name: Q2, type: NPN, ports: {C: Vout2, B: Vin2, E: P}
name: Q3, type: PNP, ports: {C: Vout1, B: Vb, E: VCC}
name: Q4, type: PNP, ports: {C: Vout2, B: Vb, E: VCC}
name: R1, type: Resistor, value: R1, ports: {N1: Vout1, N2: r1r2}
name: R2, type: Resistor, value: R2, ports: {N1: r1r2, N2: Vout2}
name: I_EE, type: CurrentSource, value: I_EE, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with two NPN transistors (Q1 and Q2) and two PNP transistors (Q3 and Q4). It uses resistors R1 and R2 to connect the collectors of Q1 and Q2, and a current source I_EE to bias the emitters. The bases of Q3 and Q4 are connected to a bias voltage Vb, and their emitters are connected to VCC. The circuit is designed to amplify the difference between Vin1 and Vin2.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: Vin1, E: GND}
name: Q3, type: PNP, ports: {C: Vout, B: GND, E: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a differential amplifier with a current source I_EE connected to ground. Q1 and Q3 form a complementary pair, with Q1 being NPN and Q3 being PNP. The resistor R1 is connected between the output node Vout and ground.

Figure 10.19
Thus, the voltage gain is equal to

$$
\begin{equation*}
A_{v}=-g_{m 1}\left(r_{O 1}\left\|r_{O 3}\right\| R_{1}\right) \tag{10.95}
\end{equation*}
$$

Exercise $\quad$ Repeat the above example if $R_{1} \neq R_{2}$.

Calculate the differential gain of the circuit illustrated in Fig. 10.20(a) if $V_{A}<\infty$.

10.13

image_name:Fig. 10.20(a)
description:
[
name: Q1, type: NPN, ports: {C: Vout1, B: Vin1, E: GND}
name: Q2, type: NPN, ports: {C: Vout2, B: Vin2, E: P}
name: Q3, type: PNP, ports: {C: Vout1, B: X, E: VCC}
name: Q4, type: PNP, ports: {C: Vout2, B: X, E: VCC}
name: R1, type: Resistor, value: R1, ports: {N1: Vout1, N2: X}
name: R2, type: Resistor, value: R2, ports: {N1: Vout2, N2: X}
name: I_EE, type: CurrentSource, value: I_EE, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with two NPN transistors (Q1 and Q2) and two PNP transistors (Q3 and Q4). The resistors R1 and R2 are connected to the output nodes Vout1 and Vout2, respectively. The current source I_EE provides biasing current. The voltage gain is given by Av = -gm1 * (ro1 || ro3 || R1).
image_name:Fig. 10.20(b)
description:
[
name: Q1, type: NPN, ports: {C: Vout1, B: Vin1, E: GND}
name: Q3, type: PNP, ports: {C: Vout1, B: X, E: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vout1, N2: X}
]
extrainfo:The circuit is a differential amplifier with two NPN transistors (Q1 and Q2) and two PNP transistors (Q3 and Q4). It uses resistors R1 and R2 for load and current source I_EE for biasing. The circuit provides differential outputs Vout1 and Vout2.

(a)
(b)

Figure 10.20
Solution For small differential inputs and outputs, $V_{X}$ remains constant, leading to the conceptual half circuit shown in Fig. 10.20(b) -the same as that in the above example. This is because $Q_{3}$ and $Q_{4}$ experience a constant base-emitter voltage in both cases, thereby serving as current sources and exhibiting only an output resistance. It follows that

$$
\begin{equation*}
A_{v}=-g_{m 1}\left(r_{O 1}\left\|r_{O 3}\right\| R_{1}\right) \tag{10.96}
\end{equation*}
$$

Exercise Calculate the gain if $V_{A}=4 \mathrm{~V}$ for all transistors, $R_{1}=R_{2}=10 \mathrm{k} \Omega$, and $I_{E E}=1 \mathrm{~mA}$.

Example
Determine the gain of the degenerated differential pairs shown in Figs. 10.21(a) and (b).
Assume $V_{A}=\infty$. Assume $V_{A}=\infty$.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: X, B: Vin1, E: e1}
name: Q2, type: NPN, qqports: {C: Y, B: Vin2, E: e2}
name: RC, type: Resistor, value: RC, ports: {N1: X, N2: VCC}
name: RC, type: Resistor, value: RC, ports: {N1: Y, N2: VCC}
name: RE, type: Resistor, value: RE, ports: {N1: P, N2: e1}
name: RE, type: Resistor, value: RE, ports: {N1: P, N2: e2}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: P, Nn: GND}
]
extrainfo:This is a differential amplifier circuit with two NPN transistors (Q1 and Q2) sharing a common emitter node P. The circuit is powered by VCC and has a current source IEE connected to the common emitter node.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: X, B: Vin1, E: e1}
name: Q2, type: NPN, ports: {C: Y, B: Vin2, E: e2}
name: RC, type: Resistor, value: RC, ports: {N1: X, N2: VCC}
name: RC, type: Resistor, value: RC, ports: {N1: Y, N2: VCC}
name: RE, type: Resistor, value: RE, ports: {N1: e1, N2: e2}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: e1, Nn: GND}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: e2, Nn: GND}
]
extrainfo:This circuit is a differential amplifier with two NPN transistors (Q1 and Q2). The emitters of Q1 and Q2 are connected through a resistor RE, and each emitter has a current source IEE connected to ground. The collectors of the transistors are connected to VCC through resistors RC. The inputs are applied to the bases of the transistors, and the output is taken differentially from the collectors.
image_name:(c)
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: Vin1, E: e1}
name: RC, type: Resistor, value: RC, ports: {N1: Vout, N2: GND}
name: RE, type: Resistor, value: RE, ports: {N1: e1, N2: GND}
]
extrainfo:The circuit represents a half circuit of a differential amplifier with a single NPN transistor Q1. The collector is connected to the output node Vout through resistor RC, while the emitter is connected to ground through resistor RE and a current source IEE. The input is applied to the base of Q1.
image_name:(d)
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: Vin1, E: e1}
name: RC, type: Resistor, value: RC, ports: {N1: GND, N2: Vout}
name: RE, type: Resistor, value: RE/2, ports: {N1: e1, N2: GND}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
]
extrainfo:The circuit is a single-ended differential amplifier with a degenerated emitter resistor RE/2. The current source IEE provides bias current to the transistor Q1. The output voltage is taken across the collector resistor RC.

Figure 10.21

Solution

In the topology of Fig. 10.21(a), node $P$ is a virtual ground, yielding the half circuit depicted in Fig. 10.21(c). From Chapter 5, we have

$$
\begin{equation*}
A_{v}=-\frac{R_{C}}{R_{E}+\frac{1}{g_{m}}} \tag{10.97}
\end{equation*}
$$

In the circuit of Fig. 10.21(b), the line of symmetry passes through the "midpoint" of $R_{E}$. In other words, if $R_{E}$ is regarded as two $R_{E} / 2$ units in series, then the node between the units acts as a virtual ground [Fig. 10.21(d)]. It follows that

$$
\begin{equation*}
A_{v}=-\frac{R_{C}}{\frac{R_{E}}{2}+\frac{1}{g_{m}}} \tag{10.98}
\end{equation*}
$$

The two circuits provide equal gains if the pair in Fig. 10.21(b) incorporates a total degeneration resistance of $2 R_{E}$.

Exercise Design each circuit for a gain of 5 and power consumption of 2 mW . Assume $V_{C C}=2.5 \mathrm{~V}$, $V_{A}=\infty$, and $R_{E}=2 / g_{m}$.

I/O Impedances For a differential pair, we can define the input impedance as illustrated in Fig. 10.22(a). From the equivalent circuit in Fig. 10.22(b), we have

$$
\begin{equation*}
\frac{v_{\pi 1}}{r_{\pi 1}}=i_{X}=-\frac{v_{\pi 2}}{r_{\pi 2}} \tag{10.99}
\end{equation*}
$$

image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: c1, B: b1, E: P}
name: Q2, type: NPN, ports: {C: c2, B: b2, E: P}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: C1}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: C2}
name: Vx, type: VoltageSource, value: Vx, ports: {Np: b2, Nn: b1}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with two NPN transistors (Q1 and Q2) configured to amplify the differential input voltage. The circuit includes degeneration resistors and capacitors for stability and frequency response. The input impedance is defined by rπ1 and rπ2, and the output is taken across the collector resistors RC. The circuit is powered by a current source IEE and a voltage source VCC.
image_name:(b)
description:
[
name: V_X, type: VoltageSource, value: V_X, ports: {Np: b1, Nn: b2}
name: r_π1, type: Resistor, value: r_π1, ports: {N1: b1, N2: P}
name: r_π2, type: Resistor, value: r_π2, ports: {N1: b2, N2: P}
name: g_m1v_π1, type: CurrentControlledCurrentSource, ports: {Np: c1, Nn: P}
name: g_m2v_π2, type: CurrentControlledCurrentSource, ports: {Np: ‘c2, Nn: P}
name: RC, type: Resistor, value: RC, ports: {N1: GND, N2: c1}
name: RC, type: Resistor, value: RC, ports: {N1: GND, N2: c2'}
]
extrainfo:The circuit is a differential amplifier with a total degeneration resistance of 2RE. It is designed for a gain of 5 and power consumption of 2 mW. The input impedance is defined using r_π1 and r_π2, and the differential input impedance is 2r_π1.

Figure 10.22 (a) Method for calculation of differential input impedance, (b) equivalent circuit of (a).

Also,

$$
\begin{align*}
v_{X} & =v_{\pi 1}-v_{\pi 2}  \tag{10.100}\\
& =2 r_{\pi 1} i_{X} \tag{10.101}
\end{align*}
$$

It follows that

$$
\begin{equation*}
\frac{v_{X}}{i_{X}}=2 r_{\pi 1} \tag{10.102}
\end{equation*}
$$

as if the two base-emitter junctions appear in series.
The above quantity is called the "differential input impedance" of the circuit. It is also possible to define a "single-ended input impedance" with the aid of a half circuit (Fig. 10.23), obtaining

$$
\begin{equation*}
\frac{v_{X}}{i_{X}}=r_{\pi 1} \tag{10.103}
\end{equation*}
$$

This result provides no new information with respect to that in Eq. (10.102) but proves useful in some calculations.
image_name:Figure 10.23 Calculation of single-ended input impedance
description:
[
name: Vx, type: VoltageSource, value: vx, ports: {Np: Vx, Nn: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: C1}
name: Q1, type: NPN, ports: {C: C1, B: Vx, E: GND}
]
extrainfo:The circuit is used to calculate the single-ended input impedance. It consists of a voltage source Vx, a resistor RC, a capacitor C1, an NPN transistor Q1, and a diode ix. The transistor is configured with its emitter connected to ground, base connected to the node Vx, and collector connected to the node C1. The diode ix is connected between the nodes Vx and B.

Figure 10.23 Calculation of single-ended input impedance.

In a manner similar to the foregoing development, the reader can show that the differential and single-ended output impedances are equal to $2 R_{C}$ and $R_{C}$, respectively.

## 10.3 MOS DIFFERENTIAL PAIR

Most of the principles studied in the previous section for the bipolar differential pair apply directly to the MOS counterpart as well. For this reason, our treatment of the MOS circuit in this section is more concise. We continue to assume perfect symmetry.
image_name:Figure 10.24
description:
[
name: M1, type: NMOS, ports: {S: S1S2, D: X, G: VCM}
name: M2, type: NMOS, ports: {S: S1S2, D: Y, G: VCM}
name: RD, type: Resistor, value: RD, ports: {N1: X, N2: VDD}
name: RD, type: Resistor, value: RD, ports: {N1: Y, N2: VDD}
name: VCM, type: VoltageSource, value: VCM, ports: {Np: VCM, Nn: GND}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: S1S2, Nn: GND}
]
extrainfo:The circuit is a symmetric MOS differential pair with common-mode voltage VCM and current source ISS. The resistors RD are connected from the drain of each NMOS to VDD.

Figure 10.24 Response of MOS differential pair to input CM variation.

### 10.3.1 Qualitative Analysis

Figure 10.24(a) depicts the MOS pair with the two inputs tied to $V_{C M}$, yielding

$$
\begin{equation*}
I_{D 1}=I_{D 2}=\frac{I_{S S}}{2} \tag{10.104}
\end{equation*}
$$

and

$$
\begin{equation*}
V_{X}=V_{Y}=V_{D D}-R_{D} \frac{I_{S S}}{2} . \tag{10.105}
\end{equation*}
$$

That is, a zero differential input gives a zero differential output. Note that the output CM level is equal to $V_{D D}-R_{D} I_{S S} / 2$.

For our subsequent derivations, it is useful to compute the "equilibrium overdrive voltage" of $M_{1}$ and $M_{2},\left(V_{G S}-V_{T H}\right)_{\text {equil. }}$. We assume $\lambda=0$ and hence $I_{D}=$ $(1 / 2) \mu_{n} C_{o x}(W / L)\left(V_{G S}-V_{T H}\right)^{2}$. Carrying a current of $I_{S S} / 2$, each device exhibits an overdrive of

$$
\begin{equation*}
\left(V_{G S}-V_{T H}\right)_{e q u i l .}=\sqrt{\frac{I_{S S}}{\mu_{n} C_{o x} \frac{W}{L}}} \tag{10.106}
\end{equation*}
$$

As expected, a greater tail current or a smaller $W / L$ translates to a larger equilibrium overdrive.

To guarantee that $M_{1}$ and $M_{2}$ operate in saturation, we require that their drain voltages not fall below $V_{C M}-V_{T H}$ :

$$
\begin{equation*}
V_{D D}-R_{D} \frac{I_{S S}}{2}>V_{C M}-V_{T H} \tag{10.107}
\end{equation*}
$$

It can also be observed that a change in $V_{C M}$ cannot alter $I_{D 1}=I_{D 2}=I_{S S} 2$, leaving $V_{X}$ and $V_{Y}$ undisturbed. The circuit thus rejects input CM variations.

Example A MOS differential pair is driven with an input CM level of 1.6 V . If $I_{S S}=0.5 \mathrm{~mA}$, 10.15 $V_{T H}=0.5 \mathrm{~V}$, and $V_{D D}=1.8 \mathrm{~V}$, what is the maximum allowable load resistance?

Solution From Eq. (10.107), we have

$$
\begin{align*}
R_{D} & <2 \frac{V_{D D}-V_{C M}+V_{T H}}{I_{S S}}  \tag{10.108}\\
& <2.8 \mathrm{k} \Omega . \tag{10.109}
\end{align*}
$$

We may suspect that this limitation in turn constrains the voltage gain of the circuit, as explained later.

What is the maximum tail current if the load resistance is $5 \mathrm{k} \Omega$ ?

Figure 10.25 illustrates the response of the MOS pair to large differential inputs. If $V_{i n 1}$ is well above $V_{i n 2}$ [Fig. 10.25(a)], then $M_{1}$ carries the entire tail current, generating

$$
\begin{align*}
& V_{X}=V_{D D}-R_{D} I_{S S}  \tag{10.110}\\
& V_{Y}=V_{D D} . \tag{10.111}
\end{align*}
$$

Similarly, if $V_{\text {in2 }}$ is well above $V_{\text {in } 1}$ [Fig. 10.25(b)], then

$$
\begin{align*}
& V_{X}=V_{D D}  \tag{10.112}\\
& V_{Y}=V_{D D}-R_{D} I_{S S} \tag{10.113}
\end{align*}
$$

The circuit therefore steers the tail current from one side to the other, producing a differential output in response to a differential input. Figure 10.25(c) sketches the characteristics of the circuit.

Let us now examine the circuit's behavior for a small input difference. Depicted in Fig. 10.26(a), such a scenario maintains $V_{P}$ constant because Eqs. (10.27)-(10.32) apply to this case equally well. It follows that

$$
\begin{align*}
\Delta I_{D 1} & =g_{m} \Delta V  \tag{10.114}\\
\Delta I_{D 2} & =-g_{m} \Delta V \tag{10.115}
\end{align*}
$$

image_name:Figure 10.25(a)
description:
[
name: M1, type: NMOS, ports: {S: s1s2, D: X, G: Vin1}
name: M2, type: NMOS, ports: {S: s1s2, D: Y, G: Vin2}
name: RD1, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: RD2, type: Resistor, value: RD, ports: {N1: VDD, N2: Y}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: s1s2, Nn: GND}
]
extrainfo:This is a differential amplifier circuit using NMOS transistors. The circuit is biased with a current source ISS, and the output voltage Vout is the differential voltage between nodes X and Y. The resistors RD provide load resistance for the transistors M1 and M2.

(a)
image_name:Figure 10.25 (c)
description:The graph in Figure 10.25 (c) is a qualitative plot representing the behavior of currents in a MOS differential pair circuit. The x-axis is labeled as \( V_{in1} - V_{in2} \), indicating the differential input voltage, and it is centered at zero. The y-axis represents the currents \( I_{D1} \) and \( I_{D2} \), which are the drain currents of the transistors in the differential pair.

The graph shows two intersecting curves. The curve labeled \( I_{D1} \) starts at the maximum current \( I_{SS} \) when \( V_{in1} - V_{in2} \) is negative and decreases towards zero as \( V_{in1} - V_{in2} \) becomes positive. Conversely, the curve labeled \( I_{D2} \) starts at zero and increases to \( I_{SS} \) as \( V_{in1} - V_{in2} \) becomes positive. The intersection point of the two curves occurs at \( V_{in1} - V_{in2} = 0 \), where both currents are equal to \( \frac{I_{SS}}{2} \).

The dotted horizontal line at \( I_{SS} \) indicates the maximum possible current that can flow through either transistor, while the dotted line at \( \frac{I_{SS}}{2} \) marks the point where the currents are equal. This behavior illustrates the current steering characteristic of a differential pair, where the total current \( I_{SS} \) is split between the two transistors depending on the differential input voltage.

image_name:Figure 10.26
description:
[
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: M1, type: NMOS, ports: {S: S1S2, D: X, G: Vin1}
name: M2, type: NMOS, ports: {S: S1S2, D: Y, G: Vin2}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: S1S2, Nn: GND}
]
extrainfo:The circuit is a differential pair with NMOS transistors M1 and M2. The current source ISS provides biasing, splitting the current between M1 and M2 depending on the differential input voltage Vin1 and Vin2. RD resistors are used for load, and Vout is taken from the middle point between the resistors.

(b)
image_name:Figure 10.25 (a)
description:The graph in Figure 10.25 (a) represents the response of a MOS differential pair to a very positive input. It is a plot illustrating the relationship between the differential input voltage \( V_{in1} - V_{in2} \) on the horizontal axis and the voltages \( V_X \) and \( V_Y \) on the vertical axis.

1. **Type of Graph and Function:**
- The graph is a qualitative plot showing the behavior of voltages in a differential pair circuit in response to varying input voltages.

2. **Axes Labels and Units:**
- The horizontal axis represents the differential input voltage \( V_{in1} - V_{in2} \), although the units are not explicitly marked, it is typically in volts.
- The vertical axis represents the output voltages \( V_X \) and \( V_Y \), again typically in volts.

3. **Overall Behavior and Trends:**
- The graph shows two curves, \( V_X \) and \( V_Y \), which intersect at the origin where the differential input voltage is zero.
- As the differential input voltage becomes very positive, \( V_X \) increases towards \( V_{DD} \), while \( V_Y \) decreases towards \( V_{DD} - R_D I_{SS} \).
- The curves are symmetrical around the vertical axis, indicating a balanced response to positive and negative inputs.

4. **Key Features and Technical Details:**
- The maximum value \( V_X \) approaches is \( V_{DD} \), the supply voltage.
- The minimum value \( V_Y \) approaches is \( V_{DD} - R_D I_{SS} \), determined by the load resistor \( R_D \) and the bias current \( I_{SS} \).
- The mid-point value where \( V_X \) and \( V_Y \) are equal is \( V_{DD} - \frac{R_D I_{SS}}{2} \).

5. **Annotations and Specific Data Points:**
- The graph is annotated with horizontal dashed lines indicating the levels of \( V_{DD} \), \( V_{DD} - \frac{R_D I_{SS}}{2} \), and \( V_{DD} - R_D I_{SS} \).
- The intersection point at the origin is marked as zero, indicating no differential input voltage.

(c)

Figure 10.25 (a) Response of MOS differential pair to very positive input, (b) response of MOS differential pair to very negative input, (c) qualitative plots of currents and voltages.
image_name:Figure 10.26
description:
[
name: M1, type: NMOS, ports: {S: S1S2, D: X, G: VCM+ΔV}
name: M2, type: NMOS, ports: {S: S1S2, D: Y, G: VCM-ΔV}
name: RD1, type: Resistor, value: RD, ports: {N1: X, N2: VDD}
name: RD2, type: Resistor, value: RD, ports: {N1: Y, N2: VDD}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential pair using NMOS transistors M1 and M2 with a current source ISS. The resistors RD are connected to VDD. The differential input voltages are applied to the gates of M1 and M2.

Figure 10.26 Response of MOS pair to small differential inputs.
and

$$
\begin{equation*}
\Delta V_{X}-\Delta V_{Y}=-2 g_{m} R_{D} \Delta V \tag{10.116}
\end{equation*}
$$

As expected, the differential voltage gain is given by

$$
\begin{equation*}
A_{v}=-g_{m} R_{D}, \tag{10.117}
\end{equation*}
$$

similar to that of a common-source stage.

Example Design an NMOS differential pair for a voltage gain of 5 and a power budget of 2 mW
10.16 subject to the condition that the stage following the differential pair requires an input CM level of at least 1.6 V . Assume $\mu_{n} C_{o x}=100 \mu \mathrm{~A} / \mathrm{V}^{2}, \lambda=0$, and $V_{D D}=1.8 \mathrm{~V}$.

Solution From the power budget and the supply voltage, we have

$$
\begin{equation*}
I_{S S}=1.11 \mathrm{~mA} \tag{10.118}
\end{equation*}
$$

The output CM level (in the absence of signals) is equal to

$$
\begin{equation*}
V_{C M, \text { out }}=V_{D D}-R_{D} \frac{I_{S S}}{2} \tag{10.119}
\end{equation*}
$$

For $V_{C M, \text { out }}=1.6 \mathrm{~V}$, each resistor must sustain a voltage drop of no more than 200 mV , thereby assuming a maximum value of

$$
\begin{equation*}
R_{D}=360 \Omega . \tag{10.120}
\end{equation*}
$$

Setting $g_{m} R_{D}=5$, we must choose the transistor dimensions such that $g_{m}=5 /(360 \Omega)$. Since each transistor carries a drain current of $I_{S S} / 2$,

$$
\begin{equation*}
g_{m}=\sqrt{2 \mu_{n} C_{o x} \frac{W}{L} \frac{I_{S S}}{2}}, \tag{10.121}
\end{equation*}
$$

and hence

$$
\begin{equation*}
\frac{W}{L}=1738 \tag{10.122}
\end{equation*}
$$

The large aspect ratio arises from the small drop allowed across the load resistors.
Exercise If the aspect ratio must remain below 200, what voltage gain can be achieved?

We rewrite Eq. (10.107) as

$$
\begin{align*}
V_{C M, \text { in }} & <V_{D D}-R_{D} \frac{I_{S S}}{2}+V_{T H}  \tag{10.123}\\
& <V_{C M, \text { out }}+V_{T H} \tag{10.124}
\end{align*}
$$

This is conceptually illustrated in Fig. 10.27. Thus,

$$
\begin{equation*}
V_{C M, \text { in }}<2 \mathrm{~V} \tag{10.125}
\end{equation*}
$$

Interestingly, the input CM level can comfortably remain at $V_{D D}$. In contrast to Example 10.5 , the constraint on the load resistor in this case arises from the output CM level requirement.
image_name:Figure 10.27
description:
[
name: M1, type: NMOS, ports: {S: s1s2, D: X, G: VCM,in}
name: M2, type: NMOS, ports: {S: s1s2, D: Y, G: VCM,in}
name: RD1, type: Resistor, value: RD, ports: {N1: X, N2: VDD}
name: RD2, type: Resistor, value: RD, ports: {N1: Y, N2: VDD}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: VCM,in, type: VoltageSource, value: VCM,in, ports: {Np: VCM,in, Nn: GND}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: s1s2, Nn: GND}
]
extrainfo:The circuit is a differential pair with NMOS transistors M1 and M2. The common-mode input voltage VCM,in is applied to the gates of both transistors. The current source ISS sets the bias current for the differential pair. The resistors RD1 and RD2 are connected to the drains of M1 and M2, respectively, and are connected to the supply voltage VDD. The circuit is designed to operate with a common-mode input voltage less than 2V.
image_name:Figure 10.28
description:The system block diagram in Figure 10.28 represents a differential amplifier circuit using MOSFET transistors. The main components of the circuit include:

1. **Transistors (M1 and M2):** These are N-channel MOSFETs arranged in a differential pair configuration. They are labeled as M1 and M2 and serve as the primary amplifying elements.

2. **Load Resistors (R_D):** Two identical resistors, labeled R_D, are connected to the drain of each transistor (M1 and M2) and the supply voltage V_DD. These resistors convert the current changes through the transistors into voltage changes at nodes X and Y.

3. **Current Source (I_SS):** A constant current source labeled I_SS is connected to the common source connection of the transistors. This current source sets the bias current for the differential pair.

4. **Input Voltage (V_CM,in):** The input common-mode voltage (V_CM,in) is applied to the gates of both transistors, with a reference to ground (GND).

5. **Output Voltage (V_CM,out):** The output common-mode voltage (V_CM,out) is represented in the diagram, indicating the voltage level at the output nodes relative to the input.

6. **Threshold Voltage (V_TH):** A voltage difference labeled V_TH is shown between V_CM,in and V_CM,out, representing the threshold voltage level.

**Flow of Information:**
- The input common-mode voltage V_CM,in is applied to the gates of the transistors M1 and M2. The differential pair amplifies any differential input signal while maintaining a constant common-mode level.
- The current source I_SS ensures that the total current through M1 and M2 remains constant, which stabilizes the operation of the amplifier.
- The amplified signals are converted to output voltages across the load resistors R_D at nodes X and Y. These nodes provide the output common-mode voltage V_CM,out.

**Overall System Function:**
- The primary function of this differential amplifier is to amplify the difference between the input signals applied to the gates of M1 and M2 while rejecting common-mode signals. The circuit maintains a stable bias condition through the current source I_SS and converts current variations into voltage variations at the output nodes through the load resistors R_D. The threshold voltage V_TH indicates the limit for the input common-mode voltage level to ensure proper operation.

Figure 10.27

Exercise Does the above result hold if $V_{T H}=0.2 \mathrm{~V}$ ?
image_name:Figure 10.28 (left)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1r, G: Vin}
name: R, type: Resistor, value: R, ports: {N1: d1r, N2: VDD}
name: M1, type: NMOS, ports: {S: s1s2, D: VDD, G: Vin1}
name: M2, type: NMOS, ports: {S: s1s2, D: VDD, G: Vin2}
name: R, type: Resistor, value: R, ports: {N1: VDD, N2: d1}
name: R, type: Resistor, value: R, ports: {N1: VDD, N2: d2}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: s1s2, Nn: GND}
]
extrainfo:The circuit contains a common-source stage and a differential pair with load resistors. The common-source stage uses NMOS M1 with a resistor R connected to VDD. The differential pair consists of NMOS transistors M1 and M2, sharing a current source Iss, with load resistors connected to VDD. The circuit is used for comparing input signals Vin1 and Vin2, rejecting common-mode signals.
image_name:Figure 10.28 (right)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1r, G: Vin}
name: R, type: Resistor, value: R, ports: {N1: VDD, N2: d1r}
name: M1, type: NMOS, ports: {S: s1s2, D: VDD, G: Vin1}
name: M2, type: NMOS, ports: {S: s1s2, D: VDD, G: Vin2}
name: R, type: Resistor, value: R, ports: {N1: VDD, N2: M1_D}
name: R, type: Resistor, value: R, ports: {N1: VDD, N2: M2_D}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: s1s2, Nn: GND}
]
extrainfo:The circuit includes a common-source stage and a differential pair with load resistors. The NMOS transistors M1 and M2 form a differential pair with a shared current source Iss. The circuit is designed to compare voltage gains and power dissipation for given transistor dimensions.

Figure 10.28

Solution (a) For the two circuits to consume the same amount of power $I_{D 1}=I_{S S}=2 I_{D 2}=2 I_{D 3}$; i.e., each transistor in the differential pair carries a current equal to half of the drain current of the CS transistor. Equation (10.121) therefore requires that the differential pair transistors be twice as wide as the CS device to obtain the same voltage gain. (b) If the transistors in both circuits have the same dimensions, then the tail current of the differential pair must be twice the bias current of the CS stage for $M_{1}-M_{3}$ to have the same transconductance, doubling the power consumption.

Exercise Discuss the above results if the CS stage and the differential pair incorporate equal source degeneration resistors.

### 10.3.2 Large-Signal Analysis

As with the large-signal analysis of the bipolar pair, our objective here is to derive the input/output characteristics of the MOS pair as the differential input varies from very negative to very positive values. From Fig. 10.29, we have

$$
\begin{align*}
V_{\text {out }} & =V_{\text {out } 1}-V_{\text {out } 2}  \tag{10.126}\\
& =-R_{D}\left(I_{D 1}-I_{D 2}\right) \tag{10.127}
\end{align*}
$$

To obtain $I_{D 1}-I_{D 2}$, we neglect channellength modulation and write a KVL around the input network and a KCL at the tail node:

$$
\begin{gather*}
V_{i n 1}-V_{G S 1}=V_{i n 2}-V_{G S 2}  \tag{10.128}\\
I_{D 1}+I_{D 2}=I_{S S} . \tag{10.129}
\end{gather*}
$$

Did you know?

The MOS differential pair was a natural extension of its bipolar counterpart, offering an important advantage: very little input current. But the need for high-input-impedance op amps had in fact arisen well before MOS op amps became manufacturable. The challenge was to integrate fieldeffect transistors (which generally have a small gate current) on the same chip as the other bipolar devices. The FETs were poorly controlled and suffered from a large offset. It was not until 1970s that high-input-impedance op amps became common. MOS op amps also began to play a profound role in analog integrated circuits, serving as the core of "switched-capacitor" filters and analog-to-digital converters.

Since $I_{D}=(1 / 2) \mu_{n} C_{o x}(W / L)\left(V_{G S}-V_{T H}\right)^{2}$,

$$
\begin{equation*}
V_{G S}=V_{T H}+\sqrt{\frac{2 I_{D}}{\mu_{n} C_{o x} \frac{W}{L}}} \tag{10.130}
\end{equation*}
$$

image_name:Figure 10.29 MOS differential pair for large-signal analysis
description:
[
name: M1, type: NMOS, ports: {S: SS, D: Vout1, G: Vin1}
name: M2, type: NMOS, ports: {S: SS, D: Vout2, G: Vin2}
name: RD1, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout1}
name: RD2, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout2}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: SS, Nn: GND}
]
extrainfo:The circuit is a MOS differential pair used for large-signal analysis. It consists of two NMOS transistors (M1 and M2) with a current source ISS providing the tail current. The differential outputs are taken from Vout1 and Vout2 across the load resistors RD.

Figure 10.29 MOS differential pair for large-signal analysis.

Substituting for $V_{G S 1}$ and $V_{G S 2}$ in Eq. (10.128), we have

$$
\begin{align*}
V_{i n 1}-V_{i n 2} & =V_{G S 1}-V_{G S 2}  \tag{10.131}\\
& =\sqrt{\frac{2}{\mu_{n} C_{o x} \frac{W}{L}}}\left(\sqrt{I_{D 1}}-\sqrt{I_{D 2}}\right) \tag{10.132}
\end{align*}
$$

Squaring both sides yields

$$
\begin{align*}
\left(V_{i n 1}-V_{i n 2}\right)^{2} & =\frac{2}{\mu_{n} C_{o x} \frac{W}{L}}\left(I_{D 1}+I_{D 2}-2 \sqrt{I_{D 1} I_{D 2}}\right)  \tag{10.133}\\
& =\frac{2}{\mu_{n} C_{o x} \frac{W}{L}}\left(I_{S S}-2 \sqrt{I_{D 1} I_{D 2}}\right) \tag{10.134}
\end{align*}
$$

We now find $\sqrt{I_{D 1} I_{D 2}}$,

$$
\begin{equation*}
4 \sqrt{I_{D 1} I_{D 2}}=2 I_{S S}-\mu_{n} C_{o x} \frac{W}{L}\left(V_{i n 1}-V_{i n 2}\right)^{2} \tag{10.135}
\end{equation*}
$$

square the result again,

$$
\begin{equation*}
16 I_{D 1} I_{D 2}=\left[2 I_{S S}-\mu_{n} C_{o x} \frac{W}{L}\left(V_{i n 1}-V_{i n 2}\right)^{2}\right]^{2} \tag{10.136}
\end{equation*}
$$

and substitute $I_{S S}-I_{D 1}$ for $I_{D 2}$,

$$
\begin{equation*}
16 I_{D 1}\left(I_{S S}-I_{D 1}\right)=\left[2 I_{S S}-\mu_{n} C_{o x} \frac{W}{L}\left(V_{i n 1}-V_{i n 2}\right)^{2}\right]^{2} \tag{10.137}
\end{equation*}
$$

It follows that

$$
\begin{equation*}
16 I_{D 1}^{2}-16 I_{S S} I_{D 1}+\left[2 I_{S S}-\mu_{n} C_{o x} \frac{W}{L}\left(V_{i n 1}-V_{i n 2}\right)^{2}\right]^{2}=0 \tag{10.138}
\end{equation*}
$$

and hence

$$
\begin{equation*}
I_{D 1}=\frac{I_{S S}}{2} \pm \frac{1}{4} \sqrt{4 I_{S S}^{2}-\left[\mu_{n} C_{o x} \frac{W}{L}\left(V_{i n 1}-V_{i n 2}\right)^{2}-2 I_{S S}\right]^{2}} \tag{10.139}
\end{equation*}
$$

In Problem 10.44, we show that only the solution with the sum of the two terms is acceptable:

$$
\begin{equation*}
I_{D 1}=\frac{I_{S S}}{2}+\frac{V_{i n 1}-V_{i n 2}}{4} \sqrt{\mu_{n} C_{o x} \frac{W}{L}\left[4 I_{S S}-\mu_{n} C_{o x} \frac{W}{L}\left(V_{i n 1}-V_{i n 2}\right)^{2}\right]} \tag{10.140}
\end{equation*}
$$

The symmetry of the circuit also implies that

$$
\begin{equation*}
I_{D 2}=\frac{I_{S S}}{2}+\frac{V_{i n 2}-V_{i n 1}}{4} \sqrt{\mu_{n} C_{o x} \frac{W}{L}\left[4 I_{S S}-\mu_{n} C_{o x} \frac{W}{L}\left(V_{i n 2}-V_{i n 1}\right)^{2}\right]} \tag{10.141}
\end{equation*}
$$

That is,

$$
\begin{equation*}
I_{D 1}-I_{D 2}=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{i n 1}-V_{i n 2}\right) \sqrt{\frac{4 I_{S S}}{\mu_{n} C_{o x} \frac{W}{L}}-\left(V_{i n 1}-V_{i n 2}\right)^{2}} \tag{10.142}
\end{equation*}
$$

image_name:Figure 10.30 MOS differential pair with one device off
description:
[
name: M1, type: NMOS, ports: {S: GND, D: S1S2, G: VTH}
name: M2, type: NMOS, ports: {S: GND, D: S1S2, G: VGS2}
name: ISS, type: CurrentSource, ports: {Np: S1S2, Nn: GND}
]
extrainfo:The circuit is a MOS differential pair with one device off. M1 and M2 are NMOS transistors sharing the same drain node S1S2. The current source ISS provides the bias current to the differential pair. The gate of M1 is at the threshold voltage VTH, indicating it is at the edge of conduction.

Figure 10.30 MOS differential pair with one device off.
Equations (10.140)-(10.142) form the foundation of our understanding of the MOS differential pair.

Let us now examine Eq. (10.142) closely. As expected from the characteristics in Fig. 10.25 (c), the right-hand side is an odd (symmetric) function of $V_{i n 1}-V_{i n 2}$, dropping to zero for a zero input difference. But, can the difference under the square root vanish, too? That would suggest that $I_{D 1}-I_{D 2}$ falls to zero as $\left(V_{i n 1}-V_{i n 2}\right)^{2}$ reaches $4 I_{S S} /\left(\mu_{n} C_{o x} W / L\right)$, an effect not predicted by our qualitative sketches in Fig. 10.25(c). Furthermore, it appears that the argument of the square root becomes negative as $\left(V_{i n 1}-V_{i n 2}\right)^{2}$ exceeds this value! How should these results be interpreted?

Implicit in our foregoing derivations is the assumption both transistors are on. However, as $\left|V_{i n 1}-V_{i n 2}\right|$ rises, at some point $M_{1}$ or $M_{2}$ turns off, violating the above equations. We must therefore determine the input difference that places one of the transistors at the edge of conduction. This can be accomplished by equating Eqs. (10.140), (10.141), or (10.142) to $I_{S S}$, but this leads to lengthy algebra. Instead, we recognize from Fig. 10.30 that if, for example, $M_{1}$ approaches the edge of conduction, then its gate-source voltage falls to a value equal to $V_{T H}$. Also, the gate-source voltage of $M_{2}$ must be sufficiently large to accommodate a drain current of $I_{S S}$ :

$$
\begin{align*}
V_{G S 1} & =V_{T H}  \tag{10.143}\\
V_{G S 2} & =V_{T H}+\sqrt{\frac{2 I_{S S}}{\mu_{n} C_{o x} \frac{W}{L}}} \tag{10.144}
\end{align*}
$$

It follows from Eq. (10.128) that

$$
\begin{equation*}
\left|V_{i n 1}-V_{i n 2}\right|_{\max }=\sqrt{\frac{2 I_{S S}}{\mu_{n} C_{o x} \frac{W}{L}}} \tag{10.145}
\end{equation*}
$$

where $\left|V_{i n 1}-V_{i n 2}\right|_{\text {max }}$ denotes the input difference that places one transistor at the edge of conduction. Equation (10.145) is invalid for input differences greater than this value. Indeed, substituting from Eq. (10.145) in (10.142) also yields $\left|I_{D 1}-I_{D 2}\right|=I_{S S}$. We also note that $\left|V_{i n 1}-V_{i n 2}\right|_{\max }$ can be related to the equilibrium overdrive [Eq. (10.106)] as follows:

$$
\begin{equation*}
\left|V_{i n 1}-V_{i n 2}\right|_{\max }=\sqrt{2}\left(V_{G S}-V_{T H}\right)_{\text {equil. }} . \tag{10.146}
\end{equation*}
$$

The above findings are very important and stand in contrast to the behavior of the bipolar differential pair and Eq. (10.78): the MOS pair steers all of the tail current ${ }^{3}$ for $\left|V_{i n 1}-V_{i n 2}\right|_{\text {max }}$ whereas the bipolar counterpart only approaches this condition for a finite

[^1]image_name:(a)
description:The graph labeled (a) represents the variation of drain currents \( I_{D1} \) and \( I_{D2} \) as a function of the input voltage difference \( V_{in1} - V_{in2} \). This is a plot typically used in the analysis of a differential pair circuit.

1. **Type of Graph and Function:**
- This is a line graph showing the relationship between the differential input voltage and the drain currents in a MOS differential pair.

2. **Axes Labels and Units:**
- The horizontal axis represents the input voltage difference \( V_{in1} - V_{in2} \), marked from \(-\Delta V_{in,max}\) to \(+\Delta V_{in,max}\).
- The vertical axis represents the drain currents \( I_{D1} \) and \( I_{D2} \), with significant markers at 0, \( \frac{I_{SS}}{2} \), and \( I_{SS} \).

3. **Overall Behavior and Trends:**
- The curves for \( I_{D1} \) and \( I_{D2} \) are symmetrical about the vertical axis (\( V_{in1} - V_{in2} = 0 \)).
- As \( V_{in1} - V_{in2} \) increases from negative to positive, \( I_{D1} \) decreases from \( I_{SS} \) to 0, while \( I_{D2} \) increases from 0 to \( I_{SS} \).
- At \( V_{in1} - V_{in2} = 0 \), both currents are equal at \( \frac{I_{SS}}{2} \).

4. **Key Features and Technical Details:**
- The maximum current \( I_{SS} \) is reached by one of the currents as the input difference approaches its maximum value in either direction.
- The currents transition smoothly from one extreme to the other, indicating the full steering of the tail current \( I_{SS} \) between the two transistors in the differential pair.

5. **Annotations and Specific Data Points:**
- The graph is annotated with \( I_{SS} \), \( \frac{I_{SS}}{2} \), and the points \( \pm \Delta V_{in,max} \) on the input axis.
- The symmetry of the graph illustrates the balanced nature of the differential pair operation.
image_name:(b)
description:The graph labeled as (b) is a plot illustrating the variation of the difference between drain currents (ID1 and ID2) as a function of the input voltage difference \( V_{in1} - V_{in2} \).

1. **Type of Graph and Function:**
- This is a linear graph depicting the relationship between the input voltage difference and the drain currents in a differential pair configuration.

2. **Axes Labels and Units:**
- The horizontal axis represents the input voltage difference \( V_{in1} - V_{in2} \), with units likely in volts.
- The vertical axis represents the drain currents \( I_{D1} \) and \( I_{D2} \), with units likely in amperes.

3. **Overall Behavior and Trends:**
- The graph shows two curves, \( I_{D1} \) and \( I_{D2} \), which are symmetric about the vertical axis at \( V_{in1} - V_{in2} = 0 \).
- As \( V_{in1} - V_{in2} \) increases from negative to positive, \( I_{D1} \) decreases from the maximum current \( I_{SS} \) to zero, while \( I_{D2} \) increases from zero to \( I_{SS} \).
- Conversely, as \( V_{in1} - V_{in2} \) decreases from positive to negative, \( I_{D1} \) increases from zero to \( I_{SS} \) and \( I_{D2} \) decreases from \( I_{SS} \) to zero.

4. **Key Features and Technical Details:**
- The maximum and minimum points for \( I_{D1} \) and \( I_{D2} \) occur at \( \pm \Delta V_{in, max} \), where one current reaches \( I_{SS} \) and the other reaches zero.
- At \( V_{in1} - V_{in2} = 0 \), both currents are equal to \( I_{SS}/2 \), indicating a balanced condition.

5. **Annotations and Specific Data Points:**
- The graph is annotated with \( I_{SS} \) as the total current, and \( I_{SS}/2 \) as the balanced current level for each drain.
- The points \( \pm \Delta V_{in, max} \) are marked to indicate the maximum input voltage differences where the currents reach their extreme values.
image_name:(c)
description:The graph in Figure 10.31(c) is a plot of differential output voltage as a function of the input difference \(V_{in1} - V_{in2}\). The x-axis represents the input voltage difference \(V_{in1} - V_{in2}\), and the y-axis represents the differential output voltage. The graph is centered around the origin (0,0) on the x-axis, with the input difference varying from negative to positive values, denoted as \(-\Delta V_{in, max}\) to \(+\Delta V_{in, max}\).

The graph shows a symmetrical shape about the y-axis, indicating that the differential output voltage is a function of the absolute value of the input difference. The overall behavior is a smooth, continuous curve that increases in magnitude as the input difference moves away from zero, either in the positive or negative direction.

Key features of the graph include:
- At \(V_{in1} - V_{in2} = 0\), the differential output voltage is zero, indicating no difference in the output.
- As \(V_{in1} - V_{in2}\) increases or decreases, the differential output voltage increases, showing a linear-like behavior initially, followed by a saturation as it approaches \(\pm \Delta V_{in, max}\).
- The curve appears to reach a maximum plateau, indicating a saturation level where further increases in \(V_{in1} - V_{in2}\) do not significantly affect the output voltage.

This graph is typical of a differential amplifier output, where the output voltage is proportional to the difference between the two input voltages, up to a certain limit, beyond which it saturates due to the non-linear characteristics of the amplifier.

(a)
image_name:(b)
description:The graph in Figure 10.31(b) is a plot of the difference between drain currents \(I_{D1} - I_{D2}\) as a function of the input voltage difference \(V_{in1} - V_{in2}\). This graph is typical of a differential amplifier, where the output (in this case, the difference in drain currents) is proportional to the input difference up to a certain point, beyond which saturation occurs.

1. **Type of Graph and Function:**
- This is a linear graph with saturation, commonly seen in differential amplifier characteristics.

2. **Axes Labels and Units:**
- The x-axis represents the input voltage difference \(V_{in1} - V_{in2}\), with no specific units indicated but typically in volts.
- The y-axis represents the difference between drain currents \(I_{D1} - I_{D2}\), also without specific units but typically in amperes.
- The graph is linear, with no logarithmic scale.

3. **Overall Behavior and Trends:**
- The graph shows a linear region around the origin where the output current difference is directly proportional to the input voltage difference.
- As \(V_{in1} - V_{in2}\) increases or decreases beyond \(\pm \Delta V_{in,max}\), the curve reaches a plateau, indicating saturation.
- The saturation levels are at \(+I_{SS}\) and \(-I_{SS}\), meaning further increases in the input difference do not significantly change the current difference.

4. **Key Features and Technical Details:**
- The graph has a central linear region that transitions smoothly into saturation levels at both positive and negative extremes.
- The saturation occurs at \(+\Delta V_{in,max}\) and \(-\Delta V_{in,max}\).
- The saturation current levels are marked as \(+I_{SS}\) and \(-I_{SS}\).

5. **Annotations and Specific Data Points:**
- The graph is annotated with \(-\Delta V_{in,max}\), \(+\Delta V_{in,max}\), \(+I_{SS}\), and \(-I_{SS}\) to indicate the saturation points and levels.
- The origin is marked as a reference point for the linear region.

(b)
image_name:Figure 10.31(c)
description:The graph in Figure 10.31(c) illustrates the differential output voltage \(V_{out1} - V_{out2}\) as a function of the input voltage difference \(V_{in1} - V_{in2}\). The graph is plotted on a Cartesian plane with the horizontal axis representing the input voltage difference \(V_{in1} - V_{in2}\) and the vertical axis representing the differential output voltage \(V_{out1} - V_{out2}\).

Axes Labels and Units:
- **Horizontal Axis:** Labeled as \(V_{in1} - V_{in2}\), indicating the difference in input voltages.
- **Vertical Axis:** Labeled as \(V_{out1} - V_{out2}\), indicating the difference in output voltages.
- Units are not explicitly mentioned, but they are typically in volts.

Overall Behavior and Trends:
- The graph shows a characteristic S-shaped curve, indicating a non-linear relationship.
- It exhibits a linear region around the origin where the output voltage difference changes proportionally with the input voltage difference.
- Beyond certain threshold values \(-\Delta V_{in,max}\) and \(+\Delta V_{in,max}\), the curve levels off, indicating saturation.

Key Features and Technical Details:
- The graph is symmetric around the origin.
- **Saturation Points:**
- Positive saturation occurs at \(+\Delta V_{in,max}\), where the output voltage difference reaches \(+R_D I_{SS}\).
- Negative saturation occurs at \(-\Delta V_{in,max}\), where the output voltage difference reaches \(-R_D I_{SS}\).
- The linear region is centered around the origin \(0\), where the input and output voltage differences are zero.

Annotations and Specific Data Points:
- The graph is annotated with critical points \(-\Delta V_{in,max}\), \(+\Delta V_{in,max}\), \(+R_D I_{SS}\), and \(-R_D I_{SS}\) to indicate the saturation levels and threshold voltages.
- Dashed lines are used to visually mark the saturation levels and the linear region boundaries.

(c)

Figure 10.31 Variation of (a) drain currents, (b) the difference between drain currents, and (c) differential output voltage as a function of input.
input difference. Equation (10.146) provides a great deal of intuition into the operation of the MOS pair. Specifically, we plot $I_{D 1}$ and $I_{D 2}$ as in Fig. 10.31(a), where $\Delta V_{i n}=V_{i n 1}-V_{i n 2}$, arriving at the differential characteristics in Figs. 10.31(b) and (c). The circuit thus behaves linearly for small values of $\Delta V_{\text {in }}$ and becomes completely nonlinear for $\Delta V_{\text {in }}>\Delta V_{i n, \max }$. In other words, $\Delta V_{\text {in,max }}$ serves as an absolute bound on the input signal levels that have any effect on the output.

Example <br> Examine the input/output characteristic of a MOS differential pair if (a) the tail current

10.19 is doubled, or (b) the transistor aspect ratio is doubled.

Solution (a) Equation (10.145) suggests that doubling $I_{S S}$ increases $\Delta V_{i n, \max }$ by a factor of $\sqrt{2}$. Thus, the characteristic of Fig. 10.31(c) expands horizontally. Furthermore, since $I_{S S} R_{D}$ doubles, the characteristic expands vertically as well. Figure 10.32(a) illustrates the result, displaying a greater slope.
(b) Doubling $W / L$ lowers $\Delta V_{i n, \max }$ by a factor of $\sqrt{2}$ while maintaining $I_{S S} R_{D}$ constant. The characteristic therefore contracts horizontally [Fig. 10.32(b)], exhibiting a larger slope in the vicinity of $\Delta V_{i n}=0$.

Exercise Repeat the above example if (a) the tail current is halved, or (b) the transistor aspect ratio is halved.

image_name:(a)
description:The graph labeled (a) illustrates the voltage difference \( V_{out1} - V_{out2} \) against the differential input voltage \( V_{in1} - V_{in2} \) for an NMOS differential pair. The graph is a plot typically used in analog circuit design to show the transfer characteristics of a differential amplifier.

1. **Type of Graph and Function:**
- This is a transfer characteristic graph showing the relationship between the output differential voltage and the input differential voltage.

2. **Axes Labels and Units:**
- The horizontal axis represents \( V_{in1} - V_{in2} \), which is the differential input voltage.
- The vertical axis represents \( V_{out1} - V_{out2} \), which is the differential output voltage.
- Units for both axes are in volts.

3. **Overall Behavior and Trends:**
- The graph shows a nonlinear relationship between the input and output voltages.
- The curve is S-shaped, indicating that for small input voltage differences near zero, the output changes linearly with a larger slope.
- As the input voltage difference increases positively or negatively, the slope decreases, showing saturation behavior.

4. **Key Features and Technical Details:**
- At \( V_{in1} - V_{in2} = 0 \), the slope is maximum, indicating high sensitivity to input changes.
- The graph shows saturation effects at both positive and negative extremes of \( V_{in1} - V_{in2} \).
- The output voltage saturates at approximately \( +2R_D I_{SS} \) and \( -2R_D I_{SS} \), where \( R_D \) is the load resistance and \( I_{SS} \) is the tail current.
- The key points are annotated with \( \pm \Delta V_{in, max} \) and \( \pm \sqrt{2} \Delta V_{in, max} \), indicating maximum input voltage swings.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for key points such as \( \pm \Delta V_{in, max} \) and \( \pm \sqrt{2} \Delta V_{in, max} \) on the input axis.
- The output axis is annotated with \( \pm R_D I_{SS} \) and \( \pm 2R_D I_{SS} \), showing the saturation levels.
image_name:(b)
description:The graph labeled (b) is a plot of the differential output voltage \( V_{out1} - V_{out2} \) versus the differential input voltage \( V_{in1} - V_{in2} \) for an NMOS differential pair.

Type of Graph and Function:
This is a voltage transfer characteristic graph showing the relationship between input and output voltages in a differential pair.

Axes Labels and Units:
- **Horizontal Axis:** Represents the differential input voltage \( V_{in1} - V_{in2} \).
- **Vertical Axis:** Represents the differential output voltage \( V_{out1} - V_{out2} \).
- No specific units are given, but it is implied that both axes are in volts.

Overall Behavior and Trends:
- The graph exhibits an S-shaped curve with a steep slope around the origin \( V_{in1} - V_{in2} = 0 \).
- As the input voltage increases or decreases from zero, the output voltage initially increases or decreases linearly, then levels off, indicating saturation.

Key Features and Technical Details:
- The graph is symmetric around the origin.
- The maximum differential input voltage \( \pm \Delta V_{in, max} \) is marked on the horizontal axis.
- The corresponding maximum output voltage levels \( \pm R_D I_{SS} \) are marked on the vertical axis.
- Notably, the slopes near the origin are sharper compared to other regions, indicating higher gain.
- The graph shows a linear region between \( -\Delta V_{in, max}/\sqrt{2} \) and \( +\Delta V_{in, max}/\sqrt{2} \), where the gain is approximately constant.

Annotations and Specific Data Points:
- Critical points such as \( \pm \Delta V_{in, max} \) and \( \pm R_D I_{SS} \) are annotated on the graph.
- The graph also highlights the points \( \pm \Delta V_{in, max}/\sqrt{2} \) on the input voltage axis, indicating the boundaries of the linear region.

Figure 10.32

Solution The tail current must not exceed $3 \mathrm{~mW} / 1.8 \mathrm{~V}=1.67 \mathrm{~mA}$. From Eq. (10.145), we write

$$
\begin{align*}
\frac{W}{L} & =\frac{2 I_{S S}}{\mu_{n} C_{o x} \Delta V_{i n, \max }^{2}}  \tag{10.147}\\
& =133.6 \tag{10.148}
\end{align*}
$$

The value of the load resistors is determined by the required voltage gain.

Exercise How does the above design change if the power budget is raised to 5 mW ?

### 10.3.3 Small-Signal Analysis

The small-signal analysis of the MOS differential pair proceeds in a manner similar to that in Section 10.2.3 for the bipolar counterpart. The definition of "small" signals in this case can be seen from Eq. (10.142); if

$$
\begin{equation*}
\left|V_{i n 1}-V_{i n 2}\right| \ll \frac{4 I_{S S}}{\mu_{n} C_{o x} \frac{W}{L}}, \tag{10.149}
\end{equation*}
$$

then

$$
\begin{align*}
I_{D 1}-I_{D 2} & \approx \frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{i n 1}-V_{i n 2}\right) \sqrt{\frac{4 I_{S S}}{\mu_{n} C_{o x} \frac{W}{L}}}  \tag{10.150}\\
& =\sqrt{\mu_{n} C_{o x} \frac{W}{L} I_{S S}\left(V_{i n 1}-V_{i n 2}\right) .} \tag{10.151}
\end{align*}
$$

Now, the differential inputs and outputs are linearly proportional, and the circuit operates linearly.

We now use the small-signal model to prove that the tail node remains constant in the presence of small differential inputs. If $\lambda=0$, the circuit reduces to that shown in Fig. 10.33(a), yielding

$$
\begin{align*}
v_{i n 1}-v_{1} & =v_{i n 2}-v_{2}  \tag{10.152}\\
g_{m 1} v_{1}+g_{m 2} v_{2} & =0 \tag{10.153}
\end{align*}
$$

Assuming perfect symmetry, we have from Eq. (10.153)

$$
\begin{equation*}
v_{1}=-v_{2} \tag{10.154}
\end{equation*}
$$

and for differential inputs, we require $v_{i n 1}=-v_{i n 2}$. Thus, Eq. (10.152) translates to

$$
\begin{equation*}
v_{i n 1}=v_{1} \tag{10.155}
\end{equation*}
$$

and hence

$$
\begin{align*}
v_{P} & =v_{i n 1}-v_{1}  \tag{10.156}\\
& =0 \tag{10.157}
\end{align*}
$$

Alternatively, we can simply utilize Eqs. (10.81)-(10.86) with the observation that $v_{\pi} / r_{\pi}=0$ for a MOSFET, arriving at the same result.
image_name:(a)
description:
[
name: Vin1, type: VoltageSource, value: Vin1, ports: {Np: vin1, Nn: GND}
name: Vin2, type: VoltageSource, value: Vin2, ports: {Np: vin2, Nn: GND}
name: RD, type: Resistor, value: RD, ports: {N1: GND, N2: P}
name: P1, type: VoltageControlledCurrentSource, ports: {Np: P, Nn: v1}
name: P2, type: VoltageControlledCurrentSource, ports: {Np: P, Nn: v2}
]
extrainfo:The circuit diagram (a) represents a small-signal model of a MOS differential pair. Node P acts as a virtual ground. The circuit utilizes voltage-controlled current sources with transconductance values gm1 and gm2.
image_name:(b)
description:
[
name: Vin1, type: VoltageSource, value: Vin1, ports: {Np: vin1, Nn: GND}
name: Vin2, type: VoltageSource, value: Vin2, ports: {Np: vin2, Nn: GND}
name: RC, type: Resistor, value: RC, ports: {N1: P, N2: GND}
name: P1, type: VoltageControlledCurrentSource, ports: {Np: P, Nn: v1}
name: P2, type: VoltageControlledCurrentSource, ports: {Np: P, Nn: v2}
]
extrainfo:The circuit is a simplified small-signal model of a MOS differential pair with node P acting as a virtual ground. The resistors RC are connected to ground, and the voltage-controlled current sources represent the transconductance of the MOSFETs.

(b)

Figure 10.33 (a) Small-signal model of MOS differential pair, (b) simplified circuit.

With node $P$ acting as a virtual ground, the concept of half circuit applies, leading to the simplified topology in Fig. 10.33(b). Here,

$$
\begin{align*}
& v_{\text {out } 1}=-g_{m} R_{D} v_{\text {in } 1}  \tag{10.158}\\
& v_{\text {out } 2}=-g_{m} R_{D} v_{\text {in } 2} \tag{10.159}
\end{align*}
$$

and, therefore,

$$
\begin{equation*}
\frac{v_{\text {out } 1}-v_{\text {out } 2}}{v_{\text {in } 1}-v_{\text {in } 2}}=-g_{m} R_{D} \tag{10.160}
\end{equation*}
$$

Example
Prove that Eq. (10.151) can also yield the differential voltage gain.
10.21

Solution $\quad$ Since $V_{\text {out } 1}-V_{\text {our } 2}=-R_{D}\left(I_{D 1}-I_{D 2}\right)$ and since $g_{m}=\sqrt{\mu_{n} C_{o x}(W / L) I_{S S}}$ (why?), we have from Eq. (10.151)

$$
\begin{align*}
V_{\text {out } 1}-V_{\text {out } 2} & =-R_{D} \sqrt{\mu_{n} C_{o x} \frac{W}{L} I_{S S}}\left(V_{\text {in } 1}-V_{\text {in } 2}\right)  \tag{10.161}\\
& =-g_{m} R_{D}\left(V_{\text {in } 1}-V_{\text {in } 2}\right) . \tag{10.162}
\end{align*}
$$

This is, of course, to be expected. After all, small-signal operation simply means approximating the input/output characteristic [Eq. (10.142)] with a straight line [Eq. (10.151)] around an operating point (equilibrium).

Exercise Using the equation $g_{m}=2 I_{D} /\left(V_{G S}-V_{T H}\right)$, express the above result in terms of the equilibrium overdrive voltage.

As with the bipolar circuits studied in Examples 10.10 and 10.14, the analysis of MOS differential topologies is greatly simplified if virtual grounds can be identified. The following examples reinforce this concept.

Example Determine the voltage gain of the circuit shown in Fig. 10.34(a). Assume $\lambda \neq 0$.
10.22
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: S1S2, D: Vout, G: Vin1}
name: M2, type: NMOS, ports: {S: S1S2, D: Vout, G: Vin2}
name: M3, type: PMOS, ports: {S: VDD, D: Vout, G: Vout}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: Vout}
name: I_SS, type: CurrentSource, value: I_SS, ports: {Np: S1S2, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with NMOS transistors M1 and M2 forming the input differential pair, and PMOS transistors M3 and M4 as active loads. The current source I_SS provides the biasing current. The circuit aims to amplify the difference between Vin1 and Vin2, with Vout as the output node.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout1, G: Vin1}
name: M3, type: PMOS, ports: {S: GND, D: Vout1, G: Vout}
]
extrainfo:The circuit diagram (b) is a simplified half-circuit of a differential pair with a current source bias. It consists of an NMOS transistor (M1) and a PMOS transistor (M3). The NMOS M1 is connected to the input voltage Vin1, and its drain is connected to the output node Vout1. The PMOS M3 is connected to the output node Vout1 and is biased by the output voltage Vout.

Figure 10.34

Solution Drawing the half circuit as in Fig. 10.34(b), we note that the total resistance seen at the drain of $M_{1}$ is equal to $\left(1 / g_{m 3}\right)\left\|r_{O 3}\right\| r_{O 1}$. The voltage gain is therefore equal to

$$
\begin{equation*}
A_{v}=-g_{m 1}\left(\frac{1}{g_{m 3}}\left\|r_{O 3}\right\| r_{O 1}\right) \tag{10.163}
\end{equation*}
$$

Exercise $\quad$ Repeat the above example if a resistance of value $R_{1}$ is inserted in series with the sources of $M_{3}$ and $M_{4}$.

Example Assuming $\lambda=0$, compute the voltage gain of the circuit illustrated in Fig. 10.35(a).
10.23
image_name:Fig. 10.35(a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: Voutn, G: Vin1}
name: M2, type: NMOS, ports: {S: Q, D: Voutp, G: Vin2}
name: M3, type: NMOS, ports: {S: GND, D: Voutn, G: Vout}
name: M4, type: NMOS, ports: {S: GND, D: Voutp, G: Vout}
name: ISS1, type: CurrentSource, ports: {Np: P, Nn: GND}
name: ISS2, type: CurrentSource, ports: {Np: Q, Nn: GND}
]
extrainfo:The circuit is a differential pair with NMOS transistors M1 and M2 acting as input transistors. M3 and M4 are the load transistors. ISS1 and ISS2 are current sources providing biasing. The circuit is powered by VDD.
image_name:Fig. 10.35(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Voutn, G: Vin1}
name: M3, type: NMOS, ports: {S: GND, D: Vout, G: Voutn}
name: ISS1, type: CurrentSource, ports: {Np: GND, Nn: P}
]
extrainfo:The circuit is a simplified half-circuit representation with NMOS transistors M1 and M3, and a current source ISS1. Nodes P and Q are virtual grounds.

(a)
(b)

Figure 10.35

Solution Identifying both nodes $P$ and $Q$ as virtual grounds, we construct the half circuit shown in Fig. 10.35(b), and write

$$
\begin{equation*}
A_{v}=-\frac{g_{m 1}}{g_{m 3}} \tag{10.164}
\end{equation*}
$$

Exercise Repeat the above example if $\lambda \neq 0$.

Example 10.24

Assuming $\lambda=0$, calculate the voltage gain of the topology shown in Fig. 10.36(a).
image_name:Figure 10.36(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Voutp, G: Vin1}
name: M2, type: NMOS, ports: {S: GND, D: Vouth, G: Vin2}
name: RDD, type: Resistor, value: RDD, ports: {N1: Voutp, N2: Vouth}
name: RSS, type: Resistor, value: RSS, ports: {N1: GND, N2: S1}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: Voutp, type: VoltageSource, value: Voutp, ports: {Np: Vout, Nn: Voutp}
name: Vouth, type: VoltageSource, value: Vouth, ports: {Np: Vout, Nn: Vouth}
name: S1, type: CurrentSource, value: S1, ports: {Np: Voutp, Nn: GND}
name: S2, type: CurrentSource, value: S2, ports: {Np: Vouth, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with NMOS transistors M1 and M2, and resistors RDD and RSS. It uses current sources S1 and S2 for biasing, and VDD as the power supply. The outputs are taken from Voutp and Vouth.

(a)
image_name:Figure 10.36(b)
description:
[
name: R_DD/2, type: Resistor, value: R_DD/2, ports: {N1: Vout1, N2: GND}
name: M1, type: NMOS, ports: {S: GND, D: Vout1, G: Vin1}
name: R_SS/2, type: Resistor, value: R_SS/2, ports: {N1: Vin1, N2: GND}
]
extrainfo:The circuit is a simplified half-circuit of a differential amplifier, showing one NMOS transistor M1 with resistors R_DD/2 and R_SS/2. The input is applied at Vin1, and the output is taken from Vout1.

(b)

Figure 10.36

Solution Grounding the midpoint of $R_{S S}$ and $R_{D D}$, we obtain the half circuit in Fig. 10.36(b), where

$$
\begin{equation*}
A_{v}=-\frac{\frac{R_{D D}}{2}}{\frac{R_{S S}}{2}+\frac{1}{g_{m}}} \tag{10.165}
\end{equation*}
$$

Exercise Repeat the above example if the load current sources are replaced with diode-connected PMOS devices.

## 10.4 CASCODE DIFFERENTIAL AMPLIFIERS

Recall from Chapter 9 that cascode stages provide a substantially higher voltage gain than simple CE and CS stages do. Noting that the differential gain of differential pairs is equal to the single-ended gain of their corresponding half circuits, we surmise that cascoding boosts the gain of differential pairs as well.

We begin our study with the structure depicted in Fig. 10.37(a), where $Q_{3}$ and $Q_{4}$ serve as cascode devices and $I_{1}$ and $I_{2}$ are ideal. Recognizing that the bases of $Q_{3}$ and $Q_{4}$ are at ac ground, we construct the half circuit shown in Fig. 10.37(b). Equation (9.51) readily gives the gain as

$$
\begin{equation*}
A_{v}=-g_{m 1}\left[g_{m 3}\left(r_{O 1} \| r_{\pi 3}\right) r_{O 3}+r_{O 1} \| r_{\pi 3}\right], \tag{10.166}
\end{equation*}
$$

confirming that a differential cascode achieves a much higher gain.
The developments in Chapter 9 also suggest the use of $p n p$ cascodes for current sources $I_{1}$ and $I_{2}$ in Fig. 10.37(a). Illustrated in Fig. 10.38(a), the resulting configuration can be analyzed with the aid of its half circuit, Fig. 10.38(b). Utilizing Eq. (9.61), we express the voltage gain as

$$
\begin{equation*}
A_{v} \approx-g_{m 1}\left[g_{m 3} r_{O 3}\left(r_{O 1} \| r_{\pi 3}\right)\right] \|\left[g_{m 5} r_{O 5}\left(r_{O 7} \| r_{\pi 5}\right)\right] . \tag{10.167}
\end{equation*}
$$

image_name:Figure 10.37 (a)
description:
[
name: Q1, type: NPN, ports: {C: X, B: Vin1, E: GND}
name: Q2, type: NPN, ports: {C: Voutp, B: Vin2, E: X}
name: Q3, type: NPN, ports: {C: Voutn, B: Vb, E: X}
name: Q4, type: NPN, ports: {C: Vout, B: Vb, E: Voutp}
name: I1, type: CurrentSource, value: I1, ports: {Np: VCC, Nn: Voutn}
name: I2, type: CurrentSource, value: I2, ports: {Np: VCC, Nn: Voutp}
name: I_EE, type: CurrentSource, value: I_EE, ports: {Np: X, Nn: GND}
]
extrainfo:The circuit is a bipolar cascode differential pair with cascode loads, designed for high gain and high output impedance. It uses NPN transistors Q1 and Q2 as the input differential pair, with Q3 and Q4 as cascode transistors. Current sources I1 and I2 provide biasing for the cascode loads, while I_EE sets the tail current for the differential pair.

(a)
image_name:Figure 10.37 (a)
description:
[
name: Q1, type: NPN, ports: {C: c1e3, B: Vin1, E: GND}
name: Q3, type: NPN, ports: {C: Vout1, B: GND, E: c1e3}
]
extrainfo:The circuit is a part of a bipolar cascode differential pair with transistors Q1 and Q3 forming a cascode stage. Q1 is the input transistor, and Q3 is the cascode transistor. The configuration enhances output impedance and gain.

(b)

Figure 10.37 (a) Bipolar cascode differential pair, (b) half circuit of (a).
image_name:Figure 10.37 (a)
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: e1e2, G: Vin1}
name: Q2, type: NMOS, ports: {S: GND, D: e1e2, G: Vin2}
name: Q3, type: NMOS, ports: {S: e1e2, D: Vout, G: Vb1}
name: Q4, type: NMOS, ports: {S: e1e2, D: Vout, G: Vb1}
name: Q5, type: PMOS, ports: {S: Vcc, D: Vout, G: Vb2}
name: Q6, type: PMOS, ports: {S: Vcc, D: Vout, G: Vb2}
name: Q7, type: PMOS, ports: {S: Vcc, D: Vb2, G: Vb3}
name: Q8, type: PMOS, ports: {S: Vcc, D: Vb2, G: Vb3}
name: IEE, type: CurrentSource, ports: {Np: e1e2, Nn: GND}
]
extrainfo:The circuit is a bipolar cascode differential pair with NMOS input transistors (Q1, Q2) and PMOS cascode loads (Q5, Q6). It enhances output impedance and gain, and is part of the internal circuit of some operational amplifiers.
image_name:Figure 10.37 (b)
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: c1e3, G: Vin1}
name: Q3, type: NMOS, ports: {S: c1e3, D: Vout1, G: GND}
name: Q5, type: PMOS, ports: {S: GND, D: Vout1, G: GND}
name: Q7, type: PMOS, ports: {S: GND, D: GND, G: GND}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: c1e3, Nn: GND}
]
extrainfo:The circuit in Figure 10.37(b) is a half circuit of a bipolar cascode differential pair. It includes NMOS transistors Q1 and Q3, and PMOS transistors Q5 and Q7. The circuit is designed to enhance output impedance and gain, and is part of a telescopic cascode topology commonly used in operational amplifiers.

Figure 10.38 (a) Bipolar cascode differential pair with cascode loads, (b) half circuit of (a).

Called a "telescopic cascode," the topology of Fig. 10.38(b) exemplifies the internal circuit of some operational amplifiers.

Example
10.25

Due to a manufacturing defect, a parasitic resistance has appeared between nodes $A$ and $B$ in the circuit of Fig. 10.39(a). Determine the voltage gain of the circuit.
image_name:Figure 10.39(a)
description:
[
name: Q1, type: NPN, ports: {C: Voutp, B: Vb1, E: I_EE}
name: Q2, type: NPN, ports: {C: Voutn, B: Vin2, E: I_EE}
name: Q3, type: NPN, ports: {C: Voutp, B: Vin1, E: I_EE}
name: Q4, type: NPN, ports: {C: Voutn, B: Vb1, E: I_EE}
name: Q5, type: PNP, ports: {C: Voutp, B: Vb2, E: A}
name: Q6, type: PNP, ports: {C: Voutn, B: Vb2, E: B}
name: Q7, type: PNP, ports: {C: A, B: Vb3, E: Vcc}
name: Q8, type: PNP, ports: {C: B, B: Vb3, E: Vcc}
name: R1, type: Resistor, value: R1, ports: {N1: A, N2: B}
name: I_EE, type: CurrentSource, value: I_EE, ports: {Np: I_EE, Nn: GND}
]
extrainfo:The circuit is a bipolar cascode differential pair with cascode loads, featuring a parasitic resistance between nodes A and B. It is used to illustrate a telescopic cascode topology in operational amplifiers. The presence of the parasitic resistance affects the output impedance and consequently the voltage gain of the amplifier.

(a)
image_name:Figure 10.39(b)
description:
[
name: Q7, type: PNP, ports: {C: GND, B: GND, E: R1}
name: Q5, type: PNP, ports: {C: R1, B: GND, E: Q3}
name: Q3, type: NPN, ports: {C: Q5, B: Q1, E: GND}
name: Q1, type: NPN, ports: {C: Q3, B: Vin1, E: GND}
name: R1, type: Resistor, value: R1/2, ports: {N1: GND, N2: Q5}
]
extrainfo:The circuit is a half of a bipolar cascode differential pair with cascode loads. It features a parasitic resistance between nodes A and B, affecting output impedance and voltage gain. The symmetry implies that the midpoint of R1 is a virtual ground, leading to the half circuit shown. The parasitic resistance R1/2 appears in parallel with r_O7, lowering the output impedance of the PNP cascode.

(b)

Figure 10.39

Solution
The symmetry of the circuit implies that the midpoint of $R_{1}$ is a virtual ground, leading to the half circuit shown in Fig. 10.39(b). Thus, $R_{1} / 2$ appears in parallel with $r_{O 7}$, lowering the output impedance of the pnp cascode. Since the value of $R_{1}$ is not given, we cannot
make approximations and must return to the original expression for the cascode output impedance, Eq. (9.1):

$$
\begin{equation*}
R_{o p}=\left[1+g_{m 5}\left(r_{O 7}\left\|r_{\pi 5}\right\| \frac{R_{1}}{2}\right)\right] r_{O 5}+r_{O 7}\left\|r_{\pi 5}\right\| \frac{R_{1}}{2} \tag{10.168}
\end{equation*}
$$

The resistance seen looking down into the $n p n$ cascode remains unchanged and approximately equal to $g_{m 3} r_{O 3}\left(r_{O 1} \| r_{\pi 3}\right)$. The voltage gain is therefore equal to

$$
\begin{equation*}
A_{v}=-g_{m 1}\left[g_{m 3} r_{O 3}\left(r_{O 1} \| r_{\pi 3}\right)\right] \| R_{o p} \tag{10.169}
\end{equation*}
$$

Exercise If $\beta=50$ and $V_{A}=4 \mathrm{~V}$ for all transistors and $I_{E E}=1 \mathrm{~mA}$, what value of $R_{1}$ degrades the gain by a factor of two?
image_name:Figure 10.40 (a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1s3, G: Vin1}
name: M2, type: NMOS, ports: {S: GND, D: d2s4, G: Vin2}
name: M3, type: NMOS, ports: {S: d1s3, D: Vout, G: Vb1}
name: M4, type: NMOS, ports: {S: d2s4, D: Vout, G: Vb1}
name: Iss, type: CurrentSource, ports: {Np: GND, Nn: s1s2}
name: VDD, type: VoltageSource, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a MOS cascode differential pair with a current source biasing the sources of M1 and M2. M3 and M4 form the cascode configuration, enhancing the gain of the differential amplifier.

(a)
image_name:(b)
description:
[
name: M3, type: NMOS, ports: {S: d1s3, D: Vout1, G: GND}
name: M1, type: NMOS, ports: {S: GND, D: d1s3, G: Vin1}
]
extrainfo:The circuit is a half-circuit of a MOS cascode differential pair. M3 and M1 form the cascode configuration, with M1 serving as the input transistor and M3 as the cascode transistor, enhancing gain and output impedance.

(b)

Figure 10.40 (a) MOS cascode differential pair, (b) half circuit of (a).

We now turn our attention to differential MOS cascodes. Following the above developments for bipolar counterparts, we consider the simplified topology of Fig. 10.40(a) and draw the half circuit as depicted in Fig. 10.40(b). From Eq. (9.69),

$$
\begin{equation*}
A_{v} \approx-g_{m 3} r_{O 3} g_{m 1} r_{O 1} \tag{10.170}
\end{equation*}
$$

Illustrated in Fig. 10.41(a), the complete CMOS telescopic cascode amplifier incorporates PMOS cascades as load current sources, yielding the half circuit shown in Fig. 10.41(b). It follows from Eq. (9.72) that the voltage gain is given by

$$
\begin{equation*}
A_{v} \approx-g_{m 1}\left[\left(g_{m 3} r_{O 3} r_{O 1}\right) \|\left(g_{m 5} r_{O 5} r_{O 7}\right)\right] \tag{10.171}
\end{equation*}
$$

Did you know?

Most stand-alone bipolar op amps do not use the telescopic cascode differential pair. One reason may be that the input common-mode range of this circuit is quite limited, a serious issue for generalpurpose op amps. In analog integrated circuits, on the other hand, telescopic cascode op amps have been utilized extensively because they provide a high voltage gain and have a better high-frequency behavior than other op amp topologies. If you open up your WiFi or cell phone receiver, it is likely that you will see some analog filters and analog-todigital converters using telescopic op amps.

Due to a manufacturing defect, two equal parasitic resistances, $R_{1}$ and $R_{2}$, have appeared as shown in Fig. 10.42(a). Compute the voltage gain of the circuit.
image_name:Figure 10.41 (a)
description:
[
name: M7, type: PMOS, ports: {S: VDD, D: ss7d7, G: Vb3}
name: M8, type: PMOS, ports: {S: VDD, D: s6d8, G: Vb3}
name: M5, type: PMOS, ports: {S: ss7d7, D: d1s3, G: Vb2}
name: M6, type: PMOS, ports: {S: s6d8, D: Vout, G: Vb2}
name: M3, type: NMOS, ports: {S: d1s3, D: GND, G: Vb1}
name: M4, type: NMOS, ports: {S: Vout, D: d2s4, G: Vb1}
name: M1, type: NMOS, ports: {S: GND, D: d1s3, G: Vin1}
name: M2, type: NMOS, ports: {S: GND, D: d2s4, G: Vin2}
name: Iss, type: CurrentSource, ports: {Np: GND, Nn: GND}
]
extrainfo:The circuit is a telescopic cascode amplifier with PMOS and NMOS transistors. It uses bias voltages Vb1, Vb2, and Vb3 for gate control of the transistors. The amplifier is designed for high voltage gain and improved high-frequency behavior. Parasitic resistances R1 and R2 are present in parallel with the output impedances.

(a)
image_name:Figure 10.41 (a)
description:
[
name: M7, type: PMOS, ports: {S: GND, D: s5d7, G: GND}
name: M5, type: PMOS, ports: {S: GND, D: s5d7, G: GND}
name: M3, type: NMOS, ports: {S: d1s3, D: Vout1, G: s5d7}
name: M1, type: NMOS, ports: {S: GND, D: d1s3, G: Vin1}
]
extrainfo:The circuit is a telescopic cascode amplifier with a combination of PMOS and NMOS transistors, designed for high voltage gain and improved high-frequency behavior. Parasitic resistances R1 and R2 are present in parallel with the output impedances.

(b)

Figure 10.41 (a) MOS telescopic cascode amplifier, (b) half circuit of (a).

Solution Noting that $R_{1}$ and $R_{2}$ appear in parallel with $r_{O 5}$ and $r_{O 6}$, respectively, we draw the half circuit as depicted in Fig. 10.42(b). Without the value of $R_{1}$ given, we must resort to the original expression for the output impedance, Eq. (9.3):

$$
\begin{equation*}
R_{p}=\left[1+g_{m 5}\left(r_{O 5} \| R_{1}\right)\right] r_{O 7}+r_{O 5} \| R_{1} \tag{10.172}
\end{equation*}
$$

The resistance seen looking into the drain of the NMOS cascode can still be approximated as

$$
\begin{equation*}
R_{n} \approx g_{m 3} r_{O 3} r_{O 1} \tag{10.173}
\end{equation*}
$$

The voltage gain is then simply equal to

$$
\begin{equation*}
A_{v}=-g_{m 1}\left(R_{p} \| R_{n}\right) \tag{10.174}
\end{equation*}
$$

image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: s1s2, D: Voutn, G: Vin1}
name: M2, type: NMOS, ports: {S: s1s2, D: Voutp, G: Vin2}
name: M3, type: NMOS, ports: {S: Voutn, D: Vout, G: Vb1}
name: M4, type: NMOS, ports: {S: Voutp, D: Vout, G: Vb1}
name: M5, type: PMOS, ports: {S: VDD, D: s5d7, G: Vb2}
name: M6, type: PMOS, ports: {S: VDD, D: s6d8, G: Vb2}
name: M7, type: PMOS, ports: {S: s5d7, D: Voutn, G: Vb3}
name: M8, type: PMOS, ports: {S: s6d8, D: Voutp, G: Vb3}
name: R1, type: Resistor, value: R1, ports: {N1: s5d7, N2: Voutn}
name: R2, type: Resistor, value: R2, ports: {N1: s6d8, N2: Voutp}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: s1s2, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with cascode configuration, utilizing NMOS and PMOS transistors to achieve high gain. It features a current source Iss connected to the sources of M1 and M2, and resistors R1 and R2 connected between the PMOS transistors and the output nodes.

(a)
image_name:(a)
description:
[
name: M7, type: PMOS, ports: {S: GND, D: s5d7, G: GND}
name: M5, type: PMOS, ports: {S: GND, D: s5d7, G: GND}
name: M3, type: NMOS, ports: {S: d1s3, D: Vout1, G: GND}
name: M1, type: NMOS, ports: {S: GND, D: d1s3, G: Vin1}
name: R1, type: Resistor, value: R1, ports: {N1: s5d7, N2: Vout1}
]
extrainfo:The circuit is a differential amplifier with a cascode configuration. It includes PMOS transistors M7 and M5, NMOS transistors M3 and M1, and a resistor R1. The PMOS transistors are connected to the node s5d7, which is also connected to one end of R1. The NMOS transistors form the differential pair, with M3 connected to the output node Vout1. The circuit is designed to achieve high gain with common-mode rejection properties.

(b)

Figure 10.42

Exercise
Repeat the above example if in addition to $R_{1}$ and $R_{2}$, a resistor of value $R_{3}$ appears between the sources of $M_{3}$ and $M_{4}$.

## 10.5 COMMON-MODE REJECTION

In our study of bipolar and MOS differential pairs, we have observed that these circuits produce no change in the output if the input CM level changes. The common-mode rejection property of differential circuits plays a critical role in today's electronic systems. As the reader may have guessed, in practice the CM rejection is not infinitely high. In this section, we examine the CM rejection in the presence of nonidealities.

The first nonideality relates to the output impedance of the tail current source. Consider the topology shown in Fig. 10.43(a), where $R_{E E}$ denotes the output impedance of $I_{E E}$. What happens if the input CM level changes by a small amount? The symmetry requires that $Q_{1}$ and $Q_{2}$ still carry equal currents and $V_{\text {out } 1}=V_{\text {out } 2}$. But, since the base voltages of both $Q_{1}$ and $Q_{2}$ rise, so does $V_{P}$. In fact, noting that $V_{\text {out } 1}=V_{\text {out } 2}$, we can place a short circuit between the output nodes, reducing the topology to that shown in Fig. 10.43(b). That is, as far as node $P$ is concerned, $Q_{1}$ and $Q_{2}$ operate as an emitter follower. As $V_{P}$ increases, so does the current through $R_{E E}$ and hence the collector currents of $Q_{1}$ and $Q_{2}$. Consequently, the output common-mode level falls. The change in the output CM level can be computed by noting that the stage in Fig. 10.43(b) resembles a degenerated CE stage. That is, from Chapter 5,

$$
\begin{align*}
\frac{\Delta V_{\text {out }, C M}}{\Delta V_{i n, C M}} & =-\frac{\frac{R_{C}}{2}}{R_{E E}+\frac{1}{2 g_{m}}}  \tag{10.175}\\
& =-\frac{R_{C}}{2 R_{E E}+g_{m}^{-1}}, \tag{10.176}
\end{align*}
$$

where the term $2 g_{m}$ represents the transconductance of the parallel combination of $Q_{1}$ and $Q_{2}$. This quantity is called the "common-mode gain." These observations apply to the MOS counterpart equally well. An alternative approach to arriving at Eq. (10.175) is outlined in Problem 10.65.

In summary, if the tail current exhibits a finite output impedance, the differential pair produces an output CM change in response to an input CM change. The reader
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: Vout1, B: VCM, E: P}
name: Q2, type: NPN, ports: {C: Vout2, B: VCM, E: P}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Vout1}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Vout2}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: VCM, type: VoltageSource, value: VCM, ports: {Np: VCM, Nn: GND}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: P, Nn: GND}
name: REE, type: Resistor, value: REE, ports: {N1: P, N2: GND}
]
extrainfo:The circuit is a differential amplifier with NPN transistors Q1 and Q2. It uses a common-mode voltage source VCM and a tail current source IEE. The resistors RC are connected to the collectors of the transistors, and REE is connected to the emitter node P. The circuit is powered by VCC.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: VCM, E: P}
name: Q2, type: NPN, ports: {C: Vout, B: VCM, E: P}
name: RC, type: Resistor, value: RC/2, ports: {N1: VCC, N2: Vout}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: VCM, type: VoltageSource, value: VCM, ports: {Np: VCM, Nn: GND}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: P, Nn: GND}
name: REE, type: Resistor, value: REE, ports: {N1: P, N2: GND}
]
extrainfo:This circuit is a differential pair with a finite tail impedance. The circuit responds to common-mode noise at the input, affecting the output. The use of REE influences the common-mode gain and the output response to input common-mode changes.

Figure 10.43 (a) CM response of differential pair in the presence of finite tail impedance, (b) simplified circuit of (a).
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: Vin1, E: P}
name: Q2, type: NPN, ports: {C: VCC, B: Vin2, E: P}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Vout1}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Vout2}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: Vout1, type: VoltageSource, value: Vout1, ports: {Np: Vout1, Nn: GND}
name: Vout2, type: VoltageSource, value: Vout2, ports: {Np: Vout2, Nn: GND}
name: Vin1, type: VoltageSource, value: Vin1, ports: {Np: Vin1, Nn: GND}
name: Vin2, type: VoltageSource, value: Vin2, ports: {Np: Vin2, Nn: GND}
name: VCM, type: VoltageSource, value: VCM, ports: {Np: VCM, Nn: GND}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: P, Nn: GND}
name: REE, type: Resistor, value: REE, ports: {N1: P, N2: GND}
]
extrainfo:The circuit is a differential pair with finite tail impedance, responding to common-mode noise at the input. The use of REE influences the common-mode gain and output response to input common-mode changes. The waveforms illustrate the differential pair's response to common-mode noise under different conditions of REE.
image_name:(b)
description:Figure 10.44(b) illustrates the output response of a differential pair circuit to common-mode noise, with the condition that the tail resistor \( R_{EE} \) is infinite. The graph is a time-domain waveform depicting the behavior of the output voltages \( V_{out1} \) and \( V_{out2} \), as well as their difference \( V_{out1} - V_{out2} \), over time.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform plot.

2. **Axes Labels and Units:**
- The horizontal axis represents time \( t \), though specific units are not provided.
- The vertical axis represents voltage, but specific units are not given.

3. **Overall Behavior and Trends:**
- \( V_{out1} \) and \( V_{out2} \) are shown as sinusoidal waveforms, indicating a smooth oscillatory behavior over time.
- The difference \( V_{out1} - V_{out2} \) is also a sinusoidal waveform, reflecting the differential nature of the pair.

4. **Key Features and Technical Details:**
- The waveforms of \( V_{out1} \) and \( V_{out2} \) are out of phase, which is typical for differential outputs.
- The sinusoidal shape of \( V_{out1} - V_{out2} \) suggests effective common-mode rejection, as the differential output remains clean and unaffected by common-mode noise.

5. **Annotations and Specific Data Points:**
- No specific numerical values or annotations are provided in the graph.

This graph effectively demonstrates that with \( R_{EE} = \infty \), the differential pair maintains a clean differential output despite the presence of common-mode noise.
image_name:(c)
description:The graph labeled "(c)" illustrates the effect of common-mode (CM) noise on the output of a differential pair circuit with a finite tail impedance, characterized by the presence of a resistor, $R_{EE}$. This graph is a time-domain waveform plot that shows how the outputs $V_{out1}$ and $V_{out2}$ respond to input CM noise.

**Axes Labels and Units:**
- The horizontal axis represents time ($t$), although specific units are not provided.
- The vertical axis represents voltage, but specific units are again not provided.

**Overall Behavior and Trends:**
- The waveforms for $V_{out1}$ and $V_{out2}$ exhibit significant fluctuations due to the CM noise, depicted as jagged or zigzag patterns overlaying the sinusoidal signals.
- Despite the noise, the differential output ($V_{out1} - V_{out2}$) remains a smooth sinusoidal waveform, indicating that the differential pair effectively cancels out the common-mode noise.

**Key Features and Technical Details:**
- The individual outputs ($V_{out1}$ and $V_{out2}$) are affected by the noise, showing distortion from their ideal sinusoidal shapes.
- The differential output waveform is consistent and smooth, suggesting that the common-mode rejection ratio (CMRR) of the circuit is effectively high, mitigating the impact of common-mode noise.

**Annotations and Specific Data Points:**
- The graph does not provide specific numerical values or annotations, focusing instead on the qualitative behavior of the waveforms.

Overall, this graph demonstrates the differential pair's ability to reject common-mode noise, maintaining a clean differential output even when the individual outputs are noisy.

Figure 10.44 (a) Differential pair sensing input CM noise, (b) effect of CM noise at output with $R_{E E}=\infty$, (c) effect of CM noise at the output with $R_{E E} \neq \infty$.
may naturally wonder whether this is a serious issue. After all, so long as the quantity of interest is the difference between the outputs, a change in the output CM level introduces no corruption. Figure 10.44(a) illustrates such a situation. Here, two differential inputs, $V_{i n 1}$ and $V_{i n 2}$, experience some common-mode noise, $V_{i n, C M}$. As a result, the base voltages of $Q_{1}$ and $Q_{2}$ with respect to ground appear as shown in Fig. 10.44(b). With an ideal tail current source, the input CM variation would have no effect at the output, leading to the output waveforms shown in Fig. 10.44(b). On the other hand, with $R_{E E}<\infty$, the single-ended outputs are corrupted, but not the differential output [Fig. 10.44(c)].

In summary, the above study indicates that, in the presence of input CM noise, a finite CM gain does not corrupt the differential output and hence proves benign. ${ }^{4}$ However, if the circuit suffers from asymmetries and a finite tail current source impedance, then the differential output is corrupted. During manufacturing, random "mismatches" appear between the two sides of the differential pair; for example, the transistors or the load resistors may display slightly different dimensions. Consequently, the change in the tail current due to an input CM variation may affect the differential output.

As an example of the effect of asymmetries, we consider the simple case of load resistor mismatch. Depicted in Fig. 10.45(a) for a MOS pair, ${ }^{5}$ this imperfection leads to a difference between $V_{\text {out } 1}$ and $V_{\text {our } 2}$. We must compute the change in $I_{D 1}$ and $I_{D 2}$ and multiply the result by $R_{D}$ and $R_{D}+\Delta R_{D}$.

[^2]image_name:Figure 10.45
description:
[
name: M1, type: NMOS, ports: {S: P, D: Vout1, G: VCM}
name: M2, type: NMOS, ports: {S: P, D: Vout2, G: VCM}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout1}
name: RD+ΔRD, type: Resistor, value: RD+ΔRD, ports: {N1: VDD, N2: Vout2}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: GND}
name: RSS, type: Resistor, value: RSS, ports: {N1: P, N2: GND}
]
extrainfo:The circuit is a differential pair with asymmetric load resistors, RD and RD+ΔRD. The MOS transistors M1 and M2 are driven by the common-mode voltage VCM. The tail current source ISS and resistor RSS provide biasing for the differential pair.

Figure 10.45 MOS pair with asymmetric loads.

How do we determine the change in $I_{D 1}$ and $I_{D 2}$ ? Neglecting channel-length modulation, we first observe that

$$
\begin{align*}
& I_{D 1}=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S 1}-V_{T H}\right)^{2}  \tag{10.177}\\
& I_{D 2}=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S 2}-V_{T H}\right)^{2}, \tag{10.178}
\end{align*}
$$

concluding that $\Delta I_{D 1}$ must be equal to $\Delta I_{D 2}$ because $V_{G S 1}=V_{G S 2}$ and hence $\Delta V_{G S 1}=$ $\Delta V_{G S 2}$. In other words, the load resistor mismatch does not impact the symmetry of currents carried by $M_{1}$ and $M_{2}{ }^{6}$ Writing $\Delta I_{D 1}=\Delta I_{D 2}=\Delta I_{D}$ and $\Delta V_{G S 1}=\Delta V_{G S 2}=\Delta V_{G S}$, we recognize that both $\Delta I_{D 1}$ and $\Delta I_{D 2}$ flow through $R_{S S}$, creating a voltage change of $2 \Delta I_{D} R_{S S}$ across it. Thus,

$$
\begin{equation*}
\Delta V_{C M}=\Delta V_{G S}+2 \Delta I_{D} R_{S S} \tag{10.179}
\end{equation*}
$$

and, since $\Delta V_{G S}=\Delta I_{D} / g_{m}$,

$$
\begin{equation*}
\Delta V_{C M}=\Delta I_{D}\left(\frac{1}{g_{m}}+2 R_{S S}\right) \tag{10.180}
\end{equation*}
$$

That is,

$$
\begin{equation*}
\Delta I_{D}=\frac{\Delta V_{C M}}{\frac{1}{g_{m}}+2 R_{S S}} \tag{10.181}
\end{equation*}
$$

Produced by each transistor, this current change flows through both $R_{D}$ and $R_{D}+\Delta R_{D}$, thereby generating a differential output change of

$$
\begin{align*}
\Delta V_{\text {out }} & =\Delta V_{\text {out } 1}-\Delta V_{\text {out } 2}  \tag{10.182}\\
& =\Delta I_{D} R_{D}-\Delta I_{D}\left(R_{D}+\Delta R_{D}\right)  \tag{10.183}\\
& =-\Delta I_{D} \cdot \Delta R_{D}  \tag{10.184}\\
& =-\frac{\Delta V_{C M}}{\frac{1}{g_{m}}+2 R_{S S}} \Delta R_{D} . \tag{10.185}
\end{align*}
$$

[^3]It follows that

$$
\begin{equation*}
\left|\frac{\Delta V_{\text {out }}}{\Delta V_{C M}}\right|=\frac{\Delta R_{D}}{\frac{1}{g_{m}}+2 R_{S S}} \tag{10.186}
\end{equation*}
$$

(This result can also be obtained through small-signal analysis.) We say the circuit exhibits "common mode to differential mode (DM) conversion" and denote the above gain by $A_{C M-D M}$. In practice, we strive to minimize this corruption by maximizing the output impedance of the tail current source. For example, a bipolar current source may employ emitter degeneration and a MOS current source may incorporate a relatively long transistor. It is therefore reasonable to assume $R_{S S} \gg 1 / g_{m}$ and

$$
\begin{equation*}
A_{C M-D M} \approx \frac{\Delta R_{D}}{2 R_{S S}} \tag{10.187}
\end{equation*}
$$

Example Determine $A_{C M-D M}$ for the circuit shown in Fig. 10.46. Assume $V_{A}=\infty$ for $Q_{1}$ and $Q_{2}$.
10.27
image_name:Figure 10.46
description:
[
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Vout1}
name: RC_Delta, type: Resistor, value: RC + ΔRC, ports: {N1: VCC, N2: Vout2}
name: V_CM, type: VoltageSource, value: V_CM, ports: {Np: VCM, Nn: GND}
name: Q1, type: NPN, ports: {C: Vout1, B: VCM, E: P}
name: Q2, type: NPN, ports: {C: Vout2, B: VCM, E: P}
name: Q3, type: NPN, ports: {C: P, B: Vb, E: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vb, N2: GND}
]
extrainfo:The circuit is a differential amplifier with a current mirror load. It uses emitter degeneration to increase the output impedance of the tail current source. The voltage source V_CM provides common-mode input voltage. The resistors RC and RC + ΔRC are connected to the collectors of Q1 and Q2, respectively, leading to the output nodes Vout1 and Vout2.

Figure 10.46

Solution Recall from Chapter 5 that emitter degeneration raises the output impedance to

$$
\begin{equation*}
R_{\text {out } 3}=\left[1+g_{m 3}\left(R_{1} \| r_{\pi 3}\right)\right] r_{O 3}+R_{1} \| r_{\pi 3} \tag{10.188}
\end{equation*}
$$

Replacing this value for $R_{S S}$ in Eq. (10.186) yields

$$
\begin{equation*}
A_{C M-D M}=\frac{\Delta R_{C}}{\frac{1}{g_{m 1}}+2\left\{\left[1+g_{m 3}\left(R_{1} \| r_{\pi 3}\right)\right] r_{O 3}+R_{1} \| r_{\pi 3}\right\}} \tag{10.189}
\end{equation*}
$$

Exercise $\quad$ Calculate the above result if $R_{1} \rightarrow \infty$.

The mismatches between the transistors in a differential pair also lead to CM-DM conversion. This effect is beyond the scope of this book [1].

While undesirable, CM-DM conversion cannot be simply quantified by $A_{C M-D M}$. If the circuit provides a large differential gain, $A_{D M}$, then the relative corruption at the output is small. We therefore define the "common-mode rejection ratio" (CMRR) as

$$
\begin{equation*}
\text { CMRR }=\frac{A_{D M}}{A_{C M-D M}} \tag{10.190}
\end{equation*}
$$

Representing the ratio of "good" to "bad," CMRR serves as a measure of how much wanted signal and how much unwanted corruption appear at the output if the input consists of a differential component and common-mode noise.

Example

10.28

Calculate the CMRR of the circuit in Fig. 10.46.

Solution For small mismatches (e.g., $1 \%$ ), $\Delta R_{C} \ll R_{C}$, and the differential gain is equal to $g_{m 1} R_{C}$. Thus,

$$
\begin{equation*}
\mathrm{CMRR}=\frac{g_{m 1} R_{C}}{\Delta R_{C}}\left\{\frac{1}{g_{m 1}}+2\left[1+g_{m 3}\left(R_{1} \| r_{\pi 3}\right)\right] r_{O 3}+2\left(R_{1} \| r_{\pi 3}\right)\right\} \tag{10.191}
\end{equation*}
$$

## 10.6 DIFFERENTIAL PAIR WITH ACTIVE LOAD

In this section, we study an interesting combination of differential pairs and current mirrors that proves useful in many applications. To arrive at the circuit, let us first address a problem encountered in some cases.

Recall that the op amps used in Chapter 8 have a differential input but a single-ended output [Fig. 10.47(a)]. Thus, the internal circuits of such op amps must incorporate a stage
image_name:(a)
description:The diagram labeled (a) depicts a simplified operational amplifier (op-amp) configuration with a differential input and a single-ended output. This configuration is crucial for applications where the input signals are differential, meaning two input voltages, \( V_{in1} \) and \( V_{in2} \), are provided to the op-amp. The output, \( V_{out} \), is single-ended, meaning it is referenced to ground (GND).

Main Components:
1. **Differential Input Stage:**
- The op-amp receives two input signals, \( V_{in1} \) and \( V_{in2} \), which are processed by the internal circuitry to produce an output.
- The differential input stage is responsible for amplifying the difference between \( V_{in1} \) and \( V_{in2} \).

2. **Single-Ended Output:**
- The output \( V_{out} \) is taken with respect to ground. This single-ended output is typical in many op-amp applications where the output needs to be referenced to a common ground.

Flow of Information:
- The input signals \( V_{in1} \) and \( V_{in2} \) enter the op-amp through the differential input stage. The op-amp processes these signals to amplify the difference between them.
- The amplified signal is then outputted as \( V_{out} \), referenced to ground.

Labels and Annotations:
- The diagram clearly labels the input and output terminals, aiding in understanding the signal flow.
- The reference to ground (GND) is shown, indicating the single-ended nature of the output.

Overall System Function:
The primary function of this system is to convert a differential input signal into a single-ended output. This is a common requirement in various electronic applications, where the ability to handle differential inputs while providing a single-ended output is necessary for interfacing with other circuit components or systems. The op-amp's differential input stage allows for the amplification of the difference between the two input signals, while the single-ended output provides a straightforward interface for further signal processing or measurement.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: X, E: e1e2}
name: Q2, type: NPN, ports: {C: VCC, B: Y, E: e1e2}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: X}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Y}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: OpAmp, type: OpAmp, ports: {InP: Vin1, InN: Vin2, Out: Vout}
]
extrainfo:The circuit is a differential amplifier with active load using NPN transistors Q1 and Q2. It converts a differential input to a single-ended output. The resistors RC are used as load resistors, and the output is taken from node Y.

Figure 10.47 (a) Circuit with differential input and single-ended output, (b) possible implementation of (a).
that "converts" a differential input to a single-ended output. We may naturally consider the topology shown in Fig. 10.47(b) as a candidate for this task. Here, the output is sensed at node $Y$ with respect to ground rather than with respect to node $X .{ }^{7}$ Unfortunately, the voltage gain is now halved because the signal swing at node $X$ is not used.

We now introduce a topology that serves the task of "differential to single-ended" conversion while resolving the above issues. Shown in Fig. 10.48, the circuit employs a symmetric differential pair, $Q_{1}-Q_{2}$, along with a current-mirror load, $Q_{3}-Q_{4}$. (Transistors $Q_{3}$ and $Q_{4}$ are also identical.) The output is sensed with respect to ground.
image_name:Figure 10.48
description:
[
name: Q1, type: NPN, ports: {C: N, B: Vin1, E: S1S2}
name: Q2, type: NPN, ports: {C: Vout, B: Vin2, E: S1S2}
name: Q3, type: PNP, ports: {C: N, B: N, E: VCC}
name: Q4, type: PNP, ports: {C: Vout, B: N, E: VCC}
name: I_EE, type: CurrentSource, ports: {Np: S1S2, Nn: GND}
]
extrainfo:The circuit is a differential pair with an active load, consisting of a symmetric differential pair (Q1 and Q2) and a current-mirror load (Q3 and Q4). The output is taken with respect to ground.

Figure 10.48 Differential pair with active load.

### 10.6.1 Qualitative Analysis

It is instructive to first decompose the circuit of Fig. 10.48 into two sections: the input differential pair and the current-mirror load. As depicted in Fig. 10.49(a) (along with a fictitious load $R_{L}$ ), $Q_{1}$ and $Q_{2}$ produce equal and opposite changes in their collector currents in response to a differential change at the input, creating a voltage change of $\Delta I R_{L}$ across $R_{L}$. Now consider the circuit in Fig. 10.49(b) and suppose the current drawn from $Q_{3}$ increases from $I_{E E} / 2$ to $I_{E E} / 2+\Delta I$. What happens? First, since the small-signal impedance seen at node $N$ is approximately equal to $1 / g_{m 3}, V_{N}$ changes by $\Delta I / g_{m 3}$ (for small $\Delta I$ ). Second, by virtue of current mirror action, the collector current of $Q_{4}$ also increases by $\Delta I$. As a result, the voltage across $R_{L}$ changes by $\Delta I R_{L}$.
image_name:Figure 10.49 (a)
description:
[
name: Q1, type: NPN, ports: {C: c2, B: Vin, E: P}
name: Q2, type: NPN, ports: {C: Vb, B: Vin, E: P}
name: Q3, type: PNP, ports: {C: N, B: c2, E: VCC}
name: Q4, type: PNP, ports: {C: c4, B: N, E: VCC}
name: I_EE, type: CurrentSource, value: I_EE, ports: {Np: P, Nn: GND}
name: R_L, type: Resistor, value: R_L, ports: {N1: c4, N2: GND}
]
extrainfo:This circuit is a differential amplifier with an active load. Q1 and Q2 form a differential pair, while Q3 and Q4 act as a current mirror load. The current source I_EE provides biasing, and R_L is the load resistor.
image_name:Figure 10.49 (b)
description:
[
name: Q3, type: PNP, ports: {C: VCC, B: N, E: GND}
name: Q4, type: PNP, ports: {C: VCC, B: N, E: c4}
name: I_EE, type: CurrentSource, value: I_EE, ports: {Np: P, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: c4, N2: GND}
]
extrainfo:The circuit in Figure 10.49(b) is a current mirror configuration with transistors Q3 and Q4. The current source I_EE provides a bias current, and the resistor RL is used to convert the output current into a voltage. The node N is a key point for the current mirror action, ensuring that the currents through Q3 and Q4 are matched.

Figure 10.49 (a) Response of input pair to input change, (b) response of active load to current change.
${ }^{7}$ In practice, additional stages precede this stage so as to provide a high gain.
image_name:Figure 10.50
description:
[
name: Q1, type: NPN, ports: {C: N, B: VCM+ΔV, E: P}
name: Q2, type: NPN, ports: {C: Vout, B: VCM-ΔV, E: P}
name: Q3, type: PNP, ports: {C: VCC, B: N, E: Vout}
name: Q4, type: PNP, ports: {C: VCC, B: Vout, E: Vout}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with a current mirror active load. Q3 and Q4 form the current mirror, ensuring equal currents through Q1 and Q2. The resistor RL converts the output current to a voltage at Vout.

Figure 10.50 Detailed operation of pair with active load.

In order to understand the detailed operation of the circuit, we apply small, differential changes at the input and follow the signals to the output (Fig. 10.50). The load resistor, $R_{L}$, is added to augment our intuition but it is not necessary for the actual operation. With the input voltage changes shown here, we note that $I_{C 1}$ increases by some amount $\Delta I$ and $I_{C 2}$ decreases by the same amount. Ignoring the role of $Q_{3}$ and $Q_{4}$ for the moment, we observe that the fall in $I_{C 2}$ translates to a rise in $V_{\text {out }}$ because $Q_{2}$ draws less current from $R_{L}$. The output change can therefore be an amplified version of $\Delta V$.

Let us now determine how the change in $I_{C 1}$ travels through $Q_{3}$ and $Q_{4}$. Neglecting the base currents of these two transistors, we recognize that the change in $I_{C 3}$ is also equal to $\Delta I$. This change is copied into $I_{C 4}$ by virtue of the current mirror action. In other words, in response to the differential input shown in Fig. 10.50, $I_{C 1},\left|I_{C 3}\right|$, and $\left|I_{C 4}\right|$ increase by $\Delta I$. Since $Q_{4}$ "injects" a greater current into the output node, $V_{\text {out }}$ rises.

In summary, the circuit of Fig. 10.50 contains two signal paths, one through $Q_{1}$ and $Q_{2}$ and another through $Q_{1}, Q_{3}$ and $Q_{4}$ [Fig. 10.51(a)]. For a differential input change, each path experiences a current change, which translates to a voltage change at the output node. The key point here is that the two paths enhance each other at the output; in the above example, each path forces $V_{\text {out }}$ to increase.

Our initial examination of $Q_{3}$ and $Q_{4}$ in Fig. 10.50 indicates an interesting difference with respect to current mirrors studied in Chapter 9: here $Q_{3}$ and $Q_{4}$ carry signals in
image_name:Figure 10.51
description:
[
name: Q1, type: NPN, ports: {C: N, B: Vin1, E: Iee}
name: Q2, type: NPN, ports: {C: Vout, B: Vin2, E: Iee}
name: Q3, type: PNP, ports: {C: Vcc, B: N, E: N}
name: Q4, type: PNP, ports: {C: Vcc, B: Vout, E: N}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: Iee, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with active load. Q1 and Q2 form the differential pair, while Q3 and Q4 are the active loads. The output voltage is taken from the node labeled Vout.

Figure 10.51 Signal paths in pair with active load.
image_name:Figure 10.52 Differential pair with current-source loads
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: Vin1, E: P}
name: Q2, type: NPN, ports: {C: Vout, B: Vin2, E: P}
name: Q3, type: PNP, ports: {C: Vcc, B: Vb, E: Vout}
name: Q4, type: PNP, ports: {C: Vcc, B: Vb, E: Vout}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with active load. Q1 and Q2 form the differential pair, while Q3 and Q4 are the active loads. The output voltage is taken from the node labeled Vout.

(a)

Figure 10.52 Differential pair with current-source loads.

Did you know?

The active load was a significant breakthrough in op amp design. Earlier op amps employed a differential pair at the input but discarded the signal on one side at the final output. The first trace of active loads can be seen in the LM101A op amp designed by Robert Widlar at National Semiconductor in 1967. Widlar recognized that the active load avoids large resistor values (which would occupy a large chip area), saves voltage headroom, and provides a high gain. The differential pair with active load is also known as the "five-transistor OTA," where OTA stands for "operational transconductance amplifier" and was used to refer to CMOS op amps in olden days.
addition to bias currents. This also stands in contrast to the current-source loads in Fig. 10.52, where the baseemitter voltage of the load transistors remains constant and independent of signals. Called an "active load" to distinguish it from the load transistors in Fig. 10.52, the combination of $Q_{3}$ and $Q_{4}$ plays a critical role in the operation of the circuit.

The foregoing analysis directly applies to the CMOS counterpart, shown in Fig. 10.53. Specifically, in response to a small, differential input, $I_{D 1}$ rises to $I_{S S} / 2+\Delta I$ and $I_{D 2}$ falls to $I_{S S} / 2-\Delta I$. The change in $I_{D 2}$ tends to raise $V_{\text {out }}$. Also, the change in $I_{D 1}$ and $I_{D 3}$ is copied into $I_{D 4}$, increasing $\left|I_{D 4}\right|$ and raising $V_{\text {out }}$. (In this circuit, too, the current mirror transistors are identical.)
image_name:Figure 10.53 MOS differential pair with active load
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1d3g3, G: +ΔV}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: -ΔV}
name: M3, type: PMOS, ports: {S: VDD, D: d1d3g3, G: d1d3g3}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: d1d3g3}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: d1d3g3, Nn: GND}
]
extrainfo:The circuit is a MOS differential pair with an active load, using a current mirror configuration. The PMOS transistors M3 and M4 form the active load, providing high output impedance and increased gain. The differential input is applied to the gates of NMOS transistors M1 and M2, and the output is taken from the drain of M2.

Figure 10.53 MOS differential pair with active load.

### 10.6.2 Quantitative Analysis

The existence of the signal paths in the differential to single-ended converter circuit suggests that the voltage gain of the circuit must be greater than that of a differential topology in which only one output node is sensed with respect to ground [e.g., Fig. 10.47(b)]. To confirm this conjecture, we wish to determine the small-signal single-ended output, $v_{\text {out }}$, divided by the small-signal differential input, $v_{i n 1}-v_{i n 2}$. We deal with a CMOS implementation here (Fig. 10.54) to demonstrate that both CMOS and bipolar versions are treated identically.
image_name:Figure 10.54 MOS pair for small-signal analysis
description:
[
name: M1, type: NMOS, ports: {S: P, D: A, G: Vin1}
name: M2, type: NMOS, ports: {S: P, D: Vout, G: Vin2}
name: M3, type: PMOS, ports: {S: VDD, D: A, G: A}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: A}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: VDD, Nn: P}
]
extrainfo:The circuit is a differential amplifier with NMOS input pair (M1, M2) and PMOS load (M3, M4). The current source Iss provides biasing. The diode-connected PMOS M3 creates a low impedance at node A.

Figure 10.54 MOS pair for small-signal analysis.

The circuit of Fig. 10.54 presents a quandary. While the transistors themselves are symmetric and the input signals are small and differential, the circuit is asymmetric. With the diode-connected device, $M_{3}$, creating a low impedance at node $A$, we expect a relatively small voltage swing-on the order of the input swing-at this node. On the other hand, transistors $M_{2}$ and $M_{4}$ provide a high impedance and hence a large voltage swing at the output node. (After all, the circuit serves as an amplifier.) The asymmetry resulting from the very different voltage swings at the drains of $M_{1}$ and $M_{2}$ disallows grounding node $P$ for small-signal analysis. We present two approaches to solving this circuit.

Approach I Without a half circuit available, the analysis can be performed through the use of a complete small-signal model of the amplifier. Referring to the equivalent circuit shown in Fig. 10.55, where the dashed boxes indicate each transistor, we perform the analysis in two steps. In the first step, we note that $i_{X}$ and $i_{Y}$ must add up to zero at node $P$ and hence $i_{X}=-i_{Y}$. Also, $v_{A}=-i_{X}\left(g_{m P}^{-1} \| r_{O P}\right)$ and

$$
\begin{align*}
-i_{Y} & =\frac{v_{\text {out }}}{r_{O P}}+g_{m P} v_{A}  \tag{10.192}\\
& =\frac{v_{\text {out }}}{r_{O P}}-g_{m P} i_{X}\left(\frac{1}{g_{m P}} \| r_{O P}\right)  \tag{10.193}\\
& =i_{X} \tag{10.194}
\end{align*}
$$

Thus,

$$
\begin{equation*}
i_{X}=\frac{v_{\text {out }}}{r_{O P}\left[1+g_{m P}\left(\frac{1}{g_{m P}} \| r_{O P}\right)\right]} \tag{10.195}
\end{equation*}
$$

image_name:Figure 10.55 Small-signal equivalent circuit of differential pair with active load
description:
[
name: M1, type: NMOS, ports: {S: P, D: A, G: Vin1}
name: M2, type: NMOS, ports: {S: P, D: Vout, G: Vin2}
name: M3, type: PMOS, ports: {S: VDD, D: A, G: A}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: Vout}
name: Vin1, type: VoltageSource, value: Vin1, ports: {Np: Vin1, Nn: GND}
name: Vin2, type: VoltageSource, value: Vin2, ports: {Np: Vin2, Nn: GND}
name: g_mN V1, type: VoltageControlledCurrentSource, ports: {Np: A, Nn: P}
name: g_mN V2, type: VoltageControlledCurrentSource, ports: {Np: Vout, Nn: P}
name: g_mP V_A, type: VoltageControlledCurrentSource, ports: {Np: Vout, Nn: A}
name: r_ON, type: Resistor, value: r_ON, ports: {N1: A, N2: P}
name: r_OP, type: Resistor, value: r_OP, ports: {N1: Vout, N2: VDD}
]
extrainfo:The circuit is a small-signal equivalent of a differential pair with an active load. It uses NMOS transistors M1 and M2 for the input differential pair and PMOS transistors M3 and M4 as the active load. The circuit operates with input voltages Vin1 and Vin2, and produces an output at Vout.

Figure 10.55 Small-signal equivalent circuit of differential pair with active load.

In the second step, we write a KVL around the loop consisting of all four transistors. The current through $r_{O N}$ of $M_{1}$ is equal to $i_{X}-g_{m N} v_{1}$ and that through $r_{O N}$ of $M_{2}$ equal to $i_{Y}-g_{m N} v_{2}$. It follows that

$$
\begin{equation*}
-v_{A}+\left(i_{X}-g_{m N} v_{1}\right) r_{O N}-\left(i_{Y}-g_{m N} v_{2}\right) r_{O N}+v_{\text {out }}=0 \tag{10.196}
\end{equation*}
$$

Since $v_{1}-v_{2}=v_{i n 1}-v_{i n 2}$ and $i_{X}=-i_{Y}$,

$$
\begin{equation*}
-v_{A}+2 i_{X} r_{O N}-g_{m N} r_{O N}\left(v_{i n 1}-v_{i n 2}\right)+v_{o u t}=0 \tag{10.197}
\end{equation*}
$$

Substituting for $v_{A}$ and $i_{X}$ from above, we have

$$
\begin{align*}
\frac{v_{\text {out }}}{r_{O P}\left[1+g_{m P}\left(\frac{1}{g_{m P}} \| r_{O P}\right)\right]}\left(\frac{1}{g_{m P}} \| r_{O P}\right) & +2 r_{\text {ON }} \frac{v_{\text {out }}}{r_{O P}\left[1+g_{m P}\left(\frac{1}{g_{m P}} \| r_{O P}\right)\right]} \\
+v_{\text {out }} & =g_{m N} r_{\text {ON }}\left(v_{\text {in } 1}-v_{\text {in } 2}\right) \tag{10.198}
\end{align*}
$$

Solving for $v_{\text {out }}$ yields

$$
\begin{equation*}
\frac{v_{\text {out }}}{v_{\text {in } 1}-v_{\text {in } 2}}=g_{m N} r_{O N} \frac{r_{O P}\left[1+g_{m P}\left(\frac{1}{g_{m P}} \| r_{O P}\right)\right]}{2 r_{O N}+2 r_{O P}} \tag{10.199}
\end{equation*}
$$

This is the exact expression for the gain. If $g_{m P} r_{O P} \gg 1$, then

$$
\begin{equation*}
\frac{v_{\text {out }}}{v_{\text {in } 1}-v_{\text {in } 2}}=g_{m N}\left(r_{O N} \| r_{O P}\right) \tag{10.200}
\end{equation*}
$$

The gain is indepedent of $g_{m P}$ and equal to that of the fully-differential circuit. In other words, the use of the active load has restored the gain.

Approach II* In this approach, we decompose the circuit into sections that more easily lend themselves to analysis by inspection. As illustrated in Fig. 10.56(a), we first seek a Thevenin equivalent for the section consisting of $v_{i n 1}, v_{i n 2}, M_{1}$ and $M_{2}$, assuming $v_{i n 1}$ and $v_{i n 2}$ are differential. Recall that $v_{T h e v}$ is the voltage between $A$ and $B$ in the "open-circuit condition" [Fig. 10.56(b)]. Under this condition, the circuit is symmetric, resembling the topology of Fig. 10.16(a). Equation (10.92) thus yields

$$
\begin{equation*}
v_{\text {Thev }}=-g_{m N} r_{O N}\left(v_{i n 1}-v_{i n 2}\right) \tag{10.201}
\end{equation*}
$$

where the subscript $N$ refers to NMOS devices.
To determine the Thevenin resistance, we set the inputs to zero and apply a voltage between the output terminals [Fig. 10.56(c)]. Noting that $M_{1}$ and $M_{2}$ have equal gate-source voltages $\left(v_{1}=v_{2}\right)$ and writing a KVL around the "output" loop, we have

$$
\begin{equation*}
\left(i_{X}-g_{m 1} v_{1}\right) r_{O 1}+\left(i_{X}+g_{m 2} v_{2}\right) r_{O 2}=v_{X} \tag{10.202}
\end{equation*}
$$

and hence

$$
\begin{equation*}
R_{\text {Thev }}=2 r_{O N} \tag{10.203}
\end{equation*}
$$

The reader is encouraged to obtain this result using half circuits as well.
Having reduced the input sources and transistors to a Thevenin equivalent, we now compute the gain of the overall amplifier. Figure 10.57 depicts the simplified circuit, where the diode-connected transistor $M_{3}$ is replaced with $\left(1 / g_{m 3}\right) \| r_{O 3}$ and the output impedance

[^4]image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: A, G: Vin1}
name: M2, type: NMOS, ports: {S: P, D: B, G: Vin2}
name: M3, type: PMOS, ports: {S: VDD, D: A, G: A}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: B}
name: I_SS, type: CurrentSource, value: I_SS, ports: {Np: P, Nn: GND}
name: R_Thev, type: Resistor, value: R_Thev, ports: {N1: VThev, N2: GND}
name: V_Thev, type: VoltageSource, value: V_Thev, ports: {Np: VThev, Nn: GND}
name: r_o1, type: Resistor, value: r_o1, ports: {N1: A, N2: V1}
name: r_o2, type: Resistor, value: r_o2, ports: {N1: B, N2: V2}
name: V_x, type: VoltageSource, value: V_x, ports: {Np: Vx, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with a Thevenin equivalent representation. It includes NMOS and PMOS transistors with diode-connected configurations. The current source I_SS provides biasing for the NMOS transistors. The diagram shows how the input differential pair is connected to a Thevenin equivalent circuit with V_Thev and R_Thev. The output voltage Vout is derived from the connection of the PMOS transistors M3 and M4.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: P, D: A, G: Vin1}
name: M2, type: NMOS, ports: {S: P, D: B, G: Vin2}
name: I_SS, type: CurrentSource, ports: {Np: P, Nn: GND}
name: R_Thev, type: Resistor, value: R_Thev, ports: {N1: A, N2: B}
]
extrainfo:The circuit represents a Thevenin equivalent with NMOS transistors M1 and M2 forming a differential pair. The current source I_SS provides a bias current, and the resistor R_Thev models the Thevenin resistance between nodes A and B.
image_name:(c)
description:
[
name: M1, type: NMOS, ports: {S: P, D: v1, G: Vin1}
name: M2, type: NMOS, ports: {S: P, D: v2, G: Vin2}
name: M3, type: PMOS, ports: {S: VDD, D: A, G: A}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: B}
name: I_SS, type: CurrentSource, ports: {Np: P, Nn: GND}
name: R_Thev, type: Resistor, value: R_Thev, ports: {N1: A, N2: B}
name: r_o1, type: Resistor, value: r_o1, ports: {N1: v1, N2: A}
name: r_o2, type: Resistor, value: r_o2, ports: {N1: v2, N2: B}
name: V_Thev, type: VoltageSource, value: V_Thev, ports: {Np: A, Nn: B}
name: V_x, type: VoltageSource, value: V_x, ports: {Np: v1, Nn: v2}
]
extrainfo:The circuit diagram represents a differential amplifier with NMOS input transistors M1 and M2, and PMOS load transistors M3 and M4. The current source I_SS provides biasing. V_Thev and R_Thev form a Thevenin equivalent circuit. The resistors r_o1 and r_o2 model the output resistances of M1 and M2. The voltage source V_x models the differential input voltage.

Figure 10.56 (a) Thevenin equivalent, (b) Thevenin voltage, and (c) Thevenin resistance of input pair.
of $M_{4}$ is drawn explicitly. The objective is to calculate $v_{\text {out }}$ in terms of $v_{T h e v}$. Since the voltage at node $E$ with respect to ground is equal to $v_{\text {out }}+v_{\text {Thev }}$, we can view $v_{A}$ as a divided version of $v_{E}$ :

$$
\begin{equation*}
v_{A}=\frac{\frac{1}{g_{m 3}} \| r_{O 3}}{\frac{1}{g_{m 3}} \| r_{O 3}+R_{T h e v}}\left(v_{\text {out }}+v_{\text {Thev }}\right) . \tag{10.204}
\end{equation*}
$$

Given by $g_{m 4} v_{A}$, the small-signal drain current of $M_{4}$ must satisfy KCL at the output node:

$$
\begin{equation*}
g_{m 4} v_{A}+\frac{v_{\text {out }}}{r_{O 4}}+\frac{v_{\text {out }}+v_{\text {Thev }}}{\frac{1}{g_{m 3}} \| r_{O 3}+R_{\text {Thev }}}=0, \tag{10.205}
\end{equation*}
$$

image_name:Figure 10.57
description:
[
name: M4, type: PMOS, ports: {S: VDD, D: B, G: A}
name: RThev, type: Resistor, value: RThev, ports: {N1: A, N2: E}
name: VThev, type: VoltageSource, value: VThev, ports: {Np: E, Nn: GND}
name: rO3, type: Resistor, value: rO3, ports: {N1: A, N2: VDD}
name: rO4, type: Resistor, value: rO4, ports: {N1: B, N2: GND}
]
extrainfo:The circuit is a simplified model for calculating voltage gain, involving PMOS transistor M4, a Thevenin equivalent voltage source VThev, and resistors RThev, rO3, and rO4. Node A is connected to both rO3 and RThev, while node B is the output node Vout.

Figure 10.57 Simplified circuit for calculation of voltage gain.
where the last term on the left-hand side represents the current flowing through $R_{\text {Thev }}$. It follows from Eqs. (10.204) and (10.205) that

$$
\begin{equation*}
\left(g_{m 4} \frac{\frac{1}{g_{m 3}} \| r_{O 3}}{\frac{1}{g_{m 3}} \| r_{O 3}+R_{\text {Thev }}}+\frac{1}{\frac{1}{g_{m 3}} \| r_{O 3}+R_{\text {Thev }}}\right)\left(v_{\text {out }}+v_{\text {Thev }}\right)+\frac{v_{\text {out }}}{r_{O 4}}=0 . \tag{10.206}
\end{equation*}
$$

Recognizing that $1 / g_{m 3} \ll r_{O 3}$, and $1 / g_{m 3} \ll R_{T h e v}$ and assuming $g_{m 3}=g_{m 4}=g_{m p}$ and $r_{O 3}=r_{O 4}=r_{O P}$, we reduce Eq. (10.206) to

$$
\begin{equation*}
\frac{2}{R_{\text {Thev }}}\left(v_{\text {out }}+v_{\text {Thev }}\right)+\frac{v_{\text {out }}}{r_{O P}}=0 . \tag{10.207}
\end{equation*}
$$

Equations (10.201) and (10.207) therefore give

$$
\begin{equation*}
v_{\text {out }}\left(\frac{1}{r_{O N}}+\frac{1}{r_{O P}}\right)=\frac{g_{m N} r_{O N}\left(v_{i n 1}-v_{i n 2}\right)}{r_{O N}} \tag{10.208}
\end{equation*}
$$

and hence

$$
\begin{equation*}
\frac{v_{\text {out }}}{v_{\text {in } 1}-v_{\text {in } 2}}=g_{m N}\left(r_{O N} \| r_{O P}\right) . \tag{10.209}
\end{equation*}
$$

The gain is independent of $g_{m p}$. Interestingly, the gain of this circuit is the same as the differential gain of the topology in Fig. 10.51(b). In other words, the path through the active load restores the gain even though the output is single-ended.

Example In our earlier observations, we surmised that the voltage swing at node $A$ in Fig. 10.56 is 10.29 much less than that at the output. Prove this point.

Solution As depicted in Fig. 10.58, KCL at the output node indicates that the total current drawn by $M_{2}$ must be equal to $-v_{\text {out }} / r_{O 4}-g_{m 4} v_{A}$. This current flows through $M_{1}$ and hence through $M_{3}$, generating

$$
\begin{equation*}
v_{A}=-\left(v_{\text {out }} / r_{O 4}+g_{m 4} v_{A}\right)\left(\frac{1}{g_{m 3}} \| r_{O 3}\right) . \tag{10.210}
\end{equation*}
$$

Figure 10.58

That is,

$$
\begin{equation*}
v_{A} \approx-\frac{v_{\text {out }}}{2 g_{m P} r_{O P}} \tag{10.211}
\end{equation*}
$$

revealing that $v_{A}$ is indeed much less that $v_{\text {out }}$.

Exercise Calculate the voltage gain from the differential input to node $A$.

## 10.7 CHAPTER SUMMARY

- Single-ended signals are voltages measured with respect to ground. A differential signal consists of two single-ended signals carried over two wires, with the two components beginning from the same dc (common-mode) level and changing by equal and opposite amounts.
- Compared with single-ended signals, differential signals are more immune to common-mode noise.
- A differential pair consists of two identical transistors, a tail current, and two identical loads.
- The transistor currents in a differential pair remain constant as the input CM level changes, i.e., the circuit "rejects" input CM changes.
- The transistor currents change in opposite directions if a differential input is applied, i.e., the circuit responds to differential inputs.
- For small, differential changes at the input, the tail node voltage of a differential pair remains constant and is thus considered a virtual ground node.
- Bipolar differential pairs exhibit a hyperbolic tangent input/output characteristic. The tail current can be mostly steered to one side with a differential input of about $4 V_{T}$.
- For small-signal operation, the input differential swing of a bipolar differential pair must remain below roughly $V_{T}$. The pair can then be decomposed into two half circuits, each of which is simply a common-emitter stage.
- MOS differential pairs can steer the tail current with a differential input equal to $\sqrt{2 I_{S S} /\left(\mu_{n} C_{o x} W / L\right)}$, which is $\sqrt{2}$ larger than the equilibrium overdrive of each transistor.
- Unlike their bipolar counterparts, MOS differential pairs can provide more or less linear characteristics depending on the choice of the device dimensions.
- The input transistors of a differential pair can be cascoded so as to achieve a higher voltage gain. Similarly, the loads can be cascoded to maximize the voltage gain.
- The differential output of a perfectly symmetric differential pair remains free from input CM changes. In the presence of asymmetries and a finite tail current source impedance, a fraction of the input CM change appears as a differential component at the output, corrupting the desired signal.
- The gain seen by the CM change normalized to the gain seen by the desired signal is called the common-mode rejection ration.
- It is possible to replace the loads of a differential pair with a current mirror so as to provide a single-ended output while maintaining the original gain. The circuit is called a differential pair with active load.
