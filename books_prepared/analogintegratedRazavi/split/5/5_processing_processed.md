# CHAPTER 5 Current Mirrors and Biasing Techniques

Our study of single-stage and differential amplifiers in Chapters 3 and 4 points to the wide usage of current sources. In these circuits, current sources act as a large resistor without consuming excessive voltage headroom. We also noted that MOS devices operating in saturation can act as a current source.

Current sources find other applications in analog design as well. For example, some digital-to-analog (D/A) converters employ an array of current sources to produce an analog output proportional to the digital input. Also, current sources, in conjunction with "current mirrors," can perform useful functions on analog signals.

This chapter deals with the design of current mirrors and bias circuits. Following a review of basic current mirrors, we study the cascode mirror. Next, we analyze active current mirrors and describe the properties of differential pairs using such circuits as loads. Finally, we introduce various biasing techniques for amplifier stages.

## 5.1 - Basic Current Mirrors

Figure 5.1 illustrates two examples in which a current source proves useful. From our study in Chapter 2, recall that the output resistance and capacitance and the voltage headroom of a current source trade with the magnitude of the output current. In addition to these issues, several other aspects of current sources are important: supply, process, and temperature dependence; output noise current; and matching with other current sources. We defer the noise and matching considerations to Chapters 7 and 14, respectively.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: M2, type: PMOS, ports: {S: VDD, D: Vout, G: Vout}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: Vout}
]
extrainfo:The circuit diagram (a) shows a configuration with NMOS M1 and PMOS M2 and M3 transistors, forming a current source with output at Vout. The current source I1 is connected between VDD and Vout. M3 is used for biasing with gate connected to Vb.
image_name:(b)
description:The circuit diagram (b) shows a current mirror configuration with NMOS and PMOS transistors. The NMOS transistor M1 is connected to the input voltage Vin and the PMOS transistors M2 and M3 form a current mirror. The current source ISS is connected between node p and ground, providing biasing current for the PMOS transistors.
Figure 5.1 Applications of current sources.

image_name:Figure 5.2 Definition of current by resistive divider.
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: g1}
name: R2, type: Resistor, value: R2, ports: {N1: g1, N2: GND}
name: M1, type: NMOS, ports: {S: GND, D: Iout, G: g1}
]
extrainfo:The circuit diagram shows a simple resistive biasing network for an NMOS transistor M1. The resistors R1 and R2 form a voltage divider that sets the gate voltage of M1. The NMOS transistor is configured to operate as a current source with Iout as the output current. The load is connected to the drain of M1.

How should a MOSFET be biased so as to operate as a stable current source? To gain a better view of the issues, let us consider the simple resistive biasing shown in Fig. 5.2. Assuming $M_{1}$ is in saturation, we can write

$$
\begin{equation*}
I_{\text {out }} \approx \frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(\frac{R_{2}}{R_{1}+R_{2}} V_{D D}-V_{T H}\right)^{2} \tag{5.1}
\end{equation*}
$$

This expression reveals various PVT dependencies of $I_{\text {out }}$. The overdrive voltage is a function of $V_{D D}$ and $V_{T H}$; the threshold voltage may vary by 50 to 100 mV from wafer to wafer. Furthermore, both $\mu_{n}$ and $V_{T H}$ exhibit temperature dependence. Thus, $I_{o u t}$ is poorly defined. The issue becomes more severe as the device is biased with a smaller overdrive voltage, e.g., to consume less headroom and support greater voltage swings at the drain. With a nominal overdrive of, say, 200 mV , a $50-\mathrm{mV}$ error in $V_{T H}$ results in a $44 \%$ error in the output current.

It is important to note that process and temperature dependencies exist even if the gate voltage is not a function of the supply voltage. In other words, if the gate-source voltage of a MOSFET is precisely defined, then its drain current is not! For this reason, we must seek other methods of biasing MOS current sources.

The design of current sources in analog circuits is based on "copying" currents from a reference, with the assumption that one precisely-defined current source is already available. While this method may appear to entail an endless loop, it is carried out as illustrated in Fig. 5.3. A relatively complex circuit-sometimes requiring external adjustments-is used to generate a stable reference current, $I_{R E F}$, which is then "cloned" to create many current sources in the system. We study the copying operation here and the reference generator (which is based on "bandgap" techniques) in Chapter 12.
image_name:Figure 5.3 Use of a reference to generate various currents.
description:
[
name: I_REF, type: CurrentSource, value: I_REF, ports: {Np: Reference Generator, Nn: X_I1}
name: I_1, type: CurrentSource, value: I_1, ports: {Np: VDD, Nn: X_I1}
name: I_2, type: CurrentSource, value: I_2, ports: {Np: X_I1, Nn: GND}
name: V_DD, type: VoltageSource, value: V_DD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit uses a reference current (I_REF) generated by a reference generator to create multiple current sources (I_1 and I_2). The current I_1 is connected to the power supply VDD and node X_I1, while I_2 is connected between node X_I1 and ground.

How do we generate copies of a reference current? For example, in Fig. 5.4, how do we guarantee that $I_{\text {out }}=I_{R E F}$ ? For a MOSFET, if $I_{D}=f\left(V_{G S}\right)$, where $f(\cdot)$ denotes the dependence of $I_{D}$ upon $V_{G S}$, then $V_{G S}=f^{-1}\left(I_{D}\right)$. That is, if a transistor is biased at $I_{R E F}$, then it produces $V_{G S}=f^{-1}\left(I_{R E F}\right)[F i g$. 5.5(a)]. Thus, if this voltage is applied to the gate and source terminals of a second MOSFET, the resulting current is $I_{\text {out }}=f\left[f^{-1}\left(I_{R E F}\right)\right]=I_{R E F}[$ Fig. $5.5(\mathrm{~b})]$. From another point of view, two identical MOS devices that have equal gate-source voltages and operate in saturation carry equal currents (if $\lambda=0$ ).
image_name:Figure 5.4
description:The circuit in Figure 5.4 is a conceptual representation of a current copying mechanism. It uses a current mirror configuration to replicate the reference current I_REF at the output, I_out, across a load. The NMOS transistors M1 and M2 are configured such that M1 is diode-connected, and M2 mirrors the current from M1 to the output.
image_name:Fig. 5.5(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1g1, G: d1g1}
name: I_REF, type: CurrentSource, value: I_REF, ports: {Np: VDD, Nn: d1g1}
name: V_DD, type: VoltageSource, value: V_DD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit in Fig. 5.5(a) is a diode-connected NMOS transistor configuration used to establish a reference voltage across M1. The current source I_REF biases the NMOS M1, creating a voltage drop across its gate and drain, which are shorted together.
image_name:Fig. 5.5(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1g1g2, G: d1g1g2}
name: M2, type: NMOS, ports: {S: GND, D: d2g1g2, G: d1g1g2}
name: I_REF, type: CurrentSource, value: I_REF, ports: {Np: VDD, Nn: d1g1}
name: V_DD, type: VoltageSource, value: V_DD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit in Fig. 5.5(b) is a basic current mirror consisting of two NMOS transistors, M1 and M2. M1 is diode-connected, meaning its gate and drain are connected together, forming a reference current path with I_REF. M2 mirrors the current from M1 to the output node d2. This setup is used to replicate the reference current I_REF at the output.

The structure consisting of $M_{1}$ and $M_{2}$ in Fig. 5.5(b) is called a "current mirror." In the general case, the transistors need not be identical. Neglecting channel-length modulation, we can write

$$
\begin{align*}
I_{R E F} & =\frac{1}{2} \mu_{n} C_{o x}\left(\frac{W}{L}\right)_{1}\left(V_{G S}-V_{T H}\right)^{2}  \tag{5.2}\\
I_{o u t} & =\frac{1}{2} \mu_{n} C_{o x}\left(\frac{W}{L}\right)_{2}\left(V_{G S}-V_{T H}\right)^{2} \tag{5.3}
\end{align*}
$$

obtaining

$$
\begin{equation*}
I_{\text {out }}=\frac{(W / L)_{2}}{(W / L)_{1}} I_{R E F} \tag{5.4}
\end{equation*}
$$

The key property of this topology is that it allows precise copying of the current with no dependence on process and temperature. The translation from $I_{R E F}$ to $I_{\text {out }}$ merely involves the ratio of device dimensions, a quantity that can be controlled with reasonable accuracy.

It is important to appreciate the cause-and-effect relationships stipulated by $V_{G S}=f^{-1}\left(I_{R E F}\right)$ and $f\left[f^{-1}\left(I_{R E F}\right)\right]=I_{R E F}$. The former suggests that we must generate a $V_{G S}$ from $I_{R E F}$; i.e., $I_{R E F}$ is the cause and $V_{G S}$ is the effect. A MOSFET can perform this function only if it is configured as a diode while carrying a current of $I_{R E F}$ [ $M_{1}$ in Fig. 5.5(b)]. Similarly, the latter equation indicates that a transistor must sense $f^{-1}\left(I_{R E F}\right)\left(=V_{G S}\right)$ and generate $f\left[f^{-1}\left(I_{R E F}\right)\right]$. In this case, the cause is $V_{G S}$ and the effect is the output current, $f\left[f^{-1}\left(I_{R E F}\right)\right]$ [as provided by $M_{2}$ in Fig. 5.5(b)].

With the aid of these observations, we can understand why a circuit such as that in Fig. 5.6 does not perform current copying. Here, $V_{b}$ is not caused by $I_{R E F}$, and hence $I_{\text {out }}$ does not track $I_{R E F}$.
image_name:Figure 5.6 Circuit incapable of copying current.
description:
[
name: IREF, type: CurrentSource, value: IREF, ports: {Np: VDD, Nn: d1}
name: M1, type: NMOS, ports: {S: GND, D: d1, G: Vb}
name: M2, type: NMOS, ports: {S: GND, D: Iout, G: Vb}
]
extrainfo:The circuit is intended to copy current but fails because Vb is not influenced by IREF, causing Iout not to track IREF. The circuit includes a load connected to the drain of M2.

#### Example 5.1

In Fig. 5.7, find the drain current of $M_{4}$ if all of the transistors are in saturation.
image_name:Figure 5.7
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1g1g2, G: d1g1g2}
name: M2, type: NMOS, ports: {S: GND, D: X, G: d1g1g2}
name: M3, type: PMOS, ports: {S: VDD, D: X, G: X}
name: M4, type: PMOS, ports: {S: VDD, D: Iout, G: X}
name: I_REF, type: CurrentSource, ports: {Np: VDD, Nn: d1g1g2}
]
extrainfo:The circuit is designed to establish a current mirror configuration using NMOS and PMOS transistors. The drain current of M4 can be determined using the given relationships between the transistor dimensions. All transistors are assumed to be in saturation.

#### Solution

We have $I_{D 2}=I_{R E F}\left[(W / L)_{2} /(W / L)_{1}\right]$. Also, $\left|I_{D 3}\right|=\left|I_{D 2}\right|$ and $I_{D 4}=I_{D 3} \times\left[(W / L)_{4} /(W / L)_{3}\right]$. Thus, $\left|I_{D 4}\right|=$ $\alpha \beta I_{R E F}$, where $\alpha=(W / L)_{2} /(W / L)_{1}$ and $\beta=(W / L)_{4} /(W / L)_{3}$. Proper choice of $\alpha$ and $\beta$ can establish large or small ratios between $I_{D 4}$ and $I_{R E F}$. For example, $\alpha=\beta=5$ yields a magnification factor of 25 . Similarly, $\alpha=\beta=0.2$ can be utilized to generate a small, well-defined current.

We should also remark that the copy of a copy may not be as "clear" as the original. Owing to random "mismatches" between $M_{1}$ and $M_{2}$ in the above example, $I_{D 2}$ slightly deviates from its nominal value. Similarly, as $I_{D 2}$ is copied onto $I_{D 4}$, additional errors accumulate. We must therefore avoid long current mirror chains.

Current mirrors find wide application in analog circuits. Figure 5.8 illustrates a typical case, where a differential pair is biased by means of an NMOS mirror for the tail current source and a PMOS mirror
image_name:Figure 5.8
description:The circuit is a differential amplifier biased by NMOS and PMOS current mirrors. The NMOS devices M0, M1, M2, M7, and M8 form the tail current source and differential pair. PMOS devices M3, M4, M5, M6, and M9 form the load current sources. The circuit is designed to increase gain by reducing the drain current in M3 and M4, achieved through specific device sizing.
Figure 5.8 Current mirrors used to bias a differential amplifier.
for the load current sources. The device dimensions shown establish a drain current of $0.4 I_{T}$ in $M_{5}$ and $M_{6}$, reducing the drain current of $M_{3}$ and $M_{4}$ and hence increasing the amplifier's gain.

Sizing Issues Current mirrors usually employ the same length for all of the transistors so as to minimize errors due to the side-diffusion of the source and drain areas $\left(L_{D}\right)$. For example, in Fig. 5.8, the NMOS current sources must have the same channel length as $M_{0}$. This is because if $L_{\text {drawn }}$ is, say, doubled, then $L_{\text {eff }}=L_{\text {drawn }}-2 L_{D}$ is not. Furthermore, the threshold voltage of short-channel devices exhibits some dependence on the channel length (Chapter 17). Thus, current ratioing is achieved by scaling only the width of the transistors.

