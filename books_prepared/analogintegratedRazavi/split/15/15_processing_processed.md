# CHAPTER 16 Phase-Locked Loops

The concept of phase locking was invented in the 1930s and swiftly found wide usage in electronics and communication. While the basic phase-locked loop has remained nearly the same since then, its implementation in different technologies and for different applications continues to challenge designers. A PLL serving the task of clock generation in a microprocessor appears quite similar to a frequency synthesizer used in a cellphone, but the actual circuits are designed quite differently.

This chapter deals with the analysis and design of PLLs, with particular attention to implementations in VLSI technologies. A thorough study of PLLs would require an entire book by itself, but our objective here is to lay the foundation for more advanced work. Beginning with a simple PLL architecture, we study the phenomenon of phase locking and analyze the behavior of PLLs in the time and frequency domains. We then address the problem of lock acquisition and describe charge-pump PLLs (CPPLLs) and their nonidealities. Finally, we examine jitter in PLLs, study delay-locked loops (DLLs), and present a number of PLL applications.

## 16.1 ■ Simple PLL

A PLL is a feedback system that compares the output phase with the input phase. The comparison is performed by a "phase comparator" or "phase detector" (PD). It is therefore beneficial to define the PD rigorously.

### 16.1.1 Phase Detector

A phase detector is a circuit whose average output, $\overline{V_{\text {out }}}$, is linearly proportional to the phase difference, $\Delta \phi$, between its two inputs (Fig. 16.1). In the ideal case, the relationship between $\overline{V_{\text {out }}}$ and $\Delta \phi$ is linear, crossing the origin for $\Delta \phi=0$. Called the "gain" of the PD, the slope of the line, $K_{P D}$, is expressed in V/rad.
image_name:Figure 16.1
description:The graph in Figure 16.1 represents the output behavior of a phase detector. It is a linear plot showing the relationship between the average output voltage, \( \overline{V_{\text{out}}} \), and the phase difference, \( \Delta \phi \), between two input signals.

1. **Type of Graph and Function:**
- This is a linear graph depicting the function of a phase detector.

2. **Axes Labels and Units:**
- The horizontal axis represents the phase difference \( \Delta \phi \) in radians.
- The vertical axis represents the average output voltage \( \overline{V_{\text{out}}} \) in volts.
- The scales on both axes are linear.

3. **Overall Behavior and Trends:**
- The graph shows a straight line passing through the origin, indicating a direct proportionality between the phase difference and the output voltage.
- The slope of the line is positive, representing the gain of the phase detector, \( K_{PD} \), which is the ratio of the change in output voltage to the change in phase difference (V/rad).

4. **Key Features and Technical Details:**
- The line crosses the origin, which means that when there is no phase difference (\( \Delta \phi = 0 \)), the average output voltage is zero.
- The slope of the line represents the gain \( K_{PD} \), which is a crucial parameter for the phase detector's performance.

5. **Annotations and Specific Data Points:**
- There are no specific annotations or numerical values provided on the graph, but the linearity and origin crossing are significant features that define the ideal behavior of a phase detector.

Figure 16.1 Definition of phase detector.
image_name:Figure 16.2 Exclusive OR gate as phase detector
description:The diagram titled "Figure 16.2 Exclusive OR gate as phase detector" illustrates the operation of an XOR gate used as a phase detector. The graph is a time-domain waveform showing how the XOR gate processes two input signals, \( V_1(t) \) and \( V_2(t) \), and produces an output \( V_{out}(t) \).

1. **Type of Graph and Function:**
- This is a time-domain waveform graph displaying digital signals over time.

2. **Axes Labels and Units:**
- The horizontal axis represents time \( t \), though no specific units or scales are provided.
- The vertical axis depicts the voltage levels of the signals, typically in logic levels (0 or 1 for digital signals).

3. **Overall Behavior and Trends:**
- The input signals \( V_1(t) \) and \( V_2(t) \) are square waves with a visible phase difference, \( \Delta \phi \).
- The output \( V_{out}(t) \) is also a square wave, where the pulse width is proportional to the phase difference between \( V_1(t) \) and \( V_2(t) \).
- As the phase difference \( \Delta \phi \) changes, the width of the output pulses varies, reflecting the XOR gate's function.

4. **Key Features and Technical Details:**
- The XOR gate outputs high (logic 1) when the inputs differ and low (logic 0) when they are the same.
- The phase difference \( \Delta \phi \) is marked between \( V_1(t) \) and \( V_2(t) \), indicating the time shift.
- The output \( V_{out}(t) \) has pulses that align with the times when \( V_1(t) \) and \( V_2(t) \) differ.

5. **Annotations and Specific Data Points:**
- The graph includes a visual marker for the phase difference \( \Delta \phi \), but no specific numerical values are provided.
- The behavior of the XOR gate as a phase detector is highlighted by the variation in pulse width of \( V_{out}(t) \), which is a key characteristic of this configuration.

Figure 16.2 Exclusive OR gate as phase detector.

A familiar example of a phase detector is the exclusive OR (XOR) gate. As shown in Fig. 16.2, as the phase difference between the inputs varies, so does the width of the output pulses, thereby providing a dc level proportional to $\Delta \phi$. While the XOR circuit produces error pulses on both rising and falling edges, other types of PD may respond only to positive or negative transitions.

#### Example 16.1

If the output swing of the XOR in Fig. 16.2 is $V_{0}$ volts, what is the gain of the circuit as a phase detector? Plot the input-output characteristic of the PD.

#### Solution

If the phase difference increases from zero to $\Delta \phi$ radians, the area under each pulse increases by $V_{0} \cdot \Delta \phi$. Since each period contains two pulses, the average value rises by $2\left[V_{0} \cdot \Delta \phi /(2 \pi)\right]$, yielding a gain of $V_{0} / \pi$. Note that the gain is independent of the input frequency.

To construct the input-output characteristic, we examine the circuit's response to various input phase differences. As illustrated in Fig. 16.3, the average output voltage rises to $\left[V_{0} / \pi\right] \times \pi / 2=V_{0} / 2$ for $\Delta \phi=\pi / 2$ and $V_{0}$ for
image_name:Δφ ≈ 0
description:The diagram consists of multiple parts illustrating the relationship between phase difference (Δφ) and output voltage (V_out) in a phase-locked loop (PLL) system. The graph in question, labeled "Δφ ≈ 0," is part of a larger set of diagrams showing different phase differences.

1. **Type of Graph and Function**:
- The lower part of the image is a piecewise linear graph depicting the average output voltage (V_out) as a function of phase difference (Δφ). It is not a typical Bode plot or Nyquist diagram but rather a characteristic curve showing the behavior of a PLL.

2. **Axes Labels and Units**:
- The x-axis is labeled Δφ, representing phase difference in radians, ranging from -2π to 2π.
- The y-axis is labeled V̅_out, representing the average output voltage, with a maximum value of V_0.

3. **Overall Behavior and Trends**:
- The graph shows a triangular waveform, indicating periodic behavior.
- The average output voltage increases linearly from 0 at Δφ = 0 to V_0 at Δφ = π, then decreases linearly back to 0 at Δφ = 2π.
- This pattern repeats symmetrically on the negative side, with V_out reaching -V_0 at Δφ = -π.

4. **Key Features and Technical Details**:
- The graph exhibits symmetry around Δφ = 0.
- Peaks occur at Δφ = ±π with a maximum average output voltage of V_0.
- Zero crossings occur at Δφ = 0, ±2π.
- The periodic nature indicates both positive and negative gains depending on the phase difference.

5. **Annotations and Specific Data Points**:
- The graph is marked with significant points at Δφ = 0, ±π, and ±2π.
- V_out reaches V_0 at Δφ = π and -V_0 at Δφ = -π, indicating maximum gain.

Overall, the graph illustrates the periodic and symmetric nature of the PLL output voltage as a function of phase difference, highlighting key points where the gain is maximized or neutralized.
image_name:Δφ ≈ π/2
description:The graph consists of two main parts: a set of waveform diagrams at the top and a characteristic curve at the bottom.

1. **Type of Graph and Function:**
- The top section displays time-domain waveforms for different phase differences (Δφ) between two input signals, V1 and V2. These are square waveforms plotted against time (t).
- The bottom section is a piecewise linear plot showing the average output voltage (V_out) as a function of the phase difference (Δφ).

2. **Axes Labels and Units:**
- The top waveforms have the horizontal axis labeled as time (t), without specific units, showing the phase difference scenarios: Δφ ≈ 0, Δφ ≈ π/2, Δφ ≈ π, and Δφ ≈ 3π/2.
- The bottom graph has the horizontal axis labeled as Δφ, ranging from -2π to 2π, and the vertical axis as V_out, with a peak at V_0.

3. **Overall Behavior and Trends:**
- **Top Waveforms:**
- For Δφ ≈ 0, the output voltage (V_out) is a series of narrow pulses.
- As Δφ increases to π/2, the pulses widen.
- At Δφ ≈ π, V_out becomes a constant high level, indicating maximum overlap.
- For Δφ ≈ 3π/2, the pulses narrow again.
- **Bottom Characteristic Curve:**
- The curve is triangular, symmetric about Δφ = 0, with peaks at ±π.
- V_out increases linearly from -2π to 0, reaching V_0 at π, and then decreases back to 0 at 2π.

4. **Key Features and Technical Details:**
- The characteristic curve shows periodic behavior with a period of 2π, indicating that the output voltage is periodic with respect to the phase difference.
- The maximum output voltage, V_0, occurs at Δφ = ±π.
- The curve exhibits linear rising and falling edges, reflecting the linear relationship between V_out and Δφ within each period.

5. **Annotations and Specific Data Points:**
- The waveform diagrams are annotated with specific phase differences to illustrate how V_out changes with Δφ.
- The bottom graph has dashed lines marking the key points at Δφ = ±π and the peak voltage V_0.
image_name:Δφ ≈ π
description:The function graph in Figure 16.3 illustrates the relationship between the phase difference (Δφ) and the average output voltage (V_out) of a phase detector. This is a piecewise linear graph that shows how V_out varies as Δφ changes from -2π to 2π.

**Type of Graph and Function:**
The graph is a piecewise linear plot that represents the input-output characteristic of a phase detector circuit. It is used to show the relationship between the phase difference and the output voltage.

**Axes Labels and Units:**
- The horizontal axis represents the phase difference Δφ, measured in radians, ranging from -2π to 2π.
- The vertical axis represents the average output voltage V_out, with a scale from 0 to V_0.

**Overall Behavior and Trends:**
- The graph is periodic and symmetric about the origin, repeating every 2π.
- As Δφ increases from 0 to π, V_out increases linearly from 0 to V_0.
- As Δφ continues from π to 2π, V_out decreases linearly back to 0.
- For negative values of Δφ, the behavior is symmetric, with V_out decreasing from 0 to -V_0 as Δφ goes from 0 to -π, and increasing back to 0 as Δφ goes from -π to -2π.

**Key Features and Technical Details:**
- The graph exhibits peaks at Δφ = π and Δφ = -π, where V_out reaches V_0 and -V_0, respectively.
- It crosses zero at Δφ = 0, ±2π.
- The slopes of the linear segments are equal in magnitude but opposite in direction on either side of the peaks.

**Annotations and Specific Data Points:**
- Key points include (0, 0), (π, V_0), (2π, 0), (-π, -V_0), and (-2π, 0).
- The graph is marked with dashed lines at the peaks to indicate the maximum output voltage V_0.
image_name:Δφ ≈ 3π/2
description:The graph in Figure 16.3 illustrates the relationship between the average output voltage \( V_{out} \) and the phase difference \( \Delta \phi \) for a given system. The graph is a piecewise linear plot that represents the periodic behavior of the output voltage as a function of the phase difference.

Type of Graph and Function:
This is a piecewise linear plot that shows the output voltage \( V_{out} \) as a function of the phase difference \( \Delta \phi \). The plot is periodic and symmetric about the origin.

Axes Labels and Units:
- **Horizontal Axis (x-axis):** Represents the phase difference \( \Delta \phi \) in radians, ranging from \( -2\pi \) to \( 2\pi \).
- **Vertical Axis (y-axis):** Represents the average output voltage \( V_{out} \), with key values marked at \( 0 \), \( V_{0}/2 \), and \( V_{0} \).

Overall Behavior and Trends:
- The graph has a triangular shape, with peaks at \( \Delta \phi = 0 \) and \( \Delta \phi = \pi \), where \( V_{out} = V_{0} \).
- As \( \Delta \phi \) increases from \( 0 \) to \( \pi \), \( V_{out} \) rises linearly from \( 0 \) to \( V_{0} \).
- Beyond \( \Delta \phi = \pi \), \( V_{out} \) decreases linearly back to \( 0 \) at \( \Delta \phi = 2\pi \).
- The pattern repeats symmetrically for negative values of \( \Delta \phi \).

Key Features and Technical Details:
- **Peaks:** At \( \Delta \phi = 0 \) and \( \Delta \phi = \pi \), the average output voltage reaches its maximum value of \( V_{0} \).
- **Zero Crossings:** The output voltage is zero at \( \Delta \phi = -2\pi, 0, 2\pi \).
- **Symmetry:** The plot is symmetric about the origin, indicating that the behavior of the system is periodic with a period of \( 2\pi \).

Annotations and Specific Data Points:
- The graph includes dashed lines marking the zero crossings and peak values.
- The triangular shape indicates a linear rise and fall, highlighting the periodic nature of the circuit's response to the phase difference.

Contextual Explanation:
This plot is part of the input-output characteristic analysis of a system that responds to phase differences. The periodic nature of the graph shows how the average output voltage varies with the input phase difference, exhibiting both positive and negative gains as described in the context provided.
image_name:V_out vs Δφ
description:The graph titled "V_out vs Δφ" is a plot representing the relationship between the average output voltage \( V_{out} \) and the phase difference \( \Delta \phi \). This is a piecewise linear graph that shows periodic behavior.

1. **Type of Graph and Function:**
- This is a linear plot that depicts the variation of average output voltage with respect to the phase difference.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \( \Delta \phi \) and represents the phase difference in radians.
- The vertical axis is labeled \( \overline{V_{out}} \) and represents the average output voltage.
- The graph is linear, with key points marked at \( -2\pi, -\pi, 0, \pi, \) and \( 2\pi \) on the \( \Delta \phi \) axis.

3. **Overall Behavior and Trends:**
- The graph shows a triangular wave pattern, indicating a periodic relationship.
- Starting from \( \Delta \phi = -2\pi \), the average output voltage increases linearly to a peak at \( \Delta \phi = 0 \), reaching \( V_0 \).
- After reaching the peak, it decreases linearly back to zero at \( \Delta \phi = 2\pi \).
- This pattern repeats, showing periodicity with a period of \( 2\pi \).

4. **Key Features and Technical Details:**
- The peak voltage \( V_0 \) occurs at \( \Delta \phi = 0 \).
- The average output voltage is \( V_0/2 \) at \( \Delta \phi = \pm \pi/2 \) and \( \pm 3\pi/2 \).
- The voltage returns to zero at \( \Delta \phi = \pm 2\pi \), indicating the completion of one full period.

5. **Annotations and Specific Data Points:**
- The graph has vertical dashed lines at \( \Delta \phi = -\pi \), \( \Delta \phi = 0 \), and \( \Delta \phi = \pi \), highlighting key phase differences.
- The maximum average output voltage \( V_0 \) is marked with a horizontal dashed line.

Figure 16.3
$\Delta \phi=\pi$. For $\Delta \phi>\pi$, the average begins to drop, falling to $V_{0} / 2$ for $\Delta \phi=3 \pi / 2$ and zero for $\Delta \phi=2 \pi$. The characteristic is therefore periodic, exhibiting both negative and positive gains.

### 16.1.2 Basic PLL Topology

To arrive at the concept of phase locking, let us consider the problem of aligning the output phase of a VCO with the phase of a reference clock. (The reader is encouraged to review the VCO mathematical model in the previous chapter.) As illustrated in Fig. 16.4(a), the rising edges of $V_{\text {out }}$ are "skewed" by $\Delta t$ seconds with respect to $V_{C K}$, and we wish to eliminate this error. Assuming that the VCO has a single control input, $V_{\text {cont }}$, we note that to vary the phase, we must vary the frequency and allow the integration $\phi=\int\left(\omega_{0}+K_{V C O} V_{c o n t}\right) d t$ to take place. For example, suppose that, as shown in Fig. 16.4(b), the VCO frequency is stepped to a higher value at $t=t_{1}$. The circuit then accumulates phase faster, gradually decreasing the phase error. At $t=t_{2}$, the phase error drops to zero and, if $V_{c o n t}$ returns to its original value, $V_{V C O}$ and $V_{C K}$ remain aligned. Interestingly, the alignment can be accomplished by stepping the VCO frequency to a lower value for a certain time interval as well (Problem 16.2). Thus, phase alignment can be achieved only by a (temporary) frequency change.
image_name:(a)
description:The graph labeled as (a) is a time-domain waveform diagram displaying two digital signals, V_CK and V_out, plotted against time (t). Both signals are square waves, indicating digital clock signals. The horizontal axis represents time, but specific units are not indicated, suggesting a general analysis rather than a precise measurement.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph showing digital signals.

2. **Axes Labels and Units:**
- The horizontal axis is labeled 't' for time.
- The vertical axis shows two signals: V_CK and V_out, both represented as square waveforms.
- There are no specific units or scales provided on the axes.

3. **Overall Behavior and Trends:**
- V_CK and V_out are both periodic square waves.
- There is a noticeable skew or phase difference between the two waveforms, marked as Δt.
- V_out lags behind V_CK by a time delay Δt.

4. **Key Features and Technical Details:**
- Δt represents the phase skew or delay between the two signals.
- The waveforms are consistent in frequency and amplitude, suggesting a stable clock signal.

5. **Annotations and Specific Data Points:**
- The phase skew Δt is specifically annotated, highlighting the time difference between corresponding edges of V_CK and V_out.

This diagram illustrates the concept of phase skew between two clock signals, which is a key consideration in timing analysis and synchronization tasks in digital circuits.
image_name:(b)
description:The graph in figure 16.4 (b) illustrates the behavior of two waveforms, \( V_{CK} \) and \( V_{out} \), in relation to a control voltage \( V_{cont} \) over time. This is a time-domain waveform graph.

**Axes Labels and Units:**
- The horizontal axis represents time \( t \), with no specific units provided, indicating a continuous progression of time.
- The vertical axis represents voltage levels for three signals: \( V_{CK} \), \( V_{out} \), and \( V_{cont} \).

**Overall Behavior and Trends:**
- Initially, \( V_{CK} \) and \( V_{out} \) are out of phase, as shown by the misalignment of their rising and falling edges.
- At time \( t_1 \), a step change in \( V_{cont} \) occurs, temporarily increasing the frequency of \( V_{out} \).
- This frequency increase causes \( V_{out} \) to accumulate phase faster, gradually aligning with \( V_{CK} \).
- By time \( t_2 \), \( V_{out} \) is in phase with \( V_{CK} \), and \( V_{cont} \) returns to its original level, maintaining this alignment.

**Key Features and Technical Details:**
- The step in \( V_{cont} \) between \( t_1 \) and \( t_2 \) is crucial for achieving phase alignment.
- The change in \( V_{cont} \) results in a temporary frequency shift, allowing \( V_{out} \) to catch up with \( V_{CK} \).
- The graph demonstrates that phase alignment can be achieved through a controlled, temporary frequency change.

**Annotations and Specific Data Points:**
- \( t_1 \) and \( t_2 \) are marked as significant time points where the frequency adjustment begins and ends.
- The alignment of \( V_{CK} \) and \( V_{out} \) by \( t_2 \) indicates successful phase locking.

This graph effectively demonstrates the concept of phase alignment using a phase-locked loop (PLL) mechanism by showing how a temporary change in control voltage can synchronize two initially misaligned waveforms.

Figure 16.4 (a) Two waveforms with a skew; (b) change of VCO frequency to eliminate the skew.
The foregoing experiment suggests that the output phase of a VCO can be aligned with the phase of a reference if (1) the frequency of the VCO is changed momentarily, and (2) a means of comparing the two phases, i.e., a phase detector, is used to determine when the VCO and the reference signals are aligned. The task of aligning the output phase of the VCO with the phase of the reference is called "phase locking."

From the above observations, we surmise that a PLL simply consists of a PD and a VCO in a feedback loop [Fig. 16.5(a)]. The PD compares the phases of $V_{\text {out }}$ and $V_{\text {in }}$, generating an error that varies the VCO frequency until the phases are aligned, i.e., the loop is locked. This topology, however, must be modified
image_name:(a)
description:The system block diagram labeled "(a)" represents a basic phase-locked loop (PLL) configuration. It consists of two main components: a Phase Detector (PD) and a Voltage-Controlled Oscillator (VCO), arranged in a feedback loop.

1. **Main Components:**
- **Phase Detector (PD):** This block receives two input signals: the reference signal \( V_{in} \) and the feedback signal \( V_{out} \). The PD compares the phases of these two signals and generates an output voltage \( V_{PD} \) that is proportional to the phase difference.
- **Voltage-Controlled Oscillator (VCO):** The VCO receives the output from the PD, \( V_{PD} \), and adjusts its frequency accordingly. The output of the VCO is \( V_{out} \), which is fed back to the PD for continuous phase comparison.

2. **Flow of Information or Control:**
- The input reference signal \( V_{in} \) and the feedback signal \( V_{out} \) are fed into the PD.
- The PD outputs a control voltage \( V_{PD} \), which is sent to the VCO.
- The VCO adjusts its output frequency based on \( V_{PD} \) and generates the output signal \( V_{out} \).
- \( V_{out} \) is then fed back into the PD, creating a feedback loop that continuously aligns the phase of \( V_{out} \) with \( V_{in} \).

3. **Labels, Annotations, and Key Indicators:**
- \( V_{in} \) and \( V_{out} \) are labeled as input and output signals, respectively.
- \( V_{PD} \) is the control voltage output from the PD to the VCO.

4. **Overall System Function:**
- The primary function of this system is to achieve phase locking, where the phase of the output signal \( V_{out} \) is aligned with the phase of the input reference signal \( V_{in} \). This is accomplished by the feedback loop that continuously adjusts the VCO's frequency based on the phase difference detected by the PD. This basic PLL configuration is fundamental in applications where precise phase alignment is required, such as in communication systems and signal processing.
image_name:(b)
description:The system block diagram labeled as "(b)" represents a simple Phase-Locked Loop (PLL) with a low-pass filter (LPF) included in the feedback loop to achieve phase locking between an input signal and an output signal.

1. **Main Components:**
- **Phase Detector (PD):** This block compares the phase of the input signal \(V_{in}\) with the phase of the output signal \(V_{out}\). It generates an output voltage \(V_{PD}\) that represents the phase difference between these two signals.
- **Low-Pass Filter (LPF):** The output \(V_{PD}\) from the phase detector contains both a DC component and high-frequency noise. The LPF filters out the high-frequency components, allowing only the DC component, \(V_{cont}\), to pass through. This filtered signal is crucial for adjusting the VCO.
- **Voltage-Controlled Oscillator (VCO):** The VCO receives the control voltage \(V_{cont}\) from the LPF and adjusts its output frequency accordingly. The output of the VCO is \(V_{out}\), which is fed back to the PD for continuous phase comparison.

2. **Flow of Information or Control:**
- The input signal \(V_{in}\) is fed into the PD, which also receives the feedback signal \(V_{out}\) from the VCO.
- The PD outputs \(V_{PD}\), which is then passed through the LPF to remove high-frequency noise, resulting in the control voltage \(V_{cont}\).
- \(V_{cont}\) is used to control the VCO, adjusting its output frequency \(V_{out}\) to match the phase of \(V_{in}\).
- \(V_{out}\) is fed back to the PD, completing the feedback loop.

3. **Labels, Annotations, and Key Indicators:**
- The input phase is labeled as \(\phi_{in}\) and the output phase as \(\phi_{out}\), indicating their roles in phase comparison and locking.
- The control voltage is labeled as \(V_{cont}\), emphasizing its role in controlling the VCO.

4. **Overall System Function:**
- The primary function of this PLL is to synchronize the phase of the VCO output with the phase of the input signal. The PD detects phase differences and generates an error signal \(V_{PD}\), which is filtered by the LPF to produce a stable control voltage \(V_{cont}\). This voltage adjusts the VCO's frequency to align \(\phi_{out}\) with \(\phi_{in}\), achieving phase lock. The inclusion of the LPF ensures that the control voltage remains stable and free from high-frequency noise, which is critical for the steady-state operation of the VCO.

Figure 16.5 (a) Feedback loop comparing input and output phases; (b) simple PLL.
because (1) as exemplified by the waveforms of Fig. 16.2, the PD output, $V_{P D}$, consists of a dc component (desirable) and high-frequency components (undesirable), and (2) as mentioned in Chapter 15, the control voltage of the oscillator must remain quiet in the steady state, i.e., the PD output must be filtered. We therefore interpose a low-pass filter (LPF) between the PD and the VCO [Fig. 16.5(b)], suppressing the high-frequency components of the PD output and presenting the dc level to the oscillator. This forms the basic PLL topology. For now, we assume that the LPF has a gain of unity at low frequencies (e.g., as in a first-order RC section).

It is important to bear in mind that the feedback loop of Fig. 16.5(b) compares the phases of the input and output. Unlike the feedback topologies studied in the previous chapters, PLLs typically require no knowledge of voltages or currents in their feedback operation. If the loop gain is large enough, the difference between the input phase, $\phi_{i n}$, and the output phase, $\phi_{\text {out }}$, falls to a small value in the steady state, providing phase alignment.

For subsequent analyses of PLLs, we must define the phase-lock condition carefully. If the loop of Fig. 16.5(b) is locked, we postulate that $\phi_{\text {out }}-\phi_{\text {in }}$ is constant and preferably small. We therefore define the loop to be locked if $\phi_{\text {out }}-\phi_{\text {in }}$ does not change with time. An important corollary of this definition is that

$$
\begin{equation*}
\frac{d \phi_{\text {out }}}{d t}-\frac{d \phi_{\text {in }}}{d t}=0 \tag{16.1}
\end{equation*}
$$

and hence

$$
\begin{equation*}
\omega_{\text {out }}=\omega_{\text {in }} \tag{16.2}
\end{equation*}
$$

This is a unique property of PLLs and will be revisited more closely later.
In summary, when locked, a PLL produces an output that has a small phase error with respect to the input but exactly the same frequency. The reader may then wonder why a PLL is used at all. A short piece of wire would seem to perform the task even better! We answer this question in Sec. 16.5.

