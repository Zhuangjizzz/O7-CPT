# Frequency Response

The need for operating circuits at increasingly higher speeds has always challenged designers. From radar and television systems in the 1940s to gigahertz microprocessors today, the demand to push circuits to higher frequencies has required a solid understanding of their speed limitations.

In this chapter, we study the effects that limit the speed of transistors and circuits, identifying topologies that better lend themselves to high-frequency operation. We also develop skills for deriving transfer functions of circuits, a critical task in the study of stability and frequency compensation (12). We assume bipolar transistors remain in the active mode and MOSFETs in the saturation region. The outline is shown below.

Fundamental Concepts

- Bode's Rules
- Association of Poles with Nodes
- Miller's Theorem

High-Frequency Models of Transistors

- Bipolar Model
- MOS Model
- Transit Frequency

Frequency Response of Circuits

- CE/CS Stages
- CB/CG Stages
- Followers
- Cascode Stage
- Differential Pair

## 11.1 FUNDAMENTAL CONCEPTS

### 11.1.1 General Considerations

What do we mean by "frequency response?" Illustrated in Fig. 11.1(a), the idea is to apply a sinusoid at the input of the circuit and observe the output while the input frequency is varied. As exemplified by Fig. 11.1(a), the circuit may exhibit a high gain at low frequencies but a "roll-off" as the frequency increases. We plot the magnitude of the gain as in Fig. 11.1(b) to represent the circuit's behavior at all frequencies of interest. We may loosely call $f_{1}$ the useful bandwidth of the circuit. Before investigating the cause of this roll-off,
image_name:(a)
description:The system block diagram in Fig. 11.1(a) illustrates the concept of frequency response testing in a circuit. The diagram has three main components:

1. **Input Sinusoidal Signal**: Three different sinusoidal waveforms are shown entering the circuit, representing varying frequencies. These are labeled as \( \text{In}(A_0) \), indicating the input amplitude.

2. **Amplifier Block**: Each input signal passes through an amplifier block labeled \( A_0 \). The amplifier's function is to increase the amplitude of the input signal. This block is crucial for analyzing how the circuit responds to different frequencies.

3. **Output Sinusoidal Signal**: The output of the amplifier is labeled \( \text{Out}(A_0) \), showing the amplified sinusoidal waveforms. As the frequency of the input signal increases, the amplitude of the output signal decreases, illustrating the roll-off effect.

The flow of information is straightforward: the input sinusoidal signal enters the amplifier, is amplified, and then exits as an output signal. This setup is used to observe how the circuit's gain changes with frequency.

Fig. 11.1(b) complements this by plotting the magnitude of the gain \( |A_v| \) against frequency \( f \). The plot shows a high gain at low frequencies, which decreases or "rolls off" as the frequency increases. The point \( f_1 \) is marked as the useful bandwidth, indicating the frequency range where the circuit maintains a relatively high gain before the roll-off becomes significant.

Overall, the system's primary function is to demonstrate the frequency response of a circuit, emphasizing how gain varies with input frequency and identifying the bandwidth over which the circuit operates effectively.
image_name:(b)
description:The graph in Figure 11.1(b) is a Bode plot representing the frequency response of a circuit. The x-axis is labeled 'f' and represents frequency, typically in hertz (Hz), while the y-axis is labeled '|A_v|' and represents the magnitude of voltage gain, usually in decibels (dB). The graph is plotted on a logarithmic scale for frequency, which is common in Bode plots to cover a wide range of frequencies effectively.

The overall behavior of the graph shows a high gain at low frequencies, which remains relatively constant until a certain frequency, labeled as 'f₁'. This point is marked by a vertical dashed line and is referred to as the cutoff frequency or the -3 dB point, indicating the useful bandwidth of the circuit. Beyond this point, the graph shows a downward trend, indicating a roll-off in gain as the frequency increases. This roll-off is typically due to the reactive components in the circuit, such as capacitors and inductors, which affect the gain at higher frequencies.

The key feature of this graph is the roll-off region, where the gain decreases, highlighting the circuit's limited ability to amplify signals at higher frequencies. This behavior is crucial for understanding the bandwidth limitations of the circuit and is a common characteristic in filters and amplifiers. The slope of the roll-off can provide additional information about the order of the filter or the dominant reactive elements in the circuit.

Annotations on the graph include the 'Roll-Off' label, which points to the region where the gain decreases, emphasizing the frequency-dependent nature of the circuit's gain. The cutoff frequency 'f₁' is a critical value for determining the circuit's bandwidth and is essential for designing circuits that need to operate effectively within a specific frequency range.

Figure 11.1 (a) Conceptual test of frequency response, (b) gain roll-off with frequency.
we must ask: why is frequency response important? The following examples illustrate the issue.

Example Explain why people's voices over the phone sound different from their voices in face11.1 to-face conversation.

Solution The human voice contains frequency components from 20 Hz to 20 kHz [Fig. 11.2(a)]. Thus, circuits processing the voice must accommodate this frequency range. Unfortunately, the phone system suffers from a limited bandwidth, exhibiting the frequency response shown in Fig. 11.2(b). Since the phone suppresses frequencies above 3.5 kHz , each person's voice is altered. In high-quality audio systems, on the other hand, the circuits are designed to cover the entire frequency range.
image_name:(a)
description:The graph labeled (a) is a frequency response graph, showing the range of frequencies present in the human voice. It is a filled area plot, illustrating a continuous range from 20 Hz to 20 kHz on the horizontal axis, which represents frequency (f) in hertz (Hz). The vertical axis is not explicitly labeled, but it typically represents amplitude or relative power.

1. **Type of Graph and Function:**
- The graph is a frequency response plot, commonly used to depict the range of frequencies that a system or signal can handle.

2. **Axes Labels and Units:**
- **Horizontal Axis (Frequency):** Ranges from 20 Hz to 20 kHz.
- **Vertical Axis:** Not labeled, but generally represents amplitude or power.

3. **Overall Behavior and Trends:**
- The plot shows a relatively flat response across the frequency range from 20 Hz to 20 kHz, indicating that the human voice contains components across this entire frequency spectrum.
- The flatness suggests an even distribution of energy across the frequencies shown.

4. **Key Features and Technical Details:**
- The graph illustrates the full frequency range of human voice components, from the low end at 20 Hz to the high end at 20 kHz.
- There are no significant peaks or valleys, indicating a broad and consistent frequency range.

5. **Annotations and Specific Data Points:**
- The graph is shaded to emphasize the entire frequency range covered by the human voice.

This graph is used to demonstrate the full range of frequencies that can be present in human speech, contrasting with the limited bandwidth typically available in phone systems, as shown in graph (b).
image_name:(b)
description:**Type of Graph and Function:**
The graph in Figure 11.2(b) is a frequency response graph, likely representing a Bode plot, which illustrates the bandwidth of a phone system.

**Axes Labels and Units:**
- The horizontal axis is labeled 'f' and represents frequency in hertz (Hz).
- The range on the frequency axis spans from 400 Hz to 3.5 kHz.
- The vertical axis is not explicitly labeled, but it typically represents amplitude or gain in decibels (dB).

**Overall Behavior and Trends:**
- The graph shows a bandpass characteristic, allowing frequencies between approximately 400 Hz and 3.5 kHz to pass through.
- The response begins to rise sharply from 400 Hz, indicating the lower cutoff frequency, and then levels off, maintaining a relatively constant amplitude.
- After reaching a peak, the response starts to decline sharply beyond 3.5 kHz, indicating the upper cutoff frequency.

**Key Features and Technical Details:**
- The graph exhibits a peak within the passband, suggesting a resonant frequency where the gain is maximized.
- The bandwidth of the phone system is limited to approximately 3.1 kHz (from 400 Hz to 3.5 kHz).
- There is a steep roll-off beyond the upper cutoff frequency, indicating significant attenuation of frequencies above 3.5 kHz.

**Annotations and Specific Data Points:**
- The lower cutoff frequency is marked at 400 Hz, and the upper cutoff frequency is marked at 3.5 kHz.
- The peak within the passband likely represents a frequency where the system's gain is at its maximum, although specific gain values are not provided in the graph.

Figure 11.2

Exercise Whose voice does the phone system alter more, men's or women's?

Example
11.2

Solution During recording, your voice propagates through the air and reaches the audio recorder. On the other hand, when you speak and listen to your own voice simultaneously, your voice propagates not only through the air but also from your mouth through your skull to your ear. Since the frequency response of the path through your skull is different
from that through the air (i.e., your skull passes some frequencies more easily than others), the way you hear your own voice is different from the way other people hear your voice.

Exercise Explain what happens to your voice when you have a cold.

Example Video signals typically occupy a bandwidth of about 5 MHz . For example, the graphics

11.3 card delivering the video signal to the display of a computer must provide at least 5 MHz of bandwidth. Explain what happens if the bandwidth of a video system is insufficient.

Solution With insufficient bandwidth, the "sharp" edges on a display become "soft," yielding a fuzzy picture. This is because the circuit driving the display is not fast enough to abruptly change the contrast from, e.g., complete white to complete black from one pixel to the next. Figures 11.3(a) and (b) illustrate this effect for a high-bandwidth and low-bandwidth driver, respectively. (The display is scanned from left to right.)
image_name:(a)
description:The image labeled as (a) shows a clear and sharp letter 'E'. The edges of the letter are well-defined, indicating that the image is likely representing the effect of a high-bandwidth driver on a display. The contrast between the black letter and the white background is distinct, demonstrating how sufficient bandwidth allows for precise transitions between different colors or shades on a screen. This clarity contrasts with what would be expected in a low-bandwidth scenario, where the edges would appear softer and more blurred.
image_name:(b)
description:The image labeled as (b) shows the letter 'E' with blurred edges, representing the effect of insufficient bandwidth in a video system. The edges of the letter are not sharp, indicating a lack of clarity and definition. This visual illustrates how low bandwidth results in a 'soft' or fuzzy appearance of sharp transitions, such as from black to white, due to the slower response time of the display driver. This effect is used to contrast with a high-bandwidth driver, which would display the letter with crisp, well-defined edges.

(a)
image_name:(a)
description:The image labeled "(a)" displays a large black letter 'E' with blurred edges, illustrating the effect of insufficient bandwidth in a video system. The edges of the letter are not sharp, indicating a lack of clarity and definition, which is characteristic of a low-bandwidth display driver. The blurred or 'soft' appearance of the transitions from black to white around the edges of the letter demonstrates how slower response times in the system result in less distinct image rendering. This visual serves as a contrast to what would be expected with a high-bandwidth driver, where the letter 'E' would be depicted with crisp, well-defined edges. There are no additional components, connections, or annotations visible in this image, as it primarily serves to illustrate the concept of bandwidth limitations visually.

(b)

Figure 11.3

Exercise What happens if the display is scanned from top to bottom?

What causes the gain roll-off in Fig. 11.1? As a simple example, let us consider the low-pass filter depicted in Fig. 11.4(a). At low frequencies, $C_{1}$ is nearly open and the current through $R_{1}$ nearly zero; thus, $V_{\text {out }}=V_{\text {in }}$. As the frequency increases, the impedance of $C_{1}$ falls and the voltage divider consisting of $R_{1}$ and $C_{1}$ attenuates $V_{i n}$ to a greater extent. The circuit therefore exhibits the behavior shown in Fig. 11.4(b).

As a more interesting example, consider the common-source stage illustrated in Fig. 11.5(a), where a load capacitance, $C_{L}$, appears at the output. At low frequencies, the signal current produced by $M_{1}$ prefers to flow through $R_{D}$ because the impedance of
image_name:Figure 11.4 (a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: Vout}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: GND}
]
extrainfo:This is a simple low-pass filter circuit. The frequency response shows that the output voltage decreases as the frequency increases, indicating attenuation of high-frequency signals.
image_name:Figure 11.4 (b)
description:The graph in Figure 11.4(b) is a frequency response plot, specifically a Bode plot, for a simple low-pass filter circuit. The x-axis represents frequency (f) and is typically plotted on a logarithmic scale, though the specific scale is not depicted in the image. The y-axis represents the magnitude of the voltage gain (|V_out/V_in|), and it is dimensionless, indicating the ratio of output voltage to input voltage.

**Overall Behavior and Trends:**
- The graph shows a flat response at low frequencies, where the gain remains constant at a value of 1.0. This indicates that the circuit allows low-frequency signals to pass through without attenuation.
- As the frequency increases, the gain begins to decrease, demonstrating the low-pass filter behavior. This decline in gain signifies that higher frequency components are attenuated.
- The transition from the flat region to the declining region marks the cutoff frequency, where the filter starts to significantly attenuate the input signal.

**Key Features and Technical Details:**
- The cutoff frequency, where the gain drops to approximately 0.707 (or -3 dB point), is not explicitly marked but is a critical point on the curve.
- The slope of the decline in the gain beyond the cutoff frequency is typically -20 dB/decade for a first-order low-pass filter, though exact values are not provided in the image.

**Annotations and Specific Data Points:**
- The plot does not display specific numerical values or annotations for the cutoff frequency or gain levels beyond the initial flat region. The absence of gridlines or markers makes it challenging to extract precise quantitative data from the graph.

Figure 11.4 (a) Simple low-pass filter, and (b) its frequency response.
image_name:Figure 11.5 (a)
description:
[
name: RD, type: Resistor, ports: {N1: VDD, N2: Vout}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: CL, type: Capacitor, ports: {Np: Vout, Nn: GND}
]
extrainfo:This circuit is a common-source (CS) amplifier stage with a load capacitance (CL). The NMOS transistor M1 amplifies the input signal Vin. The resistor RD is connected to VDD and the drain of M1, setting the DC bias point and providing load resistance. The capacitor CL is connected at the output Vout, which filters the high-frequency noise, stabilizing the output signal.

(a)
image_name:Figure 11.5 (b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: gmVin, type: VoltageControlledCurrentSource, ports: {Np: Vout, Nn: GND}
name: RD, type: Resistor, value: RD, ports: {N1: Vout, N2: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:This circuit is a small-signal model of a common-source amplifier stage with load capacitance. The voltage source Vin provides the input signal. The voltage-controlled current source gmVin represents the transconductance of the NMOS transistor. The resistor RD and capacitor CL are connected in parallel at the output node Vout, filtering high-frequency noise and stabilizing the output signal.

(b)

Figure 11.5 (a) CS stage with load capacitance, (b) small-signal model of the circuit.
$C_{L}, 1 /\left(C_{L} s\right)$, remains high. At high frequencies, on the other hand, $C_{L}$ "steals" some of the signal current and shunts it to ground, leading to a lower voltage swing at the output. In fact, from the small-signal equivalent circuit of Fig. 11.5(b), ${ }^{1}$ we note that $R_{D}$ and $C_{L}$ are in parallel and hence:

$$
\begin{equation*}
V_{\text {out }}=-g_{m} V_{\text {in }}\left(R_{D} \| \frac{1}{C_{L} S}\right) \tag{11.1}
\end{equation*}
$$

That is, as the frequency increases, the parallel impedance falls and so does the amplitude of $V_{\text {out }} .{ }^{2}$ The voltage gain therefore drops at high frequencies.

The reader may wonder why we use sinusoidal inputs in our study of frequency response. After all, an amplifier may sense a voice or video signal that bears no resemblance to sinusoids. Fortunately, such signals can be viewed as a summation of many sinusoids with different frequencies (and phases). Thus, responses such as that in Fig. 11.5(b) prove useful so long as the circuit remains linear and hence superposition can be applied.

### 11.1.2 Relationship Between Transfer Function and Frequency Response

We know from basic circuit theory that the transfer function of a circuit can be written as

$$
\begin{equation*}
H(s)=A_{0} \frac{\left(1+\frac{s}{\omega_{z 1}}\right)\left(1+\frac{s}{\omega_{z 2}}\right) \ldots}{\left(1+\frac{s}{\omega_{p 1}}\right)\left(1+\frac{s}{\omega_{p 2}}\right) \ldots} \tag{11.2}
\end{equation*}
$$

where $A_{0}$ denotes the low-frequency gain because $H(s) \rightarrow A_{0}$ as $s \rightarrow 0$. The frequencies $\omega_{z j}$ and $\omega_{p j}$ represent the zeros and poles of the transfer function, respectively. If the input to the circuit is a sinusoid of the form $x(t)=A \cos (2 \pi f t)=A \cos \omega t$, then the output can be expressed as

$$
\begin{equation*}
y(t)=A|H(j \omega)| \cos [\omega t+\angle H(j \omega)] \tag{11.3}
\end{equation*}
$$

[^5]where $H(j \omega)$ is obtained by making the substitution $s=j \omega$. Called the "magnitude" and the "phase," $|H(j \omega)|$ and $\angle H(j \omega)$ respectively reveal the frequency response of the circuit. In this chapter, we are primarily concerned with the former. Note that $f$ (in Hz) and $\omega$ (in radians per second) are related by a factor of $2 \pi$. For example, we may write $\omega=5 \times 10^{10} \mathrm{rad} / \mathrm{s}=2 \pi(7.96 \mathrm{GHz})$.

Example Determine the transfer function and frequency response of the CS stage shown in Fig. 11.4 11.5(a).

Solution From Eq. (11.1), we have

$$
\begin{align*}
H(s)=\frac{V_{\text {out }}}{V_{\text {in }}}(s) & =-g_{m}\left(R_{D} \| \frac{1}{C_{L} s}\right)  \tag{11.4}\\
& =\frac{-g_{m} R_{D}}{R_{D} C_{L} s+1} . \tag{11.5}
\end{align*}
$$

For a sinusoidal input, we replace $s=j \omega$ and compute the magnitude of the transfer function: ${ }^{3}$

$$
\begin{equation*}
\left|\frac{V_{\text {out }}}{V_{\text {in }}}\right|=\frac{g_{m} R_{D}}{\sqrt{R_{D}^{2} C_{L}^{2} \omega^{2}+1}} \tag{11.6}
\end{equation*}
$$

As expected, the gain begins at $g_{m} R_{D}$ at low frequencies, rolling off as $R_{D}^{2} C_{L}^{2} \omega^{2}$ becomes comparable with unity. At $\omega=1 /\left(R_{D} C_{L}\right)$,

$$
\begin{equation*}
\left|\frac{V_{\text {out }}}{V_{\text {in }}}\right|=\frac{g_{m} R_{D}}{\sqrt{2}} . \tag{11.7}
\end{equation*}
$$

Since $20 \log \sqrt{2} \approx 3 \mathrm{~dB}$, we say the -3 dB bandwidth of the circuit is equal to $1 /\left(R_{D} C_{L}\right)$ (Fig. 11.6).
image_name:Figure 11.6
description:The graph in Figure 11.6 is a Bode plot, illustrating the frequency response of a circuit. The horizontal axis represents angular frequency (ω) and is typically in radians per second, while the vertical axis represents the magnitude of the voltage gain, \(|V_{out}/V_{in}|\), in decibels (dB).

Axes Labels and Units:
- **Horizontal Axis (ω):** Angular frequency in radians per second (rad/s).
- **Vertical Axis (|V_out/V_in|):** Voltage gain magnitude, usually in decibels (dB).

Overall Behavior and Trends:
- At low frequencies, the gain starts at a constant level, represented as \(g_m R_D\).
- As frequency increases, the gain remains constant until it reaches the cutoff frequency.
- Beyond this point, the gain begins to roll off.

Key Features and Technical Details:
- **-3 dB Point:** The graph shows a significant point where the gain drops to \(\frac{g_m R_D}{\sqrt{2}}\), which corresponds to a -3 dB reduction in gain. This occurs at the frequency \(\omega = \frac{1}{R_D C_L}\).
- **Bandwidth:** The bandwidth of the circuit is defined as the range of frequencies over which the gain is within 3 dB of its maximum value. This is marked by the horizontal arrow labeled "-3 dB Bandwidth."
- **Rolloff:** After the -3 dB point, the gain decreases at a rate that is determined by the circuit's characteristics, indicated by the curve labeled "-3 dB Rolloff."

Annotations and Specific Data Points:
- The graph includes annotations such as "-3 dB Bandwidth" and "-3 dB Rolloff," highlighting the critical points and regions of interest.
- A vertical dashed line marks the cutoff frequency \(\omega = \frac{1}{R_D C_L}\), which is a key value for determining the bandwidth.

This Bode plot effectively demonstrates the frequency response of the circuit, showing how the gain behaves across different frequencies and highlighting the critical -3 dB bandwidth and rolloff regions.

Figure 11.6
Exercise Derive the above results if $\lambda \neq 0$.
${ }^{3}$ The magnitude of the complex number $a+j b$ is equal to $\sqrt{a^{2}+b^{2}}$.

Example Consider the common-emitter stage shown in Fig.11.7. Derive a relationship among the 11.5 gain, the -3 dB bandwidth, and the power consumption of the circuit. Assume $V_{A}=\infty$.
image_name:Figure 11.7
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: Vin, E: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Vout}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a common-emitter amplifier stage with an NPN transistor (Q1). The input is connected to the base of Q1, and the output is taken from the collector. The resistor RC is connected between the collector and VCC, and the capacitor CL is connected from the output to ground. The emitter is grounded. The circuit is designed to amplify the input signal Vin.

Figure 11.7
Solution In a manner similar to the CS topology of Fig. 11.5(a), the bandwidth is given by $1 /\left(R_{C} C_{L}\right)$, the low-frequency gain by $g_{m} R_{C}=\left(I_{C} / V_{T}\right) R_{C}$, and the power consumption by $I_{C} \cdot V_{C C}$. For the highest performance, we wish to maximize both the gain and the bandwidth (and hence the product of the two) and minimize the power dissipation. We therefore define a "figure of merit" as

$$
\begin{align*}
\frac{\text { Gain } \times \text { Bandwidth }}{\text { Power Consumption }} & =\frac{\frac{I_{C}}{V_{T}} R_{C} \times \frac{1}{R_{C} C_{L}}}{I_{C} \cdot V_{C C}}  \tag{11.8}\\
& =\frac{1}{V_{T} \cdot V_{C C}} \frac{1}{C_{L}} . \tag{11.9}
\end{align*}
$$

Thus, the overall performance can be improved by lowering (a) the temperature; ${ }^{4}$ (b) $V_{C C}$ but at the cost of limiting the voltage swings; or (c) the load capacitance. In practice, the load capacitance receives the greatest attention. Equation (11.9) becomes more complex for CS stages (Problem 11.15).

Exercise Derive the above results if $V_{A}<\infty$.

Example Explain the relationship between the frequency response and step response of the simple 11.6 low-pass filter shown in Fig. 11.4(a).

Solution To obtain the transfer function, we view the circuit as a voltage divider and write

$$
\begin{align*}
H(s)=\frac{V_{\text {out }}}{V_{\text {in }}}(s) & =\frac{\frac{1}{C_{1} s}}{\frac{1}{C_{1} s}+R_{1}}  \tag{11.10}\\
& =\frac{1}{R_{1} C_{1} s+1} . \tag{11.11}
\end{align*}
$$

[^6]The frequency response is determined by replacing $s$ with $j \omega$ and computing the magnitude:

$$
\begin{equation*}
|H(s=j \omega)|=\frac{1}{\sqrt{R_{1}^{2} C_{1}^{2} \omega^{2}+1}} \tag{11.12}
\end{equation*}
$$

The -3 dB bandwidth is equal to $1 /\left(R_{1} C_{1}\right)$.
The circuit's response to a step of the form $V_{0} u(t)$ is given by

$$
\begin{equation*}
V_{\text {out }}(t)=V_{0}\left(1-\exp \frac{-t}{R_{1} C_{1}}\right) u(t) \tag{11.13}
\end{equation*}
$$

The relationship between Eqs. (11.12) and (11.13) is that, as $R_{1} C_{1}$ increases, the bandwidth drops and the step response becomes slower. Figure 11.8 plots this behavior, revealing that a narrow bandwidth results in a sluggish time response. This observation explains the effect seen in Fig. 11.3(b): since the signal cannot rapidly jump from low (white) to high (black), it spends some time at intermediate levels (shades of gray), creating "fuzzy" edges.
image_name:Figure 11.8
description:The graph in Figure 11.8 is a Bode plot illustrating the magnitude response \(|H|\) of a system as a function of frequency \(f\). The vertical axis represents the magnitude \(|H|\), which is dimensionless, while the horizontal axis represents frequency \(f\), typically in hertz (Hz). The graph uses a logarithmic scale for frequency.

The plot shows the behavior of the system's frequency response as the product \(R_1 C_1\) increases. Initially, the magnitude \(|H|\) is constant at a value of 1.0, indicating that the system passes low frequencies with no attenuation. As frequency increases, the magnitude begins to decrease, showing a roll-off characteristic of a low-pass filter.

The graph includes three lines representing different values of \(R_1 C_1\). As \(R_1 C_1\) increases, the cutoff frequency decreases, resulting in a narrower bandwidth. The solid black line represents the response with the highest \(R_1 C_1\), showing the steepest decline and the narrowest bandwidth. The dashed black line and the gray line represent lower values of \(R_1 C_1\), with the gray line having the widest bandwidth and the least steep decline.

Key features include the initial flat response at low frequencies and the subsequent decline at higher frequencies, illustrating the trade-off between bandwidth and the time response of the system. The graph highlights how increasing \(R_1 C_1\) affects the system's ability to respond quickly to changes in input, as seen by the slower roll-off and reduced bandwidth.

(a)
image_name:(a)
description:The graph depicted is a time-domain waveform representing the output voltage \( V_{out} \) over time \( t \). This graph illustrates the effect of different values of the product \( R_1 C_1 \) on the system's response. The horizontal axis is labeled \( t \), representing time, while the vertical axis is labeled \( V_{out} \), representing the output voltage.

Three curves are shown on the graph:

1. **Solid Black Line**: Represents a higher value of \( R_1 C_1 \). It shows a slower response with a more gradual rise to the final value, indicating a longer time constant.
2. **Dashed Black Line**: Represents a moderate value of \( R_1 C_1 \). The response is quicker than the solid black line but slower than the gray line.
3. **Gray Line**: Represents a lower value of \( R_1 C_1 \). This line has the fastest rise time and reaches the steady state more quickly, illustrating the widest bandwidth and the least steep decline.

Overall, the graph demonstrates the trade-off between bandwidth and time response in the system. As \( R_1 C_1 \) increases, the system's ability to respond quickly to changes in input decreases, resulting in a slower roll-off and reduced bandwidth. The initial flat response at low frequencies transitions into a steeper decline at higher frequencies, highlighting this trade-off.

(b)

Figure 11.8
Exercise At what frequency does $|H|$ fall by a factor of two?

### 11.1.3 Bode's Rules

The task of obtaining $|H(j \omega)|$ from $H(s)$ and plotting the result is somewhat tedious. For this reason, we often utilize Bode's rules (approximations) to construct $|H(j \omega)|$ rapidly. Bode's rules for $|H(j \omega)|$ are as follows:

- As $\omega$ passes each pole frequency, the slope of $|H(j \omega)|$ decreases by $20 \mathrm{~dB} /$ dec. (A slope of $20 \mathrm{~dB} /$ dec simply means a tenfold change in $H$ for a tenfold increase in frequency);
- As $\omega$ passes each zero frequency, the slope of $|H(j \omega)|$ increases by $20 \mathrm{~dB} / \mathrm{dec} .^{5}$

Example

11.7

Construct the Bode plot of $|H(j \omega)|$ for the CS stage depicted in Fig. 11.5(a).

Solution Equation (11.5) indicates a pole frequency of

$$
\begin{equation*}
\left|\omega_{p 1}\right|=\frac{1}{R_{D} C_{L}} \tag{11.14}
\end{equation*}
$$

[^7]The magnitude thus begins at $g_{m} R_{D}$ at low frequencies and remains flat up to $\omega=\left|\omega_{p 1}\right|$. At this point, the slope changes from zero to $-20 \mathrm{~dB} / \mathrm{dec}$. Figure 11.9 illustrates the result. In contrast to Fig. 11.5(b), the Bode approximation ignores the 3 dB roll-off at the pole frequency-but it greatly simplifies the algebra. As evident from Eq. (11.6), for $R_{D}^{2} C_{L}^{2} \omega^{2} \gg 1$, Bode's rule provides a good approximation.
image_name:Figure 11.9
description:The graph in Figure 11.9 is a Bode plot representing the magnitude response of a system. It is a logarithmic plot with the x-axis labeled as 'log(ω)', representing the logarithm of frequency (ω), and the y-axis labeled as '20 log |V_out/V_in|', representing the magnitude of the output-to-input voltage ratio in decibels (dB).

Overall Behavior and Trends:
- **Flat Region:** The plot begins with a flat region where the magnitude is constant at \( g_m R_D \) for low frequencies.
- **Break Point:** At the frequency \( \omega_{p1} \), the plot shows a distinct break point where the behavior changes.
- **Slope Change:** Beyond \( \omega_{p1} \), the slope of the plot changes to \(-20 \text{ dB/decade}\), indicating a decrease in magnitude with increasing frequency.

Key Features and Technical Details:
- **Initial Magnitude:** The initial flat section of the plot indicates that the gain is constant and equal to \( g_m R_D \).
- **Pole Frequency:** The frequency \( \omega_{p1} \) is marked on the plot as the point where the slope changes.
- **Slope:** After the pole frequency, the plot drops at a rate of \(-20 \text{ dB/decade}\), which is typical for a single-pole system.

Annotations and Specific Data Points:
- The plot clearly indicates the transition at \( \omega_{p1} \) with a dashed vertical line marking this frequency.
- The slope of \(-20 \text{ dB/decade}\) is annotated on the plot to highlight the rate of decrease in magnitude.

This Bode plot provides a simplified view of the system's frequency response, ignoring minor details such as the 3 dB roll-off at the pole frequency, which is typical in Bode approximations.

Figure 11.9
Exercise Construct the Bode plot for $g_{m}=(150 \Omega)^{-1}, R_{D}=2 \mathrm{k} \Omega$, and $C_{L}=100 \mathrm{fF}$.

### 11.1.4 Association of Poles with Nodes

The poles of a circuit's transfer function play a central role in the frequency response. The designer must therefore be able to identify the poles intuitively so as to determine which parts of the circuit appear as the "speed bottleneck."

The CS topology studied in Example 11.4 serves as a good example for identifying poles by inspection. Equation (11.5) reveals that the pole frequency is given by the inverse of the product of the total resistance seen between the output node and ground and the total capacitance seen between the output node and ground. Applicable to many circuits, this observation can be generalized as follows: if node $j$ in the signal path exhibits a small-signal resistance of $R_{j}$ to ground and a capacitance of $C_{j}$ to ground, then it contributes a pole of magnitude $\left(R_{j} C_{j}\right)^{-1}$ to the transfer function.

Did you know?

Bode's rules are an example of "necessity is mother of invention." While working on electronic filters and equalizers at Bell Labs in the 1930s, Hendrik Bode, like other researchers in the field, faced the problem of determining the stability of complex circuits and systems. With no computers or even calculators available, the engineers of that era had to perform lengthy hand calculations for this purpose. Bode thus came up with his approximations of the frequency response and, as seen in Chapter 12, a simple method of studying the stability of feedback systems.

Determine the poles of the circuit shown in Fig. 11.10. Assume $\lambda=0$.
image_name:Figure 11.10
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: g1}
name: Cin, type: Capacitor, value: Cin, ports: {Np: g1, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: g1}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
]
extrainfo:The circuit is a common-source amplifier with an NMOS transistor M1. It has an input pole determined by RS and Cin, and an output pole determined by RD and CL.

