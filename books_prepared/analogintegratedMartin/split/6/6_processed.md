# 6. Basic Opamp Design and Compensation

This chapter describes the fundamental principles of basic opamp design. To illustrate many of these principles, the design of a traditional opamp-namely, the two-stage CMOS opamp-is used first. This example illustrates compensation techniques needed to ensure stability in closed-loop amplifiers as well as a number of other important design techniques, such as ensuring zero systematic input-offset-voltage and process-insensitive lead compensation.

Although the two-stage CMOS opamp is a classic circuit used in many integrated circuits, other architectures have gained popularity. A few of the most important applications of opamps in analog integrated circuits are illustrated in Fig. 6.1. Note that in many cases, the loads being driven by the opamp are purely capacitive. This fact may be used to advantage by designing opamps to have high output impedances, providing large voltage gain in a single stage with relatively low power consumption. Opamps exemplifying this approach are described later in the chapter. However, one should not overlook the potential of the two-stage opamp, which is well-suited to lowvoltage applications since it does not require a cascode output stage. Fully-differential opamps are also described.

## 6.1 TWO-STAGE CMOS OPAMP

The two-stage circuit architecture has historically been the most popular approach to opamp design. When properly designed, the two-stage opamp has a performance very close to designs that employ cascode stages and is somewhat more suitable when resistive loads need to be driven. ${ }^{1}$ It can provide a high gain and high output swing, making it an important circuit for advanced CMOS technologies where transistor intrinsic gain and supply voltages may be limited. Furthermore, it is an excellent example to illustrate many important design concepts that are also directly applicable to other designs.
image_name:(a)
description:
[
name: C, type: Capacitor, value: C, ports: {Np: Out(A1), Nn: InN(A1)}
name: R1, type: Resistor, value: R1, ports: {N1: Out(A1), N2: InN(A1)}
name: R2, type: Resistor, value: R2, ports: {N1: Vin, N2: InN(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Out(A1), OutN: ''}
]
extrainfo:The circuit diagram (a) is an opamp-based amplification and filtering circuit. It uses a feedback loop with a capacitor C and resistors R1 and R2 to set the gain and frequency response.
image_name:(b)
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Vreg, InN: Vin, OutP: , OutN:}
name: M1, type: NMOS, ports: {S: GND, D: VDD, G: Out(A1)}
]
extrainfo:This circuit diagram (b) shows an op-amp A1 configured with an NMOS transistor M1. The op-amp receives input at Vin and Vreg, with its output controlling the gate of M1. The NMOS transistor M1 is connected to VDD and GND, forming a basic voltage regulation circuit.
image_name:(c)
description:
[
name: SW1, type: Switch, ports: {N1: Vin, N2: X1}
name: SW2, type: Switch, ports: {N1: X2, N2: InN(A1)}
name: SW3, type: Switch, ports: {N1: X1, N2: GND}
name: SW4, type: Switch, ports: {N1: X2, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: InN(A1)}
name: C2, type: Capacitor, value: C2, ports: {Np: X1, Nn: X2}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Vout}
]
extrainfo:The circuit diagram (c) is a switched-capacitor circuit using an op-amp. It includes two capacitors (C1 and C2) and four switches (SW1, SW2, SW3, SW4) to control the charging and discharging paths of the capacitors. This configuration is typical for sampling and filtering applications in analog integrated circuits.

Fig. 6.1 Typical applications of opamps in analog integrated circuits: (a) amplification and filtering; (b) biasing and regulation; (c) switched-capacitor circuits.

[^3]A block diagram of a typical two-stage CMOS opamp is shown in Fig. 6.2. "Twostage" refers to the number of gain stages in the opamp. Fig. 6.2 actually shows three stages - two gain stages and a unity-gain output stage. The output buffer is normally present only when resistive loads need to be driven. If the load is purely capacitive, then it is seldom included. The first gain stage is a differential-input single-ended output stage, often very similar to that shown in Fig. 3.19. The second gain stage is normally a com-mon-source gain stage that has an active load, often very similar to that shown previously

Key Point: The classic two-stage opamp comprises a differential input gain stage, a commonsource second gain stage, and optionally a unity-gain output buffer stage.
in Fig. 3.4. Capacitor $\mathrm{C}_{\mathrm{C}}$ is included to ensure stability when the opamp is used with feedback. Because $\mathrm{C}_{\mathrm{C}}$ is between the input and the output of the high-gain second stage, it is often called a Miller capacitance since its effective capacitive load on the first stage is larger than its physical value. The third stage, when present, is typically a source-follower, similar to that shown in Fig. 3.6.

An example of a practical CMOS version of the two-stage opamp is shown in Fig. 6.3. In this example, it is assumed that a capacitive load is being driven, so the source-follower output buffer is omitted. This example is used to illustrate many of the important design principles when realizing the two-stage amplifier.

It should be noted that the first stage has a p -channel differential input pair with an n -channel current-mirror active load. This is a complementary differential gain stage to that shown previously in Fig. 3.19. The trade-offs between having p -channel input transistors versus this stage and the alternative
image_name:Fig. 6.2
description:The system block diagram, labeled as Fig. 6.2, represents a two-stage operational amplifier (opamp). It consists of three main components: a differential input stage, a second gain stage, and an optional output buffer.

1. **Differential Input Stage**:
- This stage is represented by an amplifier block labeled with gain \(-A_1\). It receives the input voltage \(V_{in}\) and provides the first level of amplification. The differential input stage is crucial for amplifying the difference between two input signals while rejecting any common-mode signals.

2. **Second Gain Stage**:
- The output from the differential input stage feeds into the second gain stage, represented by another amplifier block labeled with gain \(-A_2\). This stage further amplifies the signal. The output of this stage is marked as \(Out (-A_2)\).

3. **Compensation Capacitor (\(C_{cmp}\))**:
- A compensation capacitor \(C_{cmp}\) is connected between the output of the first gain stage and the output of the second gain stage. This capacitor is used to stabilize the amplifier and control its frequency response, ensuring stability and preventing oscillations.

4. **Output Buffer (Optional)**:
- The final component is an optional output buffer, represented by a unity gain amplifier (labeled as "1"). This stage is used to drive the load without affecting the previous stages, providing isolation and ensuring that the load does not affect the amplifier's performance.

5. **Flow of Information**:
- The signal flow starts at the input \(V_{in}\), moves through the differential input stage, and is amplified by \(-A_1\). The amplified signal is then passed to the second gain stage, where it is further amplified by \(-A_2\). After this, the signal can optionally pass through the output buffer before reaching the output \(V_{out}\).

6. **Overall Function**:
- The primary function of this two-stage opamp is to amplify the input signal \(V_{in}\) through two stages of amplification, potentially driving a load if the output buffer is included. The compensation capacitor ensures stability across the amplification process, making the opamp suitable for high-performance applications.

Fig. 6.2 A block diagram of a two-stage opamp.
stage of Fig. 3.19 will be discussed later in this chapter. Also, the numbers next to the transistors represent reasonable transistor sizes for a $0.18-\mu \mathrm{m}$ process. Reasonable sizes for the lengths of the transistor might be somewhere between 1.5 and 2 times the minimum transistor length of a particular technology, whereas digital logic typically makes use of the minimum transistor length.

### 6.1.1 Opamp Gain

First we discuss the overall gain of the opamp. For low-frequency applications, this gain is one of the most critical parameters of an opamp.
image_name:Fig. 6.3 A CMOS two-stage amplifier
description:The circuit is a CMOS two-stage amplifier. It consists of a differential-input first stage and a common-source second stage. The bias circuitry is provided by Q8 and a current source of 20 μA. The first stage transistors Q1 and Q2 form a differential pair with NMOS loads Q3 and Q4. The second stage is a common-source amplifier with Q6 and Q7. Resistor RC and capacitor CC form a compensation network to stabilize the amplifier.

Fig. 6.3 A CMOS two-stage amplifier. All transistor lengths are $0.3 \mu \mathrm{~m}$ and widths are shown in $\mu \mathrm{m}$ next to each transistor.

The gain of the first stage has already been derived, resulting in (3.79), and is repeated here for convenience:

$$
\begin{equation*}
A_{v 1}=-g_{m 1}\left(r_{d s 2} \| d r_{d s 4}\right) \tag{6.1}
\end{equation*}
$$

Recall from Chapter 1 that $\mathrm{g}_{\mathrm{m} 1}$ is given by

$$
\begin{equation*}
g_{m 1}=\sqrt{2 \mu_{p} C_{o x}\left(\frac{W}{L}\right)_{1} I_{D 1}}=\sqrt{2 \mu_{p} C_{o x}\left(\frac{W}{L}\right)_{1} \frac{I_{\text {bias }}}{2}} \tag{6.2}
\end{equation*}
$$

The second gain stage is simply a common-source gain stage with a $p$-channel active load, $Q_{6}$ Its gain is given by

$$
\begin{equation*}
\mathrm{A}_{\mathrm{v} 2}=-\mathrm{g}_{\mathrm{m} 7}\left(\mathrm{r}_{\mathrm{ds} 6} \| \mathrm{r}_{\mathrm{ds} 7}\right) \tag{6.3}
\end{equation*}
$$

Key Point: The dc gain of the two-stage opamp is approximated by the product of two stages, each having a gain of approximately $g_{m} r_{d s} / 2$.

The third stage, if included, is a common-drain buffer stage similar to that shown in Fig. 3.6. This stage is often called a source follower, because the source voltage follows the gate voltage, except for a level shift. When possible, it is desirable to tie the substrate of the source-follower device to its source in order to eliminate gain degradations due to the body effect. This connection also results in a smaller dc voltage drop from the gate to the source of the source-follower device, which is a major limitation on the maximum positive output voltage.

#### EXAMPLE 6.1

SPICE! Simulate this opamp with the provided netlist.

Find the gain of the opamp shown in Fig. 6.3. Assume the power supply is $\mathrm{V}_{\mathrm{DD}}=1.8 \mathrm{~V}$ and a purely capacitive load. Assume the process parameters for the $0.18-\mu \mathrm{m}$ process in Table 1.5.

#### Solution

First the bias currents are calculated. Since $\mathrm{I}_{\mathrm{D} 8}=20 \mu \mathrm{~A}$, we have

$$
\mathrm{I}_{\mathrm{D} 1}=\mathrm{I}_{\mathrm{D} 2}=\mathrm{I}_{\mathrm{D} 3}=\mathrm{I}_{\mathrm{D} 4}=\mathrm{I}_{\mathrm{D} 5} / 2=\left(\mathrm{W}_{5} / 2 \mathrm{~W}_{8}\right) \mathrm{I}_{\mathrm{D} 8}=100 \mu \mathrm{~A}
$$

and

$$
\mathrm{I}_{\mathrm{D} 6}=\mathrm{I}_{\mathrm{D} 7}=\left(\mathrm{W}_{6} / \mathrm{W}_{5}\right) \mathrm{I}_{\mathrm{D} 5}=300 \mu \mathrm{~A}
$$

We can now calculate the transconductances of $\mathrm{Q}_{1}, \mathrm{Q}_{2}, \mathrm{Q}_{7}$, and $\mathrm{Q}_{8}$. Using (6.2), we have $\mathrm{g}_{\mathrm{m} 1}=\mathrm{g}_{\mathrm{m} 2}=1.30 \mathrm{~mA} / \mathrm{V}$, and $g_{m 7}=3.12 \mathrm{~mA} / \mathrm{V}$.

Next, we estimate the output impedances of the transistors using (1.86). It should be mentioned here that (1.86) is only of very moderate accuracy, perhaps 50 percent at best. These values for the transistor output impedances can be corrected later once a SPICE analysis is run. With the use of (1.86), we find that all of the transistors in the first stage have output impedances of approximately

$$
r_{d s 1}=r_{d s 2}=r_{d s 3}=r_{d s 4}=37.5 \mathrm{k} \Omega
$$

The output impedances of transistors in the second stage are

$$
r_{\mathrm{ds} 6}=r_{\mathrm{ds} 7}=12.5 \mathrm{k} \Omega
$$

Finally, using (6.1), we calculate that

$$
A_{v 1}=-g_{m 1}\left(r_{d s 2} \| r_{d s 4}\right)=-24.4 \mathrm{~V} / \mathrm{V}
$$

Using (6.3),

$$
A_{v 2}=-g_{m 7}\left(r_{d s 6} \| r_{d s 7}\right)=-19.5 \mathrm{~V} / \mathrm{V}
$$

Thus, the total gain is equal to $A_{v 1} A_{v 2}=-1043 \mathrm{~V} / \mathrm{V}$ or 60.4 dB . Once again, it should be mentioned here that this result is a rough approximation and should be verified using SPICE. The benefit of performing the hand calculations is to see how the gain is affected by different design parameters.

### 6.1.2 Frequency Response

#### First-Order Model

We now wish to investigate the frequency response of the two-stage opamp at frequencies where the compensation capacitor, $\mathrm{C}_{\mathrm{C}}$, has caused the magnitude of the gain to begin to decrease, but still at frequencies well below the unity-gain frequency of the opamp. This corresponds to midband frequencies for many applications. This allows us to make a couple of simplifying assumptions. First, we will ignore all capacitors except the compensation capacitor, $\mathrm{C}_{\mathrm{C}}$, which normally dominates at all frequencies except around the unity-gain frequency of the opamp. ${ }^{2}$ Second, we also assume that resistor $\mathrm{R}_{\mathrm{C}}$ is not present. This resistor is included to achieve lead compensation and it has an effect only around the unity-gain frequency of the opamp, as we will see when we discuss compensation in Section 6.2. The simplified circuit used for analysis is shown in Fig. 6.4. It is worth mentioning that this simplified circuit is often used during system-level simulations when speed is more important than accuracy, although aspects such as slew-rate limiting (see next subsection) should also be included in the simulation.

The second stage introduces primarily a capacitive load on the first stage due to the compensation capacitor, $\mathrm{C}_{\mathrm{C}}$. Using Miller's theorem (Section 4.2.3), one can show that the equivalent load capacitance, $\mathrm{C}_{\text {eq }}$, at node $\mathrm{v}_{1}$ is given by

$$
\begin{equation*}
C_{e q}=C_{C}\left(1+A_{v 2}\right) \approx C_{C} A_{v 2} \tag{6.4}
\end{equation*}
$$

The gain in the first stage can now be found using the small-signal model of Figure 4.37, resulting in

$$
\begin{equation*}
A_{v 1}=\frac{v_{1}}{v_{i n}}=-g_{m 1} Z_{o u t 1} \tag{6.5}
\end{equation*}
$$

image_name:Fig. 6.4
description:
[
name: Q1, type: PMOS, ports: {S: X1, D: X2, G: Vin-}
name: Q2, type: PMOS, ports: {S: X1, D: d2d4, G: Vin+}
name: Q3, type: NMOS, ports: {S: GND, D: X2, G: X2}
name: Q4, type: NMOS, ports: {S: GND, D: d2d4, G: X2}
name: Q5, type: PMOS, ports: {S: VDD, D: X1, G: Vbias}
name: Cc, type: Capacitor, value: Cc, ports: {Np: V1, Nn: V2}
name: -A_v2, type: OpAmp, value: -A_v2, ports: {InP: V1, InN: GND, Out: V2(Vout)}
]
extrainfo:The circuit is a simplified model of an op-amp with a differential input stage and a compensation capacitor Cc. The transistors Q1 and Q2 form a differential pair, while Q3 and Q4 act as current sinks. Q5 provides a bias current. The op-amp A_v2 is used for gain in the second stage. The circuit aims to achieve a specific midband frequency response.

Fig. 6.4 A simplified model for the opamp used to find the midband frequency response.
2. Recall that the unity-gain frequency of an opamp is that frequency where the magnitude of the open-loop opamp gain has decreased to 1.
where

$$
\begin{equation*}
Z_{\mathrm{out} 1}=r_{\mathrm{ds} 2}\left\|r_{\mathrm{ds} 4}\right\| \frac{1}{s C_{\mathrm{eq}}} \tag{6.6}
\end{equation*}
$$

For midband frequencies, the impedance of $C_{e q}$ dominates, and we can write

$$
\begin{equation*}
\mathrm{Z}_{\mathrm{out} 1} \cong \frac{1}{\mathrm{~s} \mathrm{C}_{\mathrm{eq}}} \cong \frac{1}{\mathrm{~s} \mathrm{C}_{\mathrm{C}} \mathrm{~A}_{\mathrm{v} 2}} \tag{6.7}
\end{equation*}
$$

For the overall gain, we have

$$
\begin{equation*}
A_{v}(s) \equiv \frac{v_{\text {out }}}{v_{\text {in }}}=A_{v 2} A_{v 1} \cong A_{v 2} \frac{g_{\mathrm{m} 1}}{s C_{C} A_{v 2}}=\frac{g_{\mathrm{m} 1}}{s C_{c}} \tag{6.8}
\end{equation*}
$$

using (6.5) and (6.7). This simple equation can be used to find the approximate ${ }^{3}$ unity-gain frequency. Specifically, to find the unity-gain frequency, $\omega_{\mathrm{ta}}$, we set $\left|\mathrm{A}_{\mathrm{v}}\left(\mathrm{j} \omega_{\mathrm{ta}}\right)\right|=1$, and solve for $\omega_{\mathrm{ta}}$. Performing such a procedure with (6.8), we obtain the following relationship:

$$
\begin{equation*}
\omega_{\mathrm{ta}}=\frac{\mathrm{g}_{\mathrm{m} 1}}{\mathrm{C}_{\mathrm{c}}} \tag{6.9}
\end{equation*}
$$

Note here that the unity-gain frequency is directly proportional to $\mathrm{g}_{\mathrm{m} 1}$ and inversely proportional to $\mathrm{C}_{\mathrm{C}}$. Substituting (1.78) into (6.9) provides another expression for the unity-gain frequency.

$$
\begin{equation*}
\omega_{\mathrm{ta}}=\frac{2 \mathrm{I}_{\mathrm{D} 1}}{\mathrm{~V}_{\mathrm{eff} 1} \mathrm{C}_{\mathrm{C}}}=\frac{\mathrm{I}_{\mathrm{D} 5}}{\mathrm{~V}_{\mathrm{eff} 1} \mathrm{C}_{\mathrm{C}}} \tag{6.10}
\end{equation*}
$$

Key Point: The two-stage opamp's frequency response is dominated by a pole at the input to the second stage arising from the introduced Miller capacitor, $\mathrm{C}_{\mathrm{C}}$. A dominant-pole approximation yields a unity-gain frequency of $\mathrm{g}_{\mathrm{m} 1} / \mathrm{C}_{\mathrm{C}}$.

Equation (6.10) indicates that, for a fixed unity-gain frequency, the bias current and hence power consumption is minimized with small values of $\mathrm{V}_{\text {eff } 1}$. Ordinarily, a downside of selecting a small value for $\mathrm{V}_{\text {eff } 1}$ would be increased distortion, but this is mitigated in the case of opamps used with feedback since only very small differential signals appear at the differential pair inputs. Equation (6.10) presumes a square-law for $Q_{1}, Q_{2}$; the current is minimized when these devices are operated in subthreshold where, from (1.122), we have $\mathrm{g}_{\mathrm{m} 1 \text { (sub-th) }}=\mathrm{ql}_{\mathrm{D}_{1}} / \mathrm{nkT}$ which, when substituted into (6.9) yields $\omega_{\mathrm{ta}}=\mathrm{ql}_{\mathrm{D} 1} / \mathrm{nkTC}_{\mathrm{C}}$.

#### EXAMPLE 6.2

Using the same parameters as in Example 6.1 , and assuming $\mathrm{C}_{\mathrm{C}}=1 \mathrm{pF}$, what is the unity-gain frequency in Hz ?

#### Solution

Using $\mathrm{g}_{\mathrm{m} 1}=1.30 \mathrm{~mA} / \mathrm{V}$ and (6.9), we find that

$$
\omega_{\mathrm{ta}}=\frac{1.3 \times 10^{-3} \mathrm{~A} / \mathrm{V}}{1 \times 10^{-12} \mathrm{~F}}=1.3 \cdot 10^{9} \mathrm{rad} / \mathrm{sec}
$$

Thus, we find that $\mathrm{f}_{\mathrm{ta}}=\omega_{\mathrm{ta}} /(2 \pi)=207 \mathrm{MHz}$.

#### Second-Order Model

A simplified small-signal model for the two-stage opamp is shown in Fig. 6.5, where the output buffer has again been ignored. Also, it is assumed that any parasitic poles in the first stage are at frequencies much higher than the opamp unity-gain frequency $\omega_{\mathrm{ta}}$ and that the first stage can therefore be modelled by a simple voltagecontrolled current source. In the small-signal model, we have

$$
\begin{gather*}
\mathrm{R}_{1}=\mathrm{r}_{\mathrm{ds} 4} \| \mathrm{r}_{\mathrm{ds} 2}  \tag{6.11}\\
\mathrm{C}_{1}=\mathrm{C}_{\mathrm{db} 2}+\mathrm{C}_{\mathrm{db} 4}+\mathrm{C}_{\mathrm{gs} 7}  \tag{6.12}\\
\mathrm{R}_{2}=\mathrm{r}_{\mathrm{ds} 6} \| \mathrm{r}_{\mathrm{ds} 7}  \tag{6.13}\\
\mathrm{C}_{2}=\mathrm{C}_{\mathrm{db} 7}+\mathrm{C}_{\mathrm{db} 6}+\mathrm{C}_{\mathrm{L} 2} \tag{6.14}
\end{gather*}
$$

Note that if no output buffer is present, then $\mathrm{C}_{\mathrm{L} 2}$ is the output load capacitance. If an output buffer is present, then $\mathrm{C}_{\mathrm{L} 2}$ is the load capacitance introduced by the output buffer.

To show the need for $R_{C}$, we first assume $R_{C}=0$ and perform nodal analysis at the nodes designated by $v_{1}$ and $\mathrm{v}_{\text {out }}$. The following transfer function is obtained:

$$
\begin{equation*}
A_{v}(s)=\frac{v_{\text {out }}}{v_{\text {in }}}=\frac{g_{m 1} g_{m 7} R_{1} R_{2}\left(1-\frac{s C_{c}}{g_{m 7}}\right)}{1+s a+s^{2} b} \tag{6.15}
\end{equation*}
$$

where

$$
\begin{equation*}
\mathrm{a}=\left(\mathrm{C}_{2}+\mathrm{C}_{\mathrm{C}}\right) \mathrm{R}_{2}+\left(\mathrm{C}_{1}+\mathrm{C}_{\mathrm{C}}\right) \mathrm{R}_{1}+\mathrm{g}_{\mathrm{m} 7} \mathrm{R}_{1} \mathrm{R}_{2} \mathrm{C}_{\mathrm{C}} \tag{6.16}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{b}=\mathrm{R}_{1} \mathrm{R}_{2}\left(\mathrm{C}_{1} \mathrm{C}_{2}+\mathrm{C}_{1} \mathrm{C}_{\mathrm{C}}+\mathrm{C}_{2} \mathrm{C}_{\mathrm{C}}\right) \tag{6.17}
\end{equation*}
$$

It is possible to find approximate equations for the two poles based on the assumption that the poles are real and widely separated. ${ }^{4}$ This assumption allows us to express the denominator, $\mathrm{D}(\mathrm{s})$, as ${ }^{5}$

$$
\begin{equation*}
D(s)=\left(1+\frac{s}{\omega_{\mathrm{p} 1}}\right)\left(1+\frac{s}{\omega_{\mathrm{p} 2}}\right) \cong 1+\frac{s}{\omega_{\mathrm{p} 1}}+\frac{\mathrm{s}^{2}}{\omega_{\mathrm{p} 1} \omega_{\mathrm{p} 2}} \tag{6.18}
\end{equation*}
$$

