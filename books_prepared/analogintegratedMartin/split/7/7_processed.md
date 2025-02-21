# 7. Biasing, References, and Regulators

Although often ignored during the course of first-pass analog design, a critical factor in determining a circuit's overall performance is the quality of the dc voltage and current sources. This chapter covers the design of circuits used to establish those dc voltages or currents. They are, themselves, sophisticated analog circuits usually employing feedback.

## 7.1 ANALOG INTEGRATED CIRCUIT BIASING

In an analog integrated circuit, many subcircuits work together to generate all of the various dc voltages and currents. These include bias circuits, reference circuits, and regulators. A bias circuit generates the dc voltages required to keep transistors near some desired operating point; of course, as transistor parameters change, either from chip to chip or with changes in temperature, so must the bias voltages. A reference circuit generates a voltage and/or current of a known fixed absolute value (for example, one volt). Finally, a regulator circuit improves the quality of a dc voltage or current, usually decreasing the noise. Fig. 7.1 shows how these circuits may work together to support the analog circuits on a large mixed analog-digital chip.
image_name:Fig. 7.1
description:The system block diagram in Fig. 7.1 represents a large mixed analog-digital integrated circuit, emphasizing the roles of biasing, reference circuits, and voltage regulation.

Main Components:
1. **Voltage Regulator**: This component is connected to the supply voltage \( V_{DD} \) and is responsible for stabilizing the voltage supplied to other components, minimizing noise and voltage fluctuations.
2. **Analog Interface**: This block interfaces with external analog signals, ensuring proper communication and signal translation between the external environment and the internal circuits.
3. **Critical Analog + Biasing**: This block handles critical analog operations and biasing, adjusting the operating points of transistors to accommodate variations in process and temperature.
4. **Analog Circuits**: Two blocks labeled "Analog Circuit" are present, handling various analog processing tasks. They receive inputs from the critical analog and biasing block and are connected to the digital circuit.
5. **Digital Circuit**: This block represents the digital processing part of the chip, interacting with the analog circuits.
6. **Reference Circuit**: Provides a stable reference voltage or current, crucial for maintaining consistent operation across varying conditions.
7. **Bias Circuit**: Adjusts bias voltages to maintain the desired operating points of transistors within the analog circuits.

Flow of Information or Control:
- The **Voltage Regulator** receives the main supply voltage \( V_{DD} \) and distributes regulated power to the analog interface, critical analog + biasing, and analog circuits.
- The **Analog Interface** exchanges signals with external components and passes processed signals to the critical analog + biasing block.
- The **Critical Analog + Biasing** block processes signals and manages biasing, sending outputs to the analog circuits.
- **Analog Circuits** further process these signals and interact with the digital circuit.
- The **Digital Circuit** exchanges signals with the analog circuits, facilitating mixed-signal processing.
- **Reference** and **Bias Circuits** provide necessary voltage and current references to stabilize and adjust the operating conditions of the analog components.

Labels, Annotations, and Key Indicators:
- The diagram is labeled with the main supply voltage \( V_{DD} \) and clearly delineates the flow of signals between analog and digital components.
Overall System Function:
The primary function of this integrated circuit is to facilitate robust mixed-signal processing on a chip by integrating analog and digital components. The arrangement ensures stable operation through regulated power supply, biasing, and reference voltages, enabling the analog circuits to work effectively alongside digital processing units. This integration is crucial for applications requiring precise analog signal handling and digital processing in a single chip.

Fig. 7.1 A large mixed analog-digital integrated circuit emphasizing the role of biasing, references, and regulators.

### 7.1.1 Bias Circuits

Generally, the objective of a bias circuit is to ensure that the dc operating points of the transistors in an analog circuit remain within a desired range. Unlike a reference circuit, this means that the dc outputs of a bias circuit may adjust to process and temperature variations. Several approaches may be taken towards biasing. One is to ensure that circuits are biased to permit constant voltage swings; another is to ensure that constant currents are maintained; yet another is to try to ensure constant gain is maintained. These are

Key Point: A bias circuit generates the dc voltages required to keep transistors near some desired operating point; as transistor parameters change, either from chip to chip or with changes in temperature, so must the bias voltages.
illustrated in the following example.

#### EXAMPLE 7.1

Consider the simple NMOS differential pair in Fig. 7.2 biased, nominally, with $\mathrm{V}_{\text {eff, } 1}=200 \mathrm{mV}$ and $V_{t n}=450 \mathrm{mV}$. With a $10 \%$ decrease in both $\mu_{n} C_{o x}$ and $R$, and a $10 \%$ increase in $V_{t n}$, how must $V_{b}$ change to ensure: a) a constant drain current in the matched differential pair devices $Q_{2,3}$; b) a constant voltage drop across the resistors R ; c) a constant gain.

#### Solution

Assume all MOSFETs are in active mode and obeying a simple square-law voltage-current relationship. Before the $10 \%$ changes, $\mathrm{V}_{\mathrm{b}}=\mathrm{V}_{\mathrm{tn}}+\mathrm{V}_{\text {eff, } 1}=650 \mathrm{mV}$.
a) The drain currents of $Q_{2,3}$ are one-half the drain current in $Q_{1}$,

$$
\mathrm{I}_{\mathrm{D} 1}=\frac{1}{2} \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)\left(\mathrm{V}_{\mathrm{b}}-\mathrm{V}_{\mathrm{tn}}\right)^{2}
$$

Hence, to maintain a constant drain current the gate voltage $\mathrm{V}_{\mathrm{b}}$ will have to increase 45 mV along with $\mathrm{V}_{\mathrm{tn}}$. In addition, the effective gate-source voltage $\mathrm{V}_{\text {eff, } 1}=\mathrm{V}_{\mathrm{b}}-\mathrm{V}_{\mathrm{tn}}$ must change in inverse proportion to changes in $\sqrt{\mu_{n} C_{o x}}$. However, $R$ has only secondary effects on drain current, so little if any change is required in $V_{b}$ in response to small changes in $R$. Therefore,

$$
\mathrm{V}_{\mathrm{b}}=\mathrm{V}_{\mathrm{tn}}+\mathrm{V}_{\mathrm{eff}, 1}=1.1(450 \mathrm{mV})+(200 \mathrm{mV}) /(\sqrt{0.9})=706 \mathrm{mV}
$$

image_name:Fig. 7.2 NMOS differential pair biased by a simple current source
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: s2s3d1, G: Vb}
name: Q2, type: NMOS, ports: {S: s2s3d1, D: Voutn, G: Vin}
name: Q3, type: NMOS, ports: {S: s2s3d1, D: Voutp, G: Vip}
name: R1, type: Resistor, value: R, ports: {N1: Voutn, N2: VDD}
name: R2, type: Resistor, value: R, ports: {N1: Voutp, N2: VDD}
]
extrainfo:This circuit is an NMOS differential pair biased by a simple current source. The differential pair consists of Q2 and Q3, with Q1 acting as the current source. The resistors R1 and R2 are used as load resistors for the differential pair.

Fig. 7.2 NMOS differential pair biased by a simple current source.
b) The voltage drop across $R$ is given by $I_{D 1} R / 2$. In addition to the dependencies described in part (a) above, keeping the voltage drop constant will require the drain current, and hence $\left(V_{b}-V_{t n}\right)$, to change in inverse proportion to changes in R. Therefore,

$$
\mathrm{V}_{\mathrm{b}}=1.1(450 \mathrm{mV})+(200 \mathrm{mV}) /(0.9 \sqrt{0.9})=729 \mathrm{mV}
$$

c) The small-signal gain of the differential pair is $g_{m 2} R$ where it may be shown that

$$
g_{m 2} \propto \mu_{n} C_{o x}\left(V_{b}-V_{t n}\right)
$$

Hence, as in parts (a) and (b), keeping the gain constant demands that $\mathrm{V}_{\mathrm{b}}$ change in direct proportion to any changes in $\mathrm{V}_{\mathrm{tn}}$. Moreover, $\mathrm{V}_{\text {eff, } 1}=\mathrm{V}_{\mathrm{b}}-\mathrm{V}_{\mathrm{tn}}$ must change in inverse proportion to changes in $\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}$ and R . Therefore,

$$
V_{b}=1.1(450 \mathrm{mV})+(200 \mathrm{mV}) /(0.9 \cdot 0.9)=742 \mathrm{mV}
$$

Example 7.1 illustrates the challenge of designing a good bias circuit which must somehow monitor multiple device parameters and automatically adjust multiple analog voltages to achieve a desired effect.

Since bias circuits only support other analog circuits by providing their dc voltages, their area and power consumption represents an overhead cost that a designer will want to minimize. Hence, one bias circuit is usually shared by several subcircuits. An important practical consideration is, therefore, how to distribute the bias circuit outputs without subjecting them to noise and inaccuracies due to component mismatches across the chip.

Most (or all) of a bias circuit's outputs will be the gate (or base) voltages used to bias current sources. When distributing these bias voltages, any devices that are required to operate as a current mirror should be placed within the same subcircuit in close physical proximity to one another to ensure good matching between those devices.

For example, consider the common scenario depicted in Fig. 7.3: a reference current, $\mathrm{I}_{\mathrm{b}}$, is available at one location on an integrated circuit and must be replicated at the drain of NMOS device $Q_{2}$ located at a great distance across the chip. Two methods for generating the gate voltage of $Q_{2}$ are shown. In Fig. 7.3(a), a simple NMOS current mirror is used and the mirror devices are separated by a long wire. In this scheme, the long wire carries zero current and it is hence referred to as "voltage-mode" bias distribution. Inevitable differences between the threshold voltages of $Q_{1}$ and $Q_{2}$, and even the ground potentials at their source and body terminals lead to considerable uncertainty in the resulting current $\mathrm{I}_{\mathrm{c}}$.

In Fig. 7.3(b), PMOS current mirror $Q_{3 / 4}$ is introduced to generate an intermediate current $I_{d}$ that is transmitted across the chip. Unlike Fig. 7.3(a), here the long wire carries a non-zero current making this a "currentmode" approach to bias distribution. It is preferred since both pairs of current mirror devices are co-located, so that their currents may be well-matched. Naturally, the simple current mirrors in Fig. 7.3 may be replaced by high output impedance variants to improve their accuracy, but the basic advantage of current-mode bias distribution remains. Current-mode distribution may consume more power and area than voltage-mode distribution due to the additional devices and bias current required. However, these minor disadvantages are ameliorated by recognizing that $Q_{1}$ and $Q_{3}$ in Fig. $7.3(b)$ can be made quite small and the current $I_{d}$ reduced so that the added power and area are minimal. ${ }^{1}$

Also note that Fig. 7.3(b) includes decoupling capacitors at the gates of all transistors. These are important to filter noise at those nodes and may be implemented as MOS capacitors. The decoupling capacitor is connected to

[^0]image_name:(a)
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: Vg2, G: Vg2}
name: Q2, type: NMOS, ports: {S: GND, D: LOAD2, G: Vg2}
]
extrainfo:The circuit diagram (a) shows two NMOS transistors Q1 and Q2. Both transistors have their sources connected to GND. Q1 has its drain connected to LOAD1 and gate to Vg2, while Q2 has its drain connected to LOAD2 and gate to Vg2. The circuit is part of a bias distribution system with a long wire connecting the Vg2 nodes.
image_name:(b)
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: Vg2, G: Vg2}
name: Q2, type: NMOS, ports: {S: GND, D: LOAD1, G: Vg2}
name: Q3, type: PMOS, ports: {S: VDD, D: Vg2, G: P}
name: Q4, type: PMOS, ports: {S: VDD, D: P, G: P}
name: C1, type: Capacitor, value: C1, ports: {Np: Vb, Nn: P}
name: C2, type: Capacitor, value: C2, ports: {Np: Vg2, Nn: GND}
]
extrainfo:The circuit in Fig. 7.3(b) is a current-mode bias distribution network with decoupling capacitors connected to the gates of all transistors to filter noise. The decoupling capacitors are connected to the positive supply (VDD) to maintain a constant gate-source voltage on Q3 and Q4, ensuring a stable bias current Id.

Fig. 7.3 Two approaches to bias distribution: (a) voltage-mode (not recommended); (b) current-mode.
the positive supply, not ground, because its purpose is to maintain a constant gate-source voltage on $Q_{3}$ and $Q_{4}$. Hence, it is desirable for that gate voltage to track any noise on the positive supply, thereby maintaining a constant bias current $I_{d}$.

### 7.1.2 Reference Circuits

Known absolute values of voltage or current are most useful at the interface between integrated circuits, or between an integrated circuit and some other discrete component. For example, two integrated circuits may be required to interface with a signal swing of one volt. A reference voltage or current may sometimes be derived from the supply voltage, but the supply is not always controlled with sufficient accuracy in which case a ref-