#### Example 16.2

Implement a simple PLL in CMOS technology.

#### Solution

Figure 16.6 illustrates an implementation utilizing an XOR gate as the phase detector. The VCO is configured as a negative- $G_{m}$ LC oscillator whose frequency is tuned by varactor diodes.
image_name:Figure 16.6
description:The circuit is a simple PLL implemented in CMOS technology. It uses an XOR gate as a phase detector and a negative-Gm LC oscillator with varactor diodes for frequency tuning. The PLL is designed to lock the output frequency to the input frequency with a small phase difference.

### Waveforms in a Locked PLL

PLL Waveforms in Locked Condition In order to familiarize ourselves with the behavior of PLLs, we begin with the simplest case: the circuit is locked and we wish to examine the waveforms at each point around the loop. As illustrated in Fig. 16.7(a), $V_{\text {in }}$ and $V_{\text {out }}$ exhibit a small phase difference but equal frequencies. The PD therefore generates pulses as wide as the skew between the input and the output, ${ }^{1}$ and the low-pass filter extracts the dc component of $V_{P D}$, applying the result to the VCO. We assume that the LPF has a gain of unity at low frequencies. The small pulses in $V_{L P F}$ are called "ripple."
image_name:Fig. 16.7(a)
description:The graph in Fig. 16.7(a) illustrates waveforms within a Phase-Locked Loop (PLL) system when it is in a locked condition. The graph is a time-domain waveform display, showing the behavior of various signals over time.

1. **Axes Labels and Units:**
- The horizontal axis represents time, denoted as 't'. The unit of time is not specified, but it is typically in seconds or milliseconds for such waveforms.
- The vertical axis represents voltage levels for different signals, though specific voltage units are not labeled (typically in volts).

2. **Overall Behavior and Trends:**
- The top two waveforms, $V_{\text{in}}$ and $V_{\text{out}}$, are square waves with equal frequencies but a small phase difference, indicated by $\phi_0$. This phase difference is visually marked between the rising edges of $V_{\text{in}}$ and $V_{\text{out}}$.
- The third waveform, $V_{PD}$, is a pulse waveform. The width of each pulse corresponds to the phase difference between $V_{\text{in}}$ and $V_{\text{out}}$.
- The bottom waveform, $V_{\text{cont}}$, is a smoother waveform compared to the others, showing a low-frequency ripple superimposed on a DC level. This ripple is the result of the low-pass filtering of $V_{PD}$.

3. **Key Features and Technical Details:**
- The phase difference $\phi_0$ is crucial as it determines the width of the pulses in $V_{PD}$.
- The ripple in $V_{\text{cont}}$ is highlighted, indicating small variations around a central DC level. This ripple is characteristic of the low-pass filter output in a PLL.

4. **Annotations and Specific Data Points:**
- An annotation indicates the phase difference $\phi_0$ between $V_{\text{in}}$ and $V_{\text{out}}$.
- The ripple in $V_{\text{cont}}$ is specifically labeled, emphasizing its presence and significance.

This waveform analysis provides insight into the dynamics of the PLL system, particularly how phase differences and filtering affect the control voltage and system behavior.

image_name:(b)
description:The diagram labeled (b) consists of two linear graphs, each depicting a relationship pertinent to the operation of a Phase-Locked Loop (PLL).

1. **Upper Graph:**
- **Type of Graph:** Linear plot showing the relationship between output frequency and control voltage in a Voltage-Controlled Oscillator (VCO).
- **Axes Labels and Units:**
- The vertical axis is labeled as \( \omega_{\text{out}} \), representing the output frequency.
- The horizontal axis is labeled as \( V_{\text{cont}} \), representing the control voltage.
- **Overall Behavior and Trends:**
- The graph shows a linear increase in output frequency \( \omega_{\text{out}} \) as the control voltage \( V_{\text{cont}} \) increases.
- **Key Features and Technical Details:**
- The graph starts at a frequency \( \omega_0 \) and increases to \( \omega_1 \) as \( V_{\text{cont}} \) reaches \( V_1 \).
- A dashed line indicates the specific point \( V_1 \) where the frequency is \( \omega_1 \).

2. **Lower Graph:**
- **Type of Graph:** Linear plot showing the relationship between phase error and output voltage in a Phase Detector (PD).
- **Axes Labels and Units:**
- The vertical axis is labeled as \( \overline{V}_{\text{out}} \), representing the average output voltage.
- The horizontal axis is labeled with phase difference symbols \( \phi_0 \) and \( \Delta \phi \), indicating the phase error.
- **Overall Behavior and Trends:**
- The graph shows a linear increase in average output voltage \( \overline{V}_{\text{out}} \) with increasing phase error.
- **Key Features and Technical Details:**
- The graph intersects the vertical axis at \( V_1 \), indicating the specific output voltage when the phase difference is \( \phi_0 \).
- A dashed line highlights the phase difference \( \phi_0 \) and the corresponding output voltage \( V_1 \).

These graphs collectively illustrate the dependencies of both frequency and voltage on control parameters within a PLL system, highlighting the linear characteristics of the VCO and PD components.

Figure 16.7 (a) Waveforms in a PLL in locked condition; (b) calculation of phase error.
In the waveforms of Fig. 16.7(a), two quantities are unknown: $\phi_{0}$ and the dc level of $V_{\text {cont }}$. To determine these values, we construct the VCO and PD characteristics [Fig. 16.7(b)]. If the input and output frequencies are equal to $\omega_{1}$, then the required oscillator control voltage is unique and equal to $V_{1}$. This voltage must be produced by the phase detector, demanding a phase error determined by the PD characteristic. More specifically, since $\omega_{\text {out }}=\omega_{0}+K_{V C O} V_{\text {cont }}$ and $\overline{V_{P D}}=K_{P D} \Delta \phi$, we can write

$$
\begin{equation*}
V_{1}=\frac{\omega_{1}-\omega_{0}}{K_{V C O}} \tag{16.3}
\end{equation*}
$$

and

$$
\begin{align*}
\phi_{0} & =\frac{V_{1}}{K_{P D}}  \tag{16.4}\\
& =\frac{\omega_{1}-\omega_{0}}{K_{P D} K_{V C O}} \tag{16.5}
\end{align*}
$$

Equation (16.5) reveals two important points: (1) as the input frequency of the PLL varies, so does the phase error; and (2) to minimize the phase error, $K_{P D} K_{V C O}$ must be maximized.

#### Example 16.3

A PLL incorporates a VCO and a PD having the characteristics shown in Fig. 16.8. Explain what happens as the input frequency varies in the locked condition.

image_name:Figure 16.8
description:The graph in Figure 16.8 consists of two separate plots that illustrate the characteristics of a Phase-Locked Loop (PLL) system, specifically focusing on the Voltage-Controlled Oscillator (VCO) and Phase Detector (PD).

Left Plot: VCO Characteristic
- **Type of Graph:** Linear plot.
- **Axes Labels and Units:**
- The horizontal axis is labeled as $V_{cont}$, representing the control voltage.
- The vertical axis is labeled as $\omega_{out}$, representing the output frequency.
- **Overall Behavior and Trends:**
- The plot shows a linear relationship between the control voltage $V_{cont}$ and the output frequency $\omega_{out}$.
- The line starts at $\omega_{0}$ when $V_{cont}$ is zero and increases linearly with $V_{cont}$.
- **Key Features and Technical Details:**
- The line reaches $\omega_{x}$ at the control voltage $V_{0}$, indicating the maximum output frequency achievable with this setup.
- This behavior suggests that increasing the control voltage results in a proportional increase in the output frequency, up to a certain limit.

Right Plot: PD Characteristic
- **Type of Graph:** Sine wave characteristic.
- **Axes Labels and Units:**
- The horizontal axis is labeled as $\Delta \phi$, representing the phase difference.
- The vertical axis is labeled as $\overline{V_{out}}$, representing the average output voltage.
- **Overall Behavior and Trends:**
- The plot depicts a sinusoidal relationship between the phase difference $\Delta \phi$ and the average output voltage $\overline{V_{out}}$.
- The sine wave crosses the horizontal axis at the origin and has peaks at $\pm \pi/2$.
- **Key Features and Technical Details:**
- The maximum and minimum average output voltages are $\pm V_{0}$, occurring at phase differences of $\pm \pi/2$.
- This indicates that the PD has a linear response near the origin but saturates at $\pm \pi/2$, where the average output reaches its extreme values.

Annotations and Specific Data Points:
- The linear plot on the left marks the specific points $\omega_{0}$ and $\omega_{x}$, with the corresponding control voltages $0$ and $V_{0}$, respectively.
- The sinusoidal plot on the right highlights the critical phase differences $\pm \pi/2$ where the output voltage reaches $\pm V_{0}$.

#### Solution

The PD characteristic is relatively linear near the origin but exhibits a small-signal gain of zero if the phase difference equals $\pm \pi / 2$, at which point the average output is equal to $\pm V_{0}$. Now suppose the input frequency increases from $\omega_{0}$, requiring a greater control voltage. If the frequency is high enough $\left(=\omega_{x}\right)$ to dictate $V_{c o n t}=V_{0}$, then the PD must operate at the peak of its characteristic. However, the PD gain drops to zero here and the feedback loop fails. Thus, the circuit cannot lock if the input frequency reaches $\omega_{X}$.

With the basic understanding of PLLs developed thus far, we now return to Eq. (16.2). The exact equality of the input and output frequencies of a PLL in the locked condition is a critical attribute. The significance of this property can be seen from two observations. First, in many applications, even a very small (deterministic) frequency error may prove unacceptable. For example, if a data stream is to be processed synchronously by a clocked system, even a slight difference between the data rate and the clock frequency results in a "drift," creating errors (Fig. 16.9). Second, the equality would not exist if the PLL compared the input and output frequencies rather than phases. As illustrated in Fig. 16.10(a), a loop employing a frequency detector (FD) would suffer from a finite difference between $\omega_{\text {in }}$ and $\omega_{\text {out }}$ due to various mismatches and other nonidealities. This can be understood by an analogy with the unity-gain feedback circuit of Fig. 16.10(b). Even if the op amp's open-loop gain is infinity, the input-referred offset voltage leads to a finite error between $V_{i n}$ and $V_{\text {out }}$.
Small Transients in Locked Condition Let us now analyze the response of a PLL in the locked condition to small phase or frequency transients at the input.
image_name:Figure 16.9 Drift of data with respect to clock in the presence of small frequency error.
description:The graph in Figure 16.9 illustrates the drift of data with respect to a clock signal in the presence of a small frequency error. This is a time-domain waveform graph with two signals plotted against time on the horizontal axis, which is typically measured in arbitrary time units (e.g., seconds, milliseconds). The vertical axis represents the logical levels of the signals, commonly denoted as high and low states. The two signals shown are labeled as 'Data' and 'Clock'.

- **Data Signal**: This waveform is a square wave with a periodic pattern, representing a digital data signal. It alternates between high and low states. The transitions between these states are vertical, indicating instantaneous changes, which is characteristic of digital signals.

- **Clock Signal**: Below the data signal is the clock waveform, which is also a square wave with a similar periodicity. However, due to a small frequency error, there is a noticeable drift between the data and clock signals. The clock signal is meant to synchronize with the data signal, but the misalignment due to frequency error is evident.

- **Drift Observation**: The graph shows that over time, the rising and falling edges of the data signal gradually shift relative to the clock signal. This drift is highlighted by dotted vertical lines that emphasize the misalignment at specific points in the waveform. Initially, the data and clock transitions are aligned, but as time progresses, the data signal transitions occur slightly later than the corresponding clock transitions.

- **Key Features**: The graph highlights the critical issue of timing misalignment due to frequency mismatches in systems that rely on precise synchronization, such as phase-locked loops (PLLs) in communication systems. This drift can lead to errors in data interpretation if not corrected.

This graph effectively demonstrates the concept of timing drift and serves as a visual representation of the challenges posed by frequency errors in synchronized digital systems.

Figure 16.9 Drift of data with respect to clock in the presence of small frequency error.
image_name:(a)
description:The system block diagram labeled "(a)" represents a Frequency-Locked Loop (FLL), which is commonly used in communication systems to maintain synchronization between an input and output frequency. This configuration consists of three main components:

1. **Frequency Detector (FD):** This block receives the input signal \( V_{in} \) and compares its frequency with the feedback signal. The output of the FD is a signal that represents the frequency difference between the input and the feedback loop.

2. **Low Pass Filter (LPF):** The output from the FD is fed into the LPF. The LPF smooths out the frequency difference signal by filtering out high-frequency noise, providing a stable control signal to the next stage. This helps in maintaining a steady state in the loop by removing rapid fluctuations.

3. **Voltage-Controlled Oscillator (VCO):** The filtered signal from the LPF is used to control the VCO. The VCO adjusts its output frequency based on the control signal, aligning it closely with the input frequency. The output \( V_{out} \) is then fed back into the FD to complete the loop.

**Flow of Information:**
- The input signal \( V_{in} \) enters the FD, where it is compared with the feedback signal.
- The FD outputs a frequency error signal to the LPF.
- The LPF processes this signal, filtering out noise, and sends a stable control signal to the VCO.
- The VCO adjusts its frequency output based on the control signal, producing \( V_{out} \).
- \( V_{out} \) is fed back into the FD, forming a closed-loop system.

**Overall System Function:**
The primary function of this system is to lock the output frequency \( V_{out} \) to the input frequency \( V_{in} \) by continuously adjusting the VCO based on the feedback from the FD and the control signal from the LPF. This ensures that any frequency drift is corrected, maintaining synchronization between input and output frequencies.
image_name:(b)
description:
[
name: OpAmp, type: OpAmp, ports: {InP: Vin, InN: Vout, OutP: Vout}
]
extrainfo:The circuit diagram (b) represents a unity-gain feedback amplifier, where the output is directly connected to the inverting input, creating a buffer configuration.

Figure 16.10 (a) Frequency-locked loop; (b) unity-gain feedback amplifier.

Consider a PLL in the locked condition and assume that the input and output waveforms can be expressed as

$$
\begin{align*}
V_{\text {in }}(t) & =V_{A} \cos \omega_{1} t  \tag{16.6}\\
V_{\text {out }}(t) & =V_{B} \cos \left(\omega_{1} t+\phi_{0}\right) \tag{16.7}
\end{align*}
$$

where higher harmonics are neglected and $\phi_{0}$ is the static phase error. Suppose, as shown in Fig. 16.11, the input experiences a phase step of $\phi_{1}$ at $t=t_{1}$, i.e., $\phi_{i n}=\omega_{1} t+\phi_{1} u\left(t-t_{1}\right) .^{2}$ The phase step manifests itself as a rising edge in $V_{i n}$ that occurs earlier (or later) than the periodicity would dictate. Alternatively, we can say that the phase step results in a shorter (or longer) period just before $t_{1}$. Since the output of the LPF does not change instantaneously, the VCO initially continues to oscillate at $\omega_{1}$. The growing phase difference between the input and the output then creates wide pulses at the output of the PD, forcing $V_{L P F}$ to rise gradually. As a result, the VCO frequency begins to change, attempting to minimize the phase error. Note that the loop is not locked during the transient because the phase error varies with time.
image_name:Figure 16.11 Response of a PLL to a phase step
description:The graph depicts the response of a Phase-Locked Loop (PLL) to a phase step, as illustrated in Figure 16.11. This is a time-domain waveform graph, which shows the behavior of various signals within the PLL system over time.

1. **Type of Graph and Function:**
- The graph consists of multiple time-domain waveforms, representing different signals in the PLL circuit.

2. **Axes Labels and Units:**
- The horizontal axis represents time, denoted as 't'.
- The vertical axes represent different signals: \(V_{in}\), \(V_{out}\), \(V_{PD}\), \(V_{LPF}\), and \(\omega_{out}\).
- The units for these signals are not explicitly labeled, but they are typically in volts for voltage signals and radians per second for frequency.

3. **Overall Behavior and Trends:**
- **\(V_{in}\) and \(V_{out}\):** These signals are square waves with the same frequency \(\omega_1\). At time \(t_1\), a phase step \(\phi_1\) is introduced to \(V_{in}\), causing a phase difference between \(\phi_{in}\) and \(\phi_{out}\).
- **\(V_{PD}\):** The phase detector output shows wide pulses starting at \(t_1\), indicating the phase difference.
- **\(V_{LPF}\):** The low-pass filter output rises gradually after \(t_1\) due to the integration of the phase detector output, creating a smooth curve that peaks and then decays back towards its original value.
- **\(\omega_{out}\):** The VCO frequency initially remains at \(\omega_1\) but begins to change after \(t_1\), attempting to correct the phase error. The frequency curve shows a smooth rise and fall, reflecting the transient response of the PLL.

4. **Key Features and Technical Details:**
- The phase step \(\phi_1\) at \(t_1\) is a critical event, initiating the transient response.
- The gray areas under the \(V_{LPF}\) and \(\omega_{out}\) curves indicate the transient response of the PLL system as it attempts to lock back to the input frequency.

5. **Annotations and Specific Data Points:**
- The time \(t_1\) is marked with a vertical dashed line, indicating the moment the phase step occurs.
- The phase shift \(\phi_1\) is annotated between the \(\phi_{in}\) and \(\phi_{out}\) lines, highlighting the initial phase difference introduced to the system.

Figure 16.11 Response of a PLL to a phase step.

What happens after the VCO frequency begins to change? If the loop is to return to lock, $\omega_{\text {out }}$ must eventually go back to $\omega_{1}$, requiring that $V_{L P F}$ and hence $\phi_{\text {out }}-\phi_{i n}$ also return to their original values. Since $\phi_{\text {in }}$ has changed by $\phi_{1}$, the variation in the VCO frequency is such that the area under $\omega_{\text {out }}$ provides an additional phase of $\phi_{1}$ in $\phi_{\text {out }}$ :

$$
\begin{equation*}
\int_{t 1}^{\infty} \omega_{\text {out }} d t=\phi_{1} \tag{16.8}
\end{equation*}
$$

[^116]Thus, when the loop settles, the output becomes equal to

$$
\begin{equation*}
V_{\text {out }}(t)=V_{B} \cos \left[\omega_{1} t+\phi_{0}+\phi_{1} u\left(t-t_{1}\right)\right] \tag{16.9}
\end{equation*}
$$

Consequently, as shown in Fig. 16.11, $\phi_{\text {out }}$ gradually "catches up" with $\phi_{i n}$.
It is important to make two observations. (1) After the loop returns to lock, all of the parameters (except for the total input and output phases) assume their original values. That is, $\phi_{\text {in }}-\phi_{\text {out }}, V_{L P F}$, and the VCO frequency remain unchanged-an expected result because these three parameters bear a one-to-one relationship and the input frequency has stayed the same. (2) The control voltage of the oscillator can serve as a suitable test point in the analysis of PLLs. While it is difficult to measure the time variations of phase and frequency in Fig. 16.11, $V_{\text {cont }}\left(=V_{L P F}\right)$ can be readily monitored in simulations and measurements.

The reader may wonder whether an input phase step always gives rise to the response shown in Fig. 16.11. For example, is it possible for $V_{L P F}$ to ring before settling to its final value? Such behavior is indeed possible and will be quantified in Sec. 16.1.3.

Let us now examine the response of PLLs to a small input frequency step $\Delta \omega$ at $t=t_{1}$ (Fig. 16.12). As with the case of a phase step, the VCO continues to oscillate at $\omega_{1}$ immediately after $t_{1}$. Thus, the PD generates increasingly wider pulses, and $V_{L P F}$ rises with time. As $\omega_{\text {out }}$ approaches $\omega_{1}+\Delta \omega$, the width of the pulses generated by the PD decreases, eventually settling to a value that produces a dc component equal to $\left(\omega_{1}+\Delta \omega-\omega_{0}\right) / K_{V C O}$. In contrast to the case of a phase step, the response of a PLL to a frequency step entails a permanent change in both the control voltage and the phase error. If the input frequency is varied slowly, $\omega_{\text {out }}$ simply "tracks" $\omega_{\text {in }}$.
image_name:Figure 16.12
description:The graph in Figure 16.12 illustrates the response of a Phase-Locked Loop (PLL) to a small frequency step. It is a time-domain waveform showing several related signals over time.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform depicting the behavior of a PLL system when subjected to a small frequency step.

2. **Axes Labels and Units:**
- The x-axis represents time (t).
- The y-axis is not explicitly labeled with units, but it shows various signals associated with the PLL: input voltage (V_in), output voltage (V_out), phase detector output (V_PD), low-pass filter output (V_LPF), and output frequency (ω_out).

3. **Overall Behavior and Trends:**
- **V_in and V_out:** Both signals are square waves. Initially, both have the same frequency ω1. After time t1, V_in changes to a new frequency ω2 = ω1 + Δω, while V_out continues to follow ω1 initially and then adjusts to track the new input frequency.
- **Phase (φ_in and φ_out):** The phase of the input (φ_in) and output (φ_out) is shown with a slight divergence after t1, indicating a phase error that the PLL will correct over time.
- **V_PD:** The phase detector output initially shows pulses corresponding to the phase difference, which decrease over time as the PLL locks to the new frequency.
- **V_LPF:** The low-pass filter output shows a gradual increase, indicating the PLL's control voltage adjusting to the new frequency.
- **ω_out:** The output frequency starts at ω1 and gradually increases to match ω2, demonstrating the PLL's tracking capability.

4. **Key Features and Technical Details:**
- The graph shows a critical transition at time t1, where the input frequency changes.
- The PLL's response is characterized by an initial phase error and a gradual correction as the control voltage (V_LPF) increases.
- The system settles into a new steady state where the output frequency ω_out matches the input frequency ω2.

5. **Annotations and Specific Data Points:**
- The vertical dashed line at t1 marks the point of frequency step change from ω1 to ω2.
- The labels ω1 and ω2 on V_in and V_out indicate the respective frequencies before and after the step.
- The graph visually demonstrates the PLL's ability to lock onto a new frequency while minimizing phase error over time.

Figure 16.12 Response of a PLL to a small frequency step.
The exact settling behavior of PLLs depends on the various loop parameters and will be studied in Sec. 16.1.3. But, to arrive at an important observation, we consider the phase step response depicted in Fig. 16.13, where $V_{\text {cont }}$ rings before settling to its final value. Consider the state of the loop at $t=t_{2}$. At this point, the output frequency is equal to its final value (because $V_{\text {cont }}$ is equal to its final value), but the loop continues the transient because the phase error deviates from the required value. Similarly, at $t=t_{3}$, the phase error is equal to its final value, but the output frequency is not. In other words, for the loop to settle, both the phase and the frequency must settle to their proper values.
image_name:Figure 16.13 Example of phase step response
description:The graph in Figure 16.13 illustrates the phase step response of a system, specifically focusing on a phase-locked loop (PLL). The graph consists of three key parts:

1. **Type of Graph and Function:**
- The graph is a time-domain waveform showing the response of a PLL to a phase step.

2. **Axes Labels and Units:**
- The horizontal axis represents time (t), but no specific units are provided.
- The vertical axis has three separate plots labeled as $V_{in}$, $V_{out}$, and $V_{cont}$, indicating input voltage, output voltage, and control voltage, respectively. Again, no specific units are given for voltage.

3. **Overall Behavior and Trends:**
- **$V_{in}$ and $V_{out}$:** Both these signals are square waves. Initially, $V_{in}$ and $V_{out}$ are synchronized, indicating a locked state.
- **$V_{cont}$:** This waveform shows a transient response. Initially, it is steady, then it rises to a peak after $t_1$, decreases to a minimum before $t_2$, and finally oscillates with decreasing amplitude until it stabilizes. This behavior indicates the system's attempt to lock back to the input phase after a disturbance.

4. **Key Features and Technical Details:**
- At $t_1$, a disturbance causes $V_{cont}$ to rise, indicating a phase error.
- By $t_2$, $V_{cont}$ crosses a reference line (dashed), which might represent the desired steady state.
- The oscillations in $V_{cont}$ decrease over time, showing a damping effect as the system stabilizes.

5. **Annotations and Specific Data Points:**
- The graph includes vertical dashed lines at $t_1$, $t_2$, and $t_3$, marking significant time points in the response.
- The steady-state value of $V_{cont}$ is indicated by a horizontal dashed line.

This graph effectively demonstrates how the PLL responds to phase disturbances, with $V_{cont}$ adjusting to correct the phase error and eventually stabilizing to maintain synchronization between $V_{in}$ and $V_{out}$. The decreasing oscillations in $V_{cont}$ reflect the system's damping characteristics as it returns to a stable state.

Figure 16.13 Example of phase step response.

#### Example 16.4

In the PLL shown in Fig. 16.14, an external voltage $V_{e x}$ is added to the output of the low-pass filter. ${ }^{3}$ (a) Determine the phase error and $V_{L P F}$ if the loop is locked and $V_{e x}=V_{1}$. (b) Suppose $V_{e x}$ steps from $V_{1}$ to $V_{2}$ at $t=t_{1}$. How does the loop respond?
image_name:Figure 16.14
description:The block diagram labeled as Figure 16.14 illustrates a Phase-Locked Loop (PLL) system. It consists of several key components arranged in a feedback loop configuration:

1. **Phase Detector (PD):** The system begins with a phase detector that receives an input signal $V_{in}$. The phase detector compares the phase of the input signal with the phase of the feedback signal (from the output) and generates a phase difference voltage $V_{PD}$.

2. **Low-Pass Filter (LPF):** The output from the phase detector, $V_{PD}$, is fed into a low-pass filter. The LPF smooths the phase difference signal by filtering out high-frequency components, resulting in a control voltage $V_{LPF}$.

3. **Summing Junction:** An external voltage $V_{ex}$ is added to the filtered signal $V_{LPF}$ at a summing junction. This results in a combined control voltage $V_{cont} = V_{LPF} + V_{ex}$.

4. **Voltage-Controlled Oscillator (VCO):** The control voltage $V_{cont}$ is used to adjust the frequency of a voltage-controlled oscillator. The VCO generates an output signal $V_{out}$ whose frequency is proportional to the control voltage.

5. **Feedback Loop:** The output signal $V_{out}$ is fed back into the phase detector, completing the feedback loop. This feedback is crucial for maintaining phase lock by continuously adjusting the VCO frequency to match the input signal phase.

**Flow of Information:**
- The input signal $V_{in}$ is compared with the feedback signal in the phase detector.
- The phase error is filtered and adjusted by the external voltage at the summing junction.
- The VCO adjusts its frequency based on the control voltage, and the output is fed back to the phase detector.

