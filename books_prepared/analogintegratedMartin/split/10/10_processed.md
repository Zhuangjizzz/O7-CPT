# 10 Comparator

Perhaps the second most widely used electronic components (after amplifiers) are comparators. A comparator is used to detect whether a signal is greater or smaller than zero, or to compare the size of one signal to another. As we will see in Chapter 17, comparators are used in large abundance in A/D converters. They also find widespread use in many other applications, such as data transmission, switching power regulators, and others. In this chapter, we look at comparator design and practical limitations, where a number of different approaches are discussed. First, we examine a simplistic approach of using an open-loop opamp for a comparator. Although this approach is too slow for practical applications, it is a good example to use when we discuss several design principles for minimizing input-offset voltage and charge-injection errors. A number of other approaches are also described, such as multiple-stage comparators, positive-feedback track-and-latch comparators, and fully differential comparators. Finally, examples of both CMOS and bipolar comparator circuits are also described.

## 10.1 COMPARATOR SPECIFICATIONS

### 10.1.1 Input Offset and Noise

The input offset of a comparator is the input voltage at which its output changes from one logic level to the other (neglecting noise). In an ideal comparator, this value would be zero. In a practical comparator, input offset might be caused by device mismatches (Chapter 2) or might be inherent in the design of the comparator.

Random circuit noise can cause the output of a comparator to change from one logic state to the other, even when the comparator input is held constant. Hence, in order to measure the input-offset voltage in the presence of circuit

Key Point: The input offset of a comparator is the input at which the output is equally likely to be high or low. Noise determines how the output statistics vary as a function of input.
noise, one would look for the input voltage that results in the output state of the comparator being high and low with equal likelihood. The input-referred noise is then observed by changing the input around this value and observing how the output statistics vary as a function of the input voltage around this dc offset.

#### EXAMPLE 10.1

The output of a comparator is observed while slowly sweeping the input over the range -10 mV to +10 mV . The fraction of time that the comparator output is high is plotted as a function of the input voltage in
image_name:Fig. 10.1
description:The graph in Fig. 10.1 is a probability curve, specifically a sigmoid or S-curve, depicting the likelihood of a high output logic level from a comparator as a function of varying input voltage.

**Axes Labels and Units:**
- The horizontal axis represents the input voltage in millivolts (mV), ranging from -10 mV to +10 mV.
- The vertical axis represents the probability of the comparator output being high, ranging from 0 to 1.

**Overall Behavior and Trends:**
- The curve starts at a low probability near 0 when the input voltage is around -10 mV. As the input voltage increases, the probability of a high output rises sharply, forming an S-shaped curve.
- The curve transitions from low to high probability around the 0 to 5 mV range, indicating the region where the comparator is most sensitive to input changes.

**Key Features and Technical Details:**
- At an input voltage of 3 mV, the probability of a high output is 50%, which indicates the input offset of the comparator.
- At an input voltage of 4.28 mV, the probability reaches 90%, suggesting a high confidence level in the output being high.

**Annotations and Specific Data Points:**
- The graph includes dashed lines marking the 50% probability at 3 mV and the 90% probability at 4.28 mV, which are critical points for assessing the comparator’s performance.

The graph effectively illustrates how the comparator's output transitions from low to high probability as the input voltage crosses the offset level, providing insights into the device's noise characteristics and sensitivity.

Fig. 10.1 Probability of a high output logic level with varying input level for a particular comparator.

Fig. 10.1. Estimate the comparator's input offset and noise. For this comparator, what is the smallest input that can be resolved with an error rate of $10^{-12}$ ?

#### Solution

The plot in Fig. 10.1 is recognized as a normal distribution. At an input of 3 mV , the comparator output is equally likely to be high or low; hence, the comparator's input offset is 3 mV . The $90 \%$ confidence interval for a normal distribution is at 1.2816 times its standard deviation (rms) value. In Fig. 10.1, this occurs at an input of 4.28 mV , implying an rms input noise of

$$
\frac{4.28-3}{1.2816} \mathrm{mV}=1 \mathrm{mV}_{\mathrm{rms}}
$$

For an error rate of $10^{-12}$, the input must exceed the input offset by 7.0344 times the rms noise level. Hence, for a high output logic level the required input voltage is $3+7.0344 \cdot 1 \mathrm{mV}=10.0 \mathrm{mV}$. For a low output logic level, the input must be below -4 mV .

### 10.1.2 Hysteresis

Key Point: Hysteresis is "memory" in a comparator that tends to make it remain in its past output state, usually due to charge retained on internal circuit capacitances.

Many comparator designs have an input threshold that is dependent upon the past state of the comparator. Specifically, most comparators have a tendency to remain in their past state. For example, when a comparator's output is at a high logic level, it might remain so for input voltages as low as -20 mV , but when that same comparator's output is at a low logic level an input voltage of +20 mV might be required to cause the input to change to a high logic level. The comparator's "memory" results from charge stored on the its internal capacitances, and is referred to as hysteresis. Generally, hysteresis is a nonideality in comparators that should be minimized, usually by ensuring all internal capacitances are completely discharged periodically. However, in some applications hysteresis may be used
to advantage. For example, if the comparator is to be operated with near-zero input for long periods of time, some hysteresis will prevent the comparator's output from toggling back and forth between high and low logic levels due to noise.

## 10.2 USING AN OPAMP FOR A COMPARATOR

A simplistic approach for realizing a comparator is to use an open-loop opamp, as shown in Fig. 10.2. The main drawback to this approach is the slow response time since the opamp output has to slew a large amount of output voltage and settles too slowly. However, temporarily ignoring this slow response time, we will first investigate its input offset voltage.

The simplistic opamp approach shown in Fig. 10.2 has a resolution limited to the input-offset voltage of the opamp. This offset might be on the order of 2 mV to 5 mV for typical MOS processes, which is inadequate for many applications. An alternative architecture that can resolve signals with accuracies much less than the inputoffset voltages of opamps is shown in Fig. 10.3 [McCreary, 1975; Yee, 1978]. Although this circuit has been used many times in early analog-to-digital converters, as we will see, it is not preferable nowadays. However, it is a simple example that can be used to illustrate many important design principles. The circuit of Fig. 10.3 operates as follows: During $\phi_{1}$, known as the reset phase, the bottom plate ${ }^{1}$ of the capacitor C (i.e., the left side of capacitor C ) is connected to ground, and the top plate is connected to the inverting input of the opamp. At the same time, the output of the opamp is also connected to the inverting input of the opamp by closing switch $\mathrm{S}_{\mathrm{r}}$. Assuming the opamp is ideal, this connection causes the capacitor to be charged to zero volts. Next, during the comparison phase, the reset switch, $\mathrm{S}_{\mathrm{r}}$, is turned off, and the bottom plate of the capacitor is connected to the input voltage. The opamp is now in an open-loop configuration. If the input signal is greater than zero, the output of the opamp swings to a large negative voltage. If the input signal is less than zero, the output of the opamp swings to a large positive voltage. These two cases are easily resolved and the decision can be stored using a simple digital latch.
image_name:Fig. 10.2
description:
[
name: OpAmp1, type: OpAmp, ports: {InP: Vin, InN: GND, OutP: Vout}
]
extrainfo:The circuit is an open-loop op-amp comparator. When Vin > 0, the output Vout swings to a large negative voltage; when Vin < 0, Vout swings to a large positive voltage. The op-amp is used in a comparator configuration without feedback.

Fig. 10.2 A simplistic approach of using an open-loop opamp for a comparator.
image_name:Fig. 10.3
description:The circuit is a comparator with offset voltage cancellation using a capacitor and switch. The op-amp is configured with a feedback switch Sr, which closes during the phase φ1a to stabilize the comparator and reduce charge injection effects. The capacitor C is used to store charge and cancel offset voltages, with the bottom plate connected to the less sensitive input side.

Fig. 10.3 Cancelling the offset voltage of a comparator-the comparator here must be stable, with unity-gain feedback during $\phi_{1 \mathrm{a}}$. ( $\phi_{1 \mathrm{a}}$ is a slightly advanced version of $\phi_{1}$ so that chargeinjection effects are reduced.)

1. The bottom plate of a capacitor has significant parasitic capacitance between it and ground. Therefore, it is almost always connected to the less sensitive input side rather than to the critical amplifier side (see Chapter 14).

The limitations of this approach become apparent when one considers nonideal opamps, which have finite gains and require compensation to be stable during the reset phase.

### EXAMPLE 10.2

Consider the case in which a $0.2-\mathrm{mV}$ signal must be resolved using the circuit shown in Fig. 10.3, where the opamp's output should be 2 V . Assuming the opamp's unity-gain frequency is 10 MHz , find the maximum clocking rate of the comparator circuit if reset and comparison phases are equal and if six time constants are allowed for settling.

### Solution

After the comparison phase, the output of the opamp should have a 2-V difference between the cases in which the input signal is either -0.1 mV or $+0.1 \mathrm{mV} .^{2}$ As a result, the opamp gain must be at least $10,000 \mathrm{~V} / \mathrm{V}$. By assuming that the dominant-pole compensation is used to guarantee stability during the reset phase, we obtain an open-loop transfer function for the opamp similar to that shown in Fig. 10.4. Here, the $-3-\mathrm{dB}$ frequency of the opamp is given by

$$
\begin{equation*}
\mathrm{f}_{-3 \mathrm{~dB}}=\frac{\mathrm{f}_{\mathrm{t}}}{\mathrm{~A}_{0}}=1 \mathrm{kHz} \tag{10.1}
\end{equation*}
$$

During the comparison phase, the output of the opamp will have a transient response similar to that of a first-order system that has a time constant given by

$$
\begin{equation*}
\tau=\frac{1}{2 \pi \mathrm{f}_{-3 \mathrm{~dB}}} \cong 0.16 \mathrm{~ms} \tag{10.2}
\end{equation*}
$$