Key Point: A reference circuit generates a voltage and/or current of a known fixed absolute value.
erence voltage or current must be produced by an integrated reference circuit. Unfortunately, although dimensionless quantities may be accurately controlled on integrated circuits (e.g., ratios of device sizes), there are very few dimensioned quantities that do not vary significantly from one integrated circuit to another, or with variations in temperature.

#### EXAMPLE 7.2

Transistor $Q_{1}$ in Fig. 7.4 has an aspect ratio of $W / L=10, \mu_{n} C_{0 x}=190 \mu \mathrm{~A} / \mathrm{V}^{2}$ and $\mathrm{V}_{\mathrm{tn}}=0.45 \mathrm{~V}$. Resistor $R=20 \mathrm{k} \Omega$ and $V_{D D}=1.5 \mathrm{~V}$. How much will $V_{o}$ change if the value of $\mu_{n} C_{o x}$ decreases by $30 \%, R$ decreases by $10 \%, \mathrm{~V}_{\mathrm{tn}}$ increases by 30 mV , and $\mathrm{V}_{\mathrm{DD}}$ increases by 100 mV ?
image_name:Fig. 7.4
description:
[
name: R, type: Resistor, value: R, ports: {N1: VDD, N2: Vo}
name: Q1, type: NMOS, ports: {S: GND, D: Vo, G: Vo}
]
extrainfo:The circuit consists of an NMOS transistor Q1 and a resistor R. The resistor is connected between VDD and the output node Vo, which is also connected to the drain and gate of the NMOS. The source of the NMOS is connected to ground. This configuration is often used to establish a DC voltage at the output Vo.

Fig. 7.4 A simple circuit to establish a dc voltage at $V_{0}$.

#### Solution

Assuming a square-law model for $\mathrm{Q}_{1}$ and neglecting its finite output impedance to get an approximate answer, $\mathrm{V}_{\circ}$ may be found by solving the following equation.

$$
\begin{equation*}
\frac{V_{D D}-V_{0}}{R}=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{o}-V_{t n}\right)^{2} \tag{7.1}
\end{equation*}
$$

Equation (7.1) is a quadratic in $V_{0}$ that has only one valid solution with $V_{0}>V_{t n}$.

$$
\begin{equation*}
\mathrm{V}_{\mathrm{o}}=\mathrm{V}_{\mathrm{tn}}+\frac{1}{\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L}) \mathrm{R}}\left[\sqrt{2\left(\mathrm{~V}_{\mathrm{DD}}-\mathrm{V}_{\mathrm{tn}}\right) \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L}) \mathrm{R}+1}-1\right] \tag{7.2}
\end{equation*}
$$

Substituting the nominal values given above into (7.2) yields $\mathrm{V}_{0}=660 \mathrm{mV}$. Making the prescribed changes to the circuit parameters results in $\mathrm{V}_{\mathrm{o}}=747 \mathrm{mV}$. This represents an increase of $13 \%$ under variations that are quite typical.

The most widely used quantity for generating a reference of high accuracy in integrated circuits (on the order of $1 \%$ or better) has proven to be the bandgap of silicon. It is a constant whose value does not change with variations in temperature, dopant concentrations, or device dimensions. Circuits that produce a voltage proportional to the bandgap of silicon are described in Section 7.3.

### 7.1.3 Regulator Circuits

Key Point: A regulator circuit improves the quality of a dc voltage or current, usually decreasing the noise.

A regulator's main purpose is to produce a voltage which has low noise and from which some current may be drawn. They are common, for example, when a critical analog circuit must operate from the same supply voltage as other circuits. As shown in Fig. 7.5, the other circuits introduce significant noise onto the common supply, but a regulator can maintain a quiet supply for the critical circuitry. Digital circuits in particular are major sources of power supply noise, so regulators are common in mixed analog-digital systems.

The general approach is to use a feedback amplifier operating under the noisy supply to generate a quiet dc voltage that supplies the critical circuit. Hence, the regulated voltage is generally lower than the regulator's supply voltage. Important specifications are the immunity of the regulator's output to variations in supply voltage and in the load current.
image_name:Fig. 7.5
description:The block diagram in Fig. 7.5 illustrates a system designed to maintain a stable supply voltage for a critical analog circuit within a larger system that includes a noisy digital circuit.

1. **Main Components:**
- **Noisy Digital Circuit:** This block represents the part of the system that generates noise on the power supply line. It is connected directly to the main supply voltage, V_DD.
- **Voltage Regulator:** This component is crucial for reducing noise. It takes the noisy supply voltage from V_DD and outputs a regulated voltage, V_reg.
- **Critical Analog Circuit:** This block receives the regulated voltage, V_reg, ensuring it operates with minimal interference from the noise generated by the digital circuit.

2. **Flow of Information or Control:**
- The noisy digital circuit is directly powered by the main supply voltage, V_DD, introducing noise into the system.
- The voltage regulator is connected to V_DD and provides a stable, lower output voltage, V_reg, to the critical analog circuit.
- The critical analog circuit is isolated from the noisy supply by receiving power through the voltage regulator.

3. **Labels, Annotations, and Key Indicators:**
- **V_DD:** Represents the main supply voltage, which is noisy due to the digital circuit.
- **V_reg:** The regulated output voltage from the voltage regulator, which is quieter and used to power the critical analog circuit.

4. **Overall System Function:**
- The primary function of this system is to ensure that the critical analog circuit operates with a clean power supply, free from the noise generated by the digital circuit. The voltage regulator plays a key role by filtering out noise from the main supply voltage, V_DD, and providing a stable output voltage, V_reg, to the sensitive analog components. This arrangement allows the analog circuit to function correctly without being affected by the digital circuit's noise.

Fig. 7.5 A regulator maintains a quiet supply voltage for a critical analog circuit within a larger system having a noisy supply voltage.

## 7.2 ESTABLISHING CONSTANT TRANSCONDUCTANCE

### 7.2.1 Basic Constant-Transconductance Circuit

We have seen that transistor transconductances are perhaps the most important parameters in analog amplifiers that must be stabilized. This stabilization can be achieved by using a circuit approach first proposed in [Steininger, 1990] in which transistor transconductances are matched to the conductance of a resistor. As a result, to a firstorder effect, the transistor transconductances are independent of power-supply voltage as well as process and temperature variations.

The bias circuit is shown in Fig. 7.6. First it is assumed that $(\mathrm{W} / \mathrm{L})_{10}=(\mathrm{W} / \mathrm{L})_{11}$. This equality results in both sides of the circuit having the same current due to the current-mirror pair $Q_{10}, Q_{11}$. As a result, we also must have $I_{D 15}=I_{D 13}$. Now, around the loop consisting of $Q_{13}, Q_{15}$, and $R_{B}$, we have

$$
\begin{equation*}
\mathrm{V}_{\mathrm{GS} 13}=\mathrm{V}_{\mathrm{GS} 15}+\mathrm{I}_{\mathrm{D} 15} \mathrm{R}_{\mathrm{B}} \tag{7.3}
\end{equation*}
$$

and recalling that $\mathrm{V}_{\text {effi }}=\mathrm{V}_{\mathrm{GSi}}-\mathrm{V}_{\mathrm{t}}$, we can subtract the threshold voltage, $V_{t}$, from both sides, resulting in

$$
\begin{equation*}
\mathrm{V}_{\mathrm{eff} 13}=\mathrm{V}_{\mathrm{eff} 15}+\mathrm{I}_{\mathrm{D} 15} \mathrm{R}_{\mathrm{B}} \tag{7.4}
\end{equation*}
$$

This equation can also be written as

$$
\begin{equation*}
\sqrt{\frac{2 \mathrm{I}_{\mathrm{D} 13}}{\mu_{\mathrm{n}} \mathrm{C}_{\text {ox }}(\mathrm{W} / \mathrm{L})_{13}}}=\sqrt{\frac{2 \mathrm{I}_{\mathrm{D} 15}}{\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L})_{15}}}+\mathrm{I}_{\mathrm{D} 15} \mathrm{R}_{\mathrm{B}} \tag{7.5}
\end{equation*}
$$

and since $I_{D 13}=I_{D 15}$, we can also write

$$
\begin{equation*}
\sqrt{\frac{2 \mathrm{I}_{\mathrm{D} 13}}{\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L})_{13}}}=\sqrt{\frac{2 \mathrm{I}_{\mathrm{D} 13}}{\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L})_{15}}}+\mathrm{I}_{\mathrm{D} 13} \mathrm{R}_{\mathrm{B}} \tag{7.6}
\end{equation*}
$$

image_name:Fig. 7.6
description:
[
name: Q10, type: PMOS, ports: {S: VDD, D: x1, G: x1}
name: Q11, type: PMOS, ports: {S: VDD, D: x2, G: x1}
name: Q14, type: NMOS, ports: {S: s14d15, D: x1, G: x2}
name: Q12, type: NMOS, ports: {S: x3, D: x2, G: x2}
name: Q15, type: NMOS, ports: {S: s15, D: s14d15, G: x3}
name: Q13, type: NMOS, ports: {S: GND, D: x3, G: x3}
name: RB, type: Resistor, value: RB, ports: {N1: s15, N2: GND}
]
extrainfo:The circuit is a bias circuit designed for stable transistor transconductance. It includes PMOS and NMOS transistors with resistive loads. The resistors are labeled with their resistance values, and the circuit is configured for predictable operation of n-channel devices.

Fig. 7.6 A bias circuit that gives very predictable and stable transistor transconductances, especially for n-channel devices.

Rearranging, we obtain

$$
\begin{equation*}
\frac{2}{\sqrt{2 \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L})_{13} \mathrm{I}_{\mathrm{D} 13}}}\left[1-\sqrt{\frac{\mathrm{W} / \mathrm{L}_{13}}{\mathrm{~W} / \mathrm{L}_{15}}}\right]=\mathrm{R}_{\mathrm{B}} \tag{7.7}
\end{equation*}
$$

and recalling that $\mathrm{g}_{\mathrm{m} 13}=\sqrt{2 \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{W} / \mathrm{L})_{13} \mathrm{I}_{\mathrm{D} 13}}$ results in the important relationship

$$
\begin{equation*}
\mathrm{g}_{\mathrm{m} 13}=\frac{2\left[1-\sqrt{\frac{(\mathrm{W} / \mathrm{L})_{13}}{(\mathrm{~W} / \mathrm{L})_{15}}}\right]}{\mathrm{R}_{\mathrm{B}}} \tag{7.8}
\end{equation*}
$$

Key Point: A constant-transconductance bias circuit produces a small-signal transconductance that is a fixed fraction of a resistor value, independent of process, temperature, or supply variations.

Thus, the transconductance of $Q_{13}$ is determined by $R_{B}$ and geometric ratios only, independent of power-supply voltages, process parameters, temperature, or any other parameters with large variability. For the special case of $(W / L)_{15}=4(W / L)_{13}$, we have simply

$$
\begin{equation*}
g_{m 13}=\frac{1}{R_{B}} \tag{7.9}
\end{equation*}
$$

Not only is $\mathrm{g}_{\mathrm{m} 13}$ stabilized, but all other transconductances are also stabilized since all transistor currents are derived from the same biasing network, and, therefore, the ratios of the currents are mainly dependent on geometry. For example, for all n-channel transistors,

$$
\begin{equation*}
g_{\mathrm{mi}}=\sqrt{\frac{(\mathrm{W} / \mathrm{L})_{\mathrm{i}} \mathrm{I}_{\mathrm{Di}}}{(\mathrm{~W} / \mathrm{L})_{13} \mathrm{I}_{\mathrm{D} 13}}} \times \mathrm{g}_{\mathrm{m} 13} \tag{7.10}
\end{equation*}
$$

and for all p -channel transistors

$$
\begin{equation*}
g_{m i}=\sqrt{\frac{\mu_{\mathrm{p}}}{\mu_{\mathrm{n}}(W / W / L)_{13} I_{D} I_{D 13}}} \times g_{m 13} \tag{7.11}
\end{equation*}
$$

Key Point: The constant-transconductance bias circuit ensures a constant transconductance in all transistors of the same type as $Q_{13}$. However, the transconductance of transistors of the opposite type will vary.

Since $g_{m 13}$ is an n-channel device, the additional term $\sqrt{\mu_{\mathrm{p}} / \mu_{\mathrm{n}}}$ appears in (7.11) modifying the transconductance of all p-channel devices. This, unfortunately, exhibits large variations from chip-to-chip and small variations with temperature.

