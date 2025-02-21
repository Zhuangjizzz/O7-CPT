# Physics of Bipolar Transistors

The bipolar transistor was invented in 1945 by Shockley, Brattain, and Bardeen at Bell Laboratories, subsequently replacing vacuum tubes in electronic systems and paving the way for integrated circuits.

In this chapter, we analyze the structure and operation of bipolar transistors, preparing ourselves for the study of circuits employing such devices. Following the same thought process as in Chapter 2 for $p n$ junctions, we aim to understand the physics of the transistor, derive equations that represent its I/V characteristics, and develop an equivalent model that can be used in circuit analysis and design. The outline below illustrates the sequence of concepts introduced in this chapter.

| Voltage-Controlled |
| :---: |
| Device as |
| Amplifying |
| Element |

| Structure of |
| :---: |
| Bipolar |
| Transistor |

| Operation of |
| :---: |
| Bipolar |
| Transistor |

## 4.1 GENERAL CONSIDERATIONS

In its simplest form, the bipolar transistor can be viewed as a voltage-dependent current source. We first show how such a current source can form an amplifier and hence why bipolar devices are useful and interesting.

Consider the voltage-dependent current source depicted in Fig. 4.1(a), where $I_{1}$ is proportional to $V_{1}: I_{1}=K V_{1}$. Note that $K$ has a dimension of resistance ${ }^{-1}$. For example, with $K=0.001 \Omega^{-1}$, an input voltage of 1 V yields an output current of 1 mA . Let us now construct the circuit shown in Fig. 4.1(b), where a voltage source $V_{\text {in }}$ controls $I_{1}$ and the output current flows through a load resistor $R_{L}$, producing $V_{\text {out }}$. Our objective is to demonstrate that this circuit can operate as an amplifier, i.e., $V_{\text {out }}$ is an amplified replica of $V_{\text {in }}$. Since $V_{1}=V_{\text {in }}$ and $V_{\text {out }}=-R_{L} I_{1}$, we have

$$
\begin{equation*}
V_{\text {out }}=-K R_{L} V_{\text {in }} \tag{4.1}
\end{equation*}
$$

image_name:(a)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
name: I1, type: CurrentSource, ports: {Np: X2, Nn: X1}
name: KV1, type: VoltageControlledVoltageSource, value: KV1, ports: {Np: X2, Nn: X1}
]
extrainfo:The circuit diagram (a) represents a voltage-dependent current source. V1 is the input voltage source, I1 is the current source controlled by V1, and KV1 is a voltage-controlled voltage source connected between nodes X2 and X1.
image_name:(b)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: Vin, Nn: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vout, Nn: GND}
name: KV1, type: VoltageControlledVoltageSource, value: KV1, ports: {Np: Vout, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a simple amplifier where the input voltage Vin controls the current I1. The output voltage Vout is an inverted amplified version of Vin, determined by the equation Vout = -K * RL * Vin. The circuit uses a voltage-controlled voltage source KV1 and a load resistor RL to achieve amplification.
image_name:V_{in} and V_{out} graphs
description:The graph titled "V_{in} and V_{out} graphs" consists of two time-domain waveforms.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform representation, showing the input voltage \( V_{in} \) and the output voltage \( V_{out} \) as functions of time \( t \).

2. **Axes Labels and Units:**
- The horizontal axis represents time \( t \), but specific units are not marked. It is implied to be in a linear scale.
- The vertical axis represents voltage, with the top waveform labeled as \( V_{in} \) and the bottom as \( V_{out} \). Specific voltage units are not marked, but peak values are indicated.

3. **Overall Behavior and Trends:**
- The \( V_{in} \) waveform shows a sinusoidal pattern with a peak voltage labeled as \( V_{p} \).
- The \( V_{out} \) waveform also shows a sinusoidal pattern, maintaining the same frequency as \( V_{in} \) but with a larger amplitude.
- The output waveform \( V_{out} \) is inverted relative to \( V_{in} \), indicating a 180-degree phase shift.

4. **Key Features and Technical Details:**
- The amplitude of \( V_{out} \) is labeled as \( K R_{L} V_{p} \), indicating that the output voltage is an amplified version of the input voltage by a factor of \( K R_{L} \).
- The negative sign in the amplification factor \( -K R_{L} \) suggests that the output is inverted.

5. **Annotations and Specific Data Points:**
- The peak value of \( V_{in} \) is annotated as \( V_{p} \).
- The peak value of \( V_{out} \) is annotated as \( K R_{L} V_{p} \), showing the amplification effect.

Overall, the graph illustrates the concept of amplification with phase inversion, where the output voltage is an amplified and inverted replica of the input voltage.

Figure 4.1 (a) Voltage-dependent current source, (b) simple amplifier.

Interestingly, if $K R_{L}>1$, then the circuit amplifies the input. The negative sign indicates that the output is an "inverted" replica of the input circuit [Fig. 4.1(b)]. The amplification factor or "voltage gain" of the circuit, $A_{V}$, is defined as

$$
\begin{align*}
A_{V} & =\frac{V_{\text {out }}}{V_{\text {in }}}  \tag{4.2}\\
& =-K R_{L} \tag{4.3}
\end{align*}
$$

and depends on both the characteristics of the controlled current source and the load resistor. Note that $K$ signifies how strongly $V_{1}$ controls $I_{1}$, thus directly affecting the gain.
image_name:Fig. 4.2
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: rin, type: Resistor, value: rin, ports: {N1: Vin, N2: Vout}
name: I1, type: VoltageControlledCurrentSource, value: KV1, ports: {Np: Vout, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a voltage-controlled current source with an internal resistance rin. It exhibits a voltage gain determined by the load resistor RL and the control factor K.

Figure 4.2 Voltage-dependent current source with an internal resistance $r_{\text {in }}$.

Solution Since $V_{1}$ is equal to $V_{i n}$ regardless of the value of $r_{i n}$, the voltage gain remains unchanged. This point proves useful in our analyses later.

Exercise Repeat the above example if $r_{i n}=\infty$.

The foregoing study reveals that a voltage-controlled current source can indeed provide signal amplification. Bipolar transistors are an example of such current sources and can ideally be modeled as shown in Fig. 4.3.Note that the device contains three terminals and its output current is an exponential function of $V_{1}$. We will see in Section 4.4.4 that under certain conditions, this model can be approximated by that in Fig. 4.1(a).
image_name:Figure 4.3 Exponential voltage-dependent current source
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: 1, Nn: 2}
name: I_S exp(V1/V_T), type: CurrentSource, ports: {Np: 3, Nn: 2}
]
extrainfo:The circuit is an exponential voltage-dependent current source, which models a voltage-controlled current source. It includes a voltage source V1 and a current source with an exponential relationship to V1.

Figure 4.3 Exponential voltage-dependent current source.

As three-terminal devices, bipolar transistors make the analysis of circuits more difficult. Having dealt with two-terminal components such as resistors, capacitors, inductors, and diodes in elementary circuit analysis and the previous chapters of this book, we are accustomed to a one-to-one correspondence between the current through and the voltage across each device. With three-terminal elements, on the other hand, one may consider the current and voltage between every two terminals, arriving at a complex set of equations. Fortunately, as we develop our understanding of the transistor's operation, we discard some of these current and voltage combinations as irrelevant, thus obtaining a relatively simple model.

## 4.2 STRUCTURE OF BIPOLAR TRANSISTOR

The bipolar transistor consists of three doped regions forming a sandwich. Shown in Fig. 4.4(a) is an example comprising of a $p$ layer sandwiched between two $n$ regions and called an "npn" transistor. The three terminals are called the "base," the "emitter," and the "collector." As explained later, the emitter "emits" charge carriers and the collector "collects" them while the base controls the number of carriers that make this journey. The circuit symbol for the $n p n$ transistor is shown in Fig. 4.4(b). We denote the terminal voltages by $V_{E}, V_{B}$, and $V_{C}$, and the voltage differences by $V_{B E}, V_{C B}$, and $V_{C E}$. The transistor is labeled $Q_{1}$ here.
image_name:(a)
description:The image consists of two parts labeled (a) and (b), representing the structure and circuit symbol of an NPN bipolar transistor, respectively.

1. **Identification of Components and Structure:**
- **Figure 4.4(a):** This part shows the physical structure of an NPN transistor. It consists of three layers: an n-type layer at the top (Collector), a p-type layer in the middle (Base), and another n-type layer at the bottom (Emitter). The layers are stacked vertically, with the Collector and Emitter at opposite ends and the Base in between.
- **Figure 4.4(b):** This part displays the circuit symbol of an NPN transistor labeled as Q1. It includes three terminals: the Base (B), Collector (C), and Emitter (E).

2. **Connections and Interactions:**
- In the circuit symbol (b), the arrow on the Emitter indicates the direction of conventional current flow, pointing outward, which is characteristic of an NPN transistor.
- The Base controls the flow of charge carriers between the Collector and Emitter.

3. **Labels, Annotations, and Key Features:**
- **Figure 4.4(b):** Voltage differences are labeled as V_BE (Base-Emitter voltage), V_CB (Collector-Base voltage), and V_CE (Collector-Emitter voltage). Positive and negative signs indicate the polarity of these voltages.
- The transistor is labeled as Q1, indicating its designation in a circuit.
- The physical structure diagram in (a) visually represents the two PN junctions: one between the Base and Emitter and another between the Base and Collector.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: Collector, B: Base, E: Emitter}
]
extrainfo:The circuit diagram shows the symbol and structure of an NPN transistor labeled Q1. It includes nodes for Collector (C), Base (B), and Emitter (E). Voltage differences V_CB, V_BE, and V_CE are indicated.

Figure 4.4 (a) Structure and (b) circuit symbol of bipolar transistor.
We readily note from Fig. 4.4(a) that the device contains two $p n$ junction diodes: one between the base and the emitter and another between the base and the collector. For example, if the base is more positive than the emitter, $V_{B E}>0$, then this junction is forward-biased. While this simple diagram may suggest that the device is symmetric with
respect to the emitter and the collector, in reality, the dimensions and doping levels of these two regions are quite different. In other words, $E$ and $C$ cannot be interchanged. We will also see that proper operation requires a thin base region, e.g., about $100 \AA$ in modern integrated bipolar transistors.

As mentioned in the previous section, the possible combinations of voltages and currents for a three-terminal device can prove overwhelming. For the device in Fig. 4.4(a), $V_{B E}, V_{B C}$, and $V_{C E}$ can assume positive or negative values, leading to $2^{3}$ possibilities for the terminal voltages of the transistor. Fortunately, only one of these eight combinations finds practical value and comes into our focus here.

Before continuing with the bipolar transistor, it is instructive to study an interesting effect in pn junctions. Consider the reverse-biased junction depicted in Fig. 4.5(a) and recall from Chapter 2 that the depletion region sustains a strong electric field. Now suppose an electron is somehow "injected" from outside into the right side of the depletion region. What happens to this electron? Serving as a minority carrier on the $p$ side, the electron experiences the electric field and is rapidly swept away into the $n$ side. The ability of a reverse-biased $p n$ junction to efficiently "collect" externally-injected electrons proves essential to the operation of the bipolar transistor.
image_name:Figure 4.5 Injection of electrons into depletion region.
description:
[
name: VR, type: VoltageSource, value: VR, ports: {Np: X2, Nn: X1}
]
extrainfo:The diagram shows a reverse-biased p-n junction with an electric field E across the depletion region. An electron is injected from outside into the depletion region on the p-side, where it is swept across to the n-side by the electric field. This setup is essential for the operation of a bipolar transistor in active mode, where externally injected electrons are collected efficiently.

Figure 4.5 Injection of electrons into depletion region.

## 4.3 OPERATION OF BIPOLAR TRANSISTOR IN ACTIVE MODE

In this section, we analyze the operation of the transistor, aiming to prove that, under certain conditions, it indeed acts as a voltage-controlled current source. More specifically, we intend to show that (a) the current flow from the emitter to the collector can be viewed as a current source tied between these two terminals, and (b) this current is controlled by the voltage difference between the base and the emitter, $V_{B E}$.

We begin our study with the assumption that the base-emitter junction is forwardbiased $\left(V_{B E}>0\right)$ and the base-collector junction is reverse-biased $\left(V_{B C}<0\right)$. Under these conditions, we say the device is biased in the "forward active region" or simply in the "active mode." For example, with the emitter connected to ground, the base voltage is set to about 0.8 V and the collector voltage to a higher value, e.g., 1 V [Fig. 4.6(a)]. The base-collector junction therefore experiences a reverse bias of 0.2 V .

Let us now consider the operation of the transistor in the active mode. We may be tempted to simplify the example of Fig. 4.6(a) to the equivalent circuit shown in Fig. 4.6(b). After all, it appears that the bipolar transistor simply consists of two diodes sharing their
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: VCE, B: VBE, E: GND}
name: D1, type: Diode, ports: {Na: VBE, Nc: GND}
name: D2, type: Diode, ports: {Na: VCE, Nc: VBE}
name: VBE, type: VoltageSource, value: +0.8V, ports: {Np: VBE, Nn: GND}
name: VCE, type: VoltageSource, value: +1V, ports: {Np: VCE, Nn: GND}
]
extrainfo:The circuit diagram (a) shows a bipolar NPN transistor with bias voltages applied to the base and collector. The base-emitter voltage is set to +0.8V and the collector-emitter voltage is set to +1V, reverse-biasing the base-collector junction by 0.2V.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: VCE, B: VBE, E: GND}
name: D1, type: Diode, ports: {Na: VBE, Nc: GND}
name: D2, type: Diode, ports: {Na: VCE, Nc: VBE}
name: VBE, type: VoltageSource, value: +0.8V, ports: {Np: VBE, Nn: GND}
name: VCE, type: VoltageSource, value: +1V, ports: {Np: VCE, Nn: GND}
]
extrainfo:The circuit diagram (b) represents a simplistic view of a bipolar transistor with diodes D1 and D2 illustrating the base-emitter and base-collector junctions. Voltage sources VBE and VCE provide the biasing for the base-emitter and collector-emitter junctions respectively.

Figure 4.6 (a) Bipolar transistor with base and collector bias voltages, (b) simplistic view of bipolar transistor.
anodes at the base terminal. This view implies that $D_{1}$ carries a current and $D_{2}$ does not; i.e., we should anticipate current flow from the base to the emitter but no current through the collector terminal. Were this true, the transistor would not operate as a voltage-controlled current source and would prove of little value.

To understand why the transistor cannot be modeled as merely two back-to-back diodes, we must examine the flow of charge inside the device, bearing in mind that the base region is very thin. Since the base-emitter junction is forward-biased, electrons flow from the emitter to the base and holes from the base to the emitter. For proper transistor operation, the former current component must be much greater than the latter, requiring that the emitter doping level be much greater than that of the base (Chapter 2). Thus, we denote the emitter region with $n^{+}$, where the superscript emphasizes the high doping level. Figure 4.7(a) summarizes our observations thus far, indicating that the emitter
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: VCE, B: VBE, E: GND}
name: VBE, type: VoltageSource, value: +0.8V, ports: {Np: VBE, Nn: GND}
name: VCE, type: VoltageSource, value: +1V, ports: {Np: VCE, Nn: GND}
]
extrainfo:The circuit diagram (a) illustrates the flow of electrons and holes in an NPN transistor. The emitter is heavily doped (n+) and injects electrons into the base (p), which then move towards the collector (n). The base-emitter junction is forward-biased with VBE = +0.8V, and the collector-emitter junction is reverse-biased with VCE = +1V.
image_name:(b)
description:
[
name: VBE, type: VoltageSource, value: +0.8V, ports: {Np: B, Nn: GND}
name: VCE, type: VoltageSource, value: +1V, ports: {Np: C, Nn: GND}
]
extrainfo:The diagram (b) shows a transistor with a base-emitter voltage VBE of +0.8V and a collector-emitter voltage VCE of +1V. Electrons flow from the n+ emitter through the p base to the n collector, with a depletion region at the collector-base junction.
image_name:(c)
description:
[

]
extrainfo:The diagram illustrates the flow of electrons and holes in a bipolar junction transistor (BJT) during operation. The emitter-base junction is forward-biased with V_BE = +0.8 V, and the collector-emitter junction is reverse-biased with V_CE = +1 V. Electrons flow from the emitter (n+) to the base (p) and then to the collector (n), while holes flow from the base to the emitter. The image depicts the depletion region at the collector-base junction, which facilitates the movement of electrons towards the collector.

Figure 4.7 (a) Flow of electrons and holes through base-emitter junction, (b) electrons approaching collector junction, (c) electrons passing through collector junction.
injects a large number of electrons into the base while receiving a small number of holes from it.

What happens to electrons as they enter the base? Since the base region is thin, most of the electrons reach the edge of the collector-base depletion region, beginning to experience the built-in electric field. Consequently, as illustrated in Fig. 4.5, the electrons are swept into the collector region (as in Fig. 4.5) and absorbed by the positive battery terminal. Figures 4.7(b) and (c) illustrate this effect in "slow motion." We therefore observe that the reverse-biased collector-base junction carries a current because minority carriers are "injected" into its depletion region.

Let us summarize our thoughts. In the active mode, an npn bipolar transistor carries a large number of electrons from the emitter, through the base, to the collector while drawing a small current of holes through the base terminal. We must now answer several questions. First, how do electrons travel through the base: by drift or diffusion? Second, how does the resulting current depend on the terminal voltages? Third, how large is the base current?

Operating as a moderate conductor, the base region sustains but a small electric field, i.e., it allows most of the field to drop across the base-emitter depletion layer. Thus, as explained for $p n$ junctions in Chapter 2, the drift current in the base is negligible, ${ }^{1}$ leaving diffusion as the principal mechanism for the flow of electrons injected by the emitter. In fact, two observations directly lead to the necessity of diffusion: (1) redrawing the diagram of Fig. 2.29 for the emitter-base junction [Fig. 4.8(a)], we recognize that the density of electrons at $x=x_{1}$ is very high; (2) since any electron arriving at $x=x_{2}$ in Fig. 4.8(b) is swept away, the density of electrons falls to zero at this point. As a result,
image_name:(a)
description:
[
name: V_BE, type: VoltageSource, ports: {Np: GND, Nn: GND}
name: V_CE, type: VoltageSource, ports: {Np: GND, Nn: GND}
]
extrainfo:The diagram shows the electron and hole profiles across the base-emitter and base-collector junctions of a bipolar junction transistor (BJT). The base-emitter junction is forward-biased, and the base-collector junction is reverse-biased. The electron density profile indicates a gradient for diffusion from the emitter to the collector.
image_name:(b)
description:
[
name: V_BE, type: VoltageSource, value: V_BE, ports: {Np: GND, Nn: Base}
name: V_CE, type: VoltageSource, value: V_CE, ports: {Np: Collector, Nn: GND}
]
extrainfo:The circuit diagram (b) represents a reverse-biased collector-base junction in a bipolar junction transistor (BJT). The electron density is zero at x2, indicating that electrons are swept away at this point.
image_name:(c)
description:The graph in Figure 4.8(c) illustrates the electron density profile within the base of a bipolar junction transistor (BJT). The x-axis represents the position within the base, denoted as \( x \), with two specific points marked: \( x_1 \) and \( x_2 \). The y-axis represents the electron density, though specific units are not provided, the trend is depicted qualitatively.