Figure 11.10

Solution Setting $V_{i n}$ to zero, we recognize that the gate of $M_{1}$ sees a resistance of $R_{S}$ and a capacitance of $C_{i n}$ to ground. Thus,

$$
\begin{equation*}
\left|\omega_{p 1}\right|=\frac{1}{R_{S} C_{i n}} . \tag{11.15}
\end{equation*}
$$

We may call $\omega_{p 1}$ the "input pole" to indicate that it arises in the input network. Similarly, the "output pole" is given by

$$
\begin{equation*}
\left|\omega_{p 2}\right|=\frac{1}{R_{D} C_{L}} \tag{11.16}
\end{equation*}
$$

Since the low-frequency gain of the circuit is equal to $-g_{m} R_{D}$, we can readily write the magnitude of the transfer function as:

$$
\begin{equation*}
\left|\frac{V_{\text {out }}}{V_{\text {in }}}\right|=\frac{g_{m} R_{D}}{\sqrt{\left(1+\omega^{2} / \omega_{p 1}^{2}\right)\left(1+\omega^{2} \omega_{p 2}^{2}\right)}} . \tag{11.17}
\end{equation*}
$$

Exercise If $\omega_{p 1}=\omega_{p 2}$, at what frequency does the gain drop by 3 dB ?

Example Compute the poles of the circuit shown in Fig. 11.11. Assume $\lambda=0$

11.9
image_name:Figure 11.11
description:
[
name: M1, type: NMOS, ports: {S: S1, D: Vout, G: Vb}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: S1}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
name: Cin, type: Capacitor, value: Cin, ports: {Np: S1, Nn: GND}
]
extrainfo:The circuit is a common-source amplifier with NMOS transistor M1. RD is the load resistor, RS is the source resistor, and CL is the load capacitor. Cin is the input coupling capacitor. The gate of M1 is biased with Vb.

Figure 11.11
Solution With $V_{i n}=0$, the small-signal resistance seen at the source of $M_{1}$ is given by $R_{S} \|\left(1 / g_{m}\right)$, yielding a pole at

$$
\begin{equation*}
\omega_{p 1}=\frac{1}{\left(R_{S} \| \frac{1}{g_{m}}\right) C_{i n}} \tag{11.18}
\end{equation*}
$$

The output pole is given by $\omega_{p 2}=\left(R_{D} C_{L}\right)^{-1}$.

Exercise
How do we choose the value of $R_{D}$ such that the output pole frequency is ten times the input pole frequency?

The reader may wonder how the foregoing technique can be applied if a node is loaded with a "floating" capacitor, i.e., a capacitor whose other terminal is also connected to a node in the signal path (Fig. 11.12). In general, we cannot utilize this technique and must
image_name:Figure 11.12 Circuit with floating capacitor
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: g1}
name: CF, type: Capacitor, ports: {Np: g1, Nn: Vout}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: g1}
]
extrainfo:The circuit contains a floating capacitor CF connected between the input node g1 and the output node Vout. Miller's theorem can be applied to simplify the analysis by transforming CF into two grounded capacitors.

Figure 11.12 Circuit with floating capacitor.
write the circuit's equations and obtain the transfer function. However, an approximation given by "Miller's theorem" can simplify the task in some cases.

### 11.1.5 Miller's Theorem

Our above study and the example in Fig. 11.12 make it desirable to obtain a method that "transforms" a floating capacitor to two grounded capacitors, thereby allowing association of one pole with each node. Miller's theorem is such a method. Miller's theorem, however, was originally conceived for another reason. In the late 1910s, John Miller had observed that parasitic capacitances appearing between the input and output of an amplifier may drastically lower the input impedance. He then proposed an analysis that led to the theorem.

Consider the general circuit shown in Fig. 11.13(a), where the floating impedance, $Z_{F}$, appears between nodes 1 and 2 . We wish to transform $Z_{F}$ to two grounded impedances as depicted in Fig. 11.13(b), while ensuring all of the currents and voltages in the circuit remain unchanged. To determine $Z_{1}$ and $Z_{2}$, we make two observations: (1) the current drawn by $Z_{F}$ from node 1 in Fig. 11.13(a) must be equal to that drawn by $Z_{1}$ in Fig. 11.13(b); and (2) the current injected to node 2 in Fig. 11.13(a) must be equal to that injected by $Z_{2}$ in Fig. 11.13(b). (These requirements guarantee that the circuit does not "feel" the transformation.) Thus,

$$
\begin{align*}
& \frac{V_{1}-V_{2}}{Z_{F}}=\frac{V_{1}}{Z_{1}}  \tag{11.19}\\
& \frac{V_{1}-V_{2}}{Z_{F}}=-\frac{V_{2}}{Z_{2}} \tag{11.20}
\end{align*}
$$

Denoting the voltage gain from node 1 to node 2 by $A_{v}$, we obtain

$$
\begin{align*}
Z_{1} & =Z_{F} \frac{V_{1}}{V_{1}-V_{2}}  \tag{11.21}\\
& =\frac{Z_{F}}{1-A_{v}} \tag{11.22}
\end{align*}
$$

image_name:(a)
description:
[
name: ZF, type: Resistor, value: ZF, ports: {N1: 1, N2: 2}
]
extrainfo:The circuit in diagram (a) includes a floating impedance ZF between nodes 1 and 2, with voltage sources V1 and V2 connected to ground at nodes 1 and 2 respectively.
image_name:(b)
description:
[
name: Z1, type: Resistor, value: Z1, ports: {N1: 1, N2: GND}
name: Z2, type: Resistor, value: Z2, ports: {N1: 2, N2: GND}
]
extrainfo:The circuit diagram (b) represents the equivalent circuit using Miller's theorem, where the floating impedance ZF is replaced by two grounded impedances Z1 and Z2. V1 and V2 are voltage sources connected to nodes 1 and 2 respectively, with both having a common ground.

Figure 11.13 (a) General circuit including a floating impedance, (b) equivalent of (a) as obtained from Miller's theorem.
and

$$
\begin{align*}
Z_{2} & =Z_{F} \frac{-V_{2}}{V_{1}-V_{2}}  \tag{11.23}\\
& =\frac{Z_{F}}{1-\frac{1}{A_{v}}} \tag{11.24}
\end{align*}
$$

Called Miller's theorem, the results expressed by Eqs. (11.22) and (11.24) prove extremely useful in analysis and design. In particular, Eq. (11.22) suggests that the floating impedance is reduced by a factor of $1-A_{v}$ when "seen" at node 1 .

As an important example of Miller's theorem, let us assume $Z_{F}$ is a single capacitor, $C_{F}$, tied between the input and output of an inverting amplifier [Fig. 11.14(a)]. Applying Eq. (11.22), we have

$$
\begin{align*}
Z_{1} & =\frac{Z_{F}}{1-A_{v}}  \tag{11.25}\\
& =\frac{1}{\left(1+A_{0}\right) C_{F} S} \tag{11.26}
\end{align*}
$$

where the substitution $A_{v}=-A_{0}$ is made. What type of impedance is $Z_{1}$ ? The $1 / s$ dependence suggests a capacitor of value $\left(1+A_{0}\right) C_{F}$, as if $C_{F}$ is "amplified" by a factor of $1+A_{0}$. In other words, a capacitor $C_{F}$ tied between the input and output of an inverting amplifier with a gain of $A_{0}$ raises the input capacitance by an amount equal to $\left(1+A_{0}\right) C_{F}$. We say such a circuit suffers from "Miller multiplication" of the capacitor.

The effect of $C_{F}$ at the output can be obtained from Eq. (11.24):

$$
\begin{align*}
Z_{2} & =\frac{Z_{F}}{1-\frac{1}{A_{v}}}  \tag{11.27}\\
& =\frac{1}{\left(1+\frac{1}{A_{0}}\right) C_{F} S} \tag{11.28}
\end{align*}
$$

which is close to $\left(C_{F} s\right)^{-1}$ if $A_{0} \gg 1$. Figure 11.14(b) summarizes these results.
The Miller multiplication of capacitors can also be explained intuitively. Suppose the input voltage in Fig. 11.14(a) goes up by a small amount $\Delta V$. The output then goes down by $A_{0} \Delta V$. That is, the voltage across $C_{F}$ increases by $\left(1+A_{0}\right) \Delta V$, requiring that the input provide a proportional charge. By contrast, if $C_{F}$ were not a floating capacitor and its right plate voltage did not change, it would experience only a voltage change of $\Delta V$ and require less charge.
image_name:(a)
description:
[
name: CF, type: Capacitor, value: CF, ports: {Np: Vout, Nn: Vin}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: Vin, OutP: Vout, OutN: GND}
]
extrainfo:The circuit is an inverting amplifier with a floating capacitor CF connected between the output and input of the op-amp A0. The input voltage is Vin and the output voltage is Vout. The circuit demonstrates the Miller effect.
image_name:(b)
description:
[
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: Vin, Out: Vout}
name: CF(1+1/A0), type: Capacitor, value: CF(1+1/A0), ports: {Np: Vout, Nn: GND}
name: CF(1+A0), type: Capacitor, value: CF(1+A0), ports: {Np: Vin, Nn: GND}
]
extrainfo:The circuit diagram (b) is an equivalent circuit using Miller's theorem, converting a floating capacitor to a grounded capacitor. It shows an inverting amplifier configuration with an operational amplifier and a grounded capacitor CF(1+1/A0). The input voltage is Vin, and the output is Vout.

Figure 11.14 (a) Inverting circuit with floating capacitor, (b) equivalent circuit as obtained from Miller's theorem.

The above study points to the utility of Miller's theorem for conversion of floating capacitors to grounded capacitors. The following example demonstrates this principle.

Did you know?

The Miller effect was discovered by John Miller in 1919. In his original paper, Miller observes that "the apparent input capacity can become a number of times greater than the actual capacities between the tube electrodes." (Back then, capacitance and capacitor were called "capacity" and "condensor," respectively.) A curious effect with respect to Miller multiplication is that, if the amplifier gain is positive and greater than unity, then we obtain a negative input capacitance, $\left(1-A_{v}\right) C_{F}$. Does this happen? Yes, indeed. Shown below is a circuit realizing a negative capacitance. Since the gain from $V_{i n 1}$ to $V_{Y}$ (and from $V_{i n 2}$ to $V_{X}$ ) is positive, $C_{F}$ can be multiplied by a negative number. This technique is used in many high-speed circuits to partially cancel the effect of undesired (positive) capacitances.
image_name:Circuit with negative input capacitance
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin1}
name: M2, type: NMOS, ports: {S: P, D: Y, G: Vin2}
name: RD1, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: RD2, type: Resistor, value: RD, ports: {N1: VDD, N2: Y}
name: CF1, type: Capacitor, value: CF, ports: {Np: Vin1, Nn: X}
name: CF2, type: Capacitor, value: CF, ports: {Np: Vin2, Nn: Y}
name: I1, type: CurrentSource, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit uses NMOS transistors M1 and M2 to create a negative input capacitance effect. The resistors RD and capacitors CF are used to achieve the desired gain and capacitance cancellation. The current source provides biasing.

Circuit with negative input capacitance.

Example $\quad$ Estimate the pole of the circuit shown in Fig. 11.15(a). Assume $\lambda=0$.
image_name:(a)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: g1}
name: CF, type: Capacitor, value: CF, ports: {Np: g1, Nn: Vout}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: g1}
]
extrainfo:The circuit uses NMOS transistor M1 and resistor RD to form an inverting amplifier with a gain of -gmRD. Capacitor CF is used for capacitance cancellation. The circuit exhibits a negative input capacitance effect.

(a)
image_name:Figure 11.15(b)
description:
[
name: Rs, type: Resistor, value: Rs, ports: {N1: Vin, N2: g1}
name: Cin, type: Capacitor, value: Cin, ports: {Np: g1, Nn: GND}
name: Cout, type: Capacitor, value: Cout, ports: {Np: Vout, Nn: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: g1}
]
extrainfo:The circuit is an inverting amplifier using an NMOS transistor with a gain of -gmRD. Capacitors Cin and Cout are used for input and output coupling, respectively. RD is connected to VDD, and the output is taken from the drain of M1.

(b)

Figure 11.15

Solution Noting that $M_{1}$ and $R_{D}$ constitute an inverting amplifier having a gain of $-g_{m} R_{D}$, we utilize the results in Fig. 11.14(b) to write:

$$
\begin{align*}
C_{i n} & =\left(1+A_{0}\right) C_{F}  \tag{11.29}\\
& =\left(1+g_{m} R_{D}\right) C_{F} \tag{11.30}
\end{align*}
$$

and

$$
\begin{equation*}
C_{\text {out }}=\left(1+\frac{1}{g_{m} R_{D}}\right) C_{F}, \tag{11.31}
\end{equation*}
$$

thereby arriving at the topology depicted in Fig. 11.15(b). From our study in Example 11.8, we have:

$$
\begin{align*}
\omega_{\text {in }} & =\frac{1}{R_{S} C_{i n}}  \tag{11.32}\\
& =\frac{1}{R_{S}\left(1+g_{m} R_{D}\right) C_{F}} \tag{11.33}
\end{align*}
$$

and

$$
\begin{align*}
\omega_{\text {out }} & =\frac{1}{R_{D} C_{\text {out }}}  \tag{11.34}\\
& =\frac{1}{R_{D}\left(1+\frac{1}{g_{m} R_{D}}\right) C_{F}} . \tag{11.35}
\end{align*}
$$

Why does the circuit in (a) have one pole but that in (b) two? This is explained below.
Exercise Calculate $C_{i n}$ if $g_{m}=(150 \Omega)^{-1}, R_{D}=2 \mathrm{k} \Omega$, and $C_{F}=80 \mathrm{fF}$.

The reader may find the above example somewhat inconsistent. Miller's theorem requires that the floating impedance and the voltage gain be computed at the same frequency whereas Example 11.10 uses the low-frequency gain, $g_{m} R_{D}$, even for the purpose of finding high-frequency poles. After all, we know that the existence of $C_{F}$ lowers the voltage gain from the gate of $M_{1}$ to the output at high frequencies. Owing to this inconsistency, we call the procedure in Example 11.10 the "Miller approximation." Without this approximation, i.e., if $A_{0}$ is expressed in terms of circuit parameters at the frequency of interest, application of Miller's theorem would be no simpler than direct solution of the circuit's equations. Due to the approximation, the circuit in the above example exhibits two poles.

Another artifact of Miller's approximation is that it may eliminate a zero of the transfer function. We return to this issue in Section 11.4.3.

The general expression in Eq. (11.22) can be interpreted as follows: an impedance tied between the input and output of an inverting amplifier with a gain of $A_{v}$ is lowered by a factor of $1+A_{v}$ if seen at the input (with respect to ground). This reduction of impedance (hence increase in capacitance) is called "Miller effect." For example, we say Miller effect raises the input capacitance of the circuit in Fig. 11.15(a) to $\left(1+g_{m} R_{D}\right) C_{F}$.

### 11.1.6 General Frequency Response

Our foregoing study indicates that capacitances in a circuit tend to lower the voltage gain at high frequencies. It is possible that capacitors reduce the gain at low frequencies as well. As a simple example, consider the high-pass filter shown in Fig. 11.16(a), where the voltage
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: Vout}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a simple high-pass filter. The frequency response shows that the gain increases with frequency, reaching a maximum at high frequencies. The cutoff frequency is determined by the time constant R1*C1.
image_name:(b)
description:The graph in Fig. 11.16(b) is a Bode plot representing the frequency response of a simple high-pass filter.

1. **Type of Graph and Function:**
- The graph is a magnitude Bode plot, showing the gain of the high-pass filter as a function of frequency.

2. **Axes Labels and Units:**
- The horizontal axis represents angular frequency (\(\omega\)), typically measured in radians per second.
- The vertical axis represents the magnitude of the voltage gain \(\left|\frac{V_{\text{out}}}{V_{\text{in}}}\right|\), which is unitless.
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The plot shows an increasing trend in gain with frequency.
- At low frequencies, the gain is near zero, indicating that the filter attenuates low-frequency signals.
- As frequency increases, the gain approaches a maximum value of 1, indicating that high-frequency signals are passed with little attenuation.

4. **Key Features and Technical Details:**
- The cutoff frequency, where the gain is \(\frac{1}{\sqrt{2}}\) of the maximum (approximately 0.707), is marked by the vertical dashed line at \(\frac{1}{R_1 C_1}\).
- Beyond the cutoff frequency, the gain asymptotically approaches 1, showing that the filter effectively allows high-frequency signals to pass.

5. **Annotations and Specific Data Points:**
- The graph includes a horizontal dashed line at the gain level of 1, indicating the maximum gain.
- The significant point at \(\frac{1}{R_1 C_1}\) is annotated, marking the transition from low to high gain.

Figure 11.16 (a) Simple high-pass filter, and (b) its frequency response.
division between $C_{1}$ and $R_{1}$ yields

$$
\begin{align*}
\frac{V_{\text {out }}}{V_{\text {in }}}(s) & =\frac{R_{1}}{R_{1}+\frac{1}{C_{1} s}}  \tag{11.36}\\
& =\frac{R_{1} C_{1} s}{R_{1} C_{1} s+1} \tag{11.37}
\end{align*}
$$

and hence

$$
\begin{equation*}
\left|\frac{V_{\text {out }}}{V_{\text {in }}}\right|=\frac{R_{1} C_{1} \omega}{\sqrt{R_{1}^{2} C_{1}^{2} \omega_{1}^{2}+1}} \tag{11.38}
\end{equation*}
$$

Plotted in Fig. 11.16(b), the response exhibits a roll-off as the frequency of operation falls below $1 /\left(R_{1} C_{1}\right)$. As seen from Eq. (11.37), this roll-off arises because the zero of the transfer function occurs at the origin.

The low-frequency roll-off may prove undesirable. The following example illustrates this point.

Example
11.11