The circuit in Fig. 7.6 forms a positive feedback loop, and stability is a significant concern. Transistor $Q_{11}$ acts as a common-source amplifier for any small signals appearing at its gate, having diode-connected $\mathrm{Q}_{13}$ as a load. The resulting signal then appears at the gate of $Q_{15}$, another common-source stage
stor. As long as $R_{B}$ is large enough, this second stage will have a gain much less with $R_{B}$ serving as a degeneration resistor. As long as $R_{B}$ is large enough, this second stage will have a gain much less than unity, ensuring stability of the loop. However, at high frequencies any parasitic capacitance across $R_{B}$ will reduce its impedance and tend to make the circuit unstable [Nicolson, 2004]. If $R_{B}$ is to be a precision off-chip resistor, the parasitic capacitances will be large including the chip pad and board. Therefore, it is usually necessary to implement at least part of the resistance $R_{B}$ on-chip. Unfortunately, on-chip resistances are relatively poorly controlled.

The preceding analysis has ignored many second-order effects such as the transistor output impedance and the body effect. The body effect will modify the equation slightly, but the relationship will still depend primarily on geometry alone. The major limitation is due to the transistor output impedance. Both effects can be mitigated using the modified circuit shown in Fig. 7.7. Here, the pair $Q_{14,15}$ is implemented with PMOS devices which in most CMOS processes permits connection to an independent body terminal. Connecting the source and body of $\mathrm{Q}_{15}$ together eliminates the body effect. Furthermore, an amplifier is used to maintain equal voltages at the transistor drain terminals, thus reducing the effect of finite transistor output impedance. Another advantage of the amplifier is that it reduces the impedance at the drain of $\mathrm{Q}_{15}$, which will reduce the gain around the positive feedback loop $Q_{12-15}$ and improve stability. The negative feedback loop comprising the amplifier and common-source transistors $Q_{12,13}$ may be stabilized by proper sizing of compensation capacitor $C_{C}$.

Unfortunately, both Fig. 7.6 and Fig. 7.7 have a second stable state where all the currents are zero. To guarantee this condition doesn't happen, it is necessary to add a start-up circuit that only affects the operation if all the currents are zero at start up.

A fundamental limitation of constant-transconductance biasing is that at high temperatures, the currents and effective gate-source voltages increase substantially to compensate for decreasing carrier mobility and keep the transconductances stable. This limits signal swings which is particularly problematic under low supply voltages. Since the carrier mobility is proportional to $\mathrm{T}^{-3 / 2}$, this corresponds to a 27 -percent reduction from room temperature ( 300 K ) to $100^{\circ} \mathrm{C}$ ( 373 K ). Thus, the effective gate-source voltages increase by 27 percent to keep the transistor transconductance unchanged since

$$
\begin{equation*}
g_{m i}=\mu_{i} C_{o x}\left(\frac{W}{L}\right)_{i} V_{\text {eff-i }} \tag{7.12}
\end{equation*}
$$

As long as the effective gate-source voltages have not initially been designed to be too large, this limitation is tolerable in most applications. ${ }^{2}$ A typical value for effective gate-source voltages might be 0.2 V to 0.25 V at room temperature.

### 7.2.2 Improved Constant-Transconductance Circuits

It is possible to incorporate wide-swing current mirrors into the constant-transconductance bias circuit described above. This modification greatly minimizes most of the detrimental second-order imperfections caused by the finite-output impedance of the transistors, without greatly restricting signal swings. The complete circuit is shown in Fig. 7.8 [McLaren, 2001]. This circuit is a modification of the circuit described in Fig. 7.6, and has both wide-swing current mirrors and a start-up circuit.
image_name:Fig. 7.7
description:The circuit is a modified bias circuit designed to provide predictable and stable transistor transconductances. It includes wide-swing current mirrors and a start-up circuit to prevent zero-current states. The PMOS transistors Q14 and Q15 form the current mirror with a 4:1 ratio, and NMOS transistors Q12 and Q13 provide constant-transconductance biasing.

Fig. 7.7 A modified bias circuit for giving predictable and stable transistor transconductances.

Key Point: Many bias circuits require auxiliary start-up circuits to prevent them from resting in a zerocurrent state indefinitely.

A constant-transconductance bias is provided by transistors $Q_{12-15}$, so that $g_{m 14}=1 / R_{B}$ as in Fig. 7.7. The resulting current is then mirrored to $Q_{1}$ and used to the generate the PMOS gate bias voltage $\mathrm{V}_{\text {bias-p }}$. Notice that the current density $I_{D} /(W / L)$ of $Q_{13}$ is five times greater than that of $Q_{4}$. Hence, the gate voltage of $Q_{13}$ is suitable for use as the PMOS cascode bias $\bigvee_{\text {casc-p }}$ Similarly, $Q_{3,4,6,7}$ form a wide-swing PMOS cascode current mirror that directs current into $Q_{5}$ with five times greater current density than in $Q_{1}$, so that the gate voltage $V_{G s}$ is a suitable NMOS cascode bias $\mathrm{V}_{\text {casc-n }}$.

An example of a start-up circuit is also shown on the right side of Fig. 7.8. In the event that all currents in the bias loop are zero, $Q_{9}$ will be off. Since $Q_{8}$ operates as a high-impedance load that is always on, the gates of $Q_{10,11}$ will be pulled low. These transistors then will inject currents into the bias loop, which will start up the circuit. Once the loop starts up, $Q_{9}$ will turn on, sourcing all of the current for $Q_{8}$, pulling the gates of $Q_{10,11}$ high, and thereby turning them off so they no longer affect the bias loop. This circuit is only one example of a start-up loop, and there are many other variations. For example, sometimes the n -channel transistor, $\mathrm{Q}_{8}$, is replaced by an actual resistor (perhaps realized using a well resistor).

It is of interest to note that the bias circuit shown consists of four different loops-the main loop with positive feedback, the start-up loop that eventually gets disabled, and the two loops used for establishing the bias voltages for the cascode transistors. These latter two loops also constitute positive feedback but with very little gain. Finally, note that the opamp included in the constant- $g_{m}$ bias loop may itself be biased by the loop.

[^1]image_name:Fig. 7.8
description:The circuit is a constant-transconductance bias circuit with wide-swing cascode current mirrors. It consists of four loops: a main loop with positive feedback, a start-up loop, and two loops for establishing bias voltages for cascode transistors. The opamp in the bias loop may be biased by the loop itself.

SPICE! Simulate this circuit with the provided netlist.

Fig. 7.8 A constant-transconductance bias circuit having wide-swing cascode current mirrors. Shown next to each device are reasonable choices for the device widths normalized to the width of $Q_{1}$ assuming equal gate lengths.

## 7.3 ESTABLISHING CONSTANT VOLTAGES AND CURRENTS

An important analog building block, especially in data acquisition systems, is a voltage reference. Ideally, this block will supply a fixed dc voltage of known amplitude that does not change with temperature. This can be combined with an accurate resistance to provide a stable dc current, if needed. There have been a number of approaches that have been taken to realize voltage references in integrated circuits. These include,

1. Making use of a zener diode that breaks down at a known voltage when reverse biased.
2. Making use of the difference in the threshold voltage between an enhancement transistor and a depletion transistor.
3. Cancelling the negative temperature dependence of a pn junction with a positive temperature dependence from a PTAT (proportional-to-absolute-temperature) circuit.
The first approach is no longer popular because the breakdown voltage of a zener diode is typically larger than the power supplies of modern integrated circuits. The second approach cannot be used when depletion transistors are not available, as is often the case. In addition, although it can be used to make quite stable references, the actual value of the reference is difficult to determine accurately because of the process sensitivity of the difference between the threshold voltage of an enhancement device and a depletion device. For these reasons, the first two approaches are not covered here. Rather, the last approach, which is currently the most popular for both bipolar and CMOS technologies, will be discussed. Voltage references based on the last approach are commonly called "bandgap" voltage references for reasons that will become apparent shortly.

### 7.3.1 Bandgap Voltage Reference Basics

As just mentioned, a bandgap voltage reference is based on subtracting the voltage of a forward-biased diode (or base-emitter junction) having a negative temperature coefficient from a voltage proportional to absolute temperature
image_name:Fig. 7.9
description:The circuit is a simplified bandgap voltage reference. It uses a PTAT generator and an op-amp to create a reference voltage of approximately 1.26 V. The NPN transistor is used to generate a voltage with a negative temperature coefficient, which is then combined with the PTAT voltage to achieve temperature stability.

Fig. 7.9 A simplified circuit of a bandgap voltage reference.
(PTAT). As we shall see, this PTAT voltage is realized by amplifying the voltage difference of two forward-biased base-emitter (or diode) junctions. A bandgap voltage reference system is shown symbolically in Fig. 7.9.

A forward-biased base-emitter junction of a bipolar transistor ${ }^{3}$ has an I-V relationship given by

$$
\begin{equation*}
\mathrm{I}_{\mathrm{C}}=\mathrm{I}_{\mathrm{S}} \mathrm{e}^{\mathrm{qV} \mathrm{~V}_{\mathrm{BE}} / \mathrm{kT}} \tag{7.13}
\end{equation*}
$$

where $I_{S}$ is the transistor scale current and, although not shown, has a strong dependence on temperature.
Writing the base-emitter voltage as a function of collector current and temperature, it can be shown that [Brugler, 1967; Tsividis, 1980]

$$
\begin{equation*}
V_{B E}=V_{G 0}\left(1-\frac{T}{T_{0}}\right)+V_{B E 0} \frac{T}{T_{0}}+\frac{m k T}{q} \ln \left(\frac{T_{0}}{T}\right)+\frac{k T}{q} \ln \left(\frac{J_{C}}{J_{C 0}}\right) \tag{7.14}
\end{equation*}
$$

Here, $\mathrm{V}_{\mathrm{G} 0}$ is the bandgap voltage of silicon extrapolated to 0 K (approximately 1.206 V ), k is Boltzmann's constant, and m is a temperature constant approximately equal to 2.3 . Also, $\mathrm{J}_{\mathrm{c}}$ and T are the collector current density and temperature, respectively, while the subscript 0 designates an appropriate quantity at a reference temperature, $T_{0}$. Specifically, $J_{C 0}$ is the collector current density at the reference temperature, $T_{0}$, whereas $J_{C}$ is the collector current density at the true temperature, T . Also, $\mathrm{V}_{\mathrm{BE} 0}$ is the junction voltage at the reference temperature, $\mathrm{T}_{0}$, whereas $\mathrm{V}_{\mathrm{BE}}$ is the base-emitter junction voltage at the true temperature, T . Note that the junction current is related to the junction current density according to the relationship

$$
\begin{equation*}
\mathrm{I}_{\mathrm{C}}=\mathrm{A}_{\mathrm{E}} \mathrm{~J}_{\mathrm{C}} \tag{7.15}
\end{equation*}
$$

where $A_{E}$ is the effective area of the base-emitter junction. For $\mathrm{I}_{\mathrm{C}}$ constant, $\mathrm{V}_{\mathrm{BE}}$ will have approximately a $-2 \mathrm{mV} /{ }^{\circ} \mathrm{K}$ temperature dependence around room temperature. This negative temperature dependence is cancelled by a PTAT temperature dependence of the amplified difference of two base-emitter junctions biased at fixed but different current densities. Using (7.14), it is seen that if there are two base-emitter junctions biased at currents $J_{2}$ and $J_{1}$, then the difference in their junction voltages is given by

Key Point: An integrated voltage reference is made by adding the forward bias voltage of a pn junction to the difference in the forward voltages of two pn junctions biased at different current densities. Before adding them, these voltages are scaled so that their respective positive and negative temperature coefficients cancel precisely.

$$
\begin{equation*}
\Delta \mathrm{V}_{\mathrm{BE}}=\mathrm{V}_{2}-\mathrm{V}_{1}=\frac{\mathrm{kT}}{\mathrm{q}} \ln \left(\frac{\mathrm{~J}_{2}}{\mathrm{~J}_{1}}\right) \tag{7.16}
\end{equation*}
$$

Thus, the difference in the junction voltages is proportional to absolute temperature. This proportionality is quite accurate and holds even when the collector currents are temperature dependent, as long as their ratio remains fixed.

[^2]
#### EXAMPLE 7.3

Assume two transistors are biased at a current-density ratio of $10: 1$ at $\mathrm{T}=300 \mathrm{~K}$. What is the difference in their base-emitter voltages and what is its temperature dependence?

#### Solution

Using (7.16), we have

$$
\begin{equation*}
\Delta \mathrm{V}_{\mathrm{BE}}=\frac{\mathrm{kT}}{\mathrm{q}} \ln \left(\frac{\mathrm{~J}_{2}}{\mathrm{~J}_{1}}\right)=\frac{1.38 \times 10^{-23}(300)}{1.602 \times 10^{-19}} \ln (10)=59.5 \mathrm{mV} \tag{7.17}
\end{equation*}
$$

Since this voltage is proportional to absolute temperature, after a 1 K temperature increase, the voltage difference will be

