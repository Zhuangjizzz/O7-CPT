# Cascode Stages and Current Mirrors

Following our study of basic bipolar and MOS amplifiers in previous chapters, we deal with two other important building blocks in this chapter. The "cascode" stage is a modified version of common-emitter or common-source topologies and proves useful in high-performance circuit design, and the "current mirror" is an interesting and versatile technique employed extensively in integrated circuits. Our study includes both bipolar and MOS implementations of each building block. Shown below is the outline of the chapter.

Cascode Stages

- Cascode as Current Source
- Cascode as Amplifier

Current Mirrors

- Bipolar Mirrors
- MOS Mirrors

## 9.1 CASCODE STAGE

### 9.1.1 Cascode as a Current Source

Recall from Chapters 5 and 7 that the use of current-source loads can markedly increase the voltage gain of amplifiers. We also know that a single transistor can operate as a current source but its output impedance is limited due to the Early effect (in bipolar devices) or channel-length modulation (in MOSFETs).

How can we increase the output impedance of a transistor that acts as a current source? An important observation made in Chapters 5 and 7 forms the foundation for our

[^3]image_name:R_{out1}
description:
[
name: Q1, type: NPN, ports: {C: Rout1, B: Vb, E: GND}
name: RE, type: Resistor, value: RE, ports: {N1: E, N2: GND}
]
extrainfo:The circuit shows two configurations for increasing output impedance using emitter degeneration for the NPN transistor and source degeneration for the NMOS transistor.
image_name:R_{out2}
description:
[
name: M1, type: NMOS, ports: {S: c1, D: Rout2, G: Vb}
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: c1}
]
extrainfo:The circuit diagram represents a current source with an NMOS transistor M1 and resistor RS to increase output impedance. Capacitor CI is connected between the output and bias voltage Vb for stabilization.

Figure 9.1 Output impedance of degenerated bipolar and MOS devices.
study here: emitter or source degeneration "boosts" the impedance seen looking into the collector or drain, respectively. For the circuits shown in Fig. 9.1, we have

$$
\begin{align*}
R_{\text {out } 1} & =\left[1+g_{m}\left(R_{E} \| r_{\pi}\right)\right] r_{O}+R_{E} \| r_{\pi}  \tag{9.1}\\
& =\left(1+g_{m} r_{O}\right)\left(R_{E} \| r_{\pi}\right)+r_{O}  \tag{9.2}\\
R_{\text {out } 2} & =\left(1+g_{m} R_{S}\right) r_{O}+R_{S}  \tag{9.3}\\
& =\left(1+g_{m} r_{O}\right) R_{S}+r_{O} \tag{9.4}
\end{align*}
$$

observing that $R_{E}$ or $R_{S}$ can be increased to raise the output resistance. Unfortunately, however, the voltage drop across the degeneration resistor also increases proportionally, consuming voltage headroom and ultimately limiting the voltage swings provided by the circuit using such a current source. For example, if $R_{E}$ sustains 300 mV and $Q_{1}$ requires a minimum collector-emitter voltage of 500 mV , then the degenerated current source "consumes" a headroom of 800 mV .

Bipolar Cascode In order to relax the trade-off between the output impedance and the voltage headroom, we can replace the degeneration resistor with a transistor. Depicted in Fig. 9.2(a) for the bipolar version, the idea is to introduce a high small-signal resistance $\left(=r_{O 2}\right)$ in the emitter of $Q_{1}$ while consuming a headroom independent of the current. In this case, $Q_{2}$ requires a headroom of approximately 0.4 V to remain in soft saturation. This configuration is called the "cascode" stage. ${ }^{2}$ To emphasize that $Q_{1}$ and $Q_{2}$ play distinctly different roles here, we call $Q_{1}$ the cascode transistor and $Q_{2}$ the degeneration transistor. Note that $I_{C 1} \approx I_{C 2}$ if $\beta_{1} \gg 1$.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: Cl, B: Vb1, E: e1c2}
name: Q2, type: NPN, ports: {C: e1c2, B: Vb2, E: GND}
]
extrainfo:This is a cascode bipolar current source consisting of two NPN transistors (Q1 and Q2). Q1 is the cascode transistor, and Q2 is the degeneration transistor. The configuration aims to increase output impedance by using Q2 as a small-signal resistance.

(a)
image_name:Figure 9.2 (b)
description:
[
name: Q1, type: NPN, ports: {C: Cl, B: Vb, E: e1}
name: rO2, type: Resistor, value: rO2, ports: {N1: e1, N2: GND}
]
extrainfo:This circuit is a cascode bipolar current source. Q1 is the cascode transistor, and it is configured to increase output impedance. The capacitor Cl and resistor Rout are connected to the collector of Q1. The resistor rO2 is connected to the emitter of Q1 and ground.

(b)

Figure 9.2 (a) Cascode bipolar current source, (b) equivalent circuit.

Let us compute the output impedance of the bipolar cascode of Fig. 9.2(a). Since the base-emitter voltage of $Q_{2}$ is constant, this transistor simply operates as a small-signal resistance equal to $r_{O 2}$ [Fig. 9.2(b)]. In analogy with the resistively-degenerated counterpart
${ }^{2}$ Or simply the "cascode."
in Fig. 9.1, we have

$$
\begin{equation*}
R_{\text {out }}=\left[1+g_{m 1}\left(r_{O 2} \| r_{\pi 1}\right)\right] r_{O 1}+r_{O 2} \| r_{\pi 1} \tag{9.5}
\end{equation*}
$$

Since typically $g_{m 1}\left(r_{O 2} \| r_{\pi 1}\right) \gg 1$,

$$
\begin{align*}
R_{\text {out }} & \approx\left(1+g_{m 1} r_{O 1}\right)\left(r_{O 2} \| r_{\pi 1}\right)  \tag{9.6}\\
& \approx g_{m 1} r_{O 1}\left(r_{O 2} \| r_{\pi 1}\right) . \tag{9.7}
\end{align*}
$$

Note, however, that $r_{O}$ cannot generally be assumed much greater than $r_{\pi}$.
image_name:Example 9.1
description:The image is a simple label or title that reads "Example 9.1". It is displayed against a blue background, indicating that it is likely a reference to a specific example or section within a textbook or academic material. There are no additional diagrams or figures included in the image itself.

If $Q_{1}$ and $Q_{2}$ in Fig. 9.2(a) are biased at a collector current of 1 mA , determine the output resistance. Assume $\beta=100$ and $V_{A}=5 \mathrm{~V}$ for both transistors.

Solution Since $Q_{1}$ and $Q_{2}$ are identical and biased at the same current level, Eq. (9.7) can be simplified by noting that $g_{m}=I_{C} / V_{T}, r_{O}=V_{A} / I_{C}$, and $r_{\pi}=\beta V_{T} / I_{C}$ :

$$
\begin{align*}
R_{\text {out }} & \approx \frac{I_{C 1}}{V_{T}} \cdot \frac{V_{A 1}}{I_{C 1}} \cdot \frac{\frac{V_{A 2}}{I_{C 2}} \cdot \frac{\beta V_{T}}{I_{C 1}}}{\frac{V_{A 2}}{I_{C 2}}+\frac{\beta V_{T}}{I_{C 1}}}  \tag{9.8}\\
& \approx \frac{1}{I_{C 1}} \cdot \frac{V_{A}}{V_{T}} \cdot \frac{\beta V_{A} V_{T}}{V_{A}+\beta V_{T}}, \tag{9.9}
\end{align*}
$$

where $I_{C}=I_{C 1}=I_{C 2}$ and $V_{A}=V_{A 1}=V_{A 2}$. At room temperature, $V_{T} \approx 26 \mathrm{mV}$ and hence

$$
\begin{equation*}
R_{\text {out }} \approx 328.9 \mathrm{k} \Omega . \tag{9.10}
\end{equation*}
$$

By comparison, the output resistance of $Q_{1}$ with no degeneration would be equal to $r_{O 1}=5 \mathrm{k} \Omega$; i.e., "cascoding" has boosted $R_{\text {out }}$ by a factor of 66 here. Note that $r_{O 2}$ and $r_{\pi 1}$ are comparable in this example.

Exercise What Early voltage is required for an output resistance of $500 \mathrm{k} \Omega$ ?

It is interesting to note that if $r_{O 2}$ becomes much greater than $r_{\pi 1}$, then $R_{\text {out } 1}$ approaches

$$
\begin{align*}
R_{\text {out }, \text { max }} & \approx g_{m 1} r_{O 1} r_{\pi 1}  \tag{9.11}\\
& \approx \beta_{1} r_{O 1} . \tag{9.12}
\end{align*}
$$

This is the maximum output impedance provided by a bipolar cascode. After all, even with $r_{O 2}=\infty$ (Fig. 9.3) [or $R_{E}=\infty$ in Eq. (9.1)], $r_{\pi 1}$ still appears from the emitter of $Q_{1}$ to ac ground, thereby limiting $R_{\text {out }}$ to $\beta_{1} r_{O 1}$.

Example Suppose in Example 9.1, the Early voltage of $Q_{2}$ is equal to $50 \mathrm{~V} .{ }^{3}$ Compare the resulting output impedance of the cascode with the upper bound given by Eq. (9.12).

[^4]image_name:Figure 9.3
description:
[
name: Q1, type: NPN, ports: {C: C1, B: GND, E: e1}
name: rπ1, type: Resistor, value: rπ1, ports: {N1: GND, N2: e1}
name: I1, type: CurrentSource, value: Ideal, ports: {Np: e1, Nn: GND}
]
extrainfo:This circuit is a bipolar cascode configuration using an NPN transistor Q1. It includes a resistor rπ1, a capacitor C1, and an ideal current source. The output is taken across Rout.

Figure 9.3 Cascode topology using an ideal current source.

Solution Since $g_{m 1}=(26 \Omega)^{-1}, r_{\pi 1}=2.6 \mathrm{k} \Omega, r_{O 1}=5 \mathrm{k} \Omega$, and $r_{O 2}=50 \mathrm{k} \Omega$, we have

$$
\begin{align*}
R_{\text {out }} & \approx g_{m 1} r_{O 1}\left(r_{O 2} \| r_{\pi 1}\right)  \tag{9.13}\\
& \approx 475 \mathrm{k} \Omega . \tag{9.14}
\end{align*}
$$

The upper bound is equal to $500 \mathrm{k} \Omega$, about $5 \%$ higher.
Exercise Repeat the above example if the Early voltage of $Q_{1}$ is 10 V .

Example We wish to increase the output resistance of the bipolar cascode of Fig. 9.2(a) by a factor of two through the use of resistive degeneration in the emitter of $Q_{2}$. Determine the required value of the degeneration resistor if $Q_{1}$ and $Q_{2}$ are identical.

Solution As illustrated in Fig. 9.4, we replace $Q_{2}$ and $R_{E}$ with their equivalent resistance from Eq. (9.1):

$$
\begin{equation*}
R_{\text {out } A}=\left[1+g_{m 2}\left(R_{E} \| r_{\pi 2}\right)\right] r_{O 2}+R_{E} \| r_{\pi 2} \tag{9.15}
\end{equation*}
$$

It follows from Eq. (9.7) that

$$
\begin{equation*}
R_{\text {out }} \approx g_{m 1} r_{O 1}\left(R_{\text {out } A} \| r_{\pi 1}\right) \tag{9.16}
\end{equation*}
$$

We wish this value to be twice that given by Eq. (9.7):

$$
\begin{equation*}
R_{\text {outA }} \| r_{\pi 1}=2\left(r_{O 2} \| r_{\pi 1}\right) \tag{9.17}
\end{equation*}
$$

image_name:Figure 9.4
description:
[
name: Q1, type: NPN, ports: {C: Cl, B: Vb1, E: e1c2}
name: Q2, type: NPN, ports: {C: e1c2, B: Vb2, E: e2}
name: RE, type: Resistor, value: RE, ports: {N1: e2, N2: GND}
name: Rout, type: Resistor, value: Rout, ports: {N1: e1, N2: GND}
name: Q1, type: NPN, ports: {C: c1, B: Vb, E: e1}
]
extrainfo:The circuit depicted is a cascode amplifier with emitter degeneration. Q1 and Q2 are NPN transistors forming the cascode configuration. The circuit aims to explore the effect of emitter degeneration on output impedance. The analysis shows that doubling the output impedance of the cascode by emitter degeneration is not feasible, as demonstrated by the equations provided.

Figure 9.4

That is,