Type of Graph and Function:
This is a qualitative spatial distribution graph showing the electron density within the base of a BJT. It is not a traditional function graph with numerical data but rather a conceptual diagram.

Axes Labels and Units:
- **X-axis:** Position \( x \) within the base, with specific points \( x_1 \) and \( x_2 \) marked.
- **Y-axis:** Electron density (qualitative, no units specified).

Overall Behavior and Trends:
The graph shows a linear increase in electron density from \( x_1 \) to \( x_2 \). At \( x_1 \), the electron density is higher due to the injection from the emitter, and it decreases linearly towards \( x_2 \) where the density approaches zero. This gradient indicates the diffusion of electrons across the base.

Key Features and Technical Details:
- **Point \( x_1 \):** High electron density due to injection from the emitter.
- **Point \( x_2 \):** Electron density approaches zero as electrons are swept away by the electric field towards the collector.
- **Gradient:** The linear decrease represents the diffusion of electrons, which is the primary mechanism for electron flow in the base.

Annotations and Specific Data Points:
- The graph is annotated with an arrow indicating the direction of electron diffusion from \( x_1 \) to \( x_2 \). This reflects the movement of electrons due to the concentration gradient within the base.

In summary, the graph in Figure 4.8(c) conceptually illustrates the diffusion-driven electron density profile within the base of a BJT, highlighting the decrease in density from \( x_1 \) to \( x_2 \) as electrons diffuse and are collected.

Figure 4.8 (a) Hole and electron profiles at base-emitter junction, (b) zero electron density near collector, (c) electron profile in base.

[^14]the electron density in the base assumes the profile depicted in Fig. 4.8(c), providing a gradient for the diffusion of electrons.

### 4.3.1 Collector Current

We now address the second question raised previously and compute the current flowing from the collector to the emitter. ${ }^{2}$ As a forward-biased diode, the base-emitter junction exhibits a high concentration of electrons at $x=x_{1}$ in Fig. 4.8(c) given by Eq. (2.96):

$$
\begin{align*}
\Delta n\left(x_{1}\right) & =\frac{N_{E}}{\exp \frac{V_{0}}{V_{T}}}\left(\exp \frac{V_{B E}}{V_{T}}-1\right)  \tag{4.4}\\
& =\frac{N_{B}}{n_{i}^{2}}\left(\exp \frac{V_{B E}}{V_{T}}-1\right) \tag{4.5}
\end{align*}
$$

Here, $N_{E}$ and $N_{B}$ denote the doping levels in the emitter and the base, respectively, and we have utilized the relationship $\exp \left(V_{0} / V_{T}\right)=N_{E} N_{B} / n_{i}^{2}$. In this chapter, we assume $V_{T}=26 \mathrm{mV}$. Applying the law of diffusion [Eq. (2.42)], we determine the flow of electrons into the collector as

$$
\begin{align*}
J_{n} & =q D_{n} \frac{d n}{d x}  \tag{4.6}\\
& =q D_{n} \cdot \frac{0-\Delta n\left(x_{1}\right)}{W_{B}} \tag{4.7}
\end{align*}
$$

where $W_{B}$ is the width of the base region. Multipling this quantity by the emitter cross section area, $A_{E}$, substituting for $\Delta n\left(x_{1}\right)$ from Eq. (4.5), and changing the sign to obtain the conventional current, we obtain

$$
\begin{equation*}
I_{C}=\frac{A_{E} q D_{n} n_{i}^{2}}{N_{B} W_{B}}\left(\exp \frac{V_{B E}}{V_{T}}-1\right) \tag{4.8}
\end{equation*}
$$

In analogy with the diode current equation and assuming $\exp \left(V_{B E} / V_{T}\right) \gg 1$, we write

$$
\begin{equation*}
I_{C}=I_{S} \exp \frac{V_{B E}}{V_{T}} \tag{4.9}
\end{equation*}
$$

where

$$
\begin{equation*}
I_{S}=\frac{A_{E} q D_{n} n_{i}^{2}}{N_{B} W_{B}} \tag{4.10}
\end{equation*}
$$

Equation (4.9) implies that the bipolar transistor indeed operates as a voltagecontrolled current source, proving a good candidate for amplification. We may alternatively say the transistor performs "voltage-to-current conversion."

[^15]Example 4.2

Determine the current $I_{X}$ in Fig. 4.9(a) if $Q_{1}$ and $Q_{2}$ are identical and operate in the active mode and $V_{1}=V_{2}$.
image_name:Fig. 4.9(a)
description:
[
name: Q1, type: NPN, ports: {C: V3, B: V1, E: GND}
name: Q2, type: NPN, ports: {C: V3, B: V2, E: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
name: V2, type: VoltageSource, value: V2, ports: {Np: V2, Nn: GND}
name: V3, type: VoltageSource, value: V3, ports: {Np: V3, Nn: GND}
]
extrainfo:The circuit consists of two identical NPN transistors (Q1 and Q2) connected in parallel, sharing the same collector node (V3). The emitters are grounded, and each base is connected to separate voltage sources (V1 and V2). The circuit is designed to sum the collector currents (IC1 and IC2) to produce the output current IX at node V3.

(a)
image_name:(a)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
name: V3, type: VoltageSource, value: V3, ports: {Np: V3, Nn: GND}
name: Q1, type: NPN, ports: {C: V3, B: V1, E: GND}
name: Q2, type: NPN, ports: {C: V3, B: V2, E: GND}
name: Qeq, type: NPN, ports: {C: V3, B: V1, E: GND}
]
extrainfo:The circuit consists of two identical NPN transistors (Q1 and Q2) connected in parallel, sharing the same collector node (V3). The emitters are grounded, and each base is connected to separate voltage sources (V1 and V2). The circuit is designed to sum the collector currents (IC1 and IC2) to produce the output current IX at node V3. The equivalent circuit shows a single transistor (Qeq) with twice the emitter area (2AE), representing the combined effect of Q1 and Q2.
image_name:(b)
description:The image presents a conceptual diagram illustrating the equivalence of two identical NPN transistors to a single larger transistor. **

1. **Identification of Components and Structure:**
- The left side of the diagram shows two NPN transistors, labeled as Q1 and Q2, connected in parallel. Each transistor has its collector connected to a common node labeled V3, which serves as the output node for the summed collector currents (IC1 and IC2).
- The bases of Q1 and Q2 are connected to separate voltage sources, V1 and V2, respectively, while their emitters are grounded (GND).
- On the right side, the diagram simplifies this configuration by showing a single equivalent transistor, labeled Qeq, with an emitter area of 2AE, which is twice that of the individual transistors.

2. **Connections and Interactions:**
- In the parallel configuration, the collector currents IC1 and IC2 from Q1 and Q2 are summed at node V3 to produce the output current IX. This is represented by arrows indicating the direction of current flow.
- The equivalent transistor (Qeq) is shown to have a single base connection to V1, a collector connection to V3, and a grounded emitter, similar to the original configuration but with a doubled emitter area to account for the combined effect of Q1 and Q2.

3. **Labels, Annotations, and Key Features:**
- The diagram includes labels for the voltage sources (V1, V2, and V3), ground connections (GND), and current paths (IC1, IC2, IX).
- The notation 2AE highlights the increased emitter area of the equivalent transistor, reflecting the summation of the two original transistors' areas.
- The transition from the two-transistor configuration to the single-transistor equivalent is visually represented by arrows and a simplified schematic diagram on the right.

Overall, the image effectively communicates the concept of equivalently replacing two parallel transistors with a single transistor of larger area to achieve the same electrical behavior.

(b)

Figure 4.9 (a) Two identical transistors drawing current from $V_{C}$, (b) equivalence to a single transistor having twice the area.

Solution $\quad$ Since $I_{X}=I_{C 1}+I_{C 2}$, we have

$$
\begin{equation*}
I_{X} \approx 2 \frac{A_{E} q D_{n} n_{i}^{2}}{N_{B} W_{B}} \exp \frac{V_{1}}{V_{T}} \tag{4.11}
\end{equation*}
$$

This result can also be viewed as the collector current of a single transistor having an emitter area of $2 A_{E}$. In fact, redrawing the circuit as shown in Fig. 4.9(b) and noting that $Q_{1}$ and $Q_{2}$ experience identical voltages at their respective terminals, we say the two transistors are "in parallel," operating as a single transistor with twice the emitter area of each.

Exercise Repeat the above example if $Q_{1}$ has an emitter area of $A_{E}$ and $Q_{2}$ an emitter area of $8 A_{E}$.

Example In the circuit of Fig. 4.9 (a), $Q_{1}$ and $Q_{2}$ are identical and operate in the active mode.
4.3 Determine $V_{1}-V_{2}$ such that $I_{C 1}=10 I_{C 2}$.

Solution From Eq. (4.9), we have

$$
\begin{equation*}
\frac{I_{C 1}}{I_{C 2}}=\frac{I_{S} \exp \frac{V_{1}}{V_{T}}}{I_{S} \exp \frac{V_{2}}{V_{T}}} \tag{4.12}
\end{equation*}
$$

and hence

$$
\begin{equation*}
\exp \frac{V_{1}-V_{2}}{V_{T}}=10 \tag{4.13}
\end{equation*}
$$

That is,

$$
\begin{align*}
V_{1}-V_{2} & =V_{T} \ln 10  \tag{4.14}\\
& \approx 60 \mathrm{mV} \text { at } T=300 \mathrm{~K} \tag{4.15}
\end{align*}
$$

Identical to Eq. (2.109), this result is, of course, expected because the exponential dependence of $I_{C}$ upon $V_{B E}$ indicates a behavior similar to that of diodes. We therefore consider the base-emitter voltage of the transistor relatively constant and approximately equal to 0.8 V for typical collector current levels.

Exercise $\quad$ Repeat the above example if $Q_{1}$ and $Q_{2}$ have different emitter areas, i.e., $A_{E 1}=n A_{E 2}$.

Example Typical discrete bipolar transistors have a large area, e.g., $500 \mu \mathrm{~m} \times 500 \mu \mathrm{~m}$, whereas
4.4 modern integrated devices may have an area as small as $0.5 \mu \mathrm{~m} \times 0.2 \mu \mathrm{~m}$. Assuming other device parameters are identical, determine the difference between the base-emitter voltage of two such transistors for equal collector currents.

Solution From Eq. (4.9), we have $V_{B E}=V_{T} \ln \left(I_{C} / I_{S}\right)$ and hence

$$
\begin{equation*}
V_{B E i n t}-V_{B E d i s}=V_{T} \ln \frac{I_{S 1}}{I_{S 2}} \tag{4.16}
\end{equation*}
$$

where $V_{B E i n t}=V_{T} \ln \left(I_{C 2} / I_{S 2}\right)$ and $V_{B E d i s}=V_{T} \ln \left(I_{C 1} / I_{S 1}\right)$ denote the base-emitter voltages of the integrated and discrete devices, respectively. Since $I_{S} \propto A_{E}$,

$$
\begin{equation*}
V_{B E i n t}-V_{B E d i s}=V_{T} \ln \frac{A_{E 2}}{A_{E 1}} \tag{4.17}
\end{equation*}
$$

For this example, $A_{E 2} / A_{E 1}=2.5 \times 10^{6}$, yielding

$$
\begin{equation*}
V_{\text {BEint }}-V_{\text {BEdis }}=383 \mathrm{mV} \tag{4.18}
\end{equation*}
$$

In practice, however, $V_{\text {BEint }}-V_{\text {BEdis }}$ falls in the range of 100 to 150 mV because of differences in the base width and other parameters. The key point here is that $V_{B E}=800 \mathrm{mV}$ is a reasonable approximation for integrated transistors and should be lowered to about 700 mV for discrete devices.

Exercise Repeat the above comparison for a very small integrated device with an emitter area of $0.15 \mu \mathrm{~m} \times 0.15 \mu$.

Since many applications deal with voltage quantities, the collector current generated by a bipolar transistor typically flows through a resistor to produce a voltage.
image_name:Figure 4.10
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: 750mV, E: GND}
name: RL, type: Resistor, value: 1kΩ, ports: {N1: V1, N2: Vout}
name: V1, type: VoltageSource, value: 3V, ports: {Np: V1, Nn: GND}
name: V2, type: VoltageSource, value: 750mV, ports: {Np: 750mV, Nn: GND}
]
extrainfo:The circuit is a simple stage with biasing using an NPN transistor. The collector current IC is 1.69 mA, and the output voltage Vout is calculated to be 1.31 V using the given parameters.

Exercise What happens if the load resistor is halved?

Equation (4.9) reveals an interesting property of the bipolar transistor: the collector current does not depend on the collector voltage (so long as the device remains in the active mode). Thus, for a fixed base-emitter voltage, the device draws a constant current, acting as a current source [Fig. 4.11(a)]. Plotted in Fig. 4.11(b) is the current as a function of the collector-emitter voltage, exhibiting a constant value for $V_{C E}>V_{1}{ }^{3}$ Constant current sources find application in many electronic circuits and we will see numerous examples of their usage in this book. In Section 4.5, we study the behavior of the transistor for $V_{C E}<V_{B E}$.
image_name:Figure 4.11 (a)
description:
[
name: Q1, type: NPN, ports: {C: LOAD, B: Vi, E: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: Vi, Nn: GND}
]
extrainfo:The circuit diagram shows an NPN transistor (Q1) configured as a current source, with the collector connected to the LOAD and the emitter grounded. The base is driven by a voltage source (V1), which establishes the base-emitter voltage.
image_name:Figure 4.11 (b)
description:The graph in Figure 4.11(b) is an I/V characteristic plot for a bipolar transistor used as a current source. It shows the relationship between the collector current (I_C) on the vertical axis and the collector-emitter voltage (V_CE) on the horizontal axis.

1. **Type of Graph and Function:**
- This is a characteristic curve graph, specifically illustrating the behavior of a bipolar transistor in its forward active region.

2. **Axes Labels and Units:**
- The vertical axis is labeled as I_C, representing the collector current. The horizontal axis is labeled as V_CE, representing the collector-emitter voltage.
- The units are not explicitly mentioned, but typically, I_C would be in amperes (A) and V_CE in volts (V).

3. **Overall Behavior and Trends:**
- The graph shows a constant collector current (I_C) once the collector-emitter voltage (V_CE) exceeds a certain threshold value (V_1).
- For V_CE greater than V_1, the current remains constant, indicating the transistor is in the forward active region.
- This behavior demonstrates the transistor acting as a constant current source.

4. **Key Features and Technical Details:**
- The constant current level is given by the expression I_S * exp(V_1 / V_T), where I_S is the saturation current and V_T is the thermal voltage.
- The threshold voltage V_1 is a critical point where the transition to the constant current region begins.
- The region labeled as 'Forward Active Region' indicates where the transistor operates as a current source.

5. **Annotations and Specific Data Points:**
- The graph includes a reference line marking the constant current level in the forward active region.
- The point V_1 on the V_CE axis marks the beginning of the constant current behavior.
- No other specific numerical values or annotations are provided on the graph.

Figure 4.11 (a) Bipolar transistor as a current source, (b) I/V characteristic.

### 4.3.2 Base and Emitter Currents

Having determined the collector current, we now turn our attention to the base and emitter currents and their dependence on the terminal voltages. Since the bipolar transistor must satisfy Kirchoff's current law, calculation of the base current readily yields the emitter current as well.

[^16]image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: VCE, B: VBE, E: GND}
name: VBE, type: VoltageSource, value: VBE, ports: {Np: VBE, Nn: GND}
name: VCE, type: VoltageSource, value: VCE, ports: {Np: VCE, Nn: GND}
]
extrainfo:The diagram shows an NPN transistor used as a current source. The collector is connected to VCE, the base to VBE, and the emitter to GND. The currents IC, IB, and IE are labeled, indicating the flow of electrons and holes.
image_name:(b)
description:
[
name: V_BE, type: VoltageSource, value: V_BE, ports: {Np: V_BE, Nn: GND}
name: V_CE, type: VoltageSource, value: V_CE, ports: {Np: V_CE, Nn: GND}
]
extrainfo:The diagram (b) shows an NPN transistor with base-emitter voltage (V_BE) and collector-emitter voltage (V_CE). The base current (I_B) results from holes crossing to the emitter, and the collector current (I_C) is shown flowing from the collector to the emitter. The emitter current (I_E) flows to ground.

Figure 4.12 Base current resulting from holes (a) crossing to emitter and (b) recombining with electrons.

In the npn transistor of Fig. 4.12 (a), the base current, $I_{B}$, results from the flow of holes. Recall from Eq. (2.99) that the hole and electron currents in a forward-biased pn junction bear a constant ratio given by the doping levels and other parameters. Thus, the number of holes entering from the base to the emitter is a constant fraction of the number of electrons traveling from the emitter to the base. As an example, for every 200 electrons injected by the emitter, one hole must be supplied by the base.

In practice, the base current contains an additional component of holes. As the electrons injected by the emitter travel through the base, some may "recombine" with the holes [Fig. 4.12 (b)]; inessence, some electrons and holes are "wasted" as a result of recombination. For example, on the average, out of every 200 electrons injected by the emitter, one recombines with a hole.

In summary, the base current must supply holes for both reverse injection into the emitter and recombination with the electrons traveling toward the collector. We can therefore view $I_{B}$ as a constant fraction of $I_{E}$ or a constant fraction of $I_{C}$. It is common to write

$$
\begin{equation*}
I_{C}=\beta I_{B}, \tag{4.20}
\end{equation*}
$$

where $\beta$ is called the "current gain" of the transistor because it shows how much the base current is "amplified." Depending on the device structure, the $\beta$ of $n p n$ transistors typically ranges from 50 to 200.

In order to determine the emitter current, we apply the KCL to the transistor with the current directions depicted in Fig. 4.12 (a):