$$
\begin{equation*}
\Delta \mathrm{V}_{\mathrm{BE}}=59.5 \mathrm{mV} \frac{301}{300}=59.7 \mathrm{mV} \tag{7.18}
\end{equation*}
$$

Thus, the voltage dependence is $59.5 \mathrm{mV} / 300 \mathrm{~K}$ or $0.198 \mathrm{mV} / \mathrm{K}$. Since the temperature dependence of a single $\mathrm{V}_{\mathrm{BE}}$ is $-2 \mathrm{mV} / \mathrm{K}$, if it is desired to cancel the temperature dependence of a single $\mathrm{V}_{\mathrm{BE}}$, then $\Delta \mathrm{V}_{\mathrm{BE}}$ should be amplified by about a factor of 10 , as explained next.

It will be seen shortly that when realizing a bandgap voltage reference, although the output voltage is temperature independent, the junction currents turn out to be proportional to absolute temperature (assuming the resistors used are temperature independent). Thus, to simplify derivations, we will first assume the junction currents are proportional to absolute temperature. Later, it will be verified that this proportionality relationship is true when circuit realizations are described. We therefore first assume

$$
\begin{equation*}
\frac{J_{i}}{J_{i 0}}=\frac{T}{T_{0}} \tag{7.19}
\end{equation*}
$$

where $J_{i}$ is the current density of the collector current of the $i^{\text {th }}$ transistor, whereas $J_{i 0}$ is the same current density at the reference temperature.

Now, assume that the difference between two base-emitter voltages is multiplied by a factor of K and added to the base-emitter voltage of the junction with the larger current density. Using (7.16) and (7.19) along with (7.14), we have

$$
\begin{align*}
\mathrm{V}_{\text {ref }} & =\mathrm{V}_{\mathrm{BE} 2}+\mathrm{K} \Delta \mathrm{~V}_{\mathrm{BE}} \\
& =\mathrm{V}_{\mathrm{G} 0}+\frac{\mathrm{T}}{\mathrm{~T}_{0}}\left(\mathrm{~V}_{\mathrm{BE}-2-2}-\mathrm{V}_{\mathrm{G} 0}\right)+(\mathrm{m}-1) \frac{\mathrm{kT}}{\mathrm{q}} \ln \left(\frac{\mathrm{~T}_{0}}{\mathrm{~T}}\right)+\mathrm{K} \frac{\mathrm{kT}}{\mathrm{q}} \ln \left(\frac{\mathrm{~J}_{2}}{\mathrm{~J}_{1}}\right) \tag{7.20}
\end{align*}
$$

Equation (7.20) is the fundamental equation giving the relationship between the output voltage of a bandgap voltage reference and temperature. Here, $\mathrm{V}_{\mathrm{BE0-2}}$ is the base-emitter junction voltage of the second transistor at temperature $\mathrm{T}_{0}$. If we want zero temperature dependence at a particular temperature, we can differentiate (7.20) with respect to temperature and set the derivative to zero at the desired reference temperature. From (7.20), we have

$$
\begin{equation*}
\frac{\partial \mathrm{V}_{\text {ref }}}{\partial \mathrm{T}}=\frac{1}{\mathrm{~T}_{0}}\left(\mathrm{~V}_{\mathrm{BE} 0-2}-\mathrm{V}_{\mathrm{G} 0}\right)+\mathrm{K} \frac{\mathrm{k}}{\mathrm{q}} \ln \left(\frac{\mathrm{~J}_{2}}{\mathrm{~J}_{1}}\right)+(\mathrm{m}-1) \frac{\mathrm{k}}{\mathrm{q}}\left[\ln \left(\frac{\mathrm{~T}_{0}}{\mathrm{~T}}\right)-1\right] \tag{7.21}
\end{equation*}
$$

Setting (7.21) equal to zero at $\mathrm{T}=\mathrm{T}_{0}$, we see that for zero temperature dependence at the reference temperature, we need

$$
\begin{equation*}
V_{B E 0-2}+K \frac{k T_{0}}{q} \ln \left(\frac{J_{2}}{J_{1}}\right)=V_{G 0}+(m-1) \frac{k T_{0}}{q} \tag{7.22}
\end{equation*}
$$

The left side of (7.22) is the output voltage $\mathrm{V}_{\text {ref }}$ at $\mathrm{T}=\mathrm{T}_{0}$ from (7.20). Thus for zero temperature dependence at $\mathrm{T}=\mathrm{T}_{0}$, we need

$$
\begin{equation*}
V_{\text {ref- } 0}=V_{G 0}+(m-1) \frac{\mathrm{kT}_{0}}{q} \tag{7.23}
\end{equation*}
$$

For the special case of $\mathrm{T}_{0}=300{ }^{\circ} \mathrm{K}$ and $\mathrm{m}=2.3$, (7.23) implies that

$$
\begin{equation*}
V_{\text {ref-0 }}=1.24 \mathrm{~V} \tag{7.24}
\end{equation*}
$$

for zero temperature dependence. Notice that this value is independent of the current densities chosen. Thus, if a larger current density is chosen, then K must be taken appropriately smaller to achieve the correct reference output voltage. In precision integrated voltage references, this correct output voltage is achieved by trimming at the time the wafer is being tested. From (7.22), the required value for K is

$$
\begin{equation*}
K=\frac{V_{\mathrm{G} 0}+(m-1) \frac{k T_{0}}{q}-V_{B E 0-2}}{\frac{k T_{0}}{q} \ln \left(\frac{J_{2}}{J_{1}}\right)}=\frac{1.24-V_{B E 0-2}}{0.0258 \ln \left(\frac{J_{2}}{J_{1}}\right)} \tag{7.25}
\end{equation*}
$$

at $300{ }^{\circ} \mathrm{K}$.
The reason for the name of the bandgap voltage should now be apparent. Specifically, for zero temperature dependence, the output of a bandgap voltage reference is given by the bandgap voltage plus a small correction term to account for second-order effects.

The output voltage of the reference for temperatures different from the reference is found after backsubstituting (7.22) and (7.23) into (7.20). After some manipulations, the result is

$$
\begin{equation*}
V_{\text {ref }}=V_{G 0}+(m-1) \frac{k T}{q}\left[1+\ln \left(\frac{T_{0}}{T}\right)\right] \tag{7.26}
\end{equation*}
$$

and

$$
\begin{equation*}
\frac{\partial V_{\text {ref }}}{\partial T}=(m-1) \frac{k}{q} \ln \left(\frac{T_{0}}{T}\right) \tag{7.27}
\end{equation*}
$$

These equations can be used to estimate the temperature dependence at temperatures different from the reference temperature. In the next section, a practical bipolar realization of a bandgap reference will be described.

#### EXAMPLE 7.4

Estimate the temperature dependence at $0^{\circ} \mathrm{C}$ for a bandgap voltage reference that was designed to have zero temperature dependence at $20^{\circ} \mathrm{C}$. Present the result as $\mathrm{ppm} / \mathrm{K}$.

#### Solution

Recalling that $0^{\circ} \mathrm{K}$ corresponds to $-273^{\circ} \mathrm{C}$, we can write $\mathrm{T}_{0}=293 \mathrm{~K}$ and $\mathrm{T}=273 \mathrm{~K}$. Substituting these values into (7.27), we have

$$
\begin{equation*}
\frac{\partial \mathrm{V}_{\mathrm{ref}}}{\partial \mathrm{~T}}=(2.3-1) \frac{1.38 \times 10^{-23}}{1.6 \times 10^{-19}} \ln \left(\frac{293}{273}\right)=8 \mu \mathrm{~V} / \mathrm{K} \tag{7.28}
\end{equation*}
$$

For a reference voltage of 1.24 V , a dependency of $8 \mu \mathrm{~V} / \mathrm{K}$ results in

$$
\begin{equation*}
\frac{8 \mu \mathrm{~V} /{ }^{\circ} \mathrm{K}}{1.24 \mathrm{~V}}=6.5 \times 10^{-6} \text { parts } /{ }^{\circ} \mathrm{K}=6.5 \mathrm{ppm} / \mathrm{K} \tag{7.29}
\end{equation*}
$$

where ppm represents parts per million. It should be mentioned here that practical effects result in voltage references with typically 4 to 10 times larger values than this small amount of temperature dependency. It should also be noted that the ideal first-order temperature dependence of this bandgap voltage circuit is $0 \mathrm{ppm} / \mathrm{K}$ at the reference temperature of $20^{\circ} \mathrm{C}$.

### 7.3.2 Circuits for Bandgap References

#### Bipolar Bandgap References

A voltage reference originally proposed in [Brokaw, 1974] has been the basis for many bipolar bandgap references. A simplified schematic of the circuit is shown in Fig. 7.10. The amplifier in the feedback loop keeps the collector voltages of $Q_{1}$ and $Q_{2}$ equal. Since $R_{3}=R_{4}$, this guarantees that both transistors have the same collector currents and collector-emitter voltages. Also, notice that the emitter area of $Q_{1}$ has been taken eight times larger than the emitter area of $Q_{2}$. Therefore, $Q_{2}$ has eight times the current density of $Q_{1}$, resulting in

$$
\begin{equation*}
\frac{J_{2}}{J_{1}}=8 \tag{7.30}
\end{equation*}
$$

We have for the circuit

$$
\begin{equation*}
V_{\text {ref }}=V_{B E 2}+V_{R 1} \tag{7.31}
\end{equation*}
$$

Also

$$
\begin{align*}
V_{\mathrm{R} 1} & =\mathrm{I}_{\mathrm{R} 1} \mathrm{R}_{1} \\
& =2 \mathrm{I}_{\mathrm{R}_{2}} \mathrm{R}_{1} \tag{7.32}
\end{align*}
$$

image_name:Fig. 7.10
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Y, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: X, N2: Y}
name: R3, type: Resistor, value: R3, ports: {N1: VDD, N2: InN(A1)}
name: R4, type: Resistor, value: R4, ports: {N1: VDD, N2: InP(A1)}
name: Q1, type: NPN, ports: {C: InN(A1), B: Vref, E: X}
name: Q2, type: NPN, ports: {C: InP(A1), B: Vref, E: Y}
name: A1, type: OpAmp, ports: {InP: InP(A1), InN: InN(A1), OutP: Vref}
]
extrainfo:This is a simplified schematic of a bipolar bandgap voltage reference. The area of Q1's emitter is eight times that of Q2, resulting in a current density ratio of 8:1. The circuit uses an operational amplifier to maintain a stable reference voltage (Vref). Resistors R3 and R4 are equal and help balance the current through the transistors. The circuit is connected to ground at the bottom of R1.

Fig. 7.10 A simplified schematic of a bipolar bandgap voltage reference.

But

$$
\begin{equation*}
\mathrm{I}_{\mathrm{R} 2}=\frac{\mathrm{V}_{\mathrm{R} 2}}{\mathrm{R}_{2}}=\frac{\mathrm{V}_{\mathrm{BE} 2}-\mathrm{V}_{\mathrm{BE} 1}}{\mathrm{R}_{2}}=\frac{\Delta \mathrm{V}_{\mathrm{BE}}}{\mathrm{R}_{2}} \tag{7.33}
\end{equation*}
$$

Substituting (7.32) and (7.33) into (7.31) gives

$$
\begin{equation*}
\mathrm{V}_{\mathrm{ref}}=\mathrm{V}_{\mathrm{BE} 2}+\frac{2 \mathrm{R}_{1}}{\mathrm{R}_{2}} \Delta \mathrm{~V}_{\mathrm{BE}} \tag{7.34}
\end{equation*}
$$

which is of the form desired to realize a bandgap reference. It is immediately recognizable that

$$
\begin{equation*}
\mathrm{K}=\frac{2 \mathrm{R}_{1}}{\mathrm{R}_{2}} \tag{7.35}
\end{equation*}
$$

Assuming $\mathrm{V}_{\mathrm{BE2}-0}=0.65 \mathrm{~V}$, from (7.25)

$$
\begin{equation*}
\frac{\mathrm{R}_{1}}{\mathrm{R}_{2}}=\frac{1}{2} \times \frac{1.24-0.65}{0.0258 \times \ln (8)}=5.5 \tag{7.36}
\end{equation*}
$$

In an integrated implementation, $R_{1}$ or $R_{2}$ would be trimmed while monitoring $V_{\text {ref }}$ to force it equal to the desired reference voltage. Furthermore, the optimum value for this voltage might be determined empirically during the prototype phase of the design cycle.

Notice also, from (7.16) and (7.33), we have

$$
\begin{equation*}
I_{E 1}=I_{E 2}=I_{R 2}=\frac{\Delta V_{B E}}{R_{2}}=\frac{\frac{k T}{q} \ln \left(\frac{J_{2}}{J_{1}}\right)}{R_{2}} \tag{7.37}
\end{equation*}
$$