**Labels and Annotations:**
- The diagram includes waveforms for $V_{in}$, $V_{ex}$, $V_{out}$, the frequency $
\omega_{out}$, and $V_{LPF}$ over time.
- At time $t_1$, $V_{ex}$ steps from $V_1$ to $V_2$, affecting the control voltage and subsequently the output frequency and phase.

**Overall System Function:**
The PLL system is designed to synchronize the frequency and phase of the output signal $V_{out}$ with the input signal $V_{in}$. The addition of the external voltage $V_{ex}$ allows for adjustment of the control voltage, influencing how the loop responds to changes and maintains lock, particularly when $V_{ex}$ changes from $V_1$ to $V_2$. The system's stability and damping characteristics are reflected in the gradual changes observed in the frequency and phase of the output signal.
image_name:Example of phase step response
description:The graph in Figure 16.14 illustrates the phase step response of a Phase-Locked Loop (PLL) system. It is a time-domain waveform showing the behavior of various signals in the PLL circuit when an external voltage $V_{ex}$ is stepped from $V_1$ to $V_2$ at time $t_1$.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph depicting the response of a PLL system to a step change in external voltage.

2. **Axes Labels and Units:**
- The x-axis represents time ($t$), though no specific units are given, it is typically in seconds or milliseconds.
- The y-axis shows various voltages and frequencies but is not explicitly labeled with units.

3. **Overall Behavior and Trends:**
- The graph shows a step change in $V_{ex}$ from $V_1$ to $V_2$ at time $t_1$.
- The input voltage $V_{in}$ and output voltage $V_{out}$ are depicted as square waveforms.
- The frequency of the output $
\omega_{out}$ and the low-pass filter voltage $V_{LPF}$ both show a gradual increase after $t_1$, indicating the system's response to the change in $V_{ex}$.

4. **Key Features and Technical Details:**
- The step change in $V_{ex}$ at $t_1$ causes a change in $V_{cont}$, which is reflected in the gradual increase of $
\omega_{out}$ and $V_{LPF}$.
- The shaded region between the lines of $
\omega_{out}$ and $V_{LPF}$ indicates the difference in response, showing how $V_{LPF}$ lags behind $
\omega_{out}$.
- The difference between $V_1$ and $V_2$ is highlighted at the end of the graph, showing the change in system response.

5. **Annotations and Specific Data Points:**
- The step at $t_1$ is marked with a dotted vertical line, indicating the point of change in $V_{ex}$.
- The graph shows how the system gradually reaches a new stable state after the step change, with $V_{LPF}$ and $
\omega_{out}$ increasing towards their new values.

Figure 16.14

#### Solution

(a) If the loop is locked, $\omega_{\text {out }}=\omega_{\text {in }}$ and $V_{\text {cont }}=\left(\omega_{\text {in }}-\omega_{0}\right) / K_{V C O}$. Thus, $V_{L P F}=\left(\omega_{\text {in }}-\omega_{0}\right) / K_{V C O}-V_{1}$ and $\Delta \phi=V_{L P F} / K_{P D}=\left(\omega_{i n}-\omega_{0}\right) /\left(K_{P D} K_{V C O}\right)-V_{1} / K_{P D}$.
(b) When $V_{e x}$ steps from $V_{1}$ to $V_{2}, V_{c o n t}$ immediately goes from $\left(\omega_{i n}-\omega_{0}\right) / K_{V C O}$ to $\left(\omega_{i n}-\omega_{0}\right) / K_{V C O}+\left(V_{2}-V_{1}\right)$, changing the VCO frequency to $\omega_{\text {in }}-K_{V C O}\left(V_{1}-V_{2}\right)$. Since $V_{L P F}$ cannot change instantaneously, the PD begins to

[^117]generate increasingly wider pulses, raising $V_{L P F}$ and increasing $\omega_{\text {out }}$. When the loop returns to lock, $\omega_{\text {out }}$ becomes equal to $\omega_{i n}$ and $V_{L P F}=\left(\omega_{i n}-\omega_{0}\right) / K_{V C O}-V_{2}$. The phase error also changes to $\left(\omega_{i n}-\omega_{0}\right) /\left(K_{P D} K_{V C O}\right)-$ $V_{2} / K_{P D}$. Note that the area under $\omega_{\text {out }}$ during the transient is equal to the change in the output phase and hence the change in the phase error:
\$\$

$$
\begin{equation*}
\int_{t 1}^{\infty} \omega_{\text {out }} d t=\frac{V_{1}-V_{2}}{K_{P D}} \tag{16.10}
\end{equation*}
$$

\$\$

From our study thus far, we conclude that phase-locked loops are "dynamic" systems, i.e., their response depends on the past values of the input and output. This is to be expected because the low-pass filter and the VCO introduce poles (and possibly zeros) in the loop transfer function. Moreover, we note that, so long as the input and the output remain perfectly periodic (i.e., $\phi_{\text {in }}=\omega_{\text {in }} t$ and $\phi_{\text {out }}=\omega_{\text {in }} t+\phi_{0}$ ), the loop operates in the steady state, exhibiting no transient. Thus, the PLL responds only to variations in the excess phase of the input or output. For example, in Fig. 16.11, $\phi_{\text {in }}=\omega_{1} t+\phi_{1} u\left(t-t_{1}\right)$, and in Fig. 16.12, $\phi_{i n}=\omega_{1} t+\Delta \omega \cdot t u\left(t-t_{1}\right)$.

### 16.1.3 Dynamics of Simple PLL

With the qualitative analysis of PLLs in the previous section, we can now study their transient behavior more rigorously. Assuming that the loop is initially locked, we treat the PLL as a feedback system but recognize that the output quantity in this analysis must be the (excess) phase of the VCO because the "error amplifier" can only compare phases. Our objective is to determine the transfer function $\Phi_{\text {out }}(s) / \Phi_{\text {in }}(s)$ for both open-loop and closed-loop systems and subsequently study the time-domain response. Note that the dimensions change from phase to voltage through the PD and from voltage to phase through the VCO.

What does $\Phi_{\text {out }}(s) / \Phi_{\text {in }}(s)$ signify? An analogy with more familiar transfer functions proves useful here. A circuit having a transfer function $V_{\text {out }}(s) / V_{\text {in }}(s)=1 /\left(1+s / \omega_{0}\right)$ is considered a low-pass filter because if $V_{\text {in }}$ varies rapidly, $V_{\text {out }}$ cannot fully track the input variations. Similarly, $\Phi_{\text {out }}(s) / \Phi_{\text {in }}(s)$ reveals how the output phase tracks the input phase if the latter changes slowly or rapidly.

To visualize the variation of the excess phase with time, consider the waveforms in Fig. 16.15. The period varies slowly in Fig. 16.15(a) and rapidly in Fig. 16.15(b). Thus, $y_{2}(t)$ experiences faster phase variations than does $y_{1}(t)$.
image_name:(a)
description:The graph labeled "(a)" in Fig. 16.15 is a time-domain waveform depicting the function $y_1(t)$. The horizontal axis represents time, denoted as $t$, and the vertical axis represents the amplitude of the waveform, labeled as $y_1(t)$. The waveform is a periodic square wave, characterized by a consistent and uniform cycle of high and low states. The period of the waveform is relatively long, indicating a slow variation in phase over time.

The waveform maintains a constant amplitude during each high and low state, with sharp transitions between these states, typical of a square wave. There are no annotations or specific markers on the graph, suggesting a focus on the qualitative behavior of the waveform rather than precise quantitative measurements. The general trend shows a steady repetition of the waveform pattern, implying stable phase characteristics over the observed time interval.
image_name:(b)
description:The diagram labeled \( (b) \) in the provided image represents a time-domain waveform \( y_2(t) \). This is a square wave graph that illustrates the variation of a signal over time.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform depicting a square wave.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \( t \), representing time. The units of time are not explicitly stated, but it is typically in seconds or milliseconds in such contexts.
- The vertical axis represents the amplitude of the waveform. The amplitude values are not numerically labeled, but the waveform alternates between two levels, likely +1 and -1 or similar values.

3. **Overall Behavior and Trends:**
- The waveform is periodic and oscillates between two distinct amplitude levels.
- Compared to \( y_1(t) \) in the same figure, \( y_2(t) \) has a faster variation, indicating a higher frequency.
- The waveform exhibits a consistent and regular pattern of rising and falling edges, characteristic of a square wave.

4. **Key Features and Technical Details:**
- The waveform has a constant amplitude and period, with sharp transitions between the high and low states.
- There are no visible annotations or numerical markers indicating specific data points or values.

5. **Annotations and Specific Data Points:**
- No explicit numerical values or reference lines are provided in the diagram. The focus is on the qualitative difference in frequency between \( y_1(t) \) and \( y_2(t) \).

This waveform is used to illustrate how \( y_2(t) \) experiences faster phase variations compared to \( y_1(t) \), as mentioned in the context provided. This is relevant in the context of phase-locked loops (PLLs) and their response to varying input phases.

Figure 16.15 Slow and fast variation of the excess phase.
Let us construct a linear model of the PLL, assuming a first-order low-pass filter for simplicity. The PD output contains a dc component equal to $K_{P D}\left(\phi_{\text {out }}-\phi_{i n}\right)$ as well as high-frequency components. Since the latter are suppressed by the LPF, we simply model the PD by a subtractor whose output is "amplified" by $K_{P D}$. Illustrated in Fig. 16.16, the overall PLL model consists of the phase subtractor, the LPF transfer function $1 /\left(1+s / \omega_{L P F}\right)$, where $\omega_{L P F}$ denotes the $-3-\mathrm{dB}$ bandwidth, and the VCO transfer function $K_{V C O} / s$ (Chapter 15). Here, $\Phi_{\text {in }}$ and $\Phi_{\text {out }}$ denote the excess phases of the input and
image_name:Figure 16.16 Linear model of type I PLL
description:The system block diagram represents a linear model of a Type I Phase-Locked Loop (PLL). The key components of this PLL model include a phase detector (PD), a low-pass filter (LPF), and a voltage-controlled oscillator (VCO).

1. **Main Components:**
- **Phase Detector (PD):** This block is represented by a subtractor followed by an amplifier with a gain of \(K_{PD}\). The subtractor takes the input phase \(\Phi_{in}\) and subtracts the feedback phase \(\Phi_{out}\), producing a phase difference.
- **Low-Pass Filter (LPF):** This block is characterized by the transfer function \(\frac{1}{1 + \frac{s}{\omega_{LPF}}}\), where \(\omega_{LPF}\) is the cutoff frequency. It filters the output of the PD to suppress high-frequency noise.
- **Voltage-Controlled Oscillator (VCO):** The VCO is represented by the transfer function \(\frac{K_{VCO}}{s}\), where \(K_{VCO}\) is the gain of the VCO. It converts the filtered phase difference into the output phase \(\Phi_{out}\).

2. **Flow of Information or Control:**
- The input phase \(\Phi_{in}\) enters the PD, where it is compared with the feedback phase \(\Phi_{out}\). The resulting phase difference is amplified by \(K_{PD}\).
- The amplified signal is then passed through the LPF to remove high-frequency components, resulting in a smoothed control signal.
- This smoothed signal controls the VCO, which adjusts its output phase \(\Phi_{out}\) accordingly.
- The output phase \(\Phi_{out}\) is fed back to the PD, completing the feedback loop.

3. **Labels, Annotations, and Key Indicators:**
- \(\Phi_{in}\) and \(\Phi_{out}\) are labeled as the input and output phases, respectively.
- \(K_{PD}\) and \(K_{VCO}\) are the gains for the phase detector and VCO.
- The LPF is defined by its cutoff frequency \(\omega_{LPF}\).

4. **Overall System Function:**
- The primary function of this Type I PLL is to lock the output phase \(\Phi_{out}\) to the input phase \(\Phi_{in}\) by continuously adjusting the VCO based on the phase difference detected by the PD. The LPF ensures stability by filtering out high-frequency noise, allowing the VCO to produce a stable and accurate output phase.

Figure 16.16 Linear model of type I PLL.
output waveforms, respectively. For example, if the total input phase experiences a step change, $\phi_{1} u(t)$, then $\Phi_{i n}(s)=\phi_{1} / s$.

The open-loop transfer function is given by

$$
\begin{align*}
\left.H(s)\right|_{\text {open }} & =\left.\frac{\Phi_{\text {out }}}{\Phi_{\text {in }}}(s)\right|_{\text {open }}  \tag{16.11}\\
& =K_{P D} \cdot \frac{1}{1+\frac{s}{\omega_{L P F}}} \cdot \frac{K_{V C O}}{s} \tag{16.12}
\end{align*}
$$

revealing one pole at $s=-\omega_{L P F}$ and another at $s=0$. Note that the loop gain is equal to $\left.H(s)\right|_{\text {open }}$ because of the unity feedback factor. Since the loop gain contains a pole at the origin, the system is called "type I."

Before computing the closed-loop transfer function, let us make an important observation. What is the loop gain if $s$ is very small, i.e., if the input excess phase varies very slowly? Owing to the pole at the origin, the loop gain goes to infinity as $s$ approaches zero, a point of contrast to the feedback circuits studied in Chapters 8 and 10. Thus, the phase-locked loop (under closed-loop, locked condition) ensures that the change in $\phi_{\text {out }}$ is exactly equal to the change in $\phi_{\text {in }}$ as $s$ goes to zero. This result predicts two interesting properties of PLLs. First, if the input excess phase varies very slowly, the output excess phase "tracks" it. (After all, $\phi_{\text {out }}$ is "locked" to $\phi_{\text {in }}$.) Second, if the transients in $\phi_{i n}$ have decayed (another case corresponding to $s \rightarrow 0$ ), then the change in $\phi_{\text {out }}$ is precisely equal to the change in $\phi_{i n}$. This is indeed true in the example depicted in Fig. 16.11.

From (16.12), we can write the closed-loop transfer function as

$$
\begin{equation*}
\left.H(s)\right|_{\text {closed }}=\frac{K_{P D} K_{V C O}}{\frac{s^{2}}{\omega_{L P F}}+s+K_{P D} K_{V C O}} \tag{16.13}
\end{equation*}
$$

For the sake of brevity, we hereafter denote $\left.H(s)\right|_{\text {closed }}$ simply by $H(s)$ or $\Phi_{\text {out }} / \Phi_{\text {in }}$. As expected, if $s \rightarrow 0, H(s) \rightarrow 1$ because of the infinite loop gain.

In order to analyze $H(s)$ further, we derive a relationship that allows a more intuitive understanding of the system. Recall from Chapter 15 that the instantaneous frequency of a waveform is equal to the time derivative of the phase: $\omega=d \phi / d t$. Since the frequency and the phase are related by a linear operator, the transfer function of (16.13) applies to variations in the input and output frequencies as well:

$$
\begin{equation*}
\frac{\omega_{\text {out }}}{\omega_{\text {in }}}(s)=\frac{K_{P D} K_{V C O}}{\frac{s^{2}}{\omega_{L P F}}+s+K_{P D} K_{V C O}} \tag{16.14}
\end{equation*}
$$

For example, this result predicts that if $\omega_{\text {in }}$ changes very slowly $(s \rightarrow 0)$, then $\omega_{\text {out }}$ tracks $\omega_{\text {in }}$, again an expected result because the loop is assumed locked. Equation (16.14) also indicates that if $\omega_{\text {in }}$ changes
abruptly, but the system is given enough time to settle ( $s \rightarrow 0$ ), then the change in $\omega_{\text {out }}$ equals that in $\omega_{\text {in }}$ (as illustrated in the example of Fig. 16.12).

The above observation aids the analysis in two directions. First, some transient responses of the closedloop system may be simpler to visualize in terms of changes in the frequency quantities rather than the phase quantities. Second, since a change in $\omega_{\text {out }}$ must be accompanied by a change in $V_{\text {cont }}$, we have

$$
\begin{equation*}
H(s)=K_{V C O} \cdot \frac{V_{\text {cont }}}{\omega_{\text {in }}}(s) \tag{16.15}
\end{equation*}
$$

That is, monitoring the response of $V_{\text {cont }}$ to variations in $\omega_{\text {in }}$ indeed yields the response of the closed-loop system.

The second-order transfer function of (16.13) suggests that the step response of the type I system can be overdamped, critically damped, or underdamped. To derive the condition for each case, we rewrite the denominator in a familiar form used in control theory, $s^{2}+2 \zeta \omega_{n} s+\omega_{n}^{2}$, where $\zeta$ is the "damping factor" and $\omega_{n}$ is the "natural frequency." That is

$$
\begin{equation*}
H(s)=\frac{\omega_{n}^{2}}{s^{2}+2 \zeta \omega_{n} s+\omega_{n}^{2}} \tag{16.16}
\end{equation*}
$$

where

$$
\begin{array}{r}
\omega_{n}=\sqrt{\omega_{L P F} K_{P D} K_{V C O}} \\
\zeta=\frac{1}{2} \sqrt{\frac{\omega_{L P F}}{K_{P D} K_{V C O}}} \tag{16.18}
\end{array}
$$

The two poles of the closed-loop system are given by

$$
\begin{align*}
s_{1,2} & =-\zeta \omega_{n} \pm \sqrt{\left(\zeta^{2}-1\right) \omega_{n}^{2}}  \tag{16.19}\\
& =\left(-\zeta \pm \sqrt{\left.\zeta^{2}-1\right)} \omega_{n}\right. \tag{16.20}
\end{align*}
$$

Thus, if $\zeta>1$, both poles are real, the system is overdamped, and the transient response contains two exponentials with time constants $1 / s_{1}$ and $1 / s_{2}$. On the other hand, if $\zeta<1$, the poles are complex and the response to an input frequency step $\omega_{i n}=\Delta \omega u(t)$ is equal to

$$
\begin{align*}
\omega_{\text {out }}(t) & =\left\{1-e^{-\zeta \omega_{n} t}\left[\cos \left(\omega_{n} \sqrt{1-\zeta^{2}} t\right)+\frac{\zeta}{\sqrt{1-\zeta^{2}}} \sin \left(\omega_{n} \sqrt{1-\zeta^{2}} t\right)\right]\right\} \Delta \omega u(t)  \tag{16.21}\\
& =\left[1-\frac{1}{\sqrt{1-\zeta^{2}}} e^{-\zeta \omega_{n} t} \sin \left(\omega_{n} \sqrt{1-\zeta^{2}} t+\theta\right)\right] \Delta \omega u(t) \tag{16.22}
\end{align*}
$$

where $\omega_{\text {out }}$ denotes the change in the output frequency and $\theta=\sin ^{-1} \sqrt{1-\zeta^{2}}$. Thus, as shown in Fig. 16.17, the step response contains a sinusoidal component with a frequency $\omega_{n} \sqrt{1-\zeta^{2}}$ that decays with a time constant $\left(\zeta \omega_{n}\right)^{-1}$. Note that the system exhibits the same response if a phase step is applied to the input and the output phase is observed.

The settling speed of PLLs is of great concern in most applications. Equation (16.22) indicates that the exponential decay determines how fast the output approaches its final value, implying that $\zeta \omega_{n}$ must be maximized. For the type I PLL under study here, (16.17) and (16.18) yield

$$
\begin{equation*}
\zeta \omega_{n}=\frac{1}{2} \omega_{L P F} \tag{16.23}
\end{equation*}
$$

image_name:Figure 16.17 Underdamped response of PLL to a frequency step
description:The graph in Figure 16.17 illustrates the underdamped response of a Phase-Locked Loop (PLL) to a frequency step. This is a time-domain waveform graph.

**Axes Labels and Units:**
- The horizontal axis represents time \(t\), though specific units are not labeled, it is typically in seconds or milliseconds in such contexts.
- The vertical axis represents frequency, with \(\omega_{in}\) indicating the input frequency step and \(\omega_{out}\) representing the output frequency response.

**Overall Behavior and Trends:**
- The graph shows an initial step increase in the input frequency \(\omega_{in}\), which causes the output frequency \(\omega_{out}\) to respond.
- The output frequency exhibits an underdamped response characterized by oscillations that decrease in amplitude over time.
- The oscillations gradually settle towards a steady-state value, indicating the system's settling time.

**Key Features and Technical Details:**
- The response begins with a sharp rise as the system attempts to follow the input step change.
- The oscillatory behavior is typical of an underdamped system, where the amplitude of oscillations decreases exponentially over time.
- The dotted line represents the envelope of the decaying oscillations, following an exponential decay function \(e^{-\zeta \omega_{n} t}\), where \(\zeta\) is the damping ratio and \(\omega_{n}\) is the natural frequency.
- The peak of the first oscillation is the maximum overshoot, a common characteristic of underdamped systems.

**Annotations and Specific Data Points:**
- The graph includes a label indicating the exponential decay \(e^{-\zeta \omega_{n} t}\), highlighting the rate at which oscillations decrease.
- No specific numerical values or scales are provided in the graph, but the behavior suggests typical PLL dynamics in response to frequency steps, emphasizing the trade-off between rapid settling and overshoot/ripple characteristics.

Figure 16.17 Underdamped response of PLL to a frequency step.

This result reveals a critical trade-off between the settling speed and the ripple on the VCO control line: the lower the $\omega_{L P F}$, the greater the suppression of the high-frequency components produced by the PD, but the longer the settling time constant.

#### Example 16.5

A cellular telephone incorporates a $900-\mathrm{MHz}$ phase-locked loop to generate the carrier frequencies. If $\omega_{L P F}=$ $2 \pi \times(20 \mathrm{kHz})$ and the output frequency is to be changed from 901 MHz to 901.2 MHz , how long does the PLL output frequency take to settle within 100 Hz of its final value?

#### Solution

Since the step size is 200 kHz , we have

$$
\begin{equation*}
\left[1-e^{-\zeta \omega_{n} t_{s}} \sin \left(\omega_{n} \sqrt{1-\zeta^{2}} t_{s}+\theta\right)\right] \times 200 \mathrm{kHz}=200 \mathrm{kHz}-100 \mathrm{~Hz} \tag{16.24}
\end{equation*}
$$

Thus,

$$
\begin{equation*}
e^{-\zeta \omega_{n} t_{s}} \sin \left(\omega_{n} \sqrt{1-\zeta^{2}} t_{s}+\theta\right)=\frac{100 \mathrm{~Hz}}{200 \mathrm{kHz}} \tag{16.25}
\end{equation*}
$$

In the worst case, the sinusoid is equal to unity and

$$
\begin{equation*}
e^{-\zeta \omega_{n} t_{s}}=0.0005 \tag{16.26}
\end{equation*}
$$

That is

$$
\begin{align*}
t_{s} & =\frac{7.6}{\zeta \omega_{n}}  \tag{16.27}\\
& =\frac{15.2}{\omega_{L P F}}  \tag{16.28}\\
& =0.12 \mathrm{~ms} \tag{16.29}
\end{align*}
$$

In addition to the product $\zeta \omega_{n}$, the value of $\zeta$ itself is also important. Illustrated in Fig. 16.18 for several values of $\zeta$ and a constant $\omega_{n}$, the step response exhibits severe ringing for $\zeta<0.5$. In view of process and temperature variation of the loop parameters, $\zeta$ is usually chosen to be greater than $\sqrt{2} / 2$ or even 1 to avoid excessive ringing. ${ }^{4}$

image_name:Figure 16.18
description:The graph in Figure 16.18 depicts the step response of a second-order system for various damping ratios (\(\zeta\)). This is a time-domain waveform graph.

**Axes Labels and Units:**
- The horizontal axis represents time (\(t\)), though no specific units are marked, it is typically in seconds or milliseconds in such contexts.
- The vertical axis represents the amplitude of the response, which is usually normalized.

**Overall Behavior and Trends:**
- The graph shows three distinct curves, each corresponding to different values of the damping ratio \(\zeta\): 0.2, 0.5, and \(\sqrt{2}/2\).
- The curve with \(\zeta = 0.2\) exhibits significant oscillations and overshoot, indicating a highly underdamped system with severe ringing.
- The curve with \(\zeta = 0.5\) shows less oscillation and a quicker settling time compared to \(\zeta = 0.2\), but still has noticeable overshoot.
- The curve with \(\zeta = \sqrt{2}/2\) is more critically damped, showing minimal overshoot and oscillation, approaching the steady-state value more smoothly.

**Key Features and Technical Details:**
- For \(\zeta = 0.2\), the peak amplitude is the highest among the three, with the oscillations gradually decaying over time.
- For \(\zeta = 0.5\), the peak is lower, and the oscillations are less pronounced, indicating a reduction in system energy dissipation.
- For \(\zeta = \sqrt{2}/2\), the response is nearly critically damped, with a smooth rise to the final value and minimal oscillation.

**Annotations and Specific Data Points:**
- The graph includes annotations indicating the values of \(\zeta\) for each curve.
- There are no specific numerical values provided for the time or amplitude, but the general behavior of the system for different damping ratios is clearly illustrated.

Figure 16.18 Underdamped response of a second-order system for various values of $\zeta$.
The choice of $\zeta$ entails other trade-offs as well. First, (16.18) implies that as $\omega_{L P F}$ is reduced to minimize the ripple on the control voltage, the stability degrades. Second, (16.5) and (16.18) indicate that both the phase error and $\zeta$ are inversely proportional to $K_{P D} K_{V C O}$; lowering the phase error inevitably makes the system less stable. In summary, the type I PLL suffers from trade-offs among the settling speed, the ripple on the control voltage (i.e., the quality of the output signal), the phase error, and the stability.

The stability behavior of PLLs can also be analyzed graphically, providing more insight. Recall from Chapter 10 that the Bode plots of the magnitude and phase of the loop gain readily yield the phase margin. Let us utilize (16.12) to construct such plots. As shown in Fig. 16.19, the loop gain begins from infinity at $\omega=0$ and falls at a rate of $20 \mathrm{~dB} / \mathrm{dec}$ for $\omega<\omega_{L P F}$ and at a rate of $40 \mathrm{~dB} / \mathrm{dec}$ thereafter. The phase begins at $-90^{\circ}$ and asymptotically reaches $-180^{\circ}$.
image_name:Figure 16.19 Bode plots of type I PLL
description:The graph in Figure 16.19 consists of two Bode plots representing the magnitude and phase of the loop gain of a type I Phase-Locked Loop (PLL).

Type of Graph and Function:
- **Type:** Bode plot
- **Function:** Loop gain of a type I PLL

Axes Labels and Units:
- **Magnitude Plot:**
- Vertical Axis: `20log|H_open|` in decibels (dB)
- Horizontal Axis: Frequency `ω` on a logarithmic scale
- **Phase Plot:**
- Vertical Axis: `∠H_open` in degrees
- Horizontal Axis: Frequency `ω` on a logarithmic scale

