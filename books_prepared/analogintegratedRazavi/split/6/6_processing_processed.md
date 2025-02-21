# Frequency Response of Amplifiers

Our analysis of simple amplifiers has thus far focused on low-frequency characteristics, neglecting the effect of device and load capacitances. In most analog circuits, however, the speed trades with many other parameters such as gain, power dissipation, and noise. It is therefore necessary to understand the frequency-response limitations of each circuit.

In this chapter, we study the behavior of single-stage and differential amplifiers in the frequency domain. Following a review of basic concepts, we analyze the high-frequency response of commonsource and common-gate stages and source followers. Next, we deal with cascode and differential amplifiers. Finally, we consider the effect of active current mirrors on the frequency response of differential pairs.

## 6.1 ■ General Considerations

Recall that a MOS device exhibits four capacitances: $C_{G S}, C_{G D}, C_{D B}$, and $C_{S B}$. For this reason, the transfer function of CMOS circuits can rapidly become complicated, calling for approximations that simplify the circuit. In this section, we introduce two such approximations, namely, Miller's theorem and association of poles with nodes. We remind the reader that a two-terminal impedance, $Z$, is defined as $Z=V / I$, where $V$ and $I$ denote the voltage across and the current flowing through the device. For example, $Z=1 /(C s)$ for a capacitor. Also, the transfer function of a circuit yields the frequency response if we replace $s$ with $j \omega$, i.e., if we assume a sinusoidal input such as $A \cos \omega t$. For example, $H(j \omega)=(R C j \omega+1)^{-1}$ provides the magnitude and phase of a simple low-pass filter.

In this chapter, we are primarily interested in the magnitude of the transfer function (with $s=$ $j \omega)$. Figure 6.1 shows examples of magnitude response. We should also remark that, even if computed exactly, some transfer functions do not offer much insight. We therefore study numerous special cases by considering extreme conditions, e.g., if the load capacitance is very small or very large.

A few basic concepts are used extensively throughout this chapter and merit a brief review. (1) The magnitude of a complex number $a+j b$ is given by $\sqrt{a^{2}+b^{2}}$. (2) Zeros and poles are respectively defined as the roots of the numerator and denominator of the transfer function. (3) According to Bode's approximations, the slope of the magnitude of a transfer function increases by $20 \mathrm{~dB} /$ decade as $\omega$ passes a pole frequency and decreases by $20 \mathrm{~dB} /$ decade as $\omega$ passes a zero frequency.
image_name:(a)
description:The graph labeled (a) is a frequency response plot, specifically a Bode magnitude plot, for a low-pass filter.

1. **Type of Graph and Function:**
- This is a Bode magnitude plot, showing the frequency response of a low-pass filter.

2. **Axes Labels and Units:**
- The vertical axis represents the magnitude of the transfer function, \(\left| \frac{V_{out}}{V_{in}}(j\omega) \right|\), typically in decibels (dB), although the exact unit isn't specified in the image.
- The horizontal axis represents the angular frequency \(\omega\), usually in radians per second or hertz, plotted on a logarithmic scale.

3. **Overall Behavior and Trends:**
- The plot shows a characteristic low-pass filter response, where the magnitude is relatively constant at low frequencies, indicating that these frequencies are passed through.
- As the frequency increases past a certain cutoff frequency, the magnitude begins to decrease, indicating attenuation of higher frequencies.
- The slope of the decrease is typically \(-20 \text{ dB/decade}\) for a first-order low-pass filter.

4. **Key Features and Technical Details:**
- The plot starts at a higher magnitude, indicating that low frequencies are allowed to pass with little attenuation.
- There is a noticeable point where the slope changes, marking the cutoff frequency. This is the frequency beyond which the filter significantly attenuates the input signal.
- The exact cutoff frequency and gain levels are not specified numerically in the graph.

5. **Annotations and Specific Data Points:**
- There are no specific annotations or numerical data points provided on the graph. The cutoff frequency is implied by the change in slope but is not explicitly marked.
image_name:(b)
description:The graph labeled as (b) represents a band-pass frequency response. This type of graph is typically a Bode plot, which is used to illustrate the frequency response of a system.

1. **Type of Graph and Function:**
- This is a Bode plot showing the magnitude response of a band-pass filter.

2. **Axes Labels and Units:**
- The vertical axis is labeled as the magnitude of the transfer function, \(|V_{out}/V_{in}(j\omega)|\), indicating the ratio of output voltage to input voltage. The scale is logarithmic, which is common for Bode plots.
- The horizontal axis represents angular frequency, \(\omega\), typically measured in radians per second. The scale is also logarithmic.

3. **Overall Behavior and Trends:**
- The graph shows a peak in magnitude at a certain frequency, indicating the passband of the filter. This is characteristic of a band-pass filter, which allows frequencies within a certain range to pass through while attenuating frequencies outside this range.
- The magnitude increases as the frequency approaches the center of the passband, reaches a peak, and then decreases as the frequency moves away from the passband.

4. **Key Features and Technical Details:**
- The peak of the graph represents the center frequency of the band-pass filter, where the gain is highest.
- The bandwidth of the filter is defined by the range of frequencies over which the magnitude is significantly above the baseline.
- There are two critical points where the slope changes: one where the magnitude starts increasing towards the peak and another where it starts decreasing after the peak.

5. **Annotations and Specific Data Points:**
- While specific numerical values are not provided in this graph, key points would include the center frequency and the -3 dB points that define the bandwidth.
- No additional annotations or reference lines are present in the graph.
image_name:(c)
description:The graph labeled (c) is a frequency-response curve representing a high-pass filter. This is a Bode magnitude plot, which shows the gain of the filter as a function of frequency.

1. **Axes Labels and Units:**
- The vertical axis is labeled as the magnitude of the transfer function, \( \left| \frac{V_{\text{out}}}{V_{\text{in}}}(j\omega) \right| \), which represents the ratio of the output voltage to the input voltage in the frequency domain. This axis typically uses a logarithmic scale in decibels (dB), although specific units are not shown in the diagram.
- The horizontal axis is labeled with \( \omega \), representing angular frequency. This axis is typically on a logarithmic scale, indicating that the frequency increases exponentially from left to right.

2. **Overall Behavior and Trends:**
- The graph starts with a low magnitude at low frequencies, indicating that the filter attenuates signals in this range.
- As the frequency increases, the magnitude sharply rises, indicating the cutoff frequency where the filter begins to pass higher frequencies with less attenuation.
- After the initial rise, the magnitude levels off and remains constant, showing that high frequencies are passed with consistent gain.

3. **Key Features and Technical Details:**
- The sharp increase in magnitude at a certain frequency indicates the cutoff frequency, beyond which the filter effectively passes signals.
- The flat region at higher frequencies suggests that the filter provides a constant gain for frequencies above the cutoff.

4. **Annotations and Specific Data Points:**
- While specific numerical values for the cutoff frequency or gain are not provided in the graph, the general shape is indicative of a standard high-pass filter response.

Figure 6.1 (a) Low-pass, (b) band-pass, and (c) high-pass frequency-response examples.

### 6.1.1 Miller Effect

An important phenomenon that occurs in many analog (and digital) circuits is related to the "Miller effect," as described by Miller in a theorem.
Miller's Theorem If the circuit of Fig. 6.2(a) can be converted to that of Fig. 6.2(b), then $Z_{1}=$ $Z /\left(1-A_{v}\right)$ and $Z_{2}=Z /\left(1-A_{v}^{-1}\right)$, where $A_{v}=V_{Y} / V_{X}$.
image_name:(a)
description:
[
name: Z, type: Resistor, value: Z, ports: {N1: X, N2: Y}
]
extrainfo:The diagram illustrates the application of Miller's theorem, showing a floating impedance Z between nodes X and Y in configuration (a).
image_name:(b)
description:
[
name: Z1, type: Resistor, value: Z1, ports: {N1: X, N2: GND}
name: Z2, type: Resistor, value: Z2, ports: {N1: Y, N2: GND}
]
extrainfo:The circuit diagram (b) applies the Miller effect, splitting the impedance Z into two grounded impedances Z1 and Z2 at nodes X and Y respectively.

Figure 6.2 Application of Miller effect to a floating impedance.

Proof The current flowing through $Z$ from $X$ to $Y$ is equal to $\left(V_{X}-V_{Y}\right) / Z$. For the two circuits to be equivalent, the same current must flow through $Z_{1}$. Thus,

$$
\begin{equation*}
\frac{V_{X}-V_{Y}}{Z}=\frac{V_{X}}{Z_{1}} \tag{6.1}
\end{equation*}
$$

that is

$$
\begin{equation*}
Z_{1}=\frac{Z}{1-\frac{V_{Y}}{V_{X}}} \tag{6.2}
\end{equation*}
$$

Similarly,

$$
\begin{equation*}
Z_{2}=\frac{Z}{1-\frac{V_{X}}{V_{Y}}} \tag{6.3}
\end{equation*}
$$

This decomposition of a "floating" impedance, $Z$, into two "grounded" impedances proves useful in analysis and design.

#### Example 6.1

Consider the circuit shown in Fig. 6.3(a), where the voltage amplifier has a negative gain equal to $-A$ and is otherwise ideal. Calculate the input capacitance of the circuit.
image_name:Figure 6.3(a)
description:
[
name: A, type: OpAmp, value: A, ports: {InP: X OutP: Y}
name: CF, type: Capacitor, value: CF, ports: {Np: X, Nn: Y}
]
extrainfo:The circuit in Fig. 6.3(a) is an inverting amplifier configuration with a feedback capacitor CF, which introduces Miller multiplication of the input capacitance. The input capacitance is effectively multiplied by the factor (1+A) due to the feedback mechanism.
image_name:Figure 6.3(b)
description:
[
name: Z1, type: Resistor, value: Z1, ports: {N1: X, N2: GND}
name: Z2, type: Resistor, value: Z2, ports: {N1: Y, N2: GND}
name: -A, type: OpAmp, value: -A, ports: {InP: X OutP: Y}
]
extrainfo:The circuit in diagram (b) represents a feedback configuration using resistors Z1 and Z2 connected to an operational amplifier with negative gain -A. The nodes X and Y are connected to the resistors and the amplifier.
image_name:Figure 6.3(c)
description:
[
name: CF, type: Capacitor, value: CF, ports: {Np: X, Nn: Y}
name: A, type: OpAmp, value: -A, ports: {InP: X, Out: Y}
name: ΔV, type: VoltageSource, value: ΔV, ports: {Np: X, Nn: GND}
]
extrainfo:The circuit in diagram (c) is a negative feedback amplifier with a voltage source ΔV applied at the input. The feedback capacitor CF and the input capacitor Cin form a capacitive divider. The op-amp has a negative gain of -A, and the output is -A times the input voltage ΔV. This setup demonstrates the Miller effect in capacitors.

#### Solution

Using Miller's theorem to convert the circuit to that shown in Fig. 6.3(b), we have $Z=1 /\left(C_{F} s\right)$ and $Z_{1}=$ $\left[1 /\left(C_{F} s\right)\right] /(1+A)$. That is, the input capacitance is equal to $C_{F}(1+A)$. We call this effect "Miller multiplication" of the capacitor.

Why is $C_{F}$ multiplied by $1+A$ ? Suppose, as depicted in Fig. 6.3(c), we measure the input capacitance by applying a voltage step at the input and calculating the charge supplied by the voltage source. A step equal to $\Delta V$ at $X$ results in a change of $-A \Delta V$ at $Y$, yielding a total change of $(1+A) \Delta V$ in the voltage across $C_{F}$. Thus, the charge drawn by $C_{F}$ from $V_{i n}$ is equal to $(1+A) C_{F} \Delta V$ and the equivalent input capacitance equal to $(1+A) C_{F}$.

#### Example 6.2

A student needs a large capacitor for a filter and decides to utilize the Miller multiplication of [Fig. 6.4(a)]. Explain the issues in this approach.
image_name:Figure 6.4(a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: X}
name: CF, type: Capacitor, value: CF, ports: {Np: X, Nn: Y}
name: -A, type: OpAmp, value: -A, ports: {InP: X,OutP: Y}
]
extrainfo:The circuit utilizes the Miller effect to multiply the capacitance CF by (A+1). The voltage at node X affects the voltage at node Y through the op-amp, creating a large effective capacitance between Vin and Vout.
image_name:Figure 6.4(b)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: X}
name: CF, type: Capacitor, value: CF, ports: {Np: X, Nn: Y}
name: M1, type: NMOS, ports: {S: GND, D: Y, G: X}
name: Is, type: CurrentSource, value: Is, ports: {N1: VDD, N2: Y}
]
extrainfo:The circuit in (b) utilizes an NMOS transistor M1 to manage the feedback path. The output voltage swing at Y is AV0, which is A times the input swing V0 at X. The design aims to leverage Miller multiplication for effective capacitance increase.

#### Solution

The issues relate to the amplifier, particularly to its output swing. As exemplified by the implementation in Fig. 6.4(b), if the voltage at $X$ swings by $V_{0}$, then $Y$ must accommodate a swing of $A V_{0}$ without saturating the amplifier. In addition, the dc level in $V_{i n}$ must be compatible with the input of the amplifier.

It is important to understand that (6.2) and (6.3) hold if we know a priori that the circuit of Fig. 6.2(a) can be converted to that of Fig. 6.2(b). That is, Miller's theorem does not stipulate the conditions under which this conversion is valid. If the impedance $Z$ forms the only signal path between $X$ and $Y$, then the conversion is often invalid. Illustrated in Fig. 6.5 for a simple resistive divider, the theorem gives a correct
image_name:Figure 6.5 Improper application of Miller's theorem.(a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: X, N2: Y}
name: R2, type: Resistor, value: R2, ports: {N1: Y, N2: X2}
]
extrainfo:The circuit diagram (a) is a simple resistive divider with resistors R1 and R2 connected in series between nodes X and X2, with node Y as the intermediate point.
image_name:Figure 6.5 Improper application of Miller's theorem.(b)
description:
[
name: R1+R2, type: Resistor, value: R1+R2, ports: {N1: X, N2: X1}
name: R2, type: Resistor, value: R2, ports: {N1: Y, N2: X1}
name: -R2, type: Resistor, value: -R2, ports: {N1: Y, N2: X1}
]
extrainfo:The circuit diagram (b) is a modified version of a resistive divider using Miller's theorem. It shows an equivalent transformation with resistors R1+R2, R2, and -R2 connected between nodes X, Y, and X1.

input impedance but an incorrect gain. Nevertheless, Miller's theorem proves useful in cases where the impedance $Z$ appears in parallel with the main signal (Fig. 6.6).
image_name:Figure 6.6 Typical case for valid application of Miller's theorem.
description:
[
name: Z, type: Resistor, value: Z, ports: {N1: Input, N2: Output}
name: A, type: OpAmp, value: -A, ports: {InP: Input, InN: Output, OutP: Output}
]
extrainfo:This circuit diagram represents a typical application of Miller's theorem, where the impedance Z appears in parallel with the main signal path. The op-amp is configured as an inverting amplifier with feedback through the impedance Z.

#### Example 6.3

Calculate the input resistance of the circuit shown in Fig. 6.7(a).
image_name:Figure 6.7(a)
description:
[
name: M1, type: NMOS, ports: {S: X, D: Y, G: Vb}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: Y}
name: ro, type: Resistor, value: ro, ports: {N1: Y, N2: X}
]
extrainfo:The circuit represents a typical application of Miller's theorem. It includes an NMOS transistor M1 with its source connected to node X, drain to node Y, and gate to the bias voltage Vb. A current source I1 is connected from VDD to node Y. Resistor ro is connected between nodes Y and X, and resistor Rin is connected between node X and ground. This configuration is used to calculate the input resistance of the circuit.

image_name:Figure 6.7(b)
description:
[
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: Y}
name: M1, type: NMOS, ports: {S: X, D: Y, G: Vb}
name: ro/(1-1/Av), type: Resistor, value: ro/(1-1/Av), ports: {N1: Y, N2: GND}
name: ro/(1-Av), type: Resistor, value: ro/(1-Av), ports: {N1: X, N2: GND}
]
extrainfo:The circuit is used to calculate the input resistance, applying Miller's theorem. It includes a current source I1 from VDD to node Y, an NMOS transistor M1 with its source at node X, drain at node Y, and gate at bias voltage Vb. Resistors ro/(1-1/Av) and ro/(1-Av) are connected to nodes Y and X respectively. The input resistance is a parallel combination of rO/(1-Av) and 1/(gm+gmb).

#### Solution

The reader can prove that the voltage gain from $X$ to $Y$ is equal to $1+\left(g_{m}+g_{m b}\right) r_{O}$. As shown in Fig. 6.7(b), the input resistance is given by the parallel combination of $r_{O} /\left(1-A_{v}\right)$ and $1 /\left(g_{m}+g_{m b}\right)$. Since $A_{v}$ is usually greater than unity, $r_{O} /\left(1-A_{v}\right)$ is a negative resistance. We therefore have

$$
\begin{align*}
R_{i n} & =\frac{r_{O}}{1-\left[1+\left(g_{m}+g_{m b}\right) r_{O}\right]} \| \frac{1}{g_{m}+g_{m b}}  \tag{6.4}\\
& =\frac{-1}{g_{m}+g_{m b}} \| \frac{1}{g_{m}+g_{m b}}  \tag{6.5}\\
& =\infty \tag{6.6}
\end{align*}
$$

This is the same result as obtained in Chapter 3 (Fig. 3.54) by direct calculation.

