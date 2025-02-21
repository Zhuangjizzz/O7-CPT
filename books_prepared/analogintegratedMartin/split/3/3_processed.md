# 3. Basic Current Mirrors and Single-Stage Amplifiers

In this chapter, fundamental building blocks are described. These blocks include a variety of current mirrors, single-stage amplifiers with active loads, and differential pairs. A good knowledge of these building blocks is critical to understanding many subjects in the rest of this book and for analog IC design in general. CMOS mirrors and gain stages are emphasized because they are prevalent in modern designs. Fortunately, most of the small-signal analyses presented can be applied to bipolar circuits with little change. In addition, rather than using resistive loads and ac coupling, the gain stages covered are shown with current-mirror active loads since such loads are almost always used in integrated circuits.

When analyzing electronic circuits containing transistors to determine their small-signal behavior, it is implicitly assumed that signals are small enough that linear approximations about an operating point accurately reflect how the circuit operates. These linear approximations may be represented schematically by replacing transistors with their small-signal equivalents, whose parameters $\left(g_{m}, r_{d s}\right.$, etc.) are related to the device's operating point currents and voltages and are summarized in Section 1.3. The general procedure for small-signal analysis is therefore:
a. Set all signal sources to zero and perform an operating point analysis for all currents and voltages. A voltage source set to 0 V is the same as an ideal wire-a short circuit. A current source set to 0 A is the same as an open circuit.
b. Replace all transistors with their small-signal equivalents where the parameters $g_{m}, r_{d s}$, etc, are found from the operating point voltages and currents using the relationships in summarized in Section 1.3.
c. Set all independent sources equal to zero, except for the signal sources that were zeroed in step (a). This includes power supply voltages, bias currents, etc. Remember that setting a voltage source to zero means replacing it with a short circuit, and setting a current source to zero means replacing it with an open circuit.
d. Analyze the resulting linearized small-signal circuit to find small-signal node voltages, branch currents, smallsignal resistances, etc.
e. If desired, the complete solution may be found by superimposing the results of the operating point analysis in step (a) and those of small-signal analysis in step (d). The result so obtained is approximate because the small-signal analysis approximates transistor nonlinear behavior with linearized models.

To the extent possible in this chapter, operating point quantities are represented with uppercase voltage and current symbols (e.g., $\mathrm{V}_{\mathrm{GS}}, \mathrm{I}_{\mathrm{D}}$ ) and small-signal quantities with lowercase symbols (e.g., $\mathrm{V}_{\mathrm{gs}}, \mathrm{i}_{\mathrm{d}}$ ). However, the practicing designer must always be alert to imprecise notation and remain able to interpret meanings within their proper context.

## 3.1 SIMPLE CMOS CURRENT MIRROR

image_name:Fig. 3.1 A simple CMOS current mirror
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: V1, G: Vi}
name: Q2, type: NMOS, ports: {S: GND, D: Vout, G: Vi}
name: I_in, type: CurrentSource, ports: {Np: LOAD, Nn: V1}
]
extrainfo:The circuit is a simple CMOS current mirror with two NMOS transistors, Q1 and Q2. The input current I_in is mirrored to the output current I_out. The gate of Q1 is connected to the gate of Q2, and the source of both transistors is connected to GND. The drain of Q1 is connected to the input current source, while the drain of Q2 is connected to the output load.

Fig. 3.1 A simple CMOS current mirror.

An ideal current mirror is a two-port circuit that accepts an input current $\mathrm{I}_{\text {in }}$ and produces and output current $\mathrm{I}_{\text {out }}=\mathrm{I}_{\text {in }}$. Since current sensing is best done with a low resistance, as in for example an ammeter, the ideal current source will have zero input resistance. An ideal current source has a high output resistance and, hence, so will an ideal current mirror. In this way, the ideal current mirror faithfully reproduces the input current regardless of the source and load impedances to which it is connected.

A simple CMOS current mirror is shown in Fig. 3.1, in which it is assumed that both transistors are in the active region, which means that the drain voltage of $Q_{2}$ must be greater than $\mathrm{V}_{\text {eff } 2}$. If the finite small-signal drain-source impedances of the transistors are ignored, and it is assumed that both transistors are the same size, then $Q_{1}$ and $Q_{2}$ will have the same current since they both have the same gate-source voltage, $\mathrm{V}_{\mathrm{gs}}$. However, when finite drain-source impedance is considered, whichever transistor has a larger drain-source voltage will also have a larger current. Let us compare this basic circuit to the "ideal" current source with zero input resistance and infinite output resistance.

To find the input resistance, consider the small-signal model for $Q_{1}$ alone, as shown in Fig. 3.2(a). The independent current source $I_{i n}$ does not exist in the small-signal model and is replaced with an open circuit. Also note that a low-frequency small-signal model is used for $Q_{1}$ (i.e., all the capacitors are ignored in the model). This small-signal model can be further reduced by finding the Thévenin-equivalent circuit. The Thévenin-equivalent output voltage is 0 since the circuit is stable and contains no input signal. This circuit's Thévenin-equivalent input impedance is found by applying a test signal voltage, $v_{y}$, at $v_{1}$ and measuring the signal current, $i_{y}$, as shown. Here, the current $\mathrm{i}_{\mathrm{y}}$ is given by

$$
\begin{equation*}
\mathrm{i}_{\mathrm{y}}=\frac{v_{\mathrm{y}}}{\mathrm{r}_{\mathrm{ds} 1}}+\mathrm{g}_{\mathrm{m} 1} v_{\mathrm{gs} 1}=\frac{v_{\mathrm{y}}}{r_{\mathrm{ds} 1}}+\mathrm{g}_{\mathrm{m} 1} v_{\mathrm{y}} \tag{3.1}
\end{equation*}
$$

