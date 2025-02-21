# 7. Frequency Response of Integrated Circuits

## 7.1 Introduction

The analysis of integrated-circuit behavior in previous chapters was concerned with lowfrequency performance, and the effects of parasitic capacitance in transistors were not considered. However, as the frequency of the signal being processed by a circuit increases, the capacitive elements in the circuit eventually become important.

In this chapter, the small-signal behavior of integrated circuits at high frequencies is considered. The frequency response of single-stage amplifiers is treated first, followed by an analysis of multistage amplifiers. Finally, the frequency response of the NE5234 operational amplifier is considered, and those parts of the circuit that limit its frequency response are identified.

## 7.2 Single-Stage Amplifiers

The basic topology of the small-signal equivalent circuits of bipolar and MOS single-stage amplifiers are similar. Therefore in the following sections, the frequency-response analysis for each type of single-stage circuit is initially carried out using a general small-signal model that applies to both types of transistors, and the general results are then applied to each type of transistor. The general small-signal transistor model is shown in Fig. 7.1. Table 7.1 lists the parameters of this small-signal model and the corresponding parameters that transform it into a bipolar or MOS model. For example, $C_{\text {in }}$ in the general model becomes $C_{\pi}$ in the bipolar model and $C_{g s}$ in the MOS model. However, some device-specific small-signal elements are not included in the general model. For example, the $g_{m b}$ generator and capacitors $C_{s b}$ and $C_{g b}$ in the MOS models are not incorporated in the general model. The effect of such device-specific elements will be handled separately in the bipolar and MOS sections.

The common-emitter and common-source stages are analyzed in the sections below on differential amplifiers.

### 7.2.1 Single-Stage Voltage Amplifiers and the Miller Effect

Single-transistor voltage-amplifier stages are widely used in integrated circuits. Figures $7.2 a$ and $7.2 b$ show the ac schematics for common-emitter and common-source amplifiers with resistive loads, respectively. Resistance $R_{S}$ is the source resistance, and $R_{L}$ is the load resistance. A simple linear model that can be applied to both of these circuits is shown in Fig. 7.2c. The elements in the dashed box form the general small-signal transistor model from Fig. 7.1 without $r_{o}$. We will assume that the output resistance of the transistor $r_{o}$ is much larger than $R_{L}$. Since these resistors are connected in parallel in the small-signal circuit, $r_{o}$ can be neglected. An approximate analysis of this circuit can be made using the Miller-effect approximation.
image_name:Figure 7.1 A general small-signal transistor model
description:
[
name: rx, type: Resistor, value: rx, ports: {N1: B or G, N2: rx rin}
name: rin, type: Resistor, value: rin, ports: {N1: rx rin, N2: E or S}
name: Cin, type: Capacitor, value: Cin, ports: {Np: rx rin, Nn: E or S}
name: Cf, type: Capacitor, value: Cf, ports: {Np: rx rin, Nn: C or D}
name: 8mv1, type: CurrentSource, value: 8mv1, ports: {Np: C or D, Nn: E or S}
name: ro, type: Resistor, value: ro, ports: {N1: C or D, N2: E or S}
]
extrainfo:The circuit is a general small-signal transistor model with resistors, capacitors, and a dependent current source. The output resistance ro is neglected in the analysis due to its large value compared to RL. The circuit uses the Miller-effect approximation for analysis.

Figure 7.1 A general small-signal transistor model.

This analysis is done by considering the input impedance seen looking across the plane AA in Fig. 7.2c. To find this impedance, we calculate the current $i_{1}$ produced by the voltage $v_{1}$.

$$
\begin{equation*}
i_{1}=\left(v_{1}-v_{o}\right) s C_{f} \tag{7.1}
\end{equation*}
$$

KCL at the output node gives

$$
\begin{equation*}
g_{m} v_{1}+\frac{v_{o}}{R_{L}}+\left(v_{o}-v_{1}\right) s C_{f}=0 \tag{7.2}
\end{equation*}
$$

From (7.2), the voltage gain $A_{v}$ from $v_{1}$ to $v_{o}$ can be expressed as

$$
\begin{equation*}
A_{v}(s)=\frac{v_{o}}{v_{1}}=-g_{m} R_{L}\left(\frac{1-s \frac{C_{f}}{g_{m}}}{1+s R_{L} C_{f}}\right) \tag{7.3}
\end{equation*}
$$

Using $v_{o}=A_{v}(s) v_{1}$ from (7.3) in (7.1) gives

$$
\begin{equation*}
i_{1}=\left[1-A_{v}(s)\right] s C_{f} v_{1} \tag{7.4}
\end{equation*}
$$

Equation 7.4 indicates that the admittance seen looking across the plane AA has a value $\left[1-A_{v}(s)\right] s C_{f}$. This modification to the admittance $s C_{f}$ stems from the voltage gain across $C_{f}$ and is referred to as the Miller effect. Unfortunately, this admittance is complicated, due to the frequency dependence of $A_{v}(s)$. Replacing the voltage gain $A_{\nu}(s)$ in (7.4) with its low-frequency value $A_{\nu 0}=A_{\nu}(0)$, (7.4) indicates that a capacitance of value

$$
\begin{equation*}
C_{M}=\left(1-A_{\nu 0}\right) C_{f} \tag{7.5}
\end{equation*}
$$

is seen looking across plane AA. The use of the low-frequency voltage gain here is called the Miller approximation, and $C_{M}$ is called the Miller capacitance. From (7.3), $A_{v 0}=A_{v}(0)=$ $-g_{m} R_{L}$; therefore, (7.5) can be written as

$$
\begin{equation*}
C_{M}=\left(1+g_{m} R_{L}\right) C_{f} \tag{7.6}
\end{equation*}
$$

The Miller capacitance is often much larger than $C_{f}$ because usually $g_{m} R_{L} \gg 1$.

Table 7.1 Small-Signal Model Elements

| General Model | Bipolar Model | MOS Model |
| :---: | :---: | :---: |
| $r_{x}$ | $r_{b}$ | 0 |
| $r_{\text {in }}$ | $r_{\pi}$ | $\infty$ |
| $C_{\mathrm{in}}$ | $C_{\pi}$ | $C_{g s}$ |
| $C_{f}$ | $C_{\mu}$ | $C_{g d}$ |
| $r_{o}$ | $r_{o}$ | $r_{o}$ |

image_name:(a)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: vi, N2: b0}
name: RL, type: Resistor, value: RL, ports: {N1: vo, N2: GND}
name: M0, type: NPN, ports: {e: GND, c: vo, b: V0}
]
extrainfo:The circuit is a common-emitter amplifier with an NMOS transistor M0. The input voltage source vi is connected to the gate of M0 through the resistor RS. The output is taken from the drain of M0, which is connected to RL.
image_name:(b)
description:
[
name: vi, type: VoltageSource, value: vi, ports: {Np: vi, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: vi, N2: g0}
name: M0 (b), type: NMOS, ports: {S: GND, D: vo, G: g0}
name: RL, type: Resistor, value: RL, ports: {N1: vo, N2: GND}
]
extrainfo:The circuit diagram (b) represents an AC schematic of a common-source amplifier using an NMOS transistor. The input voltage source 'vi' is connected through a resistor 'RS' to the gate of the NMOS transistor 'M0'. The drain of the NMOS is connected to the output node 'vo' and load resistor 'RL'. The source is connected to ground.
image_name:(c)
description:
[
name: vi, type: VoltageSource, ports: {Np: vi, Nn: GND}
name: RS, type: Resistor, ports: {N1: vi, N2: X1}
name: rx, type: Resistor, ports: {N1: X1, N2: X2}
name: rin, type: Resistor, ports: {N1: X2, N2: GND}
name: Cin, type: Capacitor, value: Cin, ports: {Np: X2, Nn: GND}
name: Cf, type: Capacitor, value: Cf, ports: {Np: X2, Nn: vo}
name: gmv1, type: VoltageControlledCurrentSource, ports: {Np: vo, Nn: GND}
name: RL, type: Resistor, ports: {N1: vo, N2: GND}
]
extrainfo:The circuit is a small-signal model for a common-source amplifier using the Miller-effect approximation. It includes a voltage source, resistors, capacitors, and a voltage-controlled current source. The input is at node 'vi', and the output is at node 'vo'.

Figure 7.2 (a) An ac schematic of a common-emitter amplifier. (b) An ac schematic of a commonsource amplifier. (c) A general model for both amplifiers.

We can now form a new equivalent circuit that is useful for calculating the forward transmission and input impedance of the circuit. This is shown in Fig. 7.3 using the Miller-effect approximation. Note that this equivalent circuit is not useful for calculating high-frequency reverse transmission or output impedance. From this circuit, we can see that at high frequencies the input impedance will eventually approach $r_{x}$.

The physical origin of the Miller capacitance is found in the voltage gain of the circuit. At low frequencies, a small input voltage $v_{1}$ produces a large output voltage $v_{o}=A_{v 0} v_{1}=$ $-g_{m} R_{L} v_{1}$ of opposite polarity. Thus the voltage across $C_{f}$ in Fig. $7.2 c$ is $\left(1+g_{m} R_{L}\right) v_{1}$ and a correspondingly large current $i_{1}$ flows in this capacitor. The voltage across $C_{M}$ in Fig. 7.3 is only $v_{1}$, but $C_{M}$ is larger than $C_{f}$ by the factor $\left(1+g_{m} R_{L}\right)$; therefore, $C_{M}$ conducts the same current as $C_{f}$.
image_name:Figure 7.3
description:
[
name: vi, type: VoltageSource, value: vi, ports: {Np: Vi, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vi, N2: RSx}
name: rx, type: Resistor, value: rx, ports: {N1: RSx, N2: rXrin}
name: rin, type: Resistor, value: rin, ports: {N1: rXrin, N2: GND}
name: Cin, type: Capacitor, value: Cin, ports: {Np: Xrin, Nn: GND}
name: CM, type: Capacitor, value: CM, ports: {Np: rXrin, Nn: GND}
name: gmv1, type: VoltageControlledCurrentSource, value: gmv1, ports: {Np: GND, Nn: Vo}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is an equivalent model using the Miller approximation. It includes a voltage source, resistors, capacitors, a voltage-controlled current source, and a load resistor. The Miller capacitance CM impacts the bandwidth of the amplifier.

Figure 7.3 Equivalent circuit for Fig. 7.2c using the Miller approximation.

In Fig. 7.3, the Miller capacitance adds directly to $C_{\text {in }}$ and thus reduces the bandwidth of the amplifier, which can be seen by calculating the gain of the amplifier as follows:

$$
\begin{gather*}
v_{1}=\frac{\frac{r_{\text {in }}}{1+s r_{\text {in }} C_{t}}}{\frac{r_{\text {in }}}{1+s r_{\text {in }} C_{t}}+R_{S}+r_{x}} v_{i}  \tag{7.7}\\
v_{o}=-g_{m} R_{L} v_{1} \tag{7.8}
\end{gather*}
$$

where

$$
\begin{equation*}
C_{t}=C_{M}+C_{\mathrm{in}} \tag{7.9}
\end{equation*}
$$

Substitution of (7.7) in (7.8) gives the gain

$$
\begin{gather*}
A(s)=\frac{v_{o}}{v_{i}}=-g_{m} R_{L} \frac{r_{\text {in }}}{R_{S}+r_{x}+r_{\text {in }}} \frac{1}{1+s C_{t} \frac{\left(R_{S}+r_{x}\right) r_{\mathrm{in}}}{R_{S}+r_{x}+r_{\text {in }}}}  \tag{7.10a}\\
=K \frac{1}{1-\frac{s}{p_{1}}} \tag{7.10b}
\end{gather*}
$$

where $K$ is the low-frequency voltage gain and $p_{1}$ is the pole of the circuit. Comparing (7.10a) and (7.10b) shows that

$$
\begin{gather*}
K=-g_{m} R_{L} \frac{r_{\text {in }}}{R_{S}+r_{x}+r_{\text {in }}}  \tag{7.11a}\\
p_{1}=-\frac{R_{S}+r_{x}+r_{\text {in }}}{\left(R_{S}+r_{x}\right) r_{\text {in }}} \cdot \frac{1}{C_{t}}=-\frac{1}{\left[\left(R_{S}+r_{x}\right) \| r_{\text {in }}\right] C_{t}} \\
=-\frac{1}{\left[\left(R_{S}+r_{x}\right) \| r_{\text {in }}\right] \cdot\left[C_{\text {in }}+C_{f}\left(1+g_{m} R_{L}\right)\right]} \tag{7.11b}
\end{gather*}
$$

This analysis indicates that the circuit has a single pole, and setting $s=j \omega$ in (7.10b) shows that the voltage gain is 3 dB below its low-frequency value at a frequency

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}}=\left|p_{1}\right|=\frac{R_{S}+r_{x}+r_{\mathrm{in}}}{\left(R_{S}+r_{x}\right) r_{\mathrm{in}}} \cdot \frac{1}{C_{t}}=\frac{1}{\left[\left(R_{S}+r_{x}\right) \| r_{\mathrm{in}}\right] \cdot\left[C_{\mathrm{in}}+C_{f}\left(1+g_{m} R_{L}\right)\right]} \tag{7.12}
\end{equation*}
$$

As $C_{t}, R_{L}$, or $R_{S}$ increase, the $-3-\mathrm{dB}$ frequency of the amplifier is reduced.
The exact gain expression for this circuit can be found by analyzing the equivalent circuit shown in Fig. 7.4. The poles from an exact analysis can be compared to the pole found using the Miller effect. In Fig. 7.4, a Norton equivalent is used at the input where

$$
\begin{gather*}
R=\left(R_{S}+r_{x}\right) \| r_{\text {in }}  \tag{7.13}\\
i_{i}=\frac{v_{i}}{R_{S}+r_{x}} \tag{7.14}
\end{gather*}
$$

image_name:Figure 7.4
description:
[
name: i_i, type: CurrentSource, value: i_i, ports: {Np: X1, Nn: X1}
name: R, type: Resistor, value: R, ports: {N1: X1, N2: X}
name: C_in, type: Capacitor, value: C_in, ports: {Np: X, Nn: X1}
name: C_f, type: Capacitor, value: C_f, ports: {Np: X, Nn: Y}
name: g_m v_1, type: VoltageControlledCurrentSource, ports: {Np: X, Nn: Y}
name: R_L, type: Resistor, value: R_L, ports: {N1: Y, N2: X1}
]
extrainfo:The circuit is a Norton equivalent with feedback components, including capacitors C_in and C_f, a voltage-controlled current source g_m v_1, and resistors R and R_L. It demonstrates current and voltage relationships at nodes X and Y.

Figure 7.4 Figure $7.2 c$ redrawn using a Norton equivalent circuit at the input.

KCL at node $X$ gives

$$
\begin{equation*}
i_{i}=\frac{v_{1}}{R}+v_{1} s C_{\mathrm{in}}+\left(v_{1}-v_{o}\right) s C_{f} \tag{7.15}
\end{equation*}
$$

KCL at node $Y$ gives

$$
\begin{equation*}
g_{m} v_{1}+\frac{v_{o}}{R_{L}}+\left(v_{o}-v_{1}\right) s C_{f}=0 \tag{7.16a}
\end{equation*}
$$

Equation 7.16 a can be written as

$$
\begin{equation*}
v_{1}\left(g_{m}-s C_{f}\right)=-v_{o}\left(\frac{1}{R_{L}}+s C_{f}\right) \tag{7.16b}
\end{equation*}
$$

and thus

$$
\begin{equation*}
v_{1}=-v_{o} \frac{\frac{1}{R_{L}}+s C_{f}}{g_{m}-s C_{f}} \tag{7.17}
\end{equation*}
$$

Substitution of (7.17) in (7.15) gives

$$
i_{i}=-\left(\frac{1}{R}+s C_{\mathrm{in}}+s C_{f}\right) \frac{\frac{1}{R_{L}}+s C_{f}}{g_{m}-s C_{f}} v_{o}-s C_{f} v_{o}
$$

and the transfer function can be calculated as

$$
\begin{equation*}
\frac{v_{o}}{i_{i}}=-\frac{R R_{L}\left(g_{m}-s C_{f}\right)}{1+s\left(C_{f} R_{L}+C_{f} R+C_{\mathrm{in}} R+g_{m} R_{L} R C_{f}\right)+s^{2} R_{L} R C_{f} C_{\mathrm{in}}} \tag{7.18}
\end{equation*}
$$

Substitution of $i_{i}$ from (7.14) in (7.18) gives

$$
\begin{equation*}
\frac{v_{o}}{v_{i}}=-\frac{g_{m} R_{L} R}{R_{S}+r_{x}} \frac{1-s \frac{C_{f}}{g_{m}}}{1+s\left(C_{f} R_{L}+C_{f} R+C_{\mathrm{in}} R+g_{m} R_{L} R C_{f}\right)+s^{2} R_{L} R C_{f} C_{\mathrm{in}}} \tag{7.19}
\end{equation*}
$$

Substitution of $R$ from (7.13) into (7.19) gives, for the low-frequency gain,

$$
\begin{equation*}
\left.\frac{v_{o}}{v_{i}}\right|_{\omega=0}=-g_{m} R_{L} \frac{r_{\text {in }}}{R_{S}+r_{x}+r_{\mathrm{in}}} \tag{7.20}
\end{equation*}
$$

as obtained in (7.10).
Equation 7.19 shows that the transfer function $v_{o} / v_{i}$ has a positive real zero with magnitude $g_{m} / C_{f}$. This zero stems from the transmission of the signal directly through $C_{f}$ to the output. The effect of this zero is small except at very high frequencies, and it will be neglected here. However, this positive real zero can be important in the stability analysis of some operational amplifiers, and it will be considered in detail in Chapter 9. The denominator of (7.19) shows that the transfer function has two poles, which are usually real and widely separated in practice. If the poles are at $p_{1}$ and $p_{2}$, we can write the denominator of (7.19) as

$$
\begin{equation*}
D(s)=\left(1-\frac{s}{p_{1}}\right)\left(1-\frac{s}{p_{2}}\right) \tag{7.21}
\end{equation*}
$$

and thus

$$
\begin{equation*}
D(s)=1-s\left(\frac{1}{p_{1}}+\frac{1}{p_{2}}\right)+\frac{s^{2}}{p_{1} p_{2}} \tag{7.22}
\end{equation*}
$$

We now assume that the poles are real and widely separated, and we let the lower frequency pole be $p_{1}$ (the dominant pole) and the higher frequency pole be $p_{2}$ (the nondominant pole). Then $\left|p_{2}\right| \gg\left|p_{1}\right|$ and (7.22) becomes

$$
\begin{equation*}
D(s) \approx 1-\frac{s}{p_{1}}+\frac{s^{2}}{p_{1} p_{2}} \tag{7.23}
\end{equation*}
$$

If the coefficient of $s$ in (7.23) is compared with that in (7.19), we can identify

$$
\begin{align*}
p_{1} & =-\frac{1}{C_{\text {in }} R+C_{f}\left(R+g_{m} R_{L} R+R_{L}\right)} \\
& =-\frac{1}{R\left[C_{\mathrm{in}}+C_{f}\left(1+g_{m} R_{L}+\frac{R_{L}}{R}\right)\right]} \tag{7.24}
\end{align*}
$$

If the value of $R$ from (7.13) is substituted in (7.24), then the dominant pole is

$$
\begin{align*}
p_{1} & =-\frac{R_{S}+r_{x}+r_{\mathrm{in}}}{\left(R_{S}+r_{x}\right) r_{\mathrm{in}}} \frac{1}{\left[C_{\mathrm{in}}+C_{f}\left(1+g_{m} R_{L}+\frac{R_{L}}{R}\right)\right]} \\
& =-\frac{1}{\left[\left(R_{S}+r_{x}\right) \| r_{\mathrm{in}}\right] \cdot\left[C_{\mathrm{in}}+C_{f}\left(1+g_{m} R_{L}+\frac{R_{L}}{R}\right)\right]} \tag{7.25}
\end{align*}
$$

This value of $p_{1}$ is almost identical to that given in (7.11b) by the Miller approximation. The only difference between these equations is in the last term in the denominator of (7.25), $R_{L} / R$, and this term is usually small compared to the $\left(1+g_{m} R_{L}\right)$ term. This result shows that the Miller-effect calculation is nearly equivalent to calculating the dominant pole of the amplifier and neglecting higher frequency poles. The Miller approximation gives a good estimate of $\omega_{-3 \mathrm{~dB}}$ in many circuits.

Let us now calculate the nondominant pole by equating the coefficient of $s^{2}$ in (7.23) with that in (7.19), giving

$$
\begin{equation*}
p_{2}=\frac{1}{p_{1}} \frac{1}{R_{L} R C_{f} C_{\mathrm{in}}} \tag{7.26}
\end{equation*}
$$

Substitution of $p_{1}$ from (7.24) in (7.26) gives

$$
\begin{equation*}
p_{2}=-\left(\frac{1}{R_{L} C_{f}}+\frac{1}{R C_{\mathrm{in}}}+\frac{1}{R_{L} C_{\mathrm{in}}}+\frac{g_{m}}{C_{\mathrm{in}}}\right) \tag{7.27}
\end{equation*}
$$

The results in this section were derived using a general small-signal model. The general model parameters and the corresponding parameters for a bipolar and MOS transistor are listed in Table 7.1. By substituting values from Table 7.1, the general results of this section will be extended to the bipolar common-emitter and MOS common-source amplifiers, which appear in the half-circuits for differential amplifiers in the following sections.

#### 7.2.1.1 The Bipolar Differential Amplifier: Differential-Mode Gain

A basic building block of analog bipolar integrated circuits is the differential stage shown in Fig. 7.5. For small-signal differential inputs at $v_{i}$, the node $E$ is a virtual ground, and we can form the differential-mode (DM) ac half-circuit of Fig. 7.6a. The gain of this commonemitter circuit is equal to the DM gain of the full circuit. The circuit analysis that follows applies to this DM half-circuit as well as any single-stage common-emitter amplifier of the form shown in Fig. 7.6a. The small-signal equivalent circuit of Fig. 7.6a is shown in Fig. 7.6b
image_name:Figure 7.5 Bipolar differential amplifier circuit
description:
[
name: Q0, type: NPN, ports: {C: Vop, B: b0, E: E}
name: Q1, type: NPN, ports: {C: Von, B: b1, E: E}
name: RS, type: Resistor, value: RS, ports: {N1: Vip, N2: b0}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: b1}
name: RL, type: Resistor, value: RL, ports: {N1: Vcc, N2: Vop}
name: RL, type: Resistor, value: RL, ports: {N1: Von, N2: VCC}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: E, Nn: -VEE}
]
extrainfo:This is a bipolar differential amplifier circuit. It features two NPN transistors (Q0 and Q1) forming a differential pair. Each transistor is connected to a resistor (RS) at its base for input signal coupling. The circuit is powered by a dual supply (VCC and -VEE) and includes load resistors (RL) and coupling capacitors (Co and Cl) at the collectors. The current source IEE provides biasing current.

Figure 7.5 Bipolar differential amplifier circuit.
and, for compactness, the factor of $1 / 2$ has been omitted from the input and output voltages. This change does not alter the analysis in any way. Also, for simplicity, the collector-substrate capacitance of the transistor has been omitted. Since this capacitance would be connected in parallel with $R_{L}$, its effect could be included in the following analysis by replacing $R_{L}$ with $Z_{L}$, where $Z_{L}$ equals $R_{L}$ in parallel with $C_{c s}$.
image_name:(a)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: vi/2, N2: b0}
name: RL, type: Resistor, value: RL, ports: {N1: vo/2, N2: GND}
name: MO, type: NPN, ports: {C: vo/2, B: b0, E: GND}
]
extrainfo:The circuit is a small-signal model of a bipolar differential amplifier with an NPN transistor MO, input voltage vi/2, and output voltage vo/2. The resistor RS is connected to the base of the transistor, and RL is connected to the collector, with both having ground as a common reference.

image_name:(b)
description:
[
name: Vi, type: VoltageSource, value: vi, ports: {Np: Vi, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vi, N2: g0}
name: rb, type: Resistor, value: rb, ports: {N1: g0, N2: c0}
name: rπ, type: Resistor, value: rπ, ports: {N1: c0, N2: GND}
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: c0, Nn: GND}
name: Cμ, type: Capacitor, value: Cμ, ports: {Np: c0, Nn: Vo}
name: gmv1, type: CurrentSource, value: gmv1, ports: {Np: c0, Nn: Vo}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a small-signal model of a bipolar differential amplifier. It includes an NPN transistor modeled by a transconductance current source (gmv1), with input voltage vi/2 and output voltage vo/2. Resistors RS and RL are connected to the base and collector respectively, both referenced to ground.

Figure 7.6 (a) Differential-mode ac half-circuit for Fig. 7.5. (b) Small-signal equivalent circuit for (a).
image_name:Figure 7.7
description:The graph depicted is a pole-zero plot in the complex s-plane, which is typically used in control systems and signal processing to analyze the stability and frequency response of a system.

1. **Type of Graph and Function:**
- This is a pole plot in the complex s-plane, showing the location of poles.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \( \sigma \), representing the real part of the complex frequency.
- The vertical axis is labeled \( j\omega \), representing the imaginary part of the complex frequency.
- The graph is plotted in the complex plane with no specific units marked, as it is a conceptual representation.

3. **Overall Behavior and Trends:**
- The graph shows two poles located on the real axis of the s-plane.
- Both poles, labeled \( p_1 \) and \( p_2 \), are positioned on the left half of the s-plane, indicating a stable system if this were a control system analysis.