We should also mention that, strictly speaking, the value of $A_{v}=V_{Y} / V_{X}$ in (6.2) and (6.3) must be calculated at the frequency of interest, complicating the algebra significantly. To understand this point, let us return to Example 6.1 and assume an amplifier with a finite output resistance. Depicted in Fig. 6.8, the equivalent circuit reveals that $V_{Y} \neq-A V_{X}$ at high frequencies, and hence $C_{F}$ cannot be simply multiplied by $1+A$ to yield the input capacitance. However, in many cases we use the low-frequency value of $V_{Y} / V_{X}$ to gain insight into the behavior of the circuit. We call this approach "Miller's approximation."
image_name:Figure 6.8 Equivalent circuit showing gain change at high frequencies.
description:
[
name: CF, type: Capacitor, value: CF, ports: {Np: X, Nn: Y}
name: Rout, type: Resistor, value: Rout, ports: {N1: -AVx, N2: GND}
name: -AVx, type: VoltageControlVoltageSource, ports: {Np: -AVx, Nn:GND}
]
extrainfo:The circuit is an amplifier with feedback capacitor CF and output resistor Rout. The amplifier has an input at node X and output at node Y, with the output voltage being -AVx.

#### Example 6.4

Determine the transfer function of the circuit shown in Fig. 6.9(a) using (a) direct analysis and (b) Miller's approximation.
image_name:Figure 6.9(a)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: CF, type: Capacitor, value: CF, ports: {Np: X, Nn: Vout}
name: Rout, type: Resistor, value: Rout, ports: {N1: -AVx, N2: Vout}
name: -AVx, type: VoltageControlledVoltageSource, value: -AVx, ports: {Np: -AVx, Nn: GND}
]
extrainfo:The circuit is an amplifier with feedback capacitor CF and output resistor Rout. The amplifier has an input at node X and output at node Y, with the output voltage being -AVx. The transfer function analysis involves considering the feedback network and gain change at high frequencies.
image_name:Figure 6.9(b)
description:The graph labeled (b) is a Bode plot, which is used to represent the frequency response of a system. The plot is shown on a logarithmic scale for the frequency axis (horizontal axis, denoted as \( \omega \)) and a decibel scale for the magnitude of the transfer function \( 20 \log \left| \frac{V_{out}}{V_{in}}(j\omega) \right| \) on the vertical axis.

1. **Axes Labels and Units:**
- The horizontal axis is labeled as \( \omega \), representing frequency on a logarithmic scale.
- The vertical axis is labeled as \( 20 \log \left| \frac{V_{out}}{V_{in}}(j\omega) \right| \), indicating the gain in decibels (dB).

2. **Overall Behavior and Trends:**
- The plot starts with a flat region at a gain level of \( A \) dB, indicating a constant gain at low frequencies.
- As the frequency increases, the plot shows a downward slope at a rate of \(-20 \text{ dB/decade}\), indicating a reduction in gain.
- After this slope, the plot flattens out again, reaching a constant gain level at high frequencies.

3. **Key Features and Technical Details:**
- The point \( \omega_p \) marks the beginning of the slope where the gain starts to decrease.
- The point \( \omega_z \) marks where the slope ends and the gain stabilizes again.
- The slope of \(-20 \text{ dB/decade}\) suggests the presence of a single pole in the system.

4. **Annotations and Specific Data Points:**
- The plot is annotated with two significant frequencies: \( \omega_p \) and \( \omega_z \).
- These points are typically associated with the pole and zero frequencies of the system, respectively.

This Bode plot effectively illustrates how the gain of the system changes with frequency, highlighting the impact of poles and zeros on the frequency response.
image_name:Figure 6.9(c)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: Rout, type: Resistor, value: Rout, ports: {N1: -AVx, N2: Vout}
name: CF, type: Capacitor, value: CF/(A+1), ports: {Np: Y(Vout), Nn: GND}
name: -AVx, type: VoltageControlledVoltageSource, ports: {Np: AVx, Nn: GND}
]
extrainfo:The circuit is an amplifier with feedback capacitor CF and output resistor Rout. The amplifier has an input at node X and output at node Y, with the output voltage being -AVx. The diagram (c) shows the equivalent circuit with Miller's approximation applied to CF, resulting in CF/(A+1) at the output.

#### Solution

(a) We note that the current flowing through $R_{S}$ is given by $\left(V_{i n}-V_{X}\right) / R_{S}$, yielding a voltage drop across $R_{\text {out }}$ equal to $\left(V_{\text {in }}-V_{X}\right) R_{\text {out }} / R_{S}$. It follows that

$$
\begin{equation*}
\frac{V_{\text {in }}-V_{X}}{R_{S}} R_{\text {out }}-A V_{X}=V_{\text {out }} \tag{6.7}
\end{equation*}
$$

We also equate the currents flowing through $R_{S}$ and $C_{F}$ :

$$
\begin{equation*}
\frac{V_{\text {in }}-V_{X}}{R_{S}}=\left(V_{X}-V_{\text {out }}\right) C_{F} s \tag{6.8}
\end{equation*}
$$

The reader can find $V_{X}$ from the first equation and substitute the result in the second, thereby obtaining

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}(s)=\frac{R_{\text {out }} C_{F} s-A}{\left[(A+1) R_{S}+R_{\text {out }}\right] C_{F} s+1} \tag{6.9}
\end{equation*}
$$

The circuit thus exhibits a zero at $\omega_{z}=A /\left(R_{\text {out }} C_{F}\right)$ and a pole at $\omega_{p}=-1 /\left[(A+1) R_{S} C_{F}+R_{\text {out }} C_{F}\right]$. Figure 6.9(b) plots the response for the case of $\left|\omega_{p}\right|<\left|\omega_{z}\right|$.
(b) Applying Miller's approximation, we decompose $C_{F}$ into $(1+A) C_{F}$ at the input and $C_{F} /\left(1+A^{-1}\right)$ at the output [Fig. 6.9(c)]. Since $V_{\text {out }} / V_{\text {in }}=\left(V_{X} / V_{\text {in }}\right)\left(V_{\text {out }} / V_{X}\right)$, we first write $V_{X} / V_{\text {in }}$ by considering $R_{S}$ and $(1+A) C_{F}$ as a voltage divider:

$$
\begin{align*}
\frac{V_{X}}{V_{\text {in }}} & =\frac{\frac{1}{(1+A) C_{F} s}}{\frac{1}{(1+A) C_{F} s}+R_{S}}  \tag{6.10}\\
& =\frac{1}{(1+A) R_{S} C_{F} s+1} \tag{6.11}
\end{align*}
$$

As for $V_{\text {out }} / V_{X}$, we first amplify $V_{X}$ by $-A$ and subject the result to the output voltage divider,

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{X}}=\frac{-A}{\frac{1}{1+A^{-1}} C_{F} R_{\text {out }} s+1} \tag{6.12}
\end{equation*}
$$

That is

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}(s)=\frac{-A}{\left[(1+A) R_{S} C_{F} s+1\right]\left(\frac{1}{1+A^{-1}} C_{F} R_{\text {out }} s+1\right)} \tag{6.13}
\end{equation*}
$$

Sadly, Miller's approximation has eliminated the zero and predicted two poles for the circuit! Despite these shortcomings, Miller's approximation can provide intuition in many cases. ${ }^{1}$

If applied to obtain the input-output transfer function, Miller's theorem cannot be used simultaneously to calculate the output impedance. To derive the transfer function, we apply a voltage source to the input of the circuit, obtaining a value for $V_{Y} / V_{X}$ in Fig. 6.2(a). On the other hand, to determine the output impedance, we must apply a voltage source to the output of the circuit, obtaining a value for $V_{X} / V_{Y}$ that may not be equal to the inverse of the $V_{Y} / V_{X}$ measured in the first test. For example, the circuit of Fig. 6.7 (b) may suggest that the output impedance is equal to

$$
\begin{align*}
R_{\text {out }} & =\frac{r_{O}}{1-1 / A_{v}}  \tag{6.14}\\
& =\frac{r_{O}}{1-\left[1+\left(g_{m}+g_{m b}\right) r_{O}\right]^{-1}}  \tag{6.15}\\
& =\frac{1}{g_{m}+g_{m b}}+r_{O} \tag{6.16}
\end{align*}
$$

whereas the actual value is equal to $r_{O}$ (if $X$ is grounded). Other subtleties of Miller's theorem are described in the Appendix C.

In summary, Miller's approximation divides a floating impedance by the low-frequency gain and faces the following limitations: (1) it may eliminate zeros, (2) it may predict additional poles, and (3) it does not correctly compute the "output" impedance.

### 6.1.2 Association of Poles with Nodes

Consider the simple cascade of amplifiers depicted in Fig. 6.10. Here, $A_{1}$ and $A_{2}$ are ideal voltage amplifiers, $R_{1}$ and $R_{2}$ model the output resistance of each stage, $C_{i n}$ and $C_{N}$ represent the input capacitance of each stage, and $C_{P}$ denotes the load capacitance. The overall transfer function can be written as

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}(s)=\frac{A_{1}}{1+R_{S} C_{\text {in }} s} \cdot \frac{A_{2}}{1+R_{1} C_{N} s} \cdot \frac{1}{1+R_{2} C_{P} s} \tag{6.17}
\end{equation*}
$$

The circuit exhibits three poles, each of which is determined by the total capacitance seen from each node to ground multiplied by the total resistance seen at the node to ground. We can therefore associate each pole with one node of the circuit, i.e., $\omega_{j}=\tau_{j}^{-1}$, where $\tau_{j}$ is the product of the capacitance and resistance seen at node $j$ to ground. From this perspective, we may say that "each node in the circuit contributes one pole to the transfer function."
image_name:Figure 6.10 Cascade of amplifiers
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: M}
name: Cin, type: Capacitor, value: Cin, ports: {Np: M, Nn: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: M, InN: GND, OutP: Out(A1)}
name: R1, type: Resistor, value: R1, ports: {N1: Out(A1), N2: N}
name: CN, type: Capacitor, value: CN, ports: {Np: N, Nn: GND}
name: A2, type: OpAmp, value: A2, ports: {InP: N, InN: GND, Out: Out(A2)}
name: R2, type: Resistor, value: R2, ports: {N1: Out(A2), N2: P(Vout)}
name: CP, type: Capacitor, value: CP, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a cascade of two amplifiers, each followed by a resistor-capacitor network, which helps in determining the poles of the transfer function. The input is connected through a resistor and capacitor to the first amplifier, and the output is taken from the second amplifier.

The above statement is not valid in general. For example, in the circuit of Fig. 6.11, the location of the poles is difficult to calculate because $R_{3}$ and $C_{3}$ create interaction between $X$ and $Y$. Nevertheless, in many circuits, association of one pole with each node provides an intuitive approach to estimating the transfer function: we simply multiply the total equivalent capacitance by the total incremental (smallsignal) resistance (both from the node of interest to ground), thus obtaining an equivalent time constant and hence a pole frequency.
image_name:Figure 6.11 Example of interaction between nodes.
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: X}
name: C1, type: Capacitor, value: C1, ports: {Np: X, Nn: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: X, InN: GND, OutP: X3, OutN: GND}
name: R3, type: Resistor, value: R3, ports: {N1: X, N2: X2}
name: C3, type: Capacitor, value: C3, ports: {Np: X2, Nn: Y}
name: R2, type: Resistor, value: R2, ports: {N1: X3, N2: Y}
name: C2, type: Capacitor, value: C2, ports: {Np: Y, Nn: GND}
]
extrainfo:This circuit is a feedback amplifier with an op-amp (A1) and passive components forming a feedback network. The interaction between nodes X and Y is influenced by R3 and C3, affecting the pole locations in the transfer function.

#### Example 6.5

Neglecting channel-length modulation, compute the transfer function of the common-gate stage shown in Fig. 6.12(a).
image_name:Figure 6.12(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: M1, type: NMOS, ports: {S: X, D: Y, G: Vb}
name: I1, type: CurrentSource, value: I1, ports: {Np: X, Nn: GND}
name: RD, type: Resistor, value: RD, ports: {N1: Y, N2: VDD}
]
extrainfo:This circuit is a common-gate amplifier with an NMOS transistor (M1) and passive components forming the biasing and feedback network. The input signal is applied to the source of M1, and the output is taken from the drain. Parasitic capacitances affect the pole frequencies at nodes X and Y.
image_name:Figure 6.12(b)
description:
[
name: RD, type: Resistor, value: RD, ports: {N1: Vout, N2: VDD}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: gmV1, type: VoltageControlCurrentSource, value: gmV1, ports: {Np: Vout, Nn: X}
name: CGD, type: Capacitor, value: CGD, ports: {Np: Vout, Nn: X}
name: CDB, type: Capacitor, value: CDB, ports: {Np: Vout, Nn: GND}
name: CGS, type: Capacitor, value: CGS, ports: {Np: X, Nn: GND}
name: CSB, type: Capacitor, value: CSB, ports: {Np: X, Nn: GND}
]
extrainfo:This circuit is a common-gate amplifier with parasitic capacitances at the input and output. The NMOS transistor M1 is used as the amplifying device, with RD as the load resistor. The input is applied at Vin, and the output is taken from Vout. Parasitic capacitances CGD, CDB, CGS, and CSB affect the frequency response of the amplifier.
Figure 6.12 Common-gate stage with parasitic capacitances.

#### Solution

In this circuit, the capacitances contributed by $M_{1}$ are connected from the input and output nodes to ground [Fig. 6.12(b)]. At node $X, C_{S}=C_{G S}+C_{S B}$, giving a pole frequency

$$
\begin{equation*}
\omega_{i n}=\left[\left(C_{G S}+C_{S B}\right)\left(R_{S} \| \frac{1}{g_{m}+g_{m b}}\right)\right]^{-1} \tag{6.18}
\end{equation*}
$$

Similarly, at node $Y, C_{D}=C_{D G}+C_{D B}$, yielding a pole frequency

$$
\begin{equation*}
\omega_{\text {out }}=\left[\left(C_{D G}+C_{D B}\right) R_{D}\right]^{-1} \tag{6.19}
\end{equation*}
$$

The overall transfer function is thus given by

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}(s)=\frac{\left(g_{m}+g_{m b}\right) R_{D}}{1+\left(g_{m}+g_{m b}\right) R_{S}} \cdot \frac{1}{\left(1+\frac{s}{\omega_{\text {in }}}\right)\left(1+\frac{s}{\omega_{\text {out }}}\right)} \tag{6.20}
\end{equation*}
$$

where the first fraction represents the low-frequency gain of the circuit. Note that if we do not neglect $r_{O 1}$, the input and output nodes interact, making it difficult to calculate the poles.

## 6.2 ■ Common-Source Stage

The common-source topology exhibits a relatively high input impedance while providing voltage gain and requiring a minimal voltage headroom. As such, it finds wide application in analog circuits and its frequency response is of interest.

Shown in Fig. 6.13(a) is a common-source stage driven by a finite source resistance, $R_{S} .{ }^{2}$ We identify all of the capacitances in the circuit, noting that $C_{G S}$ and $C_{D B}$ are "grounded" capacitances while $C_{G D}$ appears between the input and the output. In reality, the circuit also drives a load capacitance, which can be merged with $C_{D B}$.
image_name:Figure 6.13(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: CGS, type: Capacitor, value: CGS, ports: {Np: X, Nn: GND}
name: CGD, type: Capacitor, value: CGD, ports: {Np: Vout, Nn: X}
name: CDB, type: Capacitor, value: CDB, ports: {Np: Vout, Nn: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: X}
]
extrainfo:The circuit is a common-source amplifier stage with a finite source resistance and includes parasitic capacitances CGS, CGD, and CDB. The NMOS transistor M1 is in saturation, and the circuit drives a load capacitance merged with CDB.
image_name:Figure 6.13(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: CGS, type: Capacitor, value: CGS, ports: {Np: X, Nn: GND}
name: (1-Av)CGD, type: Capacitor, value: (1-Av)CGD, ports: {Np: Vout, Nn: X}
name: CDB, type: Capacitor, value: CDB, ports: {Np: Vout, Nn: GND}
name: (1-1/Av)CGD, type: Capacitor, value: (1-1/Av)CGD, ports: {Np: Vout, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: X}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
]
extrainfo:The circuit is a high-frequency model of a common-source amplifier using Miller's approximation. The NMOS transistor M1 operates in saturation, driven by the input voltage Vin. The output is taken across the load resistor RD. Capacitances CGS, CGD, and CDB are considered, with the Miller effect applied to CGD.

Figure 6.13 (a) High-frequency model of a common-source stage, and (b) simplified circuit using Miller's approximation.

Miller's Approximation Assuming that $\lambda=0$ and $M_{1}$ operates in saturation, let us first estimate the transfer function by associating one pole with each node. The total capacitance seen from $X$ to ground is equal to $C_{G S}$ plus the Miller multiplication of $C_{G D}$, namely, $C_{G S}+\left(1-A_{v}\right) C_{G D}$, where $A_{v}=-g_{m} R_{D}$ [Fig. 6.13(b)]. The magnitude of the "input" pole is therefore given by

$$
\begin{equation*}
\omega_{i n}=\frac{1}{R_{S}\left[C_{G S}+\left(1+g_{m} R_{D}\right) C_{G D}\right]} \tag{6.21}
\end{equation*}
$$

At the output node, the total capacitance seen to ground is equal to $C_{D B}$ plus the Miller effect of $C_{G D}$, i.e., $C_{D B}+\left(1-A_{v}^{-1}\right) C_{G D} \approx C_{D B}+C_{G D}$ (if $\left.A_{v} \gg 1\right)$. Thus,

$$
\begin{equation*}
\omega_{\text {out }}=\frac{1}{R_{D}\left(C_{D B}+C_{G D}\right)} \tag{6.22}
\end{equation*}
$$