$$
\begin{align*}
I_{E} & =I_{C}+I_{B}  \tag{4.21}\\
& =I_{C}\left(1+\frac{1}{\beta}\right) . \tag{4.22}
\end{align*}
$$

We can summarize our findings as follows:

$$
\begin{align*}
I_{C} & =I_{S} \exp \frac{V_{B E}}{V_{T}}  \tag{4.23}\\
I_{B} & =\frac{1}{\beta} I_{S} \exp \frac{V_{B E}}{V_{T}}  \tag{4.24}\\
I_{E} & =\frac{\beta+1}{\beta} I_{S} \exp \frac{V_{B E}}{V_{T}} . \tag{4.25}
\end{align*}
$$

It is sometimes useful to write $I_{C}=[\beta /(\beta+1)] I_{E}$ and denote $\beta /(\beta+1)$ by $\alpha$. For $\beta=100$, $\alpha=0.99$, suggesting that $\alpha \approx 1$ and $I_{C} \approx I_{E}$ are reasonable approximations. In this book, we assume that the collector and emitter currents are approximately equal.

Example
4.6

A bipolar transistor having $I_{S}=5 \times 10^{-16} \mathrm{~A}$ is biased in the forward active region with $V_{B E}=750 \mathrm{mV}$. If the current gain varies from 50 to 200 due to manufacturing variations, calculate the minimum and maximum terminal currents of the device.

Solution For a given $V_{B E}$, the collector current remains independent of $\beta$ :

$$
\begin{align*}
I_{C} & =I_{S} \exp \frac{V_{B E}}{V_{T}}  \tag{4.26}\\
& =1.685 \mathrm{~mA} \tag{4.27}
\end{align*}
$$

The base current varies from $I_{C} / 200$ to $I_{C} / 50$ :

$$
\begin{equation*}
8.43 \mu \mathrm{~A}<I_{B}<33.7 \mu \mathrm{~A} \tag{4.28}
\end{equation*}
$$

On the other hand, the emitter current experiences only a small variation because $(\beta+1) / \beta$ is near unity for large $\beta$ :

$$
\begin{align*}
1.005 I_{C} & <I_{E}<1.02 I_{C}  \tag{4.29}\\
1.693 \mathrm{~mA} & <I_{E}<1.719 \mathrm{~mA} \tag{4.30}
\end{align*}
$$

Exercise Repeat the above example if the area of the transistor is doubled.

## 4.4 BIPOLAR TRANSISTOR MODELS AND CHARACTERISTICS

### 4.4.1 Large-Signal Model

With our understanding of the transistor operation in the forward active region and the derivation of Eqs. (4.23)-(4.25), we can now construct a model that proves useful in the analysis and design of circuits-in a manner similar to the developments in Chapter 2 for the $p n$ junction.

Since the base-emitter junction is forward-biased in the active mode, we can place a diode between the base and emit-

Did you know?

The first bipolar transistor introduced by Bell Labs in 1948 was implemented in germanium rather than silicon, had a base thickness of about $30 \mu \mathrm{~m}$, and provided a maximum operation frequency (called the "transit frequency") of 10 MHz . By contrast, bipolar transistors realized in today's silicon integrated circuits have a base thickness less than $0.01 \mu \mathrm{~m}$ and a transit frequency of several hundred gigahertz.
ter terminals. Moreover, since the current drawn from the collector and flowing into the emitter depends on only the base-emitter voltage, we add a voltage-controlled current source between the collector and the emitter, arriving at the model shown in Fig. 4.13. As illustrated in Fig. 4.11, this current remains independent of the collector-emitter voltage.
image_name:Figure 4.13 Large-signal model of bipolar transistor in active region
description:
[
name: Q1, type: NPN, ports: {C: C, B: B, E: E}
name: D1, type: Diode, ports: {Na: B, Nc: E}
name: I1, type: CurrentSource, ports: {Np: C, Nn: E}
]
extrainfo:The circuit is a large-signal model of a bipolar transistor in the active region. It includes a bipolar junction transistor (BJT) represented by an NPN, a diode modeling the base-emitter junction, and a current source modeling the collector current.

Figure 4.13 Large-signal model of bipolar transistor in active region.

But how do we ensure that the current flowing through the diode is equal to $1 / \beta$ times the collector current? Equation (4.24) suggests that the base current is equal to that of a diode having a reverse saturation current of $I_{S} / \beta$. Thus, the base-emitter junction is modeled by a diode whose cross section area is $1 / \beta$ times that of the actual emitter area.

With the interdependencies of currents and voltages in a bipolar transistor, the reader may wonder about the cause and effect relationships. We view the chain of dependencies as $V_{B E} \rightarrow I_{C} \rightarrow I_{B} \rightarrow I_{E}$; i.e., the base-emitter voltage generates a collector current, which requires a proportional base current, and the sum of the two flows through the emitter.

Example
4.7

Consider the circuit shown in Fig. 4.14 (a), where $I_{S, Q 1}=5 \times 10^{-17} \mathrm{~A}$ and $V_{B E}=$ 800 mV . Assume $\beta=100$. (a) Determine the transistor terminal currents and voltages and verify that the device indeed operates in the active mode. (b) Determine the maximum value of $R_{C}$ that permits operation in the active mode.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: X, B: VBE, E: GND}
name: RC, type: Resistor, value: 500Ω, ports: {N1: VCC, N2: X}
name: VBE, type: VoltageSource, value: VBE, ports: {Np: VBE, Nn: GND}
name: VCC, type: VoltageSource, value: 2V, ports: {Np: VCC, Nn: GND}
]
extrainfo:The circuit is a basic NPN transistor amplifier with a biasing network. It includes a collector resistor RC and a voltage source VBE for base-emitter biasing. The collector voltage is influenced by the resistor RC connected to VCC.

(a)
(b)

Figure 4.14 (a) Simple stage with biasing, (b) variation of collector voltage as a function of collector resistance.

Solution (a) Using Eq. (4.23)-(4.25), we have

$$
\begin{align*}
I_{C} & =1.153 \mathrm{~mA}  \tag{4.31}\\
I_{B} & =11.53 \mu \mathrm{~A}  \tag{4.32}\\
I_{E} & =1.165 \mathrm{~mA} . \tag{4.33}
\end{align*}
$$

The base and emitter voltages are equal to +800 mV and zero, respectively. We must now calculate the collector voltage, $V_{X}$. Writing a KVL from the 2-V power supply and $\operatorname{across} R_{C}$ and $Q_{1}$, we obtain

$$
\begin{equation*}
V_{C C}=R_{C} I_{C}+V_{X} \tag{4.34}
\end{equation*}
$$

That is,

$$
\begin{equation*}
V_{X}=1.424 \mathrm{~V} \tag{4.35}
\end{equation*}
$$

Since the collector voltage is more positive than the base voltage, this junction is reversebiased and the transistor operates in the active mode.
(b) What happens to the circuit as $R_{C}$ increases? Since the voltage drop across the resistor, $R_{C} I_{C}$, increases while $V_{C C}$ is constant, the voltage at node $X$ drops.

The device approaches the "edge" of the forward active region if the base-collector voltage falls to zero, i.e., as $V_{X} \rightarrow+800 \mathrm{mV}$. Rewriting Eq. (4.33) yields:

$$
\begin{equation*}
R_{C}=\frac{V_{C C}-V_{X}}{I_{C}}, \tag{4.36}
\end{equation*}
$$

which, for $V_{X}=+800 \mathrm{mV}$, reduces to

$$
\begin{equation*}
R_{C}=1041 \Omega \tag{4.37}
\end{equation*}
$$

Figure 4.14(b) plots $V_{X}$ as a function of $R_{C}$.
This example implies that there exists a maximum allowable value of the collector resistance, $R_{C}$, in the circuit of Fig. 4.14(a). As we will see in Chapter 5, this limits the voltage gain that the circuit can provide.

Exercise In the above example, what is the minimum allowable value of $V_{C C}$ for transistor operation in the active mode? Assume $R_{C}=500 \Omega$.

The reader may wonder why the equivalent circuit of Fig. 4.13 is called the "large-signal model." After all, the above example apparently contains no signals! This terminology emphasizes that the model can be used for arbitrarily large voltage and current changes in the transistor (so long as the device operates in the active mode). For example, if the base-emitter voltage varies from 800 mV to 300 mV , and hence the collector current by many orders of magnitude, ${ }^{4}$ the model still applies. This is in contrast to the small-signal model, studied in Section 4.4.4.

### 4.4.2 I/V Characteristics

The large-signal model naturally leads to the I/V characteristics of the transistor. With three terminal currents and voltages, we may envision plotting different currents as a function of the potential difference between every two terminals-an elaborate task. However, as explained below, only a few of such characteristics prove useful.

The first characteristic to study is, of course, the exponential relationship inherent in the device. Figure 4.15 (a) plots $I_{C}$ versus $V_{B E}$ with the assumption that the collector voltage is constant and no lower than the base voltage. As shown in Fig. 4.11, $I_{C}$ is independent of $V_{C E}$; thus, different values of $V_{C E}$ do not alter the characteristic.

Next, we examine $I_{C}$ for a given $V_{B E}$ but with $V_{C E}$ varying. Illustrated in Fig. 4.15(b), the characteristic is a horizontal line because $I_{C}$ is constant if the device remains in the active mode $\left(V_{C E}>V_{B E}\right)$. On the other hand, if different values are chosen for $V_{B E}$, the characteristic moves up or down.

The two plots of Fig. 4.15 constitute the principal characteristics of interest in most analysis and design tasks. Equations (4.24) and (4.25) suggest that the base and emitter currents follow the same behavior.

[^17]image_name:(a)
description:The graph labeled "(a)" in Figure 4.15 is a plot of the collector current ($I_C$) as a function of the base-emitter voltage ($V_{BE}$) for a bipolar junction transistor (BJT).

1. **Type of Graph and Function:**
- This is a characteristic curve showing the relationship between the collector current and base-emitter voltage in a BJT.

2. **Axes Labels and Units:**
- The x-axis represents the base-emitter voltage ($V_{BE}$), typically measured in volts.
- The y-axis represents the collector current ($I_C$), typically measured in amperes or microamperes.
- The scales appear to be linear, with $V_{BE}$ increasing to the right and $I_C$ increasing upwards.

3. **Overall Behavior and Trends:**
- The graph shows an exponential increase of the collector current with increasing base-emitter voltage. This is typical of BJTs, where a small increase in $V_{BE}$ can cause a significant increase in $I_C$.
- The curve starts at the origin and rises steeply as $V_{BE}$ increases, indicating the transistor is moving from cutoff to active mode.

4. **Key Features and Technical Details:**
- The steep rise in $I_C$ as $V_{BE}$ increases suggests that the transistor is in the active region, where current amplification occurs.
- There are no specific numerical values or annotations on the graph, but the exponential nature is evident.

5. **Annotations and Specific Data Points:**
- The graph does not contain specific markers or reference lines, but it visually represents the exponential relationship between $I_C$ and $V_{BE}$, which is a key characteristic of BJTs in the active region.
image_name:(b)
description:The graph labeled as (b) depicts the collector current \( I_C \) as a function of the collector-emitter voltage \( V_{CE} \) for a bipolar transistor. This is a characteristic curve often used in analyzing and designing transistor circuits.

1. **Type of Graph and Function:**
- This is a characteristic curve graph showing the relationship between collector current \( I_C \) and collector-emitter voltage \( V_{CE} \) for a bipolar junction transistor.

2. **Axes Labels and Units:**
- The vertical axis represents the collector current \( I_C \), typically measured in amperes (A).
- The horizontal axis represents the collector-emitter voltage \( V_{CE} \), typically measured in volts (V).
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The graph shows horizontal lines indicating that the collector current \( I_C \) remains constant regardless of the increase in \( V_{CE} \), provided the transistor is in the active region (i.e., \( V_{CE} > V_{BE} \)).
- This horizontal behavior indicates that \( I_C \) is independent of \( V_{CE} \) in this region.

4. **Key Features and Technical Details:**
- There are multiple horizontal lines, each corresponding to different base-emitter voltages \( V_{BE} \). The graph indicates two specific \( V_{BE} \) levels, \( V_{BE} = V_{B1} \) and \( V_{BE} = V_{B2} \), showing that as \( V_{BE} \) increases, the collector current \( I_C \) also increases.
- The collector current values are given by the expression \( I_S \exp\left(\frac{V_{BE}}{V_T}\right) \), where \( I_S \) is the saturation current and \( V_T \) is the thermal voltage.

5. **Annotations and Specific Data Points:**
- The graph is annotated with expressions for \( I_C \) in terms of \( V_{BE} \) and \( V_T \), specifically \( I_S \exp\left(\frac{V_{BE1}}{V_T}\right) \) and \( I_S \exp\left(\frac{V_{BE2}}{V_T}\right) \), indicating the collector current levels for two different base-emitter voltages.
- Horizontal dashed lines are used to represent these constant current levels across different \( V_{CE} \) values.

Figure 4.15 Collector current as a function of (a) base-emitter voltage and (b) collectoremitter voltage.

Example
4.8

For a bipolar transistor, $I_{S}=5 \times 10^{-17} \mathrm{~A}$ and $\beta=100$. Construct the $I_{C}-V_{B E}, I_{C}-V_{C E}$, $I_{B}-V_{B E}$, and $I_{B}-V_{C E}$ characteristics.

Solution We determine a few points along the $I_{C}-V_{B E}$ characteristics, e.g.,

$$
\begin{align*}
& V_{B E 1}=700 \mathrm{mV} \Rightarrow I_{C 1}=24.6 \mu \mathrm{~A}  \tag{4.38}\\
& V_{B E 2}=750 \mathrm{mV} \Rightarrow I_{C 2}=169 \mu \mathrm{~A}  \tag{4.39}\\
& V_{B E 3}=800 \mathrm{mV} \Rightarrow I_{C 3}=1.153 \mathrm{~mA} \tag{4.40}
\end{align*}
$$

The characteristic is depicted in Fig. 4.16 (a).
image_name:(a)
description:The graph in Figure 4.16 (a) is a plot of collector current ($I_C$) versus base-emitter voltage ($V_{BE}$). This is a typical characteristic curve for a bipolar junction transistor (BJT).

1. **Type of Graph and Function:**
- This is a current-voltage characteristic graph.

2. **Axes Labels and Units:**
- The x-axis represents the base-emitter voltage ($V_{BE}$) in millivolts (mV), ranging from 700 mV to 800 mV.
- The y-axis represents the collector current ($I_C$) in microamperes (µA) and milliamperes (mA), ranging from 24.6 µA to 1.153 mA.

3. **Overall Behavior and Trends:**
- The graph shows an exponential increase in the collector current as the base-emitter voltage increases. This indicates the typical exponential relationship between $I_C$ and $V_{BE}$ in BJTs.

4. **Key Features and Technical Details:**
- At $V_{BE} = 700$ mV, the collector current $I_C$ is 24.6 µA.
- At $V_{BE} = 750$ mV, $I_C$ increases to 169 µA.
- At $V_{BE} = 800$ mV, $I_C$ further increases to 1.153 mA.
- The curve demonstrates the sensitivity of the collector current to changes in the base-emitter voltage, a critical aspect of transistor operation.

5. **Annotations and Specific Data Points:**
- The graph includes horizontal dashed lines and vertical markers to indicate the specific data points at which measurements were taken: 700 mV, 750 mV, and 800 mV for $V_{BE}$, corresponding to collector currents of 24.6 µA, 169 µA, and 1.153 mA, respectively.

This graph is essential for understanding how the base-emitter voltage influences the collector current in a BJT, highlighting the transistor's operation in its active region.
image_name:(b)
description:The graph labeled (b) is a plot of collector current (I_C) versus collector-emitter voltage (V_CE) for a transistor, with constant base-emitter voltages (V_BE).

1. **Type of Graph and Function:**
- This is a characteristic curve graph showing the behavior of a transistor's collector current with respect to the collector-emitter voltage, while keeping the base-emitter voltage constant.

2. **Axes Labels and Units:**
- The horizontal axis represents the collector-emitter voltage (V_CE) in volts (V).
- The vertical axis represents the collector current (I_C) in microamperes (μA) and milliamperes (mA).

3. **Overall Behavior and Trends:**
- The graph shows that the collector current (I_C) remains constant as the collector-emitter voltage (V_CE) changes, indicating that the transistor is operating in the active region as a constant current source.
- For each constant base-emitter voltage, the collector current is stable, suggesting that changes in V_CE do not significantly affect I_C.

4. **Key Features and Technical Details:**
- The graph contains three horizontal lines, each representing a different constant base-emitter voltage (V_BE).
- At V_BE = 700 mV, I_C = 24.6 μA.
- At V_BE = 750 mV, I_C = 169 μA.
- At V_BE = 800 mV, I_C = 1.153 mA.
- These constant lines demonstrate the transistor's ability to maintain a steady collector current for a given base-emitter voltage, regardless of variations in V_CE.

5. **Annotations and Specific Data Points:**
- The graph is annotated with the specific V_BE values alongside the corresponding I_C values, clearly indicating the relationship between the base-emitter voltage and the collector current.
- The horizontal lines emphasize the constant current characteristic of the transistor in this configuration.
image_name:(c)
description:The graph labeled (c) is a plot of base current \( I_B \) as a function of base-emitter voltage \( V_{BE} \). This graph is a part of the transistor characteristic curves and is specifically focused on the behavior of the base current with changes in the base-emitter voltage.

1. **Type of Graph and Function:**
- This is a characteristic curve graph, specifically plotting \( I_B \) versus \( V_{BE} \).

2. **Axes Labels and Units:**
- The x-axis represents the base-emitter voltage \( V_{BE} \) in millivolts (mV), ranging from 700 mV to 800 mV.
- The y-axis represents the base current \( I_B \) in microamperes (\( \mu A \)), ranging from 0.025 \( \mu A \) to 11.5 \( \mu A \).

3. **Overall Behavior and Trends:**
- The graph demonstrates an exponential increase in base current \( I_B \) as the base-emitter voltage \( V_{BE} \) increases.
- The curve starts at a low base current at \( V_{BE} = 700 \) mV and rises steeply as \( V_{BE} \) approaches 800 mV.

4. **Key Features and Technical Details:**
- At \( V_{BE} = 700 \) mV, \( I_B \) is approximately 0.025 \( \mu A \).
- At \( V_{BE} = 750 \) mV, \( I_B \) is approximately 0.169 \( \mu A \).
- At \( V_{BE} = 800 \) mV, \( I_B \) reaches about 11.5 \( \mu A \).
- The graph clearly shows the non-linear relationship between \( I_B \) and \( V_{BE} \), typical of a semiconductor junction behavior.