Figure 11.17 depicts a source follower used in a high-quality audio amplifier. Here, $R_{i}$ establishes a gate bias voltage equal to $V_{D D}$ for $M_{1}$, and $I_{1}$ defines the drain bias current. Assume $\lambda=0, g_{m}=1 /(200 \Omega)$, and $R_{1}=100 \mathrm{k} \Omega$. Determine the minimum required value of $C_{1}$ and the maximum tolerable value of $C_{L}$.
image_name:Figure 11.17
description:
[
name: Ri, type: Resistor, value: Ri, ports: {N1: g1, N2: VDD}
name: Ci, type: Capacitor, value: Ci, ports: {Np: Vin, Nn: g1}
name: M1, type: NMOS, ports: {S: Vout, D: VDD, G: g1}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vout, Nn: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a source follower configuration used in a high-quality audio amplifier. It includes an NMOS transistor (M1) with gate bias set by Ri and a drain bias current defined by I1. The input is Vin, and the output is Vout. The low-frequency roll-off is managed by Ci, and the load capacitance is CL.

Figure 11.17
Solution Similar to the high-pass filter of Fig. 11.16, the input network consisting of $R_{i}$ and $C_{i}$ attenuates the signal at low frequencies. To ensure that audio components as low as 20 Hz experience a small attenuation, we set the corner frequency $1 /\left(R_{i} C_{i}\right)$ to $2 \pi \times(20 \mathrm{~Hz})$, thus obtaining

$$
\begin{equation*}
C_{i}=79.6 \mathrm{nF} \tag{11.39}
\end{equation*}
$$

This value is, of course, much too large to be integrated on a chip. Since Eq. (11.38) reveals a 3 dB attenuation at $\omega=1 /\left(R_{i} C_{i}\right)$, in practice we must choose even a larger capacitor if a lower attenuation is desired.

The load capacitance creates a pole at the output node, lowering the gain at high frequencies. Setting the pole frequency to the upper end of the audio range, 20 kHz , and recognizing that the resistance seen from the output node to ground is equal to $1 / g_{m}$, we have

$$
\begin{align*}
\omega_{p, \text { out }} & =\frac{g_{m}}{C_{L}}  \tag{11.40}\\
& =2 \pi \times(20 \mathrm{kHz}) \tag{11.41}
\end{align*}
$$

and hence

$$
\begin{equation*}
C_{L}=39.8 \mathrm{nF} \tag{11.42}
\end{equation*}
$$

An efficient driver, the source follower can tolerate a very large load capacitance (for the audio band).

Exercise $\quad$ Repeat the above example if $I_{1}$ and the width of $M_{1}$ are halved.

Why did we use capacitor $C_{i}$ in the above example? Without $C_{i}$, the circuit's gain would not fall at low frequencies, and we would not need perform the above calculations. Called a "coupling" capacitor, $C_{i}$ allows the signal frequencies of interest to pass through the circuit while blocking the dc content of $V_{i n}$. In other words, $C_{i}$ isolates the bias conditions of the source follower from those of the preceding stage. Figure 11.18(a) illustrates an example in which a CS stage precedes the source follower. The coupling capacitor permits independent bias voltages at nodes $X$ and $Y$. For example, $V_{Y}$ can be chosen relatively low (placing $M_{2}$ near the triode region) to allow a large drop across $R_{D}$, thereby maximizing the voltage gain of the CS stage (why?).
image_name:Figure 11.18(a)
description:
[
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Y}
name: Ri, type: Resistor, value: Ri, ports: {N1: VDD, N2: X}
name: Ci, type: Capacitor, value: Ci, ports: {Np: Y, Nn: X}
name: M1, type: NMOS, ports: {S: Vout, D: VDD, G: X}
name: M2, type: NMOS, ports: {S: GND, D: Y, G: Vin}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a cascade of a common-source (CS) stage and a source follower. The coupling capacitor Ci allows independent biasing of the CS stage and the source follower. RD and Ri are used to set the bias conditions. M1 acts as a source follower, and M2 as a common-source amplifier. I1 is a current source providing biasing current to the source follower stage.

(a)
image_name:(b)
description:
[
name: RD, type: Resistor, ports: {N1: VDD, N2: P}
name: M2, type: NMOS, ports: {S: GND, D: P, G: Vin}
name: M1, type: NMOS, ports: {S: Vout, D: VDD, G: P}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a cascade of a common-source (CS) stage and a source follower. The coupling capacitor Ci allows independent biasing of the CS stage and the source follower. RD and Ri are used to set the bias conditions. M1 acts as a source follower, and M2 as a common-source amplifier. I1 is a current source providing biasing current to the source follower stage.

(b)

Figure 11.18 Cascade of CS stage and source follower with (a) capacitor coupling and (b) direct coupling.

To convince the reader that capacitive coupling proves essential in Fig. 11.18(a), we consider the case of "direct coupling" [Fig. 11.18(b)] as well. Here, to maximize the voltage gain, we wish to set $V_{P}$ just above $V_{G S 2}-V_{T H 2}$, e.g., 200 mV . On the other hand, the gate of $M_{2}$ must reside at a voltage of at least $V_{G S 1}+V_{I 1}$, where $V_{I 1}$ denotes the minimum voltage required by $I_{1}$. Since $V_{G S 1}+V_{I 1}$ may reach $600-700 \mathrm{mV}$, the two stages are quite incompatible in terms of their bias points, necessitating capacitive coupling.

Capacitive coupling (also called "ac coupling") is more common in discrete circuit design due to the large capacitor values required in many applications (e.g., $C_{i}$ in the above audio example). Nonetheless, many integrated circuits also employ capacitive coupling, especially at low supply voltages, if the necessary capacitor values are no more than a few picofarads.

Figure 11.19 shows a typical frequency response and the terminology used to refer to its various attributes. We call $\omega_{L}$ the lower corner or lower "cut-off" frequency and $\omega_{H}$ the upper corner or upper cut-off frequency. Chosen to accommodate the signal frequencies of interest, the band between $\omega_{L}$ and $\omega_{H}$ is called the "midband range" and the corresponding gain the "midband gain."
image_name:Figure 11.19 Typical frequency response.
description:The graph in Figure 11.19 is a typical frequency response plot, often used to illustrate the behavior of electronic filters or amplifiers. It is a Bode plot showing the magnitude of the transfer function, |H|, as a function of angular frequency, ω.

1. **Type of Graph and Function:**
- This is a Bode magnitude plot, which is a logarithmic graph used to represent the frequency response of a system.

2. **Axes Labels and Units:**
- The vertical axis is labeled |H|, representing the magnitude of the transfer function, typically in decibels (dB), although the specific unit is not shown.
- The horizontal axis is labeled ω, which represents the angular frequency in radians per second.
- The frequency axis is usually logarithmic, although this is not explicitly shown in the diagram.

3. **Overall Behavior and Trends:**
- The graph shows a low-frequency rise to a flat midband region, followed by a high-frequency roll-off.
- The curve begins at a lower corner frequency, ω_L, where the gain starts to increase.
- It reaches a flat region called the "midband range," where the gain is constant and labeled as "Midband Gain."
- After the midband, the gain decreases at a higher corner frequency, ω_H.

4. **Key Features and Technical Details:**
- The lower cutoff frequency is denoted by ω_L, marking the point where the gain begins to rise toward the midband.
- The upper cutoff frequency is denoted by ω_H, marking the point where the gain starts to decline from the midband.
- The constant gain level in the midband is labeled as "Midband Gain."
- The bandwidth of the system is the range between ω_L and ω_H.

5. **Annotations and Specific Data Points:**
- The graph includes dashed lines at ω_L and ω_H to indicate the cutoff frequencies.
- An arrow labeled "Midband" indicates the range over which the gain remains constant.

This graph is typical of a bandpass filter or amplifier, where the system allows frequencies within a certain range to pass through with minimal attenuation while attenuating frequencies outside this range.

Figure 11.19 Typical frequency response.

## 11.2 HIGH-FREQUENCY MODELS OF TRANSISTORS

The speed of many circuits is limited by the capacitances within each transistor. It is therefore necessary to study these capacitances carefully.

### 11.2.1 High-Frequency Model of Bipolar Transistor

Recall from Chapter 4 that the bipolar transistor consists of two pn junctions. The depletion region associated with the junctions ${ }^{6}$ gives rise to a capacitance between base and emitter, denoted by $C_{j e}$, and another between base and collector, denoted by $C_{\mu}$ [Fig. 11.20(a)]. We may then add these capacitances to the small-signal model to arrive at the representation shown in Fig. 11.20(b).
image_name:(a)
description:The image consists of three parts labeled (a), (b), and (c), each representing different models of a bipolar transistor.

1. **Part (a) - Structure of Bipolar Transistor:**
- **Components and Structure:** The diagram shows a cross-sectional view of a bipolar transistor with two pn junctions. It includes an n-type region, a p-type region, and another n+ region, representing the base (B), collector (C), and emitter (E) terminals, respectively.
- **Connections and Interactions:** Capacitances are depicted between the base and collector (C_μ) and between the base and emitter (C_je). These capacitances arise from the depletion regions at the junctions.
- **Labels and Annotations:** The terminals are labeled as B (Base), C (Collector), and E (Emitter), with the capacitances marked as C_μ and C_je.

2. **Part (b) - Small-Signal Model with Junction Capacitances:**
- **Components and Structure:** This is a small-signal equivalent circuit model of the bipolar transistor. It includes resistors, capacitors, and a dependent current source.
- **Connections and Interactions:** The diagram shows C_μ and C_je capacitances connected between the terminals. The base-emitter junction is represented by a resistor r_π and a voltage source v_π. A dependent current source, g_m * v_π, represents the transistor's transconductance, and r_o represents the output resistance.
- **Labels and Annotations:** The components are labeled with their respective symbols and parameters, such as C_μ, C_je, r_π, v_π, g_m, and r_o.

3. **Part (c) - Complete Model Accounting for Base Charge:**
- **Components and Structure:** This model is an extension of the small-signal model, incorporating additional elements to account for the base charge.
- **Connections and Interactions:** Similar to part (b), it includes C_μ and C_π capacitances, a resistor r_π, and a dependent current source g_m * v_π. The model also includes a voltage-controlled current source to account for the base charge dynamics.
- **Labels and Annotations:** The labels include C_μ, C_π, r_π, v_π, g_m, and r_o, along with the base, collector, and emitter terminals.
image_name:(b)
description:
[
name: C_μ, type: Capacitor, value: C_μ, ports: {Np: B, Nn: C}
name: C_je, type: Capacitor, value: C_je, ports: {Np: B, Nn: E}
name: r_π, type: Resistor, value: r_π, ports: {N1: B, N2: E}
name: g_m v_π, type: CurrentSource, value: g_m v_π, ports: {Np: C, Nn: E}
name: r_o, type: Resistor, value: r_o, ports: {N1: C, N2: E}
]
extrainfo:The circuit represents a high-frequency small-signal model of a bipolar transistor, including junction capacitances C_μ and C_je, as well as a dependent current source g_m v_π representing the transconductance effect.
image_name:(c)
description:
[
name: C_μ, type: Capacitor, value: C_μ, ports: {Np: B, Nn: C}
name: C_π, type: Capacitor, value: C_π, ports: {Np: B, Nn: E}
name: r_π, type: Resistor, value: r_π, ports: {N1: B, N2: E}
name: g_m v_π, type: CurrentSource, value: g_m v_π, ports: {Np: C, Nn: E}
name: r_o, type: Resistor, value: r_o, ports: {N1: C, N2: E}
]
extrainfo:This is a high-frequency small-signal model of a bipolar transistor, incorporating junction capacitances C_μ and C_π, as well as resistances and controlled sources to model transistor behavior.

Figure 11.20 (a) Structure of bipolar transistor showing junction capacitances, (b) small-signal model with junction capacitances, (c) complete model accounting for base charge.

Unfortunately, this model is incomplete because the base-emitter junction exhibits another effect that must be taken into account. As explained in Chapter 4, the operation of the transistor requires a (nonuniform) charge profile in the base region to allow the

[^8]diffusion of carriers toward the collector. In other words, if the transistor is suddenly turned on, proper operation does not begin until enough charge carriers enter the base region and accumulate so as to create the necessary profile. Similarly, if the transistor is suddenly turned off, the charge carriers stored in the base must be removed for the collector current to drop to zero.

The above phenomenon is quite similar to charging and discharging a capacitor: to change the collector current, we must change the base charge profile by injecting or removing some electrons or holes. Modeled by a second capacitor between the base and emitter, $C_{b}$, this effect is typically more significant than the depletion region capacitance. Since $C_{b}$ and $C_{j e}$ appear in parallel, they are lumped into one and denoted by $C_{\pi}$ [Fig. 11.20(c)].

In integrated circuits, the bipolar transistor is fabricated atop a grounded substrate [Fig. 11.21(a)]. The collector-substrate junction remains reverse-biased (why?), exhibiting a junction capacitance denoted by $C_{C S}$. The complete model is depicted in Fig. 11.21(b). We hereafter employ this model in our analysis. In modern integrated-circuit bipolar transistors, $C_{j e}, C_{\mu}$, and $C_{C S}$ are on the order of a few femtofarads for the smallest allowable devices.
image_name:(a)
description:The image labeled as Figure 11.21(a) shows the cross-sectional structure of an integrated bipolar transistor. The diagram illustrates a transistor fabricated on a grounded substrate. Key components and features include:

1. **Components and Structure:**
- **Collector (C):** Positioned at the top left of the diagram, connected to the n-type region.
- **Base (B):** Located centrally, connected to the p-type region.
- **Emitter (E):** Situated at the top right, connected to the n+ region within the p-type base.
- **Substrate:** The n-type substrate forms the bottom layer of the structure, providing a grounded base for the device.

2. **Connections and Interactions:**
- The collector is connected to the n-type region, which is part of the main body of the transistor.
- The base is connected to the p-type region, which separates the collector and emitter regions.
- The emitter is connected to the n+ region, which is a heavily doped section within the base.
- A junction capacitance, denoted as **C_CS**, exists between the collector and the substrate, indicating a reverse-biased collector-substrate junction.

3. **Labels, Annotations, and Key Features:**
- The diagram is labeled with C, B, and E to denote the collector, base, and emitter, respectively.
- The substrate is labeled at the bottom, indicating its role as the grounding layer.
- The capacitance C_CS is explicitly shown between the collector and substrate, highlighting its significance in the model.

This diagram provides a visual representation of the physical structure of a bipolar transistor within an integrated circuit, emphasizing the layout and connections of its components.
image_name:(b)
description:
[
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: B, Nn: E}
name: Cμ, type: Capacitor, value: Cμ, ports: {Np: B, Nn: C}
name: CCS, type: Capacitor, value: CCS, ports: {Np: C, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: B, N2: E}
name: ro, type: Resistor, value: ro, ports: {N1: C, N2: E}
name: gmvπ, type: VoltageControlledCurrentSource, ports: {Np: C, Nn: E}
]
extrainfo:The circuit represents a small-signal model of an NPN transistor including the collector-substrate capacitance. The capacitances Cπ, Cμ, and CCS are connected between the base-emitter, base-collector, and collector-ground respectively. The voltage-controlled current source gmvπ is controlled by the voltage across rπ.
image_name:(c)
description:
[
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: B, Nn: E}
name: Cμ, type: Capacitor, value: Cμ, ports: {Np: B, Nn: C}
name: CCS, type: Capacitor, value: CCS, ports: {Np: C, Nn: GND}
name: Q1, type: NPN, ports: {C: C, B: B, E: E}
]
extrainfo:The circuit diagram represents the small-signal model of an integrated bipolar transistor, including parasitic capacitances Cπ, Cμ, and CCS. The model is used to analyze frequency response, and it shows the connection of the transistor with its associated capacitances and resistances.

Figure 11.21 (a) Structure of an integrated bipolar transistor, (b) small-signal model including collector-substrate capacitance, (c) device symbol with capacitances shown explicitly.

In the analysis of frequency response, it is often helpful to first draw the transistor capacitances on the circuit diagram, simplify the result, and then construct the small-signal equivalent circuit. We may therefore represent the transistor as shown in Fig. 11.21(c).

Identify all of the capacitances in the circuit shown in Fig. 11.22(a).
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: c1e2, B: Vin, E: GND}
name: Q2, type: NPN, ports: {C: Vout, B: Vb1, E: c1e2}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Vout}
]
extrainfo:The circuit diagram represents a cascode amplifier configuration with two NPN transistors (Q1 and Q2). The circuit includes various parasitic capacitances such as Cμ1, Cμ2, Cπ1, Cπ2, CCS1, and CCS2. The resistive load is represented by RC. The output node is labeled as Vout, and the input is at Vin. The circuit is powered by VCC.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: Vin, E: GND}
name: Q2, type: NPN, ports: {C: Vout, B: Vb, E: Vout}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Vout}
name: Cπ1, type: Capacitor, value: Cπ1, ports: {Np: Vin, Nn: GND}
name: Cμ1, type: Capacitor, value: Cμ1, ports: {Np: Vout, Nn: Vin}
name: CCS1, type: Capacitor, value: CCS1, ports: {Np: Vout, Nn: GND}
name: Cπ2, type: Capacitor, value: Cπ2, ports: {Np: Vb, Nn: Vin}
name: Cμ2, type: Capacitor, value: Cμ2, ports: {Np: Vout, Nn: Vb}
name: CCS2, type: Capacitor, value: CCS2, ports: {Np: Vout, Nn: GND}
name: CIE2, type: Capacitor, value: CIE2, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit diagram represents a cascode amplifier with two NPN transistors, Q1 and Q2, and various capacitors indicating high-frequency behavior. The configuration includes common capacitive elements such as Cπ, Cμ, and CCS, which are crucial for modeling the transistor's frequency response. The resistive load is connected to VCC, and the output is taken at Vout. This setup is typical for improving bandwidth and stability in amplifier circuits.

Figure 11.22

Solution From Fig. 11.21(b), we add the three capacitances of each transistor as depicted in Fig. 11.22(b). Interestingly, $C_{C S 1}$ and $C_{\pi 2}$ appear in parallel, and so do $C_{\mu 2}$ and $C_{C S 2}$.

Exercise Construct the small-signal equivalent circuit of the above cascode.

### 11.2.2 High-Frequency Model of MOSFET

Our study of the MOSFET structure in Chapter 6 revealed several capacitive components. We now study these capacitances in the device in greater detail.

Illustrated in Fig. 11.23(a), the MOSFET displays three prominent capacitances: one between the gate and the channel (called the "gate oxide capacitance" and given by $W L C_{o x}$ ), and two associated with the reverse-biased source-bulk and drain-bulk junctions. The first component presents a modeling difficulty because the transistor model does not contain a "channel." We must therefore decompose this capacitance into one between the gate and the source and another between the gate and the drain [Fig. 11.23(b)]. The exact partitioning of this capacitance is beyond the scope of this book, but, in the saturation region, $C_{1}$ is about $2 / 3$ of the gate-channel capacitance whereas $C_{2} \approx 0$.
image_name:(a)
description:The image labeled as Figure 11.23(a) depicts the cross-sectional structure of a MOS (Metal-Oxide-Semiconductor) device, highlighting various capacitances associated with it. The main components visible in the diagram include:

1. **p-substrate**: This is the base layer of the semiconductor device, indicated at the bottom of the diagram. It is labeled as 'p-substrate' and serves as the foundational layer upon which the MOS structure is built.

2. **n+ Regions**: Two heavily doped n-type regions are shown, labeled as 'n+'. These regions represent the source and drain of the MOSFET. They are embedded within the p-substrate and are crucial for the operation of the MOS device.

3. **Gate Structure**: Above the n+ regions and the p-substrate, there is a horizontal structure representing the gate. This includes a thin insulating layer (likely silicon dioxide) and a conductive gate terminal on top.

4. **Capacitances**: The diagram indicates capacitance elements associated with the MOS structure. These are shown as small capacitor symbols connected to the n+ regions and the gate. These represent the capacitances between the gate and the source/drain regions, which are critical in modeling the behavior of the MOSFET.

The image provides a simplified view of the MOSFET, focusing on the interaction between the gate and the source/drain regions through capacitances. This is essential for understanding the electrical characteristics and behavior of the device in circuits.

(a)
image_name:Figure 11.23 (b)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Gate, Nn: Drain}
name: C2, type: Capacitor, value: C2, ports: {Np: Gate, Nn: Source}
]
extrainfo:This diagram represents the partitioning of gate-channel capacitance between source and drain in a MOSFET. C1 and C2 are the capacitances between the gate and the drain/source regions.

(b)

Figure 11.23 (a) Structure of MOS device showing various capacitances, (b) partitioning of gate-channel capacitance between source and drain.

Two other capacitances in the MOSFET become critical in some circuits. Shown in Fig. 11.24, these components arise from both the physical overlap of the gate with source/drain areas ${ }^{7}$ and the fringe field lines between the edge of the gate and the top of the S/D regions. Called the gate-drain or gate-source "overlap" capacitance, this (symmetric) effect persists even if the MOSFET is off.
image_name:Figure 11.24
description:The diagram illustrates the overlap capacitance between the gate and drain of a MOSFET. This is a critical component in high-frequency models of MOSFETs, arising from the physical overlap and fringe field lines between the gate and drain regions.

Figure 11.24 Overlap capacitance between gate and drain (or source).
We now construct the high-frequency model of the MOSFET. Depicted in Fig. 11.25(a), this representation consists of: (1) the capacitance between the gate and source, $C_{G S}$ (including the overlap component); (2) the capacitance between the gate and drain (including the overlap component); (3) the junction capacitances between the source and bulk and the drain and bulk, $C_{S B}$ and $C_{D B}$, respectively. (We assume the bulk remains at ac ground.)

[^9]image_name:(a)
description:
[
name: C_GS, type: Capacitor, value: C_GS, ports: {Np: G, Nn: S}
name: C_GD, type: Capacitor, value: C_GD, ports: {Np: G, Nn: D}
name: C_DB, type: Capacitor, value: C_DB, ports: {Np: D, Nn: GND}
name: C_SB, type: Capacitor, value: C_SB, ports: {Np: S, Nn: GND}
name: g_m V_GS, type: VoltageControlledCurrentSource, ports: {Np: D, Nn: S}
name: r_O, type: Resistor, value: r_O, ports: {N1: D, N2: S}
]
extrainfo:This diagram represents the high-frequency model of a MOSFET with various capacitances and a voltage-controlled current source. The bulk is assumed to remain at AC ground.

(a)
image_name:Figure 11.25(b)
description:
[
name: C_GS, type: Capacitor, value: C_GS, ports: {Np: G, Nn: S}
name: C_GD, type: Capacitor, value: C_GD, ports: {Np: G, Nn: D}
name: C_DB, type: Capacitor, value: C_DB, ports: {Np: D, Nn: GND}
name: C_SB, type: Capacitor, value: C_SB, ports: {Np: S, Nn: GND}
name: NMOS, type: NMOS, ports: {S: S, D: D, G: G}
]
extrainfo:This diagram represents the high-frequency model of a MOSFET with various capacitances, including gate-source (C_GS), gate-drain (C_GD), drain-bulk (C_DB), and source-bulk (C_SB) capacitances. The bulk is assumed to remain at AC ground.

(b)

Figure 11.25 (a) High-frequency model of MOSFET, (b) device symbol with capacitances shown explicitly.

As mentioned in Section 11.2.1, we often draw the capacitances on the transistor symbol [Fig. 11.25(b)] before constructing the small-signal model.

Example Identify all of the capacitances in the circuit of Fig. 11.26(a).
11.13
image_name:Figure 11.26(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: M2, type: PMOS, ports: {S: VDD, D: Vout, G: Vout}
]
extrainfo:The circuit consists of an NMOS transistor M1 and a PMOS transistor M2, forming a common-source amplifier with a diode-connected load. Various parasitic capacitances are included, reflecting a high-frequency small-signal model. M2 is diode-connected, and several capacitances are combined at the output node.
image_name:Figure 11.26(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: M2, type: PMOS, ports: {S: VDD, D: Vout, G: Vout}
name: CGS2, type: Capacitor, value: CGS2, ports: {Np: Vout, Nn: VDD}
name: CSB2, type: Capacitor, value: CSB2, ports: {Np: S2, Nn: VDD}
name: CDB2, type: Capacitor, value: CDB2, ports: {Np: Vout, Nn: VDD}
name: CGD2, type: Capacitor, value: CGD2, ports: {Np: Vout, Nn: Vout}
name: CGD1, type: Capacitor, value: CGD1, ports: {Np: Vin, Nn: Vout}
name: CGS1, type: Capacitor, value: CGS1, ports: {Np: Vin, Nn: GND}
name: CSB1, type: Capacitor, value: CSB1, ports: {Np: GND, Nn: GND}
name: CDB1, type: Capacitor, value: CDB1, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a high-frequency model of a MOSFET amplifier with M2 as a diode-connected PMOS. The capacitors represent various parasitic capacitances in the circuit. The output is at Vout, and the input is at Vin. The circuit reduces parasitic effects by connecting certain capacitances to ground.
image_name:Figure 11.26(c)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: M2, type: PMOS, ports: {S: VDD, D: Vout, G: Vout}
name: CGS1, type: Capacitor, value: CGS1, ports: {Np: Vin, Nn: GND}
name: CGD1, type: Capacitor, value: CGD1, ports: {Np: Vin, Nn: Vout}
name: CSB1, type: Capacitor, value: CSB1, ports: {Np: GND, Nn: GND}
name: CSB2, type: Capacitor, value: CSB2, ports: {Np: VDD, Nn: VDD}
name: CDB1, type: Capacitor, value: CDB1, ports: {Np: Vout, Nn: GND}
name: CDB2, type: Capacitor, value: CDB2, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a high-frequency model of a MOSFET amplifier with M2 being diode-connected. The capacitors CDB1, CDB2, and CGS2 appear in parallel at the output node Vout. CSB1 and CSB2 are shorted to AC ground. CGD2 is shorted out.

Figure 11.26

Solution Adding the four capacitances of each device from Fig. 11.25, we arrive at the circuit in Fig. 11.26(b). Note that $C_{S B 1}$ and $C_{S B 2}$ are shorted to ac ground on both ends, $C_{G D 2}$ is shorted "out," and $C_{D B 1}, C_{D B 2}$, and $C_{G S 2}$ appear in parallel at the output node. The circuit therefore reduces to that in Fig. 11.26(c).

Exercise
Noting that $M_{2}$ is a diode-connected device, construct the small-signal equivalent circuit of the amplifier.

### 11.2.3 Transit Frequency

With various capacitances surrounding bipolar and MOS devices, is it possible to define a quantity that represents the ultimate speed of the transistor? Such a quantity would prove useful in comparing different types or generations of transistors as well as in predicting the performance of circuits incorporating the devices.
image_name:Q_1
description:
[
name: I_in, type: CurrentSource, value: I_in, ports: {Np: GND, Nn: Vin}
name: Q_1, type: NPN, ports: {C: I_out, B: Vin, E: GND}
]
extrainfo:The circuit diagram shows two configurations: one with an NPN transistor Q1 and the other with an NMOS transistor M1. Both configurations are used to measure the transit frequency f_T by injecting a sinusoidal current I_in and measuring the output current I_out.
image_name:M_1
description:
[
name: I_in, type: CurrentSource, value: I_in, ports: {Np: GND, Nn: Vin}
name: M1, type: NMOS, ports: {S: GND, D: GND, G: Vin}
]
extrainfo:The circuit consists of a current source, a capacitor, and two NMOS transistors. The NMOS transistors are configured with source to ground and gate to Vin, sharing the same drain node I_out.

Figure 11.27 Conceptual setup for measurement of $f_{T}$ of transistors.
A measure of the intrinsic speed of transistors ${ }^{8}$ is the "transit" or "cut-off" frequency, $f_{T}$, defined as the frequency at which the small-signal current gain of the device falls to unity. Illustrated in Fig. 11.27 (without the biasing circuitry), the idea is to inject a sinusoidal current into the base or gate and measure the resulting collector or drain current while the input frequency, $f_{i n}$, is increased. We note that, as $f_{i n}$ increases, the input capacitance of the device lowers the input impedance, $Z_{i n}$, and hence the input voltage $V_{i n}=I_{i n} Z_{i n}$ and the output current. We neglect $C_{\mu}$ and $C_{G D}$ here (but take them into account in Problem 11.26). For the bipolar device in Fig. 11.27(a),

$$
\begin{equation*}
Z_{i n}=\frac{1}{C_{\pi} s} \| r_{\pi} \tag{11.43}
\end{equation*}
$$

Since $I_{\text {out }}=g_{m} I_{\text {in }} Z_{\text {in }}$,

$$
\begin{align*}
\frac{I_{\text {out }}}{I_{\text {in }}} & =\frac{g_{m} r_{\pi}}{r_{\pi} C_{\pi} s+1}  \tag{11.44}\\
& =\frac{\beta}{r_{\pi} C_{\pi} s+1} . \tag{11.45}
\end{align*}
$$

At the transit frequency, $\omega_{T}\left(=2 \pi f_{T}\right)$, the magnitude of the current gain falls to unity:

$$
\begin{align*}
r_{\pi}^{2} C_{\pi}^{2} \omega_{T}^{2} & =\beta^{2}-1  \tag{11.46}\\
& \approx \beta^{2} . \tag{11.47}
\end{align*}
$$

That is,

$$
\begin{equation*}
\omega_{T} \approx \frac{g_{m}}{C_{\pi}} \tag{11.48}
\end{equation*}
$$

The transit frequency of MOSFETs is obtained in a similar fashion. We therefore write:

$$
\begin{equation*}
2 \pi f_{T} \approx \frac{g_{m}}{C_{\pi}} \quad \text { or } \quad \frac{g_{m}}{C_{G S}} . \tag{11.49}
\end{equation*}
$$

Note that the collector-substrate or drain-bulk capacitance does not affect $f_{T}$ owing to the ac ground established at the output.

Modern bipolar and MOS transistors boast $f_{T}$ 's above 100 GHz . Of course, the speed of complex circuits using such devices is quite lower.

The minimum channel length of MOSFETs has been scaled from $1 \mu \mathrm{~m}$ in the late 1980s 11.14 to 65 nm today. Also, the inevitable reduction of the supply voltage has reduced the gate-source overdive voltage from about 400 mV to 100 mV . By what factor has the $f_{T}$ of MOSFETs increased?
${ }^{8}$ By "intrinsic" speed, we mean the performance of the device by itself, without any other limitations imposed or enhancements provided by the circuit.

Solution It can proved (Problem 11.28) that

$$
\begin{equation*}
2 \pi f_{T}=\frac{3}{2} \frac{\mu_{n}}{L^{2}}\left(V_{G S}-V_{T H}\right) \tag{11.50}
\end{equation*}
$$

Thus, the transit frequency has increased by approximately a factor of 59. For example, if $\mu_{n}=400 \mathrm{~cm}^{2} /(\mathrm{V} \cdot \mathrm{s})$, then 65 nm devices having an overdrive of 100 mV exhibit an $f_{T}$ of 226 GHz .

Exercise
Determine the $f_{T}$ if the channel length is scaled down to 45 nm but the mobility degrades to $300 \mathrm{~cm}^{2} /(\mathrm{V} \cdot \mathrm{s})$.

Did you know?

If the $f_{T}$ of 65 nm MOSFETs is around 220 GHz , is it possible to operate such a device at a higher frequency? Yes, indeed. The key is to use inductors to cancel the effect of capacitors. Suppose as shown in Fig. (a), we place inductor $L_{1}$ in parallel with $C_{G S}$. (Realized as a metal spiral on the chip, the inductor has some resistance, $R_{S \text {.) }}$ At the resonance frequency, $\omega_{0}=1 / \sqrt{L_{1} C_{G S}}$, the parallel combination reduces to a single resistor, almost as if $M_{1}$ had no gate-source capacitance! For this reason, the use of on-chip inductors has become common in high-frequency design. Figure (b) shows the chip photograph of a 300 GHz oscillator designed by the author in 65 nm technology. Such high frequencies find application in medical imaging.
image_name:(a)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: X1, N2: b1}
name: L1, type: Inductor, value: L1, ports: {N1: X1, N2: GND}
name: CGS, type: Capacitor, ports: {Np: b1, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: LOAD, G: b1}
]
extrainfo:The circuit uses resonance to cancel transistor capacitance, with an inductor L1 and resistor RS connected in series to the node X1. The NMOS transistor M1 has its gate connected to node b1, its source to ground, and its drain to the LOAD. A capacitor CGS is connected between node b1 and ground.
image_name:(b)
description:The image labeled '(b)' is a chip photograph of a 300 GHz CMOS oscillator. The photograph shows a section of an integrated circuit, likely fabricated using 65 nm technology. The layout includes several distinct features:

1. **Components and Structure:**
- The central feature is a spiral inductor, which is a common component in RF circuits for creating resonant circuits. This inductor is formed by a series of concentric loops of metal traces on the silicon substrate.
- Around the inductor, there are several rectangular and polygonal metal pads or structures, which could be connection points or other passive components.
- The overall design is compact, typical of high-frequency integrated circuits, where minimizing parasitic elements is critical.

2. **Connections and Interactions:**
- The spiral inductor is likely connected to other parts of the circuit through metal traces that extend from its ends. These traces are used to route signals to and from the inductor.
- The surrounding metal pads might serve as connections for other components, such as capacitors or transistors, to form the complete oscillator circuit.

3. **Labels, Annotations, and Key Features:**
- There are no visible labels or annotations directly on the chip photograph, as is typical with microphotographs of integrated circuits. However, the context provided indicates that this is part of a high-frequency oscillator circuit.
- The design's symmetry and the presence of the spiral inductor suggest that this section of the chip is optimized for RF performance, likely minimizing losses and maximizing the Q-factor of the inductor.

(a) Use of resonance to cancel transistor capacitance, (b) chip photograph of a 300 GHz CMOS oscillator.

## 11.3 ANALYSIS PROCEDURE

We have thus far seen a number of concepts and tools that help us study the frequency response of circuits. Specifically, we have observed that:

- The frequency response refers to the magnitude of the transfer function of a system. ${ }^{9}$
- Bode's approximation simplifies the task of plotting the frequency response if the poles and zeros are known.

[^10]- In many cases, it is possible to associate a pole with each node in the signal path.
- Miller's theorem proves helpful in decomposing floating capacitors into grounded elements.
- Bipolar and MOS devices exhibit various capacitances that limit the speed of circuits.

In order to methodically analyze the frequency response of various circuits, we prescribe the following steps:

1. Determine which capacitors impact the low-frequency region of the response and compute the low-frequency cut-off. In this calculation, the transistor capacitances can be neglected as they typically impact only the high-frequency region.
2. Calculate the midband gain by replacing the above capacitors with short circuits while still neglecting the transistor capacitances.
3. Identify and add to the circuit the capacitances contributed by each transistor.
4. Noting ac grounds (e.g., the supply voltage or constant bias voltages), merge the capacitors that are in parallel and omit those that play no role in the circuit.
5. Determine the high-frequency poles and zeros by inspection or by computing the transfer function. Miller's theorem may prove useful here.
6. Plot the frequency response using Bode's rules or exact calculations.

We now apply this procedure to various amplifier topologies.

## 11.4 FREQUENCY RESPONSE OF CE AND CS STAGES

### 11.4.1 Low-Frequency Response

As mentioned in Section 11.1.6, the gain of amplifiers may fall at low frequencies due to certain capacitors in the signal path. Let us consider a general CS stage with its input bias network and an input coupling capacitor [Fig. 11.28(a)]. At low frequencies, the transistor capacitances negligibly affect the frequency response, leaving only $C_{i}$ as the frequency-dependent component. We write $V_{\text {out }} / V_{\text {in }}=\left(V_{\text {out }} / V_{X}\right)\left(V_{X} / V_{\text {in }}\right)$, neglect channellength modulation, and note that both $R_{1}$ and $R_{2}$ are tied between $X$ and ac ground. Thus, $V_{\text {out }} / V_{X}=-R_{D} /\left(R_{S}+1 / g_{m}\right)$ and

$$
\begin{align*}
\frac{V_{X}}{V_{i n}}(s) & =\frac{R_{1} \| R_{2}}{R_{1} \| R_{2}+\frac{1}{C_{i} s}}  \tag{11.51}\\
& =\frac{\left(R_{1} \| R_{2}\right) C_{i} s}{\left(R_{1} \| R_{2}\right) C_{i} s+1} . \tag{11.52}
\end{align*}
$$

Similar to the high-pass filter of Fig. 11.16, this network attenuates the low frequencies, dictating that the lower cut-off be chosen below the lowest signal frequency, $f_{\text {sig,min }}$ (e.g., 20 Hz in audio applications):

$$
\begin{equation*}
\frac{1}{2 \pi\left[\left(R_{1} \| R_{2}\right) C_{i}\right]}<f_{\text {sig,min }} \tag{11.53}
\end{equation*}
$$

In applications demanding a greater midband gain, we place a "bypass" capacitor in parallel with $R_{S}$ [Fig. 11.28(b)] so as to remove the effect of degeneration at midband frequencies. To quantify the role of $C_{b}$, we place its impedance, $1 /\left(C_{b} s\right)$, in parallel with $R_{S}$

[^0]:    ${ }^{2}$ Since the resistors are linear, the signals need not be small in this case.

[^1]:    ${ }^{3}$ In reality, MOS devices carry a small current for $V_{G S}=V_{T H}$, making these observations only an approximate illustration.

[^2]:    ${ }^{4}$ Interestingly, older literature has considered this effect troublesome.
${ }^{5}$ We have chosen a MOS pair here to show that the treatment is the same for both technologies.

[^3]:    ${ }^{6}$ But with $\lambda \neq 0$, it would.

[^4]:    *This section can be skipped in a first reading.

[^5]:    ${ }^{1}$ Channel-length modulation is neglected here.
${ }^{2}$ We use upper-case letters for frequency-domain quantities (Laplace transforms) even though they denote small-signal values.

[^6]:    ${ }^{4}$ For example, by immersing the circuit in liquid nitrogen $(T=77 \mathrm{~K})$, but requiring that the user carry a tank around!

[^7]:    ${ }^{5}$ Complex poles may result in sharp peaks in the frequency response, an effect neglected in Bode's approximation.

[^8]:    ${ }^{6}$ As mentioned in Chapter 4, both forward-biased and reversed-biased junctions contain a depletion region and hence a capacitance associated with it.

[^9]:    ${ }^{7}$ As mentioned in Chapter 6, the S/D areas protrude under the gate during fabrication.

[^10]:    ${ }^{9}$ In a more general case, the frequency response also includes the phase of the transfer function, as studied in Chapter 12.

image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Ci, type: Capacitor, value: Ci, ports: {Np: Vin, Nn: X}
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: X}
name: R2, type: Resistor, value: R2, ports: {N1: X, N2: GND}
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: X}
]
extrainfo:This is a common source amplifier circuit with an input coupling capacitor Ci and a bypass resistor RS. The NMOS transistor M1 is used for amplification.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Ci, type: Capacitor, value: Ci, ports: {Np: Vin, Nn: X}
name: R1, type: Resistor, value: R1, ports: {N1: X, N2: VDD}
name: R2, type: Resistor, value: R2, ports: {N1: X, N2: GND}
name: RS, type: Resistor, value: RS, ports: {N1: S, N2: GND}
name: RD, type: Resistor, value: RD, ports: {N1: Vout, N2: VDD}
name: M1, type: NMOS, ports: {S: S, D: Vout, G: X}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a common source amplifier with bypassed degeneration. It includes an NMOS transistor (M1) with a source degeneration resistor (RS) bypassed by a capacitor. The input is AC-coupled via capacitor Ci, and the output is taken at Vout.
image_name:(c)
description:The graph labeled as (c) is a frequency response plot, typically used to illustrate the behavior of a system over a range of frequencies. This type of graph is often a Bode plot, which displays both the magnitude and phase of a system's transfer function.

1. **Type of Graph and Function:**
- The graph is a Bode plot, showing the frequency response of a circuit with bypassed degeneration.

2. **Axes Labels and Units:**
- The x-axis represents frequency, likely in hertz (Hz), and is typically plotted on a logarithmic scale to cover a wide range of frequencies.
- The y-axis represents gain, usually in decibels (dB), and may also include a phase plot, typically in degrees.

3. **Overall Behavior and Trends:**
- The graph likely shows a low-frequency roll-off, a midband flat gain region, and a high-frequency roll-off.
- In the midband region, the gain is relatively constant, indicating stable amplification.
- The low and high-frequency roll-offs demonstrate the bandwidth limitations of the circuit.

4. **Key Features and Technical Details:**
- The graph may show a peak or resonance at certain frequencies due to the bypassed degeneration.
- Critical points such as the -3 dB bandwidth are likely marked, indicating the frequency range where the gain is within 3 dB of the maximum.
- Phase shifts at certain frequencies may also be depicted, showing how the phase of the output signal changes relative to the input.

5. **Annotations and Specific Data Points:**
- Annotations might include markers for cutoff frequencies or resonance peaks.
- Specific numerical values for key points such as peak gain or cutoff frequencies may be provided, although these are not visible in the image description.

The graph effectively demonstrates the impact of bypassed degeneration on the frequency response, highlighting changes in gain and bandwidth.

(a)
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Ci, type: Capacitor, value: Ci, ports: {Np: Vin, Nn: X}
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: X}
name: R2, type: Resistor, value: R2, ports: {N1: X, N2: GND}
name: RS, type: Resistor, value: RS, ports: {N1: X, N2: S1}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: M1, type: NMOS, ports: {S: S1, D: Vout, G: X}
name: Cb, type: Capacitor, value: Cb, ports: {Np: S1, Nn: GND}
]
extrainfo:This is a common-source amplifier with a bypassed source degeneration. The bypass capacitor Cb increases the gain by reducing the effect of the source resistor RS at higher frequencies.

(b)
image_name:Figure 11.28(c)
description:The graph is a Bode plot representing the frequency response of a common-source amplifier with bypassed source degeneration. The x-axis represents the angular frequency (ω) on a logarithmic scale, while the y-axis represents the magnitude of the voltage gain, \( \left| \frac{V_{\text{out}}}{V_{X}} \right| \), also on a logarithmic scale.

**Axes Labels and Units:**
- **X-axis:** Angular frequency (ω)
- **Y-axis:** Voltage gain magnitude, \( \left| \frac{V_{\text{out}}}{V_{X}} \right| \)

**Overall Behavior and Trends:**
- The graph shows a low-frequency gain starting at \( \frac{g_{m}R_{D}}{1 + g_{m}R_{S}} \).
- As frequency increases, the gain rises and reaches a higher plateau at \( g_{m}R_{D} \).
- There is a noticeable transition region between these two plateaus.

**Key Features and Technical Details:**
- The initial gain plateau occurs at \( \frac{g_{m}R_{D}}{1 + g_{m}R_{S}} \), indicating the effect of source degeneration at low frequencies.
- The transition begins at the frequency \( \frac{1}{R_{S}C_{b}} \) and ends at \( \frac{1 + g_{m}R_{S}}{R_{S}C_{b}} \).
- The high-frequency plateau is \( g_{m}R_{D} \), showing the increased gain due to the bypass capacitor reducing the effect of \( R_{S} \) at higher frequencies.

**Annotations and Specific Data Points:**
- The plot includes dashed lines to indicate the cutoff frequencies \( \frac{1}{R_{S}C_{b}} \) and \( \frac{1 + g_{m}R_{S}}{R_{S}C_{b}} \), marking the transition region.
- The gain levels at both low and high frequencies are annotated as \( \frac{g_{m}R_{D}}{1 + g_{m}R_{S}} \) and \( g_{m}R_{D} \) respectively.

(c)

Figure 11.28 (a) CS stage with input coupling capacitor, (b) effect of bypassed degeneration, (c) frequency response with bypassed degeneration.
in the midband gain expression:

$$
\begin{align*}
\frac{V_{\text {out }}}{V_{X}}(s) & =\frac{-R_{D}}{R_{S} \| \frac{1}{C_{b} s}+\frac{1}{g_{m}}}  \tag{11.54}\\
& =\frac{-g_{m} R_{D}\left(R_{S} C_{b} s+1\right)}{R_{S} C_{b} s+g_{m} R_{S}+1} \tag{11.55}
\end{align*}
$$

Figure 11.28(c) shows the Bode plot of the frequency response in this case. At frequencies well below the zero, the stage operates as a degenerated CS amplifier, and at frequencies well above the pole, the circuit experiences no degeneration. Thus, the pole frequency must be chosen significantly smaller than the lowest signal frequency of interest.

The above analysis can also be applied to a CE stage. Both types exhibit low-frequency roll-off due to the input coupling capacitor and the degeneration bypass capacitor.

### 11.4.2 High-Frequency Response

Consider the CE and CS amplifiers shown in Fig. 11.29(a), where $R_{S}$ may represent the output impedance of the preceding stage, i.e., it is not added deliberately. Identifying the capacitances of $Q_{1}$ and $M_{1}$, we arrive at the complete circuits depicted in Fig. 11.29(b), where the source-bulk capacitance of $M_{1}$ is grounded on both ends. The small-signal equivalents of these circuits differ by only $r_{\pi}$ [Fig. 11.29(c)], ${ }^{10}$ and can be reduced to one if $V_{i n}, R_{S}$ and $r_{\pi}$ are replaced with their Thevenin equivalent [Fig. 11.29(d)]. In practice, $R_{S} \ll r_{\pi}$ and hence $R_{\text {Thev }} \approx R_{S}$. Note that the output resistance of each transistor would simply appear in parallel with $R_{L}$.

With this unified model, we now study the high-frequency response, first applying Miller's approximation to develop insight and then performing an accurate analysis to arrive at more general results.

### 11.4.3 Use of Miller's Theorem

With $C_{X Y}$ tied between two floating nodes, we cannot simply associate one pole with each node. However, following Miller's approximation as in Example 11.10, we can decompose

[^0]image_name:(a)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: b1}
name: RL, type: Resistor, value: RL, ports: {N1: VCC, N2: Vout}
name: Q1, type: NPN, ports: {C: VCC, B: b1, E: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: g1}
name: RL, type: Resistor, value: RL, ports: {N1: VDD, N2: Vout}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: g1}
]
extrainfo:The circuit diagram includes two configurations: a common-emitter (CE) stage using an NPN transistor (Q1) and a common-source (CS) stage using an NMOS transistor (M1). Both stages have a resistor (RL) connected to the supply voltage (VCC or VDD) and the output (Vout). A resistor (RS) is connected between the input (Vin) and the base/gate of the transistors.

(a)
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: b1, E: GND}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: b1}
name: RL, type: Resistor, value: RL, ports: {N1: VDD, N2: Vout}
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: b1, Nn: GND}
name: Cμ, type: Capacitor, value: Cμ, ports: {Np: Vout, Nn: b1}
name: CCS, type: Capacitor, value: CCS, ports: {Np: Vout, Nn: GND}
name: CGD, type: Capacitor, value: CGD, ports: {Np: Vout, Nn: Vin}
name: CGS, type: Capacitor, value: CGS, ports: {Np: Vin, Nn: GND}
name: CDB, type: Capacitor, value: CDB, ports: {Np: Vout, Nn: GND}
name: CSB, type: Capacitor, value: CSB, ports: {Np: GND, Nn: GND}
]
extrainfo:The circuit diagram includes two configurations: a common-emitter (CE) stage using an NPN transistor (Q1) and a common-source (CS) stage using an NMOS transistor (M1). Both stages have a resistor (RL) connected to the supply voltage (VCC or VDD) and the output (Vout). A resistor (RS) is connected between the input (Vin) and the base/gate of the transistors.

(b)
(c)
image_name:(c)
description:
[
name: VThev, type: VoltageSource, value: VThev, ports: {Np: X, Nn: GND}
name: RThev, type: Resistor, value: RThev, ports: {N1: X, N2: Vx}
name: Cin, type: Capacitor, value: Cin, ports: {Np: X, Nn: GND}
name: CXY, type: Capacitor, value: CXY, ports: {Np: X, Nn: Y}
name: gmVx, type: VoltageControlledCurrentSource, ports: {Np: Y, Nn: GND}
name: Cout, type: Capacitor, value: Cout, ports: {Np: Vout, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit diagram represents a small-signal equivalent model with a voltage source VThev and resistor RThev forming the Thevenin equivalent at the input. Capacitor Cin is connected to ground, and CXY is connected between nodes X and Y. The voltage-controlled current source gmVx is connected at node Y. The output is taken across the resistor RL and capacitor Cout, which are connected to ground.

(d)

Figure 11.29 (a) CE and CS stages, (b) inclusion of transistor capacitances, (c) smallsignal equivalents, (d) unified model of both circuits.
$C_{X Y}$ into two grounded components (Fig. 11.30):

$$
\begin{align*}
& C_{X}=\left(1+g_{m} R_{L}\right) C_{X Y}  \tag{11.56}\\
& C_{Y}=\left(1+\frac{1}{g_{m} R_{L}}\right) C_{X Y} \tag{11.57}
\end{align*}
$$

image_name:Figure 11.29 (c)
description:
[
name: VThev, type: VoltageSource, value: VThev, ports: {Np: VThev, Nn: GND}
name: RThev, type: Resistor, value: RThev, ports: {N1: VThev, N2: X}
name: CX, type: Capacitor, value: CX, ports: {Np: X, Nn: GND}
name: Cin, type: Capacitor, value: Cin, ports: {Np: X, Nn: GND}
name: gmVx, type: VoltageControlledCurrentSource, ports: {Np: Y, Nn: GND}
name: Cout, type: Capacitor, value: Cout, ports: {Np: Y, Nn: GND}
name: CY, type: Capacitor, value: CY, ports: {Np: Y, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Y, N2: Vout}
]
extrainfo:The circuit is a small-signal model with a voltage source VThev driving the input. The voltage-controlled current source gmVx is connected at node Y. The output is taken across RL and Cout, connected to ground. The circuit includes capacitors CX and Cin at the input, and CY at the output.

$$
\begin{aligned}
& \text { CE Stage } \\
& \hline v_{\text {Thev }}=v_{\text {in }} \frac{r_{\pi}}{r_{\pi}+R_{\mathrm{S}}} \\
& R_{\text {Thev }}=R_{\mathrm{S}} \| r_{\pi} \\
& c_{\mathrm{X}}=c_{\mu}\left(1+g_{\mathrm{m}} R_{\mathrm{L}}\right) \\
& c_{\mathrm{Y}}=c_{\mu}\left(1+\frac{1}{g_{\mathrm{m}} R_{\mathrm{L}}}\right)
\end{aligned}
$$

$$
\begin{aligned}
& c_{\mathrm{X}}=c_{\mathrm{GD}}\left(1+g_{\mathrm{m}} R_{\mathrm{L}}\right) \\
& c_{\mathrm{Y}}=c_{\mathrm{GD}}\left(1+\frac{1}{g_{\mathrm{m}} R_{\mathrm{L}}}\right)
\end{aligned}
$$

Figure 11.30 Parameters in unified model of CE and CS stages with Miller's approximation.

Now, each node sees a resistance and capacitances only to ground. In accordance with our notations in Section 11.1, we write

$$
\begin{align*}
& \left|\omega_{p, \text { in }}\right|=\frac{1}{R_{\text {Thev }}\left[C_{\text {in }}+\left(1+g_{m} R_{L}\right) C_{X Y}\right]}  \tag{11.58}\\
& \left|\omega_{p, \text { out }}\right|=\frac{1}{R_{L}\left[C_{\text {out }}+\left(1+\frac{1}{g_{m} R_{L}}\right) C_{X Y}\right]}
\end{align*}
$$

If $g_{m} R_{L} \gg 1$, the capacitance at the output node is simply equal to $C_{o u t}+C_{X Y}$.
The intuition gained from the application of Miller's theorem proves invaluable. The input pole is approximately given by the source resistance, the base-emitter or gate-source capacitance, and the Miller multiplication of the base-collector or gate-drain capacitance. The Miller multiplication makes it undesirable to have a high gain in the circuit. The output pole is roughly determined by the load resistance, the collector-substrate or drain-bulk capacitance, and the base-collector or gate-drain capacitance.

Example In the CE stage of Fig. 11.29(a), $R_{S}=200 \Omega, I_{C}=1 \mathrm{~mA}, \beta=100, C_{\pi}=100 \mathrm{fF}, C_{\mu}=$ 11.15 20 fF , and $C_{C S}=30 \mathrm{fF}$.
(a) Calculate the input and output poles if $R_{L}=2 \mathrm{k} \Omega$. Which node appears as the speed bottleneck (limits the bandwidth)?
(b) Is it possible to choose $R_{L}$ such that the output pole limits the bandwidth?

Solution (a) Since $r_{\pi}=2.6 \mathrm{k} \Omega$, we have $R_{\text {Thev }}=186 \Omega$. Fig. 11.30 and Eqs. (11.58) and (11.59) thus give

$$
\begin{align*}
\left|\omega_{p, \text { in }}\right| & =2 \pi \times(516 \mathrm{MHz})  \tag{11.60}\\
\left|\omega_{p, \text { out }}\right| & =2 \pi \times(1.59 \mathrm{GHz}) . \tag{11.61}
\end{align*}
$$

We observe that the Miller effect multiplies $C_{\mu}$ by a factor of 78 , making its contribution much greater than that of $C_{\pi}$. As a result, the input pole limits the bandwidth.
(b) We must seek such a value of $R_{L}$ that yields $\left|\omega_{p, \text { in }}\right|>\omega_{p, \text { out }} \mid$ :

$$
\begin{equation*}
\frac{1}{\left(R_{S} \| r_{\pi}\right)\left[C_{\pi}+\left(1+g_{m} R_{L}\right) C_{\mu}\right]}>\frac{1}{R_{L}\left[C_{C S}+\left(1+\frac{1}{g_{m} R_{L}}\right) C_{\mu}\right]} . \tag{11.62}
\end{equation*}
$$

If $g_{m} R_{L} \gg 1$, then we have

$$
\begin{equation*}
\left[C_{C S}+C_{\mu}-g_{m}\left(R_{S} \| r_{\pi}\right) C_{\mu}\right] R_{L}>\left(R_{S} \| r_{\pi}\right) C_{\pi} \tag{11.63}
\end{equation*}
$$

With the values assumed in this example, the left-hand side is negative, implying that no solution exists. The reader can prove that this holds even if $g_{m} R_{L}$ is not much greater than unity. Thus, the input pole remains the speed bottleneck here.

Exercise Repeat the above example if $I_{C}=2 \mathrm{~mA}$ and $C_{\pi}=180 \mathrm{fF}$.

Example An electrical engineering student designs the CS stage of Fig. 11.29(a) for a certain low11.16 frequency gain and high-frequency response. Unfortunately, in the layout phase, the student uses a MOSFET half as wide as that in the original design. Assuming that the bias current is also halved, determine the gain and the poles of the circuit.

Solution Both the width and the bias current of the transistor are halved, and so is its transconductance (why?). The small-signal gain, $g_{m} R_{L}$, is therefore halved.

Reducing the transistor width by a factor of two also lowers all of the capacitances by the same factor. From Fig. 11.30 and Eqs. (11.58) and (11.59), we can express the poles as

$$
\begin{align*}
\left|\omega_{p, \text { in }}\right| & =\frac{1}{R_{S}\left[\frac{C_{\text {in }}}{2}+\left(1+\frac{g_{m} R_{L}}{2}\right) \frac{C_{X Y}}{2}\right]}  \tag{11.64}\\
\left|\omega_{p, \text { out }}\right| & =\frac{1}{R_{L}\left[\frac{C_{\text {out }}}{2}+\left(1+\frac{2}{g_{m} R_{L}}\right) \frac{C_{X Y}}{2}\right]} \tag{11.65}
\end{align*}
$$

where $C_{i n}, g_{m}, C_{X Y}$ and $C_{\text {out }}$ denote the parameters corresponding to the original device width. We observe that $\omega_{p, i n}$ has risen in magnitude by more than a factor of two, and $\omega_{p, \text { out }}$ by approximately a factor of two (if $g_{m} R_{L} \gg 2$ ). In other words, the gain is halved and the bandwidth is roughly doubled, suggesting that the gain-bandwidth product is approximately constant.

What happens if both the width and the bias current are twice their nominal values?

### 11.4.4 Direct Analysis

The use of Miller's theorem in the previous section provides a quick and intuitive perspective on the performance. However, we must carry out a more accurate analysis so as to understand the limitations of Miller's approximation in this case.

The circuit of Fig. 11.29(d) contains two nodes and can therefore be solved by writing two KCLs. That is, ${ }^{11}$

$$
\begin{align*}
& \text { At Node } X:\left(V_{\text {out }}-V_{X}\right) C_{X Y} s=V_{X} C_{\text {in }} s+\frac{V_{X}-V_{\text {Thev }}}{R_{\text {Thev }}}  \tag{11.66}\\
& \text { At Node } Y:\left(V_{X}-V_{\text {out }}\right) C_{X Y} s=g_{m} V_{X}+V_{\text {out }}\left(\frac{1}{R_{L}}+C_{\text {out }} s\right)
\end{align*}
$$

We compute $V_{X}$ from Eq. (11.67):

$$
\begin{equation*}
V_{X}=V_{\text {out }} \frac{C_{X Y} s+\frac{1}{R_{L}}+C_{\text {out }} s}{C_{X Y} s-g_{m}} \tag{11.68}
\end{equation*}
$$

[^1]and substitute the result in Eq. (11.66) to arrive at
\$\$

$$
\begin{equation*}
V_{\text {out }} C_{X Y} s-\left(C_{X Y} s+C_{\text {in }} s+\frac{1}{R_{\text {Thev }}}\right) \frac{C_{X Y} s+\frac{1}{R_{L}}+C_{\text {out }} s}{C_{X Y} s-g_{m}} V_{\text {out }}=\frac{-V_{\text {Thev }}}{R_{\text {Thev }}} \tag{11.69}
\end{equation*}
$$

\$\$

It follows that

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {Thev }}}(s)=\frac{\left(C_{X Y} s-g_{m}\right) R_{L}}{a s^{2}+b s+1} \tag{11.70}
\end{equation*}
$$

where

$$
\begin{align*}
& a=R_{\text {Thev }} R_{L}\left(C_{\text {in }} C_{X Y}+C_{\text {out }} C_{X Y}+C_{\text {in }} C_{\text {out }}\right)  \tag{11.71}\\
& b=\left(1+g_{m} R_{L}\right) C_{X Y} R_{\text {Thev }}+R_{\text {Thev }} C_{\text {in }}+R_{L}\left(C_{X Y}+C_{\text {out }}\right) \tag{11.72}
\end{align*}
$$

Note from Fig. 11.30 that for a CE stage, Eq. (11.70) must be multiplied by $r_{\pi} /\left(R_{S}+r_{\pi}\right)$ to obtain $V_{\text {out }} / V_{\text {in }}$ —without affecting the location of the poles and the zero.

Let us examine the above results carefully. The transfer function exhibits a zero at

$$
\begin{equation*}
\omega_{z}=\frac{g_{m}}{C_{X Y}} \tag{11.73}
\end{equation*}
$$

(The Miller approximation fails to predict this zero.) Since $C_{X Y}$ (i.e., the base-collector or the gate-drain overlap capacitance) is relatively small, the zero typically appears at very high frequencies and hence is unimportant. ${ }^{12}$

As expected, the system contains two poles given by the values of $s$ that force the denominator to zero. We can solve the quadratic $a s^{2}+b s+1=0$ to determine the poles but the results provide little insight. Instead, we first make an interesting observation in regard to the quadratic denominator: if the poles are given by $\omega_{p 1}$ and $\omega_{p 2}$, we can write

$$
\begin{align*}
a s^{2}+b s+1 & =\left(\frac{s}{\omega_{p 1}}+1\right)\left(\frac{s}{\omega_{p 2}}+1\right)  \tag{11.74}\\
& =\frac{s^{2}}{\omega_{p 1} \omega_{p 2}}+\left(\frac{1}{\omega_{p 1}}+\frac{1}{\omega_{p 2}}\right) s+1 \tag{11.75}
\end{align*}
$$

