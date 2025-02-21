# CHAPTER 15 Oscillators

Oscillators are an integral part of many electronic systems. Applications range from clock generation in microprocessors to carrier synthesis in cellular telephones, requiring vastly different oscillator topologies and performance parameters. Robust, high-performance oscillator design in CMOS technology continues to pose interesting challenges. As described in Chapter 16, oscillators are usually embedded in a phaselocked system.

This chapter deals with the analysis and design of CMOS oscillators, more specifically, voltagecontrolled oscillators (VCOs). Beginning with a general study of oscillation in feedback systems, we introduce ring oscillators and LC oscillators along with methods of varying the frequency of oscillation. We then describe a mathematical model of VCOs that will be used in the analysis of PLLs in Chapter 16.

## 15.1 ■ General Considerations

A simple oscillator produces a periodic output, usually in the form of voltage. As such, the circuit has no input while sustaining the output indefinitely. How can a circuit oscillate? Recall from Chapter 10 that negative-feedback systems may oscillate, i.e., an oscillator is a badly-designed feedback amplifier! ${ }^{1}$ Consider the unity-gain negative-feedback circuit shown in Fig. 15.1, where

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}(s)=\frac{H(s)}{1+H(s)} \tag{15.1}
\end{equation*}
$$

As mentioned in Chapter 10, if the amplifier itself experiences so much phase shift at high frequencies that the overall feedback becomes positive, then oscillation may occur. More accurately, if for $s=j \omega_{0}, H\left(j \omega_{0}\right)=-1$, then the closed-loop gain approaches infinity at $\omega_{0}$. Under this condition, the circuit amplifies its own noise components at $\omega_{0}$ indefinitely. In fact, as conceptually illustrated in Fig. 15.2, a noise component at $\omega_{0}$ experiences a total gain of unity and a phase shift of $180^{\circ}$, returning to the subtractor as a negative replica of the input. Upon subtraction, the input and the feedback signals give a larger difference. Thus, the circuit continues to "regenerate," allowing the component at $\omega_{0}$ to grow.

image_name:Figure 15.1 Feedback system
description:The feedback system depicted in Figure 15.1 consists of a basic closed-loop configuration with the following main components:

1. **Adder/Subtractor (Summing Junction):** This block has two inputs and one output. It takes the input signal \( V_{in} \) and subtracts the feedback signal from it. The output of this block is the difference between \( V_{in} \) and the feedback signal.

2. **Amplifier Block \( H(s) \):** This block represents the system's transfer function and amplifies the signal from the summing junction. The gain and phase characteristics of this block are defined by \( H(s) \), which is a function of the complex frequency variable \( s \).

3. **Feedback Path:** The output \( V_{out} \) is fed back into the summing junction. The feedback loop includes a direct connection from the output to the subtractor input, providing negative feedback.

**Flow of Information:**
- The input signal \( V_{in} \) enters the summing junction, where the feedback signal is subtracted from it.
- The resulting difference signal is then passed to the amplifier \( H(s) \), where it is amplified according to the transfer function.
- The amplified output \( V_{out} \) is then fed back into the subtractor to form a closed-loop system.

**Overall System Function:**
- The primary function of this feedback system is to control the output \( V_{out} \) by adjusting the input \( V_{in} \) and the feedback loop. The negative feedback aims to stabilize the system by reducing the effect of disturbances and maintaining the desired output level. The loop gain and phase characteristics are crucial in determining the stability and performance of the system, particularly in preventing oscillations and ensuring the desired response.

image_name:Evolution of oscillatory system with time.
description:The feedback system depicted in Figure 15.1 is designed to control an output voltage \( V_{out} \) using a feedback loop. The system consists of several key components arranged in a series of repeating blocks, each performing a similar function to stabilize and control the output.

1. **Main Components:**
- **Input Signal \( V_0 \):** The system starts with an input signal \( V_0 \), which is subject to control and feedback.
- **Summing Junctions:** These are represented by circles with a plus and minus sign. They combine the input signal with the feedback signal. The positive input is the incoming signal, while the negative input is the feedback.
- **Amplifiers \( H(s) \):** Each block contains an amplifier labeled \( H(s) \), which processes the signal from the summing junction. The function \( H(s) \) represents the system's transfer function in the Laplace domain, indicating that the system operates in the frequency domain.
- **Feedback Loops:** Each block has a feedback loop that takes the output of the amplifier and feeds it back into the summing junction, creating a closed-loop system.

2. **Flow of Information or Control:**
- The input signal \( V_0 \) is introduced at the first summing junction where it is combined with the feedback signal.
- The resulting signal is amplified by the first amplifier \( H(s) \), and the output is fed into the next stage.
- This process repeats through multiple stages, each comprising a summing junction and an amplifier with a feedback loop.
- The signal flows sequentially from left to right through the system, with feedback loops in each stage ensuring stability and control.

3. **Labels, Annotations, and Key Indicators:**
- The system uses the notation \( H(s) \) to indicate the transfer function of each amplifier, suggesting that the system’s behavior is analyzed in the frequency domain.
- The plus and minus signs at the summing junctions indicate the combination of positive input signals with negative feedback.

4. **Overall System Function:**
- The primary function of this feedback system is to control the output \( V_{out} \) by adjusting the input \( V_{in} \) and the feedback loop. The negative feedback aims to stabilize the system by reducing the effect of disturbances and maintaining the desired output level. The loop gain and phase characteristics are crucial in determining the stability and performance of the system, particularly in preventing oscillations and ensuring the desired response. The system’s design allows for dynamic control, making it suitable for applications requiring precise output regulation.

Figure 15.2 Evolution of oscillatory system with time.

For the oscillation to begin, a loop gain of unity or greater is necessary. This can be seen by following the signal around the loop over many cycles and expressing the amplitude of the subtractor's output in Fig. 15.2 as a geometric series (if $\angle H\left(j \omega_{0}\right)=180^{\circ}$ ):

$$
\begin{equation*}
V_{X}=V_{0}+\left|H\left(j \omega_{0}\right)\right| V_{0}+\left|H\left(j \omega_{0}\right)\right|^{2} V_{0}+\left|H\left(j \omega_{0}\right)\right|^{3} V_{0}+\cdots \tag{15.2}
\end{equation*}
$$

If $\left|H\left(j \omega_{0}\right)\right|>1$, the above summation diverges, whereas if $\left|H\left(j \omega_{0}\right)\right|<1$, then

$$
\begin{equation*}
V_{X}=\frac{V_{0}}{1-\left|H\left(j \omega_{0}\right)\right|}<\infty \tag{15.3}
\end{equation*}
$$

In summary, if a negative-feedback circuit has a loop gain that satisfies two conditions:

$$
\begin{align*}
\left|H\left(j \omega_{0}\right)\right| & \geq 1  \tag{15.4}\\
\angle H\left(j \omega_{0}\right) & =180^{\circ} \tag{15.5}
\end{align*}
$$

then the circuit may oscillate at $\omega_{0}$. Called "Barkhausen criteria," these conditions are necessary but not sufficient [1]. ${ }^{2}$ In order to ensure oscillation in the presence of temperature and process variations, we typically choose the loop gain to be at least twice or three times the required value.

We may state the second Barkhausen criterion as $\angle H(j \omega)=180^{\circ}$ or a total phase shift of $360^{\circ}$. This should not be confusing: if the system is designed to have low-frequency negative feedback, it already produces $180^{\circ}$ of phase shift in the signal traveling around the loop (as represented by the subtractor in Fig. 15.1), and $\angle H(j \omega)=180^{\circ}$ denotes an additional frequency-dependent phase shift that, as illustrated in Fig. 15.2, ensures that the feedback signal enhances the original signal. Thus, the three cases illustrated in Fig. 15.3 are equivalent in terms of the second criterion. We say that the system of Fig. 15.3(a) exhibits a frequency-dependent phase shift of $180^{\circ}$ (denoted by the arrow) and a dc phase shift of $180^{\circ}$. The difference between Figs. 15.3(b) and (c) is that the open-loop amplifier in the former contains enough stages with proper polarities to provide a total phase shift of $360^{\circ}$ at $\omega_{0}$, whereas that in the latter produces no phase shift at $\omega_{0}$. Examples of these topologies are presented later in this chapter.

image_name:(a)
description:The system block diagram labeled as (a) represents an oscillatory feedback system characterized by a frequency-dependent phase shift and a DC phase shift of 180 degrees. The main components of this system include a summing junction and an amplifier block denoted by \( H(j\omega) \).

1. **Main Components:**
- **Summing Junction:** This is depicted as a circular block with a plus sign, indicating it combines input signals. It has two inputs: one positive and one negative.
- **Amplifier Block:** Represented by a triangular symbol labeled \( H(j\omega) \), it processes the input signal and provides amplification. The specific function of this block is to introduce a frequency-dependent phase shift.

2. **Flow of Information or Control:**
- The input signal enters the system at the left side of the summing junction.
- The output from the summing junction is fed into the amplifier block \( H(j\omega) \).
- The amplifier modifies the signal, introducing a phase shift, and the output is then fed back into the negative input of the summing junction. This creates a feedback loop.

3. **Labels, Annotations, and Key Indicators:**
- The arrow labeled "180°" indicates a frequency-dependent phase shift of 180 degrees in the feedback path.
- The plus and minus signs at the summing junction indicate the polarities of the inputs.

4. **Overall System Function:**
- The primary function of this system is to create oscillations through feedback. The phase shift introduced by the amplifier and the feedback loop is critical in achieving the conditions necessary for sustained oscillations. The total phase shift around the loop must be 360 degrees (or a multiple thereof) for oscillation to occur, which is facilitated by the 180-degree phase shift in the feedback path and the inherent phase characteristics of the amplifier \( H(j\omega) \).

image_name:(b)
description:The system block diagram labeled as "(a)" represents an oscillatory feedback system designed to generate sustained oscillations. It consists of the following main components:

1. **Amplifier Block (H(jω))**: This block represents the amplifier in the system. It introduces a specific phase shift and gain to the signal. The amplifier's phase characteristics are crucial for achieving the total required phase shift for oscillation.

2. **Summing Junction**: The summing junction is depicted as a circle with a plus sign inside. It combines the input signal with the feedback signal. The summing action is essential for creating the conditions necessary for oscillation by ensuring that the feedback signal is appropriately added to the input.

3. **Feedback Path**: The feedback path is shown looping back from the output of the amplifier to the summing junction. This path introduces a 360-degree phase shift, which includes a 180-degree phase shift inherent in the feedback path itself, and the remaining phase shift is provided by the amplifier.

**Flow of Information**:
- The signal flows from the summing junction to the amplifier, where it is amplified and phase-shifted.
- The output of the amplifier is fed back into the summing junction through the feedback path.
- The feedback loop is crucial for maintaining the oscillations by ensuring that the signal is continually recycled through the system.

**Overall System Function**:
The primary function of this system is to generate oscillations by maintaining a total phase shift of 360 degrees around the loop. This is achieved through the combination of the amplifier's phase characteristics and the feedback path. The system is designed to sustain oscillations by ensuring that the phase and gain conditions for oscillation are met, which is critical for applications such as ring oscillators in CMOS technology.

image_name:Figure 15.3(c)
description:The block diagram in Figure 15.3 represents an oscillatory feedback system designed to generate oscillations by maintaining a total phase shift of 360 degrees around the loop. This system consists of the following main components:

1. **Summation Block (+):** This block combines the input signal with the feedback signal. It is depicted as a circle with a plus sign inside, indicating that it performs an addition operation. The input and feedback signals are combined here to form the input to the next stage.

2. **Amplifier Block (H(jω)):** Following the summation block, the combined signal is fed into an amplifier, represented by a triangle with the label H(jω). This amplifier is responsible for providing the necessary gain and phase shift to sustain oscillations. The phase shift introduced by this block is crucial to achieving the total 360-degree phase shift required for oscillation.

3. **Feedback Path:** The output of the amplifier is fed back to the summation block through a feedback path. This path is depicted with an arrow indicating a 0-degree phase shift, suggesting that the feedback is in phase with the input at this point in the loop.

**Flow of Information:**
- The input signal enters the summation block where it is combined with the feedback signal.
- The resultant signal is then amplified by the amplifier block H(jω).
- The output of the amplifier is sent back through the feedback path to the summation block, completing the loop.

**Overall System Function:**
The primary function of this system is to sustain oscillations by ensuring that both the phase and gain conditions for oscillation are met. The amplifier provides the necessary gain and phase shift, while the feedback loop ensures that the total phase shift around the loop is 360 degrees. This configuration is typical in ring oscillators, particularly in CMOS technology, where such systems are used to generate clock signals and other periodic waveforms.

Figure 15.3 Various views of oscillatory feedback system.
CMOS oscillators in today's technology are typically implemented as "ring oscillators" or "LC oscillators." We study each type in the following sections.

## 15.2 ■ Ring Oscillators

A ring oscillator consists of a number of gain stages in a loop. To arrive at the actual implementation, we begin by attempting to make a single-stage feedback circuit oscillate.

Example 15.1
Explain why a single common-source stage does not oscillate if it is placed in a unity-gain loop.

#### Solution

From Fig. 15.4, it is seen that the open-loop circuit contains only one pole, thereby providing a maximum frequencydependent phase shift of $90^{\circ}$ (at a frequency of infinity). Since the common-source stage exhibits a dc phase shift of $180^{\circ}$ due to the signal inversion from the gate to the drain, the maximum total phase shift is $270^{\circ}$. The loop therefore fails to sustain oscillation growth.
image_name:Figure 15.4
description:
[
name: RD, type: Resistor, ports: {N1: VDD, N2: Vout}
name: CL, type: Capacitor, ports: {Np: Vout, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vout}
name: VDD, type: VoltageSource, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a common-source amplifier with a resistive load and capacitive load, using an NMOS transistor. The output is taken across the capacitor CL.

Figure 15.4

The above example suggests that oscillation may occur if the circuit contains multiple stages and hence multiple poles. Indeed, such a topology was considered undesirable in Chapter 10 because it led to inadequate phase margin in op amps. We therefore surmise that if the circuit of Fig. 15.4 is modified as shown in Fig. 15.5, then two significant poles appear in the signal path, allowing the frequency-dependent
image_name:Figure 15.5
description:
[
name: M1, type: NMOS, ports: {S: GND, D: E, G: Vout}
name: M2, type: NMOS, ports: {S: GND, D: F(Vout), G: E}
name: RD1, type: Resistor, value: RD, ports: {N1: VDD, N2: E}
name: RD2, type: Resistor, value: RD, ports: {N1: VDD, N2: F}
name: CL1, type: Capacitor, value: CL, ports: {Np: E, Nn: GND}
name: CL2, type: Capacitor, value: CL, ports: {Np: F, Nn: GND}
]
extrainfo:The circuit is a two-stage feedback system with two NMOS transistors, two resistors, and two capacitors. It is prone to latch-up due to positive feedback near zero frequency.

Figure 15.5 Two-pole feedback system.
phase shift to approach $180^{\circ}$. Unfortunately, this circuit exhibits positive feedback near zero frequency due to the signal inversion through each common-source stage. As a result, it simply "latches up" rather than oscillates. That is, if $V_{E}$ rises, $V_{F}$ falls, thereby turning $M_{1}$ off and allowing $V_{E}$ to rise further. This may continue until $V_{E}$ reaches $V_{D D}$ and $V_{F}$ drops to near zero, a state that will remain indefinitely.

To gain more insight into the oscillation conditions, let us assume that an ideal inverting stage (with zero phase shift at all frequencies) is inserted in the loop of Fig. 15.5, providing negative feedback near zero frequency and eliminating the problem of latch-up (Fig. 15.6). Does this circuit oscillate? We note that the loop contains only two poles: one at $E$ and another at $F$. The frequency-dependent phase shift can therefore reach $180^{\circ}$, but at a frequency of infinity. Since the loop gain vanishes at very high frequencies, we observe that the circuit does not satisfy both of Barkhausen's criteria at the same frequency (Fig. 15.7), and thus fails to oscillate.
image_name:Figure 15.6
description:
[
name: M1, type: NMOS, ports: {S: GND, D: E, G: Vout}
name: M2, type: NMOS, ports: {S: GND, D: F, G: E}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: E}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: F}
name: CL, type: Capacitor, value: CL, ports: {Np: E, Nn: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: F, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: Ideal, type: OpAmp, value: -1, ports: {InP: F, InN: GND, Out: Vout}
]
extrainfo:The circuit is a two-pole feedback system with an additional signal inversion using an ideal op-amp. It includes two NMOS transistors (M1 and M2) with capacitive loads CL and resistive loads RD. The circuit does not oscillate as it does not meet Barkhausen's criteria at the same frequency.

Figure 15.6 Two-pole feedback system with additional signal inversion.
image_name:Figure 15.7 Loop gain characteristics of a two-pole system
description:The graph titled "Figure 15.7 Loop gain characteristics of a two-pole system" is a Bode plot comprising two subplots: one for magnitude and one for phase, both plotted against frequency on a logarithmic scale.

1. **Magnitude Plot**:
- **Y-Axis (Vertical)**: Represents 20log|H(ω)|, which is the magnitude of the loop gain in decibels (dB).
- **X-Axis (Horizontal)**: Represents frequency (ω) on a logarithmic scale.
- **Behavior**: The magnitude remains constant at 0 dB up to a certain frequency, denoted as ωp,E = ωp,F. Beyond this point, the magnitude decreases linearly at a rate of -40 dB per decade. This indicates the presence of two poles contributing to the roll-off.

2. **Phase Plot**:
- **Y-Axis (Vertical)**: Represents the phase of the loop gain, /H(ω), in degrees.
- **X-Axis (Horizontal)**: Also represents frequency (ω) on a logarithmic scale.
- **Behavior**: The phase starts at 0 degrees and decreases, passing through -90 degrees and approaching -180 degrees as frequency increases. This suggests a cumulative phase shift introduced by the poles in the system.

3. **Key Features**:
- The dashed vertical line at ωp,E = ωp,F marks the pole frequency where the behavior of the magnitude plot changes.
- The magnitude plot's slope of -40 dB/decade is characteristic of a two-pole system.
- The phase plot's progression towards -180 degrees highlights the potential for instability if additional phase shift occurs, as discussed in the context of the two-pole feedback system with signal inversion.

Figure 15.7 Loop gain characteristics of a two-pole system.
The foregoing discussion points to the need for greater phase shift around the loop, suggesting the possibility of oscillation if the third inverting stage in Fig. 15.6 contains a pole that contributes significant phase. We then arrive at the topology depicted in Fig. 15.8. If the three stages are identical, the total phase shift around the loop, $\phi$, reaches $-135^{\circ}$ at $\omega=\omega_{p, E}\left(=\omega_{p, F}=\omega_{p, G}\right)$ and $-270^{\circ}$ at $\omega=\infty$. Consequently, $\phi$ equals $-180^{\circ}$ at $\omega<\infty$, where the loop gain can still be greater than or equal to unity. This circuit indeed oscillates if the loop gain is sufficient and it is an example of a ring oscillator.

It is instructive to calculate the minimum voltage gain per stage in Fig. 15.8 that is necessary for oscillation. Neglecting the effect of the gate-drain overlap capacitance and denoting the transfer function of each stage by $-A_{0} /\left(1+s / \omega_{0}\right)$, we have for the loop gain

$$
\begin{equation*}
H(s)=-\frac{A_{0}^{3}}{\left(1+\frac{s}{\omega_{0}}\right)^{3}} \tag{15.6}
\end{equation*}
$$

image_name:Figure 15.8 Three-stage ring oscillator
description:
[
name: M1, type: NMOS, ports: {S: GND, D: E, G: F}
name: M2, type: NMOS, ports: {S: GND, D: F, G: G(Vout)}
name: M3, type: NMOS, ports: {S: GND, D: G(Vout), G: Vout}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: E}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: F}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: G(Vout)}
name: CL, type: Capacitor, value: CL, ports: {Np: E, Nn: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: F, Nn: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: G(Vout), Nn: GND}
]
extrainfo:The circuit is a three-stage ring oscillator using NMOS transistors, each stage comprising an NMOS, a resistor, and a capacitor. The feedback loop is established to create oscillations.

Figure 15.8 Three-stage ring oscillator.

The circuit oscillates only if the frequency-dependent phase shift equals $180^{\circ}$, i.e., if each stage contributes $60^{\circ}$. The frequency at which this occurs is given by

$$
\begin{equation*}
\tan ^{-1} \frac{\omega_{\text {osc }}}{\omega_{0}}=60^{\circ} \tag{15.7}
\end{equation*}
$$

and hence

$$
\begin{equation*}
\omega_{o s c}=\sqrt{3} \omega_{0} \tag{15.8}
\end{equation*}
$$

The minimum voltage gain per stage must be such that the magnitude of the loop gain at $\omega_{o s c}$ is equal to unity:

$$
\begin{equation*}
\frac{A_{0}^{3}}{\left[\sqrt{1+\left(\frac{\omega_{\text {osc }}}{\omega_{0}}\right)^{2}}\right]^{3}}=1 \tag{15.9}
\end{equation*}
$$

It follows from (15.8) and (15.9) that

$$
\begin{equation*}
A_{0}=2 \tag{15.10}
\end{equation*}
$$

In summary, a three-stage ring oscillator requires a low-frequency gain of 2 per stage, and it oscillates at a frequency of $\sqrt{3} \omega_{0}$, where $\omega_{0}$ is the $3-\mathrm{dB}$ bandwidth of each stage.

Let us now examine the waveforms at the three nodes of the oscillator of Fig. 15.8. Since each stage contributes a frequency-dependent phase shift of $60^{\circ}$ as well as a low-frequency signal inversion, the waveform at each node is $240^{\circ}$ (or $120^{\circ}$ ) out of phase with respect to its neighboring nodes (Fig. 15.9). The ability to generate multiple phases is a very useful property of ring oscillators.
image_name:Figure 15.9 Waveforms of a threestage ring oscillator
description:The graph in Figure 15.9 illustrates the waveforms of a three-stage ring oscillator. It is a time-domain waveform graph, showing the voltage at three different nodes of the oscillator over time. The horizontal axis represents time \( t \), while the vertical axis indicates voltage, with three separate waveforms labeled \( V_E \), \( V_F \), and \( V_G \).

Each waveform is sinusoidal, indicating periodic oscillations. The three waveforms are out of phase with each other, specifically showing a phase difference of 120 degrees between each waveform, consistent with the description of a three-stage ring oscillator. This phase difference is a critical characteristic of the oscillator, contributing to its ability to generate multiple phases.

The amplitude of each waveform appears consistent, with no significant increase or decrease over time, indicating stable oscillation. There are no visible annotations or markers indicating specific data points or values on the graph, focusing instead on the qualitative behavior of the waveforms.

Overall, the graph effectively demonstrates the phase relationship and stability of the oscillations in a three-stage ring oscillator, highlighting its capability to maintain consistent out-of-phase waveforms across its nodes.

image_name:Figure 15.10 Linear model of three-stage ring oscillator
description:The diagram labeled "Figure 15.10 Linear model of three-stage ring oscillator" illustrates a linear feedback system designed to model a three-stage ring oscillator. The primary components and their functions are as follows:

1. **Main Components:**
- **Three Amplifiers:** The central part of the system is a series of three amplifiers arranged in a ring configuration. Each amplifier is represented as a triangle, indicating the direction of signal flow.
- **Summing Junction:** At the input, there is a summing junction where the input voltage \( V_{in} \) and the feedback voltage are combined. This is depicted by a circle with a plus sign, indicating positive feedback.
- **Feedback Path:** The output \( V_{out} \) is fed back to the input through a feedback loop, completing the ring structure.

2. **Flow of Information or Control:**
- The input signal \( V_{in} \) is first added to the feedback signal at the summing junction. The resulting signal then passes sequentially through the three amplifiers.
- Each amplifier processes the signal, with the output of one serving as the input to the next, maintaining the direction of flow through the system.
- The final output \( V_{out} \) is taken from the last amplifier and fed back to the summing junction, creating a positive feedback loop.

3. **Labels, Annotations, and Key Indicators:**
- The transfer function of the system is labeled as \( \frac{-A_0^3}{(1 + \frac{s}{\omega_0})^3} \), indicating the gain and frequency response characteristics of the oscillator.
- The negative sign in the transfer function suggests inversion, typical of oscillatory systems to maintain phase shift conditions conducive to oscillation.

4. **Overall System Function:**
- The primary function of this system is to model the behavior of a three-stage ring oscillator. The positive feedback loop ensures that the signal is continuously reinforced, allowing the system to sustain oscillations.
- The arrangement of the amplifiers and the feedback loop is crucial in maintaining the phase conditions necessary for stable oscillation, as suggested by the Barkhausen criterion, which requires the loop gain to be equal to one and the total phase shift around the loop to be 0 or 360 degrees.

This linear model helps in understanding how variations in the gain \( A_0 \) can affect the oscillation conditions, particularly highlighting the impact if \( A_0 \) is not equal to 2, as discussed in the context.

Figure 15.10 Linear model of three-stage ring oscillator.

Amplitude Limiting The natural question at this point is-What happens if in the three-stage ring of Fig. 15.8, $A_{0} \neq 2$ ? We know from Barkhausen's criteria that if $A_{0}<2$, the circuit fails to oscillate, but what if $A_{0}>2$ ? To answer this question, we first model the oscillator by a linear feedback system, as depicted in Fig. 15.10. Note that the feedback is positive (i.e., $V_{\text {out }}$ is added to $V_{i n}$ ) because $H(s)$ in Eq. (15.6) already includes the negative polarity resulting from three inversions in the signal path. The closed-loop transfer function is