The input impedance is given by $v_{y} / i_{y}$ which equals $1 / g_{m 1} \| r_{d s 1}$. Because typically $r_{d s 1}>1 / g_{m 1}$, we approximate the input impedance to be simply $1 / \mathrm{g}_{\mathrm{m} 1}$ (which is also defined to be $\mathrm{r}_{\mathrm{s} 1}$ ) resulting in the equivalent model shown in Fig. 3.2(c). This same result holds in the bipolar case and is also equivalent to the small-signal model for a diode. Hence, $\mathrm{Q}_{1}$ is often referred to as a diode-connected transistor.
image_name:Fig. 3.2 (a)
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: g1d1, G: g1d1}
]
extrainfo:The diagram shows a diode-connected NMOS transistor Q1 where the gate and drain are connected together. This configuration is often used to create a current source or a voltage reference. The equivalent small-signal model simplifies the impedance to 1/g_m1, assuming r_ds1 is much larger than 1/g_m1.
image_name:Fig. 3.2 (b)
description:
[
'name': 'r_ds1', 'type': 'Resistor', 'value': 'r_ds1', 'ports': {'N1': 'vgs1', 'N2': 'GND'
'name': 'g_m1*v_gs1', 'type': 'VoltageControlledCurrentSource', 'value': 'g_m1*v_gs1', 'ports': {'Np': 'GND', 'Nn': 'vgs1'
'name': 'v_y', 'type': 'VoltageSource', 'value': 'v_y', 'ports': {'Np': 'vy', 'Nn': 'GND'
]
extrainfo:The circuit diagram represents the small-signal model for a diode-connected NMOS transistor Q1. It includes the transconductance g_m1 and output resistance r_ds1, with an input voltage source v_y.
image_name:Fig. 3.2 (c)
description:
[
name: rin, type: Resistor,value:1/gm1, ports: {Np: V1, Nn: GND}
]
extrainfo:The circuit diagram 'Fig. 3.2 (c)' represents a simplified small-signal model for a diode-connected transistor Q1. The input impedance is approximated as 1/g_m1, and the model indicates that the transistor behaves like a resistor with value 1/g_m1 connected between Vy and GND.
Fig. 3.2 (a) A diode-connected transistor, $Q_{1}$, (b) the small-signal model for $Q_{1}$, and (c) an equivalent simplified small-signal model for $Q_{1}$.
image_name:(a)
description:The diagram represents a small-signal model of a current mirror with transistors Q1 and Q2. The input current Iin flows into the gate of Q2, and the output current Iout is taken from the drain of Q2. The resistor 1/gm1 models the input impedance of Q1, and the voltage-controlled current source gm2vgs2 models the transconductance of Q2. The resistor rds2 represents the output resistance of Q2. The voltage source Vx is used for analyzing the output characteristics.
image_name:(b)
description:The circuit diagram (b) represents a simplified small-signal model for determining the small-signal output resistance, r_out. It consists of a resistor r_ds2 and a voltage source V_x connected in parallel, both connected to ground. The voltage source V_x is applied across the nodes Vx and GND.

Fig. 3.3 (a) A small-signal model for the current mirror of Fig. 3.1 and (b) a simplified small-signal model for determining the small-signal output resistance, $r_{\text {out }}$.

Using the model just described leads to a simplified small-signal model for the overall current mirror shown in Fig. 3.3(a) where $\mathrm{v}_{\mathrm{gs} 2}$ has been connected to ground via a resistance of $1 / \mathrm{g}_{\mathrm{m} 1}$. Since no current flows through the $1 / \mathrm{g}_{\mathrm{m} 1}$ resistor, $\mathrm{v}_{\mathrm{g} \mathbf{2} 2}=0$ no matter what voltage $\mathrm{v}_{\mathrm{x}}$ is applied to the current-mirror output. This should come as no surprise, since MOS transistors operate unilaterally at low frequencies. Thus, since $\mathrm{g}_{\mathrm{m} 2} \mathbf{v}_{\mathrm{gs} 2}=0$, the circuit is simplified to the equivalent small-signal model shown in Fig. 3.3(b). The small-signal output resistance, $r_{\text {out }}$, is simply equal to $r_{\mathrm{ds} 2}$.

Key Point: A simple CMOS current mirror has a small-signal input resistance of $1 / \mathrm{g}_{\mathrm{m} 1}$ and a small-signal output resistance $\mathrm{r}_{\mathrm{ds} 2}$.

### EXAMPLE 3.1

Consider the current mirror shown in Fig.3.1, where $\mathrm{I}_{\mathrm{in}}=100 \mu \mathrm{~A}$ and each transistor has $\mathrm{W} / \mathrm{L}=10 \mu \mathrm{~m} / 0.4 \mu \mathrm{~m}$. Given the $0.35-\mu \mathrm{m}$ CMOS device parameters in Table 1.5, find $\mathrm{r}_{\text {out }}$ for the current mirror and the value of $\mathrm{g}_{\mathrm{m} 1}$. Also, estimate the change in $\mathrm{I}_{\text {out }}$ for a 100 mV change in the output voltage. What voltage must be maintained at the drain of $Q_{2}$ to ensure it remains in active mode?

### Solution

Since the $W / L$ ratios of $Q_{1}$ and $Q_{2}$ are the same, the nominal value of $I_{\text {out }}$ equals that of $I_{i n}=100 \mu \mathrm{~A}$. Thus, we have

$$
\begin{equation*}
r_{\text {out }}=r_{\text {ds } 2}=\frac{L}{\lambda L I_{D}}=\frac{0.4 \mu \mathrm{~m}}{(0.16 \mu \mathrm{~m} / \mathrm{V})(100 \mu \mathrm{~A})}=25 \mathrm{k} \Omega \tag{3.2}
\end{equation*}
$$

The value of $g_{m 1}$ is given by

$$
\begin{equation*}
\mathrm{g}_{\mathrm{m} 1}=\sqrt{2 \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L}) \mathrm{I}_{\mathrm{D} 1}}=0.97 \mathrm{~mA} / \mathrm{V} \tag{3.3}
\end{equation*}
$$

resulting in $r_{\mathrm{s} 1}=1 / \mathrm{g}_{\mathrm{m} 1} \cong 1.03 \mathrm{k} \Omega$. Note that this $\mathrm{r}_{\mathrm{s} 1}$ value is significantly less than $\mathrm{r}_{\mathrm{ds} 1}$, which equals $\mathrm{r}_{\mathrm{ds} 2}$ in this case, so that we may assume $r_{\text {in }} \cong 1.03 \mathrm{k} \Omega$.

The change in output current can be estimated, using $r_{\text {out }}$, as

$$
\begin{equation*}
\Delta \mathrm{I}_{\text {out }}=\frac{\Delta \mathrm{V}}{\mathrm{r}_{\text {out }}}=\frac{100 \mathrm{mV}}{25 \mathrm{k} \Omega}=4 \mu \mathrm{~A} \tag{3.4}
\end{equation*}
$$

In other words, if initially $\mathrm{I}_{\text {out }}$ is measured to be $101 \mu \mathrm{~A}$ (due to mismatch or a larger $\mathrm{V}_{\mathrm{DS}}$ voltage), then a 100 mV increase in output voltage would result in a new output current of about $105 \mu \mathrm{~A}$. Note that this estimate does not account for second-order effects such as the fact that $r_{d s}$ changes as the output current changes.

Finally, the drain voltage of $Q_{2}$ must be at least $\mathrm{V}_{\text {eff } 2}$ in order to keep it in active mode.

$$
V_{\text {eff } 2}=\sqrt{\frac{2 I_{D}}{\mu_{\mathrm{n}} C_{\mathrm{ox}}(W / L)}}=205 \mathrm{mV}
$$

You may compare these results to those obtained with a SPICE simulation.

## 3.2 COMMON-SOURCE AMPLIFIER

image_name:Fig. 3.4 A common-source amplifier with a current-mirror active load
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: Q2, type: PMOS, ports: {S: VDD, D: Vout, G: P}
name: Q3, type: PMOS, ports: {S: VDD, D: P, G: P}
name: Ibias, type: CurrentSource, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a common-source amplifier with a current-mirror active load. Q1 is the n-channel MOSFET amplifier, and Q2 and Q3 form the p-channel current mirror that provides the active load. Ibias supplies the bias current for the circuit.

Fig. 3.4 A common-source amplifier with a current-mirror active load.

A common use of simple current mirrors is in a single-stage amplifier with an active load, as shown in Fig. 3.4. This common-source topology is the most popular gain stage, especially when high input impedance is desired.

Here, an n -channel common-source amplifier has a p-channel current mirror used as an active load to supply the bias current for the drive transistor. By using an active load, a high-impedance output load can be realized without using excessively large resistors or a large power-supply voltage. As a result, for a given powersupply voltage, a larger voltage gain can be achieved using an active load than would be possible if a resistor were used for the load. For example, if a $100-\mathrm{k} \Omega$ load were required with a $100-\mu \mathrm{A}$ bias current, a resistive-load approach would require a power-supply voltage of $100 \mathrm{k} \Omega \times 100 \mu \mathrm{~A}=10 \mathrm{~V}$. An active load takes advantage of the nonlinear, large-signal transistor current-voltage relationship to provide large small-signal resistances without large dc voltage drops.

Key Point: The common-source amplifier is a popular gain stage, especially when high input impedance is desired. The use of an active load takes advantage of the nonlinear, large-signal transistor current-voltage relationship to provide large small-signal resistances without large dc voltage drops.

A small-signal equivalent circuit for the low-frequency analysis of the common-source amplifier of Fig. 3.4 is shown in Fig. 3.5 where $V_{\text {in }}$ and $R_{\text {in }}$ are the Thévenin equivalent of the input source. It is assumed that the bias voltages are such that both transistors are in the active region. The output resistance, $R_{2}$, is made up of the parallel combination of the drain-to-source resistance of $Q_{1}$, that is, $r_{d s}$, and the drain-to-source resistance of $Q_{2}$, that is, $r_{\text {ds } 2}$. Notice that the voltage-controlled current source modelling the body effect has not been included since the source is at a smallsignal ground, and, therefore, this source always has 0 current.

Using small-signal analysis, we have $\mathrm{v}_{\mathrm{gs} 1}=\mathrm{v}_{\mathrm{in}}$ and, therefore,

$$
\begin{equation*}
A_{v}=\frac{v_{\text {out }}}{V_{\text {in }}}=-g_{m 1} R_{2}=-g_{m 1}\left(r_{d s 1} \| r_{d s 2}\right) \tag{3.5}
\end{equation*}
$$

image_name:Fig. 3.5
description:
[{'name': 'Vin', 'type': 'VoltageSource', 'value': 'Vin', 'ports': {'Np': 'Vin', 'Nn': 'GND'}}, {'name': 'Rin', 'type': 'Resistor', 'value': 'Rin', 'ports': {'N1': 'Vin', 'N2': 'Vgs1'}}]
[{'name': 'g_m1V_gs1', 'type': 'VoltageControlledCurrentSource', 'ports': {'Np': 'Vgs1', 'Nn': 'GND'}}, {'name': 'R2', 'type': 'Resistor', 'value': 'rds1||rds2', 'ports': {'N1': 'Vout', 'N2': 'GND'}}]
extrainfo:The circuit is a small-signal equivalent of a common-source amplifier with a voltage gain of Av = -gm1 * R2. The gain is determined by the transconductance gm1 and the parallel combination of rds1 and rds2.

Fig. 3.5 A small-signal equivalent circuit for the common-source amplifier.

Depending on the device sizes, currents, and the technology used, a typical gain for this circuit is in the range of -5 to -100 . To achieve similar gains with resistive loads, much larger power-supply voltages must be used which also greatly increases the power dissipation. However, it should be mentioned here that for low-gain, highfrequency stages, it may be desirable to use resistor loads (if they do not require much silicon area) because they often have less parasitic capacitances associated with them. They are also typically less noisy than active loads.

### EXAMPLE 3.2

Assume $\mathrm{I}_{\text {bias }}=100 \mu \mathrm{~A}$, all transistors have $\mathrm{W} / \mathrm{L}=10 \mu \mathrm{~m} / 0.4 \mu \mathrm{~m}$ in Fig. 3.4, and the device parameters are those of the $0.35-\mu \mathrm{m}$ CMOS process in Table 1.5. What is the gain of the stage?

### Solution

We have

$$
\begin{equation*}
\mathrm{g}_{\mathrm{m} 1}=\sqrt{2 \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L})_{1} \mathrm{I}_{\text {bias }}}=0.97 \mathrm{~mA} / \mathrm{V} \tag{3.6}
\end{equation*}
$$

In this case, $\lambda \mathrm{L}$ is the same for both NMOS and PMOS devices, so

$$
\begin{equation*}
r_{d s 1}=r_{d s 2}=\frac{L}{\lambda L I_{D}}=\frac{0.4 \mu \mathrm{~m}}{(0.16 \mu \mathrm{~m} / \mathrm{V})(100 \mu \mathrm{~A})}=25 \mathrm{k} \Omega \tag{3.7}
\end{equation*}
$$

Using Eq. (3.5), we have

$$
\begin{equation*}
\mathrm{A}_{\mathrm{V}}=-\mathrm{g}_{\mathrm{m} 1}\left(\mathrm{r}_{\mathrm{ds} 1} \| \mathrm{r}_{\mathrm{ds} 2}\right)=-0.97 \mathrm{~mA} / \mathrm{V}(25 \mathrm{k} \Omega \| 25 \mathrm{k} \Omega)=-12.1 \mathrm{~V} / \mathrm{V} \tag{3.8}
\end{equation*}
$$

Compare these results to those obtained with a SPICE simulation.

Under the simple assumption that $\mathrm{r}_{\mathrm{ds} 2} \approx \mathrm{r}_{\mathrm{ds} 1}$, the gain of the common source amplifier is one-half the intrinsic gain of transistor $Q_{1}: A_{i}=g_{m 1} r_{d s 1} \approx 2 /\left(\lambda V_{\text {eff }}\right)$. Hence, in order to maximize the gain of this stage, it is desirable to maximize the intrinsic gain by operating $Q_{1}$ with small $\mathrm{V}_{\text {eff }}$. For a fixed bias drain current, $\mathrm{I}_{\mathrm{D}}$, the effective overdrive voltage is reduced by increasing the device width W . However, beyond a certain width, $\mathrm{V}_{\text {eff }}$ approaches zero, the transistor will enter subthreshold operation, and no further increases in intrinsic gain are observed.

### EXAMPLE 3.3

Modify the design in Example 3.2 to increase the gain by 20\% by changing only the device width, W.

### Solution

Neglecting higher-order effects, with the drain current fixed the output resistance ( $r_{\mathrm{ds} 1} \| \mathrm{r}_{\mathrm{ds} 2}$ ) is nominally unchanged. Hence, in order to increase gain by $20 \%$, we must increase $\mathrm{g}_{\mathrm{m} 1}$ by $20 \%$. Due to the square-root dependence of $g_{m}$ on $W$ (with fixed current), this in turn requires a $44 \%$ increase in $W_{1}$. Hence, the new size of $Q_{1}$ is $(14.4 \mu \mathrm{~m} / 0.4 \mu \mathrm{~m})$. The resulting gain is

$$
\begin{gathered}
\mathrm{g}_{\mathrm{m} 1}=\sqrt{2 \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L})_{1} \mathrm{I}_{\mathrm{bias}}}=1.17 \mathrm{~mA} / \mathrm{V} \\
\Rightarrow \mathrm{~A}_{\mathrm{V}}=-\mathrm{g}_{\mathrm{m} 1}\left(\mathrm{r}_{\mathrm{ds} 1} \| \mathrm{r}_{\mathrm{ds} 2}\right)=-1.17 \mathrm{~mA} / \mathrm{V}(25 \mathrm{k} \Omega \| 25 \mathrm{k} \Omega)=-14.6 \mathrm{~V} / \mathrm{V}
\end{gathered}
$$

This is, indeed, $20 \%$ greater than the gain of $-12.1 \mathrm{~V} / \mathrm{V}$ computed in Example 3.2. The resulting effective gatesource voltage is

$$
V_{\text {eff } 1}=\sqrt{\frac{2 I_{D}}{\mu_{\mathrm{n}} C_{o x}(W / L)}}=171 \mathrm{mV}
$$

which is sufficient to keep $Q_{1}$ out of subthreshold operation.

## 3.3 SOURCE-FOLLOWER OR COMMON-DRAIN AMPLIFIER

image_name:Fig. 3.6
description:
[
name: I_bias, type: CurrentSource, value: I_bias, ports: {Np: VDD, Nn: P}
name: Q1, type: NMOS, ports: {S: Vout, D: VDD, G: Vin}
name: Q2, type: NMOS, ports: {S: GND, D: Vout, G: P}
name: Q3, type: NMOS, ports: {S: GND, D: P, G: P}
]
extrainfo:The circuit is a source-follower stage with a current mirror used to supply the bias current. Q1 is the source follower, and Q2 and Q3 form the active load that supplies the bias current of Q1. The circuit is commonly used as a voltage buffer.

