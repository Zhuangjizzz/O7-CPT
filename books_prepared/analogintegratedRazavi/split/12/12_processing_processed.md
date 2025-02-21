# CHAPTER 12 Bandgap

Analog circuits incorporate voltage and current references extensively. Such references are dc quantities that exhibit little dependence on supply and process parameters and a well-defined dependence on the temperature. For example, the bias current of a differential pair must be generated according to a reference, for it affects the voltage gain and noise of the circuit. We have also seen the need for precise voltages to define common-mode levels in op amps. Moreover, in systems such as A/D and D/A converters, a reference is required to define the input or output full-scale range.

In this chapter, we deal with the design of reference generators in CMOS technology, focusing on well-established "bandgap" techniques. First, we study supply-independent biasing and the problem of start-up. Next, we describe temperature-independent references and examine issues such as the effect of offset voltages. Finally, we present constant- $G_{m}$ biasing and study an example of state-of-the-art bandgap references.

## 12.1 ■ General Considerations

As mentioned above, the objective of reference generation is to establish a dc voltage or current that is independent of the supply and process and has a well-defined behavior with temperature. In most applications, the required temperature dependence assumes one of three forms: (1) proportional to absolute temperature (PTAT); (2) constant- $G_{m}$ behavior, i.e., such that the transconductance of certain transistors remains constant; (3) temperature independent. We can therefore divide the task into two design problems: supply-independent biasing and definition of the temperature variation.

In addition to supply, process, and temperature variability, several other parameters of reference generators may be critical as well. These include output impedance, output noise, and power dissipation. We return to these issues later in this chapter.

## 12.2 ■ Supply-Independent Biasing

Our use of bias currents and current mirrors in previous chapters has implicitly assumed that a "golden" reference current is available. As shown in Fig. 12.1(a), if $I_{R E F}$ does not vary with $V_{D D}$, and channellength modulation of $M_{2}$ and $M_{3}$ is neglected, then $I_{D 2}$ and $I_{D 3}$ remain independent of the supply voltage. The question then is-How do we generate $I_{R E F}$ ?
image_name:Figure 12.1(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: X}
name: M2, type: NMOS, ports: {S: GND, D: LOAD1, G: X}
name: M3, type: NMOS, ports: {S: GND, D: LOAD2, G: X}
name: IREF, type: CurrentSource, value: IREF, ports: {Np: VDD, Nn: X}
]
extrainfo:Figure 12.1(a) shows a current mirror biasing circuit using an ideal current source. The circuit consists of three NMOS transistors (M1, M2, M3) and a current source IREF. The output currents ID2 and ID3 are drawn from nodes LOAD1 and LOAD2 respectively. The circuit aims to maintain these currents independent of the supply voltage VDD.
image_name:Figure 12.1(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: X}
name: M2, type: NMOS, ports: {S: GND, D: Load1, G: X}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: X}
]
extrainfo:The circuit is a current mirror with a supply-independent biasing scheme. It uses a resistor R1 to generate a reference current IREF that is less sensitive to variations in VDD. M1 and M2 form the current mirror, with M2 providing the output current Iout.

Figure 12.1 Current mirror biasing using (a) an ideal current source and (b) a resistor.
As an approximation of a current source, we tie a resistor from $V_{D D}$ to the gate of $M_{1}$ [Fig. 12.1(b)]. However, the output current of this circuit is quite sensitive to $V_{D D}$ :

$$
\begin{equation*}
\Delta I_{\text {out }}=\frac{\Delta V_{D D}}{R_{1}+1 / g_{m 1}} \cdot \frac{(W / L)_{2}}{(W / L)_{1}} \tag{12.1}
\end{equation*}
$$

In order to arrive at a less sensitive solution, we postulate that the circuit must bias itself, i.e., $I_{R E F}$ must be somehow derived from $I_{\text {out }}$. The idea is that if $I_{\text {out }}$ is to be ultimately independent of $V_{D D}$, then $I_{R E F}$ can be a replica of $I_{\text {out }}$. Figure 12.2 illustrates an implementation where $M_{3}$ and $M_{4}$ copy $I_{\text {out }}$, thereby defining $I_{R E F}$. In essence, $I_{R E F}$ is "bootstrapped" to $I_{o u t}$. With the sizes chosen here, we have $I_{\text {out }}=K I_{R E F}$ if channel-length modulation is neglected. Note that, since each diode-connected device feeds from a current source, $I_{o u t}$ and $I_{R E F}$ are relatively independent of $V_{D D}$.
image_name:Figure 12.2
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: X}
name: M2, type: NMOS, ports: {S: GND, D: Y, G: X}
name: M3, type: PMOS, ports: {S: VDD, D: Y, G: Y}
name: M4, type: PMOS, ports: {S: VDD, D: X, G: Y}
]
extrainfo:The circuit is designed to establish supply-independent currents with Iout and IREF having little dependence on VDD. M3 and M4 mirror Iout to define IREF, with Iout = K * IREF assuming saturation and negligible channel-length modulation.

Figure 12.2 Simple circuit to establish supply-independent currents.

Since $I_{\text {out }}$ and $I_{R E F}$ in Fig. 12.2 display little dependence on $V_{D D}$, their magnitude is set by other parameters. How do we calculate these currents? Interestingly, if $M_{1}-M_{4}$ operate in saturation and $\lambda \approx 0$, then the circuit is governed by only one equation, $I_{\text {out }}=K I_{R E F}$, and hence can support any current level! For example, if we initially force $I_{R E F}$ to be $10 \mu \mathrm{~A}$, the resulting $I_{\text {out }}$ of $K \times 10 \mu \mathrm{~A}$ "circulates" around the loop, sustaining these current levels in the left and right branches indefinitely.

To uniquely define the currents, we add another constraint to the circuit, e.g., as shown in Fig. 12.3(a). Here, resistor $R_{S}$ decreases the current of $M_{2}$ while the PMOS devices require that $I_{\text {out }}=I_{R E F}$ because they have identical dimensions and thresholds. We can write $V_{G S 1}=V_{G S 2}+I_{D 2} R_{S}$, or

$$
\begin{equation*}
\sqrt{\frac{2 I_{\text {out }}}{\mu_{n} C_{o x}(W / L)_{N}}}+V_{T H 1}=\sqrt{\frac{2 I_{\text {out }}}{\mu_{n} C_{o x} K(W / L)_{N}}}+V_{T H 2}+I_{\text {out }} R_{S} \tag{12.2}
\end{equation*}
$$

Neglecting body effect, we have

$$
\begin{equation*}
\sqrt{\frac{2 I_{\text {out }}}{\mu_{n} C_{o x}(W / L)_{N}}}\left(1-\frac{1}{\sqrt{K}}\right)=I_{\text {out }} R_{S} \tag{12.3}
\end{equation*}
$$

image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: X}
name: M2, type: NMOS, ports: {S: s2, D: Y(Iout), G: X}
name: M3, type: PMOS, ports: {S: VDD, D: Y(Iout), G: Y}
name: M4, type: PMOS, ports: {S: VDD, D: X, G: Y}
name: RS, type: Resistor, value: RS, ports: {N1: s2, N2: GND}
]
extrainfo:The circuit is a current mirror configuration with M1 and M2 as NMOS transistors, and M3 and M4 as PMOS transistors. The resistor RS sets the output current Iout. The circuit uses a reference current IREF to define the currents through M1 and M2.

image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: Y}
name: M2, type: NMOS, ports: {S: GND, D: Y(Iout), G: Y}
name: M3, type: PMOS, ports: {S: s3, D: Y(Iout), G: X}
name: M4, type: PMOS, ports: {S: VDD, D: X, G: X}
name: RS, type: Resistor, value: RS, ports: {N1: VDD, N2: s3}
]
extrainfo:The circuit is a current mirror configuration with M1 and M2 as NMOS transistors, and M3 and M4 as PMOS transistors. The resistor RS sets the output current Iout. The circuit uses a reference current IREF to define the currents through M1 and M2.

Figure 12.3 (a) Addition of $R_{S}$ to define the currents; (b) alternative implementation eliminating body effect.
and hence

$$
\begin{equation*}
I_{\text {out }}=\frac{2}{\mu_{n} C_{o x}(W / L)_{N}} \cdot \frac{1}{R_{S}^{2}}\left(1-\frac{1}{\sqrt{K}}\right)^{2} \tag{12.4}
\end{equation*}
$$

As expected, the current is independent of the supply voltage (but still a function of process and temperature).

The assumption $V_{T H 1}=V_{T H 2}$ introduces some error in the foregoing calculations because the sources of $M_{1}$ and $M_{2}$ are at different voltages. Shown in Fig. 12.3(b) is to place the resistor in the source of $M_{3}$ while eliminating body effect by tying the source and bulk of each PMOS transistor. Another solution is described in Problem 12.1.

The circuits of Figs. 12.3(a) and (b) exhibit little supply dependence if channel-length modulation is negligible. For this reason, relatively long channels are used for all of the transistors in the circuit. This also helps reduce their flicker noise.

#### Example 12.1

Assuming $\lambda \neq 0$ in Fig. 12.3(a), estimate the change in $I_{\text {out }}$ for a small change $\Delta V_{D D}$ in the supply voltage.

#### Solution

Simplifying the circuit as depicted in Fig. 12.4, where $R_{1}=r_{O 1} \|\left(1 / g_{m 1}\right)$ and $R_{3}=r_{O 3} \|\left(1 / g_{m 3}\right)$, we calculate the "gain" from $V_{D D}$ to $I_{\text {out }}$. The small-signal gate-source voltage of $M_{4}$ equals $-I_{o u t} R_{3}$, and the current through $r_{O 4}$ is $\left(V_{D D}-V_{X}\right) / r_{O 4}$. Thus,

$$
\begin{equation*}
\frac{V_{D D}-V_{X}}{r_{O 4}}+I_{o u t} R_{3} g_{m 4}=\frac{V_{X}}{R_{1}} \tag{12.5}
\end{equation*}
$$

image_name:Figure 12.4
description:
[
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: ro4, type: Resistor, value: ro4, ports: {N1: VDD, N2: X}
name: M4, type: PMOS, ports: {S: VDD, D: X, G: g4d2}
name: R1, type: Resistor, value: R1, ports: {N1: X, N2: GND}
name: M2, type: NMOS, ports: {S: s2, D: g4d2, G: X}
name: R3, type: Resistor, value: R3, ports: {N1: VDD, N2: g4d2}
name: ro2, type: Resistor, value: ro2, ports: {N1: g4d2, N2: s2}
name: RS, type: Resistor, value: RS, ports: {N1: s2, N2: GND}
]
extrainfo:The circuit is a small-signal model involving a PMOS (M4) and NMOS (M2) transistor configuration. It calculates the gain from VDD to Iout, considering the transconductance and output resistances of the transistors and resistors in the circuit.