$$
\begin{align*}
\frac{V_{\text {out }}(s)}{V_{\text {in }}(s)} & =\frac{\frac{-A_{0}^{3}}{\left(1+s / \omega_{0}\right)^{3}}}{1+\frac{A_{0}^{3}}{\left(1+s / \omega_{0}\right)^{3}}}  \tag{15.11}\\
& =\frac{-A_{0}^{3}}{\left(1+s / \omega_{0}\right)^{3}+A_{0}^{3}} \tag{15.12}
\end{align*}
$$

The denominator of (15.12) can be expanded as

$$
\begin{equation*}
\left(1+\frac{s}{\omega_{0}}\right)^{3}+A_{0}^{3}=\left(1+\frac{s}{\omega_{0}}+A_{0}\right)\left[\left(1+\frac{s}{\omega_{0}}\right)^{2}-\left(1+\frac{s}{\omega_{0}}\right) A_{0}+A_{0}^{2}\right] \tag{15.13}
\end{equation*}
$$

Thus, the closed-loop system exhibits three poles:

$$
\begin{align*}
s_{1} & =\left(-A_{0}-1\right) \omega_{0}  \tag{15.14}\\
s_{2,3} & =\left[\frac{A_{0}(1 \pm j \sqrt{3})}{2}-1\right] \omega_{0} \tag{15.15}
\end{align*}
$$

Since $A_{0}$ itself is positive, the first pole leads to a decaying exponential term: $\exp \left[\left(-A_{0}-1\right) \omega_{0} t\right]$, which can be neglected in the steady state. Figure 15.11 illustrates the locations of the poles for different values of $A_{0}$, revealing that for $A_{0}>2$, the two complex poles exhibit a positive real part and hence give rise to a growing sinusoid. Neglecting the effect of $s_{1}$, we express the output waveform as

$$
\begin{equation*}
V_{\text {out }}(t)=a \exp \left(\frac{A_{0}-2}{2} \omega_{0} t\right) \cos \left(\frac{A_{0} \sqrt{3}}{2} \omega_{0} t\right) \tag{15.16}
\end{equation*}
$$

Thus, if $A_{0}>2$, the exponential envelope grows to infinity.
In practice, as the oscillation amplitude increases, the stages in the signal path experience nonlinearity and eventually "saturation," limiting the maximum amplitude. We may say that the poles begin in the right half plane and eventually move to the imaginary axis to stop the growth. If the small-signal loop
image_name:0 < A_0 < 2
description:The graph presented is a pole-zero plot for a three-stage ring oscillator, illustrating the position of poles for different values of the gain parameter $A_0$. The graph is divided into three separate plots, each corresponding to a specific range of $A_0$: $0 < A_0 < 2$, $A_0 = 2$, and $A_0 > 2$.

1. **Type of Graph and Function:**
- This is a pole-zero plot, which is commonly used in control systems and signal processing to represent the poles and zeros of a transfer function in the complex plane.

2. **Axes Labels and Units:**
- The horizontal axis is labeled with the real part of the complex frequency, denoted as $\sigma$.
- The vertical axis is labeled with the imaginary part of the complex frequency, denoted as $j\omega$.
- The axes do not specify units explicitly, but they are typically in radians per second for frequency.

3. **Overall Behavior and Trends:**
- **For $0 < A_0 < 2$:** The poles are located in the left half of the complex plane, indicating a stable system. The poles are positioned at a negative real value, specifically around $-3\omega_0$.
- **For $A_0 = 2$:** The poles lie on the imaginary axis at $-3\omega_0$, suggesting a marginally stable system.
- **For $A_0 > 2$:** The poles move into the right half of the complex plane, indicating an unstable system where the exponential envelope grows to infinity.

4. **Key Features and Technical Details:**
- The transition of poles from the left half to the right half of the complex plane as $A_0$ increases past 2 is critical. It signifies the onset of instability in the oscillator.
- The pole positions are symmetrically distributed about the real axis, which is typical for oscillatory systems.

5. **Annotations and Specific Data Points:**
- The plot includes markers at $-3\omega_0$ on the real axis for reference.
- The poles are marked with crosses, indicating their positions in the complex plane.

This pole-zero plot effectively illustrates the stability characteristics of the oscillator for different values of the gain parameter, highlighting the critical transition at $A_0 = 2$. The movement of poles from stable to unstable regions as $A_0$ increases is a key feature of this analysis.
image_name:A_0 = 2
description:The graph consists of three separate plots, each representing the pole-zero configuration of a three-stage ring oscillator for different values of the gain parameter $A_0$. The plots are drawn on the complex plane with the horizontal axis labeled as $\sigma$ (real part) and the vertical axis labeled as $j\omega$ (imaginary part). The key features and behavior of each plot are as follows:

1. **Plot for $0 < A_0 < 2$:**
- There are three poles depicted as crosses, all located in the left half of the complex plane.
- The poles are positioned such that their real parts are negative, indicating a stable system.
- The horizontal axis is marked at $-3\omega_0$, suggesting a reference point for the real parts of the poles.

2. **Plot for $A_0 = 2$:**
- The poles are located exactly on the imaginary axis, indicating a marginally stable system.
- This configuration suggests that the system is at the brink of oscillation.
- The poles are positioned symmetrically along the imaginary axis, with no real part.

3. **Plot for $A_0 > 2$:**
- The poles have shifted into the right half of the complex plane, indicating an unstable system.
- The presence of poles with positive real parts suggests that the system will exhibit growing oscillations.
- This configuration is consistent with the context stating that an exponential envelope grows to infinity when $A_0 > 2$.

Overall, the graph illustrates how the pole positions move from a stable configuration to an unstable one as the gain $A_0$ increases, highlighting the transition from stability to oscillation and then to instability in the ring oscillator system.
image_name:A_0 > 2
description:The graph is a pole-zero plot for a three-stage ring oscillator depicted in three different scenarios based on the parameter \( A_0 \). Each scenario is represented on a separate plot, showing the movement of poles as \( A_0 \) changes.

Type of Graph:
- This is a pole-zero plot, commonly used in control systems and signal processing to analyze the stability and behavior of systems.

Axes Labels and Units:
- The horizontal axis represents the real part of the complex frequency, denoted as \( \sigma \).
- The vertical axis represents the imaginary part of the complex frequency, denoted as \( j\omega \).
- Units are typically in radians per second, although not explicitly labeled.

Overall Behavior and Trends:
- **For \( 0 < A_0 < 2 \):**
- The poles are located in the left half of the complex plane, indicating a stable system. The poles are positioned at approximately \( -3\omega_0 \) on the real axis and have imaginary components, suggesting oscillatory behavior with damping.
- **For \( A_0 = 2 \):**
- The poles lie on the imaginary axis, indicating marginal stability. This suggests that the system is at the brink of oscillation without decay or growth.
- **For \( A_0 > 2 \):**
- The poles move to the right half of the complex plane, indicating an unstable system. This suggests that the oscillations will grow without bound unless saturation or non-linear effects intervene.

Key Features and Technical Details:
- The poles' movement from the left to the right half-plane as \( A_0 \) increases demonstrates the transition from stability to instability.
- The critical value \( A_0 = 2 \) serves as a threshold where the system transitions from stable to marginally stable.
- The position \( -3\omega_0 \) on the real axis is a reference point for the poles in the stable and marginally stable scenarios.

Annotations and Specific Data Points:
- The plots are annotated with the conditions \( 0 < A_0 < 2 \), \( A_0 = 2 \), and \( A_0 > 2 \) to indicate the different scenarios.
- The point \( -3\omega_0 \) is marked on the real axis as a reference for the pole locations in each scenario.

Figure 15.11 Poles of three-stage ring oscillator for various values of gain.
gain is greater than unity, the circuit must spend enough time in saturation so that the "average" loop gain is still equal to unity. ${ }^{3}$

#### Example 15.2

Shown in Fig. 15.12 is a differential implementation of the oscillator of Fig. 15.8. What is the maximum voltage swing of each stage?
image_name:Figure 15.12
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: X}
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: Y}
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: X1}
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: Y1}
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: X2}
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: Y2}
name: M1, type: NMOS, ports: {S: P12, D: X, G: X2}
name: M2, type: NMOS, ports: {S: P12, D: Y, G: Y2}
name: M3, type: NMOS, ports: {S: P34, D: X1, G: Y}
name: M4, type: NMOS, ports: {S: P34, D: Y1, G: X}
name: M5, type: NMOS, ports: {S: P56, D: X2, G: Y1}
name: M6, type: NMOS, ports: {S: P56, D: Y2, G: X1}
name: Iss, type: CurrentSource, ports: {Np: P12, Nn: GND}
name: Iss, type: CurrentSource, ports: {Np: P34, Nn: GND}
name: Iss, type: CurrentSource, ports: {Np: P56, Nn: GND}
]
extrainfo:The circuit is a differential three-stage ring oscillator with each stage consisting of a differential pair of NMOS transistors and resistors connected to VDD. The current sources Iss provide biasing for each stage. The waveform shows that the voltage swing at each stage is VDD - R1*ISS.
image_name:V_X, V_Y vs t
description:The graph labeled "V_X, V_Y vs t" is a time-domain waveform illustrating the voltage variations of two signals, V_X and V_Y, over time.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph.

2. **Axes Labels and Units:**
- The horizontal axis represents time (t), though no specific units are marked. The axis is linear, indicating a continuous progression of time.
- The vertical axis represents voltage, with specific reference levels marked as V_DD and V_DD - R_1I_SS.

3. **Overall Behavior and Trends:**
- The graph shows two sinusoidal waveforms, V_X and V_Y, which are out of phase with each other. This indicates oscillatory behavior typical of differential signals in a ring oscillator.
- The waveforms are symmetrical and have consistent amplitude and frequency, suggesting stable oscillation.

4. **Key Features and Technical Details:**
- The peaks of the waveforms reach the level of V_DD, while the troughs reach V_DD - R_1I_SS. This indicates the maximum and minimum voltage swing for the signals.
- The signals cross each other at their midpoint, demonstrating the differential nature of the oscillation.

5. **Annotations and Specific Data Points:**
- The annotations V_DD and V_DD - R_1I_SS indicate the voltage levels corresponding to the maximum and minimum swing of the signals.
- No specific numerical values are provided for the time period or amplitude, but the consistent waveform shape suggests a regular oscillation pattern.

Overall, the graph effectively demonstrates the differential oscillation behavior of the circuit, with V_X and V_Y maintaining consistent amplitude and frequency, indicative of a well-functioning oscillator circuit.

#### Solution

If the gain per stage is well above 2, then the amplitude grows until each differential pair experiences complete switching, that is, until $I_{S S}$ is completely steered to one side every half cycle. As a result, the swing at each node is equal to $I_{S S} R_{1}$. From the waveforms shown in Fig. 15.12, we also observe that each stage is in its high-gain region for only a fraction of the period, (e.g., when $\left|V_{X}-V_{Y}\right|$ is small).

image_name:Figure 15.13
description:This is a ring oscillator circuit using three CMOS inverters. The nodes X, Y, and Z represent the outputs of each inverter stage, showing oscillating waveforms over time.
image_name:Figure 15.13
description:The graph in Figure 15.13 is a time-domain waveform illustrating the behavior of voltages at three nodes (Vx, Vy, Vz) in a ring oscillator circuit composed of three inverters. The x-axis represents time (t) in an unspecified unit, and the y-axis represents voltage (V) for each node, also in an unspecified unit. The time axis is linear, and there are no specific markers or gridlines indicated.

**Overall Behavior and Trends:**
The waveforms for Vx, Vy, and Vz show periodic oscillations, indicating the oscillatory nature of the ring oscillator circuit. Each waveform exhibits a sinusoidal-like pattern with increasing amplitude over time, which is characteristic of the growing oscillations in such circuits. The waveforms are slightly phase-shifted relative to each other due to the propagation delay through the inverters.

**Key Features and Technical Details:**
- The amplitude of each waveform increases until it reaches a steady state, where the voltage swing is maximized.
- The waveforms demonstrate complete switching behavior, as described in the context, where each differential pair experiences full switching.
- The initial small amplitude grows due to noise or disturbances, leading to the observed oscillations.

**Annotations and Specific Data Points:**
- The diagram visually represents the inverters and their connections, labeled as nodes X, Y, and Z, corresponding to the waveforms Vx, Vy, and Vz.
- The horizontal dashed lines in each waveform indicate the trip point voltage, around which the oscillations occur.

This description captures the essential behavior and characteristics of the waveforms in the ring oscillator circuit as depicted in Figure 15.13.

Figure 15.13 Ring oscillator using CMOS inverters.

A simple implementation of ring oscillators that does not require resistors is depicted in Fig. 15.13. Suppose the circuit is released with an initial voltage at each node equal to the trip point of the inverters, $V_{\text {trip }} .{ }^{4}$ With identical stages and no noise in the devices, the circuit would remain in this state indefinitely, ${ }^{5}$ but noise components disturb each node voltage, yielding a growing waveform. The signal eventually exhibits rail-to-rail swings.
image_name:Figure 15.14
description:Figure 15.14 depicts the time-domain waveforms of a ring oscillator circuit with three nodes labeled as $V_X$, $V_Y$, and $V_Z$. The x-axis represents time ($t$), and the y-axis represents voltage levels, specifically between 0 and $V_{DD}$, with no specific units or scale markers shown.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform showing the voltage transitions of a ring oscillator over time.

2. **Axes Labels and Units:**
- The x-axis is labeled as time ($t$), but no units are specified.
- The y-axis indicates voltage levels, ranging from 0 to $V_{DD}$.
- The graph uses a linear scale.

3. **Overall Behavior and Trends:**
- The waveform shows periodic oscillations for each node voltage ($V_X$, $V_Y$, $V_Z$), with each exhibiting a square wave pattern.
- Initially, $V_X$ starts at $V_{DD}$ and then falls to 0, $V_Y$ starts at 0 and rises to $V_{DD}$, and $V_Z$ follows a similar pattern to $V_Y$ but with an additional delay.
- The transitions between high and low states are sharp, indicating a rapid change in voltage levels typical of digital signals.

4. **Key Features and Technical Details:**
- Each transition (from high to low or low to high) occurs after a specific inverter delay, denoted as $T_D$.
- The periodicity of the waveform is determined by the inverter delays, with each node experiencing a delay relative to the previous one.
- The waveform of $V_X$ leads those of $V_Y$ and $V_Z$, with $V_Y$ and $V_Z$ experiencing delays of $T_D$ and $2T_D$, respectively.

5. **Annotations and Specific Data Points:**
- The diagram includes arrows and dashed lines to indicate the inverter delay $T_D$ between the transitions of each waveform.
- There are no numerical values given for $T_D$, but its presence is crucial for understanding the timing sequence of the oscillations.

Overall, the graph illustrates the behavior of a ring oscillator circuit where the oscillation period and the phase relationship between nodes are defined by the inverter delays.

Figure 15.14 Waveforms of ring oscillator when one node is initialized at $V_{D D}$.

Let us now assume that the circuit of Fig. 15.13 begins with $V_{X}=V_{D D}$ (Fig. 15.14). Under this condition, $V_{Y}=0$ and $V_{Z}=V_{D D}$. Thus, when the circuit is released, $V_{X}$ begins to fall to zero (because the first inverter senses a high input), forcing $V_{Y}$ to rise to $V_{D D}$ after one inverter delay, $T_{D}$, and $V_{Z}$ to fall to zero after another inverter delay. The circuit therefore oscillates with a delay of $T_{D}$ between consecutive node voltages, yielding a period of $6 T_{D}$.

The above small-signal and large-signal analyses raise an interesting question. While the small-signal oscillation frequency is given by $A_{0} \sqrt{3} \omega_{0} / 2$ [from Eq. (15.16)], the large-signal value is $1 /\left(6 T_{D}\right)$. Are these two values equal? Not necessarily. After all, $\omega_{0}$ is determined by the small-signal output resistance and capacitance of each inverter near the trip point, whereas $T_{D}$ results from the large-signal, nonlinear

image_name:(a)
description:The circuit is a five-stage single-ended ring oscillator, where each inverter is connected in a loop to form a feedback path.

image_name:(b)
description:The circuit is a four-stage differential ring oscillator. Each op-amp stage is connected in a loop to form a feedback path, enabling oscillation.

Figure 15.15 (a) Five-stage single-ended ring oscillator; (b) four-stage differential ring oscillator.
current drive and capacitances of each stage. In other words, when the circuit is released with all inverters at their trip point, the oscillation begins with a frequency of $\sqrt{3} A_{0} \omega_{0} / 2$, but, as the amplitude grows and the circuit becomes nonlinear, the frequency shifts to $1 /\left(6 T_{D}\right)$ (which is a lower value).

Ring oscillators employing more than three stages are also feasible. The total number of inversions in the loop must be odd so that the circuit does not latch up. For example, as shown in Fig. 15.15(a), a ring can incorporate five inverters, providing a frequency of $1 /\left(10 T_{D}\right)$. On the other hand, the differential implementation can utilize an even number of stages by simply configuring one stage such that it does not invert. Illustrated in Fig. 15.15(b), this flexibility demonstrates another advantage of differential circuits over their single-ended counterparts.

#### Example 15.3

What is the minimum required voltage gain per stage in the four-stage oscillator of Fig. 15.15(b)? How many signal phases are provided by the circuit?

#### Solution

Using a notation similar to that for Fig. 15.8, we have

$$
\begin{equation*}
H(s)=-\frac{A_{0}^{4}}{\left(1+\frac{s}{\omega_{0}}\right)^{4}} \tag{15.17}
\end{equation*}
$$

For the circuit to oscillate, each stage must contribute a frequency-dependent phase shift of $180^{\circ} / 4=45^{\circ}$. The frequency at which this occurs is given by $\tan ^{-1} \omega_{\text {osc }} / \omega_{0}=45^{\circ}$ and hence $\omega_{\text {osc }}=\omega_{0}$. The minimum voltage gain is therefore derived as

$$
\begin{equation*}
\frac{A_{0}}{\sqrt{1+\left(\frac{\omega_{o s c}}{\omega_{0}}\right)^{2}}}=1 \tag{15.18}
\end{equation*}
$$

That is, $A_{0}=\sqrt{2}$. As expected, this value is lower than that required in a three-stage ring.
With $45^{\circ}$ of phase shift per stage, the oscillator provides four phases and their complements. This is illustrated in Fig. 15.16.

The number of stages in a ring oscillator is determined by various requirements, including speed, power dissipation, noise immunity, etc. In most applications, three to five stages provide optimum performance (for differential implementations).
image_name:Figure 15.16
description:The graph in Figure 15.16 is a time-domain waveform representing the output voltages of a ring oscillator with differential stages. The x-axis is labeled as time \( t \), and the y-axis represents voltage levels, although specific units are not provided.

1. **Type of Graph and Function:**
- This is a time-domain waveform illustrating the voltage levels at different nodes in a ring oscillator circuit.

2. **Axes Labels and Units:**
- The x-axis is labeled \( t \), representing time, and the y-axis represents voltage levels at various nodes (\( V_{X1}, V_{Y1}, V_{Y2}, \) etc.). Specific voltage units are not indicated.

3. **Overall Behavior and Trends:**
- The waveforms exhibit square wave behavior with distinct high and low states, indicating complete switching between two voltage levels.
- The waveforms are periodic, with each waveform showing a similar pattern shifted in time relative to the others.

4. **Key Features and Technical Details:**
- Each waveform represents the voltage at a specific node in the oscillator, with nodes \( V_{X1}, V_{Y1}, V_{Y2}, V_{X2}, V_{X3}, V_{Y3}, V_{X4}, \) and \( V_{Y4} \) shown.
- The time delay \( T_D \) between the transitions of consecutive waveforms is marked, indicating the phase shift between stages.
- The graph illustrates the phase relationship between the outputs of different stages, with each stage providing a 45-degree phase shift.

5. **Annotations and Specific Data Points:**
- The time delay \( T_D \) is annotated on the graph, highlighting the temporal separation between the waveforms.
- The waveforms are drawn in alternating bold and light lines to differentiate between complementary outputs, indicating differential signaling.

#### Example 15.4

Determine the maximum voltage swings and the minimum supply voltage of a ring oscillator incorporating differential pairs with resistive loads (e.g., as in Fig. 15.12) if no transistor must enter the triode region. Assume that each stage experiences complete switching.

#### Solution

Figure 15.17(a) shows two stages in cascade. If each stage experiences complete switching, then each drain voltage, e.g., $V_{X}$ or $V_{Y}$, varies between $V_{D D}$ and $V_{D D}-I_{S S} R_{P}$. Thus, when $M_{1}$ is fully on, its gate and drain voltages are equal to $V_{D D}$ and $V_{D D}-I_{S S} R_{P}$, respectively. For this transistor to remain in saturation, we have $I_{S S} R_{P} \leq V_{T H}$, i.e., the peak-to-peak swing at each drain must not exceed $V_{T H}$.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: d1, G: Y}
name: M2, type: NMOS, ports: {S: P, D: d2, G: X}
name: M3, type: NMOS, ports: {S: P1, D: X, G: Vip}
name: M4, type: NMOS, ports: {S: P1, D: Y, G: Vin}
name: M5, type: NMOS, ports: {S: GND, D: P1, G: Vb}
name: M6, type: NMOS, ports: {S: GND, D: P, G: Vb}
name: RP, type: Resistor, value: RP, ports: {N1: VDD, N2: X}
name: RP, type: Resistor, value: RP, ports: {N1: VDD, N2: Y}
name: RP, type: Resistor, value: RP, ports: {N1: VDD, N2: d1}
name: RP, type: Resistor, value: RP, ports: {N1: VDD, N2: d2}
]
extrainfo:The circuit in Figure 15.17(a) is a differential amplifier with NMOS transistors M1 to M6 and load resistors RP. The circuit is biased with a current ISS and uses a voltage Vb for biasing the gates of M5 and M6. The diagram shows the voltage swings at nodes X, Y, and P, indicating the operation of the amplifier stages.
image_name:(b)
description:The graph in Figure 15.17(b) is a time-domain waveform plot showing the behavior of voltages $V_1$, $V_2$, and $V_P$ over time. The x-axis represents time, denoted as $t$, and the y-axis represents voltage levels, although specific units are not labeled, we can infer they are in volts.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform plot illustrating voltage levels over time.

2. **Axes Labels and Units:**
- **X-axis:** Time ($t$), units not specified.
- **Y-axis:** Voltage levels ($V_1$, $V_2$, $V_P$), units not specified but likely in volts.

3. **Overall Behavior and Trends:**
- The waveform shows a crossing pattern where $V_1$ and $V_2$ intersect.
- $V_1$ and $V_2$ appear to be sinusoidal or similar, with one increasing while the other decreases, indicative of complementary or differential signals.
- $V_P$ is shown as a dashed line, remaining relatively constant or having less variation compared to $V_1$ and $V_2$.

4. **Key Features and Technical Details:**
- **Intersection Point:** $V_1$ and $V_2$ intersect at a central point, indicating a phase crossover or balance point.
- The amplitude of $V_1$ and $V_2$ suggests a symmetrical swing around a central voltage level, typical in differential signaling.
- $V_P$ maintains a steady level, possibly indicating a reference or bias voltage.

5. **Annotations and Specific Data Points:**
- No specific numerical values or annotations are provided on the graph, but the intersection and relative levels are the main features.
- The graph visually emphasizes the crossing and differential nature of $V_1$ and $V_2$, with $V_P$ as a stabilizing reference.
image_name:(c)
description:The graph in Figure 15.17(c) is a time-domain waveform depicting the voltage variations at three different nodes, labeled $V_X$, $V_Y$, and $V_P$, over time. The horizontal axis represents time ($t$) without specific units, indicating a continuous observation of voltage changes. The vertical axis represents voltage levels, though specific units are not provided.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph showing voltage variations over time.

2. **Axes Labels and Units:**
- **Horizontal Axis:** Represents time ($t$), no specific units given.
- **Vertical Axis:** Represents voltage levels at nodes $V_X$, $V_Y$, and $V_P$, no specific units given.

3. **Overall Behavior and Trends:**
- The waveforms for $V_X$ and $V_Y$ appear as sinusoidal or periodic oscillations with a consistent frequency and amplitude, indicating complete switching at these nodes.
- The waveform for $V_P$ shows a different pattern, suggesting a steady or less dynamic change compared to $V_X$ and $V_Y$. This reflects the behavior of the common source node in a differential pair, as described in the context.

4. **Key Features and Technical Details:**
- The waveforms for $V_X$ and $V_Y$ have a clear periodic nature, likely corresponding to the switching actions of transistors $M_1$ and $M_2$.
- The waveform for $V_P$ is smoother and less oscillatory, indicating its role as a common source node, which should remain relatively stable to maintain the tail transistor in saturation.

5. **Annotations and Specific Data Points:**
- There are no specific annotations or numerical values provided on the graph. However, the relative positions and behaviors of the waveforms provide insight into the circuit's operation, as discussed in the context.

Figure 15.17

How is the minimum supply voltage determined? If $V_{D D}$ is lowered, the voltage at the common source node of each differential pair, e.g., $V_{P}$ in Fig. 15.17(a), falls, eventually driving the tail transistor into the triode region. We must therefore calculate $V_{P}$ for the worst case, noting that $V_{P}$ does vary with time because $M_{1}$ and $M_{2}$ carry unequal currents when the input difference becomes large.

Now consider the stand-alone circuit of Fig. 15.17(b), assuming that the inputs vary between $V_{D D}$ and $V_{D D}-$ $I_{S S} R_{P}$. How does $V_{P}$ vary? When the gate voltage of $M_{1}, V_{1}$, is equal to $V_{D D}$ and $M_{1}$ carries all of $I_{S S}$,