Fig. 3.6 A source-follower stage with a current mirror used to supply the bias current.

Another general use of current mirrors is to supply the bias current of source-follower amplifiers, as shown in Fig. 3.6. In this example, $Q_{1}$ is the source follower and $Q_{2}$ is an active load that supplies the bias current of $Q_{1}$. These amplifiers are commonly used as voltage buffers and are therefore commonly called source followers. They are also referred to as common-drain amplifiers, since the input and output nodes are at the gate and source nodes, respectively, with the drain node being at small-signal ground. Although the dc level of the output voltage is not the same as the dc level of the input voltage, ideally the small-signal voltage gain is close to unity. In reality, it is somewhat less than unity. However, although this circuit does not generate voltage gain, it does have the ability to generate current gain.

Key Point: The sourcefollower provides a voltage gain close to unity, and often limited by the body effect. It can provide a large current gain and it is unilateral so it is often used as a voltage buffer.

A small-signal model for low-frequency analysis of this source-follower stage is shown in Fig. 3.7. Note that the voltage-controlled current source that models the body effect of MOS transistors has been included because the source is not at small-signal ground. The body effect is a major limitation on the smallsignal gain. Note that in Fig. 3.7, $r_{\mathrm{ds} 1}$ is in parallel with $r_{\mathrm{ds} 2}$. Notice also that the voltage-controlled current source modelling the body effect produces a current that is proportional to the voltage across it. This relationship makes the body effect equivalent to a resistor of size $1 / \mathrm{g}_{\mathrm{s} 1}$, which is also in parallel with $\mathrm{r}_{\mathrm{ds} 1}$ and $r_{\mathrm{ds} 2}$. Thus, the small-signal model of Fig. 3.7 is equivalent to the simplified small-signal model of Fig. 3.8, in which $R_{s 1}=r_{d s 1}\left\|r_{d s}\right\| 1 / g_{s 1}$. Writing the nodal equation at $v_{\mathrm{out}}$, and noting that $v_{g s 1}=v_{\mathrm{in}}-v_{\text {out }}$, we have

$$
\begin{equation*}
v_{\text {out }} / R_{s 1}-g_{m 1}\left(v_{\text {in }}-v_{\text {out }}\right)=0 \tag{3.9}
\end{equation*}
$$

To minimize circuit equation errors, a consistent methodology should be maintained when writing nodal equations. The methodology employed here is as follows: The first term is always the node at which the currents are being summed. This node voltage is multiplied by the sum of all admittances connected to the node. The next negative terms are the adjacent node voltages, and each is multiplied by the connecting admittance. The last terms are any current sources with a multiplying negative sign used if the current is shown to flow into the node.

Solving for $\mathrm{v}_{\text {out }} / \mathrm{v}_{\text {in }}$, we have

$$
\begin{equation*}
A_{v}=\frac{v_{\text {out }}}{v_{\text {in }}}=\frac{g_{m 1}}{g_{m 1}+G_{s 1}}=\frac{g_{m 1}}{g_{m 1}+g_{s 1}+g_{d s 1}+g_{d s}}=g_{m 1}\left(\frac{1}{g_{m 1}}\left\|\frac{1}{g_{s 1}}\right\| r_{d s 1} \| r_{d s 2}\right) \tag{3.10}
\end{equation*}
$$

image_name:Fig. 3.7 The low-frequency model of the source-follower amplifier
description:
[
name: g_m1v_gs1, type: VoltageControlledCurrentSource, ports: {Np: Vd1, Nn: Vs1}
name: g_s1v_s1, type: VoltageControlledVoltageSource, ports: {Np: Vd1, Nn: Vs1}
name: r_ds1, type: Resistor, value: r_ds1, ports: {N1: Vd1, N2: Vd1}
name: r_ds2, type: Resistor, value: r_ds2, ports: {N1: Vs1, N2: GND}
]
extrainfo:This is a low-frequency model of a source-follower amplifier. The circuit includes a voltage-controlled current source and a voltage-controlled voltage source, along with two resistors connected to ground. The input voltage is labeled Vin, and the output voltage is Vout, which is equal to Vs1.

Fig. 3.7 The low-frequency model of the source-follower amplifier.
where the notation $G_{s 1}=1 / R_{s 1}$ is used. ${ }^{1}$ Normally, $g_{s 1}$ is on the order of one-tenth to one-fifth that of $\mathrm{g}_{\mathrm{m} 1}$. Also, the transistor output admittances, $\mathrm{g}_{\mathrm{ds} 1}$ and $\mathrm{g}_{\mathrm{ds} 2}$, might be one-tenth that of the body-effect parameter, $\mathrm{g}_{\mathrm{s} 1}$. Therefore, it is seen that the body-effect parameter is the major source of error causing the gain to be less than unity. Notice also that at low frequencies the stage is completely unilateral. In other words, there is no signal flow from the output to the input. This can be seen by applying a small test signal to the output and noting that it induces no voltage or current at the input.
image_name:Fig. 3.8 An equivalent small-signal model for the source follower.
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: Vout}
name: g_m1v_gs1, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: Vout}
name: Rs1, type: Resistor, value: Rs1, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a small-signal model of a source follower with a voltage-controlled current source representing the transconductance. The input is applied to Vin and the output is taken from Vout. Rs1 is connected between Vout and ground.

Fig. 3.8 An equivalent small-signal model for the source follower.

### EXAMPLE 3.4

Consider the source follower of Fig. 3.6 where $\mathrm{I}_{\text {bias }}=100 \mu \mathrm{~A}$, all transistors have $\mathrm{W} / \mathrm{L}=2 \mu \mathrm{~m} / 0.2 \mu \mathrm{~m}$, $\phi_{\mathrm{F}} \cong 0.4 \mathrm{~V}$ and $\gamma=0.3 \mathrm{~V}^{-1 / 2}$, and the other device parameters are those of the $0.18-\mu \mathrm{m}$ CMOS process in Table 1.5. What is the gain of the stage?

### Solution

We first find the transconductance,

$$
\begin{equation*}
\mathrm{g}_{\mathrm{m} 1}=\sqrt{2 \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L})_{1} \mathrm{I}_{\mathrm{bias}}}=0.735 \mathrm{~mA} / \mathrm{V} \tag{3.11}
\end{equation*}
$$

Also,

$$
\begin{equation*}
r_{d s 1}=r_{d s 2}=\frac{L}{\lambda L I_{D}}=\frac{0.2 \mu \mathrm{~m}}{(0.08 \mu \mathrm{~m} / \mathrm{V})(100 \mu \mathrm{~A})}=25 \mathrm{k} \Omega \tag{3.12}
\end{equation*}
$$

[^2]The equation for the body-effect parameter, from Chapter 1, is

$$
\begin{equation*}
g_{\mathrm{s} 1}=\frac{\gamma \mathrm{g}_{\mathrm{m}}}{2 \sqrt{V_{\mathrm{SB}}+\left|2 \phi_{\mathrm{F}}\right|}} \tag{3.13}
\end{equation*}
$$

To calculate this parameter, we need to know the source-bulk voltage, $\mathrm{V}_{\mathrm{SB}}$. Unfortunately, this voltage is dependent on the application and cannot be known accurately beforehand. Here we will assume that $\mathrm{V}_{\mathrm{SB}} \approx 0.5 \mathrm{~V}$ to obtain an estimate. We therefore have

$$
\begin{equation*}
\mathrm{g}_{\mathrm{s} 1}=\frac{0.3 \mathrm{~V}^{-1 / 2} \cdot \mathrm{~g}_{\mathrm{m}}}{2 \sqrt{0.5 \mathrm{~V}+0.8 \mathrm{~V}}} \cong 0.13 \mathrm{~g}_{\mathrm{m}}=0.1 \mathrm{~mA} / \mathrm{V} \tag{3.14}
\end{equation*}
$$

Using (3.10), we have

$$
\begin{equation*}
A_{V}=\frac{0.735 \mathrm{~mA} / \mathrm{V}}{0.735 \mathrm{~mA} / \mathrm{V}+0.1 \mathrm{~mA} / \mathrm{V}+0.04 \mathrm{~mA} / \mathrm{V}+0.04 \mathrm{~mA} / \mathrm{V}}=0.8 \mathrm{~V} / \mathrm{V}=-1.9 \mathrm{~dB} \tag{3.15}
\end{equation*}
$$

Note that, as mentioned above, the body-effect parameter, $\mathrm{g}_{\mathrm{s} 1}$ is larger than the other parasitic conductances $\mathrm{g}_{\mathrm{ds} 1}$ and $g_{d s 2}$ and, hence, plays a dominant role in limiting the gain. If the body effect were not present (for example, if the source and body could be shorted together) the gain would be increased to around -0.9 dB .

## 3.4 COMMON-GATE AMPLIFIER