4. **Key Features and Technical Details:**
- The poles are marked with an 'X'.
- \( p_1 \) is closer to the origin compared to \( p_2 \).
- The positions of the poles suggest a system with real and negative roots, typically associated with exponential decay in time-domain responses.

5. **Annotations and Specific Data Points:**
- The graph includes labels for the poles as \( p_1 \) and \( p_2 \), but no numerical values for their exact positions are provided.

This graph provides insight into the dynamics of a system, where the location of poles can indicate stability and transient response characteristics.

Figure 7.7 Typical pole positions for the circuit in Fig. 7.4.

The small-signal circuit in Fig. 7.2c becomes the circuit in Fig. 7.6b when the bipolar model parameters in the second column of Table 7.1 are substituted for the general model parameters in Fig. 7.2c. Therefore, the analysis results from the previous section can be used here. Substituting the values in the second column of Table 7.1 into (7.19), the voltage gain is given by

$$
\begin{equation*}
\frac{v_{o}}{v_{i}}=-\frac{\frac{g_{m} R_{L} R}{R_{S}+r_{b}}\left(1-s \frac{C_{\mu}}{g_{m}}\right)}{1+s\left(C_{\mu} R_{L}+C_{\mu} R+C_{\pi} R+g_{m} R_{L} R C_{\mu}\right)+s^{2} R_{L} R C_{\mu} C_{\pi}} \tag{7.28}
\end{equation*}
$$

where $R=\left(R_{S}+r_{b}\right) \| r_{\pi}$. Using (7.25), the dominant pole is given by

$$
\begin{equation*}
p_{1}=-\frac{1}{\left[\left(R_{S}+r_{b}\right) \| r_{\pi}\right]\left[C_{\pi}+C_{\mu}\left(1+g_{m} R_{L}+\frac{R_{L}}{R}\right)\right]} \tag{7.29}
\end{equation*}
$$

Calculation of $p_{1}$ using (7.11b), which is based on the Miller-effect approximation, gives

$$
\begin{equation*}
p_{1}=-\frac{1}{\left[\left(R_{S}+r_{b}\right) \| r_{\pi}\right]\left[C_{\pi}+C_{\mu}\left(1+g_{m} R_{L}\right)\right]}=-\frac{1}{\left[\left(R_{S}+r_{b}\right) \| r_{\pi}\right]\left(C_{\pi}+C_{M}\right)} \tag{7.30}
\end{equation*}
$$

where

$$
\begin{equation*}
C_{M}=C_{\mu}\left(1+g_{m} R_{L}\right) \tag{7.31}
\end{equation*}
$$

is the Miller capacitance. Equation 7.30 gives virtually the same $p_{1}$ as (7.29) if $R_{L} / R \ll$ $\left(1+g_{m} R_{L}\right)$, which is usually true. This result shows that the Miller approximation is useful for finding the dominant pole. From (7.27), the nondominant pole is given by

$$
\begin{equation*}
p_{2}=-\left(\frac{1}{R_{L} C_{\mu}}+\frac{1}{R C_{\pi}}+\frac{1}{R_{L} C_{\pi}}+\frac{g_{m}}{C_{\pi}}\right) \tag{7.32}
\end{equation*}
$$

The last term of (7.32) is $g_{m} / C_{\pi}>g_{m} /\left(C_{\pi}+C_{\mu}\right)=\omega_{T}$ and thus $\left|p_{2}\right|>\omega_{T}$. (Recall that $\omega_{T}$ is the transition frequency for the transistor, as defined in Chapter 1.) Consequently, $\left|p_{2}\right|$ is a very high frequency; therefore, $\left|p_{1}\right|$ is almost always much less than $\left|p_{2}\right|$, as assumed. In the $s$ plane, the poles of the amplifier are thus widely separated, as shown in Fig. 7.7.

#### EXAMPLE

Using the Miller approximation, calculate the $-3-\mathrm{dB}$ frequency of a common-emitter transistor stage using the following parameters:

$$
\begin{array}{cccc}
R_{S}=1 \mathrm{k} \Omega & r_{b}=200 \Omega & I_{C}=1 \mathrm{~mA} & \beta_{0}=100 \\
f_{T}=400 \mathrm{MHz}\left(\text { at } I_{C}=1 \mathrm{~mA}\right) & C_{\mu}=0.5 \mathrm{pF} & R_{L}=5 \mathrm{k} \Omega
\end{array}
$$

The transistor small-signal parameters are

$$
\begin{gathered}
r_{\pi}=\frac{\beta_{0}}{g_{m}}=100 \times 26 \Omega=2.6 \mathrm{k} \Omega \\
\tau_{T}=\frac{1}{2 \pi f_{T}}=398 \mathrm{ps}
\end{gathered}
$$

Using (1.129) gives

$$
C_{\pi}+C_{\mu}=g_{m} \tau_{T}=\left(\frac{1 \mathrm{~mA}}{26 \mathrm{mV}}\right) 398 \mathrm{ps}=15.3 \mathrm{pF}
$$

Thus

$$
C_{\pi}=14.8 \mathrm{pF}
$$

Substitution of data in (7.31) gives for the Miller capacitance

$$
C_{M}=\left(1+g_{m} R_{L}\right) C_{\mu}=\left(1+\frac{1 \mathrm{~mA}}{26 \mathrm{mV}}(5 \mathrm{k} \Omega)\right)(0.5 \mathrm{pF})=96.7 \mathrm{pF}
$$

This term is much greater than $C_{\pi}$ and dominates the frequency response. Substitution of values in (7.30) gives

$$
f_{-3 \mathrm{~dB}}=\frac{\left|p_{1}\right|}{2 \pi}=\frac{1}{2 \pi} \frac{1000+200+2600}{(1000+200) 2600} \frac{10^{12}}{14.8+96.7}=1.74 \mathrm{MHz}
$$

For comparison, using (7.29) gives $\left|p_{1}\right|=10.7 \mathrm{Mrad} / \mathrm{s}$ and $f_{-3 \mathrm{~dB}}=1.70 \mathrm{MHz}$, which is in close agreement with the value using the Miller effect. The low-frequency gain can be calculated from (7.28) as

$$
\left.\frac{v_{o}}{v_{i}}\right|_{\omega=0}=-g_{m} R_{L} \frac{r_{\pi}}{R_{S}+r_{b}+r_{\pi}}=-\frac{5000}{26} \frac{2.6}{5+0.2+2.6}=-64.1
$$

The gain magnitude at low frequency is thus 36.1 dB and the gain versus frequency on log scales is plotted in Fig. 7.8 for frequencies below and slightly above $\left|p_{1}\right|$.
image_name:Figure 7.8
description:The graph in Figure 7.8 is a Bode plot representing the gain magnitude |A<sub>dm</sub>| in decibels (dB) versus frequency in hertz (Hz) for a circuit. The x-axis is labeled with frequency, ranging from 10<sup>3</sup> Hz to 10<sup>9</sup> Hz on a logarithmic scale, while the y-axis represents the gain magnitude in dB, ranging from 0 to 40 dB.

At low frequencies, the gain is constant at approximately 36.1 dB. This flat region extends up to a frequency of about 1.74 MHz, which is marked on the graph as a significant point. Beyond this frequency, the gain begins to decrease at a rate of -6 dB per octave, indicating a single-pole roll-off characteristic typical of many amplifier circuits.

The graph is annotated with a dashed horizontal line at 36.1 dB, indicating the low-frequency gain level, and a vertical dashed line at 1.74 MHz, highlighting the cutoff frequency where the gain starts to drop. The slope of the roll-off is also marked as -6 dB/octave, showing the rate of decrease in gain with increasing frequency beyond the cutoff point.

Overall, the graph illustrates a typical low-pass filter response with a flat passband and a gradual attenuation of gain at higher frequencies.

Figure 7.8 Gain magnitude versus frequency for the circuit in Fig. 7.3 using typical bipolar transistor data.
image_name:Figure 7.9 MOS differential amplifier circuit
description:
[
name: M0, type: NMOS, ports: {S: s0s1, D: d0, G: g0}
name: M1, type: NMOS, ports: {S: s0s1, D: d1, G: g1}
name: RS, type: Resistor, value: RS, ports: {N1: Vip, N2: g0}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: g1}
name: RL, type: Resistor, value: RL, ports: {N1: VDD, N2: d0}
name: RL, type: Resistor, value: RL, ports: {N1: VDD, N2: d1}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: s0s1, Nn: GND}
]
extrainfo:The circuit is a MOS differential amplifier with resistive loads. It features two NMOS transistors (M0 and M1) with a common source connection at node s0s1. The differential input is applied at nodes Vip and Vin, while the differential output is taken from nodes Vop and Von. The resistors RL provide load resistance, and the current source ISS establishes the bias current. The circuit operates between VDD and VSS power supplies.

Figure 7.9 MOS differential amplifier circuit.

#### 7.2.1.2 The MOS Differential Amplifier: Differential-Mode Gain

A MOS differential amplifier with resistive loads is shown in Fig. 7.9. The differential-mode (DM) ac half-circuit and the corresponding small-signal circuit are shown in Figs. 7.10a and $7.10 b$, respectively. For compactness, the factor of $1 / 2$ has been omitted from the input and output voltages in Fig. 7.10b, but this change does not alter the analysis in any way. This circuit is a common-source amplifier. The $g_{m b}$ generator and source-body capacitance $C_{s b}$ are not shown; they have no effect because $v_{b s}=0$ here. For simplicity, the drain-body capacitance $C_{d b}$ of the transistor has been omitted. Since this capacitance would be connected in parallel with $R_{L}$, its effect could be handled in the following analysis by replacing $R_{L}$ with $Z_{L}$, where $Z_{L}$ equals $R_{L}$ in parallel with $C_{d b}$. For simplicity, the gate-body capacitance $C_{g b}$ is ignored. It could be included by simply adding it to $C_{g s}$ since $C_{g b}$ appears in parallel with $C_{g s}$ in the common-source amplifier. However, usually $C_{g s} \gg C_{g b}$, so $C_{g s}+C_{g b} \approx C_{g s}$. The analysis of this ac circuit applies to this DM half-circuit as well as any single-stage common-source amplifier of the form shown in Fig. 7.10a. The small-signal circuit in Fig. 7.10b is the same as the circuit in Fig. $7.2 c$ if we rename the model parameters as listed in Table 7.1. Therefore, we can use the results of the analysis of Fig. 7.2c. Substituting the values from the third column in Table 7.1 in (7.19), the exact transfer function is given by

$$
\begin{equation*}
\frac{v_{o}}{v_{i}}=-\frac{g_{m} R_{L}\left(1-s \frac{C_{g d}}{g_{m}}\right)}{1+s\left(C_{g d} R_{L}+C_{g d} R_{S}+C_{g s} R_{S}+g_{m} R_{L} R_{S} C_{g d}\right)+s^{2} R_{L} R_{S} C_{g d} C_{g s}} \tag{7.33}
\end{equation*}
$$

Using (7.25), the dominant pole is given by

$$
\begin{equation*}
p_{1}=-\frac{1}{R_{S}\left[C_{g s}+C_{g d}\left(1+g_{m} R_{L}+\frac{R_{L}}{R_{S}}\right)\right]} \tag{7.34}
\end{equation*}
$$

Calculation of $p_{1}$ using (7.11b), which is based on the Miller-effect approximation, gives

$$
\begin{equation*}
p_{1} \approx-\frac{1}{R_{S}\left[C_{g s}+C_{g d}\left(1+g_{m} R_{L}\right)\right]}=-\frac{1}{R_{S}\left(C_{g s}+C_{M}\right)} \tag{7.35}
\end{equation*}
$$

image_name:Figure 7.10 (a)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: vi/2, N2: g0}
name: RL, type: Resistor, value: RL, ports: {N1: vo/2, N2: GND}
name: M0, type: NMOS, ports: {S: GND, D: vo, G: g0}
]
extrainfo:The circuit is a differential-mode AC half-circuit with a small-signal equivalent circuit. It includes an NMOS transistor with gate node g0, drain node vo, and source node connected to ground. The circuit models the Miller effect with capacitors Cgs and Cgd. The current source g_mV1 represents the transconductance effect of the NMOS.
image_name:Figure 7.10 (b)
description:
[
name: vi, type: VoltageSource, value: vi, ports: {Np: Vi, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vi, N2: g0}
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: g0, Nn: GND}
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: Vo, Nn: g0}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
name: gmv1, type: VoltageControlCurrentSource, ports: {Np: V0, Nn: GND}
]
extrainfo:The circuit is a small-signal equivalent circuit for a differential-mode AC half-circuit. It includes an NMOS transistor with gate connected to the node 'g0', drain connected to 'Vo', and source connected to ground. The circuit also features Miller capacitance effect represented by Cgd.

Figure 7.10 (a) Differential-mode ac half-circuit for Fig. 7.9. (b) Small-signal equivalent circuit for (a).
where

$$
\begin{equation*}
C_{M}=C_{g d}\left(1+g_{m} R_{L}\right) \tag{7.36}
\end{equation*}
$$

is the Miller capacitance. Equation 7.35 gives nearly the same value for $p_{1}$ as (7.34) if $R_{L} / R_{S} \ll\left(1+g_{m} R_{L}\right)$, which shows that the Miller approximation is useful for finding the dominant pole. From (7.27), the nondominant pole is given by

$$
\begin{equation*}
p_{2}=-\left(\frac{1}{R_{L} C_{g d}}+\frac{1}{R_{S} C_{g s}}+\frac{1}{R_{L} C_{g s}}+\frac{g_{m}}{C_{g s}}\right) \tag{7.37}
\end{equation*}
$$

The last term of (7.37) is $g_{m} / C_{g s}>g_{m} /\left(C_{g s}+C_{g d}+C_{g b}\right)=\omega_{T}$ and thus $\left|p_{2}\right|>\omega_{T}$. (Recall that $\omega_{T}$ is the transition frequency for the transistor, as defined in Chapter 1.) Consequently, $\left|p_{2}\right|$ is a very high frequency; therefore, $\left|p_{1}\right|$ is almost always much less than $\left|p_{2}\right|$. In the $s$ plane, the poles of the amplifier are thus widely separated, as shown in Fig. 7.7.

#### EXAMPLE

Using the Miller approximation, calculate the $-3-\mathrm{dB}$ frequency of a common-source transistor stage using the following parameters:

$$
\begin{gathered}
R_{S}=1 \mathrm{k} \Omega \quad I_{D}=1 \mathrm{~mA} \quad k^{\prime} \frac{W}{L}=100 \frac{\mathrm{~mA}}{\mathrm{~V}^{2}} \\
f_{T}=400 \mathrm{MHz}\left(\text { at } I_{D}=1 \mathrm{~mA}\right) \quad C_{g d}=0.5 \mathrm{pF} \quad C_{g b}=0 \quad R_{L}=5 \mathrm{k} \Omega
\end{gathered}
$$

The small-signal transconductance is

$$
g_{m}=\sqrt{2\left(100 \frac{\mathrm{~mA}}{\mathrm{~V}^{2}}\right)(1 \mathrm{~mA})}=14.1 \frac{\mathrm{~mA}}{\mathrm{~V}}
$$

Using (1.207) from Chapter 1 and $C_{g b}=0$ gives

$$
C_{g s}+C_{g d}=\frac{g_{m}}{\omega_{T}}=\frac{14.1 \mathrm{~mA} / \mathrm{V}}{2 \pi(400 \mathrm{MHz})}=5.6 \mathrm{pF}
$$

Thus

$$
C_{g s}=5.6 \mathrm{pF}-C_{g d}=5.1 \mathrm{pF}
$$

Substitution of data in (7.36) gives for the Miller capacitance

$$
C_{M}=\left(1+g_{m} R_{L}\right) C_{g d}=\left[1+\left(14.1 \frac{\mathrm{~mA}}{\mathrm{~V}}\right)(5 \mathrm{k} \Omega)\right](0.5 \mathrm{pF})=35.7 \mathrm{pF}
$$

This capacitance is much greater than $C_{g s}$ and dominates the frequency response. Substitution of values in (7.35) gives

$$
f_{-3 \mathrm{~dB}}=\frac{\left|p_{1}\right|}{2 \pi}=\frac{1}{2 \pi} \frac{1}{(1000 \Omega)(5.1 \mathrm{pF}+35.7 \mathrm{pF})}=3.9 \mathrm{MHz}
$$

For comparison, using (7.34) gives $\left|p_{1}\right|=23.1 \mathrm{Mrad} / \mathrm{s}$ and $f_{-3 \mathrm{~dB}}=3.7 \mathrm{MHz}$, which is close to the result using the Miller effect. The low-frequency gain can be calculated from (7.33) as

$$
\left.\frac{v_{o}}{v_{i}}\right|_{\omega=0}=-g_{m} R_{L}=-\left(14.1 \frac{\mathrm{~mA}}{\mathrm{~V}}\right)(5000 \Omega)=-70.5
$$

### 7.2.2 Frequency Response of the Common-Mode Gain for a Differential Amplifier

In Chapter 3, the importance of the common-mode (CM) gain of a differential amplifier was described. It was shown that low values of CM gain are desirable so that the circuit can reject undesired signals that are applied equally to both inputs. Because undesired CM signals may have high-frequency components, the frequency response of the CM gain is important. The CM frequency response of the differential circuits in Figures 7.5 and 7.9 can be calculated from the CM half-circuits shown in Figs. 7.11a and 7.11b. In Fig. 7.11, $R_{T}$ and $C_{T}$ are the equivalent output resistance and capacitance of the tail current source. Since impedances common to the two devices are doubled in the CM half-circuit, $R_{T}$ and $C_{T}$ become $2 R_{T}$ and $C_{T} / 2$, respectively. A general small-signal equivalent circuit for Fig. 7.11a-b is shown in Fig. 7.11c. The parallel combination of $2 R_{T}$ and $C_{T} / 2$ will be referred to as $Z_{T}$.

The complete analysis of Fig. 7.11c is quite complex. However, the important aspects of the frequency response can be calculated by making some approximations. Consider the time constant $R_{T} C_{T}$. The resistance $R_{T}$ is the output resistance of the current source and is usually greater than or equal to the $r_{o}$ of a transistor. Let us assume that this resistance is on the order of $1 \mathrm{M} \Omega$. The capacitor $C_{T}$ includes $C_{c s}$ of the bipolar current-source transistor or $C_{d b}$ of the current-source transistor plus $C_{s b}$ of the input transistors in the MOS circuit. Typically, $C_{T}$ is 1 pF or less. Using $R_{T}=1 \mathrm{M} \Omega$ and $C_{T}=1 \mathrm{pF}$, the time constant $R_{T} C_{T}$ is $1 \mu \mathrm{~s}$, and the break frequency corresponding to this time constant is $1 /\left(2 \pi R_{T} C_{T}\right)=166 \mathrm{kHz}$. Below this frequency the impedance $Z_{T}$ is dominated by $R_{T}$, and above this frequency $C_{T}$ dominates. Thus as the frequency of operation is increased, the impedance $Z_{T}$ will exhibit frequency variation before the rest of the circuit. We now calculate the frequency response assuming
image_name:(a)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: vic, N2: bo}
name: RL, type: Resistor, value: RL, ports: {N1: voc, N2: GND}
name: RT, type: Resistor, value: 2RT, ports: {N1: eo, N2: GND}
name: CT, type: Capacitor, value: CT/2, ports: {Np: eo, Nn: GND}
name: M0, type: NMOS, ports: {S: eo, D: voc, G: bo}
name: vic, type: VoltageSource, value: vic, ports: {Np: vic, Nn: GND}
]
extrainfo:The circuit diagram (a) represents a common-mode ac half-circuit. It includes a voltage source vic, resistors RS, RL, and 2RT, a capacitor CT/2, and an NMOS transistor M0. The circuit is grounded at multiple points, and the output voltage voc is across RL.
image_name:(b)
description:
[
name: M0, type: NMOS, ports: {S: s0, D: voc, G: g0}
name: RS, type: Resistor, value: RS, ports: {N1: vic, N2: g0}
name: RL, type: Resistor, value: RL, ports: {N1: voc, N2: GND}
name: RT, type: Resistor, value: 2RT, ports: {N1: s0, N2: GND}
name: CT, type: Capacitor, value: CT/2, ports: {Np: s0, Nn: GND}
name: vic, type: VoltageSource, value: vic, ports: {Np: vic, Nn: GND}
]
extrainfo:The circuit is a common-mode AC half-circuit with an NMOS transistor used to analyze frequency response. The impedance Z_T is affected by the resistor R_T and capacitor C_T, influencing the common-mode gain. The key nodes include the input vic, the gate of the NMOS g0, the drain voc, and the source connected to ground.
image_name:(c)
description:
[
name: vic, type: VoltageSource, ports: {Np: vic, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: vic, N2: RSrx}
name: rx, type: Resistor, value: rx, ports: {N1: RSrx, N2: x2}
name: rin(v1), type: Resistor, value: rin, ports: {N1: x2, N2: X1}
name: Cin, type: Capacitor, value: Cin, ports: {Np: x2, Nn: X1}
name: Cf, type: Capacitor, value: Cf, ports: {Np: X2, Nn: voc}
name: RL, type: Resistor, value: RL, ports: {N1: voc, N2: GND}
name: g_m*v1, type: VoltageControlledCurrentSource, ports: {Np: X1, Nn: voc}
name: RT, type: Resistor, value: 2RT, ports: {N1: X1, N2: GND}
name: CT, type: Capacitor, value: CT/2, ports: {Np: X1, Nn: GND}
]
extrainfo:The circuit diagram (c) represents a common-mode ac half-circuit with a voltage source vic driving the circuit. The circuit includes resistors RS, rx, rin, and RL, capacitors Cin, Cf, and CT, and a voltage-controlled current source g_m*v1. The circuit is grounded at multiple points and includes nodes X1 and X2 for interconnections. The resistor RT and capacitor CT form a parallel RC network connected to ground.

Figure 7.11 (a) Common-mode ac half-circuit for Fig. 7.5. (b) Common-mode ac half-circuit for Fig. 7.9. (c) A general model for both half-circuits.
that $C_{T}$ is the only significant capacitance. Since the impedance $Z_{T}$ is high, almost all of $v_{i c}$ appears across $Z_{T}$ if $R_{S}$ is small. Therefore, we can approximate the CM gain as

$$
\begin{equation*}
A_{c m}=\frac{v_{o c}}{v_{i c}} \approx-\frac{R_{L}}{Z_{T}} \tag{7.38}
\end{equation*}
$$

where

$$
\begin{equation*}
Z_{T}=\frac{2 R_{T}}{1+s C_{T} R_{T}} \tag{7.39}
\end{equation*}
$$

Substitution of (7.39) in (7.38) gives

$$
\begin{equation*}
A_{c m}(s)=\frac{v_{o c}}{v_{i c}}(s) \approx-\frac{R_{L}}{2 R_{T}}\left(1+s C_{T} R_{T}\right) \tag{7.40}
\end{equation*}
$$

Equation 7.40 shows that the CM gain expression contains a zero, which causes the CM gain to rise at $6 \mathrm{~dB} /$ octave above a frequency $\omega=1 / R_{T} C_{T}$. This behavior is undesirable because the CM gain should ideally be as small as possible. The increase in CM gain cannot continue indefinitely, however, because the other capacitors in the circuit of Fig. 7.11c eventually become important. The other capacitors cause the CM gain to fall at very high frequencies, and this behavior is shown in the plot of CM gain versus frequency in Fig. 7.12a.
image_name:(a)
description:The graph labeled "(a)" is a Bode plot showing the common-mode (CM) gain \( |A_{cm}| \) in decibels (dB) plotted against frequency \( f \) on a logarithmic scale. The vertical axis represents the gain in dB, and the horizontal axis represents frequency in a logarithmic scale.

Overall Behavior and Trends:
- **Low Frequencies:** At low frequencies, the CM gain starts at a relatively low value and remains flat, indicating a constant gain.
- **Mid Frequencies:** As the frequency increases, starting from \( \omega = \frac{1}{R_T C_T} \), the CM gain begins to rise at a rate of +6 dB/octave. This indicates that the gain is increasing logarithmically with frequency.
- **High Frequencies:** At very high frequencies, the rise in gain does not continue indefinitely. The graph shows a peak followed by a downward trend, suggesting that other capacitive effects in the circuit cause the gain to eventually decrease.

Key Features and Technical Details:
- The plot indicates a critical frequency at \( \omega = \frac{1}{R_T C_T} \), marked by a vertical dashed line. This is where the gain begins to rise.
- The slope of +6 dB/octave is clearly marked on the graph, showing the rate of increase in the mid-frequency range.
- At very high frequencies, the gain starts to fall, indicating the influence of other capacitors in the circuit, though specific slopes or rates of decrease are not annotated.

Annotations and Specific Data Points:
- A specific point on the frequency axis is labeled \( \frac{1}{2\pi R_T C_T} \), marking the frequency where the gain begins to rise.

This graph provides insight into the undesirable rise in CM gain with frequency and highlights the frequency-dependent behavior of the differential amplifier's common-mode gain.
image_name:(b)
description:The graph labeled (b) is a Bode plot of the differential-mode gain (|A_dm|) in decibels (dB) versus frequency (f) on a logarithmic scale. The y-axis represents the differential-mode gain in dB, while the x-axis represents frequency in a log scale.

Overall Behavior and Trends:
- The plot starts with a flat response, indicating a constant differential-mode gain over a range of frequencies.
- At a specific frequency, denoted as \( \frac{1}{2\pi RC_t} \), the gain begins to decrease.
- The slope of the decrease is -6 dB/octave, indicating a linear decline on the logarithmic scale.

