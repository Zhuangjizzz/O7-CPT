# 12. Fully Differential Operational Amplifiers

## 12.1 Introduction

The analysis of integrated-circuit operational amplifiers (op amps) in Chapter 6 focused on op amps with single-ended outputs. The topic of this chapter is fully differential op amps, which have a differential input and produce a differential output. Fully differential op amps are widely used in modern integrated circuits because they have some advantages over their single-ended counterparts. They provide a larger output voltage swing and are less susceptible to common-mode noise. Also, even-order nonlinearities are not present in the differential output of a balanced circuit. (A balanced circuit is symmetric with perfectly matched elements on either side of an axis of symmetry.) A disadvantage of fully differential op amps is that they require two matched feedback networks and a common-mode feedback circuit to control the common-mode output voltage.

In this chapter, the properties of fully differential amplifiers are presented first, followed by some common-mode feedback approaches. A number of fully differential CMOS op amps are covered. Some of the terminology used in this chapter was introduced for a simple fully differential amplifier (a differential pair with resistive loads) in Section 3.5. In most of the chapter, the circuits are assumed to be perfectly balanced. The effects of imbalance are considered in Section 12.7. The circuits in this chapter are CMOS; however, most of the techniques and topologies described can be readily extended to bipolar technologies.

## 12.2 Properties of Fully Differential Amplifiers ${ }^{1,2}$

A fully differential feedback amplifier is shown in Fig. 12.1 $a$. It differs from the single-ended feedback amplifier in Fig. $12.1 b$ in the following two ways. The op amp has two outputs, and two identical resistive networks provide feedback. While many fully differential op-amp topologies exist, the simple fully differential amplifier in Fig. 12.2 will be used for illustration purposes. It consists of a differential pair $M_{1}-M_{2}$, active loads $M_{3}$ and $M_{4}$, and tail current source $M_{5}$.

Fully differential op amps provide a larger output voltage swing than their single-ended counterparts, which is important when the power-supply voltage is small. The larger output voltage swing provided by a fully differential op amp can be explained using the two feedback circuits in Fig. 12.1. Assume that each op-amp output, $V_{o 1}, V_{o 2}$, or $V_{o}$, can swing up to $V_{\max }$ and down to $V_{\min }$. For the single-ended-output circuit in Fig. 12.1b, the peak-to-peak output voltage can be as large as $V_{\max }-V_{\min }$. In the fully differential circuit in Fig. 12.1a, if $V_{o 1}$ swings up to $V_{\max }$ and $V_{o 2}$ swings down to $V_{\min }$, the peak differential output is $V_{\max }-V_{\min }$. Therefore, the peak-to-peak differential output is $2\left(V_{\max }-V_{\min }\right)$. Thus, the output swing of
image_name:(a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vs1, N2: Vi1}
name: R1, type: Resistor, value: R1, ports: {N1: Vs2, N2: Vi2}
name: R3, type: Resistor, value: R3, ports: {N1: Vi1, N2: Vo1}
name: R3, type: Resistor, value: R3, ports: {N1: Vi2, N2: Vo2}
name: A, type: OpAmp, value: A, ports: {InP: Vi2, InN: Vi1, OutP: Vo1, OutN: Vo2}
]
extrainfo:The circuit is a fully differential amplifier with inputs Vs1 and Vs2, and outputs Vo1 and Vo2. The resistors R1 and R3 are used to set the gain of the amplifier. The output swing is represented with Vmax and Vmin, showing the peak-to-peak differential output as 2(Vmax-Vmin).
image_name:V_o1, V_o2, V_od
description:The diagram represents a fully differential amplifier circuit and its corresponding output waveforms. The circuit consists of two input voltages, $V_{s1}$ and $V_{s2}$, each connected through resistors $R_1$ to the inverting and non-inverting inputs of an operational amplifier, denoted as $A_{\text{o}}$. The amplifier outputs two voltages, $V_{o1}$ and $V_{o2}$, through resistors $R_3$. The differential output voltage is represented as $V_{od}$.

The graph shows three waveforms:

1. **$V_{o1}$ Waveform:**
- **Type:** Time-domain waveform
- **Axes:**
- X-axis: Time ($t$)
- Y-axis: Voltage ($V$)
- **Behavior:** The waveform oscillates between $V_{\text{max}}$ and $V_{\text{min}}$, indicating a sinusoidal waveform centered around a midpoint. The oscillation suggests periodic behavior.

2. **$V_{o2}$ Waveform:**
- **Type:** Time-domain waveform
- **Axes:**
- X-axis: Time ($t$)
- Y-axis: Voltage ($V$)
- **Behavior:** Similar to $V_{o1}$, this waveform oscillates between $V_{\text{max}}$ and $V_{\text{min}}$. This waveform is also sinusoidal and has a similar periodic nature.

3. **$V_{od}$ (Differential Output) Waveform:**
- **Type:** Time-domain waveform
- **Axes:**
- X-axis: Time ($t$)
- Y-axis: Voltage ($V$)
- **Behavior:** The differential output waveform oscillates between $V_{\text{max}} - V_{\text{min}}$ and $-(V_{\text{max}} - V_{\text{min}})$, showing a doubled peak-to-peak amplitude compared to $V_{o1}$ and $V_{o2}$. This indicates that the differential output has twice the swing of the single-ended outputs, consistent with fully differential operation.

The graph effectively illustrates the relationship between the single-ended voltages $V_{o1}$ and $V_{o2}$ and the resultant differential voltage $V_{od}$, demonstrating the increased dynamic range achieved through differential amplification.

image_name:Figure 12.1 (b)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs+, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vs+, N2: InN(Ao)}
name: R3, type: Resistor, value: R3, ports: {N1: In(Ao), N2: Vo}
name: Ao, type: OpAmp, value: Ao, ports: {InP: GND, InN: In(Ao), Out: Vo}
]
extrainfo:The circuit is a single-ended inverting amplifier with input voltage Vs and output voltage Vo. R1 and R3 form the feedback network, and the op-amp Ao provides the amplification.

(b)
image_name:Figure 12.1 (b)
description:The graph in Figure 12.1 (b) represents a time-domain waveform of an output voltage \( V_o \) over time \( t \). The vertical axis is labeled \( V_o \) and represents the output voltage, while the horizontal axis is labeled \( t \) and represents time. The waveform exhibits a sinusoidal shape, indicating an oscillating voltage output.

The waveform starts at zero and initially increases to a maximum positive value labeled \( V_{\text{max}} \). After reaching this peak, it decreases back to zero and continues to a minimum negative value labeled \( V_{\text{min}} \), before returning to zero to complete one full cycle. This pattern suggests a periodic oscillation typical of an inverting amplifier's output.

Key features of the graph include the maximum and minimum voltage levels \( V_{\text{max}} \) and \( V_{\text{min}} \), which are marked by dashed horizontal lines. The waveform is symmetric about the horizontal axis, indicating that the amplitude of the positive and negative peaks is equal. The presence of these peaks suggests the operational characteristics of the single-ended inverting amplifier, which produces an output that is 180 degrees out of phase with the input signal.
Figure 12.1 (a) Fully differential and (b) single-ended inverting amplifiers.
image_name:Figure 12.2
description:
[
name: M1, type: NMOS, ports: {S: s1s2d5, D: Vo1, G: Vi1}
name: M2, type: NMOS, ports: {S: s1s2d5, D: Vo2, G: Vi2}
name: M3, type: PMOS, ports: {S: VDD, D: Vo1, G: Vbias}
name: M4, type: PMOS, ports: {S: VDD, D: Vo2, G: Vbias}
name: M5, type: NMOS, ports: {S: -VSS, D: s1s2d5, G: Vcmc}
]
extrainfo:This is a fully differential op amp circuit with NMOS and PMOS transistors. It utilizes differential inputs (Vi1, Vi2) and produces differential outputs (Vo1, Vo2). The circuit is powered by VDD and -VSS, with a bias voltage Vbias controlling PMOS transistors and a common mode voltage Vcmc controlling the tail NMOS transistor M5.
Figure 12.2 A simple, one-stage, fully differential op amp.
a fully differential op amp is twice as large as that of a similar op amp with a single-ended output.

This larger output swing can result in a higher signal-to-noise ratio. Ignoring the noise from the op amp and from the feedback resistor $R_{3}$, we see that thermal noise associated with the $R_{1}$ input resistors is the only source of noise. In the single-ended circuit in Fig. 12.1b, the
output noise power due to resistor $R_{1}$ is

$$
\begin{equation*}
\overline{v_{o N}^{2}}(\text { s.e. })=\left(\frac{R_{3}}{R_{1}}\right)^{2} 4 k T R_{1}\left(B W_{N}\right) \tag{12.1}
\end{equation*}
$$

where $B W_{N}$ is the equivalent noise bandwidth of the closed-loop amplifier. In the fully differential amplifier in Fig. 12.1a, the differential output noise power due to the two $R_{1}$ resistors is

$$
\begin{equation*}
\overline{v_{o N}^{2}}(\text { diff })=2\left(\frac{R_{3}}{R_{1}}\right)^{2} 4 k T R_{1}\left(B W_{N}\right) \tag{12.2}
\end{equation*}
$$

because the output noise terms from the two $R_{1}$ resistors are uncorrelated and hence their contributions add together to give the total output noise power. From (12.1) and (12.2), the output noise power in the fully differential circuit is twice that in the single-ended circuit. Since the peak output signal in the differential circuit is twice that in the single-ended circuit, the maximum output signal power is four times that in the single-ended circuit. The maximum output signal-to-noise ratio (SNR) for a maximum sinusoidal output signal with amplitude $V_{\text {sig(peak })}$ is given by

$$
\begin{equation*}
\mathrm{SNR}_{\max }=\frac{\text { maximum output signal power }}{\text { output noise power }}=\frac{\frac{V_{\text {sig(peak })}^{2}}{2}}{\overline{v_{o N}^{2}}} \tag{12.3}
\end{equation*}
$$

This SNR is twice as large, or 3 dB larger, for the fully differential circuit when compared to the single-ended circuit if the same resistance $R_{1}$ is used in both circuits and $R_{1}$ is the dominant noise source.

Fully differential circuits are less susceptible than their single-ended counterparts to common-mode (CM) noise, such as noise on the power supplies that is generated by digital circuits that are integrated on the same substrate as the analog circuits. To explain the reduced sensitivity to CM noise, consider the circuit in Fig. 12.3. This circuit is the same as Fig. $12.1 a$ with two capacitors $C_{i p}$ added. Each capacitor connects from an op-amp input to voltage source $v_{n}$. Here $C_{i p}$ models parasitic capacitance from the substrate to each opamp input, and $v_{n}$ models noise that exists on the power-supply voltage that connects to the substrate. The parasitic capacitors couple equal signals to the op-amp inputs, causing a CM disturbance at the op-amp input. If the op amp is perfectly balanced and has zero CM gain, this CM noise does not affect the CM output voltage. If the op-amp CM gain is nonzero but small, $v_{n}$ causes a small CM output voltage but does not affect the differential output voltage
image_name:Figure 12.3
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vs1, N2: In(Ao)}
name: R1, type: Resistor, value: R1, ports: {N1: Vs2, N2: Ip(Ao)}
name: R3, type: Resistor, value: R3, ports: {N1: V01, N2: Vo1}
name: R3, type: Resistor, value: R3, ports: {N1: V02, N2: Vo2}
name: Cip, type: Capacitor, value: Cip, ports: {Np: Vn, Nn: In(Ao)}
name: Cip, type: Capacitor, value: Cip, ports: {Np: Vn, Nn: Ip(Ao)}
name: Ao, type: OpAmp, value: Ao, ports: {InP: Ip(Ao), InN: In(Ao), OutP: V01, OutN: V02}
name: Vs1, type: VoltageSource, value: Vs1, ports: {Np: Vs1, Nn: GND}
name: Vs2, type: VoltageSource, value: Vs2, ports: {Np: Vs2, Nn: GND}
name: vn, type: VoltageSource, value: vn, ports: {Np: Vn, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with parasitic capacitors Cip introducing common-mode noise. The op-amp Ao has two inputs and two outputs, with resistors R1 and R3 setting the gain. Voltage sources Vs1 and Vs2 provide input signals, and vn models the noise on the power supply.

Figure 12.3 The inverting amplifier of Fig. 12.1a including parasitic capacitors $C_{i p}$ and noise source $v_{n}$.
if the circuit is perfectly balanced. This capacitive coupling to the op-amp inputs can cause a nonzero differential-mode (DM) output voltage if the circuit is not perfectly balanced. For example, mismatch between the $C_{i p}$ capacitors causes the coupled noise at the two op-amp inputs to be unequal and introduces a differential noise signal across the op-amp inputs.

Even without the capacitive coupling to the substrate in Fig. 12.3, noise on the positive or negative power supply can couple to the op-amp outputs through the transistors in the op amp (see Section 6.2.6). If the circuit is balanced, such coupling is the same at each op-amp output. Therefore, power-supply noise in a balanced circuit alters the CM output but does not affect the DM output.

Even-order nonlinearities are not present in the differential output of a balanced circuit. The cancellation of even-order nonlinearities can be explained using Fig. 12.1 $a$. Assume that the circuit is perfectly balanced but is not perfectly linear. First, consider the case when the inputs are $V_{s 1}=V_{a}$ and $V_{s 2}=V_{b}$, and let the resulting output voltages be $V_{o 1}=V_{x}$ and $V_{o 2}=V_{y}$. In this case, the differential input and output are

$$
\begin{equation*}
V_{s d}=V_{a}-V_{b} \quad \text { and } \quad V_{o d}=V_{x}-V_{y} \tag{12.4}
\end{equation*}
$$

Next, consider the circuit with the inputs swapped; that is, $V_{s 1}=V_{b}$ and $V_{s 2}=V_{a}$. Then the output voltages will also be swapped ( $V_{o 1}=V_{y}$ and $V_{o 2}=V_{x}$ ) because the circuit is symmetric. In this second case,

$$
\begin{equation*}
V_{s d}=V_{b}-V_{a}=-\left(V_{a}-V_{b}\right) \quad \text { and } \quad V_{o d}=V_{y}-V_{x}=-\left(V_{x}-V_{y}\right) \tag{12.5}
\end{equation*}
$$

Equations 12.4 and 12.5 show that changing the polarity of the differential input of a balanced circuit causes only a polarity change in the differential output voltage. Therefore, the differential input-output characteristic $f()$ is an odd function; that is, if $V_{o d}=f\left(V_{i d}\right)$, then $-V_{o d}=f\left(-V_{i d}\right)$. Hence, the differential transfer characteristic of a balanced amplifier exhibits only odd-order nonlinearities, so only odd-order distortion can appear in the differential output when a differential input is applied. Even-order distortion may exist in each individual output $V_{o 1}$ and $V_{o 2}$, but such distortion in these output voltages is identical and cancels when they are subtracted to form $V_{o d}$.

In a balanced, fully differential amplifier, the small-signal differential output voltage is proportional to the small-signal differential input voltage but is independent of the CM input voltage, as was shown in Section 3.5.4. Similarly, the small-signal CM output voltage is proportional to the small-signal CM input voltage but is independent of the differential input voltage.

## 12.3 Small-Signal Models for Balanced Differential Amplifiers

A balanced signal source driving a balanced, fully differential amplifier is shown in Fig. 12.4. A $T$-network small-signal model for the balanced signal source is shown in Fig. 12.5. Equations that describe this model are found as follows. Applying KVL from $v_{s 1}$ to ground,

$$
\begin{equation*}
v_{s 1}=\frac{v_{s d}^{\prime}}{2}+v_{s c}^{\prime}+\frac{R_{s d}}{2} i_{s 1}+\left(\frac{R_{s c}}{2}-\frac{R_{s d}}{4}\right)\left(i_{s 1}+i_{s 2}\right) \tag{12.6}
\end{equation*}
$$

Rearranging gives

$$
\begin{equation*}
v_{s 1}=\frac{v_{s d}^{\prime}}{2}+v_{s c}^{\prime}+\frac{R_{s d}}{2} \frac{i_{s 1}-i_{s 2}}{2}+R_{s c} \frac{i_{s 1}+i_{s 2}}{2} \tag{12.7}
\end{equation*}
$$

image_name:Figure 12.4 A block diagram of a fully differential signal source and amplifier driving a complex load.
description:The block diagram in Figure 12.4 illustrates a fully differential signal source and amplifier system driving a complex load. The main components of this system include a signal source, an amplifier (Amp), and a complex load made up of impedances.

1. **Main Components:**
- **Signal Source:** This block generates differential signals, denoted as \( v_{s1} \) and \( v_{s2} \), which are inputs to the amplifier.
- **Amplifier (Amp):** This block amplifies the input signals \( v_{s1} \) and \( v_{s2} \) and produces output signals \( v_{o1} \) and \( v_{o2} \).
- **Load Impedances (\( Z_{L1} \) and \( Z_{L2} \)):** These are the components that the amplified signals drive. \( Z_{L1} \) is connected to ground on both the positive and negative sides of the differential output, while \( Z_{L2} \) is connected between the two outputs.

2. **Flow of Information or Control:**
- The signal source provides differential signals \( v_{s1} \) and \( v_{s2} \) to the amplifier.
- The amplifier processes these inputs and outputs amplified signals \( v_{o1} \) and \( v_{o2} \).
- The amplified signals \( v_{o1} \) and \( v_{o2} \) drive the complex load composed of \( Z_{L1} \) and \( Z_{L2} \).
- Currents \( i_{l1} \) and \( i_{l2} \) flow through the load impedances, with the differential voltage \( v_{od} \) across \( Z_{L2} \).

3. **Labels, Annotations, and Key Indicators:**
- The diagram is labeled with voltages \( v_{s1}, v_{s2}, v_{o1}, v_{o2}, v_{od} \) and currents \( i_{l1}, i_{l2} \).
- Impedances \( Z_{L1} \) and \( Z_{L2} \) are shown, indicating the complex load configuration.
- Ground connections are marked to show reference points for the voltages.

4. **Overall System Function:**
- The system's primary function is to amplify differential signals from the signal source and drive a complex load with these amplified signals. The arrangement allows for balanced signal transmission and minimizes common-mode noise. The differential output voltage \( v_{od} \) across \( Z_{L2} \) is a key outcome of this system, representing the amplified differential signal.
Figure 12.4 A block diagram of a fully differential signal source and amplifier driving a complex load.

image_name:Figure 12.5
description:
[
name: R_sd/2, type: Resistor, value: R_sd/2, ports: {N1: vs1, N2: x2}
name: "V_sd/2", type: VoltageSource, value: "V_sd/2", ports: {Np: x2, Nn: x1}
name: R_sc/2 - R_sd/4, type: Resistor, value: R_sc/2 - R_sd/4, ports: {N1: x1, N2: "v_sc"}
name: "V_sc", type: VoltageSource, value: "V_sc", ports: {Np: "v_sc", Nn: GND}
name: "V_sd/2", type: VoltageSource, value: "V_sd/2", ports: {Np: x1, Nn: x3}
name: R_sd/2, type: Resistor, value: R_sd/2, ports: {N1: x3, N2: vs2}
]
extrainfo:The circuit diagram represents a model for a differential signal source. It includes resistors and voltage sources configured to model the differential and common-mode signals. The nodes x1, x2, and x3 are key connection points in the circuit, with x1 being the central node connecting the two voltage sources and the resistor modeling common-mode resistance.
Figure 12.5 A model for a differential signal source.

Define

$$
\begin{align*}
i_{s d} & =\frac{i_{s 1}-i_{s 2}}{2}  \tag{12.8}\\
i_{s c} & =\frac{i_{s 1}+i_{s 2}}{2} \tag{12.9}
\end{align*}
$$

Then

$$
\begin{gather*}
i_{s 1}=i_{s d}+i_{s c}  \tag{12.10}\\
i_{s 2}=-i_{s d}+i_{s c} \tag{12.11}
\end{gather*}
$$

Substituting (12.8) and (12.9) in (12.7) gives

$$
\begin{equation*}
v_{s 1}=\frac{v_{s d}^{\prime}}{2}+v_{s c}^{\prime}+\frac{R_{s d}}{2} i_{s d}+R_{s c} i_{s c} \tag{12.12}
\end{equation*}
$$

A similar analysis applied from $v_{s 2}$ to ground yields

$$
\begin{equation*}
v_{s 2}=-\frac{v_{s d}^{\prime}}{2}+v_{s c}^{\prime}-\frac{R_{s d}}{2} i_{s d}+R_{s c} i_{s c} \tag{12.13}
\end{equation*}
$$

The usual definitions apply for the DM and CM source voltages: $v_{s d}=v_{s 1}-v_{s 2}$ and $v_{s c}=\left(v_{s 1}+v_{s 2}\right) / 2$. Voltages $v_{s d}^{\prime}$ and $v_{s c}^{\prime}$ are the DM and CM open-circuit source voltages, respectively. That is, if $i_{s d}=i_{s c}=0$, then $v_{s d}=v_{s d}^{\prime}$ and $v_{s c}=v_{s c}^{\prime}$. Resistances $R_{s d}$ and $R_{s c}$ are the DM and CM resistances, respectively, associated with the signal source. Subtracting (12.13) from (12.12) and manipulating the result, we can write

$$
\begin{equation*}
R_{s d}=\left.\frac{v_{s d}}{i_{s d}}\right|_{v_{s d}^{\prime}=0} \tag{12.14}
\end{equation*}
$$

image_name:(a)
description:
[
name: Zid/2_1, type: Resistor, value: Zid/2, ports: {N1: vi1, N2: N1}
name: Zid/2_2, type: Resistor, value: Zid/2, ports: {N1: N1, N2: vi2}
name: Zic/2 - Zid/4, type: Resistor, value: Zic/2 - Zid/4, ports: {N1: N1, N2: GND}
]
extrainfo:This is a T-network model for the input impedance of a fully differential amplifier.

image_name:(b)
description:
[
name: Zid||(-2Zic), type: Resistor, value: Zid||(-2Zic), ports: {N1: vi1, N2: vi2}
name: Zic_1, type: Resistor, value: Zic, ports: {N1: vi1, N2: GND}
name: Zic_2, type: Resistor, value: Zic, ports: {N1: vi2, N2: GND}
]
extrainfo:This is a T-network model for the input impedance of a fully differential amplifier.

Figure 12.6 Models for the input impedance of a fully differential amplifier: (a) a $T$-network model and ( $b$ ) a $\pi$-network model.

Adding (12.12) and (12.13), we find

$$
\begin{equation*}
R_{s c}=\left.\frac{v_{s c}}{i_{s c}}\right|_{v_{s c}^{\prime}=0} \tag{12.15}
\end{equation*}
$$

These simple expressions result from the definitions of the CM and DM currents in (12.8) and (12.9), and the standard definitions for the CM and DM voltages.

Two equivalent models for the inputs of the amplifier in Fig. 12.4 are shown in Fig. 12.6. These models are extensions of Fig. 3.61 and (3.197) and (3.198), which were derived to model the inputs for a differential pair with resistive loads. Two equivalent models for the output ports of the amplifier are shown in Fig. 12.7. The equations that describe the model in Fig. 12.7a,
image_name:(a)
description:
[
name: Rod/2, type: Resistor, value: Rod/2, ports: {N1: vo1, N2: x3}
name: a_dm * vid/2, type: VoltageControlledVoltageSource, ports: {Np: x3, Nn: x2}
name: a_dm * vid/2, type: VoltageControlledVoltageSource, ports: {Np: x2, Nn: x4}
name: Rod/2, type: Resistor, value: Rod/2, ports: {N1: x4, N2: vo2}
name: Roc/2-Rod/4, type: Resistor, value: Roc/2-Rod/4, ports: {N1: x2, N2: x1}
name: a_cm * vic, type: VoltageControlledVoltageSource, ports: {Np: x1, Nn: GND}
]
extrainfo:The circuit diagram (a) represents a Thévenin-network model of a fully differential amplifier output, utilizing voltage-controlled voltage sources and resistors. The diagram (b) represents a Norton-network model using voltage-controlled current sources and resistors. Both models are used to describe the output behavior of the amplifier.
image_name:(b)
description:
[
name: Rod||(-2Roc), type: Resistor, value: Rod||(-2Roc), ports: {N1: Vo1, N2: Vo2}
name: Roc, type: Resistor, value: Roc, ports: {N1: Vo1, N2: GND}
name: Roc, type: Resistor, value: Roc, ports: {N1: Vo2, N2: GND}
name: GmcVic, type: VoltageControlledCurrentSource, value: GmcVic, ports: {Np: Vo1, Nn: GND}
name: GmcVic, type: VoltageControlledCurrentSource, value: GmcVic, ports: {Np: Vo2, Nn: GND}
name: GmdVid, type: VoltageControlledCurrentSource, value: GmdVid, ports: {Np: Vo1, Nn: Vo2}
]
extrainfo:This is a Norton-network model for the output ports of a fully differential amplifier, showing the connections of resistors and current sources between the nodes Vo1, Vo2, and GND.
Figure 12.7 Models for the output ports of a fully differential amplifier: (a) a Thévenin-network model and (b) a Norton-network model.
which uses voltage-controlled voltage sources, are

$$
\begin{align*}
& v_{o 1}=a_{d m} \frac{v_{i d}}{2}+a_{c m} v_{i c}+\frac{R_{o d}}{2} i_{o d}+R_{o c} i_{o c}  \tag{12.16}\\
& v_{o 2}=-a_{d m} \frac{v_{i d}}{2}+a_{c m} v_{i c}-\frac{R_{o d}}{2} i_{o d}+R_{o c} i_{o c} \tag{12.17}
\end{align*}
$$

where

$$
\begin{align*}
& a_{d m}=\left.\frac{v_{o d}}{v_{i d}}\right|_{i_{o d}=0} \quad a_{c m}=\left.\frac{v_{o c}}{v_{i c}}\right|_{i_{o c}=0}  \tag{12.18}\\
& R_{o d}=\left.\frac{v_{o d}}{i_{o d}}\right|_{v_{i d}=0} \quad R_{o c}=\left.\frac{v_{o c}}{i_{o c}}\right|_{v_{i c}=0} \tag{12.19}
\end{align*}
$$

and $\quad v_{i d}=v_{i 1}-v_{i 2}, \quad v_{i c}=\left(v_{i 1}+v_{i 2}\right) / 2, \quad v_{o d}=v_{o 1}-v_{o 2}, \quad v_{o c}=\left(v_{o 1}+v_{o 2}\right) / 2, \quad i_{o d}=$ $\left(i_{o 1}-i_{o 2}\right) / 2$, and $i_{o c}=\left(i_{o 1}+i_{o 2}\right) / 2$. Figure $12.7 b$ shows an alternative model that uses voltage-controlled current sources, and the corresponding equations are

$$
\begin{align*}
& i_{o 1}=i_{o d}+i_{o c}=G_{m d} v_{i d}+G_{m c} v_{i c}+\frac{v_{o d}}{R_{o d}}+\frac{v_{o c}}{R_{o c}}  \tag{12.20}\\
& i_{o 2}=-i_{o d}+i_{o c}=-G_{m d} v_{i d}+G_{m c} v_{i c}-\frac{v_{o d}}{R_{o d}}+\frac{v_{o c}}{R_{o c}} \tag{12.21}
\end{align*}
$$

where

$$
\begin{align*}
G_{m d} & =\left.\frac{i_{o d}}{v_{i d}}\right|_{v_{o d}=0}  \tag{12.22}\\
G_{m c} & =\left.\frac{i_{o c}}{v_{i c}}\right|_{v_{o c}=0} \tag{12.23}
\end{align*}
$$

The parameters for the models in Fig. 12.7 can be computed from the corresponding halfcircuits.

The DM and CM output-load impedances can be computed using

$$
\begin{equation*}
Z_{L d}=\frac{v_{o d}}{i_{l d}} \tag{12.24}
\end{equation*}
$$

and

$$
\begin{equation*}
Z_{L c}=\frac{v_{o c}}{i_{l c}} \tag{12.25}
\end{equation*}
$$

where $i_{l d}=\left(i_{l 1}-i_{l 2}\right) / 2, i_{l c}=\left(i_{l 1}+i_{l 2}\right) / 2$, and $i_{l 1}$ and $i_{l 2}$ are defined in Fig. 12.4. A fully balanced output load can be modeled using a passive network of the form shown in Fig. 12.6a or Fig. $12.6 b$, with $Z_{i d}$ and $Z_{i c}$ replaced by $Z_{L d}$ and $Z_{L c}$, respectively.

The DM and CM half-circuits for the amplifier, signal source, and output load in Fig. 12.4 are shown in Figs. 12.8 and 12.9. The DM load $Z_{L d}$ and the CM load $Z_{L c}$ can be found using (12.24) and (12.25) for the load network in Fig. 12.4, and the resulting load elements are

$$
\begin{gather*}
Z_{L d}=Z_{L 2} \|\left(2 Z_{L 1}\right)  \tag{12.26}\\
Z_{L c}=Z_{L 1} \tag{12.27}
\end{gather*}
$$

The DM and CM loads are different for the following reason. The axis of symmetry in Fig. 12.4 passes through the middle of $Z_{L 2}$. For purely DM signals, points along the axis of symmetry are ac grounds (see Section 3.5.5). Therefore, the load for the DM half-circuit is half of $Z_{L 2}$
image_name:(a)
description:
[
name: Vsd/2, type: VoltageSource, value: Vsd/2, ports: {Np: Vsd/2, Nn: GND}
name: Rsd/2, type: Resistor, value: Rsd/2, ports: {N1: Vsd/2, N2: Vid/2}
name: Zid/2, type: Resistor, value: Zid/2, ports: {N1: Vid/2, N2: GND}
]
extrainfo:The circuit diagram represents a differential mode half-circuit with a voltage source, a series resistor, and a load resistor to ground. The current flowing through the circuit is labeled as 'iid'.

image_name:(b)
description:
[
name: a_dm*vid/2, type: VoltageSource, value: a_dm, ports: {Np: Vid/2, Nn: GND}
name: R_od/2, type: Resistor, value: R_od/2, ports: {N1: Vid/2, N2: Vod/2}
name: Z_Ld/2, type: Resistor, value: Z_Ld/2, ports: {N1: Vod/2, N2: GND}
]
extrainfo:The circuit diagram represents the output port using a Thevenin equivalent for a differential signal source and amplifier. The current flowing through the circuit is labeled as 'iod'.

image_name:(c)
description:
[
name: GmdVid, type: VoltageControlledCurrentSource, ports: {Np: Vod/2, Nn: GND}
name: Rod, type: Resistor, value: Rod/2, ports: {N1: Vod/2, N2: Vod/2}
name: ZLd, type: Other, value: ZLd/2, ports: {N1: Vod/2, N2: GND}
]
extrainfo:The circuit diagram represents a differential signal source and amplifier using a Thevenin equivalent. The current flowing through the circuit is labeled as 'iod'.

Figure 12.8 DM half-circuits for a fully differential signal source and amplifier: (a) the input port, (b) the output port using a Thevenin equivalent, (c) the output port using a Norton equivalent.
image_name:(a)
description:
[
name: Vsc, type: VoltageSource, value: Vsc, ports: {Np: Vsc, Nn: GND}
name: Rsc, type: Resistor, value: Rsc, ports: {N1: Vsc, N2: Vic}
name: Zic, type: Other, value: Zic, ports: {N1: Vic, N2: GND}
]
extrainfo:The circuit diagram represents a differential signal source and amplifier using a Thevenin equivalent. The current flowing through the circuit is labeled as 'ic'. The input voltage source 'Vsc' is connected to a resistor 'Rsc' and an impedance 'Zic', forming a series circuit with the ground.
image_name:(b)
description:
[
name: Vi, type: VoltageSource, value: acmVic, ports: {Np: Vi, Nn: GND}
name: Roc, type: Resistor, value: Roc, ports: {N1: Vi, N2: Voc}
name: ZLc, type: Impedance, value: ZLc, ports: {N1: Voc, N2: GND}
]
extrainfo:The circuit diagram represents the output port of a fully differential signal source and amplifier using a Thevenin equivalent. The current flowing through the circuit is labeled as 'ioc'.
image_name:(c)
description:
[
name: GmcVic, type: CurrentSource, value: GmcVic, ports: {Np: Vic, Nn: GND}
name: Roc, type: Resistor, value: Roc, ports: {N1: Voc, N2: Vic}
name: ZLc, type: Other, value: ZLc, ports: {N1: Voc, N2: GND}
]
extrainfo:The circuit diagram (c) represents the output port using a Norton equivalent for a fully differential signal source and amplifier. The current source GmcVic is connected between Vic and GND, and the resistor Roc is connected between Voc and Vic. ZLc is connected between Voc and GND.
Figure 12.9 CM half-circuits for a fully differential signal source and amplifier: (a) the input port, $(b)$ the output port using a Thévenin equivalent, $(c)$ the output port using a Norton equivalent.

image_name:Figure 12.10
description:
[
name: a_cm v_ic, type: VoltageControlledVoltageSource, ports: {Np: Node1, Nn: GND}
name: a_dm v_id/2, type: VoltageControlledVoltageSource, ports: {Np: v_o1, Nn: Node1}
name: a_dm v_id/2, type: VoltageControlledVoltageSource, ports: {Np: Node1, Nn: v_o2}
]
extrainfo:The circuit diagram represents a simple small-signal model for a balanced fully differential op amp, assuming infinite input impedance and zero output impedance. It includes two differential voltage-controlled voltage sources and one common-mode voltage-controlled voltage source.

Figure 12.10 A simple small-signal model for a balanced fully differential op amp, assuming infinite input impedance and zero output impedance.
in parallel with $Z_{L 1}$. However, points along the axis of symmetry are open circuits for purely CM signals (see Section 3.5.5). Therefore, $Z_{L 2}$ does not affect the load in the CM half-circuit.

These amplifier models can be used to model any balanced, fully differential amplifier, including an op amp. If the model is simplified to just the dependent sources (assuming infinite input impedance and zero output impedance), the equations that describe the model reduce to

$$
\begin{equation*}
v_{o d}=v_{o 1}-v_{o 2}=a_{d m} v_{i d} \tag{12.28}
\end{equation*}
$$

and

$$
\begin{equation*}
v_{o c}=\frac{v_{o 1}+v_{o 2}}{2}=a_{c m} v_{i c} \tag{12.29}
\end{equation*}
$$

In an ideal, fully differential op amp, $a_{c m}=0$ and $a_{d m} \rightarrow-\infty$. If $a_{c m}=0$, then $v_{o c}=0$ if $v_{i c}$ is finite. If $a_{d m} \rightarrow-\infty$, then $v_{i d} \rightarrow 0$ if $v_{o d}$ is finite. A simple small-signal model for a balanced, fully differential op amp that is based on (12.28) and (12.29) is shown in Fig. 12.10. Because of its simplicity, this model will be used to illustrate some key points in the following sections.

## 12.4 Common-Mode Feedback

The fully differential feedback amplifier in Fig. 12.1 $a$ is redrawn in Fig. 12.11 $a$ using the ideal op-amp model from Fig. 12.10. In Fig. 12.11a, the axis of symmetry is shown as a dashed line. The $a_{c m}$ controlled source is shown twice, once on each side of the axis of symmetry. The DM half-circuit is shown in Fig. 12.11b. Here all nodes intersecting the axis of symmetry are connected to ac ground. Using this half-circuit and letting $a_{d m} \rightarrow-\infty$, the differential gain is

$$
\begin{equation*}
\frac{v_{o d}}{v_{s d}}=\frac{v_{o d}}{v_{s 1}-v_{s 2}}=-\frac{R_{3}}{R_{1}} \tag{12.30}
\end{equation*}
$$

Thus, the DM output voltage is determined by the DM gain, which is accurately set by the DM feedback loop in Fig. 12.11b. However, the CM output voltage is set by a different feedback loop. The CM half-circuit for Fig. 12.1 $a$ is shown in Fig. 12.11c. If $a_{c m}=0$, the closed-loop CM gain $v_{o c} / v_{s c}$ is zero, and the loop gain (or return ratio) for the CM feedback loop in Fig. $12.11 c$ is zero. Therefore, the CM output voltage $v_{o c}$ is independent of the CM op-amp input voltage $v_{i c}$ and the CM source voltage $v_{s c}$. In practice, $\left|a_{c m}\right|$ is nonzero but small in op amps that use an input differential pair with a tail current source because the tail current source provides local feedback for CM signals and makes the CM gain of the input stage small. If $\left|a_{c m}\right|$ is small, the magnitude of the loop gain (or return ratio) for the CM feedback loop in Fig. 12.11c is small, and this feedback loop exerts little control on the CM output voltage. As a
image_name:(a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: vs1, N2: vi1}
name: R3, type: Resistor, value: R3, ports: {N1: vi1, N2: vo1}
name: acmVic, type: VoltageSource, value: acmVic, ports: {Np: x1, Nn: GND}
name: admVid/2, type: VoltageSource, value: admVid/2, ports: {Np: x1, Nn: vo2}
name: vsd/2, type: VoltageSource, value: vsd/2, ports: {Np: vsd/2, Nn: GND}
name: Vid/2, type: VoltageSource, value: Vid/2, ports: {Np: Vid/2, Nn: GND}
name: vsc, type: VoltageSource, value: vsc, ports: {Np: vsc, Nn: GND}
]
extrainfo:The circuit is an inverting feedback amplifier with symmetric configuration. It utilizes resistors and voltage sources to manage differential and common-mode signals. The nodes vi1 and vo1 are part of the feedback loop, while x1 and vo2 are influenced by the differential mode voltage source admVid/2.