If six time constants are allowed for settling during the comparison phase, then approximately 1 ms is needed for the comparison phase. Assuming the reset time is the same as the comparison time, the clock frequency can be no greater than 500 Hz -a frequency that is much too slow for most applications.
image_name:Fig. 10.4
description:The graph in Fig. 10.4 is a Bode plot representing the open-loop transfer function of an operational amplifier (opamp) used in a comparator. The graph is plotted with frequency on the x-axis and the magnitude of the gain, |A(w)|, in decibels (dB) on the y-axis.

1. **Type of Graph and Function:**
- This is a Bode plot, specifically showing the magnitude response of the opamp's open-loop transfer function.

2. **Axes Labels and Units:**
- The x-axis represents frequency, marked in a logarithmic scale from 1 kHz to 10 MHz.
- The y-axis represents the gain magnitude, |A(w)|, in decibels (dB).

3. **Overall Behavior and Trends:**
- The graph starts at a high gain level of 80 dB at low frequencies.
- There is a sharp transition starting at the cutoff frequency (f₀) of 1 kHz, where the magnitude of the gain begins to decrease linearly with an increase in frequency.
- The slope of the decrease is typical of a single-pole system, indicating a reduction of 20 dB/decade.
- The gain continues to decrease until it reaches 0 dB at 10 MHz, suggesting the bandwidth limit of the opamp.

4. **Key Features and Technical Details:**
- The initial gain is A₀ = 80 dB at frequencies below 1 kHz.
- The cutoff frequency, f₀, is marked at 1 kHz, which is a pivotal point where the gain begins to drop.
- The linear decrease in gain indicates a first-order low-pass filter characteristic.
- The bandwidth of the opamp is indicated to extend up to 10 MHz.

5. **Annotations and Specific Data Points:**
- The graph is annotated with key values such as the initial gain (A₀ = 80 dB) and the cutoff frequency (f₀ = 1 kHz).
- The final frequency marker at 10 MHz indicates the extent of the frequency response shown in the plot.

Fig. 10.4 The open-loop transfer function of the opamp used to realize the comparator.
image_name:Fig. 10.5
description:The circuit is an opamp with a compensation capacitor Cc that can be disconnected by switch Q1 during the comparison phase. The inputs are labeled as Vin+ and Vin-, and the output is labeled as Vout. The circuit contains current sources and MOS transistors, indicating differential amplification and current mirroring.

Fig. 10.5 An opamp that has its compensation capacitor disconnected during the comparison phase.

One possibility for speeding up the comparison time is to disconnect the compensation capacitor during the comparison phase. For example, a simplified opamp schematic is shown in Fig. 10.5. In this opamp, transistor $Q_{1}$ is used to achieve lead compensation when it is on during the reset phase, $\phi_{1}$. During the comparison phase, $Q_{1}$ is turned off, which disconnects the compensation capacitor, $\mathrm{C}_{\mathrm{C}}$, thereby greatly speeding up the opamp during this phase. Using this technique, it is possible to use clock frequencies ten to fifty times greater

Key Point: Regular opamps are compensated to ensure stability in closed-loop configurations, resulting in a low 3-dB bandwidth and, hence, very slow settling if used open-loop as a comparator.
than would otherwise be the case-perhaps as high as 25 or 50 kHz in our example. If this is adequate, then the approach is reasonable. Unfortunately, this often isn't adequate, and other approaches, to be described shortly, are necessary.

One superior aspect of the approach just described is that the input capacitor, C in Fig. 10.3, is never charged or discharged during operation. Specifically, in phase $\phi_{1}, \mathrm{C}$ is always charged to 0 V . In phase $\phi_{2}$, the top plate, connected to the inverting input of the opamp, is open-circuited at that time (assuming the parasitic capacitors are ignored), and the voltage across capacitor C remains at 0 V (in other words, the top-plate voltage follows $\mathrm{V}_{\text {in }}$ ). This approach greatly minimizes the charge required from the input when $\mathrm{V}_{\mathrm{in}}$ changes. If the switches attached to the bottom plate had their phases interchanged, then the comparison operation would be noninverting, but now capacitor C must be charged or discharged during the reset phase since the bottom plate follows $\mathrm{V}_{\mathrm{in}}$, whereas the top plate remains at virtual ground. Normally, we like to use a reasonably large input capacitor to minimize clockfeedthrough effects (described in Section 10.3). This charging/discharging requirement puts severe constraints on the input signal source, and, thus, the clock phasing shown in Fig. 10.3 should be used. Besides, it is usually possible to tolerate an inverting comparison since it can be made noninverting through the use of a digital inversion somewhere else in the system.

### 10.2.1 Input-Offset Voltage Errors

In switched-capacitor comparators, such as that shown in Fig. 10.3, input offset is not a problem since it is stored across the capacitor during the reset phase, and then the error is cancelled during the comparison phase. To appreciate this cancellation, assume the opamp has an input-offset voltage error that is modelled as a voltage source in series with one of the opamp's inputs. The circuit configuration during the reset phase is shown in

Key Point: An input capacitor is sometimes used to sample the input offset voltage of a comparator during a reset phase, and then subtract it from the input during the comparison phase.
image_name:(a)
description:The circuit diagram (a) shows a configuration during the reset phase (ϕ1) where the input capacitor is charged to the offset voltage Voff. The switch Sr is closed, connecting the op-amp's output to its inverting input, creating a feedback loop. The voltage source Voff models the op-amp's input-offset voltage.
image_name:(b)
description:The circuit is configured to cancel the input-offset voltage error of the opamp by sampling it during the reset phase and subtracting it during the comparison phase. This is achieved by charging the capacitor to the offset voltage during the reset phase and using it to adjust the input during the comparison phase.

Fig. 10.6 The circuit configuration (a) during the reset phase, and (b) during the comparison phase, assuming the opamp has an input-offset voltage given by $\mathrm{V}_{\text {off }}$.

Fig. 10.6(a). Assuming the opamp gain is very large, then the inverting input of the opamp is at the voltage $\mathrm{V}_{\text {off }}$, which implies that the input capacitor is charged to $\mathrm{V}_{\text {off }}$ during this phase. Next, during $\phi_{2}$, as shown in Fig. $10.6(b)$, the left side of capacitor C is connected to the input voltage. The right side of the capacitor has a voltage given by $\mathrm{V}_{\text {in }}+\mathrm{V}_{\text {off }}$, which results in the comparator output becoming negative if $\mathrm{V}_{\text {in }}$ is greater than zero or positive if $\mathrm{V}_{\text {in }}$ is less than zero, regardless of the value of $\mathrm{V}_{\text {off }}$. Furthermore, notice that very low-frequency inputreferred noise is indistinguishable from input-offset, and hence is cancelled along with $\mathrm{V}_{\text {off }}$. Therefore, not only does this technique eliminate input-offset voltage errors, but it also minimizes errors caused by low-frequency $1 / \mathrm{f}$ noise, which can be large in CMOS microcircuits.

## 10.3 CHARGE-INJECTION ERRORS

Perhaps the major limitation on the resolution of comparators is due to what is referred to as charge-injection, also commonly called clock feedthrough. This error is due to unwanted charges being injected into the circuit when the transistors turn off. For the comparator in Fig. 10.3, the switches are normally realized by either n-channel transistors alone or CMOS transmission gates (which consist of n -channel transistors in parallel with p -channel transistors, both of which must turn off). When MOS switches are on, they operate in the triode region and have zero volts between their drain and their source. When MOS switches turn off, charge errors occur by two mechanisms. The first is due to the channel charge, which must flow out from the channel region of the transistor
image_name:Fig. 10.7
description:The circuit is a comparator with n-channel MOS switches and parasitic capacitances. It utilizes three NMOS transistors and several capacitors to manage charge distribution and signal comparison. The op-amp is used to amplify the difference between the input and reference signals.

Fig. 10.7 The comparator in Fig. 10.3, with n-channel switches and overlap parasitic capacitances shown. Transistors turned on also have channel charge.
to the drain and the source junctions. ${ }^{3}$ The channel charge of a transistor that has zero $\mathrm{V}_{\mathrm{DS}}$ is given by

$$
\begin{equation*}
Q_{c h}=W L C_{o x} V_{\text {eff }}=W L C_{o x}\left(V_{G s}-V_{t}\right) \tag{10.3}
\end{equation*}
$$

This charge often dominates. The second charge (typically smaller, unless $\mathrm{V}_{\text {eff }}$ is very small) is due to the overlap capacitance between the gate and the junctions.

Figure 10.7 shows the comparator of Fig. 10.3, where the switches have been realized as n-channel transistors. Also shown in Fig. 10.7 are the parasitic capacitances due to gate-drain and gate-source overlap capacitors. Finally, although it is not shown in Fig. 10.7, one should remember to include the channel charge dispersion of any transistors that change from being on to off. ${ }^{4}$ In the circuit shown, all transistors are n -channel, implying that the channel charge is negative.

Consider first when $Q_{3}$ turns off. If the clock waveform is very fast, the channel charge due to $Q_{3}$ will flow equally out through both junctions [Shieh, 1987]. The $\mathrm{Q}_{\mathrm{ch}} / 2$ charge that goes to the output node of the opamp will have very little effect other than causing a temporary glitch. However, the $Q_{c h} / 2$ charge that goes to the inverting-input node of the opamp will cause the voltage across $C$ to change, which introduces an error. Since this charge is negative, for an $n$-channel transistor, the node voltage $\mathrm{V}^{\prime \prime}$ will become negative. The voltage change due to the channel charge is given by

$$
\begin{equation*}
\Delta V^{\prime \prime}=\frac{\left(Q_{\mathrm{ch}} / 2\right)}{C}=-\frac{V_{\text {eff } 3} C_{o x} W_{3} L_{3}}{2 C}=-\frac{\left(V_{D D}-V_{t n}\right) C_{o x} W_{3} L_{3}}{2 C} \tag{10.4}
\end{equation*}
$$

since the effective gate-source voltage of $Q_{3}$ is given by $V_{\text {eff } 3}=V_{G S_{3}}-V_{t n}=V_{D D}-V_{t n}$. The preceding voltage change in $\mathrm{V}^{\prime \prime}$ is based on the assumption that $Q_{2}$ turns off slightly after $Q_{3}$ turns off. More will be said about this assumption shortly.

