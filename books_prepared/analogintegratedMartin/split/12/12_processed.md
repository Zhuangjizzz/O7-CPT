# 12 Continuous-Time Filters

Integrated analog filters can be realized in either discrete time or continuous time. Discrete-time filters and signal processing are addressed in Chapter 13 and their implementation, switched-capacitor circuits, are discussed in Chapter 14. In switched-capacitor circuits, although the signals remain continuous in voltage (i.e., they are never quantized) they require sampling in the time domain. Because of this time-domain sampling, the clock rate must always be at least twice that of the highest frequency being processed to eliminate aliasing. In fact, typically the clock rate is much greater than twice the signal bandwidth, to reduce the requirements of an anti-aliasing filter. As a result, switched-capacitor filters are limited in their ability to process high-frequency signals.

This chapter focuses on continuous-time filtering. As their name suggests, continuous-time filters have signals that remain continuous in time and that have analog signal levels. Since no sampling is required, continuous-time filters have a significant speed advantage over their switched-capacitor counterparts. However, continuous-time filters do have some disadvantages. One is their need for tuning circuitry. Tuning is required because their filter coefficients are determined by the product of two dissimilar elements, such as capacitance and resistance (or transconductance) values. Thus, whereas switched-capacitor filter coefficients are determined by capacitance ratios and therefore have accuracies of 0.1 percent, integrated continuous-time coefficients are initially set to only

Key Point: Continuous-time integrated analog filters process signals that are both continuous in amplitude and time. Discrete-time analog filters process signals sampled in time, and therefore generally operate on lower-frequency signals than their continuoustime counterparts.
about 30 -percent accuracy! Fortunately, tuning circuitry can set the filter coefficient accuracy to around 1 percent at the cost of more (and sometimes complex) circuitry, as we will see in Section 12.9. Another practical disadvantage exhibited by most continuous-time filters is their relatively poor linearity and noise performance. Although low-frequency switched-capacitor filters have been realized with nonlinear distortion and noise performance better than 90 dB , high-frequency continuous-time filters typically have distortion plus noise performance not much better than 60 dB (often it is much worse). However, there are numerous high-speed applications in which distortion and noise performances are not too demanding, such as many data communication and video circuits.

## 12.1 INTRODUCTION TO CONTINUOUS-TIME FILTERS

The basics of first- and second-order transfer functions were presented in Section 4.1. In analog filters, these transfer functions are realized by combinations of integrators, summers, and gain elements. These are the fundamental building blocks of integrated continuous-time filters. Combining these elements, any rational transfer function may be realized.

Key Point: Integrators, summers, and gain stages are the fundamental building blocks of analog filters.

Key Point: Any rational transfer function with real-valued coefficients may be factored into first- and second-order terms and, therefore, implemented as a cascade of first- and second-order filters.

Any rational transfer function with real-valued coefficients may be factored into first- and second-order terms that also have real-valued coefficients, so any order filter can be realized by cascading first- and second-order sections. Such a cascade is common in practice, and we therefore restrict ourselves to a discussion of first- and second-order filters here.

### 12.1.1 First-Order Filters

Key Point: One integrator is required for each pole in an analog filter.

A block diagram for a general first-order continuous-time filter is shown in Fig. 12.1. It is composed of one integrator, one summer, and up to three gain elements. In general, the number of integrators required is equal to the order of the desired transfer function.

It can be shown that the transfer function for this block diagram is given by

$$
\begin{equation*}
H(s) \equiv \frac{V_{\text {out }}(s)}{V_{\text {in }}(s)}=\frac{k_{1} s+k_{0}}{s+\omega_{0}} \tag{12.1}
\end{equation*}
$$

It has a real pole at a frequency $\omega_{0}$. To ensure the pole is in the left half of the s-plane, the value of $\omega_{0}$ must be positive. The dc gain is $H(0)=k_{0} / \omega_{0}$, and the gain at very high frequencies is $H(\infty)=k_{1}$.

### 12.1.2 Second-Order Filters

Second-order filters are also called biquadratic filters or biquads for short because in their most general form their transfer function is the ratio of two quadratic polynomials. The block diagram of a practical implementation is shown in Fig. 12.2. The transfer function for this second-order filter is given by
image_name:Fig. 12.1
description:The block diagram in Fig. 12.1 represents a general first-order continuous-time filter. It consists of the following main components:

1. **Input and Output Ports:**
- **Input Port:** Labeled as \( V_{in}(s) \), this is where the input signal enters the system.
- **Output Port:** Labeled as \( V_{out}(s) \), this is where the filtered output signal exits the system.

2. **Summing Junction:**
- The input signal \( V_{in}(s) \) is split into two paths. One path is directly fed into the summing junction, while the other path is multiplied by \( k_1 s \) before entering the summing junction.
- The summing junction adds the weighted input signal \( k_0 \) and the feedback signal from the output, which is multiplied by \(-\omega_0\).

3. **Integrator Block:**
- Represented by the block labeled \( 1/s \), this block integrates the signal from the summing junction. It is a key component in determining the system's dynamic behavior.

4. **Feedback Path:**
- A feedback loop is present, where the output \( V_{out}(s) \) is fed back into the summing junction after being multiplied by \(-\omega_0\). This feedback is crucial for setting the system's frequency response characteristics.

**Flow of Information:**
- The input \( V_{in}(s) \) is processed through two paths: one directly to the summing junction and the other through a gain \( k_1 s \).
- The summing junction combines these inputs with the feedback signal, producing a combined signal.
- This combined signal is then integrated by the \( 1/s \) block.
- The output of the integrator is \( V_{out}(s) \), which is also fed back into the system as part of the feedback loop.

**Overall System Function:**
- This system functions as a first-order filter, utilizing both feedforward and feedback paths to manipulate the input signal's frequency characteristics. The feedback loop, in particular, helps to determine the filter's stability and frequency response. The constants \( k_0 \), \( k_1 \), and \( \omega_0 \) are parameters that influence the gain and cutoff frequency of the filter. The arrangement of these components allows the system to modify the input signal into a desired output signal, emphasizing or attenuating specific frequency components.
image_name:Fig. 12.2
description:The block diagram in Fig. 12.2 represents a general second-order (biquadratic) continuous-time filter. This filter is designed to process an input signal \( V_{in}(s) \) and produce an output signal \( V_{out}(s) \) through a series of operations that involve both amplification and integration.

**Main Components:**
1. **Input Signal \( V_{in}(s) \):** This is the signal that enters the system and is subjected to filtering.
2. **Summing Junction:** The input signal \( V_{in}(s) \) is split and fed into a summing junction. Here, it is combined with two other signals: one scaled by \( k_0 \) and another scaled by \( k_1 s \).
3. **Gain Blocks:**
- **\( k_0 \) Gain Block:** This block scales the input signal by a constant factor \( k_0 \).
- **\( k_1 s \) Gain Block:** This block scales the input signal proportional to the complex frequency variable \( s \), effectively differentiating it.
4. **Integrator Block \( \frac{1}{s} \):** This block integrates the signal from the summing junction output. Integration in the Laplace domain is represented as division by \( s \).
5. **Feedback Path:** A feedback loop is created by feeding the output of the integrator back into the summing junction after being scaled by \(-\omega_0\).

**Flow of Information or Control:**
- The input \( V_{in}(s) \) is split into two paths. One path goes directly to the summing junction after being multiplied by \( k_0 \), and the other path is multiplied by \( k_1 s \) before reaching the summing junction.
- The summing junction combines these scaled inputs with the feedback signal, which is the output of the integrator scaled by \(-\omega_0\).
- The combined signal is then integrated by the \( \frac{1}{s} \) block, producing the output \( V_{out}(s) \).
- The feedback loop ensures that \( V_{out}(s) \) is continuously adjusted based on the difference between the input and the feedback signal, achieving the desired filter characteristics.

**Overall System Function:**
The primary function of this second-order filter is to modify the frequency characteristics of the input signal \( V_{in}(s) \) according to the specified transfer function. The arrangement of gain blocks, the integrator, and the feedback loop allows the filter to selectively enhance or attenuate certain frequency components, thereby shaping the output signal \( V_{out}(s) \) as required for specific applications.

Fig. 12.1 A block diagram of a general first-order continuous-time filter.
image_name:Fig. 12.2
description:The block diagram labeled "Fig. 12.2" represents a general second-order (biquadratic) continuous-time filter. This filter is designed to modify the frequency characteristics of an input signal \( V_{in}(s) \) and produce an output signal \( V_{out}(s) \) according to a specified transfer function.

Main Components:
1. **Summing Junctions**: There are two summing junctions in the diagram. The first one combines the input signal \( V_{in}(s) \) with feedback signals, and the second one combines the output from the first integrator with additional feedback.
2. **Integrators**: Two integrator blocks are present, each labeled with \( 1/s \). These are crucial for implementing the continuous-time filter.
3. **Feedback Paths**: Multiple feedback paths are present, each labeled with specific parameters \( -\omega_0, -\omega_0/Q \), and gains \( k_0/\omega_0, k_1, k_2s \).

Flow of Information or Control:
- The input signal \( V_{in}(s) \) is fed into the first summing junction, where it is combined with feedback signals.
- The output of the first summing junction is processed through the first integrator \( 1/s \), producing an intermediate signal.
- This intermediate signal is then fed into the second summing junction, where it is again combined with feedback signals.
- The output of the second summing junction is processed through the second integrator \( 1/s \), resulting in the output signal \( V_{out}(s) \).
- Feedback paths are used to control the characteristics of the filter, with specific gains applied at various points to shape the frequency response.

Labels, Annotations, and Key Indicators:
- **Gain Values**: The diagram includes gain values such as \( k_0/\omega_0, k_1, k_2s \), which are used to adjust the filter's response.
- **Feedback Parameters**: \( -\omega_0, -\omega_0/Q \) are used to define the feedback characteristics, crucial for determining the poles and zeros of the system.

Overall System Function:
The primary function of this second-order filter is to selectively enhance or attenuate certain frequency components of the input signal \( V_{in}(s) \). This is achieved through the arrangement of integrators, feedback loops, and gain blocks, which collectively define the transfer function \( H(s) \). The filter is capable of shaping the output signal \( V_{out}(s) \) to meet specific application needs, such as in audio processing, communication systems, or signal conditioning.

Fig. 12.2 A block diagram of a general second-order (biquadratic) continuous-time filter.

$$
\begin{equation*}
H(s) \equiv \frac{V_{\text {out }}(s)}{V_{\text {in }}(s)}=\frac{k_{2} s^{2}+k_{1} s+k_{0}}{s^{2}+\left(\frac{\omega_{0}}{Q}\right) s+\omega_{0}^{2}} \tag{12.2}
\end{equation*}
$$

The system's poles, like any linear system, can be determined by considering the system's undriven behavior, $\mathrm{V}_{\text {in }}=0$, and are therefore independent of the feed-in gains, $\mathrm{k}_{1,2,3}$. Two integrators are needed to realize the two poles. To ensure stability, $\omega_{0} / Q$ must be positive, which implies that one of the two integrators in Fig. 12.2 must have negative feedback around it, making it lossy. A large feedback coefficient $\omega_{0} / Q$ implies a very lossy integrator and, therefore, a low $Q$-factor. With $Q<1 / 2$ the two poles are real, whereas with $\mathrm{Q}>1 / 2$ the poles form a complex-conjugate pair arranged as illustrated in Fig. 4.9.

The numerator of (12.2) and hence the zeros of the biquad are determined by the feed-in gains $\mathrm{k}_{1,2,3}$. By omitting some of the feed-in branches of Fig. 12.2, it can be used to realize either low-pass, high-pass, or band-pass biquads.

#### EXAMPLE 12.1

Find the gain coefficients in the biquad of Fig. 12.2 required to realize a low-pass transfer function with a dc gain of $6 \mathrm{~dB}, Q=1 / \sqrt{2}$, and a $3-\mathrm{dB}$ bandwidth of $\omega_{3-\mathrm{dB}}=10^{6} \mathrm{rad} / \mathrm{sec}$.

#### Solution

A low-pass biquad is obtained with $\mathrm{k}_{1}=\mathrm{k}_{2}=0$.

$$
\begin{equation*}
H(s)=\frac{k_{0}}{s^{2}+\left(\frac{\omega_{0}}{Q}\right) s+\omega_{0}^{2}} \tag{12.3}
\end{equation*}
$$

The $3-\mathrm{dB}$ bandwidth is the frequency at which the magnitude of the denominator is $\sqrt{2}$ times larger than its dc value, which for $Q=1 / \sqrt{2}$ is the solution to

$$
\begin{align*}
\left|-\omega_{3-\mathrm{dB}}^{2}+\mathrm{j} \sqrt{2} \omega_{0} \omega_{3-\mathrm{dB}}+\omega_{\mathrm{o}}^{2}\right| & =\sqrt{2} \omega_{\mathrm{o}}^{2}  \tag{12.4}\\
\Rightarrow \omega_{3-\mathrm{dB}} & =\omega_{0}
\end{align*}
$$

Hence, in this case $\omega_{0}=10^{6}$. Finally, for a dc gain of $6 \mathrm{~dB}, \mathrm{k}_{0} / \omega_{0}^{2}=2 \Rightarrow \mathrm{k}_{0}=2 \omega_{0}^{2}$. The block diagram of Fig. 12.2 may be simplified somewhat by incorporating a gain $\omega_{0}$ into each integrator, resulting in the biquad of Fig. 12.3.

## 12.2 INTRODUCTION TO $\mathrm{G}_{\mathrm{m}}$-C FILTERS

This section gives a brief introduction to $\mathrm{G}_{\mathrm{m}}-\mathrm{C}$ filters. We will see here that the main circuit building blocks of $\mathrm{G}_{\mathrm{m}}-\mathrm{C}$ filters are transconductors. The basic functions of transconductors are described in this section, and circuit techniques for realizing transconductors are presented in the following sections.
image_name:Fig. 12.3
description:The diagram labeled "Fig. 12.3" represents a biquad filter, which is a type of second-order filter. This particular filter is implemented using the Gm-C (transconductance-capacitance) approach, commonly used in continuous-time analog filters.

Main Components:
1. **Input Signal (Vin(s)):** The system receives an input signal denoted as Vin(s).
2. **Summing Junctions:** There are two summing junctions in the system. The first one adds the input signal with feedback signals, and the second one processes the signal between the two integrators.
3. **Integrators:** Two integrator blocks are present:
- The first integrator has a transfer function of \(\omega_o/s = 10^6/s\).
- The second integrator also has the same transfer function \(\omega_o/s = 10^6/s\).
4. **Feedback Paths:** There are two feedback paths:
- A feedback path with a gain of \(-1\) loops from the output of the second integrator back to the input summing junction.
- Another feedback path with a gain of \(-1/Q = \sqrt{2}\) connects from the output of the first integrator to the second summing junction.
5. **Output Signal (Vout(s)):** The output signal is denoted as Vout(s).

Flow of Information or Control:
- The input signal Vin(s) enters the system through the first summing junction, where it is combined with feedback signals.
- The resultant signal is then processed by the first integrator, which outputs a signal that is fed forward to the second summing junction and also fed back with a gain of \(-1/Q = \sqrt{2}\) to the second summing junction.
- The second summing junction combines its inputs and sends the resultant signal to the second integrator.
- The output of the second integrator is fed back to the first summing junction with a gain of \(-1\) and also provides the final output signal Vout(s).

Labels, Annotations, and Key Indicators:
- The gain factor at the input is denoted as \(k_o/\omega_o^2 = 2\).
- The feedback gains are labeled as \(-1\) and \(-1/Q = \sqrt{2}\).
- Integrators are labeled with their transfer functions \(\omega_o/s = 10^6/s\).

Overall System Function:
The biquad filter is designed to process the input signal through a series of integrations and feedback loops to achieve a specific frequency response. The arrangement of integrators and feedback paths allows the filter to perform complex filtering operations, such as bandpass or low-pass filtering, depending on the specific configuration and values of the components.

Fig. 12.3 The biquad filter of Example 12.1.

### 12.2.1 Integrators and Summers

Key Point: In $\mathrm{G}_{\mathrm{m}}-\mathrm{C}$ filters, integrators are realized with a transconductor, which produces a output current proportional to the input voltage, and a capacitor, which integrates the current to produce the output voltage.

An integrator is the main building block for most continuous-time filters. To realize an integrator in $\mathrm{G}_{\mathrm{m}}-\mathrm{C}$ technology, a transconductor and a capacitor can be used as shown in Fig. 12.4. A transconductor is essentially a transconductance cell (an input voltage creates an output current) with the additional requirement that the output current be linearly related to the input voltage. Here, the output of the transconductor is the current $i_{0}$, and, in the ideal case, both the input and output impedance of this block are infinite. The output current is linearly related to the differential input voltage signal by

$$
\begin{equation*}
\mathrm{i}_{\mathrm{o}}=\mathrm{G}_{\mathrm{m}} \mathrm{v}_{\mathrm{i}} \tag{12.5}
\end{equation*}
$$

where $G_{m}$ is the transconductance of the cell. It should be re-emphasized that this relationship is different from that of an operational-transconductance amplifier (OTA) in that here, the output current should be linearly related to the input voltage. In addition, a transconductor should have a well-known (or at least controllable) transconductance value. In the case of an OTA, the transconductance does not necessarily need to be a linear function of the input voltage or a well-controlled value (though usually the transconductance value should be as large as possible).

This output current is applied to the integrating capacitor, $\mathrm{C}_{1}$, resulting in the voltage across $\mathrm{C}_{1}$ being given by

$$
\begin{equation*}
V_{o}=\frac{I_{0}}{s C_{1}}=\frac{G_{m} V_{i}}{s C_{1}} \tag{12.6}
\end{equation*}
$$

Defining $\omega_{\mathrm{ti}}$ to be the unity-gain frequency of the integrator, we can write

$$
\begin{equation*}
V_{o} \equiv\left(\frac{\omega_{i t}}{s}\right) V_{i}=\left(\frac{G_{m}}{s C_{i}}\right) V_{i} \tag{12.7}
\end{equation*}
$$

image_name:Fig. 12.4
description:The circuit is a single-ended Gm-C integrator. The input voltage vi is converted to a current io by the transconductor Gm. This current is then integrated by the capacitor C1, resulting in the output voltage vo. The integrator has infinite input and output resistances (Rin = ∞, Rout = ∞). The unity-gain frequency of the integrator is defined as ωti = Gm / C1.

Fig. 12.4 $A$ single-ended $G_{m}-C$ integrator.
image_name:Fig. 12.5
description::The circuit is a three-input, single-ended integrator/summer circuit. The output voltage Vo is the integration of the weighted sum of the input voltages V1, V2, and V3. The weights are determined by the transconductance values Gm1, Gm2, and Gm3, and the integration is performed by the capacitor C1. The output voltage is given by Vo = (1/sC1)(Gm1*V1 - Gm2*V2 + Gm3*V3).

Fig. 12.5 A three-input, single-ended integrator/summer circuit.

Thus, we see that the output voltage is equal to the integration of the differential input voltage multiplied by the integrator unity-gain frequency, which is given by

$$
\begin{equation*}
\omega_{\mathrm{ti}}=\frac{\mathrm{G}_{\mathrm{m}}}{\mathrm{C}_{1}} \tag{12.8}
\end{equation*}
$$

To realize a more general integrator/summer circuit, one need only connect multiple transconductors in parallel since the output currents all sum together. An example of a three-input integrator/summer circuit is shown in Fig. 12.5.

Key Point: Current signals are readily summed by simply shorting them together.

#### EXAMPLE 12.2

What transconductance is needed for an integrator that has a unity-gain frequency of 20 MHz , assuming a 2-pF integrating capacitor?

#### Solution

Rearranging (12.8), we have

$$
\begin{align*}
\mathrm{G}_{\mathrm{m}} & =2 \pi \times 20 \mathrm{MHz} \times 2 \mathrm{pF}  \tag{12.9}\\
& =0.251 \mathrm{~mA} / \mathrm{V}
\end{align*}
$$

Note that this transconductance value corresponds to

$$
\begin{equation*}
\mathrm{G}_{\mathrm{m}}=1 / 3.98 \mathrm{k} \Omega \tag{12.10}
\end{equation*}
$$

which, not surprisingly, is related to the unity-gain frequency by

$$
\begin{equation*}
2 \pi \times 20 \mathrm{MHz}=\frac{1}{3.98 \mathrm{k} \Omega \times 2 \mathrm{pF}} \tag{12.11}
\end{equation*}
$$

In other words, the required transconductance value is the inverse of the resistance value needed to form an RC time constant that corresponds to the desired unity-gain frequency.

### 12.2.2 Fully Differential Integrators

Key Point: Fully-differential circuits are often preferred in analog integrated circuits as they provide improved linearity and noise immunity.

Although the preceding blocks have all been shown with single-ended signals, ${ }^{1}$ in most integrated applications it is desirable to keep the signals fully differential. As discussed in Section 6.7, fully differential circuits have better noise immunity and distortion properties. Thus, fully differential circuits are the primary focus of the remainder of this chapter.

A fully differential transconductor has two outputs-one positive output (current flowing out for a positive input voltage) and one negative output (current flowing in for a positive input voltage). With this new degree of freedom (having two outputs instead of just one), a fully differential integrator can be realized in one of two ways, as shown in Fig. 12.6.

Note that the integrator shown in Fig. 12.6(a) requires one-fourth the capacitance needed for the integrator of Fig. $12.6(b)$ to achieve the same integrator coefficient. Although at first glance, this increase in size appears to be a disadvantage of the circuit shown in Fig. 12.6(b), it should be mentioned that fully differential circuits require some method of common-mode feedback. This requirement is due to the fact that, although the differential signal remains stable due to connections of the filter feedback network, the common-mode signal is free to drift if it is not also controlled using some feedback circuit. As a result, one must also be concerned with the stability of the common-mode feedback circuit. Since dominant pole compensation using capacitors on the output nodes is often used to stabilize the common-mode network, the integrator shown in Fig. $12.6(b)$ has the advantage that the integrating capacitors, $2 \mathrm{C}_{1}$, can also be used for this purpose. Also, recall that the single capacitor of the integrator shown in Fig. 12.6(a) must be realized using integrated capacitors, and thus top- and bottom-plate parasitic capacitances exist. Since the bottom-plate parasitic capacitance can be quite large (up to 20 percent of the capacitance value), to maintain symmetry, $\mathrm{C}_{1}$ is often realized using two parallel capacitors, as shown in Fig. 12.7. We take the parallel combination of the two capacitances,
image_name:(a)
description:
[
name: OpAmp, type: OpAmp, value: OpAmp, ports: {InP: vi+, InN: vi-, OutP: vo+, OutN: vo-}
name: C1, type: Capacitor, value: C1, ports: {Np: vo+, Nn: vo-}
]
extrainfo:The circuit is a fully differential Gm-C integrator with a single capacitor C1. The output voltage Vo is given by the equation Vo = Io/sC1 = GmVi/sC1, and the integrator's time constant is defined as ωti = Gm/C1. The diagram illustrates the relationship between the input voltage vi, output current io, and the transconductance Gm.
image_name:(b)
description:The circuit is a fully differential Gm-C integrator with two capacitors 2C1 connected to the output nodes Vo+ and Vo-. It is designed to provide an output voltage Vo = 2Io/(s(2C1)) = GmVi/(sC1), with a transconductance Gm and a time constant ωti = Gm/C1.

Fig. 12.6 Fully differential $\mathrm{G}_{\mathrm{m}}-\mathrm{C}$ integrators: (a) single capacitor, (b) two capacitors.

1. The transconductor input may be differential, but its output is single ended, and single-ended signals are typically applied to the transconductor inputs.
image_name:Fig. 12.7
description:
[
name: OpAmp, type: OpAmp, value: OpAmp, ports: {InP: vi+, InN: vi-, OutP: vo+, OutN: vo-}
name: C1, type: Capacitor, value: C1, ports: {Np: vo+, Nn: vo-}
name: Cp1, type: Capacitor, value: Cp, ports: {Np: vo+, Nn: GND}
name: Cp2, type: Capacitor, value: Cp, ports: {Np: vo-, Nn: GND}
]
extrainfo:The circuit is a fully differential Gm-C integrator with parasitic capacitances Cp. It provides an output voltage Vo = GmVi/(s(C1+Cp/2)) with a time constant ωti = Gm/(C1+Cp/2).

$$
v_{o}=\frac{G_{m} v_{i}}{s\left(C_{1}+C_{p} / 2\right)} \quad \omega_{t i}=\frac{G_{m}}{\left(C_{1}+C_{p} / 2\right)}
$$

Fig. 12.7 A fully differential integrator maintaining symmetry and showing parasitic capacitances.
image_name:Fig. 12.8
description:
[
name: C_X, type: Capacitor, value: C_X, ports: {Np: Vin, Nn: Vout(S)}
name: G_m1, type: OpAmp, value: G_m1, ports: {InP: Vin(s), InN: GND, Out: Vout(S)}
name: C_A, type: Capacitor, value: C_A, ports: {Np: Vout(S), Nn: GND}
name: G_m2, type: OpAmp, value: G_m2, ports: {InP: GND, InN: Vout(S), Out: Vout(S)}
]
extrainfo:The circuit is a single-ended first-order Gm-C filter. It includes a capacitor C_X and an op-amp G_m1 connected to the input voltage Vin(s). The capacitor C_A is connected to the output of G_m1 and the input of G_m2. The output voltage Vout(s) is taken from the output of G_m2. The values of C_X and G_m1 depend on the parameters k1 and k0, respectively.

Fig. 12.8 A single-ended first-order $\mathrm{G}_{m}-\mathrm{C}$ filter.
which equals $C_{1}$, and include the effect of the parasitic capacitances, $C_{p}$, to obtain the output voltage, given by

$$
\begin{equation*}
V_{o}=\frac{G_{m} V_{i}}{s\left(C_{1}+C_{p} / 2\right)} \tag{12.12}
\end{equation*}
$$

Thus, we see here that the parasitic capacitances affect the integration coefficient and must be taken into account.

### 12.2.3 First-Order Filter

A single-ended $\mathrm{G}_{\mathrm{m}}$-C filter that realizes the first-order filter depicted in Fig. 12.1 is shown in Fig. 12.8. Note that the gains in Fig. 12.1 are provided by the transconductors, the integration is performed by the capacitor $C_{A}$, and the capacitor $C_{x}$ corresponds to the differentiating feed-in path $\mathrm{k}_{1}$ in Fig. 12.1.

The transfer function for this first-order $\mathrm{G}_{\mathrm{m}}-\mathrm{C}$ filter is found by writing a cur-

Key Point: Differentiating signal paths are sometimes provided by capacitive feed-ins.
rent equation for the output node, $\mathrm{V}_{\text {out }}(\mathrm{s})$ :

$$
\begin{equation*}
G_{m 1} V_{\text {in }}(s)+s C_{x}\left[V_{\text {in }}(s)-V_{\text {out }}(s)\right]-s C_{A} V_{\text {out }}(s)-G_{m 2} V_{\text {out }}(s)=0 \tag{12.13}
\end{equation*}
$$

Rearranging to find $\mathrm{V}_{\text {out }}(\mathrm{s}) / \mathrm{V}_{\text {in }}(\mathrm{s})$, we have

$$
\begin{equation*}
\frac{V_{\text {out }}(s)}{V_{\text {in }}(s)}=\frac{s C_{x}+G_{m 1}}{s\left(C_{A}+C_{x}\right)+G_{m 2}}=\frac{\left[s\left(\frac{C_{X}}{C_{A}+C_{X}}\right)+\left(\frac{G_{m 1}}{C_{A}+C_{X}}\right)\right]}{\left[s+\left(\frac{G_{m 2}}{C_{A}+C_{X}}\right)\right]} \tag{12.14}
\end{equation*}
$$

image_name:Fig. 12.9
description:The circuit is a fully differential Gm-C filter. Gm1 and Gm2 are voltage-controlled current sources. Capacitors 2CX and 2CA form the filter structure. The equations provided define the relationships between the components' values and the filter parameters.

Fig. 12.9 A fully differential general first-order $G_{m}-C$ filter.
Equating (12.14) with (12.1) results in the following relationships:

$$
\begin{align*}
\mathrm{C}_{\mathrm{x}} & =\left(\frac{\mathrm{k}_{1}}{1-\mathrm{k}_{1}}\right) \mathrm{C}_{\mathrm{A}}  \tag{12.15}\\
\mathrm{G}_{\mathrm{m} 1} & =\mathrm{k}_{0}\left(\mathrm{C}_{\mathrm{A}}+\mathrm{C}_{\mathrm{x}}\right)  \tag{12.16}\\
\mathrm{G}_{\mathrm{m} 2} & =\omega_{0}\left(\mathrm{C}_{\mathrm{A}}+\mathrm{C}_{\mathrm{X}}\right) \tag{12.17}
\end{align*}
$$

It should be noted from (12.15) that, for $\mathrm{C}_{\mathrm{x}}$ to remain a positive value, the term $\mathrm{k}_{1}$ must satisfy $0 \leq \mathrm{k}_{1}<1$. What this restriction implies is that the shown circuit cannot realize a filter that has a high-frequency gain that is either negative or greater than 1 . Such a result should come as no surprise since the high-frequency gain of this circuit is simply a capacitor-divider circuit, and hence the restriction on $\mathrm{k}_{1}$.

Finally, the equivalent fully differential first-order $\mathrm{G}_{\mathrm{m}}-\mathrm{C}$ filter is shown in Fig. 12.9. Note that capacitor sizes are doubled here, in relation to the single-ended case, so that the same design equations occur. Also note that the same restriction holds on $\mathrm{k}_{1}$, although a negative value of $\mathrm{k}_{1}$ can be realized by cross-coupling the feed-in capacitor pair, $\mathrm{C}_{\mathrm{x}}$.

#### EXAMPLE 12.3

Based on Fig. 12.9, find component values for a first-order filter with a dc gain of 0.5 , a pole at 20 MHz , and a zero at 40 MHz . Assume the integrating capacitors are sized $\mathrm{C}_{\mathrm{A}}=2 \mathrm{pF}$.

#### Solution

A first-order filter with a zero at 40 MHz and a pole at 20 MHz is given by

$$
\begin{equation*}
\mathrm{H}(\mathrm{~s})=\frac{\mathrm{k}(\mathrm{~s}+2 \pi \times 40 \mathrm{MHz})}{(\mathrm{s}+2 \pi \times 20 \mathrm{MHz})} \tag{12.18}
\end{equation*}
$$

The leading coefficient is determined by setting the dc gain to 0.5 , resulting in $\mathrm{k}=0.25$. Thus, we have

$$
\begin{equation*}
\mathrm{H}(\mathrm{~s})=\frac{0.25 \mathrm{~s}+2 \pi \times 10 \mathrm{MHz}}{\mathrm{~s}+2 \pi \times 20 \mathrm{MHz}} \tag{12.19}
\end{equation*}
$$

and equating this transfer function to (12.1) results in

$$
\begin{gather*}
\mathrm{k}_{1}=0.25  \tag{12.20}\\
\mathrm{k}_{0}=2 \pi \times 10^{7}  \tag{12.21}\\
\omega_{0}=4 \pi \times 10^{7} \tag{12.22}
\end{gather*}
$$

image_name:Fig. 12.10
description:This is a fully differential Gm-C second-order filter. The circuit uses five voltage-controlled voltage sources (Gm1 to Gm5) and several capacitors (2CA, 2CB, 2CX) to achieve the desired filtering characteristics. The input is differential (Vin+ and Vin-) and the output is also differential (Vout+ and Vout-). The capacitors are connected in a manner to provide necessary feedback and filtering paths.

Fig. 12.10 A general second-order filter using fully differential $G_{m}-C$ techniques.

Using the design equations shown in Fig. 12.9, we find

$$
\begin{gather*}
\mathrm{C}_{\mathrm{x}}=2 \mathrm{pF} \times \frac{0.25}{1-0.25}=0.667 \mathrm{pF}  \tag{12.23}\\
\mathrm{G}_{\mathrm{m} 1}=2 \pi \times 10^{7} \times 2.667 \mathrm{pF}=0.168 \mathrm{~mA} / \mathrm{V}  \tag{12.24}\\
\mathrm{G}_{\mathrm{m} 2}=4 \pi \times 10^{7} \times 2.667 \mathrm{pF}=0.335 \mathrm{~mA} / \mathrm{V} \tag{12.25}
\end{gather*}
$$

where $\mathrm{C}_{\mathrm{A}}=2 \mathrm{pF}$, as given.

### 12.2.4 Biquad Filter

A fully-differential biquadratic $\mathrm{G}_{\mathrm{m}-} \mathrm{C}$ filter is shown in Fig. 12.10. The transfer function of this biquad filter is found to be given by

