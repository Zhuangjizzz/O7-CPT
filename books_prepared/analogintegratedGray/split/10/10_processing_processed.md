# 10. Nonlinear Analog Circuits

## 10.1 Introduction

Chapters 1 through 9 dealt almost entirely with analog circuits whose primary function is linear amplification of signals. Although some of the circuits discussed (such as Class AB output stages) were actually nonlinear in their operation, the operations performed on the signal passing through the amplifier were well approximated by linear relations.

Nonlinear operations on continuous-valued analog signals are often required in instrumentation, communication, and control-system design. These operations include modulation, demodulation, frequency translation, multiplication, and division. In this chapter, we analyze the most commonly used techniques for performing these operations within a monolithic integrated circuit. We first discuss the use of the bipolar transistor to synthesize nonlinear analog circuits and analyze the Gilbert multiplier cell, which is the basis for a wide variety of such circuits. Next we consider the application of this building block as a small-signal analog multiplier, as a modulator, as a phase comparator, and as a large-signal, four-quadrant multiplier.

Following the multiplier discussion, we introduce a highly useful circuit technique for performing demodulation of FM and AM signals and, at the same time, performing bandpass filtering. This circuit, the phase-locked-loop (PLL), is particularly well-suited to monolithic construction. After exploring the basic concepts involved, we analyze the behavior of the PLL in the locked condition, and then consider the capture transient. Finally, some methods of realizing arbitrary nonlinear transfer functions using bipolar transistors are considered.

## 10.2 Analog Multipliers Employing the Bipolar Transistor

In analog-signal processing the need often arises for a circuit that takes two analog inputs and produces an output proportional to their product. Such circuits are termed analog multipliers. In the following sections we examine several analog multipliers that depend on the exponential transfer function of bipolar transistors.

### 10.2.1 The Emitter-Coupled Pair as a Simple Multiplier

The emitter-coupled pair, shown in Fig. 10.1, was shown in Chapter 3 to produce output currents that are related to the differential input voltage by

$$
\begin{align*}
I_{c 1} & =\frac{I_{E E}}{1+\exp \left(-\frac{V_{i d}}{V_{T}}\right)}  \tag{10.1}\\
I_{c 2} & =\frac{I_{E E}}{1+\exp \left(\frac{V_{i d}}{V_{T}}\right)} \tag{10.2}
\end{align*}
$$

image_name:Figure 10.1 Emitter-coupled pair
description:
[
name: Q1, type: NPN, ports: {C: LOAD1, B: Vip, E: e1e2}
name: Q2, type: NPN, ports: {C: LOAD2, B: Vin, E: e1e2}
name: I_EE, type: CurrentSource, value: I_EE, ports: {Np: e1e2, Nn: GND}
]
extrainfo:The circuit is an emitter-coupled pair used as a simple multiplier. It consists of two NPN transistors (Q1 and Q2) with their emitters connected together and to a current source I_EE. The differential input voltage (Vid) is applied between the bases of Q1 and Q2, and the output currents (Ic1 and Ic2) are taken from the collectors connected to LOAD1 and LOAD2 respectively.
Figure 10.1 Emitter-coupled pair.
where base current has been neglected. Equations 10.1 and 10.2 can be combined to give the difference between the two output currents:

$$
\begin{equation*}
\Delta I_{c}=I_{c 1}-I_{c 2}=I_{E E} \tanh \left(\frac{V_{i d}}{2 V_{T}}\right) \tag{10.3}
\end{equation*}
$$

This relationship is plotted in Fig. 10.2 and shows that the emitter-coupled pair by itself can be used as a primitive multiplier. We first assume that the differential input voltage $V_{i d}$ is much less than $V_{T}$. If this is true, we can utilize the approximation

$$
\begin{equation*}
\tanh \frac{V_{i d}}{2 V_{T}} \approx \frac{V_{i d}}{2 V_{T}} \quad \frac{V_{i d}}{2 V_{T}} \ll 1 \tag{10.4}
\end{equation*}
$$

And (10.3) becomes

$$
\begin{equation*}
\Delta I_{c} \approx I_{E E}\left(\frac{V_{i d}}{2 V_{T}}\right) \tag{10.5}
\end{equation*}
$$

The current $I_{E E}$ is actually the bias current for the emitter-coupled pair. With the addition of more circuitry, we can make $I_{E E}$ proportional to a second input signal $V_{i 2}$, as shown in
image_name:Figure 10.2
description:The graph in Figure 10.2 is a plot of the DC transfer characteristic of an emitter-coupled pair. It is a sigmoidal curve representing the relationship between the differential input voltage \( V_{id} \) on the horizontal axis and the change in collector current \( \Delta I_c \) on the vertical axis.

1. **Type of Graph and Function:**
- This is a DC transfer characteristic graph, commonly used in analog electronics to show how an output current changes with an input voltage.

2. **Axes Labels and Units:**
- The horizontal axis represents the differential input voltage \( V_{id} \), and the vertical axis represents the change in collector current \( \Delta I_c \).
- There are no specific units marked on the graph, but typically, \( V_{id} \) would be in volts and \( \Delta I_c \) in amperes or milliamperes.

3. **Overall Behavior and Trends:**
- The graph shows a sigmoidal or S-shaped curve.
- As \( V_{id} \) increases from a negative value, \( \Delta I_c \) starts from \(-I_{EE}\), increases through the origin, and approaches \( I_{EE} \) as \( V_{id} \) becomes positive.
- The curve is symmetric around the origin.

4. **Key Features and Technical Details:**
- The curve passes through the origin (0,0), which is an inflection point where the slope is steepest.
- The curve flattens out as \( V_{id} \) approaches \( \pm V_T \), with \( \Delta I_c \) approaching \( \pm I_{EE} \).
- The region between \( -V_T \) and \( +V_T \) is where the curve is most linear, indicating the range of input voltages for which the output current changes most predictably.

5. **Annotations and Specific Data Points:**
- The graph includes dashed lines at \( \Delta I_c = I_{EE} \) and \( \Delta I_c = -I_{EE} \), marking the asymptotic limits of the curve.
- The points \( -V_T \) and \( +V_T \) on the \( V_{id} \) axis are labeled, indicating the threshold voltages where the curve starts to saturate.
Figure 10.2 The dc transfer characteristic of the emitter-coupled pair.

### 10.2.3 The Gilbert Cell as an Analog Multiplier

As mentioned earlier, the hyperbolic tangent function may be represented by the infinite series:

$$
\begin{equation*}
\tanh x=x-\frac{x^{3}}{3} \cdots \tag{10.20}
\end{equation*}
$$

image_name:Figure 10.5 Gilbert multiplier with emitter degeneration applied to improve input voltage range on V2 input.
description:
[
name: Q1, type: NPN, ports: {C: d1e4, B: Vip2, E: e1}
name: Q2, type: NPN, ports: {C: e5e6d2, B: Vin2, E: e2}
name: Q3, type: NPN, ports: {C: d3d5, B: Vip1, E: d1e4}
name: Q4, type: NPN, ports: {C: d4d6, B: Vin1, E: d1e4}
name: Q5, type: NPN, ports: {C: d3d5, B: Vin1, E: e5e6d2}
name: Q6, type: NPN, ports: {C: d4d6, B: Vip1, E: e5e6d2}
name: R, type: Resistor, value: R, ports: {N1: e1, N2: X1}
name: R, type: Resistor, value: R, ports: {N1: e2, N2: X1}
name: I_EE, type: CurrentSource, value: I_EE, ports: {Np: X1, Nn: GND}
]
extrainfo:The circuit is a Gilbert cell multiplier with emitter degeneration to improve the input voltage range on V2 input. It uses six NPN transistors and two resistors to achieve the multiplication of two input signals, V1 and V2. The differential output current I_out is given by I_out = I_c3-5 - I_c4-6.
Figure 10.5 Gilbert multiplier with emitter degeneration applied to improve input voltage range on $V_{2}$ input.

Assuming that $x$ is much less than one, the hyperbolic tangent can then be approximated by

$$
\begin{equation*}
\tanh x \approx x \tag{10.21}
\end{equation*}
$$

Applying this relation to (10.19), we have

$$
\begin{equation*}
\Delta I \approx I_{E E}\left(\frac{V_{1}}{2 V_{T}}\right)\left(\frac{V_{2}}{2 V_{T}}\right) \quad V_{1}, V_{2} \ll V_{T} \tag{10.22}
\end{equation*}
$$

Thus for small-amplitude signals, the circuit performs an analog multiplication. Unfortunately, the amplitudes of the input signals are often much larger than $V_{T}$, but larger signals can be accommodated in this mode in a number of ways. In the event that only one of the signals is large compared to $V_{T}$, emitter degeneration can be utilized in the lower emitter-coupled pair, increasing the linear input range for $V_{2}$ as shown in Fig. 10.5. Unfortunately, this cannot be done with the cross-coupled pairs $Q_{3}-Q_{6}$ because the degeneration resistors destroy the required nonlinear relation between $I_{c}$ and $V_{b e}$ in those devices.

An alternate approach is to introduce a nonlinearity that predistorts the input signals to compensate for the hyperbolic tangent transfer characteristic of the basic cell. The required nonlinearity is an inverse hyperbolic tangent characteristic, and a hypothetical example of such a system is shown in Fig. 10.6. Fortunately, this particular nonlinearity is straightforward to generate.

Referring to Fig. 10.7, we assume for the time being that the circuitry within the box develops a differential output current that is linearly related to the input voltage $V_{1}$. Thus

$$
\begin{align*}
& I_{1}=I_{o 1}+K_{1} V_{1}  \tag{10.23}\\
& I_{2}=I_{o 1}-K_{1} V_{1} \tag{10.24}
\end{align*}
$$

image_name:Figure 10.6 Gilbert multiplier with predistortion circuits
description:The circuit is a Gilbert cell multiplier with predistortion using inverse hyperbolic tangent circuits. It takes differential inputs V1 and V2, processes them through the inverse tanh blocks, and uses a differential pair of transistors to produce an output current ΔIout = Ic3-5 - Ic4-6.
Figure 10.6 Gilbert multiplier with predistortion circuits.
image_name:Figure 10.7 Inverse hyperbolic tangent circuit
description:The circuit is an inverse hyperbolic tangent circuit used in a Gilbert cell multiplier. It processes differential input V1 through a voltage-current converter and uses transistors Q7 and Q8 to produce a differential output voltage ΔV.

Figure 10.7 Inverse hyperbolic tangent circuit.

Here $I_{o 1}$ is the dc current that flows in each output lead if $V_{1}$ is equal to zero, and $K_{1}$ is the transconductance of the voltage-to-current converter. The differential voltage developed across the two diode-connected transistors is

$$
\begin{align*}
\Delta V & =V_{T} \ln \left(\frac{I_{o 1}+K_{1} V_{1}}{I_{S}}\right)-V_{T} \ln \left(\frac{I_{o 1}-K_{1} V_{1}}{I_{S}}\right) \\
& =V_{T} \ln \left(\frac{I_{o 1}+K_{1} V_{1}}{I_{o 1}-K_{1} V_{1}}\right) \tag{10.25}
\end{align*}
$$

This function can be transformed using the identity

$$
\begin{equation*}
\tanh ^{-1} x=\frac{1}{2} \ln \left(\frac{1+x}{1-x}\right) \tag{10.26}
\end{equation*}
$$

into the desired relationship.

$$
\begin{equation*}
\Delta V=2 V_{T} \tanh ^{-1}\left(\frac{K_{1} V_{1}}{I_{o 1}}\right) \tag{10.27}
\end{equation*}
$$

Thus if this functional block is used as the compensating nonlinearity in series with each input as shown in Fig. 10.6, the overall transfer characteristic becomes, using (10.19),

$$
\begin{equation*}
\Delta I=I_{E E}\left(\frac{K_{1} V_{1}}{I_{o 1}}\right)\left(\frac{K_{2} V_{2}}{I_{o 2}}\right) \tag{10.28}
\end{equation*}
$$

where $I_{o 2}$ and $K_{2}$ are the parameters of the functional block following $V_{2}$.
Equation 10.28 shows that the differential output current is directly proportional to the product $V_{1} V_{2}$, and, in principle, this relationship holds for all values of $V_{1}$ and $V_{2}$ for which the two output currents of the differential voltage-to-current converters are positive. For this to be true, $I_{1}$ and $I_{2}$ must always be positive, and from (10.23) and (10.24), we have

$$
\begin{align*}
& -\frac{I_{o 1}}{K_{1}}<V_{1}<\frac{I_{o 1}}{K_{1}}  \tag{10.29}\\
& -\frac{I_{o 2}}{K_{2}}<V_{2}<\frac{I_{o 2}}{K_{2}} \tag{10.30}
\end{align*}
$$

Note that the inclusion of a compensating nonlinearity on the $V_{2}$ input simply makes the collector currents of $Q_{1}$ and $Q_{2}$ directly proportional to input voltage $V_{2}$ rather than to its hyperbolic tangent. Thus the combination of the pair $Q_{1}-Q_{2}$ and the compensating nonlinearity on the $V_{2}$ input is redundant, and the output currents of the voltage-to-current converter on the $V_{2}$ input can be fed directly into the emitters of the $Q_{3}-Q_{4}$ and $Q_{5}-Q_{6}$ pairs with exactly the same results. The multiplier then takes on the form shown in Fig. 10.8.