[^0]Fig. 10.8 A capacitor divider.
image_name:Fig. 10.8 A capacitor divider
description:The circuit is a capacitor divider with two capacitors, C1 and C2, connected in series. Vout is taken across C2, and it equals VC2.

Key Point: As a MOSFET goes from triode mode to off, the charge stored in the channel region must flow out of the transistor terminals; in a comparator, the charge may accumulate on circuit capacitances causing offset.

To calculate the change in voltage due to the overlap capacitance, it is first necessary to introduce the capacitor-divider formula. This formula is used to calculate the voltage change at the internal node of two series capacitors, when the voltage at one of the end terminals changes. This situation is shown in Fig. 10.8, where it is assumed that $\mathrm{V}_{\text {in }}$ is changing and we want to calculate the change in $\mathrm{V}_{\text {out }}=\mathrm{V}_{\mathrm{C} 2}$. The series combination of $\mathrm{C}_{1}$ and $\mathrm{C}_{2}$ is equal to a single capacitor, $\mathrm{C}_{\mathrm{eq}}$, given by

$$
\begin{equation*}
\mathrm{C}_{\mathrm{eq}}=\frac{\mathrm{C}_{1} \mathrm{C}_{2}}{\mathrm{C}_{1}+\mathrm{C}_{2}} \tag{10.5}
\end{equation*}
$$

When $\mathrm{V}_{\text {in }}$ changes, the charge flow into this equivalent capacitor is given by

$$
\begin{equation*}
\Delta \mathrm{Q}_{\mathrm{eq}}=\Delta \mathrm{V}_{\mathrm{in}} \mathrm{C}_{\mathrm{eq}}=\Delta \mathrm{V}_{\mathrm{in}} \frac{\mathrm{C}_{1} \mathrm{C}_{2}}{\mathrm{C}_{1}+\mathrm{C}_{2}} \tag{10.6}
\end{equation*}
$$

All of the charge that flows into $\mathrm{C}_{\mathrm{eq}}$ is equal to the charge flow into $\mathrm{C}_{1}$, which is also equal to the charge flow into $\mathrm{C}_{2}$. Thus, we have

$$
\begin{equation*}
\Delta \mathrm{V}_{\text {out }}=\Delta \mathrm{V}_{\mathrm{C} 2}=\frac{\Delta \mathrm{Q}_{\mathrm{C} 2}}{\mathrm{C}_{2}}=\frac{\Delta \mathrm{V}_{\text {in }} \mathrm{C}_{1}}{\mathrm{C}_{1}+\mathrm{C}_{2}} \tag{10.7}
\end{equation*}
$$

This formula is often useful when calculating charge flow in integrated circuits. It can be applied to the circuit of Fig. 10.7 to calculate the change in $\mathrm{V}^{\prime \prime}$ due to the overlap capacitance of $\mathrm{Q}_{3}$ when it turns off. For this case, we have $\mathrm{C}_{1}=\mathrm{C}_{\mathrm{ov}}, \mathrm{C}_{2}=\mathrm{C}$, and $\Delta \mathrm{V}_{\mathrm{in}}=-\left(\mathrm{V}_{\mathrm{DD}}-\mathrm{V}_{\mathrm{SS}}\right)$. This assumes the clock signals change from $\mathrm{V}_{\mathrm{DD}}$ to $\mathrm{V}_{\mathrm{Ss}}$. The change in $\mathrm{V}^{\prime \prime}$ due to the overlap capacitance is now found to be given by

$$
\begin{equation*}
\Delta \mathrm{V}^{\prime \prime}=\frac{-\left(\mathrm{V}_{\mathrm{DD}}-\mathrm{V}_{\mathrm{SS}}\right) \mathrm{C}_{\mathrm{ov}}}{\mathrm{C}_{\mathrm{ov}}+\mathrm{C}} \tag{10.8}
\end{equation*}
$$

This change is normally less than that due to the change caused by the channel charge since $\mathrm{C}_{\text {ov }}$ is small.

#### EXAMPLE 10.3

Assume that a resolution of $\pm 2.5 \mathrm{mV}$ is required from the circuit of Fig. 10.7. The following values are given: $\mathrm{C}=0.1 \mathrm{pF}, \mathrm{C}_{\mathrm{ox}}=8.5 \mathrm{fF} /(\mu \mathrm{m})^{2},(\mathrm{~W} / \mathrm{L})_{3}=4 \mu \mathrm{~m} / 0.2 \mu \mathrm{~m}, \mathrm{~L}_{\mathrm{ov}}=0.04 \mu \mathrm{~m}, \mathrm{~V}_{\mathrm{tn}}=0.45 \mathrm{~V}$, and $\mathrm{V}_{\mathrm{DD}}=1 \mathrm{~V}$. What is the change in $\Delta \mathrm{V}^{\prime \prime}$ when $\mathrm{Q}_{3}$ turns off?

#### Solution

Using (10.4), we have $\Delta \mathrm{V}^{\prime \prime}=-53 \mathrm{mV}$. The overlap capacitance is given by $\mathrm{C}_{\mathrm{ov}}=\mathrm{W}_{3} \mathrm{~L}_{\mathrm{ov}} \mathrm{C}_{\mathrm{ox}}=1.4 \mathrm{fF}$. Using (10.8), this gives a voltage change in $\Delta \mathrm{V}^{\prime \prime}$ of $\Delta \mathrm{V}^{\prime \prime}=-2.8 \mathrm{mV}$, which is smaller than the change due to the channel charge, but not insignificant. The total change is found by adding the two effects so that $\Delta \mathrm{V}^{\prime \prime}=-56 \mathrm{mV}$.

This result is on the order of 10 times greater than the value of $\pm 2.5 \mathrm{mV}$ that should be resolved. Clearly, additional measures should be taken to minimize the effects of charge-injection if this resolution is required.
image_name:Fig. 10.9
description:The circuit is a clock generator that produces two clock signals, φ1 and φ2, from a single input voltage source Vin. It uses AND gates and inverters to create the clock waveforms.

Fig. 10.9 A clock generator suitable for generating the desired clock waveforms for the comparator in Fig. 10.3.

### 10.3.1 Making Charge-Injection Signal Independent

The charge-injection due to transistors $Q_{1}$ and $Q_{2}$ may cause temporary glitches, but it will have much less effect than the charge-injection chargeinjection due to $Q_{3}$ if we assume that $Q_{2}$ turns off slightly after $Q_{3}$ does [Haigh, 1983]. This time difference is the reason why the clock voltage of $Q_{2}$ is denoted $\phi_{1}$, whereas the clock voltage of $Q_{3}$ is denoted $\phi_{1 a}\left(\phi_{1}\right.$ advanced). The argument for this arrangement is as follows: When $Q_{2}$ turns off, its charge-injection causes a negative glitch at $\mathrm{V}^{\prime}$, but this will

Key Point: The deleterious effects of charge-injection can be reduced by using "advanced" clocks which open-circuit the discharge paths through which signal-dependent charge-injection flows.
not cause any change in the charge stored in $C$ since the right side of $C$ is connected to an effective open circuit, assuming that $Q_{3}$ has already turned off. Later, when $Q_{1}$ turns on, the voltage $\mathrm{V}^{\prime}$ will settle to $V_{\text {in }}$ regardless of the previous charge-injection of $Q_{2}$. Thus, the voltage at the left of $C$ is unaffected by the chargeinjection of $Q_{2}$, and the voltage across $C$ is also unaffected by the charge-injection of $Q_{2}$. Therefore, the voltage $\mathrm{V}^{\prime \prime}$ is unaffected by the charge-injection of $\mathrm{Q}_{2}$. This is not the case if $\mathrm{Q}_{2}$ is turned off at the same time or before $Q_{3}$ is turned off. The charge-injection of $Q_{1}$ has no effect for a simpler reason-the comparison has already been made when it turns off. In addition, its charge-injection has no effect when it turns on because the right side of C is connected to an open circuit at that time, assuming the clocks do not overlap. In summary, by turning off $\phi_{1 \mathrm{a}}$ first, the cir cuit is affec ted only by the char ge-injection of $\mathrm{Q}_{3}$ and not by any of the othe $r$ switches.

Figure 10.9 shows a simple digital circuit [Martin, 1980] that is capable of generating the desired clock waveforms. The waveforms $\phi_{1}$ and $\phi_{1 a}$ do not overlap with $\phi_{2}$ and $\phi_{2 a}$. Also, $\phi_{1 \mathrm{a}}$ will be advanced slightly (by two inverter delays), compared to $\phi_{1}$.

### 10.3.2 Minimizing Errors Due to Charge-Injection

The simplest way to reduce errors due to charge-injection is to use larger capacitors. For our previous example, capacitors on the order of about 10 pF guarantee that the clock-feedthrough errors are approximately 0.5 mV . Unfortunately, this large amount of capacitance would require a large amount of silicon area. Also, integrated capacitors have parasitic capacitances between their terminals and the substrate that might be about 20 percent of the size of the realized capacitor. Thus, a parasitic capacitance of about 2 pF would have to be driven by the input circuits, which would greatly slow down the circuits.
image_name:Fig. 10.10
description:The circuit is a fully differential, single-stage, switched-capacitor comparator. It uses a fully differential design to minimize errors due to charge injection. The reset switches can be connected to a common-mode voltage reference instead of ground.

Fig. 10.10 A fully differential, single-stage, switched-capacitor comparator.
An alternative approach for minimizing errors due to charge-injection is to use fully differential design techniques for comparators, similar to what is often done for opamps. A simple example of a one-stage, switchedcapacitor, fully differential comparator is shown in Fig. 10.10. Note that the ground connections to the reset switches $\varphi_{1}$ in Fig. 10.10 may be replaced by a common-mode voltage reference located midway between the ana$\log$ supplies. Ideally, when the comparator is taken out of reset mode, the clock feedthrough of reset switch $Q_{3 a}$ matches the clock feedthrough of $Q_{3 b}$. In this case, the common-mode voltage may be slightly affected, but the differential input voltage is unaffected. The only errors now are due to mismatches in the clock feedthrough of the two switches, which will typically be at least ten times smaller than in the single-ended case. For this reason, virtually all modern integrated comparators utilize fully differential design techniques.