image_name:Fig. 6.5
description:
[
name: gm1Vin, type: VoltageControlledCurrentSource, ports: {Np: V1, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: V1, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: V1, Nn: GND}
name: Rc, type: Resistor, value: Rc, ports: {N1: V1, N2: rc_cc}
name: Cc, type: Capacitor, value: Cc, ports: {Np: Vout, Nn: rc_cc}
name: g_m7*V1, type: VoltageControlledCurrentSource, ports: {Np: Vout, Nn: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vout, N2: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a two-stage operational amplifier model for compensation analysis. It includes resistors, capacitors, and voltage-controlled current sources. The main nodes include the input node V1, output node Vout, and ground.

Fig. 6.5 A small-signal model of the two-stage opamp used for compensation analysis.

[^4]Equating the coefficients of (6.15) equal to the coefficients of (6.18) and solving for $\omega_{\mathrm{p} 1}$ and $\omega_{\mathrm{p} 2}$ results in the following relationships. The dominant pole, $\omega_{\mathrm{p} 1}$, is given by

$$
\begin{align*}
\omega_{\mathrm{p} 1} & \cong \frac{1}{R_{1}\left[C_{1}+C_{c}\left(1+g_{m 7} R_{2}\right)\right]+R_{2}\left(C_{2}+C_{C}\right)} \\
& \cong \frac{1}{R_{1} C_{c}\left(1+g_{m 7} R_{2}\right)}  \tag{6.19}\\
& \cong \frac{1}{g_{m 7} R_{1} R_{2} C_{c}}
\end{align*}
$$

whereas the nondominant pole, $\omega_{\mathrm{p} 2}$, is given by

$$
\begin{align*}
\omega_{\mathrm{p} 2} & \cong \frac{g_{\mathrm{m} 7} C_{\mathrm{C}}}{\mathrm{C}_{1} C_{2}+C_{2} C_{C}+C_{1} C_{C}}  \tag{6.20}\\
& \cong \frac{g_{\mathrm{m} 7}}{\mathrm{C}_{1}+C_{2}}
\end{align*}
$$

Note that, from (6.15), another zero, $\omega_{z}$, is located in the right half plane and is given by

$$
\begin{equation*}
\omega_{\mathrm{z}}=\frac{-\mathrm{g}_{\mathrm{m} 7}}{\mathrm{C}_{\mathrm{c}}} \tag{6.21}
\end{equation*}
$$

This zero should come as no surprise since there are two signal paths having opposite signs in the small-signal circuit of Fig. 6.5 -one through the voltage-controlled current source, $g_{m} v_{1}$, and the other through the compensation capacitor, $\mathrm{C}_{\mathrm{C}}$.

Key Point: The two-stage opamp's second pole arises at the output node and may be increased by increasing the secondstage transconductance, $\mathrm{g}_{\mathrm{m} 7}$.

From the preceding relationships for $\omega_{\mathrm{p} 1}$ and $\omega_{\mathrm{p} 2}$, we can see that, as $\mathrm{g}_{\mathrm{m} 7}$ increases, the separation between the first and second poles increases. This separation tends to make the circuit more stable; hence, the use of a Miller capacitance for compensation is often called pole-splitting compensation. Also note that increasing $\mathrm{C}_{\mathrm{C}}$ moves the dominant pole, $\omega_{\mathrm{p} 1}$, to a lower frequency without affecting the second pole, $\omega_{\mathrm{p} 2}$. This effect also makes the opamp more stable.

However, a problem arises due to the right-half-plane zero, $\omega_{\mathrm{z}}$. Because the zero is in the right half plane, it introduces negative phase shift, or phase lag, in the transfer function of the opamp. This makes stability more difficult. Making $\mathrm{C}_{\mathrm{C}}$ larger does not help matters because this decreases the frequencies of both the first pole and the zero without making them more widely separated. Indeed, because of this right-half-plane zero, it is often impossible to choose $\mathrm{C}_{\mathrm{C}}$ such that the step response has no overshoot (assuming $R_{C}=0$ ). Fortunately, all is not lost, since introducing $R_{C}$ allows adequate compensation, as we discuss in the next subsection.

#### EXAMPLE 6.3

Using the same parameters as in Example 6.1, and assuming $\mathrm{C}_{\mathrm{C}}=1 \mathrm{pF}$ and a load capacitance $\mathrm{C}_{\mathrm{L} 2}=5 \mathrm{pF}$, estimate the second pole and zero frequencies. Suggest a design change that would increase both frequencies.

#### Solution

Assuming $\mathrm{C}_{\mathrm{db} 6}$ and $\mathrm{C}_{\mathrm{db} 7}$ are both much smaller than $\mathrm{C}_{\mathrm{L} 2}$, we take $\mathrm{C}_{2} \cong \mathrm{C}_{\mathrm{L} 2}=5 \mathrm{pF}$. Substituting this and $\mathrm{g}_{\mathrm{m} 7}=3.12 \mathrm{~mA} / \mathrm{V}$ into (6.20),

$$
\omega_{\mathrm{p} 2} \cong \frac{3.12 \mathrm{~mA} / \mathrm{V}}{5 \mathrm{pF}+1 \mathrm{pF}}=520 \cdot 10^{6} \mathrm{rad} / \mathrm{sec}=2 \pi \cdot 82.8 \mathrm{MHz}
$$

The zero is located at

$$
\left|\omega_{z}\right| \cong \frac{3.12 \mathrm{~mA} / \mathrm{V}}{5 \mathrm{pF}}=624 \cdot 10^{6} \mathrm{rad} / \mathrm{sec}=2 \pi \cdot 99.3 \mathrm{MHz}
$$

Both $\omega_{\mathrm{p} 2}$ and $\left|\omega_{\mathrm{z}}\right|$ could be increased by widening both $Q_{6}$ and $Q_{7}$, which would in turn increase $g_{m 7}$. However, doing so would also increase the current consumption of second stage.

Normally one has little control over $\omega_{\mathrm{ta}}$, assuming a given maximum power dissipation is allowed. It is usually constrained by stability requirements to be less than approximately one-half of the second-pole frequency, $\omega_{\mathrm{p} 2}$, as we have seen in Section 5.3.2. ${ }^{6}$ The second pole frequency approximated in (6.20) is, in turn, dependent upon the load capacitance via $C_{2}$, and the power dissipation of the second stage via $g_{m 7}$.

### 6.1.3 Slew Rate

The maximum rate at which the output of an opamp can change is limited by the finite bias currents within it. When the input to an opamp circuit changes too quickly, the opamp is unable to maintain a virtual ground between its inputs so the opamp temporarily sees a large differential input. The opamp's output voltage then changes at its maximum rate, called the slew rate, SR. Under slew-rate limiting, the opamp's response is nonlinear. The effect is illustrated in Fig. 6.6 where a large step input

Key Point: The slew rate is the maximum rate at which the output of an opamp changes when a large differential input signal is present.
causes the output to increase at its slew rate until such time as it is able to resume linear operation without exceeding the opamp slew rate. Such transient behavior is common in switched capacitor circuits, where the slew rate is a major factor determining the circuit's settling time.

#### EXAMPLE 6.4

Consider a closed-loop feedback amplifier with a first-order linear settling time constant of $\tau=0.2 \mu \mathrm{~s}$ and a slew rate of $1 \mathrm{~V} / \mu \mathrm{s}$. What is the time required for the output to settle when generating to a $10-\mathrm{mV}$ step output with 0.1 mV accuracy? What about a 1-V step output?
image_name:Fig. 6.6
description:The graph in Fig. 6.6 illustrates the step response of an operational amplifier, focusing on the effects of slew-rate limiting. The graph is a time-domain waveform, showing how the output voltage of a system responds to a step input over time.

**Axes Labels and Units:**
- The x-axis represents time, though no specific units are labeled, it is typically in microseconds (µs) for such applications.
- The y-axis represents the step response, which is a measure of the output voltage, typically in volts (V).

**Overall Behavior and Trends:**
- The dashed line represents the ideal step response expected from a linear system, which shows a smooth, exponential increase towards a final value.
- The solid line shows the actual response of the system to a large step input. Initially, the response is limited by the slew rate, resulting in a linear increase. Once the slew-rate limit is no longer the dominant factor, the response transitions to exponential settling.
- For a small step input, the response follows a purely exponential (linear) settling, as indicated by the lower solid curve.

**Key Features and Technical Details:**
- The initial linear segment of the actual response curve is characterized by the slew rate, which is the maximum rate of change of the output voltage.
- The transition point where the response shifts from slew-rate limited to exponential settling is marked on the graph.
- The graph highlights the difference between the ideal and actual response, emphasizing how the slew rate affects large step inputs but not small ones.

**Annotations and Specific Data Points:**
- Annotations on the graph describe the behavior of both the ideal and actual responses, with markers indicating the transition from slew-rate limitation to exponential settling.
- The graph effectively demonstrates the impact of slew-rate limitations on the settling behavior of opamps, providing insight into how these limitations can affect circuit performance.

Fig. 6.6 An illustration of the effect of slew-rate limiting in opamps.

#### Solution

The amplifier will slew-rate limit whenever the slope demanded by linear settling exceeds the maximum imposed by slew-rate limiting. For a step height $\mathrm{V}_{\text {step }}$, linear settling is exponential.

$$
\begin{equation*}
v_{0}=V_{\text {step }}\left(1-e^{-t / \tau}\right) \tag{6.22}
\end{equation*}
$$

The highest rate of change is observed right at the time of the step.

$$
\begin{equation*}
\left.\frac{d v_{o}}{d t}\right|_{\max }=\left.\frac{d v_{o}}{d t}\right|_{t=0}=\frac{V_{\text {step }}}{\tau} \tag{6.23}
\end{equation*}
$$

So long as this maximum slope is less than the slew rate, slew-rate limiting is avoided. Hence, the maximum step size that can be tolerated without slew-rate limiting is

$$
\begin{equation*}
\mathrm{V}_{\text {step }, \max }<\mathrm{SR} \cdot \tau \tag{6.24}
\end{equation*}
$$

In this case, linear settling is observed as long as the output step amplitude is less than 0.2 V . For a $10-\mathrm{mV}$ step, the slope predicted by (6.23) is only $0.05 \mathrm{~V} / \mathrm{s}$, far below the specified maximum slew rate. Hence, $99 \%$ settling is observed after $-\ln (0.1 / 10) \tau=4.6 \tau=0.92 \mu \mathrm{~s}$.

With a 1-V step, the amplifier output will initially increase at the slew rate until it is close enough to its final value that linear settling may begin. This happens when the output is within $\mathrm{V}_{\text {step, } \max }$ of its final value. Hence, the amplifier will be slew-rate limited for $(1 \mathrm{~V}-0.2 \mathrm{~V}) / 1 \mathrm{~V} / \mu \mathrm{s}=0.8 \mu \mathrm{~s}$. From this time on, linear settling is observed and $-\ln (0.1 / 200)=7.6$ additional time constants are required for settling with 0.1 mV accuracy, as shown in Fig. 6.7. Hence, the total settling time is $0.8 \mu \mathrm{~s}+7.6 \tau=2.32 \mu \mathrm{~s}$. If the amplifier slew rate were made large enough that slew-rate limiting could be avoided, the settling time would be only $-\ln (0.1 / 1000) \tau=1.84 \mu \mathrm{~s}$.

When the opamp of Fig. 6.3 is limited by its slew rate because a large input signal is present, all of the bias current of $Q_{5}$ goes into either $Q_{1}$ or $Q_{2}$, depending on whether $v_{i n}$ is negative or positive. When $v_{i n}$ is a large positive voltage, the bias current, $\mathrm{I}_{\mathrm{D}}$, goes entirely through $\mathrm{Q}_{1}$ and also goes into the current-mirror pair, $\mathrm{Q}_{3}, \mathrm{Q}_{4}$. Thus, the current coming out of the compensation capacitor, $C_{C}$, (i.e., $I_{D 4}$ ) is simply equal to $I_{D 5}$ since $Q_{2}$ is off. When $v_{i n}$ is a large negative voltage, the current-mirror pair $Q_{3}$ and $Q_{4}$ is shut off because $Q_{1}$ is off, and now the bias current, $\mathrm{I}_{\mathrm{D} 5}$, goes directly into $\mathrm{C}_{\mathrm{C}}$. In either case, the maximum current entering or leaving $\mathrm{C}_{\mathrm{C}}$ is simply the total bias current, $\mathrm{I}_{\mathrm{D} .}{ }^{7}$
image_name:Fig. 6.7
description:The graph depicted is a time-domain waveform illustrating the effect of slew rate limiting on the settling behavior of a system, specifically with a 1-V step output. The horizontal axis represents time, labeled as 't', with units in microseconds (μs), while the vertical axis represents the output voltage, labeled as 'V₀', with units in volts (V).

Axes Labels and Units:
- **Horizontal Axis (Time):** Labeled 't', measured in microseconds (μs).
- **Vertical Axis (Voltage):** Labeled 'V₀', measured in volts (V).

Overall Behavior and Trends:
The graph shows two curves: a solid curve and a dashed curve. The solid curve represents the actual output voltage behavior, while the dashed curve indicates the ideal or expected output without slew rate limiting.
- **Solid Curve:** Initially rises linearly, indicating a constant rate of change, which corresponds to the slew rate (SR). After reaching approximately 0.8 V at 0.8 μs, the curve begins to level off, approaching an asymptotic value of 1 V.
- **Dashed Curve:** Follows a similar initial linear rise but deviates from the solid curve as it approaches the 1 V level more quickly, indicating faster settling without the slew rate limitation.

Any Features and Technical Details:
- **Slew Rate (SR):** Represented by the initial linear portion of the solid curve, showing the maximum rate of change of the output voltage.
- **Settling Behavior:** The solid curve approaches 1 V asymptotically, indicating the final settled output voltage level.
- **Time to Settle to 0.8 V:** Occurs at approximately 0.8 μs.

Annotations and Specific Data Points:
- **Voltage Levels:** Marked at 0.8 V and 1 V on the vertical axis.
- **Time Marker:** A vertical dashed line at 0.8 μs indicates the time at which the output voltage reaches 0.8 V.

This graph effectively demonstrates the impact of slew rate limiting on the time it takes for the output voltage to settle to its final value, highlighting the slower response compared to an ideal system without such limitations.

Fig. 6.7 The effect of slew rate limiting upon the settling of Example 6.4 with a 1-V step output.

Defining the slew rate to be the maximum rate that $\mathrm{v}_{2}$ can change, and recalling that $\mathrm{v}_{\text {out }} \cong \mathrm{v}_{2}$, we have

$$
\begin{equation*}
\left.\mathrm{SR} \equiv \frac{\mathrm{~d} \mathrm{v}_{\text {out }}}{\mathrm{dt}}\right|_{\max }=\frac{\left.\mathrm{I}_{\mathrm{C}_{\mathrm{c}}}\right|_{\max }}{\mathrm{C}_{\mathrm{C}}}=\frac{\mathrm{I}_{\mathrm{DS}}}{\mathrm{C}_{\mathrm{C}}} \tag{6.25}
\end{equation*}
$$

where we used the charge equation $q=C V$, which leads to $I=d q / d t=C(d V / d t)$. Since $I_{D S}=2 I_{D 1}$, we can also write

$$
\begin{equation*}
S R=\frac{2 I_{D 1}}{C_{C}}=\frac{I_{D S}}{C_{C}} \tag{6.26}
\end{equation*}
$$

where $I_{D 1}$ is the original bias current of $Q_{1}$ with no signals present. Also, using (6.9), we have $C_{C}=g_{m 1} / \omega_{t a}$, and substituting this into (6.26), we have

$$
\begin{equation*}
\mathrm{SR}=\frac{2 \mathrm{I}_{\mathrm{D} 1} \omega_{\mathrm{ta}}}{\mathrm{~g}_{\mathrm{m} 1}} \tag{6.27}
\end{equation*}
$$

Recalling that

$$
\begin{equation*}
g_{\mathrm{m} 1}=\sqrt{2 \mu_{\mathrm{p}} \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)_{1} \mathrm{I}_{\mathrm{D} 1}} \tag{6.28}
\end{equation*}
$$

and

$$
\begin{equation*}
V_{\text {eff } 1}=\sqrt{\frac{2 I_{D 1}}{\mu_{\mathrm{p}} C_{o x}(W / L)_{1}}} \tag{6.29}
\end{equation*}
$$

from Chapter 1, we finally have another relationship for the slew-rate value.

$$
\begin{equation*}
\mathrm{SR}=\frac{2 \mathrm{I}_{\mathrm{D} 1}}{\sqrt{2 \mu_{\mathrm{p}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L})_{1} \mathrm{I}_{\mathrm{D} 1}}} \omega_{\mathrm{ta}}=\mathrm{V}_{\mathrm{eff} 1} \omega_{\mathrm{ta}} \tag{6.30}
\end{equation*}
$$

Since stability demands that $\omega_{\mathrm{ta}}$ be lower than $\omega_{\mathrm{p} 2}$, the only ways of improving the slew rate for a properly-compensated two-stage CMOS opamp is to increase $\mathrm{V}_{\mathrm{eff} 1}$ or $\omega_{\mathrm{p} 2}$.

Key Point: The only ways of improving the slew rate of a twostage opamp is to increase $\mathrm{V}_{\mathrm{eff} 1}$ or $\omega_{\mathrm{p} 2}$.

#### EXAMPLE 6.5

Using the same parameters as in Example 6.1, and assuming $\mathrm{C}_{\mathrm{C}}=1 \mathrm{pF}$, what is the slew rate? What circuit changes could be made to double the slew rate but keep $\omega_{\mathrm{ta}}$ and bias currents unchanged?

#### Solution

From (6.26), we have

$$
\begin{equation*}
\mathrm{SR}=\frac{200 \mu \mathrm{~A}}{1 \mathrm{pF}}=200 \mathrm{~V} / \mu \mathrm{s} \tag{6.31}
\end{equation*}
$$

To double the slew rate while maintaining the same bias currents, $\mathrm{C}_{\mathrm{C}}$ should be set to 0.5 pF . To maintain the same unity-gain frequency, $g_{m 1}$ should be halved, which can be accomplished by decreasing the widths of $Q_{1}$ and $Q_{2}$ by 4 (i.e., one could let $W_{1}=W_{2}=9 \mu \mathrm{~m}$ ).

Assuming a fixed power consumption, and hence fixed bias currents, increasing $\mathrm{V}_{\text {eff } 1}$ improves the slew rate (6.30) and helps to minimize distortion, but also lowers the transconductance of the input stage which decreases the dc gain (6.1), and increases the equivalent input thermal noise (see Chapter 9).

### 6.1.4 $\boldsymbol{n}$-Channel or $p$-Channel Input Stage

The two-stage opamp shown in Fig. 6.3 and discussed thusfar has p-channel input transistors. It is also possible to realize a complementary opamp where the first stage has an n -channel differential pair and the second stage is a common-source amplifier having a p-channel input drive transistor. The choice of which configuration to use depends on a number of trade-offs that are discussed here.

First, the overall dc gain is largely unaffected by the choice since both designs have one stage with one or more n -channel driving transistors, and one stage with one or more p -channel driving transistors.

Having a p -channel input first stage implies that the second stage has an n -channel input drive transistor. This arrangement maximizes the transconductance of the drive transistor of the second stage, which is critical when high-frequency operation is important. As shown in Section 6.1.2, the equivalent second pole, and therefore the unity-gain frequency as well, are both proportional to the transconductance of the second stage.

Another consideration is whether a p -channel or n -channel source-follower output stage is desired. Typically, an n -channel source follower is preferable because this will have less of a voltage drop. Also, since an $n$-channel transistor has a higher transconductance, the effect on the equivalent second pole due to its load capacitance is minimized, which is another important consideration. Finally, there is less degradation of the gain when small load resistances are being driven. The one disadvantage of having an n -channel source follower is that, for n -well processes, it is not possible to connect the source to the substrate, thereby minimizing the voltage drop. Finally, note that, for opamps that drive purely capacitive loads, the buffer stage should not be included, and for this case, the output stage is clearly not a consideration.

Key Point: When using a two-stage opamp, p-channel input transistors are almost always the best choice for the first stage because they offer larger unity-gain frequency and lower 1/f noise, with the major disadvantage being an increase in wideband thermal noise.

Noise is another important consideration when choosing which input stage to use. Perhaps the major noise source of MOS opamps is due to $1 / \mathrm{f}$ noise caused by carriers randomly entering and leaving traps introduced by defects near the semiconductor surface. This $1 / \mathrm{f}$ noise source can be especially troublesome unless special circuit design techniques are used. ${ }^{8}$ Typically, p-channel transistors have less $1 / \mathrm{f}$ noise than n -channel transistors since their majority carriers (holes) have less potential to be trapped in surface states. Thus, having a firststage with p -channel inputs minimizes the output noise due to the $1 / \mathrm{f}$ noise. The same is not true when thermal noise is considered. When thermal noise is referred to the input of the opamp, it is minimized by using input transistors that have large transconductances, which unfortunately degrades the slew rate. However, when thermal noise is a major consideration, then a single-stage architecture, such as a folded-cascode opamp, is normally used.

In summary, when using a two-stage opamp, a p-channel input transistor for the first stage is almost always the best choice because it optimizes unity-gain frequency and minimizes $1 / \mathrm{f}$ noise, with the major disadvantage being an increase in wideband thermal noise.

### 6.1.5 Systematic Offset Voltage

When designing the two-stage CMOS opamp, if one is not careful, it is possible that the design will have an inherent (or systematic) input-offset voltage. Indeed, this was the case for many of the original designs used in

[^5]production integrated circuits. To see what is necessary to guarantee that no inherent input-offset voltage exists, consider the opamp shown in Fig. 6.3. When the differential input voltage is zero (i.e, when $\mathrm{V}_{\text {in }}^{+}=\mathrm{V}_{\text {in }}^{-}$), the output voltage of the first stage, $\mathrm{V}_{\mathrm{G} 57}$, should be that which is required to make $\mathrm{I}_{\mathrm{D} 7}$ equal to its bias current, $\mathrm{I}_{\mathrm{D} 6}$. Specifically, the value of $\mathrm{V}_{\mathrm{GS} 7}$ should be given by
\$\$

$$
\begin{equation*}
\mathrm{V}_{\mathrm{GS} 7}=\sqrt{\frac{2 \mathrm{I}_{\mathrm{D} 6}}{\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L})_{7}}}+\mathrm{V}_{\mathrm{tn}} \tag{6.32}
\end{equation*}
$$

\$\$

When the differential input voltage is zero, the drain voltages of both $Q_{3}$ and $Q_{4}$ are equal by arguments of symmetry. Therefore, the output voltage of the first stage, $\mathrm{V}_{\mathrm{GS}}$, is given by

$$
\begin{equation*}
\mathrm{V}_{\mathrm{GS} 7}=\mathrm{V}_{\mathrm{DS} 3}=\mathrm{V}_{\mathrm{GS} 4} \tag{6.33}
\end{equation*}
$$

This value is the voltage necessary to cause $\mathrm{I}_{\mathrm{D} 7}$ to be equal to $\mathrm{I}_{\mathrm{D} 6}$, or, in other words, to satisfy (6.32). If this value is not achieved, then the output of the second stage (with $Q_{6}, Q_{7}$ ) would clip at either the negative or positive rail since this stage has such a high gain. ${ }^{9}$ However, the gate-source voltage of $Q_{4}$ is given by

$$
\begin{equation*}
\mathrm{V}_{\mathrm{GS} 4}=\sqrt{\frac{2 \mathrm{I}_{\mathrm{D} 4}}{\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L})_{4}}}+\mathrm{V}_{\mathrm{tn}} \tag{6.34}
\end{equation*}
$$

so equating (6.32) and (6.34) to satisfy (6.33) results in

$$
\begin{equation*}
\sqrt{\frac{2 \mathrm{I}_{\mathrm{D} 4}}{\mu_{\mathrm{n}} \mathrm{C}_{\text {ox }}(\mathrm{W} / \mathrm{L})_{4}}}=\sqrt{\frac{2 \mathrm{I}_{\mathrm{D} 6}}{\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L})_{7}}} \tag{6.35}
\end{equation*}
$$

or, equivalently,

$$
\begin{equation*}
\frac{\mathrm{I}_{\mathrm{D} 4}}{(\mathrm{~W} / \mathrm{L})_{4}}=\frac{\mathrm{I}_{\mathrm{D} 6}}{(\mathrm{~W} / \mathrm{L})_{7}} \tag{6.36}
\end{equation*}
$$

This equality, when the current density of $Q_{4}$ is equal to the current density of $Q_{7}$, guarantees that they both have the same effective gate-source voltages.

Since

$$
\begin{equation*}
\frac{\mathrm{I}_{\mathrm{D} 6}}{\mathrm{I}_{\mathrm{D} 4}}=\frac{\mathrm{I}_{\mathrm{D} 6}}{\mathrm{I}_{\mathrm{D} 5} / 2}=\frac{(\mathrm{W} / \mathrm{L})_{6}}{(\mathrm{~W} / \mathrm{L})_{5} / 2} \tag{6.37}
\end{equation*}
$$

we see that the necessary condition to ensure that no input-offset voltage is present is

$$
\begin{equation*}
\frac{(\mathrm{W} / \mathrm{L})_{7}}{(\mathrm{~W} / \mathrm{L})_{4}}=2 \frac{(\mathrm{~W} / \mathrm{L})_{6}}{(\mathrm{~W} / \mathrm{L})_{5}} \tag{6.38}
\end{equation*}
$$

which is satisfied for the sizes shown. Note that this analysis ignores any voltage drop in a output buffer sourcefollower stage (not shown in Fig. 6.3) and any mismatches between the output impedance of p-channel and n -channel transistors. Fortunately, these effects cause only minor offset voltages, and by satisfying (6.38), offset voltages on the order of 5 mV or less can be obtained.

#### EXAMPLE 6.6

Consider the opamp of Fig. 6.3, where $Q_{3}$ and $Q_{4}$ are each changed to widths of $10 \mu \mathrm{~m}$, and we want the output stage to have a bias current of $400 \mu \mathrm{~A}$. Find the new sizes of $Q_{6}$ and $Q_{7}$, such that there is no systematic offset voltage.

#### Solution

Since $\mathrm{I}_{\mathrm{D} 6}$ determines the bias current of the output stage, and since it should have 2-times more current than $\mathrm{I}_{\mathrm{D} 5}$, its width should be 2-times greater than $\mathrm{W}_{5}$, resulting in

$$
\begin{equation*}
\mathrm{W}_{6}=60 \mu \mathrm{~m} \tag{6.39}
\end{equation*}
$$

For $Q_{7}$, we use (6.38), which leads to

$$
\begin{equation*}
\mathrm{W}_{7}=\frac{2(60)(10)}{30} \mu \mathrm{~m}=40 \mu \mathrm{~m} \tag{6.40}
\end{equation*}
$$

## 6.2 OPAMP COMPENSATION