$$
\begin{equation*}
R_{o u t A}=\frac{2 r_{O 2} r_{\pi 1}}{r_{\pi 1}-r_{O 2}} \tag{9.18}
\end{equation*}
$$

In practice, $r_{\pi 1}$ is typically less than $r_{O 2}$, and no positive value of $R_{\text {outA }}$ exists! In other words, it is impossible to double the output impedance of the cascode by emitter degeneration.

What does the above result mean? Comparing the output resistances obtained in Examples 9.1 and 9.2 , we recognize that even identical transistors yield an $R_{\text {out }}$ $(=328.9 \mathrm{k} \Omega)$ that is not far from the upper bound $(=500 \mathrm{k} \Omega)$. More specifically, the ratio of (9.7) and (9.12) is equal to $r_{O 2} /\left(r_{O 2}+r_{\pi 1}\right)$, a value greater than 0.5 if $r_{O 2}>r_{\pi 1}$.

For completeness, Fig. 9.5 shows a pnp cascode, where $Q_{1}$ serves as the cascode device and $Q_{2}$ as the degeneration device. The output impedance is given by Eq. (9.5).
image_name:Figure 9.5 PNP cascode current source
description:
[
name: Q1, type: PNP, ports: {C: c1, B: Vb1, E: e1c2}
name: Q2, type: PNP, ports: {C: e1c2, B: Vb2, E: Vcc}
]
extrainfo:The circuit is a PNP cascode current source with Q1 as the cascode device and Q2 as the degeneration device. The output is taken from the node labeled c1, and the circuit is biased with Vb1 and Vb2.

While we have arrived at the cascode as an extreme case of emitter degeneration, it is also possible to view the evolution as illustrated in Fig. 9.6. That is, since $Q_{2}$ provides only an output impedance of $r_{O 2}$, we "stack" $Q_{1}$ on top of it to raise $R_{\text {out }}$.

Figure 9.6 Evolution of cascode topology viewed as stacking $Q_{1}$ atop $Q_{2}$.

Example Explain why the topologies depicted in Fig. 9.7 are not cascodes.
9.4
image_name:Figure 9.6
description:
[
name: Q2, type: NPN, ports: {C: C2, B: Vb2, E: GND}
name: Q1, type: NPN, ports: {C: Vout, B: Vb1, E: e1c2}
name: Q2, type: PNP, ports: {C: e1c2, B: Vb2, E: GND}
]
extrainfo:This circuit is a cascode current source with Q1 as the cascode device and Q2 as the degeneration device. The output is taken from node C1, and the circuit is biased with Vb1 and Vb2. The output impedance is approximately g_m1 * r_o1 * (r_o2 || r_pi1).
image_name:Figure 9.7
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: Vb1, E: x}
name: Q2, type: PNP, ports: {C: GND, B: Vb2, E: X}
name: 1/gm2 || ro2, type: Resistor, value: 1/gm2 || ro2, ports: {N1: GND, N2: e1}
name: Q1, type: NPN, ports: {C: Vout, B: Vb1, E: e1}
]
extrainfo:This is a cascode current source circuit with transistors Q1 (NPN) and Q2 (PNP). Q1 is the cascode device, and Q2 is diode-connected, presenting an impedance of (1/gm2 || ro2) at node X. The circuit is biased with Vb1 and Vb2, and the output is taken from node C1. The output impedance is approximately g_m1 * r_o1 * (r_o2 || r_pi1). The diagram shows the equivalent impedance at the emitter of Q1.
image_name:(b)
description:
[
name: Q2, type: NPN, ports: {C: Vcc, B: Vb1, E: X}
name: Q1, type: PNP, ports: {C: Vout, B: Vb2, E: x}
name: 1/gm2 || ro2, type: Resistor, value: 1/gm2 || ro2, ports: {N1: Vcc, N2: e1}
name: Q1, type: PNP, ports: {C: Vout, B: Vb2, E: e1}
]
extrainfo:This diagram illustrates a cascode current source with transistors Q1 and Q2. Q1 serves as the cascode device, and Q2 as the degeneration device. The output is taken from node C1, and the circuit is biased with Vb1 and Vb2. The output impedance is approximately g_m1 * r_o1 * (r_o2 || r_pi1). The right side of the diagram shows the equivalent impedance seen at the emitter of Q1. Transistor Q2 is diode-connected, presenting an impedance of (1/gm2) || ro2 at node X.

Solution Unlike the cascode of Fig. 9.2(a), the circuits of Fig. 9.7 connect the emitter of $Q_{1}$ to the emitter of $Q_{2}$. Transistor $Q_{2}$ now operates as a diode-connected device (rather than a current source), thereby presenting an impedance of $\left(1 / g_{m 2}\right) \| r_{O 2}\left(\right.$ rather than $\left.r_{O 2}\right)$ at node $X$. Given by Eq. (9.1), the output impedance, $R_{\text {out }}$, is therefore considerably lower:

$$
\begin{equation*}
R_{\text {out }}=\left[1+g_{m 1}\left(\frac{1}{g_{m 2}}\left\|r_{O 2}\right\| r_{\pi 1}\right)\right] r_{O 1}+\frac{1}{g_{m 2}}\left\|r_{O 2}\right\| r_{\pi 1} \tag{9.19}
\end{equation*}
$$

In fact, since $1 / g_{m 2} \ll r_{O 2}, r_{\pi 1}$ and since $g_{m 1} \approx g_{m 2}$ (why?),

$$
\begin{align*}
R_{\text {out }} & \approx\left(1+\frac{g_{m 1}}{g_{m 2}}\right) r_{O 1}+\frac{1}{g_{m 2}}  \tag{9.20}\\
& \approx 2 r_{O 1} . \tag{9.21}
\end{align*}
$$

The same observations apply to the topology of Fig. 9.7(b).
Exercise Estimate the output impedance for a collector bias current of 1 mA and $V_{A}=8 \mathrm{~V}$.

MOS Cascodes The similarity of Eqs. (9.1) and (9.3) for degenerated stages suggests that cascoding can also be realized with MOSFETs so as to increase the output impedance of a current source. Illustrated in Fig. 9.8, the idea is to replace the degeneration resistor with a MOS current source, thus presenting a small-signal resistance of $r_{O 2}$ from $X$ to ground. Equation (9.3) can now be written as

$$
\begin{align*}
R_{\text {out }} & =\left(1+g_{m 1} r_{O 2}\right) r_{O 1}+r_{O 2}  \tag{9.22}\\
& \approx g_{m 1} r_{O 1} r_{O 2}, \tag{9.23}
\end{align*}
$$

where it is assumed $g_{m 1} r_{O 1} r_{O 2} \gg r_{O 1}, r_{O 2}$.
image_name:Figure 9.8
description:
[
name: M1, type: NMOS, ports: {S: X, D: d1, G: Vb1}
name: M2, type: NMOS, ports: {S: GND, D: X, G: Vb2}
name: M1, type: NMOS, ports: {S: s1, D: d1, G: Vb}
name: rO2, type: Resistor, value: rO2, ports: {N1: s1, N2: GND}
]
extrainfo:The circuit is a MOS cascode current source designed to increase output impedance. It uses two NMOS transistors and a resistor to achieve high output impedance by replacing the degeneration resistor with a MOS current source.

Figure 9.8 MOS cascode current source and its equivalent.

Equation (9.23) is an extremely important result, implying that the output impedance is proportional to the intrinsic gain of the cascode device.

| Example | Design an NMOS cascode for an output impedance <br> 9.5 |
| :---: | :--- |
| 0.5 mA . For simplicity, assume $M_{1}$ and $M_{2}$ in Fig. 9.8 a |  |
|  | Assume $\mu_{n} C_{o x}=100 \mu \mathrm{~A} / \mathrm{V}^{2}$ and $\lambda=0.1 \mathrm{~V}^{-1}$. |

Since $r_{O 1}=r_{O 2}=\left(\lambda I_{D}\right)^{-1}=20 \mathrm{k} \Omega$, we require that $g_{m 1}=(800 \Omega)^{-1}$ and hence

$$
\begin{equation*}
\sqrt{2 \mu_{n} C_{o x} \frac{W}{L} I_{D}}=\frac{1}{800 \Omega} . \tag{9.25}
\end{equation*}
$$

It follows that

$$
\begin{equation*}
\frac{W}{L}=15.6 . \tag{9.26}
\end{equation*}
$$

We should also note that $g_{m 1} r_{O 1}=25 \gg 1$.
Exercise What is the output resistance if $W / L=32$ ?

Invoking the alternative view depicted in Fig. 9.6 for the MOS counterpart (Fig. 9.9), we recognize that stacking a MOSFET on top of a current source "boosts" the impedance by a factor of $g_{m 2} r_{O 2}$ (the intrinsic gain of the cascode transistor). This observation reveals an interesting point of contrast between bipolar and MOS cascodes: in the former, raising $r_{O 2}$ eventually leads to $R_{\text {out }, b i p}=\beta r_{O 1}$, whereas in the latter, $R_{\text {out }, M O S}=g_{{ }_{m 1}} r_{O 1} r_{O 2}$ increases with no bound. ${ }^{4}$ This is because in MOS devices, $\beta$ and $r_{\pi}$ are infinite (at low frequencies).
image_name:Figure 9.9 MOS cascode viewed as stack of M1 atop M2
description:
[
name: M1, type: NMOS, ports: {S: X, D: d1, G: Vb1}
name: M2, type: NMOS, ports: {S: GND, D: X, G: Vb2}
name: M2, type: NMOS, ports: {S: GND, D: vout, G: Vb2}
]
extrainfo:The circuit is a MOS cascode configuration with two NMOS transistors, M1 and M2. The output resistance is approximately g_m1 * r_o1 * r_o2.

Figure 9.9 MOS cascode viewed as stack of $M_{1}$ atop $M_{2}$.
Figure 9.10 illustrates a PMOS cascode. The output resistance is given by Eq. (9.22).
image_name:Figure 9.10 PMOS cascode
description:
[
name: M1, type: PMOS, ports: {S: X, D: Rout, G: Vb1}
name: M2, type: PMOS, ports: {S: VDD, D: X, G: Vb2}
]
extrainfo:The circuit is a MOS cascode configuration using NMOS transistors M1 and M2. The output resistance is approximately g_m1 * r_o1 * r_o2.

Figure 9.10 PMOS cascode current source.

[^5]Example During manufacturing, a large parasitic resistor, $R_{P}$, has appeared in a cascode as shown
9.6 in Fig. 9.11. Determine the output resistance.
image_name:Figure 9.11
description:
[
name: M1, type: NMOS, ports: {S: X, D: d1, G: Vb1}
name: M2, type: NMOS, ports: {S: GND, D: X, G: Vb2}
name: RP, type: Resistor, value: RP, ports: {N1: X, N2: d1}
]
extrainfo:The circuit is a MOS cascode configuration using NMOS transistors M1 and M2 with a parasitic resistor RP in parallel with the output resistance. The output resistance is calculated as g_m1 * (r_o1 || RP) * r_o2.

Figure 9.11
Solution We observe that $R_{P}$ is in parallel with $r_{O 1}$. It is therefore possible to rewrite Eq. (9.23) as

$$
\begin{equation*}
R_{\text {out }}=g_{m 1}\left(r_{O 1} \| R_{P}\right) r_{O 2} \tag{9.27}
\end{equation*}
$$

If $g_{m 1}\left(r_{O 1} \| R_{P}\right)$ is not much greater than unity, we return to the original equation, (9.22), substituting $r_{O 1} \| R_{P}$ for $r_{O 1}$ :

$$
\begin{equation*}
R_{\text {out }}=\left(1+g_{m 1} r_{O 2}\right)\left(r_{O 1} \| R_{P}\right)+r_{O 2} \tag{9.28}
\end{equation*}
$$

Exercise What value of $R_{P}$ degrades the output impedance by a factor of two?

Did you know?

The cascode can be viewed as a two-transistor circuit, i.e., as a CE/CB cascade. An interesting question is, how many meaningful two-transistor circuit topologies can we realize? Shown below are some: which ones look familiar? Can you think of any others? How about npn-pnp combinations?
image_name:Various two-transistor circuits
description:The diagram shows various two-transistor circuit topologies, each consisting of an NPN and a PNP transistor. These configurations are commonly used in amplifier and switching applications. The circuits demonstrate different connections of the transistors, illustrating various ways to achieve amplification and switching functions.

Various two-transistor circuits.