If we denote the equivalent transconductance of $M_{2}$ and $R_{S}$ by $G_{m 2}=I_{\text {out }} / V_{X}$, then

$$
\begin{equation*}
\frac{I_{\text {out }}}{V_{D D}}=\frac{1}{r_{O 4}}\left[\frac{1}{G_{m 2}\left(r_{O 4} \| R_{1}\right)}-g_{m 4} R_{3}\right]^{-1} \tag{12.6}
\end{equation*}
$$

Note from Chapter 3 that

$$
\begin{equation*}
G_{m 2}=\frac{g_{m 2} r_{O 2}}{R_{S}+r_{O 2}+\left(g_{m 2}+g_{m b 2}\right) R_{S} r_{O 2}} \tag{12.7}
\end{equation*}
$$

Interestingly, the sensitivity vanishes if $r_{O 4}=\infty$.

In some applications, the sensitivity given by (12.6) is prohibitively large. Also, owing to various capacitive paths, the supply sensitivity of the circuit rises at high frequencies. For these reasons, the supply voltage of the core is often derived from a locally-generated, less sensitive voltage. We return to this point in Sec. 12.8.

An important issue in supply-independent biasing is the existence of "degenerate" bias points. In the circuit of Fig. 12.3(a), for example, if all of the transistors carry zero current when the supply is turned on, they may remain off indefinitely because the loop can support a zero current in both branches. This condition is not predicted by (12.4) because in manipulating (12.3), we divided both sides by $\sqrt{I_{o u t}}$, tacitly assuming that $I_{\text {out }} \neq 0$. In other words, the circuit can settle in one of two different operating conditions.

Called the "start-up" problem, the above issue is resolved by adding a mechanism that drives the circuit out of the degenerate bias point when the supply is turned on. Shown in Fig. 12.5(a) is a simple example, where the diode-connected device $M_{5}$ provides a current path from $V_{D D}$ through $M_{3}$ and $M_{1}$ to ground upon start-up. Thus, $M_{3}$ and $M_{1}$, and hence $M_{2}$ and $M_{4}$, cannot remain off. Of course, this technique is practical only if $V_{T H 1}+V_{T H 5}+\left|V_{T H 3}\right|<V_{D D}$ and $V_{G S 1}+V_{T H 5}+\left|V_{G S 3}\right|>V_{D D}$, the latter to ensure that $M_{5}$ remains off after start-up. Another start-up circuit is analyzed in Problem 12.2.

The problem of start-up generally requires careful analysis and simulation. The supply voltage must be ramped from zero in a dc sweep simulation (such that parasitic capacitances do not cause false start-up) as well as in a transient simulation and the behavior of the circuit examined for each supply voltage. Figure 12.5(b) depicts an example of the observed behavior in the presence of the start-up circuit. In complex implementations, more than one degenerate point may exist.
image_name:Figure 12.5(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Y, G: Y}
name: M2, type: NMOS, ports: {S: s2, D: X, G: Y}
name: M5, type: NMOS, ports: {S: Y, D: X, G: X}
name: M3, type: PMOS, ports: {S: VDD, D: X, G: X}
name: M4, type: PMOS, ports: {S: VDD, D: Y, G: X}
name: RS, type: Resistor, value: RS, ports: {N1: S2, N2: GND}
]
extrainfo:This circuit diagram illustrates a start-up circuit with NMOS and PMOS transistors and a resistor. The circuit is connected to VDD and GND, with a resistor RS connected to node S2 and ground. The start-up circuit is designed to avoid false start-up by ensuring proper biasing of the transistors.
image_name:Figure 12.5(b)
description:The graph labeled (b) is a plot depicting the relationship between the drain current (I_D2) and the supply voltage (V_DD) in the context of a start-up circuit.

1. **Type of Graph and Function:**
- This is a current-voltage (I-V) graph, illustrating how the drain current changes as the supply voltage is varied.

2. **Axes Labels and Units:**
- The horizontal axis represents the supply voltage (V_DD), typically measured in volts.
- The vertical axis represents the drain current (I_D2), usually measured in amperes.
- Both axes appear to use a linear scale.

3. **Overall Behavior and Trends:**
- The graph starts at the origin, indicating that when the supply voltage is zero, the drain current is also zero.
- As the supply voltage increases, the drain current initially rises sharply.
- After this initial increase, the curve begins to level off, indicating that the current reaches a saturation point where further increases in voltage result in minimal changes in current.

4. **Key Features and Technical Details:**
- A notable feature of this graph is the presence of a 'degenerate point,' which is marked on the curve. This point represents a specific condition where the behavior of the circuit might change or become unstable.
- The curve suggests that beyond this degenerate point, the circuit stabilizes as the current reaches a steady state.

5. **Annotations and Specific Data Points:**
- The degenerate point is specifically annotated on the graph, highlighting its importance in the analysis of the start-up behavior.
- No specific numerical values are provided for the axes or the degenerate point, but the qualitative behavior is clearly depicted.

Figure 12.5 (a) Addition of start-up device to the circuit of Fig. 12.3(a), and (b) illustration of degenerate point.

### 12.3.1 Negative-TC Voltage

The base-emitter voltage of bipolar transistors or, more generally, the forward voltage of a $p n$-junction diode exhibits a negative TC. We first obtain the expression for the TC in terms of readily-available quantities.

For a bipolar device, we can write $I_{C}=I_{S} \exp \left(V_{B E} / V_{T}\right)$, where $V_{T}=k T / q$. The saturation current $I_{S}$ is proportional to $\mu k T n_{i}^{2}$, where $\mu$ denotes the mobility of minority carriers and $n_{i}$ is the intrinsic carrier concentration of silicon. The temperature dependence of these quantities is represented as $\mu \propto \mu_{0} T^{m}$, where $m \approx-3 / 2$, and $n_{i}^{2} \propto T^{3} \exp \left[-E_{g} /(k T)\right]$, where $E_{g} \approx 1.12 \mathrm{eV}$ is the bandgap energy of silicon. Thus,

$$
\begin{equation*}
I_{S}=b T^{4+m} \exp \frac{-E_{g}}{k T} \tag{12.8}
\end{equation*}
$$

where $b$ is a proportionality factor. Writing $V_{B E}=V_{T} \ln \left(I_{C} / I_{S}\right)$, we can now compute the TC of the base-emitter voltage. In taking the derivative of $V_{B E}$ with respect to $T$, we must know the behavior of $I_{C}$ as a function of the temperature. To simplify the analysis, we assume for now that $I_{C}$ is held constant. Thus,

$$
\begin{equation*}
\frac{\partial V_{B E}}{\partial T}=\frac{\partial V_{T}}{\partial T} \ln \frac{I_{C}}{I_{S}}-\frac{V_{T}}{I_{S}} \frac{\partial I_{S}}{\partial T} \tag{12.9}
\end{equation*}
$$

From (12.8), we have

$$
\begin{equation*}
\frac{\partial I_{S}}{\partial T}=b(4+m) T^{3+m} \exp \frac{-E_{g}}{k T}+b T^{4+m}\left(\exp \frac{-E_{g}}{k T}\right)\left(\frac{E_{g}}{k T^{2}}\right) \tag{12.10}
\end{equation*}
$$

Therefore,

$$
\begin{equation*}
\frac{V_{T}}{I_{S}} \frac{\partial I_{S}}{\partial T}=(4+m) \frac{V_{T}}{T}+\frac{E_{g}}{k T^{2}} V_{T} \tag{12.11}
\end{equation*}
$$

With the aid of (12.9) and (12.11), we can write

$$
\begin{align*}
\frac{\partial V_{B E}}{\partial T} & =\frac{V_{T}}{T} \ln \frac{I_{C}}{I_{S}}-(4+m) \frac{V_{T}}{T}-\frac{E_{g}}{k T^{2}} V_{T}  \tag{12.12}\\
& =\frac{V_{B E}-(4+m) V_{T}-E_{g} / q}{T} \tag{12.13}
\end{align*}
$$

Equation (12.13) gives the temperature coefficient of the base-emitter voltage at a given temperature $T$, revealing dependence on the magnitude of $V_{B E}$ itself. With $V_{B E} \approx 750 \mathrm{mV}$ and $T=300 \mathrm{~K}$, we have $\partial V_{B E} / \partial T \approx-1.5 \mathrm{mV} / \mathrm{K}$.

In old bipolar technologies, where $I_{C} / I_{S}$ was relatively small (because the transistors were large), $V_{B E} \approx 700 \mathrm{mV}$ and $\partial V_{B E} / \partial T \approx-1.9 \mathrm{mV} / \mathrm{K}$ at room temperature. Modern bipolar transistors typically operate at much higher current densities, exhibiting $V_{B E} \approx 800 \mathrm{mV}$ and hence $\partial V_{B E} / \partial T \approx-1.5 \mathrm{mV} / \mathrm{K}$ at $T=300 \mathrm{~K}$.

From (12.13), we note that the temperature coefficient of $V_{B E}$ itself depends on the temperature, creating error in constant reference generation if the positive-TC quantity exhibits a constant temperature coefficient.
image_name:Figure 12.6 Generation of PTAT voltage
description:
[
name: Q1, type: NPN, ports: {C: b1c1, B: b1c1, E: GND}
name: Q2, type: NPN, ports: {C: b2c2, B: b2c2, E: GND}
name: nI0, type: CurrentSource, value: nI0, ports: {Np: VDD, Nn: b1c1}
name: I0, type: CurrentSource, value: I0, ports: {Np: VDD, Nn: b2c2}
]
extrainfo:The circuit generates a Proportional To Absolute Temperature (PTAT) voltage by using two NPN transistors Q1 and Q2 biased at different current densities. The voltage difference ΔV_BE is proportional to the absolute temperature. The transistors are connected to ground, and the current sources nI0 and I0 are connected to VDD.

### 12.3.2 Positive-TC Voltage

It was recognized in 1964 [3] that if two bipolar transistors operate at unequal current densities, ${ }^{1}$ then the difference between their base-emitter voltages is directly proportional to the absolute temperature. For example, as shown in Fig. 12.6, if two identical transistors ( $I_{S 1}=I_{S 2}$ ) are biased at collector currents of $n I_{0}$ and $I_{0}$ and their base currents are negligible, then