image_name:(b)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: vsd/2, N2: vid/2}
name: R3, type: Resistor, value: R3, ports: {N1: vid/2, N2: vod/2}
name: admVid/2, type: VoltageSource, value: admVid/2, ports: {Np: GND, Nn: vod/2}
]
extrainfo:The circuit diagram (b) represents a differential mode half-circuit. It includes resistors R1 and R3, and several voltage sources that provide differential and common-mode signals. The symmetry axis indicates the balanced nature of the differential circuit.
image_name:(c)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vsc, N2: Vic}
name: R3, type: Resistor, value: R3, ports: {N1: Vic, N2: Voc}
name: Vsc, type: VoltageSource, value: Vsc, ports: {Np: Vsc, Nn: GND}
name: acmVic, type: VoltageSource, value: acmVic, ports: {Np: GND, Nn: Voc}
]
extrainfo:The circuit diagram represents a common-mode feedback loop with resistors R1 and R3, and voltage sources Vsc and VcmVic. It shows the path from the input Vsc through the resistors to the output Voc, with a feedback mechanism represented by VcmVic.

Figure 12.11 (a) The inverting feedback amplifier of Fig. 12.1 $a$, using the op-amp model ${ }_{-}^{-} \quad$ in Fig. 12.10. (b) The DM half-circuit. (c) The CM half-circuit.
result, a different feedback loop with high loop gain is used to control the CM output voltage, as described next.

### 12.4.1 Common-Mode Feedback at Low Frequencies

For the op amp in Fig. 12.2, the ideal operating point biases $M_{1}-M_{5}$ in the active region and sets the dc CM output voltage $V_{O C}$ to the value that maximizes the swing at the op-amp outputs for which all transistors operate in the active region. However, as described in Section 4.3.5.1, $V_{O C}$ is very sensitive to mismatches and component variations, and the circuit is not practical from a bias stability standpoint. (Section 4.3.5.1 describes the circuit in Fig. 4.24a,
which is Fig. 12.2 with the addition of two diode-connected transistors and two ideal current sources that set the dc drain currents.) Accurately setting $V_{O C}$ in Fig. 12.2 to a desired voltage is impossible in practice because $I_{D 5}$ is set independently of $\left|I_{D 3}\right|+\left|I_{D 4}\right|$.

To set $V_{O C}$ to a desired de voltage $V_{C M}$ that biases all transistors in the active region and maximizes the output voltage swing, either $V_{\text {BIAS }}$ or $V_{G S 5}$ must be adjusted so that $I_{D 5}=$ $\left|I_{D 3}\right|+\left|I_{D 4}\right|$ when $V_{S D 3}=V_{S D 4}=V_{D D}-V_{C M}$, which makes $V_{O C}=V_{C M}$. We will focus on adjusting $V_{G S 5}$. Adjusting $V_{G S 5}$ to force $V_{O C}=V_{C M}$ requires the use of feedback in practice. Circuitry is added to form a negative feedback loop that adjusts $V_{G S 5}$ to set $V_{O C}=V_{C M}$. Figure 12.12 shows a block diagram of such a feedback loop, which will be referred to as the common-mode feedback (CMFB) loop. The added blocks will be called the CM-sense blocks. One CM-sense block, the CM detector, calculates the CM output voltage, $V_{o c}=\left(V_{o 1}+V_{o 2}\right) / 2$. This voltage is subtracted from the desired CM output voltage, $V_{C M}$. The difference $V_{o c}-V_{C M}$ is scaled by an amplifier with gain $a_{c m s}$. Then a dc voltage $V_{C S B I A S}$ is added, and the result is $V_{c m s}$, where

$$
\begin{equation*}
V_{c m s}=a_{c m s}\left(V_{o c}-V_{C M}\right)+V_{C S B I A S} \tag{12.31}
\end{equation*}
$$

$V_{c m s}$ drives a new op-amp input labeled CMC (for common-mode control). The CMC input is chosen so that changing $V_{c m c}$ changes $V_{o c}$ but does not affect $V_{o d}$ if the circuit is perfectly balanced. (The voltages $V_{c m s}$ and $V_{c m c}$ are equal in Fig. 12.12. The label $V_{c m c}$ will be used when referring to the CMC input of the op amp, while $V_{c m s}$ will be used to refer to the output of the CM-sense circuit.) For the op amp in Fig. 12.2, the CMC input is the gate of $M_{5}$. If the gain in this CMFB loop is high, the negative feedback forces $V_{o c} \approx V_{C M}$ and $V_{c m c}$ to be approximately constant with $V_{c m c} \approx V_{C S B I A S}$. Transistor $M_{5}$ supplies the tail current for the pair $M_{1}$ and $M_{2}$. Bias voltage $V_{C S B I A S}$ is added to provide the nominal dc component of $V_{c m c}$ that sets $\left|I_{D 3}\right|+\left|I_{D 4}\right|=I_{D 5}$ when $V_{o c}=V_{C M}$.

The magnitude of the small-signal gain from $V_{c m c}$ to $V_{o c}$ is typically much larger than unity. For example, in the op amp in Fig. 12.2, this gain magnitude is high because it is the gain of common-source $M_{5}$ with a large load resistance at the op-amp output. (This gain is computed in the next example.) Often the magnitude of the gain from $V_{c m c}$ to $V_{o c}$ is large enough to provide all the gain needed in the CMFB loop. Therefore, the CM-sense amplifier $a_{c m s}$ can have
image_name:Figure 12.12
description:The block diagram in Figure 12.12 represents a Common-Mode Feedback (CMFB) loop system. The diagram can be divided into two main sections: the common-mode control (CMC) path and the common-mode sense (CM-sense) blocks.

1. **Main Components:**
- **CMC Amplifier:** This block is represented by a triangle symbol, indicating an operational amplifier. It amplifies the common-mode control voltage \( V_{cmc} \), which is the sum of \( V_{CMC} \) and a small signal \( v_{cmc} \). The output of this amplifier is connected to the outputs \( V_{o1} \) and \( V_{o2} \).
- **CM Detector:** This block detects the common-mode output voltage \( V_{oc} \) from the outputs \( V_{o1} \) and \( V_{o2} \).
- **Summing Junctions:** These are used to sum the input signals. One summing junction calculates \( V_{oc} - V_{CM} \), and another sums \( V_{cms} \) with a bias voltage \( V_{CSBIAS} \).
- **CM-Sense Amplifier:** This amplifier, labeled with a gain \( a_{cms} \), amplifies the difference \( V_{oc} - V_{CM} \).

2. **Flow of Information or Control:**
- The CM detector receives the outputs \( V_{o1} \) and \( V_{o2} \) and determines the common-mode output voltage \( V_{oc} \).
- The difference \( V_{oc} - V_{CM} \) is calculated at a summing junction and then amplified by the CM-sense amplifier.
- The amplified signal \( V_{cms} \) is summed with a bias voltage \( V_{CSBIAS} \) to produce the control voltage \( V_{cmc} \).
- This control voltage \( V_{cmc} \) is then fed into the CMC amplifier to regulate the outputs \( V_{o1} \) and \( V_{o2} \).

3. **Labels, Annotations, and Key Indicators:**
- The gain of the CMC amplifier is labeled as \( a_{cmc} \).
- The gain of the CM-sense amplifier is labeled as \( a_{cms} \).
- \( V_{CMC} \) and \( v_{cmc} \) are components of the control voltage \( V_{cmc} \).

4. **Overall System Function:**
- The primary function of this CMFB loop is to maintain a stable common-mode voltage at the output of the system. The CM detector senses the common-mode output voltage, and any deviation from the desired common-mode voltage \( V_{CM} \) is corrected by the feedback loop. The CM-sense amplifier and the CMC amplifier work together to adjust \( V_{o1} \) and \( V_{o2} \), ensuring that the common-mode voltage remains stable and within desired limits. This system is crucial in minimizing common-mode noise and ensuring the proper functioning of differential circuits.
Figure 12.12 A conceptual block diagram of the CMFB loop.
image_name:(a)
description:The circuit diagram represents a common-mode feedback (CMFB) loop with voltage sources and controlled sources. It is designed to maintain a stable common-mode voltage by adjusting the outputs v_o1 and v_o2 based on the inputs v_i1, v_i2, and v_cm.
image_name:(b)
description:The circuit diagram represents a simplified model of a common-mode feedback (CMFB) loop with voltage sources and controlled sources. It is designed to maintain stable common-mode voltage levels in differential circuits.

Figure 12.13 The simple op-amp model of Fig. 12.10 (a) including the CMC gain $a_{c m c}$ and (b) replacing the $a_{c m}$ and $a_{c m c}$ controlled sources with an equivalent controlled source $a_{c m}^{\prime}$.
low gain, and, as a result, a wide bandwidth. Because the CM-sense amplifier is in the CMFB loop, wide bandwidth in this amplifier simplifies the frequency compensation of the CMFB loop. If $V_{o c}=V_{C M}$ in Fig. 12.12, $V_{c m c}=V_{C S B I A S}$. In practice, the bias voltage $V_{C S B I A S}$ is usually generated in the CM -sense-amplifier circuit. Hence, the CM -sense amplifier is designed so that when its differential input voltage is zero, its output voltage equals the nominal bias voltage required at the single-ended CMC input. For the op amp in Fig. 12.2, this bias voltage is $V_{G S 5}-V_{S S}$. Practical CM-sense amplifiers that can generate such an output bias voltage will be shown in Section 12.5.

The simple op-amp model in Fig. 12.10 is modified to include the CM control (CMC) input in Fig. 12.13a. Controlled source $a_{c m c}$ models the small-signal voltage gain from this new input to $v_{o c}$. That is,

$$
\begin{equation*}
a_{c m c}=\left.\frac{v_{o c}}{v_{c m c}}\right|_{v_{i c}=0} \tag{12.32}
\end{equation*}
$$

When this gain is included, the equation for the CM output voltage in (12.29) becomes

$$
\begin{equation*}
v_{o c}=a_{c m} v_{i c}+a_{c m c} v_{c m c} \tag{12.33}
\end{equation*}
$$

#### EXAMPLE

Compute the three voltage gains in the model in Fig. 12.13a for the op amp in Fig. 12.2. Use the $0.8-\mu \mathrm{m}$ CMOS model data in Table 2.3 with $\left|V_{o v}\right|=\left|V_{G S}-V_{t}\right|=0.2 \mathrm{~V}$ and $L_{\text {eff }}=0.8 \mu \mathrm{~m}$ for all devices. Take $I_{D 5}=200 \mu \mathrm{~A},\left|V_{A p}\right|=20 \mathrm{~V}$, and $V_{A n}=10 \mathrm{~V}$. (These $V_{A}$ values follow from (1.163) and the data in Table 2.3 with $L_{\text {eff }}=0.8 \mu \mathrm{~m}$.) Ignore body effect.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vod/2, G: Vid/2}
name: M3, type: PMOS, ports: {S: GND, D: Vdd/2, G: GND}
name: CLd, type: Capacitor, value: CLd, ports: {Np: Vod/2, Nn: GND}
name: Vid, type: VoltageSource, value: Vid, ports: {Np: Vid/2, Nn: GND}
]
extrainfo:The circuit in (a) is a common-source amplifier with an active load, consisting of NMOS M1 and PMOS M3. The output is taken across the capacitor CLd. The input signal is applied through the voltage source Vid.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vic, G: Vic}
name: M3, type: PMOS, ports: {S: GND, D: Voc, G: GND}
name: CLc, type: Capacitor, value: CLc, ports: {Np: Voc, Nn: GND}
name: Vic, type: VoltageSource, value: Vic, ports: {Np: Vic, Nn: GND}
name: M5h, type: NMOS, ports: {S: GND, D: s1d5h, G: Vcmc}
name: Vcmc, type: VoltageSource, value: Vcmc, ports: {Np: Vcmc, Nn: GND}
]
extrainfo:The circuit diagram (b) is a CM half-circuit for an op-amp, showing the output load capacitance CLc. It includes NMOS and PMOS transistors, voltage sources, and a capacitor. The NMOS transistor M1 is connected to the ground and the node Vic, which is also connected to the voltage source Vic. The PMOS transistor M3 connects the node Vic to the power supply VDD. The capacitor CLc is connected between the node Voc and the ground.

Figure 12.14 (a) The DM half-circuit for Fig.
12.2, explicitly showing the output load capacitance. (b) The CM half-circuit for Fig. 12.2, explicitly showing the output load capacitance.

The DM half-circuit is shown in Fig. 12.14a. It is a common-source amplifier with an active load. The low-frequency DM gain is

$$
\begin{equation*}
a_{d m}=\frac{v_{o d}}{v_{i d}}=-g_{m 1}\left(r_{o 1} \| r_{o 3}\right) \tag{12.34}
\end{equation*}
$$

Using (1.181) and $I_{D 1}=\left|I_{D 3}\right|$ in (12.34),

$$
a_{d m}=-\frac{2 I_{D 1}}{V_{o v 1}}\left(\frac{V_{A 1}}{I_{D 1}} \| \frac{\left|V_{A 3}\right|}{\left|I_{D 3}\right|}\right)=-\frac{2}{V_{o v 1}} \frac{V_{A 1}\left|V_{A 3}\right|}{V_{A 1}+\left|V_{A 3}\right|}=-\frac{2}{0.2} \frac{10 \times 20}{10+20}=-66.7
$$

The CM half-circuit is shown in Fig. 12.14b. To form this half-circuit, the original circuit was transformed into a symmetric circuit by splitting $M_{5}$ into two identical halves in parallel, each called $M_{5 h}$ with $(W / L)_{5 h}=(W / L)_{5} / 2\left(W_{5 h}=W_{5} / 2, L_{5 h}=L_{5}\right)$ and $I_{D 5 h}=I_{D 5} / 2$. This half-circuit has two inputs, $v_{i c}$ and $v_{c m c}$. First, we find the gain from $v_{c m c}$ to $v_{o c}$ with $v_{i c}=0$. This circuit consists of common-source $M_{5 h}$, common-gate $M_{1}$, and active load $M_{3}$. The low-frequency gain is

$$
\begin{equation*}
a_{c m c}=\frac{v_{o c}}{v_{c m c}}=-g_{m 5 h}\left(R_{o(\text { down })} \| r_{o 3}\right) \tag{12.35}
\end{equation*}
$$

where $R_{o(\text { down })}$ is the resistance looking into the drain of $M_{1}$, which is given by

$$
\begin{equation*}
R_{o(\text { down })}=r_{o 1}\left(1+g_{m 1} r_{o 5 h}\right) \approx r_{o 1}\left(g_{m 1} r_{o 5 h}\right) \tag{12.36}
\end{equation*}
$$

Using the approximation in (12.36), (1.181), and $I_{D 1}=\left|I_{D 3}\right|=I_{D 5 h}$ in (12.35), we find

$$
\begin{aligned}
a_{c m c} & =-\frac{2 I_{D 5 h}}{V_{o v h}}\left\{\left[\frac{V_{A 1}}{I_{D 1}}\left(\frac{2 I_{D 1}}{V_{o v 1}} \frac{V_{A 5 h}}{I_{D 5 h}}\right)\right] \| \frac{\left|V_{A 3}\right|}{\left|I_{D 3}\right|}\right\}=-\frac{2}{V_{o v 5 h}} \frac{V_{A 1}\left(\frac{2 V_{A 5 h}}{V_{o v 1}}\right)\left|V_{A 3}\right|}{V_{A 1}\left(\frac{2 V_{A 5 h}}{V_{o v 1}}\right)+\left|V_{A 3}\right|} \\
& =-\frac{2}{0.2} \frac{10\left(\frac{2(10)}{0.2}\right) 20}{10\left(\frac{2(10)}{0.2}\right)+20}=-196
\end{aligned}
$$

Finally, we calculate the gain from $v_{i c}$ to $v_{o c}$ with $v_{c m c}=0$. In this circuit, $M_{1}$ is a commonsource amplifier with a degeneration resistance that is the output resistance of $M_{5 h}$. The gain is

$$
\begin{equation*}
a_{c m}=\frac{v_{o c}}{v_{i c}}=-\frac{g_{m 1}}{1+g_{m 1} r_{o 5 h}}\left(R_{o(\mathrm{down})} \| r_{o 3}\right) \approx-\frac{1}{r_{o 5 h}}\left(R_{o(\mathrm{down})} \| r_{o 3}\right) \tag{12.37}
\end{equation*}
$$

The approximation is accurate if $g_{m 1} r_{o 5 h} \gg 1$. Using the approximation in (12.36), (1.181), and $I_{D 1}=\left|I_{D 3}\right|=I_{D 5 h}$ in (12.37),

$$
\begin{align*}
a_{c m} & =-\frac{I_{D 5 h}}{V_{A 5 h}}\left\{\left[\frac{V_{A 1}}{I_{D 1}}\left(\frac{2 I_{D 1}}{V_{o v 1}} \frac{V_{A 5 h}}{I_{D 5 h}}\right)\right] \| \frac{\left|V_{A 3}\right|}{\left|I_{D 3}\right|}\right\}=-\frac{1}{V_{A 5 h}} \frac{V_{A 1}\left(\frac{2 V_{A 5 h}}{V_{o v 1}}\right)\left|V_{A 3}\right|}{V_{A 1}\left(\frac{2 V_{A 5 h}}{V_{o v 1}}\right)+\left|V_{A 3}\right|} \\
& =-\frac{1}{10} \frac{10\left(\frac{2(10)}{0.2}\right) 20}{10\left(\frac{2(10)}{0.2}\right)+20}=-1.96 \tag{12.38}
\end{align*}
$$

In this example, $\left|a_{c m c}\right|$ is much larger than $\left|a_{c m}\right|$ because the transconductance in (12.35) is much larger than the degenerated transconductance in (12.37).

The CMFB loop uses negative feedback to make $V_{o c} \approx V_{C M}$. If $V_{C M}$ changes by a small amount from its design value due to parameter variations in the circuit that generates $V_{C M}$, $V_{o c}$ should change by an equal amount so that $V_{o c}$ tracks $V_{C M}$. The ratio $\Delta V_{o c} / \Delta V_{C M}$ is the closed-loop small-signal gain of the CMFB loop, which from Fig. 12.12 is

$$
\begin{equation*}
A_{C M F B}=\frac{\Delta V_{o c}}{\Delta V_{C M}}=\frac{v_{o c}}{v_{c m}}=\frac{a_{c m s}\left(-a_{c m c}\right)}{1+a_{c m s}\left(-a_{c m c}\right)} \tag{12.39}
\end{equation*}
$$

If $a_{c m s}\left(-a_{c m c}\right) \gg 1, A_{C M F B} \approx 1$ and $\Delta V_{o c} \approx \Delta V_{C M}$.
The CM gain from $v_{i c}$ to $v_{o c}$ is affected by the CMFB loop. This gain can be calculated using the CMFB block diagram in Fig. 12.12 and the op-amp model in Fig. 12.13a. The op-amp CM gain when the CMFB is present, which we will call $a_{c m}^{\prime}$, is found with the DM input signal set to zero. Using (12.31), the small-signal CM-sense voltage is related to the small-signal CM output voltage by

$$
\begin{equation*}
v_{c m s}=a_{c m s} v_{o c} \tag{12.40}
\end{equation*}
$$

Using this equation, (12.33), and $v_{c m s}=v_{c m c}$, we find

$$
\begin{equation*}
a_{c m}^{\prime}=\left.\frac{v_{o c}}{v_{i c}}\right|_{\text {with CMFB }}=\frac{a_{c m}}{1+a_{c m s}\left(-a_{c m c}\right)} \tag{12.41}
\end{equation*}
$$

Therefore, $\left|a_{c m}^{\prime}\right| \ll\left|a_{c m}\right|$ if $\left|a_{c m s}\left(-a_{c m c}\right)\right| \gg 1$.

The CM gain for a balanced differential amplifier with CMFB can be found using either the model in Fig. $12.13 a$ or $12.13 b$ with $a_{c m}^{\prime}$ given by (12.41). These models are equivalent because the effect of the controlled source $a_{c m c}$ that is part of the CMFB loop is included in $a_{c m}^{\prime}$.

#### EXAMPLE

Compute the CM gain from $v_{i c}$ to $v_{o c}$ when the CMFB loop is active, $a_{c m}^{\prime}$, for the op amp in the last example. Assume that $a_{c m s}=1$.

Substituting values from the last example in (12.41) with $a_{c m s}=1$ gives

$$
a_{c m}^{\prime}=\left.\frac{v_{o c}}{v_{i c}}\right|_{\text {with } \mathrm{CMFB}}=\frac{-1.96}{1+(1)(196)}=-0.01
$$

Comparing this result with (12.38), we see that the CMFB has reduced the CM gain by more than two orders of magnitude.

### 12.4.2 Stability and Compensation Considerations in a CMFB Loop

Since the CMFB loop is a negative feedback loop, stability is a key issue. For illustration purposes, consider the op amp in Fig. 12.2 driving a load capacitance and using the CMFB scheme shown in Fig. 12.12. The gain in the CMFB loop is $\left(-a_{c m c}\right) a_{c m s}$. The dominant pole $p_{1 c}$ in the CMFB loop is set by the load capacitance and the output resistance in the CM half-circuit in Fig. 12.14b. Ignoring all nondominant poles and using (12.35), we find

$$
\begin{equation*}
a_{c m c}(s)=-\frac{g_{m 5 h}\left(R_{o(\text { down })} \| r_{o 3}\right)}{1+s\left(R_{o(\text { down })} \| r_{o 3}\right) C_{L c}} \tag{12.42}
\end{equation*}
$$

At high frequencies $\left[\omega \gg\left|p_{1 c}\right|=1 /\left(R_{o(\text { down })}| | r_{o 3}\right) C_{L c}\right]$, (12.42) reduces to

$$
\begin{equation*}
\left.a_{c m c}(j \omega)\right|_{\omega \gg\left|p_{1 c}\right|} \approx-\frac{g_{m 5 h}}{j \omega C_{L c}} \tag{12.43}
\end{equation*}
$$

This equation follows from the observation that the drain current from $M_{5 h}$ flows into the load capacitor at high frequencies. From (12.43), $\left|a_{c m c}\right|=1$ at the frequency

$$
\begin{equation*}
\omega_{u, c m}=\frac{g_{m 5 h}}{C_{L c}} \tag{12.44}
\end{equation*}
$$

Nondominant poles exist in the CMFB loop, due to capacitance at the source of $M_{1}$ in Fig. $12.14 b$ and due to poles in the gain $a_{c m s}(s)$ of the CM-sense circuit. If the gain roll-off in (12.43) due to the dominant pole does not provide adequate phase margin for the CMFB loop, the unity-gain frequency for the CMFB loop gain can be decreased to increase the phase margin. From (12.44), increasing the CM load capacitance $C_{L c}$ decreases $\omega_{u, c m}$. However, adding capacitance to the op-amp outputs increases both the CM and DM load capacitances, as can be seen from (12.26) and (12.27). The CMFB loop gain may need a smaller unity-gain frequency than the DM loop gain because the CMFB loop may have more high frequency poles than the DM loop. For example, poles of $a_{c m s}(s)$ of the CM-sense amplifier and the pole associated with the capacitance at the source of $M_{1}$ in Fig. $12.14 b$ are poles in the CMFB loop. However, they are not poles in the DM feedback loop since the source of $M_{1}$ is an ac ground in the DM half-circuit. As a result, the load capacitance required in (12.43) to provide adequate phase margin for the CMFB loop may result in a larger DM load capacitance than desired, thereby overcompensating the DM feedback loop. While such overcompensation increases the phase margin of the DM feedback loop, it also decreases the unity-gain bandwidth of the DM
image_name:Figure 12.15
description:
[
name: M1, type: NMOS, ports: {S: X1, D: Vo1, G: Vi1}
name: M2, type: NMOS, ports: {S: X1, D: Vo2, G: Vi2}
name: M3, type: PMOS, ports: {S: VDD, D: Vo1, G: Vbias}
name: M4, type: PMOS, ports: {S: VDD, D: Vo2, G: Vbias}
name: M51, type: NMOS, ports: {S: -VSS, D: X1, G: VBB2}
name: M52, type: NMOS, ports: {S: -VSS, D: X1, G: Vcmc}
]
extrainfo:The circuit is a differential amplifier with common-mode feedback. It uses NMOS and PMOS transistors to achieve amplification. The differential inputs are Vi1 and Vi2, and the outputs are Vo1 and Vo2. The circuit includes a common-mode feedback mechanism using M51 and M52 to stabilize the common-mode voltage.
Figure 12.15 The op amp of Fig. 12.2 modified by replacing $M_{5}$ with $M_{51}$ with $V_{g 51}$ constant, and $M_{52}$ with $V_{g 52}=V_{c m c}$.
loop gain and the 3-dB bandwidth of the DM closed-loop gain, which is undesirable when high bandwidth is desired in the DM feedback circuit to amplify a wide-band DM signal.

To overcome this problem, (12.44) shows that decreasing $g_{m 5 h}=g_{m 5} / 2$ decreases the unity-gain frequency of the gain $a_{c m c}$ in the CMFB loop and therefore increases the phase margin of the CMFB loop. Assuming that the tail bias current $I_{D 5}$ cannot be changed, this decrease could be achieved by decreasing $(W / L)_{5}$. However, decreasing $(W / L)_{5}$ increases $V_{o v 5}$, which affects the CM input range of the op amp. Alternatively, a reduction in $g_{m 5 h}$ can be realized by splitting $M_{5}$ into two parallel transistors, which are labeled $M_{51}$ and $M_{52}$ in Fig. 12.15. Transistor $M_{51}$ has its gate connected to a bias voltage and carries a constant drain current. The gate of $M_{52}$ acts as the CMC input. To keep the bias currents in the op amp the same as in Fig. 12.2, we want

$$
\begin{equation*}
I_{D 51}+I_{D 52}=I_{D 5} \tag{12.45}
\end{equation*}
$$

To keep the CM input range of the op amp unchanged, we need

$$
\begin{equation*}
V_{o v 51}=V_{o v 52}=V_{o v 5} \tag{12.46}
\end{equation*}
$$

From (1.181), (12.45), and (12.46),

$$
\begin{equation*}
g_{m 52}=\frac{2 I_{D 52}}{V_{o v 52}}<g_{m 5}=\frac{2 I_{D 5}}{V_{o v 5}} \tag{12.47}
\end{equation*}
$$

as desired. For the circuit in Fig. 12.15, $g_{m 52 h}=g_{m 52} / 2$ replaces $g_{m 5 h}=g_{m 5} / 2$ in (12.42), (12.43), and (12.44). A disadvantage of this approach is that reducing the transconductance in (12.42) reduces the magnitude of the CMC gain, $\left|a_{c m c}\right|$, at dc.

## 12.5 CMFB Circuits

In this section, circuits that detect the CM output voltage and generate a signal (a current or a voltage) that is a function of $V_{O C}-V_{C M}$ are described. These circuits are part of the CMFB loop and will be referred to as CM -sense circuits. For simplicity, these circuits are described using the simple, fully differential amplifier shown in Fig. 12.2.

### 12.5.1 CMFB Using Resistive Divider and Amplifier

A straightforward way to detect the CM output voltage is to use two equal resistors, as shown in Fig. 12.16 $a$. ${ }^{3,4}$ The voltage between the two resistors is

$$
\begin{equation*}
V_{o c}=\frac{V_{o 1}+V_{o 2}}{2} \tag{12.48}
\end{equation*}
$$

This voltage is subtracted from the desired CM output voltage, $V_{C M}$, and scaled by the differencing CM-sense amplifier in Fig. $12.16 b$ that consists of source-coupled pair $M_{21}-M_{22}$, diode-connected loads $M_{23}$ and $M_{24}$, and tail-current source $M_{25}$. The output of this amplifier, which drives the CMC input of the op amp, is

$$
\begin{equation*}
V_{c m s}=a_{c m s}\left(V_{o c}-V_{C M}\right)+V_{C S B I A S} \tag{12.49}
\end{equation*}
$$

If $V_{o c}=V_{C M}$, then $V_{c m s}=V_{C S B I A S}$. Therefore, for the circuit of Fig. $12.16 b, V_{C S B I A S}=$ $V_{G S 23}-V_{S S}$ when $I_{D 23}=I_{D 25} / 2$. The value of $V_{G S 23}$ [or, equivalently, $I_{D 23}$ and $(W / L)_{23}$ ] is chosen so that $I_{D 5}$ is equal to the design value of $\left|I_{D 3}\right|+\left|I_{D 4}\right|$ in Fig. 12.2 when $V_{o c}=V_{C M}$.
image_name:Figure 12.16 (a)
description:The circuit is a common-mode feedback (CMFB) system using a resistive divider to detect the common-mode voltage Voc and a CM-sense amplifier to adjust VCM. Two resistors Rcs form a voltage divider between Vo1 and Vo2, producing Voc. The CM Sense Amp takes Vcms as input and outputs VCM to control the common-mode voltage.