### 10.2.4 A Complete Analog Multiplier ${ }^{2}$

In order to be useful in a wide variety of applications, the multiplier circuit must develop an output voltage that is referenced to ground and can take on both positive and negative values. The transistors $Q_{3}, Q_{4}, Q_{5}, Q_{6}, Q_{7}$, and $Q_{8}$, shown in Fig. 10.8 , are referred to as the multiplier core and produce a differential current output that then must be amplified, converted to a single-ended signal, and referenced to ground. An output amplifier is thus required, and the complete multiplier consists of two voltage-current converters, the core transistors, and an output current-to-voltage amplifier. While the core configuration of Fig. 10.8 is common to most four-quadrant transconductance multipliers, the rest of the circuitry can be realized in a variety of ways.

The most common configurations used for the voltage-current converters are emittercoupled pairs with emitter degeneration as shown in Fig. 10.5. The differential-to-single-ended converter of Fig. 10.8 is often realized with an op amp circuit of the type shown in Fig. 6.4. If this circuit has a transresistance given by

$$
\begin{equation*}
\frac{V_{\text {out }}}{\Delta I}=K_{3} \tag{10.31}
\end{equation*}
$$

image_name:Figure 10.8 Complete four-quadrant multiplier
description:The circuit is a complete four-quadrant multiplier with differential voltage-to-current converters and a differential-to-single-ended converter. The circuit multiplies two input voltages V1 and V2, producing an output voltage Vout proportional to their product. The transistors Q3 to Q8 form the multiplier core, and the differential-to-single-ended converter processes the output.

Figure 10.8 Complete four-quadrant multiplier.
then substitution in (10.28) gives for the overall multiplier characteristic

$$
\begin{equation*}
V_{\text {out }}=I_{E E} K_{3} \frac{K_{1}}{I_{o 1}} \frac{K_{2}}{I_{o 2}} V_{1} V_{2} \tag{10.32}
\end{equation*}
$$

The output voltage is thus proportional to the product $V_{1} V_{2}$ over a wide range. The constants in (10.32) are usually chosen so that

$$
\begin{equation*}
V_{\text {out }}=0.1 V_{1} V_{2} \tag{10.33}
\end{equation*}
$$

and all voltages have $\mathrm{a} \pm 10-\mathrm{V}$ range.

### 10.2.5 The Gilbert Multiplier Cell as a Balanced Modulator and Phase Detector

The four-quadrant multiplier just described is an example of an application of the multiplier cell in which all the devices remain in the active region during normal operation. Used in this way the circuit is capable of performing precise multiplication of one continuously varying analog signal by another. In communications systems, however, the need frequently arises for the multiplication of a continuously varying signal by a square wave. This is easily accomplished with the multiplier circuit by applying a sufficiently large signal (i.e., large compared to $2 V_{T}$ ) directly to the cross-coupled pair so that two of the four transistors alternately turn completely off and the other two conduct all the current. Since the transistors in the circuit do not enter saturation, this process can be accomplished at high speed. A set of typical waveforms that might result when a sinusoid is applied to the small-signal input and a square wave to the large-signal input is shown in Fig. 10.9. Note that since the devices in the multiplier are being switched on and off by the incoming square wave, the amplitude of the output waveform is independent of the amplitude of the square wave as long as it is large enough to cause the devices in the multiplier circuit to be fully on or fully off. Thus the circuit in this mode does not perform a linear multiplication of two waveforms, but actually causes the output voltage of the circuit produced by the small-signal input to be alternately multiplied by +1 and -1 .
image_name:Small – signal input
description:The graph consists of three separate time-domain waveforms: the small-signal input, the large-signal modulating input, and the output waveform.

1. **Small-Signal Input (Top Left):**
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The vertical axis is labeled as \( V_m(t) \), representing voltage, and the horizontal axis is labeled as \( t \), representing time.
- **Overall Behavior and Trends:** The waveform is a sinusoidal wave, indicating a periodic oscillation with a single frequency. The amplitude appears consistent, and the waveform crosses the time axis at regular intervals, indicating zero crossings.
- **Key Features:** The sinusoidal wave has a smooth, continuous curve with peaks (maxima) and valleys (minima) at regular intervals.

2. **Large-Signal Modulating Input (Top Right):**
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The vertical axis is labeled as \( V_c(t) \), representing voltage, and the horizontal axis is labeled as \( t \), representing time.
- **Overall Behavior and Trends:** The waveform is a square wave, characterized by abrupt transitions between high and low voltage levels. This indicates a non-sinusoidal periodic waveform with alternating positive and negative amplitudes.
- **Key Features:** The square wave alternates between two levels, likely +1 and -1, as indicated by the context, with equal time durations for each level.

3. **Output (Bottom):**
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The vertical axis is labeled as \( V_o(t) \), representing voltage, and the horizontal axis is labeled as \( t \), representing time.
- **Overall Behavior and Trends:** The output waveform is a result of the small-signal input being modulated by the large-signal square wave. It shows a pattern of alternating segments that resemble the input sinusoidal waveform but with sections inverted, reflecting the multiplication by +1 and -1.
- **Key Features:** The waveform maintains the frequency of the small-signal input but introduces modulation effects from the square wave, resulting in an alternating pattern of positive and negative sinusoidal segments.
image_name:Large – signal modulating input
description:The graph consists of three separate time-domain waveforms, labeled as 'Small – signal input,' 'Large – signal modulating input,' and 'Output.' Each waveform is plotted against time (t) on the horizontal axis.

1. **Small – Signal Input (V_m(t))**:
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The vertical axis represents the small-signal voltage \( V_m(t) \), and the horizontal axis represents time \( t \).
- **Overall Behavior and Trends:** This waveform is a sinusoidal wave, indicating a periodic oscillation. It starts from zero, reaches a positive peak, returns to zero, reaches a negative peak, and then returns to zero again, completing one full cycle.
- **Key Features:** The waveform exhibits smooth oscillations typical of a cosine or sine function.

2. **Large – Signal Modulating Input (V_c(t))**:
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The vertical axis represents the large-signal modulating voltage \( V_c(t) \), and the horizontal axis represents time \( t \).
- **Overall Behavior and Trends:** This waveform is a square wave with alternating high and low values. The amplitude alternates between +1 and -1, indicating a binary switching characteristic.
- **Key Features:** The waveform has sharp transitions between high and low states, with equal durations for each state, indicating a symmetrical duty cycle.

3. **Output (V_o(t))**:
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The vertical axis represents the output voltage \( V_o(t) \), and the horizontal axis represents time \( t \).
- **Overall Behavior and Trends:** The output waveform is a modulated version of the input signals. It appears as a series of sinusoidal segments with alternating polarity, corresponding to the multiplication by +1 and -1 as described in the context.
- **Key Features:** The waveform's amplitude and shape change according to the modulation by the square wave input, showing a periodic pattern of alternating positive and negative segments.

This graph illustrates a phase detector operation where the small-signal input is modulated by the large-signal square wave, resulting in an output that alternates in polarity with each cycle of the square wave.
image_name:Output
description:The graph consists of three distinct waveforms, each representing different signals involved in a phase detection process.

1. **Small-Signal Input (Top Left):**
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The vertical axis is labeled as \( V_m(t) \), representing voltage, while the horizontal axis is labeled as \( t \), representing time.
- **Overall Behavior and Trends:** The waveform is a sinusoidal signal, showing a single full cycle of a cosine wave. It starts at zero, reaches a positive peak, returns to zero, reaches a negative peak, and returns to zero again.
- **Key Features:** The waveform is symmetric around the horizontal axis, indicating a pure sinusoidal input without any DC offset.

2. **Large-Signal Modulating Input (Top Right):**
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The vertical axis is labeled as \( V_c(t) \), representing voltage, and the horizontal axis is labeled as \( t \), representing time.
- **Overall Behavior and Trends:** This is a square wave signal alternating between +1 and -1. The waveform shows several cycles of a square wave, with sharp transitions between its high and low states.
- **Key Features:** The waveform has a constant amplitude and period, indicating a consistent switching pattern.

3. **Output (Bottom):**
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The vertical axis is labeled as \( V_o(t) \), representing voltage, and the horizontal axis is labeled as \( t \), representing time.
- **Overall Behavior and Trends:** The output waveform is a modulated signal resulting from the interaction of the small-signal input and the large-signal modulating input. It shows a pattern of alternating segments, where the amplitude of the sinusoidal input is multiplied by +1 and -1, creating a series of positive and negative lobes.
- **Key Features:** The waveform reflects the multiplication of the input sinusoid by the square wave, resulting in a full-wave rectified-like appearance but with alternating polarity. This demonstrates the phase detection or modulation process in action, where the output closely follows the form of the input sinusoid but is switched in polarity according to the square wave.

Figure 10.9 Input and output waveforms for a phase detector with large input signals.

The spectrum of the output may be developed directly from the Fourier series of the two inputs. For the low-frequency modulating sinusoidal input,

$$
\begin{equation*}
V_{m}(t)=V_{m} \cos \omega_{m} t \tag{10.34}
\end{equation*}
$$

and for the high-frequency square wave input, which we assume has an amplitude of $\pm 1$ as discussed above,

$$
\begin{equation*}
V_{c}(t)=\sum_{n=1}^{\infty} A_{n} \cos n \omega_{c} t, \quad A_{n}=\frac{\sin \frac{n \pi}{2}}{\frac{n \pi}{4}} \tag{10.35}
\end{equation*}
$$

Thus the output signal is

$$
\begin{align*}
V_{o}(t) & =K\left[V_{c}(t) V_{m}(t)\right]=K \sum_{n=1}^{\infty} A_{n} V_{m} \cos \omega_{n} t \cos n \omega_{c} t  \tag{10.36}\\
& =K \sum_{n=1}^{\infty} \frac{A_{n} V_{m}}{2}\left[\cos \left(n \omega_{c}+\omega_{m}\right) t+\cos \left(n \omega_{c}-\omega_{m}\right) t\right] \tag{10.37}
\end{align*}
$$

where $K$ is the magnitude of the gain of the multiplier from the small-signal input to the output.
The spectrum has components located at frequencies $\omega_{m}$ above and below each of the harmonics of $\omega_{c}$, but no component at the carrier frequency $\omega_{c}$ or its harmonics. The spectrum of the input signals and the resulting output signal is shown in Fig. 10.10. The lack of an output component at the carrier frequency is a very useful property of balanced modulators. The signal is usually filtered following the modulation process so that only the components near $\omega_{c}$ are retained.

If a dc component is added to the modulating input, the result is a signal component in the output at the carrier frequency and its harmonics. If the modulating signal is given by

$$
\begin{equation*}
V_{m}(t)=V_{m}\left(1+M \cos \omega_{m} t\right) \tag{10.38}
\end{equation*}
$$

image_name:V_m(ω)
description:The graph titled "V_m(ω)" is a spectral representation of the modulating signal in the frequency domain. It is a line spectrum graph, showing discrete frequency components.

1. **Type of Graph and Function:**
- The graph is a frequency spectrum plot, displaying the amplitude of the modulating signal as a function of angular frequency (ω).

2. **Axes Labels and Units:**
- The horizontal axis represents angular frequency (ω) in radians per second.
- The vertical axis represents the amplitude of the modulating signal, V_m(ω).
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The graph shows a single spectral line at the frequency ω_m, indicating that the modulating signal is a single-frequency sinusoid.
- There are no other frequency components present, which implies a pure tone modulation.

4. **Key Features and Technical Details:**
- A prominent peak is observed at ω_m, representing the fundamental frequency of the modulating signal.
- The absence of other peaks indicates no harmonic distortion or additional frequency components in the modulating signal.

5. **Annotations and Specific Data Points:**
- The graph does not have additional annotations or reference lines.
- The key data point is the peak at ω_m, which is the only significant frequency component in the modulating signal.

This graph illustrates a simple modulating signal characterized by a single frequency component, essential for understanding the modulation process in a balanced modulator system.
image_name:V_c(ω)
description:The graph labeled "V_c(ω)" is a frequency domain representation of a carrier signal, part of a series of spectra illustrating the input and output of a balanced modulator. This graph is plotted on a standard linear scale with the horizontal axis representing angular frequency, ω, in radians per second, and the vertical axis representing the amplitude of the carrier signal, V_c(ω).

Type of Graph and Function
This is a spectral plot showing discrete frequency components of the carrier signal.

Axes Labels and Units
- **Horizontal Axis (ω):** Frequency in radians per second.
- **Vertical Axis (V_c(ω)):** Amplitude of the carrier frequency.

Overall Behavior and Trends
The graph displays discrete spikes at specific frequencies, indicating the presence of sinusoidal components at those frequencies. The primary component is at the carrier frequency ω_c, with additional components at multiples of the carrier frequency (3ω_c, 5ω_c, etc.), each decreasing in amplitude as the frequency increases.

Key Features and Technical Details
- **Primary Spike:** At ω_c, the carrier frequency, showing the main component of the signal.
- **Harmonic Components:** Additional spikes are present at odd harmonics of the carrier frequency (3ω_c and 5ω_c). These harmonics have smaller amplitudes compared to the primary carrier frequency.