5. **Annotations and Specific Data Points:**
- The graph is annotated with horizontal dashed lines indicating the specific \( I_B \) values at the given \( V_{BE} \) points (700 mV, 750 mV, and 800 mV), highlighting the steep rise in current as voltage increases.
image_name:(d)
description:The graph labeled (d) is a plot of base current \( I_B \) as a function of collector-emitter voltage \( V_{CE} \). This type of graph is used to illustrate the behavior of a transistor's base current under varying \( V_{CE} \) conditions.

1. **Axes Labels and Units:**
- The horizontal axis represents \( V_{CE} \), the collector-emitter voltage, in volts (V).
- The vertical axis represents \( I_B \), the base current, in microamperes (\( \mu A \)).

2. **Overall Behavior and Trends:**
- The graph shows horizontal lines, indicating that the base current \( I_B \) remains constant as the collector-emitter voltage \( V_{CE} \) changes. This suggests that \( I_B \) is independent of \( V_{CE} \) in this configuration.

3. **Key Features and Technical Details:**
- The graph includes three distinct horizontal lines corresponding to different base-emitter voltages \( V_{BE} \):
- For \( V_{BE} = 700 \) mV, \( I_B \) is approximately 0.025 \( \mu A \).
- For \( V_{BE} = 750 \) mV, \( I_B \) is approximately 0.169 \( \mu A \).
- For \( V_{BE} = 800 \) mV, \( I_B \) is approximately 11.5 \( \mu A \).

4. **Annotations and Specific Data Points:**
- The graph is annotated with dashed lines indicating constant \( I_B \) values at specific \( V_{BE} \) levels.
- These annotations highlight the dependency of \( I_B \) on \( V_{BE} \) while remaining unaffected by \( V_{CE} \).

Overall, this graph effectively demonstrates how the base current \( I_B \) is controlled by the base-emitter voltage \( V_{BE} \) and remains constant across varying collector-emitter voltages \( V_{CE} \).

Figure 4.16 (a) Collector current as a function of $V_{B E}$, (b) collector current as a function of $V_{C E}$, (c) base current as a function of $V_{B E}$, (d) base current as a function of $V_{C E}$.

Using the values obtained above, we can also plot the $I_{C}-V_{C E}$ characteristic as shown in Fig. 4.16(b), concluding that the transistor operates as a constant current source of, e.g., $169 \mu \mathrm{~A}$ if its base-emitter voltage is held at 750 mV . We also remark that, for equal increments in $V_{B E}, I_{C}$ jumps by increasingly greater steps: $24.6 \mu \mathrm{~A}$ to $169 \mu \mathrm{~A}$ to 1.153 mA . We return to this property in Section 4.4.3.

For $I_{B}$ characteristics, we simply divide the $I_{C}$ values by 100 [Figs. 4.16(c) and (d)].
Exercise What change in $V_{B E}$ doubles the base current?

The reader may wonder what exactly we learn from the I/V characteristics. After all, compared to Eqs. (4.23)-(4.25), the plots impart no additional information. However, as we will see throughout this book, the visualization of equations by means of such plots greatly enhances our understanding of the devices and the circuits employing them.

### 4.4.3 Concept of Transconductance

Our study thus far shows that the bipolar transistor acts as a voltage-dependent current source (when operating in the forward active region). An important question that arises here is, how is the performance of such a device quantified? In other words, what is the measure of the "goodness" of a voltage-dependent current source?

The example depicted in Fig. 4.1 suggests that the device becomes "stronger" as $K$ increases because a given input voltage yields a larger output current. We must therefore concentrate on the voltage-to-current conversion property of the transistor, particularly as it relates to amplification of signals. More specifically, we ask, if a signal changes the base-emitter voltage of a transistor by a small amount (Fig. 4.17), how much change is produced in the collector current? Denoting the change in $I_{C}$ by $\Delta I_{C}$, we recognize that the "strength" of the device can be represented by $\Delta I_{C} / \Delta V_{B E}$. For example, if a base-emitter voltage change of 1 mV results in a $\Delta I_{C}$ of 0.1 mA in one transistor and 0.5 mA in another, we can view the latter as a better voltage-dependent current source or "voltage-to-current converter."

The ratio $\Delta I_{C} / \Delta V_{B E}$ approaches $d I_{C} / d V_{B E}$ for very small changes and, in the limit, is called the "transconductance," $g_{m}$ :*

$$
\begin{equation*}
g_{m}=\frac{d I_{C}}{d V_{B E}} . \tag{4.41}
\end{equation*}
$$

image_name:Figure 4.17 Test circuit for measurement of g_m
description:
[
name: Q1, type: NPN, ports: {C: VCE, B: VBE, E: GND}
name: VBE, type: VoltageSource, value: VBE, ports: {Np: VBE, Nn: GND}
name: VCE, type: VoltageSource, value: VCE, ports: {Np: VCE, Nn: GND}
]
extrainfo:The circuit is used for measuring the transconductance (g_m) of an NPN transistor. The base-emitter voltage (VBE) is controlled to vary the collector current (IC), while the collector-emitter voltage (VCE) is kept constant.

Figure 4.17 Test circuit for measurement of $g_{m}$.
${ }^{*}$ Note that $V_{C E}$ is constant here.

Note that this definition applies to any device that approximates a voltage-dependent current source (e.g., another type of transistor described in Chapter 6). For a bipolar transistor, Eq. (4.9) gives

$$
\begin{align*}
g_{m} & =\frac{d}{d V_{B E}}\left(I_{S} \exp \frac{V_{B E}}{V_{T}}\right)  \tag{4.42}\\
& =\frac{1}{V_{T}} I_{S} \exp \frac{V_{B E}}{V_{T}}  \tag{4.43}\\
& =\frac{I_{C}}{V_{T}} \tag{4.44}
\end{align*}
$$

The close resemblance between this result and the small-signal resistance of diodes [Eq. (3.58)] is no coincidence and will become clearer in the next chapter.

Equation (4.44) reveals that, as $I_{C}$ increases, the transistor becomes a better amplifying device by producing larger collector current excursions in response to a given signal level applied between the base and the emitter. The transconductance may be expressed in $\Omega^{-1}$ or "siemens," S. For example, if $I_{C}=1 \mathrm{~mA}$, then with $V_{T}=26 \mathrm{mV}$, we have

$$
\begin{align*}
g_{m} & =0.0385 \Omega^{-1}  \tag{4.45}\\
& =0.0385 \mathrm{~S}  \tag{4.46}\\
& =38.5 \mathrm{mS} \tag{4.47}
\end{align*}
$$

However, as we will see throughout this book, it is often helpful to view $g_{m}$ as the inverse of a resistance; e.g., for $I_{C}=1 \mathrm{~mA}$, we may write

$$
\begin{equation*}
g_{m}=\frac{1}{26 \Omega} \tag{4.48}
\end{equation*}
$$

The concept of transconductance can be visualized with the aid of the transistor I/V characteristics. As shown in Fig. 4.18, $g_{m}=d I_{C} / d V_{B E}$ simply represents the slope of $I_{C}-V_{B E}$ characteristic at a given collector current, $I_{C 0}$, and the corresponding base-emitter voltage, $V_{B E 0}$. In other words, if $V_{B E}$ experiences a small perturbation $\pm \Delta V$ around $V_{B E 0}$, then the collector current displays a change of $\pm g_{m} \Delta V$ around $I_{C 0}$, where $g_{m}=I_{C 0} / V_{T}$. Thus, the
image_name:Figure 4.18
description:The graph in Figure 4.18 is a characteristic curve representing the relationship between the collector current \( I_C \) and the base-emitter voltage \( V_{BE} \) of a transistor. It is a plot of \( I_C \) on the vertical axis against \( V_{BE} \) on the horizontal axis. The axes are labeled with \( I_C \) for the collector current, and \( V_{BE} \) for the base-emitter voltage, respectively.

The graph illustrates a non-linear curve, which starts at the origin and rises steeply, indicating an exponential relationship between \( I_C \) and \( V_{BE} \). The point \( (V_{BE0}, I_{C0}) \) is marked, representing a specific operating point or bias point of the transistor, where \( V_{BE} = V_{BE0} \) and \( I_C = I_{C0} \).

Around the operating point, the graph shows a small sinusoidal variation in \( V_{BE} \) denoted by \( \pm \Delta V \). This perturbation in \( V_{BE} \) leads to a corresponding change in \( I_C \), represented by \( \pm g_m \Delta V \), where \( g_m \) is the transconductance of the transistor. The transconductance \( g_m \) is depicted as the slope of the curve at the bias point, indicating how the collector current changes with small changes in base-emitter voltage.

Overall, the graph emphasizes the sensitivity of the collector current to changes in base-emitter voltage at the bias point, illustrating the concept of transconductance in transistors. The annotations highlight the specific changes \( \Delta V \) and \( g_m \Delta V \), showcasing the linear approximation of the curve around the operating point.

Figure 4.18 Illustration of transconductance.
value of $I_{C 0}$ must be chosen according to the required $g_{m}$ and, ultimately, the required gain. We say the transistor is "biased" at a collector current of $I_{C 0}$, meaning the device carries a bias (or "quiescent") current of $I_{C 0}$ in the absence of signals. ${ }^{5}$
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: VCE, B: VBE0, E: GND}
name: V_BE0, type: VoltageSource, value: V_BE0, ports: {Np: VBE0, Nn: GND}
name: V_CE, type: VoltageSource, value: V_CE, ports: {Np: VCE, Nn: GND}
]
extrainfo:The circuit diagram (a) shows a single NPN transistor Q1 with a collector current I_C0, biased with V_BE0 and V_CE voltages. The circuit is used to analyze the effect of increasing the device area on transconductance.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: VCE, B: VBEO, E: GND}
name: Q2, type: NPN, ports: {C: VCE, B: VBEO, E: GND}
name: Q3, type: NPN, ports: {C: VCE, B: VBEO, E: GND}
]
extrainfo:The circuit shows three NPN transistors (Q1, Q2, Q3) in parallel, each with a collector current of I_C0. The base-emitter voltage (V_BE0) is constant across all transistors. The transconductance increases by a factor of n when n identical transistors are used.

Figure 4.19 (a) One transistor and (b) $n$ transistors providing transconductance.
Solution Since $I_{S} \propto A_{E}, I_{S}$ is multiplied by the same factor. Thus, $I_{C}=I_{S} \exp \left(V_{B E} / V_{T}\right)$ also rises by a factor of $n$ because $V_{B E}$ is constant. As a result, the transconductance increases by a factor of $n$. From another perspective, if $n$ identical transistors, each carrying a collector current of $I_{C 0}$, are placed in parallel, then the composite device exhibits a transconductance equal to $n$ times that of each [Fig. 4.19(b)]. On the other hand, if the total collector current remains unchanged, then so does the transconductance.

Exercise Repeat the above example if $V_{B E 0}$ is reduced by $V_{T} \ln n$.

It is also possible to study the transconductance in the context of the $I_{C}-V_{C E}$ characteristics of the transistor with $V_{B E}$ as a parameter. Illustrated in Fig. 4.20 for two different bias currents $I_{C 1}$ and $I_{C 2}$, the plots reveal that a change of $\Delta V$ in $V_{B E}$ results in a greater change in $I_{C}$ for operation around $I_{C 2}$ than around $I_{C 1}$ because $g_{m 2}>g_{m 1}$.

The derivation of $g_{m}$ in Eqs. (4.42)-(4.44) suggests that the transconductance is fundamentally a function of the collector current rather than the base current. For example, if $I_{C}$ remains constant but $\beta$ varies, then $g_{m}$ does not change but $I_{B}$ does. For this reason, the collector bias current plays a central role in the analysis and design, with the base current viewed as secondary, often undesirable effect.

As shown in Fig. 4.10,the current produced by the transistor may flow through a resistor to generate a proportional voltage. We exploit this concept in Chapter 5 to design amplifiers.

### 4.4.4 Small-Signal Model

Electronic circuits, e.g., amplifiers, may incorporate a large number of transistors, thus posing great difficulties in the analysis and design. Recall from Chapter 3 that diodes can

[^18]image_name:Figure 4.20 Transconductance for different collector bias currents
description:The graph in Figure 4.20 illustrates the transconductance behavior for different collector bias currents in a transistor. It is a line graph that plots collector current (I_C) on the vertical axis against collector-emitter voltage (V_CE) on the horizontal axis.

Axes Labels and Units:
- **Vertical Axis (Y-Axis):** Represents the collector current (I_C), with specific points labeled as I_C1 and I_C2. The units are typically in amperes (A), though not explicitly labeled.
- **Horizontal Axis (X-Axis):** Represents the collector-emitter voltage (V_CE), with the units likely in volts (V), though not explicitly labeled.

Overall Behavior and Trends:
The graph depicts two horizontal lines corresponding to different base-emitter voltages (V_BE) states:
1. **Lower Line:** Represents the initial base-emitter voltage V_BE = V_B1. When a small voltage increment ΔV is applied, it shifts to a new line, indicating a change in collector current due to increased transconductance g_m1.
2. **Upper Line:** Represents a higher initial base-emitter voltage V_BE = V_B2. Similarly, an increment ΔV results in a shift to a new level of collector current with transconductance g_m2.

Key Features and Technical Details:
- **Transconductance (g_m):** The graph illustrates the effect of transconductance (g_m1 and g_m2) as a function of the applied voltage increment ΔV. The transconductance is depicted as the slope of the change in collector current per unit change in base-emitter voltage.
- **Voltage Increments (ΔV):** The graph shows the impact of a small voltage increment (ΔV) on the collector current for each base-emitter voltage level.
- **Collector Bias Currents (I_C1 and I_C2):** The graph highlights two distinct collector currents corresponding to different bias conditions.

Annotations and Specific Data Points:
- The graph includes annotations showing the base-emitter voltage states (V_BE = V_B1, V_B1 + ΔV, V_B2, V_B2 + ΔV) and the corresponding transconductance values (g_m1, g_m2).
- The dashed lines indicate the initial and final states of the collector current as the voltage changes.

Figure 4.20 Transconductance for different collector bias currents.
be reduced to linear devices through the use of the small-signal model. A similar benefit accrues if a small-signal model can be developed for transistors.

The derivation of the small-signal model from the large-signal counterpart is relatively straightforward. We perturb the voltage difference between every two terminals (while the third terminal remains at a constant potential), determine the changes in the currents flowing through all terminals, and represent the results by proper circuit elements such as controlled current sources or resistors. Figure 4.21 depicts two conceptual examples where $V_{B E}$ or $V_{C E}$ is changed by $\Delta V$ and the changes in $I_{C}, I_{B}$, and $I_{E}$ are examined.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: ΔI_C, B: ΔI_B, E: ΔI_E}
name: ΔV, type: VoltageSource, value: ΔV, ports: {Np: V, Nn: GND}
name: V_CE, type: VoltageSource, value: V_CE, ports: {Np: ΔI_C, Nn: GND}
name: V_BE, type: VoltageSource, value: V_BE, ports: {Np: ΔI_B, Nn: GND}
]
extrainfo:The circuit diagram shows an NPN transistor (Q1) with changes in base-emitter voltage (V_BE) and collector-emitter voltage (V_CE). The voltage source ΔV is applied between the base and ground, influencing the currents ΔI_C, ΔI_B, and ΔI_E.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: V, B: VBE, E: GND}
name: ΔV, type: VoltageSource, value: ΔV, ports: {Np: V, Nn: GND}
name: VCE, type: VoltageSource, value: VCE, ports: {Np: V, Nn: GND}
name: VBE, type: VoltageSource, value: VBE, ports: {Np: VBE, Nn: GND}
]
extrainfo:The circuit diagram shows an NPN transistor Q1 with its collector connected to node V, the base to node VBE, and the emitter to ground. A voltage source ΔV is connected between node V and ground, while the voltage source VCE is also connected between node V and ground. The voltage source VBE is connected between node VBE and ground.

Figure 4.21 Excitation of bipolar transistor with small changes in (a) base-emitter and (b) collector-emitter voltage.

Let us begin with a change in $V_{B E}$ while the collector voltage is constant (Fig. 4.22).We know from the definition of transconductance that

$$
\begin{equation*}
\Delta I_{C}=g_{m} \Delta V_{B E} \tag{4.49}
\end{equation*}
$$

concluding that a voltage-controlled current source must be connected between the collector and the emitter with a value equal to $g_{m} \Delta V$. For simplicity, we denote $\Delta V_{B E}$ by $v_{\pi}$ and the change in the collector current by $g_{m} v_{\pi}$.
image_name:Figure 4.22 Development of small-signal model
description:
[
name: Q1, type: NPN, ports: {C: VCE, B: VBE, E: GND}
name: VBE, type: VoltageSource, value: VBE, ports: {Np: VBE, Nn: GND}
name: VCE, type: VoltageSource, value: VCE, ports: {Np: VCE, Nn: GND}
]
extrainfo:The circuit represents a small-signal model where the change in collector current (ΔIC) is controlled by the transconductance (gm) and the change in base-emitter voltage (ΔVBE). The NPN transistor Q1 is driven by the voltage source VBE and outputs to VCE.

image_name:Figure 4.22
description:
[
name: ΔVBE, type: VoltageSource, ports: {Np: ΔVBE, Nn: GND}
name: VBE, type: VoltageSource, ports: {Np: VBE, Nn: GND}
name: ΔIB, type: CurrentSource, ports: {Np: VBE, Nn: Diode}
name: Diode, type: Diode, ports: {Na: VBE, Nc: GND}
name: IS exp, type: CurrentSource, ports: {Np: VCE, Nn: VBE}
name: VCE, type: VoltageSource, ports: {Np: VCE, Nn: GND}
]
extrainfo:The circuit represents a small-signal model where the change in collector current (ΔIC) is controlled by the transconductance (gm) and the change in base-emitter voltage (ΔVBE). The NPN transistor Q1 is driven by the voltage source VBE and outputs to VCE. The change in VBE creates a change in IB, which is proportional to the change in IC divided by the current gain β.