image_name:Figure 6.14 Model for calculation of output impedance.
description:
[
name: CGD, type: Capacitor, value: CGD, ports: {Np: gi, Nn: d1}
name: CDB, type: Capacitor, value: CDB, ports: {Np: d1, Nn: GND}
name: CGS, type: Capacitor, value: CGS, ports: {Np: gi, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: d1, G: gi}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: d1}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a simplified model for calculating the output impedance with a focus on the Miller effect and output pole approximation. It includes an NMOS transistor M1, a resistor RD, and capacitors CGD, CDB, and CGS. The node labeled 'd1' is the output node connected to the drain of M1 and the resistor RD.

Another approximation of the output pole can be obtained if $R_{S}$ is relatively large. Simplifying the circuit as shown in Fig. 6.14, where the effect of $R_{S}$ is neglected, the reader can prove that

$$
\begin{equation*}
Z_{X}=\frac{1}{C_{e q} s} \|\left(\frac{C_{G D}+C_{G S}}{C_{G D}} \cdot \frac{1}{g_{m 1}}\right) \tag{6.23}
\end{equation*}
$$

[^27]where $C_{e q}=C_{G D} C_{G S} /\left(C_{G D}+C_{G S}\right)$. Thus, the output pole is roughly equal to
\$\$

$$
\begin{equation*}
\omega_{\text {out }}=\frac{1}{\left[R_{D} \|\left(\frac{C_{G D}+C_{G S}}{C_{G D}} \cdot \frac{1}{g_{m 1}}\right)\right]\left(C_{e q}+C_{D B}\right)} \tag{6.24}
\end{equation*}
$$

\$\$

We should point out that the sign of $\omega_{\text {in }}$ and $\omega_{\text {out }}$ in the above equations is positive because we eventually write the denominator of the transfer function in the form of $\left(1+s / \omega_{\text {in }}\right)\left(1+s / \omega_{\text {out }}\right)$; i.e., the denominator vanishes at $s=-\omega_{i n}$ and $s=-\omega_{\text {out }}$. Alternatively, we could express the values of $\omega_{\text {in }}$ and $\omega_{\text {out }}$ with a negative sign and hence write the denominator as $\left(1-s / \omega_{\text {in }}\right)\left(1-s / \omega_{\text {out }}\right)$. We adopt the former notation in this book. We then surmise that the transfer function is

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}(s)=\frac{-g_{m} R_{D}}{\left(1+\frac{s}{\omega_{\text {in }}}\right)\left(1+\frac{s}{\omega_{\text {out }}}\right)} \tag{6.25}
\end{equation*}
$$

Note that $r_{O 1}$ and any load capacitance can easily be included here.
The primary error in this estimation is that we have not considered the existence of zeros in the circuit. Another concern stems from approximating the gain of the amplifier by $-g_{m} R_{D}$ whereas in reality the gain varies with frequency (for example, due to the capacitance at the output node).

Direct Analysis We now obtain the exact transfer function, investigating the validity of the above approach. Using the equivalent circuit depicted in Fig. 6.15, we can sum the currents at each node:

$$
\begin{align*}
\frac{V_{X}-V_{\text {in }}}{R_{S}}+V_{X} C_{G S} s+\left(V_{X}-V_{\text {out }}\right) C_{G D} s & =0  \tag{6.26}\\
\left(V_{\text {out }}-V_{X}\right) C_{G D} s+g_{m} V_{X}+V_{\text {out }}\left(\frac{1}{R_{D}}+C_{D B} S\right) & =0 \tag{6.27}
\end{align*}
$$

image_name:Figure 6.15 Equivalent circuit of Fig. 6.13.
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: CGS, type: Capacitor, value: CGS, ports: {Np: X, Nn: GND}
name: CGD, type: Capacitor, value: CGD, ports: {Np: X, Nn: Vout}
name: gmVx, type: VoltageControlledCurrentSource, ports: {Np: Vout, Nn: GND}
name: CDB, type: Capacitor, value: CDB, ports: {Np: Vout, Nn: GND}
name: RD, type: Resistor, value: RD, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is an equivalent model for analyzing the transfer function, with a voltage source Vin, resistors, capacitors, and a voltage-controlled current source representing the transconductance gmVx.

From (6.27), $V_{X}$ is obtained as

$$
\begin{equation*}
V_{X}=-\frac{V_{\text {out }}\left(C_{G D} s+\frac{1}{R_{D}}+C_{D B} s\right)}{g_{m}-C_{G D} s} \tag{6.28}
\end{equation*}
$$

which, upon substitution in (6.26), yields

$$
\begin{equation*}
-V_{\text {out }} \frac{\left[R_{S}^{-1}+\left(C_{G S}+C_{G D}\right) s\right]\left[R_{D}^{-1}+\left(C_{G D}+C_{D B}\right) s\right]}{g_{m}-C_{G D} s}-V_{\text {out }} C_{G D} s=\frac{V_{\text {in }}}{R_{S}} \tag{6.29}
\end{equation*}
$$

That is

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}(s)=\frac{\left(C_{G D} s-g_{m}\right) R_{D}}{R_{S} R_{D} \xi s^{2}+\left[R_{S}\left(1+g_{m} R_{D}\right) C_{G D}+R_{S} C_{G S}+R_{D}\left(C_{G D}+C_{D B}\right)\right] s+1} \tag{6.30}
\end{equation*}
$$

where $\xi=C_{G S} C_{G D}+C_{G S} C_{D B}+C_{G D} C_{D B}$. Note that the transfer function is of second order even though the circuit contains three capacitors. This is because the capacitors form a "loop," allowing only two independent initial conditions in the circuit and hence yielding a second-order differential equation for the time response.

#### Example 6.6

A student considers only $C_{G D}$ in Fig. 6.13(a) so as to obtain a one-pole response, reasons that the voltage gain drops by 3 dB (by a factor of $=\sqrt{2}$ ) at the pole frequency, and concludes that a better approximation of the Miller effect should multiply $C_{G D}$ by $1+g_{m} R_{D} \sqrt{2}$. Explain the flaw in this reasoning.

#### Solution

Setting $C_{G S}$ and $C_{D B}$ to zero, we obtain

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}(s)=\frac{\left(C_{G D} s-g_{m}\right) R_{D}}{\frac{s}{\omega_{0}}+1} \tag{6.31}
\end{equation*}
$$

where $\omega_{0}=R_{S}\left(1+g_{m} R_{D}\right) C_{G D}+R_{D} C_{G D}$. We note that $C_{G D}$ is multiplied by $1+g_{m} R_{D}$ in this exact analysis. So where is the flaw in the student's argument? It is true that the voltage gain in Fig. 6.13(a) falls by $\sqrt{2}$ at $\omega_{0}$, but this gain would be from $V_{\text {in }}$ to $V_{\text {out }}$ and not the gain seen by $C_{G D}$. The reader can readily express the transfer function from node $X$ to $V_{\text {out }}$ as

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{X}}(s)=\frac{\left(C_{G D} s-g_{m}\right) R_{D}}{R_{D} C_{G D}+1} \tag{6.32}
\end{equation*}
$$

observing that this gain begins to roll off at a higher frequency, namely, at $1 /\left(R_{D} C_{G D}\right)$. Thus, the multiplication of $C_{G D}$ by $1+g_{m} R_{D}$ is still justified.

Special Cases If manipulated judiciously, Eq. (6.30) reveals several interesting points about the circuit. While the denominator appears rather complicated, it can yield intuitive expressions for the two poles, $\omega_{p 1}$ and $\omega_{p 2}$, if we assume that $\left|\omega_{p 1}\right| \ll\left|\omega_{p 2}\right|$. This is called the "dominant pole" approximation. Writing the denominator as

$$
\begin{align*}
D & =\left(\frac{s}{\omega_{p 1}}+1\right)\left(\frac{s}{\omega_{p 2}}+1\right)  \tag{6.33}\\
& =\frac{s^{2}}{\omega_{p 1} \omega_{p 2}}+\left(\frac{1}{\omega_{p 1}}+\frac{1}{\omega_{p 2}}\right) s+1 \tag{6.34}
\end{align*}
$$

we recognize that the coefficient of $s$ is approximately equal to $1 / \omega_{p 1}$ if $\omega_{p 2}$ is much farther from the origin. It follows from (6.30) that the dominant pole is given by

$$
\begin{equation*}
\omega_{p 1}=\frac{1}{R_{S}\left(1+g_{m} R_{D}\right) C_{G D}+R_{S} C_{G S}+R_{D}\left(C_{G D}+C_{D B}\right)} \tag{6.35}
\end{equation*}
$$

How does this compare with the "input" pole given by (6.21)? The only difference results from the term $R_{D}\left(C_{G D}+C_{D B}\right)$, which may be negligible in some cases. The key point here is that the intuitive approach of associating a pole with the input node provides a rough estimate with much less effort. We also note that the Miller multiplication of $C_{G D}$ by the low-frequency gain of the amplifier is relatively accurate in this case. Of course, for a given set of values, we must check to ensure that $\omega_{p 1} \ll \omega_{p 2}$.

Other special cases are also of interest. We consider the case of $C_{G D}=0$ in Problem 6.26 and the case of $R_{D}=\infty$ below.

#### Example 6.7

The circuit shown in Fig. 6.16(a) is a special case where $R_{D} \rightarrow \infty$. Calculate the transfer function (with $\lambda=0$ ) and explain why the Miller effect vanishes as $C_{D B}$ (or the load capacitance) increases.
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: CGS, type: Capacitor, value: CGS, ports: {Np: X, Nn: GND}
name: CGD, type: Capacitor, value: CGD, ports: {Np: X, Nn: Vout}
name: CDB, type: Capacitor, value: CDB, ports: {Np: Vout, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: X}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: Vout}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a common-source NMOS amplifier with a load capacitance CDB. The transfer function shows two poles, with the Miller effect diminishing as CDB increases. The Bode plot indicates a -20 dB/decade slope initially, transitioning to -40 dB/decade after the pole at ωp2.
image_name:(b)
description:The graph in part (b) is a Bode plot representing the magnitude response of a transfer function. The x-axis is labeled with frequency \( \omega \) on a logarithmic scale, and the y-axis is labeled with the magnitude of the transfer function in decibels \( 20 \log \left| \frac{V_{\text{out}}}{V_{\text{in}}}(j\omega) \right| \) .

**Overall Behavior and Trends:**
- The plot starts at 0 dB, indicating that at low frequencies, the magnitude of the output equals the magnitude of the input.
- As the frequency increases, the plot shows a downward slope at a rate of \(-20\) dB/decade, indicating a single-pole roll-off.
- At a certain frequency \( \omega_{p2} \), marked by a vertical dashed line, the slope steepens to \(-40\) dB/decade, indicating the presence of a second pole.

**Key Features and Technical Details:**
- The initial slope of \(-20\) dB/decade corresponds to the dominance of the first pole.
- The transition to a \(-40\) dB/decade slope at \( \omega_{p2} \) suggests the influence of a second pole, which further attenuates the signal at higher frequencies.

**Annotations and Specific Data Points:**
- The plot includes annotations indicating the slopes of \(-20\) dB/decade and \(-40\) dB/decade.
- The frequency \( \omega_{p2} \) is a critical point where the behavior of the system changes due to the second pole, although its exact value is not provided in the graph.

Figure 6.16

#### Solution

Using (6.30) and letting $R_{D}$ approach infinity, we have

$$
\begin{align*}
\frac{V_{\text {out }}}{V_{\text {in }}}(s) & =\frac{C_{G D} s-g_{m}}{R_{S} \xi s^{2}+\left[g_{m} R_{S} C_{G D}+\left(C_{G D}+C_{D B}\right)\right] s}  \tag{6.36}\\
& =\frac{C_{G D} s-g_{m}}{s\left[R_{S}\left(C_{G S} C_{G D}+C_{G S} C_{D B}+C_{G D} C_{D B}\right) s+\left(g_{m} R_{S}+1\right) C_{G D}+C_{D B}\right]}
\end{align*}
$$

As expected, the circuit exhibits two poles-one at the origin because the dc gain is infinity [Fig. 6.16(b)]. The magnitude of the other pole is given by

$$
\begin{equation*}
\omega_{p 2} \approx \frac{\left(1+g_{m} R_{S}\right) C_{G D}+C_{D B}}{R_{S}\left(C_{G D} C_{G S}+C_{G S} C_{D B}+C_{G D} C_{D B}\right)} \tag{6.37}
\end{equation*}
$$

For a large $C_{D B}$ or load capacitance, this expression reduces to

$$
\begin{equation*}
\omega_{p 2} \approx \frac{1}{R_{S}\left(C_{G S}+C_{G D}\right)} \tag{6.38}
\end{equation*}
$$

indicating that $C_{G D}$ experiences no Miller multiplication. This can be explained by noting that, for a large $C_{D B}$, the voltage gain from node $X$ to the output begins to drop even at low frequencies. As a result, for frequencies close to $\left[R_{S}\left(C_{G S}+C_{G D}\right)\right]^{-1}$, the effective gain is quite small and $C_{G D}\left(1-A_{v}\right) \approx C_{G D}$. Such a case is an example where the application of the Miller effect using low-frequency gain does not provide a reasonable estimate.

From (6.30) and applying the dominant pole approximation, we can also estimate the second pole of the CS stage of Fig. 6.13(a). Since the coefficient of $s^{2}$ is equal to $\left(\omega_{p 1} \omega_{p 2}\right)^{-1}$, we have

$$
\begin{align*}
\omega_{p 2} & =\frac{1}{\omega_{p 1}} \cdot \frac{1}{R_{S} R_{D}\left(C_{G S} C_{G D}+C_{G S} C_{D B}+C_{G D} C_{D B}\right)}  \tag{6.39}\\
& =\frac{R_{S}\left(1+g_{m} R_{D}\right) C_{G D}+R_{S} C_{G S}+R_{D}\left(C_{G D}+C_{D B}\right)}{R_{S} R_{D}\left(C_{G S} C_{G D}+C_{G S} C_{D B}+C_{G D} C_{D B}\right)} \tag{6.40}
\end{align*}
$$

We emphasize that these results hold only if $\omega_{p 1} \ll \omega_{p 2}$.
As a special case, if $C_{G S} \gg\left(1+g_{m} R_{D}\right) C_{G D}+R_{D}\left(C_{G D}+C_{D B}\right) / R_{S}$, then

$$
\begin{align*}
\omega_{p 2} & \approx \frac{R_{S} C_{G S}}{R_{S} R_{D}\left(C_{G S} C_{G D}+C_{G S} C_{D B}\right)}  \tag{6.41}\\
& =\frac{1}{R_{D}\left(C_{G D}+C_{D B}\right)} \tag{6.42}
\end{align*}
$$

the same as (6.22). Thus, the "output" pole approach is valid only if $C_{G S}$ dominates the response.

The transfer function of (6.30) exhibits a zero given by $\omega_{z}=+g_{m} / C_{G D}$, an effect not predicted by Miller's approximation and (6.25). Located in the right half plane, the zero arises from direct coupling of the input to the output through $C_{G D}$. As illustrated in Fig. 6.17, $C_{G D}$ provides a feedthrough path that conducts the input signal to the output at very high frequencies, resulting in a slope in the frequency response that is less negative than $-40 \mathrm{~dB} / \mathrm{dec}$. Note that $g_{m} / C_{G D}>g_{m} / C_{G S}$ because $C_{G D}<C_{G S}$, implying that the zero lies beyond the transistor's $f_{T}$. However, as explained in Chapter 10, this zero falls to lower frequencies in cases where we deliberately add a capacitor between the gate and the drain, introducing other difficulties.
image_name:Figure 6.17 Feedforward path through C_{G D}
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: g1}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: M, type: NMOS, ports: {S: GND, D: Vout, G: g1}
name: Cgd, type: Capacitor, value: Cgd, ports: {N1: g1, N2: Vout}
]
extrainfo:The circuit diagram shows a feedforward path through CGD and a main path through an NMOS transistor g1. The frequency response graph indicates a zero at frequency ωz, with slopes of -20 dB/dec, -40 dB/dec, and back to -20 dB/dec.
image_name:Figure 6.17 Feedforward path through C_{G D} (log-log scale)
description:The graph depicted is a Bode plot on a log-log scale, representing the frequency response of a feedforward path through the capacitance \( C_{GD} \). The x-axis is labeled with frequency \( \omega \) on a logarithmic scale, while the y-axis represents the magnitude of the transfer function in decibels, specifically \( 20 \log \left| \frac{V_{out}}{V_{in}}(j\omega) \right| \).

Overall Behavior and Trends:
- **Initial Flat Region:** The graph starts with a flat region indicating a constant gain at low frequencies.
- **First Slope (-20 dB/dec):** As frequency increases, the plot shows a slope of \(-20 \text{ dB/decade}\) starting at \( \omega_{p1} \), indicating the presence of a pole.
- **Steeper Slope (-40 dB/dec):** The slope becomes steeper at \( \omega_{p2} \) with \(-40 \text{ dB/decade}\), signifying another pole.
- **Return to Slope (-20 dB/dec):** At \( \omega_{z} \), the slope returns to \(-20 \text{ dB/decade}\), indicating the effect of a zero.

Key Features and Technical Details:
- **Poles and Zero:**
- \( \omega_{p1} \) and \( \omega_{p2} \) are the frequencies where the poles occur, causing the initial and subsequent slope changes.
- \( \omega_{z} \) is the frequency where the zero occurs, reducing the slope.
- **Gain Levels:** The gain decreases as the frequency increases, with distinct changes at the poles and zero.

Annotations and Specific Data Points:
- The graph includes dashed vertical lines at \( \omega_{p1} \), \( \omega_{p2} \), and \( \omega_{z} \), marking the critical frequencies where the slope changes occur.