A third alternative that can be used along with fully differential design techniques is to realize a multi-stage comparator [Poujois, 1978; Vittoz, 1985], where the clock feedthrough of the first stage is stored on coupling capacitors between the first and second stage, thereby eliminating its effect. The clock feedthrough of the second stage can be stored on the coupling capacitors between the second and the third stages, and so on. Although this technique is almost always used along with fully differential configurations, we will explain the technique using single-ended configurations, for simplicity. Consider the three-stage comparator shown in Fig. 10.11(a), along with the appropriate clock waveforms shown in Fig. 10.11(b). Consider the time when $\phi_{1}^{\prime}$ drops and the switch of the first stage has charge-injection. Figure 10.12 illustrates this case, along with the parasitic capacitances of the first-stage switch. When $\phi_{1}^{\prime}$ drops, $Q_{1}$ injects charge into both the inverting input and the output of the first stage through parasitic capacitors $C_{p 1}$ and $C_{p 2}$, respectively. The charge injected at the first stage output causes only a temporary glitch there. The charge injected at the inverting input causes this node to become negative. The amount by which this node voltage becomes negative is calculated using the analysis method described previously. Let us assume this amount will be in the range of tens of millivolts, as calculated in Example 10.3. After the inverting input becomes negative, the output of the first stage becomes positive by an amount equal to the negative transition of the inverting input multiplied by the first stage's gain. However, at this time, $\phi_{1}^{\prime \prime}$ is still high. Therefore, the second stage is still being reset and $\mathrm{C}_{2}$ is charged up to the output error caused by the clock feedthrough of the first stage, thereby eliminating its effect. In a similar manner, when $\phi_{1}^{\prime \prime}$ turns off and the second stage goes from closed-loop reset mode to open-loop comparison mode, the third stage is still in reset mode and the clock feedthrough of the second stage is stored on coupling capacitor $\mathrm{C}_{3}$. Finally, when the third stage turns off, its charge-injection is not cancelled. However, the error it causes in resolving an input voltage to all three stages is small, equal to the voltage transition at the inverting input of the third stage divided by the negative of the gains of the first two stages (i.e., this is the input voltage needed to cancel the effect of the clock feedthrough of the third stage coming out of reset mode).
image_name:(a)
description:This is a multi-stage comparator circuit designed to eliminate clock feedthrough errors. It consists of three stages, each with an operational amplifier and coupling capacitors. The circuit uses multiple clock phases to control the switches, allowing for the cancellation of input offset voltages and minimizing errors during transitions.
image_name:(b)
description:The graph labeled "(b)" is a set of time-domain waveforms representing clock signals used in a multi-stage comparator circuit. The graph displays four distinct waveforms, each corresponding to a different clock phase: \( \phi_1 \), \( \phi_1' \), \( \phi_1'' \), and \( \phi_2 \).

1. **Type of Graph and Function:**
- **Graph Type:** Time-domain waveform.
- **Function:** Represents clock signal phases used to control the switching in a multi-stage comparator circuit.

2. **Axes Labels and Units:**
- **Horizontal Axis:** Represents time. No specific units are marked, but it is implied to be in consistent time intervals.
- **Vertical Axis:** Represents the logical state of the clock signals (high or low). No specific voltage levels are indicated, but it is typically in digital logic levels (e.g., 0V for low, Vcc for high).

3. **Overall Behavior and Trends:**
- Each waveform exhibits a rectangular shape, typical of digital clock signals, alternating between high and low states.
- The waveforms are staggered relative to each other, indicating different timing for each clock phase.
- \( \phi_1 \) and \( \phi_2 \) appear to have a similar period but are not synchronized, with \( \phi_2 \) starting low while \( \phi_1 \) starts high.
- \( \phi_1' \) and \( \phi_1'' \) are also staggered versions of \( \phi_1 \), indicating sequential clock phases.

4. **Key Features and Technical Details:**
- The staggered nature of the waveforms suggests a sequential switching operation in the circuit.
- The timing differences between the phases are critical for the proper operation of the comparator, ensuring that each stage is triggered at the correct time.

5. **Annotations and Specific Data Points:**
- No specific numerical values or annotations are provided on the graph, but the timing relationships are visually clear.
- The sequence and duration of the high and low states are essential for the clocking mechanism of the multi-stage comparator circuit, which aims to minimize clock feedthrough errors.

Fig. 10.11 (a) A multi-stage comparator used to eliminate clock feedthrough errors, with (b) the appropriate clock waveforms.

In a variation on this multi-stage approach [Poujois, 1978], the first stage was not reset. However, the inputoffset voltage of the first stage was still cancelled by storing it on coupling capacitors between the first and second stage during a reset mode. This approach is described Section 10.5.
image_name:Fig. 10.12
description:This is a multi-stage comparator circuit designed to minimize clock feedthrough errors. It includes coupling capacitors to store the input offset voltage of the first stage during a reset mode. The circuit uses two operational amplifiers in sequence, with capacitors providing coupling between stages.

Fig. 10.12 The first stage of the comparator in Fig. 10.11, when the first stage is injecting charge.

#### EXAMPLE 10.4

Assume all capacitors are 0.1 pF , transistor sizes are $\mathrm{W} / \mathrm{L}=4 \mu \mathrm{~m} / 0.2 \mu \mathrm{~m}, \mathrm{C}_{\mathrm{ox}}=8.5 \mathrm{fF} /(\mu \mathrm{m})^{2}$, $\mathrm{L}_{\mathrm{ov}}=0.04 \mu \mathrm{~m}, \mathrm{~V}_{\mathrm{tn}}=0.45 \mathrm{~V}$, and $\mathrm{V}_{\mathrm{DD}}=2 \mathrm{~V}$, and each stage has a gain of 20 . What is the input-offset voltage error caused by the clock feedthrough of the third stage when the third stage comes out of reset?

#### Solution

The values used are identical to those used in Example 10.3. Therefore, the charge-injection at the inverting input of the third stage is the same as that found in the solution to Example 10.3, or -56 mV . The input signal that can overcome this value 56 mV is given by

$$
\begin{equation*}
\Delta \mathrm{V}_{\mathrm{in}}=\frac{56 \mathrm{mV}}{\mathrm{~A}_{1} \mathrm{~A}_{2}}=140 \mu \mathrm{~V} \tag{10.9}
\end{equation*}
$$

Thus, the equivalent input-offset voltage is $140 \mu \mathrm{~V}$, which is much better than the resolution found in Example 10.3 of 56 mV .

### 10.3.3 Speed of Multi-Stage Comparators

The approach just described can be used to realize very-high-resolution comparators, especially when it is combined with fully differential circuit design techniques. However, this approach does have the limitation that it requires multiple-phase clock waveforms, which slow down the circuits.

Although the multi-stage approach is limited in speed due to the need for the signal to propagate through all the stages, it can still be reasonably fast because each of the individual stages can be made to operate fast. Typically, each stage consists of a single-stage amplifier that has only a $90^{\circ}$ phase shift and therefore does not need compensation capacitors (i.e., each stage has a $90^{\circ}$ phase margin without compensation). To see why this multistage approach can be fast, consider the simplified case of a cascade of first-order, uncompensated inverters, as shown in Fig. 10.13. This circuit is a very rough approximation of a multi-stage comparator when it is not being reset. The parasitic load capacitance at the output of the ith stage is approximately given by

$$
\begin{equation*}
C_{p i} \cong C_{0-i}+C_{g s-i+1} \tag{10.10}
\end{equation*}
$$

where $\mathrm{C}_{0-\mathrm{i}}$ is the output capacitance of the ${ }_{i}$ th stage, which would normally be due to junction capacitances, and $\mathrm{C}_{\mathrm{gs}-\mathrm{i}+1}$ is the gate-source capacitance of the input transistor of the succeeding stage. Equation (10.10) will not necessarily be true for the last stage, but the load of the last stage should be of roughly the same magnitude. If one
image_name:Fig. 10.13
description:The circuit is a cascade of first-order gain stages forming a comparator. Each stage consists of a current source and a capacitor, suggesting integration of signals. The capacitors are connected to ground, indicating AC coupling or filtering.

Fig. 10.13 Realizing a comparator by using a cascade of first-order gain stages.
assumes the stages are matched, then normally $\mathrm{C}_{0 . \mathrm{i}}<\mathrm{C}_{\mathrm{gs}-\mathrm{i}+1}$ since junction capacitances are usually less than gatesource capacitances, implying that one can usually assume

$$
\begin{equation*}
C_{p i}<2 C_{g s-i} \tag{10.11}
\end{equation*}
$$

The unity-gain frequency of a single stage is then on the order of

$$
\begin{equation*}
\omega_{\mathrm{ti}} \sim \frac{g_{\mathrm{mi}}}{2 C_{\mathrm{gs-i}}} \tag{10.12}
\end{equation*}
$$

or larger, where $\mathrm{g}_{\mathrm{mi}}$ is the transconductance of the input capacitor of the i th stage. Thus, the unity-gain frequency of a single gain-stage is on the order of one-half the unity-gain frequency of a single transistor. If one assumes the ith stage has a dc gain $A_{0-i}$ and that the ith stage is well described by a first-order transfer function, then the transfer function of a single stage is approximately given by

$$
\begin{equation*}
A_{i}(s)=\frac{A_{0-i}}{1+s / \omega_{p-i}} \tag{10.13}
\end{equation*}
$$

where

$$
\begin{equation*}
\omega_{p-i} \cong \frac{\omega_{\mathrm{ti-}}}{\mathrm{~A}_{0-\mathrm{i}}} \sim \frac{\mathrm{~g}_{\mathrm{mi}}}{2 \mathrm{~A}_{0-\mathrm{i}} \mathrm{C}_{\mathrm{gs-i}}} \tag{10.14}
\end{equation*}
$$

Thus, the $-3-\mathrm{dB}$ frequency of a single stage is on the order of one-half the unity-gain frequency of a transistor divided by the gain of the stage. If one has a cascade of n stages, then the overall transfer function is given by

$$
\begin{equation*}
\mathrm{A}_{\text {total }}(\mathrm{s})=\prod \mathrm{A}_{i}(\mathrm{~s}) \tag{10.15}
\end{equation*}
$$

This result can be approximated by a first-order transfer function, where all higher-order terms are ignored, resulting in

$$
\begin{equation*}
\mathrm{A}_{\text {total }}(\mathrm{s}) \cong \frac{1 \mathrm{~A}_{0-\mathrm{i}}}{1+\mathrm{s} \sum 1 / \omega_{\mathrm{p}-\mathrm{i}}} \cong \frac{\mathrm{~A}_{0}^{\mathrm{n}}}{1+\mathrm{ns} / \omega_{\mathrm{p}-\mathrm{i}}} \tag{10.16}
\end{equation*}
$$

Thus, a cascade of n stages has a time constant approximately given by

$$
\begin{equation*}
\tau_{\text {total }} \cong \frac{2 \mathrm{nA}_{0} \mathrm{C}_{\mathrm{gs}}}{\mathrm{~g}_{\mathrm{m}}} \cong 2 \mathrm{nA}_{0} \tau_{\mathrm{T}} \tag{10.17}
\end{equation*}
$$

where $\tau_{T}=C_{g s} / g_{m}$ is the approximate transit time of a single transistor (i.e., 1 over the unity-gain frequency of a single transistor). In other words, the time constant of the cascade of first-order stages is approximately equal to n times the time constant of a single stage, which is roughly given by $2 \mathrm{~A}_{0}$ times the transit time of a single transistor. This result should be compared to using a single opamp, which, for the same overall gain, will have a time constant considerably greater than $2 \mathrm{~A}_{0}^{n}$ times the transit time of a single transistor. Although the preceding speed estimate is valid for simple single-ended stages only, the general principles apply to more complicated, fully differential stages as long as each stage is first order and doesn't require compensation.

Equation (10.17) can be simplified further. Recall from Chapter 1 that

$$
\begin{equation*}
C_{g s}=\frac{2}{3} C_{o x} W L \tag{10.18}
\end{equation*}
$$

for a transistor in the active region, and that

$$
\begin{equation*}
\mathrm{g}_{\mathrm{m}}=\sqrt{2 \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L}) \mathrm{I}_{\mathrm{D}}} \tag{10.19}
\end{equation*}
$$