$$
\begin{equation*}
H(s) \equiv \frac{V_{\text {out }}(s)}{V_{\text {in }}(s)}=\frac{s^{2}\left(\frac{C_{x}}{C_{x}+C_{B}}\right)+s\left(\frac{G_{m 5}}{C_{x}+C_{B}}\right)+\left(\frac{G_{m 2} G_{m 4}}{C_{A}\left(C_{x}+C_{B}\right)}\right.}{s^{2}+s\left(\frac{G_{m 3}}{C_{x}+C_{b}}\right)+\left(\frac{G_{m 1} G_{m 2}}{C_{A}\left(C_{x}+C_{B}\right)}\right)} \tag{12.26}
\end{equation*}
$$

Equating the coefficients of (12.2) and (12.26) results in

$$
\begin{align*}
k_{2} & =\frac{C_{x}}{C_{X}+C_{B}}  \tag{12.27}\\
k_{1} & =\frac{G_{m 5}}{C_{x}+C_{B}}  \tag{12.28}\\
k_{0} & =\frac{G_{m 2} G_{m 4}}{C_{A}\left(C_{X}+C_{B}\right)} \tag{12.29}
\end{align*}
$$

and

$$
\begin{equation*}
\omega_{\circ}^{2}=\frac{G_{m 1} G_{m 2}}{C_{A}\left(C_{X}+C_{B}\right)} \tag{12.30}
\end{equation*}
$$

For Q, we note that

$$
\begin{equation*}
\frac{\omega_{o}}{Q}=\frac{G_{m 3}}{C_{x}+C_{b}} \tag{12.31}
\end{equation*}
$$

and so, by using (12.30), we can solve for $Q$, resulting in

$$
\begin{equation*}
Q=\sqrt{\left(\frac{G_{m 1} G_{m}}{G_{m 3}^{2}}\right)\left(\frac{C_{X}+C_{B}}{C_{A}}\right)} \tag{12.32}
\end{equation*}
$$

Although the preceding equations are for analyzing a given circuit, they can also be used for design, resulting in the following design equations:

$$
\begin{gathered}
C_{x}=C_{B}\left(\frac{k_{2}}{1-k_{2}}\right) \quad \text { where } 0 \leq k_{2}<1 \\
G_{m 1}=\omega_{0} C_{A} \quad G_{m 2}=\omega_{0}\left(C_{B}+C_{x}\right) \quad G_{m 3}=\frac{\omega_{0}\left(C_{B}+C_{x}\right)}{Q} \\
G_{m 4}=\left(k_{0} C_{A}\right) / \omega_{0} \quad G_{m 5}=k_{1}\left(C_{B}+C_{x}\right)
\end{gathered}
$$

Note that for this design, there is a restriction on the high-frequency gain coefficient, $\mathrm{k}_{2}$, similar to that occurring in the first-order case.

#### EXAMPLE 12.4

Find the transconductance and capacitor values for a second-order filter that has a bandpass response with a center frequency of 20 MHz , a $Q$ value of 5 , and a center frequency gain of 1 . Assume that $C_{A}=C_{B}=2 \mathrm{pF}$.

#### Solution

A bandpass transfer function has the form

$$
\begin{equation*}
H(s) \equiv \frac{V_{\text {out }}(s)}{V_{\text {in }}(s)}=\frac{G s \frac{\omega_{o}}{Q}}{s^{2}+s \frac{\omega_{o}}{Q}+\omega_{0}^{2}} \tag{12.33}
\end{equation*}
$$

where $G=1$ is the gain at the center frequency. Using the facts that $\omega_{0}=2 \pi \times 20 \mathrm{MHz}$ and $\mathrm{Q}=5$, we find

$$
\begin{equation*}
\mathrm{k}_{1}=\mathrm{G} \frac{\omega_{0}}{\mathrm{Q}}=2.513 \times 10^{7} \mathrm{rad} / \mathrm{s} \tag{12.34}
\end{equation*}
$$

Since $k_{0}$ and $k_{2}$ are zero, we have $C_{x}=G_{m 4}=0$ and

$$
\begin{gather*}
G_{m 1}=\omega_{0} C_{A}=0.2513 \mathrm{~mA} / \mathrm{V}  \tag{12.35}\\
G_{m 2}=\omega_{0}\left(C_{B}+C_{x}\right)=0.2513 \mathrm{~mA} / \mathrm{V} \tag{12.36}
\end{gather*}
$$

and, in this case,

$$
\begin{equation*}
\mathrm{G}_{\mathrm{m} 3}=\mathrm{G}_{\mathrm{m} 5}=\mathrm{k}_{1} \mathrm{C}_{\mathrm{B}}=50.27 \mu \mathrm{~A} / \mathrm{V} \tag{12.37}
\end{equation*}
$$

## 12.3 TRANSCONDUCTORS USING FIXED RESISTORS

Two similar approaches for using resistors to linearize the relationship between differential input voltage and output current of a differential pair of transistors are shown in Fig. 12.11. To understand the basic operation of the two circuits, we first make the simplifying assumption that the $\mathrm{V}_{\mathrm{gs}}$ voltages of the transistors are constant. As a result, we see that the differential input voltage, $\mathrm{v}_{\mathrm{i}}$, appears across the two $\mathrm{R}_{\mathrm{S}} / 2$ resistors in Fig. 12.11(a) and across $R_{S}$ in Fig. 12.11(b). Thus, the drain current $I_{D 1}$ is given by

$$
\begin{equation*}
I_{D 1}=I_{1}+\frac{v_{i}}{R_{S}} \tag{12.38}
\end{equation*}
$$

and the drain current $I_{D 2}$ is given by

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D} 2}=\mathrm{I}_{1}-\frac{\mathrm{v}_{\mathrm{i}}}{\mathrm{R}_{\mathrm{S}}} \tag{12.39}
\end{equation*}
$$

Then defining $\mathrm{i}_{01}$ to be the difference in the drain currents from $I_{1}$ (as shown), we have

$$
\begin{equation*}
\mathrm{i}_{01}=\frac{v_{i}}{R_{S}} \tag{12.40}
\end{equation*}
$$

image_name:(a)
description:
[
name: Q1, type: NMOS, ports: {S: s1, D: x2, G: ViP}
name: Q2, type: NMOS, ports: {S: s2, D: x3, G: Vin}
name: Rs/2, type: Resistor, value: Rs/2, ports: {N1: s1, N2: x1}
name: Rs/2, type: Resistor, value: Rs/2, ports: {N1: s2, N2: x1}
name: 2I1, type: CurrentSource, value: 2I1, ports: {Np: x1, Nn: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vcc, Nn: x2}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vcc, Nn: x3}
]
extrainfo:The circuit in (a) is a differential pair with source degeneration resistors Rs/2, which linearizes the relationship between differential input voltage (vi) and output current (io1). The bias currents flow through the Rs/2 resistors, affecting common-mode range and output swing. The transconductance Gm is determined by the formula Gm = 1 / (2/gm1 + Rs).
image_name:(b)
description:
[
name: Q1, type: NMOS, ports: {S: X1, D: P1, G: Vip}
name: Q2, type: NMOS, ports: {S: X2, D: P2, G: Vin}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vcc, Nn: P1}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vcc, Nn: P2}
name: Rs, type: Resistor, value: Rs, ports: {N1: X1, N2: X2}
name: I1, type: CurrentSource, value: I1, ports: {Np: X1, Nn: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: X2, Nn: GND}
]
extrainfo:The circuit (b) is a differential pair with source degeneration using a resistor Rs. It consists of two NMOS transistors Q1 and Q2, each with a current source I1 connected to their drains, and a resistor Rs connecting their sources. The circuit is designed for improved linearity in the transconductance by using source degeneration.

Fig. 12.11 Fixed transconductors using resistors. The circuit in (a) has smaller common-mode range and output swing than the circuit in (b) due to bias currents flowing through the $\mathrm{R}_{\mathrm{S}} / 2$ resistors.

Key Point: Source-degenerating a differential pair with a resistor linearizes the relationship between differential input voltage and output current. The result is a transconductor with a value approximately equal to the degeneration resistance.

Thus, we see that the transconductance of these two differential input circuits is a fixed value of $1 / R_{S}$. One important difference between the two fixed transconductors of Fig. 12.11 is that, in the case of $v_{i}=0$, a bias current of $I_{1}$ flows through the two $R_{S} / 2$ resistors in Fig. 12.11(a), whereas no bias current is flowing through $\mathrm{R}_{\mathrm{S}}$ in Fig. 12.11(b). As a result, the common-mode voltage of Fig. $12.11(b)$ can be closer to ground. For example, if a bias current of $I_{1}=100 \mu \mathrm{~A}$ is used together with $R_{S}=20 \mathrm{k} \Omega$, then the voltage drop across each of the two $R_{S} / 2$ resistors would result in 1 V less of common-mode range. It should be noted here that the common-mode input voltage must be far enough above ground to account for the largest expected differential input voltage, $v_{i}$. Specifically, one must ensure that the circuit remains functional while the gate on one side of the differential pair is lower than the common-mode voltage by $\mathrm{v}_{\mathrm{i}} / 2$.

A simple estimate of the maximum differential input range for both these circuits can be found by determining how much voltage exists across the linearizing resistors at the point where one transistor just turns off. For example, in Fig. $12.11(a)$, when $Q_{2}$ turns off due to a large positive input voltage, all of $2 I_{1}$ flows through $R_{s} / 2$ on the left and nothing flows through $R_{s} / 2$ on the right. Thus, the voltage at the center of the two resistors equals that of the source of $Q_{2}$ (since no current flows right), and the maximum input voltage equals that voltage across the left $R_{S} / 2$ resistor, giving

$$
\begin{equation*}
V_{i, \max }=I_{1} R_{S} \tag{12.41}
\end{equation*}
$$

A similar argument gives the same maximum input voltage for the circuit of Fig. 12.11(b). It should be noted here that this simple estimate does not take into account that significant distortion occurs when this maximum input voltage is applied. Specifically, at $\mathrm{V}_{\mathrm{i}, \max }=\mathrm{I}_{1} \mathrm{R}_{\mathrm{S}}$, one of the two transistors will be off, implying that $\mathrm{V}_{\mathrm{Gs}}$ has not remained a relatively constant value, as we assumed earlier in this section. Typically, the maximum input range that applies to the preceding fixed transconductors might be one-half that of (12.41), or, equivalently, $\left(I_{1} / 2\right) R_{S}$.

So far, we have assumed that the transistor's $\mathrm{V}_{\mathrm{gs}}$ voltages remain constant. Such an assumption is reasonably valid if the MOSFETs are replaced by bipolar transistors as shown in Fig. 12.12 due to the exponential currentvoltage relationship of bipolar transistors. However, it is less accurate with a MOFET differential pair, whose
image_name:(a)
description:This is a bipolar differential pair circuit with resistive degeneration. The circuit utilizes NPN transistors Q1 and Q2 with emitter degeneration resistors RS/2, and a tail current source 2I1. The input voltage Vi is applied to the base of Q1.
image_name:(b)
description:The circuit diagram (b) is a differential amplifier with two NPN transistors (Q1 and Q2). It uses current sources to bias the transistors and a resistor RS to set the transconductance. The circuit is designed to amplify the input voltage Vi.

Fig. 12.12 Bipolar implementations of the transconductors shown in Fig. 12.11.
gate-source voltage changes appreciably with input voltage. In either the MOS or bipolar circuits, the assumption is reasonable when one restricts the minimum drain (or collector) current, $\mathrm{I}_{\mathrm{D}, \mathrm{min}}$, in either transistor to be that which keeps the small-signal transconductance, $g_{m}$, large enough to ensure $1 / g_{m}<<R_{S}$, recalling that

$$
\begin{equation*}
g_{m}=\sqrt{2 \mu_{n} C_{o x}(W / L) I_{D}} \gg 1 / R_{S} \tag{12.42}
\end{equation*}
$$

For the bipolar circuit, we have the simpler requirement,

$$
\begin{equation*}
\mathrm{r}_{\mathrm{e}, \max }=\frac{\mathrm{V}_{\mathrm{T}}}{\mathrm{I}_{\mathrm{E}, \min }} \ll \mathrm{R}_{\mathrm{S}} \tag{12.43}
\end{equation*}
$$

or equivalently,

$$
\begin{equation*}
I_{E, \min }>>\frac{V_{T}}{R_{S}} \tag{12.44}
\end{equation*}
$$

For example, if $R_{S}=20 \mathrm{k} \Omega$ and $\mathrm{V}_{\mathrm{T}}=25 \mathrm{mV}$, the minimum emitter current in either transistor should be much greater than $1.25 \mu \mathrm{~A}$. A good question is, How much is "much greater than"? The answer to this question depends on how much distortion can be tolerated since, when $1 / g_{m}$ becomes a comparable size to $R_{S}$, the varying $\mathrm{V}_{\mathrm{gs}}$ or $\mathrm{V}_{\mathrm{be}}$ voltage will result in the output current, $i_{o}$, being a significant nonlinear function of the input voltage, $v_{i}$. For example, if the maximum value of $1 / g_{m}$ goes to 10 percent of that of $R_{S}$ when the maximum applied input voltage is $\left(I_{1} / 2\right) R_{S}$, then a linearity deviation of about 3 percent occurs. Thus, to attain a high linearity with the preceding circuits, the bias currents should be large and the input signal should be small (to ensure large values of $\mathrm{g}_{\mathrm{m}}$ ). Of course, the use of small input signals may result in noise becoming a problem.

In applications in which a moderate amount of nonlinearity can be tolerated, $\mathrm{R}_{\mathrm{S}}$ might be chosen similar in size to the nominal bias value of $1 / \mathrm{g}_{\mathrm{m}}$. In this case, the overall transconductance of this transconductor is most easily found using the hybrid T model for the input transistor pair. With such an approach, the output current is more accurately described by

$$
\begin{equation*}
i_{01}=\frac{v_{i}}{1 / g_{m 1}+R_{S}+1 / g_{m} 2}=\frac{v_{i}}{2 / g_{m}+R_{s}} \tag{12.45}
\end{equation*}
$$

Note that (12.45) reduces to (12.40) when $R_{S}$ is chosen much larger than $2 / g_{m}$. In summary, a more accurate formula for the transconductance of the circuits of Fig. 12.11 (and Fig. 12.12) is

$$
\begin{equation*}
G_{m}=\frac{i_{o 1}}{v_{i}}=\frac{1}{2 / g_{m}+R_{s}} \tag{12.46}
\end{equation*}
$$

#### EXAMPLE 12.5

Consider the circuit of Fig. $12.12(b)$, where $R_{S}=3 \mathrm{k} \Omega$ (such that $G_{m} \approx 0.333 \mathrm{~mA} / \mathrm{V}$ ) and the maximum differential input voltage is $\pm 500 \mathrm{mV}$. Choose an appropriate bias current, $I_{1}$, such that $r_{e, \max }<0.1 R_{s}$, and find a more precise value for $G_{m}$. Find the new value of $I_{1}$ and $G_{m}$ if the constraint $r_{e, \max }<0.01 R_{s}$ is used instead.

#### Solution

In the first case, we have $r_{\mathrm{e}, \max }<0.1 \mathrm{R}_{\mathrm{s}}=300 \Omega$. Thus, in the case of $\mathrm{v}_{\mathrm{i}}=500 \mathrm{mV}$, we require that $\mathrm{r}_{\mathrm{e} 2} \approx 300 \Omega$, which is attained for an emitter current of

$$
\begin{equation*}
\mathrm{I}_{\mathrm{E} 2, \min }=\frac{\mathrm{V}_{\mathrm{T}}}{\mathrm{r}_{\mathrm{e}, \max }}=\frac{26 \mathrm{mV}}{300 \Omega}=86.7 \mu \mathrm{~A} \tag{12.47}
\end{equation*}
$$

For this same input voltage, the resistor current is approximately

$$
\begin{equation*}
\mathrm{I}_{\mathrm{RE}} \cong \frac{500 \mathrm{mV}}{3 \mathrm{k} \Omega}=167 \mu \mathrm{~A} \tag{12.48}
\end{equation*}
$$

and since the current through $R_{s}$ plus $I_{\mathrm{E} 2}$ must equal $I_{1}$ (according to the node currents at the emitter of $Q_{2}$ ), we have

$$
\begin{equation*}
I_{1}=167+86.7=253 \mu \mathrm{~A} \tag{12.49}
\end{equation*}
$$

In other words, a minimum bias current of $253 \mu \mathrm{~A}$ should be chosen. For this value of bias current, the nominal value of $r_{e}$ is given by

$$
\begin{equation*}
\mathrm{r}_{\mathrm{e}}=\frac{\mathrm{V}_{\mathrm{T}}}{\mathrm{I}_{1}}=103 \Omega \tag{12.50}
\end{equation*}
$$

resulting in

$$
\begin{equation*}
\mathrm{G}_{\mathrm{m}}=\frac{1}{\left(2 \mathrm{r}_{\mathrm{e}}+\mathrm{R}_{\mathrm{s}}\right)}=0.312 \mathrm{~mA} / \mathrm{V} \tag{12.51}
\end{equation*}
$$

For the case $r_{e, \max }<0.01 R_{E}$, one finds $I_{1}=1.03 \mathrm{~mA}$ and $G_{m}=0.328 \mathrm{~mA} / V$. Note here that the nominal value of $r_{e}$ is now only $26 \Omega$, which is significantly less than $R_{s}$. Although this second design will have less distortion than the first (about 10 times better), it uses much more power. Next, we look at using feedback to improve distortion without resorting to large bias currents.

One way to improve the distortion properties of the preceding fixed transconductors without using large bias currents and small input signal levels is to use an extra pair of amplifiers, as shown in Fig. 12.13. Here, the virtual ground in each opamp forces the source voltages of $Q_{1}$ and $Q_{2}$ to equal those of $v_{i}^{+}$and $v_{i}^{-}$. As a result, the input voltage appears directly across $R_{s}$ and does not depend on the $V_{g s}$ voltages of $Q_{1}$ and $Q_{2}$. Thus, the transconductance of this circuit is given by

$$
\begin{equation*}
G_{m}=\frac{i_{o 1}}{v_{i}^{+}-v_{i}^{-}}=\frac{1}{R_{S}} \tag{12.52}
\end{equation*}
$$

It should be mentioned here that the opamps can be quite simple (typically, a single stage) because they merely improve an input stage that is already reasonably linear.
image_name:Fig. 12.13
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Vi+, InN: InN(A1), OutP: Out(A1)}
name: A2, type: OpAmp, value: A2, ports: {InP: Vi-, InN: InN(A2), OutP: Out(A2)}
name: Q1, type: NMOS, ports: {S: InN(A1), D: P1, G: Out(A1)}
name: Q2, type: NMOS, ports: {S: InN(A2), D: P2, G: Out(A2)}
name: RS, type: Resistor, value: RS, ports: {N1: InN(A1), N2: InN(A2)}
name: I1, type: CurrentSource, value: I1, ports: {Np: VCC, Nn: P1}
name: I1, type: CurrentSource, value: I1, ports: {Np: VCC, Nn: P2}
name: I1, type: CurrentSource, value: I1, ports: {Np: InN(A1), Nn: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: InN(A1), Nn: GND}
]
extrainfo:The circuit uses opamps A1 and A2 to improve the linearity of a fixed transconductor by controlling the gates of NMOS transistors Q1 and Q2. The transconductance is determined by the resistor RS, and constant currents are maintained through Q1 and Q2 by current sources I1. The input voltage is applied differentially across the opamps, and the output is taken at the nodes P1 and P2.

Fig. 12.13 Improving the linearity of a fixed transconductor through the use of opamps.

Another method for improving the linearity of a fixed transconductor is to force constant currents through $\mathrm{Q}_{1}$ and $\mathrm{Q}_{2}$, as shown in Fig. 12.14 for a bipolar input pair [Koyama, 1993]. Here, $I_{1}$ flows through each of $Q_{1}$ and $Q_{2}$ so that $V_{\text {be1 }}$ and $V_{\text {be2 }}$ are fixed, while $Q_{3}$ and $Q_{4}$ have varying collector currents corresponding to the current flow through $R_{s}$. The output currents can then be obtained at the collectors of $\mathrm{Q}_{7}$ and $\mathrm{Q}_{8}$, which mirror the current through $Q_{3}$ and $Q_{4}$. Thus, assuming the current mirror transistors consisting of $Q_{7}$ and $Q_{8}$ are equal in size to those of $Q_{3}$ and $Q_{4}$, the transconductance of this cell is given by

$$
\begin{equation*}
G_{m}=\frac{i_{01}}{v_{i}^{+}-v_{i}^{-}}=\frac{1}{R_{s}} \tag{12.53}
\end{equation*}
$$

If the current mirror transistors are scaled in relation to $Q_{3}$ and $Q_{4}$, then the transconductance for this cell is also scaled by the same amount.

It should be noted that simple diode-connected transistors are not used at $Q_{3}$ and $Q_{4}$ since a feedback circuit is required to set the voltage level at the collectors of $Q_{1}$ and $Q_{2}$ without drawing much current. The feedback loop occurs as follows: If the voltage at the collector of $Q_{1}$ increases because $I_{C 1}$ is less than $I_{1}$, then $V_{\text {be3 }}$ also increases, forcing more current through $Q_{3}$ and $Q_{1}$ until $I_{C 1}$ once again equals $I_{1}$. Although the circuit shown results in each of $Q_{1}$ and $Q_{2}$ collector voltages being set to two diode drops above ground (i.e., $V_{\text {be3 }}+V_{\text {be } 5}$ ), a larger voltage can be obtained by adding diode-connected transistors that operate as voltage level-shifters. It is possible to combine parts of this fixed-transconductor circuit with a gain-cell stage, as was done in [Koyama, 1993]. The same linearization technique has been used in a CMOS variable transconductor that will be presented in Section 12.4.1, where the resistance $R_{S}$ is realized using a MOS transistor operating in the triode region [Welland, 1994].

A problem with the transconductors shown so far is that there is no obvious mechanism for tuning the transconductance to ensure accuracy over process, voltage, and temperature variations. One solution is to provide an array of degeneration resistors $\mathrm{R}_{\mathrm{S}}$ and somehow select the most appropriate value using switches. Alternatively, triode devices may be used in series with or in place of $\mathrm{R}_{\mathrm{S}}$, and their gate voltage used to tune the effective source degeneration. This is the topic of the following section.
image_name:Fig. 12.14
description:The circuit is a transconductor that uses feedback to maintain a constant Vbe voltage for Q1 and Q2, improving linearity. It includes equal-sized current mirrors and degeneration resistors for tuning transconductance.

Fig. 12.14 Improving the linearity of a fixed transconductor by maintaining a constant $\mathrm{V}_{\text {be }}$ voltage for $Q_{1}$ and $Q_{2}$. Level shifts should be added at the emitters of $Q_{5}, Q_{6}$ if a larger input range is desired.

Key Point: Feedback may be used to more accurately reproduce the input voltage across the degeneration resistor or further improve the linearity of transconductors with fixed resistors.

## 12.4 CMOS TRANSCONDUCTORS USING TRIODE TRANSISTORS

In this section, we discuss transconductor circuit techniques that rely on transistors operating in the triode region. It should be stated here that in the following circuits, not all transistors are in the triode region. As we will see, most of the transistors are biased in the active region, but the transconductance of the circuit relies on one or two key transistors biased in the triode region.

We begin this section by recalling the classical model equation for an $n$-channel transistor operating in the triode region.

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D}}=\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)\left[\left(\mathrm{V}_{\mathrm{GS}}-\mathrm{V}_{\mathrm{tn}}\right) \mathrm{V}_{\mathrm{DS}}-\frac{\mathrm{V}_{\mathrm{DS}}^{2}}{2}\right] \tag{12.54}
\end{equation*}
$$

Also recall that a transistor remains in the triode region as long as the drain-source voltage is lower than the effective gate-source voltage. In other words, the following condition must be satisfied:

$$
\begin{equation*}
V_{D s}<V_{\text {eff }} \quad \text { where } V_{\text {eff }}=V_{G S}-V_{t n} \tag{12.55}
\end{equation*}
$$

We will see next that if the preceding equations were exact, then perfectly linear circuits could be realized. However, these equations are only mildly accurate for a modern short-channel process, and therefore some distortion occurs because higher-order terms are not modelled in the preceding equations. Hence, almost all practical continuous-time circuits use fully differential architectures to reduce even-order distortion products, leaving the third-order term to dominate.

### 12.4.1 Transconductors Using a Fixed-Bias Triode Transistor

We see from (12.54) that if a small drain-source voltage, $\mathrm{V}_{\mathrm{DS}}$, is used, the $\mathrm{V}_{\mathrm{DS}}^{2}$ term goes to zero quickly and the drain current is approximately linear with respect to an applied drain-source voltage. Thus, we can model a transistor in triode as a resistor given by

$$
\begin{equation*}
\left.r_{D S} \equiv\left(\frac{\partial i_{D}}{\partial v_{D S}}\right)^{-1}\right|_{v_{D S}=0} \tag{12.56}
\end{equation*}
$$

which results in a small-signal resistance of

$$
\begin{equation*}
r_{D S}=\frac{1}{\mu_{\mathrm{n}} C_{o x}\left(\frac{W}{L}\right)\left(V_{G S}-V_{\mathrm{tn}}\right)} \tag{12.57}
\end{equation*}
$$

Key Point: Triode transistors can be used in placed of fixed resistors to make transconductors tunable, although their linearity is generally reduced.

One approach for using this equivalent resistance to realize a transconductor with moderate linearity is shown in Fig. 12.15 [Welland, 1994]. This circuit has the same structure as that of the bipolar circuit of Fig. 12.14. However, here the bipolar transistors are replaced with their MOSFET counterparts (biased in the active region), and the resistor is replaced with a transistor operating in the triode region. Note that the circuit of Fig. 12.15 forces constant currents through $\mathrm{Q}_{1}$ and $\mathrm{Q}_{2}$ (as in the bipolar case) such that their individual gate-source voltages remain
image_name:Fig. 12.15
description:The circuit is a CMOS transconductor using Q9 in the triode region. It forces constant currents through Q1 and Q2, maintaining their gate-source voltages constant. The transconductance Gm is related to the small-signal resistance of Q9.

Fig. 12.15 A CMOS transconductor using $Q_{9}$ in the triode region.
constant. As a result, the transconductance of this cell is equal to the inverse of the small-signal resistance, $r_{d s}$, of $Q_{9}$. Using the small-signal resistance result of (12.57), the overall transconductance of this cell is given by

$$
\begin{equation*}
\mathrm{G}_{\mathrm{m}}=\frac{\mathrm{i}_{\mathrm{ol}}}{\mathrm{v}_{\mathrm{i}}^{+}-\mathrm{v}_{\mathrm{i}}^{-}}=\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)_{9}\left(\mathrm{~V}_{\mathrm{gs} 9}-\mathrm{V}_{\mathrm{tn}}\right) \tag{12.58}
\end{equation*}
$$

Thus, this transconductor has a variable transconductance value that can be adjusted by changing the value of $V_{\text {gs9. }}$. As in the bipolar case, this transconductance value can be scaled by scaling the current mirrors $Q_{7}$ and $Q_{8}$ with respect to $Q_{3}$ and $Q_{4}$.

A similar approach but with reduced complexity and fewer p -channel inputs is shown in Fig. 12.16 [Kwan, 1991]. Here, a constant current of $I_{2}$ is forced through each of $Q_{1}$ and $Q_{2}$, whereas the dc bias current for each of $Q_{3}$ and $Q_{4}$ equals the difference between $I_{1}$ and $I_{2}$. The signal current, $i_{11}$, also flows through $Q_{3}$ and $Q_{4}$, which is mirrored to the output transistors, $Q_{5}$ and $Q_{6}$. Note that this configuration has one less transistor stage around the input transistor loops. Specifically, the $Q_{5}$ and $Q_{6}$ source followers shown in Fig. 12.15 are not required in the circuit of Fig. 12.16, which usually results in a speed advantage for the latter.

An advantage of the transconductors in Figs. 12.15 and 12.16 (and other similar ones) is that they are easily modified to have multiple outputs by simply including additional output transistors. For example, the transconductor in Fig. 12.16 with two outputs is shown in Fig. 12.17. These additional transistors can be scaled for any desired ratio of output currents. These multiple outputs often allow filters to be realized using fewer transconductors. For example, a biquad similar to that in Fig. 12.10, but using multiple-output transconductors, is shown in Fig. 12.18. The transconductors are now associated with the outputs rather than the inputs. There is one transconductor per filter order plus an additional one for the input conversion from voltage to current. This approach has resulted in a savings of two transconductors. Not only does this approach save die area, but, often more importantly, it saves power.
image_name:Fig. 12.16 A CMOS transconductor with p-channel inputs
description:The circuit is a CMOS transconductor with p-channel inputs, featuring multiple PMOS and NMOS transistors. The PMOS transistors Q1 and Q2 are used to control the current flow into nodes p1 and p2, respectively. NMOS transistors Q3, Q4, Q5, and Q6 provide the differential pair and load functions. Q7 is used as a current mirror. Current sources I1 and I2 provide biasing currents. The circuit is designed to operate with differential input voltages Vi+ and Vi-.

Fig. 12.16 A CMOS transconductor with p-channel inputs.
image_name:Fig. 12.16 A CMOS transconductor with p-channel inputs
description:he circuit is a CMOS transconductor with p-channel inputs. It features differential inputs Vi+ and Vi-, and uses PMOS transistors Q1 and Q2 for controlling current flow. The current mirror is formed by Q7. NMOS transistors Q3 and Q4 serve as a differential pair, while Q5 and Q6 act as loads. Current sources I1 and I2 provide biasing currents. The transconductance Gm is given by the equation Gm = μpCox(W/L)7(Vsg7 - |Vtp|).

Fig. 12.17 A multiple-output CMOS transconductor.

### 12.4.2 Transconductors Using Varying Bias-Triode Transistors

Another way to linearize a MOSFET differential stage, using transistors primarily in the triode region, is shown in Fig. 12.19 [Krummenacher, 1988]. Note that here the gates of transistors $Q_{3}, Q_{4}$ are connected to the differential input voltage rather than to a bias voltage. As a result, triode transistors $Q_{3}$ and $Q_{4}$ undergo varying bias conditions to improve the linearity of this circuit (as discussed shortly). To see that $Q_{3}$ and $Q_{4}$ are generally in the triode region, we look at the case of equal input signals (i.e., $v_{1}=v_{2}$ ), resulting in

$$
\begin{equation*}
v_{x}=v_{y}=v_{1}-v_{G S 1}=v_{1}-\left(v_{\text {eff } 1}+V_{t \mathrm{t}}\right) \tag{12.59}
\end{equation*}
$$

Thus, the drain-source voltages of $Q_{3}, Q_{4}$ are both zero. However, their gate-source voltages equal those of $\mathrm{Q}_{1}, \mathrm{Q}_{2}$, implying that they are indeed in the triode region.
image_name:Fig. 12.18 A general biquad realized using multiple-output transconductors.
description:The circuit is a general biquad filter realized using multiple-output transconductors. It consists of three operational amplifiers (Gm1, Gm2, Gm3) and capacitors (2CA, 2CB, 2CX). The configuration allows for differential input (Vin+, Vin-) and differential output (Vout+, Vout-). The capacitors 2CA and 2CB are connected to ground, while 2CX connects the input to the output nodes, providing feedback and frequency-dependent response.

Fig. 12.18 A general biquad realized using multiple-output transconductors.
image_name:Fig. 12.19
description:
[
name: Q1, type: NMOS, ports: {S: Vx, D: P, G: V1}
name: Q2, type: NMOS, ports: {S: Vy, D: P2, G: V2}
name: Q3, type: NMOS, ports: {S: Vy, D: Vx, G: V1}
name: Q4, type: NMOS, ports: {S: Vy, D: Vx, G: V2}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vx, Nn: -VEE}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vy, Nn: -VEE}
]
extrainfo:The circuit is a linearized CMOS differential pair using NMOS transistors Q3 and Q4 in the triode region. The current sources are set equal to maintain common-mode feedback. The transconductance Gm is given by the formula shown in the diagram.

Fig. 12.19 A linearized CMOS differential pair using transistors $Q_{3}, Q_{4}$ primarily in the triode region. The top pair of current sources can be set equal to the bottom pair through the use of a common-mode feedback.

To determine the small-signal transconductance of this stage, we note from (12.57) that the small-signal drain-source resistance of $Q_{3}, Q_{4}$ is given by