Annotations and Specific Data Points
- **ω_c:** The fundamental carrier frequency, being the largest spike on the graph.
- **3ω_c and 5ω_c:** Indicate the presence of odd harmonics, which are characteristic of certain types of modulated signals, particularly when considering non-linearities or intentional harmonic generation in modulation processes.

This spectral plot is essential in understanding the frequency components involved in the modulation process and is typically used to analyze the efficiency and purity of modulation in communication systems.
image_name:V_o(ω)
description:The graph labeled "V_o(ω)" is a frequency-domain representation of the output of a balanced modulator. This type of graph is a spectral plot showing the amplitude of different frequency components present in the signal.

Axes Labels and Units:
- **Horizontal Axis (ω):** Represents frequency in radians per second (rad/s). The axis is marked with significant frequency points such as ω_c (carrier frequency), 2ω_c, 3ω_c, etc.
- **Vertical Axis:** Represents the amplitude of the frequency components. The scale is not specified but is consistent across the graph.

Overall Behavior and Trends:
- The graph shows discrete frequency components, indicating that the output signal consists of multiple sinusoidal components at specific frequencies.
- The presence of components at ω_c - ω_m and ω_c + ω_m indicates the modulation of the carrier frequency ω_c by the modulating frequency ω_m.
- Additional components are observed at harmonics of the carrier frequency (3ω_c, 5ω_c) and their respective sidebands (e.g., 3ω_c - ω_m, 3ω_c + ω_m).

Key Features and Technical Details:
- **Carrier Frequency (ω_c):** A prominent peak at ω_c, indicating the presence of the carrier frequency in the output.
- **Sidebands:** Peaks at ω_c - ω_m and ω_c + ω_m, which are characteristic of amplitude modulation.
- **Harmonics:** Peaks at 3ω_c and 5ω_c, which are higher harmonics of the carrier frequency.
- **Harmonic Sidebands:** Peaks at 3ω_c - ω_m, 3ω_c + ω_m, 5ω_c - ω_m, and 5ω_c + ω_m, showing the modulation effects on higher harmonics.

Annotations and Specific Data Points:
- The graph is annotated with specific frequency components, highlighting the modulated signal's structure. These annotations help in identifying the carrier and sideband frequencies resulting from the modulation process.

This spectral plot effectively illustrates the frequency components present in the output of a balanced modulator, emphasizing the carrier frequency and its modulation by the input signal.

Figure 10.10 Input and output spectra for a balanced modulator.
where the parameter $M$ is called the modulation index, then the output is given by

$$
\begin{equation*}
V_{o}(t)=K \sum_{n=1}^{\infty} A_{n} V_{m}\left[\cos \left(n \omega_{c} t\right)+\frac{M}{2} \cos \left(n \omega_{c}+\omega_{m}\right) t+\frac{M}{2} \cos \left(n \omega_{c}-\omega_{m}\right) t\right] \tag{10.39}
\end{equation*}
$$

This dc component can be introduced intentionally to provide conventional amplitude modulation or it can be the result of offset voltages in the devices within the modulator, which results in undesired carrier feedthrough in suppressed-carrier modulators.

Note that the balanced modulator actually performs a frequency translation. Information contained in the modulating signal $V_{m}(t)$ was originally concentrated at the modulating frequency $\omega_{m}$. The modulator has translated this information so that it is now contained in spectral components located near the harmonics of the high-frequency signal $V_{c}(t)$, usually called the carrier. Balanced modulators are also useful for performing demodulation, which is the extraction of information from the frequency band near the carrier and retranslation of the information back down to low frequencies.

In frequency translation, signals at two different frequencies are applied to the two inputs, and the sum or the difference frequency component is taken from the output. If unmodulated signals of identical frequency $\omega_{o}$ are applied to the two inputs, the circuit behaves as a phase detector and produces an output whose dc component is proportional to the phase difference between the two inputs. For example, consider the two input waveforms in Fig. 10.11, which are applied to the Gilbert multiplier shown in the same figure. We assume first for simplicity that both inputs are large in magnitude so that all the transistors in the circuit are behaving as switches. The output waveform that results is shown in Fig. 10.11c and consists of a dc component and a component at twice the incoming frequency. The dc component of this
image_name:(a)
description:The graph labeled "(a)" is a time-domain waveform representing the input voltage $V_{in1}$ as a function of time, denoted by $\omega_0 t$. This is a square waveform, characterized by periodic transitions between high and low states.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform depicting a square wave input.

2. **Axes Labels and Units:**
- The horizontal axis represents time, labeled as $\omega_0 t$, indicating angular frequency times time.
- The vertical axis represents the input voltage, labeled as $V_{in1}$.
- The waveform is periodic with transitions occurring at intervals of $\pi$, $2\pi$, $3\pi$, and $4\pi$.

3. **Overall Behavior and Trends:**
- The waveform is a square wave, alternating between high and low states at regular intervals.
- The high state is maintained for a duration of $\pi$ radians, followed by a low state for the same duration.
- The waveform is periodic and consistent, with no decay or growth over time.

4. **Key Features and Technical Details:**
- The waveform shows a phase shift $\phi$ at the beginning, indicating a delay in the transition from low to high state.
- The waveform maintains a consistent amplitude throughout the observed period.

5. **Annotations and Specific Data Points:**
- The phase shift $\phi$ is marked, indicating the delay in the initial transition.
- No other specific data points or annotations are provided on this graph.
image_name:Figure 10.11
description:The circuit is a Gilbert multiplier used as a phase detector. It consists of six NPN transistors arranged to multiply two input signals, producing an output with a DC component and a component at twice the input frequency. The phase difference between the inputs affects the DC output voltage.
image_name:(c)
description:The graph labeled (c) in Figure 10.11 is a time-domain waveform representing the output voltage \( V_o \) of a phase detector circuit. The x-axis is labeled \( \omega_0 t \) and is measured in radians, indicating the phase angle over time. The y-axis represents the output voltage \( V_o \) and is measured in volts.

The waveform is a square wave oscillating between \(+I_{EE}R_C\) and \(-I_{EE}R_C\). The waveform has a periodicity of \(2\pi\), with each cycle consisting of two distinct sections: a positive section where \( V_o = +I_{EE}R_C \), and a negative section where \( V_o = -I_{EE}R_C \).

The graph highlights two areas, \( A_1 \) and \( A_2 \), which are shaded. These areas represent the integral parts of the waveform that contribute to the average output voltage \( V_{\text{average}} \). The phase difference \( \phi \) between the input signals is marked on the graph, indicating the offset of the waveform from a reference point.

The overall behavior of the waveform is periodic with a constant amplitude, and the phase shift \( \phi \) affects the balance between the positive and negative areas of the waveform, thus influencing the dc component of the output. The waveform maintains a constant frequency, with no variation in amplitude or frequency over time.
Figure 10.11 Typical input and output waveforms for a phase detector.
waveform is given by

$$
\begin{align*}
V_{\text {average }} & =\frac{1}{2 \pi} \int_{0}^{2 \pi} V_{o}(t) d\left(\omega_{0} t\right)  \tag{10.40}\\
& =\frac{-1}{\pi}\left(A_{1}-A_{2}\right) \tag{10.41}
\end{align*}
$$

where areas $A_{1}$ and $A_{2}$ are as indicated in Fig. 10.11c. Thus,

$$
\begin{align*}
V_{\text {average }} & =-\left[I_{E E} R_{C} \frac{(\pi-\phi)}{\pi}-\frac{I_{E E} R_{C} \phi}{\pi}\right]  \tag{10.42}\\
& =I_{E E} R_{C}\left(\frac{2 \phi}{\pi}-1\right) \tag{10.43}
\end{align*}
$$

image_name:Figure 10.12
description:The graph in Figure 10.12 is a plot of the DC component of the phase detector output, denoted as \( V_o \), against the phase difference \( \phi \). It is a piecewise linear graph that illustrates how the output voltage of a phase detector varies with the phase difference between two input signals.

**Axes Labels and Units:**
- The vertical axis represents \( V_o \), the DC component of the phase detector output, with values marked as \( I_{EE}R_C \) and \(-I_{EE}R_C \).
- The horizontal axis represents the phase difference \( \phi \), with key points marked at \( \pi/2 \) and \( \pi \).

**Overall Behavior and Trends:**
- The graph starts at \( -I_{EE}R_C \) when \( \phi = 0 \), indicating a negative DC component.
- As \( \phi \) increases from 0 to \( \pi/2 \), \( V_o \) increases linearly from \( -I_{EE}R_C \) to \( I_{EE}R_C \).
- From \( \pi/2 \) to \( \pi \), the graph continues to increase linearly, reaching a peak at \( \phi = \pi \) with \( V_o = I_{EE}R_C \).
- Beyond \( \phi = \pi \), \( V_o \) decreases linearly back to \( -I_{EE}R_C \) at \( \phi = 2\pi \), completing the cycle.

**Key Features and Technical Details:**
- The graph is symmetric about \( \phi = \pi \), showing a linear increase and decrease.
- The slope of the line segments is constant, indicating a uniform rate of change in the output voltage with respect to the phase difference.
- The graph crosses the horizontal axis at \( \phi = \pi/2 \) and \( \phi = 3\pi/2 \), where the DC component is zero.

**Annotations and Specific Data Points:**
- The graph is annotated with the labels \( V_o = \text{dc component in phase detector output} \) and critical values are indicated by dashed lines at \( I_{EE}R_C \) and \(-I_{EE}R_C \).

Figure 10.12 Phase detector output versus phase difference.

This phase relationship is plotted in Fig. 10.12. This phase demodulation technique is widely used in phase-locked loops.

We assumed above that the input waveforms were large in amplitude and were square waves. If the input signal amplitude is large, the actual waveform shape is unimportant since the multiplier simply switches from one state to the other at the zero crossings of the waveform. For the case in which the amplitude of one or both of the input signals has an amplitude comparable to or smaller than $V_{T}$, the circuit still acts as a phase detector. However, the output voltage then depends both on the phase difference and on the amplitude of the two input waveforms. The operation of the circuit in this mode is considered further in Section 10.3.3.

## 10.3 Phase-Locked Loops (PLL)

The phase-locked loop concept was first developed in the 1930s. ${ }^{3}$ It has since been used in communications systems of many types, particularly in satellite communications systems. Until recently, however, phase-locked systems have been too complex and costly for use in most consumer and industrial systems, where performance requirements are more modest and other approaches are more economical. The PLL is particularly amenable to monolithic construction, however, and integrated-circuit phase-locked loops can now be fabricated at very low cost. ${ }^{4}$ Their use has become attractive for many applications such as FM demodulators, stereo demodulators, tone detectors, frequency synthesizers, and others. In this section we first explore the basic operation of the PLL, and then consider analytically the performance of the loop in the locked condition. We then discuss the design of monolithic PLLs.

### 10.3.1 Phase-Locked Loop Concepts

A block diagram of the basic phase-locked loop system is shown in Fig. 10.13. The elements of the system are a phase comparator, a loop filter, an amplifier, and a voltage-controlled oscillator. The voltage-controlled oscillator, or VCO, is simply an oscillator whose frequency is proportional to an externally applied voltage. When the loop is locked on an incoming periodic signal, the VCO frequency is exactly equal to that of the incoming signal. The phase detector produces a dc or low-frequency signal proportional to the phase difference between the incoming signal and the VCO output signal. This phase-sensitive signal is then passed through the loop filter and amplifier and is applied to the control input of the VCO. If, for example, the frequency of the incoming signal shifts slightly, the phase difference between
image_name:Figure 10.13 Phase-locked-loop system
description:The phase-locked-loop (PLL) system depicted in Figure 10.13 consists of four main components: a Phase Detector, a Loop Filter, an Amplifier, and a Voltage-Controlled Oscillator (VCO).

1. **Main Components:**
- **Phase Detector:** This block receives the input signal and compares its phase with the output from the VCO. It produces a signal proportional to the phase difference between these two inputs.
- **Loop Filter:** The output from the phase detector is fed into the loop filter. This filter smooths the signal, reducing high-frequency noise and providing a stable control voltage.
- **Amplifier:** The filtered signal is then amplified to a suitable level to drive the VCO.
- **Voltage-Controlled Oscillator (VCO):** The VCO generates an output signal whose frequency is controlled by the input voltage from the amplifier. This signal is fed back to the phase detector for continuous phase comparison.

2. **Flow of Information or Control:**
- The system begins with the input signal entering the phase detector.
- The phase detector outputs a signal based on the phase difference, which is passed to the loop filter.
- The loop filter processes the signal to remove noise and then sends it to the amplifier.
- The amplifier increases the signal’s strength before it is applied to the VCO.
- The VCO adjusts its frequency based on the input from the amplifier, producing a signal that is fed back to the phase detector, completing the feedback loop.

3. **Labels, Annotations, and Key Indicators:**
- The diagram is labeled with the input and output points, as well as each component's function, such as "Phase detector," "Loop filter," "Amplifier," and "Voltage-controlled oscillator."