implying that all currents are proportional to absolute temperature (assuming that resistor $\mathrm{R}_{2}$ is temperature independent). Thus, as assumed earlier, all currents are indeed PTAT. It is worth mentioning here that PTAT currents are often used to bias many bipolar circuits, as they result in transistor transconductances being independent of temperature. This constant transconductance has the desirable feature that circuit speed is relatively independent of temperature, but, unfortunately, has the undesirable feature that the circuit power dissipation goes up considerably at high temperatures, which makes it more difficult to dissipate the heat.

In applications where it is desirable to have reference voltages larger than 1.24 V , a modified bandgap reference as shown in Fig. 7.11 can be used. It is not difficult to show that the output voltage is now given by

$$
\begin{equation*}
V_{\text {ref-0 }}=\left(1+\frac{\mathrm{R}_{4}}{\mathrm{R}_{5}}\right)\left[\mathrm{V}_{\mathrm{G} 0}+(\mathrm{m}-1) \frac{\mathrm{k} T_{0}}{\mathrm{q}}\right] \cong\left(1+\frac{\mathrm{R}_{4}}{\mathrm{R}_{5}}\right) 1.24 \mathrm{~V} \tag{7.38}
\end{equation*}
$$

Resistor $R_{3}$ has been added to cancel the effects of the finite base currents going through $R_{4}$ and should be chosen according to the formula in the figure. The interested reader is referred to [Brokaw, 1974] for additional details concerning this realization.

#### CMOS Bandgap References

The most popular method for realizing CMOS voltage references also makes use of a bandgap voltage reference despite the fact that independent bipolar transistors are not available. These CMOS circuits rely on using what are commonly called well transistors. These devices are vertical bipolar transistors that use wells as their bases and the substrate as their collectors. In an n well process (a common modern process), these vertical bipolar transistors are

Key Point: The implementation of bandgap references in a CMOS process makes use of bipolar transistors formed using doped well regions in the silicon substrate.
pnp types with their collectors connected to ground, as shown in Fig. 7.12(a). In a p-well process, they would be npn transistors with their collectors connected to the positive power supply, as
image_name:Fig. 7.11
description:The circuit is a bipolar bandgap reference with an output voltage greater than 1.24 V. It uses two NPN transistors (Q1 and Q2) and a set of resistors to generate a stable reference voltage. The resistors R3, R4, and R5 are configured to set the gain and feedback of the operational amplifier. The equation for R3 is provided: R3 = (R2/R1) * (R4 || R5). The area of the emitter of Q1 is eight times that of Q2 (AE1 = 8 * AE2).

Fig. 7.11 A bipolar bandgap with output voltages greater than 1.24 V .
shown in Fig. 7.12(b). These transistors have reasonable current gains, but their main limitation is the series base resistance, which can be high due to the large lateral dimensions between the base contact and the effective emitter region. To minimize errors due to this base resistance, the maximum collector currents through the transistors are usually constrained to be less than 0.1 mA . It is possible to use these transistors to implement bandgap voltage references using configurations similar to those shown in Fig. 7.13(a) for n-well processes [Kujik, 1973] or Fig. 7.13(b) for p-well processes [Ye, 1982].

With respect to the n-well implementation of Fig. 7.13(a), we have

$$
\begin{equation*}
V_{\text {ref }}=V_{E B 1}+V_{R 1} \tag{7.39}
\end{equation*}
$$

Also, assuming the opamp has large gain and that its input terminals are at the same voltage, then

$$
\begin{equation*}
V_{R 2}=V_{E B 1}-V_{E B 2}=\Delta V_{E B} \tag{7.40}
\end{equation*}
$$

Now, since the current through $R_{3}$ is the same as the current through $R_{2}$, we have

$$
\begin{equation*}
\mathrm{V}_{\mathrm{R} 3}=\frac{\mathrm{R}_{3}}{\mathrm{R}_{2}} \mathrm{~V}_{\mathrm{R} 2}=\frac{\mathrm{R}_{3}}{\mathrm{R}_{2}} \Delta \mathrm{~V}_{\mathrm{EB}} \tag{7.41}
\end{equation*}
$$

using (7.40). The opamp feedback also makes the voltage across $R_{1}$ equal to the voltage across $R_{3}$. Using this fact and substituting (7.41) into (7.39) results in

$$
\begin{equation*}
V_{\text {ref }}=V_{E B 1}+\frac{R_{3}}{R_{2}} \Delta V_{E B} \tag{7.42}
\end{equation*}
$$

image_name:Fig. 7.12 (a)
description:The image labeled "Fig. 7.12 (a)" depicts a vertical CMOS well transistor structure implemented using an n-well process. The diagram shows a cross-sectional view of a semiconductor device, illustrating the arrangement of different layers and regions.

1. **Identification of Components and Structure:**
- **n-well:** A region within the p-type substrate where n-type material is diffused. This is typically used to form the body of PMOS transistors.
- **p+ and n+ regions:** These are heavily doped regions. The n+ region is connected to the n-well, while the p+ region forms the source or drain of the transistor.
- **p-substrate:** The base material of the semiconductor, which is p-type in this case.

2. **Connections and Interactions:**
- The n-well is connected via a resistor to the n+ region. This indicates a connection between the n-well and the source/drain of the transistor.
- The p+ region is shown connected to ground, indicating that it likely serves as the source of the PMOS transistor.
- The structure suggests that the transistor is isolated from the substrate by the n-well, which allows for independent control of the transistor body potential.

3. **Labels, Annotations, and Key Features:**
- The diagram includes labels such as "n-well" and "p-substrate," which help in identifying the different regions.
- Ground symbol is used to denote the connection of the p+ region to ground.
- The diagram is a conceptual representation, focusing on the layout and connections rather than specific dimensions or material properties.

Overall, this figure illustrates the basic structure and connections of a vertical CMOS transistor in an n-well process, highlighting the isolation and configuration of the n-well and its associated regions.
image_name:Fig. 7.12 (b)
description:The image labeled "Fig. 7.12 (b)" depicts a vertical CMOS well transistor implemented in a p-well process. The diagram is a cross-sectional view showing the following components:

1. **Substrate and Wells:**
- The main body of the structure is an n-type substrate, which serves as the base for the p-well.
- A p-well is embedded within the n-type substrate.

2. **Transistor Structure:**
- The p-well contains n+ regions that form the source and drain of the NMOS transistor.
- A gate is situated above the p-well between the n+ regions, controlling the channel between the source and drain.

3. **Connections and Interactions:**
- The source of the NMOS transistor is connected to VDD, indicating a power supply connection.
- The drain is connected through a resistor to a p+ region, which is part of the p-well.
- The p-well is connected to ground, ensuring proper biasing and isolation within the n-substrate.

4. **Key Features and Annotations:**
- The diagram is annotated with labels such as "n-substrate," "p-well," and "VDD," which provide information about the material types and electrical connections.
- The ground symbol is used to denote the connection of the p-well to the ground.

This configuration is typical for CMOS processes where p-wells are used to create NMOS transistors, allowing for the integration of both NMOS and PMOS transistors on the same chip, facilitating CMOS technology.

Fig. 7.12 Vertical CMOS well transistors realized in (a) an n-well process and (b) a p-well process.
image_name:(a)Bandgap voltage reference circuit
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vref, N2: InP(A1)}
name: R2, type: Resistor, value: R2, ports: {N1: InN(A1), N2: X}
name: R3, type: Resistor, value: R3, ports: {N1: Vref, N2: InN(A1)}
name: Q1, type: PNP, ports: {c: GND, b: GND, e: InP(A1)}
name: Q2, type: PNP, ports: {c: GND, b: GND, e: X}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Vref}
]
extrainfo:The circuit is a bandgap voltage reference using PMOS transistors Q1 and Q2. Resistors R1, R2, and R3 help set the reference voltage Vref. The operational amplifier A1 stabilizes the output voltage Vref.

image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: VDD, B: Vref, E: InP(A1)}
name: Q2, type: NPN, ports: {C: VDD, B: Vref, E: e2}
name: R1, type: Resistor, value: R1, ports: {N1: InP(A1), N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: e2, N2: InN(A1)}
name: R3, type: Resistor, value: R3, ports: {N1: InN(A1), N2: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Vref}
]
extrainfo:The circuit is a bandgap voltage reference using NPN transistors Q1 and Q2. Resistors R1, R2, and R3 help set the reference voltage Vref. The operational amplifier A1 stabilizes the output voltage Vref. I1 and I2 are currents through resistors R1 and R3 respectively.
Fig. 7.13 Bandgap voltage references implemented with well transistors in (a) an n-well CMOS process, and (b) a p-well CMOS process.
which is in the required form to realize a bandgap reference. In integrated realizations of this reference, the bipolar transistors are often taken the same size, and the different current-densities are realized by taking $\mathrm{R}_{3}$ greater than $R_{1}$, which causes $I_{1}$ to be larger than $I_{2}$. In this case, we would have

$$
\begin{equation*}
\frac{J_{1}}{J_{2}}=\frac{R_{3}}{R_{1}} \tag{7.43}
\end{equation*}
$$

since $R_{1}$ and $R_{3}$ have the same voltage across them. Also, recalling from (7.16) that

$$
\begin{equation*}
\Delta \mathrm{V}_{\mathrm{EB}}=\mathrm{V}_{\mathrm{EB} 1}-\mathrm{V}_{\mathrm{EB} 2}=\frac{\mathrm{kT}}{\mathrm{q}} \ln \left(\frac{\mathrm{~J}_{1}}{\mathrm{~J}_{2}}\right) \tag{7.44}
\end{equation*}
$$

and using (7.43) in (7.42) gives

$$
\begin{equation*}
V_{\text {ref }}=V_{E B 1}+\frac{R_{3}}{R_{2}} \frac{k T}{q} \ln \left(\frac{R_{3}}{R_{1}}\right) \tag{7.45}
\end{equation*}
$$

It is immediately recognizable that

$$
\begin{equation*}
\mathrm{K}=\frac{\mathrm{R}_{3}}{\mathrm{R}_{2}} \tag{7.46}
\end{equation*}
$$

#### EXAMPLE 7.5

Find the resistances of a bandgap voltage reference based on Fig. $7.13(a)$, where $I_{1}=80 \mu \mathrm{~A}, I_{2}=8 \mu \mathrm{~A}$, and $\mathrm{V}_{\mathrm{EB} 1-0}=0.65 \mathrm{~V}$ at $\mathrm{T}=300 \mathrm{~K}$.

#### Solution

Recalling from (7.24) that

$$
\begin{equation*}
V_{\text {ref-0 }}=1.24 \mathrm{~V} \tag{7.47}
\end{equation*}
$$

therefore, from (7.39), we require

$$
\begin{equation*}
\mathrm{V}_{\mathrm{R} 1}=\mathrm{V}_{\text {ref- }-0}-\mathrm{V}_{\mathrm{EB} 1-0}=0.59 \mathrm{~V} \tag{7.48}
\end{equation*}
$$

Also, since $\mathrm{V}_{\mathrm{R} 3}=\mathrm{V}_{\mathrm{R} 1}$, we have

$$
\begin{equation*}
\mathrm{R}_{3}=\frac{\mathrm{V}_{\mathrm{R} 3}}{\mathrm{I}_{2}}=\frac{0.59 \mathrm{~V}}{8 \mu \mathrm{~A}}=73.8 \mathrm{k} \Omega \tag{7.49}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{R}_{1}=\mathrm{R}_{3} \frac{\mathrm{I}_{2}}{\mathrm{I}_{1}}=7.38 \mathrm{k} \Omega \tag{7.50}
\end{equation*}
$$

Now, recalling from (7.26) that

$$
\begin{equation*}
\mathrm{K}=\frac{1.24-0.65 \mathrm{~V}}{0.0258 \times \ln (10)}=9.93 \tag{7.51}
\end{equation*}
$$

therefore

$$
\begin{equation*}
\mathrm{R}_{2}=\frac{\mathrm{R}_{3}}{\mathrm{~K}}=7.43 \mathrm{k} \Omega \tag{7.52}
\end{equation*}
$$

It is of interest to note here that using (7.44) and noting that $J_{1} / J_{2}=I_{1} / I_{2}$ (since the sizes of $Q_{1}$ and $Q_{2}$ are assumed to be the same), we find that

$$
\begin{equation*}
\Delta \mathrm{V}_{\mathrm{EB}}=\frac{\mathrm{kT}_{0}}{\mathrm{q}} \ln \left(\frac{\mathrm{I}_{1}}{\mathrm{I}_{2}}\right)=59 \mathrm{mV} \tag{7.53}
\end{equation*}
$$