$$
\begin{equation*}
r_{\mathrm{ds} 3}=r_{\mathrm{ds} 4}=\frac{1}{2 \mathrm{k}_{3}\left(\mathrm{~V}_{\mathrm{GS} 1}-\mathrm{V}_{\mathrm{tn}}\right)} \tag{12.60}
\end{equation*}
$$

where we have assumed that $Q_{3}$ and $Q_{4}$ are matched devices and have defined

$$
\begin{equation*}
\mathrm{k}_{3}=\frac{\mu_{\mathrm{n}} \mathrm{Cox}_{\mathrm{ox}}}{2}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)_{3} \tag{12.61}
\end{equation*}
$$

Note that in this circuit we cannot ignore the effect of the varying gate-source voltages of $Q_{1}$ and $Q_{2}$ since their drain currents are not fixed to a constant value (as in Fig. 12.15). The small-signal source resistance values of $Q_{1}$ and $Q_{2}$ are given by

$$
\begin{equation*}
r_{s 1}=r_{s 2}=\frac{1}{g_{m 1}}=\frac{1}{2 k_{1}\left(V_{\mathrm{GS} 1}-V_{t n}\right)} \tag{12.62}
\end{equation*}
$$

Using the small-signal T model, we find the small-signal output current of $i_{01}$ to be equal to

$$
\begin{equation*}
i_{01}=\frac{v_{1}-v_{2}}{r_{s 1}+r_{s 2}+\left(r_{d s 3} \| r_{d s 4}\right)} \tag{12.63}
\end{equation*}
$$

Thus, defining $G_{m} \equiv i_{01} /\left(v_{1}-v_{2}\right)$, we have

$$
\begin{equation*}
\mathrm{G}_{\mathrm{m}}=\frac{1}{\mathrm{r}_{\mathrm{s} 1}+\mathrm{r}_{\mathrm{s} 2}+\left(\mathrm{r}_{\mathrm{ds} 3} \| \mathrm{r}_{\mathrm{ds} 4}\right)} \tag{12.64}
\end{equation*}
$$

which can be shown to be

$$
\begin{equation*}
\mathrm{G}_{\mathrm{m}}=\frac{4 \mathrm{k}_{1} \mathrm{k}_{3}\left(\mathrm{~V}_{\mathrm{GS} 1}-\mathrm{V}_{\mathrm{tn}}\right)}{\mathrm{k}_{1}+4 \mathrm{k}_{3}} \tag{12.65}
\end{equation*}
$$

Finally, to modify this result such that it is in terms of current, we note that

$$
\begin{equation*}
\mathrm{I}_{1}=\mathrm{k}_{1}\left(\mathrm{~V}_{\mathrm{GS} 1}-\mathrm{V}_{\mathrm{tn}}\right)^{2} \tag{12.66}
\end{equation*}
$$

or, equivalently,

$$
\begin{equation*}
\left(\mathrm{V}_{\mathrm{GS} 1}-\mathrm{V}_{\mathrm{tn}}\right)=\sqrt{\frac{\mathrm{I}_{1}}{\mathrm{k}_{1}}} \tag{12.67}
\end{equation*}
$$

which leads to

$$
\begin{equation*}
\mathrm{G}_{\mathrm{m}}=\frac{4 \mathrm{k}_{1} \mathrm{k}_{3} \sqrt{\mathrm{I}_{1}}}{\left(\mathrm{k}_{1}+4 \mathrm{k}_{3}\right) \sqrt{\mathrm{k}_{1}}} \tag{12.68}
\end{equation*}
$$

Thus, we see that the transconductance of this transconductor can be tuned by changing the bias current, $I_{1}$. Note also that the transconductance is proportional to the square root of the bias current as opposed to a linear relation in the case of a bipolar transconductor.

To see how varying bias conditions for the triode transistors improves the linearity of this circuit, first consider the case of small differences in $\mathrm{V}_{1}$ and $\mathrm{V}_{2}$ (say, 100 mV ). In this small-input-signal case, $Q_{3}$ and $Q_{4}$ essentially act as two source degeneration resistors. Thus, linearity improves (assuming $r_{\mathrm{ds} 3}>>r_{s 1}$ ) over that of a simple differential pair, since transistors in triode are more linear than the source resistances of transistors in the active region. In other words, for a small-input-signal value, the linearity of this circuit is similar to that for a circuit in which the gates of $Q_{3}, Q_{4}$ are connected to fixed-bias voltages. However, if the gates of $Q_{3}, Q_{4}$ were connected to fixed-bias voltages, (12.54) shows that, as their drain-source voltage is increased, the drain current is reduced below that which would occur in a linear relationship due to the squared $\mathrm{V}_{\mathrm{DS}}$ term. In addition, the changing values of $\mathrm{V}_{\mathrm{GS} 1}$ and $\mathrm{V}_{\mathrm{GS} 2}$ (due to current changes) also reduce the value of $\mathrm{V}_{\mathrm{DS}}$, and hence the transconductance of the cell for large input signals. To alleviate this reduction in transconductance for large input signals, the gates of $Q_{3}$ or $Q_{4}$ are connected to the input signals as shown. Now, as the input signal is increased, the small-signal resistance of one of the two triode transistors in parallel, $Q_{3}$ or $Q_{4}$, is reduced. This reduced resistance attempts to increase the transconductance, resulting in a partial cancelling of the decreasing transconductance value. Thus, if a proper ratio of $k_{1} / k_{3}$ is chosen, a more stable transconductance (and hence better linearity) is achieved. For a 4-MHz filter presented in [Krummenacher, 1988], a ratio of $k_{1} / k_{3}=6.7$ is used to obtain distortion levels around 50 dB below the maximum output signal level of 350
mVrms. Also, an extension of this approach is presented in [Silva-Martinez, 1991], where the input signal is split over two input stages to further improve the distortion performance.

#### EXAMPLE 12.6

Consider the circuit of Fig. 12.19 with the following values: $I_{1}=100 \mu \mathrm{~A}, \quad \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}=96 \mu \mathrm{~A} / \mathrm{V}^{2}$, $(\mathrm{W} / \mathrm{L})_{1}=(\mathrm{W} / \mathrm{L})_{2}=20,(\mathrm{~W} / \mathrm{L})_{3}=(\mathrm{W} / \mathrm{L})_{4}=3$, and $\mathrm{v}_{2}=0 \mathrm{~V}$.

1. Assuming a perfectly linear transconductor, use (12.68) to find $i_{01}$ when $v_{1}$ equals 2.5 mV and 250 mV .
2. Assume the gates of $Q_{3}, Q_{4}$ are connected to ground and use classical models for both the triode and active regions. Find the true value of $i_{01}$ when $v_{1}$ equals 2.5 mV and 250 mV . Compare your results with those in part 1.
3. Repeat part 2 , assuming the gates of $\mathrm{Q}_{3}, \mathrm{Q}_{4}$ are connected to the input signals as shown in Fig. 12.19.

#### Solution

1. For the given values, we have

$$
\begin{align*}
& \mathrm{k}_{1}=\frac{96}{2} \times 20=960 \mu \mathrm{~A} / \mathrm{V}^{2}  \tag{12.69}\\
& \mathrm{k}_{3}=\frac{96}{2} \times 3=144 \mu \mathrm{~A} / \mathrm{V}^{2} \tag{12.70}
\end{align*}
$$

and substituting the above values in (12.68), we have

$$
\begin{equation*}
\mathrm{G}_{\mathrm{m}}=\frac{4 \mathrm{k}_{1} \mathrm{k}_{3} \sqrt{100}}{\left(\mathrm{k}_{1}+4 \mathrm{k}_{3}\right) \sqrt{\mathrm{k}_{1}}}=116.2 \mu \mathrm{~A} / \mathrm{V} \tag{12.71}
\end{equation*}
$$

Now, to find $i_{01}$, we use the definition of $G_{m}$ to find

$$
\begin{equation*}
\mathrm{i}_{\mathrm{o} 1}=\mathrm{G}_{\mathrm{m}}\left(\mathrm{v}_{1}-\mathrm{v}_{2}\right)=\mathrm{G}_{\mathrm{m}} \mathrm{v}_{1} \tag{12.72}
\end{equation*}
$$

Thus, for $\mathrm{v}_{1}=2.5 \mathrm{mV}$, we have $\mathrm{i}_{01}=0.2905 \mu \mathrm{~A}$. However, if $\mathrm{v}_{1}=250 \mathrm{mV}$, then $\mathrm{i}_{\mathrm{ol}}=29.05 \mu \mathrm{~A}$. In other words, for a $250-\mathrm{mV}$ input voltage, the total drain current of $\mathrm{Q}_{1}$ would be $129.05 \mu \mathrm{~A}$, whereas that for $Q_{2}$ would be $70.95 \mu \mathrm{~A}$.
2. To find $i_{01}$ in this case, we first note that the sum of the drain currents in $Q_{1}$ and $Q_{2}$ must equal the total bias current, $200 \mu \mathrm{~A}$. In other words,

$$
\begin{equation*}
\mathrm{i}_{\mathrm{D} 1}+\mathrm{i}_{\mathrm{D} 2}=2 \mathrm{I}_{1}=200 \mu \mathrm{~A} \tag{12.73}
\end{equation*}
$$

And since (using $\mathrm{V}_{\text {effi }}=\mathrm{V}_{\mathrm{GSi}}-\mathrm{V}_{\mathrm{tn}}$ ) the drain currents in $\mathrm{Q}_{1}$ and $\mathrm{Q}_{2}$ are given by

$$
\begin{equation*}
\mathrm{i}_{\mathrm{D} 1}=\frac{\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}}{2}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)_{1}\left(\mathrm{v}_{\mathrm{eff} 1}^{2}\right) \quad \text { and } \quad \mathrm{i}_{\mathrm{D} 2}=\frac{\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}}{2}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)_{2}\left(\mathrm{v}_{\mathrm{eff} 2}^{2}\right) \tag{12.74}
\end{equation*}
$$

we can write (12.73) as

$$
\begin{equation*}
v_{\mathrm{eff} 1}^{2}+\mathrm{v}_{\mathrm{eff} 2}^{2}=\frac{5}{24} \mathrm{~V}^{2} \tag{12.75}
\end{equation*}
$$

The current from node $\mathrm{v}_{\mathrm{x}}$ to $\mathrm{v}_{\mathrm{y}}$ through the two triode transistors is given by

$$
\begin{equation*}
\mathrm{i}_{\mathrm{xy}}=2 \times \mathrm{i}_{\mathrm{D} 3}=2 \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)_{3}\left(\mathrm{v}_{\mathrm{eff} 2} \mathrm{v}_{\mathrm{xy}}-\frac{\mathrm{v}_{\mathrm{xy}}^{2}}{2}\right) \tag{12.76}
\end{equation*}
$$

where we have noted that $v_{\text {eff } 3}=v_{\text {eff } 2}$. The sum of $i_{x y}$ and $i_{D 2}$ must equal $I_{1}$, resulting in

$$
\begin{equation*}
960 v_{\text {eff } 2}^{2}+576\left(v_{\text {eff } 2} v_{x y}-\frac{v_{\mathrm{xy}}^{2}}{2}\right)=100 \tag{12.77}
\end{equation*}
$$

Finally, we note that the input signal is equal to the following sum (the threshold voltage terms cancel):

$$
\begin{equation*}
-v_{\text {eff } 2}+v_{\mathrm{xy}}+v_{\text {eff } 1}=v_{\text {in }} \tag{12.78}
\end{equation*}
$$

Equations (12.75), (12.77), and (12.78) can be solved using an equation solver and then choosing the solution that has all positive values.

For a value of $\mathrm{v}_{\mathrm{in}}=2.5 \mathrm{mV}$, the following results are obtained.

$$
\begin{align*}
\mathrm{v}_{\text {eff } 1} & =0.32322 \mathrm{~V} \\
\mathrm{v}_{\mathrm{eff} 2} & =0.32228 \mathrm{~V} \\
\mathrm{v}_{\mathrm{xy}} & =0.0015648 \mathrm{~V} \tag{12.79}
\end{align*}
$$

These values of effective gate voltages imply that the drain currents are

$$
\begin{equation*}
\mathrm{i}_{\mathrm{D} 1}=100.2898 \mu \mathrm{~A} \quad \mathrm{i}_{\mathrm{D} 2}=99.7104 \mu \mathrm{~A} \tag{12.80}
\end{equation*}
$$

which, in turn, imply that

$$
\begin{equation*}
\mathrm{i}_{\mathrm{ol}}=\mathrm{i}_{\mathrm{D} 1}-100 \mu \mathrm{~A}=0.2898 \mu \mathrm{~A} \tag{12.81}
\end{equation*}
$$

Such a result agrees closely with that of part 1 .
However, for the case of $\mathrm{v}_{\mathrm{in}}=250 \mathrm{mV}$, we have

$$
\begin{align*}
\mathrm{v}_{\text {eff } 1} & =0.35452 \mathrm{~V} \\
\mathrm{v}_{\text {eff } 2} & =0.28749 \mathrm{~V} \\
\mathrm{v}_{\mathrm{xy}} & =0.18297 \mathrm{~V} \tag{12.82}
\end{align*}
$$

resulting in $\mathrm{i}_{01}=20.66 \mu \mathrm{~A}$. This result is about 30 percent lower than that expected by a linear transconductor value of $29.05 \mu \mathrm{~A}$, as found in part 1 .
3. Finally, if the gates are connected to the input signal, the preceding equations in part 2 remain the same, except for $i_{x y}$, which is now the sum of $i_{D 3}$ and $i_{D 4}$, resulting in,

$$
\begin{align*}
\mathrm{i}_{\mathrm{xy}}= & \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)_{3}\left[\left(\mathrm{v}_{\mathrm{eff} 2}+\mathrm{v}_{\mathrm{in}}\right) \mathrm{v}_{\mathrm{xy}}-\frac{\mathrm{v}_{\mathrm{xy}}^{2}}{2}\right]  \tag{12.83}\\
& +\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)_{4}\left(\mathrm{v}_{\mathrm{eff} 2} \mathrm{v}_{\mathrm{xy}}-\frac{\mathrm{v}_{\mathrm{xy}}^{2}}{2}\right)
\end{align*}
$$

and so (12.77) is replaced with

$$
\begin{equation*}
960 v_{\text {eff } 2}^{2}+576\left[\left(2 v_{\text {eff } 2}+v_{i n}\right) v_{x y}-v_{x y}^{2}\right]=100 \tag{12.84}
\end{equation*}
$$

image_name:Fig. 12.20
description:The circuit is a differential transconductor using NMOS transistors in triode region with constant drain-source voltages. The transconductance is controlled by the voltage VC, and a common-mode voltage VCM is applied. The circuit is balanced with two identical branches, each containing an NMOS transistor pair controlled by an op-amp.

$$
G_{m}=\mu_{n} C_{o x}\left(\frac{W}{L}\right)_{1} V_{D S}
$$

Fig. 12.20 A differential transconductor using triode transistors that have constant drain-source voltages. The control signal, $\mathrm{V}_{\mathrm{C}}$, adjusts the transconductance value, whereas $\mathrm{V}_{\mathrm{CM}}$ is a fixed common-mode voltage. The top current pair, $\mathrm{I}_{1}$, is set equal to the bias current through $\mathrm{Q}_{1}, \mathrm{Q}_{2}$, using a common-mode feedback circuit (not shown).

Once again, using an equation solver, we find that in the case of $\mathrm{v}_{\mathrm{in}}=2.5 \mathrm{mV}$, the results are essentially the same as in parts 1 and 2 . However, in the case of $v_{i n}=250 \mathrm{mV}$, we find that

$$
\begin{align*}
\mathrm{v}_{\text {eff } 1} & =0.36620 \mathrm{~V} \\
\mathrm{v}_{\text {eff } 2} & =0.27245 \mathrm{~V} \\
\mathrm{v}_{\mathrm{xy}} & =0.15625 \mathrm{~V} \tag{12.85}
\end{align*}
$$

These values lead to $\mathrm{i}_{01}=28.74 \mu \mathrm{~A}$, which is only 1 percent below that expected by a linear transconductor value of $29.05 \mu \mathrm{~A}$.

### 12.4.3 Transconductors Using Constant Drain-Source Voltages

Recall, once again, the classical model for a transistor biased in the triode region,

$$
\begin{equation*}
\mathrm{i}_{\mathrm{D}}=\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)\left[\left(\mathrm{V}_{\mathrm{GS}}-\mathrm{V}_{\mathrm{tn}}\right) \mathrm{V}_{\mathrm{DS}}-\frac{\mathrm{V}_{\mathrm{DS}}^{2}}{2}\right] \tag{12.86}
\end{equation*}
$$

We see here that if the drain-source voltage, $\mathrm{V}_{\mathrm{DS}}$, is kept constant, the drain current is linear with respect to an applied gate-source voltage (ignoring the dc offset current due to the squared $\mathrm{V}_{\mathrm{DS}}$ term) [Pennock, 1985]. Unfortunately, this simple model does not account for important second-order effects (such as velocity saturation and mobility degradation) that severely limit the accuracy of the preceding equation model. However, if fully differential structures are used to cancel even-order error terms, a reasonably linear transconductor (around 50 dB ) can be built using this constant- $\mathrm{V}_{\mathrm{DS}}$ approach.

One possible implementation based on the linearization scheme just described is shown in Fig. 12.20. Here, $Q_{1}$ and $Q_{2}$ are placed in the triode region and their drain-source voltages are set equal to $V_{C}$ through the use of $Q_{3}, Q_{4}$
and two extra amplifiers. The differential input signal is applied to the gates of $Q_{1}, Q_{2}$ and is superimposed on a constant common-mode voltage signal, $\mathrm{V}_{\mathrm{CM}}$. An alternative design here is to use an extra opamp to create a $\mathrm{G}_{\mathrm{m}}-\mathrm{C}$ opamp integrator [Wong, 1989].

For the circuit of Fig. 12.20, we have

$$
\begin{equation*}
\mathrm{i}_{\mathrm{D} 1}=\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)_{1}\left[\left(\frac{\mathrm{~V}_{\mathrm{i}}}{2}+\mathrm{V}_{\mathrm{CM}}-\mathrm{V}_{\mathrm{tn}}\right) \mathrm{V}_{\mathrm{DS}}-\mathrm{V}_{\mathrm{DS}}^{2} / 2\right] \tag{12.87}
\end{equation*}
$$

Noting that $i_{01}$ is the difference between this current and $I_{1}$, which is set via a common-mode feedback signal equal to

$$
\begin{equation*}
\mathrm{I}_{1}=\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)_{1}\left[\left(\mathrm{~V}_{\mathrm{CM}}-\mathrm{V}_{\mathrm{tn}}\right) \mathrm{V}_{\mathrm{DS}}-\mathrm{V}_{\mathrm{DS}}^{2} / 2\right] \tag{12.88}
\end{equation*}
$$

we then have

$$
\begin{equation*}
\mathrm{i}_{\mathrm{ol}}=\mathrm{i}_{\mathrm{D} 1}-\mathrm{I}_{1}=\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)_{1}\left(\frac{\mathrm{v}_{\mathrm{i}}}{2}\right) \mathrm{V}_{\mathrm{DS}} \tag{12.89}
\end{equation*}
$$

Then, defining $G_{m} \equiv i_{01} / v_{i}$ results in

$$
\begin{equation*}
\mathrm{G}_{\mathrm{m}}=\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)_{1} \mathrm{~V}_{\mathrm{DS}} \tag{12.90}
\end{equation*}
$$

Note that here the transconductance value is proportional to the drain-source voltage, and from (12.88), we see that the bias current is also approximately proportional to the drain-source voltage (if $\mathrm{V}_{\mathrm{DS}}$ is small).

#### EXAMPLE 12.7

Consider the circuit shown in Fig. 12.20, where $\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}=96 \mu \mathrm{~A} / \mathrm{V}^{2},(\mathrm{~W} / \mathrm{L})_{1}=(\mathrm{W} / \mathrm{L})_{2}=10, \mathrm{~V}_{\mathrm{tn}}=0.8 \mathrm{~V}$, and $\mathrm{V}_{\mathrm{CM}}=2 \mathrm{~V}$. Find the transconductance value when $\mathrm{V}_{\mathrm{C}}=0.2 \mathrm{~V}$ and when $\mathrm{V}_{\mathrm{C}}=0.4 \mathrm{~V}$. For these two controlsignal values, also find the bias currents through $Q_{1}$ and $Q_{2}$ (i.e., when $v_{i}=0$ ) and the maximum input signal swing before either transistor exits the triode region (assume the classical transistor model).

#### Solution

Using (12.90), for $\mathrm{V}_{\mathrm{C}}=0.2 \mathrm{~V}$, we have

$$
\mathrm{G}_{\mathrm{m}}=96 \mu \mathrm{~A} / \mathrm{V}^{2} \times 10 \times 0.2 \mathrm{~V}=0.192 \mathrm{~mA} / \mathrm{V}
$$

Also, the bias current through $Q_{1}$ or $Q_{2}$ for this $V_{C}$ value can be found using (12.88):

$$
I_{1}=96 \mu \mathrm{~A} / \mathrm{V}^{2} \times 10\left[(2-0.8) 0.2-\frac{0.2^{2}}{2}\right]=0.211 \mathrm{~mA}
$$

Finally, to remain in the triode region, the effective gate-source voltages of $Q_{1}$ and $Q_{2}$ must remain above $V_{D S}=0.2 \mathrm{~V}$. In other words, their gate-source voltages must remain above $V_{D S}+V_{t}=1.0 \mathrm{~V}$. Since the commonmode voltage, $\mathrm{V}_{\mathrm{CM}}$, equals 2 V , the negative portion, $\mathrm{v}_{\mathrm{i}} / 2$, must not go below a level of -1 V , otherwise the transistor will enter the active region. Thus, a maximum differential input voltage, $\mathrm{v}_{\mathrm{i}}$, of 2 V can be applied in this case.

Similarly, for $\mathrm{V}_{\mathrm{C}}=0.4 \mathrm{~V}$, we have twice the transconductance value of $\mathrm{G}_{\mathrm{m}}=0.384 \mathrm{~mA} / \mathrm{V}$. Here, the bias current is found to be $I_{1}=0.384 \mathrm{~mA}$ and the maximum input signal swing is a differential voltage of $v_{i}=1.6 \mathrm{~V}$. Note that doubling the drain-source voltage doubles the transconductance (as expected) but requires almost a doubling of the bias current and a loss of signal swing.

## 12.5 CMOS TRANSCONDUCTORS USING ACTIVE TRANSISTORS

In general, CMOS transconductors based on the use of active transistors ${ }^{2}$ have worse linearity performance than their triode-based counterparts. However, active-based designs often have improved speed performance (assuming equal bias currents in the two cases). The linearity of active-transistor transconductors is only moderate (around 30 to 50 dB ) because they rely on the square-law model of MOS transistors, which is not very accurate (particularly in short-channel processes). In addition, only the difference in output

Key Point: Transconductors whose gain is based upon the small-signal transconductance of active-mode transistors generally offer increased speed, butreduced linearity, compared with transconductors based upon triode devices.
currents is ideally linear, whereas individual currents have significant sec-ond-order harmonics. Thus, second-order harmonic distortion also occurs if the difference is not taken precisely.

We should mention here that not all linearization techniques using active transistors are discussed. For example, one approach not discussed is a technique in which the tail current of a differential pair is adaptively biased [Nedungadi, 1984]. This technique is limited in its frequency response, and thus a designer would usually choose a triode-based design instead. In summary, in this section we present CMOS linearization techniques intended for high-speed operation and only moderate linearity.

### 12.5.1 CMOS Pair

Before proceeding to look at transconductor circuits that have active transistors, it is worthwhile to introduce a two-transistor circuit known as the CMOS pair, as shown in Fig. 12.21 [Seevinck, 1987]. As we will show, this two-transistor pair acts as a single transistor, assuming that both transistors remain in the active region. Such an observation allows one to more easily derive some of the CMOS transconductors described later in this section.

To show that this two-transistor pair acts as a single transistor, we first assume that both transistors remain in the active region. Thus, we can write their drain currents as

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D}}=\mathrm{K}_{\mathrm{n}}\left(\mathrm{~V}_{\mathrm{GSn}}-\mathrm{V}_{\mathrm{tn}}\right)^{2} \quad \text { where } \mathrm{V}_{\mathrm{tn}}>0 \tag{12.91}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D}}=\mathrm{K}_{\mathrm{p}}\left(\mathrm{~V}_{\mathrm{SGp}}+\mathrm{V}_{\mathrm{tp}}\right)^{2} \quad \text { where } \mathrm{V}_{\mathrm{tp}}<0 \tag{12.92}
\end{equation*}
$$

image_name:Fig. 12.21
description:
[
name: Qn, type: NMOS, ports: {S: snsp, D: LOAD1, G: VGS-eq}
name: Qp, type: PMOS, ports: {S: snsp, D: LOAD2, G: VGS-eq}
]
extrainfo:The circuit is a CMOS pair with both transistors in the active region. The equivalent transistor has a threshold voltage Vt-eq and device parameter Keq.

Fig. 12.21 A CMOS pair, where both transistors are in the active region. The transistor pair is equivalent to a single transistor with an equivalent threshold voltage, $\mathrm{V}_{\mathrm{t} \text {-eq }}$, and device parameter, $\mathrm{K}_{\text {eq }}$
2. Active transistors are those transistors that operate in the active region. The active region is also known as the pinch-off, or saturation, region. This active region for an $n$-channel transistor occurs when $V_{G S}$ is greater than $V_{t n}$ and $V_{D S} \geq V_{G S}-V_{t n}=V_{\text {eff }}$.

Rearranging these two equations in terms of their gate-source voltages gives
and

$$
\begin{equation*}
\mathrm{V}_{\mathrm{SGp}}=-\mathrm{V}_{\mathrm{tp}}+\frac{1}{\sqrt{\mathrm{~K}_{\mathrm{p}}}} \sqrt{\mathrm{I}_{\mathrm{D}}} \tag{12.94}
\end{equation*}
$$

Defining the equivalent gate-source voltage, $\mathrm{V}_{\mathrm{GS}-\mathrm{eq}}$, to be the difference between the two gate voltages, we have

$$
\begin{equation*}
\mathrm{V}_{\mathrm{GS}-\mathrm{eq}} \equiv \mathrm{~V}_{\mathrm{GSn}}+\mathrm{V}_{\mathrm{SGp}}=\left(\mathrm{V}_{\mathrm{tn}}-\mathrm{V}_{\mathrm{tp}}\right)+\left(\frac{1}{\sqrt{\mathrm{~K}_{\mathrm{n}}}}+\frac{1}{\sqrt{\mathrm{~K}_{\mathrm{p}}}}\right) \sqrt{\mathrm{I}_{\mathrm{D}}} \tag{12.95}
\end{equation*}
$$

Since this equation has the same form as those for a single transistor (equations (12.93) and (12.94)), we define the equivalent threshold voltage, $\mathrm{V}_{\mathrm{t} \text {-eq }}$, as

$$
\begin{equation*}
\mathrm{V}_{\mathrm{t}-\mathrm{eq}} \equiv \mathrm{~V}_{\mathrm{tn}}-\mathrm{V}_{\mathrm{tp}} \quad \text { where } \mathrm{V}_{\mathrm{tn}}>0 \text { and } \mathrm{V}_{\mathrm{tp}}<0 \tag{12.96}
\end{equation*}
$$

and we define the equivalent device parameter, $\mathrm{K}_{\mathrm{eq}}$, as

$$
\begin{equation*}
\frac{1}{\sqrt{\mathrm{~K}_{\mathrm{eq}}}} \equiv \frac{1}{\sqrt{\mathrm{~K}_{\mathrm{n}}}}+\frac{1}{\sqrt{\mathrm{~K}_{\mathrm{p}}}} \tag{12.97}
\end{equation*}
$$

which can be rewritten as

$$
\begin{equation*}
\mathrm{K}_{\mathrm{eq}}=\frac{\mathrm{K}_{\mathrm{n}} \mathrm{~K}_{\mathrm{p}}}{\left(\sqrt{\mathrm{~K}_{\mathrm{n}}}+\sqrt{\mathrm{K}_{\mathrm{p}}}\right)^{2}} \tag{12.98}
\end{equation*}
$$

Finally, combining (12.95), (12.96), and (12.98) and rearranging, we see that when both transistors are in their active regions, the drain current can be written as

$$
\begin{equation*}
\mathrm{i}_{\mathrm{D}}=\mathrm{K}_{\mathrm{eq}}\left(\mathrm{~V}_{\mathrm{GS}-\mathrm{eq}}-\mathrm{V}_{\mathrm{t}-\mathrm{eq}}\right)^{2} \tag{12.99}
\end{equation*}
$$

where $\mathrm{K}_{\text {eq }}, \mathrm{V}_{\mathrm{GS}-\mathrm{eq}}$, and $\mathrm{V}_{\mathrm{t} \text {-eq }}$ are defined as just described. Clearly, this equation is in the same form as that for a single transistor, and thus this two-transistor pair can replace single transistors in many circuits. As we will see next, this replacement can be quite useful in designing linear transconductor circuits.

### 12.5.2 Constant Sum of Gate-Source Voltages

One popular approach for creating an active transistor transconductor is by using a constant sum of gatesource voltages, as shown in Fig. 12.22. Assuming the two transistors are operating in the active region (i.e., the drain voltages are high and each of $\mathrm{v}_{\mathrm{GS} 1}$ and $\mathrm{V}_{\mathrm{GS} 2}$ remain greater than $\mathrm{V}_{\mathrm{tn}}$ ), the output differential current is given by

$$
\begin{equation*}
\left(\mathrm{i}_{\mathrm{D} 1}-\mathrm{i}_{\mathrm{D} 2}\right)=\mathrm{K}\left(\mathrm{v}_{\mathrm{GS} 1}+\mathrm{v}_{\mathrm{GS} 2}-2 \mathrm{~V}_{\mathrm{tn}}\right)\left(\mathrm{v}_{\mathrm{GS} 1}-\mathrm{v}_{\mathrm{GS} 2}\right) \tag{12.100}
\end{equation*}
$$

Here, the output differential current is linear if the sum of the two gate-sour ce voltages remains constant. As we will see next, there are a variety of ways to make the sum of the gate-source voltages remain constant when applying an input signal. One important point to note here is that, although the differential current is linear, the individual drain currents are not linear. Thus, if the subtraction between currents has some error (as it certainly will), some distortion products will occur even if perfect square-law devices are obtainable.
image_name:Matched devices
description:The circuit consists of two matched NMOS transistors Q1 and Q2, with their sources connected to ground. The gate-source voltages are VGS1 and VGS2, and the drain currents are ID1 and ID2 respectively.

(Matched devices)