This Bode plot effectively illustrates the impact of the feedforward path through \( C_{GD} \) on the frequency response, highlighting the roles of poles and zeros in shaping the response curve.

Figure 6.17 Feedforward path through $C_{G D}$ (log-log scale).
The zero, $s_{z}$, can also be computed by noting that the transfer function $V_{\text {out }}(s) / V_{\text {in }}(s)$ must drop to zero for $s=s_{z}$. For a finite $V_{i n}$, this means that $V_{\text {out }}\left(s_{z}\right)=0$, and hence the output can be shorted to ground at this (possibly complex) frequency with no current flowing through $R_{D}$ or the short (Fig. 6.18). Therefore, the currents through $C_{G D}$ and $M_{1}$ are equal and opposite:

$$
\begin{equation*}
V_{1} C_{G D} s_{z}=g_{m} V_{1} \tag{6.43}
\end{equation*}
$$

That is, $s_{z}=+g_{m} / C_{G D} .^{3}$

image_name:Figure 6.18 Calculation of the zero in a CS stage.
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: g1}
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: g1, Nn: GND}
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: GND, Nn: g1}
name: RD, type: Resistor, value: RD, ports: {N1: GND, N2: VDD}
name: M1, type: NMOS, ports: {S: GND, D: GND, G: g1}
]
extrainfo:This circuit represents a common-source amplifier stage with a zero in the transfer function due to the cancellation of signals through two paths. The NMOS transistor M1 is used for amplification, with capacitors Cgs and Cgd representing parasitic capacitances. The output current Iout is zero, indicating a specific frequency condition where the output can be shorted to ground.

#### Example 6.8

We have seen that the signals traveling through two paths within an amplifier may cancel each other at one frequency, creating a zero in the transfer function (Fig. 6.19). Can this occur if $H_{1}(s)$ and $H_{2}(s)$ are first-order low-pass circuits?
image_name:Figure 6.19
description:The system block diagram in Figure 6.19 illustrates a parallel signal processing configuration. The primary components of the system are two blocks labeled \( H_1(s) \) and \( H_2(s) \), which represent two separate transfer functions. These blocks are designed to process an input signal \( V_{in} \) and contribute to the output signal \( V_{out} \).

1. **Main Components:**
- **\( H_1(s) \) and \( H_2(s) \):** These are the key blocks in the system, each representing a first-order low-pass filter with their respective transfer functions. \( H_1(s) \) and \( H_2(s) \) are modeled by \( \frac{A_1}{1+s/\omega_{p1}} \) and \( \frac{A_2}{1+s/\omega_{p2}} \) respectively, where \( A_1 \) and \( A_2 \) are the gains, and \( \omega_{p1} \) and \( \omega_{p2} \) are the pole frequencies.

2. **Flow of Information or Control:**
- The input signal \( V_{in} \) is divided and simultaneously fed into both \( H_1(s) \) and \( H_2(s) \). The outputs from these two blocks are then summed together at a summing junction to produce the output signal \( V_{out} \).
- The diagram shows a parallel signal path where the input is split and processed through two different pathways before being recombined. This configuration can lead to the cancellation of signals at certain frequencies, resulting in a zero in the transfer function.

3. **Labels, Annotations, and Key Indicators:**
- The diagram is annotated with input \( V_{in} \) and output \( V_{out} \) points, indicating the flow of the signal through the system.
- The summing junction is indicated by a circle with a plus sign, showing the combination of the two processed signals.

4. **Overall System Function:**
- The overall function of this system is to process an input signal through two parallel low-pass filters and combine the results. The structure is particularly useful for analyzing the conditions under which the signals might cancel each other out, creating a zero in the transfer function. This cancellation occurs when the contributions from \( H_1(s) \) and \( H_2(s) \) are equal and opposite at a specific frequency.

#### Solution

Modeling $H_{1}(s)$ by $A_{1} /\left(1+s / \omega_{p 1}\right)$ and $H_{2}(s)$ by $A_{2} /\left(1+s / \omega_{p 2}\right)$, we have

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}(s)=\frac{\left(\frac{A_{1}}{\omega_{p 2}}+\frac{A_{2}}{\omega_{p 1}}\right) s+A_{1}+A_{2}}{\left(1+\frac{s}{\omega_{p 1}}\right)\left(1+\frac{s}{\omega_{p 2}}\right)} \tag{6.44}
\end{equation*}
$$

Indeed, the overall transfer function contains a zero.

#### Example 6.9

Determine the transfer function of the complementary CS stage shown in Fig. 6.20(a).
image_name:Figure 6.20(a)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: g1g2}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: g1g2}
name: M2, type: PMOS, ports: {S: VDD, D: Vout, G: g1g2}
]
extrainfo:The circuit is a complementary common-source (CS) amplifier stage, using both NMOS and PMOS transistors for amplification. The input is applied at Vin through a resistor RS, and the output is taken at Vout. The gate of both transistors is connected to the same node g2.

image_name:Figure 6.20(b)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: g1g2}
name: CGS1 + CGS2, type: Capacitor, value: CGS1 + CGS2, ports: {Np: g1g2, Nn: GND}
name: CGD1 + CGD2, type: Capacitor, value: CGD1 + CGD2, ports: {Np: g1g2, Nn: Vout}
name: (gm1 + gm2)V1, type: CurrentSource, value: (gm1 + gm2)V1, ports: {Np: g2, Nn: Vout}
name: rO1 || rO2, type: Resistor, value: rO1 || rO2, ports: {N1: Vout, N2: GND}
name: CDB1 + CDB2, type: Capacitor, value: CDB1 + CDB2, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a small-signal model of a complementary common-source amplifier stage. It includes parasitic capacitances and a dependent current source representing the transconductance of the combined NMOS and PMOS transistors. The input is applied at Vin, and the output is taken at Vout.

#### Solution

Since the corresponding terminals of $M_{1}$ and $M_{2}$ are shorted to one another in the small-signal model, we merge the two transistors, drawing the equivalent circuit as shown in Fig. 6.20(b). The circuit thus has the same transfer function as the simple CS stage studied above.

In high-speed applications, the input impedance of the common-source stage is also important. With the aid of Miller's approximation, we have from Fig. 6.21(a)

$$
\begin{equation*}
Z_{i n}=\frac{1}{\left[C_{G S}+\left(1+g_{m} R_{D}\right) C_{G D}\right] s} \tag{6.45}
\end{equation*}
$$

image_name:Figure 6.21(a)
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: CGD, type: Capacitor, value: CGD, ports: {Np: Vin, Nn: Vout}
name: CDB, type: Capacitor, value: CDB, ports: {Np: Vout, Nn: GND}
name: CGS, type: Capacitor, value: CGS, ports: {Np: Vin, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
]
extrainfo:The circuit diagram in (a) represents a common-source amplifier with the input impedance Zin. It includes an NMOS transistor M1, and the capacitors CGD, CDB, and CGS are used to model the parasitic capacitances. The resistor RD is connected between VDD and the output node Vout. The voltage source Vin provides the input signal.
image_name:Figure 6.21(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vx}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: CGD, type: Capacitor, value: CGD, ports: {Np: Vx, Nn: Vout}
name: CDB, type: Capacitor, value: CDB, ports: {Np: Vout, Nn: GND}
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Vx, Nn: GND}
]
extrainfo:The circuit is a common-source amplifier with an NMOS transistor M1. The input impedance is affected by the capacitors CGD and CDB. A voltage source Vx is used to model the input voltage.
image_name:Figure 6.21(c)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vout}
name: CDB, type: Capacitor, value: CDB, ports: {Np: Vout, Nn: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit diagram is a common-source amplifier stage with feedback from the output to the input through Zin. The NMOS transistor M1 is configured with its gate and drain connected to the output node Vout, providing a feedback path. The capacitors CGD and CDB are used for frequency compensation.

Figure 6.21 Calculation of input impedance of a CS stage.
But at high frequencies, the effect of the output node capacitance must be taken into account. Ignoring $C_{G S}$ for the moment and using the circuit of Fig. 6.21(b), we add the voltage drops across $R_{D} \|\left(C_{D B} s\right)^{-1}$ and $C_{G D}$, equating the result to $V_{X}$ :

$$
\begin{equation*}
\left(I_{X}-g_{m} V_{X}\right) \frac{R_{D}}{1+R_{D} C_{D B} S}+\frac{I_{X}}{C_{G D} S}=V_{X} \tag{6.46}
\end{equation*}
$$

and hence

$$
\begin{equation*}
\frac{V_{X}}{I_{X}}=\frac{1+R_{D}\left(C_{G D}+C_{D B}\right) s}{C_{G D} s\left(1+g_{m} R_{D}+R_{D} C_{D B} s\right)} \tag{6.47}
\end{equation*}
$$

The actual input impedance consists of the parallel combination of (6.47) and $1 /\left(C_{G S} S\right)$.
As a special case, suppose that at the frequency of interest, $\left|R_{D}\left(C_{G D}+C_{D B}\right) s\right| \ll 1$ and $\left|R_{D} C_{D B} s\right| \ll$ $1+g_{m} R_{D}$. Then, (6.47) reduces to $\left[\left(1+g_{m} R_{D}\right) C_{G D} S\right]^{-1}$ (as expected), indicating that the input impedance is primarily capacitive. At higher frequencies, however, (6.47) contains both real and imaginary parts. In fact, if $C_{G D}$ is large, it provides a low-impedance path between the gate and the drain of $M_{1}$, yielding the equivalent circuit of Fig. 6.21(c) and suggesting that $1 / g_{m 1}$ and $R_{D}$ appear in parallel with the input.

#### Example 6.10

Explain what happens to Eq. (6.47) if the circuit drives a large load capacitance.

#### Solution

Merged with $C_{D B}$, the large load capacitance reduces the numerator to $R_{D} C_{D B} S$ and the denominator to $C_{G D} s\left(R_{D} C_{D B} s\right)$, yielding $V_{X} / I_{X} \approx 1 /\left(C_{G D} s\right)$. In a manner similar to that in Example 6.7, the large load capacitance lowers the gain at high frequencies, suppressing Miller multiplication of $C_{G D}$.

## 6.3 ■ Source Followers
Source followers are occasionally employed as level shifters or buffers, affecting the overall frequency response. Consider the circuit depicted in Fig. 6.22(a), where $C_{L}$ represents the total capacitance seen at the output node to ground, including $C_{S B 1}$. The strong interaction between nodes $X$ and $Y$ through $C_{G S}$ in Fig. 6.22(a) makes it difficult to associate a pole with each node in a source follower. Neglecting channel-length modulation and body effect for simplicity and using the equivalent circuit shown in Fig. 6.22(b), we sum the currents at the output node:

$$
\begin{equation*}
V_{1} C_{G S} s+g_{m} V_{1}=V_{\text {out }} C_{L} s \tag{6.48}
\end{equation*}
$$

obtaining

$$
\begin{equation*}
V_{1}=\frac{C_{L} s}{g_{m}+C_{G S} S} V_{\text {out }} \tag{6.49}
\end{equation*}
$$

Also, noting that the voltage across $C_{G D}$ is equal to $V_{1}+V_{\text {out }}$ and beginning from $V_{i n}$, we add the voltage across $R_{S}$ to $V_{1}$ and $V_{\text {out }}$ :

$$
\begin{equation*}
V_{\text {in }}=R_{S}\left[V_{1} C_{G S} s+\left(V_{1}+V_{\text {out }}\right) C_{G D} s\right]+V_{1}+V_{\text {out }} \tag{6.50}
\end{equation*}
$$

Substituting for $V_{1}$ from (6.49), we have

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}(s)=\frac{g_{m}+C_{G S} s}{R_{S}\left(C_{G S} C_{L}+C_{G S} C_{G D}+C_{G D} C_{L}\right) s^{2}+\left(g_{m} R_{S} C_{G D}+C_{L}+C_{G S}\right) s+g_{m}} \tag{6.51}
\end{equation*}
$$

Interestingly, the transfer function contains a zero in the left half plane (and near the $f_{T}$ ). This is because the signal conducted by $C_{G S}$ at high frequencies adds with the same polarity to the signal produced by the intrinsic transistor. We study some special cases below.
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: M1, type: NMOS, ports: {S: Y, D: VDD, G: X}
name: I1, type: CurrentSource, value: I1, ports: {Np: Y, Nn: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a source follower configuration with an NMOS transistor. The input voltage is applied through a resistor RS, and the output is taken across a capacitor CL. A current source I1 is connected to the source of the NMOS, which is grounded.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: "Vin", N2: X2}
name: CGD, type: Capacitor, value: CGD, ports: {Np: X2, Nn: GND}
name: CGS, type: Capacitor, value: CGS, ports: {Np: X2, Nn: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: X2, Nn: Vout}
name: gmV1, type: VoltageControlledCurrentSource, value: gmV1, ports: {Np: V1, Nn: Vout}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND'}
]
extrainfo:The circuit represents a high-frequency equivalent of a source follower. It includes capacitors CGD and CGS connected to a node X2, and a voltage-controlled current source gmV1.

Figure 6.22 (a) Source follower; (b) high-frequency equivalent circuit.

#### Example 6.11

Examine the source follower transfer function if $C_{L}=0$.

#### Solution

We have

$$
\begin{align*}
\frac{V_{\text {out }}}{V_{\text {in }}} & =\frac{g_{m}+C_{G S} s}{R_{S} C_{G S} C_{G D} s^{2}+\left(g_{m} R_{S} C_{G D}+C_{G S}\right) s+g_{m}}  \tag{6.52}\\
& =\frac{g_{m}+C_{G S} s}{\left(1+R_{S} C_{G D} s\right)\left(g_{m}+C_{G S} s\right)}  \tag{6.53}\\
& =\frac{1}{1+R_{S} C_{G D} s} \tag{6.54}
\end{align*}
$$

The circuit now has only one pole at the input. Why does $C_{G S}$ disappear here? This is because, in the absence of channel-length modulation and body effect, the voltage gain from the gate to the source is equal to unity. Since a change of $\Delta V$ at the gate translates to an equal change at the source (Fig. 6.23), no current flows through $C_{G S}$. Consequently, $C_{G S}$ contributes neither a zero nor a pole. We say $C_{G S}$ is "bootstrapped" by the source follower. With $\lambda, \gamma>0$, the output change is less than $\Delta V$, requiring some change in the voltage across $C_{G S}$.
image_name:Figure 6.23 Bootstrapping of C_{GS} in a source follower
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: CGS, type: Capacitor, ports: {Np: X, Nn: Y}
name: M1, type: NMOS, ports: {S: Y, D: VDD, G: X}
name: I1, type: CurrentSource, value: I1, ports: {Np: Y, Nn: GND}
]
extrainfo:The circuit is a source follower configuration with bootstrapping of CGS. The input voltage Vin affects the gate of NMOS M1, and the source follows this voltage, affecting the current source I1 connected to the source.

Figure 6.23 Bootstrapping of $C_{G S}$ in a source follower.

If the two poles of (6.51) are assumed far apart, then the lower one has a magnitude of

$$
\begin{align*}
\omega_{p 1} & \approx \frac{g_{m}}{g_{m} R_{S} C_{G D}+C_{L}+C_{G S}}  \tag{6.55}\\
& =\frac{1}{R_{S} C_{G D}+\frac{C_{L}+C_{G S}}{g_{m}}} \tag{6.56}
\end{align*}
$$

Also, if $R_{S}=0$, then $\omega_{p 1}=g_{m} /\left(C_{L}+C_{G S}\right)$ —as expected.
Let us now calculate the input impedance of the circuit, noting that $C_{G D}$ simply shunts the input and can be ignored initially. Shown in Fig. 6.24, the equivalent circuit includes body effect, but channel-length modulation can also be added by replacing $1 / g_{m b}$ with $\left(1 / g_{m b}\right) \| r_{O}$. The small-signal gate-source voltage of $M_{1}$ is equal to $I_{X} /\left(C_{G S} s\right)$, giving a source current of $g_{m} I_{X} /\left(C_{G S} s\right)$. Starting from the input and adding
image_name:Figure 6.24 Calculation of source follower input impedance.
description:
[
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Vx, Nn: GND}
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: g1, Nn: Vout}
name: M1, type: NMOS, ports: {S: Vout, D: VDD, G: Vx}
name: 1/gmb, type: Resistor, value: 1/gmb, ports: {N1: Vout, N2: GND}
name: Cl, type: Capacitor, value: Cl, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit analyzes the input impedance of a source follower. It includes a voltage source Vx, a capacitor Cgs shunting the input, an NMOS transistor M1, a resistor representing 1/gmb, and a load capacitor Cl. The circuit considers body effect and channel-length modulation.

the voltages, we have

$$
\begin{equation*}
V_{X}=\frac{I_{X}}{C_{G S} s}+\left(I_{X}+\frac{g_{m} I_{X}}{C_{G S} s}\right)\left(\frac{1}{g_{m b}} \| \frac{1}{C_{L} s}\right) \tag{6.57}
\end{equation*}
$$

that is

$$
\begin{equation*}
Z_{i n}=\frac{1}{C_{G S} S}+\left(1+\frac{g_{m}}{C_{G S} S}\right) \frac{1}{g_{m b}+C_{L} S} \tag{6.58}
\end{equation*}
$$

We consider some special cases. First, if $g_{m b}=0$ and $C_{L}=0$, then $Z_{i n}=\infty$, because $C_{G S}$ is entirely bootstrapped by the source follower and draws no current from the input. Second, at relatively low frequencies, $g_{m b} \gg\left|C_{L} s\right|$ and

$$
\begin{equation*}
Z_{i n} \approx \frac{1}{C_{G S} S}\left(1+\frac{g_{m}}{g_{m b}}\right)+\frac{1}{g_{m b}} \tag{6.59}
\end{equation*}
$$