Suppose we wish to copy a reference current, $I_{R E F}$, and generate $2 I_{R E F}$. We begin with a width of $W_{R E F}$ for the diode-connected reference transistor and hence choose $2 W_{R E F}$ for the current source [Fig. 5.9(a)]. Unfortunately, direct scaling of the width also faces difficulties. As illustrated in Fig. 5.9(b), since the "corners" of the gate are poorly defined, if the drawn $W$ is doubled, the actual width does not exactly double. We thus prefer to employ a "unit" transistor and create copies by repeating such a device [Fig. 5.9(c)].
image_name:(a)
description:The circuit diagram (a) shows a current mirror configuration to multiply the reference current I_REF by 2 using two NMOS transistors. The transistor MREF is diode-connected with its gate and drain connected to the node X1. M2 is configured to provide a mirrored current of 2*I_REF to the load. The current source IREF provides the reference current to the circuit.
image_name:(b)
description:The image labeled as (b) illustrates the effect of gate corners on current accuracy in a transistor. This diagram provides both a top view and a cross-sectional view labeled 'AA View'.

1. **Identification of Components and Structure:**
- The **top view** shows a rectangular structure with a width labeled 'W'. It features several square elements, likely representing contact points or regions on the transistor gate.
- The **AA view** is a cross-section that highlights the gate structure, showing how the corners of the gate are rounded or poorly defined.
- Key components in the cross-section include the **gate**, **oxide layer**, and **channel**.

2. **Connections and Interactions:**
- The cross-sectional view emphasizes the interaction between the gate, oxide, and channel. The rounded corners of the gate can lead to inaccuracies in current flow, as they affect the effective width 'W' of the channel.
- The oxide layer serves as an insulating barrier between the gate and the channel, crucial for controlling the current flow.

3. **Labels, Annotations, and Key Features:**
- The width 'W' is a critical dimension in both views, illustrating the intended width of the gate.
- The label 'Gate Corner' highlights the area where inaccuracies may arise due to the physical shape of the gate.
- The terms 'Oxide' and 'Channel' in the cross-section indicate the layers involved in the transistor's operation, with the channel being the path for current flow.

This diagram is used to explain why simply scaling up the width of a transistor may not proportionally increase the current, due to the imprecise definition of the gate corners.
image_name:(c)
description:The circuit diagram (c) shows a more accurate current multiplication technique using unit transistors to generate both 2I_REF and I_REF/2 from I_REF. The transistors M3 and M4 are used to split the current, with each carrying I_REF/2.

Figure 5.9 (a) Current mirror multiplying $I_{R E F}$ by 2, (b) effect of gate corner on current accuracy, and (c) more accurate current multiplication.

But how do we generate a current equal to $I_{R E F} / 2$ from $I_{R E F}$ ? In this case, the diode-connected device itself must consist of two units, each carrying $I_{R E F} / 2$. Figure 5.10(a) depicts an example for the generation of both $2 I_{R E F}$ and $I_{R E F} / 2$; each unit has a width of $W_{0}$ (and the same length).
image_name:Figure 5.10(a)
description:The circuit diagram in Figure 5.10(a) illustrates a current mirror configuration that generates both 2*I_REF and I_REF/2 using NMOS transistors. The transistors M1 and M2 are diode-connected and form the reference current mirror. Transistors M3 to M7 are used to multiply and divide the reference current. Each NMOS transistor in the diagram has a width of W0.
image_name:Figure 5.10(b)
description:The circuit in Figure 5.10(b) is a current mirror that generates both 2*IREF and IREF/2 currents using series transistors. The approach reduces complexity and avoids errors due to LD by doubling the equivalent length with series transistors.
Figure 5.10 Current mirrors providing $I_{R E F} / 2$ from $I_{R E F}$ by (a) half-width device and (b) series transistors.
The above approach requires a large number of unit transistors if many different currents must be generated. It is possible to reduce the complexity by scaling the lengths, but not directly. In order to avoid the errors due to $L_{D}$, we can, for example, double the equivalent length by placing two unit
transistors in series. Illustrated in Fig. 5.10(b), this approach preserves an effective length of $L_{\text {drawn }}-2 L_{D}$ for each unit, yielding an equivalent length of $2\left(L_{\text {drawn }}-2 L_{D}\right)$ for the composite device and hence halving the current. Note that this structure is not a cascode because the bottom device is in the triode region (why?).

We should also mention that current mirrors can process signals as well. In Fig. 5.5(b), for example, if $I_{R E F}$ increases by $\Delta I$, then $I_{\text {out }}$ increases by $\Delta I(W / L)_{2} /(W / L)_{1}$. That is, the circuit amplifies the small-signal current if $(W / L)_{2} /(W / L)_{1}>1$ (but at the cost of proportional multiplication of the bias current).

#### Example 5.2

Calculate the small-signal voltage gain of the circuit shown in Fig. 5.11.
image_name:Figure 5.11
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: Vin}
name: M2, type: PMOS, ports: {S: VDD, D: X, G: X}
name: M3, type: PMOS, ports: {S: VDD, D: Vout, G: X}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a cascode current mirror amplifier. It uses two PMOS transistors (M2 and M3) and one NMOS transistor (M1) to amplify a small-signal input voltage (Vin) into an output voltage (Vout). The resistor RL is connected to the output node Vout and ground.

#### Solution

The small-signal drain current of $M_{1}$ is equal to $g_{m 1} V_{i n}$. Since $I_{D 2}=I_{D 1}$ and $I_{D 3}=I_{D 2}(W / L)_{3} /(W / L)_{2}$, the small-signal drain current of $M_{3}$ is equal to $g_{m 1} V_{i n}(W / L)_{3} /(W / L)_{2}$, yielding a voltage gain of $g_{m 1} R_{L}(W / L)_{3} /(W / L)_{2}$.

## 5.2 ■ Cascode Current Mirrors

In our discussion of current mirrors thus far, we have neglected channel-length modulation. In practice, this effect produces significant error in copying currents, especially if minimum-length transistors are used so as to minimize the width and hence the output capacitance of the current source. For the simple mirror of Fig. 5.5(b), we can write

$$
\begin{align*}
I_{D 1} & =\frac{1}{2} \mu_{n} C_{o x}\left(\frac{W}{L}\right)_{1}\left(V_{G S}-V_{T H}\right)^{2}\left(1+\lambda V_{D S 1}\right)  \tag{5.5}\\
I_{D 2} & =\frac{1}{2} \mu_{n} C_{o x}\left(\frac{W}{L}\right)_{2}\left(V_{G S}-V_{T H}\right)^{2}\left(1+\lambda V_{D S 2}\right) \tag{5.6}
\end{align*}
$$

and hence

$$
\begin{equation*}
\frac{I_{D 2}}{I_{D 1}}=\frac{(W / L)_{2}}{(W / L)_{1}} \cdot \frac{1+\lambda V_{D S 2}}{1+\lambda V_{D S 1}} \tag{5.7}
\end{equation*}
$$

While $V_{D S 1}=V_{G S 1}=V_{G S 2}, V_{D S 2}$ may not equal $V_{G S 2}$ because of the circuitry fed by $M_{2}$. For example, in Fig. 5.8, the potential at node $P$ is determined by the input common-mode level and the gate-source voltage of $M_{1}$ and $M_{2}$, and it may not equal $V_{X}$.

In order to suppress the effect of channel-length modulation in Fig. 5.5(b), we can (1) force $V_{D S 2}$ to be equal to $V_{D S 1}$, or (2) force $V_{D S 1}$ to be equal to $V_{D S 2}$. These two principles lead to two different topologies.

First Approach We begin with the first principle and wish to ensure that $V_{D S 2}$ in Fig. 5.5(b) is both constant and equal to $V_{D S 1}$. Recall from Chapter 3 that a cascode device can shield a current source, thereby reducing the voltage variations across it. As shown in Fig. 5.12(a), even though the analog circuit may allow $V_{P}$ to vary substantially, $V_{Y}$ remains relatively constant. But how do we ensure that $V_{D S 2}=V_{D S 1}$ ? We must generate $V_{b}$ such that $V_{b}-V_{G S 3}=V_{D S 1}\left(=V_{G S 1}\right)$, i.e., $V_{b}=V_{G S 3}+V_{G S 1}$. In other words, $V_{b}$ can be established by two diode-connected devices in series [Fig. 5.12(b)], provided that $V_{G S 0}+V_{G S 1}=V_{G S 3}+V_{G S 1}$, and hence $V_{G S 0}=V_{G S 3}$. We now attach the $V_{b}$ generator of Fig. 5.12(b) to the cascode current source as shown in Fig. 5.12(c). The result allows accurate copying of the current even in the presence of body effect (why?).
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: X}
name: M2, type: NMOS, ports: {S: GND, D: Y, G: X}
name: M3, type: NMOS, ports: {S: Y, D: P, G: Vb}
]
extrainfo:The circuit is a cascode current source with a bias voltage Vb. The NMOS transistors M1, M2, and M3 form the cascode structure, allowing accurate current copying. I_REF is the reference current flowing from VDD to node X.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: X}
name: M0, type: NMOS, ports: {S: X, D: N, G: N}
name: I_REF, type: CurrentSource, value: I_REF, ports: {Np: VDD, Nn: N}
]
extrainfo:The circuit diagram (b) represents a modification of a mirror circuit to generate the cascode bias voltage Vb. It uses two diode-connected NMOS transistors (M0 and M1) in series to establish Vb as V_GS0 + V_GS1. This configuration allows for accurate current copying even in the presence of body effect.
image_name:(c)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: X}
name: M2, type: NMOS, ports: {S: GND, D: Y, G: X}
name: M3, type: NMOS, ports: {S: Y, D: P, G: N}
name: M0, type: NMOS, ports: {S: X, D: N, G: X}
name: I_REF, type: CurrentSource, value: I_REF, ports: {Np: VDD, Nn: N}
]
extrainfo:The circuit is a cascode current mirror designed to accurately mirror the reference current I_REF to the output current I_out, even in the presence of body effect. Transistors M0 and M1 form a bias generator, while M2 and M3 form the cascode current mirror.

Figure 5.12 (a) Cascode current source, (b) modification of mirror circuit to generate the cascode bias voltage, and (c) cascode current mirror.

A few notes on the sizing of the transistors in Fig. 5.12(c) are warranted. As explained earlier, we typically select $L_{2}=L_{1}$ and scale $W_{2}$ (in integer units) with respect to $W_{1}$ to obtain the desired multiple of $I_{R E F}$. Similarly, for $V_{G S 3}$ to be equal to $V_{G S 0}$, we choose $L_{3}=L_{0}$ and scale $W_{3}$ with respect to $W_{0}$ by the same factor, i.e., $W_{3} / W_{0}=W_{2} / W_{1}$. In practice, $L_{3}$ and $L_{0}$ are equal to the minimum allowable value so as to minimize their width, while $L_{1}$ and $L_{2}$ may be longer in some cases. ${ }^{1}$

#### Example 5.3

In Fig. 5.13, sketch $V_{X}$ and $V_{Y}$ as a function of $I_{R E F}$. If $I_{R E F}$ requires 0.5 V to operate as a current source, what is its maximum value?

#### Solution

Since $M_{2}$ and $M_{3}$ are properly ratioed with respect to $M_{1}$ and $M_{0}$, we have $V_{Y}=V_{X} \approx \sqrt{2 I_{R E F} /\left[\mu_{n} C_{o x}(W / L)_{1}\right]}+$ $V_{T H 1}$. The behavior is plotted in Fig. 5.13(b).

To find the maximum value of $I_{R E F}$, we note that

$$
\begin{align*}
V_{N} & =V_{G S 0}+V_{G S 1}  \tag{5.8}\\
& =\sqrt{\frac{2 I_{R E F}}{\mu_{n} C_{o x}}}\left[\sqrt{\left(\frac{L}{W}\right)_{0}}+\sqrt{\left(\frac{L}{W}\right)_{1}}\right]+V_{T H 0}+V_{T H 1} \tag{5.9}
\end{align*}
$$

image_name:Figure 5.13(a)
description:
[
name: M0, type: NMOS, ports: {S: X, D: N, G: N}
name: M1, type: NMOS, ports: {S: GND, D: X, G: X}
name: M2, type: NMOS, ports: {S: GND, D: Y, G: X}
name: M3, type: NMOS, ports: {S: Y, D: VDD, G: N}
]
extrainfo:The circuit is a current mirror with NMOS transistors. IREF is mirrored to Iout through M3. Nodes X and Y are connected to the gates of M1 and M2 respectively, forming a differential pair.
image_name:Figure 5.13(b)
description:The graph labeled (b) is a plot showing the relationship between the reference current $I_{REF}$ on the horizontal axis and the voltages $V_X$ and $V_Y$ on the vertical axis. The vertical axis is labeled with $V_X, V_Y$ and is measured in volts, while the horizontal axis is labeled $I_{REF}$ and is measured in amperes.

**Type of Graph and Function:**
The graph appears to be a voltage-current characteristic curve, specifically showing how the voltages $V_X$ and $V_Y$ vary with changes in the reference current $I_{REF}$. It is likely a part of an electronic circuit analysis, possibly involving MOSFETs given the context.

**Axes Labels and Units:**
- **Horizontal Axis:** $I_{REF}$ (Reference Current), in amperes.
- **Vertical Axis:** $V_X, V_Y$ (Voltages), in volts.

**Overall Behavior and Trends:**
The curve starts at a point on the vertical axis at $V_{TH1}$, indicating the threshold voltage. As $I_{REF}$ increases, the voltages $V_X$ and $V_Y$ rise sharply initially and then level off, suggesting a saturation behavior typical in transistor operation where the increase in voltage becomes less pronounced with higher current.

**Key Features and Technical Details:**
- The starting point of the curve at $V_{TH1}$ indicates the threshold voltage where the transistor begins to conduct.
- The curve shows a rapid increase initially, indicating a strong dependence of the voltages on the reference current at low values.
- As the current increases further, the slope of the curve decreases, indicating a saturation region where the changes in voltage with respect to current are minimal.