4. **Overall System Function:**
- The primary function of this PLL system is to synchronize the VCO frequency with the frequency of the incoming signal. It achieves this by continuously adjusting the VCO based on the phase difference detected between the incoming signal and the VCO’s output. This allows the system to maintain lock with the input signal, even if its frequency changes slightly. This makes the PLL particularly useful for applications such as FM demodulation, where maintaining frequency lock is crucial.

Figure 10.13 Phase-locked-loop system.
the VCO signal and the incoming signal will begin to increase with time. This will change the control voltage on the VCO in such a way as to bring the VCO frequency back to the same value as the incoming signal. Thus the loop can maintain lock when the input signal frequency changes, and the VCO input voltage is proportional to the frequency of the incoming signal. This behavior makes PLLs particularly useful for the demodulation of FM signals, where the frequency of the incoming signal varies in time and contains the desired information. The range of input signal frequencies over which the loop can maintain lock is called the lock range.

An important aspect of PLL performance is the capture process, by which the loop goes from the unlocked, free-running condition to that of being locked on a signal. In the unlocked condition, the VCO runs at the frequency corresponding to zero applied dc voltage at its control input. This frequency is called the center frequency, or free-running frequency. When a periodic signal is applied that has a frequency near the free-running frequency, the loop may or may not lock on it depending on a number of factors. The capture process is inherently nonlinear in nature, and we will describe the transient in only a qualitative way.

First assume that the loop is opened between the loop filter and the VCO control input, and that a signal whose frequency is near, but not equal to, the free-running frequency is applied to the input of the PLL. The phase detector is usually of the type discussed in the last section, but for this qualitative discussion we assume that the phase detector is simply an analog multiplier that multiplies the two sinusoids together. Thus the output of the multiplierphase detector contains the sum and difference frequency components, and we assume that the sum frequency component is sufficiently high in frequency that it is filtered out by the low-pass filter. The output of the low-pass filter, then, is a sinusoid with a frequency equal to the difference between the VCO free-running frequency and the incoming signal frequency.

Now assume that the loop is suddenly closed, and the difference frequency sinusoid is now applied to the VCO input. This will cause the VCO frequency itself to become a sinusoidal function of time. Let us assume that the incoming frequency was lower than the free-running frequency. Since the VCO frequency is varying as a function of time, it will alternately move closer to the incoming signal frequency and farther away from the incoming signal frequency. The output of the phase detector is a near-sinusoid whose frequency is the difference between the VCO frequency and the input frequency. When the VCO frequency moves away from the incoming frequency, this sinusoid moves to a higher frequency. When the VCO frequency moves closer to the incoming frequency, the sinusoid moves to a lower frequency. If we examine the effect of this on the phase detector output, we see that the frequency of this sinusoidal difference-frequency waveform is reduced when its incremental amplitude is negative, and increased when its amplitude is positive. This causes the phase detector output to have an asymmetrical waveform during capture, as shown in Fig. 10.14. This asymmetry in the waveform introduces a dc component in the phase detector output that shifts the average VCO frequency toward the incoming signal frequency, so that the difference frequency gradually decreases. Once the system becomes locked, of course, the difference frequency becomes zero and only a dc voltage remains at the loop-filter output.
image_name:Figure 10.14
description:The graph depicted in Figure 10.14 is a time-domain waveform representing the output of a phase detector during the capture transient of a phase-locked loop (PLL) system. The horizontal axis is labeled as 't,' indicating time, while the vertical axis is labeled as 'V_o,' representing the output voltage of the phase detector.

Axes Labels and Units:
- **Horizontal Axis (t):** Represents time, though specific units (e.g., milliseconds, seconds) are not provided.
- **Vertical Axis (V_o):** Represents voltage output, with no specific units given.

Overall Behavior and Trends:
The waveform exhibits a series of oscillations that gradually decrease in amplitude over time. Initially, the waveform starts with larger oscillations, indicating a free-running dc output. As time progresses, the oscillations diminish in amplitude, approaching a stable dc output level, which corresponds to the locked condition of the PLL.

Key Features and Technical Details:
- **Oscillations:** The waveform shows a periodic oscillatory behavior at the beginning, with peaks and troughs indicating variations in the phase detector output.
- **Damping:** The amplitude of the oscillations decreases over time, suggesting a damping effect as the system approaches lock.
- **Stable DC Level:** Two horizontal dashed lines are marked on the graph. The upper line represents the free-running dc output level, while the lower line indicates the dc output level when the system is locked.
- **Loop Closure:** A vertical dashed line labeled 'Loop closed here' marks the point in time where the loop is closed, initiating the transition from free-running to locked condition.

Annotations and Specific Data Points:
- The transition from oscillatory behavior to a stable dc output is clearly annotated with the 'Loop closed here' line, providing a reference point for when the PLL begins to capture the signal and stabilize.
- The graph visually demonstrates the process of the PLL capturing and locking onto the incoming signal, with the decreasing oscillations indicating the reduction in frequency difference between the VCO and the input signal.

Overall, this graph effectively illustrates the dynamic behavior of a phase-locked loop during the capture phase, highlighting the transition from an initial oscillatory state to a stable locked condition.

Figure 10.14 Typical phase detector output during capture transient.

The capture range of the loop is that range of input frequencies around the center frequency onto which the loop will become locked from an unlocked condition. The pull-in time is the time required for the loop to capture the signal. Both these parameters depend on the amount of gain in the loop itself, and the bandwidth of the loop filter. The objective of the loop filter is to filter out difference components resulting from interfering signals far away from the center frequency. It also provides a memory for the loop in case lock is momentarily lost due to a large interfering transient. Reducing the loop filter bandwidth thus improves the rejection of out-of-band signals, but, at the same time, the capture range is decreased, the pull-in time becomes longer, and the loop phase margin becomes poorer.

### 10.3.2 The Phase-Locked Loop in the Locked Condition

Under locked conditions, a linear relationship exists between the output voltage of the phase detector and the phase difference between the VCO and the incoming signal. This fact allows the loop to be analyzed using standard linear feedback concepts when in the locked condition. A block diagram representation of the system in this mode is shown in Fig. 10.15. The gain of the phase comparator is $K_{D} \mathrm{~V} / \mathrm{rad}$ of phase difference, the loop-filter transfer function is $F(s)$, and any gain in the forward loop is represented by $A$. The VCO gain is $K_{o} \mathrm{rad} / \mathrm{s}$ per volt.

If a constant input voltage is applied to the VCO control input, the output frequency of the VCO remains constant. However, the phase comparator is sensitive to the difference between the phase of the VCO output and the phase of the incoming signal. The phase of the VCO output is actually equal to the time integral of the VCO output frequency, since

$$
\begin{equation*}
\omega_{\mathrm{osc}}(t)=\frac{d \phi_{\mathrm{osc}}(t)}{d t} \tag{10.44}
\end{equation*}
$$

and thus

$$
\begin{equation*}
\phi_{\mathrm{osc}}(t)=\left.\phi_{\mathrm{osc}}\right|_{t=0}+\int_{0}^{t} \omega_{\mathrm{osc}}(t) d t \tag{10.45}
\end{equation*}
$$

image_name:Figure 10.15 Block diagram of the PLL system
description:The block diagram in Figure 10.15 represents a Phase-Locked Loop (PLL) system, which is used to synchronize the phase of the voltage-controlled oscillator (VCO) output with that of an incoming signal. Here is a detailed breakdown of the system:

1. **Main Components:**
- **Phase Detector:** This component compares the phase of the incoming signal, \( \phi_i \), with the phase of the VCO output, \( \phi_{osc} \). It outputs a phase error signal, \( \phi_\epsilon \), which indicates the difference between these two phases.
- **Gain Block (\( K_D \) V/rad):** This block scales the phase error signal \( \phi_\epsilon \) by a gain factor \( K_D \), converting it into a voltage.
- **Filter (\( F(s) \)):** The filtered error signal helps stabilize the loop and determines the dynamic characteristics of the PLL.
- **Amplifier (\( A \)):** This block further amplifies the filtered signal to drive the VCO input.
- **Voltage-Controlled Oscillator (VCO):** The VCO generates an output frequency \( \omega_{osc} \) that is controlled by the input voltage \( V_o \). The relationship is defined as \( \omega_{osc} = \omega_0 + K_O V_o \), where \( \omega_0 \) is the free-running frequency and \( K_O \) is the VCO gain.
- **Integrator (\( 1/s \)):** This block represents the integration of the VCO output frequency to produce the phase \( \phi_{osc} \).

2. **Flow of Information or Control:**
- The input phase \( \phi_i \) and the feedback phase \( \phi_{osc} \) are compared in the phase detector, generating a phase error \( \phi_\epsilon \).
- The error signal \( \phi_\epsilon \) is processed through the gain block \( K_D \), filter \( F(s) \), and amplifier \( A \) to produce the control voltage \( V_o \) for the VCO.
- The VCO adjusts its output frequency \( \omega_{osc} \) based on \( V_o \), and this frequency is integrated to update the phase \( \phi_{osc} \).
- The updated phase \( \phi_{osc} \) is fed back to the phase detector, completing the control loop.

3. **Labels, Annotations, and Key Indicators:**
- The gain of the phase detector is labeled as \( K_D \) V/rad.
- The VCO gain is labeled as \( K_O \) rad/s/V.
- The integrator is represented by \( 1/s \).
- The output of the amplifier is denoted as \( V_o \).

4. **Overall System Function:**
- The primary function of this PLL system is to lock the phase of the VCO output to the phase of the incoming signal \( \phi_i \). This is achieved through the feedback loop, which continuously adjusts the VCO frequency to minimize the phase error \( \phi_\epsilon \). The integration in the loop ensures that the VCO's phase tracks the incoming signal's phase over time, maintaining synchronization.

Figure 10.15 Block diagram of the PLL system.

Thus an integration inherently takes place within the phase-locked loop. This integration is represented by the $1 / s$ block in Fig. 10.15.

For practical reasons, the VCO is actually designed so that when the VCO input voltage (i.e., $V_{o}$ ) is zero, the VCO frequency is not zero. The relation between the VCO output frequency $\omega_{\text {osc }}$ and $V_{o}$ is actually

$$
\omega_{\mathrm{osc}}=\omega_{o}+K_{O} V_{o}
$$

where $\omega_{o}$ is the free-running frequency that results when $V_{o}=0$.
The system can be seen from Fig. 10.15 to be a classical linear feedback control system. ${ }^{5}$ The closed-loop transfer function is given by

$$
\begin{align*}
\frac{V_{o}}{\phi_{i}} & =\frac{K_{D} F(s) A}{1+K_{D} F(s) A \frac{K_{o}}{s}}  \tag{10.46}\\
& =\frac{s K_{D} F(s) A}{s+K_{D} K_{O} A F(s)} \tag{10.47}
\end{align*}
$$

Usually we are interested in the response of this loop to frequency variations at the input, so that the input variable is frequency rather than phase. Since

$$
\begin{equation*}
\omega_{i}=\frac{d \phi_{i}}{d t} \tag{10.48}
\end{equation*}
$$

then

$$
\begin{equation*}
\omega_{i}(s)=s \phi_{i}(s) \tag{10.49}
\end{equation*}
$$

and

$$
\begin{equation*}
\frac{V_{o}}{\omega_{i}}=\frac{1}{s} \frac{V_{o}}{\phi_{i}}=\frac{K_{D} F(s) A}{s+K_{D} K_{O} A F(s)} \tag{10.50}
\end{equation*}
$$

We first consider the case in which the loop filter is removed entirely, and $F(s)$ is unity. This is called a first-order loop and we have

$$
\begin{equation*}
\frac{V_{o}}{\omega_{i}}=\left(\frac{K_{v}}{s+K_{v}}\right)\left(\frac{1}{K_{O}}\right) \tag{10.51}
\end{equation*}
$$

where

$$
\begin{equation*}
K_{v}=K_{O} K_{D} A \tag{10.52}
\end{equation*}
$$

Thus the loop inherently produces a first-order, low-pass transfer characteristic. Remember that we regard the input variable as the frequency $\omega_{i}$ of the incoming signal. The response calculated above, then, is really the response from the frequency modulation on the incoming carrier to the loop voltage output.

The constant above $\left(K_{v}\right)$ is termed the loop bandwidth. If the loop is locked on a carrier signal, and the frequency of that carrier is made to vary sinusoidally in time with a frequency $\omega_{m}$, then a sinusoid of frequency $\omega_{m}$ will be observed at the loop output. When $\omega_{m}$ is increased above $K_{v}$, the magnitude of the sinusoid at the output falls. The loop bandwidth $K_{v}$, then, is the effective bandwidth for the modulating signal that is being demodulated by the PLL. In terms of the loop parameters, $K_{v}$ is simply the product of the phase detector gain, VCO gain, and any other electrical gain in the loop. The root locus of this single pole as a function of loop gain $K_{v}$ is shown in Fig. 10.16a. The frequency response is also shown in this figure. The response of the loop to variations in input frequency is illustrated in Fig. $10.16 b$ and by the following example.
image_name:Root locus
description:### Graph Description of Figure 10.16

1. Type of Graph and Function:
The graph consists of two main parts: a root locus plot and a frequency response plot for a first-order phase-locked loop (PLL). Additionally, there is a time-domain response illustrating the loop output voltage's behavior to step changes in input frequency.