$$
\begin{gathered}
\mathrm{K}=\left(\mu_{\mathrm{n}} / 2\right) \mathrm{C}_{\mathrm{Ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right) \\
\mathrm{i}_{\mathrm{D} 1}=\mathrm{K}\left(\mathrm{v}_{\mathrm{GS} 1}-\mathrm{V}_{\mathrm{tn}}\right)^{2} \quad \text { and } \quad \mathrm{i}_{\mathrm{D} 2}=\mathrm{K}\left(\mathrm{v}_{\mathrm{GS} 2}-\mathrm{V}_{\mathrm{tn}}\right)^{2} \\
\left(\mathrm{i}_{\mathrm{D} 1}-\mathrm{i}_{\mathrm{D} 2}\right)=\mathrm{K}\left(\mathrm{v}_{\mathrm{GS} 1}+\mathrm{v}_{\mathrm{GS} 2}-2 \mathrm{~V}_{\mathrm{tn}}\right)\left(\mathrm{v}_{\mathrm{GS} 1}-\mathrm{v}_{\mathrm{GS} 2}\right)
\end{gathered}
$$

Fig. 12.22 Two-transistor circuit in which the difference in the drain currents is linear with respect to $\left(\mathrm{v}_{\mathrm{GS} 1}-\mathrm{v}_{\mathrm{GS} 2}\right)$ if the sum of the two gate-source voltages remains constant. Transistors are matched and in the active region.

### 12.5.3 Source-Connected Differential Pair

One approach to maintain a constant sum of gate-source voltages is to apply a balanced differential input voltage, as shown in Fig. 12.23. Here, the differential pair is biased using the dc common-mode voltage, $\mathrm{V}_{\mathrm{CM}}$, whereas the input signal varies symmetrically around this common-mode voltage. Note that, from the preceding analysis, this input signal symmetry is important in maintaining linearity. However, in practice, a slightly nonbalanced input signal is not the dominant source of nonlinearity. Specifically, the linearity achievable with this approach is quite limited because MOS transistors are not well modelled by square-law behavior. In addition, it is difficult to obtain a precise difference between the two drain currents, which also causes even-order harmonics. As a result, this technique is typically limited to less than 50 dB of linearity.

To tune the transconductance of this circuit, the common-mode voltage, $\mathrm{V}_{\mathrm{CM}}$, can be adjusted. However, it should be noted that, in a short-channel process and when moderate gate-source voltages are used, carrier velocity saturation occurs and limits the transconductance variation. In addition, one should be aware that as the input common-mode voltage is adjusted, linearity performance and maximum signal swing levels change as well. One example of this approach is presented in [Snelgrove, 1992] where speeds up to 450 MHz are demonstrated in a $0.9-\mu \mathrm{m}$ CMOS process with around a $30-$ to $40-\mathrm{dB}$ dynamic range performance.

### 12.5.4 Inverter-Based

A transconductor approach similar to the source-connected differential pair is the inverter-based transconductor, shown in Fig. 12.24 [Park, 1986]. Here, two CMOS pairs, $Q_{1 a}, Q_{1 b}$ and $Q_{2 a}, Q_{2 b}$, have replaced the two individual
image_name:Fig. 12.23
description:
[
name: M1, type: NMOS, ports: {S: VSS, D: LOAD1, G: VCM+(Vi/2)}
name: M2, type: NMOS, ports: {S: VSS, D: LOAD2, G: VCM-(Vi/2)}
]
extrainfo:The circuit is a source-connected differential-pair transconductor. It uses two NMOS transistors as loads, with the input signals balanced around VCM for linearization. The difference in drain currents (iD1 - iD2) is proportional to the input voltage difference (Vi). The transconductance Gm is given by the expression Gm = 2K(VCM - VSS - Vtn).

Fig. 12.23 A source-connected differential-pair transconductor. The differential input signal must be balanced around $\mathrm{V}_{\mathrm{CM}}$ for linearization of the transistor square-law relation to occur.
image_name:Fig. 12.24
description:
[
name: Q1b, type: NMOS, ports: {S: s1bs1a, D: VDD, G: Vc1}
name: Q1a, type: PMOS, ports: {S: s1bs1a, D: vout, G: vin}
name: Q2a, type: PMOS, ports: {S: s2as2b, D: vout, G: vin}
name: Q2b, type: NMOS, ports: {S: s2as2b, D: VSS=-VDD, G: Vc2=-Vc1}
]
extrainfo:This circuit is a complementary differential-pair transconductor using CMOS pairs. The output current i_o is the difference between the currents i_1 and i_2. The transconductance Gm is given by Gm = 4Keq(VC1 - Vt-eq). The input voltage is balanced around Vin, and the circuit operates with VDD as the positive supply and VSS as the negative supply.

Fig. 12.24 Complementary differential-pair transconductor using CMOS pairs.
transistors in a traditional CMOS inverter, and the difference in their output currents is the overall output current, $\mathrm{i}_{\mathrm{o}}$. Assuming that all four transistors are in the active region and that the two CMOS pairs are matched, we can use the previous results on CMOS pairs to write

$$
\begin{equation*}
\mathrm{i}_{1}=\mathrm{K}_{\mathrm{eq}}\left(\mathrm{~V}_{\mathrm{GS}-\mathrm{eq} 1}-\mathrm{V}_{\mathrm{t}-\mathrm{eq}}\right)^{2} \tag{12.101}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{i}_{2}=\mathrm{K}_{\mathrm{eq}}\left(\mathrm{~V}_{\mathrm{GS}-\mathrm{eq} 2}-\mathrm{V}_{\mathrm{t}-\mathrm{eq}}\right)^{2} \tag{12.102}
\end{equation*}
$$

Note here that these equations are in the same form as those shown in Fig. 12.22. Thus, as in (12.100), the output current is given by

$$
\begin{equation*}
\mathrm{i}_{\mathrm{o}} \equiv \mathrm{i}_{1}-\mathrm{i}_{2}=\mathrm{K}_{\mathrm{eq}}\left(\mathrm{~V}_{\mathrm{GS}-\mathrm{eq} 1}+\mathrm{V}_{\mathrm{GS}-\mathrm{eq} 2}-2 \mathrm{~V}_{\mathrm{t}-\mathrm{eq}}\right)\left(\mathrm{V}_{\mathrm{GS}-\mathrm{eq} 1}-\mathrm{V}_{\mathrm{GS}-\mathrm{eq} 2}\right) \tag{12.103}
\end{equation*}
$$

Thus, the output current is linearly related to the difference in equivalent gate-source voltages of the CMOS pairs if the sum of their equivalent gate-source voltages is a constant value. To see that a constant equivalent gate-source voltage sum occurs, we have

$$
\begin{equation*}
\mathrm{V}_{\mathrm{GS} \text {-eq1 }}=\mathrm{V}_{\mathrm{C} 1}-\mathrm{V}_{\mathrm{in}} \tag{12.104}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{V}_{\mathrm{GS}-\mathrm{eq} 2}=\mathrm{V}_{\mathrm{in}}-\mathrm{V}_{\mathrm{C} 2} \tag{12.105}
\end{equation*}
$$

and therefore

$$
\begin{equation*}
\mathrm{V}_{\mathrm{GS}-\mathrm{eq} 1}+\mathrm{V}_{\mathrm{GS}-\mathrm{eq} 2}=\mathrm{V}_{\mathrm{C} 1}-\mathrm{V}_{\mathrm{C} 2} \tag{12.106}
\end{equation*}
$$

Also, the difference in equivalent gate-source voltages is given by

$$
\begin{equation*}
\mathrm{V}_{\mathrm{GS}-\mathrm{eq} 1}-\mathrm{V}_{\mathrm{GS}-\mathrm{eq} 2}=\mathrm{V}_{\mathrm{C} 1}+\mathrm{V}_{\mathrm{C} 2}-2 \mathrm{~V}_{\mathrm{in}} \tag{12.107}
\end{equation*}
$$

Finally, in the case where we choose $\mathrm{V}_{\mathrm{C} 2}=-\mathrm{V}_{\mathrm{C} 1}$, we have

$$
\begin{equation*}
\mathrm{i}_{\mathrm{o}}=4 \mathrm{~K}_{\mathrm{eq}}\left(\mathrm{~V}_{\mathrm{C} 1}-\mathrm{V}_{\mathrm{t}-\mathrm{eq}}\right)\left(\mathrm{V}_{\mathrm{in}}\right) \tag{12.108}
\end{equation*}
$$

and the transconductance value can be varied by changing the control voltages, $\mathrm{V}_{\mathrm{C} 1}$ and $\mathrm{V}_{\mathrm{C} 2}$ (which, incidentally, are high-input impedance nodes and thus are easily adjustable). Note that, with this transconductor, matching need occur only for transistors of the same type. Specifically, the n -channel transistors should match and the p -channel transistors should match, but there is no need to match n - and p -channel transistors to each other.

### 12.5.5 Differential-Pair with Floating Voltage Sources

Another approach to maintain a constant sum of gate-source voltages is by using two floating dc voltage sources, as shown in Fig. 12.25 [Nedungadi, 1984]. Writing a voltage equation around the loop, we have

$$
\begin{equation*}
\mathrm{V}_{\mathrm{GS} 1}-\left(\mathrm{V}_{\mathrm{x}}+\mathrm{V}_{\mathrm{tn}}\right)+\mathrm{V}_{\mathrm{GS} 2}-\left(\mathrm{V}_{\mathrm{x}}+\mathrm{V}_{\mathrm{tn}}\right)=0 \tag{12.109}
\end{equation*}
$$

and thus,

$$
\begin{equation*}
\mathrm{V}_{\mathrm{GS} 1}+\mathrm{V}_{\mathrm{GS} 2}=2\left(\mathrm{~V}_{\mathrm{x}}+\mathrm{V}_{\mathrm{tn}}\right) \tag{12.110}
\end{equation*}
$$

As a result, this circuit maintains a constant sum of gate-source voltages even if the applied differential signal is not balanced. Also, writing two equations that describe the relationship between $v_{1}$ and $v_{2}$, we have

$$
\begin{equation*}
\mathrm{V}_{1}-\mathrm{V}_{\mathrm{GS} 1}+\mathrm{V}_{\mathrm{x}}+\mathrm{V}_{\mathrm{tn}}=\mathrm{V}_{2} \tag{12.111}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{V}_{2}-\mathrm{V}_{\mathrm{GS} 2}+\mathrm{V}_{\mathrm{x}}+\mathrm{V}_{\mathrm{tn}}=\mathrm{V}_{1} \tag{12.112}
\end{equation*}
$$

Subtracting (12.111) from (12.112) and rearranging, we obtain

$$
\begin{equation*}
\mathrm{v}_{\mathrm{GS} 1}-\mathrm{v}_{\mathrm{GS} 2}=2\left(\mathrm{v}_{1}-\mathrm{v}_{2}\right) \tag{12.113}
\end{equation*}
$$

Thus, the difference between the input voltages is equal to one half the difference between the gate-source voltages. Finally, the differential output current is found by combining (12.100), (12.110), and (12.113) to give

$$
\begin{equation*}
\left(i_{D 1}-i_{D 2}\right)=4 K V_{x}\left(v_{1}-v_{2}\right) \tag{12.114}
\end{equation*}
$$

One simple way to realize the floating voltage sources of Fig. 12.25 is to use two source followers, as shown in Fig. 12.26 [Nedungadi, 1984]. The transistors labelled nK are n times larger than the other two transistors, and thus
image_name:Fig. 12.25
description:The circuit is a linearized differential pair using floating voltage sources. It includes two NMOS transistors (M1 and M2) with their gates driven by separate voltage sources (VGS1 and VGS2). The differential output current is determined by the difference between the drain currents of M1 and M2.

$$
\begin{aligned}
\left(\mathrm{i}_{\mathrm{D} 1}-\mathrm{i}_{\mathrm{D} 2}\right) & =4 \mathrm{KV} \mathrm{~V}_{\mathrm{x}}\left(\mathrm{v}_{1}-\mathrm{V}_{2}\right) \\
\mathrm{G}_{\mathrm{m}} & =4 \mathrm{KV} \mathrm{~V}_{\mathrm{x}}
\end{aligned}
$$

Fig. 12.25 A linearized differential pair using floating voltage sources.
image_name:Fig. 12.26 A linear transconductor for large n.
description:This circuit is a linear transconductor for large n, utilizing NMOS transistors M1, M2, and M3. The differential output current is determined by the drain currents of M1 and M2. The current sources provide a bias current of (n+1)IB. The circuit operates between VDD and VSS.

$$
\begin{array}{r}
\left(i_{D 1}-i_{D 2}\right)=\left(\frac{n}{n+1}\right) 4 \sqrt{K I_{B}}\left(v_{1}-v_{2}\right) \\
G_{m}=\left(\frac{n}{n+1}\right) 4 \sqrt{K I_{B}}
\end{array}
$$

Fig. 12.26 A linear transconductor for large n.
image_name:Fig. 12.27 A linearized differential pair
description:The circuit is a linearized differential pair using NMOS and PMOS transistors. It includes floating voltage sources that drive only the transistor gates. The differential output current is determined by the drain currents of the NMOS transistors Q1a and Q2a.

$$
\left(\mathrm{i}_{\mathrm{D} 1}-\mathrm{i}_{\mathrm{D} 2}\right)=4 \mathrm{~K}_{\mathrm{eq}} \mathrm{~V}_{\mathrm{x}}\left(\mathrm{v}_{1}-\mathrm{v}_{2}\right)
$$

Fig. 12.27 A linearized differential pair in which the floating voltage sources need drive only the transistor gates.
image_name:Fig. 12.28
description:The circuit is a linearized differential pair using NMOS and PMOS transistors with floating voltage sources driving only the transistor gates. The differential output current is determined by the drain currents of NMOS transistors Q1a and Q2a, expressed as (i_D1 - i_D2) = 4 * sqrt(K_eq) * I_B * (v1 - v2). The circuit is designed to act as a transconductor with a transconductance G_m = 4 * sqrt(K_eq) * I_B.

Fig. 12.28 A transconductor that uses CMOS pairs and floating voltage sources.
they act as source followers when n is large (typically, when n is 5 or greater). If n is not large, the bias current through the two source followers changes as the input signal is applied and linearity is worsened. A disadvantage of this circuit is that a large dc bias current passes through the two source followers. However, if only moderate linearity is desired and the input signal is relatively small (say, 500 mV ), then this approach can be quite useful.

Since it is difficult to realize a floating voltage source that drives the source of another transistor, another approach is to modify the circuit of Fig. 12.25 such that the floating voltage sources need drive only the transistor gates. Such a modification is possible by replacing the single transistors shown in Fig. 12.25 with their CMOS pairs, as shown in Figure 12.27. Note that the voltage sources must now be larger than $\mathrm{V}_{\mathrm{t} \text {-eq }}$ and must include a controllable $\mathrm{V}_{\mathrm{x}}$ voltage. Fortunately, such circuits are easily accomplished by using two more CMOS pairs, as shown in Fig. 12.28, where the pairs $\mathrm{Q}_{3 \mathrm{a}}, \mathrm{Q}_{3 \mathrm{~b}}$ and $\mathrm{Q}_{4 \mathrm{a}}, \mathrm{Q}_{4 \mathrm{~b}}$ have been added together with two adjustable current sources [Seevinck, 1987]. Referring back to (12.99), we see that $\mathrm{V}_{\mathrm{x}}$ is given by

$$
\begin{equation*}
\mathrm{V}_{\mathrm{x}}=\frac{1}{\sqrt{\mathrm{~K}_{\mathrm{eq}}}} \sqrt{\mathrm{I}_{\mathrm{B}}} \tag{12.115}
\end{equation*}
$$

where, for simplicity, we have assumed that all CMOS pairs are matched. As a result, the differential output current is given by

$$
\begin{equation*}
\left(i_{D 1}-i_{D 2}\right)=4 \sqrt{K_{e q} I_{B}}\left(v_{1}-v_{2}\right) \tag{12.116}
\end{equation*}
$$

Thus, we see that the output current can be tuned by adjusting the dc bias current, $\mathrm{I}_{\mathrm{B}}$. Note that the transconductance coefficient is proportional to the square root of $I_{B}$ and thus a fourfold increase in current results in only a factor of 2 coefficient increase.

Before leaving this circuit, a couple of points are worth mentioning. First, note that the output currents from this circuit are available at both the upper pair, $Q_{1 a}, Q_{2 a}$, as well as at the lower pair, $Q_{1 b}, Q_{2 b}$. Such flexibility may be useful in the remaining transconductor circuitry. Second, note that $V_{\text {ss }}$ must be at least $V_{\mathrm{tn}}+\left|V_{\mathrm{tp}}\right|$ below the most negative input signal swing of either $v_{1}$ or $V_{2}$. If we assume $v_{1}$ and $v_{2}$ have $\pm 1-V$ signals associated with them around ground, then, for $\mathrm{V}_{\mathrm{tn}}=-\mathrm{V}_{\mathrm{tp}}=1 \mathrm{~V}$, $\mathrm{V}_{\mathrm{ss}}$ would have to be less than -3 V . Thus, assuming we have symmetrical power supplies, a 6-V power supply would be needed for only a $2-\mathrm{V}$ signal swing.

### 12.5.6 Bias-Offset Cross-Coupled Differential Pairs

Another approach to realize a transconductor with active transistors is to use two cross-coupled differential pairs where the input into one pair is intentionally voltage offset [Wang, 1990]. One implementation of this approach is shown in Fig. 12.29, where the differential pair $Q_{1}, Q_{2}$ is cross coupled with the bias-offset differential pair $Q_{3}, Q_{4}$. Here, we assume all transistors are in the active region and are matched (i.e., we assume all transistors have equal device parameters of K and equal threshold voltages of $\mathrm{V}_{\mathrm{tn}}$ ).

To find the differential output current, we first find

$$
\begin{equation*}
\mathrm{i}_{1}=\mathrm{K}\left(\mathrm{~V}_{1}-\mathrm{V}_{\mathrm{x}}-\mathrm{V}_{\mathrm{tn}}\right)^{2}+\mathrm{K}\left(\mathrm{~V}_{2}-\mathrm{V}_{\mathrm{B}}-\mathrm{V}_{\mathrm{x}}-\mathrm{V}_{\mathrm{tn}}\right)^{2} \tag{12.117}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{i}_{2}=\mathrm{K}\left(\mathrm{~V}_{2}-\mathrm{V}_{\mathrm{x}}-\mathrm{V}_{\mathrm{tn}}\right)^{2}+\mathrm{K}\left(\mathrm{~V}_{1}-\mathrm{V}_{\mathrm{B}}-\mathrm{V}_{\mathrm{x}}-\mathrm{V}_{\mathrm{tn}}\right)^{2} \tag{12.118}
\end{equation*}
$$

Now finding the difference, $\boldsymbol{i}_{1}-\mathrm{i}_{2}$, we have

$$
\begin{equation*}
\left(i_{1}-i_{2}\right)=2 K V_{B}\left(v_{1}-v_{2}\right) \tag{12.119}
\end{equation*}
$$

Thus, the output differential current is linear with respect to the differential input voltage (as expected) and the transconductance value is proportional to $\mathrm{V}_{\mathrm{B}}$. Note, however, that the bias currents through $\mathrm{Q}_{5}, \mathrm{Q}_{6}, \mathrm{Q}_{7}$, and $\mathrm{Q}_{8}$ are all square-law related to $\mathrm{V}_{\mathrm{B}}$. Thus, the transconductance value is proportional to the square root of the changing bias current, as in the other active transistor CMOS transconductors. Also, note that the bias current, $\mathrm{I}_{\mathrm{SS}}$, does not affect the transconductance value but does determine the maximum (or minimum) output current available.

Finally, note that this offset-bias linearization technique can also be realized in a single-ended version with only a few transistors, as shown in Fig. 12.30 [Bult, 1987]. The analysis is left to the reader.
image_name:Fig. 12.29
description:This circuit is a bias-offset cross-coupled transconductor. It uses NMOS transistors to create differential pairs and control current flow. The bias current ISS helps in determining the maximum or minimum output current available. The circuit is designed to linearize the transconductance.

$$
\begin{aligned}
\left(i_{1}-i_{2}\right) & =2 K V_{B}\left(V_{1}-v_{2}\right) \\
G_{m} & =2 K V_{B}
\end{aligned}
$$

Fig. 12.29 A bias-offset cross-coupled transconductor.
image_name:Fig. 12.29 A bias-offset cross-coupled transconductor
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: X, G: V1}
name: Q2, type: NMOS, ports: {S: GND, D: i2, G: X}
name: Q3, type: NMOS, ports: {S: X, D: i1, G: VB}
]
extrainfo:This circuit is a bias-offset cross-coupled transconductor using NMOS transistors. It creates differential pairs to control current flow, with a bias current ISS determining the output current. The design aims to linearize the transconductance.

$$
\mathrm{i}_{1}-\mathrm{i}_{2}=\mathrm{K}\left(\mathrm{~V}_{\mathrm{B}}-2 \mathrm{~V}_{\mathrm{tn}}\right)\left(2 \mathrm{v}_{1}-\mathrm{V}_{\mathrm{B}}\right)
$$

Fig. 12.30 A single-ended offset-bias transconductor.

## 12.6 BIPOLAR TRANSCONDUCTORS

There are two main approaches for realizing bipolar transconductors. One approach is to use a fixed transconductor cascaded with a gain cell. The fixed transconductor is typically a differential pair linearized through resistor degeneration. The gain cell allows scaling of the output current by varying the ratio of two current sources. The other approach is to use a differential input stage with multiple inputs, where the transistors are scaled such that improved linearity occurs. In this case, the transconductance value can be tuned by varying the bias current through the input stage.

### 12.6.1 Gain-Cell Transconductors

Key Point: Bipolar transconductors based on fixed resistors may be made tunable by cascading them with an adjustable-gain cell.

The bipolar transconductors in Fig. 12.12 and Fig. 12.14 have a fixed transconductance value equal to approximately $1 / R_{S}$. However, to accommodate tuning, variable transconductance values are required. One common approach for creating tunable transconductors that have a fixed transconductance input stage is to use a gain cell as described in Section 11.5. Recall that in a gain cell, the output current is equal to a scaled version of the input current, where the scaling factor is determined by the ratio of two dc bias currents. In addition, the circuit is highly linear.

A tunable transconductor that uses a gain cell is shown in Fig. 12.31. Here, the voltage sources, $\mathrm{V}_{\mathrm{Ls}}$, represent voltage level shifters and could be realized using the circuit shown in Fig. 12.32. By combining the relationships given for the fixed transconductor and the gain cell, specifically, (12.40) and (11.17), then the output current is given by

$$
\begin{equation*}
\mathrm{i}_{\mathrm{o}}=\frac{\mathrm{v}_{\mathrm{i}} \mathrm{I}_{2}}{\mathrm{R}_{\mathrm{E}} \mathrm{I}_{1}} \tag{12.120}
\end{equation*}
$$

resulting in a transconductance value equal to

$$
\begin{equation*}
\mathrm{G}_{\mathrm{m}}=\left(\frac{1}{\mathrm{R}_{\mathrm{E}}}\right)\left(\frac{\mathrm{I}_{2}}{\mathrm{I}_{1}}\right) \tag{12.121}
\end{equation*}
$$

Thus, the transconductance value is proportional to the ratio of $\mathrm{I}_{2} / \mathrm{I}_{1}$.
It is also possible to place the gain cell below the input differential pair, as shown in Fig. 12.33 [Wyszynski, 1993; Moree, 1993]. Note that while the previous designs have $2 r_{e}$ in series with the degeneration resistor, $R_{E}$, this circuit has $4 r_{e}$ in series with $R_{E}$ (that of $Q_{1}-Q_{4}$ ), which might affect the distortion performance. However, the gain cell shown has less distortion due to finite $\beta$ effects and has therefore been referred to as a beta-immune type- $A$ cell [Gilbert, 1990].

[^0]:    3. For a transistor in the triode region that has zero $\mathrm{V}_{\mathrm{DS}}$, it doesn't matter which junctions are called the drain and the source, since both junctions are at the same potential.
4. Transistors also accumulate channel charge when turning on, but this does not typically affect circuit performance since the charge comes from low-impedance nodes.
[^1]:    7. p-channel transistors exhibit trapping for positive gate voltages since only electrons, and not holes, are trapped. Therefore, to prevent trapping, they should never be turned off.
[^2]:    4. A translinear multiplier is also commonly called a Gilbert multiplier or an analog multiplier.

image_name:Fig. 12.31 A typical gain-cell transconductor.
description:This circuit is a typical gain-cell transconductor using bipolar junction transistors (BJTs). It employs multiple differential pairs to achieve partial linearization of the input stage. The transconductance Gm is given by the expression (1/RE)(I2/I1). The circuit includes current sources I1 and I2, as well as a double current source 2I2. The output current io is derived from the collector currents of Q5 and Q6.

Fig. 12.31 A typical gain-cell transconductor.

### 12.6.2 Transconductors Using Multiple Differential Pairs

Quite a different approach for realizing a bipolar transconductor is by partially linearizing the input stage through the use of multiple differential pairs. To see how this linearization is achieved, consider a simple differential pair, as shown in Fig. 12.34(a). Ignoring base currents, we saw in Section 8.5.3 that the collector current $\mathbf{i}_{\mathrm{C} 2}$ is given by

$$
\begin{equation*}
\mathrm{i}_{\mathrm{C} 2}=\frac{\mathrm{I}_{1}}{1+\mathrm{e}^{\mathrm{v}_{\mathrm{i}} / \mathrm{V}_{\mathrm{T}}}} \tag{12.122}
\end{equation*}
$$

This current is plotted in Fig. $12.34(b)$, where we note that the curve is relatively linear near $v_{i}=0$. It is well known that the slope at this point equals the transconductance of this differential Ginput stage and is given by

$$
\begin{equation*}
\mathrm{G}_{\mathrm{m}}=\frac{1}{2 \mathrm{r}_{\mathrm{e}}}=\frac{\mathrm{I}_{1}}{4 \mathrm{~V}_{\mathrm{T}}} \tag{12.123}
\end{equation*}
$$

image_name:Fig. 12.32
description:The circuit represents a level shifter. VLS is a voltage source connected to a switch, and Q1 is an NPN transistor connected to VCC with a current source I3 flowing through its emitter to ground.

Fig. 12.32 A possible realization of the level shifters.
image_name:Fig. 12.33 A gain-cell transconductor with the gain cell below the input differential pair.
description:The circuit is a gain-cell transconductor with a differential input pair formed by Q1 and Q2. Q3 and Q4 form a current mirror. The output current is proportional to the input voltage difference. The transconductance Gm is determined by the resistors and current sources as shown in the formula.

Fig. 12.33 A gain-cell transconductor with the gain cell below the input differential pair.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: ic1, B: vi+, E: P}
name: Q2, type: NPN, ports: {C: ic2, B: vi-, E: P}
]
extrainfo:The circuit is a differential input pair with transistors Q1 and Q2. It is part of a gain-cell transconductor where the output current is proportional to the input voltage difference.
image_name:(b)
description:The graph in Fig. 12.34 (b) is a plot of the normalized output current \( \frac{i_{C2}}{I_1} \) versus the normalized input voltage \( \frac{v_i}{V_T} \), where \( V_T \) is the thermal voltage. This is a characteristic curve for a differential pair, showing how the current through one of the transistors (Q2) changes with respect to the input voltage difference across the differential pair.

**Type of Graph and Function:**
This is a characteristic curve for a differential amplifier, specifically showing the current transfer characteristic of a differential pair.

**Axes Labels and Units:**
- The x-axis represents the normalized input voltage \( \frac{v_i}{V_T} \), with values ranging from -10 to 10.
- The y-axis represents the normalized output current \( \frac{i_{C2}}{I_1} \), with values ranging from 0 to 1.

**Overall Behavior and Trends:**
The graph shows a sigmoidal curve, typical of differential pairs. At large negative input voltages, the normalized current \( \frac{i_{C2}}{I_1} \) approaches 1, indicating that most of the bias current \( I_1 \) flows through Q2. As the input voltage increases, the current through Q2 decreases, reaching approximately 0 when the input voltage is large and positive. This behavior is symmetric around the origin.

**Key Features and Technical Details:**
- The curve is steepest around the origin, indicating high sensitivity of the output current to changes in input voltage in this region. This is where the differential pair is most linear.
- The transition region, where the output current changes rapidly, occurs approximately between \( \frac{v_i}{V_T} = -2 \) and \( \frac{v_i}{V_T} = 2 \).

**Annotations and Specific Data Points:**
- The curve is symmetric around the y-axis, which is typical for differential pairs.
- No specific numerical annotations are provided, but the graph clearly shows the saturation regions and the linear operating region.

Fig. 12.34 (a) Differential pair. (b) Current output versus input voltage.

Thus, we see that the transconductance is proportional to the bias current, $\mathrm{I}_{1}$. Unfortunately, this two-transistor input stage has a very limited input range when used as a linear transconductor. In fact, when $\mathrm{v}_{\mathrm{i}}$ becomes greater than around $32 \mathrm{mV}_{\mathrm{pp}}$ (i.e., $\mathrm{v}_{\mathrm{i}}> \pm 16 \mathrm{mV}$ ), the total harmonic distortion of the output current becomes greater than 1 percent (see Example 12.8). We now discuss a method to use parallel differential pairs to increase the linear input range [Calder, 1984].

Consider the input stage shown in Fig. 12.35(a), where two differential pairs are connected in parallel but with a dc offset voltage applied to each. The currents of the right side transistors in each transistor pair are shown in Fig. 12.35(b). If the dc offset voltages, $\mathrm{v}_{1}$, are chosen carefully, then the two current curves will partially linearize each other when they are added together, as shown in Fig. 12.35(c). In this case, $\mathrm{v}_{1}$ is chosen to be equal to $1.317 \mathrm{~V}_{\mathrm{T}}$ to maximize the linear input range [Tanimoto, 1991]. As a result of this linearization technique, the input range can now be approximately three times that of the original differential pair or, equivalently, $96 \mathrm{mV}_{\mathrm{pp}}$, and achieve the same distortion performance.
image_name:(a)
description:The circuit is a linearized differential input stage using PNP transistors. It includes a technique to maximize the linear input range by choosing V1 = 1.317 VT. The current sources I1 are used for biasing the transistors Q2 and Q4.
image_name:(b)
description:The graph labeled (b) is a plot of the individual right-side collector currents, \(i_{C2}\) and \(i_{C4}\), in a differential pair circuit. The x-axis represents the normalized input voltage \(v_i/V_T\), where \(V_T\) is the thermal voltage, and it ranges from -10 to 10. The y-axis represents the normalized collector currents, \(i_{C2}/I_1\) and \(i_{C4}/I_1\), where \(I_1\) is a reference current, and it ranges from 0 to 1.

The graph shows two curves, each representing one of the collector currents. Both curves exhibit a sigmoidal shape, starting from a high value near 1 when \(v_i/V_T\) is negative, and decreasing to near 0 as \(v_i/V_T\) becomes positive. The curve for \(i_{C2}\) is slightly to the left of the curve for \(i_{C4}\), indicating that \(i_{C2}\) decreases slightly earlier than \(i_{C4}\) as \(v_i/V_T\) increases.

The behavior of the graph indicates a transition from a state where one transistor is conducting more current to a state where the other transistor conducts more, typical of a differential pair operation. The sigmoidal shape suggests a smooth transition between these states, with a central region where both currents are changing rapidly. This behavior is crucial for understanding the linearization effects and input range of the differential pair circuit as described in the context.
image_name:(c)
description:The graph labeled (c) is a plot demonstrating the total linearized current response of a differential pair of transistors. This is depicted as a function of the normalized input voltage, \( v_i/V_T \), where \( V_T \) is the thermal voltage.

1. **Type of Graph and Function:**
- This is a current-voltage (I-V) characteristic graph.

2. **Axes Labels and Units:**
- The x-axis represents the normalized input voltage \( v_i/V_T \) and is dimensionless, ranging from -10 to 10.
- The y-axis represents the normalized total collector current \((i_{c2} + i_{c4})/2I_1\), also dimensionless, ranging from 0 to 1.
- The scales on both axes are linear.

3. **Overall Behavior and Trends:**
- The graph shows a sigmoid-like curve, indicating a smooth transition from high to low current levels as the input voltage increases.
- Initially, for negative values of \( v_i/V_T \), the current remains high and close to 1.
- As \( v_i/V_T \) approaches zero and becomes positive, the current decreases significantly, eventually stabilizing at a lower value.

4. **Key Features and Technical Details:**
- The central transition region of the curve is where the linearization effect is most pronounced, and this is crucial for extending the linear input range.
- The curve demonstrates how the linearization technique allows for a broader range of input voltages while maintaining a consistent current response.

5. **Annotations and Specific Data Points:**
- The graph is marked with \((i_{c2} + i_{c4})/2I_1\), emphasizing the total current response of the system.
- No specific numerical data points or annotations are provided on this plot, but the overall shape and behavior are indicative of the linearization effect discussed.

Fig. $\mathbf{1 2 . 3 5}$ (a) A linearized differential input; (b) individual right-side currents; (c) total linearized
To reduce circuitry, the two dc offset voltage sources can be eliminated by sizing the differential pair of transistors appropriately. Specifically, assuming that $\mathrm{V}_{\mathrm{i}}=0$, then when $\mathrm{V}_{1}=1.317 \mathrm{~V}_{\mathrm{T}}$, the collector currents of $\mathrm{Q}_{2}$ and $Q_{4}$ are given by

$$
\begin{equation*}
\mathrm{i}_{\mathrm{C} 2}=\frac{\mathrm{I}_{1}}{1+\mathrm{e}^{1.317}}=0.2113 \mathrm{I}_{1} \tag{12.124}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathbf{i}_{\mathrm{C} 4}=\mathbf{i}_{\mathrm{C} 1}=\frac{\mathrm{I}_{1}}{1+\mathrm{e}^{-1.317}}=0.7887 \mathrm{I}_{1} \tag{12.125}
\end{equation*}
$$

If a two-transistor differential pair has unequal-sized transistors such that the same two currents occur for $v_{i}=0$, then this unequal-sized differential pair will behave the same as that of an equal-sized differential pair with a dc offset applied. To determine the sizing of the unequal-sized differential pair, define k to be the ratio of the baseemitter area of $Q_{1}$ with respect to $Q_{2}$. Thus, for this unequal-sized case, when $v_{i}=0$, we have

$$
\begin{equation*}
\mathrm{i}_{\mathrm{C} 1}=\mathrm{kI} \mathrm{I}_{\mathrm{s}} \mathrm{e}^{\left(\mathrm{v}_{\mathrm{be}} / \mathrm{V}_{\mathrm{T}}\right)}=0.7887 \mathrm{I}_{1} \tag{12.126}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathbf{i}_{\mathrm{C} 2}=\mathrm{I}_{\mathrm{s}} \mathrm{e}^{\left(\mathrm{v}_{\mathrm{be}} / \mathrm{v}_{\mathrm{T}}\right)}=0.2113 \mathrm{I}_{1} \tag{12.127}
\end{equation*}
$$