**Annotations and Specific Data Points:**
- The graph is marked with $V_{TH1}$ on the vertical axis, indicating the threshold voltage level.
- No specific numerical values or markers are provided on the axes, but the shape suggests typical MOSFET behavior.

Thus,

$$
\begin{equation*}
V_{D D}-\sqrt{\frac{2 I_{R E F}}{\mu_{n} C_{o x}}}\left[\sqrt{\left(\frac{L}{W}\right)_{0}}+\sqrt{\left(\frac{L}{W}\right)_{1}}\right]-V_{T H 0}-V_{T H 1}=0.5 \mathrm{~V} \tag{5.10}
\end{equation*}
$$

and hence

$$
\begin{equation*}
I_{R E F, \max }=\frac{\mu_{n} C_{o x}}{2} \frac{\left(V_{D D}-0.5 \mathrm{~V}-V_{T H 0}-V_{T H 1}\right)^{2}}{\left(\sqrt{(L / W)_{0}}+\sqrt{\left.(L / W)_{1}\right)^{2}}\right.} \tag{5.11}
\end{equation*}
$$

While operating as a current source with a high output impedance and accurate value, the topology of Fig. 5.12(c) nonetheless consumes substantial voltage headroom. For simplicity, let us neglect the body effect and assume that all of the transistors are identical. Then, the minimum allowable voltage at node $P$ is equal to

$$
\begin{align*}
V_{N}-V_{T H} & =V_{G S 0}+V_{G S 1}-V_{T H}  \tag{5.12}\\
& =\left(V_{G S 0}-V_{T H}\right)+\left(V_{G S 1}-V_{T H}\right)+V_{T H} \tag{5.13}
\end{align*}
$$

i.e., two overdrive voltages plus one threshold voltage. How does this value compare with that in Fig. 5.12(a) if $V_{b}$ could be chosen more arbitrarily? As shown in Fig. 5.14(a), $V_{b}$ could be so low
image_name:Figure 5.14 (a)
description:The circuit in Figure 5.14 (a) is a cascode current source configuration. It shows how the minimum allowable voltage at node P can be reduced by adjusting the bias voltage Vb. The circuit uses NMOS transistors M1, M2, and M3 to achieve this configuration, with a reference current I_REF flowing from VDD to ground through these transistors. The diagram illustrates the concept of headroom voltage in a cascode configuration.
image_name:Figure 5.14 (b)
description:The circuit in Figure 5.14(b) is a cascode current mirror with minimum headroom voltage. It ensures Iout = IREF by maintaining VDS2 = VGS1. The configuration uses four NMOS transistors and a reference current source.

Figure 5.14 (a) Cascode current source with minimum headroom voltage; (b) headroom consumed by a cascode mirror.
$\left(=V_{G S 3}+V_{G S 2}-V_{T H 2}\right)$ that the minimum allowable voltage at $P$ is merely two overdrive voltages. Thus, the cascode mirror of Fig. 5.12(c) "wastes" one threshold voltage in the headroom. This is because $V_{D S 2}=V_{G S 2}$, whereas $V_{D S 2}$ could be as low as $V_{G S 2}-V_{T H}$ while maintaining $M_{2}$ in saturation.

Figure 5.14 summarizes our discussion. In Fig. 5.14(a), $V_{b}$ is chosen to allow the lowest possible value of $V_{P}$, but the output current does not accurately track $I_{R E F}$ because $M_{1}$ and $M_{2}$ sustain unequal drain-source voltages. In Fig. 5.14(b), a higher accuracy is achieved, but the minimum level at $P$ is higher by one threshold voltage.

Before resolving this issue, it is instructive to examine the large-signal behavior of a cascode current source.

#### Example 5.4

In Fig. 5.15(a), assume that all of the transistors are identical and sketch $I_{X}$ and $V_{B}$ as $V_{X}$ drops from a large positive value.
image_name:Figure 5.15(a)
description:
[
name: M0, type: NMOS, ports: {S: A, D: N, G: N}
name: M1, type: NMOS, ports: {S: GND, D: A, G: A}
name: M2, type: NMOS, ports: {S: GND, D: B, G: A}
name: M3, type: NMOS, ports: {S: B, D: VX, G: N}
name: I_REF, type: CurrentSource, ports: {Np: VDD, Nn: N}
]
extrainfo:The circuit is a cascode current source with NMOS transistors M0, M1, M2, and M3. The current source I_REF feeds into node N, and the output current IX is taken from the drain of M3. VDD is the power supply voltage, and the ground is the common reference node.
image_name:Figure 5.15(b)
description:The graph labeled (b) is a plot of \( V_B \) versus \( V_X \). It is a voltage transfer characteristic graph that shows how the voltage \( V_B \) at point B changes as \( V_X \) decreases from a high positive value.

1. **Type of Graph and Function:**
- The graph is a voltage transfer characteristic plot.

2. **Axes Labels and Units:**
- The horizontal axis represents \( V_X \), which is the voltage at node X.
- The vertical axis represents \( V_B \), the voltage at point B.
- The graph does not specify units, but typically these would be in volts.

3. **Overall Behavior and Trends:**
- As \( V_X \) decreases, \( V_B \) initially increases linearly.
- The graph shows a saturation point where \( V_B \) levels off and remains constant.

4. **Key Features and Technical Details:**
- The graph starts from the origin (or a value near zero) and increases linearly until it reaches a threshold.
- The threshold point is marked at \( V_N - V_{TH3} \), where \( V_B \) becomes constant.
- The saturation level of \( V_B \) is \( V_N - V_{GS3} \).

5. **Annotations and Specific Data Points:**
- There is a dashed line indicating the point \( V_N - V_{TH3} \) on the \( V_X \) axis, showing where \( V_B \) stops increasing and becomes constant.
- Another horizontal dashed line shows the constant value \( V_N - V_{GS3} \) on the \( V_B \) axis, indicating the saturation level.
image_name:Figure 5.15(c)
description:The graph labeled "(c)" depicts the behavior of the current $I_X$ as a function of the voltage $V_X$. This is a plot relevant to the analysis of a cascode current source.

1. **Type of Graph and Function:**
- The graph is a plot of current versus voltage, specifically showing $I_X$ on the y-axis and $V_X$ on the x-axis.

2. **Axes Labels and Units:**
- **Y-axis:** Labeled as $I_X$, representing the current. The scale is linear and includes a reference line at $I_{REF}$, which is the reference current.
- **X-axis:** Labeled as $V_X$, representing the voltage. The scale is linear, and there are significant markers at specific voltage levels, such as $V_N - V_{TH3}$ and $V_A - V_{TH2} + V_{DS3}$.

3. **Overall Behavior and Trends:**
- The graph shows that as $V_X$ increases from zero, the current $I_X$ initially rises sharply. After reaching a certain voltage threshold, the current levels off and remains constant at $I_{REF}$, indicating that the transistors are in saturation.

4. **Key Features and Technical Details:**
- **Initial Rise:** The current rises sharply from zero as $V_X$ increases until it reaches the reference current $I_{REF}$.
- **Saturation Region:** Beyond the voltage $V_N - V_{TH3}$, the current $I_X$ remains constant at $I_{REF}$, indicating saturation.
- **Thresholds:** The graph marks two critical voltage points: $V_N - V_{TH3}$, which is the point where $I_X$ reaches $I_{REF}$, and $V_A - V_{TH2} + V_{DS3}$, indicating a boundary condition related to the transistor operation.

5. **Annotations and Specific Data Points:**
- The graph includes a dashed line at the level of $I_{REF}$ to indicate the saturation current level.
- Vertical dashed lines at $V_N - V_{TH3}$ and $V_A - V_{TH2} + V_{DS3}$ mark significant voltage thresholds related to the operation of the transistors in the circuit.

#### Solution

For $V_{X} \geq V_{N}-V_{T H}$, both $M_{2}$ and $M_{3}$ are in saturation, $I_{X}=I_{R E F}$ and $V_{B}=V_{A}$. As $V_{X}$ drops, which transistor enters the triode region first, $M_{3}$ or $M_{2}$ ? Suppose $M_{2}$ enters the triode region before $M_{3}$ does. For this to occur, $V_{D S 2}$ must drop and, since $V_{G S 2}$ is constant, so must $I_{D 2}$. This means that $V_{G S 3}$ increases while $I_{D 3}$ decreases, which is not possible if $M_{3}$ is still in saturation. Thus, $M_{3}$ enters the triode region first.

As $V_{X}$ falls below $V_{N}-V_{T H}, M_{3}$ enters the triode region, requiring a greater gate-source overdrive to carry the same current. Thus, as shown in Fig. 5.15 (b), $V_{B}$ begins to drop, causing $I_{D 2}$ and hence $I_{X}$ to decrease slightly. As $V_{X}$ and $V_{B}$ decrease further, eventually we have $V_{B}<V_{A}-V_{T H}$, and $M_{2}$ enters the triode region. At this point, $I_{D 2}$ begins to drop sharply. For $V_{X}=0, I_{X}=0$, and $M_{2}$ and $M_{3}$ operate in the deep triode region. Note that as $V_{X}$ drops below $V_{N}-V_{T H 3}$, the output impedance of the cascode falls rapidly because $g_{m 3}$ degrades in the triode region.

Second Approach In order to avoid the $V_{T H}$ penalty in the voltage headroom of the above cascode current source, we force $V_{D S 1}$ to be equal to $V_{D S 2}$ instead. To understand this principle, we return to Fig. 5.14(a) and recognize that the $V_{T H}$ headroom consumption is eliminated only if $V_{b}=V_{G S 3}+\left(V_{G S 2}-\right.$ $V_{T H 2}$ ), i.e., only if $V_{D S 2}$ is around one overdrive voltage. How can we then ensure that $V_{D S 1}=V_{D S 2}$ $\left(=V_{G S 2}-V_{T H 2}\right)$ ? Since $M_{1}$ is a diode-connected device, it appears impossible to expect a $V_{D S 1}$ less than one threshold.