Now suppose one pole is much farther from the origin than the other: $\omega_{p 2} \gg \omega_{p 1}$. (This is called the "dominant pole" approximation to emphasize that $\omega_{p 1}$ dominates the frequency response). Then, $\omega_{p 1}^{-1}+\omega_{p 2}^{-1} \approx \omega_{p 1}^{-1}$, i.e.,

$$
\begin{equation*}
b=\frac{1}{\omega_{p 1}} \tag{11.76}
\end{equation*}
$$

and from Eq. (11.72),

$$
\begin{equation*}
\left|\omega_{p 1}\right|=\frac{1}{\left(1+g_{m} R_{L}\right) C_{X Y} R_{\text {Thev }}+R_{\text {Thev }} C_{\text {in }}+R_{L}\left(C_{X Y}+C_{\text {out }}\right)} \tag{11.77}
\end{equation*}
$$

How does this result compare with that obtained using the Miller approximation? Equation (11.77) does reveal the Miller effect of $C_{X Y}$ but it also contains the additional term $R_{L}\left(C_{X Y}+C_{\text {out }}\right)$ [which is close to the output time constant predicted by Eq. (11.59)].

[^2]To determine the "nondominant" pole, $\omega_{p 2}$, we recognize from Eqs. (11.75) and (11.76) that

$$
\begin{align*}
\left|\omega_{p 2}\right| & =\frac{b}{a}  \tag{11.78}\\
& =\frac{\left(1+g_{m} R_{L}\right) C_{X Y} R_{\text {Thev }}+R_{\text {Thev }} C_{\text {in }}+R_{L}\left(C_{X Y}+C_{\text {out }}\right)}{R_{\text {Thev }} R_{L}\left(C_{\text {in }} C_{X Y}+C_{\text {out }} C_{X Y}+C_{\text {in }} C_{\text {out }}\right)} . \tag{11.79}
\end{align*}
$$

Example Using the dominant-pole approximation, compute the poles of the circuit shown in Fig. 11.17 11.31(a). Assume both transistors operate in saturation and $\lambda \neq 0$.

Solution Noting that $C_{S B 1}, C_{G S 2}$, and $C_{S B 2}$ do not affect the circuit (why?), we add the remaining capacitances as depicted in Fig. 11.31(b), simplifying the result as illustrated in Fig. 11.31(c), where

$$
\begin{align*}
C_{\text {in }} & =C_{G S 1}  \tag{11.80}\\
C_{X Y} & =C_{G D 1}  \tag{11.81}\\
C_{\text {out }} & =C_{D B 1}+C_{G D 2}+C_{D B 2} \tag{11.82}
\end{align*}
$$

It follows from Eqs. (11.77) and (11.79) that

$$
\begin{align*}
& \omega_{p 1} \approx \frac{1}{\left[1+g_{m 1}\left(r_{O 1} \| r_{O 2}\right)\right] C_{X Y} R_{S}+R_{S} C_{\text {in }}+\left(r_{O 1} \| r_{O 2}\right)\left(C_{X Y}+C_{\text {out }}\right)}  \tag{11.83}\\
& \omega_{p 2} \approx \frac{\left[1+g_{m 1}\left(r_{O 1} \| r_{O 2}\right)\right] C_{X Y} R_{S}+R_{S} C_{\text {in }}+\left(r_{O 1} \| r_{O 2}\right)\left(C_{X Y}+C_{\text {out }}\right)}{R_{S}\left(r_{O 1} \| r_{O 2}\right)\left(C_{\text {in }} C_{X Y}+C_{\text {out }} C_{X Y}+C_{\text {in }} C_{\text {out }}\right)} \tag{11.84}
\end{align*}
$$

image_name:(a)
description:
[
name: M2, type: PMOS, ports: {S: VDD, D: Vout, G: Vb}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: g1}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: g1}
name: CDB2, type: Capacitor, value: CDB2, ports: {Np: GND, Nn: GND}
name: CGD2, type: Capacitor, value: CGD2, ports: {Np: GND, Nn: Vout}
name: CGD1, type: Capacitor, value: CGD1, ports: {Np: GND, Nn: Vout}
name: CDB1, type: Capacitor, value: CDB1, ports: {Np: Vout, Nn: GND}
name: CGS1, type: Capacitor, value: CGS1, ports: {Np: g1, Nn: GND}
name: CXY, type: Capacitor, value: CXY, ports: {Np: Vout, Nn: Vout}
name: Cin, type: Capacitor, value: Cin, ports: {Np: g1, Nn: GND}
name: Cout, type: Capacitor, value: Cout, ports: {Np: Vout, Nn: GND}
name: ro1||ro2, type: Resistor, value: ro1||ro2, ports: {N1: Vout, N2: GND}
]
extrainfo:This circuit represents a multi-stage amplifier with PMOS and NMOS transistors. The PMOS transistor M2 is connected to VDD, while the NMOS transistor M1 is connected to ground. The input voltage Vin is fed through a resistor RS to the gate of M1. Various capacitors are connected to the nodes for frequency compensation and stabilization.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: M2, type: PMOS, ports: {S: VDD, D: Vout, G: Vb}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: G1}
name: CSB2, type: Capacitor, value: CSB2, ports: {Np: GND, Nn: Vout}
name: CGD2, type: Capacitor, value: CGD2, ports: {Np: GND, Nn: Vout}
name: CGD1, type: Capacitor, value: CGD1, ports: {Np: GND, Nn: Vout}
name: CDB2, type: Capacitor, value: CDB2, ports: {Np: GND, Nn: Vout}
name: CDB1, type: Capacitor, value: CDB1, ports: {Np: GND, Nn: Vout}
name: CGS1, type: Capacitor, value: CGS1, ports: {Np: GND, Nn: Vin}
name: CXY, type: Capacitor, value: CXY, ports: {Np: GND, Nn: Vout}
name: Cin, type: Capacitor, value: Cin, ports: {Np: GND, Nn: Vin}
name: Cout, type: Capacitor, value: Cout, ports: {Np: GND, Nn: Vout}
name: ro1||ro2, type: Resistor, value: ro1||ro2, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a common-source amplifier with NMOS M1 and PMOS M2. The input is Vin, and the output is Vout. Various capacitors are connected to manage frequency response and stability.
image_name:(c)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: g1}
name: M2, type: PMOS, ports: {S: VDD, D: Vout, G: Vb}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: g1}
name: CDB1, type: Capacitor, value: CDB1, ports: {Np: Vout, Nn: GND}
name: CDB2, type: Capacitor, value: CDB2, ports: {Np: GND, Nn: Vout}
name: CGD1, type: Capacitor, value: CGD1, ports: {Np: Vout, Nn: g1}
name: CGD2, type: Capacitor, value: CGD2, ports: {Np: Vout, Nn: Vb}
name: CGS1, type: Capacitor, value: CGS1, ports: {Np: g1, Nn: GND}
name: CXY, type: Capacitor, value: CXY, ports: {Np: g1, Nn: Vout}
name: Cin, type: Capacitor, value: Cin, ports: {Np: g1, Nn: GND}
name: Cout, type: Capacitor, value: Cout, ports: {Np: Vout, Nn: GND}
name: rO1||rO2, type: Resistor, value: rO1||rO2, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit diagram (c) is a common-source amplifier configuration with an NMOS transistor (M1). The input signal is applied to the gate of M1 through a resistor RS, and the output is taken from the drain of M1. The circuit includes various capacitors for frequency response shaping, and a parallel resistor rO1||rO2 connected to the output node.

(a)

Figure 11.31
Exercise Repeat the above example if $\lambda \neq 0$.

Example In the CS stage of Fig. 11.29(a), we have $R_{S}=200 \Omega, C_{G S}=250 \mathrm{fF}, C_{G D}=80 \mathrm{fF}$, 11.18 $C_{D B}=100 \mathrm{fF}, g_{m}=(150 \Omega)^{-1}, \lambda=0$, and $R_{L}=2 \mathrm{k} \Omega$. Plot the frequency response with the aid of (a) Miller's approximation, (b) the exact transfer function, (c) the dominantpole approximation.

Solution (a) With $g_{m} R_{L}=13.3$, Eqs. (11.58) and (11.59) yield

$$
\begin{align*}
\left|\omega_{p, \text { in }}\right| & =2 \pi \times(571 \mathrm{MHz})  \tag{11.85}\\
\left|\omega_{p, \text { out }}\right| & =2 \pi \times(428 \mathrm{MHz}) \tag{11.86}
\end{align*}
$$

(b) The transfer function in Eq. (11.70) gives a zero at $g_{m} / C_{G D}=2 \pi \times(13.3 \mathrm{GHz})$. Also, $a=2.12 \times 10^{-20} \mathrm{~s}^{-2}$ and $b=6.39 \times 10^{-10} \mathrm{~s}$. Thus,

$$
\begin{align*}
& \left|\omega_{p 1}\right|=2 \pi \times(264 \mathrm{MHz})  \tag{11.87}\\
& \left|\omega_{p 2}\right|=2 \pi \times(4.53 \mathrm{GHz}) \tag{11.88}
\end{align*}
$$

Note the large error in the values predicted by Miller's approximation. This error arises because we have multiplied $C_{G D}$ by the midband gain $\left(1+g_{m} R_{L}\right)$ rather than the gain at high frequencies. ${ }^{13}$
(c) The results obtained in part (b) predict that the dominant-pole approximation produces relatively accurate results as the two poles are quite far apart. From Eqs. (11.77) and (11.79), we have

$$
\begin{align*}
& \left|\omega_{p 1}\right|=2 \pi \times(249 \mathrm{MHz})  \tag{11.89}\\
& \left|\omega_{p 2}\right|=2 \pi \times(4.79 \mathrm{GHz}) \tag{11.90}
\end{align*}
$$

Figure 11.32 plots the results. The low-frequency gain is equal to $22 \mathrm{~dB} \approx 13$ and the -3 dB bandwidth predicted by the exact equation is around 250 MHz .
image_name:Figure 11.32
description:The graph in Figure 11.32 is a Bode plot illustrating the magnitude of a transfer function in decibels (dB) versus frequency in hertz (Hz). The x-axis represents frequency on a logarithmic scale ranging from \(10^7\) Hz to \(10^{10}\) Hz, while the y-axis represents the magnitude of the transfer function, also on a logarithmic scale, ranging from -30 dB to 30 dB.

Three different curves are plotted:
1. **Dominant-Pole Approximation:** This is shown as a dash-dot line. It starts at a low-frequency gain of approximately 22 dB and shows a gradual decrease in magnitude as frequency increases.
2. **Miller's Approximation:** Represented by a dashed line, this curve also begins at the low-frequency gain of around 22 dB but diverges more significantly from the dominant-pole approximation as frequency increases, showing a more rapid decline.
3. **Exact Equation:** Illustrated by a solid line, this curve provides the most precise representation of the system's behavior, starting at the same low-frequency gain and maintaining accuracy across the frequency range.

Key features include:
- The low-frequency gain is approximately 22 dB, consistent across all three curves.
- The -3 dB point, indicating the bandwidth limit, occurs around 250 MHz for the exact equation, aligning with the context provided.
- As frequency increases beyond this point, the magnitude decreases, with the exact equation showing the most gradual decline compared to the approximations.

Annotations include a legend in the upper right corner identifying each curve type. The gridlines facilitate the reading of frequency and magnitude values at various points on the plot. This graph effectively demonstrates the differences in transfer function magnitude predictions between the dominant-pole approximation, Miller's approximation, and the exact equation across a broad frequency range.

Figure 11.32

Exercise Repeat the above example if the device width (and hence its capacitances) and the bias current are halved.

### 11.4.5 Input Impedance

The high-frequency input impedances of the CE and CS amplifiers determine the ease with which these circuits can be driven by other stages. Our foregoing analysis of

[^3]image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: c1, B: b1, E: GND}
name: RC, type: Resistor, value: RC, ports: {N1: c1, N2: VCC}
name: Cμ, type: Capacitor, value: Cμ, ports: {Np: b1, Nn: c1}
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: b1, Nn: GND}
name: CCS, type: Capacitor, value: CCS, ports: {Np: c1, Nn: GND}
]
extrainfo:This circuit is a common-emitter (CE) amplifier with input impedance defined by the capacitors and the transistor configuration. The input is at node 'b1', and the output is taken from the collector of Q1. The circuit is biased with VCC.

(a)
image_name:Figure 11.33 (b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: C1, G: b1}
name: RD, type: Resistor, value: RD, ports: {N1: C1, N2: VDD}
name: CGD, type: Capacitor, value: CGD, ports: {Np: b1, Nn: C1}
name: CGS, type: Capacitor, value: CGS, ports: {Np: b1, Nn: GND}
name: CDB, type: Capacitor, value: CDB, ports: {Np: C1, Nn: GND}
]
extrainfo:This circuit is a common-source (CS) amplifier stage. The input is at node 'b1', and the output is taken from the drain of M1. The circuit is biased with VDD. The input impedance is defined by the capacitors CGS and CGD, along with the transistor configuration.

(b)

Figure 11.33 Input impedance of (a) CE and (b) CS stages.
the frequency response and particularly the Miller approximation readily yields this impedance.

As illustrated in Fig. 11.33(a), the input impedance of a CE stage consists of two parallel components: $C_{\pi}+\left(1+g_{m} R_{D}\right) C_{\mu}$ and $r_{\pi} \cdot{ }^{14}$ That is,

$$
\begin{equation*}
Z_{i n} \approx \frac{1}{\left[C_{\pi}+\left(1+g_{m} R_{D}\right) C_{\mu}\right] s} \| r_{\pi} \tag{11.91}
\end{equation*}
$$

Similarly, the MOS counterpart exhibits an input impedance given by

$$
\begin{equation*}
Z_{i n} \approx \frac{1}{\left[C_{G S}+\left(1+g_{m} R_{D}\right) C_{G D}\right] s} \tag{11.92}
\end{equation*}
$$

With a high voltage gain, the Miller effect may substantially lower the input impedance at high frequencies.

Did you know?

Most RF receivers incorporate a common-source or common-emitter amplifier at their front end. This "low-noise" amplifier must present an input resistance of $50 \Omega$ so as to "match" the impedance of the antenna [Fig. (a)]. But how could a CS stage have such a low input resistance? A clever technique is to add an inductor in series with the source of the transistor [Fig. (b)]. It can be shown that the input impedance is given by

$$
Z_{i n}(s)=\frac{1}{C_{G S S}}+L_{15}+\frac{L_{1} g_{m}}{C_{G S}}
$$

Note that the last term is a real quantity, reprsenting a resistance. Proper choice of $L_{1}, g_{m}$, and $C_{G S}$ provides a value of $50 \Omega$. Next time you turn on your cell phone or your GPS, you may be receiving an RF signal through an inductively-degenerated CS amplifier.
image_name:(a)
description:The block diagram labeled as "(a)" represents a simplified receiver front-end, focusing on input impedance matching. It consists of the following key components:

1. **Antenna**: This is the input component that captures the RF signal from the environment. It is represented as a triangular symbol and is the entry point for the signal into the system.

2. **Low-Noise Amplifier (LNA)**: The antenna is directly connected to a Low-Noise Amplifier. The LNA is depicted as a triangle with the label \(A_0\), symbolizing its gain. The primary function of the LNA is to amplify the weak signals received by the antenna while adding minimal noise, thus improving the signal-to-noise ratio.

3. **Input Impedance \(R_{in}\)**: The input impedance of the system is specified as 50 Ω. This is a standard impedance value that ensures maximum power transfer from the antenna to the amplifier.

4. **Signal Flow**: The RF signal captured by the antenna flows into the LNA, where it is amplified. The input and output of the LNA are labeled as \(In(A_0)\) and \(Out(A_0)\) respectively, indicating the points at which the signal enters and exits the amplifier.

Overall, the system's primary function is to receive RF signals through the antenna and amplify them using the LNA with minimal noise addition, while ensuring proper impedance matching for efficient signal transfer. This setup is crucial for applications such as cell phones and GPS devices, where clear signal reception is necessary.
image_name:(b)
description:
[
name: Rin, type: Resistor, value: 50Ω, ports: {N1: In(A0), N2: b1}
name: A0, type: OpAmp, value: A0, ports: {InP: In(A0), InN: GND, OutP: Out(A0), OutN: GND}
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: b1, Nn: GND}
name: M1, type: NMOS, ports: {S: s1, D: LOAD, G: b1}
name: L1, type: Inductor, value: L1, ports: {N1: s1, N2: GND}
]
extrainfo:The circuit diagram (b) shows an inductively-degenerated common-source amplifier used for input impedance matching in a receiver. The NMOS transistor M1 has an inductor L1 in series with its source, which helps achieve the desired input impedance.

Input impedance matching in a receiver.

[^4]
## 11.5 FREQUENCY RESPONSE OF CB AND CG STAGES

### 11.5.1 Low-Frequency Response

As with CE and CS stages, the use of capacitive coupling leads to low-frequency roll-off in CB and CG amplifiers. Consider the CB circuit depicted in Fig. 11.34(a), where $I_{1}$ defines the bias current of $Q_{1}$ and $V_{b}$ is chosen to ensure operation in the forward active region ( $V_{b}$ is less than the collector bias voltage). How large should $C_{i}$ be? Since $C_{i}$ appears in series with $R_{S}$, we replace $R_{S}$ with $R_{S}+\left(C_{i} s\right)^{-1}$ in the midband gain expression, $R_{C} /\left(R_{S}+1 / g_{m}\right)$, and write the resulting transfer function as

$$
\begin{align*}
\frac{V_{\text {out }}}{V_{\text {in }}}(s) & =\frac{R_{C}}{R_{S}+\left(C_{i} s\right)^{-1}+1 / g_{m}}  \tag{11.93}\\
& =\frac{g_{m} R_{C} C_{i} s}{\left(1+g_{m} R_{S}\right) C_{i} s+g_{m}} \tag{11.94}
\end{align*}
$$

Equation (11.93) implies that the signal does not "feel" the effect of $C_{i}$ if $\left|\left(C_{i} s\right)^{-1}\right| \ll$ $R_{S}+1 / g_{m}$. From another perspective, Eq. (11.94) yields the response shown in Fig. 11.34(b), revealing a pole at

$$
\begin{equation*}
\left|\omega_{p}\right|=\frac{g_{m}}{\left(1+g_{m} R_{S}\right) C_{i}} \tag{11.95}
\end{equation*}
$$

and suggesting that this pole must remain quite lower than the minimum signal frequency of interest. These two conditions are equivalent.
image_name:(a)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: Ci, type: Capacitor, value: Ci, ports: {Np: X, Nn: e1}
name: RC, type: Resistor, value: RC, ports: {N1: Vout, N2: Vcc}
name: Q1, type: NPN, ports: {C: Vout, B: Vb, E: e1}
name: I1, type: CurrentSource, value: I1, ports: {Np: e1, Nn: GND}
]
extrainfo:The circuit is a common base (CB) amplifier stage with input capacitor coupling. It includes a resistor RS at the input, a coupling capacitor Ci, and a load resistor RC. The transistor Q1 is biased with a current source I1. The output is taken across the collector of Q1.
image_name:(b)
description:The graph in Figure 11.34(b) is a frequency response plot, specifically a Bode plot, showing the magnitude of the voltage gain \( |V_{out}/V_{in}| \) versus frequency \( \omega \).

Axes Labels and Units:
- **Horizontal Axis (x-axis):** Represents frequency \( \omega \). The units are not explicitly stated but are typically in radians per second in such contexts.
- **Vertical Axis (y-axis):** Represents the magnitude of the voltage gain \( |V_{out}/V_{in}| \). This is a dimensionless quantity and is often expressed in decibels (dB), though the axis here is not explicitly labeled with units.

Overall Behavior and Trends:
- The graph starts at a low frequency with a low gain and increases linearly on a logarithmic scale until it reaches a plateau.
- This behavior indicates the presence of a single dominant pole that dictates the high-frequency roll-off of the system.

Key Features and Technical Details:
- **Low-Frequency Gain:** At low frequencies, the gain is low, which is typical before the influence of the pole is felt.
- **Cutoff Frequency/Pole Location:** The graph shows a pole at \( \left|\omega_{p}\right| = \frac{g_{m}}{(1 + g_{m} R_{S}) C_{i}} \). This is the frequency at which the gain begins to level off.
- **High-Frequency Plateau:** Beyond the cutoff frequency, the gain stabilizes at a value of \( \frac{R_{D}}{R_{S} + \frac{1}{g_{m}}} \). This indicates the maximum gain achievable by the circuit at high frequencies.

Annotations and Specific Data Points:
- The graph is annotated with the expression for the pole \( \frac{g_{m}}{(1 + g_{m} R_{S}) C_{i}} \), highlighting the critical frequency where the behavior changes.
- The high-frequency gain level is marked as \( \frac{R_{D}}{R_{S} + \frac{1}{g_{m}}} \), indicating the asymptotic gain value.

This frequency response is typical for a common-base (CB) amplifier stage with input capacitor coupling, which avoids the Miller effect and thus maintains a higher bandwidth compared to other configurations.

Figure 11.34 (a) CB stage with input capacitor coupling, (b) resulting frequency response.

### 11.5.2 High-Frequency Response

We know from Chapters 5 and 7 that CB and CG stages exhibit a relatively low input impedance $\left(\approx 1 / g_{m}\right)$. The high-frequency response of these circuits does not suffer from Miller effect, an important advantage in some cases.

Consider the stages shown in Fig. 11.35, where $r_{O}=\infty$ and the transistor capacitances are included. Since $V_{b}$ is at ac ground, we note that (1) $C_{\pi}$ and $C_{G S}+C_{S B}$ go to ground; (2) $C_{C S}$ and $C_{\mu}$ of $Q_{1}$ appear in parallel to ground, and so do $C_{G D}$ and $C_{D B}$ of $M_{1}$; (3) no capacitance appears between the input and output networks, avoiding the Miller effect. In fact, with all of the capacitances seeing ground at one of their terminals, we can readily associate one pole with each node. At node $X$, the total resistance seen to ground is given
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: Y, B: Vb, E: X}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Y}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: CCS, type: Capacitor, value: CCS, ports: {Np: Y, Nn: GND}
name: Cμ, type: Capacitor, value: Cμ, ports: {Np: Y, Nn: Vb}
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: Vb, Nn: GND}
]
extrainfo:The circuit is a common-base amplifier stage with transistor capacitances included. It features an NPN transistor Q1 with a collector at node Y, a base at node Vb, and an emitter at node X. Capacitors CCS and Cμ are connected at node Y, while Cπ is connected to the base node Vb. The input is at Vin and the output is at Vout, connected to node Y.

(a)
image_name:(b)
description:
[
name: RD, type: Resistor, ports: {N1: VDD, N2: Y}
name: CDB, type: Capacitor, value: CDB, ports: {Np: Y, Nn: GND}
name: CGD, type: Capacitor, value: CGD, ports: {Np: Y, Nn: Vb}
name: M1, type: NMOS, ports: {S: X, D: Y, G: Vb}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: CSB, type: Capacitor, value: CSB, ports: {Np: X, Nn: GND}
name: CGS, type: Capacitor, value: CGS, ports: {Np: Vb, Nn: X}
]
extrainfo:The circuit is a common-gate amplifier stage with NMOS transistor M1. The input is at Vin and the output is at Vout, connected to node Y. The circuit includes parasitic capacitances CGD, CDB, CGS, and CSB. RD provides the load at the output node Y.

(b)

Figure 11.35 (a) CB and (b) CG stages including transistor capacitances.
by $R_{S} \|\left(1 / g_{m}\right)$, yielding

$$
\begin{equation*}
\left|\omega_{p, X}\right|=\frac{1}{\left(R_{S} \| \frac{1}{g_{m}}\right) C_{X}} \tag{11.96}
\end{equation*}
$$

where $C_{X}=C_{\pi}$ or $C_{G S}+C_{S B}$. Similarly, at $Y$,

$$
\begin{equation*}
\left|\omega_{p, Y}\right|=\frac{1}{R_{L} C_{Y}} \tag{11.97}
\end{equation*}
$$

where $C_{Y}=C_{\mu}+C_{C S}$ or $C_{G D}+C_{D B}$.
It is interesting to note that the "input" pole magnitude is on the order of the $f_{T}$ of the transistor: $C_{X}$ is equal to $C_{\pi}$ or roughly equal to $C_{G S}$ while the resistance seen to ground is less than $1 / g_{m}$. For this reason, the input pole of the $\mathrm{CB} / \mathrm{CG}$ stage rarely creates a speed bottleneck. ${ }^{15}$

Example Compute the poles of the circuit shown in Fig. 11.36(a). Assume $\lambda=0$.
11.19
image_name:Fig. 11.36(a)
description:
[
name: M1, type: NMOS, ports: {S: s1, D: Vout, G: Vb}
name: M2, type: PMOS, ports: {S: VDD, D: Vout, G: Vout}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: s1}
name: CSB1 + CGS1, type: Capacitor, value: CSB1 + CGS1, ports: {Np: X, Nn: GND}
name: CDB1, type: Capacitor, value: CDB1, ports: {Np: Y, Nn: GND}
name: CGD1, type: Capacitor, value: CGD1, ports: {Np: Y, Nn: GND}
name: CGS2, type: Capacitor, value: CGS2, ports: {Np: Y, Nn: GND}
name: CDB2, type: Capacitor, value: CDB2, ports: {Np: Y, Nn: GND}
]
extrainfo:The circuit is a two-stage amplifier with an NMOS (M1) and a PMOS (M2) transistor. M1 is configured with its source at node s1, drain at Vout, and gate at Vb. M2 has its source at VDD, drain at Vout, and gate also at Vout. The resistive element RS connects Vin to s1. Capacitive elements are connected to nodes X and Y, with multiple capacitances connected to ground from node Y.
image_name:Fig. 11.36(b)
description:
[
name: M1, type: NMOS, ports: {S: s1, D: X, G: Vb}
name: M2, type: PMOS, ports: {S: VDD, D: Vout, G: Y}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: s1}
name: CDB1, type: Capacitor, value: CDB1, ports: {Np: Y, Nn: GND}
name: CGD1, type: Capacitor, value: CGD1, ports: {Np: Y, Nn: GND}
name: CGS1, type: Capacitor, value: CGS1, ports: {Np: X, Nn: GND}
name: CDB2, type: Capacitor, value: CDB2, ports: {Np: Vout, Nn: GND}
name: CGS2, type: Capacitor, value: CGS2, ports: {Np: Y, Nn: GND}
name: CSB1, type: Capacitor, value: CSB1, ports: {Np: X, Nn: GND}
name: CSB2, type: Capacitor, value: CSB2, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a common-source amplifier with a PMOS load. The input is at Vin and the output is at Vout. The circuit includes device capacitances for pole calculation.

(a)

Figure 11.36
Solution Noting that $C_{G D 2}$ and $C_{S B 2}$ play no role in the circuit, we add the device capacitances as depicted in Fig. 11.36(b). The input pole is thus given by

$$
\begin{equation*}
\left|\omega_{p, X}\right|=\frac{1}{\left(R_{S} \| \frac{1}{g_{m 1}}\right)\left(C_{S B 1}+C_{G D 1}\right)} \tag{11.98}
\end{equation*}
$$

[^5]Since the small-signal resistance at the output node is equal to $1 / g_{m 2}$, we have