indicating that the equivalent input capacitance is equal to $C_{G S} g_{m b} /\left(g_{m}+g_{m b}\right)$ and hence quite less than $C_{G S}$. In other words, the overall input capacitance is equal to $C_{G D}$ plus a fraction of $C_{G S}$-again because of bootstrapping.

#### Example 6.12

Apply Miller's approximation to the above circuit if $C_{L}=0$.

#### Solution

As illustrated in Fig. 6.25, the low-frequency gain from the gate to the source is equal to $\left(1 / g_{m b}\right) /\left[\left(1 / g_{m}\right)+\right.$ $\left.\left(1 / g_{m b}\right)\right]=g_{m} /\left(g_{m}+g_{m b}\right)$. The Miller multiplication of $C_{G S}$ at the input is thus equal to $C_{G S}\left[1-g_{m} /\left(g_{m}+g_{m b}\right)\right]=$ $C_{G S} g_{m b} /\left(g_{m}+g_{m b}\right)$.
image_name:Figure 6.25
description:
[
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Vx, Nn: GND}
name: M1, type: NMOS, ports: {S: Y, D: VDD, G: X}
name: C_GS, type: Capacitor, value: C_GS, ports: {Np: X, Nn: Y}
name: 1/g_mb, type: Resistor, value: 1/g_mb, ports: {N1: Y, N2: GND}
]
extrainfo:The circuit applies Miller's approximation with a focus on the gate-source capacitance C_GS and its effect on the input impedance at high frequencies. The NMOS transistor M1 is used in the configuration, and the circuit involves a voltage source Vx and a resistor with value 1/g_mb.


At high frequencies, $g_{m b} \ll\left|C_{L} s\right|$ and

$$
\begin{equation*}
Z_{i n} \approx \frac{1}{C_{G S} s}+\frac{1}{C_{L} S}+\frac{g_{m}}{C_{G S} C_{L} s^{2}} \tag{6.60}
\end{equation*}
$$

For a given $s=j \omega$, the input impedance consists of the series combination of capacitors $C_{G S}$ and $C_{L}$ and a negative resistance equal to $-g_{m} /\left(C_{G S} C_{L} \omega^{2}\right)$ (Fig. 6.26). The negative resistance property can be utilized in oscillators (Chapter 15). It is important to bear in mind that a source follower driving a load capacitance exhibits a negative input resistance, possibly causing instability.
image_name:Figure 6.26 Negative resistance seen at the input of a source follower.
description:
[
name: M1, type: NMOS, ports: {S: S1, D: VDD, G: Vin}
name: CGS, type: Capacitor, value: CGS, ports: {Np: Vin, Nn: s1}
name: CL, type: Capacitor, value: CL, ports: {Np: S1, Nn: GND}
]
extrainfo:The circuit depicts a source follower configuration with an NMOS transistor M1. It includes capacitors CGS and CL, which form a series combination at the input. The negative resistance property is utilized for stability analysis in oscillators.

#### Example 6.13

Neglecting channel-length modulation and body effect, calculate the transfer function of the circuit shown in Fig. 6.27(a).
image_name:Figure 6.27(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: M1, type: NMOS, ports: {S: Y, D: VDD, G: X}
name: M2, type: NMOS, ports: {S: GND, D: X, G: Y}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
name: Is, type: CurrentSource, ports: {Np: Y, Nn: GND}
]
extrainfo:The circuit is a source follower configuration utilizing NMOS transistors M1 and M2. It includes capacitors Cx, Cxy, and CY for stability and frequency response adjustments. The voltage-controlled current sources gm1V1 and gm2V2 indicate feedback mechanisms for controlling the output.
image_name:Figure 6.27(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: CX, type: Capacitor, value: CX, ports: {Np: X, Nn: GND}
name: gm2V2, type: VoltageControlledCurrentSource, ports: {Np: X, Nn: GND}
name: CXY, type: Capacitor, value: CXY, ports: {Np: X, Nn: Y}
name: gm1V1, type: VoltageControlledCurrentSource, ports: {Np: GND Nn: Y(Vout)}
name: CY, type: Capacitor, value: CY, ports: {Np: Y, Nn: GND}
]
extrainfo:The circuit is a small-signal equivalent model of a two-stage amplifier with feedback. It includes capacitors CX, CXY, and CY, and voltage-controlled current sources gm2V2 and gm1V1. The circuit is used for analyzing the frequency response and stability of the amplifier.

#### Solution

Let us first identify all of the capacitances in the circuit. At node $X, C_{G D 1}$ and $C_{D B 2}$ are connected to ground and $C_{G S 1}$ and $C_{G D 2}$ to $Y$. At node $Y, C_{S B 1}, C_{G S 2}$, and $C_{L}$ are connected to ground. Similar to the source follower of Fig. 6.22(b), this circuit has three capacitances in a loop and hence a second-order transfer function. Using the equivalent circuit shown in Fig. 6.27(b), where $C_{X}=C_{G D 1}+C_{D B 2}, C_{X Y}=C_{G S 1}+C_{G D 2}$, and $C_{Y}=C_{S B 1}+C_{G S 2}+C_{L}$, we have $V_{1} C_{X Y} s+g_{m 1} V_{1}=V_{\text {out }} C_{Y} s$, and hence $V_{1}=V_{\text {out }} C_{Y} s /\left(C_{X Y} s+g_{m 1}\right)$. Also, since $V_{2}=V_{\text {out }}$, the summation of currents at node $X$ gives

$$
\begin{equation*}
\left(V_{1}+V_{\text {out }}\right) C_{X} s+g_{m 2} V_{\text {out }}+V_{1} C_{X Y} s=\frac{V_{\text {in }}-V_{1}-V_{\text {out }}}{R_{S}} \tag{6.61}
\end{equation*}
$$

Substituting for $V_{1}$ and simplifying the result, we obtain

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}(s)=\frac{g_{m 1}+C_{X Y} s}{R_{S} \xi s^{2}+\left[C_{Y}+g_{m 1} R_{S} C_{X}+\left(1+g_{m 2} R_{S}\right) C_{X Y}\right] s+g_{m 1}\left(1+g_{m 2} R_{S}\right)} \tag{6.62}
\end{equation*}
$$

where $\xi=C_{X} C_{Y}+C_{X} C_{X Y}+C_{Y} C_{X Y}$. As expected, (6.62) reduces to a form similar to (6.51) for $g_{m 2}=0$.

The output impedance of source followers is also of interest. In Fig. 6.22(a), the body effect and $C_{S B}$ simply yield an impedance in parallel with the output. Ignoring this impedance and neglecting $C_{G D}$, we note from the equivalent circuit of Fig. 6.28(a) that $V_{1} C_{G S} s+g_{m} V_{1}=-I_{X}$. Also, $V_{1} C_{G S} s R_{S}+V_{1}=-V_{X}$.
image_name:(a)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: X1}
name: CGS, type: Capacitor, value: CGS, ports: {Np: X1, Nn: VX}
name: VX, type: VoltageSource, value: V1, ports: {Np: Vx, Nn: GND}
name: gmV1, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: Vx}
]
extrainfo:The circuit in Figure 6.28(a) is a source follower configuration used for calculating output impedance. The output impedance Z_out is analyzed as a function of frequency, showing behavior at low and high frequencies. At low frequencies, Z_out approximates 1/gm, while at high frequencies, it approaches RS.
image_name:(b)
description:The graph labeled as "(b)" is a plot of the output impedance \( Z_{\text{out}} \) of a source follower circuit as a function of angular frequency \( \omega \). It is a Bode plot illustrating the impedance behavior across different frequencies.

1. **Axes Labels and Units:**
- The vertical axis represents the magnitude of the output impedance \( Z_{\text{out}} \).
- The horizontal axis represents angular frequency \( \omega \).
- The plot does not specify units explicitly, but typically \( \omega \) is in radians per second, and impedance is in ohms.

2. **Overall Behavior and Trends:**
- At low frequencies, the output impedance \( Z_{\text{out}} \) starts at approximately \( 1/g_m \), where \( g_m \) is the transconductance.
- As the frequency increases, the impedance gradually rises.
- At very high frequencies, the impedance approaches \( R_S \), the source resistance, indicating that the impedance becomes dominated by \( R_S \).

3. **Key Features and Technical Details:**
- The curve shows a smooth transition from a low impedance value \( 1/g_m \) at low frequencies to a higher value \( R_S \) at high frequencies.
- This behavior is typical for a source follower circuit where the capacitive effects become significant at high frequencies, causing the impedance to increase.

4. **Annotations and Specific Data Points:**
- The graph includes a dotted line indicating the level of \( R_S \), showing the asymptotic behavior of the impedance at high frequencies.
- A horizontal line at \( 1/g_m \) marks the starting point of the impedance at low frequencies.

This graph effectively illustrates how the output impedance of a source follower varies with frequency, highlighting the influence of both the transconductance and the source resistance across the frequency spectrum.
image_name:(c)
description:The graph labeled "(c)" is a plot of the magnitude of the output impedance \( |Z_{\text{out}}| \) of a source follower as a function of frequency \( \omega \). It is a Bode plot, showing the relationship between frequency and impedance magnitude.

1. **Axes Labels and Units:**
- The horizontal axis represents frequency \( \omega \), typically measured in radians per second (rad/s).
- The vertical axis represents the magnitude of the output impedance \( |Z_{\text{out}}| \).

2. **Overall Behavior and Trends:**
- At low frequencies, the magnitude of the output impedance starts at approximately \( 1/g_m \), where \( g_m \) is the transconductance.
- As the frequency increases, the impedance magnitude gradually rises.
- At very high frequencies, the impedance approaches \( R_S \), the source resistance, indicating that the capacitive effects diminish and the impedance is dominated by \( R_S \).

3. **Key Features and Technical Details:**
- The curve shows a smooth transition from \( 1/g_m \) to \( R_S \) as frequency increases.
- This behavior reflects the capacitive shorting effect of \( C_{GS} \) at high frequencies, which reduces the effect of \( g_m \) on the impedance.

4. **Annotations and Specific Data Points:**
- There are no specific annotations or numerical markers on the graph, but the key values of \( 1/g_m \) and \( R_S \) are indicated with horizontal dashed lines.

This graph effectively illustrates how the output impedance of a source follower changes with frequency, highlighting the transition from a low impedance determined by the transconductance to a higher impedance dominated by the source resistance.

Figure 6.28 Calculation of source follower output impedance.

Dividing both sides of these equations gives

$$
\begin{align*}
Z_{\text {out }} & =\frac{V_{X}}{I_{X}}  \tag{6.63}\\
& =\frac{R_{S} C_{G S} s+1}{g_{m}+C_{G S} s} \tag{6.64}
\end{align*}
$$

It is instructive to examine the magnitude of this impedance as a function of frequency. At low frequencies, $Z_{\text {out }} \approx 1 / g_{m}$, as expected. At very high frequencies, $Z_{\text {out }} \approx R_{S}$ (because $C_{G S}$ shorts the gate and the source). We therefore surmise that $\left|Z_{\text {out }}\right|$ varies as shown in Figs. 6.28(b) or (c). Which one of these variations is more realistic? Operating as buffers, source followers must lower the output impedance, i.e., $1 / g_{m}<R_{S}$. For this reason, the characteristic shown in Fig. 6.28(c) occurs more commonly than that in Fig. 6.28(b).

The behavior illustrated in Fig. 6.28(c) reveals an important attribute of source followers. Since the output impedance increases with frequency, we postulate that it contains an inductive component. To confirm this guess, we represent $Z_{\text {out }}$ by a first-order passive network, noting that $Z_{\text {out }}$ equals $1 / g_{m}$ at $\omega=0$ and $R_{S}$ at $\omega=\infty$. The network can therefore be realized as shown in Fig. 6.29 because $Z_{1}$ equals $R_{2}$ at $\omega=0$ and $R_{1}+R_{2}$ at $\omega=\infty$. In other words, $Z_{1}=Z_{\text {out }}$ if three conditions hold: $R_{2}=1 / g_{m}$, $R_{1}=R_{S}-1 / g_{m}$, and $L$ is chosen properly.
image_name:Figure 6.29 Equivalent output impedance of a source follower
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: X1, N2: X2}
name: R2, type: Resistor, value: R2, ports: {N1: X1, N2: X3}
name: L, type: Inductor, value: L, ports: {N1: X1, N2: X2}
]
extrainfo:The circuit represents an equivalent output impedance of a source follower with an inductor (L), two resistors (R1, R2), and a component Z1. The network is designed to model the output impedance Z_out as a first-order passive network.

Figure 6.29 Equivalent output impedance of a source follower.

To calculate $L$, we can simply obtain an expression for $Z_{1}$ in terms of the three components in Fig. 6.29 and equate the result to $Z_{\text {out }}$ found above. Alternatively, since $R_{2}$ is a series component of $Z_{1}$, we can subtract its value from $Z_{\text {out }}$, thereby obtaining an expression for the parallel combination of $R_{1}$ and $L$ :

$$
\begin{equation*}
Z_{\text {out }}-\frac{1}{g_{m}}=\frac{C_{G S} S\left(R_{S}-\frac{1}{g_{m}}\right)}{g_{m}+C_{G S} s} \tag{6.65}
\end{equation*}
$$

Inverting the result to obtain the admittance of the parallel circuit, we have

$$
\begin{equation*}
\frac{1}{Z_{\text {out }}-\frac{1}{g_{m}}}=\frac{1}{R_{S}-\frac{1}{g_{m}}}+\frac{1}{\frac{C_{G S} S}{g_{m}}\left(R_{S}-\frac{1}{g_{m}}\right)} \tag{6.66}
\end{equation*}
$$

We can thus identify the first term on the right-hand side as the inverse of $R_{1}$ and the second term as the inverse of an impedance equal to $\left(C_{G S} s / g_{m}\right)\left(R_{S}-1 / g_{m}\right)$, i.e., an inductor with the value

$$
\begin{equation*}
L=\frac{C_{G S}}{g_{m}}\left(R_{S}-\frac{1}{g_{m}}\right) \tag{6.67}
\end{equation*}
$$

Note that $C_{G S} / g_{m}$ is approximately equal to $\omega_{T}=2 \pi f_{T}$.

#### Example 6.14

Can we construct a (two-terminal) inductor from a source follower?

#### Solution

Yes, we can. Called an "active inductor," such a structure is shown in Fig. 6.30(a), providing an inductance of $\left(C_{G S 2} / g_{m 2}\right)\left(R_{S}-1 / g_{m 2}\right)$. But the inductor is not ideal because it also incurs a parallel resistance equal to $R_{1}=$ $R_{S}=1 / g_{m 2}$ and a series resistance equal to $1 / g_{m 2}$. Figure 6.30(b) depicts an application of active inductors: the inductance can partially cancel the load capacitance, $C_{L}$, at high frequencies, thus extending the bandwidth. However, the voltage headroom consumed by $M_{2}\left(=V_{G S 2}\right)$ limits the gain. Also, $C_{G D 2}$, which has been neglected in our analysis, limits the bandwidth enhancement.
image_name:Figure 6.30(a)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: VDD, N2: g1}
name: CGS2, type: Capacitor, value: CGS2, ports: {Np: g1, Nn: S2}
name: M2, type: NMOS, ports: {S: s2, D: VDD, G: g1}
]
extrainfo:The circuit diagram (a) shows a configuration with an NMOS transistor M2, a resistor RS, and a capacitor CGS2. It is part of a common-gate stage that helps in bandwidth enhancement by partially canceling the load capacitance. The node g1 connects RS, CGS2, and the source of M2. M2's gate is connected to node S2, and its drain is connected to VDD.
image_name:Figure 6.30(b)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: VDD, N2: g1}
name: CGS2, type: Capacitor, value: CGS2, ports: {Np: g1, Nn: Vout}
name: M2, type: NMOS, ports: {S: Vout, D: VDD, G: g1}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
]
extrainfo:The circuit in diagram (b) is a common-gate stage with NMOS transistors M1 and M2. It includes a feedback loop from the output to the gate of M2. RS and CGS2 form part of the input network, while CL is connected to the output node to ground. The input is at Vin and output is taken from Vout.

## 6.4 ■ Common-Gate Stage

As explained in Example 6.5, in a common-gate stage, the input and output nodes are "isolated" if channellength modulation is neglected. For a common-gate stage such as that in Fig. 6.31, the calculation of Example 6.5 suggested a transfer function

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}(s)=\frac{\left(g_{m}+g_{m b}\right) R_{D}}{1+\left(g_{m}+g_{m b}\right) R_{S}} \frac{1}{\left(1+\frac{C_{S}}{g_{m}+g_{m b}+R_{S}^{-1}} s\right)\left(1+R_{D} C_{D} s\right)} \tag{6.68}
\end{equation*}
$$

image_name:Figure 6.31 Common-gate stage at high frequencies.
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: s1}
name: M1, type: NMOS, ports: {S: s1, D: Vout, G: Vb}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: CD, type: Capacitor, value: CD, ports: {Np: VDD, Nn: Vout}
name: CS, type: Capacitor, value: CS, ports: {Np: s1, Nn: GND}
]
extrainfo:The circuit is a common-gate amplifier stage. It uses an NMOS transistor with the gate connected to a bias voltage Vb. The input is applied to the source, and the output is taken from the drain. The circuit is designed for high-frequency applications and exhibits no Miller multiplication of capacitances, which allows for a potentially wide bandwidth. The low input impedance may load the preceding stage, and the DC level of the input signal must be low due to the voltage drop across RD.