A simple escape from the foregoing quandary is to create a deliberate voltage difference between the gate and drain of $M_{1}$ by a means of a resistor. Illustrated in Fig. 5.16(a), the idea is to choose $R_{1} I_{R E F} \approx V_{T H 1}$ and $V_{b}=V_{G S 3}+\left(V_{G S 1}-V_{T H 1}\right)$. Now, $V_{D S 1}=V_{G S 1}-R_{1} I_{R E F} \approx V_{G S 1}-V_{T H 1}$, which is equal to $V_{b}-V_{G S 3}$ and hence to $V_{D S 2}$.
image_name:(a)
description:The circuit diagram (a) illustrates a method to improve the accuracy of a current mirror using an IR drop. The NMOS transistors M1 and M2 form the core of the current mirror, with M3 acting as a load. The resistor R1 creates a voltage drop to maintain the required gate-source voltage difference for proper operation. The current source I_REF provides the reference current.
image_name:(b)
description:
[
name: M5, type: NMOS, ports: {S: GND, D: g5d5, G: g5d5}
name: R6, type: Resistor, value: R6, ports: {N1: g5d5, N2: Vb}
name: I6, type: CurrentSource, value: I6, ports: {Np: VDD, Nn: Vb}
]
extrainfo:The circuit in diagram (b) is a biasing circuit that uses a current source I6 and a resistor R6 to generate a bias voltage Vb. NMOS transistor M5 is configured with both its source and drain connected to node g5d5, and its gate connected to the bias voltage Vb.
image_name:(c)
description:
[
name: I6, type: CurrentSource, ports: {Np: VDD, Nn: g6}
name: R6, type: Resistor, value: R6, ports: {N1: g6, N2: Vb}
name: M6, type: NMOS, ports: {S: X, D: Vb, G: g6}
name: M5, type: NMOS, ports: {S: GND, D: X, G: X'}
]
extrainfo:The circuit diagram (c) illustrates a configuration where two NMOS transistors (M5 and M6) are used. The current source I6 provides current from VDD to node g6. Resistor R6 is connected between node g6 and bias voltage Vb, which also serves as the gate voltage for transistor M6. Transistor M5 is connected in a diode configuration with its gate and drain tied together, forming a connection to the source of M6 at node g5d5s6. The circuit is designed to generate a bias voltage Vb using the resistor R6 and current source I6.

Figure 5.16 (a) Use of IR drop to improve accuracy of current mirror, (b) generation of $V_{b}$, and (c) alternative generation of $V_{b}$.

#### Example 5.5

Is the $M_{1}-R_{1}$ combination in Fig. 5.16(a) a diode-connected device? Assume $\lambda>0$.

#### Solution

From the small-signal equivalent shown in Fig. 5.17, we express the voltage drop across $R_{1}$ as $I_{X} R_{1}$ and write a KCL at the drain node:

$$
\begin{equation*}
\frac{V_{X}-I_{X} R_{1}}{r_{O}}+g_{m} V_{X}=I_{X} \tag{5.14}
\end{equation*}
$$

It follows that
image_name:Figure 5.17
description:
[
name: Vx, type: VoltageSource, value: Vx, ports: {Np: X1, Nn: X2}
name: R1, type: Resistor, value: R1, ports: {N1: X1, N2: X3}
name: gmV1, type: VoltageControlledCurrentSource, value: gmV1, ports: {Np: X3, Nn: X2}
name: ro, type: Resistor, value: ro, ports: {N1: X2, N2: X3}
]
extrainfo:The circuit is a small-signal model of a diode-connected NMOS transistor M1 with a resistor R1, a voltage source Vx, and a voltage-controlled current source gmV1 representing the transconductance of M1. The circuit is used to analyze the impedance seen at the drain of M1.

$$
\begin{equation*}
\frac{V_{X}}{I_{X}}=\frac{R_{1}+r_{O}}{1+g_{m} r_{O}} \tag{5.15}
\end{equation*}
$$

which reduces to $1 / g_{m}$ in the absence of channel-length modulation. (Is it a coincidence that this impedance is the same as that seen at the source of a common-gate stage with $\gamma=0$ ?!) Thus, from a small-signal point of view, the combination is close to a diode-connected device. From a large-signal point of view, $V_{G S 1} \approx \sqrt{2 I_{D} /\left[\mu_{n} C_{o x}(W / L)\right]}+$ $V_{T H}$ if $\lambda$ is small, suggesting diode-connected operation as well.

The circuit of Fig. 5.16(a) entails two issues. First, in the presence of PVT variations, it may be difficult to guarantee that $R_{1} I_{R E F} \approx V_{T H 1}$ as $R_{1}$ and $V_{T H}$ may vary differently. Second, the generation of $V_{b}=V_{G S 3}+\left(V_{G S 1}-V_{T H 1}\right)$ is not straightforward. Let us address the latter issue first. We seek an arrangement that adds one gate-source voltage to an overdrive, surmising that we must begin with a diodeconnected device. We consider the branch shown in Fig. 5.16(b) as a candidate and write $V_{b}=V_{G S 5}+R_{6} I_{6}$. We can readily choose $I_{6}$ and the dimensions of $M_{5}$ to ensure that $V_{G S 5}=V_{G S 3}$. However, the condition $R_{6} I_{6}=V_{G S 1}-V_{T H 1}=V_{G S 1}-R_{1} I_{R E F}$ translates to $R_{6} I_{6}+R_{1} I_{R E F}=V_{G S 1}$, which is difficult to meet
because the $I R$ products do not "track" the MOS gate-source voltage. For example, the value of the resistors may fall with temperature while $V_{G S}$ may rise.

Depicted in Fig. 5.16(c) is another example, where $M_{5}$ establishes the $V_{G S}$, and $M_{6}$ and $R_{6}$ the overdrive. We select $I_{6}$ and the device parameters such that

$$
\begin{align*}
& V_{G S 5}=V_{G S 3}  \tag{5.16}\\
& V_{G S 6}-R_{6} I_{6}=V_{G S 1}-V_{T H 1}  \tag{5.17}\\
& =V_{G S 1}-R_{1} I_{R E F} \tag{5.18}
\end{align*}
$$

observing that it is now possible to ensure that $V_{G S 6}$ and $V_{G S 1}$ track each other, and so do $R_{1} I_{R E F}$ and $R_{6} I_{6}$. For example, we may simply choose $I_{6}=I_{R E F}, R_{6}=R_{1}$, and $(W / L)_{6}=(W / L)_{1} .{ }^{2}$

To avoid the first issue mentioned above, we develop another circuit topology that forces the $V_{D S}$ of the diode-connected device to be equal to the $V_{D S}$ of the current source transistor. The level shift between the gate and drain voltages need not be created by a resistor. In particular, suppose we tie the output node of a cascode topology to its input [Fig. 5.18(a)]. In this case, $V_{D S 1}=V_{b}-V_{G S 0}$, and $V_{b}$ can be chosen to place $M_{1}$ at the edge of saturation. We now connect this branch to the main cascode current source as shown in Fig. 5.18(b), recognizing that $V_{D S 1}$ is forced to be equal to $V_{D S 2}$ if $V_{G S 0}=V_{G S 3}$. Called a "low-voltage cascode," this configuration finds wider usage than the regular cascode shown in Fig. 5.14(b).
image_name:(a)
description:
[
name: I_REF, type: CurrentSource, value: I_REF, ports: {Np: VDD, Nn: X}
name: M0, type: NMOS, ports: {S: A, D: X, G: Vb}
name: M1, type: NMOS, ports: {S: GND, D: A, G: X}
]
extrainfo:This is a low-voltage cascode configuration with two NMOS transistors, M0 and M1, connected in series. The gate of M0 is controlled by the bias voltage Vb, while the gate of M1 is connected to node X. The current source I_REF provides a reference current from VDD to node X.

image_name:(b)
description:
[
name: I_REF, type: CurrentSource, ports: {Np: VDD, Nn: X}
name: M0, type: NMOS, ports: {S: A, D: X, G: Vb}
name: M1, type: NMOS, ports: {S: GND, D: A, G: X}
name: M2, type: NMOS, ports: {S: GND, D: B, G: X}
name: M3, type: NMOS, ports: {S: B, D: Iout, G: Vb}
]
extrainfo:The circuit is a modification of a cascode current mirror for low-voltage operation. It uses NMOS transistors M0, M1, M2, and M3, with a bias voltage Vb applied to control the gates of M0 and M3. The configuration ensures that all transistors remain in saturation for proper current mirroring. The output current Iout is drawn from the node B through the load.

Figure 5.18 Modification of cascode mirror for low-voltage operation.

We must now answer two questions. First, how do we choose $V_{b}$ in Fig. 5.18(a) so that both $M_{1}$ and $M_{0}$ are in saturation? We must have $V_{b}-V_{T H 0} \leq V_{X}\left(=V_{G S 1}\right)$ for $M_{0}$ to be saturated and $V_{G S 1}-V_{T H 1} \leq V_{A}$ $\left(=V_{b}-V_{G S 0}\right)$ for $M_{1}$ to be saturated. Thus,

$$
\begin{equation*}
V_{G S 0}+\left(V_{G S 1}-V_{T H 1}\right) \leq V_{b} \leq V_{G S 1}+V_{T H 0} \tag{5.19}
\end{equation*}
$$

A solution exists if $V_{G S 0}+\left(V_{G S 1}-V_{T H 1}\right)<V_{G S 1}+V_{T H 0}$, i.e., if $V_{G S 0}-V_{T H 0}<V_{T H 1}$. We must therefore size $M_{0}$ to ensure that its overdrive is well below $V_{T H 1}$.

The second question is how to generate $V_{b}$. For minimal voltage headroom consumption, $V_{A}=V_{G S 1}-V_{T H 1}$, and hence $V_{b}$ must be equal to (or slightly greater than) $V_{G S 0}+\left(V_{G S 1}-V_{T H 1}\right)$. Figure 5.19(a) depicts an example where $M_{5}$ generates $V_{G S 5} \approx V_{G S 0}$ and $M_{6}$ together with $R_{b}$

image_name:Figure 5.19(a)
description:This circuit generates a gate voltage Vb for cascode mirrors. M5 and M6 are used to create the voltage Vb. M0 and M1 form a cascode configuration with Vb as the bias voltage.
image_name:Figure 5.19(b)
description:The circuit is a cascode mirror with a diode-connected NMOS (M7) providing biasing voltage Vb. The current source I1 supplies current from VDD to Vb. NMOS transistors M0 and M1 are configured to provide a cascoded output at node A.

Figure 5.19 Generation of gate voltage $V_{b}$ for cascode mirrors.
produces $V_{D S 6}=V_{G S 6}-R_{b} I_{1} \approx V_{G S 1}-V_{T H 1}$. Some inaccuracy nevertheless arises because $M_{5}$ does not suffer from body effect whereas $M_{0}$ does. Also, the magnitude of $R_{b} I_{1}$ is not well-controlled.

A simpler alternative is shown in Fig. 5.19(b), where the diode-connected transistor $M_{7}$ provides the necessary $V_{G S}$ and $M_{6}$ creates a $V_{D S}$ equal to the required overdrive.

#### Example 5.6

Shown in Fig. 5.20(a) is a differential pair along with its bias network. In this particular design, the voltage headroom is too small to allow the use of a cascode current source. Devise a method to reduce the current mirror error due to channel-length modulation.
image_name:Figure 5.20(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: g1g2d1, G: g1g2d1}
name: M2, type: NMOS, ports: {S: GND, D: P, G: g1g2d1}
name: M3, type: NMOS, ports: {S: VDD, D: LOAD, G: A}
name: M4, type: NMOS, ports: {S: P, D: LOAD, G: B}
name: I_REF, type: CurrentSource, value: I_REF, ports: {Np: VDD, Nn: g1g2d1}
name: V_DD, type: VoltageSource, value: V_DD, ports: {Np: VDD, Nn: GND}
]
extrainfo:This circuit is a differential pair with a bias network. It includes NMOS transistors M1 to M4 and a current source I_REF. The circuit aims to maintain equal V_DS across M1 and M2 to reduce current mirror error due to channel-length modulation.
image_name:Figure 5.20(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: "P", G: g1g2d3d4}
name: M2, type: NMOS, ports: {S: GND, D: P, G: "g1g2d3d4"}
name: M3, type: NMOS, ports: {S: P', D: g1g2d3d4, G: A}
name: M4, type: NMOS, ports: {S: P', D: g1g2d3d4, G: B}
name: M5, type: NMOS, ports: {S: P, D: LOAD, G: A}
name: M6, type: NMOS, ports: {S: P, D: LOAD, G: B}
name: IREF, type: CurrentSource, value: IREF, ports: {Np: VDD, Nn: g1g2d3d4'}
]
extrainfo:The circuit is a differential pair with a bias network. It includes a current mirror formed by M3 and M4. The circuit is designed to minimize current mirror error due to channel-length modulation by ensuring that VDS1 equals VDS2 through the use of additional transistors M5 and M6.

#### Solution

Since the limited headroom does not allow us to make $V_{D S 2}$ equal to $V_{D S 1}$, we seek to make $V_{D S 1}$ equal to $V_{D S 2}$. As exemplified by Fig. 5.16(a), we can simply insert a resistor in series with the drain of $M_{1}$ and select the voltage drop across it such that $V_{D S 1}=V_{D S 2}$. However, if variations in the circuit preceding the differential pair change the common-mode level at $A$ and $B$, then $V_{D S 1} \neq V_{D S 2}$. We must therefore force the voltage at node $P$ upon the drain of $M_{1}$. Let us replicate the differential pair and insert the replica as shown in Fig. 5.20(b). Now, the voltages at $P^{\prime}$ and $P$ track even if the CM level at $A$ and $B$ varies. To ensure that $V_{P^{\prime}}=V_{P}$, the two differential pairs must incorporate the same lengths and scale their widths according to $W_{r} / W_{d}=I_{R E F} / I_{S S}$. Of course, if the CM level at $A$ and $B$ rises excessively, the replica transistors enter the triode region, introducing some error.

Example 5.7
Figure 5.21(a) shows an alternative current mirror exhibiting a high output impedance. Study the small-signal and large-signal properties of the circuit.
image_name:Figure 5.21(a)
description:
[
name: I_REF, type: CurrentSource, value: I_REF, ports: {Np: VDD, Nn: N}
name: V_DD, type: VoltageSource, value: V_DD, ports: {Np: VDD, Nn: GND}
name: V_X, type: VoltageSource, value: V_X, ports: {Np: X, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: X, G: N}
name: M2, type: NMOS, ports: {S: GND, D: N, G: N}
name: M3, type: NMOS, ports: {S: GND, D: N, G: X}
]
extrainfo:The circuit is a high output impedance current mirror. It uses NMOS transistors M1, M2, and M3 to mirror the reference current I_REF to the output node X. The voltage V_X is used to control the output node X.

image_name:(b)
description:The graph labeled as "(a)" is a plot of the drain current \( I_{D1} \) against the control voltage \( V_X \). This is a typical characteristic curve for a MOSFET device, illustrating how the currenb through the transistor changes with varying gate-source voltage.

1. **Type of Graph and Function:**
- This is a characteristic curve graph for an NMOS transistor, specifically showing the relationship between drain current and gate-source voltage.

2. **Axes Labels and Units:**
- The horizontal axis represents the voltage \( V_X \), which is the control voltage applied to the output node. The units are volts (V).
- The vertical axis represents the drain current \( I_{D1} \), with units in amperes (A).

3. **Overall Behavior and Trends:**
- The graph starts with a steep increase in \( I_{D1} \) as \( V_X \) increases from a low value, indicating the transistor is turning on.
- After reaching a certain threshold, the graph levels off, indicating saturation where the current remains relatively constant despite further increases in \( V_X \).
- Beyond a certain point (marked as \( V_{TH3} \)), the current begins to decrease, showing that \( M_1 \) begins to turn off.

4. **Key Features and Technical Details:**
- The curve has distinct regions separated by threshold voltages \( V_{GS1} - V_{TH1} \) and \( V_{TH3} \), where behavior changes from linear increase to saturation, and finally to a decrease.
- The point where \( M_1 \) begins to turn off is annotated on the graph.
- This behavior is typical for a MOSFET operating in different regions: cutoff, saturation, and finally the onset of cutoff again.

5. **Annotations and Specific Data Points:**
- The graph includes vertical dashed lines indicating important threshold voltages: \( V_{GS1} - V_{TH1} \) and \( V_{TH3} \).
- An annotation "\( M_1 \) begins to turn off" indicates the point of interest where the current begins to decrease.

#### Solution

In this circuit, $M_{3}$ raises the output impedance by sensing the voltage change at node $X$ and adjusting the voltage at node $N$. For example, suppose $V_{X}$ rises by $\Delta V$ and tends to increase $I_{D 1}$ by $\Delta V / r_{O 1}$. Transistor $M_{3}$ then draws a current change of $g_{m 3} \Delta V$ from node $N$, causing $V_{N}$ to fall by approximately $g_{m 3} \Delta V / g_{m 2}$ and $I_{D 1}$ to decrease by $\left(g_{m 3} \Delta V / g_{m 2}\right) g_{m 1}$. In other words, if we choose $g_{m 3} g_{m 1} / g_{m 2} \approx r_{O 1}^{-1}$, the net change in $I_{D 1}$ is small.

The circuit displays interesting large-signal properties. Let us sweep $V_{X}$ from 0 to a high value and examine $I_{D 1}$. At $V_{X}=0, M_{1}$ operates in the deep triode region, carrying a zero current, and $M_{3}$ is off. As $V_{X}$ rises, so does $I_{D 1}$ proportionally, up to $V_{X}=V_{G S 1}-V_{T H 1}$. Beyond this point, $I_{D 1}$ varies more gradually [Fig. 5.21(b)]. If $V_{X}$ exceeds $V_{T H 3}, M_{3}$ turns on and begins to "regulate" $I_{D 1}$, creating a higher output impedance. However, for a sufficiently large $V_{X}, M_{3}$ absorbs all of $I_{R E F}$ and turns $M_{1}$ off.

While providing a high output impedance without a cascode device, the above circuit does pose its own voltage headroom limitation, i.e., $V_{X}$ must exceed $V_{T H 3}\left(>V_{D S, s a t}\right)$.

## 5.3 ■ Active Current Mirrors

As mentioned earlier and exemplified by the circuit of Fig. 5.11, current mirrors can also process signals, i.e., operate as "active" elements. Particularly useful is a type of mirror topology used in conjunction with differential pairs. In this section, we study this circuit and its properties. Shown in Fig. 5.22 and sometimes called a five-transistor "operational transconductance amplifier" (OTA), this topology finds application in many analog and digital systems and merits a detailed study here. Note that the output is single-ended; hence the circuit is sometimes used to convert differential signals to a single-ended output. We analyze a simpler topology with passive load before studying the OTA.

Differential Pair with Passive Load To generate a single-ended output, we may simply discard one output of a differential pair as shown in Fig. 5.23(a). Here, a current source in a "passive " mirror arrangement serves as the load. What is the small-signal gain, $A_{v}=V_{\text {out }} / V_{\text {in }}$, of this circuit? We
image_name:Figure 5.22
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin1}
name: M2, type: NMOS, ports: {S: P, D: Vout, G: Vin2}
name: M3, type: PMOS, ports: {S: VDD, D: X, G: X}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: X}
name: I1, type: CurrentSource, value: I1, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a five-transistor operational transconductance amplifier (OTA). The differential pair M1 and M2 are loaded by a current mirror formed by M3 and M4. The circuit is used for converting differential input signals to a single-ended output.
image_name:(a)
description:The circuit diagram (a) represents a differential pair with a current-source load. The NMOS transistors M1 and M2 form the differential pair, while PMOS transistors M3 and M4 serve as the current-source load. The current sources I1 and Iss provide biasing. The output is taken from the drain of M4, labeled as Vout. Resistors ro4, Rout, ro2, and ro1 are used to model various resistances in the circuit.
image_name:(b)
description:The circuit (b) is a differential pair with a current-source load. It features NMOS transistors M1 and M2, and PMOS transistors M3 and M4. Current sources I1 and Iss provide biasing. The output is taken at Vout. Resistors ro4, Rout, ro2, and ro1 are part of the load and biasing network.
image_name:(c)
description:The circuit diagram (c) represents a differential pair with a current-source load. It includes an NMOS transistor M2 with its source connected to node s2, drain to Vout, and gate to Vb. Resistors ro4 and Rout are connected between VDD and Vout, and Vout and GND respectively. Resistors ro2 and ro1 connect Vb and s2 to GND.