This section discusses using opamps in closed-loop configurations and how to compensate an opamp to ensure that the closed-loop configuration is not only stable, but also has good settling characteristics. Although the twostage opamp is used as an example, almost all the material discussed here applies to other opamps as well.

Optimum compensation of opamps is typically considered to be one of the most difficult parts of the opamp design procedure. However, if the systematic approach taken here is used, then a straightforward procedure can be followed that almost always results in a near-optimum compensation network.

### 6.2.1 Dominant-Pole Compensation and Lead Compensation

The two most popular tools available to analog circuit designers for opamp compensation are dominant-pole compensation and lead compensation.

Key Point: In general, dominant-pole compensation is performed by decreasing the frequency of one pole in a feedback loop while leaving the others relatively unchanged.

Dominant-pole compensation is performed by forcing a feedback system's open-loop response to be closely approximated by a first-order response up to the loop's unity gain frequency. As described in Section 5.3.1, first-order feedback systems are unconditionally stable with at least $90^{\circ}$ phase margin. Unfortunately, opamp circuits generally have multiple poles and zeros. Increasing the frequency of poles in a circuit is not generally practical since that would demand increased power consumption or some other undesirable trade-off. Hence, the easiest way to make the system behave like a first-order system is to intentionally decrease the frequency of one dominant pole, making it much lower than the other poles and zeros of the system. The idea is illustrated in Fig. 6.8 which plots the open loop response, $L(\omega)$. Recall that $L(\omega)$ is the product of the amplifier response and the feedback network response, $A(\omega) \beta$. During dominant-pole compensation the pole frequency $\omega_{\mathrm{p} 1}$ has been decreased to a new much lower frequency. The result is a decrease in the unity-gain frequency of $\mathrm{L}, \omega_{\mathrm{t}}$, and an attendant increase in phase margin.

A further increase in phase margin is obtained by lead compensation which introduces a left half-plane zero, $\omega_{z}$, at a frequency slightly greater than $\omega_{t}$. If done properly, this has minimal effect on the unity-gain frequency, but does introduce an additional approximately $+20^{\circ}$ phase shift around the unity-gain frequency. This results in a higher unity-gain frequency for a specified phase margin than would be attainable using dominant-pole compensation alone.

In Fig. 6.8, both dominant-pole and lead compensation are illustrated having minimal impact on the dc loop gain and the other pole and zero frequencies. Depending upon the specific circuit implementation of the compensation, the situation may be somewhat more complicated. The approach is next described in detail for a classic two-stage opamp.

Key Point: Lead compensation in opamp circuits introduces into the loop response a left half-planezero at a frequency slightly greater than the unity gain frequency to provide a small phase lead and, therefore, and increase in phase margin.

### 6.2.2 Compensating the Two-Stage Opamp

Stability and phase margin depend upon the loop gain of a feedback amplifier, $L(s)$, whereas our analysis so far has focused on the response of the amplifier alone, $\mathrm{A}_{\mathrm{v}}(\mathrm{s})$. The feedback network must be ac counted for in compensation. It was shown in Section 5.4 that for either inverting or noninverting opamp configurations, the undriven circuit is as shown in Fig. 6.9 and that assuming the opamp has relatively high input impedance and an output impedance

Key Point: The feedback network must be accounted for in compensation.
smaller than the load or feedback network, the loop gain may be approximated as

$$
\begin{equation*}
\mathrm{L}(\mathrm{~s}) \approx \mathrm{A}_{\mathrm{v}}(\mathrm{~s}) \frac{\mathrm{Z}_{1}}{\mathrm{Z}_{1}+\mathrm{Z}_{2}} \tag{6.41}
\end{equation*}
$$

image_name:Fig. 6.8
description:The graph in Fig. 6.8 is a Bode plot, which is used to illustrate the frequency response of a system, specifically focusing on the open-loop gain and phase characteristics. The Bode plot is divided into two main sections: the magnitude plot (top) and the phase plot (bottom).

1. **Type of Graph and Function:**
- This is a Bode plot, showing both magnitude and phase response of the open-loop gain.

2. **Axes Labels and Units:**
- The horizontal axis represents frequency, denoted as \( \omega \), and is typically in a logarithmic scale.
- The vertical axis of the magnitude plot is \(|L(\omega)|\), showing the gain, and the vertical axis of the phase plot is \(\angle L(\omega)\), showing the phase angle in degrees.

3. **Overall Behavior and Trends:**
- **Magnitude Plot:**
- Initially, the magnitude remains constant at \( A_0 \beta \) until it reaches the first pole \( \omega_{p1} \), after which it begins to decrease linearly on a logarithmic scale.
- The plot shows three scenarios: no compensation, dominant-pole compensation, and dominant-pole plus lead compensation. Without compensation, the magnitude continues to drop sharply beyond \( \omega_t \). With dominant-pole compensation, the drop is less steep, and with lead compensation, the curve flattens further, improving stability.
- **Phase Plot:**
- The phase starts at 0° and begins to decrease as frequency increases. The phase margin is improved with dominant-pole and lead compensation, indicating enhanced stability.

4. **Key Features and Technical Details:**
- **Cut-off Frequencies:**
- \( \omega_{p1}, \omega_{p2}, \omega_{p3} \) are pole frequencies where the slope changes.
- \( \omega_t \) is the frequency where the transition occurs.
- \( \omega_z \) is the zero frequency introduced by lead compensation.
- **Phase Margin:**
- The phase margin increases with compensation strategies, as indicated by the annotations.

5. **Annotations and Specific Data Points:**
- The plot includes annotations for various compensation strategies, showing their impact on both magnitude and phase.
- Reference lines are drawn at key frequencies and phase angles (90° and 180°) to highlight changes in behavior.
- The phase margin improvement is specifically noted after applying dominant-pole and lead compensation.
Fig. 6.8 A Bode plot of open-loop gain illustrating dominant-pole and lead compensation.

image_name:Fig. 6.9
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Out(A1)}
name: Z1, type: Resistor, value: Z1, ports: {N1: GND, N2: InN(A1)}
name: Z2, type: Resistor, value: Z2, ports: {N1: InN(A1), N2: Out(A1)}
]
extrainfo:The circuit is a basic feedback network with an operational amplifier, where Z1 and Z2 form a voltage divider connected to the inverting input of the op-amp.

Fig. 6.9 An undriven opamp circuit with a general feedback network.

Although there are several different possible ways to factor $L(s)$ into $A(s)$ and $\beta,{ }^{10}$ the following straightforward approximation $\beta=Z_{1} /\left(Z_{1}+Z_{2}\right)$ may be adopted and it is assumed for analysis that $\beta$ is constant up to the loop's unity gain frequency. For example, in a unity gain configuration, $\beta=1$ and $L(s) \cong A_{v}(s)$. For an accurate determination of phase margin, simulation may be used to properly account for the impact of loading.

The capacitor, $\mathrm{C}_{\mathrm{C}}$, controls the dominant first pole, (i.e., $\omega_{\mathrm{pl}}$ ), and thereby the loop's unity-gain frequency, $\omega_{\mathrm{t}}$.

$$
\begin{equation*}
\omega_{\mathrm{t}}=\mathrm{L}_{0} \omega_{\mathrm{p} 1}=\beta \mathrm{g}_{\mathrm{m} 1} / \mathrm{C}_{\mathrm{c}} \tag{6.42}
\end{equation*}
$$

Hence, by properly selecting the value of $\mathrm{C}_{\mathrm{C}}$ dominant-pole compensation can be achieved.
Lead compensation is achieved using $\mathrm{R}_{\mathrm{C}}$. If the small-signal model of Fig. 6.5 is reanalyzed with a nonzero $\mathrm{R}_{\mathrm{C}}$, then a third-order denominator results. The first two poles are still approximately at the frequencies given by (6.19) and (6.20). The third pole is at a high frequency and has almost no effect. However, the zero is now determined by the relationship

$$
\begin{equation*}
\omega_{\mathrm{z}}=\frac{-1}{\mathrm{C}_{\mathrm{C}}\left(1 / \mathrm{g}_{\mathrm{m} 7}-\mathrm{R}_{\mathrm{C}}\right)} \tag{6.43}
\end{equation*}
$$

This result allows the designer a number of possibilities. One could take

$$
\begin{equation*}
\mathrm{R}_{\mathrm{C}}=1 / \mathrm{g}_{\mathrm{m} 7} \tag{6.44}
\end{equation*}
$$

to eliminate the right-half-plane zero altogether. Alternatively, one could choose $R_{C}$ to be larger and thus move the right-half-plane zero into the left half plane to cancel the nondominant pole, $\omega_{\mathrm{p} 2}$. Setting (6.43) equal to (6.20) and solving for $R_{C}$ results in the following equation for $R_{C}$ :

$$
\begin{equation*}
\mathrm{R}_{\mathrm{C}}=\frac{1}{\mathrm{~g}_{\mathrm{m} 7}}\left(1+\frac{\mathrm{C}_{1}+\mathrm{C}_{2}}{\mathrm{C}_{\mathrm{c}}}\right) \tag{6.45}
\end{equation*}
$$

Unfortunately, $\mathrm{C}_{2}$ is often not known a priori, especially when no output stage is present.
The third possibility (recommended by the authors) is to choose $R_{C}$ even larger to move the now left-halfplane zero to a frequency slightly greater than the unity-gain frequency that would result if the lead resistor were not present [Roberge, 1975]. For example, if the new zero frequency is taken $70 \%$ higher than the unity-gain frequency, it will introduce a phase lead of $\tan ^{-1}(1 / 1.7)=30^{\circ}$. For this case, one should satisfy the following equation:

$$
\begin{equation*}
\omega_{\mathrm{z}}=1.7 \omega_{\mathrm{t}} \tag{6.46}
\end{equation*}
$$

Assuming $R_{C} \gg>\left(1 / g_{m 7}\right)$, then $\omega_{z} \cong 1 /\left(R_{C} C_{c}\right)$. Recalling from (6.42) that $\omega_{t}=\beta g_{m 1} / C_{c}$, then one should choose $R_{C}$ according to

$$
\begin{equation*}
\mathrm{R}_{\mathrm{C}} \cong \frac{1}{1.7 \beta \mathrm{~g}_{\mathrm{m} 1}} \tag{6.47}
\end{equation*}
$$

[^6]Finally, the lead compensation resistor $\mathrm{R}_{\mathrm{C}}$ may be replaced by a transistor operating in the triode region, as illustrated in Fig. 6.10. Transistor $Q_{9}$ has $V_{D S 9}=0$ since no dc bias current flows through it, and therefore $Q_{9}$ is deep in the triode region. Thus, this transistor operates as a resistor, $\mathrm{R}_{\mathrm{C}}$, with a value given by

$$
\begin{equation*}
R_{C}=r_{d s 9}=\frac{1}{\mu_{\mathrm{n}} C_{o x}\left(\frac{W}{L}\right)_{9} V_{\text {eff9 }}} \tag{6.48}
\end{equation*}
$$

It should be noted here that $r_{\text {ds }}$ indicates the drain-source resistance of $Q_{9}$ when it is in the triode region as opposed to the finite-output impedance of $Q_{9}$ when it is in the active mode. The same notation, $r_{\mathrm{ds}}$, is used to indicate the drain-source resistance in both cases-whether the transistor is in the active or the triode region. One simply has to check which region a transistor is operating in to ensure that the correct equation is used to determine $r_{d s}$.

This approach leads to the following design procedure for compensation of a two-stage CMOS opamp:

Key Point: Compensation of the two-stage opamp proceeds by selecting Miller capacitor $\mathrm{C}_{\mathrm{C}}$ to provide 55 degrees phase margin, then introducing a lead compensation series resistor to add another 30 degrees of phase margin.

1. Start by choosing, somewhat arbitrarily, $C_{C}^{\prime} \cong\left(\beta g_{m 1} / g_{m 7}\right) C_{L}$. This initially places the loop's unity gain frequency (6.42) approximately at the frequency of the second pole (6.20), where it has been assumed that the load capacitance $\mathrm{C}_{\mathrm{L}}$ is dominant.
2. Using SPICE, find the frequency at which a $-125^{\circ}$ phase shift exists. Let the gain at this frequency be denoted $A^{\prime}$. Also, let the frequency be denoted $\omega_{\mathrm{t}}$. This is the frequency that we would like to become the unity-gain frequency of the loop gain.
3. Choose a new $\mathrm{C}_{\mathrm{C}}$ so that $\omega_{\mathrm{t}}$ becomes the unity-gain frequency of the loop gain, thus resulting in a $55^{\circ}$ phase margin. (Obtaining this phase margin is the reason we chose $-125^{\circ}$ in step 2.) This can be achieved by taking $\mathrm{C}_{\mathrm{C}}$ according to the equation

$$
\begin{equation*}
C_{C}=C_{C}^{\prime} A^{\prime} \tag{6.49}
\end{equation*}
$$

It might be necessary to iterate on $\mathrm{C}_{\mathrm{C}}$ a couple of times using SPICE.
4. Choose $R_{C}$ according to

$$
\begin{equation*}
\mathrm{R}_{\mathrm{C}}=\frac{1}{1.7 \omega_{\mathrm{t}} \mathrm{C}_{\mathrm{c}}} \tag{6.50}
\end{equation*}
$$

This choice will increase the phase margin approximately $30^{\circ}$ resulting in a total phase margin of approximately $85^{\circ}$. It allows a margin of $5^{\circ}$ to account for processing variations without the poles of the closed-loop response becoming real. This choice is a lso almost optimum lead compensation for almost any opamp
image_name:Fig. 6.10
description:
[{'name': 'Q6', 'type': 'PMOS', 'ports': {'S': 'Vdd', 'D': 'Vout', 'G': 'Vbp'}}, {'name': 'Q7', 'type': 'NMOS', 'ports': {'S': 'GND', 'D': 'Vout', 'G': 'Vin'}}, {'name': 'Rc', 'type': 'Resistor', 'ports': {'N1': 'Vin', 'N2': 'rc'}}, {'name': 'CC', 'type': 'Capacitor', 'value': 'CC', 'ports': {'N1': 'X', 'N2': 'Vout'}}]
[{'name': 'Q6', 'type': 'PMOS', 'ports': {'S': 'Vdd', 'D': 'Vout', 'G': 'Vbp'}}, {'name': 'Q7', 'type': 'NMOS', 'ports': {'S': 'GND', 'D': 'Vout', 'G': 'Vin'}}, {'name': 'Q9', 'type': 'NMOS', 'ports': {'S': 'Vin', 'D': 'X', 'G': 'Vg9'}}, {'name': 'CC', 'type': 'Capacitor', 'value': 'CC', 'ports': {'N1': 'X', 'N2': 'Vout'}}]
extrainfo:The circuit shows a common-source second stage of a CMOS two-stage amplifier with lead compensation using a triode transistor Q9 as the compensation resistor RC. The phase margin is increased approximately by 30 degrees, resulting in a total phase margin of about 85 degrees.

Fig. 6.10 The commonsource second stage of a CMOS two-stage amplifier, showing the lead compensation resistor $\mathrm{R}_{\mathrm{c}}$ replaced by triode transistor $\mathrm{Q}_{9}$.
when a resistor is placed in series with the compensation capacitor. It might be necessary to iterate on $R_{C}$ a couple of times to optimize the phase margin because the unity-gain frequency may be shifted somewhat by the lead compensation, and because ( 6.50 ) assumes $R_{C}>>\left(1 / g_{m 7}\right)$. However, one should check that the gain continues to steadily decrease at frequencies above the new unity-gain frequency; otherwise, the transient response can be poor. This situation sometimes occurs when unexpected zeros at frequencies only slightly greater than $\omega_{\mathrm{t}}$ are present.
5. If, after step 4 , the phase margin is not adequate, then increase $C_{C}$ while leaving $R_{C}$ constant. This will move both $\omega_{\mathrm{t}}$ and the lead zero to lower frequencies while keeping their ratio approximately constant, thus minimizing the effects of higher-frequency poles and zeros which, hopefully, do not also move to lower frequencies. In most cases, the higher-frequency poles and zeros (except for the lead zero) will not move to significantly lower frequencies when $\mathrm{C}_{\mathrm{C}}$ is increased.
6. The final step is to replace $R_{C}$ by a transistor. The size of the transistor can be chosen using equation (6.48), which is repeated here for convenience:

$$
\begin{equation*}
R_{C}=r_{d s 9}=\frac{1}{\mu_{\mathrm{n}} C_{o x}\left(\frac{W}{L}\right)_{9} V_{\text {eff9 }}} \tag{6.51}
\end{equation*}
$$

Finally, SPICE can be used again to fine-tune the device dimensions to optimize the phase margin to that obtained in steps 4 and 5.
Not only does the procedure just described apply to the two-stage opamp, but it (or a very similar procedure) has been found to be almost optimum for compensating most types of opamps.

#### EXAMPLE 6.7

An opamp has an open-loop transfer function given by

$$
\begin{equation*}
A(s)=\frac{A_{0}\left(1+s / \omega_{z}\right)}{\left(1+s / \omega_{\mathrm{p} 1}\right)\left(1+s / \omega_{2}\right)} \tag{6.52}
\end{equation*}
$$

Here, $\mathrm{A}_{0}$ is the dc gain of the opamp and $\omega_{z}, \omega_{\mathrm{p}}$, and $\omega_{2}$ are the frequencies of a zero, the dominant pole, and the equivalent second pole, respectively. Assume that $\omega_{2}=2 \pi \times 50 \mathrm{MHz}$ and that $\mathrm{A}_{0}=10^{4}$. The opamp is to be used in a unity-gain configuration so that $\beta=1$ and $L(s)=A(s)$.
a. Assuming $\omega_{z} \rightarrow \infty$, find $\omega_{\mathrm{p} 1}$ and the unity-gain frequency, $\omega_{\mathrm{t}}^{\prime}$, so that the opamp has a unity-gain phase margin of $55^{\circ}$.
b. Assuming $\omega_{\mathrm{z}}=1.7 \omega_{\mathrm{t}}^{\prime}$ (where $\omega_{\mathrm{t}}^{\prime}$ is as found in part (a)), what is the new unity-gain frequency, $\omega_{\mathrm{t}}$ ? Also, find the new phase margin.

#### Solution

First, note that at frequencies much greater than the dominant-pole frequency (i.e., $\omega>>\omega_{\text {p }}$ ), such as the unitygain frequency, (6.52) can be approximated by

$$
\begin{equation*}
L(s)=A(s) \cong \frac{A_{0}\left(1+s / \omega_{z}\right)}{\left(s / \omega_{p 1}\right)\left(1+s / \omega_{2}\right)} \tag{6.53}
\end{equation*}
$$

(a) For $\omega_{\mathrm{z}} \rightarrow \infty$ we use (6.53) to find the phase angle at $\omega_{\mathrm{t}}^{\prime}$ :

$$
\begin{equation*}
\angle \mathrm{A}\left(\mathrm{j} \omega_{\mathrm{t}}^{\prime}\right)=-90^{\circ}-\tan ^{-1}\left(\omega_{\mathrm{t}}^{\prime} / \omega_{2}\right) \tag{6.54}
\end{equation*}
$$

For a phase margin of $\mathrm{PM}=55^{\circ}$, we need

$$
\begin{equation*}
\angle A\left(j \omega_{\mathrm{t}}^{\prime}\right)=-180^{\circ}+P M=-125^{\circ} \tag{6.55}
\end{equation*}
$$

Setting (6.54) equal to (6.55) and solving for $\omega_{\mathrm{t}}^{\prime} / \omega_{2}$ results in

$$
\begin{align*}
& \tan ^{-1}\left(\omega_{\mathrm{t}}^{\prime} / \omega_{2}\right)=35^{\circ}  \tag{6.56}\\
\Rightarrow \omega_{\mathrm{t}}^{\prime}= & 2.2 \times 10^{8} \mathrm{rad} / \mathrm{s}=2 \pi \times 35 \mathrm{MHz}
\end{align*}
$$

Next, setting $\left|A\left(j \omega_{\mathrm{t}}^{\prime}\right)\right|=1$ and again using (6.53) results in

$$
\begin{gather*}
\frac{\mathrm{A}_{0}}{\left(\omega_{\mathrm{t}}^{\prime} / \omega_{\mathrm{p} 1}\right) \sqrt{1+\left(\omega_{\mathrm{t}}^{\prime} / \omega_{2}\right)^{2}}}=1  \tag{6.57}\\
\Rightarrow \omega_{\mathrm{p} 1}=\frac{\omega_{\mathrm{t}}^{\prime} \sqrt{1+\left(\omega_{\mathrm{t}}^{\prime} / \omega_{2}\right)^{2}}}{\mathrm{~A}_{0}}=2 \pi \times 4.28 \mathrm{kHz}
\end{gather*}
$$

(b) First, we set

$$
\begin{equation*}
\omega_{\mathrm{z}}=1.7 \omega_{\mathrm{t}}^{\prime}=2 \pi \times 59.5 \mathrm{MHz} \tag{6.58}
\end{equation*}
$$

To find the new unity-gain frequency, setting $\left|\mathrm{A}\left(\mathrm{j} \omega_{\mathrm{t}}\right)\right|=1$ in (6.53) now gives

$$
\begin{align*}
& \frac{\mathrm{A}_{0} \sqrt{1+\left(\omega_{\mathrm{t}} / \omega_{\mathrm{z}}\right)^{2}}}{\left(\omega_{\mathrm{t}} / \omega_{\mathrm{p} 1}\right) \sqrt{1+\left(\omega_{\mathrm{t}} / \omega_{2}\right)^{2}}}=1  \tag{6.59}\\
& \Rightarrow \omega_{\mathrm{t}}=\frac{\mathrm{A}_{0} \omega_{\mathrm{p} 1} \sqrt{1+\left(\omega_{\mathrm{t}} / \omega_{\mathrm{z}}\right)^{2}}}{\sqrt{1+\left(\omega_{\mathrm{t}} / \omega_{\mathrm{z}}\right)^{2}}}
\end{align*}
$$

This equation can be solved for the new unity-gain frequency. Both sides can be squared, resulting in a quadratic equation in $\omega_{t}$, which can be solved exactly. Alternatively, the value for $\omega_{\mathrm{t}}^{\prime}$ found in part (a) can be used as an initial guess, and (6.59) can be solved iteratively. After four iterations, one finds that $\omega_{t}=2 \pi \times 39.8 \mathrm{MHz}$. This unity-gain frequency is a 14 percent increase over that found in part (a). We can solve for the new phase shift by using

$$
\begin{equation*}
\angle \mathrm{A}\left(\mathrm{j} \omega_{\mathrm{t}}\right)=-90^{\circ}+\tan ^{-1}\left(\omega_{\mathrm{t}} / \omega_{\mathrm{z}}\right)-\tan ^{-1}\left(\omega_{\mathrm{t}} / \omega_{2}\right)=-95^{\circ} \tag{6.60}
\end{equation*}
$$

Note that this phase value gives a phase margin of $85^{\circ}$, which is a $30^{\circ}$ improvement. In practice, the improvement may not be this great due to additional high-frequency poles and zeros (which have been ignored here). Regardless of this degradation, the improvement from using lead compensation is substantial.

### 6.2.3 Making Compensation Independent of Process and Temperature

This section shows how lead compensation can be made process and temperature insensitive. Repeating equations (6.9) and (6.20) here, we have

$$
\begin{equation*}
\omega_{\mathrm{t}}=\frac{\mathrm{g}_{\mathrm{m} 1}}{\mathrm{C}_{\mathrm{c}}} \tag{6.61}
\end{equation*}
$$

and

$$
\begin{equation*}
\omega_{\mathrm{p} 2} \cong \frac{g_{\mathrm{m} 7}}{\mathrm{C}_{1}+C_{2}} \tag{6.62}
\end{equation*}
$$

We see here that the second pole is proportional to the transconductance of the drive transistor of the second stage, $\mathrm{g}_{\mathrm{m} 7}$. Also, the unity-gain frequency is proportional to the transconductance of the input transistor of the first stage, $\mathrm{g}_{\mathrm{m}}$. Furthermore, the ratios of all of the transconductances remain relatively constant over process and temperature variations since the transconductances are all determined by the same biasing network. ${ }^{11}$ Also, most of the capacitances also track each other since they are primarily determined by gate oxides. Repeating (6.43), when a resistor is used to realize lead compensation, the lead zero is at a frequency given by

$$
\begin{equation*}
\omega_{\mathrm{z}}=\frac{-1}{\mathrm{C}_{\mathrm{C}}\left(1 / \mathrm{g}_{\mathrm{m} 7}-\mathrm{R}_{\mathrm{C}}\right)} \tag{6.63}
\end{equation*}
$$

Thus, if $R_{C}$ can also be made to track the inverse of transconductances, and in particular $1 / g_{m}$, then the lead zero will also be proportional to the transconductance of $Q_{7}$. As a result, the lead zero will remain at the same relative frequency with respect to $\omega_{\mathrm{t}}$ and $\omega_{\mathrm{p} 2}$, as well as all other high-frequency poles and zeros. In other words, the lead compensation will be mostly independent of process and temperature variations.

It turns out that $R_{C}$ can be made proportional to $1 / g_{m 7}$ as long as $R_{C}$ is realized by a transistor in the triode region that has an effective gate-source voltage proportional to that of $Q_{7}$. To see this result, recall that $R_{C}$ is actually realized by $Q_{9}$, and therefore we have