gives the temperature dependence value of $0.198 \mathrm{mV} / \mathrm{K}$, as found in Example 7.3, which requires approximately a gain of 10 to cancel temperature dependency (actually 9.93 in this case).

The design equations for a voltage reference that is suitable for p -well processes and shown in Fig. 7.13(b) are essentially identical to those just given for the n -well reference.

In CMOS realizations of the references just described, the large value resistors are often realized by well resistors. Unfortunately, these resistors have a temperature dependence approximately given by [Michejda, 1984]

$$
\begin{equation*}
\mathrm{R}(\mathrm{~T})=\mathrm{R}_{0} \frac{\mathrm{~T}^{\eta}}{\mathrm{T}_{0}^{\eta}} \tag{7.54}
\end{equation*}
$$

where $\eta=2.2$. The errors caused by this temperature dependence can be eliminated by offsetting $\mathrm{V}_{\text {ref-0 }}$ slightly positive from the value given by (7.23) to

$$
\begin{equation*}
V_{\text {ref-0 }}=V_{G 0}+(m+\eta-1) \frac{k T_{0}}{q} \tag{7.55}
\end{equation*}
$$

Assuming the effects of the temperature coefficient of the resistors have been minimized, the next major source of error is often due to the input-offset voltage of the opamp [Michejda, 1984]. This results in an error term in the equation for $\Delta \mathrm{V}_{\mathrm{BE}}$ that is roughly equal to K times the input-offset voltage of the opamp. For example, a 1 mV offset error that is temperature independent causes a temperature coefficient (TC), error approximately given by [Song, 1983]

$$
\begin{equation*}
\mathrm{TC}_{\text {error }} \cong 26 \mathrm{ppm} /{ }^{\circ} \mathrm{C} \tag{7.56}
\end{equation*}
$$

One means of eliminating this source of error is to use switched-capacitor (SC) amplifiers that have input-offset compensation circuits [Song, 1983]. One possible SC-based voltage reference is shown in Fig. 7.14, where it makes use of an amplifier described in [Martin, 1987]. The amplifier shown results in a circuit having its output
image_name:Fig. 7.14
description:The circuit is an SC-based voltage reference designed to be insensitive to opamp input-offset voltages. It uses switched-capacitor techniques to minimize errors.

Fig. 7.14 An SC-based voltage reference that is insensitive to opamp input-offset voltages.
valid at all times and is less sensitive to finite opamp gain. A detailed explanation of how the amplifier shown in Fig. 7.14 operates is deferred until Chapter 14, where switched-capacitor circuits are discussed.

Assuming errors due to the input-offset voltage of the opamp have been minimized, there is still an inherent temperature dependence of the bandgap voltage reference, as we saw in (7.27). In addition, a further temperature dependence occurs because $\mathrm{V}_{\mathrm{G} 0}$ varies slightly with temperature (which has been ignored in the above analysis). Together, these two error sources limit the best achievable temperature coefficient to about $25 \mathrm{ppm} /{ }^{\circ} \mathrm{K}$. Minimizing these second-order effects is beyond the scope of this book, but the interested reader is referred to [Palmer, 1981; Meijer, 1982; Song, 1983] to see examples of how errors due to second-order effects have been minimized.

An alternative realization of a CMOS bandgap reference was reported in [Degrauwe, 1985], where lateral npn well transistors were used. Also, in [Tzanateas, 1979] a voltage reference was reported that was based on a realized PTAT voltage from the difference of the source-gate voltages of two MOS transistors biased in weak inversion. The interested reader can consult the references for details on these circuits.

### 7.3.3 Low-Voltage Bandgap Reference

A problem with the bandgap circuits described so far is that they are not compatible with supply voltages of 1.5 V or less. The fundamental problem is that all these circuits produce, in series, the inverse-PTAT voltage across a pn-junction and a PTAT voltage scaled to provide temperatureindependence. Together, these voltages exceed 1 V making it impossible to use these circuits with a 1-V supply. The solution is to instead sum currents: one inverse-PTAT and one PTAT, passing them through a resistor to form a temperature-insensitive reference voltage below 1 V .

A low-voltage bandgap circuit based on this idea is shown in Fig. 7.15 [Banba, 1999]. The feedback loop formed by the amplifier and current mirror $Q_{1} / Q_{2}$ ensures that the voltages at the drains of $Q_{1}$ and $Q_{2}$ are very well matched and equal to the forward voltage drop across diode $\mathrm{D}_{1}, \mathrm{~V}_{\mathrm{BE}, 1}$, which is inversely proportional to absolute temperature.

Key Point: Connecting PTAT and IPTAT voltages in series to produce a precision reference results in a voltage larger than the bandgap of silicon. To produce a bandgap reference under a lower supply voltage, it is necessary to first convert the PTAT and IPTAT quantities into currents, and then sum them by shunting.
image_name:Fig. 7.15 A low-voltage bandgap circuit
description:This circuit is a low-voltage bandgap reference circuit. It uses a combination of PTAT (Proportional To Absolute Temperature) and IPTAT (Inversely Proportional To Absolute Temperature) currents to create a temperature-independent reference voltage. The circuit employs a current mirror formed by Q1 and Q2, and a scaling factor of M:1 for the current through Q1 and Q2. The voltage across Rb is PTAT and is used to generate a stable reference voltage Vref. The op-amp ensures that the voltage difference across the diodes D1 and D2 is maintained.

Fig. 7.15 A low-voltage bandgap circuit [Banba, 1999].
The voltage across $R_{b}$ is equal to the difference between the forward bias voltages of $D_{1}$ and $D_{2}, \Delta V_{B E}$, and is therefore PTAT. The current mirror and matched resistors $\mathrm{R}_{\mathrm{a}}$ ensure that the current through the diodes differs by the factor M , and that the diode current densities differ by a factor $M N$.

$$
\begin{equation*}
\Delta V_{B E}=\frac{k T}{q} \ln (\mathrm{MN}) \tag{7.57}
\end{equation*}
$$

The inverse PTAT $V_{B E, 1}$ and PTAT $\Delta V_{B E}$ are converted into the currents $I_{2 a}$ and $I_{2 b}$ by the resistors $R_{a}$ and $R_{b}$, respectively.

$$
\begin{align*}
\mathrm{I}_{2 \mathrm{a}} & =\frac{\mathrm{V}_{\mathrm{BE}, 1}}{\mathrm{R}_{\mathrm{a}}}  \tag{7.58}\\
\mathrm{I}_{2 \mathrm{~b}} & =\frac{\Delta \mathrm{V}_{\mathrm{BE}}}{\mathrm{R}_{\mathrm{b}}} \tag{7.59}
\end{align*}
$$

These two currents are summed at the drain of $Q_{2}$ and mirrored to device $Q_{3}$. The resulting current then passes back through resistor $R$ to yield the reference output.

$$
\begin{equation*}
\mathrm{V}_{\mathrm{ref}}=\mathrm{KI}_{2} \mathrm{R}=\mathrm{V}_{\mathrm{BE}, 1}\left(\frac{\mathrm{KR}}{\mathrm{R}_{\mathrm{a}}}\right)+\frac{\mathrm{kT}}{\mathrm{q}} \ln (\mathrm{MN})\left(\frac{\mathrm{KR}}{\mathrm{R}_{\mathrm{b}}}\right) \tag{7.60}
\end{equation*}
$$

The values $M, N, R_{a}$, and $R_{b}$ are chosen to ensure that the inverse temperature coefficient of the first term is precisely cancelled by the positive temperature coefficient of the second term. Notice that nowhere are there DC voltages exceeding $\mathrm{V}_{\mathrm{BE}}$, so this circuit has been used with supply voltages as low as 0.8 V . The values of K and R can be chosen to scale the actual value of the reference potential at $V_{\text {ref }}$, while the values of $N, R_{a}$ and $R_{b}$ are chosen to cancel the negative and positive temperature coefficients of the first and second terms in (7.60). Opamp offset and mismatch in the current mirror devices, diodes, and resistors are all sources of error.

### 7.3.4 Current Reference

Once a bandgap voltage has been established, it can be used in combination with a resistor to provide a reference current. The basic approach is illustrated in Fig. 7.16. Feedback is used to generate the PMOS gate voltage that results in a voltage drop of precisely $\mathrm{V}_{\text {ref }}$ across a resistor R . This gate voltage can then be used to generate a scaled copy of the resulting current, $\mathrm{I}_{\mathrm{ref}}=\mathrm{MV}_{\text {ref }} / \mathrm{R}$. If $R$ is an on-chip resistor, the reference current will vary
image_name:Fig. 7.16
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Vref, InN: Vref, OutP: Out(A1)}
name: M1, type: PMOS, ports: {S: VDD, D: InP(A1), G: Out(A1)}
name: M2, type: PMOS, ports: {S: VDD, D: InP(A1), G: InP(A1)}
name: R, type: Resistor, value: R, ports: {N1: InP(A1), N2: GND}
]
extrainfo:The circuit generates a reference current Iref from a voltage reference Vref using an operational amplifier and PMOS transistors. The current Iref is given by the equation Iref = (M * Vref) / R, where M is the scaling factor determined by the PMOS transistors.

Fig. 7.16 Obtaining a reference current from a voltage reference.
with the value of on-chip resistors. This may be desirable if the current is passing through another on-chip resistor matched to $R$, in which case the resulting voltage drop will be stable. If, however, an absolute current reference is required, a precision resistor may be realized either off-chip or by trimming $R$ and somehow compensating for its temperature variations.

## 7.4 VOLTAGE REGULATION

A voltage regulator produces a low-noise dc voltage from which some current can be drawn. Its primary use is to provide a quiet supply voltage to an analog circuit, particularly in environments when a noisy supply voltage will otherwise limit performance.

A basic voltage regulator is shown in Fig. 7.17. It accepts as input a reference voltage, $\mathrm{V}_{\text {ref }}$, and produces as output $\mathrm{V}_{\text {reg }}$. It is essentially a unity-gain feedback buffer. The amplifier provides gain in the loop which ensures $\mathrm{V}_{\text {reg }} \cong \mathrm{V}_{\text {ref }}$ while $\mathrm{Q}_{1}$, called the pass transistor, sources the load current. The reference input may be derived from a bandgap circuit, if it is to remain fixed over process and temperature variations. Variable-output regulators have a fixed reference voltage and incorporate a resistive voltage divider in the feedback

Key Point: A voltage regulator comprises a feedback loop that keeps an output voltage equal to a reference voltage by controlling the flow of current to the output through a passtransistor.
loop which is adjusted to effect change in the output voltage.
image_name:Fig. 7.17 A basic voltage regulator.
description:The circuit is a basic voltage regulator that uses an OpAmp (A1) to control an NMOS transistor (Q1) for regulating the output voltage (Vreg). The feedback loop is established via the OpAmp, which compares the reference voltage (Vref) with the output voltage and adjusts the gate voltage of the NMOS to maintain a stable Vreg. Capacitors C1 and CL are used for stabilization and filtering.

Fig. 7.17 A basic voltage regulator.

### 7.4.1 Regulator Specifications

Power Supply Rejection

A regulator's ability to maintain a quiet voltage at $\bigvee_{\text {reg }}$ in the presence of noise on $V_{D D}$ is measured by superimposing a small signal onto $\mathrm{V}_{\mathrm{DD}}$ and measuring the resulting variations in $\mathrm{V}_{\text {reg }}$. The ratio of the two small signals $v_{d d}$ and $v_{\text {reg }}$ is its power supply rejection ratio which is usually expressed in decibels and is frequency-dependent.

$$
\begin{equation*}
\operatorname{PSRR}(\omega)=20 \log _{10}\left|\mathrm{~V}_{\mathrm{dd}} / \mathrm{v}_{\mathrm{reg}}\right| \mathrm{dB} \tag{7.61}
\end{equation*}
$$

Evaluated at dc, the inverse of supply rejection may be referred to as the line regulation.
Clearly the supply rejection of the reference generator and the opamp play important roles in the supply rejection of a regulator. For example, since $\mathrm{V}_{\text {reg }}$ will track $\mathrm{V}_{\text {ret }}$ within the feedback loop's bandwidth, low frequency supply rejection is often determined by the supply rejection of the reference generator.

Output Impedance

Variations in the current drawn by the regulator's load, $\mathrm{i}_{\mathrm{L}}$, will generally cause variations in $\mathrm{V}_{\text {reg }}$. If the changes are small, they are related by the regulator's small-signal output impedance, $Z_{\text {out }}$. At high frequencies, this will be determined by the impedance of the load capacitance, $1 / \mathrm{j} \omega \mathrm{C}_{\mathrm{L}}$. At low frequencies, it is determined by the impedance of the pass transistor $1 / \mathrm{g}_{\mathrm{m}, 1}$ divided by the opamp gain.