An important property of this circuit is that it exhibits no Miller multiplication of capacitances, potentially achieving a wide band. Note, however, that the low input impedance may load the preceding stage. Furthermore, since the voltage drop across $R_{D}$ is typically maximized to obtain a reasonable gain, the dc level of the input signal must be quite low. For these reasons, the CG stage finds two principal applications: as an amplifier in cases where a low input impedance is required (Chapter 3) and in cascode stages.

If channel-length modulation is not negligible, the calculations become quite complex. Recall from Chapter 3 that the input impedance of a common-gate topology does depend on the drain load if $\lambda \neq 0$. From Eq. (3.117), we can express the impedance seen looking into the source of $M_{1}$ in Fig. 6.31 as

$$
\begin{equation*}
Z_{i n} \approx \frac{Z_{L}}{\left(g_{m}+g_{m b}\right) r_{O}}+\frac{1}{g_{m}+g_{m b}} \tag{6.69}
\end{equation*}
$$

where $Z_{L}=R_{D} \|\left[1 /\left(C_{D} s\right)\right]$. Since $Z_{i n}$ now depends on $Z_{L}$, it is difficult to associate a pole with the input node.

#### Example 6.15

For the common-gate stage shown in Fig. 6.32(a), calculate the transfer function and the input impedance, $Z_{i n}$. Explain why $Z_{i n}$ becomes independent of $C_{L}$ as this capacitance increases.
image_name:Figure 6.32(a)
description:
[
name: I1, type: CurrentSource, ports: {Np: VDD, Nn: Vout}
name: VDD, type: VoltageSource, ports: {Np: VDD, Nn: Vout}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
name: ro, type: Resistor, value: ro, ports: {N1: Vout, N2: s1}
name: M1, type: NMOS, ports: {S: s1, D: Vout, G: Vb}
name: Vb, type: VoltageSource, ports: {Np: Vb, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: s1}
name: Cin, type: Capacitor, value: Cin, ports: {Np: s1, Nn: GND}
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
]
extrainfo:The circuit is a common-gate amplifier with input impedance analysis. It includes a current source, a voltage source, an NMOS transistor, resistors, and capacitors. The input impedance becomes independent of CL as the capacitance increases.
image_name:Figure 6.32(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X2}
name: Cin, type: Capacitor, value: Cin, ports: {Np: X2, Nn: GND}
name: gmV1, type: VoltageControlledCurrentSource, value: gmV1, ports: {Np: Vout, Nn: X2}
name: ro, type: Resistor, value: ro, ports: {N1: X2, N2: Vout}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit in Fig. 6.32(b) is an equivalent representation of a common-gate amplifier stage, showing the input voltage source, series resistance, and capacitive loading at the output. The equivalent model includes a voltage-controlled current source representing transconductance.


#### Solution

Using the equivalent circuit shown in Fig. 6.32(b), we can write the current through $R_{S}$ as $-V_{\text {out }} C_{L} s+V_{1} C_{\text {in }} s$. Noting that the voltage across $R_{S}$ plus $V_{i n}$ must equal $-V_{1}$, we have

$$
\begin{equation*}
\left(-V_{\text {out }} C_{L} s+V_{1} C_{\text {in }} s\right) R_{S}+V_{\text {in }}=-V_{1} \tag{6.70}
\end{equation*}
$$

That is

$$
\begin{equation*}
V_{1}=-\frac{-V_{\text {out }} C_{L} s R_{S}+V_{\text {in }}}{1+C_{\text {in }} R_{S} s} \tag{6.71}
\end{equation*}
$$

We also observe that the voltage across $r_{O}$ minus $V_{1}$ equals $V_{\text {out }}$ :

$$
\begin{equation*}
r_{O}\left(-V_{\text {out }} C_{L} s-g_{m} V_{1}\right)-V_{1}=V_{\text {out }} \tag{6.72}
\end{equation*}
$$

Substituting for $V_{1}$ from (6.71), we obtain the transfer function:

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}(s)=\frac{1+g_{m} r_{O}}{r_{O} C_{L} C_{\text {in }} R_{S} s^{2}+\left[r_{O} C_{L}+C_{\text {in }} R_{S}+\left(1+g_{m} r_{O}\right) C_{L} R_{S}\right] s+1} \tag{6.73}
\end{equation*}
$$

The reader can prove that body effect can be included by simply replacing $g_{m}$ with $g_{m}+g_{m b}$. As expected, the gain at very low frequencies is equal to $1+g_{m} r_{O}$. For $Z_{i n}$, we can use (6.69) by replacing $Z_{L}$ with $1 /\left(C_{L} s\right)$, obtaining

$$
\begin{equation*}
Z_{i n}=\frac{1}{g_{m}+g_{m b}}+\frac{1}{C_{L} s} \cdot \frac{1}{\left(g_{m}+g_{m b}\right) r_{O}} \tag{6.74}
\end{equation*}
$$

We note that as $C_{L}$ or $s$ increases, $Z_{i n}$ approaches $1 /\left(g_{m}+g_{m b}\right)$, and hence the input pole can be defined as

$$
\begin{equation*}
\omega_{p, i n}=\frac{1}{\left(R_{S} \| \frac{1}{g_{m}+g_{m b}}\right) C_{i n}} \tag{6.75}
\end{equation*}
$$

Why does $Z_{i n}$ become independent of $C_{L}$ at high frequencies? This is because $C_{L}$ lowers the voltage gain of the circuit, thereby suppressing the effect of the negative resistance introduced by the Miller effect through $r_{O}$ (Fig. 6.7). In the limit, $C_{L}$ shorts the output node to ground, and $r_{O}$ affects the input impedance negligibly.

Our analysis of the CG frequency response has assumed a zero impedance in series with the gate. In practice, the bias network providing the gate voltage exhibits a finite impedance, altering the frequency response. Shown in Fig. 6.33(a) is an example in which this impedance is modeled by a resistor, $R_{G}$. If all of the device capacitances are included here, the circuit's transfer function is of third order. For simplicity, we consider only $C_{G S}$ here and only $C_{G D}$ in Appendix B. From the equivalent circuit in Fig. 6.33(b), ${ }^{4}$ we have $g_{m} V_{1}=-V_{\text {out }} / R_{D}$, and hence $V_{1}=-V_{\text {out }} /\left(g_{m} R_{D}\right)$. The current flowing through $R_{S}$ is equal to $V_{1} C_{G S} s+g_{m} V_{1}=-\left(C_{G S} s+g_{m}\right) V_{o u t} /\left(g_{m} R_{D}\right)$, and that through $R_{G}$ equal to $V_{1} C_{G S} s=$ $-C_{G S} s V_{\text {out }} /\left(g_{m} R_{D}\right)$. Writing a KVL around the input network, we have

$$
\begin{equation*}
V_{\text {in }}-\left(C_{G S}+g_{m}\right) \frac{V_{\text {out }}}{g_{m} R_{D}} R_{S}+\frac{V_{\text {out }}}{g_{m} R_{D}}-C_{G S} s \frac{V_{\text {out }}}{g_{m} R_{D}} R_{G}=0 \tag{6.76}
\end{equation*}
$$

It follows that

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=\frac{g_{m} R_{D}}{\left(R_{G}+R_{S}\right) C_{G S} s+1+g_{m} R_{S}} \tag{6.77}
\end{equation*}
$$

yielding a pole at

$$
\begin{equation*}
\omega_{p}=\frac{1+g_{m} R_{S}}{\left(R_{G}+R_{S}\right) C_{G S}} \tag{6.78}
\end{equation*}
$$

Thus, $R_{G}$ directly adds to $R_{S}$ in this case, lowering the pole magnitude.

image_name:(a)
description:The circuit is a common-gate amplifier stage with a series gate resistance RG and a source resistance RS. It includes an NMOS transistor M1, and the output is taken across RD. The equivalent circuit (b) shows the parasitic capacitance CGS and the transconductance gm modeled as a voltage-controlled current source. The input is driven by Vin, and the biasing is provided by Vb.
image_name:(b)
description:The circuit diagram (b) is an equivalent model of a common-gate stage with a series resistance at the gate. It includes a voltage source, resistors, a capacitor, an NMOS transistor, and a voltage-controlled current source. The circuit is used to analyze the frequency response and pole location in a common-gate configuration.

Figure 6.33 (a) CG stage with resistance in series with gate, and (b) equivalent circuit.

If a common-gate stage is driven by a relatively large source impedance, then the output impedance of the circuit drops at high frequencies. This effect is better described in the context of cascode circuits.

## 6.5 ■ Cascode Stage

As explained in Chapter 3, cascoding proves beneficial in increasing the voltage gain of amplifiers and the output impedance of current sources while providing shielding as well. The invention of the cascode (in the vacuum tube era), however, was motivated by the need for high-frequency amplifiers with a relatively high input impedance. Viewed as a cascade of a common-source stage and a common-gate stage, a cascode circuit offers the speed of the latter-by suppressing the Miller effect-and the input impedance of the former.

Let us consider the cascode shown in Fig. 6.34, first identifying all of the device capacitances. At node $A, C_{G S 1}$ is connected to ground and $C_{G D 1}$ to node $X$. At node $X, C_{D B 1}, C_{S B 2}$, and $C_{G S 2}$ are tied to ground, and at node $Y, C_{D B 2}, C_{G D 2}$, and $C_{L}$ are connected to ground. The Miller effect of $C_{G D 1}$ is determined by the gain from $A$ to $X$. As an approximation, we use the low-frequency value of this gain, which for low values of $R_{D}$ (or negligible channel-length modulation) is equal to $-g_{m 1} /\left(g_{m 2}+g_{m b 2}\right)$. Thus, if $M_{1}$ and $M_{2}$ have roughly equal dimensions, $C_{G D 1}$ is multiplied by approximately 2 rather than the large
image_name:Figure 6.34 High-frequency model of a cascode stage
description:This circuit is a high-frequency model of a cascode stage. It employs two NMOS transistors (M1 and M2) in a cascode configuration to reduce the Miller effect and improve bandwidth. The input is provided through Vin, and the output is taken from node Y (Vout). The circuit utilizes multiple capacitors to manage frequency response and stability, including CGD1, CGD2, CGS1, CDB1+CSB2, and CDB2+CL. The resistors RS and RD set the biasing and load conditions, respectively.

Figure 6.34 High-frequency model of a cascode stage.
voltage gain in a simple common-source stage. We therefore say that the Miller effect is less significant in cascode amplifiers than in common-source stages. The pole associated with node $A$ is estimated as

$$
\begin{equation*}
\omega_{p, A}=\frac{1}{R_{S}\left[C_{G S 1}+\left(1+\frac{g_{m 1}}{g_{m 2}+g_{m b 2}}\right) C_{G D 1}\right]} \tag{6.79}
\end{equation*}
$$

We can also attribute a pole to node $X$. The total capacitance at this node is roughly equal to $2 C_{G D 1}+$ $C_{D B 1}+C_{S B 2}+C_{G S 2}$, giving a pole

$$
\begin{equation*}
\omega_{p, X}=\frac{g_{m 2}+g_{m b 2}}{2 C_{G D 1}+C_{D B 1}+C_{S B 2}+C_{G S 2}} \tag{6.80}
\end{equation*}
$$

How does this pole compare with $2 \pi f_{T} \approx g_{m 2} / C_{G S 2}$ ? The other capacitances in the denominator reduce the magnitude of $\omega_{p, X}$ to roughly $2 \pi f_{T} / 2$. Finally, the output node yields a third pole:

$$
\begin{equation*}
\omega_{p, Y}=\frac{1}{R_{D}\left(C_{D B 2}+C_{L}+C_{G D 2}\right)} \tag{6.81}
\end{equation*}
$$

The relative magnitudes of the three poles in a cascode circuit depend on the actual design parameters, but $\omega_{p, X}$ is typically quite a lot higher than the other two.

But what if $R_{D}$ in Fig. 6.34 is replaced by a current source so as to achieve a higher dc gain? We know from Chapter 3 that the impedance seen at node $X$ reaches high values if the load impedance at the drain of $M_{2}$ is large. For example, Eq. (3.117) predicts that the pole at node $X$ may be quite a lot lower than $\left(g_{m 2}+g_{m b 2}\right) / C_{X}$ if $R_{D}$ itself is the output impedance of a PMOS cascode current source. Interestingly, however, the overall transfer function is negligibly affected by this phenomenon. This can be better seen by an example.

#### Example 6.16

Consider the cascode stage shown in Fig. 6.35(a), where the load resistor is replaced by an ideal current source. Neglecting the capacitances associated with $M_{1}$, representing $V_{i n}$ and $M_{1}$ by a Norton equivalent as in Fig. 6.35(b), and assuming $\gamma=0$, compute the transfer function.
image_name:Figure 6.35 Simplified model of a cascode stage.(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: g1}
name: M1, type: NMOS, ports: {S: GND, D: X, G: g1}
name: M2, type: NMOS, ports: {S: X, D: Y, G: Vb}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: Y}
name: rO2, type: Resistor, value: rO2, ports: {N1: Y, N2: X}
name: CX, type: Capacitor, value: CX, ports: {Np: X, Nn: GND}
name: CY, type: Capacitor, value: CY, ports: {Np: Y, Nn: GND}
]
extrainfo:The circuit diagram represents a cascode stage with an NMOS configuration. It includes a voltage source Vin, two NMOS transistors M1 and M2, a resistor RS, two capacitors CX and CY, and a current source I1. The circuit is designed to analyze the transfer function by neglecting the capacitances associated with M1 and representing it with a Norton equivalent. The nodes are annotated with labels like X, Y, Vout, and Vb to indicate various connection points in the circuit.
image_name:Figure 6.35 Simplified model of a cascode stage.(b)
description:
[
name: M2, type: NMOS, ports: {S: X, D: Y, G: Vb}
name: rO2, type: Resistor, value: rO2, ports: {N1: Y, N2: X}
name: CY, type: Capacitor, value: CY, ports: {Np: Y, Nn: GND}
name: CX, type: Capacitor, value: CX, ports: {Np: X, Nn: GND}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: X, Nn: GND}
]
extrainfo:This is a simplified model of a cascode stage with an NMOS transistor M2, resistive load rO2, and capacitive loads CX and CY. The input current source Iin is connected to node X.

#### Solution

Since the current through $C_{X}$ is equal to $-V_{\text {out }} C_{Y} s-I_{\text {in }}$, we have $V_{X}=-\left(V_{\text {out }} C_{Y} s+I_{i n}\right) /\left(C_{X} s\right)$, and the smallsignal drain current of $M_{2}$ is $-g_{m 2}\left(-V_{\text {out }} C_{Y} s-I_{\text {in }}\right) /\left(C_{X} s\right)$. The current through $r_{O 2}$ is then equal to $-V_{\text {out }} C_{Y} s-$ $g_{m 2}\left(V_{\text {out }} C_{Y} s+I_{\text {in }}\right) /\left(C_{X} s\right)$. Noting that $V_{X}$ plus the voltage drop across $r_{O 2}$ is equal to $V_{\text {out }}$, we write

$$
\begin{equation*}
-r_{O 2}\left[\left(V_{\text {out }} C_{Y} s+I_{\text {in }}\right) \frac{g_{m 2}}{C_{X} s}+V_{\text {out }} C_{Y} s\right]-\left(V_{\text {out }} C_{Y} s+I_{\text {in }}\right) \frac{1}{C_{X} s}=V_{\text {out }} \tag{6.82}
\end{equation*}
$$

That is

$$
\begin{equation*}
\frac{V_{\text {out }}}{I_{\text {in }}}=-\frac{g_{m 2} r_{O 2}+1}{C_{X} s} \cdot \frac{1}{1+\left(1+g_{m 2} r_{O 2}\right) \frac{C_{Y}}{C_{X}}+C_{Y} r_{O 2} s} \tag{6.83}
\end{equation*}
$$

which, for $g_{m 2} r_{O 2} \gg 1$ and $g_{m 2} r_{O 2} C_{Y} / C_{X} \gg 1$ (i.e., $C_{Y}>C_{X}$ ), reduces to

$$
\begin{equation*}
\frac{V_{\text {out }}}{I_{\text {in }}} \approx-\frac{g_{m 2}}{C_{X} s} \frac{1}{\frac{C_{Y}}{C_{X}} g_{m 2}+C_{Y} s} \tag{6.84}
\end{equation*}
$$

and hence

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=-\frac{g_{m 1} g_{m 2}}{C_{Y} C_{X} s} \frac{1}{g_{m 2} / C_{X}+s} \tag{6.85}
\end{equation*}
$$

The magnitude of the pole at node $X$ is still given by $g_{m 2} / C_{X}$. This is because at high frequencies (as we approach this pole), $C_{Y}$ shunts the output node, dropping the gain and suppressing the Miller effect of $r_{O 2}$.

If a cascode structure is used as a current source, then the variation of its output impedance with frequency is of interest. Neglecting $C_{G D 1}$ and $C_{Y}$ in Fig. 6.35(a), we have

$$
\begin{equation*}
Z_{\text {out }}=\left(1+g_{m 2} r_{O 2}\right) Z_{X}+r_{O 2} \tag{6.86}
\end{equation*}
$$

where $Z_{X}=r_{O 1} \|\left(C_{X} s\right)^{-1}$. Thus, $Z_{\text {out }}$ contains a pole at $\left(r_{O 1} C_{X}\right)^{-1}$ and falls at frequencies higher than this value.

## 6.6 ■ Differential Pair

The versatility of differential pairs and their extensive use in analog systems motivate us to characterize their frequency response for both differential and common-mode signals.

### 6.6.1 Differential Pair with Passive Loads