$$
\begin{equation*}
R_{C}=r_{\mathrm{ds} 9}=\frac{1}{\mu_{\mathrm{n}} C_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L})_{9} \mathrm{~V}_{\mathrm{eff} \varphi}} \tag{6.64}
\end{equation*}
$$

Also, $\mathrm{g}_{\mathrm{m} 7}$ is given by

$$
\begin{equation*}
g_{m 7}=\mu_{\mathrm{n}} C_{o x}(W / L)_{7} V_{\text {eff } 7} \tag{6.65}
\end{equation*}
$$

Thus, the product $R_{C} g_{m 7}$, which we want to be a constant, is given by

$$
\begin{equation*}
\mathrm{R}_{\mathrm{C}} \mathrm{~g}_{\mathrm{m} 7}=\frac{(\mathrm{W} / \mathrm{L})_{7} \mathrm{~V}_{\mathrm{eff} 7}}{(\mathrm{~W} / \mathrm{L})_{9} \mathrm{~V}_{\text {eff } 9}} \tag{6.66}
\end{equation*}
$$

image_name:Fig. 6.11
description:
[
name: Q11, type: PMOS, ports: {S: Vdd, D: X, G: Vbias}
name: Q12, type: NMOS, ports: {S: Va, D: X, G: X}
name: Q13, type: NMOS, ports: {S: GND, D: Va, G: Va}
name: Q6, type: PMOS, ports: {S: Vdd, D: d6d7, G: Vbias}
name: Q9, type: NMOS, ports: {S: Vb, D: Y, G: X}
name: CC, type: Capacitor, value: CC, ports: {Np: Y, Nn: d6d7}
name: Q7, type: NMOS, ports: {S: GND, D: d6d7, G: Vb}
]
extrainfo:This is a two-stage opamp with a bias circuit and compensation. The circuit stabilizes the opamp by ensuring that the ratio of effective voltages is constant across process and temperature variations.

Fig. 6.11 The bias circuit, second stage, and compensation circuit of the two-stage opamp.

Therefore, all that remains is to ensure that $\mathrm{V}_{\text {eff } 9} / \mathrm{V}_{\text {eff } 7}$ is independent of process and temperature variations since clearly the remaining terms depend only on a geometric relationship. The ratio $\mathrm{V}_{\text {eff9 }} / \mathrm{V}_{\text {eff } 7}$ can be made constant by deriving $\mathrm{V}_{\mathrm{GS9}}$ from the same biasing circuit used to derive $\mathrm{V}_{\mathrm{GS} 7}$. Specifically, consider the circuit shown in Fig. 6.11 which consists of a bias stage, the second stage, and the compensation network of the two-stage opamp. First we must make $V_{a}=V_{b}$, which is possible by making $\mathrm{V}_{\text {eff13 }}=\mathrm{V}_{\text {eff7 }}$. These two effective gatesource voltages can be made equal by taking

$$
\begin{equation*}
\sqrt{\frac{2 \mathrm{I}_{\mathrm{D} 7}}{\mu_{\mathrm{n}} \mathrm{C}_{\text {ox }}(\mathrm{W} / \mathrm{L})_{7}}}=\sqrt{\frac{2 \mathrm{I}_{\mathrm{D} 13}}{\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L})_{13}}} \tag{6.67}
\end{equation*}
$$

Squaring and simplifying, we see that the following condition must be satisfied:

$$
\begin{equation*}
\frac{\mathrm{I}_{\mathrm{D} 7}}{\mathrm{I}_{\mathrm{D} 13}}=\frac{(\mathrm{W} / \mathrm{L})_{7}}{(\mathrm{~W} / \mathrm{L})_{13}} \tag{6.68}
\end{equation*}
$$

[^7]to $0.4-\mu \mathrm{m}$ CMOS processes).

However, the ratio $I_{D 7} / I_{D 13}$ is set from the current mirror pair $Q_{6}, Q_{11}$, resulting in

$$
\begin{equation*}
\frac{\mathrm{I}_{\mathrm{D} 7}}{\mathrm{I}_{\mathrm{D} 13}}=\frac{(\mathrm{W} / \mathrm{L})_{6}}{(\mathrm{~W} / \mathrm{L})_{11}} \tag{6.69}
\end{equation*}
$$

Thus, to make $\mathrm{V}_{\text {eff13 }}=\mathrm{V}_{\text {eff7 }}$, from (6.68) and (6.69), we need to satisfy the following relationship:

$$
\begin{equation*}
\frac{(\mathrm{W} / \mathrm{L})_{6}}{(\mathrm{~W} / \mathrm{L})_{7}}=\frac{(\mathrm{W} / \mathrm{L})_{11}}{(\mathrm{~W} / \mathrm{L})_{13}} \tag{6.70}
\end{equation*}
$$

Assuming this condition is satisfied, we have $\mathrm{V}_{\text {eff } 13}=\mathrm{V}_{\text {eff } 7}$, and therefore we also have $\mathrm{V}_{\mathrm{a}}=\mathrm{V}_{\mathrm{b}}$. Since the gates of $Q_{12}$ and $Q_{9}$ are connected and their source voltages are the same, we also have $V_{\text {eff12 }}=V_{\text {eff9 }}$. Next, using these gate-source relationships and noting that $\mathrm{I}_{\mathrm{D} 12}=\mathrm{I}_{\mathrm{D} 13}$, we can write

$$
\begin{equation*}
\frac{V_{\text {eff17 }}}{V_{\text {eff16 }}}=\frac{V_{\text {eff13 }}}{V_{\text {eff12 }}}=\frac{\sqrt{\frac{2 I_{D 13}}{\mu_{n} C_{0 x}(W / L)_{13}}}}{\sqrt{\frac{2 I_{D 12}}{\mu_{n} C_{0 x}(W / L)_{12}}}}=\sqrt{\frac{(W / L)_{12}}{(W / L)_{13}}} \tag{6.71}
\end{equation*}
$$

Finally, substituting (6.71) into (6.66), we have the product $\mathrm{R}_{\mathrm{C}} \mathrm{g}_{\mathrm{m} 7}$, given by

$$
\begin{equation*}
\mathrm{R}_{\mathrm{c}} \mathrm{~g}_{\mathrm{m} 7}=\frac{(\mathrm{W} / \mathrm{L})_{7}}{(\mathrm{~W} / \mathrm{L})_{9}} \sqrt{\frac{(\mathrm{~W} / \mathrm{L})_{12}}{(\mathrm{~W} / \mathrm{L})_{13}}} \tag{6.72}
\end{equation*}
$$

which is only dependent on geometry and not on processing or temperature variations.
As a result, we have guaranteed that the drain-source resistance of a transistor in the triode region is inversely matched to the transconductance of a different transistor. This relationship can be very useful for many other applications as well. Indeed, in Chapter 7 we will see that it's quite simple to make all of the transconductances of transistors in a microcircuit match the conductance of a single off-chip resistor. This approach results in the possibility of on-chip "resistors," realized by using triode-region transistors that are accurately ratioed with respect to a single off-chip resistor. This relationship can be very useful in modern circuit design.

## 6.3 ADVANCED CURRENT MIRRORS

### 6.3.1 Wide-Swing Current Mirrors

As newer technologies with shorter channel lengths are used, it becomes more difficult to achieve reasonable opamp gains due to transistor output-impedance degradation caused by short-channel effects. As a result, designers are often forced to use cascode current mirrors. Unfortunately, the use of conventional cascode current mirrors limits the signal swings available, which may not be tolerated in certain applications. Fortunately, circuits exist that do not limit the signal swings as much as the current mirrors discussed in Chapter 3. One such circuit is shown in Fig. 6.12 and is often called the "wide-swing cascode current mirror" [Sooch, 1985; Babanezhad,
image_name:Fig. 6.12
description:This circuit is a wide-swing cascode current mirror designed to bias the drain-source voltages of transistors Q2 and Q3 close to the minimum possible without entering the triode region. It allows for larger signal swings compared to conventional cascode current mirrors.

Fig. 6.12 The wide-swing cascode Current. 1987].

The basic idea of this current mirror is to bias the drain-source voltages of transistors $Q_{2}$ and $Q_{3}$ to be close to the minimum possible without them going into the triode region. Specifically, if the sizes shown in Fig. 6.12 are used, and assuming the classical square-law equations for long channel-length devices are valid, transistors $Q_{2}$ and $Q_{3}$ will be biased right at the edge of the triode region. Before seeing how these bias voltages are created, note that the transistor pair $\mathrm{Q}_{3}, \mathrm{Q}_{4}$ acts like a single diode-connected transistor in creating the gate-source voltage for $Q_{3}$. These two transistors operate very similarly to how $Q_{3}$ alone would operate if its gate were connected to its drain. The reason for including $Q_{4}$ is to lower the drain-source voltage of $Q_{3}$ so that it is matched to the drainsource voltage of $Q_{2}$. This matching makes the output current, $I_{\text {out }}$, more accurately match the input current, $I_{\text {in }}$. If $\mathrm{Q}_{4}$ were not included, then the output current would be a little smaller than the input current due to the finite output impedances of $Q_{2}$ and $Q_{3}$. Other than this, $Q_{4}$ has little effect on the circuit's operation.

To determine the bias voltages for this circuit, let $\mathrm{V}_{\text {eff }}$ be the effective gate-source voltage of $Q_{2}$ and $Q_{3}$, and assume all of the drain currents are equal. We therefore have

$$
\begin{equation*}
V_{\text {eff }}=V_{\text {eff } 2}=V_{\text {eff } 3}=\sqrt{\frac{2 I_{\mathrm{D} 2}}{\mu_{\mathrm{n}} C_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L})}} \tag{6.73}
\end{equation*}
$$

Furthermore, since $Q_{5}$ has the same drain current but is $(n+1)^{2}$ times smaller, we have

$$
\begin{equation*}
V_{\text {eff } 5}=(n+1) V_{\text {eff }} \tag{6.74}
\end{equation*}
$$

Similar reasoning results in the effective gate-source voltages of $Q_{1}$ and $Q_{4}$ being given by

$$
\begin{equation*}
V_{\text {eff } 1}=V_{\text {eff } 4}=n V_{\text {eff }} \tag{6.75}
\end{equation*}
$$

Thus,

$$
\begin{equation*}
\mathrm{V}_{\mathrm{G} 5}=\mathrm{V}_{\mathrm{G} 4}=\mathrm{V}_{\mathrm{G} 1}=(\mathrm{n}+1) \mathrm{V}_{\mathrm{eff}}+\mathrm{V}_{\mathrm{tn}} \tag{6.76}
\end{equation*}
$$

Furthermore,

$$
\begin{equation*}
V_{D S 2}=V_{D S 3}=V_{G 5}-V_{G S 1}=V_{G 5}-\left(n V_{\text {eff }}+V_{t \mathrm{t}}\right)=V_{\text {eff }} \tag{6.77}
\end{equation*}
$$

This drain-source voltage puts both $Q_{2}$ and $Q_{3}$ right at the edge of the triode region. Thus, the minimum allowable output voltage is now

$$
\begin{equation*}
V_{\text {out }}>V_{\text {eff } 1}+V_{\text {eff } 2}=(n+1) V_{\text {eff }} \tag{6.78}
\end{equation*}
$$

A common choice for n might be simply unity, in which case the current mirror operates correctly as long as

$$
\begin{equation*}
V_{\text {out }}>2 V_{\text {eff }} \tag{6.79}
\end{equation*}
$$

With a typical value of $\mathrm{V}_{\text {eff }}$ between 0.2 V and 0.25 V , the wide-swing current mirror can guarantee that all of the transistors are in the active (i.e., saturation) region even when the voltage drop across the mirror is as small as 0.4 V to 0.5 V .

However, there is one other requirement that must be met to ensure that all transistors are in the active region. Specifically, we need

$$
\begin{equation*}
V_{D S 4}>V_{\text {eff } 4}=n V_{\text {eff }} \tag{6.80}
\end{equation*}
$$

to guarantee that $Q_{4}$ is in the active region. To find $V_{D S 4}$, we note that the gate of $Q_{3}$ is connected to the drain of $\mathrm{Q}_{4}$, resulting in

$$
\begin{equation*}
V_{D S 4}=V_{G 3}-V_{D S 3}=\left(V_{\text {eff }}+V_{t n}\right)-V_{\text {eff }}=V_{t n} \tag{6.81}
\end{equation*}
$$

Key Point: Cascoding is a key technique to enable high gain using transistors with low drain-source resistance, but if the cascode transistor is improperly biased, output swing is greatly reduced.

As a result, one need only ensure that $V_{t n}$ be greater than $n V_{\text {eff }}$ for $Q_{4}$ to remain in the active region-not a difficult requirement.

It should be noted that this circuit was analyzed assuming the bias current, $I_{\text {bias }}$, equals the input current, $I_{i n}$. Since, in general, $I_{\text {in }}$ may be a varying current level, there is some choice as to what $I_{\text {bias }}$ value should be chosen. One choice is to set $I_{\text {bias }}$ to the largest expected value for $I_{i n}$. Such a choice will ensure that none of the devices exit their active region, though
the drain-source voltage of $Q_{2}$ and $Q_{3}$ will be larger than necessary except when the maximum $I_{i n}$ is applied. As a result, some voltage swing will be lost. Perhaps the more common choice in a wide-swing opamp is to let $\mathrm{I}_{\text {bias }}$ equal the nominal value of $\mathrm{I}_{\mathrm{in}}$. With this setting, some devices will enter triode and the output impedance will be reduced for larger $\mathrm{I}_{\text {in }}$ values (say, during slew-rate limiting), but such an effect during transient conditions can often be tolerated.

Before leaving this circuit, a few design comments are worth mentioning. In most applications, an experienced designer would take $(\mathrm{W} / \mathrm{L})_{5}$ smaller than the size given in Fig. 6.12 to bias transistors $Q_{2}$ and $Q_{3}$ with slightly larger drain-source voltages than the minimum required (perhaps 0.1 V larger). This increase accounts for the fact that practical transistors don't have a sharp transition between the triode and active regions. This increase would also help offset a second-order effect due to the body effect of $Q_{1}$ and $Q_{4}$, which causes their threshold voltages to increase, which tends to push $Q_{2}$ and $Q_{3}$ more into the triode region. In addition, to save on power dissipation, the bias branch consisting of $Q_{5}$ and $I_{\text {bias }}$ might be scaled to have lower currents while keeping the same current densities and, therefore, the same effective gate-source voltages. A final common modification is to choose the lengths of $Q_{2}$ and $Q_{3}$ just a little larger than the minimum allowable gate length (as the drain-source voltage across them is quite small), but $Q_{1}$ and $Q_{4}$ would be chosen to have longer gate lengths since the output transistor (i.e., $Q_{1}$ ) often has larger voltages across it. A typical size might be twice the minimum allowable channel length. This choice of gate lengths helps eliminate detrimental short-channel effects, such as the drain-to-substrate leakage currents of $Q_{1}$ that might otherwise result. Minimizing the lengths of $Q_{2}$ and $Q_{3}$ maximizes the frequency response, as their gate-source capacitances are the most significant capacitances contributing to highfrequency poles.

### 6.3.2 Enhanced Output-Impedance Current Mirrors and Gain Boosting

Another variation on the cascode current mirror is often referred to as the enhanced output-impedance current mirror. A simplified form of this circuit is shown in Fig. 6.13, and it is used to increase the output impedance. The basic idea is to use a feedback amplifier to keep the drain-source voltage across $Q_{2}$ as stable as possible, irrespective of the output voltage. The addition of this amplifier ideally increases the output impedance by a factor equal to one plus the loop gain over that which would occur for a classical cascode current mirror. Specifically, using the results from Chapter 3,

$$
\begin{equation*}
R_{\text {out }} \cong g_{m 1} r_{d s 1} r_{d s 2}(1+A) \tag{6.82}
\end{equation*}
$$

In practice, the output impedance might be limited by a parasitic conductance between the drain of $Q_{1}$ and its substrate due to
image_name:Fig. 6.13
description:
[
name: Vdd, type: VoltageSource, value: Vdd, ports: {Np: Vdd, Nn: GND}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: Vdd, Nn: P}
name: A, type: OpAmp, value: A, ports: {InP: Vbias, InN: InN, OutP: Out(A)}
name: Q1, type: NMOS, ports: {S: InN, D: Vout, G: Out(A)}
name: Q2, type: NMOS, ports: {S: GND, D: InN, G: P}
name: Q3, type: NMOS, ports: {S: GND, D: InN(A), G: P}
]
extrainfo:The circuit is an enhanced output impedance current mirror with an operational amplifier to increase the output impedance. It uses NMOS transistors Q1, Q2, and Q3, and the output is taken across Rout.

Fig. 6.13 The enhanced outputimpedance current mirror.
short-channel effects. This parasitic conductance is a result of collisions between highly energized electrons resulting in electron-hole pairs to be generated with the holes escaping to the substrate. The generation of these electron-hole pairs is commonly called impact ionization. Stability of the feedback loop comprising the amplifier $A(s)$ and $Q_{1}$ must of course be verified.

The same technique can be applied to increase the output impedance of a cascode gain stage, as shown in Fig. 6.14. The gain of the stage is given by

$$
\begin{equation*}
A_{V}(s)=\frac{V_{\text {out }}(s)}{V_{\text {in }}(s)}=-g_{m_{2}}\left(R_{\text {out }}(s) \| \frac{1}{s C_{\mathrm{L}}}\right) \tag{6.83}
\end{equation*}
$$

where $R_{\text {out }}$ is now a function of frequency and given by

$$
\begin{equation*}
R_{\text {out }}(s)=g_{\mathrm{m} 1} r_{\mathrm{ds} 1} r_{\mathrm{ds} 2}(1+\mathrm{A}(\mathrm{~s})) \tag{6.84}
\end{equation*}
$$

Key Point: Auxiliary amplifiers may be used to enhance the output impedance of cascode current mirrors and gain stages, thereby boosting dc gain.

Note that the gain is increased over a conventional cascode amplifier by a factor $(1+\mathrm{A}(\mathrm{s}))$. The technique is therefore called gain-boosting, and may be used to improve the dc gain of opamp circuits described later in this chapter. Note that gain-boosting is only realized if the output impedance the current mirror active load, denoted $\mathrm{I}_{\text {bias }}$ in Fig. 6.14, is similarly enhanced.

#### EXAMPLE 6.8