2. Axes Labels and Units:
- **Root Locus Plot (a):**
- Horizontal axis: Real part (\(\sigma\))
- Vertical axis: Imaginary part (\(j\omega\))
- The plot shows the open-loop and closed-loop pole positions.

- **Frequency Response Plot (a):**
- Horizontal axis: Frequency (\(\omega\)) on a logarithmic scale
- Vertical axis: Magnitude \(\left| \frac{V_o}{\omega_i} (j\omega) \right|\) on a logarithmic scale
- A key marker is at \(\frac{1}{K_O}\) indicating the closed-loop response level.

- **Time-Domain Response (b):**
- Horizontal axis: Time (\(t\))
- Vertical axis: Input Voltage (\(V_i\)) and Output Voltage (\(V_o\)) in volts
- Key frequencies are marked: \(\omega_i = 2\pi(500 \text{ Hz})\), \(\omega_i = 2\pi(1 \text{ kHz})\), and \(\omega_i = 2\pi(250 \text{ Hz})\).

3. Overall Behavior and Trends:
- **Root Locus Plot:**
- The plot indicates the movement of poles from the open-loop to the closed-loop positions as the loop gain changes.

- **Frequency Response Plot:**
- Shows a flat response at low frequencies, which then decreases at higher frequencies, illustrating a typical low-pass filter behavior.

- **Time-Domain Response:**
- The response shows oscillations at different input frequencies, with the output voltage adjusting to changes in input frequency.

4. Key Features and Technical Details:
- **Root Locus Plot:**
- The transition from open-loop to closed-loop indicates stabilization with gain adjustments.

- **Frequency Response Plot:**
- The cutoff frequency is implied by the slope change in the response curve.
- The response level \(\frac{1}{K_O}\) is a critical value for interpreting the loop's behavior.

- **Time-Domain Response:**
- Step changes in input frequency lead to corresponding changes in output voltage.
- The response time \(\tau = \frac{1}{K_v} = 2 \text{ ms}\) is marked, indicating the loop's speed of response.
- Voltage changes are calculated as \(V = \frac{\omega_i - \omega_o}{K_O}\), with specific examples shown (e.g., \(0.5 \text{ V}\), \(0.25 \text{ V}\)).

5. Annotations and Specific Data Points:
- **Root Locus Plot:**
- Open-loop and closed-loop pole positions are annotated.

- **Frequency Response Plot:**
- The closed-loop response level is annotated at \(\frac{1}{K_O}\).

- **Time-Domain Response:**
- Frequencies and corresponding voltage changes are annotated, providing clear examples of the PLL's behavior under varying conditions.
image_name:Closed-loop response
description:The graph labeled "Closed-loop response" is a frequency response plot of a first-order phase-locked loop (PLL). It is a Bode plot that shows the magnitude of the closed-loop transfer function on a logarithmic scale.

Axes Labels and Units:
- **Horizontal Axis (ω):** Represents frequency in radians per second (logarithmic scale).
- **Vertical Axis (|V_o/ω_i(jω)|):** Represents the magnitude of the output voltage to input frequency ratio, also on a logarithmic scale.

Overall Behavior and Trends:
- The graph exhibits a flat response at low frequencies, indicating that the loop gain is constant until a certain cutoff frequency.
- At higher frequencies, the magnitude decreases, showing a roll-off characteristic typical of low-pass filters.
- The transition point, marked by a change in slope, corresponds to the loop bandwidth, determined by the loop gain constant (K_v).

Key Features and Technical Details:
- The plot starts with a constant magnitude at low frequencies, indicating a stable closed-loop response.
- The magnitude begins to decrease at the frequency determined by K_v, indicating the bandwidth of the loop.
- The slope of the roll-off is determined by the order of the system; for a first-order loop, it is typically -20 dB/decade.
- The gain level at the lower frequencies is marked as 1/K_O, where K_O is the VCO gain.

Annotations and Specific Data Points:
- The cutoff frequency is marked by the loop gain K_v.
- The magnitude at low frequencies is annotated as 1/K_O, providing a reference for the initial gain level.

This graph effectively shows how the PLL maintains a consistent gain up to a certain frequency, after which the gain decreases, illustrating the loop's ability to track input frequency changes within its bandwidth.
image_name:(b)
description:The graph labeled (b) is a time-domain waveform illustrating the response of a phase-locked loop (PLL) to step changes in input frequency. It consists of two main parts: the input frequency waveform and the output voltage response.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform showing the input frequency and output voltage of a PLL.

2. **Axes Labels and Units:**
- The horizontal axis represents time \( t \).
- The vertical axis on the upper graph represents input frequency \( V_i \), while the vertical axis on the lower graph represents output voltage \( V_o \) in volts.

3. **Overall Behavior and Trends:**
- The input frequency \( \omega_i \) changes in a step-like manner at specific time intervals. Initially, it starts at \( \omega_i = 2\pi(500 \text{ Hz}) \), then jumps to \( \omega_i = 2\pi(1 \text{ kHz}) \), drops to \( \omega_i = 2\pi(250 \text{ Hz}) \), and finally returns to \( \omega_i = 2\pi(1 \text{ kHz}) \).
- The output voltage \( V_o \) responds to these changes with a characteristic exponential rise and fall, demonstrating the PLL's ability to track the input frequency changes.

4. **Key Features and Technical Details:**
- The output voltage \( V_o \) shows an exponential rise when the input frequency increases and an exponential decay when it decreases.
- The time constant \( \tau \) is given as \( \frac{1}{K_v} = 2 \text{ ms} \).
- The voltage change \( V \) is calculated as \( \frac{\omega_i - \omega_o}{K_O} \), with specific values annotated as 0.5 V and 0.25 V for different frequency changes.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for the input frequencies at \( \omega_i = 2\pi(500 \text{ Hz}) \), \( \omega_i = 2\pi(1 \text{ kHz}) \), and \( \omega_i = 2\pi(250 \text{ Hz}) \).
- Specific voltage values are marked for the output voltage response, showing how the PLL adjusts to maintain lock with the input frequency changes.

Parameters for example:
$\omega_{o}=$ Oscillator free-run frequency $=500 \mathrm{~Hz}$
$K_{O}=1 \mathrm{kHz} / \mathrm{V}$
$K_{v}=500 \mathrm{~s}^{-1}$
(b)

Figure 10.16 (a) Root locus and frequency response of a first-order, phase-locked loop. (b) Response of the loop output voltage to step changes in input frequency, example first-order loop.

#### EXAMPLE

A PLL has a $K_{O}$ of $2 \pi(1 \mathrm{kHz} / \mathrm{V})$, a $K_{v}$ of $500 \mathrm{~s}^{-1}$, and a free-running frequency of 500 Hz .
(a) For a constant input signal frequency of 250 Hz and 1 kHz , find $V_{o}$.

$$
V_{o}=\frac{\omega_{i}-\omega_{o}}{K_{O}}
$$

where

$$
\omega_{o}=\text { oscillator free-running frequency }
$$

At 250 Hz

$$
V_{o}=\frac{2 \pi(250 \mathrm{~Hz})-2 \pi(500 \mathrm{~Hz})}{2 \pi(1 \mathrm{kHz} / \mathrm{V})}=-0.25 \mathrm{~V}
$$

At 1 kHz

$$
V_{o}=\frac{2 \pi(1 \mathrm{kHz})-2 \pi(500 \mathrm{~Hz})}{2 \pi(1 \mathrm{kHz} / \mathrm{V})}=+0.5 \mathrm{~V}
$$

(b) Now the input signal is frequency modulated, so that

$$
\omega_{i}(t)=(2 \pi) 500 \mathrm{~Hz}\left[1+0.1 \sin \left(2 \pi \times 10^{2}\right) t\right]
$$

Find the output signal $V_{o}(t)$. From (10.51) we have

$$
\begin{aligned}
\frac{V_{o}(j \omega)}{\omega_{i}(j \omega)} & =\frac{1}{K_{O}}\left(\frac{K_{v}}{K_{v}+j \omega}\right)=\frac{1}{K_{O}}\left[\frac{K_{v}}{K_{v}+j\left(2 \pi \times 10^{2}\right)}\right] \\
& =\frac{1}{2 \pi(1 \mathrm{kHz} / \mathrm{V})}\left(\frac{500}{500+j 628}\right) \\
& =\frac{1}{2 \pi(1 \mathrm{kHz} / \mathrm{V})}(0.39-j 0.48)
\end{aligned}
$$

The magnitude of $\omega_{i}(j \omega)$ is

$$
\left|\omega_{i}(j \omega)\right|=(0.1)(500 \mathrm{~Hz})(2 \pi)=(50)(2 \pi)
$$

Therefore

$$
V_{o}(j \omega)=\frac{50 \mathrm{~Hz}}{1 \mathrm{kHz}}(0.39-j 0.48)=\frac{50}{1000}\left(0.62 \angle-51^{\circ}\right)
$$

and

$$
V_{o}(t)=0.031 \sin \left[\left(2 \pi \times 10^{2} t\right)-51^{\circ}\right]
$$

Operating the loop with no loop filter has several practical drawbacks. Since the phase detector is really a multiplier, it produces a sum frequency component at its output as well as the difference frequency component. This component at twice the carrier frequency will be fed directly to the output if there is no loop filter. Also, all the out-of-band interfering signals present at the input will appear, shifted in frequency, at the output. Thus, a loop filter is very desirable in applications where interfering signals are present.

The most common configuration for integrated circuit PLLs is the second-order loop. Here, loop filter $F(s)$ is simply a single-pole, low-pass filter, usually realized with a single
image_name:Single-pole loop filter
description:
[
name: R, type: Resistor, value: R, ports: {N1: Vin, N2: X1}
name: C, type: Capacitor, value: C, ports: {Np: X1, Nn: GND}
]
extrainfo:The circuit is a single-pole loop filter consisting of a resistor and a capacitor. The cutoff frequency is given by \( \omega_1 = \frac{1}{RC} \). The diagram includes root locus and closed-loop response plots, indicating stability and frequency response characteristics.
image_name:Root locus
description:The provided graph is a root locus diagram for a second-order phase-locked loop (PLL) system. It is accompanied by a closed-loop frequency response graph. Here's a detailed analysis:

Root Locus Diagram:
1. **Type of Graph:**
- This is a root locus plot, which is used to analyze the stability of control systems as a parameter (here, likely the loop gain) is varied.

2. **Axes Labels and Units:**
- **Horizontal Axis (σ):** Represents the real part of the complex plane.
- **Vertical Axis (jω):** Represents the imaginary part of the complex plane.

3. **Overall Behavior and Trends:**
- The plot illustrates the trajectory of the system's poles in the complex plane as the gain is varied.
- The root locus starts at the poles of the open-loop transfer function and moves towards the zeros as the gain increases.

4. **Key Features and Technical Details:**
- There are two poles marked on the real axis at \(-\omega_1\) and \(-\frac{\omega_1}{2}\).
- As the gain increases, the poles move along the indicated paths, which may include crossing into the right half-plane, indicating potential instability.
- The dashed line and arrows indicate the direction of movement of the poles.

5. **Annotations and Specific Data Points:**
- The plot is annotated with the pole locations and the direction of movement as gain increases.

Closed-Loop Frequency Response:
1. **Type of Graph:**
- A closed-loop frequency response plot is shown, typically used to illustrate the magnitude response of the system.

2. **Axes Labels and Units:**
- **Horizontal Axis (ω):** Frequency in radians per second, plotted on a logarithmic scale.
- **Vertical Axis (|V_o/ω_i(jω)|):** Magnitude of the frequency response, also on a logarithmic scale.

3. **Overall Behavior and Trends:**
- The frequency response shows a flat region at low frequencies, indicating stable gain.
- There is a peak at a frequency near \(K_v\), indicating a resonance or bandwidth limit.
- Beyond this peak, the response rolls off, indicating attenuation of higher frequencies.

4. **Key Features and Technical Details:**
- The flat region at low frequencies corresponds to a gain of \(\frac{1}{K_O}\).
- The peak in the response suggests a resonant frequency, which is a critical point for system stability and performance.

5. **Annotations and Specific Data Points:**
- The frequency \(\sim K_v\) is marked to indicate the location of the peak in the frequency response.
- The gain level \(\frac{1}{K_O}\) is annotated on the plot.
image_name:Closed-loop response
description:The graph titled "Closed-loop response" is a Bode plot, which represents the frequency response of a second-order phase-locked loop (PLL). This plot is shown on a logarithmic scale for both the frequency (x-axis) and the magnitude (y-axis).

1. **Type of Graph and Function:**
- This is a Bode plot, which is commonly used to display the frequency response of a system.

2. **Axes Labels and Units:**
- The x-axis represents frequency (ω) on a logarithmic scale.
- The y-axis represents the magnitude of the closed-loop transfer function \( \left| \frac{V_o}{\omega_i}(j\omega) \right| \) also on a logarithmic scale.

3. **Overall Behavior and Trends:**
- The graph shows an initial flat response at lower frequencies, indicating a constant gain.
- As frequency increases, there is a peak, suggesting a resonant frequency or gain peak around \( \sim K_v \).
- After the peak, the magnitude decreases sharply, indicating a roll-off, which is characteristic of a low-pass filter behavior.