image_name:Figure 4.22a
description:
[
name: gmΔV_BE, type: VoltageControlledCurrentSource, ports: {Np: C, Nn: E}
name: gmv_π, type: VoltageControlledCurrentSource, ports: {Np: C, Nn: E}
name: r_π, type: Resistor, value: r_π, ports: {N1: B, N2: E}
]
extrainfo:The circuit diagram represents a small-signal model of an NPN transistor. The change in base-emitter voltage (ΔV_BE) influences the collector current through the transconductance (gm). The diagram shows the evolution of the model with a voltage-controlled current source (gmΔV_BE) and a resistor (r_π) representing the base-emitter resistance. The final stage includes the effect of the transconductance (gmv_π) on the collector current.
image_name:Figure 4.22b
description:
[
name: g_m ΔV_BE, type: VoltageControlledCurrentSource, ports: {Np: C, Nn: E}
name: g_m v_π, type: VoltageControlledCurrentSource, ports: {Np: C, Nn: E}
name: r_π, type: Resistor, value: r_π, ports: {N1: B, N2: E}
]
extrainfo:The circuit is a small-signal model of an NPN transistor. The change in base-emitter voltage (ΔVBE) controls the collector current through the transconductance (gm). The voltage-controlled current source represents the output current proportional to gm times the input voltage. The resistor r_π models the base resistance.
image_name:Figure 4.22c
description:
[
name: vπ, type: VoltageSource, ports: {Np: B, Nn: E}
name: gmvπ, type: VoltageControlledCurrentSource, ports: {Np: C, Nn: E}
name: rπ, type: Resistor, value: rπ, ports: {N1: B, N2: E}
]
extrainfo:The circuit diagram represents a small-signal model of an NPN transistor, showing the relationship between the base-emitter voltage (vπ) and the collector current controlled by the transconductance (gm). The resistor rπ models the input resistance at the base-emitter junction.

Figure 4.22 Development of small-signal model.
The change in $V_{B E}$ creates another change as well:

$$
\begin{align*}
\Delta I_{B} & =\frac{\Delta I_{C}}{\beta}  \tag{4.50}\\
& =\frac{g_{m}}{\beta} \Delta V_{B E} \tag{4.51}
\end{align*}
$$

That is, if the base-emitter voltage changes by $\Delta V_{B E}$, the current flowing between these two terminals changes by $\left(g_{m} / \beta\right) \Delta V_{B E}$. Since the voltage and current correspond to the same two terminals, they can be related by Ohm's Law, i.e., by a resistor placed between the base and emitter having a value:

$$
\begin{align*}
r_{\pi} & =\frac{\Delta V_{B E}}{\Delta I_{B}}  \tag{4.52}\\
& =\frac{\beta}{g_{m}} \tag{4.53}
\end{align*}
$$

Thus, the forward-biased diode between the base and the emitter is modeled by a small-signal resistance equal to $\beta / g_{m}$. This result is expected because the diode carries a bias current equal to $I_{C} / \beta$ and, from Eq. (3.58), exhibits a small-signal resistance of $V_{T} /\left(I_{C} / \beta\right)=\beta\left(V_{T} / I_{C}\right)=\beta / g_{m}$.

We now turn our attention to the collector and apply a voltage change with respect to the emitter (Fig. 4.23). As illustrated in Fig. 4.11, for a constant $V_{B E}$, the collector voltage has no effect on $I_{C}$ or $I_{B}$ because $I_{C}=I_{S} \exp \left(V_{B E} / V_{T}\right)$ and $I_{B}=I_{C} / \beta$. Since $\Delta V_{C E}$ leads to no change in any of the terminal currents, the model developed in Fig. 4.22 need not be altered.

How about a change in the collector-base voltage? As studied in Problem 4.18, such a change also results in a zero change in the terminal currents.
image_name:Fig. 4.23
description:
[
name: Q1, type: NPN, ports: {C: V_CE, B: V_BE, E: GND}
name: V_BE, type: VoltageSource, value: V_BE, ports: {Np: V_BE, Nn: GND}
name: I_S exp(V_BE/V_T), type: CurrentSource, ports: {Np: V_BE, Nn: GND}
name: ΔV_CE, type: VoltageControlledVoltageSource, ports: {Np: V_CE, Nn: GND}
]
extrainfo:The circuit represents a small-signal model of a bipolar transistor showing the effect of changes in V_CE on the current I_C. It includes an NPN transistor, a voltage source V_BE, a current source dependent on V_BE, and a voltage-controlled voltage source representing ΔV_CE.
image_name:Fig. 4.22
description:
[
name: Q1, type: NPN, ports: {C: VCE, B: VBE, E: GND}
name: VBE, type: VoltageSource, value: VBE, ports: {Np: VBE, Nn: GND}
name: IS, type: CurrentSource, value: IS, ports: {Np: GND, Nn: VCE}
name: VCE, type: VoltageSource, value: ΔVCE, ports: {Np: VCE, Nn: GND}
]
extrainfo:The circuit illustrates a small-signal model of a bipolar transistor with a constant base-emitter voltage (VBE) and a change in collector-emitter voltage (ΔVCE). The current source IS represents the collector current IC as a function of VBE, and the voltage source VCE represents the change in collector-emitter voltage.

Figure 4.23 Response of bipolar transistor to small change in $V_{C E}$.

The simple small-signal model developed in Fig. 4.22 serves as a powerful, versatile tool in the analysis and design of bipolar circuits. We should remark that both parameters of the model, $g_{m}$ and $r_{\pi}$, depend on the bias current of the device. With a high collector bias current, a greater $g_{m}$ is obtained, but the impedance between the base and emitter falls to lower values. Studied in Chapter 5, this trade-off proves undesirable in some cases.
image_name:Figure 4.24 (a)
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: V1, E: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
name: VCC, type: VoltageSource, value: 1.8V, ports: {Np: VCC, Nn: GND}
]
extrainfo:The circuit is a simple NPN transistor amplifier with a bias voltage of 1.8V and a small-signal input represented by v1. The transistor operates in active mode with a beta of 100. The small-signal parameters are calculated based on a collector current of 6.92 mA and a base-emitter voltage of 800 mV. The change in collector current due to a 1 mV input is 0.267 mA.
image_name:Figure 4.24 (b)
description:
[
name: V1, type: VoltageSource, value: 800mV, ports: {Np: Vin, Nn: GND}
name: VCC, type: VoltageSource, value: 1.8V, ports: {Np: VCC, Nn: GND}
name: Q1, type: NPN, ports: {C: VCC, B: Vin, E: GND}
]
extrainfo:The circuit is a small-signal model of a transistor with bias and small-signal excitation. The parameters g_m and r_π are calculated based on the bias current. The circuit is used to determine changes in collector and base currents due to a small input signal.

The equivalent circuit also predicts the change in the base current as

$$
\begin{align*}
\Delta I_{B} & =\frac{v_{1}}{r_{\pi}}  \tag{4.61}\\
& =\frac{1 \mathrm{mV}}{375 \Omega}  \tag{4.62}\\
& =2.67 \mu \mathrm{~A} \tag{4.63}
\end{align*}
$$

which is, of course, equal to $\Delta I_{C} / \beta$.

Exercise Repeat the above example if $I_{S}$ is halved.

The above example is not a useful circuit. The microphone signal produces a change in $I_{C}$, but the result flows through the $1.8-\mathrm{V}$ battery. In other words, the circuit generates no output. On the other hand, if the collector current flows through a resistor, a useful output is provided.
image_name:Figure 4.25
description:
[
name: RC, type: Resistor, value: 100Ω, ports: {N1: Vout, N2: VCC}
name: Q1, type: NPN, ports: {C: Vout, B: b1, E: GND}
name: V1, type: VoltageSource, value: 800mV, ports: {Np: b1, Nn: X1}
name: VCC, type: VoltageSource, value: 1.8V, ports: {Np: VCC, Nn: GND}
]
extrainfo:The circuit is a simple transistor amplifier stage with biasing and small-signal excitation. The collector current is converted to a voltage across RC, providing an output at Vout.

Figure 4.25 Simple stage with bias and small-signal excitation.

Solution
(a) The collector bias current of 6.92 mA flows through $R_{C}$, leading to a potential drop of $I_{C} R_{C}=692 \mathrm{mV}$. The collector voltage, which is equal to $V_{\text {out }}$, is thus given by:

$$
\begin{align*}
V_{\text {out }} & =V_{C C}-R_{C} I_{C}  \tag{4.64}\\
& =1.108 \mathrm{~V} . \tag{4.65}
\end{align*}
$$

Since the collector voltage (with respect to ground) is more positive than the base voltage, the device operates in the active mode.
(b) As seen in the previous example, a $1-\mathrm{mV}$ microphone signal leads to a $0.267-\mathrm{mA}$ change in $I_{C}$. Upon flowing through $R_{C}$, this change yields a change of $0.267 \mathrm{~mA} \times 100 \Omega=26.7 \mathrm{mV}$ in $V_{\text {out }}$. The circuit therefore amplifies the input by a factor of 26.7 .

Exercise What value of $R_{C}$ results in a zero collector-base voltage?

Did you know?

The first revolution afforded by the transistor was the concept of portable radios. Up to the 1940s, radios incorporated vacuum tubes, which required very high supply voltages (e.g., 60 V ) and hence a bulky and heavy radio design. The transistor, on the other hand, could operate with a few batteries. The portable "transistor radio" was thus introduced by Regency and Texas Instruments in 1954. Interestingly, a Japanese company called Tsushin Kogyo had also been working on a transistor radio around that time and was eager to enter the American market. Since the company's name was difficult to pronounce for westerners, they picked the Latin word "sonus" for sound and called themselves Sony.

The foregoing example demonstrates the amplification capability of the transistor. We will study and quantify the behavior of this and other amplifier topologies in the next chapter.

Small-Signal Model of Supply Voltage We have seen that the use of the small-signal model of diodes and transistors can simplify the analysis considerably. In such an analysis, other components in the circuit must also be represented by a small-signal model. In particular, we must determine how the supply voltage, $V_{C C}$, behaves with respect to small changes in the currents and voltages of the circuit.

The key principle here is that the supply voltage (ideally) remains constant even though various voltages and currents within the circuit may change with time. Since the supply does not change and since the smallsignal model of the circuit entails only changes in the quantities, we observe that $V_{C C}$ must be replaced with a zero voltage to signify the zero change. Thus, we simply "ground" the supply voltage in small-signal analysis. Similarly, any other constant voltage in the circuit is replaced with a ground connection. To emphasize that such grounding holds for only signals, we sometimes say a node is an "ac ground."

### 4.4.5 Early Effect

Our treatment of the bipolar transistor has thus far concentrated on the fundamental principles, ignoring second-order effects in the device and their representation in the largesignal and small-signal models. However, some circuits require attention to such effects if meaningful results are to be obtained. The following example illustrates this point.

| Example | Considering the circuit of Example 4.11 , suppose we raise $R_{C}$ to $200 \Omega$ and $V_{C C}$ to 3.6 V. |
| :---: | :--- |
| 4.12 | Verify that the device operates in the active mode and compute the voltage gain. |

Solution The voltage drop across $R_{C}$ now increases to $6.92 \mathrm{~mA} \times 200 \Omega=1.384 \mathrm{~V}$, leading to a collector voltage of $3.6 \mathrm{~V}-1.384 \mathrm{~V}=2.216 \mathrm{~V}$ and guaranteeing operation in the active mode. Note that if $V_{C C}$ is not doubled, then $V_{\text {out }}=1.8 \mathrm{~V}-1.384 \mathrm{~V}=0.416 \mathrm{~V}$ and the transistor is not in the forward active region.