$$
\begin{align*}
\Delta V_{B E} & =V_{B E 1}-V_{B E 2}  \tag{12.14}\\
& =V_{T} \ln \frac{n I_{0}}{I_{S 1}}-V_{T} \ln \frac{I_{0}}{I_{S 2}}  \tag{12.15}\\
& =V_{T} \ln n \tag{12.16}
\end{align*}
$$

Thus, the $V_{B E}$ difference exhibits a positive temperature coefficient:

$$
\begin{equation*}
\frac{\partial \Delta V_{B E}}{\partial T}=\frac{k}{q} \ln n \tag{12.17}
\end{equation*}
$$

Interestingly, this TC is independent of the temperature or behavior of the collector currents. ${ }^{2}$

- Example 12.2

How must $n$ be chosen to yield a TC of $+1.5 \mathrm{mV} / \mathrm{K}$ so as to cancel the TC of the base-emitter voltage at $T=300 \mathrm{~K}$ ?

#### Solution

We choose $n$ so that $(k / q) \ln n=1.5 \mathrm{mV} / \mathrm{K}$. Since $k / q=V_{T} / T=0.087 \mathrm{mV} / \mathrm{K}$, we have $\ln n \approx 17.2$ and hence $n=2.95 \times 10^{7}$ !! We must therefore modify the circuit to avoid such a large disparity between the two currents.

#### Example 12.3

Calculate $\Delta V_{B E}$ in the circuit of Fig. 12.7, where $Q_{2}$ is formed as the parallel combination of $m$ units, each identical to $Q_{1}$.
image_name:Figure 12.7
description:
[
name: Q1, type: NPN, ports: {C: b1c1, B: b1c1, E: GND}
name: Q2, type: NPN, ports: {C: b2c2, B: b2c2, E: GND}
name: Io, type: CurrentSource, value: Io, ports: {Np: VDD, Nn: b2c2}
name: nIo, type: CurrentSource, value: nIo, ports: {Np: VDD, Nn: b1c1}
]
extrainfo:Q2 is formed by parallel combination of m identical units. The circuit shows a voltage difference ΔV_BE across the bases of Q1 and Q2.

#### Solution

Neglecting base currents, we can write

$$
\begin{align*}
\Delta V_{B E} & =V_{T} \ln \frac{n I_{0}}{I_{S}}-V_{T} \ln \frac{I_{0}}{m I_{S}}  \tag{12.18}\\
& =V_{T} \ln (n m) \tag{12.19}
\end{align*}
$$

The temperature coefficient is therefore equal to $(k / q) \ln (n m)$. In this circuit, the two transistors' current densities differ by a factor of $n m$.

#### Example 12.4

In Fig. 12.9, $R_{1}$ and $R_{2}$ are equal and sustain equal voltages, each carrying a current of $\left(V_{T} \ln n\right) / R_{3}$. We therefore have

$$
\begin{equation*}
V_{\text {out }}=V_{B E 1}+\left(V_{T} \ln n\right) \frac{R_{1}}{R_{3}} \tag{12.24}
\end{equation*}
$$

But the second term is not equal to $17.2 V_{T}$ if we have already chosen $\left(V_{T} \ln n\right)\left(1+R_{2} / R_{3}\right)=17.2 V_{T}$. Explain this discrepancy.

#### Solution

The first terms in (12.23) and (12.24) are different. We substitute $V_{B E 1}=V_{B E 2}+V_{T} \ln n$ in Eq. (12.13):

$$
\begin{align*}
\frac{\partial V_{B E 1}}{\partial T} & =\frac{V_{B E 2}+V_{T} \ln n-(4+m) V_{T}-E_{g} / q}{T}  \tag{12.25}\\
& =\frac{\partial V_{B E 2}}{\partial T}+\frac{k}{q} \ln n \tag{12.26}
\end{align*}
$$

Thus,

$$
\begin{align*}
\frac{\partial V_{o u t}}{\partial T} & =\frac{\partial V_{B E 1}}{\partial T}+\left(\frac{k}{q} \ln n\right) \frac{R_{1}}{R_{3}}  \tag{12.27}\\
& =\frac{\partial V_{B E 2}}{\partial T}+\left(\frac{k}{q} \ln n\right)\left(1+\frac{R_{1}}{R_{3}}\right) \tag{12.28}
\end{align*}
$$

which is consistent with (12.23).

The circuit of Fig. 12.9 entails a number of design issues. We consider each one below.
Collector Current Variation The circuit of Fig. 12.9 violates one of our earlier assumptions: the collector currents of $Q_{1}$ and $Q_{2}$, given by $\left(V_{T} \ln n\right) / R_{3}$, are proportional to $T$, whereas $\partial V_{B E} / \partial T \approx$ $-1.5 \mathrm{mV} / \mathrm{K}$ was derived for a constant current. What happens to the temperature coefficient of $V_{B E}$ if the collector currents are PTAT? As a first-order iterative solution, let us assume that $I_{C 1}=I_{C 2} \approx$ $\left(V_{T} \ln n\right) / R_{3}$. Returning to Eq. (12.9) and including $\partial I_{C} / \partial T$, we have

$$
\begin{equation*}
\frac{\partial V_{B E}}{\partial T}=\frac{\partial V_{T}}{\partial T} \ln \frac{I_{C}}{I_{S}}+V_{T}\left(\frac{1}{I_{C}} \frac{\partial I_{C}}{\partial T}-\frac{1}{I_{S}} \frac{\partial I_{S}}{\partial T}\right) \tag{12.29}
\end{equation*}
$$

Since $\partial I_{C} / \partial T \approx\left(V_{T} \ln n\right) /\left(R_{3} T\right)=I_{C} / T$, we can write

$$
\begin{equation*}
\frac{\partial V_{B E}}{\partial T}=\frac{\partial V_{T}}{\partial T} \ln \frac{I_{C}}{I_{S}}+\frac{V_{T}}{T}-\frac{V_{T}}{I_{S}} \frac{\partial I_{S}}{\partial T} \tag{12.30}
\end{equation*}
$$

Equation (12.13) is therefore modified as

$$
\begin{equation*}
\frac{\partial V_{B E}}{\partial T}=\frac{V_{B E}-(3+m) V_{T}-E_{g} / q}{T} \tag{12.31}
\end{equation*}
$$

indicating that the TC is slightly less negative than $-1.5 \mathrm{mV} / \mathrm{K}$. In practice, accurate simulations are necessary to predict the temperature coefficient.
Compatibility with CMOS Technology Our derivation of a temperature-independent voltage relies on the exponential characteristics of bipolar devices for both negative- and positive-TC quantities. We must therefore seek structures in a standard CMOS technology that exhibit such characteristics.

In $n$-well processes, a $p n p$ transistor can be formed as depicted in Fig. 12.10. A $p^{+}$region (the same as the S/D region of PFETs) inside an $n$-well serves as the emitter and the $n$-well itself as the base. The $p$-type substrate acts as the collector and it is inevitably connected to the most negative supply (usually ground). The circuit of Fig. 12.9 can therefore be redrawn as shown in Fig. 12.11.
image_name:Figure 12.10 Realization of a pnp bipolar transistor in CMOS technology.
description:The image labeled "Figure 12.10 Realization of a pnp bipolar transistor in CMOS technology" depicts a cross-sectional view of a pnp transistor implemented in a standard CMOS technology utilizing an n-well process.

1. **Identification of Components and Structure:**
- **Emitter (E):** Represented by a p+ region within the n-well. This region is connected to the emitter terminal, marked as 'E'.
- **Base (B):** The n-well serves as the base of the transistor. A separate n+ region within the n-well is connected to the base terminal, marked as 'B'.
- **Collector (C):** The p-type substrate acts as the collector, and a p+ region in the substrate is connected to the collector terminal, marked as 'C'.

2. **Connections and Interactions:**
- The p+ region within the n-well (emitter) injects holes into the n-well (base), which then recombine with electrons. The holes that do not recombine continue to flow into the p-substrate (collector), completing the current path.
- The n-well base is isolated from the p-substrate by the pn junction, allowing control of the transistor operation by modulating the base-emitter voltage.

3. **Labels, Annotations, and Key Features:**
- The diagram includes labels for each terminal (C, E, B) and indicates the type of doping in each region (p+, n+).
- The n-well and p-substrate regions are clearly marked to illustrate the structure of the transistor.
- An arrow on the emitter indicates the conventional current direction, which is from the emitter to the collector in a pnp transistor.

image_name:Figure 12.11 Circuit of Fig. 12.9 implemented with pnp transistors.
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: X}
name: R2, type: Resistor, value: R2, ports: {N1: Y, N2: Vout}
name: R3, type: Resistor, value: R3, ports: {N1: Y, N2: e2}
name: Q1, type: PNP, ports: {C: GND, B: GND, E: X}
name: Q2, type: PNP, ports: {C: GND, B: GND, E: e2}
name: A1, type: OpAmp, value: A1, ports: {InP: X, InN: Y, OutP: Vout, OutN: GND}
]
extrainfo:The circuit is an amplifier using two PNP transistors (Q1 and Q2) and an operational amplifier (A1). The resistors R1, R2, and R3 set the biasing and feedback for the amplifier. The output voltage is taken across Vout.

Op Amp Offset and Output Impedance As explained in Chapter 14, owing to asymmetries, op amps suffer from input "offsets," i.e., the output voltage of the op amp is not zero if the input is set to zero. The input offset voltage of the op amp in Fig. 12.9 introduces error in the output voltage. Included in Fig. 12.12, the effect is quantified as $V_{B E 1}-V_{O S} \approx V_{B E 2}+R_{3} I_{C 2}$ (if $A_{1}$ is large) and $V_{\text {out }}=V_{B E 2}+\left(R_{3}+R_{2}\right) I_{C 2}$. Thus,

$$
\begin{align*}
V_{\text {out }} & =V_{B E 2}+\left(R_{3}+R_{2}\right) \frac{V_{B E 1}-V_{B E 2}-V_{O S}}{R_{3}}  \tag{12.32}\\
& =V_{B E 2}+\left(1+\frac{R_{2}}{R_{3}}\right)\left(V_{T} \ln n-V_{O S}\right) \tag{12.33}
\end{align*}
$$