Figure 5.23 (a) Differential pair with current-source load; (b) circuit for calculation of $G_{m}$; (c) circuit for calculation of $R_{\text {out }}$.
calculate $A_{v}$ using two different approaches, assuming $\gamma=0$ for simplicity. Owing to the asymmetry, the half-circuit concept cannot be applied directly here.

Writing $\left|A_{v}\right|=G_{m} R_{\text {out }}$, we must compute the short-circuit transconductance, $G_{m}$, and the output resistance, $R_{\text {out }}$. We recognize from Fig. $5.23(\mathrm{~b})$ that $M_{1}$ and $M_{2}$ become symmetric when the output is shorted to ac ground. Thus, $G_{m}=I_{o u t} / V_{i n}=\left(g_{m 1} V_{i n} / 2\right) / V_{i n}=g_{m 1} / 2$. As illustrated in Fig. 5.23(c), for the $R_{\text {out }}$ calculation, $M_{2}$ is degenerated by the source output impedance of $M_{1}, R_{d e g}=\left(1 / g_{m 1}\right) \| r_{O 1}$, thereby exhibiting an output impedance equal to $\left(1+g_{m 2} r_{O 2}\right) R_{d e g}+r_{O 2} a \approx 2 r_{O 2}$. It follows that $R_{\text {out }}=\left(2 r_{O 2}\right) \| r_{O 4}$, and

$$
\begin{equation*}
\left|A_{v}\right|=\frac{g_{m 1}}{2}\left[\left(2 r_{O 2}\right) \| r_{O 4}\right] \tag{5.20}
\end{equation*}
$$

Interestingly, if $r_{O 4} \rightarrow \infty$, then $A_{v} \rightarrow-g_{m 1} r_{O 2}$.
In our second approach, we calculate $V_{P} / V_{\text {in }}$ and $V_{\text {out }} / V_{P}$ in Fig. 5.23(a) and multiply the results to obtain $V_{\text {out }} / V_{\text {in }}$. With the aid of Fig. 5.24 and viewing $M_{1}$ as a source follower, we write

$$
\begin{equation*}
\frac{V_{P}}{V_{i n}}=\frac{R_{e q} \| r_{O 1}}{R_{e q} \| r_{O 1}+\frac{1}{g_{m 1}}} \tag{5.21}
\end{equation*}
$$

image_name:Figure 5.24
description:
[
name: M1, type: NMOS, ports: {S: P, D: VDD, G: Vin}
name: M2, type: NMOS, ports: {S: P, D: Vout, G: GND}
name: ro4, type: Resistor, value: ro4, ports: {N1: VDD, N2: Vout}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is designed to calculate the voltage gain Vout/Vin using a source follower configuration with NMOS transistors M1 and M2. The circuit includes a current source Iss and resistors  ro4, with the output taken across ro4.

Figure 5.24 Circuit for calculation of $V_{P} / V_{\text {in }}$.
where $R_{e q}$ denotes the resistance seen looking into the source of $M_{2}$. Since the drain of $M_{2}$ is terminated by a relatively large resistance, $r_{O 4}$, the value of $R_{e q}$ must be obtained from Eq. (3.117):

$$
\begin{equation*}
R_{e q}=\frac{r_{O 2}+r_{O 4}}{1+g_{m 2} r_{O 2}} \tag{5.22}
\end{equation*}
$$

It follows that

$$
\begin{equation*}
\frac{V_{P}}{V_{i n}}=\frac{g_{m 1} r_{O 1}\left(r_{O 2}+r_{O 4}\right)}{\left(1+g_{m 1} r_{O 1}\right)\left(r_{O 2}+r_{O 4}\right)+\left(1+g_{m 2} r_{O 2}\right) r_{O 1}} \tag{5.23}
\end{equation*}
$$

We now calculate $V_{\text {out }} / V_{P}$. From Fig. 5.25,

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{P}}=\frac{\left(1+g_{m 2} r_{O 2}\right) r_{O 4}}{r_{O 2}+r_{O 4}} \tag{5.24}
\end{equation*}
$$

image_name:Figure 5.25 Circuit for calculation of $V_{\text {out }} / V_{P}$.
description:
[
name: ro4, type: Resistor, value: ro4, ports: {N1: VDD, N2: Vout}
name: ro2, type: Resistor, value: ro2, ports: {N1: Vout, N2: Vp}
name: M2, type: NMOS, ports: {S: Vp, D: Vout, G: Vb}
name: Vp, type: VoltageSource, value: Vp, ports: {Np: Vp, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with an active load, using NMOS transistor M2 and resistors ro2 and ro4. The output voltage Vout is taken from the drain of M2. Vp is the input voltage source.

From (5.23) and (5.24), we have

$$
\begin{align*}
\frac{V_{\text {out }}}{V_{\text {in }}} & =\frac{g_{m 2} r_{O 2} r_{O 4}}{2 r_{O 2}+r_{O 4}}  \tag{5.25}\\
& =\frac{g_{m 2}}{2}\left[\left(2 r_{O 2}\right) \| r_{O 4}\right] \tag{5.26}
\end{align*}
$$

Differential Pair with Active Load In the circuit of Fig. 5.23(a), the small-signal drain current of $M_{1}$ is "wasted." As conceptually shown in Fig. 5.26(a), it is desirable to utilize this current with proper polarity at the output. This can be accomplished by the five-transistor OTA shown in Fig. 5.26(b), where $M_{3}$ and $M_{4}$ are identical and operate as an active current mirror.
image_name:(a)
description:The circuit is a differential pair with an active load. M3 and M4 form an active current mirror to enhance the gain. The input nodes are Vip and Vin, and the output node is Vout. The current source Iss provides biasing.
image_name:(b)
description:The circuit is a five-transistor operational transconductance amplifier (OTA) with a differential pair (M1 and M2) and an active load (M3 and M4). The current source Iss provides biasing. The differential input is applied to M1 and M2, and the output is taken at Vout. M3 and M4 form a current mirror to enhance gain.
image_name:(c)
description:The circuit is a differential pair with an active load, utilizing a five-transistor operational transconductance amplifier (OTA) configuration. The NMOS transistors M1 and M2 form the differential pair, while PMOS transistors M3 and M4 act as a current mirror load, enhancing the gain by combining the drain currents of M1 and M2.

Figure 5.26 (a) Concept of combining the drain currents of $M_{1}$ and $M_{2}$, (b) realization of (a), and (c) response of the circuit to differential inputs.

To see how $M_{3}$ enhances the gain, suppose the gate voltages of $M_{1}$ and $M_{2}$ change by equal and opposite amounts [Fig. 5.26(c)]. Consequently, $I_{D 1}$ increases, $V_{F}$ falls, and $I_{D 2}$ decreases. Thus, the output voltage rises by means of two mechanisms: $M_{2}$ draws less current from $X$ to ground and $M_{4}$ pushes a greater current from $V_{D D}$ to $X$. By contrast, in the circuit of Fig. 5.23(a), $M_{4}$ plays no active role in changing $V_{\text {out }}$ because its gate voltage is constant. The five-transistor OTA is also called a differential pair with active load.

### 5.3.1 Large-Signal Analysis

Let us study the large-signal behavior of the five-transistor OTA. To this end, we replace the ideal tail current source by a MOSFET as shown in Fig. 5.27(a). If $V_{i n 1}$ is much more negative than $V_{i n 2}, M_{1}$ is off, and so are $M_{3}$ and $M_{4}$. Since no current can flow from $V_{D D}$, both $M_{2}$ and $M_{5}$ operate in the deep triode region, carrying zero current. Thus, $V_{\text {out }}=0 .{ }^{3}$ As $V_{i n 1}$ approaches $V_{i n 2}, M_{1}$ turns on, drawing a fraction of $I_{D 5}$ from $M_{3}$ and turning $M_{4}$ on. The output voltage then depends on the difference between $I_{D 4}$ and $I_{D 2}$. For a small difference between $V_{i n 1}$ and $V_{i n 2}$, both $M_{2}$ and $M_{4}$ are saturated, providing a high gain [Fig. 5.27(b)]. As $V_{i n 1}$ becomes more positive than $V_{i n 2}, I_{D 1},\left|I_{D 3}\right|$, and $\left|I_{D 4}\right|$ increase and $I_{D 2}$ decreases, allowing $V_{\text {out }}$ to rise and eventually driving $M_{4}$ into the triode region. If $V_{i n 1}-V_{i n 2}$ is sufficiently large, $M_{2}$ turns off, $M_{4}$ operates in the deep triode region with zero current, and $V_{\text {out }}=V_{D D}$.
image_name:Figure 5.27 (a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: F, G: Vin1}
name: M2, type: NMOS, ports: {S: P, D: Vout, G: Vin2}
name: M3, type: PMOS, ports: {S: VDD, D: F, G: F}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: F}
name: M5, type: NMOS, ports: {S: GND, D: P, G: Vb}
]
extrainfo:The circuit is a differential amplifier with an active current mirror load. M1 and M2 form a differential pair, M3 and M4 act as a current mirror, and M5 provides biasing.
image_name:Figure 5.27 (b)
description:Figure 5.27(b) shows a large-signal input-output characteristic graph for a differential pair circuit. The graph is a plot of the output voltage \( V_{out} \) versus the differential input voltage \( V_{in1} - V_{in2} \).

1. **Type of Graph and Function:**
- The graph is a voltage transfer characteristic curve, commonly used to depict the behavior of differential amplifiers.

2. **Axes Labels and Units:**
- The x-axis represents the differential input voltage \( V_{in1} - V_{in2} \), typically in volts.
- The y-axis represents the output voltage \( V_{out} \), also in volts.
- The graph is plotted with a linear scale on both axes.

3. **Overall Behavior and Trends:**
- The curve starts at a low output voltage when \( V_{in1} - V_{in2} \) is negative, indicating that the output is initially low.
- As \( V_{in1} - V_{in2} \) increases, the output voltage \( V_{out} \) rises sharply, indicating a high-gain region.
- The curve eventually levels off, approaching the supply voltage \( V_{DD} \) as \( V_{in1} - V_{in2} \) becomes sufficiently positive.