image_name:(b)
description:
[
name: M21, type: PMOS, ports: {S: VDD, D: X3, G: VCM}
name: M22, type: PMOS, ports: {S: VDD, D: X3, G: Voc}
name: M25, type: PMOS, ports: {S: VDD, D: X3, G: VB}
name: M23, type: NMOS, ports: {S: VSS, D: X1, G: X1}
name: M24, type: NMOS, ports: {S: VSS, D: X2, G: X2}
]
extrainfo:The circuit is a common-mode feedback (CMFB) system with a CM-sense amplifier. It uses PMOS and NMOS transistors to control the common-mode voltage. The PMOS transistors are connected to the VDD, and the NMOS transistors are connected to the VSS. The system adjusts the output VCM to maintain a stable common-mode voltage.

Figure 12.16 (a) CMFB using a resistive divider to detect $V_{o c}$ and a CM-sense amplifier. (b) A schematic for the CM -sense amplifier that can be used with the op amp in Fig. 12.2.

In (12.49), $a_{c m s}$ is the small-signal voltage gain of the CM-sense amplifier

$$
\begin{equation*}
a_{c m s}=\left.\frac{v_{c m s}}{v_{o c}}\right|_{\text {CMFB loop open }}=\frac{1}{2} \frac{g_{m 21}}{g_{m 23}} \tag{12.50}
\end{equation*}
$$

Here, we have assumed that the CM gain of the CM-sense amplifier is much smaller in magnitude than its DM gain. The factor of $1 / 2$ multiplies $g_{m 21} / g_{m 23}$ in $(12.50)$ because the output is taken from only one side of the differential amplifier.

#### EXAMPLE

Determine the value of $V_{C M}$ that maximizes the output swing for the differential op amp in Fig. 12.2. Use the CMFB scheme in Fig. 12.16a, and design the CM-sense amplifier in Fig. 12.16b. Assume that the CM-sense resistors $R_{c s}$ are very large and can be neglected when computing small-signal voltage gains for the op amp. Use the data and assumptions in the next-to-last example with $V_{D D}=V_{S S}=2.5 \mathrm{~V}$. Assume $V_{i c}=0$. Ignore the body effect.

For the op amp in Fig. 12.2, if the magnitude of its DM gain is large and if the op amp operates in a DM negative feedback loop (for example, as shown in Fig. 12.1a), $V_{i d} \approx 0$. Therefore, both op-amp inputs will be close to ground since $V_{i c}=0$; that is, $V_{i 1}=V_{i c}+$ $V_{i d} / 2 \approx 0$ and $V_{i 2}=V_{i c}-V_{i d} / 2 \approx 0$. The output $V_{o 1}$ reaches its lower limit when $M_{1}$ enters the triode region, which occurs when $V_{g d 1}=V_{t 1}$; therefore,

$$
V_{o 1(\min )}=-V_{t 1}+V_{i 1} \approx-V_{t 1}=-0.7 \mathrm{~V}
$$

(Body effect would increase $V_{t 1}$ and decrease $V_{o 1(\min )}$.) The upper output swing limit occurs when $M_{3}$ enters the triode region, and

$$
V_{o 1(\max )}=V_{D D}-\left|V_{o v 3}\right|=2.5-0.2=2.3 \mathrm{~V}
$$

To maximize the output swing, the dc CM output voltage $V_{O C}$ should be halfway between the swing limits:

$$
V_{O C}=\frac{V_{o 1(\max )}+V_{O 1(\min )}}{2}=\frac{2.3+(-0.7)}{2}=0.8 \mathrm{~V}
$$

Therefore, we choose $V_{C M}=0.8 \mathrm{~V}$. The resulting peak differential output voltage is

$$
V_{o d(\text { peak })}=V_{o 1(\max )}-V_{o 2(\min )}=V_{o 1(\max )}-V_{o 1(\min )}=2.3-(-0.7)=3.0 \mathrm{~V}
$$

To design the CM-sense amplifier in Fig. 12.16b, we must choose a value for its lowfrequency gain. In the CMFB loop, the loop gain is $\left(-a_{c m c}\right) a_{c m s}$. From the previous example, $a_{c m c}=-196$. If we design for $a_{c m s}=1$, the CMFB loop gain is 196, and (12.39) gives $A_{C M F B}=0.995$. Therefore, $V_{o c}$ closely tracks changes in $V_{C M}$. With this choice of gain in the CM-sense amplifier in Fig. 12.16b, (12.50) gives

$$
\begin{equation*}
a_{c m s}=\frac{1}{2} \frac{g_{m 21}}{g_{m 23}}=\frac{1}{2} \frac{\sqrt{2 k_{p}^{\prime}(W / L)_{21}\left|I_{D 21}\right|}}{\sqrt{2 k_{n}^{\prime}(W / L)_{23} I_{D 23}}}=\frac{1}{2} \frac{\sqrt{k_{p}^{\prime}(W / L)_{21}}}{\sqrt{k_{n}^{\prime}(W / L)_{23}}}=1 \tag{12.51}
\end{equation*}
$$

The dc output voltage of the CM-sense amplifier when $V_{o c}=V_{C M}$ should equal the dc voltage needed at the CMC op-amp input, which is

$$
-V_{S S}+V_{G S 5}=-V_{S S}+V_{t 5}+V_{o v 5}
$$

This dc voltage is produced by the CM-sense amplifier if $M_{5}$ and $M_{23}$ have equal overdrive voltages. Assuming that $r_{o} \rightarrow \infty$, matching $V_{o v 5}$ and $V_{o v 23}$ requires that $M_{5}$ and $M_{23}$ have
equal drain-current-to- $W / L$ ratios:

$$
\begin{equation*}
\frac{I_{D 5}}{(W / L)_{5}}=\frac{I_{D 23}}{(W / L)_{23}} \tag{12.52}
\end{equation*}
$$

In (12.51) and (12.52), there are three unknowns: $I_{D 23},(W / L)_{23}$, and $(W / L)_{21}$. Therefore, many possible solutions exist. [Note that $(W / L)_{5}$ can be determined from $V_{o v 5}=0.2 \mathrm{~V}$ (by assumption) and $I_{D 5}=200 \mu \mathrm{~A}$.]

One simple solution is $I_{D 23}=I_{D 5}$ and $(W / L)_{23}=(W / L)_{5}$. Then $(W / L)_{21}$ can be determined from (12.51). While this solution is simple, it requires as much dc current in the CM -sense amplifier as in the op amp. Equations 12.51 and 12.52 can be solved with $I_{D 23}<I_{D 5}$, which reduces the power dissipation in the CM-sense amplifier. However, the magnitude of the pole associated with the $M_{5}-M_{23}$ current mirror decreases as $I_{D 23}$ decreases. To illustrate this point, we will ignore all capacitors except the gate-source capacitors for $M_{5}$ and $M_{23}$ and assume $L_{23}$ is fixed. Then the magnitude of the nondominant pole associated with the current mirror is

$$
\begin{equation*}
\left|p_{n d}\right|=\frac{g_{m 23}}{C_{g s 5}+C_{g s 23}}=\frac{\frac{2 I_{D 23}}{V_{o v 23}}}{C_{g s 5}+(2 / 3) C_{o x} W_{23} L_{23}} \tag{12.53}
\end{equation*}
$$

since the small-signal resistance of diode-connected $M_{23}$ is $1 / g_{m 23}$ (assuming that $r_{o 23} \gg$ $1 / g_{m 23}$ ). If $I_{D 23}$ is scaled by a factor $x(x<1)$ and if $M_{5}$ is unchanged, $W_{23}$ must also scale by the factor $x$ to satisfy (12.52). With this scaling, the pole magnitude in (12.53) decreases because the numerator scales by the factor $x$, but the denominator scales by a factor greater than $x$ due to the constant $C_{g 5}$ term in the denominator. This pole appears in the CMFB loop gain. Therefore, the phase margin of the CMFB loop decreases as this pole magnitude decreases due to a decrease in $I_{D 23}$.

Finally, we must verify that the CM input range of the CM-sense amplifier includes its CM input voltage, which is $V_{C M}=0.8 \mathrm{~V}$. The upper limit of the CM input voltage occurs when $M_{25}$ enters the triode region, when $\left|V_{D S 25}\right|=\left|V_{o v 25}\right|$; therefore, we want

$$
\begin{aligned}
V_{I C}<V_{D D}-\left|V_{o v 25}\right|-\left|V_{G S 21}\right| & =V_{D D}-\left|V_{o v 25}\right|-\left|V_{t p}\right|-\left|V_{o v 21}\right| \\
& =2.5-0.2-0.7-0.2=1.4 \mathrm{~V}
\end{aligned}
$$

The lower limit of the CM input voltage occurs when $M_{21}$ (or $M_{22}$ ) enters the triode region (when $V_{G D 21}=V_{t 21}$ ); hence,

$$
\begin{aligned}
V_{I C}>-V_{S S}+V_{G S 23}-\left|V_{t 21}\right| & =-V_{S S}+\left(V_{t n}+V_{o v 23}\right)-\left|V_{t p}\right| \\
& =-2.5+(0.7+0.2)-0.7=-2.3 \mathrm{~V}
\end{aligned}
$$

The applied CM input voltage of 0.8 V falls between these limits; therefore, all transistors operate in the active region as assumed.

In this CMFB approach, the inputs to the CM-sense amplifier are ideally constant, which simplifies its design. One disadvantage of this CM -sense circuit is that the $R_{c s}$ resistors and the input capacitance of the CM-sense amplifier introduce a pole in the transfer function of the CM-sense circuit and therefore in the CMFB loop. A capacitor $C_{c s}$ can be connected in parallel with each sense resistor to introduce a left-half-plane zero in the CM-sense circuit to reduce the effect of the pole at high frequencies. (See Problem 12.18.)

Another disadvantage of this CM-sense circuit is that the sense resistor $R_{c s}$ loads the op-amp output in the DM half-circuit, since the node between the resistors is a DM ac ground. This loading reduces the open-loop differential voltage gain unless $R_{c s}$ is much larger than the output resistance of the DM half-circuit.
image_name:Figure 12.17
description:The circuit diagram is a CMFB scheme with source followers as buffers between the op-amp outputs and the Rcs resistors. It aims to introduce a left-half-plane zero in the CM-sense circuit and reduce loading on the op-amp output in the DM half-circuit.

Figure 12.17 The CMFB scheme of Fig. 12.16 with source followers added as buffers between the op-amp outputs and the $R_{c s}$ resistors.

To avoid this resistive output loading, voltage buffers can be added between the op-amp outputs and the $R_{c s}$ resistors. Source followers are used as buffers in Fig. 12.17. One potential problem is that each source follower introduces a dc offset of $V_{G S}$ between its input and output. To avoid a shift in the CM operating point caused by these offsets, voltage $V_{C M}$ can be buffered by an identical source follower so that the op-amp output voltages and $V_{C M}$ experience equal offsets. However, these offsets limit the op-amp output swing since each source-follower transistor that connects to an op-amp output must remain in the active region over the entire output voltage swing.

The CMFB scheme in Fig. 12.16 can be modified to eliminate the $M_{23}-M_{5}$ current mirror from the CMFB loop, as shown in Fig. 12.18. This modified CM-sense amplifier directly injects currents to control the op-amp CM output. ${ }^{5}$ Here, $M_{21}$ in Fig. $12.16 b$ is split into two matched transistors, $M_{21 A}$ and $M_{21 B}$, and the drain of each transistor connects to an op-amp output. The current injected by $M_{21 A}$ and $M_{21 B}$ into either output is

$$
I_{c m s}=\frac{I_{26}}{4}-\frac{g_{m 21 A}}{2}\left(V_{o c}-V_{C M}\right)
$$

Transistors $M_{3}-M_{5}$ act as current sources. The CMFB loop will adjust $I_{c m s}$ so that

$$
\left|I_{D 3}\right|+\left|I_{D 4}\right|+2 I_{c m s}=I_{D 5}
$$

If $V_{o c}=V_{C M}, M_{21 A}, M_{21 B}$, and $M_{22}$ give $2 I_{c m s}=I_{26} / 2$. Therefore, $I_{26}$ should be chosen so that

$$
\left|I_{D 3}\right|+\left|I_{D 4}\right|+\frac{I_{26}}{2}=I_{D 5}
$$

when all devices are active.
An advantage of this approach is that it avoids the pole associated with the $M_{5}-M_{23}$ current mirror in Figs. 12.2 and 12.16. However, $M_{21 A}$ and $M_{21 B}$ add resistive and capacitive loading
image_name:Figure 12.18
description:The circuit is a CM-sense amplifier with an op-amp stage and a CM detection stage. M21A, M21B, and M22 are used to adjust the common-mode output voltage by injecting currents into the op-amp. The current source I26 provides biasing current for the CM sense stage.

Figure 12.18 A CM-sense amplifier that injects currents into the op amp to control the op-amp CM output voltage. In the CM-sense circuit, $(W / L)_{21 A}=(W / L)_{21 B}=0.5(W / L)_{22}$.
at the op-amp outputs. If an op amp uses cascoded devices, $M_{21 A}$ and $M_{21 B}$ can connect to low-impedance cascode nodes to reduce the impact of this loading.

### 12.5.2 CMFB Using Two Differential Pairs

A CMFB scheme that uses only transistors is shown in simplified form in Fig. 12.19. Here $M_{21}-M_{24}$ are matched. The source-coupled pairs $M_{21}-M_{22}$ and $M_{23}-M_{24}$ together sense the CM output voltage and generate an output that is proportional to the difference between $V_{o c}$ and $V_{C M} .{ }^{5,6,7}$ To show this, assume at first that the differential inputs to the two source-coupled pairs, which are $V_{o 1}-V_{C M}$ and $V_{o 2}-V_{C M}$, are small enough to allow the use of small-signal
image_name:Figure 12.19
description:The circuit uses a common-mode feedback (CMFB) configuration with two differential pairs to sense and control the common-mode output voltage. The transistors M21-M24 are matched, and the circuit ensures that the common-mode gain is zero. The current source Icms provides biasing for the feedback loop.

Figure 12.19 A CMFB approach that uses two differential pairs. This circuit can be used with the op amp in Fig. 12.2.
analysis. Also, assume that the CM gain of these source-coupled pairs is zero. Under these assumptions, the drain currents in $M_{22}$ and $M_{23}$ are

$$
\begin{align*}
& I_{d 22}=-\frac{I_{20}}{2}-g_{m 22} \frac{\left(V_{o 2}-V_{C M}\right)}{2}  \tag{12.54}\\
& I_{d 23}=-\frac{I_{20}}{2}-g_{m 23} \frac{\left(V_{o 1}-V_{C M}\right)}{2} \tag{12.55}
\end{align*}
$$

These currents are summed in diode-connected $M_{25}$ to give the CM sensor output current

$$
\begin{align*}
I_{c m s}=I_{d 25} & =-I_{d 22}-I_{d 23}=I_{20}+g_{m 22}\left(\frac{V_{o 1}+V_{o 2}}{2}-V_{C M}\right) \\
& =I_{20}+g_{m 22}\left(V_{o c}-V_{C M}\right) \tag{12.56}
\end{align*}
$$

since $g_{m 22}=g_{m 23}$. This last expression shows that the current through $M_{25}$ includes a dc term $I_{20}$ plus a term that is proportional to $V_{o c}-V_{C M}$. The current $I_{d 25}$ is mirrored by $M_{5}$ in Fig. 12.2 to produce the tail current in the op amp, which controls the CM output voltage.

The dc output of the CM-sense circuit should provide the dc voltage needed at the CMC input to give $V_{o c}=V_{C M}$. If $V_{o c}=V_{C M}$, the drain current in $M_{25}$ is

$$
\begin{equation*}
I_{D 25}=\left|I_{D 22}\right|+\left|I_{D 23}\right|=\frac{I_{20}}{2}+\frac{I_{20}}{2}=I_{20} \tag{12.57}
\end{equation*}
$$

Choosing $I_{20}=\left|I_{D 3}\right|+\left|I_{D 4}\right|$ and $(W / L)_{25}=(W / L)_{5}$ is one design option. Again, as for the CM-sense amplifier in Fig. 12.16b, a smaller value of $I_{20}$ can be used, but such current reduction causes the magnitude of the pole associated with the $M_{5}-M_{25}$ current mirror to decrease. [See the text associated with (12.53).] This scheme does not resistively load the op-amp outputs, but the source-coupled pairs $M_{21}-M_{24}$ capacitively load the op-amp outputs.

The above analysis of this CM-sense circuit assumed that $M_{21}-M_{24}$ always operate in the active region and that voltages $V_{o 1}-V_{C M}$ and $V_{o 2}-V_{C M}$ could be treated as small-signal inputs. Even if these voltages become large, the CMFB loop continues to operate as long as $M_{21}-M_{24}$ remain on. However, the small-signal analysis is not valid if the transistors leave the active region. If the op-amp outputs become large enough to turn off any of $M_{21}-M_{24}$ during a portion of the output swing, the CMFB loop will not operate properly during that part of the output swing. The requirement that $M_{21}-M_{24}$ remain on during the entire output swing imposes a limit on the output swing of the op amp. The input voltage range for which both transistors in a differential pair remain on is related to the gate overdrive voltage of those transistors. [See (3.161).] Therefore, to keep $M_{21}-M_{24}$ on for a large $V_{o 1}$ and $V_{o 2}, M_{21}-M_{24}$ require large overdrives. In contrast, the scheme that uses resistors to detect the CM output voltage does not impose such an output-swing limit since the CM-sense amplifier is driven by $V_{o c}$, which is ideally constant, rather than $V_{o 1}$ and $V_{o 2}$, which include CM and DM components.

Equation 12.56 implies that this CM-sense circuit is nearly perfect since it produces an output current that includes a constant term plus a term that is proportional to $V_{o c}-V_{C M}$. This result is based on a linear small-signal analysis. However, the inputs to the differential pairs in the CM-sense circuit can include large signals because the op-amp DM output voltage can be large. Next, a large signal analysis of this circuit is carried out.

The drain current in $M_{25}$ is

$$
\begin{equation*}
I_{d 25}=-I_{d 22}-I_{d 23} \tag{12.58}
\end{equation*}
$$

The differential input of the $M_{21}-M_{22}$ pair is $V_{o 2}-V_{C M}$. Using (3.159) and (1.166) gives

$$
\begin{align*}
& -I_{d 22}=\frac{I_{20}}{2}+\frac{k_{p}^{\prime}}{4}\left(\frac{W}{L}\right)_{22}\left(V_{o 2}-V_{C M}\right) \sqrt{4 V_{o v 22}^{2}-\left(V_{o 2}-V_{C M}\right)^{2}} \\
& \approx \frac{I_{20}}{2}+\frac{k_{p}^{\prime}}{4}\left(\frac{W}{L}\right)_{22}\left(-\frac{V_{o d}}{2}+V_{o c}-V_{C M}\right) \sqrt{4 V_{o v 22}^{2}-\left(V_{o d} / 2\right)^{2}+\left(V_{o c}-V_{C M}\right) V_{o d}} \\
& =\frac{I_{20}}{2}+\frac{k_{p}^{\prime}}{4}\left(\frac{W}{L}\right)_{22}\left(-\frac{V_{o d}}{2}+V_{o c}-V_{C M}\right) \sqrt{4 V_{o v 22}^{2}-\left(V_{o d} / 2\right)^{2}} \sqrt{1+\frac{\left(V_{o c}-V_{C M}\right) V_{o d}}{4 V_{o v 22}^{2}-\left(V_{o d} / 2\right)^{2}}} \\
& \approx \frac{I_{20}}{2}+\frac{k_{p}^{\prime}}{4}\left(\frac{W}{L}\right)_{22}\left(-\frac{V_{o d}}{2}+V_{o c}-V_{C M}\right) \sqrt{4 V_{o v 22}^{2}-\left(V_{o d} / 2\right)^{2}} \\
& \times\left[1+\frac{1}{2}\left(\frac{\left(V_{o c}-V_{C M}\right) V_{o d}}{4 V_{o v 22}^{2}-\left(V_{o d} / 2\right)^{2}}\right)-\frac{1}{8}\left(\frac{\left(V_{o c}-V_{C M}\right) V_{o d}}{4 V_{o v 22}^{2}-\left(V_{o d} / 2\right)^{2}}\right)^{2}+\cdots\right] \tag{12.59}
\end{align*}
$$

where $\left|V_{o c}-V_{C M}\right| \ll\left|V_{o d}\right|$ was assumed in the first approximation above and $\sqrt{1+x} \approx$ $1+x / 2-x^{2} / 8+\cdots$, where $x=\left[\left(V_{o c}-V_{C M}\right) V_{o d}\right] /\left[4 V_{o v 22}^{2}-\left(V_{o d} / 2\right)^{2}\right]$, was used in the last line.

The differential input of the $M_{23}-M_{24}$ pair is $V_{o 1}-V_{C M}$. A similar analysis to that above for this differential pair yields

$$
\begin{align*}
-I_{d 23} \approx & \frac{I_{20}}{2}+\frac{k_{p}^{\prime}}{4}\left(\frac{W}{L}\right)_{23}\left(\frac{V_{o d}}{2}+V_{o c}-V_{C M}\right) \sqrt{4 V_{o v 23}^{2}-\left(V_{o d} / 2\right)^{2}} \\
& \times\left[1-\frac{1}{2}\left(\frac{\left(V_{o c}-V_{C M}\right) V_{o d}}{4 V_{o v 23}^{2}-\left(V_{o d} / 2\right)^{2}}\right)-\frac{1}{8}\left(\frac{\left(V_{o c}-V_{C M}\right) V_{o d}}{4 V_{o v 23}^{2}-\left(V_{o d} / 2\right)^{2}}\right)^{2}+\cdots\right] \tag{12.60}
\end{align*}
$$

Substituting (12.59) and (12.60) in (12.58) with $V_{\text {ov } 22}=V_{\text {ov23 }}$ and $(W / L)_{22}=(W / L)_{23}$ gives

$$
\begin{align*}
I_{c m s}=I_{d 25} \approx & I_{20}+\frac{k_{p}^{\prime}}{2}\left(\frac{W}{L}\right)_{23}\left(V_{o c}-V_{C M}\right) \sqrt{4 V_{o v 23}^{2}-\left(V_{o d} / 2\right)^{2}} \\
& \times\left[1-\frac{1}{4}\left(\frac{V_{o d}^{2}}{4 V_{o v 23}^{2}-\left(V_{o d} / 2\right)^{2}}\right)-\frac{1}{8}\left(\frac{\left(V_{o c}-V_{C M}\right) V_{o d}}{4 V_{o v 23}^{2}-\left(V_{o d} / 2\right)^{2}}\right)^{2}+\cdots\right] \tag{12.61}
\end{align*}
$$

If $\left|V_{o d} / 2\right| \ll\left|2 V_{o v 23}\right|$, this equation reduces to (12.56). To interpret (12.61), first consider the case when $V_{o c}=V_{C M}$. Then (12.61) shows that the CM-sense output current is constant with $I_{c m s}=I_{20}$. Whereas $I_{c m s}$ is constant, (12.59) and (12.60) show that $I_{d 22}$ and $I_{d 23}$ are not constant if $V_{o d}$ is nonzero and time-varying, and $I_{d 22}$ and $I_{d 23}$ are nonlinear functions of $V_{o d}$ (see the plot in Fig. 3.51). However, the variation in $I_{d 22}$ due to nonzero $V_{o d}$ is equal and opposite to the variation in $I_{d 23}$ due to $V_{o d}$; therefore, these variations cancel when these currents are summed to form $I_{c m s}$. Next, consider the case when $V_{o c} \neq V_{C M} . V_{o c}$ may not equal $V_{C M}$ due to device mismatch, finite gain in the CMFB loop, or the presence of an ac component in $V_{o c}$. Equation 12.61 shows that $I_{c m s}$ has terms that include $V_{o d}^{2}$ that affect $I_{c m s}$ when $V_{o c} \neq V_{C M}$. Therefore, even if the transistors are perfectly matched, this CM sensor does not behave like an ideal CM sensor as described by (12.49). The terms that include $V_{o d}^{2}$ stem from the (square-law) nonlinearity associated with the $M_{21}-M_{22}$ and $M_{23}-M_{24}$ differential pairs that convert $V_{o 1}-V_{C M}$ and $V_{o 2}-V_{C M}$ into currents. The dependence of $I_{c m s}$ on $V_{o d}^{2}$ can cause a shift in the dc CM output voltage. Moreover, if $V_{o d}$ is not constant, this dependence can produce an ac component in $V_{o c}$.
image_name:Figure 12.20
description:
[
name: M1, type: NMOS, ports: {S: s1s2d30, D: Vo1, G: Vi1}
name: M2, type: NMOS, ports: {S: s1s2d30, D: Vo2, G: Vi2}
name: M3, type: PMOS, ports: {S: VDD, D: Vo1, G: Vb}
name: M4, type: PMOS, ports: {S: VDD, D: Vo2, G: Vb}
name: M30, type: NMOS, ports: {S: s1s2d30, D: s30d31d32, G: Vcm}
name: M31, type: NMOS, ports: {S: s30d31d32, D: X1, G: Vo1}
name: M32, type: NMOS, ports: {S: s30d31d32, D: X1, G: Vo2}
name: M33, type: NMOS, ports: {S: X1, D: s33d34d35, G: Vcm}
name: M34, type: NMOS, ports: {S: s33d34d35, D: -VSS, G: Vo2}
name: M35, type: NMOS, ports: {S: s33d34d35, D: -VSS, G: Vo1}
name: M36, type: PMOS, ports: {S: VDD, D: Vb3, G: Vb}
]
extrainfo:The circuit is a Common Mode Feedback (CMFB) circuit using NMOS and PMOS transistors. The transistors M31, M32, M34, and M35 are biased in the triode region to control the common mode voltage. The CMFB loop includes transistors M30 to M35. The circuit is designed to stabilize the common mode output voltage by adjusting the biasing of these transistors.

Figure 12.20 A CMFB approach that uses transistors $M_{31}, M_{32}, M_{34}$, and $M_{35}$ biased in the triode region.

### 12.5.3 CMFB Using Transistors in the Triode Region

Another CMFB scheme is shown in Fig. 12.20. ${ }^{8}$ The simple op amp of Fig. 12.2 is redrawn here, with $M_{5}$ replaced by $M_{30}-M_{32}$. Transistors $M_{30}-M_{35}$ are part of the CMFB loop. Here, $M_{31}, M_{32}, M_{34}$, and $M_{35}$ operate in the triode region, while $M_{30}, M_{33}$, and $M_{36}$ operate in the active region. The desired CM output voltage $V_{C M}$ is connected to the gates of $M_{34}$ and $M_{35}$. To simplify the description of this circuit, assume that $M_{30}-M_{35}$ are matched and ignore body effect. Before this CMFB approach is mathematically analyzed, its operation will be explained intuitively. At first, assume that the op-amp outputs in Fig. 12.20 have only a CM component; that is, $V_{o 1}=V_{o 2}=V_{o c}$. Then the gate voltages of $M_{31}$ and $M_{32}$ equal $V_{o c}$. Since $\left|I_{D 3}\right|=\left|I_{D 4}\right|=I_{1}$, the drain current in $M_{30}$ must equal $2 I_{1}$ to satisfy KCL. Transistors $M_{30}-M_{35}$ form a degenerated current mirror and give $I_{D 30}=I_{D 33}=2 I_{1}$ when $V_{o c}=V_{C M}$ because $M_{30}-M_{35}$ are matched. Therefore, $V_{o c}=V_{C M}$ is a possible operating point for this circuit. Negative feedback forces the circuit to this operating point, as described below. So far, we have assumed that only CM signals are present. Differential signals do not affect the operation of this feedback loop, as shown by the following analysis.

Since $M_{31}$ and $M_{32}$ are matched and operate in the triode region, the sum of their drain currents $I_{c m s}$ is [using (1.152)]

$$
\begin{align*}
I_{c m s}=I_{d 31}+I_{d 32}= & k_{n}^{\prime}\left(\frac{W}{L}\right)_{31}\left(\left(V_{o 1}+V_{S S}-V_{t 31}\right) V_{d s 31}-\frac{V_{d s 31}^{2}}{2}\right) \\
& +k_{n}^{\prime}\left(\frac{W}{L}\right)_{32}\left(\left(V_{o 2}+V_{S S}-V_{t 32}\right) V_{d s 32}-\frac{V_{d s 32}^{2}}{2}\right) \\
= & 2 k_{n}^{\prime}\left(\frac{W}{L}\right)_{31}\left(V_{o c}+V_{S S}-V_{t n}-\frac{V_{d s 31}}{2}\right) V_{d s 31} \tag{12.62}
\end{align*}
$$

since $V_{d s 31}=V_{d s 32}, V_{t 31}=V_{t 32}=V_{t n}$, and $(W / L)_{31}=(W / L)_{32}$. This equation shows that $I_{c m s}$ is dependent on the CM output voltage and independent of the differential output voltage
because changes in the drain currents in $M_{31}$ and $M_{32}$ due to nonzero $V_{o d}$ are equal in magnitude and opposite in sign. Therefore, these changes cancel when the drain currents are summed in (12.62).

Applying KVL around the lower transistors $M_{30}-M_{35}$ gives

$$
\begin{equation*}
V_{d s 31}=V_{d s 35}+V_{g s 33}-V_{g s 30} \tag{12.63}
\end{equation*}
$$

Assuming that $I_{d 30} \approx I_{d 33}$, we have $V_{g s 30} \approx V_{g s 33}$, and (12.63) reduces to

$$
\begin{equation*}
V_{d s 31} \approx V_{d s 35} \tag{12.64}
\end{equation*}
$$

Since $M_{35}$ operates in the triode region with $I_{D 35}=I_{1}$, rearranging (1.152) gives

$$
\begin{equation*}
V_{d s 35}=\frac{I_{1}}{k_{n}^{\prime}\left(\frac{W}{L}\right)_{35}\left(V_{C M}+V_{S S}-V_{t n}-\frac{V_{d s 35}}{2}\right)} \tag{12.65}
\end{equation*}
$$

Using (12.64) and (12.65) in (12.62) with $(W / L)_{31}=(W / L)_{35}$ gives

$$
\begin{align*}
I_{c m s} & \approx I_{1} \frac{2 k_{n}^{\prime}\left(\frac{W}{L}\right)_{35}\left(V_{o c}+V_{S S}-V_{t n}-\frac{V_{d s 35}}{2}\right)}{k_{n}^{\prime}\left(\frac{W}{L}\right)_{35}\left(V_{C M}+V_{S S}-V_{t n}-\frac{V_{d s 35}}{2}\right)}=2 I_{1} \frac{V_{o c}+V_{S S}-V_{t n}-\frac{V_{d s 35}}{2}}{V_{C M}+V_{S S}-V_{t n}-\frac{V_{d s 35}}{2}} \\
& =2 I_{1} \frac{V_{C M}+V_{S S}-V_{t n}-\frac{V_{d s 35}}{2}}{V_{C M}+V_{S S}-V_{t n}-\frac{V_{d s 35}}{2}}+2 I_{1} \frac{V_{o c}-V_{C M}}{V_{C M}+V_{S S}-V_{t n}-\frac{V_{d s 35}}{2}}  \tag{12.66}\\
& =2 I_{1}+2 I_{1} \frac{V_{o c}-V_{C M}}{V_{C M}+V_{S S}-V_{t n}-\frac{V_{d s 35}}{2}}
\end{align*}
$$

This last expression shows that the op-amp tail current $I_{c m s}$ consists of a constant term $2 I_{1}$ plus a term that depends on $V_{o c}-V_{C M}$. If $\left|I_{d 3}\right|=\left|I_{d 4}\right|=I_{1}$, then KCL requires that $I_{c m s}=2 I_{1}$. Using this value in (12.66) gives $V_{o c} \approx V_{C M}$, as desired. In practice, mismatches can cause $V_{o c}$ to deviate from $V_{C M}$. For example, if the drain currents in $M_{3}$ and $M_{4}$ are larger than $I_{1}$, then (12.66) shows that $V_{o c}$ must be larger than $V_{C M}$ to force $I_{c m s}$ to be larger than $2 I_{1}$.

To see that the CMFB loop here is a negative feedback loop, assume that $V_{o c}$ increases. Then the gate-source voltages on $M_{31}$ and $M_{32}$ increase, which in turn increases $I_{c m s}$. Increasing $I_{c m s}$ causes $V_{s d 3}=V_{s d 4}$ to increase since $M_{3}$ and $M_{4}$ have fixed gate-source voltages. This increase in $V_{s d 3}=V_{s d 4}$ causes $V_{o c}$ to fall and counteract the assumed increase in $V_{o c}$. In steady state, this CMFB loop forces $V_{o c} \approx V_{C M}$.