$$
\begin{equation*}
\left|\omega_{p, Y}\right|=\frac{1}{\frac{1}{g_{m 2}}\left(C_{D B 1}+C_{G D 1}+C_{G S 2}+C_{D B 2}\right)} \tag{11.99}
\end{equation*}
$$

Exercise Repeat the above example if $M_{2}$ operates as a current source, i.e., its gate is connected to a constant voltage.

Example The CS stage of Example 11.18 is reconfigured to a common-gate amplifier (with $R_{S}$ tied 11.20 to the source of the transistor). Plot the frequency response of the circuit.

Solution With the values given in Example 11.18 and noting that $C_{S B}=C_{D B},{ }^{16}$ we obtain from Eqs. (11.96) and (11.97),

$$
\begin{align*}
& \left|\omega_{p, \text { in }}\right|=2 \pi \times(5.31 \mathrm{GHz})  \tag{11.100}\\
& \left|\omega_{p, \text { out }}\right|=2 \pi \times(442 \mathrm{MHz}) \tag{11.101}
\end{align*}
$$

With no Miller effect, the input pole has dramatically risen in magnitude. The output pole, however, limits the bandwidth. Also, the low-frequency gain is now equal to $R_{D} /\left(R_{S}+1 / g_{m}\right)=5.7$, more than a factor of two lower than that of the CS stage. Figure 11.37 plots the result. The low-frequency gain is equal to $15 \mathrm{~dB} \approx 5.7$ and the -3 dB bandwidth is around 450 MHz .
image_name:Figure 11.37
description:The graph in Figure 11.37 is a Bode plot illustrating the magnitude of frequency response in decibels (dB) versus frequency in hertz (Hz). The x-axis represents frequency on a logarithmic scale ranging from 10^6 Hz (1 MHz) to 10^10 Hz (10 GHz), while the y-axis shows the magnitude of the frequency response in dB, ranging from -20 dB to 20 dB.

In this graph, the low-frequency gain is approximately 15 dB, which corresponds to a linear gain of about 5.7. This gain remains constant over a wide range of frequencies, indicating a flat response at lower frequencies. As the frequency increases, the magnitude begins to decline, indicating a roll-off in the response. The -3 dB point, which signifies the bandwidth limit, occurs around 450 MHz. This is where the gain drops by 3 dB from its maximum value, marking the cutoff frequency.

The overall trend shows a stable gain at low frequencies with a gradual decline as frequency increases, typical of a low-pass filter response. There are no peaks or oscillations, suggesting a smooth transition without resonance effects. The graph is typical for analyzing the frequency response of electronic amplifiers, particularly in assessing bandwidth limitations and gain stability.

Figure 11.37

Exercise Repeat the above example if the CG amplifier drives a load capacitance of 150 fF .

[^6]
## 11.6 FREQUENCY RESPONSE OF FOLLOWERS

The low-frequency response of followers is similar to that studied in Example 11.11 and that of CE/CS stages. We thus study the high-frequency behavior here.

In Chapters 5 and 7, we noted that emitter and source followers provide a high input impedance and a relatively low output impedance while suffering from a sub-unity (positive) voltage gain. Emitter followers, and occasionally source followers, are utilized as buffers and their frequency characteristics are of interest.

Figure 11.38 illustrates the stages with relevant capacitances. The emitter follower is loaded with $C_{L}$ to create both a more general case and greater similarity between the bipolar and MOS counterparts. We observe that each circuit contains two grounded capacitors and one floating capacitor. While the latter may be decomposed using Miller's approximation, the resulting analysis is beyond the scope of this book. We therefore perform a direct analysis by writing the circuit's equations. Since the bipolar and MOS versions in Fig. 11.38 differ by only $r_{\pi}$, we first analyze the emitter follower and subsequently let $r_{\pi}$ (or $\beta$ ) approach infinity to obtain the transfer function of the source follower.
image_name:(a)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: X, Nn: Y}
name: Cμ, type: Capacitor, value: Cμ, ports: {Np: VCC, Nn: X}
name: Q1, type: NPN, ports: {C: CL, B: X, E: Y}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
]
extrainfo:The circuit is an emitter follower configuration with a grounded capacitor CL at the output and a floating capacitor Cμ between the collector of Q1 and VCC. The input is applied at Vin and the output is taken at Vout. The emitter of the transistor is connected to a node labeled Y, which is also connected to the ground through a current source.

(a)
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: Y, D: X, G: Vin}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: CGS, type: Capacitor, value: CGS, ports: {Np: Vin, Nn: X}
name: CGD, type: Capacitor, value: CGD, ports: {Np: X, Nn: VDD}
name: CDB, type: Capacitor, value: CDB, ports: {Np: VDD, Nn: Y}
name: CSB + CL, type: Capacitor, value: CSB + CL, ports: {Np: Y, Nn: GND}
]
extrainfo:This is a source follower circuit with an NMOS transistor M1. The input voltage is applied at Vin, and the output is taken at Vout. The circuit includes parasitic capacitances CGS, CGD, and CDB. The capacitor CSB + CL is connected between the node Y (emitter) and ground. The voltage source VDD powers the circuit.

(b)

Figure 11.38 (a) Emitter follower and (b) source follower including transistor capacitances.

Consider the small-signal equivalent shown in Fig. 11.39. Recognizing that $V_{X}=$ $V_{\text {out }}+V_{\pi}$ and the current through the parallel combination of $r_{\pi}$ and $C_{\pi}$ is given by $V_{\pi} / r_{\pi}+V_{\pi} C_{\pi} s$, we write a KCL at node $X$ :

$$
\begin{equation*}
\frac{V_{\text {out }}+V_{\pi}-V_{\text {in }}}{R_{S}}+\left(V_{\text {out }}+V_{\pi}\right) C_{\mu} s+\frac{V_{\pi}}{r_{\pi}}+V_{\pi} C_{\pi} s=0 \tag{11.102}
\end{equation*}
$$

and another at the output node:

$$
\begin{equation*}
\frac{V_{\pi}}{r_{\pi}}+V_{\pi} C_{\pi} s+g_{m} V_{\pi}=V_{o u t} C_{L} s \tag{11.103}
\end{equation*}
$$

image_name:Figure 11.39 Small-signal equivalent of emitter follower
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: Cμ, type: Capacitor, value: Cμ, ports: {Np: X, Nn: Vout}
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: X, Nn: Vout}
name: rπ, type: Resistor, value: rπ, ports: {N1: X, N2: Vout}
name: gmVπ, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: Vout}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a small-signal equivalent of an emitter follower. It includes a voltage source, resistors, capacitors, and a voltage-controlled current source. The circuit demonstrates the relationship between input and output voltages with the given parameters.

Figure 11.39 Small-signal equivalent of emitter follower.

The latter gives

$$
\begin{equation*}
V_{\pi}=\frac{V_{\text {out }} C_{L} s}{\frac{1}{r_{\pi}}+g_{m}+C_{\pi} s} \tag{11.104}
\end{equation*}
$$

which, upon substitution in Eq. (11.102) and with the assumption $r_{\pi} \gg g_{m}^{-1}$, leads to

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=\frac{1+\frac{C_{\pi}}{g_{m}} s}{a s^{2}+b s+1} \tag{11.105}
\end{equation*}
$$

where

$$
\begin{align*}
a & =\frac{R_{S}}{g_{m}}\left(C_{\mu} C_{\pi}+C_{\mu} C_{L}+C_{\pi} C_{L}\right)  \tag{11.106}\\
b & =R_{S} C_{\mu}+\frac{C_{\pi}}{g_{m}}+\left(1+\frac{R_{S}}{r_{\pi}}\right) \frac{C_{L}}{g_{m}} \tag{11.107}
\end{align*}
$$

The circuit thus exhibits a zero at

$$
\begin{equation*}
\left|\omega_{z}\right|=\frac{g_{m}}{C_{\pi}} \tag{11.108}
\end{equation*}
$$

which, from Eq. (11.49), is near the $f_{T}$ of the transistor. The poles of the circuit can be computed using the dominant-pole approximation described in Section 11.4.4. In practice, however, the two poles do not fall far from each other, necessitating direct solution of the quadratic denominator.

The above results also apply to the source follower if $r_{\pi} \rightarrow \infty$ and corresponding capacitance substitutions are made ( $C_{S B}$ and $C_{L}$ are in parallel):

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=\frac{1+\frac{C_{G S}}{g_{m}} s}{a s^{2}+b s+1}, \tag{11.109}
\end{equation*}
$$

where

$$
\begin{align*}
a & =\frac{R_{S}}{g_{m}}\left[C_{G D} C_{G S}+C_{G D}\left(C_{S B}+C_{L}\right)+C_{G S}\left(C_{S B}+C_{L}\right)\right]  \tag{11.110}\\
b & =R_{S} C_{G D}+\frac{C_{G D}+C_{S B}+C_{L}}{g_{m}} \tag{11.111}
\end{align*}
$$

Example A source follower is driven by a resistance of $200 \Omega$ and drives a load capacitance of 11.21 100 fF . Using the transistor parameters given in Example 11.18, plot the frequency response of the circuit.

Solution The zero occurs at $g_{m} / C_{G S}=2 \pi \times(4.24 \mathrm{GHz})$. To compute the poles, we obtain $a$ and $b$ from Eqs. (11.110) and (11.111), respectively:

$$
\begin{align*}
& a=2.58 \times 10^{-21} \mathrm{~s}^{-2}  \tag{11.112}\\
& b=5.8 \times 10^{-11} \mathrm{~s} . \tag{11.113}
\end{align*}
$$

The two poles are then equal to

$$
\begin{align*}
& \omega_{p 1}=2 \pi[-1.79 \mathrm{GHz}+j(2.57 \mathrm{GHz})]  \tag{11.114}\\
& \omega_{p 2}=2 \pi[-1.79 \mathrm{GHz}-j(2.57 \mathrm{GHz})] \tag{11.115}
\end{align*}
$$

image_name:Figure 11.40
description:The graph in Figure 11.40 is a Bode plot illustrating the magnitude of the frequency response of a system. The x-axis represents the frequency in hertz (Hz) on a logarithmic scale, ranging from 10^6 Hz to 10^10 Hz. The y-axis shows the magnitude of the frequency response in decibels (dB), ranging from 0 dB to -14 dB.

The plot shows a typical low-pass filter response. At lower frequencies (below 10^9 Hz), the magnitude remains relatively constant and close to 0 dB, indicating that these frequencies pass through the system with minimal attenuation. As the frequency increases beyond approximately 10^9 Hz, the magnitude begins to decrease sharply, indicating the onset of significant attenuation.

The -3 dB point, which marks the cutoff frequency, is approximately at 3.5 GHz (3.5 x 10^9 Hz). Beyond this frequency, the magnitude continues to drop, showcasing the roll-off characteristic of the filter.

The graph is characterized by a smooth curve that transitions from a flat response to a steep decline, typical of a low-pass filter with complex poles, as mentioned in the context. This behavior aligns with the poles calculated in the context, contributing to the observed frequency response.

Figure 11.40
With the values chosen here, the poles are complex. Figure 11.40 plots the frequency response. The -3 dB bandwidth is approximately equal to 3.5 GHz .

Exercise For what value of $g_{m}$ do the two poles become real and equal?

Example Determine the transfer function of the source follower shown in Fig. 11.41(a), where $M_{2}$ 11.22 acts as a current source.
image_name:Figure 11.41(a)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: b1}
name: M1, type: NMOS, ports: {S: Vout, D: VDD, G: b1}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: Vb}
]
extrainfo:The circuit is a source follower configuration with M2 acting as a current source. The input is applied at Vin and the output is taken from Vout. Vb provides the bias voltage for M2.

(a)
image_name:Figure 11.41(b)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: M1, type: NMOS, ports: {S: Y, D: VDD, G: X}
name: M2, type: NMOS, ports: {S: GND, D: Y, G: Vb}
name: CGD1, type: Capacitor, value: CGD1, ports: {Np: d1, Nn: X}
name: CGS1, type: Capacitor, value: CGS1, ports: {Np: Vin, Nn: GND}
name: CDB1, type: Capacitor, value: CDB1, ports: {Np: d1, Nn: GND}
name: CGD2, type: Capacitor, value: CGD2, ports: {Np: Vb, Nn: Y}
name: CGS2, type: Capacitor, value: CGS2, ports: {Np: Vb, Nn: GND}
name: CDB2, type: Capacitor, value: CDB2, ports: {Np: Y, Nn: GND}
name: CSB1, type: Capacitor, value: CSB1, ports: {Np: Y, Nn: GND}
name: CSB2, type: Capacitor, value: CSB2, ports: {Np: GND, Nn: GND}
]
extrainfo:The circuit is a source follower configuration with M2 acting as a current source. The input is applied at Vin and the output is taken from Vout. Vb provides the bias voltage for M2. Capacitors CGD1, CGS1, CDB1, CGD2, CGS2, CDB2, CSB1, and CSB2 are included to model the transistor capacitances.

Figure 11.41

Solution Noting that $C_{G S 2}$ and $C_{S B 2}$ play no role in the circuit, we include the transistor capacitances as illustrated in Fig. 11.41(b). The result resembles that in Fig. 11.38, but with $C_{G D 2}$ and
$C_{D B 2}$ appearing in parallel with $C_{S B 1}$. Thus, Eq. (11.109) can be rewritten as

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}(s)=\frac{1+\frac{C_{G S 1}}{g_{m 1}} s}{a s^{2}+b s+1} \tag{11.116}
\end{equation*}
$$

where

$$
\begin{align*}
a & =\frac{R_{S}}{g_{m 1}}\left[C_{G D 1} C_{G S 1}+\left(C_{G D 1}+C_{G S 1}\right)\left(C_{S B 1}+C_{G D 2}+C_{D B 2}\right)\right]  \tag{11.117}\\
b & =R_{S} C_{G D 1}+\frac{C_{G D 1}+C_{S B 1}+C_{G D 2}+C_{D B 2}}{g_{m 1}} \tag{11.118}
\end{align*}
$$

Exercise Assuming $M_{1}$ and $M_{2}$ are identical and using the transistor parameters given in Example 11.18, calculate the pole frequencies.

### 11.6.1 Input and Output Impedances

In Chapter 5, we observed that the input resistance of the emitter follower is given by $r_{\pi}+(\beta+1) R_{L}$, where $R_{L}$ denotes the load resistance. Also, in Chapter 7 , we noted that the source follower input resistance approaches infinity at low frequencies. We now employ an approximate but intuitive analysis to obtain the input capacitance of followers.

Consider the circuits shown in Fig. 11.42, where $C_{\pi}$ and $C_{G S}$ appear between the input and output and can therefore be decomposed using Miller's theorem. Since the low-frequency gain is equal to

$$
\begin{equation*}
A_{v}=\frac{R_{L}}{R_{L}+\frac{1}{g_{m}}} \tag{11.119}
\end{equation*}
$$

we note that the "input" component of $C_{\pi}$ or $C_{G S}$ is expressed as

$$
\begin{align*}
C_{X} & =\left(1-A_{v}\right) C_{X Y}  \tag{11.120}\\
& =\frac{1}{1+g_{m} R_{L}} C_{X Y} . \tag{11.121}
\end{align*}
$$

Interestingly, the input capacitance of the follower contains only a fraction of $C_{\pi}$ or $C_{G S}$, depending on how large $g_{m} R_{L}$ is. Of course, $C_{\mu}$ or $C_{G D}$ directly adds to this value to yield the total input capacitance.
image_name:Figure 11.43
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: X, E: Y}
name: Cμ, type: Capacitor, value: Cμ, ports: {Np: VCC, Nn: X}
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: X, Nn: Y}
name: RL, type: Resistor, value: RL, ports: {N1: Y, N2: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: Y, Nn: GND}
]
extrainfo:The circuit is a follower configuration with an NPN transistor Q1. It includes parasitic capacitances Cμ and Cπ, and is biased by VCC. The load is connected to the emitter, and the input is at node X.

(a)
image_name:Figure 11.43
description:
[
name: M1, type: NMOS, ports: {S: Y, D: VDD, G: X}
name: C_GS, type: Capacitor, value: C_GS, ports: {Np: X, Nn: Y}
name: C_GD, type: Capacitor, value: C_GD, ports: {Np: X, Nn: VDD}
name: C_DB, type: Capacitor, value: C_DB, ports: {Np: VDD, Nn: GND}
name: C_L, type: Capacitor, value: C_L, ports: {Np: Y, Nn: GND}
name: C_SB, type: Capacitor, value: C_SB, ports: {Np: Y, Nn: GND}
name: R_L, type: Resistor, value: R_L, ports: {N1: Y, N2: GND}
name: V_DD, type: VoltageSource, value: V_DD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit in Figure 11.43 is a source follower configuration using an NMOS transistor M1. It is biased by a voltage source VDD, with parasitic capacitances C_GS, C_GD, C_DB, C_L, and C_SB. The input is at node X, and the output is taken from node Y. The load resistor R_L is connected to the ground.

(b)

Figure 11.42 Input impedance of (a) emitter follower and (b) source follower.

Estimate the input capacitance of the follower shown in Fig. 11.43. Assume $\lambda \neq 0$.
image_name:Figure 11.43
description:
[
name: M1, type: NMOS, ports: {S: s1d2, D: VDD, G: Vin}
name: M2, type: NMOS, ports: {S: GND, D: s1d2, G: Vb}
]
extrainfo:The circuit is a source follower configuration using NMOS transistors M1 and M2. M1's source is connected to the node s1d2, and its gate is connected to the input Vin. M2's drain is connected to the same node s1d2, and its gate is connected to the bias voltage Vb. The circuit is powered by VDD, and the output is taken from node s1d2.

Figure 11.43

Solution From Chapter 7, the low-frequency gain of the circuit can be written as

$$
\begin{equation*}
A_{v}=\frac{r_{O 1} \| r_{O 2}}{r_{O 1} \| r_{O 2}+\frac{1}{g_{m 1}}} \tag{11.122}
\end{equation*}
$$

Also, from Fig. 11.42(b), the capacitance appearing between the input and output is equal to $C_{G S 1}$, thereby providing

$$
\begin{align*}
C_{i n} & =C_{G D 1}+\left(1-A_{v}\right) C_{G S 1}  \tag{11.123}\\
& =C_{G D 1}+\frac{1}{1+g_{m 1}\left(r_{O 1} \| r_{O 2}\right)} C_{G S 1} . \tag{11.124}
\end{align*}
$$

For example, if $g_{m 1}\left(r_{O 1} \| r_{O 2}\right) \approx 10$, then only $9 \%$ of $C_{G S 1}$ appears at the input.
Exercise Repeat the above example if $\lambda=0$.

Let us now turn our attention to the output impedance of followers. Our study of the emitter follower in Chapter 5 revealed that the output resistance is equal to $R_{S} /(\beta+1)+1 / g_{m}$. Similarly, Chapter 7 indicated an output resistance of $1 / g_{m}$ for the source follower. At high frequencies, these circuits display an interesting behavior.

Consider the followers depicted in Fig. 11.44(a), where other capacitances and resistances are neglected for the sake of simplicity. As usual, $R_{S}$ represents the output resistance of a preceding stage or device. We first compute the output impedance of the emitter follower and subsequently let $r_{\pi} \rightarrow \infty$ to determine that of the source follower. From the
image_name:(a)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: b1}
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: b1, Nn: GND}
name: Q1, type: NPN, ports: {C: VCC, B: b1, E: Cl}
name: Cl, type: Capacitor, value: Cl, ports: {Np: Cl, Nn: Zout}
name: M1, type: NMOS, ports: {S: GND, D: Zout, G: b1}
name: CGS, type: Capacitor, value: CGS, ports: {Np: b1, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vx, N2: b1}
name: gmVπ, type: VoltageControlledCurrentSource, ports: {Np: Vx, Nn: GND}
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Vx, Nn: GND}
]
extrainfo:The circuit illustrates the output impedance of emitter and source followers. It includes an NPN transistor and an NMOS transistor, each with associated resistors and capacitors. The circuit models the small-signal behavior of the followers, focusing on the high-frequency output impedance characteristics.
image_name:(b)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: X}
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: X, Nn: Vx}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vx, N2: X}
name: gmVπ, type: VoltageControlledCurrentSource, ports: {Np: Vx, Nn: GND}
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Vx, Nn: GND}
]
extrainfo:The circuit represents a small-signal model for analyzing the output impedance of emitter and source followers.

Figure 11.44 (a) Output impedance of emitter and source followers, (b) small-signal model.
equivalent circuit in Fig. 11.44(b), we have

$$
\begin{equation*}
\left(I_{X}+g_{m} V_{\pi}\right)\left(r_{\pi} \| \frac{1}{C_{\pi} s}\right)=-V_{\pi} \tag{11.125}
\end{equation*}
$$

and also

$$
\begin{equation*}
\left(I_{X}+g_{m} V_{\pi}\right) R_{S}-V_{\pi}=V_{X} . \tag{11.126}
\end{equation*}
$$

Finding $V_{\pi}$ from Eq. (11.125)

$$
\begin{equation*}
V_{\pi}=-I_{X} \frac{r_{\pi}}{r_{\pi} C_{\pi} s+\beta+1} \tag{11.127}
\end{equation*}
$$

and substituting in Eq. (11.126), we obtain

$$
\begin{equation*}
\frac{V_{X}}{I_{X}}=\frac{R_{S} r_{\pi} C_{\pi} s+r_{\pi}+R_{S}}{r_{\pi} C_{\pi} s+\beta+1} . \tag{11.128}
\end{equation*}
$$

As expected, at low frequencies $V_{X} / I_{X}=\left(r_{\pi}+R_{S}\right) /(\beta+1) \approx 1 / g_{m}+R_{S} /(\beta+1)$. On the other hand, at very high frequencies, $V_{X} / I_{X}=R_{S}$, a meaningful result considering that $C_{\pi}$ becomes a short circuit.

The two extreme values calculated above for the output impedance of the emitter follower can be used to develop greater insight. Plotted in Fig. 11.45, the magnitude of this impedance falls with $\omega$ if $R_{S}<1 / g_{m}+R_{S} /(\beta+1)$ or rises with $\omega$ if $R_{S}>1 / g_{m}+R_{S} /(\beta+1)$. In analogy with the impedance of capacitors and inductors, we say $Z_{\text {out }}$ exhibits a capacitive behavior in the former case and an inductive behavior in the latter.
image_name:(a)
description:The graph labeled (a) is a plot of the magnitude of the output impedance \(|Z_{out}|\) of an emitter follower as a function of frequency \(\omega\). It is a Bode plot showing the behavior of the output impedance with respect to frequency when the source resistance \(R_S\) is small.

**Axes Labels and Units:**
- The horizontal axis represents frequency \(\omega\), likely in radians per second, although specific units are not labeled.
- The vertical axis represents the magnitude of the output impedance \(|Z_{out}|\).

**Overall Behavior and Trends:**
- At low frequencies, \(|Z_{out}|\) starts at a value approximately equal to \(\frac{R_S}{\beta+1} + \frac{1}{g_m}\).
- As frequency increases, the impedance decreases, indicating a capacitive behavior.
- The graph shows a downward slope, suggesting that the impedance becomes smaller at higher frequencies.

**Key Features and Technical Details:**
- The initial high value of impedance at low frequency is marked by the expression \(\frac{R_S}{\beta+1} + \frac{1}{g_m}\).
- There is a dotted line indicating the value of \(R_S\), which the impedance approaches as frequency increases.
- The graph suggests that at very high frequencies, the impedance approaches a lower limit, which is approximately equal to \(R_S\).

**Annotations and Specific Data Points:**
- The graph is annotated with two specific impedance values: \(\frac{R_S}{\beta+1} + \frac{1}{g_m}\) at low frequency and \(R_S\) as the asymptotic value at high frequency.
image_name:(b)
description:The graph labeled as (b) in Figure 11.45 illustrates the behavior of the output impedance \( |Z_{out}| \) of an emitter follower as a function of frequency \( \omega \) when the source resistance \( R_S \) is large. This is a Bode plot, which typically represents the magnitude of impedance on the vertical axis and frequency on the horizontal axis.

1. **Axes Labels and Units:**
- The vertical axis represents the magnitude of the output impedance \( |Z_{out}| \).
- The horizontal axis represents frequency \( \omega \), likely in radians per second.
- The scale used for frequency is typically logarithmic in Bode plots, although it is not explicitly marked here.

2. **Overall Behavior and Trends:**
- At low frequencies, the magnitude of the output impedance starts at a value of \( \frac{R_S}{\beta + 1} + \frac{1}{g_m} \), indicating a relatively low impedance.
- As frequency increases, the impedance rises, exhibiting an inductive behavior. This is shown by the upward trend in the curve.
- The curve approaches an asymptotic value at higher frequencies, leveling off at approximately \( R_S \), indicating that the impedance becomes stable.

3. **Key Features and Technical Details:**
- The graph shows a transition from a lower impedance to a higher impedance as frequency increases, consistent with inductive behavior.
- There are no specific peaks or valleys; the trend is a smooth increase.
- The dotted line at \( R_S \) represents the asymptotic value of the output impedance at high frequencies.

4. **Annotations and Specific Data Points:**
- The graph is annotated to show the initial value \( \frac{R_S}{\beta + 1} + \frac{1}{g_m} \) and the asymptotic value \( R_S \).
- These annotations help to understand the impedance behavior over the frequency range.

This graph effectively demonstrates the inductive behavior of the emitter follower's output impedance at high frequencies when \( R_S \) is large, which is more commonly encountered in practical scenarios.

Figure 11.45 Output impedance of emitter follower as a function of frequency for (a) small $R_{S}$ and (b) large $R_{S}$.

Which case is more likely to occur in practice? Since a follower serves to reduce the driving impedance, it is reasonable to assume that the follower low-frequency output impedance is lower than $R_{S} .{ }^{17}$ Thus, the inductive behavior is more commonly encountered. (It is even possible that the inductive output impedance leads to oscillation if the follower sees a certain amount of load capacitance.)

The above development can be extended to source followers by factoring $r_{\pi}$ from the numerator and denominator of Eq. (11.128) and letting $r_{\pi}$ and $\beta$ approach infinity:

$$
\begin{equation*}
\frac{V_{X}}{I_{X}}=\frac{R_{S} C_{G S} s+1}{C_{G S} s+g_{m}} \tag{11.129}
\end{equation*}
$$

where $(\beta+1) / r_{\pi}$ is replaced with $g_{m}$, and $C_{\pi}$ with $C_{G D}$. The plots of Fig. 11.45 are redrawn for the source follower in Fig. 11.46, displaying a similar behavior.

[^7]image_name:(a)
description:The graph labeled \( (a) \) is a plot of the magnitude of the output impedance \( |Z_{out}| \) of a source follower as a function of frequency \( \omega \). The vertical axis represents \( |Z_{out}| \) and the horizontal axis represents frequency \( \omega \). The graph is likely plotted on a logarithmic scale for frequency, which is common in such analyses.

1. **Type of Graph and Function:**
- This is a Bode plot showing the magnitude of the output impedance versus frequency.

2. **Axes Labels and Units:**
- Vertical Axis: \( |Z_{out}| \) (output impedance magnitude)
- Horizontal Axis: \( \omega \) (frequency), likely in radians per second or hertz

3. **Overall Behavior and Trends:**
- At low frequencies, the output impedance \( |Z_{out}| \) starts at a value of \( \frac{1}{g_m} \), where \( g_m \) is the transconductance.
- As frequency increases, the impedance initially remains constant and then begins to decrease.
- Eventually, it approaches a lower asymptotic value of \( R_S \), the source resistance.