We can substitute (10.18) and (10.19) into (10.17), and, after simple manipulation, arrive at
where, again from Chapter 1,

$$
\begin{equation*}
V_{\text {eff }}=\sqrt{\frac{2 I_{D}}{\mu_{n} C_{o x}(W / L)}} \tag{10.21}
\end{equation*}
$$

Equation (10.20) is very useful in quickly accessing the speed and resolution capabilities of a given technology. It also gives some insight into designing comparators. First, the effective gate-source voltages of input drivers of each stage should be as large as possible to maximize speed. Second, the widths of the transistors have little effect on comparator speed, assuming they are large enough so that $\mathrm{C}_{\mathrm{gs}}$ dominates parasitic capacitances due to interconnect and external loading. However, larger input transistor sizes will be better matched, resulting in less offset, and will generally have higher transconductance, resulting in lower input-referred noise.

#### EXAMPLE 10.5

Assume for a $0.2-\mu \mathrm{m}$ technology that $\mathrm{A}_{0}=20, \mathrm{n}=3, \mathrm{~V}_{\text {eff }}=0.5 \mathrm{~V}$, and $\mu_{\mathrm{n}}=0.03 \mathrm{~m}^{2} / \mathrm{V} \cdot \mathrm{s}$. What is the maximum clocking frequency of the comparator?

#### Solution

Using (10.20), we have $\tau_{\text {total }}=0.21 \mathrm{~ns}$. If we assume that $3 \tau$ is required for each half period, then a complete period requires $6 \tau$, which corresponds to a clocking frequency of 781 MHz . The resolution is on the order of $2 \mathrm{~V} / \mathrm{A}_{0}^{\mathrm{n}}=0.25 \mathrm{mV}$.

## 10.4 LATCHED COMPARATORS

Modern high-speed comparators typically have one or two stages of preamplification followed by a track-andlatch stage, as Fig. 10.14 [Yukawa, 1985] shows in simplified form for a CMOS implementation. The rationale
image_name:Fig. 10.14
description:The circuit is a high-speed comparator with a preamplifier stage followed by a track-and-latch stage. The preamplifier stage increases the input signal resolution, while the track-and-latch stage further amplifies the signal and minimizes kickback effects. The comparator uses NMOS transistors in the latch to achieve high-speed operation.

Fig. 10.14 A typical architecture for a high-speed comparator.
behind this architecture is as follows: The preamplifier or preamplifiers are used to obtain higher resolution and to minimize the effects of kickback (which will be explained shortly). The output of the preamplifier, although larger than the comparator input, is still much smaller than the voltage levels needed to drive digital circuitry. The track-and-latch stage then amplifies this signal further during the track phase, and then amplifies it again during the latch-phase, when positive feedback is enabled. The positive feedback regenerates the analog signal into a full-scale digital signal. The track-and-latch stage minimizes the total number of gain stages required, even when good resolution is needed, and, thus, is faster than the multi-stage approach just described.

The preamplifier typically has some gain, perhaps 2 to 10 . The preamplifier usually does not have gains much greater than 10 ; otherwise its time constant is too large and its speed is limited. One or two simple resistively-loaded differential pair stages are often suitable. Note that the input offset and noise of the track-and-latch stage are attenuated by the gain of the preamplifier when referred to the comparator input. Hence, assuming it provides at least a modest gain, the preamplifier's noise and offset will often limit the noise and offset of the comparator. ${ }^{5}$ If very high speed but only moderate resolution is required, the preamplifier may sometimes simply be a unity-gain buffer.

It is not good practice to eliminate the preamplifier altogether since kickback into the driving circuitry will then result in very limited accuracy. Kickback denotes the charge transfer either into or out of the inputs when the track-and-latch stage goes from track mode to latch mode. This charge transfer is caused by the charge needed to turn the transistors in the positive-feedback circuitry on and by the charge that must be removed to turn transistors in the tracking circuitry off. Without a preamplifier or buffer, this kickback will enter the driving circuitry and cause very large glitches, especially in the case when the

Key Point: Latched comparators typically employ a simple preamplifier to mitigate kickback and reduce the requirements placed upon the latch stage, followed by a latch which alternates between a reset phase and a positive feedback phase that quickly generates full-swing digital signals from the preamplifier output.
impedances seen looking into the two inputs are not perfectly matched.

In high-resolution applications, capacitive coupling and reset switches are also typically included to eliminate any input-offset-voltage and clock-feedthrough errors, in a manner similar to that described in Sections 10.2 and 10.3.

One very important consideration for comparators is to ensure that no memory is transferred from one decision cycle to the next. Recall that when a comparator toggles in one direction, it might have a tendency to stay in that direction, referred to as hysteresis. To eliminate hysteresis, one can reset the different stages before entering track mode. This might be achieved by connecting internal nodes to one of the power supplies or by connecting differential nodes together using switches before entering track mode. For example, the comparator shown in Fig. 10.14 has internal nodes of the latch reset to both $\mathrm{V}_{\mathrm{DD}}$ and ground when the $\mathrm{V}_{\text {Itch }}$ signal is low. Not only does this eliminate memory, but it also sets the comparator to its trip point, which speeds up operation when the comparator resolves small input signals.

Another consideration for comparators is that the gain in track mode should not be too large; otherwise the time constants are too large, which limits the speed.

The track-and-latch stage has many variations. The circuitry shown in Fig. 10.14 should be considered only symbolic, although it will suffice in many applications.

### 10.4.1 Latch-Mode Time Constant

The time constant of the latch, when it is in its positive-feedback (i.e., latch) phase, can be found by analyzing a simplified circuit consisting of two back-to-back inverters, such as those shown in Fig. 10.15. If we assume that the output voltages of the inverters are close to each other at the beginning of the latch phase, and that the inverters are in their linear range, then each of the inverters can be modelled as a voltage controlled current source driving an
5. The reader may refer to Chapters 2 and 9 to see what determines the random offset and noise, respectively, of simply designed preamplifiers, such as a resistively loaded differential pair.

Fig. 10.15 Two back-to-back inverters used as a simplified model of a track-and-latch stage in its latch phase.
image_name:Fig. 10.15
description:The circuit consists of two back-to-back inverters forming a loop. The input and output of the first inverter are connected to the output and input of the second inverter, respectively, creating a feedback loop between nodes Vy and Vx.

RC load, as shown in Fig. 10.16, where $A_{V}$ is the low-frequency gain of each inverter, which has a transconductance given by $G_{m}=A_{V} / R_{L}$. For this linearized model, we have

$$
\begin{equation*}
\frac{A_{v}}{R_{L}} V_{y}=-C_{L}\left(\frac{d V_{x}}{d t}\right)-\left(\frac{V_{x}}{R_{D}}\right) \tag{10.22}
\end{equation*}
$$

and

$$
\begin{equation*}
\frac{A_{v}}{R_{L}} V_{x}=-C_{L}\left(\frac{d V_{y}}{d t}\right)-\left(\frac{V_{y}}{R_{L}}\right) \tag{10.23}
\end{equation*}
$$

Multiplying (10.22) and (10.23) by $\mathrm{R}_{\mathrm{L}}$ and rearranging gives

$$
\begin{equation*}
\tau\left(\frac{d V_{x}}{d t}\right)+V_{x}=-A_{v} V_{y} \tag{10.24}
\end{equation*}
$$

and

$$
\begin{equation*}
\tau\left(\frac{d V_{y}}{d t}\right)+V_{y}=-A_{v} V_{x} \tag{10.25}
\end{equation*}
$$