One limitation of this scheme is that the CMFB loop will not function properly whenever the output voltage swing is large enough to turn off either $M_{31}$ or $M_{32}$. Therefore, neither op-amp output is allowed to swing within a threshold voltage of $-V_{S S}$. Thus, the op-amp output swing is limited by this CMFB scheme. Another limitation is that the magnitude of the small-signal gain in the CMFB loop is smaller here than in the previous approaches because the transconductance of $M_{31}$ or $M_{32}$ in the triode region is smaller than it is in the active region. (See Problem 12.19.) Reducing the CMFB loop gain reduces the control that the CMFB loop exerts on the CM output voltage. Also, the bandwidth of the CMFB loop is lower here than in other cases due to the low transconductance of $M_{31}$ and $M_{32}$. Bandwidth requirements for the CMFB loop are considered in Section 12.8.
image_name:Figure 12.21 A CMFB scheme that uses switched capacitors
description:
[
name: a_cmcV_cmc, type: VoltageSource, ports: {Np: Vcmc, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: X1, Nn: X2}
name: C1, type: Capacitor, value: C1, ports: {Np: X1, Nn: X3}
name: C2, type: Capacitor, value: C2, ports: {Np: Vo1, Nn: Vcmc}
name: C2, type: Capacitor, value: C2, ports: {Np: Vo2, Nn: Vcmc}
name: S1, type: Switch, ports: {N1: X2, N2: VCM}
name: S2, type: Switch, ports: {N1: X1, N2: VCSBIAS}
name: S3, type: Switch, ports: {N1: X3, N2: VCM}
name: S4, type: Switch, ports: {N1: Vo1, N2: X2}
name: S5, type: Switch, ports: {N1: Vcmc, N2: X1}
name: S6, type: Switch, ports: {N1: Vo2, N2: X3}
]
extrainfo:This circuit represents a switched-capacitor common-mode feedback (CMFB) scheme. It uses capacitors instead of resistors to detect the common-mode output voltage, thus avoiding resistive loading on the op-amp. The switches control the connection paths based on the clock phases φ1 and φ2, allowing the capacitors to sample and hold the common-mode voltage.

Figure 12.21 A CMFB scheme that uses switched capacitors.

### 12.5.4 Switched-Capacitor CMFB

To overcome the op-amp output swing limitations imposed by the last two CMFB approaches and to avoid resistive output loading of the op amp, capacitors can be used to detect the CM output voltage. If the CM-sense resistors $R_{c s}$ in Fig. 12.16 are replaced with capacitors, the resistive output loading is eliminated, but these capacitors are open circuits at dc. To avoid a dc bias problem, switched capacitors can be used as the CM detector. ${ }^{9}$ A switched-capacitor (SC) CMFB scheme that is often used in switched-capacitor amplifiers and filters (see Section 6.1.7) is shown in Fig. 12.21. Here the network that consists of switches $S_{1}-S_{6}$ and capacitors $C_{1}$ and $C_{2}$ sense the CM output voltage and subtract it from the desired CM output voltage $V_{C M}$. Voltage $V_{C S B I A S}$ is a dc bias voltage. As in Fig. 6.8, assume that each switch is on when its control signal is high and is off when its control signal is low. The switches are controlled by two nonoverlapping clocks, $\phi_{1}$ and $\phi_{2}$ (that is, $\phi_{1}$ and $\phi_{2}$ are never high at the same time). In this section, we will assume that these switches are ideal. In practice, switches $S_{1}-S_{6}$ are implemented with MOS transistors. As in the previous section, we use the simple op amp in Fig. 12.2 as the op amp in Fig. 12.21.

The SC CMFB circuit is a linear, balanced, discrete-time circuit. Therefore, all points on the axis of symmetry (shown as a dashed line in Fig. 12.21) operate at ac ground for differential signals. The op-amp CMC input is along the axis of symmetry, so $V_{c m c}$ has a CM component but zero DM component. Therefore, the switched-capacitor circuit is a good CM sensor. To show that voltage $V_{c m c}$ depends on the difference between the actual and desired CM output voltages, consider the CM half-circuit shown in Fig. 12.22a. Capacitor $C_{2}$ is not switched and connects from $V_{c m c}$ to $V_{o c}$. Since $V_{c m c}$ is the gate voltage of $M_{5}$ in Fig. 12.2, there is voltage gain from $V_{c m c}$ to $V_{o c}$, which is modeled by controlled source $a_{c m c}$. Comparing this half-circuit to Fig. 6.10a, we see that $C_{2}$ connected across the gain stage and switched-capacitor $C_{1}$ form a switched-capacitor integrator. This integrator is in a negative feedback loop since its output $V_{o c}$ is connected back to a switch that connects to $C_{1}$.

When $\phi_{1}$ is high, $C_{1}$ charges to $V_{C M}-V_{C S B I A S}$. When $\phi_{2}$ is high, $C_{1}$ connects between $V_{o c}$ and $V_{c m c}$. In steady state, $V_{o c}$ is constant because the applied voltages $V_{C M}$ and $V_{C S B I A S}$ are both dc voltages and because the switched-capacitor integrator operates in a negative feedback loop. After $V_{o c}$ becomes constant, $C_{1}$ does not transfer charge onto $C_{2}$ when $\phi_{2}$ is high. This
image_name:(a)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: X1, Nn: X2}
name: C2, type: Capacitor, value: C2, ports: {Np: Vcmc, Nn: Voc}
name: Vcmc, type: VoltageSource, ports: {Np: Vcmc, Nn: GND}
name: acmc_vcmc, type: VoltageSource, ports: {Np: Voc, Nn: GND}
]
extrainfo:The circuit diagram (a) is a switched-capacitor integrator operating in a negative feedback loop. The capacitors C1 and C2, along with switches controlled by phi1 and phi2, manage charge transfer and voltage levels. Vcmc is a sum of VCMC and acmc*vcmc.
image_name:(b)
description:
[
name: M3, type: PMOS, ports: {S: VDD, D: X1, G: Vbias}
name: M4, type: PMOS, ports: {S: VDD, D: X1, G: Vbias}
name: M5, type: NMOS, ports: {S: -Vss, D: Vcsbias, G: Vcsbias}
]
extrainfo:The circuit is a replica bias circuit for generating Vcsbias for a differential op amp. It uses a combination of PMOS and NMOS transistors to establish the biasing condition. The capacitors C1 and C2 are involved in charge transfer operations, controlled by the switching signals phi1 and phi2.

Figure 12.22 (a) A CM half-circuit for Fig. 12.21. (b) Replica bias circuit for generating $V_{C S B I A S}$ for the differential op amp in Fig. 12.2.
condition is satisfied if the charge on $C_{1}$ when $\phi_{1}$ is high is the same when $\phi_{2}$ is high, or

$$
\begin{equation*}
Q\left(\phi_{1}\right)=C_{1}\left(V_{C M}-V_{C S B I A S}\right)=Q\left(\phi_{2}\right)=C_{1}\left(V_{o c}-V_{c m c}\right) \tag{12.67}
\end{equation*}
$$

This equation reduces to

$$
\begin{equation*}
V_{C M}-V_{o c}=V_{C S \mathrm{BIAS}}-V_{c m c} \tag{12.68}
\end{equation*}
$$

If $V_{C S B I A S}$ equals the nominal bias voltage required at the CMC input and if $\left|a_{c m c}\right| \gg 1, V_{c m c}$ is about constant with $V_{c m c} \approx V_{C S B I A S}$. Then (12.68) reduces to

$$
\begin{equation*}
V_{o c} \approx V_{C M} \tag{12.69}
\end{equation*}
$$

as desired. For the op amp in Fig. 12.2, bias voltage $V_{C S B I A S}$ could be generated by passing a current equal to $\left|I_{D 3}\right|+\left|I_{D 4}\right|$ through a diode-connected copy of $M_{5}$ connected to $-V_{S S}$, as shown in Fig. 12.22b. The copies of $M_{3}$ and $M_{4}$ have the same source and gate connections as in the op amp and duplicate the currents $\left|I_{D 3}\right|$ and $\left|I_{D 4}\right|$ that flow in Fig. 12.2. The voltage $V_{C S B I A S}$ is the gate voltage of the copy of $M_{5}$. Since this bias circuit uses copies or replicas of the transistors in the op amp to generate $V_{C S B I A S}$, this technique is referred to as replica biasing.

An advantage of this CMFB approach is that the op-amp output voltage swing is not limited by this CM-sense circuit because it consists only of passive elements (capacitors) and switches. (If a switch is constructed of $n$-channel and $p$-channel transistors in parallel driven by
clock $\phi$ and its inverse, respectively, it can pass any signal that falls between the power-supply voltages if $V_{D D}+V_{S S}>V_{t n}+\left|V_{t p}\right| .^{10}$ ) In practice, an MOS transistor is not an ideal switch. It must have a $W / L$ that is large enough to give a sufficiently low drain-source resistance when it is on. However, when each transistor turns off, charge from its channel and charge associated with its gate overlap capacitance transfer onto its drain and source nodes. Therefore, the MOS transistors acting as switches will transfer charge onto $C_{1}$. Let $\Delta Q$ represent the net charge transferred onto $C_{1}$ each clock period. Including the effect of this charge, (12.67) becomes

$$
\begin{equation*}
C_{1}\left(V_{C M}-V_{C S B I A S}\right)=C_{1}\left(V_{o c}-V_{c m c}\right)+\Delta Q \tag{12.70}
\end{equation*}
$$

or

$$
\begin{equation*}
V_{C M}-V_{o c}=V_{C S B I A S}-V_{c m c}+\frac{\Delta Q}{C_{1}} \tag{12.71}
\end{equation*}
$$

Comparing (12.71) with (12.68) shows that $\Delta Q / C_{1}$ introduces an offset in $V_{o c}$, making $V_{o c}$ differ from $V_{C M}$ when $V_{C S B I A S}=V_{c m c}$. If $V_{C M}$ was chosen to maximize the op-amp output swing, a shift in $V_{o c}$ will reduce the op-amp output swing. The magnitude of the charge transferred by each switch transistor increases with its width $W$ [since the gate-channel and overlap capacitances are proportional to $W$ as shown in (1.187) and (2.45)], so a trade-off exists between low switch on-resistance and small charge transfer. From (12.71), increasing $C_{1}$ reduces the effect of the transferred charge on $V_{o c}$, but increasing $C_{1}$ increases the capacitive loading at the op-amp outputs when $\phi_{2}$ is high.

## 12.6 Fully Differential Op Amps

Some fully differential op amps are presented in this section. The singled-ended counterpart of each op amp was covered in previous chapters (low-frequency operation in Chapter 6 and compensation in Chapter 9). The two-stage op amp will be covered first, followed by single-stage op amps.

### 12.6.1 A Fully Differential Two-Stage Op Amp

A fully differential two-stage op amp is shown in Fig. 12.23. Compared to its single-ended counterpart in Fig. 6.16, two differences are the addition of $M_{9}-M_{10}$, which is a copy of the common-source stage $M_{6}-M_{7}$, to generate the second output, and the removal of the gate-todrain connection on $M_{3}$ to give a symmetric input stage. The input stage is a complementary version of the differential stage in Fig. 12.2. The common-mode control (CMC) input is the gate of tail current source $M_{5}$. If the voltage at the gate of $M_{5}$ changes, the magnitudes of the drain currents in $M_{1}-M_{4}$ change by equal amounts. Therefore, $V_{d s 3}$ and $V_{d s 4}$ change by equal amounts. These voltage changes are amplified by the common-source stages $M_{6}-M_{7}$ and $M_{9}-M_{10}$ to cause equal changes in output voltages $V_{o 1}$ and $V_{o 2}$, which changes $V_{o c}$. Therefore, the CM output voltage can be controlled by a CMFB loop that connects to the gate of $M_{5}$.

In Fig. 12.23, two Miller compensation capacitors $C$ are connected across the symmetric second stages. These capacitors compensate both the DM and CM half-circuits, which are shown in Fig. 12.24. Although not shown, any of the approaches described in Chapter 9 for eliminating the right-half-plane zero associated with feedforward through the compensation capacitor could be used here.
image_name:Figure 12.23
description:
[
name: M10, type: PMOS, ports: {S: VDD, D: Vo2, G: VB1}
name: M5, type: PMOS, ports: {S: VDD, D: s5s2d5, G: Vcmc}
name: M1, type: PMOS, ports: {S: s5s2d5, D: d1d3g9, G: Vi1}
name: M2, type: PMOS, ports: {S: s5s2d5, D: d2d4g6, G: Vi2}
name: M7, type: PMOS, ports: {S: VDD, D: Vo1, G: VB1}
name: M9, type: NMOS, ports: {S: -VSS, D: Vo2, G: d1d3g9}
name: M3, type: NMOS, ports: {S: -Vss, D: d1d3g9, G: VB2}
name: M4, type: NMOS, ports: {S: -Vss, D: d2d4g6, G: VB2}
name: M6, type: NMOS, ports: {S: -VSS, D: Vo1, G: d2d4g6}
name: C, type: Capacitor, value: C, ports: {Np: Vo2, Nn: d1d3g9}
name: C, type: Capacitor, value: C, ports: {Np: Vo1, Nn: d2d4g6}
name: ro4, type: Resistor, value: ro4, ports: {N1: d2g6, N2: GND}
name: ro7, type: Resistor, value: ro7, ports: {N1: d6, N2: GND}
]
extrainfo:The circuit is a fully differential two-stage CMOS operational amplifier with Miller compensation capacitors. It includes PMOS and NMOS transistors arranged in a specific configuration to achieve differential amplification. The capacitors C are used for Miller compensation to stabilize the amplifier. The circuit has differential inputs Vi1 and Vi2 and differential outputs Vo1 and Vo2. The CMFB loop controls the CM output voltage by connecting to the gate of M5.
image_name:(a)
description:The circuit diagram shows a fully differential two-stage CMOS operational amplifier. The circuit is designed for differential mode (DM) and common mode (CM) operations with Miller compensation capacitors connected to the second stage. The amplifier uses PMOS and NMOS transistors in a symmetric configuration to achieve high gain and stability. The CM feedback loop is used to control the CM output voltage by connecting to the gate of M5. The DM half-circuit consists of two cascaded common-source amplifiers with active loads, providing the low-frequency DM gain.
image_name:(b)
description:The circuit is a fully differential two-stage CMOS op amp with Miller compensation capacitors. It includes PMOS and NMOS transistors configured to form differential pairs and current mirrors. The circuit also uses capacitors to stabilize the amplifier and compensate both differential and common-mode signals.

Figure 12.24 (a) The DM half-circuit and (b) the CM half-circuit for the op amp in Fig. 12.23.

The DM half-circuit in Fig. 12.24a is a cascade of two common-source amplifiers with active loads. The low-frequency DM gain is

$$
\begin{equation*}
a_{d m 0}=\frac{v_{o d}}{v_{i d}}=-g_{m 2}\left(r_{o 2} \| r_{o 4}\right) g_{m 6}\left(r_{o 6} \| r_{o 7}\right) \tag{12.72}
\end{equation*}
$$

The Miller-compensated second stage can be modeled by the circuit in Fig. 9.21 with $R_{1}=$ $r_{o 2}\left\|r_{o 4}, g_{m}=g_{m 6}, R_{2}=r_{o 6}\right\| r_{o 7}, C_{1}=C_{1 d}$, and $C_{2}=C_{2 d}$. (The input capacitance $C_{1 d}$ of the second stage and load capacitance $C_{2 d}$ of the second stage are not shown explicitly in

Fig. 12.24a.) Therefore, the poles $p_{1 d}$ and $p_{2 d}$ of the DM half-circuit are given by (9.32) and (9.33). Assume that the op amp is operating in a feedback loop, the feedback factor $f_{d m}$ for the DM feedback loop is frequency-independent, and the right-half-plane zero has been eliminated. Then to achieve $45^{\circ}$ phase margin, the magnitude of the DM loop gain should be unity at the frequency $\left|p_{2 d}\right|$. Since $\mid$ gain $\mid \times$ frequency is constant from $\left|p_{1 d}\right|$ to $\left|p_{2 d}\right|$ due to the one-pole roll-off there, we can write

$$
\begin{equation*}
\left|a_{d m 0} f_{d m} p_{1 d}\right|=1 \cdot\left|p_{2 d}\right| \tag{12.73}
\end{equation*}
$$

Substituting (12.72), (9.32), and (9.33) in (12.73) gives

$$
\begin{equation*}
\frac{g_{m 2}}{C} f_{d m} \approx \frac{g_{m 6}}{C_{2 d}} \tag{12.74}
\end{equation*}
$$

assuming that the DM load capacitance $C_{2 d}$ and the compensation capacitor $C$ are much larger than the internal node capacitance $C_{1 d}$. If the other values are known, the compensation capacitor is determined by (12.74).

The CM half-circuit is shown in Fig. 12.24b. The first stages of the CM and DM halfcircuits are different, but the second stages are identical. To focus on the CMFB loop, we will assume $v_{i c}=0$. (Nonzero $v_{i c}$ will be considered later.) In the CM half-circuit, the first stage consists of common-source $M_{5 h}$ with common-gate $M_{2}$ and active load $M_{4}$. As in Fig. $12.14 b, M_{5 h}$ is one half of $M_{5}$, with $(W / L)_{5 h}=(W / L)_{5} / 2$ and $I_{D 5 h}=I_{D 5} / 2$. The first stage is followed by the common-source second stage, $M_{6}-M_{7}$. The low-frequency CMC gain is

$$
\begin{equation*}
a_{c m c 0}=\frac{v_{o c}}{v_{c m c}} \approx g_{m 5 h}\left[\left(r_{o 2} g_{m 2} r_{o 5 h}\right) \| r_{o 4}\right] g_{m 6}\left(r_{o 6} \| r_{o 7}\right) \tag{12.75}
\end{equation*}
$$

Capacitance associated with the source of cascode $M_{1}$ introduces a pole $p_{x}$ in the CMC gain. If $\left|p_{x}\right|$ is much larger than the magnitude of the nondominant pole $\left|p_{2 c}\right|$ in (9.33) from the Millercompensated second stage, pole $p_{x}$ can be ignored, and the gain $a_{c m c}$ can be approximated as having two poles that are given by (9.32) and (9.33). These poles can be different than the poles in the DM gain for two reasons. First the output load capacitances in the DM and CM half-circuits can be different, and second the output resistances of the first stages in the half-circuits can be different. The zero due to feedforward is the same as for DM gain and can be eliminated as described in Chapter 9. To simplify the following analysis, we will assume that all poles and zeros in the CMFB loop other than the two poles associated with the Miller compensation can be ignored. To achieve $45^{\circ}$ phase margin, the magnitude of the CMFB loop gain should fall to unity at $\left|p_{2 c}\right|$. Therefore,

$$
\begin{equation*}
\left|a_{c m c 0} a_{c m s} 0 p_{1 c}\right|=1 \cdot\left|p_{2 c}\right| \tag{12.76}
\end{equation*}
$$

where $a_{c m s 0}$ is the low-frequency gain through the CM-sense circuit

$$
\begin{equation*}
a_{c m s 0}=\left.\frac{v_{c m c}}{v_{o c}}\right|_{\omega=0, \text { CMFB loop open }}=\left.\frac{v_{c m s}}{v_{o c}}\right|_{\omega=0, \text { CMFB loop open }} \tag{12.77}
\end{equation*}
$$

Substituting (12.75), (9.32), and (9.33) in (12.76) and using $R_{1} \approx r_{o 2} g_{m 2} r_{o 5 h}$ gives

$$
\begin{equation*}
\frac{g_{m 5 h}}{C}\left|a_{c m s}\right| \approx \frac{g_{m 6}}{C_{2 c}} \tag{12.78}
\end{equation*}
$$

assuming that the CM load capacitance $C_{2 c}$ and the compensation capacitor $C$ are much larger than the internal node capacitance $C_{1 c}$. The compensation capacitor required for the CMFB loop can be found from (12.78).

Ideally, the compensation capacitor values calculated in (12.74) and (12.78) would be equal, and the CMFB and DM loops would each have a phase margin of $45^{\circ}$. In practice, these values are rarely equal. If the value of $C$ is chosen to be the larger of the values given
by (12.74) and (12.78), one feedback loop will have a phase margin of $45^{\circ}$, and the other loop will have a phase margin larger than $45^{\circ}$ and will be overcompensated. A drawback of overcompensation is that the unity-gain frequency of the loop gain and the closed-loop bandwidth are smaller than they would be if the loop were optimally compensated. If the larger $C$ is required to compensate the DM feedback loop, using that compensation capacitor will overcompensate the CMFB loop. Since the CMFB ideally operates on only dc signals, reducing its bandwidth may be acceptable. (See Section 12.8 for more on this topic.) If the larger $C$ is required to compensate the CMFB feedback loop, using that compensation capacitor will overcompensate the DM loop. However, reducing the bandwidth of the DM feedback loop by overcompensation is usually undesirable because this loop operates on the DM input signal, which may have a wide bandwidth.

An alternative to using the larger $C$ value that optimally compensates the CMFB loop but overcompensates the DM loop is the following. The value of $C$ that gives a $45^{\circ}$ phase margin in the DM loop from (12.74) can be used if $g_{m 5 h}$ is scaled down to satisfy (12.78). This approach gives a $45^{\circ}$ phase margin for both feedback loops without sacrificing bandwidth in the DM loop. Scaling of $g_{m 5 h}=g_{m 5} / 2$ could be achieved by reducing $(W / L)_{5}$, but such scaling would reduce the CM input range of the op amp because decreasing $(W / L)_{5}$ increases $\left|V_{o v 5}\right|$. Another solution is to split $M_{5}$ into two parallel transistors, one that has its gate connected to a bias voltage and the other with its gate connected to CMC, as described in Section 12.4.2 and Fig. 12.15. A drawback of this approach is that reducing $g_{m 5 h}$ reduces $\left|a_{c m c 0}\right|$, as can be seen in (12.75).

Ignoring limitations imposed by the CM-sense circuit, we see that each op-amp output in Fig. 12.23 can swing until a transistor in the second stage enters the triode region. The maximum value of $V_{o 1}$ is $V_{D D}-\left|V_{o v 7}\right|$, and its minimum value is $-V_{S S}+V_{o v 6}$. Therefore, the peak differential output voltage is

$$
\begin{align*}
V_{o d(\text { peak })} & =V_{o 1(\max )}-V_{o 2(\min )}=V_{o 1(\max )}-V_{o 1(\min )}=V_{D D}-\left|V_{o v 7}\right|-\left(-V_{S S}+V_{o v 6}\right) \\
& =V_{D D}+V_{S S}-V_{o v 6}-\left|V_{o v 7}\right| \tag{12.79}
\end{align*}
$$

The CM input range of the op amp is limited in the positive direction by the tail current source, which transitions from active to triode when $\left|V_{d s}\right|=\left|V_{o v 5}\right|$; therefore, we want

$$
\begin{equation*}
V_{I C}<V_{D D}-\left|V_{G S 1}\right|-\left|V_{o v 5}\right| \tag{12.80}
\end{equation*}
$$

The lower limit of the CM input range occurs when input transistor $M_{1}$ (or $M_{2}$ ) enters the triode region, so

$$
\begin{equation*}
V_{I C}>-V_{S S}+V_{G S 6}+V_{t 1} \tag{12.81}
\end{equation*}
$$

#### EXAMPLE

Modify the single-ended two-stage op amp from the examples in Section 6.3.5 and Section 9.4.3 into a fully differential op amp. It will be used in the feedback circuit shown in Fig. 12.25, which represents the connections in a switched-capacitor circuit when one clock is high (assuming the switches are ideal). The capacitor values are $C_{S}=2 \mathrm{pF}, C_{F}=5 \mathrm{pF}$, and $C_{L}=2 \mathrm{pF}$. Design for 1-V peak output swing and phase margins of $45^{\circ}$ or greater in the DM and CMFB loops. Use $V_{D D}=V_{S S}=1.65 \mathrm{~V}$, and design for a CM output voltage of 0 V .

First, we will design the devices to satisfy the bias and low-frequency requirements. Then we will compensate the amplifier. Using the device sizes and bias currents from the example in Section 6.3.5, we have

$$
\begin{gathered}
(W / L)_{1}=(W / L)_{2}=77 \quad(W / L)_{3}=(W / L)_{4}=4 \quad(W / L)_{5}=25 \\
(W / L)_{6}=(W / L)_{9}=16 \quad(W / L)_{7}=(W / L)_{10}=50
\end{gathered}
$$

image_name:Figure 12.25
description:
[
name: Vs1, type: VoltageSource, value: Vs1, ports: {Np: Vs1, Nn: GND}
name: Vs2, type: VoltageSource, value: Vs2, ports: {Np: Vs2, Nn: GND}
name: Cs, type: Capacitor, value: Cs, ports: {Np: Vs1, Nn: Vi1}
name: Cs, type: Capacitor, value: Cs, ports: {Np: Vs2, Nn: Vi2}
name: Cf, type: Capacitor, value: Cf, ports: {Np: Vi1, Nn: Vo1}
name: Cf, type: Capacitor, value: Cf, ports: {Np: Vi2, Nn: Vo2}
name: Cl, type: Capacitor, value: Cl, ports: {Np: Vo1, Nn: GND}
name: Cl, type: Capacitor, value: Cl, ports: {Np: Vo2, Nn: GND}
name: A0, type: OpAmp, value: A0, ports: {InP: Vi2, InN: Vi1, OutP: Vo2, OutN: Vo1}
]
extrainfo:The circuit is a fully differential operational amplifier with capacitive load and feedback. It uses two voltage sources (Vs1 and Vs2) to provide input signals, and includes capacitors Cs for coupling, Cf for feedback, and Cl for load. The op-amp A0 processes differential input signals with outputs Vo1 and Vo2.

Figure 12.25 A fully differential op amp with capacitive load and feedback.
with $L_{\mathrm{drwn}}=1 \mu \mathrm{~m},\left|I_{D 1}\right|=\left|I_{D 2}\right|=100 \mu \mathrm{~A}$, and $I_{D 6}=400 \mu \mathrm{~A}$. In that example, these values gave a calculated dc gain of $a_{d m 0}=-7500$ and a simulated gain of $a_{d m 0}=-6200$.

For CMFB, we will use two differential pairs as shown in Fig. 12.26. Since the input stage in Fig. 12.23 is the complement of the op amp in Fig. 12.2, the CMFB circuit in Fig. 12.26 is the complement of the circuit in Fig. 12.19 to allow control of the op-amp tail current $I_{D 5}$ through a current mirror formed by $M_{5}$ and $M_{25}$. Also, the CM-sense output $V_{c m s}$ is taken from the drains of $M_{21}$ and $M_{24}$, which makes the gain $a_{c m s}$ negative. This inversion is needed here to give negative feedback in the CMFB loop because the CMC gain $a_{c m c}$ is positive at low frequencies in this two-stage op amp. We choose $M_{25}$ to be matched to $M_{5}$, so they form a unity-gain current mirror. Since the desired tail current is $\left|I_{D 5}\right|=200 \mu \mathrm{~A}$, we want

$$
\left|I_{D 25}\right|=I_{D 26}=I_{D 27}=200 \mu \mathrm{~A}
$$

Therefore, each transistor $M_{21}-M_{24}$ nominally carries $100 \mu \mathrm{~A}$ of drain current. These transistors must remain active over the entire range of the op-amp output swing. For a differential
image_name:Figure 12.26 A fully differential two-stage CMOS op amp using the CMFB scheme from Fig. 12.19.
description:This is a fully differential two-stage CMOS operational amplifier using a common-mode feedback (CMFB) scheme. The circuit consists of two main sections: the op-amp section and the CM sense section. The op-amp section includes differential input pairs and current mirrors for amplification, while the CM sense section manages the common-mode voltage. The circuit is designed to keep transistors active throughout the op-amp output swing.

Figure 12.26 A fully differential two-stage CMOS op amp using the CMFB scheme from Fig. 12.19.
output voltage of 1 V peak, each op-amp output $\left(V_{o 1}\right.$ or $\left.V_{o 2}\right)$ must swing $\pm 0.5$ V. From (3.161), the transistors in a differential pair remain active as long as the magnitude of the differential input voltage is less than $\sqrt{2} V_{o v}$. Therefore, we want

$$
\sqrt{2} V_{o v}=0.5 \mathrm{~V}
$$

or $V_{o v}=0.35 \mathrm{~V}$ for $M_{21}-M_{24}$. From (1.157), we get

$$
\left(\frac{W}{L}\right)_{21}=\left(\frac{W}{L}\right)_{22}=\left(\frac{W}{L}\right)_{23}=\left(\frac{W}{L}\right)_{24}=\frac{2 I_{D 21}}{k_{n}^{\prime}\left(V_{o v 21}\right)^{2}}=\frac{2(100)}{(194)(0.35)^{2}}=8.4
$$

The only remaining device sizes to be determined are for matched transistors $M_{26}$ and $M_{27}$. Each device acts as a current source carrying $200 \mu \mathrm{~A}$. For those transistors to act as current sources, they should always be active. Focusing on $M_{26}$, we want $V_{o v 26}<V_{d s 26(\mathrm{~min})}$. To determine $V_{d s 26(\min )}$, consider an extreme case when $M_{21}$ just turns off as $V_{o 1}$ swings down to its lowest value. In this case, $M_{22}$ carries $200 \mu \mathrm{~A}$, and

$$
V_{g s 22(\max )}=V_{t 22}+\sqrt{\frac{2 I_{D 22(\max )}}{k_{n}^{\prime}(W / L)_{22}}}=V_{t 22}+\sqrt{\frac{2(200)}{194(8.4)}}=V_{t 22}+0.5 \mathrm{~V}
$$

The gate voltage of $M_{22}$ is $V_{C M}=0$. Therefore, the minimum source-body voltage for $M_{22}$, which is the minimum drain-source voltage of $M_{26}$, is

$$
\begin{align*}
V_{s b 22(\min )} & =V_{d s 26(\min )}=V_{s 22(\min )}-\left(-V_{S S}\right)=V_{C M}-V_{g s 22(\max )}+V_{S S} \\
& =0-\left(0.5+V_{t 22}\right)+1.65=1.15-V_{t 22} \tag{12.82}
\end{align*}
$$

Since $V_{s b 22}$ is not zero, the threshold voltage of $M_{22}$ is given by (1.140) as

$$
\begin{equation*}
V_{t 22}=V_{t n 0}+\gamma\left[\sqrt{V_{s b 22}+2 \phi_{f}}-\sqrt{2 \phi_{f}}\right] \tag{12.83}
\end{equation*}
$$

Using the data in Table 2.4, (1.141), and (2.28), we calculate $\left|\phi_{f}\right|=0.33 \mathrm{~V}$ and $\gamma=0.28 \mathrm{~V}^{1 / 2}$ [assuming $V_{s b 22}$ is small and using $N_{A}+N_{s i}$ as the effective substrate doping in (1.141)]. Solving (12.82) and (12.83) gives $V_{t 22}=0.67 \mathrm{~V}, V_{s 22(\min )}=-1.17 \mathrm{~V}$, and

$$
V_{s b 22(\min )}=V_{d s 26(\min )}=1.15-V_{t 22}=1.15-0.67=0.48 \mathrm{~V}
$$

If we chose $V_{\text {ov } 26}=0.38 \mathrm{~V}$ (to allow for a -0.1 V shift in $V_{C M}$ ), then

$$
\left(\frac{W}{L}\right)_{26}=\frac{2 I_{D 26}}{k_{n}^{\prime}\left(V_{o v 26}\right)^{2}}=\frac{2(200)}{(194)(0.38)^{2}} \approx 14
$$

Also, $(W / L)_{27}=14$ since $M_{26}$ and $M_{27}$ are matched.
In the example in Section 9.4.3, a compensation capacitor of 3.2 pF provided a $45^{\circ}$ phase margin for a feedback factor of unity and a $5-\mathrm{pF}$ load. The DM half-circuits for this example with the independent voltage sources $V_{s 1}$ and $V_{s 2}$ set to zero are shown in Fig. 12.27a. Here, we have assumed that $C_{L}$ is much larger than the input capacitance of the CM-sense devices $M_{21}-M_{24}$. The two feedback networks connect between the two half-circuits in this negative feedback circuit. The feedback factor is less than one because it is set by the capacitive divider formed by $C_{F}$ and $C_{S}$. Also, the feedback networks affect the capacitive loading at the outputs. The upper DM half-circuit in Fig. 12.27a is redrawn in Fig. $12.27 b$ with the feedback loop broken. Here, capacitor $C_{i d h}$ is the capacitance looking into the gate of $M_{1}$ in the DM halfcircuit, which is the same as the capacitance looking into the gate of $M_{2}$. Looking into the gate of $M_{2}$, we see $C_{g s 2}$ and overlap capacitance $C_{g d 2}$ increased by the Miller effect as in (7.5);
image_name:(a)
description:This is a differential amplifier circuit with feedback capacitors (C_F) and load capacitors (C_L). The circuit employs PMOS transistors (M1, M2) for input stages and NMOS transistors (M6, M9) for output stages. Resistors (r_o3, r_o4, r_o7, r_o10) are used for load and biasing purposes. The input differential voltage is applied across the gates of M1 and M2, and the output differential voltage is taken across the load capacitors. Feedback is provided through the capacitor C_F, influencing the stability and frequency response of the amplifier.
image_name:(b)
description:
[
name: Cs, type: Capacitor, value: Cs, ports: {Np: X1, Nn: GND}
name: CF, type: Capacitor, value: CF, ports: {Np: X1, Nn: Vod/2}
name: CL, type: Capacitor, value: CL, ports: {Np: Vod/2, Nn: GND}
name: Cidh, type: Capacitor, value: Cidh, ports: {Np: X1, Nn: GND}
name: M2, type: PMOS, ports: {S: GND, D: d2g6, G: -Vid/2}
name: M6, type: NMOS, ports: {S: GND, D: Vod/2, G: d2g6}
name: ro4, type: Resistor, value: ro4, ports: {N1: d2g6, N2: GND}
name: ro7, type: Resistor, value: ro7, ports: {N1: Vod/2, N2: GND}
name: C, type: Capacitor, value: C, ports: {Np: d2g, Nn: Vod/2}
]
extrainfo:The circuit is a differential amplifier with feedback, including PMOS and NMOS transistors. Capacitors Cs and Cidh are used for input coupling and feedback. Resistors ro4 and ro7 provide load and biasing.