4. **Key Features and Technical Details:**
- The graph shows a transition from \( \frac{1}{g_m} \) to \( R_S \) as frequency increases.
- The behavior suggests an inductive nature at the output at high frequencies, which is typical for source followers.

5. **Annotations and Specific Data Points:**
- The starting point at low frequency is marked as \( \frac{1}{g_m} \).
- The asymptotic low value at high frequency is marked as \( R_S \).
- The transition between these two points is smooth and gradual, indicating a frequency-dependent change in impedance characteristics.
image_name:(b)
description:The graph labeled "(b)" is a plot of the magnitude of the output impedance \(|Z_{out}|\) of a source follower as a function of frequency \(\omega\). The plot is a Bode plot, which typically represents frequency response.

**Axes Labels and Units:**
- The horizontal axis represents frequency \(\omega\), but no specific units are provided; it's implied to be in a logarithmic scale typical of Bode plots.
- The vertical axis represents the magnitude of the output impedance \(|Z_{out}|\), with significant markers at \(\frac{1}{g_m}\) and \(R_S\).

**Overall Behavior and Trends:**
- The graph starts at a low impedance level of \(\frac{1}{g_m}\) at low frequencies.
- As frequency increases, the impedance begins to rise.
- The curve approaches a higher impedance level, \(R_S\), as frequency continues to increase, indicating an inductive behavior at higher frequencies.

**Key Features and Technical Details:**
- The plot shows a smooth transition from a low impedance value \(\frac{1}{g_m}\) to a higher value \(R_S\), suggesting frequency-dependent behavior typical of active inductors.
- The dotted line at \(R_S\) indicates the asymptotic maximum value of the output impedance at high frequencies.

**Annotations and Specific Data Points:**
- The transition region between \(\frac{1}{g_m}\) and \(R_S\) is not marked with specific frequency values, but it represents the range where the source follower's output impedance changes significantly with frequency.

Figure 11.46 Output impedance of source follower as a function of frequency for (a) small $R_{S}$ and (b) large $R_{S}$.

The inductive impedance seen at the output of followers proves useful in the realization of "active inductors."

Example Figure 11.47 depicts a two-stage amplifier consisting of a CS circuit and a source follower.

11.24

Assuming $\lambda \neq 0$ for $M_{1}$ and $M_{2}$ but $\lambda=0$ for $M_{3}$, and neglecting all capacitances except $C_{G S 3}$, compute the output impedance of the amplifier.
image_name:Figure 11.47
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1d2g3, G: Vin}
name: M2, type: PMOS, ports: {S: VDD, D: d1d2g3, G: Vb}
name: M3, type: NMOS, ports: {S: d1d2g3, D: Vout, G: Vout}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a two-stage amplifier with a CS stage followed by a source follower. The output impedance is influenced by the parallel combination of the output resistances of M1 and M2.

(a)
image_name:(a)
description:
[
name: r01||r02, type: Resistor, ports: {N1: GND, N2: b3}
name: M3, type: NMOS, ports: {S: b3, D: Zout, G: b3}
]
extrainfo:The circuit is a part of a two-stage amplifier, focusing on the output stage. The NMOS transistor M3 is configured as a source follower, with its gate and source connected to node b3. The resistor r01||r02 is connected between ground and node b3. The output is taken from the drain of M3, labeled as Zout.

(b)

Figure 11.47

Solution The source impedance seen by the follower is equal to the output resistance of the CS stage, which is equal to $r_{O 1} \| r_{O 2}$. Assuming $R_{S}=r_{O 1} \| r_{O 2}$ in Eq. (11.129), we have

$$
\begin{equation*}
\frac{V_{X}}{I_{X}}=\frac{\left(r_{O 1} \| r_{O 2}\right) C_{G S 3} s+1}{C_{G S 3} s+g_{m 3}} . \tag{11.130}
\end{equation*}
$$

Exercise Determine $Z_{\text {out }}$ in the above example if $\lambda \neq 0$ for $M_{1}-M_{3}$.

## 11.7 FREQUENCY RESPONSE OF CASCODE STAGE

Our analysis of the CE/CS stage in Section 11.4 and the CB/CG stage in Section 11.5 reveals that the former provides a relatively high input resistance but suffers from Miller effect whereas the latter exhibits a relatively low input resistance but is free from Miller effect. We wish to combine the desirable properties of the two topologies, obtaining a circuit with a relatively high input resistance and no or little Miller effect. Indeed, this thought process led to the invention of the cascode topology in the 1940s.

Consider the cascodes shown in Fig. 11.48. As mentioned in Chapter 9, this structure can be viewed as a CE/CS transistor, $Q_{1}$ or $M_{1}$, followed by a CB/CG device, $Q_{2}$ or $M_{2}$. As
image_name:(a)
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: Q1, type: NPN, ports: {C: Y, B: X, E: GND}
name: Q2, type: NPN, ports: {C: Vout, B: Vb1, E: Y}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: VCC}
name: Cμ1, type: Capacitor, value: Cμ1, ports: {Np: X, Nn: Y}
]
extrainfo:The circuit is a bipolar cascode amplifier with transistors Q1 and Q2. It has a high output impedance, high voltage gain, and reduced Miller effect. The input is connected through RS to the base of Q1, and the output is taken from the collector of Q2.

(a)
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Y, G: X}
name: M2, type: NMOS, ports: {S: Y, D: Vout, G: Vb}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: RL, type: Resistor, value: RL, ports: {N1: VDD, N2: Vout}
name: CGD1, type: Capacitor, value: CGD1, ports: {Np: X, Nn: Y}
]
extrainfo:The circuit is a MOS cascode amplifier with transistors M1 and M2. It features high output impedance and high voltage gain. The input is connected through RS to the gate of M1, and the output is taken from the drain of M2. The cascode structure reduces the Miller effect and enhances stability.

(b)

Figure 11.48 (a) Bipolar and (b) MOS cascode stages.

Did you know?

In addition to reducing Miller multiplication of $C_{\mu}$ or $C_{G D}$, the cascode structure provides a higher output impedance, a higher voltage gain, and greater stability. By stability, we mean the tendency of the amplifier not to oscillate. Since $C_{\mu}$ or $C_{G D}$ returns a fraction of the output signal to the input, it can cause instability in highfrequency amplifiers. For this reason, we commonly use the cascode topology at the front end of RF receivers, often with inductive degeneration as shown below.
image_name:Use of cascode in a cellphone low-noise amplifier
description:
[
name: M1, type: NMOS, ports: {S: s1, D: d1s2, G: g1}
name: M2, type: NMOS, ports: {S: d1s2, D: Vout, G: Vb}
name: L1, type: Inductor, value: L1, ports: {N1: s1, N2: GND}
name: L2, type: Inductor, value: L2, ports: {N1: VDD, N2: Vout}
]
extrainfo:The circuit is a cascode low-noise amplifier used in RF applications. It features a two-stage NMOS configuration with inductive degeneration for improved stability and gain.

Use of cascode in a cellphone low-noise amplifier.
such, the circuit still exhibits a relatively high (for $Q_{1}$ ) or infinite (for $M_{1}$ ) input resistance while providing a voltage gain equal to $g_{m 1} R_{L} \cdot{ }^{18}$ But, how about the Miller multiplication of $C_{\mu 1}$ or $C_{G D 1}$ ? We must first compute the voltage gain from node $X$ to node $Y$. Assuming $r_{O}=\infty$ for all transistors, we recognize that the impedance seen at $Y$ is equal to $1 / g_{m 2}$, yielding a smallsignal gain of

$$
\begin{align*}
A_{v, X Y} & =\frac{v_{Y}}{v_{X}}  \tag{11.131}\\
& =-\frac{g_{m 1}}{g_{m 2}} . \tag{11.132}
\end{align*}
$$

In the bipolar cascode, $g_{m 1}=g_{m 2}$ (why?), resulting in a gain of -1 . In the MOS counterpart, $M_{1}$ and $M_{2}$ need not be identical, but $g_{m 1}$ and $g_{m 2}$ are comparable because of their relatively weak dependence upon $W / L$. We therefore say the gain from $X$ to $Y$ remains near -1 in most practical cases, concluding that the Miller effect of $C_{X Y}=C_{\mu 1}$ or $C_{G D 1}$ is given by

$$
\begin{align*}
C_{X} & =\left(1-A_{v, X Y}\right) C_{X Y}  \tag{11.133}\\
& \approx 2 C_{X Y} . \tag{11.134}
\end{align*}
$$

This result stands in contrast to that expressed by Eq. (11.56), suggesting that the cascode transistor breaks the trade-off between the gain and the input capacitance due to Miller effect.

Let us continue our analysis and estimate the poles of the cascode topology with the aid of Miller's approximation. Illustrated in Fig. 11.49 is the bipolar cascode along with the transistor capacitances. Note that the effect of $C_{\mu 1}$ at $Y$ is also equal to $\left(1-A_{v, X Y}^{-1}\right) C_{\mu 1}=2 C_{\mu 1}$.

[^8]image_name:Figure 11.49 Bipolar cascode including transistor capacitances
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: Q1, type: NPN, ports: {C: Y, B: X, E: GND}
name: Q2, type: NPN, ports: {C: Vout, B: Vb1, E: Y}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: VCC}
name: CCS1, type: Capacitor, value: CCS1, ports: {Np: Y, Nn: GND}
name: CCS2, type: Capacitor, value: CCS2, ports: {Np: Vout, Nn: GND}
name: Cπ1, type: Capacitor, value: Cπ1, ports: {Np: X, Nn: GND}
name: Cπ2, type: Capacitor, value: Cπ2, ports: {Np: Y, Nn: GND}
name: Cμ1, type: Capacitor, value: Cμ1, ports: {Np: X, Nn: GND}
name: Cμ2, type: Capacitor, value: Cμ2, ports: {Np: Vout, Nn: GND}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: Vb1, type: VoltageSource, value: Vb1, ports: {Np: Vb1, Nn: GND}
]
extrainfo:The circuit is a bipolar cascode amplifier with two NPN transistors, Q1 and Q2. It includes various capacitors to manage frequency response and stability, as well as resistors for biasing and load. The input is applied at Vin, and the output is taken from Vout. The circuit is powered by a VCC supply.

Figure 11.49 Bipolar cascode including transistor capacitances.
Associating one pole with each node gives

$$
\begin{align*}
\left|\omega_{p, X}\right| & =\frac{1}{\left(R_{S} \| r_{\pi 1}\right)\left(C_{\pi 1}+2 C_{\mu 1}\right)}  \tag{11.135}\\
\left|\omega_{p, Y}\right| & =\frac{1}{\frac{1}{g_{m 2}}\left(C_{C S 1}+C_{\pi 2}+2 C_{\mu 1}\right)}  \tag{11.136}\\
\left|\omega_{p, \text { out }}\right| & =\frac{1}{R_{L}\left(C_{C S 2}+C_{\mu 2}\right)} \tag{11.137}
\end{align*}
$$

It is interesting to note that the pole at node $Y$ falls near the $f_{T}$ of $Q_{2}$ if $C_{\pi 2} \gg C_{C S 1}+2 C_{\mu 1}$. Even for comparable values of $C_{\pi 2}$ and $C_{C S 1}+2 C_{\mu 1}$, we can say this pole is on the order of $f_{T} / 2$, a frequency typically much higher than the signal bandwidth. For this reason, the pole at node $Y$ often has negligible effect on the frequency response of the cascode stage.

The MOS cascode is shown in Fig. 11.50 along with its capacitances after the use of Miller's approximation. Since the gain from $X$ to $Y$ in this case may not be equal to -1 , we use the actual value, $-g_{m 1} / g_{m 2}$, to arrive at a more general solution. Associating one pole with each node, we have

$$
\begin{align*}
\left|\omega_{p, X}\right| & =\frac{1}{R_{S}\left[C_{G S 1}+\left(1+\frac{g_{m 1}}{g_{m 2}}\right) C_{G D 1}\right]}  \tag{11.138}\\
\left|\omega_{p, Y}\right| & =\frac{1}{\frac{1}{g_{m 2}}\left[C_{D B 1}+C_{G S 2}+\left(1+\frac{g_{m 2}}{g_{m 1}}\right) C_{G D 1}+C_{S B 2}\right]}  \tag{11.139}\\
\left|\omega_{p, \text { out }}\right| & =\frac{1}{R_{L}\left(C_{D B 2}+C_{G D 2}\right)} \tag{11.140}
\end{align*}
$$

image_name:Figure 11.50 MOS cascode including transistor capacitances
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Y, G: X}
name: M2, type: NMOS, ports: {S: Y, D: Vout, G: Vb}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: VDD}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: CGD2, type: Capacitor, value: CGD2, ports: {Np: Vout, Nn: GND}
name: CDB2, type: Capacitor, value: CDB2, ports: {Np: Vout, Nn: GND}
name: CGS1, type: Capacitor, value: CGS1, ports: {Np: X, Nn: GND}
name: CGD1, type: Capacitor, value: CGD1, ports: {Np: X, Nn: GND}
name: CGS2, type: Capacitor, value: CGS2, ports: {Np: Y, Nn: GND}
name: CDB1, type: Capacitor, value: CDB1, ports: {Np: Y, Nn: GND}
name: CSB2, type: Capacitor, value: CSB2, ports: {Np: Y, Nn: GND}
]
extrainfo:The circuit is a MOS cascode amplifier with two NMOS transistors (M1 and M2). It includes various capacitances that contribute to the frequency response, with poles at nodes X, Y, and Vout. The cascode topology is used to improve bandwidth and gain.

Figure 11.50 MOS cascode including transistor capacitances.

We note that $\omega_{p, Y}$ is still in the range of $f_{T} / 2$ if $C_{G S 2}$ and $C_{D B 1}+\left(1+g_{m 2} / g_{m 1}\right) C_{G D 1}$ are comparable.

Example The CS stage studied in Example 11.18 is converted to a cascode topology. Assuming 11.25 the two transistors are identical, estimate the poles, plot the frequency response, and compare the results with those of Example 11.18. Assume $C_{D B}=C_{S B}$.

Solution Using the values given in Example 11.18, we write from Eqs. (11.138), (11.139), and (11.140):

$$
\begin{align*}
\left|\omega_{p, X}\right| & =2 \pi \times(1.95 \mathrm{GHz})  \tag{11.141}\\
\left|\omega_{p, Y}\right| & =2 \pi \times(1.73 \mathrm{GHz})  \tag{11.142}\\
\left|\omega_{p, \text { out }}\right| & =2 \pi \times(442 \mathrm{MHz}) \tag{11.143}
\end{align*}
$$

Note that the pole at node $Y$ is significantly lower than $f_{T} / 2$ in this particular example. Compared with the Miller approximation results obtained in Example 11.18, the input pole has risen considerably. Compared with the exact values derived in that example, the cascode bandwidth ( 442 MHz ) is nearly twice as large. Figure 11.51 plots the frequency response of the cascode stage.
image_name:Figure 11.51
description:The graph in Figure 11.51 is a Bode plot showing the magnitude of the frequency response of a cascode stage. The x-axis represents frequency in hertz (Hz) on a logarithmic scale, ranging from 10^6 Hz (1 MHz) to 10^10 Hz (10 GHz). The y-axis represents the magnitude of the frequency response in decibels (dB), ranging from -30 dB to 30 dB.

**Overall Behavior and Trends:**
- The graph shows a flat response at approximately 20 dB for frequencies below 10^8 Hz (100 MHz), indicating a stable gain in this frequency range.
- After this point, the magnitude begins to decrease, indicating a roll-off in gain as frequency increases.
- The roll-off becomes more pronounced as the frequency approaches 10^9 Hz (1 GHz), reflecting the bandwidth limitations of the cascode stage.

**Key Features and Technical Details:**
- The bandwidth of the cascode stage is indicated to be around 442 MHz, which is consistent with the context provided.
- The -3 dB point, which is a common marker for bandwidth, would be slightly below 10^8 Hz, where the magnitude starts to drop noticeably from the flat region.
- The roll-off appears to follow a typical single-pole response, with a consistent slope after the initial drop.

**Annotations and Specific Data Points:**
- There are no specific annotations or markers on the graph, but the general shape and trends are consistent with typical cascode amplifier behavior, emphasizing the increased bandwidth achieved in this design.

Figure 11.51
Exercise Repeat the above example if the width of $M_{2}$ and hence all of its capacitances are doubled. Assume $g_{m 2}=(100 \Omega)^{-1}$.

In the cascode shown in Fig. 11.52, transistor $M_{3}$ serves as a constant current source, 11.26 allowing $M_{1}$ to carry a larger current than $M_{2}$. Estimate the poles of the circuit, assuming $\lambda=0$.

Solution Transistor $M_{3}$ contributes $C_{G D 3}$ and $C_{D B 3}$ to node $Y$, thus lowering the corresponding pole magnitude. The circuit contains the following poles:

$$
\begin{align*}
\left|\omega_{p, X}\right| & =\frac{1}{R_{S}\left[C_{G S 1}+\left(1+\frac{g_{m 1}}{g_{m 2}}\right) C_{G D 1}\right]}  \tag{11.144}\\
\left|\omega_{p, Y}\right| & =\frac{1}{\frac{1}{g_{m 2}}\left[C_{D B 1}+C_{G S 2}+\left(1+\frac{g_{m 2}}{g_{m 1}}\right) C_{G D 1}+C_{G D 3}+C_{D B 3}+C_{S B 2}\right]}  \tag{11.145}\\
\left|\omega_{p, \text { out }}\right| & =\frac{1}{R_{L}\left(C_{D B 2}+C_{G D 2}\right)} . \tag{11.146}
\end{align*}
$$

Note that $\omega_{p, X}$ also reduces in magnitude because the addition of $M_{3}$ lowers $I_{D 2}$ and hence $g_{m 2}$.
image_name:Figure 11.52
description:
[
name: M3, type: PMOS, ports: {S: VDD, D: Y, G: Vb2}
name: M2, type: NMOS, ports: {S: Y, D: Vout, G: Vb1}
name: M1, type: NMOS, ports: {S: GND, D: Y, G: X}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: RL, type: Resistor, value: RL, ports: {N1: VDD, N2: Vout}
]
extrainfo:The circuit is a cascode amplifier with a high output impedance, serving as a good current source or high-gain amplifier. It reduces the Miller effect for better high-frequency performance.

Figure 11.52
Exercise Calculate the pole frequencies in the above example using the transistor parameters given in Example 11.18 for $M_{1}-M_{3}$.

From our studies of the cascode topology in Chapter 9 and in this chapter, we identify two important, distinct attributes of this circuit: (1) the ability to provide a high output impedance and hence serve as a good current source and/or high-gain amplifier; (2) the reduction of the Miller effect and hence better high-frequency performance. Both of these properties are exploited extensively.

### 11.7.1 Input and Output Impedances

The foregoing analysis of the cascode stage readily provides estimates for the I/O impedances. From Fig. 11.49, the input impedance of the bipolar cascode is given by

$$
\begin{equation*}
Z_{i n}=r_{\pi 1} \| \frac{1}{\left(C_{\pi 1}+2 C_{\mu 1}\right) s}, \tag{11.147}
\end{equation*}
$$

where $Z_{\text {in }}$ does not include $R_{S}$. The output impedance is equal to

$$
\begin{equation*}
Z_{\text {out }}=R_{L} \| \frac{1}{\left(C_{\mu 2}+C_{C S 2}\right) s}, \tag{11.148}
\end{equation*}
$$

where the Early effect is neglected. Similarly, for the MOS stage shown in Fig. 11.50, we have

$$
\begin{align*}
Z_{\text {in }} & =\frac{1}{\left[C_{G S 1}+\left(1+\frac{g_{m 1}}{g_{m 2}}\right) C_{G D 1}\right] s}  \tag{11.149}\\
Z_{\text {out }} & =\frac{1}{R_{L}\left(C_{G D 2}+C_{D B 2}\right)} \tag{11.150}
\end{align*}
$$

where it is assumed $\lambda=0$.
If $R_{L}$ is large, the output resistance of the transistors must be taken into account. This calculation is beyond the scope of this book.

## 11.8 FREQUENCY RESPONSE OF DIFFERENTIAL PAIRS

The half-circuit concept introduced in Chapter 10 can also be applied to the high-frequency model of differential pairs, thus reducing the circuit to those studied above.

Figure 11.53(a) depicts two bipolar and MOS differential pairs along with their capacitances. For small differential inputs, the half circuits can be constructed as shown in
image_name:Figure 11.53(a)
description:
[
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: c1}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: c2}
name: RS, type: Resistor, value: RS, ports: {N1: Vin1, N2: b1}
name: RS, type: Resistor, value: RS, ports: {N1: Vin2, N2: b2}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: d1}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: d2}
name: CCS1, type: Capacitor, value: CCS1, ports: {Np: c1, Nn: GND}
name: CCS2, type: Capacitor, value: CCS2, ports: {Np: c2, Nn: GND}
name: Cμ1, type: Capacitor, value: Cμ1, ports: {Np: c1, Nn: b1}
name: Cμ2, type: Capacitor, value: Cμ2, ports: {Np: c2, Nn: b2}
name: Cπ1, type: Capacitor, value: Cπ1, ports: {Np: b2, Nn: GND}
name: Cπ2, type: Capacitor, value: Cπ2, ports: {Np: b1, Nn: GND}
name: CGS1, type: Capacitor, value: CGS1, ports: {Np: b1, Nn: GND}
name: CGS2, type: Capacitor, value: CGS2, ports: {Np: b2, Nn: GND}
name: CDB1, type: Capacitor, value: CDB1, ports: {Np: d1, Nn: GND}
name: CDB2, type: Capacitor, value: CDB2, ports: {Np: d2, Nn: GND}
name: CGD1, type: Capacitor, value: CGD1, ports: {Np: d1, Nn: b1}
name: CGD2, type: Capacitor, value: CGD2, ports: {Np: d2, Nn: b2}
name: CSB1, type: Capacitor, value: CSB1, ports: {Np: GND, Nn: GND}
name: CSB2, type: Capacitor, value: CSB2, ports: {Np: GND, Nn: GND}
name: Q1, type: NPN, ports: {C: c1, B: b1, E: ie1}
name: Q2, type: NPN, ports: {C: c2, B: b2, E: ie2}
name: M1, type: NMOS, ports: {S: ie1, D: d1, G: b1}
name: M2, type: NMOS, ports: {S: ie2, D: d2, G: b2}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: ie1, Nn: GND}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: ie2, Nn: GND}
]
extrainfo:The circuit diagram in Figure 11.53(a) shows two differential pairs, one using bipolar junction transistors (BJTs) Q1 and Q2, and the other using MOSFETs M1 and M2. Both pairs include various capacitances for high-frequency modeling. The circuit is powered by VCC for the BJTs and VDD for the MOSFETs, with current sources IEE and ISS providing bias currents. The resistors RC and RD are used as load resistors for the BJTs and MOSFETs respectively.
image_name:Figure 11.53(b)
description:
[
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Vout1}
name: RS, type: Resistor, value: RS, ports: {N1: Vin1, N2: b1}
name: CCS1, type: Capacitor, value: CCS1, ports: {Np: Vout1, Nn: GND}
name: Cμ1, type: Capacitor, value: Cμ1, ports: {Np: Vout1, Nn: b1}
name: Cπ2, type: Capacitor, value: Cπ2, ports: {Np: b1, Nn: GND}
name: Q1, type: NPN, ports: {C: Vout1, B: b1, E: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: d1}
name: RS, type: Resistor, value: RS, ports: {N1: Vin1, N2: g1}
name: CGS1, type: Capacitor, value: CGS1, ports: {Np: g1, Nn: GND}
name: CGD1, type: Capacitor, value: CGD1, ports: {Np: d1, Nn: g1}
name: CDB1, type: Capacitor, value: CDB1, ports: {Np: d1, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: d1, G: g1}
]
extrainfo:This is a half-circuit representation of a differential pair. It includes an NPN transistor (Q1) and an NMOS transistor (M1), showing their connections to resistors, capacitors, and input/output nodes. The NPN transistor is connected to VCC and the NMOS transistor is connected to VDD. The circuit models the frequency response of the differential pair using various capacitances.

Figure 11.53 (a) Bipolar and MOS differential pairs including transistor capacitances, (b) half circuits.

Fig. 11.53(b). The transfer function is therefore given by Eq. (11.70):

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {Thev }}}(s)=\frac{\left(C_{X Y} s-g_{m}\right) R_{L}}{a s^{2}+b s+1} \tag{11.151}
\end{equation*}
$$

where the same notation is used for various parameters. Similarly, the input and output impedances (from each node to ground) are equal to those in Eqs. (11.91) and (11.92), respectively.

Example A differential pair employs cascode devices to lower the Miller effect [Fig. 11.54(a)]. 11.27 Estimate the poles of the circuit.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: s1s2, D: d1s3, G: Vin1}
name: M2, type: NMOS, ports: {S: s1s2, D: d2s4, G: Vin2}
name: M3, type: NMOS, ports: {S: d1s3, D: Vout1, G: Vb}
name: M4, type: NMOS, ports: {S: d2s4, D: Vout2, G: Vb}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: RS, type: Resistor, value: RS, ports: {N1: Vin1, N2: g1}
name: RS, type: Resistor, value: RS, ports: {N1: Vin2, N2: g2}
name: CGD3 + CDB3, type: Capacitor, value: CGD3 + CDB3, ports: {Np: Vout, Nn: GND}
name: CGS3 + CGD1, type: Capacitor, value: CGS3 + CGD1, ports: {Np: X, Nn: GND}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: s1s2, Nn: GND}
]
extrainfo:The circuit is a differential pair with cascode devices to reduce the Miller effect. It consists of two NMOS transistors (M1 and M2) forming a differential pair, with M3 and M4 acting as cascode devices. The circuit is biased with a current source (ISS) and has resistors (RD, RS) and capacitors for stabilization and frequency response.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: s1s2, D: d1s3, G: Vin1}
name: M2, type: NMOS, ports: {S: s1s2, D: d2s4, G: Vin2}
name: M3, type: NMOS, ports: {S: d1s3, D: Vout1, G: Vb}
name: M4, type: NMOS, ports: {S: d2s4, D: Vout2, G: Vb}
name: RD, type: Resistor, value: RD, ports: {N1: Vout1, N2: VDD}
name: RS, type: Resistor, value: RS, ports: {N1: Vin1, N2: g1}
name: RS, type: Resistor, value: RS, ports: {N1: Vin2, N2: g2}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: s1s2, Nn: GND}
name: CGS1, type: Capacitor, value: CGS1, ports: {Np: g1, Nn: GND}
name: CGD1, type: Capacitor, value: CGD1, ports: {Np: d1s3, Nn: GND}
name: CGD3, type: Capacitor, value: CGD3, ports: {Np: Vout, Nn: GND}
name: CDB3, type: Capacitor, value: CDB3, ports: {Np: Vout, Nn: GND}
name: CDB1, type: Capacitor, value: CDB1, ports: {Np: d1s3, Nn: GND}
name: CSB3, type: Capacitor, value: CSB3, ports: {Np: s1s2, Nn: GND}
]
extrainfo:The circuit is a differential pair with cascode devices to reduce the Miller effect. It includes NMOS transistors M1 to M4, resistors RD and RS, and various capacitors. The circuit is designed to estimate poles and uses a current source ISS.

(a)
(b)