where $\tau=R_{\llcorner } C_{\llcorner }$is the time constant at the output node of each inverter. Subtracting (10.25) from (10.24) and rearranging terms gives

$$
\begin{equation*}
\left(\frac{\tau}{\mathrm{A}_{\mathrm{V}}-1}\right)\left(\frac{\mathrm{d} \Delta \mathrm{~V}}{\mathrm{dt}}\right)=\Delta \mathrm{V} \tag{10.26}
\end{equation*}
$$

where $\Delta \mathrm{V}=\mathrm{V}_{\mathrm{x}}-\mathrm{V}_{\mathrm{y}}$ is the voltage difference between the output voltages of the inverters. Equation (10.26) is a first-order differential equation with no forcing function. Its solution is given by

$$
\begin{equation*}
\Delta V=\Delta V_{0} e^{\left(A_{v}-1\right) t / \tau} \tag{10.27}
\end{equation*}
$$

Fig. 10.16 A linearized model of the track-and-latch stage when it is in its latch phase.
image_name:Fig. 10.16
description:The circuit diagram represents a linearized model of a track-and-latch stage in its latch phase. It involves two voltage-controlled current sources, two capacitors, and two resistors. The circuit is designed to amplify the voltage difference exponentially over time with a specific time constant.

where $\Delta \mathrm{V}_{0}$ is the initial voltage difference at the beginning of the latch phase. Thus, the voltage difference increases exponentially in time with a time constant given by

$$
\begin{equation*}
\tau_{\text {ltch }}=\frac{\tau}{A_{V}-1} \cong \frac{R_{L} C_{L}}{A_{V}}=\frac{C_{L}}{G_{m}} \tag{10.28}
\end{equation*}
$$

where, again, $G_{m}=A_{V} / R_{L}$ is the transconductance of each inverter. Note that $\tau_{\text {tton }}$ is roughly equal to the inverse of the unity-gain frequency of each inverter.

In the case of MOS devices, normally the output load is proportional to the gate-source capacitance of a single transistor, or specifically,

$$
\begin{equation*}
C_{\mathrm{L}}=\mathrm{K}_{1} \mathrm{WLC}_{\mathrm{ox}} \tag{10.29}
\end{equation*}
$$

Here, $\mathrm{K}_{1}$ is a proportionality constant, usually between 1 and 2 . Also, the inverter transconductance is proportional to the transconductance of a single transistor, and is given by

$$
\begin{equation*}
\mathrm{G}_{\mathrm{m}}=\mathrm{K}_{2} \mathrm{~g}_{\mathrm{m}}=\mathrm{K}_{2} \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}} \frac{\mathrm{~W}}{\mathrm{~L}} \mathrm{~V}_{\text {eff }} \tag{10.30}
\end{equation*}
$$

where $\mathrm{K}_{2}$ might be between 0.5 and 1 . Substituting (10.29) and (10.30) into (10.28) gives

$$
\begin{equation*}
\tau_{\text {ltch }}=\frac{\mathrm{K}_{1}}{\mathrm{~K}_{2}} \frac{\mathrm{~L}^{2}}{\mu_{\mathrm{n}} \mathrm{~V}_{\mathrm{eff}}}=\mathrm{K}_{3} \frac{\mathrm{~L}^{2}}{\mu_{\mathrm{n}} \mathrm{~V}_{\mathrm{eff}}} \tag{10.31}
\end{equation*}
$$

where $\mathrm{K}_{3}$ might be between 2 and 4 . Note that (10.31) implies that $\tau_{\text {Itch }}$ depends primarily on the technology and not on the design (assuming a reasonable choice of $V_{\text {eff }}$ and that $C_{L}$ is minimized). Note also the similarity between (10.31) and (10.20), the equation for the time constant of a cascade of gain stages. For a given technology, (10.31) is very useful in determining a rough estimate for the maximum clock frequency of a latch-and-track comparator.

If it is necessary for a voltage difference of $\Delta \mathrm{V}_{\text {logic }}$ to be obtained in order for succeeding logic circuitry to safely recognize the correct output value, then, by using (10.27), we find the time necessary for this to happen is given by

$$
\begin{equation*}
\mathrm{T}_{\text {tlch }}=\frac{\mathrm{C}_{\mathrm{L}}}{\mathrm{G}_{\mathrm{m}}} \ln \left(\frac{\Delta \mathrm{~V}_{\text {logic }}}{\Delta \mathrm{V}_{0}}\right)=\mathrm{K}_{3} \frac{\mathrm{~L}^{2}}{\mu_{\mathrm{n}} \mathrm{~V}_{\text {eff }}} \ln \left(\frac{\Delta \mathrm{V}_{\text {logic }}}{\Delta \mathrm{V}_{0}}\right) \tag{10.32}
\end{equation*}
$$

If $\Delta \mathrm{V}_{0}$ is small, this latch time can be large, perhaps larger than the allowed time for the latch phase. Such an occurrence is often referred to as metastability. In other words, because its initial value is too small, the differential output voltage of the latch does not increase enough to be recognized as the correct logic value by succeeding circuitry. Sometimes, even when the initial voltage difference is large enough, it is possible that circuit noise can cause the initial voltage difference to become small enough to cause metastability.

Key Point: A positive-feedback latch output grows exponentially with a time constant given by the unity-gain frequency, $\mathrm{G}_{\mathrm{m}} / \mathrm{C}_{\mathrm{L}}$. When the initial input is too small, metastability may occur whereby the growth is too slow for a recognizable logic signal to appear at the latch output before the onset of the reset phase.

#### EXAMPLE 10.6

Assume for a $0.2-\mu \mathrm{m}$ technology that $\mathrm{K}_{3}=2.5, \quad \Delta \mathrm{~V}_{0}=1 \mathrm{mV}, \Delta \mathrm{V}_{\text {logic }}=1 \mathrm{~V}, \mathrm{~V}_{\text {eff }}=0.5 \mathrm{~V}$, and $\mu_{\mathrm{n}}=0.03 \mathrm{M}^{2} / \mathrm{V} \cdot \mathrm{s}$. What is the maximum clocking frequency of the comparator?

#### Solution

Using (10.32), we have $\mathrm{T}_{\text {Itch }}=46 \mathrm{ps}$. Assuming this is half the total period (which might be quite an optimistic assumption), the smallest possible period for a track-and-latch might be 92 ps , which corresponds to a clocking frequency of 11 GHz . In a typical comparator, the maximum clock rate would probably be limited by the frequency response of the preamplifiers and the track-and-latch during the track phase, rather than by the speed of the latch during the latch phase.

### 10.4.2 Latch Offset

The input offset of a latch is influenced by random and systematic mismatch between its two half-circuits. When very small transistors are used, this mismatch may be significant often leading of offset of 10 's of mV or more. In such cases, additional components may be introduced to so that by appropriately controlling the imbalances in the circuit, the effects of random mismatch can be cancelled, resulting in a latch with near-zero overall offset.

The latch model in Fig. 10.16 is modified in Fig. 10.17 to illustrate several contributors to latch offset. The imbalances $i_{01} \neq i_{02}, G_{m 1} \neq G_{m}$, etc. may be due to random mismatch and/or they may be introduced intentionally to provide a means of adjusting the latch offset. Clearly, when $i_{01} \neq i_{02}$ and/or $G_{m 1} \neq G_{m 2}$ some offset is introduced since, with $V_{x}=V_{y} \neq 0$, different currents flow in each half circuit. However, even if the offset current $i_{0}$ and transconductances $G_{m}$ are perfectly matched and $V_{x}(0)=V_{y}(0) \neq 0$, if the $R_{L}$ loads are mismatched the node voltages $V_{x}$ and $V_{y}$ will respond with different time constants immediately giving rise to a finite differential voltage $\Delta \mathrm{V}=\mathrm{V}_{\mathrm{x}}=\mathrm{V}_{\mathrm{y}}$ which in turn initiates the circuit's positive feedback, eventually regenerating a logic signal. The evolution of the node voltages in this circumstance is illustrated in Fig. 10.18.

Key Point: Latches have offset due to imbalances between the two half-circuits providing positive feedback. Imbalances arise due to random mismatch. Additional controllable imbalances are sometimes included by design in order to cancel random offsets and provide an accurate comparator.

A latch incorporating an offset adjustment mechanism is shown in Fig. 10.19 [Cho, 1995]. In latch mode, the cross-coupled pair $Q_{1,2}$ is source-degenerated by the triode transistors, $Q_{3-6}$. Hence the transconductance of each half-circuit, $\mathbf{G}_{\mathrm{m} 1,2}$, depends upon the applied differential voltage $\mathrm{V}_{\text {ref }}^{ \pm}$and the input voltage $\mathrm{V}_{\mathrm{in}}^{ \pm}$. A dc current $\mathrm{i}_{\text {。 }}$ flows at the onset of latch mode since the node voltages $\mathrm{V}_{\text {out }}^{ \pm}$have been reset to the positive supply, and all NMOS transistors are turned on. Hence, in the absence of any random mismatch, the latch will be in a balanced state with equal half-circuit currents flowing only when

$$
\begin{equation*}
\Delta \mathrm{V}_{\mathrm{in}}=\left(\frac{\mathrm{W}_{3,6}}{\mathrm{~W}_{4,5}}\right) \Delta \mathrm{V}_{\mathrm{ref}} \tag{10.33}
\end{equation*}
$$

image_name:Fig. 10.17
description:The circuit represents a linearized latch model with a voltage-controlled current source, a capacitor, a resistor, and a current source all connected to a common node Vy. The voltages and currents are referenced to ground.

Fig. 10.17 A linearized model of the latch illustrating various sources of offset, random and/or intended.
image_name:Fig. 10.17
description:The circuit represents a linearized latch model with a voltage-controlled current source, a capacitor, a resistor, and a current source all connected to a common node Vy. The voltages and currents are referenced to ground.

image_name:Fig. 10.18
description:**Type of Graph and Function:**
The graph is a time-domain waveform showing the evolution of voltages at two nodes, Vx and Vy, over time in a latch circuit.