$$
\begin{equation*}
V_{P}=V_{D D}-\sqrt{\frac{2 I_{S S}}{\mu_{n} C_{o x}(W / L)_{1,2}}}-V_{T H} \tag{15.19}
\end{equation*}
$$

As $V_{1}$ falls and $V_{2}$ rises, so does $V_{P}$ because, so long as $M_{2}$ is off, $M_{1}$ operates as a source follower. When the difference between $V_{1}$ and $V_{2}$ reaches $\sqrt{2}\left(V_{G S, e q}-V_{T H}\right)$, where $V_{G S, e q}$ denotes the equilibrium overdrive of each transistor, $M_{2}$ turns on. To calculate $V_{P}$ after this point, we note that $I_{D 1}+I_{D 2}=I_{S S}, V_{G S 1}=V_{1}-V_{P}$, and $V_{G S 2}=V_{2}-V_{P}$. Thus,

$$
\begin{equation*}
\frac{1}{2} \mu_{n} C_{o x}\left(\frac{W}{L}\right)_{1,2}\left(V_{1}-V_{P}-V_{T H}\right)^{2}+\frac{1}{2} \mu_{n} C_{o x}\left(\frac{W}{L}\right)_{1,2}\left(V_{2}-V_{P}-V_{T H}\right)^{2}=I_{S S} \tag{15.20}
\end{equation*}
$$

Expanding the quadratic terms and rearranging the result, we have

$$
\begin{equation*}
2 V_{P}^{2}-2\left(V_{1}-V_{T H}+V_{2}-V_{T H}\right) V_{P}+\left(V_{1}-V_{T H}\right)^{2}+\left(V_{2}-V_{T H}\right)^{2}-\frac{2 I_{S S}}{\mu_{n} C_{o x}(W / L)_{1,2}}=0 \tag{15.21}
\end{equation*}
$$

It follows that

$$
\begin{equation*}
V_{P}=\frac{1}{2}\left[V_{1}+V_{2}-2 V_{T H} \pm \sqrt{-\left(V_{1}-V_{2}\right)^{2}+\frac{4 I_{S S}}{\mu_{n} C_{o x}(W / L)_{1,2}}}\right] \tag{15.22}
\end{equation*}
$$

If $V_{1}$ and $V_{2}$ vary differentially, they can be expressed as $V_{1}=V_{C M}+\Delta V$ and $V_{2}=V_{C M}-\Delta V$, where $V_{C M}=V_{D D}-I_{S S} R_{P} / 2$, yielding

$$
\begin{equation*}
V_{P}=V_{C M}-V_{T H} \pm \frac{1}{2} \sqrt{-(2 \Delta V)^{2}+\frac{4 I_{S S}}{\mu_{n} C_{o x}(W / L)_{1,2}}} \tag{15.23}
\end{equation*}
$$

This expression reveals why node $P$ is considered a virtual ground in small-signal operation: if $|\Delta V|$ is much less than the maximum overdrive voltage, then $V_{P}$ is relatively constant. Since the term under the square root reaches a maximum for $\Delta V=0$ (equilibrium condition),

$$
\begin{equation*}
V_{P, \min }=V_{C M}-V_{T H}-\sqrt{\frac{I_{S S}}{\mu_{n} C_{o x}(W / L)_{1,2}}} \tag{15.24}
\end{equation*}
$$

As expected, the last term in (15.24) represents the overdrive voltage of each transistor in equilibrium (where $I_{D 1}=I_{D 2}=I_{S S} / 2$ ).

Figure 15.17(c) shows typical waveforms in the oscillator. Note that $V_{P}$ varies at twice the oscillation frequency. This property is sometimes exploited in "frequency doublers."

To determine the minimum supply voltage, we write $V_{P, \text { min }} \geq V_{I S S}$, where $V_{I S S}$ denotes the minimum required voltage across $I_{S S}$. Thus,

$$
\begin{equation*}
V_{D D}-\frac{R_{P} I_{S S}}{2}-V_{T H}-\sqrt{\frac{I_{S S}}{\mu_{n} C_{o x}(W / L)_{1,2}}} \geq V_{I S S} \tag{15.25}
\end{equation*}
$$

and

$$
\begin{equation*}
V_{D D} \geq V_{I S S}+V_{T H}+\sqrt{\frac{I_{S S}}{\mu_{n} C_{o x}(W / L)_{1,2}}}+\frac{R_{P} I_{S S}}{2} \tag{15.26}
\end{equation*}
$$

The terms on the right are the voltage headroom consumed by a current source, one threshold voltage, the equilibrium overdrive, and half of the swing at each node.

In CMOS technologies lacking high-quality resistors, the implementation of Fig. 15.17(a) must be modified. While a PMOS transistor operating in the deep triode region can serve as the load [Fig. 15.18(a)], the gate voltage must be set so as to define the on-resistance accurately. Alternatively, a diodeconnected load can be utilized [Fig. 15.18(b)], but at the cost of one threshold voltage in the headroom. Figure 15.18(c) shows a more efficient load where an NMOS source follower is inserted between the drain and gate of each PMOS transistor. With the output sensed at nodes $X$ and $Y, M_{3}$ and $M_{4}$ consume only a voltage headroom equal to $\left|V_{D S 3,4}\right|$. If $V_{G S 5} \approx V_{T H 3}$, then $M_{3}$ operates at the edge of the triode region and the small-signal resistance of the load is roughly equal to $1 / g_{m 3}$ (with the assumption that $\lambda=\gamma=0$ ) (Problem 15.4).
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: Voutp, G: Vip}
name: M2, type: NMOS, ports: {S: P, D: Voutn, G: Vin}
name: M3, type: PMOS, ports: {S: VDD, D: Voutp, G: Vb}
name: M4, type: PMOS, ports: {S: VDD, D: Voutn, G: Vb}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential stage using PMOS loads with an NMOS current source ISS. M1 and M2 are NMOS transistors configured as differential pairs. M3 and M4 are PMOS transistors used as loads. The output is taken at Vout. The PMOS transistors M3 and M4 have their gates connected to a bias voltage Vb.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: P, D: Voutp, G: Vip}
name: M2, type: NMOS, ports: {S: P, D: Voutn, G: Vin}
name: M3, type: PMOS, ports: {S: VDD, D: Voutp, G: Vb}
name: M4, type: PMOS, ports: {S: VDD, D: Voutn, G: Vb}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with PMOS loads, using NMOS transistors M1 and M2 for input differential pair and PMOS transistors M3 and M4 as active loads. The output is taken from Vout. ISS is the tail current source providing biasing for the NMOS pair.
image_name:(c)
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: Vip}
name: M2, type: NMOS, ports: {S: P, D: Y, G: Vin}
name: M3, type: PMOS, ports: {S: VDD, D: X, G: g3s5}
name: M4, type: PMOS, ports: {S: VDD, D: Y, G: g4s6}
name: M5, type: NMOS, ports: {S: g3s5, D: VDD, G: X}
name: M6, type: NMOS, ports: {S: g4s6, D: VDD, G: Y}
name: ISS, type: CurrentSource, ports: {Np: g3s5, Nn: GND}
name: ISS, type: CurrentSource, ports: {Np: g4s6, Nn: GND}
]
extrainfo:The circuit is a differential stage with PMOS loads, where NMOS source followers (M5 and M6) are inserted between the drain and gate of each PMOS transistor (M3 and M4). This configuration improves the load efficiency by reducing the voltage headroom consumed by M3 and M4. The circuit outputs are sensed at nodes X and Y, and the load exhibits a smaller time constant due to the source follower.

Figure 15.18 Differential stages using PMOS loads.
The load of Fig. 15.18(c) exhibits another interesting property as well. Since the gate-source capacitance of $M_{3}$ is driven by the source follower, the time constant associated with the load is smaller than that of a diode-connected transistor. Also, the finite output resistance of the follower may yield an inductive behavior for the load (Problem 15.5).

## 15.3 ■ LC Oscillators

Monolithic inductors have become common in CMOS technologies, making it possible to design oscillators based on passive resonant circuits. Before delving into such oscillators, it is instructive to review the basic properties of RLC circuits.

### 15.3.1 Basic Concepts

As shown in Fig. 15.19(a), an inductor $L_{1}$ placed in parallel with a capacitor $C_{1}$ resonates at a frequency $\omega_{\text {res }}=1 / \sqrt{L_{1} C_{1}}$. At this frequency, the impedances of the inductor, $j L_{1} \omega_{\text {res }}$, and the capacitor, $1 /\left(j C_{1} \omega_{\text {res }}\right)$, are equal and opposite, thereby yielding an infinite impedance. We say that the circuit has an infinite quality factor, $Q$. In practice, inductors (and capacitors) suffer from resistive components. For example, the series resistance of the metal wire used in the inductor can be modeled as shown in Fig. 15.19(b). We define the $Q$ of the inductor as $L_{1} \omega / R_{S}$. For this circuit, the reader can show that the equivalent impedance is given by

$$
\begin{equation*}
Z_{e q}(s)=\frac{R_{S}+L_{1} s}{1+L_{1} C_{1} s^{2}+R_{S} C_{1} s} \tag{15.27}
\end{equation*}
$$

image_name:(a)
description:
[
name: L1, type: Inductor, value: L1, ports: {N1: X, N2: Y}
name: C1, type: Capacitor, value: C1, ports: {Np: Y, Nn: X}
]
extrainfo:The circuit in diagram (a) is an ideal LC tank circuit with an inductor L1 and a capacitor C1 connected in parallel between nodes X and Y.
image_name:(b)
description:
[
name: L1, type: Inductor, value: L1, ports: {N1: Y, N2: r_l}
name: C1, type: Capacitor, value: C1, ports: {Np: Y, Nn: X}
name: Rs, type: Resistor, value: Rs, ports: {N1: Y, N2: r_l}
]
extrainfo:The circuit diagram (b) represents a realistic LC tank with a series resistor Rs modeling the series resistance of the inductor L1. The circuit is connected between nodes Y and X.
Figure 15.19 (a) Ideal and (b) realistic LC tanks.
and hence,

$$
\begin{equation*}
\left|Z_{e q}(s=j \omega)\right|^{2}=\frac{R_{S}^{2}+L_{1}^{2} \omega^{2}}{\left(1-L_{1} C_{1} \omega^{2}\right)^{2}+R_{S}^{2} C_{1}^{2} \omega^{2}} \tag{15.28}
\end{equation*}
$$

That is, the impedance does not go to infinity at any $s=j \omega$. We say that the circuit has a finite $Q$. The magnitude of $Z_{e q}$ in (15.28) reaches a peak in the vicinity of $\omega=1 / \sqrt{L_{1} C_{1}}$, but the actual resonance frequency has some dependency on $R_{S}$.

The circuit of Fig. 15.19(b) can be transformed to an equivalent topology that more easily lends itself to analysis and design. To this end, we first consider the series combination shown in Fig. 15.20(a). For a narrow frequency range, it is possible to convert the circuit to the parallel configuration of Fig. 15.20(b).
image_name:(a)
description:
[
name: L1, type: Inductor, value: L1, ports: {N1: Y, N2: r_l}
name: RS, type: Resistor, value: RS, ports: {N1: X, N2: r_l}
]
extrainfo:The circuit diagram (a) shows a series combination of an inductor L1, a resistor rL, and another resistor RS. The nodes X and Y are the input and output nodes of the circuit.
image_name:(b)
description:
[
name: LP, type: Inductor, value: LP, ports: {N1: X, N2: Y}
name: RP, type: Resistor, value: RP, ports: {N1: X, N2: Y}
]
extrainfo:The circuit in diagram (b) is a parallel LC circuit with an inductor LP and a resistor RP connected between nodes X and Y. This circuit is equivalent to the series circuit in diagram (a) for a narrow frequency range.

Figure 15.20 Conversion of a series combination to a parallel combination.

For the two impedances to be equivalent,

$$
\begin{equation*}
L_{1} s+R_{S}=\frac{R_{P} L_{P} s}{R_{P}+L_{P} s} \tag{15.29}
\end{equation*}
$$

Considering only the steady-state response, we assume that $s=j \omega$ and rewrite (15.29) as

$$
\begin{equation*}
\left(L_{1} R_{P}+L_{P} R_{S}\right) j \omega+R_{S} R_{P}-L_{1} L_{P} \omega^{2}=R_{P} L_{P} j \omega \tag{15.30}
\end{equation*}
$$

This relationship must hold for all values of $\omega$ (in a narrow range), dictating that

$$
\begin{align*}
L_{1} R_{P}+L_{P} R_{S} & =R_{P} L_{P}  \tag{15.31}\\
R_{S} R_{P}-L_{1} L_{P} \omega^{2} & =0 \tag{15.32}
\end{align*}
$$

Calculating $R_{P}$ from the latter and substituting in the former, we have

$$
\begin{equation*}
L_{P}=L_{1}\left(1+\frac{R_{S}^{2}}{L_{1}^{2} \omega^{2}}\right) \tag{15.33}
\end{equation*}
$$

Recall that $L_{1} \omega / R_{S}=Q$, a value typically greater than 3 for monolithic inductors. Thus,

$$
\begin{equation*}
L_{P} \approx L_{1} \tag{15.34}
\end{equation*}
$$

and

$$
\begin{align*}
R_{P} & \approx \frac{L_{1}^{2} \omega^{2}}{R_{S}}  \tag{15.35}\\
& \approx Q^{2} R_{S} \tag{15.36}
\end{align*}
$$

In other words, the parallel network has the same reactance but a resistance $Q^{2}$ times the series resistance. This concept holds valid for a first-order RC network as well if the $Q$ of the series combination is defined as $1 /(C \omega) / R_{S}$.
image_name:Figure 15.21 Conversion of a tank to three parallel components.
description:
[
name: L1, type: Inductor, value: L1, ports: {N1: Y, N2: r_l}
name: C1, type: Capacitor, value: C1, ports: {Np: Y, Nn: X}
name: RS, type: Resistor, value: RS, ports: {N1: X, N2: r_L}
'name': 'LP', 'type': 'Inductor', 'value': 'LP', 'ports': {'N1': 'Y', 'N2': 'X'
'name': 'RP', 'type': 'Resistor', 'value': 'RP', 'ports': {'N1': 'Y', 'N2': 'X'
'name': 'CP', 'type': 'Capacitor', 'value': 'CP', 'ports': {'Np': 'Y', 'Nn': 'X'
]
extrainfo:The circuit diagram illustrates the conversion of a series LC tank circuit with a resistor into an equivalent parallel LC tank circuit with a resistor. The left side shows the series configuration with L1, C1, RS, and rL, while the right side shows the parallel configuration with LP, CP, and RP. This transformation is used to simplify the analysis of the circuit at its resonance frequency.

Figure 15.21 Conversion of a tank to three parallel components.

The above transformation allows the conversion illustrated in Fig. 15.21, where $C_{P}=C_{1}$. The equivalence of course breaks down as $\omega$ departs substantially from the resonance frequency. The insight gained from the parallel combination is that at $\omega_{1}=1 / \sqrt{L_{p} C_{p}}$, the tank reduces to a simple resistor; i.e., the phase difference between the voltage and current of the tank drops to zero. Plotting the magnitude of the tank impedance versus frequency [Fig. 15.22(a)], we note that the behavior is inductive for $\omega<\omega_{1}$ and capacitive for $\omega>\omega_{1}$. We then surmise that the phase of the impedance is positive for $\omega<\omega_{1}$ and negative for $\omega>\omega_{1}$ [Fig. 15.22(b)]. These observations prove useful in studying LC oscillators. (Why do we expect the phase shift to approach $+90^{\circ}$ at very low frequencies and $-90^{\circ}$ at very high frequencies?)
image_name:(a)
description:The graph labeled (a) represents the magnitude of the impedance (|Z|) of an LC tank circuit as a function of frequency (ω). The x-axis is labeled with angular frequency (ω), and the y-axis represents the magnitude of the impedance. The graph shows a peak at a specific frequency, ω₁, indicating resonance. The magnitude increases sharply as it approaches ω₁ from both sides and reaches a maximum at ω₁, then decreases symmetrically. Below ω₁, the behavior is inductive, and above ω₁, it is capacitive, as inferred from the context.

The graph labeled (b) illustrates the phase angle of the impedance (∠Z) versus frequency (ω). The x-axis again represents the frequency, while the y-axis shows the phase angle in degrees. The phase angle starts at +90° at very low frequencies, indicating a predominantly inductive behavior. As the frequency increases towards ω₁, the phase angle decreases, crossing zero at ω₁, where the impedance is purely resistive. Beyond ω₁, the phase angle continues to decrease, approaching -90° at very high frequencies, indicating a predominantly capacitive behavior. This transition from +90° to -90° is smooth and continuous, reflecting the change from inductive to capacitive nature of the impedance as frequency increases.
image_name:(b)
description:The graph labeled (b) depicts the phase of the impedance (∠Z) of an LC tank as a function of frequency (ω). This is a phase-frequency plot, which is a type of Bode plot.

1. **Axes Labels and Units:**
- The horizontal axis represents frequency (ω), typically in radians per second (rad/s).
- The vertical axis represents the phase of the impedance (∠Z), measured in degrees.

2. **Overall Behavior and Trends:**
- The phase starts at +90° for very low frequencies, indicating inductive behavior.
- As frequency increases, the phase decreases, crossing the zero-degree line at a specific frequency, denoted as ω₁.
- Beyond ω₁, the phase continues to decrease and approaches -90° at very high frequencies, indicating capacitive behavior.

3. **Key Features and Technical Details:**
- The frequency ω₁ is a critical point where the phase crosses zero degrees. This is typically the resonant frequency of the LC tank circuit.
- The transition from +90° to -90° indicates a shift from inductive to capacitive behavior as frequency increases past ω₁.
- The phase shift is smooth and continuous, reflecting the natural behavior of LC circuits.

4. **Annotations and Specific Data Points:**
- There are no additional annotations or markers other than the phase values at low and high frequencies (+90° and -90°, respectively) and the zero crossing at ω₁.

This phase response is essential for understanding the behavior of LC oscillators, particularly in determining stability and frequency response characteristics.

Figure 15.22 (a) Magnitude and (b) phase of the impedance of an LC tank as a function of frequency.

Let us now consider the "tuned" stage of Fig. 15.23(a), where an LC tank operates as the load. At resonance, $j L_{p} \omega=1 /\left(j C_{p} \omega\right)$ and the voltage gain equals $-g_{m 1} R_{P}$. (Note that the gain of the circuit is very small at frequencies near zero.) Does this circuit oscillate if the output is connected to the input [Fig. 15.23(b)]? At resonance, the total phase shift around the loop is equal to $180^{\circ}$ (rather than $360^{\circ}$ ). Also, from Fig. 15.22(b), the frequency-dependent phase shift of the tank never reaches $180^{\circ}$. Thus, the circuit does not oscillate.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: LP, type: Inductor, value: LP, ports: {N1: VDD, N2: Vout}
name: RP, type: Resistor, value: RP, ports: {N1: VDD, N2: Vout}
name: CP, type: Capacitor, value: CP, ports: {Np: VDD, Nn: Vout}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a tuned gain stage with an NMOS transistor M1, a parallel LC tank circuit (LP and CP), and a resistor RP. The output node is Vout. The circuit is powered by a voltage source VDD.

image_name:(b)
description:
[
name: LP, type: Inductor, value: LP, ports: {N1: VDD, N2: Vout}
name: RP, type: Resistor, value: RP, ports: {N1: VDD, N2: Vout}
name: CP, type: Capacitor, value: CP, ports: {Np: VDD, Nn: Vout}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vout}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a tuned gain stage with an NMOS transistor M1, a parallel LC tank circuit (LP and CP), and a resistor RP. The output node is Vout. The circuit is powered by a voltage source VDD.

Figure 15.23 (a) Tuned gain stage; (b) stage of (a) in feedback.
Before modifying the circuit for oscillatory behavior, let us observe another interesting property of the gain stage of Fig. 15.23(a) that distinguishes it from a common-source topology using a resistive load. Suppose, as shown in Fig. 15.24, the stage is biased at a drain current $I_{1}$. If the series resistance of $L_{p}$ is small, the dc level of $V_{\text {out }}$ is close to $V_{D D}$. How does $V_{\text {out }}$ vary if a small sinusoidal voltage at the resonance frequency is applied to the input? We expect $V_{\text {out }}$ to be an inverted sinusoid with an average value near $V_{D D}$ because the inductor cannot sustain a large dc drop. In other words, if the average value of $V_{\text {out }}$ deviates significantly from $V_{D D}$, then the inductor series resistance must carry an average current greater than $I_{1}$. Thus, the peak output level in fact exceeds the supply voltage, an important and often useful attribute of the LC load. For example, with proper design, the output peak-to-peak swing can be larger than $V_{D D}$.
image_name:Figure 15.24
description:The graph in Figure 15.24 illustrates the output signal levels in a tuned stage of an LC oscillator. The diagram is composed of two parts: a schematic on the left and a waveform on the right.

1. **Type of Graph and Function:**
- The graph on the right is a time-domain waveform representing the output voltage, \( V_{\text{out}} \), of the LC circuit.

2. **Axes Labels and Units:**
- The horizontal axis represents time (though it is not explicitly labeled, it is implied by the waveform nature).
- The vertical axis represents voltage, \( V_{\text{out}} \), with a dotted line indicating the DC supply voltage, \( V_{DD} \).

3. **Overall Behavior and Trends:**
- The waveform is sinusoidal, indicating oscillatory behavior typical of an LC circuit.
- The sinusoid oscillates above and below the DC supply voltage, \( V_{DD} \), suggesting that the peak-to-peak amplitude of the output exceeds \( V_{DD} \).
- This behavior highlights the ability of the LC circuit to generate output voltages larger than the supply voltage due to resonance and energy storage in the inductor and capacitor.

4. **Key Features and Technical Details:**
- The waveform shows a consistent oscillation with no visible distortion, indicating stable operation at resonance.
- The average value of the waveform is close to \( V_{DD} \), which is typical as the inductor cannot sustain a large DC drop.
- The peak and trough of the waveform exceed \( V_{DD} \), demonstrating the circuit's capability to achieve a peak-to-peak swing larger than the supply voltage.

5. **Annotations and Specific Data Points:**
- The dotted line represents the DC supply voltage, \( V_{DD} \), serving as a reference level for the waveform.
- No specific numerical values are provided for the amplitude or frequency of the oscillation, but the qualitative behavior is clear from the sinusoidal waveform and its relation to \( V_{DD} \).

Figure 15.24 Output signal levels in a tuned stage.
We now study two types of LC oscillators.

### 15.3.2 Cross-Coupled Oscillator

Suppose we place two stages of Fig. 15.23(a) in a cascade, as depicted in Fig. 15.25. While similar to the topology of Fig. 15.5, this configuration does not latch up because its low-frequency gain is very small. Furthermore, at resonance, the total phase shift around the loop is zero because each stage contributes zero frequency-dependent phase shift. That is, if $g_{m 1} R_{P} g_{m 2} R_{P} \geq 1$, then the loop oscillates. Note that $V_{X}$ and $V_{Y}$ are differential waveforms. (Why?)
image_name:Figure 15.25
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: Vout}
name: M2, type: NMOS, ports: {S: GND, D: Y(Vout), G: X}
name: RP1, type: Resistor, value: RP, ports: {N1: VDD, N2: X}
name: RP2, type: Resistor, value: RP, ports: {N1: VDD, N2: Y}
name: CP1, type: Capacitor, value: CP, ports: {Np: VDD, Nn: X}
name: CP2, type: Capacitor, value: CP, ports: {Np: VDD, Nn: Y}
name: LP1, type: Inductor, value: LP, ports: {N1: VDD, N2: X}
name: LP2, type: Inductor, value: LP, ports: {N1: VDD, N2: Y}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit consists of two cascaded tuned amplifier stages using NMOS transistors M1 and M2. Each stage is connected to a parallel LC tank circuit (RP, LP, CP) for tuning. Vout is the output node, and the circuit is powered by VDD. The configuration is designed to prevent latch-up by maintaining a low-frequency gain and ensuring zero phase shift at resonance.

Figure 15.25 Two tuned stages in a feedback loop.

#### Example 15.5

Sketch the open-loop voltage gain and phase of the circuit shown in Fig. 15.25. Neglect transistor capacitances.

#### Solution

The magnitude of the transfer function has a shape similar to that in Fig. 15.22(a), but with a sharper rise and fall because it results from the product of those of the two stages. The total phase at low frequencies is given by signal inversion by each common-source stage plus a $90^{\circ}$ phase shift due to each tank. A similar behavior occurs at high frequencies. The gain and phase are sketched in Fig. 15.26. From these plots, the reader can prove that the circuit cannot oscillate at any other frequency.
image_name:|H1|
description:The graph labeled "|H1|" is part of a set of Bode plots illustrating the magnitude and phase characteristics of a transfer function. The specific graph for "|H1|" is a magnitude plot, showing the response of a single stage in the system.

1. **Type of Graph and Function:**
- This is a Bode plot representing the magnitude of a transfer function, specifically for a single stage labeled as "|H1|".

2. **Axes Labels and Units:**
- The horizontal axis represents angular frequency (ω) in radians per second, marked as ω₁ at the center.
- The vertical axis represents the magnitude of the transfer function |H1|, likely in decibels (dB), although specific units are not labeled.

3. **Overall Behavior and Trends:**
- The graph shows a resonant peak at frequency ω₁, indicating a bandpass characteristic.
- The magnitude rises sharply to a peak at ω₁ and falls symmetrically on either side, suggesting a narrow bandwidth.

4. **Key Features and Technical Details:**
- The peak at ω₁ is the most significant feature, indicating the frequency at which the stage has maximum gain.
- The sharp rise and fall around ω₁ suggest a high Q-factor, typical of resonant circuits.

5. **Annotations and Specific Data Points:**
- The graph does not have specific numerical annotations or markers, but the symmetry around ω₁ is a critical aspect.

This description of "|H1|" is part of a composite analysis where multiple stages are combined to determine the overall system behavior, as shown in subsequent plots where |H2| and the product |H1 H2| are also analyzed alongside their phase characteristics.
image_name:|H2|
description:The graph labeled |H2| is part of a series of plots illustrating the magnitude and phase characteristics of a two-stage system. The magnitude plot of |H2| is a Bode plot, showing frequency response with the magnitude |H2| on the vertical axis and angular frequency \( \omega \) on the horizontal axis. Both axes are likely on a logarithmic scale, which is typical for Bode plots. The graph shows a peak at a specific frequency \( \omega_1 \), indicating a resonant frequency where the magnitude is maximized. This peak is sharp, suggesting a high Q-factor, typical of LC circuits.

In the phase plot for |H2|, the vertical axis represents phase in degrees, ranging from +90° to -90°, while the horizontal axis is again the angular frequency \( \omega \). The phase starts at +90° at low frequencies, transitions through 0° at the resonant frequency \( \omega_1 \), and approaches -90° at high frequencies. This indicates a phase shift characteristic of a bandpass filter centered around \( \omega_1 \).

Key features include:
- A sharp peak in the magnitude plot at \( \omega_1 \), indicating resonance.
- A phase shift from +90° to -90° through the resonant frequency \( \omega_1 \).

The combined magnitude plot |H1H2| shows an even sharper peak at \( \omega_1 \), resulting from the product of two similar resonant responses. The phase plot for the product |H1H2| shows a total phase shift from +180° to -180°, indicating the cumulative effect of the two stages in the system.
image_name:|H1H2|
description:The graph consists of two main parts: magnitude plots and phase plots for the transfer functions \(|H_1|\), \(|H_2|\), and their product \(|H_1H_2|\).

Magnitude Plots:
1. **\(|H_1|\) and \(|H_2|\):**
- Both plots show a peak at frequency \(\omega_1\), indicating resonance.
- The shape is bell-like, with a sharp rise and fall around \(\omega_1\), suggesting a narrow bandwidth.
- The x-axis represents frequency \(\omega\), and the scale is likely logarithmic due to typical convention, though not explicitly marked.

2. **\(|H_1H_2|\):**
- The product of \(|H_1|\) and \(|H_2|\) results in a similar bell-shaped curve but with a sharper peak at \(\omega_1\).
- This indicates that the combined effect of both stages results in a more pronounced resonance at the same frequency.

Phase Plots:
1. **\(\angle H_1\) and \(\angle H_2\):**
- Both start at +90° at low frequencies and transition to -90° at high frequencies.
- This indicates a phase shift of 180° across the frequency range, centered around \(\omega_1\).

2. **\(\angle H_1H_2\):**
- The combined phase plot starts at +180° and shifts to -180° as frequency increases, showing a total phase shift of 360°.
- The transition is centered around \(\omega_1\), similar to the individual phase plots.

Key Features:
- The resonance at \(\omega_1\) is a critical point for both magnitude and phase responses.
- The sharpness of the peaks in both magnitude and phase plots indicates high selectivity and narrow bandwidth, typical for LC oscillators.
- The total phase shift of 360° confirms the conditions necessary for sustained oscillations at \(\omega_1\), aligning with the context that the circuit cannot oscillate at other frequencies.
image_name:∠H1
description:The graph consists of two main parts, each depicting the characteristics of a transfer function and its phase response. Here is a detailed description of each part:

Magnitude Response:
1. **Type of Graph:**
- The top row shows the magnitude response of the transfer functions, represented as Bode plots.

2. **Axes Labels and Units:**
- The horizontal axis represents angular frequency (ω), typically in radians per second.
- The vertical axis represents the magnitude of the transfer functions |H₁| and |H₂|, as well as their product |H₁H₂|.

3. **Overall Behavior and Trends:**
- Each of the individual magnitude plots, |H₁| and |H₂|, shows a peak at a specific frequency ω₁, indicating resonance.
- The product of the two, |H₁H₂|, also shows a peak at the same frequency ω₁, but with a sharper rise and fall, suggesting a higher Q factor or selectivity.
- The plots are symmetric around ω₁, showing a bell-shaped curve typical of resonant circuits.

4. **Key Features and Technical Details:**
- The peak at ω₁ is the most significant feature, where the magnitude is maximized.
- The symmetry and sharpness of the |H₁H₂| curve indicate the combined effect of the two stages.

### Phase Response:
1. **Type of Graph:**
- The bottom row depicts the phase response of the transfer functions, also represented as Bode plots.

2. **Axes Labels and Units:**
- The horizontal axis again represents angular frequency (ω).
- The vertical axis represents phase angle in degrees.

3. **Overall Behavior and Trends:**
- Each of the individual phase plots, ∠H₁ and ∠H₂, starts at +90° at low frequencies and transitions to -90° at high frequencies, crossing through 0° at ω₁.
- The combined phase response, ∠H₁H₂, starts at +180° and transitions to -180° through ω₁, maintaining a similar transition shape but doubling the phase shift due to the multiplication of the two functions.

4. **Key Features and Technical Details:**
- The crossing through 0° (for ∠H₁ and ∠H₂) and through 180° (for ∠H₁H₂) at ω₁ is a critical point, indicating the phase shift at resonance.
- The phase response indicates the inversion and phase shift introduced by each stage and their cumulative effect.

5. **Annotations and Specific Data Points:**
- The frequency ω₁ is marked as a critical frequency for both magnitude and phase responses, indicating the point of resonance and maximum phase shift.
image_name:∠H2
description:The graph titled "∠H2" is part of a series of plots illustrating the loop gain characteristics of a circuit. It is a Bode plot focusing on the phase response of the transfer function.

1. **Type of Graph and Function:**
- This is a Bode plot, specifically showing the phase response of a transfer function.

2. **Axes Labels and Units:**
- The horizontal axis represents angular frequency (ω), typically measured in radians per second.
- The vertical axis represents phase angle, measured in degrees.

3. **Overall Behavior and Trends:**
- The plot shows a phase response that starts at +90 degrees at low frequencies.
- As the frequency increases, the phase decreases, passing through 0 degrees at a certain point, and continues to decrease to -90 degrees at high frequencies.

4. **Key Features and Technical Details:**
- The phase shift begins at +90 degrees and transitions smoothly to -90 degrees.
- This behavior is typical for a second-order system where each stage contributes a +90 to -90 degree phase shift.
- The transition occurs around the resonant frequency ω1, which is marked on the plot.
- The total phase shift at resonance is 180 degrees, indicating that the circuit meets the phase condition for oscillation at this frequency.

5. **Annotations and Specific Data Points:**
- The critical frequency ω1 is marked as the point where the phase shift transitions rapidly.
- The plot does not explicitly show numerical values for ω1 but indicates its position relative to the phase shift.
- The sum of the phase contributions from two stages (each contributing a phase shift similar to ∠H2) results in a total phase shift of +180 degrees at low frequencies and -180 degrees at high frequencies, as shown in the combined plot ∠H1H2.

This phase response is crucial for understanding the stability and oscillation conditions of the circuit, as it demonstrates that the circuit can only oscillate at the designated frequency ω1 due to the specific phase shift behavior.
image_name:∠H1H2
description:The graph titled "∠H1H2" is a Bode plot, which consists of two main sections: magnitude and phase response, each composed of multiple subplots.

1. **Magnitude Response**:
- **Type of Graph**: The magnitude plots are shown as frequency response curves.
- **Axes Labels and Units**: The horizontal axis represents frequency (ω), and it is likely in a logarithmic scale, though not explicitly marked. The vertical axis represents the magnitude of the transfer functions |H1|, |H2|, and their product |H1H2|.
- **Overall Behavior and Trends**:
- Each individual magnitude plot, |H1| and |H2|, shows a peak at a specific frequency ω1, indicating a resonant frequency. These plots are symmetrical and bell-shaped, characteristic of a bandpass filter.
- The product |H1H2| also shows a similar bell-shaped curve with a sharper peak at the same frequency ω1, due to the multiplication of the two responses.
- **Key Features and Technical Details**: The peak at ω1 signifies the frequency at which the system has maximum gain, and the sharpness of the peak in |H1H2| indicates a narrow bandwidth.

2. **Phase Response**:
- **Type of Graph**: The phase plots are shown as phase shift curves.
- **Axes Labels and Units**: The horizontal axis is the same as the magnitude plots, representing frequency (ω). The vertical axis represents phase shift in degrees.
- **Overall Behavior and Trends**:
- The phase plots for ∠H1 and ∠H2 each start at +90° and decrease to -90° as frequency increases, with a smooth transition around ω1.
- The combined phase plot ∠H1H2 starts at +180° and decreases to -180°, showing a similar smooth transition around ω1.
- **Key Features and Technical Details**: The phase plots indicate a total phase shift of 360° (from +180° to -180°) across the frequency range, which is critical in determining the stability and oscillation conditions of the system.

3. **Annotations and Specific Data Points**:
- The plots are marked with the resonant frequency ω1, highlighting the frequency of interest.
- The phase shift values are explicitly marked at +90°, -90°, +180°, and -180°, providing clear reference points for analysis.

Overall, the graph illustrates the combined magnitude and phase response of a system characterized by two stages, each contributing to the overall behavior observed in the product response |H1H2| and ∠H1H2. The sharp peaks and phase shifts are indicative of the system's selective frequency amplification and phase characteristics, crucial for understanding the oscillation conditions of the circuit in question.

Figure 15.26 Loop gain characteristics of the circuit shown in Fig. 15.25.

The circuit of Fig. 15.25 serves as the core of many LC oscillators and is sometimes drawn as in Fig. 15.27(a) or (b). However, the drain currents of $M_{1}$ and $M_{2}$, and hence the output swings, heavily depend on the supply voltage. Since the waveforms at $X$ and $Y$ are differential, the drawing in Fig. 15.27(b) suggests that $M_{1}$ and $M_{2}$ can be converted to a differential pair as depicted in Fig. 15.27(c), where the total bias current is defined by $I_{S S}$.

#### Example 15.6

For the circuit of Fig. 15.27(c), plot $V_{X}$ and $V_{Y}$ and $I_{D 1}$ and $I_{D 2}$ as the oscillation begins.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: Y}
name: M2, type: NMOS, ports: {S: GND, D: Y, G: X}
name: CP1, type: Capacitor, value: CP, ports: {Np: VDD, Nn: X}
name: CP2, type: Capacitor, value: CP, ports: {Np: VDD, Nn: Y}
name: RP1, type: Resistor, value: RP, ports: {N1: VDD, N2: X}
name: RP2, type: Resistor, value: RP, ports: {N1: VDD, N2: Y}
name: LP1, type: Inductor, value: LP, ports: {N1: VDD, N2: X}
name: LP2, type: Inductor, value: LP, ports: {N1: VDD, N2: Y}
]
extrainfo:The circuit is a differential oscillator with two NMOS transistors M1 and M2, each forming a cross-coupled pair. The capacitors CP, resistors RP, and inductors LP are used to form the resonant tank circuits connected to VDD. The nodes X and Y are the differential outputs, and the circuit is grounded at the source of both transistors.