Consider the simple differential pair shown in Fig. 6.36(a), with the differential half circuit and the common-mode equivalent circuit depicted in Figs. 6.36(b) and (c), respectively. For differential signals, the response is identical to that of a common-source stage, exhibiting Miller multiplication of $C_{G D}$. Note that since $+V_{i n 2} / 2$ and $-V_{i n 2} / 2$ are multiplied by the same transfer function, the number of poles in $V_{\text {out }} / V_{\text {in }}$ is equal to that of each path (rather than the sum of the number of poles in the two paths).

For common-mode signals, the total capacitance at node $P$ in Fig. 6.36(c) determines the highfrequency gain. Arising from $C_{G D 3}, C_{D B 3}, C_{S B 1}$, and $C_{S B 2}$, this capacitance can be quite substantial if $M_{1}-M_{3}$ are wide transistors. For example, limited voltage headroom often necessitates that $W_{3}$ be so large
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: p, D: Voutp, G: Vin1}
name: M2, type: NMOS, ports: {S: p, D: Voutn, G: Vin2}
name: M3, type: NMOS, ports: {S: GND, D: p, G: Vb}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Voutp}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Voutn}
]
extrainfo:The circuit is a differential pair with a current mirror load. M1 and M2 form the differential pair, and M3 acts as a current source. RD resistors are used as loads for the differential pair. The circuit is powered by VDD with outputs Voutp and Voutn.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout1, G: Vin1}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout1}
name: CGD, type: Capacitor, value: CGD, ports: {Np: VDD, Nn: Vin1}
name: CGS, type: Capacitor, value: CGS, ports: {Np: Vin1, Nn: GND}
name: CDB, type: Capacitor, value: CDB, ports: {Np: Vout1, Nn: GND}
]
extrainfo:The circuit diagram (b) represents a half-circuit equivalent for analyzing differential pairs. It includes an NMOS transistor M1 connected to a resistor RD and capacitors CGD, CGS, and CDB. The input is applied at Vin1, and the output is taken from Vout1. The circuit is powered by VDD.
image_name:(c)
description:
[
name: M1, type: NMOS, ports: {S: p, D: Vout, G: Vin,CM}
name: M2, type: NMOS, ports: {S: p, D: Vout, G: Vin,CM}
name: M3, type: NMOS, ports: {S: GND, D: p, G: Vb}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: CGD, type: Capacitor, value: CGD, ports: {Np: Vin1, Nn: Vout1}
name: CGS, type: Capacitor, value: CGS, ports: {Np: Vin1, Nn: GND}
name: CDB, type: Capacitor, value: CDB, ports: {Np: Vout1, Nn: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: VDD, Nn: Vout}
name: rO3, type: Resistor, value: rO3, ports: {N1: p, N2: GND}
name: CP, type: Capacitor, value: CP, ports: {Np: p, Nn: GND}
]
extrainfo:The circuit is a common-mode equivalent circuit for a differential pair. It includes NMOS transistors M1 and M2 with a shared source node p connected to the ground through a resistor rO3 and a capacitor CP. The output is taken across RD and CL, connected to VDD and Vout. The circuit is designed to analyze the common-mode response of the differential pair.

Figure 6.36 (a) Differential pair; (b) half-circuit equivalent; (c) equivalent circuit for common-mode inputs.
that $M_{3}$ does not require a large drain-source voltage for operating in the saturation region. If only the mismatch between $M_{1}$ and $M_{2}$ is considered, the high-frequency common-mode gain can be calculated with the aid of Eq. (4.53). We replace $r_{O 3}$ with $r_{O 3} \|\left[1 /\left(C_{P} s\right)\right]$ and $R_{D}$ by $R_{D} \|\left[1 /\left(C_{L} s\right)\right]$, where $C_{L}$ denotes the total capacitance seen at each output node. ${ }^{5}$ Thus,

$$
\begin{equation*}
A_{v, C M}=-\frac{\Delta g_{m}\left[R_{D} \|\left(\frac{1}{C_{L} s}\right)\right]}{\left(g_{m 1}+g_{m 2}\right)\left[r_{O 3} \|\left(\frac{1}{C_{P} S}\right)\right]+1} \tag{6.87}
\end{equation*}
$$

This result suggests that the common-mode rejection of the circuit degrades considerably at high frequencies. In fact, writing the CMRR from Chapter 4 for this case gives

$$
\begin{align*}
\mathrm{CMRR} & \approx \frac{g_{m}}{\Delta g_{m}}\left[1+2 g_{m}\left(r_{O 3} \| \frac{1}{C_{P} s}\right)\right]  \tag{6.88}\\
& \approx \frac{g_{m}}{\Delta g_{m}} \frac{r_{O 3} C_{P} s+1+2 g_{m} r_{O 3}}{r_{O 3} C_{P} s+1} \tag{6.89}
\end{align*}
$$

where $g_{m}=\left(g_{m 1}+g_{m 2}\right) / 2$. We observe that this transfer function contains a zero at $\left(1+2 g_{m 3} r_{O 3}\right) /$ $\left(r_{O 3} C_{P}\right)$ and a pole at $1 /\left(r_{O 3} C_{P}\right)$. Since $2 g_{m 3} r_{O 3} \gg 1$, the magnitude of the zero is much greater than the pole and approximately equal to $2 g_{m 3} / C_{P}$. The CMRR response thus appears as shown in Fig. 6.37.
image_name:Figure 6.37
description:The graph in Figure 6.37 is a Bode plot illustrating the Common-Mode Rejection Ratio (CMRR) as a function of frequency for a differential pair. The axes are both on a logarithmic scale. The vertical axis represents the CMRR measured in decibels (dB), while the horizontal axis represents angular frequency (ω) in logarithmic scale.

Overall Behavior and Trends:
- **Initial Plateau:** The CMRR starts at a high value, indicated as \( \frac{2g_m^2 r_{O3}}{\Delta g_m} \), and remains constant over a range of low frequencies.
- **First Break Point:** At the frequency \( \frac{1}{r_{O3}C_P} \), the CMRR begins to decrease, indicating the onset of a roll-off.
- **Slope:** The plot shows a downward slope, suggesting a decrease in CMRR with increasing frequency.
- **Second Break Point:** The slope changes again at the frequency \( \frac{2g_{m3}}{C_P} \), where the CMRR stabilizes to a lower value.

Key Features and Technical Details:
- **High Initial CMRR:** The graph begins with a high CMRR value, emphasizing strong common-mode rejection at low frequencies.
- **Roll-off:** The downward slope between the two break points represents the frequency range where the common-mode rejection diminishes.
- **Stabilization:** After the second break point, the CMRR stabilizes, indicating a region where further increases in frequency do not significantly affect the CMRR.

Annotations and Specific Data Points:
- The plot is annotated with the expressions for the break frequencies, \( \frac{1}{r_{O3}C_P} \) and \( \frac{2g_{m3}}{C_P} \), which are critical points determining the behavior of the CMRR across frequencies.
- The initial CMRR level is marked as \( \frac{2g_m^2 r_{O3}}{\Delta g_m} \), which is a significant parameter for understanding the performance of the differential pair in rejecting common-mode signals.

Figure 6.37 CMRR for a differential pair vs. frequency.

As illustrated in Fig. 6.38, if the supply voltage contains high-frequency noise and the circuit exhibits mismatches, the resulting common-mode disturbance at node $P$ translates to a differential noise component at the output. This effect becomes more pronounced as the noise frequency exceeds $1 /\left(2 \pi r_{O 3} C_{P}\right)$.
image_name:Figure 6.38
description:The circuit is a differential pair with NMOS transistors M1 and M2 forming the main differential pair, and M3 and M4 serving as input transistors. The resistors and capacitors are used for biasing and frequency response shaping. The circuit is designed to study the effect of high-frequency supply noise on differential pairs, and includes nodes for Voutp and Voutn to analyze the output.

Figure 6.38 Effect of high-frequency supply noise in differential pairs.
We should emphasize that the circuit of Fig. 6.36(a) suffers from a trade-off between voltage headroom and CMRR. To minimize the headroom consumed by $M_{3}$, its width is maximized, introducing substantial capacitance at the sources of $M_{1}$ and $M_{2}$ and degrading the high-frequency CMRR. The issue becomes more serious at low supply voltages.

We now study the frequency response of differential pairs with high-impedance loads. Shown in Fig. 6.39(a) is a fully differential implementation. As with the topology of Fig. 6.36, this circuit can be analyzed for differential and common-mode signals separately. Note that here $C_{L}$ includes the drain junction capacitance and the gate-drain overlap capacitance of each PMOS transistor as well. Also,
image_name:(a)
description:This is a fully differential pair with current-source loads. The circuit is designed to study the frequency response with high-impedance loads. Node G acts as an ac ground due to the capacitors CGD3 and CGD4 conducting equal and opposite currents. The circuit uses NMOS transistors M1, M2, M3, M4, and M5, and includes capacitors CL, CGD1, CGD3, and CGD4, along with current sources I1 and Iss.
image_name:(b)
description:The circuit is a differential pair with current-source loads, focusing on the effect of differential swings at node G. Capacitors CGD3 and CGD4 conduct equal and opposite currents to node G, effectively making it an AC ground. The circuit is designed to analyze differential signals.
image_name:(c)
description:The circuit in diagram (c) is a differential half circuit. It includes an NMOS transistor M1, a capacitor CGD1, a resistor ro1||ro3, and a load capacitor CL. The node Vout1 is connected to the drain of M1, and the gate is connected to Vin1. The circuit is grounded at the source of M1 and at the resistor and capacitor ends.

Figure 6.39 (a) Differential pair with current-source loads; (b) effect of differential swings at node $G$; (c) half-circuit equivalent.
as depicted in Fig. 6.39(b) for differential output signals, $C_{G D 3}$ and $C_{G D 4}$ conduct equal and opposite currents to node $G$, making this node an ac ground. (In practice, node $G$ is still bypassed to ground by means of a capacitor.)

The differential half circuit is depicted in Fig. 6.39(c), with the output resistance of $M_{1}$ and $M_{3}$ shown explicitly. This topology implies that Eq. (6.30) can be applied to this circuit if $R_{L}$ is replaced by $r_{O 1} \| r_{O 3}$. In practice, the relatively high value of this resistance makes the output pole, given by $\left[\left(r_{O 1} \| r_{O 3}\right) C_{L}\right]^{-1}$, the "dominant" pole. We return to this observation in Chapter 10. The common-mode behavior of the circuit is similar to that of Fig. 6.36(c).

### 6.6.2 Differential Pair with Active Load

Let us now consider a differential pair with an active current mirror (Fig. 6.40). How many poles does this circuit have? In contrast to the fully differential configuration of Fig. 6.39(a), this topology contains two signal paths with different transfer functions. The path consisting of $M_{3}$ and $M_{4}$ includes a pole at node $E$, approximately given by $g_{m 3} / C_{E}$, where $C_{E}$ denotes the total capacitance from $E$ to ground. This capacitance arises from $C_{G S 3}, C_{G S 4}, C_{D B 3}, C_{D B 1}$, and the Miller effect of $C_{G D 1}$ and $C_{G D 4}$. Even if only $C_{G S 3}$ and $C_{G S 4}$ are considered, the severe trade-off between $g_{m}$ and $C_{G S}$ of PMOS devices results in a pole that impacts the performance of the circuit. The pole associated with node $E$ is called a "mirror pole." Note that, as with the circuit of Fig. 6.39(a), both signal paths shown in Fig. 6.40 contain a pole at the output node.

In order to estimate the frequency response of the differential pair with an active current mirror, we construct the simplified model depicted in Fig. 6.41(a), where all other capacitances are neglected.
image_name:Figure 6.40
description:
[
name: M1, type: NMOS, ports: {S: GND, D: P, G: Vin}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: M3, type: PMOS, ports: {S: VDD, D: E, G: E}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: E}
name: Iss, type: CurrentSource, ports: {Np: P, Nn: GND}
name: CE, type: Capacitor, value: CE, ports: {Np: E, Nn: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
name: RX, type: Resistor, value: RX, ports: {N1: E, N2: VX}
name: rOP, type: Resistor, value: rOP, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a high-frequency model of a differential pair with an active current mirror. It contains a mirror pole at node E and an output pole at Vout. The PMOS devices M3 and M4 form the current mirror, while NMOS devices M1 and M2 form the differential pair. A current source Iss is connected to the sources of M1 and M2, providing biasing. Capacitors CE and CL introduce capacitive loading at nodes E and Vout, respectively.
image_name:Figure 6.41(a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: E, G: Vin}
name: M2, type: NMOS, ports: {S: P, D: Vout, G: Vin}
name: M3, type: PMOS, ports: {S: VDD, D: E, G: E}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: E}
name: Iss, type: CurrentSource, ports: {Np: P, Nn: GND}
name: CE, type: Capacitor, value: CE, ports: {Np: E, Nn: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
name: RX, type: Resistor, value: RX, ports: {N1: E, N2: VX}
name: rOP, type: Resistor, value: rOP, ports: {N1: Vout, N2: Vout}
]
extrainfo:The circuit is a high-frequency model of a differential pair with an active current mirror. It features a mirror pole at node E and an output pole at the output node. The circuit utilizes an NMOS differential pair (M1 and M2) and a PMOS current mirror (M3 and M4). The current source Iss provides the biasing current. Capacitors CE and CL model the capacitances at nodes E and Vout, respectively.
image_name:Figure 6.41(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: P, G: Vin}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: M3, type: PMOS, ports: {S: VDD, D: E, G: E}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: E}
name: Iss, type: CurrentSource, ports: {Np: P, Nn: GND}
name: CE, type: Capacitor, value: CE, ports: {Np: E, Nn: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
name: RX, type: Resistor, value: RX, ports: {N1: E, N2: VX}
name: rOP, type: Resistor, value: rOP, ports: {N1: Vout, N2: Vout}
]
extrainfo:The circuit is a differential pair with an active current mirror. It includes a mirror pole at node E and an output pole at the output node. The circuit is simplified using a Thevenin equivalent for frequency response estimation.

Figure 6.41 (a) Simplified high-frequency model of differential pair with active current mirror; (b) circuit of (a) with a Thevenin equivalent.

Replacing $V_{i n}, M_{1}$, and $M_{2}$ by a Thevenin equivalent, we arrive at the circuit of Fig. 6.41(b), where $V_{X}=g_{m N} r_{O N} V_{i n}$ and $R_{X}=2 r_{O N}$ (why?). Here, the subscripts $P$ and $N$ refer to PMOS and NMOS devices, respectively, and we have assumed that $1 / g_{m P} \ll r_{O P}$. The small-signal voltage at $E$ is equal to

$$
\begin{equation*}
V_{E}=\left(V_{\text {out }}-V_{X}\right) \frac{\frac{1}{C_{E} S+g_{m P}}}{\frac{1}{C_{E} S+g_{m P}}+R_{X}} \tag{6.90}
\end{equation*}
$$

and the small-signal drain current of $M_{4}$ is $g_{m 4} V_{E}$. Noting that $-g_{m 4} V_{E}-I_{X}=V_{\text {out }}\left(C_{L} s+r_{O P}^{-1}\right)$, we have

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=\frac{g_{m N} r_{O N}\left(2 g_{m P}+C_{E} s\right) r_{O P}}{2 r_{O P} r_{O N} C_{E} C_{L} s^{2}+\left[\left(2 r_{O N}+r_{O P}\right) C_{E}+r_{O P}\left(1+2 g_{m P} r_{O N}\right) C_{L}\right] s+2 g_{m P}\left(r_{O N}+r_{O P}\right)} \tag{6.91}
\end{equation*}
$$

Since the mirror pole is typically much higher in magnitude than the output pole, we can utilize the results of Eq. (6.34) to write

$$
\begin{equation*}
\omega_{p 1} \approx \frac{2 g_{m P}\left(r_{O N}+r_{O P}\right)}{\left(2 r_{O N}+r_{O P}\right) C_{E}+r_{O P}\left(1+2 g_{m P} r_{O N}\right) C_{L}} \tag{6.92}
\end{equation*}
$$

Neglecting the first term in the denominator and assuming that $2 g_{m P} r_{O N} \gg 1$, we have

$$
\begin{equation*}
\omega_{p 1} \approx \frac{1}{\left(r_{O N} \| r_{O P}\right) C_{L}} \tag{6.93}
\end{equation*}
$$

an expected result. The second pole is then given by

$$
\begin{equation*}
\omega_{p 2} \approx \frac{g_{m P}}{C_{E}} \tag{6.94}
\end{equation*}
$$

which is also expected.
An interesting point revealed by Eq. (6.91) is a zero with a magnitude of $2 g_{m P} / C_{E}$ in the left half plane. The appearance of such a zero can be understood by noting that the circuit consists of a "slow path" $\left(M_{1}, M_{3}\right.$, and $\left.M_{4}\right)$ in parallel with a "fast path" ( $M_{1}$ and $M_{2}$ ). Representing the two by $A_{0} /[(1+$ $\left.\left.s / \omega_{p 1}\right)\left(1+s / \omega_{p 2}\right)\right]$ and $A_{0} /\left(1+s / \omega_{p 1}\right)$, respectively, we have

$$
\begin{align*}
\frac{V_{\text {out }}}{V_{\text {in }}} & =\frac{A_{0}}{1+s / \omega_{p 1}}\left(\frac{1}{1+s / \omega_{p 2}}+1\right)  \tag{6.95}\\
& =\frac{A_{0}\left(2+s / \omega_{p 2}\right)}{\left(1+s / \omega_{p 1}\right)\left(1+s / \omega_{p 2}\right)} \tag{6.96}
\end{align*}
$$

That is, the system exhibits a zero at $2 \omega_{p 2}$. The zero can also be obtained by the method of Fig. 6.18 (Problem 6.15).

Comparing the circuits of Figs. 6.39(a) and 6.40, we conclude that the former entails no mirror pole, another advantage of fully differential circuits over single-ended topologies.