Key Features and Technical Details:
- The critical frequency \( \frac{1}{2\pi RC_t} \) marks the point where the gain starts to fall off. This is a significant transition point in the graph.
- The initial flat section represents the bandwidth over which the differential-mode gain is constant before the roll-off.

Annotations and Specific Data Points:
- The graph is annotated with a dashed line showing the -6 dB/octave slope, providing a visual guide to the rate of decrease in gain.
- A marker at the frequency \( \frac{1}{2\pi RC_t} \) highlights the onset of the gain reduction.

This graph is important for understanding how the differential-mode gain of the circuit behaves across different frequencies, particularly how it maintains a constant gain up to a certain point before decreasing at higher frequencies.
image_name:(c)
description:The graph labeled (c) is a Bode plot depicting the variation of the Common-Mode Rejection Ratio (CMRR) in decibels (dB) with respect to frequency on a logarithmic scale.

Axes Labels and Units:
- **Y-axis (Vertical):** CMRR in dB
- **X-axis (Horizontal):** Frequency (f) in hertz, presented on a logarithmic scale

Overall Behavior and Trends:
The CMRR starts at a certain level and decreases as frequency increases. Initially, the CMRR decreases at a rate of \(-6 \text{ dB/octave}\). As the frequency continues to rise, the slope of the curve becomes steeper, decreasing at \(-12 \text{ dB/octave}\).

Key Features and Technical Details:
- **Initial Slope:** The CMRR decreases at \(-6 \text{ dB/octave}\) until reaching a critical frequency.
- **Transition Point:** At the frequency \(\frac{1}{2\pi RC_t}\), the slope changes, and the CMRR begins to decrease more steeply at \(-12 \text{ dB/octave}\).

Annotations and Specific Data Points:
- The critical frequency \(\frac{1}{2\pi RC_t}\) is marked on the graph, indicating the point where the slope changes.
- The graph clearly shows the transition between the two regions of different slopes, providing insight into the behavior of the differential amplifier's CMRR over a range of frequencies.

Figure 7.12 Variation with frequency of the gain parameters for the differential amplifier in Fig. 7.5 or Fig. 7.9.
(a) Common-mode gain. (b) Differential-mode gain. (c) Common-mode rejection ratio.

The differential-mode (DM) gain $A_{d m}$ of the circuit of Fig. 7.5 or Fig. 7.9 is plotted versus frequency in Fig. $7.12 b$ using (7.10). As described earlier, $\left|A_{d m}\right|$ begins to fall off at a frequency given by $f=1 / 2 \pi R C_{t}$, where $R=\left(R_{S}+r_{x}\right) \| r_{\text {in }}$ and $C_{t}=C_{\text {in }}+C_{M}$. As pointed out in Chapter 3, an important differential amplifier parameter is the common-mode rejection ratio (CMRR) defined as

$$
\begin{equation*}
\mathrm{CMRR}=\frac{\left|A_{d m}\right|}{\left|A_{c m}\right|} \tag{7.41}
\end{equation*}
$$

The CMRR is plotted as a function of frequency in Fig. $7.12 c$ by simply taking the magnitude of the ratio of the DM and CM gains. This quantity begins to decrease at frequency $f=1 / 2 \pi R_{T} C_{T}$ when $\left|A_{c m}\right|$ begins to increase. The rate of decrease of CMRR further increases when $\left|A_{d m}\right|$ begins to fall with increasing frequency. Thus differential amplifiers are far less able to reject CM signals as the frequency of those signals increases.

### 7.2.3 Frequency Response of Voltage Buffers

Single-stage voltage buffers are often used in integrated circuits. The ac circuits for bipolar and MOS voltage buffers are shown in Figs. 7.13a and 7.13b, respectively. A small-signal model
image_name:(a)
description:
[
name: vi, type: VoltageSource, value: vi, ports: {Np: Vi, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vi, N2: b0}
name: M0, type: NMOS, ports: {S: V0, D: GND, G: b0}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is an emitter-follower amplifier with a voltage source vi, a resistor RS connected to the gate of NMOS M0, and a load resistor RL at the output Vo.
image_name:(b)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vi, N2: g0}
name: M0, type: NMOS, ports: {S: GND, D: Vo, G: g0}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is an NMOS source-follower amplifier with input voltage Vi, source resistor RS, load resistor RL, and output voltage Vo. The NMOS transistor M0 is used to buffer the input signal.
image_name:(c)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vi, N2: X1}
name: rx, type: Resistor, value: rx, ports: {N1: X1, N2: X2}
name: rin, type: Resistor, value: rin, ports: {N1: X1, N2: X2}
name: Cin, type: Capacitor, value: Cin, ports: {Np: X2, Nn: X1}
name: gmv1, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: X1}
]
extrainfo:The circuit is a small-signal model of a voltage buffer with input voltage Vi and output at node X1. The voltage-controlled current source gmv1 is dependent on the voltage across Cin.

Figure 7.13 (a) An ac schematic of an emitter-follower amplifier. (b) An ac schematic of a source-follower amplifier. (c) A general model for both amplifiers.
that can be used to model both of these circuits is shown in Fig. 7.13c. Resistance $R_{S}$ is the source resistance, and $R_{L}$ is the load resistance. We will assume that the output resistance of the transistor $r_{o}$ is much larger than $R_{L}$. Since these resistors are in parallel in the small-signal circuit, $r_{o}$ can be neglected. The series input resistance in the transistor model and the source resistance are in series and can be lumped together as $R_{S}^{\prime}=R_{S}+r_{x}$. For simplicity, the effect of capacitor $C_{f}$ in Fig. 7.1 is initially neglected, a reasonable approximation if $R_{S}^{\prime}$ is small. The effect of $C_{f}$ is to form a low-pass circuit with $R_{S}^{\prime}$ and to cause the gain to decrease at very high frequencies. From Fig. 7.13c,

$$
\begin{gather*}
v_{i}=i_{i} R_{S}^{\prime}+v_{1}+v_{o}  \tag{7.42}\\
i_{i}=\frac{v_{1}}{z_{\text {in }}}  \tag{7.43}\\
z_{\text {in }}=\frac{r_{\text {in }}}{1+s C_{\text {in }} r_{\text {in }}}  \tag{7.44}\\
i_{i}+g_{m} v_{1}=\frac{v_{o}}{R_{L}} \tag{7.45}
\end{gather*}
$$

Using (7.43) and (7.44) in (7.45) gives

$$
\frac{v_{1}}{r_{\mathrm{in}}}\left(1+s C_{\mathrm{in}} r_{\mathrm{in}}\right)+g_{m} v_{1}=\frac{v_{o}}{R_{L}}
$$

and thus

$$
\begin{equation*}
v_{1}=\frac{v_{o}}{R_{L}} \frac{1}{g_{m}+\frac{1}{r_{\text {in }}}\left(1+s C_{\text {in }} r_{\text {in }}\right)} \tag{7.46}
\end{equation*}
$$

Using (7.46) and (7.43) in (7.42) gives

$$
v_{i}=\left(\frac{R_{S}^{\prime}}{z_{\text {in }}}+1\right) \frac{v_{o}}{R_{L}} \frac{1}{g_{m}+\frac{1}{r_{\text {in }}}\left(1+s C_{\text {in }} r_{\text {in }}\right)}+v_{o}
$$

Collecting terms in this equation, we find

$$
\begin{equation*}
\frac{v_{o}}{v_{i}}=\frac{g_{m} R_{L}+\frac{R_{L}}{r_{\text {in }}}}{1+g_{m} R_{L}+\frac{R_{S}^{\prime}+R_{L}}{r_{\text {in }}}}\left[\frac{1-\frac{s}{z_{1}}}{1-\frac{s}{p_{1}}}\right] \tag{7.47}
\end{equation*}
$$

where

$$
\begin{gather*}
z_{1}=-\frac{g_{m}+\frac{1}{r_{\mathrm{in}}}}{C_{\mathrm{in}}}  \tag{7.48}\\
p_{1}=-\frac{1}{R_{1} C_{\mathrm{in}}} \tag{7.49}
\end{gather*}
$$

with

$$
\begin{equation*}
R_{1}=r_{\text {in }} \| \frac{R_{S}^{\prime}+R_{L}}{1+g_{m} R_{L}} \tag{7.50}
\end{equation*}
$$

Equation 7.47 shows that, as expected, the low-frequency voltage gain is about unity if $g_{m} R_{L} \gg 1$ and $g_{m} R_{L} \gg\left(R_{S}^{\prime}+R_{L}\right) / r_{\text {in }}$. The high-frequency gain is controlled by the presence of a pole at $p_{1}$ and a zero at $z_{1}$.

#### 7.2.3.1 Frequency Response of the Emitter Follower

The small-signal circuit for the emitter follower in Fig. 7.13a is shown in Fig. 7.14. We initially ignore $C_{\mu}$, as in the general analysis in Section 7.2.3. The transfer function for the emitter follower can be found by substituting the appropriate values in Table 7.1 into (7.47) through
image_name:Figure 7.14
description:
[
name: vi, type: VoltageSource, value: vi, ports: {Np: Vi, Nn: GND}
name: "RS", type: Resistor, value: "RS", ports: {N1: Vi, N2: "B"}
name: rπ, type: Resistor, value: rπ, ports: {N1: "B", N2: Vo}
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: "B", Nn: Vo}
name: gmv1, type: CurrentSource, value: gmv1, ports: {Np: C, Nn: Vo}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND'}
]
extrainfo:The circuit is a small-signal model of an emitter follower. It consists of a voltage source, resistors, a capacitor, and a current source. The input is at node Vi, and the output is taken across RL at node Vo. The current source gmv1 models the transconductance of the transistor, and the capacitor Cπ represents the parasitic capacitance.

Figure 7.14 Small-signal model for the emitter follower in Fig. 7.13a.
(7.50). If $g_{m} R_{L} \gg 1$ and $g_{m} R_{L} \gg\left(R_{S}^{\prime}+R_{L}\right) / r_{\pi}$, where $R_{S}^{\prime}=R_{S}+r_{b}$, the low-frequency gain is about unity. The zero and pole are given by

$$
\begin{gather*}
z_{1}=-\frac{g_{m}+\frac{1}{r_{\pi}}}{C_{\pi}} \approx-\frac{g_{m}}{C_{\pi}} \approx-\omega_{T}  \tag{7.51}\\
p_{1}=-\frac{1}{C_{\pi} R_{1}} \tag{7.52}
\end{gather*}
$$

where

$$
\begin{equation*}
R_{1}=r_{\pi} \| \frac{R_{S}^{\prime}+R_{L}}{1+g_{m} R_{L}} \tag{7.53}
\end{equation*}
$$

Typically, the zero has a magnitude that is slightly larger than the pole, and both are approximately equal to $\omega_{T}$ of the device. In particular, if $g_{m} R_{L} \gg 1$ and $R_{S}^{\prime} \ll R_{L}$ in (7.53), then $R_{1} \approx 1 / g_{m}$ and (7.52) gives $p_{1} \approx-g_{m} / C_{\pi} \approx-\omega_{T}$. However, if $R_{S}$ is large, then $R_{S}^{\prime}$ in (7.53) becomes large compared to $R_{L}$, and the pole magnitude will be significantly less than $\omega_{T}$.

#### EXAMPLE

Calculate the transfer function for an emitter follower with $C_{\pi}=10 \mathrm{pF}, C_{\mu}=0, R_{L}=2 \mathrm{k} \Omega$, $R_{S}=50 \Omega, r_{b}=150 \Omega, \beta=100$, and $I_{C}=1 \mathrm{~mA}$.

From the data, $g_{m}=38 \mathrm{~mA} / \mathrm{V}, r_{\pi}=2.6 \mathrm{k} \Omega$, and $R_{S}^{\prime}=R_{S}+r_{b}=200 \Omega$. Since $C_{\mu}=0$, $\omega_{T}$ of the device is

$$
\begin{equation*}
\omega_{T}=\frac{g_{m}}{C_{\pi}}=\frac{1 \mathrm{~mA}}{26 \mathrm{mV}} \frac{1}{10 \mathrm{pF}}=3.85 \times 10^{9} \mathrm{rad} / \mathrm{s} \tag{7.54}
\end{equation*}
$$

and thus $f_{T}=612 \mathrm{MHz}$. From (7.51) and (7.54), the zero of the transfer function is

$$
z_{1} \approx-\omega_{T}=-3.85 \times 10^{9} \mathrm{rad} / \mathrm{s}
$$

From (7.53)

$$
R_{1}=2.6 \mathrm{k} \Omega \|\left(\frac{200+2000}{1+\frac{2000}{26}} \Omega\right) \approx 28 \Omega
$$

Using (7.52), the pole is

$$
p_{1}=-\frac{10^{12}}{10} \frac{1}{28} \mathrm{rad} / \mathrm{s}=-3.57 \times 10^{9} \mathrm{rad} / \mathrm{s}
$$

The pole and zero are thus quite closely spaced, as shown in the $s$-plane plot of Fig. 7.15a.
The low-frequency gain of the circuit from (7.47) is

$$
\frac{v_{o}}{v_{i}}=\frac{g_{m} R_{L}+\frac{R_{L}}{r_{\pi}}}{1+g_{m} R_{L}+\frac{R_{S}^{\prime}+R_{L}}{r_{\pi}}}=\frac{\frac{2000}{26}+\frac{2000}{2600}}{1+\frac{2000}{26}+\frac{2200}{2600}}=0.986
$$

The parameters derived above are used in (7.47) to plot the circuit gain versus frequency in Fig. 7.15b. The gain is flat with frequency until near $f_{T}=612 \mathrm{MHz}$ where a decrease of 0.4 dB occurs. The analysis predicts that the gain is then flat as frequency is increased further.
image_name:Figure 7.15 (a)
description:The graph in Figure 7.15 (a) is a pole-zero plot on the complex plane, typically used in control systems and signal processing to represent the poles and zeros of a system's transfer function.

**Type of Graph:** Pole-zero plot.

**Axes Labels and Units:**
- The horizontal axis, labeled as \( \sigma \), represents the real part of the complex frequency, measured in units of \( \times 10^9 \) rad/s.
- The vertical axis, labeled as \( j\omega \), represents the imaginary part of the complex frequency.

**Overall Behavior and Trends:**
- The plot shows the locations of poles and zeros of the system in the complex plane.
- There is one zero located on the real axis at approximately -2 (\( \times 10^9 \) rad/s).
- There is one pole located further left on the real axis at approximately -4 (\( \times 10^9 \) rad/s).

**Key Features and Technical Details:**
- The presence of a pole on the left half of the complex plane indicates a stable system.
- The zero is positioned closer to the imaginary axis than the pole, which can affect the frequency response of the system.

**Annotations and Specific Data Points:**
- The zero is marked with an 'o', and the pole is marked with an 'x'.
- The plot does not include any annotations for gain or phase margins, as it focuses on the pole-zero configuration.
image_name:Figure 7.15 (b)
description:Figure 7.15 (b) is a Bode plot representing the voltage gain \( \frac{v_o}{v_i} \) in decibels (dB) versus frequency in Hertz (Hz) for a voltage buffer.

1. **Type of Graph and Function:**
- The graph is a Bode plot focusing on the gain response of a voltage buffer circuit.

2. **Axes Labels and Units:**
- The x-axis represents frequency \( f \) in Hertz (Hz), plotted on a logarithmic scale, ranging from 1 MHz to 1 GHz.
- The y-axis represents the voltage gain \( \frac{v_o}{v_i} \) in decibels (dB), with values ranging from 0 dB to -8 dB.

3. **Overall Behavior and Trends:**
- The gain is flat at 0 dB across the frequency range until approximately 612 MHz.
- Beyond this frequency, the gain starts to decrease slightly, showing a 0.4 dB drop.
- The gain remains flat again at higher frequencies after this initial drop.

4. **Key Features and Technical Details:**
- The cutoff frequency \( f_{-3dB} \) is marked at 725 MHz, where the gain drops to -3 dB.
- The solid line represents the gain with no parasitic capacitance \( C_{\mu} = 0 \) or \( C_{gd} = 0 \).
- The dashed line represents the gain with a parasitic capacitance \( C_{\mu} = 1 \) pF, showing a more realistic frequency response.

5. **Annotations and Specific Data Points:**
- The transition frequency \( f_T \) is noted at 612 MHz, indicating where the gain starts to decrease.
- The graph includes a horizontal dashed line at -3 dB to highlight the cutoff frequency.
- Annotations specify the conditions for both the solid and dashed lines, providing context for the changes in gain.

Figure 7.15 (a) Pole-zero plot for a voltage buffer. (b) Voltage gain versus frequency for the voltage buffer.

By inspecting Fig. 7.14 we can see that the high-frequency gain is asymptotic to $R_{L} /\left(R_{L}+R_{S}^{\prime}\right)$ since $C_{\pi}$ becomes a short circuit. This forces $v_{1}=0$ and thus the controlled current $g_{m} \nu_{1}$ is also zero. If a value of $C_{\mu}=1 \mathrm{pF}$ is included in the equivalent circuit, the more realistic dashed frequency response of Fig. $7.15 b$ is obtained. Since the collector is grounded, $C_{\mu}$ is connected from $B^{\prime}$ to ground and thus high-frequency signals are attenuated by voltage division between $R_{S}^{\prime}$ and $C_{\mu}$. As a result, the circuit has a $-3-\mathrm{dB}$ frequency of 725 MHz due to the low-pass action of $R_{S}^{\prime}$ and $C_{\mu}$. However, the bandwidth of the emitter follower is still quite large, and bandwidths of the order of the $f_{T}$ of the device can be obtained in practice.

The preceding considerations have shown that large bandwidths are available from the emitter-follower circuit. One of the primary uses of an emitter follower is as a voltage buffer circuit due to its high input impedance and low output impedance. The behavior of these terminal impedances as a function of frequency is thus significant, especially when driving large loads, and will now be examined.

In Chapter 3, the terminal impedances of the emitter follower were calculated using a circuit similar to that of Fig. $7.14 b$ except that $C_{\pi}$ was not included. The results obtained there can be used here if $r_{\pi}$ is replaced by $z_{\pi}$, which is a parallel combination of $r_{\pi}$ and $C_{\pi}$. In the low-frequency calculation, $\beta_{0}$ was used as a symbol for $g_{m} r_{\pi}$ and thus is now replaced by $g_{m} z_{\pi}$. Using these substitutions in (3.73) and (3.76), including $r_{b}$ and letting $r_{o} \rightarrow \infty$, we
obtain for the emitter follower

$$
\begin{gather*}
z_{i}=r_{b}+z_{\pi}+\left(g_{m} z_{\pi}+1\right) R_{L}  \tag{7.55}\\
z_{o}=\frac{z_{\pi}+R_{S}+r_{b}}{1+g_{m} z_{\pi}} \tag{7.56}
\end{gather*}
$$

where

$$
\begin{equation*}
z_{\pi}=\frac{r_{\pi}}{1+s C_{\pi} r_{\pi}} \tag{7.57}
\end{equation*}
$$

Consider first the input impedance. Substituting (7.57) in (7.55) gives

$$
\begin{align*}
z_{i} & =r_{b}+\frac{r_{\pi}}{1+s C_{\pi} r_{\pi}}+\left(\frac{g_{m} r_{\pi}}{1+s C_{\pi} r_{\pi}}+1\right) R_{L} \\
& =r_{b}+\frac{\left(1+g_{m} R_{L}\right) r_{\pi}}{1+s C_{\pi} r_{\pi}}+R_{L}  \tag{7.58}\\
& =r_{b}+\frac{\left(1+g_{m} R_{L}\right) r_{\pi}}{1+s \frac{C_{\pi}}{1+g_{m} R_{L}}\left(1+g_{m} R_{L}\right) r_{\pi}}+R_{L} \\
& =r_{b}+\frac{R}{1+s C R}+R_{L} \tag{7.59}
\end{align*}
$$

where

$$
\begin{equation*}
R=\left(1+g_{m} R_{L}\right) r_{\pi} \tag{7.59a}
\end{equation*}
$$

and

$$
\begin{equation*}
C=\frac{C_{\pi}}{1+g_{m} R_{L}} \tag{7.59b}
\end{equation*}
$$

Thus $z_{i}$ can be represented as a parallel R-C circuit in series with $r_{b}$ and $R_{L}$ as shown in Fig. 7.16. The effective input capacitance is $C_{\pi} /\left(1+g_{m} R_{L}\right)$ and is much less than $C_{\pi}$ for typical values of $g_{m} R_{L}$. The collector-base capacitance $C_{\mu}$ may dominate the input capacitance and can be added to this circuit from $B^{\prime}$ to ground. Thus, at high frequencies, the input impedance of the emitter follower becomes capacitive and its magnitude decreases.

The emitter-follower high-frequency output impedance can be calculated by substituting (7.57) in (7.56). Before proceeding, we will examine (7.57) to determine the high and low
image_name:Figure 7.16 Equivalent circuit for the input impedance of an emitter follower with C_{\mu}=0
description:
[
name: rb, type: Resistor, value: rb, ports: {N1: B, N2: "B"}
name: Cπ/(1+gmRL), type: Capacitor, value: Cπ/(1+gmRL), ports: {Np: "B", Nn: X1}
name: (1+gmRL)rπ, type: Resistor, value: (1+gmRL)rπ, ports: {N1: "B", N2: X1}
name: RL, type: Resistor, value: RL, ports: {N1: X1, N2: GND'}
]
extrainfo:This circuit represents the input impedance of an emitter follower with Cμ=0. The input impedance is characterized by a resistor rb in series with a parallel combination of a capacitor and a resistor, both connected to a load resistor RL.

Figure 7.16 Equivalent circuit for the input impedance of an emitter follower with $C_{\mu}=0$.
frequency limits on $\left|z_{o}\right|$. At low frequencies, $z_{\pi}=r_{\pi}$ and

$$
\begin{equation*}
\left.z_{o}\right|_{\omega=0} \approx \frac{1}{g_{m}}+\frac{R_{S}+r_{b}}{\beta_{0}} \tag{7.60}
\end{equation*}
$$

At high frequencies, $z_{\pi} \rightarrow 0$ because $C_{\pi}$ becomes a short circuit and thus

$$
\begin{equation*}
\left.z_{o}\right|_{\omega=\infty}=R_{S}+r_{b} \tag{7.61}
\end{equation*}
$$

Thus $z_{o}$ is resistive at very low and very high frequencies and its behavior in between depends on parameter values. At very low collector currents, $1 / g_{m}$ is large. If $1 / g_{m}>\left(R_{S}+r_{b}\right)$, a comparison of (7.60) and (7.61) shows that $\left|z_{o}\right|$ decreases as frequency increases and the output impedance appears capacitive. However, at collector currents of more than several hundred micro amperes, we usually find that $1 / g_{m}<\left(R_{S}+r_{b}\right)$. Then $\left|z_{o}\right|$ increases with frequency, which represents inductive behavior that can have a major influence on the circuit behavior, particularly when driving capacitive loads. If $1 / g_{m}=\left(R_{S}+r_{b}\right)$ then the output impedance is resistive and independent of frequency over a wide bandwidth. To maintain this condition over variations in process, supply, and temperature, practical design goals are $R_{S} \approx 1 / g_{m}$ and $r_{b} \ll R_{S}$.

Assuming that the collector bias current is such that $z_{o}$ is inductive, we can postulate an equivalent circuit for $z_{o}$ as shown in Fig. 7.17. At low frequencies the inductor is a short circuit and

$$
\begin{equation*}
\left.z_{o}\right|_{\omega=0}=R_{1} \| R_{2} \tag{7.62}
\end{equation*}
$$

At high frequencies the inductor is an open circuit and

$$
\begin{equation*}
\left.z_{o}\right|_{\omega=\infty}=R_{2} \tag{7.63}
\end{equation*}
$$

If we assume that $\left.\left.z_{o}\right|_{\omega=0} \ll z_{o}\right|_{\omega=\infty}$ then $R_{1} \ll R_{2}$, and we can simplify (7.62) to

$$
\begin{equation*}
\left.z_{o}\right|_{\omega=0} \approx R_{1} \tag{7.64}
\end{equation*}
$$

The impedance of the circuit of Fig. 7.17 can be expressed as

$$
\begin{equation*}
z_{o}=\frac{\left(R_{1}+s L\right) R_{2}}{R_{1}+R_{2}+s L} \approx \frac{\left(R_{1}+s L\right) R_{2}}{R_{2}+s L} \tag{7.65}
\end{equation*}
$$

assuming that $R_{1} \ll R_{2}$.
image_name:Figure 7.17
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Load, N2: RIL}
name: L, type: Inductor, value: L, ports: {N1: RIL, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: LOAD, N2: GND}
]
extrainfo:The circuit diagram represents the output impedance of an emitter follower at moderate current levels. The impedance is analyzed assuming R1 is much less than R2, allowing simplification of the impedance expression.

Figure 7.17 Equivalent circuit for the output impedance of an emitter follower at moderate current levels.

The complete emitter-follower output impedance can be calculated by substituting (7.57) in (7.56) with $R_{S}^{\prime}=r_{b}+R_{S}$, which gives

$$
\begin{gather*}
z_{o}=\frac{\frac{r_{\pi}}{1+s C_{\pi} r_{\pi}}+R_{S}^{\prime}}{1+\frac{g_{m} r_{\pi}}{1+s C_{\pi} r_{\pi}}}=\frac{r_{\pi}+R_{S}^{\prime}+s C_{\pi} r_{\pi} R_{S}^{\prime}}{\beta_{0}+1+s C_{\pi} r_{\pi}} \\
\approx \frac{\left(\frac{1}{g_{m}}+\frac{R_{S}^{\prime}}{\beta_{0}}+s C_{\pi} r_{\pi} \frac{R_{S}^{\prime}}{\beta_{0}}\right) R_{S}^{\prime}}{R_{S}^{\prime}+s C_{\pi} r_{\pi} \frac{R_{S}^{\prime}}{\beta_{0}}} \tag{7.66}
\end{gather*}
$$