4. **Key Features and Technical Details:**
- The graph shows a high-gain region where small changes in \( V_{in1} - V_{in2} \) result in large changes in \( V_{out} \).
- The curve is sigmoidal, with an initial flat region, a steep linear region, and a final saturation region.
- The saturation region occurs when \( V_{out} \) approaches \( V_{DD} \), indicating that the transistors are either in cutoff or deep triode region.

5. **Annotations and Specific Data Points:**
- The graph is annotated with a label indicating the 'High-Gain Region.'
- The output voltage \( V_{out} \) reaches \( V_{DD} \) in the saturation region, showing the limits of the output range.

Figure 5.27 (a) Differential pair with active current mirror and realistic current source; (b) large-signal input-output characteristic.

Note that if $V_{i n 1}>V_{F}+V_{T H}$, then $M_{1}$ enters the triode region. Also, $V_{\text {out }}$ is in-phase with respect to $V_{i n 1}$ but $180^{\circ}$ out of phase with respect to $V_{i n 2}$.

The choice of the input common-mode voltage of the circuit is also important. For $M_{2}$ to be saturated, the output voltage cannot be less than $V_{i n, C M}-V_{T H}$. Thus, to allow maximum output swings, the input CM level must be as low as possible, with the minimum given by $V_{G S 1,2}+V_{D S 5, \min }$. The constraint imposed by the input CM level upon the output swing in this circuit is a critical drawback.

What is the output voltage of the circuit when $V_{\text {in1 }}=V_{\text {in } 2}$ ? With perfect symmetry, $V_{\text {out }}=V_{F}=$ $V_{D D}-\left|V_{G S 3}\right|$. This can be proved by contradiction as well. Suppose, for example, that $V_{\text {out }}<V_{F}$. Then, due to channel-length modulation, $M_{1}$ must carry a greater current than $M_{2}$ (and $M_{4}$ a greater current than $M_{3}$ ). In other words, the total current through $M_{1}$ is greater than half of $I_{S S}$. But this means that the total current through $M_{3}$ also exceeds $I_{S S} / 2$, violating the assumption that $M_{4}$ carries more current than $M_{3}$. In reality, however, asymmetries in the circuit may result in a large deviation in $V_{\text {out }}$, possibly driving $M_{2}$ or $M_{4}$ into the triode region. For example, if the threshold voltage of $M_{2}$ is slightly smaller than that of $M_{1}$, the former carries a greater current than the latter even with $V_{i n 1}=V_{i n 2}$, causing $V_{\text {out }}$ to drop significantly. For this reason, the circuit is rarely used in an open-loop configuration to amplify small signals. Nonetheless, the open-loop OTA proves useful as a differential to a single-ended converter for large swings, as illustrated by the following example.

#### Example 5.8

Some digital circuits operate with differential (complementary) signals having voltage swings less than $V_{D D}$. For example, the single-ended swing can be $300 \mathrm{mV}_{p p}$. Explain how a five-transistor OTA can convert the moderate-swing differential signals to a single-ended rail-to-rail signal.

#### Solution

Consider the OTA shown in Fig. 5.28, where $M_{1}$ and $M_{2}$ sense swings equal to $V_{2}-V_{1}=300 \mathrm{mV}$. With proper choice of $(W / L)_{1,2}$ and $I_{S S}$, we can guarantee that such a swing turns off one side. For example, if $M_{1}$ carries all of $I_{S S}$, then $M_{2}$ remains off, allowing $M_{4}$ to pull $V_{\text {out }}$ to $V_{D D}$. Conversely, when $M_{2}$ hogs $I_{S S}, M_{1}, M_{2}$, and $M_{4}$ turn off, $M_{2}$ and $M_{5}$ remain on with zero current, and $V_{\text {out }}=0$. The "push-pull" action between $M_{2}$ and $M_{4}$ thus produces rail-to-rail swings at the output.
image_name:Figure 5.28
description:
[
name: M1, type: NMOS, ports: {S: P, D: F, G: vip}
name: M2, type: NMOS, ports: {S: P, D: X, G: vin}
name: M3, type: PMOS, ports: {S: VDD, D: F, G: F}
name: M4, type: PMOS, ports: {S: VDD, D: X, G: F}
name: M5, type: NMOS, ports: {S: P, D: GND, G: Vb}
]
extrainfo:The circuit is an operational transconductance amplifier (OTA) with NMOS and PMOS transistors. It uses a differential pair (M1 and M2) with a current source (M5) and active load (M3 and M4). The output is taken from node X. The circuit is designed to produce rail-to-rail swings at the output.

In practice, $V_{\text {out }}$ does not reach exactly $V_{D D}$ or zero if $V_{1}>V_{T H 1,2}$. The proof is left as an exercise for the reader. (Hint: if $M_{2}$ and $M_{5}$ are in the deep triode region, then $V_{P}$ approaches zero, possibly turning on $M_{1}$.) For this reason, the OTA is typically followed by a CMOS inverter to obtain rail-to-rail swings.

#### Example 5.9

Assuming perfect symmetry, sketch the output voltage of the circuit in Fig. 5.29(a) as $V_{D D}$ varies from 3 V to zero. Assume that for $V_{D D}=3 \mathrm{~V}$, all of the devices are saturated.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: F, G: Vip}
name: M2, type: NMOS, ports: {S: P, D: Vout, G: Vin}
name: M3, type: PMOS, ports: {S: VDD, D: F, G: F}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: F}
name: M5, type: NMOS, ports: {S: GND, D: P, G: Vb}
]
extrainfo:The circuit is a differential amplifier with PMOS current mirror load. M1 and M2 form the differential pair, while M3 and M4 form the current mirror. M5 acts as a current source.
image_name:(b)
description:The graph in Figure 5.29(b) is a plot of the output voltage \( V_{\text{out}} \) versus the supply voltage \( V_{DD} \). It is a linear graph depicting how the output voltage changes as \( V_{DD} \) varies from 0 to 3 volts.

1. **Type of Graph and Function:**
- The graph is a linear plot.
- It represents the relationship between the output voltage \( V_{\text{out}} \) and the supply voltage \( V_{DD} \).

2. **Axes Labels and Units:**
- The horizontal axis represents \( V_{DD} \) in volts, ranging from 0 to +3 V.
- The vertical axis represents \( V_{\text{out}} \) in volts.

3. **Overall Behavior and Trends:**
- The graph shows an increasing trend of \( V_{\text{out}} \) as \( V_{DD} \) increases.
- Initially, at low values of \( V_{DD} \), the slope is gentle, indicating a slower increase in \( V_{\text{out}} \).
- As \( V_{DD} \) approaches 3 V, the slope becomes steeper, indicating a more rapid increase in \( V_{\text{out}} \).
- The graph suggests that \( V_{\text{out}} \) reaches a maximum value of \( 3V - |V_{GS3}| \) when \( V_{DD} \) is +3 V.

4. **Key Features and Technical Details:**
- The graph crosses the \( V_{DD} \) axis at \( V_{THP} \), which is the threshold voltage for the PMOS.
- The slope of the graph is close to unity beyond \( V_{THP} \), indicating a linear relationship between \( V_{DD} \) and \( V_{\text{out}} \).

5. **Annotations and Specific Data Points:**
- The graph is annotated with \( 3V - |V_{GS3}| \) as the maximum \( V_{\text{out}} \) value.
- The threshold voltage \( V_{THP} \) is marked on the \( V_{DD} \) axis, indicating where the output starts to increase significantly.

Figure 5.29

#### Solution

For $V_{D D}=3 \mathrm{~V}$, symmetry requires that $V_{\text {out }}=V_{F}$. As $V_{D D}$ drops, so do $V_{F}$ and $V_{\text {out }}$ with a slope close to unity [Fig. 5.29(b)]. As $V_{F}$ and $V_{\text {out }}$ fall below $+1.5 \mathrm{~V}-V_{T H N}, M_{1}$ and $M_{2}$ enter the triode region, but their drain currents are constant if $M_{5}$ is saturated. Further decrease in $V_{D D}$ and hence $V_{F}$ and $V_{\text {out }}$ causes $V_{G S 1}$ and $V_{G S 2}$ to increase, eventually driving $M_{5}$ into the triode region. Thereafter, the bias current of all of the transistors drops, lowering the rate at which $V_{\text {out }}$ decreases. For $V_{D D}<\left|V_{T H P}\right|$, we have $V_{\text {out }}=0$.

#### Example 5.10

Sketch the large-signal input-output characteristic of the unity-gain buffer shown in Fig. 5.30(a) if the op amp is realized as a five-transistor OTA.
image_name:Figure 5.30(a)
description:
[
name: A, type: OpAmp, value: A, ports: {InP: Vin, InN: Vout, OutP: Vout}
]
extrainfo:The circuit is a unity-gain buffer using a five-transistor operational transconductance amplifier (OTA). The op-amp is configured with feedback to maintain Vout equal to Vin.
image_name:Figure 5.30(b)
description:
[
name: M1, type: NMOS, ports: {S: P, D: d1d3g3g4, G: Vin}
name: M2, type: NMOS, ports: {S: P, D: Vout, G: Vout}
name: M3, type: PMOS, ports: {S: VDD, D: d1d3g3g4, G: d1d3g3g4}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: d1d3g3g4}
name: M5, type: NMOS, ports: {S: GND, D: P, G: Vb}
]
extrainfo:The circuit is a unity-gain buffer using a five-transistor operational transconductance amplifier (OTA). M5 acts as a current source, and M1 and M2 form a differential pair. M3 and M4 are active loads. The output voltage Vout is fed back to the input of the op-amp to maintain unity gain.
image_name:Figure 5.30(c)
description:The graph in Figure 5.30(c) represents the large-signal input-output characteristic of a unity-gain buffer using a five-transistor operational transconductance amplifier (OTA). This is a voltage transfer characteristic graph.

1. **Type of Graph and Function:**
- The graph is a voltage transfer characteristic curve showing the relationship between input voltage (V_in) and output voltage (V_out).

2. **Axes Labels and Units:**
- The horizontal axis represents the input voltage, V_in.
- The vertical axis represents the output voltage, V_out.
- Both axes are likely in volts, though specific units are not labeled on the graph.

3. **Overall Behavior and Trends:**
- The graph starts at the origin, indicating that when V_in is zero, V_out is also zero.
- As V_in increases, V_out initially rises slowly, indicating a non-linear region at low input voltages.
- After surpassing a certain threshold voltage (V_TH), the curve becomes linear, indicating that V_out approximately equals V_in. This is the expected behavior for a unity-gain buffer.
- As V_in continues to increase, the graph shows a deviation from the linear behavior, indicating that M_4 enters the triode region, which affects the linearity.

4. **Key Features and Technical Details:**
- The threshold voltage (V_TH) is marked on the graph, showing the point where the behavior changes from non-linear to linear.
- The linear region is depicted with a dashed line, representing the ideal V_out = V_in line.
- The point where M_4 enters the triode region is annotated, indicating the onset of non-linearity due to this transistor's behavior.

5. **Annotations and Specific Data Points:**
- Annotations indicate the transition points such as V_TH and the region where M_4 enters the triode region, highlighting the non-ideal behavior at higher input voltages.
- The ideal linear behavior is illustrated with a dashed line for reference, showing how actual performance deviates from the ideal as conditions change.

#### Solution

Drawing the circuit as shown in Fig. 5.30(b), we begin with $V_{i n}=0$ and note that $M_{1}, M_{3}$, and $M_{4}$ are off. Thus, $M_{5}$ enters the triode region with zero drain current and the diode-connected device $M_{2}$ sustains a zero $V_{G S} .{ }^{4}$ We therefore have $V_{\text {out }}=V_{P}=0[$ Fig. 5.30 (c) $]$. As $V_{\text {in }}$ rises and exceeds one threshold, $M_{1}$ begins to draw current from $M_{3}$,

turning $M_{4}$ and hence $M_{2}$ on. Note that, since $I_{D 3} \approx I_{D 4}$, we have $I_{D 1} \approx I_{D 2}$ and $V_{G S 1} \approx V_{G S 2}$. That is, $V_{\text {out }} \approx V_{\text {in }}$. This unity-gain action continues as $V_{i n}$ increases. For a sufficiently high $V_{i n}$, two phenomena occur: (a) $M_{1}$ enters the triode region if $V_{\text {in }}>V_{D D}-\left|V_{G S 3}\right|+V_{T H 1}$, and (b) $M_{4}$ enters the triode region if $V_{\text {out }}>V_{D D}-\left|V_{G S 4}-V_{T H 4}\right|$, and hence $V_{i n}>V_{D D}-\left|V_{G S 4}-V_{T H 4}\right|$. These two values are roughly equal if $V_{T H 1}$ and $\left|V_{T H 4}\right|$ are comparable. Beyond this point, $\left|I_{D 4}\right|<\left|I_{D 3}\right|$ (why?), and hence $V_{G S 1}>V_{G S 2}$, yielding $V_{\text {out }}<V_{i n}$. If $V_{i n}=V_{D D}$, then $M_{4}$ carries little current and $V_{\text {out }}$ incurs substantial error.

### 5.3.2 Small-Signal Analysis