Dividing (12.126) by (12.127), we obtain

$$
\begin{equation*}
k=3.73 \tag{12.128}
\end{equation*}
$$

Thus, we should make $Q_{1} 3.73$ times larger than $Q_{2}$, and similarily $Q_{4}$ should be 3.73 times larger than $Q_{3}$. Such transistor sizing achieves the same result as the dc offset voltages. This result should make intuitive sense
image_name:Fig. 12.36
description:The circuit is a linearized differential transconductor with transistors Q1 and Q4 sized 4 times larger than Q2 and Q3. The transconductance Gm is given by 8I1/25VT.

Fig. 12.36 Using transistor sizing to create a linearized differential transconductor.
since we require that the ratio of the two currents be $0.7887 / 0.2113$ when their base-emitter voltages are equal; this requirement results in the area ratio. Typically, this area ratio is set to 4 for practical reasons, and the final linearized transconductor is realized as shown in Fig. 12.36. Thus, for this circuit with $\mathrm{v}_{\mathrm{i}}=0$, the currents through $Q_{1}$ and $Q_{2}$ are $0.8 I_{1}$ and $0.2 I_{1}$, respectively.

To determine the transconductance of the circuit of Fig. 12.36, we note that $\mathrm{G}_{\mathrm{m}}$ equals the sum of the transconductance of the two differential pairs, resulting in

$$
\begin{equation*}
G_{m}=\frac{1}{r_{e 1}+r_{e 2}}+\frac{1}{r_{e 3}+r_{e 4}} \tag{12.129}
\end{equation*}
$$

Also, at $\mathrm{v}_{\mathrm{i}}=0$, we have

$$
\begin{equation*}
r_{e 1}=r_{e 4}=\frac{V_{T}}{0.8 I_{1}} \tag{12.130}
\end{equation*}
$$

and

$$
\begin{equation*}
r_{e 2}=r_{e 3}=\frac{V_{T}}{0.2 I_{1}} \tag{12.131}
\end{equation*}
$$

Combining (12.129) to (12.131), we have

$$
\begin{equation*}
\mathrm{G}_{\mathrm{m}}=\frac{8 \mathrm{I}_{1}}{25 \mathrm{~V}_{\mathrm{T}}} \tag{12.132}
\end{equation*}
$$

which is 28 percent greater than the transconductance value for the transistor pair shown in Fig. 12.34(a). However, this comparison is not fair since two differential pairs and twice the current are used in this linearized approach. If two differential pairs of Fig. 12.34(a) are used together, then their total transconductance would be $\mathrm{G}_{\mathrm{m}}=\mathrm{I}_{1} /\left(2 \mathrm{~V}_{\mathrm{T}}\right)$, implying that this linearized approach has a 36 percent smaller transconductance. Also note that, as in the two-transistor pair case, this transconductance value is also proportional to the bias current, $\mathrm{I}_{1}$, and thus no gain cell is required.

This approach was ued in a 2 - to $10-\mathrm{MHz}$ programmable filter intended for disk-drive applications in [De Veirman, 1992]. This same technique can be extended to a larger number of input stages to further improve the
linear input range [Tanimoto, 1991]. Using four differential input pairs in parallel, the linear input range was reported to be 16 times better than that for a single differential pair.

#### EXAMPLE 12.8

Consider the single differential pair shown in Fig. 12.34(a), where $I_{1}=2 \mathrm{~mA}$. Find the percentage error between an ideal linear transconductor and the true output current when $\mathrm{v}_{\mathrm{i}}=16 \mathrm{mV}$.

#### Solution

Using (12.123), we have

$$
\begin{equation*}
\mathrm{G}_{\mathrm{m}}=\frac{\mathrm{I}_{1}}{4 \mathrm{~V}_{\mathrm{T}}}=19.2 \mathrm{~mA} / \mathrm{V} \tag{12.133}
\end{equation*}
$$

Thus, for an ideal linear transconductor, the output current for a $16-\mathrm{mV}$ input voltage would be

$$
\begin{equation*}
\mathrm{i}_{\mathrm{o}}=\mathrm{G}_{\mathrm{m}} \times 16 \mathrm{mV}=0.307 \mathrm{~mA} \tag{12.134}
\end{equation*}
$$

The true output current can be found from (12.122) as

$$
\begin{align*}
& \mathrm{I}_{\mathrm{C} 2}=\frac{2 \mathrm{~mA}}{1+\mathrm{e}^{16 / 26}}=0.702 \mathrm{~mA}  \tag{12.135}\\
& \mathrm{I}_{\mathrm{C} 1}=\frac{2 \mathrm{~mA}}{1+\mathrm{e}^{-16 / 26}}=1.298 \mathrm{~mA} \tag{12.136}
\end{align*}
$$

implying that the change in current from the bias current of 1 mA is 0.298 mA . Thus, the percentage error between the true output current and the ideal linear transconductor output is

$$
\begin{equation*}
\frac{0.298-0.307}{0.307} \times 100=-3 \% \tag{12.137}
\end{equation*}
$$

In this case, the deviation is three-percent worst case, which results in about a one-percent total-harmonicdistortion (THD) measurement (see Section 9.5.1).

#### EXAMPLE 12.9

Consider the linearized differential pairs shown in Fig. 12.35(a), where $I_{1}=2 \mathrm{~mA}$. Find the percentage error between an ideal linear transconductor and the true output current when $\mathrm{v}_{\mathrm{i}}=16 \mathrm{mV}$.

#### Solution

First, we need to derive a formula for $G_{m}$ in a manner similar to that for (12.132), where

$$
\begin{align*}
& r_{\mathrm{e} 1}=r_{\mathrm{e} 4}=\frac{\mathrm{V}_{\mathrm{T}}}{0.7887 \mathrm{I}_{1}}  \tag{12.138}\\
& \mathrm{r}_{\mathrm{e} 2}=\mathrm{r}_{\mathrm{e} 3}=\frac{\mathrm{V}_{\mathrm{T}}}{0.2113 \mathrm{I}_{1}} \tag{12.139}
\end{align*}
$$

Thus, the transconductance is given by

$$
\begin{equation*}
\mathrm{G}_{\mathrm{m}}=\frac{1}{\mathrm{r}_{\mathrm{e} 1}+\mathrm{r}_{\mathrm{e} 2}}+\frac{1}{\mathrm{r}_{\mathrm{e} 3}+\mathrm{r}_{\mathrm{e} 4}}=\frac{0.333 \mathrm{I}_{1}}{\mathrm{~V}_{\mathrm{T}}}=25.6 \mathrm{~mA} / \mathrm{V} \tag{12.140}
\end{equation*}
$$

For an ideal linear transconductor, the output current for a $16-\mathrm{mV}$ input voltage would result in

$$
\begin{equation*}
\mathrm{i}_{\mathrm{o}}=\mathrm{G}_{\mathrm{m}} \times 16 \mathrm{mV}=0.4102 \mathrm{~mA} \tag{12.141}
\end{equation*}
$$

To calculate the true output current, we first note that

$$
\begin{equation*}
\mathrm{v}_{1}=1.317 \mathrm{~V}_{\mathrm{T}}=34.24 \mathrm{mV} \tag{12.142}
\end{equation*}
$$

and since $v_{i}=16 \mathrm{mV}$, we use $v_{i}+v_{1}$ to find $I_{C 1}$, resulting in

$$
\begin{align*}
& \mathrm{I}_{\mathrm{C} 1}=\frac{2 \mathrm{~mA}}{1+\mathrm{e}^{-50.24 / 26}}=1.747 \mathrm{~mA}  \tag{12.143}\\
& \mathrm{I}_{\mathrm{C} 2}=2 \mathrm{~mA}-\mathrm{I}_{\mathrm{C} 1}=0.253 \mathrm{~mA} \tag{12.144}
\end{align*}
$$

For $\mathrm{I}_{\mathrm{C} 4}$, we use $\mathrm{v}_{1}-\mathrm{v}_{\mathrm{i}}$ to obtain

$$
\begin{align*}
& \mathrm{I}_{\mathrm{C} 4}=\frac{2 \mathrm{~mA}}{1+\mathrm{e}^{-18.24 / 26}}=1.337 \mathrm{~mA}  \tag{12.145}\\
& \mathrm{I}_{\mathrm{C} 3}=2 \mathrm{~mA}-\mathrm{I}_{\mathrm{C} 4}=0.663 \mathrm{~mA} \tag{12.146}
\end{align*}
$$

The true output is then equal to

$$
\begin{align*}
& \mathrm{I}_{\mathrm{C} 1}+\mathrm{I}_{\mathrm{C} 3}=2.41 \mathrm{~mA}  \tag{12.147}\\
& \mathrm{I}_{\mathrm{C} 2}+\mathrm{I}_{\mathrm{C} 4}=1.59 \mathrm{~mA} \tag{12.148}
\end{align*}
$$

implying that the change in current from the bias current of 2 mA is 0.4099 mA . Thus, the percentage error between the true output current and the ideal linear transconductor output is

$$
\begin{equation*}
\frac{0.4099-0.4102}{0.4102} \times 100=-0.1 \% \tag{12.149}
\end{equation*}
$$

Note that this error is over ten times better than with a simple differential pair.

## 12.7 BICMOS TRANSCONDUCTORS

In this section, we discuss some of the reported approaches for realizing BiCMOS transconductors and filters.

### 12.7.1 Tunable MOS in Triode

One approach for realizing a BiCMOS integrator is shown in Fig. 12.37 [Laber, 1993]. Here, linearization and tuning are accomplished by using transistors $Q_{1}$ through $Q_{4}$, which are all assumed to be in the triode region. As we saw in Section 12.4, the currents through these transistors are ideally linear if their drain-source voltages are kept constant. Although in practice these currents have rather large second-order distortion, fortunately even-order distortion products are significantly reduced in a fully differential structure. The drain-source voltages of $Q_{1}$ through $Q_{4}$ are controlled through the use of the two emitter followers, $Q_{5}, Q_{6}$. This simple voltage control is one of the benefits of using a BiCMOS process since a MOS source follower would have too much voltage variation. Note that additional inputs into this integrator are added as simply two extra transistors (a two-input integrator is shown). Various coefficient ratios can be obtained by scaling the sizes of the input transistors. However, because of the shown tuning circuit connection, all coefficients in one integrator will scale together as the control voltage is varied. Note also that a $\mathrm{G}_{\mathrm{m}}-\mathrm{C}$ opamp integrator is used to reduce the effects of parasitic capacitance.
image_name:Fig. 12.37
description:The circuit is a fully differential two-input BiCMOS integrator using MOS transistors in triode mode. It includes common-mode feedback for the output and lead compensation realized by Q7 and Q8. The integrator uses a Gm-C opamp configuration to reduce parasitic capacitance effects. The control voltage scales all coefficients in the integrator simultaneously.

Fig. 12.37 A fully differential two-input BiCMOS integrator using MOS transistors in triode, $\mathrm{Q}_{1}$ through $Q_{4} G_{m}-C$ opamp integration is used to reduce parasitic capacitance effects. Note that, in addition to a common-mode feedback circuit for the output (not shown), the common-mode voltage at the input nodes of the opamp must also be set.

Also, transistors $\mathrm{Q}_{7}, \mathrm{Q}_{8}$ are included to realize lead compensation. Finally, it should be mentioned that a common-mode feedback circuit is required at the output nodes of the differential opamp. Also, some method is needed for setting the common-mode voltage at the opamp inputs. The BiCMOS filter in [Laber, 1993] is built in a $1.5-\mu \mathrm{m}, 4-\mathrm{GHz}$ BiCMOS technology and operated around 20 MHz using a $5-\mathrm{V}$ supply. The transconductor demonstrated moderate linearity of around 50 dB when processing $2-\mathrm{V}_{\mathrm{pp}}$ differential output signals, but no mention is made of any intermodulation results or the frequency of the test signals.

### 12.7.2 Fixed-Resistor Transconductor with a Translinear Multiplier

Another approach that has been successfully used to realize BiCMOS filters that have very high linearity has been to use highly linear transconductors realized using fixed resistors and then achieve tuning by following the transconductor with a translinear multiplier. As we saw in Chapter 11, the output of a translinear multiplier is linear with respect to one of its input currents, and its gain coefficient can be scaled as the ratio of two other currents in either a positive or negative fashion.

A translinear multiplier can be used for realizing a low-distortion BiCMOS integrator, as shown in Fig. 12.38 [Willingham, 1993]. Here, the output currents from fixed-value transconductors are applied to a translinear multiplier, such that tuning can be accomplished while maintaining high linearity. The outputs of the translinear multiplier are applied to a opamp-based integrator to maintain high linearity. In this implementation, the input impedance of the fully differential opamp is kept low such that a fixed voltage occurs at the input nodes of the opamp, thereby setting the input common-mode voltage. Phase-lead resistors are also used in series with the integration capacitors (not shown) to improve the integrator's phase response.

The fixed transconductors are realized using resistor degeneration and local feedback, as shown in Fig. 12.39. Fig. 12.39(a) shows that local feedback around the two shown opamps force their input nodes to be equal, and therefore the applied input voltage appears across $\mathrm{R}_{\mathrm{x}}$. A simplified circuit implementation of this approach is shown in Fig. 12.39(b), which shows that the opamps are implemented with only a PMOS transistor and current source.

This integrator was used to build a seventh-order low-pass filter in a $2-\mu \mathrm{m}, 2.5-\mathrm{GHz}$ BiCMOS process that featured thin-film resistors. The filter passband edge was tunable from 7.5 MHz to 10 MHz . The results of this low-distortion BiCMOS filter are quite impressive; third-order intermodulation products remained below 65 dB ,
image_name:Fig. 12.38
description:The system block diagram in Fig. 12.38 represents a two-input BiCMOS integrator using fixed resistor-degenerated transconductors in conjunction with a translinear multiplier for tuning. This integrator is designed to manage signal processing in a BiCMOS environment.

1. **Main Components:**
- **Transconductors (g_{m1} and g_{m2}):** These are the initial components that receive the input signals (v₁⁺, v₁⁻, v₂⁺, v₂⁻). They convert input voltage signals into current signals (I₂ + i₂ and I₂ - i₂).
- **Translinear Multiplier:** This block receives the current outputs from the transconductors and is responsible for controlling and tuning the output signal. It has two inputs labeled as Input 1 (Control) and Input 2, and provides an output that is connected to nodes A and B.
- **Operational Amplifier (Op-Amp):** Connected to the output of the translinear multiplier through nodes A and B, this op-amp is configured with capacitors (C_I) in a feedback loop to form an integrator.
- **Capacitors (C_I):** These are connected in feedback loops around the op-amp to create integration of the input signal, contributing to the low-pass filter functionality.

2. **Flow of Information or Control:**
- The input signals (v₁⁺, v₁⁻, v₂⁺, v₂⁻) are fed into the transconductors, which convert them into currents.
- These currents (I₂ + i₂ and I₂ - i₂) are directed into the translinear multiplier, which modulates them according to the control input (Input 1).
- The output of the translinear multiplier is then sent to nodes A and B, which are inputs to the op-amp.
- The op-amp, with capacitors in the feedback loop, integrates the signal, producing output voltages (vₒ⁺ and vₒ⁻).

3. **Labels, Annotations, and Key Indicators:**
- Inputs are labeled as Input 1 (Control) and Input 2, indicating their roles in modulation and signal processing.
- Nodes A and B serve as critical connection points between the translinear multiplier and the op-amp.

4. **Overall System Function:**
- The primary function of this system is to integrate input signals using a BiCMOS process. The use of transconductors and a translinear multiplier allows for precise control and tuning of the signal integration, which is essential for applications like low-pass filtering. The configuration ensures that the common-mode voltage at nodes A and B is maintained, enhancing the stability and performance of the integrator.

Fixed transconductors
Fig. 12.38 A two-input BiCMOS integrator using fixed resistor-degenerated transconductors together with a translinear multiplier for tuning. The common-mode voltage at nodes A and B was set by using a low-input-impedance opamp.
image_name:(a)
description:This is a two-input BiCMOS integrator using fixed resistor-degenerated transconductors. The integrator uses a translinear multiplier for tuning, and the common-mode voltage at nodes is set by using a low-input-impedance opamp.
image_name:(b)
description:The circuit is a BiCMOS integrator using fixed resistor-degenerated transconductors and a translinear multiplier for tuning. It maintains the common-mode voltage at nodes A and B using low-input-impedance opamps. The current sources IB1 and IB2, along with the resistors and transistors, control the signal integration. The diagram shows a configuration that enhances stability and performance by setting the common-mode voltage.

Fig. 12.39 A fixed BiCMOS transconductor: (a) the two local feedbacks keep the input voltage applied across $R_{x}$; (b) circuit implementation.
with respect to the input signal, when measured using two-tone inputs near 4 MHz . Finally, it should be mentioned that the circuit also uses a center tap on each of the $\mathrm{R}_{\mathrm{x}}$ resistors to set the common-mode voltage of the preceding output. With this simple addition, much of the traditional common-mode circuitry is eliminated since it is necessary only to compare the center tap voltage with a dc reference signal and then feed back the appropriate control signal.

Similar approaches, in which a highly linear transconductor that has local feedback is followed by a current attenuator, are also possible using ordinary CMOS and are now gaining in popularity [Chang, 1995].

### 12.7.3 Fixed Active MOS Transconductor with a Translinear Multiplier

A BiCMOS integrator intended for applications that require high-speed operation, wide tuning range, and only moderate linearity is shown in Fig. 12.40 [Shoval, 1993]. In this circuit, the common-mode voltage, $\mathrm{V}_{\mathrm{CM}}$, is set to a constant value (it is set by a common-mode feedback circuit); the result is that the differential currents of $Q_{1}, Q_{4}$ and $Q_{2}, Q_{3}$ are linearly related to the balanced differential voltage (as discussed in Section 12.5). This linear volt-age-to-current conversion remains at a fixed value (resulting in a relatively constant linearity performance and
image_name:Fig. 12.40
description:The circuit is a BiCMOS integrator using MOS transistors in the active region for linearization and a translinear multiplier for tuning. It features common-mode feedback to maintain constant linearity performance. The input swing is controlled by two pairs of MOS transistors performing voltage-to-current conversion on the balanced input signal.

Fig. 12.40 A BiCMOS integrator using MOS transistors in the active region for linearization, and a translinear multiplier for tuning. The common-mode feedback circuit is not shown.
input swing level), and transconductance tuning is performed with the aid of a translinear multiplier. Note, however, that two pairs of MOS transistors are performing voltage-to-current conversion on the balanced input signal. The reason for using two pairs is to maximize the largest possible transconductance of the overall circuit for a given bias current. Specifically, if the multiplier is tuned to send all of $\mathrm{i}_{\mathrm{C} 6}, \mathrm{i}_{\mathrm{C} 7}$ through to $\mathrm{v}_{\mathrm{o}}^{+}, \mathrm{v}_{\mathrm{o}}^{-}$, respectively, then the signal currents add together and the overall transconductance is equal to twice that which occurs for a single set of MOS transistors (without an increase in bias current). Alternatively, if the multiplier is tuned to send all of $\mathrm{i}_{\mathrm{C} 6}, \mathrm{i}_{\mathrm{C} 7}$ through to $\mathrm{v}_{\mathrm{o}}^{-}, \mathrm{v}_{\mathrm{o}}^{+}$, respectively, then the currents subtract, causing a zero overall transconductance. Finally, if the translinear multiplier is tuned to cause a zero output (i.e., to cause two constant dc currents at the multiplier outputs), the overall transconductance is equal to that caused by transistors $Q_{2}, Q_{3}$, which is half the maximum value. Thus, the use of two pairs on the input signal doubles the maximum possible transconductance at the cost of being able to tune the transconductance only from zero to the maximum value. In other words, the overall transconductance value cannot change signs by changing the multiplier control signal. Of course, both positive and negative transconductance values can be obtained by cross-coupling the output signals.

This BiCMOS integrator is used to realize a second-order pulse-shaping filter operating on $100-\mathrm{Mb} / \mathrm{s}$ data. Although the filter has a wide tuning range of approximately $10: 1$, it achieves only a moderate spurious-free dynamic range level of 35 dB .

## 12.8 ACTIVE RC AND MOSFET-C FILTERS

Another technique for the realization of analog integrated filters is active RC or MOSFET-C filters. In both techniques, integration of current is performed upon capacitors connected in feedback around a high-gain amplifier, as opposed to transconductance-C filters which use grounded capacitors to integrate current. This is sometimes called Miller integration, since like the Miller compensation capacitor in a two-stage opamp, integrating capacitors are connected around high-gain amplifiers. Miller integration improves linearity, but the need for a high gain-bandwidth product in the amplifier makes active RC and MOSFET-C filters generally slower than their $\mathrm{G}_{\mathrm{m}}-\mathrm{C}$ counterparts. Also, they are further reduced in speed in a CMOS technology because opamps capable of driving resistive loads are required as opposed to only capacitive loads in $\mathrm{G}_{\mathrm{m}}-\mathrm{C}$ filters. However, they are particularly attractive in BiCMOS technologies where high-transconductance opamps are available.

### 12.8.1 Active RC Filters

Active RC filters are well established in both discrete component and integrated analog filter design. Recall that the basic building blocks of analog filters are the integrator, summer, and gain stage. A basic active RC integrator is shown in single-ended form in Fig. 12.41(a). Assuming an ideal opamp, a virtual ground is maintained at $\mathrm{V}_{\mathrm{x}}$. Hence, voltage-to-current conversion is performed by the resistor $R$. The gain of this conversion is determined by the resistor value, which unfortunately will vary under process and temperature variations. However, the use of a passive resistor provides excellent linearity. The resulting current is the integrated upon the capacitor $C_{1}$ and the inverted output appears at $v_{0}$.

Key Point: Active RC filters employ resistors connected to virtual ground nodes to perform voltage-to-current conversion, and then integrate the resulting currents upon Miller capacitors, connected in feedback around high-gain amplifiers.

In Fig. $12.41(b)$, summing is incorporated into the integrator. Its fully-differential implementation is shown. The resistors $\mathrm{R}_{\mathrm{p} 1, \mathrm{p} 2, \mathrm{n} 1, \mathrm{n} 2}$ convert the differential voltage inputs into differential currents. The currents $i_{p 1, p_{2}}$ and $i_{n 1, n 2}$ are then summed by shunting them at the virtual ground nodes $\mathrm{V}_{\mathrm{x}}$. The resulting total current is integrated upon the capacitors $C_{1}$. If pure gain and/or summartion is required without integration, the capacitors may be replaced by resistors in feedback around the opamp, resulting in the familiar inverting opamp configuration.

#### EXAMPLE 12.10

Consider the basic active RC integrator of Fig. 12.41(a), but assume the opamp has a first-order open-loop response characterized by a finite dc gain of $\mathrm{A}_{0}$ and unity-gain frequency $\omega_{\mathrm{ta}}$. What is the resulting frequency response of the integrator?

#### Solution

The frequency response is the expected ideal value of $-1 /(s R C)$ multiplied by $\mathrm{L}(\mathrm{s}) /(1+\mathrm{L}(\mathrm{s})$ ) where $\mathrm{L}(\mathrm{s})$ is the open loop response, being the product of the opamp's open-loop frequency response,

$$
\begin{equation*}
\mathrm{A}(\mathrm{~s})=\frac{\mathrm{A}_{0}}{1+\frac{\mathrm{A}_{0} \mathrm{~S}}{\omega_{\mathrm{ta}}}} \tag{12.150}
\end{equation*}
$$

and the feedback network's frequency response

$$
\begin{equation*}
\beta(s)=\frac{s R C}{1+s R C} \tag{12.151}
\end{equation*}
$$

image_name:(a)
description:
[
name: R, type: Resistor, value: R, ports: {N1: Vi, N2: Vx}
name: C_I, type: Capacitor, value: C_I, ports: {Np: Vx, Nn: Vo}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: Vx, Out: Vo}
]
extrainfo:This is a single-ended active RC integrator circuit. The input voltage is vi, and the output voltage is Vo. The circuit integrates the input signal over time, producing an output that is proportional to the integral of the input.
image_name:(b)
description:
[
name: Rp1, type: Resistor, value: Rp1, ports: {N1: vp1, N2: Vx}
name: Rp2, type: Resistor, value: Rp2, ports: {N1: vp2, N2: Vx}
name: Rn2, type: Resistor, value: Rn2, ports: {N1: vn2, N2: Vx}
name: Rn1, type: Resistor, value: Rn1, ports: {N1: vn1, N2: Vx}
name: CI, type: Capacitor, value: CI, ports: {Np: Vx, Nn: vno}
name: CI, type: Capacitor, value: CI, ports: {Np: Vx, Nn: vpo}
name: A1, type: OpAmp, value: A1, ports: {InP: Vx, InN: Vx, OutP: Vno, OutN: Vpo}
]
extrainfo:This is a two-input active-RC fully differential integrator. The circuit integrates multiple input signals over time, producing differential outputs.

Fig. 12.41 (a) A single-ended active RC integrator. (b) A two-input active-RC fully differential integrator.
image_name:Fig. 12.42
description:The graph in Fig. 12.42 is a Bode plot depicting the frequency response of an active RC integrator with finite opamp bandwidth and unity-gain frequency. It consists of two subplots: one for magnitude and one for phase.

1. **Magnitude Plot (|H(ω)|):**
- **Axes:**
- The vertical axis represents the magnitude of the transfer function, |H(ω)|, in decibels (dB).
- The horizontal axis represents frequency, ω, in a logarithmic scale.
- **Behavior:**
- The plot starts at a high gain value, A₀, and shows a downward slope as frequency increases.
- The slope of the magnitude plot is approximately -20 dB/decade, indicating a first-order roll-off.
- At the frequency ωₜₐ, the slope becomes steeper, deviating from the ideal integrator's slope, which is represented by a dashed line continuing at -20 dB/decade.
- **Key Features:**
- The starting point at A₀ indicates the DC gain of the integrator.
- The deviation point at ωₜₐ marks the transition from the ideal behavior due to the finite bandwidth of the opamp.

2. **Phase Plot (∠H(ω)):**
- **Axes:**
- The vertical axis represents the phase angle of the transfer function, ∠H(ω), in degrees.
- The horizontal axis represents frequency, ω, in a logarithmic scale.
- **Behavior:**
- The phase starts at 90° for low frequencies, consistent with an ideal integrator.
- As frequency increases, the phase gradually decreases, approaching 180°.
- This shift indicates the phase lag introduced by the non-ideal components of the circuit.
- **Key Features:**
- The phase shift is gradual, with a notable deviation from the ideal 90° line as frequency approaches ωₜₐ.
- The dashed line at 90° represents the ideal integrator phase response.

Overall, the Bode plot illustrates how the integrator's performance deviates from the ideal due to the opamp's finite bandwidth, affecting both gain and phase at higher frequencies.

Fig. 12.42 The Bode plot of an active RC integrator with finite opamp bandwidth and unity-gain frequency.

Using (12.150) and (12.151) allows us to find the nonideal integrator's actual frequency response.

$$
\begin{equation*}
H(s)=-\frac{1}{(s R C)} \cdot \frac{\left(\frac{A_{0}}{1+\mathrm{A}_{0} s / \omega_{\mathrm{ta}}}\right)\left(\frac{\mathrm{sRC}}{1+\mathrm{sRC}}\right)}{1+\left(\frac{\mathrm{A}_{0}}{1+\mathrm{A}_{0} \mathrm{~s} / \omega_{\mathrm{ta}}}\right)\left(\frac{\mathrm{sRC}}{1+\mathrm{sRC}}\right)} \tag{12.152}
\end{equation*}
$$

Making the assumption $\omega_{\mathrm{ta}} \gg>1 / \mathrm{RC},(12.152)$ may be manipulated to show

$$
\begin{equation*}
\mathrm{H}(\mathrm{~s}) \cong-\frac{\mathrm{A}_{0}}{\left(1+\mathrm{sA} \mathrm{~A}_{0} \mathrm{RC}\right)\left(1+\mathrm{s} / \omega_{\mathrm{ta}}\right)} \tag{12.153}
\end{equation*}
$$

A bode plot of $\mathrm{H}(\mathrm{s})$ appears in Fig. 12.42. Rather than the infinite dc gain provided by an ideal integrator, the dc gain is simply that of the opamp, $A_{0}$. At angular frequencies above $1 / A_{0} R C$, the frequency response is a good approximation of the ideal integrator, $-1 / \mathrm{sRC}$. Then, at frequencies around the unity gain frequency of the opamp, the integrator again deviates from its ideal value due to the limited gain-bandwidth of the opamp. Hence, the integrator is well behaved over the frequency range $1 / A_{0} R C<\omega<\omega_{t a}$ which may place requirements upon the opamp's dc gain and unity gain frequency.
image_name:Fig. 12.43
description:
[
name: Qp1, type: PMOS, ports: {S: Vp1, D: Vx, G: Vc}
name: Qp2, type: PMOS, ports: {S: Vp2, D: Vx, G: Vc}
name: Qn2, type: NMOS, ports: {S: Vx, D: Vn2, G: Vc}
name: Qn1, type: NMOS, ports: {S: Vx, D: Vn1, G: Vc}
name: CI1, type: Capacitor, value: CI, ports: {Np: Vx, Nn: Vno}
name: CI2, type: Capacitor, value: CI, ports: {Np: Vx, Nn: Vpo}
name: OpAmp, type: OpAmp, ports: {InP: Vx, InN: Vx, OutP: Vno, OutN: Vpo}
]
extrainfo:The circuit is a MOSFET-C integrator using two PMOS and two NMOS transistors, with an operational amplifier and two capacitors. The MOS transistors are in the triode region, and the circuit is designed to function as an integrator over a specific frequency range.

Fig. 12.43 A two-input two-transistor MOSFET-C integrator. The MOS transistors are in the triode region.

Based on the block diagram shown in Fig. 12.2, an example active RC implementation of the two-integrator biquad is illustrated in Fig. 12.44(a). The negative conductances are easily realized by cross-connections in a fully-differential implementation. Note that two opamps are required: one for each integrator-hence, one for each pole in the filter. The output of the first integrator is given by

$$
\begin{equation*}
v_{1}(s)=-\frac{G_{1}}{s C_{A}} v_{i}(s)-\frac{G_{4}}{s C_{A}} v_{o}(s) \tag{12.154}
\end{equation*}
$$

whereas the second integrator's output is given by

$$
\begin{equation*}
s C_{B} v_{0}(s)=G_{3} v_{1}(s)-G_{2} v_{i}(s)-s C_{1} v_{i}(s)-G_{5} v_{0}(s) \tag{12.155}
\end{equation*}
$$

Combining the preceding two equations and rearranging, we have

$$
\begin{equation*}
\frac{v_{o}(s)}{v_{i}(s)}=-\frac{\left[\left(\frac{C_{1}}{C_{B}}\right) s^{2}+\left(\frac{G_{2}}{C_{B}}\right) s+\left(\frac{G_{1} G_{3}}{C_{A} C_{B}}\right)\right]}{\left[s^{2}+\left(\frac{G_{5}}{C_{B}}\right) s+\left(\frac{G_{3} G_{4}}{C_{A} C_{B}}\right)\right]} \tag{12.156}
\end{equation*}
$$

Thus, we see that the transfer function is general, and that negative coefficients can be realized by crosscoupling appropriate signal wires.

### 12.8.2 MOSFET-C Two-Transistor Integrators

MOSFET-C filters are similar to fully differential active-RC filters, except resistors are replaced with equivalent MOS transistors in triode. Since active-RC and MOSFET-C filters are closely related, one benefit of MOSFET-C filters is that a designer can use the wealth of knowledge available for active-RC filters. Here, we discuss three variations of MOSFET-C filters-two-transistor integrators, four-transistor integrators, and R-MOSFET-C filters.

An example of a two-transistor MOSFET-C integrator is shown in Fig. 12.43 [Banu, 1983]. It is the counterpart of the two-input fully differential active-RC integrator of Fig. 12.41(b). Before we look at the linearization mechanism that occurrs in a MOSFET-C integrator, let us look at the equivalence of the two circuits in Fig. 12.41(b) and Fig. 12.43. In the active-RC filter, the two input voltages of the opamp are equal (due to negative feedback) and, defining these two input voltages to be $\mathrm{V}_{\mathrm{x}}$, we can write