Overall Behavior and Trends:
- **Magnitude Plot:**
- The plot starts at infinity for `ω=0` and decreases at a rate of `-20 dB/decade` for frequencies less than `ω_LPF`.
- After `ω_LPF`, the slope increases to `-40 dB/decade`, indicating a steeper decline.
- **Phase Plot:**
- The phase begins at `-90°` and asymptotically approaches `-180°` as the frequency increases.

Key Features and Technical Details:
- **Magnitude Plot:**
- Breakpoint at `ω_LPF`, where the slope changes from `-20 dB/decade` to `-40 dB/decade`.
- **Phase Plot:**
- The phase shift starts at `-90°` and approaches `-180°`, indicating a phase lag as frequency increases.

Annotations and Specific Data Points:
- **Magnitude Plot:**
- The slope change is marked and the frequency `ω_LPF` is highlighted with a vertical dashed line.
- **Phase Plot:**
- The asymptotic behavior towards `-180°` is shown with horizontal dashed lines at `-90°`, `-135°`, and `-180°`.

This graph visually demonstrates how the loop gain's magnitude and phase behave over a range of frequencies, with the transition at `ω_LPF` being a critical point for both magnitude and phase characteristics. The plots provide insight into the stability and response of the PLL system, with the phase margin being an essential parameter for assessing stability.

Figure 16.19 Bode plots of type I PLL.
What happens if a higher $K_{P D} K_{V C O}$ is chosen so as to minimize $\phi_{o u t}-\phi_{\text {in }}$ ? Since the entire gain plot in Fig. 16.19 is shifted up, the gain crossover moves to the right, thus degrading the phase margin. This is consistent with the dependence of $\zeta$ upon $K_{P D} K_{V C O}$.

As observed thus far, $K_{P D} K_{V C O}$ affects many important parameters of PLLs. This quantity is sometimes called the loop gain (even though it is not dimensionless) because of the resemblance of $\Delta \phi=\left(\omega_{\text {out }}-\omega_{0}\right) /\left(K_{P D} K_{V C O}\right)$ to the error equation in a feedback system.

The stability behavior of type I PLLs can also be analyzed by the locus of their poles in the complex plane as the parameter $K_{P D} K_{V C O}$ varies (Fig. 16.20). With $K_{P D} K_{V C O}=0$, the loop is open, $\zeta=\infty$, and the two poles are given by $s_{1}=-\omega_{L P F}$ and $s_{2}=0$. As $K_{P D} K_{V C O}$ increases (i.e., the feedback becomes
image_name:Figure 16.20 Root locus of type IPLL
description:Figure 16.20 presents a root locus plot for a type I Phase-Locked Loop (PLL). This graph is used to analyze the stability and dynamic behavior of the PLL as the loop gain, represented by the product \(K_{PD} K_{VCO}\), varies.

**1. Type of Graph and Function:**
- The graph is a root locus plot, which is a graphical representation of the roots of a system's characteristic equation in the complex plane as a particular parameter varies.

**2. Axes Labels and Units:**
- The horizontal axis (\(\sigma\)) represents the real part of the poles.
- The vertical axis (\(j\omega\)) represents the imaginary part of the poles.
- The axes are in terms of frequency, with units likely in radians per second.

**3. Overall Behavior and Trends:**
- The plot shows the movement of poles in the complex plane as the loop gain increases.
- Initially, when \(K_{PD} K_{VCO} = 0\), the poles are located at \(-\omega_{LPF}\) and the origin (0).
- As the gain increases, the poles move towards each other along the real axis.
- At a critical damping point (\(\zeta = 1\)), the poles coincide at \(-\omega_{LPF}/2\).
- Beyond this point, the poles become complex conjugates, moving vertically along lines parallel to the imaginary axis, indicating oscillatory behavior.

**4. Key Features and Technical Details:**
- The plot shows a pole starting at \(-\omega_{LPF}\) on the real axis and another at the origin.
- The poles meet at \(-\omega_{LPF}/2\) when the system is critically damped.
- Beyond this point, the poles are complex, with a constant real part of \(-\omega_{LPF}/2\), indicating a stable oscillatory response.
- The angle \(\phi\) represents the phase margin, a critical parameter for stability analysis.

**5. Annotations and Specific Data Points:**
- The graph includes annotations for \(-\omega_{LPF}\), \(\omega_{LPF}/2\), and the angle \(\phi\).
- The arrows indicate the direction of pole movement as the gain increases, providing insight into the system's stability changes.

Figure 16.20 Root locus of type IPLL.
stronger), $\zeta$ drops and the two poles, given by $s_{1,2}=\left(-\zeta \pm \sqrt{\zeta^{2}-1}\right) \omega_{n}$, move toward each other on the real axis. For $\zeta=1$ (i.e., $\left.K_{P D} K_{V C O}=\omega_{L P F} / 4\right), s_{1}=s_{2}=-\zeta \omega_{n}=-\omega_{L P F} / 2$. As $K_{P D} K_{V C O}$ increases further, the two poles become complex, with a real part equal to $-\zeta \omega_{n}=-\omega_{L P F} / 2$, moving in parallel with the $j \omega$ axis.

We recognize from Fig. 16.20 that, as $s_{1}$ and $s_{2}$ move away from the real axis, the system becomes less stable. In fact, the reader can prove that $\cos \psi=\zeta$ (Problem 16.8), concluding that as $\psi$ approaches $90^{\circ}, \zeta$ drops to zero.

Another transfer function that reveals the settling behavior of PLLs is that of the error at the output of the phase subtractor in Fig. 16.16. Defined as $H_{e}(s)=\left(\phi_{\text {in }}-\phi_{\text {out }}\right) / \phi_{i n}$, this transfer function can be obtained by noting that $\phi_{\text {out }} / \phi_{\text {in }}=H(s)$ and, from (16.13),

$$
\begin{align*}
H_{e}(s) & =1-H(s)  \tag{16.30}\\
& =\frac{s^{2}+2 \zeta \omega_{n} s}{s^{2}+2 \zeta \omega_{n} s+\omega_{n}} \tag{16.31}
\end{align*}
$$

As expected, $H_{e}(s) \rightarrow 0$ if $s \rightarrow 0$ because the output tracks the input when the input varies very slowly or the transient has settled.

#### Example 16.6

Suppose a type I PLL experiences a frequency step $\Delta \omega$ at $t=0$. Calculate the change in the phase error.

#### Solution

The Laplace transform of the frequency step equals $\Delta \omega / s$. Since $H_{e}(s)$ relates the phase error to the input phase, we write $\Phi_{i n}(s)=(\Delta \omega / s) / s=\Delta \omega / s^{2}$. Thus, the Laplace transform of the phase error is

$$
\begin{align*}
\Phi_{e}(s) & =H_{e}(s) \cdot \frac{\Delta \omega}{s^{2}}  \tag{16.32}\\
& =\frac{s^{2}+2 \zeta \omega_{n} s}{s^{2}+2 \zeta \omega_{n} s+\omega_{n}^{2}} \cdot \frac{\Delta \omega}{s^{2}} \tag{16.33}
\end{align*}
$$

From the final value theorem,

$$
\begin{align*}
\phi_{e}(t=\infty) & =\lim _{s \rightarrow 0} s \Phi_{e}(s)  \tag{16.34}\\
& =\frac{2 \zeta}{\omega_{n}} \Delta \omega  \tag{16.35}\\
& =\frac{\Delta \omega}{K_{P D} K_{V C O}} \tag{16.36}
\end{align*}
$$

which agrees with (16.5).

## 16.2 ■ Charge-Pump PLLs

While type I PLLs have been realized widely in discrete form, their shortcomings often prohibit usage in high-performance integrated circuits. In addition to the trade-offs among $\zeta, \omega_{L P F}$, and the phase error, type I PLLs suffer from another critical drawback: limited acquisition range.

### 16.2.2 Phase/Frequency Detector

For periodic signals, it is possible to merge the two loops of Fig. 16.21 by devising a circuit that can detect both phase and frequency differences. Called a phase/frequency detector (PFD) and illustrated conceptually in Fig. 16.22, the circuit employs sequential logic to create three states and respond to the rising (or falling) edges of the two inputs. If initially $Q_{A}=Q_{B}=0$, then a rising transition on $A$ leads to $Q_{A}=1, Q_{B}=0$. The circuit remains in this state until $B$ goes high, at which point $Q_{A}$ returns to zero. In other words, if a rising edge on $A$ is followed by a rising edge on $B$, then $Q_{A}$ goes high and returns to low. The behavior is similar for the $B$ input.
image_name:PFD
description:The system block diagram represents a Phase Frequency Detector (PFD) used to compare the phases and frequencies of two input signals, A and B. The diagram consists of the following main components and flow of information:

1. **Main Components:**
- **PFD Block:** This is the central component that receives two input signals, A and B, and produces two output signals, Q_A and Q_B.

2. **Flow of Information or Control:**
- **Inputs:**
- Signal A and Signal B are the input signals fed into the PFD block.
- **Outputs:**
- Q_A and Q_B are the output signals generated by the PFD block.
- **Signal Flow:**
- The PFD compares the phases (ϕ) and frequencies (ω) of the input signals A and B. The outputs Q_A and Q_B are determined by the relative phase and frequency differences between A and B.

3. **Labels, Annotations, and Key Indicators:**
- The diagram is divided into two scenarios labeled (a) and (b).
- **Scenario (a):**
- Describes a condition where the phases of A and B are unequal (ϕ_A ≠ ϕ_B), resulting in Q_A producing pulses while Q_B remains at zero.
- **Scenario (b):**
- Describes a condition where the frequencies of A and B are unequal (ω_A ≠ ω_B), leading to Q_A generating pulses while Q_B remains quiet.

4. **Overall System Function:**
- The primary function of the PFD is to detect and indicate phase and frequency differences between two input signals. When the phase or frequency of A leads B, Q_A produces output pulses. Conversely, if A lags B, Q_B would produce pulses (not shown in the diagram). This behavior is crucial in applications like phase-locked loops (PLLs) where maintaining phase and frequency alignment between signals is necessary.
image_name:(a)
description:The graph in Fig. 16.22(a) is a time-domain waveform illustrating the operation of a Phase Frequency Detector (PFD) with two input signals, **A** and **B**, and two output signals, **Q_A** and **Q_B**. The horizontal axis represents time (**t**), and the waveforms are aligned vertically to show their timing relationships.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph, showing the behavior of digital signals over time.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as time (**t**), though specific units are not provided, it is typically in seconds or a submultiple.

3. **Overall Behavior and Trends:**
- The input signals **A** and **B** are digital square waves with equal frequencies, but signal **A** leads signal **B** in phase (i.e., **φ_A ≠ φ_B**).
- The output **Q_A** produces pulses whose width is proportional to the phase difference between **A** and **B**.
- The output **Q_B** remains at a constant low level, indicating that it is not active when **A** leads **B**.

4. **Key Features and Technical Details:**
- **A** and **B** are shown as square waves with a consistent period, indicating equal frequencies.
- **Q_A** generates pulses at each rising edge of **A** until **B** catches up, reflecting the phase difference.
- **Q_B** remains low throughout the observation period, as **B** is lagging.

5. **Annotations and Specific Data Points:**
- The annotation **φ_A ≠ φ_B** indicates the phase difference between **A** and **B**.
- The waveform shows that the width of the pulses in **Q_A** corresponds to the lead of **A** over **B**.
image_name:(b)
description:The diagram labeled "(b)" in Figure 16.22 illustrates the operation of a Phase Frequency Detector (PFD) when the input signals have different frequencies, denoted by \( \omega_A \neq \omega_B \). This is a time-domain waveform graph, showing the behavior of the signals over time.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform representation.
- It displays the input signals \( A \) and \( B \) and the output signals \( Q_A \) and \( Q_B \) from the PFD.

2. **Axes Labels and Units:**
- The horizontal axis represents time \( t \), with no specific units or scale indicated.
- There are no vertical axis labels, but the vertical position indicates the logic levels (high or low) of the signals.

3. **Overall Behavior and Trends:**
- Signal \( A \) has a higher frequency than signal \( B \), as indicated by more frequent rising and falling edges.
- The output \( Q_A \) generates pulses corresponding to the frequency difference, while \( Q_B \) remains low.
- The pulses in \( Q_A \) occur at the rising edges of \( A \) where \( B \) remains low, indicating that \( A \) is leading in frequency.

4. **Key Features and Technical Details:**
- The waveform for \( A \) shows more cycles in the same time frame compared to \( B \), confirming that \( A \) has a higher frequency.
- \( Q_A \) produces narrow pulses at each rising edge of \( A \) when \( B \) is low, illustrating the phase difference.
- \( Q_B \) remains consistently low, indicating no phase lead of \( B \) over \( A \).

5. **Annotations and Specific Data Points:**
- The graph is annotated with \( \omega_A \neq \omega_B \) to emphasize the frequency difference.
- No specific numerical values or additional markers are provided in the graph.

Figure 16.22 Conceptual operation of a PFD.
In Fig. 16.22(a), the two inputs have equal frequencies, but $A$ leads $B$. The output $Q_{A}$ continues to produce pulses whose width is proportional to $\phi_{A}-\phi_{B}$ while $Q_{B}$ remains at zero. In Fig. 16.22(b), $A$ has a higher frequency than $B$, and $Q_{A}$ generates pulses while $Q_{B}$ does not. By symmetry, if $A$ lags $B$ or has a lower frequency than $B$, then $Q_{B}$ produces pulses and $Q_{A}$ remains quiet. Thus, the dc contents of $Q_{A}$ and $Q_{B}$ provide information about $\phi_{A}-\phi_{B}$ or $\omega_{A}-\omega_{B}$. The outputs $Q_{A}$ and $Q_{B}$ are called the "UP" and "DOWN" pulses, respectively.

#### Example 16.7

Explain whether a master-slave D flipflop can operate as a phase detector or a frequency detector. Assume that the flipflop provides differential outputs.

#### Solution

As shown in Fig. 16.23(a), we first apply inputs having equal frequencies and a finite phase difference, assuming that the output changes on the rising edge of the clock input. If $A$ leads $B$, then $V_{\text {out }}$ remains at a logical ONE indefinitely because the flipflop continues to sample the high levels of $A$. Conversely, if $A$ lags $B$, then $V_{\text {out }}$ remains low. Plotted in Fig. 16.23(b), the input-output characteristic of the circuit displays a very high gain at $\Delta \phi=$ $0, \pm \pi, \cdots$ and a zero gain at other values of $\Delta \phi$. The D flipflop is sometimes called a "bang-bang" phase detector to emphasize that the average value of $V_{\text {out }}$ jumps from $-V_{1}$ to $+V_{1}$ as $\Delta \phi$ varies from slightly below zero to slightly above zero.

Now let us assume unequal frequencies for $A$ and $B$. If the flipflop is to behave as a frequency detector, then the average value of $V_{\text {out }}$ must exhibit different polarities for $\omega_{A}>\omega_{B}$ and $\omega_{A}<\omega_{B}$. However, as illustrated in Fig. 16.23(c), the average value is zero in both cases.
image_name:(a)
description:The diagram labeled (a) illustrates a D flip-flop circuit used as a phase detector. The main components of this system are:

1. **D Flip-Flop**: This is the central component of the circuit. It has two inputs labeled A and B, and two outputs labeled Q and \(\overline{Q}\). The D input is set to a logical ONE, and the clock input (CK) is connected to signal B.

2. **Inputs**:
- **A**: A digital signal input to the D flip-flop.
- **B**: Another digital signal input, which acts as the clock (CK) for the flip-flop.

3. **Outputs**:
- **\(V_{out}\)**: The output of the flip-flop, taken from the Q output, which shows the phase relationship between inputs A and B.

**Flow of Information**:
- Signal A is fed into the D input of the flip-flop, while signal B is connected to the clock input. The flip-flop samples the value of A at the rising edge of B.
- The output \(V_{out}\) reflects the sampled value of A, depending on the phase relationship between A and B.

**Annotations and Indicators**:
- The diagram shows timing waveforms for both inputs A and B, as well as the resulting \(V_{out}\).
- The output \(V_{out}\) is depicted as switching between +\(V_1\) and -\(V_1\), indicating the phase relationship.

**Overall System Function**:
The primary function of this system is to detect the phase difference between two digital signals, A and B. When A leads B, the average value of \(V_{out}\) is +\(V_1\), and when A lags B, the average value is -\(V_1\). This behavior allows the D flip-flop to function as a phase detector, indicating the phase relationship between the input signals through the average output voltage.
image_name:(b)
description:The graph labeled as "(b)" represents the input-output characteristic of a D flip-flop used as a phase detector. This is a plot of the time average of the output voltage, $V_{\text{out}}$, against the phase difference, $\Delta \phi$, between two input signals A and B.

1. **Type of Graph and Function:**
- The graph is a characteristic curve showing the relationship between the average output voltage and the phase difference, which is typical for phase detectors.

2. **Axes Labels and Units:**
- The x-axis represents the phase difference, $\Delta \phi$, measured in radians. It is marked with values ranging from $-\pi$ to $\pi$.
- The y-axis represents the time average of the output voltage, $V_{\text{out}}$, with units in volts. The axis is labeled with values $-V_1$ and $+V_1$.

3. **Overall Behavior and Trends:**
- The graph shows a periodic waveform with a square shape, alternating between $+V_1$ and $-V_1$ as the phase difference varies.
- The waveform has a period of $2\pi$, indicating that the output voltage repeats every $2\pi$ radians of phase difference.

4. **Key Features and Technical Details:**
- The waveform crosses the zero line at $\Delta \phi = 0$, indicating that the average output voltage is zero when there is no phase difference between the input signals.
- The graph exhibits abrupt transitions at phase differences of $\pm\pi$, where the average output voltage jumps from $-V_1$ to $+V_1$ or vice versa.

5. **Annotations and Specific Data Points:**
- The key data points are the transitions at $\Delta \phi = -\pi$, $0$, and $\pi$, where the time average of $V_{\text{out}}$ changes polarity.
- There are no additional annotations or markers on the graph, but the periodic nature and symmetry about the origin are visually clear.
image_name:(c)
description:The graph in Figure 16.23(c) is a time-domain waveform illustrating the behavior of a D flipflop when subjected to two unequal input frequencies, denoted as signals A and B. The graph displays the input signals A and B as square waves, along with the resulting output signal, V_out, over time.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph showing the output response of a digital circuit (D flipflop) to varying input signals.

2. **Axes Labels and Units:**
- The horizontal axis represents time (t), although no specific units are provided. The vertical axis represents voltage levels, with specific reference to +V1 and -V1 as potential output levels.

3. **Overall Behavior and Trends:**
- The input signals A and B are shown as periodic square waves with slightly different frequencies. The output V_out is also a square wave that changes according to the phase relationship between A and B. When the frequencies are unequal, V_out averages to zero over time, as indicated by the dashed line at the zero-voltage level.

4. **Key Features and Technical Details:**
- The output waveform V_out is highlighted with shaded areas, indicating the portions of time when the output is either high or low. Despite the unequal frequencies, the average value of V_out remains zero, demonstrating the flipflop's inability to detect frequency differences through average voltage.

5. **Annotations and Specific Data Points:**
- The graph includes a dashed line representing the zero-voltage level, which is the average value of V_out over time. The shaded regions in the V_out waveform indicate the high and low states relative to this average.

Figure 16.23 (a) D flipflop as a phase detector; (b) input-output characteristic; (c) response of D flipflop to unequal input frequencies.

The circuit of Fig. 16.22 can be realized in various forms. Figure 16.24(a) shows a simple implementation consisting of two edge-triggered, resettable D flipflops with their D inputs tied to a logical ONE.
image_name:Figure 16.24 (a)
description:The circuit is a Phase Frequency Detector (PFD) using two D flip-flops and an AND gate. Inputs A and B serve as clocks for the flip-flops. QA and QB outputs are reset simultaneously by the AND gate when both are high. This configuration helps detect phase differences between inputs A and B.
image_name:A, B, Q_A, Q_B waveforms
description:The graph titled "A, B, Q_A, Q_B waveforms" is a time-domain waveform representation. The x-axis represents time (t) with no specific units or scale indicated, suggesting a continuous flow of time. The y-axis denotes the logical states of the signals A, B, Q_A, and Q_B, which typically switch between logical high (1) and low (0).

1. **Type of Graph and Function:**
- This is a time-domain waveform graph showing digital signals.

2. **Axes Labels and Units:**
- The x-axis is labeled as time (t), while the y-axis represents the logical state of the signals. No specific units are provided.

3. **Overall Behavior and Trends:**
- The waveforms for A and B are periodic square waves, both having similar frequencies but with a phase difference, where A leads B.
- Q_A and Q_B are also square waves but are triggered by the rising edges of A and B, respectively.
- Q_A goes high when A goes high and remains high until a reset condition is met.
- Similarly, Q_B goes high when B goes high and is reset shortly after.

4. **Key Features and Technical Details:**
- The signals A and B serve as clock inputs for the flip-flops, and they are shown as periodic signals with equal time intervals between transitions.
- Q_A and Q_B are outputs of D flip-flops that respond to the rising edges of A and B, respectively.
- The reset condition, which is not explicitly shown in the waveforms, is implied to occur when both Q_A and Q_B are high, resetting both to low.

5. **Annotations and Specific Data Points:**
- The diagram does not provide specific numerical values or annotations for the waveforms, focusing instead on the logical interaction between A, B, Q_A, and Q_B.
- The timing of the reset is critical in ensuring that Q_A and Q_B do not remain high simultaneously for extended periods, which is a key aspect of their operation in phase detection.

Overall, the graph illustrates how the D flip-flops respond to the input signals A and B, with Q_A and Q_B reflecting the phase relationship between these inputs, crucial for applications like phase frequency detectors.
image_name:Figure 16.24 (b)
description:
[
name: D Flip-Flop 1, type: Other, ports: {N1: A, N2: Reset, N3: QA}
name: D Flip-Flop 2, type: Other, ports: {N1: B, N2: Reset, N3: QB}
name: AND Gate, type: Other, ports: {N1: QA, N2: QB, N3: Reset}
name: Latch 1, type: Other, ports: {N1: CK, N2: Q}
name: Latch 2, type: Other, ports: {N1: Q, N2: Reset}
]
extrainfo:The circuit is a Phase Frequency Detector (PFD) using D flip-flops and an AND gate. It compares the phase and frequency of two input signals, A and B.

Figure 16.24 (a) Implementation of PFD; (b) implementation of D flipflop.

The inputs of interest, $A$ and $B$, serve as the clocks of the flipflops. If $Q_{A}=Q_{B}=0$ and $A$ goes high, $Q_{A}$ rises. If this event is followed by a rising transition on $B, Q_{B}$ goes high and the AND gate resets both flipflops. In other words, $Q_{A}$ and $Q_{B}$ are simultaneously high for a short time, but the difference between their average values still represents the input phase or frequency difference correctly. Each flipflop can be implemented as shown in Fig. 16.24(b), where two RS latches are cross-coupled. Latch 1 and Latch 2 respond to the rising edges of $C K$ and Reset, respectively.

#### Example 16.8

Determine the width of the narrow reset pulses that appear in the $Q_{B}$ waveform in Fig. 16.24(a).

#### Solution

Figure 16.25(a) illustrates the overall PFD at the gate level. If the circuit begins with $A=1, Q_{A}=1$, and $Q_{B}=0$, a rising edge on $B$ forces $\overline{Q_{B}}$ to go low and, one gate delay later, $Q_{B}$ to go high. As shown in Fig. 16.25(b), this transition propagates to Reset, $\bar{E}$ and $\bar{F}, E$ and $F$, and finally to $Q_{A}$ and $Q_{B}$. Thus, the width of the pulse on $Q_{B}$ is approximately equal to 5 gate delays. ${ }^{8}$
image_name:Figure 16.25(a)
description:The diagram represents a Phase Frequency Detector (PFD) circuit at the gate level. It consists of a combination of logic gates, including XOR and AND gates, with feedback loops that generate signals QA and QB based on inputs A and B. The circuit is designed to detect the phase difference between two input signals, A and B, and produce outputs that control further stages in a phase-locked loop (PLL) system. The reset mechanism ensures the system returns to a known state after each cycle, maintaining synchronization between inputs.

image_name:Figure 16.25(b)
description:The graph in Figure 16.25(b) is a time-domain waveform illustrating the behavior of signals in a phase frequency detector (PFD) circuit. The graph consists of multiple horizontal segments representing digital signals, with each segment corresponding to a specific signal in the circuit.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform, showing the digital signal transitions over time.
- It is used to illustrate the operation of a PFD circuit, specifically showing how the signals change in response to inputs and the reset mechanism.

2. **Axes Labels and Units:**
- The horizontal axis represents time, though it is not explicitly labeled or scaled in the image.
- The vertical axis represents the logic levels of different signals in the circuit, with each signal labeled on the left side of the graph.

3. **Overall Behavior and Trends:**
- The signals exhibit step-like transitions between high and low logic levels, characteristic of digital waveforms.
- The signal labeled **B** shows a high-to-low transition, indicating a change in one of the input signals.
- **QB** and its complement **\( \overline{QB} \)** exhibit complementary transitions, reflecting the XOR operation in the PFD logic.
- The **Reset** signal shows a pulse, indicating the resetting of the circuit to synchronize the inputs.
- **F** and its complement **\( \overline{F} \)** also show complementary transitions, which are part of the feedback loop in the PFD.

4. **Key Features and Technical Details:**
- The transitions in the signals are marked by dashed arrows, indicating the direction and nature of change.
- The **Reset** signal plays a crucial role in maintaining synchronization, as seen by its pulse that resets the state of the circuit.
- The complementary nature of **QB** and **\( \overline{QB} \)**, as well as **F** and **\( \overline{F} \)**, highlights the XOR and feedback mechanisms in the PFD.

5. **Annotations and Specific Data Points:**
- The graph includes dashed lines and arrows to indicate the flow of transitions and the effect of the reset pulse.
- There are no numerical values provided for specific time points or duration of pulses, as the focus is on the qualitative behavior of the signals.

It is instructive to plot the input-output characteristic of the above PFD. Defining the output as the difference between the average values of $Q_{A}$ and $Q_{B}$ when $\omega_{A}=\omega_{B}$ and neglecting the effect of the narrow reset pulses, we note that the output varies symmetrically as $|\Delta \phi|$ begins from zero (Fig. 16.26). For $\Delta \phi= \pm 360^{\circ}, V_{\text {out }}$ reaches its extrema and subsequently changes sign. The slope of the characteristic can be viewed as the gain.