We now analyze the small-signal properties of the circuit shown in Fig. 5.27(a), assuming $\gamma=0$ for simplicity. Can we apply the half-circuit concept to calculate the differential gain here? As illustrated in Fig. 5.31, with small differential inputs, the voltage swings at nodes $F$ and $X$ are vastly different. This is because the diode-connected device $M_{3}$ yields a much lower voltage gain from the input to node $F$ than that from the input to node $X$. As a result, the effects of $V_{F}$ and $V_{X}$ at node $P$ (through $r_{O 1}$ and $r_{O 2}$, respectively) do not cancel each other, and this node cannot be considered a virtual ground. Using the lemma $\left|A_{v}\right|=G_{m} R_{\text {out }}$, we first perform an approximate analysis so as to develop insight and then carry out an exact calculation of the gain.
image_name:Figure 5.31 Asymmetric swings in a differential pair with active current mirror
description:
[
name: M1, type: NMOS, ports: {S: P, D: F, G: Vip}
name: M2, type: NMOS, ports: {S: P, D: X, G: Vin}
name: M3, type: PMOS, ports: {S: VDD, D: F, G: F}
name: M4, type: PMOS, ports: {S: VDD, D: X, G: X}
name: ro1, type: Resistor, value: ro1, ports: {N1: F, N2: P}
name: ro2, type: Resistor, value: ro2, ports: {N1: X, N2: P}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential pair with active current mirror using PMOS and NMOS transistors. M3 and M4 form the active current mirror. The circuit is designed to handle asymmetric voltage swings at nodes F and X, with node P approximated as a virtual ground for analysis.

Figure 5.31 Asymmetric swings in a differential pair with active current mirror.

Approximate Analysis For the calculation of $G_{m}$, consider Fig. 5.32(a). The circuit is not quite symmetric, but because the impedance seen at node $F$ is relatively low and the swing at this node small, the current returning from $F$ to $P$ through $r_{O 1}$ is negligible, and node $P$ can be approximated by a virtual ground [Fig. 5.32(b)]. Thus, $I_{D 1}=\left|I_{D 3}\right|=\left|I_{D 4}\right|=g_{m 1,2} V_{i n} / 2$ and $I_{D 2}=-g_{m 1,2} V_{i n} / 2$, yielding $I_{\text {out }}=-g_{m 1,2} V_{i n}$, and hence $\left|G_{m}\right|=g_{m 1,2}$. Note that, by virtue of active current mirror operation, this value is twice the transconductance of the circuit of Fig. 5.23(b).

Calculation of $R_{\text {out }}$ is less straightforward. We may surmise that the output resistance of this circuit is equal to that of the circuit in Fig. 5.23(c), namely, $\left(2 r_{O 2}\right) \| r_{O 4}$. In reality, however, the active mirror operation yields a different value because when a voltage is applied to the output to measure $R_{\text {out }}$, the gate voltage of $M_{4}$ does not remain constant. Rather than draw the entire equivalent circuit, we observe that for small signals, $I_{S S}$ is open [Fig. 5.33(a)], any current flowing into $M_{1}$ must flow out of $M_{2}$, and the role of the two transistors can be represented by a resistor $R_{X Y}=2 r_{O 1,2}$ [Fig. 5.33(b)]. As a result, the current drawn from $V_{X}$ by $R_{X Y}$ is mirrored by $M_{3}$ onto $M_{4}$ with unity gain. This current is equal to
image_name:Figure 5.32 (a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: F, G: Vin/2}
name: M2, type: NMOS, ports: {S: P, D: GND, G: -Vin/2}
name: M3, type: PMOS, ports: {S: VDD, D: F, G: F}
name: M4, type: PMOS, ports: {S: VDD, D: GND, G: F}
name: Iss, type: CurrentSource, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is designed to calculate the transconductance Gm. It uses a differential pair of NMOS transistors (M1 and M2) with a current mirror formed by PMOS transistors (M3 and M4). The current source Iss provides a bias current, and the output current Iout is mirrored to the output node G(N).
image_name:Figure 5.32 (b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: F, G: Vin/2}
name: M2, type: NMOS, ports: {S: GND, D: GND, G: -Vin/2}
name: M3, type: PMOS, ports: {S: VDD, D: F, G: F}
name: M4, type: PMOS, ports: {S: VDD, D: GND, G: F}
]
extrainfo:The circuit is a differential amplifier with a current mirror load. M1 and M2 form the input differential pair, while M3 and M4 act as the current mirror load. The current source Iss provides the bias current. The output is taken from the node labeled GND.

Figure 5.32 (a) Circuit for calculation of $G_{m}$; (b) circuit of (a) with node $P$ grounded.
image_name:Figure 5.32 (a)
description:The circuit is a differential amplifier with a current mirror load. M1 and M2 form the input differential pair, while M3 and M4 act as the current mirror load. The current source Iss provides the bias current. The output is taken from the node labeled Vx.
image_name:Figure 5.32 (b)
description:The circuit is a differential amplifier with a current mirror load. M1 and M2 form the input differential pair, while M3 and M4 act as the current mirror load. The current source Iss provides the bias current. The output is taken from the node labeled GND.

Figure 5.33 (a) Circuit for calculating $R_{\text {out }}$; (b) substitution of a resistor for $M_{1}$ and $M_{2}$.
$V_{X} /\left[2 r_{O 1,2}+\left(1 / g_{m 3}\right) \| r_{O 3}\right]$. We multiply this current by $\left(1 / g_{m 3}\right) \| r_{O 3}$ to obtain the gate-source voltage of $M_{4}$ and then multiply the result by $g_{m 4}$. It follows that

$$
\begin{equation*}
I_{X}=\frac{V_{X}}{2 r_{O 1,2}+\frac{1}{g_{m 3}} \| r_{O 3}}\left[1+\left(\frac{1}{g_{m 3}} \| r_{O 3}\right) g_{m 4}\right]+\frac{V_{X}}{r_{O 4}} \tag{5.27}
\end{equation*}
$$

For $2 r_{O 1,2} \gg\left(1 / g_{m 3}\right) \| r_{O 3}$, we have

$$
\begin{equation*}
R_{\text {out }} \approx r_{O 2} \| r_{O 4} \tag{5.28}
\end{equation*}
$$

The overall voltage gain is approximately equal to $\left|A_{v}\right|=G_{m} R_{o u t}=g_{m 1,2}\left(r_{O 2} \| r_{O 4}\right)$, somewhat higher than that of the circuit in Fig. 5.23(a).
Exact Analysis We must compute both the $G_{m}$ and $R_{\text {out }}$ of the OTA. Let us determine the $G_{m}$, without grounding node $P$, by solving the equivalent circuit shown in Fig. 5.34. For the sake of brevity, we use the subscript 1 to denote both $M_{1}$ and $M_{2}$. Since the current flowing downward through $\left(1 / g_{m 3}\right) \| r_{O 3}$ (denoted by $r_{d}$ hereafter) is $-V_{4} / r_{d}, r_{O 1}$ sustains a voltage equal to $\left(-V_{4} / r_{d}-g_{m 1} V_{1}\right) r_{O 1}$. Adding this voltage to $V_{P}=V_{i n 1}-V_{1}$, we have

$$
\begin{equation*}
\left(-\frac{V_{4}}{r_{d}}-g_{m 1} V_{1}\right) r_{O 1}+V_{i n 1}-V_{1}=V_{4} \tag{5.29}
\end{equation*}
$$

image_name:Figure 5.34 Equivalent circuit of five-transistor OTA
description:This circuit is an equivalent model of a five-transistor operational transconductance amplifier (OTA). It includes two input voltage sources (Vin1 and Vin2), three voltage-controlled current sources (gm1V1, gm2V2, gm4V4), and four resistors (ro1, ro2, ro3, ro4). The circuit is designed to model the behavior of an OTA, with the output current Iout flowing from the node labeled as Vout.

Figure 5.34 Equivalent circuit of five-transistor OTA

We also recognize that the sum of $g_{m 2} V_{2}$ and the current flowing through $r_{O 2}$ is equal to $V_{4} / r_{d}$ (why?). That is

$$
\begin{equation*}
g_{m 2} V_{2}-\frac{V_{i n 2}-V_{2}}{r_{O 2}}=\frac{V_{4}}{r_{D}} \tag{5.30}
\end{equation*}
$$

Obtaining $V_{1}$ and $V_{2}$ from these equations in terms of $V_{4}$ and noting that $V_{1}-V_{2}=V_{i n 1}-V_{i n 2}$ and $I_{\text {out }}=g_{m 4} V_{4}+V_{4} / r_{d}$, we arrive at

$$
\begin{equation*}
I_{\text {out }}=-g_{m 1} r_{O 1} \frac{g_{m 4} r_{d}+1}{r_{d}+2 r_{O 1}}\left(V_{i n 1}-V_{i n 2}\right) \tag{5.31}
\end{equation*}
$$

It follows that

$$
\begin{equation*}
G_{m}=-g_{m 1} r_{O 1} \frac{g_{m 4} r_{d}+1}{r_{d}+2 r_{O 1}} \tag{5.32}
\end{equation*}
$$

In the next step, we calculate $R_{\text {out }}$. Let us express the output admittance from Eq. (5.27) as

$$
\begin{align*}
\frac{I_{X}}{V_{X}} & =\frac{1+g_{m 4} r_{d}}{2 r_{O 1}+r_{d}}+\frac{1}{r_{O 4}}  \tag{5.33}\\
& =\frac{\left(1+g_{m 4} r_{d}\right) r_{O 4}+2 r_{O 1}+r_{d}}{\left(2 r_{O 1}+r_{d}\right) r_{O 4}} \tag{5.34}
\end{align*}
$$

and hence

$$
\begin{equation*}
G_{m} R_{o u t}=-g_{m 1} r_{O 1} \frac{\left(g_{m 4} r_{d}+1\right) r_{O 4}}{\left(g_{m 4} r_{d}+1\right) r_{O 4}+2 r_{O 1}+r_{d}} \tag{5.35}
\end{equation*}
$$

Since $r_{d}=r_{O 3} /\left(1+g_{m 3} r_{O 3}\right)$, this expression reduces to

$$
\begin{align*}
G_{m} R_{o u t} & =-g_{m 1} r_{O 1} r_{O 4} \frac{2 g_{m 3} r_{O 3}+1}{\left(2 g_{m 3} r_{O 3}+1\right) r_{O 4}+2 r_{O 1}\left(1+g_{m 3} r_{O 3}\right)+r_{O 3}}  \tag{5.36}\\
& =-\frac{g_{m 1} r_{O 1} r_{O 4}}{r_{O 1}+r_{O 3}} \cdot \frac{2 g_{m 3} r_{O 3}+1}{2\left(g_{m 3} r_{O 3}+1\right)} \tag{5.37}
\end{align*}
$$

We thus obtain a simple but exact expression for the gain:

$$
\begin{equation*}
\left|A_{v}\right|=g_{m 1}\left(r_{O 1}| | r_{O 4}\right) \frac{2 g_{m 4} r_{O 4}+1}{2\left(g_{m 4} r_{O 4}+1\right)} \tag{5.38}
\end{equation*}
$$

We can view this result as our approximate solution, $g_{m 1}\left(r_{O 1} \| r_{O 4}\right)$, multiplied by a "correction" factor that is less than unity. For example, if $g_{m 4} r_{O 4}=5$, then $\left|A_{v}\right|=0.92 g_{m 1}\left(r_{O 1} \| r_{O 4}\right)$.

#### Example 5.11

With the aid of the above results, determine the output response to an input CM change if mismatches are neglected.

#### Solution

To represent an input CM change, we choose $V_{i n 1}=V_{i n 2}$ in Fig. 5.34, obtaining from Eq. (5.31) $I_{o u t}=0$. The single-ended output voltage is therefore free from the input CM change.

#### Example 5.12

Calculate the small-signal voltage gain of the circuit shown in Fig. 5.35. How does the performance of this circuit compare with that of a differential pair with active mirror?
image_name:Figure 5.35
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: M2, type: PMOS, ports: {S: VDD, D: Vout, G: Vb}
]
extrainfo:The circuit is a common-source amplifier with NMOS M1 and PMOS M2. M1 is driven by input voltage Vin, and M2 is used as a load. The output is taken at Vout. The circuit is biased with Vb and powered by VDD.

#### Solution

We have $A_{v}=g_{m 1}\left(r_{O 1} \| r_{O 2}\right)$, similar to the value derived above. For given device dimensions, this circuit requires half of the bias current to achieve the same gain as a differential pair. However, advantages of differential operation (less sensitivity to CM noise and less distortion) often outweigh the power penalty.

The above calculations of the gain have assumed an ideal tail current source. In reality, the output impedance of this source affects the gain, but the error is relatively small.

Headroom Issues The five-transistor OTA does not easily lend itself to low-voltage operation as the diode-connected PMOS device tends to consume a substantial voltage headroom. To arrive at a modification, we observe that the gate voltage of this device need not be equal to its drain voltage. As shown in Fig. 5.36, we insert a resistor in series with the gate and draw a constant current from it, thereby
image_name:Figure 5.36 OTA headroom improvement by level shift
description:
[
name: M1, type: NMOS, ports: {S: P, D: P, G: Vip}
name: M2, type: NMOS, ports: {S: P, D: Vout, G: Vin}
name: M3, type: PMOS, ports: {S: VDD, D: F, G: G}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: G}
name: R1, type: Resistor, value: R1, ports: {N1: F, N2: G}
name: I1, type: CurrentSource, value: I1, ports: {Np: G, Nn: GND}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a five-transistor OTA with headroom improvement by level shifting. It uses a resistor R1 to allow the gate voltage of M3 to be below the drain voltage by a certain amount, improving input CM level handling. The current source I1 is used to draw constant current, and Iss provides the tail current for the NMOS differential pair M1 and M2.

allowing $V_{G}$ to be below $V_{F}$ by $R_{1} I_{1} \leq V_{T H 3}$. With this level shift, the input CM level can be higher, easing the design of the preceding stage and the tail current source. The value of $I_{1}$ must be much less than $I_{S S} / 2$ so as to introduce negligible asymmetry between the two sides of the circuit. The reader is encouraged to compute the input-referred offset voltage arising from $I_{1}$.