### 9.1.2 Cascode as an Amplifier

In addition to providing a high output impedance as a current source, the cascode topology can also serve as a high-gain amplifier. In fact, the output impedance and the gain of amplifiers are closely related.

For our study below, we need to understand the concept of the transconductance for circuits. In Chapters 4 and 6, we defined the transconductance of a transistor as the change in the collector or drain current divided by the change in the base-emitter or gate-source voltage. This concept can be generalized to circuits as well. As illustrated in Fig. 9.12, the output voltage is set to zero by shorting the output node to ground, and the "shortcircuit transconductance" of the circuit is defined as

$$
\begin{equation*}
G_{m}=\left.\frac{i_{\text {out }}}{v_{\text {in }}}\right|_{v o u t=0} \tag{9.29}
\end{equation*}
$$

The transconductance signifies the "strength" of a circuit in converting the input voltage to a current. ${ }^{5}$ Note the direction of $i_{\text {out }}$ in Fig. 9.12.

[^6]image_name:Figure 9.12
description:The circuit diagram illustrates the computation of transconductance by shorting the output to ground. The output current i_out is directed towards the ground.

Figure 9.12 Computation of transconductance for a circuit.

Example Calculate the transconductance of the CS stage shown in Fig. 9.13(a).
9.7
image_name:Figure 9.13
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit diagram is a common-source (CS) amplifier configuration using an NMOS transistor (M1). The output current i_out is directed towards the ground. The resistor RD is connected between the drain of M1 and VDD. The input voltage source Vin is connected to the gate of M1. The source of M1 is connected to ground.

image_name:(b)
description:
[
name: RD, type: Resistor, ports: {N1: VDD, N2: D}
name: M1, type: NMOS, ports: {S: GND, D: D, G: Vin}
]
extrainfo:The circuit is a common-source amplifier using an NMOS transistor (M1). The resistor RD is connected between VDD and the drain of M1. The input voltage source Vin is connected to the gate of M1, and the source of M1 is connected to ground. The output current i_out is directed towards the ground through a diode.

(b)

Figure 9.13

Solution As depicted in Fig. 9.13(b), we short the output node to ac ground and, noting that $R_{D}$ carries no current (why?), write

$$
\begin{align*}
G_{m} & =\frac{i_{\text {out }}}{v_{\text {in }}}  \tag{9.30}\\
& =\frac{i_{D 1}}{v_{G S 1}}  \tag{9.31}\\
& =g_{m 1} \tag{9.32}
\end{align*}
$$

Thus, in this case, the transconductance of the circuit is equal to that of the transistor.

Exercise How does $G_{m}$ change if the width and bias current of the transistor are doubled?

Lemma The voltage gain of a linear circuit can be expressed as

$$
\begin{equation*}
A_{v}=-G_{m} R_{\text {out }} \tag{9.33}
\end{equation*}
$$

where $R_{\text {out }}$ denotes the output resistance of the circuit (with the input voltage set to zero).
Proof We know that a linear circuit can be replaced with its Norton equivalent [Fig. 9.14(a)]. Norton's theorem states that $i_{\text {out }}$ is obtained by shorting the output to ground $\left(v_{\text {out }}=0\right)$ and computing the short-circuit current [Fig. 9.14(b)]. We also relate $i_{\text {out }}$ to $v_{\text {in }}$ by the transconductance of the circuit, $G_{m}=i_{\text {out }} / v_{\text {in }}$. Thus, in Fig. 9.14(a),

$$
\begin{align*}
v_{\text {out }} & =-i_{\text {out }} R_{\text {out }}  \tag{9.34}\\
& =-G_{m} v_{\text {in }} R_{\text {out }} \tag{9.35}
\end{align*}
$$

image_name:Figure 9.14 (a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Ao, type: OpAmp, value: Ao, ports: {InP: Vin, InN: GND, OutP: Vout, OutN: GND}
name: iout, type: CurrentSource, value: iout, ports: {Np: Vout, Nn: GND}
]
extrainfo:The diagram shows a Norton equivalent circuit transformation. The left side is an op-amp circuit with a voltage input Vin and voltage output Vout. The right side is the Norton equivalent with a current source iout and resistor Rout connected to ground.

image_name:(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: A0, type: OpAmp, value: A0, ports: {InP: Vin, InN: GND, OutP: Vout, OutN: GND}
]
extrainfo:The circuit diagram shows a Norton equivalent circuit transformation. The left side is an op-amp circuit with a voltage input Vin and voltage output Vout. The right side is the Norton equivalent with a current source iout connected to ground.

(b)

Figure 9.14 (a) Norton equivalent of a circuit, (b) computation of short-circuit output current.
and hence

$$
\begin{equation*}
\frac{v_{\text {out }}}{v_{\text {in }}}=-G_{m} R_{\text {out }} \tag{9.36}
\end{equation*}
$$

Example
Determine the voltage gain of the common-emitter stage shown in Fig. 9.15(a).
image_name:(a)
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vcc, Nn: Vout}
]
extrainfo:This circuit is a common-emitter amplifier stage with an NMOS transistor Q1. The input voltage Vin controls the transistor, and the output is taken from Vout. The current source I1 provides the necessary biasing current. The circuit is powered by Vcc and grounded at GND.

(a)
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: GND, B: Vin, E: GND}
]
extrainfo:This circuit is a simplified representation showing the short-circuit transconductance measurement setup for an NPN transistor. The output current iout is equal to the collector current of Q1, which is gm1 * Vin when the output is shorted to ground.

(b)
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: Vx, B: GND, E: GND}
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Vx, Nn: GND}
]
extrainfo:The circuit is a simple NPN transistor setup with the collector connected to node ix, base and emitter to GND. A voltage source Vx is connected between node ix and GND.

(c)

Figure 9.15

Solution
To calculate the short-circuit transconductance of the circuit, we place an ac short from the output to ground and find the current through it [Fig. 9.15(b)]. In this case, $i_{\text {out }}$ is simply equal to the collector current of $Q_{1}, g_{m 1} v_{i n}$, i.e.,

$$
\begin{align*}
G_{m} & =\frac{i_{\text {out }}}{v_{\text {in }}}  \tag{9.37}\\
& =g_{m 1} \tag{9.38}
\end{align*}
$$

Note that $r_{O}$ does not carry a current in this test (why?). Next, we obtain the output resistance as depicted in Fig. 9.15(c):

$$
\begin{align*}
R_{\text {out }} & =\frac{v_{X}}{i_{X}}  \tag{9.39}\\
& =r_{O 1} \tag{9.40}
\end{align*}
$$

It follows that

$$
\begin{align*}
A_{v} & =-G_{m} R_{\text {out }}  \tag{9.41}\\
& =-g_{m 1} r_{O 1} . \tag{9.42}
\end{align*}
$$

Suppose the transistor is degenerated by an emitter resistor equal to $R_{E}$. The transconductance falls but the ouput resistance rises. Does the voltage gain increase or decrease?

The above lemma serves as an alternative method of gain calculation. It also indicates that the voltage gain of a circuit can be increased by raising the output impedance, as in cascodes.

Bipolar Cascode Amplifier Recall from Chapter 4 that to maximize the voltage gain of a common-emitter stage, the collector load impedance must be maximized. In the limit, an ideal current source serving as the load [Fig. 9.16(a)] yields a voltage gain of

$$
\begin{align*}
A_{v} & =-g_{m 1} r_{O 1}  \tag{9.43}\\
& =-\frac{V_{A}}{V_{T}} \tag{9.44}
\end{align*}
$$

In this case, the small-signal current, $g_{m 1} v_{i n}$, produced by $Q_{1}$ flows through $r_{O 1}$, thus generating an output voltage equal to $-g_{m 1} v_{i n} r_{O 1}$.

Now, suppose we stack a transistor on top of $Q_{1}$ as shown in Fig. 9.16(b). We know from Section 9.1.1 that the circuit achieves a high output impedance and, from the above lemma, a voltage gain higher than that of a CE stage.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: Vin, E: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vcc, Nn: Vout}
name: rO1, type: Resistor, value: rO1, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a common-emitter amplifier with a current source I1 providing biasing. The output is taken across the resistor rO1.

(a)
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: C1E2, B: Vin, E: GND}
name: Q2, type: NPN, ports: {C: Vout, B: Vb1, E: C1E2}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vcc, Nn: Vout}
]
extrainfo:The circuit is a cascode amplifier with a current source I1 providing biasing. The output is taken from the collector of Q2, and the cascode configuration increases the output impedance.

(b)

Figure 9.16 (a) Flow of output current generated by a CE stage through $r_{O 1}$, (b) use of cascode to increase the output impedance.

Let us determine the voltage gain of the bipolar cascode with the aid of the above lemma. As shown in Fig. 9.17(a), the short-circuit transconductance is equal to $i_{\text {out }} / v_{\text {in }}$. As a common-emitter stage, $Q_{1}$ still produces a collector current of $g_{m 1} v_{i n}$, which subsequently flows through $Q_{2}$ and hence through the output short:

$$
\begin{equation*}
i_{\text {out }}=g_{m 1} v_{i n} \tag{9.45}
\end{equation*}
$$

That is,

$$
\begin{equation*}
G_{m}=g_{m 1} \tag{9.46}
\end{equation*}
$$

image_name:(a)
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: C1E2, G: Vin}
name: Q2, type: NMOS, ports: {S: C1E2, D: Iout, G: GND}
]
extrainfo:The circuit is a bipolar cascode configuration with transistor Q1 acting as a common-emitter stage, providing a collector current of gm1*Vin. The current flows through Q2, which is configured as a diode-connected transistor, to the output. The diagram illustrates the short-circuit output current of the cascode amplifier.
image_name:(b)
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: X, G: Vin}
name: Q2, type: NMOS, ports: {S: X, D: GND, G: GND}
name: rO2, type: Resistor, value: rO2, ports: {N1: GND, N2: X}
name: rO1, type: Resistor, value: rO1, ports: {N1: X, N2: GND}
]
extrainfo:The circuit is a bipolar cascode configuration with two NMOS transistors Q1 and Q2. The output current Iout is derived from the collector of Q2. The resistor rO2 is connected between the output and node X, and resistor rO1 is connected between node X and ground. Capacitor C1e2 is connected between node X and ground. The input voltage Vin controls the gate of Q1, and the gate of Q2 is grounded.

Figure 9.17 (a) Short-circuit output current of a cascode, (b) detailed view of (a).

The reader may view Eq. (9.46) dubiously. After all, as shown in Fig. 9.17(b), the collector current of $Q_{1}$ must split between $r_{O 1}$ and the impedance seen looking into the emitter of $Q_{2}$. We must therefore verify that only a negligible fraction of $g_{m 1} v_{i n}$ is "lost" in $r_{O 1}$. Since the base and collector voltages of $Q_{2}$ are equal, this transistor can be viewed as a diode-connected device having an impedance of $\left(1 / g_{m 2}\right) \| r_{O 2}$. Dividing $g_{m 1} v_{i n}$ between this impedance and $r_{O 1}$, we have

$$
\begin{equation*}
i_{\text {out }}=g_{m 1} v_{i n} \frac{r_{O 1} \| r_{\pi 2}}{r_{O 1}\left\|r_{\pi 2}+\frac{1}{g_{m 2}}\right\| r_{O 2}} \tag{9.47}
\end{equation*}
$$

For typical transistors, $1 / g_{m 2} \ll r_{O 2}, r_{O 1}$, and hence

$$
\begin{equation*}
i_{\text {out }} \approx g_{m 1} v_{\text {in }} \tag{9.48}
\end{equation*}
$$

That is, the approximation $G_{m}=g_{m 1}$ is reasonable.
To obtain the overall voltage gain, we write from Eqs. (9.33) and (9.5),

$$
\begin{align*}
A_{v} & =-G_{m} R_{\text {out }}  \tag{9.49}\\
& =-g_{m 1}\left\{\left[1+g_{m 2}\left(r_{O 1} \| r_{\pi 2}\right)\right] r_{O 2}+r_{O 1} \| r_{\pi 2}\right\}  \tag{9.50}\\
& \approx-g_{m 1}\left[g_{m 2}\left(r_{O 1} \| r_{\pi 2}\right) r_{O 2}+r_{O 1} \| r_{\pi 2}\right] . \tag{9.51}
\end{align*}
$$

Also, since $Q_{1}$ and $Q_{2}$ carry approximately equal bias currents, $g_{m 1} \approx g_{m 2}$ and $r_{O 1} \approx r_{O 2}$ :