where we have assumed that $I_{C 2} \approx I_{C 1}$ despite the offset voltage. The key point here is that $V_{O S}$ is amplified by $1+R_{2} / R_{3}$, introducing error in $V_{\text {out }}$. More important, as explained in Chapter $14, V_{O S}$ itself varies with temperature, raising the temperature coefficient of the output voltage.
image_name:Figure 12.12 Effect of op amp offset on the reference voltage.
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: X}
name: R2, type: Resistor, value: R2, ports: {N1: Vout, N2: Y}
name: R3, type: Resistor, value: R3, ports: {N1: Y, N2: e2}
name: Q1, type: PNP, ports: {C: GND, B: GND, E: X}
name: Q2, type: PNP, ports: {C: GND, B: GND, E: e2}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: Y, OutP: Vout}
name: Vos, type: VoltageSource, value: Vos, ports: {Np: C, Nn: InP(A1)}
]
extrainfo:The circuit is a differential amplifier with two PNP transistors and an operational amplifier. The offset voltage Vos is introduced at the inverting input of the op-amp, affecting the output voltage Vout. Resistors R1, R2, and R3 form a network to balance the input and feedback.

#### Example 12.5

Assuming an ideal op amp, determine the small-signal gain from $V_{O S}$ to $V_{\text {out }}$ in Fig. 12.12.

#### Solution

In the absence of the op amp offset, the two diode-connected bipolar transistors carry equal bias currents, exhibiting a transconductance of $g_{m}$. Replacing $Q_{1}$ and $Q_{2}$ with a small-signal resistance equal to $1 / g_{m}$ and noting that $V_{X}-V_{O S} \approx V_{Y}$, we write the following small-signal equation:

$$
\begin{equation*}
\frac{1 / g_{m}}{1 / g_{m}+R_{1}} V_{\text {out }}-V_{O S}=\frac{1 / g_{m}+R_{3}}{1 / g_{m}+R_{3}+R_{2}} V_{\text {out }} \tag{12.34}
\end{equation*}
$$

Since $R_{1}=R_{2}$,

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{O S}}=-\left[1+\frac{1}{g_{m} R_{2}}+\frac{\left(1 / g_{m}+R_{2}\right)^{2}}{R_{2} R_{3}}\right] \tag{12.35}
\end{equation*}
$$

If $g_{m} R_{2} \gg 1$, then $V_{\text {out }} / V_{O S} \approx-\left(1+R_{2} / R_{3}\right)$, agreeing with the results obtained previously. (After all, if $1 / g_{m} \approx 0$, $V_{O S}$ simply sees a noninverting amplifier with a gain of $1+R_{2} / R_{3}$.)

Why does (12.35) not completely agree with the $-\operatorname{Vos}\left(1+R_{2} / R_{3}\right)$ component in (12.33)? Recall that (12.33) was derived with the assumption that $I_{C 1} \approx I_{C 2}$ despite the offset voltage. Since $V_{X}-V_{O S}=V_{Y}$, we have $I_{C 1} R_{1}-V_{O S}=I_{C 2} R_{2}$, and hence $I_{C 1}=I_{C 2}+V_{O S} / R_{2}$. Let us return to (12.32) and write

$$
\begin{align*}
V_{B E 1}-V_{B E 2}-V_{O S} & =V_{T} \ln \frac{I_{C 1}}{I_{S 1}}-V_{T} \ln \frac{I_{C 2}}{I_{S 2}}-V_{O S}  \tag{12.36}\\
& =V_{T} \ln n-V_{T} \ln \frac{I_{C 1}}{I_{C 2}}-V_{O S}  \tag{12.37}\\
& =V_{T} \ln n-V_{T} \ln \left(1+\frac{V_{O S}}{R_{2} I_{C 2}}\right)-V_{O S}  \tag{12.38}\\
& \approx V_{T} \ln n-V_{T} \frac{V_{O S}}{R_{2} I_{C 2}}-V_{O S}  \tag{12.39}\\
& \approx V_{T} \ln n-\left(1+\frac{1}{g_{m} R_{2}}\right) V_{O S} \tag{12.40}
\end{align*}
$$

The output offset contribution therefore amounts to $-\left[1+1 /\left(g_{m} R_{2}\right)\right]\left(1+R_{2} / R_{3}\right) V_{O S}$, which is approximately the same as (12.35).

Several methods are employed to lower the effect of $V_{O S}$. First, the op amp incorporates large devices in a carefully chosen topology so as to minimize the offset (Chapter 19). Second, as illustrated in Fig. 12.7, the collector currents of $Q_{1}$ and $Q_{2}$ can be ratioed by a factor of $m$ such that $\Delta V_{B E}=V_{T} \ln (m n)$. Third, each branch may use two $p n$ junctions in series to double $\Delta V_{B E}$. Figure 12.13 depicts a realization using the last two techniques. Here, $R_{1}$ and $R_{2}$ are ratioed by a factor of $m$, producing $I_{1} \approx m I_{2}$. Neglecting base currents and assuming that $A_{1}$ is large, we can now write $V_{B E 1}+V_{B E 2}-V_{O S}=V_{B E 3}+V_{B E 4}+R_{3} I_{2}$ and $V_{\text {out }}=V_{B E 3}+V_{B E 4}+\left(R_{3}+R_{2}\right) I_{2}$. It follows that

$$
\begin{align*}
V_{\text {out }} & =V_{B E 3}+V_{B E 4}+\left(R_{3}+R_{2}\right) \frac{2 V_{T} \ln (m n)-V_{O S}}{R_{3}}  \tag{12.41}\\
& =2 V_{B E}+\left(1+\frac{R_{2}}{R_{3}}\right)\left[2 V_{T} \ln (m n)-V_{O S}\right] \tag{12.42}
\end{align*}
$$

image_name:Figure 12.13 Reduction of the effect of op amp offset
description:The circuit reduces the effect of op-amp offset voltage by using a configuration involving four PNP transistors (Q1, Q2, Q3, Q4) and resistors (R1, R2, R3). The op-amp A1 is used to control the output voltage Vout. The resistors R1 and R2 form a voltage divider, while R3 is used in the feedback loop to adjust the offset voltage Vos.

Figure 12.13 Reduction of the effect of op amp offset.

Thus, the effect of the offset voltage is reduced by increasing the first term in the square brackets. The issue, however, is that $V_{\text {out }} \approx 2 \times 1.25 \mathrm{~V}=2.5 \mathrm{~V}$, a value difficult to generate by the op amp at low supply voltages.

In the circuits studied above, the op amp drives two resistive branches and must therefore provide a low output impedance. Fortunately, it is possible to avoid this issue by a simple modification described below.

The implementation of Fig. 12.13 is not feasible in a standard CMOS technology because the collectors of $Q_{2}$ and $Q_{4}$ are not grounded. In order to utilize the bipolar structure shown in Fig. 12.10, we modify the series combination of the diodes as illustrated in Fig. 12.14(a), converting one of the diodes to an emitter follower. However, we must ensure that the bias currents of both transistors have the same behavior with temperature. Thus, we bias each transistor by a PMOS current source rather than a resistor [Fig. 12.14(b)]. The overall circuit then assumes the topology shown in Fig. 12.15, where the op amp adjusts the gate voltage of the PMOS devices so as to equalize $V_{X}$ and $V_{Y}$. Interestingly, in this circuit, the op amp experiences no resistive loading, but the mismatch and channel-length modulation of the PMOS devices introduce error at the output (Problem 12.3).
image_name:Figure 12.14 (a)
description:The circuit in Figure 12.14 (a) shows a configuration of PNP transistors Q1 and Q2 with grounded emitters. In Figure 12.14 (b), the transistors are biased by PMOS current sources M1 and M2. The circuit equalizes the voltages at nodes X and 2V_BE using the PMOS devices and a bias voltage Vb. The op amp in the full circuit adjusts the gate voltage of the PMOS to maintain this condition. The main concern is the low current gain of the PNP transistors, which may introduce errors in the emitter currents.
image_name:Figure 12.14 (b)
description:The circuit in Figure 12.14 (b) uses PMOS transistors M1 and M2 to bias the PNP transistors Q1 and Q2. The op amp adjusts the gate voltage to equalize Vx and Vy, minimizing resistive loading. However, mismatch and channel-length modulation in PMOS can introduce errors.

Figure 12.14 (a) Conversion of series diodes to a topology with grounded collectors; (b) circuit of part (a) biased by PMOS current sources.

An important concern in the circuit of Fig. 12.15 is the relatively low current gain of the "native" $p n p$ transistors. Since the base currents of $Q_{2}$ and $Q_{4}$ generate an error in the emitter currents of $Q_{1}$ and $Q_{3}$, a means of base current cancellation may be necessary (Problem 12.5).
image_name:Figure 12.15
description:The circuit is a reference generator incorporating two series base-emitter voltages. It uses PMOS current sources for biasing and includes feedback through an operational amplifier. The circuit is designed to address low current gain issues in PNP transistors by potentially canceling base currents.

Figure 12.15 Reference generator incorporating two series base-emitter voltages.

Feedback Polarity In the circuit of Fig. 12.9, the feedback signal produced by the op amp returns to both of its inputs. The negative-feedback factor is given by

$$
\begin{equation*}
\beta_{N}=\frac{1 / g_{m 2}+R_{3}}{1 / g_{m 2}+R_{3}+R_{2}} \tag{12.43}
\end{equation*}
$$

and the positive-feedback factor by

$$
\begin{equation*}
\beta_{P}=\frac{1 / g_{m 1}}{1 / g_{m 1}+R_{1}} \tag{12.44}
\end{equation*}
$$

To ensure an overall negative feedback, $\beta_{P}$ must be less than $\beta_{N}$, preferably by roughly a factor of two so that the circuit's transient response remains well behaved with large capacitive loads.
Bandgap Reference The voltage generated according to (12.20) is called a "bandgap reference." To understand the origin of this terminology, let us write the output voltage as

$$
\begin{equation*}
V_{R E F}=V_{B E}+V_{T} \ln n \tag{12.45}
\end{equation*}
$$

and hence:

$$
\begin{equation*}
\frac{\partial V_{R E F}}{\partial T}=\frac{\partial V_{B E}}{\partial T}+\frac{V_{T}}{T} \ln n \tag{12.46}
\end{equation*}
$$

Setting this to zero and substituting for $\partial V_{B E} / \partial T$ from (12.13), we have

$$
\begin{equation*}
\frac{V_{B E}-(4+m) V_{T}-E_{g} / q}{T}=-\frac{V_{T}}{T} \ln n \tag{12.47}
\end{equation*}
$$