How is the PFD of Fig. 16.24(a) utilized in a phase-locked loop? Since the difference between the average values of $Q_{A}$ and $Q_{B}$ is of interest, the two outputs can be low-pass filtered and sensed differentially (Fig. 16.27). A PLL employing such a topology always locks, but, due to the finite "loop gain," $K_{P F D} K_{V C O}$, it suffers from a finite phase error.

### 16.2.3 Charge Pump

In order to avoid the finite phase error present in type I PLLs, we wish to raise the loop gain to infinity, perhaps by means of an integrator. As our first step, we interpose a "charge pump" (CP) between the PFD

image_name:Figure 16.26 Input-output characteristic of the three-state PFD
description:The graph titled "Figure 16.26 Input-output characteristic of the three-state PFD" is a piecewise linear function graph depicting the relationship between the output voltage \( V_{out} \) and the phase difference \( \Delta \phi \).

1. **Type of Graph and Function:**
- This is a piecewise linear graph representing the input-output characteristic of a three-state phase frequency detector (PFD).

2. **Axes Labels and Units:**
- The horizontal axis represents the phase difference \( \Delta \phi \) in degrees.
- The vertical axis represents the output voltage \( V_{out} \) in arbitrary units.

3. **Overall Behavior and Trends:**
- The graph shows a periodic triangular waveform with a period of 720 degrees.
- The waveform linearly increases from \(-360^\circ\) to \(+360^\circ\), resets to a lower voltage, and then repeats this pattern.
- The slope of the line segments indicates a linear relationship between \( V_{out} \) and \( \Delta \phi \) within each segment.

4. **Key Features and Technical Details:**
- The graph has key points at \( \Delta \phi = -360^\circ, 0^\circ, \) and \( +360^\circ \).
- At \( \Delta \phi = 0^\circ \), \( V_{out} \) crosses the origin, indicating a phase difference of zero.
- The graph exhibits a sawtooth pattern, characteristic of the three-state PFD, which is used to detect phase differences in PLL circuits.

5. **Annotations and Specific Data Points:**
- The graph includes annotations at \(-360^\circ\) and \(+360^\circ\) on the horizontal axis, marking the boundaries of the linear segments.
- No specific numerical values for \( V_{out} \) are provided, as the output is in arbitrary units.

Figure 16.26 Input-output characteristic of the three-state PFD.
image_name:Figure 16.27 PFD followed by low-pass filters.
description:The circuit diagram represents a PFD with a charge pump configuration, using an OpAmp (A0) to drive the output Vout. The signals QA and QB are inputs to the resistors R1 and R2, which are part of the filtering and amplification stage.

image_name:Figure 16.28 PFD with charge pump
description:The circuit diagram represents a Phase Frequency Detector (PFD) with a charge pump configuration. It uses two D flip-flops with inputs A and B, and outputs QA and QB. The charge pump is driven by these outputs. The current sources I1 and I2 are controlled by switches S1 and S2 to charge or discharge the capacitor CP, thereby controlling the output voltage Vout. The waveform timing diagrams illustrate the operation of the PFD and charge pump with respect to input signals A and B.
image_name:Figure 16.28 PFD with charge pump
description:The graph in Figure 16.27 illustrates the behavior of a Phase Frequency Detector (PFD) followed by low-pass filters in a charge pump configuration. The graph consists of several time-domain waveforms, each representing a different signal in the circuit.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform plot showing the behavior of digital signals and the resulting analog output over time.

2. **Axes Labels and Units:**
- The horizontal axis represents time (t), although specific units are not provided. The vertical axis shows the logical levels of the digital signals and the voltage level of the analog output.

3. **Overall Behavior and Trends:**
- The signals A and B are digital waveforms with periodic square waves. QA and QB are derived signals from D flip-flops, showing narrower pulses triggered by the rising edges of A and B, respectively. The Vout signal represents the output voltage across the capacitor CP, showing a stepped increase as it integrates the current pulses from the charge pump.

4. **Key Features and Technical Details:**
- The digital signals A and B exhibit periodic square wave patterns. QA and QB show narrower pulse widths, indicating the triggering and reset behavior of the PFD.
- The output Vout shows a staircase-like increase, indicating charge accumulation over time. This behavior is typical of a charge pump circuit, where the output voltage increases in discrete steps when one of the switches (S1 or S2) is activated.

5. **Annotations and Specific Data Points:**
- There are no specific numerical values or annotations in the graph. The key observation is the relationship between the digital input signals and the resulting analog output, highlighting the integration effect of the charge pump and low-pass filter.

and the loop filter. A charge pump consists of two switched current sources that pump charge into or out of the loop filter according to two logical inputs. Figure 16.28 illustrates a charge pump driven by a PFD and driving a capacitor. The circuit has three states. If $Q_{A}=Q_{B}=0$, then $S_{1}$ and $S_{2}$ are off and $V_{\text {out }}$ remains constant. If $Q_{A}$ is high and $Q_{B}$ is low, then $I_{1}$ charges $C_{P}$. Conversely, if $Q_{A}$ is low and $Q_{B}$ is high, then $I_{2}$ discharges $C_{P}$. Thus, if, for example, $A$ leads $B$, then $Q_{A}$ continues to produce pulses and $V_{\text {out }}$ rises steadily. Called UP and DOWN currents, respectively, $I_{1}$ and $I_{2}$ are nominally equal.

#### Example 16.9

What is the effect of the narrow pulses that appear in the $Q_{B}$ waveform in Fig. 16.28?

#### Solution

Since $Q_{A}$ and $Q_{B}$ are simultaneously high for a finite period (approximately 5 gate delays from Example 16.8), the current supplied by the charge pump to $C_{P}$ is affected. In fact, if $I_{1}=I_{2}$, the current through $S_{1}$ simply flows through $S_{2}$ during the narrow reset pulse, leaving no current to charge $C_{P}$. As shown in Fig. 16.29, $V_{\text {out }}$ remains constant after $Q_{B}$ goes high.
image_name:Figure 16.29
description:The graph in Figure 16.29 is a time-domain waveform chart that shows the behavior of signals A, B, Q_A, Q_B, and V_out over time. The horizontal axis represents time \( t \), but no specific time units are provided. The vertical axis represents the states of the signals, which are binary (high or low).

1. **Signal A**: This waveform starts low, goes high, and then returns to low, forming a rectangular pulse.

2. **Signal B**: This waveform follows a similar pattern to A but remains high for a longer duration before returning to low. It leads to a wider pulse compared to A.

3. **Signal Q_A**: This waveform is derived from the phase comparison between A and B. It starts low, goes high when A is high and B is low, and returns to low when both A and B are high.

4. **Signal Q_B**: This waveform shows narrow pulses that occur when both A and B are high, indicating a reset condition in the phase detector logic.

5. **V_out**: This waveform starts at a low level, rises steadily during the duration when Q_A is high and Q_B is low, and then remains constant when Q_B goes high. This reflects the charging behavior of a capacitor \( C_P \) in the charge pump circuit, where the current flow is interrupted during the narrow pulses of Q_B, causing V_out to plateau.

Overall, the graph illustrates the interaction between phase detector signals and the resulting output voltage behavior in a phase-locked loop (PLL) system. The key feature is the steady rise of V_out when Q_A is active, which is halted during the reset pulses of Q_B, demonstrating the charge pump's influence on the output voltage.

The PFD/CP/LPF cascade shown in Fig. 16.28 has an interesting property. If $A$, say, leads $B$ by a finite amount, $Q_{A}$ produces pulses indefinitely, allowing the charge pump to inject $I_{1}$ into $C_{P}$ and forcing $V_{\text {out }}$ to rise steadily. In other words, for a finite input error, the output eventually goes to $+\infty$ or $-\infty$, i.e., the "gain" of the circuit is infinity. In this cascade, the PFD converts the input phase error to a pulse width on $Q_{A}$ or $Q_{B}$, the charge pump translates this pulse width to charge, and the capacitor accumulates this charge.

### 16.2.4 Basic Charge-Pump PLL

Let us now construct a PLL using the circuit of Fig. 16.28. Shown in Fig. 16.30 and called a charge-pump PLL, such an implementation senses the transitions at the input and output, detects phase or frequency differences, and activates the charge pump accordingly. When the loop is turned on, $\omega_{\text {out }}$ may be far from $\omega_{\text {in }}$, and the PFD and the charge pump adjust the control voltage such that $\omega_{\text {out }}$ approaches $\omega_{\text {in }}$. When the input and output frequencies are sufficiently close, the PFD operates as a phase detector, performing phase lock. The loop locks when the phase difference drops to zero and the charge pump remains relatively idle.

As observed above, the gain of the PFD/CP/LPF combination is infinite, i.e., a nonzero (deterministic) difference between $\phi_{\text {in }}$ and $\phi_{\text {out }}$ leads to indefinite charge buildup on $C_{P}$. What is the consequence of this attribute in a charge-pump PLL? When the loop of Fig. 16.30 is locked, $V_{\text {cont }}$ is finite. Therefore, the input phase error must be exactly zero. ${ }^{9}$ This is in contrast to the behavior of the type I PLL, in which the phase error is finite and a function of the output frequency.

image_name:Figure 16.30 Simple charge-pump PLL
description:
[
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: QA}
name: I2, type: CurrentSource, value: I2, ports: {Np: QB, Nn: GND}
name: CP, type: Capacitor, value: CP, ports: {Np: Vcont, Nn: GND}
name: VCO, type: Other, ports: {N1: Vcont, N2: Vout}
name: S1, type: Switch, ports: {N1: QA, N2: Vcont}
name: S2, type: Switch, ports: {N1: QB, N2: Vcont}
]
extrainfo:The circuit is a simple charge-pump Phase-Locked Loop (PLL) containing a phase frequency detector, charge pump, and voltage-controlled oscillator (VCO). The input phase is compared to the output phase to control the VCO frequency.

To gain more insight into the operation of the PLL shown in Fig. 16.30, let us ignore the narrow reset pulses on $Q_{A}$ and $Q_{B}$ and assume that after $\phi_{\text {out }}-\phi_{\text {in }}$ drops to zero, the PFD simply produces $Q_{A}=Q_{B}=0$. The charge pump thus remains idle, and $C_{P}$ sustains a constant control voltage. Does this mean that the PFD and the CP are no longer needed?! If $V_{\text {cont }}$ remains constant for a long time, the VCO frequency and phase begin to drift. In particular, the noise sources in the VCO create random variations in the oscillation frequency that can result in a large accumulation of phase error. The PFD then detects the phase difference, producing a corrective pulse on $Q_{A}$ or $Q_{B}$ that adjusts the VCO frequency through the charge pump and the filter. This is why we stated earlier that the PLL responds only to the excess phase of waveforms. We also note that, since in Fig. 16.30 phase comparison is performed in every cycle, the VCO phase and frequency cannot drift substantially.

Dynamics of CPPLL In order to quantify the behavior of charge-pump PLLs, we develop a linear model for the combination of the PFD, the charge pump, and the low-pass filter, thereby obtaining the transfer function. We raise two questions: (1) Is the PFD/CP/LPF combination in Fig. 16.28 a linear system? (2) If so, how can its transfer function be computed?

To answer the first question, we test the system for linearity. For example, as illustrated in Fig. 16.31(a), we double the input phase difference and see if $V_{\text {out }}$ exactly doubles. Interestingly, the flat sections of $V_{\text {out }}$ double, but not the ramp sections. After all, the current charging or discharging $C_{P}$ is constant, yielding a constant slope for the ramp-an effect similar to slewing in op amps. Thus, the system is not linear in the strict sense. To overcome this quandary, we approximate the output waveform by a ramp [Fig. 16.31(b)], arriving at a linear relationship between $V_{\text {out }}$ and $\Delta \phi$. In a sense, we approximate a discrete-time system by a continuous-time model.

To answer the second question, we recall that the transfer function is the Laplace transform of the impulse response, requiring that we apply a phase difference impulse and compute $V_{\text {out }}$ in the time domain. Since a phase difference impulse is difficult to visualize, we apply a phase difference step, obtain $V_{\text {out }}$, and differentiate the result with respect to time.

Let us assume that the input period is $T_{i n}$ and the charge pump provides a current of $\pm I_{P}$ to the capacitor. As shown in Fig. 16.32, we begin with a zero phase difference and, at $t=0$, step the phase of $B$ by $\phi_{0}$, i.e., $\Delta \phi=\phi_{0} u(t)$. As a result, $Q_{A}$ or $Q_{B}$ continues to produce pulses that are $\phi_{0} T_{i n} /(2 \pi)$ seconds wide, raising the output voltage by $\left(I_{P} / C_{P}\right) \phi_{0} T_{i n} /(2 \pi)$ in every period. ${ }^{10}$ Approximated by a ramp, $V_{\text {out }}$ thus exhibits a slope of $\left(I_{P} / C_{P}\right) \phi_{0} /(2 \pi)$ and can be expressed as

$$
\begin{equation*}
V_{\text {out }}(t)=\frac{I_{P}}{2 \pi C_{P}} t \cdot \phi_{0} u(t) \tag{16.37}
\end{equation*}
$$

image_name:(a)
description:The graph labeled as Figure 16.31 (a) depicts the test of linearity for a PFD/CP/LPF combination. The graph is a time-domain waveform showing two pulse signals, labeled A and B, and the resultant output voltage, \( V_{out} \), over time \( t \).

1. **Type of Graph and Function:**
- The graph is a time-domain waveform illustrating the linearity test of a Phase Frequency Detector (PFD) with a Charge Pump (CP) and a Low Pass Filter (LPF).

2. **Axes Labels and Units:**
- The horizontal axis represents time \( t \), though specific units are not provided. The vertical axis represents the output voltage \( V_{out} \).

3. **Overall Behavior and Trends:**
- The pulse signals A and B are square waves with a phase difference \( \Delta \phi \). The output \( V_{out} \) is shown as a staircase waveform, indicating discrete steps in voltage over time.
- The graph on the left shows a smaller phase difference \( \Delta \phi \) between A and B, resulting in smaller voltage steps in \( V_{out} \).
- The graph on the right shows a larger phase difference \( 2\Delta \phi \), leading to larger voltage steps in \( V_{out} \).

4. **Key Features and Technical Details:**
- The staircase nature of \( V_{out} \) suggests that the system responds to the phase difference by adjusting the output voltage in discrete increments.
- The step size in \( V_{out} \) is proportional to the phase difference between the signals A and B.

5. **Annotations and Specific Data Points:**
- The phase differences \( \Delta \phi \) and \( 2\Delta \phi \) are annotated between the rising edges of signals A and B.
- The graph illustrates the linear relationship between the phase difference and the output voltage increment, demonstrating the linearity of the PFD/CP/LPF combination.
image_name:(b)
description:The graph labeled as "(b)" in the image is a time-domain waveform illustrating the ramp approximation of the response from a Phase Frequency Detector (PFD), Charge Pump (CP), and Loop Filter (LPF) combination.

Type of Graph and Function
- **Type:** Time-domain waveform
- **Function:** Ramp approximation of the output voltage response

Axes Labels and Units
- **X-axis (Horizontal):** Time \( t \)
- **Y-axis (Vertical):** Output Voltage \( V_{out} \)
- **Scale:** Linear

Overall Behavior and Trends
- The graph represents a piecewise linear waveform, where the output voltage \( V_{out} \) increases in discrete steps over time.
- The waveform exhibits a consistent upward trend, indicating a positive slope that approximates a continuous ramp.

Key Features and Technical Details
- The waveform consists of a series of linear segments, each with a small, constant positive slope.
- The dotted line in the graph represents the ideal continuous ramp that the stepwise waveform approximates.
- The slope of the dotted line corresponds to the expression \( \frac{I_{P}}{2 \pi C_{P}} \phi_{0} \), indicating the rate of change of \( V_{out} \) with respect to time.

Annotations and Specific Data Points
- The graph does not include specific numerical values or annotations for key data points, but the dotted line serves as a reference for the ideal ramp behavior.
- The stepwise nature of the waveform implies the presence of discrete pulses from the PFD/CP combination that contribute to the incremental increases in \( V_{out} \).

Figure 16.31 (a) Test of linearity of PFD/CP/LPF combination; (b) ramp approximation of the response.
image_name:Figure 16.32 Step response of PFD/CP/LPF combination.
description:The graph in Figure 16.31 (a) is a time-domain waveform illustrating the behavior of a Phase Frequency Detector (PFD), Charge Pump (CP), and Low Pass Filter (LPF) combination. The horizontal axis represents time \( t \), with no specific units or numerical values provided, while the vertical axis represents various signals involved in the system.

Graph Components:
1. **Waveforms A and B:**
- These are square wave signals with a period denoted as \( T_{in} \). They are shown as alternating high and low states, typical of digital clock signals.
- The phase difference between these signals is indicated as \( \phi_0 \).

2. **Signal \( Q_A \):**
- This signal is a digital output from the PFD, which appears to be a pulse train synchronized with the rising edges of waveform A.

3. **Output Voltage \( V_{out} \):**
- This is the main output of the PFD/CP/LPF combination. It is depicted as a stepwise increasing function over time.
- The stepwise nature indicates the presence of discrete pulses from the PFD/CP combination, causing incremental increases in \( V_{out} \).
- A dotted line is included as a reference, showing the ideal ramp behavior. This line has a slope of \( \frac{I_P}{2\pi C_P} \phi_0 \), indicating the expected linear increase in the absence of discrete steps.

Overall Behavior and Trends:
- The graph shows how the PFD/CP/LPF combination attempts to approximate a linear ramp response. The actual output, \( V_{out} \), increases in a stepwise fashion, reflecting the discrete nature of the pulses from the charge pump.
- The dotted line serves as a reference for the ideal continuous ramp, highlighting the deviation of the actual output due to the discrete pulses.

Key Features:
- The phase difference \( \phi_0 \) between waveforms A and B is crucial for determining the behavior of \( V_{out} \).
- The slope of the dotted line \( \frac{I_P}{2\pi C_P} \phi_0 \) represents the ideal linear increase in the output voltage, which the stepwise \( V_{out} \) aims to approximate.

The impulse response is therefore given by

$$
\begin{equation*}
h(t)=\frac{I_{P}}{2 \pi C_{P}} u(t) \tag{16.38}
\end{equation*}
$$

yielding the transfer function

$$
\begin{equation*}
\frac{V_{\text {out }}}{\Delta \phi}(s)=\frac{I_{P}}{2 \pi C_{P}} \cdot \frac{1}{s} \tag{16.39}
\end{equation*}
$$

Consequently, the PFD/CP/LPF combination contains a pole at the origin, a point of contrast to the $\mathrm{PD} / \mathrm{LPF}$ circuit used in the type I PLL. In analogy with the expression $K_{V C O} / s$, we call $I_{P} /\left(2 \pi C_{P}\right)$ the "gain" of the PFD and denote it by $K_{P F D}$.

#### Example 16.10

Suppose the output quantity of interest in the circuit of Fig. 16.28 is the current injected by the charge pump into the capacitor. Determine the transfer function from $\Delta \phi$ to this current, $I_{\text {out }}$.

#### Solution

Since $V_{\text {out }}(s)=I_{\text {out }} /\left(C_{P} s\right)$, we have

$$
\begin{equation*}
\frac{I_{\text {out }}}{\Delta \phi}(s)=\frac{I_{P}}{2 \pi} \tag{16.40}
\end{equation*}
$$

Let us now construct a linear model of charge-pump PLLs. Shown in Fig. 16.33, the model gives an open-loop transfer function

$$
\begin{equation*}
\left.\frac{\Phi_{\text {out }}}{\Phi_{\text {in }}}(s)\right|_{\mathrm{open}}=\frac{I_{P}}{2 \pi C_{P}} \frac{K_{V C O}}{s^{2}} \tag{16.41}
\end{equation*}
$$

Since the loop gain has two poles at the origin, this topology is called a "type II" PLL. The closed-loop transfer function, denoted by $H(s)$ for the sake of brevity, is thus equal to

$$
\begin{equation*}
H(s)=\frac{\frac{I_{P} K_{V C O}}{2 \pi C_{P}}}{s^{2}+\frac{I_{P} K_{V C O}}{2 \pi C_{P}}} \tag{16.42}
\end{equation*}
$$

This result is alarming because the closed-loop system contains two imaginary poles at $s_{1,2}=$ $\pm j \sqrt{I_{P} K_{V C O} /\left(2 \pi C_{P}\right)}$ and is therefore unstable. The instability arises because the loop gain has only two poles at the origin (i.e., two ideal integrators). As shown in Fig. 16.34(a), each integrator contributes a constant phase shift of $90^{\circ}$, allowing the system to oscillate at the gain crossover frequency.
image_name:Figure 16.33 Linear model of simple charge-pump PLL
description:The block diagram represents a simple charge-pump Phase-Locked Loop (PLL) system, composed of several key components:

1. **Main Components:**
- **Phase Frequency Detector (PFD):** This block receives the input phase signal \( \phi_{in} \) and the feedback signal from the output \( \phi_{out} \). It compares these two signals and produces an error signal that indicates the phase difference.
- **Charge Pump (CP) and Loop Filter (LPF):** The error signal from the PFD is fed into the charge pump and loop filter. The LPF is represented by the transfer function \( \frac{I_P}{2\pi C_P} \frac{1}{s} \), which indicates an integration function with a proportionality constant. This block converts the phase error into a control voltage.
- **Voltage-Controlled Oscillator (VCO):** This block is represented by the transfer function \( \frac{K_{VCO}}{s} \), indicating that it integrates the control voltage to produce the output frequency. The output phase \( \phi_{out} \) is fed back to the PFD for comparison.

2. **Flow of Information or Control:**
- The input phase \( \phi_{in} \) is compared with the feedback phase \( \phi_{out} \) in the PFD.
- The resulting error signal is processed by the CP and LPF to generate a control voltage.
- This control voltage adjusts the frequency of the VCO, thus controlling the output phase \( \phi_{out} \).
- The output phase is fed back to the PFD, creating a closed-loop control system.

3. **Labels, Annotations, and Key Indicators:**
- \( \phi_{in} \) and \( \phi_{out} \) are the input and output phase signals, respectively.
- The transfer functions \( \frac{I_P}{2\pi C_P} \frac{1}{s} \) and \( \frac{K_{VCO}}{s} \) indicate the integration characteristics of the LPF and VCO.

4. **Overall System Function:**
- The primary function of this PLL system is to synchronize the output phase \( \phi_{out} \) with the input phase \( \phi_{in} \) by adjusting the VCO frequency based on the phase difference. The loop aims to minimize the phase error, thereby achieving phase lock between the input and output signals.

Figure 16.33 Linear model of simple charge-pump PLL.
In order to stabilize the system, we must modify the phase characteristic such that the phase shift is less than $180^{\circ}$ at the gain crossover. As shown in Fig. 16.34(b), this is accomplished by introducing a zero in the loop gain, i.e., by adding a resistor in series with the loop filter capacitor (Fig. 16.35). Using the result of Example 16.10, the reader can prove (Problem 16.11) that the PFD/CP/LPF now has a transfer function

$$
\begin{equation*}
\frac{V_{\text {out }}}{\Delta \phi}(s)=\frac{I_{P}}{2 \pi}\left(R_{P}+\frac{1}{C_{P} S}\right) \tag{16.43}
\end{equation*}
$$

It follows that the PLL open-loop transfer function is equal to

$$
\begin{equation*}
\left.\frac{\Phi_{\text {out }}}{\Phi_{\text {in }}}(s)\right|_{\text {open }}=\frac{I_{P}}{2 \pi}\left(R_{P}+\frac{1}{C_{P} s}\right) \frac{K_{V C O}}{s} \tag{16.44}
\end{equation*}
$$

image_name:Figure 16.34 (a)
description:The graph in Figure 16.34 (a) is a Bode plot representing the loop gain characteristics of a simple charge-pump PLL. This plot consists of two separate graphs: the magnitude plot and the phase plot.

1. **Magnitude Plot:**
- **Type:** Logarithmic scale Bode plot.
- **Axes:**
- The horizontal axis represents the logarithm of angular frequency (log \( \omega \)).
- The vertical axis represents the magnitude of the open-loop gain expressed in decibels (20 log |\( H_{\text{open}} \)|).
- **Behavior:**
- The plot starts at 0 dB and decreases linearly with a slope of \(-40 \text{ dB/decade}\).
- **Key Features:**
- The consistent slope indicates a second-order system behavior, which is typical for a charge-pump PLL without additional zeros or poles.

2. **Phase Plot:**
- **Type:** Logarithmic scale Bode plot.
- **Axes:**
- The horizontal axis is the same as the magnitude plot, log \( \omega \).
- The vertical axis represents the phase angle of the open-loop transfer function (\( \angle H_{\text{open}} \)) in degrees.
- **Behavior:**
- The phase is constant at \(-180^{\circ}\) across all frequencies shown.
- **Key Features:**
- The constant phase of \(-180^{\circ}\) suggests that there is no phase lead or lag introduced by zeros or additional poles in this frequency range.

Overall, this Bode plot indicates a basic second-order system with a consistent phase lag and a magnitude slope characteristic of a simple charge-pump PLL without any additional compensatory elements like zeros or poles.
image_name:Figure 16.34 (b)
description:Figure 16.34 (b) is a Bode plot, which illustrates the loop gain characteristics of a charge-pump PLL with the addition of a zero. The graph is divided into two sections: the magnitude plot at the top and the phase plot at the bottom.

**Magnitude Plot:**
- **Vertical Axis:** Represents the magnitude of the open-loop gain in decibels (dB), denoted as \(20\log|H_{\text{open}}|\).
- **Horizontal Axis:** Represents the logarithm of angular frequency \(\log \omega\).
- **Behavior:** The plot shows an initial slope of -40 dB/decade, indicating a steep decrease in gain. After the introduction of the zero, the slope reduces to -20 dB/decade, showing a less steep decline.

**Phase Plot:**
- **Vertical Axis:** Represents the phase of the open-loop gain in degrees, denoted as \(\angle H_{\text{open}}\).
- **Horizontal Axis:** Also represents the logarithm of angular frequency \(\log \omega\).
- **Behavior:** The phase starts at -180°. With the addition of the zero, the phase begins to increase, moving through -135° and approaching -90° as the frequency increases.

**Key Features:**
- The introduction of the zero is evident in both the magnitude and phase plots, as it reduces the slope of the magnitude plot and causes an upward shift in the phase plot.
- This adjustment in the Bode plot indicates improved stability and phase margin in the PLL system.

Figure 16.34 (a) Loop gain characteristics of simple charge-pump PLL; (b) addition of zero.