where $\beta_{0} \gg 1$ is assumed.
Comparing (7.66) with (7.65) shows that, under the assumptions made in this analysis, the emitter-follower output impedance can be represented by the circuit of Fig. 7.17 with

$$
\begin{gather*}
R_{1}=\frac{1}{g_{m}}+\frac{R_{S}^{\prime}}{\beta_{0}}  \tag{7.67}\\
R_{2}=R_{S}^{\prime}  \tag{7.68}\\
L=C_{\pi} r_{\pi} \frac{R_{S}^{\prime}}{\beta_{0}} \tag{7.69}
\end{gather*}
$$

The effect of $C_{\mu}$ was neglected in this calculation, which is a reasonable approximation for low to moderate values of $R_{S}^{\prime}$.

The preceding calculations have shown that the input and output impedances of the emitter follower are frequency dependent. One consequence of this dependence is that the variation of the terminal impedances with frequency may limit the useful bandwidth of the circuit.

#### EXAMPLE

Calculate the elements in the equivalent circuits for input and output impedance of the emitter follower in the previous example. In Fig. 7.16 the input capacitance can be calculated from (7.59)

$$
\frac{C_{\pi}}{1+g_{m} R_{L}}=\frac{10}{1+\frac{2000}{26}} \mathrm{pF}=0.13 \mathrm{pF}
$$

The resistance in shunt with this capacitance is

$$
\left(1+g_{m} R_{L}\right) r_{\pi}=\left(1+\frac{2000}{26}\right)(2.6 \mathrm{k} \Omega)=202 \mathrm{k} \Omega
$$

In addition, $r_{b}=150 \Omega$ and $R_{L}=2 \mathrm{k} \Omega$. The elements in the output equivalent circuit of Fig. 7.17 can be calculated from (7.67), (7.68), and (7.69) as

$$
\begin{gathered}
R_{1}=\left(26+\frac{200}{100}\right) \Omega=28 \Omega \\
R_{2}=200 \Omega \\
L=10^{-11} \times 2600 \times \frac{200}{100} \mathrm{H}=52 \mathrm{nH}
\end{gathered}
$$

Note that the assumption $R_{1} \ll R_{2}$ is valid in this case.
image_name:Figure 7.18 Small-signal model for the source follower
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vi, N2: G}
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: G, Nn: X1}
name: Cgd + Cgb, type: Capacitor, value: Cgd + Cgb, ports: {Np: G, Nn: GND}
name: gmV1, type: VoltageControlledCurrentSource, value: gmV1, ports: {Np: G, Nn: X1}
name: gmbVsb, type: VoltageControlledCurrentSource, value: gmbVsb, ports: {Np: X1, Nn: X1}
name: RL, type: Resistor, value: RL, ports: {N1: X1, N2: GND}
name: Csb, type: Capacitor, value: Csb, ports: {Np: X1, Nn: GND}
]
extrainfo:This circuit is a small-signal model for a source follower. It includes a voltage source, resistors, capacitors, and voltage-controlled current sources. The circuit models the frequency response of the source follower with components such as Cgs, Cgd, Cgb, and Csb, which represent parasitic capacitances. The resistors and current sources model the transconductance and body effect.

Figure 7.18 Small-signal model for the source follower in Fig. 7.13b.

#### 7.2.3.2 Frequency Response of the Source Follower

The small-signal circuit for the source follower in Fig. 7.13b is shown in Fig. 7.18. Here, $C_{g d}$, $C_{g b}$, and $C_{s b}$ are ignored initially. One key difference between Figures 7.18 and $7.13 c$ is the $g_{m b}$ generator. Since the current through the $g_{m b}$ generator is controlled by the voltage across it, this generator can be replaced with a resistor of value $1 / g_{m b}$ from $v_{o}$ to ground, which is in parallel with $R_{L}$. Therefore, the total effective load resistance is $R_{L}^{\prime}=R_{L} \|\left(1 / g_{m b}\right)$. The transfer function for the source follower can be found by substituting the appropriate values from Table 7.1 into (7.47), (7.48), and (7.49). If $g_{m} R_{L}^{\prime} \gg 1$, the low-frequency gain is about unity. The zero and pole are given by

$$
\begin{gather*}
z_{1}=-\frac{g_{m}}{C_{g s}} \approx-\omega_{T}  \tag{7.70}\\
p_{1}=-\frac{1}{C_{g s} R_{1}} \tag{7.71}
\end{gather*}
$$

where

$$
\begin{equation*}
R_{1}=\frac{R_{S}+R_{L}^{\prime}}{1+g_{m} R_{L}^{\prime}} \tag{7.72}
\end{equation*}
$$

Typically, the zero has a magnitude that is slightly larger than the pole. If $g_{m} R_{L}^{\prime} \gg 1$ and $R_{S} \ll R_{L}^{\prime}$ in (7.72), then $R_{1} \approx 1 / g_{m}$ and (7.71) gives $p_{1} \approx-g_{m} / C_{g s} \approx-\omega_{T}$. However, if $R_{S}$ in (7.72) becomes large compared to $R_{L}$ or if $g_{m} R_{L}^{\prime}$ is not much larger than one, the pole magnitude will be significantly less than $\omega_{T}$.

#### EXAMPLE

Calculate the transfer function for a source follower with $C_{g s}=7.33 \mathrm{pF}, k^{\prime} W / L=100 \mathrm{~mA} / \mathrm{V}^{2}$, $R_{L}=2 \mathrm{k} \Omega, R_{S}=190 \Omega$, and $I_{D}=4 \mathrm{~mA}$. Ignore body effect, and let $C_{g d}=0, C_{g b}=0$, and $C_{s b}=0$.

From the data, $g_{m}=\sqrt{2(100) 4} \mathrm{~mA} / \mathrm{V}=28.2 \mathrm{~mA} / \mathrm{V}$. Ignoring body effect, we have $R_{L}^{\prime}=$ $R_{L} \|\left(1 / g_{m b}\right)=R_{L}$. Since $C_{g d}=0, \omega_{T}$ of the device is

$$
\begin{equation*}
\omega_{T}=\frac{g_{m}}{C_{g s}}=\frac{28.2 \frac{\mathrm{~mA}}{\mathrm{~V}}}{7.33 \mathrm{pF}}=3.85 \times 10^{9} \mathrm{rad} / \mathrm{s} \tag{7.73}
\end{equation*}
$$

and thus $f_{T}=612 \mathrm{MHz}$. From (7.70) and (7.73), the zero of the transfer function is

$$
z_{1}=-\frac{g_{m}}{C_{g s}}=-3.85 \times 10^{9} \mathrm{rad} / \mathrm{s}
$$

From (7.72)

$$
R_{1}=\frac{190+2000}{1+0.0282 \times 2000} \Omega=38.2 \Omega
$$

The pole from (7.71) is

$$
p_{1}=-\frac{10^{12}}{7.33} \frac{1}{38.2} \mathrm{rad} / \mathrm{s}=-3.57 \times 10^{9} \mathrm{rad} / \mathrm{s}
$$

The pole and zero are thus quite closely spaced, as shown in Fig. 7.15a.
The low-frequency gain of the circuit from (7.67) is

$$
\frac{v_{o}}{v_{i}}=\frac{g_{m} R_{L}^{\prime}}{1+g_{m} R_{L}^{\prime}}=\frac{28.2 \times 10^{-3} \times 2000}{1+28.2 \times 10^{-3} \times 2000}=0.983
$$

The parameters derived above can be used in (7.47) to plot the circuit gain versus frequency, and this plot is similar to the magnitude plot shown in Fig. $7.15 b$ for $C_{g d}=0$. The gain is flat with frequency until near $f_{T}=612 \mathrm{MHz}$, where a decrease of about 0.4 dB occurs. The analysis predicts that the gain is then flat as frequency is increased further because the input signal is simply fed forward to $R_{L}^{\prime}$ via $C_{g s}$ at very high frequencies. In practice, capacitors $C_{g d}, C_{g b}$, and $C_{s b}$ that were assumed to be zero in this example cause the gain to roll off at high frequencies, as will be demonstrated in the next example.

When capacitors $C_{g d}, C_{g b}$, and $C_{s b}$ that were ignored above are included in the analysis, the voltage-gain expression becomes more complicated than (7.47). An exact analysis, with all the capacitors included, follows the same steps as the analysis of Fig. 7.13c and yields

$$
\begin{equation*}
\frac{v_{o}}{v_{i}}=\frac{g_{m} R_{L}^{\prime}}{1+g_{m} R_{L}^{\prime}} \frac{1+s \frac{C_{g s}}{g_{m}}}{1+a s+b s^{2}} \tag{7.74a}
\end{equation*}
$$

with

$$
\begin{gather*}
a=\frac{R_{L}^{\prime}\left(C_{g s}+C_{s b}\right)+R_{S}\left(C_{g s}+C_{g d}^{\prime}\right)+R_{S} g_{m} R_{L}^{\prime} C_{g d}^{\prime}}{1+g_{m} R_{L}^{\prime}} \\
\approx \frac{R_{L}^{\prime}\left(C_{g s}+C_{s b}\right)+R_{S} C_{g s}+R_{S} g_{m} R_{L}^{\prime} C_{g d}^{\prime}}{1+g_{m} R_{L}^{\prime}}  \tag{7.74b}\\
b=\frac{R_{S} R_{L}^{\prime}\left[C_{s b}\left(C_{g s}+C_{g d}^{\prime}\right)+C_{g s} C_{g d}^{\prime}\right]}{1+g_{m} R_{L}^{\prime}} \approx \frac{R_{S} R_{L}^{\prime}\left[C_{s b} C_{g s}+C_{g s} C_{g d}^{\prime}\right]}{1+g_{m} R_{L}^{\prime}} \tag{7.74c}
\end{gather*}
$$

where $C_{g d}^{\prime}=C_{g d}+C_{g b}$. The approximations for $a$ and $b$ use $C_{g s}+C_{g d}^{\prime} \approx C_{g s}$ since $C_{g s} \gg C_{g d}^{\prime}$. This exact transfer function has a zero at $-g_{m} / C_{g s}$, in agreement with (7.70), and two poles. If $C_{g d}^{\prime}$ and $C_{s b}$ are set to zero, (7.74) has one pole as given by (7.71). Making approximations in (7.74) that lead to simple, useful expressions for the poles is difficult since a dominant real pole does not always exist. In fact, the poles can be complex.

#### EXAMPLE

Calculate the transfer function for a source follower with $C_{g s}=7.33 \mathrm{pF}, C_{g d}=0.1 \mathrm{pF}$, $C_{g b}=0.05 \mathrm{pF}, C_{s b}=0.5 \mathrm{pF}, k^{\prime} W / L=100 \mathrm{~mA} / \mathrm{V}^{2}, R_{L}=2 \mathrm{k} \Omega, R_{S}=190 \Omega$, and $I_{D}=$ 4 mA . Ignore body effect.

These data are the same as in the last example, except we now have non-zero $C_{g d}, C_{g b}$, and $C_{s b}$. From the data, $g_{m}=28.2 \mathrm{~mA} / \mathrm{V}$ and $C_{g d}^{\prime}=C_{g d}+C_{g b}=0.15 \mathrm{pF}$. Also, ignoring body effect, we have $R_{L}^{\prime}=R_{L} \|\left(1 / g_{m b}\right)=R_{L}$. The low-frequency gain of the circuit, as calculated in the previous example, is 0.983 . From (7.74a), the zero is

$$
z=-\frac{g_{m}}{C_{g s}}=-\frac{28.2 \frac{\mathrm{~mA}}{\mathrm{~V}}}{7.33 \mathrm{pF}}=-3.85 \times 10^{9} \mathrm{rad} / \mathrm{s}
$$

From (7.74b) and (7.74c), the coefficients of the denominator of the transfer function are

$$
\begin{aligned}
& a \approx \frac{2 \mathrm{k}(7.33 \mathrm{p}+0.5 \mathrm{p})+190(7.33 \mathrm{p})+190(0.0282)(2 \mathrm{k})(0.15 \mathrm{p})}{1+(0.0282)(2 \mathrm{k})} \mathrm{s}=0.324 \mathrm{~ns} \\
& b \approx \frac{190(2 \mathrm{k})[(0.5 \mathrm{p})(7.33 \mathrm{p})+(7.33 \mathrm{p})(0.15 \mathrm{p})]}{1+(0.0282)(2 \mathrm{k})} \mathrm{s}^{2}=0.0315(\mathrm{~ns})^{2}
\end{aligned}
$$

Using the quadratic formula to solve for the poles, we find that the poles are

$$
p_{1,2}=-5.1 \times 10^{9} \pm j 2.3 \times 10^{9} \mathrm{rad} / \mathrm{s}
$$

The poles and zero are fairly close together, as shown in Fig. 7.19a. The gain magnitude and phase are plotted in Fig. 7.19. The $-3-\mathrm{dB}$ bandwidth is 1.6 GHz . Because the two poles and zero are fairly close together, the gain versus frequency approximates a one-pole roll-off.

High-frequency input signals are attenuated by capacitors $C_{g d}$ and $C_{g b}$ that connect between the gate and ground, causing the gain to roll off and approach zero as $\omega \rightarrow \infty$. However, the bandwidth of the source follower is still quite large, and bandwidths of the order of the $f_{T}$ of the device can be obtained in practice.

If the source follower drives a load capacitance in parallel with the load resistance, its value can be added to $C_{s b}$ in (7.74). Such a load capacitance is present whenever the source-follower transistor is fabricated in a well and its source is connected to its well to avoid body effect. The well-body capacitance can be large and may significantly affect the $3-\mathrm{dB}$ bandwidth of the circuit.

In Section 7.2.3.1, calculations were carried out for the input and output impedances of the emitter follower. Since the equivalent circuit for the MOSFET is similar to that for the
image_name:Figure 7.19 (a)
description:The graph in Figure 7.19 (a) is a pole-zero plot used to analyze the source-follower circuit. This type of graph is typically used in control systems and signal processing to represent the poles and zeros of a transfer function in the complex plane.

1. **Axes Labels and Units:**
- The horizontal axis is labeled \( \sigma \) and represents the real part of the complex frequency, in units of radians per second (rad/s).
- The vertical axis is labeled \( j\omega \) and represents the imaginary part of the complex frequency, also in units of rad/s. The scale on this axis is denoted as \( \times 10^9 \) rad/s, indicating that values are in the billions of radians per second.

2. **Overall Behavior and Trends:**
- The plot displays a single zero and a single pole, both located on the real axis, indicating that there are no imaginary components to these values.
- The zero is marked with an '×' and is located at approximately \( \sigma = -5 \times 10^9 \) rad/s.
- The pole is marked with an 'o' and is located at approximately \( \sigma = -4 \times 10^9 \) rad/s.

3. **Key Features and Technical Details:**
- The positioning of the pole and zero on the left half of the complex plane suggests a stable system, as poles on the left half-plane typically indicate stability in linear time-invariant systems.
- The proximity of the pole and zero suggests that they may have a cancelling effect on the system's response, particularly affecting the frequency response and bandwidth.

4. **Annotations and Specific Data Points:**
- The zero is clearly marked at \( \sigma = -5 \times 10^9 \) rad/s, and the pole is marked at \( \sigma = -4 \times 10^9 \) rad/s.
- There are no additional annotations or reference lines on the plot, but the key data points are clearly indicated with their respective symbols (× for zero and o for pole).

Figure 7.19 (a) Pole-zero plot for the source-follower example using (7.74).
image_name:Figure 7.19 (b)
description:**Type of Graph and Function:**
The graph is a Bode plot, specifically showing the magnitude of the gain versus frequency for a source follower circuit.

**Axes Labels and Units:**
- The x-axis represents frequency in hertz (Hz) and is plotted on a logarithmic scale, ranging from 10 Hz to 100 GHz.
- The y-axis represents the magnitude of the gain in decibels (dB), ranging from 0 dB to -30 dB.

**Overall Behavior and Trends:**
- The graph shows a flat response at 0 dB gain across a broad frequency range, indicating a constant gain in this region.
- As the frequency increases beyond 1 GHz, the gain begins to drop sharply, indicating a decrease in gain at higher frequencies.
- The graph suggests a low-pass filter behavior, where the gain remains constant over a wide range and then decreases at higher frequencies.

**Key Features and Technical Details:**
- The transition point or cutoff frequency appears to be around 1 GHz, where the gain starts to decrease.
- The sharp decline in gain suggests the presence of a pole at high frequencies, aligning with the pole-zero plot context.

**Annotations and Specific Data Points:**
- There are no specific annotations or markers on the plot, but the transition in gain is a critical feature, indicating the bandwidth limit of the circuit.
image_name:Figure 7.19 (c)
description:The graph in Figure 7.19 (c) is a Bode plot depicting the phase response of a source follower circuit's gain versus frequency.

1. **Type of Graph and Function:**
- This is a phase Bode plot, commonly used in control systems and signal processing to analyze the phase shift of a system over a range of frequencies.

2. **Axes Labels and Units:**
- The horizontal axis represents frequency, labeled 'Frequency (Hz)', and is displayed on a logarithmic scale, ranging from 10 Hz to 100 GHz.
- The vertical axis represents the phase of the gain, labeled '∠Gain (degrees)', ranging from 0° to -90°.

3. **Overall Behavior and Trends:**
- The phase response remains at 0° for low frequencies up to around 100 MHz.
- Beyond this point, the phase begins to decrease, indicating a phase lag introduced by the circuit, reaching approximately -90° as the frequency approaches 10 GHz.

4. **Key Features and Technical Details:**
- The phase shift starts occurring sharply after 100 MHz, suggesting a critical frequency or bandwidth limit.
- The transition from 0° to -90° is smooth, indicating a single dominant pole contributing to the phase shift.

5. **Annotations and Specific Data Points:**
- There are no specific markers or additional annotations on the plot, but the smooth transition in phase highlights the frequency at which the system begins to lag significantly.

Figure 7.19 (b) Magnitude and (c) phase of the gain versus frequency for this source follower.
bipolar transistor (apart from the $g_{m b}$ generator), similar results can be found for the source follower by substituting the appropriate values from Table 7.1 in the formulas for $z_{i}$ and $z_{o}$ in Section 7.2.3.1. One major difference is that the MOSFET has a $g_{m}$ that is usually much lower than for the bipolar transistor with the same bias current. Therefore, the condition that produces an inductive output impedance ( $1 / g_{m}<R_{S}$ ) occurs less often with source followers than emitter followers.

### 7.2.4 Frequency Response of Current Buffers