Figure 11.54
Solution Employing the half circuit shown in Fig. 11.54(b), we utilize the results obtained in Section 11.7:

$$
\begin{align*}
\left|\omega_{p, X}\right| & =\frac{1}{R_{S}\left[C_{G S 1}+\left(1+\frac{g_{m 1}}{g_{m 3}}\right) C_{G D 1}\right]}  \tag{11.152}\\
\left|\omega_{p, Y}\right| & =\frac{1}{\frac{1}{g_{m 3}}\left[C_{D B 1}+C_{G S 3}+\left(1+\frac{g_{m 3}}{g_{m 1}}\right) C_{G D 1}+C_{S B 3}\right]}  \tag{11.153}\\
\left|\omega_{p, \text { out }}\right| & =\frac{1}{R_{L}\left(C_{D B 3}+C_{G D 3}\right)} \tag{11.154}
\end{align*}
$$

Exercise Calculate the pole frequencies using the transistor parameters given in Example 11.18. Assume the width and hence the capacitances of $M_{3}$ are twice those of $M_{1}$. Also, $g_{m 3}=\sqrt{2} g_{m 1}$.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: Vout1, G: VCM}
name: M2, type: NMOS, ports: {S: P, D: Vout2, G: VCM}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout1}
name: RD+ΔRD, type: Resistor, value: RD+ΔRD, ports: {N1: VDD, N2: Vout2}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: VCM, type: VoltageSource, value: VCM, ports: {Np: VCM, Nn: GND}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: P, Nn: GND}
name: RSS, type: Resistor, value: RSS, ports: {N1: P, N2: GND}
name: CSS, type: Capacitor, value: CSS, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential pair with NMOS transistors M1 and M2. It has a common-mode input voltage VCM and outputs Vout1 and Vout2. The resistors RD and RD+ΔRD are connected to the power supply VDD. The tail current source IEE provides biasing, and RSS along with CSS forms a feedback network for stability.

(a)
image_name:(b) CM frequency response
description:The graph is a Bode plot illustrating the common-mode (CM) frequency response of a differential pair circuit. The x-axis represents angular frequency (ω) on a logarithmic scale, while the y-axis represents the CM gain.

**Axes Labels and Units:**
- **X-axis (ω):** Frequency, presented in a logarithmic scale.
- **Y-axis (CM Gain):** Gain, with specific gain levels marked.

**Overall Behavior and Trends:**
- The graph starts at a lower gain level, specifically at \( \frac{\Delta R_D}{2R_{SS} + \frac{1}{g_m}} \).
- As frequency increases, the gain remains constant initially, then begins to rise at a certain point.
- The gain eventually levels off at a higher gain value of \( g_m \Delta R_D \).

**Key Features and Technical Details:**
- There are two significant frequency markers on the x-axis:
- \( \frac{1}{R_{SS}C_{SS}} \): Marks the frequency where the gain starts to increase.
- \( \frac{2g_m}{C_{SS}} \): Marks the frequency where the gain levels off.
- The plot shows an increase in gain between these two frequencies, indicating the effect of parasitic capacitance at higher frequencies.

**Annotations and Specific Data Points:**
- The graph is annotated with dotted lines at the key frequency points and gain levels to highlight the transitions in gain behavior.
- The initial gain level and the final gain level are explicitly marked, providing clear reference points for the CM response behavior.

(b)

Figure 11.55 (a) Differential pair with parasitic capacitance at the tail node, (b) CM frequency response.

### 11.8.1 Common-Mode Frequency Response*

The CM response studied in Chapter 10 included no transistor capacitances. At high frequencies, capacitances may raise the CM gain (and lower the differential gain), thus degrading the common-mode rejection ratio.

Let us consider the MOS differential pair shown in Fig. 11.55(a), where a finite capacitance appears between node $P$ and ground. Since $C_{S S}$ shunts $R_{S S}$, we expect the total impedance between $P$ and ground to fall at high frequencies, leading to a higher CM gain. In fact, we can simply replace $R_{S S}$ with $R_{S S} \|\left[1 /\left(C_{S S} s\right)\right]$ in Eq. (10.186):

$$
\begin{align*}
\left|\frac{\Delta V_{\text {out }}}{\Delta V_{C M}}\right| & =\frac{\Delta R_{D}}{\frac{1}{g_{m}}+2\left(R_{S S} \| \frac{1}{C_{S S} s}\right)}  \tag{11.155}\\
& =\frac{g_{m} \Delta R_{D}\left(R_{S S} C_{S S}+1\right)}{R_{S S} C_{S S} s+2 g_{m} R_{S S}+1} \tag{11.156}
\end{align*}
$$

Since $R_{S S}$ is typically quite large, $2 g_{m} R_{S S} \gg 1$, yielding the following zero and pole frequencies:

$$
\begin{align*}
& \left|\omega_{z}\right|=\frac{1}{R_{S S} C_{S S}}  \tag{11.157}\\
& \left|\omega_{p}\right|=\frac{2 g_{m}}{C_{S S}} \tag{11.158}
\end{align*}
$$

and the Bode approximation plotted in Fig. 11.55(b). The CM gain indeed rises dramatically at high frequencies-by a factor of $2 g_{m} R_{S S}$ (why?).

Figure 11.56 depicts the transistor capacitances that constitute $C_{S S}$. For example, $M_{3}$ is typically a wide device so that it can operate with a small $V_{D S}$, thereby adding large capacitances to node $P$.

[^9]image_name:Figure 11.56
description:
[
name: M1, type: NMOS, ports: {S: P, D: LOAD, G: LOAD}
name: M2, type: NMOS, ports: {S: P, D: LOAD, G: LOAD}
name: M3, type: NMOS, ports: {S: GND, D: P, G: Vb}
name: CSB1, type: Capacitor, value: CSB1, ports: {Np: GND, Nn: P}
name: CSB2, type: Capacitor, value: CSB2, ports: {Np: GND, Nn: P}
name: CSB3, type: Capacitor, value: CSB3, ports: {Np: P, Nn: GND}
name: CGD3, type: Capacitor, value: CGD3, ports: {Np: P, Nn: Vb}
]
extrainfo:The circuit in Figure 11.56 illustrates the transistor capacitance contributions to the tail node. The NMOS transistors M1 and M2 are connected in a configuration where their sources are tied to node P, and their drains and gates are connected to a load. M3 is used to connect node P to ground, controlled by a bias voltage Vb. Capacitors CSB1, CSB2, and CSB3 are connected to node P and ground, contributing to the tail node capacitance along with CGD3, which is connected between P and Vb.

Figure 11.56 Transistor capacitance contributions to the tail node.

## 11.9 ADDITIONAL EXAMPLES

Example The amplifier shown in Fig. 11.57(a) incorporates capacitive coupling both at the input
11.28 and between the two stages. Determine the low-frequency cut-off of the circuit. Assume $I_{S}=5 \times 10^{-16} \mathrm{~A}, \beta=100$, and $V_{A}=\infty$.
image_name:Figure 11.57 (a)
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: C1, type: Capacitor, value: 200 nF, ports: {Np: Vin, Nn: X}
name: RB1, type: Resistor, value: 100 kΩ, ports: {N1: VCC, N2: X}
name: RC, type: Resistor, value: 1 kΩ, ports: {N1: VCC, N2: C1}
name: Q1, type: NPN, ports: {C: C1, B: X, E: GND}
name: C2, type: Capacitor, value: 200 nF, ports: {Np: C1, Nn: Y}
name: RB2, type: Resistor, value: 50 kΩ, ports: {N1: VCC, N2: Y}
name: Q2, type: NPN, ports: {C: VCC, B: Y, E: Vout}
name: RE, type: Resistor, value: 1 kΩ, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a two-stage amplifier with capacitive coupling at the input and between the two stages. The amplifier uses NPN transistors Q1 and Q2 with biasing resistors RB1 and RB2. The capacitors C1 and C2 provide AC coupling, and RE provides emitter degeneration for Q2.

(a)
image_name:(a)
description:
[
name: I1, type: CurrentSource, value: I1, ports: {Np: GND, Nn: P}
name: RC, type: Resistor, value: RC, ports: {N1: P, N2: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: P, Nn: VY}
name: Rin2, type: Resistor, value: Rin2, ports: {N1: VY, N2: GND}
]
extrainfo:The circuit is part of a two-stage amplifier with a current source I1, resistor RC, and capacitor C2 providing AC coupling. Rin2 is connected to the output node VY, and the circuit is grounded at multiple points.

(b)
image_name:(b)
description:
[
name: VThev, type: VoltageSource, value: VThev, ports: {Np: VThev, Nn: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VThev, N2: X}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: VY}
name: Rin2, type: Resistor, value: Rin2, ports: {N1: VY, N2: GND}
]
extrainfo:The circuit is a part of a two-stage amplifier. It includes a voltage source VThev, a resistor RC, and a capacitor C2 for AC coupling. The output node is VY, and the circuit is grounded at multiple points.

(c)

Figure 11.57

Solution We must first compute the operating point and small-signal parameters of the circuit. From Chapter 5, we begin with an estimate of for $V_{B E 1}$, e.g., 800 mV , and express the base current of $Q_{1}$ as $\left(V_{C C}-V_{B E 1}\right) / R_{B 1}$ and hence

$$
\begin{align*}
I_{C 1} & =\beta \frac{V_{C C}-V_{B E 1}}{R_{B 1}}  \tag{11.159}\\
& =1.7 \mathrm{~mA} \tag{11.160}
\end{align*}
$$

It follows that $V_{B E 1}=V_{T} \ln \left(I_{C 1} / I_{S 1}\right)=748 \mathrm{mV}$ and $I_{C 1}=1.75 \mathrm{~mA}$. Thus, $g_{m 1}=$ $(14.9 \Omega)^{-1}$ and $r_{\pi 1}=1.49 \mathrm{k} \Omega$. For $Q_{2}$, we have

$$
\begin{equation*}
V_{C C}=I_{B 2} R_{B 2}+V_{B E 2}+R_{E} I_{C 2} \tag{11.161}
\end{equation*}
$$

and therefore

$$
\begin{align*}
I_{C 2} & =\frac{V_{C C}-V_{B E 2}}{R_{B 2} / \beta+R_{E}}  \tag{11.162}\\
& =1.13 \mathrm{~mA} \tag{11.163}
\end{align*}
$$

where it is assumed $V_{B E 2} \approx 800 \mathrm{mV}$. Iteration yields $I_{C 2}=1.17 \mathrm{~mA}$. Thus, $g_{m 2}=$ $(22.2 \Omega)^{-1}$ and $r_{\pi 2}=2.22 \mathrm{k} \Omega$.

Let us now consider the first stage by itself. Capacitor $C_{1}$ forms a high-pass filter along with the input resistance of the circuit, $R_{i n 1}$, thus attenuating low frequencies. Since $R_{i n 1}=r_{\pi 2} \| R_{B 1}$, the low-frequency cut-off of this stage is equal to

$$
\begin{align*}
\omega_{L 1} & =\frac{1}{\left(r_{\pi 1} \| R_{B 1}\right) C_{1}}  \tag{11.164}\\
& =2 \pi \times(542 \mathrm{~Hz}) \tag{11.165}
\end{align*}
$$

The second coupling capacitor also creates a high-pass response along with the input resistance of the second stage, $R_{i n 2}=R_{B 2} \|\left[r_{\pi 2}+(\beta+1) R_{E}\right]$. To compute the cut-off frequency, we construct the simplified interface shown in Fig. 11.57(b) and determine $V_{Y} / I_{1}$. In this case, it is simpler to replace $I_{1}$ and $R_{C}$ with a Thevenin equivalent, Fig. 11.57(c), where $V_{\text {Thev }}=-I_{1} R_{C}$. We now have
obtaining a pole at

$$
\begin{equation*}
\frac{V_{Y}}{V_{T h e v}}(s)=\frac{R_{i n 2}}{R_{C}+\frac{1}{C_{2} s}+R_{i n 2}} \tag{11.166}
\end{equation*}
$$

obtaining a pole at

$$
\begin{align*}
\omega_{L 2} & =\frac{1}{\left(R_{C}+R_{i n 2}\right) C_{2}}  \tag{11.167}\\
& =\pi \times(22.9 \mathrm{~Hz}) \tag{11.168}
\end{align*}
$$

Since $\omega_{L 2} \ll \omega_{L 1}$, we conclude that $\omega_{L 1}$ "dominates" the low-frequency response, i.e., the gain drops by 3 dB at $\omega_{L 1}$.

Exercise Repeat the above example if $R_{E}=500 \Omega$.

Example 11.29

The circuit of Fig. 11.58(a) is an example of amplifiers realized in integrated circuits. It consists of a degenerated stage and a self-biased stage, with moderate values for
image_name:(a)
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: Rs, type: Resistor, value: 200Ω, ports: {N1: Vin, N2: g1}
name: M1, type: NMOS, ports: {S: GND, D: d1, G: g1}
name: RS1, type: Resistor, value: 200Ω, ports: {N1: s1, N2: GND}
name: RD1, type: Resistor, value: 1kΩ, ports: {N1: d1, N2: VDD}
name: RD2, type: Resistor, value: 1kΩ, ports: {N1: VDD, N2: Vout}
name: RF, type: Resistor, value: 10kΩ, ports: {N1: X, N2: Vout}
name: C1, type: Capacitor, value: 50pF, ports: {Np: s1, Nn: GND}
name: C2, type: Capacitor, value: 10pF, ports: {Np: d1, Nn: X}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: X}
name: CGS1, type: Capacitor, value: CGS1, ports: {Np: g1, Nn: GND}
name: CGS2, type: Capacitor, value: CGS2, ports: {Np: X, Nn: GND}
name: CGD1, type: Capacitor, value: CGD1, ports: {Np: g1, Nn: X}
name: CGD2, type: Capacitor, value: CGD2, ports: {Np: X, Nn: Vout}
name: CDB1, type: Capacitor, value: CDB1, ports: {Np: d1, Nn: GND}
name: CDB2, type: Capacitor, value: CDB2, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a two-stage amplifier with feedback, consisting of two NMOS transistors M1 and M2. The first stage is a common-source amplifier with a degenerated resistor RS1 and a bypass capacitor C1. The second stage is also a common-source amplifier with feedback resistor RF. The circuit includes parasitic capacitances CGS, CGD, and CDB for both transistors.
image_name:(b)
description:
[
name: RS, type: Resistor, value: 200Ω, ports: {N1: Vin, N2: g1}
name: RD1, type: Resistor, value: 1kΩ, ports: {N1: VDD, N2: d1}
name: RD2, type: Resistor, value: 1kΩ, ports: {N1: VDD, N2: Vout}
name: RF, type: Resistor, value: 10kΩ, ports: {N1: X, N2: Vout}
name: M1, type: NMOS, ports: {S: s1, D: d1, G: g1}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: X}
name: C1, type: Capacitor, value: 50pF, ports: {Np: s1, Nn: GND}
name: C2, type: Capacitor, value: 10pF, ports: {Np: d1, Nn: X}
name: CGS1, type: Capacitor, ports: {Np: g1, Nn: GND}
name: CGD1, type: Capacitor, ports: {Np: d1, Nn: X}
name: CDB1, type: Capacitor, ports: {Np: d1, Nn: GND}
name: CGS2, type: Capacitor, ports: {Np: X, Nn: GND}
name: CGD2, type: Capacitor, ports: {Np: X, Nn: Vout}
name: CDB2, type: Capacitor, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a two-stage amplifier with NMOS transistors M1 and M2. The first stage is a common-source amplifier with degeneration, and the second stage is a common-source amplifier with feedback. Capacitors C1 and C2 are used for frequency compensation. The resistors RD1 and RD2 are the load resistors for the NMOS transistors. Capacitors CGS1, CGD1, CDB1, CGS2, CGD2, and CDB2 are parasitic capacitances that affect the frequency response.

(c)
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: vin}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: X}
name: RS, type: Resistor, value: 200 Ω, ports: {N1: vin, N2: G1}
name: RD1, type: Resistor, value: 1 kΩ, ports: {N1: X, N2: VDD}
name: RD2, type: Resistor, value: 1 kΩ, ports: {N1: Vout, N2: VDD}
name: RF, type: Resistor, value: 10 kΩ, ports: {N1: X, N2: Vout}
name: Rin2, type: Resistor, value: Rin2, ports: {N1: X, N2: GND}
name: CGD1, type: Capacitor, value: CGD1, ports: {Np: X, Nn: G1}
name: CGS1, type: Capacitor, value: CGS1, ports: {Np: G1, Nn: GND}
name: CDB1 + CGS2 + (1-Av2)CGD2, type: Capacitor, value: CDB1 + CGS2 + (1-Av2)CGD2, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a two-stage amplifier with NMOS transistors M1 and M2. The first stage is a common-source amplifier with degeneration, and the second stage is a common-source amplifier with feedback. Capacitors C1 and C2 are used for frequency compensation. The resistors RD1 and RD2 are the load resistors for the NMOS transistors. Capacitors CGS1, CGD1, CDB1, CGS2, and CGD2 are parasitic capacitances that affect the frequency response.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: VX, G: Vin}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: VX}
name: RS, type: Resistor, value: 200Ω, ports: {N1: Vin, N2: G1}
name: RD1, type: Resistor, value: 1kΩ, ports: {N1: VDD, N2: VX}
name: RD2, type: Resistor, value: 1kΩ, ports: {N1: VDD, N2: Vout}
name: RF, type: Resistor, value: 10kΩ, ports: {N1: Vout, N2: VX}
name: Rin2, type: Resistor, value: Rin2, ports: {N1: VX, N2: GND}
name: CGD1, type: Capacitor, value: CGD1, ports: {Np: VX, Nn: G1}
name: CGS1, type: Capacitor, value: CGS1, ports: {Np: G1, Nn: GND}
name: CDB1, type: Capacitor, value: CDB1, ports: {Np: VX, Nn: GND}
name: CGS2, type: Capacitor, value: CGS2, ports: {Np: Vout, Nn: GND}
name: CGD2, type: Capacitor, value: CGD2, ports: {Np: VX, Nn: Vout}
]
extrainfo:The circuit is a two-stage amplifier with NMOS transistors M1 and M2. The first stage is a common-source amplifier with degeneration, and the second stage is a common-source amplifier with feedback. Capacitors C1 and C2 are used for frequency compensation. The resistors RD1 and RD2 are the load resistors for the NMOS transistors. Capacitors CGS1, CGD1, CDB1, CGS2, CGD2, and CDB2 are parasitic capacitances that affect the frequency response.

(d)

Figure 11.58
$C_{1}$ and $C_{2}$. Assuming $M_{1}$ and $M_{2}$ are identical and have the same parameters as those given in Example 11.18, plot the frequency response of the amplifier.

Solution
Low-Frequency Behavior We begin with the low-frequency region and first consider the role of $C_{1}$. From Eq. (11.55) and Fig. 11.28(c), we note that $C_{1}$ contributes a lowfrequency cut-off at

$$
\begin{align*}
\omega_{L 1} & =\frac{g_{m 1} R_{S 1}+1}{R_{S 1} C_{1}}  \tag{11.169}\\
& =2 \pi \times(37.1 \mathrm{MHz}) \tag{11.170}
\end{align*}
$$

A second low-frequency cut-off is contributed by $C_{2}$ and the input resistance of the second stage, $R_{i n 2}$. This resistance can be calculated with the aid of Miller's theorem:

$$
\begin{equation*}
R_{i n 2}=\frac{R_{F}}{1-A_{v 2}} \tag{11.171}
\end{equation*}
$$

where $A_{v 2}$ denotes the voltage gain from $X$ to the output. Since $R_{F} \gg R_{D 2}$, we have $A_{v 2} \approx-g_{m 2} R_{D 2}=-6.67,{ }^{19}$ obtaining $R_{i n 2}=1.30 \mathrm{k} \Omega$. Using an analysis similar to that in the previous example, the reader can show that

$$
\begin{align*}
\omega_{L 2} & =\frac{1}{\left(R_{D 1}+R_{\text {in } 2}\right) C_{2}}  \tag{11.172}\\
& =2 \pi \times(6.92 \mathrm{MHz}) \tag{11.173}
\end{align*}
$$

Since $\omega_{L 1}$ remains well above $\omega_{L 2}$, the cut-off is dominated by the former.

Midband Behavior In the next step, we compute the midband gain. At midband frequencies, $C_{1}$ and $C_{2}$ act as a short circuit and the transistor capacitances play a negligible role, allowing the circuit to be reduced to that in Fig. 11.58(b). We note that $v_{\text {out }} / v_{\text {in }}=\left(v_{X} / v_{\text {in }}\right)\left(v_{\text {out }} / v_{X}\right)$ and recognize that the drain of $M_{1}$ sees two resistances to ac ground: $R_{D 1}$ and $R_{\text {in } 2}$. That is,

$$
\begin{align*}
\frac{v_{X}}{v_{i n}} & =-g_{m 1}\left(R_{D 1} \| R_{i n 2}\right)  \tag{11.174}\\
& =-3.77 \tag{11.175}
\end{align*}
$$

The voltage gain from node $X$ to the output is approximately equal to $-g_{m 2} R_{D 2}$ because $R_{F} \gg R_{D 2}{ }^{20}$ The overall midband gain is therefore roughly equal to 25.1 .

High-Frequency Behavior To study the response of the amplifier at high frequencies, we insert the transistor capacitances, noting that $C_{S B 1}$ and $C_{S B 2}$ play no role because the source terminals of $M_{1}$ and $M_{2}$ are at ac ground. We thus arrive at the simplified topology shown in Fig. 11.58(c), where the overall transfer function is given by $V_{\text {out }} / V_{\text {in }}=\left(V_{X} / V_{\text {in }}\right)\left(V_{\text {out }} / V_{X}\right)$.

[^10]How do we compute $V_{X} / V_{\text {in }}$ in the presence of the loading of the second stage? The two capacitances $C_{D B 1}$ and $C_{G S 2}$ are in parallel, but how about the effect of $R_{F}$ and $C_{G D 2}$ ? We apply Miller's approximation to both components so as to convert them to grounded elements. The Miller effect of $R_{F}$ was calculated above to be equivalent to $R_{\text {in } 2}=1.3 \mathrm{k} \Omega$. The Miller multiplication of $C_{G D 2}$ is given by $\left(1-A_{v 2}\right) C_{G D 2}=614 \mathrm{fF}$. The first stage can now be drawn as illustrated in Fig. 11.58(d), lending itself to the CS analysis performed in Section 11.4. The zero is given by $g_{m 1} / C_{G D 1}=2 \pi \times(13.3 \mathrm{GHz})$. The two poles can be calculated from Eqs. (11.70), (11.71), and (11.72):

$$
\begin{align*}
& \left|\omega_{p 1}\right|=2 \pi \times(242 \mathrm{MHz})  \tag{11.176}\\
& \left|\omega_{p 2}\right|=2 \pi \times(2.74 \mathrm{GHz}) \tag{11.177}
\end{align*}
$$

The second stage contributes a pole at its output node. The Miller effect of $C_{G D 2}$ at the output is expressed as $\left(1-A_{v 2}^{-1}\right) C_{G D 2} \approx 1.15 C_{G D 2}=92 \mathrm{fF}$. Adding $C_{D B 2}$ to this value yields the output pole as

$$
\begin{align*}
\left|\omega_{p 3}\right| & =\frac{1}{R_{L 2}\left(1.15 C_{G D 2}+C_{D B 2}\right)}  \tag{11.178}\\
& =2 \pi \times(0.829 \mathrm{GHz}) \tag{11.179}
\end{align*}
$$

We observe that $\omega_{p 1}$ dominates the high-frequency response. Figure 11.59 plots the overall response. The midband gain is about $26 \mathrm{~dB} \approx 20$, around $20 \%$ lower than the calculated result. This is primarily due to the use of Miller approximation for $R_{F}$. Also, the "useful" bandwidth can be defined from the lower -3 dB cut-off ( $\approx 40 \mathrm{MHz}$ ) to the upper -3 dB cut-off $(\approx 300 \mathrm{MHz})$ and is almost one decade wide. The gain falls to unity at about 2.3 GHz .
image_name:Figure 11.59
description:The graph in Figure 11.59 is a Bode plot illustrating the magnitude of the frequency response of a system. The x-axis represents frequency in hertz (Hz) on a logarithmic scale ranging from $10^6$ to $10^{10}$ Hz. The y-axis shows the magnitude of the frequency response in decibels (dB), ranging from -30 dB to 30 dB.

The overall behavior of the graph shows a typical bandpass response. The gain increases from a low frequency, reaching a peak at around 26 dB in the mid-frequency range, which is approximately between $10^7$ and $10^8$ Hz. This peak represents the midband gain of the system. Following the peak, the gain decreases sharply, crossing the 0 dB line and continuing to fall as frequency increases, indicating the roll-off at high frequencies.

Key features include:
- The midband gain is about 26 dB, which is slightly lower than the calculated result due to the Miller approximation for $R_F$.
- The useful bandwidth is defined from the lower -3 dB cut-off at approximately 40 MHz ($4 \times 10^7$ Hz) to the upper -3 dB cut-off at approximately 300 MHz ($3 \times 10^8$ Hz), spanning almost one decade.
- The gain falls to unity (0 dB) at around 2.3 GHz ($2.3 \times 10^9$ Hz), indicating the frequency beyond which the system no longer amplifies the signal.

The graph effectively demonstrates how the gain of the system varies with frequency, highlighting the limitations imposed by high-frequency roll-off due to capacitances in the circuit.

Figure 11.59

## 11.10 CHAPTER SUMMARY

- The speed of circuits is limited by various capacitances that the transistors and other components contribute to each node.
- The speed can be studied in the time domain (e.g., by applying a step) or in the frequency domain (e.g., by applying a sinusoid). The frequency response of a circuit corresponds to the latter test.
- As the frequency of operation increases, capacitances exhibit a lower impedance, reducing the gain. The gain thus rolls off at high signal frequencies.
- To obtain the frequency response, we must derive the transfer function of the circuit. The magnitude of the transfer function indicates how the gain varies with frequency.
- Bode's rules approximate the frequency response if the poles and zeros are known.
- A capacitance tied between the input and output of an inverting amplifier appears at the input with a factor equal to one minus the gain of the amplifier. This is called the Miller effect.
- In many circuits, it is possible to associate a pole with each node, i.e., calculate the pole frequency as the inverse of the product of the capacitance and resistance seen between the node and ac ground.
- Miller's theorem allows a floating impedance to be decomposed into to grounded impedances.
- Owing to coupling or degeneration capacitors, the frequency response may also exhibit roll-off as the frequency falls to very low values.
- Bipolar and MOS transistors contain capacitances between their terminals and from some terminals to ac ground. When solving a circuit, these capacitances must be identified and the resulting circuit simplified.
- The CE and CS stages exhibit a second-order transfer function and hence two poles. Miller's approximation indicates an input pole that embodies Miller multiplication of the base-collector or gate-drain capacitance.
- If the two poles of a circuit are far from each other, the "dominant-pole approximation" can be used to find a simple expression for each pole frequency.
- The CB and CG stages do not suffer from the Miller effect and achieve a higher speed than CE/CS stages, but their lower input impedance limits their applicability.
- Emitter and source followers provide a wide bandwidth. Their output impedance, however, can be inductive, causing instability in some cases.
- To benefit from the higher input impedance of CE/CS stages but reduce the Miller effect, a cascode stage can be used.
- The differential frequency response of differential pairs is similar to that of CE/CS stages.