4. **Key Features and Technical Details:**
- The magnitude starts at \( \frac{1}{K_O} \) at low frequencies, which is the DC gain of the system.
- The peak near \( \sim K_v \) is a critical point that indicates the system's resonant frequency.
- The roll-off after the peak shows the bandwidth of the system and the effectiveness of the loop filter in attenuating high-frequency signals.

5. **Annotations and Specific Data Points:**
- There is a dotted vertical line marking the frequency \( \sim K_v \), which is significant as it represents the frequency where the gain starts to decrease.
- The plot effectively demonstrates the filtering properties of the PLL, showing how it maintains stability while attenuating out-of-band signals.

Figure 10.17 Root locus and frequency response of second-order, phase-locked loop.
resistor and capacitor. Thus

$$
\begin{equation*}
F(s)=\left(\frac{1}{1+\frac{s}{\omega_{1}}}\right) \tag{10.53}
\end{equation*}
$$

By substituting into (10.50), the transfer function becomes

$$
\begin{equation*}
\frac{V_{o}}{\omega_{1}}(s)=\frac{1}{K_{O}}\left(\frac{1}{1+\frac{s}{K_{v}}+\frac{s^{2}}{\omega_{1} K_{v}}}\right) \tag{10.54}
\end{equation*}
$$

The root locus for this feedback system as $K_{v}$ varies is shown in Fig. 10.17, along with the corresponding frequency response. The roots of the transfer function are

$$
\begin{equation*}
s=-\frac{\omega_{1}}{2}\left(1 \pm \sqrt{1-\frac{4 K_{v}}{\omega_{1}}}\right) \tag{10.55}
\end{equation*}
$$

Equation 10.54 can be expressed as

$$
\begin{equation*}
\frac{V_{o}}{\omega_{i}}=\frac{1}{K_{O}}\left(\frac{1}{\frac{s^{2}}{\omega_{n}^{2}}+\frac{2 \zeta}{\omega_{n}} s+1}\right) \tag{10.56}
\end{equation*}
$$

where

$$
\begin{align*}
\omega_{n} & =\sqrt{K_{v} \omega_{1}}  \tag{10.57}\\
\zeta & =\frac{1}{2} \sqrt{\frac{\omega_{1}}{K_{v}}} \tag{10.58}
\end{align*}
$$

The basic factor setting the loop bandwidth is $K_{v}$ as in the first-order case. The magnitude $\omega_{1}$ of the additional pole is then made as low as possible without causing an unacceptable amount of peaking in the frequency response. This peaking is of concern both because it distorts the demodulated FM output and because it causes the loop to ring, or experience a poorly damped oscillatory response, when a transient disturbs the loop. A good compromise is using a maximally flat low-pass pole configuration in which the poles are placed on radials angled $45^{\circ}$ from the negative real axis. For this response, the damping factor $\zeta$ should be equal to $1 / \sqrt{2}$. Thus

$$
\begin{equation*}
\frac{1}{\sqrt{2}}=\frac{1}{2} \sqrt{\frac{\omega_{1}}{K_{v}}} \tag{10.59}
\end{equation*}
$$

and

$$
\begin{equation*}
\omega_{1}=2 K_{v} \tag{10.60}
\end{equation*}
$$

The $-3-\mathrm{dB}$ frequency of the transfer function $\left(V_{o} / \omega_{i}\right)(j \omega)$ is then

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}}=\omega_{n}=\sqrt{K_{v} \omega_{1}}=\sqrt{2} K_{v} \tag{10.61}
\end{equation*}
$$

A disadvantage of the second-order loop as discussed thus far is that the $-3-\mathrm{dB}$ bandwidth of the loop is basically dictated by loop gain $K_{v}$ as shown by (10.61). As we will show, the loop gain also sets the lock range, so that with the simple filter used above these two parameters are constrained to be comparable. Situations do arise in phase-locked communications in which a wide lock range is desired for tracking large signal-frequency variations, yet a narrow loop bandwidth is desired for rejecting out-of-band signals. Using a very small $\omega_{1}$ would accomplish this were it not for the fact that this produces underdamped loop response. By adding a zero to the loop filter, the loop filter pole can be made small while still maintaining good loop dampening.

The effect of the addition of a zero on the loop response is best seen by examining the open-loop response of the circuit. Shown in Fig. $10.18 a$ is the open-loop response of the circuit with no loop filter. Because of the integration inherent in the loop, the response has a $-20-\mathrm{dB} /$ decade slope throughout the frequency range and crosses unity gain at $K_{v}$. In Fig. $10.18 b$, a loop filter in which $\omega_{1}$ is much less than $K_{v}$ has been added, and, as a result, the loop
image_name:Figure 10.18 (a)
description:The graph in Figure 10.18 (a) is a Bode plot illustrating the open-loop response of a Phase-Locked Loop (PLL) circuit without a loop filter. It consists of two separate plots: the magnitude plot and the phase plot.

1. **Type of Graph and Function:**
- The graph is a Bode plot, which is used to represent the frequency response of a system. It includes a magnitude plot and a phase plot.

2. **Axes Labels and Units:**
- The horizontal axis for both plots represents frequency, denoted by \( \omega \), and is on a logarithmic scale.
- The vertical axis of the magnitude plot represents the loop gain, also on a logarithmic scale, with a reference level of 1 (or 0 dB).
- The vertical axis of the phase plot represents phase in degrees, ranging from 0° to -180°.

3. **Overall Behavior and Trends:**
- In the magnitude plot, the loop gain decreases linearly with frequency, indicating a -20 dB/decade slope. This is characteristic of a first-order system with integral action.
- The phase plot shows a constant phase shift of -90° across all frequencies, typical of a system with a pure integrator.

4. **Key Features and Technical Details:**
- The unity gain crossover frequency, where the magnitude plot crosses the 0 dB line, is marked as \( K_v \).
- There are no peaks or valleys in either the magnitude or phase plots, indicating a straightforward integrative response without additional dynamics.

5. **Annotations and Specific Data Points:**
- The magnitude plot is annotated with a marker at the unity gain frequency \( K_v \).
- The phase plot maintains a constant -90° line, demonstrating the integrative nature of the system without any phase lead or lag introduced by additional components.

Figure 10.18 (a) PLL open-loop response with no loop filter.
image_name:Figure 10.18 (b)
description:The graph in Figure 10.18 (b) is a Bode plot representing the open-loop response of a Phase-Locked Loop (PLL) with a single-pole filter. This plot consists of two separate graphs: a magnitude plot and a phase plot.

1. **Type of Graph and Function:**
- The graph is a Bode plot, which is used to describe the frequency response of a system.
- It shows the behavior of the PLL with a single-pole filter.

2. **Axes Labels and Units:**
- The horizontal axis for both plots represents frequency (ω) on a logarithmic scale.
- The vertical axis of the magnitude plot represents loop gain, also on a logarithmic scale.
- The vertical axis of the phase plot represents phase in degrees.

3. **Overall Behavior and Trends:**
- **Magnitude Plot:**
- The loop gain starts at a high value at low frequencies and decreases linearly on a logarithmic scale as frequency increases.
- There is a distinct crossover frequency where the gain crosses the unity level (0 dB).
- **Phase Plot:**
- The phase starts at 0° and drops to -90° as frequency increases, indicating the integrative nature of the system.
- The phase remains constant at -90° after the initial drop.

4. **Key Features and Technical Details:**
- **Magnitude Plot:**
- The crossover frequency is marked, indicating where the loop gain equals one (unity gain frequency \( K_v \)).
- The presence of a single pole is evident from the slope of the magnitude plot.
- **Phase Plot:**
- The phase plot shows a consistent -90° line, reflecting the single-pole filter's effect without additional phase shift components.

5. **Annotations and Specific Data Points:**
- The magnitude plot includes annotations such as the crossover frequency and the unity gain frequency \( K_v \).
- The phase plot maintains a clear -90° line, demonstrating the consistent phase behavior of the system.
image_name:Figure 10.18 (c)
description:**Type of Graph and Function:**
The graph is a Bode plot, which includes both magnitude and phase plots. It represents the open-loop response of a Phase-Locked Loop (PLL) with a single-pole-single-zero loop filter.

**Axes Labels and Units:**
- The x-axis represents frequency (ω) on a logarithmic scale.
- The y-axis for the magnitude plot is labeled "Loop gain" with no specific units, also on a logarithmic scale.
- The y-axis for the phase plot is labeled "Phase" in degrees.

**Overall Behavior and Trends:**
- In the magnitude plot, the loop gain initially decreases with frequency. This decrease is linear on the logarithmic scale until it approaches the unity gain frequency (K_v).
- A zero is introduced at frequency ω_2, causing a change in the slope of the magnitude plot, flattening it slightly as it approaches the crossover frequency.
- In the phase plot, the phase begins at 0°, drops towards -90°, and shows a dip near -180° as it approaches ω_2, before stabilizing back towards -90°.

**Key Features and Technical Details:**
- The magnitude plot shows a crossover at the unity gain frequency, K_v, where the gain is 1.
- The introduction of a zero at ω_2 creates a noticeable change in the phase response, improving the phase margin at the crossover frequency.
- The phase plot has significant points at -90° and -180°, indicating the impact of the zero in the loop filter.

**Annotations and Specific Data Points:**
- The crossover frequency is marked on both the magnitude and phase plots.
- ω_1 and ω_2 are indicated on the magnitude plot, showing the locations of the pole and zero, respectively.

Figure 10.18 (b) PLL open-loop response with a single-pole filter and $\omega_{1} \ll K_{v}$.

Figure 10.18 (c) PLL open-loop response with a zero added in loop filter at $s=-\omega_{2}$.
phase shift is very nearly $180^{\circ}$ at the crossover frequency. The result is a sharp peak in the closed-loop frequency response at the crossover frequency. By adding a zero in the loop filter at $\omega_{2}$, as shown in Fig. 10.18c, the loop phase margin can be greatly improved. Note that for this case the loop bandwidth, which is equal to the crossover frequency, is much lower than $K_{v}$. This ability to set loop bandwidth and $K_{\nu}$ independently is an advantage of this type of loop filter. An R-C circuit that provides the necessary pole and zero in the filter response is shown in Fig. 10.18d. The root locus for this loop filter and the resulting closed-loop response are also shown.

Loop Lock Range. The loop lock range is the range of input frequencies about the center frequency for which the loop maintains lock. In most cases, it is limited by the fact that the phase comparator has a limited phase comparison range; once the phase difference between
image_name:Figure 10.18 (d)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: 1, N2: 2}
name: R2, type: Resistor, value: R2, ports: {N1: 3, N2: 4}
name: C, type: Capacitor, value: C, ports: {Np: 2, Nn: 3}
]
extrainfo:The circuit is a single-pole, single-zero loop filter. It includes the transfer function F(s) with a zero at ω2 = 1/(CR2) and a pole at ω1 = 1/(C(R1 + R2)). The root locus diagram and closed-loop response are shown for the filter with a large loop gain.
image_name:Root locus
description:The diagram in Figure 10.18(d) consists of two main components: the root locus plot and the closed-loop frequency response of a second-order Phase-Locked Loop (PLL) with a zero.

Root Locus Plot
1. **Type of Graph:**
- This is a root locus plot, which illustrates the paths of the poles of a control system as a system parameter (typically gain) is varied.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \( \sigma \), representing the real part of the complex frequency (damping).
- The vertical axis is labeled \( j\omega \), representing the imaginary part of the complex frequency (oscillation frequency).

3. **Overall Behavior and Trends:**
- The root locus begins at the open-loop poles and moves towards the open-loop zeros as the gain increases.
- The plot shows a single zero at \(-\omega_2\) and a single pole at \(-\omega_1\), indicating a single-pole, single-zero loop filter.
- The locus path is shown moving from the pole at \(-\omega_1\) towards the zero at \(-\omega_2\).

4. **Key Features and Technical Details:**
- Closed-loop poles are indicated along the locus path.
- The path is semi-circular, indicating a transition from stability to potential instability as gain increases.

Closed-Loop Frequency Response
1. **Type of Graph:**
- This is a frequency response plot on a logarithmic scale, showing the magnitude of the transfer function versus frequency.

2. **Axes Labels and Units:**
- The horizontal axis is \( \omega \), representing angular frequency.
- The vertical axis is \( \frac{V_o}{\omega_i}(j\omega) \), representing the magnitude of the output to input frequency ratio.

3. **Overall Behavior and Trends:**
- The plot shows a flat response at low frequencies, indicating stable gain.
- There is a roll-off at higher frequencies, typical of low-pass filter behavior.

4. **Key Features and Technical Details:**
- The -3dB point is approximated at \( \omega_{-3dB} \approx K_v \left(\frac{\omega_1}{\omega_2}\right) \), where the gain drops to \( \frac{1}{K_o} \).
- The transition from the flat response to the roll-off is a critical point for determining bandwidth and stability.