image_name:Fig. 3.9
description:
[
name: Q3, type: PMOS, ports: {S: VDD, D: P, G: P}
name: Q2, type: PMOS, ports: {S: VDD, D: Vout, G: P}
name: Q1, type: NMOS, ports: {S: Vin, D: Vout, G: Vbias}
name: Ibias, type: CurrentSource, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a common-gate amplifier with a current-mirror active load. It is designed to have a low input impedance and is commonly used to terminate transmission lines or as the first stage of an amplifier where the input signal is a current.

Fig. 3.9 A common-gate amplifier with a current-mirror active load.

A common-gate amplifier with an active load is shown in Fig. 3.9. This stage is commonly used as a gain stage when a relatively small input impedance is desired. For example, it might be designed to have an input impedance of $50 \Omega$ to terminate a $50-\Omega$ transmission line. Another common application for a common-gate amplifier is as the first stage of an amplifier where the input signal is a current; in such cases a small input impedance is desired in order to ensure all of the current signal is drawn into the amplifier, and none is "lost" in the signal source impedance. Aside from its low input impedance, the commongate amplifier is similar to a common-source amplifier; in both cases the input is applied across $\mathrm{v}_{\mathrm{gs}}$, except with opposite polarities, and the output is taken at the drain. Hence, in both cases the small signal gain magnitude approximately equals the product of $g_{m}$ and the total impedance at the drain.

If we use straightforward small-signal analysis, when the impedance seen at $\mathrm{V}_{\text {out }}$ (in this case, the output impedance of the current mirror formed by $Q_{2}$ ) is much less than $r_{d s 1}$, the input impedance, $r_{\text {out }}$, is found to be $1 / g_{m 1}$ at low frequencies. However, in integrated applications, the impedance seen at $V_{\text {out }}$ is often on the same order of magnitude or even much greater than $r_{\mathrm{ds} 1}$. In this case, the input impedance at low frequencies can be considerably larger than $1 / \mathrm{g}_{\mathrm{m} 1}$. To see this result, consider the small-signal model shown in Fig. 3.10. In this model, the voltage-dependent current source that models the body effect has been included. Notice that $\mathrm{v}_{\mathrm{gs} 1}=-\mathrm{v}_{\mathrm{s} 1}$ and therefore the two current sources can be combined into a single current source, as shown in Fig. 3.11. This simplification is always possible for a transistor that has a grounded gate in a small-signal model, and considerably simplifies taking the body effect
into account. Specifically, one can simply ignore the body effect for transistors with grounded gates, and then, after the analysis is complete, simply replace the constants $\mathrm{g}_{\mathrm{mi}}$ with $\mathrm{g}_{\mathrm{mi}}+\mathrm{g}_{\mathrm{si}}$. However, for this example, we include the body-effect parameter throughout the analysis.

At node $v_{\text {out }}$, we have

$$
\begin{equation*}
v_{\text {out }}\left(G_{L}+g_{d s 1}\right)-v_{s 1} g_{d s 1}-\left(g_{m 1}+g_{s 1}\right) v_{s 1}=0 \tag{3.16}
\end{equation*}
$$

Rearranging slightly, we have

$$
\begin{equation*}
\frac{v_{\text {out }}}{v_{\mathrm{s} 1}}=\frac{g_{\mathrm{m} 1}+g_{\mathrm{s} 1}+g_{\mathrm{ds} 1}}{G_{\mathrm{L}}+g_{\mathrm{ds} 1}}=\left(g_{\mathrm{m} 1}+g_{\mathrm{s} 1}+g_{\mathrm{ds} 1}\right)\left(R_{\mathrm{L}} \| r_{\mathrm{ds} 1}\right) \cong g_{\mathrm{m} 1}\left(R_{\mathrm{L}} \| r_{\mathrm{ds} 1}\right) \tag{3.17}
\end{equation*}
$$

image_name:Fig. 3.10 The small-signal model of the common-gate amplifier at low frequencies
description:
[
name: Vgs1, type: VoltageSource, value: Vgs1, ports: {Np: GND, Nn: Vs1}
name: Rs, type: Resistor, value: Rs, ports: {N1: Vs1, N2: Vin}
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: gm1Vgs1, type: VoltageControlledCurrentSource, ports: {Np: Vout, Nn: Vs1}
name: gs1Vs1, type: VoltageControlledCurrentSource, ports: {Np: Vout, Nn: Vs1}
name: rds1, type: Resistor, value: rds1, ports: {N1: Vout, N2: Vs1}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a small-signal model of a common-gate amplifier at low frequencies. It includes voltage sources, resistors, and voltage-controlled current sources. The output voltage is taken across RL, and the input is applied to Vin.

Fig. 3.10 The small-signal model of the common-gate amplifier at low frequencies.
image_name:Fig. 3.10
description:
[
name: Vs1, type: VoltageSource, value: Vs1, ports: {Np: GND, Nn: Vs1}
name: Rs, type: Resistor, value: Rs, ports: {N1: Vs1, N2: Vin}
name: rds1, type: Resistor, value: rds1, ports: {N1: Vout, N2: Vs1}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: (gm1+gs1)Vs1, type: VoltageControlledVoltageSource, ports: {N1: Vout, N2: Vs1}
]
extrainfo:The circuit is a small-signal model of a common-gate amplifier at low frequencies. It includes voltage sources, resistors, and voltage-controlled current sources. The output voltage is taken across RL, and the input is applied to Vin.

Fig. 3.11 A simplified small-signal model of the common-gate amplifier.

The current going into the source of $Q_{1}$ is given by

$$
\begin{equation*}
i_{s}=v_{s 1}\left(g_{m 1}+g_{s 1}+g_{d s 1}\right)-v_{\text {out }} g_{d s 1} \tag{3.18}
\end{equation*}
$$

Combining (3.17) and (3.18) to find the input admittance, $\mathrm{g}_{\mathrm{in}}=1 / \mathrm{r}_{\mathrm{in}}$, we have

$$
\begin{equation*}
g_{\mathrm{in}} \equiv \frac{i_{\mathrm{s}}}{v_{s 1}} \equiv \frac{g_{\mathrm{m} 1}+g_{\mathrm{s} 1}+g_{\mathrm{ds} 1}}{1+\frac{g_{\mathrm{ds} 1}}{G_{\mathrm{L}}}} \cong \frac{g_{\mathrm{m} 1}}{1+\frac{g_{\mathrm{ds} 1}}{G_{\mathrm{L}}}} \tag{3.19}
\end{equation*}
$$

Alternatively, we have

$$
\begin{equation*}
r_{\text {in }}=\frac{1}{g_{i n}}=\left(\frac{1}{g_{m 1}}\left\|\frac{1}{g_{s 1}}\right\| r_{d s 1}\right)\left(1+\frac{R_{L}}{r_{d s 1}}\right) \cong \frac{1}{g_{m 1}}\left(1+\frac{R_{L}}{r_{d s 1}}\right) \tag{3.20}
\end{equation*}
$$

Key Point: The common-gate amplifier provides a voltage gain comparable to that of the common-source amplifier, but with a relatively low input resistance on the order of $1 / \mathrm{g}_{\mathrm{m}}$. However, the input resistance can be larger when the amplifier has a large small-signal load resistance.

With the p -channel active load shown in Fig. 3.9, $R_{\mathrm{L}}=r_{\mathrm{ds} 2}$. Since, in this case, $R_{L}$ is approximately the same magnitude as $r_{\text {ds }}$, the input impedance, $r_{i n}$, is about $2 / g_{m 1}$ for low frequencies-twice as large as the expected value of $1 / \mathrm{g}_{\mathrm{m} 1}$. This increased input impedance must be taken into account in applications such as transmission-line terminations. In some examples, the current-mirror output impedance realized by $Q_{2}$ is much larger than $r_{d s 1}$ (i.e., $\mathrm{R}_{\mathrm{L}}>>\mathrm{r}_{\mathrm{dst}}$ ), and so the input impedance for this common-gate amplifier is much lar ger than $1 / \mathrm{g}_{\mathrm{m} 1}$. This increased input impedance often occurs in integrated circuits and is not commonly known.

The attenuation from the input source to the transistor source can be considerable for a common-gate amplifier when $R_{s}$ is large. This attenuation is given by

$$
\begin{equation*}
\frac{v_{s 1}}{v_{\text {in }}}=\frac{r_{\text {in }}}{R_{s}+r_{\text {in }}} \tag{3.21}
\end{equation*}
$$

Using (3.20) to replace $r_{\text {in }}$, we have

$$
\begin{equation*}
\frac{v_{s 1}}{v_{i n}}=\frac{\left(\frac{1}{g_{m 1}}\left\|\frac{1}{g_{s 1}}\right\| r_{d s 1}\right)\left(1+\frac{R_{L}}{r_{d s 1}}\right)}{R_{s}+\left(\frac{1}{g_{m 1}}\left\|\frac{1}{g_{s 1}}\right\| r_{d s 1}\right)\left(1+\frac{R_{L}}{r_{d s 1}}\right)}=\frac{1}{1+R_{s}\left(\frac{g_{m 1}+g_{s 1}+g_{d s 1}}{1+R_{L} / r_{d s 1}}\right)} \tag{3.22}
\end{equation*}
$$

Using (3.17) and (3.22), we find that the overall dc gain is given by

$$
\begin{equation*}
A_{v}=\frac{v_{\text {out }}}{v_{\text {in }}}=\frac{\left(g_{m 1}+g_{s 1}+g_{d s 1}\right)\left(R_{L} \| r_{d s 1}\right)}{1+R_{s}\left(\frac{g_{m 1}+g_{s 1}+g_{d s 1}}{1+R_{L} / r_{d s 1}}\right)} \cong \frac{g_{m 1}\left(R_{L} \| r_{d s 1}\right)}{1+R_{s}\left(\frac{g_{m 1}+g_{s 1}+g_{d s 1}}{1+R_{L} / r_{d s 1}}\right)} \tag{3.23}
\end{equation*}
$$

### EXAMPLE 3.5

Design the common-gate amplifier of Fig. 3.9 to have an input impedance of approximately $50 \Omega$ using the $0.18-\mu \mathrm{m}$ CMOS devices in Table 1.5 with $\mathrm{I}_{\text {bias }}=100 \mu \mathrm{~A},(\mathrm{~W} / \mathrm{L})_{3}=2 \mu \mathrm{~m} / 0.2 \mu \mathrm{~m}$.

### Solution

Since $(\lambda L)_{1}=(\lambda L)_{2}$, if we take $L_{1}=L_{2}=0.2 \mu \mathrm{~m}$ we ensure $r_{\mathrm{ds} 2}=R_{L}=r_{d s 1}$ and using (3.20),

$$
\begin{equation*}
\mathrm{r}_{\mathrm{in}} \cong 2 / \mathrm{g}_{\mathrm{m} 1} \tag{3.24}
\end{equation*}
$$

Hence, to ensure $r_{\text {in }}=50 \Omega$,

$$
\begin{equation*}
\mathrm{g}_{\mathrm{m} 1} \cong 2 /(50 \Omega)=40 \mathrm{~mA} / \mathrm{V} \tag{3.25}
\end{equation*}
$$

If we take $\mathrm{V}_{\text {eff } 1}=200 \mathrm{mV}$,

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D} 2}=\mathrm{I}_{\mathrm{D} 1}=\mathrm{g}_{\mathrm{m} 1} \mathrm{~V}_{\mathrm{eff} 1} / 2=(40 \mathrm{~mA} / \mathrm{V})(200 \mathrm{mV}) / 2=4 \mathrm{~mA} \tag{3.26}
\end{equation*}
$$

This requires the current mirror to provide a gain of $4 \mathrm{~mA} / 100 \mu \mathrm{~A}=40$.

$$
(\mathrm{W} / \mathrm{L})_{2}=40(\mathrm{~W} / \mathrm{L})_{3}=80 \mu \mathrm{~m} / 0.2 \mu \mathrm{~m}
$$

Finally, using the values in (3.25) and (3.26),

$$
(\mathrm{W} / \mathrm{L})_{1}=\frac{\mathrm{g}_{\mathrm{m} 1}^{2}}{2 \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}} \mathrm{I}_{\mathrm{D} 1}}=148 \mu \mathrm{~m} / 0.2 \mu \mathrm{~m}
$$

In reality, the input impedance will be somewhat lower than $50 \Omega$ due to the body effect and finite drain-source resistance, $r_{\mathrm{ds} 1}$, not included in (3.24).

## 3.5 SOURCE-DEGENERATED CURRENT MIRRORS

We saw in Section 3.1 that a current mirror can be realized using only two transistors, where the output impedance of this current source was seen to be $r_{\text {ds2 }}$. To increase this output impedance, a source-degenerated current mirror can be used, as shown in Fig. 3.12. The small-signal model for this current mirror is shown in Fig. 3.13. Since no small-signal current flows into the gate, the gate voltage is 0 V in Fig. 3.13.

Note that the current $i_{x}$ sourced by the applied voltage source is equal to the current through the degeneration resistor, $\mathrm{R}_{\mathrm{s}}$. Therefore, we have

$$
\begin{equation*}
v_{s}=i_{x} R_{s} \tag{3.27}
\end{equation*}
$$

Also, note that

$$
\begin{equation*}
\mathrm{V}_{\mathrm{gs}}=-\mathrm{V}_{\mathrm{s}} \tag{3.28}
\end{equation*}
$$

image_name:Fig. 3.12
description:
[
name: Q1, type: NMOS, ports: {S: s1, D: P, G: P}
name: Q2, type: NMOS, ports: {S: s2, D: LOAD, G: P}
name: Rs, type: Resistor, value: Rs, ports: {N1: s1, N2: GND}
name: Rs, type: Resistor, value: Rs, ports: {N1: s2, N2: GND}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: VDD, Nn: P}
]
extrainfo:The circuit is a current mirror with source degeneration, using two NMOS transistors Q1 and Q2. The degeneration resistors Rs are connected to the sources of Q1 and Q2, providing feedback to stabilize the current. The input current Iin flows through Q1, and the output current Iout is mirrored through Q2.