image_name:Fig. 6.14 A cascode amplifier with gain-boosting
description:
[
name: A, type: OpAmp, value: A, ports: {InP: Vbias, InN: InN(A), Out: Out(A)}
name: Q1, type: NMOS, ports: {S: InN(A), D: VOut, G: Out(A)}
name: Q2, type: NMOS, ports: {S: GND, D: InN(A), G: Vin}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
name: Ibias, type: CurrentSource, value: Ibias, ports: {Np: VDD, Nn: Vout}
]
extrainfo:The circuit is a cascode amplifier with gain-boosting. The gain is increased by a factor of (1+A(s)) due to the gain-boosting technique. The output impedance of the current mirror active load is enhanced. The amplifier A(s) has a transfer function A(s) = A0 / (1 + sτ1').

Fig. 6.14 A cascode amplifier with gain-boosting.

Assume an amplifier, $\mathrm{A}(\mathrm{s})$, has a transfer function given by

$$
\begin{equation*}
\mathrm{A}(\mathrm{~s})=\frac{\mathrm{A}_{0}}{1+\mathrm{s} \tau_{1}^{\prime}} \cong \frac{\mathrm{A}_{0}}{\mathrm{~s} \tau^{\prime}{ }_{1}} \tag{6.85}
\end{equation*}
$$

around its unity-gain frequency. Find approximate equations for any additional poles and/or zeros introduced by the gain enhancement circuit that are significant around the unity-gain frequency of the commonsource amplifier shown in Fig. 6.14.

#### Solution

Note that at high frequencies, it is not possible to assume that $|A(j \omega)| \gg 1$. Working with conduc-
tances, we have

$$
\begin{equation*}
\mathrm{G}_{\text {out }}(s)=\frac{1}{R_{\text {out }}(s)}=\frac{g_{\mathrm{ds} 1} g_{\mathrm{ds} 2}}{g_{\mathrm{m} 1}(1+A(s))} \tag{6.86}
\end{equation*}
$$

which can be inserted into (6.83) giving

$$
\begin{align*}
A_{V}(s) & =\frac{-g_{m 2}}{s C_{L}+G_{o u t}(s)}=\frac{-g_{m 2}}{s C_{L}+\frac{g_{d s 1} g_{d s 2}}{g_{m 1}(1+A(s))}}  \tag{6.87}\\
& =\frac{-g_{m 2}(1+A(s))}{s C_{L}(1+A(s))+\frac{g_{d s 1} g_{d s}}{g_{m 1}}}
\end{align*}
$$

Substituting (6.85) into (6.87) and rearranging gives

$$
\begin{equation*}
A_{V}(s)=\frac{-g_{m 2}\left(A_{0}+s \tau_{1}^{\prime}\right)}{s\left(A_{0} C_{L}+\frac{g_{d s} g_{d s} \tau_{1}^{\prime}}{g_{m 1}}+s C_{L} \tau_{1}^{\prime}\right)} \tag{6.88}
\end{equation*}
$$

From (6.88), we see that there is a left-hand-plane zero at a frequency given by

$$
\begin{equation*}
\omega_{z}=\frac{A_{0}}{\tau_{1}^{\prime}} \tag{6.89}
\end{equation*}
$$

which is the approximate unity-gain frequency of the amplifier, $A(s)$. Also, there are two poles, but the pole at dc is not accurate since we have made use of approximate equations that are valid only near the unity-gain frequency
of the amplifier. However, the other pole location is a good approximation and it occurs in the left-half-plane given by (after some rearranging)

$$
\begin{equation*}
p_{2}=\frac{A_{0}}{\tau_{1}^{\prime}}+\frac{g_{d s 1} g_{d s 2}}{C_{\llcorner } g_{m 1}}=\frac{A_{0}}{\tau_{1}^{\prime}}+\frac{1}{C_{\mathrm{L}} R^{\prime}} \tag{6.90}
\end{equation*}
$$

Here, we have defined

$$
\begin{equation*}
R^{\prime}=g_{m 1} r_{d s 1} r_{d s 2} \tag{6.91}
\end{equation*}
$$

which is approximately the output impedance of the cascode mirror without enhancement and is quite a large value. Furthermore, note that the term $\mathrm{A}_{0} / \tau_{1}^{\prime}$ is a value near the unity-gain frequency of the amplifier, and therefore, typically the first term in (6.90) dominates. Thus, the added pole frequency is approximately given by

$$
\begin{equation*}
\mathrm{p}_{2} \cong \frac{\mathrm{~A}_{0}}{\tau_{1}^{\prime}} \cong \omega_{\mathrm{z}}^{\prime} \tag{6.92}
\end{equation*}
$$

Therefore, like the new zero, the new pole also occurs around the unity-gain frequency of the amplifier, and their effects mostly cancel each other out. In addition, if the unity-gain frequency of the enhancement loop is greater than the unity-gain frequency of the opamp, the frequency response of the enhancement amplifier shouldn't have a large detrimental effect on the overall frequency response.

The enhanced output-impedance current mirror appears to have been originally proposed in [Hosticka, 1979] for singleended input amplifiers and more recently described almost simultaneously in [Bult, 1990] and [Säckinger, 1990] for differentialinput amplifiers. Bult proposed that complete opamps be used for each current mirror. In a modern fully differential opamp, this might increase the number of opamps by four, although these extra opamps can be scaled to have less power dissipation. The implementation proposed by Säckinger is shown in Fig. 6.15. The feedback amplifier in this case is realized by the common-source amplifier consisting of $Q_{3}$ and its current source $I_{B 1}$. Assuming the output impedance of current source $I_{B 1}$ is approximately equal to $r_{d s 3}$, the loop gain will be $\left(g_{m 3} r_{d s 3}\right) / 2$, and the final ideal output impedance will be given by

$$
\begin{equation*}
r_{\text {out }} \cong \frac{g_{m 1} g_{m 3} r_{d s 1} r_{d s 2} r_{d s 3}}{2} \tag{6.93}
\end{equation*}
$$

image_name:Fig. 6.15
description:The circuit is a Säckinger implementation of an enhanced output-impedance current mirror. It uses NMOS transistors and current sources to ensure accurate matching of input and output currents. The feedback amplifier is realized by a common-source amplifier with Q3 and its current source I_B1.

Fig. 6.15 The Säckinger implementation of the enhanced output-impedance current mirror.

The circuit consisting of $Q_{4}, Q_{5}, Q_{6}, I_{i n}$, and $I_{B 2}$ operates almost identically to a diode-connected transistor, but is used instead to guarantee that all transistor bias voltages are accurately matched to those of the output circuitry consisting of $Q_{1}, Q_{2}, Q_{3}$, and $I_{B 1}$. As a result, $I_{\text {out }}$ will very accurately match $I_{i n}$.

The Säckinger realization is much simpler than that proposed by Bult, but has a major limitation in that the signal swing is significantly reduced. This reduction is a result of $Q_{2}$ and $Q_{5}$ being biased to have drain-source voltages much larger than the minimum required. Specifically, their drain-source voltages are given by

$$
\begin{equation*}
\mathrm{V}_{\mathrm{DS} 2}=\mathrm{V}_{\mathrm{DS} 5}=\mathrm{V}_{\mathrm{eff} 3}+\mathrm{V}_{\mathrm{tn}} \tag{6.94}
\end{equation*}
$$

rather than the minimum required, which would be equal to $\mathrm{V}_{\text {efit }}$. This limitation is especially harmful for modern technologies operating with power supply voltages of 3.3 V or lower. In the next subsection, an alternative realization is described that combines the wide-swing current mirror with the enhanced output-impedance circuit.

### 6.3.3 Wide-Swing Current Mirror with Enhanced Output Impedance

This current mirror was originally described in [Gatti, 1990] for use in current-mode continuous-time filters and was then used in the design of wide-signal-swing opamps [Coban, 1994; Martin, 1994]. It is very similar to the enhanced output-impedance current mirrors of [Säckinger, 1990], except that diode-connected transistors used as level shifters have been added in front of the common-source enhancement amplifiers, as shown in Fig. 6.16. At the output side, the level shifter is the diode-connected transistor, $Q_{4}$, biased with current $I_{\text {bias }}$. The circuitry at the input basically acts as a diode-connected transistor while ensuring that all bias voltages are matched to the output circuitry so that $\mathrm{I}_{\text {out }}$ accurately matches $\mathrm{I}_{\text {in }}$. Shown next to each transistor is a reasonable width in $\mu \mathrm{m}$. Note that for the case in which

$$
\begin{equation*}
\mathrm{I}_{\mathrm{bias}}=\mathrm{I}_{\mathrm{in}} / 7 \tag{6.95}
\end{equation*}
$$

all transistors are biased with nearly the same current density, except for $Q_{3}$ and $Q_{7}$. As a result, all transistors have the same effective gate-source voltages, $\mathrm{V}_{\text {eff }}$, except for $\mathrm{Q}_{3}$ and $\mathrm{Q}_{7}$, which have gate-source voltages of $2 \mathrm{~V}_{\text {eff }}$ because they are biased at four times the current density. Thus, we find that the gate voltage of $Q_{3}$ equals

$$
\begin{equation*}
V_{G 3}=2 V_{\text {eff }}+V_{t n} \tag{6.96}
\end{equation*}
$$

and the drain-source voltage of $Q_{2}$ is given by

$$
\begin{equation*}
\mathrm{V}_{\mathrm{DS} 2}=\mathrm{V}_{\mathrm{S} 4}=\mathrm{V}_{\mathrm{G} 3}-\mathrm{V}_{\mathrm{GS} 4}=\left(2 \mathrm{~V}_{\mathrm{eff}}+\mathrm{V}_{\mathrm{tn}}\right)-\left(\mathrm{V}_{\mathrm{eff}}+\mathrm{V}_{\mathrm{tn}}\right)=\mathrm{V}_{\mathrm{eff}} \tag{6.97}
\end{equation*}
$$

Therefore, $Q_{2}$ is biased on the edge of the triode region and the minimum output voltage is given by

$$
\begin{equation*}
V_{\text {out }}>V_{D S 2}+V_{\text {eff } 1}=2 V_{\text {eff }} \tag{6.98}
\end{equation*}
$$

With the shown values for the $W / L$ ratios, the power dissipation would be almost doubled over that of a classical cascode current mirror, assuming $\mathrm{I}_{\text {bias }}$ is set to one-seventh the nominal or maximum input current value, $I_{i n}$. However, it is possible to bias the enhancement circuitry at lower densities and thereby save on power dissipation, albeit at the expense of speed, as the additional poles introduced by the enhancement circuitry would then be at lower frequencies.

A slightly modified version of the wide-swing enhanced output-impedance mirror is shown in Fig. 6.17. This variation obtains the bias voltage of the cascode transistor of the input diode-connected branch from the bias-generation circuitry of Fig. 6.3. This circuit suffers slightly with regard to large-signal dc matching, but has less power dissipation and area than the circuit of Fig. 6.16. Notice also that $Q_{2}$ of Fig. 6.16 has now been
image_name:Fig. 6.16 A wide-swing current mirror with enhanced output impedance
description:
[
name: Q1, type: NMOS, ports: {S: 80, D: LOAD, G: 70}
name: Q2, type: NMOS, ports: {S: GND, D: 80, G: P1}
name: Q3, type: NMOS, ports: {S: GND, D: 80, G: P4}
name: Q4, type: NMOS, ports: {S: 10, D: P4, G: P3}
name: Q5, type: NMOS, ports: {S: 80, D: 70, G: P1}
name: Q6, type: NMOS, ports: {S: GND, D: 80, G: P1}
name: Q7, type: NMOS, ports: {S: GND, D: 10, G: P3}
name: Q8, type: NMOS, ports: {S: 10, D: P3, G: P3}
name: P1, type: CurrentSource, value: 7Ibias, ports: {Np: VDD, Nn: 70}
name: P2, type: CurrentSource, value: 4Ibias, ports: {Np: VDD, Nn: P2}
name: P3, type: CurrentSource, value: Ibias, ports: {Np: VDD, Nn: P3}
name: P4, type: CurrentSource, value: Ibias, ports: {Np: VDD, Nn: P4}
name: P5, type: CurrentSource, value: 4Ibias, ports: {Np: VDD, Nn: 70}
]
extrainfo:The circuit is a wide-swing current mirror with enhanced output impedance. It uses multiple NMOS transistors and current sources to achieve this. The current source P1 provides the input current Iin equivalent to 7 times the bias current Ibias. The transistors Q5 and Q6 are used for mirroring the input current to the output. The circuit is designed to provide high output impedance and wide swing at the output node. The load current Iout equals the input current Iin.

Fig. 6.16 A wide-swing current mirror with enhanced output impedance. Current source $7 \mathrm{I}_{\text {bias }}$ is typically set to the nominal or maximum input current, $\mathrm{I}_{\mathrm{in}}$.
separated into two transistors, $Q_{2}$ and $Q_{5}$, in Fig. 6.17. This change allows one to design an opamp without the output-impedance enhancement, but with wide-swing mirrors. Then, when output-impedance enhancement is desired, one simply includes the appropriate enhancement amplifiers and the only change required to the original amplifier is to connect the gates of the output cascode mirrors of the appropriate current mirrors to the enhancement amplifiers rather than the bias-generation circuit. Finally, it has been found through simulation that the modified circuit of Fig. 6.17 is less prone to instability than the circuit of Fig. 6.16.

It is predicted that this current mirror will become more important as the newer technologies force designers to use smaller power-supply voltages, which limit voltage swings. Also, the short-channel effects of newer technologies make the use of current mirrors with enhanced output impedance more desirable.

There are a couple of facts that designers should be aware of when they use outputimpedance enhancement. The first fact is that sometimes it may be necessary to add local compensation capacitors to the enhancement loops to prevent ringing during transients. The second fact is that the inclusion of output-impedance enhancement can
image_name:Fig. 6.17 A modified wide-swing current mirror with enhanced output impedance.
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: x, G: P3}
name: Q2, type: NMOS, ports: {S: GND, D: x, G: 70}
name: Q3, type: NMOS, ports: {S: GND, D: P2, G: 10}
name: Q4, type: NMOS, ports: {S: P2, D: P1, G: P2}
name: Q5, type: NMOS, ports: {S: GND, D: x, G: P2}
name: Q6, type: NMOS, ports: {S: sb/d1, D: P1, G: 70}
name: Q7, type: NMOS, ports: {S: GND, D: sb/d1, G: 70}
name: I_in, type: CurrentSource, ports: {Np: P1, Nn: VDD}
name: I_bias, type: CurrentSource, ports: {Np: P2, Nn: VDD}
name: 4I_bias, type: CurrentSource, ports: {Np: P3, Nn: VDD}
name: P1, type: Resistor, value: 70, ports: {N1: P1, N2: sb/d1}
name: P2, type: Resistor, value: 10, ports: {N1: P2, N2: P2}
name: P3, type: Resistor, value: 10, ports: {N1: P3, N2: x}
]
extrainfo:This circuit is a modified wide-swing current mirror with enhanced output impedance. It includes NMOS transistors Q1 to Q7, current sources I_in, I_bias, and 4I_bias, and resistors P1, P2, and P3. The circuit is designed to provide a high output impedance and is used to mirror the input current (I_in) to the output (I_out). The presence of multiple transistors in cascode configuration enhances the output impedance. The resistors and current sources are used to bias the transistors and control the current flow through the circuit.

Fig. 6.17 A modified wide-swing current mirror with enhanced output impedance.
substantially slow down the settling times for large-signal transients. This is because during large-signal transients, the outputs of the enhancement loops can slew to voltages very different from those required after settling, and it can take a while for the outputs to return to the necessary voltages. A typical settling-time difference might be around a 50-percent increase. Whether this is worth the substantial increase in gain (perhaps as much as 30 dB or so) depends on the individual application.

### 6.3.4 Current-Mirror Symbol

It should now be clear that there are a number of different current-mirror circuits, each having various advantages and disadvantages, that can be used in a particular circuit application. Thus, from an architectural perspective, it is often desirable to describe a circuit without showing which particular current mirror is used. In these cases, we make use of the current-mirror symbol shown in Fig. 6.18(a). The arrow is on the input side of
image_name:(a)
description:The diagram represents a current mirror symbol with a current gain ratio of 1:K. The arrows indicate the direction of current flow, with the input side having low impedance.

image_name:(b)
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: g1d1g2, G: g1d1g2}
name: M2, type: PMOS, ports: {S: VDD, D: LOAD2, G: g1d1g2}
]
extrainfo:The circuit is a simple current mirror with PMOS transistors M1 and M2. The current mirror has a current gain ratio of 1:K. The node labeled 'q1d1g2' is the common drain and gate connection of M1 and M2. LOAD1 and LOAD2 are connected to the sources of M1 and M2 respectively.

Fig. 6.18 (a) A symbol representing a current mirror.
(b) Example of a simple current mirror. the mirror, which is the low-impedance side (with an impedance typically equal to $1 / g_{m}$ ). The arrow also designates the direction of current flow on the input side. The ratio, $1: \mathrm{K}$, represents the current gain of the mirror. For example, the current mirror shown in Fig. 6.18(a) might be realized by the simple current mirror shown in Fig. 6.18(b). Finally, it should be mentioned that for illustrative purposes, some circuits in this book will be shown with a particular current mirror (such as the wide-swing mirror) to realize a circuit architecture. However, it should be kept in mind that similar circuits using almost any of the current mirrors just described (or described elsewhere) are possible.

## 6.4 FOLDED-CASCODE OPAMP

Many modern integrated CMOS opamps are designed to drive only capacitive loads. With such capacitive-only loads, it is not necessary to use a voltage buffer to obtain a low output impedance for the opamp. As a result, it is possible to realize opamps having higher speeds and larger signal swings than those that must also drive resistive loads. These improvements are obtained by having only a single high-impedance node at the output of an opamp that drives only capacitive loads. The admittance seen at all other nodes in these opamps is on the order of a transistor's transconductance, and thus they have relatively low impedance. By having all internal nodes of relatively low impedance, the speed of the opamp is maximized. It should also be mentioned that these low node impedances result in reduced voltage signals at all nodes other than the output node; however, the current signals in the various transistors can be quite large. ${ }^{12}$ With these opamps, we shall see that the compensation is usually achieved by the load capacitance. Thus, as the load capacitance gets larger, the opamp usually becomes more stable but also slower. One of the most important parameters of these modern opamps is their transconductance value (i.e., the ratio of the output current to the input voltage). Therefore, some designers refer to these modern opamps as transconductance opamps, or Operational Transconductance Amplifiers (OTAs). A simple first-order smallsignal model for an OTA is shown in Fig. 6.19. The amplifier's transconductance is $\mathrm{G}_{\mathrm{ma}}$ and its frequency response in Fig. 6.19 is given simply by $G_{m a} Z_{L}$.

Key Point: Operational transconductance amplifiers provide a large dc gain from a single stage. Their high output impedance makes them suitable for driving the mostly-capacitive loads encountered in CMOS integrated circuits. With feedback, they can also drive some resistive load.

It should also be noted that feedback generally reduces the output impedance of a opamp circuit by a large factor. Hence, although the OTA itself has high output impedance, the output impedance of the overall feedback circuit is much lower, making it sometimes possible to drive resistive loads with OTAs, as long as the load resistance is modest.

An example of an opamp with a high-output impedance is the foldedcascode opamp, as shown in Fig. 6.20. The design shown is a differential-input single-ended output design. Note that all current mirrors in the circuit are wideswing cascode current mirrors, discussed in Section 6.3.1. The use of these mirrors results in high-output impedance for the mirrors (compared to simple current mirrors), thereby maximizing the dc gain of the opamp. The basic idea of the folded-cascode opamp is to apply cascode transistors to the input differential pair but using transistors opposite in type from those used in the input stage. For example, the differential-pair transistors consisting of $Q_{1}$ and $Q_{2}$ are n -channel transistors in Fig. 6.20, whereas the cascode transistors consisting of $Q_{5}$ and $Q_{6}$ are $p$-channel transistors. This arrangement of opposite-type transistors allows the output of this single gain-stage amplifier to be taken at the same bias-voltage levels as the input signals. It should be mentioned that even though a folded-cascode amplifier is basically a single gain stage, its gain can be quite reasonable, on the order of 700 to 3,000 . Such a high gain occurs because the gain is determined by the product of the input transconductance

Fig. 6.19 First-order model of an operational transconductance amplifier (OTA) driving a capacitive load.
image_name:Fig. 6.19 First-order model of an operational transconductance amplifier (OTA)
description:
[
name: Cin, type: Capacitor, value: Cin, ports: {Np: vip, Nn: vin}
name: GmaVi, type: VoltageControlledCurrentSource, value: GmaVi, ports: {Np: vo, Nn: GND}
name: rout, type: Resistor, value: rout, ports: {N1: vo, N2: GND}
name: Cout, type: Capacitor, value: Cout, ports: {Np: vo, Nn: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: vo, Nn: GND}
]
extrainfo:The circuit is a first-order model of an operational transconductance amplifier (OTA) driving a capacitive load. It includes an input capacitor Cin, a voltage-controlled current source GmaVi, a resistor rout, and capacitors Cout and CL, all connected to the output node vo. The circuit is grounded at multiple points.

image_name:Fig. 6.20 A folded-cascode opamp
description:The circuit is a folded-cascode operational amplifier with differential input and single-ended output. It includes biasing current sources and multiple NMOS and PMOS transistors arranged to achieve high gain and wide output swing. The output is loaded with a capacitor C_L. The design utilizes cascode techniques to increase output impedance and improve gain.

Fig. 6.20 A folded-cascode opamp.
and the output impedance, and the output impedance is quite high due to the use of cascode techniques. In technologies where transistor intrinsic gain is poor, auxiliary gain boosting amplifiers can be used to drive the gates of cascode devices $Q_{5-8}$ and increase dc gain as described in Section 6.3.2.

The shown differential-to-single-ended conversion is realized by the wide-swing current mirror composed of $\mathrm{Q}_{7}, \mathrm{Q}_{8}, \mathrm{Q}_{9}$, and $\mathrm{Q}_{10}$. In a differential-output design, these might be replaced by two wide-swing cascode current sinks, and common-mode feedback circuitry would be added, as is discussed in Sections 6.7 and 6.8.

It should be mentioned that a simplified bias network is shown so as not to complicate matters unnecessarily when the intent is to show the basic architecture. In practical realizations, $Q_{11}$ and $I_{\text {bias } 1}$ might be replaced by the constant-transconductance bias network described in Chapter 7. In this case, $\mathrm{V}_{\mathrm{B} 1}$ and $\mathrm{V}_{\mathrm{B} 2}$ would be connected to $\mathrm{V}_{\text {casc-p }}$ and $\mathrm{V}_{\text {casc-n }}$, respectively, of Fig. 7.8 to maximize the output voltage signal swing.

An important addition of the folded-cascode opamp shown is the inclusion of two extra transistors, $\mathrm{Q}_{12}$ and $\mathrm{Q}_{13}$. These two transistors serve two purposes. One is to increase the slew-rate performance of the opamp, as will be discussed in Example 6.9. However, more importantly, during times of slew-rate limiting, these transistors prevent the drain voltages of $Q_{1}$ and $Q_{2}$ from having large transients where they change from their small-signal voltages to voltages very close to the negative power-supply voltage. Thus the inclusion of $Q_{12}$ and $Q_{13}$ allows the opamp to recover more quickly following a slew-rate condition.

The compensation is realized by the load capacitor, $\mathrm{C}_{\mathrm{L}}$, and realizes dominant-pole compensation. In applications where the load capacitance is very small, it is necessary to add additional compensation capacitance in parallel with the load to guarantee stability. If lead compensation is desired, a resistor can be placed in series with $\mathrm{C}_{\mathrm{L}}$. While lead compensation may not be possible in some applications, such as when the compensation capacitance is mostly supplied by the load capacitance, it is more often possible than many designers realize (i.e., it is often possible to include a resistor in series with the load

Key Point: The foldedcascode opamp is a transconductance amplifier whose frequency response is dominated by the output pole at $1 / R_{\text {out }} \mathrm{C}_{\mathrm{L}}$.
capacitance).

The bias currents for the input differential-pair transistors are equal to $\mathrm{I}_{\mathrm{bias} 2} / 2$. The bias current of one of the p-channel cascode transistors, $Q_{5}$ or $Q_{6}$, and hence the transistors in the output-summing current mirror as well, is
equal to the drain current of $Q_{3}$ or $Q_{4}$ minus $I_{\text {bias } 2} / 2$. This drain current is established by $I_{\text {bias } 1}$ and the ratio of $(\mathrm{W} / \mathrm{L})_{3}$, or $(\mathrm{W} / \mathrm{L})_{4}$, to $(\mathrm{W} / \mathrm{L})_{11}$. Since the bias current of one of the cascode transistors is derived by a current subtraction, for it to be accurately established, it is necessary that both $I_{\text {bias1 }}$ and $I_{\text {bias2 }}$ be derived from a singlebias network. In addition, any current mirrors used in deriving these currents should be composed of transistors realized as parallel combinations of unit-size transistors. This approach eliminates inaccuracies due to secondorder effects caused by transistors having non-equal widths.

### 6.4.1 Small-Signal Analysis

In a small-signal analysis of the folded-cascode amplifier, it is assumed that the differential output current from the drains of the differential pair, $Q_{1}, Q_{2}$, is applied to the load capacitance, $C_{L}$. Specifically, the small-signal current from $Q_{1}$ passes directly from the source to the drain of $Q_{6}$ and thus $C_{\llcorner }$, while the current from $Q_{2}$ goes indirectly through $Q_{5}$ and the current mirror consisting of $Q_{7}$ to $Q_{10}{ }^{13}$ Although these two paths have slightly different transfer functions due to the poles caused by the current mirror, when an $n$-channel transistor current mirror is used, a pole-zero doublet occurs at frequencies quite a bit greater than the opamp unity-gain frequency and can usually be ignored. Hence, ignoring the high-frequency poles and zero, an approximate small-signal transfer function for the folded-cascode opamp is given by

$$
\begin{equation*}
A_{V}=\frac{V_{\text {out }}(s)}{V_{\text {in }}(s)}=g_{m 1} Z_{L}(s) \tag{6.99}
\end{equation*}
$$

In this case, the amplifier's transconductance gain is simply the transconductance of each of the transistors in the input differential pair, $G_{m a}=g_{m 1}$, and $Z_{L}(s)$ is the impedance to ground seen at the output node. This impedance consists of the parallel combination of the output load capacitance, the impedance of any additional network added for stability, and the output impedance of the opamp (i.e., looking into the drains of $Q_{6}$ and $Q_{8}$ ). Thus, neglecting other parasitic poles, we have

$$
\begin{equation*}
A_{V}=\frac{g_{\mathrm{m} 1} r_{\text {out }}}{1+\mathrm{sr}_{\text {out }} C_{\mathrm{L}}} \tag{6.100}
\end{equation*}
$$

where $r_{\text {out }}$ is the output impedance of the opamp. This impedance is quite high, on the order of $g_{m} r_{d s}^{2} / 2$ or greater if output-impedance enhancement is used.

For mid-band and high frequencies, the load capacitance dominates, and we can ignore the unity term in the denominator and thus have

$$
\begin{equation*}
A_{V} \cong \frac{g_{m 1}}{s C_{L}} \tag{6.101}
\end{equation*}
$$

from which the unity-gain frequency of the opamp is found to be

$$
\begin{equation*}
\omega_{\mathrm{ta}}=\frac{\mathrm{g}_{\mathrm{m} 1}}{\mathrm{C}_{\mathrm{L}}} \tag{6.102}
\end{equation*}
$$

Key Point: If the bandwidth of a foldedcascode opamp is insufficient, one must increase the input transconductance.

With feedback, the loop unity-gain frequency is $\omega_{t}=\beta g_{m 1} / C_{L}$. Therefore, for large load capacitances, the unity-gain frequency is much less than the second- and higherorder poles, and the phase margin, even with $\beta=1$, is close to $90^{\circ}$. Hence, amplifier bandwidth is maximized by maximizing the transconductance of the input transistors, which in turn is maximized by using wide n -channel devices and ensuring that the input transistor pair's bias current is substantially larger than the bias current of the cascode
transistors and current mirror. Note that this approach also maximizes the dc gain (i.e., $\mathrm{g}_{\mathrm{m} 1} \mathrm{r}_{\mathrm{out}}$ ) since not only does it maximize $g_{m 1}$, but it also maximizes $r_{\text {out }}$ since all transistors connected to the output node are biased at lower current levels (for a given total power dissipation). A practical upper limit on the ratio of the bias currents of the input transistors to the currents of the cascode transistors might be around four or so. If too high a ratio is used, the bias currents of the cascode transistors cannot be well established since they are derived by current subtractions. Another advantage of having very large transconductances for the input devices is that the thermal noise due to this input pair is reduced. Thus, since much of the bias current in folded-cascode opamps flows through the input differential pair, these opamps often have a better thermal noise performance than other opamp designs having the same power dissipation.

If the unity-gain frequency (6.102) is high enough, the second- and higher-order poles may become significant. The second poles of this opamp are primarily due to the time constants introduced by the impedance and parasitic capacitances at the sources of the $p$-channel cascode transistors, $Q_{5}$ and $Q_{6}$. The impedances at these nodes is one over the transconductance of the cascode transistors. ${ }^{14}$ Since p -channel transistors are used here, possibly biased at lower currents, these impedance are typically substantially greater than the source impedance of most n -channel transistors in the signal path. As a consequence, when high-frequency operation is important, these impedances can be reduced by making the currents in the p -channel cascode transistors around the same level as the bias currents of the input transistors. The parasitic capacitance at the sources of the cascode transistors is primarily due to the gate-source capacitances of the cascode transistors as well as the drain-to-bulk and drain-togate capacitances of the input transistors and the current-source transistors $Q_{3}$ and $Q_{4}$. Therefore, minimizing junction areas and peripheries at these two nodes is important.

In summary, if the phase margin of a folded-cascode opamp with feedback is insufficient, one has two choices:
a. Add an additional capacitance in parallel with the load to decrease the dominant pole. This improves phase margin without additional power consumption and without effecting the dc gain, but decreases amplifier bandwidth and increases area.
b. Increase the current and device widths in the output stage, $\mathrm{I}_{\mathrm{D} 5}$ and $\mathrm{I}_{\mathrm{D} 6}$. This will increase the second pole frequency and improve phase margin,

Key Point: If the phase margin of a folded-cascode opamp is insufficient, one must either reduce the bandwidth by adding output capacitance, or burn more power in the output transistors to increase the second pole frequency.
but sacrifices dc gain and increases power consumption.
Note that we have already seen in Chapter 4 that an upper limit on the second pole frequency of a cascode gain stage is imposed by the intrinsic speed (unity-gain frequency) of the cascode transistor-in this case $\mathrm{Q}_{5,6}$.

$$
\begin{equation*}
\mathrm{f}_{\mathrm{p} 2}<\frac{3 \mu_{\mathrm{p}} \mathrm{~V}_{\mathrm{eff5}}}{4 \pi \mathrm{~L}_{5}^{2}}=\mathrm{f}_{\mathrm{TS}} \tag{6.103}
\end{equation*}
$$

Hence, option (b) above is ultimately subject to this constraint.
It is also possible to employ lead compensation. When the load is a series combination of a compensation capacitance, $C_{L}$, and a lead resistance, $R_{C}$, the small-signal transfer function is given by

$$
\begin{equation*}
A_{V}=\frac{g_{m 1}}{\frac{1}{r_{\text {out }}}+\frac{1}{R_{C}+1 / s C_{\mathrm{L}}}} \cong \frac{g_{m 1}\left(1+s R_{C} C_{L}\right)}{s C_{\mathrm{L}}} \tag{6.104}
\end{equation*}
$$

where the approximate term is valid at mid and high frequencies. Here we see that, as in Section $6.2, \mathrm{R}_{\mathrm{C}}$ can be chosen to place a zero at 1.7 times the unity-gain frequency.
14. This is true only at high frequencies, where the output impedance of the amplifier is small due to the load and/or compensation capacitance. This is the case of interest here. At low frequencies, the impedance looking into the source of $Q_{6}$ is given by $R_{s 6}=1 / g_{m 6}+R_{L} /\left(g_{m 6} r_{d s 6}\right)$, where $R_{L}$ is the resistance seen looking out the drain of $Q_{6}$.

### 6.4.2 Slew Rate