The common-base (CB) and common-gate (CG) amplifier configurations are shown in ac schematic form in Fig. 7.20. These stages have a low input impedance, high output impedance, approximately unity current gain, and wide bandwidth. They find use in wideband applications and also in applications requiring low input impedance. As described in Chapter 1, the bipolar transistor breakdown voltage is maximum in this configuration. The combination of
image_name:(a)
description:
[
name: vi, type: VoltageSource, value: vi, ports: {Np: Vi, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vi, N2: eo}
name: Q0, type: NPN, ports: {C: Vo, B: GND, E: e0}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:This is a common-base amplifier configuration using an NPN transistor. The input is applied to the emitter, and the output is taken from the collector. The circuit is designed to provide low input impedance and high output impedance.
image_name:(b)
description:
[
name: Vi, type: VoltageSource, value: vi, ports: {Np: Vi, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vi, N2: eo}
name: M0, type: NMOS, ports: {S: s0, D: Vo, G: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a common-gate amplifier configuration using an NMOS transistor. It has a low input impedance and high output impedance, suitable for wideband applications.
image_name:(c)
description:The diagram labeled (c) represents a general model for both common-base (CB) and common-gate (CG) amplifiers. The main components of this system include:

1. **Input Source (Vi):** This is the input voltage source, labeled as \( v_i \), which provides the initial signal to the system.

2. **Source Resistor (Rs):** Connected to the input source, this resistor, labeled \( R_S \), limits the current entering the transistor and helps set the input impedance of the amplifier.

3. **Transistor (Qo):** The central component is a transistor, labeled \( Q_0 \), which acts as the amplification device. In the common-base configuration, this would be a bipolar junction transistor (BJT), and in the common-gate configuration, it would be a field-effect transistor (FET). The transistor is grounded at the base (or gate for FET), which is characteristic of these configurations.

4. **Output Node (Vo):** The amplified output is taken across this node, labeled \( v_o \), which is connected to the load resistor.

5. **Load Resistor (RL):** This resistor, labeled \( R_L \), is connected to the output node. It defines the output impedance and affects the voltage gain of the amplifier.

Flow of Information:
- The input signal \( v_i \) is applied across \( R_S \) and enters the transistor \( Q_0 \).
- The transistor amplifies the current, maintaining approximately unity current gain, and the amplified signal is delivered to the output node \( v_o \).
- The output signal \( v_o \) is then taken across the load resistor \( R_L \).

Overall System Function:
This model functions as a current buffer, characterized by low input impedance, high output impedance, and wide bandwidth. It is suitable for applications requiring these properties, such as wideband amplifiers. The arrangement of components ensures efficient current transfer from input to output with minimal voltage gain but high current gain, making it ideal for driving low impedance loads.

Figure 7.20 (a) An ac schematic of a common-base amplifier. (b) An ac schematic of a common-gate amplifier. (c) A general model for both amplifiers.
this property and the wideband property make the CB stages useful in high-voltage wideband output stages driving oscilloscope deflection plates.

A small-signal equivalent circuit that can model both the CB and CG stage by using a general small-signal model is shown in Fig. 7.20c. The input voltage source and source resistance are represented by a Norton equivalent. Resistance $R_{S}$ is neglected in the following analysis since the input impedance of the amplifier is quite low. Another good approximation if $r_{x}$ is small is that $C_{f}$ simply shunts $R_{L}$, as shown in Fig. 7.20c. In this analysis, $r_{o}$ will be neglected and the output signal $i_{o}$ will be taken as the output of the $g_{m}$ controlled source. The approximate output voltage $v_{o}$ is obtained by assuming $i_{o}$ flows in the parallel combination of $R_{L}$ and $C_{f}$.

The analysis of the circuit of Fig. $7.20 c$ proceeds by applying KCL at node $W$. Neglecting $R_{S}$,

$$
\begin{equation*}
i_{i}+\frac{v_{1}}{z_{\text {in }}}+g_{m} v_{1}=0 \tag{7.75}
\end{equation*}
$$

where

$$
\begin{equation*}
z_{\text {in }}=\frac{r_{\mathrm{in}}}{1+s C_{\mathrm{in}} r_{\text {in }}} \tag{7.76}
\end{equation*}
$$

From (7.75) and (7.76)

$$
\begin{equation*}
i_{i}=-v_{1}\left(g_{m}+\frac{1}{r_{\mathrm{in}}}+s C_{\mathrm{in}}\right) \tag{7.77}
\end{equation*}
$$

Now

$$
\begin{equation*}
i_{o}=-g_{m} v_{1} \tag{7.78}
\end{equation*}
$$

Substituting (7.77) into (7.78) gives

$$
\begin{equation*}
\frac{i_{o}}{i_{i}}=\frac{g_{m} r_{\mathrm{in}}}{g_{m} r_{\mathrm{in}}+1} \frac{1}{1+s \frac{r_{\mathrm{in}}}{g_{m} r_{\mathrm{in}}+1} C_{\mathrm{in}}} \tag{7.79}
\end{equation*}
$$

#### 7.2.4.1 Common-Base Amplifier Frequency Response

The small-signal circuit for the common-base (CB) amplifier of Fig. $7.20 a$ is shown in Fig. 7.21. Substituting the values in Table 7.1 into (7.79) gives for the current gain

$$
\begin{equation*}
\frac{i_{o}}{i_{i}}=\frac{g_{m} r_{\pi}}{g_{m} r_{\pi}+1} \frac{1}{1+s \frac{r_{\pi}}{g_{m} r_{\pi}+1} C_{\pi}} \tag{7.80}
\end{equation*}
$$

Using $\beta_{0}=g_{m} r_{\pi}$ and assuming $\beta_{0} \gg 1$, (7.80) simplifies to

$$
\begin{equation*}
\frac{i_{o}}{i_{i}} \approx \frac{\beta_{0}}{\beta_{0}+1} \frac{1}{1+s \frac{C_{\pi}}{g_{m}}}=\alpha_{0} \frac{1}{1+s \frac{C_{\pi}}{g_{m}}} \tag{7.81}
\end{equation*}
$$

where $\alpha_{0}=\beta_{0} /\left(\beta_{0}+1\right)$. This analysis shows that the CB stage current gain has a lowfrequency value $\alpha_{0} \approx 1$ and a pole at $p_{1}=-g_{m} / C_{\pi} \approx-\omega_{T}$. The CB stage is thus a wide-band unity-current gain amplifier with low input impedance and high output impedance. It can be seen from the polarities in Fig. 7.20a that the phase shift between $v_{i}$ and $v_{o}$ in the CB stage is zero at low frequencies. This result can be compared with the case of the common-emitter stage of Fig. $7.2 a$, which has $180^{\circ}$ phase shift between $v_{i}$ and $v_{o}$ at low frequencies.

If the desired output is the current flowing through $R_{L}$, then $C_{\mu}$ and $R_{L}$ form a current divider from $i_{o}$ to this desired current (under the assumption that $C_{\mu}$ is in parallel with $R_{L}$ because $r_{b}$ is very small). When included in the analysis, this current divider introduces an additional pole $p_{2}=-1 / R_{L} C_{\mu}$ in the transfer function.

Comparing Fig. 7.20a with Fig. 7.13a shows that the input impedance of the commonbase stage is the same as the output impedance of the emitter follower with $R_{S}=0$. Thus the
image_name:Figure 7.21 Small-signal model for the common-base circuit
description:
[
name: i_i, type: CurrentSource, ports: {Np: E, Nn: GND}
name: R_S, type: Resistor, value: R_S, ports: {N1: E, N2: GND}
name: r_π, type: Resistor, value: r_π, ports: {N1: E, N2: B}
name: C_π, type: Capacitor, value: C_π, ports: {Np: E, Nn: B}
name: C_μ, type: Capacitor, value: C_μ, ports: {Np: Vo, Nn: "B"}
name: r_b, type: Resistor, value: r_b, ports: {N1: "B", N2: B}
name: R_L, type: Resistor, value: R_L, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a small-signal model for a common-base amplifier. The input current source i_i flows from node E to ground. The resistors R_S and r_π are connected at node E with r_π also connecting to node B. Capacitor C_π is parallel to r_π. The output current source i_o is connected to node Vo. Capacitor C_μ and resistor R_L form a current divider at node Vo. Resistor r_b connects nodes B and B'.

Figure 7.21 Small-signal model for the common-base circuit in Fig. 7.20a.
common-base stage input impedance is low at low frequencies and becomes inductive at high frequencies for collector bias currents of several hundred microamperes or more. As shown in Chapter 3, the output resistance of the common-base stage at low frequencies with large $R_{S}$ is approximately $\beta_{0} r_{o}$, which is extremely large. At high frequencies the output impedance is capacitive and is dominated by $C_{\mu}$ (and $C_{c s}$ for $n p n$ transistors).

Unlike the common-emitter stage where $C_{\mu}$ is Miller multiplied, the common-base stage does not contain a feedback capacitance from collector to emitter to cause the Miller effect. As a consequence, the effect of large values of $R_{L}$ on the frequency response of the common-base stage is much less than in the common-emitter stage.

#### 7.2.4.2 Common-Gate Amplifier Frequency Response

The small-signal circuit for the common-gate (CG) amplifier of Fig. 7.20 b is shown in Fig. 7.22. One element in this circuit that does not appear in the general model in Fig. 7.20c is the $g_{m b}$ generator. Since $v_{b s}=v_{g s}$ and the $g_{m}$ and $g_{m b}$ generators are in parallel here, these controlled sources can be combined. Also, capacitors $C_{g b}, C_{d b}$, and $C_{s b}$ are not included in the general model. Here, $C_{g b}$ is shorted and can be ignored. Capacitance $C_{d b}$ is in parallel with $R_{L}$ and therefore can be ignored if the output variable of interest is the current $i_{o}$. Capacitance $C_{s b}$ appears in parallel with $C_{g s}$ in the small-signal circuit since the body and gate both connect to small-signal ground. Using the combined transconductance and input capacitance and values from Table 7.1 in (7.79) gives

$$
\begin{equation*}
\frac{i_{o}}{i_{i}}=\frac{1}{1+s \frac{C_{g s}+C_{s b}}{g_{m}+g_{m b}}} \tag{7.82}
\end{equation*}
$$

From this equation, the current gain of the common-gate stage has a low-frequency value of unity and a pole at $p_{1}=-\left(g_{m}+g_{m b}\right) /\left(C_{g s}+C_{s b}\right)$. If $C_{g s} \gg C_{s b}$, then $\left|p_{1}\right| \approx\left(g_{m}+\right.$ $\left.g_{m b}\right) / C_{g s}>g_{m} / C_{g s} \approx \omega_{T}$. The CG stage is thus a wideband unity-current-gain amplifier with low input impedance and high output impedance. It can be seen from the polarities in Fig. $7.20 b$ that there is zero phase shift between $v_{i}$ and $v_{o}$ in the CG stage at low frequencies. This phase shift can be compared with the case of the common-source stage of Fig. 7.2b, which has $180^{\circ}$ phase shift between $v_{i}$ and $v_{o}$ at low frequencies.

If the desired output is the current flowing through $R_{L}$, then $C_{d b}, C_{g d}$, and $R_{L}$ form a current divider from $i_{o}$ to this desired current. When included in the analysis, this current divider introduces an additional pole $p_{2}=-1 / R_{L}\left(C_{d b}+C_{g d}\right)$ in the transfer function.
image_name:Figure 7.22 Small-signal model for the common-gate circuit
description:
[
name: I1, type: CurrentSource, value: I1, ports: {Np: S, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: S, N2: GND}
name: Cgs+Cs, type: Capacitor, value: Cgs+Cs, ports: {Np: G(GND), Nn: S}
name: gmv1, type: VoltageControlledCurrentSource, value: gmv1, ports: {Np: S, Nn: Vo}
name: gmbv1, type: VoltageControlledCurrentSource, value: gmbv1, ports: {Np: S, Nn: Vo}
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: Vo, Nn: G}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a small-signal model for a common-gate amplifier. It includes a current source, resistors, capacitors, and voltage-controlled current sources. The input current is divided among components, and the circuit introduces an additional pole in the transfer function due to the current divider formed by Cgd and RL.
Figure 7.22 Small-signal model for the common-gate circuit in Fig. 7.20b.

Unlike the common-source stage where $C_{g d}$ is Miller multiplied, the common-gate stage does not contain a feedback capacitance from drain to source to cause the Miller effect. As a consequence, the effect of large values of $R_{L}$ on the frequency response of the common-gate stage is much less than in the common-source stage.

## 7.3 Multistage Amplifier Frequency Response

The above analysis of the frequency behavior of single-stage circuits indicates the complexity that can arise even with simple circuits. The complete analysis of the frequency response of multistage circuits with many capacitive elements rapidly becomes very difficult and the answers become so complicated that little use can be made of the results. For this reason approximate methods of analysis have been developed to aid in the circuit design phase, and computer simulation is used to verify the final design. One such method of analysis is the zerovalue time constant analysis that will now be described. First some ideas regarding dominant poles are developed.

### 7.3.1 Dominant-Pole Approximation

For any electronic circuit we can derive a transfer function $A(s)$ by small-signal analysis to give

$$
\begin{equation*}
A(s)=\frac{N(s)}{D(s)}=\frac{a_{0}+a_{1} s+a_{2} s^{2}+\cdots+a_{m} s^{m}}{1+b_{1} s+b_{2} s^{2}+\cdots+b_{n} s^{n}} \tag{7.83}
\end{equation*}
$$

where $a_{0}, a_{1}, \ldots, a_{m}$, and $b_{1}, b_{2}, \ldots, b_{n}$ are constants. Very often the transfer function contains poles only (or the zeros are unimportant). In this case we can factor the denominator of (7.83) to give

$$
\begin{equation*}
A(s)=\frac{K}{\left(1-\frac{s}{p_{1}}\right)\left(1-\frac{s}{p_{2}}\right) \cdots\left(1-\frac{s}{p_{n}}\right)} \tag{7.84}
\end{equation*}
$$

where $K$ is a constant and $p_{1}, p_{2}, \ldots, p_{n}$ are the poles of the transfer function.
It is apparent from (7.84) that

$$
\begin{equation*}
b_{1}=\sum_{i=1}^{n}\left(-\frac{1}{p_{i}}\right) \tag{7.85}
\end{equation*}
$$

An important practical case occurs when one pole is dominant. That is, when

$$
\left|p_{1}\right| \ll\left|p_{2}\right|,\left|p_{3}\right|, \ldots \quad \text { so that } \quad\left|\frac{1}{p_{1}}\right| \gg\left|\sum_{i=2}^{n}\left(-\frac{1}{p_{i}}\right)\right|
$$

This situation is shown in the $s$ plane in Fig. 7.23 and in this case it follows from (7.85) that

$$
\begin{equation*}
b_{1} \simeq\left|\frac{1}{p_{1}}\right| \tag{7.86}
\end{equation*}
$$

If we return now to (7.84) and calculate the gain magnitude in the frequency domain, we obtain

$$
\begin{equation*}
|A(j \omega)|=\frac{K}{\sqrt{\left[1+\left(\frac{\omega}{p_{1}}\right)^{2}\right]\left[1+\left(\frac{\omega}{p_{2}}\right)^{2}\right] \cdots\left[1+\left(\frac{\omega}{p_{n}}\right)^{2}\right]}} \tag{7.87}
\end{equation*}
$$

image_name:Figure 7.23
description:The graph in Figure 7.23 is a pole diagram plotted on the complex \( s \)-plane, which is commonly used in control systems and signal processing to represent the poles of a transfer function.

1. **Type of Graph and Function:**
- The graph is a pole-zero plot on the complex \( s \)-plane.
- It is used to visualize the poles of a system, which are critical in determining the system's stability and frequency response.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \( \sigma \) and represents the real part of the complex frequency.
- The vertical axis is labeled \( j\omega \) and represents the imaginary part of the complex frequency.
- The axes do not have specific units marked, as they represent complex frequency components.

3. **Overall Behavior and Trends:**
- The poles are plotted along the real axis, indicating that they are purely real and negative.
- This suggests a stable system, as all poles lie in the left half of the \( s \)-plane.

4. **Key Features and Technical Details:**
- There are three poles marked as \( p_1, p_2, \) and \( p_3 \), all located along the real axis.
- The pole \( p_1 \) is identified as a dominant pole due to its proximity to the imaginary axis compared to the other poles.
- The dominant pole \( p_1 \) plays a significant role in determining the system's low-frequency behavior and bandwidth.

5. **Annotations and Specific Data Points:**
- The diagram is annotated with the pole locations \( p_1, p_2, \) and \( p_3 \) marked with crosses.
- The specific values of the poles are not provided, but their relative positions indicate their influence on the system's dynamics.

Figure 7.23 Pole diagram for a circuit with a dominant pole.

If a dominant pole exists, then (7.87) can be approximated by

$$
\begin{equation*}
|A(j \omega)| \simeq \frac{K}{\sqrt{1+\left(\frac{\omega}{p_{1}}\right)^{2}}} \tag{7.88}
\end{equation*}
$$

This approximation will be quite accurate at least until $\omega \simeq\left|p_{1}\right|$, and thus (7.88) will accurately predict the $-3-\mathrm{dB}$ frequency and we can write

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}} \simeq\left|p_{1}\right| \tag{7.89}
\end{equation*}
$$

Use of (7.86) in (7.89) gives

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}} \simeq \frac{1}{b_{1}} \tag{7.90}
\end{equation*}
$$

for a dominant-pole situation.

### 7.3.2 Zero-Value Time Constant Analysis

This is an approximate method of analysis that allows an estimate to be made of the dominant pole (and thus the $-3-\mathrm{dB}$ frequency) of complex circuits. Considerable saving in computational effort is achieved because a full analysis of the circuit is not required. The method will be developed by considering a practical example.

Consider the equivalent circuit shown in Fig. 7.24. This is a single-stage bipolar transistor amplifier with resistive source and load impedances. The feedback capacitance is split into two parts $\left(C_{x}\right.$ and $\left.C_{\mu}\right)$ as shown. This is a slightly better approximation to the actual situation than the single collector-base capacitor we have been using, but is rarely used in hand calculations because of the analysis complexity. For purposes of analysis, the capacitor voltages $v_{1}, v_{2}$, and $v_{3}$ are chosen as variables. The external input $v_{i}$ is removed and the circuit excited with three independent current sources $i_{1}, i_{2}$, and $i_{3}$ across the capacitors, as shown in Fig. 7.24. We can show that with this choice of variables the circuit equations are of the form

$$
\begin{align*}
& i_{1}=\left(g_{11}+s C_{\pi}\right) v_{1}+g_{12} v_{2}+g_{13} v_{3}  \tag{7.91}\\
& i_{2}=g_{21} v_{1}+\left(g_{22}+s C_{\mu}\right) v_{2}+g_{23} v_{3}  \tag{7.92}\\
& i_{3}=g_{31} v_{1}+g_{32} v_{2}+\left(g_{33}+s C_{x}\right) v_{3} \tag{7.93}
\end{align*}
$$

where the $g$ terms are conductances. Note that the terms involving $s$ contributed by the capacitors are associated only with their respective capacitor voltage variables and only appear on the diagonal of the system determinant.
image_name:Figure 7.24
description:
[
name: V_i, type: VoltageSource, value: V_i, ports: {Np: V3, Nn: V1}
name: R_S, type: Resistor, value: R_S, ports: {N1: V3, N2: X_2}
name: r_b, type: Resistor, value: r_b, ports: {N1: X_2, N2: X_1}
name: C_π, type: Capacitor, value: C_π, ports: {Np: X_1, Nn: V_1}
name: r_π, type: Resistor, value: r_π, ports: {N1: X_1, N2: V_1}
name: g_mV_1, type: CurrentControlledCurrentSource, ports: {Np: V_2, Nn: V_1}
name: R_L, type: Resistor, value: R_L, ports: {N1: V_2, N2: V_1}
name: C_μ, type: Capacitor, value: C_μ, ports: {Np: X_1, Nn: V_2}
name: C_x, type: Capacitor, value: C_x, ports: {Np: X_2, Nn: V_2}
name: i_1, type: CurrentSource, ports: {Np: X_1, Nn: V_1}
name: i_2, type: CurrentSource, ports: {Np: X_1, Nn: V_2}
name: i_3, type: CurrentSource, ports: {Np: X_2, Nn: V_2}
]
extrainfo:This is a small-signal equivalent circuit of a common-emitter stage with internal feedback. The circuit includes resistors, capacitors, and controlled current sources to model the behavior of the transistor stage. The feedback is represented by the capacitors C_μ and C_x, and the controlled current source g_mV_1. The input is provided by V_i and the output is across R_L.

capacitors $C_{\mu}$ and $C_{x}$.

The poles of the circuit transfer function are the zeros of the determinant $\Delta$ of the circuit equations, which can be written in the form

$$
\begin{equation*}
\Delta(s)=K_{3} s^{3}+K_{2} s^{2}+K_{1} s+K_{0} \tag{7.94}
\end{equation*}
$$

where the coefficients $K$ are composed of terms from the above equations. For example, $K_{3}$ is the sum of the coefficients of all terms involving $s^{3}$ in the expansion of the determinant. Equation 7.94 can be expressed as

$$
\begin{equation*}
\Delta(s)=K_{0}\left(1+b_{1} s+b_{2} s^{2}+b_{3} s^{3}\right) \tag{7.95}
\end{equation*}
$$

where this form corresponds to (7.83). Note that this is a third-order determinant because there are three capacitors in the circuit. The term $K_{0}$ in (7.94) is the value of $\Delta(s)$ if all capacitors are zero $\left(C_{x}=C_{\mu}=C_{\pi}=0\right.$ ). This can be seen from (7.91), (7.92), and (7.93). Thus

$$
K_{0}=\left.\Delta\right|_{C_{\pi}=C_{\mu}=C_{x}=0}
$$

and it is useful to define

$$
\begin{equation*}
K_{0} \triangleq \Delta_{0} \tag{7.96}
\end{equation*}
$$

Consider now the term $K_{1} s$ in (7.94). This is the sum of all the terms involving $s$ that are obtained when the system determinant is evaluated. However, from (7.91) to (7.93) it is apparent that $s$ only occurs when associated with a capacitance. Thus the term $K_{1} s$ can be written as

$$
\begin{equation*}
K_{1} s=h_{1} s C_{\pi}+h_{2} s C_{\mu}+h_{3} s C_{x} \tag{7.97}
\end{equation*}
$$

where the $h$ terms are constants. The term $h_{1}$ can be evaluated by expanding the determinant of (7.91) to (7.93) about the first row:

$$
\begin{equation*}
\Delta(s)=\left(g_{11}+s C_{\pi}\right) \Delta_{11}+g_{12} \Delta_{12}+g_{13} \Delta_{13} \tag{7.98}
\end{equation*}
$$

where $\Delta_{11}, \Delta_{12}$, and $\Delta_{13}$ are cofactors of the determinant. Inspection of (7.91), (7.92), and (7.93) shows that $C_{\pi}$ occurs only in the first term of (7.98). Thus the coefficient of $C_{\pi} s$ in (7.98) is found by evaluating $\Delta_{11}$ with $C_{\mu}=C_{x}=0$, which will eliminate the other capacitive terms
in $\Delta_{11}$. But this coefficient of $C_{\pi} s$ is just $h_{1}$ in (7.97), and so

$$
\begin{equation*}
h_{1}=\left.\Delta_{11}\right|_{C_{\mu}}=C_{x}=0 \tag{7.99}
\end{equation*}
$$

Now consider expansion of the determinant about the second row. This must give the same value for the determinant, and thus

$$
\begin{equation*}
\Delta(s)=g_{21} \Delta_{21}+\left(g_{22}+s C_{\mu}\right) \Delta_{22}+g_{23} \Delta_{23} \tag{7.100}
\end{equation*}
$$

In this case $C_{\mu}$ occurs only in the second term of (7.100). Thus the coefficient of $C_{\mu} s$ in this equation is found by evaluating $\Delta_{22}$ with $C_{\pi}=C_{x}=0$, which will eliminate the other capacitive terms. This coefficient of $C_{\mu} s$ is just $h_{2}$ in (7.97), and thus

$$
\begin{equation*}
h_{2}=\left.\Delta_{22}\right|_{C_{\pi}=C_{x}=0} \tag{7.101}
\end{equation*}
$$

Similarly by expanding about the third row it follows that

$$
\begin{equation*}
h_{3}=\left.\Delta_{33}\right|_{C_{\pi}}=C_{\mu}=0 \tag{7.102}
\end{equation*}
$$

Combining (7.97) with (7.99), (7.101), and (7.102) gives

$$
\begin{equation*}
K_{1}=\left(\left.\Delta_{11}\right|_{C_{\mu}=C_{x}=0} \times C_{\pi}\right)+\left(\left.\Delta_{22}\right|_{C_{\pi}=C_{x}=0} \times C_{\mu}\right)+\left(\left.\Delta_{33}\right|_{C_{\mu}=C_{\pi}=0} \times C_{x}\right) \tag{7.103}
\end{equation*}
$$

and

$$
\begin{gather*}
b_{1}=\frac{K_{1}}{K_{0}}=\frac{\left.\Delta_{11}\right|_{C_{\mu}}}{\Delta_{0}}=C_{x}=0 \\
\times C_{\pi}+\frac{\left.\Delta_{22}\right|_{C_{\pi}}}{\Delta_{0}}=C_{x}=0 \times C_{\mu}  \tag{7.104}\\
+\frac{\left.\Delta_{33}\right|_{C_{\mu}}}{\Delta_{0}}=C_{\pi}=0 \times C_{x}
\end{gather*}
$$

where the boundary conditions on the determinants are the same as in (7.103). Now consider putting $i_{2}=i_{3}=0$ in Fig. 7.24. Solving (7.91) to (7.93) for $v_{1}$ gives

$$
v_{1}=\frac{\Delta_{11} i_{1}}{\Delta(s)}
$$

and thus

$$
\begin{equation*}
\frac{v_{1}}{i_{1}}=\frac{\Delta_{11}}{\Delta(s)} \tag{7.105}
\end{equation*}
$$

Equation 7.105 is an expression for the driving-point impedance at the $C_{\pi}$ node pair. Thus

$$
\frac{\left.\Delta_{11}\right|_{C_{\mu}}}{\Delta_{0}}=C_{x}=0
$$

is the driving-point resistance at the $C_{\pi}$ node pair with all capacitors equal to zero because

$$
\begin{equation*}
\frac{\Delta_{11} \mid C_{\mu}}{\Delta_{0}}=C_{x}=0=\left.\frac{\Delta_{11}}{\Delta}\right|_{C_{\mu}=C_{x}=C_{\pi}=0} \tag{7.106}
\end{equation*}
$$

We now define

$$
\begin{equation*}
R_{\pi 0}=\left.\frac{\Delta_{11}}{\Delta_{0}}\right|_{C_{\mu}=C_{x}=0} \tag{7.107}
\end{equation*}
$$

Similarly,

$$
\frac{\Delta_{22} \mid C_{\pi}}{\Delta_{0}}=C_{x}=0
$$

is the driving-point resistance at the $C_{\mu}$ node pair with all capacitors put equal to zero and is represented by $R_{\mu 0}$. Thus we can write from (7.104)

$$
\begin{equation*}
b_{1}=R_{\pi 0} C_{\pi}+R_{\mu 0} C_{\mu}+R_{x 0} C_{x} \tag{7.108}
\end{equation*}
$$

The time constants in (7.108) are called zero-value time constants because all capacitors are set equal to zero to perform the calculation. Although derived in terms of a specific example, this result is true in any circuit for which the various assumptions made in this analysis are valid. In its most general form, (7.108) becomes

$$
\begin{equation*}
b_{1}=\Sigma T_{0} \tag{7.109}
\end{equation*}
$$

where $\Sigma T_{0}$ is the sum of the zero-value time constants.
We showed previously that if there are no dominant zeros in the circuit transfer function, and if there is a dominant pole $p_{1}$, then

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}} \approx\left|p_{1}\right| \tag{7.110}
\end{equation*}
$$

Using (7.90), (7.109), and (7.110) we can write

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}} \approx\left|p_{1}\right| \approx \frac{1}{b_{1}}=\frac{1}{\Sigma T_{0}} \tag{7.111}
\end{equation*}
$$

For example, consider the circuit of Fig. 7.24. By inspection,

$$
\begin{equation*}
R_{\pi 0}=r_{\pi} \|\left(R_{S}+r_{b}\right) \tag{7.112}
\end{equation*}
$$

In order to calculate $R_{\mu 0}$ it is necessary to write some simple circuit equations. We apply a test current $i$ at the $C_{\mu}$ terminals as shown in Fig. 7.25 and calculate the resulting $v$.

$$
\begin{align*}
& v_{1}=R_{\pi 0} i  \tag{7.113}\\
& v_{o}=-\left(i+g_{m} v_{1}\right) R_{L} \tag{7.114}
\end{align*}
$$

Substituting (7.113) in (7.114) gives

$$
\begin{equation*}
v_{o}=-\left(i+g_{m} R_{\pi 0} i\right) R_{L} \tag{7.115}
\end{equation*}
$$

Now

$$
R_{\mu 0}=\frac{v}{i}
$$

and

$$
\begin{equation*}
R_{\mu 0}=\frac{v_{1}-v_{o}}{i} \tag{7.116}
\end{equation*}
$$

image_name:Figure 7.25
description:
[
name: RS+rb, type: Resistor, value: RS+rb, ports: {N1: V1, N2: V2}
name: rπ, type: Resistor, value: rπ, ports: {N1: V1, N2: V2}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: V1}
name: i, type: VoltageControlledCurrentSource, value: v, ports: {Np: V2, Nn: Vo}
name: gmv1, type: VoltageControlledCurrentSource, value: gmv1, ports: {Np: V1, Nn: Vo}
]
extrainfo:The circuit is used to calculate the resistance R_{\mu 0} by applying a test current i at the C_{\mu} terminals and measuring the resulting voltage v. The circuit includes resistors RS+rb, rπ, and RL, and two voltage-controlled current sources i and gmv1.

Figure 7.25 Equivalent circuit for the calculation of $R_{\mu 0}$ for Fig. 7.24.

Substitution of (7.113) and (7.115) in (7.116) gives

$$
\begin{equation*}
R_{\mu 0}=R_{\pi 0}+R_{L}+g_{m} R_{L} R_{\pi 0} \tag{7.117}
\end{equation*}
$$

$R_{x 0}$ can be calculated in a similar fashion, and it is apparent that $R_{x 0} \simeq R_{\mu 0}$ if $r_{b} \ll r_{\pi}$. This justifies the common practice of lumping $C_{x}$ in with $C_{\mu}$ if $r_{b}$ is small. Assuming that this is done, (7.111) gives, for the $-3-\mathrm{dB}$ frequency,

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}}=\frac{1}{R_{\pi 0} C_{\pi}+R_{\mu}{ }^{0} C_{\mu}} \tag{7.118}
\end{equation*}
$$

Using (7.117) in (7.118) gives

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}}=\frac{1}{R_{\pi 0}\left\{C_{\pi}+C_{\mu}\left[\left(1+g_{m} R_{L}\right)+\frac{R_{L}}{R_{\pi 0}}\right]\right\}} \tag{7.119}
\end{equation*}
$$

Equation 7.119 is identical with the result obtained in (7.29) by exact analysis. [Recall that $\left(R_{S}+r_{b}\right) \| r_{\pi}$ in (7.29) is the same as $R_{\pi 0}$ in (7.119).] However, the zero-value time-constant analysis gives the result with much less effort. It does not give any information on the nondominant pole.

As a further illustration of the uses and limitations of the zero-value time-constant approach, consider the emitter-follower circuit of Fig. 7.13a, where only the capacitance $C_{\pi}$ has been included. The value of $R_{\pi 0}$ can be calculated by inserting a current source $i$ as shown in Fig. 7.26 and calculating the resulting voltage $v_{1}$ :

$$
\begin{gather*}
i=\frac{v_{1}}{r_{\pi}}+\frac{v_{1}+v_{o}}{R_{S}+r_{b}}  \tag{7.120}\\
\frac{v_{1}}{r_{\pi}}-i+g_{m} v_{1}=\frac{v_{o}}{R_{L}} \tag{7.121}
\end{gather*}
$$

Substituting (7.121) in (7.120) gives

$$
i=\frac{v_{1}}{r_{\pi}}+\frac{v_{1}}{R_{S}+r_{b}}+\frac{R_{L}}{R_{S}+r_{b}}\left(\frac{v_{1}}{r_{\pi}}+g_{m} v_{1}-i\right)
$$