Fig. 3.12 A current mirror with source degeneration.

Fig. 3.13 The small-signal model for the source-degenerated current source.
image_name:Fig. 3.13 The small-signal model for the source-degenerated current source
description:The circuit represents a small-signal model of a source-degenerated current source. It includes a voltage-controlled current source and resistors for source degeneration, with the current ix flowing through the circuit.

Setting $i_{x}$ equal to the total current through $g_{m 2} \mathbf{v}_{\mathrm{gs}}$ and $r_{\mathrm{ds} 2}$ gives

$$
\begin{equation*}
i_{x}=g_{m 2} v_{g s}+\frac{v_{x}-v_{s}}{r_{d s}} \tag{3.29}
\end{equation*}
$$

Substituting (3.27) and (3.28) into (3.29) gives

$$
\begin{equation*}
i_{x}=-i_{x} g_{m 2} R_{s}+\frac{v_{x}-i_{x} R_{s}}{r_{d s}} \tag{3.30}
\end{equation*}
$$

Rearranging, we find the output impedance to be given by

$$
\begin{equation*}
r_{\text {out }}=\frac{v_{x}}{i_{x}}=r_{d s 2}\left[1+R_{s}\left(g_{m 2}+g_{d s 2}\right)\right] \cong r_{d s 2}\left(1+R_{s} g_{m 2}\right) \tag{3.31}
\end{equation*}
$$

where $\mathrm{g}_{\mathrm{ds} 2}$ is equal to $1 / \mathrm{r}_{\mathrm{d} 2}$, which is much less than $\mathrm{g}_{\mathrm{m} 2}$. Thus, the output impedance has been increased by a factor approximately equal to $\left(1+R_{s} g_{m 2}\right)$.

Key Point: When a small-signal resistance $\mathrm{R}_{\mathrm{s}}$ is introduced at the source of both transistors in a simple current mirror, the output resistance is increased by a factor approximately equal to $\left(1+R_{s} g_{m}\right)$.

This formula can often be applied to moderately complicated circuits to quickly estimate the impedances looking into a node. Such an example follows, in the derivation of the output impedance of cascode current mirrors. It should be noted that the above derivation ignores the body effect of the transistor, even though the source of the transistor is not connected to a small-signal ground. As discussed earlier, in Section 3.4, since the gate is at a small-signal ground, the body effect can be taken into account by simply replacing $g_{\mathrm{m} 2}$ in Eq. (3.31) with $g_{m 2}+g_{s}$. This substitution results in

$$
\begin{equation*}
r_{\text {out }}=\frac{v_{x}}{i_{x}}=r_{d s 2}\left[1+R_{s}\left(g_{m 2}+g_{s 2}+g_{d s 2}\right)\right] \cong r_{d s 2}\left[1+R_{s}\left(g_{m 2}+g_{s 2}\right)\right] \tag{3.32}
\end{equation*}
$$

where $g_{s 2}$ is the body-effect constant. This result is only slightly different since $g_{s}$ is roughly one-fifth of $g_{m}$.

### EXAMPLE 3.6

Consider the current mirror shown in Fig. 3.12, where $\mathrm{I}_{\text {in }}=100 \mu \mathrm{~A}$, each transistor has $\mathrm{W} / \mathrm{L}=10 \mu \mathrm{~m} / 0.2 \mu \mathrm{~m}$, and $R_{s}=1 \mathrm{k} \Omega$. Using the $0.18-\mu \mathrm{m}$ CMOS devices in Table 1.5 , find $r_{\text {out }}$ for the current mirror. Assume the body effect can be approximated by $\mathrm{g}_{\mathrm{s}}=0.15 \mathrm{~g}_{\mathrm{m}}$.

### Solution

Nominally, $\mathrm{I}_{\text {out }}=\mathrm{I}_{\mathrm{in}}$, and thus we find the small-signal parameters for this current mirror to be

$$
\begin{equation*}
\mathrm{g}_{\mathrm{m} 2}=\sqrt{2 \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L}) \mathrm{I}_{\mathrm{out}}}=1.64 \mathrm{~mA} / \mathrm{V} \tag{3.33}
\end{equation*}
$$

Also we have

$$
\begin{equation*}
\mathrm{r}_{\mathrm{ds} 2}=\frac{0.2 \mu \mathrm{~m}}{0.08 \mu \mathrm{~m} / \mathrm{V} 100 \mu \mathrm{~A}}=25 \mathrm{k} \Omega \tag{3.34}
\end{equation*}
$$

Now, making use of (3.32), the output impedance is given by

$$
\begin{equation*}
\mathrm{r}_{\text {out }}=25 \mathrm{k} \Omega\left[1+1 \mathrm{k} \Omega\left(1.64 \mathrm{~mA} / \mathrm{V}+0.15 \cdot 1.64 \mathrm{~mA} / \mathrm{V}+\frac{1}{25 \mathrm{k} \Omega}\right)\right]=73.15 \mathrm{k} \Omega \tag{3.35}
\end{equation*}
$$

Note that this result is nearly three times the output impedance for a simple current mirror which would be simply $r_{\mathrm{ds} 2}=25 \mathrm{k} \Omega$. Also note that the voltage drop across $R_{s}$ equals $100 \mu \mathrm{~A} \times 1 \mathrm{k} \Omega=0.1 \mathrm{~V}$ due to the dc bias current through it.

## 3.6 CASCODE CURRENT MIRRORS

A cascode current mirror is shown in Fig. 3.14. First, note that the out-
put impedance looking into the drain of $Q_{2}$ is simply $r_{d s 2}$, which is seen using an analysis very similar to that which was used for the simple current mirror. Thus, the output impedance can be immediately derived by considering $Q_{4}$ as a current source with a source-degeneration resistor of value $r_{\mathrm{ds} 2}$. Making use of (3.32), and noting that $Q_{4}$ is now the cascode transistor rather than $Q_{2}$, we have

$$
\begin{equation*}
r_{\text {out }}=r_{d s 4}\left[1+R_{s}\left(g_{m 4}+g_{s 4}+g_{d s 4}\right)\right] \tag{3.36}
\end{equation*}
$$

where now $R_{s}=r_{d s 2}$. Therefore, the output impedance is given by

$$
\begin{align*}
r_{\text {out }} & =r_{d s 4}\left[1+r_{d s 2}\left(g_{m 4}+g_{s 4}+g_{d s 4}\right)\right] \\
& \cong r_{d s 4}\left[1+r_{d s 2}\left(g_{m 4}+g_{s 4}\right)\right]  \tag{3.37}\\
& \cong r_{d s 4}\left(r_{d s 2} g_{m 4}\right)
\end{align*}
$$

image_name:Fig. 3.14 A cascode current mirror
description:
[
name: I_in, type: CurrentSource, ports: {Np: VDD, Nn: P}
name: Q1, type: NMOS, ports: {S: GND, D: d1g3s3, G: d1g3s3}
name: Q2, type: NMOS, ports: {S: GND, D: s2s4, G: d1g3s3}
name: Q3, type: NMOS, ports: {S: d1g3s3, D: P, G: P}
name: Q4, type: NMOS, ports: {S: s2s4, D: Vout, G: P}
]
extrainfo:The circuit is a cascode current mirror, which increases the output impedance significantly. The cascode configuration is achieved by stacking transistors Q3 and Q4 on top of Q1 and Q2, respectively. This configuration improves the output impedance by a factor of g_{m4} r_{ds4}, enhancing the gain of the circuit.

Fig. 3.14 A cascode current mirror.

Thus, the output impedance has been increased by a factor of $g_{m 4} r_{d s 4}$, which is an upper limit on the gain of a single-transistor MOS gain-stage, and might be a value between 10 and 100 , depending on the transistor sizes and currents and the technology being used. This significant increase in output impedance can be instrumental in realizing singlestage amplifiers with large low-frequency gains.

The disadvantage in using a cascode current mirror is that it reduces the maximum output voltage swings possible before transistors enter the triode region. To understand this reduction, recall that for an n-channel transistor to be in the active region (also called the saturation or pinch-off region) its drain-source voltage must be greater than

Key Point: The addition of a cascode device to a CMOS current mirror increases its output resistance by approximately the gain of the cascode device, $\mathrm{g}_{\mathrm{m}} \mathrm{r}_{\mathrm{ds}}$. The voltage swing available at the current mirror output is reduced because some voltage drop must be maintained across the cascode device to keep it in active mode.

$$
\begin{equation*}
V_{\text {eff }} \equiv V_{G S}-V_{t n} \tag{3.38}
\end{equation*}
$$

which was shown in Chapter 1 to be given by

$$
\begin{equation*}
V_{\text {eff }}=\sqrt{\frac{2 I_{D}}{\mu_{n} C_{o x}(W / L)}} \tag{3.39}
\end{equation*}
$$

If we assume all transistors have the same sizes and currents, then they also all have the same $\mathrm{V}_{\text {eff }}$ and, therefore, the same gate-source voltages, $\mathrm{V}_{\mathrm{Gsi}}=\mathrm{V}_{\text {eff }}+\mathrm{V}_{\mathrm{tn}}$. Also, from Fig. 3.14, we see that

$$
\begin{equation*}
\mathrm{V}_{\mathrm{G} 3}=\mathrm{V}_{\mathrm{GS} 1}+\mathrm{V}_{\mathrm{GS} 3}=2 \mathrm{~V}_{\mathrm{eff}}+2 \mathrm{~V}_{\mathrm{tn}} \tag{3.40}
\end{equation*}
$$

and

$$
\begin{equation*}
V_{D S 2}=V_{G 3}-V_{G S 4}=V_{G 3}-\left(V_{\text {eff }}+V_{\mathrm{tn}}\right)=V_{\text {eff }}+V_{\mathrm{tn}} \tag{3.41}
\end{equation*}
$$

Thus, the drain-source voltage of $Q_{2}$ is larger than the minimum needed to place it at the edge of the active region. Specifically, the drain-source voltage of $\mathrm{Q}_{2}$ is $\mathrm{V}_{\mathrm{tn}}$ greater than what is required. Since the smallest output voltage, $V_{D 4}$, can be without $Q_{4}$ entering the triode region is given by $V_{D S 2}+V_{\text {eff }}$, the minimum allowed voltage for $V_{\text {out }}$ is given by

$$
\begin{equation*}
V_{\text {out }}>V_{D S 2}+V_{\text {eff }}=2 V_{\text {eff } 1}+V_{\text {tn }} \tag{3.42}
\end{equation*}
$$

which, again, is $\mathrm{V}_{\mathrm{tn}}$ greater than the minimum value of $2 \mathrm{~V}_{\text {eff }}$. This loss of signal swing is a serious disadvantage when modern technologies are used that might have a maximum allowed power-supply voltage as small as 1 V . In Section 6.3 , we will see how the cascode current mirror can be modified to maintain large output impedances and yet still allow for near minimum voltages at the output of the mirror.

### EXAMPLE 3.7

Consider the cascode current mirror shown in Fig. 3.14, where $\mathrm{I}_{\mathrm{in}}=100 \mu \mathrm{~A}$ and each transistor has $\mathrm{W} / \mathrm{L}=10 \mu \mathrm{~m} / 0.4 \mu \mathrm{~m}$. Given the $0.35-\mu \mathrm{m}$ CMOS device parameters in Table 1.5, find $\mathrm{r}_{\text {out }}$ for the current mirror (approximating the body effect by $0.2 \mathrm{~g}_{\mathrm{m}}$ ). Also find the minimum output voltage at $\mathrm{V}_{\text {out }}$ such that the output transistors remain in the active region.