Figure 12.27 (a) The DM half-circuits for Figs. 12.25 and 12.26. (b) The upper DM half-circuit in (a) with the feedback loop broken.
therefore,

$$
\begin{aligned}
C_{i d h} & =C_{g s 2}+C_{g d 2}\left(1-a_{d m 1}\right) \approx \frac{2}{3} C_{o x} W_{2} L_{2}+C_{o l} W_{2}\left(1-a_{d m 1}\right) \\
& =\frac{2}{3}\left(4.43 \frac{\mathrm{fF}}{\mu \mathrm{~m}^{2}}\right)(77 \mu \mathrm{~m})(0.82 \mu \mathrm{~m})+\left(0.35 \frac{\mathrm{fF}}{\mu \mathrm{~m}}\right)(77 \mu \mathrm{~m})(1+137)=3.9 \mathrm{pF}
\end{aligned}
$$

Here, we used $L_{2}=1 \mu \mathrm{~m}-2 L_{d}=0.82 \mu \mathrm{~m}$ and $a_{d m 1}=-g_{m 2}\left(r_{o 2} \| r_{o 4}\right)=-137$ for the low-frequency gain of the first stage. These values follow from the example in Section 6.3.5.

The total capacitive load from the output to ground in the DM half-circuit is

$$
\begin{equation*}
C_{2 d}=C_{L}+\frac{C_{F}\left(C_{S}+C_{i d h}\right)}{C_{F}+C_{S}+C_{i d h}}=2+\frac{5(2+3.9)}{5+2+3.9}=4.7 \mathrm{pF} \tag{12.84}
\end{equation*}
$$

Here, we have assumed that $C_{L}$ is much larger than the junction capacitance and other parasitic capacitances at the op-amp output. The DM feedback factor is

$$
\begin{equation*}
f_{d m}=\left.\frac{v_{f b} / 2}{v_{o d} / 2}\right|_{\text {loop broken }}=\frac{C_{F}}{C_{F}+C_{S}+C_{i d h}}=\frac{5}{5+2+3.9}=0.459 \tag{12.85}
\end{equation*}
$$

Substituting (12.84), (12.85), and values for $g_{m 2}=g_{m 1}$ and $g_{m 6}$ from the example in Section 9.4.3 into (12.74), we have

$$
\begin{equation*}
C \approx \frac{g_{m 2}}{g_{m 6}} C_{2 d} f_{d m}=\frac{1.0}{1.55}(4.7 \mathrm{pF})(0.459)=1.39 \mathrm{pF} \tag{12.86}
\end{equation*}
$$

This compensation capacitor gives a $45^{\circ}$ phase margin in the DM half-circuit (ignoring the right-half-plane zero).

The CM half-circuits are shown in Fig. $12.28 a$ with the source voltages $V_{s 1}$ and $V_{s 2}$ set to zero. Only the upper CM half-circuit is shown in detail. The capacitive feedback networks connect between the two CM half-circuits. A simplified drawing of the upper CM half-circuit is shown in Fig. 12.28b. The key simplification here is that capacitor $C_{F}$, which was connected to the input of the lower CM half-circuit (which is the gate of $M_{1}$ ) in Fig. 12.28a, now connects to the gate of $M_{2}$. This change does not affect the CM analysis because the elements and signals in the two CM half-circuits are identical.

In the CM half-circuit in Fig. 12.28b, there are two feedback loops. One loop is the CMFB loop that includes the CM-sense block. We will refer to this loop as loop \#1. This loop is a negative feedback loop, since there are three inverting stages in the loop: actively loaded common-source stages $M_{5 h}$ and $M_{6}$, and the inverting CM-sense circuit. The magnitude of the low-frequency gain in this loop is large because each common-source stage provides significant voltage gain. The other feedback loop goes through the op amp from $v_{i c}$ to $v_{o c}$ and then back from $v_{o c}$ to the input $v_{i c}$ through the capacitive divider formed by $C_{F}$ and $C_{S}$, and it will be called loop \#2. Here, loop \#2 is a positive feedback loop because it contains two inverting gain stages. This feedback loop is stable, however, because the loop gain in loop \#2, which is the product of the forward gain $a_{c m}^{\prime}$ and the feedback factor through the capacitive divider, has a magnitude that is less than one at all frequencies. The forward gain $a_{c m}^{\prime}$ in this loop, which is $a_{c m}^{\prime}=v_{o c} / v_{i c}$ with the CMFB (loop \#1) active, has a magnitude that is less than unity due to the presence of the CMFB loop (loop\#1), which works to force $v_{o c} \approx 0$. (See Problem 12.27.) To explain this low gain, first consider the CM half-circuit with loop \#1 disabled. In this case, if $v_{i c}$ is nonzero, $I_{d 2}$ changes, which changes $V_{g s 6}$ and produces a nonzero $v_{o c}$. When the CMFB loop \#1 is enabled, this loop senses any nonzero $v_{o c}$ and adjusts $V_{c m c}$ to produce a change in $I_{d 5}$ that counteracts the change in $I_{d 2}$ to give $v_{o c} \approx 0$.

The magnitude responses of the loop gains for these two loops are plotted in Fig. 12.29, ignoring any zeros and poles other than the dominant and nondominant poles, $p_{1 c}$ and $p_{2 c}$, associated with the Miller-compensated gain stage in Fig. 12.28b. Here, loop \#1 is assumed to be compensated so that its unity-gain frequency is equal to $\left|p_{2 c}\right|$, which gives a $45^{\circ}$ phase margin. Since loop \#2 is stable, we need only focus on the stability and compensation of the high-gain CMFB loop (loop \#1).

This CMFB loop is shown in Fig. 12.28c. Here, the lumped load capacitance $C_{2 c}$ includes the output loading due to $C_{L}$ and the capacitive feedback network, including the capacitance $C_{i c h}$ looking into the gate of $M_{2}$ in Fig. 12.28b. This capacitance is smaller than $C_{i d h}$ because $M_{2}$ has a large source degeneration resistance $\left(r_{o 5 h}\right)$ that provides local CM feedback. This
image_name:(a)
description:The circuit diagram (a) represents the CM half-circuit for common-mode feedback (CMFB) sensing. It includes PMOS transistors M5h, M2, and M6, capacitors CS, CF, C, and CL, and resistors ro4 and ro7. This setup is used to stabilize and compensate the high-gain CMFB loop, with Loop #1 and Loop #2 depicted in diagram (b). The circuit is designed to enhance impedance and reduce capacitance at specific nodes, particularly at the gate of M2, to improve feedback performance.
image_name:(b)
description:The circuit diagram (b) represents a CMFB loop with emphasis on stability and compensation. Two feedback loops, Loop #1 and Loop #2, are indicated. The circuit involves capacitive feedback and load components, and uses NMOS transistors for common-mode feedback sensing.
Figure 12.28 (a) The CM half-circuits for Figs. 12.25 and 12.26. (b) The upper CM half-circuit in (a) simplified.
feedback increases the impedance (decreases the capacitance) looking into the gate of $M_{2}$. Also, this feedback reduces the magnitude of the voltage gain from the gate to the drain of $M_{2}$, which decreases the Miller input capacitance due to $C_{g d 2}$. Therefore, assuming $C_{i c h} \ll C_{S}$, we find

$$
C_{2 c}=C_{L}+\frac{C_{F}\left(C_{S}+C_{i c h}\right)}{C_{F}+C_{S}+C_{i c h}} \approx C_{L}+\frac{C_{F} C_{S}}{C_{F}+C_{S}}=2+\frac{5(2)}{5+2}=3.43 \mathrm{pF}
$$

image_name:Figure 12.28 (c)
description:
[
name: M5h, type: PMOS, ports: {S: vcmc, D: d3hS2, G: GND}
name: M2, type: PMOS, ports: {S: d3hS2, D: d2b6, G: Vic}
name: M6, type: NMOS, ports: {S: GND, D: Voc, G: d2g6}
name: r_o4, type: Resistor, value: r_o4, ports: {N1: GND, N2: d2b6}
name: r_o7, type: Resistor, value: r_o7, ports: {N1: Voc, N2: voc}
name: C, type: Capacitor, value: C, ports: {Np: d2b6, Nn: d2g6}
name: C_2c, type: Capacitor, value: C_2c, ports: {Np: Voc, Nn: GND}
]
extrainfo:The circuit is a common-mode feedback (CMFB) loop focusing on improving the impedance and reducing capacitance at the gate of M2. The PMOS transistor M5h is used to control the common-mode voltage, while M6 acts as an NMOS load. The resistors and capacitors are used to stabilize and control the feedback loop.

Figure 12.28 (c) The CM half-circuit in (b), focusing on the CMFB loop (loop \#1).
image_name:Figure 12.29
description:The graph in Figure 12.29 is a Bode plot showing the loop gains for two feedback loops in the common-mode (CM) half-circuit. The plot is divided into two main sections: one for the common-mode feedback loop (|T_CMFB| = |T_loop1|) and another for the second loop (|T_loop2|).

1. **Type of Graph and Function:**
- This is a Bode plot, which displays the magnitude of the transfer function in decibels (dB) against frequency (ω).

2. **Axes Labels and Units:**
- The vertical axis is labeled |T| (dB), representing the magnitude of the transfer function in decibels.
- The horizontal axis is labeled ω, representing frequency. The specific unit is not provided, but it is typically in radians per second for such analyses.

3. **Overall Behavior and Trends:**
- The graph shows a piecewise linear representation of the loop gains.
- For |T_CMFB| = |T_loop1|, the gain remains constant initially, then begins to decrease linearly with frequency, indicating a roll-off.
- For |T_loop2|, the gain is lower and also decreases linearly, but with a different slope.

4. **Key Features and Technical Details:**
- There are two significant points marked on the frequency axis: |p1| and |p2|. These likely represent pole frequencies where the gain starts to decrease more sharply.
- The initial gain for |T_CMFB| = |T_loop1| is higher than for |T_loop2|.
- The plot indicates a typical behavior of feedback systems where the gain decreases with increasing frequency, aiding in stability analysis.

5. **Annotations and Specific Data Points:**
- The graph highlights two specific loop gains: |T_CMFB| = |T_loop1| and |T_loop2|.
- The points |p1| and |p2| are critical as they likely denote frequencies where phase changes significantly, impacting stability and performance.

This Bode plot is crucial for analyzing the stability and performance of the common-mode feedback loop in the CM half-circuit, providing insights into how the system behaves at different frequencies.

Figure 12.29 Plots of the loop gains for the two feedback loops in the CM half-circuit in Fig. 12.28b.

Here, we also assumed that $C_{L}$ is much larger than the input capacitance of the CM-sense half-circuit. To use (12.78) to calculate the compensation capacitor that gives a $45^{\circ}$ phase margin in the CMFB loop, we must find the dc small-signal gain through the CM-sense circuit. In Fig. 12.26, $I_{c m s}$ flows through diode-connected $M_{25}$; therefore,

$$
\begin{equation*}
v_{c m c}=-\frac{i_{c m s}}{g_{m 25}} \tag{12.87}
\end{equation*}
$$

if $r_{o 25} \gg 1 / g_{m 25}$. A small-signal version of (12.56) is $i_{c m s}=g_{m 22} v_{o c}=g_{m 21} v_{o c}$. Using this expression and (12.87), the gain $a_{c m s}$ at low frequency is

$$
\begin{align*}
\left|a_{c m s 0}\right| & =\left.\frac{\left|v_{c m c}\right|}{\left|v_{o c}\right|}\right|_{\text {CMFB loop open }}=\frac{\left|v_{c m c}\right|}{\left|i_{c m s}\right|}\left|\frac{\left|i_{c m s}\right|}{\left|v_{o c}\right|}\right|_{\text {CMFB loop open }} \\
& =\frac{g_{m 21}}{g_{m 25}}=\frac{\frac{2 I_{D 21}}{V_{o v 21}}}{\frac{2\left|I_{D 25}\right|}{\left|V_{o v 25}\right|}}=\frac{\frac{2(100)}{0.35}}{\frac{2(200)}{0.5}}=0.71 \tag{12.88}
\end{align*}
$$

Solving (12.78) for a $45^{\circ}$ phase margin in the CMFB loop, using (12.88) and the value of $g_{m 6}$ from the example in Section 9.4.3, gives

$$
\begin{align*}
C & =\frac{g_{m 5 h}}{g_{m 6}}\left|a_{c m s 0}\right| C_{2 c}=\frac{\left(g_{m 5} / 2\right)}{g_{m 6}}\left|a_{c m s 0}\right| C_{2 c} \\
& =\frac{\frac{2(200 \mu \mathrm{HA})}{0.5 \mathrm{~V}} \frac{1}{2}}{1.55 \mathrm{~mA} / \mathrm{V}}(0.71)(3.43 \mathrm{pF})=0.63 \mathrm{pF} \tag{12.89}
\end{align*}
$$

From (12.86) and (12.89), a larger compensation capacitor is required to compensate the DM loop than the CMFB loop. Therefore, using $C=1.39 \mathrm{pF}$ will give phase margins of $45^{\circ}$ for the DM feedback loop and greater than $45^{\circ}$ for the CMFB loop, which is acceptable.

To verify this design, SPICE simulations of this op amp were carried out with $C=1.39 \mathrm{pF}$ in series with $R_{Z}=758 \Omega$, which was found to eliminate the right-half-plane zero in the example in Section 9.4.3. The SPICE models are based on the data in Table 2.4. The phase margins of the DM and CMFB loops were simulated using techniques developed for fully differential circuits. ${ }^{11}$ The DM feedback loop has a simulated phase margin of $43^{\circ}$ and unitygain frequency of 53 MHz . The CMFB loop has a simulated phase margin of $62^{\circ}$ and unity-gain frequency of 24 MHz . Thus, the CMFB loop is overcompensated. Changing the compensation capacitor to 0.63 pF , which is the value calculated from (12.89) to give a $45^{\circ}$ phase margin in the CMFB loop, we find the simulated phase margin of the CMFB loop changes to $41^{\circ}$, but the DM phase margin drops to an unacceptably low $29^{\circ}$. These simulation results verify that the formulas in this section give a reasonable estimate for the compensation capacitor.

In the previous example, the op-amp output swing is limited by the linear input range of the CMFB circuit. The output swing could be increased by using either a switched-capacitor or resistive-divider CM detector.

An alternative CMFB approach for the op amp in Fig. 12.23 is to connect the gate of $M_{5}$ to a dc bias voltage and to use the gates of $M_{3}-M_{4}$ as the CMC input. In this case, the first gain stage of the CM half-circuit in Fig. $12.28 c$ consists of common-source $M_{4}$ with a cascoded active load. Also, the pole associated with the capacitance at the source of $M_{2}$ is not in the signal path of the CMFB loop.

### 12.6.2 Fully Differential Telescopic Cascode Op Amp

A fully differential cascode op amp is shown in Fig. 12.30. Compared to its single-ended complementary counterpart, which is the first stage in Fig. 6.25, the main difference is that diode connections are removed from transistors $M_{3}$ and $M_{3 A}$. Also, the gates of cascode transistors $M_{1 A}-M_{4 A}$ are connected to bias voltages here. The op-amp outputs are taken from the drains of $M_{1 A}$ and $M_{2 A}$. The resulting circuit is symmetric with each output loaded by a cascoded current source. An advantage of the topology in Fig. 12.30 is that the DM signal path consists only of $n$-channel transistors. That is, only the $n$-channel transistors conduct timevarying currents. The $p$-channel transistors conduct constant currents. Such a configuration maximizes the op-amp speed because $n$-channel transistors have higher mobility and $f_{T}$ than their $p$-channel counterparts (if the channel lengths and overdrive voltages are the same). One CMFB approach is to set the currents through $M_{3}-M_{4}$ by connecting their gates to a dc bias voltage (set by a diode-connected transistor that is the input of a current mirror) and use the gate of $M_{5}$ as the CMC input. In this case, the magnitude of the low-frequency CMC gain $\left|a_{c m c 0}\right|$ can be large since $M_{1}-M_{2}$ and $M_{1 A}-M_{2 A}$ provide two levels of NMOS cascoding, and $M_{3 A}-M_{4 A}$ provide one level of PMOS cascoding. This cascoding increases the output resistance, but the two levels of NMOS cascoding introduce high-frequency poles in $a_{c m c}(s)$.
image_name:Figure 12.30 A fully differential CMOS telescopic-cascode op amp.
description:
[
name: M1, type: NMOS, ports: {S: s1s2d5, D: d1s1A, G: Vi1}
name: M2, type: NMOS, ports: {S: s1s2d5, D: d2s2A, G: Vi2}
name: M3, type: PMOS, ports: {S: VDD, D: d3s3A, G: Vbias}
name: M4, type: PMOS, ports: {S: VDD, D: d4s4A, G: Vbias}
name: M5, type: NMOS, ports: {S: -Vss, D: s1s2d5, G: Vcmc}
name: M1A, type: NMOS, ports: {S: d1s1A, D: Vo1, G: VBB2}
name: M2A, type: NMOS, ports: {S: d2s2A, D: Vo2, G: VBB2}
name: M3A, type: PMOS, ports: {S: d3s3A, D: Vo1, G: VBB1}
name: M4A, type: PMOS, ports: {S: d4s4A, D: Vo2, G: VBB1}
name: VBB1, type: VoltageSource, value: VBB1, ports: {Np: VBB1, Nn: GND}
name: VBB2, type: VoltageSource, value: VBB2, ports: {Np: VBB2, Nn: GND}
]
extrainfo:The circuit is a fully differential CMOS telescopic-cascode operational amplifier. It uses NMOS and PMOS transistors to achieve high gain and bandwidth. The design features multiple levels of cascoding to enhance output resistance and reduce power consumption. The output nodes are Vo1 and Vo2, and the circuit is powered by VDD and VSS. Biasing is provided by VBB1 and VBB2.
Figure 12.30 A fully differential CMOS telescopic-cascode op amp.

An alternative CMFB approach is to set the current through $M_{5}$ by connecting its gate to a dc bias voltage and use the gates of $M_{3}$ and $M_{4}$ as the CMC input. This approach has one level of cascoding in the CMC gain path, which introduces one high-frequency pole in $a_{c m c}(s)$. Here, however, the amplifying devices in the CMFB loop are $p$-channel $M_{3}$ and $M_{4}$, which have lower mobility and $f_{T}$ than $n$-channel $M_{5}$ if they have the same channel lengths and overdrive voltages.

The DM and CMFB feedback loops are compensated by the load capacitances at the opamp outputs. The phase margin of the CMFB loop can be changed without changing the load capacitance, by splitting the transistor(s) that connect to the CMC input into parallel transistors, as described in Section 12.4.2 and shown in Fig. 12.15.

### 12.6.3 Fully Differential Folded-Cascode Op Amp

A fully differential folded-cascode op amp is shown in Fig. 12.31. Compared to its single-ended counterpart shown in Fig. 6.28, the main difference is that the diode connections on $M_{3}$ and $M_{3 A}$ have been eliminated. The resulting circuit is symmetric, and the outputs are taken from the drains of $M_{1 A}$ and $M_{2 A}$.

To satisfy KCL, the sum of the currents flowing through $M_{3}, M_{4}$, and $M_{5}$ must equal the sum of the drain currents flowing through $M_{11}$ and $M_{12}$. To satisfy KCL with all transistors active and to accurately set $V_{o c}$, CMFB is used. The CMC input could be taken as the gate of $M_{5}$, the gates of $M_{3}-M_{4}$, or the gates of $M_{11}-M_{12}$, which is shown in Fig. 12.31. With this last option, the CMFB loop contains less nodes than the other two cases, and the gain $a_{c m c}$ is provided by common-source $n$-channel transistor $M_{11}$ (or $M_{12}$ ), which has a larger $g_{m}$ than $p$-channel $M_{3}\left(\right.$ or $\left.M_{4}\right)$ if $(W / L)_{11} \approx(W / L)_{3}$ because $k_{n}^{\prime}>k_{p}^{\prime}$ and $I_{D 11}>\left|I_{D 3}\right|$.

The DM and CMFB feedback loops are compensated by the capacitances at the op-amp outputs.

The folded-cascode op amp with active cascodes that is shown in Fig. 6.30 can also be converted to a fully differential op amp. ${ }^{12}$ As for the folded-cascode op amp, there are three choices for the CMC input.
image_name:Figure 12.31
description:This is a fully differential CMOS folded-cascode operational amplifier with active cascodes. It features two differential input stages and is designed for high input impedance applications. The circuit includes bias voltages Vb1, Vb2, VBB3, and VBB4 for controlling various transistors.

Figure 12.31 A fully differential CMOS folded-cascode op amp.

### 12.6.4 A Differential Op Amp with Two Differential Input Stages

The fully differential op amps presented above have two input terminals that accept one differential input. Those op amps can be used in the amplifier, integrator, and differentiator shown in Fig. 12.32. To implement a fully differential non-inverting gain stage with a very large input impedance, an op amp with four input terminals is needed. Two inputs connect to the feedback networks and the other two inputs connect to the differential signal source, as shown in Fig. 12.33. Assuming the magnitudes of the op amp gains from $v_{i d 1}$ and $v_{i d 2}$ to $v_{o d}$ are large, negative feedback forces $v_{i d 1} \approx 0$ and $v_{i d 2} \approx 0$. The two pairs of inputs are produced by two source-coupled pairs, as shown for a two-stage op amp in Fig. 12.34. The two source-coupled pairs, $M_{1}-M_{2}$ and $M_{1 X}-M_{2 X}$, share a pair of current-source loads. Assuming the input pairs are matched, the differential small-signal voltage gain is the same from either input; therefore,

$$
\begin{equation*}
v_{o d}=a_{d m}\left(v_{i d 1}+v_{i d 2}\right) \tag{12.90}
\end{equation*}
$$

The CM input range for the op amp must be large enough to include the full range of the input signals, $V_{s 1}$ and $V_{s 2}$, because they connect directly to op-amp inputs. In this op amp, the CMFB loop could adjust either $I_{1}$ or $I_{2}$ by controlling the gate voltages of the transistors that generate those currents.

### 12.6.5 Neutralization

In a fully differential op amp, a technique referred to as capacitive neutralization can be used to reduce the component of the op-amp input capacitance due to the Miller effect (see Chapter 7). Reducing the input capacitance increases the input impedance, which is desirable. Neutralization is illustrated in Fig. 12.35a. The gate-to-drain overlap capacitances are shown explicitly for $M_{1}$ and $M_{2}$. First, ignore the neutralization capacitors $C_{n}$. Then the DM capacitance looking into either op-amp input (with respect to ground) is

$$
\begin{equation*}
C_{i d h}=C_{g s 1}+C_{g d 1}\left(1-a_{d m 1}\right) \tag{12.91}
\end{equation*}
$$

image_name:(a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vsd+, N2: InP(Ao)}
name: R2, type: Resistor, value: R2, ports: {N1: Vsd-, N2: InN(Ao)}
name: R3, type: Resistor, value: R3, ports: {N1: InP(Ao), N2: Vop}
name: R4, type: Resistor, value: R4, ports: {N1: InN(Ao), N2: Von}
name: Ao, type: OpAmp, value: Ao, ports: {InP: InP(Ao), InN: InN(Ao), OutP: Vop, OutN: Von}
]
extrainfo:The circuit diagram (a) represents a fully differential inverting gain stage using an operational amplifier. It uses resistors R1 and R2 for the input differential pair and resistors R3 and R4 for feedback. The op-amp Ao has differential inputs and outputs, with Vop and Von as the output nodes. The input voltage is labeled as Vsd.
image_name:(b)
description:
[
name: R, type: Resistor, value: R, ports: {N1: Vsd+, N2: InN(A0)}
name: R, type: Resistor, value: R, ports: {N1: Vsd-, N2: InP(A0)}
name: A0, type: OpAmp, value: A0, ports: {InP: InP(A0), InN: InN(A0), OutP: Vop, OutN: Von}
name: C, type: Capacitor, value: C, ports: {Np: InN(A0), Nn: Vop}
name: C, type: Capacitor, value: C, ports: {Np: InP(A0), Nn: Von}
]
extrainfo:This is a noninverting fully differential feedback amplifier with capacitive feedback. It uses two identical resistors at the input and two identical capacitors in the feedback path.
image_name:(c)
description:
[
name: C1, type: Capacitor, value: C, ports: {Np: Vsd+, Nn: InN(A0)}
name: C2, type: Capacitor, value: C, ports: {Np: Vsd-, Nn: InP(A0)}
name: R1, type: Resistor, value: R, ports: {N1: InN(A0), N2: Vop}
name: R2, type: Resistor, value: R, ports: {N1: InP(A0), N2: Von}
name: A0, type: OpAmp, value: A0, ports: {InP: InP(A0), InN: InN(A0), OutP: Vop, OutN: Von}
]
extrainfo:The circuit is a differentiator configuration using an op-amp with capacitors at the input and resistors in the feedback loop. It processes the differential input voltage Vsd and outputs a differential output voltage Vod.
Figure 12.32 Fully differential
(a) inverting gain stage, (b) integrator, and (c) differentiator.

image_name:Figure 12.33(a)
description:The circuit is a fully differential amplifier using an op-amp. It processes two differential input voltages, Vid1 and Vid2, and produces a differential output voltage, Vod.

image_name:Figure 12.33 (b)
description:
[
name: RA1, type: Resistor, value: RA, ports: {N1: VCM, N2: X1}
name: RB1, type: Resistor, value: RB, ports: {N1: X1, N2: Vop}
name: RA2, type: Resistor, value: RA, ports: {N1: VCM, N2: X2}
name: RB2, type: Resistor, value: RB, ports: {N1: X2, N2: Von}
name: A0, type: OpAmp, value: A0, ports: {InP: Vs1, InN: Vs2, OutP: Vop, OutN: Von}
]
extrainfo:The circuit is a fully differential inverting gain stage using an op-amp. It amplifies the differential input voltage Vsd and produces a differential output voltage Vod. The gain of the amplifier is determined by the ratio of RB to RA, as shown in the equation Vod/Vsd = 1 + RB/RA.
Figure 12.33 (a) An op amp with two pairs of inputs. (b) A noninverting fully differential feedback amplifier.
image_name:Figure 12.34
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: s1s2, G: Vip1}
name: M2, type: PMOS, ports: {S: VDD, D: s1s2, G: Vin1}
name: M1X, type: PMOS, ports: {S: VDD, D: s1xs2x, G: Vip2}
name: M2X, type: PMOS, ports: {S: VDD, D: s1xs2x, G: Vin2}
name: M9, type: NMOS, ports: {S: VSS, D: Vo2, G: d1d2x99}
name: M6, type: NMOS, ports: {S: VSS, D: Vo1, G: d2d2x96}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: s1s2}
name: I2, type: CurrentSource, value: I2, ports: {Np: d1d2x99, Nn: VSS}
name: I3, type: CurrentSource, value: I3, ports: {Np: VDD, Nn: Vo2}
name: CC, type: Capacitor, value: CC, ports: {Np: Vo2, Nn: d1d2x99}
name: RZ, type: Resistor, value: RZ, ports: {N1: d1d2x99, N2: x1}
name: CC, type: Capacitor, value: CC, ports: {Np: Vo1, Nn: d2d2x96}
name: RZ, type: Resistor, value: RZ, ports: {N1: d2d2x96, N2: x2}
]
extrainfo:The circuit is a two-stage op-amp with differential inputs and outputs. It uses PMOS transistors M1, M2, M1X, and M2X for the input stage and NMOS transistors M9 and M6 for the output stage. The design includes capacitive compensation with capacitors CC and resistors RZ for stability. The current sources I1, I2, and I3 provide biasing to the circuit. The inputs are differential (Vip1, Vin1, Vip2, Vin2), and the outputs are also differential (Vo1, Vo2). The circuit is powered by VDD and VSS.

Figure 12.34 A simplified schematic of a two-stage op amp with two pairs of inputs.
image_name:Figure 12.34
description:
[
name: M1, type: NMOS, ports: {S: s1s2, D: d1s3, G: Vi1}
name: M2, type: NMOS, ports: {S: s1s2, D: d2s4, G: Vi2}
name: M3, type: NMOS, ports: {S: VDD, D: d1s3, G: VB}
name: M4, type: NMOS, ports: {S: VDD, D: d2s4, G: VB}
name: M21, type: NMOS, ports: {S: LOAD2, D: d2s2d1d2, G: Vi1}
name: M22, type: NMOS, ports: {S: LOAD1, D: d2s2d1d2, G: Vi2}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: Vo1}
name: I2, type: CurrentSource, value: I2, ports: {Np: s1s2, Nn: VSS}
name: Cn, type: Capacitor, value: Cn, ports: {Np: Vi1, Nn: d1s3}
name: Cgd1, type: Capacitor, value: Cgd1, ports: {Np: Vi1, Nn: d1s3}
name: Cgd2, type: Capacitor, value: Cgd2, ports: {Np: Vi2, Nn: d2s4}
]
extrainfo:The circuit is a two-stage operational amplifier with differential inputs and outputs. It includes capacitive neutralization using transistors M21 and M22, which are in cutoff, to implement the neutralization capacitors. The circuit is designed for stability with capacitive compensation and biasing provided by current sources I1 and I2. The op amp is balanced with a low-frequency voltage gain across each capacitor Cn.

image_name:Figure 12.35
description:The circuit is a two-stage operational amplifier with capacitive neutralization using transistors M21 and M22. The input is differential with nodes Vi1 and Vi2, and the output is also differential at nodes Vo1 and Vo2. The circuit is powered by VDD and VSS, with current sources I1 and I2 providing biasing. Capacitors Cn, Cgd1, and Cgd2 are used for compensation and stability.

Figure 12.35 (a) An example of capacitive neutralization. (b) Using transistors $M_{21}$ and $M_{22}$ in cutoff to implement the neutralization capacitors.
where $a_{d m 1}$ is the low-frequency DM gain from the gate to drain of $M_{1}$ :

$$
\begin{equation*}
a_{d m 1}=\left.\frac{v_{d 1}}{\left(v_{i d} / 2\right)}\right|_{\omega=0} \tag{12.92}
\end{equation*}
$$

Because the op amp is balanced, the low-frequency voltage gain across each capacitor $C_{n}$ is $-a_{d m 1}$. Therefore, when $C_{n}$ is included, the capacitance in (12.91) becomes

$$
\begin{equation*}
C_{i d h}=C_{g s 1}+C_{g d 1}\left(1-a_{d m 1}\right)+C_{n}\left(1+a_{d m 1}\right) \tag{12.93}
\end{equation*}
$$

If $C_{n}=C_{g d 1},(12.93)$ reduces to

$$
\begin{equation*}
C_{i d h}=C_{g s 1}+2 C_{g d 1} \tag{12.94}
\end{equation*}
$$

which is less than the value in (12.91) if $\left|a_{d m 1}\right|>1$. The Miller effect on $C_{g d 1}$ is canceled here when $C_{n}=C_{g d 1}$ because the gain across $C_{n}$ is exactly the opposite of the gain across $C_{g d 1}$. To set $C_{n}=C_{g d 1}$, matched transistors $M_{21}$ and $M_{22}$ can be used to implement the $C_{n}$ capacitors as shown in Fig. 12.35b. ${ }^{13,14}$ These transistors operate in the cutoff region because $V_{G D 1}<V_{t 1}$ and $V_{G D 2}<V_{t 2}$ since $M_{1}$ and $M_{2}$ operate in the active region. The capacitance $C_{n}$ is the sum of the gate-to-drain and gate-to-source overlap capacitances. Setting $C_{n}=C_{g d 1}$ gives

$$
\begin{equation*}
C_{g d 1}=C_{o l} W_{1}=C_{n}=C_{g d 21}+C_{g s 21}=2 C_{o l} W_{21} \tag{12.95}
\end{equation*}
$$

where $C_{o l}$ is the overlap capacitance per unit width. Therefore, if $W_{21}=W_{1} / 2, C_{n}=C_{g d 1}$. Precise matching of $C_{n}$ and $C_{g d 1}$ is not crucial here. For example, if $C_{n}$ is slightly larger than $C_{g d 1}$, the capacitance $C_{i d h}$ will be slightly less than the value in (12.94). A drawback of this technique is that junction capacitances associated with $M_{21}$ and $M_{22}$ increase the capacitances at the nodes where their sources and drains are connected, reducing the magnitude of the non-dominant pole associated with those nodes.