The diode-connected transistors, $\mathrm{Q}_{12}$ and $\mathrm{Q}_{13}$, are turned off during normal operation and have almost no effect on the opamp. However, they substantially improve the operation during times of slew-rate limiting [Law, 1983]. To appreciate their benefit, consider first what happens during times of slew-rate limiting when they are not present. Assume there is a large differential input voltage that causes $Q_{1}$ to be turned on hard and $Q_{2}$ to be turned off. Since $Q_{2}$ is off, all of the bias current of $Q_{4}$ will be directed through the cascode transistor $Q_{5}$, through the $n$-channel current mirror, and out of the load capacitance. Thus, the output voltage will decrease linearly with a slew-rate given by

$$
\begin{equation*}
\mathrm{SR}=\frac{\mathrm{I}_{\mathrm{D} 4}}{\mathrm{C}_{\mathrm{L}}} \tag{6.105}
\end{equation*}
$$

Also, since all of $I_{\text {bias } 2}$ is being diverted through $Q_{1}$, and since this current is usually designed to be greater than $I_{D 3}$, both $Q_{1}$ and the current source $I_{\text {bias2 }}$ will go into the triode region, causing $I_{\text {bias2 }}$ to decrease until it is equal to $I_{D 3}$. As a result, the drain voltage of $Q_{1}$ approaches that of the negative power-supply voltage. When the opamp is coming out of slew-rate limiting, the drain voltage of $Q_{1}$ must slew back to a voltage close to the positive power supply before the opamp operates in its linear region again. This additional slewing time greatly increases the distortion and also increases the transient times during slew-rate limiting (which occurs often for opamps used in switched-capacitor applications).

Next, consider the case where the diode-connected transistors, $\mathrm{Q}_{12}$ and $\mathrm{Q}_{13}$, are included. Their main purpose is to clamp the drain voltages of $\mathrm{Q}_{1}$ or $\mathrm{Q}_{2}$ so they don't change as much during slew-rate limiting. A second, more subtle effect dynamically increases the bias currents of both $Q_{3}$ and $Q_{4}$ during times of slew-rate limiting. This increased bias current results in a larger maximum current available for charging or discharging the load capacitance. To see this increase in bias current, consider a case similar to the one just described, where a large differential input causes $Q_{1}$ to be fully on while $Q_{2}$ is off. In this case, the diode-connected transistor $Q_{12}$ conducts with the current through $Q_{12}$ coming from the diode-connected transistor $Q_{11}$. Thus, the current in $Q_{11}$ increases, causing the currents in bias transistors $Q_{3}$ and $Q_{4}$ to also increase, until the sum of the currents of $Q_{12}$ and $Q_{3}$ are equal to the bias current $I_{\text {bias2 }}$. Note that the current in $Q_{4}$ also increases since it is equal to the current in $Q_{3}$. This increase in bias current of $Q_{4}$ results in an increase of the maximum current available for discharging $C_{L}$. In summary, not only are the voltage excursions less, but the maximum available current for charging or discharging the load capacitance is also greater during times of slew-rate limiting.

#### EXAMPLE 6.9

Find reasonable transistor sizes for the folded-cascode opamp shown in Fig. 6.20 to satisfy the following design parameters. Also find the opamp's unity-gain frequency (without feedback) and slew rate, both without and with the clamp transistors.

- Assume the process parameters for the $0.18-\mu \mathrm{m}$ process in Table 1.5 , a single $1.8-\mathrm{V}$ power supply, and limit the current dissipation of the opamp to 0.4 mA .
- Set the ratio of the current in the input transistors to that of the cascode transistors to be 4:1. Also, set the bias current of $Q_{11}$ to be 1/10th that of $Q_{3}$ (or $Q_{4}$ ) such that its current can be ignored in the power dissipation calculation.
- The maximum transistor width should be $180 \mu \mathrm{~m}$ and channel lengths of $0.4 \mu \mathrm{~m}$ should be used in all transistors.
- All transistors should have effective gate-source voltages of around 0.24 V except for the input transistors, whose widths should be set to the maximum value of $180 \mu \mathrm{~m}$. Also, round all transistor widths to the closest multiple of $2 \mu \mathrm{~m}$, keeping in mind that if a larger transistor is to be matched to a smaller one, the larger transistor should be built as a parallel combination of smaller transistors.
- Finally, assume the load capacitance is given by $\mathrm{C}_{\mathrm{L}}=2.5 \mathrm{pF}$.

#### Solution

The total current in the opamp, $\mathrm{I}_{\text {total }}$, excluding the current in the bias network, is equal to $\mathrm{I}_{\mathrm{D} 3}+\mathrm{I}_{\mathrm{D} 4}$, which is equal to $2\left(I_{D 1}+I_{D 6}\right)$. Defining $I_{B} \equiv I_{D S}=I_{D 6}$ and noting that we are asked to make $I_{D 1}=4 I_{D 6}$, we have

$$
\begin{equation*}
\mathrm{I}_{\text {total }}=2\left(\mathrm{I}_{\mathrm{D} 1}+\mathrm{I}_{\mathrm{D} 6}\right)=2\left(4 \mathrm{I}_{\mathrm{B}}+\mathrm{I}_{\mathrm{B}}\right)=10 \mathrm{I}_{\mathrm{B}} \tag{6.106}
\end{equation*}
$$

Since the current dissipation is specified to be 0.4 mA , we have

$$
\begin{equation*}
\mathrm{I}_{\mathrm{B}}=\mathrm{I}_{\mathrm{D} 5}=\mathrm{I}_{\mathrm{D} 6}=\frac{\mathrm{I}_{\text {total }}}{10}=40 \mu \mathrm{~A} \tag{6.107}
\end{equation*}
$$

This bias current for $I_{B}$ implies that $I_{D 3}=I_{D 4}=5 I_{D 5}=200 \mu \mathrm{~A}$, and $I_{D 1}=I_{D 2}=4 I_{D 5}=160 \mu \mathrm{~A}$. Now, we let all transistor channel lengths be $0.4 \mu \mathrm{~m}$, about $2 \times$ larger than the minimum gate length in this technology. This choice allows us to immediately determine the sizes of most transistors using

$$
\begin{equation*}
\left(\frac{W}{L}\right)_{i}=\frac{2 I_{D_{i}}}{\mu_{i} C_{o x} V_{e f f i}^{2}} \tag{6.108}
\end{equation*}
$$

0SPICE! Simulate this opamp with the provided netlist.
and then round to the closest multiple of $2 \mu \mathrm{~m}$ in transistor widths. Input transistors $Q_{1}$ and $Q_{2}$ were an exception; their widths are set at the prescribed maximum of $180 \mu \mathrm{~m}$. This puts those devices on the border of subthreshold operation, thereby maximizing their transconductance for the given bias current. Table 6.1 lists reasonable values for the resulting dimensions of all transistors. Note that the larger widths are exactly divisible by the smaller widths of a transistor of the same type and thus allows larger transistors to be realized as a parallel combination of smaller transistors. The width of $Q_{11}$ was determined from the requirement that $I_{D 11}=I_{D 3} / 10=20 \mu \mathrm{~A}=I_{\text {bias, } 1 .}$. The widths of $Q_{12}$ and $Q_{13}$ were somewhat arbitrarily chosen to equal the width of $Q_{11}$.

Under a square-law assumption, the transconductance of the input transistors would be given by

$$
\begin{equation*}
\sqrt{2 \mathrm{I}_{\mathrm{D} 1} \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L})_{1}}=6.24 \mathrm{~mA} / \mathrm{V} \tag{6.109}
\end{equation*}
$$

However, this is greater than the maximum transconductance achieved in subthreshold operation.

$$
\begin{equation*}
g_{\mathrm{m} 1(\text { sub - th })}=\frac{\mathrm{q} \mathrm{l}_{\mathrm{D} 1}}{\mathrm{nkT}}=4 \mathrm{~mA} / \mathrm{V} \tag{6.110}
\end{equation*}
$$

The maximum value computed in (6.110) is assumed as an approximation, although the real transconductance will be less than this upper limit. The unity-gain frequency of the opamp is given by

$$
\begin{equation*}
\omega_{\mathrm{ta}}=\frac{\mathrm{g}_{\mathrm{m} 1}}{\mathrm{C}_{\mathrm{L}}}=1.6 \times 10^{9} \mathrm{rad} / \mathrm{s} \Rightarrow \mathrm{f}_{\mathrm{ta}}=255 \mathrm{MHz} \tag{6.111}
\end{equation*}
$$

Table 6.1 The transistor dimensions (in $\mu \mathrm{m}$ ) of the opamp of Fig. 6.20.

| $\mathrm{Q}_{1}$ | $180 / 0.4$ | $\mathrm{Q}_{6}$ | $8 / 0.4$ | $\mathrm{Q}_{11}$ | $4 / 0.4$ |
| ---: | ---: | :--- | ---: | :--- | :--- |
| $\mathrm{Q}_{2}$ | $180 / 0.4$ | $\mathrm{Q}_{7}$ | $2 / 0.4$ | $\mathrm{Q}_{12}$ | $4 / 0.4$ |
| $\mathrm{Q}_{3}$ | $40 / 0.4$ | $\mathrm{Q}_{8}$ | $2 / 0.4$ | $\mathrm{Q}_{13}$ | $4 / 0.4$ |
| $\mathrm{Q}_{4}$ | $40 / 0.4$ | $\mathrm{Q}_{9}$ | $2 / 0.4$ |  |  |
| $\mathrm{Q}_{5}$ | $8 / 0.4$ | $\mathrm{Q}_{10}$ | $2 / 0.4$ |  |  |

The slew rate without the clamp transistors is given by

$$
\begin{equation*}
\mathrm{SR}=\frac{\mathrm{I}_{\mathrm{D} 4}}{\mathrm{C}_{\mathrm{L}}}=80 \mathrm{~V} / \mu \mathrm{s} \tag{6.112}
\end{equation*}
$$

When the clamp transistors are included, during slew-rate limiting, we have

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D} 12}+\mathrm{I}_{\mathrm{D} 3}=\mathrm{I}_{\mathrm{bias} 2} \tag{6.113}
\end{equation*}
$$

But

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D} 3}=10 \mathrm{I}_{\mathrm{D} 11} \tag{6.114}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D} 11}=20 \mu \mathrm{~A}+\mathrm{I}_{\mathrm{D} 12} \tag{6.115}
\end{equation*}
$$

Substituting (6.114) and (6.115) into (6.113) and solving for $I_{D 11}$ gives

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D} 11}=\frac{\mathrm{I}_{\mathrm{bias} 2}+20 \mu \mathrm{~A}}{11} \tag{6.116}
\end{equation*}
$$

which implies that the value of $\mathrm{I}_{\mathrm{D} 11}$ during slew-rate limiting is $30.9 \mu \mathrm{~A}$ and $\mathrm{I}_{\mathrm{D} 3}=\mathrm{I}_{\mathrm{D} 4}=10 \mathrm{I}_{\mathrm{D} 11}=0.309 \mathrm{~mA}$, which is substantially larger than the slew current available without the clamp transistors. This larger bias current will give a slew-rate value of

$$
\begin{equation*}
\mathrm{SR}=\frac{\mathrm{I}_{\mathrm{D} 4}}{\mathrm{C}_{\mathrm{L}}}=124 \mathrm{~V} / \mu \mathrm{s} \tag{6.117}
\end{equation*}
$$

More importantly, the time it takes to recover from slew-rate limiting will be substantially decreased.

#### EXAMPLE 6.10

The opamp in Example 6.9 is simulated and found to have an equivalent second pole frequency at $\omega_{\text {eq }}=2 \pi \cdot 365 \mathrm{MHz}$. Select a value for the lead compensation resistor, $\mathrm{R}_{\mathrm{C}}$, to provide a phase margin of $85^{\circ}$ when the opamp is used in a unity-gain configuration.

#### Solution

The phase margin without $R_{C}$ is given by

$$
\text { Phase Margin }=90^{\circ}-\tan ^{-1}\left(\frac{\omega_{\mathrm{t}}}{\omega_{\mathrm{eq}}}\right)=90^{\circ}-\tan ^{-1}\left(\frac{2 \pi \cdot 255 \mathrm{MHz}}{2 \pi \cdot 365 \mathrm{MHz}}\right)=55^{\circ}
$$

In order to increase this by $30^{\circ}=\tan ^{-1}(1 / 1.7)$, the lead compensation zero must be placed at $1 / R_{C} C_{L}=1.7 \omega_{t}$. Since $\beta=1$, we have $\omega_{t}=\omega_{t a}$. Hence, a reasonable size for $R_{C}$ in series with $C_{L}$ is given by

$$
\begin{equation*}
\mathrm{R}_{\mathrm{C}}=\frac{1}{1.7 \mathrm{C}_{\mathrm{L}} \omega_{\mathrm{t}}}=\frac{1}{1.7 \mathrm{~g}_{\mathrm{m} 1}}=147 \Omega \tag{6.118}
\end{equation*}
$$

## 6.5 CURRENT MIRROR OPAMP

Another popular opamp often used when driving on-chip capacitive-only loads is the current mirror opamp shown in simplified form in Fig. 6.21. It is immediately seen that all nodes are low impedance except for the output node. By using good current mirrors having high output impedance, a reasonable overall gain can be achieved. A more detailed example of a current mirror opamp is shown in Fig. 6.22.

The overall transfer function of this opamp will closely approximate dominant-pole operation. In a similar analysis to that given for the folded-cascode opamp, we have
image_name:Fig. 6.21 A simplified current-mirror opamp.
description:The circuit is a simplified current-mirror operational amplifier. It uses wide-swing cascode current mirrors to achieve high output impedance, improving the overall gain. The transfer function approximates dominant-pole operation, and the opamp is designed to enhance performance in analog signal processing.

Fig. 6.21 A simplified current-mirror opamp.
image_name:Fig. 6.22
description:The circuit is a current-mirror operational amplifier with wide-swing cascode current mirrors. It is designed to achieve high output impedance and improve overall gain. The amplifier's transfer function approximates dominant-pole operation, enhancing performance in analog signal processing. The current gain ratio W5:W8 is 1:K, and ID14 = KID1 = KIb/2.

Fig. 6.22 A current-mirror opamp with wide-swing cascode current mirrors.

$$
\begin{equation*}
A_{V}=\frac{V_{\text {out }}(s)}{V_{\text {in }}(s)}=K g_{m 1} Z_{L}(s)=\frac{K g_{m 1} r_{\text {out }}}{1+s r_{\text {out }} C_{\mathrm{L}}} \cong \frac{K_{\mathrm{m} 1}}{s C_{\mathrm{L}}} \tag{6.119}
\end{equation*}
$$

The K factor is the current gain from the input transistors to the output sides of the current mirrors connected to the output node. Hence, the amplifier's overall transconductance is $\mathrm{G}_{\mathrm{ma}}=\mathrm{Kg}_{\mathrm{m} 1}$. Using (6.119), we can solve for the opamp's unity-gain frequency (without feedback), resulting in

$$
\begin{equation*}
\omega_{\mathrm{ta}}=\frac{\mathrm{Kg}_{\mathrm{m} 1}}{\mathrm{C}_{\mathrm{L}}}=\frac{2 \mathrm{KI}_{\mathrm{D} 1}}{\mathrm{C}_{\mathrm{L}} \mathrm{~V}_{\mathrm{eff}, 1}} \tag{6.120}
\end{equation*}
$$

If the power dissipation is specified, the total current,

$$
\begin{equation*}
\mathrm{I}_{\text {total }}=(3+\mathrm{K}) \mathrm{I}_{\mathrm{D} 1} \tag{6.121}
\end{equation*}
$$

is known for a given power-supply voltage. Substituting (6.121) into (6.120), we obtain

$$
\begin{equation*}
\omega_{\mathrm{ta}}=\frac{\mathrm{K}}{(3+\mathrm{K})} \frac{2 \mathrm{I}_{\mathrm{total}}}{\mathrm{~V}_{\mathrm{eff}, 1} \mathrm{C}_{\mathrm{L}}} \tag{6.122}
\end{equation*}
$$

Equations (6.120) and (6.122) assume a square law for input transistors $\mathrm{Q}_{1,2}$ and emphasize the desire to bias the input pair with low values of $\mathrm{V}_{\text {eff }}$. If they are biased with very low $\mathrm{V}_{\text {eff }}$, their transconductance approaches the upper limit obtained in subthreshold operation, $\mathrm{g}_{\mathrm{m} 1 \text { (sub -th })} \cong \mathrm{ql}_{\mathrm{D} 1} / \mathrm{nkT}$ in which case

$$
\begin{equation*}
\omega_{\mathrm{ta}}=\frac{\mathrm{Kq}\left(\frac{\mathrm{I}_{\text {total }}}{3+\mathrm{K}}\right)}{n k T C_{\mathrm{L}}}=\frac{\mathrm{K}}{(3+\mathrm{K})} \frac{\mathrm{qI}_{\text {total }}}{n \mathrm{kTC}} \tag{6.123}
\end{equation*}
$$

Regardless, the opamp's transconductance (i.e., $\mathrm{Kg}_{\mathrm{m}_{1}}$ ) increases with increasing K , and therefore the unity-gain frequency is also larger. This simple result assumes the unity-gain frequency is limited by the load capacitance rather than any high-frequency poles caused by the time constants of the internal nodes. A practical upper limit on K might be around five. The use of large K values also maximizes the gain for $\mathrm{I}_{\text {total }}$ fixed since $\mathrm{r}_{\text {out }}$ is roughly independent of K for large K .

In the circuit shown in Fig. 6.22, the important nodes for determining the non-dominant poles are the drain of $Q_{1}$, primarily, and the drains of $Q_{2}$ and $Q_{9}$, secondly. Increasing $K$ increases the capacitances of these nodes while also increasing the equivalent resistances. ${ }^{15}$ As a result, the equivalent second pole moves to lower frequencies. If K is increased too much, the second pole frequency will approach $\omega_{\mathrm{ta}}$, and an increase in $C_{\mathrm{L}}$ will be required to decrease $\omega_{\mathrm{ta}}$ and maintain stability, unless $\beta$ is very small. Thus, increasing K decreases the bandwidth when the equivalent second pole dominates. This is most likely to occur when the load capacitance is small. If it is very important that speed is maximized, K might be taken as small as one. A reasonable compromise for a general-purpose opamp might be $\mathrm{K}=2$.

The slew rate of the current-mirror opamp is found by assuming there is a very large input voltage. In this case, all of the bias current of the first stage will be diverted through either $Q_{1}$ or $Q_{2}$. This current will be amplified by the current gain from the input stage to the output stage, (i.e., K). Thus, during slew-rate limiting, the total current available to charge or discharge $C_{L}$ is $\mathrm{KI}_{\mathrm{b}}$. The slew rate is therefore given by

$$
\begin{equation*}
\mathrm{SR}=\frac{\mathrm{KI}}{\mathrm{C}_{\mathrm{L}}} \tag{6.124}
\end{equation*}
$$

15. Increasing K implies that the currents at the input sides of the current mirrors are smaller, for a given total power dissipation. Also, the widths of transistors at the input sides of current mirrors will be smaller. Both of these effects cause the transconductances of transistors at the input side of current mirrors to be smaller, and therefore the impedances (in this case, $1 / \mathrm{g}_{\mathrm{m}}$ ) will be larger.

For a given total power dissipation, this slew rate is maximized by choosing a large K value. For example, with $\mathrm{K}=4$ and during slewrate limiting, $4 / 5$ of the total bias current of the opamp will be available for charging or discharging $C_{L}$. This result gives a current-mirror opamp superior slew rates when compared to a folded-cascode opamp, even when the clamp transistors have been included in the folded-cascode opamp. Also, there are no problems with large voltage transients during slew-rate limiting for the current-mirror opamp.

In summary, due primarily to the larger bandwidth and slew rate, the current-mirror opamp is often preferred over a folded-cascode opamp.

Key Point: For a current-mirror opamp, when the load capacitance is large and the output pole clearly dominant, a large current mirror ratio, $K$, maximizes gain and bandwidth. If the second pole frequency becomes significant, lower values of $K$ are required to keep the second pole frequency above the unity-gain frequency and maintain a healthy phase margin.

However, it will suffer from larger thermal noise when compared to a folded-cascode amplifier because its input transistors are biased at a lower proportion of the total bias current and therefore have a smaller transconductance. As seen in the chapter on noise, a smaller transconductance results in larger thermal noise when the noise is referred back to the input of the opamp.

### EXAMPLE 6.11

Assume the current-mirror opamp shown in Fig. 6.22 has all transistor lengths equal to $0.4 \mu \mathrm{~m}$ and transistor widths as given in Table 6.2. Notice that $\mathrm{K}=2$. Assume the process parameters for the $0.18-\mu \mathrm{m}$ process in Table 1.5 , a single $1.8-\mathrm{V}$ power supply, and that the opamp's total current dissipation is 0.4 mA . The load capacitance is

|  | SPICE! Simulate this opamp with the provided netlist. |
| :---: | :---: |

$\mathrm{C}_{\mathrm{L}}=2.5 \mathrm{pF}$.

Find the slew rate and the unity-gain frequency, assuming the equivalent second pole does not dominate. Estimate the equivalent second pole. Would it be necessary to increase $C_{\llcorner }$if a $75^{\circ}$ phase margin were required with $\beta=1$ and without using lead compensation? What if lead compensation were used?

### Solution

Since the total bias current is given by $(3+K) I_{b} / 2$, we have

$$
\begin{equation*}
I_{b}=\frac{2 I_{\text {total }}}{(3+K)}=\frac{2(0.4 \mathrm{~mA})}{(3+\mathrm{K})}=160 \mu \mathrm{~A} \tag{6.125}
\end{equation*}
$$

Thus, the bias currents of all transistors, except those in the output stage, are $80 \mu \mathrm{~A}$. The bias currents of transistors in the output stage are twice that of the input stage, which is $160 \mu \mathrm{~A}$. The effective gate-source voltage of the input transistors may be shown to be less than 100 mV , so their transconductance is near the limit obtained in subthreshold.

$$
\begin{equation*}
g_{\mathrm{m} 1(\text { sub-th })}=\frac{q l_{D 1}}{n k T}=2 \mathrm{~mA} / \mathrm{V} \tag{6.126}
\end{equation*}
$$

Table 6.2 The transistor sizes (in $\mu \mathrm{m}$ ) for the opamp used in Example 6.11.

| $\mathrm{Q}_{1}$ | $90 / 0.4$ | $\mathrm{Q}_{7}$ | $20 / 0.4$ | $\mathrm{Q}_{13}$ | $4 / 0.4$ |
| :--- | :--- | :--- | ---: | :--- | :--- |
| $\mathrm{Q}_{2}$ | $90 / 0.4$ | $\mathrm{Q}_{8}$ | $40 / 0.4$ | $\mathrm{Q}_{14}$ | $8 / 0.4$ |
| $\mathrm{Q}_{3}$ | $20 / 0.4$ | $\mathrm{Q}_{9}$ | $20 / 0.4$ |  |  |
| $\mathrm{Q}_{4}$ | $20 / 0.4$ | $\mathrm{Q}_{10}$ | $40 / 0.4$ |  |  |
| $\mathrm{Q}_{5}$ | $20 / 0.4$ | $\mathrm{Q}_{11}$ | $4 / 0.4$ |  |  |
| $\mathrm{Q}_{6}$ | $20 / 0.4$ | $\mathrm{Q}_{12}$ | $8 / 0.4$ |  |  |

The transconductance of the opamp will be K times this or $4 \mathrm{~mA} / \mathrm{V}$. The opamp unity-gain frequency is now given by

$$
\begin{equation*}
\omega_{\mathrm{ta}}=\frac{\mathrm{Kg}_{\mathrm{m} 1}}{\mathrm{C}_{\mathrm{L}}}=1.6 \times 10^{9} \mathrm{rad} / \mathrm{s} \Rightarrow \mathrm{f}_{\mathrm{ta}}=255 \mathrm{MHz} \tag{6.127}
\end{equation*}
$$

This is the same result obtained for the folded-cascode opamp of the previous example with the same current consumption and load capacitance. If a higher value of K were chosen, the current-mirror opamp would provide superior bandwidth.

Continuing, the slew rate is given by

$$
\begin{equation*}
\mathrm{SR}=\frac{\mathrm{KI}_{\mathrm{b}}}{\mathrm{C}_{\mathrm{L}}}=128 \mathrm{~V} / \mu \mathrm{s} \tag{6.128}
\end{equation*}
$$

which compares favorably to $80 \mathrm{~V} / \mu$ s for the folded-cascode opamp without the clamp transistors and slightly higher than the folded-cascode opamp with the clamp transistors.

When estimating the equivalent second pole, the junction capacitances will be ignored to simplify matters. In reality, the drain-to-bulk capacitances of the input transistors could contribute a significant factor, and this amount can be determined using simulation. The dominant node almost certainly will occur at the drain of $Q_{1}$. The impedance at this node is given by

$$
\begin{equation*}
\mathrm{R}_{1}=1 / \mathrm{g}_{\mathrm{m} 5}=1.3 \mathrm{k} \Omega \tag{6.129}
\end{equation*}
$$

In addition, the capacitance will be primarily due to the gate-source capacitances of $Q_{5}$ and $Q_{8}$. We therefore have

$$
\begin{equation*}
C_{1}=C_{g s 5}+C_{g s 8}=(1+K) C_{g s 5} \tag{6.130}
\end{equation*}
$$