Dropout Voltage

An important specification of analog integrated circuit regulators is the maximum regulated voltage that can be maintained under a given global supply voltage, or equivalently the minimum voltage drop between the global supply and the regulated voltage, $\mathrm{V}_{\mathrm{DD}}-\mathrm{V}_{\text {reg }}$, called the dropout voltage, $\mathrm{V}_{\mathrm{DO}}$. Notice that the dc power dissipation in the transistor $Q_{1}$ is

$$
\begin{equation*}
P_{1}=\left(V_{D D}-V_{r e g}\right) i_{L} \tag{7.62}
\end{equation*}
$$

This power is not being delivered to the load, so it is a major inefficiency in the system. A lower limit on this power is imposed by the dropout voltage,

$$
\begin{equation*}
P_{1, \text { min }}=V_{D O} i_{L} \tag{7.63}
\end{equation*}
$$

motivating one to operate with $\left(V_{D D}-V_{\text {reg }}\right)$ near $V_{D O}$ and to minimize $V_{D O}$.
Looking at Fig. 7.17, clearly a voltage of $\mathrm{V}_{\text {eff, } 1}$ must be maintained between the drain and source of $Q_{1}$, otherwise the transconductance of $Q_{1}$ will drop, causing a decrease in loop gain and in the accuracy with which $\bigvee_{\text {reg }}$ tracks $\mathrm{V}_{\text {ref }}$. A more important consideration in determining the dropout voltage, however, is that $\mathrm{V}_{\text {reg }}$ must be below $\mathrm{V}_{1}$ by at least $\mathrm{V}_{\mathrm{GS}, 1}$. If the opamp is operated under the same supply voltage as $\mathrm{Q}_{1}$, and assuming the opamp output must be at least $\mathrm{V}_{\text {eff }}$ below $\mathrm{V}_{\mathrm{DD}}$ to prevent some device there from entering triode, the dropout voltage is at least $2 \mathrm{~V}_{\text {eff }}+\mathrm{V}_{\mathrm{tn}, 1}$. This quantity is not too large if native NMOS devices (having $\mathrm{V}_{\mathrm{tn}} \approx 0$ ) are available. Alternatively, in some cases the opamp is operated from a higher supply voltage.

### 7.4.2 Feedback Analysis

The open loop analysis of the voltage regulator with NMOS pass device in Fig. 7.17 is very similar to that of a basic source follower. Assuming a single-stage opamp with transconductance $G_{m a}$ and output resistance $R_{0 a}$, the loop is broken at the opamp's input and a test signal is injected, $v_{t}$. The resulting small-signal equivalent circuit is shown in Fig. 7.18. The regulator load is modeled by the small-signal resistance $R_{L}$ and combined with $r_{\text {ds1 }}$ and $1 / g_{s 1}$ to form $R_{L}{ }^{\prime}$. Applying the results from Chapter 4, the open-loop response is
image_name:Fig. 7.18
description:The circuit is a small-signal equivalent of a voltage regulator with an NMOS pass device. It includes an opamp, voltage-controlled current sources, resistors, and capacitors to model the open-loop response of the regulator.

Fig. 7.18 The open-loop small-signal schematic of a voltage regulator with NMOS pass device.

$$
\begin{equation*}
L(s)=\left(\frac{G_{m a} R_{o a} R_{L^{\prime}}}{R_{L^{\prime}}+1 / g_{m 1}}\right) \frac{\left(1+\frac{s C_{g s 1}}{g_{m 1}}\right)}{\left(1+\frac{s}{\omega_{0} Q}+\frac{s^{2}}{\omega_{0}^{2}}\right)} \tag{7.64}
\end{equation*}
$$

where

$$
\begin{gather*}
\omega_{0}=\sqrt{\frac{\left(1 / R_{o a}\right)\left(g_{m 1}+1 / R_{L}^{\prime}\right)}{C_{g s 1} C_{L}+C_{1}\left(C_{g s 1}+C_{L}\right)}}  \tag{7.65}\\
Q=\frac{\sqrt{\left(1 / R_{o a}\right)\left(g_{m 1}+1 / R_{L}\right)\left[C_{g s 1} C_{L}+C_{1}\left(C_{g s 1}+C_{\mathrm{L}}\right)\right]}}{C_{\mathrm{L}} / R_{o a}+C_{1}\left(g_{m 1}+1 / R_{o a}\right)+C_{g s 1} / R_{\mathrm{L}}^{\prime}} \tag{7.66}
\end{gather*}
$$

Assuming the loop is dominant-pole compensated, then Q «1 and the denominator (7.64) may be factored into two first-order terms.

$$
\begin{equation*}
L(s)=\left(\frac{G_{m a} R_{o a} R_{L}^{\prime}}{R_{L^{\prime}}^{\prime}+1 / g_{m 1}}\right) \frac{\left(1+\frac{s}{\omega_{z}}\right)}{\left(1+\frac{s}{\omega_{\mathrm{p} 1}}\right)\left(1+\frac{s}{\omega_{\mathrm{p} 2}}\right)} \tag{7.67}
\end{equation*}
$$

Hence, there are poles at

$$
\begin{align*}
& -\omega_{p 1}=-\omega_{0} Q=-\frac{\left(1 / R_{o a}\right)\left(g_{m 1}+1 / R_{L^{\prime}}\right)}{C_{\mathrm{L}} / R_{o a}+C_{1}\left(g_{m 1}+1 / R_{o a}\right)+C_{g s 1} / R_{L^{\prime}}}  \tag{7.68}\\
& -\omega_{\mathrm{p} 2}=-\frac{\omega_{0}}{\mathrm{Q}}=-\frac{\mathrm{C}_{\mathrm{L}} / \mathrm{R}_{\mathrm{oa}}+\mathrm{C}_{1}\left(\mathrm{~g}_{\mathrm{m} 1}+1 / \mathrm{R}_{\mathrm{oa}}\right)+\mathrm{C}_{\mathrm{g} 1} / \mathrm{R}_{\mathrm{L}}{ }^{\prime}}{\mathrm{C}_{\mathrm{gs} 1} \mathrm{C}_{\mathrm{L}}+\mathrm{C}_{1}\left(\mathrm{C}_{\mathrm{gs} 1}+\mathrm{C}_{\mathrm{L}}\right)} \tag{7.69}
\end{align*}
$$

and there is a zero due to the feedforward signal path through $\mathrm{C}_{\mathrm{gs} 1}$

$$
\begin{equation*}
-\omega_{z}=-g_{m 1} / C_{g s 1} \tag{7.70}
\end{equation*}
$$

There are two different ways to compensate the loop. If $\mathrm{C}_{1}$ is made large by including an additional compensation capacitor between $V_{1}$ and ground, $\mathrm{C}_{1} \mathrm{~g}_{\mathrm{m} 1}$ becomes the dominant term in the denominator of (7.68) and in the numerator of (7.69). As a result, the dominant pole $\omega_{\mathrm{p} 1} \approx 1 / R_{o \mathrm{a}} C_{1}$ is associated with the time constant at
$v_{1}$ and $\omega_{\mathrm{p} 2} \approx \mathrm{~g}_{\mathrm{m} 1} / C_{\mathrm{L}}$ is associated with the time constant at $\mathrm{v}_{\mathrm{reg}}$. In this case, a capacitor is still required at the output $C_{L}$ to filter high frequency noise on $v_{\text {reg }}$. Alternatively, $C_{L}$ can be made very large and $R_{o a}$ decreased so that $C_{L} / R_{o a}$ is a dominant term in both (7.68) and (7.69). In this case, the two poles change roles so that $\omega_{p 1}$ is the output pole and $\omega_{\mathrm{p} 2}$ is the pole at $\mathrm{v}_{1}$. This generally requires a larger compensation capacitor and/or higher power consumption in the opamp, but it provides a large capacitance at the output where it also improves supply rejection and output impedance at medium-to-high frequencies. Generally, $\omega_{z}$ will be at a much higher frequency than the poles and have little effect on stability.

### 7.4.3 Low Dropout Regulators

When the regulated output must be at a voltage only $200-400 \mathrm{mV}$ below $\mathrm{V}_{\mathrm{DD}}$, and especially when native (near-zero- $V_{t}$ ) NMOS devices are unavailable, it is necessary to utilize a PMOS device for $Q_{1}$ as shown in Fig. 7.19. In this case, the gate voltage $\mathrm{V}_{1}$ is well below $\mathrm{V}_{\mathrm{DD}}$ so the dropout voltage is only limited by $\mathrm{V}_{\text {eff, } 1}$. This is commonly referred to as a low dropout ( $L D O$ ) voltage regulator and is popular when power efficiency is critical. Notice that the polarity of the opamp's input terminals has been reversed because there is now negative small-signal gain from $V_{1}$ to $V_{\text {reg }}$. Although the resistance seen looking into $Q_{1}$ is increased compared with Fig. 7.17 from $1 / g_{m, 1}$ to $r_{d s, 1}$, the loop gain is also increased by roughly a factor $g_{m, 1} r_{d s, 1}$ so the regulator's closed-loop output resistance is roughly the same.

Key Point: Whereas an NMOS pass-transistor provides superior supply rejection, unless native NMOS devices are available, a PMOS pass-transistor permits a lower dropout voltage and, hence, better efficiency.

A significant drawback of PMOS devices is their reduced power supply rejection. With respect to small signals at $\mathrm{V}_{\mathrm{DD}}, \mathrm{Q}_{1}$ behaves like a commongate amplifier having considerable gain. At low frequencies, the feedback loop tracks and cancels the resulting variations in $\mathrm{V}_{\text {reg }}$, and at high frequencies the variations are filtered by $\mathrm{C}_{\mathrm{L}}$, but there is generally a mid-band frequency range where it is difficult to provide good supply rejection using a LDO.

The feedback analysis of a LDO is similar to that of a two-stage opamp, where the opamp in Fig. 7.19 is presumed to have only a single stage and the common-source pass transistor $Q_{1}$ provides the second gain stage. Neglecting $\mathrm{C}_{\mathrm{gd}}$, there are clearly two poles in the open loop response corresponding to the two nodes in the system.
image_name:Fig. 7.19 A low dropout (LDO) voltage regulator
description:This is a low dropout (LDO) voltage regulator circuit. The OpAmp A1 compares the reference voltage Vref with the regulated output Vreg and controls the PMOS transistor Q1 to maintain the desired output voltage. Capacitors C1 and CL provide stability and filtering.

Fig. 7.19 A low dropout (LDO) voltage regulator.

$$
\begin{equation*}
\mathrm{L}(\mathrm{~s})=\frac{\mathrm{G}_{\mathrm{ma}} \mathrm{R}_{\mathrm{oa}} \mathrm{~g}_{\mathrm{m} 1} \mathrm{R}_{\mathrm{L}^{\prime}}}{\left(1+\frac{\mathrm{s}}{\omega_{\mathrm{pa}}}\right)\left(1+\frac{\mathrm{s}}{\omega_{\mathrm{pL}}}\right)} \tag{7.71}
\end{equation*}
$$

The pole at the amplifier output (gate of $Q_{1}$ ) is

$$
\begin{equation*}
\omega_{\mathrm{pa}}=\frac{1}{\mathrm{R}_{\mathrm{oa}} \mathrm{C}_{\mathrm{l}^{\prime}}} \tag{7.72}
\end{equation*}
$$

where $\mathrm{C}_{1}{ }^{\prime}=\mathrm{C}_{1}+\mathrm{C}_{\mathrm{gs} 1}$, and the output pole is

$$
\begin{equation*}
\omega_{\mathrm{pL}}=\frac{1}{\mathrm{R}_{\mathrm{L}} \mathrm{C}_{\mathrm{L}}} \tag{7.73}
\end{equation*}
$$

Again, either pole can be made dominant to compensate the loop. A dominant output pole, $\omega_{\mathrm{pL}}$ « $\omega_{\mathrm{pa}}$, requires high power consumption in the opamp to keep $R_{o a}$ low, but has the advantage of providing a low output impedance at medium frequencies which improves the supply rejection. This is particularly important in LDOs since the PMOS pass transistor tends to amplify supply noise as described above.

Key Point: Compensation of a voltage regulator presents a difficult decision: either make the output pole dominant, resulting in high power consumption in the feedback amplifier, or make the pass-transistor gate node dominant, in which case supply rejection is worse.

#### EXAMPLE 7.6

What is the supply rejection of the basic voltage regulator shown in Fig. 7.20?

#### Solution

A small-signal equivalent circuit is shown in Fig. 7.21 with a small-signal source shown at $\mathrm{V}_{\mathrm{DD}}$. With the loop open, the response from $V_{D D}$ to $V_{\text {reg }}$ is simply that of a common-gate amplifier loaded by $R_{L}| |\left(1 / s C_{L}\right)$.