Overall, this diagram illustrates the behavior of a second-order PLL with a single zero, showing both the root locus for stability analysis and the frequency response for performance evaluation.
image_name:Closed-loop response
description:The graph titled "Closed-loop response" is a frequency response plot, displayed on logarithmic scales. It represents the behavior of a second-order phase-locked loop (PLL) with a zero, specifically showing how the output-to-input frequency ratio \( \frac{V_o}{\omega_i} \) changes with frequency \( \omega \).

Axes Labels and Units:
- **Horizontal Axis (\( \omega \))**: Represents frequency, likely in radians per second, given the context of the root locus and PLL design.
- **Vertical Axis (\( \frac{V_o}{\omega_i}(j\omega) \))**: Represents the magnitude of the frequency response, depicted on a logarithmic scale.

Overall Behavior and Trends:
- The graph shows a typical low-pass filter response with an initial flat region followed by a roll-off.
- At lower frequencies, the response is flat, indicating that the output follows the input closely, maintaining a constant ratio.
- As frequency increases, the response begins to decline, marking the onset of the filter's roll-off region.

Key Features and Technical Details:
- The plot has a distinct cutoff point indicated by the \(-3 \text{dB}\) point, which is approximately \( \omega_{-3dB} \approx K_v \left( \frac{\omega_1}{\omega_2} \right) \).
- The magnitude at low frequencies is inversely proportional to the loop gain \( \frac{1}{K_o} \), showing how gain affects the steady-state response.

Annotations and Specific Data Points:
- The cutoff frequency \( \omega_{-3dB} \) is a critical point marked on the graph, signifying the frequency beyond which the output starts to significantly attenuate.
- The plot does not show specific numerical values for \( K_o \), \( \omega_1 \), or \( \omega_2 \), but these are crucial for determining the exact shape and characteristics of the response.

This graph is essential for understanding the frequency response characteristics of the PLL system with a second-order filter, emphasizing how the loop's gain and the pole-zero placement affect its ability to maintain lock across varying frequencies.

Figure 10.18 (d) Root locus and frequency response of a second-order PLL with a zero. Frequency response shown is for large loop gain such that poles are located as shown in the root locus.
the input signal and the VCO output reaches some critical value, the phase comparator ceases to behave linearly. The transfer characteristic of a typical analog phase comparator is shown in Fig. 10.12. It is clear from this figure that in order to maintain lock, the phase difference between the VCO output and the incoming signal must be kept between zero and $\pi$. If the phase difference is equal to either zero or $\pi$, then the magnitude of the dc voltage at the output of the phase comparator is

$$
\begin{equation*}
V_{o(\max )}= \pm K_{D}\left(\frac{\pi}{2}\right) \tag{10.62}
\end{equation*}
$$

This dc voltage is amplified by the electrical gain $A$, and the result is applied to the VCO input, producing a frequency shift away from the free-running center frequency of

$$
\begin{equation*}
\Delta \omega_{\mathrm{osc}}=K_{D} A K_{O}\left(\frac{\pi}{2}\right)=\left(\frac{K_{v} \pi}{2}\right) \tag{10.63}
\end{equation*}
$$

If the input frequency is now shifted away from the free-running frequency, more voltage will have to be applied to the VCO in order for the VCO frequency to shift accordingly. However, the phase detector can produce no more dc output voltage to shift the VCO frequency further,
image_name:Figure 10.19 PLL output versus frequency of input
description:The graph in Figure 10.19 is a piecewise linear plot showing the output voltage (V_out) of a Phase-Locked Loop (PLL) as a function of the input frequency (f_in). The graph is divided into sections indicating different frequency ranges and their effects on the PLL output.

1. **Type of Graph and Function:**
- The graph is a piecewise linear function displaying the relationship between PLL output voltage and input frequency.

2. **Axes Labels and Units:**
- The vertical axis represents the output voltage (V_out) of the PLL.
- The horizontal axis represents the input frequency (f_in).
- Both axes use a linear scale, but specific units are not labeled.

3. **Overall Behavior and Trends:**
- The graph shows a series of linear segments with both positive and negative slopes.
- As input frequency increases from the center frequency, the output voltage increases linearly until it reaches a peak and then decreases sharply.
- The pattern repeats symmetrically on either side of the center frequency, indicating periodic behavior.

4. **Key Features and Technical Details:**
- The graph includes two critical frequency ranges labeled as 2ω_L and 2ω_C.
- The range 2ω_L represents the lock range of the PLL, where the loop can maintain lock with the input frequency.
- The range 2ω_C indicates the capture range, beyond which the PLL cannot acquire lock.
- Each linear segment represents a stable phase relationship maintained by the PLL within the lock range.

5. **Annotations and Specific Data Points:**
- The graph includes arrows indicating the direction of frequency change and phase adjustments within each linear segment.
- A magnified section shows a triangular waveform, emphasizing the repetitive nature of the phase adjustments within the lock range.
- The graph's symmetry around the center frequency suggests balanced performance for both increasing and decreasing frequency shifts.

Overall, the graph illustrates how the PLL output voltage varies with input frequency, highlighting the lock and capture ranges essential for PLL operation.

Figure 10.19 PLL output versus frequency of input.
so the loop will lose lock. The lock range $\omega_{L}$ is then given by

$$
\begin{equation*}
\omega_{L}=K_{v} \frac{\pi}{2} \tag{10.64}
\end{equation*}
$$

This is the frequency range on either side of the free-running frequency for which the loop will track input frequency variations. It is a parameter that depends only on the dc gain in the loop and is independent of the properties of the loop filter. Other types ${ }^{6}$ of phase detectors can give larger linear ranges of phase-comparator operation.

The capture range is the range of input frequencies for which the initially unlocked loop will lock on an input signal when initially in an unlocked condition and is always less than the lock range. When the input frequency is swept through a range around the center frequency, the output voltage as a function of input frequency displays a hysteresis effect, as shown in Fig. 10.19. As discussed earlier, the capture range is difficult to predict analytically. As a very rough rule of thumb, the approximate capture range can be estimated using the following procedure: Refer to Fig. 10.13 and assume that the loop is opened at the loop-amplifier output and that a signal with a frequency not equal to the free-running VCO frequency is applied at the input of the PLL. The sinusoidal difference frequency component that appears at the output of the phase detector has the value

$$
\begin{equation*}
V_{p}(t)=\frac{\pi}{2} K_{D} \cos \left(\omega_{i}-\omega_{\mathrm{osc}}\right) t \tag{10.65}
\end{equation*}
$$

where $\omega_{i}$ is the input signal frequency and $\omega_{\text {osc }}$ is the VCO free-running frequency. This component is passed through the loop filter, and the output from the loop amplifier resulting
from this component is

$$
\begin{equation*}
V_{o}(t)=\frac{\pi}{2} K_{D} A\left|F\left[j\left(\omega_{i}-\omega_{\mathrm{osc}}\right)\right]\right| \cos \left[\left(\omega_{i}-\omega_{\mathrm{osc}}\right) t+\phi\right] \tag{10.66}
\end{equation*}
$$

where

$$
\phi=\angle F\left[j\left(\omega_{i}-\omega_{\mathrm{osc}}\right)\right]
$$

The output from the loop amplifier thus consists of a sinusoid at the difference frequency whose amplitude is reduced by the loop filter. In order for capture to occur, the magnitude of the voltage that must be applied to the VCO input is

$$
\begin{equation*}
\left|V_{\mathrm{osc}}\right|=\frac{\omega_{i}-\omega_{\mathrm{osc}}}{K_{O}} \tag{10.67}
\end{equation*}
$$

The capture process itself is rather complex, but the capture range can be estimated by setting the magnitudes of (10.66) and (10.67) equal. The result is that capture is likely to occur if the following inequality is satisfied:

$$
\begin{equation*}
\left|\left(\omega_{i}-\omega_{\mathrm{osc}}\right)\right|<\frac{\pi}{2} K_{D} K_{O} A\left|F\left[j\left(\omega_{i}-\omega_{\mathrm{osc}}\right)\right]\right| \tag{10.68}
\end{equation*}
$$

This equation implicitly gives an estimation of the capture range. For the first-order loop, where $F(s)$ is unity, it predicts that the lock range and capture range are approximately equal, and that for the second-order loop the capture range is significantly less than the lock range because $\left|F\left[j\left(\omega_{i}-\omega_{\text {oss }}\right)\right]\right|$ is then less than unity.

### 10.3.3 Integrated-Circuit Phase-Locked Loops

The principal reason that PLLs have come to be widely used as system components is that the elements of the phase-locked loop are particularly suited to monolithic construction, and complete PLL systems can be fabricated on a single chip. We now discuss the design of the individual PLL components.

Phase Detector. Phase detectors for monolithic PLL applications are generally of the Gilbert multiplier configuration shown in Fig. 10.4. As illustrated in Fig. 10.11, if two signals large enough in amplitude to cause limiting in the emitter-coupled pairs making up the circuit are applied to the two inputs, the output will contain a dc component given by

$$
\begin{equation*}
V_{\text {average }}=-I_{E E} R_{C}\left(1-\frac{2 \phi}{\pi}\right) \tag{10.69}
\end{equation*}
$$

where $\phi$ is the phase difference between the input signals. An important aspect of the performance of this phase detector is that if the amplitude of the applied signal at $V_{\mathrm{in} 2}$ is small compared to the thermal voltage $V_{T}$, the circuit behaves as a balanced modulator, and the dc compartment of the output depends on the amplitude of the low-level input. The output waveform is then a sinusoid multiplied by a synchronous square wave, as shown in Fig. 10.20. In the limiting case when the small input is small compared to $V_{T}$, the dc component in the output becomes, referring to Fig. 10.20,

$$
\begin{align*}
V_{\text {average }} & =\frac{1}{\pi} g_{m} R_{C} V_{i}\left[\int_{0}^{\phi}(\sin \omega t) d(\omega t)-\int_{\phi}^{\pi}(\sin \omega t) d(\omega t)\right]  \tag{10.70}\\
& =-\frac{2 g_{m} R_{C} V_{i} \cos \phi}{\pi} \tag{10.71}
\end{align*}
$$

image_name:Figure 10.20
description:**Type of Graph and Function:**\nThe graph is a time-domain waveform depicting a sinusoidal function.\n\n**Axes Labels and Units:**\n- The horizontal axis is labeled as \( \omega t \), representing the angular frequency multiplied by time, which is typically dimensionless.\n- The vertical axis is labeled as \( V_{\text{in2}} \), representing the input voltage in volts.\n\n**Overall Behavior and Trends:**\nThe graph shows a sinusoidal waveform, characterized by a smooth, periodic oscillation. This sinusoid starts from zero, rises to a positive peak, descends back through zero to a negative peak, and returns to zero, completing one full cycle. The waveform is symmetrical about the horizontal axis, indicating equal positive and negative amplitudes.\n\n**Key Features and Technical Details:**\n- The sinusoidal function is represented by \( V_i \sin \omega t \), where \( V_i \) is the amplitude of the sine wave.\n- The waveform exhibits periodic behavior, with regular intervals between peaks and zero crossings.\n- The maximum and minimum points (peaks) of the waveform correspond to the amplitude \( V_i \), denoting the highest positive and lowest negative voltages reached.\n- Zero crossings occur at regular intervals, indicating points where the waveform changes polarity.\n\n**Annotations and Specific Data Points:**\n- The graph is annotated with the expression \( V_i \sin \omega t \) along the curve, indicating the mathematical form of the sinusoidal function.\n- No specific numerical values are provided for the amplitude or frequency, but the general sinusoidal shape is clearly depicted.

image_name:Figure 10.20 Sinusoid multiplied by a synchronous square wave
description:The graph in Figure 10.20 depicts two waveforms plotted against time (\( \omega t \)). The top waveform is a synchronous square wave, labeled \( V_{in1} \), and the bottom waveform is a sinusoidal wave, labeled \( V_o \). Both waveforms share the same time axis, \( \omega t \).

1. **Type of Graph and Function:**
- The graph is a time-domain waveform representation.
- It shows the interaction of a sinusoidal wave with a synchronous square wave.

2. **Axes Labels and Units:**
- The horizontal axis represents time, denoted as \( \omega t \), where \( \omega \) is the angular frequency.
- The vertical axis for the top waveform is labeled \( V_{in1} \), and for the bottom waveform, it is labeled \( V_o \). No specific units are provided, indicating a general representation of voltage.

3. **Overall Behavior and Trends:**
- The top waveform is a square wave alternating between high and low states with a constant period.
- The bottom waveform is a sinusoidal wave showing regular oscillations with a consistent amplitude and period.
- The sinusoidal wave \( V_o \) appears to be modulated by the square wave \( V_{in1} \), as indicated by the phase shift \( \phi \).

4. **Key Features and Technical Details:**
- The square wave \( V_{in1} \) has a duty cycle that appears to be 50%, with equal time spent in the high and low states.
- The sinusoidal wave \( V_o \) maintains its sinusoidal shape but is influenced by the phase \( \phi \), which is marked on the graph.
- Zero crossings of the sinusoidal wave occur at regular intervals, indicating consistent periodicity.

5. **Annotations and Specific Data Points:**
- The phase shift \( \phi \) is annotated on both waveforms, indicating the time difference between the square wave transition and the sinusoidal wave's zero crossing.
- There are no specific numerical values for amplitude, frequency, or phase shift, but the general behavior and interaction of the waveforms are clearly depicted.