If $V_{T} \ln n$ is found from this equation and inserted in (12.45), we obtain

$$
\begin{equation*}
V_{R E F}=\frac{E_{g}}{q}+(4+m) V_{T} \tag{12.48}
\end{equation*}
$$

Thus, the reference voltage exhibiting a nominally-zero TC is given by a few fundamental numbers: the bandgap voltage of silicon, $E_{g} / q$, the temperature exponent of mobility, $m$, and the thermal voltage, $V_{T}$. The term "bandgap" is used here because as $T \rightarrow 0, V_{R E F} \rightarrow E_{g} / q$.

#### Example 12.6

Prove directly that, as $T \rightarrow 0, V_{B E} \rightarrow E_{g} / q$, and hence $V_{R E F}=V_{B E}+V_{T} \ln n \rightarrow E_{g} / q$.

#### Solution

From Eq. (12.8), we have

$$
\begin{align*}
V_{B E} & =V_{T} \ln \frac{I_{C}}{I_{S}}  \tag{12.49}\\
& =V_{T}\left[\ln I_{C}-\ln b-(4+m) \ln T+\frac{E_{g}}{k T}\right] \tag{12.50}
\end{align*}
$$

Thus, $V_{B E} \rightarrow E_{g} / q$ if $T \rightarrow 0$ and $I_{C}$ is constant.

Supply Dependence and Start-Up In the circuit of Fig. 12.9, the output voltage is relatively independent of the supply voltage so long as the open-loop gain of the op amp is sufficiently high. The circuit may require a start-up mechanism because if $V_{X}$ and $V_{Y}$ are equal to zero, the input differential pair of the op amp may turn off. Start-up techniques similar to those of Fig. 12.5 can be added to ensure that the op amp turns on when the supply is applied.

The supply rejection of the circuit typically degrades at high frequencies owing to the op amp's rejection properties, often mandating "supply regulation." An example is described in Sec. 12.8.

Curvature Correction If plotted as a function of temperature, bandgap voltages exhibit a finite "curvature," i.e., their TC is typically zero at one temperature and positive or negative at other temperatures (Fig. 12.16). The curvature arises from temperature variation of base-emitter voltages, collector currents, and offset voltages.
image_name:Figure 12.16
description:The graph depicted in Figure 12.16 is a plot of bandgap reference voltage \( V_{REF} \) as a function of temperature \( T \). The graph is a simple 2D plot with the x-axis representing temperature \( T \) and the y-axis representing the reference voltage \( V_{REF} \). There are no specific units or scales provided for the axes, indicating a qualitative representation.

**Overall Behavior and Trends:**
The graph exhibits a concave downward parabolic shape, illustrating the curvature in the temperature dependence of the bandgap voltage. The voltage \( V_{REF} \) increases initially with temperature, reaching a peak at a certain temperature \( T_0 \), and then decreases as temperature continues to rise.

**Key Features and Technical Details:**
- The peak of the curve occurs at temperature \( T_0 \), marked by a vertical dashed line. This point represents the temperature where the temperature coefficient (TC) of the bandgap voltage is zero.
- The curve is symmetric around \( T_0 \), indicating that the voltage changes similarly on either side of this temperature.

**Annotations and Specific Data Points:**
- The graph includes a vertical dashed line at \( T_0 \), highlighting the temperature at which the curvature is centered. This line signifies the zero-TC point, a critical feature in understanding the behavior of bandgap voltages over temperature.

This graph visually demonstrates the challenge in achieving a constant bandgap voltage over varying temperatures due to inherent curvature, which is a key consideration in designing circuits with stable voltage references.

Figure 12.16 Curvature in temperature dependence of a bandgap voltage.

Many curvature correction techniques have been devised to suppress the variation of $V_{R E F}$ [5, 6] in bipolar bandgap circuits, but they are seldom used in CMOS counterparts. This is because, due to large offsets and process variations, samples of a bandgap reference display substantially different zero-TC temperatures (Fig. 12.17), making it difficult to correct the curvature reliably.
image_name:Figure 12.17 Variation of the zero-TC temperature for different samples.
description:The graph in Figure 12.17 is a plot showing the variation of the zero-TC (temperature coefficient) temperature for different samples in a bandgap voltage reference circuit. This is a typical line graph with temperature (T) on the horizontal axis and the reference voltage (V_REF) on the vertical axis. Both axes are likely using linear scales, but specific units are not provided.

The graph displays multiple curves, each representing a different sample. These curves exhibit a bell-shaped or parabolic trend, indicating that the reference voltage first increases with temperature, reaches a peak, and then decreases. This shape demonstrates the curvature in the temperature dependence of the bandgap voltage.

The overall behavior shows that the zero-TC temperature, where the temperature coefficient is minimal or zero, varies across different samples. This variation is depicted by the different positions of the peaks along the temperature axis, suggesting that each sample has a distinct zero-TC temperature.

Key features of the graph include the peaks of each curve, which represent the zero-TC temperatures for the respective samples. These peaks are not labeled with specific values, but their horizontal spread indicates substantial sample-to-sample variation. This variability is a critical aspect of the graph, highlighting challenges in achieving consistent zero-TC temperatures across different samples in CMOS bandgap references.

Figure 12.17 Variation of the zero-TC temperature for different samples.

## 12.4 ■ PTAT Current Generation

In the analysis of bandgap circuits, we noted that the bias currents of the bipolar transistors are in fact proportional to absolute temperature. Useful in many applications, PTAT currents can be generated by a topology such as that shown in Fig. 12.18. Alternatively, we can combine the supply-independent biasing scheme of Fig. 12.2 with a bipolar core, arriving at Fig. 12.19. ${ }^{3}$ Assuming for simplicity that $M_{1}-M_{2}$ and $M_{3}-M_{4}$ are identical pairs, we note that for $I_{D 1}=I_{D 2}$, the circuit must ensure that $V_{X}=V_{Y}$. Thus, $I_{D 1}=I_{D 2}=\left(V_{T} \ln n\right) / R_{1}$, yielding the same behavior for $I_{D 5}$. In practice, due to mismatches between the transistors and, more important, the temperature coefficient of $R_{1}$, the variation of $I_{D 5}$ deviates from the ideal equation. For low-voltage operation, the topology of Fig. 12.18 is preferred.
image_name:Figure 12.18 Generation of a PTAT current.
description:This circuit generates a PTAT (Proportional To Absolute Temperature) current. It uses an op-amp and a combination of PMOS and NMOS transistors, along with PNP transistors and a resistor, to produce a current that is proportional to temperature. The circuit is designed for low-voltage operation.
image_name:Figure 12.19 Alternative method of generating a PTAT current.
description:The circuit in Figure 12.19 is an alternative method for generating a PTAT (Proportional To Absolute Temperature) current. It involves a differential pair of NMOS transistors (M1 and M2) and a current mirror formed by PMOS transistors (M3, M4, and M5). The PNP transistors (Q1 and Q2) are used for biasing. The operational amplifier (A0) stabilizes the current through feedback.

The circuit of Fig. 12.18 can be readily modified to provide a bandgap reference voltage as well. Illustrated in Fig. 12.20, the idea is to add a PTAT voltage $I_{D 5} R_{2}$ to a base-emitter voltage. The output therefore equals

$$
\begin{equation*}
V_{R E F}=\left|V_{B E 3}\right|+\frac{R_{2}}{R_{1}} V_{T} \ln n \tag{12.51}
\end{equation*}
$$

image_name:Figure 12.20 Generation of a temperature-independent voltage
description:The circuit generates a temperature-independent voltage using a bandgap reference. PMOS transistors M3, M4, and M5 are used for current mirroring. PNP transistors Q1, Q2, and Q3 are involved in generating the base-emitter voltage terms. Resistors R1 and R2 are used to scale the PTAT voltage.

Figure 12.20 Generation of a temperature-independent voltage.
where all of the PMOS transistors are assumed identical. Note that the value of $V_{B E 3}$ and hence the size of $Q_{3}$ are somewhat arbitrary so long as the sum of the two terms in (12.51) gives a zero TC. In reality, mismatches of the PMOS devices introduce error in $V_{\text {out }}$.

## 12.5 ■ Constant $-G_{m}$ Biasing

The transconductance of MOSFETs plays a critical role in analog circuits, determining such performance parameters as noise, small-signal gain, and speed. For this reason, it is often desirable to bias the transistors such that their transconductance does not depend on the temperature, process, or supply voltage.

A simple circuit used to define the transconductance is the supply-independent bias topology of Fig. 12.3. Recall that the bias current is given by

$$
\begin{equation*}
I_{\text {out }}=\frac{2}{\mu_{n} C_{o x}(W / L)_{N}} \frac{1}{R_{S}^{2}}\left(1-\frac{1}{\sqrt{K}}\right)^{2} \tag{12.52}
\end{equation*}
$$

Thus, the transconductance of $M_{1}$ equals

$$
\begin{align*}
g_{m 1} & =\sqrt{2 \mu_{n} C_{o x}\left(\frac{W}{L}\right)_{N} I_{D 1}}  \tag{12.53}\\
& =\frac{2}{R_{S}}\left(1-\frac{1}{\sqrt{K}}\right) \tag{12.54}
\end{align*}
$$

a value independent of the supply voltage and MOS device parameters.
In reality, the value of $R_{S}$ in (12.54) does vary with temperature and process. If the temperature coefficient of the resistor is known, bandgap and PTAT reference generation techniques can be utilized to cancel the temperature dependence. Process variations, however, limit the accuracy with which $g_{m 1}$ is defined.

In systems where a precise clock frequency is available, the resistor $R_{S}$ in Fig. 12.3 can be replaced by a switched-capacitor equivalent (Chapter 13) to achieve a somewhat higher accuracy. Depicted in Fig. 12.21, the idea is to establish an average resistance equal to $\left(C_{S} f_{C K}\right)^{-1}$ between the source of $M_{2}$ and ground, where $f_{C K}$ denotes the clock frequency. Capacitor $C_{B}$ is added to shunt the high-frequency components resulting from switching to ground. Since the absolute value of capacitors is typically more tightly controlled and since the TC of capacitors is much smaller than that of resistors, this technique provides a higher reproducibility in the bias current and transconductance.
image_name:Figure 12.21 Constant- $G_{m}$ biasing by means of a switched-capacitor "resistor."
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Y, G: Y}
name: M2, type: NMOS, ports: {S: s2, D: X, G: Y}
name: M3, type: PMOS, ports: {S: VDD, D: Y, G: X}
name: M4, type: PMOS, ports: {S: VDD, D: X, G: X}
name: CB, type: Capacitor, value: CB, ports: {Np: X, Nn: GND}
name: CS, type: Capacitor, value: CS, ports: {Np: Z, Nn: GND}
name: S1, type: Switch, ports: {N1: s2, N2: Z}
name: S2, type: Switch, ports: {N1: Z, N2: GND}
]
extrainfo:The circuit implements a constant-Gm biasing using a switched-capacitor technique. The switched-capacitor network (S1, S2, CS) emulates a resistor RS. Capacitor CB shunts high-frequency components to ground.