$$
\begin{equation*}
i_{n o}=i_{p 1}+i_{p 2}=\frac{v_{p 1}-V_{x}}{R_{p 1}}+\frac{v_{p 2}-V_{x}}{R_{p 2}} \tag{12.157}
\end{equation*}
$$

and

$$
\begin{equation*}
i_{p o}=i_{n 1}+i_{n 2}=\frac{v_{n 1}-V_{x}}{R_{n 1}}+\frac{v_{n 2}-V_{x}}{R_{n 2}} \tag{12.158}
\end{equation*}
$$

The output signals are given by

$$
\begin{equation*}
v_{p o}=V_{x}-\frac{i_{p o}}{s C_{I}} \tag{12.159}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{v}_{\mathrm{no}}=\mathrm{V}_{\mathrm{x}}-\frac{\mathrm{i}_{\mathrm{no}}}{\mathrm{~s} \mathrm{C}_{\mathrm{I}}} \tag{12.160}
\end{equation*}
$$

Thus, the differential output signal, $\mathrm{v}_{\text {diff }}$, is

$$
\begin{equation*}
v_{\text {diff }} \equiv v_{\mathrm{po}}-\mathrm{v}_{\mathrm{no}}=\frac{\mathrm{i}_{\mathrm{no}}-\mathrm{i}_{\mathrm{p}}}{\mathrm{~s} C_{\mathrm{I}}} \tag{12.161}
\end{equation*}
$$

Assuming the component values in the positive and negative half circuits are equal, or specifically, if

$$
\begin{equation*}
\mathrm{R}_{1} \equiv \mathrm{R}_{\mathrm{p} 1}=\mathrm{R}_{\mathrm{n} 1} \quad \text { and } \quad \mathrm{R}_{2} \equiv \mathrm{R}_{\mathrm{p} 2}=\mathrm{R}_{\mathrm{n} 2} \tag{12.162}
\end{equation*}
$$

we have

$$
\begin{equation*}
v_{\text {diff }}=\frac{1}{s R_{1} C_{I}}\left(v_{p 1}-v_{n 1}\right)+\frac{1}{s R_{2} C_{I}}\left(v_{p 2}-v_{n 2}\right) \tag{12.163}
\end{equation*}
$$

Thus, we see that the differential output signal, $\mathrm{v}_{\text {diff }}$, equals positive integration of the two input differential signals. Negative integration is easily obtained by cross-coupling two input or output wires. Note that the commonmode signal, $\mathrm{V}_{\mathrm{x}}$, does not affect the final result.

Since the transistors in the MOSFET-C integrator, shown in Fig. 12.43, are assumed to be in the triode region, the small-signal analysis for the MOSFET-C integrator is quite similar to that for the active-RC circuit. Recall from (12.57) that the small-signal equivalent resistance of a transistor in triode is given by

$$
\begin{equation*}
r_{D S}=\frac{1}{\mu_{\mathrm{n}} C_{o x}\left(\frac{W}{L}\right)\left(V_{G S}-V_{t n}\right)} \tag{12.164}
\end{equation*}
$$

Thus, assuming the transistors are matched, the differential output of the MOSFET-C integrator is given by

$$
\begin{equation*}
v_{\text {diff }}=\frac{1}{s r_{\mathrm{DS} 1} C_{I}}\left(v_{p 1}-v_{n 1}\right)+\frac{1}{s r_{D S 2} C_{I}}\left(v_{p 2}-v_{n 2}\right) \tag{12.165}
\end{equation*}
$$

where

$$
\begin{equation*}
r_{D S i}=\frac{1}{\mu_{n} C_{o x}\left(\frac{W}{L}\right)_{i}\left(V_{c}-V_{x}-V_{t n}\right)} \tag{12.166}
\end{equation*}
$$

image_name:(a)
description:
[
name: G1, type: Resistor, value: G1, ports: {N1: Vi, N2: A1_InN}
name: G2, type: Resistor, value: G2, ports: {N1: V1, N2: A2_InN}
name: G3, type: Resistor, value: -G3, ports: {N1: A1_Out, N2: A2_InN}
name: G4, type: Resistor, value: G4, ports: {N1: InN(A1), N2: Vo}
name: G5, type: Resistor, value: G5, ports: {N1: InN(A2), N2: Vo}
name: CA, type: Capacitor, value: CA, ports: {Np: A1_Out, Nn: A1_InN}
name: CB, type: Capacitor, value: CB, ports: {Np: A2_Out, Nn: A2_InN}
name: C1, type: Capacitor, value: C1, ports: {Np: Vi, Nn: A2_InN}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: A1_InN, OutP: A1_Out}
name: A2, type: OpAmp, value: A2, ports: {InP: GND, InN: A2_InN, OutP: Vo}
]
extrainfo:This circuit is a second-order active-RC filter with two operational amplifiers, A1 and A2. The resistors G1 to G5 and capacitors CA, CB, and C1 are configured to create a filter that processes the input voltage Vi to produce an output voltage Vo. The circuit allows for tunability by replacing fixed resistors with transistors in triode mode, as mentioned in the context.
image_name:(b)
description:The circuit diagram (b) represents a differential MOSFET-C integrator with two operational amplifiers, providing tunability by using transistors in place of fixed resistors. This design allows for the adjustment of the integrator's characteristics by varying the control voltage, Vc. The circuit is designed to process differential input signals and provide differential output with reduced linearity due to the transistors' characteristics.

Fig. 12.44 (a) A general second-order active-RC half circuit. (b) The equivalent MOSFET-C filter.

Here, note that $\mathrm{V}_{\mathrm{x}}$ is important because it helps to determine the small-signal resistance of the transistors. Tuning can be accomplished by varying the control voltage, $\mathrm{V}_{\mathrm{c}}$.

Key Point: Replacing the fixed resistors of an active $R C$ integrator with transistors in triode provides tunability, but reduces linearity.

So far, we have analyzed the small-signal operation of a MOSFET-C integrator. In this MOSFET-C case, the differential input signals, $\left(\mathrm{v}_{\mathrm{p} 1}, \mathrm{v}_{\mathrm{n} 1}\right)$ and $\left(\mathrm{v}_{\mathrm{p} 2}, \mathrm{v}_{\mathrm{n} 2}\right)$, are assumed to be balanced around a common-mode voltage, $\mathrm{V}_{\mathrm{CM}}$, set by the output common-mode feedback from the previous integrators. The common-mode feedback of the integrator causes the integrator's two outputs to be balanced also. As a result, it can be shown that $\mathrm{V}_{\mathrm{x}}$ is related to the square of the input signal. This nonlinear relationship at $\mathrm{V}_{\mathrm{x}}$ together with the nonlinear current through triode transistors results in quite linear single-ended signals at $\mathrm{V}_{\mathrm{no}}$ and $\mathrm{V}_{\mathrm{po}}$. In addition, since the circuit is fully differential, evenorder distortion products cancel, as depicted in Section 6.7. Thus, two-transistor MOSFET-C integrators can be used to realize filters with around a $50-\mathrm{dB}$ linearity.

An example of a general second-order MOSFET-C filter is shown in Fig. 12.44(b). It is equivalent to the active RC filter half-circuit of Fig. $12.44(a)$, with the terms $\mathrm{G}_{\mathrm{i}}$ representing the small-signal drain-source conductance of the transistors. The transfer function for this filter is the same as its equivalent active-RC half circuit, given by (12.156).

### 12.8.3 Four-Transistor Integrators

One way to improve the linearity of a MOSFET-C filter is to use four-transistor MOSFET-C integrators, as shown in Fig. 12.45 [Czarnul, 1986]. The small-signal analysis of this four-transistor integrator can be found by treating this one-input integrator as effectively a two-input integrator in which the two input signals are $\left(\mathrm{v}_{\mathrm{pi}}-\mathrm{v}_{\mathrm{ni}}\right)$ and the inverted signal is $\left(\mathrm{v}_{\mathrm{ni}}-\mathrm{v}_{\mathrm{pi}}\right)$. With such an observation, and applying (12.165), the output signal is given by

$$
\begin{equation*}
\mathrm{v}_{\mathrm{diff}}=\frac{1}{\mathrm{sr}_{\mathrm{DS} 1} \mathrm{C}_{\mathrm{I}}}\left(\mathrm{v}_{\mathrm{pi}}-\mathrm{v}_{\mathrm{ni}}\right)+\frac{1}{\mathrm{sr}_{\mathrm{DS} 2} \mathrm{C}_{\mathrm{I}}}\left(\mathrm{v}_{\mathrm{ni}}-\mathrm{v}_{\mathrm{pi}}\right) \tag{12.167}
\end{equation*}
$$

where

$$
\begin{equation*}
\mathrm{r}_{\mathrm{DS} 1}=\frac{1}{\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)_{1}\left(\mathrm{~V}_{\mathrm{C} 1}-\mathrm{V}_{\mathrm{x}}-\mathrm{V}_{\mathrm{t}}\right)} \tag{12.168}
\end{equation*}
$$

and

$$
\begin{equation*}
r_{D S 2}=\frac{1}{\mu_{n} C_{o x}\left(\frac{W}{L}\right)_{2}\left(V_{C 2}-V_{x}-V_{t}\right)} \tag{12.169}
\end{equation*}
$$

In the case where all four transistors are matched, we can combine the preceding equations to obtain

$$
\begin{equation*}
\mathrm{v}_{\mathrm{diff}}=\mathrm{v}_{\mathrm{po}}-\mathrm{v}_{\mathrm{no}}=\frac{1}{\mathrm{sr}_{\mathrm{DS}} \mathrm{C}_{\mathrm{I}}}\left(\mathrm{v}_{\mathrm{pi}}-\mathrm{v}_{\mathrm{ni}}\right) \tag{12.170}
\end{equation*}
$$

where $r_{D S}$ is given by

$$
\begin{equation*}
\mathrm{r}_{\mathrm{DS}}=\frac{1}{\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)\left(\mathrm{V}_{\mathrm{C} 1}-\mathrm{V}_{\mathrm{C} 2}\right)} \tag{12.171}
\end{equation*}
$$

Thus, we see that the effective resistance is determined by the difference in the control voltages.
With regard to the distortion properties of this integrator, it has been shown for long channel-length transistors that the drain-source current in a triode transistor is reasonably well modelled by an equation in which the nonlinear distortion terms do not depend on the controlling gate voltage. In other words, although the linear term of each drain
image_name:Fig. 12.45
description:The circuit is a single-input four-transistor MOSFET-C integrator that can cancel both even and odd distortion products if the nonlinear terms are not dependent on the control signals VC1 and VC2. All transistors are matched.

Fig. 12.45 A single-input four-transistor MOSFET-C integrator. It can cancel both even and odd distortion products if the nonlinear terms are not dependent on the control signals, $\mathrm{V}_{\mathrm{C} 1}$ and $\mathrm{V}_{\mathrm{C} 2}$.
current is set by the controlling gate voltage, all distortion terms of the drain currents remain equal in the pair $\mathrm{Q}_{\mathrm{p} 1}, \mathrm{Q}_{\mathrm{p} 2}$ as well as in the pair, $\mathrm{Q}_{\mathrm{n} 1}, \mathrm{Q}_{\mathrm{n} 2}$ since, within each pair, the drain-source voltages are equal. As a result of the cross-coupling connection, both the even and odd distortion terms cancel. Unfortunately, this model does not hold as well for short-channel devices, and transistor mismatch also limits the achievable distortion performance. Hence, in practice, one might expect around a $10-\mathrm{dB}$ linearity improvement using this technique over the two-transistor MOSFET-C integrator.

### 12.8.4 R-MOSFET-C Filters

Another technique intended to improve the linearity of MOSFET-C filters is the use of additional linear resistors [Moon, 1993]. An R-MOSFET-C first-order filter and its MOSFET-C counterpart are shown in Fig. 12.46. Using the equivalent active-RC half circuit, shown in Fig. 12.46(c), one finds the transfer function of this first-order R-MOSFET-C filter to be given by

$$
\begin{equation*}
\frac{v_{0}(s)}{v_{i}(s)}=-\frac{R_{2} / R_{1}}{s C_{1}\left[R_{2}\left(1+\frac{R_{Q_{1}}}{R_{1}\left\|R_{2}\right\| R_{Q_{2}}}\right)\right]+1} \tag{12.172}
\end{equation*}
$$

Key Point: Adding fixed passive series resistors to active MOSFET-C filters can improve their linearity.
where $R_{Q 1}$ and $R_{Q 2}$ represent the small-signal drain-source resistances of $Q_{1}$ and $\mathrm{Q}_{2}$, respectively. Note that the dc gain of this first-order filter is not adjustable. However, it can be set precisely since it is determined by the ratio of two resistors. In addition, the time constant can vary from a minimum value of $R_{2} C_{I}$ to an arbitrarily large value by changing the values of $R_{Q_{1}}$ and $R_{Q 2}$ via the control voltages, $\mathrm{V}_{\mathrm{C} 1}$ and $\mathrm{V}_{\mathrm{C} 2}$. What this transfer function equation indicates is that at low frequencies, the feedback around $R_{2}$ forces node $v_{x}$ to act as a virtual ground, and therefore excellent linearity is obtained since the circuit is essentially a resistor-only circuit. In [Moon, 1993], a linearity of approximately -90 dB is observed with input signals in the range of a few kilohertz. At higher frequencies, the linearity steadily decreases, and measured results of -70 dB are reported at the passband edge of a fifth-order Bessel filter (the passband is around 20 kHz ). However, it should be noted that the measured values are total-harmonic-distortion values, and no intermodulation results are reported.

One other approach that has been used to realize high-linearity continuous-time filters is simply to realize differential active-RC filters, but to realize the capacitors using digitally programmable capacitor arrays. For example, [Durham, 1993] describes a filter intended for digital-audio interfaces that achieves distortion products at a -94-dB and a $95-\mathrm{dB}$ signal-to-noise ratio.

## 12.9 TUNING CIRCUITRY

Key Point: Analog filter time constants, determined by $\mathrm{G}_{\mathrm{m}} / \mathrm{C}$ or RC products, vary considerably over process and temperature. Hence, tuning is required to ensure accurate and repeatable frequency responses.

As mentioned at the beginning of this chapter, one disadvantage of continuoustime integrated filters is the requirement of additional tuning circuitry. This requirement is a result of large time-constant fluctuations due mainly to process variations. For example, integrated capacitors might have 10 percent variations, whereas resistors or transconductance values might have around 20 percent variations. Since these elements are constructed quite differently, the resulting RC or $\mathrm{G}_{\mathrm{m}} / \mathrm{C}$ time-constant products are accurate to only around 30 percent with these process variations. In addition, temperature variations further aggravate the situation because resistance and transconductance values change substantially
image_name:(a)(b)
description:This circuit is a first-order MOSFET-C filter. It uses NMOS transistors and capacitors to form a filter network, with an operational amplifier providing gain and feedback. The circuit is designed to process an input signal Vi and produce an output Vo, with tuning achieved through the control of the NMOS gate voltages.

image_name:(c)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vi, N2: Vx}
name: RQ1, type: Resistor, value: RQ1, ports: {N1: Vx, N2: InN(A1)}
name: RQ2, type: Resistor, value: RQ2, ports: {N1: Vx, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vx, N2: Vo}
name: CI, type: Capacitor, value: CI, ports: {Np: InN(A1), Nn: Vo}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Vo}
]
extrainfo:This circuit is a first-order MOSFET-C filter using NMOS transistors and capacitors. It processes an input signal Vi and produces an output Vo, with tuning achieved through the control of the NMOS gate voltages.

$$
\frac{v_{0}(s)}{v_{i}(s)}=-\frac{R_{2} / R_{1}}{s C_{I}\left[R_{2}\left(1+\frac{R_{Q 1}}{R_{1}\left\|R_{2}\right\| R_{Q 2}}\right)\right]+1}
$$

Fig. 12.46 (a) A first-order MOSFET-C filter. (b) A first-order R-MOSFET-C filter. (c) Equivalent active-RC half-circuit for R-MOSFET-C filter.
over temperature. Thus, we need tuning circuitry to modify transconductance values such that the resulting overall time constants are set to known values. It should be noted, however, that although absolute component tolerances are high, relative accuracies can be quite good. Specifically, the ratio of two capacitors (or two resistors, or two transistors) can be matched to under 1 percent. This section discusses some techniques to realize tuning circuitry for integrated continuous-time filters. Note that, although the tuning approaches are discussed while we refer to $\mathrm{G}_{\mathrm{m}}-\mathrm{C}$ (transconductance-C) filters, the concepts are easily extended to other integrated continuous-time filters, such as MOSFET-C filters.

### 12.9.1 Tuning Overview

Consider once again the $G_{m}-C$ continuous-time biquad filter shown in Fig. 12.10. Its transfer function, repeated here for convenience, is given by

$$
\begin{equation*}
H(s)=\frac{s^{2}\left[\frac{C K_{x}}{C_{x}+C_{B}}\right]+s\left[\frac{G_{m 5}}{C_{X}+C_{B}}\right]+\left(\frac{G_{m 2} G_{m 4}}{\left[C_{A}\left(C_{x}+C_{B}\right)\right]}\right)}{s^{2}+s\left[\frac{G_{m 3}}{C_{x}+C_{B}}\right]+\left(\frac{G_{m 1} G_{m 2}}{\left[C_{A}\left(C_{X}+C_{B}\right)\right]}\right)} \tag{12.173}
\end{equation*}
$$

image_name:Fig. 12.47 Indirect frequency tuning
description:The system block diagram labeled "Fig. 12.47 Indirect frequency tuning" illustrates a continuous-time filter system based on transconductance and capacitance (Gm-C filter). The main components and their functions are as follows:

1. **Transconductance-C Filter:**
- This is the central block of the diagram, which consists of multiple transconductors arranged in sequence. These are depicted as operational amplifier symbols with transconductance functionality. The transconductors work together with capacitors to form a biquad filter structure.
- **Function:** The transconductance-C filter processes the input signal (V_in) to produce a filtered output signal (V_out). The filter's behavior, including its frequency response, is influenced by the transconductance values and the capacitances within this block.

2. **Extra Transconductor Plus Tuning Circuitry:**
- This block is responsible for adjusting the frequency characteristics of the transconductance-C filter. It includes an additional transconductor and associated tuning circuitry.
- **Function:** It provides a control voltage (V_cntl) that tunes the filter's characteristics, such as its cutoff frequency or Q-factor. This tuning is achieved by varying the transconductance or other parameters within the filter.

3. **Flow of Information:**
- The input signal (V_in) enters the transconductance-C filter block, where it is processed by the series of transconductors and capacitors.
- The output signal (V_out) exits the filter block after processing.
- The extra transconductor and tuning circuitry generate a control signal (V_cntl) that feeds back into the transconductance-C filter. This feedback loop allows for dynamic adjustment of the filter’s properties.

4. **Overall System Function:**
- The system functions as a tunable continuous-time filter. The indirect frequency tuning mechanism allows for precise control over the filter characteristics by adjusting the control voltage (V_cntl). This setup is particularly useful in applications requiring adaptable filtering, such as signal processing in communication systems, where maintaining specific frequency responses is crucial despite variations in component values.

Fig. 12.47 Indirect frequency tuning. Note that, although the tuning signal is shown here as a voltage signal, it may also be realized using a set of current controlling signals.

Although the transconductances, $\mathrm{G}_{\mathrm{mi}}$, have large variations in their absolute values, relative transconductance values can also be set reasonably accurately. For example, if the transconductors are realized as bipolar differential pairs with an emitter degeneration resistor (as shown in Fig. 12.12), then the relative transconductance values of two transconductors is set by the ratio of their respective emitter degeneration resistors (assuming the gain-cell currents are equal in the two transconductors). Similarly, if other transconductors of the same type are used, their relative $G_{m}$ values can be accurately set by choosing appropriate transistor sizes, bias currents, or resistor values (or some combination of the three). As a result, we can write all the transconductance values, $\mathrm{G}_{\mathrm{mi}}$, as an accurate constant multiplied by some basic transconductance value. Specifically, let us write all the transconductance values, $G_{m i}$, as a function of $G_{m 1}$, resulting in

$$
\begin{equation*}
G_{m i}=k_{m i} G_{m 1} \tag{12.174}
\end{equation*}
$$

Here, the constants, $\mathrm{k}_{\mathrm{mi}}$, are set reasonably accurately by appropriate transistor, resistor, or bias-current scaling. Furthermore, let us also write

$$
\begin{equation*}
C_{X}+C_{B}=k_{X B} C_{A} \tag{12.175}
\end{equation*}
$$

where $k_{X B}$ is a constant that is accurately set as the ratio of capacitance values. Similarly, let $k_{X}=C_{X} / C_{A}$. With such an approach, (12.173) becomes

$$
\begin{equation*}
H(s)=\frac{s^{2}\left[\frac{k_{x}}{k_{x B}}\right]+s\left(\frac{k_{m 5}}{k_{X B}}\right)\left(\frac{G_{m 1}}{C_{A}}\right)+\left(\frac{k_{m 2} k_{m 4}}{k_{X B}}\right)\left(\frac{G_{m 1}}{C_{A}}\right)^{2}}{s^{2}+s\left(\frac{k_{m 3}}{k_{x B}}\right)\left(\frac{G_{m 1}}{C_{A}}\right)+\left(\frac{k_{m 1} k_{m 2}}{k_{x B}}\right)\left(\frac{G_{m 1}}{C_{A}}\right)^{2}} \tag{12.176}
\end{equation*}
$$

We see from (12.176) that the coefficients for this second-order filter can be accurately set if only one ratio is tuned-that of $G_{m 1} / C_{A}$. Since it is difficult to tune $C_{A}$, the ratio $G_{m 1} / C_{A}$ is tuned by changing $G_{m 1}$. Of course, as $G_{m 1}$ is varied, all the other transconductance values, $G_{m i}$, are also changed since their values must track that of $\mathrm{G}_{\mathrm{m} 1}$ by their respective constants, $\mathrm{k}_{\mathrm{m}}$. It should be mentioned here that this same single transconductance tuning is also valid for higher-order filter structures.

In summary, the most common way to tune a continuous-time integrated filter is to build an extra transconductor that is tuned (tuning details are discussed next) and to use the resulting tuning signal to control the filter transconductors, as shown in Fig. 12.47. Such an approach is commonly referred to as indirect frequency tuning. This tuning is indirect since one relies on matching between the filter transconductors (and parasitic capacitances) and the extra transconductor. In other words, the filter is not directly tuned by looking at its output signal. Frequency tuning refers to the fact that the ratio $G_{m 1} / C_{A}$ is equal to the unity-gain frequency of a $G_{m}-C$ integrator. ( $\mathrm{G}_{\mathrm{m} 1} / \mathrm{C}_{\mathrm{A}}$ is also proportional to the pole frequency, $\omega_{0}$, in a first- or second-order filter.)

Unfortunately, this frequency-tuning approach may not be sufficient in some applications due to nonideal integrators or mismatch effects. In these applications, some extra tuning circuitry known as Q-factor tuning (discussed later in this section) can be used. It is also possible to implement direct tuning where the filter is tuned by directly looking at the filter's output. Two such direct approaches are also discussed in this section.

### 12.9.2 Constant Transconductance

As just discussed, if no tuning is performed, one might expect around a 30-percent tolerance on the absolute value for the $\mathrm{G}_{\mathrm{m}} / \mathrm{C}$ ratio. However, integrated capacitance tolerance typically accounts for only a 10 -percent variation in the overall 30-percent tolerance. Thus, in applications where a 10-percent variation can be permitted (such as an anti-aliasing filter with a sample rate moderately higher than the Nyquist rate), it is sufficient to set only the $\mathrm{G}_{\mathrm{m}}$ value with the use of a fixed external resistor. As we will see below, such tuning of a $G_{m}$ value is not difficult and does not require any clock signals.

In the case where 10-percent accuracy is not enough, clearly one must also account for capacitor tolerance. One way to do so (while still not needing a clock signal) is to have a variety of external resistors available and choose the most appropriate one to also account for capacitor tolerance. With such an approach, one might expect that the overall $G_{m} / C$ ratio would be accurate to under 1 percent. Although a variety of methods exist for choosing this external resistance, one way is to use a known value of external resistance and measure the step response of the filter during system production. This step-response result can then be used to determine the C value, and hence the proper resistance value can be calculated. Finally, since integrated capacitors typically have small temperature coefficients, overall temperature effects are small if the external resistor is also chosen to have a low temperature coefficient.

To set a transconductance value equal to the inverse of an external resistance, (i.e., $G_{m}=1 / R_{\text {ext }}$ ), a variety of feedback circuits can be used. Two example circuits are shown in Fig. 12.48, where it should be noted that, in both cases, it is assumed the transconductor's transconductance increases as the level of the control signal is increased. In Fig. 12.48(a), if $\mathrm{G}_{\mathrm{m}}$ is too small, the current through $\mathrm{R}_{\text {ext }}$ is larger than the current supplied by the transconductor, and the difference between these two currents is integrated with the opamp and capacitor. As a result, the control voltage, $\mathrm{V}_{\text {cntt }}$, is increased until these two currents are equal (but opposite in direction) and, therefore, $\mathrm{G}_{\mathrm{m}}=1 / \mathrm{R}_{\text {ext }}$. The circuit in Fig. 12.48(b) shows two voltage-to-current converters-one is the transconductor being tuned, and the other is a fixed voltage-to-current converter that simply needs a large transconductance and is
image_name:(a)
description:The circuit diagram (a) shows a voltage-controlled transconductor (Gm) being tuned. It consists of a voltage source VB, a resistor Rext, a capacitor CI, and a voltage-controlled current source Gm. The control voltage Vcntl is used to adjust the transconductance of Gm. The goal is to achieve a constant transconductance by tuning Gm such that Gm = 1/Rext.
image_name:(b)
description:The circuit is a constant transconductance tuning circuit. It uses a voltage-controlled transconductor (Gm) and a fixed voltage-to-current converter (V/I) to control the current Icntl. The circuit is designed to ensure that Gm equals 1/Rext, maintaining a constant transconductance.

(For both circuits)

$$
\begin{equation*}
G_{m}=\frac{1}{R_{e x t}} \tag{b}
\end{equation*}
$$

Fig. 12.48 Constant transconductance tuning. Possible tuning circuits if the transconductors are (a) voltage controlled or (b) current controlled. In both circuits, it is assumed the transconductor's transconductance increases as the level of the control signal increases. $\mathrm{V}_{\mathrm{B}}$ is an arbitrary voltage level, whereas $C_{I}$ is an integrating capacitor used to maintain loop stability.
not necessarily linear. (It might be implemented as a simple differential pair.) This circuit operates as follows: If $G_{m}$ is too small, then the voltage at the top of $R_{\text {ext }}$ will be less than $V_{B}$ and the fixed $V / I$ converter will increase $I_{\text {cntl }}$. At steady state, the differential voltage into the fixed V/I converter will be zero, resulting in $G_{m}=1 / R_{\text {ext }}$.

### 12.9.3 Frequency Tuning

A precise tuning of a $G_{m} / C_{A}$ ratio can be achieved if an accurate time period is available. For example, assuming one has available an accurate clock frequency, say, $\mathrm{f}_{\mathrm{clk}}$, then one method of frequency tuning is by using a switchcapacitor circuit as shown in Fig. 12.49 [Viswanathan, 1982]. Here, the tuning circuit is quite similar to the constant-transconductance approaches of Fig. 12.48, except that the external resistance is replaced with a switched-capacitor equivalent resistance. From Chapter 14, the equivalence resistance of the switched-capacitor circuit is given by $R_{e q}=1 /\left(f_{c l k} C_{m}\right)$, and therefore the transconductance value, $G_{m}$, is set to $f_{c l k} C_{m}$. In this way, the $G_{m} / C_{A}$ ratio is accurately set to $\left(f_{c \mid k} C_{m}\right) / C_{A}$, and hence precise frequency tuning can be achieved without any external components. Note that an additional low-pass filter, $\mathrm{R}_{1} \mathrm{C}_{1}$, has been added here to remove the highfrequency ripple voltage due to using a switched-capacitor circuit. It should also be noted that, since this method requires a clock signal, there is a strong possibility that some of the clock signal will leak into the continuous-time filter, either mainly through the transconductor controlling signal or through the IC substrate.

One difficulty with this switched-capacitor tuning approach is that it requires large transconductance ratios (and hence poorer matching) if high-frequency filters are desired. For example, consider the case of a $100-\mathrm{MHz}$ filter, where the $G_{m} / C_{A}$ ratio should be set to around $2 \pi \times 100 \mathrm{MHz}$. If a capacitance value, $C_{A}$, is assumed to be 1 pF , then $\mathrm{G}_{\mathrm{m}}=2 \pi \times 10^{-4} \mathrm{~V} / \mathrm{A}$. Thus, in the tuning circuit of Fig. 12.49 , assuming that $\mathrm{C}_{\mathrm{m}}=1 \mathrm{pF}$, we would require the switched-capacitor circuit to be clocked at the impractical frequency of

$$
\begin{equation*}
\mathrm{f}_{\mathrm{clk}}=\frac{\mathrm{G}_{\mathrm{m}}}{\mathrm{C}_{\mathrm{m}}}=\frac{2 \pi \times 10^{-4}}{1 \times 10^{-12}}=628 \mathrm{MHz} \tag{12.177}
\end{equation*}
$$

At first glance, one might consider reducing this clock frequency by increasing the value of $C_{m}$, but, although $f_{c k}$ is reduced, settling-time requirements remain difficult since the capacitance, $C_{m}$, is larger. Another way to reduce $f_{c l k}$ is to let the tuning circuit set a smaller transconductance value, say, $0.1 \mathrm{G}_{\mathrm{m}}$. In this way, $\mathrm{f}_{\mathrm{cl}}$ is reduced by ten but the filter's transconductors must be 10 times greater than the tuning circuitry's transconductor. Thus, poorer matching occurs between the filter and the tuning circuitry, resulting in a less accurate frequency setting for the filter.

Another approach to lower the clock frequency of this switched-capacitor tuning circuitry is by using two scaled current sources, as shown in Fig. 12.50 [SilvaMartinez, 1992]. Using an equivalent resistance of
image_name:Fig. 12.49
description:The circuit is a frequency-tuning circuit using a switched-capacitor transconductor. The transconductance Gm is set by the switched-capacitor circuit, with a clock frequency f_clk. The low-pass filter R1C1 is used to reduce high-frequency ripple voltage. The equation Gm = f_clk * Cm describes the relationship between the transconductance and the clock frequency.

Fig. 12.49 A frequency-funing circuit where $G_{m}$ is set by a switched-capacitor circuit. The switched-capacitor branch has a clock frequency of $f_{c l k}$. The low-pass filter, $R_{1} C_{1}$, is set to a frequency low enough to reduce the high-frequency ripple voltage.
image_name:Fig. 12.50
description:The circuit is a frequency-tuning circuit using a switched-capacitor network. The transconductance Gm is set by the equation Gm = Nf_clkCm, where Cm is the capacitance and f_clk is the clock frequency. The low-pass filter is used to reduce high-frequency ripple voltage.

Fig. 12.50 A switched-capacitor frequency-tuning circuit that operates at a lower clock frequency.
$-1 / \mathrm{f}_{\mathrm{ck}} \mathrm{C}_{\mathrm{m}}$ for the switched-capacitance circuit, and noting that the diode-connected transconductor is equivalent to a resistor of value $1 / \mathrm{G}_{\mathrm{m}}$, one can show that when the average current into the integrator is zero, the transconductance value is given by

$$
\begin{equation*}
\mathrm{G}_{\mathrm{m}}=N \mathrm{f}_{\mathrm{clk}} \mathrm{C}_{\mathrm{m}} \tag{12.178}
\end{equation*}
$$

Thus, the clock frequency of this circuit is N times lower than that for the circuit shown in 15.47. This circuit was used to tune a $10.7-\mathrm{MHz}$ bandpass filter, where a value of $\mathrm{N}=148$ was used, resulting in a clock frequency of only 450 kHz . The low-pass filter was also realized by using a switched-capacitor circuit and an off-chip capacitor.