and this equation can be expressed as

$$
i=\frac{v_{1}}{r_{\pi}}+v_{1} \frac{1+g_{m} R_{L}}{R_{S}+r_{b}+R_{L}}
$$

image_name:Figure 7.26 Equivalent circuit for the calculation of R_{\pi 0} for the emitter follower
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: RSrb, N2: GND}
name: rb, type: Resistor, value: rb, ports: {N1: RSrb, N2: rbrπ}
name: rπ, type: Resistor, value: rπ, ports: {N1: rbrπ, N2: Vo}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
name: i, type: CurrentSource, value: i, ports: {Np: rbrπ, Nn: Vo}
name: gₘv₁, type: CurrentSource, value: gₘv₁, ports: {Np: Vo, Nn: GND}
]
extrainfo:The circuit represents an equivalent model for calculating R_{\pi 0} for an emitter follower. It includes resistors RS, rb, rπ, and RL, and current sources i and gₘv₁. The configuration is used to derive equations for the emitter follower's dominant pole and input resistance R_{\pi 0}.

Figure 7.26 Equivalent circuit for the calculation of $R_{\pi 0}$ for the emitter follower.

Finally, $R_{\pi 0}$ can be calculated as

$$
\begin{equation*}
R_{\pi 0}=\frac{v_{1}}{i}=r_{\pi} \| \frac{R_{S}+r_{b}+R_{L}}{1+g_{m} R_{L}} \tag{7.122}
\end{equation*}
$$

Thus the dominant pole of the emitter follower is at

$$
\begin{equation*}
|p|=\frac{1}{R_{\pi 0} C_{\pi}} \tag{7.123}
\end{equation*}
$$

This is in agreement with the result obtained in (7.52) by exact analysis and requires less effort. However, the zero-value time-constant approach tells us nothing of the zero that exact analysis showed. Because of the dominant zero, the dominant-pole magnitude is not the $-3-\mathrm{dB}$ frequency in this case. This shows that care must be exercised in interpreting the results of zero-value time-constant analysis. However, it is a useful technique, and with experience the designer can recognize circuits that are likely to contain dominant zeros. Such circuits usually have a capacitive path directly coupling input and output as $C_{\pi}$ does in the emitter follower.

### 7.3.3 Cascade Voltage-Amplifier Frequency Response

The real advantages of the zero-value time-constant approach appear when circuits containing more than one device are analyzed. For example, consider the two-stage common-source amplifier shown in Fig. 7.27. This circuit could be a drawing of a single-ended amplifier or the differential half-circuit of a fully differential amplifier. Exact analysis of this circuit to find the $-3-\mathrm{dB}$ frequency is extremely arduous, but the zero-value time-constant analysis is quite straightforward, as shown below. To show typical numerical calculations, specific parameter values are assumed. In the example below, as in others in this chapter, parasitic capacitance associated with resistors is neglected. This approximation is often reasonable for monolithic resistors of several thousand ohms or less, but should be checked in each case.

The zero-value time-constant analysis for Fig. 7.27 is carried out in the following example. Analysis of a two-stage common-emitter amplifier would follow similar steps.

#### EXAMPLE

Calculate the $-3-\mathrm{dB}$ frequency of the circuit of Fig. 7.27 assuming the following parameter values:

$$
\begin{aligned}
& R_{S}=10 \mathrm{k} \Omega \quad R_{L 1}=10 \mathrm{k} \Omega \quad R_{L 2}=5 \mathrm{k} \Omega \\
& C_{g s 1}=5 \mathrm{pF} \quad C_{g s 2}=10 \mathrm{pF} \quad C_{g d 1}=C_{g d 2}=1 \mathrm{pF} \\
& C_{d b 1}=C_{d b 2}=2 \mathrm{pF} \quad g_{m 1}=3 \mathrm{~mA} / \mathrm{V} \quad g_{m 2}=6 \mathrm{~mA} / \mathrm{V}
\end{aligned}
$$

Ignore $C_{g b}$ (which is in parallel with $C_{g s}$ and is much smaller than $C_{g s}$ ).
image_name:Figure 7.27
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vs, N2: g1}
name: M1, type: NMOS, ports: {S: GND, D: d1g2, G: g1}
name: RL1, type: Resistor, value: RL1, ports: {N1: d1g2, N2: d1g2}
name: M2, type: NMOS, ports: {S: GND, D: Vo, G: d1g2}
name: RL2, type: Resistor, value: RL2, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a two-stage, common-source cascade amplifier. It amplifies the input voltage Vs to produce the output voltage Vo. The NMOS transistors M1 and M2 are used in each stage to provide amplification, while the resistors RS, RL1, and RL2 are used for biasing and load purposes.

Figure 7.27 Two-stage, common-source cascade amplifier.
image_name:Figure 7.28(a)
description:
[
name: V_s, type: VoltageSource, ports: {Np: V_s, Nn: GND}
name: R_S, type: Resistor, value: R_S, ports: {N1: V_s, N2: V_1}
name: C_gs1, type: Capacitor, value: C_gs1, ports: {Np: V_1, Nn: GND}
name: C_gd1, type: Capacitor, value: C_gd1, ports: {Np: V_1, Nn: V_2}
name: g_m1V_1, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: V_2}
name: C_db1, type: Capacitor, value: C_db1, ports: {Np: V_2, Nn: GND}
name: R_L1, type: Resistor, value: R_L1, ports: {N1: V_2, N2: GND}
name: C_gs2, type: Capacitor, value: C_gs2, ports: {Np: V_2, Nn: GND}
name: C_gd2, type: Capacitor, value: C_gd2, ports: {Np: V_2, Nn: V_o}
name: g_m2V_2, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: V_o}
name: C_db2, type: Capacitor, value: C_db2, ports: {Np: V_o, Nn: GND}
name: R_L2, type: Resistor, value: R_L2, ports: {N1: V_o, N2: GND}
]
extrainfo:The circuit is a small-signal equivalent of a two-stage, common-source cascade amplifier. It includes capacitors for coupling and bypassing, resistors for biasing and loading, and voltage-controlled current sources for amplification. The input voltage is Vs, and the output voltage is Vo.

image_name:(b)
description:
[
name: RA, type: Resistor, value: RA, ports: {N1: Vx, N2: GND}
name: RB, type: Resistor, value: RB, ports: {N1: Vo, N2: GND}
name: g_m v_x, type: VoltageControlledCurrentSource, ports: {Np: Vo, Nn: GND}
]
extrainfo:The circuit is a small-signal equivalent of a two-stage, common-source cascade amplifier. It includes resistors for biasing and loading, and a voltage-controlled current source for amplification. The input voltage is Vx, and the output voltage is Vo. R_gd0 represents the resistance seen by the capacitor C_gd in the original circuit.

Figure 7.28 Small-signal equivalent circuit of Fig. 7.27.
The small-signal equivalent circuit of Fig. 7.27 is shown in Fig. 7.28a. The zero-value time constants for this circuit are determined by calculating the resistance seen by each capacitor across its own terminals. However, significant effort can be saved by recognizing that some capacitors in the circuit are in similar configurations and the same formula can be applied to them. For example, consider $C_{g d 1}$ and $C_{g d 2}$. The resistance seen by either $C_{g d}$ capacitor can be found by calculating the resistance $R_{g d 0}$ in the circuit in Fig. 7.28b. This circuit is the same as the circuit in Fig. 7.25 if we let $R_{A}=R_{\pi 0}$ and $R_{B}=R_{L}$. Therefore, the resistance $R_{g d 0}$ in Fig. 7.28b is given by substituting $R_{A}$ for $R_{\pi 0}$ and $R_{B}$ for $R_{L}$ in (7.117):

$$
\begin{equation*}
R_{g d 0}=R_{A}+R_{B}+g_{m} R_{B} R_{A} \tag{7.124}
\end{equation*}
$$

This equation can be used to find the zero-value time constants for both gate-drain capacitors:

$$
\begin{aligned}
C_{g d 1} R_{g d 01} & =C_{g d 1}\left(R_{S}+R_{L 1}+g_{m 1} R_{L 1} R_{S}\right) \\
& =(1 \mathrm{p})\left[10 \mathrm{k}+10 \mathrm{k}+\left(3 \times 10^{-3}\right)(10 \mathrm{k})(10 \mathrm{k})\right] \mathrm{s}=320 \mathrm{~ns} \\
C_{g d 2} R_{g d 02} & =C_{g d 2}\left(R_{L 1}+R_{L 2}+g_{m 2} R_{L 2} R_{L 1}\right) \\
& =(1 \mathrm{p})\left[10 \mathrm{k}+5 \mathrm{k}+\left(6 \times 10^{-3}\right)(10 \mathrm{k})(5 \mathrm{k})\right] \mathrm{s}=315 \mathrm{~ns}
\end{aligned}
$$

The value of $R_{g s 0}$ for each device can be found by inspection

$$
\begin{gathered}
R_{g s 01}=R_{S} \\
R_{g s 02}=R_{L 1}
\end{gathered}
$$

The corresponding time constants are

$$
\begin{gathered}
C_{g s 1} R_{g s 01}=C_{g s 1} R_{S}=(5 \mathrm{p})(10 \mathrm{k}) \mathrm{s}=50 \mathrm{~ns} \\
C_{g s 2} R_{g s 02}=C_{g s 2} R_{L 1}=(10 \mathrm{p})(10 \mathrm{k}) \mathrm{s}=100 \mathrm{~ns}
\end{gathered}
$$

Also, the value for $R_{d b 0}$ for each device can also be found without computation

$$
\begin{aligned}
& R_{d b 01}=R_{L 1} \\
& R_{d b 02}=R_{L 2}
\end{aligned}
$$

Thus

$$
\begin{gathered}
C_{d b 1} R_{d b 01}=(2 \mathrm{p})(10 \mathrm{k}) \mathrm{s}=20 \mathrm{~ns} \\
C_{d b 2} R_{d b 02}=(2 \mathrm{p})(5 \mathrm{k}) \mathrm{s}=10 \mathrm{~ns}
\end{gathered}
$$

Assuming that the circuit transfer function has a dominant pole, the $-3-\mathrm{dB}$ frequency can be estimated as

$$
\begin{align*}
\omega_{-3 \mathrm{~dB}}=\frac{1}{\sum T_{0}} & =\frac{10^{9}}{320+315+50+100+20+10} \mathrm{rad} / \mathrm{s} \\
& =\frac{10^{9}}{815} \mathrm{rad} / \mathrm{s}=1.2 \times 10^{6} \mathrm{rad} / \mathrm{s} \tag{7.125}
\end{align*}
$$

and therefore

$$
f_{-3 \mathrm{~dB}}=196 \mathrm{kHz}
$$

A computer simulation of this circuit using SPICE gave a $-3-\mathrm{dB}$ frequency of 205 kHz , which is close to the calculated value. The simulation gave three negative real poles with magnitudes $205 \mathrm{kHz}, 4.02 \mathrm{MHz}$, and 39.98 MHz . There were two positive real zeros with magnitudes 477 MHz and 955 MHz . From the simulation, the sum of the reciprocals of the pole magnitudes was 815 ns , which exactly equals the sum of the zero-value time constants as calculated by hand.

An exact analysis of Fig. 7.28a would first apply KCL at three nodes and produce a transfer function with a third-order denominator, in which some coefficients would consist of a sum of many products of small-signal model parameters. Many simplifying approximations would be needed to give useful design equations. As the circuit complexity increases, the number of equations increases and the order of the denominator increases, eventually making exact analysis by hand impractical and making time-constant analysis quite attractive.

The foregoing analytical result was obtained with relatively small effort and the calculation has focused on the contributions to the $-3-\mathrm{dB}$ frequency from the various capacitors in the circuit. In this example, as is usually the case in a cascade of this kind, the time constants associated with the gate-drain capacitances are the major contributors to the $-3-\mathrm{dB}$ frequency of the circuit. One of the major benefits of the zero-value time-constant analysis is the information it gives on the circuit elements that most affect the $-3-d B$ frequency of the circuit.

In the preceding calculation, we assumed that the circuit of Fig. 7.28 had a dominant pole. The significance of this assumption will now be examined in more detail. For purposes of illustration, assume that capacitors $C_{g d 1}, C_{g d 2}, C_{d b 1}$, and $C_{d b 2}$ in Fig. 7.28 are zero and that $R_{S}=R_{L 1}=R_{L 2}$ and $C_{g s 1}=C_{g s 2}$. Then the circuit has two identical stages, and each will contribute a pole with the same magnitude; that is, a dominant-pole situation does not exist because the circuit has two identical poles. However, inclusion of nonzero $C_{g d 1}$ and $C_{g d 2}$ tends to cause these poles to split apart and produces a dominant-pole situation. (See Chapter 9.) For this reason, most practical circuits of this kind do have a dominant pole, and the zero-value time-constant analysis gives a good estimate of $\omega_{-3 \mathrm{~dB}}$. Even if the circuit has two identical poles, however, the zero-value time-constant analysis is still useful. Equations 7.85 and 7.109 are valid in general, and thus

$$
\begin{equation*}
\Sigma T_{0}=\sum_{i=1}^{n}\left(-\frac{1}{p_{i}}\right) \tag{7.126}
\end{equation*}
$$

is always true. That is, the sum of the zero-value time constants equals the sum of the negative reciprocals of all the poles whether or not a dominant pole exists. Consider a circuit with two
identical negative real poles with magnitudes $\omega_{x}$. Then the gain magnitude of the circuit is

$$
\begin{equation*}
|G(j \omega)|=\frac{G_{0}}{1+\left(\frac{\omega}{\omega_{x}}\right)^{2}} \tag{7.127}
\end{equation*}
$$

The -3-dB frequency of this circuit is the frequency where $|G(j \omega)|=G_{0} / \sqrt{2}$, which can be shown to be

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}}=\omega_{x} \sqrt{\sqrt{2}-1}=0.64 \omega_{x} \tag{7.128}
\end{equation*}
$$

The zero-value time-constant approach predicts

$$
\Sigma T_{0}=\frac{2}{\omega_{x}}
$$

and thus

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}}=\frac{1}{\Sigma T_{0}}=0.5 \omega_{x} \tag{7.129}
\end{equation*}
$$

Even in this extreme case, the prediction is only 22 percent in error and gives a pessimistic estimate.

### 7.3.4 Cascode Frequency Response

The cascode connection is a multiple-device configuration that is useful in high-frequency applications. An ac schematic of a bipolar version, shown in Fig. 7.29a, consists of a
image_name:(a)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: Rs, type: Resistor, value: Rs, ports: {N1: Vs, N2: b1}
name: Q1, type: NPN, ports: {C: vx, B: b1, E: GND}
name: Q2, type: NPN, ports: {C: Vout, B: GND, E: vx}
]
extrainfo:The diagram shows a cascode amplifier using bipolar junction transistors. Q1 is configured in a common-emitter stage, driving Q2 in a common-base stage. The voltage gain is approximately -gm1*RL.
image_name:(b)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: Rs, type: Resistor, value: Rs, ports: {N1: Vs, N2: gi}
name: M1, type: NMOS, ports: {S: GND, D: vx, G: g1}
name: M2, type: NMOS, ports: {S: vx, D: Vo, G: GND}
name: Ri2, type: Resistor, value: Ri2, ports: {N1: vx, N2: Vi}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:This is a MOS cascode circuit with a common-source stage driving a common-gate stage. The input voltage is applied at the gate of M1, and the output is taken across RL. M2 acts as a current buffer.

Figure 7.29 Cascode circuit connections (a) bipolar and (b) MOS.
common-emitter stage driving a common-base stage. An MOS version, shown in Fig. 7.29b, consists of a common-source stage driving a common-gate stage. In both circuits, transistor $T_{2}$ operates as a current buffer. Therefore, the voltage gain of the cascode circuit is approximately

$$
\begin{equation*}
\frac{v_{o}}{v_{i}} \approx-g_{m 1} R_{L} \tag{7.130}
\end{equation*}
$$

assuming that the output resistance of the cascode circuit is large compared to $R_{L}$. This result is the same as the voltage gain for a common-emitter or common-source stage without the current buffer $T_{2}$. The cascode derives its advantage at high frequencies from the fact that the load for transistor $T_{1}$ is the low input impedance of the current buffer. This impedance at low frequencies was shown in Sections 3.3.3 and 3.3.4 to be

$$
\begin{equation*}
R_{i 2} \approx \frac{1}{g_{m 2}} \tag{7.131}
\end{equation*}
$$

if $r_{o 2} \rightarrow \infty$, ignoring body effect in the MOS transistor and assuming $r_{b} /\left(\beta_{0}+1\right) \ll 1 / g_{m 2}$ and $\beta_{0} \gg 1$ for the bipolar transistor. If transistors $T_{1}$ and $T_{2}$ have equal bias currents and device dimensions, then $g_{m 1}=g_{m 2}$. Since the load resistance seen by $T_{1}$ is about $1 / g_{m 2}$, the magnitude of the voltage gain from $v_{i}$ to $v_{x}$ is about unity. Thus the influence of the Miller effect on $T_{1}$ is minimal, even for fairly large values of $R_{L}$. Since the current-buffer stage $T_{2}$ has a wide bandwidth (see Section 7.2.4), the cascode circuit overall has good high-frequency performance when compared to a single common-emitter or common-source stage, especially for large $R_{L}$. (See Problems 7.29 and 7.30.)

If the assumption that $r_{o 2} \rightarrow \infty$ is removed, the magnitude of the voltage gain from $v_{i}$ to $v_{x}$ can be larger than one. For example, $R_{L}$ might be the output resistance of a cascoded current source in an amplifier stage. In this case, $R_{L}$ is large compared to $r_{o 2}$, and the input resistance of the current buffer $T_{2}$ is given by

$$
\begin{equation*}
R_{i 2} \approx \frac{1}{g_{m 2}}+\frac{1}{g_{m 2}} \frac{R_{L}}{r_{o 2}} \tag{7.132}
\end{equation*}
$$

from Section 3.3.5.1 [ignoring body effect in the MOS transistor and assuming $r_{b} /\left(\beta_{0}+1\right) \ll$ $1 / g_{m 2}$ and $\beta_{0} \gg 1$ for the bipolar transistor]. Since this resistance is significantly bigger than $1 / g_{m 2}$ when $R_{L} \gg r_{o 2}$, the magnitude of the gain from $v_{i}$ to $v_{x}$ can be significantly larger than one. However, this gain is still much smaller in magnitude than the gain from $v_{i}$ to $v_{o}$; therefore, the Miller effect on $T_{1}$ is smaller with the cascode transistor $T_{2}$ than without it. To further reduce the Miller effect when $R_{L}$ is large, the input resistance of the current buffer in (7.132) can be reduced by replacing the cascode transistor with the active cascode shown in Chapter 3.

A useful characteristic of the cascode is the small amount of reverse transmission that occurs in the circuit. The current-buffer stage provides good isolation that is required in highfrequency tuned-amplifier applications. Another useful characteristic of the cascode is its high output resistance. This characteristic is used to advantage in current-source design, as described in Chapter 4, and in operational amplifier design, as described in Chapter 6.

As an example of the calculation of the -3-dB frequency of a cascode amplifier, consider the circuit of Fig. 7.30. The input differential pair is biased using a resistor $R_{3}$. If commonmode rejection is an important consideration, $R_{3}$ can be replaced with an active current source. The resistive divider composed of $R_{1}$ and $R_{2}$ sets the bias voltage at the bases of $Q_{3}$ and $Q_{4}$, and this voltage is chosen to give adequate collector-emitter bias voltage for each device.

For purposes of analysis, the circuit is assumed driven with source resistance $R_{S}$ from each base to ground. If the base of $Q_{2}$ is grounded, the frequency response of the circuit is not greatly affected if $R_{S}$ is small. The circuit of Fig. 7.30 can be analyzed using the ac differential
image_name:Figure 7.30 Cascode differential amplifier
description:The circuit is a cascode differential amplifier with NPN transistors Q1, Q2, Q3, and Q4. The resistive divider composed of R1 and R2 sets the bias voltage at the bases of Q3 and Q4. The circuit is driven by a source voltage Vs through a resistor RS. The load resistors RL are connected to the collectors of Q3 and Q4. Capacitors C1 and C2 are used for coupling. The circuit is powered by VCC and VEE voltage sources.

Figure 7.30 Cascode differential amplifier.
half-circuit of Fig. 7.31a. Note that in forming the differential half-circuit, the common-base point of $Q_{3}$ and $Q_{4}$ is assumed to be a virtual ground for differential signals. The frequency response $\left(v_{o} / v_{s}\right)(j \omega)$ of the circuit of Fig. 7.31 $a$ will be the same as that of Fig. 7.30 if $R_{3}$ in Fig. 7.30 is large enough to give a reasonable value of common-mode rejection. The smallsignal equivalent circuit of Fig. 7.31 $a$ is shown in Fig. 7.31b.
image_name:(a)
description:The circuit is a small-signal equivalent of a differential amplifier. It includes transistors Q1 and Q3, resistors, capacitors, and controlled sources to model transistor behavior. The circuit is designed to analyze frequency response and gain characteristics.
image_name:(b)
description:This circuit is a small-signal equivalent model of a differential amplifier. It includes transistors Q1 and Q3, resistors, capacitors, and voltage-controlled current sources. The circuit is designed to analyze the frequency response and gain.
Figure 7.31 (a) The ac differential half-circuit of Fig. 7.30. (b) Small-signal equivalent of the circuit in (a).

#### EXAMPLE

Calculate the low-frequency, small-signal gain and $-3-\mathrm{dB}$ frequency of the circuit of Fig. 7.30 using the following data: $R_{S}=1 \mathrm{k} \Omega, R_{E}=75 \Omega, R_{3}=4 \mathrm{k} \Omega, R_{L}=1 \mathrm{k} \Omega$, $R_{1}=4 \mathrm{k} \Omega, R_{2}=10 \mathrm{k} \Omega$, and $V_{C C}=V_{E E}=10 \mathrm{~V}$. Device data are $\beta=200, V_{B E(\mathrm{on})}=0.7 \mathrm{~V}$, $\tau_{F}=0.25 \mathrm{~ns}, r_{b}=200 \Omega, r_{c}($ active region $)=150 \Omega, C_{j e 0}=1.3 \mathrm{pF}, C_{\mu 0}=0.6 \mathrm{pF}, \psi_{0 c}=$ $0.6 \mathrm{~V}, C_{c s} 0=2 \mathrm{pF}, \psi_{0 s}=0.58 \mathrm{~V}$, and $n_{s}=0.5$.

The dc bias conditions are first calculated neglecting transistor base currents. The voltage at the base of $Q_{3}$ and $Q_{4}$ is

$$
V_{B 3}=V_{C C}-\frac{R_{1}}{R_{1}+R_{2}}\left(V_{C C}+V_{E E}\right)=10-\frac{4}{14} \times 20=4.3 \mathrm{~V}
$$

The voltage at the collectors of $Q_{1}$ and $Q_{2}$ is

$$
V_{C 1}=V_{B 3}-V_{B E 3(\mathrm{on})}=3.6 \mathrm{~V}
$$

Assuming that the bases of $Q_{1}$ and $Q_{2}$ are grounded, we can calculate the collector currents of $Q_{1}$ and $Q_{2}$ as

$$
I_{C 1}=\frac{V_{E E}-V_{B E(\mathrm{on})}}{2 R_{3}+R_{E}}=\frac{10-0.7}{8.075} \mathrm{~mA}=1.15 \mathrm{~mA}
$$

Therefore, we have

$$
I_{C 1}=I_{C 2}=I_{C 3}=I_{C 4}=1.15 \mathrm{~mA}
$$

The dc analysis is completed by noting that the voltage at the collectors of $Q_{3}$ and $Q_{4}$ is

$$
V_{C 3}=V_{C C}-I_{C 3} R_{L}=10 \mathrm{~V}-1.15 \mathrm{~V}=8.85 \mathrm{~V}
$$

The low-frequency gain can be calculated from the ac differential half-circuit of Fig. 7.31a, using the results derived in Chapter 3 for a stage with emitter resistance. If we neglect base resistance, the small-signal transconductance of $Q_{1}$ including $R_{E}$ is given by (3.93) as

$$
G_{m 1} \approx \frac{g_{m 1}}{1+g_{m 1} R_{E}}=10.24 \mathrm{~mA} / \mathrm{V}
$$

The small-signal input resistance of $Q_{1}$ including $R_{E}$ is given by (3.90) as

$$
R_{i 1} \approx r_{\pi 1}+(\beta+1) R_{E}=19.5 \mathrm{k} \Omega
$$

As shown in Chapter 3, the common-base stage has a current gain of approximately unity, and thus the small-signal collector current of $Q_{1}$ appears in the collector of $Q_{3}$. By inspection, the voltage gain of the circuit of Fig. 7.31 $a$ is

$$
\frac{v_{o}}{v_{s}}=-\frac{R_{i 1}}{R_{i 1}+R_{S}} G_{m 1} R_{L}=-\frac{19.5}{19.5+1} \times 10.24 \times 1=-9.74
$$

To calculate the $-3-\mathrm{dB}$ frequency of the circuit, the parameters in the small-signal equivalent circuit of Fig. $7.31 b$ must be determined. The resistive parameters are $g_{m 1}=g_{m 3}=$ $q I_{C 1} / k T=44.2 \mathrm{~mA} / \mathrm{V}, r_{\pi 1}=r_{\pi 3}=\beta / g_{m 1}=4525 \Omega, r_{c 1}=r_{c 3}=150 \Omega, r_{b 1}=r_{b 3}=$ $200 \Omega$, and $R_{S}+r_{b}=1.2 \mathrm{k} \Omega$. Because of the low resistances in the circuit, transistor output resistances are neglected.