The switched-capacitor approach of Fig. 12.21 can be applied to other circuits as well. For example, as shown in Fig. 12.22, a voltage-to-current converter with a relatively high accuracy can be constructed.
image_name:Figure 12.22 Voltage-to-current conversion by means of a switched-capacitor resistor.
description:
[
name: A0, type: OpAmp, value: A0, ports: {InP: VREF, InN: Inn(A0), OutP: Out(A0)}
name: M1, type: NMOS, ports: {S: InN(A0), D: LOAD1, G: Out(A0)}
name: CB, type: Capacitor, value: CB, ports: {Np: Inn(A0), Nn: GND}
name: S1, type: Switch, ports: {N1: Inn(A0), N2: x}
name: S2, type: Switch, ports: {N1: x, N2: GND}
]
extrainfo:The circuit uses a switched-capacitor network to emulate a resistor and achieves voltage-to-current conversion with a constant-Gm biasing technique. The NMOS transistor M1 is used to control the output current IREF.

## 12.6 ■ Speed and Noise Issues

Even though reference generators are low-frequency circuits, they may affect the speed of the circuits that they feed. Furthermore, various building blocks may experience "crosstalk" through reference lines. These difficulties arise because of the finite output impedance of reference voltage generators, especially if they incorporate op amps. As an example, let us consider the configuration shown in Fig. 12.23, assuming that the voltage at node $N$ is heavily disturbed by the circuit fed by $M_{5}$. For fast changes in $V_{N}$, the op amp cannot maintain $V_{P}$ constant, and the bias currents of $M_{5}$ and $M_{6}$ experience large transient changes. Also, the duration of the transient at node $P$ may be quite long if the op amp suffers from a slow response. For this reason, many applications may require a high-speed op amp in the reference generator.

In systems where the power consumed by the reference circuit must be small, the use of a high-speed op amp may not be feasible. Alternatively, the critical node, e.g., node $P$ in Fig. 12.23, can be bypassed to ground by means of a large capacitor $\left(C_{B}\right)$ so as to suppress the effect of external disturbances. This approach involves two issues. First, the stability of the op amp must not degrade with the addition of the capacitor, requiring the op amp to be of a one-stage nature (Chapter 10). Second, since $C_{B}$ generally slows down the transient response of the op amp, its value must be much greater than the capacitance that couples the disturbance to node $P$. As illustrated in Fig. 12.24, if $C_{B}$ is not sufficiently large, then $V_{P}$
image_name:Figure 12.23 Effect of circuit transients on reference voltages and currents
description:The circuit is a reference generator affected by transients, with a bypass capacitor CB to suppress disturbances. The NMOS transistors M5 and M6 are used to control the flow of current, and the resistor R1 is connected to node B.

image_name:Figure 12.24 Effect of increasing bypass capacitor on the response of a reference generator
description:The graph in Figure 12.24 is a time-domain waveform that illustrates the effect of increasing the bypass capacitor (C_B) on the response of a reference generator. The horizontal axis represents time (t), while the vertical axis represents the voltage at node V_P.

The graph contains three distinct curves, each corresponding to different sizes of the bypass capacitor: C_B1, C_B2, and C_B3, with C_B1 being the smallest and C_B3 the largest. The curves show the transient response of the reference voltage when a disturbance occurs.

- **C_B1 (smallest capacitor):** The curve exhibits a significant dip, indicating a large transient response with a deep and prolonged deviation from the initial value. This implies that the reference voltage is less stable and takes longer to return to its steady state.

- **C_B2 (medium capacitor):** The curve shows a moderate dip, with a reduced magnitude and duration of the transient response compared to C_B1. This indicates improved stability and faster recovery.

- **C_B3 (largest capacitor):** The curve is the most stable, with the smallest and shortest transient response. The voltage deviation is minimal, and it returns to its steady state rapidly, demonstrating enhanced stability.

The graph effectively demonstrates that increasing the size of the bypass capacitor enhances the stability of the reference voltage by reducing both the magnitude and duration of the transient response. The trade-off highlighted here is that while larger capacitors improve stability, they may also slow down the circuit's ability to respond quickly to changes, as indicated by the smoother, less agile response with very large C_B.

Figure 12.24 Effect of increasing bypass capacitor on the response of a reference generator.
experiences a change and takes a long time to return to its original value, possibly degrading the settling speed of the circuits biased by the reference generator. In other words, depending on the environment, it may be preferable to leave node $P$ agile so that it can quickly recover from transients. In general, as depicted in Fig. 12.25, the response of the circuit must be analyzed by applying a disturbance at the output and observing the settling behavior.
image_name:Figure 12.25 Setup for testing the transient response of a reference generator.
description：The circuit tests the transient response of a reference generator by applying a disturbance at the output (Vout) and observing the settling behavior.

#### Example 12.7

Determine the small-signal output impedance of the bandgap reference shown in Fig. 12.23 and examine its behavior with frequency.

#### Solution

Figure 12.26 depicts the equivalent circuit, modeling the open-loop op amp by a one-pole transfer function $A(s)=$ $A_{0} /\left(1+s / \omega_{0}\right)$ and an output resistance $R_{\text {out }}$ and each bipolar transistor by a resistance $1 / g_{m N}$. If $M_{1}$ and $M_{2}$ are identical, each having a transconductance of $g_{m P}$, then their drain currents are equal to $g_{m P} V_{X}$, producing a differential voltage at the input of the op amp equal to

$$
\begin{align*}
V_{A B} & =-g_{m P} V_{X} \frac{1}{g_{m N}}+g_{m P} V_{X}\left(\frac{1}{g_{m N}}+R_{1}\right)  \tag{12.55}\\
& =g_{m P} V_{X} R_{1} \tag{12.56}
\end{align*}
$$

image_name:Figure 12.26 Circuit for calculation of the output impedance of a reference generator.
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: A, G: P}
name: M2, type: PMOS, ports: {S: VDD, D: B, G: P}
name: Rout, type: Resistor, value: Rout, ports: {N1: P, N2: Out(A(s))}
name: A(s), type: OpAmp, value: A(s), ports: {InP: B, InN: A, Out: Out(A(s))}
name: 1/gmN, type: Resistor, value: 1/gmN, ports: {N1: A, N2: GND}
name: 1/gmN + R1, type: Resistor, value: 1/gmN + R1, ports: {N1: B, N2: GND}
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Vx(P), Nn: GND}
]
extrainfo:The circuit is designed to analyze the output impedance of a reference generator. It involves PMOS transistors, resistors, an operational amplifier, and a voltage source. The PMOS transistors M1 and M2 are identical, contributing to the differential voltage at the op-amp input. The current Ix flows through the output resistance Rout, influenced by the transconductance gmP and the op-amp gain A(s).

The current flowing through $R_{\text {out }}$ is therefore given by

$$
\begin{equation*}
I_{X}=\frac{V_{X}+g_{m P} V_{X} R_{1} A(s)}{R_{\text {out }}} \tag{12.57}
\end{equation*}
$$

yielding

$$
\begin{align*}
\frac{V_{X}}{I_{X}} & =\frac{R_{\text {out }}}{1+g_{m P} R_{1} A(s)}  \tag{12.58}\\
& =\frac{R_{\text {out }}}{1+g_{m P} R_{1} \frac{A_{0}}{1+s / \omega_{0}}}  \tag{12.59}\\
& =\frac{R_{\text {out }}}{1+g_{m P} R_{1} A_{0}} \frac{1+\frac{s}{\omega_{0}}}{1+\frac{s}{\left(1+g_{m P} R_{1} A_{0}\right) \omega_{0}}} \tag{12.60}
\end{align*}
$$

Thus, the output impedance exhibits a zero at $\omega_{0}$ and a pole at $\left(1+g_{m P} R_{1} A_{0}\right) \omega_{0}$, with the magnitude behavior plotted in Fig. 12.27. Note that $\left|Z_{\text {out }}\right|$ is small for $\omega<\omega_{0}$, but it rises to a high value as the frequency approaches the pole. In fact, setting $\omega=\left(1+g_{m P} R_{1} A_{0}\right) \omega_{0}$ and assuming $g_{m P} R_{1} A_{0} \gg 1$, we have

$$
\begin{align*}
\left|Z_{\text {out }}\right| & =\frac{R_{\text {out }}}{1+g_{m P} R_{1} A_{0}}\left|\frac{1+j\left(1+g_{m P} R_{1} A_{0}\right)}{1+j}\right|  \tag{12.61}\\
& =\frac{R_{\text {out }}}{\sqrt{2}} \tag{12.62}
\end{align*}
$$

which is only $30 \%$ lower than the open-loop value.
image_name:Figure 12.27 Variation of the reference generator output impedance with frequency
description:The graph in Figure 12.27 is a plot illustrating the variation of the reference generator output impedance with frequency. It appears to be a Bode plot focusing on the magnitude of the impedance.

1. **Type of Graph and Function**:
- This is a magnitude plot showing the behavior of the output impedance of a reference generator across different frequencies.

2. **Axes Labels and Units**:
- The horizontal axis represents frequency (denoted by \( \omega \)), though the units are not explicitly mentioned, it is typically in radians per second or hertz.
- The vertical axis represents the magnitude of the output impedance \( |Z_{\text{out}}| \).
- Significant points on the frequency axis include \( \omega_0 \) and \((1 + g_{mP} R_1 A_0) \omega_0\).
- The vertical axis has marked values of \( \frac{R_{\text{out}}}{1 + g_{mP} R_1 A_0} \) and \( \frac{R_{\text{out}}}{\sqrt{2}} \).

3. **Overall Behavior and Trends**:
- The graph starts at a low impedance value \( \frac{R_{\text{out}}}{1 + g_{mP} R_1 A_0} \) at low frequencies.
- As the frequency increases towards \( \omega_0 \), the impedance begins to rise.
- The impedance continues to rise and levels off at a higher value of \( \frac{R_{\text{out}}}{\sqrt{2}} \) as the frequency approaches \((1 + g_{mP} R_1 A_0) \omega_0\).