Another approach to achieving frequency tuning is to use a phase-locked loop (PLL) (described in Chapter 19) as shown in Fig. 12.51 [Tan, 1978]. Here, two continuous-time integrators are placed in a loop to realize a voltage-controlled oscillator that is placed into a phase-locked loop. After the circuit is powered up, the negative feedback of the PLL causes the VCO frequency and phase to lock to the external reference clock. Once the VCO output is locked to an external reference signal, the $\mathrm{G}_{\mathrm{m}} / \mathrm{C}$ ratio of the VCO is set to a desired value, and the control voltage, $\mathrm{V}_{\text {cntt }}$, can be used to tune the integrated filter. It should be noted that choosing the external reference clock is a trade-off because it affects both the tuning accuracy as well as the tuning signal leak into the main filter. Specifically, for best matching between the tuning circuitry and the main filter, it is best to choose the reference frequency that is equal to the filter's upper passband edge. However, noise gains for the main filter are typically the largest at the filter's upper passband edge, and therefore the reference-signal leak into the main filter's output might be too severe. As one moves away from the upper passband edge, the matching will be poorer, but an improved immunity to the reference signal results. Another problem with this approach is that, unless some kind of power-supply-insensitive voltage control is added to the VCO, any power-supply noise will inject jitter into the control signal, $\mathrm{V}_{\mathrm{cnt1}}$. The addition of amplitude control is quite complicated. For a good discussion of this phase-locked-loop approach, see [Krummenacher, 1988; Khoury, 1991]. For a better understanding of the operation of a phase-locked loop, see Chapter 19.
image_name:Fig. 12.51 Frequency tuning using a phase-locked loop
description:The system block diagram in Fig. 12.51 illustrates a phase-locked loop (PLL) used for frequency tuning. This PLL comprises three main components: a phase detector, a low-pass filter, and a voltage-controlled oscillator (VCO).

1. **Main Components:**
- **Phase Detector:** This block receives two inputs: an external reference clock and the feedback signal from the VCO. It compares the phase of these two signals and produces an error signal proportional to the phase difference.
- **Low-pass Filter:** The output of the phase detector is fed into a low-pass filter. This filter smooths the error signal by removing high-frequency noise, producing a clean control voltage.
- **Voltage-Controlled Oscillator (VCO):** The filtered control voltage is used to adjust the frequency of the VCO. The VCO generates an output signal whose frequency is proportional to the input control voltage.

2. **Flow of Information or Control:**
- The system begins with the external reference clock, which is input to the phase detector.
- The phase detector outputs an error signal based on the phase difference between the reference clock and the VCO feedback.
- This error signal is processed by the low-pass filter to produce a smooth control voltage, denoted as $V_{cnt1}$.
- The control voltage adjusts the frequency of the VCO, which outputs a signal back to the phase detector, completing the feedback loop.

3. **Labels, Annotations, and Key Indicators:**
- The diagram labels the external reference clock input and the control voltage output ($V_{cnt1}$).
- The feedback loop is clearly indicated, showing the continuous adjustment of the VCO frequency based on the control voltage.

4. **Overall System Function:**
- The primary function of this PLL is to synchronize the VCO's frequency with the external reference clock. The phase detector compares the phases, the low-pass filter smooths the resulting error signal, and the VCO adjusts its frequency accordingly. This configuration ensures that the VCO remains locked to the reference frequency, minimizing phase error and frequency deviation.

Fig. 12.51 Frequency tuning using a phase-locked loop. The VCO is realized by using transconductor-based integrators that are tuned to adjust the VCO's frequency.
image_name:Fig. 12.51 Frequency tuning using a phase-locked loop
description:The system block diagram in Fig. 12.51 illustrates a frequency tuning mechanism using a phase-locked loop (PLL). The main components involved in this configuration are:

1. **External Reference Clock**: This serves as the input signal to the system, providing a stable frequency reference.

2. **Low-pass Filter**: The external reference clock signal is fed into a low-pass filter. This filter smooths the signal, removing high-frequency noise and allowing only the low-frequency components to pass through. The output of this filter is labeled as a control voltage, \( V_{cntrl} \), which is used to adjust the subsequent components.

3. **Multiplier (Mixer)**: The filtered signal is then fed into a multiplier (or mixer), where it is combined with another signal path. This multiplication process is crucial for phase detection and error signal generation.

4. **Integrator**: Following the multiplier, the signal is passed through an integrator. The integrator accumulates the signal over time, effectively acting as a frequency control element that adjusts the oscillator frequency based on the input signal.

5. **Feedback Loop**: The output of the integrator is fed back into the low-pass filter, creating a feedback loop that is essential for maintaining the lock between the VCO's frequency and the reference clock. This loop helps in continuously adjusting the VCO to minimize phase error and frequency deviation.

6. **Output to Other Filters**: The final output of the integrator is directed "to other filters," indicating that the tuned frequency signal is used to control or drive additional filtering stages in the system.

**Overall System Function**: The primary function of this PLL-based system is to synchronize the voltage-controlled oscillator (VCO) frequency with the external reference clock. The low-pass filter smooths the error signal, and the integrator adjusts the VCO frequency to maintain phase alignment with the reference clock. This ensures that the VCO remains locked to the reference frequency, minimizing phase error and frequency deviation, thereby achieving accurate frequency tuning.

Fig. 12.52 Using a tracking filter to derive a control signal for tuning continuous-time filters.

Another, somewhat similar, approach that has been used is based on having a tracking filter that locks onto a fixed-frequency input [Khorramabadi, 1984]. This approach is reported to be less sensitive to power-supply noise. The control voltage for the tracking filter is used to adjust the transconductors that are used in the actual system, assuming the transconductors in the tracking filter match the transconductors in the actual system. An example calibration system is shown in Fig. 12.52. When the low-pass filter has the same resonant frequency as the external reference clock, it has exactly a 90 -degree phase shift. Therefore, the correlation between its input and output is zero. If the frequencies are not the same, then the correlation, as obtained by the multiplier and integrator, is nonzero. The negative feedback from the output of the integrator to the frequency-control voltage of the filter drives the resonant frequency in the proper direction to equalize the two frequencies. After lock is obtained, the same control voltage can be used for other filters. The other filters will be tuned to known time constants, assuming they match the filter in the control loop.

It is important that the integrator in the loop have a very low-frequency time constant in order to filter out the component at twice the external reference frequency that is present at the output of the multiplier. Otherwise, this component can cause clock leakage into the other filters being tuned. A variant on this scheme drives the correlation between a notch output and a low-pass filter output (obtained from the same biquad) to zero when one is obtaining the control voltage [Kwan, 1991]. This latter method has much fewer signal components at twice the frequency of the external reference clock and does not require as large a time constant for the integrator in the loop. This makes the latter method more readily integrable without external components. Also, the loop is less sensitive to phase errors; it will always converge to the notch frequency, even when the difference in phase between the low-pass and notch outputs is not exactly $90^{\circ}$.

### 12.9.4 Q-Factor Tuning

In some applications, such as high-speed or highly-selective filtering, nonideal integrator effects and parasitic components force the need to also tune the Q-factors of the poles of the integrated filter. Although we have seen that tuning a single time constant can set all coefficients of an integrated filter with around $1 \%$ accuracy, when $\mathrm{Q}>1$, even small errors in the Q -factor can result in large errors in the filter frequency and step response. Hence, in some applications additional tuning is needed to precisely set the Q -factors.

One way to perform Q-factor tuning is to tune the phase of the filter's integrators to ensure that they all have a 90-degree phase lag near the filter's passband edge. An integrator's phase response can be adjusted by introducing a tunable resistance (say, realized as a transistor in triode) in series with the integrating capacitor. The control voltage for this tunable resistance, $\mathrm{V}_{\mathrm{Q}}$, is generated by a Q -factor tuning circuit, shown in Fig. 12.53, and passed to all the filter integrators.

Alternatively, in the case where the integrated filter is second order, the pole Q can be adjusted by changing the transconductance of the damping transconductor in the filter. Specifically, referring back to (12.176) and equating the denominator to a second-order denominator written in the form of $\omega_{0}$ and $Q$, we have

$$
\begin{equation*}
s^{2}+s\left(\frac{k_{m 3}}{k_{X B}}\right)\left(\frac{G_{m 1}}{C_{A}}\right)+\left(\frac{k_{m 1} k_{m 2}}{k_{X B}}\right)\left(\frac{G_{m 1}}{C_{A}}\right)^{2}=s^{2}+s\left(\frac{\omega_{o}}{Q}\right)+\omega_{o}^{2} \tag{12.179}
\end{equation*}
$$

image_name:Fig. 12.53
description:The system block diagram labeled "Fig. 12.53" represents a magnitude-locked loop designed for Q-factor tuning. This loop primarily consists of several interconnected components that collaborate to maintain a specific Q-factor in a filter system.

1. **Main Components:**
- **Q-reference Circuit:** This block is central to the system and is responsible for generating a reference signal that corresponds to the desired Q-factor. It is frequency-tuned via a control voltage, \( V_{cntl} \).
- **Peak Detector (Two Instances):** There are two peak detectors in the system. The first one is connected directly to the output of the Q-reference circuit, and the second one is connected to the reference frequency input.
- **Gain Block (K):** This block amplifies the signal from the second peak detector before it is fed into the summing amplifier.
- **Summing Amplifier:** This component receives inputs from the two peak detectors (one via the gain block) and computes the difference, effectively comparing the magnitudes of the signals.
- **Low-pass Filter:** It processes the output of the summing amplifier to smooth out the signal, providing a stable output voltage, \( V_Q \), which is fed back into the Q-reference circuit.

2. **Flow of Information or Control:**
- The reference frequency, \( V_R \cos(\omega_R t) \), is input into the system and split between the Q-reference circuit and the second peak detector.
- The Q-reference circuit processes this reference frequency, influenced by the control voltage \( V_{cntl} \), and outputs \( V_Q \).
- This output is then fed into the first peak detector, which measures its magnitude.
- The second peak detector measures the magnitude of the reference frequency.
- The outputs from both peak detectors are sent to the summing amplifier, where the second peak detector's output is first amplified by the gain block (K).
- The summing amplifier calculates the difference between these magnitudes and sends the result to the low-pass filter.
- The low-pass filter then outputs a smoothed signal, \( V_Q \), which is fed back into the Q-reference circuit as part of a feedback loop.

3. **Labels, Annotations, and Key Indicators:**
- The diagram is annotated with labels such as \( V_Q \) and \( V_{cntl} \), indicating the flow of signals and control within the system.
- The gain block is marked as "Gain K," emphasizing its role in amplifying the signal.

4. **Overall System Function:**
- The primary function of this system is to tune and stabilize the Q-factor of a filter. It achieves this by comparing the magnitude of the output from the Q-reference circuit with the magnitude of a reference frequency. The feedback loop, facilitated by the low-pass filter, ensures that the Q-factor remains locked to the desired value by adjusting \( V_{cntl} \) based on the difference calculated by the summing amplifier. This arrangement allows for precise control of the filter's Q-factor through continuous monitoring and adjustment.

Fig. 12.53 A magnitude-locked loop for Q-factor tuning. The Q-reference circuit is typically a second-order filter that is frequency tuned through the use of $\mathrm{V}_{\text {cntt }}$.

Solving, we find the following relationships:

$$
\begin{align*}
\omega_{o} & =\left(\frac{G_{m 1}}{C_{A}}\right) \sqrt{\frac{k_{m 1} k_{m}}{k_{X B}}}  \tag{12.180}\\
Q & =\left(\frac{k_{x B}}{k_{m 3}}\right) \sqrt{\frac{k_{m 1} k_{m} 2}{k_{x B}}} \tag{12.181}
\end{align*}
$$

From this $Q$ relationship, we see that the $Q$ factor of the filter's poles is inversely proportional to $k_{m 3}$, and hence one need only tune $G_{m 3}$ to adjust the Q factor of this second-order filter.

The control signal, $\mathrm{V}_{\mathrm{Q}}$, for either of the preceding Q -factor tuning approaches can be realized using the mag-nitude-locked loop system shown in Fig. 12.53 [Schaumann, 1990]. The circuit's operation is based on the knowledge that a Q-factor error results in a magnitude error in a filter's frequency response. To measure the magnitude error, a sinusoidal signal of an appropriate reference frequency is applied to a Q-reference circuit, and the magnitude of its output is compared to a scaled version of the input signal's magnitude. This sinusoidal frequency might be obtained as the output of the VCO in the frequency-tuning circuitry.

### 12.9.5 Tuning Methods Based on Adaptive Filtering

Adaptive filters are commonly used in digital-signal-processing applications such as model matching, channel equalization, and noise (or echo) cancellation. It is also possible to use adaptive filter techniques to tune a continuous-time integrated filter to a given specification. One example of such an approach is shown in Fig. 12.54 [Kozma, 1991], where the adaptive tuning circuitry is used to minimize the error signal. During tuning, the input to the tunable filter is a predetermined output from a pseudorandom (PN) 4-bit sequence and a D/A converter. Since the input is known and repetitive, the ideal output from a desired transfer-function can be precalculated (or simulated) and used as a reference signal for the adaptive system. After adaptation, the transfer function of the tunable filter should match that of the desired filter, and, by freezing the coefficients (assuming they are digitally controlled), the tunable filter can be disconnected from the tuning circuit and used in the desired operation. With this approach, it is possible to tune all the poles and zeros of the tunable filter to better match the desired transfer function.

Another adaptive-filter tuning method intended for high-speed data transmission over a twisted-wire pair is shown in Fig. 12.55 [Shoval, 1995]. In this application, the filter input is a data stream of ones and zeros that are represented by the input signal being either high or low. Before transmission, a pulse-shaping filter is required to ensure that not too much high-frequency power is radiated from the twisted-wire channel. The two tuning loops
image_name:Fig. 12.54
description:The system block diagram in Fig. 12.54 illustrates a tuning approach for a tunable filter, where all the poles and zeros can be adjusted to achieve the desired filter response. The main components of the diagram include a 4-bit PN sequence plus DAC, a tunable filter, a 15-level DAC, adaptive tuning circuitry, and a summing junction.

**Main Components:**
1. **4-bit PN Sequence plus DAC:** This block generates a pseudo-random binary sequence, which is converted into an analog signal by the Digital-to-Analog Converter (DAC). This signal serves as the input to the tunable filter.

2. **Tunable Filter:** The core component of the system, this filter receives the input signal from the 4-bit PN sequence plus DAC. Its response is adjusted based on the coefficient signals it receives from the adaptive tuning circuitry.

3. **15-level DAC:** This component provides a reference signal that represents the ideal filter response. It outputs a multi-level analog signal used for comparison with the tunable filter's output.

4. **Summing Junction:** This block calculates the error signal by subtracting the tunable filter's output from the reference signal generated by the 15-level DAC. The error signal is then used to adjust the filter's parameters.

5. **Adaptive Tuning Circuitry:** This block receives the error signal and generates gradient signals to minimize the error. It adjusts the tunable filter's coefficients to align the filter's output with the desired response.

**Flow of Information or Control:**
- The input signal, a series of steps from the 4-bit PN sequence plus DAC, enters the tunable filter.
- The tunable filter's output is compared to the reference signal from the 15-level DAC at the summing junction, producing an error signal.
- The error signal is fed into the adaptive tuning circuitry, which computes gradient signals to fine-tune the filter's coefficients, thereby minimizing the error.
- Coefficient signals from the adaptive tuning circuitry are fed back into the tunable filter to adjust its response.

**Overall System Function:**
The system functions as an adaptive filter tuning mechanism. It continuously adjusts the tunable filter's parameters to minimize the error between the actual filter output and the desired response, represented by the reference signal. This tuning ensures that the filter's step response aligns with the ideal characteristics, optimizing the filter for high-speed data transmission applications.

Fig. 12.54 A tuning approach in which all the poles and zeros of the tunable filter can be adjusted. The 15-level DAC outputs are determined by what the ideal filter response would generate, while the adaptive tuning circuitry minimizes the error signal.
(frequency and Q-factor loops) rely on the fact that the input to the filter is a series of steps (say, $\pm 1 \mathrm{~V}$ ), and thus, in fact, tune the step response of the filter. Specifically, frequency tuning is accomplished by ensuring that the zero crossing of the filter's low-pass output occurs at the correct time period after a data transition. Also, Q-factor tuning is performed by comparing the peak in the filter's bandpass output with a known voltage. Fortunately, the peak in the bandpass output occurs at approximately the same time as the zero crossing, so both detectors can be realized through the use of two clocked comparators, which are triggered at a set time after a data transition. In summary, clever tuning techniques can be implemented when a restricted set of input signals are applied to a tunable filter such as in data communication circuits.
image_name:Fig. 12.55 A tuning method to implement a pulse-shaping filter needed for data communication systems.
description:The system block diagram in Fig. 12.55 illustrates a tuning method for implementing a pulse-shaping filter used in data communication systems. The primary components of the system include a digital data stream input, a second-order filter, digital counters with Digital-to-Analog Converters (DACs), and detection circuits for peak and zero-crossing events.

Main Components:
1. **Digital Data Stream**: This is the input to the system, driven by a clock signal \( f_{clk} \).
2. **Second-Order Filter**: This filter processes the digital data stream and produces two outputs: a bandpass output and a low-pass output. These outputs are used for pulse shaping in data communication.
3. **Digital Counter plus DAC (Q-factor tuning)**: This component is responsible for adjusting the quality factor (Q) of the second-order filter. It receives input from the peak detection block and outputs a control voltage \( V_Q \) to the filter.
4. **Peak Detect**: This block detects the peak in the bandpass output and generates a voltage \( V_{peak} \) used for Q-factor tuning. It operates with a delayed clock signal \( f_{clk}(delay) \).
5. **Digital Counter plus DAC (Frequency tuning)**: Similar to the Q-factor tuning, this component adjusts the frequency of the second-order filter. It receives input from the zero-crossing detection block and outputs a control voltage \( V_{cntl} \) to the filter.
6. **Zero Crossing Detect**: This block detects zero crossings in the bandpass output and provides input to the frequency tuning digital counter. It also uses a delayed clock signal \( f_{clk}(delay) \).

Flow of Information or Control:
- The digital data stream is processed by the second-order filter, producing bandpass and low-pass outputs.
- The bandpass output is monitored by both the peak detect and zero crossing detect blocks.
- The peak detect block sends feedback to the digital counter plus DAC for Q-factor tuning, influencing the filter's quality factor through \( V_Q \).
- The zero crossing detect block sends feedback to the digital counter plus DAC for frequency tuning, influencing the filter's frequency response through \( V_{cntl} \).

Labels, Annotations, and Key Indicators:
- **\( V_{peak} \)**: Voltage representing the detected peak, used in Q-factor tuning.
- **\( V_{cntl} \)**: Control voltage for frequency tuning.
- **Pulse-shaping filter output**: The low-pass output of the second-order filter, which is the final output of the pulse-shaping process.

Overall System Function:
The system functions as a tunable pulse-shaping filter for data communication. It dynamically adjusts the filter's Q-factor and frequency based on the characteristics of the input data stream, optimizing signal processing through feedback loops involving peak and zero-crossing detection. This ensures precise shaping of data pulses, crucial for effective data transmission.

Fig. 12.55 A tuning method to implement a pulse-shaping filter needed for data communication systems.

## 12.10 INTRODUCTION TO COMPLEX FILTERS

This section is based upon the tutorial introduction published in [Martin, 2004] much of which is in turn based upon work published in [Lang, 1981], [Snelgrove, 1981], [Snelgrove, 1982], [Allen, 1985].

### 12.10.1 Complex Signal Processing

A complex signal consists of a pair of real signals at an instant in time. If one denotes the complex signal, $\mathrm{X}(\mathrm{t})$, as $\mathrm{X}(\mathrm{t})=\mathrm{X}_{\mathrm{r}}(\mathrm{t})+\mathrm{j} \mathrm{x}_{\mathrm{q}}(\mathrm{t})$, where $\mathrm{j}=\sqrt{-1}$, then a Hilbert Space can be defined using appropriate definitions for addition, multiplication, and an inner-product and norm. In an actual physical system, the signals are both real (but are called the real and imaginary parts) and are found in two distinct signal paths. The multiplier " j " is used to help define operations between different complex signals, and is to some degree imaginary; i.e., it doesn't actually exist in real systems. Often the dependence of signals on time is not shown explicitly.

The use of complex signal processing to describe wireless systems is increasingly important and ubiquitous for the following reasons: it often allows for image-reject architectures to be described more compactly and simply; it leads to a graphical or signal-flow-graph (SFG) description of signal-processing systems providing insight, and it often leads to the development of new systems where the use of high-frequency highly selective image-reject filters is minimized. The result is more highly integrated systems using less power and requiring less physical space.

As an example, consider the popular "quadrature" mixer with a real input as shown in Fig. 12.56. In the complex SFG, two real multiplications have been replaced by a single complex multiplication. Furthermore, since in the time domain we have

$$
\begin{align*}
Y(t) & =y_{r}(t)+j y_{q}(t)  \tag{12.182}\\
& =X(t) e^{j \omega_{i} t} \\
Y(\omega) & =X\left(\omega-\omega_{i}\right) \tag{12.183}
\end{align*}
$$

then taking the Fourier transform we have
and we see that an ideal quadrature mixer results in a simple frequency-shift of the input signal with no images occurring, a conclusion that is obvious from Fig. 12.56(b), but is certainly not obvious from Fig. 12.56(a). If this mixer is followed by a low-pass filter in each path, then it can be used to directly demodulate carrier-frequency signals without images. For this reason, it often called an image-reject mixer although if one is being accurate, the term should denote the combination of the quadrature mixer and lowpass filters.

Complex signal processing systems operate on ordered pairs of real signals. A possible definition for a complex inner-product is

$$
\begin{equation*}
\left\langle\mathrm{x}_{1}(\mathrm{t}), \mathrm{x}_{2}(\mathrm{t})\right\rangle=\lim _{\mathrm{t} \rightarrow \infty} \frac{1}{2 \mathrm{t}} \int_{-\mathrm{t}}^{\mathrm{t}} \mathrm{x}_{1}(\tau) \mathrm{x}_{2}^{*}(\tau) \mathrm{d} \tau \tag{12.184}
\end{equation*}
$$

image_name:Fig. 12.56
description:The block diagram in Fig. 12.56 represents a quadrature mixer, which is a fundamental component in signal processing used for converting a real signal into its quadrature components. This system involves the following key components:

1. **Input Signal \( x_r(t) \):**
- The input to the system is a real signal denoted by \( x_r(t) \).

2. **Mixers (Multipliers):**
- There are two mixers in the diagram. Each mixer multiplies the input signal \( x_r(t) \) with a different sinusoidal signal.
- **First Mixer:** Multiplies \( x_r(t) \) with \( \cos(\omega_i t) \) to produce the in-phase component \( y_r(t) \).
- **Second Mixer:** Multiplies \( x_r(t) \) with \( \sin(\omega_i t) \) to produce the quadrature component \( y_q(t) \).

3. **Outputs:**
- The outputs of the system are two signals: \( y_r(t) \) and \( y_q(t) \), representing the in-phase and quadrature components, respectively.

4. **Signal Flow:**
- The input signal \( x_r(t) \) is split and fed into both mixers.
- The sinusoidal signals \( \cos(\omega_i t) \) and \( \sin(\omega_i t) \) are used to modulate the input signal, creating two separate paths for the in-phase and quadrature components.

5. **Overall System Function:**
- The primary function of this quadrature mixer is to decompose the real input signal \( x_r(t) \) into two orthogonal components, \( y_r(t) \) and \( y_q(t) \), which are used in various applications such as modulation, demodulation, and signal processing tasks that require phase and amplitude information of a signal.

$$
X(t)=x_{r}(t)+j \times 0
$$

image_name:Y(t)
description:The system block diagram labeled "Y(t)" depicts a fundamental component of a quadrature mixer, specifically a multiplier block. This block is crucial for the decomposition of a real input signal into its orthogonal components.

1. **Main Components:**
- The central component is a multiplier, denoted by the multiplication symbol (×) within a circle. This multiplier is responsible for combining input signals to produce a desired output.

2. **Flow of Information or Control:**
- The diagram shows three incoming arrows pointing towards the multiplier block, indicating three input signals. These inputs are likely to be the in-phase and quadrature components of a signal, along with a local oscillator signal, which are typically used in a quadrature mixing process.
- The output is represented by a single arrow pointing to the right, labeled "Y(t)," which signifies the output signal after the multiplication process.

3. **Labels, Annotations, and Key Indicators:**
- The label "Y(t)" next to the output arrow indicates the time-domain representation of the output signal, which is the result of the mixing process performed by the multiplier.

4. **Overall System Function:**
- This block's primary function is to modulate or demodulate signals by multiplying the input signals. In the context of a quadrature mixer, this operation helps in decomposing a real input signal into its in-phase and quadrature components, which are essential for applications in modulation, demodulation, and advanced signal processing tasks. The arrangement allows for the extraction of phase and amplitude information from the input signal, facilitating further processing in communication systems.

$$
e^{j \omega_{i} t}
$$

(b)

Fig. 12.56 A signal-flow-graph (SFG) of an quadrature mixer using (a) a real SFG and (b) a complex SFG.
image_name:(a)
description:The diagram labeled "(a)" represents a real signal-flow graph (SFG) for adding two complex signals. It consists of two primary summation blocks that process the real and imaginary components of the input signals separately.

1. **Main Components:**
- There are two summation blocks, each represented by a circle with a plus sign inside. These are used to add the incoming signals.
- The inputs to these summation blocks are labeled as \(x_{1r}\), \(x_{2r}\) for the real part, and \(x_{1q}\), \(x_{2q}\) for the imaginary part.

2. **Flow of Information or Control:**
- The first summation block receives inputs \(x_{1r}\) and \(x_{2r}\) and outputs a signal labeled \(y_{r}\), which represents the real component of the combined signal.
- The second summation block receives inputs \(x_{1q}\) and \(x_{2q}\) and outputs a signal labeled \(y_{q}\), which represents the imaginary component of the combined signal.
- The arrows indicate the direction of signal flow from the inputs to the outputs.

3. **Labels, Annotations, and Key Indicators:**
- Each input and output is clearly labeled to indicate whether it pertains to the real or imaginary part of the signal.
- The summation blocks are annotated with plus signs, indicating their function as adders.

4. **Overall System Function:**
- The overall function of this system is to decompose and recombine the real and imaginary components of two complex input signals. By processing these components separately, the system can effectively combine them into a single complex output signal, facilitating applications in modulation, demodulation, and signal processing where phase and amplitude information are critical.
image_name:(b)
description:The diagram labeled (b) depicts a complex signal-flow graph (SFG) used for adding two complex signals. It consists of the following main components:

1. **Addition Block:**
- The central component is an addition block, represented by a circle with a plus sign inside. This block is responsible for performing the addition of two input signals.

2. **Input Signals:**
- There are two input signals labeled as \(X_1\) and \(X_2\). These signals are fed into the addition block.
- Each input signal is represented as an arrow pointing towards the addition block, indicating the direction of signal flow.

3. **Output Signal:**
- The result of the addition is the output signal labeled as \(Y\). This is represented by a single arrow emanating from the addition block, indicating the direction of the output flow.

4. **Flow of Information:**
- The signals \(X_1\) and \(X_2\) are combined in the addition block to produce the output signal \(Y\).
- The flow of information is straightforward, with the inputs being added together to generate the output.

5. **Annotations and Labels:**
- The inputs \(X_1\) and \(X_2\) and the output \(Y\) are clearly labeled, indicating the roles of each signal in the system.

6. **Overall System Function:**
- The primary function of this system is to add two complex signals. The arrangement of the blocks allows for a straightforward addition of the input signals to produce a single combined output. This is essential in signal processing tasks where combining signals is required, such as in modulation and demodulation processes in communication systems.

Fig. 12.57 (a) The real SFG for adding two complex signals and (b) the equivalent complex SFG.

Combining this definition with the typical definitions for complex inversion, addition, and multiplication, and with the properties of commutation and association, constitutes a Hilbert space. It is assumed that all signals are periodic and frequency-limited and therefore can be expressed as a finite series of "complexoids" ${ }^{3}$

$$
\begin{equation*}
x_{i}(t)=\sum_{i=-N} k_{i} e^{j \omega_{0} i t} \tag{12.185}
\end{equation*}
$$

where $k_{i}$ is in general complex. Here, we will limit our consideration to a single (or a few) complexoids in order to simplify explanations.

### 12.10.2 Complex Operations

Complex continuous-time filters are realized using only three basic operations: complex addition, complex multiplication, and complex integration.

Key Point: Complex filters are realized using three basic operations performed on ordered pairs of real signals: complex addition, multiplication, and integration.

A complex addition of two complex signals simply adds the two real parts and the two imaginary parts independently. Consider the real SFG that represents adding a complex signal to a second complex signal, as is shown in Fig. 12.57(a). Its complex SFG is shown in Fig. 12.57(b).

Slightly more complicated is a complex multiplication; consider multiplying a complexoid $X(t)=e^{j \omega_{i} t}$ by a complex coefficient $\mathrm{K}=\mathrm{a}+\mathrm{jb}$. We have

$$
\begin{align*}
\mathrm{Y}(\mathrm{t})= & \left\{\mathrm{a} \cos \left(\omega_{\mathrm{i}} \mathrm{t}\right)-\mathrm{b} \sin \left(\omega_{\mathrm{i}} \mathrm{t}\right)\right\}  \tag{12.186}\\
& +\mathrm{j}\left\{\mathrm{a} \sin \left(\omega_{\mathrm{i}} \mathrm{t}\right)+\mathrm{b} \cos \left(\omega_{\mathrm{i}} \mathrm{t}\right)\right\}
\end{align*}
$$

The real SFG of this operation is shown in Fig. 12.58(a). Once again the complex SFG of a multiplication operation, as shown in Fig. 12.58(b), is considerably simpler. Note that the real SFG does not include the constant j anywhere, whereas, in the complex SFG, it is admissible.
image_name:(a)
description:The diagram labeled "(a)" represents the real signal flow graph (SFG) of a complex multiplication operation. The diagram consists of the following key components:

1. **Input Signals:**
- **x_r = cos(ω_it):** This input signal represents the cosine component of the input.
- **x_q = sin(ω_it):** This input signal represents the sine component of the input.

2. **Multiplication and Summation Blocks:**
- The input signals are each split into two paths.
- **Multiplier Blocks:**
- The cosine component (x_r) is multiplied by constants 'a' and 'b'.
- The sine component (x_q) is also multiplied by 'b' and 'a', respectively.
- **Summation Blocks:**
- The products are then summed in two separate summation blocks.
- The first summation block calculates: **y_r = a * x_r - b * x_q**.
- The second summation block calculates: **y_q = b * x_r + a * x_q**.

3. **Output Signals:**
- **y_r:** The real part of the output, resulting from the summation of the respective products.
- **y_q:** The imaginary part of the output, also resulting from the summation of the respective products.

4. **Flow of Information:**
- The signals flow from left to right, starting with the input signals being split and multiplied by their respective constants.
- The multiplied signals are then summed to produce the output signals y_r and y_q.

5. **Overall System Function:**
- This real SFG represents the multiplication of a complex number by another complex number, where the input is expressed in terms of its real and imaginary parts. The diagram illustrates how the real and imaginary components are separately processed and combined to produce the final output components, y_r and y_q, in a real-valued implementation of complex multiplication.
image_name:(b)
description:The diagram labeled (b) represents a complex signal flow graph (SFG) for a multiplication operation involving complex numbers. This diagram is simpler compared to its real counterpart.

Main Components:
1. **Multiplier Block (×):** The central component of the diagram is a multiplier block. This block is responsible for multiplying two complex signals.
2. **Inputs:**
- **e^(jωt):** One input to the multiplier is a complex exponential function, representing a rotating phasor in the frequency domain.
- **K = a + jb:** The other input is a complex constant, K, which is composed of a real part 'a' and an imaginary part 'jb'.
3. **Output (Y):** The output of the multiplier block is labeled as 'Y'. This represents the product of the complex exponential and the complex constant.

Flow of Information or Control:
- The complex exponential e^(jωt) and the complex constant K = a + jb are fed into the multiplier block.
- The multiplier performs the complex multiplication of these two inputs, resulting in an output signal 'Y'.

Labels, Annotations, and Key Indicators:
- The annotation **K = a + jb** indicates the input complex constant, explicitly showing its real and imaginary components.
- The notation **e^(jωt)** specifies the rotating phasor input, which is a common representation in signal processing for time-varying signals in the frequency domain.

Overall System Function:
The primary function of this system is to multiply a complex exponential signal by a complex constant. This operation is fundamental in signal processing, particularly in modulating signals or transforming them within the frequency domain. The simplicity of the complex SFG, as depicted in this diagram, highlights its efficiency in handling complex multiplication operations compared to real SFGs.

Fig. 12.58 (a) The real SFG of a complex multiplication and (b) the equivalent complex SFG.
image_name:(a)
description:The system block diagram labeled "(a)" depicts a complex signal flow graph (SFG) for multiplying an input signal by the imaginary constant 'j'. This operation is crucial in signal processing for handling imaginary components in complex networks.

Main Components:
- **Multiplier Block (X):** The central component of the diagram is a circular block representing multiplication. It takes an input signal 'X' and multiplies it by the imaginary unit 'j'.
- **Input and Output Signals:** The diagram shows an input signal labeled 'X' on the left and an output signal labeled 'Y' on the right.