The capacitive elements in Fig. $7.31 b$ are calculated as described in Chapter 1. First consider base-emitter, depletion-layer capacitance $C_{j e}$. As described in Chapter 1, the value of $C_{j e}$ in the forward-active region is difficult to estimate, and a reasonable approximation is to double $C_{j e 0}$. This gives $C_{j e}=2.6 \mathrm{pF}$. From (1.104) the base-charging capacitance for $Q_{1}$ is

$$
C_{b 1}=\tau_{F} g_{m 1}=0.25 \times 10^{-9} \times 44.2 \times 10^{-3} \mathrm{~F}=11.1 \mathrm{pF}
$$

Use of (1.118) gives

$$
C_{\pi 1}=C_{b 1}+C_{j e 1}=13.7 \mathrm{pF}
$$

Since the collector currents of $Q_{1}$ and $Q_{3}$ are equal, $C_{\pi 3}=C_{\pi 1}=13.7 \mathrm{pF}$.
The collector-base capacitance $C_{\mu 1}$ of $Q_{1}$ can be calculated using (1.117a) and noting that the collector-base bias voltage of $Q_{1}$ is $V_{C B 1}=3.6 \mathrm{~V}$. Thus

$$
C_{\mu 1}=\frac{C_{\mu 0}}{\sqrt{1+\frac{V_{C B}}{\psi_{0 c}}}}=\frac{0.6}{\sqrt{1+\frac{3.6}{0.6}}} \mathrm{pF}=0.23 \mathrm{pF}
$$

The collector-substrate capacitance of $Q_{1}$ can also be calculated using (1.117a) with a collectorsubstrate voltage of $V_{C S}=V_{C 1}+V_{E E}=13.6 \mathrm{~V}$. (The substrate is assumed connected to the negative supply voltage.) Thus we have

$$
C_{c s 1}=\frac{C_{c s 0}}{\sqrt{1+\frac{V_{C S}}{\psi_{0 s}}}}=\frac{2}{\sqrt{1+\frac{13.6}{0.58}}} \mathrm{pF}=0.40 \mathrm{pF}
$$

Similar calculations show that the parameters of $Q_{3}$ are $C_{\mu 3}=0.20 \mathrm{pF}$ and $C_{c s 3}=$ 0.35 pF .

The $-3-\mathrm{dB}$ frequency of the circuit can now be estimated by calculating the zero-value time constants for the circuit. First consider $C_{\pi 1}$. The resistance seen across its terminals is given by (7.122), which was derived for the emitter follower. The presence of resistance in series with the collector of $Q_{1}$ makes no difference to the calculation because of the infinite impedance of the current generator $g_{m 1} v_{1}$. Thus from (7.122)

$$
R_{\pi 01}=r_{\pi 1} \| \frac{R_{S}+r_{b 1}+R_{E}}{1+g_{m 1} R_{E}}=\left(4525 \| \frac{1000+200+75}{1+44.2 \times 0.075}\right) \Omega=(4525 \| 295) \Omega=277 \Omega
$$

Note that the effect of $R_{E}$ is to reduce $R_{\pi 01}$, which increases the bandwidth of the circuit by reducing the zero-value time constant associated with $C_{\pi 1}$. This time constant has a value

$$
C_{\pi 1} R_{\pi 01}=13.7 \times 0.277 \mathrm{~ns}=3.79 \mathrm{~ns}
$$

The collector-substrate capacitance of $Q_{1}$ sees a resistance equal to $r_{c 1}$ plus the common-base stage input resistance, which is

$$
R_{i 3}=\frac{1}{g_{m 3}}+\frac{r_{b 3}}{\beta+1}=23.6 \Omega
$$

and thus $C_{c s 1}$ sees a resistance

$$
R_{c s 01}=R_{i 3}+r_{c 1}=174 \Omega
$$

The zero-value time constant is

$$
C_{c s 1} R_{c s 01}=0.4 \times 0.174 \mathrm{~ns}=0.07 \mathrm{~ns}
$$

The zero-value time constant associated with $C_{\mu 1}$ of $Q_{1}$ can be determined by calculating the resistance $R_{\mu 01}$ seen across the terminals of $C_{\mu 1}$ using the equivalent circuit of Fig. 7.32a. To simplify the analysis, the circuit in Fig. 7.32a is transformed into the circuit of Fig. 7.32b, where the transistor with emitter degeneration is represented by parameters $R_{i 1}$ and $G_{m 1}$, which were defined previously. The circuit of Fig. $7.32 b$ is in the form of a common-emitter stage as shown in Fig. 7.25, and the formula derived for that case can be used now. Thus from (7.117)

$$
\begin{equation*}
R_{\mu 01}=R_{1}+R_{L 1}+G_{m 1} R_{L 1} R_{1} \tag{7.133}
\end{equation*}
$$

image_name:Figure 7.32 (a)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: X2}
name: rb, type: Resistor, value: rb, ports: {N1: GND, N2: X2}
name: rπ1, type: Resistor, value: rπ1, ports: {N1: X2, N2: X1}
name: RE, type: Resistor, value: RE, ports: {N1: X1, N2: GND}
name: RL1, type: Resistor, value: RL1, ports: {N1: LOAD, N2: GND}
name: Rμ01, type: Resistor, value: Rμ01, ports: {N1: LOAD, N2: GND}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: X1, Nn: GND}
name: gm1V1, type: CurrentControlledCurrentSource, ports: {Np: LOAD, Nn: GND}
name: Gm1Vi, type: CurrentControlledCurrentSource, ports: {Np: LOAD, Nn: GND}
]
extrainfo:The circuit in Figure 7.32(a) is a common-emitter stage with emitter degeneration. It includes resistors, a current source, and current-controlled current sources. The circuit is used to calculate the resistance Rμ01 for transistor Q1.
image_name:Figure 7.32 (b)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: Vi, N2: GND}
name: rb, type: Resistor, value: rb, ports: {N1: Vi, N2: GND}
name: Ri1, type: Resistor, value: Ri1, ports: {N1: Vi, N2: GND}
name: RL1, type: Resistor, value: RL1, ports: {N1: LOAD, N2: GND}
name: Rμ01, type: Resistor, value: Rμ01, ports: {N1: LOAD, N2: GND}
name: Gm1Vi, type: VoltageControlledCurrentSource, ports: {Np: LOAD, Nn: GND}
]
extrainfo:The circuit in Fig. 7.32b represents a common-emitter stage with parameters Ri1 and Gm1. The equivalent load resistance RL1 is given as 174 Ω. The circuit is transformed from a more complex one with emitter degeneration.

Figure 7.32 (a) Circuit for the calculation of $R_{\mu 01}$ for $Q_{1}$. (b) Equivalent circuit for the circuit in (a).
where

$$
R_{1}=R_{i 1} \|\left(R_{S}+r_{b}\right)=(19.5 \| 1.2) \mathrm{k} \Omega=1.13 \mathrm{k} \Omega
$$

The load resistance $R_{L 1}$ is just $r_{c 1}$ plus the input resistance of $Q_{3}$. Using the previously calculated values, we obtain

$$
R_{L 1}=174 \Omega
$$

Substituting into (7.133) gives

$$
R_{\mu 01}=[1.13+0.17+(10.24 \times 1.13 \times 0.17)] \mathrm{k} \Omega=3.27 \mathrm{k} \Omega
$$

The zero-value time constant associated with $C_{\mu 1}$ is thus

$$
C_{\mu 1} R_{\mu 01}=0.23 \times 3.27 \mathrm{~ns}=0.75 \mathrm{~ns}
$$

Because the input impedance of the common-base stage is small, the contribution of $C_{\mu 1}$ to the sum of the zero value time constants is much smaller than that due to $C_{\pi 1}$.

The time constant associated with $C_{\pi 3}$ of $Q_{3}$ can be calculated by recognizing that (7.122) derived for the emitter follower also applies here. The effective source resistance $R_{S}$ is zero as the base is grounded, and the effective emitter resistance $R_{L}$ is infinite because the collector of $Q_{1}$ is connected to the emitter of $Q_{3}$. Thus (7.122) gives

$$
R_{\pi 03}=r_{\pi 3} \| \frac{1}{g_{m 3}}=22.6 \Omega
$$

The zero-value time constant associated with $C_{\pi 3}$ is thus

$$
C_{\pi 3} R_{\pi 03}=13.7 \times 0.0023 \mathrm{~ns}=0.32 \mathrm{~ns}
$$

The time constant associated with collector-base capacitance $C_{\mu 3}$ of $Q_{3}$ can be calculated using (7.133) with $G_{m 1}$ equal to zero since the effective value of $R_{E}$ is infinite in this case. In (7.133) the effective value of $R_{1}$ is just $r_{b}$ and thus

$$
R_{\mu 03}=r_{b}+R_{L 3}
$$

where

$$
R_{L 3}=r_{c 3}+R_{L}
$$

and $R_{L 3}$ is the load resistance seen by $Q_{3}$. Thus

$$
R_{\mu 03}=[200+150+1000] \Omega=1.35 \mathrm{k} \Omega
$$

and the time constant is

$$
C_{\mu 3} R_{\mu 03}=0.2 \times 1.35 \mathrm{~ns}=0.27 \mathrm{~ns}
$$

Finally, the collector-substrate capacitance of $Q_{3}$ sees a resistance

$$
R_{c s} 03=r_{c 3}+R_{L}=1.15 \mathrm{k} \Omega
$$

and

$$
C_{c s 3} R_{c s 03}=0.35 \times 1.15 \mathrm{~ns}=0.4 \mathrm{~ns}
$$

The sum of the zero-value time constants is thus

$$
\Sigma T_{0}=(3.79+0.07+0.75+0.32+0.27+0.4) \mathrm{ns}=5.60 \mathrm{~ns}
$$

The $-3-\mathrm{dB}$ frequency is estimated as

$$
f_{-3 \mathrm{~dB}}=\frac{1}{2 \pi \Sigma T_{0}}=28.4 \mathrm{MHz}
$$

Computer simulation of this circuit using SPICE gave a $-3-\mathrm{dB}$ frequency of 34.7 MHz . The computer simulation showed six poles, of which the first two were negative real poles with magnitudes 35.8 MHz and 253 MHz . The zero-value time constant analysis has thus given a reasonable estimate of the $-3-\mathrm{dB}$ frequency and has also shown that the major limitation on the circuit frequency response comes from $C_{\pi 1}$ of $Q_{1}$. The circuit can thus be broadbanded even further by increasing resistance $R_{E}$ in the emitter of $Q_{1}$, since the calculation of $R_{\pi 01}$ showed that increasing $R_{E}$ will reduce the value of $R_{\pi} 01$. Note that this change will reduce the gain of the circuit.

Further useful information regarding the circuit frequency response can be obtained from the previous calculations by recognizing that $Q_{3}$ in Fig. 7.31 effectively isolates $C_{\mu 3}$ and $C_{c s 3}$ from the rest of the circuit. In fact, if $r_{b 3}$ is zero then these two capacitors are connected in parallel across the output and will contribute a separate pole to the transfer function. The magnitude of this pole can be estimated by summing zero-value time constants for $C_{\mu 3}$ and $C_{c s 3}$ alone to give $\Sigma T_{0}=0.67 \mathrm{~ns}$. This time constant corresponds to a pole with magnitude $1 /\left(2 \pi \Sigma T_{0}\right)=237 \mathrm{MHz}$, which is very close to the second pole calculated by the computer. The dominant pole would then be estimated by summing the rest of the time constants to give $\Sigma T_{0}=4.93 \mathrm{~ns}$, which corresponds to a pole with magnitude 32.3 MHz and is also close to the computer-calculated value. This technique can be used any time a high degree of isolation
exists between various portions of a circuit. To estimate the dominant pole of a given section, the zero-value time constants may be summed for that section.

In this example, the bandwidth of the differential-mode gain was estimated by computing the zero-value time constants for the differential half-circuit. The bandwidth of the commonmode gain could be estimated by computing the zero-value time constants for the commonmode half-circuit.

### 7.3.5 Frequency Response of a Current Mirror Loading a Differential Pair

A CMOS differential pair with current-mirror load is shown in Fig. 7.33a. The current mirror here introduces a pole and a zero that are not widely separated. To show this result, consider the simplified small-signal circuit in Fig. 7.33 b for finding the transconductance $G_{m}=i_{o} / v_{i d}$ with $v_{o}=0$. The circuit has been simplified by letting $r_{o} \rightarrow \infty$ for all transistors and ignoring
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: Y, D: X, G: in+}
name: M2, type: NMOS, ports: {S: Y, D: Vo, G: in-}
name: M3, type: PMOS, ports: {S: VDD, D: X, G: X}
name: M4, type: PMOS, ports: {S: VDD, D: Vo, G: X}
name: I_TAIL, type: CurrentSource, value: I_TAIL, ports: {Np: Y, Nn: GND}
name: 1/gm3, type: Resistor, value: 1/gm3, ports: {N1: X, N2: GND}
name: Cx, type: Capacitor, value: Cx, ports: {Np: X, Nn: GND}
name: Vid/2, type: VoltageSource, value: Vid/2, ports: {Np: V1, Nn: GND}
]
extrainfo:The circuit is a CMOS differential pair with a current-mirror load. It consists of NMOS transistors M1 and M2 forming the differential pair, and PMOS transistors M3 and M4 forming the current mirror load. The current source I_TAIL provides the bias current. The node Y is at AC ground for differential input signals. The circuit introduces a pole and a zero due to the capacitance Cx at node X.
image_name:(b)
description:The circuit diagram (b) is a simplified small-signal model of a CMOS differential pair with a current-mirror load. It shows the transconductance calculation with a pole and zero introduced by the current mirror. The capacitance C_x models the total capacitance at node X, and the zero-value time constant associated with C_x is T_0 = C_x / g_m3. Node Y is an AC ground with a purely differential input.
Figure 7.33 (a) Differential pair with current-mirror load and (b) a simplified small-signal model.
all capacitors except $C_{x}$. Here $C_{x}$ models the total capacitance from node $X$ to ground, which consists of $C_{g s 3}, C_{g s 4}$, and other smaller capacitances. With a purely differential input, node $Y$ is an ac ground. The zero-value time constant associated with $C_{x}$ is $T_{0}=C_{x} / g_{m 3}$; therefore,

$$
\begin{equation*}
p=-\frac{g_{m 3}}{C_{x}} \tag{7.134}
\end{equation*}
$$

An exact analysis of this circuit yields a transfer function with a pole given by (7.134) and a zero at $z=-2 g_{m 3} / C_{x}$. (See Problem 7.48.) The magnitudes of the pole and zero are separated by one octave. The magnitude and phase responses for $G_{m}(s)$ are plotted in Fig. 7.34. The phase shift from this pole-zero pair is between 0 and -19.4 degrees.

The frequency-response plot can be explained as follows. The drain currents in the differential pair are $i_{d 1}=g_{m 1} v_{i d} / 2$ and $i_{d 2}=-g_{m 1} v_{i d} / 2$. At low frequencies, $M_{3}$ and $M_{4}$ mirror $i_{d 1}$, giving for the output current

$$
\begin{equation*}
i_{o}=-i_{d 2}-i_{d 4}=-i_{d 2}+i_{d 1}=g_{m 1} v_{i d} \tag{7.135}
\end{equation*}
$$

image_name:(a)
description:The graph presented is a Bode plot representing the magnitude response of the transconductance, denoted as \(|G_m|\), versus frequency. It is a typical representation used in control systems and electronics to analyze frequency response.

1. **Axes Labels and Units:**
- The horizontal axis is labeled "Frequency (rad/s)," indicating that it represents frequency in radians per second. The scale is logarithmic, which is common for Bode plots to cover a wide range of frequencies.
- The vertical axis is labeled \(|G_m|\), which represents the magnitude of the transconductance. The values on this axis are typically in linear scale.

2. **Overall Behavior and Trends:**
- At low frequencies, the magnitude \(|G_m|\) is constant and equal to \(g_{m1}\). This indicates that the transconductance is stable and unaffected by frequency at these low values.
- As the frequency increases, the magnitude begins to decrease, showing a downward slope. This behavior is indicative of a system experiencing a roll-off, which is typical when approaching a pole in the system.
- At high frequencies, the magnitude levels off to a value of \(g_{m1}/2\), suggesting that the system has reached a new steady-state response at these higher frequencies.

3. **Key Features and Technical Details:**
- The graph shows a clear transition region where the slope changes, indicating the presence of a pole-zero pair. The magnitude drop is associated with this pair, affecting the system’s response.
- The magnitude change from \(g_{m1}\) to \(g_{m1}/2\) suggests a halving of the transconductance at high frequencies.

4. **Annotations and Specific Data Points:**
- The plot includes markers labeled \(|p|\) and \(|z|\) on the frequency axis, which likely denote the frequencies of the pole and zero, respectively. These are critical points where the system's behavior changes noticeably.
- The graph does not specify exact numerical values for these frequencies, but their relative positions indicate the frequency range over which the transition occurs.

This Bode plot effectively illustrates how the transconductance \(G_m\) behaves across different frequency ranges, showing both the stable low-frequency response and the reduced high-frequency response due to the pole-zero pair.

(a)
image_name:(b)
description:The graph in question is a Bode plot representing the phase response of the transconductance \( G_m = i_o / v_{id} \) as a function of frequency. The x-axis is labeled 'Frequency (rad/s)' and is likely on a logarithmic scale, although this is not explicitly shown. The y-axis is labeled '∠G_m (degrees)' and represents the phase angle of the transconductance in degrees.

Overall Behavior and Trends:
The phase plot starts at 0° at low frequencies, indicating that there is no phase shift initially. As the frequency increases, the phase begins to decrease, reaching a minimum value of approximately -19.4° at a certain frequency range. This dip in phase corresponds to the influence of a pole-zero pair, which is marked on the plot as \(|p|\|z|\), suggesting that the pole and zero are closely spaced in frequency.

After reaching the minimum, the phase begins to recover and approaches back towards 0° as the frequency continues to increase. This trend indicates a phase lag introduced by the pole-zero pair, which is characteristic of such a system.

Key Features and Technical Details:
- **Initial Phase:** 0° at low frequencies.
- **Minimum Phase:** Approximately -19.4° at a certain frequency range.
- **Frequency Range of Interest:** Marked by \(|p|\|z|\), indicating the critical region where the pole-zero pair has a significant effect on the phase.
- **Phase Recovery:** The phase returns towards 0° at higher frequencies, showing the system's tendency to stabilize in phase response beyond the influence of the pole-zero pair.

Annotations:
- A dashed line is drawn at -19.4° to highlight the minimum phase shift.
- The critical frequency range is annotated with \(|p|\|z|\), emphasizing the region of significant phase change due to the pole-zero pair.

This phase plot provides insight into how the transconductance's phase response changes with frequency, highlighting the impact of the pole-zero pair on the system's behavior.

(b)

Figure 7.34 (a) Magnitude and (b) phase versus frequency of the transconductance $G_{m}=i_{o} / v_{i d}$ for the circuit in Fig. 7.33.

At high frequencies $(\omega \rightarrow \infty), C_{x}$ becomes a short, so $v_{g s 4} \rightarrow 0$ and $i_{d 4} \rightarrow 0$. Therefore,

$$
\begin{equation*}
i_{o}=-i_{d 2}-i_{d 4}=-i_{d 2}-0=\frac{g_{m 1} v_{i d}}{2} \tag{7.136}
\end{equation*}
$$

These equations show that the transconductance falls from $g_{m 1}$ at low frequencies to $g_{m 1} / 2$ at high frequencies. This result stems from the observation that the current mirror does not contribute to the output current when $C_{x}$ becomes a short. The change in the transconductance occurs between frequencies $|p|$ and $|z|$. This analysis shows that the pole and zero are both important in this circuit. Since $C_{x} \approx C_{g s 3}+C_{g s 4}=2 C_{g s 3}$, (7.134) gives $|p| \approx g_{m 3} / 2 C_{g s 3} \approx$ $\omega_{T\left(M_{3}\right)} / 2$. Therefore, the pole-zero pair has an effect only at very high frequencies, and the effect of this pair is much less than that of either an isolated pole or zero.

Analysis of a bipolar version of the circuit in Fig. 7.33a gives a similar result.

### 7.3.6 Short-Circuit Time Constants

Zero-value time-constant analysis (which is sometimes called open-circuit time-constant analysis) can be used to estimate the smallest-magnitude pole of an amplifier. This estimated pole magnitude is approximately equal to the $-3-\mathrm{dB}$ frequency of the gain of a dc-coupled amplifier with a low-pass transfer function. Another type of time-constant analysis is called short-circuit time-constant analysis. Short-circuit time constants can be used to estimate the location of the largest-magnitude pole. While short-circuit time-constant analysis is often used to estimate the lower $-3-\mathrm{dB}$ frequency in ac-coupled amplifiers, ${ }^{1,2}$ we will use these time constants to estimate the magnitude of the nondominant pole in dc-coupled amplifiers that have only two widely spaced, real poles.

The short-circuit time-constant formulas will be derived for the small-signal circuit in Fig. 7.24. Equations 7.91 to 7.93 describe this circuit, and (7.94) is the determinant $\Delta(s)$ of these equations. This determinant can be written as

$$
\begin{align*}
\Delta(s) & =K_{3}\left(s^{3}+\frac{K_{2}}{K_{3}} s^{2}+\frac{K_{1}}{K_{3}} s+\frac{K_{0}}{K_{3}}\right)  \tag{7.137}\\
& =K_{3}\left(s-p_{1}\right)\left(s-p_{2}\right)\left(s-p_{3}\right)
\end{align*}
$$

since the zeros of $\Delta(s)$ are the poles of the transfer function. Expanding the right-most expression and equating the coefficients of $s^{2}$ gives

$$
\begin{equation*}
\frac{K_{2}}{K_{3}}=-\sum_{i=1}^{3} p_{i} \tag{7.138}
\end{equation*}
$$

Now a formula for calculating $K_{2} / K_{3}$ will be derived. Evaluating the determinant of the circuit equations in (7.91) to (7.93), the term $K_{3}$ that multiplies $s^{3}$ in (7.94) is given by

$$
\begin{equation*}
K_{3}=C_{\pi} C_{\mu} C_{x} \tag{7.139}
\end{equation*}
$$

and the $K_{2}$ term is

$$
\begin{equation*}
K_{2}=g_{11} C_{\mu} C_{x}+g_{22} C_{\pi} C_{x}+g_{33} C_{\pi} C_{\mu} \tag{7.140}
\end{equation*}
$$

From (7.139) and (7.140), the ratio $K_{2} / K_{3}$ is

$$
\begin{equation*}
\frac{K_{2}}{K_{3}}=\frac{g_{11}}{C_{\pi}}+\frac{g_{22}}{C_{\mu}}+\frac{g_{33}}{C_{x}}=\frac{1}{r_{11} C_{\pi}}+\frac{1}{r_{22} C_{\mu}}+\frac{1}{r_{33} C_{x}} \tag{7.141}
\end{equation*}
$$

where $r_{i i}=1 / g_{i i}$. Now, let us examine each term in the right-most expression. The first term is $1 /\left(r_{11} C_{\pi}\right)$. Using (7.91), $r_{11}=1 / g_{11}$ can be found as

$$
\begin{equation*}
r_{11}=\frac{1}{g_{11}}=\left.\frac{v_{1}}{i_{1}}\right|_{v_{2}=v_{3}=0, C_{\pi}=0} \tag{7.142}
\end{equation*}
$$

That is, $r_{11}$ is the resistance in parallel with $C_{\pi}$, computed with $C_{\pi}$ removed from the circuit and with the other capacitors $C_{\mu}$ and $C_{x}$ shorted. (Note that shorting $C_{\mu}$ makes $v_{2}=0$; shorting $C_{x}$ makes $v_{3}=0$.) Therefore, the product $r_{11} C_{\pi}$ is called the short-circuit time constant for capacitor $C_{\pi}$. Similarly, from (7.92)

$$
\begin{equation*}
r_{22}=\frac{1}{g_{22}}=\left.\frac{v_{2}}{i_{2}}\right|_{v_{1}=v_{3}=0, C_{\mu}=0} \tag{7.143}
\end{equation*}
$$

This $r_{22}$ is the resistance in parallel with $C_{\mu}$, computed with $C_{\mu}$ removed from the circuit and with the other capacitors $C_{\pi}$ and $C_{x}$ shorted. Finally, from (7.93)

$$
\begin{equation*}
r_{33}=\frac{1}{g_{33}}=\left.\frac{v_{3}}{i_{3}}\right|_{v_{1}=v_{2}=0, C_{x}=0} \tag{7.144}
\end{equation*}
$$

So $r_{33}$ is the resistance in parallel with $C_{x}$, computed with $C_{x}$ removed from the circuit and with the other capacitors $C_{\pi}$ and $C_{\mu}$ shorted. Using (7.142) to (7.144), (7.141) can be rewritten as

$$
\begin{equation*}
\frac{K_{2}}{K_{3}}=\sum_{i=1}^{3} \frac{1}{\tau_{s i}} \tag{7.145}
\end{equation*}
$$

where $\tau_{s i}$ is the short-circuit time constant associated with the $i^{\text {th }}$ capacitor in the circuit. The short-circuit time constant for the $i^{\text {th }}$ capacitor is found by multiplying its capacitance by the driving-point resistance in parallel with the $i^{\text {th }}$ capacitor, computed with all other capacitors shorted.

Combining (7.138) and (7.145) gives

$$
\begin{equation*}
\sum_{i=1}^{3} p_{i}=-\sum_{i=1}^{3} \frac{1}{\tau_{s i}} \tag{7.146}
\end{equation*}
$$