4. **Key Features and Technical Details**:
- There is a significant increase in impedance as the frequency approaches the pole at \((1 + g_{mP} R_1 A_0) \omega_0\).
- The impedance at high frequencies is only about 30% lower than the open-loop value, indicating a substantial rise from the initial value at low frequencies.

5. **Annotations and Specific Data Points**:
- The graph includes dashed lines marking the significant frequencies \( \omega_0 \) and \((1 + g_{mP} R_1 A_0) \omega_0\).
- The impedance levels at these critical points are explicitly noted, providing clear reference values for analysis.

The output noise of reference generators may affect the performance of low-noise circuits considerably. Figure 12.28 illustrates an example: the load current source of a common-source stage is driven by a bandgap circuit with a current multiplication factor of $N$. Thus, the noise current of $M_{1}$ (or $M_{2}$ ) is amplified by the same factor as it appears in $M_{3}$. Note that $M_{1}-M_{3}$ carry noise due to the op amp $A_{1}$ as well.
image_name:Figure 12.28 Effect of bandgap circuit noise on a CS stage.
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: X, G: Out(A1)}
name: M2, type: PMOS, ports: {S: VDD, D: Y, G: Out(A1)}
name: M3, type: PMOS, ports: {S: VDD, D: Vout, G: Out(A1)}
name: M4, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: R1, type: Resistor, value: R1, ports: {N1: Y, N2: e2}
name: A1, type: OpAmp, value: A1, ports: {InP: Y, InN: X, OutP: Out(A1)}
name: Q1, type: PNP, ports: {C: GND, B: GND, E: X}
name: Q2, type: PNP, ports: {C: GND, B: GND, E: e2}
]
extrainfo:The circuit diagram represents a common-source stage driven by a bandgap circuit. The op amp A1 amplifies the difference between nodes X and Y, and the PMOS transistors M1, M2, and M3 form a current mirror. NMOS transistor M4 acts as a load transistor. The resistors and transistors contribute to the amplification and noise characteristics of the circuit.

As another example, if a high-precision A/D converter employs a bandgap voltage as the reference with which the analog input signal is compared (Fig. 12.29), then the noise in the reference is directly added to the input.
image_name:Figure 12.29 A/D converter using a reference generator
description:The system block diagram labeled "Figure 12.29 A/D converter using a reference generator" consists of two main components: a Reference Generator and an A/D Converter.

1. **Main Components:**
- **Reference Generator:** This block generates a stable reference voltage or current, which is used as a benchmark for the analog-to-digital conversion process.
- **A/D Converter (Analog-to-Digital Converter):** This block converts the analog input signal, denoted as \( V_{in} \), into a digital output signal. The digital output is typically a binary representation of the input analog signal.

2. **Flow of Information or Control:**
- The analog input signal \( V_{in} \) is fed into the A/D Converter. Simultaneously, the Reference Generator provides a reference signal to the A/D Converter.
- The A/D Converter uses the reference signal from the Reference Generator to accurately convert the analog input \( V_{in} \) into a digital output. The flow of information is primarily unidirectional, from input to output, without any feedback loops indicated in the diagram.

3. **Labels, Annotations, and Key Indicators:**
- The input to the system is labeled as \( V_{in} \), indicating the point where the analog signal enters the system.
- The output of the A/D Converter is labeled as "Digital Output," indicating the conversion result.

4. **Overall System Function:**
- The primary function of this system is to convert an analog input signal into a digital format. The Reference Generator ensures that the conversion process is accurate by providing a stable reference signal to the A/D Converter. This setup is crucial for applications requiring precise digital representations of analog signals, such as in high-precision measurement systems or digital communication interfaces.

Figure 12.29 A/D converter using a reference generator.

As a simple example, let us calculate the output noise voltage of the circuit shown in Fig. 12.30, taking into account only the input-referred noise voltage of the op amp, $V_{n, o p}$. Since the small-signal drain currents of $M_{1}$ and $M_{2}$ are equal to $V_{n, \text { out }} /\left(R_{1}+g_{m N}^{-1}\right)$, we have $V_{P}=-g_{m P}^{-1} V_{n, \text { out }} /\left(R_{1}+g_{m N}^{-1}\right)$, obtaining the differential voltage at the input of the op amp as $-g_{m P}^{-1} A_{0}^{-1} V_{n, \text { out }} /\left(R_{1}+g_{m N}^{-1}\right)$. Beginning
image_name:Figure 12.30 Circuit for calculation of noise in a reference generator.
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: A, G: P}
name: M2, type: PMOS, ports: {S: VDD, D: B, G: P}
name: Ao, type: OpAmp, value: Ao, ports: {InP: InP(A0), InN: A, Out: P}
name: Vn,op, type: VoltageSource, value: Vn,op, ports: {Np: InP(A0), Nn: B}
name: 1/gmN, type: Resistor, value: 1/gmN, ports: {N1: A, N2: GND}
name: 1/(gmN) +R1, type: Resistor, value: 1/(gmN) + R1, ports: {N1: B, N2: Vn,out'}
]
extrainfo:The circuit is a reference generator focusing on input-referred noise voltage of the op amp. It uses two PMOS transistors (M1 and M2) and an operational amplifier (Ao) to manage noise levels. The resistors are used for biasing and feedback.

from node $A$, we can then write

$$
\begin{equation*}
\frac{V_{n, \text { out }}}{R_{1}+g_{m N}^{-1}} \cdot \frac{1}{g_{m N}}-\frac{V_{n, \text { out }}}{g_{m P} A_{0}\left(R_{1}+g_{m N}^{-1}\right)}=V_{n, \text { op }}+V_{n, \text { out }} \tag{12.63}
\end{equation*}
$$

and hence

$$
\begin{equation*}
V_{n, \text { out }}\left[\frac{1}{R_{1}+g_{m N}^{-1}}\left(\frac{1}{g_{m N}}-\frac{1}{g_{m P} A_{0}}\right)-1\right]=V_{n, \text { op }} \tag{12.64}
\end{equation*}
$$

Since typically $g_{m P} A_{0} \gg g_{m N} \gg R_{1}^{-1}$,

$$
\begin{equation*}
\left|V_{n, \text { out }}\right| \approx V_{n, \text { op }} \tag{12.65}
\end{equation*}
$$

suggesting that the noise of the op amp directly appears at the output. Note that even the addition of a large capacitor from the output to ground may not suppress low-frequency $1 / f$ noise components, a serious difficulty in low-noise applications. The noise contributed by other devices in the circuit is studied in Problem 12.6.

#### Example 12.8

If the op amp in Fig. 12.32(c) has an input-referred offset voltage, $V_{O S}$, determine $V_{B G}$.
image_name:Figure 12.33
description:
[
name: M3, type: PMOS, ports: {S: VDD, D: X, G: Out(A1)}
name: M4, type: PMOS, ports: {S: VDD, D: Y, G: Out(A1)}
name: M5, type: PMOS, ports: {S: VDD, D: VBG, G: Out(A1)}
name: R1, type: Resistor, value: R1, ports: {N1: Y, N2: e2}
name: R2, type: Resistor, value: R2, ports: {N1: Y, N2: GND}
name: R3, type: Resistor, value: R3, ports: {N1: X, N2: GND}
name: R4, type: Resistor, value: R4, ports: {N1: VBG, N2: GND}
name: Q1, type: PNP, ports: {C: GND, B: GND, E: X}
name: Q2, type: PNP, ports: {C: GND, B: GND, E: e2}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: X, OutP: Out(A1)}
name: Vos, type: VoltageSource, value: Vos, ports: {Np: InP(A1), Nn: Y}
]
extrainfo:The circuit includes a differential amplifier configuration with an op-amp, two PNP transistors, and PMOS transistors for current mirroring. The voltage source Vos introduces an offset voltage between nodes X and Y. Resistors R1 and R2 are connected to ground, providing biasing for the PNP transistors. The op-amp output is connected to the gates of the PMOS transistors, controlling their conduction.

#### Solution

As shown in Fig. 12.33, we now have $V_{X} \approx V_{Y}+V_{O S} \approx\left|V_{B E 1}\right|$ and

$$
\begin{equation*}
I_{C 1}+\frac{\left|V_{B E 1}\right|}{R_{3}}=I_{C 2}+\frac{\left|V_{B E 1}\right|-V_{O S}}{R_{2}} \tag{12.70}
\end{equation*}
$$

which implies that $I_{C 1}=I_{C 2}-V_{O S} / R_{2}$ if $R_{2}=R_{3}$. Since $\left|V_{B E 1}\right|=\left|V_{B E 2}\right|+R_{1} I_{C 2}+V_{O S}$, we have $I_{C 2}=$ $\left(V_{T} \ln n-V_{O S}\right) / R_{1}$. This current and the current flowing through $R_{2},\left(\left|V_{B E 1}\right|-V_{O S}\right) / R_{2}$, add up to $\left|I_{D 4}\right|$ :

$$
\begin{equation*}
\left|I_{D 4}\right|=\frac{V_{T} \ln n-V_{O S}}{R_{1}}+\frac{\left|V_{B E 1}\right|-V_{O S}}{R_{2}} \tag{12.71}
\end{equation*}
$$

It follows that

$$
\begin{equation*}
V_{B G}=\frac{R_{4}}{R_{2}}\left(\left|V_{B E 1}\right|+\frac{R_{2}}{R_{1}} V_{T} \ln n\right)-\frac{R_{4}}{R_{1}| | R_{2}} V_{O S} \tag{12.72}
\end{equation*}
$$

revealing that the op amp offset is amplified by a factor of $R_{4} /\left(R_{1} \| R_{2}\right)$. Alternatively, we can write

$$
\begin{equation*}
V_{B G}=\frac{R_{4}}{R_{2}}\left[\left|V_{B E 1}\right|+\frac{R_{2}}{R_{1}} V_{T} \ln n-\left(1+\frac{R_{2}}{R_{1}}\right) V_{O S}\right] \tag{12.73}
\end{equation*}
$$

concluding that the effect of $V_{O S}$ can be minimized only by maximizing $n$.