## 6.7 ■ Gain-Bandwidth Trade-Offs

In many applications, we wish to maximize both the gain and the bandwidth of amplifiers. For example, optical communication receivers employ an amplifier that must achieve a high gain and a wide bandwidth. This section deals with gain-bandwidth trade-offs encountered in high-speed design. As shown in Fig. 6.43, we are interested in both the $-3-\mathrm{dB}$ bandwidth, $\omega_{-3 d B}$, and the "unity-gain" bandwidth, $\omega_{u}$.
image_name:Figure 6.43 Frequency response showing $-3-\mathrm{dB}$ and unity-gain bandwidths.
description:The graph in Figure 6.43 is a Bode plot representing the frequency response of an amplifier. The horizontal axis is labeled with angular frequency \( \omega \) and is plotted on a logarithmic scale, while the vertical axis represents the gain in decibels (dB), specifically \( 20 \log \left| \frac{V_{\text{out}}}{V_{\text{in}}}(j\omega) \right| \).

Axes Labels and Units:
- **Horizontal Axis (\( \omega \))**: Frequency, plotted on a logarithmic scale.
- **Vertical Axis**: Gain in decibels (dB).

Overall Behavior and Trends:
The graph shows a typical low-pass filter response. It starts with a flat region where the gain is constant, indicating that the amplifier maintains a steady gain over a range of low frequencies. As the frequency increases, the graph exhibits a downward slope, indicating a decrease in gain.

Key Features and Technical Details:
- **\( \omega_{-3\text{dB}} \)**: The cutoff frequency where the gain drops by 3 dB from its maximum value. This point is marked on the graph with a vertical dashed line.
- **\( \omega_{u} \)**: The unity-gain bandwidth, where the gain reaches 0 dB. This point is also marked on the graph.
- The slope after the \( \omega_{-3\text{dB}} \) point indicates the roll-off of the amplifier's gain as frequency increases.

Annotations and Specific Data Points:
- The graph is annotated with two critical frequencies: \( \omega_{-3\text{dB}} \) and \( \omega_{u} \), which are essential for understanding the bandwidth characteristics of the amplifier. The \( \omega_{-3\text{dB}} \) point signifies the boundary of the -3 dB bandwidth, while \( \omega_{u} \) indicates the frequency at which the amplifier's gain becomes unity (0 dB).

### 6.7.1 One-Pole Circuits

In some circuits, the load capacitance seen at the output node produces a dominant pole, allowing a one-pole approximation. That is, we can say that the $-3-\mathrm{dB}$ bandwidth is equal to the pole frequency. For example, the CS stage of Fig. 6.44 exhibits an output pole given by $\omega_{p}=\left[\left(r_{O 1} \| r_{O 2}\right) C_{L}\right]^{-1}$ if other capacitances are neglected. Noting that the low-frequency gain is equal to $\left|A_{0}\right|=g_{m 1}\left(r_{O 1}| | r_{O 2}\right)$, we define the "gain-bandwidth" product (GBW) as

$$
\begin{align*}
\mathrm{GBW} & =A_{0} \omega_{p}  \tag{6.98}\\
& =g_{m 1}\left(r_{O 1} \| r_{O 2}\right) \frac{1}{2 \pi\left(r_{O 1} \| r_{O 2}\right) C_{L}}  \tag{6.99}\\
& =\frac{g_{m 1}}{2 \pi C_{L}}
\end{align*}
$$

image_name:Figure 6.44 CS stage with one pole
description:
[
name: M2, type: PMOS, ports: {S: VDD, D: Vout, G: Vb}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a common-source (CS) amplifier stage with a single pole. It consists of a PMOS transistor (M2) as the load and an NMOS transistor (M1) as the amplifying device. The output is taken across a load capacitor CL connected to ground. The input is applied to the gate of M1, and the bias voltage Vb controls the gate of M2. The supply voltage is VDD, and the circuit provides an amplified output at Vout.

Figure 6.44 CS stage with one pole.
As an example, if $g_{m 1}=(100 \Omega)^{-1}$ and $C_{L}=50 \mathrm{fF}$, then GBW $=31.8 \mathrm{GHz}$. For a one-pole system, the gain-bandwidth product is approximately equal to the unity-gain bandwidth; this can be seen by writing

$$
\begin{equation*}
\frac{A_{0}}{\sqrt{1+\left(\frac{\omega_{u}}{\omega_{p}}\right)^{2}}}=1 \tag{6.101}
\end{equation*}
$$

and hence

$$
\begin{align*}
\omega_{u} & =\sqrt{A_{0}^{2}-1} \omega_{p}  \tag{6.102}\\
& \approx A_{0} \omega_{p} \tag{6.103}
\end{align*}
$$

if $A_{0}^{2} \gg 1$.

#### Example 6.18

Does cascoding increase the GBW product? Assume that the output pole is dominant.

#### Solution

No, it does not. Equation (6.100) suggests that the GBW product is independent of the output resistance. More specifically, if cascoding in Fig. 6.44 raises the output impedance by a factor of $K$, then $\left|A_{0}\right|\left(=G_{m} R_{\text {out }}\right)$ rises and $\omega_{p}$ fafls, both by a factor of $K$, yielding a constant GBW product.

### 6.7.2 Multi-Pole Circuits

It is possible to increase the GBW product by cascading two or more gain stages. Consider the amplifier shown in Fig. 6.45, where, for simplicity, we assume that the two stages are identical and neglect other capacitances. Associating one pole with each node, we write the transfer function as $\left(V_{\text {out }} / V_{X}\right)\left(V_{X} / V_{\text {in }}\right)$ :

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=\frac{A_{0}^{2}}{\left(1+\frac{s}{\omega_{p}}\right)^{2}} \tag{6.104}
\end{equation*}
$$

image_name:Figure 6.45 Cascaded CS stages
description:
[
name: M1, type:NMOS, ports: {S: GND, D: Vx, G: Vin}
name: M2, type: PMOS, ports: {S: VDD, D: Vx, G: Vb}
name: M3, type: NMOS, ports: {S: GND, D: Vout, G: Vx}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: Vb}
name: CL, type: Capacitor, value: CL, ports: {Np: Vx, Nn: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit consists of two cascaded common-source (CS) amplifier stages. Each stage is formed by an NMOS and a PMOS transistor pair (M1-M2 and M3-M4) with capacitive loads (CL) at the intermediate and output nodes. The bias voltage Vb is used to set the gate voltage of the PMOS transistors. The circuit is designed to enhance the gain-bandwidth product by cascading two identical stages.

Figure 6.45 Cascaded CS stages.
where $A_{0}=g_{m N}\left(r_{O N} \| r_{O P}\right)$ and $\omega_{\underline{p}}=\left[\left(r_{O N} \| r_{O P}\right) C_{L}\right]^{-1}$. To obtain the $-3-\mathrm{dB}$ bandwidth, we equate the magnitude of $V_{\text {out }} / V_{\text {in }}$ to $A_{0}^{2} / \sqrt{2}$ :

$$
\begin{equation*}
\frac{A_{0}^{2}}{1+\frac{\omega_{-3 d B}^{2}}{\omega_{p}^{2}}}=\frac{A_{0}^{2}}{\sqrt{2}} \tag{6.105}
\end{equation*}
$$

and

$$
\begin{align*}
\omega_{-3 d B} & =\sqrt{\sqrt{2}-1} \omega_{p}  \tag{6.106}\\
& \approx 0.64 \omega_{p} \tag{6.107}
\end{align*}
$$

The GBW product thus rises to

$$
\begin{equation*}
\mathrm{GBW}=\sqrt{\sqrt{2}-1} A_{0}^{2} \omega_{p} \tag{6.108}
\end{equation*}
$$

a factor of $0.64 A_{0}$ greater than that in Eq. (6.103). Of course, the power consumption is doubled.
While raising the GBW product, cascading reduces the bandwidth, as evidenced by Eq. (6.107). In fact, we prove in Problem 6.25 that for $N$ identical stages,

$$
\begin{equation*}
\omega_{-3 d B}=\sqrt{\sqrt[N]{2}-1} \omega_{p} \tag{6.109}
\end{equation*}
$$

observing a steady decline in the bandwidth as $N$ increases. Another disadvantage of cascading is that the resulting multiple poles lead to instability if the circuit is placed in a negative-feedback loop (Chapter 10).

## 6.8 - Appendix A: Extra Element Theorem

Introduced by Middlebrook [1], the extra element theorem (EET) proves useful in calculating some transfer functions. Suppose the transfer function of a circuit is known and denoted by $H(s)$. Now, as shown in Fig. 6.46(a), we add an extra impedance $Z_{1}$ between two nodes of the circuit. We wish to determine the new transfer function, $G(s)$. Middlebrook proves that

$$
\begin{equation*}
G(s)=H(s) \frac{1+\frac{Z_{\text {out }, 0}}{Z_{1}}}{1+\frac{Z_{\text {in }, 0}}{Z_{1}}} \tag{6.110}
\end{equation*}
$$

i.e., the original transfer function is multiplied by a "correction factor." The terms $Z_{\text {out }, 0}$ and $Z_{\text {in }, 0}$ are quantities measured between nodes $A$ and $B$ in the absence of $Z_{1}$. The former is computed as depicted in Fig. 6.46(b): we apply a voltage source between $A$ and $B$ while $V_{i n}$ is present and choose their values so that $V_{\text {out }}=0$; then $Z_{\text {out }, 0}=V_{1} / I_{1}$. This calculation appears rather complex and unintuitive, but, as shown below, it is in fact quite simple. We should also remark that $Z_{\text {out }, 0}$ is not an impedance in the standard sense because it is obtained with a finite $V_{i n}$. The latter, $Z_{i n, 0}$, is simply equal to the impedance seen between $A$ and $B$ when $V_{i n}=0[$ Fig. 6.46(c)].
image_name:(a)
description:The circuit diagram (a) consists of a voltage source Vin connected to a resistor Z1 between nodes A and B. The output is labeled as Vout. The diagram is used for analyzing the impedance Zout,0 and Zin,0 in the context of frequency-response analysis.
image_name:(b)
description:The circuit is set up to calculate Z_out,0 by setting V_out to 0. It involves a voltage source V1 and a current source I1 connected between nodes A and B.
image_name:(c)
description:The diagram shows a setup for calculating the input impedance Z_in,0 with a voltage source Vin and additional sources V1 and I1 across nodes A and B. Vout is set to 0.

Figure 6.46 (a) Circuit with extra parallel element, $Z_{1}$, (b) $Z_{\text {out }, 0}$ calculation, and (c) $Z_{\text {in }, 0}$ calculation.

This theorem is particularly useful for frequency-response analysis because we can begin with no capacitances in the circuit, find $H(s)$ as the low-frequency gain, add the capacitors one by one, and calculate the correction factors. Note that $H(s)$ cannot be zero or infinity because the EET's proof relies on division by $H(s)$.

#### Example 6.19

Using the EET, find the transfer function of the circuit in Fig. 6.47(a).

#### Solution

We first consider the circuit without $C_{F}$ and write $H(s)=-g_{m}\left(R_{D} \| r_{O}\right)$. Next, we find $Z_{\text {out }, 0}$ using the setup shown in Fig. 6.47(b), exploiting the condition that $V_{\text {out }}$ is zero and so is the current through $R_{D}$. Since $V_{\text {out }}=0$, we have $V_{G S}=V_{1}$ and $I_{1}=-g_{m} V_{G S}=-g_{m} V_{1}$. That is, $Z_{\text {out }, 0}=-1 / g_{m}$. Note that we resisted the temptation to
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: A}
name: CF, type: Capacitor, value: CF, ports: {Np: A, Nn: B}
name: RD, type: Resistor, value: RD, ports: {N1: B, N2: VDD}
name: M1, type: NMOS, ports: {S: GND, D: B, G: A}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a common-source amplifier with feedback capacitor CF. The input is applied to the gate of the NMOS transistor M1, and the output is taken across RD. The feedback capacitor CF is connected between the input and output nodes to stabilize the circuit's frequency response.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: A}
name: M1, type: NMOS, ports: {S: GND, D: B, G: A}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: B}
name: V1, type: VoltageSource, value: V1, ports: {Np: A, Nn: B}
]
extrainfo:The circuit represents a small-signal model for analyzing output impedance. The voltage source V1 and current source I1 are used for test purposes to determine the output impedance Z_out.
image_name:(c)
description:The circuit in diagram (c) is a common-source NMOS amplifier with feedback capacitor CF. The input is applied through RS, and the output is taken across RD. The NMOS transistor M1 is configured with its source connected to ground, gate to node A, and drain to node B. The circuit includes a feedback path via the capacitor CF from node A to node B.

Figure 6.47
write equations involving $V_{i n}$. Also, the negative sign of $Z_{\text {out }, 0}$ does not imply a negative impedance between $A$ and $B$ because $V_{\text {in }} \neq 0$.

For $Z_{i n, 0}$, we have from Fig. 6.47(c), $V_{A}=I_{1} R_{S}=V_{G S}$. A KCL at node $B$ gives the current through $R_{D}$ as $g_{m} I_{1} R_{S}+I_{1}$, and a KVL across $R_{D}, V_{1}$, and $R_{S}$ leads to $I_{1} R_{D}\left(1+g_{m} R_{S}\right)-V_{1}+I_{1} R_{S}=0$. It follows that $Z_{i n, 0}=\left(1+g_{m} R_{S}\right) R_{D}+R_{S}=\left(1+g_{m} R_{D}\right) R_{S}+R_{D}$ and

$$
\begin{equation*}
G(s)=-g_{m}\left(R_{D} \| r_{O}\right) \frac{1-\frac{1}{g_{m}} C_{F} s}{1+\left[\left(1+g_{m} R_{D}\right) R_{S}+R_{D}\right] C_{F} s} \tag{6.111}
\end{equation*}
$$

We see that the EET beautifully predicts the zero and the pole produced by $C_{F}$.

#### Example 6.20

Repeat the above example while including both $C_{F}$ and a capacitor, $C_{B}$, from node $B$ to ground.

#### Solution

Since we have already obtained the transfer function with $C_{F}$ present, we must seek the $Z_{\text {out }, 0}$ and $Z_{i n, 0}$ corresponding to $C_{B}$. The arrangement depicted in Fig. 6.48(a) suggests that $Z_{\text {out }, 0}=0$ because the drain voltage must be zero while $V_{1}$ is not, requiring an infinite current to flow through $V_{1}$.
image_name:Figure 6.48(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: A}
name: M1, type: NMOS, ports: {S: GND, D: B, G: A}
name: CF, type: Capacitor, value: CF, ports: {Np: A, Nn: B}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: B}
name: V1, type: VoltageSource, value: V1, ports: {Np: B, Nn: GND}
]
extrainfo:The circuit diagram (a) shows an NMOS amplifier configuration with a feedback capacitor CF connected from the drain to VDD. The input is applied at node A through resistor RS, and the output is taken from node B. The circuit includes a current source I1 and a voltage source V1 connected to node B.
image_name:Figure 6.48(b)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: A}
name: CF, type: Capacitor, value: CF, ports: {Np: A, Nn: B}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: B}
name: V1, type: VoltageSource, value: V1, ports: {Np: B, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: B, G: A}
]
extrainfo:The circuit is a common-source NMOS amplifier with feedback capacitor CF and a load resistor RD. The input is applied at Vin, and the output is taken across V1.

For $Z_{i n, 0}$, we note from Fig. 6.48(b) that $V_{G S}=V_{1} R_{S} C_{F} s /\left(R_{S} C_{F} s+1\right)$ and the current flowing through $C_{F}$ is equal to $V_{1} /\left[\left(C_{F} s\right)^{-1}+R_{S}\right]$. A KCL at the drain node gives

$$
\begin{equation*}
\frac{V_{1}}{R_{D}}+\frac{V_{1} C_{F} s}{R_{S} C_{F} s+1}+g_{m} V_{1} \frac{R_{S} C_{F} s}{R_{S} C_{F} s+1}=I_{1} \tag{6.112}
\end{equation*}
$$

Thus,

$$
\begin{equation*}
Z_{i n, 0}=\frac{R_{D}\left(R_{S} C_{F} s+1\right)}{\left[R_{S}\left(1+g_{m} R_{D}\right)+R_{D}\right] C_{F} s+1} \tag{6.113}
\end{equation*}
$$

Using Eq. (6.111), we write the new transfer function as

$$
\begin{align*}
G(s) & =-g_{m}\left(R_{D} \| r_{O}\right) \frac{1-\frac{C_{F}}{g_{m}} s}{1+\left[\left(1+g_{m} R_{D}\right) R_{S}+R_{D}\right] C_{F} s} \frac{1}{1+\frac{R_{D}\left(R_{S} C_{F} s+1\right) C_{B} s}{\left[R_{S}\left(1+g_{m} R_{D}\right)+R_{D}\right] C_{F} s+1}} \\
& =-g_{m}\left(R_{D} \| r_{O}\right) \frac{1-\frac{C_{F}}{g_{m}} s}{\left[R_{S}\left(1+g_{m} R_{D}\right)+R_{D}\right] C_{F} s+R_{D}\left(R_{S} C_{F} s+1\right) C_{B} s+1} \tag{6.114}
\end{align*}
$$

The EET can also be expressed for series elements [1]. That is, if the transfer function of a circuit is $H(s)$ before we insert an element, $Z_{1}$, in series with a branch, then the new transfer function is given by [1]

$$
\begin{equation*}
G(s)=H(s) \frac{1+\frac{Z_{1}}{Z_{\text {out }, 0}}}{1+\frac{Z_{1}}{Z_{\text {in }, 0}}} \tag{6.115}
\end{equation*}
$$