resulting in

$$
\begin{equation*}
\mathrm{C}_{1}=(1+\mathrm{K})(2 / 3) \mathrm{C}_{\mathrm{ox}} \mathrm{~W}_{5} \mathrm{~L}_{5}=0.14 \mathrm{pF} \tag{6.131}
\end{equation*}
$$

With these values of impedance, the time constant for this node is given by

$$
\begin{equation*}
\tau_{1}=\mathrm{R}_{1} \mathrm{C}_{1}=0.18 \mathrm{~ns} \tag{6.132}
\end{equation*}
$$

In a similar manner, we can calculate the impedances and, hence, the time constant for the drain of $Q_{2}$ to be $\mathrm{R}_{2}=1.3 \mathrm{k} \Omega, \mathrm{C}_{2}=0.091 \mathrm{pF}$, and $\tau_{2}=\mathrm{R}_{2} \mathrm{C}_{2}=0.12 \mathrm{~ns}$. The other important time constant comes from the parasitic capacitors at the drain of $Q_{9}$. Here, we have

$$
\begin{equation*}
\mathrm{R}_{3}=1 / \mathrm{g}_{\mathrm{m} 13}=1.5 \mathrm{k} \Omega \tag{6.133}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{C}_{3}=\mathrm{C}_{\mathrm{gs} 13}+\mathrm{C}_{\mathrm{gs} 14}=(1+\mathrm{K})(2 / 3) \mathrm{C}_{\mathrm{ox}} \mathrm{~W}_{13} \mathrm{~L}_{13}=0.027 \mathrm{pF} \tag{6.134}
\end{equation*}
$$

resulting in $\tau_{3}=0.04 \mathrm{~ns}$. The time constant of the equivalent second pole can now be estimated to be given by

$$
\begin{equation*}
\tau_{2 \mathrm{eq}}=\tau_{1}+\tau_{2}+\tau_{3}=0.34 \mathrm{~ns} \tag{6.135}
\end{equation*}
$$

This result gives an equivalent second pole at the approximate frequency of

$$
\begin{equation*}
\mathrm{p}_{2 \mathrm{eq}}=\frac{1}{\tau_{2 \mathrm{eq}}}=2.94 \times 10^{9} \mathrm{rad} / \mathrm{s}=2 \pi \times 468 \mathrm{MHz} \tag{6.136}
\end{equation*}
$$

If lead compensation is not used and a $75^{\circ}$ phase margin is required, the unity-gain frequency must be constrained to be less than 0.27 times the equivalent second pole from Table 5.1 of Chapter 5. Specifically, the unity-gain
frequency must be less than 126 MHz . To achieve this unity-gain frequency, we need to increase $\mathrm{C}_{\mathrm{L}}$ by the factor $255 \mathrm{MHz} /(126 \mathrm{MHz})$, resulting in $\mathrm{C}_{\mathrm{L}}$ being 5 pF .

If lead compensation is to be used, the unity-gain frequency can be chosen so that only a $55^{\circ}$ phase margin is achieved before the lead resistor is added. This approach would allow the unity-gain frequency to be as high as 0.7 times the equivalent second-pole frequency, which is greater than the value computed in (6.127). The benefits of lead compensation are obvious: the unity-gain frequency is increased by $150 \%$ and no compensation capacitor is required, reducing the physical area of the circuit.

As a final comment, notice that the delay through the signal path from the drain of $Q_{2}$ to the output (i.e., $\tau_{2}+\tau_{3}=0.16 \mathrm{~ns}$ ) is approximately the same as the delay through the signal path from the drain of $\mathrm{Q}_{1}$ to the output, which is $\tau_{1}=0.18 \mathrm{~ns}$. This near equivalence helps to minimize harmful effects caused by the pole-zero doublet introduced at high frequencies (i.e. around the frequency of the second pole) by the existence of two signal paths.

## 6.6 LINEAR SETTLING TIME REVISITED

We saw in Chapter 5 that the time constant for linear settling time was equal to the inverse of $\omega_{-3} \mathrm{~dB}$ for the closedloop circuit gain. We also saw that $\omega_{-3}$ dB is given by the relationship

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}}=\omega_{t} \tag{6.137}
\end{equation*}
$$

However, while for the classical two-stage CMOS opamp the unity-gain frequency remains relatively constant for varying load capacitances, the unity-gain frequencies of the folded-cascode and current-mirror amplifiers are strongly related to their load capacitance. As a result, their settling-time performance is affected by both the feedback factor as well as the effective load capacitance.

For the folded-cascode opamp, its unity-gain frequency is given by

$$
\begin{equation*}
\omega_{\mathrm{ta}}=\frac{\mathrm{g}_{\mathrm{m} 1}}{\mathrm{C}_{\mathrm{L}}} \tag{6.138}
\end{equation*}
$$

whereas for a current-mirror opamp, it is equal to

$$
\begin{equation*}
\omega_{\mathrm{ta}}=\frac{\mathrm{Kg}_{\mathrm{m} 1}}{\mathrm{C}_{\mathrm{L}}} \tag{6.139}
\end{equation*}
$$

Thus we see that for both these high-output impedance opamps, their unity-gain frequency is inversely proportional to the load capacitance. To determine the $-3-\mathrm{dB}$ frequency of a closed-loop opamp, consider the general case shown in Fig. 6.23. At the opamp output, $\mathrm{C}_{\text {load }}$ represents the capacitance of the next stage that the opamp
image_name:Fig. 6.23
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: InN(A1)}
name: Cp, type: Capacitor, value: Cp, ports: {Np: InN(A1), Nn: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Vout}
name: C2, type: Capacitor, value: C2, ports: {Np: Vout, Nn: InN(A1)}
name: Cc, type: Capacitor, value: Cc, ports: {Np: Vout, Nn: GND}
name: C_load, type: Capacitor, value: C_load, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a closed-loop amplifier with feedback for determining the -3 dB frequency. The op-amp is configured with a feedback capacitor C2, and compensation capacitor Cc is used to maintain phase margin. The load capacitance is represented by Cload, and parasitic capacitance at the input is represented by Cp.

Fig. 6.23 A general circuit for determining the $-3-d B$ frequency of a closed-loop amplifier.
must drive, while $\mathrm{C}_{\mathrm{C}}$ is a compensation capacitance that might be added to maintain a sufficient phase margin. At the input side, $\mathrm{C}_{\mathrm{p}}$ represents parasitic capacitance due to large transistors at the opamp input as well as any switch capacitance.

Defining $\omega_{\mathrm{t}}=\beta \omega_{\mathrm{ta}}$, the feedback network is due to capacitances $\mathrm{C}_{1}, \mathrm{C}_{2}$, and $\mathrm{C}_{\mathrm{p}}$ resulting in

$$
\begin{equation*}
\beta=\frac{1 /\left[s\left(C_{1}+C_{p}\right)\right]}{1 /\left[s\left(C_{1}+C_{p}\right)\right]+1 /\left(s C_{2}\right)}=\frac{C_{2}}{C_{1}+C_{p}+C_{2}} \tag{6.140}
\end{equation*}
$$

To determine the unity-gain frequency it is necessary to consider the circuit's open-loop operation. Specifically, treating the negative opamp input as an open circuit, the effective load capacitance, $\mathrm{C}_{\mathrm{L}}$, is seen to be given by the parallel combination of $\mathrm{C}_{\mathrm{C}}$ and $\mathrm{C}_{\text {load }}$, as well as that seen looking into $\mathrm{C}_{2}$. The capacitance seen looking into $C_{2}$ is equal to the series combination of $C_{2}$ together with $C_{1}+C_{p}$. Combining all these capacitances together, we have

$$
\begin{equation*}
C_{\mathrm{L}}=\mathrm{C}_{\mathrm{C}}+\mathrm{C}_{\text {load }}+\frac{\mathrm{C}_{2}\left(\mathrm{C}_{1}+\mathrm{C}_{\mathrm{p}}\right)}{\mathrm{C}_{1}+\mathrm{C}_{\mathrm{p}}+\mathrm{C}_{2}} \tag{6.141}
\end{equation*}
$$

#### EXAMPLE 6.12

Consider the current-mirror opamp with no lead compensation in Example 6.11 being used in the circuit shown in Fig. 6.23 with $C_{1}=C_{2}=C_{C}=C_{\text {load }}=5 \mathrm{pF}$. What is the linear settling time required for 0.1 percent accuracy with?

#### Solution

First, the gate-source capacitances of the input devices of the current-mirror opamp can be calculated to be

$$
\begin{equation*}
\mathrm{C}_{\mathrm{gs} 1}=(2 / 3) \times 90 \times 0.4 \times 8.5 \mathrm{fF} / \mu \mathrm{m}^{2}=0.21 \mathrm{pF} \tag{6.142}
\end{equation*}
$$

The capacitance seen looking into the inverting input of the opamp is one-half this value since the gate-source capacitances of the two input devices are in series. Thus, the parasitic capacitance, $C_{P}$, is 0.11 pF . Therefore, the effective load capacitance is given by

$$
\begin{equation*}
C_{\mathrm{L}}=5+5+\frac{5(5+0.11)}{5+5+0.11}=12.53 \mathrm{pF} \tag{6.143}
\end{equation*}
$$

which results in

$$
\begin{equation*}
\omega_{\mathrm{ta}}=\frac{\mathrm{Kg}_{\mathrm{m} 1}}{\mathrm{C}_{\mathrm{L}}}=\frac{2 \times 2 \mathrm{~mA} / \mathrm{V}}{12.53 \mathrm{pF}}=3.19 \times 10^{8} \mathrm{rad} / \mathrm{s} \tag{6.144}
\end{equation*}
$$

or equivalently,

$$
\begin{equation*}
\mathrm{f}_{\mathrm{ta}}=50.8 \mathrm{MHz} \tag{6.145}
\end{equation*}
$$

Now, the feedback factor, $\beta$, is seen to be

$$
\begin{equation*}
\beta=\frac{5}{5+0.11+5}=0.49 \tag{6.146}
\end{equation*}
$$

resulting in

$$
\begin{equation*}
\tau=\frac{1}{\beta \omega_{\mathrm{ta}}}=6.4 \mathrm{~ns} \tag{6.147}
\end{equation*}
$$

Finally, for 0.1 percent accuracy, we need a linear settling time of $7 \tau$ or 45 ns .

## 6.7 FULLY DIFFERENTIAL OPAMPS

There is often little difference between the circuits required to process singleended and fully differential signals. In particular, Fig. 6.24 compares fully differential pair circuit its single-ended output counterpart. The only difference them is that a current mirror load is replaced by two matched current sources in the fully differential circuit. Notice that the power dissipated in these two circuits is the same. Since the voltage swing on any individual node in a circuit is usually limited by fixed supply and bias voltages, fully differential circuits have twice the available signal swing of their single-ended counterparts because they make full

Key Point: Fully differential amplifiers generally have similar power consumption, but twice the available signal swing of their single-ended counterparts. They can also exhibit similar small signal gain and bandwidth.
use of the swing available at two circuit nodes instead of just one. Also, note that $\qquad$ the single-ended circuit has a slew rate equal to the total available bias current over the load capacitance, $\mathrm{I} / \mathrm{C}_{\mathrm{L}}$, whereas in the fully differential circuit each side has $\mathrm{I} / 2$ available when slew rate limited and so the slew rate of the differential voltage $\mathrm{v}_{\mathrm{o}}$ is also $\mathrm{I} / 2 \mathrm{C}_{\mathrm{L}}-\left(-\mathrm{I} / 2 \mathrm{C}_{\mathrm{L}}\right)=\mathrm{I} / \mathrm{C}_{\mathrm{L}}$. Although Fig. 6.24 illustrates these points for an actively-loaded differential pair, they are also true for more complex amplifiers, such as the folded cascode opamp.

The small signal performance of a fully differential amplifier is in many way equivalent to that of a singleended amplifier with similar power consumption. Fig. 6.25 illustrates the point for single-stage amplifiers. Assuming that the circuit's input stage is in both cases a differential pair under the same dc bias, and each half of the fully differential output has an output and load impedance similar to that of the single-ended output, the circuits have similar small-signal gain and bandwidth.

One of the major driving forces behind the use of fully differential signals is to help reject common mode noise. Fig. 6.26 illustrates the impact of additive noise on fully differential signals. Common mode noise, $\mathrm{n}_{\mathrm{cm}}$, appears identically on both half-signals, and is therefore cancelled when only the difference between them is considered (for example, when the noisy signal $\mathrm{v}_{\mathrm{o}}{ }^{\prime}$ serves as the differential input to a circuit with good common-mode rejection). In many analog integrated circuits, the largest noise sources are due to fluctuations in supply and bias voltages and from pass-transistor switches turning off in switched-capacitor applications. These appear as common mode noise and are
image_name:(a)
description:The circuit is a simple actively loaded differential pair with a single-ended output. The power consumption is given by IVDD, the voltage swing is Vpp,max, and the slew rate is 1/CL.
image_name:(b)
description:The circuit is a fully differential actively loaded differential pair. It uses NMOS transistors M1 and M2 with a current source I and a load capacitor CL. The power supply is VDD, and there is a current-controlled current source d1. The circuit provides a fully differential output with improved swing and common-mode rejection.

Fig. 6.24 A comparison of simple actively loaded differential pairs: (a) single-ended output; (b) fully differential.
image_name:Fig. 6.24 (a)
description:
[
name: G_ma*Vi, type: VoltageControlledCurrentSource, value: G_ma*Vi, ports: {Np: GND, Nn: Vo}
name: r_out, type: Resistor, value: r_out, ports: {N1: Vo, N2: GND}
name: C_L, type: Capacitor, value: C_L, ports: {Np: Vo, Nn: GND}
]
extrainfo:The circuit is a simple single-ended output stage with a voltage-controlled current source G_ma, a resistor r_out, and a capacitor C_L. The output is taken from the node Vo. The circuit is grounded at multiple points.

dc gain: $G_{m a} r_{\text {out }}$

$$
\begin{aligned}
\omega_{-3 \mathrm{~dB}} & =1 /\left(\mathrm{r}_{\mathrm{out}} \mathrm{C}_{\mathrm{L}}\right) \\
\omega_{\mathrm{ta}} & =\mathrm{G}_{\mathrm{ma}} / \mathrm{C}_{\mathrm{L}}
\end{aligned}
$$

image_name:(b)
description:
[
name: Gmavi/2, type: VoltageControlledCurrentSource, ports: {Np: V1, Nn: V2}
name: r_out, type: Resistor, value: r_out, ports: {N1: V2, N2: GND}
name: r_out, type: Resistor, value: r_out, ports: {N1: V1, N2: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: V2, Nn: Vo}
name: CL, type: Capacitor, value: CL, ports: {Np: V1, Nn: GND}
]
extrainfo:The circuit is a fully differential small-signal amplifier. It consists of a voltage-controlled current source Gmavi/2, two resistors r_out, and two capacitors CL. The output is taken from node Vo. The circuit is grounded at multiple points, providing stability and reference.

dc gain: $\frac{G_{\text {ma }}}{2} 2 r_{\text {out }}=G_{\text {ma }} r_{\text {out }}$

$$
\begin{gathered}
\omega_{-3 \mathrm{~dB}}=1 /\left(\mathrm{r}_{\mathrm{out}} \mathrm{C}_{\mathrm{L}}\right) \\
\omega_{\mathrm{ta}}=\mathrm{G}_{\mathrm{ma}} / \mathrm{C}_{\mathrm{L}}
\end{gathered}
$$

(b)

Fig. 6.25 Equivalent (a) single-ended and (b) fully differential small-signal amplifiers.

Fig. 6.26 The impact of additive noise on fully differential signals.
image_name:Fig. 6.26
description:The block diagram in Fig. 6.26 illustrates the impact of additive noise on fully differential signals. It consists of three main summing nodes arranged in a configuration that emphasizes the differential nature of the system.