### Solution

Nominally, $\mathrm{I}_{\mathrm{out}}=\mathrm{I}_{\mathrm{in}}$, and thus we can find the small-signal parameters for this current mirror to be

$$
\begin{equation*}
\mathrm{g}_{\mathrm{m} 4}=\sqrt{2 \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L}) \mathrm{I}_{\mathrm{out}}}=0.97 \mathrm{~mA} / \mathrm{V} \tag{3.43}
\end{equation*}
$$

We also have

$$
\begin{equation*}
r_{\mathrm{ds} 2}=r_{\mathrm{ds} 4}=\frac{0.4 \mu \mathrm{~m}}{0.16 \mu \mathrm{~m} / \mathrm{V} 100 \mu \mathrm{~A}}=25 \mathrm{k} \Omega \tag{3.44}
\end{equation*}
$$

Now, making use of (3.37), the output impedance is given by

$$
\begin{equation*}
\mathrm{r}_{\text {out }}=25 \mathrm{k} \Omega[25 \mathrm{k} \Omega(0.97 \mathrm{~mA} / \mathrm{V}+0.2 \times 0.97 \mathrm{~mA} / \mathrm{V}+1 / 25 \mathrm{k} \Omega)]=753 \mathrm{k} \Omega \tag{3.45}
\end{equation*}
$$

To find the minimum output voltage, we first need to determine $\mathrm{V}_{\text {eff }}$ :

$$
\begin{equation*}
\mathrm{V}_{\mathrm{eff}}=\sqrt{\frac{2 \mathrm{I}_{\mathrm{out}}}{\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L})}}=0.205 \mathrm{~V} \tag{3.46}
\end{equation*}
$$

Thus, the minimum output voltage is determined to be $2 \mathrm{~V}_{\text {eff }}+\mathrm{V}_{\mathrm{tn}}=0.98 \mathrm{~V}$. Hence, compared with the simple current mirror with the same current and transistors in Example 3.1, the output resistance is increased by a factor of 30 , but the voltage swing available at the output is decreased by 0.76 V .

## 3.7 CASCODE GAIN STAGE

In modern IC design, a commonly used configuration for a single-stage amplifier is a cascode configuration. This configuration consists of a common-source-connected transistor feeding into a common-gate-connected transistor. Two examples of cascode amplifiers are shown in Fig. 3.15. The configuration in Fig. 3.15(a) has both an n-channel common-source transistor, $\mathrm{Q}_{1}$, and an n -channel common-gate cascode transistor, $\mathrm{Q}_{2}$. This configuration is sometimes called a telescopic-cascode amplifier. The configuration shown in Fig. 3.15(b) has an n-channel input (or drive) transistor, but a p -channel transistor is used for the cascode (or common-gate) transistor. This configuration is usually called a folded-cascode stage. When incorporated into an operational amplifier, the folded cascode can provide greater output swing than the telescopic cascode. However, the folded cascode usually consumes more power since the drain bias currents for $Q_{1}$ and $Q_{2}$ are drawn in parallel from the supply voltage, whereas in the telescopic cascode the same dc drain current is shared by both transistors.

There are two major reasons for the popularity of cascode stages. The first is that they can have quite large gain for a single stage due to the large impedances at the output. To enable this high gain, the current sources connected to the output nodes are realized using high-quality cascode current mirrors. The second major reason for the use of cascode stages is that they limit the voltage across the input drive transistor. This minimizes any shortchannel effects, which becomes more important with modern technologies having very short channel-length transistors. It can also permit the circuit to handle higher output voltages without risking damage to the common-source transistor.

Key Point: The cascode gain stage uses a common-gate transistor $\mathrm{Q}_{2}$ to reduce the $\mathrm{V}_{\mathrm{DS}}$ variations on a common-source transistor $\mathrm{Q}_{1}$. The result is high output resistance providing potentially high gain and reduced short-channel effects. However, the available output voltage swing is reduced.
image_name:(a)
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: d1s2, G: Vin}
name: Q2, type: NMOS, ports: {S: d1s2, D: Vout, G: Vbias}
name: Ibias, type: CurrentSource, value: Ibias, ports: {Np: VDD, Nn: Vout}
]
extrainfo:The circuit diagram (a) is a telescopic-cascode amplifier. It uses a common-gate transistor Q2 to reduce V_DS variations on a common-source transistor Q1, resulting in high output resistance and potentially high gain. The diagram shows a current source Ibias connected to the output node Vout, providing biasing for the amplifier.
image_name:(b)
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: P1, G: Vin}
name: Q2, type: PMOS, ports: {S: P1, D: Vout, G: Vbias}
name: Ibias1, type: CurrentSource, value: Ibias1, ports: {Np: LOAD, Nn: P1}
name: Ibias2, type: CurrentSource, value: Ibias2, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a folded-cascode amplifier configuration. It uses an NMOS transistor Q1 and a PMOS transistor Q2. The current sources Ibias1 and Ibias2 provide biasing for the circuit, and the output is taken from the node labeled Vout.

Fig. 3.15 (a) A telescopic-cascode amplifier and (b) a folded-cascode amplifier.

The main drawback of cascode amplifiers is that the output voltage is restricted to a narrower range than the common-source amplifier in order to keep all devices in the active region. This is because some voltage must be kept between drain and source of the extra cascode transistor, $Q_{2}$.

### EXAMPLE 3.8

For the telescopic cascode gain stage pictured in Fig. 3.15(a), what is the minimum voltage that can appear at $\mathrm{v}_{\text {out }}$ while keeping both $Q_{1}$ and $Q_{2}$ in the active region? How does this compare with the common-source amplifier in, for example, Fig. 3.4? Assume that all transistors are biased with $V_{\text {eff }}=250 \mathrm{mV}$.

### Solution

In order to keep $Q_{1}$ in active mode, a voltage of at least $V_{\text {eff }}$ is required at the drain of $Q_{1}$. Hence,

$$
\begin{equation*}
\mathrm{V}_{\text {bias }} \geq \mathrm{V}_{\mathrm{eff}, 1}+\mathrm{V}_{\mathrm{GS}, 2}=2 \mathrm{~V}_{\mathrm{eff}}+\mathrm{V}_{\mathrm{tn}} \tag{3.47}
\end{equation*}
$$

The absolute minimum voltage possible at $\mathrm{V}_{\text {out }}$ is achieved by taking the minimum possible value for $\mathrm{V}_{\text {bias }}$ allowed by (3.47). Since $\mathrm{V}_{\text {out }}$ may be at most one threshold voltage below $\mathrm{V}_{\text {bias }}$, it is required that

$$
\begin{equation*}
V_{\text {out }} \geq 2 \mathrm{~V}_{\text {eff }}=500 \mathrm{mV} \tag{3.48}
\end{equation*}
$$

In practice, a significant margin is provided beyond this value since the exact values of $\mathrm{V}_{\mathrm{tn}}$ and $\mathrm{V}_{\text {eff }}$ are not known.
In the common-source amplifier of Fig. 3.4, there is only one transistor between $\mathrm{V}_{\text {out }}$ and ground $\left(Q_{1}\right)$. Hence, the output can drop to within one $\mathrm{V}_{\text {eff }}$ of ground, or just 250 mV . The additional 250 mV of swing provided by the com-mon-source amplifier compared with a cascode amplifier can be very significant when operating with low supply voltages. This is a major reason why common-source amplifiers are often used as the output stage of operational amplifiers.

The small-signal analysis of the telescopic cascode gain stage of Fig. 3.15(a) will next be described. The same analysis, with only minor modifications, also applies for the folded-cascode stage of Fig. 3.15(b). A smallsignal schematic for the analysis is shown in Fig. 3.16, where the transistor symbols remain as shorthand for their complete small-signal models.

It is useful to know the small-signal resistances at several points in the circuit, which are defined in Fig. 3.16. From the section on cascode current-mirrors, we know that the impedance looking into the drain of cascode

Fig. 3.16 A small-signal equivalent circuit of the telescopic cascode amplifier where MOS transistor symbols are used as shorthand for their small-signal models.
image_name:Fig. 3.16
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: Vs2, G: Vin}
name: Q2, type: NMOS, ports: {S: Vs2, D: Vout, G: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: G1}
name: VS2, type: VoltageSource, value: VS2, ports: {Np: Vs2, Nn: G1}
]
extrainfo:The circuit is a telescopic cascode amplifier with two NMOS transistors Q1 and Q2. Q1 is configured as a common-source amplifier, and Q2 is configured as a cascode transistor. The output resistance is defined by the parallel combination of the drain resistance of Q2 and the load resistance RL.

transistor $Q_{2}$ is approximately given by

$$
\begin{equation*}
r_{\mathrm{d} 2} \cong g_{\mathrm{m} 2} r_{\mathrm{ds} 1} r_{\mathrm{ds} 2} \tag{3.49}
\end{equation*}
$$

The total output resistance will be

$$
\begin{equation*}
R_{\text {out }}=r_{d 2} \| R_{L} \tag{3.50}
\end{equation*}
$$

where $R_{L}$ is the output impedance of the bias current source, $I_{\text {bias }}$. We found earlier that the low-frequency admittance looking into the source of the common-gate or cascode transistor, $Q_{2}$, is ${ }^{2}$

$$
\begin{equation*}
g_{\text {in } 2}=1 / r_{\mathrm{in} 2}=\frac{g_{\mathrm{m} 2}+g_{\mathrm{s} 2}+g_{\mathrm{ds} 2}}{1+\frac{\mathrm{R}_{\mathrm{L}}}{r_{\mathrm{ds} 2}}} \cong \frac{g_{\mathrm{m} 2}}{1+\frac{\mathrm{R}_{\mathrm{L}}}{r_{\mathrm{ds} 2}}} \tag{3.51}
\end{equation*}
$$

The gain from the input to the source of $\mathrm{Q}_{2}$ is simply that of a common-source amplifier with a load resistance of $r_{\text {in } 2}$ and is therefore given by

$$
\begin{equation*}
\frac{v_{s 2}}{v_{\mathrm{in}}}=-g_{\mathrm{m} 1}\left(r_{\mathrm{ds} 1} \| r_{\mathrm{in} 2}\right)=-\frac{g_{\mathrm{m} 1}}{g_{\mathrm{ds} 1}+g_{\mathrm{in} 2}} \tag{3.52}
\end{equation*}
$$

The gain from the source of $Q_{2}$ to the output is simply that derived earlier for the common-gate stage.

$$
\begin{align*}
& \frac{v_{\text {out }}}{v_{\mathrm{s} 2}}=\frac{g_{\mathrm{m} 2}+g_{\mathrm{s} 2}+g_{\mathrm{ds} 2}}{g_{\mathrm{ds} 2}+G_{\mathrm{L}}}  \tag{3.53}\\
& \quad \cong g_{\mathrm{m} 2}\left(r_{\mathrm{ds} 2} \| R_{\mathrm{L}}\right)=\frac{g_{\mathrm{m} 2}}{\left(g_{\mathrm{ds} 2}+G_{\mathrm{L}}\right)}
\end{align*}
$$

The overall gain is the product of (3.52) and (3.53).

$$
\begin{equation*}
A_{V}=\frac{v_{\mathrm{s} 2}}{v_{\text {in }}} \frac{v_{\text {out }}}{v_{2}} \cong-g_{m 1} g_{m 2}\left(r_{\mathrm{ds} 1} \| r_{\text {in } 2}\right)\left(r_{\mathrm{ds} 2} \| R_{\mathrm{L}}\right) \tag{3.54}
\end{equation*}
$$