image_name:Figure 16.35
description:The circuit is a charge-pump phase-locked loop (PLL) featuring two flip-flops, two current sources, two switches, a resistor, a capacitor, and a voltage-controlled oscillator (VCO). The circuit is designed to stabilize the output frequency by adjusting the control voltage at node X, which is influenced by the charge-pump action of I1, I2, S1, and S2.

and hence

$$
\begin{equation*}
H(s)=\frac{\frac{I_{P} K_{V C O}}{2 \pi C_{P}}\left(R_{P} C_{P} s+1\right)}{s^{2}+\frac{I_{P}}{2 \pi} K_{V C O} R_{P} s+\frac{I_{P}}{2 \pi C_{P}} K_{V C O}} \tag{16.45}
\end{equation*}
$$

The closed-loop system contains a zero at $s_{z}=-1 /\left(R_{P} C_{P}\right)$. Using the same notation as that for the type I PLL, we have

$$
\begin{align*}
\omega_{n} & =\sqrt{\frac{I_{P} K_{V C O}}{2 \pi C_{P}}}  \tag{16.46}\\
\zeta & =\frac{R_{P}}{2} \sqrt{\frac{I_{P} C_{P} K_{V C O}}{2 \pi}} \tag{16.47}
\end{align*}
$$

As expected, if $R_{P}=0$, then $\zeta=0$. With complex poles, the decay time constant is given by $1 /\left(\zeta \omega_{n}\right)=$ $4 \pi /\left(R_{P} I_{P} K_{V C O}\right)$.

Stability Issues The stability behavior of type II PLLs is quite different from that of type I PLLs. We begin the analysis with the Bode plots of the loop gain (the loop transmission) [Eq. (16.44)]. Shown in Fig. 16.36, these plots suggest that if $I_{P} K_{V C O}$ decreases, the gain crossover frequency moves toward the origin, degrading the phase margin. Predicted by (16.47), this trend is in sharp contrast to that expressed by (16.18) and illustrated in Fig. 16.19.
image_name:Figure 16.36
description:The graph in Figure 16.36 is a Bode plot, which consists of two separate plots: a magnitude plot (top) and a phase plot (bottom). Both plots are used to analyze the stability of a charge-pump Phase-Locked Loop (PLL) as the product of $I_{P}$ and $K_{VCO}$ changes.

**Magnitude Plot (Top):**
- **Y-Axis:** Represents the magnitude of the open-loop gain in decibels (dB), denoted as $20\log|H_{open}|$.
- **X-Axis:** Represents the frequency in logarithmic scale, denoted as $\log \omega$.
- **Behavior:** The magnitude plot shows a decreasing trend with a noticeable slope change at a certain frequency, $\omega_1$.
- **Trend:** As $I_{P} K_{VCO}$ decreases, the gain crossover frequency shifts towards the origin, indicating a reduction in phase margin and potentially leading to stability issues. This is illustrated by the comparison between the initial curve and the lower $I_{P} K_{VCO}$ curve, which is shown in a lighter shade.

**Phase Plot (Bottom):**
- **Y-Axis:** Represents the phase of the open-loop gain in degrees, denoted as $\angle H_{open}$.
- **X-Axis:** Also represents the frequency in logarithmic scale, denoted as $\log \omega$.
- **Behavior:** The phase plot begins at 0 degrees and decreases, showing a dip towards -180 degrees.
- **Key Points:** The phase crosses -90 degrees and approaches -180 degrees, which are critical for assessing the phase margin and stability of the system.

**Annotations and Specific Data Points:**
- The point $\omega_1$ is marked on the magnitude plot, indicating a significant frequency where the slope of the magnitude changes.
- The graph highlights the effect of a lower $I_{P} K_{VCO}$ by showing a shift in the curves, emphasizing the degradation of stability as phase margin decreases.

It is also possible to construct the root locus of the closed-loop system in the complex plane. For $I_{P} K_{V C O}=0$ (e.g., $I_{P}=0$ ), the loop is open and both poles lie at the origin. For $I_{P} K_{V C O}>0$, we have $s_{1,2}=-\zeta \omega_{n} \pm \omega_{n} \sqrt{\zeta^{2}-1}$, and, since $\zeta \propto \sqrt{I_{P} K_{V C O}}$, the poles are complex if $I_{P} K_{V C O}$ is small. The reader can prove (Problem 16.14) that as $I_{P} K_{V C O}$ increases, $s_{1}$ and $s_{2}$ move on a circle centered at $\sigma=-1 /\left(R_{P} C_{P}\right)$ with a radius $1 /\left(R_{P} C_{P}\right)$ (Fig. 16.37). The poles return to the real axis at $\zeta=1$, assuming a value of $-2 /\left(R_{P} C_{P}\right)$. For $\zeta>1$, the poles remain real, one approaching $-1 /\left(R_{P} C_{P}\right)$ and the other going to $-\infty$ as $I_{P} K_{V C O} \rightarrow+\infty$. Since for complex $s_{1}$ and $s_{2}, \zeta=\cos \psi$, we observe that as $I_{P} K_{V C O}$ exceeds zero, the system becomes more stable.
image_name:Figure 16.37 Root locus of type II PLL
description:The graph depicted is a root locus plot for a type II Phase-Locked Loop (PLL) system. The plot is shown in the complex plane with the horizontal axis labeled as \( \sigma \) (real part) and the vertical axis labeled as \( j\omega \) (imaginary part).

Key Features:
1. **Axes and Units:**
- The \( \sigma \) axis is marked with key values \( -\frac{1}{R_PC_P} \) and \( -\frac{2}{R_PC_P} \), indicating the real parts of the poles.
- The \( j\omega \) axis represents the imaginary component of the complex plane, typical in root locus plots.

2. **Overall Behavior and Trends:**
- The root locus begins at \( \sigma = -\frac{1}{R_PC_P} \) on the real axis and forms a semicircular path in the left half of the complex plane.
- The semicircle has a radius of \( \frac{1}{R_PC_P} \) and is centered at \( \sigma = -\frac{1}{R_PC_P} \).
- As \( \zeta \) (damping ratio) increases, the poles move along the semicircular path.
- The poles return to the real axis at \( \zeta = 1 \), reaching the point \( \sigma = -\frac{2}{R_PC_P} \).

3. **Trends for \( \zeta > 1 \):**
- For values of \( \zeta \) greater than 1, the poles remain on the real axis.
- One pole approaches \( \sigma = -\frac{1}{R_PC_P} \) while the other moves towards negative infinity as \( I_P K_{VCO} \) increases indefinitely.

4. **Annotations and Specific Data Points:**
- The plot includes a dashed line indicating the angle \( \phi \), which corresponds to the angle of the poles when they are complex conjugates.
- The arrows on the plot indicate the direction of movement of the poles as the system parameter \( I_P K_{VCO} \) changes.

This root locus demonstrates the stability characteristics of a type II PLL, showing how the poles migrate in the complex plane as system parameters vary, crucial for understanding the system's response to different damping ratios and gain values.

#### Example 16.11

A student considers the Bode plots in Fig. 16.36 and observes that at $\omega_{1}$, the loop gain exceeds unity and the phase shift is $-180^{\circ}$. The student then reasons that the PLL must oscillate at this frequency! Explain the flaw in this reasoning.

#### Solution

The phase shift is in fact slightly less than zero unless $\omega_{1}=0$. As explained using Nyquist's approach in Chapter 10, a system containing two integrators and one zero does not oscillate.

The compensated type II PLL of Fig. 16.35 suffers from a critical drawback. Since the charge pump drives the series combination of $R_{P}$ and $C_{P}$, each time a current is injected into the loop filter, the control voltage experiences a large jump. Even in the locked condition, the mismatches between $I_{1}$ and $I_{2}$ and the charge injection and clock feedthrough of $S_{1}$ and $S_{2}$ introduce voltage jumps in $V_{\text {cont }}$. The resulting ripple severely disturbs the VCO, corrupting the output phase. To relax this issue, a second capacitor is usually added in parallel with $R_{P}$ and $C_{P}$ (Fig. 16.38), suppressing the initial step. The loop filter now is of second order, yielding a third-order PLL and creating stability difficulties [4]. Nonetheless, if $C_{2}$ is about one-fifth to one-tenth of $C_{P}$, the closed-loop time and frequency responses remain relatively unchanged.
image_name:Figure 16.38
description:The circuit is a phase-locked loop (PLL) with a third-order loop filter for improved stability. It uses two current sources (I1 and I2) and two switches (S1 and S2) to control the voltage across RP, CP, and C2, which in turn controls the VCO output.

Figure 16.38 Addition of $C_{2}$ to reduce ripple on the control line.
Equation (16.47) implies that the loop becomes more stable as $R_{P}$ increases. In reality, as $R_{P}$ becomes very large, the stability degrades again. This effect is not predicted by the foregoing derivations because we have approximated the discrete-time system by a continuous-time loop. A more accurate analysis is given in [2], but simulations are often necessary to determine the stability bounds of CPPLLs.

## 16.3 ■ Nonideal Effects in PLLs

### 16.3.1 PFD/CP Nonidealities

Several imperfections in the PFD/CP circuit lead to high ripple on the control voltage even when the loop is locked. As mentioned earlier, the ripple modulates the VCO frequency, producing a waveform that is no longer periodic. In this section, we study these nonidealities.

The PFD implementation of Fig. 16.24(a) generates narrow, coincident pulses on both $Q_{A}$ and $Q_{B}$ even when the input phase difference is zero. As illustrated in Fig. 16.39, if $A$ and $B$ rise simultaneously, so do $Q_{A}$ and $Q_{B}$, thereby activating the reset. That is, even when the PLL is locked, $Q_{A}$ and $Q_{B}$ simultaneously turn on the charge pump for a finite period $T_{P} \approx 5 T_{D}$, where $T_{D}$ denotes the gate delay (Example 16.8).

What are the consequences of the reset pulses on $Q_{A}$ and $Q_{B}$ ? To understand why these pulses are desirable, we consider a hypothetical PFD that produces no pulses for a zero input phase difference [Fig. 16.40(a)]. How does such a PFD respond to a small phase error? As shown in Fig. 16.40(b), the circuit generates very narrow pulses on $Q_{A}$ or $Q_{B}$. However, owing to the finite rise time and fall time resulting from the capacitance seen at these nodes, the pulse may not find enough time to reach a logical high level fail to turn on the charge pump switches. In other words, if the input phase difference, $\Delta \phi$, falls below a certain value $\phi_{0}$, then the output voltage of the PFD/CP/LPF combination is no longer a
image_name:Figure 16.39
description:The graph in Figure 16.39 is a time-domain waveform illustrating the output of a Phase Frequency Detector (PFD) with zero phase difference. The graph consists of four distinct waveforms labeled A, B, Q_A, and Q_B, plotted against time (t) on the horizontal axis.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph depicting digital signals over time.

2. **Axes Labels and Units:**
- The horizontal axis represents time (t), though specific units are not provided. The vertical axis represents the logical state of the signals, typically high or low (binary states).

3. **Overall Behavior and Trends:**
- **Waveforms A and B:** These two waveforms are identical, consisting of square waves with equal high and low durations, indicating zero phase difference between them.
- **Waveforms Q_A and Q_B:** These are narrow pulse waveforms generated as a result of the PFD operation. Each pulse corresponds to the edges of the square waves A and B.

4. **Key Features and Technical Details:**
- **Coincident Pulses:** Both Q_A and Q_B generate pulses simultaneously due to the zero phase difference between A and B.
- **Pulse Width (T_P):** The pulse width is denoted as T_P, which is very narrow, reflecting the precision of the PFD in detecting phase differences.

5. **Annotations and Specific Data Points:**
- The pulse width T_P is annotated between the pulses of Q_A, indicating a critical parameter for understanding pulse generation in the PFD.
- No specific numerical values are provided for the pulse width or timing.

This graph effectively demonstrates the operation of a PFD under conditions of zero phase difference, where coincident pulses are generated on both Q_A and Q_B outputs, highlighting the precision and timing characteristics of the circuit.

Figure 16.39 Coincident pulses generated by PFD with zero phase difference.

image_name:Figure 16.40
description:Figure 16.40 presents two sets of time-domain waveforms illustrating the output of a hypothetical Phase Detector (PD) under different input phase conditions. The graph is divided into two parts, labeled (a) and (b), each showing four waveforms aligned vertically, plotted against time (t) on the horizontal axis.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform plot, showing the behavior of signals over time.

2. **Axes Labels and Units:**
- The horizontal axis represents time (t), though no specific units are provided.
- There are no explicit labels or units provided for the vertical axis, but it represents signal levels or states.

3. **Overall Behavior and Trends:**
- **(a) Zero Input Phase Difference:**
- Waveforms A and B are identical square waves, indicating zero phase difference.
- Outputs Q_A and Q_B are flat lines at zero, showing no pulse generation due to the lack of phase difference.
- **(b) Small Input Phase Difference:**
- Waveforms A and B are square waves with a slight phase difference, where A leads B.
- Output Q_A shows periodic pulses, indicating the detection of a phase difference.
- Q_B remains a flat line, suggesting no pulse generation or a different response to the phase difference.

4. **Key Features and Technical Details:**
- In (a), the lack of pulses in Q_A and Q_B highlights the PD's behavior under zero phase difference.
- In (b), the pulses in Q_A are marked with dashed lines, illustrating the effect of a small phase difference.
- The periodicity of the pulses in Q_A corresponds to the timing difference between A and B.

5. **Annotations and Specific Data Points:**
- There are no specific numerical markers or annotations provided in the graph.
- The dashed lines in (b) emphasize the presence of pulses in Q_A, correlating with the phase difference between A and B.

Figure 16.40 Output waveforms of a hypothetical PD with (a) zero input phase difference, and (b) a small input phase difference.
function of $\Delta \phi$. Since, as depicted in Fig. 16.41, for $|\Delta \phi|<\phi_{0}$ the charge pump injects no current, Eq. (16.41) implies that the loop gain drops to zero and the output phase is not locked. We say that the PFD/CP circuit suffers from a dead zone equal to $\pm \phi_{0}$ around $\Delta \phi=0$.
image_name:Figure 16.41 Dead zone in the charge pump current
description:The graph depicted in Figure 16.41 is a plot of charge pump current versus phase difference (Δφ). The x-axis represents the phase difference (Δφ), while the y-axis represents the charge pump current, with positive and negative current values denoted as +I_P and -I_P respectively.

The graph is a piecewise function showing a dead zone around the origin. In this dead zone, between -φ₀ and φ₀ on the x-axis, the charge pump current remains at zero, indicating no current is injected by the charge pump. This flat region signifies the dead zone where the phase detector and charge pump do not respond to small phase differences.

Outside of the dead zone, the graph shows a sharp transition in current. As Δφ becomes greater than φ₀, the charge pump current jumps to a positive value, +I_P. Conversely, when Δφ is less than -φ₀, the current drops to a negative value, -I_P. This behavior indicates that the charge pump actively injects current to correct phase differences outside the dead zone.

The overall shape of the graph is similar to a step function with a flat section (dead zone) in the middle and steep transitions to constant positive and negative current values beyond the thresholds of -φ₀ and φ₀. These transitions are marked by dashed lines at -φ₀ and φ₀, highlighting the boundaries of the dead zone. This graph illustrates the undesired effect of the dead zone in phase-locked loop circuits, where no corrective action is taken for small phase errors, potentially leading to jitter in the system.

Figure 16.41 Dead zone in the chargepump current.

The dead zone is highly undesirable because it allows the VCO to accumulate as much random phase error as $\phi_{0}$ with respect to the input while receiving no corrective feedback. Thus, as illustrated in Fig. 16.42, the zero crossing points of the VCO output experience substantial random variations, an effect called "jitter."

Interestingly, the coincident pulses on $Q_{A}$ and $Q_{B}$ can eliminate the dead zone. This is because, for $\Delta \phi=0$, the pulses always turn on the charge pump if they are sufficiently wide. Consequently, as shown in Fig. 16.43, an infinitesimal increment in the phase difference results in a proportional increase in the net current produced by the charge pump. In other words, the dead zone vanishes if $T_{P}$ is long enough to allow $Q_{A}$ and $Q_{B}$ to reach a valid logical level and turn on the switches in the charge pump.
image_name:Figure 16.42 Jitter resulting from the dead zone
description:The graph depicted in Figure 16.42 illustrates the effect of jitter resulting from the dead zone in a phase-locked loop (PLL) system. It is a time-domain waveform graph that compares the input signal with the output of a Voltage-Controlled Oscillator (VCO).

1. **Type of Graph and Function:**
- The graph is a time-domain waveform showing two digital square wave signals.

2. **Axes Labels and Units:**
- The x-axis represents time, denoted as \( t \). The scale is linear.
- There are no specific units or numerical values marked on the x-axis.
- The y-axis is not explicitly labeled with units but represents the logical states (high and low) of the digital signals.

3. **Overall Behavior and Trends:**
- The graph shows two square wave signals: the "Input" and the "VCO Output."
- Both signals have a similar frequency, but there is a noticeable phase difference between them.
- The VCO Output signal lags behind the Input signal, as indicated by the horizontal shift between the two waveforms.

4. **Key Features and Technical Details:**
- Vertical dotted lines are drawn to highlight the phase difference between the rising edges of the Input and VCO Output signals.
- The phase difference is consistent across the cycles, indicating a steady state of phase misalignment due to the dead zone.
- This phase misalignment is the cause of jitter in the system.

5. **Annotations and Specific Data Points:**
- The graph does not include any specific numerical annotations or data points, but the consistent phase difference is visually marked by the dotted lines.

This graph visually represents how the dead zone in the PLL affects the synchronization between the input and the VCO output, leading to jitter characterized by a consistent phase lag.

Figure 16.42 Jitter resulting from the dead zone.
image_name:Figure 16.43 Jitter resulting from the dead zone
description:The graph consists of two sets of waveforms, each representing the output signals $Q_A$ and $Q_B$ over time, denoted by $t$. The graph is split into two sections: one where the phase difference $\Delta\phi = 0$ and another where $\Delta\phi \neq 0$.

Type of Graph and Function:
This is a time-domain waveform graph showing the behavior of signals in a phase-locked loop (PLL) system.

Axes Labels and Units:
- **Horizontal Axis:** Time ($t$), though the specific units are not provided, it is typically in seconds or a subunit like milliseconds.
- **Vertical Axis:** Output signals $Q_A$ and $Q_B$, which might represent voltage levels or signal states.

Overall Behavior and Trends:
- **Left Section ($\Delta\phi = 0$):**
- Both $Q_A$ and $Q_B$ show a similar waveform pattern.
- The signals rise sharply, reach a peak, and then decay exponentially.
- The dotted lines indicate a consistent phase or timing difference, suggesting a dead zone effect.

- **Right Section ($\Delta\phi \neq 0$):**
- Both $Q_A$ and $Q_B$ exhibit similar behavior to the left section but with a noticeable phase difference.
- The signals rise and fall in a similar pattern but are slightly shifted in time relative to each other, indicating the presence of jitter.

Key Features and Technical Details:
- The dead zone is visually represented by the dotted lines, showing the phase misalignment.
- The timing period $T_p$ is indicated by a bidirectional arrow, marking the duration of the phase difference.
- The consistent phase lag between $Q_A$ and $Q_B$ is highlighted, illustrating the effect of the dead zone on signal synchronization.

Annotations and Specific Data Points:
- No specific numerical data points are provided, but the dotted lines serve as visual markers for phase misalignment.
- The graph effectively demonstrates how phase misalignment due to the dead zone can lead to jitter in the PLL system.

Figure 16.43 Response of actual PD to a small input phase difference.

While eliminating the dead zone, the reset pulses on $Q_{A}$ and $Q_{B}$ introduce other difficulties. Let us first implement the charge pump using MOS transistors [Fig. 16.44(a)]. Here, $M_{1}$ and $M_{2}$ operate as current sources and $M_{3}$ and $M_{4}$ as switches. The output $Q_{A}$ is inverted so that when it goes high, $M_{4}$ turns on.

The first issue in the circuit of Fig. 16.44(a) stems from the delay difference between $\overline{Q_{A}}$ and $Q_{B}$ in turning on their respective switches. As shown in Fig. 16.44(b), the net current injected by the charge pump into the loop filter jumps to $+I_{P}$ and $-I_{P}$, disturbing the oscillator control voltage periodically even if the loop is locked. To suppress this effect, a complementary pass gate can be interposed between $Q_{B}$ and the gate of $M_{3}$, equalizing the delays [Fig. 16.44(c)].

The second issue in the CP of Fig. 16.44(c) relates to the mismatch between the drain currents of $M_{1}$ and $M_{2}$. As depicted in Fig. 16.45(a), even with perfect alignment of the UP and DOWN pulses, the net current produced by the charge pump is nonzero, changing $V_{\text {cont }}$ by a constant increment at each phase comparison instant. How does the PLL respond to this error? For the loop to remain locked, the average value of the control voltage must remain constant. The PLL therefore creates a phase error between the input and the output such that the net current injected by the CP in every cycle is zero [Fig. 16.45(b)]. The relationship between the current mismatch and the phase error is determined in Problem 16.12. It is important to note that (1) the control voltage still experiences a periodic ripple; (2) owing to the low output impedance of short-channel MOSFETs, the current mismatch varies with the output voltage (i.e., with the VCO frequency); and (3) the clock feedthrough and charge injection mismatch between $M_{3}$ and $M_{4}$ further increase both the phase error and the ripple.

The third issue in the circuit of Fig. 16.44(c) originates from the finite capacitance seen at the drains of the current sources. Suppose, as illustrated in Fig. 16.46(a), $S_{1}$ and $S_{2}$ are off, allowing $M_{1}$ to discharge $X$ to ground and $M_{2}$ to charge $Y$ to $V_{D D}$. At the next phase comparison instant, both $S_{1}$ and $S_{2}$ turn on, $V_{X}$ rises, $V_{Y}$ falls, and $V_{X} \approx V_{Y} \approx V_{\text {cont }}$ if the voltage drop across $S_{1}$ and $S_{2}$ is neglected [Fig. 16.46(b)]. If the phase error is zero and $I_{D 1}=\left|I_{D 2}\right|$, does $V_{\text {cont }}$ remain constant after the switches turn on? Even if $C_{X}=C_{Y}$, the change in $V_{X}$ is not equal to that in $V_{Y}$. For example, if $V_{\text {cont }}$ is relatively high, $V_{X}$ changes by a large amount and $V_{Y}$ by a small amount. The difference between the two changes must therefore be supplied by $C_{P}$, leading to a jump in $V_{\text {cont }}$.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1s3, G: Vb1}
name: M2, type: PMOS, ports: {S: VDD, D: d2s4, G: Vb2}
name: M3, type: NMOS, ports: {S: d1s3, D: Vout, G: QB}
name: M4, type: PMOS, ports: {S: d2s4, D: Vout, G: QA}
name: C, type: Capacitor, value: C, ports: {Np: Vcont, Nn: GND}
name: PFD, type: Other, ports: {N1: A, N2: B, N3: QA, N4: QB}
name: Vb1, type: VoltageSource, value: Vb1, ports: {Np: Vb1, Nn: GND}
name: Vb2, type: VoltageSource, value: Vb2, ports: {Np: Vb2, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a charge pump implementation with phase frequency detector (PFD) and involves NMOS and PMOS transistors for controlling the charge and discharge paths. The PFD outputs QA and QB control the gates of M4 and M3, respectively, affecting the Vout and consequently Vcont. The capacitors and voltage sources provide biasing and power supply.
image_name:(b)
description:The graph in part (b) of the image is a time-domain waveform illustrating the behavior of various signals in a charge pump circuit. The horizontal axis represents time, while the vertical axis represents signal levels or current values.

1. **Type of Graph and Function**:
- The graph is a time-domain waveform showing the timing relationship between signals $Q_A$, $\overline{Q_A}$, $Q_B$, current levels, and the control voltage $V_{cont}$.

2. **Axes Labels and Units**:
- The horizontal axis is labeled "time," though specific units are not provided in the image.
- The vertical axis represents signal levels and current values, with specific signals and currents labeled on different lines.

3. **Overall Behavior and Trends**:
- The waveform begins with signal $Q_A$ rising, followed shortly by $\overline{Q_A}$ and $Q_B$.
- The currents $|I_{D4}|$ and $I_{D3}$ show step-like changes, indicating the switching behavior of the circuit.
- The net current alternates between positive $+I_P$ and negative $-I_P$, depicted by shaded regions, indicating charge and discharge cycles.
- The control voltage $V_{cont}$ exhibits a dip and recovery, reflecting the effect of the net current changes.

4. **Key Features and Technical Details**:
- The delay $T_D$ is marked between the rising edges of $Q_A$ and $\overline{Q_A}$, indicating the skew effect.
- The net current shows distinct positive and negative phases, corresponding to the charge pump operation.
- $V_{cont}$ shows a dip during the negative phase of the net current and recovers during the positive phase.

5. **Annotations and Specific Data Points**:
- The graph highlights the skew $T_D$ between the signals $Q_A$ and $\overline{Q_A}$.
- The transitions in $V_{cont}$ are related to the net current phases, crucial for understanding the charge pump dynamics.
image_name:(c)
description:
[
name: M2, type: PMOS, ports: {S: VDD, D: d2s4, G: Vb2}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: QA}
name: M3, type: NMOS, ports: {S: GND, D: d1s3, G: QB}
name: M1, type: NMOS, ports: {S: GND, D: d1s3, G: Vb1}
name: C, type: Capacitor, value: C, ports: {Np: Vcont, Nn: GND}
name: PFD, type: Other, ports: {N1: A, N2: B}
name: Inverter, type: Inverter, ports: {In: QA, Out: QA}
]
extrainfo:The circuit diagram (c) shows a charge pump with a Phase Frequency Detector (PFD), an inverter, and a set of PMOS and NMOS transistors. The PMOS transistors M2 and M4 are connected to the VDD supply, while the NMOS transistors M3 and M1 are connected to GND. The capacitor C is used to stabilize the Vcont node. The PFD compares input signals A and B, and the inverter processes the QA signal.

Figure 16.44 (a) Implementation of charge pump; (b) effect of skew between $\overline{Q_{A}}$ and $Q_{B}$; (c) suppression of skew by a pass gate.