**Axes Labels and Units:**
- The horizontal axis represents time, though specific units are not provided, it is typically in seconds or milliseconds in such contexts.
- The vertical axis represents voltage, likely in volts, though specific units are not provided.

**Overall Behavior and Trends:**
- The graph shows two curves, Vx and Vy, which start from a common point and diverge over time.
- Vx increases over time, indicating a positive trend, while Vy decreases, showing a negative trend.
- The divergence indicates the development of a differential voltage due to different time constants (τ1 ≠ τ2).
- Positive feedback is noted to regenerate logic signals, which suggests that the circuit is amplifying the difference between Vx and Vy.

**Key Features and Technical Details:**
- The initial point where both Vx and Vy start is a crucial point, likely representing the initial condition of the latch.
- The graph highlights two regions with ellipses, indicating critical points where the behavior of the voltages is significant, possibly where the rate of change is most pronounced.
- The system's dynamics are influenced by the different time constants, τ1 and τ2, which affect how quickly Vx and Vy diverge.

**Annotations and Specific Data Points:**
- Annotations on the graph indicate the cause of differential voltage due to different time constants and the role of positive feedback in regenerating logic signals.
- The graph does not provide specific numerical values but emphasizes the qualitative behavior of the voltages over time.

Fig. 10.18 Evolution of the latch node voltages when $i_{01}=i_{02} \neq 0$ and $R_{L 1} C_{L 1} \neq R_{L 2} C_{L 2}$.
image_name:Fig. 10.19
description:The circuit is a latch with controllable offset. It uses a combination of NMOS and PMOS transistors to create a differential output based on input and reference voltages. The circuit is designed to adjust for offsets, potentially due to mismatches or parasitics.

Fig. 10.19 A latch circuit with controllable offset [Cho, 1995].

Equation (10.33) is the latch offset due $\Delta \mathrm{V}_{\text {ref }}$, which may be adjusted to cancel other sources of offset, such as those arising from mismatches in device sizes, parasitics, etc. A rigorous general analysis relating all sources of offset to the circuit parameters is quite complex [He, 2009].

## 10.5 EXAMPLES OF CMOS AND BiCMOS COMPARATORS

This section describes a number of possible high-speed comparators.
The literature on integrated circuit technology has many examples of latched comparators. For example, either of the latches shown in Fig. 10.14 and Fig. 10.19 may be preceded by a resistively loaded differential pair preamplifier to realize a latched comparator. Figure 10.20 shows another comparator [Song, 1990]. It has the positive feedback of the second stage always enabled. In track mode, when the two diode-connected transistors of the gain stage are enabled, the gain around the positive-feedback loop is less than one, and the circuit is stable. The combination of the diode-connected transistors of the gain stage and the transistors of the positive-feedback loop acts as a moderately large impedance and gives gain from the preamplifier stage to the track-and-latch stage. The diode-connected loads of the preamplifier stage give a limited amount of gain in order to maximize speed, while still buffering the kickback from the input circuitry.
image_name:Fig. 10.20
description:The circuit is a two-stage comparator with a preamplifier and a positive-feedback track-and-latch stage. It uses diode-connected loads to keep node impedances low, enhancing speed. Precharging is used to eliminate memory from previous decisions, reducing hysteresis.

Fig. 10.20 A two-stage comparator that has a preamplifier and a positive-feedback track-andlatch stage.

Another comparator is shown in Fig. 10.21 [Norsworthy, 1989]. This design also uses diode-connected loads to keep all nodes at relatively low impedance (similar to current-mode circuit-design techniques), thereby keeping all node time constants small and giving fast operation. It uses precharging to eliminate any memory from the previous decision that might lead to hysteresis. For example, the positive-feedback stage is precharged low, whereas the digital-restoration stage is precharged high, somewhat similar to what is done in Domino CMOS logic [Krambeck, 1982].

Yet another comparator is shown in Fig. 10.22 with appropriate clock waveforms. ${ }^{6}$ This design eliminates any input-offset voltages from both the first and second stages by using capacitive coupling. It also has common-mode feedback circuitry for the first preamplifier stage, which allows for input signals that have large common-mode signals. Unlike in fully differential opamps, in fully differential comparators, the linearity of the common-mode feedback circuitry is noncritical since, whenever large signals are present (and the common-mode feedback circuitry becomes nonlinear), there is no ambiguity in resolving the sign of the input signal. This allows a simple differential pair to be used for CMFB circuitry. Measured (but unpublished) performance of this circuit resulted in a $0.1-\mathrm{mV}$ resolution at a $2-\mathrm{MHz}$ clock frequency, despite a very old $5-\mu \mathrm{m}$ technology. The performance measured was limited by the test setup rather than by the circuitry.

A BiCMOS comparator that exhibits very good performance is described in [Razavi, 1992]. It is based on the idea that it is not necessary to reset the first stage; the input-offset errors of the first stage can still be eliminated by resetting the right side of the coupling capacitors between the first stage and the second stage, assuming that the gain of the first stage is not too large [Poujois, 1978] [Vittoz, 1985]. A simplified schematic of this comparator is shown in Fig. 10.24. During the reset phase, the inputs to the preamplifier are connected directly to
image_name:Fig. 10.21 A two-stage comparator.
description:The circuit is a two-stage comparator with a preamp and latch stages. It employs positive feedback and digital signal-level restoration. The preamp stage is used to amplify the input signal, while the latch stage provides the decision-making capability. The circuit is designed to minimize input-offset errors by resetting the right side of the coupling capacitors.

Fig. 10.21 A two-stage comparator.
ground (or to a reference voltage), and the outputs of the coupling capacitors are connected to ground as well. This stores any offset voltages of the first stage on the capacitors. When the comparator is taken out of reset phase, then the effect of the clock feedthrough of $S_{5}$ and $S_{6}$ on the input resolution is divided by the gain of the first stage. In the realization described in [Razavi, 1992], the first stage is a BiCMOS preamplifier, consisting of MOS source followers followed by a bipolar differential amplifier and emitter-follower output buffers, as shown in Fig. 10.25. Notice that the circuit operates between ground and a negative voltage supply. Note also that the switches are realized using p -channel transistors. The track-and-latch stage has both a bipolar latch and a CMOS latch, as shown in Fig. 10.23. During the reset phase, $\phi_{1}$ is low and $\phi_{2}$ is high, $X_{1}$ and $Y_{1}$ are connected to ground through switches $M_{1}$ and $M_{2}, C_{3}$ is discharged to the minus supply through $M_{11}$, and $X_{2}$ and $Y_{2}$ are discharged to the minus supply through $M_{9}$ and $M_{10}$. Also, at this time, $M_{3}$ and $M_{4}$ are off. Next, $\phi_{1}$ becomes high, which leaves $X_{1}$ and $Y_{1}$ floating and connects the outputs of the preamplifier to its input signal. After a short delay, which is needed for the transient response of the preamplifier, $\phi_{2}$ becomes low, which turns on $M_{12}$, thereby activating the positive feedback action of $Q_{5}$ and $Q_{6}$. This develops a differential voltage between $X_{1}$ and $Y_{1}$ of about 200 mV , since $C_{3}$ is about one-fifth the size of $C_{1}$ and $C_{2}$. The offset of this bipolar latch is quite small, typically on the order of one millivolt or less. Also note that, when activated, the only power dissipated is that required to charge $\mathrm{C}_{3}$-there is no dc power dissipation. A short time after the bipolar latch is activated, the inverter connected to $C_{3}$ changes state, and its output voltage will drop. This low voltage turns on $M_{3}$ and $M_{4}$, which activates the CMOS part of the latch consisting of cross-coupled $M_{5}$ and $M_{6}$ and cross-coupled
image_name:Fig. 10.22
description:The circuit is a two-stage comparator with capacitive coupling to eliminate input-offset-voltage and clock-feedthrough errors. It includes a first switched-capacitor gain stage and a second gain stage, with positive feedback for fast operation. The timing diagram shows the clock phases used for the switches.
image_name:Fig. 10.22
description:The diagram illustrates a two-stage comparator circuit with capacitive coupling designed to eliminate input-offset-voltage and clock-feedthrough errors, while incorporating positive feedback for rapid operation. It consists of several key components and stages:

1. **First Switched-Capacitor Gain Stage:**
- The input voltage \( V_{in} \) is fed into this stage through capacitors \( C_{1A} \) and \( C_{1B} \).
- The stage employs switches controlled by clock signals \( \phi_1 \) and \( \phi_2 \) to manage the charge transfer and amplification.
- There is a common-mode feedback mechanism to stabilize the output.