The reader should be cautioned that (3.54) is only approximate primarily due to the difficulty of accurately determining the output resistance $r_{d s}$ for the different transistors. For example, one problem in estimating $r_{d s}$ is that it is voltage-dependent. Therefore, prudent designers should never create a design where successful operation is dependent on knowing the gain accurately rather than just knowing it will be greater than some minimum value.

### EXAMPLE 3.9

Find approximate expressions for the gain and output resistance of the cascode stage in Fig. 3.15(a) assuming $\mathrm{I}_{\text {bias }}$ is a simple current source with an output impedance on the order of

$$
\begin{equation*}
R_{L} \approx r_{d s-p} \tag{3.55}
\end{equation*}
$$

Compute approximate numerical results assuming all transistors have $\mathrm{g}_{\mathrm{m}}$ on the order of $0.5 \mathrm{~mA} / \mathrm{V}$ and $\mathrm{r}_{\mathrm{ds}}$ on the order of $100 \mathrm{k} \Omega$.

[^3]
### Solution

We shall drop the indices for all small-signal values under the assumption that the transistors are somewhat matched and to simplify matters since we are only deriving an approximate answer.

The resistance looking into the source of $Q_{2}$ is obtained by substituting (3.55) into (3.51).

$$
\begin{equation*}
\mathrm{g}_{\mathrm{in} 2} \approx \frac{1}{2} \mathrm{~g}_{\mathrm{m}} \Rightarrow \mathrm{r}_{\mathrm{in} 2} \approx \frac{2}{\mathrm{~g}_{\mathrm{m}}} \tag{3.56}
\end{equation*}
$$

Assuming $r_{\mathrm{ds} 1}$ is much larger than $\mathrm{r}_{\mathrm{in} 2}$, the gain from the input to the source of $\mathrm{Q}_{2}$ simplifies to

$$
\begin{equation*}
\frac{v_{s} 2}{v_{i n}} \approx-\frac{g_{m}}{g_{m} / 2}=-2 \tag{3.57}
\end{equation*}
$$

For instance, compared with a common-source amplifer assuming the same numerical values for the transistor small-signal parameters, $\left(\mathrm{v}_{\mathrm{s} 2} / \mathrm{v}_{\mathrm{in}}\right)$ has decreased from -25 to -2 . The gain of the common-gate stage also decreases. Substituting (3.55) into (3.53) gives

$$
\begin{equation*}
\frac{v_{\text {out }}}{v_{\mathrm{s} 2}} \approx \frac{1}{2} g_{\mathrm{m}} r_{\mathrm{ds}} \tag{3.58}
\end{equation*}
$$

Hence, the overall gain is,

$$
\begin{equation*}
A_{V}=\frac{v_{\mathrm{s} 2}}{v_{\text {in }}} \cdot \frac{v_{\text {out }}}{v_{s 2}} \approx-g_{m} r_{d s} \tag{3.59}
\end{equation*}
$$

Since $R_{L}$ « $r_{d 2}$, the output resistance is now dominated by (3.55).

$$
\begin{equation*}
\mathrm{R}_{\mathrm{out}} \approx \mathrm{r}_{\mathrm{ds}} \tag{3.60}
\end{equation*}
$$

The corresponding numerical results are $A_{V} \approx-50$ or 34 dB and $R_{\text {out }} \approx 100 \mathrm{k} \Omega$, The gain in this case is, in fact, only a factor of 2 larger than would be obtained with a common-source amplifier (i.e. excluding $Q_{2}$ ). Notice that almost all of the gain appears across the common-gate transistor, $\mathrm{Q}_{2}$.

The cascode amplifier is most often used in analog integrated circuits to provide a large low-frequency gain from a single stage. Considering equation (3.50), this may only be done if $R_{L}$ is large. Since $R_{L}$ is the output resistance of the current source, $\mathrm{I}_{\text {bias }}$ should be a high-quality current source whose output resistance is on the order of $\mathrm{R}_{\mathrm{L}} \approx \mathrm{g}_{\mathrm{m}-\mathrm{p}} \mathrm{r}_{\mathrm{d} \text { sp-p }}^{2}$.

We shall now obtain expressions for the gain and output resistance in this case using the results of our previous analysis and dropping all indices to obtain an approximate result. Substituting $R_{L} \approx \mathrm{~g}_{\mathrm{m}} \mathrm{r}_{\mathrm{ds}}^{2}$ into (3.51) reveals that the conductance looking into the source of $\mathrm{Q}_{2}$ is

$$
\begin{gather*}
g_{\mathrm{in} 2}=1 / r_{\mathrm{in} 2} \approx \frac{g_{\mathrm{m}}}{1+g_{\mathrm{ds}} g_{\mathrm{m}} r_{\mathrm{ds}}^{2}} \cong g_{\mathrm{ds}}  \tag{3.61}\\
\Rightarrow \mathrm{r}_{\mathrm{in} 2} \approx \mathrm{r}_{\mathrm{ds}}
\end{gather*}
$$

Therefore, the gain from the input to $\mathrm{v}_{\mathrm{s} 2}$ in (3.52) may be simplified to,

$$
\begin{equation*}
\frac{\mathrm{v}_{\mathrm{s} 2}}{\mathrm{v}_{\mathrm{in}}} \approx-\frac{1}{2} \mathrm{~g}_{\mathrm{m}} \mathrm{r}_{\mathrm{ds}} \tag{3.62}
\end{equation*}
$$

and since $R_{L}$ » $r_{d s 2}$, the gain from $v_{s 2}$ to the output in (3.53) becomes simply

$$
\begin{equation*}
\frac{v_{\text {out }}}{v_{\mathrm{s} 2}} \approx g_{\mathrm{m}} r_{\mathrm{ds}} \tag{3.63}
\end{equation*}
$$

The approximate overall gain is the product of (3.62) and (3.63),

$$
\begin{equation*}
A_{v} \approx-\frac{1}{2} g_{m}^{2} r_{d s}^{2}=-\frac{1}{2}\left(\frac{g_{m}}{g_{d s}}\right)^{2} \tag{3.64}
\end{equation*}
$$

The output resistance is

$$
\begin{equation*}
\mathrm{R}_{\mathrm{out}}=\mathrm{R}_{\mathrm{L}} \| \mathrm{r}_{\mathrm{d} 2} \approx \frac{1}{2} \mathrm{~g}_{\mathrm{m}} \mathrm{r}_{\mathrm{ds}}^{2} \tag{3.65}
\end{equation*}
$$

### EXAMPLE 3.10

Compare the gain and output resistance of the cascode amplifier with a high-quality current source to the values obtained in Example 3.9 where a simple current source was assumed. As in Example 3.9, assume all transistors have $\mathrm{g}_{\mathrm{m}}$ on the order of $0.5 \mathrm{~mA} / \mathrm{V}$ and $\mathrm{r}_{\mathrm{ds}}$ on the order of $100 \mathrm{k} \Omega$.

### Solution

Substituting the numerical values into equation (3.65) yields $A_{v} \approx-1250$, a very large gain from a single amplifier stage. The output resistance is huge, $R_{\text {out }} \approx 2.5 \mathrm{M} \Omega$. These are both over an order of magnitude larger than the values $A_{v} \approx-50$ and $R_{\text {out }} \approx 100 \mathrm{k} \Omega$ obtained in Example 3.9 ; the values have been effectively magnified by the gain of the common-gate transistor $Q_{2}$.

## 3.8 MOS DIFFERENTIAL PAIR AND GAIN STAGE

Most integrated amplifiers have a differential input. To realize this differential input, almost all amplifiers use what is commonly called a differential transistor pair. A differential pair together with a biasing current source is shown in Fig. 3.17. The transistors $\mathrm{Q}_{1}$ and $\mathrm{Q}_{2}$ are sized identically and are biased with the same dc gate voltage. A low-frequency, smallsignal model of the differential pair is shown in Fig. 3.18. This small-signal equivalent circuit is based on the T model for a MOS transistor that was described in Chapter 1. To simplify the analysis, we ignore the output impedance of the transistors temporarily. Defining the differential input voltage as $\mathrm{v}_{\mathrm{in}} \equiv \mathrm{v}^{+}-\mathrm{v}^{-}$, we have
image_name:Fig. 3.17 A MOS differential pair
description:
[
name: Q1, type: NMOS, ports: {S: P, D: LOAD2, G: V+}
name: Q2, type: NMOS, ports: {S: P, D: LOAD3, G: V-}
name: I_bias, type: CurrentSource, ports: {Np: P, Nn: LOAD1}
]
extrainfo:The circuit is a MOS differential pair with two NMOS transistors Q1 and Q2, sharing a common source node P. The transistors are biased with a current source I_bias, and two current sources P2 and P3 are connected to the drains of Q1 and Q2, respectively. The differential input is applied between V+ and V-.

Fig. 3.17 A MOS differential pair.

$$
\begin{equation*}
i_{d 1}=i_{s 1}=\frac{v_{i n}}{r_{\mathrm{s} 1}+r_{\mathrm{s} 2}}=\frac{v_{\text {in }}}{1 / g_{\mathrm{m} 1}+1 / g_{\mathrm{m} 2}} \tag{3.66}
\end{equation*}
$$

image_name:Fig. 3.18 The small-signal model of a MOS differential pair.
description:
[
name: rs1, type: Resistor, value: rs1, ports: {N1: V+, N2: p}
name: rs2, type: Resistor, value: rs2, ports: {N1: V-, N2: p}
name: LOAD2, type: CurrentControlledCurrentSource, ports: {Np: V+, Nn: VDD}
name: LOAD3, type: CurrentControlledCurrentSource, ports: {Np: V-, Nn: VDD}
]
extrainfo:This circuit is a small-signal model of a MOS differential pair with two resistors and two current-controlled current sources. The differential input is applied between V+ and V-, and the common node is labeled as p.

Fig. 3.18 The small-signal model of a MOS differential pair.

Since both $Q_{1}$ and $Q_{2}$ have the same bias currents, $g_{m 1}=g_{m 2}$. Therefore, we find

$$
\begin{equation*}
\mathrm{i}_{\mathrm{d} 1}=\frac{\mathrm{g}_{\mathrm{m} 1}}{2} \mathrm{v}_{\mathrm{in}} \tag{3.67}
\end{equation*}
$$

Also, since $i_{\mathrm{d} 2}=i_{\mathrm{s} 2}=-\mathrm{i}_{\mathrm{d} 1}$, we find that

$$
\begin{equation*}
\mathrm{i}_{\mathrm{d} 2}=-\frac{\mathrm{g}_{\mathrm{m} 1}}{2} \mathrm{v}_{\mathrm{in}} \tag{3.68}
\end{equation*}
$$

Finally, defining a differential output current, $i_{\text {out }} \equiv i_{d 1}-i_{d 2}$, the following relationship is obtained:

$$
\begin{equation*}
\mathrm{i}_{\text {out }}=\mathrm{g}_{\mathrm{m} 1} \mathrm{v}_{\mathrm{in}} \tag{3.69}
\end{equation*}
$$

Key Point: The differential pair with active load is classically the first stage of a twostage operational amplifier. It accepts a differential input and produces a single-ended output with a gain comparable to that of a common-source stage.