image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: Y}
name: M2, type: NMOS, ports: {S: GND, D: Y, G: X}
name: RP1, type: Resistor, value: RP, ports: {N1: VDD, N2: X}
name: RP2, type: Resistor, value: RP, ports: {N1: VDD, N2: Y}
name: CP1, type: Capacitor, value: CP, ports: {Np: VDD, Nn: X}
name: CP2, type: Capacitor, value: CP, ports: {Np: VDD, Nn: Y}
name: LP1, type: Inductor, value: LP, ports: {N1: VDD, N2: X}
name: LP2, type: Inductor, value: LP, ports: {N1: VDD, N2: Y}
]
extrainfo:The circuit is a differential oscillator with two NMOS transistors M1 and M2, forming a cross-coupled pair. Capacitors CP, resistors RP, and inductors LP form the resonant tank circuits connected to VDD. Nodes X and Y are the differential outputs, grounded at the source of both transistors.

image_name:(c)
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: Y}
name: M2, type: NMOS, ports: {S: P, D: Y, G: X}
name: RP1, type: Resistor, value: RP, ports: {N1: VDD, N2: X}
name: RP2, type: Resistor, value: RP, ports: {N1: VDD, N2: Y}
name: CP1, type: Capacitor, value: CP, ports: {Np: VDD, Nn: X}
name: CP2, type: Capacitor, value: CP, ports: {Np: VDD, Nn: Y}
name: LP1, type: Inductor, value: LP, ports: {N1: VDD, N2: X}
name: LP2, type: Inductor, value: LP, ports: {N1: VDD, N2: Y}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential oscillator with two NMOS transistors M1 and M2, forming a cross-coupled pair. Capacitors CP, resistors RP, and inductors LP form the resonant tank circuits connected to VDD. Nodes X and Y are the differential outputs, grounded at the source of both transistors. The tail current source ISS is used to lower supply sensitivity.

Figure 15.27 (a) Redrawing of the oscillator shown in Fig. 15.25; (b) another redrawing of the circuit; (c) addition of tail current source to lower supply sensitivity.

#### Solution

If the circuit begins with zero difference between $V_{X}$ and $V_{Y}$, then $V_{X}=V_{Y} \approx V_{D D}$. The two transistors share the tail current equally. If $\left(g_{m 1,2} R_{P}\right)^{2} \geq 1$, where $R_{P}$ is the equivalent parallel resistance of the tank at resonance, then noise components at the resonance frequency are amplified by $M_{1}$ and $M_{2}$, allowing the oscillation to grow. The drain currents of $M_{1}$ and $M_{2}$ vary according to the instantaneous value of $V_{X}-V_{Y}$ (as in a differential pair).

As shown in Fig. 15.28, the oscillation amplitude grows until the loop gain drops at the peaks. In fact, if $g_{m 1,2} R_{P}$ is large enough, the difference between $V_{X}-V_{Y}$ reaches a level that steers the entire tail current to one transistor, turning the other off. Thus, in the steady state, $I_{D 1}$ and $I_{D 2}$ vary between zero and $I_{S S}$.
image_name:Figure 15.28
description:The graph in Figure 15.28 is a time-domain waveform illustrating the behavior of voltages $V_X$ and $V_Y$, and drain currents $I_{D1}$ and $I_{D2}$ over time. The horizontal axis represents time ($t$), while the vertical axis is used for both voltage and current, though not explicitly labeled with units.

1. **Type of Graph and Function**: This is a time-domain waveform graph showing oscillations in voltages and currents.

2. **Axes Labels and Units**: The horizontal axis is labeled with time ($t$), but no specific time units are provided. The vertical axis has two references: $V_{DD}$ for the voltages $V_X$ and $V_Y$, and $I_{SS}/2$ for the currents $I_{D1}$ and $I_{D2}$. The units for voltage and current are not specified but are likely in volts and amperes, respectively.

3. **Overall Behavior and Trends**: The graph shows that both $V_X$ and $V_Y$ start with small oscillations around $V_{DD}$ and grow in amplitude over time. Similarly, $I_{D1}$ and $I_{D2}$ oscillate around $I_{SS}/2$ with increasing amplitude. The oscillations for both voltage and current appear sinusoidal and symmetric, indicating a stable oscillatory behavior as time progresses.

4. **Key Features and Technical Details**: The key feature is the increasing amplitude of oscillations for both voltage and current over time. This suggests a growing oscillation amplitude until a steady state is reached, which is characteristic of an oscillator circuit as described in the context. The oscillations reach a point where the loop gain drops at the peaks, stabilizing the amplitude.

5. **Annotations and Specific Data Points**: The diagram includes annotations for $V_X$, $V_Y$, $I_{D1}$, and $I_{D2}$, with reference lines at $V_{DD}$ and $I_{SS}/2$. These reference lines help in visualizing the oscillations around these central values. No specific numerical values or markers are provided for peaks or troughs.

Figure 15.28

The oscillator of Fig. 15.27(c) is constructed in fully differential form. The supply sensitivity of the circuit, however, is nonzero even with perfect symmetry. This is because the drain junction capacitances of $M_{1}$ and $M_{2}$ vary with the supply voltage. We return to this issue in Example 15.9.

### 15.3.3 Colpitts Oscillator

An LC oscillator may be realized with only one transistor in the signal path. Consider the gain stage of Fig. 15.23(a) again and recall that the drain voltage cannot be applied to the gate because the overall phase shift at resonance equals $180^{\circ}$ rather than $360^{\circ}$. Also, recall that in a common-gate stage, the phase shift from the source to the drain is zero. We then surmise that if, as shown in Fig. 15.29(a), the drain voltage is returned to the source rather than the gate, the circuit may oscillate. The coupling must incorporate a capacitor to avoid disturbing the bias point of $M_{1}$.
image_name:Figure 15.29 (a)
description:
[
name: LP, type: Inductor, value: LP, ports: {N1: VDD, N2: Vout}
name: RP, type: Resistor, value: RP, ports: {N1: VDD, N2: Vout}
name: CP, type: Capacitor, value: CP, ports: {Np: VDD, Nn: Vout}
name: M1, type: NMOS, ports: {S: s1, D: Vout, G: Vb}
name: C2, type: Capacitor, value: C2, ports: {Np: Vout, Nn: s1}
name: Ib, type: CurrentSource, value: Ib, ports: {Np: s1, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a tuned stage with feedback applied from drain to source. It includes an NMOS transistor M1, with feedback provided through a capacitor C2 to avoid disturbing the bias point. The circuit is intended for oscillation, but does not oscillate due to insufficient loop gain.
image_name:Figure 15.29 (b)
description:
[
name: M1, type: NMOS, ports: {S: S1, D: Vout, G: Vb}
name: LP, type: Inductor, value: LP, ports: {N1: VDD, N2: Vout}
name: RP, type: Resistor, value: RP, ports: {N1: VDD, N2: Vout}
name: CP, type: Capacitor, value: CP, ports: {Np: VDD, Nn: Vout}
name: C2, type: Capacitor, value: C2, ports: {Np: Vout, Nn: S1}
name: Ib, type: CurrentSource, value: Ib, ports: {Np: S1, Nn: GND}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: GND, Nn: s1}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a feedback system with insufficient loop gain to oscillate. It includes an NMOS transistor with feedback from the drain to the source, a tank circuit with an inductor, resistor, and capacitor, and a bias current source. An additional input current source is present to calculate the closed-loop gain.

Figure 15.29 (a) Tuned stage with feedback applied from drain to source; (b) addition of input current to calculate closed-loop gain.

Unfortunately, owing to insufficient loop gain, the circuit of Fig. 15.29(a) does not oscillate. To prove this point, we invoke the view of Fig. 15.1, where an oscillator is considered a feedback system with infinite closed-loop gain. Applying an input current as depicted in Fig. 15.29(b) and neglecting transistor parasitics, we obtain the closed-loop gain as

$$
\begin{equation*}
\frac{V_{\text {out }}}{I_{\text {in }}}=L_{P} s\left\|\frac{1}{C_{P} S}\right\| R_{P} \tag{15.37}
\end{equation*}
$$

because $M_{1}$ and $C_{2}$ directly conduct the input current to the tank. Since the closed-loop gain cannot be equal to infinity at any frequency, the circuit fails to oscillate.

#### Example 15.7

The reader may wonder why the input to the feedback system is realized as a current source applied to the source of the transistor rather than a voltage source applied to its gate. Perform the analysis with the latter stimulus.

#### Solution

From Fig. 15.30, we note that with a finite variation of $V_{i n}$, the change in $I_{b}$ is still zero if the bias current source is ideal. Thus, if the source-bulk junction capacitance of $M_{1}$ is neglected, the change in the tank current is zero, yielding $V_{\text {out }} / V_{\text {in }}=0$. Interestingly, $V_{X}$ does vary with $V_{i n}$, but $M_{1}$ generates a small-signal current that cancels that through $C_{2}$. The reader can prove that $V_{X} / V_{i n}=g_{m} /\left(g_{m}+C_{2} s\right)$.

The above example reveals two important points. First, to excite a circuit into oscillation, the stimulus can be applied at different points. (That is, the noise of any device in the loop can initiate the
image_name:Figure 15.30
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Ib, type: CurrentSource, value: Ib, ports: {Np: X, Nn: GND}
name: M1, type: NMOS, ports: {S: X, D: Vout, G: Vin}
name: RP, type: Resistor, value: RP, ports: {N1: Vout, N2: VDD}
name: CP, type: Capacitor, value: CP, ports: {Np: Vout, Nn: VDD}
name: C2, type: Capacitor, value: C2, ports: {Np: Vout, Nn: X}
name: LP, type: Inductor, value: LP, ports: {N1: VDD, N2: Vout}
]
extrainfo:The circuit is an oscillator with an NMOS transistor M1 and a tank circuit consisting of RP, CP, and LP. The input voltage Vin controls the gate of M1, and the current source Ib biases the circuit. The output Vout is taken across the tank circuit.

Figure 15.30
oscillation. ${ }^{6}$ ) Second, in Fig. 15.30, $V_{\text {out }} / V_{\text {in }}$ is zero because the impedance connected between the source of $M_{1}$ and ground is infinity. We then add a capacitor from this node to ground as shown in Fig. 15.31(a), seeking conditions of oscillation. Note that the capacitor in parallel with $L_{P}$ is removed. The reason will become clear later.
image_name:(a)
description:
[
name: LP, type: Inductor, value: LP, ports: {N1: VDD, N2: Vout}
name: RP, type: Resistor, value: RP, ports: {N1: VDD, N2: Vout}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vb}
name: C2, type: Capacitor, value: C2, ports: {Np: Vout, Nn: s1}
name: Is, type: CurrentSource, ports: {Np: s1, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: s1, Nn: GND}
]
extrainfo:This circuit is a Colpitts oscillator. The inductor LP and resistor RP form a parallel tank circuit connected to the drain of the NMOS transistor M1. The output Vout is taken across the tank circuit, and the transistor is biased by the voltage source S1 at the gate. Capacitors C1 and C2 are used to provide feedback necessary for oscillation.

image_name:(b)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: GND, Nn: x}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: GND, Nn: X}
name: gmV1, type: VoltageControlledCurrentSource, ports: {Np: Vout, Nn: x}
name: C1, type: Capacitor, value: C1, ports: {Np: x, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: Vout, Nn: x}
name: LP, type: Inductor, value: LP, ports: {N1: Vout, N2: GND}
name: RP, type: Resistor, value: RP, ports: {N1: Vout, N2: GND}
]
extrainfo:This circuit is a Colpitts oscillator. The voltage source V1 biases the circuit, while the current source Iin provides input stimulus. The voltage-controlled current source gmV1 models the active device. Capacitors C1 and C2, along with inductor LP and resistor RP, form the feedback network necessary for oscillation. The output is taken across the parallel combination of LP and RP.

Figure 15.31 (a) Colpitts oscillator; (b) equivalent circuit of (a) with input stimulus.
Approximating $M_{1}$ by a single voltage-dependent current source, we construct the equivalent circuit of Fig. 15.31(b). Since the current through the parallel combination of $L_{P}$ and $R_{P}$ is given by $V_{\text {out }} /\left(L_{P} s\right)+$ $V_{\text {out }} / R_{P}$, the total current through $C_{1}$ is equal to $I_{\text {in }}-V_{\text {out }} /\left(L_{P} s\right)-V_{\text {out }} / R_{P}$, yielding

$$
\begin{equation*}
V_{1}=-\left(I_{\text {in }}-\frac{V_{\text {out }}}{L_{P} S}-\frac{V_{\text {out }}}{R_{P}}\right) \frac{1}{C_{1} S} \tag{15.38}
\end{equation*}
$$

Writing the current through $C_{2}$ as $\left(V_{\text {out }}+V_{1}\right) C_{2} s$, we sum all of the currents at the output node:

$$
\begin{equation*}
-g_{m}\left(I_{\text {in }}-\frac{V_{\text {out }}}{L_{P} S}-\frac{V_{\text {out }}}{R_{P}}\right) \frac{1}{C_{1} s}+\left[V_{\text {out }}-\left(I_{\text {in }}-\frac{V_{\text {out }}}{L_{P} S}-\frac{V_{\text {out }}}{R_{P}}\right) \frac{1}{C_{1} s}\right] C_{2} s+\frac{V_{\text {out }}}{L_{P} S}+\frac{V_{\text {out }}}{R_{P}}=0 \tag{15.39}
\end{equation*}
$$

It follows that

$$
\begin{equation*}
\frac{V_{\text {out }}}{I_{\text {in }}}=\frac{R_{P} L_{P} s\left(g_{m}+C_{2} s\right)}{R_{P} C_{1} C_{2} L_{P} s^{3}+\left(C_{1}+C_{2}\right) L_{P} s^{2}+\left[g_{m} L_{P}+R_{P}\left(C_{1}+C_{2}\right)\right] s+g_{m} R_{P}} \tag{15.40}
\end{equation*}
$$

[^105]Note that, as expected, (15.40) reduces to $\left(L_{P} S \| R_{P}\right)$ if $C_{1}=0$. The circuit oscillates if the closed-loop transfer function goes to infinity at an imaginary value of $s, s_{R}=j \omega_{R}$. Consequently, both the real and imaginary parts of the denominator must drop to zero at this frequency:

$$
\begin{align*}
& -R_{P} C_{1} C_{2} L_{P} \omega_{R}^{3}+\left[g_{m} L_{P}+R_{P}\left(C_{1}+C_{2}\right)\right] \omega_{R}=0  \tag{15.41}\\
& -\left(C_{1}+C_{2}\right) L_{P} \omega_{R}^{2}+g_{m} R_{P}=0 \tag{15.42}
\end{align*}
$$

Since with typical values, $g_{m} L_{P} \ll R_{P}\left(C_{1}+C_{2}\right)$, Eq. (15.41) yields,

$$
\begin{equation*}
\omega_{R}^{2}=\frac{1}{L_{P} \frac{C_{1} C_{2}}{C_{1}+C_{2}}} \tag{15.43}
\end{equation*}
$$

and Eq. (15.42) results in

$$
\begin{align*}
g_{m} R_{P} & =\frac{\left(C_{1}+C_{2}\right)^{2}}{C_{1} C_{2}}  \tag{15.44}\\
& =\frac{C_{1}}{C_{2}}\left(1+\frac{C_{2}}{C_{1}}\right)^{2} \tag{15.45}
\end{align*}
$$

Recognizing that $g_{m} R_{P}$ is the voltage gain from the source of $M_{1}$ to the output (if $g_{m b}=0$ ), we determine the ratio $C_{1} / C_{2}$ for the minimum required gain. The reader can prove that the minimum occurs for $C_{1} / C_{2}=1$, requiring

$$
\begin{equation*}
g_{m} R_{P} \geq 4 \tag{15.46}
\end{equation*}
$$

Equation (15.46) demonstrates an important disadvantage of the Colpitts oscillator with respect to the cross-coupled topology of Fig. 15.27(c). The former demands a voltage gain of at least 4 at resonance, and the latter, only unity. This issue is critical if the inductor suffers from a low $Q$ and hence a small $R_{P}$, a common situation in CMOS technologies. As a consequence, the cross-coupled scheme is used more widely.

The foregoing analysis neglected the capacitance that appears in parallel with the inductor. As suggested in Problem 15.10, if this capacitance, $C_{P}$, is included in the equivalent circuit, Eq. (15.43) is modified as

$$
\begin{equation*}
\omega_{R}^{2}=\frac{1}{L_{P}\left(C_{P}+\frac{C_{1} C_{2}}{C_{1}+C_{2}}\right)} \tag{15.47}
\end{equation*}
$$

whereas (15.46) remains unchanged. Thus, $C_{P}$ is simply included in parallel with the series combination of $C_{1}$ and $C_{2}$.

### 15.3.4 One-Port Oscillators

Our development of oscillators thus far has been based on feedback systems. An alternative view that provides more insight into the oscillation phenomenon employs the concept of "negative resistance." To arrive at this view, let us first consider a simple tank that is stimulated by a current impulse [Fig. 15.32(a)]. The tank responds with a decaying oscillatory behavior because, in every cycle, some of the energy that reciprocates between the capacitor and the inductor is lost in the form of heat in the resistor. Now suppose a resistor equal to $-R_{P}$ is placed in parallel with $R_{P}$ and the experiment is repeated [Fig. 15.32(b)].
image_name:(a)
description:
[
name: Iin, type: CurrentSource, value: Iin, ports: {Np: GND, Nn: Iin}
name: Cp, type: Capacitor, value: Cp, ports: {Np: Vout, Nn: GND}
name: Lp, type: Inductor, value: Lp, ports: {N1: Vout, N2: GND}
name: Rp, type: Resistor, value: Rp, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit in (a) is a simple tank circuit with a capacitor Cp, an inductor Lp, and a resistor Rp connected in parallel to a current source Iin. The tank circuit exhibits a decaying oscillatory response due to energy loss in the resistor Rp.
image_name:(b)
description:
[
name: Iin, type: CurrentSource, value: Iin, ports: {Np: GND, Nn: Vout}
name: Cp, type: Capacitor, value: Cp, ports: {Np: Vout, Nn: GND}
name: Lp, type: Inductor, value: Lp, ports: {N1: Vout, N2: GND}
name: Rp, type: Resistor, value: Rp, ports: {N1: Vout, N2: GND}
name: -Rp, type: Resistor, value: -Rp, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit in diagram (b) represents a tank circuit with added negative resistance to counteract the losses in the resistor Rp, allowing for sustained oscillations.
image_name:(c)
description:The circuit in diagram (c) is a one-port oscillator with an active circuit providing negative resistance to counteract the losses in Rp. This configuration allows the tank circuit to oscillate indefinitely.

Figure 15.32 (a) Decaying impulse response of a tank; (b) addition of negative resistance to cancel loss in $R_{P}$; (c) use of an active circuit to provide negative resistance.

Since $R_{P} \|\left(-R_{P}\right)=\infty$, the tank oscillates indefinitely. Thus, if a one-port circuit exhibiting a negative resistance is placed in parallel with a tank [Fig. 15.32(c)], the combination may oscillate. Such a topology is called a one-port oscillator.

How can a circuit provide a negative resistance? Recall that feedback multiplies or divides the input and output impedances of circuits by a factor equal to one plus the loop gain. Thus, if the loop gain is sufficiently negative (i.e., the feedback is sufficiently positive), a negative resistance is achieved. As a simple example, let us apply positive feedback around a source follower. The follower introduces no signal inversion, and neither must the feedback network. As depicted in Fig. 15.33(a), we implement the feedback by a common-gate stage and add the current source $I_{b}$ to provide the bias current of $M_{2}{ }^{7}$ From the equivalent circuit in Fig. 15.33(b) (where channel-length modulation and body effect are neglected),
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: s1s2, D: VDD, G: X}
name: M2, type: NMOS, ports: {S: s1s2, D: X, G: Vb}
name: Ib, type: CurrentSource, ports: {Np: VDD, Nn: X}
name: Is, type: CurrentSource, ports: {Np: s1s2, Nn: GND}
]
extrainfo:The circuit in Fig. 15.33(a) is a source follower with positive feedback to create negative input impedance. It uses two NMOS transistors (M1 and M2) with a current source (Ib) to provide bias. The equivalent circuit in Fig. 15.33(b) is used to calculate the input impedance, showing the relationships between currents and voltages in the system.
image_name:(b)
description:The circuit in Figure 15.33(b) is an equivalent circuit for calculating input impedance, featuring a combination of voltage and current sources, and NMOS transistors with positive feedback to create negative input impedance.

Figure 15.33 (a) Source follower with positive feedback to create negative input impedance; (b) equivalent circuit of (a) to calculate the input impedance.

[^106]we have
\$\$

$$
\begin{equation*}
I_{X}=g_{m 2} V_{2}=-g_{m 1} V_{1} \tag{15.48}
\end{equation*}
$$

$$
and
$$

$$
\begin{align*}
V_{X} & =V_{1}-V_{2}  \tag{15.49}\\
& =-\frac{I_{X}}{g_{m 1}}-\frac{I_{X}}{g_{m 2}} \tag{15.50}
\end{align*}
$$

\$\$

Thus,

$$
\begin{equation*}
\frac{V_{X}}{I_{X}}=-\left(\frac{1}{g_{m 1}}+\frac{1}{g_{m 2}}\right) \tag{15.51}
\end{equation*}
$$

and, if $g_{m 1}=g_{m 2}=g_{m}$, then

$$
\begin{equation*}
\frac{V_{X}}{I_{X}}=\frac{-2}{g_{m}} \tag{15.52}
\end{equation*}
$$

Negative resistance becomes more intuitive if we bear in mind that it is an incremental quantity; that is, negative resistance indicates that if the applied voltage increases, the current drawn by the circuit decreases. In Fig. 15.33(a), for example, if the input voltage increases, so does the source voltage of $M_{1}$, decreasing the drain current of $M_{2}$ and allowing part of $I_{b}$ to flow to the input source.
image_name:Figure 15.34
description:
[
name: LP, type: Inductor, value: LP, ports: {N1: VDD, N2: g1d2}
name: RP, type: Resistor, value: RP, ports: {N1: VDD, N2: g1d2}
name: CP, type: Capacitor, value: CP, ports: {Np: VDD, Nn: g1d2}
name: M1, type: NMOS, ports: {S: s1s2, D: VDD, G: g1d2}
name: M2, type: NMOS, ports: {S: s1s2, D: g1d2, G: Vb}
name: IS, type: CurrentSource, value: IS, ports: {Np: s1s2, Nn: GND}
]
extrainfo:The circuit is an oscillator using the negative input resistance of a source follower with positive feedback. The inductor LP provides the bias current for M2, eliminating the need for an additional current source. The condition for oscillation is RP - 2/gm >= 0.

Figure 15.34 Oscillator using the negative input resistance of a source follower with positive feedback.

With a negative resistance available, we can now construct an oscillator as illustrated in Fig. 15.34. Here, $R_{P}$ denotes the equivalent parallel resistance of the tank and, for oscillation build-up, $R_{P}-2 / g_{m} \geq 0$. Note that the inductor provides the bias current of $M_{2}$, obviating the need for a current source. If the small-signal resistance presented by $M_{1}$ and $M_{2}$ to the tank is less negative than $-R_{P}$, then the circuit experiences large swings such that each transistor is nearly off for part of the period, thereby yielding an "average" resistance of $-R_{P}$.

The circuit of Fig. 15.34 is similar to the stage of Fig. 15.29(a), but with the feedback capacitor replaced by a source follower. More interestingly, the circuit can be redrawn as in Fig. 15.35(a), bearing a resemblance to Fig. 15.27(c). In fact, if the drain current of $M_{1}$ flows through a tank and the resulting voltage is applied to the gate of $M_{2}$, the topology of Fig. 15.35(b) is obtained. Ignoring bias paths and merging the two tanks into one (Fig. 15.36), we note that the cross-coupled pair must provide a negative resistance of $-R_{P}$ between nodes $X$ and $Y$ to enable oscillation. The reader can prove that this resistance is equal to $-2 / g_{m}$ and hence it is necessary that $R_{P} \geq 1 / g_{m}$. Thus, the circuit can be viewed as either a feedback system or a negative resistance in parallel with a lossy tank. This topology is also called a "negative- $G_{m}$ oscillator."
image_name:(a)
description:
[
name: LP, type: Inductor, value: LP, ports: {N1: VDD, N2: g1d2}
name: RP, type: Resistor, value: RP, ports: {N1: VDD, N2: g1d2}
name: CP, type: Capacitor, value: CP, ports: {Np: VDD, Nn: g1d2}
name: M1, type: NMOS, ports: {S: P, D: VDD, G: g1d2}
name: M2, type: NMOS, ports: {S: p, D: g1d2, G: Vb}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: Vb, type: VoltageSource, value: Vb, ports: {Np: Vb, Nn: GND}
name: Is, type: CurrentSource, value: Is, ports: {Np: p, Nn: GND}
]
extrainfo:The circuit is a negative-Gm oscillator with a cross-coupled NMOS pair providing negative resistance to sustain oscillations. The tank circuit is formed by LP, RP, and CP.
image_name:(b)
description:
[
name: LP, type: Inductor, value: LP, ports: {N1: g1d2, N2: VDD}
name: RP, type: Resistor, value: RP, ports: {N1: g1d2, N2: VDD}
name: CP, type: Capacitor, value: CP, ports: {Np: g1d2, Nn: VDD}
name: LP, type: Inductor, value: LP, ports: {N1: g2d1, N2: VDD}
name: RP, type: Resistor, value: RP, ports: {N1: g2d1, N2: VDD}
name: CP, type: Capacitor, value: CP, ports: {Np: g2d1, Nn: VDD}
name: M1, type: NMOS, ports: {S: P, D: d1g2, G: g1d2}
name: M2, type: NMOS, ports: {S: P, D: g1d2, G: d1g2}
]
extrainfo:The circuit is a differential negative-Gm oscillator with a cross-coupled pair of NMOS transistors (M1 and M2) providing negative resistance. The tank circuit is formed by LP, RP, and CP. The bias voltage Vb controls the gates of M1 and M2.
Figure 15.35 (a) Redrawing of the topology shown in Fig. 15.34; (b) differential version of (a).
image_name:Figure 15.36(a)
description:
[
name: CP, type: Capacitor, value: CP, ports: {Np: X, Nn: Z}
name: LP, type: Inductor, value: LP, ports: {N1: X, N2: Z}
name: RP, type: Resistor, value: RP, ports: {N1: X, N2: Z}
name: M1, type: NMOS, ports: {S: P, D: Y, G: X}
name: M2, type: NMOS, ports: {S: P, D: X, G: Y}
name: Is, type: CurrentSource, value: Is, ports: {Np: P, Nn: GND}
name: Cp, type: Capacitor, value: Cp/2, ports: {Np: X, Nn: Y}
name: Lp, type: Inductor, value: 2Lp, ports: {N1: X, N2: Y}
name: Rp, type: Resistor, value: 2Rp, ports: {N1: X, N2: Y}
name: M1, type: NMOS, ports: {S: P, D: Y, G: X}
name: M2, type: NMOS, ports: {S: P, D: X, G: Y}
name: Is, type: CurrentSource, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential negative-Gm oscillator using a cross-coupled NMOS pair (M1 and M2) to provide negative resistance. It includes an LC tank circuit formed by two parallel LC sections with components Cp, Lp, and Rp. The circuit is designed to create oscillations by balancing the negative resistance with the losses in the LC tank.
Figure 15.36 Equivalent circuit of Fig. 15.35(b).
As another method of creating negative resistance, consider the topology depicted in Fig. 15.37(a), where none of the nodes is grounded and channel-length modulation, body effect, and transistor capacitances are neglected. Since the drain current of $M_{1}$ is equal to $\left(-I_{X} / C_{1} s\right) g_{m}$, we have

$$
\begin{equation*}
V_{X}=\left(I_{X}-\frac{-I_{X}}{C_{1} s} g_{m}\right) \frac{1}{C_{2} s}+\frac{I_{X}}{C_{1} s} \tag{15.53}
\end{equation*}
$$

image_name:(a)
description:
[
name: Vx, type: VoltageSource, value: Vx, ports: {Np: g1, Nn: d1}
name: M1, type: NMOS, ports: {S: s1, D: 3, G: 2}
name: C1, type: Capacitor, value: C1, ports: {Np: 4, Nn: 5}
name: C2, type: Capacitor, value: C2, ports: {Np: 3, Nn: 5}
name: d1, type: Diode, ports: {Na: 3, Nc: 5}
name: g1, type: VoltageControlledCurrentSource, value: g1, ports: {Np: 2, Nn: 4}
name: S1, type: Switch, ports: {N1: 4, N2: 5}
]
extrainfo:The circuit provides a topology for generating negative resistance using an NMOS transistor and passive components. Capacitors C1 and C2 are used alongside a diode and a voltage-controlled current source.
image_name:(b)
description:
[
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Vx, Nn: GND}
name: Ix, type: CurrentSource, value: Ix, ports: {Np: Ix, Nn: d1}
name: -Ix, type: CurrentSource, value: -Ix, ports: {Np: GND, Nn: s1}
name: M1, type: NMOS, ports: {S: s1, D: d1, G: G1}
name: C1, type: Capacitor, value: C1, ports: {Np: s1, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: d1, Nn: GND}
name: S1, type: Switch, ports: {N1: s1, N2: GND}
name: D1, type: Diode, ports: {Na: d1, Nc: GND}
name: G1, type: VoltageControlledCurrentSource, value: G1, ports: {Np: G1, Nn: GND}
]
extrainfo:The circuit represents an equivalent circuit topology providing negative resistance. It includes voltage and current sources, capacitors, a diode, a switch, and an NMOS transistor. The circuit is designed to demonstrate how negative resistance can be achieved using these components.
image_name:(c)
description:
[
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Vx, Nn: GND}
name: Ix, type: CurrentSource, value: Ix, ports: {Np: Ix, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: d1, G: g1}
name: C1, type: Capacitor, value: C1, ports: {Np: g1, Nn: s1}
name: C2, type: Capacitor, value: C2, ports: {Np: d1, Nn: GND}
name: d1, type: Diode, ports: {Na: d1, Nc: GND}
name: g1, type: VoltageControlledCurrentSource, value: g1, ports: {Np: Vx, Nn: g1}
name: s1, type: VoltageControlledVoltageSource, value: s1, ports: {Np: s1, Nn: GND}
]
extrainfo:The circuit diagram represents an oscillator using a topology that provides negative resistance. The NMOS transistor M1 is connected with its drain at node d1 and gate at node g1. Capacitors C1 and C2 are used to control the frequency of oscillation.

Figure 15.37 (a) Circuit topology providing negative resistance; (b) equivalent circuit of (a); (c) oscillator using (a).
and hence

$$
\begin{equation*}
\frac{V_{X}}{I_{X}}=\frac{g_{m}}{C_{1} C_{2} s^{2}}+\frac{1}{C_{2} s}+\frac{1}{C_{1} s} \tag{15.54}
\end{equation*}
$$

For $s=j \omega$, this impedance consists of a negative resistance equal to $-g_{m} /\left(C_{1} C_{2} \omega^{2}\right)$ in series with the series combination of $C_{1}$ and $C_{2}$ [Fig. 15.37(b)]. Thus, as shown in Fig. 15.37(c), if an inductor is placed between the gate and drain of $M_{1}$, the circuit may oscillate. Of the three nodes in the circuit, one can be an ac ground, resulting in the three different topologies illustrated in Fig. 15.38. The circuit of Fig. 15.38(a) is in fact based on a source follower, whose input impedance was found in Chapter 6 to contain a negative real part. The configuration of Fig. 15.38(b) is a Colpitts oscillator.
image_name:(a)
description:
[
name: L1, type: Inductor, value: L1, ports: {N1: GND, N2: g1}
name: M1, type: NMOS, ports: {S: s1, D: VDD, G: g1}
name: C1, type: Capacitor, value: C1, ports: {Np: s1, Nn: g1}
name: C2, type: Capacitor, value: C2, ports: {Np: s1, Nn: GND}
]
extrainfo:The circuit in diagram (a) represents a source follower topology with an NMOS transistor M1. The inductor L1 is connected between ground and the gate of M1, while capacitors C1 and C2 are connected in parallel between the source of M1 and ground. This configuration can potentially lead to oscillations.
image_name:(b)
description:
[
name: L1, type: Inductor, value: L1, ports: {N1: VDD, N2: d1}
name: M1, type: NMOS, ports: {S: s1, D: d1, G: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: s1, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: d1, Nn: s1}
name: C1, type: VoltageSource, value: C1, ports: {Np: s1, Nn: GND}
]
extrainfo:The circuit diagram represents a Colpitts oscillator topology with an inductor L1 connected between the VDD and the drain of the NMOS M1. Capacitors C1 and C2 form a voltage divider that determines the feedback ratio. The gate of M1 is connected to the drain through C2, while the source is grounded. This configuration can lead to oscillations due to the feedback loop created by C1, C2, and L1.
image_name:(c)
description:
[
name: L1, type: Inductor, value: L1, ports: {N1: g1, N2: d1}
name: M1, type: NMOS, ports: {S: GND, D: d1, G: g1}
name: C1, type: Capacitor, value: C1, ports: {Np: g1, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: d1, Nn: GND}
]
extrainfo:The circuit is a Colpitts oscillator configuration using an NMOS transistor M1 with an inductor L1 and capacitors C1 and C2. The voltage source g1 provides gate biasing.

Figure 15.38 Oscillator topologies derived from the circuit of Fig. 15.37(c).

#### Example 15.8

Redraw the circuits of Fig. 15.38 with proper biasing.

#### Solution

The circuits are redrawn in Fig. 15.39.
image_name:(a)
description:
[
name: L1, type: Inductor, value: L1, ports: {N1: Vb, N2: g1}
name: M1, type: NMOS, ports: {S: s1, D: VDD, G: g1}
name: C1, type: Capacitor, value: C1, ports: {Np: g1, Nn: s1}
name: C2, type: Capacitor, value: C2, ports: {Np: s1, Nn: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: s1, Nn: GND}
]
extrainfo:The circuit is a Colpitts oscillator configuration using an NMOS transistor M1 with an inductor L1 and capacitors C1 and C2. The voltage source g1 provides gate biasing.
image_name:(b)
description:
[
name: L1, type: Inductor, value: L1, ports: {N1: VDD, N2: d1}
name: M1, type: NMOS, ports: {S: s1, D: d1, G: Vb}
name: C1, type: Capacitor, value: C1, ports: {Np: s1, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: d1, Nn: s1}
name: I1, type: CurrentSource, value: I1, ports: {Np: s1, Nn: GND}
]
extrainfo:The circuit is a Colpitts oscillator configuration using an NMOS transistor M1 with an inductor L1 and capacitors C1 and C2. The voltage source g1 provides gate biasing.
image_name:(c)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1, G: g1}
name: L1, type: Inductor, value: L1, ports: {N1: g1, N2: d1}
name: C1, type: Capacitor, value: C1, ports: {Np: g1, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: d1, Nn: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: d1}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit diagram (c) is a Colpitts oscillator using an NMOS transistor M1. It includes an inductor L1 and capacitors C1 and C2. The gate of the NMOS is biased by the voltage source g1. The circuit is powered by VDD and has a current source I1 connected to the node s1.

Figure 15.39

## 15.4 ■ Voltage-Controlled Oscillators

Most applications require that oscillators be "tunable," i.e., that their output frequency be a function of a control input, usually a voltage. An ideal voltage-controlled oscillator is a circuit whose output frequency

Sec. 15.4 Voltage-Controlled Oscillators
image_name:Figure 15.40
description:The system block diagram labeled "Figure 15.40" illustrates the functional representation of a Voltage-Controlled Oscillator (VCO). The diagram is divided into two main sections: a block diagram and a graph.

Main Components:
- **Voltage-Controlled Oscillator Block:** This is the central component of the system. It receives an input control voltage \( V_{cont} \) and produces an output frequency \( \omega_{out} \). The VCO's primary function is to convert the input voltage into a corresponding output frequency, making the frequency directly dependent on the control voltage.

Flow of Information or Control:
- **Input:** The control voltage \( V_{cont} \) is fed into the VCO. This input determines the oscillation frequency of the output.
- **Output:** The output frequency \( \omega_{out} \) is generated by the VCO as a function of the control voltage. The relationship between the input and output is linear, as depicted in the graph below the block diagram.

Labels, Annotations, and Key Indicators:
- **Graph:** Below the VCO block, a graph shows the relationship between \( V_{cont} \) (x-axis) and \( \omega_{out} \) (y-axis). The graph is a linear plot indicating that the output frequency increases linearly with an increase in control voltage.
- **\( \omega_{0} \):** This is the intercept on the y-axis, representing the output frequency when the control voltage is zero.
- **\( K_{VCO} \):** This is the slope of the line in the graph, representing the gain or sensitivity of the VCO, measured in rad/s/V.
- **\( \omega_{1} \) and \( \omega_{2} \):** These are specific frequency points on the y-axis, indicating the range of frequencies achievable by varying the control voltage from \( V_{1} \) to \( V_{2} \).

Overall System Function:
The primary function of this system is to provide a tunable frequency output that varies linearly with the input control voltage. The VCO is designed to have a specific gain \( K_{VCO} \), allowing for precise control of the output frequency over a defined tuning range. This makes it suitable for applications requiring adjustable frequency outputs based on varying voltage inputs.
image_name:Definition of a VCO.
description:The graph in Figure 15.40 is a linear plot representing the relationship between the control voltage \( V_{\text{cont}} \) and the output frequency \( \omega_{\text{out}} \) of a voltage-controlled oscillator (VCO). The graph is a two-dimensional Cartesian plot with the horizontal axis labeled as \( V_{\text{cont}} \), representing the control voltage. The vertical axis is labeled \( \omega_{\text{out}} \), representing the output angular frequency.

The plot shows a linear relationship between \( V_{\text{cont}} \) and \( \omega_{\text{out}} \), indicating that the output frequency increases linearly with an increase in control voltage. The line starts at \( \omega_{0} \) when \( V_{\text{cont}} = 0 \), which is the intercept on the \( \omega_{\text{out}} \) axis.

The slope of the line, \( K_{\text{VCO}} \), represents the gain or sensitivity of the VCO, expressed in radians per second per volt (rad/s/V). This slope indicates how much the output frequency changes per unit change in control voltage.

The graph also highlights two specific points, \( V_1 \) and \( V_2 \), on the \( V_{\text{cont}} \) axis, corresponding to \( \omega_1 \) and \( \omega_2 \) on the \( \omega_{\text{out}} \) axis, respectively. These points define the tuning range of the VCO, \( \omega_2 - \omega_1 \), which is the range over which the oscillator can vary its output frequency based on the control voltage. The dashed lines help illustrate these points and the linear relationship.

Figure 15.40 Definition of a VCO.
is a linear function of its control voltage (Fig. 15.40):

$$
\begin{equation*}
\omega_{\text {out }}=\omega_{0}+K_{V C O} V_{\text {cont }} \tag{15.55}
\end{equation*}
$$

Here, $\omega_{0}$ represents the intercept corresponding to $V_{c o n t}=0$ and $K_{V C O}$ denotes the "gain" or "sensitivity" of the circuit (expressed in rad/s/V). ${ }^{8}$ The achievable range, $\omega_{2}-\omega_{1}$, is called the "tuning range."

#### Example 15.9

In the negative- $G_{m}$ oscillator of Fig. 15.27(c), assume that $C_{P}=0$, consider only the drain junction capacitance, $C_{D B}$, of $M_{1}$ and $M_{2}$, and explain why $V_{D D}$ can be viewed as the control voltage. Calculate the gain of the VCO.

#### Solution