## 12.7 Unbalanced Fully Differential Circuits ${ }^{1,2}$

In practice, every fully differential circuit is somewhat imbalanced, due to mismatches introduced by imperfect fabrication. When mismatches are included, the models and analysis of fully differential circuits become more complicated because the mismatches introduce interaction between the CM and DM signals. The DM-to-CM and CM-to-DM cross-gain terms, as defined in Section 3.5.4, are

$$
\begin{align*}
& A_{d m-c m}=\left.\frac{v_{o c}}{v_{i d}}\right|_{v_{i c}=0}  \tag{12.96}\\
& A_{c m-d m}=\left.\frac{v_{o d}}{v_{i c}}\right|_{v_{i d}=0} \tag{12.97}
\end{align*}
$$

These cross gains are zero if a circuit is perfectly balanced and nonzero otherwise, as shown in Section 3.5.4. In a feedback circuit such as the inverting amplifier in Fig. 12.32a, imbalance in the op amp or in the feedback network generates nonzero cross-gain terms.

#### EXAMPLE

Compute the small-signal gains for the inverting amplifier shown in Fig. 12.32a. For simplicity, assume the op amp is balanced, has infinite input impedance, zero output impedance, $a_{d m} \rightarrow$ $-\infty$ and $a_{c m}^{\prime}=-0.1$. (This $a_{c m}^{\prime}$ is the CM gain, including the effect of the CMFB loop.) The
image_name:(a)
description:
[
name: Vsd/2, type: VoltageSource, value: Vsd/2, ports: {Np: Vsd/2, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: X1, N2: Vsd/2}
name: R3, type: Resistor, value: R3, ports: {N1: Vid/2, N2: Vod/2}
name: adm*vid/2, type: VoltageControlledVoltageSource, value: adm*Vid/2, ports: {Np: Vod/2, Nn: GND}
name: irc*ΔR/2, type: VoltageSource, value: irc*ΔR/2’, ports: {Np: X1, Nn: Vid/2'}
]
extrainfo:The circuit is a differential mode (DM) half-circuit for an inverting amplifier with a balanced op amp. The circuit includes a voltage source 'Vsd' connected to a resistor 'R', which is then connected to another voltage source 'Vid'. The output is taken across a resistor 'R3' and a voltage-controlled voltage source 'adm'.
image_name:(b)
description:
[
name: Vsc, type: VoltageSource, value: Vsc, ports: {Np: Vsc, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: Vsc, N2: X1}
name: i_Rd/2*ΔR, type: Resistor, value: i_rd/2*ΔR/2, ports: {N1: X1, N2: Vic}
name: R3, type: Resistor, value: R3, ports: {N1: Vic, N2: Voc}
name: Acm, type: VoltageControlledVoltageSource, value: Acm Vic, ports: {Np: Voc, Nn: GND}
]
extrainfo:The circuit diagram represents a common-mode (CM) half-circuit for analyzing the gain stage in a feedback amplifier with a balanced op amp. The circuit includes a voltage source Vsc, resistors R and ΔR/2, and a voltage-controlled voltage source Acm Vic.
Figure 12.36 Coupled (a) DM and (b) CM half-circuits for the gain stage in Fig. $12.32 a$ with a balanced op amp and mismatch in the feedback network.
resistors across the op amp are matched with $R_{3}=R_{4}=5 \mathrm{k} \Omega$, but the resistors that connect to the signal source are mismatched with $R_{1}=1.01 \mathrm{k} \Omega$ and $R_{2}=0.99 \mathrm{k} \Omega$. Therefore, the only imbalance in this circuit stems from the mismatch between $R_{1}$ and $R_{2}$.

We will analyze this circuit using coupled half-circuits, which were introduced in Section 3.5.6.9. The two coupled half-circuits are shown in Fig. 12.36. The circuits are coupled by the nonzero resistor mismatch

$$
\Delta R=R_{1}-R_{2}=0.02 \mathrm{k} \Omega
$$

The resistance $R$ in the figure is the average value of the mismatched resistors

$$
R=\frac{R_{1}+R_{2}}{2}=1 \mathrm{k} \Omega
$$

Letting $a_{d m} \rightarrow-\infty$ in the DM half-circuit gives

$$
\begin{equation*}
\frac{v_{o d}}{2}=-\frac{R_{3}}{R}\left(\frac{v_{s d}}{2}-i_{R c} \frac{\Delta R}{2}\right) \tag{12.98}
\end{equation*}
$$

Analysis of the CM half-circuit gives

$$
\begin{equation*}
v_{o c}=-\frac{R_{3}}{R}\left(v_{s c}-\frac{i_{R d}}{2} \frac{\Delta R}{2}\right) \frac{1}{1+\left[\frac{R+R_{3}}{\left(-a_{c m}^{\prime}\right) R}\right]} \tag{12.99}
\end{equation*}
$$

From these equations and the coupled half-circuits, exact input-output relationships could be found. However, for small mismatches, the approximate method described in Section 3.5.6.9 simplifies the analysis and provides sufficient accuracy for hand calculations. The key simplification in the approximate analysis is that the currents $i_{R d}$ and $i_{R c}$ are estimated from their respective half-circuits, ignoring mismatch effects. If the mismatch is ignored in Fig. 12.36a
(i.e., if $\Delta R=0$ ), then

$$
\begin{equation*}
\frac{i_{R d}}{2} \approx \frac{\hat{i}_{R d}}{2}=\frac{v_{s d}}{2 R} \tag{12.100}
\end{equation*}
$$

since $v_{i d} / 2=0$ (because $a_{d m} \rightarrow-\infty$ ). Ignoring resistor mismatch in Fig. 12.36b, we find

$$
\begin{equation*}
i_{R c} \approx \hat{i}_{R c}=\frac{v_{s c}}{R+R_{3}}\left(1+\frac{R_{3}}{R} \cdot \frac{1}{1+\left[\frac{R+R_{3}}{\left(-a_{c m}^{\prime}\right) R}\right]}\right) \tag{12.101}
\end{equation*}
$$

Using (12.101) in (12.98) gives

$$
\begin{equation*}
\frac{v_{o d}}{2}=-\frac{R_{3}}{R}\left\{\frac{v_{s d}}{2}-v_{s c} \frac{\Delta R}{2\left(R+R_{3}\right)}\left(1+\frac{R_{3}}{R} \cdot \frac{1}{1+\left[\frac{R+R_{3}}{\left(-a_{c m}^{\prime}\right) R}\right]}\right)\right\} \tag{12.102}
\end{equation*}
$$

Substituting (12.100) into (12.99) gives

$$
\begin{equation*}
v_{o c}=-\frac{R_{3}}{R}\left(v_{s c}-v_{s d} \frac{\Delta R}{4 R}\right) \frac{1}{1+\left[\frac{R+R_{3}}{\left(-a_{c m}^{\prime}\right) R}\right]} \tag{12.103}
\end{equation*}
$$

From (12.102),

$$
\begin{gathered}
A_{d m}=\left.\frac{v_{o d}}{v_{s d}}\right|_{v_{s c}=0}=-\frac{R_{3}}{R}=-\frac{5}{1}=-5 \\
A_{c m-d m}=\left.\frac{v_{o d}}{v_{s c}}\right|_{v_{s d}=0}=\frac{R_{3}}{R} \frac{\Delta R}{\left(R+R_{3}\right)}\left(1+\frac{R_{3}}{R} \cdot \frac{1}{1+\left[\frac{R+R_{3}}{\left(-a_{c m}^{\prime}\right) R}\right]}\right) \\
=\frac{5}{1} \cdot \frac{0.02}{(1+5)}\left(1+\frac{5}{1} \cdot \frac{1}{1+\left[\frac{1+5}{0.1(1)}\right]}\right)=0.018
\end{gathered}
$$

From (12.103),

$$
\begin{aligned}
& A_{c m}=\left.\frac{v_{o c}}{v_{s c}}\right|_{v_{s d}=0}=-\frac{R_{3}}{R} \frac{1}{1+\left[\frac{R+R_{3}}{\left(-a_{c m}^{\prime}\right) R}\right]}=-\frac{5}{1} \cdot \frac{1}{1+\left[\frac{1+5}{0.1(1)}\right]}=-0.082 \\
& A_{d m-c m}=\left.\frac{v_{o c}}{v_{s d}}\right|_{v_{s c}=0}=\frac{R_{3}}{R} \frac{\Delta R}{4 R} \frac{1}{1+\left[\frac{R+R_{3}}{\left(-a_{c m}^{\prime}\right) R}\right]}=\frac{5}{1} \frac{0.02}{4(1)} \frac{1}{1+\left[\frac{1+5}{0.1(1)}\right]}=0.00041
\end{aligned}
$$

The resistor mismatch causes nonzero cross-gain terms in the closed-loop amplifier. Exact analysis of this circuit gives essentially the same gain values as above.

A model for an op amp with mismatch (but assuming infinite input impedance and zero output impedance, for simplicity) is shown in Fig. 12.37. The equations corresponding to this
image_name:Figure 12.37
description:The circuit diagram represents a fully differential amplifier model with cross-gain terms. It includes an op-amp and several voltage-controlled voltage sources representing different gain factors related to differential and common-mode signals. The circuit assumes infinite input impedance and zero output impedance for the op-amp.

Figure 12.37 A simple
small-signal model of a fully differential amplifier including cross-gain terms, assuming infinite input impedance and zero output impedance.
model are

$$
\begin{align*}
& v_{o d}=a_{d m} v_{i d}+a_{c m-d m} v_{i c}+a_{c m c-d m} v_{c m c}  \tag{12.104}\\
& v_{o c}=a_{c m} v_{i c}+a_{d m-c m} v_{i d}+a_{c m c} v_{c m c} \tag{12.105}
\end{align*}
$$

The cross-gain terms $a_{c m-d m}, a_{d m-c m}$, and $a_{c m c-d m}$ are zero when the op amp is perfectly balanced. If the CM -sense circuit is not perfectly balanced, its output $v_{c m s}$, which ideally is proportional to the CM output, contains a component that depends on the DM output:

$$
\begin{equation*}
v_{c m s}=a_{c m s} v_{o c}+a_{d m-c m s} v_{o d} \tag{12.106}
\end{equation*}
$$

Also, $v_{c m c}=v_{c m s}$ when the CMFB loop is closed.
To illustrate the effect of feedback on the open-loop op-amp gains, consider the inverting amplifier in Fig. $12.32 a$ with a balanced feedback network ( $R_{1}=R_{2}$ and $R_{3}=R_{4}$ ) but with imbalances in the op amp. The circuit could be analyzed exactly to find the closed-loop gains, but the analysis is difficult. Therefore, we will use the approximate, coupled half-circuit analysis that was used in the last example. The coupled DM and CM half-circuits are shown in Fig. 12.38. The imbalances in the op amp are modeled by the $a_{c m-d m}, a_{d m-c m}$, and $a_{c m c-d m}$ controlled sources in Fig. 12.38, based on (12.104) and (12.105). To simplify the analysis, we will assume that the CM-sense circuit is balanced (i.e., $a_{d m-c m s}=0$ ). Under this assumption, (12.106) reduces to

$$
\begin{equation*}
v_{c m c}=v_{c m s}=a_{c m s} v_{o c} \tag{12.107}
\end{equation*}
$$

image_name:(a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vsd/2, N2: Vid/2}
name: R3, type: Resistor, value: R3, ports: {N1: Vid/2, N2: Vod/2}
name: Vsd/2, type: VoltageSource, value: Vsd/2, ports: {Np: Vsd/2, Nn: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: Vid/2, Nn: GND}
name: V2, type: VoltageSource, value: V2, ports: {Np: Vic/2, Nn: GND}
name: Vsc, type: VoltageSource, value: Vsc, ports: {Np: Vic, Nn: GND}
]
extrainfo:The circuit consists of differential mode (DM) and common mode (CM) half-circuits. The DM half-circuit includes resistors R1 and R3, and the CM half-circuit includes controlled voltage sources modeling op amp imbalances. The DM circuit has a voltage source Vsd/2 and the CM circuit has a voltage source Vsc.
image_name:(b)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vsc, N2: Vic}
name: R3, type: Resistor, value: R3, ports: {N1: Vic, N2: Voc}
name: Vsd, type: VoltageSource, value: Vsc, ports: {Np: Vsc, Nn: GND}
name: Vic, type: VoltageSource, value: Vic, ports: {Np: Vic, Nn: GND}
name: Voc, type: VoltageSource, value: Voc, ports: {Np: Voc, Nn: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: a_cm*Vic, Nn: a_dm-cm*Vid}
name: V2, type: VoltageSource, value: V2, ports: {Np: a_dm-cm*Vid, Nn: a_cmc*Vcmc}
]
extrainfo:This is a common-mode (CM) half-circuit for analyzing the gain stage with an unbalanced op amp and a balanced feedback network. It includes resistors, voltage sources, and controlled voltage sources modeling the imbalances in the op amp.

Figure 12.38 Coupled (a) DM and (b) CM half-circuits for the gain stage in Fig. 12.32a with an unbalanced op amp and a balanced feedback network.

Substituting (12.107) in (12.104) and (12.105) gives

$$
\begin{align*}
& v_{o d}=a_{d m} v_{i d}+a_{c m-d m} v_{i c}+a_{c m c-d m} a_{c m s} v_{o c}  \tag{12.108}\\
& v_{o c}=a_{c m} v_{i c}+a_{d m-c m} v_{i d}+a_{c m c} a_{c m s} v_{o c} \tag{12.109}
\end{align*}
$$

To carry out the approximate analysis, each half-circuit is first analyzed with the coupling between the half-circuits eliminated. Then the results of these analyses are used to find the closed-loop cross gains. The coupling in the DM half-circuit is eliminated by setting $a_{c m-d m}=$ 0 and $a_{c m c-d m}=0$. With these changes, analysis of Fig. 12.38a gives

$$
\begin{equation*}
\hat{v}_{i d}=-\frac{R_{3}}{R_{1}} \cdot \frac{1}{1+\frac{R_{1}+R_{3}}{\left(-a_{d m}\right) R_{1}}} \frac{v_{s d}}{a_{d m}} \tag{12.110}
\end{equation*}
$$

Similarly, the coupling in the CM half-circuit is eliminated by setting $a_{d m-c m}=0$. With this coupling eliminated, analysis of Fig. $12.38 b$ gives

$$
\begin{equation*}
\hat{v}_{i c}=\frac{\hat{v}_{o c}}{a_{c m}^{\prime}}=-\frac{R_{3}}{R_{1}} \cdot \frac{1}{1+\frac{R_{1}+R_{3}}{\left(-a_{c m}^{\prime}\right) R_{1}}} \frac{v_{s c}}{a_{c m}^{\prime}} \tag{12.111}
\end{equation*}
$$

where

$$
\begin{equation*}
a_{c m}^{\prime}=\frac{a_{c m}}{1+\left(-a_{c m c} a_{c m s}\right)} \tag{12.112}
\end{equation*}
$$

Assuming $\hat{v}_{i d} \approx v_{i d}, \hat{v}_{i c} \approx v_{i c}$, and $\hat{v}_{o c} \approx v_{o c},(12.110)$ and (12.111) can be used in (12.108) to give

$$
\begin{equation*}
v_{o d}=-\frac{R_{3}}{R_{1}} \cdot \frac{1}{1+\frac{R_{1}+R_{3}}{\left(-a_{d m}\right) R_{1}}} v_{s d}+\frac{a_{c m-d m}^{\prime}}{1+\frac{\left(-a_{d m}\right) R_{1}}{R_{1}+R_{3}}} \frac{\frac{R_{3}}{R_{3}+R_{1}}}{1+\frac{\left(-a_{c m}^{\prime}\right) R_{1}}{R_{1}+R_{3}}} v_{s c} \tag{12.113}
\end{equation*}
$$

where

$$
\begin{equation*}
a_{c m-d m}^{\prime}=a_{c m-d m}+a_{c m}^{\prime} a_{c m s} a_{c m c-d m} \tag{12.114}
\end{equation*}
$$

This gain has two components. The first term is $a_{c m-d m}$, which is the CM-to-DM gain of the op amp. The second term is the product of three gains: 1) $a_{c m}^{\prime}$, which is the gain from $v_{i c}$ to $v_{o c}$ including the effect of the CMFB loop, 2) $a_{c m s}$, which is the CM-sense gain from $v_{o c}$ to $v_{c m s}=v_{c m c}$, and 3) $a_{c m c-d m}$, which is the gain from $v_{c m c}$ to $v_{o d}$ (due to mismatch in the op amp). Therefore, the second term in (12.114) is the gain through an indirect path from $v_{i c}$ to $v_{o d}$.

Again assuming $\hat{v}_{i d} \approx v_{i d}, \hat{v}_{i c} \approx v_{i c}$, and $\hat{v}_{O C} \approx v_{O c},(12.110)$ and (12.111) can be used in (12.109) to give

$$
\begin{equation*}
v_{o c}=\frac{\frac{a_{c m}^{\prime} R_{3}}{R_{1}+R_{3}}}{1+\frac{\left(-a_{c m}^{\prime}\right) R_{1}}{R_{1}+R_{3}}} v_{s c}+\frac{a_{d m-c m}^{\prime}}{1+\frac{\left(-a_{c m}^{\prime}\right) R_{1}}{R_{1}+R_{3}}} \frac{\frac{R_{3}}{R_{1}+R_{3}}}{1+\frac{\left(-a_{d m}\right) R_{1}}{R_{1}+R_{3}}} v_{s d} \tag{12.115}
\end{equation*}
$$

where

$$
\begin{equation*}
a_{d m-c m}^{\prime}=\frac{a_{d m-c m}}{1+\left(-a_{c m c} a_{c m s}\right)} \tag{12.116}
\end{equation*}
$$

Equations 12.113 and 12.115 relate the DM and CM source and output voltages for the feedback amplifier. The open-loop-gain and cross-gain terms in (12.108) and (12.109) have been modified by the feedback. To allow simplification of these gain terms, define

$$
\begin{align*}
& T_{d m}=\frac{\left(-a_{d m}\right) R_{1}}{R_{1}+R_{3}}  \tag{12.117}\\
& T_{c m}=\frac{\left(-a_{c m}^{\prime}\right) R_{1}}{R_{1}+R_{3}}  \tag{12.118}\\
& T_{c m f b}=-a_{c m c} a_{c m s} \tag{12.119}
\end{align*}
$$

which are the loop gains around the DM, CM, and CMFB loops, respectively. Using (12.117)(12.119), the closed-loop gain terms in (12.113) can be written as

$$
\begin{equation*}
A_{d m}=\left.\frac{v_{o d}}{v_{s d}}\right|_{v_{s c}=0}=-\frac{R_{3}}{R_{1}} \cdot \frac{1}{1+\frac{1}{T_{d m}}} \approx-\frac{R_{3}}{R_{1}} \tag{12.120}
\end{equation*}
$$

where $\left|T_{d m}\right| \gg 1$ has been used, and

$$
\begin{equation*}
A_{c m-d m}=\left.\frac{v_{o d}}{v_{s c}}\right|_{v_{s d}=0}=\frac{a_{c m-d m}^{\prime}\left(\frac{R_{3}}{R_{3}+R_{1}}\right)}{\left(1+T_{d m}\right)\left(1+T_{c m}\right)} \tag{12.121}
\end{equation*}
$$

As $\left|T_{d m}\right|$ increases, $\left|A_{c m-d m}\right|$ decreases. Therefore, $\left|T_{d m}\right| \gg 1$ is desired to reduce the magnitude of the closed-loop CM-to-DM cross gain. The $\left(1+T_{c m}\right)$ term has little effect here since (12.112) usually gives $\left|a_{c m}^{\prime}\right| \ll 1$; therefore, $\left(1+T_{c m}\right) \approx 1$.

Using (12.116)-(12.119), the closed-loop gain terms in (12.115) can be written as

$$
\begin{equation*}
A_{c m}=\left.\frac{v_{o c}}{v_{s c}}\right|_{v_{s d}=0}=\frac{\frac{a_{c m}^{\prime} R_{3}}{R_{1}+R_{3}}}{1+T_{c m}} \approx \frac{a_{c m}^{\prime} R_{3}}{R_{1}+R_{3}} \tag{12.122}
\end{equation*}
$$

where $\left(1+T_{c m}\right) \approx 1$ has been used, and

$$
\begin{align*}
A_{d m-c m}=\left.\frac{v_{o c}}{v_{s d}}\right|_{v_{s c}=0} & =\frac{a_{d m-c m}^{\prime}}{1+T_{c m}} \frac{\frac{R_{3}}{R_{1}+R_{3}}}{1+T_{d m}} \\
& =\frac{a_{d m-c m} \frac{R_{3}}{R_{1}+R_{3}}}{\left(1+T_{c m f b}\right)\left(1+T_{d m}\right)\left(1+T_{c m}\right)} \tag{12.123}
\end{align*}
$$

As $\left|T_{d m}\right|$ or $\left|T_{c m f b}\right|$ increases, $\left|A_{d m-c m}\right|$ decreases. Therefore, the DM and CMFB loops work to reduce the closed-loop DM-to-CM cross gain. Again, the $\left(1+T_{c m}\right)$ term has little effect here since $\left|1+T_{c m}\right| \approx 1$.

The analysis in this section shows how the closed-loop cross-gain terms for the feedback amplifier in Fig. 12.32 $a$ are affected by imbalances in the op amp and feedback network. In practice, the imbalances are usually caused by random mismatches between components, and the effect of such mismatches on circuit performance is often evaluated through SPICE simulations.

## 12.8 Bandwidth of the CMFB Loop

Ideally, a fully differential circuit processes a DM input signal and produces a purely DM output signal. The closed-loop bandwidth required for the DM gain is set by the bandwidth of the DM signal. For example, consider the differential gain stage in Fig. 12.32a. To avoid filtering the signal, the closed-loop bandwidth of the DM gain must be larger than the highest frequency in the applied DM input signal. Since the closed-loop bandwidth is approximately equal to the unity-gain frequency of the DM loop gain (or return ratio), this unity-gain frequency should be about equal to the required closed-loop bandwidth. However, the unity-gain frequency required for the CMFB loop is not so easily determined. Consider a fully differential feedback circuit that is linear and perfectly balanced. If no ac CM signals are present in the circuit, the ac CM output voltage will be zero and the CM output voltage is constant. In such a case, the bandwidth of the CMFB loop is unimportant since it only operates on dc signals.

In practice, there are many sources of ac CM signals. For example, an ac CM signal can be present in the signal source, or CM noise can be introduced by coupling from a noisy power supply. Furthermore, even when the signal source is purely differential, an ac CM signal can be created by circuit imbalance that causes DM-to-CM conversion. Regardless of the source of an ac CM signal, the CMFB works to suppress the ac CM output signal and to give a CM output voltage that is about constant. Suppression of the ac CM output component is important for two reasons. First, if the CM output varies, the DM output swing must be reduced to allow for the CM output swing. Second, if two feedback amplifiers are cascaded, any ac CM output voltage from the first amplifier is a CM input voltage for the second amplifier, and any imbalance in the second amplifier will convert some of its CM input voltage into a DM output voltage.

To see how the CMFB suppresses the ac CM output signal, consider the small-signal block diagram in Fig. 12.39. Here, $v_{n}$ is a CM disturbance (for example, an ac signal on the power
image_name:Figure 12.39
description:The block diagram in Figure 12.39 represents a Common-Mode Feedback (CMFB) loop designed to suppress the AC common-mode (CM) output signal in a circuit. This diagram consists of several key components and signal paths:

1. **Main Components:**
- **Amplifier $a_n$:** This block represents the voltage gain from the common-mode disturbance $v_n$ to the common-mode output voltage $v_{oc}$ when the CMFB loop is disabled. It is the initial stage where the disturbance is amplified.
- **Summing Junctions ($\Sigma$):** There are two summing junctions in the diagram. The first one combines the output from the amplifier $a_n$ with the feedback signal. The second summing junction subtracts the feedback signal from the reference common-mode voltage $v_{cm} = 0$.
- **Amplifiers $a_{cmc}$ and $a_{cms}$:** These blocks represent the gain stages in the feedback loop. $a_{cmc}$ processes the feedback signal, and $a_{cms}$ further adjusts the signal before it is fed back to the first summing junction.

2. **Flow of Information or Control:**
- The common-mode disturbance $v_n$ is input into the amplifier $a_n$, which produces an output that is fed into the first summing junction.
- The output $v_{oc}$ from the first summing junction is the common-mode output voltage, which is also routed back into the feedback loop.
- The feedback loop starts with $v_{oc}$ being fed into the amplifier $a_{cmc}$, producing a signal that enters the second summing junction.
- At the second summing junction, the amplified feedback signal is subtracted from the reference common-mode voltage $v_{cm} = 0$.
- The result is then amplified by $a_{cms}$ and fed back into the first summing junction, completing the loop.

3. **Labels, Annotations, and Key Indicators:**
- $v_n$: Common-mode disturbance input.
- $v_{oc}$: Common-mode output voltage.
- $v_{cm} = 0$: Reference common-mode voltage, indicating no intended common-mode signal.
- $a_n$, $a_{cmc}$, $a_{cms}$: Gain values for the respective amplifiers.

4. **Overall System Function:**
- The primary function of this system is to suppress any AC common-mode output signals that arise due to disturbances like $v_n$. By employing a feedback loop, any common-mode output is fed back, compared against a reference, and adjusted to minimize its effect, thereby stabilizing the output against common-mode disturbances. The arrangement of amplifiers and summing junctions ensures that the feedback effectively cancels out unwanted common-mode signals.

Figure 12.39 A model for the CMFB loop with injected noise $v_{n}$.
supply). The signal $v_{c m}$, which is the small-signal component of the applied dc voltage $V_{C M}$, is zero. Also, $a_{n}$ is the voltage gain from the CM disturbance to the CM output voltage when the CMFB loop is disabled. That is,

$$
\begin{equation*}
a_{n}=\left.\frac{v_{o c}}{v_{n}}\right|_{\mathrm{no} \mathrm{CMFB}}=\left.\frac{v_{o c}}{v_{n}}\right|_{v_{c m c}=0} \tag{12.124}
\end{equation*}
$$

When the CMFB is active, the small-signal gain from $v_{n}$ to $v_{o c}$ becomes

$$
\begin{equation*}
A_{n}=\left.\frac{v_{o c}}{v_{n}}\right|_{\text {with } \mathrm{CMFB}}=\frac{a_{n}}{1+a_{c m s}\left(-a_{c m c}\right)} \tag{12.125}
\end{equation*}
$$

The CMFB gives $\left|A_{n}\right| \ll\left|a_{n}\right|$ at frequencies where $\left|a_{c m s}\left(-a_{c m c}\right)\right| \gg 1$. Therefore, $\left|a_{c m s}\left(-a_{c m c}\right)\right| \gg 1$ is desired at frequencies where a significant ac CM output voltage would be generated without CMFB. One possible objective is to satisfy this condition over the bandwidth of DM input signal, or equivalently to make the unity-gain frequencies of the DM and CMFB loops about equal. ${ }^{15}$ While desirable, this goal can be difficult to achieve in practice because the CMFB loop often includes more transistors and has more nondominant poles than the DM loop. In any case, suppression of spurious CM signals is an important consideration in determining the required bandwidth of the CMFB loop in practical fully differential amplifiers.

## 12.9 Analysis of a CMOS Fully Differential Folded-Cascode Op Amp

In this section, we analyze an example fully differential folded-cascode op amp. The particular op amp considered here is similar to an op amp used in an analog-to-digital converter that uses switched-capacitor gain stages. ${ }^{16}$

The core of the op amp is shown in Fig. 12.40. The op amp is a complementary version of the folded-cascode op amp shown in Fig. 12.31. Transistors $M_{1}-M_{2}$ form the NMOS input differential pair. NMOS transistors are used here because they have larger $k^{\prime}$ than PMOS devices and therefore yield larger $g_{m}$ for the same device dimensions and currents. Transistors $M_{3}-M_{5}$ and $M_{11}-M_{12}$ act as current sources. Transistors $M_{1 A}, M_{2 A}, M_{3 A}$ and $M_{4 A}$ are cascode
image_name:Figure 12.40 Folded-cascode op-amp circuit
description:The circuit is a folded-cascode operational amplifier. It uses NMOS transistors for the input differential pair to provide larger transconductance. PMOS transistors are used in the cascode configuration to enhance the output resistance and gain. The gate of M6 is used for common-mode control.

Figure 12.40 Folded-cascode op-amp circuit.
devices that boost the output resistance and also the dc voltage gain of the op amp. Finally, $M_{6}$ is a transistor that does not appear in Fig. 12.31. The gate of $M_{6}$ is the common-mode control (CMC) input. The common-mode sense circuit, which will be described later, connects to the CMC node.

The op amp makes repeated use of unit transistors to assure good matching, accurate ratios of $W / L$ values, and process insensitivity, as described in Section 6.3 .3 [see the paragraph after (6.68)]. Multiple unit transistors are connected either in parallel to increase the $W / L$ or in series to decrease the $W / L$. The unit transistor has $W=40 \mu \mathrm{~m}$ and $L=0.4 \mu \mathrm{~m}$.

The bias circuits for the op amp in Fig. 12.40 are shown in Fig. 12.41. The nodes BiasA through BiasD of the bias circuit connect to the nodes with the same labels in the op amp in Fig. 12.40.

The dimensions of the transistors in Figures 12.40 and 12.41 are given in Tables 12.1 and 12.2 , respectively. In these tables, $m$ is a factor that multiplies the $W / L$ of a unit transistor to give the aspect ratio of a transistor. For example, $m=10$ for $M_{1}$ (i.e., $m_{1}=10$ ), which means that $M_{1}$ consists of ten unit transistors connected in parallel. Therefore, $(W / L)_{1}=10 \cdot[W / L$ of a unit transistor $]$. For $M_{23}, \quad m_{23}=1 / 3$, which means that $M_{23}$ consists of three unit transistors connected in series. Therefore, $(W / L)_{23}=$ $(1 / 3) \cdot[W / L$ of a unit transistor $]$.

The bias circuit consists of three branches: $M_{21}-M_{24}, M_{25}-M_{30}$, and $M_{31}-M_{33}$. The bias circuit makes extensive use of the Sooch cascode current mirror, which was described in Section 4.2.5.2 and shown in Fig. 4.12. For simplicity, first consider transistors $M_{21}-M_{26}$. The topology here is the PMOS counterpart of the Sooch current mirror in Fig. 4.12b. Input bias current $I_{\text {BIAS }}$ flows through the left-hand branch that contains $M_{21}-M_{24}$. Since $M_{21}-M_{22}$ and $M_{25}-M_{26}$ are all identical, these transistors form a 1:1 current mirror, so $I_{\text {BIAS }}$ flows through $M_{25}-M_{26}$ and then through $M_{27}-M_{30}$. Since $M_{21}-M_{22}$ and $M_{31}-M_{32}$ are identical, $I_{\text {BIAS }}$ also flows through $M_{31}-M_{33}$. The value of $I_{\text {BIAS }}$ is 0.2 mA .
image_name:Figure 12.41 Bias circuit for the op amp
description:The circuit is a bias circuit for an op-amp, utilizing a current mirror configuration. The input bias current (IBIAS) is 0.2 mA. The transistors M21-M22 and M25-M26 form a 1:1 current mirror, and the same current flows through M31-M32. The configuration is used to maintain a stable biasing condition across different branches of the circuit.

Figure 12.41 Bias circuit for the op amp.

Table 12.1 Op-amp transistor data. A unit transistor has $W=40 \mu \mathrm{~m}, L=0.4 \mu \mathrm{~m}$ and $L_{\text {eff }}=0.3 \mu \mathrm{~m}$.

|  | $M_{1}, M_{2}$ | $M_{1 A}, M_{2 A}$ | $M_{3}, M_{3 A}, M_{4}, M_{4 A}$ | $M_{5}, M_{6}$ | $M_{11}, M_{12}$ |
| :--- | :---: | :---: | :---: | :---: | :---: |
| $m(W / L$ scale factor $)$ | 10 | 24 | 12 | 10 | 44 |
| calculated $\left\|I_{D}\right\|(\mathrm{mA})$ | 2.0 | 2.4 | 2.4 | 2.0 | 4.4 |
| simulated $\left\|I_{D}\right\|(\mathrm{mA})$ | 2.01 | 2.40 | 2.40 | $2.05,1.97$ | 4.41 |

Table 12.2 Bias-circuit transistor data. A unit transistor has $W=40 \mu \mathrm{~m}, L=0.4 \mu \mathrm{~m}$ and $L_{\text {eff }}=0.3 \mu \mathrm{~m}$.

|  | $M_{21}, M_{22}, M_{25}, M_{26}, M_{31}, M_{32}$ | $M_{23}$ | $M_{24}, M_{27}$ | $M_{28}$ | $M_{29}, M_{30}$ | $M_{33}$ |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| $m(W / L$ scale factor) | 2 | $1 / 3$ | 3 | $1 / 9$ | 1 | $1 / 14$ |
| calculated $\left\|I_{D}\right\|(\mathrm{mA})$ | 0.20 | 0.20 | 0.20 | 0.20 | 0.20 | 0.20 |
| simulated $\left\|I_{D}\right\|(\mathrm{mA})$ | 0.20 | 0.20 | 0.20 | 0.20 | 0.20 | 0.20 |