Recall from part (b) of the above example that the change in the output voltage is equal to the change in the collector current multiplied by $R_{C}$. Since $R_{C}$ is doubled, the voltage gain must also double, reaching a value of 53.4. This result is also obtained with the aid of the small-signal model. Illustrated in Fig. 4.26, the
image_name:Figure 4.26
description:
[
name: v1, type: VoltageSource, ports: {Np: Vi, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vi, N2: vπ}
name: RC, type: Resistor, value: 200Ω, ports: {N1: Vout, N2: GND}
name: gmvπ, type: VoltageControlledCurrentSource, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a small-signal model of a transistor amplifier stage. The voltage gain is given by the expression -gm * RC. The current source gmvπ generates a current proportional to the voltage across rπ, affecting the output voltage Vout.

Figure 4.26 Small-signal equivalent circuit of the stage shown in Fig. 4.25.
equivalent circuit yields $v_{\text {out }}=-g_{m} v_{\pi} R_{C}=-g_{m} v_{1} R_{C}$ and hence $v_{\text {out }} / v_{1}=-g_{m} R_{C}$. With $g_{m}=(3.75 \Omega)^{-1}$ and $R_{C}=200 \Omega$, we have $v_{\text {out }} / v_{1}=-53.4$.

Exercise What happens if $R_{C}=250 \Omega$ ?

This example points to an important trend: if $R_{C}$ increases, so does the voltage gain of the circuit. Does this mean that, if $R_{C} \rightarrow \infty$, then the gain also grows indefinitely? Does another mechanism in the circuit, perhaps in the transistor, limit the maximum gain that can be achieved? Indeed, the "Early effect" translates to a nonideality in the device that can limit the gain of amplifiers.

To understand this effect, we return to the internal operation of the transistor and reexamine the claim shown in Fig. 4.11that "the collector current does not depend on the collector voltage." Consider the device shown in Fig. 4.27(a), where the collector voltage is somewhat higher than the base voltage and the reverse bias across the junction creates a certain depletion region width. Now suppose $V_{C E}$ is raised to $V_{C E 2}$ [Fig. 4.27(b)], thus increasing the reverse bias and widening the depletion region in the collector and base areas. Since the base charge profile must still fall to zero at the edge of depletion region, $x_{2}^{\prime}$, the slope of the profile increases. Equivalently, the effective base width, $W_{B}$, in Eq. (4.8) decreases, thereby increasing the collector current. Discovered by Early, this phenomenon poses interesting problems in amplifier design (Chapter 5).
image_name:Figure 4.27 (a)
description:
[
name: VBE, type: VoltageSource, value: VBE, ports: {Np: VBE, Nn: GND}
name: VCE1, type: VoltageSource, value: VCE1, ports: {Np: VCE1, Nn: GND}
name: VCE2, type: VoltageSource, value: VCE2, ports: {Np: VCE2, Nn: GND}
]
extrainfo:The circuit illustrates the Early effect in bipolar transistors, showing two configurations with different collector-emitter voltages (VCE1 and VCE2). The increase in VCE widens the depletion region and affects the base charge profile.

(a)
(b)

Figure 4.27 (a) Bipolar device with base and collector bias voltages, (b) effect of higher collector voltage.

How is the Early effect represented in the transistor model? We must first modify Eq. (4.9) to include this effect. It can be proved that the rise in the collector current with $V_{C E}$ can be approximately expressed by a multiplicative factor:

$$
\begin{align*}
I_{C} & =\frac{A_{E} q D_{n} n_{i}^{2}}{N_{E} W_{B}}\left(\exp \frac{V_{B E}}{V_{T}}-1\right)\left(1+\frac{V_{C E}}{V_{A}}\right)  \tag{4.66}\\
& \approx\left(I_{S} \exp \frac{V_{B E}}{V_{T}}\right)\left(1+\frac{V_{C E}}{V_{A}}\right) \tag{4.67}
\end{align*}
$$

where $W_{B}$ is assumed constant and the second factor, $1+V_{C E} / V_{A}$, models the Early effect. The quantity $V_{A}$ is called the "Early voltage."
image_name:(a)
description:The graph labeled (a) in the image represents the collector current \( I_C \) as a function of the base-emitter voltage \( V_{BE} \). The graph is a plot that examines the influence of the Early effect on the transistor's behavior.

1. **Type of Graph and Function:**
- This is a plot of \( I_C \) versus \( V_{BE} \) for a bipolar junction transistor (BJT), showing the effects of the Early effect.

2. **Axes Labels and Units:**
- The horizontal axis represents the base-emitter voltage \( V_{BE} \) (in volts), and the vertical axis represents the collector current \( I_C \) (in amperes).
- The scales for both axes are linear.

3. **Overall Behavior and Trends:**
- The graph shows an exponential increase in collector current \( I_C \) with increasing \( V_{BE} \).
- Two curves are depicted: one with the Early effect and one without.
- The curve labeled "With Early Effect" shows a steeper slope compared to the "Without Early Effect" curve, indicating a more pronounced increase in \( I_C \) for a given \( V_{BE} \).

4. **Key Features and Technical Details:**
- The Early effect causes the slope of the \( I_C \) versus \( V_{BE} \) curve to increase, reflecting a higher sensitivity of \( I_C \) to changes in \( V_{BE} \).
- The graph visually demonstrates the impact of the Early voltage \( V_A \), which modifies the collector current's response to \( V_{BE} \).

5. **Annotations and Specific Data Points:**
- The graph includes annotations indicating the presence or absence of the Early effect.
- No specific numerical values or critical points are marked on this graph, but the trend lines clearly illustrate the difference in behavior with and without the Early effect.
image_name:(b)
description:The graph labeled (b) in the provided context is a plot of collector current ($I_C$) versus collector-emitter voltage ($V_{CE}$). This graph illustrates the influence of the Early effect on the $I_C-V_{CE}$ characteristic of a bipolar junction transistor.

1. **Type of Graph and Function:**
- This is a characteristic curve graph showing the relationship between collector current and collector-emitter voltage.

2. **Axes Labels and Units:**
- The x-axis represents the collector-emitter voltage, $V_{CE}$.
- The y-axis represents the collector current, $I_C$.
- There are no specific units or scales indicated, but typically $V_{CE}$ is measured in volts and $I_C$ in amperes or milliamperes.

3. **Overall Behavior and Trends:**
- Without the Early effect, the graph shows a horizontal line, indicating that the collector current $I_C$ remains constant as $V_{CE}$ increases, after reaching a certain threshold, typical of ideal transistor behavior.
- With the Early effect, the graph exhibits a slight positive slope, indicating that $I_C$ increases linearly with $V_{CE}$. This demonstrates the Early effect, where $I_C$ is not entirely independent of $V_{CE}$ due to the modulation of the effective base width.

4. **Key Features and Technical Details:**
- The Early effect introduces a linear relationship between $I_C$ and $V_{CE}$, resulting in a non-zero slope. This slope reflects the impact of the Early voltage, $V_A$, on the transistor's performance.
- The graph with Early effect is represented by a solid line, while the graph without Early effect is depicted as a dashed line.

5. **Annotations and Specific Data Points:**
- The graph is annotated to clearly differentiate between the behaviors with and without the Early effect, using arrows and labels to indicate the respective curves.
- The constant level of $I_C$ without Early effect is marked by a dashed line parallel to the x-axis, whereas the line with Early effect slopes upwards, indicating the increase in $I_C$ with $V_{CE}$.

Overall, this graph effectively illustrates the Early effect's impact on the collector current as a function of the collector-emitter voltage, highlighting the deviation from ideal behavior in real-world transistors.

Figure 4.28 Collector current as a function of (a) $V_{B E}$ and (b) $V_{C E}$ with and without Early effect.

It is instructive to examine the I/V characteristics of Fig. 4.15 in the presence of the Early effect. For a constant $V_{C E}$, the dependence of $I_{C}$ upon $V_{B E}$ remains exponential but with a somewhat greater slope [Fig. 4.28(a)]. On the other hand, for a constant $V_{B E}$, the $I_{C}-V_{C E}$ characteristic displays a nonzero slope [Fig. 4.28(b)]. In fact, differentiation of Eq. (4.67) with respect to $V_{C E}$ yields

$$
\begin{align*}
\frac{\delta I_{C}}{\delta V_{C E}} & =I_{S}\left(\exp \frac{V_{B E}}{V_{T}}\right)\left(\frac{1}{V_{A}}\right)  \tag{4.68}\\
& \approx \frac{I_{C}}{V_{A}} \tag{4.69}
\end{align*}
$$

where it is assumed $V_{C E} \ll V_{A}$ and hence $I_{C} \approx I_{S} \exp \left(V_{B E} / V_{T}\right)$. This is a reasonable approximation in most cases.

The variation of $I_{C}$ with $V_{C E}$ in Fig. 4.28(b) reveals that the transistor in fact does not operate as an ideal current source, requiring modification of the perspective shown in Fig. 4.11(a). The transistor can still be viewed as a two-terminal device but with a current that varies to some extent with $V_{C E}$ (Fig. 4.29).
image_name:Figure 4.29
description:
[
name: Q1, type: NPN, ports: {C: X, B: V1, E: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
]
extrainfo:The diagram illustrates a realistic model of a bipolar transistor as a current source. The current through the transistor is expressed as I_S exp(V1/V_T) (1 + Vx/V_A), indicating that the current depends on both V1 and Vx.

Figure 4.29 Realistic model of bipolar transistor as a current source.

[^0]:    ${ }^{67}$ Recall from Eq. (2.109) that a tenfold change in a diode's current translates to a $60-\mathrm{mV}$ change in its voltage.

[^1]:    ${ }^{8}$ This is also to be expected. Writing Eq. (3.45) to obtain the change in $I_{D}$ for a small change in $V_{D}$ is in fact equivalent to taking the derivative.

[^2]:    ${ }^{9}$ The function $\exp (a \sin b t)$ can be approximated by a Taylor expansion or Bessel functions.

[^3]:    ${ }^{10} \mathrm{~A}$ cellphone in reality draws a much higher current.

[^4]:    ${ }^{12}$ The water pipe analogy in Fig. 3.3(c) proves useful here.

[^5]:    ${ }^{13}$ This circuit is also called a "peak detector."

[^6]:    *This section can be skipped in a first reading.

[^7]:    ${ }^{34}$ Recall that $I=C I V / d t$ and hence $d V=(I / C) d t$.

[^8]:    ${ }^{15}$ The four diodes are typically manufactured in a single package having four terminals.

[^9]:    *This section can be skipped in a first reading.
${ }^{17}$ Voltage doublers are an example of "dc-dc converters."

[^10]:    ${ }^{18}$ If we assume $D_{1}$ does not turn on, then the circuit resembles that in Fig. 3.54(a), requiring that $V_{\text {out }}$ rise and $D_{1}$ turn on.

[^11]:    ${ }^{19}$ As always, the reader is encouraged to assume otherwise (i.e., $D_{1}$ remains off) and arrive at a conflicting result.

[^12]:    ${ }^{20} \mathrm{As}$ usual, $I_{D 1}$ denotes the current flowing from the anode to the cathode.

[^13]:    *This section can be skipped in a first reading.
${ }^{21}$ The diode is drawn vertically to emphasize that $V_{\text {out }}$ is lower than $V_{\text {in }}$.

[^14]:    ${ }^{1}$ This assumption simplifies the analysis here but may not hold in the general case.

[^15]:    ${ }^{2}$ In an npn transistor, electrons go from the emitter to the collector. Thus, the conventional direction of the current is from the collector to the emitter.

[^16]:    ${ }^{3}$ Recall that $V_{C E}>V_{1}$ is necessary to ensure the collector-base junction remains reverse biased.

[^17]:    ${ }^{4} \mathrm{~A} 500-\mathrm{mV}$ change in $V_{B E}$ leads to $500 \mathrm{mV} / 60 \mathrm{mV}=8.3$ decades of change in $I_{C}$.

[^18]:    ${ }^{5}$ Unless otherwise stated, we use the term "bias current" to refer to the collector bias current.

A bipolar transistor carries a collector current of 1 mA with $V_{C E}=2 \mathrm{~V}$. Determine the 4.13 required base-emitter voltage if $V_{A}=\infty$ or $V_{A}=20 \mathrm{~V}$. Assume $I_{S}=2 \times 10^{-16} \mathrm{~A}$.

Solution With $V_{A}=\infty$, we have from Eq. (4.67)

$$
\begin{align*}
V_{B E} & =V_{T} \ln \frac{I_{C}}{I_{S}}  \tag{4.70}\\
& =760.3 \mathrm{mV} \tag{4.71}
\end{align*}
$$

If $V_{A}=20 \mathrm{~V}$, we rewrite Eq. (4.67) as

$$
\begin{align*}
V_{B E} & =V_{T} \ln \left(\frac{I_{C}}{I_{S}} \frac{1}{1+\frac{V_{C E}}{V_{A}}}\right)  \tag{4.72}\\
& =757.8 \mathrm{mV} \tag{4.73}
\end{align*}
$$

In fact, for $V_{C E} \ll V_{A}$, we have $\left(1+V_{C E} / V_{A}\right)^{-1} \approx 1-V_{C E} / V_{A}$

$$
\begin{align*}
V_{B E} & \approx V_{T} \ln \frac{I_{C}}{I_{S}}+V_{T} \ln \left(1-\frac{V_{C E}}{V_{A}}\right)  \tag{4.74}\\
& \approx V_{T} \ln \frac{I_{C}}{I_{S}}-V_{T} \frac{V_{C E}}{V_{A}} \tag{4.75}
\end{align*}
$$

where it is assumed $\ln (1-\epsilon) \approx-\epsilon$ for $\epsilon \ll 1$.
Exercise Repeat the above example if two such transistors are placed in parallel.

Large-Signal and Small-Signal Models The presence of Early effect alters the transistor models developed in Sections 4.4.1 and 4.4.4. The large-signal model of Fig. 4.13 must now be modified to that in Fig. 4.30, where

$$
\begin{align*}
I_{C} & =\left(I_{S} \exp \frac{V_{B E}}{V_{T}}\right)\left(1+\frac{V_{C E}}{V_{A}}\right)  \tag{4.76}\\
I_{B} & =\frac{1}{\beta}\left(I_{S} \exp \frac{V_{B E}}{V_{T}}\right)  \tag{4.77}\\
I_{E} & =I_{C}+I_{B} \tag{4.78}
\end{align*}
$$

Note that $I_{B}$ is independent of $V_{C E}$ and still given by the base-emitter voltage.
image_name:Figure 4.30
description:
[
name: Q1, type: NPN, ports: {C: C, B: A, E: k}
name: D1, type: Diode, ports: {Na: A, Nc: k}
name: I1, type: CurrentSource, ports: {Np: C, Nn: k}
]
extrainfo:The circuit diagram shows a large-signal model of a bipolar transistor including the Early effect. It includes an NPN transistor Q1 with its collector at node C, base at node A, and emitter at node k. A diode D1 is connected between nodes A and k, and a current source I1 is connected between nodes C and k.

Figure 4.30 Large-signal model of bipolar transistor including Early effect.

For the small-signal model, we note that the controlled current source remains unchanged and $g_{m}$ is expressed as

$$
\begin{align*}
g_{m} & =\frac{d I_{C}}{d V_{B E}}  \tag{4.79}\\
& =\frac{1}{V_{T}}\left(I_{S} \exp \frac{V_{B E}}{V_{T}}\right)\left(1+\frac{V_{C E}}{V_{A}}\right)  \tag{4.80}\\
& =\frac{I_{C}}{V_{T}} \tag{4.81}
\end{align*}
$$

Similarly,

$$
\begin{align*}
r_{\pi} & =\frac{\beta}{g_{m}}  \tag{4.82}\\
& =\beta \frac{V_{T}}{I_{C}} \tag{4.83}
\end{align*}
$$

Considering that the collector current does vary with $V_{C E}$, let us now apply a voltage change at the collector and measure the resulting current change [Fig. 4.31(a)]:

$$
\begin{equation*}
I_{C}+\Delta I_{C}=\left(I_{S} \exp \frac{V_{B E}}{V_{T}}\right)\left(1+\frac{V_{C E}+\Delta V_{C E}}{V_{A}}\right) \tag{4.84}
\end{equation*}
$$

It follows that

$$
\begin{equation*}
\Delta I_{C}=\left(I_{S} \exp \frac{V_{B E}}{V_{T}}\right) \frac{\Delta V_{C E}}{V_{A}} \tag{4.85}
\end{equation*}
$$

which is consistent with Eq. (4.69). Since the voltage and current change correspond to the same two terminals, they satisfy Ohm's Law, yielding an equivalent resistor:

$$
\begin{align*}
r_{O} & =\frac{\Delta V_{C E}}{\Delta I_{C}}  \tag{4.86}\\
& =\frac{V_{A}}{I_{S} \exp \frac{V_{B E}}{V_{T}}}  \tag{4.87}\\
& \approx \frac{V_{A}}{I_{C}} \tag{4.88}
\end{align*}
$$

Depicted in Fig. 4.31(b), the small-signal model contains only one extra element, $r_{O}$, to represent the Early effect. Called the "output resistance," $r_{O}$ plays a critical role in highgain amplifiers (Chapter 5). Note that both $r_{\pi}$ and $r_{O}$ are inversely proportionally to the bias current, $I_{C}$.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: V, B: V_BE, E: GND}
name: V_BE, type: VoltageSource, value: V_BE, ports: {Np: V_BE, Nn: GND}
name: ΔI_C, type: CurrentSource, value: ΔI_C, ports: {Np: V, Nn: GND}
]
extrainfo:The circuit diagram (a) shows a small-signal model of a transistor biased with a voltage source V_BE and a current source ΔI_C. The transistor Q1 is an NPN type with its base connected to V_BE, collector to node V, and emitter to ground. The diagram illustrates the Early effect with the inclusion of output resistance r_O in the model.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: C, B: B, E: E}
name: VBE, type: VoltageSource, value: VBE, ports: {Np: B, Nn: GND}
name: IC, type: CurrentSource, value: IC, ports: {Np: C, Nn: E}
name: rπ, type: Resistor, value: rπ, ports: {N1: B, N2: E}
name: gmvπ, type: VoltageControlledCurrentSource, value: gmvπ, ports: {Np: C, Nn: E}
name: rO, type: Resistor, value: rO, ports: {N1: C, N2: C}
]
extrainfo:The circuit diagram represents a small-signal model of a transistor including the Early effect. It consists of an NPN transistor, a voltage source for the base-emitter voltage, a current source representing the collector current, a resistor for the base-emitter resistance, a voltage-controlled current source, and a resistor representing the output resistance due to the Early effect.

Figure 4.31 (a) Small change in $V_{C E}$ and (b) small-signal model including Early effect.

| Example |
| :--- |
| 4.14 |

A transistor is biased at a collector current of 1 mA . Determine the small-signal model
if $\beta=100$ and $V_{A}=15 \mathrm{~V}$.

Exercise What early voltage is required if the output resistance must reach $25 \mathrm{k} \Omega$ ?

In the next chapter, we return to Example 4.12 and determine the gain of the amplifier in the presence of the Early effect. We will conclude that the gain is eventually limited by the transistor output resistance, $r_{O}$. Figure 4.32 summarizes the concepts studied in this section.

An important notion that has emerged from our study of the transistor is the concept of biasing. We must create proper dc voltages and currents at the device terminals to accomplish two goals: (1) guarantee operation in the active mode ( $V_{B E}>0, V_{C E} \geq 0$ ); e.g., the load resistance tied to the collector faces an upper limit for a given supply voltage (Example 4.7); (2) establish a collector current that yields the required values for the smallsignal parameters $g_{m}, r_{O}$, and $r_{\pi}$. The analysis of amplifiers in the next chapter exercises these ideas extensively.

Finally, we should remark that the small-signal model of Fig. 4.31(b) does not reflect the high-frequency limitations of the transistor. For example, the base-emitter and basecollector junctions exhibit a depletion-region capacitance that impacts the speed. These properties are studied in Chapter 11.
image_name:Operation in Active Mode
description:
[
name: I_S exp(V_BE/V_T), type: CurrentSource, ports: {Np: C, Nn: E}
name: r_π, type: Resistor, value: r_π, ports: {N1: B, N2: E}
name: g_m V_π, type: CurrentControlledCurrentSource, ports: {Np: C, Nn: E}
name: r_o, type: Resistor, value: r_o, ports: {N1: C, N2: E}
]
extrainfo:The diagram illustrates the operation of a bipolar transistor in active mode, highlighting the large-signal model, small-signal model, and the modified small-signal model considering the Early effect. Key parameters include the collector current I_C, base-emitter voltage V_BE, and collector-emitter voltage V_CE. The models show how these parameters influence the transistor's behavior in active mode.
image_name:I/V Characteristics
description:The graph labeled "I/V Characteristics" is a plot typically used to illustrate the current-voltage relationship in a bipolar junction transistor (BJT). The graph is part of a larger diagram showing different models and aspects of BJT operation.

1. Type of Graph and Function:
- **Type:** This is an I/V characteristics graph, commonly used in electronic engineering to show the relationship between collector current (I_C) and base-emitter voltage (V_BE).

2. Axes Labels and Units:
- **X-Axis:** Represents the base-emitter voltage (V_BE).
- **Y-Axis:** Represents the collector current (I_C).
- **Scale:** The graph appears to be on a linear scale, although specific units are not marked.

3. Overall Behavior and Trends:
- **General Shape:** The graph shows an exponential increase in collector current (I_C) with increasing base-emitter voltage (V_BE). This is typical of the exponential I-V relationship in the forward-active region of a BJT.
- **Trend:** As V_BE increases, I_C increases sharply, indicating the transistor is moving from cutoff to active mode.

4. Key Features and Technical Details:
- **Exponential Growth:** The curve demonstrates the exponential relationship between I_C and V_BE, which is a fundamental characteristic of BJTs.
- **Threshold/Turn-On Voltage:** There is an implicit threshold where the current starts to increase significantly, indicating the turn-on voltage of the transistor.

5. Annotations and Specific Data Points:
- **Reference Line:** There is a reference line at I_S exp(V_BE1/V_T), indicating a specific current level for a given V_BE value.
- **Annotations:** The graph is part of a more comprehensive illustration showing the transition from the large-signal model to the small-signal model, highlighting the exponential relationship of I_C with V_BE.

Overall, this I/V characteristics graph is crucial for understanding how a BJT operates in different regions, particularly in the forward-active mode, and is used to derive small-signal parameters such as transconductance (g_m).
image_name:Early Effect
description:
[
name: V_BE, type: VoltageSource, value: V_BE, ports: {Np: B, Nn: E}
name: V_CE, type: VoltageSource, value: V_CE, ports: {Np: C, Nn: E}
name: I_S, type: CurrentSource, value: I_S, ports: {Np: E, Nn: B}
name: r_π, type: Resistor, value: r_π, ports: {N1: B, N2: E}
name: g_m, type: VoltageControlledCurrentSource, value: g_m, ports: {Np: E, Nn: C}
name: r_o, type: Resistor, value: r_o, ports: {N1: C, N2: E}
]
extrainfo:The diagram illustrates the operation of a bipolar transistor, focusing on the Early effect and its impact on the small-signal model. It includes large-signal and modified small-signal models, highlighting parameters like g_m, r_π, and r_o. The Early effect is shown to influence the collector current I_C.

Figure 4.32 Summary of concepts studied thus far.

## 4.5 OPERATION OF BIPOLAR TRANSISTOR

IN SATURATION MODE

As mentioned in the previous section, it is desirable to operate bipolar devices in the forward active region, where they act as voltage-controlled current sources. In this section, we study the behavior of the device outside this region and the resulting difficulties.

Let us set $V_{B E}$ to a typical value, e.g., 750 mV , and vary the collector voltage from a high level to a low level [Fig. 4.33(a)]. As $V_{C E}$ approaches $V_{B E}$, and $V_{B C}$ goes from a negative value toward zero, the base-collector junction experiences less reverse bias. For $V_{C E}=V_{B E}$, the junction sustains a zero voltage difference, but its depletion region still absorbs most of the electrons injected by the emitter into the base. But what happens if $V_{C E}<V_{B E}$, i.e., $V_{B C}>0$ and the B-C junction is forward biased? We say the transistor enters the "saturation region." Suppose $V_{C E}=550 \mathrm{mV}$ and hence $V_{B C}=+200 \mathrm{mV}$. We know from Chapter 2 that a typical diode sustaining 200 mV of forward bias carries an extremely small current. ${ }^{1}$ Thus, even in this case the

[^0]image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: VCE, B: VBE, E: GND}
name: V_BE, type: VoltageSource, value: V_BE, ports: {Np: VBE, Nn: GND}
name: V_CE, type: VoltageSource, value: V_CE, ports: {Np: VCE, Nn: GND}
]
extrainfo:The circuit diagram shows a bipolar NPN transistor Q1 with its base connected to a voltage source V_BE and its collector connected to another voltage source V_CE. The emitter is connected to ground. The diagram illustrates the transistor operating in a forward-biased base-collector junction condition, leading to soft saturation.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: VCE, B: VBE, E: GND}
name: V_BE, type: VoltageSource, value: V_BE, ports: {Np: VBE, Nn: GND}
name: V_CE, type: VoltageSource, value: V_CE, ports: {Np: VCE, Nn: GND}
]
extrainfo:The circuit diagram (b) shows a bipolar transistor Q1 with its base-emitter and base-collector junctions forward-biased. The voltage sources V_BE and V_CE are connected to the base-emitter and collector-emitter junctions respectively. The transistor operates in the saturation region with a current flowing from the collector to the base.

Figure 4.33 (a) Bipolar transistor with forward-biased base-collector junction, (b) flow of holes to collector.
transistor continues to operate as in the active mode, and we say the device is in "soft saturation."