Since $C_{D B}$ varies with the drain-bulk voltage, if $V_{D D}$ changes, so does the resonance frequency of the tank. Noting that the average voltage across $C_{D B}$ is approximately equal to $V_{D D}$, we write

$$
\begin{equation*}
C_{D B}=\frac{C_{D B 0}}{\left(1+\frac{V_{D D}}{\phi_{B}}\right)^{m}} \tag{15.56}
\end{equation*}
$$

and

$$
\begin{align*}
K_{V C O} & =\frac{\partial \omega_{\text {out }}}{\partial V_{D D}}  \tag{15.57}\\
& =\frac{\partial \omega_{\text {out }}}{\partial C_{D B}} \cdot \frac{\partial C_{D B}}{\partial V_{D D}} \tag{15.58}
\end{align*}
$$

With $\omega_{\text {out }}=1 / \sqrt{L_{P} C_{D B}}$, we have

$$
\begin{align*}
K_{V C O} & =\frac{-1}{2 \sqrt{L_{P} C_{D B} C_{D B}}} \cdot \frac{-m C_{D B}}{\phi_{B}\left(1+\frac{V_{D D}}{\phi_{B}}\right)}  \tag{15.59}\\
& =\frac{m}{2 \phi_{B}\left(1+\frac{V_{D D}}{\phi_{B}}\right)} \cdot \omega_{\text {out }} \tag{15.60}
\end{align*}
$$

Note that the relationship between $\omega_{\text {out }}$ and $V_{\text {cont }}$ is nonlinear because $K_{V C O}$ varies with $V_{D D}$ and $\omega_{\text {out }}$.

Before modifying the oscillators studied in the previous sections for tunability, we summarize the important performance parameters of VCOs.

Center Frequency The center frequency (i.e., the midrange value in Fig. 15.40) is determined by the environment in which the VCO is used. For example, in the clock generation network of a microprocessor, the VCO may be required to run at the clock rate or even twice that. Today's CMOS VCOs achieve center frequencies as high as hundreds of gigahertz.
Tuning Range The required tuning range is dictated by two parameters: (1) the variation of the VCO center frequency with process and temperature, and (2) the frequency range necessary for the application. The center frequency of some CMOS oscillators may vary by a factor of two at the extremes of process and temperature, thus mandating a sufficiently wide $(\geq 2 \times)$ tuning range to guarantee that the VCO output frequency can be driven to the desired value. Also, some applications incorporate clock frequencies that must vary by one to two orders of magnitude depending on the mode of operation, demanding a proportionally wide tuning range.

An important concern in the design of VCOs is the disturbance of the output phase and frequency as a result of noise on the control line. For a given noise amplitude, the noise in the output frequency is proportional to $K_{V C O}$ because $\omega_{\text {out }}=\omega_{0}+K_{V C O} V_{\text {cont }}$. Thus, to minimize the effect of noise in $V_{\text {cont }}$, the VCO gain must be minimized, a constraint in direct conflict with the required tuning range. In fact, if, as shown in Fig. 15.40, the allowable range of $V_{\text {cont }}$ is from $V_{1}$ to $V_{2}$ (e.g., from 0 to $V_{D D}$ ) and the tuning range must span at least $\omega_{1}$ to $\omega_{2}$, then $K_{V C O}$ must satisfy the following requirement:

$$
\begin{equation*}
K_{V C O} \geq \frac{\omega_{2}-\omega_{1}}{V_{2}-V_{1}} \tag{15.61}
\end{equation*}
$$

Note that, for a given tuning range, $K_{V C O}$ increases as the supply voltage decreases, making the oscillator more sensitive to noise on the control line.

Tuning Linearity As exemplified by Eq. (15.60), the tuning characteristics of VCOs exhibit nonlinearity, i.e., their gain, $K_{V C O}$, is not constant. As explained in Chapter 16, such nonlinearity degrades the settling behavior of phase-locked loops. For this reason, it is desirable to minimize the variation of $K_{V C O}$ across the tuning range.

Actual oscillator characteristics typically exhibit a high-gain region in the middle of the range and a low gain at the two extremes (Fig. 15.41). Compared to a linear characteristic (the gray line), the actual behavior displays a maximum gain greater than that predicted by (15.61), implying that, for a given tuning range, nonlinearity inevitably leads to higher sensitivity for some region of the characteristic.
image_name:Figure 15.41 Nonlinear VCO characteristic
description:The graph depicted is a characteristic curve of a Voltage-Controlled Oscillator (VCO), illustrating the nonlinear relationship between the output frequency (ω_out) and the control voltage (V_cont). The horizontal axis represents the control voltage (V_cont), while the vertical axis represents the output frequency (ω_out). Both axes appear to use linear scales.

In this graph, there is a black curve that represents the actual nonlinear characteristic of the VCO, and a gray line that indicates an ideal linear characteristic for comparison. The black curve shows a typical S-shaped nonlinear behavior.

1. **Axes Labels and Units:**
- **Horizontal Axis (V_cont):** Represents the control voltage.
- **Vertical Axis (ω_out):** Represents the output frequency.

2. **Overall Behavior and Trends:**
- The curve starts at a lower frequency (ω1) when the control voltage is at V1.
- As the control voltage increases towards V2, the output frequency rises, reaching an upper frequency limit (ω2).
- The curve exhibits a high-gain region in the middle of the range, where the slope is steepest, indicating increased sensitivity to changes in control voltage.
- At the extremes (near V1 and V2), the curve flattens, indicating lower sensitivity and gain.

3. **Key Features and Technical Details:**
- **High-Gain Region:** The middle portion of the curve is where the gain is highest, corresponding to the steepest slope.
- **Low-Gain Regions:** At the beginning and end of the curve, the slope decreases, indicating reduced sensitivity.
- Compared to the gray linear line, the actual characteristic (black curve) has a higher peak gain, demonstrating nonlinearity.

4. **Annotations and Specific Data Points:**
- The graph is annotated with dashed lines indicating the frequencies ω1 and ω2 and the control voltages V1 and V2, marking the range of operation.
- The gray line serves as a reference for a linear response, highlighting the nonlinearity of the actual characteristic.

This graph effectively demonstrates the nonlinear behavior of a VCO, emphasizing the trade-offs between gain and control voltage across the tuning range.

Output Amplitude It is desirable to achieve a large output oscillation amplitude, thus making the waveform less sensitive to noise. The amplitude trades with power dissipation, supply voltage, and (as explained in Sec. 15.4.2) even the tuning range. Also, the amplitude may vary across the tuning range, an undesirable effect.

Power Dissipation As with other analog circuits, oscillators suffer from trade-offs among speed, power dissipation, and noise. Typical oscillators drain 1 to 10 mW of power.
Supply and Common-Mode Rejection Oscillators are quite sensitive to noise, especially if they are realized in single-ended form. As seen in Example 15.9, even differential oscillators exhibit supply sensitivity. The design of oscillators for high noise immunity is a difficult challenge.
Output Signal Purity Even with a constant control voltage, the output waveform of a VCO is not perfectly periodic. The electronic noise of the devices in the oscillator and supply noise lead to noise in the output phase and frequency. These effects are quantified by "jitter" and "phase noise" and determined by the requirements of each application.

### 15.4.1 Tuning in Ring Oscillators

Recall from Sec. 15.2 that the oscillation frequency, $f_{o s c}$, of an $N$-stage ring equals $\left(2 N T_{D}\right)^{-1}$, where $T_{D}$ denotes the large-signal delay of each stage. Thus, to vary the frequency, $T_{D}$ can be adjusted.
image_name:Figure 15.42 Differential pair with variable output time constant
description:
[
name: M1, type: NMOS, ports: {S: P, D: Voutn, G: Vip}
name: M2, type: NMOS, ports: {S: P, D: Voutp, G: Vin}
name: M3, type: PMOS, ports: {S: VDD, D: Voutn, G: Vcont}
name: M4, type: PMOS, ports: {S: VDD, D: Voutp, G: Vcont}
name: CL1, type: Capacitor, value: CL, ports: {Np: VoutN, Nn: GND}
name: CL2, type: Capacitor, value: CL, ports: {Np: Voutp, Nn: GND}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential pair used in a ring oscillator with variable output time constant. M3 and M4 act as variable resistors controlled by Vcont, affecting the oscillation frequency.

Figure 15.42 Differential pair with variable output time constant.

As a simple example, consider the differential pair of Fig. 15.42 as one stage of a ring oscillator. Here, $M_{3}$ and $M_{4}$ operate in the triode region, each acting as a variable resistor controlled by $V_{\text {cont }}$. As $V_{\text {cont }}$ becomes more positive, the on-resistance of $M_{3}$ and $M_{4}$ increases, thus raising the time constant at the output, $\tau_{1}$, and lowering $f_{o s c}$. If $M_{3}$ and $M_{4}$ remain in the deep triode region,

$$
\begin{align*}
\tau_{1} & =R_{o n 3,4} C_{L}  \tag{15.62}\\
& =\frac{C_{L}}{\mu_{p} C_{o x}\left(\frac{W}{L}\right)_{3,4}\left(V_{D D}-V_{c o n t}-\left|V_{T H P}\right|\right)} \tag{15.63}
\end{align*}
$$

In the above equation, $C_{L}$ denotes the total capacitance seen at each output to ground (including the input capacitance of the following stage). The delay of the circuit is roughly proportional to $\tau_{1}$, yielding

$$
\begin{align*}
f_{\text {osc }} & \propto \frac{1}{T_{D}}  \tag{15.64}\\
& \propto \frac{\mu_{p} C_{o x}\left(\frac{W}{L}\right)_{3,4}\left(V_{D D}-V_{c o n t}-\left|V_{T H P}\right|\right)}{C_{L}} \tag{15.65}
\end{align*}
$$

Interestingly, $f_{\text {osc }}$ is linearly proportional to $V_{\text {cont }}$.

- Example 15.10

For the given device dimensions and bias currents in Fig. 15.42, determine the maximum allowable value of $V_{\text {cont }}$. What happens if $M_{3}$ and $M_{4}$ enter saturation?

#### Solution

Let us assume (somewhat arbitrarily) that $M_{3}$ and $M_{4}$ remain in the deep triode region if $\left|V_{D S 3,4}\right| \leq 0.2 \times 2 \mid V_{G S 3,4}-$ $V_{T H P} \mid$. If each stage in the ring experiences complete switching, then the maximum drain current of $M_{3}$ and $M_{4}$ is equal to $I_{S S}$. To satisfy the above condition, we must have $I_{S S} R_{o n 3,4} \leq 0.4\left(V_{D D}-V_{c o n t}-\left|V_{T H P}\right|\right)$, and hence

$$
\begin{equation*}
\frac{I_{S S}}{\mu_{p} C_{o x}\left(\frac{W}{L}\right)_{3,4}\left(V_{D D}-V_{\text {cont }}-\left|V_{T H P}\right|\right)} \leq 0.4\left(V_{D D}-V_{\text {cont }}-\left|V_{T H P}\right|\right) \tag{15.66}
\end{equation*}
$$

It follows that

$$
\begin{equation*}
V_{\text {cont }} \leq V_{D D}-\left|V_{T H P}\right|-\sqrt{\frac{I_{S S}}{0.4 \mu_{p} C_{o x}\left(\frac{W}{L}\right)_{3,4}}} \tag{15.67}
\end{equation*}
$$

If $V_{\text {cont }}$ exceeds this level by a large margin, $M_{3}$ and $M_{4}$ eventually enter saturation. Each stage then requires common-mode feedback to produce the output swings around a well-defined CM level.

The differential pair of Fig. 15.42 suffers from a critical drawback: the output swing of the circuit varies considerably across the tuning range. With complete switching, each stage provides a differential output swing of $2 I_{S S} R_{\text {on } 3,4}$. Thus, a tuning range of, say, two to one translates to a twofold variation in the swing.

In order to minimize the swing variation, the tail current can be adjusted by $V_{\text {cont }}$ as well such that, as $V_{\text {cont }}$ becomes more positive, $I_{S S}$ decreases. The circuit nonetheless requires a means of maintaining $I_{S S} R_{\text {on } 3,4}$ relatively constant. To this end, let us consider the circuit in Fig. 15.43(a), where $M_{5}$ operates in the deep triode region and amplifier $A_{1}$ applies negative feedback to the gate of $M_{5}$. If the loop gain is sufficiently large, the differential input voltage of $A_{1}$ must be small, giving $V_{P} \approx V_{R E F}$ and $\left|V_{D S 5}\right| \approx V_{D D}-V_{R E F}$. Thus, the feedback ensures a relatively constant drain-source voltage even if $I_{1}$ varies. In fact, as $I_{1}$, say, decreases, $A_{1}$ raises the gate voltage of $M_{5}$ such that $R_{o n 5} I_{1} \approx V_{D D}-V_{R E F}$.
image_name:Figure 15.43(a)
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: P, InN: VREF, OutP: g5}
name: M5, type: PMOS, ports: {S: VDD, D: P, G: g5}
name: I1, type: CurrentSource, value: I1, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a feedback loop with an operational amplifier A1 providing negative feedback to the gate of PMOS M5. The current source I1 is connected to node P and ground. VREF is used as a reference voltage for the op-amp.

image_name:Figure 15.43(b)
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: P, InN: VREF, OutP: g5}
name: M1, type: NMOS, ports: {S: P, D: X, G: Vip}
name: M2, type: NMOS, ports: {S: P, D: Y, G: Vin}
name: M3, type: PMOS, ports: {S: VDD, D: X, G: g5}
name: M4, type: PMOS, ports: {S: VDD, D: Y, G: g5}
name: M5, type: PMOS, ports: {S: VDD, D: P, G: g5}
name: I1, type: CurrentSource, value: I1, ports: {Np: P, Nn: GND}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit provides negative feedback to stabilize the drain-source voltage of M5 by controlling its gate voltage through the op-amp A1. The current source I1 is connected between node Vcont and ground. The topology can serve as a replica circuit for the stages of a ring oscillator, defining the oscillation amplitude.

Figure 15.43 (a) Simple feedback circuit defining $V_{P}$; (b) replica biasing to define voltage swings in a ring oscillator.

The topology of Fig. 15.43(a) can serve as a "replica circuit" for the stages of a ring oscillator, thereby defining the oscillation amplitude. Illustrated in Fig. 15.43(b), the idea is to "servo" the on-resistance of $M_{3}$ and $M_{4}$ to that of $M_{5}$ and vary the frequency by adjusting $I_{1}$ and $I_{S S}$ simultaneously [2]. If $M_{3}$ and $M_{4}$ are identical to $M_{5}$ and $I_{S S}$ to $I_{1}$, then $V_{X}$ and $V_{Y}$ vary from $V_{D D}$ to $V_{D D}-V_{R E F}$ as $M_{1}$ and $M_{2}$ steer the tail current to one side or the other. Thus, if process and temperature variations, say, decrease $I_{1}$ and $I_{S S}$, then $A_{1}$ increases the on-resistance of $M_{3}-M_{5}$, forcing $V_{P}$ and hence $V_{X}$ and $V_{Y}$ (when $M_{1}$ or $M_{2}$ is fully on) equal to $V_{R E F}$.

The bandwidth of the op amp $A_{1}$ in Fig. 15.43(b) is of some concern. If a change in $V_{\text {cont }}$ takes a long time to change $\omega_{\text {out }}$, then the settling speed of a PLL using this VCO degrades significantly (Chapter 16).

Example 15.11
How does the oscillation frequency depend on $I_{S S}$ for a VCO incorporating the stage of Fig. 15.43(b)?

#### Solution

Noting that $R_{o n 3,4} I_{S S} \approx V_{D D}-V_{R E F}$, we have $R_{o n 3,4} \approx\left(V_{D D}-V_{R E F}\right) / I_{S S}$, and hence

$$
\begin{align*}
f_{\text {osc }} & \propto \frac{1}{R_{o n 3,4} C_{L}}  \tag{15.68}\\
& \propto \frac{I_{S S}}{\left(V_{D D}-V_{R E F}\right) C_{L}} \tag{15.69}
\end{align*}
$$

Thus, the characteristic is relatively linear.

Delay Variation by Positive Feedback To arrive at another tuning technique, recall that a crosscoupled transistor pair such as that of Fig. 15.36 exhibits a negative resistance of $-2 / g_{m}$, a value that can be controlled by the bias current. A negative resistance $-R_{N}$ placed in parallel with a positive resistance $+R_{P}$ gives an equivalent value $+R_{N} R_{P} /\left(R_{N}-R_{P}\right)$, which is more positive if $\left|-R_{N}\right|>\left|+R_{P}\right|$. This idea can be applied to each stage of a ring oscillator as illustrated in Fig. 15.44(a). Here, the load of the differential pair consists of resistors $R_{1}$ and $R_{2}\left(R_{1}=R_{2}=R_{P}\right)$ and the cross-coupled pair $M_{3}-M_{4}$. As $I_{1}$ increases, the small-signal differential resistance $-2 / g_{m 3,4}$ becomes less negative and, from the half circuit of Fig. 15.44(b), the equivalent resistance $R_{P} \|\left(-1 / g_{m 3,4}\right)=R_{P} /\left(1-g_{m 3,4} R_{P}\right)$ increases, thereby lowering the frequency of oscillation.
image_name:Figure 15.44 (a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: Voutp}
name: R2, type: Resistor, value: R2, ports: {N1: VDD, N2: Voutn}
name: M1, type: NMOS, ports: {S: P, D: Voutp, G: Vip}
name: M2, type: NMOS, ports: {S: P, D: Voutn, G: Vin}
name: M3, type: NMOS, ports: {S: P1, D: Voutp, G: Voutn}
name: M4, type: NMOS, ports: {S: P1, D: Voutn, G: Voutp}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: P1, Nn: GND}
]
extrainfo:The circuit is a differential stage with variable negative-resistance load. It consists of a differential pair (M1 and M2) with resistive loads (R1 and R2) and a cross-coupled pair (M3 and M4). The current sources ISS and I1 provide biasing.

image_name:(b)
description:
[
name: RP, type: Resistor, ports: {N1: VDD, N2: Vout}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: R, type: Resistor,value:-1/gm3,4, ports: {N1: VDD, N2: Vout}
]
extrainfo:The circuit is a half-circuit equivalent of a differential stage with a variable negative-resistance load. It includes a resistor RP connected between VDD and Voutn, and an NMOS transistor M1. The transistor M1 has its source connected to ground, drain to Voutn, and gate to Vin.

Figure 15.44 (a) Differential stage with variable negative-resistance load; (b) half-circuit equivalent of (a).
An important issue in the circuit of Fig. 15.44(a) is that as $I_{1}$ varies, so do the currents steered by $M_{3}$ and $M_{4}$ to $R_{1}$ and $R_{2}$. Thus, the output voltage swing is not constant across the tuning range. To minimize this effect, $I_{S S}$ can be varied in the opposite direction such that the total current steered between $R_{1}$ and $R_{2}$ remains constant. In other words, it is desirable to vary $I_{1}$ and $I_{S S}$ differentially while their sum is fixed, a characteristic provided by a differential pair. Illustrated in Fig. 15.45, the idea is to employ a differential pair $M_{5}-M_{6}$ to steer $I_{T}$ to $M_{1}-M_{2}$ or $M_{3}-M_{4}$ so that $I_{S S}+I_{1}=I_{T}$. Since $I_{T}$ must flow through $R_{1}$ and $R_{2}$, if $M_{1}-M_{4}$ experience complete switching in each cycle of oscillation, then $I_{T}$ is steered to $R_{1}$ (through $M_{1}$ and $M_{3}$ ) in half a period and to $R_{2}$ (through $M_{2}$ and $M_{4}$ ) in the other half, giving a differential swing of $2 R_{P} I_{T}$.
image_name:Figure 15.45
description:The circuit is a differential pair steering current between two branches. M5 and M6 form a differential pair that steers current IT between M1-M2 and M3-M4 branches. The control voltages Vcont1 and Vcont2 determine the steering. The resistors R1 and R2 are connected to VDD, providing a differential output swing across Voutp and Voutn.

Figure 15.45 Use of a differential pair to steer current between $M_{1}-M_{2}$ and $M_{3}-M_{4}$.

In the circuit of Fig. 15.45, $V_{\text {cont } 1}$ and $V_{\text {cont } 2}$ can be viewed as differential control lines if they vary by equal and opposite amounts. Such a topology provides higher noise immunity for the control input than if $V_{\text {cont }}$ is single-ended. Now, note that as $V_{\text {cont } 1}$ decreases and $V_{\text {cont } 2}$ increases, the cross-coupled pair exhibits a greater transconductance, thereby raising the time constant at the output nodes. But what happens if all of $I_{T}$ is steered by $M_{6}$ to $M_{3}$ and $M_{4}$ ? Since $M_{1}$ and $M_{2}$ carry no current, the gain of the stage falls to zero, prohibiting oscillation. To avoid this effect, a small constant current source, $I_{H}$, can be connected from node $P$ to ground, thereby ensuring that $M_{1}$ and $M_{2}$ always remain on. With typical values, this ring oscillator provides a two-to-one tuning range and reasonable linearity.

#### Example 15.12

Calculate the minimum value of $I_{H}$ in Fig. 15.45 to guarantee a low-frequency gain of 2 when all of $I_{T}$ is steered to the cross-coupled pair.

#### Solution

The small-signal voltage gain of the circuit equals $g_{m 1,2} R_{P} /\left(1-g_{m 3,4} R_{P}\right)$. Assuming square-law devices, we have

$$
\begin{equation*}
\sqrt{\mu_{n} C_{o x}\left(\frac{W}{L}\right)_{1,2} I_{H}} \frac{R_{P}}{1-\sqrt{\mu_{n} C_{o x}\left(\frac{W}{L}\right)_{3,4} I_{T} R_{P}}} \geq 2 \tag{15.70}
\end{equation*}
$$

That is

$$
\begin{equation*}
I_{H} \geq \frac{4\left[1-\sqrt{\mu_{n} C_{o x}\left(\frac{W}{L}\right)_{3,4} I_{T}} R_{P}\right]^{2}}{\mu_{n} C_{o x}\left(\frac{W}{L}\right)_{1,2} R_{P}^{2}} \tag{15.71}
\end{equation*}
$$

An important drawback of using the differential pair $M_{5}-M_{6}$ in the circuit of Fig. 15.45 is the additional voltage headroom that it consumes. As depicted in Fig. 15.46, for $M_{5}$ to remain in saturation, $V_{P}$ must be sufficiently higher than $V_{N}$. When $V_{\text {cont } 1}=V_{\text {cont } 2}$, the minimum allowable drain-source voltage of $M_{5}$ is equal to its equilibrium overdrive voltage, implying that, compared to that calculated in Example 15.4,
image_name:Figure 15.46
description:
[
name: M1, type: NMOS, ports: {S: P, D: LOAD1, G: Vip}
name: M2, type: NMOS, ports: {S: P, D: LOAD2, G: Vin}
name: M5, type: NMOS, ports: {S: N, D: P, G: Vcont1}
name: M6, type: NMOS, ports: {S: N, D: LOAD3, G: Vcont2}
name: M7, type: NMOS, ports: {S: GND, D: N, G: Vb}
]
extrainfo:The circuit includes a differential pair M5-M6, which affects voltage headroom. M7 acts as a current sink to ground.

Figure 15.46 Headroom calculation for a current-steering topology.
the supply voltage must be higher by this value. Note also that if $V_{\text {cont } 1}$ or $V_{\text {cont2 }}$ is allowed to vary above its equilibrium value by more than $V_{T H}$, then $M_{5}$ or $M_{6}$ enters the triode region.

The previous observation reveals a trade-off between voltage headroom and the sensitivity of the VCO. In order to minimize the sensitivity with a given tuning range, the transconductance of $M_{5}-M_{6}$ must be minimized. (That is, to steer all of the tail current, the differential pair must require a large $V_{\text {cont } 1}-V_{\text {cont } 2}$.) However, for a given tail current, $g_{m}=2 I_{D} /\left(V_{G S}-V_{T H}\right)$, indicating a large equilibrium overdrive for $M_{5}-M_{6}$ and a correspondingly higher value for the minimum required supply voltage.

We should mention that the pair $M_{5}-M_{6}$ need not remain in complete saturation. If the drain voltages are low enough to drive these transistors into the triode region, then the equivalent transconductance of the differential pair drops, demanding a greater $V_{\text {cont } 1}-V_{\text {cont2 }}$ to steer the tail current. This phenomenon in fact translates to a lower VCO sensitivity. In practice, careful simulations are required to ensure that the VCO characteristic remains relatively linear across the range of interest. ${ }^{9}$
image_name:(a)
description:The circuit represents a current folding topology with differential pairs driving two current mirrors. The NMOS transistors (M1 to M4) form the differential pairs and current mirrors. PMOS transistors (M9 and M10) are used for current steering with control voltages Vcont1 and Vcont2. The circuit is designed to maintain linearity across a range of interest by ensuring the transistors operate within the desired regions.
image_name:(b)
description:The circuit diagram represents a current folding topology applied to current steering. It uses NMOS and PMOS transistors along with resistors and a current source to manage current paths. The PMOS transistors M9 and M10 control the current through the differential pair M1 and M2, which is mirrored by NMOS transistors M3 and M4. The circuit is designed to operate efficiently at low supply voltages by avoiding voltage headroom issues.