In the following analysis, we will ignore body effect for simplicity and assume the squarelaw equations describe the transistor operation. Typical process parameters $\lambda_{n}=0.15 \mathrm{~V}^{-1}$, $\lambda_{p}=0.17 \mathrm{~V}^{-1}, k_{n}^{\prime}=170 \mu \mathrm{~A} / \mathrm{V}, k_{p}^{\prime}=45 \mu \mathrm{~A} / \mathrm{V}$, and $V_{t n}=-V_{t p}=0.50 \mathrm{~V}$ are used. For simplicity, $\Delta W$ is assumed negligible (i.e., $\Delta W=0$ ), and $L_{\text {eff }}=0.3 \mu \mathrm{~m}$ will be used for transistors with $L=0.4 \mu \mathrm{~m}$. The supply voltage for the op amp is $V_{D D}=2 \mathrm{~V}$.

### 12.9.1 DC Biasing

The gates of $M_{11}-M_{12}$ and $M_{1 A}-M_{2 A}$ in the op amp are biased by voltages BiasB and BiasC, respectively, developed in the bias circuit. $M_{11}$ and $M_{12}$ mirror the current flowing in $M_{21}$, with a current gain of

$$
\begin{equation*}
\frac{I_{D 11}}{I_{D 21}}=\frac{I_{D 12}}{I_{D 21}}=\frac{(W / L)_{11}}{(W / L)_{21}}=\frac{m_{11}}{m_{21}}=\frac{(W / L)_{12}}{(W / L)_{21}}=\frac{m_{12}}{m_{21}}=\frac{44}{2}=22 \tag{12.126}
\end{equation*}
$$

Here we have used the fact that the ratio of transistor $W / L$ values is equal to the ratio of the corresponding $m$ values when unit devices are used. Therefore,

$$
\begin{equation*}
I_{D 11}=I_{D 12}=22 I_{\mathrm{BIAS}}=22(0.2 \mathrm{~mA})=4.4 \mathrm{~mA} \tag{12.127}
\end{equation*}
$$

Transistors $M_{27}-M_{30}$ form the input branch of a NMOS Sooch cascode current mirror with three output branches: cascode mirrors $M_{3}-M_{3 A}$ and $M_{4}-M_{4 A}$, and simple current source $M_{5}$. Transistor $M_{5}$ mirrors the current flowing in $M_{30}$ with a current gain of

$$
\begin{equation*}
\frac{I_{D 5}}{I_{D 30}}=\frac{m_{5}}{m_{30}}=\frac{10}{1} \tag{12.128}
\end{equation*}
$$

Hence

$$
\begin{equation*}
I_{D 5}=10 I_{D 30}=10(0.2 \mathrm{~mA})=2.0 \mathrm{~mA} \tag{12.129}
\end{equation*}
$$

Transistors $M_{3}$ and $M_{4}$ mirror the current flowing in $M_{30}$ with a current gain of

$$
\begin{equation*}
\frac{I_{D 3}}{I_{D 30}}=\frac{I_{D 4}}{I_{D 30}}=\frac{m_{3}}{m_{30}}=\frac{m_{4}}{m_{30}}=\frac{12}{1} \tag{12.130}
\end{equation*}
$$

so

$$
\begin{equation*}
I_{D 3}=I_{D 4}=12 I_{D 30}=12(0.2 \mathrm{~mA})=2.4 \mathrm{~mA} \tag{12.131}
\end{equation*}
$$

The $M_{31}-M_{33}$ branch is included to generate a dc voltage at node BiasE. This voltage is used to bias nodes in the switched-capacitor feedback application, which is described later in this section.

In the bias circuit in Fig. 12.41, the drain current of each transistor is 0.2 mA . In the op amp, the drain currents range from 2.0 mA to 4.4 mA . Lower current is used in the bias circuit to reduce power dissipation there. While low-power dissipation in the bias circuit is desirable, the impedances associated with the bias nodes BiasA-BiasE increase as the current $I_{\text {BIAS }}$ decreases. The device dimensions are scaled based on the drain currents. Two transistors will have the same $V_{o v}$ if they have the same ratios of drain current to $W / L$, or the same current densities (as defined in Section 6.3.3). The $W / L$ values in the bias circuit were chosen to make the $V_{D S}$ of each transistor in the op amp greater than its $V_{o v}$, so it operates in the active (or saturation) region with high output resistance as explained in Section 4.2.5.2.

Calculated and simulated drain currents are given in Tables 12.1 and 12.2.
To estimate the output voltage swing of the op amp, the voltages $V_{\text {BiasC }}$ and $V_{B i a s D}$ at nodes BiasC and BiasD, respectively, are needed. To find BiasD, we first find the voltage at node BiasA, $V_{\text {BiasA }}$ :

$$
\begin{equation*}
V_{\text {BiasA }}=V_{G S 30}=V_{t 30}+V_{o v 30} \tag{12.132}
\end{equation*}
$$

where

$$
\begin{equation*}
V_{o v 30}=\sqrt{\frac{2\left(I_{D 30}\right)}{k_{n}^{\prime}(W / L)_{30}}}=\sqrt{\frac{2(0.2 \mathrm{~mA})}{\left(170 \mu \mathrm{~A} / \mathrm{V}^{2}\right)(40 / 0.3)}}=0.13 \mathrm{~V} \tag{12.133}
\end{equation*}
$$

Therefore,

$$
\begin{equation*}
V_{\text {BiasA }}=V_{G S 30}=V_{t 30}+V_{o v 30}=(0.50+0.13) \mathrm{V}=0.63 \mathrm{~V} \tag{12.134}
\end{equation*}
$$

Now, we will find $V_{\text {Bias }}$. Using KVL,

$$
\begin{equation*}
V_{\text {BiasD }}=V_{G S 30}+V_{D S 28} \tag{12.135}
\end{equation*}
$$

The drain currents in $M_{27}$ and $M_{28}$ are equal:

$$
\begin{equation*}
I_{D 27}=I_{D 28} \tag{12.136}
\end{equation*}
$$

Since $M_{27}$ operates in the active or saturation region and $M_{28}$ operates in the triode region, (12.136) can be rewritten as

$$
\begin{equation*}
\frac{k_{n}^{\prime}}{2}\left(\frac{W}{L}\right)_{27}\left(V_{G S 27}-V_{t 27}\right)^{2}=\frac{k_{n}^{\prime}}{2}\left(\frac{W}{L}\right)_{28}\left[2\left(V_{G S 28}-V_{t 28}\right) V_{D S 28}-V_{D S 28}^{2}\right] \tag{12.137}
\end{equation*}
$$

Using KVL,

$$
\begin{equation*}
V_{G S 28}=V_{D S 28}+V_{G S 27} \tag{12.138}
\end{equation*}
$$

Substituting (12.138) into (12.137) and using $V_{t 27}=V_{t 28}$ yields

$$
\begin{equation*}
\frac{k_{n}^{\prime}}{2}\left(\frac{W}{L}\right)_{27}\left(V_{G S 27}-V_{t 27}\right)^{2}=\frac{k_{n}^{\prime}}{2}\left(\frac{W}{L}\right)_{28}\left[2\left(V_{D S 28}+V_{G S 27}-V_{t 27}\right) V_{D S 28}-V_{D S 28}^{2}\right] \tag{12.139}
\end{equation*}
$$

Dividing both sides by $k_{n}^{\prime} / 2$ and replacing $V_{G S 27}-V_{t 27}$ with $V_{o v 27}$ gives

$$
\begin{equation*}
\left(\frac{W}{L}\right)_{27}\left(V_{o v 27}\right)^{2}=\left(\frac{W}{L}\right)_{28}\left[2\left(V_{D S 28}+V_{o v 27}\right) V_{D S 28}-V_{D S 28}^{2}\right] \tag{12.140}
\end{equation*}
$$

The unknowns in (12.140) are $V_{D S 28}$ and $V_{o v 27}$. The overdrive voltage $V_{o v 27}$ is

$$
\begin{equation*}
V_{o v 27}=\sqrt{\frac{2\left(I_{D 27}\right)}{k_{n}^{\prime}(W / L)_{27}}}=\sqrt{\frac{2(0.2 \mathrm{~mA})}{\left(170 \mu \mathrm{~A} / \mathrm{V}^{2}\right)(40 / 0.3)(3)}}=0.077 \mathrm{~V} \tag{12.141}
\end{equation*}
$$

Substituting this overdrive voltage and $W / L$ values from Table 12.2 into (12.140) gives

$$
\begin{equation*}
V_{D S 28}=0.33 \mathrm{~V} \tag{12.142}
\end{equation*}
$$

Finally, substituting (12.134) and (12.142) into (12.135) gives

$$
\begin{equation*}
V_{\text {Bias } D}=0.63 \mathrm{~V}+0.33 \mathrm{~V}=0.96 \mathrm{~V} \tag{12.143}
\end{equation*}
$$

A similar analysis could be carried out to find the voltage at node BiasC. However, an alternative approach is used next to find this voltage. First, we find the voltage at node BiasB, $V_{B i a s B}$, which is $V_{S G 21}$ below $V_{D D}$ :

$$
\begin{equation*}
V_{\text {BiasB }}=V_{D D}-V_{S G 21} \tag{12.144}
\end{equation*}
$$

A component of $V_{S G 21}$ is

$$
\begin{equation*}
\left|V_{o v 21}\right|=\sqrt{\frac{2\left|I_{D 21}\right|}{k_{p}^{\prime}(W / L)_{21}}}=\sqrt{\frac{2(0.2 \mathrm{~mA})}{\left(45 \mu \mathrm{~A} / \mathrm{V}^{2}\right)(40 / 0.3)(2)}}=0.18 \mathrm{~V} \tag{12.145}
\end{equation*}
$$

Hence

$$
\begin{equation*}
V_{S G 21}=\left|V_{t 21}\right|+\left|V_{o v 21}\right|=(0.50+0.18) \mathrm{V}=0.68 \mathrm{~V} \tag{12.146}
\end{equation*}
$$

Using KVL,

$$
\begin{equation*}
V_{\text {BiasC }}=V_{\text {BiasB }}-V_{S G 23 \oplus 24}+V_{S G 24} \tag{12.147}
\end{equation*}
$$

Here, the symbol $\oplus$ means "in series with." Therefore, $V_{S G 23 \oplus 24}$ is the gate-to-source voltage of a transistor $M_{23 \oplus 24}$ that is equivalent to $M_{23}$ in series with $M_{24}$. The aspect ratio of this equivalent transistor $M_{23 \oplus 24}$ can be found by adding the lengths of the series transistors, after scaling to match their $W$ values:

$$
\begin{equation*}
\left(\frac{W}{L}\right)_{23 \oplus 24}=\frac{1}{3}\left(\frac{W}{L}\right)_{u} \oplus \frac{3}{1}\left(\frac{W}{L}\right)_{u}=\frac{3}{9}\left(\frac{W}{L}\right)_{u} \oplus \frac{3}{1}\left(\frac{W}{L}\right)_{u}=\frac{3}{10}\left(\frac{W}{L}\right)_{u} \tag{12.148}
\end{equation*}
$$

Hence

$$
\begin{equation*}
\left|V_{o v 23 \oplus 24}\right|=\sqrt{\frac{2\left|I_{D 23 \oplus 24}\right|}{k_{p}^{\prime}(W / L)_{23 \oplus 24}}}=\sqrt{\frac{2(0.2 \mathrm{~mA})}{\left(45 \mu \mathrm{~A} / \mathrm{V}^{2}\right)(40 / 0.3)(3 / 10)}}=0.47 \mathrm{~V} \tag{12.149}
\end{equation*}
$$

The overdrive voltage for $M_{24}$, which is active, is

$$
\begin{equation*}
\left|V_{o v 24}\right|=\sqrt{\frac{2\left|I_{D 24}\right|}{k_{n}^{\prime}(W / L)_{24}}}=\sqrt{\frac{2(0.2 \mathrm{~mA})}{\left(45 \mu \mathrm{~A} / \mathrm{V}^{2}\right)(40 / 0.3)(3)}}=0.15 \mathrm{~V} \tag{12.150}
\end{equation*}
$$

Using (12.144), (12.145), (12.147), (12.149), and (12.150), the voltage at node BiasC is

$$
\begin{align*}
V_{\text {BiasC }} & =V_{\text {BiasB }}-V_{S G 23 \oplus 24}+V_{S G 24} \\
& =V_{D D}-V_{S G 21}-\left(\left|V_{t 23 \oplus 24}\right|+\left|V_{\text {ov } 23 \oplus 24}\right|\right)+\left(\left|V_{t 24}\right|+\left|V_{\text {ov } 24}\right|\right) \\
& =[2.0-0.68-(0.50+0.47)+(0.50+0.15)] \mathrm{V}=1.0 \mathrm{~V} \tag{12.151}
\end{align*}
$$

### 12.9.2 Low-Frequency Analysis

The low-frequency DM gain of the op amp can be found using the DM half-circuit in Fig. 12.42 and is given by

$$
\begin{equation*}
a_{d m 0}=-g_{m 1} \times R_{o d h} \tag{12.152}
\end{equation*}
$$

where $R_{\text {odh }}$ is the output resistance of the DM half-circuit. This resistance is the parallel combination of the resistance looking into the drain of $M_{1 A}$ and the resistance looking into the drain of $M_{3 A}$. It is given by

$$
\begin{equation*}
R_{o d h} \approx\left[r_{o 1 A} g_{m 1 A}\left(r_{o 11} \| r_{o 1}\right)\right] \|\left(r_{o 3 A} g_{m 3 A} r_{o 3}\right) \tag{12.153}
\end{equation*}
$$

We now compute transconductance values that will be used in this section:

$$
\begin{align*}
g_{m 1} & =\sqrt{2 k_{n}^{\prime}(W / L)_{1} I_{D 1}} \\
& =\sqrt{2\left(170 \times 10^{-6}\right)[10(40 / 0.3)] 0.002} \frac{\mathrm{~A}}{\mathrm{~V}}=30 \mathrm{~mA} / \mathrm{V} \tag{12.154}
\end{align*}
$$

image_name:Figure 12.42 DM half-circuit for the op amp.
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1s1A, G: Vid/2}
name: M3, type: NMOS, ports: {S: GND, D: d3s3A, G: BiasA}
name: M3A, type: NMOS, ports: {S: d3s3A, D: Vod/2, G: BiasD}
name: M1A, type: PMOS, ports: {S: VDD, D: d1s1A, G: BiasC}
name: M11, type: PMOS, ports: {S: VDD, D: d1s1A, G: BiasB}
name: CL, type: Capacitor, value: CL, ports: {Np: Vod/2, Nn: GND}
]
extrainfo:The circuit is a DM half-circuit for an op amp, involving NMOS and PMOS transistors with biasing voltages. It includes a capacitor CL connected to the output Vod/2. The nodes are labeled according to their connections with the transistors and bias voltages.

Figure 12.42 DM half-circuit for the op amp.

$$
\begin{align*}
g_{m 1 A} & =\sqrt{2 k_{p}^{\prime}(W / L)_{1 A}\left|I_{D 1 A}\right|} \\
& =\sqrt{2\left(45 \times 10^{-6}\right)[24(40 / 0.3)] 0.0024} \frac{\mathrm{~A}}{\mathrm{~V}}=26 \mathrm{~mA} / \mathrm{V}  \tag{12.155}\\
g_{m 3} & =g_{m 3 A}=\sqrt{2 k_{n}^{\prime}(W / L)_{3 A} I_{D 3}} \\
& =\sqrt{2\left(170 \times 10^{-6}\right)[12(40 / 0.3)] 0.0024} \frac{\mathrm{~A}}{\mathrm{~V}}=36 \mathrm{~mA} / \mathrm{V}  \tag{12.156}\\
g_{m 6} & =\sqrt{2 k_{n}^{\prime}(W / L)_{6} I_{D 6}} \\
& =\sqrt{2\left(170 \times 10^{-6}\right)[10(40 / 0.3)] 0.002} \frac{\mathrm{~A}}{\mathrm{~V}}=30 \mathrm{~mA} / \mathrm{V}  \tag{12.157}\\
g_{m 11} & =\sqrt{2 k_{p}^{\prime}(W / L)_{11}\left|I_{D 11}\right|} \\
& =\sqrt{2\left(45 \times 10^{-6}\right)[44(40 / 0.3)] 0.0044} \frac{\mathrm{~A}}{\mathrm{~V}}=48 \mathrm{~mA} / \mathrm{V} \tag{12.158}
\end{align*}
$$

The output resistances, using $r_{o}=1 /\left(\left|I_{D}\right| \lambda\right)$, are

$$
\begin{gather*}
r_{o 1}=\frac{1}{(2.0 \mathrm{~mA})\left(0.15 \mathrm{~V}^{-1}\right)}=3330 \Omega  \tag{12.159}\\
r_{o 1 A}=\frac{1}{(2.4 \mathrm{~mA})\left(0.17 \mathrm{~V}^{-1}\right)}=2450 \Omega  \tag{12.160}\\
r_{o 3}=r_{o 3 A}=\frac{1}{(2.4 \mathrm{~mA})\left(0.15 \mathrm{~V}^{-1}\right)}=2780 \Omega \tag{12.161}
\end{gather*}
$$

$$
\begin{gather*}
r_{o 5}=r_{o 6}=\frac{1}{(2.0 \mathrm{~mA})\left(0.15 \mathrm{~V}^{-1}\right)}=3330 \Omega  \tag{12.162}\\
r_{o 11}=\frac{1}{(4.4 \mathrm{~mA})\left(0.17 \mathrm{~V}^{-1}\right)}=1340 \Omega \tag{12.163}
\end{gather*}
$$

Plugging values into (12.153) and (12.152) gives:

$$
\begin{align*}
R_{o d h} & \approx\left[r_{o 1 A} g_{m 1 A}\left(r_{o 11} \| r_{o 1}\right)\right] \|\left(r_{o 3 A} g_{m 3 A} r_{o 3}\right) \\
& =[2450(0.026)(1340 \| 3330)] \|[2780(0.036) 2780] \Omega \\
& =(60.9 \mathrm{k}) \|(278 \mathrm{k}) \Omega=50.0 \mathrm{k} \Omega \tag{12.164}
\end{align*}
$$

and

$$
\begin{equation*}
a_{d m 0}=-g_{m 1} \times R_{o d h} \approx-0.030 \times 50.0 \mathrm{k}=-1500 \tag{12.165}
\end{equation*}
$$

The CM half-circuit is shown in Fig. 12.43. The transistor labeled " $1 / 2 \cdot M_{5}$ " is half of $M_{5}$, that is, it has half the $W$, half the drain current, and the same $L$ as $M_{5}$. Therefore, " $1 / 2 \cdot M_{5}$ " has half the transconductance of $M_{5}$ and twice the output resistance of $M_{5}$. Similarly, the transistor labeled " $1 / 2 \cdot M_{6}$ " is half of $M_{6}$. The CM gain of the op amp is the gain of the half-circuit from $v_{i c}$ to $v_{o c}$ with $v_{c m c}=0$ :

$$
\begin{equation*}
a_{c m 0}=\left.\frac{v_{o c}}{v_{i c}}\right|_{v_{c m c}=0}=-\frac{g_{m 1}}{1+g_{m 1} R_{t}} \cdot R_{o c h} \approx-\frac{1}{R_{t}} \cdot R_{o c h} \tag{12.166}
\end{equation*}
$$

This gain is the product of the transconductance of $M_{1}$ degenerated by resistance $R_{t}$ and the output resistance of the CM half-circuit, $R_{o c h}$. Here $R_{t}$ is the resistance looking down into the drains of " $1 / 2 \cdot M_{5}$ " and " $1 / 2 \cdot M_{6}$ "; therefore, $R_{t}$ is the parallel connection of the output resistances of " $1 / 2 \cdot M_{5}$ " $\left(=2 r_{05}\right)$ and " $1 / 2 \cdot M_{6}$ " $\left(=2 r_{06}\right)$. The approximation in (12.166) is
image_name:Figure 12.43 CM half-circuit for the op amp
description:
[
name: M1, type: NMOS, ports: {S: s1d5d6, D: d1s1A, G: Vic}
name: M6, type: NMOS, ports: {S: GND, D: s1d5d6, G: Vcmc}
name: M5, type: NMOS, ports: {S: GND, D: s1d5d6, G: BiasA}
name: M11, type: NMOS, ports: {S: GND, D: d1s1A, G: BiasB}
name: M1A, type: PMOS, ports: {S: VDD, D: d1s1A, G: BiasC}
name: M3A, type: NMOS, ports: {S: s3Ad3, D: Voc, G: BiasD}
name: M3, type: NMOS, ports: {S: GND, D: s3Ad3, G: BiasA}
]
extrainfo:This circuit is a CM half-circuit for an op amp, designed to find the Common Mode (CM) and Common Mode Control (CMC) gains. It features NMOS and PMOS transistors with biasing nodes labeled BiasA, BiasB, BiasC, and BiasD. The circuit uses a combination of NMOS and PMOS transistors to achieve desired gain characteristics.

Figure 12.43 CM half-circuit for the op amp, for finding the CM and CMC gains.
image_name:Figure 12.44
description:This circuit is a switched-capacitor CM sense network with capacitors Ca and Cb, each valued at 0.1 pF. The nodes labeled Vo1, CMC, and Vo2 are connected through capacitors to the BiasE and BiasA nodes. The circuit is designed to sense common mode signals and is part of a larger op amp circuit.

Figure 12.44 The switched-capacitor CM sense network. $C_{a}=C_{b}=0.1 \mathrm{pF}$. The nodes labeled $V_{C M}$ are connected to BiasE in Fig. 12.41.
based on the assumption that $g_{m 1} R_{t} \gg 1$. Resistance $R_{o c h}$ is the parallel combination of the resistance looking into the drain of $M_{1 A}$, and the resistance looking into the drain of $M_{3 A}$ in the CM half-circuit. Hence

$$
\begin{align*}
R_{o c h} & \approx\left[r_{o 1 A} g_{m 1 A}\left(r_{o 11} \| R_{o}\left(M_{1}\right)\right)\right] \|\left(r_{o 3 A} g_{m 3 A} r_{o 3}\right) \\
& \approx\left[r_{o 1 A} g_{m 1 A}\left(r_{o 11}\right)\right] \|\left(r_{o 3 A} g_{m 3 A} r_{o 3}\right) \\
& =[2450(0.026) 1340] \|[2780(0.036) 2780] \Omega \\
& =(85.0 \mathrm{k}) \|(278 \mathrm{k}) \Omega=65.3 \mathrm{k} \Omega \tag{12.167}
\end{align*}
$$

where $R_{o}\left(M_{1}\right) \approx r_{o 1} g_{m 1}\left[\left(2 r_{o 5}\right) \|\left(2 r_{o 6}\right)\right]$ is the resistance looking into the drain of $M_{1}$. The assumption $R_{o}\left(M_{1}\right) \gg r_{o 11}$ was used in (12.167), which yields $r_{o 11} \| R_{o}\left(M_{1}\right) \approx r_{o 11}$. Substituting values into (12.166) gives

$$
\begin{align*}
a_{c m 0} & \approx-\frac{1}{R_{t}} \cdot R_{o c h}=-\frac{1}{\left(2 r_{o 5}\right) \|\left(2 r_{o 6}\right)} \cdot R_{o c h}  \tag{12.168}\\
& =-\frac{1}{(2 \cdot 3330) \|(2 \cdot 3330)} \cdot(65.3 \mathrm{k})=-\frac{1}{3330} \cdot(65.3 \mathrm{k})=-19.6
\end{align*}
$$

The CM sense circuit consists of four capacitors and six switches and is shown in Fig. 12.44. This switched-capacitor network was described in Section 12.5.4 and shown previously in Fig. 12.21. Here, the switches, which are implemented with MOS transistors in practice, are drawn as ideal switches for simplicity. For a purely CM output, the gain of the CM sense circuit in Fig. 12.44 is close to unity, so $v_{c m c} \approx v_{o c}$. The CMC node of the CM sense circuit connects to the gate of $M_{6}$ in the op amp, which is also labeled $C M C$ in Figure 12.40. The CM sense network and the op amp form a negative feedback loop that forces the CM output voltage of the op amp to approximately equal the voltage $V_{\text {BiasE }}$, which is generated in Fig. 12.41 and is about 0.9 V .

The common-mode control (CMC) gain of the op amp is the gain from $v_{c m c}$ to $v_{o c}$ with $v_{i c}=0$. It can be found using the CM half-circuit in Fig. 12.43:

$$
\begin{equation*}
a_{c m c 0}=\left.\frac{v_{o c}}{v_{c m c}}\right|_{v_{i c}=0}=-\frac{g_{m b}}{2} \times R_{o c h} \tag{12.169}
\end{equation*}
$$

where $R_{\text {och }}$ is the output resistance of the CM half-circuit as given by (12.167). Substituting values into (12.169) yields

$$
\begin{align*}
a_{c m c 0} & =-\frac{g_{m 6}}{2} \times R_{o c h} \approx-\left(\frac{0.030}{2}\right)(65.3 \mathrm{k})  \tag{12.170}\\
& =-980
\end{align*}
$$

The low-frequency DM, CM, and CMC gains calculated above and from SPICE simulations are listed in Table 12.3. Reasons for the differences between calculated and simulated values include short-channel effects (the transistor behavior deviates from the simple

Table 12.3 Calculated and simulated op-amp gains.

|  | Calculated | Simulated |
| :--- | :---: | :---: |
| $\left\|a_{d m 0}\right\|$ | 1500 | 1280 |
| $\left\|a_{c m 0}\right\|$ | 19.6 | 20.5 |
| $\left\|a_{c m c 0}\right\|$ | 980 | 660 |

square-law equations on which our small-signal formulas are based), errors in $r_{o}$ ( $\lambda_{n}$ and $\lambda_{p}$ are not constant in practice and depend on $V_{D S}$ ), body effect (which was ignored in the calculations), and approximations used to simplify the calculations.

The output voltage swing of the op amp is now estimated. Consider the output swing of $V_{o 1}$ in Fig. 12.40. The upper swing limit occurs when $M_{1 A}$ enters the triode region. This occurs when the gate-to-drain voltage of $M_{1 A}$ equals a threshold voltage. Thus, using (12.151), the upper swing limit of $V_{o 1}$ is

$$
\begin{equation*}
V_{o 1}(\max )=V_{\text {Bias } C}+\left|V_{t 1 A}\right|=1.0 \mathrm{~V}+0.50 \mathrm{~V}=1.50 \mathrm{~V} \tag{12.171}
\end{equation*}
$$

The lower swing limit of $V_{o 1}$ occurs when $M_{3 A}$ enters the triode region. This occurs when the gate-to-drain voltage of $M_{3 A}$ equals a threshold voltage. Using (12.143), the lower swing limit of $V_{o 1}$ is

$$
\begin{equation*}
V_{o 1}(\min )=V_{B i a s D}-V_{t 3 A}=0.96 \mathrm{~V}-0.50 \mathrm{~V}=0.46 \mathrm{~V} \tag{12.172}
\end{equation*}
$$

Therefore the peak-to-peak output swing of $V_{o 1}$ is

$$
\begin{equation*}
V_{o 1, p p}=V_{o 1}(\max )-V_{o 1}(\min )=1.50 \mathrm{~V}-0.46 \mathrm{~V}=1.04 \mathrm{~V} \tag{12.173}
\end{equation*}
$$

if the CMFB circuit biases $V_{o 1}$ midway between the swing limits. In that case, the peak-to-peak differential output swing, which is twice the swing of either $V_{o 1}$ or $V_{o 2}$, is

$$
\begin{equation*}
V_{o d, p p}=2 V_{o 1, p p}=2(1.04) \mathrm{V}=2.08 \mathrm{~V} \tag{12.174}
\end{equation*}
$$

Simulation gives a differential output swing of 2.4 V .
The common-mode input range (CMIR) of the op amp is the range of CM input voltage over which the transistors associated with the input differential pair remain in the active or saturation region. The lower limit of the CMIR occurs when the CM input voltage forces either $M_{5}$ or $M_{6}$ into the triode region. Since $M_{5}$ and $M_{6}$ have equal drain currents and aspect ratios, they both enter the triode region when $V_{D S 5}=V_{D S 6}=V_{o v 5}$. The corresponding CM input voltage is

$$
\begin{align*}
V_{I C}(\min ) & =V_{G S 1}+V_{o v 5}=V_{t 1}+V_{o v 1}+V_{o v 5} \\
& =V_{t 1}+\sqrt{\frac{2\left(I_{D 1}\right)}{k_{n}^{\prime}(W / L)_{1}}}+\sqrt{\frac{2\left(I_{D 5}\right)}{k_{n}^{\prime}(W / L)_{5}}} \\
& =0.50 \mathrm{~V}+\sqrt{\frac{2(2.0 \mathrm{~mA})}{\left(170 \mu \mathrm{~A} / \mathrm{V}^{2}\right)(40 / 0.3)(10)}}+\sqrt{\frac{2(2.0 \mathrm{~mA})}{\left(170 \mu \mathrm{~A} / \mathrm{V}^{2}\right)(40 / 0.3)(10)}} \\
& =0.50 \mathrm{~V}+0.13 \mathrm{~V}+0.13 \mathrm{~V}=0.76 \mathrm{~V} \tag{12.175}
\end{align*}
$$

The upper limit of the CMIR occurs when the CM input voltage forces either $M_{1}$ or $M_{2}$ into the triode region. Since $M_{1}$ and $M_{2}$ are matched with equal drain currents, they both enter the triode region when the CM input voltage is a threshold voltage above the voltage at the drain
of $M_{1}$ or $M_{2}$. Considering $M_{1}$, its drain voltage is also the voltage at the source of $M_{1 A}, V_{S 1 A}$. Therefore, using (12.151):

$$
\begin{align*}
V_{I C}(\max ) & =V_{S 1 A}+V_{t 1}=V_{\text {BiasC }}+V_{S G 1 A}+V_{t 1} \\
& =V_{\text {BiasC }}+\left|V_{t 1 A}\right|+\left|V_{o v 1 A}\right|+V_{t 1} \\
& =V_{\text {BiasC }}+\left|V_{t 1 A}\right|+\sqrt{\frac{2\left|I_{D 1 A}\right|}{k_{p}^{\prime}(W / L)_{1 A}}}+V_{t 1}  \tag{12.176}\\
& =1.0 \mathrm{~V}+0.50 \mathrm{~V}+\sqrt{\frac{2(2.4 \mathrm{~mA})}{\left(45 \mu \mathrm{~A} / \mathrm{V}^{2}\right)(40 / 0.3)(24)}}+0.50 \mathrm{~V}=2.2 \mathrm{~V}
\end{align*}
$$

From (12.175) and (12.176), the CMIR is from 0.76 V to 2.2 V . The bias circuit generates $V_{\text {BiasE }}=0.9 \mathrm{~V}$. As described in the next subsection, this voltage sets the CM input voltage of the op amp to 0.9 V , which falls within the CMIR of the op amp. The CMIR for this foldedcascode op amp is fairly large. The CMIR for a folded-cascode op amp is usually larger than the CMIR for a telescopic-cascode op amp designed in the same CMOS technology, due to the "folded" topology.

The input-referred noise of the op amp can be found by considering a DM half-circuit, summing the contributions of the device noise-current generators to the output current when the output node is shorted to small-signal ground, and then referring the output noise to the op-amp input. These calculations are carried out next. Flicker noise is ignored for simplicity here.

Fig. 12.45 shows the DM small-signal half-circuit including a noise generator for each transistor. Here, the output is shorted to ground to allow calculation of the output noise current. For simplicity, let $r_{o} \rightarrow \infty$ for all transistors and ignore all capacitors. The drain currents of $M_{1}, M_{3}$, and $M_{11}$ all flow into the short at the output. Therefore, noise in these currents directly
image_name:Figure 12.45 DM small-signal half-circuit of the op amp showing the noise-voltage generators
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1s1A, G: g1}
name: M11, type: PMOS, ports: {S: GND, D: d1s1A, G: g11}
name: M1A, type: PMOS, ports: {S: GND, D: d1s1A, G: g1A}
name: M3A, type: NMOS, ports: {S: GND, D: d3s3A, G: g3A}
name: M3, type: NMOS, ports: {S: GND, D: d3s3A, G: g3}
]
extrainfo:The circuit is a DM small-signal half-circuit of an op amp including noise-voltage generators. The output is shorted to ground for noise current calculation. NMOS transistors M1 and M3 contribute to the output noise current, while PMOS transistors M1A and M11 do not.