Figure 10.20 Sinusoid multiplied by a synchronous square wave.
where $R_{C}$ is the collector resistor in the Gilbert multiplier and $g_{m}$ is the transconductance of the transistors. The phase detector output voltage then becomes proportional to the amplitude $V_{i}$ of the incoming signal, and if the signal amplitude varies, then the loop gain of the phaselocked loop changes. Thus when the signal amplitude varies, it is often necessary to precede the phase detector with an amplifier/limiter to avoid this problem. In FM demodulators, for example, any amplitude modulation appearing on the incoming frequency-modulated signal will be demodulated, producing an erroneous output.

In PLL applications the frequency response of the phase detector is usually not the limiting factor in the usable operating frequency range of the loop itself. At high operating frequencies, the parasitic capacitances of the devices result in a feedthrough of the carrier frequency, giving an erroneous component in the output at the center frequency. This component is removed by the loop filter, however, and does not greatly affect loop performance. The VCO is usually the limiting factor in the operating frequency range.

Voltage-Controlled Oscillator. The operating frequency range, FM distortion, centerfrequency drift, and center-frequency supply-voltage sensitivity are all determined by the performance of the VCO. Integrated-circuit VCOs often are simply R-C multivibrators in which the charging current in the capacitor is varied in response to the control input. We first consider the emitter-coupled multivibrator as shown in Fig. 10.21a, which is typical of those
image_name:(a)
description:The circuit is a voltage-controlled, emitter-coupled multivibrator used in VCO applications. It consists of multiple NPN transistors, resistors, capacitors, and current sources.

Figure 10.21 (a) Voltagecontrolled, emitter-coupled multivibrator.
image_name:The circuit is a voltage-controlled, emitter-coupled multivibrator used in VCO applications. It consists of multiple NPN transistors, resistors, capacitors, and current sources. The circuit operates by alternately turning on and off transistors Q1 and Q2, creating a square wave output at Vout. Diodes Q5 and Q6 help in maintaining the voltage levels required to switch the transistors. The capacitors and resistors determine the timing characteristics of the multivibrator.

Figure 10.21 (b) Equivalent circuit during one half-cycle.
used in this application. We calculate the period by first assuming that $Q_{1}$ is turned off and $Q_{2}$ is turned on. The circuit then appears as shown in Fig. 10.21b. We assume that current $I$ is large so that the voltage drop $I R$ is large enough to turn on diode $Q_{6}$. Thus the base of $Q_{4}$ is one diode drop below $V_{C C}$, the emitter is two diode drops below $V_{C C}$, and the base of $Q_{1}$ is two diode drops below $V_{C C}$. If we can neglect the base current of $Q_{3}$, its base is at $V_{C C}$ and its
image_name:Voltage at base of Q2 (Vb2)
description:The graph titled "Voltage at base of Q2 (Vb2)" is a time-domain waveform illustrating the voltage changes at the base of transistor Q2 over time. The horizontal axis represents time (t), while the vertical axis represents voltage levels in relation to V_CC, the supply voltage.

Axes Labels and Units:
- **Horizontal Axis (t):** Represents time, likely in arbitrary units as no specific time unit is given.
- **Vertical Axis (Voltage):** Shows voltage levels with respect to V_CC, specifically marking V_CC, V_CC - 0.6V, and V_CC - 1.2V.

Overall Behavior and Trends:
- The waveform is a rectangular pulse train, oscillating between two voltage levels: V_CC - 0.6V and V_CC - 1.2V.
- The waveform indicates a periodic behavior, with the voltage at the base of Q2 switching between these levels as Q2 turns on and off.

Key Features and Technical Details:
- **When Q2 is on:** The voltage is at V_CC - 0.6V.
- **When Q1 is on:** The voltage drops to V_CC - 1.2V.
- This transition between states is sharp and occurs at regular intervals, suggesting a stable oscillation.

Annotations and Specific Data Points:
- The graph is annotated to indicate the on-states of Q2 and Q1, with Q2 being on when the voltage is at V_CC - 0.6V and Q1 being on when the voltage is at V_CC - 1.2V.
- The periodicity of the waveform is visually marked by vertical dashed lines, indicating the duration of each state.

Overall, the graph depicts a clear, periodic switching behavior in the emitter-coupled multivibrator circuit, showing how the base voltage of Q2 changes in response to the on/off states of transistors Q1 and Q2.
image_name:Voltage at emitter of Q2 (Ve2)
description:The graph titled "Voltage at emitter of Q2 (Ve2)" is a time-domain waveform. The horizontal axis represents time (t), and the vertical axis represents voltage, specifically the voltage at the emitter of Q2, denoted as Ve2. The voltage is measured relative to V_CC, the supply voltage.

**Axes Labels and Units:**
- **Horizontal Axis (t):** Represents time, though specific units are not provided.
- **Vertical Axis (Ve2):** Represents voltage, with key reference levels labeled as V_CC, V_CC - 1.2, and V_CC - 1.8 volts.

**Overall Behavior and Trends:**
The waveform shows a periodic pattern with distinct linear segments. The voltage at the emitter of Q2 alternates between two levels:
- A high level at V_CC - 1.2 volts.
- A low level at V_CC - 1.8 volts.

The waveform begins at the high level (V_CC - 1.2 volts) and then linearly decreases to the low level (V_CC - 1.8 volts), after which it abruptly returns to the high level and the cycle repeats. This behavior suggests a sawtooth-like waveform with a linear decline and sudden reset.

**Key Features and Technical Details:**
- **Initial Voltage Level:** Starts at V_CC - 1.2 volts.
- **Minimum Voltage Level:** Drops to V_CC - 1.8 volts.
- **Transition Points:** The transitions between these voltage levels are sharp, indicating a rapid change in state, likely due to the switching action of transistors in the circuit.

**Annotations and Specific Data Points:**
- The graph is annotated with the states of transistors Q1 and Q2, indicating which transistor is on during specific intervals. When Q2 is on, the voltage is at the high level, and when Q1 is on, the voltage is at the low level.
- The periodicity of the waveform corresponds to the operation of the emitter-coupled multivibrator, as described in the context.

This waveform is crucial in understanding the timing and switching behavior of the circuit, specifically how the emitter voltage of Q2 changes over time in response to the multivibrator's operation.
image_name:Capacitor voltage (Vc)
description:The graph titled 'Capacitor voltage (Vc)' is a time-domain waveform illustrating the behavior of the capacitor voltage in an emitter-coupled multivibrator circuit.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph depicting the voltage across a capacitor over time.

2. **Axes Labels and Units:**
- The horizontal axis represents time (t) and is unscaled, indicating a qualitative analysis rather than precise measurement.
- The vertical axis represents the capacitor voltage (Vc) in volts.
- Key voltage levels are marked at +0.6V and -0.6V.

3. **Overall Behavior and Trends:**
- The waveform exhibits a triangular shape, indicating a periodic charging and discharging cycle of the capacitor.
- The voltage alternates between +0.6V and -0.6V, suggesting a symmetrical oscillation about zero volts.
- The waveform is periodic, with consistent rise and fall times, reflecting the multivibrator's oscillatory nature.

4. **Key Features and Technical Details:**
- The waveform has peaks (maxima) at +0.6V and valleys (minima) at -0.6V.
- The slopes of the rising and falling edges are linear, indicating a constant rate of change during charging and discharging.
- The transitions occur at regular intervals, suggesting a stable frequency of oscillation.

5. **Annotations and Specific Data Points:**
- The graph includes annotations at the peaks and valleys, marking the voltage levels of +0.6V and -0.6V.
- There are reference lines indicating these voltage levels, providing a visual guide for the waveform's amplitude range.

This waveform is typical of a multivibrator circuit, where the capacitor alternately charges and discharges, creating a continuous oscillation between two voltage levels.
image_name:Vout
description:The function graph labeled "Vout" is a time-domain waveform representing the output voltage of an emitter-coupled multivibrator circuit. The graph is divided into four sections, each showing different voltages over time (t).

1. **Voltage at Base of Q2 (Vb2):**
- **Y-Axis:** Voltage at the base of Q2 (Vb2)
- **X-Axis:** Time (t)
- **Behavior:** The voltage alternates between two levels: \( V_{CC} - 0.6 \) and \( V_{CC} - 1.2 \). It starts at \( V_{CC} - 0.6 \) when Q2 is on, drops to \( V_{CC} - 1.2 \) when Q1 turns on, and returns to \( V_{CC} - 0.6 \) as Q2 turns on again.

2. **Voltage at Emitter of Q2 (Ve2):**
- **Y-Axis:** Voltage at the emitter of Q2 (Ve2)
- **X-Axis:** Time (t)
- **Behavior:** This voltage also alternates between \( V_{CC} - 1.2 \) and \( V_{CC} - 1.8 \). It follows a similar pattern to Vb2, with a sharp drop when Q1 turns on and a return to the higher level when Q2 turns on.

3. **Capacitor Voltage (Vc):**
- **Y-Axis:** Capacitor voltage (Vc)
- **X-Axis:** Time (t)
- **Behavior:** The capacitor voltage shows a triangular waveform oscillating between +0.6V and -0.6V. The voltage decreases linearly when Q1 is on and increases linearly when Q2 is on, indicating the charging and discharging of the capacitor.

4. **Output Voltage (Vout):**
- **Y-Axis:** Output voltage (Vout)
- **X-Axis:** Time (t)
- **Behavior:** The output voltage is a square wave alternating between \( V_{CC} \) and \( V_{CC} - 0.6 \). It remains at \( V_{CC} \) when Q2 is on and drops to \( V_{CC} - 0.6 \) when Q1 is on.

**Overall Trends:**
- The waveforms are periodic, with the transitions between states indicating the switching of transistors Q1 and Q2.
- The capacitor voltage oscillates in a triangular pattern, directly influencing the switching behavior of the transistors.
- The output voltage Vout exhibits a square wave pattern, making it suitable for applications requiring a stable oscillating signal.

Figure 10.21 (c) Waveforms within the emitter-coupled multivibrator.
emitter is one diode drop below $V_{C C}$. Thus the emitter of $Q_{2}$ is two diode drops below $V_{C C}$. Since $Q_{1}$ is off, the current $I_{1}$ is charging the capacitor so that the emitter of $Q_{1}$ is becoming more negative. $Q_{1}$ will turn on when the voltage at its emitter becomes equal to three diode drops below $V_{C C}$. Transistor $Q_{1}$ will then turn on, and the resulting collector current in $Q_{1}$ turns on $Q_{5}$. As a result, the base of $Q_{3}$ moves in the negative direction by one diode drop, causing the base of $Q_{2}$ to move in the negative direction by one diode drop. $Q_{2}$ will turn off, causing the base of $Q_{1}$ to move positive by one diode drop because $Q_{6}$ also turns off. As a result, the emitter-base junction of $Q_{2}$ is reverse biased by one diode drop because the voltage on $C$ cannot change instantaneously. Current $I_{1}$ must now charge the capacitor voltage in the negative direction by an amount equal to two diode drops before the circuit will switch back again. Since the circuit is symmetrical, the half period is given by the time required to charge
the capacitor and is

$$
\begin{equation*}
\frac{T}{2}=\frac{Q}{I_{1}} \tag{10.72}
\end{equation*}
$$

where $Q=C \Delta V=2 C V_{B E(\text { on })}$ is the charge on the capacitor. The frequency of the oscillator is thus

$$
\begin{equation*}
f=\frac{1}{T}=\frac{I_{1}}{4 C V_{B E(\mathrm{on})}} \tag{10.73}
\end{equation*}
$$

The various waveforms in the circuit are shown in Fig. 10.21c. This emitter-coupled configuration is nonsaturating and contains only npn transistors. Furthermore, the voltage swings within the circuit are small. As a result, the circuit is capable of operating up to approximately 1 GHz for typical integrated-circuit transistors. However, the usable frequency range is limited to a value lower than this because the center frequency drift with temperature variations becomes large at the higher frequencies. This drift occurs because the switching transients themselves become a large percentage of the period of the oscillation, and the duration of the switching transients depends on circuit parasitics, circuit resistances, transistor transconductance, and transistor input resistance, which are all temperature sensitive.

Although the emitter-coupled configuration is capable of high operating speed, it displays considerable sensitivity of center frequency to temperature even at low frequencies, since the period is dependent on $V_{B E(\text { on })}$. Utilizing $(10.73)$ we can calculate the temperature coefficient of the center frequency as

$$
\begin{equation*}
\frac{1}{\omega_{\mathrm{osc}}} \frac{d \omega_{\mathrm{osc}}}{d T}=-\frac{1}{V_{B E(\mathrm{on})}} \frac{d V_{B E(\mathrm{on})}}{d T}=\frac{+2 \mathrm{mV} /{ }^{\circ} \mathrm{C}}{600 \mathrm{mV}}=+3300 \mathrm{ppm} /{ }^{\circ} \mathrm{C} \tag{10.74}
\end{equation*}
$$

This temperature sensitivity of center frequency can be compensated by causing current $I_{1}$ to be temperature sensitive in such a way that its effect is equal and opposite to the effect of the variation of $V_{B E(\text { on })}$.