$$
\begin{align*}
A_{v} & =-g_{m 1} r_{O 1}\left[g_{m 1}\left(r_{O 1} \| r_{\pi 2}\right)+1\right]  \tag{9.52}\\
& \approx-g_{m 1} r_{O 1} g_{m 1}\left(r_{O 1} \| r_{\pi 2}\right) . \tag{9.53}
\end{align*}
$$

Compared to the simple CE stage of Fig. 9.16(a), the cascode amplifier exhibits a gain that is higher by a factor of $g_{m 1}\left(r_{O 1} \| r_{\pi 2}\right)$-a relatively large value because $r_{O 1}$ and $r_{\pi 2}$ are much greater than $1 / g_{m 1}$. $\beta=100$ for both transistors, determine the voltage gain. Assume the load is an ideal current source.

Solution We have $g_{m 1}=(26 \Omega)^{-1}, r_{\pi 1} \approx r_{\pi 2} \approx 2600 \Omega, r_{O 1} \approx r_{O 2}=5 \mathrm{k} \Omega$. Thus,

$$
\begin{equation*}
g_{m 1}\left(r_{O 1} \| r_{\pi 2}\right)=65.8 \tag{9.54}
\end{equation*}
$$

and from Eq. (9.53),

$$
\begin{equation*}
\left|A_{v}\right|=12,654 . \tag{9.55}
\end{equation*}
$$

Cascoding thus raises the voltage gain by a factor of 65.8.
Exercise What Early voltage gives a gain of 5,000?

It is possible to view the cascode amplifier as a common-emitter stage followed by a common-base stage. Illustrated in Fig. 9.18, the idea is to consider the cascode device, $Q_{2}$, as a common-base transistor that senses the small-signal current produced by $Q_{1}$. This perspective may prove useful in some cases.
image_name:Figure 9.18
description:
[
name: I1, type: CurrentSource, value: I1, ports: {Np: VCC, Nn: Vout}
name: Q1, type: NPN, ports: {C: C1E2, B: Vin, E: GND}
name: Q2, type: NPN, ports: {C: Vout, B: Vb, E: C1E2}
]
extrainfo:The circuit is a cascode amplifier with a common-emitter (CE) stage formed by Q1 and a common-base (CB) stage formed by Q2. The current source I1 provides biasing from VCC, and the output is taken from the collector of Q2.

Figure 9.18 Cascode amplifier as a cascade of a CE stage and a CB stage.

The high voltage gain of the cascode topology makes it attractive for many applications. But, in the circuit of Fig. 9.16(b), the load is assumed to be an ideal current source. An actual current source lowers the impedance seen at the output node and hence the voltage gain. For example, the circuit illustrated in Fig. 9.19(a) suffers from a low gain because the pnp current source introduces an impedance of only $r_{O 3}$ from the output node to ac ground, dropping the output impedance to

$$
\begin{align*}
R_{\text {out }} & =r_{O 3} \|\left\{\left[1+g_{m 2}\left(r_{O 1} \| r_{\pi 2}\right)\right] r_{O 2}+r_{O 1} \| r_{\pi 2}\right\}  \tag{9.56}\\
& \approx r_{O 3} \|\left[g_{m 2} r_{O 2}\left(r_{O 1} \| r_{\pi 2}\right)+r_{O 1} \| r_{\pi 2}\right] . \tag{9.57}
\end{align*}
$$

How should we realize the load current source to maintain a high gain? We know from Section 9.1.1 that cascoding also raises the output impedance of current sources, postulating that the circuit of Fig. 9.5 is a good candidate and arriving at the stage depicted in Fig. 9.19(b). The output impedance is now given by the parallel
image_name:Figure 9.19 (a)
description:
[
'name': 'Q1', 'type': 'NPN', 'ports': {'C': 'c1e2', 'B': 'Vin', 'E': 'GND'
'name': 'Q2', 'type': 'NPN', 'ports': {'C': 'Vout', 'B': 'Vb1', 'E': 'c1e2'
'name': 'Q3', 'type': 'PNP', 'ports': {'C': 'Vout', 'B': 'Vb2', 'E': 'VCC'
'name': 'Q1', 'type': 'NPN', 'ports': {'C': 'c1e2', 'B': 'Vin', 'E': 'c1e2'
'name': 'Q2', 'type': 'NPN', 'ports': {'C': 'c2', 'B': 'Vb1', 'E': 'c1e2'
'name': 'ro3', 'type': 'Resistor', 'value': 'ro3', 'ports': {'N1': 'VCC', 'N2': 'Vout'
]
extrainfo:The circuit in Figure 9.19 (a) is a cascode amplifier with a simple current-source load. It consists of two NPN transistors (Q1 and Q2) and two PNP transistors (Q3 and Q4) used to increase the voltage gain by raising the output impedance. Capacitors C2 and Cie2 are used for AC coupling and bypassing, respectively. Resistors Rop and Ron form a part of the load to achieve high gain. The circuit is powered by Vcc.
image_name:Figure 9.19 (b)
description:
[
name: Q1, type: NPN, ports: {C: c1e2, B: Vin, E: GND}
name: Q2, type: NPN, ports: {C: Vout, B: Vb1, E: c1e2}
name: Q3, type: PNP, ports: {C: Vout, B: Vb2, E: e3c4}
name: Q4, type: PNP, ports: {C: Vcc, B: Vb3, E: e3c4}
]
extrainfo:The circuit in Figure 9.19(b) is a cascode amplifier with a high output impedance achieved by using both NPN and PNP transistors in a cascode configuration. The load consists of a combination of resistors and capacitors to enhance voltage gain. The NPN transistors Q1 and Q2 form the input stage, while the PNP transistors Q3 and Q4 form the cascode load to increase output impedance and gain.

Figure 9.19 (a) Cascode with a simple current-source load, (b) use of cascode in the load to raise the voltage gain.
combination of those of the $n p n$ and $p n p$ cascodes, $R_{o n}$ and $R_{o p}$, respectively. Using Eq. (9.7), we have

$$
\begin{align*}
& R_{o n} \approx g_{m 2} r_{O 2}\left(r_{O 1} \| r_{\pi 2}\right)  \tag{9.58}\\
& R_{o p} \approx g_{m 3} r_{O 3}\left(r_{o 4} \| r_{\pi 3}\right) \tag{9.59}
\end{align*}
$$

Note that, since $n p n$ and $p n p$ devices may display different Early voltages, $r_{O 1}\left(=r_{O 2}\right)$ may not be equal to $r_{O 3}\left(=r_{O 4}\right)$.

Recognizing that the short-circuit transconductance, $G_{m}$, of the stage is still approximately equal to $g_{m 1}$ (why?), we express the voltage gain as

$$
\begin{align*}
A_{v} & =-g_{m 1}\left(R_{o n} \| R_{o p}\right)  \tag{9.60}\\
& \approx-g_{m 1}\left\{\left[g_{m 2} r_{O 2}\left(r_{o 1} \| r_{\pi 2}\right)\right] \|\left[g_{m 3} r_{O 3}\left(r_{O 4} \| r_{\pi 3}\right)\right]\right\} . \tag{9.61}
\end{align*}
$$

This result represents the highest voltage gain that can be obtained in a cascode stage. For comparable values of $R_{o n}$ and $R_{o p}$, this gain is about half of that expressed by Eq. (9.53).

Example Suppose the circuit of Example 9.9 incorporates a cascode load using pnp transistors with $V_{A}=4 \mathrm{~V}$ and $\beta=50$. What is the voltage gain?

Solution The load transistors carry a collector current of approximately 1 mA . Thus,

$$
\begin{align*}
R_{o p} & =g_{m 3} r_{O 3}\left(r_{O 4} \| r_{\pi 3}\right)  \tag{9.62}\\
& =151 \mathrm{k} \Omega \tag{9.63}
\end{align*}
$$

and

$$
\begin{equation*}
R_{o n}=329 \mathrm{k} \Omega \tag{9.64}
\end{equation*}
$$

It follows that

$$
\begin{align*}
\left|A_{v}\right| & =g_{m 1}\left(R_{o n} \| R_{o p}\right)  \tag{9.65}\\
& =3,981 . \tag{9.66}
\end{align*}
$$

Compared to the ideal current source case, the gain has fallen by approximately a factor of 3 because the $p n p$ devices suffer from a lower Early voltage and $\beta$.

Exercise Repeat the above example for a collector bias current of 0.5 mA .

It is important to take a step back and appreciate our analysis techniques. The cascode of Fig. 9.19(b) proves quite formidable if we attempt to replace each transistor with its small-signal model and solve the resulting circuit. Our gradual approach to constructing this stage reveals the role of each device, allowing straightforward calculation of the output impedance. Moreover, the lemma illustrated in Fig. 9.14 utilizes our knowledge of the output impedance to quickly provide the voltage gain of the stage.

Did you know?

The cascode stage was originally invented to suppress an undesirable high-frequency phenomenon called the "Miller effect" (Chapter 11). In fact, many discrete bipolar amplifiers still employ cascoding for the same reason. However, it was recognized in early days of CMOS technology that cascodes could also provide a high output impedance and a high voltage gain, hence their widespread use.

CMOS Cascode Amplifier The foregoing analysis of the bipolar cascode amplifier can readily be extended to the CMOS counterpart. Depicted in Fig. 9.20(a) with an ideal current-source load, this stage also provides a short-circuit transconductance $G_{m} \approx g_{m 1}$ if $1 / g_{m 2} \ll r_{O 1}$. The output resistance is given by Eq. (9.22), yielding a voltage gain of

$$
\begin{align*}
A_{v} & =-G_{m} R_{\text {out }}  \tag{9.67}\\
& \approx-g_{m 1}\left[\left(1+g_{m 2} r_{O 2}\right) r_{O 1}+r_{O 2}\right]  \tag{9.68}\\
& \approx-g_{m 1} r_{O 1} g_{m 2} r_{O 2} . \tag{9.69}
\end{align*}
$$

In other words, compared to a simple common-source stage, the voltage gain has risen by a factor of $g_{m_{2}} r_{O 2}$ (the intrinsic gain of the cascode device). Since $\beta$ and $r_{\pi}$ are infinite for MOS
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: Vin}
name: M2, type: NMOS, ports: {S: X, D: Vout, G: Vb1}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: Vout}
]
extrainfo:The circuit is a MOS cascode amplifier with a PMOS cascode current source. M1 and M2 are NMOS transistors, while M3 and M4 are PMOS transistors. The current source I1 provides biasing. The circuit is designed to enhance voltage gain by using cascode configurations.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: Vin}
name: M2, type: NMOS, ports: {S: X, D: Vout, G: Vb1}
name: M3, type: PMOS, ports: {S:  s3d4, D: Vout, G: Vb2}
name: M4, type: PMOS, ports: {S: VDD, D: s3d4, G: Vb2}
]
extrainfo:The circuit is a PMOS cascode amplifier with a cascode PMOS current source to maintain a high output impedance. It includes two NMOS transistors (M1 and M2) and two PMOS transistors (M3 and M4) with a current source I1 connected from VDD to Vout.

Figure 9.20 (a) MOS cascode amplifier, (b) realization of load by a PMOS cascode.
devices (at low frequencies), we can also utilize Eq. (9.53) to arrive at Eq. (9.69). Note, however, that $M_{1}$ and $M_{2}$ need not exhibit equal transconductances or output resistances (their widths and lengths need not be the same) even though they carry equal currents (why?).

As with the bipolar counterpart, the MOS cascode amplifier must incorporate a cascode PMOS current source so as to maintain a high voltage gain. Illustrated in Fig. 9.20(b), the circuit exhibits the following output impedance components:

$$
\begin{align*}
& R_{o n} \approx g_{m 2} r_{O 2} r_{O 1}  \tag{9.70}\\
& R_{o p} \approx g_{m 3} r_{O 3} r_{O 4} \tag{9.71}
\end{align*}
$$

The voltage gain is therefore equal to

$$
\begin{equation*}
A_{v} \approx-g_{m 1}\left[\left(g_{m 2} r_{O 2} r_{O 1}\right) \|\left(g_{m 3} r_{O 3} r_{O 4}\right)\right] . \tag{9.72}
\end{equation*}
$$

Example
9.11

The cascode amplifier of Fig. 9.20(b) incorporates the following device parameters: $(W / L)_{1,2}=30,(W / L)_{3,4}=40, I_{D 1}=\cdots=I_{D 4}=0.5 \mathrm{~mA}$. If $\mu_{n} C_{o x}=100 \mu \mathrm{~A} / \mathrm{V}^{2}$, $\mu_{p} C_{o x}=50 \mu \mathrm{~A} / \mathrm{V}^{2}, \lambda_{n}=0.1 \mathrm{~V}^{-1}$ and $\lambda_{p}=0.15 \mathrm{~V}^{-1}$, determine the voltage gain.

Solution With the particular choice of device parameters here, $g_{m 1}=g_{m 2}, r_{O 1}=r_{O 2}, g_{m 3}=g_{m 4}$, and $r_{O 3}=r_{O 4}$. We have

$$
\begin{align*}
g_{m 1,2} & =\sqrt{2 \mu_{n} C_{o x}\left(\frac{W}{L}\right)_{1,2} I_{D 1,2}}  \tag{9.73}\\
& =(577 \Omega)^{-1} \tag{9.74}
\end{align*}
$$

and

$$
\begin{equation*}
g_{m 3,4}=(707 \Omega)^{-1} \tag{9.75}
\end{equation*}
$$

Also,

$$
\begin{align*}
r_{O 1,2} & =\frac{1}{\lambda_{n} I_{D 1,2}}  \tag{9.76}\\
& =20 \mathrm{k} \Omega \tag{9.77}
\end{align*}
$$

and

$$
\begin{equation*}
r_{O 3,4}=13.3 \mathrm{k} \Omega . \tag{9.78}
\end{equation*}
$$

Equations (9.70) and (9.71) thus respectively give

$$
\begin{align*}
& R_{o n} \approx 693 \mathrm{k} \Omega  \tag{9.79}\\
& R_{o p} \approx 250 \mathrm{k} \Omega \tag{9.80}
\end{align*}
$$

and

$$
\begin{align*}
A_{v} & =-g_{m 1}\left(R_{o n} \| R_{o p}\right)  \tag{9.81}\\
& \approx-318 . \tag{9.82}
\end{align*}
$$

Exercise Explain why a lower bias current results in a higher output impedance in the above example. Calculate the output impedance for a drain current of 0.25 mA .

## 9.2 CURRENT MIRRORS

### 9.2.1 Initial Thoughts

The biasing techniques studied for bipolar and MOS amplifiers in Chapters 4 and 6 prove inadequate for high-performance microelectronic circuits. For example, the bias current of CE and CS stages is a function of the supply voltage-a serious issue because in practice, this voltage experiences some variation. The rechargeable battery in a cellphone or laptop computer, for example, gradually loses voltage as it is discharged, thereby mandating that the circuits operate properly across a range of supply voltages.

Another critical issue in biasing relates to ambient temperature variations. A cellphone must maintain its performance at $-20^{\circ} \mathrm{C}$ in Finland and $+50^{\circ} \mathrm{C}$ in Saudi Arabia. To understand how temperature affects the biasing, consider the bipolar current source shown in Fig. 9.21(a), where $R_{1}$ and $R_{2}$ divide $V_{C C}$ down to the required $V_{B E}$. That is, for a desired current $I_{1}$, we have

$$
\begin{equation*}
\frac{R_{2}}{R_{1}+R_{2}} V_{C C}=V_{T} \ln \frac{I_{1}}{I_{S}} \tag{9.83}
\end{equation*}
$$

where the base current is neglected. But, what happens if the temperature varies? The left-hand side remains constant if the resistors are made of the same material and hence vary by the same percentage. The right-hand side, however, contains two temperaturedependent parameters: $V_{T}=k T / q$ and $I_{S}$. Thus, even if the base-emitter voltage remains constant with temperature, $I_{1}$ does not.

A similar situation arises in CMOS circuits. Illustrated in Fig. 9.21(b), a MOS current source biased by means of a resistive divider suffers from dependence on $V_{D D}$ and temperature. Here, we can write

$$
\begin{align*}
I_{1} & =\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2}  \tag{9.84}\\
& =\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(\frac{R_{2}}{R_{1}+R_{2}} V_{D D}-V_{T H}\right)^{2} . \tag{9.85}
\end{align*}
$$