If the collector voltage drops further, the B-C junction experiences greater forward bias, carrying a significant current [Fig. 4.33(b)]. Consequently, a large number of holes must be supplied to the base terminal-as if $\beta$ is reduced. In other words, heavy saturation leads to a sharp rise in the base current and hence a rapid fall in $\beta$.

| Example 4.15 | A bipolar transistor is biased with $V_{B E}=750 \mathrm{mV}$ and has a nominal $\beta$ of 100 . How much B-C forward bias can the device tolerate if $\beta$ must not degrade by more than $10 \%$ ? For simplicity, assume base-collector and base-emitter junctions have identical structures and doping levels. |
| :---: | :---: |
| Solution | If the base-collector junction is forward-biased so much that it carries a current equal to one-tenth of the nominal base current, $I_{B}$, then the $\beta$ degrades by $10 \%$. Since $I_{B}=I_{C} / 100$, the B-C junction must carry no more than $I_{C} / 1000$. We therefore ask, what B-C voltage results in a current of $I_{C} / 1000$ if $V_{B E}=750 \mathrm{mV}$ gives a collector current of $I_{C}$ ? Assuming identical B-E and B-C junctions, we have |
|  | $\begin{equation*} V_{B E}-V_{B C}=V_{T} \ln \frac{I_{C}}{I_{S}}-V_{T} \ln \frac{I_{C} / 1000}{I_{S}} \tag{4.95} \end{equation*}$ |
|  | $=V_{T} \ln 1000$ |
|  | 的 180 mV |
|  | That is, $V_{B C}=570 \mathrm{mV}$. |

Exercise Repeat the above example if $V_{B E}=800 \mathrm{mV}$.

It is instructive to study the transistor large-signal model and I-V characteristics in the saturation region. We construct the model as shown in Fig. 4.34(a), including the base-collector diode. Note that the net collector current decreases as the device enters
image_name:(a)
description:
[
name: D_BE, type: Diode, ports: {Na: B, Nc: E}
name: D_BC, type: Diode, ports: {Na: B, Nc: C}
name: I_S1, type: CurrentSource, ports: {Np: C, Nn: E}
name: I_S2, type: CurrentSource, ports: {Np: B, Nn: C}
name: V_BE, type: VoltageSource, value: V_BE, ports: {Np: B, Nn: E}
]
extrainfo:The circuit diagram represents a bipolar transistor model including saturation effects. The base-emitter and base-collector diodes are represented by D_BE and D_BC, respectively. The current sources I_S1 and I_S2 model the exponential current flow based on the base-emitter voltage V_BE. The circuit illustrates how the controlled current is split between the collector and the base-collector diode in saturation.
image_name:(b)
description:
[
name: D_BC, type: Diode, ports: {Na: V_BE, Nc: K}
name: D_BE, type: Diode, ports: {Na: V_BE, Nc: GND}
name: I_S1, type: CurrentSource, ports: {Np: K, Nn: GND}
name: I_S2, type: CurrentSource, ports: {Np: C, Nn: B}
name: V_BE, type: VoltageSource, value: V_BE, ports: {Np: V_BE, Nn: GND}
]
extrainfo:The circuit diagram (b) represents a bipolar transistor model in saturation with an open collector terminal. The diode D_BC is forward-biased, allowing current to flow from node V_BE to node K. The base-emitter voltage source V_BE is connected between V_BE and GND. The current source I_S1 flows from node K to GND, and I_S2 flows from node C to node B.

Figure 4.34 (a) Model of bipolar transistor including saturation effects, (b) case of open collector terminal.
saturation because part of the controlled current $I_{S 1} \exp \left(V_{B E} / V_{T}\right)$ is provided by the B-C diode and need not flow from the collector terminal. In fact, as illustrated in Fig. 4.34(b), if the collector is left open, then $D_{B C}$ is forward-biased so much that its current becomes equal to the controlled current.

The above observations lead to the $I_{C}-V_{C E}$ characteristics depicted in Fig. 4.35, where $I_{C}$ begins to fall for $V_{C E}$ less than $V_{1}$, about a few hundred millivolts. The term "saturation" is used because increasing the base current in this region of operation leads to little change in the collector current.
image_name:Figure 4.35 Transistor I/V characteristics
description:The graph in Figure 4.35 is a plot of the collector current (I_C) versus the collector-emitter voltage (V_CE) for a bipolar junction transistor (BJT), illustrating its I/V characteristics across different regions of operation.

1. **Type of Graph and Function:**
- This is an I/V characteristic curve for a transistor, specifically a BJT.

2. **Axes Labels and Units:**
- The vertical axis represents the collector current (I_C), typically measured in amperes (A).
- The horizontal axis represents the collector-emitter voltage (V_CE), measured in volts (V).
- Both axes appear to use a linear scale.

3. **Overall Behavior and Trends:**
- The graph shows several curves representing different levels of base current.
- For values of V_CE less than a certain threshold voltage V1, the transistor is in the saturation region. In this area, the collector current (I_C) does not significantly increase with an increase in V_CE, indicating a flat or slightly decreasing trend.
- Beyond V1, the transistor enters the forward active region, where I_C increases with V_CE, showing a more linear relationship.

4. **Key Features and Technical Details:**
- The threshold voltage V1 marks the transition from saturation to the forward active region.
- In the saturation region, increasing base current results in minimal change in collector current, indicating the device's limited response to further increases in base current.
- In the forward active region, the collector current increases with increasing V_CE, demonstrating the transistor's amplifying action.

5. **Annotations and Specific Data Points:**
- The graph is annotated with labels for the saturation region and the forward active region, along with schematic symbols of transistors to illustrate the operational mode.
- The vertical dashed line at V1 represents the boundary between these two regions, emphasizing the change in behavior of the transistor's operation.

Figure 4.35 Transistor I/V characteristics in different regions of operation.

In addition to a drop in $\beta$, the speed of bipolar transistors also degrades in saturation (Chapter 11). Thus, electronic circuits rarely allow operation of bipolar devices in this mode. As a rule of thumb, we permit soft saturation with $V_{B C}<400 \mathrm{mV}$ because the current in the B-C junction is negligible, provided that various tolerances in the component values do not drive the device into deep saturation.

It is important to recognize that the transistor simply draws a current from any component tied to its collector, e.g., a resistor. Thus, it is the external component that defines the collector voltage and hence the region of operation.

Example
4.16

For the circuit of Fig. 4.36, determine the relationship between $R_{C}$ and $V_{C C}$ that guarantees operation in soft saturation or active region.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: d1rc, B: VBE, E: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: d1rc}
name: VBE, type: VoltageSource, value: VBE, ports: {Np: VBE, Nn: GND}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
]
extrainfo:The circuit consists of an NPN transistor Q1 with its collector connected to a resistor RC and a voltage source VCC. The base is connected to a voltage source VBE. The emitter is grounded. The collector current IC flows through RC.

(a)
image_name:(b)
description:The graph in Figure 4.36 (b) is a linear plot depicting the acceptable range of the supply voltage \( V_{CC} \) and the collector resistor \( R_{C} \) for a given transistor circuit.

**Axes Labels and Units:**
- The horizontal axis represents the collector resistor \( R_{C} \), likely in ohms, although the unit is not explicitly marked.
- The vertical axis represents the supply voltage \( V_{CC} \), likely in volts.

**Overall Behavior and Trends:**
- The graph shows a linear relationship between \( V_{CC} \) and \( R_{C} \). As \( R_{C} \) increases, \( V_{CC} \) must also increase to remain within the acceptable region.
- The line starts at \( V_{BE} - 400 \) mV on the vertical axis, indicating the minimum voltage threshold.

**Key Features and Technical Details:**
- The solid line represents the boundary condition where \( V_{CC} = I_{C} R_{C} + (V_{BE} - 400 \text{ mV}) \), as derived from the equation \( V_{CC} \geq I_{C} R_{C} + (V_{BE} - 400 \text{ mV}) \).
- The area above this line is labeled as the "Acceptable Region," indicating that for the circuit to operate properly, \( V_{CC} \) must be above this line for a given \( R_{C} \).

**Annotations and Specific Data Points:**
- The graph includes an annotation pointing to the acceptable region, emphasizing the operational limits.
- The starting point of the line at \( V_{BE} - 400 \) mV is a critical reference point for determining the minimum \( V_{CC} \) for any given \( R_{C} \).

(b)

Figure 4.36 (a) Simple stage, (b) acceptable range of $V_{C C}$ and $R_{C}$.

Solution In soft saturation, the collector current is still equal to $I_{S} \exp \left(V_{B E} / V_{T}\right)$. The collector voltage must not fall below the base voltage by more than 400 mV :

$$
\begin{equation*}
V_{C C}-R_{C} I_{C} \geq V_{B E}-400 \mathrm{mV} \tag{4.98}
\end{equation*}
$$

Thus,

$$
\begin{equation*}
V_{C C} \geq I_{C} R_{C}+\left(V_{B E}-400 \mathrm{mV}\right) \tag{4.99}
\end{equation*}
$$

For a given value of $R_{C}, V_{C C}$ must be sufficiently large so that $V_{C C}-I_{C} R_{C}$ still maintains a reasonable collector voltage.

Exercise $\quad$ Determine the maximum tolerable value of $R_{C}$.

In the deep saturation region, the collector-emitter voltage approaches a constant value called $V_{C E, \text { sat }}$ (about 200 mV ). Under this condition, the transistor bears no resemblance to a controlled current source and can be modeled as shown in Fig. 4.37. (The battery tied between C and E indicates that $V_{C E}$ is relatively constant in deep saturation.)
image_name:Figure 4.37 Transistor model in deep saturation
description:
[
name: 800 mV, type: VoltageSource, value: 800 mV, ports: {Np: B, Nn: E}
name: 200 mV, type: VoltageSource, value: 200 mV, ports: {Np: C, Nn: E}
]
extrainfo:The circuit represents a transistor model in deep saturation with two voltage sources connected between the base, collector, and emitter.

Figure 4.37 Transistor model in deep saturation.

## 4.6 THE PNP TRANSISTOR

We have thus far studied the structure and properties of the $n p n$ transistor, i.e., with the emitter and collector made of $n$-type materials and the base made of a $p$-type material. We may naturally wonder if the dopant polarities can be inverted in the three regions, forming a "pnp" device. More importantly, we may wonder why such a device would be useful.

### 4.6.1 Structure and Operation

Figure 4.38(a) shows the structure of a pnp transistor, emphasizing that the emitter is heavily doped. As with the npn counterpart, operation in the active region requires forwardbiasing the base-emitter junction and reverse-biasing the collector junction. Thus, $V_{B E}<0$ and $V_{B C}>0$. Under this condition, majority carriers in the emitter (holes) are injected into the base and swept away into the collector. Also, a linear profile of holes is formed in the base region to allow diffusion. A small number of base majority carriers (electrons) are injected into the emitter or recombined with the holes in the base region, thus creating the base current. Figure 4.38(b) illustrates the flow of the carriers. All of the operation principles and equations described for $n p n$ transistors apply to $p n p$ devices as well.
image_name:(a) Structure of pnp transistor
description:
[
name: Q1, type: PNP, ports: {C: x, B: -VBE, E: GND}
name: VBE, type: VoltageSource, value: VBE, ports: {Np: GND, Nn: -VBE}
name: VCE, type: VoltageSource, value: VCE, ports: {Np: x, Nn: GND}
]
extrainfo:The diagram shows the structure of a PNP transistor with two voltage sources, VBE and VCE, properly biased. The transistor operates with the collector at node x, the base at node -VBE, and the emitter at ground. The hole density and current flow are indicated within the transistor.

(a)
image_name:(c)
description:
[
name: Q1, type: PNP, ports: {C: x, B: -VBE, E: GND}
name: VBE, type: VoltageSource, value: VBE, ports: {Np: GND, Nn: -VBE}
name: VCE, type: VoltageSource, value: VCE, ports: {Np: x, Nn: GND}
]
extrainfo:The diagram shows a PNP transistor Q1 with voltage sources VBE and VCE. The collector is at node x, the base at node -VBE, and the emitter at ground. The transistor is properly biased for operation.

image_name:(b)
description:The image depicts the internal structure and current flow of a PNP transistor. The transistor is shown with three distinct layers: two p-type semiconductor layers sandwiching an n-type layer. The top and bottom layers are labeled 'p', and the middle layer is labeled 'n', representing the PNP configuration.

1. **Components and Structure**:
- The diagram shows a PNP transistor with its internal layers marked as p+, n-, and p.
- Arrows indicate the flow of holes (h+) and electrons (e-).
- The diagram includes voltage sources labeled VBE and VCE.

2. **Connections and Interactions**:
- The base of the transistor is connected to a voltage source labeled VBE, with its negative terminal connected to a point marked as -VBE.
- The collector is connected to another voltage source labeled VCE, with its negative terminal connected to a point marked as -VCE.
- The emitter is grounded (GND).
- The diagram illustrates the flow of holes (h+) from the emitter to the collector, indicating the direction of conventional current flow in a PNP transistor.
- Electrons (e-) flow from the base to the emitter, indicating the direction of electron flow.

3. **Labels, Annotations, and Key Features**:
- The image is annotated with voltage labels VBE and VCE, indicating the biasing voltages applied to the transistor.
- The ground symbol is used to denote the emitter's connection to ground.
- The arrows within the layers show the movement of charge carriers, with a large arrow indicating the hole current (h+) and a smaller arrow indicating the electron current (e-).

Overall, the diagram provides a clear visualization of the PNP transistor's structure, the direction of current flow, and the biasing configuration necessary for its operation.

(b)
image_name:Figure 4.38 (c)
description:
[
name: Q1, type: PNP, ports: {C: VCE, B: b, E: GND}
name: V_BE, type: VoltageSource, value: V_BE, ports: {Np: b, Nn: GND}
name: V_CE, type: VoltageSource, value: V_CE, ports: {Np: VCE, Nn: GND}
]
extrainfo:The diagram shows a PNP transistor Q1 with its collector connected to V_CE, base to V_BE, and emitter to ground. The biasing voltages V_BE and V_CE are used to maintain the transistor in the active region. Current directions are indicated as I_E for emitter current, I_C for collector current, and I_B for base current.

Figure 4.38 (a) Structure of pnp transistor, (b) current flow in pnp transistor, (c) proper biasing, (d) more intuitive view of (c).

Figure 4.38(c) depicts the symbol of the pnp transistor along with constant voltage sources that bias the device in the active region. In contrast to the biasing of the $n p n$ transistor in Fig. 4.6, here the base and collector voltages are lower than the emitter voltage. Following our convention of placing more positive nodes on the top of the page, we redraw the circuit as in Fig. 4.38(d) to emphasize $V_{E B}>0$ and $V_{B C}>0$ and to illustrate the actual direction of current flow into each terminal.

### 4.6.2 Large-Signal Model

The current and voltage polarities in $n p n$ and $p n p$ transistors can be confusing. We address this issue by making the following observations. (1) The (conventional) current always flows from a positive supply (i.e., top of the page) toward a lower potential (i.e., bottom of the page). Figure 4.39(a) shows two branches employing $n p n$ and $p n p$ transistors, illustrating that the (conventional) current flows from collector to emitter in npn devices and from emitter to collector in pnp counterparts. Since the base current must be included in the emitter current, we note that $I_{B 1}$ and $I_{C 1}$ add up to $I_{E 1}$, whereas $I_{E 2}$ "loses" $I_{B 2}$ before emerging as $I_{C 2}$. (2) The distinction between active and saturation regions is based on the
image_name:Figure 4.39(a)
description:
[
name: Q1, type: NPN, ports: {C: R1, B: LOAD, E: GND}
name: Q2, type: PNP, ports: {C: VCC, B: LOAD, E: R2}
name: R1, type: Resistor, value: R1, ports: {N1: VCC, N2: Q1}
name: R2, type: Resistor, value: R2, ports: {N1: Q2, N2: GND}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
]
extrainfo:The circuit includes an NPN transistor Q1 and a PNP transistor Q2, configured to demonstrate current flow from collector to emitter in NPN and from emitter to collector in PNP. R1 and R2 are connected to the collectors of Q1 and Q2, respectively. The VCC voltage source powers the circuit.

(a)
image_name:Active Mode
description:
[
name: Q1, type: NPN, ports: {C: LOAD, B: LOAD, E: LOAD}
]
extrainfo:The circuit diagram 'Active Mode' includes an NPN transistor Q1. It is connected to a load at the collector, base, and emitter, indicating a configuration where the transistor is in active mode. The '+' and '-' signs suggest a voltage source is applied across the load.

image_name:Active Mode
description:
[
name: Q1, type: NPN, ports: {C: LOAD, B: LOAD, E: LOAD}
]
extrainfo:The circuit diagram 'Active Mode' includes an NPN transistor Q1. It is connected to a load at the collector, base, and emitter, indicating a configuration where the transistor is in active mode. The '+' and '-' signs suggest a voltage source is applied across the load.

image_name:Edge of Saturation
description:
[
name: Q1, type: NPN, ports: {C: LOAD, B: LOAD, E: LOAD}
]
extrainfo:The circuit diagram 'Edge of Saturation' includes an NPN transistor Q1. It is connected to a load at the collector, base, and emitter, indicating a configuration where the transistor is at the edge of saturation. The '+' and '-' signs suggest a voltage source is applied across the load.

LOAD
image_name:Edge of Saturation
description:
[
name: Q1, type: NPN, ports: {C: LOAD, B: LOAD, E: LOAD}
]
extrainfo:The circuit diagram 'Edge of Saturation' includes an NPN transistor Q1. It is connected to a load at the collector, base, and emitter, indicating a configuration where the transistor is at the edge of saturation. The '+' and '-' signs suggest a voltage source is applied across the load.

(b)
image_name:Edge of Saturation
description:
[
name: Q1, type: NPN, ports: {C: LOAD, B: LOAD, E: LOAD}
name: Q1, type: PNP, ports: {C: LOAD, B: LOAD, E: LOAD}
]
extrainfo:The circuit diagram 'Edge of Saturation' includes two transistors, one NPN and one PNP, both labeled Q1. They are both connected to a load at the collector, base, and emitter, indicating they are in saturation mode. A voltage source is applied across the load with marked polarities.

Figure 4.39 (a) Voltage and current polarities in $n p n$ and $p n p$ transistors, (b) illustration of active and saturation regions.

B-C junction bias. The different cases are summarized in Fig. 4.39(b), where the relative position of the base and collector nodes signifies their potential difference. We note that an $n p n$ transistor is in the active mode if the collector (voltage) is not lower than the base (voltage). For the pnp device, on the other hand, the collector must not be higher than the base. (3) The npn current equations (4.23)-(4.25) must be modified as follows for the pnp device:

$$
\begin{align*}
& I_{C}=I_{S} \exp \frac{V_{E B}}{V_{T}}  \tag{4.100}\\
& I_{B}=\frac{I_{S}}{\beta} \exp \frac{V_{E B}}{V_{T}}  \tag{4.101}\\
& I_{E}=\frac{\beta+1}{\beta} I_{S} \exp \frac{V_{E B}}{V_{T}}, \tag{4.102}
\end{align*}
$$

where the current directions are defined in Fig. 4.40. The only difference between the $n p n$ and $p n p$ equations relates to the base-emitter voltage that appears in the
image_name:Figure 4.40 Large-signal model of pnp transistor
description:
[
name: Q1, type: PNP, ports: {C: C, B: B, E: E}
name: D1, type: Diode, ports: {Na: B, Nc: E}
name: I1, type: CurrentSource, ports: {Np: E, Nn: C}
]
extrainfo:The circuit is a large-signal model of a PNP transistor with a diode representing the base-emitter junction and a current source modeling the collector current.

Figure 4.40 Large-signal model of pnp transistor.
exponent, an expected result because $V_{B E}<0$ for pnp devices and must be changed to $V_{E B}$ to create a large exponential term. Also, the Early effect can be included as

$$
\begin{equation*}
I_{C}=\left(I_{S} \exp \frac{V_{E B}}{V_{T}}\right)\left(1+\frac{V_{E C}}{V_{A}}\right) \tag{4.103}
\end{equation*}
$$

Example
4.17

In the circuit shown in Fig. 4.41, determine the terminal currents of $Q_{1}$ and verify operation in the forward active region. Assume $I_{S}=2 \times 10^{-16} \mathrm{~A}$ and $\beta=50$, but $V_{A}=\infty$.
image_name:Figure 4.41
description:
[
name: Q1, type: PNP, ports: {C: X, B: b1, E: Vcc}
name: RC, type: Resistor, value: 200 Ω, ports: {N1: X, N2: GND}
name: VCC, type: VoltageSource, value: 2 V, ports: {Np: Vcc, Nn: GND}
name: 1.2 V, type: VoltageSource, value: 1.2 V, ports: {Np: b1, Nn: GND}
]
extrainfo:The circuit is a simple stage using a PNP transistor with a collector resistor RC connected to ground. The base is connected to a 1.2 V source, and the emitter is connected to a 2 V supply. The transistor operates in the forward active region.

Figure 4.41 Simple stage using a pnp transistor.
Solution We have $V_{E B}=2 \mathrm{~V}-1.2 \mathrm{~V}=0.8 \mathrm{~V}$ and hence

$$
\begin{align*}
I_{C} & =I_{S} \exp \frac{V_{E B}}{V_{T}}  \tag{4.104}\\
& =4.61 \mathrm{~mA} \tag{4.105}
\end{align*}
$$

It follows that

$$
\begin{align*}
I_{B} & =92.2 \mu \mathrm{~A}  \tag{4.106}\\
I_{E} & =4.70 \mathrm{~mA} \tag{4.107}
\end{align*}
$$

We must now compute the collector voltage and hence the bias across the B-C junction. Since $R_{C}$ carries $I_{C}$,

$$
\begin{align*}
V_{X} & =R_{C} I_{C}  \tag{4.108}\\
& =0.922 \mathrm{~V} \tag{4.109}
\end{align*}
$$

which is lower than the base voltage. Invoking the illustration in Fig. 4.39(b), we conclude that $Q_{1}$ operates in the active mode and the use of equations (4.100)-(4.102) is justified.

Exercise What is the maximum value of $R_{C}$ if the transistor must remain in soft saturation?

We should mention that some books assume all of the transistor terminal currents flow into the device, thus requiring that the right-hand side of Eqs. (4.100) and (4.101) be multiplied by a negative sign. We nonetheless continue with our notation as it reflects the actual direction of currents and proves more efficient in the analysis of circuits containing many $n p n$ and $p n p$ transistors.
image_name:Figure 4.42
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: VCC, type: VoltageSource, value: 2.5V, ports: {Np: VCC, Nn: GND}
name: RC, type: Resistor, value: 300Ω, ports: {N1: Vout, N2: VCC}
name: Q1, type: PNP, ports: {C: Vout, B: Vin, E: VCC}
]
extrainfo:The circuit is a PNP transistor stage with bias and small-signal voltages. It is used to determine the output voltage Vout for different input voltages Vin (0 and +5 mV) with a constant saturation current Is of 1.5 × 10^−16 A. The circuit demonstrates the behavior of a PNP transistor in response to small signal inputs.

Exercise Determine $V_{\text {out }}$ if $V_{\text {in }}=-5 \mathrm{mV}$.

### 4.6.3 Small-Signal Model

Since the small-signal model represents changes in the voltages and currents, we expect $n p n$ and $p n p$ transistors to have similar models. Depicted in Fig. 4.43(a), the smallsignal model of the pnp transistor is indeed identical to that of the npn device. Following the convention in Fig. 4.38(d), we sometimes draw the model as shown in Fig. 4.43(b).

The reader may notice that the terminal currents in the small-signal model bear an opposite direction with respect to those in the large-signal model of Fig. 4.40. This is not an inconsistency and is studied in Problem 4.50.

Did you know?

Some of the early low-cost radios used only two germanium (rather than silicon) pnp transistors to form two amplifier stages. (Silicon transistors became manufacturable later.) However, these radios had poor performance and could receive only one or two stations. For this reason, many manufacturers would proudly print the number of the transistors inside a radio on its front panel along with the brand name, e.g., "Admiral-Eight Transistors."
image_name:(a)
description:
[
name: rπ, type: Resistor, value: rπ, ports: {N1: B, N2: E}
name: ro, type: Resistor, value: ro, ports: {N1: C, N2: E}
name: gmvπ, type: VoltageControlledCurrentSource, value: gmvπ, ports: {Np: E, Nn: C}
name: Q1, type: NPN, ports: {C: C, B: B, E: E}
]
extrainfo:The diagram represents a small-signal model of a pnp transistor with resistors rπ and ro, a voltage-controlled current source gmvπ, and an NPN transistor Q1. The circuit is used to illustrate the small-signal behavior and the relationships between the base, collector, and emitter currents and voltages.
image_name:(b)
description:
[
name: Transistor1, type: PNP, ports: {C: C, B: B, E: E}
name: rπ, type: Resistor, value: rπ, ports: {N1: B, N2: E}
name: ro, type: Resistor, value: ro, ports: {N1: C, N2: E}
name: gmvπ, type: VoltageControlledCurrentSource, ports: {Np: E, Nn: C}
]
extrainfo:The circuit diagram is a small-signal model of a PNP transistor with a resistor rπ between base and emitter, a resistor ro between collector and emitter, and a voltage-controlled current source gmvπ between emitter and collector.

Figure 4.43 (a) Small-signal model of $p n p$ transistor, (b) more intuitive view of (a).

The small-signal model of pnp transistors may cause confusion, especially if drawn as in Fig. 4.43(b). In analogy with $n p n$ transistors, one may automatically assume that the "top" terminal is the collector and hence the model in Fig. 4.43(b) is not identical to that in Fig. 4.31(b). We caution the reader about this confusion. A few examples prove helpful here.

Example 4.19

If the collector and base of a bipolar transistor are tied together, a two-terminal device results. Determine the small-signal impedance of the devices shown in Fig. 4.44(a). Assume $V_{A}=\infty$.
image_name:Fig. 4.44(a)
description:
[
name: Q1, type: NPN, ports: {C: b1c1, B: b1c1, E: e1}
name: Q2, type: PNP, ports: {C: b2c2, B: b2c2, E: e2}
]
extrainfo:The circuit contains two transistors, Q1 and Q2. Q1 is an NPN transistor with its collector and base tied together at node b1c1, and its emitter connected to node e1. Q2 is a PNP transistor with its collector and base tied together at node b2c2, and its emitter connected to node e2.

(a)
image_name:Fig. 4.44(a)
description:
[
name: vx, type: VoltageSource, value: vx, ports: {Np: vx, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: vx, N2: vx}
name: gmvπ, type: VoltageControlledCurrentSource, ports: {Np: vx, Nn: GND}
]
extrainfo:The circuit diagram represents a small-signal model of a bipolar transistor Q1. It includes a voltage source vx, a resistor rπ, and a voltage-controlled current source gmvπ. The current ix flows from the voltage source through the resistor to the ground, and the voltage-controlled current source is connected between the node vx and ground.

(b)

Figure 4.44

Solution We replace the bipolar transistor $Q_{1}$ with its small-signal model and apply a small-signal voltage across the device [Fig. 4.44(b)]. Noting that $r_{p i}$ carries a current equal to $v_{X} / r_{\pi}$, we write a KCL at the input node:

$$
\begin{equation*}
\frac{v_{X}}{r_{\pi}}+g_{m} v_{\pi}=i_{X} \tag{4.115}
\end{equation*}
$$

Since $g_{m} r_{\pi}=\beta \gg 1$, we have

$$
\begin{align*}
\frac{v_{X}}{i_{X}} & =\frac{1}{g_{m}+r_{\pi}^{-1}}  \tag{4.116}\\
& \approx \frac{1}{g_{m}}  \tag{4.117}\\
& =\frac{V_{T}}{I_{C}} . \tag{4.118}
\end{align*}
$$

Interestingly, with a bias current of $I_{C}$, the device exhibits an impedance similar to that of a diode carrying the same bias current. We call this structure a "diode-connected transistor." The same results apply to the pnp configuration in Fig. 4.44(a).

What is the impedance of a diode-connected device operating at a current of 1 mA ?

Draw the small-signal equivalent circuits for the topologies shown in Figs. 4.45(a)-(c) and compare the results.
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Vout}
name: Q1, type: NPN, ports: {C: Vout, B: Vin, E: GND}
]
extrainfo:The circuit is a common-emitter amplifier with an NPN transistor Q1. The input voltage Vin is applied to the base of Q1, and the output voltage Vout is taken from the collector. RC is the load resistor connected between VCC and the collector of Q1.

(a)
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Vout}
name: Q1, type: PNP, ports: {C: VCC, B: Vin, E: Vout}
]
extrainfo:The circuit is a common-emitter amplifier with a PNP transistor Q1. The input voltage Vin is applied to the base of Q1, and the output voltage Vout is taken from the emitter. RC is the load resistor connected between VCC and the emitter of Q1.

(b)
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Vout}
name: Q1, type: PNP, ports: {C: VCC, B: Vin, E: Vout}
]
extrainfo:The circuit is a common-emitter amplifier with a PNP transistor Q1. The input voltage Vin is applied to the base of Q1, and the output voltage Vout is taken from the emitter. RC is the load resistor connected between VCC and the emitter of Q1.

(c)
image_name:(d)
description:
[
name: v_in, type: VoltageSource, value: v_in, ports: {Np: Vin, Nn: GND}
name: r_π, type: Resistor, value: r_π, ports: {N1: Vin, N2: GND}
name: v_π, type: VoltageSource, value: v_π, ports: {Np: GND, Nn: GND}
name: g_m v_π, type: CurrentSource, value: g_m v_π, ports: {Np: GND, Nn: Vout}
name: r_o, type: Resistor, value: r_o, ports: {N1: Vout, N2: GND}
name: R_C, type: Resistor, value: R_C, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a small-signal equivalent model of a common-emitter amplifier. It uses a voltage source (v_in) as input, and the output voltage (v_out) is taken across the resistor R_C. The circuit includes a dependent current source (g_m v_π) representing the transistor's transconductance.
image_name:(f)
description:
[
name: v_in, type: VoltageSource, value: v_in, ports: {Np: Vin, Nn: GND}
name: r_π, type: Resistor, value: r_π, ports: {N1: Vin, N2: GND}
name: g_m v_π, type: VoltageControlledCurrentSource, value: g_m v_π, ports: {Np: GND, Nn: Vout}
name: r_o, type: Resistor, value: r_o, ports: {N1: Vout, N2: GND}
name: R_C, type: Resistor, value: R_C, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a small-signal equivalent model of a PNP transistor stage. The input voltage 'v_in' is applied at the base-emitter junction, represented by 'r_π'. The controlled current source 'g_m v_π' models the transistor's transconductance. 'r_o' and 'R_C' are connected at the output node 'Vout', modeling the output impedance and load.

(d)
image_name:(d)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vin, N2: GND}
name: g_mvπ, type: VoltageControlledCurrentSource, value: g_mvπ, ports: {Np: GND, Nn: Vout}
name: rO, type: Resistor, value: rO, ports: {N1: Vout, N2: GND}
name: RC, type: Resistor, value: RC, ports: {N1: Vout, N2: GND}
name: vout, type: VoltageSource, value: vout, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a small-signal equivalent model of a PNP transistor stage. The input voltage 'v_in' is applied at the base-emitter junction, represented by 'r_π'. The controlled current source 'g_m v_π' models the transistor's transconductance. 'r_o' and 'R_C' are connected at the output node 'Vout', modeling the output impedance and load.
image_name:(e)
description:
[
name: v_in, type: VoltageSource, value: v_in, ports: {Np: Vin, Nn: GND}
name: r_π, type: Resistor, value: r_π, ports: {N1: Vin, N2: GND}
name: g_m v_π, type: VoltageControlledCurrentSource, ports: {Np: Vout, Nn: GND}
name: r_O, type: Resistor, value: r_O, ports: {N1: Vout, N2: GND}
name: R_C, type: Resistor, value: R_C, ports: {N1: Vout, N2: GND}
name: v_out, type: VoltageSource, value: v_out, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a small-signal equivalent model of a PNP transistor stage. It includes a voltage source 'v_in' at the input, a resistor 'r_π' modeling the base-emitter junction, and a controlled current source 'g_m v_π' representing the transistor's transconductance. The resistors 'r_O' and 'R_C' are connected at the output node 'Vout', modeling the output impedance and load. The output voltage 'v_out' is measured across the 'Vout' and 'GND' nodes.

(f)

Figure 4.45 (a) Simple stage using an $n p n$ transistor, (b) simple stage using a $p n p$ transistor, (c) another $p n p$ stage, (d) small-signal equivalent of (a), (e) small-signal equivalent of (b),
(f) small-signal equivalent of (f).

Solution As illustrated in Figs. 4.45(d)-(f), we replace each transistor with its small-signal model and ground the supply voltage. It is seen that all three topologies reduce to the same equivalent circuit because $V_{C C}$ is grounded in the small-signal representation.

Exercise
Repeat the preceding example if a resistor is placed between the collector and base of each transistor.
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RC1, type: Resistor, value: RC1, ports: {N1: VCC, N2: C1e2}
name: C1e2, type: Capacitor, value: C1e2, ports: {Np: C1e2, Nn: GND}
name: Q1, type: NPN, ports: {C: C1e2, B: Vin, E: GND}
name: RC2, type: Resistor, value: RC2, ports: {N1: Vout, N2: GND}
name: Q2, type: PNP, ports: {C: Vout, B: C1e2, E: GND}
]
extrainfo:The circuit is a two-stage amplifier using NPN and PNP transistors. The small-signal equivalent circuit simplifies to a common topology with grounded supply voltage.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: r_pi1, type: Resistor, value: r_pi1, ports: {N1: Vin, N2: v_pi1}
name: g_m1_v_pi1, type: CurrentControlledCurrentSource, ports: {Np: v_pi1, Nn: GND}
name: r_O1, type: Resistor, value: r_O1, ports: {N1: v_pi1, N2: GND}
name: RC1, type: Resistor, value: RC1, ports: {N1: v_pi1, N2: GND}
name: r_pi2, type: Resistor, value: r_pi2, ports: {N1: v_pi1, N2: v_pi2}
name: g_m2_v_pi2, type: CurrentControlledCurrentSource, ports: {Np: v_pi2, Nn: GND}
name: r_O2, type: Resistor, value: r_O2, ports: {N1: v_pi2, N2: Vout}
name: RC2, type: Resistor, value: RC2, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a small-signal equivalent for an amplifier stage using NPN and PNP transistors. It includes resistors and current-controlled current sources to model transistor operation.

Exercise Show that the circuit depicted in Fig. 4.47 has the same small-signal model as the above amplifier.
image_name:Figure 4.47
description:
[
name: RC1, type: Resistor, value: RC1, ports: {N1: VCC, N2: Q2.C}
name: RD, type: Resistor, value: RD, ports: {N1: VCC, N2: Vout}
name: Q1, type: NPN, ports: {C: Q2.B, B: Vin, E: GND}
name: Q2, type: NPN, ports: {C: Q2.C, B: Q2.B, E: Q1.C}
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: C1E2, type: Other, ports: {N1: Q2.C, N2: Q1.C}
]
extrainfo:The circuit is a small-signal model for an amplifier stage using two NPN transistors (Q1 and Q2). The input voltage source Vin is connected to the base of Q1. Q1 is connected in a common-emitter configuration, while Q2 is configured as a common-collector stage. The resistors RC1 and RD provide biasing and load for the transistors. The circuit is powered by a VCC voltage source.

Figure 4.47 Stage using two npn devices.

## 4.7 CHAPTER SUMMARY

- A voltage-dependent current source can form an amplifier along with a load resistor. Bipolar transistors are electronic devices that can operate as voltage-dependent current sources.
- The bipolar transistor consists of two pn junctions and three terminals: base, emitter, and collector. The carriers flow from the emitter to the collector and are controlled by the base.
- For proper operation, the base-emitter junction is forward-biased and the basecollector junction reverse-biased (forward active region). Carriers injected by the emitter into the base approach the edge of collector depletion region and are swept away by the high electric field.
- The base terminal must provide a small flow of carriers, some of which go to the emitter and some others recombine in the base region. The ratio of collector current and base current is denoted by $\beta$.
- In the forward active region, the bipolar transistor exhibits an exponential relationship between its collector current and base-emitter voltage.
- In the forward active region, a bipolar transistor behaves as a constant current source.
- The large-signal model of the bipolar transistor consists of an exponential voltagedependent current source tied between the collector and emitter, and a diode (accounting for the base current) tied between the base and emitter.
- The transconductance of a bipolar transistor is given by $g_{m}=I_{C} / V_{T}$ and remains independent of the device dimensions.
- The small-signal model of bipolar transistors consists of a linear voltage-dependent current source, a resistance tied between the base and emitter, and an output resistance.
- If the base-collector junction is forward-biased, the bipolar transistor enters saturation and its performance degrades.
- The small-signal models of $n p n$ and $p n p$ transistors are identical.