1. **Main Components:**
- **Summing Nodes:** There are three summing nodes in the diagram. These nodes are responsible for adding or subtracting signals as they pass through the system.
- **Inputs and Outputs:** The diagram has two main inputs labeled \( v_o \) and \( v_o' \), and corresponding outputs on the opposite side.
- **Noise Sources:** There are two noise sources labeled \( n_{i1} \) and \( n_{i2} \), which are injected into the system at different points.
- **Common Mode Noise:** A common mode noise \( n_{cm} \) is also depicted, affecting the path between the two main signal lines.

2. **Flow of Information or Control:**
- The signal \( v_o \) enters through the leftmost summing node, where it is combined with the common mode noise \( n_{cm} \). This summed signal then flows to the next summing node on the top right, where the noise \( n_{i1} \) is added.
- Simultaneously, the signal \( v_o' \) is processed in a similar manner through the bottom summing node, where noise \( n_{i2} \) is added. The common mode noise \( n_{cm} \) affects this path as well.
- The outputs are taken from the rightmost side, showing the result of the differential processing.

3. **Labels, Annotations, and Key Indicators:**
- The labels \( v_o \), \( v_o' \), \( n_{i1} \), \( n_{i2} \), and \( n_{cm} \) are critical for understanding the role of each component and the nature of the signals and noise in the system.

4. **Overall System Function:**
- The primary function of this system is to demonstrate how a fully differential signal processing path can handle and potentially reject common mode and other additive noise. The differential configuration helps in minimizing the impact of common mode noise \( n_{cm} \), as well as other noise sources \( n_{i1} \) and \( n_{i2} \), thereby enhancing the integrity of the differential signal outputs.

therefore rejected by fully differential circuits. In reality, this rejection only partially occurs since, unfortunately, the mechanisms introducing the noise are usually nonlinear with respect to voltage levels. For example, substrate noise will usually feed in through junction capacitances, which are nonlinear with voltage. Also, the clock feedthrough noise introduced by switches turning off usually has some voltage-dependent nonlinearities that can cause more noise to feed into one path than the other, thereby injecting a differential noise. However, almost certainly, the noise rejection of a fully differential design will be much better than that of a single-ended output design.

Key Point: A significant advantage of fully differential amplifiers is that common mode noise is rejected. Although random noise power may be 2-times greater than in a similar single-ended circuit, the increased signal swing available in fully differential circuits generally affords them a higher maximum signal-to-noise ratio.

There are also significant random noise sources which appear completely uncorrelated in each of the two half-signals: $n_{i 1}$ and $n_{i 2}$ in Fig. 6.26. ${ }^{16}$ Under the practical assumption that $n_{i 1}$ and $n_{i 2}$ have the same variance, $\mathrm{N}_{0}^{2}$, the noise variance observed at the differential output is the sum of the variances of the two noise contributors, hence $2 \mathrm{~N}_{\mathrm{o}}^{2}$. This increased random noise may at first appear to be a drawback of fully differential signals. However, since the available voltage swing in fully differential circuits is 2 -times greater than in single-ended circuits, the maximum signal power is increased by $2^{2}=4$-times, resulting in a net $3-\mathrm{dB}$ increase in the maximum achievable signal-to-noise ratio.
Fully differential circuits have the additional benefit that if each single-ended signal is distorted symmetrically around the common-mode voltage, the differential signal will have only odd-order distortion terms (which are often much smaller). To see this distortion improvement, consider the block diagram shown in Fig. 6.27, where the two nonlinear elements are identical and, for simplicity, the common-mode voltage is assumed to be
image_name:Fig. 6.27
description:The system block diagram depicted in Fig. 6.27 illustrates a fully differential circuit designed to demonstrate the cancellation of even-order distortion terms when the distortion is symmetrical around the common-mode voltage, which is assumed to be zero in this case.

Main Components:
1. **Nonlinear Elements:** There are two identical nonlinear elements in the system. These elements process input signals with a non-linear response, modeled by a Taylor series expansion.
- The top nonlinear element receives an input signal $v_1$.
- The bottom nonlinear element receives the inverse of the input signal, $-v_1$.

2. **Differential Summing Node:** This component combines the outputs of the two nonlinear elements. It calculates the difference between the two outputs, effectively performing a subtraction.

Flow of Information or Control:
- **Input Signals:** The input $v_1$ is fed into the top nonlinear element, while its inverse $-v_1$ is fed into the bottom nonlinear element.
- **Nonlinear Processing:** Each nonlinear element processes its input according to the Taylor series expansion:
- For the top element, the output $v_{p1}$ is given by: \( v_{p1} = k_1 v_1 + k_2 v_1^2 + k_3 v_1^3 + k_4 v_1^4 + \cdots \)
- For the bottom element, the output $v_{n1}$ is given by: \( v_{n1} = -k_1 v_1 + k_2 v_1^2 - k_3 v_1^3 + k_4 v_1^4 + \cdots \)
- **Differential Output:** The differential summing node calculates the difference between $v_{p1}$ and $v_{n1}$, resulting in the differential output $v_{diff}$:
\( v_{diff} = 2k_1 v_1 + 2k_3 v_1^3 + 2k_5 v_1^5 + \cdots \)
This shows that even-order terms cancel out, leaving only odd-order terms.

Labels, Annotations, and Key Indicators:
- The nonlinear elements are labeled with their respective input-output relationships, highlighting the presence of even and odd-order terms.
- The differential output equation clearly shows the cancellation of even-order terms.

Overall System Function:
The primary function of this system is to demonstrate that in fully differential circuits, even-order distortion terms cancel out if the distortion is symmetrical around the common-mode voltage. This is achieved by using two identical nonlinear elements with inputs that are inverses of each other, and a differential summing node that calculates the difference between their outputs. This configuration results in a differential signal that predominantly contains odd-order distortion terms, which are typically smaller and less detrimental to signal quality.

Fig. 6.27 Demonstrating that even-order distortion terms cancel in fully differential circuits if the distortion is symmetrical around the common-mode voltage. Here, the common-mode voltage is assumed to be zero.
zero. If the nonlinearity is memoryless, then the outputs can be models by the following Taylor series expansion,

$$
\begin{equation*}
v_{0}=k_{1} v_{i}+k_{2} v_{i}^{2}+k_{3} v_{i}^{3}+k_{4} v_{i}^{4}+\cdots \tag{6.148}
\end{equation*}
$$

where $\mathrm{k}_{\mathrm{i}}$ are constant terms. In this case, the differential output signal, $\mathrm{v}_{\text {diff }}$, consists of only the linear term, $2 \mathrm{k}_{1} \mathrm{v}_{\mathrm{l}}$, and odd-order distortion terms (which are typically smaller than the second-order term). With these two important advantages, most modern analog signal processing circuits are realized using fully differential structures.

One drawback of using fully differential opamps is that a common-mode feedback (CMFB) circuit must be added. This extra circuitry is needed to establish the common-mode (i.e., average) output voltage. Consider the simple fully differential stage in Fig. 6.24(b) in the presence of a tiny error in the value of the tail current. Even a $0.0001 \%$ increase in the tail current not accompanied by a corresponding increase in the active load currents causes all nodes in the circuit to decrease slowly towards ground, eventually leaving some transistors in triode and degrading the circuit's gain. In practice, this is avoided by a CMFB circuit

Key Point: Compared to singleended circuits, fully-differential amplifiers offer reduced harmonic distortion. However, they require additional commonmode feedback circuitry in order to establish the signals' com-mon-mode levels.
that somehow observes the output voltages and establishes currents that keep all transistors biased properly. Ideally, the CMFB will keep the common-mode voltages immovable, preferably close to halfway between the power-supply voltages, even when large differential signals are present.

Although in the simple example of Fig. 6.24 the power dissipation is the same for both fully-differential and sin-gle-ended output circuits, in general some additional power consumption may be required by fully differential circuits. Specifically, some power may be consumed by the CMFB. In addition, fully differential current mirror opamps and two-stage opamps require additional power consumption in order to produce two output signals instead of one.

### 6.7.1 Fully Differential Folded-Cascode Opamp

A simplified schematic of a fully differential folded-cascode opamp is shown in Fig. 6.28. The n-channel current-mirror of Fig. 6.20 has been replaced by two cascode current sources, one composed of $Q_{7}$ and $Q_{8}$, the other composed of $Q_{9}$ and $Q_{10}$. In addition, a common-mode feedback (CMFB) circuit has been added. The gate voltage on the drive transistors of these current sources is determined by the output voltage, $\mathrm{V}_{\text {cntrt }}$, of the common-mode feedback circuit. The inputs to the CMFB circuit are the two outputs of the fully differential amplifier. The CMFB circuit will detect the average of these two outputs and force it to be equal to a predetermined value, as we shall see in the next section.

Note that when the opamp output is slewing, the maximum current available for the negative slew rate is limited by the bias currents of $Q_{7}$ or $Q_{9}$. If the CMFB circuit is very fast, these will be increased dynamically to some degree during slewing, but seldom to the degree of a single-ended output fully differential opamp. For this reason, fully differential folded-cascode opamps are usually designed with the bias currents in the output stage equal to
image_name:Fig. 6.28 A fully differential folded-cascode opamp.
description:The circuit is a fully differential folded-cascode operational amplifier with a common-mode feedback (CMFB) circuit. It uses PMOS transistors for the current mirrors and NMOS transistors for differential input pairs. Clamp transistors Q11 and Q12 are used to improve transient response. The CMFB circuit helps maintain output common-mode voltage.

Fig. 6.28 A fully differential folded-cascode opamp.
the bias currents in the input transistors. Also, to minimize transient voltage changes during slew-rate limiting, clamp transistors $Q_{11}$ and $Q_{12}$ have been added, as in the single-ended design presented earlier. If these transistors are not included (as has historically been the case), the time to recover from slew-rate limiting of the folded-cascode amplifier can be comparatively poor.

Each signal path now consists of only one node in addition to the output nodes, namely the drain nodes of the input devices. These nodes will most certainly be responsible for the equivalent second poles. In cases where the load capacitance is small, and it is important to maximize the bandwidth, a complementary design (i.e., n - and p-channel transistors and the power supplies interchanged) would be preferable to maximize the frequency of the equivalent second poles. This complementary circuit would result in the impedance at the drains of the input devices being the inverse of the transconductance of n -channel transistors, rather than p -channel transistors, resulting in smaller impedances and therefore faster time constants. The trade-off involved is that the opamp's transconductance, and therefore the opamp's dc gain, would become smaller due to the input transistors now being p-channel transistors. Also, the CMFB circuitry could possibly be slower, as the current sources being modulated would also have to be p -channel drive transistors. In any case, a complementary design is often a reasonable choice for high-speed fully differential designs.

### 6.7.2 Alternative Fully Differential Opamps

An alternative design is the fully differential current-mirror opamp, as shown in simplified form in Fig. 6.29. As with the folded-cascode design, this circuit can be realized as shown or in a complementary design, with p-channel input transistors, n -channel current mirrors, and p -channel bias current sources. Which design is preferable is primarily determined by whether the load capacitance or the equivalent second poles are limiting the bandwidth, and by whether maximizing the dc gain or the bandwidth is more important. n -channel inputs are preferable in the former case and p -channel inputs are preferable in the latter case, for reasons similar to those discussed for the folded-cascode opamp. Also, n-channel input transistors will give lower thermal noise (due to their larger transconductances), whereas p-channel inputs will result in less opamp input-referred 1/f noise.
image_name:Fig. 6.29 A fully differential current-mirror opamp.
description:The circuit is a fully differential current-mirror operational amplifier with a current gain of K=2. It includes a common-mode feedback (CMFB) circuit to stabilize the output common-mode voltage. The input stage uses NMOS transistors Q1 and Q2, while the output stage uses NMOS transistors Q3 to Q6. The bias current is provided by a current source Ibias. The circuit is designed for wide-swing and enhanced output-impedance cascode mirrors.

Fig. 6.29 A fully differential current-mirror opamp.

If a general-purpose fully differential opamp is desired, then this design with large p-channel input transistors, a current gain of $\mathrm{K}=2$, and wide-swing enhanced output-impedance cascode mirrors and current sources is probably a good choice, compared to all other fully differential alternatives.

One of the limitations of the fully differential opamps seen so far is that the maximum current at the output for single-ended slewing in one direction is limited by fixed current sources. It is possible to modify the designs to get bidirectional drive capability at the output, as is shown in Fig. 6.30. This opamp is similar to the current mirror design of Fig. 6.29, but now the current mirrors at the top (i.e., the p-channel current mirrors) have been replaced
image_name:Fig. 6.30 A fully differential opamp with bidirectional output drive.
description:The circuit is a fully differential opamp with bidirectional output drive capability, utilizing current mirrors with two outputs for increased current handling.

Fig. 6.30 A fully differential opamp with bidirectional output drive.
image_name:Fig. 6.30
description:The circuit is a fully differential opamp with bidirectional output drive capability, utilizing current mirrors with two outputs for increased current handling. It includes transformers with different turns ratios (1:1, 1:K, K:1) to manage current gains and outputs.

Fig. 6.31 A fully differential opamp composed of two single-ended output current-mirror opamps. CMFB circuit not shown.
by current mirrors having two outputs. The first output has a current gain of K and goes to the output of the opamp, as before. The second output has a gain of one and goes to a new n -channel current mirror that has a current gain of K , where it is mirrored a second time and then goes to the opamp's opposite output, as shown. Assume now the differential output is slewing in the positive direction. For this case, the differential input will be very positive and the slewing current going into $\mathrm{V}_{\text {outt }}$ will be $\mathrm{KI}_{\text {bias }}$, but due to the additional n -channel mirrors, the current being sinked from $\mathrm{V}_{\text {out- }}$ will also be $\mathrm{KI}_{\text {bias }}$. This circuit has an improved slew rate at the expense of slower smallsignal response due to the addition of the extra outputs on the p -channel mirrors and the additional n -channel mirrors, although in many applications this trade-off may be well merited. Of course, common-mode feedback must be added to the circuit of Fig. 6.30.

Another alternative for a fully differential opamp is to use two single-ended output opamps with their inputs connected in parallel and each of their outputs being one output side of the fully differential circuit. An example of such an approach using current-mirror subcircuits is shown in Fig. 6.31. This design has a fairly large slew rate when compared to the simpler fully differential current-mirror opamp of Fig. 6.29, but has additional current mirrors and complexity. Another advantage of this design is that the noise voltages due to the input transistors sum in a squared fashion, while the two signal paths sum linearly. ${ }^{17}$ As a result, this design has an improvement in signal-to-noise ratio of the input-referred gain by a factor of $\sqrt{2}$, or 3 dB . Also, the increase in total power dissipation is not significant when K is moderately large. As for the previous design, the compensation of the common-mode feedback loop is more difficult than for designs having fixed current sources biasing the output stages.

### 6.7.3 Low Supply Voltage Opamps

Low supply voltages complicate opamp design considerably. The input common-mode voltage must be restricted within a very tight range to ensure the input differential pair tail current remains in active mode. For example, referring to the folded cascode opamp in Fig. 6.28, and assuming that a simple NMOS transistor is used as the tail current source $\mathrm{I}_{\text {bias }}$, the input common-mode voltage must be greater than $\mathrm{V}_{\mathrm{GS} 1}+\mathrm{V}_{\text {eff }}$ in order to keep the tail
image_name:Fig. 6.32
description:The circuit is a folded cascode opamp with rail-to-rail input common-mode voltage range. It features two current sources I1 and I2 connected to the power supply. The input stage consists of PMOS transistors M1 and M2, and NMOS transistors Q1 and Q2. The output stage is composed of NMOS transistors Q7, Q8, Q9, and Q10. The circuit is designed to accommodate a wide range of input common-mode voltages.

Fig. 6.32 An opamp having rail-to-rail input common-mode voltage range. CMFB circuit not shown.
current source device in active mode. Assuming $\mathrm{V}_{\text {eff }} \cong 200 \mathrm{mV}, \mathrm{V}_{\mathrm{tn}} \cong 450 \mathrm{mV}$, and an additional 50 mV of margin to account for process and temperature variations, this means the input common model voltage must be at least 950 mV , a significant limitation if the supply voltage is only 1.2 V .

The opamp shown in somewhat simplified form in Fig. 6.32 makes use of both n -channel and p -channel transistors in the two differential input pairs. Hence, the input common-mode voltage range is increased [Babanezhad, 1988; Hogervorst, 1992; Coban, 1994], a particularly important feature when low power-supply voltages are being used. When the input commonmode voltage range is close to one of the power-supply voltages, one of the

Key Point: Low supply-voltages dictate the use of special circuit techniques to permit commonmode signal levels near the supply rails and/or to provide sufficient gain and output swing.
input differential pairs will turn off, but the other one will remain active. In an effort to keep the opamp gain relatively constant during this time, the bias currents of the still-active differential pair are dynamically increased. For example, if the input common-mode voltage range was close to the positive power-supply voltage, $Q_{3}$ and $Q_{4}$ would turn off, and $Q_{6}$ would conduct all of $I_{2}$. This current would go through current mirror $M_{1}$ and increase the bias current of the differential pair consisting of $Q_{1}$ and $Q_{2}$, which is still active. A similar situation occurs if the input common-mode voltage is near the negative power-supply rail. With careful design, it has been reported that the transconductance of the input stage can be held constant to within 15 percent of its nominal value with an input common-mode voltage range as large as the difference between the power-supply voltages [Coban, 1994].

Another challenge of low supply voltage designs is that it is very difficult to use single-stage folded-cascode architectures while maintaining a reasonable output swing. Referring to the folded-cascode schematic in Fig. 6.28, notice that the output nodes must remain at least $2 \mathrm{~V}_{\text {eff }}$ away from both the positive supply and ground in order to keep all of transistors $\mathrm{Q}_{3}-\mathrm{Q}_{10}$ in active mode. For example, if a $1.2-\mathrm{V}$ supply is to be used, assuming $\mathrm{V}_{\text {eff }} \approx 200 \mathrm{mV}$, and allowing a additional 50 mV of margin on both the NMOS and PMOS cascode voltages, the
output nodes will only be able to swing within the range 450 mV to 750 mV . The opamp circuit in Fig. 6.33 [Dessouky, 2001] is a two-stage opamp with a folded cascode first stage and common-source second stage. The cascode stage can provide high gain, but is not required to drive the opamp outputs, and hence is not required to accommodate the full output swing. The signal swing at $\mathrm{V}_{1}^{+}$and $\mathrm{V}_{1}^{-}$will be less than the output swing by a factor equal to the small-signal gain of the common-source second stage. Miller compensation is provided, just as with the conventional two-stage opamp, suing $\mathrm{C}_{\mathrm{C}}$ and $\mathrm{R}_{\mathrm{C}}$. This architecture can provide large gain even within a low supply voltage.

## 6.8 COMMON-MODE FEEDBACK CIRCUITS

Typically, when using fully-differential opamps in a feedback application, the applied feedback determines the differential signal voltages, but does not affect the common-mode voltages. It is therefore necessary to add additional circuitry to determine the output common-mode voltage and to control it to be equal to some specified voltage, usually about halfway between the power-supply voltages. This circuitry, referred to as the commonmode feedback (CMFB) circuitry, is often the most difficult part of the opamp to design.

There are two typical approaches to designing CMFB circuits-a continuous-time approach and a switchedcapacitor approach. The former approach is often the limiting factor on maximizing the signal swings, and, if nonlinear, may actually introduce common-mode signals. The latter approach is typically only used in switchedcapacitor circuits, since in continuous-time applications it introduces clock-feedthrough glitches.

An example of a continuous-time CMFB circuit is shown in Fig. 6.34 [Martin, 1985; Whatly, 1986]. To illustrate its operation, assume a common-mode output voltage, $\mathrm{V}_{\mathrm{out}, \mathrm{CM}}$, equal to the reference voltage, $\mathrm{V}_{\text {ref }, \mathrm{CM}}$, and that $\mathrm{V}_{\text {outt }}$ is equal in magnitude, but opposite in sign, to $\mathrm{V}_{\text {out }}$. Furthermore, assume the two differential pairs have infinite common-mode input rejection, which implies that the large-signal output currents of the differential pairs depend only on their input differential voltages. Since the two pairs have the same differential voltages being applied, the current in $Q_{1}$ will be equal to the current in $Q_{3}$, while the current in $Q_{2}$ will equal the current in $Q_{4}$. This result is valid independent of the nonlinear relationship between a differential pair's input voltage and its large-signal differential drain currents. Now, letting the current in $Q_{2}$ be denoted as $I_{D 2}=I_{B} / 2+\Delta I$, where $I_{B}$ is
image_name:Fig. 6.33 A differential Miller-compensated two-stage amplifier with a folded cascode first-stage
description:This is a differential Miller-compensated two-stage amplifier with a folded cascode first-stage. It includes a common-source second stage. The amplifier uses PMOS and NMOS transistors with current sources for biasing. The circuit is designed for differential input with a common-mode feedback not shown in the diagram.

Fig. 6.33 A differential Miller-compensated two-stage amplifier with a folded cascode first-stage [Dessouky, 2001]. (Common-mode feedback not shown.)
image_name:Fig. 6.34
description:This circuit represents a continuous-time common-mode feedback (CMFB) circuit. It uses PMOS and NMOS transistors to control the biasing and feedback mechanisms. The PMOS transistors are used to mirror the current, while the NMOS transistors are used for feedback control. The circuit is designed to maintain a stable common-mode voltage.

Fig. 6.34 An example of a continuous-time CMFB circuit.
the bias current of the differential pair and $\Delta I$ is the large-signal current change in $I_{D 2}$, the current in $Q_{3}$ is given by $\mathrm{I}_{\mathrm{D} 3}=\left(\mathrm{I}_{\mathrm{B}} / 2\right)-\Delta \mathrm{I}$, and the current in $\mathrm{Q}_{5}$ is given by

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D} 5}=\mathrm{I}_{\mathrm{D} 2}+\mathrm{I}_{\mathrm{D} 3}=\left(\mathrm{I}_{\mathrm{B}} / 2+\Delta \mathrm{I}\right)+\left(\left(\mathrm{I}_{\mathrm{B}} / 2\right)-\Delta \mathrm{I}\right)=\mathrm{I}_{\mathrm{B}} \tag{6.149}
\end{equation*}
$$

Thus, as long as the voltage $\mathrm{V}_{\text {out }}$ is equal to the negative value of $\mathrm{V}_{\text {out }}$, the current through diode-connected $\mathrm{Q}_{5}$ will not change even when large differential signal voltages are present. Since the voltage across diode-connected $\mathrm{Q}_{5}$ is used to control the bias voltages of the output stage of the opamps, this means that when no common-mode voltage is present, the bias currents in the output stage will be the same regardless of whether a signal is present or not. Note, however, that the above result does not remain valid if the output voltage is so large that transistors in the differential pairs turn off.

Next consider what happens when a common-mode voltage greater than $\mathrm{V}_{\mathrm{CM} \text {, ref }}$ is present. This positive voltage will cause the currents in both $Q_{2}$ and $Q_{3}$ to increase, which causes the current in diode-connected $Q_{5}$ to increase, which in turn causes its voltage to increase. This voltage is the bias voltage that sets the current levels in the n -channel current sources at the output of the opamp (e.g. transistors $\mathrm{Q}_{7,9}$ in Fig. 6.28 or $\mathrm{Q}_{3,5}$ in Fig. 6.29). Thus, both current sources will have larger currents pulling down to the negative rail, which will cause the com-mon-mode output voltage, $\mathrm{V}_{\text {out, } \mathrm{CM}}$, to decrease towards $\mathrm{V}_{\text {ref, } \mathrm{CM}}$. Thus, as long as the common-mode loop gain is large enough, and the differential signals are not so large as to cause transistors in the differential pairs to turn off, the common-mode output voltage will be kept very close to ground $\mathrm{V}_{\text {ref, CM. }}$.

The size of the differential signals that can be processed without one of the differential-pair signals turning off is maximized if the differential-pair transistors are designed to have large effective gate-source voltages. Additionally, source degeneration can be used to allow them to have larger input signals without all of the current being directed to one side of the differential pair, as shown in Fig. 6.35. However, even when this maximization is performed, the CMFB circuit may still limit the differential signals to be less than what can be processed by the rest of the opamp.

Finally the current sources $I_{B}$ should be high-output impedance cascode current sources to ensure good com-mon-mode rejection of the two differential pairs.
image_name:Fig. 6.35
description:This circuit is a continuous-time Common-Mode Feedback (CMFB) circuit designed to accommodate increased output swing. It features PMOS and NMOS transistors configured to control the common-mode voltage of the output signals. The circuit uses resistors to establish reference voltages and control the common-mode feedback loop. The current sources labeled as IB/2 and IB ensure proper biasing of the transistors.

Fig. 6.35 A continuous-time CMFB circuit that can accommodate increased output swing.
image_name:Fig. 6.35
description:The circuit is a continuous-time Common-Mode Feedback (CMFB) circuit designed to accommodate increased output swing. It uses PMOS and NMOS transistors to control the common-mode voltage of the output signals. Resistors establish reference voltages and control the common-mode feedback loop. Current sources labeled as IB/2 ensure proper biasing of the transistors. The circuit generates the common-mode voltage of the output signals at node VA, which is compared to a reference voltage, Vref.

Fig. 6.36 An alternative continuous-time CMFB circuit.

An alternative approach for realizing CMFB circuits is shown in Fig. 6.36 [Banu, 1988]. This circuit generates the common-mode voltage of the output signals (minus a dc level shift) at node $\mathrm{V}_{\mathrm{A}}$. This voltage is then compared to a reference voltage, $\mathrm{V}_{\text {ref }}$, using a separate amplifier. Although this approach works well, it has a major limitation in that the voltage drop across the source-follower transistors $Q_{1}, Q_{2}$ severely limits the differential signals that can be processed (unless transistors with native threshold voltages, such as 0.3 volts, are available). This limitation is particularly important when small power-supply voltages are used. In addition, the additional nodes of the common-mode feedback circuitry make the circuit slightly more difficult to compensate. When bipolar transistors are available, as is the case in a BiCMOS process, this approach is much more desirable.
image_name:Fig. 6.37
description:The circuit is a common-mode feedback loop in a fully differential folded-cascode opamp. It includes PMOS and NMOS transistors, an operational amplifier, and capacitors. The design aims to stabilize the common-mode output voltage using feedback control. The circuit is part of a negative feedback loop and must be well compensated to avoid instability.

Fig. 6.37 The common-mode feedback loop in a fully differential folded-cascode opamp.

An important consideration when designing CMFB circuits is that they are part of a negative feedback loop, as illustrated in Fig. 6.37, and must therefore be well compensated, otherwise the injection of common-mode signals can cause them to ring or even possibly become unstable. Thus, when the circuit is being designed, the phase margin and step-response of the common-mode loop should be found and verified by simulation. Phase margin might be observed, for example, by breaking the gate connections at $\mathrm{V}_{\text {cntrl }}$, applying a test small-signal and looking at the returned signal. A step-response test could be performed by applying a small step to the common-mode reference signal, $\mathrm{V}_{\text {ref, }, \mathrm{cm}}$.

Compensation of the CMFB loop may be difficult because it includes two high-impedance nodes: $\mathrm{V}_{\text {cntrl }}$ and the amplifier output. Moreover, high bandwidth is desirable in order to suppress high-frequency common-mode noise that may appear due to neighbouring on-chip clock signals. However, it is not generally necessary to set the output common-mode level extremely precisely; a few millivolts of error should certainly be tolerable. Hence, very high dc gain is not required in the CMFB. In fact too much dc loop gain may complicate compensation.

Often, the common-mode loop is stabilized using the same capacitors used to compensate the differential loop. This multipurpose compensation is achieved by connecting two compensation (or loading) capacitors between the opamp outputs and ground (or some other reference voltage). However, if the deferential loop is compensated using a single compensation capacitor connected directly between the two outputs, the common-mode loop remains uncompensated. It should be mentioned that by having as few nodes in the common-mode loop as possible, compensation is simplified without having to severely limit the speed of the CMFB circuit. For this reason, the CMFB circuit is usually used to control current sources in the output stage of the opamp, as opposed to the current sources in the input stage of the opamp. For the same reason, in two-stage fully-differential opamps such as in Fig. 6.33, the common-mode output voltage of each stage is observed and controlled using a separate CMFB circuit. High speed in the CMFB circuit is necessary to minimize the effects of high-frequency common-mode noise, which could otherwise be amplified, causing the opamp outputs to saturate. Designing continuous-time CMFB circuits that are both linear and operate with low power-supply voltages is an area of continuing research.

A third approach for realizing CMFB circuits is based on the use of switched-capacitor circuits. An example of this approach is shown in Fig. 6.38 [Senderowicz, 1982; Castello, 1985]. In this approach, capacitors labelled $\mathrm{C}_{\mathrm{C}}$ generate the average of the output voltages, which is used to create control voltages for the opamp current
image_name:Fig. 6.38
description:This circuit is a switched-capacitor common-mode feedback (CMFB) circuit. It uses capacitors CS and CC to generate control voltages for the opamp current sources. The circuit functions similarly to a switched-capacitor low-pass filter with a DC input signal. Bias voltages are set to control the desired common-mode voltage and opamp current source control voltage.

Fig. 6.38 A switched-capacitor CMFB circuit.
sources. The dc voltage across $C_{C}$ is determined by capacitors $C_{s}$, which are switched between bias voltages and between being in parallel with $\mathrm{C}_{\mathrm{C}}$. This circuit acts much like a simple switched-capacitor low-pass filter having a dc input signal. The bias voltages are designed to be equal to the difference between the desired common-mode voltage and the desired control voltage used for the opamp current sources.

Key Point: Common-mode feedback may be performed using switchedcapacitor circuits in discrete-time applications. When continuous-time signals are present, the design of a suitable CMFB can be a significant challenge because it introduces constraints on output swing, and may reduce the opamp's load impedance.

The capacitors being switched, $\mathrm{C}_{\mathrm{S}}$, might be between one-quarter and one-tenth the sizes of the fixed (not switched) capacitors, $\mathrm{C}_{\mathrm{C}}$. Using larger capacitance values overloads the opamp more than is necessary during the phase $\phi_{2}$, and their size is not critical to circuit performance. Reducing the capacitors too much causes common-mode offset voltages due to charge injection of the switches. Normally, all of the switches would be realized by minimum-size n -channel transistors only, except for the switches connected to the outputs, which might be realized by transmission gates (i.e., parallel n -channel and p -channel transistors both having minimum size) to accommodate a wider signal swing.
In applications where the opamp is being used to realize switched-capacitor circuits, switched-capacitor CMFB circuits are generally preferred over their continuous-time counterparts since they allow a larger output signal swing.

## 6.9 SUMMARY OF KEY POINTS

- The classic two-stage opamp comprises a differential input gain stage, a common-source second gain stage, and optionally a unity-gain output buffer stage. [p. 243]
- The dc gain of the two-stage opamp is approximated by the product of two stages, each having a gain of approximately $\mathrm{g}_{\mathrm{m}} \mathrm{r}_{\mathrm{ds}} / 2$. [p. 244]
- The two-stage opamp's frequency response is dominated by a pole at the input to the second stage arising from the introduced Miller capacitor, $C_{C}$. A dominant-pole approximation yields a unity-gain frequency of $g_{m 1} / C_{C}$. [p. 246]
- The two-stage opamp's second pole arises at the output node and may be increased by increasing the secondstage transconductance, $\mathrm{gm}_{7}$. [p. 248]
- The slew rate is the maximum rate at which the output of an opamp changes when a large differential input signal is present. [p. 249]
- The only ways of improving the slew rate of a two-stage opamp is to increase $\mathrm{V}_{\text {eff1 }}$ or $\omega_{\mathrm{p} 2}$. [p. 251]
- When using a two-stage opamp, p-channel input transistors are almost always the best choice for the first stage because they offer larger unity-gain frequency and lower $1 / \mathrm{f}$ noise, with the major disadvantage being an increase in wideband thermal noise. [p. 252]
- In general, dominant-pole compensation is performed by decreasing the frequency of one pole in a feedback loop while leaving the others relatively unchanged. [p. 254]
- Lead compensation in opamp circuits introduces into the loop response a left half-plane zero at a frequency slightly greater than the unity gain frequency to provide a small phase lead and, therefore, and increase in phase margin. [p. 255]
- The feedback network must be accounted for in compensation. [p. 255]
- Compensation of the two-stage opamp proceeds by selecting Miller capacitor $C_{C}$ to provide 55 degrees phase margin, then introducing a lead compensation series resistor to add another 30 degrees of phase margin. [p. 257]
- Cascoding is a key technique to enable high gain using transistors with low drain-source resistance, but if the cascode transistor is improperly biased, output swing is greatly reduced. [p. 262]
- Auxiliary amplifiers may be used to enhance the output impedance of cascode current mirrors and gain stages, thereby boosting dc gain. [p. 264]
- Operational transconductance amplifiers provide a large dc gain from a single stage. Their high output impedance makes them suitable for driving the mostly-capacitive loads encountered in CMOS integrated circuits. With feedback, they can also drive some resistive load. [p. 268]
- The folded-cascode opamp is a transconductance amplifier whose frequency response is dominated by the output pole at $1 / \mathrm{R}_{\mathrm{out}} \mathrm{C}_{\mathrm{L}}$. [p. 269]
- If the bandwidth of a folded-cascode opamp is insufficient, one must increase the input transconductance. [p. 270]
- If the phase margin of a folded-cascode opamp is insufficient, one must either reduce the bandwidth by adding output capacitance, or burn more power in the output transistors to increase the second pole frequency. [p. 271]
- For a current-mirror opamp, when the load capacitance is large and the output pole clearly dominant, a large current mirror ratio, $K$, maximizes gain and bandwidth. If the second pole frequency becomes significant, lower values of K are required to keep the second pole frequency above the unity-gain frequency and maintain a healthy phase margin. [p. 277]
- Fully differential amplifiers generally have similar power consumption, but twice the available signal swing of their single-ended counterparts. They can also exhibit similar small signal gain and bandwidth. [p. 281]
- A significant advantage of fully differential amplifiers is that common mode noise is rejected. Although random noise power may be 2-times greater than in a similar single-ended circuit, the increased signal swing available in fully differential circuits generally affords them a higher maximum signal-to-noise ratio. [p. 282]
- Compared to singleended circuits, fully-differential amplifiers offer reduced harmonic distortion. However, they require additional commonmode feedback circuitry in order to establish the signals' common-mode levels. [p. 283]
- Low supply-voltages dictate the use of special circuit techniques to permit common-mode signal levels near the supply rails and/or to provide sufficient gain and output swing. [p. 287]
- Common-mode feedback may be performed using switched-capacitor circuits in discrete-time applications. When continuous-time signals are present, the design of a suitable CMFB can be a significant challenge because it introduces constraints on output swing, and may reduce the opamp's load impedance. [p. 292]