Figure 12.45 DM small-signal half-circuit of the op amp showing the noise-voltage generators.
contributes to the noise in the output current $i_{o 1}$. However, $M_{1 A}$ and $M_{3 A}$ do not contribute to the output noise current. To understand why, first consider $M_{3 A}$. Using superposition, consider only the noise-voltage source connected to its gate. The drain current of $M_{3 A}$ is the product of this noise voltage and the transconductance of $M_{3 A}$ degenerated by the resistance $r_{o 3}$. With $r_{o 3} \rightarrow \infty$, the degenerated transconductance is zero, and therefore $\overline{v_{i 3 A}^{2}}$ does not contribute to the noise in the output current $i_{o 1}$. Similarly, $M_{1 A}$ does not contribute to the noise in the output current. Therefore, the total noise current at the output is the sum of the noise-current contributions from $M_{1}, M_{3}$, and $M_{11}$ in Fig. 12.45:

$$
\begin{equation*}
\frac{\overline{i_{o 1}^{2}}}{\Delta f}=g_{m 1}^{2} \frac{\overline{v_{i 1}^{2}}}{\Delta f}+g_{m 11}^{2} \frac{\overline{v_{i 11}^{2}}}{\Delta f}+g_{m 3}^{2} \frac{\overline{v_{i 3}^{2}}}{\Delta f} \tag{12.177}
\end{equation*}
$$

Using the thermal-noise voltage expression from (11.68a):

$$
\begin{equation*}
\frac{\overline{v_{i}^{2}}}{\Delta f}=4 k T \frac{2}{3} \frac{1}{g_{m}} \tag{12.178}
\end{equation*}
$$

for each noise-voltage generator, the total output noise current in (12.177) can be written:

$$
\begin{equation*}
\frac{\overline{i_{o 1}^{2}}}{\Delta f}=g_{m 1}^{2} 4 k T \frac{2}{3} \frac{1}{g_{m 1}}+g_{m 11}^{2} 4 k T \frac{2}{3} \frac{1}{g_{m 11}}+g_{m 3}^{2} 4 k T \frac{2}{3} \frac{1}{g_{m 3}} \tag{12.179}
\end{equation*}
$$

At $T=300^{\circ} \mathrm{K}, 4 k T=1.66 \times 10^{-16} \mathrm{~V}$-C. Substituting $4 k T$ and $g_{m}$ values into (12.179) and evaluating gives

$$
\begin{equation*}
\overline{\frac{i_{o 1}^{2}}{\Delta f}}=(3.32+5.32+3.98) \times 10^{-22} \mathrm{~A}^{2} / \mathrm{Hz}=12.6 \times 10^{-22} \mathrm{~A}^{2} / \mathrm{Hz} \tag{12.180}
\end{equation*}
$$

Referring this output noise current to an equivalent noise voltage $v_{\text {eq } H}$ at the input of the DM half-circuit yields

$$
\begin{equation*}
\frac{\overline{v_{\mathrm{eq} H}^{2}}}{\Delta f}=\frac{\overline{i_{o 1}^{2}}}{\Delta f} \cdot \frac{1}{g_{m 1}^{2}}=12.6 \times 10^{-22} \mathrm{~A}^{2} / \mathrm{Hz} \cdot \frac{1}{(30 \mathrm{~mA} / \mathrm{V})^{2}}=1.40 \times 10^{-18} \mathrm{~V}^{2} / \mathrm{Hz} \tag{12.181}
\end{equation*}
$$

Analysis of the other DM half-circuit yields the same input-referred noise, and the noise voltages in each half-circuit are uncorrelated. Therefore, the total equivalent input-noise voltage for the fully differential op amp, $v_{\text {eq } T}$, is

$$
\begin{equation*}
\frac{\overline{v_{\mathrm{eq} T}^{2}}}{\Delta f}=2 \frac{\overline{v_{\mathrm{eq} H}^{2}}}{\Delta f}=2 \times 1.40 \times 10^{-18} \mathrm{~V}^{2} / \mathrm{Hz}=2.80 \times 10^{-18} \mathrm{~V}^{2} / \mathrm{Hz} \tag{12.182}
\end{equation*}
$$

or

$$
\begin{equation*}
\sqrt{\frac{\overline{v_{\mathrm{eq} T}^{2}}}{\Delta f}}=\sqrt{2.80 \times 10^{-18} \mathrm{~V}^{2} / \mathrm{Hz}}=1.67 \frac{\mathrm{nV}}{\sqrt{\mathrm{~Hz}}} \tag{12.183}
\end{equation*}
$$

SPICE simulation gives $1.9 \mathrm{nV} / \sqrt{\mathrm{Hz}}$. The flicker noise could be included in the above calculations using the formulas in Chapter 11.

### 12.9.3 Frequency and Time Responses in a Feedback Application

The DM gain of the op amp is frequency dependent due to poles and zeros caused by the capacitances associated with the transistors in the op amp. Hand calculation of the frequency response
image_name:Figure 12.46 Switched-capacitor amplifier
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: In(A0), Nn: Vs1}
name: C1, type: Capacitor, value: C1, ports: {Np: Ip(A0), Nn: Vs2}
name: C2, type: Capacitor, value: C2, ports: {Np: In(A0), Nn: V1}
name: C2, type: Capacitor, value: C2, ports: {Np: Ip(A0), Nn: V2}
name: CL, type: Capacitor, value: CL, ports: {Np: Vo1, Nn: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: Vo2, Nn: GND}
name: A0, type: OpAmp, value: A0, ports: {InP: Ip(A0), InN: In(A0), OutP: Vo2, OutN: Vo1}
]
extrainfo:The circuit is a switched-capacitor amplifier using an op-amp with differential inputs and outputs. It includes capacitors for charge transfer and switches controlled by clock phases φ1 and φ2. The circuit operates with differential signals Vs1 and Vs2, and provides differential outputs Vo1 and Vo2. The op-amp is used to amplify the difference between the input signals. The capacitors C1 and C2 are used for charge storage and transfer, while CL provides load capacitance at the output. Bias voltages and clock signals control the operation of switches to facilitate the amplification process.

Figure 12.46 Switched-capacitor amplifier that uses the op amp in Figure 12.40. The CM sense circuitry is not shown.
is possible but the result is often inaccurate since the poles and zeros depend on device and parasitic capacitances. Therefore, the frequency response of the op-amp gain is usually simulated. Also, the op amp is always used in feedback, and the stability of the feedback loops, under the loading imposed in part by the passive feedback elements, is a key issue. Therefore, the magnitude and phase responses of the return ratio of each feedback loop is of interest. The feedback loops will be considered later in this section for the feedback circuit that is described next.

Fig. 12.46 shows the op amp used in a fully differential switched-capacitor application. The operation of this circuit is similar to that of the single-ended switched-capacitor gain stage in Fig. 6.8a, and it uses the clocks shown in Fig. 6.8b. Ideally, this circuit provides a voltage gain during $\phi_{1}$ of $-C_{1} / C_{2}$. In practice, the MOS transistors act as switches, and the switches are designed so that their resistance when on (and in the triode region) is small enough to be ignored. The ideal value of the CM input and output voltages is $V_{\text {BiasE }}$, which is the voltage at node BiasE, and $V_{B B}$ is the CM value of the input sources $V_{s 1}$ and $V_{s 2}$. When $\phi_{1}$ is high, the circuit is redrawn in Fig. 12.47. (The CM input and output voltages of the op amp are the same in Fig. 12.46, but they could be different. The CM input voltage must fall within the CM input range, and the CM output voltage is usually chosen to maximize output swing. Sometimes two different bias voltages are used to independently optimize these voltages.) Here, switches driven by the $\phi_{1}$ clock are short circuits, and switches driven by $\phi_{2}$ are open circuits. An op amp can appear in the feedback configuration in Fig. 12.47 in many applications, such as a switched-capacitor gain stage and a switched-capacitor integrator, which is shown in Fig. 6.10a.

Because node BiasE connects to switches in Fig. 12.46, its voltage can experience significant transients after switching. If other bias voltages were produced by the same branch in Fig. 12.41 that generates $V_{\text {BiasE }}$, significant transients could be introduced in these other bias voltages also. To avoid this problem, the branch in Fig. 12.41 that generates $V_{\text {BiasE }}$ generates no other bias voltages.

For the feedback circuit in Fig. 12.47, stability of the DM and CM feedback loops is considered next, using a combination of simulations and calculations. Return ratio is used to investigate stability. In the following, $C_{1}=C_{2}=1 \mathrm{pF}$ and the value of the load capacitance $C_{L}$ varies.
image_name:Figure 12.47
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Vs1, Nn: InN(A0)}
name: C1, type: Capacitor, value: C1, ports: {Np: Vs2, Nn: InP(A0)}
name: C2, type: Capacitor, value: C2, ports: {Np: InN(A0), Nn: Vo1}
name: C2, type: Capacitor, value: C2, ports: {Np: InP(A0), Nn: Vo2}
name: CL, type: Capacitor, value: CL, ports: {Np: Vo1, Nn: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: Vo2, Nn: GND}
name: A0, type: OpAmp, value: A0, ports: {InP: InP(A0), InN: InN(A0), OutP: Vo1, OutN: Vo2}
]
extrainfo:The circuit is a switched-capacitor amplifier with a common-mode feedback (CMFB) circuit. Capacitors C1 and C2 are used for sampling and integrating the input signals Vs1 and Vs2, respectively. The operational amplifier A0 amplifies the differential input, while CL capacitors serve as load capacitors. The CM Sense block is used to stabilize the common-mode voltage.

Figure 12.47 The switchedcapacitor amplifier of Figure 12.46 when phase $\phi_{1}$ is high.

The return ratio can be simulated using an extension of the technique described in Problem 8.33, which allows exact simulation of the return ratio when a controlled source is not accessible. ${ }^{11}$ For example, with the feedback broken at the $\times$ marks in Fig. 12.48, the quantities $\mathcal{R}_{v, d m}^{\prime}$ and $\mathcal{R}_{i, d m}^{\prime}$ are simulated, and then these quantities are combined to calculate the return ratio $\mathcal{R}_{d m}$ using the equation in Problem 8.33.

For the return-ratio simulation, a dc path to each op-amp input is provided by each resistor $R_{\text {BIG }}$ in Fig. 12.48. A very large resistance, $R_{\text {BIG }}=1 \times 10^{12} \Omega$, is used that has little effect on the simulation results at frequencies where $\omega \gg 1 /\left(R_{\mathrm{BIG}} C_{1}\right)$. The dc voltage at each op-amp input is $V_{\text {BiasE }}$, which is developed at node BiasE in the bias circuit in Fig. 12.41. Without these resistors, the dc op-amp input voltages are undefined, and therefore, SPICE would not be able to simulate the circuit. In normal operation, one plate of each switched capacitor is alternately connected to BiasE or an op-amp input as shown in Fig. 12.46. This switching makes the dc voltage at the op-amp inputs equal the voltage $V_{B i a s E}$.

The simulated magnitude and phase responses of the return ratio for the DM feedback loop are plotted in Fig. 12.49. Here, the load capacitance in the DM half-circuit is $C_{L}=2 \mathrm{pF}$. The phase margin is $72^{\circ}$, and the gain margin is 38 dB . The frequency $f_{r}$ where the magnitude of the return ratio is unity is 390 MHz .

For comparison to simulation, the DM return ratio will now be calculated. The feedback circuit in Fig. 12.47 is shown in Fig. 12.50a with two capacitors $C_{i a}$ added; these capacitors
image_name:Figure 12.48
description:The circuit is a differential amplifier with feedback, using an op-amp (A_0) with input signals V_s1 and V_s2. The feedback network includes capacitors C_2 and load capacitors C_L. The op-amp outputs are connected to a common-mode sense circuit.

Figure 12.48 The feedback circuit in Figure 12.47, with resistors $R_{\text {BIG }}$ added to bias the op-amp inputs.
image_name:(a)
description:The graph in Figure 12.49(a) is a Bode plot representing the magnitude response of the differential mode (DM) return ratio for a circuit with a load capacitance of 2 pF. The x-axis is labeled "Frequency (Hz)" and is plotted on a logarithmic scale, ranging from 100 Hz to 10 GHz. The y-axis is labeled "|Return Ratio|" and is also on a logarithmic scale, ranging from 0.01 to 1000.

**Overall Behavior and Trends:**
- The graph shows a flat region at lower frequencies, indicating a constant return ratio.
- As the frequency increases, there is a noticeable drop in the return ratio starting around 100 MHz, indicating a decrease in feedback effectiveness as frequency increases.
- The graph crosses the 1 (unity) return ratio line at approximately 380 MHz, marking the frequency where the feedback becomes ineffective.

**Key Features and Technical Details:**
- A gain margin (GM) of 38 dB is indicated on the graph, showing the difference in decibels between the unity gain frequency and the frequency where the phase crosses -180 degrees (as shown in the phase plot).
- The return ratio decreases sharply beyond the 380 MHz point, indicating a high-frequency roll-off.

**Annotations and Specific Data Points:**
- The unity gain crossover frequency is marked at 380 MHz.
- The graph includes a dashed line highlighting the gain margin of 38 dB.
image_name:(b)
description:The graph labeled "(b)" is a Bode plot depicting the phase response of the differential mode (DM) return ratio for a circuit with a load capacitance \( C_L = 2 \text{ pF} \).

1. **Type of Graph and Function:**
- This is a Bode plot focusing on the phase response of the return ratio.

2. **Axes Labels and Units:**
- The x-axis represents frequency in hertz (Hz), ranging from 100 Hz to 10 GHz, presented on a logarithmic scale.
- The y-axis represents the phase of the return ratio in degrees, ranging from 0° to -225°.

3. **Overall Behavior and Trends:**
- The phase starts at 0° and decreases steadily as the frequency increases.
- There is a notable drop in phase around the 380 MHz frequency, indicating a significant phase shift.
- The phase continues to decrease, approaching -180° as the frequency nears the upper limit.

4. **Key Features and Technical Details:**
- A significant phase shift occurs at 380 MHz, which is marked on the graph.
- The phase margin (PM) is given as 72°, indicating the stability margin of the system.
- The phase crosses -180° at a higher frequency, which is crucial for assessing stability.

5. **Annotations and Specific Data Points:**
- The graph annotates the frequency of 380 MHz and the phase margin of 72°.
- A horizontal line at -180° is used as a reference to indicate the critical phase shift point for stability analysis.

Figure 12.49 Simulated DM return ratio for $C_{L}=2 \mathrm{pF}$. (a) Magnitude and (b) phase responses.
model the op-amp input impedance. The corresponding DM small-signal half-circuit is shown in Fig. 12.50b, where the op-amp output port is modeled simply by a transconductance $g_{m 1}$ and resistance $R_{\text {odh }}$ [based on (12.165)]. This model ignores all poles and zeros except the pole associated with the $R C$ time constant at the op-amp output node.

If the feedback is broken at the $\times$ in Fig. $12.50 b$ and the input voltage $V_{s d} / 2$ is set to zero for calculation of the DM return ratio, the total load capacitance from the op-amp output to ground is

$$
\begin{equation*}
C_{L \mathrm{eff}}=C_{L}+\frac{C_{2}\left(C_{1}+C_{i a}\right)}{C_{2}+C_{1}+C_{i a}} \tag{12.184}
\end{equation*}
$$

Here the capacitors in the CM sense block are ignored for simplicity; in practice, they are small compared to the capacitors $C_{1}, C_{2}$ and $C_{L}$. The right-most term in (12.184) is the capacitance associated with $C_{2}$ in series with the parallel connection of $C_{1}$ and $C_{i a}$. Based on a simulation
image_name:(a)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Vs1, Nn: IN(A0)}
name: C1, type: Capacitor, value: C1, ports: {Np: Vs2, Nn: IP(A0)}
name: Cia, type: Capacitor, value: Cia, ports: {Np: IN(A0), Nn: x1}
name: Cia, type: Capacitor, value: Cia, ports: {Np: IP(A0), Nn: x1}
name: C2, type: Capacitor, value: C2, ports: {Np: 1N(A0), Nn: Vo1}
name: C2, type: Capacitor, value: C2, ports: {Np: 1P(A0), Nn: Vo2}
name: CL, type: Capacitor, value: CL, ports: {Np: Vo1, Nn: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: Vo2, Nn: GND}
name: A0, type: OpAmp, value: A0, ports: {InP: 1N(A0), InN: 1P(A0), OutP: Vo1, OutN: Vo2}
]
extrainfo:The circuit is a feedback configuration with an operational amplifier (A0) that has input impedance modeled by capacitors Cia. The output nodes Vo1 and Vo2 are connected to ground through capacitors CL. The circuit includes a CM (Common Mode) Sense block to monitor the output.

image_name:(b)
description:The circuit is a differential mode small-signal half-circuit with an operational amplifier. The op-amp input impedance is modeled by capacitor Cia, and the output is connected to ground through capacitor CL. The circuit includes a feedback path with a resistor Rodh and a voltage-controlled current source gm1Ve.

Figure 12.50 (a) The feedback circuit with the op-amp input impedance modeled by the $C_{i a}$ capacitors, which are shown explicitly. (b) The DM smallsignal half-circuit. The node between the two $C_{i a}$ capacitors is a ground for DM signals. The $X$ marks a break point for calculating the DM return ratio.
of the input impedance of the op amp (by applying an ac voltage across the op-amp input, measuring the op-amp input current, and then computing the input capacitance), $C_{i a} \approx 2.58 \mathrm{pF}$. Capacitance $C_{i a}$ is the sum of $C_{g s 1}$ and $C_{g d 1}$ increased by the Miller effect. Substituting values into (12.184) gives

$$
\begin{equation*}
C_{L \text { eff }}=C_{L}+\frac{C_{2}\left(C_{1}+C_{i a}\right)}{C_{2}+C_{1}+C_{i a}}=2 \mathrm{pF}+\frac{1(1+2.58)}{1+1+2.58} \mathrm{pF}=2.72 \mathrm{pF} \tag{12.185}
\end{equation*}
$$

For comparison, the DM return ratio can be calculated with the feedback loop broken in the simplified circuit in Fig. 12.50b. Following Section 8.8, the calculated return ratio is:

$$
\begin{equation*}
\mathcal{R}_{d m}(\omega)=g_{m 1} R_{o d h} \cdot \frac{1}{1+j \omega R_{o d h} C_{L e f f}} \cdot \frac{C_{2}}{C_{2}+C_{1}+C_{i a}} \tag{12.186}
\end{equation*}
$$

The pole here is $-1 /\left(R_{o d h} C_{L \text { eff }}\right)$, due to the $R C$ time constant at the op-amp output in Fig. $12.50 b$. Here $C_{L \text { eff }}$ is the effective output load capacitance with the loop broken, as given by (12.184). At dc, (12.186) reduces to

$$
\begin{equation*}
\mathcal{R}_{d m 0}=\mathcal{R}_{d m}(\omega=0)=g_{m 1} R_{o d h} \cdot 1 \cdot \frac{C_{2}}{C_{2}+C_{1}+C_{i a}} \tag{12.187}
\end{equation*}
$$

At high frequencies $\left[\omega \gg 1 /\left(R_{o d h} C_{L e f f}\right)\right],(12.186)$ reduces to

$$
\begin{equation*}
\mathcal{R}_{d m}(\omega) \approx g_{m 1} \cdot \frac{1}{j \omega C_{L \mathrm{eff}}} \cdot \frac{C_{2}}{C_{2}+C_{1}+C_{i a}} \tag{12.188}
\end{equation*}
$$

The unity-gain frequency $\omega_{r}$ of the return ratio [i.e., the frequency where $\left|\mathcal{R}_{d m}\left(\omega_{r}\right)\right|=1$ ] can be found using (12.185) and (12.188):

$$
\begin{align*}
\omega_{r} & \approx \frac{g_{m 1}}{C_{L \text { eff }}} \cdot \frac{C_{2}}{C_{2}+C_{1}+C_{i a}}=\frac{0.030}{2.72 \times 10^{-12}} \cdot \frac{1}{1+1+2.58} \mathrm{rad} / \mathrm{s} \\
& =2.4 \mathrm{Grad} / \mathrm{s}=2 \pi(380 \mathrm{MHz}) \tag{12.189}
\end{align*}
$$

This calculated unity-gain frequency is in good agreement with the simulated value of 390 MHz .

The DM return ratio in (12.186), which is based on the simplified op-amp model in Fig. 12.50 b , would give a phase margin of at least $90^{\circ}$, since $\mathcal{R}_{d m}(\omega)$ has only one pole that will introduce at most $-90^{\circ}$ of phase shift at $\omega_{r}$. However, poles and zeros associated with internal nodes in the op amp, along with the dominant pole $-1 /\left(R_{\text {odh }} C_{\text {Leff }}\right)$, contribute to the returnratio magnitude and phase responses at high frequencies. Therefore, the return ratio may have unacceptable gain or phase margin due to these poles and zeros. In practice, $C_{L}$, which is a significant component of $C_{L \text { eff }}$ in (12.185), is chosen to assure good gain and phase margins for the CM and DM feedback loops.

For the DM feedback loop in Fig. 12.47 with $C_{L}=1 \mathrm{pF}$, the phase margin is $65^{\circ}$, and the gain margin is 35 dB . The frequency where the magnitude of the return ratio is unity is $f_{r}=$ 550 MHz .

For the DM feedback loop in Fig. 12.47 with $C_{L}=0 \mathrm{pF}$, the capacitance $C_{L \text { eff }}$ is dominated by capacitors $C_{1}, C_{2}$, and $C_{i a}$. The phase margin is $55^{\circ}$ and the gain margin is 31 dB . The frequency where the magnitude of the return ratio is unity is $f_{r}=810 \mathrm{MHz}$.

Note that as $C_{L}$ increases, the phase margin increases and the unity-gain frequency of the DM return ratio ( $\omega_{r}=2 \pi f_{r}$ ) decreases. This is as expected, since increasing $C_{L}$ increases $C_{L e f f}$, which reduces the magnitude of the dominant pole in the return ratio without affecting the other poles and zeros.

The low-frequency closed-loop DM gain is given by

$$
\begin{equation*}
A_{c l 0, d m}=\frac{v_{o d}}{v_{s d}}=A_{\infty} \cdot \frac{\mathcal{R}_{d m 0}}{1+\mathcal{R}_{d m 0}} \tag{12.190}
\end{equation*}
$$

from (8.209). The direct feedthrough $d=0$ for this circuit, due to the capacitive feedback elements that are open circuits at dc, and hence block signal feedthrough at dc. The ideal closed-loop gain is $A_{\infty}=-C_{1} / C_{2}=-1$. Using the simulated value of $\mathcal{R}_{d m 0}$ in (12.190) yields

$$
\begin{equation*}
A_{c l 0, d m}=A_{\infty} \cdot \frac{\mathcal{R}_{d m 0}}{1+\mathcal{R}_{d m 0}}=-1 \cdot \frac{280}{1+280}=-0.996 \tag{12.191}
\end{equation*}
$$

SPICE simulation agrees exactly with this closed-loop gain. The simulated $-3-\mathrm{dB}$ bandwidth of the closed-loop gain is 630 MHz with $C_{L}=2 \mathrm{pF}$.

The CM return ratio can be simulated ${ }^{11}$ by breaking the feedback at the $\times$ marks in Fig. 12.48, simulating the quantities $\mathcal{R}_{v, c m}^{\prime}$ and $\mathcal{R}_{i, c m}^{\prime}$, and then combining these quantities to calculate the CM return ratio $\mathcal{R}_{c m}$ using the equation in Problem 8.33. There are two CM feedback loops in Fig. 12.48. One includes the CM sense circuit and the gain from the opamp CMC input to the op-amp CM output voltage. The other includes the feedback elements $C_{1}$ and $C_{2}$ and the CM gain from the op-amp CM input voltage to the op-amp CM output voltage. When the feedback is broken at the $\times$ marks in Fig. 12.48, both of these CM loops are broken. ${ }^{11}$ The simulated CM return ratio is shown in Fig. 12.51 for $C_{L}=2 \mathrm{pF}$. The phase margin is $76^{\circ}$, and the gain margin is 41 dB . So the CM loop is stable with good margins for $C_{L}=2 \mathrm{pF}$. The unity-gain frequency for this return ratio is 420 MHz .
image_name:(a)
description:The graph labeled (a) is a Bode plot depicting the magnitude response of the common-mode (CM) return ratio for a capacitance load \(C_{L}=2 \mathrm{pF}\). The plot is characterized by the following features:

1. **Axes Labels and Units:**
- **X-axis:** Frequency in Hertz (Hz), presented on a logarithmic scale ranging from 100 Hz to 10 GHz.
- **Y-axis:** Magnitude of the return ratio, \(|\text{Return Ratio}|\), also on a logarithmic scale, ranging from 0.01 to 1000.

2. **Overall Behavior and Trends:**
- The graph begins with a high return ratio magnitude at lower frequencies, close to 1000.
- As frequency increases, the magnitude remains relatively constant until around 10 MHz, after which it starts to decrease.
- A significant drop in magnitude occurs as the frequency approaches the unity-gain frequency of 420 MHz.
- Beyond this point, the magnitude continues to decline sharply, reaching below 0.1 at frequencies close to 10 GHz.

3. **Key Features and Technical Details:**
- The unity-gain frequency is marked at 420 MHz, where the return ratio magnitude crosses 1.
- The gain margin (GM) at the unity-gain frequency is indicated as 41 dB.

4. **Annotations and Specific Data Points:**
- A horizontal dashed line marks the unity-gain level (magnitude = 1).
- A vertical dashed line at 420 MHz denotes the unity-gain frequency.
- The gain margin is visually represented by a double-headed arrow indicating the distance from the unity-gain level to the point where the magnitude plot intersects the frequency axis beyond 1 GHz.

This plot provides insight into the stability and performance of the CM loop, highlighting the stability with good gain margins for the specified capacitance load.
image_name:(b)
description:The graph labeled as (b) is a Bode plot depicting the phase response of the Common Mode (CM) return ratio as a function of frequency. The x-axis represents frequency in Hertz (Hz), with a logarithmic scale ranging from 100 Hz to 10 GHz. The y-axis represents the phase of the return ratio in degrees, ranging from 0° to -225°.

**Overall Behavior and Trends:**
- The phase starts at 0° at low frequencies and decreases as the frequency increases.
- There is a notable phase dip reaching approximately -90° around the 10 MHz to 100 MHz range.
- The phase continues to decrease, crossing -180° at a frequency just below 1 GHz.

**Key Features and Technical Details:**
- The unity-gain frequency is marked at 420 MHz. At this frequency, the phase margin (PM) is indicated as 76°, showing the stability of the loop.
- The phase margin is measured between the phase at the unity-gain frequency and the -180° line, ensuring that the system remains stable with good phase margins.

**Annotations and Specific Data Points:**
- A dashed vertical line at 420 MHz highlights the unity-gain frequency.
- The phase margin of 76° is annotated on the graph, indicating a stable system with a good margin against oscillations.
- The graph shows a gradual decline in phase, emphasizing the stability characteristics of the CM loop over the frequency range.

Figure 12.51 Simulated CM return ratio for $C_{L}=2 \mathrm{pF}$. (a) Magnitude and (b) phase responses.

The CM return ratio differs from the DM return ratio because the small-signal half-circuits differ; points of symmetry are open circuits for CM signals but are small-signal grounds for DM signals. For example, the node between the two $C_{i a}$ capacitors in Fig. 12.50a is a ground for DM signals but is an open circuit for CM signals. Differences between the return ratios can be seen by comparing Figs. 12.49 and 12.51. For example, a left-half-plane zero exists in the CM return ratio at about 60 MHz . It causes the magnitude response to flatten and the phase response to increase. It was determined through simulations that this zero is related to the nonzero output impedances in the bias circuit at the BiasC and BiasD nodes. When the impedance at nodes Bias $C$ and BiasD was decreased by connecting a large capacitor from those bias nodes to ground, the effect of the zero was not visible in the magnitude or phase response, and the general shape of the CM return-ratio response resembled the plots in Fig. 12.49. With these bypass capacitors, the CM return-ratio phase margin is $54^{\circ}$, and the gain margin is 16 dB .

The step responses of the DM op-amp output voltage $V_{o d}$ for three values of $C_{L}$ are plotted in Fig. 12.52. The ideal output $V_{o d}$ is also shown; ideally $V_{o d}$ is the differential input inverted since the closed-loop DM gain is $-C_{1} / C_{2}=-1$. The overshoot/ringing in the step response
image_name:Figure 12.52
description:The graph depicted is a time-domain waveform illustrating the step responses of the differential-mode (DM) op-amp output voltage $V_{od}$ versus time $t$. The x-axis represents time in nanoseconds (ns), ranging from 0 to 6 ns, while the y-axis represents the output voltage $V_{od}$ in volts (V), ranging from 0 to 0.2 V.

The graph includes three different curves corresponding to different values of load capacitance $C_L$: 0 pF, 1 pF, and 2 pF. Additionally, a dashed line represents the ideal output $V_{od}$, which is a direct inversion of the differential input with a closed-loop DM gain of -1, resulting in a step from 0 V to -0.2 V at $t = 0.4$ ns.

1. **$C_L = 0$ pF:** This curve shows the most pronounced overshoot and ringing, indicating a lower phase margin. The response initially overshoots above 0.2 V before settling back to the steady-state value.

2. **$C_L = 1$ pF:** This curve exhibits less overshoot compared to $C_L = 0$ pF, with a more damped response. It still overshoots but to a lesser extent, suggesting a moderate phase margin.

3. **$C_L = 2$ pF:** This curve has the least overshoot and the smoothest transition to the steady-state value, indicating the highest phase margin among the three. The response is more critically damped.

The behavior of the curves demonstrates that as the load capacitance $C_L$ increases, the overshoot and ringing decrease, reflecting an increase in phase margin. The poles of the closed-loop transfer function move away from the $j \omega$ axis, stabilizing the system response.

Figure 12.52 Step responses $\left(V_{o d}\right.$ versus $t$ ) for $C_{L}=0,1$ and 2 pF . The ideal output is plotted with a dashed line. The input is a -0.2 V step applied at $t=0.4 \mathrm{~ns}$.
increases as $C_{L}$ decreases (and the phase margin decreases). As the phase margin decreases, the poles of the closed-loop transfer function move toward the $j \omega$ axis. (In a two-pole system, the closed-loop poles will be on the $j \omega$ axis when the phase margin is zero. In that case, the step response contains a sinusoid in steady state.) In switched-capacitor applications, the output of the op amp must settle to its final value within one-half clock period. For example, the output voltage of the op amp in Fig. 12.46 must settle during the time when clock $\phi_{1}$ is high. The settling time is usually found by applying a step input. Then the settling time is measured from the time the input changes until the output voltage remains within a specified band around its steady-state value. For the step responses in Fig. 12.52, the 1 percent settling times (the time until the output remains within 1 percent of the final output voltage) are 1.67 ns for $C_{L}=$ $2 \mathrm{pF}, 1.35 \mathrm{~ns}$ for $C_{L}=1 \mathrm{pF}$, and 1.37 ns for $C_{L}=0 \mathrm{pF}$.

Equation 12.189 shows that $\omega_{r}$ can be increased by increasing $g_{m 1}$, by decreasing $C_{L e f f}$ (by decreasing some or all of the capacitances that contribute to it), or by increasing the term $C_{2} /\left(C_{2}+C_{1}+C_{i a}\right)$, which is sometimes called "the feedback factor." Assuming a constant phase margin, if $\omega_{r}$ increases, the closed-loop -3-dB bandwidth increases (see Fig. 9.10) and the settling time of the step response decreases. Also, if the phase margin is larger than required, $\omega_{r}$ could be increased (and phase margin decreased) by increasing the magnitude of the dominant pole. This can be achieved by reducing $C_{L}$.

During slewing, a large voltage appears between op-amp inputs and causes one of the input transistors ( $M_{1}$ or $M_{2}$ ) in Fig. 12.40 to turn off while the other remains on. In that case, the sum of the drain currents from $M_{5}$ and $M_{6}$ flows through the input transistor that is on. This causes a current change in both $M_{1}$ and $M_{2}$ of magnitude $I_{\text {slew }}=\left(I_{D 5}+I_{D 6}\right) / 2$; this current flows from the op-amp outputs and through the differential load. The op-amp inputs are not virtually shorted during slewing because one of the op-amp input transistors is off, and thus the op-amp operation is highly nonlinear. Therefore, the total load capacitance from each op-amp output to ground is equal to $C_{L \text { eff }}$ as given in (12.184). The differential load capacitance between the two op-amp outputs will be half of $C_{L \text { eff }}$, since two $C_{L \text { eff }}$ capacitors are in series between the two op-amp outputs. Therefore, the DM output slew rate is

$$
\begin{equation*}
\frac{d V_{o d}}{d t}=\frac{I_{o}(\mathrm{max})}{\frac{C_{\text {Leff }}}{2}}=\frac{I_{\text {slew }}}{\frac{C_{L e f f}}{2}}=\frac{\frac{I_{D 5}+I_{D 6}}{2}}{\frac{C_{L \text { eff }}}{2}}=\frac{\frac{4.0}{2} \mathrm{~mA}}{\frac{2.72 \mathrm{pF}}{2}}=1.47 \frac{\mathrm{~V}}{\mathrm{~ns}} \tag{12.192}
\end{equation*}
$$

assuming all current-source transistors remain in the active region during slewing. A SPICE simulation gives a slew rate of $1.2 \mathrm{~V} / \mathrm{ns}$.