### 5.3.3 Common-Mode Properties

Let us now study the common-mode properties of the differential pair with active current mirror. We assume $\gamma=0$ for simplicity and leave a more general analysis including body effect for the reader. Our objective is to predict the consequences of a finite output impedance in the tail current source. As depicted in Fig. 5.37, a change in the input CM level leads to a change in the bias current of all of the transistors. How do we define the common-mode gain here? Recall from Chapter 4 that the CM gain represents the corruption of the output signal of interest due to variations in the input CM level. In the circuits of Chapter 3, the output signal was sensed differentially, and hence the CM gain was defined in terms of the output differential component generated by the input CM change. In the circuit of Fig. 5.37, on the other hand, the output signal of interest is sensed with respect to ground. Thus, we define the CM gain in terms of the single-ended output component produced by the input CM change:

$$
\begin{equation*}
A_{C M}=\frac{\Delta V_{\text {out }}}{\Delta V_{\text {in }, C M}} \tag{5.39}
\end{equation*}
$$

image_name:Figure 5.37
description:
[
name: M1, type: NMOS, ports: {S: P, D: F, G: Vin,CM}
name: M2, type: NMOS, ports: {S: P, D: X, G: Vin,CM}
name: M3, type: PMOS, ports: {S: VDD, D: F, G: F}
name: M4, type: PMOS, ports: {S: VDD, D: X, G: F}
name: RSS, type: Resistor, value: RSS, ports: {N1: P, N2: GND}
]
extrainfo:The circuit is a differential pair with an active current mirror. The common-mode gain is defined in terms of the single-ended output component produced by the input common-mode change.

Figure 5.37 Differential pair with active current mirror sensing a common-mode change.

To determine $A_{C M}$, we observe that if the transistors are symmetric, $V_{\text {out }}=V_{F}$ for any input CM level (Section 5.3.1). For example, as $V_{i n, C M}$ increases, $V_{F}$ drops and so does $V_{\text {out }}$. In other words, nodes $F$ and $X$ can be shorted [Fig. 5.38(a)], resulting in the equivalent circuit shown in Fig. 5.38(b). Here, $M_{1}$ and $M_{2}$ appear in parallel and so do $M_{3}$ and $M_{4}$. It follows that

$$
\begin{align*}
A_{C M} & \approx \frac{-\frac{1}{2 g_{m 3,4}} \| \frac{r_{O 3,4}}{2}}{\frac{1}{2 g_{m 1,2}}+R_{S S}}  \tag{5.40}\\
& =\frac{-1}{1+2 g_{m 1,2} R_{S S}} \frac{g_{m 1,2}}{g_{m 3,4}} \tag{5.41}
\end{align*}
$$

image_name:Figure 5.38(a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: F, G: Vin,CM}
name: M2, type: NMOS, ports: {S: P, D: X, G: Vin,CM}
name: M3, type: PMOS, ports: {S: VDD, D: F, G: F}
name: M4, type: PMOS, ports: {S: VDD, D: X, G: F}
name: RSS, type: Resistor, value: RSS, ports: {N1: P, N2: GND}
]
extrainfo:The circuit is a differential amplifier with NMOS transistors M1 and M2 forming the input differential pair, and PMOS transistors M3 and M4 acting as active loads. RSS is the tail resistor providing a bias current to the differential pair.
image_name:Figure 5.38(b)
description:The circuit in figure (b) is an equivalent circuit of figure (a), showing M1 and M2 in parallel and M3 and M4 in parallel. It simplifies the analysis by focusing on the key components affecting the common-mode rejection ratio (CMRR). The resistors and transistors are arranged to form a differential amplifier with a focus on common-mode gain.

Figure 5.38 (a) Simplified circuit of Fig. 5.37; (b) equivalent circuit of (a).
where we have assumed that $1 /\left(2 g_{m 3,4}\right) \ll r_{O 3,4}$ and neglected the effect of $r_{O 1,2} / 2$. The CMRR is then given by

$$
\begin{align*}
\mathrm{CMRR} & =\left|\frac{A_{D M}}{A_{C M}}\right|  \tag{5.42}\\
& =g_{m 1,2}\left(r_{O 1,2} \| r_{O 3,4}\right) \frac{g_{m 3,4}\left(1+2 g_{m 1,2} R_{S S}\right)}{g_{m 1,2}}  \tag{5.43}\\
& =\left(1+2 g_{m 1,2} R_{S S}\right) g_{m 3,4}\left(r_{O 1,2} \| r_{O 3,4}\right) \tag{5.44}
\end{align*}
$$

For example, if $R_{S S}=r_{O}$ and $2 g_{m 1,2} r_{O} \gg 1$, then CMRR is on the order of $\left(g_{m} r_{O}\right)^{2}$.
Equation (5.41) indicates that, even with perfect symmetry, the output signal is corrupted by input CM variations. High-frequency common-mode noise therefore degrades the performance considerably as the capacitance shunting the tail current source exhibits a lower impedance.

#### Example 5.13

The CM gain of the circuit of Fig. 5.37 can be shown to be zero by a (flawed) argument. As shown in Fig. 5.39(a), if $V_{i n, C M}$ introduces a change of $\Delta I$ in the drain current of each input transistor, then $I_{D 3}$ also experiences the same change, and so does $I_{D 4}$. Thus, $M_{4}$ seemingly provides the additional current required by $M_{2}$, and the output voltage need not change, i.e., $A_{C M}=0$. Explain the flaw in this proof.

#### Solution

The assumption that $\Delta I_{D 4}$ completely cancels the effect of $\Delta I_{D 2}$ is incorrect. Consider the equivalent circuit shown in Fig. 5.39(b). Since

$$
\begin{equation*}
\Delta V_{F}=\Delta I_{1}\left(\frac{1}{g_{m 3}} \| r_{O 3}\right) \tag{5.45}
\end{equation*}
$$

we have

$$
\begin{align*}
\left|\Delta I_{D 4}\right| & =g_{m 4} \Delta V_{F}  \tag{5.46}\\
& =g_{m 4} \Delta I_{1} \frac{r_{O 3}}{1+g_{m 3} r_{O 3}} \tag{5.47}
\end{align*}
$$

image_name:Fig 5.39(a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: F, G: ΔVin,CM}
name: M2, type: NMOS, ports: {S: P, D: X, G: ΔVin,CM}
name: M3, type: PMOS, ports: {S: VDD, D: F, G: F}
name: M4, type: PMOS, ports: {S: VDD, D: X, G: F}
name: Rss, type: Resistor, value: Rss, ports: {N1: P, N2: GND}
]
extrainfo:The circuit is a differential amplifier with NMOS transistors M1 and M2 forming the input stage and PMOS transistors M3 and M4 forming the active load. The resistors ro3 and ro4 are connected to the drains of M3 and M4, respectively, and serve as load resistances. The circuit is powered by VDD and has a current source ΔI1 at node F and ΔI2 at node X. The output voltage is taken across node X.
image_name:Fig 5.39(b)
description:
[
name: M3, type: PMOS, ports: {S: VDD, D: F, G: F}
name: M4, type: PMOS, ports: {S: VDD, D: X, G: F}
name: ro3, type: Resistor, value: ro3, ports: {N1: VDD, N2: F}
name: ro4, type: Resistor, value: ro4, ports: {N1: VDD, N2: X}
name: ΔI1, type: CurrentSource, value: ΔI1, ports: {Np: F, Nn: GND}
name: ΔI2, type: CurrentSource, value: ΔI2, ports: {Np: X, Nn: GND}
]
extrainfo:The circuit in diagram (b) is a differential amplifier stage with PMOS loads (M3, M4) and NMOS inputs (M1, M2). The resistors ro3 and ro4 represent the output resistances of the PMOS transistors. The current sources ΔI1 and ΔI2 are connected to the nodes F and X, respectively. The voltage output is measured at Vout.

This current and $\Delta I_{2}\left(=\Delta I_{1}=\Delta I\right)$ give a net voltage change equal to

$$
\begin{align*}
\Delta V_{\text {out }} & =\left(\Delta I_{1} g_{m 4} \frac{r_{O 3}}{1+g_{m 3} r_{O 3}}-\Delta I_{2}\right) r_{O 4}  \tag{5.48}\\
& =-\Delta I \frac{1}{g_{m 3} r_{O 3}+1} r_{O 4} \tag{5.49}
\end{align*}
$$

which is equal to the voltage change at node $F$.

Effect of Mismatches It is also instructive to calculate the common-mode gain in the presence of mismatches. As an example, we consider the case where the input transistors exhibit slightly different transconductances [Fig. 5.40(a)]. How does $V_{\text {out }}$ depend on $V_{i n, C M}$ ? Since the change at nodes $F$ and $X$ is relatively small, we can compute the change in $I_{D 1}$ and $I_{D 2}$ while neglecting the effect of $r_{O 1}$ and $r_{O 2}$. As shown in Fig. 5.40(b), the voltage change at $P$ can be obtained by considering $M_{1}$ and $M_{2}$ as a single transistor (in a source follower configuration) with a transconductance equal to $g_{m 1}+g_{m 2}$, i.e.,

$$
\begin{equation*}
\Delta V_{P}=\Delta V_{i n, C M} \frac{R_{S S}}{R_{S S}+\frac{1}{g_{m 1}+g_{m 2}}} \tag{5.50}
\end{equation*}
$$

where body effect is neglected. The changes in the drain currents of $M_{1}$ and $M_{2}$ are therefore given by

$$
\begin{align*}
\Delta I_{D 1} & =g_{m 1}\left(\Delta V_{i n, C M}-\Delta V_{P}\right)  \tag{5.51}\\
& =\frac{\Delta V_{i n, C M}}{R_{S S}+\frac{1}{g_{m 1}+g_{m 2}}} \frac{g_{m 1}}{g_{m 1}+g_{m 2}}  \tag{5.52}\\
\Delta I_{D 2} & =g_{m 2}\left(\Delta V_{i n, C M}-\Delta V_{P}\right)  \tag{5.53}\\
& =\frac{\Delta V_{i n, C M}}{R_{S S}+\frac{1}{g_{m 1}+g_{m 2}}} \frac{g_{m 2}}{g_{m 1}+g_{m 2}} \tag{5.54}
\end{align*}
$$

image_name:Figure 5.40(a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: F, G: Vin,CM}
name: M2, type: NMOS, ports: {S: P, D: X, G: Vin,CM}
name: M3, type: PMOS, ports: {S: VDD, D: F, G: F}
name: M4, type: PMOS, ports: {S: VDD, D: X, G: F}
name: Rss, type: Resistor, value: Rss, ports: {N1: P, N2: GND}
]
extrainfo:The circuit is a differential pair with NMOS input transistors (M1 and M2) and PMOS load transistors (M3 and M4). The output is taken at node X, labeled as Vout. The resistor Rss connects the source of M1 and M2 to ground, providing a common source configuration.
image_name:Figure 5.40(b)
description:
[
name: M1, type: NMOS, ports: {S: P, D: LOAD1, G: Vin,CM}
name: M2, type: NMOS, ports: {S: P, D: LOAD2, G: Vin,CM}
name: Rss, type: Resistor, value: Rss, ports: {N1: P, N2: GND}
]
extrainfo:The circuit is a differential pair with NMOS transistors M1 and M2. Both transistors share a common source node P connected to resistor Rss, which is grounded. The gates of M1 and M2 are connected to the input node Vin,CM. The drains are connected to LOAD1 and LOAD2, respectively.

Figure 5.40 Differential pair with $g_{m}$ mismatch.

The change $\Delta I_{D 1}$ multiplied by $\left(1 / g_{m 3}\right) \| r_{O 3}$ yields $\left|\Delta I_{D 4}\right|=g_{m 4}\left[\left(1 / g_{m 3}\right) \| r_{O 3}\right] \Delta I_{D 1}$. The difference between this current and $\Delta I_{D 2}$ flows through the output impedance of the circuit, which is equal to $r_{O 4}$ because we have neglected the effect of $r_{O 1}$ and $r_{O 2}$ :

$$
\begin{align*}
\Delta V_{\text {out }} & =\left[\frac{g_{m 1} \Delta V_{\text {in,CM }}}{1+\left(g_{m 1}+g_{m 2}\right) R_{S S}} \frac{r_{O 3}}{r_{O 3}+\frac{1}{g_{m 3}}}-\frac{g_{m 2} \Delta V_{i n, C M}}{1+\left(g_{m 1}+g_{m 2}\right) R_{S S}}\right] r_{O 4}  \tag{5.55}\\
& =\frac{\Delta V_{i n, C M}}{1+\left(g_{m 1}+g_{m 2}\right) R_{S S}} \frac{\left(g_{m 1}-g_{m 2}\right) r_{O 3}-g_{m 2} / g_{m 3}}{r_{O 3}+\frac{1}{g_{m 3}}} r_{O 4} \tag{5.56}
\end{align*}
$$

If $r_{O 3} \gg 1 / g_{m 3}$, we have

$$
\begin{equation*}
\frac{\Delta V_{\text {out }}}{\Delta V_{\text {in }, C M}} \approx \frac{\left(g_{m 1}-g_{m 2}\right) r_{O 3}-g_{m 2} / g_{m 3}}{1+\left(g_{m 1}+g_{m 2}\right) R_{S S}} \tag{5.57}
\end{equation*}
$$

Compared to Eq. (5.41), this result contains the additional term $\left(g_{m 1}-g_{m 2}\right) r_{O 3}$ in the numerator, revealing the effect of transconductance mismatch on the common-mode gain.