Figure 15.47 (a) Current folding topology; (b) application of current folding to current steering.
At low supply voltages, it is desirable to avoid the voltage headroom consumed by $M_{5}-M_{6}$ in Fig. 15.45. The issue can be resolved by means of "current folding." Suppose, as illustrated in Fig. 15.47(a), a differential pair drives two current mirrors, generating $I_{\text {out } 1}$ and $I_{\text {out } 2}$. Since $I_{1}+I_{2}=I_{S S}, I_{\text {out } 1}=K I_{1}$, and $I_{\text {out } 2}=K I_{2}$, we have $I_{\text {out } 1}+I_{\text {out } 2}=K I_{S S}$. Thus, as $V_{\text {in } 1}-V_{\text {in } 2}$ goes from a very negative value to a very positive value, $I_{\text {out } 1}$ varies from $K I_{S S}$ to zero and $I_{\text {out } 2}$ from zero to $K I_{S S}$ while their sum remains constant-a behavior similar to that of a differential pair.

[^108]We now utilize the topology of Fig. 15.47(a) in the gain stage of Fig. 15.44(a). Shown in Fig. 15.47(b), the resulting circuit operates from a low supply voltage. However, the devices in the control path contribute substantial noise, modulating the oscillation frequency.

Delay Variation by Interpolation Another approach to tuning ring oscillators is based on "interpolation" [3, 4]. As illustrated in Fig. 15.48(a), each stage consists of a fast path and a slow path whose outputs are summed and whose gains are adjusted by $V_{\text {cont }}$ in opposite directions. At one extreme of the control voltage, only the fast path is on and the slow path is disabled, yielding the maximum oscillation frequency [Fig. 15.48(b)]. Conversely, at the other extreme, only the slow path is on and the fast path is off, providing the minimum oscillation frequency [Fig. 15.48(c)]. If $V_{\text {cont }}$ lies between the two extremes, each path is partially on, and the total delay is a weighted sum of their delays.
image_name:(a)
description:The diagram labeled (a) represents an interpolating delay stage used in oscillators to control the frequency by adjusting the delay through two paths: a fast path and a slow path.

1. **Main Components:**
- **Input and Output Ports:** The diagram shows an input voltage ($V_{in}$) and an output voltage ($V_{out}$).
- **Fast Path:** This path consists of a single amplifier block which provides a faster delay.
- **Slow Path:** This path includes two amplifier blocks in series, introducing a slower delay.
- **Summation Block:** A summation block combines the outputs of the fast and slow paths.
- **Control Voltage ($V_{cont}$):** A control signal that adjusts the contribution of each path to the output.

2. **Flow of Information or Control:**
- The input voltage ($V_{in}$) is fed into both the fast and slow paths.
- The fast path directly connects to the summation block with one amplifier, providing a quicker response.
- The slow path, consisting of two amplifiers, also connects to the summation block but with a longer delay.
- The control voltage ($V_{cont}$) modulates the signals from both paths, allowing for interpolation between the delays.

3. **Labels, Annotations, and Key Indicators:**
- The paths are clearly labeled as "Fast Path" and "Slow Path."
- The control voltage ($V_{cont}$) is indicated as influencing both paths, showing its role in adjusting the delay.

4. **Overall System Function:**
- The primary function of this system is to provide a controllable delay stage that can interpolate between a fast and slow response. By adjusting $V_{cont}$, the system can achieve a range of oscillation frequencies, with the fast path providing the minimum delay and the slow path providing the maximum delay. The summation block combines the outputs of both paths, weighted by the control voltage, to produce the final output ($V_{out}$). This mechanism allows for fine-tuning of the oscillator's frequency.
image_name:(b)
description:The system block diagram labeled as (b) illustrates a configuration for achieving the smallest delay in an interpolating delay stage. This diagram consists of two main paths: a fast path and a slow path, with the focus on the fast path being fully active and the slow path being disabled, as indicated by the greyed-out components.

1. **Main Components:**
- **Amplifiers:** The diagram includes two amplifier blocks in series along the fast path. These amplifiers are responsible for processing the input signal and providing the necessary gain to achieve fast signal propagation.
- **Summing Junction:** There is a summing junction (depicted as a circle with a plus sign) that combines signals from different paths. In this configuration, it primarily processes the output from the fast path.

2. **Flow of Information or Control:**
- The input signal, denoted as a single arrow entering the first amplifier, passes through the fast path amplifiers.
- The output of the first amplifier is fed directly into the summing junction.
- The output of the summing junction is then fed into another amplifier, which processes the combined signal before producing the final output.
- The slow path is shown but inactive, indicated by the greyed-out amplifiers and connections, meaning no signal is processed through this path in this configuration.

3. **Labels, Annotations, and Key Indicators:**
- The fast path is highlighted with bold lines, emphasizing its active role in this configuration.
- The greyed-out components of the slow path indicate that they are not contributing to the signal delay in this setup.

4. **Overall System Function:**
- The primary function of this configuration is to achieve the minimum delay by utilizing only the fast path. This is accomplished by disabling the slow path, ensuring that the signal propagates as quickly as possible through the active amplifiers and summing junction. The control voltage, $V_{\text{cont}}$, is adjusted such that it enables only the fast path, aligning with the requirement for the smallest possible delay.
image_name:(c)
description:The block diagram labeled (c) illustrates a delay stage configuration where only the slow path is active. This setup provides the largest delay in the system.

1. **Main Components:**
- **Input and Output:** The diagram includes an input point on the left and an output point on the right.
- **Amplifiers/Inverters:** There are two amplifiers (or inverters) in series along the slow path, depicted as triangles pointing to the right, which indicate signal amplification or inversion.
- **Summing Junctions:** Two summing junctions, represented by circles with a plus sign inside, are present. These are used to combine signals from different paths.

2. **Flow of Information or Control:**
- The signal enters from the left, first encountering a summing junction, which is primarily involved in combining signals from different paths.
- The signal then passes through the two amplifiers in the slow path, which introduce a delay.
- After passing through the amplifiers, the signal reaches another summing junction, where it is combined with other potential signal paths (though in this configuration, only the slow path is active).
- Finally, the processed signal exits to the right.

3. **Labels, Annotations, and Key Indicators:**
- The slow path is emphasized in bold, indicating that it is the active path in this configuration.
- The fast path components are shown in a lighter shade, indicating they are inactive.

4. **Overall System Function:**
- The primary function of this configuration is to provide the maximum delay by utilizing only the slow path. The control voltage, $V_{\text{cont}}$, is set such that the fast path is disabled, and the slow path is fully active, resulting in the longest possible delay in signal processing. This setup is crucial for applications requiring precise timing adjustments where slower signal propagation is necessary.

Figure 15.48 (a) Interpolating delay stage; (b) smallest delay; (b) largest delay.

To better understand the concept of interpolation, let us implement the topology of Fig. 15.48(a) at the transistor level. Each stage can be simply realized as a differential pair whose gain is controlled by its tail current. But how are the two outputs summed? Since the two transistors in a differential pair provide output currents, the outputs of the two pairs can be added in the current domain. As depicted in Fig. 15.49(a), simply shorting the outputs of two pairs performs the current addition, e.g., for small signals, $I_{o u t}=g_{m 1,2} V_{i n 1}+g_{m 3,4} V_{i n 2}$. The overall interpolating stage therefore assumes the configuration shown in Fig. 15.49(b), where $V_{\text {cont }}^{+}$and $V_{\text {cont }}^{-}$denote voltages that vary in opposite directions (so that when one path turns on, the other turns off). The output currents of $M_{1}-M_{2}$ and $M_{3}-M_{4}$ are summed at $X$ and $Y$ and flow through $R_{1}$ and $R_{2}$, producing $V_{\text {out }}$.

In the circuit of Fig. 15.49(b), the gain of each stage is varied by the tail current to achieve interpolation. But it is desirable to maintain constant voltage swings. We also recognize that the gain of the differential pair $M_{5}-M_{6}$ need not be varied because even if only the gain of $M_{3}-M_{4}$ drops to zero, the slow path is fully disabled. We then surmise that if the tail currents of $M_{1}-M_{2}$ and $M_{3}-M_{4}$ vary in opposite directions such that their sum remains constant, we achieve both interpolation between the two paths and constant output swings. Illustrated in Fig. 15.50, the resulting circuit employs the differential pair $M_{7}-M_{8}$ to steer $I_{S S}$ between $M_{1}-M_{2}$ and $M_{3}-M_{4}$. If $V_{\text {cont }}$ is very negative, $M_{8}$ is off and only the fast path amplifies the input. Conversely, if $V_{\text {cont }}$ is very positive, $M_{7}$ is off and only the slow path is enabled. Since the
image_name:(a)
description:This circuit is a differential pair configuration with NMOS transistors M1-M4. It combines the outputs of two differential pairs to produce outputs Iout1 and Iout2. The current source Iss provides biasing.
image_name:(b)
description:The circuit is an interpolating delay stage with current steering, using differential pairs M1-M2 and M3-M4 for signal processing. The control voltage Vcont steers the current between these paths to adjust the delay. Resistors R1 and R2 are used for load balancing, and the current source Iss provides biasing.

Figure 15.49 (a) Addition of currents of two differential pairs; (b) interpolating delay stage.
image_name:Figure 15.50
description:The circuit is an interpolating delay stage with current steering, using differential pairs M1-M2 and M3-M4 for signal processing. The control voltage Vcont steers the current between these paths to adjust the delay. Resistors R1 and R2 are used for load balancing, and the current source Iss provides biasing. The slow path employs one more stage than the fast path, achieving a tuning range of roughly two to one.

Figure 15.50 Interpolating delay stage with current steering.
slow path in this case employs one more stage than the fast path, the VCO achieves a tuning range of roughly two to one. For operation with low supply voltages, the control pair $M_{7}-M_{8}$ can be replaced by the current-folding topology of Fig. 15.47(a).

#### Example 15.13

Combine the tuning techniques of Figs. 15.45 and 15.50 to achieve a wider tuning range.

#### Solution

We begin with the interpolating stage of Fig. 15.50 and add a cross-coupled pair to the output nodes [Fig. 15.51(a)]. However, in order to obtain constant voltage swings, the total current through the load resistors must remain
image_name:(a)
description:The circuit is a differential amplifier configuration with cross-coupled NMOS transistors (M10, M11) for improved performance. It includes PMOS transistors (M1, M2) forming a differential pair, NMOS transistors (M3, M4) for current mirroring, and NMOS transistors (M5, M6) as current sources. Resistors R1 and R2 are connected to VDD for load, and the current source Iss provides biasing. The Vcont node is used for controlling the current flow through the cross-coupled NMOS transistors.
image_name:(b)
description:The circuit diagram (b) shows a wide-range tuning circuit with PMOS and NMOS transistors. The PMOS transistors M1 and M2 form a differential pair driven by Vin. NMOS transistors M3 and M4 are connected to the output Vout. The circuit uses current sources ISS1, ISS2, and ISS3 to control the current distribution. Resistors R1 and R2 are connected between VDD and Vout. Transistors M10 and M11 are used for current steering controlled by Vcont. The circuit is designed for wide-range tuning by adjusting the current distribution through the transistors.

Figure 15.51
constant. This is accomplished by replacing the control differential pair with the current-folding circuit of Fig. 15.47(a). Depicted in Fig. 15.51(b), the resulting configuration steers the current to $M_{1}-M_{2}$ to speed up the circuit and to $M_{3}-M_{4}$ and $M_{10}-M_{11}$ to slow down the circuit. The tail current source dimensions are chosen such that $I_{S S 1}=I_{S S 2}+I_{S S 3}$.