$$
\begin{equation*}
\mathrm{H}_{\mathrm{CG}}(\mathrm{~s})=\left(\frac{\mathrm{R}_{\mathrm{L}}}{\mathrm{r}_{\mathrm{ds} 1}+\mathrm{R}_{\mathrm{L}}}\right) \frac{1}{1+s \mathrm{R}_{\mathrm{L}} \mathrm{C}_{\mathrm{L}}} \tag{7.74}
\end{equation*}
$$

image_name:Fig. 7.20
description:This circuit represents an open-loop small-signal model of an LDO voltage regulator with a PMOS pass device. The key components include an operational amplifier, a voltage source, and various passive components such as resistors and capacitors. The circuit is designed to analyze the frequency response and stability of the voltage regulator.

Fig. 7.20 The open-loop small-signal schematic of a LDO voltage regulator with a PMOS pass device.
image_name:Fig. 7.21
description:
[
name: g_m v_i, type: VoltageControlledCurrentSource, value: g_m v_i, ports: {Np: GND, Nn: v_1}
name: R_1, type: Resistor, value: R_1, ports: {N1: v_1, N2: GND}
name: C_1, type: Capacitor, value: C_1, ports: {Np: v_1, Nn: GND}
name: g_m1 V_gs1, type: VoltageControlledCurrentSource, value: g_m1 V_gs1, ports: {Np: VDD, Nn: Vreg}
name: r_ds1, type: Resistor, value: r_ds1, ports: {N1: VDD, N2: Vreg}
name: V_DD, type: VoltageSource, value: V_DD, ports: {Np: VDD, Nn: GND}
name: C_L, type: Capacitor, value: C_L, ports: {Np: Vreg, Nn: GND}
name: R_L, type: Resistor, value: R_L, ports: {N1: Vreg, N2: GND}
]
extrainfo:This circuit represents a small-signal model of a basic voltage regulator. It includes a voltage-controlled current source, resistors, capacitors, and a voltage source. The circuit is used to analyze the stability and frequency response of the voltage regulator.

Fig. 7.21 The small-signal schematic of a basic voltage regulator.

With the loop closed, this first-order lowpass response is shaped by $1 /(1+\mathrm{L}(\mathrm{s}))$. The resulting frequency response from small signals on the supply voltage to small signals at the regulator output is the inverse of the power supply rejection

$$
\begin{equation*}
\frac{v_{\mathrm{reg}}}{v_{\mathrm{dd}}}(s)=\operatorname{PSRR}^{-1}(s)=\frac{H_{\mathrm{CG}}(s)}{1+\mathrm{L}(\mathrm{~s})} \tag{7.75}
\end{equation*}
$$

The responses are plotted in Fig. 7.22 for two cases: where the load pole $\omega_{\mathrm{pL}}$ is dominant, Fig. 7.22(c), and where the opamp output pole $\omega_{\mathrm{pa}}$ is dominant, Fig. $7.22(d)$. In both cases, the dc rejection (line regulation) is given by

$$
\begin{equation*}
\operatorname{PSRR}^{-1}(s)=\left(\frac{R_{L}}{r_{d s 1}+R_{L}}\right) \frac{1}{G_{m a} R_{o a} g_{m 1} R_{L}} \tag{7.76}
\end{equation*}
$$

image_name:(a)
description:### Graph (a): Open Loop Supply Rejection

1. **Type of Graph and Function:**
- The graph is a Bode plot representing the magnitude of the open-loop supply rejection, denoted as \(|H_{CG}(\omega)|\).

2. **Axes Labels and Units:**
- The horizontal axis represents frequency \(\omega\), typically in radians per second. The scale appears to be logarithmic, which is common in Bode plots.
- The vertical axis represents the magnitude of the transfer function \(|H_{CG}(\omega)|\).

3. **Overall Behavior and Trends:**
- The plot shows a constant magnitude at lower frequencies, indicating a stable gain.
- At a certain frequency, labeled approximately as \(\omega_{pL}\), the magnitude begins to decrease, suggesting a roll-off.

4. **Key Features and Technical Details:**
- The graph shows a flat response at low frequencies, indicating effective supply rejection in this range.
- A significant change occurs around \(\omega_{pL}\), where the slope of the graph changes, indicating a transition point.
- The slope beyond \(\omega_{pL}\) suggests a first-order roll-off, typical of a single-pole system.

5. **Annotations and Specific Data Points:**
- The point labeled \(\approx \omega_{pL}\) is an important frequency where the behavior of the system changes, marking the onset of the roll-off.
- There are no specific numerical values provided, but the transition point is clearly marked on the graph.
image_name:(b)
description:The graph labeled (b) is a Bode plot showing the frequency response of the closed-loop shaping function, represented as \( \frac{1}{1 + L(\omega)} \). The axes are as follows: the vertical axis represents the magnitude of the function \( \frac{1}{1 + L(\omega)} \), and the horizontal axis represents the frequency \( \omega \), likely in a logarithmic scale, though specific units are not provided.

**Overall Behavior and Trends:**
- The plot begins with a flat response at low frequencies, indicating a constant magnitude.
- At the cutoff frequency \( \omega_{p1} \), the plot shows a distinct upward slope, suggesting an increase in magnitude as frequency increases.
- This slope continues until it reaches a frequency \( \omega_t \), where the graph levels off again, indicating another region of constant magnitude at higher frequencies.

**Key Features and Technical Details:**
- The initial flat region suggests a low-pass characteristic with a stable gain before \( \omega_{p1} \).
- The slope between \( \omega_{p1} \) and \( \omega_t \) indicates a transitional frequency range where the system's response changes significantly.
- The flat region after \( \omega_t \) implies a stabilization of the response, possibly indicating a high-frequency asymptotic behavior.

**Annotations and Specific Data Points:**
- The graph is marked with two significant frequencies: \( \omega_{p1} \) and \( \omega_t \), both of which are important in defining the behavior of the system.
- The transition at \( \omega_{p1} \) and leveling at \( \omega_t \) are critical points that highlight changes in the system's response.
image_name:(c)
description:The graph in Fig. 7.22(c) is a Bode plot representing the inverse power supply rejection ratio (PSRR) for a low dropout (LDO) regulator. This specific plot shows the case where the load pole (ω_pL) is dominant over the operational amplifier output pole (ω_pa).

1. **Type of Graph and Function:**
- The graph is a Bode plot, which is typically used to display the gain or magnitude of a system as a function of frequency.

2. **Axes Labels and Units:**
- The horizontal axis represents frequency (ω) and is typically measured in radians per second.
- The vertical axis represents the magnitude of the inverse PSRR, denoted as |PSRR^{-1}(ω)|.

3. **Overall Behavior and Trends:**
- The graph starts with a flat response at lower frequencies, indicating a constant magnitude.
- At a certain frequency, labeled as ω_t, there is a noticeable downward slope, indicating a decrease in magnitude as frequency increases.

4. **Key Features and Technical Details:**
- The flat region at the beginning of the graph corresponds to low-frequency behavior where the PSRR is stable and not significantly affected by frequency changes.
- The downward slope after ω_t suggests a roll-off, where the inverse PSRR decreases, indicating that the regulator becomes less effective at rejecting power supply variations at higher frequencies.
- The point ω_t marks the transition frequency where the behavior changes from flat to decreasing.

5. **Annotations and Specific Data Points:**
- The graph is annotated with the condition ω_p1 = ω_pL < ω_pa, emphasizing that the load pole is dominant.
- The transition frequency ω_t is a critical point where the slope begins, although specific numerical values are not provided in the graph.

Overall, this graph illustrates how the inverse PSRR of the LDO regulator behaves with frequency, highlighting the impact of the dominant load pole on the frequency response.
image_name:(d)
description:The graph labeled (d) is a Bode plot depicting the magnitude of the inverse power supply rejection ratio, denoted as |PSRR^{-1}(ω)|. The x-axis represents frequency (ω) on a logarithmic scale, while the y-axis represents the magnitude of PSRR^{-1} in decibels (dB).

Key Features:
1. **Dominant Pole Configuration:**
- The graph represents the case where the operational amplifier (opamp) output pole (ω_pa) is dominant, with the relationship ω_p1 = ω_pa < ω_pL.

2. **Behavior and Trends:**
- Initially, the magnitude is constant at low frequencies.
- As frequency increases, the magnitude rises, indicating an increase in PSRR^{-1} up to a certain point.
- The graph reaches a peak at a frequency between ω_pa and ω_pL, showing the highest magnitude.
- After the peak, the magnitude decreases steadily, indicating a reduction in PSRR^{-1} at higher frequencies.

3. **Critical Points:**
- **ω_pa:** This is the frequency where the initial rise in magnitude begins.
- **ω_t:** The frequency where the magnitude peaks, marking the transition between increasing and decreasing trends.
- **ω_pL:** The frequency where the decreasing trend continues after the peak.

4. **Annotations and Markers:**
- The graph is annotated with vertical dashed lines at ω_pa, ω_t, and ω_pL to indicate these critical frequencies.
- The slope of the graph changes at these marked frequencies, emphasizing the transitions in behavior.

Overall, this graph illustrates the frequency response of the PSRR for a configuration where the opamp output pole is dominant, showing the characteristic rise and fall in magnitude across the frequency spectrum.

Fig. 7.22 The power supply rejection of a LDO regulator: (a) open loop supply rejection;
(b) closed-loop shaping frequency response; (c) $|\operatorname{PSRR}(\omega)|=\left|\mathrm{H}_{\mathrm{CG}}(\omega)\right| /|1+\mathrm{L}(\omega)|$ with $\omega_{\mathrm{pL}}<\omega_{\mathrm{pa}}$;
(d) $|\operatorname{PSRR}(\omega)|=\left|\mathrm{H}_{\mathrm{CG}}(\omega)\right| /|1+\mathrm{L}(\omega)|$ with $\omega_{\mathrm{pa}}<\omega_{\mathrm{pL}}$.

As the loop gain increases beyond its dominant pole frequency $\omega_{\mathrm{pl}}$, the supply rejection worsens. In the first case, this occurs at the same frequency as the output pole begins to filter out the supply noise, so the supply rejection remains high. In the second case, the opamp pole $\omega_{\mathrm{pa}}$ occurs first at frequencies where the load capacitor is still unable to provide filtering of supply-induced noise, so the supply rejection worsens until the load pole kicks in. Unfortunately, for stability the poles $\omega_{\mathrm{pa}}$ and $\omega_{\mathrm{pL}}$ must be widely spaced, so the deterioration is significant. This usually occurs at frequencies in the range of 100 's of MHz where supply noise due to digital circuitry can be very high, and is therefore a major challenge.

## 7.5 SUMMARY OF KEY POINTS

- A bias circuit generates the dc voltages required to keep transistors near some desired operating point; as transistor parameters change, either from chip to chip or with changes in temperature, so must the bias voltages. [p. 303]
- A reference circuit generates a voltage and/or current of a known fixed absolute value. [p. 305]
- A regulator circuit improves the quality of a dc voltage or current, usually decreasing the noise. [p. 306]
- A constant-transconductance bias circuit produces a small-signal transconductance that is a fixed fraction of a resistor value, independent of process, temperature, or supply variations. [p. 308]
- The constant-transconductance bias circuit ensures a constant transconductance in all transistors of the same type as $\mathrm{Q}_{13}$. However, the transconductance of transistors of the opposite type will vary. [p. 308]
- Many bias circuits require auxiliary start-up circuits to prevent them from resting in a zero-current state indefinitely. [p. 309]
- An integrated voltage reference is made by adding the forward bias voltage of a pn junction to the difference in the forward voltages of two pn junctions biased at different current densities. Before adding them, these voltages are scaled so that their respective positive and negative temperature coefficients cancel precisely. [p. 311]
- The implementation of bandgap references in a CMOS process makes use of bipolar transistors formed using doped well regions in the silicon substrate. [p. 315]
- Connecting PTAT and IPTAT voltages in series to produce a precision reference results in a voltage larger than the bandgap of silicon. To produce a bandgap reference under a lower supply voltage, it is necessary to first convert the PTAT and IPTAT quantities into currents, and then sum them by shunting. [p. 319]
- A voltage regulator comprises a feedback loop that keeps an output voltage equal to a reference voltage by controlling the flow of current to the output through a pass-transistor. [p. 321]
- Whereas an NMOS pass-transistor provides superior supply rejection, unless native NMOS devices are available, a PMOS pass-transistor permits a lower dropout voltage and, hence, better efficiency. [p. 324]
- Compensation of a voltage regulator presents a difficult decision: either make the output pole dominant, resulting in high power consumption in the feedback amplifier, or make the pass-transistor gate node dominant, in which case supply rejection is worse. [p. 325]