Flow of Information or Control:
- **Signal Flow:** The input signal 'X' enters the multiplier block from the left. Inside the block, it is multiplied by the imaginary constant 'j'. The resulting output signal 'Y' exits to the right.

Labels, Annotations, and Key Indicators:
- **Imaginary Constant 'j':** The diagram prominently features the label 'j' pointing into the multiplier block, indicating the multiplication operation with the imaginary unit.
- **Input/Output Labels:** The input is labeled 'X', and the output is labeled 'Y', clarifying the direction of signal flow.

Overall System Function:
The primary function of this system is to perform a complex multiplication of an input signal by the imaginary constant 'j'. This operation effectively interchanges the real and imaginary parts of the signal, with the imaginary part being inverted. This is a fundamental operation in signal processing, particularly for transforming signals within the frequency domain and realizing imaginary components in complex networks.
image_name:(b)
description:The diagram labeled "(b)" depicts a real Signal Flow Graph (SFG) for the multiplication of a complex signal by the imaginary constant \( j \). This operation is fundamental in signal processing, particularly for manipulating the imaginary components of signals.

**Main Components:**
1. **Input Ports \( x_r \) and \( x_q \):** These represent the real and imaginary parts of the input complex signal, respectively.
2. **Output Ports \( y_r \) and \( y_q \):** These represent the real and imaginary parts of the output complex signal, respectively.
3. **Cross-Coupling Paths:**
- The path from \( x_r \) to \( y_q \) indicates that the real part of the input is directly transferred to the imaginary part of the output.
- The path from \( x_q \) to \( y_r \) includes a multiplication by \(-1\), indicating that the imaginary part of the input is inverted and transferred to the real part of the output.

**Flow of Information:**
- The real part of the input \( x_r \) is directed towards the output \( y_q \) without modification, representing the transfer of the real component to the imaginary output.
- The imaginary part of the input \( x_q \) is inverted (multiplied by \(-1\)) and directed towards the output \( y_r \), representing the transfer of the inverted imaginary component to the real output.

**Labels and Annotations:**
- The label \(-1\) on the path from \( x_q \) to \( y_r \) indicates the inversion of the imaginary component.

**Overall System Function:**
The primary function of this system is to multiply the input complex signal by the imaginary unit \( j \), effectively rotating the signal by 90 degrees in the complex plane. This is achieved by interchanging the real and imaginary parts of the input signal, with the imaginary part being inverted. This operation is crucial for signal modulation and transformation in complex signal processing networks.
image_name:Fig. 12.60
description:The system block diagram labeled "Fig. 12.60" illustrates an analog integration operator for complex signals. This operator is depicted in two forms: a single complex block and its equivalent representation using real components.

1. **Main Components:**
- **Complex Integration Block (Top Left):** This block shows the integration operation for a complex input signal `X`, resulting in an output `Y`. The integration is denoted by the operator `1/s`, where `s` represents the complex frequency variable in the Laplace transform domain.
- **Real Component Blocks (Bottom Right):** This section breaks down the complex integration into two separate real integrators. Each integrator is represented by a block labeled `1/s`:
- The first block processes the real component of the input signal `x_r`, producing the real component of the output `y_r`.
- The second block processes the imaginary component of the input signal `x_q`, producing the imaginary component of the output `y_q`.

2. **Flow of Information or Control:**
- In the complex block (top left), the input `X` is a complex signal that flows into the integration block, and the output `Y` is the integrated complex signal.
- In the real component blocks (bottom right), the real and imaginary parts of the input signal (`x_r` and `x_q`) are separately fed into their respective integrators. The outputs are the integrated real and imaginary components (`y_r` and `y_q`), maintaining the integrity of the complex signal through separate real processing paths.

3. **Labels, Annotations, and Key Indicators:**
- The complex block is labeled with `1/s`, indicating integration in the Laplace domain.
- The real component blocks are also labeled `1/s`, emphasizing that each block performs integration on its respective component.

4. **Overall System Function:**
- The primary function of this system is to perform integration on a complex signal. By using separate real integrators for the real and imaginary parts of the signal, the system effectively handles complex integration. This setup allows for the processing of complex signals in analog systems, maintaining the separation and integrity of the real and imaginary components while performing the integration operation.
image_name:Fig. 12.59
description:The diagram labeled "Fig. 12.59" illustrates two distinct system block diagrams for multiplying a signal by the imaginary constant \( j \), depicted using both complex and real Signal Flow Graphs (SFGs).

Main Components:
1. **Complex SFG (a):**
- **Multiplier Block:** A circle with an 'X' inside represents the multiplication operation.
- **Input and Output:** The input signal \( X \) is multiplied by the constant \( j \) to produce the output \( Y \).

2. **Real SFG (b):**
- **Input Signals:** The real part \( x_r \) and imaginary part \( x_q \) of the input signal are indicated.
- **Cross-Coupling Paths:** Two lines cross each other, with one path including a multiplier of \( -1 \).
- **Output Signals:** The real part \( y_r \) and imaginary part \( y_q \) of the output signal are indicated.

Flow of Information or Control:
- **Complex SFG (a):**
- The input signal \( X \) is directly multiplied by \( j \), transforming it into the output \( Y \).
- **Real SFG (b):**
- The real input \( x_r \) is directed to the imaginary output \( y_q \) without modification.
- The imaginary input \( x_q \) is inverted (multiplied by \( -1 \)) before being directed to the real output \( y_r \).

Labels, Annotations, and Key Indicators:
- **Complex SFG (a):** Clearly labeled with \( j \) to indicate the multiplication by the imaginary unit.
- **Real SFG (b):** The \( -1 \) label indicates the inversion of the imaginary component.

Overall System Function:
The primary function of these diagrams is to demonstrate the multiplication of a signal by the imaginary constant \( j \). The complex SFG (a) simplifies this operation by directly multiplying the input by \( j \). In contrast, the real SFG (b) illustrates how this can be achieved using real components by interchanging and inverting parts of the signal, effectively separating the real and imaginary components for processing. This operation is crucial for realizing imaginary components in complex networks, enabling the representation and manipulation of complex signals in signal processing applications.

Fig. 12.5 9 Multiplying a signal by the imaginary constant j.

Fig. 12.60 The analog integration operator for complex signals.

A special case is the multiplication of an input signal by the constant j . This is shown using a complex SFG in Fig. 12.59(a) and a real SFG in Fig. 12.59(b). This operation is simply an interchanging of the real and inverted imaginary parts; this operation is the basis of realizing imaginary components in complex networks; that is, imaginary gains are realized by cross-coupling in the two real networks.

One additional operation is required for realizing complex filters: the integration operator. This simply consists of applying the corresponding real operation to each part of the complex signal, as shown in Fig. 12.60.

### 12.10.3 Complex Filters

Complex filters are important and widely used signal processing blocks in modern wireless transceivers. Complex filters use cross-coupling between the real and imaginary signal paths in order to realize asymmetrical (in the frequency domain) filters having transfer functions that do not have the conjugate symmetry of real filters. This implies that their transfer functions have complex coefficients. Complex filters can be realized using the basic operations of addition and multiplication and the integrator operator.

A complex transfer function can be realized by using four real SFG filters

Key Point: Complex filters use cross-coupling between real and imaginary signal paths to realize transfer functions that do not have the frequencydomain conjugate symmetry of real filters.
as shown in Figure 12.61 where we have

$$
\begin{equation*}
\mathrm{R}(\mathrm{~s})=\frac{\mathrm{H}(\mathrm{~s})+\mathrm{H}^{*}(\mathrm{~s})}{2} \tag{12.187}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{jQ}(\mathrm{~s})=\frac{\mathrm{H}(\mathrm{~s})-\mathrm{H}^{*}(\mathrm{~s})}{2} \tag{12.188}
\end{equation*}
$$

When the filters leading from the real and imaginary branches of Fig. 12.61 do not exactly match, imaging errors (plus less harmful magnitude response errors) occur.
image_name:(a)
description:The system block diagram labeled "(a)" depicts a complex filter system with the following components and flow of information:

1. **Main Components:**
- **Complex Filter Block (H(s))**: This is the central component of the diagram. It represents a complex transfer function \( H(s) \) that processes an input signal \( X(s) \) to produce an output signal \( Y(s) \).

2. **Flow of Information or Control:**
- The input signal \( X(s) \) enters the complex filter block on the left side. This signal is processed by the complex filter \( H(s) \), and the resulting output signal \( Y(s) \) exits on the right side.
- The diagram suggests a direct flow of information from the input to the output through the complex filter, indicating a straightforward processing path without any visible feedback loops or additional control mechanisms.

3. **Labels, Annotations, and Key Indicators:**
- The input and output signals are labeled as \( X(s) \) and \( Y(s) \), respectively, indicating their roles in the system.
- The block is labeled as "Complex H(s)," which signifies that the filter performs complex signal processing.

4. **Overall System Function:**
- The primary function of this system is to apply a complex filter to the input signal \( X(s) \) to produce the output signal \( Y(s) \). The complex filter \( H(s) \) is likely designed to handle both real and imaginary components of the signal, providing a sophisticated level of filtering that can be used in applications requiring complex signal processing.
image_name:(b)
description:The block diagram labeled as (b) illustrates a system for realizing a complex filter \( H(s) = R(s) + jQ(s) \) using real signal flow graph (SFG) transfer filters \( R(s) \) and \( Q(s) \). The primary components and flow of the system are described as follows:

Main Components:
1. **Filters \( R(s) \) and \( Q(s) \):**
- Two identical \( R(s) \) filters and two identical \( Q(s) \) filters are present in the system. These filters are used to process the real and imaginary components of the input signals.

2. **Summation Blocks:**
- Two summation blocks are used to combine the outputs of the filters. They are positioned at the end of the processing chain for both real and imaginary signal paths.

Flow of Information or Control:
- **Inputs:**
- The system receives two input signals: \( x_r(s) \) (real part) and \( x_q(s) \) (imaginary part).
- **Signal Path:**
- The real input \( x_r(s) \) is fed into the first \( R(s) \) filter and the first \( Q(s) \) filter.
- The imaginary input \( x_q(s) \) is fed into the second \( Q(s) \) filter and the second \( R(s) \) filter.
- **Outputs:**
- The outputs from the \( R(s) \) and \( Q(s) \) filters are combined in the summation blocks.
- The first summation block subtracts the output of the \( Q(s) \) filter from the \( R(s) \) filter to produce \( y_r(s) \), the real part of the output.
- The second summation block adds the output of the \( Q(s) \) filter to the \( R(s) \) filter to produce \( y_q(s) \), the imaginary part of the output.

Labels, Annotations, and Key Indicators:
- The diagram clearly labels the input and output signals as \( x_r(s) \), \( x_q(s) \), \( y_r(s) \), and \( y_q(s) \) to indicate their roles in the complex filtering process.
- The filters are labeled as \( R(s) \) and \( Q(s) \), indicating their function in the system.

Overall System Function:
The system's primary function is to realize a complex filter \( H(s) \) by processing real and imaginary input signals through real-valued filters \( R(s) \) and \( Q(s) \). The arrangement of the filters and summation blocks allows for the combination of these processed signals into a complex output, effectively implementing the desired complex transfer function. This setup is crucial for applications where complex signal processing is required, such as in communication systems and signal analysis.

Fig. 12.61 Realizing a complex filter $H(s)=R(s)+j Q(s)$ by real SFG transfer filters $R(s)$ and $Q(s)$.

### 12.10.4 Frequency-Translated Analog Filters

Key Point: Real filters can be frequencytranslated into complex transfer functions by substituting $(s-j \omega)$ for $s$.

Complex analog transfer functions can be realized by frequency-translating real filters [Snelgrove, 1982], [Sedra, 1985]. Specifically, one method for deriving complex transfer functions is to employ a complex substitution for the Laplace variable s. For example, to effect a positive frequency shift, one uses the substitution

$$
\begin{equation*}
s \rightarrow s-j \omega_{0} \tag{12.189}
\end{equation*}
$$

The effect of this substitution on a low-pass filter is shown in Fig. 12.62
A method for realizing complex analog filters is to start with an active RC prototype filter and then transform it to a complex frequency-translated filter; the procedure to do this is simple:

- First, use an active-RC prototype filter that is fully-differential. This is used to make the realization of negative components trivial.
- Secondly, replicate exactly the prototype filter in order to realize the signal path for the imaginary signal components.
- Finally, add cross-coupled resistors for each capacitor. The size and signs of these resistors determine the frequency translation.
image_name:|H₀(ω)|
description:The graph titled "|H₀(ω)|" represents the magnitude response of a filter in the frequency domain. It is likely a Bode magnitude plot, given the context of filter design.

1. **Type of Graph and Function:**
- This is a frequency response graph, specifically showing the magnitude of the transfer function |H₀(ω)| as a function of frequency ω.

2. **Axes Labels and Units:**
- The horizontal axis represents frequency (ω), typically in radians per second (rad/s) or hertz (Hz).
- The vertical axis represents the magnitude of the transfer function, which is dimensionless but often expressed in decibels (dB) in similar contexts.
- The scale appears to be linear, as there are no logarithmic markers or gridlines visible.

3. **Overall Behavior and Trends:**
- The graph shows a central peak at ω = 0, indicating a bandpass or bandstop filter characteristic.
- The magnitude increases to a peak at the center and then symmetrically decreases on both sides, forming a trapezoidal shape.
- Beyond the main peak, there are smaller oscillations or ripples visible on both sides, suggesting the presence of additional frequency components or an imperfect stopband.

4. **Key Features and Technical Details:**
- The central peak suggests the filter allows or attenuates frequencies around ω = 0. The exact nature (bandpass or bandstop) depends on whether the peak represents a maximum or a minimum magnitude.
- The graph is symmetrical about the y-axis, indicating the filter's response is even.
- The smaller oscillations on either side of the main peak may indicate side lobes, which are common in filters designed with certain windowing techniques.

5. **Annotations and Specific Data Points:**
- The graph does not have specific numerical annotations or markers for critical values such as -3 dB points or bandwidth.
- The zero frequency point (ω = 0) is explicitly marked, serving as a reference for the central peak.

Overall, the graph depicts a frequency response with a central peak at zero frequency, surrounded by symmetrical side lobes, characteristic of a filter designed to process complex signals with specific frequency translation properties.

image_name:(a)
description:The graph in question is a frequency response plot, specifically representing the magnitude of a transfer function |H(ω)| against frequency ω. This type of graph is often used to illustrate the behavior of filters in the frequency domain.

**Axes Labels and Units:**
- The horizontal axis represents frequency (ω), typically measured in radians per second. The zero frequency point (ω = 0) is explicitly marked.
- The vertical axis represents the magnitude of the transfer function |H(ω)|, which is dimensionless.

**Overall Behavior and Trends:**
- The graph shows a central peak at zero frequency (ω = 0), which is the highest point of the graph, indicating the maximum magnitude of the transfer function at this frequency.
- Surrounding the central peak, there are symmetrical side lobes that decrease in magnitude as they move away from the central peak.
- The overall shape suggests a band-pass filter characteristic, where the filter allows frequencies around zero to pass while attenuating frequencies further away.

**Key Features and Technical Details:**
- The central peak at ω = 0 is a defining feature, indicating the filter's primary passband.
- The side lobes are symmetrical and decrease in magnitude, which is typical for certain types of filters designed to have specific frequency translation properties.
- The graph includes a labeled frequency difference Δω = ω₀, indicating the bandwidth or the width of the passband around the central peak.

**Annotations and Specific Data Points:**
- The graph does not have specific numerical annotations or markers for critical values such as -3 dB points or exact bandwidth measurements, other than the labeled Δω = ω₀.
- No additional gridlines or numerical scales are provided, focusing the viewer's attention on the symmetry and shape of the response curve.

Overall, the graph depicts a frequency response with a central peak at zero frequency, surrounded by symmetrical side lobes, characteristic of a filter designed to process complex signals with specific frequency translation properties.

image_name:(a)
description:
[
name: Ci, type: Capacitor, value: Ci, ports: {Np: x, Nn: y}
]
extrainfo:The diagram shows a simple real prototype filter consisting of a single capacitor 'Ci' connected between nodes 'x' and 'y'. This represents the initial stage before transforming into a complex filter.
image_name:(b)
description:
[
name: Ci, type: Capacitor, value: Ci, ports: {Np: X, Nn: Y}
name: -jGi, type: Resistor, value: -jGi, ports: {N1: X, N2: Y}
]
extrainfo:The circuit diagram (b) represents a parallel combination of a capacitor Ci and a resistor with a negative imaginary value -jGi, connecting the input node X to the output node Y. This configuration is part of a filter transformation process, aiming to achieve specific frequency translation properties in a complex filter design.
image_name:(c)
description:
[
name: Ci1, type: Capacitor, value: Ci, ports: {Np: xr, Nn: yr}
name: Gi, type: Resistor, value: Gi, ports: {N1: yr, N2: xq}
name: -Gi, type: Resistor, value: -Gi, ports: {N1: xq, N2: yq}
name: Ci2, type: Capacitor, value: Ci, ports: {Np: xq, Nn: yq}
]
extrainfo:The circuit is a realization of a complex capacitor using resistors and capacitors to achieve frequency translation properties. It involves two sections with cross-coupled resistors to introduce complex conjugate symmetry.

Fig. 12.63 (a) A capacitor in the real prototype filter, (b) the transformed capacitor in the complex filter, and (c) the real-component realization of the complex capacitor.

The second step transforms the real prototype filter into a complex conjugate symmetric filter at the same frequencies as the prototype filter. To see how the third steps results in the desired frequency translation, consider Fig. 12.63.

Fig. 12.63(a) shows one of the capacitors in a complex filter at the same frequencies as the real prototype filter. Applying the frequency translation $\mathrm{s} \rightarrow \mathrm{s}-\mathrm{j} \omega_{0}$ results in transforming the capacitor to an admittance of a capacitor (of the same size) in parallel with an imaginary resistor of size $-\mathrm{j} \omega_{0} \mathrm{C}$ according

Key Point: Beginning with an active-RC prototype filter, duplicating it, and cross-coupling the two signal paths with resistors results in a complex frequency translation of the filter response.
to the substitution

$$
\begin{equation*}
s C \rightarrow s C-j \omega_{0} C \tag{12.190}
\end{equation*}
$$

This is shown in Fig. 12.63(b) where

$$
\begin{equation*}
\mathrm{G}_{\mathrm{i}}=\omega_{0} \mathrm{C}_{\mathrm{i}} \tag{12.191}
\end{equation*}
$$

In order to realize the complex filter using real components, two identical real filters are used with crosscoupling, as is shown in Fig. 12.63(c). The negative cross-coupled resistor can be realized using fully differential circuits.

#### EXAMPLE 12.11

Design a complex filter with a transmission zero at $\mathrm{S}=-\mathrm{j} \omega_{0}$.
image_name:(a)
description:
[
name: C, type: Capacitor, value: C, ports: {Np: x, Nn: y}
name: G1, type: Resistor, value: G1, ports: {N1: y, N2: GND}
]
extrainfo:The circuit diagram (a) represents a simple high-pass filter with a capacitor C connected between nodes x and y, and a resistor G1 connected from node y to ground.
image_name:(b)
description:
[
name: C, type: Capacitor, value: C, ports: {Np: X, Nn: Y}
name: G1, type: Resistor, value: G1, ports: {N1: Y, N2: GND}
name: jG2, type: Resistor, value: jG2, ports: {N1: X, N2: Y}
]
extrainfo:The circuit diagram (b) represents a complex band-stop filter with a capacitor C and two resistors: G1 connected to ground and jG2 connected in parallel with the capacitor. The circuit is designed to realize a complex filter with a transmission zero at S=-jω0.
image_name:(c)
description:
[
name: C1, type: Capacitor, value: C, ports: {Np: X+, Nn: Y+}
name: C2, type: Capacitor, value: C, ports: {Np: X-, Nn: Y-}
name: G1/2, type: Resistor, value: G1/2, ports: {N1: Y+, N2: Y-}
name: jG2_1, type: Resistor, value: jG2, ports: {N1: X+, N2: X-}
name: jG2_2, type: Resistor, value: jG2, ports: {N1: X-, N2: X+}
]
extrainfo:The circuit diagram (c) represents a fully-differential complex filter design using real components. It uses capacitors and resistors with cross-coupling to achieve the desired filtering characteristics.
image_name:(d)
description:
[
name: C, type: Capacitor, value: C, ports: {Np: x_r+, Nn: y_r+}
name: G1/2, type: Resistor, value: G1/2, ports: {N1: y_r+, N2: y_r-}
name: C, type: Capacitor, value: C, ports: {Np: x_r-, Nn: y_r-}
name: G2, type: Resistor, value: G2, ports: {N1: x_q^+, N2: y_r+}
name: G2, type: Resistor, value: G2, ports: {N1: x_q-, N2: y_r-}
]
extrainfo:The circuit diagram (d) represents a fully differential complex filter design with cross-coupled real admittances. It consists of two identical sections, each containing a capacitor and two resistors. The resistors are labeled G2 and G1/2, and the capacitors are labeled C. The nodes are annotated as x_r, x_r^+, y_r, y_r^+, x_q, x_q^+, y_q, and y_q^+. The design aims to achieve a complex band-stop filter using real components.

Fig. 12.64 Using a complex frequency translation to realize a PPF: (a) the high-pass prototype, (b) the complex band-stop having a complex admittance, (c) a fully-differential version of (b), and (d) replacing the complex admittances with cross-coupled real admittances between the real and imaginary paths.

#### Solution

Begin with the passive RC high-pass filter shown in Fig. 12.64(a) which has a transmission zero at $\mathrm{s}=0$. The transmission zero at dc will be frequency-shifted to negative frequencies, so we use the substitution $\mathrm{s} \rightarrow \mathrm{s}+\mathrm{j} \omega_{0}$. Letting

$$
\begin{equation*}
\omega_{0}=\frac{\mathrm{G}_{2}}{\mathrm{C}} \tag{12.192}
\end{equation*}
$$

gives the required substitution as

$$
\begin{equation*}
\mathrm{sC} \rightarrow \mathrm{sC}+\mathrm{j} \mathrm{G}_{2} \tag{12.193}
\end{equation*}
$$

Thus, the complex frequency-shifted high-pass is now as shown in Fig. 12.64(b). A fully-differential version of the circuit of Fig. 12.64(b) is shown in Fig. 12.64(c). This complex filter can be realized by two parallel real filters
image_name:(a)
description:The system block diagram labeled "(a)" represents a basic integrator circuit.

1. **Main Components:**
- The primary component in this diagram is an integrator, represented by the block labeled "1/s". This block performs the mathematical integration of the input signal over time.

2. **Flow of Information or Control:**
- The input to this integrator is denoted by \( x_r \), which enters the integrator block on the left side.
- The output of the integrator is labeled \( y_r \), which exits from the right side of the block.
- The signal flow is linear and unidirectional from input \( x_r \) to output \( y_r \), indicating that the input signal is integrated to produce the output.

3. **Labels, Annotations, and Key Indicators:**
- The block "1/s" indicates the transfer function of the integrator, which is a standard representation in Laplace transform notation for continuous-time systems.
- The input and output signals are labeled as \( x_r \) and \( y_r \) respectively, providing clarity on the signal flow direction.

4. **Overall System Function:**
- The primary function of this system is to perform integration on the input signal \( x_r \). The integrator accumulates the input signal over time and provides the integrated result as the output \( y_r \). This type of block is fundamental in control systems and signal processing for tasks such as generating a ramp signal from a step input or integrating error signals in feedback control systems.
image_name:(b)
description:The block diagram labeled (b) represents a complex frequency-shifted integrator. It consists of a single block with the transfer function \( \frac{1}{s - j\omega_0} \). This indicates a frequency shift in the complex plane by \( \omega_0 \), where \( s \) is the complex frequency variable.

Main Components:
- **Integrator Block**: The central component is an integrator with a frequency shift, represented by the transfer function \( \frac{1}{s - j\omega_0} \). This implies that the integrator operates at a shifted frequency, effectively filtering the input signal around this new frequency.

Flow of Information or Control:
- **Input and Output**: The input signal \( X \) enters the integrator block, and the output \( Y \) exits from the other side. The signal flow is unidirectional from left to right, indicating a straightforward processing path through the integrator.

Labels, Annotations, and Key Indicators:
- **Transfer Function**: The key label on the block is \( \frac{1}{s - j\omega_0} \), which is crucial for understanding the frequency-shifting characteristic of this integrator.

Overall System Function:
- **Frequency-Shifted Integration**: The primary function of this system is to integrate the input signal while applying a frequency shift by \( \omega_0 \). This makes the integrator sensitive to a specific frequency range, allowing it to act as a complex filter that can isolate or process signals around the shifted frequency. This type of system is often used in applications requiring selective frequency manipulation, such as in communication systems or signal processing tasks where specific frequency bands need to be targeted.
image_name:(c)
description:The system block diagram labeled (c) represents a complex frequency-shifted high-pass filter. Here is a detailed description of the diagram:

1. **Main Components:**
- **Adder/Subtractor Blocks:** There are two adder blocks in the diagram. The first adder block combines the input signal with feedback from the output.
- **Integrator (1/s Block):** The central component is an integrator block labeled as \( \frac{1}{s} \), which is responsible for integrating the input signal over time.
- **Multiplier Block:** This block multiplies the feedback signal by a complex frequency \( j\omega_0 \), effectively shifting the frequency of the signal.

2. **Flow of Information or Control:**
- The input signal \( X \) enters the first adder block, where it is combined with a feedback signal.
- The combined signal is then fed into the integrator block \( \frac{1}{s} \), which outputs an integrated signal.
- This output is split into two paths: one is directed to the output \( Y \), and the other is fed back into the system.
- The feedback path includes a multiplier that shifts the frequency of the feedback signal by multiplying it with \( j\omega_0 \).
- The frequency-shifted feedback signal is then fed back into the first adder block, completing the loop.

3. **Labels, Annotations, and Key Indicators:**
- The diagram is labeled with the input \( X \) and output \( Y \), indicating the flow of the signal through the system.
- The frequency shift is indicated by the label \( j\omega_0 \) at the multiplier block.

4. **Overall System Function:**
- The primary function of this system is to act as a complex high-pass filter with a frequency shift. The integrator provides the basic filtering action, while the multiplier shifts the frequency of the feedback signal, allowing the filter to handle complex frequencies. This setup is useful in applications requiring frequency-selective filtering, such as communication systems or signal processing tasks that involve complex signal manipulation.
image_name:(d)
description:The system block diagram labeled (d) represents a poly-phase network used for frequency shifting in a complex filter system. This diagram consists of two parallel integrator paths with cross-coupled feedback, designed to shift real signals to complex positive-frequency signals.

Main Components:
1. **Integrators (1/s):**
- There are two integrator blocks, each represented by the transfer function 1/s. These integrators process the input signals and are crucial for the filtering operation.

2. **Adders (+):**
- Two adders are used to combine the input signals with feedback signals. Each adder has two inputs and one output, facilitating signal summation.

3. **Feedback Paths with Frequency Shift (ω₀):**
- Cross-coupled feedback paths are present, each introducing a frequency shift denoted by ω₀. This shift is essential for converting real signals into their complex counterparts.

Flow of Information or Control:
- **Inputs:** The system receives two input signals, xₑ (real part) and xₓ (imaginary part).
- **Signal Processing:**
- The real input xₑ is fed into the upper adder, where it is combined with a feedback signal from the lower integrator output, which is shifted by ω₀.
- The imaginary input xₓ is similarly processed in the lower adder, receiving feedback from the upper integrator output, also shifted by ω₀.
- **Output Generation:**
- The outputs from the integrators are yₑ (real part) and yₓ (imaginary part), representing the complex frequency-shifted signals.

Labels, Annotations, and Key Indicators:
- **ω₀:** Represents the frequency shift applied in the feedback paths, crucial for achieving complex signal processing.
- **Cross-Coupled Feedback:** Indicates the interaction between the two parallel paths, essential for the poly-phase network's operation.

Overall System Function:
The primary function of this diagram is to realize a continuous-time complex filter by employing a poly-phase network. The configuration allows for the frequency shifting of real integrator outputs to complex positive-frequency outputs, making it suitable for applications that require complex signal processing, such as communication systems. The cross-coupled feedback paths ensure the necessary phase relationships between the real and imaginary components, enabling effective frequency translation.

Fig. 12.65 Frequency shifting a real integrator to a complex positive-frequency integrator.
with cross-coupled resistors, as is shown in Fig. 12.64( $d$ ). This circuit is referred to as a poly-phase network. Taking the load $\mathrm{G}_{1}=0$ would result in very narrow notches. Normally, poly-phase networks are intended to be cascaded [Gingell, 1973] and the load on each section is the succeeding section [Behbahani, 2001].

An alternative procedure for realizing continuous-time complex filters is based on frequency-translating SFG prototype filters which are based on integrators [Snelgrove, 1982]. This procedure is illustrated by applying it to the single integrator shown in Fig. 12.65(a). In Fig. 12.65(b) and (c) are shown complex SFGs that realize the fre-quency-shifted integrator. The complex SFG of Fig. 12.65(c) is converted to the equivalent real SFG of Fig. $12.65(d)$, where the necessary cross-coupling is explicit. The procedure for frequency-shifting any real SFG integrator-based filter is simply: a) replicate the real SFG filter for the imaginary path, and b) cross-couple at each integrator, as is shown in Fig. 12.65(d); the strength of the cross-couplings determine the frequency of the shift. As always, this cross-coupling is simplified by using fully-differential circuits.

## 12.11 KEY POINTS

- Continuous-time integrated analog filters process signals that are both continuous in amplitude and time. Dis-crete-time analog filters process signals sampled in time, and therefore generally operate on lower-frequency signals than their continuous-time counterparts. [p. 469]
- Integrators, summers, and gain stages are the fundamental building blocks of analog filters. [p. 469]
- Any rational transfer function with real-valued coefficients may be factored into first- and second-order terms and, therefore, implemented as a cascade of first- and second-order filters. [p. 470]
- One integrator is required for each pole in an analog filter. [p. 470]
- A popular biquad implementation is two integrators in a loop, one being lossy. The gains around the loop determine its resonant frequency, the integrator loss determines the Q-factor, and the input gains and locations determine the transfer function zeros and gain. [p. 471]
- In $\mathrm{G}_{\mathrm{m}}-\mathrm{C}$ filters, integrators are realized with a transconductor, which produces a output current proportional to the input voltage, and a capacitor, which integrates the current to produce the output voltage. [p. 472]
- Current signals are readily summed by simply shorting them together. [p. 473]
- Fully-differential circuits are often preferred in analog integrated circuits as they provide improved linearity and noise immunity. [p. 474]
- Differentiating signal paths are sometimes provided by capacitive feed-ins. [p. 475]
- Source-degenerating a differential pair with a resistor linearizes the relationship between differential input voltage and output current. The result is a transconductor with a value approximately equal to the degeneration resistance. [p. 480]
- Feedback may be used to more accurately reproduce the input voltage across the degeneration resistor or further improve the linearity of transconductors with fixed resistors. [p. 483]
- Triode transistors can be used in placed of fixed resistors to make transconductors tunable, although their linearity is generally reduced. [p. 484]
- Transconductors whose gain is based upon the small-signal transconductance of active-mode transistors generally offer increased speed, but reduced linearity, compared with transconductors based upon triode devices. [p. 493]
- Bipolar transconductors based on fixed resistors may be made tunable by cascading them with an adjustablegain cell. [p. 500]
- Active RC filters employ resistors connected to virtual ground nodes to perform voltage-to-current conversion, and then integrate the resulting currents upon Miller capacitors, connected in feedback around high-gain amplifiers. [p. 510]
- Replacing the fixed resistors of an active RC integrator with transistors in triode provides tunability, but reduces linearity. [p. 514]
- Adding fixed passive series resistors to active MOSFET-C filters can improve their linearity. [p. 516]
- Analog filter time constants, determined by $\mathrm{G}_{\mathrm{m}} / \mathrm{C}$ or RC products, vary considerably over process and temperature. Hence, tuning is required to ensure accurate and repeatable frequency responses. [p. 516]
- Complex filters are realized using three basic operations performed on ordered pairs of real signals: complex addition, multiplication, and integration. [p. 526]
- Complex filters use cross-coupling between real and imaginary signal paths to realize transfer functions that do not have the frequency-domain conjugate symmetry of real filters. [p. 527]
- Real filters can be frequency-translated into complex transfer functions by substituting ( $\mathrm{s}-\mathrm{j} \omega$ ) for s . [p. 528]
- Beginning with an active-RC prototype filter, duplicating it, and cross-coupling the two signal paths with resistors results in a complex frequency translation of the filter response. [p. 529]