Wide-Range Tuning Except for the circuit of Fig. 15.43(b), the ring oscillator tuning techniques presented thus far achieve a tuning range of typically no more than three to one. In applications where the frequency must be varied by orders of magntitude, the topology shown in Fig. 15.52 can be used. Driven by the input, the additional PMOS transistors $M_{5}$ and $M_{6}$ pull each output node to $V_{D D}$, creating a relatively constant output swing even with large variations in $I_{S S}$. The oscillation frequency of a ring incorporating this stage can be varied by more than four orders of magnitude with less than a twofold variation in the amplitude.
image_name:Figure 15.52 Differential stage with wide tuning range
description:
[
name: M1, type: NMOS, ports: {S: P, D: VoutP, G: Vip}
name: M2, type: NMOS, ports: {S: P, D: VoutN, G: Vin}
name: M3, type: PMOS, ports: {S: VDD, D: VoutP, G: Voutp}
name: M4, type: PMOS, ports: {S: VDD, D: VoutN, G: Vboutn}
name: M5, type: PMOS, ports: {S: VDD, D: Voutp, G: Vip}
name: M6, type: PMOS, ports: {S: VDD, D: Voutn, G: Vin}
name: ISS, type: CurrentSource, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential stage with a wide tuning range. PMOS transistors M5 and M6 are used to pull each output node to VDD, maintaining constant output swing despite variations in ISS. The oscillation frequency can be varied by more than four orders of magnitude with minimal amplitude variation.

Figure 15.52 Differential stage with wide tuning range.

### 15.4.2 Tuning in LC Oscillators

The oscillation frequency of LC topologies is equal to $f_{\text {osc }}=1 /(2 \pi \sqrt{L C})$, suggesting that only the inductor and capacitor values can be varied to tune the frequency, and other parameters such as bias currents and transistor transconductances affect $f_{\text {osc }}$ negligibly. Since it is difficult to vary the value of monolithic inductors, we simply change the tank capacitance to tune the oscillator. Voltage-dependent capacitors are called "varactors." 10

A reverse-biased $p n$ junction can serve as a varactor. The voltage dependence is expressed as

$$
\begin{equation*}
C_{v a r}=\frac{C_{0}}{\left(1+\frac{V_{R}}{\phi_{B}}\right)^{m}} \tag{15.72}
\end{equation*}
$$

where $C_{0}$ is the zero-bias value, $V_{R}$ the reverse-bias voltage, $\phi_{B}$ the built-in potential of the junction, and $m$ a value typically between 0.3 and 0.4. ${ }^{11}$ Equation (15.72) reveals an important drawback of LC oscillators: at low supply voltages, $V_{R}$ has a very limited range, yielding a small range for $C_{v a r}$ and hence for $f_{\text {osc }}$. We also note that to maximize the tuning range, constant capacitances in the tank must be minimized.

#### Example 15.14

Suppose that in Eq. (15.72), $\phi_{B}=0.7 \mathrm{~V}, m=0.35$, and $V_{R}$ can vary from zero to 2 V . How much tuning range can be achieved?

#### Solution

For $V_{R}=0, C_{j}=C_{0}$ and $f_{\text {osc }, \min }=1 /\left(2 \pi \sqrt{L C_{0}}\right)$. For $V_{R}=2 \mathrm{~V}, C_{j} \approx 0.62 C_{0}$ and $f_{\text {osc }, \max }=1 /$ $\left(2 \pi \sqrt{L \times 0.62 C_{0}}\right) \approx 1.27 f_{\text {osc }, \text { min }}$. Thus, the tuning range is approximately equal to $27 \%$. As explained later, the parasitic capacitances of the inductor and the transistor(s) further limit this range because they cannot be varied by the control voltage.

Let us now add varactor diodes to a cross-coupled LC oscillator (Fig. 15.53). To avoid forward-biasing $D_{1}$ and $D_{2}$ significantly, $V_{\text {cont }}$ must not exceed $V_{X}$ or $V_{Y}$ by more than a few hundred millivolts. Thus, if the peak amplitude at each node is $A$, then $0<V_{\text {cont }}<V_{D D}-A+300 \mathrm{mV}$, where it is assumed that a forward bias of 300 mV creates negligible current. Interestingly, the circuit suffers from a trade-off between the output swing and the tuning range. This effect appears in most LC oscillators.

image_name:Figure 15.53 LC oscillator using varactor diodes
description:
[
name: LP1, type: Inductor, value: LP, ports: {N1: VDD, N2: X}
name: LP2, type: Inductor, value: LP, ports: {N1: VDD, N2: Y}
name: D1, type: Diode, ports: {Na: Vcont, Nc: X}
name: D2, type: Diode, ports: {Na: Vcont, Nc: Y}
name: M1, type: NMOS, ports: {S: P, D: X, G: Y}
name: M2, type: NMOS, ports: {S: P, D: Y, G: X}
name: IS, type: CurrentSource, value: IS, ports: {Np: Vcont, Nn: GND}
]
extrainfo:The circuit is an LC oscillator using varactor diodes. It includes two inductors LP, two diodes D1 and D2, and two NMOS transistors M1 and M2. The current source IS provides biasing. The oscillator's tuning range is controlled by Vcont, which should be kept within a specific range to avoid significant forward-biasing of the diodes.
image_name:Allowable Range of Vcont
description:The graph titled "Allowable Range of Vcont" is a conceptual illustration related to an LC oscillator circuit using varactor diodes. This graph is not a typical function graph with numerical axes but rather a schematic representation of voltage levels.

1. **Type of Graph and Function:**
- The graph is a schematic diagram illustrating the voltage levels and allowable range for the control voltage, \( V_{\text{cont}} \), in the context of an LC oscillator circuit.

2. **Axes Labels and Units:**
- The vertical axis represents voltage levels, but specific units are not labeled as this is a conceptual diagram.
- The horizontal axis is not explicitly labeled but implies time progression as it shows oscillatory behavior.

3. **Overall Behavior and Trends:**
- The graph shows oscillations with peak amplitude \( A \) around nodes \( V_X \) and \( V_Y \).
- The oscillations are depicted as sinusoidal waves indicating the voltage swings at nodes \( X \) and \( Y \).
- The allowable range for \( V_{\text{cont}} \) is depicted as a vertical bracket, indicating it must lie between 0 and \( V_{DD} - A \).

4. **Key Features and Technical Details:**
- The oscillations have a peak-to-peak amplitude \( A \), and the mean voltage level is between \( V_X \) and \( V_Y \).
- The allowable range for \( V_{\text{cont}} \) ensures that it does not forward-bias the diodes \( D_1 \) and \( D_2 \) significantly.
- The diagram emphasizes the importance of maintaining \( V_{\text{cont}} \) within the specified range to avoid affecting the oscillator's performance.

5. **Annotations and Specific Data Points:**
- The diagram includes annotations for \( V_X \), \( V_Y \), \( V_{DD} \), and the allowable range for \( V_{\text{cont}} \).
- The allowable range is visually represented by the vertical arrow labeled "Allowable Range of Vcont," showing it spans from 0 to \( V_{DD} - A \).

Figure 15.53 LC oscillator using varactor diodes.

Note that, since the swings at $X$ and $Y$ are typically large (e.g., $1 \mathrm{~V}_{p p}$ at each node), the capacitance of $D_{1}$ and $D_{2}$ varies with time. Nonetheless, the "average" value of the capacitance is still a function of $V_{\text {cont }}$, providing the tuning range.

How are varactor diodes realized in CMOS technology? Illustrated in Fig. 15.54 are two types of $p n$ junctions. In Fig. 15.54(a), the anode is inevitably grounded whereas in Fig. 15.54(b), both terminals are floating. For the circuit of Fig. 15.53, only the floating diode can be used. To increase the capacitance of the junction, the $p^{+}$and $n^{+}$areas (and hence the $n$-well) are enlarged.
image_name:(a)
description:The diagram shows two types of pn junction diodes in CMOS technology. In (a), the anode is grounded, while in (b), both terminals are floating. The diagram illustrates the side and top views of the diodes.
image_name:(b)
description:The circuit diagram (b) shows a floating pn junction diode structure in a CMOS technology, where both terminals are not connected to ground. The n-well introduces additional resistance and capacitance to the substrate, affecting the quality factor and tuning range.

Figure 15.54 Diodes realized in CMOS technology.
Upon closer examination, the structure of Fig. 15.54(b) suffers from a number of drawbacks. First, the $n$-well material has a high resistivity, creating a resistance in series with the reverse-biased diode and lowering the quality factor of the capacitance. Second, the $n$-well displays substantial capacitance to the substrate, contributing a constant capacitance to the tank and limiting the tuning range. The diode is therefore represented as shown in Fig. 15.55, where $C_{n}$ represents the (voltage-dependent) capacitance between the $n$-well and the substrate. ${ }^{12}$
image_name:Figure 15.55
description:The circuit represents a varactor model with a diode, series resistance, and parallel capacitance to ground.

Figure 15.55 Circuit model of the varactor shown in Fig. 15.54(b).

In order to decrease the series resistance of the structure shown in Fig. 15.54(b), the $p^{+}$region can be surrounded by an $n^{+}$ring so that the displacement current flowing through the junction capacitance sees a low resistance in all four directions [Fig. 15.56(a)]. Since a single minimum-size $p^{+}$area has a small capacitance, many of these units can be placed in parallel [Fig. 15.56(b)]. The $n$-well, however, must accommodate the entire set, exhibiting a large capacitance to the substrate.
image_name:Figure 15.56 (a)
description:The diagram shows a structure for reducing series resistance in a semiconductor device by surrounding a p+ region with an n+ ring. This configuration helps lower the resistance in all directions for displacement current through the junction capacitance. In part (b), multiple p+ regions are placed in parallel within an n+ well, increasing capacitance to the substrate.
image_name:Figure 15.56 (b)
description:The circuit diagram in Figure 15.56 (b) depicts several $p^{+}$ regions surrounded by $n^{+}$ rings, arranged in parallel to form a diode array. This configuration is designed to reduce series resistance by allowing displacement current to flow through the junction capacitance in all directions. The $n$-well accommodates the entire set of diodes, resulting in a large capacitance to the substrate. The diagram illustrates a layout strategy for optimizing the performance of diode arrays in integrated circuits by minimizing resistive losses and enhancing current distribution.

Figure 15.56 (a) Reduction of series resistance by surrounding the $p^{+}$region by an $n^{+}$ring; (b) several diodes in parallel.

It is instructive at this point to examine the unwanted capacitances in the circuit of Fig. 15.53, i.e., the components that are not varied by $V_{\text {cont }}$. We identify three such capacitances: (1) the capacitance between the $n$-well and the substrate associated with $D_{1}$ and $D_{2}$; (2) the capacitances contributed by the transistors to each node, i.e., $C_{G D}, 2 C_{G D}$ (the factor of 2 arising from the Miller effect ${ }^{13}$ ), and $C_{D B}$; and (3) the parasitic capacitance of the inductor itself. Monolithic inductors are typically implemented as metal spiral structures (Fig. 15.57) having relatively large dimensions ( $S \approx 100-200 \mu \mathrm{~m}$ ).
image_name:Figure 15.57 Spiral inductor structure
description:The image depicts a spiral inductor structure, which is typically implemented as a metal spiral. This structure is characterized by its large dimensions, indicated by the label \( S \), which measures approximately 100-200 micrometers (\( \mu \mathrm{m} \)).

The spiral inductor is shown as a series of concentric loops, forming a spiral pattern. The structure is designed to create inductance, which is a fundamental component in many RF and analog circuits. The inductor's spiral shape increases the length of the conductor while keeping the overall footprint compact, maximizing inductance within a given area.

There are arrows labeled \( I \) pointing towards and away from the spiral, indicating the direction of current flow through the inductor. This suggests the inductor's role in allowing current to flow in and out, contributing to its inductive properties.

Additionally, the image shows connections to ground via capacitors at two points along the spiral. This indicates the presence of parasitic capacitances associated with the inductor, which are often considered in the design and analysis of such components to account for their effect on the inductor's performance.

Overall, the image illustrates the physical layout and connections of a monolithic spiral inductor, highlighting its key features and the interactions between the inductor and its surrounding components.

Figure 15.57 Spiral inductor structure.

In Fig. 15.53, it is desirable to connect the anode of the diodes to nodes $X$ and $Y$, thereby eliminating the parasitic $n$-well capacitances from the tank. Shown in Fig. 15.58 is a topology allowing such a modification. Here, the cross-coupled pair incorporates PMOS devices, providing swings around the ground potential. The use of PMOS devices also leads to less flicker noise, an important advantage because this noise may be "upconverted," appearing around the oscillation frequency.

In modern LC VCO design, we employ MOS varactors. Recall from Chapter 2 that the gate-channel capacitance of MOSFETs varies with the gate-source voltage [Fig. 15.59(a)]. However, the nonmonotonic dependence proves undesirable in VCO design (why?). To resolve this issue, an NMOS transistor can be placed inside an $n$-well, forming an "accumulation-mode" varactor [Fig. 15.59(b)]. The source, drain, and $n$-well are ohmically connected and serve as one terminal, and the gate as the other. The capacitance of this structure varies monotonically with $V_{G S}$, as shown in Fig. 15.59(c).

image_name:Figure 15.58
description:The circuit is a negative-Gm oscillator using PMOS devices to eliminate n-well capacitance from the tanks. It utilizes a pair of cross-coupled PMOS transistors with diodes and inductors to form a resonant tank circuit. The voltage source VDD powers the oscillator, and the control voltage Vcont adjusts the frequency of oscillation.
image_name:(a)
description:The graph labeled (a) is a plot illustrating the voltage dependence of a MOS gate capacitance, specifically the gate-source capacitance (C_GS) as a function of the gate-source voltage (V_GS).

1. **Type of Graph and Function**: This is a capacitance-voltage (C-V) characteristic curve for a MOSFET.

2. **Axes Labels and Units**:
- The horizontal axis represents the gate-source voltage (V_GS), starting from zero and increasing towards the right.
- The vertical axis represents the gate-source capacitance (C_GS), with the direction of increase going upwards.

3. **Overall Behavior and Trends**:
- The curve shows a non-monotonic behavior. Initially, as V_GS starts from zero, C_GS is high, indicating the accumulation region.
- As V_GS increases towards a threshold voltage (V_TH), the capacitance decreases, reaching a minimum point. This region is typically associated with depletion.
- Beyond V_TH, the capacitance increases again as the MOSFET enters the strong inversion region.

4. **Key Features and Technical Details**:
- The graph has a distinct minimum point at the threshold voltage (V_TH), marking the transition from depletion to strong inversion.
- The curve shows two major regions: **Accumulation** on the left, where C_GS is high, and **Strong Inversion** on the right, where C_GS rises again after the minimum.
- The minimum capacitance value occurs at V_TH, which is a critical point in the graph.

5. **Annotations and Specific Data Points**:
- The graph is annotated with the terms "Accumulation" and "Strong Inversion" to denote the regions on either side of the minimum capacitance point.
- The threshold voltage (V_TH) is marked on the V_GS axis, indicating the point of minimum capacitance.
image_name:(b)
description:The image labeled as Figure 15.59(b) depicts a schematic of a MOS varactor, specifically an NMOS transistor placed inside an n-well. This structure is used to create an accumulation-mode varactor. The diagram shows the NMOS transistor with its source, drain, and n-well ohmically connected to serve as one terminal, while the gate is used as the other terminal. The n-well is embedded in a p-substrate, which provides isolation.

In this configuration, the voltage applied between the gate (V_G) and the source (V_S) controls the capacitance of the varactor. The schematic illustrates how the capacitance (C_GS) varies monotonically with the gate-source voltage (V_GS), as opposed to the nonmonotonic behavior typically seen in standard MOSFETs. This monotonic relationship is crucial for applications in voltage-controlled oscillators (VCOs), as it allows for predictable tuning of the oscillator frequency.

This setup is advantageous over a traditional pn junction varactor because it can handle both positive and negative voltages without entering forward bias, thus offering greater flexibility in circuit design. The diagram does not include detailed electrical connections or component values, focusing instead on the conceptual layout and function of the MOS varactor within the n-well structure.
image_name:(c)
description:The graph labeled as Fig. 15.59(c) is a plot illustrating the capacitance behavior of an accumulation-mode varactor as a function of gate-source voltage (V_GS).

1. **Type of Graph and Function:**
- This is a capacitance versus voltage graph, showing how the gate-source capacitance (C_GS) of a MOS varactor changes with varying gate-source voltage (V_GS).

2. **Axes Labels and Units:**
- The horizontal axis represents the gate-source voltage (V_GS), starting from 0 and increasing in the positive direction, although specific voltage units are not labeled.
- The vertical axis represents the gate-source capacitance (C_GS), with a range from a minimum capacitance (C_min) to a maximum capacitance (C_max).

3. **Overall Behavior and Trends:**
- The graph shows a monotonically increasing trend of capacitance with increasing V_GS.
- Starting from a minimum capacitance (C_min) at V_GS = 0, the capacitance increases gradually as V_GS increases.
- This behavior contrasts with the nonmonotonic trend seen in traditional MOSFET capacitance characteristics, as described in Fig. 15.59(a).

4. **Key Features and Technical Details:**
- The graph highlights a smooth, continuous increase in capacitance, indicating the absence of abrupt changes or inflection points within the range shown.
- The capacitance reaches a maximum value (C_max) as V_GS increases, suggesting a saturation effect or limit in capacitance.

5. **Annotations and Specific Data Points:**
- There are no specific numerical values or annotations provided on the graph, but the general trend from C_min to C_max is clearly depicted.

This graph effectively demonstrates the desirable monotonic capacitance behavior of an accumulation-mode varactor, which is beneficial for voltage-controlled oscillator (VCO) design, as it avoids the nonmonotonic issues seen in other MOSFET configurations.

Figure 15.59 (a) Voltage dependence of a MOS gate capacitance, (b) MOS varactor formed as an NFET inside an n-well, and (c) resulting characteristic.

An important advantage of the MOS varactor over the $p n$ junction is that the former does not experience forward bias and can therefore tolerate both positive and negative voltages. The design of LC VCOs entails numerous interesting concepts and issues. The reader is referred to [5] and the vast literature on the subject for details.

## 15.5 Mathematical Model of VCOs

The definition of the voltage-controlled oscillator given by Eq. (15.55) specifies the relationship between the control voltage and the output frequency. The dependence is "memoryless" because a change in $V_{\text {cont }}$ immediately results in a change in $\omega_{\text {out }}$. But how is the output signal of the VCO expressed as a function of time? To answer this question, we must review the concepts of phase and frequency.

Consider the waveform $V_{0}(t)=V_{m} \sin \omega_{0} t$. The argument of the sinusoid is called the "total phase" of the signal. In this example, the phase varies linearly with time, exhibiting a slope equal to $\omega_{0}$. Note that, as depicted in Fig. 15.60, every time $\omega_{0} t$ crosses an integer multiple of $\pi, V_{0}(t)$ crosses zero.
image_name:Figure 15.60
description:The graph in Figure 15.60 consists of two parts: a phase plot and a time-domain waveform plot.

1. **Type of Graph and Function**:
- The top portion of the graph is a phase plot showing the linear variation of phase over time.
- The bottom portion is a time-domain waveform representing a sinusoidal signal.

2. **Axes Labels and Units**:
- The top graph has the y-axis labeled as 'Phase' with units in multiples of \( \pi \) (\( \pi, 2\pi, 3\pi, 4\pi \)). The x-axis is labeled as time \( t \), but no specific units are provided.
- The bottom graph has the y-axis labeled as \( V_0(t) \), indicating the voltage of the sinusoidal waveform, and the x-axis is also labeled as time \( t \).

3. **Overall Behavior and Trends**:
- In the phase plot, the phase increases linearly with time, represented by a straight line with a slope of \( \omega_0 \), indicating a constant angular frequency.
- In the waveform plot, \( V_0(t) \) is a sinusoidal waveform oscillating around zero. It crosses the time axis at regular intervals, corresponding to the phase crossing integer multiples of \( \pi \).

4. **Key Features and Technical Details**:
- The phase plot shows the phase linearly increasing, indicating a constant frequency \( \omega_0 \).
- The waveform plot shows periodic zero crossings, peaks, and troughs, consistent with the sinusoidal nature of \( V_0(t) = V_m \sin(\omega_0 t) \).
- The zero crossings of \( V_0(t) \) occur at the points where the phase is an integer multiple of \( \pi \), illustrating the relationship between phase and waveform.

5. **Annotations and Specific Data Points**:
- The phase plot includes dashed lines extending from integer multiples of \( \pi \) down to the corresponding zero crossings in the waveform plot, highlighting the correlation between phase values and zero crossings of the sinusoid.
- There are no specific numerical values for amplitude or frequency provided in the plot.

Figure 15.60 Illustration of phase of a signal.

Now consider two waveforms $V_{1}(t)=V_{m} \sin \left[\phi_{1}(t)\right]$ and $V_{2}(t)=V_{m} \sin \left[\phi_{2}(t)\right]$, where $\phi_{1}(t)=$ $\omega_{1} t, \phi_{2}(t)=\omega_{2} t$, and $\omega_{1}<\omega_{2}$. As illustrated in Fig. 15.61, $\phi_{2}(t)$ crosses integer multiples of $\pi$ faster than $\phi_{1}(t)$ does, yielding faster variations in $V_{2}(t)$. We say that $V_{2}(t)$ accumulates phase faster.
image_name:Figure 15.61
description:The graph in Figure 15.61 illustrates the variation of phase for two sinusoidal signals, $V_1(t)$ and $V_2(t)$, over time. This is a time-domain waveform graph.

1. **Axes Labels and Units:**
- The horizontal axis represents time ($t$), though specific units are not provided.
- The vertical axis on the upper part of the graph shows phase in multiples of $\pi$ (e.g., $\pi$, $2\pi$, $3\pi$, etc.).

2. **Overall Behavior and Trends:**
- The graph shows two lines, $\phi_1(t)$ and $\phi_2(t)$, representing the phase of the signals $V_1(t)$ and $V_2(t)$, respectively.
- $\phi_2(t)$ increases more steeply than $\phi_1(t)$, indicating that $V_2(t)$ has a higher frequency than $V_1(t)$. This is because $\omega_2 > \omega_1$.
- Below the phase lines, two sinusoidal waveforms, $V_1(t)$ and $V_2(t)$, are depicted. $V_2(t)$ completes more cycles within the same time frame compared to $V_1(t)$, confirming its higher frequency.

3. **Key Features and Technical Details:**
- The graph highlights how $V_2(t)$ accumulates phase faster than $V_1(t)$, crossing integer multiples of $\pi$ more frequently.
- The phase lines are linear, indicating constant frequencies for both signals.

4. **Annotations and Specific Data Points:**
- The phase lines are marked with $\phi_1$ and $\phi_2$ to differentiate between the two signals.
- Dashed vertical lines connect the points where the phase lines cross multiples of $\pi$ to the corresponding points on the sinusoidal waveforms, illustrating the relationship between phase accumulation and waveform oscillation.

This graph effectively demonstrates the concept that a faster phase variation corresponds to a higher frequency waveform, as seen with $V_2(t)$ compared to $V_1(t)$. The linear increase in phase with time for both waveforms reflects their sinusoidal nature and constant frequency.

Figure 15.61 Variation of phase for two signals.

The above study reveals that the faster the phase of a waveform varies, the higher the frequency of the waveform, suggesting that the frequency ${ }^{14}$ can be defined as the derivative of the phase with respect to time:

$$
\begin{equation*}
\omega=\frac{d \phi}{d t} \tag{15.73}
\end{equation*}
$$

#### Example 15.15

Figure 15.62(a) shows the phase of a sinusoidal waveform with constant amplitude as a function of time. Plot the waveform in the time domain.

[^112]image_name:(a)
description:The graph in Figure 15.62(a) is a time-domain plot representing the phase \( \phi(t) \) of a sinusoidal waveform as a function of time \( t \). The x-axis is labeled \( t \), representing time, and the y-axis is labeled \( \phi(t) \), representing the phase of the waveform. The plot uses a linear scale for both axes.

Overall Behavior and Trends:
The graph depicts a piecewise linear function, where the phase \( \phi(t) \) increases over time. The function is characterized by segments of constant slope, indicating steady rates of phase change. These segments suggest that the frequency of the waveform changes periodically over time.

Key Features and Technical Details:
- The graph shows two distinct slopes, labeled \( \omega_1 \) and \( \omega_2 \), indicating different frequencies.
- The lower slope \( \omega_1 \) represents a slower rate of phase change, corresponding to a lower frequency.
- The higher slope \( \omega_2 \) represents a faster rate of phase change, corresponding to a higher frequency.
- The phase alternates between these two rates, suggesting a waveform that periodically changes its frequency.

Annotations and Specific Data Points:
- The graph includes dashed lines to highlight the transitions between the different slopes, emphasizing the change in frequency from \( \omega_1 \) to \( \omega_2 \).
- There are no specific numerical values provided for \( \omega_1 \) and \( \omega_2 \), but the relative difference in slopes is visually apparent.

This graph effectively illustrates the concept that the frequency of a waveform can be understood as the derivative of its phase with respect to time, as outlined in the context provided.

image_name:(a)
description:The graph labeled as "(a)" is a time-domain waveform representing frequency modulation. The horizontal axis is labeled as \( t \), denoting time, though the specific units are not provided. The vertical axis is labeled \( \omega(t) \), representing angular frequency.

This graph illustrates a binary frequency modulation, specifically frequency shift keying (FSK), where the frequency alternates between two discrete levels: \( \omega_1 \) and \( \omega_2 \). The waveform is a rectangular step function showing periodic toggling between these two frequencies.

- **Type of Graph:** Time-domain waveform.
- **Axes Labels:** The x-axis is time (\( t \)), and the y-axis is angular frequency (\( \omega(t) \)).
- **Overall Behavior:** The graph shows a periodic square wave pattern, alternating between two levels. This pattern indicates the switching of frequency from \( \omega_2 \) to \( \omega_1 \) and back to \( \omega_2 \), continuing in this manner.
- **Key Features:** The waveform consists of flat segments at \( \omega_2 \) and elevated segments at \( \omega_1 \). The transitions between these levels are instantaneous, depicted by vertical lines, highlighting the change in frequency.
- **Annotations:** The levels are annotated as \( \omega_1 \) and \( \omega_2 \), but no specific numerical values are given. The graph effectively demonstrates the concept of frequency shift keying used in communication systems.

image_name:Fig. 15.62(b)
description:**Type of Graph and Function:**
The graph is a time-domain waveform representing a signal with varying frequency over time.

**Axes Labels and Units:**
- The horizontal axis is labeled as 't', representing time. No specific units or scale are provided, but it is typically assumed to be in seconds for time-domain graphs.
- The vertical axis is labeled as 'V_o(t)', representing the output voltage at time 't'. No specific units or scale are provided, but voltage is typically measured in volts.

**Overall Behavior and Trends:**
The waveform shows a clear pattern of oscillations with varying frequency. Initially, the frequency is lower, with longer wavelengths, and as time progresses, the frequency increases, resulting in shorter wavelengths. This indicates a frequency modulation where the frequency of the waveform increases over time.

**Key Features and Technical Details:**
- The waveform does not show any changes in amplitude, suggesting that the modulation is purely frequency-based.
- The transition from lower to higher frequency appears smooth and continuous, without abrupt changes.

**Annotations and Specific Data Points:**
- There are no additional annotations or specific data points marked on the graph. The focus is on the changing frequency pattern, characteristic of frequency modulation.

#### Solution

Taking the time derivative of $\phi(t)$, we obtain the behavior illustrated in Fig. 15.62(b). The frequency therefore periodically toggles between $\omega_{1}$ and $\omega_{2}$, yielding the waveform shown in Fig. 15.62(c). (This is a simple example of binary frequency modulation, called "frequency shift keying" and utilized in wireless pagers and many other communication systems.)

Equation (15.73) indicates that, if the frequency of a waveform is known as a function of time, then the phase can be computed as

$$
\begin{equation*}
\phi=\int \omega d t+\phi_{0} \tag{15.74}
\end{equation*}
$$

In particular, since for a $\mathrm{VCO}, \omega_{o u t}=\omega_{0}+K_{V C O} V_{c o n t}$, we have

$$
\begin{align*}
V_{\text {out }}(t) & =V_{m} \cos \left(\int \omega_{\text {out }} d t+\phi_{0}\right)  \tag{15.75}\\
& =V_{m} \cos \left(\omega_{0} t+K_{V C O} \int V_{c o n t} d t+\phi_{0}\right) \tag{15.76}
\end{align*}
$$

Equation (15.76) proves essential in the analysis of VCOs and PLLs. ${ }^{15}$ The initial phase $\phi_{0}$ is usually unimportant and is assumed zero hereafter.

#### Example 15.16

The control line of a VCO senses a rectangular signal toggling between $V_{1}$ and $V_{2}$ at a period $T_{m}$. Plot the frequency, phase, and output waveform as a function of time.

#### Solution

Since $\omega_{\text {out }}=\omega_{0}+K_{V C O} V_{\text {cont }}$, the output frequency toggles between $\omega_{1}=\omega_{0}+K_{V C O} V_{1}$ and $\omega_{2}=\omega_{0}+K_{V C O} V_{2}$
(Fig. 15.63). The phase is equal to the time integral of this result, rising linearly with time at a slope of $\omega_{1}$ for half the input period and $\omega_{2}$ for the other half. The output waveform of the VCO is similar to that shown in Fig. 15.62. Thus, a VCO can operate as a frequency modulator.
image_name:Figure 15.63
description:The graph in Figure 15.63 consists of two parts: a frequency versus time plot, \( \omega(t) \), and a phase versus time plot, \( \phi(t) \).

1. **Type of Graph and Function:**
- The top graph is a time-domain waveform showing frequency changes over time.
- The bottom graph is a time-domain waveform illustrating phase changes over time.

2. **Axes Labels and Units:**
- For \( \omega(t) \): The x-axis represents time \( t \) (units not specified), and the y-axis represents frequency \( \omega \) (units not specified).
- For \( \phi(t) \): The x-axis represents time \( t \) (units not specified), and the y-axis represents phase \( \phi \) (units not specified).

3. **Overall Behavior and Trends:**
- **Frequency \( \omega(t) \):** The graph shows a square wave pattern alternating between two frequency levels, \( \omega_1 \) and \( \omega_2 \). The frequency stays at \( \omega_1 \) for half the period \( T_m \) and then switches to \( \omega_2 \) for the other half, repeating this cycle.
- **Phase \( \phi(t) \):** The phase increases linearly over time, with a slope corresponding to the frequency \( \omega(t) \). The slope is steeper during the \( \omega_2 \) intervals compared to the \( \omega_1 \) intervals, indicating a faster phase accumulation during the higher frequency period.

4. **Key Features and Technical Details:**
- The frequency \( \omega(t) \) toggles between two discrete levels, \( \omega_1 \) and \( \omega_2 \), with each level maintained for half of the modulation period \( T_m \).
- The phase \( \phi(t) \) shows a piecewise linear increase, with changes in slope occurring at the transitions between \( \omega_1 \) and \( \omega_2 \).
- The periodicity of the frequency switching is given by \( T_m \), which is the period of the modulation.

5. **Annotations and Specific Data Points:**
- The graph does not provide specific numerical values, but it clearly marks the transitions at \( T_m \) and the levels \( \omega_1 \) and \( \omega_2 \).
- Dashed vertical lines indicate the points in time where the frequency transitions occur, corresponding to changes in the slope of \( \phi(t) \).

image_name:Figure 15.63
description:The graph in Figure 15.63 is a time-domain waveform depicting the output voltage \( V_o(t) \) as a function of time \( t \). The horizontal axis represents time, while the vertical axis represents the voltage \( V_o(t) \). The units for time and voltage are not specified.

**Type of Graph and Function:**
This is a sinusoidal waveform graph that illustrates a frequency modulation pattern. The waveform shows a clear periodic oscillation with varying frequency over time.

**Axes Labels and Units:**
- **Horizontal Axis (x-axis):** Time \( t \) (units not specified)
- **Vertical Axis (y-axis):** Output Voltage \( V_o(t) \) (units not specified)

**Overall Behavior and Trends:**
The graph exhibits a sinusoidal waveform whose frequency increases over time. Initially, the waveform has a lower frequency, which gradually increases, resulting in more cycles being packed into the same time interval as time progresses. This pattern indicates frequency modulation, where the frequency of the waveform changes periodically.

**Key Features and Technical Details:**
- The waveform starts with a lower frequency, characterized by wider oscillations.
- As time progresses, the frequency increases, leading to narrower oscillations.
- This change in frequency is smooth and continuous, suggesting a linear or exponential increase in frequency over time.

**Annotations and Specific Data Points:**
- The graph does not provide specific numerical values for the frequencies or time intervals.
- No specific markers or reference lines are present, but the waveform's behavior clearly indicates a transition from a lower frequency to a higher frequency.
- The modulation period \( T_m \) and frequency levels \( \omega_1 \) and \( \omega_2 \) are referenced in the context but not explicitly marked on the graph.

Figure 15.63

As explained in Chapter 16, if a VCO is placed in a phase-locked loop, then only the second term of the total phase in Eq. (15.76) is of interest. This term, $K_{V C O} \int V_{c o n t} d t$, is called the "excess phase," $\phi_{e x}$. In fact, in the analysis of PLLs, we view the VCO as a system whose input and output are the control voltage and the excess phase, respectively:

$$
\begin{equation*}
\phi_{e x}=K_{V C O} \int V_{c o n t} d t \tag{15.77}
\end{equation*}
$$

That is, the VCO operates as an ideal integrator, providing a transfer function:

$$
\begin{equation*}
\frac{\Phi_{e x}}{V_{\text {cont }}}(s)=\frac{K_{V C O}}{s} \tag{15.78}
\end{equation*}
$$

#### Example 15.17

A VCO senses a small sinusoidal control voltage $V_{\text {cont }}=V_{m} \cos \omega_{m} t$. Determine the output waveform and its spectrum.

#### Solution

The output is expressed as

$$
\begin{align*}
V_{\text {out }}(t)= & V_{0} \cos \left(\omega_{0} t+K_{V C O} \int V_{\text {cont }} d t\right)  \tag{15.79}\\
= & V_{0} \cos \left(\omega_{0} t+K_{V C O} \frac{V_{m}}{\omega_{m}} \sin \omega_{m} t\right)  \tag{15.80}\\
= & V_{0} \cos \omega_{0} t \cos \left(K_{V C O} \frac{V_{m}}{\omega_{m}} \sin \omega_{m} t\right)  \tag{15.81}\\
& -V_{0} \sin \omega_{0} t \sin \left(K_{V C O} \frac{V_{m}}{\omega_{m}} \sin \omega_{m} t\right)
\end{align*}
$$

If $V_{m}$ is small enough that $K_{V C O} V_{m} / \omega_{m} \ll 1 \mathrm{rad}$, then

$$
\begin{align*}
V_{\text {out }}(t) & \approx V_{0} \cos \omega_{0} t-V_{0}\left(\sin \omega_{0} t\right)\left(K_{V C O} \frac{V_{m}}{\omega_{m}} \sin \omega_{m} t\right)  \tag{15.82}\\
& =V_{0} \cos \omega_{0} t-\frac{K_{V C O} V_{m} V_{0}}{2 \omega_{m}}\left[\cos \left(\omega_{0}-\omega_{m}\right) t-\cos \left(\omega_{0}+\omega_{m}\right) t\right] \tag{15.83}
\end{align*}
$$

The output therefore consists of three sinusoids having frequencies of $\omega_{0}, \omega_{0}-\omega_{m}$, and $\omega_{0}+\omega_{m}$. The spectrum is shown in Fig. 15.64. The components at $\omega_{0} \pm \omega_{m}$ are called "sidebands."
image_name:Figure 15.64
description:The graph depicted in Figure 15.64 is a frequency spectrum plot. The x-axis represents frequency, denoted by \( \omega \), and is not labeled with specific units, assuming radians per second as is typical in such contexts. The y-axis is not explicitly shown, but it typically represents amplitude or power in a spectrum plot.

In this spectrum, there are three distinct peaks at the frequencies \( \omega_0 - \omega_m \), \( \omega_0 \), and \( \omega_0 + \omega_m \). These peaks are represented by vertical arrows, indicating significant spectral components at these frequencies.

- **Peak at \( \omega_0 \):** This is the central frequency component, likely representing the main carrier frequency in the context of a voltage-controlled oscillator (VCO) output.
- **Sidebands at \( \omega_0 - \omega_m \) and \( \omega_0 + \omega_m \):** These are the sideband frequencies, resulting from modulation effects, indicating the presence of additional frequency components due to the modulation of the carrier signal by a control voltage.

The graph shows the typical result of a modulated signal where the original frequency \( \omega_0 \) is accompanied by sidebands at \( \omega_0 \pm \omega_m \). The presence of these sidebands is a key feature of amplitude modulation, where the modulation frequency \( \omega_m \) creates additional spectral components around the carrier frequency \( \omega_0 \). This behavior is typical in systems involving VCOs where control voltage variations can lead to these additional frequency components.

Figure 15.64

The above example reveals that variation of the control voltage with time may create unwanted components at the output. Indeed, when a VCO operates in the steady state, the control voltage must experience very little variation. ${ }^{16}$ This issue is studied in Chapter 16.

A common mistake in expressing the phase of signals arises from the familiar form $V_{m} \cos \omega_{0} t$. Here, the phase is equal to the product of frequency and time, creating the impression that such equality holds in all conditions. We may even deduce that, since the output frequency of a VCO is given by $\omega_{0}+K_{V C O} V_{\text {cont }}$, the output waveform can be written as $V_{m} \cos \left[\left(\omega_{0}+K_{V C O} V_{c o n t}\right) t\right]$. To understand why this is incorrect, let us compute the frequency as the derivative of the phase:

$$
\begin{align*}
\omega & =\frac{d}{d t}\left[\left(\omega_{0}+K_{V C O} V_{\text {cont }}\right) t\right]  \tag{15.84}\\
& =K_{V C O} \frac{d V_{\text {cont }}}{d t} t+\omega_{0}+K_{V C O} V_{\text {cont }} \tag{15.85}
\end{align*}
$$

The first term in this expression is redundant, vanishing only if $d V_{\text {cont }} / d t=0$. Thus, in the general case, the phase cannot be written as the product of time and frequency.

Our study of VCOs in this section has assumed sinusoidal output waveforms. In practice, depending on the type and speed of the oscillator, the output may contain significant harmonics, even approaching a rectangular waveform. How should Eq. (15.76) be modified in this case? We expect that $V_{\text {out }}(t)$ can be expressed as a Fourier series:

$$
\begin{equation*}
V_{\text {out }}(t)=V_{1} \cos \left(\omega_{0} t+\phi_{1}\right)+V_{2} \cos \left(2 \omega_{0} t+\phi_{2}\right)+\cdots \tag{15.86}
\end{equation*}
$$

We also note that if the (fundamental) frequency of a rectagular waveform is changed by $\Delta f$, the frequency of its second harmonic must change by $2 \Delta f$, etc. Thus, if $V_{\text {cont }}$ varies by $\Delta V$, then the frequency of the first harmonic varies by $K_{V C O} \Delta V$, the frequency of the second harmonic by $2 K_{V C O} \Delta V$, etc. That is
$V_{\text {out }}(t)=V_{1} \cos \left(\omega_{0} t+K_{V C O} \int V_{\text {cont }} d t+\theta_{1}\right)+V_{2} \cos \left(2 \omega_{0} t+2 K_{V C O} \int V_{\text {cont }} d t+\theta_{2}\right)+\cdots$

[^114]where $\theta_{1}, \theta_{2}, \cdots$ are constant phases necessary for the representation of each harmonic in the Fourier series expansion.

Equation (15.87) suggests that the harmonics of an oscillator output can be readily taken into account. For this reason, we often limit our calculations to the first harmonic, even though we may draw the waveforms in rectangular shape rather than sinusoidal shape.