This key equation relates the sum of the poles and the sum of the reciprocals of the short-circuit time constants. This relationship holds true for any small-signal circuit that consists of resistors, capacitors, and controlled sources, assuming that the circuit has no loops of capacitors. ${ }^{1}$

If a circuit has $n$ poles and pole $p_{n}$ has a magnitude that is much larger than the magnitude of every other pole, then a general version of (7.146) can be written as

$$
\begin{equation*}
p_{n} \approx \sum_{i=1}^{n} p_{i}=-\sum \frac{1}{\tau_{s i}} \tag{7.147}
\end{equation*}
$$

For a circuit that has only two widely spaced, real poles, (7.147) simplifies to

$$
\begin{equation*}
p_{2} \approx-\sum \frac{1}{\tau_{s i}} \tag{7.148}
\end{equation*}
$$

This simple relationship allows the magnitude of the nondominant pole to be readily estimated from the short-circuit time constants.

#### EXAMPLE

Estimate the nondominant pole magnitude for the circuit in Fig. 7.35 with

$$
\begin{gathered}
R_{S}=10 \mathrm{k} \Omega \quad R_{L}=10 \mathrm{k} \Omega \\
C_{g s}=1 \mathrm{pF} \quad C_{f}=20 \mathrm{pF} \quad g_{m}=3 \mathrm{~mA} / \mathrm{V}
\end{gathered}
$$

image_name:Figure 7.35
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vs, N2: X1}
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: X1, Nn: GND}
name: Cf, type: Capacitor, value: Cf, ports: {Np: X1, Nn: Vo}
name: gmV1, type: VoltageControlledCurrentSource, ports: {Np: Vp, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a basic amplifier configuration with feedback capacitor Cf and two resistors RS and RL. It includes a voltage-controlled current source gmV1.

Figure 7.35 Example circuit for calculating short-circuit time constants.

This circuit has two poles because it has two independent capacitors. First, we will calculate the short-circuit time constant $\tau_{s 1}$ for $C_{f}$. With $C_{g s}$ shorted and the independent source set to zero, we have $v_{1}=0$, so the current through the dependent source is also zero. Therefore, the resistance seen by $C_{f}$ is just $R_{L}$, and the corresponding time constant is

$$
\tau_{s 1}=C_{f} R_{L}=(20 \mathrm{pF})(10 \mathrm{k} \Omega)=200 \mathrm{~ns}
$$

To find the short-circuit time constant for $C_{g s}$, we short $C_{f}$ and find the resistance seen by $C_{g s}$. With $C_{f}$ shorted, the dependent source is controlled by the voltage across it; therefore, it acts as a resistance of $1 / g_{m}$. This resistance is in parallel with $R_{L}$ and $R_{S}$, so the short-circuit time constant for $C_{g s}$ is

$$
\begin{equation*}
\tau_{s 2}=C_{g s}\left[R_{S}\left\|1 / g_{m}\right\| R_{L}\right]=(1 \mathrm{pF})[10 \mathrm{k} \Omega\|333 \Omega\| 10 \mathrm{k} \Omega]=0.312 \mathrm{~ns} \tag{7.149}
\end{equation*}
$$

From (7.148),

$$
\begin{equation*}
p_{2} \approx-\sum \frac{1}{\tau_{s i}}=-\left(\frac{1}{200 \mathrm{~ns}}+\frac{1}{0.312 \mathrm{~ns}}\right)=-3.21 \mathrm{Grad} / \mathrm{s} \tag{7.150}
\end{equation*}
$$

if the poles are real and widely spaced. An exact analysis of this circuit gives $p_{2}=$ $-3.20 \mathrm{Grad} / \mathrm{s}$, which is very close to the estimate above, and $p_{1}=-156 \mathrm{krad} / \mathrm{s}$.

Using zero-value time constants, the dominant-pole magnitude can be estimated. From (7.124), the zero-value time constant for $C_{f}$ is

$$
\begin{align*}
C_{f} R_{f 0} & =C_{f}\left(R_{S}+R_{L}+g_{m} R_{L} R_{S}\right)  \tag{7.151}\\
& =(20 \mathrm{p})\left[10 \mathrm{k}+10 \mathrm{k}+\left(3 \times 10^{-3}\right)(10 \mathrm{k})(10 \mathrm{k})\right] \mathrm{s}=6.4 \mu \mathrm{~s}
\end{align*}
$$

The zero-value time constant for $C_{g s}$ is simply

$$
C_{g s} R_{S}=(1 \mathrm{pF})(10 \mathrm{k} \Omega)=10 \mathrm{~ns}
$$

Therefore, (7.111) gives

$$
p_{1} \approx-\frac{1}{6.4 \mu \mathrm{~s}+10 \mathrm{~ns}}=-156 \mathrm{krad} / \mathrm{s}
$$

Exact analysis of this circuit gives $p_{1}=-156 \mathrm{krad} / \mathrm{s}$, which is the same as the estimate above. This example demonstrates that for circuits with two widely spaced, real poles, time constant analyses can give accurate estimates of the magnitudes of the dominant and nondominant poles.

In this case of widely spaced poles, note that $p_{1}$ and $p_{2}$ can be accurately estimated using only one time constant for each pole. Since $C_{f}$ is large compared to $C_{g s}$ and the resistance $C_{f}$ sees when computing its zero-value time constant is large compared to the resistance seen by $C_{g s}$, a reasonable conclusion is that $C_{g s}$ has negligible effect near the frequency $\left|p_{1}\right|$. Therefore,
the most important zero-value time constant in (7.111) for estimating $p_{1}$ is the time constant for $C_{f}$ (computed with $C_{g s}$ replaced with an open circuit). Using only that time constant from (7.151), we estimate

$$
p_{1} \approx-\frac{1}{6.4 \mu \mathrm{~s}}=-156 \mathrm{krad} / \mathrm{s}
$$

which is a very accurate estimate of $p_{1}$.
If the real poles are widely separated and the dominant pole was set by $C_{f}$, a reasonable assumption is that $C_{f}$ is a short circuit near the frequency $\left|p_{2}\right|$. Therefore, the important shortcircuit time constant in (7.150) is the time constant for $C_{g s}$, computed with $C_{f}$ shorted. Using only that time constant from (7.149) in (7.148) gives

$$
p_{2} \approx-\frac{1}{0.312 \mathrm{~ns}}=-3.21 \mathrm{Grad} / \mathrm{s}
$$

which is an accurate estimate of $p_{2}$.
This last set of calculations shows that if two real poles are widely spaced and if one capacitor is primarily responsible for $p_{1}$ and another capacitor is responsible for $p_{2}$, we need only compute one zero-value time constant to estimate $p_{1}$ and one short-circuit time constant to estimate $p_{2}$.

## 7.4 Analysis of the Frequency Response of the NE5234 Op Amp

Up to this point, the analysis of the frequency response of integrated circuits has been limited to fairly simple configurations. The reason for this is apparent in previous sections, where the large amount of calculation required to estimate the dominant pole of some simple circuits was illustrated. A complete frequency analysis by hand of a large integrated circuit is thus out of the question. However, a circuit designer often needs insight into the frequency response of large circuits such as the NE5234 op amp, and, by making some sensible approximations, the methods of analysis described previously can be used to provide such information. We will now illustrate this point by analyzing the frequency response of the NE5234.

### 7.4.1 High-Frequency Equivalent Circuit of the NE5234

Schematics of the stages in the NE5234 are shown Chapter 6. Its frequency response is dominated by the $5.5-\mathrm{pF}$ integrated capacitor $C_{22}$ in Fig. 6.37, which is a compensation capacitor designed to prevent the circuit from oscillating when connected in a feedback loop. The choice of $C_{22}$ and its function are described in Chapter 9.

Since the NE5234 contains more than seventy interconnected transistors, a complete analysis is not attempted even using zero-value time-constant techniques. In order to obtain an estimate of the frequency response of this circuit, the circuit designer must be able to recognize those parts of the circuit that have little or no influence on the frequency response and to discard them from the analysis. As a general rule, elements involved in the bias circuit can often be eliminated. This approach leads to the ac schematic of Fig. 7.36, which is adequate for an approximate calculation of the high-frequency behavior of the NE5234 assuming that the common-mode input voltage, $V_{I C}$, is low enough that $Q_{1}$ and $Q_{2}$ in Fig. 6.36 are off.

All bias elements have been eliminated. When the magnitude of the load current is large, either $Q_{74}$ or $Q_{75}$ in the output stage will be regulated by the circuit in Fig. 6.41 to conduct a current that is almost constant as shown by (6.162) and (6.163), depending on the polarity of the load current. The frequency response of the circuit will be slightly different in these two cases.
image_name:Figure 7.36
description:This circuit represents the high-frequency gain path of the NE5234. It includes multiple NPN and PNP transistors, resistors, and capacitors. The circuit is designed to regulate the load current and has a specific frequency response. The DC load current is assumed to be 1 mA, and Q75 is omitted for simplicity.

Figure 7.36 An ac schematic of the high-frequency gain path of the NE5234 assuming that $V_{I C}$ is low enough that $Q_{1}$ and $Q_{2}$ in Fig. 6.36 are off.

Here, the dc load current is assumed to be $I_{L}=1 \mathrm{~mA}$ as in the calculations in Chapter 6. Therefore, $Q_{75}$ conducts a nearly constant current and is omitted in Fig. 7.36 along with the circuits that control it for simplicity. From the standpoint of finding the op-amp bandwidth, the major effect of these circuits is to double the transconductance of the second stage in the NE5234, as explained with Fig. 6.48 and included in the calculation below. This simplification is the major approximation in Fig. 7.36, and computer simulation shows that it is a reasonable approximation.

As mentioned above, the frequency response of the NE5234 is dominated by $C_{22}$, and the $-3-\mathrm{dB}$ frequency can be estimated by considering the effect of this capacitance alone. However, as described in Chapter 9, the presence of poles other than the dominant one has a crucial effect on the behavior of the circuit when feedback is applied. The magnitude of the nondominant poles is thus of considerable interest, and their magnitudes can be determined by simulation.

### 7.4.2 Calculation of the -3-dB Frequency of the NE5234

The $-3-\mathrm{dB}$ frequency of the circuit of Fig. 7.36 can be estimated by calculating the zerovalue resistance $R_{c 22,0}$ seen by $C_{22}$. This capacitor is connected between the input of the second stage at node 10 and the op-amp output. Resistance $R_{c 22,0}$ can be calculated from the equivalent circuit of Fig. 7.37. Here, $R_{o 1}$ is the output resistance of the first stage of the NE5234, and $R_{i 2}, G_{m 2}$, and $R_{o 2}$ are the input resistance, transconductance, and output resistance of the
image_name:Figure 7.37
description:The circuit is designed to calculate the zero-value time constant for C22. It includes resistors and voltage-controlled current sources to model the behavior of the op-amp stages. The resistors Ro1, Ro2, Ro3, and RL are part of the equivalent circuit, while Gm2vi2 and Gm3vi3 represent the transconductance of the second and third stages respectively.

Figure 7.37 Circuit for the calculation of the zero-value time constantfor $C_{22}$.
second stage, respectively. Similarly, $R_{i 3(25)}, G_{m 3}$, and $R_{o 3}$, are the input resistance from node 25 , transconductance, and output resistance of the third stage. Finally, $R_{L}$ is the load resistance connected to the op-amp output. These quantities were calculated or given in Chapter 6 as follows:

$$
\begin{aligned}
R_{o 1} & =11 \mathrm{M} \Omega & R_{i 3(25)} & =404 \mathrm{k} \Omega \\
R_{i 2} / 2 & =650 \mathrm{k} \Omega & G_{m 3} & =1 / 96 \mathrm{~A} / \mathrm{V} \\
G_{m 2} & =2 \times 170 \mu \mathrm{~A} / \mathrm{V} & R_{o 3} & =15 \mathrm{k} \Omega \\
R_{o 2} & =2.2 \mathrm{M} \Omega & R_{L} & =2 \mathrm{k} \Omega
\end{aligned}
$$

The circuit of Fig. 7.37 is similar to the circuit in Fig. 7.25 except that the output voltagecontrolled current source, $G_{m 3} v_{i 3}$, is not controlled directly by the input voltage, $v_{i 2}$. Instead, $v_{i 2}$ controls the voltage-controlled current source in the model of the second stage, $G_{m 2} v_{i 2}$. The current from this source flows in $R_{o 2} \| R_{i 3(25)}$, generating the input voltage of the third stage, $v_{i 3}$, which controls $G_{m 3} v_{i 3}$. As a result, the effective transconductance from the input to the output in Fig. 7.37 is $G_{m(\mathrm{eff})}=G_{m 2}\left(R_{o 2} \| R_{i 3(25)}\right) G_{m 3}=2 \times 170 \times(2.2 \| 0.404) /(96 \Omega)=1.2 \mathrm{~A} / \mathrm{V}$. Then $R_{c 22,0}$ can be found using this effective transconductance in (7.117)

$$
\begin{align*}
R_{c 22,0} & =R_{o 1}\left\|\frac{R_{i 2}}{2}+R_{o 3}\right\| R_{L}+G_{m(\mathrm{eff})}\left(R_{o 1} \| \frac{R_{i 2}}{2}\right)\left(R_{o 3} \| R_{L}\right) \\
& =\left[11\|0.65+0.015\| 0.002+\left(1.2 \times(11 \| 0.65) \times(15 \| 2) \times 10^{3}\right)\right] \mathrm{M} \Omega \\
& =1.3 \times 10^{9} \Omega \tag{7.152}
\end{align*}
$$

This extremely large resistance when combined with $C_{22}=5.5 \mathrm{pF}$ gives a time constant

$$
C_{22} R_{c 22,0}=5.5 \times 10^{-12} \times 1.3 \times 10^{9} \mathrm{~s}=7.2 \times 10^{-3} \mathrm{~s}
$$

This totally dominates the sum of the zero-value time constants and gives a $-3-\mathrm{dB}$ frequency of

$$
f_{-3 \mathrm{~dB}}=\frac{1}{2 \pi C_{22} R_{c 22,0}}=22 \mathrm{~Hz}
$$

A computer simulation of the complete NE5234 gave $f_{-3 \mathrm{~dB}}=21 \mathrm{~Hz}$.
An alternative means of calculating the effect of the frequency compensation is using the Miller effect as described in Section 7.2.1. The compensation capacitor is connected from node 10 to the output, and the voltage gain between these two points can be calculated from the equivalent circuit of Fig. 7.37:

$$
\begin{equation*}
A_{v}=\frac{v_{o}}{v_{i 2}}=-G_{m(\mathrm{eff})}\left(R_{o 3} \| R_{L}\right) \tag{7.153}
\end{equation*}
$$

From (7.5) the Miller capacitance seen at node 10 is

$$
\begin{equation*}
C_{M}=\left(1-A_{v}\right) C_{22} \tag{7.154}
\end{equation*}
$$

and substitution of (7.153) in (7.154) gives

$$
\begin{aligned}
C_{M} & =\left[1+G_{m(\mathrm{eff})}\left(R_{o 3} \| R_{L}\right)\right] C_{22} \\
& =\left[1+\left(1.2 \times(15 \| 2) \times 10^{3}\right)\right] \times 5.5 \mathrm{pF} \\
& =12,000 \mathrm{pF}
\end{aligned}
$$

This extremely large effective capacitance swamps all other capacitances and, when combined with resistance $R_{o 1} \|\left(R_{i 2} / 2\right)=610 \mathrm{k} \Omega$ from node 10 to ground, gives a $-3-\mathrm{dB}$ frequency for the circuit of

$$
\begin{aligned}
f_{-3 \mathrm{~dB}} & =\frac{1}{2 \pi C_{M}\left(R_{o 1} \| \frac{R_{i 2}}{2}\right)} \\
& =\frac{1}{2 \pi \times 12,000 \times 10^{-12} \times 610 \times 10^{3}} \mathrm{~Hz} \\
& =22 \mathrm{~Hz}
\end{aligned}
$$

This is the same value as predicted by the zero-value time-constant approach.

### 7.4.3 Nondominant Poles of the NE5234

The foregoing calculations have shown that the $5.5-\mathrm{pF}$ compensation capacitor produces a dominant pole in the NE5234 with a magnitude of about $2 \pi(22) \mathrm{rad} / \mathrm{sec}$. From the complexity of the circuit, it is evident that there will be a large number of poles with larger magnitudes. Although calculation of the locations of these higher frequency poles is quite difficult, computer simulations show that they contribute negative phase shift at the unity-gain frequency of the amplifier.

## 7.5 Relation Between Frequency Response and Time Response

In this chapter the effect of increasing signal frequency on circuit performance has been illustrated by considering the circuit response to a sinusoidal input signal. In practice, however, an amplifier may be required to amplify nonsinusoidal signals such as pulse trains or square waves. In addition, such signals are often used in testing circuit frequency response. The response of a circuit to such input signals is thus of some interest and will now be calculated.

Initially we consider a circuit whose small-signal transfer function can be approximated by a single-pole expression

$$
\begin{equation*}
\frac{v_{o}}{v_{i}}(s)=\frac{K}{1-\frac{s}{p_{1}}} \tag{7.156}
\end{equation*}
$$

where $K$ is the low-frequency gain and $p_{1}$ is the pole of the transfer function. As described earlier, the $-3-\mathrm{dB}$ frequency of this circuit for sinusoidal signals is $\omega_{-3 \mathrm{~dB}}=-p_{1}$. Now consider a small input voltage step of amplitude $v_{a}$ applied to the circuit. If we assume that the circuit responds linearly, we can use (7.156) to calculate the circuit response using $v_{i}(s)=v_{a} / s$. Thus

$$
v_{o}(s)=\frac{K v_{a}}{s} \frac{1}{1-\frac{s}{p_{1}}}=K v_{a}\left(\frac{1}{s}-\frac{1}{s-p_{1}}\right)
$$

image_name:Figure 7.38 (a)
description:This graph is a time-domain waveform showing the step response of a linear circuit with gain \( K \) and a single-pole transfer function. It consists of two main plots: the input voltage \( v_i(t) \) and the output voltage \( v_o(t) \).

1. **Type of Graph and Function:**
- The graph is a time-domain waveform illustrating the step response of the circuit.

2. **Axes Labels and Units:**
- The horizontal axis represents time \( t \), and the vertical axes represent voltage. The top plot has the vertical axis labeled as \( v_i \), and the bottom plot has it labeled as \( v_o \).
- No specific units are provided, but it is implied that time is in seconds and voltage is in volts.

3. **Overall Behavior and Trends:**
- **Input Voltage \( v_i(t) \):** The input voltage is a step function that jumps from 0 to \( v_a \) at \( t = 0 \) and remains constant.
- **Output Voltage \( v_o(t) \):** The output voltage starts at 0 and rises exponentially towards \( K v_a \). It asymptotically approaches this value over time.

4. **Key Features and Technical Details:**
- The output voltage \( v_o(t) \) is described by the equation \( v_o(t) = K v_a (1 - e^{p_1 t}) \).
- The time constant of the exponential response is \( -1/p_1 \).
- The graph indicates the rise time \( t_r \), which is the time taken for \( v_o(t) \) to rise from 10% to 90% of its final value \( K v_a \).
- The rise time \( t_r \) is marked between two points: \( 0.1 K v_a \) at time \( t_1 \) and \( 0.9 K v_a \) at time \( t_2 \).

5. **Annotations and Specific Data Points:**
- The graph includes horizontal dashed lines at \( 0.1 K v_a \) and \( 0.9 K v_a \) to indicate the levels corresponding to 10% and 90% of the final value.
- The rise time \( t_r \) is annotated as the interval between \( t_1 \) and \( t_2 \), highlighting the 10% to 90% rise time.

Figure 7.38 (a) Step response of a linear circuit with gain $K$ and a single-pole transfer function.
and the circuit response to a step input is

$$
\begin{equation*}
v_{o}(t)=K v_{a}\left(1-e^{p_{1} t}\right) \tag{7.157}
\end{equation*}
$$

The output voltage thus approaches $K v_{a}$ and the time constant of the exponential in (7.157) is $-1 / p_{1}$. Equation 7.157 is sketched in Fig. $7.38 a$ together with $v_{i}$. The rise time of the output is usually specified by the time taken to go from 10 percent to 90 percent of the final value. From (7.157) we have

$$
\begin{align*}
& 0.1 K v_{a}=K v_{a}\left(1-e^{p_{1} t_{1}}\right)  \tag{7.158}\\
& 0.9 K v_{a}=K v_{a}\left(1-e^{p_{1} t_{2}}\right) \tag{7.159}
\end{align*}
$$

From (7.158) and (7.159) we obtain, for the 10 percent to 90 percent rise time,

$$
\begin{equation*}
t_{r}=t_{2}-t_{1}=-\frac{1}{p_{1}} \ln 9=\frac{2.2}{\omega_{-3 \mathrm{~dB}}}=\frac{0.35}{f_{-3 \mathrm{~dB}}} \tag{7.160}
\end{equation*}
$$

This equation shows that the pulse rise time is directly related to the $-3-\mathrm{dB}$ frequency of the circuit. For example, if $f_{-3 \mathrm{~dB}}=10 \mathrm{MHz}$, then (7.160) predicts $t_{r}=35 \mathrm{~ns}$. If a square wave is applied to a circuit with a single-pole transfer function, the response is as shown in Fig. 7.38b. The edges of the square wave are rounded as described above for a single pulse.

The calculations in this section have shown the relation between frequency response and time response for small signals applied to a circuit with a single-pole transfer function. For circuits with multiple-pole transfer functions, the same general trends apply, but the pulse response may differ greatly from that shown in Fig. 7.38. In particular, if the circuit transfer function contains complex poles leading to a frequency response with a high-frequency peak (see Chapter 9), then the pulse response will exhibit overshoot ${ }^{3}$ and damped sinusoidal oscillation as shown in Fig. 7.39. Such a response is usually undesirable in pulse amplifiers.

Finally, it should be pointed out that all the foregoing results were derived on the assumption that the applied signals were small in the sense that the amplifier acted linearly. If the applied pulse is large enough to cause nonlinear operation of the circuit, the pulse response may differ significantly from that predicted here. This point is discussed further in Chapter 9.
image_name:Figure 7.38 (b)
description:The graph in Figure 7.38 (b) is a time-domain waveform illustrating the response of a linear circuit with a single-pole to a square-wave input.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform.
- It shows the input and output of a linear circuit.

2. **Axes Labels and Units:**
- The horizontal axis represents time (t), though specific units are not provided.
- The vertical axis for the input signal is labeled \( v_i \), indicating input voltage.
- The vertical axis for the output signal is labeled \( v_o \), indicating output voltage.

3. **Overall Behavior and Trends:**
- The input waveform is a square wave, characterized by abrupt transitions between high and low levels.
- The output waveform exhibits a typical response of a single-pole system to a square wave, showing an exponential rise and fall.
- The output does not instantaneously follow the input but instead shows a gradual change, indicating a lag due to the circuit's time constant.

4. **Key Features and Technical Details:**
- The output waveform starts with an exponential rise when the input switches from low to high.
- As the input returns to low, the output decreases exponentially.
- The response shows no oscillations, which is typical for a single-pole system.
- The waveform suggests a time constant that defines the rate of change in the output.

5. **Annotations and Specific Data Points:**
- No specific numerical values or annotations are provided on the graph.
- The graph visually demonstrates the lag and smoothing effect of the single-pole filter on a square-wave input.

image_name:Figure 7.38 (b)
description:Figure 7.38 (b) depicts the response of a linear circuit with a single-pole when subjected to a square-wave input. This graph is a time-domain waveform, illustrating how the output voltage \( V_o \) responds over time \( t \) to a changing input. The horizontal axis represents time \( t \), and the vertical axis represents the output voltage \( V_o \). Both axes are likely in linear scale, though specific units are not provided.

The graph shows a characteristic response typical of a single-pole low-pass filter. When the input changes from low to high, the output voltage increases exponentially, demonstrating a smooth rise without oscillations. This behavior is indicative of a first-order system's time constant, which defines the rate of change in the output. As the input returns to low, the output decreases exponentially back towards the baseline.

The waveform suggests that the system effectively smooths the transitions of the square-wave input, resulting in a lagged and smoothed output that lacks the sharp edges of the input signal. This smoothing effect is due to the filter's inherent property of attenuating high-frequency components, allowing only lower-frequency components to pass through.

There are no specific numerical values, annotations, or markers provided on the graph. The primary focus is on the qualitative behavior, illustrating the lag and smoothing effect of the single-pole filter on the square-wave input.

Figure 7.38 (b) Response of a linear circuit with a single-pole when a square-wave input is applied.
image_name:Figure 7.39
description:Figure 7.39 illustrates the typical step response of a linear circuit with complex poles. The graph is a time-domain waveform showing the output voltage \( v_o \) on the vertical axis and time \( t \) on the horizontal axis. Both axes appear to use linear scales, although specific units are not provided.

The graph starts at the origin, indicating that the initial output voltage is zero. As time progresses, the output voltage rises sharply, reaching a peak. This initial peak is followed by a series of damped oscillations, characterized by a gradual decrease in amplitude over time. The waveform eventually settles into a steady state, where the output voltage becomes constant, indicating the system's final equilibrium state.

Key features of this response include the overshoot at the initial peak, the subsequent oscillations, and the eventual stabilization. The behavior depicted suggests that the circuit is underdamped, as evidenced by the overshoot and oscillations before reaching steady state. No specific numerical values, annotations, or markers are provided on the graph, and the focus is on the qualitative behavior of the circuit's response to a step input.

Figure 7.39 Typical step response of a linear circuit whose transfer function contains complex poles.