Since both the mobility and the threshold voltage vary with temperature, $I_{1}$ is not constant even if $V_{G S}$ is.

In summary, the typical biasing schemes introduced in Chapters 4 and 6 fail to establish a constant collector or drain current if the supply voltage or the ambient temperature are subject to change. Fortunately, an elegant method of creating supply- and temperatureindependent voltages and currents exists and appears in almost all microelectronic systems. Called the "bandgap reference circuit" and employing several tens of devices, this scheme is studied in more advanced books [1].
image_name:(a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: VCC, N2: VBE}
name: R2, type: Resistor, value: R2, ports: {N1: VBE, N2: GND}
name: Q1, type: NPN, ports: {C: LOAD, B: VBE, E: GND}
]
extrainfo:This circuit represents an impractical biasing scheme for a bipolar current source, with a focus on maintaining a constant current I1 through the load. The voltage VBE is used to bias the NPN transistor Q1.
image_name:(b)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: VGS}
name: R2, type: Resistor, value: R2, ports: {N1: VGS, N2: GND}
name: M1, type: NMOS, ports: {S: GND, D: LOAD, G: VGS}
]
extrainfo:Figure 9.22(b) illustrates a MOS current source using an NMOS transistor with resistors R1 and R2 forming a voltage divider to set the gate-source voltage VGS. The current I1 flows from VDD through the load to ground.

Figure 9.21 Impractical biasing of (a) bipolar and (b) MOS current sources.
image_name:Figure 9.22
description:The system block diagram labeled "Figure 9.22" illustrates the concept of a current mirror. This diagram includes the following main components:

1. **Current Source (I_REF):**
- Positioned on the left side of the diagram, this is a reference current source providing a constant current denoted as \( I_{REF} \). This current is used as the baseline for generating a mirrored current.

2. **Current Mirror Block:**
- Located centrally in the diagram, this block is responsible for replicating the reference current. It is labeled "Current Mirror" and functions to produce a copy of the input current \( I_{REF} \) as the output current \( I_{copy} \).

3. **Output Current (I_copy):**
- On the right side of the diagram, \( I_{copy} \) represents the output current that is a mirrored version of \( I_{REF} \). This current flows from the current mirror block to an external load or circuit.

4. **Voltage Supply (V_CC):**
- Positioned above the current mirror block, \( V_{CC} \) is the supply voltage necessary for the operation of the current mirror. It provides the necessary power for the current mirroring process.

**Flow of Information or Control:**
- The reference current \( I_{REF} \) flows into the current mirror block, where it is used to generate a proportional output current \( I_{copy} \). The direction of current flow is from the current source to the current mirror and then out to the load.
- The supply voltage \( V_{CC} \) ensures that the current mirror operates correctly by providing the required voltage level for the circuit.

**Overall System Function:**
- The primary function of this system is to replicate a reference current \( I_{REF} \) through the current mirror, generating an output current \( I_{copy} \) that can be used in other parts of an integrated circuit. This is essential for applications requiring multiple matched currents, such as biasing in amplifiers or other analog circuits.

Figure 9.22 Concept of current mirror.

The bandgap circuit by itself does not solve all of our problems! An integrated circuit may incorporate hundreds of current sources, e.g., as the load impedance of CE or CS stages to achieve a high gain. Unfortunately, the complexity of the bandgap prohibits its use for each current source in a large integrated circuit.

Let us summarize our thoughts thus far. In order to avoid supply and temperature dependence, a bandgap reference can provide a "golden current" while requiring a few tens of devices. We must therefore seek a method of "copying" the golden current without duplicating the entire bandgap circuitry. Current mirrors serve this purpose.

Figure 9.22 conceptually illustrates our goal here. The golden current generated by a bandgap reference is "read" by the current mirror and a copy having the same characteristics as those of $I_{R E F}$ is produced. For example, $I_{\text {copy }}=I_{R E F}$ or $2 I_{R E F}$.

### 9.2.2 Bipolar Current Mirror

Since the current source generating $I_{\text {copy }}$ in Fig. 9.22 must be implemented as a bipolar or MOS transistor, we surmise that the current mirror resembles the topology shown in Fig. 9.23(a), where $Q_{1}$ operates in the forward active region and the black box guarantees $I_{\text {copy }}=I_{R E F}$ regardless of temperature or transistor characteristics. (The MOS counterpart is similar.)

How should the black box of Fig. 9.23(a) be realized? The black box generates an output voltage, $V_{X}\left(=V_{B E}\right)$, such that $Q_{1}$ carries a current equal to $I_{R E F}$ :

$$
\begin{equation*}
I_{S 1} \exp \frac{V_{X}}{V_{T}}=I_{R E F}, \tag{9.86}
\end{equation*}
$$

where the Early effect is neglected. Thus, the black box satisfies the following relationship:

$$
\begin{equation*}
V_{X}=V_{T} \ln \frac{I_{R E F}}{I_{S 1}} \tag{9.87}
\end{equation*}
$$

image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: LOAD, B: X, E: GND}
name: IREF, type: CurrentSource, value: IREF, ports: {Np: VCC, Nn: X}
]
extrainfo:The circuit in diagram (a) is designed to generate a voltage V_BE across a transistor Q1 such that it carries a current equal to I_REF. The black box is a voltage generator that outputs a voltage proportional to the natural logarithm of its input current. In diagram (b), QREF is used to create the voltage V1, which satisfies the equation V1 = V_T ln(I_REF/I_S1). Diagram (c) shows a current mirror configuration using Q1 and QREF to copy the reference current I_REF to the load.
image_name:(b)
description:
[
name: I_REF, type: CurrentSource, value: I_REF, ports: {Np: VCC, Nn: V1}
name: Q_REF, type: NPN, ports: {C: V1, B: V1, E: GND}
]
extrainfo:Figure 9.23(b) illustrates a circuit where a diode-connected NPN transistor (Q_REF) is used to generate a voltage V1 proportional to the natural logarithm of the current I_REF. This configuration forms a basic current mirror.
image_name:(c)
description:
[
name: I_REF, type: CurrentSource, value: I_REF, ports: {Np: VCC, Nn: X}
name: Q_REF, type: NPN, ports: {C: X, B: X, E: GND}
name: Q1, type: NPN, ports: {C: LOAD, B: X, E: GND}
]
extrainfo:The circuit is a current mirror configuration that copies the reference current I_REF to the load, maintaining the same current I_copy through Q1. The node X is a shared base connection for both transistors, ensuring the current mirror operation.

Figure 9.23 (a) Conceptual illustration of current copying, (b) voltage proportional to natural logarithm of current, (c) bipolar current mirror.

We must therefore seek a circuit whose output voltage is proportional to the natural logarithm of its input, i.e., the inverse function of bipolar transistor characteristics. Fortunately, a single diode-connected device satisfies Eq. (9.87). Neglecting the base-current in Fig. 9.23(b), we have

$$
\begin{equation*}
V_{1}=V_{T} \ln \frac{I_{R E F}}{I_{S, R E F}}, \tag{9.88}
\end{equation*}
$$

where $I_{S, R E F}$ denotes the reverse saturation current of $Q_{R E F}$. In other words, $V_{1}=V_{X}$ if $I_{S, R E F}=I_{S 1}$, i.e., if $Q_{R E F}$ is identical to $Q_{1}$.

Figure 9.23(c) consolidates our thoughts, displaying the current mirror circuitry. We say $Q_{1}$ "mirrors" or copies the current flowing through $Q_{R E F}$. For now, we neglect the base currents. From one perspective, $Q_{R E F}$ takes the natural logarithm of $I_{R E F}$ and $Q_{1}$ takes the exponential of $V_{X}$, thereby yielding $I_{c o p y}=I_{R E F}$. From another perspective, since $Q_{R E F}$ and $Q_{1}$ have equal base-emitter voltages, we can write

$$
\begin{align*}
& I_{R E F}=I_{S, R E F} \exp \frac{V_{X}}{V_{T}}  \tag{9.89}\\
& I_{c o p y}=I_{S 1} \exp \frac{V_{X}}{V_{T}} \tag{9.90}
\end{align*}
$$

and hence

$$
\begin{equation*}
I_{c o p y}=\frac{I_{S 1}}{I_{S, R E F}} I_{R E F}, \tag{9.91}
\end{equation*}
$$