It is instructive to estimate the lowest supply voltage with which the circuit of Fig. 12.32(c) can operate properly. With large bipolar transistors and a small bias current, e.g., $10 \mu \mathrm{~A}$, the base-emitter voltage can be as low as 0.7 V . Similarly, wide PMOS devices allow a $\left|V_{D S}\right|$ of about 50 mV . The circuit can thus operate with a minimum $V_{D D}$ of around 0.75 V . In this case, $R_{4}$ tends to be a large resistor, e.g., $50 \mathrm{k} \Omega$, producing significant noise and requiring a bypass capacitor at the output. Also, if the PMOS drain currents are copied to generate a larger current, say, 0.5 mA , then their noise is amplified by the same factor. This noise contains thermal and flicker components due to the PMOS devices and the noise of the op amp. In Problem 12.24, we analyze the noise behavior of this circuit, but from Example 12.8, we observe that the op amp input noise is amplified by a factor of $R_{4} /\left(R_{1} \| R_{2}\right)$.

The op amp in Fig. 12.32(c) can be realized as a five-transistor OTA. Depicted in Fig. 12.34(a) is an example. The OTA design proceeds according to the following guidelines. (1) Large transistor dimensions are chosen so as to minimize their flicker noise and offset. (2) The gate-source voltage of $M_{a}$ and $M_{b}$
image_name:(a)
description:The circuit is a low-voltage bandgap reference circuit using a five-transistor operational transconductance amplifier (OTA). It incorporates a start-up mechanism to ensure that the circuit does not remain in an off state. The PMOS transistors M3 and M4 are used to provide current to the nodes X and Y. The NMOS transistors Mc and Md form a differential pair, while Ma and Mb are used for additional current control. The bipolar junction transistors Q1 and Q2 are part of the biasing and reference generation network. Resistors R1, R2, and R3 set up the necessary voltage drops and biasing conditions.
image_name:(b) addition of start-up device.
description:This is a low-voltage bandgap reference circuit using a five-transistor OTA with a start-up device. The circuit employs PMOS and NMOS transistors, NPN transistors, and resistors to achieve a stable reference voltage. The start-up mechanism ensures proper operation by preventing the circuit from staying in an off state.

Figure 12.34 (a) Implementation of low-voltage BG circuit using a five-transistor OTA, and (b) addition of start-up device.
plus the headroom required by $I_{S S}$ must not exceed $\left|V_{B E 1}\right|$. (3) The transistors are chosen long enough to yield a reasonable loop gain, e.g., 5 to 10 .

The foregoing topology must incorporate a start-up mechanism. Otherwise, the circuit begins with $V_{X}=V_{Y}=0, M_{a}$ and $M_{b}$ remain off, and so do $M_{3}$ and $M_{4}$. Since, with $V_{D D}<1 \mathrm{~V}$, the voltage difference between node $P$ and node $X$ is initially positive but finally negative (why?), we can tie a diode-connected NMOS transistor between these two nodes to ensure start-up [Fig. 12.34(b)]. Alternatively, the NMOS device can be connected between $X$ and $V_{D D}$.

Another low-voltage bandgap circuit can be derived from the topology of Fig. 12.20 by simply tying a resistor from the output node to ground [9]. Shown in Fig. 12.35, the circuit now allows some of $I_{D 5}$ to flow through $R_{3}$ :

$$
\begin{equation*}
\left|I_{D 5}\right|=\frac{V_{\text {out }}}{R_{3}}+\frac{V_{\text {out }}-\left|V_{B E 3}\right|}{R_{2}} \tag{12.74}
\end{equation*}
$$

If the PMOS devices are identical, $\left|I_{D 5}\right|=V_{T} \ln n / R_{1}$, yielding

$$
\begin{equation*}
V_{\text {out }}=\frac{R_{3}}{R_{2}+R_{3}}\left(\left|V_{B E 3}\right|+\frac{R_{2}}{R_{1}} V_{T} \ln n\right) \tag{12.75}
\end{equation*}
$$

The standard bandgap voltage is thus scaled down by a factor of $R_{3} /\left(R_{2}+R_{3}\right)$. The reader is encouraged to compute the effect of the op amp offset at the output and compare the result with (12.72).
image_name:Figure 12.35 Alternative low-voltage BG circuit.
description:This circuit is an alternative low-voltage bandgap reference circuit. It uses NMOS transistors M3, M4, and M5 to control the current flow. The op-amp A1 is used to stabilize the voltage across the transistors. The resistors R1, R2, and R3 set the output voltage Vout, which is a scaled version of the standard bandgap voltage. The NPN transistors Q1, Q2, and Q3 are used for current mirroring and biasing. The circuit is designed for high-precision analog systems.

It is possible to add other bias branches to the foregoing circuits so as to provide curvature correction, but such schemes typically rely on trimming because the various mismatches within the circuit tend to shift the zero-TC temperature randomly. Other low-voltage bandgaps are described in [10].

## 12.8 ■ Case Study

In this section, we study a bandgap reference circuit designed for high-precision analog systems [7]. The reference generator incorporates the topology of Fig. 12.19, but with two series base-emitter voltages in each branch so as to reduce the effect of MOSFET mismatches. A simplified version of the core is depicted in Fig. 12.36, where the PMOS current mirror arrangement ensures equal collector currents for $Q_{1}-Q_{4}$. While requiring a high supply voltage, this design exemplifies issues that prove important in practice.
image_name:Figure 12.36 Simplified core of the bandgap circuit reported in [7].
description:The circuit is a simplified core of a bandgap reference circuit. It uses a PMOS current mirror arrangement to ensure equal collector currents for Q1-Q4. The design requires a high supply voltage and addresses MOSFET mismatch issues by incorporating two series base-emitter voltages in each branch.

Channel-length modulation of the MOS devices in Fig. 12.36 still results in significant supply dependence. To resolve this issue, each branch can employ both NMOS and PMOS cascode topologies. Figure 12.37(a) shows an example in which the low-voltage cascode current mirror described in Chapter 5
image_name:Figure 12.37 (a)
description:The circuit in Figure 12.37 (a) shows a cascode topology to improve supply rejection. It incorporates resistors R1, R2, and R3, along with NPN transistors Q1 and Q2. The design aims to mitigate the effects of channel-length modulation by using cascode structures.
image_name:Figure 12.37 (b)
description:The circuit diagram in Figure 12.37(b) shows a self-biased cascode configuration aimed at eliminating the need for external bias voltages Vb1 and Vb2. It utilizes resistors R2 and R3 along with current sources I1 and I2 to maintain the biasing. The circuit is designed to improve supply rejection and provide a floating reference voltage.

Figure 12.37 (a) Addition of cascode devices to improve supply rejection; (b) use of self-biased cascode to eliminate $V_{b 1}$ and $V_{b 2}$.

image_name:Figure 12.38 Generation of a floating reference voltage.
description:The circuit diagram in Figure 12.38 generates a floating reference voltage using a self-biased cascode configuration. It utilizes resistors R2 and R3 along with NMOS transistors to maintain biasing, improving supply rejection. The op-amp A1 provides the output voltage Vout, with feedback through resistors R4 and R5.

is utilized. To obviate the need for $V_{b 1}$ and $V_{b 2}$, this design actually introduces a "self-biased" cascode, shown in Fig. 12.37 (b), where $R_{2}$ and $R_{3}$ sustain proper voltages to allow all MOSFETs to remain in saturation. This cascode topology is analyzed in Problem 12.7.

The bandgap circuit reported in [7] is designed to generate a floating reference. This is accomplished by the modification shown in Fig. 12.38, where the drain currents of $M_{9}$ and $M_{10}$ flow through $R_{4}$ and $R_{5}$, respectively. Note that $M_{11}$ sets the gate voltage of $M_{9}$ at $V_{B E 4}+V_{G S 11}$, establishing a voltage equal to $V_{B E 4}$ across $R_{6}$ if $M_{9}$ and $M_{11}$ are identical. Thus, $I_{D 9}=V_{B E 4} / R_{6}$, yielding $V_{R 4}=V_{B E 4}\left(R_{4} / R_{6}\right)$. Also, if $M_{10}$ is identical to $M_{2}$, then $\left|I_{D 10}\right|=2\left(V_{T} \ln n\right) / R_{1}$, and hence $V_{R 5}=2\left(V_{T} \ln n\right)\left(R_{5} / R_{1}\right)$. Since the op amp ensures that $V_{E} \approx V_{F}$, we have

$$
\begin{equation*}
V_{\text {out }}=\frac{R_{4}}{R_{6}} V_{B E 4}+2 \frac{R_{5}}{R_{1}} V_{T} \ln n \tag{12.76}
\end{equation*}
$$

Proper choice of the resistor ratios and $n$ therefore provides a zero temperature coefficient.
In order to further enhance the supply rejection, this design regulates the supply voltage of the core and the op amp. Illustrated in Fig. 12.39, the idea is to generate a local supply, $V_{D D L}$, that is defined by a reference $V_{R 1}$ and the ratio of $R_{r 1}$ and $R_{r 2}$ and hence remains relatively independent of the global supply voltage. But how is $V_{R 1}$ itself generated? To minimize the dependence of $V_{R 1}$ upon the supply,

image_name:Figure 12.39
description:The circuit regulates the supply voltage of the core and op amp to improve supply rejection by generating a local supply VDDL defined by a reference VR1 and the ratio of Rr1 and Rr2.

Figure 12.39 Regulation of the supply voltage of the core and op amp to improve supply rejection.
this voltage is established inside the core, as depicted in Fig. 12.40. In fact, $R_{M}$ is chosen such that $V_{R 1}$ is a bandgap reference.

Figure 12.41 shows the overall implementation, omitting a few details for simplicity. A start-up circuit is also used. Operating from a $5-\mathrm{V}$ supply, the reference generator produces a $2.00-\mathrm{V}$ output while consuming 2.2 mW . The supply rejection is 94 dB at low frequencies, dropping to 58 dB at $100 \mathrm{kHz}[7]$.
image_name:Figure 12.40 Generation of $V_{R 1}$, used in Fig. 12.39.
description:The circuit in Figure 12.40 is a bandgap reference generator. It uses a combination of bipolar junction transistors (BJTs) and MOSFETs to produce a stable reference voltage. The op-amp A1 provides feedback, and the resistors R4 and R5 set the gain. The circuit operates from a supply voltage VDDL. The bandgap reference voltage is used to ensure stability across temperature variations.

image_name:Figure 12.41 Overall circuit of the bandgap generator reported in [7].
description::The circuit in Figure 12.41 is a bandgap reference generator using BJTs and MOSFETs to produce a stable reference voltage. The op-amp A1 provides feedback, and resistors R4 and R5 set the gain. The circuit operates from a supply voltage VDDL, and the bandgap reference voltage ensures stability across temperature variations.