2. **Second Gain Stage:**
- This stage is coupled with capacitor \( C_{2A} \) and uses additional switches controlled by clock signals \( \phi_1'' \) and \( \phi_1' \).
- The gain is further amplified and stabilized through common-mode feedback.

3. **Positive Feedback Stage:**
- This stage enhances the speed of operation by providing regenerative feedback, which helps in rapidly driving the output to a stable state.

4. **Clock Signals:**
- The diagram includes timing diagrams for the clock signals \( \phi_1 \), \( \phi_1' \), \( \phi_1'' \), and \( T_{rk} \), showing their respective phases and durations. These signals control the switching actions in the circuit, crucial for the proper timing of charge transfer and amplification.

Overall, the circuit is designed to provide fast and accurate signal comparison by efficiently managing charge transfer and amplification through switched-capacitor techniques and positive feedback.

Fig. 10.22 A two-stage comparator with capacitive coupling to eliminate input-offset-voltage and clock-feedthrough errors, along with positive feedback for fast operation.
image_name:Fig. 10.23
description:The circuit is a two-stage comparator with capacitive coupling designed to eliminate input-offset-voltage and clock-feedthrough errors. It uses switched-capacitor techniques and positive feedback for fast operation. The cross-coupled transistors Q5 and Q6 prevent nodes X1 and Y1 from being discharged too far.

Fig. 10.23 The BiCMOS track-and-latch stage in [Razavi, 1992].
image_name:Fig. 10.24
description:
[
name: S1, type: Switch, ports: {N1: Vin, N2: phi1}
name: S2, type: Switch, ports: {N1: Vin, N2: phi1}
name: S3, type: Switch, ports: {N1: phi1, N2: GND}
name: S4, type: Switch, ports: {N1: phi1, N2: GND}
name: S5, type: Switch, ports: {N1: phi1, N2: GND}
name: S6, type: Switch, ports: {N1: phi1, N2: GND}
name: OpAmp, type: OpAmp, ports: {InP: phi1, InN: phi1, OutP: phi1, OutN: phi1}
name: Positive-feedback latch, type: Other, ports: {N1: phi1, N2: Vout}
]
extrainfo:The circuit is a two-stage comparator with capacitive coupling designed to eliminate input-offset-voltage and clock-feedthrough errors. It uses switched-capacitor techniques and positive feedback for fast operation. The cross-coupled transistors prevent nodes from being discharged too far. The latch amplifies the 200-mV difference signal to a full-level CMOS voltage change, making the latch accurate, fast, and low power.

Fig. 10.24 A simplified schematic of the comparator described in [Razavi, 1992].
$M_{7}$ and $M_{8}$. The reasons for including cross-coupled $M_{5}$ and $M_{6}$ are to prevent nodes $X_{1}$ and $Y_{1}$ from being discharged very far from ground toward the minus power supply and at the same time to amplify the $200-\mathrm{mV}$ difference signal developed by the bipolar latch to almost a full-level CMOS voltage change. Thus, the latch is accurate, relatively fast, and low power. Also described in [Razavi, 1992] is an interesting CMOS-only comparator, which is not described here, but which interested readers may investigate.

### 10.5.1 Input-Transistor Charge Trapping

When realizing very accurate CMOS comparators, an error mechanism that must be considered is charge trapping in the gate oxide of the input transistors of the MOS comparators [Tewksbury, 1989]. When n -channel transistors are stressed with large positive gate voltages, electrons can become trapped via a tunneling mechanism in which
image_name:Fig. 10.25 A BiCMOS preamplifier.
description:The circuit diagram is a BiCMOS preamplifier with two differential inputs (V+in and V-in) and differential outputs (V+out and V-out). It uses NMOS transistors controlled by a clock signal Phi1 to modulate input signals. The diodes and resistors are used for biasing and load purposes. Current sources are used to ensure proper operation and biasing of the circuit.

Fig. 10.25 A BiCMOS preamplifier.
electrons tunnel to oxide traps close to the conduction band. The time constant for the release of these trapped electrons is on the order of milliseconds, much longer than the time it takes for them to become trapped. During the time they are trapped, the effective transistor threshold voltage is increased. This leads to a comparator hysteresis on the order of 0.1 to 1 mV . This effect correlates well with transistor $1 / \mathrm{f}$ noise and is much smaller in p-channel transistors. When very accurate comparators are needed, charge trapping must be considered and minimized. One possible means of minimizing this effect, assuming we have a BiCMOS technology, is described in [Miller, 1990] and is illustrated in Fig. 10.26. A BiCMOS technology allows diodes to be used in the input
image_name:Fig. 10.26
description:The circuit is a comparator with p-channel inputs designed to minimize hysteresis by using small bias currents and current mirrors. The use of p-channel transistors reduces charge trapping effects, leading to more accurate comparator operation.

Fig. 10.26 A comparator with little hysteresis. (Hysteresis is caused by charge trapping.)
stage, which allows the inclusion of two additional small-current sources in the input stage; this guarantees that the p -channel input transistors never turn off. ${ }^{7}$ Also, by using p -channel input transistors, the charge trapping is greatly minimized because p -channel transistors exhibit much less hysteresis than n -channel transistors.

An alternative approach is to flush the input transistors after each use where the junctions and wells of n -channel transistors are connected to a positive power supply whereas the gates are connected to a negative power supply. This effectively eliminates the trapped electrons [Swanson, 1993]. Alternatively, or in addition, two input stages can be used for the comparator-a rough stage can be used during times when large signals with overloads are possible, whereas a fine stage can be used during times when accurate comparisons are necessary and it can be guaranteed that no large signals are present [Swanson, 1993; Tan, 1990].

## 10.6 EXAMPLES OF BIPOLAR COMPARATORS

High-speed bipolar comparators are typically latched comparators, as shown previously in Fig. 10.14, where preamplifier and track-and-latch stages are used. A typical example is shown in Fig. 10.27 [Wakimoto, 1988]. The preamplifier is a simple differential amplifier that might have a gain of around 5 . Besides increasing the resolution, this preamplifier helps to eliminate kickback from the track-and-latch stage. The track-and-latch stage is very similar to a current-mode digital latch. During track phase, the differential pair consisting of transistors $Q_{3}$ and $Q_{4}$ is enabled and operates as a second differential amplifier. When latch mode is enabled, $I_{2}$ is diverted to the differential pair consisting of $Q_{5}$ and $Q_{6}$. The inputs to this third differential pair come
image_name:Fig. 10.27 A typical bipolar comparator.
description:The circuit is a typical bipolar comparator consisting of a preamplifier and a track-and-latch stage. The preamplifier uses differential pairs Q1-Q2, and the track-and-latch stage uses differential pairs Q3-Q4 and Q5-Q6. Emitter followers Q9 and Q10 buffer the outputs of the second differential pair. Positive feedback is implemented through cross-coupling of Q5 and Q6.

Fig. 10.27 A typical bipolar comparator.

[^1]image_name:Fig. 10.28 A typical bipolar comparator.
description:The circuit is a typical bipolar comparator consisting of a preamplifier and a track-and-latch stage. The preamplifier uses differential pairs Q1-Q2, and the track-and-latch stage uses differential pairs Q3-Q4 and Q5-Q6. Emitter followers Q7 and Q8 buffer the outputs of the second differential pair. Positive feedback is implemented through cross-coupling of Q5 and Q6.

Fig. 10.28 A second bipolar comparator.
from the outputs of the second differential pair through emitter-follower buffers consisting of $Q_{9}$ and $Q_{10}$. The outputs of the third differential pair are connected back to the high-impedance output nodes in a crosscoupled manner so that positive feedback results. When this positive feedback is enabled, it takes the initiallysmall differential voltage and quickly amplifies it to between 0.4 and 0.6 V (depending on the logic levels being used). There are two reasons for using the emitter-follower buffers. These buffers isolate the highimpedance nodes at the collectors of the second and third differential pairs from the base-emitter capacitances of the third differential pair. They also isolate the same high impedance nodes from the output load capacitance.

Another architecture for a bipolar comparator is shown in Fig. 10.28 [Van de Plassche, 1988]. In this comparator, the input signals go to a differential pair that is always turned on (even during the latch phase). During the track phase, $Q_{3}$ and $Q_{4}$ are on. They operate as common-base transistors, and therefore the comparator operates as a cascode amplifier during this phase. When the comparator goes into latch mode, the collector current from the input transistors is redirected from the common-base transistors to transistors $Q_{7}$ and $Q_{8}$, which are connected in a positive-feedback loop. Since the bias current of the input transistors is never turned off, the kickback from them is greatly reduced without adding additional preamplifier stages. This maximizes the bandwidth during the tracking phase.

A third bipolar comparator is shown in Fig. 10.29. Although this comparator has never been experimentally tested, it is used as an example to illustrate many comparator design principles. A small current source is added to the tracking differential pair so that this differential pair doesn't turn off completely when the comparator is in hold mode. This makes the comparator faster when it goes from hold mode into track mode. Also, a cascode common-base stage is added just below the output voltages. This stage is used to isolate the outputs from the positive-feedback loop. This in turn allows for much smaller resistors to be used in the positive-feedback loop, which speeds this loop up and eliminates the need for emitter-follower buffers in the loop. Finally, a larger resistor is added between the emitters of the cascode transistors. This resistor prevents the cascode transistors from turning off completely during the latch phase, which also speeds up the transition from latch mode to tracking mode.
image_name:Fig. 10.29 A third bipolar comparator
description:The circuit is a third bipolar comparator with a cascode stage to improve speed and prevent transistors from turning off. It uses moderately small resistors in the positive-feedback loop to enhance speed and eliminate the need for emitter-follower buffers. A larger resistor is used to keep the cascode transistors active during the latch phase, improving the transition to the tracking mode. Small bias currents are used to prevent transistors from turning off.

Fig. 10.29 A third bipolar comparator.

## 10.7 KEY POINTS

- The input offset of a comparator is the input at which the output is equally likely to be high or low. Noise determines how the output statistics vary as a function of input. [p. 413]
- Hysteresis is "memory" in a comparator that tends to make it remain in its past output state, usually due to charge retained on internal circuit capacitances. [p. 414]
- Regular opamps are compensated to ensure stability in closed-loop configurations, resulting in a low 3-dB bandwidth and, hence, very slow settling if used open-loop as a comparator. [p. 417]
- An input capacitor is sometimes used to sample the input offset voltage of a comparator during a reset phase, and then subtract it from the input during the comparison phase. [p. 417]
- As a MOSFET goes from triode mode to off, the charge stored in the channel region must flow out of the transistor terminals; in a comparator, the charge may accumulate on circuit capacitances causing offset. [p. 420]
- The deleterious effects of charge-injection can be reduced by using "advanced" clocks which open-circuit the discharge paths through which signal-dependent charge-injection flows. [p. 421]
- Latched comparators typically employ a simple preamplifier to mitigate kickback and reduce the requirements placed upon the latch stage, followed by a latch which alternates between a reset phase and a positive feedback phase that quickly generates full-swing digital signals from the preamplifier output. [p. 427]
- A positive-feedback latch output grows exponentially with a time constant given by the unity-gain frequency, $\mathrm{G}_{\mathrm{m}} / \mathrm{C}_{\mathrm{L}}$. When the initial input is too small, metastability may occur whereby the growth is too slow for a recognizable logic signal to appear at the latch output before the onset of the reset phase. [p. 429]
- Latches have offset due to imbalances between the two half-circuits providing positive feedback. Imbalances arise due to random mismatch. Additional controllable imbalances are sometimes included by design in order to cancel random offsets and provide an accurate comparator. [p. 430]