which reduces to $I_{c o p y}=I_{R E F}$ if $Q_{R E F}$ and $Q_{1}$ are identical. This holds even though $V_{T}$ and $I_{S}$ vary with temperature. Note that $V_{X}$ does vary with temperature but in such a way that $I_{\text {copy }}$ does not.

An electrical engineering student who is excited by the concept of the current mirror constructs the circuit but forgets to tie the base of $Q_{R E F}$ to its collector (Fig. 9.24). Explain what happens.
image_name:Figure 9.24
description:
[
name: I_REF, type: CurrentSource, ports: {Np: VCC, Nn: Cref}
name: Q_REF, type: NPN, ports: {C: Cref, B: bibref, E: GND}
name: Q1, type: NPN, ports: {C: LOAD, B: bibref, E: GND}
]
extrainfo:The circuit is a current mirror configuration with a missing base-collector connection for Q_REF. This results in no defined base-emitter voltage for the transistors, causing I_copy to be 0.

Figure 9.24
Solution The circuit provides no path for the base currents of the transistors. More fundamentally, the base-emitter voltage of the devices is not defined. The lack of the base currents translates to $I_{\text {copy }}=0$.

Exercise What is the region of operation of $Q_{R E F}$ ?

Example
9.13

Realizing the mistake in the above circuit, the student makes the modification shown in Fig. 9.25, hoping that the battery $V_{X}$ provides the base currents and defines the baseemitter voltage of $Q_{R E F}$ and $Q_{1}$. Explain what happens.
image_name:Figure 9.25
description:
[
name: I_REF, type: CurrentSource, ports: {Np: VCC, Nn: CREF}
name: VX, type: VoltageSource, ports: {Np: VX, Nn: GND}
name: Q_REF, type: NPN, ports: {C: CREF, B: Vx, E: GND}
name: Q_1, type: NPN, ports: {C: LOAD, B: Vx, E: GND}
]
extrainfo:The circuit includes two NPN transistors, Q_REF and Q_1, with a shared base voltage Vx. The current source I_REF provides current to the node CREF. The capacitor C_ref is connected between Vx and GND.

Figure 9.25

Solution While $Q_{1}$ now carries a finite current, the biasing of $Q_{1}$ is no different from that in Fig. 9.21; i.e.,

$$
\begin{equation*}
I_{c o p y}=I_{S 1} \exp \frac{V_{X}}{V_{T}}, \tag{9.92}
\end{equation*}
$$

which is a function of temperature if $V_{X}$ is constant. The student has forgotten that a diode-connected device is necessary here to ensure that $V_{X}$ remains proportional to $\ln \left(I_{R E F} / I_{S, R E F}\right)$.

Exercise $\quad$ Suppose $V_{X}$ is slightly greater than the necessary value, $V_{T} \ln \left(I_{R E F} / I_{S, R E F}\right)$. In what region does $Q_{R E F}$ operate?

We must now address two important questions. First, how do we make additional copies of $I_{R E F}$ to feed different parts of an integrated circuit? Second, how do we obtain different values for these copies, e.g., $2 I_{R E F}, 5 I_{R E F}$, etc.? Considering the topology in Fig. 9.22(c), we recognize that $V_{X}$ can serve as the base-emitter voltage of multiple transistors, thus arriving at the circuit shown in Fig. 9.26(a). The circuit is often drawn as in Fig. 9.26(b) for simplicity. Here, transistor $Q_{j}$ carries a current $I_{c o p y, j}$, given by

$$
\begin{equation*}
I_{c o p y}, j=I_{S, j} \exp \frac{V_{X}}{V_{T}}, \tag{9.93}
\end{equation*}
$$

which, along with Eq. (9.87), yields

$$
\begin{equation*}
I_{\text {copy }, j}=\frac{I_{S, j}}{I_{S, R E F}} I_{R E F} \tag{9.94}
\end{equation*}
$$

The key point here is that multiple copies of $I_{R E F}$ can be generated with minimal additional complexity because $I_{R E F}$ and $Q_{R E F}$ themselves need not be duplicated.

Equation (9.94) readily answers the second question as well: If $I_{S, j}(\propto$ the emitter area of $Q_{j}$ ) is chosen to be $n$ times $I_{S, R E F}\left(\propto\right.$ the emitter area of $\left.Q_{R E F}\right)$, then $I_{c o p y, j}=n I_{R E F}$. We say the copies are "scaled" with respect to $I_{R E F}$. Recall from Chapter 4 that this is equivalent to placing $n$ unit transistors in parallel. Figure 9.26(c) depicts an example where $Q_{1}-Q_{3}$ are identical to $Q_{R E F}$, providing $I_{\text {copy }}=3 I_{R E F}$.
image_name:Figure 9.26 (a)
description:
[
name: I_REF, type: CurrentSource, ports: {Np: VCC, Nn: b1}
name: Q_REF, type: NPN, ports: {C: b1, B: b1, E: GND}
name: Q1, type: NPN, ports: {C: Cref1, B: b1, E: GND}
name: Q2, type: NPN, ports: {C: Cref2, B: b1, E: GND}
name: Q3, type: NPN, ports: {C: Cref3, B: b1, E: GND}
]
extrainfo:The circuit is a current mirror setup with Q_REF as the reference transistor and Q1, Q2, Q3 as the mirror transistors. The output currents I_copy1, I_copy2, and I_copy3 are scaled copies of the reference current I_REF.

image_name:(b)
description:
[
name: I_REF, type: CurrentSource, value: I_REF, ports: {Np: VCC, Nn: Cref}
name: Q_REF, type: NPN, ports: {C: Cref, B: Cref, E: GND}
name: Q_1, type: NPN, ports: {C: Icopy1, B: Cref, E: GND}
name: Q_2, type: NPN, ports: {C: Icopy2, B: Cref, E: GND}
name: Q_3, type: NPN, ports: {C: Icopy3, B: Cref, E: GND}
]
extrainfo:The circuit is a current mirror setup with Q_REF as the reference transistor and Q1, Q2, Q3 as the mirror transistors. The output currents I_copy1, I_copy2, and I_copy3 are scaled copies of the reference current I_REF.

image_name:(c)
description:
[
name: I_REF, type: CurrentSource, value: I_REF, ports: {Np: VCC, Nn: X}
name: Q_REF, type: NPN, ports: {C: X, B: X, E: GND}
name: Q_1, type: NPN, ports: {C: C1C2C3, B: X, E: GND}
name: Q_2, type: NPN, ports: {C: C1C2C3, B: X, E: GND}
name: Q_3, type: NPN, ports: {C: C1C2C3, B: X, E: GND}
]
extrainfo:The circuit is a current mirror setup with Q_REF as the reference transistor and Q1, Q2, Q3 as the mirror transistors. The output current I_copy is a scaled copy (3 times) of the reference current I_REF.

(c)

Figure 9.26 (a) Multiple copies of a reference current, (b) simplified drawing of (a), (c) combining output currents to generate larger copies.

Example A multistage amplifier incorporates two current sources of values 0.75 mA and 9.14 0.5 mA . Using a bandgap reference current of 0.25 mA , design the required current sources. Neglect the effect of the base current for now.

Solution Figure 9.27 illustrates the circuit. Here, all transistors are identical to ensure proper scaling of $I_{R E F}$.
image_name:Figure 9.27
description:
[
name: I_REF, type: CurrentSource, value: 0.25 mA, ports: {Np: VCC, Nn: X}
name: Q_REF, type: NPN, ports: {C: X, B: X, E: GND}
name: Q1, type: NPN, ports: {C: c1c2c3, B: X, E: GND}
name: Q2, type: NPN, ports: {C: c1c2c3, B: X, E: GND}
name: Q3, type: NPN, ports: {C: c1c2c3, B: X, E: GND}
name: Q4, type: NPN, ports: {C: C4C5, B: X, E: GND}
name: Q5, type: NPN, ports: {C: C4C5, B: X, E: GND}
]
extrainfo:The circuit uses a bandgap reference current of 0.25 mA to generate multiple copies of reference currents using current mirrors. Transistors Q1, Q2, and Q3 form a mirror to provide a 0.75 mA output, while Q4 and Q5 provide a 0.5 mA output.

Figure 9.27
Exercise Repeat the above example if the bandgap reference current is 0.1 mA .

The use of multiple transistors in parallel provides an accurate means of scaling the reference in current mirrors. But, how do we create fractions of $I_{R E F}$ ? This is accomplished by realizing $Q_{R E F}$ itself as multiple parallel transistors. Exemplified by the circuit in Fig. 9.28, the idea is to begin with a larger $I_{S, R E F}$ ( $=3 I_{S}$ here) so that a unit
image_name:Figure 9.28
description:
[
name: I_REF, type: CurrentSource, value: 0.25 mA, ports: {Np: Vcc, Nn: X1}
name: Q_REF1, type: NPN, ports: {C: X1, B: X1, E: GND}
name: Q_REF2, type: NPN, ports: {C: X1, B: X1, E: GND}
name: Q_REF3, type: NPN, ports: {C: X1, B: X1, E: GND}
name: Q1, type: NPN, ports: {C: X1, B: X1, E: GND}
]
extrainfo:The circuit is a current mirror configuration that copies a fraction of the reference current I_REF to I_copy using parallel NPN transistors. The reference current is 0.25 mA.

Figure 9.28 Copying a fraction of a reference current.
transistor, $Q_{1}$, can generate a smaller current. Repeating the expressions in Eqs. (9.89) and (9.90), we have

$$
\begin{align*}
& I_{R E F}=3 I_{S} \exp \frac{V_{X}}{V_{T}}  \tag{9.95}\\
& I_{\text {copy }}=I_{S} \exp \frac{V_{X}}{V_{T}} \tag{9.96}
\end{align*}
$$

and hence

$$
\begin{equation*}
I_{\text {copy }}=\frac{1}{3} I_{R E F} \tag{9.97}
\end{equation*}
$$

Example It is desired to generate two currents equal to $50 \mu \mathrm{~A}$ and $500 \mu \mathrm{~A}$ from a reference of 9.15 $\quad 200 \mu \mathrm{~A}$. Design the current mirror circuit.

Solution To produce the smaller current, we must employ four unit transistors for $Q_{R E F}$ such that each carries $50 \mu \mathrm{~A}$. A unit transistor thus generates $50 \mu \mathrm{~A}$ (Fig. 9.29). The current of $500 \mu \mathrm{~A}$ requires 10 unit transistors, denoted by $10 A_{E}$ for simplicity.
image_name:Figure 9.29
description:
[
name: I_REF, type: CurrentSource, value: 0.2mA, ports: {Np: Vcc, Nn: X}
name: Q1, type: NPN, ports: {C: X, B: X, E: GND}
name: Q2, type: NPN, ports: {C: X, B: X, E: GND}
]
extrainfo:The circuit is a current mirror designed to produce two output currents, Icopy1 and Icopy2, from a reference current I_REF of 0.2mA. Q1 and Q2 are NPN transistors configured to mirror the reference current. Q1 is used to generate a smaller current, while Q2 generates a larger current. The circuit uses parallel transistors to achieve the desired current ratios.

Figure 9.29
Exercise Repeat the above example for a reference current of $150 \mu \mathrm{~A}$.

Effect of Base Current We have thus far neglected the base current drawn from node $X$ in Fig. 9.26(a) by all transistors, an effect leading to a significant error as the number
image_name:Figure 9.30
description:
[
name: I_REF, type: CurrentSource, value: I_REF, ports: {Np: VCC, Nn: X}
name: Q_REF, type: NPN, ports: {C: X, B: X, E: GND}
name: Q_1, type: NPN, ports: {C: LOAD, B: X, E: GND}
]
extrainfo:The circuit is designed to copy the reference current I_REF through Q_REF and Q_1, with Q_1 providing a current I_copy to the load. The base current introduces an error in the copied current, as shown in the diagram.

Figure 9.30 Error due to base currents.
of copies (i.e., the total copied current) increases. The error arises because a fraction of $I_{R E F}$ flows through the bases rather than through the collector of $Q_{R E F}$. We analyze the error with the aid of the diagram shown in Fig. 9.30, where $A_{E}$ and $n A_{E}$ denote one unit transistor and $n$ unit transistors, respectively. Our objective is to calculate $I_{\text {copy }}$, recognizing that $Q_{R E F}$ and $Q_{1}$ still have equal base-emitter voltages and hence carry currents with a ratio of $n$. Thus, the base currents of $Q_{1}$ and $Q_{R E F}$ can be expressed as