The above charge-sharing phenomenon can be suppressed by "bootstrapping." Illustrated in Fig. 16.47 [3], the idea is to "pin" $V_{X}$ and $V_{Y}$ to $V_{c o n t}$ after phase comparison is finished. When $S_{1}$ and $S_{2}$ turn off, $S_{3}$ and $S_{4}$ turn on, allowing the unity-gain amplifier to hold nodes $X$ and $Y$ at a potential equal to $V_{\text {cont }}$. Note that the amplifier need not provide much current because $I_{1} \approx I_{2}$. At the next phase comparison instant, $S_{1}$ and $S_{2}$ turn on, $S_{3}$ and $S_{4}$ turn off, and $V_{X}$ and $V_{Y}$ begin with a value equal to $V_{c o n t}$. Thus, no charge sharing occurs between $C_{P}$ and the capacitances at $X$ and $Y$.
image_name:(a) Figure 16.45 Effect of UP and DOWN current mismatch
description:The graph in Figure 16.45 (a) illustrates the effect of UP and DOWN current mismatch in a time-domain waveform format. The graph contains several waveforms stacked vertically, each representing different signals or parameters over time.

1. **Axes Labels and Units:**
- The horizontal axis represents time, labeled as 't'. No specific units are provided, but it is implied to be in a linear scale.
- The vertical axis is not explicitly labeled, but it depicts various signals such as \(\overline{Q_A}\), \(Q_{B\Delta}\), \(I_{D3}\), \(|I_{D4}|\), Net Current, and \(V_{cont}\).

2. **Overall Behavior and Trends:**
- **\(\overline{Q_A}\)** and **\(Q_{B\Delta}\):** Both signals are digital waveforms with clear high and low states. They exhibit a pulse-like behavior, transitioning between high and low states at distinct intervals.
- **\(I_{D3}\)** and **\(|I_{D4}|\):** These waveforms also show pulse-like behavior, similar to \(\overline{Q_A}\) and \(Q_{B\Delta}\), indicating periods of current flow.
- **Net Current:** This waveform highlights the mismatch effect, showing a net current that is non-zero only during a specific interval, represented by a shaded area. This suggests an imbalance between \(I_{D3}\) and \(|I_{D4}|\).
- **\(V_{cont}\):** This waveform shows a linear increase in voltage over time, followed by a steady state. It indicates a ramp-up behavior initially, which stabilizes after reaching a certain level.

3. **Key Features and Technical Details:**
- The transitions in \(\overline{Q_A}\), \(Q_{B\Delta}\), \(I_{D3}\), and \(|I_{D4}|\) are synchronized, suggesting a coordinated control mechanism.
- The shaded area in the Net Current waveform represents the period where the current mismatch is significant, leading to a non-zero net current.
- The ramp-up in \(V_{cont}\) signifies a gradual increase in control voltage, possibly used to adjust or stabilize the system in response to the current mismatch.

4. **Annotations and Specific Data Points:**
- The shaded area in the Net Current waveform is a critical feature, indicating the impact of the mismatch.
- No specific numerical values are provided, but the timing and duration of the pulses can be inferred relative to each other.

Overall, the graph effectively demonstrates the impact of mismatched currents on the net current and control voltage, highlighting the importance of synchronization and balance in the system's operation.

image_name:(b)
description:The graph labeled "(b)" is a time-domain waveform plot that illustrates the effect of UP and DOWN current mismatch on various signals. The horizontal axis represents time (t), while the vertical axis represents different signal levels without specific units indicated.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph showing multiple signals over time.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as time (t), though no specific units or scale are provided.
- The vertical axis represents different signal levels, including \( \overline{Q_A} \), \( Q_{B\Delta} \), \( I_{D3} \), \( |I_{D4}| \), Net Current, and \( V_{cont} \).

3. **Overall Behavior and Trends:**
- **\( \overline{Q_A} \) and \( Q_{B\Delta} \):** These signals show rectangular pulses with a slight timing offset between them, indicating a phase difference or mismatch.
- **\( I_{D3} \) and \( |I_{D4}| \):** These currents also show rectangular pulses, with \( |I_{D4}| \) having a similar timing offset as seen in \( Q_{B\Delta} \).
- **Net Current:** The waveform shows a shaded area indicating a mismatch effect. The net current initially increases, then stabilizes, and returns to its initial level, with the shaded area highlighting the impact of the timing mismatch.
- **\( V_{cont} \):** This control voltage shows a dip followed by a return to the baseline, indicating a response to the net current variation.

4. **Key Features and Technical Details:**
- The graph highlights the mismatch between the UP and DOWN currents through the shaded area in the Net Current waveform.
- The timing offset between \( \overline{Q_A} \) and \( Q_{B\Delta} \), as well as between \( I_{D3} \) and \( |I_{D4}| \), is a critical feature demonstrating the mismatch.

5. **Annotations and Specific Data Points:**
- The shaded area in the Net Current waveform is a critical feature, indicating the impact of the mismatch.
- No specific numerical values are provided, but the timing and duration of the pulses can be inferred relative to each other.

Overall, the graph effectively demonstrates the impact of mismatched currents on the net current and control voltage, highlighting the importance of synchronization and balance in the system's operation.

Figure 16.45 Effect of UP and DOWN current mismatch.
image_name:Figure 16.46(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: Vb1}
name: M2, type: PMOS, ports: {S: VDD, D: Y, G: Vb2}
name: Cx, type: Capacitor, value: Cx, ports: {Np: X, Nn: GND}
name: Cy, type: Capacitor, value: Cy, ports: {Np: Y, Nn: VDD}
name: Cp, type: Capacitor, value: Cp, ports: {Np: Vcont, Nn: GND}
name: S1, type: Switch, ports: {N1: X, N2: Vcont}
name: S2, type: Switch, ports: {N1: Y, N2: Vcont}
]
extrainfo:The circuit demonstrates charge sharing between capacitances at nodes X and Y with Cp, controlled by switches S1 and S2. M1 and M2 are used for switching operations controlled by bias voltages Vb1 and Vb2, respectively.

image_name:Figure 16.46(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: Vb1}
name: M2, type: PMOS, ports: {S: VDD, D: Y, G: Vb2}
name: CY, type: Capacitor, value: CY, ports: {Np: Y, Nn: GND}
name: CX, type: Capacitor, value: CX, ports: {Np: X, Nn: GND}
name: CP, type: Capacitor, value: CP, ports: {Np: Vcont, Nn: GND}
name: S1, type: Switch, ports: {N1: X, N2: Vcont}
name: S2, type: Switch, ports: {N1: Y, N2: Vcont}
]
extrainfo:The circuit demonstrates charge sharing between capacitances at nodes X and Y with Cp, controlled by switches S1 and S2. M1 and M2 are used for switching operations controlled by bias voltages Vb1 and Vb2, respectively.

Figure 16.46 Charge sharing between $C_{P}$ and capacitances at $X$ and $Y$.
image_name:Figure 16.47
description:
[
name: I1, type: CurrentSource, ports: {Np: X, Nn: GND}
name: I2, type: CurrentSource, ports: {Np: VDD, Nn: Y}
name: S1, type: Switch, ports: {N1: X, N2: Vcont}
name: S2, type: Switch, ports: {N1: Y, N2: Vcont}
name: S3, type: Switch, ports: {N1: X, N2: Out(+1)}
name: S4, type: Switch, ports: {N1: Y, N2: Out(+1)}
name: CP, type: Capacitor, value: CP, ports: {Np: Vcont, Nn: GND}
name: OpAmp, type: Buffer, ports: {In: Vcont, Out: Out(+1)}
]
extrainfo:The circuit demonstrates charge sharing between capacitances at nodes X and Y with Cp, controlled by switches S1 and S2. The OpAmp is used as a buffer to maintain the voltage at Vcont. I1 and I2 provide current to nodes X and Y, respectively.

Figure 16.47 Bootstrapping $X$ and $Y$ to minimize charge sharing.

### 16.3.2 Jitter in PLLs

The response of phase-locked loops to jitter is of extreme importance in most applications. We first describe the concepts of jitter and the rate of change of jitter.

As shown in Fig. 16.48, a strictly periodic waveform, $x_{1}(t)$, contains zero crossings that are evenly spaced in time. Now consider the nearly periodic signal $x_{2}(t)$, whose period experiences small changes, displacing the zero crossings from their ideal points. We say that the latter waveform suffers from jitter. ${ }^{11}$ Plotting the total phase, $\phi_{t o t}$, and the excess phase, $\phi_{e x}$, of the two waveforms, we observe that jitter manifests itself as variation of the excess phase with time. In fact, ignoring the harmonics above the fundamental, we can write $x_{1}(t)=A \cos \omega t$ and $x_{2}(t)=A \cos \left[\omega t+\phi_{n}(t)\right]$, where $\phi_{n}(t)$ models the variation of the period. ${ }^{12}$

The rate at which the jitter varies is also important. Consider the two jittery waveforms depicted in Fig. 16.49. The first signal, $y_{1}(t)$, experiences "slow jitter" because its instantaneous frequency varies slowly from one period to the next. The second signal, $y_{2}(t)$, experiences "fast jitter." The rate of change is also evident from the excess phase plots of the two waveforms.

image_name:x1(t) and x2(t)
description:The graph illustrates two time-domain waveforms, labeled as $x_1(t)$ and $x_2(t)$, along with their respective phase plots. The waveforms are represented as square waves over time $t$. The top portion of the graph shows the waveforms $x_1(t)$ and $x_2(t)$, where $x_1(t)$ has a constant period $T_B$, while $x_2(t)$ exhibits variations in its period, denoted as $T_B + \Delta T_1$ and $T_B + \Delta T_2$. This indicates that $x_2(t)$ is experiencing jitter, with fluctuations in the timing of its waveform transitions compared to $x_1(t)$. \n\nBelow the waveforms, the graph depicts two phase plots: one for total phase and another for excess phase. The total phase plot shows two lines, $\phi_{tot1}$ and $\phi_{tot2}$, representing the phase accumulation over time for $x_1(t)$ and $x_2(t)$, respectively. $\phi_{tot2}$ shows a steeper slope compared to $\phi_{tot1}$, indicating that the jitter in $x_2(t)$ causes a more rapid phase accumulation. \n\nThe excess phase plot at the bottom highlights the deviations from the ideal phase trajectory. It shows two lines, $\phi_{ex1}$ and $\phi_{ex2}$, corresponding to $x_1(t)$ and $x_2(t)$. The line for $\phi_{ex2}$ exhibits more fluctuations, underscoring the presence of jitter in $x_2(t)$. These fluctuations represent the phase noise or jitter, with $\phi_{ex2}$ showing more variability than $\phi_{ex1}$. \n\nOverall, the graph effectively demonstrates the concept of slow versus fast jitter by comparing the stable waveform $x_1(t)$ with the jittery waveform $x_2(t)$, and illustrates the impact of jitter on phase characteristics.
image_name:Total Phase
description:The diagram consists of three main components: two time-domain waveforms and two phase plots labeled as 'Total Phase' and 'Excess Phase'.

1. **Type of Graph and Function:**
- The diagram includes time-domain waveforms and phase plots.
- The waveforms illustrate the concept of jitter in digital signals.

2. **Axes Labels and Units:**
- The horizontal axis for all plots is labeled as time \( t \), with no specific units provided.
- The vertical sections are labeled as \( x_1(t) \), \( x_2(t) \), 'Total Phase', and 'Excess Phase'.

3. **Overall Behavior and Trends:**
- **Waveforms \( x_1(t) \) and \( x_2(t) \):**
- \( x_1(t) \) represents a waveform with a constant period \( T_B \).
- \( x_2(t) \) shows a waveform with varying periods \( T_B + \Delta T_1 \), \( T_B + \Delta T_2 \), indicating jitter.
- **Total Phase Plot:**
- Two lines, \( \phi_{tot1} \) and \( \phi_{tot2} \), show increasing trends over time, with \( \phi_{tot2} \) exhibiting a steeper slope, indicating a faster phase increase.
- **Excess Phase Plot:**
- The plot shows two lines, \( \phi_{ex1} \) and \( \phi_{ex2} \), with \( \phi_{ex2} \) demonstrating more variation and fluctuations, representing fast jitter.

4. **Key Features and Technical Details:**
- The waveforms and phase plots highlight the effects of jitter on signal integrity.
- \( x_1(t) \) serves as a reference with a stable period, while \( x_2(t) \) demonstrates the impact of jitter with varying periods.
- The phase plots further illustrate the impact of jitter through changes in total and excess phase.

5. **Annotations and Specific Data Points:**
- \( T_B \), \( \Delta T_1 \), and \( \Delta T_2 \) are annotated on the waveforms, showing the difference in period due to jitter.
- Arrows indicate the direction of phase change in the phase plots, emphasizing the increasing trend in total phase and the fluctuations in excess phase.
image_name:Excess Phase
description:The diagram illustrates two waveforms, labeled as $x_1(t)$ and $x_2(t)$, along with their respective total and excess phase plots. The waveforms are shown in the time domain, with the horizontal axis representing time ($t$).

1. **Waveforms $x_1(t)$ and $x_2(t)$:**
- **$x_1(t)$:** This waveform is depicted as a square wave with a constant period $T_B$. The transitions between high and low states occur at regular intervals, indicating a stable frequency.
- **$x_2(t)$:** This waveform also appears as a square wave but with varying periods, specifically $T_B + \Delta T_1$ and $T_B + \Delta T_2$. These variations indicate the presence of jitter, causing the waveform to deviate from the ideal periodicity.

2. **Total Phase Plot:**
- The plot shows two lines, $\phi_{tot1}$ and $\phi_{tot2}$, representing the total phase over time for $x_1(t)$ and $x_2(t)$, respectively.
- **$\phi_{tot1}$** appears as a straight line, indicating a constant frequency with no jitter.
- **$\phi_{tot2}$** shows a slightly fluctuating line, representing the jitter in $x_2(t)$, where the phase accumulates irregularly over time.

3. **Excess Phase Plot:**
- This plot illustrates the excess phase, $\phi_{ex1}$ and $\phi_{ex2}$, which is the deviation from the ideal phase.
- **$\phi_{ex1}$** remains near zero, indicating negligible excess phase and thus no jitter in $x_1(t)$.
- **$\phi_{ex2}$** fluctuates around zero, indicating the presence of jitter in $x_2(t)$. The variations in $\phi_{ex2}$ correspond to the irregularities in the waveform's period.

Overall, the diagram effectively contrasts a stable waveform with a jittery one, highlighting the impact of jitter on both the total and excess phase. The key takeaway is the difference in stability between the two waveforms, with $x_2(t)$ exhibiting noticeable jitter effects.

Figure 16.48 Ideal and jittery waveforms.
image_name:Figure 16.49 Illustration of slow and fast jitter.
description:consists of three graphs. The first two graphs depict time-domain waveforms labeled as $y_1(t)$ and $y_2(t)$, and the third graph illustrates the excess phase labeled as $\phi_{ex1}$ and $\phi_{ex2}$.

1. **Type of Graph and Function:**
- The graphs are time-domain waveforms that show the behavior of signals over time.

2. **Axes Labels and Units:**
- The horizontal axis for all graphs is labeled as time ($t$), though no specific units are provided.
- There are no explicit units or scales on the vertical axes.

3. **Overall Behavior and Trends:**
- **$y_1(t)$:** This waveform is a stable square wave with consistent period and amplitude, indicating no jitter.
- **$y_2(t)$:** This waveform is also a square wave but exhibits noticeable irregularities in its period, indicative of jitter.
- **Excess Phase ($\phi_{ex1}$ and $\phi_{ex2}$):** The excess phase for $y_1(t)$, $\phi_{ex1}$, is relatively stable and close to zero, showing minimal fluctuation. In contrast, $\phi_{ex2}$ exhibits significant fluctuations around zero, corresponding to the jitter observed in $y_2(t)$.

4. **Key Features and Technical Details:**
- The key feature of $y_1(t)$ is its stability, with a uniform pattern and no deviations in period.
- $y_2(t)$ shows irregular spacing between transitions, highlighting the presence of jitter.
- The excess phase graph emphasizes the difference in stability, with $\phi_{ex2}$ showing more variability compared to $\phi_{ex1}$.

5. **Annotations and Specific Data Points:**
- The excess phase graph includes annotations for $\phi_{ex1}$ and $\phi_{ex2}$, with the lines visually representing the stability (or lack thereof) in the phase of the waveforms.
- No specific numerical values are provided, but the qualitative differences between the stable and jittery waveforms are clearly illustrated.
image_name:Excess Phase
description:The diagram consists of three separate graphs aligned vertically, each representing different aspects of waveforms and their phase behavior over time.

1. **Waveform Graphs**:
- **Type**: Time-domain waveforms.
- **Graphs**:
- The top waveform is labeled as $y_1(t)$, and it is a square wave with consistent periodicity, indicating a stable waveform without noticeable jitter.
- The middle waveform is labeled as $y_2(t)$, also a square wave but with irregularities in its period, indicating the presence of jitter. The waveform does not maintain a consistent period, showing variations that suggest instability.
- **Axes**:
- The horizontal axis for both $y_1(t)$ and $y_2(t)$ represents time ($t$), though specific units are not provided.

2. **Excess Phase Graph**:
- **Type**: Time-domain phase deviation graph.
- **Graph**:
- The bottom graph illustrates excess phase fluctuations, with two lines labeled as $\phi_{ex1}$ and $\phi_{ex2}$.
- $\phi_{ex1}$ is shown as a smoother line with less variation, corresponding to the stable waveform $y_1(t)$.
- $\phi_{ex2}$ exhibits more pronounced fluctuations around zero, indicating the presence of jitter in $y_2(t)$. These fluctuations correspond to the irregularities in the waveform's period.
- **Axes**:
- The horizontal axis represents time ($t$), similar to the waveform graphs.
- The vertical axis is labeled "Excess Phase," though specific units are not provided.

**Overall Behavior and Trends**:
- $y_1(t)$ maintains a consistent, stable period, with its associated excess phase $\phi_{ex1}$ showing minimal deviation.
- $y_2(t)$ exhibits noticeable jitter, reflected in the irregularities in its period and the corresponding fluctuations in $\phi_{ex2}$.

**Key Features**:
- The contrast between $\phi_{ex1}$ and $\phi_{ex2}$ effectively highlights the impact of jitter on the waveform's stability. The steady behavior of $\phi_{ex1}$ versus the fluctuating nature of $\phi_{ex2}$ underscores the stability differences between the two waveforms.

Figure 16.49 Illustration of slow and fast jitter.

Two jitter phenomena in phase-locked loops are of great interest: (1) the input exhibits jitter, and (2) the VCO produces jitter. Let us study each case, assuming that the input and output waveforms are expressed as $x_{\text {in }}(t)=A \cos \left[\omega t+\phi_{\text {in }}(t)\right]$ and $x_{\text {out }}(t)=A \cos \left[\omega t+\phi_{\text {out }}(t)\right]$.

The transfer functions derived for type I and type II PLLs have a low-pass characteristic, suggesting that if $\phi_{\text {in }}(t)$ varies rapidly, then $\phi_{\text {out }}(t)$ does not fully track the variations. In other words, slow jitter at the input propagates to the output unattenuated, but fast jitter does not. We say the PLL low-pass filters $\phi_{i n}(t)$.

Now suppose the input is strictly periodic, but the VCO suffers from jitter. Viewing jitter as random phase variations, we construct the model depicted in Fig. 16.50, where the input excess phase is set to zero
image_name:Figure 16.50 Effect of VCO jitter
description:The system block diagram in Figure 16.50 illustrates the effect of VCO jitter on a phase-locked loop (PLL) system. The primary components of the diagram include:

1. **Phase-Frequency Detector/Charge Pump/Low Pass Filter (PFD/CP/LPF):**
- This block combines the functions of a phase-frequency detector, a charge pump, and a low-pass filter.
- The input to this block is the phase difference between the input phase (Φ_in = 0) and the feedback phase from the output (Φ_out).
- The output of this block is a voltage that represents the filtered phase difference, characterized by the transfer function \( \frac{I_P}{2\pi} \left( \frac{1}{C_P s} + R_P \right) \), where \( I_P \) is the charge pump current, \( C_P \) is the capacitance, \( R_P \) is the resistance, and \( s \) is the complex frequency variable.

2. **Voltage-Controlled Oscillator (VCO):**
- This block generates an output frequency that is controlled by the input voltage from the PFD/CP/LPF block.
- The transfer function of the VCO is \( \frac{K_{vco}}{s} \), where \( K_{vco} \) is the VCO gain.

3. **Adder for VCO Jitter:**
- A summation block is used to add the VCO jitter (Φ_VCO) to the output of the VCO.
- This represents the random phase variations introduced by the VCO jitter.

4. **Feedback Loop:**
- The output phase (Φ_out) is fed back to the PFD/CP/LPF block to form a closed-loop system.
- This feedback loop is crucial for maintaining phase lock and minimizing the effect of phase noise.

The overall function of the system is to maintain a stable output phase (Φ_out) despite the presence of VCO jitter. The PFD/CP/LPF block acts to filter the input phase and control the VCO, while the feedback loop ensures that the system remains locked to the desired phase. The addition of VCO jitter models the effect of random phase variations, and the system's high-pass characteristic allows it to filter out slow jitter, thereby stabilizing the output phase.

Figure 16.50 Effect of VCO jitter.
[i.e., $x_{i n}(t)=A \cos \omega t$ ] and a random component $\Phi_{V C O}$ is added to the output of the VCO to represent its jitter. The reader can show that the transfer function from $\Phi_{V C O}$ to $\Phi_{\text {out }}$ for a type II PLL is equal to

$$
\begin{equation*}
\frac{\Phi_{\text {out }}}{\Phi_{V C O}}(s)=\frac{s^{2}}{s^{2}+2 \zeta \omega_{n} s+\omega_{n}^{2}} \tag{16.48}
\end{equation*}
$$

Interestingly, the characteristic has a high-pass nature, indicating that slow jitter components generated by the VCO are suppressed, but fast jitter components are not. This can be understood with the aid of Fig. 16.50: if $\phi_{V C O}(t)$ changes slowly (e.g., the oscillation period drifts with temperature), then the comparison with $\phi_{i n}=0$ (i.e., a perfectly periodic signal) generates a slowly-varying error that propagates through the LPF and adjusts the VCO frequency, thereby counteracting the change in $\phi_{V C O}$. On the other hand, if $\phi_{V C O}$ varies rapidly (e.g., high-frequency noise modulates the oscillation period), then the error produced by the phase detector is heavily attenuated by the poles in the loop, failing to correct for the change.

Figure 16.51 conceptually summarizes the response of PLLs to input jitter and VCO jitter. Depending on the application and the environment, one or both sources may be significant, requiring an optimum choice of the loop bandwidth.
image_name:Figure 16.51
description:The graph in Figure 16.51 consists of two separate plots, each representing a transfer function related to jitter in a Phase-Locked Loop (PLL) system.

1. **Left Plot:**
- **Type of Graph:** The graph is a Bode-like plot showing the relationship between the output jitter and input jitter.
- **Axes Labels and Units:** The vertical axis represents the magnitude of the output jitter to input jitter ratio, denoted as $|\frac{\phi_{out}}{\phi_{in}}|$. The horizontal axis represents the rate of change of the input phase, $\phi_{in}$.
- **Overall Behavior and Trends:** The plot shows a decreasing trend as the rate of change of $\phi_{in}$ increases. Initially, the ratio remains relatively constant, indicating that the output jitter is similar to the input jitter. As the rate of change increases, the ratio decreases, suggesting that the PLL attenuates the input jitter more effectively at higher frequencies.
- **Key Features and Technical Details:** The plot suggests a low-pass filter behavior, where low-frequency jitter passes through the PLL, but high-frequency jitter is attenuated.

2. **Right Plot:**
- **Type of Graph:** This graph also resembles a Bode plot, focusing on the relationship between the output jitter and VCO jitter.
- **Axes Labels and Units:** The vertical axis represents the magnitude of the output jitter to VCO jitter ratio, denoted as $|\frac{\phi_{out}}{\phi_{VCO}}|$. The horizontal axis represents the rate of change of the VCO phase, $\phi_{VCO}$.
- **Overall Behavior and Trends:** The plot shows an increasing trend, indicating that as the rate of change of $\phi_{VCO}$ increases, the output jitter becomes more pronounced relative to the VCO jitter. This suggests that high-frequency changes in the VCO phase are less attenuated by the PLL.
- **Key Features and Technical Details:** The plot suggests a high-pass filter behavior, where the PLL is more sensitive to higher frequency VCO jitter.

Overall, these plots illustrate the frequency-dependent behavior of a PLL in response to different sources of jitter, emphasizing the importance of selecting an appropriate loop bandwidth based on the specific application requirements.

Figure 16.51 Transfer functions of jitter from input and VCO to the output.

## 16.4 Delay-Locked Loops

A variant of PLLs that finds usage in many applications is the "delay-locked loop." To arrive at the concept, let us begin with an example. Suppose an application requires four clock phases with a precise spacing of $\Delta T=1$ ns between consecutive edges [Fig. 16.52(a)]. How should these phases be generated? We can use a two-stage differential ring oscillator ${ }^{13}$ to produce the four phases, but how do we guarantee that $\Delta T=1 \mathrm{~ns}$ despite process and temperature variations? This requires that the oscillator be locked to a $250-\mathrm{MHz}$ reference so that the output period is exactly equal to 4 ns [Fig. 16.52(b)].

An alternative approach to generating the clock phases of Fig. 16.52(a) is to apply the input clock to four delay stages in a cascade. Illustrated in Fig. 16.53(a), this technique nonetheless does not produce a well-defined edge spacing because the delay of each stage varies with process and temperature. Now consider the circuit shown in Fig. 16.53(b), where the phase difference between $C K_{i n}$ and $C K_{4}$ is sensed by a phase detector, a proportional average voltage, $V_{\text {cont }}$, is generated, and the delay of the stages is adjusted with negative feedback. For a large loop gain, the phase difference between $C K_{i n}$ and $C K_{4}$ is small; that is, the four stages delay the clock by almost exactly one period, thereby establishing precise edge spacing. ${ }^{14}$ This topology is called a delay-locked loop to emphasize that it incorporates a voltagecontrolled delay line (VCDL) rather than a VCO. In practice, a charge pump is interposed between the PD

image_name:(a)
description:The graph in Figure 16.52 (a) is a time-domain waveform showing clock phases with an edge-to-edge delay of 1 ns. The graph features four distinct clock signals labeled CK1, CK2, CK3, and CK4 plotted against time on the horizontal axis, which is marked in nanoseconds (ns). Each clock signal is represented as a square wave, with transitions between high and low states.

The clock signals are staggered in such a way that the rising edge of each subsequent clock signal is delayed by 1 ns relative to the previous one. This results in a consistent phase shift between the clock signals. Specifically, CK1 leads, followed by CK2, CK3, and finally CK4, each separated by the 1 ns delay.