If two resistive loads $R_{L}$ are connected between the drains of $Q_{1}$ and $Q_{2}$ and a positive supply, the result is a differential output voltage between the two drain nodes, $\mathrm{v}_{\text {out }}=\left(g_{m 1} R_{L}\right) v_{\text {in }}$ and the stage has a differential small-signal gain of $g_{m 1} R_{L}$.

If a differential pair has a current mirror as an active load, a complete differential-input, single-ended-output gain stage can be realized, as shown in Fig. 3.19. This circuit is the typical first gain stage of a classical two-stage integrated opamp; in this case, the input differential pair is realized using $n$-channel transistors and the active current-mirror load is realized using p-channel transistors. From the small-signal analysis of the differential pair, we have

$$
\begin{equation*}
i_{d 1}=i_{s 1}=\frac{g_{m 1}}{2} v_{i n} \tag{3.70}
\end{equation*}
$$

Also, ignoring transistor output impedances, we have

$$
\begin{equation*}
\mathrm{i}_{\mathrm{d} 4}=\mathrm{i}_{\mathrm{d} 3}=-\mathrm{i}_{\mathrm{s} 1} \tag{3.71}
\end{equation*}
$$

image_name:Fig. 3.19 A differential-input, single-ended-output MOS gain stage.
description:
[
name: Q1, type: NMOS, ports: {S: P, D: X, G: Vip}
name: Q2, type: NMOS, ports: {S: P, D: Vout, G: Vin}
name: Q3, type: PMOS, ports: {S: VDD, D: X, G: X}
name: Q4, type: PMOS, ports: {S: VDD, D: Vout, G: X}
name: Ibias, type: CurrentSource, ports: {Np: VDD, Nn: P}
]
extrainfo:The circuit is a differential-input, single-ended-output MOS gain stage with an active current-mirror load. The input differential pair is realized using NMOS transistors (Q1 and Q2), and the active current-mirror load is realized using PMOS transistors (Q3 and Q4). The bias current source (Ibias) sets the operating point of the differential pair.

Fig. 3.19 A differential-input, single-ended-output MOS gain stage.

Note that a positive small-signal current is defined as the current going into the drain of a transistor. Using (3.71) and the fact that $i_{\mathrm{d} 2}=-i_{\mathrm{s} 1}$, we have

$$
\begin{equation*}
v_{\text {out }}=\left(-i_{d 2}-i_{d 4}\right) r_{\text {out }}=2 i_{s 1} r_{\text {out }}=g_{m 1} r_{\text {out }} v_{\text {in }} \tag{3.72}
\end{equation*}
$$

The evaluation of the output resistance, $r_{\text {out }}$, is determined by using the small-signal equivalent circuit and applying a voltage to the output node, as seen in Fig. 3.20. Note that the T model was used for both $Q_{1}$ and $Q_{2}$, whereas $Q_{3}$ was replaced by an equivalent resistance (since it is diode-connected), and the hybrid- $\pi$ model was used for $Q_{4}$. As usual, $r_{\text {out }}$ is defined as the ratio $v_{x} / i_{x}$, where $i_{x}$ is given by the sum $i_{\mathrm{x}}=\mathrm{i}_{\mathrm{x} 1}+\mathrm{i}_{\mathrm{x} 2}+\mathrm{i}_{\mathrm{x} 3}+\mathrm{i}_{\mathrm{x} 4}$. Clearly,

$$
\begin{equation*}
\mathrm{i}_{\mathrm{x} 1}=\frac{\mathrm{v}_{\mathrm{x}}}{\mathrm{r}_{\mathrm{ds} 4}} \tag{3.73}
\end{equation*}
$$

image_name:Fig. 3.20
description:
[
name: r_ds3 || r_s3, type: Resistor, value: r_ds3 || r_s3, ports: {N1: GND, N2: Va}
name: d1, type: Diode, ports: {Na: Va, Nc: GND}
name: r_ds1, type: Resistor, value: r_ds1, ports: {N1: Va, N2: s1}
name: r_s1, type: Resistor, value: r_s1, ports: {N1: s1, N2: GND}
name: r_ds4, type: Resistor, value: r_ds4, ports: {N1: GND, N2: vx}
name: g_m4 v_a, type: VoltageControlledCurrentSource, ports: {Np: vx, Nn: vx}
name: r_ds2, type: Resistor, value: r_ds2, ports: {N1: vx, N2: s2}
name: r_s2, type: Resistor, value: r_s2, ports: {N1: s2, N2: GND}
name: v_x, type: VoltageSource, value: v_x, ports: {Np: vx, Nn: GND}
]
extrainfo:This circuit is a small-signal model for calculating the output impedance of a differential-input, single-ended-output MOS gain stage. It includes resistors, a diode, a voltage-controlled current source, and a voltage source. The circuit is designed to analyze the behavior of currents i_x1, i_x2, i_x3, and i_x4 in relation to the output voltage v_x.

Fig. 3.20 The small-signal model for the calculation of the output impedance of the differentialinput, single-ended-output MOS gain stage.
implying that the resistance seen in the path taken by $i_{x 1}$ is equal to $r_{d s 4}$. Now, assuming that the effect of $r_{d s 1}$ can be ignored (since it is much larger than $r_{s 1}$ ), we see that the current $i_{x 2}$ is given by

$$
\begin{equation*}
i_{x 2} \cong \frac{v_{x}}{r_{d s 2}+\left(r_{s 1} \| r_{s 2}\right)} \cong \frac{v_{x}}{r_{d s} 2} \tag{3.74}
\end{equation*}
$$

where the second approximation is valid, since $r_{d s 2}$ is typically much greater than $r_{s 1} \| r_{s 2}$. This $i_{\mathrm{x} 2}$ current splits equally between $i_{s 1}$ and $i_{s 2}$ (assuming $r_{s 1}=r_{s 2}$ and once again ignoring $r_{d s 1}$ ), resulting in

$$
\begin{equation*}
\mathrm{i}_{\mathrm{s} 1}=\mathrm{i}_{\mathrm{s} 2}=\frac{-\mathrm{v}_{\mathrm{x}}}{2 \mathrm{r}_{\mathrm{ds} 2}} \tag{3.75}
\end{equation*}
$$

However, since the current mirror realized by $Q_{3}$ and $Q_{4}$ results in $i_{x 4}=i_{x 5}$ (assuming $g_{m 4}=1 / r_{s 4}=1 / r_{s 3}$ and $r_{d s 3}$ is much larger than $r_{s 3}$ ), the current $i_{x 4}$ is given by

$$
\begin{equation*}
i_{x 4}=-i_{s 1}=-i_{s 2}=-i_{x 3} \tag{3.76}
\end{equation*}
$$

In other words, when the current splits equally between $r_{s 1}$ and $r_{s 2}$, the current mirror of $Q_{3}$ and $Q_{4}$ causes the two currents $i_{x 3}$ and $i_{x 4}$ to cancel each other. Finally, the output resistance, $r_{o u t}$, is given by

$$
\begin{equation*}
r_{\text {out }}=\frac{v_{x}}{i_{x 1}+i_{x 2}+i_{x 3}+i_{x 4}}=\frac{v_{x}}{\left(v_{x} / r_{d s 4}\right)+\left(v_{x} / r_{d s 2}\right)} \tag{3.77}
\end{equation*}
$$

which results in the simple relationship

$$
\begin{equation*}
r_{\text {out }}=r_{\mathrm{ds} 2} \| r_{\mathrm{ds} 4} \tag{3.78}
\end{equation*}
$$

Therefore, at low frequencies the gain, $A_{v}$, is given by

$$
\begin{equation*}
A_{v}=g_{m 1}\left(r_{d s 2} \| r_{d s 4}\right) \tag{3.79}
\end{equation*}
$$

### EXAMPLE 3.11

Consider the gain stage shown in Fig. 3.19, where $\mathrm{I}_{\text {bias }}=200 \mu \mathrm{~A}$ and all transistors have $\mathrm{W} / \mathrm{L}=20 \mu \mathrm{~m} / 0.4 \mu \mathrm{~m}$. Given the transistor parameters for the $0.18 \mu \mathrm{~m}$ technology in Table 1.5, find the output impedance, $r_{\text {out }}$, and the gain from the differential input to the output, $\mathrm{V}_{\text {out }}$.

### Solution

To find the bias currents, we assume that $\mathrm{I}_{\text {bias }}$ splits evenly between the two sides of the differential circuit, resulting in

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D} 1}=\mathrm{I}_{\mathrm{D} 2}=\mathrm{I}_{\mathrm{D} 3}=\mathrm{I}_{\mathrm{D} 4}=100 \mu \mathrm{~A} \tag{3.80}
\end{equation*}
$$

Therefore, the transconductance of the input transistors is equal to

$$
\begin{equation*}
\mathrm{g}_{\mathrm{m} 1}=\mathrm{g}_{\mathrm{m} 2}=\sqrt{2 \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L})\left(\mathrm{I}_{\text {bias }} / 2\right)}=1.64 \mathrm{~mA} / \mathrm{V} \tag{3.81}
\end{equation*}
$$

The output impedance of $Q_{2}$ and $Q_{4}$ is given by

$$
\begin{equation*}
r_{d s 2}=r_{d s 4}=\frac{0.4}{0.08 \times 0.1}=50 \mathrm{k} \Omega \tag{3.82}
\end{equation*}
$$

Thus, the gain for this stage is

$$
\begin{equation*}
A_{v} \equiv \frac{v_{\text {out }}}{v_{\text {in }}}=g_{\mathrm{m} 1}\left(r_{\mathrm{ds} 2} \| r_{\mathrm{ds} 4}\right)=41 \mathrm{~V} / \mathrm{V} \tag{3.83}
\end{equation*}
$$

## 3.9 KEY POINTS

- A simple CMOS current mirror has a small-signal input resistance of $1 / g_{m 1}$ and a small-signal output resistance $r_{\text {ds2. }}$ [p. 119]
- The common-source amplifier is a popular gain stage, especially when high input impedance is desired. The use of an active load takes advantage of the nonlinear, large-signal transistor current-voltage relationship to provide large small-signal resistances without large dc voltage drops. [p. 120]
- The source-follower provides a voltage gain close to unity, and often limited by the body effect. It can provide a large current gain and it is unilateral so it is often used as a voltage buffer. [p. 122]
- The common-gate amplifier provides a voltage gain comparable to that of the common-source amplifier, but with a relatively low input resistance on the order of $1 / \mathrm{g}_{\mathrm{m}}$. However, the input resistance can be larger when the amplifier has a large small-signal load resistance. [p. 126]
- When a small-signal resistance $R_{s}$ is introduced at the source of both transistors in a simple current mirror, the output resistance is increased by a factor approximately equal to ( $1+R_{s} g_{m}$ ). [p. 128]
- The addition of a cascode device to a CMOS current mirror increases its output resistance by approximately the gain of the cascode device, $g_{m} r_{d s}$. The voltage swing available at the current mirror output is reduced because some voltage drop must be maintained across the cascode device to keep it in active mode. [p. 129]
- The cascode gain stage uses a common-gate transistor $Q_{2}$ to reduce the $V_{D S}$ variations on a common-source transistor $Q_{1}$. The result is high output resistance providing potentially high gain and reduced short-channel effects. However, the available output voltage swing is reduced. [p. 131]
- The differential pair with active load is classically the first stage of a two-stage operational amplifier. It accepts a differential input and produces a single-ended output with a gain comparable to that of a common-source stage. [p. 136]