$$
\begin{gather*}
I_{B 1}=\frac{I_{c o p y}}{\beta}  \tag{9.98}\\
I_{B, R E F}=\frac{I_{c o p y}}{\beta} \cdot \frac{1}{n} . \tag{9.99}
\end{gather*}
$$

Writing a KCL at $X$ therefore yields

$$
\begin{equation*}
I_{R E F}=I_{C, R E F}+\frac{I_{c o p y}}{\beta} \cdot \frac{1}{n}+\frac{I_{c o p y}}{\beta}, \tag{9.100}
\end{equation*}
$$

which, since $I_{C, R E F}=I_{\text {copy }} / n$, leads to

$$
\begin{equation*}
I_{c o p y}=\frac{n I_{R E F}}{1+\frac{1}{\beta}(n+1)} \tag{9.101}
\end{equation*}
$$

For a large $\beta$ and moderate $n$, the second term in the denominator is much less than unity and $I_{\text {copy }} \approx n I_{R E F}$.However, as the copied current ( $\alpha n$ ) increases, so does the error in $I_{\text {copy }}$.

To suppress the above error, the bipolar current mirror can be modified as illustrated in Fig. 9.31. Here, emitter follower $Q_{F}$ is interposed between the collector of $Q_{R E F}$ and node $X$, thereby reducing the effect of the base currents by a factor of $\beta$. More specifically,
image_name:Figure 9.31
description:
[
name: I_REF, type: CurrentSource, value: I_REF, ports: {Np: VCC, Nn: P}
name: Q_REF, type: NPN, ports: {C: P, B: X, E: GND}
name: Q_F, type: NPN, ports: {C: VCC, B: P, E: X}
name: Q_1, type: NPN, ports: {C: LOAD, B: X, E: GND}
]
extrainfo:The circuit is a modified bipolar current mirror with an emitter follower (Q_F) to reduce error due to base currents. The current mirror copies the reference current I_REF to multiple outputs with reduced error.

Figure 9.31 Addition of emitter follower to reduce error due to base currents.
assuming $I_{C, F} \approx I_{E, F}$, we can repeat the above analysis by writing a KCL at $X$ :

$$
\begin{equation*}
I_{C, F}=\frac{I_{c o p y}}{\beta}+\frac{I_{c o p y}}{\beta} \cdot \frac{1}{n} \tag{9.102}
\end{equation*}
$$

obtaining the base current of $Q_{F}$ as

$$
\begin{equation*}
I_{B, F}=\frac{I_{c o p y}}{\beta^{2}}\left(1+\frac{1}{n}\right) \tag{9.103}
\end{equation*}
$$

Another KCL at node $P$ gives

$$
\begin{align*}
I_{R E F} & =I_{B, F}+I_{C, R E F}  \tag{9.104}\\
& =\frac{I_{\text {copy }}}{\beta^{2}}\left(1+\frac{1}{n}\right)+\frac{I_{\text {copy }}}{n} \tag{9.105}
\end{align*}
$$

and hence

$$
\begin{equation*}
I_{\text {copy }}=\frac{n I_{R E F}}{1+\frac{1}{\beta^{2}}(n+1)} \tag{9.106}
\end{equation*}
$$

That is, the error is lowered by a factor of $\beta .^{*}$

Compute the error in $I_{c o p y 1}$ and $I_{c o p y 2}$ in Fig. 9.29 before and after adding a follower.

Solution Noting that $I_{\text {copy1 }}, I_{\text {copy } 2}$, and $I_{C, R E F}$ (the total current flowing through four unit transistors) still retain their nominal ratios (why?), we write a KCL at $X$ :

$$
\begin{align*}
I_{R E F} & =I_{C, R E F}+\frac{I_{c o p y 1}}{\beta}+\frac{I_{\text {copy } 2}}{\beta}+\frac{I_{C, R E F}}{\beta}  \tag{9.107}\\
& =4 I_{c o p y 1}+\frac{I_{\text {copy } 1}}{\beta}+\frac{10 I_{\text {copy } 1}}{\beta}+\frac{I_{C, R E F}}{\beta} \tag{9.108}
\end{align*}
$$

Thus,

$$
\begin{align*}
I_{c o p y 1} & =\frac{I_{R E F}}{4+\frac{15}{\beta}}  \tag{9.109}\\
I_{\text {copy } 2} & =\frac{10 I_{R E F}}{4+\frac{15}{\beta}} \tag{9.110}
\end{align*}
$$

With the addition of emitter follower (Fig. 9.32), we have at $X$ :

$$
\begin{align*}
I_{C, F} & =\frac{I_{C, R E F}}{\beta}+\frac{I_{\text {copy } 1}}{\beta}+\frac{I_{\text {copy } 2}}{\beta}  \tag{9.111}\\
& =\frac{4 I_{\text {copy } 1}}{\beta}+\frac{I_{\text {copy } 1}}{\beta}+\frac{10 I_{\text {copy } 1}}{\beta}  \tag{9.112}\\
& =\frac{15 I_{\text {copy } 1}}{\beta} \tag{9.113}
\end{align*}
$$

${ }^{*}$ In more advanced designs, a constant current is drawn from $X$.

Figure 9.32

A KCL at $P$ therefore yields

$$
\begin{align*}
I_{R E F} & =\frac{15 I_{\text {copy } 1}}{\beta^{2}}+I_{C, R E F}  \tag{9.114}\\
& =\frac{15 I_{\text {copy } 1}}{\beta^{2}}+4 I_{\text {copy } 1}, \tag{9.115}
\end{align*}
$$

and hence

$$
\begin{align*}
& I_{c o p y 1}=\frac{I_{R E F}}{4+\frac{15}{\beta^{2}}}  \tag{9.116}\\
& I_{\text {copy } 2}=\frac{10 I_{R E F}}{4+\frac{15}{\beta^{2}}} . \tag{9.117}
\end{align*}
$$

Exercise Calculate $I_{c o p y 1}$ if one of the four unit transistors is omitted, i.e., the reference transistor has an area of $3 A_{E}$.

PNP Mirrors Consider the common-emitter stage shown in Fig. 9.33(a), where a current source serves as a load to achieve a high voltage gain. The current source can be realized as a pnp transistor operating in the active region [Fig. 9.33(b)]. We must therefore define the bias current of $Q_{2}$ properly. In analogy with the npn counterpart of Fig. 9.23(c), we form
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: Vin, E: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: VCC, Nn: Vout}
]
extrainfo:The circuit is a common-emitter amplifier with a current source load. The NPN transistor Q1 is biased with a current source I1 connected to VCC, providing a high voltage gain. The input is applied to the base of Q1, and the output is taken from the collector.

(a)
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: Vin, E: GND}
name: Q2, type: PNP, ports: {C: Vout, B: Vb, E: VCC}
]
extrainfo:The circuit is a common-emitter amplifier with a current source load. Q1 is an NPN transistor with its collector connected to Vout, base to Vin, and emitter to GND. Q2 is a PNP transistor with its collector connected to Vout, base to Vb, and emitter to VCC. This configuration provides high voltage gain with proper biasing.

(b)
image_name:Figure 9.33
description:
[
name: Q_REF, type: PNP, ports: {C: X, B: X, E: VCC}
name: Q2, type: PNP, ports: {C: Vout, B: X, E: VCC}
name: Q1, type: NPN, ports: {C: Vout, B: Vin, E: GND}
name: I_REF, type: CurrentSource, ports: {Np: X, Nn: GND}
]
extrainfo:The circuit is a common-emitter amplifier with a current source load. Q1 is an NPN transistor with its collector connected to Vout, base to Vin, and emitter to GND. Q2 is a PNP transistor with its collector connected to Vout, base to node X, and emitter to VCC. Q_REF is a PNP transistor with its collector and base connected to node X and emitter to GND. I_REF is a current source connected between node X and GND.

(c)

Figure 9.33 (a) CE stage with current-source load, (b) realization of current source by a pnp device, (c) proper biasing of $Q_{2}$.
the pnp current mirror depicted in Fig. 9.33(c). For example, if $Q_{R E F}$ and $Q_{2}$ are identical and the base currents negligible, then $Q_{2}$ carries a current equal to $I_{R E F}$.

Example Design the circuit of Fig. 9.33(c) for a voltage gain of 100 and a power budget of

9.17 2 mW . Assume $V_{A, n p n}=5 \mathrm{~V}, V_{A, p n p}=4 \mathrm{~V}, I_{R E F}=100 \mu \mathrm{~A}$, and $V_{C C}=2.5 \mathrm{~V}$.

Solution From the power budget and $V_{C C}=2.5 \mathrm{~V}$, we obtain a total supply current of $800 \mu \mathrm{~A}$, of which $100 \mu \mathrm{~A}$ is dedicated to $I_{R E F}$ and $Q_{R E F}$. Thus, $Q_{1}$ and $Q_{2}$ are biased at a current of $700 \mu \mathrm{~A}$, requiring that the (emitter) area of $Q_{2}$ be 7 times that of $Q_{R E F}$. (For example, $Q_{R E F}$ incorporates one unit device and $Q_{1}$ seven unit devices.)

The voltage gain can be written as

$$
\begin{align*}
A_{v} & =-g_{m 1}\left(r_{O 1} \| r_{O 2}\right)  \tag{9.118}\\
& =-\frac{1}{V_{T}} \cdot \frac{V_{A, n p n} V_{A, p n p}}{V_{A, n p n}+V_{A, p n p}}  \tag{9.119}\\
& =-85.5 \tag{9.120}
\end{align*}
$$

What happened here?! We sought a gain of 100 but inevitably obtained a value of 85.5 ! This is because the gain of the stage is simply given by the Early voltages and $V_{T}$, a fundamental constant of the technology and independent of the bias current. Thus, with the above choice of Early voltages, the circuit's gain cannot reach 100.

Exercise What Early voltage is necessary for a voltage gain of 100?

We must now address an interesting problem. In the mirror of Fig. 9.23(c), it is assumed that the golden current flows from $V_{C C}$ to node $X$, whereas in Fig. 9.33(c) it flows from $X$ to ground. How do we generate the latter from the former? It is possible to combine the $n p n$ and $p n p$ mirrors for this purpose, as illustrated in Fig. 9.34. Assuming for simplicity that $Q_{R E F 1}, Q_{M}, Q_{R E F 2}$, and $Q_{2}$ are identical and neglecting the base currents, we observe that $Q_{M}$ draws a current of $I_{R E F}$ from $Q_{R E F 2}$, thereby forcing the same current through $Q_{2}$ and $Q_{1}$. We can also create various scaling scenarios between $Q_{R E F 1}$ and $Q_{M}$ and between $Q_{R E F 2}$ and $Q_{2}$. Note that the base currents introduce a cumulative error as $I_{R E F}$ is copied onto $I_{C, M}$, and $I_{C, M}$ onto $I_{C 2}$.
image_name:Figure 9.34
description:
[
name: I_REF, type: CurrentSource, value: I_REF, ports: {Np: VCC, Nn: X1}
name: Q_REF1, type: NPN, ports: {C: X1, B: X1, E: GND}
name: Q_M, type: NPN, ports: {C: X2, B: X1, E: GND}
name: Q_REF2, type: PNP, ports: {C: X2, B: X2, E: VCC}
name: Q_2, type: PNP, ports: {C: Vout, B: X2, E: VCC}
name: Q_1, type: NPN, ports: {C: Vout, B: Vin, E: GND}
]
extrainfo:The circuit is designed to generate currents for PNP devices, using a reference current I_REF. The current I_REF is mirrored through transistors Q_REF1, Q_M, Q_REF2, and Q_2. Scaling factors can be adjusted to optimize the number of unit transistors used.

Figure 9.34 Generation of current for pnp devices. Choose the scaling factors in the circuit so as to minimize the number of unit transistors.

Solution For an overall scaling factor of $1 \mathrm{~mA} / 25 \mu \mathrm{~A}=40$, we can choose either

$$
\begin{align*}
& I_{C, M}=8 I_{R E F}  \tag{9.121}\\
& \left|I_{C 2}\right|=5 I_{C, M} \tag{9.122}
\end{align*}
$$

or

$$
\begin{align*}
& I_{C, M}=10 I_{R E F}  \tag{9.123}\\
& \left|I_{C 2}\right|=4 I_{C, M} \tag{9.124}
\end{align*}
$$

(In each case, the $n p n$ and $p n p$ scaling factors can be swapped.) In the former case, the four transistors in the current mirror circuitry require 15 units, and in the latter case, 16 units. Note that we have implicitly dismissed the case $I_{C, M}=40 I_{C, R E F 1}$ and $I_{C 2}=I_{C, R E F 2}$ as it would necessitate 43 units.

