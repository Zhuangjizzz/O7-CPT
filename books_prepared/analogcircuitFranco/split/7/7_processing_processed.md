# Frequency and Time Responses

Chapter Outline

6.1 High-Frequency BJT Model ..... 566
6.2 High-Frequency MOSFET Model ..... 574
6.3 Frequency Response of CE/CS Amplifiers ..... 581
6.4 Frequency Response of Differential Amplifiers ..... 592
6.5 Bipolar Voltage and Current Buffers ..... 599
6.6 MOS Voltage and Current Buffers ..... 606
6.7 Open-Circuit Time-Constant (OCTC) Analysis ..... 612
6.8 Frequency Response of Cascode Amplifiers ..... 623
6.9 Frequency and Transient Responses of Op Amps ..... 629
6.10 Diode Switching Transients ..... 639
6.11 BJT Switching Transients ..... 644
6.12 Transient Response of CMOS Gates and Voltage Comparators ..... 652
Appendix 6A: Transfer Functions and Bode Plots ..... 665
References ..... 672
Problems ..... 672
n our study of electronic circuits so far we have tacitly assumed that diodes and transistors react to external signals instantaneously. This is approximately true only up to certain operating frequencies, above which various parasitic reactances come into play, whose effect is to limit the frequency response and operating speed of a circuit (speed and frequency characteristics are collectively referred to as dynamics). Since diodes and transistors operate on the principle of charge control, their internal parasitics are of the capacitive type, with the junction capacitance $C_{j}$ encountered in Chapter 1 being a familiar example. But, even without any electronic devices present, a circuit exhibits inherent reactive parasitics stemming from
its dimensions and layout. In fact, viewing a circuit as a collection of nodes and branches, we can safely say that

- each node exhibits stray capacitance toward its nearby nodes, including the reference or ground node
- each branch exhibits stray self-inductance as well as inductive coupling to its nearby branches

A capacitance, whether intentional or parasitic, tends to oppose changes in the voltage across it, whereas an inductance tends to oppose changes in the current through it. These parasitics are generally small, indicating that below certain operating frequencies, stray capacitances act as open circuits and stray inductances act as short circuits and can thus be ignored. However, as a circuit's operating frequency or operating speed is increased, the roles of capacitances and inductances are reversed, so capacitance now approach short-circuit behavior and inductances open-circuit behavior. In the circuits of interest to us here it so happens that the most severe limitations stem from stray capacitances. To be able to investigate their effect upon the dynamics of a circuit we therefore need to augment the small-signal transistor models utilized so far with suitable capacitances.

Both BJTs and MOSFETs include pn junctions, so their models must incorporate the corresponding junction capacitances. The MOSFET includes also the capacitances formed by the gate with the channel as well as with the source and drain regions. There is no counterpart of these capacitances in the BJT. On the other hand, the BJT exhibits a capacitance associated with the minority charge buildup inside the base region that does not have a counterpart in the MOSFET. We thus have similarities but also differences in the physical origin of the parasitics of the two devices. Yet, the similarities are strong enough that once the student has mastered the highfrequency analysis of one of the two device types, a good deal of it can be adapted to the other.

CHAPTER HIGHLIGHTS

The chapter begins with the physical basis of the parasitic capacitances of BJTs and MOSFETs, after which suitable high-frequency models are developed for both devices.

These models are then applied to the study of the high-frequency behavior of the basic single transistor configurations (CE/CS, CC/CD) and CB/CG configurations), as well as differential pairs, both passive loaded and active loaded. Since the distinguishing feature of the $\mathrm{CC} / \mathrm{CD}$ and $\mathrm{CB} / \mathrm{CG}$ configurations is their ability to effect impedance transformation, particular attention is given to terminal impedances and modeling thereof, especially when it comes to inductive impedances due to their notorious tendency to cause ringing or even oscillations.

As circuit complexity increases, frequency analysis tends to become prohibitively difficult. The open-circuit time-constant (OCTC) technique discussed next alleviates the task by breaking it down into multiple but simpler sub-tasks, which we
then use to estimate the circuit's bandwidth. The OCTC technique proves particularly useful in the analysis of multiple-transistor circuits such as the cascode configuration.

The frequency response illuminates only certain aspects of a circuit's dynamics. To complete the picture we need to know also the transient response, the dual counterpart. Op amps offer a classic example in which it proves useful to know both viewpoints side by side.

There are situations in which only the transient response is of interest, especially when it comes to highly nonlinear applications such as switches and logic gates. The chapter concludes with the switching transients of pn junctions and BJTs, the propagation delays of CMOS logic gates, and the response times of voltage comparators.

Frequency analysis requires a certain amount of dexterity with the manipulations of transfer functions and the construction of Bode plots. For convenience, these subjects are briefly reviewed in Appendix 6A, at the end of the chapter. The chapter makes abundant use of PSpice both as a software oscilloscope to display Bode plots and transient responses, and as a verification tool for hand calculations.

## 6.1 HIGH-FREQUENCY BJT MODEL

Recall that a BJT comprises two $p n$ junctions. In junction-isolated integrated circuits (ICs) there is a third junction providing electric isolation between each BJT and its surrounding components on the chip (this junction is always reverse biased). As we know, each junction exhibits a voltage-dependent capacitance called the junction ca pacitance, whose characteristic is depicted in Fig. 1.41b. In the case of the npn BJT of Fig. 6.1, the three capacitances of interest are:

- The base-emitter junction capacitance $C_{j e}$,

$$
\begin{equation*}
C_{j e}\left(v_{B E}\right)=\frac{C_{j e 0}}{\left(1-v_{B E} / \phi_{e}\right)^{m_{e}}} \tag{6.1a}
\end{equation*}
$$

where $C_{j e 0}$ is the zero-bias value of $C_{j e}, v_{B E}$ is the base-emitter voltage, $\phi_{e}$ is the built-in potential of the base-emitter junction, and $m_{e}$ is the junction's grading coefficient, typically between $1 / 2$ for abrupt junctions, and $1 / 3$ for graded junctions. In forward-active operation $v_{B E}$ doesn't vary much from its typical value $V_{B E(\text { on })}(=0.7 \mathrm{~V})$, so it is common practice to approximate

$$
\begin{equation*}
C_{j e}\left(V_{B E(\mathrm{on})}\right) \cong 2 C_{j e 0} \tag{6.1b}
\end{equation*}
$$

- The base-collector junction capacitance $C_{j c}$, more commonly denoted as $C_{\mu}$ in analog electronics,

$$
\begin{equation*}
C_{\mu}\left(v_{B C}\right)=\frac{C_{\mu 0}}{\left(1-v_{B C} / \phi_{c}\right)^{m_{c}}} \tag{6.2}
\end{equation*}
$$

with similar meaning for the various parameters. In forward-active operation we usually have $v_{B C}<0$, so it follows that $C_{\mu}<C_{\mu 0}$.
image_name:FIGURE 6.1
description:The diagram illustrates the junction capacitances of a monolithic npn Bipolar Junction Transistor (BJT). The image is a cross-sectional view highlighting the various layers and components within the transistor structure.

1. **Identification of Components and Structure:**
- The diagram shows three main terminals labeled as E (Emitter), B (Base), and C (Collector).
- The semiconductor layers are represented, including an n+ emitter region, a p base region, and an n+ collector region within an n- epitaxial layer.
- A buried n+ layer is depicted beneath the n- epitaxial layer, providing low-resistance paths for current flow.
- The p- substrate forms the foundation of the structure, and there are p- isolation regions (Iso) surrounding the active regions to provide electrical isolation.

2. **Connections and Interactions:**
- Capacitances are indicated at various junctions: \( C_{je} \) (base-emitter junction capacitance), \( C_{\mu} \) (base-collector junction capacitance, also known as the Miller capacitance), and \( C_{s} \) (collector-to-substrate junction capacitance).
- The base-emitter junction capacitances \( C_{je} \) are shown connected across the n+ emitter and p base regions.
- The base-collector capacitances \( C_{\mu} \) are shown across the p base and n+ collector regions.
- The collector-to-substrate capacitances \( C_{s} \) are shown between the n+ collector and the p- substrate.
- The substrate (S) is tied to the most negative voltage (MNV) to ensure the collector-to-substrate junction remains in reverse bias, preventing conduction but allowing for stray capacitance effects.

3. **Labels, Annotations, and Key Features:**
- The diagram labels the different semiconductor regions and capacitances clearly, aiding in understanding the physical layout and electrical characteristics of the BJT.
- The annotations help explain the role of each capacitance in the operation of the transistor, particularly in high-frequency applications where these parasitic capacitances can affect performance.

Overall, the diagram provides a detailed view of the internal structure and capacitances of a monolithic npn BJT, highlighting the key regions and electrical interactions within the device.

FIGURE 6.1 The junction capacitances of a monolithic npn BJT.

- The collector-to-substrate junction capacitance $C_{s}$, with a similar expression as the one above. To ensure isolation, this junction must always be in reverse bias, so to prevent it from ever turning on, the substrate $S$ is internally tied to the most negative voltage (MNV) in the circuit. With $v_{S C}<0$ this junction is nonconductive, yet it presents a stray capacitance $C_{s}$ whose effect is to shunt high-frequency collector signals to the ac grounded substrate.

Figure 6.1 indicates that all three capacitances are of the distributed type and that their areas increase as we go from $C_{j e}$ to $C_{\mu}$ to $C_{s}$. However, the depletion-layer widths also increase in the same order due to progressively lighter doping levels from emitter to base to collector and to substrate. So, if we visualize each capacitance as $C_{j}=\varepsilon_{s t} A / X_{d}$ as per Fig. 1.42b, it is not surprising that the three capacitance values do not differ that much from each other. Depending on transistor size, $C_{j e 0}, C_{\mu 0}$, and $C_{s 0}$ may range from a few picofarads ( $1 \mathrm{pF}=10^{-12} \mathrm{~F}$ ) down to ten femtofarads ( $1 \mathrm{fF}=10^{-15} \mathrm{~F}$ ) or so.

### The Base-Charging Capacitance $\boldsymbol{C}_{b}$

We now wish to demonstrate that the BJT exhibits an additional capacitance $C_{b}$ due to the injection of minority charges into its base region. Recall that in order to operate a BJT in the forward-active (FA) region we need to establish an excess of minority charge-carriers in its base (this charge, already discussed in connection with Fig. 2.8, is repeated here as Fig. 6.2 for convenience). To find this charge, henceforth denoted as $Q_{F}$ and consisting of electrons in the npn BJT and holes in the pnp BJT, we consider the charge $d Q_{F}$ contained in an infinitesimal slice of thickness $d x$ located at some point $x$ along the horizontal axis, and we then integrate $d Q_{F}$ from 0 to the base width $W_{B}$. For an $n p n$ BJT with emitter area $A_{E}$, we first multiply the volume $A_{E} d x$
image_name:FIGURE 6.2
description:The graph depicted in FIGURE 6.2 illustrates the excess minority carrier distribution in the base region of an npn Bipolar Junction Transistor (BJT) operating in the forward-active mode. This is a 3D plot showing the relationship between position within the base, denoted as \(x\), and the excess electron density \(n_{B}^{\prime}(x)\).

1. **Type of Graph and Function:**
- This is a 3D plot showing a linear relationship between the position \(x\) and the excess minority carrier density \(n_{B}^{\prime}(x)\).

2. **Axes Labels and Units:**
- The horizontal axis represents the position \(x\) within the base, extending from 0 to \(W_{B}\), the base width.
- The vertical axis represents the excess electron density \(n_{B}^{\prime}(x)\).
- There are no specific units provided for these axes in the graph.

3. **Overall Behavior and Trends:**
- The graph shows a linear decrease in excess electron density from \(n_{B}^{\prime}(0)\) at \(x = 0\) to \(n_{B}^{\prime}(W_{B})\) at \(x = W_{B}\).
- The plane formed by the graph represents the integration of the charge \(dQ_{F}\) over an infinitesimal slice of thickness \(dx\) along the base.

4. **Key Features and Technical Details:**
- The graph is shaded to highlight the volume under the curve, which corresponds to the charge \(Q_{F}\) in the base region.
- The infinitesimal slice \(dQ_{F}\) is shown as a small section between \(x\) and \(x + dx\), indicating the integration over the base width.

5. **Annotations and Specific Data Points:**
- The graph is annotated with \(n_{B}^{\prime}(0)\), \(n_{B}^{\prime}(W_{B})\), and \(dQ_{F}\), providing important reference points for understanding the distribution and calculation of the charge \(Q_{F}\).
- The linear decrease in the excess electron density is critical for understanding the behavior of the BJT in the forward-active mode.

FIGURE 6.2 Excess minority carrier distribution in the base region of an npn BJT operating in the forward-active mode.
by the local excess electron density $n_{B}^{\prime}(x)$ to find the number of electrons within the slice, then we multiply by the electron charge $-q$ to find $d Q_{F}$, finally we integrate

$$
Q_{F}=-q A_{E} \int_{0}^{W_{B}} n_{B}^{\prime}(x) d x=-q A_{E} \frac{W_{B} \times\left[n_{B}^{\prime}(0)-n_{B}^{\prime}\left(W_{B}\right)\right]}{2}
$$

where we have used the fact that the integral is just the area of the triangle with base $W_{B}$ and height $n_{B}^{\prime}(0)-n_{B}^{\prime}\left(W_{B}\right)$. We also know that the collector current $I_{C}$ is proportional to the slope of the triangle,

$$
I_{C}=A_{E} J_{n}=q A_{E} D \frac{d n_{B}^{\prime}(x)}{d x}=q A_{E} D_{n}\left(-\frac{n_{B}^{\prime}(0)-n_{B}^{\prime}\left(W_{B}\right)}{W_{B}}\right)
$$

where $D_{n}$ is the electron diffusivity. Eliminating the difference $n_{B}^{\prime}(0)-n_{B}^{\prime}\left(W_{B}\right)$ and simplifying, we get

$$
\begin{equation*}
Q_{F}=\tau_{F} I_{C} \tag{6.3}
\end{equation*}
$$

where

$$
\begin{equation*}
\tau_{F}=\frac{W_{B}^{2}}{2 D_{n}} \tag{6.4}
\end{equation*}
$$

is the mean transit time for electrons in the forward direction, so-called because it represents the average time an electron spends in crossing the base region. (To see why, rewrite as $I_{C}=Q_{F} / \tau_{F}$, and use the definition of current, $I=\Delta Q / \Delta t$, to view $\tau_{F}$ as the time taken by the charge $Q_{F}$ to diffuse through the base.) For monolithic npn BJTs, $\tau_{F}$ is typically in the range of 10 to $100 \mathrm{ps}\left(1 \mathrm{ps}=10^{-12} \mathrm{~s}\right)$. Equation (6.4) applies to the pnp BJT as well, provided we replace $D_{n}$ with $D_{p}$. By Einstein's equations, $D_{p}=\left(\mu_{p} / \mu_{n}\right) D_{n}$. Since $\mu_{p}<\mu_{n}$, it follows that $D_{p}<D_{p}$, indicating that pnp BJTs exhibit longer transit times than npn BJTs, a feature that makes the npn types inherently faster and thus better suited to high-speed applications.

Recall that a change $v_{b e}$ results in the change $i_{c}=g_{m} v_{b e}$, and hence, by Eq. (6.3), in the change $q_{f}=\tau_{F} i_{c}$, that is,

$$
q_{f}=\tau_{F} g_{m} v_{b e}
$$

Whenever a voltage change causes charge redistribution we have the phenomenon of capacitance, so we write $C_{b}=q_{f} / v_{b e}$, that is,

$$
\begin{equation*}
C_{b}=\tau_{F} g_{m}=\tau_{F} \frac{I_{C}}{V_{T}} \tag{6.5}
\end{equation*}
$$

where $C_{b}$ is the base-charging capacitance, also called the diffusion capacitance. Note that $C_{b}$ depends on the bias current $I_{C}$, just like $g_{m}, r_{\pi}$, and $r_{o}$ do.

### The High-Frequency BJT Model

We are now ready to incorporate all above information into a small-signal BJT model that will allow us to investigate the high-frequency behavior of bipolar ICs. The result is shown in Fig. 6.3, where small-signal voltages and currents, now frequency-dependent, are represented in terms of their Laplace's transforms (upper-case letters with lowercase subscripts). Proceeding from right to left, we make the following observations:

- First, we have the substrate capacitance $C_{s}$. Since the substrate of an npn BJT is connected to the MNV, which is a dc potential, the substrate appears as a signal ground in our model. (Oftentimes $C_{s}$ is ignored in order to simplify the calculations.)
- Next, we note the base-collector junction capacitance $C_{\mu}$. This capacitance is most intriguing, for there are situations in which its effect is negligible and it can thus be ignored, whereas there are others in which its role gets magnified because of a phenomenon known as the Miller effect, and thus becomes the dominant capacitance in the circuit.
- In parallel with $r_{\pi}$ we have a capacitance $C_{\pi}$ made up of two components,

$$
\begin{equation*}
C_{\pi}=C_{j e}+C_{b} \tag{6.6}
\end{equation*}
$$

namely, the approximately constant junction component $C_{j e}\left(\cong 2 C_{j e 0}\right)$, and the bias-dependent component $C_{b}\left(=\tau_{F} I_{C} / V_{T}\right)$.

- With reference to Fig. 6.1, we observe that as current enters the base terminal $B$ and progresses to the thin base region separating emitter and collector, where the
image_name:Figure 6.3
description:
[
name: rb, type: Resistor, value: rb, ports: {N1: B, N2: X}
name: rπ, type: Resistor, value: rπ, ports: {N1: X, N2: E}
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: X, Nn: E}
name: Cμ, type: Capacitor, value: Cμ, ports: {Np: X, Nn: C}
name: ro, type: Resistor, value: ro, ports: {N1: C, N2: E}
name: Cs, type: Capacitor, value: Cs, ports: {Np: C, Nn: GND}
name: gmVπ, type: VoltageControlledCurrentSource, ports: {Np: E, Nn: C}
]
extrainfo:The circuit is a high-frequency small-signal model for a BJT, featuring resistors, capacitors, and a voltage-controlled current source. The model includes base resistance (rb), base-emitter resistance (rπ), and output resistance (ro). Capacitances include Cπ and Cμ, with a bypass capacitor Cs connected to ground. The voltage-controlled current source is dependent on Vπ.

FIGURE 6.3 High-frequency small-signal model for the BJT.
central transistor action takes place, it encounters some distributed resistance. This is simply the bulk resistance $r_{b}$ of the moderately-doped $p$-type base region. Being typically on the order of $10^{2} \Omega$ in monolithic BJTs, $r_{b}$ has been ignored so far, since the voltage drop it produces in response to $i_{b}$ is usually negligible compared to that produced by $r_{\pi}$. However, we will find that in general $r_{b}$ cannot be ignored in high-frequency operation, as it limits the dynamics of certain BJT configurations, particularly the CE configuration.

EXAMPLE 6.1 Find the element values of the small-signal model of the BJT of Fig. $6.4 a$ using the data of a typical high-voltage process: $\beta_{0}=150, V_{A}=80 \mathrm{~V}, r_{b}=250 \Omega ; \tau_{F}=$ $200 \mathrm{ps} ; C_{j e 0}=1.0 \mathrm{pF}, \phi_{e}=0.8 \mathrm{~V}, m_{e}=0.33 ; C_{\mu 0}=0.5 \mathrm{pF}, \phi_{c}=0.6 \mathrm{~V}, m_{c}=0.5$; $C_{s 0}=3.0 \mathrm{pF}, \phi_{s}=0.6 \mathrm{~V}$, and $m_{s}=0.5$. Show your final circuit.
image_name:(a)
description:
[
name: 20kΩ, type: Resistor, value: 20kΩ, ports: {N1: 5V, N2: X1}
name: 43kΩ, type: Resistor, value: 43kΩ, ports: {N1: X2, N2: -5V}
name: M1, type: NPN, ports: {C: X1, B: GND, E: X2}
]
extrainfo:The circuit is a common-emitter configuration with a BJT (M1) biased between +5V and -5V. Resistors 20kΩ and 43kΩ are used for biasing.

(a)
image_name:(b)
description:
[
name: R1, type: Resistor, value: 250 Ω, ports: {N1: B, N2: X1}
name: R2, type: Resistor, value: 39 kΩ, ports: {N1: X1, N2: E}
name: C1, type: Capacitor, value: 2.77 pF, ports: {Np: X1, Nn: E}
name: C2, type: Capacitor, value: 0.2 pF, ports: {Np: X1, Nn: C}
name: C3, type: Capacitor, value: 0.8 pF, ports: {Np: C, Nn: GND}
name: R3, type: Resistor, value: 800 kΩ, ports: {N1: C, N2: E}
name: VCCS, type: VoltageControlledCurrentSource, value: Vπ/260 Ω, ports: {Np: C, Nn: E}
]
extrainfo:The circuit is a small-signal model of a BJT amplifier. It includes resistors, capacitors, and a voltage-controlled current source representing the transistor's operation. The nodes are labeled B, X1, E, and C, with the ground connected at GND. The circuit is designed for analyzing the frequency response and gain of the amplifier.

(b)

FIGURE 6.4 (a) Circuit of Example 6.1, and (b) the BJT's small-signal model values.

#### Solution

By inspection, $I_{C} \cong I_{E}=(5-0.7) / 43=0.1 \mathrm{~mA}$. Proceeding as usual, we get $g_{m}=1 /(260 \Omega), r_{\pi}=39 \mathrm{k} \Omega$, and $r_{o}=800 \mathrm{k} \Omega$. We also have

$$
\begin{aligned}
& C_{b}=\tau_{F} g_{m}=\frac{200 \times 10^{-12}}{260} \cong 0.77 \mathrm{pF} \\
& C_{j e} \cong 2 C_{j e 0}=2.0 \mathrm{pF} \\
& C_{\pi}=C_{b}+C_{j e} \cong 2.77 \mathrm{pF}
\end{aligned}
$$

To find $C_{\mu}$ we observe that $V_{C}=5-20 \times 0.1=3 \mathrm{~V}$, so $V_{B C}=V_{B}-V_{C}=$ $0-3=-3 \mathrm{~V}$. To find $C_{s}$, assume the substrate is tied to the MNV ( -5 V ), so $V_{S C}=V_{S}-V_{C}=-5-3=-8 \mathrm{~V}$. Then,

$$
C_{\mu}=\frac{0.5}{\left(1-\frac{-3}{0.6}\right)^{0.5}} \cong 0.2 \mathrm{pF} \quad C_{s}=\frac{3}{\left(1-\frac{-8}{0.6}\right)^{0.5}} \cong 0.8 \mathrm{pF}
$$

The complete small-signal model is shown in Fig. 6.4b.

### Specification of the BJT Frequency Response

It is common practice to specify the frequency capability of a BJT in terms of the transition frequency $f_{T}$, representing the frequency at which its small-signal current gain $|\beta(j f)|$ drops to unity. This frequency is used as a figure of merit for high-speed operation, and it can either be calculated or measured, using the ac concept of Fig. 6.5. Specifically, we apply a small-signal ac current $i_{b}$ to the base, we find the ac current $i_{c}$ with the collector at ac ground, and we take the ratio $\beta=I_{c} / I_{b}$, where $I_{b}$ and $I_{c}$ are the Laplace's transforms of $i_{b}$ and $i_{c}$. Finally, we obtain $f_{T}$ as the frequency such that $\left|\beta\left(f_{T}\right)\right|=1$, or 0 dB .

Turning to the equivalent circuit of Fig. $6.5 b$, we observe that shorting the collector to ground renders $r_{o}$ and $C_{s}$ irrelevant and places $C_{\mu}$ in parallel with $C_{\pi}$. We can thus apply Ohm's law and write

$$
V_{\pi}=\left[r_{\pi} / / \frac{1}{s\left(C_{\pi}+C_{\mu}\right)}\right] I_{b}=\frac{r_{\pi} I_{b}}{1+s r_{\pi}\left(C_{\pi}+C_{\mu}\right)}
$$

where $s$ is the complex frequency. It turns out (see Exercise 6.1 below) that over the frequency range of interest the current fed forward via $C_{\mu}$ is negligible compared to $g_{m} V_{\pi}$, so we approximate

$$
I_{c} \cong g_{m} V_{\pi}=\frac{g_{m} r_{\pi}}{1+s r_{\pi}\left(C_{\pi}+C_{\mu}\right)} I_{b}
$$

Letting $g_{m} r_{\pi} \rightarrow \beta_{0}$ and solving for the ratio $I_{c} / I_{b}$, we get

$$
\beta(s)=\frac{I_{c}}{I_{b}}=\frac{\beta_{0}}{1+s r_{\pi}\left(C_{\pi}+C_{\mu}\right)}
$$

We are primarily interested in the transistor's ac steady-state response, also called the frequency response, so we let $s \rightarrow j \omega$ (or $s \rightarrow j 2 \pi f$ ) and get

$$
\begin{equation*}
\beta(j \omega)=\frac{\beta_{0}}{1+j \omega / \omega_{\beta}} \tag{6.7}
\end{equation*}
$$

where

$$
\begin{equation*}
\omega_{\beta}=\frac{1}{r_{\pi}\left(C_{\pi}+C_{\mu}\right)} \tag{6.8}
\end{equation*}
$$

image_name:Figure 6.5 (a)
description:
[
name: Ib, type: CurrentSource, value: Ib, ports: {Np: B, Nn: GND}
name: M1, type: NPN, ports: {C: GND, B: B, E: GND}
]
extrainfo:The circuit in Figure 6.5 (a) is designed to determine the transistor's frequency response and find the cutoff frequency f_T. It includes a small-signal model with resistors, capacitors, and a voltage-controlled current source to analyze the AC characteristics.
image_name:Figure 6.5 (b)
description:
[
name: Ib, type: CurrentSource, value: Ib, ports: {Np: B, Nn: GND}
name: rb, type: Resistor, value: rb, ports: {N1: B, N2: VI}
name: rπ, type: Resistor, value: rπ, ports: {N1: VI, N2: E}
name: Cμ, type: Capacitor, value: Cμ, ports: {Np: VI, Nn: C}
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: VI, Nn: E}
name: gmVπ, type: VoltageControlledCurrentSource, ports: {Np: C, Nn: E}
name: ro, type: Resistor, value: ro, ports: {N1: C, N2: E}
name: Cs, type: Capacitor, value: Cs, ports: {Np: C, Nn: GND}
name: Ic, type: CurrentSource, value: Ic, ports: {Np: C, Nn: GND}
]
extrainfo:The circuit diagram represents a small-signal equivalent of an NPN transistor amplifier circuit. The diagram includes resistors, capacitors, and a voltage-controlled current source to model the transistor's behavior. The frequency response is analyzed using the parameters provided.

FIGURE 6.5 (a) Ac circuit to find $f_{T}$, and (b) its small-signal equivalent.
image_name:FIGURE 6.6 Bode plot of |β(jω)|
description:The graph is a Bode plot illustrating the magnitude of the current gain, denoted as \(|\beta(j\omega)|\), of a small-signal equivalent NPN transistor amplifier circuit. The plot is represented on logarithmic scales, with the frequency \(\omega\) on the horizontal axis in decades and the magnitude \(|\beta(j\omega)|\) in decibels (dB) on the vertical axis.

Axes Labels and Units:
- **Horizontal Axis (\(\omega\))**: Frequency in decades.
- **Vertical Axis (\(|\beta(j\omega)|\))**: Magnitude in decibels (dB).

Overall Behavior and Trends:
- The plot starts with a constant magnitude \(\beta_0\) at lower frequencies, indicating a flat response.
- As the frequency reaches \(\omega_\beta\), the magnitude begins to decrease.
- The plot shows a downward slope of \(-20 \text{ dB/dec}\), indicating a first-order system roll-off.

Key Features and Technical Details:
- **\(\beta_0\)**: The initial magnitude level at low frequencies.
- **\(\omega_\beta\)**: The pole frequency where the gain starts to decrease, marked by a 3 dB drop from \(\beta_0\).
- **\(-20 \text{ dB/dec}\)**: The slope of the graph, indicating the rate of decline in gain per decade of frequency increase.
- **\(\omega_T\)**: The frequency at which the gain approaches zero, indicating the transition frequency.

Annotations and Specific Data Points:
- The graph includes a marker for the 3 dB point at \(\omega_\beta\), which is a critical point for determining the bandwidth and stability of the amplifier.
- The slope annotation \(-20 \text{ dB/dec}\) is present to highlight the characteristic roll-off rate of the circuit.

FIGURE 6.6 Bode plot of $|\beta(j \omega)|$.
Since the denominator of the $\beta(s)$ vanishes for $s=-\omega_{\beta}$, causing $\beta(s)$ to blow up to infinity, $\omega_{\beta}$ is aptly called pole frequency (see Bode plots in Appendix 6A). The magnitude of the current gain is

$$
\begin{equation*}
|\beta(j \omega)|=\frac{\beta_{0}}{\sqrt{1+\left(\omega / \omega_{\beta}\right)^{2}}} \tag{6.9}
\end{equation*}
$$

and is plotted on logarithmic scales, with $\omega$ in decades (or octaves), and magnitude in decibels. The resulting plot, known as magnitude Bode plot and shown in Fig. 6.6, is of such a common form that it warrants some useful observations:

- For $\omega \ll \omega \beta$, Eq. (6.9) predicts the low-frequency asymptote

$$
\begin{equation*}
|\beta(j \omega)| \rightarrow \beta_{0} \tag{6.10}
\end{equation*}
$$

This is the frequency range over which we have been implicitly operating up to this chapter.

- For $\omega \gg \omega_{\beta}$, Eq. (6.9) predicts the high-frequency asymptote

$$
|\beta(j \omega)| \rightarrow \frac{\beta_{0}}{\omega / \omega_{\beta}}=\frac{\beta_{0} \omega_{\beta}}{\omega}
$$

Defining the gain-bandwidth product $\mathrm{GBP}=|\beta| \times \omega$, we observe that for $\omega \gg \omega_{\beta}$ we have

$$
\begin{equation*}
\mathrm{GBP}=|\beta(j \omega)| \times \omega=\beta_{0} \omega_{\beta} \tag{6.11}
\end{equation*}
$$

that is, the GBP is constant with frequency. In other words, if we pick any point on the high-frequency asymptote and take the product of its ordinate $|\beta(j \omega)|$ by its abscissa $\omega$, we always get the same value, namely, the GBP. In particular, increasing (decreasing) $\omega$ by a decade causes $|\beta(j \omega)|$ to decrease (increase) also by a decade, or 20 dB . Alternatively, an octave increase (or decrease) in $\omega$ results in a 6-dB decrease (or increase) in $|\beta(j \omega)|$.

- The frequency $\omega_{T}$ at which $|\beta(j \omega)|$ drops to unity, or 0 dB , is called the transition frequency because at this frequency the BJT ceases to provide current gain and starts attenuating, so it is no longer useful. By Eq. (6.11) we must have $1 \times \omega_{T}=$ $\beta_{0} \omega_{\beta}$. Using Eq. (6.8), along with $r_{\pi}=\beta_{0} / g_{m}$, we get

$$
\begin{equation*}
\omega_{T}=\frac{g_{m}}{C_{\pi}+C_{\mu}} \tag{6.12a}
\end{equation*}
$$

or, alternatively,

$$
\begin{equation*}
f_{T}=\frac{g_{m}}{2 \pi\left(C_{\pi}+C_{\mu}\right)} \tag{6.12b}
\end{equation*}
$$

In monolithic BJTs $f_{T}$ ranges from a few hundred MHz to tens of GHz .

- For $\omega=\omega_{\beta}$ Eq. (6.9) predicts $\left|\beta\left(j \omega_{\beta}\right)\right|=\beta_{0} / \sqrt{2}=0.707 \beta_{0}$, that is, at $\omega=\omega_{\beta}$ the magnitude $|\beta|$ is down to $70.7 \%$ of its low-frequency value $\beta_{0}$. Since $1 / \sqrt{2}=$ -3 db , the pole frequency $\omega_{\beta}$ is also called the $-3-d B$ frequency.

#### Exercise 6.1

The current fed forward via $C_{\mu}$ in Fig. $6.5 b$ is $I_{\mu}=V_{\pi} /\left[1 /\left(j \omega C_{\mu}\right)\right]$. Using the fact that $C_{\mu} \ll C_{\pi}$, show that for frequencies up to at least $\omega_{T}$ we have $\left|I_{\mu}\right| \ll\left|g_{m} V_{\pi}\right|$, thus justifying the approximation $I_{c} \cong g_{m} V_{\pi}$.

If a certain BJT exhibits $|\beta|=200$ at $f=1 \mathrm{kHz}$ and $|\beta|=10$ at $f=500 \mathrm{MHz}$, find $\beta_{0}, f_{\beta}$, and $f_{T}$.

#### Solution

Since 1 kHz is such a low frequency, the first datum must lie on the low-frequency asymptote, so $\beta_{0}=200$. Since the second datum is much smaller than $\beta_{0}$, it must lie on the high-frequency asymptote, where the GBP is constant. So, $f_{T}=\mathrm{GBP}=$ $10 \times 500=5 \mathrm{GHz}$. Finally, $f_{\beta}=f_{T} / \beta_{0}=5000 / 200=25 \mathrm{MHz}$.

It is instructive to take a closer look at the transition frequency $f_{T}$. Combining Eqs. (6.5), (6.6), and (6.12), we express this frequency in the insightful form

$$
\begin{equation*}
f_{T}=\frac{1 / 2 \pi}{\frac{C_{j e}+C_{\mu}}{I_{C}} V_{T}+\tau_{F}} \tag{6.13}
\end{equation*}
$$

which shows explicitly the dependence on the bias current $I_{C}$. At sufficiently low collector currents $f_{T}$ is dominated by $C_{j e}+C_{\mu}$, and it increases with $I_{C}$. For $I_{C}$ sufficiently high, $f_{T}$ saturates at

$$
\begin{equation*}
f_{T(\max )}=\frac{1}{2 \pi \tau_{F}} \tag{6.14}
\end{equation*}
$$

indicating that $\tau_{F}$ poses the ultimate limit on $f_{T}$. Figure 6.7 shows a decline in $f_{T}$ at high collector currents. This is due to the fact that $\tau_{F}$ increases with high-level injection and other high collector-current effects. ${ }^{2}$
image_name:Figure 6.7
description:The graph in Figure 6.7 is a plot showing the relationship between the transition frequency \( f_T \) and the collector current \( I_C \) for a bipolar junction transistor (BJT). The graph is plotted on a logarithmic scale for the \( I_C \) axis, while the \( f_T \) axis appears to be linear.

**Axes Labels and Units:**
- The horizontal axis represents the collector current \( I_C \) on a logarithmic scale, though specific units are not provided.
- The vertical axis represents the transition frequency \( f_T \), with a significant marker at \( 1/(2\pi\tau_F) \), indicating a critical frequency value.

**Overall Behavior and Trends:**
- At low collector current levels, \( f_T \) increases linearly with \( I_C \). In this region, \( f_T \) is dominated by the combined effect of the junction capacitance \( C_{je} \) and the base-collector capacitance \( C_\mu \).
- As \( I_C \) increases further, \( f_T \) reaches a plateau, indicating a saturation point. This plateau corresponds to \( f_{T(\max)} = 1/(2\pi\tau_F) \), where \( \tau_F \) is the forward transit time.
- At very high collector current levels, \( f_T \) begins to decline due to the increase in \( \tau_F \) caused by high-level injection and other effects.

**Key Features and Technical Details:**
- The graph shows a clear transition from an increasing trend to a saturation region, followed by a decline, illustrating the behavior of \( f_T \) across different collector current levels.
- The plateau at \( 1/(2\pi\tau_F) \) is a critical feature, marking the maximum achievable \( f_T \) due to the limitations imposed by \( \tau_F \).

**Annotations and Specific Data Points:**
- The graph is annotated with regions labeled as "\( f_T \) dominated by \( C_{je} + C_\mu \)" and "\( f_T \) dominated by \( \tau_F \)," highlighting the factors influencing \( f_T \) in different regions of \( I_C \).
- The decline in \( f_T \) at high \( I_C \) levels is also annotated, emphasizing the impact of increased \( \tau_F \) due to high-level injection.

FIGURE 6.7 Dependence of $f_{T}$ on the bias current $I_{C}$.
Using Eq. (6.4), along with Einstein's relation $D_{n}=\mu_{n} V_{T}$, we can also write, for an $n p n$ BJT,

$$
\begin{equation*}
f_{T(\max )}=\frac{1}{\pi} \frac{\mu_{n}}{W_{B}^{2}} V_{T} \tag{6.15}
\end{equation*}
$$

(For a pnp BJT replace $\mu_{n}$ with $\mu_{p}$.) It is apparent that for fast operation a BJT should be fabricated with a very narrow base, and it should be of the npn type as electrons are 2 to 3 times more mobile than holes.

EXAMPLE 6.3 Find $f_{T}$ for the BJT of Example 6.1. How does this compare with $f_{T(\max )}$ ? Which parasitic dominates $f_{T}$ in this example? Which dominates the least?

#### Solution

Equation (6.13) gives

$$
f_{T}=\frac{1 / 2 \pi}{\frac{(2+0.2) 10^{-12}}{0.1} 26+200 \times 10^{-12}}=\frac{1}{2 \pi(520+52+200) 10^{-12}}=206 \mathrm{MHz}
$$

Equation (6.14) gives

$$
f_{T(\max )}=\frac{1}{2 \pi 200 \times 10^{-12}}=796 \mathrm{MHz}
$$

It is apparent that the main culprit in this example is $C_{j e}$. This is followed by $C_{b}$, whereas $C_{\mu}$ has the least impact.

## 6.2 HIGH-FREQUENCY MOSFET MODEL

As depicted in Fig. 6.8, an integrated-circuit (IC) MOSFET presents a variety of internal capacitances: ${ }^{1}$

- The gate-channel oxide capacitance $C_{g c}$, also called the intrinsic capacitance,

$$
\begin{equation*}
C_{g c}=W L C_{o x} \tag{6.16}
\end{equation*}
$$

image_name:FIGURE 6.8
description:The image depicts a cross-sectional view of a saturated monolithic n-channel MOSFET, highlighting various internal capacitances associated with the device. The main components visible in the diagram include the source, gate, and drain, which are essential parts of the MOSFET structure.

1. **Identification of Components and Structure:**
- **Source, Gate, and Drain:** These are labeled prominently at the top of the diagram. The gate is shown as a rectangular block positioned between the source and drain.
- **Substrate:** The MOSFET is built on a p-type substrate, which is indicated at the bottom of the diagram.
- **Channel Width (W):** This is the width of the gate region.
- **Channel Length (L):** This is the distance between the inner edges of the source and drain diffusion regions.

2. **Connections and Interactions:**
- The diagram illustrates several capacitances, which are crucial for the MOSFET's high-frequency performance:
- **C_ov (Overlap Capacitance):** This capacitance exists between the gate and the source/drain due to the overlap of these regions.
- **C_gc (Gate-Channel Capacitance):** This intrinsic capacitance is defined by the oxide layer between the gate and the channel.
- **C_cb (Bulk Capacitance):** This capacitance is between the channel and the bulk (substrate).
- **C_sb (Source-Bulk Capacitance):** This capacitance is between the source and the substrate.
- **C_db (Drain-Bulk Capacitance):** This capacitance is between the drain and the substrate.
- The diagram also notes the overlap length (L_ov) and the difference in channel length (ΔL), which are important for understanding the device's physical dimensions and electrical characteristics.

3. **Labels, Annotations, and Key Features:**
- The diagram includes labels for each capacitance, indicating their respective positions and roles within the MOSFET.
- The substrate is marked with a p- symbol, indicating its doping type.
- Annotations such as L_drawn and ΔL help in understanding the design and manufacturing considerations affecting the MOSFET's performance.

Overall, this diagram provides a detailed visualization of the internal capacitances and structural elements of a high-frequency MOSFET, essential for analyzing its behavior in integrated circuits.

FIGURE 6.8 The capacitances in a saturated monolithic $n$ MOSFET.
where $W$ is the channel width, $L$ is the distance between the inner edges of the source and drain diffusion regions, and $C_{o x}$ is the oxide capacitance per unit area. Recall from Chapter 3 that

$$
\begin{equation*}
C_{o x}=\frac{\varepsilon_{o x}}{t_{o x}}=\frac{34.5}{t_{o x}} \mathrm{fF} / \mu \mathrm{m}^{2} \tag{6.17}
\end{equation*}
$$

where $t_{o x}$ is the oxide thickness, in nm . For instance, a process with $t_{o x}=10 \mathrm{~nm}$ gives $C_{o x}=34.5 / 10=3.45 \mathrm{fF} / \mu \mathrm{m}^{2}$. The gate length as drawn on the mask before fabrication is denoted as $L_{\text {drawn }}$. During fabrication of the $n^{+}$source and drain regions via ion implantation, ions diffuse laterally, resulting in some overlap between the inner edges of these regions and the outer edges of the gate electrode. Denoting the amount of overlap as $L_{o v}$ (in PSpice this is denoted as Ld) we thus have

$$
\begin{equation*}
L=L_{d r a w n}-2 L_{o v} \tag{6.18}
\end{equation*}
$$

Typically, $L_{o v}$ is on the order of 10-20\% of $L_{\text {drawn }}$. (Note that when calculating the device transconductance parameter $k=k^{\prime}(W / L)$ we must use $L$ as given above, and also use the multiplicative factor $\left(1+\lambda v_{D S}\right)$ to account for the channel length modulation $\Delta L$. When referring to a particular fabrication process, engineers use $L$ to denote what is actually $L_{\text {drawn }}$. This is also the convention used by PSpice, where statements of the type $\mathrm{L}=1$. 0u $L d=0.15 \mathrm{u}$ imply a fabrication process with $L_{\text {drawn }}=1.0 \mu \mathrm{~m}$ and $L_{o v}=0.15 \mu \mathrm{~m}$, and thus $L=1-2 \times 0.15=$ $0.7 \mu \mathrm{~m}$. For consistency with previous chapters we shall continue using $L$ to denote the distance between the inner edges of the source and drain regions.)

- The channel-body depletion capacitance $C_{c b}$. In saturation operation, which is the region of greatest interest in analog applications, this capacitance is shielded from the gate by the inversion layer and therefore plays a negligible role.
- The overlap capacitances at the source and drain edges of the gate electrode, each of which is

$$
\begin{equation*}
C_{o v} \cong W L_{o v} C_{o x} \tag{6.19}
\end{equation*}
$$

- The junction capacitances $C_{s b}$ and $C_{d b}$ between the $n^{+}$regions of the source and drain, and the $p^{-}$body, also called bulk or substrate. As we know, these capacitances take on the forms

$$
\begin{equation*}
C_{s b}=\frac{C_{s b 0}}{\left(1+v_{S B} / \phi_{0}\right)^{m}} \quad C_{d b}=\frac{C_{d b 0}}{\left(1+v_{D B} / \phi_{0}\right)^{m}} \tag{6.20}
\end{equation*}
$$

The role played by each of the above capacitances varies with the operating conditions of the MOSFET. ${ }^{2}$ In analog applications the FETs are operated in saturation, where the channel takes on the familiar tapered form (see Fig. 6.8), where $\Delta L$ is the SCL portion extending into the channel side. This asymmetry causes $(2 / 3)$ of $C_{g c}$ to go to the source side, and none to the drain side. ${ }^{2}$ Based on these considerations, the complete high-frequency model of the MOSFET is as in Fig. 6.9. As usual, smallsignal voltages and currents, now frequency-dependent, are represented in terms of their Laplace's transforms (upper-case letters with lower-case subscripts). We shall see that the capacitances playing the biggest roles in the frequency response of a FET are $C_{g s}$ and $C_{g d}$, which take on the forms

$$
\begin{equation*}
C_{g s} \cong \frac{2}{3} W L C_{o x}+W L_{o v} C_{o x} \quad C_{g d} \cong W L_{o v} C_{o x} \tag{6.21}
\end{equation*}
$$

The model includes also the stray capacitance $C_{g b}$, not immediately obvious from the structure of Fig. 6.8, to account for the capacitive coupling between the gate interconnections and the underlying substrate outside the active device area. In today's technology, the various capacitances appearing in a MOSFET's small-signal model are in the femtofarad range $\left(1 \mathrm{fF}=10^{-15} \mathrm{~F}\right)$.
image_name:FIGURE 6.9 Complete high-frequency small-signal model for the MOSFET
description:
[
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: G, Nn: S}
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: G, Nn: D}
name: Cgb, type: Capacitor, value: Cgb, ports: {Np: G, Nn: B}
name: Csb, type: Capacitor, value: Csb, ports: {Np: S, Nn: B}
name: Cdb, type: Capacitor, value: Cdb, ports: {Np: D, Nn: B}
name: gmVgs, type: VoltageControlledCurrentSource, ports: {Np: D, Nn: S}
name: gmbVbs, type: VoltageControlledCurrentSource, ports: {Np: D, Nn: S}
name: ro, type: Resistor, value: ro, ports: {N1: D, N2: S}
]
extrainfo:This is a complete high-frequency small-signal model for a MOSFET, including capacitive couplings and controlled current sources.

FIGURE 6.9 Complete high-frequency small-signal model for the MOSFET.
image_name:FIGURE 6.9 Complete high-frequency small-signal model for the MOSFET
description:
[
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: G, Nn: S}
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: G, Nn: D}
name: g_mVgs, type: VoltageControlledCurrentSource, value: g_mVgs, ports: {Np: D, Nn: S}
name: ro, type: Resistor, value: ro, ports: {N1: D, N2: S}
name: Cdb, type: Capacitor, value: Cdb, ports: {Np: D, Nn: S}
]
extrainfo:This is a high-frequency small-signal model for a MOSFET with capacitive couplings and a voltage-controlled current source representing transconductance. The gate (G), drain (D), and source (S) nodes are connected through various components.

FIGURE 6.10 High-frequency small-signal model for a MOSFET with body and source tied together.

The model of Fig. 6.9 is certainly intimidating for hand calculations-though not necessarily so for PSpice simulations. In the cases in which body and source are tied together, the model simplifies as in Fig. 6.10, where the expression for $C_{g s}$ in Eq. (6.21) is now changed as

$$
\begin{equation*}
C_{g s} \cong \frac{2}{3} W L C_{o x}+W L_{o v} C_{o x}+C_{g b} \tag{6.22}
\end{equation*}
$$

### Specification of the MOSFET Frequency Response

As in the BJT case, the frequency capability of a MOSFET is expressed in terms of the transition frequency $f_{T}$ at which the magnitude of its small-signal current gain drops to unity. As we know, no current flows into the gate terminal at dc. However, as the operating frequency is increased, the stray capacitances associated with the gate terminal draw increasing current, thus decreasing the current gain of the FET. The transition frequency represents a figure of merit for high-frequency operation, and it can either be calculated or measured, using the ac concept of Fig. 6.11a. Specifically, we apply a small-signal ac current $I_{g}$ to the gate terminal, we find the current $I_{d}$ drawn by the FET with the drain at ac ground, we take the ratio $I_{d} / I_{g}$, and we finally determine the frequency $\omega_{T}$ at which $\left|I_{d} / I_{g}\right|=1$, or 0 dB .
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: GND, G: V1}
name: Ig, type: CurrentSource, value: Ig, ports: {Np: G, Nn: GND}
]
extrainfo:The circuit is used to determine the transition frequency f_T of an NMOS transistor by applying a small-signal ac current Ig to the gate terminal and measuring the resulting drain current Id. The drain is at ac ground, making ro and Cdb irrelevant, and placing Cgd in parallel with Cgs.
image_name:(b)
description:
[
name: Ig, type: CurrentSource, value: Ig, ports: {Np: G, Nn: GND}
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: G, Nn: S}
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: G, Nn: D}
name: g_mV_gs, type: VoltageControlledCurrentSource, value: g_mV_gs, ports: {Np: D, Nn: S}
name: ro, type: Resistor, value: ro, ports: {N1: D, N2: S}
name: Cdb, type: Capacitor, value: Cdb, ports: {Np: D, Nn: GND}
]
extrainfo:The circuit diagram (b) represents a small-signal equivalent model for analyzing the transition frequency (f_T) of an NMOS transistor. The drain is shorted to ground, making r_o and C_db irrelevant. C_gd is in parallel with C_gs, and the body and source are tied together, simplifying the analysis.

FIGURE 6.11 (a) Ac circuit to find $f_{T}$, and (b) its small-signal equivalent.

Turning to the equivalent circuit of Fig. 6.11 b , we note that shorting the drain to ground renders $r_{o}$ and $C_{d b}$ irrelevant, and places $C_{g d}$ in parallel with $C_{g s}$. Moreover, with body and source tied together, $C_{g s}$ is given by Eq. (6.20). Applying the generalized Ohm's law,

$$
V_{g s}=\frac{1}{s\left(C_{g s}+C_{g d}\right)} I_{g}
$$

As in BJT case, one can verify that over our frequency range of interest, the current fed forward via $C_{g d}$ is negligible compared to that of the dependent source, so we approximate

$$
I_{d} \cong g_{m} V_{g s}=\frac{g_{m}}{s\left(C_{g s}+C_{g d}\right)} I_{g}
$$

Taking the ratio $I_{d} / I_{g}$ and letting $s \rightarrow j \omega$, we get

$$
\begin{equation*}
\frac{I_{d}}{I_{g}}=\frac{1}{j \omega / \omega_{T}} \tag{6.23}
\end{equation*}
$$

where

$$
\begin{equation*}
\omega_{T}=\frac{g_{m}}{C_{g s}+C_{g d}} \tag{6.24a}
\end{equation*}
$$

or, alternatively,

$$
\begin{equation*}
f_{T}=\frac{g_{m}}{2 \pi\left(C_{g s}+C_{g d}\right)} \tag{6.24b}
\end{equation*}
$$

(Note the formal similarity with Eq. (6.12) of the BJT.) Since $g_{m}$ depends on the bias current $I_{D}$, so does $f_{T}$. Figure 6.12 shows the Bode plot of the MOSFET's current gain. At low frequencies this gain tends to infinity because the gate draws no dc current. But, at $f=f_{T}$, the current entering the gate equals that drawn by the drain. In current monolithic MOSFETs, $f_{T}$ ranges from hundreds of MHz to tens of GHz .
image_name:Figure 6.12 Bode plot of a MOSFET's current gain
description:The graph in Figure 6.12 is a Bode plot illustrating the current gain of a MOSFET. The x-axis represents frequency (ω) on a logarithmic scale, denoted as 'dec' for decades, while the y-axis represents the magnitude of the current gain, |Id/Ig|, measured in decibels (dB).

Overall Behavior and Trends
The plot shows a linear decrease in the current gain with increasing frequency. At lower frequencies, the gain tends to be very high, theoretically approaching infinity, as indicated by the dashed line extending upwards. This reflects the fact that the gate of the MOSFET draws no direct current, leading to a high initial gain.

As the frequency increases, the gain decreases linearly at a rate of -20 dB per decade. This trend continues until the frequency reaches a specific point labeled as ωT, which is the transition frequency. At this point, the current entering the gate equals the current drawn by the drain, marking a significant change in behavior.

Key Features and Technical Details
- **Slope:** The linear decrease is characterized by a slope of -20 dB/decade, indicating a consistent reduction in gain with increasing frequency.
- **Transition Frequency (ωT):** This is a critical point on the graph where the gain is reduced to a level where the gate current equals the drain current. It represents the frequency at which the MOSFET's gain starts to significantly diminish.

Annotations and Specific Data Points
- The plot includes a visual marker for the slope (-20 dB/dec) and the transition frequency (ωT), providing a clear reference for these critical points.

This Bode plot effectively demonstrates the frequency-dependent behavior of a MOSFET's current gain, highlighting the importance of ωT in determining the operational bandwidth of the device.

FIGURE 6.12 Bode plot of a MOSFET's current gain.

#### Exercise 6.2

The current fed forward via $C_{g d}$ in Fig. $6.11 b$ is $I_{g d}=V_{g s} /\left[1 /\left(j \omega C_{g d}\right)\right]$. Exploiting the fact that $C_{g d} \ll C_{g s}$, show that for frequencies up to at least $\omega_{T}$ we have $\left|I_{g d}\right| \ll\left|g_{m} V_{g s}\right|$, thus justifying the approximation $I_{d} \cong g_{m} V_{g s}$.
(a) Assuming $V_{G S}$ has been adjusted for $I_{D}=100 \mu \mathrm{~A}$ in the circuit of Fig. 6.13a, find the element values in the small-signal model of the MOSFET, and show the final circuit. The process parameters are: $k^{\prime}=250 \mu \mathrm{~A} / \mathrm{V}^{2}, C_{o x}=4 \mathrm{fF} / \mu \mathrm{m}^{2}$, $\lambda^{\prime}=0.02 \mu \mathrm{~m} / \mathrm{V}, \gamma=0.5 \mathrm{~V}^{1 / 2}, \phi_{p}=-0.3 \mathrm{~V}, \phi_{0}=0.6 \mathrm{~V}$, and $m=0.5$. The device parameters are $W=10 \mu \mathrm{~m}, L=1.0 \mu \mathrm{~m}, L_{o v}=25 \mathrm{~nm}, C_{s b 0}=C_{d b 0}=10 \mathrm{fF}$, and $C_{g b}=5 \mathrm{fF}$.
(b) Estimate $f_{T}$.
image_name:(a)
description:
[
name: VGS, type: VoltageSource, value: VGS, ports: {Np: VGS, Nn: GND}
name: R1, type: Resistor, value: 10 kΩ, ports: {N1: GND, N2: GND}
name: M1, type: PMOS, ports: {S: V1, D: 3V, G: VGS}
]
extrainfo:The circuit is a PMOS transistor configuration with a current source and various capacitors and resistors for biasing and small-signal modeling. It includes voltage-controlled current sources representing transconductance effects.
image_name:(b)
description:
[
name: C1, type: Capacitor, value: 1fF, ports: {Np: G, Nn: D}
name: C2, type: Capacitor, value: 28fF, ports: {Np: G, Nn: S}
name: C3, type: Capacitor, value: 5fF, ports: {Np: G, Nn: B}
name: C4, type: Capacitor, value: 6fF, ports: {Np: S, Nn: B}
name: C5, type: Capacitor, value: 4fF, ports: {Np: B, Nn: D}
name: G1, type: VoltageControlledCurrentSource, value: Vgs/1.41kΩ, ports: {Np: D, Nn: S}
name: G2, type: VoltageControlledCurrentSource, value: Vbs/7.16kΩ, ports: {Np: D, Nn: S}
name: R2, type: Resistor, value: 500kΩ, ports: {N1: D, N2: S}
]
extrainfo:The circuit represents a PMOS small-signal model with various capacitors and controlled current sources reflecting the transconductance and body effect. The PMOS transistor M1 is connected with its source at node S, drain at node D, gate at node G, and body at node B. The voltage sources and capacitors are connected to these nodes as per the small-signal model configuration.

FIGURE 6.13 (a) Circuit of Example 6.2, and (b) the MOSFET's small-signal model values.

#### Solution

(a) The device transconductance parameter is $k=k^{\prime}(W / L)=0.25(10 / 1)=$ $2.5 \mathrm{~mA} / \mathrm{V}$, and the overdrive voltage is $V_{O V}=\sqrt{2 I_{D} / k}=\sqrt{2 \times 0.1 / 2.5}=$ 0.283 V . Since $V_{S}=10 \times 0.1=1 \mathrm{~V}$ and $V_{D S}=3-1=2 \mathrm{~V}$, it follows that $V_{D S}>V_{O V}$, indicating a saturated FET. We have

$$
\begin{aligned}
\lambda & =\lambda^{\prime} / L=0.02 / 1=0.02 \mathrm{~V}^{-1} \\
r_{o} & =\frac{1}{\lambda I_{D}}=\frac{1}{0.02 \times 0.1}=500 \mathrm{k} \Omega \\
g_{m} & =\sqrt{2 k I_{D}}=\sqrt{2 \times 2.5 \times 0.1}=\frac{1}{1.41 \mathrm{k} \Omega} \\
g_{m b} & =\frac{\gamma g_{m}}{2 \sqrt{V_{S B}+2\left|\phi_{p}\right|}}=\frac{0.5 / 1.41}{2 \sqrt{1+2 \times 0.3}}=\frac{1}{7.16 \mathrm{k} \Omega}
\end{aligned}
$$

#### EXAMPLE 6.4

$$
\begin{aligned}
& C_{s b}=\frac{C_{s b 0}}{\left(1+v_{S B} / \phi_{0}\right)^{m}}=\frac{10}{(1+1 / 0.6)^{0.5}} \cong 6 \mathrm{fF} \\
& C_{d b}=\frac{C_{d b 0}}{\left(1+v_{D B} / \phi_{0}\right)^{m}}=\frac{10}{(1+3 / 0.6)^{0.5}} \cong 4 \mathrm{fF} \\
& C_{g s} \cong \frac{2}{3} W L C_{o x}+W L_{o v} C_{o x}=\frac{2}{3} 10 \times 1 \times 4+10 \times 0.025 \times 4 \cong 27+1=28 \mathrm{fF} \\
& C_{g d}=1 \mathrm{fF}
\end{aligned}
$$

The complete small-signal model is shown in Fig. 6.13b.
(b) Find $f_{T}$ using Eq. (6.24b), but with $C_{g s}$ as in Eq. (6.22), namely, $C_{g s}=27+$ $1+5=33 \mathrm{fF}$. Thus

$$
f_{T}=\frac{g_{m}}{2 \pi\left(C_{g s}+C_{g d}\right)}=\frac{1 /\left(1.41 \times 10^{3}\right)}{2 \pi(33+1) 10^{-15}}=3.31 \mathrm{GHz}
$$

As in the BJT case, it is instructive to take a closer look at $f_{T}$, which we now express as

$$
\begin{equation*}
f_{T}=\frac{\sqrt{2 k I_{D}}}{2 \pi\left(C_{g s}+C_{g d}\right)} \tag{6.25}
\end{equation*}
$$

Clearly, the $f_{T}$ of a MOSFET increases with the square root of the bias current $I_{D}$. By contrast, at sufficiently low bias currents, the $f_{T}$ of a BJT increases in direct proportion to $I_{C}$. This increase continues until it saturates at $f_{T}=1 /\left(2 \pi \tau_{F}\right)$ due to the fact that current in a BJT is the result of minority-charge diffusion. By contrast, the current of a FET is by majority-charge drift, so the limiting factors in this case are exclusively the stray capacitances.

Of all capacitances in a MOSFET, the dominant one is usually the first component in the right-hand side of Eq. (6.21). If we approximate Eq. (6.24b) as $f_{T} \cong$ $g_{m} /\left(2 \pi C_{g s}\right)$ with $C_{g s} \cong(2 / 3) W L C_{o x}$, then

$$
f_{T} \cong \frac{g_{m}}{2 \pi(2 / 3) W L C_{o x}}=\frac{0.75}{\pi} \frac{g_{m}}{W L C_{o x}}
$$

Letting $g_{m}=k V_{O V}=\left[(W / L) \mu_{n} C_{o x}\right] V_{O V}$ and simplifying, we can finally place an upper limit on the $f_{T}$ of a $n$ MOSFET for a given $V_{O V}$ by writing

$$
\begin{equation*}
f_{T(\max )}=\frac{0.75}{\pi} \frac{\mu_{n}}{L^{2}} V_{O V} \tag{6.26}
\end{equation*}
$$

(For a $p$ MOSFET replace $\mu_{n}$ with $\mu_{p}$.) It is apparent that for fast operation a MOSFET should have a very short channel, and it should be of the $n$ type as electrons are 2 to 3 times as mobile as the holes of a $p$-type. Note the striking similarity to the BJT limit of Eq. (6.15), except for the replacement of the (fixed) thermal voltage $V_{T}$ by the (user-imposed) overdrive voltage $V_{O V}$ : the higher $V_{O V}$ the faster the MOSFET is likely to operate.

## 6.3 FREQUENCY RESPONSE OF CE/CS AMPLIFIERS

With the high-frequency models in hand, we are now eager to investigate the frequency response of the most popular transistor configurations. The first to come to mind are the common-emitter (CE) and common-source (CS) configurations, the workhorses of voltage amplification. Their ac equivalents, shown in Figs. $6.14 a$ and $6.15 a$, could refer to any of the discrete CE realizations of Chapters 2 and 3 , so long as the operating frequencies are such that the ac coupling and bypassing capacitors act as ac short circuits. But, they could also represent the differential-mode half-circuits of the dc-coupled EC and SC pairs of Chapter 4. Consequently, the analysis we are about to undertake is quite general.

Replacing the transistors with their high-frequency small-signal models we obtain the ac circuits of $6.14 b$ and $6.15 b$. (For the time being we are deliberately ignoring the output-node parasitics, namely, $C_{s}$ for the BJT and $C_{d b}$ for the FET, so we can focus on the two remaining capacitances and develop valuable intuition in the process. These parasitics will be taken up later in this section.) The two circuits exhibit inevitable differences, but also formal similarities. In fact, using simple circuit transformations, we can reduce them to a common form, and then perform a single analysis on this common circuit to avoid duplication (mercifully, opportunities of this type will arise often as we proceed).

- Turning first to the BJT equivalent of Fig. $6.14 b$, we simplify its left side by applying Thévenin's theorem, and its right side by combining the two parallel resistances into a single one,

$$
\begin{equation*}
V_{i}=\frac{r_{\pi}}{R_{s i g}+r_{b}+r_{\pi}} V_{s i g} \quad R_{1}=\left(R_{s i g}+r_{b}\right) / / r_{\pi} \quad R_{2}=R_{C} / / r_{o} \tag{6.27}
\end{equation*}
$$

After this, the circuit of Fig. $6.14 b$ reduces to that of Fig. 6.16, where the inputnode capacitance $C_{1}$ plays the role of $C_{\pi}$, the feedback capacitance $C_{f}$ plays that of $C_{\mu}$, and $V_{1}$ that of $V_{\pi}$.

- Likewise, turning to the MOS equivalent of Fig. $6.15 b$ and letting

$$
\begin{equation*}
V_{i}=V_{s i g} \quad R_{1}=R_{s i g} \quad R_{2}=R_{D} / / r_{o} \tag{6.28}
\end{equation*}
$$

we reduce it to the same equivalent of Fig. 6.16, where now the input-node capacitance $C_{1}$ plays the role of $C_{g s}$, the feedback capacitance $C_{f}$ plays that of $C_{g d}$, and $V_{1}$ that of $V_{g s}$.
image_name:FIGURE 6.14 (a)
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: V1}
name: NPN Transistor, type: NPN, ports: {C: Vo, B: V1, E: GND}
name: RC, type: Resistor, value: RC, ports: {N1: Vo, N2: GND}
]
extrainfo:This is an AC equivalent circuit of a common-emitter amplifier. The circuit includes a voltage source Vsig, resistors Rsig, rb, rπ, ro, and RC, capacitors Cπ and Cμ, and a voltage-controlled current source gmVπ. The NPN transistor is used for amplification.
image_name:FIGURE 6.14 (b)
description:
[
name: Vsig, type: VoltageSource, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: V1}
name: rb, type: Resistor, value: rb, ports: {N1: V1, N2: Vπ}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vπ, N2: GND}
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: Vπ, Nn: GND}
name: Cμ, type: Capacitor, value: Cμ, ports: {Np: Vx, Nn: Vo}
name: gmVπ, type: VoltageControlledCurrentSource, ports: {Np: Vo, Nn: GND}
name: ro, type: Resistor, value: ro, ports: {N1: Vo, N2: GND}
name: RC, type: Resistor, value: RC, ports: {N1: Vo, N2: GND}
]
extrainfo:This circuit is a high-frequency small-signal model of a CE amplifier. It includes a voltage source Vsig, resistors Rsig, rb, rπ, ro, and RC, capacitors Cπ and Cμ, and a voltage-controlled current source gmVπ. The input is Vsig, and the output is Vo.

FIGURE 6.14 (a) Ac equivalent of the CE amplifier, and (b) its high-frequency small-signal model.
image_name:(a)
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: Vgs}
name: VI, type: VoltageSource, value: VI, ports: {Np: Vgs, Nn: GND}
name: NMOS, type: NMOS, ports: {S: GND, D: Vo, G: Vgs}
name: RD, type: Resistor, value: RD, ports: {N1: Vo, N2: GND}
]
extrainfo:This is a common-source amplifier circuit with an NMOS transistor. The input is connected to Vsig, and the output is taken from Vo. The RD resistor is connected to the output, and Rsig is connected to the input. The NMOS transistor is biased with a voltage source VI.
image_name:(b)
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: Vgs}
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: Vgs, Nn: GND}
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: Vgs, Nn: Vo}
name: gmVgs, type: VoltageControlledCurrentSource, ports: {Np: Vo, Nn: GND}
name: ro, type: Resistor, value: ro, ports: {N1: Vo, N2: GND}
name: RD, type: Resistor, value: RD, ports: {N1: Vo, N2: GND}
]
extrainfo:This circuit is a high-frequency small-signal model of a common-source (CS) amplifier. It includes a voltage source Vsig, resistors Rsig, ro, and RD, capacitors Cgs and Cgd, and a voltage-controlled current source gmVgs. The input is Vsig, and the output is Vo.

FIGURE 6.15 (a) Ac equivalent of the CS amplifier, and (b) its high-frequency small-signal model.

Let us investigate the common circuit of Fig. 6.16, and then adapt our results to the BJT and the FET circuits of Figs. 6.14 and 6.15 with the aid of Eqs. (6.27) and (6.28), respectively. The analysis of this circuit is facilitated further if we take advantage of the Miller effect, to be discussed next. The results, though not exact, will prove quite insightful, as we shall see.
image_name:Figure 6.16
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vi, N2: V1}
name: C1, type: Capacitor, value: C1, ports: {Np: V1, Nn: GND}
name: Cf, type: Capacitor, value: Cf, ports: {Np: V1, Nn: Vo}
name: gmV1, type: VoltageControlledCurrentSource, ports: {Np: Vo, Nn: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a high-frequency small-signal model for a common-source (CS) amplifier, demonstrating the Miller effect with feedback capacitance Cf.

FIGURE 6.16 General model for the CE and CS amplifiers.

### The Miller Effect

With $C_{f}$ absent, the circuit of Fig. 6.16 gives $V_{o}=-g_{m} R_{2} V_{1}$, indicating that we can model its portion from $V_{1}$ to $V_{o}$ with an inverting amplifier as in Fig. 6.17. With $C_{f}$ present there will be some loading at the output of the amplifier; however, actual examples below will reveal that loading is negligible over the frequency range of
image_name:Figure 6.17
description:
[
name: V1, type: VoltageSource, ports: {Np: V1, Nn: GND}
name: Cf, type: Capacitor, value: Cf, ports: {Np: V1, Nn: Vo}
name: -gmR2, type: OpAmp, value: -gmR2, ports: {InP: Vo, InN: GND, Out: Vo}
]
extrainfo:The circuit demonstrates the Miller effect with feedback capacitance Cf. The op-amp has a gain of -gmR2, and the equivalent capacitance CM is calculated as Cf(1 + gmR2).
image_name:Figure 6.17
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
name: Cm, type: Capacitor, value: Cm, ports: {Np: V1, Nn: GND}
]
extrainfo:The circuit illustrates the Miller effect with feedback capacitance Cf, which affects the equivalent impedance Zeq seen by the source V1. The op-amp is modeled with a gain of -gmR2.

FIGURE 6.17 Illustrating the Miller effect.
interest. We now wish to find the equivalent impedance $Z_{e q}$ seen looking toward the right by the $V_{1}$ source of Fig. 6.17. By Ohm's law, the current supplied by $V_{1}$ is

$$
\begin{equation*}
I_{f}=\frac{V_{1}-V_{o}}{1 /\left(s C_{f}\right)} \cong s C_{f}\left[V_{1}-\left(-g_{m} R_{2} V_{1}\right)\right]=s C_{f}\left(1+g_{m} R_{2}\right) V_{1}=s C_{M} V_{1} \tag{6.29}
\end{equation*}
$$

Where

$$
\begin{equation*}
C_{M}=C_{f}\left(1+g_{m} R_{2}\right) \tag{6.30}
\end{equation*}
$$

Letting $Z_{e q}=V_{1} / I_{f}=1 /\left(s C_{M}\right)$, we conclude that the block consisting of the amplifier and its feedback capacitance appears to the $V_{1}$ source as a mere equivalent capacitance $C_{M}$ toward ground. This capacitance is $\left(1+g_{m} R_{2}\right)$ times as large as $C_{f}$ This intriguing phenomenon is called the Miller effect for John M. Miller, who first described it in 1920. The term $\left(1+g_{m} R_{2}\right)$ is called the Miller multiplier and $C_{M}$ the Miller capacitance. In general, $C_{M} \gg C_{f}$

To better understand the Miller effect, let us investigate the process of changing the voltage across a $1-\mathrm{pF}$ capacitor from 0 V to 1 mV , first for the case in which the capacitor is grounded, then for the case in which it is placed in the feedback path of an amplifier with a gain of $-99 \mathrm{~V} / \mathrm{V}$. Let us compare the two cases and comment.

#### Solution

With reference to Fig. $6.18 a$ we note that applying $\Delta V=1 \mathrm{mV}$ causes a charge transfer of $\Delta Q=C \Delta V=10^{-12} \times 10^{-3}=10^{-15} \mathrm{C}=1 \mathrm{fC}$. Consider next the case in which the (initially discharged) capacitor is in the feedback path of the amplifier as in Fig. 6.18b. As we raise the left plate from 0 V to 1 mV , the amplifier will lower the right plate from 0 V to -99 mV , causing a $100-\mathrm{mV}$ total change across the capacitor. The charge transfer is now $\Delta Q=C \Delta V=10^{-2} \times\left(100 \times 10^{-3}\right)=$ 100 fC . Even though the physical capacitance of Fig. $6.18 b$ is still 1 pF , the charge transfer is 100 times that of Fig. 6.18a. Yet, the applied voltage is still 1 mV . So if we regroup the terms as $\Delta Q=\left(10^{-12} \times 100\right) \times 10^{-3}=(100 \mathrm{pF})(1 \mathrm{mV})=$ 100 fC , we can state that things go as if the input source were driving a fictitious capacitance 100 times as large, or $C_{M}=100 \mathrm{pF}$ !
image_name:(a)
description:
[
name: V1, type: VoltageSource, value: 0-to-1 mV, ports: {Np: Vin1, Nn: GND}
name: C1, type: Capacitor, value: 1 pF, ports: {Np: Vin1, Nn: GND}
]
extrainfo:The circuit illustrates the Miller effect, showing how the apparent capacitance increases due to feedback in an amplifier configuration. The effective capacitance is increased from 1 pF to 100 pF.
image_name:(b)
description:
[
name: Voltage Source 1, type: VoltageSource, value: 0-to-1 mV, ports: {Np: Vin1, Nn: GND}
name: C1, type: Capacitor, value: 1 pF, ports: {Np: Vin1, Nn: Out}
name: OpAmp 1, type: OpAmp, value: -99, ports: {InP: GND, InN: Vin1, Out: Out}
]
extrainfo:The circuit illustrates the Miller effect, where the effective capacitance is increased due to the feedback in the op-amp configuration. The original capacitance of 1 pF appears as 100 pF due to the amplification factor of the op-amp.
image_name:Figure 6.18
description:
[
name: V1, type: VoltageSource, value: 0-to-1 mV, ports: {Np: Vin1, Nn: GND}
name: C1, type: Capacitor, value: 100 pF, ports: {Np: Vin1, Nn: GND}
]
extrainfo:This diagram illustrates the Miller effect by showing how the effective capacitance increases due to feedback in the circuit with an operational amplifier. The initial circuit has a 1 pF capacitor, and the presence of the op-amp increases the effective capacitance to 100 pF with a 100 fC charge transfer.

FIGURE 6.18 Quantitative illustration of the Miller effect.

### Analysis Using the Miller Approximation

Thanks to the Miller effect, the circuit of Fig. 6.16 simplifies as in Fig 6.19a. In fact, we can combine the two parallel capacitances into a single total capacitance $C_{t}$,

$$
\begin{equation*}
C_{t}=C_{1}+C_{M} \tag{6.31}
\end{equation*}
$$

and work with the even simpler circuit of Fig. 6.19b. Using the ac voltage divider formula,

$$
V_{o}=-g_{m} V_{1} R_{2}=-g_{m} R_{2} \frac{1 / s C_{t}}{R_{1}+1 / s C_{t}} V_{i}=\frac{-g_{m} R_{2}}{1+s R_{1} C_{t}} V_{i}
$$

so the voltage gain of the circuit is

$$
\begin{equation*}
a(s)=\frac{V_{o}}{V_{i}}=\frac{-g_{m} R_{2}}{1+s R_{1} C_{t}} \tag{6.32}
\end{equation*}
$$

The value of $s$ that makes the denominator vanish and therefore causes $a(s)$ to blow up to infinity is referred to as a pole. This value is

$$
\begin{equation*}
s=-\frac{1}{R_{1} C_{t}} \tag{6.33}
\end{equation*}
$$

indicating a real and negative pole. Letting $s \rightarrow j \omega$ in Eq. (6.32) gives the frequency response, which we express in the standard for of Eq. (6A.1) of Appendix 6A as

$$
\begin{equation*}
a(j \omega)=\frac{a_{0}}{1+j \omega / \omega_{p}} \tag{6.34}
\end{equation*}
$$

where

$$
\begin{equation*}
a_{0}=-g_{m} R_{2} \tag{6.35a}
\end{equation*}
$$

is the value of $a$ in the limit $\omega \rightarrow 0$, aptly called the low-frequency gain, and

$$
\begin{equation*}
\omega_{p}=\frac{1}{R_{1} C_{t}} \tag{6.35b}
\end{equation*}
$$

is called the pole frequency.
image_name:(a)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vi, N2: V1}
name: C1, type: Capacitor, value: C1, ports: {Np: V1, Nn: GND}
name: CM, type: Capacitor, value: CM, ports: {Np: V1, Nn: GND}
name: gmV1, type: VoltageControlledCurrentSource, ports: {Np: Vo, Nn: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit diagram (a) shows a voltage amplifier with a voltage-controlled current source, two capacitors, and two resistors. The input voltage source Vi is connected to a resistor R1 and capacitors C1 and CM. The output is taken across the resistor R2, which is connected to the voltage-controlled current source gmV1. Capacitor Ct is connected from V1 to ground.
image_name:(b)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vi, N2: V1}
name: Ct, type: Capacitor, value: Ct, ports: {Np: V1, Nn: GND}
name: gmV1, type: VoltageControlledCurrentSource, ports: {Np: Vo, Nn: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a simplified equivalent circuit using the Miller approximation. It consists of a voltage source, a resistor, a capacitor, a voltage-controlled current source, and another resistor. The configuration is used to analyze the frequency response and gain of the circuit.

FIGURE 6.19 Equivalent-circuit simplifications using the Miller approximation.
image_name:FIGURE 6.20
description:The graph in FIGURE 6.20 is a Bode plot representing the magnitude gain of a circuit as a function of frequency. The graph is plotted on a logarithmic scale, with the x-axis labeled as frequency (ω) in decades and the y-axis labeled as magnitude |a(jω)| in decibels (dB).

Axes Labels and Units:
- **X-axis:** Frequency (ω) in decades.
- **Y-axis:** Magnitude |a(jω)| in decibels (dB).

Overall Behavior and Trends:
- The plot starts with a flat region at low frequencies where the gain is constant at |a₀| dB.
- As frequency increases, the plot shows a break point at a specific frequency, labeled as ωₚ.
- Beyond this break point, the gain begins to decrease at a rate of -20 dB/decade, indicating a first-order low-pass filter behavior.

Key Features and Technical Details:
- **Initial Gain:** The initial magnitude gain is denoted as |a₀|.
- **Break Point (ωₚ):** At the frequency ωₚ, the gain drops by 3 dB from its initial value, marking the cutoff frequency.
- **Slope:** After ωₚ, the slope of the plot is -20 dB/decade, characteristic of a single-pole roll-off.

Annotations and Specific Data Points:
- The plot includes a marker at the 3 dB point, which is a standard reference for identifying the cutoff frequency.
- A reference line is drawn to indicate the -20 dB/decade slope, emphasizing the linear decrease in gain on the logarithmic scale.

FIGURE 6.20 Magnitude gain plot for the circuit of Fig. 6.19b.

The magnitude Bode plot is shown in Fig. 6.20 (see also Bode plots in Appendix 6A). It is instructive to justify this plot using physical insight. With reference to Fig. 6.19b, we observe that the frequency response is governed by the ac voltage divider formed by $C_{t}$ with $R_{1}$, the equivalent resistance seen by $C_{t}$ itself. The impedance presented by $C_{t}$ is $Z_{t}(j \omega)=1 /\left(j \omega C_{t}\right)$, and depending on how its magnitude $\left|Z_{t}(j \omega)\right|=1 /\left(\omega C_{t}\right)$ compares with $R_{1}$, we have three significant cases:

- At low frequencies we have $\left|Z_{t}(\omega)\right| \gg R_{1}$, indicating that $C_{t}$ approximates an open circuit compared to $R_{1}$. Consequently, $V_{1} \rightarrow V_{i}$, and thus $|a| \rightarrow a_{0}$. This is the situation we have been dealing with before embarking upon the present chapter.
- At high frequencies we have $\left|Z_{t}(\omega)\right| \ll R_{\mathrm{l}}$, indicating that $C_{t}$ now approximates a short circuit compared to $R_{1}$. Consequently, $V_{1} \rightarrow 0$, and $|a|$ rolls off with frequency, as shown.
- The borderline between the two limiting cases occurs when $\omega=\omega_{p}$. Rewriting Eq. (6.35b) as $1 /\left(\omega_{p} C_{t}\right)=R_{1}$, we see that at this frequency we have

$$
\begin{equation*}
\left|Z_{t}\left(\omega_{p}\right)\right|=R_{1} \tag{6.36}
\end{equation*}
$$

We now have a physical interpretation for $\omega_{p}$ : this is the frequency at which the capacitance's impedance equals, in magnitude, the equivalent resistance seen by the capacitance itself. In the MOS case of Fig. 6.15 this resistance is simply $R_{s i g}$, but in the bipolar case of Fig. 6.14 it is $r_{\pi} /\left(R_{s i g}+r_{b}\right)$. A circuit designer will always use physical insight to check the results of mathematical derivations as well as to develop a feel for the workings of the circuit at hand.

- Because of the gain roll-off with frequency, an amplifier is in effect a lowpass filter, this being the reason why $\omega_{p}$ is also variously known as corner frequency, cutoff frequency, or also break frequency. At $\omega=\omega_{p},\left|V_{1}\right|$ is down to $1 / \sqrt{2}(=0.707$, or $-3-\mathrm{dB})$ of its low-frequency value, so $\omega_{p}$ is also called the $-3-d B$ frequency. Since the power of an ac signal is proportional to the square of its magnitude, another name of $\omega_{p}$ is half-power frequency. The gain-bandwidth product is

$$
\begin{equation*}
\mathrm{GBP}=\left|a_{0}\right| \times f_{p} \tag{6.37}
\end{equation*}
$$

We are now ready to apply our results to the specific circuits of Figs. 6.14 and 6.15. Turning first to the common-emitter (CE) case, we combine Eqs. (6.27) and (6.35) to write

$$
\begin{equation*}
a_{0(\mathrm{BJT})}=\left.\frac{V_{o}}{V_{s i g}}\right|_{\omega \rightarrow 0}=\frac{r_{\pi}}{R_{s i g}+r_{b}+r_{\pi}}\left[-g_{m}\left(R_{C} / / r_{o}\right)\right] \tag{6.38a}
\end{equation*}
$$

$$
\begin{equation*}
\omega_{p(\mathrm{BJT})}=\frac{1}{\left\{r_{\pi} / /\left(R_{s i g}+r_{b}\right)\right\} \times\left\{C_{\pi}+C_{\mu}\left[1+g_{m}\left(R_{C} / / r_{o}\right)\right]\right\}} \tag{6.38b}
\end{equation*}
$$

Turning next to the common-source (CS) case, we combine Eqs. (6.28) and (6.35) to write

$$
\begin{gather*}
a_{0(\mathrm{FET})}=\left.\frac{V_{o}}{V_{s i g}}\right|_{\omega \rightarrow 0}=-g_{m}\left(R_{D} / / r_{o}\right)  \tag{6.39a}\\
\omega_{p(\mathrm{FET})}=\frac{1}{R_{s i g}\left\{C_{g s}+C_{g d}\left[1+g_{m}\left(R_{D} / / r_{o}\right)\right]\right\}} \tag{6.39b}
\end{gather*}
$$

To develop a better feel, let us look at some actual examples.

EXAMPLE 6.6 Let the CE amplifier of Fig. 6.14 use a BJT with $\beta_{0}=200, V_{A}=50 \mathrm{~V}, r_{b}=$ $200 \Omega$, and $C_{\mu}=0.5 \mathrm{pF}$. The BJT is biased at $I_{C}=1 \mathrm{~mA}$, where it exhibits $f_{T}=$ 500 MHz . Moreover, let $R_{s i g}=1 \mathrm{k} \Omega$ and $R_{C}=5 \mathrm{k} \Omega$.
(a) Estimate the amplifier's low-frequency gain as well as its $-3-\mathrm{dB}$ frequency. What is the gain-bandwidth product of this amplifier?
(b) Verify that loading of the output node by the feedback capacitance is negligible over the frequency range of interest $\left(f \leq f_{p}\right)$, thus validating the Miller approximation.

#### Solution

(a) Proceeding as usual, we find $g_{m}=1 /(26 \Omega), r_{\pi}=5.2 \mathrm{k} \Omega$, and $r_{o}=50 \mathrm{k} \Omega$. Moreover,

$$
\begin{aligned}
& R_{1}=r_{\pi} / /\left(R_{s i g}+r_{b}\right)=5.2 / /(1+0.2)=0.975 \mathrm{k} \Omega \\
& R_{2}=R_{C} / / r_{o}=5 / / 50=4.55 \mathrm{k} \Omega
\end{aligned}
$$

The low-frequency gain is

$$
\begin{aligned}
a_{0} & =\frac{r_{\pi}}{R_{s i g}+r_{b}+r_{\pi}}\left(-g_{m} R_{2}\right)=\frac{5.2}{1+0.2+5.2}(-4.55 / 0.026) \\
& \cong 0.81 \times(-175)=-142 \mathrm{~V} / \mathrm{V}
\end{aligned}
$$

By Eq. (6.12b) we have

$$
C_{\pi}=\frac{g_{m}}{2 \pi f_{T}}-C_{\mu}=\frac{1 / 26}{2 \pi \times 500 \times 10^{6}}-0.5 \times 10^{-12} \cong 12 \mathrm{pF}
$$

The Miller capacitance is

$$
C_{M}=C_{\mu}\left[1+g_{m}\left(R_{C} / / r_{o}\right)\right]=0.5 \times 10^{-12}[1+175]=88 \mathrm{pF}
$$

indicating a Miller multiplier of 176. The total capacitance is thus

$$
C_{t}=C_{\pi}+C_{M}=12+88=100 \mathrm{pF}
$$

Clearly, the Miller capacitance plays a dominant role in this amplifier. Together, $R_{1}$ and $C_{t}$ create a pole frequency at

$$
f_{p}=\frac{1}{2 \pi R_{1} C_{t}}=\frac{1}{2 \pi \times 975 \times 100 \times 10^{-12}}=1.63 \mathrm{MHz}
$$

The gain-bandwidth product is

$$
\text { GBP }=\left|a_{0}\right| \times f_{p}=142 \times 1.63 \cong 230 \mathrm{MHz}
$$

(b) By Eq. (6.29), the current fed forward via $C_{\mu}$ is maximized at the upper edge of the frequency band of interest, where

$$
I_{f}\left(j f_{p}\right) \cong j 2 \pi f_{p} C_{M} V_{\pi}=j 2 \pi \times 1.63 \times 10^{6} \times 88 \times 10^{-12} V_{\pi}=j V_{\pi} /(1110 \Omega)
$$

On the other hand, the current drawn by the dependent source is

$$
g_{m} V_{\pi}=V_{\pi} /(26 \Omega)
$$

The ratio of the two currents is thus

$$
\frac{\left|I_{f}\left(j f_{p}\right)\right|}{\left|g_{m} V_{\pi}\right|}=\frac{26}{1110} \ll 1
$$

This confirms the validity of the approximation $V_{o} \cong-g_{m} R_{2} V_{\pi}$ for the BJT.

Repeat Example 6.6, but for the CS amplifier of Fig. 6.15. Assume the MOSFET has $k=8 \mathrm{~mA} / \mathrm{V}^{2}, \lambda=1 /(50 \mathrm{~V})$, and $C_{g d}=0.1 \mathrm{pF}$, and is biased at $I_{D}=1 \mathrm{~mA}$, where it exhibits $f_{T}=500 \mathrm{MHz}$. Moreover, let $R_{s i g}=10 \mathrm{k} \Omega$ and $R_{D}=5 \mathrm{k} \Omega$.

#### Solution

(a) Proceeding as usual we find $g_{m}=4 \mathrm{~mA} / \mathrm{V}$ and $r_{o}=50 \mathrm{k} \Omega$, so the lowfrequency gain is

$$
a_{0}=-g_{m}\left(R_{D} / / r_{o}\right)=-4(5 / / 50)=-4 \times 4.55=-18.2 \mathrm{~V} / \mathrm{V}
$$

By Eq. (6.24b) we have

$$
C_{g s}=\frac{g_{m}}{2 \pi f_{T}}-C_{g d}=\frac{4 \times 10^{-3}}{2 \pi 500 \times 10^{6}}-0.1 \times 10^{-12} \cong 1.17 \mathrm{pF}
$$

EXAMPLE 6.7
-

The Miller capacitance is

$$
C_{M}=C_{g d}\left[1+g_{m}\left(R_{D} / / r_{o}\right)\right]=0.1 \times 10^{-12}[1+18.2] \cong 1.92 \mathrm{pF}
$$

indicating a Miller multiplier of 19.2. (In general, this multiplier is lower in FETs than in BJTs because a FET has notoriously a lower $g_{m}$.) The total capacitance is thus

$$
C_{t}=C_{g s}+C_{M}=1.17+1.92=3.09 \mathrm{pF}
$$

so the Miller capacitance plays a dominant role also in this amplifier. The resistance seen by $C_{t}$ is now $R_{s i g}$. Together, they create a pole frequency at

$$
f_{p}=\frac{1}{2 \pi R_{s i g} C_{t}}=\frac{1}{2 \pi \times 10^{4} \times 3.09 \times 10^{-12}}=5.15 \mathrm{MHz}
$$

The gain-bandwidth product is

$$
\mathrm{GBP}=\left|a_{0}\right| \times f_{p}=18.2 \times 5.2 \cong 94 \mathrm{MHz}
$$

(b) By Eq. (6.29), the current fed forward via $C_{g d}$ at the upper edge of the frequency band of interest is

$$
I_{f}\left(j f_{p}\right) \cong j 2 \pi f_{p} C_{M} V_{g s}=j 2 \pi \times 5.2 \times 10^{6} \times 1.92 \times 10^{-12} V_{g s}=j V_{g s} /(16 \mathrm{k} \Omega)
$$

whereas the current drawn by the dependent source is

$$
g_{m} V_{g s}=V_{g s} /(0.25 \mathrm{k} \Omega)
$$

Consequently, the ratio of the two currents is

$$
\frac{\left|I_{f}\left(j f_{p}\right)\right|}{\left|g_{m} V_{g s}\right|}=\frac{0.25}{16} \ll 1
$$

thus confirming the validity of the approximation $V_{o} \cong-g_{m} R_{2} V_{g s}$ for the MOSFET.

### A More Accurate Analysis

To assess the accuracy of the Miller approximation and also to gain additional insight into circuit behavior, let us perform the exact analysis of the small-signal circuit of Fig. 6.16. Since we are at it, we may as well generalize by including also the outputnode capacitance $C_{2}$, as in Fig. 6.21. As we know, the collector of a monolithic BJT exhibits the collector-to-substrate capacitance $C_{s}$, and the drain of a FET exhibits the drain-to-body capacitance $C_{d b}$. Moreover, in actual application, the output node is likely to be loaded by an external capacitance $C_{L}$, so, in general, $C_{2}=C_{s}+C_{L}$ for the BJT, and $C_{2}=C_{d b}+C_{L}$ for the FET.

Applying KCL at the node to the left of $C_{f}$ gives

$$
\frac{V_{i}-V_{1}}{R_{1}}=\frac{V_{1}}{1 /\left(s C_{1}\right)}+\frac{V_{1}-V_{o}}{1 /\left(s C_{f}\right)}
$$

image_name:FIGURE 6.21
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vi, N2: V1}
name: C1, type: Capacitor, value: C1, ports: {Np: V1, Nn: GND}
name: Cf, type: Capacitor, value: Cf, ports: {Np: V1, Nn: Vo}
name: gmV1, type: VoltageControlledCurrentSource, value: gmV1, ports: {Np: Vo, Nn: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vo, N2: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: Vo, Nn: GND}
]
extrainfo:The circuit is an AC small-signal model for analyzing common-emitter/common-source amplifiers with feedback capacitance Cf. It includes input voltage Vi, resistors R1 and R2, capacitors C1, Cf, and C2, and a voltage-controlled current source gmV1.

FIGURE 6.21 Ac circuit for a more accurate analysis of the CE/CS amplifiers.

Likewise, KCL at the node to the right of $C_{f}$ gives

$$
\frac{V_{1}-V_{o}}{1 / s C_{f}}=g_{m} V_{1}+\frac{V_{o}}{R_{2}}+\frac{V_{o}}{1 / s C_{2}}
$$

Eliminating $V_{1}$ and solving for the ratio $V_{o} / V_{i}$ we get, after a bit of algebraic labor,

$$
\begin{align*}
a(s) & =\frac{V_{o}}{V_{i}} \\
& =\frac{\left(-g_{m} R_{2}\right) \times\left(1-s C_{f} / g_{m}\right)}{1+s\left\{R_{1}\left[C_{1}+C_{f}\left(1+g_{m} R_{2}\right)\right]+R_{2}\left(C_{f}+C_{2}\right)\right\}+s^{2} R_{1} R_{2}\left(C_{1} C_{f}+C_{1} C_{2}+C_{f} C_{2}\right)} \tag{6.40}
\end{align*}
$$

The denominator is a quandratic polynomial in $s$, so $a(s)$ admits two poles. Denoting the corresponding pole frequencies as $\omega_{1}$ and $\omega_{2}$, we express gain more concisely in the standard form of Eq. (6A.1) in the Appendix,

$$
\begin{equation*}
a(s)=a_{0} \frac{1-s / \omega_{0}}{\left(1+s / \omega_{1}\right)\left(1+s / \omega_{2}\right)} \tag{6.41}
\end{equation*}
$$

where

$$
\begin{equation*}
a_{0}=-g_{m} R_{2} \tag{6.42}
\end{equation*}
$$

is the familiar low-frequency gain, and

$$
\begin{equation*}
\omega_{0}=\frac{g_{m}}{C_{f}} \tag{6.43}
\end{equation*}
$$

is the zero frequency of $a(s)$. Physically, the current fed forward via $C_{f}$ at this frequency equals the current drawn by the dependent source, resulting in a net current of zero through the parallel combination of $R_{2}$ and $C_{2}$. Consequently, $V_{o}$ drops to zero, implying a gain of zero at this frequency. As a physical check, when $V_{o}=0$ we have $I_{f}=\left(V_{\pi}-0\right) /\left(1 / s C_{f}\right)=s C_{f} V_{\pi}$, so imposing $s C_{f} V_{\pi}=g_{m} V_{\pi}$ yields $s=g_{m} / C_{f}$ In the $s$ plane this zero is located on the positive real axis. Note that for $\omega>\omega_{0}$ the current through $C_{f}$ exceeds that of the dependent source, indicating gain-polarity reversal. This provides a physical justification for the presence of the negative sign in
the numerator of Eq. (6.41); combined with the negative sign of Eq. (6.42), it causes gain to become positive for $\omega>\omega_{0}$. By Eqs. (6.12) and (6.24), $\omega_{0} \gg \omega_{T}$.

We now wish to derive expressions for the pole frequencies $\omega_{1}$ and $\omega_{2}$. Based on the Miller approximation, we expect $\omega_{1}$ to be close to $\omega_{p}$, and $\omega_{2}$ to be much higher than $\omega_{p}$. Consequently, expanding the denominator of Eq. (6.41) and anticipating $\omega_{2} \gg \omega_{1}$, we write

$$
\begin{equation*}
a(s)=a_{0} \frac{1-s / \omega_{0}}{1+s\left(1 / \omega_{1}+1 / \omega_{2}\right)+s^{2} /\left(\omega_{1} \omega_{2}\right)} \cong a_{0} \frac{1-s / \omega_{0}}{1+s / \omega_{1}+s^{2} /\left(\omega_{1} \omega_{2}\right)} \tag{6.44}
\end{equation*}
$$

Equating the coefficients of $s$ in the denominators of Eqs. (6.40) and (6.44), we readily find

$$
\begin{equation*}
\omega_{1}=\frac{1}{R_{1}\left[C_{1}+C_{f}\left(1+g_{m} R_{2}+R_{2} / R_{1}\right)\right]+R_{2} C_{2}} \tag{6.45}
\end{equation*}
$$

We observe that in the limit $C_{2} \rightarrow 0$ this expression differs from that of $\omega_{p}$ derived earlier only in the denominator term $R_{2} / R_{1}$. But, $R_{2} / R_{1} \ll g_{m} R_{2}$, so $\omega_{1} \cong \omega_{p}$, confirming that the Miller approximation is an excellent one, considering also how quicker is its derivation. Likewise, equating the coefficients of $s^{2}$ in the denominators of Eqs. (6.40) and (6.44),

$$
\begin{equation*}
\omega_{2}=\frac{1}{R_{1} R_{2}\left(C_{1} C_{f}+C_{1} C_{2}+C_{f} C_{2}\right) \omega_{1}} \tag{6.46}
\end{equation*}
$$

The next examples will confirm that $\omega_{2} \gg \omega_{1}$, indicating that the frequency response of Fig. 6.20, though approximate, provides a good indication of the actual response over the frequency range of interest.

EXAMPLE 6.8 (a) Find $f_{0}, f_{1}$, and $f_{2}$ for the CE amplifier of Example 6.6. Compare with the example and comment.
(b) Repeat, but taking into account a substrate capacitance $C_{s}=1 \mathrm{pF}$.
(c) Verify with PSpice.

#### Solution

(a) For the BJT, Eq. (6.43) predicts a zero frequency at

$$
f_{0}=\frac{g_{m}}{2 \pi C_{\mu}}=\frac{1 / 2 \pi}{26 \times 0.5 \times 10^{-12}} \cong 12 \mathrm{GHz}
$$

Moreover, with $R_{1}=975 \Omega, R_{2}=4.55 \mathrm{k} \Omega$, and $C_{2}=0$, Eqs. (6.45) and (6.46) predict pole frequencies at

$$
\begin{aligned}
f_{1} & =\frac{1 / 2 \pi}{R_{1}\left[C_{\pi}+C_{\mu}\left(1+g_{m} R_{2}+R_{2} / R_{1}\right)\right]} \\
& =\frac{1 / 2 \pi}{975[12+0.5(1+175+4.55 / 0.975)] 10^{-12}}=1.56 \mathrm{MHz}
\end{aligned}
$$

and

$$
\begin{aligned}
f_{2} & =\frac{1 /(2 \pi)^{2}}{R_{1} R_{2} C_{\pi} C_{\mu} f_{1}} \\
& =\frac{1 /(2 \pi)^{2}}{975 \times 4.55 \times 10^{3} \times 12 \times 10^{-12} \times 0.5 \times 10^{-12} \times 1.56 \times 10^{6}} \\
& \cong 600 \mathrm{MHz}
\end{aligned}
$$

Both $f_{0}$ and $f_{2}$ are well above $f_{1}$, so they are of irrelevant consequence in this example and can be ignored. The first pole frequency $\left(f_{1}=1.56 \mathrm{MHz}\right)$ is slightly lower than that predicted via the Miller approximation $\left(f_{p}=1.63 \mathrm{MHz}\right)$, indicating that the Miller estimate suffices for all practical pusposes.
(b) Recalculating with $C_{2}=C_{s}=1 \mathrm{pF}$ we get $f_{0}=12 \mathrm{GHz}, f_{1}=1.55 \mathrm{MHz}$, and $f_{2} \cong 1.3 \mathrm{GHz}$. The effect of $C_{s}$ is negligible in this example.
image_name:Figure 6.22
description:
[
name: Vsig, type: VoltageSource, value: 1 Vac, 0 Vdc, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: 1.0 kΩ, ports: {N1: Vsig, N2: X1}
name: rb, type: Resistor, value: 200 Ω, ports: {N1: X1, N2: V2}
name: rπ, type: Resistor, value: 5.2 kΩ, ports: {N1: V2, N2: GND}
name: Cπ, type: Capacitor, value: 12 pF, ports: {Np: V2, Nn: GND}
name: Cμ, type: Capacitor, value: 0.5 pF, ports: {Np: V2, Nn: Vo}
name: g_m, type: VoltageControlledCurrentSource, value: 38.5 mA/V, ports: {Np: V2, Nn: Vo}
name: ro, type: Resistor, value: 50 kΩ, ports: {N1: Vo, N2: GND}
name: Cs, type: Capacitor, value: 1 pF, ports: {Np: Vo, Nn: GND}
name: RC, type: Resistor, value: 5 kΩ, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a Common Emitter (CE) amplifier with a gain of approximately 43.057 dB or 142 V/V. The -3 dB frequency is around 1.522 MHz.

FIGURE 6.22 PSpice circuit to display the gain of the CE amplifier of Example 6.8.
image_name:Figure 6.23
description:The graph in Figure 6.23 is a Bode plot representing the gain of a Common Emitter (CE) amplifier. The x-axis is labeled 'Frequency f (Hz)' and is plotted on a logarithmic scale ranging from $10^4$ to $10^9$ Hz. The y-axis is labeled 'Gain a (dB)' and spans from -20 dB to 40 dB.

The plot displays two curves representing the gain for different values of the capacitor $C_s$: one for $C_s = 0$ and another for $C_s = 1$ pF. Both curves start with a high gain of approximately 43 dB at lower frequencies.

The gain remains relatively constant up to around $10^6$ Hz, after which it begins to decrease. The -3 dB cutoff frequency, where the gain drops by 3 dB from its maximum value, is indicated at approximately 1.522 MHz (or $1.522 \times 10^6$ Hz).

For frequencies beyond $10^6$ Hz, the gain decreases more rapidly, with the $C_s = 1$ pF curve showing a slightly faster decline compared to the $C_s = 0$ curve. This indicates the minimal role played by the capacitor $C_s$ in affecting the amplifier's gain at these frequencies.

The plot confirms the amplifier's gain of approximately 43.057 dB or 142 V/V as calculated and discussed in the context. The annotations highlight the different curves for the two capacitor values, emphasizing the slight impact of $C_s$ on the gain at higher frequencies.

FIGURE 6.23 Gain plot of the circuit of Fig. 6.22.
(c) Using the PSpice circuit of Fig. 6.22 we get the gain plot of Fig. 6.23. Using the cursor facilty, we find $\left|a_{0}\right|=43.057 \mathrm{~dB}$, or $142 \mathrm{~V} / \mathrm{V}$, and $f_{-3 \mathrm{~dB}}=$ 1.522 MHz , in agreement with the calculations. The plot confirms the minimal role played by $C_{s}$ in this example.

Remark: an IC designer will simulate an amplifier using a PSpice model for the transistor. But here, for pedagogical purposes, it is more convenient to work with the homebrew model depicted in Fig. 6.22.

#### Exercise 6.3

Find $f_{0}, f_{1}$, and $f_{2}$ for the CS amplifier of Example 6.7, if $C_{d b}=0.1 \mathrm{pF}$. Compare with the results obtained there and comment.
Ans. $f_{0}=6.4 \mathrm{GHz}, f_{1}=5.0 \mathrm{MHz}$, and $f_{2} \cong 1 \mathrm{GHz} ; f_{p}=5.15 \mathrm{MHz}\left(\cong f_{1}\right)$.

## 6.4 FREQUENCY RESPONSE OF DIFFERENTIAL AMPLIFIERS

Given the importance of the differential amplifier as an analog building block, it is only appropriate that we investigate its frequency response in detail. If the frequency analysis of a single-transistor stage may be laborious, that of a transistor pair can become exceedingly complex. Mercifully, the use of the half-circuit concepts introduced in Chapter 4 simplifies our task dramatically while providing precious insight with a minimum of mathematical manipulations. (Physical insight much more than formulas is what guides IC designers in their daily endeavors.)

As we know, the role of a differential amplifier is to magnify the voltage difference between two signals irrespective of their common-mode component. The common-mode rejection ratio

$$
\begin{equation*}
\mathrm{CMRR}=\left|\frac{a_{d m}(j f)}{a_{c m}(j f)}\right| \tag{6.47}
\end{equation*}
$$

constitutes a figure of merit of the differential amplifier, and as such it should be as large as possible (ideally, infinite). In practice we will find that the CMRR, however high initially, deteriorates with frequency because so do both the differential-mode gain $a_{d m}(j f)$ and the common-mode gain $a_{c m}(j f)$.

### Resistive-Loaded Differential Amplifiers

Figure 6.24 shows the basic emitter-coupled (EC) and source-coupled (SC) pairs. Recall from Chapter 4 that $a_{c m}$ is inversely proportional to the equivalent resistance $R_{E E}$ (or $R_{S S}$ ) presented to the pair by the external biasing circuitry, so in order to maximize the CMRR a designer will strive to maximize $R_{E E}$ (or $R_{S S}$ ). To this end, the current sinking transistor $Q_{3}$ (or $M_{3}$ ), whose biasing details have been omitted for simplicity, is likely to be part of a very high output-resistance topology such as the Wilson or the cascode types. As a rule, the impedance $Z_{E E}$ (or $Z_{S S}$ ) presented to the EC (or SC) pair consists of a resistive component $R_{E E}$ (or $R_{S S}$ ) in parallel with a capacitive component $C_{E E}$ (or $C_{S S}$ ). As we are about to see, it is precisely the capacitive component that causes $a_{c m}(j f)$, and thus CMRR, to deteriorate with frequency.

To investigate the CMMR, we first need to find the differential-mode and common-mode gains $a_{d m}(j f)$ and $a_{c m}(j f)$. We shall do so using the differential-mode and common-mode half circuits. Though the analysis will be carried out for the
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: Vo+, B: V1, E: P}
name: Q2, type: NPN, ports: {C: Vo-, B: Vi2, E: P}
name: Q3, type: NPN, ports: {C: P, B: LOAD, E: VEE}
name: RC1, type: Resistor, value: RC, ports: {N1: VCC, N2: Vo+}
name: RC1, type: Resistor, value: RC, ports: {N1: VCC, N2: Vo-}
name: RB, type: Resistor, value: RB, ports: {N1: Vi1, N2: V1}
name: Vi1, type: VoltageSource, value: Vi1, ports: {Np: Vi1, Nn: GND}
name: Vi2, type: VoltageSource, value: Vi2, ports: {Np: Vi2, Nn: GND}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: VEE, type: VoltageSource, value: VEE, ports: {Np: VEE, Nn: GND'}
]
extrainfo:The circuit is a differential amplifier using NPN transistors with resistive loads. It includes a common-mode feedback mechanism through Q3 and ZEE. The input signals are Vi1 and Vi2, and the output is Vo.
image_name:(b)
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: Vo+, G: V1}
name: M2, type: PMOS, ports: {S: VDD, D: Vo-, G: V2}
name: M3, type: PMOS, ports: {S: VSS, D: P, G: LOAD}
name: RD1, type: Resistor, value: RD, ports: {N1: VDD, N2: Vo+}
name: RD2, type: Resistor, value: RD, ports: {N1: VDD, N2: Vo-}
name: RG1, type: Resistor, value: RG, ports: {N1: Vi1, N2: V1}
name: RG2, type: Resistor, value: RG, ports: {N1: Vi2, N2: V2}
name: Vi1, type: VoltageSource, value: Vi1, ports: {Np: Vi1, Nn: GND}
name: Vi2, type: VoltageSource, value: Vi2, ports: {Np: Vi2, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: VSS, type: VoltageSource, value: VSS, ports: {Np: VSS, Nn: GND}
]
extrainfo:This circuit diagram (b) represents a differential amplifier using PMOS transistors. The circuit includes two PMOS transistors (M1 and M2) forming the differential pair, with a third PMOS (M3) acting as a current source. The resistors RD are the load resistors, and RG are the gate resistors. The circuit is powered by VDD and VSS voltage sources, and the inputs are provided by Vi1 and Vi2.

FIGURE 6.24 (a) The EC and (b) SC pairs with resistive loads.

EC pair, the results are readily adapted to the SC pair as well. To find $a_{d m}(j f)$ we use the half-circuit equivalent of Fig. 6.25. This is the familiar CE configuration, whose gain contains a dominant pole due primarily to the Miller capacitance. Adapting Eq. (6.45),

$$
\begin{equation*}
f_{p(\mathrm{dm})} \cong \frac{1 / 2 \pi}{\left[\left(R_{B}+r_{b}\right) / / r_{\pi}\right] \times\left\{C_{\pi}+C_{\mu}\left[1+g_{m}\left(R_{C} / / r_{o}\right)\right]\right\}+\left(R_{C} / / r_{o}\right) \times C_{s}} \tag{6.48}
\end{equation*}
$$

To find $a_{c m}(j f)$ we use the half-circuit equivalent of Fig. 6.26. Note that as we split the impedance $Z_{E E}$ into two identical parts, $R_{E E}$ must be doubled to give $\left(2 R_{E E}\right) / /\left(2 R_{E E}\right)=$ $R_{E E}$, whereas $C_{E E}$ must be halved to give $\left(C_{E E} / 2\right) / /\left(C_{E E} / 2\right)=C_{E E} / 2+C_{E E} / 2=C_{E E}$.
image_name:FIGURE 6.25 (a)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vid/2, Nn: GND}
name: RB, type: Resistor, value: RB, ports: {N1: Vid/2, N2: Vb}
name: Q1, type: NPN, ports: {C: Vout, B: Vb, E: GND}
name: RC, type: Resistor, value: RC, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a differential-mode half circuit with an NPN transistor Q1. It includes a voltage source Vi, resistors RB, RC, rb, rπ, and ro, capacitors Cμ, Cπ, and Cs, and a voltage-controlled current source gmVπ. The circuit is designed to analyze the high-frequency small-signal equivalent of a differential amplifier.
image_name:FIGURE 6.25 (b)
description:
[
name: VI, type: VoltageSource, value: VI, ports: {Np: Vid/2, Nn: GND}
name: RB, type: Resistor, value: RB, ports: {N1: Vid/2, N2: V1}
name: rb, type: Resistor, value: rb, ports: {N1: V1, N2: Vπ}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vπ, N2: GND}
name: Cμ, type: Capacitor, value: Cμ, ports: {Np: Vx, Nn: Vod/2}
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: Vπ, Nn: GND}
name: gmVπ, type: VoltageControlledCurrentSource, ports: {Np: Vod/2, Nn: GND}
name: ro, type: Resistor, value: ro, ports: {N1: Vod/2, N2: GND}
name: Cs, type: Capacitor, value: Cs, ports: {Np: Vod/2, Nn: GND}
name: RC, type: Resistor, value: RC, ports: {N1: Vod/2, N2: GND'}
]
extrainfo:The circuit is a high-frequency small-signal equivalent of a differential-mode half circuit. It includes a voltage source, resistors, capacitors, and a voltage-controlled current source. The circuit models the behavior of a transistor in a differential amplifier configuration with feedback and parasitic capacitances.

FIGURE 6.25 (a) Differential-mode half circuit, and (b) its high-frequency small-signal equivalent.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: Voc, B: V1, E: V2}
name: RB, type: Resistor, value: RB, ports: {N1: Vic, N2: V1}
name: RC, type: Resistor, value: RC, ports: {N1: Voc, N2: GND}
name: 2REE, type: Resistor, value: 2REE, ports: {N1: V2, N2: GND}
name: CEE/2, type: Capacitor, value: CEE/2, ports: {Np: V2, Nn: GND}
]
extrainfo:The circuit is a high-frequency small-signal equivalent of a differential-mode half circuit. It models the behavior of a transistor in a differential amplifier configuration with feedback and parasitic capacitances. The voltage-controlled current source represents the transistor's transconductance.
image_name:(b)
description:
[
'name': 'RB', 'type': 'Resistor', 'value': 'RB', 'ports': {'N1': 'Vic', 'N2': 'V1'
'name': 'RC', 'type': 'Resistor', 'value': 'RC', 'ports': {'N1': 'Voc', 'N2': 'V2'
'name': '2REE', 'type': 'Resistor', 'value': '2REE', 'ports': {'N1': 'V2', 'N2': 'GND'
'name': 'CEE/2', 'type': 'Capacitor', 'value': 'CEE/2', 'ports': {'Np': 'V2', 'Nn': 'GND'
'name': 'Vic', 'type': 'VoltageSource', 'value': 'Vic', 'ports': {'Np': 'Vic', 'Nn': 'GND'
'name': 'rb', 'type': 'Resistor', 'value': 'rb', 'ports': {'N1': 'V1', 'N2': 'V3'
'name': 'rπ', 'type': 'Resistor', 'value': 'rπ', 'ports': {'N1': 'V3', 'N2': 'V2'
'name': 'Cπ', 'type': 'Capacitor', 'value': 'Cπ', 'ports': {'Np': 'V3', 'Nn': 'V2'
'name': 'Cμ', 'type': 'Capacitor', 'value': 'Cμ', 'ports': {'Np': 'V3', 'Nn': 'Voc'
'name': 'gmVπ', 'type': 'VoltageControlledCurrentSource', 'ports': {'Np': 'V3', 'Nn': 'V2'
'name': 'ro', 'type': 'Resistor', 'value': 'ro', 'ports': {'N1': 'Voc', 'N2': 'V2'
'name': 'CS', 'type': 'Capacitor', 'value': 'CS', 'ports': {'Np': 'Voc', 'Nn': 'V2'
]
extrainfo:The circuit is a high-frequency small-signal equivalent of a differential-mode half circuit. It models a transistor in a differential amplifier configuration with feedback and parasitic capacitances. It includes a voltage source, resistors, capacitors, and a voltage-controlled current source.

FIGURE 6.26 (a) Common-mode half circuit, and (b) its high-frequency small-signal equivalent.

The circuit of Fig. 6.26 is the familiar CE-ED configuration, but with degeneration now provided by the impedance $2 Z_{E E}=\left(2 R_{E E}\right) / /\left[1 / s\left(C_{E E} / 2\right)\right]$. At sufficiently low frequencies $C_{E E} / 2$ acts as an open circuit compared to $2 R_{E E}$, so $a_{c m}(\mathrm{ff})$ starts out low and CMRR starts out high. As the operating frequency is increased, the impedance provided by $C_{E E} / 2$ decreases, causing $Z_{E E}$ to decrease as well. This, in turn, causes $a_{c m}(j f)$ to increase and CMRR to decrease with frequency. Clearly, $a_{c m}(j f)$ exhibits a zero frequency $f_{z(\mathrm{~cm})}$. This is the frequency at which the impedance provided by $C_{E E} / 2$ equals, in magnitude, $2 R_{E E}$. This condition yields the familiar result $f_{z(\mathrm{~cm})}=$ $1 /\left[2 \pi\left(2 R_{E E}\right)\left(C_{E E} / 2\right)\right]$, or

$$
\begin{equation*}
f_{z(c m)}=\frac{1}{2 \pi R_{E E} C_{E E}} \tag{6.49}
\end{equation*}
$$

Since $R_{E E}$ is usually quite high, $f_{z(\mathrm{~cm})}$ is usually lower than $f_{p(\mathrm{dm})}$. We can thus state the following:

- The CMRR starts out high for $f \ll f_{z(\mathrm{~cm})}$.
- At $f=f_{z(\mathrm{~mm})}$ the CMRR begins to roll off with frequency. Clearly, the zero frequency of $a_{c m}$ is a pole frequency for CMRR.
- For $f_{z(\mathrm{~cm})}<f<f_{p(\mathrm{dm})}$ the CMRR rolls off with $f$ at a rate of $-20 \mathrm{db} / \mathrm{dec}$.
- At $f=f_{p(\mathrm{dm})}$ the CMRR picks up an additional roll-off rate of $-20-\mathrm{dB} / \mathrm{dec}$. Clearly, the first pole frequency of $a_{d m}$ is a second pole frequency for CMRR.
- For $f>f_{p(\mathrm{dm})}$ the CMRR rolls off with $f$ at a rate of $-40 \mathrm{db} / \mathrm{dec}$.
- This roll-off with $f$ continues until higher-order poles and zeros come into play, by which point the CMRR has already deteriorated to fairly low values.
(a) Let the EC pair of Fig. $6.24 a$ use BJTs having $\beta_{0}=200, V_{A}=50 \mathrm{~V}, r_{b}=$ $200 \Omega, C_{\pi}=25 \mathrm{pF}, C_{\mu}=0.3 \mathrm{pF}$, and $C_{s}=1 \mathrm{pF}$. Moreover, let $R_{B}=2 \mathrm{k} \Omega$ and $R_{C}=10 \mathrm{k} \Omega$, and let the emitter-biasing current sink have $I_{E E}=1 \mathrm{~mA}, R_{E E}=$ $1 \mathrm{M} \Omega$, and $C_{E E}=1.5 \mathrm{pF}$. Estimate the low-frequency value of the CMRR as well as its two principal poles.
(b) Use PSpice to display the Bode plots of $\left|a_{d m}\right|,\left|a_{c m}\right|$, and $\left|a_{d m} / a_{c m}\right|$, and comment.

#### Solution

(a) We have $g_{m}=(200 / 201) \times(0.5) / 26=19.1 \mathrm{~mA} / \mathrm{V}, r_{\pi}=10.5 \mathrm{k} \Omega, r_{o}=$ $100 \mathrm{k} \Omega, 2 R_{E E}=2 \mathrm{M} \Omega$, and $C_{E E} / 2=0.75 \mathrm{pF}$. Also, $\left(R_{B}+r_{b}\right) / / r_{\pi}=1.82 \mathrm{k} \Omega$ and $R_{C} / / r_{o}=9.09 \mathrm{k} \Omega$. Then, Eqs. (6.48) and (6.49) give

$$
\begin{aligned}
f_{p(\mathrm{dm})} & \cong \frac{1}{2 \pi 1.82 \times 10^{3}[25+0.3 \times(1+19.1 \times 9.09)+(9.09 / 1.82) \times 1] 10^{-12}} \\
& =1.06 \mathrm{MHz}
\end{aligned}
$$

and

$$
f_{z(\mathrm{~cm})} \cong \frac{1}{2 \pi \times 1 \times 10^{6} \times 1.5 \times 10^{-12}}=106 \mathrm{kHz}
$$

At low frequencies, $\mathrm{CMRR}=\left|a_{d m 0} / a_{c m 0}\right| \cong\left|-g_{m}\left(R_{C} / / r_{o}\right) /\left(-R_{C} / 2 R_{E E}\right)\right|=$ $174 / 0.005=34,800=90.8 \mathrm{~dB}$.
(b) To generate the Bode plot of $\left|a_{d m}\right|$ we reuse the PSpice circuit of Fig. 6.22, but with the present parameter values. To generate that of $\left|a_{d m}\right|$ we use again the same circuit, but after lifting the emitter terminal off ground and inserting the parallel combination of a $2-\mathrm{M} \Omega$ resistance and a $0.75-\mathrm{pF}$ capacitance between emitter and ground, in accordance with Fig. 6.26. The plots of $\left|a_{d m}\right|$, $\left|a_{c m}\right|$, and $\left|a_{d m} / a_{c m}\right|$ are shown in Fig. 6.27. The PSpice values $\left|a_{d m 0} / a_{c m 0}\right|=$ $90.1 \mathrm{~dB}, f_{p(\mathrm{dm})}=1.05 \mathrm{MHz}$, and $f_{z(\mathrm{~cm})}=161 \mathrm{kHz}$ are in fair agreement with the calculated values.
image_name:FIGURE 6.27
description:The graph in Figure 6.27 is a Bode plot displaying the magnitude of three different gain functions: \(|A_{dm}|\), \(|A_{cm}|\), and the Common-Mode Rejection Ratio (CMRR), across a frequency range.

1. **Type of Graph and Function**:
- This is a Bode plot, which is typically used to illustrate the frequency response of a system.

2. **Axes Labels and Units**:
- The x-axis represents frequency \(f\) in hertz (Hz), ranging from \(10^4\) to \(10^9\) Hz.
- The y-axis represents gain in decibels (dB), ranging from -50 dB to 100 dB.
- The plot uses a logarithmic scale for frequency and a linear scale for gain.

3. **Overall Behavior and Trends**:
- The \(|A_{dm}|\) curve starts high at lower frequencies and shows a gradual decline as frequency increases, indicating a decrease in differential-mode gain.
- The \(|A_{cm}|\) curve starts low, increases to a peak, and then decreases again, showing a band-pass filter characteristic.
- The CMRR curve starts at a high value and decreases steadily across the frequency range, indicating a reduction in the ability to reject common-mode signals at higher frequencies.

4. **Key Features and Technical Details**:
- The peak of the \(|A_{cm}|\) curve is an important feature, indicating the frequency at which common-mode gain is maximized.
- The intersection points of the curves can indicate important frequencies related to system performance, such as the cutoff frequencies.
- The CMRR is highest at lower frequencies, which is typical for differential amplifiers.

5. **Annotations and Specific Data Points**:
- The plot is annotated with the labels \(|A_{dm}|\), \(|A_{cm}|\), and \(|CMRR|\) to indicate each curve.
- There are gridlines at significant gain levels (e.g., 0 dB, 50 dB) and frequency markers (e.g., \(10^5\), \(10^6\) Hz) to aid in reading specific values from the graph.

Overall, this plot provides a comprehensive view of how the differential-mode gain, common-mode gain, and CMRR vary with frequency for the given electronic circuit configuration.

FIGURE 6.27 Bode plots for the EC pair of Example 6.9.

The results obtained above for the EC pair are readily adapted to the SC pair. The dominant pole of $a_{d m}(j f)$, being also the second pole of the CMRR, is now

$$
\begin{equation*}
f_{p(\mathrm{dm})} \cong \frac{1 / 2 \pi}{R_{s i g}\left\{C_{g s}+C_{g d}\left[1+g_{m}\left(R_{D} / / r_{o}\right)\right]\right\}+\left(R_{D} / / r_{o}\right) C_{d b}} \tag{6.50}
\end{equation*}
$$

whereas the dominant zero of $a_{c m}(j f)$, being also the first pole of CMRR, is

$$
\begin{equation*}
f_{z(\mathrm{~cm})}=\frac{1}{2 \pi R_{S S} C_{S S}} \tag{6.51}
\end{equation*}
$$

The Bode plots are qualitatively similar to those of Fig. 6.27.

### Active-Loaded Differential Amplifiers

With an active load, the circuit loses its symmetry and the additional parasitics introduced by the load transistors tend to complicate the analysis. It is nevertheless possible to gain quick insight into the predominant characteristics of the circuit if we are willing to make suitable approximations. As shown in the CMOS version of Fig. 6.28, the circuit possesses two significant nodes, denoted as $V_{1}$ and $V_{o}$. With a balanced input drive, the third node, denoted as $V_{s s}$, would be at ac ground if the drains of $M_{1}$ and $M_{1}$ were terminated equally. In practice $M_{1}$ 's drain is terminated on the resistance $\left(1 / g_{m 3}\right) / / r_{o 3} \cong$ $1 / g_{m 3}$ while $M_{2}$ 's drain is terminated on the resistance $r_{o 4}$, such that $r_{o 4} \gg 1 / g_{m 3}$. This imbalance results in $V_{s s} \neq 0$. Let us nevertheless continue to assume an ac ground at $V_{s s}$ so that we can apply the half-circuit concept to simplify our analysis.

The net capacitances associated with the nodes $V_{1}$ and $V_{o}$ are, respectively,

$$
\begin{align*}
& C_{1} \cong C_{g s 3}+C_{g s 4}+C_{d b 3}+C_{d b 1}+C_{g d 1}  \tag{6.52a}\\
& C_{2} \cong C_{g d 4}+C_{d b 4}+C_{g d 2}+C_{d b 2}+C_{L} \tag{6.52b}
\end{align*}
$$

image_name:FIGURE 6.28 High-frequency model of the active-loaded CMOS differential amplifier
description:
[
name: M1, type: NMOS, ports: {S: Vss, D: V1, G: Vid/2}
name: M2, type: NMOS, ports: {S: Vss, D: Vo, G: -Vid/2}
name: M3, type: PMOS, ports: {S: GND, D: V1, G: V1}
name: M4, type: PMOS, ports: {S: GND, D: Vo, G: Vo}
name: C1, type: Capacitor, value: C1, ports: {Np: V1, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: Vo, Nn: GND}
name: Vid/2, type: VoltageSource, value: Vid/2, ports: {Np: Vid/2, Nn: GND}
name: -Vid/2, type: VoltageSource, value: Vid/2, ports: {Np: -Vid/2, Nn: GND}
]
extrainfo:This circuit is a high-frequency model of an active-loaded CMOS differential amplifier. It includes two NMOS transistors (M1, M2) and two PMOS transistors (M3, M4), with resistors and capacitors to model the high-frequency behavior. The differential input is provided by two voltage sources with values Vid/2 and -Vid/2.

FIGURE 6.28 High-frequency model of the active-loaded CMOS differential amplifier (to facilitate analysis, all stray capacitances have been moved outside of the FETs and lumped together into two equivalent capacitances $C_{1}$ and $C_{2}$ as shown).
where $C_{L}$ is the capacitance of the external load, if any. It can be proved that these capacitances see, respectively, the equivalent resistances

$$
\begin{gather*}
R_{1}=\frac{r_{o p} / /\left(2 r_{o n}+r_{o p}\right)}{1+g_{m p} r_{o p}}  \tag{6.53a}\\
R_{2}=r_{o p} / / r_{o n} \tag{6.53b}
\end{gather*}
$$

and as such yield two pole frequencies at $\omega_{1}=1 /\left(R_{1} C_{1}\right)$ and $\omega_{2}=1 /\left(R_{2} C_{2}\right)$.

#### Exercise 6.4

Prove Eq. (6.53).
Hint: replace each transistor with its small-signal model and use the test method, exploiting also the fact that $M_{1}$ and $M_{2}$ are matched, and so are $M_{3}$ and $M_{4}$.

By the superposition principle, $V_{o}=V_{o 4}+V_{o 2}$, where $V_{o 4}$ is due to $M_{4}$ 's response to $+V_{i d} / 2$, and $V_{o 2}$ to $M_{2}$ 's response to $-V_{i d} / 2$. By inspection, $V_{o 2}=\left[R_{2} / /\left(1 / s C_{2}\right)\right] I_{2}$, where $I_{2}=g_{m 2} V_{i d} / 2$. Expanding, we get

$$
\begin{equation*}
V_{o 2}=\frac{g_{m 2} R_{2}}{1+s R_{2} C_{2}} \frac{V_{i d}}{2} \tag{6.54a}
\end{equation*}
$$

Similarly, $V_{o 4}=\left[R_{2} / /\left(1 / s C_{2}\right)\right] I_{4}$, where $I_{4}=g_{m 4} V_{1}$. But,

$$
V_{1} \cong \frac{\left(1 / g_{m 3}\right) I_{1}}{1+s R_{1} C_{1}}=\frac{\left(1 / g_{m 3}\right)}{1+s R_{1} C_{1}} g_{m 1} \frac{V_{i d}}{2}
$$

Substituting, and exploiting the fact that $g_{m 4} / g_{m 3}=1$ because of matching, we get

$$
\begin{equation*}
V_{o 4} \cong \frac{1}{1+s R_{1} C_{1}} \frac{g_{m 2} R_{2}}{1+s R_{2} C_{2}} \frac{V_{i d}}{2} \tag{6.54b}
\end{equation*}
$$

It is interesting to note that $V_{i d}$ contributes to $V_{o}$ via the shorter signal path made up of $M_{2}$ as well as via the longer signal path made up of $M_{1}-M_{3}-M_{4}$. Both paths converge at the common output-node pole formed by $R_{2}$ and $C_{2}$. However, the longer path is slower because it includes also the additional pole due to $R_{1}$ and $C_{1}$. Letting $V_{o}=V_{o 4}+V_{o 2}$, collecting and simplifying, we finally get

$$
a_{d m}(s)=\frac{V_{o}}{V_{i d}}=g_{m 2} R_{2} \frac{1+s 0.5 R_{1} C_{1}}{1+s R_{1} C_{1}} \frac{1}{1+s R_{2} C_{2}}
$$

Letting $s \rightarrow 2 \pi f$ and $g_{m 1}=g_{m 2}=g_{m n}$, we express gain in the insightful form

$$
\begin{equation*}
a_{d m}(j f)=a_{d m 0} \frac{1+j f / f_{0}}{\left(1+j f / f_{1}\right)\left(1+j f / f_{2}\right)} \tag{6.55}
\end{equation*}
$$

where

$$
\begin{equation*}
a_{d m 0}=g_{m n}\left(r_{o p} / / r_{o p}\right) \tag{6.56}
\end{equation*}
$$

$$
\begin{equation*}
f_{1}=\frac{1}{2 \pi R_{1} C_{1}} \quad f_{2}=\frac{1}{2 \pi R_{2} C_{2}} \quad f_{0}=2 f_{1} \tag{6.57}
\end{equation*}
$$

It is apparent that beside the aforementioned pole frequencies $f_{1}$ and $f_{2}, a_{d m}(j f)$ exhibits also a zero frequency $f_{0}$ stemming from the direct signal path via $M_{2}$. At sufficiently high frequencies the slower signal path via $M_{1}-M_{3}-M_{4}$ is shunted by $C_{1}$, leaving only the faster path via $M_{2}$. Regardless, the overall frequency response is dominated by $f_{2}$ due to the fact that $R_{2} \gg R_{1}$.

EXAMPLE 6.10 In the circuit of Fig. 6.28 let all FETs have $g_{m}=1 \mathrm{~mA} / \mathrm{V}, r_{o}=50 \mathrm{k} \Omega, C_{g s}=50 \mathrm{fF}$, and $C_{g d}=C_{d b}=5 \mathrm{fF}$. Moreover, assume the circuit is terminated on a load capacitance $C_{L}=0.25 \mathrm{pF}$. Estimate all the parameters intervening in the calculation of $a_{d m}(j f)$. Hence, verify with PSpice, and comment.

#### Solution

Plugging the given data into Eqs. (6.52) and (6.53) gives $C_{1}=115 \mathrm{fF}, R_{1}=735 \Omega$, $C_{2}=270 \mathrm{fF}$, and $R_{2}=25 \mathrm{k} \Omega$. Plugging in turn into Eqs. (6.56) and (6.57) we get

$$
a_{d m 0}=25 \mathrm{~V} / \mathrm{V} \quad f_{2}=23.6 \mathrm{MHz} \quad f_{1}=1.88 \mathrm{GHz} \quad f_{0}=3.27 \mathrm{GHz}
$$

A PSpice simulation yields the gain plot of Fig. 6.29a. Using the cursor facility we find $a_{d m 0}=24.7 \mathrm{~V} / \mathrm{V}$ and $f_{-3 \mathrm{~dB}}=23.3 \mathrm{MHz}$, in good agreement with the calculated values. Figure $6.29 b$ shows the magnitude plot of the amplifier's shortcircuit transconductance $G_{m}=I_{o(\mathrm{sc})} / V_{i d}$. Short-circuiting the output node eliminates the pole frequency $f_{2}$, so the plot evidences only the pole-zero frequency pair $f_{1}$ and $f_{0}$, both of which are in the GHz range.
image_name:(a)
description:The graph labeled \((a)\) is a Bode plot representing the frequency response of an active-loaded CMOS amplifier. The plot illustrates the gain \(a\) in decibels (dB) on the vertical axis against frequency \(f\) in hertz (Hz) on the horizontal axis. The frequency scale is logarithmic, ranging from \(10^6\) Hz to \(10^9\) Hz.

Overall Behavior and Trends:
- The gain starts at approximately 30 dB at low frequencies (around \(10^6\) Hz).
- As frequency increases, the gain remains relatively constant until it approaches the cutoff frequency.
- Beyond this point, the gain begins to decrease steadily, indicating a low-pass filter behavior typical of amplifiers.

Key Features and Technical Details:
- The -3 dB cutoff frequency \(f_{-3 \text{ dB}}\) is noted at 23.3 MHz, where the gain drops by 3 dB from its maximum value.
- The initial gain value \(a_{dm0}\) is 24.7 V/V, as calculated and confirmed by the plot.

Annotations and Specific Data Points:
- The plot includes gridlines that help identify significant frequency points and gain levels.
- The gain decrease beyond the cutoff frequency suggests the presence of a dominant pole affecting the amplifier's performance at higher frequencies.
image_name:(b)
description:Figure 6.29(b) depicts a Bode plot illustrating the frequency response of the short-circuit transconductance \( G_m \) of an active-loaded CMOS amplifier. The horizontal axis represents frequency \( f \) in hertz (Hz), ranging from \( 10^7 \) Hz to \( 10^{11} \) Hz, on a logarithmic scale. The vertical axis shows the transconductance \( G_m \) in milliampere per volt (mA/V).

The graph begins with a relatively flat region where the transconductance maintains a constant value close to 1.0 mA/V for frequencies up to approximately \( 10^9 \) Hz. As the frequency increases beyond this point, the transconductance begins to decrease sharply, indicating a roll-off. This behavior continues as the frequency approaches \( 10^{11} \) Hz, where the transconductance approaches zero.

The plot highlights the presence of a pole-zero frequency pair \( f_1 \) and \( f_0 \), both situated in the GHz range, as indicated in the context. The elimination of the output node pole frequency \( f_2 \) due to short-circuiting is also noted, simplifying the frequency response to only the dominant pole-zero pair.

FIGURE 6.29 Frequency response of the active-loaded CMOS amplifier of Example 6.10.

## 6.5 BIPOLAR VOLTAGE AND CURRENT BUFFERS

Recall that the role of a voltage buffer is to provide unity voltage gain with high input impedance and low output impedance, whereas that of a current buffer is to provide unity current gain with low input impedance and high output impedance. We are about to see that the CC and CB configurations approach the above characteristics over a fairly wide frequency band because they are exempt from the Miller effect, the main frequency bottleneck of CE amplifiers. However, the BJT's stray capacitances do come into play at high frequencies, where they tend to degrade both the gain and the terminal impedances. In particular, impedances that start out high tend to decrease with frequency, thus exhibiting capacitive behavior, and impedances that start out low tend to increase with frequency (at least up to a point), thus exhibiting inductive behavior. Moreover, gain may depart appreciably from unity at high frequencies.

If the study of voltage amplifiers focuses on the frequency behavior of gain because gain is the most important amplifier parameter, the study of buffers must emphasize the frequency behavior of the terminal impedances because impedance transformation is the primary function of a buffer.

### Frequency Characteristics of the Emitter Follower

Figure 6.30 shows the ac equivalent of the emitter follower, along with its highfrequency model. Since its right plate is grounded, $C_{\mu}$ is exempt from the Miller multiplication, so we expect the CC to be an inherently fast configuration. In fact, to develop a quick (if only approximate) feel for the circuit, let us ignore $C_{\mu}$ altogether (the general case with $C_{\mu}$ present will be addressed in Section 6.7). We wish to investigate the frequency dependence of the impedance $Z_{i}(j \omega)$ seen by the signal source, the source-to-load voltage gain $a(j \omega)=V_{o} / V_{s i g}$, and the impedance $Z_{o}(j \omega)$ seen by the load.

The starting point is offered by Eqs. (2.83), (2.84), and (2.86), provided we make the substitutions

$$
\begin{equation*}
\beta_{0} \rightarrow \beta(j \omega) \quad r_{\pi} \rightarrow z_{\pi}(j \omega) \tag{6.58}
\end{equation*}
$$

image_name:(a)
description:
[
name: Vsig, type: VoltageSource, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: X1}
name: M1, type: NPN, ports: {C: GND, B: X1, E: Vo}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:This circuit is an emitter follower configuration with a high-frequency small-signal model. It analyzes the frequency dependence of the impedance seen by the signal source, the source-to-load voltage gain, and the impedance seen by the load.
image_name:(b)
description:
[
name: Vsig, type: VoltageSource, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: X1}
name: rb, type: Resistor, value: rb, ports: {N1: X1, N2: X2}
name: rπ, type: Resistor, value: rπ, ports: {N1: X2, N2: Vo}
name: g_mVπ, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: Vo}
name: Cμ, type: Capacitor, value: Cμ, ports: {Np: X2, Nn: GND}
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: X2, Nn: Vo}
name: ro, type: Resistor, value: ro, ports: {N1: Vo, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a high-frequency small-signal model of an emitter follower. It includes a voltage source Vsig, resistors Rsig, rb, rπ, ro, and RL, a capacitor Cμ, and an NPN transistor M1. The model is used to analyze the frequency dependence of the input impedance Zi, the output impedance Zo, and the voltage gain.

FIGURE 6.30 (a) The emitter follower and (b) its high-frequency small-signal model.
where

$$
\begin{equation*}
\beta(j \omega)=\frac{\beta_{0}}{1+j \omega / \omega_{\beta}} \tag{6.59a}
\end{equation*}
$$

and

$$
z_{\pi}(j \omega)=r_{\pi} / / \frac{1}{j \omega C_{\pi}}=\frac{r_{\pi}}{1+j \omega r_{\pi} C_{\pi}}
$$

By Eq. (6.8), $\omega_{\beta}=1 /\left[r_{\pi}\left(C_{\pi}+C_{\mu}\right)\right]$. As long as $C_{\mu} \ll C_{\pi}$, we can approximate $\omega_{\beta} \cong 1 /\left(r_{\pi} C_{\pi}\right)$ and write

$$
\begin{equation*}
z_{\pi}(j \omega) \cong \frac{r_{\pi}}{1+j \omega / \omega_{\beta}}=\frac{\beta(j \omega)}{g_{m}} \tag{6.59b}
\end{equation*}
$$

With the above substitutions, the emitter-follower parameters become

$$
\begin{gather*}
Z_{i}(j \omega)=r_{b}+z_{\pi}(j \omega)+[\beta(j \omega)+1]\left(R_{L} / / r_{o}\right) \\
Z_{o}(j \omega)=\frac{R_{s i g}+r_{b}+z_{\pi}(j \omega)}{\beta(j \omega)+1} / / r_{o}  \tag{6.60a}\\
a(j \omega)=\frac{V_{o}}{V_{s i g}}=\frac{1}{1+\frac{R_{s i g}+r_{b}+z_{\pi}(j \omega)}{[\beta(j \omega)+1]\left(R_{L} / / r_{o}\right)}} \tag{6.60b}
\end{gather*}
$$

At sufficiently low frequencies, where $C_{\pi}$ acts as an open circuit, we have $\beta \rightarrow \beta_{0}$ and $z_{\pi} \rightarrow r_{\pi}$, so the above expressions tend to their familiar low-frequency forms, which we identify with subscript 0 ,

$$
\begin{gather*}
Z_{i 0}=r_{b}+r_{\pi}+\left(\beta_{0}+1\right)\left(R_{L} / / r_{o}\right) \quad Z_{o 0}=\frac{R_{s i g}+r_{b}+r_{\pi}}{\beta_{0}+1} / / r_{o}  \tag{6.61a}\\
a_{0}=\frac{1}{1+\frac{R_{s i g}+r_{b}+r_{\pi}}{\left(\beta_{0}+1\right)\left(R_{L} / / r_{o}\right)}} \tag{6.61b}
\end{gather*}
$$

On the other hand, at sufficiently high frequencies, where $C_{\pi}$ acts as a short circuit, we have $\beta \rightarrow 0$ and $z_{\pi} \rightarrow 0$, so the high-frequency asymptotes, identified by subscript $\infty$, are

$$
\begin{gather*}
Z_{i \infty}=r_{b}+\left(R_{L} / / r_{o}\right) \quad Z_{o \infty}=\left(R_{s i g}+r_{b}\right) / / r_{o}  \tag{6.62a}\\
a_{\infty}=\frac{1}{1+\frac{R_{s i g}+r_{b}}{R_{L} / / r_{o}}} \tag{6.62b}
\end{gather*}
$$

We observe that $Z_{i \infty} \ll Z_{i 0}$, indicating that $Z_{i}$ is always a capacitive impedance. However, $Z_{o}$ may be inductive, capacitive, or even purely resistive, depending on how the product $g_{m}\left(R_{s i g}+r_{b}\right)$ compares with unity. One can prove (see Problem 6.18) that if the BJT is biased at a sufficiently low current to make $g_{m}\left(R_{s i g}+r_{b}\right) \leq 1$, then we have $a_{\infty} \geq a_{0}$ and $Z_{o \infty} \leq Z_{o 0}$. In practical circuits it is far more common to have $g_{m}\left(R_{s i g}+r_{b}\right) \gg 1$, in which case $a_{\infty}<a_{0}$ and $Z_{o \infty} \gg Z_{o 0}$, indicating an inductive $Z_{o}$.

Figure 6.31 shows typical magnitude plots of $Z_{i}, a$, and $Z_{o}$ for $C_{\mu}=0$ and $g_{m}\left(R_{s i g}+r_{b}\right) \gg 1$. In accordance with Appendix 6A, these parameters must take on the forms

$$
\begin{gather*}
Z_{i}(j \omega)=Z_{i 0} \frac{1+j \omega / \omega_{z i}}{1+j \omega / \omega_{p i}} \quad a(j \omega)=a_{0} \frac{1+j \omega / \omega_{z a}}{1+j \omega / \omega_{p a}} \\
Z_{o}(j \omega)=Z_{o 0} \frac{1+j \omega / \omega_{z o}}{1+j \omega / \omega_{p o}} \tag{6.63}
\end{gather*}
$$

We now seek to estimate, for each of the above expressions, the zero and pole frequencies $\omega_{z}$ and $\omega_{p}$, also known as the breakfrequencies. This task is facilitated by the fact that letting $\omega \rightarrow \infty$ in the above expressions we obtain the following constraints

$$
\begin{equation*}
\frac{Z_{i 0}}{Z_{i \infty}}=\frac{\omega_{z i}}{\omega_{p i}} \quad \frac{a_{0}}{a_{\infty}}=\frac{\omega_{z a}}{\omega_{p a}} \quad \frac{Z_{o \infty}}{Z_{o 0}}=\frac{\omega_{p o}}{\omega_{z o}} \tag{6.64}
\end{equation*}
$$

Consequently, for each expression we need only to estimate one of its two break frequencies. The other can be found via the appropriate constraint of Eq. (6.64). Though the exact derivations are left as an exercise in Problem 6.19, here we wish to pursue quick estimations to gain basic insight. Thus, according to Eq. (6.60), each of $Z_{i}(j \omega)$, $Z_{o}(j \omega)$, and $a(j \omega)$ contains the terms $z_{\pi}(j \omega)$ and $\beta(j \omega)+1$. These terms affect the frequency response up to $\omega_{T}$, beyond which $z_{\pi}(j \omega)$ becomes negligible compared to the other resistances in the circuit, and $\beta(j \omega)$ becomes negligible compared to 1 . So, we expect each curve in Fig. 6.31 to make the transition to its high-frequency asymptote in the vicinity of $\omega_{T}$, thus giving

$$
\begin{equation*}
\omega_{z i} \cong \omega_{z a} \cong \omega_{p o} \cong \omega_{T} \tag{6.65}
\end{equation*}
$$

image_name:(a)
description:The graph labeled "(a)" in Figure 6.31 is a Bode plot representing the input impedance \( |Z_i(j\omega)| \) of an emitter-follower circuit with \( C_{\mu} = 0 \). The plot is depicted on a logarithmic scale for both the magnitude of the impedance and frequency.

Axes Labels and Units:
- **Vertical Axis:** Represents the magnitude of the input impedance \( |Z_i(j\omega)| \), denoted in decibels (dec).
- **Horizontal Axis:** Represents the angular frequency \( \omega \), also in decades (dec).

Overall Behavior and Trends:
- The graph shows a decreasing trend in the input impedance as the frequency increases.
- Initially, at lower frequencies, the impedance is constant at a value \( Z_{i0} \).
- As the frequency approaches \( \omega_{pi} \), the impedance starts to decrease at a rate of \(-1 \text{ dec/dec}\).
- This decrease continues until it reaches \( \omega_{zi} \), where the impedance stabilizes at a lower constant value \( Z_{i\infty} \).

Key Features and Technical Details:
- **\( Z_{i0} \):** The initial constant value of the input impedance at low frequencies.
- **\( \omega_{pi} \):** The frequency at which the impedance begins its decline.
- **\( \omega_{zi} \):** The frequency beyond which the impedance stabilizes at \( Z_{i\infty} \).
- **\( Z_{i\infty} \):** The final constant value of the input impedance at high frequencies.
- The slope of the decrease is \(-1 \text{ dec/dec}\), indicating a first-order system response.

Annotations and Specific Data Points:
- The plot includes reference lines marking \( \omega_{pi} \) and \( \omega_{zi} \), providing clear indications of the transition points in the impedance behavior.

This graph provides a clear visualization of how the input impedance of the emitter-follower changes with frequency, highlighting the transition from low-frequency stability to high-frequency stability with a significant decrease in between.
image_name:(b)
description:The graph labeled (b) represents the voltage gain \( |a(j\omega)| \) plotted against frequency \( \omega \) on a logarithmic scale. The y-axis is labeled in decibels (dB), indicating the magnitude of the voltage gain, while the x-axis represents the frequency in decades (dec).

Overall Behavior and Trends:
The graph shows a typical emitter-follower voltage gain characteristic where the gain starts at a constant level \( a_0 \) at low frequencies. As the frequency increases, the gain remains constant until it approaches the pole frequency \( \omega_{pa} \). Beyond this point, the gain begins to decrease, indicating a roll-off that continues past the zero frequency \( \omega_{za} \) until it reaches a lower constant level \( a_\infty \) at high frequencies.

Key Features and Technical Details:
- **Initial Gain Level (\( a_0 \))**: The gain starts at \( a_0 \) dB at low frequencies, indicating the maximum gain in the passband.
- **Pole Frequency (\( \omega_{pa} \))**: This is where the gain begins to decrease. It marks the start of the transition from the passband to the roll-off region.
- **Zero Frequency (\( \omega_{za} \))**: This frequency marks a point in the roll-off region where the slope of the gain changes, indicating a transition to a flatter response as it approaches the high-frequency asymptote.
- **Final Gain Level (\( a_\infty \))**: The gain stabilizes to a lower level at high frequencies, indicating the high-frequency asymptote.

Annotations and Specific Data Points:
- The graph is annotated with the frequencies \( \omega_{pa} \) and \( \omega_{za} \), which are critical in understanding the behavior of the voltage gain across frequencies.
- The transition from \( a_0 \) to \( a_\infty \) signifies the bandwidth of the emitter-follower circuit, showing the frequency range over which the gain is effectively maintained before rolling off.
image_name:(c)
description:The graph labeled (c) in Figure 6.31 represents the frequency response of the output impedance \( |Z_o(j\omega)| \) of an emitter-follower configuration, plotted on a logarithmic scale. The x-axis represents the angular frequency \( \omega \) in decades, while the y-axis represents the magnitude of the output impedance \( |Z_o| \) in decades as well.

Overall Behavior and Trends:
- **Low-Frequency Region:** At low frequencies, the output impedance \( Z_o \) remains constant at a value \( Z_{o0} \).
- **Mid-Frequency Transition:** As the frequency increases, starting at \( \omega_{zo} \), the output impedance begins to rise at a rate of 1 decade per decade. This indicates a linear increase on the logarithmic scale.
- **High-Frequency Region:** After reaching \( \omega_{po} \), the output impedance levels off to a new constant value \( Z_{o\infty} \), indicating that it becomes frequency-independent at high frequencies.

Key Features and Technical Details:
- **Transition Point \( \omega_{zo} \):** This is the frequency at which the output impedance starts to increase.
- **Asymptotic Behavior:** The graph shows a clear transition from a low-frequency constant value \( Z_{o0} \) to a high-frequency constant value \( Z_{o\infty} \), passing through a linear increase.
- **Slope:** The slope of the increase is 1 decade per decade, which is a typical characteristic for such a response.

Annotations and Specific Data Points:
- The graph includes reference lines and annotations marking \( \omega_{zo} \) and \( \omega_{po} \), which are critical frequencies where the behavior of the output impedance changes significantly.
- The values \( Z_{o0} \) and \( Z_{o\infty} \) are the low and high-frequency asymptotic values of the output impedance, respectively.

FIGURE 6.31 Typical emitter-follower characteristics for $C_{\mu}=0$ : (a) input impedance $Z_{i}$, (b) voltage gain a, and (c) output impedance $Z_{o}$. The plots of $a$ and $Z_{o}$ are for the case $g_{m}\left(R_{s i g}+r_{b}\right) \gg 1$.

EXAMPLE 6.11 (a) Let the BJT of Fig. 6.30 have $\beta_{0}=150, V_{A}=80 \mathrm{~V}, r_{b}=200 \Omega$, and $C_{\mu}=1 \mathrm{pF}$, and suppose it is biased at $I_{C}=2 \mathrm{~mA}$, where it has $f_{T}=400 \mathrm{MHz}$. Moreover, let $R_{\text {sig }}=2 \mathrm{k} \Omega$ and $R_{L}=5 \mathrm{k} \Omega$. Ignoring $C_{\mu}$, provide quick estimates for the asymptotic values as well as the pole and zero frequencies of $a, Z_{i}$, and $Z_{o}$.
(b) Verify with PSpice and compare with the calculated values.
(c) Re-run PSpice with $C_{\mu}=1 \mathrm{pF}$ and use physical insight to justify the ensuing changes in the plots.

#### Solution

(a) Proceeding as usual we find $g_{m}=1 /(13 \Omega), r_{\pi}=1.95 \mathrm{k} \Omega$, and $r_{o}=40 \mathrm{k} \Omega$, so that $R_{s i g}+r_{b}=2+0.2=2.2 \mathrm{k} \Omega$ and $R_{L} / / r_{o}=5 / / 40=4.44 \mathrm{k} \Omega$. The asymptotic values of gain are

$$
\begin{aligned}
& a_{0}=\frac{1}{1+\frac{2.2+1.95}{151 \times 4.44}}=0.994 \mathrm{~V} / \mathrm{V}=-0.05 \mathrm{~dB} \\
& a_{\infty}=\frac{1}{1+\frac{2.2}{4.44}}=0.669 \mathrm{~V} / \mathrm{V}=-3.5 \mathrm{~dB}
\end{aligned}
$$

and its zero and pole frequencies are

$$
f_{z a} \cong f_{T}=400 \mathrm{MHz} \quad f_{p a} \cong \frac{a_{\infty}}{a_{0}} f_{z a}=\frac{0.669}{0.994} 400=269 \mathrm{MHz}
$$

which are fairly high and close to each other. The asymptotic vales of $Z_{i}$ are

$$
Z_{i 0}=0.2+1.95+151 \times 4.44=673 \mathrm{k} \Omega \quad Z_{i o}=0.2+4.44=4.64 \mathrm{k} \Omega
$$

and the approximate zero and pole frequencies of $Z_{i}$ are

$$
f_{z i} \cong f_{T}=400 \mathrm{MHz} \quad f_{p i} \cong \frac{Z_{i \infty}}{Z_{i 0}} f_{T}=\frac{4.64}{673} 400=2.76 \mathrm{MHz}
$$

Finally, the asymptotic vales of $Z_{o}$ are

$$
Z_{o 0}=\frac{2.2+1.95}{151}=27.5 \Omega \quad Z_{o \infty}=(2+0.2) / / 40=2.09 \mathrm{k} \Omega
$$

and the approximate pole and zero frequencies of $Z_{o}$ are

$$
f_{p o} \cong f_{T}=400 \mathrm{MHz} \quad f_{z 0} \cong \frac{Z_{o 0}}{Z_{o \infty}} f_{T}=\frac{27.5}{2090} 400=5.26 \mathrm{MHz}
$$

(b) Using the PSpice circuit of Fig. 6.32 we get the plots of Fig. 6.33, whose asymptotic values and break frequencies for $C_{\mu}=0$ are in good agreement with the values estimated above.
image_name:FIGURE 6.32
description:
[
name: Vsig, type: VoltageSource, value: 1 Vac, 0 Vdc, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: 2.0 kΩ, ports: {N1: Vsig, N2: X1}
name: rb, type: Resistor, value: 200 Ω, ports: {N1: X1, N2: X2}
name: rπ, type: Resistor, value: 1.95 kΩ, ports: {N1: X2, N2: Vo}
name: Cπ, type: Capacitor, value: 29.6 pF, ports: {Np: X2, Nn: Vo}
name: Cμ, type: Capacitor, value: 1 pF, ports: {Np: X2, Nn: GND}
name: gm, type: VoltageControlledCurrentSource, value: 77 mA/V, ports: {Np: Vo, Nn: GND}
name: ro, type: Resistor, value: 40 kΩ, ports: {N1: Vo, N2: GND}
name: RL, type: Resistor, value: 5 kΩ, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is an emitter follower configuration with a voltage source Vsig providing input through Rsig and rb. The transistor is modeled using rπ and gm. Capacitors Cπ and Cμ are used for frequency response analysis. Additional resistors ro and RL are connected to the output node Vo.

FIGURE 6.32 PSpice circuit to display the Bode plots of the emitter follower of Example 6.11.
(c) Re-running PSpice with $C_{\mu}=1 \mathrm{pF}$ indicates the presence of an additional pole frequency for each plot. Using physical insight we estimate the additional pole frequency of $Z_{i}$ in the vicinity of $1 /\left(2 \pi Z_{i 0} C_{\mu}\right)=236 \mathrm{MHz}$, that of $a$ in the vicinity of $1 /\left[2 \pi\left(R_{s i g}+r_{b}\right) C_{\mu}\right]=72 \mathrm{MHz}$, and that of $Z_{o}$ in the vicinity of $1 /\left\{2 \pi\left[\left(R_{s i g}+r_{b}\right) / / R_{L}\right] C_{\mu}\right\}=104 \mathrm{MHz}$. Above this frequency $Z_{o}$ changes from inductive to capacitive.
image_name:(a)
description:The graph labeled "(a)" is a Bode plot depicting the magnitude of input impedance, denoted as \(|Z_i|\), as a function of frequency \(f\). The x-axis represents frequency in hertz (Hz) on a logarithmic scale, ranging from \(10^5\) Hz to \(10^{10}\) Hz. The y-axis represents the magnitude of impedance in ohms (\(\Omega\)), also on a logarithmic scale, ranging from \(10^2\) to \(10^6\) ohms.

Two curves are plotted, corresponding to different values of \(C_\mu\), which is the parasitic capacitance. The first curve (dark line) represents \(C_\mu = 1\) pF, and the second curve (light line) represents \(C_\mu = 0\).

Overall Behavior and Trends:
- **For \(C_\mu = 0\):** The impedance starts at a high value around \(10^6\) ohms and decreases steadily as frequency increases, showing a linear decline on the logarithmic scale.
- **For \(C_\mu = 1\) pF:** The impedance begins similarly at a high value but decreases more rapidly than the \(C_\mu = 0\) case, indicating a lower impedance at higher frequencies.

Key Features and Technical Details:
- The plot shows a significant difference in behavior between the two curves as frequency increases, highlighting the effect of parasitic capacitance on input impedance.
- At lower frequencies, both curves start at similar impedance levels, but diverge as frequency increases, with the \(C_\mu = 1\) pF curve dropping more steeply.

Annotations and Specific Data Points:
- The plot is annotated with the values of \(C_\mu\) for each curve, indicating the effect of capacitance on the input impedance across the frequency spectrum.

This graph is essential for understanding how parasitic capacitance affects the input impedance of the emitter follower circuit, particularly at higher frequencies where the effects become more pronounced.
image_name:(b)
description:The graph labeled "(b)" is a Bode plot depicting the gain in decibels (dB) versus frequency in hertz (Hz) for an emitter follower configuration. The x-axis represents the frequency, spanning from $10^5$ Hz to $10^{10}$ Hz on a logarithmic scale. The y-axis shows the gain in decibels, ranging from -10 dB to 0 dB.

There are two curves plotted on this graph, each corresponding to different values of $C_{\mu}$. The curve labeled $C_{\mu} = 1$ pF shows a significant decrease in gain starting around $10^7$ Hz, dropping steeply to approximately -10 dB as the frequency approaches $10^9$ Hz. This indicates a sharp decline in gain with increasing frequency, suggesting a pole in this vicinity.

The second curve, labeled $C_{\mu} = 0$, maintains a relatively constant gain close to 0 dB across the frequency range, indicating that the absence of $C_{\mu}$ prevents the gain from declining significantly at higher frequencies.

Key features include the sharp drop in gain for $C_{\mu} = 1$ pF, showing the impact of the capacitance on the frequency response of the emitter follower. The graph highlights how the presence of $C_{\mu}$ introduces a pole affecting the gain at high frequencies, while its absence stabilizes the gain.
image_name:(c)
description:The graph labeled "(c)" is a Bode plot showing the magnitude of the output impedance $|Z_o|$ in ohms (Ω) as a function of frequency $f$ in hertz (Hz). The x-axis is logarithmically scaled from $10^5$ Hz to $10^{10}$ Hz, while the y-axis is also logarithmically scaled from $10^2$ Ω to $10^4$ Ω.

Two plots are shown, corresponding to two different values of $C_\mu$: $C_\mu = 0$ and $C_\mu = 1$ pF.

- For $C_\mu = 0$, the plot starts at around $10^3$ Ω at lower frequencies and remains relatively flat across the frequency range, indicating a constant impedance.
- For $C_\mu = 1$ pF, the plot starts at a similar value but exhibits a peak in impedance at around $10^8$ Hz, reaching a maximum value slightly above $10^3$ Ω before decreasing again as frequency increases.

The behavior of the $C_\mu = 1$ pF plot suggests a resonant peak, which is typical when inductive and capacitive elements interact, as described in the context. Above the peak frequency, the impedance decreases, indicating a transition from inductive to capacitive behavior, consistent with the given context of $Z_o$ changing from inductive to capacitive above $104$ MHz.

FIGURE 6.33 Gain and impedance plots for the emitter follower of Example 6.11.

Inductive behavior may pose problems when an emitter follower drives a capacitive load because of the tendency by capacitive and inductive impedances to resonate with each other. Depending on the damping conditions, the emitter follower may exhibit undesirable ringing or even oscillations. To better assess the situation, it is often convenient to model $Z_{o}$ in terms of a suitable network, such as the one of Fig. 6.34, consisting of an equivalent inductance $L_{o}$ with a series resistance $R_{s}$ and a parallel resistance $R_{p}$. Their values are found by matching the asymptotic values and break frequencies of the equivalent network to those of $Z_{o}$.
image_name:FIGURE 6.34
description:
[
name: Rsig, type: Resistor, value: Rsig, ports: {N1: GND, N2: B}
name: M1, type: NPN, ports: {C: GND, B: B, E: Vo}
name: Rs, type: Resistor, value: Rs, ports: {N1: Zo, N2: GND}
name: Rp, type: Resistor, value: Rp, ports: {N1: Zo, N2: GND}
name: Lo, type: Inductor, value: Lo, ports: {N1: X1, N2: GND}
]
extrainfo:The circuit on the left is an emitter follower configuration with an NPN transistor. The equivalent network on the right models the output impedance Z_o as a series of Rs, Lo, and Rp.

FIGURE 6.34 Equivalent network for the output impedance $Z_{e}$ of an emitter follower for the case $C_{\mu}=0$.

EXAMPLE 6.12 Find $R_{p}, R_{s}$, and $L_{o}$ for the emitter follower of Example 6.11. Again, ignore $C_{\mu}$.

#### Solution

In the limit $f \rightarrow \infty, L_{o}$ acts as an open circuit, resulting in $R_{p}=Z_{o \infty}$. By Example 6.11 we must thus have

$$
R_{p}=2.09 \mathrm{k} \Omega
$$

In the limit $f \rightarrow 0, L_{o}$ acts as a short circuit, giving $R_{s} / / R_{p}=Z_{o 0}$. By Example 6.11 we must thus have $1 / R_{s}+1 / 2090=1 / 27.5$, which gives

$$
R_{s} \cong 27.5 \Omega
$$

To find $L_{o}$, assume we start with $f=0$, where $L_{o}$ acts as a short compared to $R_{s}$, and we gradually increase $f$ until $\left|Z_{L}\right|$ becomes equal to $R_{s}$. This marks the zero frequency of $Z_{o}(j f)$, so imposing $\left|j 2 \pi f_{z o} L_{o}\right|=R_{s}$ gives

$$
L_{o}=\frac{R_{s}}{2 \pi f_{z o}}=\frac{27.5}{2 \pi 5 \times 10^{6}} \cong 875 \mathrm{nH}
$$

Alternatively, we could have applied physical insight at the pole frequency to get $L_{o}=R_{p} /\left(2 \pi f_{p o}\right)$.

### Frequency Characteristics of Bipolar Current Buffers

Figure 6.35 shows the ac equivalent of a bipolar current buffer, along with its highfrequency model. Like the CC configuration, the CB configuration is inherently fast because $C_{\mu}$ is exempt from the Miller effect. We wish to find the frequency dependence of the impedance $Z_{i}(j \omega)$ seen looking into the emitter, the current gain $a(j \omega)=$ $I_{o} / I_{i}$, and the impedance $Z_{o}(j \omega)$ seen looking into the collector.

To gain quick-if approximate-insight into $Z_{i}$ and $a$ it is convenient to ignore $r_{o}$ and $C_{\mu}$ for then the input port is isolated from the output port and can
image_name:(a)
description:
[
name: M1, type: NPN, ports: {C: X1, B: GND, E: X2}
name: RL, type: Resistor, value: RL, ports: {N1: X1, N2: GND}
name: Ii, type: CurrentSource, value: Ii, ports: {Np: X2, Nn: GND}
]
extrainfo:This circuit represents a high-frequency small-signal model of a bipolar current buffer. It includes an NPN transistor (M1) with associated resistors and capacitors to model the input and output impedances (Zi and Zo). The circuit is designed to analyze the frequency dependence of the input impedance, current gain, and output impedance. The model ignores certain elements like ro and Cμ for simplified calculations.
image_name:(b)
description:
[
name: rb, type: Resistor, value: rb, ports: {N1: X3, N2: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: X3, N2: X2}
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: X2, Nn: X3}
name: Cμ, type: Capacitor, value: Cμ, ports: {Np: X3, Nn: X1}
name: gmVπ, type: VoltageControlledCurrentSource, ports: {Np: X2, Nn: X1}
name: ro, type: Resistor, value: ro, ports: {N1: X1, N2: X2}
name: CS, type: Capacitor, value: CS, ports: {Np: X1, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: X1, N2: GND}
name: Ii, type: CurrentSource, value: Ii, ports: {Np: X2, Nn: GND}
]
extrainfo:The circuit is a high-frequency small-signal model of a bipolar current buffer. It includes a current source, resistors, capacitors, and a voltage-controlled current source to model the transistor behavior.

FIGURE 6.35 (a) The bipolar current buffer, and (b) its high-frequency small-signal model.
thus be analyzed separately. To find $Z_{i}(j \omega)$ we simply recycle the expression for $Z_{o}(j \omega)$ derived earlier for the CC configuration, but with $R_{s i g}=0$. The result is, for $r_{o} \rightarrow \infty$,

$$
\begin{equation*}
Z_{i}(j \omega)=Z_{i 0} \frac{1+j \omega / \omega_{z i}}{1+j \omega / \omega_{p i}} \tag{6.66a}
\end{equation*}
$$

where

$$
\begin{equation*}
Z_{i 0} \cong \frac{r_{b}+r_{\pi}}{\beta_{0}+1} \quad \omega_{p i} \cong \omega_{T} \quad \omega_{z i}=\frac{Z_{i 0}}{r_{b}} \omega_{p i} \tag{6.66b}
\end{equation*}
$$

Again, one can readily prove that this impedance is inductive for $g_{m} r_{b}>1$, capacitive for $g_{m} r_{b}<1$, and purely resistive for $g_{m} r_{b}=1$.

Using Eq. (6.59a) and expanding, we readily obtain the short-circuit current gain

$$
\begin{equation*}
\alpha(j \omega)=\frac{I_{o(\mathrm{sc})}}{I_{i}}=\frac{\beta(j \omega)}{\beta(j \omega)+1} \cong \frac{\alpha_{0}}{1+j \omega / \omega_{T}} \tag{6.67}
\end{equation*}
$$

where $I_{o(\mathrm{sc})}$ is the collector current in the limit $R_{L} \rightarrow 0$, and $\alpha_{0}=\beta_{0} /\left(\beta_{0}+1\right)$. Once it reaches the collector node, $I_{o(\mathrm{sc})}$ divides among $R_{L}, C_{\mu}$, and $C_{s}$. Since $r_{b}$ is small, we can treat $C_{\mu}$ as if its left plate was directly grounded, so we can lump $C_{\mu}$ with $C_{s}$. Using the current-divider formula we get, for $r_{o} \rightarrow \infty$,

$$
I_{o} \cong \frac{1 /\left[j \omega\left(C_{\mu}+C_{s}\right)\right]}{R_{L}+1 /\left[j \omega\left(C_{\mu}+C_{s}\right)\right]} \alpha(j \omega) I_{i}=\frac{\alpha(j \omega)}{1+j \omega R_{L}\left(C_{\mu}+C_{s}\right)} I_{i}
$$

Substituting Eq. (6.67), we finally obtain the overall current gain

$$
\begin{equation*}
a(j \omega)=\frac{I_{i}}{I_{i}} \cong \frac{\alpha_{0}}{\left(1+j \omega / \omega_{L}\right)\left(1+j \omega / \omega_{T}\right)} \quad \omega_{L} \cong \frac{1}{R_{L}\left(C_{\mu}+C_{s}\right)} \tag{6.68}
\end{equation*}
$$

It is apparent that the CB configuration provides its maximum bandwidth of $\omega_{T}$ when the load is a short circuit. For $R_{L} \neq 0$, the additional pole formed by $R_{L}$ with the effective collector capacitance $C_{\mu}+C_{s}$ reduces the bandwidth accordingly.

To develop an expression for the impedance $Z_{o}(j \omega)$ seen looking into the collector in Fig. 6.35, recall that at low frequencies this impedance takes on the familiar form $Z_{o 0}=\left(\beta_{0}+1\right) r_{o}$. This resistance forms a pole $\omega_{p o}$ with the capacitance $C_{\mu}+C_{s}$, so we have

$$
\begin{equation*}
Z_{o}(j \omega)=\frac{\left(\beta_{0}+1\right) r_{o}}{1+j \omega / \omega_{p o}} \quad \omega_{p o}=\frac{1}{\left(\beta_{0}+1\right) r_{o}\left(C_{\mu}+C_{s}\right)} \tag{6.69}
\end{equation*}
$$

EXAMPLE 6.13 The CB amplifier of Fig. $6.35 a$ uses a BJT with $\beta_{0}=200, V_{A}=50 \mathrm{~V}, r_{b}=250 \Omega$, $C_{\mu}=0.5 \mathrm{pF}$, and $C_{s}=1 \mathrm{pF}$. Also, the BJT is biased at $I_{C}=1 \mathrm{~mA}$, where it exhibits $f_{T}=500 \mathrm{MHz}$. If $R_{L}=5 \mathrm{k} \Omega$, estimate expressions for $a(j f), Z_{i}(j f)$, and $Z_{o}(j f)$.

#### Solution

We have $r_{\pi}=5.2 \mathrm{k} \Omega, r_{o}=50 \mathrm{k} \Omega$, and $C_{\mu}+C_{s}=0.5+1=1.5 \mathrm{pF}$. Plugging into the above formulas we get $\alpha_{0}=0.995, f_{L} \cong 21 \mathrm{MHz}, Z_{i 0} \cong 27 \Omega, f_{z i} \cong 54 \mathrm{MHz}$, $Z_{o 0} \cong 10 \mathrm{M} \Omega$, and $f_{p o} \cong 10.6 \mathrm{kHz}$. Consequently,

$$
a(j f) \cong \frac{0.995}{[1+j f /(21 \mathrm{MHz})][1+j f /(500 \mathrm{MHz})]}
$$

indicating that the band-limiting bottleneck for $a(j f)$ is the pole $f_{L}$. We also have

$$
Z_{i}(j f) \cong(27 \Omega) \frac{1+j f /(54 \mathrm{MHz})}{1+j f /(500 \mathrm{MHz})} \quad Z_{o}(j f)=\frac{10 \mathrm{M} \Omega}{1+j f /(10.6 \mathrm{kHz})}
$$

indicating an inductive $Z_{i}$ and a capacitive $Z_{o}$ (as we know, because of $C_{\mu}$ and $C_{s}$, $Z_{i}$ eventually will turn capacitive.
Remark: Even an apparently simple circuit such as a buffer may prove too complex for a thorough paper-and-pencil analysis. A reasonable approach is (a) to start out with a simplied but more manageable circuit version (such as Fig. 6.30b, where we ignore $C_{\mu}$ to focus on the more important $C_{\pi}$ ), (b) develop a basic feel for this simplified circuit, and $(c)$ then use PSpice to investigate higher-order effects (such as the effect of $C_{\mu}=1 \mathrm{pF}$ in Fig. 6.33). Regardless, we still need hand analysis in order to anticipate the results of computer simulation, and thus provide a form of check. This is how engineers proceed on their daily jobs.

## 6.6 MOS VOLTAGE AND CURRENT BUFFERS

The voltage/current buffer considerations at the beginning of Section 6.5 , which you are encouraged to review, hold also for MOSFETs, so our analysis will proceed along the lines of the bipolar case, with special emphasis on the frequency behavior of the terminal impedances.

### Frequency Characteristics of the Source Follower

Figure 6.36 shows the ac equivalent of the source follower, along with its highfrequency model. Since its right plate is grounded, $C_{g d}$ is exempt from the Miller multiplication, so we expect the CD to be an inherently fast configuration. In fact, to develop a quick (if only approximate) feel for the circuit, let us ignore all capacitances except for $C_{g s}$, which is the dominant capacitance in the circuit. We wish to investigate the frequency dependence of the impedance $Z_{i}(j \omega)$ seen by the signal source, the source-to-load voltage gain $a(j \omega)=V_{o} / V_{s i g}$, and the impedance $Z_{o}(j \omega)$ seen by the load.
image_name:(a)
description:
[
'name': 'Vsig', 'type': 'VoltageSource', 'ports': {'Np': 'Vsig', 'Nn': 'GND'
'name': 'Rsig', 'type': 'Resistor', 'value': 'Rsig', 'ports': {'N1': 'Vsig', 'N2': 'Vi'
'name': 'RL', 'type': 'Resistor', 'value': 'RL', 'ports': {'N1': 'Vo', 'N2': 'GND'
'name': 'Vsig', 'type': 'VoltageSource', 'value': 'Vsig', 'ports': {'Np': 'Vsig', 'Nn': 'GND'
]
extrainfo:The circuit diagram (a) represents a source follower configuration. It includes a voltage source Vsig, a resistor Rsig, and a load resistor RL. The circuit is connected to ground (GND) at multiple points, and it investigates the frequency dependence of the impedance Zi seen by the signal source, the source-to-load voltage gain a(jω) = Vo/Vsig, and the impedance Zo seen by the load.
image_name:(b)
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: X1}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
name: Cgb, type: Capacitor, value: Cgb, ports: {Np: X1, Nn: GND}
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: X1, Nn: Vo}
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: X1, Nn: GND}
name: Csb, type: Capacitor, value: Csb, ports: {Np: Vo, Nn: GND}
name: ro, type: Resistor, value: ro, ports: {N1: Vo, N2: GND}
name: gmVgs, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: Vo}
name: gmbVo, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: Vo}
]
extrainfo:This is a high-frequency small-signal model of a source follower. The circuit analyzes the impedance and voltage gain characteristics by considering dominant capacitances and lumped resistances.

FIGURE 6.36 (a) The source follower and (b) its high-frequency small-signal model.
To find the voltage gain, refer to the simplified equivalent of Fig. 6.37, obtained from that of Fig. $6.36 b$ by lumping $R_{L}, r_{o}$, and $1 / g_{m b}$ into a single equivalent resistance,

$$
\begin{equation*}
R_{1}=R_{L} / / r_{o} / / \frac{1}{g_{m b}} \tag{6.70}
\end{equation*}
$$

(Though $C_{g d}$ and $C_{g b}$ are being ignored in the present analysis, they too have been lumped together as they are in parallel in the original circuit). Applying Ohm's law, KCL, and the voltage divider rule, we write

$$
\begin{aligned}
V_{o} & =R_{1}\left(\frac{V_{g s}}{1 /\left(j \omega C_{g s}\right)}+g_{m} V_{g s}\right)=R_{1}\left(j \omega C_{g s}+g_{m}\right) V_{g s} \\
V_{g s} & =\frac{1 / j \omega C_{g s}}{R_{s i g}+1 /\left(j \omega C_{g s}\right)}\left(V_{s i g}-V_{o}\right)=\frac{1}{1+j \omega R_{s i g} C_{g s}}\left(V_{s i g}-V_{o}\right)
\end{aligned}
$$

image_name:FIGURE 6.37
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: V1}
name: Cgs, type: Capacitor, value: Cgs+Cgb, ports: {Np: V1, Nn: Vo}
name: Cgd, type: Capacitor, value: Cgd+Cgb, ports: {Np: V1, Nn: GND}
name: Csb, type: Capacitor, value: Csb, ports: {Np: Vo, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vo, N2: GND}
name: g_mVgs, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: Vo}
]
extrainfo:The circuit is a simplified equivalent model showing voltage and current relationships in a transistor configuration with parasitic capacitances. It illustrates the interaction of input voltage Vsig with the gate-source voltage Vgs, and the effect of transconductance gm on the output voltage Vo.

FIGURE 6.37 Simplified equivalent of the circuit of Fig. 6.36b.

Eliminating $V_{g s}$ and collecting gives

$$
a(j \omega)=\frac{V_{o}}{V_{s i g}}=\frac{g_{m} R_{1}+j \omega R_{1} C_{g s}}{1+g_{m} R_{1}+j \omega\left(R_{s i g}+R_{1}\right) C_{g s}}
$$

With a bit of algebraic manipulation we put gain in the more insightful form advocated in Appendix 6A,

$$
\begin{equation*}
a(j \omega)=a_{0} \frac{1+j \omega / \omega_{z a}}{1+j \omega / \omega_{p a}} \tag{6.71a}
\end{equation*}
$$

where

$$
\begin{equation*}
a_{0}=\frac{1}{1+1 /\left(g_{m} R_{1}\right)} \quad \omega_{z a}=\frac{g_{m}}{C_{g s}} \quad \omega_{p a}=\frac{1+g_{m} R_{1}}{\left(R_{s i g}+R_{1}\right) C_{g s}} \tag{6.71b}
\end{equation*}
$$

For $C_{g d} \ll C_{g s}$ we can approximate $\omega_{z a} \cong \omega_{T}$, by Eq. (6.24). We also note that at sufficiently high frequencies, where $C_{g s}$ acts as a short circuit, $R_{1}$ forms a voltage divider with $R_{s i g}$, resulting in the asymptotic gain value $a_{\infty}=1 /\left(1+R_{s i g} / R_{1}\right)$. One can easily prove that $a_{\infty} / a_{0} \leq 1$ for $g_{m} R_{s i g} \geq 1$, and $a_{\infty} / a_{0} \geq 1$ for $g_{m} R_{s i g} \leq 1$ (this, of course, under the assumption that $C_{g b}, C_{g d}$, and $C_{s b}$ are negligible).

Next, we turn to the impedance $Z_{i}(j \omega)$ seen by the signal source, that is, the impedance seen looking into the gate. Using the test circuit of Fig. 6.38a, one can prove (see Problem 6.24) that

$$
\begin{equation*}
Z_{i}(j \omega)=\frac{V_{i}}{I_{i}}=\frac{1}{j \omega C_{1}}+R_{1} \tag{6.72a}
\end{equation*}
$$

where

$$
\begin{equation*}
C_{1}=\frac{C_{g s}}{1+g_{m} R_{1}} \tag{6.72b}
\end{equation*}
$$

indicating that $Z_{i}$ appears as an equivalent capacitance $C_{1}$ in series with the resistance $R_{1}$. As depicted in Fig. 6.39a, $C_{1}$ dominates at low frequencies, leading to the familiar dc limit $Z_{i 0}=\infty$. At high frequencies, where $C_{g s}$ acts as a short circuit, $R_{1}$ dominates,
image_name:(a)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: Vi, Nn: Vo}
name: Cgd + Cgb, type: Capacitor, value: Cgd + Cgb, ports: {Np: Vi, Nn: GND}
name: Csb, type: Capacitor, value: Csb, ports: {Np: Vo, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vo, N2: GND}
name: g_m V_gs, type: VoltageControlledCurrentSource, ports: {N1: Vi, N2: Vo}
]
extrainfo:The circuit is a typical source-follower configuration with input impedance Zi and output impedance dominated by R1 in parallel with load resistances. The voltage gain is influenced by the transconductance gm and the capacitive elements Cgs, Cgd, and Cgb. The source follower provides a buffer between the input and output, offering high input impedance and low output impedance.

FIGURE 6.38 Finding (a) the impedance $Z_{i}$ seen looking into the gate and (b) $Z_{o}$ seen looking into the source.
image_name:(a)
description:The graph labeled "(a)" is a Bode plot representing the input impedance \( |Z_i(j\omega)| \) of a source follower circuit. The plot is depicted on a logarithmic scale for both axes, with frequency \( \omega \) in decades on the horizontal axis and impedance in decades on the vertical axis.

Overall Behavior and Trends:
- **Initial Decrease:** The graph begins with a downward slope at a rate of \(-1 \text{ dec/dec}\), indicating that the input impedance decreases with increasing frequency.
- **Flat Region:** After reaching a certain frequency \( \omega_{zi} \), the graph levels off to a constant value \( Z_{i\infty} \), representing the high-frequency asymptotic behavior of the input impedance.

Key Features and Technical Details:
- **Slope:** The initial downward slope of \(-1 \text{ dec/dec}\) suggests a single-pole roll-off in the impedance characteristics.
- **Frequency \( \omega_{zi} \):** This is the frequency at which the impedance stops decreasing and becomes constant, marking the transition to the flat region.
- **Asymptotic Value \( Z_{i\infty} \):** The input impedance approaches this constant value at high frequencies, which is determined by the resistive elements in the circuit.

Annotations and Specific Data Points:
- The plot includes a dashed line indicating the slope of \(-1 \text{ dec/dec}\) and a horizontal line at \( Z_{i\infty} \) to mark the steady-state impedance level.

This Bode plot effectively illustrates the frequency-dependent behavior of the input impedance in a source follower configuration, highlighting the transition from a frequency-sensitive region to a frequency-independent region.
image_name:(b)
description:The graph labeled "(b)" is a Bode plot representing the voltage gain \( a(j\omega) \) of a source-follower configuration. The graph has a logarithmic scale on the horizontal axis, labeled \( \omega \) (frequency) in decades, and a linear scale on the vertical axis, labeled \( a(j\omega) \) in decibels (dB).

Overall Behavior and Trends:
- The plot starts with a constant gain \( a_0 \) at low frequencies, indicating a flat response.
- As frequency increases, the gain begins to decrease at a certain point, marked by \( \omega_{pa} \), which is the pole frequency.
- The gain continues to decrease until it reaches another frequency, \( \omega_{za} \), where it stabilizes at a lower constant gain level \( a_\infty \).

Key Features and Technical Details:
- **Initial Gain Level (\( a_0 \))**: The initial gain level is constant at low frequencies.
- **Pole Frequency (\( \omega_{pa} \))**: This is the frequency at which the gain starts to decrease.
- **Zero Frequency (\( \omega_{za} \))**: The frequency where the gain stabilizes at the lower level \( a_\infty \).
- **Final Gain Level (\( a_\infty \))**: The gain stabilizes at this lower level after \( \omega_{za} \).

Annotations and Specific Data Points:
- The \( \omega_{pa} \) and \( \omega_{za} \) are marked on the graph, indicating significant changes in the gain behavior.
- The flat regions at \( a_0 \) and \( a_\infty \) suggest the presence of significant frequency ranges where the gain is stable.

This Bode plot effectively illustrates the frequency-dependent behavior of the voltage gain in the source-follower circuit, highlighting the transition from a higher to a lower gain level as frequency increases.
image_name:(c)
description:The graph labeled (c) is a Bode plot representing the output impedance \( |Z_o(j\omega)| \) as a function of frequency \( \omega \) on a logarithmic scale. The x-axis represents the frequency \( \omega \) in decades, while the y-axis represents the magnitude of the output impedance \( |Z_o(j\omega)| \) also in decades.

Overall Behavior and Trends
The plot shows a general trend of increasing impedance with frequency. Initially, at low frequencies, the output impedance \( Z_{o0} \) remains constant. As the frequency increases, there is a breakpoint at \( \omega_{zo} \), after which the impedance begins to rise linearly at a rate of 1 dec/dec. This linear increase continues until another breakpoint at \( \omega_{po} \), after which the impedance stabilizes at a higher constant value \( Z_{o\infty} \).

Key Features and Technical Details
- **Low-Frequency Plateau:** The impedance starts at a constant low value \( Z_{o0} \).
- **Rising Slope:** After the breakpoint \( \omega_{zo} \), the impedance increases at a rate of 1 decade per decade.
- **High-Frequency Plateau:** Following the breakpoint at \( \omega_{po} \), the impedance levels off at a higher constant value \( Z_{o\infty} \).

Annotations and Specific Data Points
- **Breakpoints:** The significant frequencies are \( \omega_{zo} \) and \( \omega_{po} \), which mark the transitions between the different regions of the plot.
- **Slope:** The slope between \( \omega_{zo} \) and \( \omega_{po} \) is annotated as 1 dec/dec, indicating the rate of increase in impedance.

This graph is crucial for understanding how the output impedance of the source follower circuit changes with frequency, particularly how it transitions from a low to high value across the frequency spectrum.

FIGURE 6.39 Typical source-follower characteristics for $C_{g b}=C_{g d}=C_{s b}=0$ : (a) input impedance $Z_{i}$, (b) voltage gain $a$, and (c) output impedance $Z_{o}$. The plots of $a$ and $Z_{o}$ are for the case $g_{m} R_{s i g} \gg 1$.
giving $Z_{i \infty}=R_{1}$. The zero frequency is $\omega_{z i}=1 /\left(R_{1} C_{1}\right)$. For $g_{m} R_{1} \gg 1$ we can approximate $\omega_{z i} \cong \omega_{T}$.

Finally, to find the impedance $Z_{o}(j \omega)$ seen by the load, we use the test circuit of Fig. 6.38b, where

$$
\begin{equation*}
R_{2}=r_{o} / / \frac{1}{g_{m b}} \tag{6.73}
\end{equation*}
$$

The result (see Problem 6.24) is

$$
\begin{equation*}
Z_{o}(j \omega)=Z_{o 0} \frac{1+j \omega / \omega_{z o}}{1+j \omega / \omega_{p o}} \tag{6.74a}
\end{equation*}
$$

where $Z_{o 0}$ is the familiar low-frequency resistance seen looking into the source terminal, and $\omega_{z o}$ and $\omega_{p o}$ are the zero and pole frequencies,

$$
\begin{equation*}
Z_{o 0}=\frac{1}{g_{m}} / / R_{2} \quad \omega_{z o}=\frac{1}{R_{s i g} C_{g s}} \quad \omega_{p o}=\frac{1+g_{m} R_{2}}{\left(R_{s i g}+R_{2}\right) C_{g s}} \tag{6.74b}
\end{equation*}
$$

By inspection, the high-frequency asymptotic value is $Z_{o \infty}=R_{s i l} / / R_{1}$. One can easily verify that as long as $C_{g b}, C_{g d}$, and $C_{s b}$ can be ignored, $Z_{o}$ is inductive for $g_{m} R_{s i g}>1$ and capacitive for $g_{m} R_{s i g}<1$.
(a) The source follower of Fig. 6.36 uses a FET with $g_{m}=1 \mathrm{~mA} / \mathrm{V}, g_{m b}=$ $0.1 \mathrm{~mA} / \mathrm{V}, r_{o}=50 \mathrm{k} \Omega$, and $C_{g s}=400 \mathrm{fF}$. Moreover, $R_{s i g}=R_{L}=10 \mathrm{k} \Omega$. Assuming $C_{g b}=C_{g d}=C_{s b}=0$, find the frequency characteristics of $Z_{i}, a$, and $Z_{o}$.
(b) Verify with PSpice both for $C_{g b}=C_{g d}=C_{s b}=0$ and for $C_{g b}=C_{g d}=C_{s b}=$ 25 fF , and comment.

#### Solution

We have

$$
\begin{aligned}
& f_{T} \cong \frac{g_{m}}{2 \pi C_{g s}}=\frac{10^{-3}}{2 \pi 400 \times 10^{-12}} \cong 400 \mathrm{MHz} \\
& R_{1}=10 / / 50 / / \frac{1}{0.1}=4.55 \mathrm{k} \Omega
\end{aligned}
$$

$C_{1}=\frac{400}{1+1 \times 4.55} \cong 72 \mathrm{fF}$
$R_{2}=50 / / \frac{1}{0.1}=8.33 \mathrm{k} \Omega$
By Eq. (6.72) the impedance seen by the signal source is
$Z_{i}=\left(\frac{1}{j 2 \pi f \times 72 \times 10^{-15}}+4.55 \times 10^{3}\right) \Omega=\left(\frac{-j 2.21 \times 10^{9}}{f}+4.55\right) \mathrm{k} \Omega$
which has a zero frequency is $f_{z i}=1 /\left(2 \pi R_{1} C_{1}\right)=486 \mathrm{MHz}$. By Eq. (6.71) the gain parameters are
$a_{0}=\frac{1}{1+1 /(1 \times 4.55)}=0.820 \mathrm{~V} / \mathrm{V}=-1.72 \mathrm{~dB}$
$a_{\infty}=\frac{1}{1+10 / 4.55}=0.312 \mathrm{~V} / \mathrm{V}=-10.1 \mathrm{~dB}$
$f_{z a}=400 \mathrm{MHz}$
$f_{p a}=\frac{1+1 \times 4.55}{2 \pi(10+4.55) 10^{3} \times 400 \times 10^{-15}}=152 \mathrm{MHz}$
By. Eq. (6.74) the parameters of the impedance seen by the load are
$Z_{o 0}=\frac{1}{1} / / 8.33=0.893 \mathrm{k} \Omega \quad Z_{o \infty}=10 / / 8.33=4.55 \mathrm{k} \Omega$
$f_{z o}=\frac{1 /(2 \pi)}{10^{4} \times 400 \times 10^{-15}} \cong 40 \mathrm{MHz}$
$f_{p o}=\frac{1+1 \times 8.33}{2 \pi(10+8.33) 10^{3} \times 400 \times 10^{-15}}=202 \mathrm{MHz}$
It is apparent that $Z_{o}$ is inductive, at least up to a point.
(b) Adapting the PSpice circuit of Fig. 6.32 to the present case we obtain the frequency plots of Fig. 6.40. The asymptotic values and break frequencies are in good agreement with the estimated ones under the assumption $C_{g b}=C_{g d}=$ $C_{s b}=0$. With $C_{g b}=C_{g d}=C_{s b}=25 \mathrm{fF}$, the high-frequency asymptotic values tend to zero, turning $Z_{o}$ from inductive to capacitive at high frequencies.
image_name:(a)
description:The graph labeled "(a)" is a Bode plot depicting the magnitude of the input impedance |Z_i| in ohms (Ω) versus frequency f in hertz (Hz). The x-axis is logarithmically scaled, ranging from 10^7 Hz to 10^10 Hz, while the y-axis, also logarithmic, spans from 10^2 Ω to 10^6 Ω. Two plots are shown on the graph, representing different capacitance conditions: \(C_{gb} = C_{gd} = C_{db} = 0\) and \(C_{gb} = C_{gd} = C_{db} = 25\) fF.

**Overall Behavior and Trends:**
- For \(C_{gb} = C_{gd} = C_{db} = 0\), the impedance starts at around 10^6 Ω at lower frequencies and decreases steadily as frequency increases, indicating a primarily inductive behavior.
- For \(C_{gb} = C_{gd} = C_{db} = 25\) fF, the impedance also begins at a high value but decreases more rapidly, showing capacitive effects at higher frequencies.

**Key Features and Technical Details:**
- The plots show a clear downward slope across the frequency range, with the impedance decreasing by approximately two orders of magnitude.
- The break frequencies are aligned at around 10^8 Hz and 10^9 Hz, where the rate of decrease changes, indicating a shift in the impedance characteristics.

**Annotations and Specific Data Points:**
- The graph includes annotations showing the capacitance conditions for each curve, with gridlines marking significant frequency points at 10^8 Hz and 10^9 Hz.

This graph provides insight into how varying capacitance values affect the input impedance of a MOS current buffer across a range of frequencies, highlighting the transition from inductive to capacitive behavior.
image_name:(b)
description:The graph labeled "(b)" is a Bode plot showing the gain in decibels (dB) as a function of frequency in hertz (Hz). The x-axis represents the frequency, ranging from 10^7 Hz to 10^10 Hz, using a logarithmic scale. The y-axis represents the gain, which ranges from -15 dB to 0 dB.

Two curves are plotted on the graph. The first curve, shown in grey, represents the scenario where the capacitances C_{gb}, C_{gd}, and C_{db} are all zero. The second curve, shown in black, represents the scenario where these capacitances are each 25 fF.

For the scenario with zero capacitances, the gain starts at approximately 0 dB at lower frequencies and begins to decrease sharply just before 10^9 Hz, continuing to decrease beyond this frequency.

For the scenario with 25 fF capacitances, the gain starts at a slightly lower value than the zero capacitance scenario at lower frequencies. It decreases more gradually compared to the zero capacitance scenario, starting to drop significantly after 10^8 Hz, and continues to decline past 10^9 Hz.

The graph illustrates the impact of parasitic capacitances on the gain of the circuit, showing that the presence of these capacitances reduces the gain more significantly at high frequencies.
image_name:(c)
description:The graph labeled (c) is a Bode plot showing the magnitude of the output impedance, \(|Z_{o}|\), as a function of frequency, \(f\), measured in hertz (Hz). The x-axis is logarithmically scaled, ranging from \(10^7\) Hz to \(10^{10}\) Hz, while the y-axis represents the magnitude of the impedance in ohms (\(\Omega\)), also on a logarithmic scale, ranging from \(10^2\) to \(10^4\) \(\Omega\).

**Overall Behavior and Trends:**
- The graph depicts two curves representing different capacitance conditions: \(C_{gb} = C_{gd} = C_{db} = 0\) and \(C_{gb} = C_{gd} = C_{db} = 25\) fF.
- For \(C_{gb} = C_{gd} = C_{db} = 0\), the curve starts at around \(10^3\) \(\Omega\) and rises slightly, reaching a peak just below \(10^4\) \(\Omega\) at around \(10^9\) Hz, before declining.
- For \(C_{gb} = C_{gd} = C_{db} = 25\) fF, the curve begins similarly but rises more sharply to a peak above \(10^3\) \(\Omega\) at a slightly higher frequency, then decreases beyond \(10^9\) Hz.

**Key Features and Technical Details:**
- The peak in both curves indicates a resonant behavior in the system's output impedance.
- The presence of capacitance \(C_{gb}, C_{gd}, C_{db} = 25\) fF shifts the peak slightly higher in frequency and increases the peak magnitude compared to when the capacitances are zero.
- Beyond the peak frequency, both curves show a downward trend, indicating a decrease in impedance with increasing frequency.

**Annotations and Specific Data Points:**
- The graph is annotated with the capacitance values used for each curve, emphasizing the impact of these capacitances on the impedance behavior.
- Gridlines at \(10^8\) and \(10^9\) Hz help in identifying the frequency range of interest and the location of the peaks.

FIGURE 6.40 Gain and impedance plots for the source follower of Example 6.14.

### Frequency Characteristics of MOS Current Buffers

Figure 6.41 shows the ac equivalent of the MOS current buffer, along with its highfrequency model. Like the CD configuration, the CG configuration is inherently fast because $C_{g d}$ is exempt from the Miller effect. We wish to find the impedance $Z_{i}(j \omega)$ seen looking into the source terminal, the current gain $a(j \omega)=I_{o} / I_{i}$, and the impedance $Z_{o}(j \omega)$ seen looking into the drain. To this end, refer to the more compact equivalent of Fig. 6.42, obtained by lumping together the capacitances as shown.
image_name:(a)
description:
[
name: RL, type: Resistor, value: RL, ports: {N1: X1, N2: GND}
name: M1, type: PMOS, ports: {S: X2, D: X1, G: GND}
name: Ii, type: CurrentSource, value: Ii, ports: {Np: X2, Nn: GND}
]
extrainfo:The circuit is a MOS current buffer with a PMOS transistor M1. The input current Ii flows into the gate of M1, and the output current Io flows through RL. The impedance Zi is seen looking into the source terminal, and Zo is seen looking into the drain.

(a)
image_name:(b)
description:
[
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: Vi, Nn: GND}
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: X1, Nn: GND}
name: Csb, type: Capacitor, value: Csb, ports: {Np: Vi, Nn: GND}
name: ro, type: Resistor, value: ro, ports: {N1: X1, N2: Vi}
name: Cdb, type: Capacitor, value: Cdb, ports: {Np: X1, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: X1, N2: GND}
name: Ii, type: CurrentSource, value: Ii, ports: {Np: GND, Nn: Vi}
]
extrainfo:The circuit is a high-frequency small-signal model of a MOS current buffer. It includes various capacitive and resistive elements to model the frequency response. The input impedance Zi and the output impedance Zo are key parameters of interest. The circuit simplifies analysis by assuming ro is infinite, which isolates the input and output ports.

(b)

FIGURE 6.41 (a) The MOS current buffer and (b) its high-frequency small-signal model.

To gain quick insight into the frequency dependence of $Z_{i}$ and $a$ it is convenient to ignore $r_{o}$ for then the input port is isolated from the output port and can thus be analyzed separately. KCL at the input node gives, for $r_{o} \rightarrow \infty$,

$$
I_{i}=\left(g_{m}+g_{m b}\right) V_{i}+\frac{V_{i}}{1 /\left[j \omega\left(C_{g s}+C_{s b}\right)\right]}=\left(g_{m}+g_{m b}\right)\left[1+\frac{j \omega\left(C_{g s}+C_{s b}\right)}{g_{m}+g_{m b}}\right] V_{i}
$$

image_name:FIGURE 6.42
description:
[
'name': 'Ii', 'type': 'CurrentSource', 'value': 'Ii', 'ports': {'Np': 'GND', 'Nn': 'Vi'
'name': 'ro', 'type': 'Resistor', 'value': 'ro', 'ports': {'N1': 'X1', 'N2': 'X2'
'name': 'Cgs+Csb', 'type': 'Capacitor', 'value': 'Cgs+Csb', 'ports': {'Np': 'Vi', 'Nn': 'GND'
'name': 'Cgd+Cdb', 'type': 'Capacitor', 'value': 'Cgd+Cdb', 'ports': {'Np': 'X1', 'Nn': 'GND'
'name': 'RL', 'type': 'Resistor', 'value': 'RL', 'ports': {'N1': 'X1', 'N2': 'GND'
'name': '(gm+gmb)Vi', 'type': 'VoltageControlledCurrentSource', 'ports': {'Np': 'Vi', 'Nn': 'X1'
]
extrainfo:The circuit is a MOS current buffer with input impedance Zi and output impedance Zo. It includes a voltage-controlled current source (gm+gmb)Vi, and the capacitors Cgs+Csb and Cgd+Cdb represent parasitic capacitances. The resistor RL is connected to the output node.

FIGURE 6.42 Compact rendition of the MOS current buffer.

Consequently, the impedance seen by the signal source is

$$
\begin{equation*}
Z_{i}=\frac{V_{i}}{I_{i}}=\frac{1}{g_{m}+g_{m b}} \times \frac{1}{1+j \omega / \omega_{p i}} \quad \omega_{p i}=\frac{g_{m}+g_{m b}}{C_{g s}+C_{s b}} \tag{6.75}
\end{equation*}
$$

The current into a short-circuit load $\left(R_{L}=0\right)$ is, for $r_{o} \rightarrow \infty, I_{o(\mathrm{sc})}=\left(g_{m}+g_{m b}\right) V_{i}=$ $\left(g_{m}+g_{m b}\right) Z_{i} I_{i}$, so the short-circuit current gain is

$$
\begin{equation*}
\alpha(j \omega)=\frac{I_{o(\mathrm{sc})}}{I_{i}}=\frac{1}{1+j \omega / \omega_{p i}} \tag{6.76}
\end{equation*}
$$

with $\omega_{p i}$ as given in Eq. (6.75). Once it reaches the drain node, $I_{o(\mathrm{sc})}$ divides between $R_{L}$ and the capacitance pair $C_{g d}+C_{d b}$, so we use the current-divider rule to write, for $r_{o} \rightarrow \infty$,

$$
I_{o}=\frac{1 /\left[j \omega\left(C_{g d}+C_{d b}\right)\right]}{R_{L}+1 /\left[j \omega\left(C_{g d}+C_{d b}\right)\right]} \alpha(j \omega) I_{i}=\frac{\alpha(j \omega)}{1+j \omega R_{L}\left(C_{g d}+C_{d b}\right)} I_{i}
$$

Substituting Eq. (6.76), we finally obtain the overall current gain

$$
\begin{equation*}
a(j \omega)=\frac{I_{o}}{I_{i}} \cong \frac{1}{\left(1+j \omega / \omega_{p i}\right)\left(1+j \omega / \omega_{L}\right)} \quad \omega_{L} \cong \frac{1}{R_{L}\left(C_{g d}+C_{d b}\right)} \tag{6.77}
\end{equation*}
$$

It is apparent that the CG configuration provides its maximum bandwidth of $\omega_{p i}\left(\cong \omega_{T}\right)$ when the load is a short circuit. For $R_{L} \neq 0$, the additional pole formed by $R_{L}$ with the effective drain capacitance $C_{g d}+C_{d b}$ reduces the bandwidth accordingly.

It is left as an exercise (see Problem 6.28) to prove that the impedance seen by the load is

$$
\begin{gather*}
Z_{o}(j \omega)=\frac{1}{j \omega C_{o}} \times \frac{1+j \omega / \omega_{z o}}{1+j \omega / \omega_{p o}} \quad C_{o}=C_{g d}+C_{d b}+\frac{C_{g s}+C_{s b}}{1+\left(g_{m}+g_{m b}\right) r_{o}}  \tag{6.78a}\\
\omega_{z o}=\frac{1+\left(g_{m}+g_{m b}\right) r_{o}}{r_{o}\left(C_{g s}+C_{s b}\right)} \quad \omega_{p o}=\omega_{z o}+\frac{1}{r_{o}\left(C_{g d}+C_{d b}\right)} \tag{6.78b}
\end{gather*}
$$

The frequency dependence of $Z_{o}$ is dominated by $C_{o}$, and $Z_{o 0} \rightarrow \infty$ at dc because the signal source has been assumed ideal. A practical signal source will have $R_{s i g}<\infty$, in which case we can approximate

$$
\begin{equation*}
Z_{o}(j \omega) \cong \frac{Z_{o 0}}{1+j \omega / \omega_{o}} \quad Z_{o 0}=r_{o}+\left[1+\left(g_{m}+g_{m b}\right) r_{o}\right] R_{s i g} \quad \omega_{o}=\frac{1}{Z_{o 0} C_{o}} \tag{6.79}
\end{equation*}
$$

The CG configuration is investigated further in the end-of-chapter problems.

## 6.7 OPEN-CIRCUIT TIME-CONSTANT (OCTC) ANALYSIS

The preceding sections indicate that ac analysis can become fairly complex even in the case of simple circuits such as single-transistor stages. As the capacitor count increases, exact analysis by paper and pencil may soon become prohibitive. Yet, in everyday practice a designer must be able to come up with quick, if approximate, estimates of a circuit's most salient ac characteristics, such as its $-3-\mathrm{dB}$ frequency,
and identify what changes need to be made in case the circuit fails to meet the specifications. Then, we turn to computer simulation to verify the modified design.

If the circuit contains a single pole, its $-3-\mathrm{dB}$ frequency is the pole frequency itself. Even if it contains additional poles and/or zeros but at sufficiently higher frequencies, $\omega_{-3 \mathrm{~dB}}$ will still be close to the frequency of the lowest pole, aptly referred to as the dominant pole. Eloquent examples were offered by the common-emitter/commonsource amplifiers of Section 6.3, where we used the Miller approximation to speed up the estimation of $\omega_{-3 \mathrm{~dB}}$. We wonder whether there is a quick way to estimate $\omega_{-3 \mathrm{~dB}}$ also in a multi-pole circuit. A widely used such technique is the Open-Circuit TimeConstant (OCTC) Analysis Technique pioneered by P. E. Gray and C. L. Searle in 1969. ${ }^{2}$

To develop an intuitive feel for this technique, start out with a circuit containing a single capacitor $C_{k}$. As we know, a pole arises at the frequency $\omega_{k}$ at which the impedance of $C_{k}$ equals, in magnitude, the equivalent resistance $R_{k}$ presented to $C_{k}$ by the surrounding circuit, a condition that we express as $1 /\left(\omega_{k} C_{k}\right)=R_{k}$. This gives $\omega_{k}=1 / \tau_{k}$, where $\tau_{k}=R_{k} C_{k}$ is the time constant formed by $C_{k}$ and $R_{k}$. As a function of frequency, $C_{k}$ starts out as an open circuit for $\omega \ll \omega_{k}$, it presents an impedance equal in magnitude to $R_{k}$ at $\omega=\omega_{k}$, and it becomes a short circuit for $\omega \gg \omega_{p}$.

What if the circuit contains more than just one capacitance? If there is a dominant pole, we can say that at that pole frequency all capacitances still act as open circuits, except for the capacitance responsible for that one pole, which will exhibit an impedance equal in magnitude to the resistance presented by the surrounding circuit. To find which capacitance is responsible for the dominant pole we need to test one capacitance at a time, assuming all remaining capacitances are acting as open circuits. We find the equivalent resistance seen by the capacitance under scrutiny, and we calculate the corresponding time constant. We repeat this procedure for each capacitance present, and finally we let $\omega_{-3 \mathrm{~dB}} \cong 1 / \tau_{D}$, where $\tau_{D}$ is by far the longest and thus dominant time constant.

What if there isn't a definite dominant time constant in the circuit? The information gathered is still useful, for the OCTC technique states that we can estimate the $-3-\mathrm{dB}$ frequency $\mathrm{as}^{2}$

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}} \cong \frac{1}{R_{1} C_{1}+R_{2} C_{2}+\cdots+R_{n} C_{n}} \tag{6.80}
\end{equation*}
$$

where $R_{i}$ is the equivalent resistance seen by the capacitance $C_{i}(i=1,2, \ldots n)$ with all other capacitances open-circuited. Note that this technique provides no information about higher-order poles and possibly zeros. It gives only an estimate of the $-3-\mathrm{dB}$ frequency, also called the half-power bandwidth, but via $n$ simple time-constant calculations. Moreover, by showing explicitly which time constant contributes most heavily to the $-3-\mathrm{dB}$ frequency, it pinpoints the parameters that need to be altered if the design fails to meet specific bandwidth requirements. Some examples will better illustrate the OCTC technique.

### OCTC Analysis of the CE/CS Amplifiers

As our first application of the open-circuit time-constant (OCTC) technique, let us return to the circuit of Fig. 6.21 (repeated in Fig. 6.43), representing the com-mon-emitter/common-source voltage amplifier. With three capacitances present
image_name:FIGURE 6.43
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vi, N2: V1}
name: C1, type: Capacitor, value: C1, ports: {Np: V1, Nn: GND}
name: Cf, type: Capacitor, value: Cf, ports: {Np: V1, Nn: Vo}
name: gmV1, type: VoltageControlledCurrentSource, value: gmV1, ports: {Np: Vo, Nn: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vo, N2: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: Vo, Nn: GND}
]
extrainfo:The circuit is a common-emitter/common-source voltage amplifier with three capacitors: C1, Cf, and C2. It includes a voltage-controlled current source (gmV1) and two resistors (R1 and R2). The circuit is designed for OCTC analysis, focusing on the resistances seen by the capacitors.

FIGURE 6.43 Revisiting the CE/CS amplifier.
$\left(C_{1}, C_{2}\right.$, and $C_{f}$ ), we need to find three open-circuit equivalent resistances. With reference to Fig. 6.44a, it is apparent that the resistances seen by $C_{1}$ and $C_{2}$ are just $R_{1}$ and $R_{2}$. However, to find $R_{f}$, we can no longer rely on mere inspection, as the presence of the dependent source mandates using the test method instead. With reference to Fig. $6.44 b$ we have, by Ohm's law, $v_{1}=R_{1} i$. By KCL, $R_{2}$ must supply the current $i+g_{m} v_{1}=i+g_{m} R_{1} i$, so $v_{2}=-R_{2}\left(i+g_{m} R_{1} i\right)=-R_{2}\left(1+g_{m} R_{1}\right) i$. By KVL,

$$
v=v_{1}-v_{2}=R_{1} i-\left[-R_{2}\left(1+g_{m} R_{1}\right) i\right]
$$

so, taking the ratio $R_{f}=v / i$ we get

$$
\begin{equation*}
R_{f}=R_{1}+R_{2}+g_{m} R_{1} R_{2} \tag{6.81}
\end{equation*}
$$

Finally, we estimate the 3-dB frequency using Eq. (6.80),

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}} \cong \frac{1}{R_{1} C_{1}+R_{f} C_{f}+R_{2} C_{2}}=\frac{1}{R_{1} C_{1}+\left(R_{1}+R_{2}+g_{m} R_{1} R_{2}\right) C_{f}+R_{2} C_{2}} \tag{6.82}
\end{equation*}
$$

Aside from a rearrangement of its denominator terms, Eq. (6.82) is identical to Eq. (6.45), which was obtained via the much more laborious exact analysis. Of course, exact analysis provides information also about the higher order pole and zero frequencies, while the OCTC method estimates only $\omega_{-3 \mathrm{~dB}}$. But this is often all the designer wants to know, so if we consider the much simpler calculations required
image_name:(a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: V1, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vout, N2: GND}
name: gmv1, type: VoltageControlledCurrentSource, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a generalized voltage amplifier using the OCTC method to estimate the -3dB frequency. It includes a voltage-controlled current source and feedback resistor.
image_name:(b)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: V1, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: V2, N2: GND}
name: gmv1, type: VoltageControlledCurrentSource, ports: {Np: v2, Nn: GND}
name: i, type: CurrentSource, ports: {Np: v1, Nn: v2}
]
extrainfo:The circuit is a generalized voltage amplifier using a voltage-controlled current source (gmv1) to provide feedback. The resistors R1 and Rf form a feedback network, and R2 is connected to the output. V1 is the input voltage source, and V2 is an additional voltage source connected to the output.

FIGURE 6.44 (a) The open-circuit resistances seen by the capacitances in the generalized voltage amplifier of Fig. 6.43. (b) Using the test method to find $R_{f}$
by the OCTC technique, the latter is a powerful tool indeed. As a final remark, we observe that if we define the multiplier term

$$
\begin{equation*}
M=1+g_{m} R_{2}+\frac{R_{2}}{R_{1}} \tag{6.83}
\end{equation*}
$$

then the time constant $\tau_{f}$ associated with $C_{f}$ is expressed as $\tau_{f}=\left(R_{1} M\right) C_{f}$ in the OCTC approximation, but as $\tau_{f}=R_{1}\left(M C_{f}\right)$ in the Miller approximation. We have two different viewpoints for the same result!

Reconsider the CE amplifier of Example 6.8, for which $g_{m}=1 /(26 \Omega)$, $R_{1}=0.975 \mathrm{k} \Omega, R_{2}=4.55 \mathrm{k} \Omega, C_{\pi}=12 \mathrm{pF}, C_{\mu}=0.5 \mathrm{pF}$ and $C_{s}=1 \mathrm{pF}$.
(a) Estimate $f_{-3 \mathrm{~dB}}$ via the OCTC method, and comment on which capacitor contributes the most and which the least to the dominant-pole frequency.
(b) Propose a way to increase the circuit's bandwidth without reducing its low-frequency gain $a_{0}$.

#### Solution

(a) By inspection, the resistances seen by $C_{\pi}$ and $C_{s}$ are, respectively, $R_{\pi}=0.975 \mathrm{k} \Omega$ and $R_{s}=4.55 \mathrm{k} \Omega$. Adapting Eq. (6.81) to the present case we get $R_{\mu}=0.975+$ $4.55+0.975 \times 4.55 / 0.026=176 \mathrm{k} \Omega$. With resistances in $\mathrm{k} \Omega\left(10^{3}\right)$ and capacitances in $\mathrm{pF}\left(10^{-12}\right)$, the time constants in Eq. (6.82) will be in $\mathrm{ns}\left(10^{-9}\right)$,

$$
\begin{aligned}
f_{-3 \mathrm{~dB}} & \cong \frac{1 / 2 \pi}{(0.975 \times 12+176 \times 0.5+4.55 \times 1) \mathrm{ns}} \\
& =\frac{1 / 2 \pi}{(11.7+88+4.6) \mathrm{ns}}=1.53 \mathrm{MHz}
\end{aligned}
$$

This is in excellent agreement with Example 6.8. As expected, the main band-limiting culprit is the time constant associated with $C_{\mu}$, whereas that associated with $C_{s}$ counts the least.
(b) An obvious way to increase the bandwidth is to reduce $R_{\mu}$ as it intervenes in the longest time constant. By Eq. (6.81), this resistance depends both on $R_{1}$ and $R_{2}$. To avoid significantly perturbing the low-frequency gain $a_{0}$, don't change $R_{2}$. This leaves $R_{1}$, which can be reduced by driving the amplifier with a low output-impedance signal source. In the limit $R_{s i g} \rightarrow 0$ we have $R_{1}=r_{n} / / r_{b}$, so

$$
\begin{aligned}
& R_{\pi}=R_{1}=5.2 / / 0.2=0.193 \mathrm{k} \Omega \\
& R_{\mu}=0.193+4.55+0.193 \times 4.55 / 0.026=38.4 \mathrm{k} \Omega
\end{aligned}
$$

Consequently, in the limit $R_{s i g} \rightarrow 0$ we get

$$
\begin{aligned}
f_{-3 \mathrm{~dB}} & \cong \frac{1 / 2 \pi}{(0.193 \times 12+38.4 \times 0.5+4.55 \times 1) \mathrm{ns}} \\
& =\frac{1 / 2 \pi}{(2.3+19.2+4.6) \mathrm{ns}} \cong 6 \mathrm{MHz}
\end{aligned}
$$

indicating a bandwidth expansion of almost two octaves. (It can be seen that with $R_{s i g}=0, a_{0}$ is raised from $-142 \mathrm{~V} / \mathrm{V}$ to $-169 \mathrm{~V} / \mathrm{V}$. Usually this is not a problem, but if it is, we can always tweak with the value of $R_{2}$ to re-establish the original gain.)

Remark: If the available signal source doesn't have a sufficiently low $R_{s i g}$, we can interpose a voltage buffer between source and amplifier. A buffer provides high input impedance, low output impedance, and close-to-unity gain over a much wider bandwidth than the voltage amplifier under consideration, so it will serve the required function of impedance translation quite well.

EXAMPLE 6.16 Reconsider the CS amplifier of Exercise 6.3, for which $g_{m}=4 \mathrm{~mA} / \mathrm{V}, R_{1}=10 \mathrm{k} \Omega$, $R_{2}=4.55 \mathrm{k} \Omega, C_{g s}=1.17 \mathrm{pF}$, and $C_{g d}=0.1 \mathrm{pF}$. Assuming $C_{d b}=0.2 \mathrm{pF}$, estimate $f_{-3 \mathrm{~dB}}$ via the OCTC method.

#### Solution

By inspection, $R_{g s}=10 \mathrm{k} \Omega$ and $R_{d b}=4.55 \mathrm{k} \Omega$. Adapting Eq. (6.81) to the present case, $R_{g d}=10+4.55+4 \times 10 \times 4.55=196 \mathrm{k} \Omega$. With resistances in $\mathrm{k} \Omega$ and capacitances in pF , the time constants will be in ns ,

$$
\begin{aligned}
f_{-3 \mathrm{~dB}} & \cong \frac{1 / 2 \pi}{(10 \times 1.17+196 \times 0.1+4.55 \times 0.2) \mathrm{ns}} \\
& =\frac{1 / 2 \pi}{(11.7+19.6+0.91) \mathrm{ns}}=4.9 \mathrm{MHz}
\end{aligned}
$$

in close agreement with Exercise 6.3.

### OCTC Analysis of Voltage Buffers

The emitter follower of Fig. 6.30b, repeated for convenience in Fig. 6.45, was analyzed under the assumption $C_{\mu}=0$ to keep the derivations manageable. We now wish to estimate its $-3-\mathrm{dB}$ frequency via the OCTC technique, but with $C_{\mu}$ present. To find the open-circuit equivalent resistances, use the circuit of Fig. $6.46 a$ with $R_{1}=R_{s i g}+r_{b}$ and $R_{2}=R_{L} / / r_{o}$, as shown. With reference to the node common to $R_{1}$ and $r_{\pi}$ we observe that looking to the left we see $R_{1}$, and looking down toward the right we see $r_{\pi}+\left(\beta_{0}+1\right) R_{2}$, so the resistance seen by $C_{\mu}$ is

$$
\begin{equation*}
R_{\mu}=R_{1} / /\left[r_{\pi}+\left(\beta_{0}+1\right) R_{2}\right] \tag{6.84}
\end{equation*}
$$

To find $R_{\pi}$ we need to apply the test method of Fig. 6.46b. By KCL, the current into $R_{1}$ is $i_{1}=i-v / r_{\pi}$ and that into $R_{2}$ is $i_{2}=v / r_{\pi}+g_{m} v-i$, so we can write

$$
v=R_{1} i_{1}-R_{2} i_{2}=R_{1}\left(i-\frac{v}{r_{\pi}}\right)-R_{2}\left(\frac{v}{r_{\pi}}+g_{m} v-i\right)
$$

image_name:FIGURE 6.45
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: V1}
name: rb, type: Resistor, value: rb, ports: {N1: V1, N2: V2}
name: rπ, type: Resistor, value: rπ, ports: {N1: V2, N2: Vo}
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: V2, Nn: Vo}
name: Cμ, type: Capacitor, value: Cμ, ports: {Np: V2, Nn: GND}
name: gmVπ, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: Vo}
name: ro, type: Resistor, value: ro, ports: {N1: Vo, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:This circuit is an amplifier with a voltage-controlled current source and includes multiple resistors and capacitors for stabilization and filtering. The input is provided by a voltage source Vsig, and the output is taken across RL. The circuit uses a feedback mechanism through the capacitor Cμ and the voltage-controlled current source gmVπ.

FIGURE 6.45 Revisiting the emitter follower.
Collecting and taking the ratio $R_{\pi}=v / i$ we get, after some algebra,

$$
\begin{equation*}
R_{\pi}=r_{\pi} / / \frac{R_{1}+R_{2}}{1+g_{m} R_{2}} \tag{6.85}
\end{equation*}
$$

Finally,

$$
\begin{align*}
\omega_{-3 \mathrm{~dB}} & \cong \frac{1}{R_{\pi} C_{\pi}+R_{\mu} C_{\mu}} \\
& =\frac{1}{\left\{r_{\pi} / /\left[\left(R_{1}+R_{2}\right) /\left(1+g_{m} R_{2}\right)\right]\right\} C_{\pi}+\left\{R_{1} / /\left[r_{\pi}+\left(\beta_{0}+1\right) R_{2}\right]\right\} C_{\mu}} \tag{6.86}
\end{align*}
$$

image_name:(a)
description:
[
name: R1, type: Resistor, value: Rsig + rb, ports: {N1: GND, N2: V1}
name: rπ, type: Resistor, value: rπ, ports: {N1: V1, N2: V2}
name: R2, type: Resistor, value: RL // ro, ports: {N1: V2, N2: GND}
name: gmvπ, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: V2}
]
extrainfo:The circuit diagram (a) is an emitter follower configuration showing open-circuit resistances seen by the capacitances. It includes resistors R1, rπ, Rμ, Rπ, and R2, and a voltage-controlled current source gmvπ. The resistors and current source are interconnected with nodes labeled V1, Vπ, V2, and GND.
image_name:(b)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: GND, N2: V1}
name: rπ, type: Resistor, value: rπ, ports: {N1: V1, N2: V2}
name: R2, type: Resistor, value: R2, ports: {N1: V2, N2: GND}
name: i, type: CurrentSource, ports: {Np: V1, Nn: V2}
name: gₘv, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: V2}
]
extrainfo:The circuit diagram (b) represents an emitter follower configuration with resistors R1 and R2, a resistor rπ, and a voltage-controlled current source gₘv. The node V1 is connected to the input, and V2 is connected to the output. The ground (GND) is used as a reference point for the circuit.

FIGURE 6.46 (a) The open-circuit resistances seen by the capacitances of the emitter follower of Fig. 6.45. (b) Using the test method to find $R_{\pi}$.

Reconsider the emitter follower of Example 6.11, for which $\beta_{0}=150, g_{m}=$
EXAMPLE 6.17 $1 /(13 \Omega), r_{\pi}=1.95 \mathrm{k} \Omega, R_{1}=2.2 \mathrm{k} \Omega, R_{2}=4.44 \mathrm{k} \Omega, C_{\pi}=29.6 \mathrm{pF}$, and $C_{\mu}=$ 1 pF . Estimate $f_{-3 \mathrm{~dB}}$ via the OCTC method, comment.

#### Solution

By Eqs. (6.84) through (6.86), we have

$$
R_{\pi}=1.95 / / \frac{2.2+4.44}{1+4.44 / 0.013} \mathrm{k} \Omega=19.2 \Omega
$$

$$
\begin{aligned}
R_{\mu}= & 2.2 / /(1.95+151 \times 4.44)=2.19 \mathrm{k} \Omega \\
f_{-3 \mathrm{~dB}} & \cong \frac{1 / 2 \pi}{19.2 \times 29.6 \times 10^{-12}+2.19 \times 10^{3} \times 10^{-12}} \\
& =\frac{1 / 2 \pi}{(0.57+2.19) \mathrm{ns}}=58 \mathrm{MHz}
\end{aligned}
$$

This estimate is in reasonable agreement with the value of 66 MHz obtained via the PSpice circuit of Fig. 6.32. Clearly, the time constant due to $C_{\mu}$ is the dominant one in this case.
image_name:Figure 6.47
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: V1}
name: Cgb, type: Capacitor, value: Cgb, ports: {Np: V1, Nn: GND}
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: V1, Nn: Vo}
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: V1, Nn: Vo}
name: g_mVgs, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: Vo}
name: g_mbVo, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: Vo}
name: Cs, type: Capacitor, value: Cs, ports: {Np: Vo, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
name: ro, type: Resistor, value: ro, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a source follower configuration with capacitors Cgb, Cgs, Cgd, and Cs. It includes voltage-controlled current sources g_mVgs and g_mbVo. The output node is Vo, and the input is Vsig.

Next, we turn to the source follower of Fig. $6.36 b$, repeated for convenience in Fig. 6.47. To find its open-circuit equivalent resistances we rearrange it in the form of Fig. 6.48. By inspection,

$$
\begin{equation*}
R_{g b}=R_{s i g} \quad R_{s b}=R_{L} / / r_{o} / / \frac{1}{g_{m b}} / / / \frac{1}{g_{m}} \tag{6.87}
\end{equation*}
$$

image_name:FIGURE 6.48
description:
[
name: R1, type: Resistor, value: Rsig, ports: {N1: V2, N2: GND}
name: R2, type: Resistor, value: RL//ro//1/gmb, ports: {N1: V1, N2: GND}
name: gmvgs, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: V1}
]
extrainfo:The circuit is a source follower with resistors and a voltage-controlled current source. It includes open-circuit resistances Rgb, Rgs, Rgd, and Rsb, with the input at V2 and the output at V1. The voltage-controlled current source is controlled by the voltage Vgs.

FIGURE 6.48 The open-circuit resistances seen by the capacitances in the source follower of Fig. 6.47.

To find $R_{g s}$ and $R_{g d}$ we note this circuit's similarity to its bipolar counterpart of Fig. 6.46, except that now $r_{\pi} \rightarrow \infty$. To save labor we thus recycle Eqs. (6.84) and (6.85) by letting $r_{\pi} \rightarrow \infty$ and $\beta_{0} \rightarrow \infty$, and get

$$
\begin{equation*}
R_{g d}=R_{1}=R_{s i g} \quad R_{g s}=\frac{R_{1}+R_{2}}{1+g_{m} R_{2}}=\frac{R_{s i g}+\left[R_{L} / / r_{o} / /\left(1 / g_{m b}\right)\right]}{1+g_{m}\left[R_{L} / / r_{o} / /\left(1 / g_{m b}\right)\right]} \tag{6.88}
\end{equation*}
$$

We now have all the parameters needed to estimate $f_{-3 \mathrm{~dB}}$.

#### Exercise 6.5

Reconsider the source follower of Example 6.14, having $g_{m}=1 \mathrm{~mA} / \mathrm{V}, g_{m b}=$ $0.1 \mathrm{~mA} / \mathrm{V}, r_{o}=50 \mathrm{k} \Omega, C_{g s}=400 \mathrm{fF}, C_{g b}=C_{g d}=C_{s b}=25 \mathrm{fF}$, and $R_{s i g}=R_{L}=$ $10 \mathrm{k} \Omega$. Use the OCTC technique to estimate $f_{-3 \mathrm{~dB}}$.
Ans. 122 MHz.

### Voltage Amplifiers with Emitter/Source Degeneration

Recall that degeneration reduces gain in a CE/CS amplifier. Consequently, we expect a reduced Miller multiplier and, hence, a higher value for $f_{-3 \mathrm{~dB}}$. Gain-bandwidth tradeoffs arise all the time in electronics, as we shall frequently see. We wish to use the OCTC technique to estimate the $-3-\mathrm{dB}$ frequency of a voltage amplifier with degeneration.

Consider first the CE-ED amplifier shown in ac form in Fig. 6.49a. As long as $r_{o}$ is fairly large compared with the resistances external to the BJT, we can ignore $r_{o}$ altogether to simplify our analysis. Turning to the open-circuit equivalent of Fig. 6.49b, we adapt Eq. (6.85) to obtain an expression for $R_{\pi}$,

$$
\begin{equation*}
R_{\pi} \cong r_{\pi} / / \frac{R_{B}+R_{E}}{1+g_{m} R_{E}} \tag{6.89}
\end{equation*}
$$

Also, by inspection,
image_name:Figure 6.49(a)
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: v1}
name: Q1, type: NPN, ports: {C: Vo, B: v1, E: v2}
name: RC, type: Resistor, value: RC, ports: {N1: Vo, N2: GND}
name: RE, type: Resistor, value: RE, ports: {N1: v2, N2: GND}
]
extrainfo:The circuit is a common-emitter amplifier with emitter degeneration. Vsig is the input signal source, Rsig is the input resistance, RC is the collector resistance, and RE is the emitter resistance. Q1 is the NPN transistor used for amplification. The output is taken across RC at node Vo.

(a)

$$
R_{s} \cong R_{C}
$$

image_name:Figure 6.49(b)
description:
[
name: RB, type: Resistor, value: RB, ports: {N1: GND, N2: V1}
name: Rπ, type: Resistor, value: Rπ, ports: {N1: V1, N2: V2}
name: ro, type: Resistor, value: ro, ports: {N1: V2, N2: Vo}
name: RC, type: Resistor, value: RC, ports: {N1: Vo, N2: GND}
name: RE, type: Resistor, value: RE, ports: {N1: V2, N2: GND}
name: gmvπ, type: VoltageControlledCurrentSource, ports: {Np: Vo, Nn: V2}
]
extrainfo:The circuit is an equivalent model for analyzing the open-circuit resistances seen by capacitances in a common-emitter amplifier with emitter degeneration. It includes resistors RB, Rπ, Rμ, ro, RC, RE, and Rs, along with a voltage-controlled current source gmvπ. The nodes V1, V2, and Vo are used for interconnections, with the output taken at node Vo.

(b)

FIGURE 6.49 (a) The CE-ED amplifier, and (b) the open-circuit resistances seen by its capacitances.
image_name:FIGURE 6.50
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: V1, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: V2, N2: GND}
name: Gm, type: VoltageControlledCurrentSource, value: Gm, ports: {Np: V2, Nn: GND}
name:  i, type: CurrentSource, value: i, ports: {Np: V1, Nn: V2}
]
extrainfo:The circuit is used to find the equivalent resistance Rμ in a common-emitter amplifier with emitter degeneration. It involves resistors R1 and R2, a voltage source V1, and a voltage-controlled current source with transconductance Gm. The nodes V1, V2, and GND are used for interconnections.

FIGURE 6.50 Equivalent circuit to find $R_{\mu}$ in Fig. 6.49b.

To find $R_{\mu}$ we use the test method, but after having reduced the circuit of Fig. 6.49b to the more compact form of Fig. 6.50. Here, $R_{1}$ and $R_{2}$ represent the equivalent resistances seen looking from the positive and from the negative terminals of the test source, and $G_{m}$ represents the degenerated transconductance. Adapting the expressions tabulated in Fig. 4.9, we have, for $R_{C} \ll r_{o}$,

$$
\begin{gather*}
R_{1} \cong\left(R_{s i g}+r_{b}\right) / /\left[r_{\pi}+\left(\beta_{0}+1\right) R_{E}\right] \quad R_{2} \cong R_{C}  \tag{6.91}\\
G_{m}=\frac{g_{m}}{1+g_{m} R_{E}} \tag{6.92}
\end{gather*}
$$

But the circuit of Fig. 6.50 is formally identical to that of Fig. 6.44b, so we adapt Eq. (6.81) to the present case and write

$$
\begin{equation*}
R_{\mu} \cong R_{1}+R_{2}+G_{m} R_{1} R_{2} \tag{6.93}
\end{equation*}
$$

We now have all the parameters needed to estimate $f_{-3 \mathrm{~dB}}$.

EXAMPLE 6.18 (a) Investigate the effect of adding an emitter-degeneration resistance $R_{E}=500 \Omega$ to the CE amplifier of Example 6.8. Compare with the example, and comment. (b) Verify via PSpice.

#### Solution

(a) Recall that $\beta_{0}=200, r_{b}=200 \Omega, g_{m}=1 /(26 \Omega), r_{\pi}=5.2 \mathrm{k} \Omega, r_{o}=50 \mathrm{k} \Omega$, $C_{\pi}=12 \mathrm{pF}, C_{\mu}=0.5 \mathrm{pF}$, and $C_{s}=1 \mathrm{pF}$. With $R_{s i g}=1 \mathrm{k} \Omega, R_{C}=5 \mathrm{k} \Omega$, and $R_{E}=0.5 \Omega$ we have $R_{B}=1+0.2=1.2 \mathrm{k} \Omega$. All these resistances are much smaller than $r_{o}$, so we expect the above approximations to be reasonable. By Eqs. (6.89) and (6.90),

$$
R_{\pi} \cong 5.2 / / \frac{1.2+0.5}{1+0.5 / 0.026}=82.7 \Omega \quad R_{s} \cong 5 \mathrm{k} \Omega
$$

By Eq. (6.91), $R_{1} \cong 1.2 / /(5.2+201 \times 0.5)=1.2 / / 105.7=1.19 \mathrm{k} \Omega$ and $R_{2} \cong$ $5 \mathrm{k} \Omega$. By Eqs. (6.92) and (6.93),

$$
G_{m}=\frac{1 / 26}{1+500 / 26}=\frac{1}{526 \Omega} \quad R_{\mu}=1.19+5+\frac{1.99 \times 5}{0.526}=17.5 \mathrm{k} \Omega
$$

Finally, expressing resistances in $\mathrm{k} \Omega$ and capacitances in pF , we get

$$
f_{-3 d B}=\frac{1 / 2 \pi}{R_{\pi} C_{\pi}+R_{\mu} C_{\mu}+R_{s} C_{s}} \cong \frac{1 / 2 \pi}{(1+8.75+5) \mathrm{ns}}=10.8 \mathrm{MHz}
$$

Compared to the case $R_{E}=0$ of Example 6.15, there has been an order-of-magnitude reduction both in $\tau_{\pi}$ and in $\tau_{\mu}$, causing $f_{-3 \mathrm{~dB}}$ to increase from about 1.53 MH to 10.8 MHz . On the other hand, the low-frequency gain has dropped from $a_{0}=-142 \mathrm{~V} / \mathrm{V}(43 \mathrm{~dB})$ of Example 6.8 to the present value

$$
a_{0}=\frac{105.7}{1.2+105.7} \times \frac{-5}{0.526} \cong-9.4 \mathrm{~V} / \mathrm{V}(19.5 \mathrm{~dB})
$$

(b) To verify via PSpice, reuse the circuit of Fig. 6.22, but after lifting the emitter terminal off ground to insert $R_{E}=500 \Omega$ between emitter and ground. The simulation yields the Bode plots of Fig. 6.51, which are in good agreement with the results found via the OCRC technique.
image_name:FIGURE 6.51
description:The graph in FIGURE 6.51 is a Bode plot illustrating the gain in decibels (dB) versus frequency in hertz (Hz) for a common emitter (CE) amplifier circuit. The x-axis represents the frequency, ranging from 10^5 Hz to 10^8 Hz on a logarithmic scale, while the y-axis represents the gain in decibels, ranging from 0 dB to 50 dB.

There are two curves on the plot:

1. **Curve for R_E = 0**: This curve starts at a gain of approximately 43 dB at lower frequencies and shows a gradual decrease in gain as the frequency increases. The gain curve maintains a relatively flat region before it starts to roll off, indicating a decrease in gain at higher frequencies.

2. **Curve for R_E = 0.5 kΩ**: This curve starts at a lower initial gain of approximately 20 dB. Similar to the first curve, it also exhibits a decrease in gain with increasing frequency, but the roll-off begins earlier compared to the R_E = 0 curve.

Key features include:
- The gain for R_E = 0 is significantly higher than for R_E = 0.5 kΩ across the frequency range.
- The -3 dB point for R_E = 0.5 kΩ is noted at approximately 10.8 MHz, indicating the frequency at which the gain has decreased by 3 dB from its maximum value.
- The data box on the graph provides additional specifications: for R_E = 0, the open-loop gain a_0 is -142 V/V with a cutoff frequency f_1 of 1.53 MHz. For R_E = 0.5 kΩ, the open-loop gain a_0 is -9.3 V/V with a -3 dB frequency of 10.8 MHz.

Overall, the plot demonstrates how the introduction of a 0.5 kΩ resistor (R_E) in the emitter significantly reduces the gain and affects the frequency response of the amplifier, shifting the -3 dB cutoff to a higher frequency.

FIGURE 6.51 Gain plots for the CE amplifier of Example $6.8\left(R_{E}=0\right)$, and the CE-ED amplifier of Example $6.18\left(R_{E}=0.5 \mathrm{k} \Omega\right)$.

Next, we turn to the CS-SD amplifier of Fig. 6.52a. With reference to its opencircuit equivalent of Fig. $6.52 b$ we find, by inspection,

$$
\begin{equation*}
R_{g b}=R_{s i g} \quad R_{s b}=R_{S} / / R_{s} \quad R_{d b}=R_{D} / / R_{d} \tag{6.94}
\end{equation*}
$$

image_name:(a)
description:
[
name: Vsig, type: VoltageSource, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: Vi}
name: RD, type: Resistor, value: RD, ports: {N1: Vo, N2: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vs, N2: GND}
name: M1, type: PMOS, ports: {S: Vs, D: Vo, G: Vi}
]
extrainfo:The circuit is a CS-SD amplifier with a PMOS transistor M1. It includes resistors for biasing and feedback, and uses voltage-controlled current sources to model the transistor's behavior. The input is applied at Vi and the output is taken from Vo.
image_name:(b)
description:
[
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: GND}
name: RD, type: Resistor, value: RD, ports: {N1: Vo, N2: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vs, N2: GND}
name: ro, type: Resistor, value: ro, ports: {N1: Vo, N2: Vs}
name: gmvgs, type: VoltageControlledCurrentSource, ports: {Np: Vs, Nn: Vo}
name: gmbvs, type: VoltageControlledCurrentSource, ports: {Np: Vs, Nn: GND}
]
extrainfo:The circuit is a common-source amplifier with a source degeneration resistor. It includes a PMOS transistor M1, various resistors, and dependent current sources. The input voltage is Vsig, and the output is taken at Vo. The circuit is designed to amplify the input signal while providing specific impedance characteristics.

FIGURE 6.52 (a) The CS-SD amplifier and (b) the open-circuit resistances seen by its capacitances.
where $R_{s}$ and $R_{d}$ are the resistances seen looking into the source and the drain, both of which are tabulated in Fig. 4.23. To find $R_{g d}$ we simply adapt Eqs. (6.92) and (6.93) to the MOS case,

$$
\begin{equation*}
R_{g d} \cong R_{s i g}+R_{d b}+\frac{g_{m}}{1+\left(g_{m}+g_{m b}\right) R_{S}} R_{s i g} R_{d b} \tag{6.95}
\end{equation*}
$$

Finally, to find $R_{g s}$ we apply the test method as usual. The result, whose derivation is left as an exercise for the reader, is

$$
\begin{equation*}
R_{g s}=\frac{R_{s i g}+R_{S}+g_{m b} R_{s i g} R_{S}+\left(R_{s i g} R_{S}+R_{s i g} R_{D}+R_{D} R_{S}\right) / r_{o}}{1+\left(g_{m}+g_{m b}\right) R_{S}+\left(R_{D}+R_{S}\right) / r_{o}} \tag{6.96}
\end{equation*}
$$

We now have all the parameters needed to estimate $f_{-3 \mathrm{~dB}}$.

EXAMPLE 6.19 Let the CS-SD amplifier of Fig. $6.52 a$ have $g_{m}=2 \mathrm{~mA} / \mathrm{V}, g_{m b}=0.25 \mathrm{~mA} / \mathrm{V}$, $r_{o}=25 \mathrm{k} \Omega, C_{g s}=100 \mathrm{fF}, C_{g b}=C_{s b}=C_{g d}=C_{d b}=7.5 \mathrm{fF}$. If $R_{s i g}=10 \mathrm{k} \Omega, R_{D}=$ $20 \mathrm{k} \Omega$, and $R_{S}=1 \mathrm{k} \Omega$, estimate its gain-bandwidth product via the OCTC method.

#### Solution

By Eq. (4.39a), the low-frequency gain is

$$
a_{0}=\frac{-2 \times 20}{1+(2+0.25) 1+(20+1) / 25}=-9.78 \mathrm{~V} / \mathrm{V}
$$

and the resistances seen looking into the source and drain are $R_{s}=0.786 \Omega$ and $R_{d}=82.3 \mathrm{k} \Omega$, so Eq. (6.94) gives

$$
R_{g b}=10 \mathrm{k} \Omega \quad R_{s b}=1 / / 0.786=0.44 \mathrm{k} \Omega \quad R_{d b}=20 / / 82.3=16.1 \mathrm{k} \Omega
$$

Likewise, Eqs. (6.95) and (6.96) give

$$
R_{g d} \cong 125 \mathrm{k} \Omega \quad R_{g s}=5.55 \mathrm{k} \Omega
$$

Consequently,

$$
\begin{aligned}
f_{-3 \mathrm{~dB}} & =\frac{1 / 2 \pi}{\tau_{g b}+\tau_{s b}+\tau_{g d}+\tau_{g s}+\tau_{d b}} \\
& \cong \frac{1 / 2 \pi}{(75+3.3+937.5+555+121) \mathrm{ps}} \cong 94.1 \mathrm{MHz}
\end{aligned}
$$

Finally, $\mathrm{GBP} \cong 9.78 \times 94.1 \cong 920 \mathrm{MHz}$. The main band-limiting culprits are $C_{g d}$ and $C_{g s^{\circ}}$. A PSpice simulation confirms the above results.

Additional examples of OCTC analysis are addressed in the end-of-chapter problems.

## 6.8 FREQUENCY RESPONSE OF CASCODE AMPLIFIERS

In Chapter 4 we investigated the use of cascoding as a means to raise the unloaded voltage gain dramatically. We are now ready to appreciate another inherent advantage of cascoding, namely, an increase in the gain-bandwidth product (GBP).

### The Bipolar Cascode

Shown in Fig. 6.53a is the ac equivalent of the bipolar cascode configuration, highlighting the capacitances intervening in the frequency response. We wish to estimate the $-3-\mathrm{dB}$ frequency via OCTC analysis. The node labeled as $V_{x}$ plays an important role in this circuit, so we start out by finding the open-circuit equivalent resistance $R_{x}$ between this node and ground. With reference to Fig. $6.53 b$ we note that $R_{x}=r_{o 1} / / R_{e 2}$, where $R_{e 2}$ is the resistance seen looking into $Q_{2}$ 's emitter. This is obtained by adapting Eq. (4.10) to the present case. The result is

$$
\begin{equation*}
R_{x}=r_{o 1} / l\left[\left(\frac{r_{b 2}+r_{\pi 2}}{\beta_{02}+1} / / r_{o 2}\right) \times \frac{1+R_{C} / r_{o 2}}{1+R_{C} /\left[\left(\beta_{02}+1\right) r_{o 2}+r_{b 2}+r_{\pi 2}\right]}\right] \tag{6.97}
\end{equation*}
$$

(Note that for large $r_{o 1}$ and $\beta_{02}$ we have $R_{x} \cong r_{e 2}+r_{b 2} /\left(\beta_{02}+1\right)$ for $R_{C} \rightarrow 0$, and $R_{x} \cong$ $r_{\pi 2}+r_{b 2}$ for $R_{C} \rightarrow \infty$ ).

We observe that $Q_{1}$ is similar to the circuit of Fig. 6.43, but with $R_{2}=R_{x}$. We can thus recycle the results developed there and write,

$$
\begin{equation*}
R_{\pi 1}=\left(R_{s i g}+r_{b 1}\right) / / r_{\pi 1} \quad R_{\mu 1}=R_{\pi 1}+R_{x}+g_{m 1} R_{\pi 1} R_{x} \quad R_{s 1}=R_{x} \tag{6.98}
\end{equation*}
$$

image_name:(a)
description:This is a bipolar cascode amplifier configuration with all relevant stray capacitances shown. The circuit includes two NPN transistors Q1 and Q2, resistors Rsig, rb1, rb2, and RC, capacitors Cpi1, Cpi2, Cmu1, Cmu2, Cs1, and Cs2, and a voltage source Vsig. The circuit is configured to amplify signals with high frequency response by reducing the Miller effect through the cascode configuration.
image_name:The circuit diagram (b) shows a configuration for calculating open-circuit equivalent resistances. It includes two NPN transistors (Q1 and Q2) with associated resistors and capacitors for modeling stray capacitances. Rsig and rb1 are connected to the base of Q1, while rb2 is connected to the base of Q2. RC is connected to the collector of Q2. The diagram is used to analyze the behavior of the cascode amplifier configuration.

FIGURE 6.53 (a) The bipolar cascode configuration, with all relevant stray capacitances explicitly shown outside of the BJTs. (b) Circuit for the calculation of the open-circuit equivalent resistances.

Likewise, $Q_{2}$ is similar to the circuit of Fig. 6.49b, but with $R_{B}=r_{b 2}$ and $R_{E}=r_{o 1}$. We can thus recycle the results developed there and write,

$$
\begin{equation*}
R_{\pi 2} \cong r_{\pi 2} / / \frac{r_{b 2}+r_{o 1}}{1+g_{m 2} r_{o 1}} \cong r_{e 2} \quad R_{\mu 2} \cong R_{1}+R_{2}+G_{m 2} R_{1} R_{2} \quad R_{s 2} \cong R_{C} \tag{6.99}
\end{equation*}
$$

where

$$
\begin{equation*}
R_{1} \cong r_{b 2} / /\left[r_{\pi 2}+\left(\beta_{02}+1\right) r_{o 1}\right] \cong r_{b 2} \quad R_{2} \cong R_{C} \quad G_{m 2}=\frac{g_{m 2}}{1+g_{m 2} r_{o 1}} \cong \frac{1}{r_{o 1}} \tag{6.100}
\end{equation*}
$$

It is now a straightforward matter to apply Eq. (6.80) to estimate the $f_{-3 \mathrm{~dB}}$ for the bipolar cascode.

EXAMPLE 6.20 The CE amplifier of Example 6.15 was found to have $f_{-3 \mathrm{~dB}}=1.53 \mathrm{MHz}$ with $R_{s i g}=1 \mathrm{k} \Omega$ and $R_{C}=5 \mathrm{k} \Omega$. What happens if we buffer it to $R_{C}$ via a CB stage, thus implementing a cascoded pair? Compare and comment. (For simplicity assume identical BJT parameters, namely, $\beta_{0}=200, r_{b}=200 \Omega, g_{m}=1 /(26 \Omega), r_{\pi}=$ $5.2 \mathrm{k} \Omega, r_{o}=50 \mathrm{k} \Omega, C_{\pi}=12 \mathrm{pF}, C_{\mu}=0.5 \mathrm{pF}$ and $C_{s}=1 \mathrm{pF}$. Also, assume $r_{\mu}=\infty$.)

#### Solution

Applying Eq. (6.97) with suitable approximations we get

$$
R_{x} \cong \frac{200+5200}{201} \times \frac{1+5 / 50}{1+0}=29.5 \Omega
$$

We immediately observe that with such a small equivalent collector resistance, $Q_{1}$ is going to provide very little voltage gain, resulting in a very small Miller multiplier for $C_{\mu 1}$. With the given data, this gain is $v_{x} / v_{b 1}=-g_{m 1} R_{x}=-29.5 / 26=$ $-1.13 \mathrm{~V} / \mathrm{V}$, indicating a Miller multiplier of just over 2 . We thus anticipate a wider bandwidth for the CE-CB pair compared to the basic CE amplifier of Example 6.15. Using Eqs. (6.98) through (6.100) we readily calculate

$$
\begin{array}{lll}
R_{\pi 1}=975 \Omega & R_{\mu 1}=2111 \Omega & R_{s 1}=29.5 \Omega \\
R_{\pi 2} \cong 26 \Omega & R_{\mu 2} \cong 5 \mathrm{k} \Omega & R_{s 2}=5 \mathrm{k} \Omega
\end{array}
$$

With resistances in $\mathrm{k} \Omega\left(10^{3}\right)$ and capacitances in $\mathrm{pF}\left(10^{-12}\right)$, the time constants will be in ns $\left(10^{-9}\right)$,

$$
\begin{aligned}
f_{-3 \mathrm{~dB}} & \cong \frac{1}{2 \pi\left(\tau_{\pi 1}+\tau_{\mu 1}+\tau_{s 1}+\tau_{\pi 2}+\tau_{\mu 2}+\tau_{s 2}\right)} \\
& =\frac{1 / 2 \pi}{(11.7+1.06+0.03+0.31+2.5+5) \mathrm{ns}} \cong 7.7 \mathrm{MHz}
\end{aligned}
$$

Compared to the basic CE amplifier of Example 6.15, the cascode pair is far less affected by the Miller effect. In fact, $\tau_{\mu 1}$ is now rather small, and the main bandlimiting culprits are $C_{\pi 1}$ and $C_{s 2}$.

Investigate the limiting case in which the cascode circuit of Example 6.20 is terminated on an ideal current-source load so that $R_{C} \rightarrow \infty$. Compare the two situations, verify with PSpice, and comment.

#### Solution

Letting $R_{C} \rightarrow \infty$ in Eq. (6.97) raises $R_{x}$ to

$$
R_{x}=r_{o 1} / /\left(r_{b 2}+r_{\pi 2}\right)=50 / /(0.2+5.2)=4.87 \mathrm{k} \Omega
$$

This increase has no effect on $R_{\pi 1}$, but raises $R_{\mu 1}$ and $R_{s 1}$. Using again Eqs. (6.98) through (6.100) we get

$$
R_{\pi 1}=975 \Omega \quad R_{\mu 1} \cong 188 \mathrm{k} \Omega \quad R_{s 1}=4.87 \mathrm{k} \Omega
$$

Also, adapting Eq. (4.11) to the present case we find, for negligible $r_{b}$,

$$
R_{s 2}=R_{c 2} \cong r_{o 2}\left(1+\beta_{02} \frac{r_{o 1}}{r_{o 1}+r_{\pi 2}}\right)=9.1 \mathrm{M} \Omega \quad R_{\mu 2} \cong R_{s 2}=9.1 \mathrm{M} \Omega
$$

With $Q_{2}$ 's collector terminated on an ac open circuit, we now have

$$
R_{\pi 2}=r_{\pi 2} / /\left(r_{b 2}+r_{o 1}\right)=4.95 \mathrm{k} \Omega
$$

Finally,

$$
\begin{aligned}
f_{-3 \mathrm{~dB}} & \cong \frac{1 / 2 \pi}{\tau_{\pi 1}+\tau_{\mu 1}+\tau_{s 1}+\tau_{\pi 2}+\tau_{\mu 2}+\tau_{s 2}} \\
& \cong \frac{1 / 2 \pi}{(12+94+5+59+4550+9100) \mathrm{ns}} \cong 11.5 \mathrm{kHz}
\end{aligned}
$$

We observe that letting $R_{C} \rightarrow \infty$ increases $R_{x}$ significantly, causing $Q_{1}$ to provide a much higher gain, namely, $v_{x} / v_{b 1}=-g_{m 1} R_{x}=-4870 / 26=-187 \mathrm{~V} / \mathrm{V}$. Consequently, we now have a Miller multiplier of 188 , which raises $\tau_{\mu 1}$ from about 1 ns to 94 ns . The other major effect of letting $R_{C} \rightarrow \infty$ is the dramatic increase in the output resistance $R_{o}$, namely, from $5 \mathrm{k} \Omega$ to $9.1 \mathrm{M} \Omega$. While raising the unloaded gain $a_{0}$, this also reduces the pole frequency $f_{-3 \mathrm{~dB}}$ in proportion.

Using the PSpice circuit of Fig. 6.54 we obtain the frequency plots of Fig. 6.55. It is apparent that in the limit $R_{C} \rightarrow \infty$ the main band-limiting culprits are $C_{\mu 2}$ and $C_{s 2}$, which establish a dominant pole at

$$
f_{p}=\frac{1}{2 \pi R_{o}\left(C_{s 2}+C_{\mu 2}\right)}=11.7 \mathrm{kHz}
$$

image_name:FIGURE 6.54
description:
[
name: rb2, type: Resistor, value: 200 Ω, ports: {N1: GND, N2: V1}
name: rπ2, type: Resistor, value: 5.2 kΩ, ports: {N1: V1, N2: VX}
name: Cπ2, type: Capacitor, value: 12 pF, ports: {Np: V1, Nn: VX}
name: Cμ2, type: Capacitor, value: 0.5 pF, ports: {Np: V1, Nn: V0}
name: ro2, type: Resistor, value: 50 kΩ, ports: {N1: VX, N2: V0}
name: Cs, type: Capacitor, value: 1 pF, ports: {Np: Vo, Nn: GND}
name: RC, type: Resistor, value: 5 kΩ, ports: {N1: Vo, N2: GND}
name: Rsig, type: Resistor, value: 1.0 kΩ, ports: {N1: Vsig, N2: V2}
name: rb1, type: Resistor, value: 200 Ω, ports: {N1: V2, N2: V3}
name: rπ1, type: Resistor, value: 5.2 kΩ, ports: {N1: V3, N2: GND}
name: Cπ1, type: Capacitor, value: 12 pF, ports: {Np: V3, Nn: GND}
name: Cμ1, type: Capacitor, value: 0.5 pF, ports: {Np: V3, Nn: GND}
name: ro1, type: Resistor, value: 50 kΩ, ports: {N1: VX, N2: VX}
name: Cs1, type: Capacitor, value: 1 pF, ports: {Np: VX, Nn: GND}
name: Vsig, type: VoltageSource, value: 1 Vac, 0 Vdc, ports: {Np: Vsig, Nn: GND}
name: gm2, type: VoltageControlledCurrentSource, value: 38.5 mA/V, ports: {Np: VX, Nn: V0}
name: gm1, type: VoltageControlledCurrentSource, value: 38.5 mA/V, ports: {Np: VX, Nn: GND}
]
extrainfo:The circuit is a CE-CB amplifier configuration with various resistors, capacitors, and voltage-controlled current sources. It is designed to analyze gain versus frequency, with components such as resistors and capacitors determining the frequency response.

FIGURE 6.54 PSpice circuit to display gain vs. frequency for the CE-CB amplifier.
image_name:FIGURE 6.55
description:The graph in FIGURE 6.55 is a Bode plot showing the gain (in decibels) versus frequency (in hertz) for a CE-CB amplifier configuration, with two different load resistances: \( R_C = 5 \text{k}\Omega \) and \( R_C = \infty \).

Axes Labels and Units:
- The x-axis represents frequency \( f \) in hertz (Hz) and is plotted on a logarithmic scale ranging from \( 10^3 \) to \( 10^8 \) Hz.
- The y-axis represents gain \( a \) in decibels (dB), ranging from 0 to 120 dB.

Overall Behavior and Trends:
- For \( R_C = 5 \text{k}\Omega \): The gain starts at approximately 43.8 dB and remains relatively flat until it starts to roll off at higher frequencies, reaching the \(-3 \text{ dB}\) point at 10.2 MHz.
- For \( R_C = \infty \): The gain starts much higher at 109 dB and shows a similar flat behavior at lower frequencies before rolling off more steeply, reaching the \(-3 \text{ dB}\) point at 11.4 kHz.

Key Features and Technical Details:
- The plot shows two distinct curves representing different configurations of the amplifier.
- Both curves exhibit a flat gain region followed by a roll-off, characteristic of amplifier frequency response.
- The \(-3 \text{ dB}\) cutoff frequencies are marked for both configurations.

Annotations and Specific Data Points:
- The annotations indicate the initial gain \( a_0 \) and the \(-3 \text{ dB}\) cutoff frequencies for both values of \( R_C \):
- \( R_C = 5 \text{k}\Omega \): \( a_0 = 43.8 \text{ dB}, f_{-3 \text{ dB}} = 10.2 \text{ MHz} \)
- \( R_C = \infty \): \( a_0 = 109 \text{ dB}, f_{-3 \text{ dB}} = 11.4 \text{ kHz} \)
- These values are crucial for understanding the frequency response and performance of the amplifier under different load conditions.

FIGURE 6.55 Gain plots for the CE-CB amplifier of Example $6.20\left(R_{C}=5 \mathrm{k} \Omega\right)$ and of Example $6.21\left(R_{C}=\infty\right)$.

### The MOS Cascode

Shown in Fig. $6.56 a$ is the ac equivalent of the MOS cascode configuration, along with all capacitances affecting its frequency response. We wish to estimate the $-3-\mathrm{dB}$ frequency via the OCTC technique. As in the bipolar case, the node labeled as $V_{x}$ plays an important role in this circuit, so we start out by finding the opencircuit equivalent resistance $R_{x}$ between this node and ground. With reference to
image_name:Fig. 6.56 a
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: g1}
name: M1, type: NMOS, ports: {S: GND, D: Vx, G: g1}
name: M2, type: PMOS, ports: {S: Vx, D: Vo, G: GND}
name: RD, type: Resistor, value: RD, ports: {N1: Vo, N2: GND}
name: Cgs1, type: Capacitor, value: Cgs1, ports: {Np: g1, Nn: GND}
name: Cgd1, type: Capacitor, value: Cgd1, ports: {Np: Vx, Nn: g1}
name: Cdb1, type: Capacitor, value: Cdb1, ports: {Np: Vx, Nn: GND}
name: Cgs2, type: Capacitor, value: Cgs2, ports: {Np: Vx, Nn: GND}
name: Cgd2, type: Capacitor, value: Cgd2, ports: {Np: Vo, Nn: GND}
name: Cdb2, type: Capacitor, value: Cdb2, ports: {Np: Vo, Nn: GND}
]
extrainfo:This is a MOS cascode configuration circuit. The circuit includes NMOS (M1) and PMOS (M2) transistors, various capacitors representing stray capacitances, and resistors for signal and load. The node Vx is a critical point for the frequency response analysis.
image_name:Fig. 6.56 b
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vx, G: g1}
name: M2, type: PMOS, ports: {S: Vx, D: Vo, G: GND}
name: RD, type: Resistor, value: RD, ports: {N1: Vo, N2: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: g1}
name: Cgs1, type: Capacitor, value: Cgs1, ports: {Np: g1, Nn: GND}
name: Cgd1, type: Capacitor, value: Cgd1, ports: {Np: Vx, Nn: GND}
name: Cdb1, type: Capacitor, value: Cdb1, ports: {Np: Vx, Nn: GND}
name: Cgs2, type: Capacitor, value: Cgs2, ports: {Np: Vx, Nn: GND}
name: Cgd2, type: Capacitor, value: Cgd2, ports: {Np: Vo, Nn: GND}
name: Cdb2, type: Capacitor, value: Cdb2, ports: {Np: Vo, Nn: GND}
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: Rgs1, type: Resistor, value: Rgs1, ports: {N1: g1, N2: GND}
name: Rgd1, type: Resistor, value: Rgd1, ports: {N1: Vx, N2: GND}
name: Rdb1, type: Resistor, value: Rdb1, ports: {N1: Vx, N2: GND}
name: Rgs2, type: Resistor, value: Rgs2, ports: {N1: Vx, N2: GND}
name: Rgd2, type: Resistor, value: Rgd2, ports: {N1: Vo, N2: GND}
name: Rdb2, type: Resistor, value: Rdb2, ports: {N1: Vo, N2: GND}
name: Rx, type: Resistor, value: Rx, ports: {N1: Vx, N2: GND}
]
extrainfo:The circuit is a MOS cascode configuration used to improve gain and bandwidth. The key node Vx is the intermediate point between M1 and M2, affecting the frequency response. The configuration includes various parasitic capacitances.

FIGURE 6.56 (a) The MOS cacode configuration, with all relevant stray capacitances explicitly shown outside of the FETs. (b) Circuit for the calculation of the open-circuit equivalent resistances.

Fig. $6.56 b$ we note that $R_{x}=R_{d 1} / / R_{s 2}$, where $R_{d 1}$ and $R_{s 2}$ are the resistances seen looking into $M_{1}$ 's drain and $M_{2}$ 's source, respectively. The former is simply $r_{o 1}$, and the latter is obtained by adapting Eq. (4.40a) to the present case. The result can be written as

$$
\begin{equation*}
R_{x}=r_{o 1} / / \frac{r_{o 2}+R_{D}}{1+\left(g_{m 2}+g_{m b 2}\right) r_{o 2}} \tag{6.101}
\end{equation*}
$$

(Note that for $R_{D} \rightarrow 0$ we have $R_{x} \cong 1 /\left(g_{m 2}+g_{m 2}\right)$, whereas for $R_{D} \rightarrow \infty$ we have $R_{x} \cong$ $r_{o 1}$.) Next, using inspection and also adapting Eq. (6.81) to the present case we write

$$
\begin{equation*}
R_{g s 1}=R_{s i g} \quad R_{g d 1}=R_{s i g}+R_{x}+g_{m 1} R_{s i g} R_{x} \quad R_{d b 1}=R_{x} \tag{6.102}
\end{equation*}
$$

Finally, using again inspection and adapting Eq. (4.41) to the present case we write

$$
\begin{equation*}
R_{g s 2}=R_{x} \quad R_{g d 2}=R_{D} / /\left[r_{o 1}+r_{o 2}+\left(g_{m 2}+g_{m b 2}\right) r_{o 1} r_{o 2}\right] \quad R_{d b 2}=R_{g d 2} \tag{6.103}
\end{equation*}
$$

It is now a straightforward matter to apply Eq. (6.80) to estimate the $-3-\mathrm{dB}$ frequency of the MOS cascode.
(a) Find the product $\left|a_{0}\right| \times f_{-3 \mathrm{~dB}}$ of a CS amplifier implemented with a MOSFET having $g_{m}=1.0 \mathrm{~mA} / \mathrm{V}, r_{o}=25 \mathrm{k} \Omega, C_{g s}=100 \mathrm{fF}$, and $C_{g d}=C_{d b}=20 \mathrm{fF}$. Assume the circuit is driven by a source with $R_{s i g}=10 \mathrm{k} \Omega$ and is terminated on an ideal current-source load so that $R_{D}=\infty$ and the low-frequency gain coincides with the intrinsic gain.
(b) Repeat, but for the case in which the CS stage is buffered to the active load via a CG stage, thus implementing a cascode pair. Compare and comment. (For simplicity, assume identical parameters for the two FETs. Also, assume $\chi_{2}=0.1$.)
(c) Verify with PSpice.

#### Solution

(a) The plain CS amplifier has a low-frequency intrinsic gain of

$$
a_{0}=-g_{m} r_{o}=-1 \times 25=-25 \mathrm{~V} / \mathrm{V} \cong 28 \mathrm{~dB}
$$

Using inspection and adapting Eq. (6.81), we write

$$
R_{g d}=R_{s i g}+r_{o}+g_{m} R_{s i g} r_{o}=10+25+1 \times 10 \times 25=285 \mathrm{k} \Omega
$$

With resistances in $\mathrm{k} \Omega\left(10^{3}\right)$ and capacitances in $\mathrm{fF}\left(10^{-15}\right)$, the time constants will be in ps ( $10^{-12}$ ),

$$
\begin{aligned}
f_{-3 \mathrm{~dB}} & \cong \frac{1}{2 \pi\left(\tau_{g s}+\tau_{g d}+\tau_{d b}\right)}=\frac{1 / 2 \pi}{(10 \times 100+285 \times 20+25 \times 20) \mathrm{ps}} \\
& =\frac{1 / 2 \pi}{(1+5.7+0.5) \mathrm{ns}} \cong 22 \mathrm{MHz}
\end{aligned}
$$

Finally, $\left|a_{0}\right| \times f_{-3 \mathrm{~dB}}=25 \times 22=550 \mathrm{MHz}$.
(b) Cascoding will raise the intrinsic gain to

$$
\begin{aligned}
a_{0} & =-g_{m 1} r_{o 1}\left[1+\left(g_{m 2}+g_{m b 2}\right) r_{o 2}\right]=-25(1+1.1 \times 25) \\
& =-712.5 \mathrm{~V} / \mathrm{V}=57 \mathrm{~dB}
\end{aligned}
$$

To apply the OCTC method we note that with an ideal current-source load we have $R_{D}=\infty$, so Eq. (6.102) gives $R_{x}=r_{o 1}=25 \mathrm{k} \Omega$. Using inspection, along with Eqs. (6.102) and (6.103), we now have

$$
\begin{aligned}
& R_{g s 1}=10 \mathrm{k} \Omega \quad R_{d b 1}=R_{g s 2}=25 \mathrm{k} \Omega \quad R_{g d 1}=285 \mathrm{k} \Omega \\
& R_{g d 2}=R_{d b 2}=737.5 \mathrm{k} \Omega
\end{aligned}
$$

With resistances in $\mathrm{k} \Omega\left(10^{3}\right)$ and capacitances in $\mathrm{pF}\left(10^{-12}\right)$, the time constants will be in ns $\left(10^{-9}\right)$,

$$
\begin{aligned}
f_{-3 \mathrm{~dB}} & \cong \frac{1 / 2 \pi}{\tau_{g s 1}+\tau_{g d 1}+\tau_{d b 1}+\tau_{g s 2}+\tau_{g d 2}+\tau_{d b 2}} \\
& =\frac{1 / 2 \pi}{(1+5.7+0.5+2.5+14.7+14.7) \mathrm{ns}}=4.1 \mathrm{MHz}
\end{aligned}
$$

image_name:FIGURE 6.57
description:The graph in Figure 6.57 is a Bode plot displaying the gain (in decibels, dB) versus frequency (in hertz, Hz) for two amplifier configurations: CS (Common Source) and CS-CG (Common Source-Common Gate).

**Axes Labels and Units:**
- The x-axis represents the frequency in Hz, and it is plotted on a logarithmic scale, ranging from 10^3 Hz to 10^6 Hz.
- The y-axis represents the gain in decibels (dB), ranging from -20 dB to 60 dB.

**Overall Behavior and Trends:**
- The CS amplifier shows a relatively flat gain curve starting at about 28 dB up to around 10^5 Hz, after which it begins to decline.
- The CS-CG amplifier starts with a higher gain of about 57 dB, maintaining this level until approximately 10^5 Hz, then it declines more sharply than the CS amplifier.

**Key Features and Technical Details:**
- The CS amplifier has a -3 dB cutoff frequency at approximately 22.3 MHz.
- The CS-CG amplifier has a -3 dB cutoff frequency at approximately 4.1 MHz.
- The gain of the CS amplifier is lower than that of the CS-CG amplifier across the entire frequency range shown.

**Annotations and Specific Data Points:**
- The plot includes annotations for the initial gain (a_0) and the -3 dB cutoff frequency (f_{-3 dB}) for both amplifier configurations.
- The CS amplifier is marked with a_0 = 28 dB and f_{-3 dB} = 22.3 MHz.
- The CS-CG amplifier is marked with a_0 = 57 dB and f_{-3 dB} = 4.1 MHz.

Overall, the graph clearly illustrates the trade-off between gain and bandwidth for the two amplifier configurations, with the CS-CG offering higher gain but a lower bandwidth compared to the CS amplifier.

FIGURE 6.57 Gain plots for the Cs and the CS-CB amplifiers of Example 6.22.
We now have $\left|a_{0}\right| \times f_{-3 \mathrm{~dB}}=712.5 \times 4.1=2.9 \mathrm{GHz}$. Cascoding has raised $a_{0}$ while lowering $f_{-3 \mathrm{~dB}}$. Yet their product is still higher than in part (a). The main band-limiting culprits are now $C_{g d 2}$ and $C_{d b 2}$, which form a pole with the high output resistance $R_{o}$ of the cascode structure.
(c) Using a PSpice circuit of the type of Fig. 6.54 we obtain the plots of Fig. 6.57, which are in excellent agreement with the hand calculations.

We summarize the advantages of cascoding by stating that the CE/CS stages $Q_{1} / M_{1}$ overcome their inherent Miller-effect drawbacks by delegating the task of voltage amplification to the $\mathrm{CB} / \mathrm{CG}$ stages $Q_{2} / M_{2}$, which are inherently much faster because they are immune from the Miller effect. The result is a dramatic increase in the gain-bandwidth product.

## 6.9 FREQUENCY AND TRANSIENT RESPONSES OF OP AMPS

Most op amps are designed for a gain that is dominated by a single low-frequency pole (the reason, to be investigated in detail in Chapter 7, is to prevent possible oscillations in negative-feedback operation). For the traditional voltage-feedback op amp of Fig. $6.58 a$ the gain $a(j f)$ exhibits the frequency profile of Fig. $6.58 b$ and takes on the mathematical form

$$
\begin{equation*}
a(j f)=\frac{V_{o}}{V_{p}-V_{n}} \cong \frac{a_{0}}{1+j f / f_{b}} \tag{6.104}
\end{equation*}
$$

where $V_{o}, V_{p}$, and $V_{n}$ are the Laplace transforms of the small signals $v_{o}, v_{p}$, and $v_{n}, a_{0}$ is the dc gain, and $f_{b}$ is the dominant-pole frequency. Gain is approximately constant up to $f_{b}$. At $f_{b}$ it is $3-\mathrm{dB}$ below its dc value. Above $f_{b}$ it rolls off with frequency at a uniform rate of $-20 \mathrm{~dB} / \mathrm{dec}$ until it drops to unity, or 0 dB , at the transition frequency $f_{t}$.
image_name:(a)
description:
[
name: a(jf), type: OpAmp, value: a(jf), ports: {InP: Vn, InN: Vp, OutP: Vo, OutN: GND}
]
extrainfo:The circuit diagram shows an operational amplifier with a transfer function a(jf). It has two input nodes Vn and Vp, and one output node Vo.

(a)
image_name:(a)
description:The graph is a Bode plot representing the frequency response of a voltage-feedback operational amplifier with a dominant pole.

1. **Type of Graph and Function:**
- This is a Bode magnitude plot.

2. **Axes Labels and Units:**
- The vertical axis is labeled \(|a(jf)|\) and represents gain in decibels (dB).
- The horizontal axis is labeled \(f\) and represents frequency in decades (dec).

3. **Overall Behavior and Trends:**
- The graph starts with a constant gain of \(a_0\) dB at low frequencies.
- At the breakpoint frequency \(f_b\), the gain begins to decrease.
- The slope of the decrease is \(-20 \text{ dB/decade}\), indicating a first-order roll-off.
- The gain continues to decrease linearly on the logarithmic scale until it reaches 0 dB at the transition frequency \(f_t\).

4. **Key Features and Technical Details:**
- The graph shows a 3 dB drop from \(a_0\) at the cutoff frequency \(f_b\), which is a typical characteristic of a single-pole low-pass filter.
- The gain-bandwidth product (GBP) is constant and defined by the equation \(GBP = f_t = a_0 \times f_b\).
- The plot illustrates the uniform roll-off rate of \(-20 \text{ dB/decade}\), characteristic of a dominant-pole op amp.

5. **Annotations and Specific Data Points:**
- The graph includes annotations such as the 3 dB point at \(f_b\) and the slope \(-20 \text{ dB/dec}\).
- The transition frequency \(f_t\) is marked where the gain reaches 0 dB, indicating unity gain.

This Bode plot effectively visualizes the frequency response characteristics of the operational amplifier, highlighting the dominant pole behavior and the constant gain-bandwidth product relationship.

(b)

FIGURE 6.58 The frequency response of a voltage-feedback op amp having a dominant pole.

Exploiting the constancy of the gain-bandwidth product (GBP) we write $a_{0} \times f_{b}=$ $1 \times f_{t}$. Consequently, a dominant-pole op amp has a constant GBP,

$$
\begin{equation*}
\text { GBP }=f_{t}=a_{0} \times f_{b} \tag{6.105}
\end{equation*}
$$

The frequency response of an op amp is easily visualized via PSpice, as demonstrated in Fig. 6.59 for the case of the 741 op amp. Using PSpice's cursor facility on the magnitude plot we find $a_{0}=105.3 \mathrm{~dB}, f_{b}=5.2 \mathrm{~Hz}$, and $f_{t}=871 \mathrm{MHz}$. Above $f_{t}$ the rolloff rate increases, indicating the presence of additional root frequencies there. (Higher-order roots will be addressed in greater detail in Chapter 7.)

Let us now investigate how the dominant pole is established in the three representative op amps discussed in Chapter 5, namely, the 741 bipolar and the two-stage and folded cascode CMOS op amps.

- Figure 6.60 shows the portion of the $\mathbf{7 4 1} \mathbf{~ o p ~ a m p ~ i n v o l v e d ~ i n ~ f r e q u e n c y ~ c o m p e n - ~}$ sation. The goal is to establish a dominant pole at a sufficiently low frequency $f_{b}$ to force gain to drop to unity before the phase shift by higher-order poles
image_name:Figure 6.59
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: μA741, type: OpAmp, value: μA741, ports: {InP: 3, InN: 2, OutP: 6, OutN: GND, Vdd: VCC, -Vdd: VEE}
name: RL, type: Resistor, value: 2kΩ, ports: {N1: GND, N2: Vo}
]
extrainfo:The circuit is a simple op-amp configuration using a μA741 with a voltage source input and a load resistor connected at the output. The op-amp is powered by a dual power supply with VCC at +15V and VEE at -15V. The input is connected to the non-inverting terminal of the op-amp.

(a)
image_name:(a)
description:The graph is a Bode plot representing the frequency response of an op-amp, specifically showing the gain in decibels (dB) versus frequency in hertz (Hz).

1. **Type of Graph and Function:**
- This is a Bode plot, which is used to describe the gain of an op-amp across a range of frequencies.

2. **Axes Labels and Units:**
- The x-axis is labeled "Frequency \( f \)" and is measured in hertz (Hz), using a logarithmic scale ranging from 1 Hz to 10 million Hz (\( 10^7 \) Hz).
- The y-axis is labeled "Gain \( a \)" and is measured in decibels (dB), with values ranging from -40 dB to 110 dB.

3. **Overall Behavior and Trends:**
- The plot shows a decreasing trend in gain as frequency increases.
- Starting at approximately 110 dB at low frequencies, the gain steadily decreases as the frequency increases.

4. **Key Features and Technical Details:**
- The gain begins at about 110 dB at 1 Hz and decreases linearly on the logarithmic scale as the frequency increases.
- At approximately 100 kHz (\( 10^5 \) Hz), the gain crosses the 0 dB level, indicating the unity-gain frequency.
- The gain continues to decrease beyond this point, reaching below 0 dB as the frequency approaches 10 million Hz.

5. **Annotations and Specific Data Points:**
- There are no specific annotations or markers on the graph, but the gridlines help in identifying the gain levels at various frequency points.
- The critical point where the gain crosses 0 dB is significant as it represents the bandwidth limit for the op-amp's stable operation in a negative-feedback configuration.

(b)

FIGURE 6.59 Using the 741 macromodel available in PSpice's library to plot the frequency response.
image_name:FIGURE 6.60
description:
[
name: Q13, type: PNP, ports: {C: Vo2C, B: LOAD13, E: VCC}
name: Q16, type: NPN, ports: {C: VCC, B: Vi2, E: V1}
name: Q17, type: NPN, ports: {C: Vo2, B: V1, E: V3}
name: R9, type: Resistor, value: 50 kΩ, ports: {N1: V1, N2: VEE}
name: R8, type: Resistor, value: 100 Ω, ports: {N1: V3, N2: VEE}
name: Cc, type: Capacitor, value: 30 pF, ports: {Np: Vi2, Nn: Vo2}
]
extrainfo:The circuit represents a part of a 741 operational amplifier model. It includes a second stage with a Miller capacitor for frequency compensation, utilizing the Miller effect to stabilize the op-amp. The transistors Q13, Q16, and Q17 are configured to manage voltage amplification and current flow. Resistors and a controlled current source are used to set the gain and frequency characteristics.
image_name:FIGURE 6.60
description:
[
name: Rol, type: Resistor, value: 6.12 MΩ, ports: {N1: Vi2, N2: GND}
name: Ri2, type: Resistor, value: 4.63 MΩ, ports: {N1: Vi2, N2: GND}
name: Ro2, type: Resistor, value: 81.3 kΩ, ports: {N1: V1, N2: GND}
name: Ri3, type: Resistor, value: 9.33 MΩ, ports: {N1: V1, N2: GND}
name: Gm2v12, type: VoltageControlledCurrentSource, ports: {Np: V1, Nn: GND}
]
extrainfo:The circuit diagram represents the second stage of the 741 op amp with frequency compensation. The capacitor Cc, valued at 30 pF, is used to stabilize the op amp by introducing a pole through the Miller effect. The transistors Q13, Q16, and Q17 form part of the amplification and stabilization network. The resistors and voltage-controlled current source are used to model the equivalent resistance and transconductance of the stage.

FIGURE 6.60 The 2nd stage of the 741 op amp and its ac equivalent for the calculation of the resistance $R_{e q}$ as seen by the frequency-compensation capacitor $C_{c}$.
destabilizes the op amp in negative-feedback operation. This pole is obtained by placing a small capacitance $C_{c}(=30 \mathrm{pF})$ across the 2 nd stage and taking advantage of the Miller effect to achieve the much larger effective value needed to establish this low-frequency pole. Since $C_{c}$ is small enough that it can be fabricated on chip, the 741 is said to be internally compensated. (In fact, the 741 was the first op amp in this category, whereas previous op amps had to be compensated externally by the user. Once internal compensation became a technological reality, the op amp took off to become the most widely used analog IC.)

Using OCTC analysis we get

$$
f_{b}=\frac{1}{2 \pi R_{e q} C_{c}}
$$

where $R_{e q}$ is the equivalent resistance seen by $C_{c}$. This resistance is depicted in the ac equivalent shown at the right. Taking advantage of the similarity to Fig. 6.44a, we adapt Eq. (6.81) and write

$$
R_{e q}=\left(R_{o 1} / / R_{i 2}\right)+\left(R_{o 2} / / R_{i 3}\right)+G_{m 2}\left(R_{o 1} / / R_{i 2}\right)\left(R_{o 2} / / R_{i 3}\right)
$$

Substituting the values shown we get

$$
\begin{gathered}
R_{e q}=\left[(6.12 / / 4.63)+(0.0813 / / 9.33)+\frac{(6.12 / / 4.63)+(0.0813 / / 9.33)}{161}\right] 10^{6}=1.32 \mathrm{G} \Omega \\
f_{b}=\frac{1}{2 \pi \times 1.32 \times 10^{9} \times 30 \times 10^{-12}}=4 \mathrm{~Hz}
\end{gathered}
$$

image_name:(a)
description:
[
name: M6, type: PMOS, ports: {S: VDD, D: vO, G: vI2}
name: M5, type: NMOS, ports: {S: VSS, D: vO, G: vI2}
name: Cc, type: Capacitor, value: Cc, ports: {Np: vI2, Nn: vO}
name: Ro1, type: Resistor, value: Ro1, ports: {N1: vO, N2: GND}
name: Ro2, type: Resistor, value: Ro2, ports: {N1: vO, N2: GND}
name: Gm2v12, type: VoltageControlledCurrentSource, ports: {Np: Vo, Nn: GND}
]
extrainfo:The circuit is a combination of PMOS and NMOS transistors forming a differential amplifier with a compensation capacitor Cc for stability. The resistors Ro1, Ro2, and Ro are used to model the output impedance. The circuit is designed to analyze the equivalent resistance and frequency response as described in the context.
image_name:(b)
description:
[
name: M6, type: PMOS, ports: {S: VDD, D: d658, G: LOADB1}
name: M8, type: PMOS, ports: {S: d658, D: vO, G: LOADB2}
name: M4, type: NMOS, ports: {S: s4d10, D: vO, G: LOADB3}
name: M10, type: NMOS, ports: {S: VSS, D: s4d10, G: LOAD4}
name: Ro, type: Resistor, value: Ro, ports: {N1: vO, N2: GND}
name: Cc, type: Capacitor, value: Cc, ports: {Np: vo, Nn: GND}
]
extrainfo:The circuit is a multi-stage amplifier with PMOS and NMOS transistors, featuring a compensation capacitor Cc connected at the output node vO. The circuit is powered by VDD and VSS, with multiple transistors forming a cascade configuration to achieve high gain. The output is taken across the resistor Ro and the capacitor Cc, which also serves as a Miller compensation component.

Alternatively, we can regard $f_{b}$ as arising from the interaction between the net input-node resistance $R_{o 1} / / R_{i 2}$ and the Miller capacitance $C_{M}=[1+$ $\left.G_{m 2}\left(R_{o 2} / / R_{i 3}\right)\right] C_{c}$. With $R_{o 1} / / R_{i 2}=6.12 / / 4.63=2.64 \mathrm{M} \Omega$ and $G_{m 2}\left(R_{o 2} / / R_{i 3}\right)=$ $[(0.0813 / / 9.33) / 161] 10^{6} \cong 500 \mathrm{~V} / \mathrm{V}$ we get $C_{M}=(1+500) \times 30 \mathrm{pF} \cong$ 15 nF . It is apparent that if it weren't for the Miller effect, which makes $C_{c}$ appear 501 times as large, internal compensation would be unfeasible as a $15-\mathrm{nF}$ capacitor cannot realistically be fabricated on chip!

In Eq. (5.22) we calculated $a_{0}=241 \times 10^{3} \mathrm{~V} / \mathrm{V}$, so $f_{t}=a_{0} \times f_{b}=241 \times$ $10^{3} \times 4 \cong 1 \mathrm{MHz}$. The manufacturer's data sheets (which you can search on the Web) give $a_{0}=200 \times 10^{3} \mathrm{~V} / \mathrm{V}, f_{b}=5 \mathrm{~Hz}$, and $f_{t}=200 \times 10^{3} \times 5=1 \mathrm{MHz}$. The discrepancy between the calculated and the data-sheet values stems primarily from the values assumed for $\beta_{0}$ and $V_{A}$ in the course of our hand calculations.

- Figure $6.61 a$ shows the portion of the two-Stage CMOS op amp involved in frequency compensation (the resistance $R_{c}$ appearing in Fig. 5.13 has been ignored because $R_{c} \ll R_{e q}$ ). Like the 741 , this amplifier is stabilized via Miller compensation, so

$$
f_{b}=\frac{1}{2 \pi R_{e q} C_{c}}
$$

where $R_{e q}$ is the equivalent resistance seen by $C_{c}$,

$$
R_{e q} \cong R_{o 1}+R_{o 2}+g_{m 5} R_{o 1} R_{o 2}
$$

- Figure $6.61 b$ shows the portion of the folded-cascode CMOS op amp involved in frequency compensation. This configuration differs from the two op amps just

FIGURE 6.61 Portions of the (a) two-stage and (b) folded-cascode CMOS op amps involved in frequency compensation, along with the ac equivalents showing the ac resistance seen by the compensation capacitance.
investigated because the dominant pole is established by the output resistance $R_{o}$ and the net output-node capacitance $C_{c}$ as

$$
f_{b}=\frac{1}{2 \pi R_{o} C_{c}}
$$

Here, $C_{c}$ is the sum of the capacitances associated with the drains of $M_{4}$ and $M_{8}$ and any external load capacitance $C_{L}$. Moreover, by Eq. (5.39),

$$
R_{o} \cong\left[\left(g_{m 6}+g_{m b 6}\right) r_{o 6} r_{o 8}\right] / /\left[\left(g_{m 4}+g_{m b 4}\right) r_{o 4}\left(r_{o 2} / / r_{o l 0}\right)\right]
$$

Looking at the folded-cascode schematic of Fig. 5.16, we expect additional poles due to the stray capacitances of the other nodes along the signal path. However, each of these nodes exhibits an equivalent resistance on the order of $1 /\left(g_{m}+g_{m b}\right)$, which is much lower than $R_{o}$, so the output-node pole dominates the entire response. This is why the folded cascode is often regarded as a single stage op amp!
(a) For the two-stage CMOS op amp of Example 5.2, find $f_{b}$ and $f_{t}$ if $C_{c}=3 \mathrm{pF}$.

#### EXAMPLE 6.23

(b) Repeat, but for the folded-cascode CMOS op amp of Example 5.4 if $C_{c}=2.5 \mathrm{pF}$.

#### Solution

(a) From Example 5.2 we have $a_{0}=2,844 \mathrm{~V} / \mathrm{V}, R_{o 1}=r_{o 2} / / r_{o 4}=400 / / 200=$ $133 \mathrm{k} \Omega, R_{o 2}=r_{o 5} / / r_{o 6}=100 / / 200=66.7 \mathrm{k} \Omega$, and $g_{m 5}=2 \times 0.1 / 0.25=$ $1 /(1.25 \mathrm{k} \Omega)$. We thus write $R_{e q}=133+66.7+133 \times 66.7 / 1.25=7.31 \mathrm{M} \Omega$, so

$$
\begin{aligned}
f_{b} & =\frac{1}{2 \pi \times 7.31 \times 10^{6} \times 3 \times 10^{-12}}=7.34 \mathrm{kHz} \\
f_{t} & =a_{0} \times f_{b}=2,844 \times 7.34 \times 10^{3}=20.9 \mathrm{MHz}
\end{aligned}
$$

(b) From Example 5.4 we have $a_{0}=2,088 \mathrm{~V} / \mathrm{V}$ and $R_{o}=5.22 \mathrm{M} \Omega$, so

$$
\begin{aligned}
f_{b} & =\frac{1}{2 \pi \times 5.22 \times 10^{6} \times 2.5 \times 10^{-12}} \cong 12.2 \mathrm{kHz} \\
f_{t} & =2,088 \times 12.2 \times 10^{3}=25.5 \mathrm{MHz}
\end{aligned}
$$

### The Transient Response

Op amps are characterized both in the frequency and the time domains. An important time-domain characteristic is the transient response, which shows how an op amp circuit reacts to an input voltage step. The circuit commonly used is the unitygain voltage follower of Fig. $6.62 a$ because this is the most difficult configuration to stabilize, as we shall see in Chapter 7. To facilitate the transient analysis, refer to the simplified renditions of Fig. 6.63, where the second stage and the compensation
image_name:(a)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
name: A, type: OpAmp, value: A, ports: {InP: V1, InN: Vo, Out: Vo}
]
extrainfo:This is a unity-gain voltage follower circuit using an op-amp.

GND
(a)
image_name:(b)
description:The graph represents a small-signal transient response for a dominant-pole operational amplifier, focusing on the voltage response over time.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph illustrating the transient response of an operational amplifier.

2. **Axes Labels and Units:**
- The horizontal axis is labeled 't (s)' and represents time in seconds.
- The vertical axis is labeled 'V (V)' and represents voltage in volts.
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The graph shows an initial rapid increase in voltage followed by a gradual approach to a steady-state value.
- The input voltage, \( v_I \), is shown as a constant line at \( V_m \), indicating a step input.
- The output voltage, \( v_O \), starts at zero and rises exponentially towards \( V_m \), illustrating the charging behavior of the circuit.

4. **Key Features and Technical Details:**
- The curve representing \( v_O \) initially rises steeply and then flattens as it approaches \( V_m \), characteristic of a first-order system response.
- The time constant \( \tau \) is marked on the time axis as \( \tau = C_c / G_{m1} \), indicating the time it takes for \( v_O \) to reach approximately 63.2% of \( V_m \).

5. **Annotations and Specific Data Points:**
- The graph includes a reference line for \( \tau \), highlighting the time constant of the system.
- There are no specific numerical data points marked, but the behavior is typical of a dominant-pole system's response to a step input, where \( v_O \) asymptotically approaches \( v_I \).

(b)

FIGURE 6.62 (a) Voltage follower and (b) small-signal transient response for a dominant-pole op amp.
capacitance have been combined together to form an integrator. As long as the gain $a_{2}$ of this stage is sufficiently high, the integrator's input terminal will approximate a virtual ground, so we have $C_{c} d\left(v_{O}-0\right) / d t=i_{C}$, or

$$
\begin{equation*}
C_{c} \frac{d v_{O}}{d t}=i_{C} \tag{6.106}
\end{equation*}
$$

We make the following considerations:

- In dc steady state both circuits yield $i_{C}=0$ and $v_{O} \cong v_{I}$. Moreover, the inputstage bias current $I_{1}$ splits equally between the two halves of the differential pair.
- Applying a positive voltage step at the input will make $Q_{2} / M_{2}$ less conductive, so a greater portion of $I_{1}$ will be diverted to $Q_{1} / M_{1}$ to be subsequently replicated at the integrator's input by the current mirror. This results in $i_{C}>0$ and causes $C_{c}$ to charge up as per Eq. (6.106). As long as the step amplitude $V_{m}$ is sufficiently
image_name:(a)
description:
[
name: Q1, type: PNP, ports: {C: C1C2, B: vN, E: X1}
name: Q2, type: PNP, ports: {C: C1C2, B: vP, E: X2}
name: Q3, type: NPN, ports: {C: X1, B: X1, E: VEE}
name: Q4, type: NPN, ports: {C: X2, B: X1, E: VEE}
name: I1, type: CurrentSource, value: I1, ports: {Np: VCC, Nn: C1C2}
name: VI, type: VoltageSource, value: VI, ports: {Np: vP, Nn: GND}
name: Cc, type: Capacitor, value: Cc, ports: {Np: X2, Nn: out(a2)}
name: a2, type: OpAmp, value: a2, ports: {InP: GND, InN: X2, Out: out(a2)}
]
extrainfo:The circuit is a simplified equivalent of a 741 op amp. It consists of a differential pair (Q1, Q2) with current mirror loading (Q3, Q4) and a compensation capacitor (Cc) connected to an operational amplifier (a2). The input voltage (VI) controls the differential pair, and the output is taken from the operational amplifier.

(a)
image_name:(a)
description:
[
name: M1, type: PMOS, ports: {S: d1d2, D: x1, G: vN}
name: M2, type: PMOS, ports: {S: d1d2, D: InN(a2), G: vP}
name: M3, type: NMOS, ports: {S: VSS, D: x1, G: x1}
name: M4, type: NMOS, ports: {S: VSS, D: InN(a2), G: x1}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: d1d2}
name: VI, type: VoltageSource, value: VI, ports: {Np: vP, Nn: GND}
name: Cc, type: Capacitor, value: Cc, ports: {Np: InN(a2), Nn: vo}
name: a2, type: OpAmp, value: a2, ports: {InP: GND, InN: InN(a2), Out: vO}
]
extrainfo:The circuit is a simplified equivalent of a 741 op amp. It consists of a differential pair (M1, M2) with current mirror loading (M3, M4) and a compensation capacitor (Cc) connected to an operational amplifier (a2). The input voltage (VI) controls the differential pair, and the output is taken from the operational amplifier.

(b)

FIGURE 6.63 Simplified equivalents of (a) the 741 op amp and (b) the two-stage CMOS op amp (the foldedcascode CMOS op amp is similar, except that there is no second stage and $C_{c}$ is connected to ground.)
small, we can use the small-signal approximation to write $i_{C}=G_{m 1}\left(v_{P}-v_{N}\right)=$ $G_{m 1}\left(V_{m}-v_{o}\right)$, where $G_{m 1}$ is the input-stage transconductance. Substituting into Eq. (6.106) and rearranging gives

$$
\begin{equation*}
\tau \frac{d v_{O}}{d t}+v_{O}=V_{m} \tag{6.107}
\end{equation*}
$$

where

$$
\begin{equation*}
\tau=\frac{C_{c}}{G_{m 1}} \tag{6.108}
\end{equation*}
$$

Recall from basic circuit courses that the solution to the above differential equation is an exponential transient governed by the time constant $\tau$. For $v_{O}=0$, Eq. (6.107) reduces to $\tau d v_{o} / d t=V_{m}$, indicating an initial slope of $d v_{o} / d t=V_{m} / \tau$ (see Fig. 6.62b). As the transient dies out, $v_{o}$ eventually settles at $V_{m}$.

- We can obtain an insightful alternative expression for $\tau$ by noting that for $f=f_{t}$ we have

$$
V_{o}\left(j f_{t}\right)=\frac{1}{j 2 \pi f_{t} C_{c}} I_{c}=\frac{1}{j 2 \pi f_{t} C_{c}} G_{m 1}\left(V_{p}-V_{n}\right)
$$

But, we also have $V_{o}\left(j f_{t}\right)=a\left(j f_{t}\right) \times\left(V_{p}-V_{n}\right)=(1 / j) \times\left(V_{p}-V_{n}\right)$, so $G_{m 1} /\left(2 \pi f_{t} C_{c}\right)=1$. Combining with Eq. (6.108) gives

$$
\begin{equation*}
\tau=\frac{1}{2 \pi f_{t}} \tag{6.109}
\end{equation*}
$$

This provides a link between the frequency-domain parameter $f_{t}$ and the timedomain parameter $\tau$. The 741 op amp has $\tau=1 /\left(2 \pi \times 10^{6}\right)=159 \mathrm{~ns}$.

### Slew-Rate (SR) Limiting

If we raise $V_{m}$ further, the small-signal approximation ceases to hold. This is so because the $i_{C}$ characteristic as a function of the difference $v_{P}-v_{N}$ takes on the familiar $s$-shaped form of Section 4.5 , so the transient response becomes a sluggish exponential. Still, $v_{O}$ will settle at $V_{m}$ once the transient has died out. For $V_{m}$ sufficiently large, all of $I_{1}$ will be diverted to $Q_{2} / M_{2}$, so $i_{C}$ will saturate at $i_{C(\max )}=I_{1}$, causing $v_{O}$ to ramp up at the maximum possible rate. This rate is called the slew rate (SR) and is expressed in $\mathrm{V} / \mu \mathrm{s}$. By Eq. (6.106),

$$
\begin{equation*}
\mathrm{SR}=\left.\frac{d v_{o}}{d t}\right|_{\max }=\frac{I_{1}}{C_{c}} \tag{6.110}
\end{equation*}
$$

The 741 op amp has $I_{1}=19 \mu \mathrm{~A}$, so $\mathrm{SR}=(19 \mu \mathrm{~A}) /(30 \mathrm{pF})=0.633 \times 10^{6} \mathrm{~V} / \mathrm{s}=$ $0.633 \mathrm{~V} / \mu \mathrm{s}$, which is fairly close to the more conservative data-sheet value of $0.5 \mathrm{~V} / \mu \mathrm{s}$.

It is of interest to know the step amplitude $V_{m(\text { onset })}$ that marks the onset of SR limiting. This occurs for $V_{m \text { (onset) }} / \tau=\mathrm{SR}$, or $V_{m \text { (onset) }}=\mathrm{SR} /\left(2 \pi f_{t}\right)$. The 741 has $V_{m \text { (onset) }}=$ $0.5 \times 10^{6} /\left(2 \pi 10^{6}\right) \cong 80 \mathrm{mV}$.

#### Exercise 6.6

Find $\tau$, SR, and $V_{m(\text { onset })}$ for (a) the two-stage and (b) the folded-cascode CMOS op amps of Example 6.23. Assume $I_{1}=100 \mu \mathrm{~A}$ for both circuits.
Ans. (a) $7.73 \mathrm{~ns}, 33.3 \mathrm{~V} / \mu \mathrm{s}, 257 \mathrm{mV}$; (b) $6.24 \mathrm{~ns}, 40 \mathrm{~V} / \mu \mathrm{s}, 250 \mathrm{mV}$.

We can readily visualize transient responses via PSpice. The circuit of $6.64 a$ uses the 741 macro-model available in PSpice's Library to display the response to an input step of magnitude $V_{m}=10 \mathrm{mV}$. Recall from Fig. 5.2 that the differential input stage of the 741 involves four base-emitter junctions, so each junction is subjected to a step of $10 / 4=2.5 \mathrm{mV}$, which is quite adequate for the small-signal approximation. The actual response, shown in Fig. 6.64b, differs somewhat from the exponential form predicted by single-pole analysis, and also exhibits overshoot. This is due to the presence of additional pole frequencies above $f_{t}$, as per Fig. 6.59 (more on this in Chapter 7).

Using the $60-\mathrm{mV}$ rule of thumb we can state that raising $V_{m}$ to $2 \times 60=120 \mathrm{mV}$ will make the current of one side of the differential stage ten times as large as the other side, thus bringing the 741 on the verge of slew-rate limiting. The pulse response of Fig. $6.65 a$ is based on $V_{m}=1.0 \mathrm{~V}$, a convincingly large overdrive. Consequently, $v_{O}$ ramps up at a constant rate of about $0.5 \mathrm{~V} / \mu \mathrm{s}$, taking about $2 \mu \mathrm{~s}$ to approach the $1.0-\mathrm{V}$ plateau. As $v_{O}$ approaches the plateau, the op amp ceases to slew-rate limit and $v_{O}$ completes the last part of the transient in small-signal fashion, according to Fig. 6.64b.

Slew-rate limiting is a form of nonlinear distortion that limits the useful frequency range for large-signal operation. This distortion is illustrated in Fig. 6.65b for the case of a sinusoidal input

$$
v_{I}=V_{m} \sin (2 \pi f t)
$$

with $V_{m}=10 \mathrm{~V}$ and $f=15 \mathrm{kHz}$. The slope of a sinusoid is steepest at the $0-\mathrm{V}$ crossings, where we have

$$
\left|\frac{d v_{t}}{d t}\right|_{\max }=\left|-2 \pi f V_{m} \cos (2 \pi f t)\right|_{\max }=2 \pi f V_{m}
$$

image_name:(a)
description:
[
name: V_I, type: VoltageSource, value: V_I, ports: {Np: vI, Nn: GND}
name: μA741, type: OpAmp, value: μA741, ports: {InP: vI, InN: vO, OutP: vO, OutN: GND, Vdd: VCC, -Vdd: VEE}
name: R_L, type: Resistor, value: 2 kΩ, ports: {N1: vO, N2: GND}
]
extrainfo:The circuit is an op-amp voltage follower configuration using a μA741 operational amplifier. It has a voltage source V_I connected to the non-inverting input and a resistor R_L connected to the output, providing a load to ground. The op-amp is powered by a dual supply VCC (+15V) and VEE (-15V).

image_name:(b) Small-signal step response
description:The graph is a time-domain waveform illustrating the small-signal step response of a μA741 operational amplifier configured as a voltage follower.

1. **Axes Labels and Units:**
- The horizontal axis represents time, labeled "Time (μs)" indicating microseconds.
- The vertical axis represents voltage, labeled "(mV)" indicating millivolts.

2. **Overall Behavior and Trends:**
- The graph shows a step input voltage, labeled as \(v_I\), which abruptly rises to 10 mV at time \(t = 0\) and remains constant thereafter.
- The output voltage, labeled as \(v_O\), follows the input with a slight delay and initially rises rapidly, then gradually approaches the input voltage level.
- The response exhibits a typical exponential rise, characteristic of the charging behavior in RC circuits, before it stabilizes.

3. **Key Features and Technical Details:**
- The output voltage \(v_O\) begins at 0 mV and rises sharply, reaching close to the input voltage level of 10 mV around 0.4 μs.
- There is a slight overshoot observed where \(v_O\) exceeds 10 mV briefly before settling back.
- The waveform stabilizes and flattens out, indicating steady-state behavior beyond 0.5 μs.

4. **Annotations and Specific Data Points:**
- The graph is annotated with arrows indicating \(v_I\) and \(v_O\), clearly showing the input and output voltages.
- The gridlines assist in determining the time constant and settling time of the response, which appears to be around 0.5 μs for the system to reach steady-state.

This graph effectively demonstrates the transient response characteristics of a voltage follower using a μA741 op-amp, highlighting the time delay and overshoot phenomena inherent in such configurations.

(b)

FIGURE 6.64 (a) PSpice circuit to display the 741 transient responses. (b) Small-signal step response.
image_name:(a)
description:The graph labeled (a) is a time-domain waveform illustrating the slew-rate limited response of a 741 op-amp voltage follower to a pulse input. The x-axis represents time in microseconds (µs), ranging from 0 to 15 µs, while the y-axis represents voltage in volts (V), ranging from 0 to 1 V.

**Overall Behavior and Trends:**
The input voltage \( v_I \) is depicted as a gray square wave, transitioning from 0 V to 1 V at 5 µs intervals. The output voltage \( v_O \), shown in black, follows the input with a noticeable delay due to the slew rate limitation of the op-amp. The output waveform exhibits a linear rise and fall, unable to keep up with the steep transitions of the input, which is characteristic of a slew-rate limited response.

**Key Features and Technical Details:**
- **Slew Rate (SR):** The graph highlights the slew rate (SR) limitation, which is the maximum rate of change of the output voltage. This is indicated by the sloped sections of the output waveform, where the op-amp cannot increase or decrease the output voltage fast enough to match the input.
- **Settling Time:** The output takes approximately 5 µs to reach the steady-state level of the input, indicating the time it takes for the output to stabilize after a change in the input.

**Annotations and Specific Data Points:**
- The graph includes annotations indicating the input \( v_I \) and output \( v_O \) voltages, as well as the slew rate (SR) region where the output is limited by the op-amp's capabilities.
- The gridlines assist in visualizing the timing of the transitions and the slew rate effect on the output waveform.
image_name:(b)
description:The graph labeled as Figure 6.65(b) illustrates the slew-rate limited response of a μA741 op-amp configured as a voltage follower, responding to a sinusoidal input.

**Type of Graph and Function:**
- This is a time-domain waveform graph showing voltage over time.

**Axes Labels and Units:**
- The x-axis represents time in microseconds (μs), ranging from 0 to 100 μs.
- The y-axis represents voltage in volts (V), ranging from -10 V to 10 V.

**Overall Behavior and Trends:**
- The input voltage \(v_I\) is depicted as a sinusoidal waveform with a smooth, continuous oscillation between -10 V and 10 V.
- The output voltage \(v_O\), however, shows a distorted waveform due to the slew rate limitation of the op-amp. It has a more triangular shape compared to the input sinusoid.
- The output cannot follow the rapid changes of the input, resulting in a linear ramp (triangular wave) rather than a smooth sine wave.

**Key Features and Technical Details:**
- The slew rate (SR) is indicated, showing the maximum rate of change of the output voltage. This is the steepest part of the output waveform.
- The output waveform \(v_O\) lags behind the input \(v_I\) in terms of both phase and amplitude due to the slew rate limitation.
- The graph highlights the inability of the op-amp to accurately reproduce the input waveform at higher frequencies or amplitudes.

**Annotations and Specific Data Points:**
- The graph is annotated with labels for the input \(v_I\) and output \(v_O\) voltages, as well as the slew rate (SR) indication.
- Gridlines are present to assist in identifying the time intervals and voltage levels, which are crucial for analyzing the slew rate effect.

FIGURE 6.65 Slew-rate limited responses of the 741 follower to (a) a pulse and (b) a sinusoid.

If we want to avoid slew-rate limiting, this slope must be less than the slew rate,

$$
\begin{equation*}
2 \pi f V_{m} \leq \mathrm{SR} \tag{6.111}
\end{equation*}
$$

For instance, a 741 op amp with $V_{m}=10 \mathrm{~V}$ requires that its frequency $f$ meet the condition

$$
f \leq \frac{\mathrm{SR}}{2 \pi V_{m}}=\frac{0.5 / 10^{-6}}{2 \pi 10} \cong 8 \mathrm{kHz}
$$

Figure $6.65 b$ shows the effect of exceeding the above limit with $f=15 \mathrm{kHz}(>8 \mathrm{kHz})$. It is apparent that as soon as the slope of $v_{I}$ exceeds the $\mathrm{SR}, v_{O}$ ceases to track $v_{I}$ and ramps up or down at a fixed rate of $\pm 0.5 \mathrm{~V} / \mu \mathrm{s}$. We can avoid slew-rate limiting either by lowering $f$ to 8 kHz or less while keeping $V_{m}=10 \mathrm{~V}$, or by suitably lowering $V_{m}$ while keeping $f=15 \mathrm{kHz}$. In fact, we can turn around Eq. (6.111) and find $V_{m} \leq$ $\mathrm{SR} /(2 \pi f)=\left(0.5 / 10^{-6}\right) /\left(2 \pi \times 15 \times 10^{3}\right) \cong 5.3 \mathrm{~V}$. Likewise, if we wish the 741 follower to give an undistorted sine wave over the entire audio range, whose upper limit is $f=20 \mathrm{kHz}$, then we must ensure that $V_{m} \leq\left(0.5 / 10^{-6}\right) /\left(2 \pi \times 20 \times 10^{3}\right) \cong 4 \mathrm{~V}$.

### Insightful Expressions for the Slew Rate

Combining Eqs. (6.108) through (6.110) we can express the slew rate in the insightful alternative form

$$
\begin{equation*}
\mathrm{SR}=2 \pi \frac{I_{1}}{G_{m 1}} f_{t} \tag{6.112}
\end{equation*}
$$

where $f_{t}$ is the op amp's transition frequency, $G_{m 1}$ is the transconductance of the differential input pair, and $I_{1}$ is the pair's bias current. In the case of CMOS op amps we use $G_{m 1}=2\left(I_{1} / 2\right) / V_{O V 1}=I_{1} / V_{O V 1}$ to obtain yet another insightful form,

$$
\begin{equation*}
\mathrm{SR}_{\mathrm{CMOS}}=2 \pi V_{O V 1} f_{t} \tag{6.113}
\end{equation*}
$$

We make the following observations:

- Whether bipolar or CMOS, an op amp with a high $f_{t}$ is likely to exhibit also a high SR.
- The IC designer can raise the SR by raising $I_{1}$ so as to charge/discharge $C_{c}$ more rapidly. The price is more power dissipation and, in the bipolar case, a higher input bias current $I_{B}\left(=I_{1} / 2 \beta_{F}\right)$.
- The IC designer can raise the SR by suitably reducing the transconductance of the differential input pair, such as via degeneration or other forms (see, for instance, Problem 5.11). The notoriously low transconductance of FETs compared to BJTs comes as a blessing in this case as it helps achieve higher slew rates. The price of a reduced transconductance is less voltage gain.
- In the case of CMOS op amps the IC designer can raise the SR by raising the overdrive voltage $V_{O V 1}$ of the differential input pair (another way of signifying low $G_{m 1}$ ). This is another reason why preference is given to $p$ MOSTETs in the differential pair: for similar dimensions and biasing conditions, the lower mobility of holes compared to electrons makes $V_{O V p}$ two to three times higher than $V_{O V n}$.

### Current-Feedback Amplifiers

The current-feedback amplifier (CFA) circuit of Fig. 5.39 reveals the presence of a number of internal low-resistance nodes along with a single high-resistance node denoted as node $C$. We anticipate the frequency response to be dominated by the pole associated with this one node. Denoting this node's total stray capacitance to ground as $C_{e q}$, as depicted in Fig. $6.66 a$, we have $V_{o}=z(s) I_{n}$, where $z(s)=R_{e q} / /\left[1 /\left(s C_{e q}\right)\right]$. Expanding and letting $s \rightarrow j 2 \pi f$, we readily find the gain of the CFA as

$$
\begin{equation*}
z(j f)=\frac{V_{o}}{I_{n}}=\frac{R_{e q}}{1+j f / f_{b}} \tag{6.114}
\end{equation*}
$$

image_name:Fig. 6.66 a
description:
[
name: Q5, type: PMOS, ports: {S: VCC, D: X1, G: X1}
name: Q7, type: PMOS, ports: {S: VCC, D: C, G: X1}
name: Q10, type: NMOS, ports: {S: VEE, D: X2, G: X2}
name: Q8, type: NMOS, ports: {S: VEE, D: C, G: X2}
name: OpAmp, type: OpAmp, ports: {InP: Vp, GND: Vn, Out: Vn}
name: Req, type: Resistor, value: Req, ports: {N1: C, N2: GND}
name: Ceq, type: Capacitor, value: Ceq, ports: {Np: C, Nn: GND}
name: OpAmp, type: OpAmp, ports: {InP: C, GND: Vn, Out: VO}
]
extrainfo:The circuit is a current-feedback operational amplifier (CFA) with a PMOS and NMOS differential pair. The frequency response is dominated by a pole associated with node C, with the gain determined by Req and Ceq. The gain expression is z(jf) = Req / (1 + jf/fb), where fb is the frequency at which gain drops to 70.7% of its low-frequency value.

(a)
image_name:FIGURE 6.66
description:The graph in FIGURE 6.66 is a Bode plot illustrating the frequency response of a current-feedback operational amplifier (CFA). The graph is plotted on a logarithmic scale, with the x-axis representing frequency \( f \) in decades and the y-axis representing the gain \( z(jf) \) also in decades.

Axes Labels and Units:
- **X-axis (Frequency \( f \))**: Measured in decades.
- **Y-axis (Gain \( z(jf) \))**: Measured in decades.

Overall Behavior and Trends:
- The graph shows a flat region at lower frequencies where the gain is constant and equal to \( R_{eq} \), representing the DC value of gain.
- At a specific frequency \( f_b \), the gain starts to decrease. This frequency \( f_b \) is where the gain drops to 70.7% of its low-frequency value, corresponding to a drop to \( 1/\sqrt{2} \) of its initial value.
- Beyond \( f_b \), the gain decreases linearly with a slope of \(-1 \text{ dec/dec}\), indicating a roll-off of one decade per decade in frequency.

Key Features and Technical Details:
- **\( R_{eq} \)**: Represents the DC gain value, the initial flat gain level.
- **\( f_b \)**: The breakpoint frequency where the gain begins to decrease, calculated as \( f_b = \frac{1}{2 \pi R_{eq} C_{eq}} \).
- The slope of the line after \( f_b \) is \(-1 \text{ dec/dec}\), which is typical for a single-pole roll-off.

Annotations and Specific Data Points:
- A vertical line at \( f_b \) marks the transition from the flat gain region to the sloped roll-off region.
- The graph includes an annotation of the slope \(-1 \text{ dec/dec}\) in the roll-off region, indicating the rate of gain decrease.

This plot effectively demonstrates the frequency-dependent behavior of the CFA, with a clear transition from constant gain to a decreasing gain as frequency increases beyond \( f_b \).

(b)

FIGURE 6.66 The frequency response of a current-feedback op amp (CFA).
where $R_{e q}$ represents the dc value of gain, and

$$
\begin{equation*}
f_{b}=\frac{1}{2 \pi R_{e q} C_{e q}} \tag{6.115}
\end{equation*}
$$

represents the frequency at which gain drops to $1 / \sqrt{2}(=70.7 \%)$ of its low-frequency value. Above $f_{b}$ gain rolls off by one $\Omega$-decade for every Hz -decade, or by $-1 \mathrm{dec} / \mathrm{dec}$, as shown. Since it has the dimensions of impedance, $z$ is also referred to as transimpedance gain, and the CFA as transimpedance amplifier.

We observe that the current dumped into $C_{e q}$ at the onset of a step in $V_{p}$ depends on the external resistance on which node $V_{n}$ is terminated as well as the step magnitude. Consequently, there are no current-saturation effects in CFAs, and, hence, no slew-rate-limiting. For instance, with $C_{e q} \sim 1 \mathrm{pF}$ and $I_{n} \sim 1 \mathrm{~mA}$ the initial slope is $d V_{o} / d t \sim 10^{-3} / 10^{-12}=10^{9}=1,000 \mathrm{~V} / \mu \mathrm{s}$. To fully appreciate the dynamic advantages of the CFA we need to investigate its frequency response in negative-feedback operation, in Chapter 7.

## 6.10 DIODE SWITCHING TRANSIENTS

Up to now diodes have been assumed to turn on or off instantaneously. An actual pn junction diode takes time to switch from one state to the other because charge must be transferred in or out of the device to effect the switching, and charge transfers cannot occur instantaneously. The transient behavior of a $p n$ junction is governed by the charge-control equation ${ }^{1,8}$

$$
\begin{equation*}
i_{D}=\frac{d Q_{j}}{d t}+\frac{d Q_{F}}{d t}+\frac{Q_{F}}{\tau_{F}} \tag{6.116}
\end{equation*}
$$

where $i_{D}$ is the diode current, $Q_{j}$ is the charge of the junction capacitance $C_{j}$, and $Q_{F}$ is the excess minority charge in forward bias. In words, the current $i_{D}$ supplied to a diode in the forward mode goes toward (a) charging up the capacitance $C_{j}$, (b) building up the excess charge $Q_{F}$, and (c) sustaining the charge $Q_{F}$ built up to that point. Once all transients have died out, the diode reaches its dc steady state, where $i_{D}=Q_{F} / \tau_{F}$. Consequently, the time-constant $\tau_{F}$ represents the ratio $Q_{F} / i_{D}$ in the forward steady state.

Recall that most practical junctions are fabricated with one side much more heavily doped than the other. For a junction with $N_{A} \gg N_{D}$ we can approximate $Q_{F} \cong$ $Q_{p}$; moreover, $\tau_{F} \cong \tau_{p}=L_{p}^{2} / D_{p}$ in the case of a long-base diode, $\tau_{F}=W_{n}^{2} /\left(2 D_{p}\right)$ in the short-base case (refer to Figs. 1.43 and 1.45). Likewise, for a junction with $N_{D} \gg N_{A}$ we have $Q_{F} \cong Q_{n}$, and $\tau_{F} \cong \tau_{n}=L_{n}^{2} / D_{n}$ for a long-base diode, $\tau_{F}=W_{p}^{2} /\left(2 D_{n}\right)$ for a short-base diode. In the long-base case $\tau_{F}$ is called the minority-carrier mean recombination time, or also the minority-carrier mean lifetime, whereas in the short-base case it is called the minority-carrier mean transit time and it is denoted as $\tau_{T}$ (this is also the symbol used by PSpice).

Figure 6.67 shows a PSpice circuit to display the switching characteristics of a diode having the parameters shown in the table. Figure 6.68 shows all relevant
image_name:Figure 6.67
description:
[
name: VS, type: VoltageSource, ports: {Np: VS, Nn: GND}
name: R, type: Resistor, value: 4.3kΩ, ports: {N1: VS, N2: vD}
name: D, type: Diode, ports: {Na: vD, Nc: GND}
]
extrainfo:The circuit is used to visualize the switching transients of a pn junction diode. The diode parameters are: Is = 2 fA, n = 1, τT = 10 ns, Cj0 = 2.5 pF, φ0 = 0.8 V, m = 0.33. The voltage source VS is connected to the resistor R and diode D in series, with the ground node GND connected to the negative terminal of the voltage source and cathode of the diode.

FIGURE 6.67 PSpice circuit to visualize the switching
transients of a pn junction diode.
waveforms for the case in which the driving source $v_{S}$ is switched from $V_{R}(=-2 \mathrm{~V})$ to $V_{F}(=5 \mathrm{~V})$ at $t=t_{0}=0 \mathrm{~ns}$, and back to -2 V at $t=t_{2}=50 \mathrm{~ns}$, with the diode in steady state prior to $t=t_{0}$. We make the following observations.

- Right after the leading edge of $v_{S}$ there is no excess charge $Q_{F}$ yet, so Eq. (6.116) simplifies as

$$
\begin{equation*}
i_{D} \cong \frac{d Q_{j}}{d t} \tag{6.117}
\end{equation*}
$$

indicating that initially all of $i_{D}$ goes toward charging $C_{j}$. As $C_{j}$ charges up, $v_{D}$ increases until the diode reaches the edge of conduction (EOC) at the instant $t_{1}$ when $v_{D} \cong 0.6 \mathrm{~V}$. Recall from Chapter 1 that the junction capacitance is

$$
\begin{equation*}
C_{j}\left(v_{D}\right)=\frac{C_{j 0}}{\left(1-v_{D} / \phi_{0}\right)^{m}} \tag{6.118}
\end{equation*}
$$

where $C_{j 0}$ is the zero-bias value of $C_{j}, \phi_{0}$ is the built-in potential, and $m$ the grading coefficient. Since $C_{j}$ is nonlinear, its charging process is rather complex, but we can estimate its charging time $t_{1}-t_{0}\left(=t_{1}\right)$ by approximating Eq. (6.117) as

$$
i_{D(\mathrm{avg})} \cong \frac{\Delta Q_{j}}{\Delta t}=\frac{C_{j(\mathrm{eq})} \Delta v_{D}}{t_{1}-t_{0}}
$$

where $i_{D(\text { avg })}$ is the average of $i_{D}\left(t_{0}^{+}\right)=[5-(-2)] / 4.3=1.63 \mathrm{~mA}$ and $i_{D}\left(t_{1}\right)=$ $(5-0.6) / 4.3=1.02 \mathrm{~mA}$, that is, $i_{D(\text { avg })}=(1.63+1.02) / 2=1.3 \mathrm{~mA}$, and $\Delta v_{D}=v_{D}\left(t_{1}\right)-v_{D}\left(t_{0}\right)=0.6-(-2)=2.6 \mathrm{~V}$. Making the crude approximation $C_{j(\mathrm{eq})} \cong C_{j 0}=2.5 \mathrm{pF}$ (see Problem 6.49 for a better estimate) we get $t_{1} \cong 2.5 \times$ $10^{-12} \times 2.6 /\left(1.3 \times 10^{-3}\right)=5 \mathrm{~ns}$. This well agrees with $t_{1}=4.77 \mathrm{~ns}$ measured via the cursor facility of PSpice.

- Following $t_{1}$, the diode is brought from the EOC $\left(v_{D} \cong 0.6 \mathrm{~V}\right)$ to full conduction $\left(v_{D} \cong 0.7 \mathrm{~V}\right)$, and this is when $Q_{F}$ comes into play. The change in $v_{D}$ from 0.6 V to 0.7 V is small enough that we can ignore the term $d Q_{j} / d t$ and simplify Eq. (6.116) as

$$
\begin{equation*}
I_{F} \cong \frac{d Q_{F}}{d t}+\frac{Q_{F}}{\tau_{F}} \tag{6.119}
\end{equation*}
$$

image_name:Input vS (V)
description:The graph labeled "Input vS (V)" is a time-domain waveform depicting the behavior of an input voltage signal over time.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph illustrating the input voltage, denoted as \( v_S \), as a function of time.

2. **Axes Labels and Units:**
- The x-axis represents time in nanoseconds (ns), ranging from 0 to 100 ns.
- The y-axis represents the input voltage in volts (V), with a range from -2 V to 5 V.
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The waveform starts at 0 V at \( t = 0 \) ns and quickly rises to 5 V, maintaining this level until around 50 ns.
- At approximately 50 ns, the voltage drops sharply back to 0 V and remains there for the rest of the observed time period.
- This behavior indicates a square wave or pulse waveform with a high period from 0 to 50 ns and a low period from 50 to 100 ns.

4. **Key Features and Technical Details:**
- The waveform transitions from 0 V to 5 V almost instantaneously at the start, indicating a step input.
- The return to 0 V at 50 ns is similarly abrupt, signifying a sharp transition characteristic of digital or pulse signals.

5. **Annotations and Specific Data Points:**
- The graph is annotated with \( V_F \) at the high level (5 V) and \( V_R \) at the low level (0 V).
- The waveform is labeled with \( v_S \) to indicate it represents the input voltage signal.

This graph is typical of input signals used in switching circuits or digital electronics, where rapid transitions between high and low states are common.
image_name:Diode voltage vD (V)
description:The provided graph titled "Diode voltage vD (V)" is a time-domain waveform illustrating the behavior of diode voltage over time. The graph is part of a multi-panel figure displaying various related waveforms, but the focus here is on the diode voltage.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform showing the diode voltage (vD) as a function of time.

2. **Axes Labels and Units:**
- The x-axis represents time in nanoseconds (ns), ranging from 0 to 100 ns.
- The y-axis represents diode voltage (vD) in volts (V), ranging from -2 V to 1 V.

3. **Overall Behavior and Trends:**
- The diode voltage (vD) starts at -2 V at t0 and quickly rises to approximately 0.6 V by t1, indicating the diode's end of conduction (EOC) state.
- From t1 to t2, the voltage remains relatively constant at around 0.7 V, indicating full conduction.
- At t2, the voltage begins to decline, reaching back towards -2 V by t3, showing the diode returning to its initial state.
- The waveform exhibits an initial rapid rise followed by a plateau and a subsequent decline, characteristic of diode switching behavior.

4. **Key Features and Technical Details:**
- **t0 to t1:** Rapid increase in voltage from -2 V to 0.6 V, marking the diode's transition to conduction.
- **t1 to t2:** Voltage plateau at approximately 0.7 V, indicating stable conduction.
- **t2 to t3:** Exponential decay back to -2 V, reflecting the diode turning off.
- The time intervals and transitions align with the described diode behavior in the context, particularly the exponential buildup and decay of charge.

5. **Annotations and Specific Data Points:**
- The points t0, t1, t2, and t3 are marked, correlating with key transition events in the diode's operation.
- The term EOC (End of Conduction) is annotated at the points where the diode transitions to and from conduction.
- The plateau region corresponds to the full conduction state of the diode, as described in the context.

This graph effectively captures the dynamic response of the diode voltage in a circuit as it transitions between different states of conduction over time.
image_name:Current iD (mA)
description:The graph titled "Current iD (mA)" is a time-domain waveform illustrating the behavior of diode current over a period of 100 nanoseconds (ns).

1. **Axes Labels and Units:**
- The horizontal axis represents time in nanoseconds (ns), ranging from 0 to 100 ns.
- The vertical axis represents the current iD in milliamperes (mA), ranging from -1 mA to 2 mA.

2. **Overall Behavior and Trends:**
- Initially, at time t0, the current iD sharply rises to approximately 2 mA.
- It quickly drops to a steady-state value of 1 mA, where it remains constant from t1 to t2, indicating a stable conduction phase.
- After t2, the current begins to decrease, reaching a value slightly above 0 mA by t3.
- The curve shows a smooth transition from the steady state to a lower current, indicative of a discharge or reverse recovery phase.

3. **Key Features and Technical Details:**
- The peak current is observed at the very beginning, around 2 mA.
- The stable conduction phase is marked by a constant current of 1 mA.
- The decrease in current post t2 suggests a reverse recovery characteristic, common in diode switching behavior.

4. **Annotations and Specific Data Points:**
- The graph is annotated with markers at significant points, such as the initial peak and the transition points t1, t2, and t3.
- These markers help in identifying the phases of the diode operation: initial conduction, stable conduction, and reverse recovery.

This graph effectively demonstrates the transient and steady-state behavior of diode current in response to changes in voltage across the diode, aligning with the theoretical considerations of diode switching dynamics.
image_name:Charge QF (pC)
description:The graph titled "Charge QF (pC)" is a time-domain waveform illustrating the charge QF in picocoulombs (pC) over time in nanoseconds (ns). The x-axis represents time, ranging from 0 to 100 ns, with linear scaling and significant gridlines at intervals such as 0, 10, 20, etc. The y-axis represents charge, ranging from -10 to 10 pC, also in a linear scale.

**Overall Behavior and Trends:**
- Initially, the charge QF starts at 0 pC at time t0.
- From t0 to approximately 20 ns, the charge increases exponentially, reaching a peak near 10 pC. This indicates an exponential buildup of charge as described in the context.
- After reaching the peak, the charge remains relatively constant around 10 pC until about 50 ns.
- At approximately 50 ns, there is a sharp decrease in charge, indicating a transition or discharge event.
- Following this, the charge decreases exponentially toward 0 pC, continuing beyond 100 ns.

**Key Features and Technical Details:**
- The exponential increase and decrease are governed by the time constant τF = 10 ns, as mentioned in the context.
- The steady-state value of QF is approximately 10 pC, which matches the calculated QF(s) = τF * IF = 10 pC.

**Annotations and Specific Data Points:**
- The graph includes markers at significant points such as the initial buildup, peak, and discharge points.
- The transition at around 50 ns is marked, corresponding to a change in the circuit conditions, likely related to the diode's conduction state.

This graph effectively visualizes the dynamic behavior of charge QF in response to changes in the circuit, highlighting both the buildup and discharge phases with clear exponential trends.

FIGURE 6.68 Relevant waveforms for the circuit of Fig. 6.67.
where $I_{F} \cong\left(V_{F}-V_{D(\text { (n) })}\right) / R=(5-0.7) / 4.3=1 \mathrm{~mA}$. The solution to this equation is an exponential buildup of $Q_{F}$, governed by the time constant $\tau_{F}=\tau_{T}=10 \mathrm{~ns}$ and tending asymptotically toward the steady-state value

$$
Q_{F(\mathrm{~s})}=\tau_{F} I_{F}=10 \times 10^{-9} \times 10^{-3}=10 \mathrm{pC}
$$

image_name:(a)
description:The graph labeled "(a)" represents the buildup of minority hole concentration in a semiconductor diode. The graph is a time-domain plot showing the exponential buildup of hole concentration over distance in the n-region of a long-base diode, where \( N_A \gg N_D \).

1. **Type of Graph and Function:**
- The graph is a time-domain waveform illustrating the exponential buildup of minority carrier concentration.

2. **Axes Labels and Units:**
- The horizontal axis \( x \) represents the position in the n-region, with a scale starting from 0 to \( x_n \).
- The vertical axis \( p_n(x) \) represents the hole concentration, starting from 0 and increasing upwards.
- There are no explicit units provided, but the context implies that the units are consistent with semiconductor physics, likely in terms of distance (e.g., micrometers) and concentration (e.g., holes per cubic centimeter).

3. **Overall Behavior and Trends:**
- The graph shows several curves representing the hole concentration at different times, with time \( t \) increasing upwards.
- Each curve exhibits an exponential increase from the origin, starting at a lower concentration and rising towards a steady-state value \( p_{n0} \) at \( x_n \).
- The curves become progressively steeper as time increases, indicating a faster buildup of hole concentration.

4. **Key Features and Technical Details:**
- The initial slope of the curves is defined by the forward current \( I_F \), and the area under each curve represents the total charge \( Q_p \).
- The steady-state concentration \( p_{n0} \) is marked on the vertical axis, showing the maximum concentration reached at \( x_n \).

5. **Annotations and Specific Data Points:**
- The graph includes an annotation indicating the direction of increasing time, emphasizing the dynamic nature of the buildup process.
- The curves tend asymptotically towards \( p_{n0} \), which is a critical value in this context as it represents the equilibrium concentration.
image_name:(b)
description:The graph labeled "(b)" depicts the minority hole distribution during the removal of the hole charge \(Q_{p}\) in a semiconductor device.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph illustrating the exponential decay of minority carrier concentration over time in the \(n\) region of a semiconductor.

2. **Axes Labels and Units:**
- The horizontal axis represents the position \(x\) within the \(n\) region, ranging from 0 to \(x_n\).
- The vertical axis represents the hole concentration \(p_n(x)\) at a given position \(x\), with \(p_n(x_n)\) denoting the concentration at the edge of the \(n\) region.

3. **Overall Behavior and Trends:**
- The curves show an exponential decay of hole concentration over time. Each curve represents the hole concentration profile at a different time, with time increasing as indicated by the arrow.
- The concentration \(p_n(x)\) decreases from an initial value \(p_{n0}\) at \(x = x_n\) towards zero as \(x\) approaches zero.
- As time progresses, the concentration decreases more rapidly, indicating the removal of hole charge \(Q_{p}\).

4. **Key Features and Technical Details:**
- The initial slope at \(x = x_n\) is determined by the forward current \(I_F\).
- The curves become progressively flatter over time, illustrating the exponential decay towards equilibrium.
- The area under each curve decreases with time, corresponding to the reduction in total hole charge \(Q_{p}\).

5. **Annotations and Specific Data Points:**
- The graph is annotated with arrows indicating the direction of increasing time.
- The initial concentration \(p_{n0}\) is marked on the vertical axis at \(x = x_n\).

This graph effectively illustrates the transient behavior of minority carriers in the \(n\) region during the removal phase, highlighting the exponential decay of hole concentration over time and space.

FIGURE 6.69 Minority hole distributions during (a) the buildup and (b) the removal of the hole charge $Q_{p}$.

The buildup of $Q_{F}$ is depicted in Fig. 6.69a for the case of a long-base diode with $N_{A} \gg N_{D}$ so that $Q_{F} \cong Q_{p}$. Recall that $I_{F}$ defines the initial slope of the excess hole concentration in the $n$ region, and the area defines $Q_{p}$ itself. Consequently, all curves exhibit the same slope at $x=x_{n}$, and the area builds up exponentially with time.

- Following the trailing edge of $v_{S}$ at the instant $t_{2}=50 \mathrm{~ns}$, we need to remove the stored charge $Q_{F}$ if we want to bring the diode back to the edge of conduction, now more properly called the edge of cutoff (EOC). Charge removal is governed by the equation

$$
\begin{equation*}
I_{R} \cong \frac{d Q_{F}}{d t}+\frac{Q_{F}}{\tau_{F}} \tag{6.120}
\end{equation*}
$$

where $I_{R} \cong\left(V_{R}-V_{D(\text { on })}\right) / R=(-2-0.7) / 4.3=-0.62 \mathrm{~mA}$. The solution to this equation is an exponential decay of $Q_{F}$, again governed by the time constant $\tau_{F}=\tau_{T}=10 \mathrm{~ns}$ and tending asymptotically toward the (fictitious) steadystate value

$$
Q_{F}(\infty)=\tau_{F} I_{R}=10 \times 10^{-9} \times(-0.62) 10^{-3}=-6.2 \mathrm{pC}
$$

The decay holds up to the instant $t_{3}$ at which $Q_{F}$ becomes to zero (hence the reason for calling $Q_{F}(\infty)$ fictitious). To find the time interval $t_{S}=t_{3}-t_{2}$, aptly called the storage time, we use ${ }^{7}$

$$
t_{S}=\tau_{F} \ln \frac{Q_{F}\left(t_{2}\right)-Q_{F}(\infty)}{Q_{F}\left(t_{3}\right)-Q_{F}(\infty)}=\tau_{F} \ln \frac{\tau_{F} I_{F}-\tau_{F} I_{R}}{0-\tau_{F} I_{R}}
$$

that is,

$$
\begin{equation*}
t_{S}=\tau_{F} \ln \frac{I_{F}-I_{R}}{-I_{R}} \tag{6.121}
\end{equation*}
$$

Presently, $t_{S}=(10 \mathrm{~ns}) \ln [(1+0.62) / 0.62]=9.6 \mathrm{~ns}$. This well agrees with the measured PSpice value of 9.5 ns . The removal of $Q_{F}$ is depicted in Fig. 6.69b, where we note that the initial slope is now defined by $I_{R}$, which is negative.

- Once all the stored charge has been removed, the diode will retrace the initial voltage transient, but in reverse. Were $C_{j}$ linear, the reverse transient would be an exponential transient from +0.6 V to -2 V governed by the time constant $\tau=R C_{j}$. In practice this transient is pseudo exponential, a bit slower at the beginning where $C_{j} \cong 2 C_{j 0}$, but getting faster as $C_{j}$ decreases in reverse bias, where $C_{j}<C_{j 0}$.
Looking at the waveforms of $v_{D}$ and $i_{D}$ we observe that the diode starts conducting right away when we turn it on. However, when we try to turn it off, it continues to remain on for $t_{s}$ nanoseconds. During this time it acts as a $\sim 0.7-\mathrm{V}$ battery and the reverse current, far from dropping instantaneously to zero as it would in the case of an ideal diode, remains at $I_{R}\left(\left|I_{R}\right| \geqslant 0\right)$, as confirmed by the waveform of $i_{D}$. It is apparent that the storage time $t_{S}$ can be a drawback, especially in high-speed applications.

According to Eq. (6.120) $t_{S}$ depends on the intrinsic $p n$-junction parameter $\tau_{F}$ as well as on the user-provided drives $I_{F}$ and $I_{R}$. Short-base diodes are preferable in high-speed applications because they have $\tau_{T} \ll \tau_{F}$. We can also reduce the logarithmic term of Eq. (6.121) by driving the diode with a large reverse current $I_{R}$ to wipe out the stored charge more rapidly. However, other design constraints may limit the reverse drive, indicating that the circuit designer must learn to live with storage-time limitations.

If a diode has $t_{S}=25 \mathrm{~ns}$ with $I_{F}=10 \mathrm{~mA}$ and $I_{R}=-2 \mathrm{~mA}$, find $t_{S}$ if $I_{F}=4 \mathrm{~mA}$ and $I_{R}=-5 \mathrm{~mA}$. Comment.

#### Solution

Imposing $25 \mathrm{~ns}=\tau_{F} \ln [(10+2) / 2]$ gives $\tau_{F} \cong 14 \mathrm{~ns}$. (This provides a means of finding $\tau_{F}$ experimentally via storage-time and current-drive measurements.) Now $t_{S}=14 \ln [(4+5) / 5]=8.23 \mathrm{~ns}$. Lowering $I_{F}$ from 10 mA to 4 mA reduces the amount of stored charge, and raising $-I_{R}$ from 2 mA to 5 mA wipes out the stored charge more rapidly. However, because of the logarithmic dependence, the reduction in $t_{S}$ is not that dramatic.

### Schottky-Barrier Diodes

Schottky-barrier diodes (SBDs) overcome the charge-storage limitation of pn junctions by avoiding minority charges altogether. The two diode types are compared in Fig. 6.70. A conventional monolithic diode, shown in Fig. 6.70a, consists of a $p-n^{-}$ junction and corresponding metal electrodes, for instance made of aluminum (Al). Consider now the Al- $n^{-}$junction of Fig. 6.70b. Because of the lightly doped $n^{-}$region (typically $N_{D} \leq 10^{-16} / \mathrm{cm}^{3}$ ), a space-charge layer (SCL) with rectifying properties forms just below the Al electrode. Applying a positive bias to the Al electrode
image_name:(a)
description:The image depicts two types of diode structures, labeled as (a) and (b).

1. **Identification of Components and Structure:**
- **(a) Ordinary pn diode structure:**
- The diagram shows a conventional pn diode consisting of a p-n junction.
- The structure includes a p-type region and an n-type region (n^-) within a semiconductor material.
- Metal electrodes labeled as "Anode" and "Cathode" are placed on top of the p and n+ regions, respectively.
- The p region is adjacent to the n- region, forming the p-n junction.
- **(b) Schottky barrier diode (SBD) structure:**
- This diagram illustrates a Schottky barrier diode with an n^- region.
- It features metal electrodes labeled as "Anode" and "Cathode" on top of the n^- and n+ regions.
- The structure lacks a p-type region, indicating the Schottky junction is formed between the metal and the n^- semiconductor material.

2. **Connections and Interactions:**
- **(a) pn Diode:**
- Current flows from the anode to the cathode when forward-biased, through the p-n junction.
- The flow of charge carriers involves both electrons and holes.
- **(b) Schottky Diode:**
- Current flows from the anode to the cathode through the Schottky barrier when forward-biased.
- Conduction is primarily through electrons, as there is no p-type region.

3. **Labels, Annotations, and Key Features:**
- Both diagrams include labels for the anode and cathode, indicating the direction of current flow.
- The pn diode symbol and Schottky diode symbol are shown next to their respective structures, providing a visual representation of each diode type.
- The n^- region is marked in both diagrams, highlighting the lightly doped nature of this region, which is crucial for the rectifying properties of the diodes.
image_name:(b)
description:The image consists of two diagrams labeled (a) and (b), each depicting a different type of diode structure.

1. **Diagram (a) - Ordinary pn Diode Structure:**
- **Components and Structure:** The diagram shows a cross-section of a conventional pn diode. It consists of a p-type region and an n-type region, with a junction between them. The n-region is further divided into an n⁻ layer, indicating a lightly doped region, and an n⁺ layer, indicating a heavily doped region near the cathode.
- **Connections and Interactions:** An anode and a cathode are positioned on top of the p and n⁺ regions, respectively. The anode and cathode are typically connected to external circuits, allowing current to flow through the diode when forward-biased.
- **Labels, Annotations, and Key Features:** The diagram includes labels for the anode and cathode, and a diode symbol is shown to represent the electrical behavior of the structure.

2. **Diagram (b) - Schottky Barrier Diode (SBD) Structure:**
- **Components and Structure:** This diagram illustrates a Schottky barrier diode. It features an n⁻ region, which is a lightly doped semiconductor, and an n⁺ region. The anode is placed directly on the n⁻ region, forming a metal-semiconductor junction, while the cathode is on the n⁺ region.
- **Connections and Interactions:** The Schottky barrier is formed at the interface between the metal anode and the n⁻ semiconductor, allowing electron flow when forward-biased. The absence of a p-type region distinguishes this from the pn diode.
- **Labels, Annotations, and Key Features:** The diagram is labeled with anode and cathode, and includes a diode symbol specific to Schottky diodes, indicating its rectifying properties. The absence of minority-charge storage is a key feature of this type of diode.

FIGURE 6.70 (a) Ordinary pn diode structure, and (b) Schottky barrier diode (SBD) structure.
relative to the $n^{-}$region will overcome the ensuing electrostatic barrier and cause electrons to flow from the $n^{-}$region, through the SCL, to the Al electrode. Since conduction is exclusively via electrons, which are the (only) charge carriers in the Al metal and are the majority carriers in the $n^{-}$material, there is no minority-charge storage in SBDs (aptly enough, SBDs are also called hot-carrier diodes because of this.) However, the SBD exhibits a junction capacitance $C_{j}$ just like the conventional $p n$ diode, indicating similar behavior during turn-on from $t_{0}$ to $t_{1}$ as well as during turnoff past $t_{3}$. But, in the $\operatorname{SBD}$ case $t_{3}$ coincides with $t_{2}$ because $t_{S}=0$.

SBDs exhibit an exponential $i-v$ characteristic just like ordinary $p n$ diodes, except that the saturation current $I_{s}$ of a SBD is some 5 orders of magnitude higher than that of a $p n$ diode of comparable dimensions. Using the $60-\mathrm{mV} /$ decade rule, we conclude that SBDs have typically $V_{D(\text { on })} \cong 0.7-5 \times 0.06=0.4 \mathrm{~V}$. The advantages of (a) a lower voltage drop and (b) the absence of minority-charge storage effects makes SBDs preferable to $p n$ diodes in applications such as switching power supplies and high-speed diode circuits. Figure $6.70 b$ shows also the circuit symbol in common use for the SBD.

Before concluding, we observe that both structures of Fig. 6.70 include an Al- $n^{+}$ junction at the cathode side. This junction too results in the formation of an SCL below the cathode electrode; however, because of heavy doping, this SCL is so narrow that electrons can easily tunnel across it in either direction to form what is known as an ohmic contact. Were the $n^{+}$region absent, the "cathode" electrode would form another SBD with the $n^{-}$material underneath, resulting in a back-to-back diode pair that would serve no useful purpose. As we know, ohmic contacts play an important role in connection with the collector of bipolar transistors as well as the tubs of CMOS transistors.

## 6.11 BJT SWITCHING TRANSIENTS

The analysis of BJT transients draws heavily from the diode treatment of the previous section, except that the BJT comprises two junctions and the analysis is therefore more complex. When used as a switch, a BJT usually alternates between the cutoff (CO) and saturation (Sat) modes, with brief transitions through the forward-active mode. In saturation both junctions are forward biased, so this mode is a combination
of forward-active (FA) and reverse-active (RA) operation. The transient behavior of the npn BJT is governed by the charge-control equations ${ }^{1,8}$

$$
\begin{gather*}
i_{B}=\frac{Q_{F}}{\tau_{B F}}+\frac{Q_{R}}{\tau_{B R}}+\frac{d}{d t}\left(Q_{F}+Q_{R}+Q_{j e}+Q_{j c}\right)  \tag{6.122}\\
i_{C}=\frac{Q_{F}}{\tau_{F}}-Q_{R}\left(\frac{1}{\tau_{R}}+\frac{1}{\tau_{B R}}\right)-\frac{d}{d t}\left(Q_{R}+Q_{j c}\right) \tag{6.123}
\end{gather*}
$$

where $i_{B}$ and $i_{C}$ are the currents into the base and into the collector terminals; $Q_{F}$ and $Q_{R}$ are the FA and RA excess minority-carrier charges in the base; $Q_{j e}$ and $Q_{j c}$ are the charges of the base-emitter (BE) and base-collector (BC) capacitances $C_{j e}$ and $C_{j c}\left(=C_{\mu}\right.$ in ac analysis). The time constants $\tau_{F}$ and $\tau_{B F}$ are called, respectively, the mean transit time and the mean lifetime of the base minority carriers in FA operation. According to Eq. (6.4) the npn BJT has

$$
\begin{equation*}
\tau_{F}=\frac{W_{B}^{2}}{2 D_{n}} \tag{6.124}
\end{equation*}
$$

where $W_{B}$ is the base width and $D_{n}$ is the electron diffusivity. The two time constants are related as ${ }^{1}$

$$
\begin{equation*}
\tau_{B F}=\beta_{F} \tau_{F} \tag{6.125}
\end{equation*}
$$

where $\beta_{F}$ is the familiar FA current gain. Similar terminology holds for the time constants $\tau_{R}$ and $\tau_{B R}\left(=\beta_{R} \tau_{R}\right)$, except that they pertain to RA operation, where the current gain is $\beta_{R}\left(\ll \beta_{F}\right)$. Equation (6.122) describes the effect of $i_{B}$ on the various charges, whereas Eq. (6.123) describes the effect of these charges on $i_{C}$, indicating a relationship of cause-and-effect between the two currents. Also, once we know $i_{B}$ and $i_{C}$, we can find the emitter current via KVL as $i_{E}=i_{B}+i_{E}$.

However intimidating the above equations might appear, we shall use them in simple and intuitive ways to investigate the response of a basic BJT inverter/switch to an input pulse. To this end we use the PSpice circuit of Fig. 6.71 to display all
image_name:FIGURE 6.71
description:
[
name: VS, type: VoltageSource, value: VS, ports: {Np: VS, Nn: GND}
name: RB, type: Resistor, value: 10kΩ, ports: {N1: VS, N2: VB}
name: RC, type: Resistor, value: 1kΩ, ports: {N1: VCC, N2: VC}
name: Q, type: NPN, ports: {C: VC, B: VB, E: GND}
]
extrainfo:The circuit is a BJT inverter/switch with a voltage source VS, a base resistor RB of 10kΩ, and a collector resistor RC of 1kΩ. The transistor Q is an NPN type connected with the collector at VC, base at VB, and emitter at GND. VCC is at +5V, and the input voltage VS switches from -2V to 5V.

FIGURE 6.71 PSpice circuit to visualize the switching transients of a BJT inverter/switch.
relevant waveforms for the case of a BJT inverter with the parameters shown in the table, and then we apply the above equations to calculate ${ }^{8}$ the various transient components. As shown in Fig. 6.72, the driving source $v_{S}$ is switched from $V_{R}(=-2 \mathrm{~V})$ to $V_{F}(=5 \mathrm{~V})$ at $t=t_{0}=0 \mathrm{~ns}$ and back to -2 V at $t=t_{3}=100 \mathrm{~ns}$. Assuming the BJT is in steady state prior to $t=t_{0}$, we identify the following operating regions and corresponding time intervals.

- Cutoff Region $\left(t_{0}\right.$ to $\left.t_{1}\right)$ : right after the leading edge of $v_{S}$ there are no base excess charges $Q_{F}$ and $Q_{R}$ yet, so Eqs. (6.122) and (6.123) simplify as

$$
\begin{equation*}
i_{B}=\frac{d}{d t}\left(Q_{j e}+Q_{j c}\right) \quad i_{C}=-\frac{d Q_{j c}}{d t} \tag{6.126}
\end{equation*}
$$

The first equation states that $i_{B}$ merely goes toward charging up the capacitances $C_{j e}$ and $C_{j c}$, and the second that the portion of $i_{B}$ flowing through $C_{j c}$ exits (hence the "-" sign in the second tem above) the collector terminal. This current then flows into $R_{C}$ to produce the initial voltage bump visible in the plot of $v_{C}$. As $C_{j e}$ and $C_{j c}$ charge up, $v_{B}$ rises until the BJT reaches the edge of conduction (EOC) at the instant $t_{1}$ when $v_{B} \cong 0.6 \mathrm{~V}$. As we know, the junction capacitances are

$$
\begin{equation*}
C_{j e}=\frac{C_{j e 0}}{\left(1-v_{B E} / \phi_{e}\right)^{m_{e}}} \quad C_{j c}=\frac{C_{j c 0}}{\left(1-v_{B C} / \phi_{c}\right)^{m_{c}}} \tag{6.127}
\end{equation*}
$$

where $C_{j e 0}$ and $C_{j c 0}$ are their zero-bias values, $\phi_{e}$ and $\phi_{c}$ are the built-in potentials of the two junctions, and $m_{e}$ and $m_{c}$ are their grading coefficients. Following the diode treatment of the previous section we estimate the charging time $t_{1}-t_{0}\left(=t_{1}\right)$ by approximating the first of Eq. (6.126) as

$$
i_{B(\mathrm{avg})} \cong \frac{\Delta Q_{j e}+\Delta Q_{j c}}{\Delta t}=\frac{C_{j e(\mathrm{eq})} \Delta v_{B E}+C_{j c(\mathrm{eq})} \Delta v_{B C}}{t_{1}-t_{0}}
$$

where $i_{B(\text { avg })}$ is the average of $i_{B}\left(t_{0}^{+}\right)=[5-(-2)] / 10=0.7 \mathrm{~mA}$ and $i_{B}\left(t_{1}\right)=$ $(5-0.6) / 10=0.44 \mathrm{~mA}$, that is, $i_{B(\text { avg })}=(0.7+0.44) / 2=0.57 \mathrm{~mA}$; moreover, $\Delta v_{B E}=v_{B E}\left(t_{1}\right)-v_{B E}\left(t_{0}\right)=0.6-(-2)=2.6 \mathrm{~V}=\Delta v_{B C}$. Making the crude approximations $C_{j e(\mathrm{eq})} \cong C_{j e 0}=1 \mathrm{pF}$ and $C_{j c(\mathrm{eq})} \cong C_{j e 0} / 2=0.5 / 2=$ 0.25 pF (see Problem 6.53 for better estimates) we get $t_{1}=(1+0.5 / 2) \times$ $10^{-12} \times 2.6 /\left(0.57 \times 10^{-3}\right)=5.7 \mathrm{~ns}$, in fair agreement with the value $t_{1}=5.2 \mathrm{~ns}$ measured via the cursor facility of PSpice.

- Active Region $\left(t_{1}\right.$ to $\left.t_{2}\right)$ : following $t_{1}$, the BJT is brought from the EOC ( $\left.v_{B} \cong 0.6 \mathrm{~V}\right)$ to full conduction ( $v_{B} \cong 0.7 \mathrm{~V}$ ). During this time $Q_{R}$ is still zero, but $Q_{F}$ builds up, causing $i_{C}$ to rise and thus $v_{C}$ to drop. At the instant $t_{2}$ when $v_{C}$ drops to $v_{C}=V_{C E(\mathrm{OSS})} \cong 0.2 \mathrm{~V}$ the BJT reaches the edge of saturation (EOS). During this time interval Eq. (6.122) simplifies as

$$
\begin{equation*}
i_{B}=\frac{Q_{F}}{\tau_{B F}}+\frac{d}{d t}\left(Q_{F}+Q_{j e}+Q_{j c}\right) \tag{6.128}
\end{equation*}
$$

image_name:V_F
description:The graph titled "V_F" consists of multiple subplots illustrating various waveforms relevant to a BJT inverter/switch. The x-axis for all plots represents time in nanoseconds (ns), ranging from 0 to 150 ns.

1. **Input Voltage ($v_S$) Plot:**
- **Type:** Time-domain waveform.
- **Y-Axis:** Input voltage $v_S$ in volts (V), ranging from -2 V to 5 V.
- **Behavior:** The waveform shows a step function. It starts at 5 V, drops to 0 V at around 100 ns, and remains constant thereafter.
- **Key Features:** The transition from high to low voltage is sharp and occurs at the 100 ns mark.

2. **Base Voltage ($v_B$) Plot:**
- **Type:** Time-domain waveform.
- **Y-Axis:** Base voltage $v_B$ in volts (V), ranging from -2 V to 5 V.
- **Behavior:** Initially, the voltage rises sharply to about 5 V, indicating the end of conduction (EOC) at around 10 ns. It remains constant until approximately 120 ns, where it decreases gradually back to -2 V.
- **Key Features:** The EOC is marked at both the rise and fall of the voltage, with a notable interval $t_S$ between these points.

3. **Base Current ($i_B$) Plot:**
- **Type:** Time-domain waveform.
- **Y-Axis:** Base current $i_B$ in microamperes (µA), ranging from -400 µA to 800 µA.
- **Behavior:** The current spikes positively to about 400 µA and remains constant until around 100 ns, where it drops and then gradually increases again after 120 ns.
- **Key Features:** The constant region is labeled $I_{BF}$, while the increase after 120 ns is labeled $I_{BR}$.

4. **Collector Voltage ($v_C$) Plot:**
- **Type:** Time-domain waveform.
- **Y-Axis:** Collector voltage $v_C$ in volts (V), ranging from 0 V to 6 V.
- **Behavior:** The voltage decreases sharply from 6 V to near 0 V between $t_0$ and $t_2$, reaching the edge of saturation (EOS). It stays low until around 100 ns, then rises sharply back to 6 V by $t_5$.
- **Key Features:** Notable points include changeover (CO), end of conduction (EOC), forward active (FA), and saturation (Sat) phases.

5. **Overdrive Charge ($Q_S$) Plot:**
- **Type:** Time-domain waveform.
- **Y-Axis:** Overdrive charge $Q_S$ in picocoulombs (pC), ranging from -6 pC to 6 pC.
- **Behavior:** The charge increases from 0 pC, peaks at around 2 pC, and then decreases after 100 ns.
- **Key Features:** The curve is smooth with a peak indicating maximum overdrive charge, followed by a decline after 120 ns.
image_name:v_B
description:The graph titled "v_B" is a time-domain waveform plot, showing the base voltage (v_B) of a BJT inverter/switch over time. The x-axis represents time in nanoseconds (ns), ranging from 0 to 150 ns. The y-axis represents base voltage in volts (V), with values ranging from -2 V to 5 V.

Overall Behavior and Trends:
- **Initial Rise:** The base voltage v_B starts at approximately -2 V and quickly rises to about 0.7 V within the first few nanoseconds, indicating the transition from cutoff to conduction.
- **Stable Region:** After the initial rise, v_B remains constant at around 0.7 V, indicating the transistor is in full conduction. This stable region persists from around 10 ns to just over 100 ns.
- **Drop:** After about 110 ns, v_B starts to decrease, indicating the transition from conduction to cutoff. The voltage drops back to approximately -2 V by the end of the observed time period.

Key Features and Technical Details:
- **EOC (End of Conduction):** Marked at both the beginning and end of the stable region, indicating the points where the base voltage stabilizes and then begins to drop.
- **t_S (Storage Time):** The time interval during which v_B remains constant at its conduction level, approximately from 10 ns to 110 ns.

Annotations and Specific Data Points:
- **Markers:** Annotations such as "EOC" indicate critical points where the behavior of v_B changes significantly.
- **Numerical Values:** The key voltage levels are approximately -2 V (cutoff) and 0.7 V (conduction). The transition times are around 10 ns for the rise and 110 ns for the fall.
image_name:i_B
description:The graph titled "i_B" represents the base current waveform of a BJT inverter/switch circuit, as part of a series of plots related to the circuit's operation.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph depicting the base current, \(i_B\), over time.

2. **Axes Labels and Units:**
- The x-axis represents time in nanoseconds (ns), ranging from 0 to 150 ns.
- The y-axis represents the base current, \(i_B\), in microamperes (µA), with a scale from -400 µA to 800 µA.

3. **Overall Behavior and Trends:**
- The waveform shows an initial spike in the base current at the start, reaching a peak slightly above 400 µA.
- Following the spike, \(i_B\) stabilizes at a constant level, denoted as \(I_{BF}\), until around 100 ns.
- After 100 ns, the base current decreases to a lower constant level, labeled \(I_{BR}\), and begins to rise slightly towards the end of the time interval.

4. **Key Features and Technical Details:**
- The initial peak indicates the charging phase of the BJT, where the base current is required to drive the transistor into saturation.
- The steady state at \(I_{BF}\) suggests the transistor is in a stable conduction phase.
- The transition to \(I_{BR}\) corresponds to a change in the circuit operation, possibly indicating the beginning of the transistor's cutoff phase.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for \(I_{BF}\) and \(I_{BR}\), marking the constant current levels during different phases of operation.
- The transition points, particularly around 100 ns, are critical as they mark the shift from one operational state to another.
image_name:v_C
description:The graph titled "Collector voltage v_C" is a time-domain waveform illustrating the behavior of the collector voltage, \( v_C \), in a BJT inverter/switch circuit. The x-axis represents time in nanoseconds, ranging from 0 to 150 ns, while the y-axis represents voltage in volts, ranging from 0 to 6 V.

Overall Behavior and Trends:
- **Initial State (t_0 to t_1):** The collector voltage starts at approximately 5.8 V at \( t_0 \) and remains relatively constant until \( t_1 \), indicating the cutoff region.
- **Transition to Saturation (t_1 to t_2):** At \( t_1 \), the voltage begins to decrease sharply, reaching approximately 0.2 V at \( t_2 \), marking the edge of saturation (EOS).
- **Saturation Region (t_2 to t_3):** From \( t_2 \) to \( t_3 \), the voltage remains low and stable, indicating saturation.
- **Transition from Saturation (t_3 to t_4):** At \( t_3 \), the voltage begins to rise sharply back to around 5.8 V by \( t_4 \), as the BJT exits saturation.
- **Final State (t_4 to t_5):** The voltage stabilizes again at the initial level, indicating the return to cutoff.

Key Features and Technical Details:
- **Critical Points:**
- \( t_0 \) and \( t_5 \): Initial and final states with \( v_C \) at approximately 5.8 V.
- \( t_2 \) and \( t_3 \): Mark the beginning and end of saturation with \( v_C \) around 0.2 V.
- **Edge of Saturation (EOS):** Clearly marked at \( t_2 \) and \( t_3 \), where the voltage is at its minimum.
- **Cutoff (CO) and Forward Active (FA) Regions:** Indicated by the transitions at \( t_1 \) and \( t_4 \).

Annotations and Specific Data Points:
- The graph includes annotations such as CO (Cutoff), EOC (End of Cutoff), FA (Forward Active), and EOS (Edge of Saturation).
- The transitions between these regions are marked by significant changes in voltage, providing insight into the BJT's switching behavior.

This waveform effectively demonstrates the dynamic response of the BJT as it switches between different operating regions, highlighting the key phases of cutoff, saturation, and the transitions between them.
image_name:Q_S
description:The graph titled "Q_S" is part of a series of plots depicting the behavior of a BJT inverter/switch over time. This graph specifically focuses on the overdrive charge $Q_S$ as a function of time, measured in nanoseconds (ns).

Type of Graph and Function:
- This is a time-domain waveform graph illustrating the overdrive charge $Q_S$ in picocoulombs (pC) over time.

Axes Labels and Units:
- **X-axis:** Time (ns), ranging from 0 to 150 ns.
- **Y-axis:** Overdrive charge $Q_S$ (pC), ranging from -4 to 6 pC.

Overall Behavior and Trends:
- The graph begins with $Q_S$ at 0 pC at time $t_0$.
- There is a rapid increase in $Q_S$, reaching approximately 3 pC around 30 ns.
- After this initial rise, $Q_S$ gradually increases and stabilizes around 4 pC during the saturation period.
- At approximately 120 ns, there is a sharp decrease in $Q_S$, dropping back toward 0 pC by 150 ns.

Key Features and Technical Details:
- **Initial Rise:** The overdrive charge $Q_S$ increases quickly from 0 to around 3 pC within the first 30 ns, indicating the transition from cutoff to saturation.
- **Stabilization:** The charge stabilizes around 4 pC, indicating the BJT is in a saturated state.
- **Sharp Decrease:** At around 120 ns, $Q_S$ sharply decreases, corresponding to the transition out of saturation back towards cutoff.

Annotations and Specific Data Points:
- **Key Points:** $t_0$, $t_2$, $t_3$, and $t_5$ are marked, with significant changes in charge occurring at these times.
- **Reference Lines:** There is a dotted line indicating the extrapolated behavior of $Q_S$ beyond the observed data.

This graph provides insight into the dynamic behavior of the BJT's overdrive charge during switching operations, highlighting the transitions between cutoff, saturation, and back to cutoff states.

FIGURE 6.72 Plot of all relevant waveforms for the BJT inverter/switch of Fig. 6.71.

We estimate the time interval $t_{2}-t_{1}$ by approximating the above expression as

$$
\begin{align*}
i_{B(\mathrm{avg})} & \cong \frac{Q_{F(\mathrm{avg})}}{\tau_{B F}}+\frac{\Delta Q_{F}+\Delta Q_{j e}+\Delta Q_{j c}}{\Delta t} \\
& =\frac{Q_{F(\mathrm{avg})}}{\tau_{B F}}+\frac{\Delta Q_{F}+C_{j e(\mathrm{eq})} \Delta v_{B E}+C_{j c(\mathrm{eq})} \Delta v_{B C}}{t_{2}-t_{1}} \tag{6.129}
\end{align*}
$$

where $i_{B \text { (avg) }}$ is the average of $i_{B}\left(t_{1}\right)=440 \mu \mathrm{~A}$ and $i_{B}\left(t_{2}\right)=(5-0.7) / 10=430 \mu \mathrm{~A}$, that is, $i_{B \text { (avg) }}=435 \mu \mathrm{~A}$. Moreover, $\Delta v_{B E}=v_{B E}\left(t_{2}\right)-v_{B E}\left(t_{1}\right)=0.7-0.6=$ $0.1 \mathrm{~V}, \Delta v_{B C}=v_{B C}\left(t_{2}\right)-v_{B C}\left(t_{1}\right)=(0.7-0.2)-(0.6-5)=4.9 \mathrm{~V}, \Delta Q_{F}=Q_{F}\left(t_{2}\right)-$ $Q_{F}\left(t_{1}\right)=\tau_{F} i_{C}\left(t_{2}\right)-0=0.2 \times 10^{-9} \times(5-0.2) / 10^{3}=0.96 \mathrm{pC}$, so $Q_{F(\text { avg })}=$ $(0+0.96) / 2=0.48 \mathrm{pC}$. Using the crude approximations $C_{j e} \cong 2 C_{j e 0}=2 \mathrm{pF}$ and $C_{j c} \cong C_{j c 0}=0.5 \mathrm{pF}$ we get

$$
435 \times 10^{-6}=\frac{0.48 \times 10^{-12}}{50 \times 0.2 \times 10^{-9}}+\frac{(0.96+2 \times 0.1+0.5 \times 4.9) 10^{-12}}{t_{2}-t_{1}}
$$

Solving gives $t_{2}-t_{1}=9.3 \mathrm{~ns}$, in fair agreement with the value of 7.8 ns measured with the cursor.

- Saturation Region $\left(t_{2}\right.$ to $\left.t_{3}\right)$ : past $t_{2}$ the BJT enters deep saturation, where both junctions are forward biased and therefore both $Q_{F}$ and $Q_{R}$ are different from zero. Since $v_{B E}$ and $v_{B C}$ remain fairly constant in this region, $C_{j e}$ and $C_{j c}$ play an insignificant role now, so we can simplify Eq. (6.122) as

$$
\begin{equation*}
I_{B F}=\frac{Q_{F}}{\tau_{B F}}+\frac{Q_{R}}{\tau_{B R}}+\frac{d}{d t}\left(Q_{F}+Q_{R}\right) \tag{6.130}
\end{equation*}
$$

where

$$
\begin{equation*}
I_{B F}=\frac{V_{F}-V_{B E \text { (sat) }}}{R_{B}} \cong \frac{5-0.8}{10}=420 \mu \mathrm{~A} \tag{6.131}
\end{equation*}
$$

The total excess base charge in saturation is $Q_{B}=Q_{F}+Q_{R}$ (see Fig. 6.73b). Rewriting as

$$
\begin{equation*}
Q_{B}=Q_{F(\mathrm{EOS})}+Q_{S} \tag{6.132}
\end{equation*}
$$

suggests that we can regard $Q_{B}$ as the sum of the charge $Q_{F(\text { EOS })}$ needed to bring the BJT to the EOS (see Fig. 6.73a), and the charge $Q_{S}$ arising as the BJT is driven deeply into saturation proper (see Fig. 6.73c). We can likewise express $I_{B F}$ as

$$
I_{B F}=I_{B(\mathrm{EOS})}+I_{B S}
$$

where

$$
\begin{equation*}
I_{B(\mathrm{EOS})}=\frac{I_{C(\mathrm{EOS})}}{\beta_{F}}=\frac{\left(V_{C C}-V_{C E(\mathrm{EOS})}\right) / R_{C}}{\beta_{F}} \cong \frac{(5-0.2) / 1}{50}=96 \mu \mathrm{~A} \tag{6.133}
\end{equation*}
$$

is the base current needed to bring the BJT to the EOS, and

$$
I_{B S}=I_{B F}-I_{B(\mathrm{EOS})}=420-96=324 \mu \mathrm{~A}
$$

image_name:(a)
description:The image consists of three diagrams labeled (a), (b), and (c), each representing the distribution of excess minority charges in the base of a BJT (Bipolar Junction Transistor) at different operating conditions.

**Diagram (a):**
- This diagram shows a triangular region labeled \(Q_{F(\text{EOS})}\) at the bottom, indicating the excess minority charge at the edge of saturation (EOS). The diagram is divided into three vertical sections labeled E, B, and C, corresponding to the emitter, base, and collector of the BJT. The region \(Q_{F(\text{EOS})}\) is shaded at the bottom, suggesting that this is the charge present when the BJT is at the edge of saturation.

**Diagram (b):**
- This diagram is more complex, showing three distinct regions labeled \(Q_F\), \(Q_B\), and \(Q_R\). The \(Q_F\) region is shaded light gray, the \(Q_B\) region is white, and the \(Q_R\) region is dark gray. This configuration illustrates the distribution of excess minority charges when the BJT is in a state with more complex charge interactions, possibly representing different levels of saturation or charge accumulation.

**Diagram (c):**
- Similar to diagram (a), this diagram shows two regions labeled \(Q_{F(\text{EOS})}\) and \(Q_S\). The \(Q_{F(\text{EOS})}\) region is shaded light gray and situated above the \(Q_S\) region, which is dark gray. This diagram likely represents the deep saturation state, where \(Q_S\) indicates the overdrive base charge that builds up, as mentioned in the context. The arrangement suggests a larger accumulation of charge compared to the EOS state shown in diagram (a).

Overall, these diagrams visually represent how excess minority charges are distributed in a BJT's base under different saturation and charge conditions, aligning with the theoretical explanation provided in the context about base current and charge control.
image_name:(b)
description:The image labeled as "(b)" is a diagram illustrating excess minority charges in the base of a BJT (Bipolar Junction Transistor) during deep saturation. The diagram is divided into three regions labeled as E (Emitter), B (Base), and C (Collector). It shows three distinct areas representing different charge components:

1. **Q_F**: This area is shaded in light gray and represents the forward excess charge in the base region.
2. **Q_B**: This area is unshaded and represents the base charge.
3. **Q_R**: This area is shaded in dark gray and represents the reverse excess charge.

The diagram visually demonstrates how these charges are distributed in the base region when the transistor is in deep saturation, with the forward and reverse charges contributing to the overall charge dynamics in the BJT.
image_name:(c)
description:Figure 6.73 consists of three diagrams labeled (a), (b), and (c), illustrating the distribution of excess minority charges in the base of a BJT (Bipolar Junction Transistor) under different conditions.

- **Diagram (a):** Shows the transistor at the edge of saturation (EOS). The base region is depicted with a triangular area labeled \(Q_{F(\text{EOS})}\), representing the minority charge at EOS. This area is shaded in a darker tone.

- **Diagram (b):** Illustrates the transistor in a state of saturation. The base region is divided into three sections: \(Q_F\), \(Q_B\), and \(Q_R\). \(Q_F\) is shaded in a lighter tone, \(Q_R\) is shaded in a darker tone, and \(Q_B\) is unshaded, showing the distribution of minority charges within the base.

- **Diagram (c):** Represents the transistor in deep saturation. The base region is divided into two main areas: \(Q_{F(\text{EOS})}\) and \(Q_S\). \(Q_{F(\text{EOS})}\) is shaded in a lighter tone, while \(Q_S\), representing the overdrive base charge, occupies a larger area and is shaded in a darker tone. This diagram emphasizes the buildup of excess minority charge due to the overdrive base current \(I_{B_S}\).

FIGURE 6.73 Excess minority charges in the base: (a) at the EOS, and (b), (c) in deep saturation.
is the amount of base current above $I_{B(\operatorname{EOS})}$ that drives the BJT in deep saturation (note that the BJT is indeed saturated because $\beta_{s a t}=4.9 / 0.42=11.7 \ll \beta_{F}$ ). Aptly called the overdrive base current, $I_{B S}$ causes the overdrive base charge $Q_{S}$ to build up according to the charge-control equation ${ }^{8}$

$$
\begin{equation*}
I_{B S}=\frac{Q_{S}}{\tau_{S}}+\frac{d Q_{S}}{d t} \tag{6.134}
\end{equation*}
$$

where the time constant $\tau_{S}$ is a linear combination ${ }^{8}$ of $\tau_{B F}$ and $\tau_{B R}$,

$$
\begin{equation*}
\tau_{S}=\frac{\left(\beta_{R}+1\right) \tau_{B F}+\beta_{F} \tau_{B R}}{\beta_{F}+\beta_{R}+1} \tag{6.135}
\end{equation*}
$$

Using the data tabulated in Fig. 6.71 we get $\tau_{S}=[(2+1) 50 \times 0.2+50 \times$ $2 \times 10] /(50+2+1)=19.4$ ns. The solution to Eq. (6.134) is an exponential buildup of $Q_{S}$, governed by the time constant $\tau_{S}$ and tending asymptotically toward the steady-state value

$$
Q_{S(\mathrm{ss})}=\tau_{S} I_{B S}=19.4 \times 10^{-9} \times 324 \times 10^{-6}=6.3 \mathrm{pC}
$$

- Storage Time $\left(t_{3}\right.$ to $\left.t_{4}\right)$ : once $v_{S}$ is switched back to -2 V at $t=t_{3}=100 \mathrm{~ns}$, we need to remove the overdrive charge $Q_{S}$ if we want to bring the BJT back to the EOS. The removal of $Q_{S}$ is still governed by Eq. (6.134) provided we now use

$$
\begin{aligned}
I_{B S} & =I_{B R}-I_{B(\mathrm{EOS})}=\frac{V_{R}-V_{B E(\mathrm{sat})}}{R_{B}}-I_{B(\mathrm{EOS})}=\frac{-2-0.7}{10 \times 10^{3}}-(96 \mu \mathrm{~A}) \\
& =-270-96=-366 \mu \mathrm{~A}
\end{aligned}
$$

(Cognizant of the small step decrease in $v_{B}$, which is $\Delta v_{B}=r_{b} \Delta I_{B}$, we are now assuming $V_{B E(\text { sat })} \cong 0.7 \mathrm{~V}$ instead of the usual 0.8 V .) Since $I_{B S}$ is now negative, the solution to Eq. (6.134) is an exponential decay in $Q_{S}$, still governed by the time constant $\tau_{S}$ but tending asymptotically toward the (fictitious) steady-state value

$$
Q_{S}(\infty)=\tau_{S} I_{B S}=19.4 \times 10^{-9} \times\left(-366 \times 10^{-6}\right)=-7.1 \mathrm{pC}
$$

The decay holds up to the instant $t_{4}$ at which $Q_{S}$ becomes zero. The time interval $t_{S}=t_{4}-t_{3}$, aptly called the storage time, is readily found as ${ }^{7}$

$$
t_{S}=\tau_{S} \ln \frac{Q_{S}\left(t_{3}\right)-Q_{S}(\infty)}{Q_{S}\left(t_{4}\right)-Q_{S}(\infty)}=\tau_{S} \ln \frac{\tau_{S}\left(I_{B F}-I_{B(\mathrm{EO})}\right)-\tau_{S}\left(I_{B R}-I_{B(\mathrm{EOS})}\right)}{0-\tau_{S}\left(I_{B R}-I_{B(\mathrm{EOS})}\right)}
$$

that is,

$$
\begin{equation*}
t_{S}=\tau_{S} \ln \frac{I_{B F}-I_{B R}}{I_{B(\mathrm{EOS})}-I_{B R}} \tag{6.136}
\end{equation*}
$$

Presently we get $t_{s}=(19.4 \mathrm{~ns}) \ln [(420+270) /(96+270)]=12.3 \mathrm{~ns}$, which matches PSpice exactly.

- Active Region Again $\left(t_{4}\right.$ to $\left.t_{5}\right)$ : after removing $Q_{S}$ to bring the BJT back to the EOS, we need to remove $Q_{F}$ to bring it back to the edge of conduction, now more properly called the edge of cutoff (EOC). The removal of $Q_{F}$ is still governed by Eq. (6.128), but with $i_{B}=\left(V_{R}-V_{B E}\right) / R_{B}$. Using $i_{B(\text { avg })}=(-2-0.65) / 10=$ $-265 \mu \mathrm{~A}$, we suitably recycle Eq. (6.129) to write

$$
-265 \times 10^{-6}=\frac{0.48 \times 10^{-12}}{50 \times 0.2 \times 10^{-9}}-\frac{(0.96+2 \times 0.1+0.5 \times 4.9) 10^{-12}}{t_{5}-t_{4}}
$$

Solving gives $t_{5}-t_{4}=11.5 \mathrm{~ns}$, in fair agreement with the PSpice value of 9.2 ns .

- Recovery Region $\left(t>t_{5}\right)$ : once all the excess base charge has been wiped out, the BJT goes through a recovery phase to return $C_{j e}$ and $C_{j c}$ to the steady-state conditions preceding $t_{0}$. During this phase $v_{B}$ makes a pseudo exponential transistion from $v_{B}=V_{B E(\mathrm{EOC})} \cong 0.6 \mathrm{~V}$ to $v_{B}=V_{R}=-2 \mathrm{~V}$, as shown.
It is apparent that a BJT inverter/switch takes time to turn on and off. In particular, during turn-off, the BE junction continues to remain on from $t_{3}$ to $t_{5}$, during which time it acts as a $0.7-\mathrm{V}$ battery. Of special significance is the storage time $t_{s}$ from $t_{3}$ to $t_{4}$, during which the BJT remains saturated. This is usually a serious drawback, especially in high-speed logic or in power-switch applications.

### Schottky-Clamped BJTs

We can eliminate the storage time $t_{S}$ altogether by placing a Schottky barrier diode (SBD) in parallel with the base-collector (BC) junction, as shown in Fig. $6.74 a$ for the case of the $n p n$ BJT. Recall that the saturation current of a SBD is typically five orders of magnitude higher than that of an ordinary $p n$ junction, indicating that the forward voltage drop across a SBD is lower than that across a pn junction by about $5 \times(60 \mathrm{mV})=0.3 \mathrm{~V}$, giving $V_{S B D(\text { on })} \cong 0.7-0.3 \cong 0.4 \mathrm{~V}$ typical. Because of the SBD clamp, the BC junction is subject to the constraint $v_{B C} \leq 0.4 \mathrm{~V}$, which is insufficient to allow the BC junction to turn convincingly on. Hence, the BJT will always have $Q_{R}=0$ and, as such, it will never saturate.

Shown in Fig. $11.4 b$ is the monolithic realization of a Schottky-clamped npn BJT. Comparing with the structure of Fig. 2.1, we observe that all it takes to Schottkyclamp the BJT is to extend the metal electrode of the base over the $n^{-}$collector
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: C, B: B, E: E}
name: D1, type: Diode, ports: {Na: B, Nc: C}
]
extrainfo:The diagram shows a Schottky-clamped npn BJT with a diode connected between the base and collector. This configuration prevents the transistor from saturating by clamping the base-collector voltage.
image_name:(b)
description:The image in Fig. 11.4 (b) illustrates the monolithic realization of a Schottky-clamped npn Bipolar Junction Transistor (BJT). This diagram is divided into two parts: the circuit symbol representation and the cross-sectional view of the physical structure.

1. **Identification of Components and Structure:**
- **Circuit Symbol (Left Side):** The left side of the diagram shows the circuit symbol for a Schottky-clamped BJT. It includes a conventional npn transistor symbol with an additional Schottky Barrier Diode (SBD) connected between the base (B) and collector (C) terminals.
- **Physical Structure (Right Side):** The right side of the diagram presents a cross-sectional view of the BJT structure. This view includes:
- **E (Emitter):** The emitter region is marked at the top, connected to the n+ region.
- **B (Base):** The base is indicated in the middle, connected to the p-type region.
- **C (Collector):** The collector is on the right side, also connected to an n+ region.
- **n+ and n- regions:** These regions are shown as part of the epitaxial layer and buried layer, with the n+ regions forming ohmic contacts and the n- epitaxial layer providing the main transistor body.
- **SBD (Schottky Barrier Diode):** The SBD is highlighted, formed by extending the metal electrode of the base over the n- collector region.

2. **Connections and Interactions:**
- The diagram shows that the Schottky diode is integrated into the BJT structure by extending the base metal over the n- collector, allowing the SBD to clamp the base-collector junction. This prevents the BJT from entering saturation by limiting the base-collector voltage to approximately 0.4 V.
- The n+ buried layer ensures good electrical conductivity and reduces collector resistance.

3. **Labels, Annotations, and Key Features:**
- The diagram includes labels for the emitter (E), base (B), and collector (C) terminals.
- The SBD is explicitly labeled, indicating its role in the transistor's operation.
- The material regions are annotated with n+, n-, and p, showing the doping types and their roles in the transistor's structure.

Overall, the image provides a detailed view of both the symbolic representation and the physical implementation of a Schottky-clamped npn BJT, highlighting the integration of the Schottky diode to prevent saturation.

FIGURE 6.74 (a) Schottky-clamped BJT and its circuit symbol. (a) Planar process fabrication.
region, where it forms the SBD. (Also shown at the right is the metal- $n^{+}$structure, which provides an ohmic contact between the metal electrode of the collector and the $n^{-}$epitaxial layer underneath.)
(a) Assuming the BJT of Fig. 6.71 is equipped with a SBD clamp having $V_{S B D(\text { (n) })} \cong 0.4 \mathrm{~V}$, find the steady-state currents $I_{B}, I_{C}$, and $I_{S B D}$ when $v_{S}=V_{F}=5 \mathrm{~V}$, and comment on your findings.
(b) Rerun the PSpice circuit of Fig. 6.71, but using a SBD. Comment on your findings.

#### Solution

(a) The current through $R_{B}$ is $I\left(R_{B}\right)=\left(V_{F}-V_{B}\right) / R_{B} \cong(5-0.7) / 10=0.43 \mathrm{~mA}$. By KVL, $V_{C}=V_{B}-V_{S B D(\text { on })} \cong 0.7-0.4=0.3 \mathrm{~V}$, so the current through $R_{C}$ is $I\left(R_{C}\right)=\left(V_{C C}-V_{C}\right) / R_{C} \cong(5-0.3) / 1=4.7 \mathrm{~mA}$. Moreover, the BJT is operating in the FA region because $V_{C E} \cong 0.3 \mathrm{~V}$, which is $0.1-\mathrm{V}$ higher than $V_{C E(\mathrm{BOS})}(\cong 0.2 \mathrm{~V})$. Consequently, we can write $I_{C}=\beta_{F} I_{B}=50 I_{B}$. We need two more equations to solve for the three unknowns. These are provided by KCL at the base and at the collector nodes, where $I_{B}=I\left(R_{B}\right)-I_{S B D}=0.43-I_{S B D}$, and $I_{C}=I\left(R_{C}\right)+I_{S B D}=4.73+I_{S B D}$. Solving, we get

$$
I_{B}=100.6 \mu \mathrm{~A} \quad I_{C}=5.03 \mathrm{~mA} \quad I_{S B D}=0.33 \mathrm{~mA}
$$

Because of the SBD, only enough current is allowed into the base to keep the BJT about $0.1-\mathrm{V}$ away from the EOS. The overdrive current is diverted by the SBD to the collector, thus preventing the BJT from ever saturating.
(b) The clamped BJT of Fig. $6.75 a$ uses a SBD with the following PSpice model:

```
.model DSBD D(IS=1nA CJO=0.25pF VJ=1.6V M=0.4 EG=0.7)
```

The waveforms of Fig. $6.75 b$ confirm the elimination of the storage time. The rise and fall times of $v_{C}$ are a bit longer than those of the unclamped circuit of Fig. 6.71 because of the SBD's junction capacitance $C_{j}$, which is in parallel with $C_{j c}$. Moreover, $v_{C}$ is clamped at about 0.3 V , a bit higher than the 0.1 V of the circuit of Fig. 6.71.
image_name:(a)
description:
[
name: V_CC, type: VoltageSource, value: +5V, ports: {Np: VCC, Nn: GND}
name: R_C, type: Resistor, value: 1kΩ, ports: {N1: VCC, N2: VC}
name: R_B, type: Resistor, value: 10kΩ, ports: {N1: VS, N2: X1}
name: Q, type: NPN, ports: {C: VC, B: X1, E: GND}
name: SBD, type: Diode, ports: {Na: X1, Nc: VC}
]
extrainfo:The circuit is a Schottky-clamped BJT inverter/switch. The Schottky Barrier Diode (SBD) is used to clamp the collector voltage and eliminate storage time, improving switching speed. The circuit operates with a supply voltage V_CC of +5V, and the output voltage v_C is clamped at about 0.3V.
image_name:(b)
description:The diagram (b) in the image illustrates the time-domain waveforms for a Schottky-clamped BJT inverter/switch circuit. The graph is composed of two plots: the input voltage vs. time and the collector voltage vs. time.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform showing the input and output voltages of a Schottky-clamped BJT circuit.

2. **Axes Labels and Units:**
- The horizontal axis represents time in nanoseconds (ns), ranging from 0 to 150 ns.
- The vertical axis of the top plot represents the input voltage \( v_S \) in volts (V), ranging from -2 V to 5 V.
- The vertical axis of the bottom plot represents the collector voltage \( v_C \) in volts (V), ranging from 0 V to 6 V.

3. **Overall Behavior and Trends:**
- The input voltage \( v_S \) is a square wave that transitions from 0 V to 5 V at around 10 ns and returns to 0 V at around 110 ns.
- The collector voltage \( v_C \) shows a delayed response to the input changes and exhibits a clamping behavior due to the Schottky diode.
- The waveform for \( v_C \) with the Schottky barrier diode (SBD) shows a faster transition compared to the unclamped case, particularly noticeable during the fall time.

4. **Key Features and Technical Details:**
- The collector voltage \( v_C \) initially starts at approximately 5 V and drops to around 0.3 V when \( v_S \) transitions high. This is due to the SBD clamping effect.
- The rise and fall times of \( v_C \) are slightly longer than the unclamped circuit, attributed to the junction capacitance \( C_j \) of the SBD.
- The waveform labeled "With SBD" shows a distinct clamping at approximately 0.3 V, confirming the elimination of storage time.

5. **Annotations and Specific Data Points:**
- The graph includes an annotation indicating the presence of the SBD, highlighting the differences in the collector voltage response.
- The voltage clamping at \( v_C \) around 0.3 V is a crucial feature, slightly higher than the 0.1 V clamping in the circuit without the SBD.

FIGURE 6.75 (a) Schottky-clamped BJT inverter/switch, and (b) input and output waveforms.

## 6.12 TRANSIENT RESPONSE OF CMOS GATES AND VOLTAGE COMPARATORS

In binary-output circuits such as logic gates and voltage comparators it is of interest to know how rapidly the output changes state in response to a sudden change at the input. It takes time for the stray capacitances of the transistors and their interconnections to charge/discharge in response to an input step. As a rule, the smaller the capacitances and the higher the currents available to charge/discharge them, the faster the response.

### Propagation Delays in Logic Gates

The dynamics of a logic gate are characterized via the propagation delays, usually specified for the case of an inverter (the most basic representative of a logic family) driving $n$ similar inverters, or for a fanout of $n$ in logic-design jargon (see Fig. 6.76). A propagation delay is the amount of time it takes for the output to accomplish 50\% of its transition from one output level to the other following an input-step edge. Denoting the output levels as $V_{O L}$ and $V_{O H}$, we define the $50 \%$-point as

$$
\begin{equation*}
V_{50 \%}=\frac{V_{O L}+V_{O H}}{2} \tag{6.137}
\end{equation*}
$$

image_name:(a)
description:
[
name: vI, type: VoltageSource, value: vI, ports: {Np: VI, Nn: GND}
name: I0, type: Inverter, ports: {In: VI, Out: VO}
name: I1, type: Inverter, ports: {In: VO, Out: OUT1}
name: I2, type: Inverter, ports: {In: VO, Out: OUT2}
name: In, type: Inverter, ports: {In: VO, Out: OUTn}
]
extrainfo:The circuit diagram represents an inverter I0 driving n similar inverters (I1, I2, ..., In), illustrating a fanout of n. The propagation delays tPHL and tPLH are shown in the timing diagram, indicating the time it takes for vO to transition to 50% of its final value.
image_name:(b)
description:The graph in Figure 6.76 (b) is a time-domain waveform illustrating the propagation delay characteristics of a logic inverter with a fanout of \( n \). This graph focuses on the output voltage \( v_O \) behavior over time as it transitions between two states.

Type of Graph and Function:
This is a time-domain waveform graph showing the voltage transition of a logic inverter's output.

Axes Labels and Units:
- **Horizontal Axis (x-axis):** Represents time \( t \). The units are not specified but typically would be in nanoseconds (ns) for such applications.
- **Vertical Axis (y-axis):** Represents voltage levels, \( v_I \) and \( v_O \), with no specific units indicated but typically in volts (V).

Overall Behavior and Trends:
The graph shows two distinct transitions:
1. A falling edge where the output voltage \( v_O \) drops from the high output voltage \( V_{OH} \) to the midpoint \( V_{50\%} \), marking the propagation delay \( t_{PHL} \).
2. A rising edge where \( v_O \) increases from the low output voltage \( V_{OL} \) to \( V_{50\%} \), marking the propagation delay \( t_{PLH} \).

Key Features and Technical Details:
- **\( V_{OH} \):** High output voltage level.
- **\( V_{OL} \):** Low output voltage level.
- **\( V_{50\%} \):** Midpoint voltage level, calculated as \( \frac{V_{OL} + V_{OH}}{2} \).
- **\( t_{PHL} \):** The time it takes for \( v_O \) to fall from \( V_{OH} \) to \( V_{50\%} \).
- **\( t_{PLH} \):** The time it takes for \( v_O \) to rise from \( V_{OL} \) to \( V_{50\%} \).

Annotations and Specific Data Points:
- The graph includes horizontal reference lines for \( V_{OH} \), \( V_{OL} \), and \( V_{50\%} \).
- Vertical lines indicate the time intervals for \( t_{PHL} \) and \( t_{PLH} \).
- The waveform has a characteristic shape indicating the non-linear nature of the transition, likely due to the inherent dissymmetries in the circuit's internal structure.

This graph is essential for understanding the timing characteristics of the inverter and how it affects the overall performance of digital circuits, especially when driving multiple similar inverters (fanout).

FIGURE 6.76 (a) Logic inverter $I_{0}$ with a fanout of $n$. (b) The propagation delays $t_{P H L}$ and $t_{P L H}$.

The time it takes for $v_{O}$ to rise from $V_{O L}$ to $V_{50 \%}$ is denoted as $t_{P L H}$, and the time it takes to drop from $V_{O H}$ to $V_{50 \%}$ is denoted as $t_{P H L}$. (Because of inherent internal circuit dissymmetries, $t_{P L H}$ and $t_{P H L}$ are not necessarily identical.) In the following we investigate the propagation delays of CMOS gates, presently the predominant digital technology. These gates have $V_{O L}=0$ and $V_{O H}=V_{D D}$, so $V_{50 \%}=V_{D D} / 2$. As circuit complexity increases, transient analysis by paper and pencil can easily become prohibitive, so we shall find the propagation delays via PSpice, and then use simplified hand analysis to obtain approximate estimates, both as a check on PSpice and as a means to gain insight into the inner workings of the gate.

### Transient Analysis of CMOS Gates via PSpice

In order to display the transient response, PSpice calculates all parasitic capacitances in the gate, so we need to provide PSpice with suitable process and device parameters. To this end, refer to the conceptual rendition of Fig. 6.77, which is similar to the basic structure of Fig. 6.8, except for an additional detail hitherto omitted for simplicity; these are the $p^{+}$channel-stop implants surrounding the $n^{+}$source and drain regions on three sides other than that facing the channel. The function of these implants is to electrically isolate adjacent FETs sharing the same bulk. (The portion of the bulk between the source/drain regions of two adjacent FETs forms a spurious channel that might become accidentally conductive. The $p^{+}$implants are designed to greatly increase the $V_{t}$ of these spurious channels and thus prevent them from accidentally turning on. Typically, the doping of the $p^{+}$implants is an order of magnitude higher than that of the $p^{-}$bulk, or $N_{\text {implant }} \cong 10 N_{\text {bulk }}$.) Because of the channel stops, each of the junction capacitances $C_{s b}$ and $C_{d b}$ consists of a bottom component $C_{j(\mathrm{btm})}$ associated with the $p^{-}-n^{+}$junction at the bottom of the source and drain region, and a sidewall component $C_{j(\mathrm{sw})}$ associated with the $p^{+}-n^{+}$junction around the region's perimeter. The net junction capacitance of the drain region is expressed as

$$
\begin{equation*}
C_{d b}=\frac{A_{d} \times C_{\mathrm{j} 0(\mathrm{btm})}}{\left(1-v_{B D} / \phi_{0(\mathrm{btm})}\right)^{m_{\mathrm{bm}}}}+\frac{P_{d} \times C_{j 0(\mathrm{sw})}}{\left(1-v_{B D} / \phi_{0(\mathrm{sw})}\right)^{m_{\mathrm{sw}}}} \tag{6.138}
\end{equation*}
$$

image_name:FIGURE 6.77
description:The image labeled "FIGURE 6.77" is a detailed diagram of an nMOSFET, showcasing both top and cross-sectional views. The illustration highlights the structural and electrical components of the device, focusing on the source, drain, and gate regions.

1. **Identification of Components and Structure:**
- **Source and Drain Regions:** These are depicted as rectangular areas on either side of the central gate region. They are surrounded by $p^{+}$ channel-stop implants on three sides, which are shaded darker to differentiate them from the rest of the structure.
- **Gate Region:** Positioned centrally, the gate is shown with an overlay labeled with a width $W$ and length $L$. The gate is responsible for controlling the current flow between the source and drain.
- **Substrate:** The $p^{-}$ substrate forms the base of the structure, supporting the source, drain, and gate regions.

2. **Connections and Interactions:**
- **Capacitances:** The diagram includes various capacitances such as $C_{ov}$ (overlap capacitance), $C_{gb}$ (gate-body capacitance), $C_{js(btm)}$ (source bottom junction capacitance), $C_{jd(btm)}$ (drain bottom junction capacitance), and $C_{j(sw)}$ (sidewall junction capacitance).
- **Junctions and Extensions:** The source and drain regions have $n^{+}$ type extensions into the substrate, with junction depths labeled as $X_j$.
- **Dimensions:** The diagram specifies several critical dimensions, including $L_{drawn}$ (drawn length of the gate), $L_{ov}$ (overlap length), $Y_s$ (source extension length), and $Y_d$ (drain extension length).

3. **Labels, Annotations, and Key Features:**
- **Annotations:** The diagram is annotated with symbols and labels indicating various capacitances and dimensions, essential for understanding the electrical characteristics of the nMOSFET.
- **Material Types:** The $p^{+}$ and $n^{+}$ regions are clearly marked, indicating the doping types and their roles in the device's operation.
- **Body Contact:** The body contact is shown at the bottom of the substrate, labeled as "Body," indicating the electrical grounding or connection point for the substrate.

Overall, the diagram provides a comprehensive view of the nMOSFET structure, detailing the physical layout and the associated electrical parameters, crucial for understanding its operation and design considerations.

FIGURE 6.77 Conceptual views (top as well as cross sectional) of an nMOSFET. Note the $p^{+}$channel-stop implants surrounding the source and drain regions on the three sides other than the side facing the channel.
where

- $A_{d}$ is the area of the drain's bottom junction and $C_{j 0(\mathrm{bm})}$ is the zero-bias junction capacitance per unit area. Moreover, $\phi_{0(b \mathrm{bm})}$ is the bottom-junction built-in potential and $m_{\mathrm{btm}}$ is the grading coefficient.
- $P_{d}$ is the perimeter of the drain's sidewall junction, $C_{j 0(\mathrm{sw})}$ is the zero-bias junction capacitance per unit perimeter, $\phi_{0(\mathrm{sw})}$ is the sidewall-junction built-in potential, and $m_{\mathrm{sw}}$ is the grading coefficient.

For the geometry depicted at the top of Fig. 6.77 we have $A_{d}=Y_{d} \times W$ and $P_{d}=$ $2 Y_{d}+W$. Moreover, adapting Eq. (1.47b) to the present case, and simplifying owing
to the fact that $N_{A \text { (bulk) }} \ll N_{D(\text { drain })}$ and $N_{A(\text { implant })} \ll N_{D(\text { drain }),}$ we have

$$
\begin{equation*}
C_{j 0(\mathrm{btm})} \cong \sqrt{\frac{\varepsilon_{s i} q N_{A(\mathrm{bulk})}}{2 \phi_{0(\mathrm{bum})}}} \quad C_{j 0(\mathrm{sw})} \cong X_{j} \sqrt{\frac{\varepsilon_{s i} q N_{A(\mathrm{mpllat})}}{2 \phi_{0(\mathrm{sw})}}} \tag{6.139}
\end{equation*}
$$

where $X_{j}$ is the depth of the drain region, also shown in the figure. The process parameters of Eq. (6.139) apply also to the source region, the only possible differences being in its area $A_{s}$ and perimeter $P_{s}$, depending on device layout geometry. The above expressions are readily adapted to the case of the $p$ MOSFET, as the following example illustrates.
(a) Assuming an $n$ MOSFET with the process parameters $t_{o x}=20 \mathrm{~nm}, \mu_{n}=$

#### EXAMPLE 6.26

$600 \mathrm{~cm}^{2} / \mathrm{Vs}, V_{t}=0.7 \mathrm{~V}, \lambda^{\prime}=0.1 \mu \mathrm{~m} / \mathrm{V}, L_{o v}=0.15 \mu \mathrm{~m}, X_{j}=0.25 \mu \mathrm{~m}$, $N_{D \text { (poly) }}=10^{20} \mathrm{~cm}^{-3}, N_{A \text { (bulk) }}=3 \times 10^{15} \mathrm{~cm}^{-3}, N_{A \text { (implant) }}=10 N_{A \text { (bulk) }}, m_{\text {btm }}=0.5$, and $m_{\text {sw }}=0.33$, find its process-related capacitances. Hence, find $A_{d}, P_{d}, A_{s}$, and $P_{s}$ if $L_{\text {drawn }}=1.0 \mu \mathrm{~m}, W=2.0 \mu \mathrm{~m}$, and $Y_{d}=Y_{s}=2.5 \mu \mathrm{~m}$.
(b) Assuming a $p$ MOSFET with the process parameters $t_{o x}=20 \mathrm{~nm}, \mu_{p}=$ $250 \mathrm{~cm}^{2} / \mathrm{Vs}, V_{t}=-0.7 \mathrm{~V}, \lambda^{\prime}=0.05 \mu \mathrm{~m} / \mathrm{V}, L_{o v}=0.2 \mu \mathrm{~m}, X_{j}=0.3 \mu \mathrm{~m}$, $N_{\text {A(poly) }}=10^{20} \mathrm{~cm}^{-3}, N_{D \text { (bulk) }}=1.8 \times 10^{16} \mathrm{~cm}^{-3}, N_{D(\text { implant })}=10 N_{D(\text { bulk })}, m_{\text {btm }}=0.5$, and $m_{\mathrm{sw}}=0.33$, find its process-related capacitances. Hence, find $A_{d}, P_{d}, A_{s}$, and $P_{s}$ if $L_{\text {drawn }}=1.0 \mu \mathrm{~m}, W=4.0 \mu \mathrm{~m}$, and $Y_{d}=Y_{s}=3.0 \mu \mathrm{~m}$.

#### Solution

(a) For the $n$ MOSFET we have

$$
\begin{aligned}
& C_{o x}=\frac{\varepsilon_{o x}}{t_{o x}}=\frac{34.5}{20}=1.725 \frac{\mathrm{fF}}{\mu \mathrm{~m}^{2}} \\
& C_{o v}=C_{o x} L_{o v}=1.725 \times 0.15=0.259 \frac{\mathrm{fF}}{\mu \mathrm{~m}}=0.259 \frac{\mathrm{nF}}{\mathrm{~m}} \\
& \phi_{0(\mathrm{btm})}=V_{T} \ln \frac{N_{A(\text { bulk })} N_{D \text { (poly })}^{2}}{n_{i}^{2}}=0.026 \ln \frac{3 \times 10^{15} \times 10^{20}}{2 \times 10^{20}}=0.909 \mathrm{~V} \\
& \phi_{0(\text { sw })}=V_{T} \ln \frac{N_{A \text { (implant }} N_{D(\text { poly })}}{n_{i}^{2}}=0.026 \ln \frac{30 \times 10^{15} \times 10^{20}}{2 \times 10^{20}}=0.968 \mathrm{~V} \\
& C_{j 0(\text { thm })} \cong \sqrt{\frac{1.04 \times 10^{-12} \times 1.602 \times 10^{-19} \times 3 \times 10^{15}}{2 \times 0.909}}=16.6 \frac{\mathrm{nF}}{\mathrm{~cm}^{2}} \\
& =0.166 \frac{\mathrm{fF}}{\mu \mathrm{~m}^{2}}=166 \frac{\mu \mathrm{~F}}{\mathrm{~m}^{2}} \\
& C_{j 0(\mathrm{sw})} \cong\left(0.25 \times 10^{-4}\right) \sqrt{\frac{1.04 \times 10^{-12} \times 1.602 \times 10^{-19} \times 30 \times 10^{15}}{2 \times 0.968}} \\
& =12.7 \frac{\mathrm{nF}}{\mathrm{~cm}}=0.127 \frac{\mathrm{fF}}{\mu \mathrm{~m}}=0.127 \frac{\mathrm{nF}}{\mathrm{~m}}
\end{aligned}
$$

Finally, $A_{s}=A_{d}=Y_{d} \times W=2.5 \times 2=5 \mu \mathrm{~m}^{2}=5 \times 10^{-12} \mathrm{~m}^{2}$, and $P_{s}=P_{d}=$ $2 Y_{d}+W=2 \times 2.5+2=7 \mu \mathrm{~m}$.
(b) For the $p$ MOSFET we likewise find

$$
\begin{aligned}
C_{o x} & =1.725 \frac{\mathrm{fF}}{\mu \mathrm{~m}^{2}} \quad C_{o v}=1.725 \times 0.2=0.345 \frac{\mathrm{fF}}{\mu \mathrm{~m}}=0.345 \frac{\mathrm{nF}}{\mathrm{~m}} \\
\phi_{0(\mathrm{btm})} & =V_{T} \ln \frac{N_{D(\text { bulk })} N_{A(\text { poly })}}{n_{i}^{2}}=0.026 \ln \frac{1.8 \times 10^{16} \times 10^{20}}{2 \times 10^{20}}=0.955 \mathrm{~V} \\
\phi_{0(\mathrm{sw})} & =V_{T} \ln \frac{N_{D(\text { implant })} N_{A(\text { poly })}}{n_{i}^{2}}=0.026 \ln \frac{18 \times 10^{16} \times 10^{20}}{2 \times 10^{20}}=1.01 \mathrm{~V} \\
C_{j 0(\mathrm{btm})} & \cong \sqrt{\frac{1.04 \times 10^{-12} \times 1.602 \times 10^{-19} \times 1.8 \times 10^{16}}{2 \times 0.955}} \\
& =39.6 \frac{\mathrm{nF}}{\mathrm{~cm}^{2}}=0.396 \frac{\mathrm{fF}}{\mu \mathrm{~m}^{2}}=396 \frac{\mu \mathrm{~F}}{\mathrm{~m}^{2}} \\
C_{j 0(\mathrm{ss})} & \cong\left(0.3 \times 10^{-4}\right) \sqrt{\frac{1.04 \times 10^{-12} \times 1.602 \times 10^{-19} \times 18 \times 10^{16}}{2 \times 1.01}} \\
& =36.6 \frac{\mathrm{nF}}{\mathrm{~cm}}=0.366 \frac{\mathrm{fF}}{\mu \mathrm{~m}}=0.366 \frac{\mathrm{nF}}{\mathrm{~m}}
\end{aligned}
$$

Finally, $A_{s}=A_{d}=Y_{d} \times W=3 \times 4=12 \mu \mathrm{~m}^{2}=12 \times 10^{-12} \mathrm{~m}^{2}$, and $P_{s}=$ $P_{d}=2 Y_{d}+W=2 \times 3+4=10 \mu \mathrm{~m}$.

We are now ready to input the above data to PSpice for the transient analysis of a CMOS inverter based on the above MOSFETs and using $V_{D D}=3.3 \mathrm{~V}$. The circuit, shown in Fig. 6.78, has been created by recycling that of Fig. 3.65, and then by suitably editing the FET models and the circuit's netlist. The example shown is for a fanout of 1 , but it can easily be adapted to a higher fanout. The circuit includes also the wire capacitance $C_{w}$ to model the parasitic capacitance of the interconnections.

Following the instructions of Appendix 3A, we create the PSpice models as follows:

```
.model Mn NMOS(Level=1 Tox=20n Uo=600 Vto=0.7 Lambda=0.1
+ Ld=0.15u Gamma=0.18 phi=0.64 Cj=166u Mj=0.5 Cjsw=0.127n
+ Mjsw=0.33 Pb=0.909 Cgso=0.259n Cgdo=0.259n)
.model Mp PMOS(Level=1 Tox=20n Uo=250 Vto=-0.7 Lambda=0.05
+ Ld=0.2u Gamma=0.42 phi=0.73 Cj=396u Mj=0.5 Cjsw=0.366n
+ Mjsw=0.33 Pb=0.955 Cgso=0.345n Cgdo=0.345n)
```

A few remarks are in order. First, note that the dimensions are V, A, m, and s, with the exception of mobilities, which must be expressed in $\mathrm{cm}^{2} / \mathrm{Vs}$ (also, doping densities, when specified, must be expressed in atoms/cm ${ }^{3}$ ). In PSpice the zero-bias bottom and sidewall capacitances are denoted as Cj and Cj sw, and both use the same built-in potential Pb . Moreover, the unit-length overlap capacitances associated with the source
image_name:FIGURE 6.78
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: V0, G: VI}
name: M2, type: NMOS, ports: {S: GND, D: V0, G: VI}
name: M3, type: PMOS, ports: {S: VDD, D: VX, G: V0}
name: M4, type: NMOS, ports: {S: GND, D: VX, G: V0}
name: V_DD, type: VoltageSource, value: +3.3V, ports: {Np: VDD, Nn: GND}
name: V_I, type: VoltageSource, ports: {Np: VI, Nn: GND}
name: C_w, type: Capacitor, value: 5fF, ports: {Np: V0, Nn: Vb}
name: C_x, type: Capacitor, value: 5fF, ports: {Np: VX, Nn: GND}
]
extrainfo:The circuit is a CMOS inverter with a fanout of 1. It uses PMOS and NMOS transistors to invert the input signal VI and drive the output nodes V0 and VX. The capacitors C_w and C_x are used for load and coupling.

FIGURE 6.78 PSpice circuit to display the transient response of CMOS inverter $I_{0}$ with a fanout of 1 .
and drain are denoted as Cgso and Cgdo. PSpice calculates automatically the parasitic capacitances of each FET in accordance with its instantaneous region of operation.

Once the process parameters have been entered in the model statements, we need to enter the device parameters in the netlist. To this end, use PSpice $\rightarrow$ Create Netlist to direct PSpice to generate the netlist, and then use PSpice $\rightarrow$ View Netlist to visualize it. The result is

```
* source CKT_of_Fig_6.78
V_VDD VDD 0 3.3Vdc
C_Cw 0 VO 5fF
C_Cx 0 VX 5fF
M_M1 VO IN VDD VDD Mp
M_M2 VO IN O O Mn
M_M3 VX VO VDD VDD Mp
M_M4 VX VO O O Mn
V_VI IN 0 PULSE 0 3.3V 100ps 0.1ps 0.1ps 400ps 1ns
```

Next, type in the individual transistor dimensions $L, W, A_{s}, P_{s}, A_{d}$, and $P_{d}$ as follows:

```
* source CKT_of_Fig_6.78
V_VDD VDD 0 3.3Vdc
C_Cw O VO 5fF
C_Cx O VX 5fF
M_M1 VO IN VDD VDD Mp L=1u W=4u As=12p Ps=10u Ad=12p
+ Pd=10u
M_M2 VO IN 0 0 Mn L=1u W=2u As=5p Ps=7u Ad=5p
+ Pd=7u
M_M3 VX VO VDD VDD Mp L=1u W=4u As=12p Ps=10u Ad=12p
+ Pd=10u
M_M4 VX VO O 0 Mn L=1u W=2u As=5p Ps=7u Ad=5p
+ Pd=7u
V_VI IN 0 PULSE 0 3.3V 100ps 0.1ps 0.1ps 400ps 1ns
```

image_name:FIGURE 6.79 Waveforms for the PSpice circuit of Fig. 6.78
description:The graph is a time-domain waveform plot that shows the input and output voltages of a CMOS circuit over time. It consists of three separate plots, each displaying a different signal.

1. **First Plot (Input vI):**
- **Type:** Step waveform.
- **Axes:**
- X-axis: Time (ps), ranging from 0 to 700 ps.
- Y-axis: Input voltage vI (V), ranging from 0 to 4 V.
- **Behavior:** The plot shows a step input that rises sharply from 0 V to 3.3 V at 0 ps and remains constant until 400 ps, where it drops back to 0 V.

2. **Second Plot (Output vO):**
- **Type:** Transient response.
- **Axes:**
- X-axis: Time (ps), ranging from 0 to 700 ps.
- Y-axis: Output voltage vO (V), ranging from -1 to 4 V.
- **Behavior:** The output voltage initially mirrors the input and remains at approximately 3.3 V. After 0 ps, it starts to decrease, reaching a minimum around 400 ps. It then increases again, reaching close to 3.3 V by 700 ps.

3. **Third Plot (Output vX):**
- **Type:** Transient response.
- **Axes:**
- X-axis: Time (ps), ranging from 0 to 700 ps.
- Y-axis: Output voltage vX (V), ranging from -1 to 4 V.
- **Behavior:** The output voltage vX starts at 0 V and gradually increases, reaching a peak slightly above 3 V. It then decreases, showing a dip before stabilizing around 2 V by 700 ps.

**Key Features:**
- The input waveform is a pulse with sharp rising and falling edges at 0 ps and 400 ps, respectively.
- The output voltage vO shows a delay and a gradual transition compared to the input, indicative of the gate's propagation delay.
- The output voltage vX shows a more complex transient behavior, with an overshoot and undershoot before stabilizing.

**Annotations:**
- The delays measured are approximately 39.6 ps for the high-to-low transition (tPHL) and 43.3 ps for the low-to-high transition (tPLH). These values are indicative of the CMOS gate's switching characteristics.

FIGURE 6.79 Waveforms for the PSpice circuit of Fig. 6.78.

Finally, use File $\rightarrow$ Save to save it, and PSpice $\rightarrow$ Run to launch PSpice. This gives the waveforms of Fig. 6.79. Using the cursor facility we measure the delays and find $t_{P H L} \cong 39.6 \mathrm{ps}$ and $t_{P L H} \cong 43.3 \mathrm{ps}$.

### Hand Calculation of CMOS Gate Delays

No matter how powerful the computational tools at hand, a scrupulous engineer will always try to anticipate/check the results of simulation via hand calculations, even if the latter may provide only gross approximations. Shown in Fig. 6.80 are all parasitic capacitances for the case of a CMOS inverter with a fanout of 1. To facilitate hand analysis we lump all stray capacitances into a single equivalent capacitance $C_{e q}$ at the output node of the driving inverter $I_{0}$. Using inspection, we express the net capacitance between node $v_{o}$ and ground as

$$
\begin{equation*}
C_{e q}=C_{0}+C_{w}+C_{1} \tag{6.140}
\end{equation*}
$$

image_name:FIGURE 6.80
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: V1, G: VI}
name: M2, type: NMOS, ports: {S: GND, D: V1, G: VI}
name: M3, type: PMOS, ports: {S: VDD, D: VX, G: V1}
name: M4, type: NMOS, ports: {S: GND, D: VX, G: V1}
name: v1, type: VoltageSource, value: v1, ports: {Np: V1, Nn: GND}
name: I0, type: OpAmp, value: I0, ports: {InP: V1, InN: GND, OutP: VO}
name: C_gsp, type: Capacitor, value: C_gsp, ports: {Np: VDD, Nn: V1}
name: C_gdp, type: Capacitor, value: C_gdp, ports: {Np: V1, Nn: V1}
name: C_gdn, type: Capacitor, value: C_gdn, ports: {Np: V1, Nn: GND}
name: C_gsn, type: Capacitor, value: C_gsn, ports: {Np: V1, Nn: GND}
name: C_dbp, type: Capacitor, value: C_dbp, ports: {Np: V1, Nn: V1}
name: C_dbn, type: Capacitor, value: C_dbn, ports: {Np: V1, Nn: GND}
name: C0, type: Capacitor, value: C0, ports: {Np: V1, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: V1, Nn: GND}
name: C_w, type: Capacitor, value: C_w, ports: {Np: V1, Nn: GND}
name: C_x, type: Capacitor, value: C_x, ports: {Np: VX, Nn: GND}
name: C_eq, type: Capacitor, value: C_eq, ports: {Np: VO, Nn: GND}
]
extrainfo:The circuit diagram illustrates a CMOS inverter with parasitic capacitances. It includes PMOS and NMOS transistors forming two inverters, each having stray capacitances. The equivalent capacitance Ceq is used to simplify analysis, representing all stray capacitances at the output of the driving inverter I0. The diagram also shows how a capacitive load is driven by the inverter.
image_name:Capacitorless
description:
[
'name': 'Vi', 'type': 'VoltageSource', 'value': 'Vi', 'ports': {'Np': 'VI', 'Nn': 'GND'
'name': 'I_0', 'type': 'OpAmp', 'value': 'I_0', 'ports': {'InP': 'VI', 'InN': 'GND', 'Out': 'VO'
'name': 'C_eq', 'type': 'Capacitor', 'value': 'C_eq', 'ports': {'Np': 'VO', 'Nn': 'GND'
]
extrainfo:The circuit diagram represents a CMOS inverter with parasitic capacitances and a fanout of 1. It includes two stages of PMOS and NMOS transistors (M1, M2 and M3, M4) with associated parasitic capacitors. The output is simplified to an equivalent capacitance C_eq driven by an op-amp I_0.

FIGURE 6.80 Showing all stray capacitances for a CMOS inverter with a fanout of 1 . To simplify hand calculations, $I_{0}$ can be regarded as a parasitics-free inverter driving a suitable equivalent capacitance $C_{e q}$.
where:

- $C_{0}$ is the equivalent capacitance seen looking into the output terminal of the inverter $I_{0}$ made up of $M_{1}$ and $M_{2}$. We have

$$
\begin{equation*}
C_{0}=C_{d b n}+C_{d b p}+2\left(C_{g d n}+C_{g d p}\right) \tag{6.141}
\end{equation*}
$$

with the factor of 2 stemming from the Miller effect (as $v_{I}$ changes from 0 to $V_{D D}$, $v_{O}$ changes from $V_{D D}$ to 0 , subjecting each of $C_{g d n}$ and $C_{g d p}$ to a voltage change of $2 V_{D D}$, in effect doubling both capacitances). Note that $C_{g s n}$ and $C_{g s p}$ are not connected to node $v_{o}$, so they do not contribute to $C_{0}$ (they only load down the input source $v_{I}$ ).

- $C_{w}$ is the capacitance of the wire interconnecting the two inverters ( $C_{w}$ increases with the fanout.)
- $C_{1}$ is the equivalent capacitance seen looking into the input terminal of the load inverter made up of $M_{3}$ and $M_{4}$. According to Fig. 6.79, the output $v_{X}$ of this inverter doesn't change significantly during $I_{0}$ 's $t_{P L H}$ or $t_{P H L}$, so we can ignore $C_{d b n}$ and $C_{d b p}$ and approximate $C_{1} \cong C_{g s n}+C_{g d n}+C_{g s p}+C_{g d n}$. Regardless of how the gate-channel capacitance splits between source and drain, we simply have

$$
\begin{equation*}
C_{1} \cong C_{o x}\left(W_{n} \times L_{n(\text { drawn })}+W_{p} \times L_{p(\text { drawn })}\right) \tag{6.142}
\end{equation*}
$$

where $L_{n(\text { drawn })}$ and $L_{p(\text { drawn })}$ are the drawn channel lengths, as depicted in Fig. 6.77.

EXAMPLE 6.27 Calculate all relevant stray capacitances in the CMOS inverter of Example 6.26.

#### Solution

Using the data of Example 6.26 we get

$$
\begin{aligned}
& C_{d b n}=\frac{C_{j 0(\mathrm{btm})} A_{d n}}{\left(1-v_{B D} / \phi_{0(\mathrm{btm})}\right)^{m_{\mathrm{bum}}}}+\frac{C_{j 0(\mathrm{sw})} P_{d n}}{\left(1-v_{B D} / \phi_{0(\mathrm{btm})}\right)^{m_{\mathrm{mim}}}} \\
& =\frac{0.166 \times 5}{\left(1+v_{o} / 0.909\right)^{0.5}}+\frac{0.127 \times 7}{\left(1+v_{o} / 0.968\right)^{0.33}} \\
& C_{d b p}=\frac{C_{j 0(\mathrm{btm})} A_{d n}}{\left(1-v_{D B} / \phi_{0(\mathrm{bmm})}\right)^{m_{\mathrm{dum}}}}+\frac{C_{j 0(\mathrm{sw})} P_{d n}}{\left(1-v_{D B} / \phi_{0(\mathrm{btm})}\right)^{m_{\mathrm{sw}}}} \\
& =\frac{0.396 \times 12}{\left[1+\left(3.3-v_{o}\right) / 0.909\right]^{0.5}}+\frac{0.366 \times 10}{\left[1+\left(3.3-v_{o}\right) / 0.968\right]^{0.33}}
\end{aligned}
$$

that is,

$$
\begin{aligned}
C_{d b n} & =\frac{0.83 \mathrm{fF}}{\left(1+v_{o} / 0.909\right)^{0.5}}+\frac{0.89 \mathrm{fF}}{\left(1+v_{o} / 0.968\right)^{0.33}} \\
C_{d b p} & =\frac{4.75 \mathrm{fF}}{\left(4.63-v_{O} / 0.909\right)^{0.5}}+\frac{3.66 \mathrm{fF}}{\left(4.41-v_{o} / 0.968\right)^{0.33}}
\end{aligned}
$$

Moreover,

$$
\begin{aligned}
2\left(C_{g d n}+C_{g d p}\right) & =2\left(C_{o v n} \times W_{n}+C_{o v p} \times W_{p}\right)=2(0.259 \times 2+0.345 \times 4) \\
& =3.80 \mathrm{fF}
\end{aligned}
$$

and

$$
\begin{aligned}
C_{1} & =C_{o x}\left(W_{n} \times L_{n(\text { drawn })}+W_{p} \times L_{p(\text { drawn })}\right)=1.725(2 \times 1+4 \times 1) \\
& =10.35 \mathrm{fF}
\end{aligned}
$$

Taking also $C_{w}=5 \mathrm{fF}$ into account and combining according to Eq. (6.140) we finally obtain

$$
\begin{aligned}
C_{e q}= & \frac{0.83 \mathrm{fF}}{\left(1+\frac{v_{O}}{0.909}\right)^{0.5}}+\frac{0.89 \mathrm{fF}}{\left(1+\frac{v_{O}}{0.968}\right)^{0.33}}+\frac{4.75 \mathrm{fF}}{\left(4.63-\frac{v_{o}}{0.909}\right)^{0.5}} \\
& +\frac{3.66 \mathrm{fF}}{\left(4.41-\frac{v_{O}}{0.968}\right)^{0.33}}+19.15 \mathrm{fF}
\end{aligned}
$$

image_name:(a)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: VI, Nn: GND}
name: Mp, type: PMOS, ports: {S: VDD, D: VO, G: VI}
name: Mn, type: NMOS, ports: {S: GND, D: VO, G: VI}
name: Ceq, type: Capacitor, value: Ceq, ports: {Np: VO, Nn: GND}
]
extrainfo:The circuit is an inverter with PMOS and NMOS transistors. It is used to estimate the propagation delay tPHL. The input voltage is VI, and the output voltage is VO. A current iDn flows through Mn, discharging the capacitor Ceq.
image_name:(b)
description:The graph labeled as '(b)' is a time-domain waveform illustrating the behavior of a circuit over time.

Axes Labels and Units:
- **X-Axis:** Represents time, likely in nanoseconds or microseconds, although the exact units are not specified. The time axis is linear, showing the progression of the waveform as time advances.
- **Y-Axis:** Represents voltage, presumably in volts. The vertical axis is also linear, displaying the voltage levels at different points in time.

Overall Behavior and Trends:
- The waveform shows a transition from a high voltage level to a low voltage level, indicating a falling edge. This is characteristic of a digital signal transitioning from a logic high to a logic low.
- The waveform likely corresponds to the output voltage, \( v_O \), as it reacts to an input signal change.
- The graph demonstrates a typical propagation delay, \( t_{PHL} \), where the output does not immediately follow the input transition.

Key Features and Technical Details:
- **Initial State:** The waveform begins at a high voltage level, which corresponds to the logic high state of the output.
- **Transition:** There is a noticeable delay before the voltage begins to fall, which is the propagation delay being analyzed.
- **Final State:** The waveform settles at a low voltage level, indicating the logic low state of the output.
- **Delay Measurement:** The time between the initial high state and the point where the waveform stabilizes at the low state is critical in determining the propagation delay.

Annotations and Specific Data Points:
- The waveform may include markers indicating key points such as the start of the transition and the point of stability at the low voltage level.
- If available, numerical values for the propagation delay \( t_{PHL} \) and the voltage levels at high and low states would be noted. However, these are not explicitly provided in the graph image.

This waveform is crucial for understanding the timing characteristics of the circuit, particularly how quickly it responds to changes in the input signal \( v_I \)."} urrences of the waveform. The graph is crucial for understanding the timing characteristics of the circuit, particularly how quickly it responds to changes in the input signal \( v_I \).

(a)
image_name:(b) waveforms
description:The graph presented is a time-domain waveform, illustrating the behavior of input and output voltages over time in a circuit. The x-axis represents time (t), and the y-axis represents voltage levels, specifically the input voltage \( v_I \) and the output voltage \( v_O \). The voltage levels are marked in terms of \( V_{DD} \) and \( V_{50\%} \).

On the y-axis, two significant voltage levels are noted: \( V_{DD} \), which is the initial high voltage level, and \( V_{50\%} \), representing half of \( V_{DD} \). The x-axis begins at zero and extends to the right, indicating the progression of time.

The waveform shows the transition of the output voltage \( v_O \) from \( V_{DD} \) to \( V_{50\%} \) over time. Initially, both \( v_I \) and \( v_O \) are at \( V_{DD} \). As time progresses, \( v_O \) decreases in a nonlinear fashion towards \( V_{50\%} \), with the waveform depicting a curve that starts steep and gradually flattens as it approaches \( V_{50\%} \). This curve is marked with a solid line initially, transitioning to a dashed line as it nears \( V_{50\%} \), indicating the estimated continuation of the trend.

The point where the waveform crosses \( V_{50\%} \) is noted as \( t_{PHL} \), which represents the propagation delay time for the output to fall from \( V_{DD} \) to \( V_{50\%} \). This is a critical parameter for understanding the timing characteristics of the circuit, particularly how quickly it responds to changes in the input signal \( v_I \). The arrow labeled \( v_I \) indicates the direction of the input voltage change from high to low, while the arrow labeled \( v_O \) follows the descending trend of the output voltage.

(b)

FIGURE 6.81 (a) Equivalent circuit for the estimation of $t_{P H L}$ and (b) waveforms.

We now wish to find quick estimates for the propagation delays. To estimate $t_{P H L}$ refer to Fig. 6.81, showing the situation after the transition of $v_{I}$ from 0 to $V_{D D}$. With $M_{p}$ off, $M_{n}$ pulls the current $i_{D n}$ out of $C_{e q}$, thus discharging it. Given the various approximations already made, we make one more and estimate the discharge from $V_{D D}$ to $V_{50 \%}\left(=0.5 V_{D D}\right)$ via the rule $C \Delta V=I \Delta t$ (cee delta vee equals aye delta tee), where $C=C_{e q}, \Delta V=0.5 V_{D D}, \Delta t=t_{P H L}$, and $I=i_{D n(\text { (avg })}$ is the average of $i_{D n}$ over the $t_{P H L}$ interval. We thus have

$$
\begin{equation*}
t_{P H L} \cong \frac{0.5 V_{D D} C_{e q}}{i_{D n(\text { avg })}} \tag{6.143a}
\end{equation*}
$$

Considering that at the beginning of the $t_{P H L}$ interval $M_{n}$ is in saturation and at the end it is in the triode region, we write

$$
\begin{equation*}
i_{D n(\mathrm{avg})}=\frac{1}{2} k_{n}^{\prime} W_{n}\left\{\frac{1}{2}\left(V_{D D}-V_{t n}\right)^{2}\left(1+\lambda_{n} V_{D D}\right)+\left[\left(V_{D D}-V_{t n}\right) \frac{V_{D D}}{2}-\frac{1}{2}\left(\frac{V_{D D}}{2}\right)^{2}\right]\left(1+\lambda_{n} \frac{V_{D D}}{2}\right)\right\} \tag{6.143b}
\end{equation*}
$$

Similar considerations hold for the estimation of $t_{P L H}$. Shown in Fig. 6.82 is the situation after the transition of $v_{I}$ from $V_{D D}$ to 0 . Now $M_{n}$ is off while $M_{p}$ sources the current $i_{D p}$ to $C_{e q}$, thus charging it. Adapting the above equations we write

$$
\begin{equation*}
t_{P L H} \cong \frac{0.5 V_{D D} C_{e q}}{i_{D p(\text { avg })}} \tag{6.144a}
\end{equation*}
$$

where

$$
\begin{equation*}
i_{D p(\mathrm{avg})}=\frac{1}{2} k_{p}^{\prime} \frac{W_{p}}{L_{p}}\left\{\frac{1}{2}\left(V_{D D}+V_{t p}\right)^{2}\left(1+\lambda_{p} V_{D D}\right)+\left[\left(V_{D D}+V_{t p}\right) \frac{V_{D D}}{2}-\frac{1}{2}\left(\frac{V_{D D}}{2}\right)^{2}\right]\left(1+\lambda_{p} \frac{V_{D D}}{2}\right)\right\} \tag{6.144b}
\end{equation*}
$$

image_name:(a)
description:
[
name: Mp, type: PMOS, ports: {S: VDD, D: Vo, G: Vin}
name: Mn, type: NMOS, ports: {S: GND, D: Vo, G: Vin}
name: Ceq, type: Capacitor, value: Ceq, ports: {Np: Vo, Nn: GND}
name: Vin, type: VoltageSource, value: 0 V, ports: {Np: Vin, Nn: GND}
]
extrainfo:The circuit is a CMOS inverter with a PMOS transistor (Mp) connected to VDD and an NMOS transistor (Mn) connected to GND. The output node Vo is connected to both the drain of Mp and Mn, and also to the capacitor Ceq. The input voltage Vin controls both transistors.
image_name:(b)
description:The graph in part (b) is a time-domain waveform illustrating the behavior of a CMOS inverter during the transition from low to high output voltage.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform showing the voltage levels over time for a CMOS inverter circuit.

2. **Axes Labels and Units:**
- The horizontal axis represents time \( t \) with an unspecified unit, typically in nanoseconds or microseconds for CMOS circuits.
- The vertical axis represents voltage \( V_I, V_O \) with the unit of volts (V).
- The graph includes significant markers such as \( V_{DD} \) and \( V_{50\%} \).

3. **Overall Behavior and Trends:**
- The waveform starts at 0 volts and rises to \( V_{DD} \), indicating the transition of the output voltage \( V_O \) from a low to a high state.
- The curve is initially steep, indicating a rapid increase in voltage, and then gradually levels off as it approaches \( V_{DD} \).

4. **Key Features and Technical Details:**
- The point \( t_{PLH} \) marks the propagation delay for the low-to-high transition, where the output voltage \( V_O \) reaches the midpoint \( V_{50\%} \) of \( V_{DD} \).
- The input voltage \( V_I \) is shown as a dashed line, remaining constant at \( V_{DD} \), indicating that the input has already transitioned to high.

5. **Annotations and Specific Data Points:**
- The graph includes a horizontal reference line at \( V_{50\%} \), indicating the halfway point of the output voltage transition.
- \( t_{PLH} \) is annotated to show the specific time at which the output voltage reaches \( V_{50\%} \).

This graph effectively illustrates the propagation delay in the CMOS inverter, providing a clear visual representation of how the output voltage transitions over time in response to a change in the input voltage.

FIGURE 6.82 (a) Equivalent circuit for the estimation of $t_{P L H}$ and (b) waveforms.
(a) Using the data of Example 6.27, estimate the propagation delays of the CMOS inverter of Fig. 6.78 and compare with PSpice.
(b) What would be the delays with a fanout of 0 and $C_{w}=0$ ?

#### Solution

(a) We have $k_{n}^{\prime}=600 \times\left(10^{-2}\right)^{2} \times 1.725 \times 10^{-15} /\left(10^{-6}\right)^{2}=103.5 \mu \mathrm{~A} / \mathrm{V}^{2}, L_{n}=$ $1.0-2 \times 0.15=0.7 \mu \mathrm{~m}, k_{p}^{\prime}=250 \times 1.725 \times(0.1)=43.1 \mu \mathrm{~A} / \mathrm{V}^{2}$, and $L_{p}=1.0-2 \times 0.2=0.6 \mu \mathrm{~m}$. By Eqs. (6.143b) and (6.144b),

$$
\begin{aligned}
i_{D n(\mathrm{avg})}= & \frac{1}{2} 103.5 \frac{2}{0.7}\left\{\frac{1}{2}(3.3-0.7)^{2}(1+0.1 \times 3.3)\right. \\
& \left.+\left[(3.3-0.7) \frac{3.3}{2}-\frac{1}{2}\left(\frac{3.3}{2}\right)^{2}\right]\left(1+0.1 \frac{3.3}{2}\right)\right\}=1.17 \mathrm{~mA} \\
i_{D p(\mathrm{avg})}= & \frac{1}{2} 43.1 \frac{4}{0.6}\left\{\frac{1}{2}(3.3-0.7)^{2}(1+0.05 \times 3.3)\right. \\
& \left.+\left[(3.3-0.7) \frac{3.3}{2}-\frac{1}{2}\left(\frac{3.3}{2}\right)^{2}\right]\left(1+0.05 \frac{3.3}{2}\right)\right\}=1.02 \mathrm{~mA}
\end{aligned}
$$

A problem with $C_{e q}$ is that its components $C_{d b n}$ and $C_{d b p}$ depend on $v_{o}$. We can simplify our analysis by computing them at the beginning and at the end of the propagation interval under consideration, and then using their average value. Thus, at the beginning of $t_{P H L}$ we have $v_{O}=3.3 \mathrm{~V}$, where we calculate $C_{d b n}(3.3)=0.93 \mathrm{fF}$ and $C_{d b p}(3.3)=8.41 \mathrm{fF}$. At the end of $t_{P H L}$ we have $v_{O}=$ 1.65 V , where we calculate $C_{d b n}(1.65)=1.15 \mathrm{fF}$ and $C_{d b p}(1.65)=5.47 \mathrm{fF}$. The average of their sum is thus $0.5(0.93+8.41+1.15+5.47)=7.98 \mathrm{fF}$. Consequently, $C_{e q}=7.98+19.15=27.13 \mathrm{fF}$, and

$$
t_{P H L} \cong \frac{1.65 \times 27.13 \times 10^{-15}}{1.17 \times 10^{-3}}=38.3 \mathrm{ps}(39.6 \mathrm{ps} \text { with PSpice })
$$

Likewise, at the beginning of $t_{P L H}$ we have $v_{O}=0$, where $C_{d b n}(0)=1.72 \mathrm{fF}$ and $C_{d b p}(0)=4.45 \mathrm{fF}$. At the end of $t_{P L H}$ we have $v_{O}=1.65 \mathrm{~V}$, so we recycle $C_{d b n}(1.65)=1.15 \mathrm{fF}$ and $C_{d b p}(3.3)=5.47 \mathrm{fF}$. The average of their sum is thus $0.5(1.72+4.45+1.65+5.47)=6.65 \mathrm{fF}$. Consequently, $C_{e q}=6.65+$ $19.15=25.80 \mathrm{fF}$, and

$$
t_{P L H} \cong \frac{1.65 \times 25.80 \times 10^{-15}}{1.02 \times 10^{-3}}=41.7 \mathrm{ps}(43.3 \mathrm{ps} \text { with PSpice })
$$

(b) With a fanout of 0 , only $C_{0}$ will appear in the calculations, so we need to recalculate but with $C_{e q}$ reduced by the sum $C_{1}+C_{w}(=10.35+5=15.35 \mathrm{fF})$. So, for $t_{P H L}$ we have $C_{e q}=27.13-15.35=11.78 \mathrm{fF}$, and we use proportionality to find $t_{P H L}=38.3(11.78 / 27.13) \cong 16.6 \mathrm{ps}$ ( 20 ps with PSpice). Likewise, using $C_{e q}=28.80-15.35=13.45 \mathrm{fF}$ we get $t_{P L H}=41.7(13.45 / 25.80) \cong$ 21.7 ps (18.7 ps with PSpice).

### Power Dissipation of CMOS Logic Gates

As a CMOS inverter is sitting in either state ( $v_{O}=0$ or $v_{O}=V_{D D}$ ), one of its two transistors is off, drawing only leakage current. We say that the static power dissipation of a CMOS gate is virtually zero. However, when the output is switched from one state to the other, energy is expended to charge/discharge the stray capacitances, thus resulting in nonzero dynamic power dissipation.

Specifically, to switch $v_{O}$ from 0 to $V_{D D}, M_{p}$ must expend some energy $E_{p}$ in order to charge $C_{e q}$ to $V_{D D}$ (see Fig. 6.82a). Once charged, $C_{e q}$ holds the energy $E_{C}=$ $(1 / 2) C_{e q} V_{D D}^{2}$. Likewise, to return $v_{O}$ from $V_{D D}$ to $0, M_{n}$ must expend some energy $E_{n}$ in order to discharge $C_{e q}$ to 0 (see Fig. 6.81a). By the energy conservation principle we must have $E_{n}=E_{C}$. Also, by symmetry, $E_{p}=E_{n}$. The amount of energy dissipated by the gate during a complete cycle is thus $E_{\text {cycle }}=E_{p}+E_{n}=2 E_{C}=C_{e q} V_{D D}^{2}$. If the gate is operated at an average frequency of $f_{\text {avg }}$ cycles/sec, the average power $P$ dissipated by the gate equals, by definition, the amount of energy dissipated in 1 sec , or $P=$ $E_{\text {cycle }} \times f_{\text {avg }}$. Consequently, we have

$$
\begin{equation*}
P=C_{e q} V_{D D}^{2} f_{a v g} \tag{6.145}
\end{equation*}
$$

It is apparent that the higher the operating frequency, the higher the dissipation. Moreover, power scales quadratically with the power supply.

Using the data of Example 6.28 , estimate $P$ for $f_{\text {avg }}=1 \mathrm{kHz}$. What happens if $f_{\text {avg }}$ is raised to 100 MHz ?

#### Solution

By Eq. (6.145), $P=25.80 \times 10^{-15} \times 3.3^{2} \times 10^{3}=0.281 \mathrm{nW}$. Now $P=$ $(0.281 \mathrm{nW}) \times\left(10^{8} / 10^{3}\right)=28.1 \mu \mathrm{~W}$.

### Transient Response of Voltage Comparators

Being digital-ouput devices, comparators are characterized via propagation delays just like logic gates. However, being analog-input devices, the input test conditions are specified differently. As shown in Fig. 6.83, the input is usually a pulse with a $100-\mathrm{mV}$ baseline and an overdrive $V_{O V}$ designed to barely exceed a level that will cause the comparator to trip (typically, $V_{O V}$ is in the mV range). Given the circuit complexity of a comparator, hand analysis is generally prohibitive, so computer simulation becomes a necessity. The IC designer will simulate a comparator at the transistor level, whereas the user will most likely simulate it using the macro-model supplied by the manufacturer.
image_name:(a)
description:
[
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
name: OpAmp, type: OpAmp, ports: {InP: GND, InN: VI, OutP: VO}
]
extrainfo:The circuit is a simple test setup to investigate the transient response of a voltage comparator using an operational amplifier and a voltage source.

GND (a)
image_name:v_I vs t graph
description:The graph titled "v_I vs t graph" is a time-domain waveform illustrating the voltage input (v_I) against time (t).

1. **Type of Graph and Function:**
- This is a time-domain waveform graph.

2. **Axes Labels and Units:**
- The horizontal axis represents time (t), although no specific units are indicated, it typically would be in seconds or milliseconds.
- The vertical axis represents the input voltage (v_I) in millivolts (mV).
- The scale appears to be linear for both axes.

3. **Overall Behavior and Trends:**
- The graph shows a constant input voltage over time. Initially, the voltage is at -100 mV and then steps to 0 mV, maintaining this level for the duration shown.
- There is no visible oscillation or transient behavior in the input voltage; it remains steady at 0 mV after the initial step.

4. **Key Features and Technical Details:**
- The graph starts at -100 mV and then transitions to 0 mV. This step change is likely used to test the response of the voltage comparator.
- The transition point is marked by an arrow labeled "V_ov," indicating the overshoot or a notable point in the waveform.
- The graph does not show any peaks, valleys, or inflection points beyond the initial step change.

5. **Annotations and Specific Data Points:**
- The graph includes an annotation "V_ov" at the transition point, which might indicate a specific overshoot or a point of interest in the context of the circuit's response.
- The initial voltage level is -100 mV, and it stabilizes at 0 mV, which are the key numerical values depicted in the graph.

image_name:(b)
description:The graph in question is a time-domain waveform depicting the transient response of a voltage comparator. The x-axis represents time, denoted as \( t \), and is likely measured in a unit such as milliseconds or microseconds, although the specific unit is not provided in the image. The y-axis represents the output voltage, \( v_O \), in volts.

The graph illustrates a step response, starting at a high output voltage level, \( V_{OH} \), and transitioning to a low output voltage level, \( V_{OL} \). The waveform shows a smooth, continuous decrease from \( V_{OH} \) to \( V_{OL} \), indicating a typical response of a comparator to an input pulse.

A key feature on the graph is the midpoint voltage, \( V_{50\%} \), which is the voltage level halfway between \( V_{OH} \) and \( V_{OL} \). This point is used to determine the propagation delay, \( t_P \), which is marked on the graph as the time it takes for the voltage to transition from \( V_{OH} \) to \( V_{50\%} \).

The waveform does not exhibit any overshoot, undershoot, or oscillations, suggesting a well-damped response. The graph is annotated with these key voltage levels and the propagation delay, providing a clear depiction of the comparator's transient behavior.

(b)

FIGURE 6.83 (a) Test circuit to investigate (b) the transient response of a voltage comparator.

Shown in Fig. 6.84 is a PSpice circuit to display the transient response of the popular LM339 comparator, using its SPICE macro-model. Figure 6.85 shows the responses to the leading as well as the trailing edge of the input pulse (note the dissymmetry reflecting internal circuit dissymmetries, particularly in the output stage). The overdrives used are $V_{O V}=5 \mathrm{mV}, 20 \mathrm{mV}$, and 100 mV . As a rule, the higher the overdrive, the shorter the propagation delays.
image_name:FIGURE 6.84
description:
[
name: LM339, type: OpAmp, value: LM339, ports: {InP: 5, InN: 4, OutP: 2, OutN: GND, Vdd: VCC, -Vdd: GND}
name: RPU, type: Resistor, value: 2kΩ, ports: {N1: 3, N2: Vout}
name: VCC, type: VoltageSource, value: +5V, ports: {Np: VCC, Nn: GND}
name: V1, type: VoltageSource, ports: {Np: 4, Nn: GND}
]
extrainfo:The circuit is a voltage comparator using the LM339. It compares the input voltage V1 to a reference level and outputs the result at Vo. The resistor RPU is used as a pull-up resistor for the open-collector output of the comparator.

FIGURE 6.84 PSpice circuit to display the transient responses of the LM339 voltage comparator for different input overdrives.
image_name:(a)
description:The graph labeled "(a)" consists of two separate plots depicting the transient response of a voltage comparator, specifically the LM339, for different input overdrives. The upper plot shows the input voltage \( v_i(t) \) over time, while the lower plot shows the corresponding output voltage \( v_o(t) \).

Upper Plot (Input Voltage \( v_i(t) \))
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:**
- **X-axis:** Time \( t \) in microseconds (\( \mu s \)), ranging from 0 to 1.8 \( \mu s \).
- **Y-axis:** Input voltage \( v_i \) in millivolts (mV), ranging from -100 mV to 100 mV.
- **Overall Behavior and Trends:**
- The plot shows three distinct constant input voltages: 5 mV, 20 mV, and 100 mV.
- Each voltage level is held constant over time, indicating different levels of input overdrive.
- **Annotations and Specific Data Points:**
- Each voltage level is annotated with its respective value (5 mV, 20 mV, 100 mV).

Lower Plot (Output Voltage \( v_o(t) \))
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:**
- **X-axis:** Time \( t \) in microseconds (\( \mu s \)), ranging from 0 to 1.8 \( \mu s \).
- **Y-axis:** Output voltage \( v_o \) in volts (V), ranging from 0 to 5 V.
- **Overall Behavior and Trends:**
- The output voltage shows a rapid transition from 5 V to 0 V for each input overdrive level.
- The transition occurs more quickly for higher input overdrive values.
- The 100 mV input results in the fastest transition, followed by 20 mV, and then 5 mV.
- **Annotations and Specific Data Points:**
- Each curve is annotated with its corresponding input overdrive value (100 mV, 20 mV, 5 mV).
- The transition points are marked, showing the response time for each input level.
image_name:(b)
description:The graph labeled "(b)" is a set of time-domain waveforms showing the transient response of an LM339 voltage comparator circuit for different negative input overdrives. The graph consists of two plots:

1. **Top Plot - Input Voltage (v_i) vs. Time (t):**
- **Type:** Time-domain waveform.
- **Axes:**
- X-axis: Time (t) in microseconds (μs), ranging from 0 to 1.8 μs.
- Y-axis: Input voltage (v_i) in millivolts (mV), ranging from -100 mV to 100 mV.
- **Behavior:** The plot shows three distinct constant input voltage levels at -5 mV, -20 mV, and -100 mV, indicated by horizontal lines.
- **Annotations:** Each line is labeled with its corresponding voltage value.

2. **Bottom Plot - Output Voltage (v_o) vs. Time (t):**
- **Type:** Time-domain waveform.
- **Axes:**
- X-axis: Time (t) in microseconds (μs), ranging from 0 to 1.8 μs.
- Y-axis: Output voltage (v_o) in volts (V), ranging from 0 to 5 V.
- **Behavior:** The plot shows the output voltage response of the comparator. For each input voltage level (-100 mV, -20 mV, -5 mV), the output voltage transitions from 0 V to 5 V. The transition occurs at different times based on the input overdrive, with larger negative overdrives resulting in earlier transitions.
- **Annotations:** The curves are labeled with their corresponding input voltage values, showing that the -100 mV input results in the earliest transition, followed by -20 mV, and finally -5 mV.

**Overall Trends:**
- The response time of the comparator decreases with increasing magnitude of negative input overdrive. This is evident as the output transitions occur earlier for larger negative input voltages.
- The output voltage sharply transitions from 0 V to 5 V, indicating a clear switching behavior typical of a comparator circuit.

FIGURE 6.85 The transient responses of the PSpice circuit of Fig. 6.84 for different input overdrives.

## APPENDIX 6A

### Transfer Functions and Bode Plots

The frequency characteristics of circuits are represented mathematically via transfer functions and are visualized graphically via Bode plots. A transfer function is a function of the complex frequency s, the most common examples being gain and input/ output impedances. Gain is the ratio of the Laplace's transforms of the output and input signals, or $a(s)=S_{o}(s) / S_{i}(s)$. The transfer functions of interest to us can always be put, through suitable algebraic manipulations, in the following insightful standard form

$$
a(s)=a_{0} \frac{\left(1+s / \omega_{z 1}\right)\left(1+s / \omega_{z 2}\right) \ldots\left(1+s / \omega_{z n}\right)}{\left(1+s / \omega_{p 1}\right)\left(1+s / \omega_{p 2}\right) \ldots\left(1+s / \omega_{p n}\right)}
$$

where $a_{0}$ is the value of $a(s)$ in the limit $s \rightarrow 0$ and is thus referred to as the lowfrequency gain. (This is the gain that we have been dealing with in the previous chapters). Since the numerator vanishes for $s=-\omega_{z 1}, s=-\omega_{z 2}, \ldots s=-\omega_{z n}$, the $\omega_{z} \mathrm{~s}$ are referred to as the zero frequencies of $a(s)$. These frequencies are real, and may be positive, negative, or even infinite. The denominator vanishes for $s=-\omega_{p 1}$, $s=-\omega_{p 2}, \ldots s=-\omega_{p n}$, causing $a(s)$ to blow up to infinity. The $\omega_{p} \mathrm{~s}$ are referred to as the pole frequencies of $a(s)$, and in this chapter they are real and positive. Poles and zeros are jointly referred to as roots.

An important tenet of systems theory ${ }^{7}$ states that if we are interested only in the ac steady-state response of a circuit, also called the frequency response, then we can restrict our transfer-function calculations to the $j \omega$ axis only. We do this simply by letting $s \rightarrow j \omega$, after which we get

$$
\begin{equation*}
a(j \omega)=a_{0} \frac{\left(1+j \omega / \omega_{z 1}\right)\left(1+j \omega / \omega_{z 2}\right) \ldots\left(1+j \omega / \omega_{z n}\right)}{\left(1+j \omega / \omega_{p 1}\right)\left(1+j \omega / \omega_{p 2}\right) \ldots\left(1+j \omega / \omega_{p n}\right)} \tag{6A.1}
\end{equation*}
$$

Clearly, $a(j \omega)$ is a complex function. Its magnitude $|a|$ and phase angle $\mathrm{ph} a$ are found as

$$
\begin{equation*}
|a(j \omega)|=\left|a_{0}\right| \sqrt{\frac{\left(1+\omega^{2} / \omega_{z 2}^{2}\right)\left(1+\omega^{2} / \omega_{z 2}^{2}\right) \ldots\left(1+\omega^{2} / \omega_{z n}^{2}\right)}{\left(1+\omega^{2} / \omega_{p 1}^{2}\right)\left(1+\omega^{2} / \omega_{p 2}^{2}\right) \ldots\left(1+\omega^{2} / \omega_{p n}^{2}\right)}} \tag{6A.2}
\end{equation*}
$$

and

$$
\begin{equation*}
\operatorname{ph} a(j \omega)=\tan ^{-1} \frac{\omega}{\omega_{z 1}}+\tan ^{-1} \frac{\omega}{\omega_{z 2}}+\cdots \tan ^{-1} \frac{\omega}{\omega_{z \mathrm{n}}}-\tan ^{-1} \frac{\omega}{\omega_{p 1}}-\tan ^{-1} \frac{\omega}{\omega_{p 2}} \cdots-\tan ^{-1} \frac{\omega}{\omega_{p n}} \tag{6A.3}
\end{equation*}
$$

The frequency behavior of $|a(j \omega)|$ and $\operatorname{ph} a(j \omega)$ is best visualized via frequency plots. Magnitude is expressed in decibels as

$$
\begin{equation*}
|a(j \omega)|_{\mathrm{dB}}=20 \log _{10}|a(j \omega)| \tag{6A.4}
\end{equation*}
$$

and $\mathrm{ph} a(j \omega)$ is expressed in degrees, and both functions are plotted versus $\omega$ on a logarithmic scale. The most common frequency intervals are decades ( $\omega=\ldots 10^{-2}$, $10^{-1}, 10^{0}, 10^{1}, 10^{2} \ldots \mathrm{rad} / \mathrm{s}$ ), though octave intervals are also used ( $\omega=\ldots 2^{-2}$, $2^{-1}, 2^{0}, 2^{1}, 2^{2} \ldots \mathrm{rad} / \mathrm{s}$ ), especially in connection with audio circuits. Following is a worth-remembering list of frequently occurring gains as well as their decibel values:

$$
\begin{equation*}
|1|_{\mathrm{dB}}=0 \mathrm{~dB} \quad\left|2^{ \pm 1 / 2}\right|_{\mathrm{dB}}= \pm 3 \mathrm{~dB} \quad\left|2^{ \pm n}\right|_{\mathrm{dB}}= \pm 6 n \mathrm{~dB} \quad\left|10^{ \pm n}\right|_{\mathrm{dB}}= \pm 20 n \mathrm{~dB} \tag{6A.5}
\end{equation*}
$$

Note that positive decibels imply amplification and negative decibels imply attenuation, with the borderline between the two being 0 dB , or unity gain. Moreover, given two transfer functions $a_{1}(j \omega)$ and $a_{2}(j \omega)$, we have, by familiar properties of logarithms,

$$
\begin{gather*}
\left|a_{1} \times a_{2}\right|_{\mathrm{dB}}=\left|a_{1}\right|_{\mathrm{dB}}+\left|a_{2}\right|_{\mathrm{dB}}  \tag{6A.6a}\\
\left|a_{1}(j \omega) / a_{2}(j \omega)\right|_{\mathrm{dB}}=\left|a_{1}\right|_{\mathrm{dB}}-\left|a_{2}\right|_{\mathrm{dB}} \tag{6A.6b}
\end{gather*}
$$

that is, the magnitude plot of a product (ratio) is simply the sum (difference) of the individual magnitude plots. In particular, $|1 / a|_{\mathrm{dB}}=-|a|_{\mathrm{AB}}$, that is, the magnitude plot of the reciprocal is simply the magnitude plot of the original, but reflected about the horizontal axis.

Given a root $\omega_{0}$, we will make use of the following approximations:

$$
\begin{gather*}
\left(\omega \ll \omega_{0}\right) \Rightarrow\left(1+j \omega / \omega_{0}\right) \rightarrow 1  \tag{6A.7a}\\
\left(\omega \gg \omega_{0}\right) \Rightarrow\left(1+j \omega / \omega_{0}\right) \rightarrow j \omega / \omega_{0} \tag{6~A.7~b}
\end{gather*}
$$

image_name:(a)
description:The graph labeled "(a)" is a Bode plot representing the frequency response of a differentiator function, specifically \( j \omega / \omega_{0} \). This plot is characterized by the following features:

1. **Type of Graph and Function:**
- This is a Bode plot, which is commonly used to represent the frequency response of linear time-invariant systems. It shows the gain of the differentiator function across a range of frequencies.

2. **Axes Labels and Units:**
- The horizontal axis is labeled "Normalized frequency \( \omega / \omega_{0} \)" and is scaled logarithmically, covering a range from 0.01 to 100.
- The vertical axis is labeled "Gain (dB)" and spans from -40 dB to 40 dB.

3. **Overall Behavior and Trends:**
- The plot shows a linear increase in gain with frequency. The slope of the line is +20 dB/decade, indicating that for every tenfold increase in normalized frequency, the gain increases by 20 dB.
- The line passes through the origin, indicating that at the normalized frequency of \( \omega = \omega_{0} \), the gain is 0 dB.

4. **Key Features and Technical Details:**
- The graph is a straight line with a consistent positive slope, reflecting the differentiator's property of amplifying higher frequencies.
- There are no peaks, valleys, or inflection points, as expected for a simple differentiator function.

5. **Annotations and Specific Data Points:**
- The slope of +20 dB/decade is explicitly annotated on the graph, reinforcing the linear relationship between frequency and gain.

This Bode plot visually represents how the differentiator function increases the gain linearly with frequency, highlighting its characteristic behavior of enhancing higher frequency components.
image_name:(b)
description:The graph labeled (b) is a Bode plot representing the gain of the integrator function \(1 /(j \omega / \omega_{0})\). The x-axis is labeled 'Normalized frequency \(\omega/\omega_{0}\) (dec)' and is logarithmically scaled, spanning from 0.01 to 100. The y-axis is labeled 'Gain (dB)' and is linearly scaled from -40 dB to 40 dB.

The plot shows a linear decreasing trend, with the gain decreasing at a constant rate of -20 dB per decade. This indicates that as the normalized frequency increases, the gain decreases. The line crosses the 0 dB gain level at a normalized frequency of 1.

Key features of the plot include:
- A slope of -20 dB/decade, characteristic of an integrator.
- The gain is 40 dB at a normalized frequency of 0.01 and decreases to -40 dB at a normalized frequency of 100.

This behavior reflects the mathematical relationship of the integrator function, where the gain decreases inversely with frequency.

FIGURE 6A. 1 Frequency plots of the (a) differentiator $j \omega / \omega_{0}$ and (b) integrator $1 /\left(j \omega / \omega_{0}\right)$ functions.

The function $j \omega / \omega_{0}$ is called the differentiator function, and its reciprocal $1 /\left(j \omega / \omega_{0}\right)$ is called the integrator function. These functions have, respectively, a zero and a pole at the origin, and their magnitudes are, $\left|j \omega / \omega_{0}\right|_{\mathrm{AB}}=20 \log \left(\omega / \omega_{0}\right)$ and $\left|1 /\left(j \omega / \omega_{0}\right)\right|_{\mathrm{dB}}=$ $-20 \log \left(\omega / \omega_{0}\right)$. With a logarithmic frequency scale, these equations are of the type $y= \pm 20 x$, that is, straight lines with a slope of $+20 \mathrm{~dB} /$ decade $(+6 \mathrm{~dB} /$ octave $)$ in the differentiator case, and $-20 \mathrm{~dB} /$ decade ( $-6 \mathrm{~dB} /$ octave) in the integrator case. These curves are shown in Fig. 6A.1. Since the two functions are the reciprocal of each other, the plot of one is obtained from the other by a simple reflection about the $0-\mathrm{dB}$ axis. Both curves intersect the $0-\mathrm{dB}$ axis at $\omega=\omega_{0}$, so $\omega_{0}$ is aptly called the unity-gain frequency.

### Bode Plots

To speed up drawing frequency plots by hand, Hendrik W. Bode (1905-1982) proposed a piecewise linear approximation consisting of suitably sloped straight segments joined together at the various root frequencies. This technique assumes the approximations of Eqs. (6A.7) to be valid not only far away from a given root, but also in the vicinity of it. It turns out that this technique is quite adequate if the roots are widely spaced, say by a decade or more. Even if they aren't, it still provides valuable insight into the frequency behavior of a circuit.

To illustrate the technique, consider the function

$$
\begin{equation*}
a(j \omega)=100 \frac{\left(1+j \omega / 10^{1}\right)\left(1+j \omega / 10^{5}\right)}{\left(1+j \omega / 10^{2}\right)\left(1+j \omega / 10^{3}\right)\left(1+j \omega / 10^{4}\right)} \tag{6A.8}
\end{equation*}
$$

having a dc gain of 100 , two zero frequencies at $10^{1}$ and $10^{5} \mathrm{rad} / \mathrm{s}$, and three pole frequencies at $10^{2}, 10^{3}$, and $10^{4} \mathrm{rad} / \mathrm{s}$. (For simplicity the roots have been assumed to have nicely rounded values, spaced a decade apart from each other.) To construct the

Bode plot, start out at low frequencies and proceed toward high frequencies, stopping at each root to determine the slope of the next segment.

- For $\omega \ll 10^{1} \mathrm{rad} / \mathrm{s}$ (first root), all numerator and denominator terms in Eq. (6A.8) satisfy Eq. (6A.7a), giving $a(j \omega) \cong 100=40 \mathrm{~dB}$. Bode's approximation is to assume that this holds all the way up to the first root of $10^{1} \mathrm{rad} / \mathrm{s}$, that is, for $\omega \leq 10^{1} \mathrm{rad} / \mathrm{s}$ (not just for $\omega \ll 10^{1} \mathrm{rad} / \mathrm{s}$ ). Consequently, the first portion of the plot is a horizontal segment positioned at 40 dB .
- For $10^{1} \ll \omega \ll 10^{2} \mathrm{rad} / \mathrm{s}$, the first numerator term satisfies Eq. (6A.7b) while all others still satisfy Eq. $(6 \mathrm{~A} .7 a)$, giving $a(j \omega) \cong 100 \times\left(j \omega / 10^{1}\right)$. This is a differentiator function with a unity-gain frequency of $\omega=10^{1} \mathrm{rad} / \mathrm{s}$, but shifted upwards by 40 dB , as per Eq. (6A.6a). The result is a segment with a slope of $+20 \mathrm{~dB} / \mathrm{dec}$. Bode's approximation is to assume that this holds over the entire interval $10^{1} \leq \omega \leq 10^{2} \mathrm{rad} / \mathrm{s}$, not just well away from its extremes.
- Proceeding in similar manner, we can say that for $10^{2} \leq \omega \leq 10^{3} \mathrm{rad} / \mathrm{s}$, the first numerator and the first denominator terms satisfy Eq. (6A.7b) while all others still satisfy Eq. $(6 \mathrm{~A} \cdot 7 a)$. Consequently, $a(j \omega) \cong 100 \times\left(j \omega / 10^{1}\right) /\left(j \omega / 10^{2}\right)=$ $1000=60 \mathrm{~dB}$. This is again a horizontal segment but positioned at 60 dB .
- For $10^{3} \leq \omega \leq 10^{4} \mathrm{rad} / \mathrm{s}$, the first numerator term, and the second and third denominator terms satisfy Eq. (6A.7b) while all others still satisfy Eq. (6A.7a), so $a(j \omega) \cong 100 \times\left(j \omega / 10^{1}\right) /\left[\left(j \omega / 10^{2}\right)\left(j \omega / 10^{3}\right)\right]=1000 /\left(j \omega / 10^{3}\right)$. This is an integrator function with a unity-gain frequency of $\omega=10^{3} \mathrm{rad} / \mathrm{s}$, but shifted upwards by 60 dB , as per Eq. (6A.6a). The result is a segment with a slope of $-20 \mathrm{~dB} / \mathrm{dec}$.
- Likewise, for $10^{4} \leq \omega \leq 10^{5} \mathrm{rad} / \mathrm{s}$ we write $a(j \omega) \cong 1000 /\left[\left(j \omega / 10^{3}\right)\left(j \omega / 10^{4}\right)\right]$, indicating that another integrator term has kicked in at $\omega=10^{4} \mathrm{rad} / \mathrm{s}$, causing an additional $-20-\mathrm{dB}$ change in slope, for a net slope of $-40 \mathrm{~dB} / \mathrm{dec}$ over this frequency interval. We can say that over this frequency interval our transfer function exhibits double-integrator behavior.
- For $\omega \geq 10^{5} \mathrm{rad} / \mathrm{s}$, all numerator and denominator terms satisfy Eq. (6A.7b), thus giving, after simplifications, $a(j \omega) \cong 1 /\left(j \omega / 10^{5}\right)$. This is again an integrator function, now with a unity-gain frequency of $10^{5} \mathrm{rad} / \mathrm{s}$. Above this breakpoint gain rolls off with frequency with a slope of $-20 \mathrm{~dB} / \mathrm{dec}$.

To get an idea of the errors incurred in using linearized magnitude plots, consider the gain at $\omega=10^{1} \mathrm{rad} / \mathrm{s}$ (first root). By Eq. (6A.2) we have

$$
\begin{aligned}
|a(j 10)| & =100 \sqrt{\frac{\left[1+\left(10 / 10^{1}\right)^{2}\right]\left[1+\left(10 / 10^{5}\right)^{2}\right]}{\left[1+\left(10 / 10^{2}\right)^{2}\right]\left[1+\left(10 / 10^{3}\right)^{2}\right]\left[1+\left(10 / 10^{4}\right)^{2}\right]}} \\
& \cong 100 \sqrt{2}=(40+3) \mathrm{dB}=43 \mathrm{~dB}
\end{aligned}
$$

indicating that our linearized plot underestimates magnitude by 3 dB at the first root frequency. Likewise, you can verify that $\left|a\left(j 10^{2}\right)\right| \cong 1000 / \sqrt{2}=60-3=57 \mathrm{~dB}$, indicating a $3-\mathrm{dB}$ overestimate at the second root. A quick look at Fig. 6A. 2 confirms that the piecewise linear approximation is fairly close to the exact plot, shown in shaded form.
image_name:FIGURE 6A. 2
description:The graph in FIGURE 6A.2 is a Bode plot, which is used to represent the gain of a system as a function of frequency. The plot is characterized by a logarithmic scale on the x-axis, labeled 'Frequency \( \omega \)' in decades, ranging from \(10^0\) to \(10^6\). The y-axis represents 'Gain' in decibels (dB), ranging from \(-20\) dB to \(60\) dB.

The graph displays both a piecewise linear approximation and an exact plot, with the exact plot shown as shaded curves. The linear approximation consists of straight-line segments that simplify the analysis of the system's behavior.

Overall Behavior and Trends
- **Low Frequency Behavior:** Starting at low frequencies, the gain is approximately constant at around 40 dB up to a frequency slightly above \(10^1\) Hz.
- **Mid Frequency Rise:** As frequency increases to around \(10^2\) Hz, the gain increases sharply, reaching a peak of about 60 dB.
- **High Frequency Decline:** Beyond this peak, the gain remains relatively constant until around \(10^4\) Hz, after which it begins to decrease steadily, dropping back to around 40 dB at \(10^5\) Hz and continuing to decline.

Key Features
- **Peaks and Valleys:** The plot has a noticeable peak at approximately \(10^2\) Hz, where the gain reaches its maximum value of about 60 dB.
- **Asymptotic Behavior:** The linear approximation shows asymptotic behavior at both low and high frequencies, with horizontal sections at low frequencies and a downward slope at high frequencies.
- **-3 dB Points:** The description indicates underestimation and overestimation by 3 dB at certain frequencies, suggesting the presence of -3 dB points near the first and second root frequencies.

Annotations and Specific Data Points
- The plot is annotated with gridlines for better reference, and the shaded area represents the exact gain, allowing comparison with the linear approximation.

This Bode plot is useful for analyzing the frequency response of the system described by Equation (6A.8), particularly in understanding how well the linear approximation aligns with the exact system behavior at various frequencies.

FIGURE 6A. 2 Linearized Bode plot for the gain of Eq. (6A.8). The shaded curves show the exact plot.

The procedure for drawing linearized Bode plots can be speeded up considerably as follows:

- Starting out at low frequencies, draw the low-frequency asymptote up to the first nonzero root. This asymptote will be horizontal if the transfer function has no roots at the origin, or will have a slope of $\pm 20-\mathrm{dB} / \mathrm{dec}$ for each zero/pole at the origin.
- As you move toward the right and hit a root frequency, change the present slope by either $+20 \mathrm{~dB} / \mathrm{dec}$ or by $-20 \mathrm{~dB} / \mathrm{dec}$, depending on whether this root is, respectively, a zero ( + ) or a pole ( - ).
- Proceed toward the right till all roots have been exhausted.

As another example, consider the function

$$
\begin{equation*}
a(j \omega)=10 \frac{j \omega\left(1+j \omega / 10^{3}\right)}{\left(1+j \omega / 10^{1}\right)\left(1+j \omega / 10^{2}\right)\left(1+j \omega / 10^{4}\right)} \tag{6A.9}
\end{equation*}
$$

To draw the linearized magnitude plot, proceed as follows:

- At low frequencies all terms within parentheses reduce to unity, so the lowfrequency asymptote is $a(j \omega) \cong 10 j \omega=j \omega / 10^{-1}$. This is a differentiator function with a unity-gain frequency of $\omega=10^{-1} \mathrm{rad} / \mathrm{s}$, so the asymptote is a straight line with a slope of $+20 \mathrm{~dB} / \mathrm{dec}$ and a $0-\mathrm{dB}$ axis intercept at $10^{-1} \mathrm{rad} / \mathrm{s}$.
- Coming from the left, draw this asymptote till you hit the first nonzero root at $10^{1} \mathrm{rad} / \mathrm{s}$.
- Since $10^{1} \mathrm{rad} / \mathrm{s}$ is a pole, change the present slope by $-20 \mathrm{db} / \mathrm{dec}$, that is, change it from $+20 \mathrm{~dB} / \mathrm{dec}$ to $+20-20=0 \mathrm{~dB} / \mathrm{dec}$. This yields a horizontal segment till the next root at $10^{2} \mathrm{rad} / \mathrm{s}$.
- Since $10^{2} \mathrm{rad} / \mathrm{s}$ is a pole, change the slope from 0 to $-20 \mathrm{~dB} / \mathrm{dec}$, and continue till the next root at $10^{3} \mathrm{rad} / \mathrm{s}$.
- Since $10^{3} \mathrm{rad} / \mathrm{s}$ is a zero, change the slope from $-20 \mathrm{~dB} / \mathrm{dec}$ back to $-20+$ $20=0 \mathrm{~dB} / \mathrm{dec}$, and continue till the next root at $10^{4} \mathrm{rad} / \mathrm{s}$.
- Since $10^{4} \mathrm{rad} / \mathrm{s}$ is a pole, change the slope to $-20 \mathrm{~dB} / \mathrm{dec}$, and draw the final asymptote accordingly. The final plot is shown in Fig. 6A.3.
image_name:Figure 6A.3
description:The graph in Figure 6A.3 is a Bode plot illustrating the gain in decibels (dB) as a function of frequency in radians per second (rad/s) on a logarithmic scale. The horizontal axis represents frequency, marked in decades from \(10^{-1}\) to \(10^{5}\) rad/s, while the vertical axis represents gain in dB, ranging from 0 to 40 dB.

Overall Behavior and Trends:
- **Initial Region (\(10^{-1}\) to \(10^{0}\) rad/s):** The plot starts at 0 dB and maintains this level until approximately \(10^{0}\) rad/s.
- **Rising Slope (\(10^{0}\) to \(10^{2}\) rad/s):** The gain increases with a slope of +20 dB/dec, rising linearly from 0 dB at \(10^{0}\) rad/s to 40 dB at \(10^{2}\) rad/s.
- **Flat Top (\(10^{2}\) to \(10^{3}\) rad/s):** The gain remains constant at 40 dB across this frequency range.
- **Falling Slope (\(10^{3}\) to \(10^{4}\) rad/s):** The gain decreases with a slope of -20 dB/dec, dropping from 40 dB at \(10^{3}\) rad/s to 20 dB at \(10^{4}\) rad/s.
- **Final Slope (\(10^{4}\) to \(10^{5}\) rad/s):** The gain continues to decrease with a slope of -20 dB/dec, reaching 0 dB at \(10^{5}\) rad/s.

Key Features and Technical Details:
- **Poles and Zeros:** The change in slope at \(10^{0}\), \(10^{3}\), and \(10^{4}\) rad/s indicates the presence of zeros and poles affecting the gain.
- **Asymptotic Behavior:** The plot shows linear asymptotic behavior in the rising and falling regions, typical of Bode plots.

Annotations and Specific Data Points:
- **Slope Changes:** Slope changes occur at \(10^{0}\), \(10^{2}\), \(10^{3}\), and \(10^{4}\) rad/s, indicating critical frequencies where the system's behavior changes due to poles and zeros.

This Bode plot effectively illustrates the frequency response of the system described by Eq. (6A.9), highlighting critical frequency points and changes in gain behavior.

FIGURE 6A. 3 Linearized Bode plot for the gain of Eq. (6A.9)

### Impedance Plots

Just like gain, impedances are plotted using logarithmic scales. However, impedances are expressed in Ohms (not in dBs!), so while the horizontal axis is still marked in frequency decades (or octaves), the vertical axis is now marked in resistance decades (or octaves). To give an idea, consider Fig. 6A.4a, showing the magnitude plots of the impedances

$$
Z_{R}=R=10^{3} \Omega \quad Z_{C}=\frac{1}{j \omega C}=\frac{1}{j \omega 10^{-6}}=-j \frac{10^{6}}{\omega}
$$

The plot of $\left|Z_{R}\right|(=R)$ is just a horizontal line positioned at $10^{3} \Omega$, whereas that of $\left|Z_{C}\right|\left(=10^{6} / \omega\right)$ is a slanted line with a slope of $-(1$ resistance-decade $) /$ (frequencydecade), or simply $-1 \mathrm{dec} / \mathrm{dec}$. Moreover, the two curves intersect each other at $\omega_{0}=1 \mathrm{krad} / \mathrm{s}$.

Knowing the individual plots of $\left|Z_{R}\right|$ and $\left|Z_{C}\right|$, we find it instructive to construct the magnitude plots of their series and parallel combinations $Z_{s}$ and $Z_{p}$ using mere
image_name:(a)
description:
[
name: R, type: Resistor, value: 1 kΩ, ports: {N1: 1, N2: 2}
name: C, type: Capacitor, value: 1 μF, ports: {Np: 2, Nn: 3}
]
extrainfo:The circuit diagram (a) shows a series combination of a resistor and a capacitor. The resistor R has a value of 1 kΩ and the capacitor C has a value of 1 μF. The nodes are labeled as 1, 2, and 3, with the resistor connected between nodes 1 and 2, and the capacitor connected between nodes 2 and 3.
image_name:(b)
description:
[
name: R, type: Resistor, value: 1 kΩ, ports: {N1: Zs, N2: Nn}
name: C, type: Capacitor, value: 1 μF, ports: {Np: Zs, Nn: ''}
]
extrainfo:The circuit diagram (b) represents a series combination of a resistor (1 kΩ) and a capacitor (1 μF). This combination is used to analyze the series impedance Zs.
image_name:(c)
description:
[
name: R, type: Resistor, value: 1 kΩ, ports: {N1: node1, N2: node2}
name: C, type: Capacitor, value: 1 μF, ports: {Np: node1, Nn: node2}
]
extrainfo:The circuit diagram (c) shows a parallel combination of a resistor and a capacitor. The resistor R has a value of 1 kΩ and the capacitor C has a value of 1 μF. The impedance plot for this parallel combination is shown in the graph labeled |Zp|.

FIGURE 6A. 4 Magnitude plots of (a) the individual impedances $Z_{R}$ and $Z_{C}$, (b) their series combination $Z_{s}=Z_{R}+Z_{C}$, and (c) their parallel combination $Z_{p}=Z_{R} / / Z_{C}$.
image_name:Z
description:
[
name: Z1, type: Resistor, value: 100kΩ, ports: {N1: node1, N2: node2}
name: Z2, type: Capacitor, value: 1μF, ports: {Np: node2, Nn: node3}
name: Z3, type: Resistor, value: 1kΩ, ports: {N1: node2, N2: node3}
name: Z4, type: Capacitor, value: 10nF, ports: {Np: node1, Nn: node1}
]
extrainfo:The circuit diagram shows a combination of resistors and capacitors forming a complex impedance network. Z1 and Z4 are in parallel, while Z2 and Z3 are in series and connected in parallel to Z1. The circuit demonstrates impedance characteristics with different frequency responses.

FIGURE 6A. 5 An impedance network.
inspection. To this end, recall that in a series combination the larger of the two impedances dominates, whereas in a parallel combination the smaller of the two dominates. We make the following observations:

- At low frequencies, where $\left|Z_{C}\right| \gg\left|Z_{R}\right|$, we have $Z_{s} \cong Z_{C}$ and $Z_{p} \cong Z_{R}$.
- At high frequencies, where $\left|Z_{C}\right| \ll\left|Z_{R}\right|$, the opposite holds, namely, $Z_{s} \cong Z_{R}$ and $Z_{p} \cong Z_{C}$.
- The individual impedances exhibit equal magnitudes ( $=1 \mathrm{k} \Omega$ in the example) at a special frequency that we shall call $\omega_{0}(=1 \mathrm{krad} / \mathrm{s}$ in the example $)$, so this frequency marks the breakpoint between the low-frequency and the high-frequency asymptotes. Imposing $\left|Z_{C}\left(j \omega_{0}\right)\right|=\left|Z_{R}\right|$, or $1 /\left(\omega_{0} C\right)=R$, we readily find $\omega_{0}=$ $1 /(R C)=1 /\left(10^{3} \times 10^{-6}\right)=1 \mathrm{krad} / \mathrm{s}$. At this frequency we have $\left|Z_{s}\left(j \omega_{0}\right)\right|=R \sqrt{ } 2$ ( $=1.414 \mathrm{k} \Omega$ in our example), and $\left|Z_{p}\left(j \omega_{0}\right)\right|=R / \sqrt{2}(=0.707 \mathrm{k} \Omega$ in the example).

As an additional example, let us apply the above intuitive reasoning to plot the magnitude of the equivalent impedance $Z$ presented by the network of Fig. 6A.5. First, plot the individual impedances as in Fig. 6A.6a. Then, starting at the lowfrequency end and gradually moving toward higher frequencies, construct the plot of $|Z|$ as in Fig 6A.6b, based on the following observations.

- At sufficiently low frequencies, where $Z_{2}$ and $Z_{4}$ act as open circuits, $Z_{1}$ dominates.
- Next, $Z_{2}$ kicks in $\omega=10^{1} \mathrm{rad} / \mathrm{s}$ because $\left|Z_{2}\right|=\left|Z_{1}\right|$ there.
- $Z_{2}$ dominates till $\omega=10^{3} \mathrm{rad} / \mathrm{s}$, where $Z_{3}$ kicks in and dominates till $\omega=$ $10^{5} \mathrm{rad} / \mathrm{s}$.
- At this final point $Z_{4}$ kicks in to dominate for the rest of the frequency spectrum.
image_name:(a)
description:The graph labeled (a) is a Bode plot, specifically a magnitude plot, illustrating the behavior of individual impedances $Z_1$, $Z_2$, $Z_3$, and $Z_4$ over a range of frequencies.

1. **Axes Labels and Units:**
- The x-axis represents frequency ($\omega$) in radians per second (rad/s), spanning from $10^0$ to $10^6$ rad/s on a logarithmic scale.
- The y-axis represents impedance (|Z|) in ohms ($\Omega$), also on a logarithmic scale, ranging from $10^2$ to $10^6$ ohms.

2. **Overall Behavior and Trends:**
- At low frequencies (around $10^0$ rad/s), $Z_1$ is the dominant impedance, with a constant value of $10^5$ ohms.
- As the frequency increases to $10^1$ rad/s, $Z_2$ becomes equal to $Z_1$ and starts to dominate, decreasing linearly on the logarithmic scale until $10^3$ rad/s.
- At $10^3$ rad/s, $Z_3$ takes over, maintaining a constant impedance of $10^3$ ohms until $10^5$ rad/s.
- Beyond $10^5$ rad/s, $Z_4$ becomes the dominant impedance, decreasing linearly on the logarithmic scale.

3. **Key Features and Technical Details:**
- The transition points where each impedance starts to dominate are clearly marked: $10^1$ rad/s for $Z_2$, $10^3$ rad/s for $Z_3$, and $10^5$ rad/s for $Z_4$.
- Each segment of the plot represents a different impedance's dominance over specific frequency ranges.

4. **Annotations and Specific Data Points:**
- The plot includes annotations for each impedance ($Z_1$, $Z_2$, $Z_3$, and $Z_4$), indicating their respective frequency ranges of dominance.
- Significant gridlines are present to help visualize the transitions at the key frequencies mentioned.
image_name:(b)
description:The graph labeled (b) is a Bode plot representing the magnitude of the overall equivalent impedance \( Z \) as a function of frequency in radians per second (rad/s). The plot is logarithmic on both axes, with the x-axis representing frequency ranging from \(10^0\) to \(10^6\) rad/s and the y-axis representing impedance in ohms (\(\Omega\)) ranging from \(10^2\) to \(10^6\) \(\Omega\).

Overall Behavior and Trends:
- **Low Frequencies (\(\omega < 10^1\) rad/s):** The impedance is dominated by \(Z_1\), starting at a high value of approximately \(10^6\) \(\Omega\).
- **Transition at \(\omega = 10^1\) rad/s:** \(Z_2\) becomes significant as it equals \(Z_1\), causing a noticeable decrease in impedance.
- **Mid Frequencies (\(10^1 < \omega < 10^3\) rad/s):** \(Z_2\) dominates, with the impedance decreasing linearly on the logarithmic scale.
- **Transition at \(\omega = 10^3\) rad/s:** \(Z_3\) takes over, further decreasing the impedance.
- **High Frequencies (\(10^3 < \omega < 10^5\) rad/s):** \(Z_3\) is dominant, with a continued linear decrease in impedance.
- **Transition at \(\omega = 10^5\) rad/s:** \(Z_4\) becomes the dominant impedance, stabilizing the decrease.
- **Very High Frequencies (\(\omega > 10^5\) rad/s):** \(Z_4\) dominates, and the impedance levels off.

Key Features:
- **Cutoff Frequencies:** The transitions are marked at \(\omega = 10^1\), \(10^3\), and \(10^5\) rad/s, which are critical points where the dominant impedance changes.
- **Linear Regions:** The impedance decreases linearly on the logarithmic scale in sections dominated by \(Z_2\), \(Z_3\), and \(Z_4\).

Annotations and Specific Data Points:
- The plot includes gridlines that help identify these critical frequencies and the slope of the impedance changes.
- The transitions between different dominating impedances are smooth, indicating gradual changes in the system's behavior across the frequency spectrum.

FIGURE 6A. 6 Magnitude plots of (a) the individual impedances of Fig. 6A.5, and (b) the overall equivalent impedance $Z$.