Overall, the graph illustrates a precise timing arrangement where the clock signals are evenly spaced, maintaining a uniform phase relationship, which is critical for synchronized operations in digital circuits.
image_name:(b)
description:The diagram labeled (b) represents a simple delay-locked loop (DLL) system, which is used to generate clock phases with precise edge spacing. The main components of this system include:

1. **Phase Frequency Detector (PFD)/Charge Pump (CP)/Low-Pass Filter (LPF) Block:** This block receives an input frequency \( f_{in} \) of 250 MHz. It serves to compare the phase of the input signal with the feedback signal, producing a control voltage \( V_{cont} \) that adjusts the delay line.

2. **Voltage-Controlled Delay Line (VCDL):** This component consists of multiple delay stages. Each stage is represented by an amplifier symbol with differential inputs and outputs. The delay stages are responsible for generating the clock signals \( CK_1, CK_3, CK_4, \) and \( CK_2 \) with specific phase differences.

3. **Feedback Loop:** The feedback loop connects the output of the VCDL back to the PFD/CP/LPF block. This loop ensures that the delay through the VCDL is adjusted to match the desired phase difference between the input and output clock signals.

**Flow of Information:**
- The input frequency \( f_{in} \) is fed into the PFD/CP/LPF block.
- The control voltage \( V_{cont} \) generated by this block is used to adjust the delay in the VCDL.
- The VCDL outputs the clock signals \( CK_1, CK_3, CK_4, \) and \( CK_2 \) with appropriate delays.
- The feedback loop takes one of these outputs back to the PFD/CP/LPF block to maintain synchronization.

**Overall System Function:**
The primary function of this DLL system is to ensure that the clock signals \( CK_1, CK_3, CK_4, \) and \( CK_2 \) are generated with precise phase differences, achieving accurate timing for digital circuits. The system continuously adjusts the delay line based on the feedback to maintain the desired phase alignment, thus ensuring stable and reliable clock signal generation.

Figure 16.52 (a) Clock phases with edge-to-edge delay of 1 ns ; (b) use of a phase-locked ring oscillator to generate the clock phases.
and the LPF to achieve an infinite loop gain. Each delay stage may be based on one of the ring oscillator stages described in Chapter 15.
image_name:16.53(a)
description:The circuit is a series of inverters, each generating a clock phase output from a single input clock signal CKin. This forms a delay line for clock signal generation.
image_name:16.53(b)
description:This circuit represents a simple delay-locked loop (DLL) with four inverter stages and a phase detector/low-pass filter (PD/LPF) providing feedback for control.

Figure 16.53 (a) Generation of clock edges by delay stages; (b) simple delay-locked loop.
The reader may wonder about the advantages of DLLs over PLLs. First, delay lines are generally less susceptible to noise than are oscillators because corrupted zero crossings of a waveform disappear at the end of a delay line, whereas they are recirculated in an oscillator, thereby experiencing more corruption. Second, in the VCDL of Fig. 16.53(b), a change in the control voltage immediately changes the delay; that is, the transfer function $\Phi_{\text {out }}(s) / V_{\text {cont }}(s)$ is simply equal to the gain of the VCDL, $K_{V C D L}$. Thus, the feedback system of Fig. 16.53(b) has the same order as the LPF, and its stability and settling issues are more relaxed than those of a PLL.

#### Example 16.12

Explain qualitatively what type of transfer function the DLL of Fig. 16.54 has.

#### Solution

Suppose the input exhibits slow phase fluctuations. Then, the phase error sees a high gain through the PD/CP/LPF combination, and the delay of the line is adjusted so as to minimize this error. That is, $\phi_{\text {out }}$ tracks $\phi_{\text {in }}$, and the gain is about unity. Now, suppose the input exhibits very fast phase changes. The feedback loop thus has little gain, providing little correction at the control of the delay line; i.e., $V_{\text {cont }}$ remains relatively constant. As a result, the input phase variations directly propagate to the output, yielding a gain of about unity. We conclude that the DLL exhibits an all-pass response, but that for moderately fast phase fluctuations, the response may have a dip or a peak.
image_name:Figure 16.54
description:The system block diagram in Figure 16.54 represents a Delay-Locked Loop (DLL). The main components of this system are:

1. **Phase Detector (PD):** This block compares the phase of the input signal, denoted as \( \phi_{in} \), with the phase of the feedback signal from the output, \( \phi_{out} \). The phase detector generates an error signal based on the phase difference.

2. **Charge Pump (CP):** The error signal from the PD is fed into the charge pump, which converts the phase difference into a control voltage, \( V_{cont} \). This voltage is used to adjust the delay line.

3. **Loop Filter:** Consisting of a resistor \( R_P \), and two capacitors \( C_P \) and \( C_2 \), the loop filter smooths the control voltage \( V_{cont} \) to reduce noise and stabilize the loop.

4. **Delay Line:** The delay line consists of a series of inverters. The control voltage \( V_{cont} \) adjusts the delay introduced by these inverters, thereby aligning the phase of the output with the input phase.

**Flow of Information:**
- The input signal \( \phi_{in} \) is fed into the phase detector and also directed to the output.
- The phase detector compares \( \phi_{in} \) with the feedback from \( \phi_{out} \) and sends the phase error to the charge pump.
- The charge pump outputs a control voltage \( V_{cont} \), which is filtered by the loop filter components \( R_P \), \( C_P \), and \( C_2 \).
- The filtered control voltage \( V_{cont} \) is then used to adjust the delay line, which consists of the series of inverters, ensuring that the output phase \( \phi_{out} \) locks to the input phase \( \phi_{in} \).

**Labels, Annotations, and Key Indicators:**
- \( \phi_{in} \) and \( \phi_{out} \) are the input and output phases, respectively.
- \( V_{cont} \) is the control voltage that adjusts the delay line.
- The loop filter components \( R_P \), \( C_P \), and \( C_2 \) are crucial for stabilizing the control voltage.

**Overall System Function:**
The DLL in this diagram is designed to align the output phase \( \phi_{out} \) with the input phase \( \phi_{in} \) by adjusting the delay through the series of inverters. The feedback loop, consisting of the phase detector, charge pump, and loop filter, ensures that any phase error is corrected by adjusting the delay line, thus achieving phase alignment.

Figure 16.54

The principal drawback of DLLs is that they cannot generate a variable output frequency. This issue becomes clearer when we study the frequency synthesis capabilities of PLLs in Sec. 16.5.1. DLLs may also suffer from locked delay ambiguity. That is, if the total delay of the four stages in Fig. 16.53(b) can vary from below $T_{i n}$ to above $2 T_{i n}$, then the loop may lock with a $C K_{i n}$-to- $C K_{4}$ delay equal to either $T_{i n}$ or $2 T_{i n}$. This ambiguity proves detrimental if the DLL must provide precisely-spaced clock edges because the edge-to-edge delay may settle to $2 T_{i n} / 4$ rather than $T_{i n} / 4$. In such cases, additional circuitry is necessary to avoid the ambiguity. Also, mismatches between the delay stages and their load capacitances introduce error in the edge spacing, requiring large devices and careful layout.

## 16.5 Applications

After nearly 90 years since its invention, phase locking continues to find new applications in electronics, communication, and instrumentation. Examples include memories, microprocessors, hard disk drive electronics, RF and wireless transceivers, and optical fiber receivers.

The reader may recall from Sec. 16.1.2 that a PLL appears no more useful than a short piece of wire because both guarantee a small phase difference between the input and the output. In this section, we present a number of applications that demonstrate the versatility of phase locking. The concepts described below have been the topic of numerous books and papers, e.g., [6, 7].

### 16.5.1 Frequency Multiplication and Synthesis

Frequency Multiplication A PLL can be modified such that it multiplies its input frequency by a factor of $M$. To arrive at the implementation, we exploit an analogy with voltage multiplication. As depicted in Fig. 16.55(a), a feedback system amplifies the input voltage by a factor of $M$ if the output voltage is divided by $M$ [i.e., if $\left.R_{2} /\left(R_{1}+R_{2}\right)=1 / M\right]$ and the result is compared with the input. Thus, as shown in Fig. 16.55(b), if the output frequency of a PLL is divided by $M$ and applied to the phase detector, we have $f_{\text {out }}=M f_{\text {in }}$. From another point of view, since $f_{D}=f_{\text {out }} / M$ and $f_{D}$ and $f_{\text {in }}$ must be equal in the
image_name:Figure 16.55(a)
description:
[
name: A0, type: OpAmp, value: A0, ports: {InP: Vin, InN: InN(A0), OutP: Vout}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: InN(A0)}
name: R2, type: Resistor, value: R2, ports: {N1: InN(A0), N2: GND}
]
extrainfo:The circuit is a feedback amplifier with an operational amplifier A0. It uses resistors R1 and R2 to set the feedback ratio, amplifying the input voltage Vin to produce the output voltage Vout.

image_name:Figure 16.55 (b)
description:The system block diagram in Figure 16.55 (b) represents a phase-locked loop (PLL) used for frequency multiplication. It consists of several key components:

1. **Phase Frequency Detector (PFD):** This block compares the input frequency \( f_{in} \) with the feedback frequency \( f_D \). The PFD outputs a signal that indicates the phase difference between these frequencies.

2. **Charge Pump/Low Pass Filter (CP/LPF):** The signal from the PFD is fed into this block. The charge pump converts the phase difference signal into a voltage, which is then smoothed by the low pass filter. This block helps in controlling the voltage-controlled oscillator (VCO).

3. **Voltage-Controlled Oscillator (VCO):** The filtered voltage from the CP/LPF controls the frequency of the VCO. The VCO generates an output frequency \( f_{out} \) which is a multiple of the input frequency.

4. **Divider (÷M):** The output frequency \( f_{out} \) is fed back into the system through a frequency divider. This block divides the output frequency by a factor \( M \) to produce the feedback frequency \( f_D \). The division ensures that the PLL locks the output frequency to \( M \) times the input frequency.

**Flow of Information:**
- The input frequency \( f_{in} \) enters the PFD where it is compared with the feedback frequency \( f_D \).
- The PFD's output controls the CP/LPF, which adjusts the VCO.
- The VCO produces the output frequency \( f_{out} \), which is divided by \( M \) to generate \( f_D \).
- This feedback loop ensures that \( f_{out} = M \times f_{in} \), effectively multiplying the input frequency by \( M \).

**Overall System Function:**
The primary function of this PLL is to multiply the input frequency \( f_{in} \) by a factor \( M \) through the use of a feedback loop that includes a frequency divider. This setup is commonly used in applications requiring precise frequency synthesis and control.

Figure 16.55 (a) Voltage amplification and (b) frequency multiplication.
locked condition, the PLL multiplies $f_{i n}$ by $M$. The $\div M$ circuit is realized as a counter that produces one output pulse for every $M$ input pulses.

As with voltage division in Fig. 16.55(a), the feedback divider in the loop of Fig. 16.55(b) alters the system characteristics. Using (16.44), we rewrite (16.45) as

$$
\begin{align*}
H(s) & =\frac{\frac{I_{P}}{2 \pi}\left(R_{P}+\frac{1}{C_{P} s}\right) \frac{K_{V C O}}{s}}{1+\frac{1}{M} \frac{I_{P}}{2 \pi}\left(R_{P}+\frac{1}{C_{P} s}\right) \frac{K_{V C O}}{s}}  \tag{16.49}\\
& =\frac{\frac{I_{P} K_{V C O}}{2 \pi C_{P}}\left(R_{P} C_{P} s+1\right)}{s^{2}+\frac{I_{P}}{2 \pi} \frac{K_{V C O}}{M} R_{P} s+\frac{I_{P}}{2 \pi C_{P}} \frac{K_{V C O}}{M}} \tag{16.50}
\end{align*}
$$

Note that $H(s) \rightarrow M$ as $s \rightarrow 0$, i.e., phase or frequency changes at the input result in an $M$-fold change in the corresponding output quantity. Comparing the denominators of (16.45) and (16.50), we observe that frequency division in the loop manifests itself as division of $K_{V C O}$ by $M$. In other words, as far as the poles of the closed-loop system are concerned, we can assume that the oscillator and the divider form a VCO with an equivalent gain of $K_{V C O} / M$. This is, of course, to be expected because, for the VCO/divider cascade shown in Fig. 16.56, we have

$$
\begin{align*}
\omega_{\text {out }} & =\frac{\omega_{0}+K_{V C O} V_{\text {cont }}}{M}  \tag{16.51}\\
& =\frac{\omega_{0}}{M}+\frac{K_{V C O}}{M} V_{c o n t} \tag{16.52}
\end{align*}
$$

Thus, the combination cannot be distinguished from a VCO having an intercept frequency of $\omega_{0} / M$ and a gain of $K_{V C O} / M$.
image_name:Figure 16.56 Equivalency of VCO/divider combination to a single VCO
description:The system block diagram titled "Figure 16.56 Equivalency of VCO/divider combination to a single VCO" consists of two main components arranged in sequence: a Voltage-Controlled Oscillator (VCO) and a Divider block labeled \( \div M \).

1. **Main Components:**
- **VCO (Voltage-Controlled Oscillator):** This block is responsible for generating an output frequency that is directly proportional to the input control voltage \( V_{cont} \). The VCO's function is to convert the voltage input into a corresponding frequency.
- **Divider (\( \div M \)):** This block takes the frequency output from the VCO and divides it by a factor \( M \). The divider reduces the frequency of the signal, effectively scaling down the VCO's output.

2. **Flow of Information or Control:**
- The input to the system is a control voltage \( V_{cont} \), which is fed into the VCO. The VCO processes this voltage to produce an output frequency signal.
- This frequency signal is then passed to the Divider block, where it is divided by \( M \), resulting in the final output frequency \( \omega_{out} \).
- The flow of information is unidirectional, moving from the input \( V_{cont} \) through the VCO, into the Divider, and finally to the output \( \omega_{out} \).

3. **Labels, Annotations, and Key Indicators:**
- The input is labeled as \( V_{cont} \), indicating its role as a control voltage.
- The output is labeled as \( \omega_{out} \), representing the output frequency after division.
- The divider is annotated with \( \div M \), specifying the division factor.

4. **Overall System Function:**
- The primary function of this system is to act as an equivalent single VCO with a modified gain and intercept frequency. The combination of the VCO and the divider results in an output frequency that is a scaled version of the VCO's frequency, effectively simulating a VCO with an equivalent gain of \( K_{VCO} / M \) and an intercept frequency of \( \omega_{0} / M \). This setup is useful in applications where specific frequency scaling is required.

Figure 16.56 Equivalency of VCO/divider combination to a single VCO.
The foregoing discussion suggests that (16.46) and (16.47) can be respectively rewritten as

$$
\begin{align*}
\omega_{n} & =\sqrt{\frac{I_{P}}{2 \pi C_{P}} \frac{K_{V C O}}{M}}  \tag{16.53}\\
\zeta & =\frac{R_{P}}{2} \sqrt{\frac{I_{P} C_{P}}{2 \pi} \frac{K_{V C O}}{M}} \tag{16.54}
\end{align*}
$$

Also, the decay time constant is modified to $\left(\zeta \omega_{n}\right)^{-1}=4 \pi M /\left(R_{P} I_{P} K_{V C O}\right)$. It follows that inserting a divider in a type II loop degrades both the stability and the settling speed, requiring a proportional increase in the charge-pump current.

The frequency-multiplying loop of Fig. 16.55(b) exhibits two interesting properties. First, unlike the voltage amplifier of Fig. 16.55(a), the PLL provides a multiplication factor exactly equal to $M$, a unique attribute resulting from phase locking. Second, the output frequency can be varied by changing the divide ratio $M$, an extremely useful property in synthesizing frequencies. Note that DLLs cannot perform such synthesis.

Frequency Synthesis Some systems require a periodic waveform whose frequency (1) must be very accurate (e.g., exhibit an error less than 10 ppm ), and (2) can be varied in very fine steps (e.g., in steps of 30 kHz from 900 MHz to 925 MHz ). Commonly encountered in wireless transceivers, such requirements can be met through frequency multiplication by PLLs.

Figure 16.57 shows the architecture of a phase-locked frequency synthesizer. The channel control input is a digital word that defines the value of $M$. Since $f_{\text {out }}=M f_{R E F}$, the relative accuracy of $f_{\text {out }}$ is equal to that of $f_{R E F}$. For this reason, $f_{R E F}$ is derived from a stable, low-noise crystal oscillator. Note that $f_{\text {out }}$ varies in steps equal to $f_{R E F}$ if $M$ changes by one each time.
image_name:Figure 16.57 Frequency synthesizer
description:The block diagram in Figure 16.57 illustrates the architecture of a phase-locked frequency synthesizer. This system is designed to generate a stable output frequency, \( f_{\text{out}} \), by locking onto a reference frequency \( f_{\text{REF}} \), using a phase-locked loop (PLL) configuration. Here's a detailed breakdown of the components and their functions:

1. **Main Components:**
- **Phase Frequency Detector (PFD):** This block compares the phase and frequency of the input reference frequency \( f_{\text{REF}} \) with the feedback signal from the output and generates an error signal based on the difference.
- **Charge Pump/Low Pass Filter (CP/LPF):** The error signal from the PFD is fed into this block, which converts it into a voltage signal to control the next stage. The low-pass filter helps in smoothing the signal and removing high-frequency noise.
- **Voltage-Controlled Oscillator (VCO):** Controlled by the output of the CP/LPF, the VCO generates the output frequency \( f_{\text{out}} \). The frequency of the VCO is adjusted based on the input control voltage.
- **Frequency Divider (\( \div M \)):** This block divides the output frequency \( f_{\text{out}} \) by a factor \( M \), which is controlled by the digital channel control input. This divided frequency is fed back to the PFD for comparison with \( f_{\text{REF}} \).

2. **Flow of Information or Control:**
- The reference frequency \( f_{\text{REF}} \) enters the PFD, where it is compared with the feedback signal from the frequency divider.
- The PFD generates an error signal that is processed by the CP/LPF to produce a control voltage.
- This control voltage adjusts the VCO, which outputs the frequency \( f_{\text{out}} \).
- \( f_{\text{out}} \) is then fed back through the frequency divider \( \div M \) to complete the feedback loop.
- The value of \( M \) is set by a digital channel control input, allowing for frequency tuning.

3. **Labels, Annotations, and Key Indicators:**
- The input and output frequencies are labeled as \( f_{\text{REF}} \) and \( f_{\text{out}} \), respectively.
- The feedback loop is clearly indicated, showing the path from the VCO through the divider back to the PFD.
- The channel control input is annotated, indicating its role in setting the division factor \( M \).

4. **Overall System Function:**
- The primary function of this frequency synthesizer is to generate a stable and precise output frequency \( f_{\text{out}} \) that is a multiple of the reference frequency \( f_{\text{REF}} \). By adjusting \( M \), the system can vary \( f_{\text{out}} \) in discrete steps of \( f_{\text{REF}} \), maintaining high accuracy and stability due to the feedback control mechanism provided by the PLL architecture.
Figure 16.57 Frequency synthesizer.

CMOS frequency synthesizers achieving gigahertz output frequencies have been reported. Issues such as noise, sidebands, settling speed, frequency range, and power dissipation continue to challenge synthesizer designers.

### 16.5.2 Skew Reduction

The earliest usage of phase locking in digital systems was for skew reduction. Suppose a synchronous pair of data and clock lines enter a large digital chip, as shown in Fig. 16.58. Since the clock typically drives a large number of transistors and long interconnects, it is first applied to a large buffer. Thus, the clock distributed on the chip may suffer from substantial skew, $\Delta T$, with respect to the data, an undesirable effect because it reduces the timing budget for on-chip operations.
image_name:Figure 16.58
description:The graph in Figure 16.58 is a time-domain waveform diagram illustrating the concept of skew between data and a buffered clock signal within a digital chip. The diagram consists of two main parts: a schematic representation of a digital chip with a buffer and a set of waveform signals.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform diagram.

2. **Axes Labels and Units:**
- The horizontal axis represents time, labeled as \( t \).
- There are no explicit units or numerical values provided on the axes, but it is implied to be a linear time scale.

3. **Overall Behavior and Trends:**
- The diagram shows three signals: \( D_{in} \), \( CK_{in} \), and \( CK_{B} \).
- \( D_{in} \) is a digital data signal with a square waveform.
- \( CK_{in} \) is the incoming clock signal, also with a square waveform.
- \( CK_{B} \) is the buffered clock signal, which is delayed relative to \( CK_{in} \), illustrating the skew \( \Delta T \).
- The skew \( \Delta T \) is marked as the time difference between the rising edges of \( CK_{in} \) and \( CK_{B} \).

4. **Key Features and Technical Details:**
- The buffer is represented in the schematic as an inverter symbol with a load capacitance \( C_L \) connected to ground.
- The skew \( \Delta T \) is a critical aspect, as it demonstrates the delay introduced by the buffer.

5. **Annotations and Specific Data Points:**
- The skew \( \Delta T \) is explicitly annotated on the waveform diagram, indicating the timing difference between \( CK_{in} \) and \( CK_{B} \).
- No specific numerical values are provided for \( \Delta T \) or other aspects of the waveforms, focusing instead on the conceptual illustration of skew.
Figure 16.58 Skew between data and buffered clock.

Now consider the circuit shown in Fig. 16.59, where $C K_{\text {in }}$ is applied to an on-chip PLL and the buffer is placed inside the loop. Since the PLL guarantees a nominally-zero phase difference between $C K_{i n}$ and $C K_{B}$, the skew is eliminated. From another point of view, the constant phase shift introduced by the buffer is divided by the infinite loop gain of the feedback system. Note that the VCO output, $V_{V C O}$, may not be aligned with $C K_{i n}$, a nonetheless unimportant issue because $V_{V C O}$ is not used.
image_name:Figure 16.59
description:The block diagram in Figure 16.59 illustrates a Phase-Locked Loop (PLL) system used to eliminate skew between an input clock signal \( CK_{in} \) and an output clock signal \( CK_{B} \). The main components of this system include:

1. **Phase Frequency Detector (PFD):** This block receives the input clock signal \( CK_{in} \) and compares its phase and frequency with a feedback signal from the output. The PFD generates an error signal that indicates the phase difference between these two signals.

2. **Charge Pump and Low-Pass Filter (CP/LPF):** The error signal from the PFD is fed into the charge pump and low-pass filter. The CP/LPF converts the phase error signal into a voltage level that controls the next stage, smoothing out high-frequency noise.

3. **Voltage-Controlled Oscillator (VCO):** The VCO receives the control voltage from the CP/LPF and generates an output signal \( V_{VCO} \) whose frequency is adjusted to minimize the phase error.

4. **Buffer:** The buffer amplifies the VCO output \( V_{VCO} \) before sending it to the output as \( CK_{B} \). This stage ensures signal integrity and drives the capacitive load \( C_{L} \) connected to ground.

5. **Feedback Loop:** The output \( CK_{B} \) is fed back to the PFD, closing the loop and allowing continuous adjustment to maintain phase alignment with \( CK_{in} \).

The system's primary function is to maintain a nominally-zero phase difference between the input and output clock signals, effectively eliminating skew. The buffer introduces a constant phase shift, but this is mitigated by the infinite loop gain of the feedback system, ensuring that \( CK_{B} \) remains aligned with \( CK_{in} \). The VCO output \( V_{VCO} \) itself may not be aligned with \( CK_{in} \), but this is not a concern since \( V_{VCO} \) is not directly used in the final output.
Figure 16.59 Use of a PLL to eliminate skew.

#### Example 16.13

Construct the voltage-domain counterpart of the loop shown in Fig. 16.59.

#### Solution

The buffer creates a constant phase shift in the signal generated by the VCO. The voltage-domain counterpart therefore assumes the topology shown in Fig. 16.60. We have

$$
\begin{equation*}
\left(V_{\text {in }}-V_{\text {out }}\right) A+V_{M}=V_{\text {out }} \tag{16.55}
\end{equation*}
$$

and hence

$$
\begin{equation*}
V_{\text {out }}=\frac{A V_{\text {in }}+V_{M}}{1+A} \tag{16.56}
\end{equation*}
$$

As $A \rightarrow \infty, V_{\text {out }} \rightarrow V_{\text {in }}$.
image_name:Figure 16.60
description:The circuit is a feedback amplifier with a voltage source VM adding to the output. The op-amp amplifies the difference between Vin and Vout, and VM shifts the output voltage.

We should note that the skew can be suppressed by a delay-locked loop as well. In fact, if frequency multiplication is not required, DLLs are preferred because they are less susceptible to noise.

### 16.5.3 Jitter Reduction

Recall from Sec. 16.3.2 that PLLs suppress fast jitter components at the input. For example, if a 1-GHz jittery signal is applied to a PLL having a bandwidth of 10 MHz , then input jitter components that vary faster than 10 MHz are attenuated. In a sense, the phase-locked loop operates as a narrowband filter centered around 1 GHz with a total bandwidth of 20 MHz . This is another important and useful property of PLLs.

Many applications must deal with jittery waveforms. Random binary signals experience jitter because of (1) crosstalk on the chip and in the package (Chapter 19), (2) package parasitics (Chapter 19), (3) additive electronic noise of devices, etc. Such waveforms are typically "retimed" by a low-noise clock so as to reduce the jitter. Illustrated in Fig. 16.61(a), the idea is to resample the midpoint of each bit by a D flipflop that is driven by the clock. However, in many applications, the clock may not be available independently. For example, an optical fiber carries only the random data stream, providing no separate clock waveform at the receive end. The circuit of Fig. 16.61(a) is therefore modified as shown in Fig. 16.61(b), where a "clock recovery circuit" (CRC) produces the clock from the data. Employing phase locking with a relatively narrow loop bandwidth, the circuit minimizes the effect of the input jitter on the recovered clock.
image_name:(a)
description：The diagram shows a D flip-flop circuit used for retiming data. The data input is a sinusoidal waveform, and the clock input is a square wave. The output is a retimed square wave. The circuit is used to synchronize the data with the clock signal, minimizing jitter.
image_name:(b)
description:
[
name: Clock Recovery Circuit, type: Other, ports: {N1: Din, N2: CK}
name: D Flip-Flop, type: Other, ports: {D: Din, CK: CK, Q: Vout}
]
extrainfo:The circuit diagram illustrates a clock recovery system using a D flip-flop. The Clock Recovery Circuit generates a clock signal from the input data signal Din, which is used to clock the D flip-flop. This setup helps in retiming the input data, reducing jitter and synchronizing it with the clock signal. The output is a retimed square wave signal Vout.

Figure 16.61 (a) Retiming data with D flipflop driven by a low-noise clock; (b) use of a phase-locked clock recovery circuit to generate the clock.