Exercise Calculate the exact value of $I_{C 2}$ if $\beta=50$ for all transistors.

Example An electrical engineering student purchases two nominally identical discrete bipolar 9.19 transistors and constructs the current mirror shown in Fig. 9.23(c). Unfortunately, $I_{\text {copy }}$ is $30 \%$ higher than $I_{R E F}$. Explain why.

Solution It is possible that the two transistors were fabricated in different batches and hence underwent slightly different processing. Random variations during manufacturing may lead to changes in the device parameters and even the emitter area. As a result, the two transistors suffer from significant $I_{S}$ mismatch. This is why current mirrors are rarely used in discrete design.

Exercise How much $I_{S}$ mismatch results in a $30 \%$ collector current mismatch?

### 9.2.3 MOS Current Mirror

The developments in Section 9.2.2 can be applied to MOS current mirrors as well. In particular, drawing the MOS counterpart of Fig. 9.23(a) as in Fig. 9.35(a), we recognize that the black box must generate $V_{X}$ such that
$\frac{1}{2} \mu_{n} C_{o x}\left(\frac{W}{L}\right)_{1}\left(V_{X}-V_{T H 1}\right)^{2}=I_{R E F}$,
where channel-length modulation is neglected. Thus, the black box must satisfy the following input (current)/output (voltage) characteristic:
$V_{X}=\sqrt{\frac{2 I_{R E F}}{\mu_{n} C_{o x}\left(\frac{W}{L}\right)_{1}}}+V_{T H 1}$.

Did you know?

A simple current mirror may also be considered a two-transistor circuit topology. We can even implement a current amplifier using such an arrangement. As shown below, if the reference (diodeconnected) device is smaller than the currentsource transistor, then $I_{\text {out }} / l_{\text {in }}>1$. For example, if $I_{\text {in }}$ changes by $1 \mu \mathrm{~A}$, then $l_{\text {out }}$ changes by $1 \mu \mathrm{~A} \times n$. Current amplifiers are occasionally used in analog systems. In fact, some analog designers promoted the notion of "current-mode circuits" in the 1990s, but the movement did not catch on.
image_name:Current mirror as an amplifier.
description:
[
name: QREF, type: NPN, ports: {C: Iin, B: Cref, E: GND}
name: Q1, type: NPN, ports: {C: Iout, B: Cref, E: GND}
]
extrainfo:The circuit is a current mirror amplifier using two NPN transistors, QREF and Q1. The input current Iin is mirrored to the output current Iout with amplification factor determined by the transistor sizing.

Current mirror as an amplifier.
image_name:(a)
description:
[
name: I_REF, type: CurrentSource, value: I_REF, ports: {Np: VDD, Nn: X}
name: M1, type: NMOS, ports: {S: GND, D: LOAD, G: X}
]
extrainfo:The circuit diagram (a) shows a conceptual illustration of copying a current using an NMOS device. The input current I_REF is mirrored to the output node LOAD through the NMOS transistor M1. The gate-source voltage V_GS is used to control the current flow. The circuit is a basic NMOS current mirror configuration.
image_name:(b)
description:
[
name: I_REF, type: CurrentSource, value: I_REF, ports: {Np: VDD, Nn: X}
name: M_REF, type: NMOS, ports: {S: GND, D: X, G: X}
]
extrainfo:The circuit is a current mirror using NMOS transistors M_REF and M1. The reference current I_REF is mirrored to the load with the node X serving as the gate voltage for both transistors.
image_name:(c)
description:
[
name: I_REF, type: CurrentSource, value: I_REF, ports: {Np: VDD, Nn: X}
name: M1, type: NMOS, ports: {S: GND, D: LOAD, G: X}
name: M_REF, type: NMOS, ports: {S: GND, D: X, G: X}
]
extrainfo:The circuit diagram (c) shows an NMOS current mirror using two NMOS transistors, M_REF and M1. The reference current I_REF is mirrored to the output current I_copy at the LOAD. The gate-source voltage V_GS for both transistors is set by the voltage at node X, which is common to both gates.

Figure 9.35 (a) Conceptual illustration of copying a current by an NMOS device, (b) generation of a voltage proportional to square root of current, (c) MOS current mirror.

That is, it must operate as a "square-root" circuit. From Chapter 6, we recall that a diode-connected MOSFET provides such a characteristic [Fig. 9.35(b)], thus arriving at the NMOS current mirror depicted in Fig. 9.35(c). As with the bipolar version, we can view the circuit's operation from two perspectives: (1) $M_{\text {REF }}$ takes the square root of $I_{R E F}$ and $M_{1}$ squares the result; or (2) the drain currents of the two transistors can be expressed as

$$
\begin{align*}
I_{D, R E F} & =\frac{1}{2} \mu_{n} C_{o x}\left(\frac{W}{L}\right)_{R E F}\left(V_{X}-V_{T H}\right)^{2}  \tag{9.127}\\
I_{c o p y} & =\frac{1}{2} \mu_{n} C_{o x}\left(\frac{W}{L}\right)_{1}\left(V_{X}-V_{T H}\right)^{2} \tag{9.128}
\end{align*}
$$

where the threshold voltages are assumed equal. It follows that

$$
\begin{equation*}
I_{c o p y}=\frac{\left(\frac{W}{L}\right)_{1}}{\left(\frac{W}{L}\right)_{R E F}} I_{R E F} \tag{9.129}
\end{equation*}
$$

which reduces to $I_{c o p y}=I_{R E F}$ if the two transistors are identical.

Example
9.20

The student working on the circuits in Examples 9.12 and 9.13 decides to try the MOS counterpart, thinking that the gate current is zero and hence leaving the gates floating (Fig. 9.36). Explain what happens.
image_name:Figure 9.36
description:
[
name: M_REF, type: NMOS, ports: {S: GND, D: dref, G: X}
name: M_1, type: NMOS, ports: {S: GND, D: LOAD, G: X}
name: I_REF, type: CurrentSource, ports: {Np: VDD, Nn: dref}
]
extrainfo:The circuit is intended to be a current mirror, but it is not functioning as such because the gates of M_REF and M_1 are floating. This causes the copy current (I_copy) to be poorly defined. The floating node X does not establish a stable gate voltage for either transistor, making the operation unpredictable. The circuit lacks a diode-connected transistor to properly mirror the current.

Figure 9.36

Solution This circuit is not a current mirror because only a diode-connected device can establish Eq. (9.129) and hence a copy current independent of device parameters and temperature. Since the gates of $M_{R E F}$ and $M_{1}$ are floating, they can assume any voltage, e.g., an initial condition created at node $X$ when the power supply is turned on. In other words, $I_{\text {copy }}$ is very poorly defined.

Exercise Is $M_{R E F}$ always off in this circuit?

Generation of additional copies of $I_{R E F}$ with different scaling factors also follows the principles shown in Fig. 9.26. The following example illustrates these concepts.

Example An integrated circuit employs the source follower and the common-source stage shown
9.21 in Fig. 9.37(a). Design a current mirror that produces $I_{1}$ and $I_{2}$ from a $0.3-\mathrm{mA}$ reference.
image_name:Figure 9.37
description:
[
name: M1, type: NMOS, ports: {S: Vout1, D: VDD, G: Vin1}
name: M2, type: PMOS, ports: {S: VDD, D: Vout2, G: Vin2}
name: I1, type: CurrentSource, value: 0.2 mA, ports: {Np: Vout1, Nn: GND}
name: I2, type: CurrentSource, value: 0.5 mA, ports: {Np: Vout2, Nn: GND}
]
extrainfo:The circuit consists of two transistor stages: an NMOS (M1) and a PMOS (M2), each connected to a current source (I1 and I2 respectively). The NMOS M1 is configured with its source connected to Vout1, drain to VDD, and gate to Vin1. The PMOS M2 has its source connected to VDD, drain to Vout2, and gate to Vin2. The current sources I1 and I2 provide currents of 0.2 mA and 0.5 mA respectively, flowing from Vout1 and Vout2 to ground.

(a)
image_name:Figure 9.37(b)
description:
[
name: M1, type: NMOS, ports: {S: Vout1, D: VDD, G: Vin1}
name: M2, type: PMOS, ports: {S: VDD, D: Vout2, G: Vin2}
name: MREF, type: NMOS, ports: {S: GND, D: X, G: X}
name: MI1, type: NMOS, ports: {S: GND, D: Vout1, G: X}
name: MI2, type: NMOS, ports: {S: GND, D: Vout2, G: X}
name: IREF, type: CurrentSource, value: 0.3 mA, ports: {Np: VDD, Nn: X}
]
extrainfo:The circuit consists of a reference current source and two transistor stages. The NMOS M1 and PMOS M2 transistors are configured to provide output voltages at Vout1 and Vout2. The current sources I1 and I2 ensure a steady current flow through the circuit. MREF, MI1, and MI2 are diode-connected to establish biasing conditions.

(b)

Figure 9.37

Solution Following the methods depicted in Figs. 9.28 and 9.29, we select an aspect ratio of $3(W / L)$ for the diode-connected device, $2(W / L)$ for $M_{I 1}$, and $5(W / L)$ for $M_{I 2}$. Figure 9.37(b) shows the overall circuit.

Exercise Repeat the above example if $I_{R E F}=0.8 \mathrm{~mA}$.

Since MOS devices draw a negligible gate current, ${ }^{6}$ MOS mirrors need not resort to the technique shown in Fig. 9.31. On the other hand, channel-length modulation in the

[^7]image_name:Figure 9.38
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: X2, G: X2}
name: M2, type: PMOS, ports: {S: Vout1, D: VDD, G: X2}
name: M3, type: PMOS, ports: {S: VDD, D: Vout2, G: X2}
name: M4, type: NMOS, ports: {S: GND, D: X1, G: X1}
name: M5, type: NMOS, ports: {S: GND, D: X2, G: Vin1}
name: M6, type: NMOS, ports: {S: GND, D: Vout2, G: Vin2}
name: M7, type: NMOS, ports: {S: Vout3, D: VDD, G: Vin3}
name: M8, type: PMOS, ports: {S: VDD, D: Vout4, G: Vin4}
name: M9, type: NMOS, ports: {S: GND, D: Vout3, G: Vin3}
name: M10, type: NMOS, ports: {S: GND, D: Vout4, G: X1}
name: MREF, type: NMOS, ports: {S: GND, D: X1, G: X1}
name: IREF, type: CurrentSource, ports: {Np: VDD, Nn: X1}
]
extrainfo:The circuit combines NMOS and PMOS current mirrors in a typical configuration. It includes cascode stages and followers, with input nodes labeled Vin1, Vin2, Vin3, and Vin4, and corresponding output nodes Vout1, Vout2, Vout3, and Vout4. The circuit is powered by VDD and grounded at GND. A reference current IREF is used for biasing.

Figure 9.38 NMOS and PMOS current mirrors in a typical circuit.
current-source transistors does lead to additional errors. Investigated in Problem 9.53, this effect mandates circuit modifications that are described in more advanced texts [1].

The idea of combining NMOS and PMOS current mirrors follows the bipolar counterpart depicted in Fig. 9.34. The circuit of Fig. 9.38 exemplifies these ideas.

## 9.3 CHAPTER SUMMARY

- Stacking a transistor atop another forms a cascode structure, resulting in a high output impedance.
- The cascode topology can also be considered an extreme case of source or emitter degeneration.
- The voltage gain of an amplifier can be expressed as $-G_{m} R_{\text {out }}$, where $G_{m}$ denotes the short-circuit transconductance of the amplifier. This relationship indicates that the gain of amplifiers can be maximized by maximing their output impedance.
- With its high output impedance, a cascode stage can operate as a high-gain amplifier.
- The load of a cascode stage is also realized as a cascode circuit so as to approach an ideal current source.
- Setting the bias currents of analog circuits to well-defined values is difficult. For example, resistive dividers tied to the base or gate of transistors result in supply- and temperature-dependent currents.
- If $V_{B E}$ or $V_{G S}$ are well-defined, then $I_{C}$ or $I_{D}$ are not.
- Current mirrors can "copy" a well-defined reference current numerous times for various blocks in an analog system.
- Current mirrors can scale a reference current by integer or non-integer factors.
- Current mirrors are rarely used in disrcete design as their accuracy depends on matching between transistors.
