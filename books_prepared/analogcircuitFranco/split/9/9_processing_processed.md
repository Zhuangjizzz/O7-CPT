# Effect of Negative Feedback on the Frequency Bandwidth

Negative feedback has a profound effect also on the frequency response. In fact, if used carelessly, it may lead to unwanted oscillation, in which case suitable measures need to be taken to stabilize the system. Though the subject of stability will be treated in detail later in this chapter, here we examine the effect of feedback upon two op amp representatives, the voltage-feedback amplifier (VFA) and the current-feedback amplifier (CFA).

Let us start out with the noninverting VFA configuration of Fig. 7.2, repeated in Fig. 7.10a for convenience. As seen in Chapter 6, the open-loop gain of the VFA is of the type

$$
\begin{equation*}
a(j f) \cong \frac{a_{0}}{1+j f / f_{b}} \tag{7.19}
\end{equation*}
$$

image_name:(a)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: InN(a), N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vo, N2: InN(a)}
name: VFA, type: OpAmp, value: a, ports: {InP: Vi, InN: InN(a), OutP: Vo, OutN: GND}
]
extrainfo:The circuit is a noninverting voltage-feedback amplifier (VFA) configuration. It uses an operational amplifier with feedback resistors R1 and R2 to set the gain.

(a)
image_name:Figure 7.10b
description:The graph in Figure 7.10b is a Bode plot representing the gain of an operational amplifier in both open-loop and closed-loop configurations. The vertical axis is labeled 'Gain' and is measured in decibels (dB), while the horizontal axis represents frequency, denoted by 'f', likely in hertz (Hz). The frequency axis is on a logarithmic scale, which is typical for Bode plots.

Overall Behavior and Trends:
- **Open-Loop Gain (|a|):** The plot shows a high open-loop gain, denoted as \(|a_0|\), which remains constant from direct current (DC) up to a frequency \(f_b\). Beyond \(f_b\), the open-loop gain \(|a|\) decreases at a rate of \(-20 \text{ dB/decade}\), indicating a single-pole roll-off characteristic.
- **Closed-Loop Gain (|A|):** The closed-loop gain, denoted as \(|A_0|\), is constant over the frequency range shown and is lower than the open-loop gain. It remains flat and does not follow the roll-off of the open-loop gain.

Key Features and Technical Details:
- **Cutoff Frequency (\(f_b\)):** This is the frequency at which the open-loop gain begins to decrease. It marks the boundary between the constant gain region and the roll-off region.
- **Unity Gain Bandwidth (\(f_t\)):** Though not explicitly marked, it is typically the frequency where the open-loop gain crosses 0 dB if the graph extends to it.
- **Slope of Roll-Off:** The slope of the open-loop gain decrease is \(-20 \text{ dB/decade}\), typical for a first-order system.

Annotations and Specific Data Points:
- The plot includes annotations indicating the gain levels \(|a_0|\) and \(|A_0|\) and the slope of the open-loop gain roll-off.
- Vertical lines at \(f_b\) and \(f_B\) mark significant points in the frequency response.

FIGURE 7.10 (a) Noninverting VFA configuration. (b) Visualizing the open-Ioop response $|a|$ and the closed-loop response $|A|$, both in dB.
where $f$ is the input-signal frequency, $a_{0}$ is the $d c$ gain, and $f_{b}$ is the open-loop bandwidth. As depicted in Fig. 7.10b, the gain $a$ is high $\left(\cong a_{0}\right)$ from dc up to $f_{b}$, after which it rolls off with $f$ at the rate of $-20 \mathrm{~dB} /$ decade. As we know, an important figure of merit of such an amplifier is its gain-bandwidth product

$$
\begin{equation*}
\mathrm{GBP}=a_{0} \times f_{b}=f_{t} \tag{7.20}
\end{equation*}
$$

For instance, the popular 741 op amp has $a_{0}=200,000 \mathrm{~V} / \mathrm{V}$ and $f_{b}=5 \mathrm{~Hz}$, so GBP $=200,000 \times 5=1 \mathrm{MHz}$. The closed-loop gain is, by Eqs. (7.6) and (7.7),

$$
A(j f)=\frac{V_{o}}{V_{i}}=\frac{1}{b} \frac{1}{1+\frac{1+j f / f_{b}}{b a_{0}}}=\frac{1}{b} \times \frac{1}{1+1 /\left(b a_{0}\right)} \times \frac{1}{1+\frac{j f}{\left(1+b a_{0}\right) f_{b}}}
$$

where $b=1 /\left(1+R_{2} / R_{1}\right)$, by Eq. (7.13). This is put in the more insightful form

$$
\begin{equation*}
A(j f)=\frac{A_{0}}{1+j f / f_{B}} \tag{7.21}
\end{equation*}
$$

where

$$
\begin{equation*}
A_{0}=\left(1+\frac{R_{2}}{R_{1}}\right) \times \frac{1}{1+1 /\left(b a_{0}\right)} \cong 1+\frac{R_{2}}{R_{1}} \tag{7.22}
\end{equation*}
$$

is the already familiar closed-loop dc gain, and

$$
\begin{equation*}
f_{B}=\left(1+b a_{0}\right) f_{b} \cong \frac{a_{0}}{A_{0}} f_{b}=\frac{f_{t}}{A_{0}} \tag{7.23}
\end{equation*}
$$

is the closed-loop bandwidth. (Again, note the use of lower-case letters to designate open-loop parameters, and upper-case letters to designate their closed-loop counterparts.) With reference to Fig. $7.10 b$ we observe that negative feedback, while reducing the dc gain from $a_{0}$ to $A_{0} \cong 1+R_{2} / R_{1}$, also expands the bandwidth from $f_{b}$ to $f_{B} \cong\left(a_{0} / A_{0}\right) f_{b}$, so the closed-loop GBP $\left(=A_{0} \times f_{B}=f_{t}\right)$ remains constant. Gainbandwidth tradeoff is exploited on purpose by the circuit designer to control amplifier dynamics.

EXAMPLE 7.6 (a) Let the non-inverting op amp of Fig. 7.2 be implemented with the popular 741 op amp , for which $a_{0}=200,000 \mathrm{~V} / \mathrm{V}$ and $f_{b}=5 \mathrm{~Hz}$. Estimate $A_{0}$ and $f_{B}$ if $R_{1}=1.0 \mathrm{k} \Omega$ and $R_{2}=999 \mathrm{k} \Omega$.
(b) Repeat if $R_{2}$ is lowered to $9.0 \mathrm{k} \Omega$.
(c) What is the closed-loop gain that results in the widest closed-loop bandwidth?

#### Solution

(a) We have $A_{0} \cong 1 / b=1+R_{2} / R_{1}=1+999 / 1=1000 \mathrm{~V} / \mathrm{V}, a_{0} b=200,000 /$ $1000=200$, and $f_{B}=\left(1+a_{0} b\right) f_{b}=(1+200) 5 \cong 1.0 \mathrm{kHz}$.
(b) We now have $A_{0} \cong 10 \mathrm{~V} / \mathrm{V}, a_{0} b=20,000$, and $f_{B} \cong 100 \mathrm{kHz}$. Compared to part (a), $A_{0}$ has been reduced by two decades while $f_{B}$ has been increased by two decades.
(c) The widest bandwidth is achieved with $b=1$, that is, when we configure the op amp as a unity-gain voltage follower by replacing $R_{2}$ with a wire and removing $R_{1}$ altogether. Then, $A_{0} \cong 1 \mathrm{~V} / \mathrm{V}, a_{0} b=a_{0} \times 1=a_{0}$, and $f_{B}=$ $\left(1+a_{0}\right) f_{b} \cong a_{0} f_{b}=f_{t}=1 \mathrm{MHz}$.

Next, let us turn to the CFA amplifier of Fig. 7.11a. Recall from Eq. (6.114) that the CFA's open loop transimpedance gain is of the type

$$
\begin{equation*}
z(j f) \cong \frac{R_{e q}}{1+j f / f_{b}} \tag{7.24}
\end{equation*}
$$

where $f$ is the input-signal frequency, $R_{e q}$ is the dc gain, and $f_{b}$ is the open-loop bandwidth (the magnitude plot of $z$ is repeated in Fig. 7.11b for convenience). To find the closed-loop gain $A(j f)$, we adapt the expression for $A$ derived in Section 5.6, but with $R_{e q}$ replaced by $z(j f)$. The result is

$$
\begin{aligned}
A(j f) & =\frac{V_{o}}{V_{i}}=\left(1+\frac{R_{2}}{R_{1}}\right) \times \frac{1}{1+\frac{R_{2}\left(1+j f / f_{b}\right)}{R_{e q}}} \\
& =\left(1+\frac{R_{2}}{R_{1}}\right) \times \frac{1}{1+R_{2} / R_{e q}} \times \frac{1}{1+\frac{j f}{\left(1+R_{e q} / R_{2}\right) f_{b}}}
\end{aligned}
$$

We put this in the more insightful form

$$
\begin{equation*}
A(j f)=\frac{A_{0}}{1+j f / f_{B}} \tag{7.25}
\end{equation*}
$$

image_name:(a)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: InN(z), N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vo, N2: InN(z)}
name: CFA, type: OpAmp, value: CFA, ports: {InP: Vi, InN: GND, OutP: Vo}
]
extrainfo:The circuit is a non-inverting current feedback amplifier (CFA) configuration. It shows the connection of a voltage source Vi, resistors R1 and R2, and an op-amp labeled CFA to create an amplifier circuit with gain.

image_name:(b)
description:The graph depicted is a Bode plot, specifically illustrating the magnitude response of a system. It shows the open-loop response $|z(jf)|$ in decibels (dec) on the vertical axis against frequency $f$ in decades (dec) on the horizontal axis.

Axes Labels and Units:
- **Vertical Axis**: $|z(jf)|$ (dec)
- **Horizontal Axis**: Frequency $f$ (dec)

Overall Behavior and Trends:
- The graph begins at a level corresponding to $R_{eq}$ at low frequencies.
- As the frequency increases, the magnitude response remains relatively flat until it reaches a corner frequency $f_b$.
- Beyond $f_b$, the response begins to decline at a rate of -1 dec/dec, indicating a first-order roll-off.
- The graph continues to decrease until it reaches a point labeled $f_B$, where the magnitude approaches the level of $R_2$.

Key Features and Technical Details:
- **Initial Level**: The response starts at $R_{eq}$, indicating the initial gain level of the system.
- **Corner Frequency ($f_b$)**: This is where the response starts to decline, marking the start of the bandwidth limitation.
- **Slope**: The slope of -1 dec/dec indicates a single-pole roll-off characteristic, typical for many amplifier responses.
- **Final Level**: The response levels off at $R_2$, indicating the closed-loop gain determined by the feedback network.

Annotations and Specific Data Points:
- The graph includes annotations marking the corner frequency $f_b$ and the bandwidth $f_B$.
- The slope is explicitly marked as -1 dec/dec, reinforcing the nature of the roll-off.

This Bode plot effectively visualizes the transition from open-loop to closed-loop behavior, highlighting the bandwidth and gain characteristics of the non-inverting current feedback amplifier configuration described in the context.

(b)

FIGURE 7.11 (a) Noninverting CFA configuration. (b) Visualizing the open-loop response $|z|$ and the closed-loop bandwidth $f_{B}$.
where

$$
\begin{equation*}
A_{0}=\left(1+\frac{R_{2}}{R_{1}}\right) \times \frac{1}{1+R_{2} / R_{e q}} \cong 1+\frac{R_{2}}{R_{1}} \tag{7.26}
\end{equation*}
$$

is the already familiar closed-loop dc gain, and

$$
\begin{equation*}
f_{B}=\left(1+\frac{R_{e q}}{R_{2}}\right) f_{b} \cong \frac{R_{e q}}{R_{2}} \times \frac{1}{2 \pi R_{e q} C_{e q}}=\frac{1}{2 \pi R_{2} C_{e q}} \tag{7.27}
\end{equation*}
$$

is the closed-loop bandwidth (both approximations exploit the fact that in a welldesigned circuit we have $R_{2} \ll R_{e q}$ ). Using simple geometry we visualize $f_{B}$ as the frequency at which $|z|$ drops to $R_{2}$, as illustrated in Fig. 7.11b. This frequency is established by the user via $R_{2}$ regardless of the closed-loop gain $A_{0}$, which is set separately via $R_{1}$. Consequently, CFA circuits are not subject to the gain-bandwidth tradeoff of their VFA counterparts. Along with the absence of slew-rate limiting, this is a fundamental advantage of CFAs compared to VFAs. (See also Problem 7.10 for higher-order effects.)

EXAMPLE 7.7 Suppose the CFA of Fig. 7.11 has $R_{e q}=750 \mathrm{k} \Omega$ and $C_{e q}=2.21 \mathrm{pF}$. If the data sheets recommend using $R_{2}=1.2 \mathrm{k} \Omega$, specify $R_{1}$ for a closed-loop dc gain of $10 \mathrm{~V} / \mathrm{V}$. What is the closed-loop bandwidth?

#### Solution

Imposing $1+1,200 / R_{1}=10$ gives $R_{1}=133.3 \Omega$. Moreover,

$$
f_{B} \cong \frac{1}{2 \pi R_{2} C_{e q}}=\frac{1}{2 \pi \times 1200 \times 2.21 \times 10^{-12}}=60 \mathrm{MHz}
$$

## 7.3 FEEDBACK TOPOLOGIES AND CLOSED-LOOP I/O RESISTANCES

The most basic parameters characterizing an amplifier are its unloaded gain, and its input and output resistances, also called the terminal resistances. These resistances come into play in actual application, when the amplifier is driven by a non-ideal input source and drives an output load. The input resistance forms a divider with the source's resistance, and the output resistance forms a divider with the load, thereby reducing the overall gain from source to load twice. This reduction is known as the loading effect. We will see next that besides stabilizing gain, negative feedback alters the terminal resistances in ways that tend to reduce the loading effect.

As mentioned, the input and output signals can be either currents or voltages, so we have four possible amplifier types: (a) the voltage amplifier, giving $v_{o}=A v_{i}$, $A$ in $\mathrm{V} / \mathrm{V} ;(b)$ the current amplifier, giving $i_{o}=A i_{i}, A$ in $\mathrm{A} / \mathrm{A} ;(c)$ the transresistance
amplifier, giving $v_{o}=A i_{i}, A$ in V/A; and (d) the transconductance amplifier, giving $i_{o}=A v_{i}, A$ in $\mathrm{A} / \mathrm{V}$. When negative feedback is applied around an amplifier, four different topologies arise. We wish to investigate how negative feedback affects gain as well as the terminal resistances of each configuration.

### The Series-Shunt Configuration

We start out by investigating the application of negative feedback around a voltage amplifier, the first of the aforementioned amplifier types. As shown in Fig. 7.12a, the amplifier's output port is modeled with a Thévenin equivalent consisting of the dependent source $a v_{\varepsilon}$ and the series output resistance $r_{o}$. The input port, assumed to play a purely passive role, is modeled with the input resistance $r_{i}$. The quantities $a$, $r_{i}$, and $r_{o}$ are referred to as open-loop parameters, and are thus denoted with lowercase letters. The role of the feedback network is to sense the output voltage $v_{o}$ and produce a scaled version of it, or $v_{f}=b v_{o}$, such that $-v_{f}$ is then summed to the input $v_{i}$ to generate the error signal $v_{\varepsilon}=v_{i}-v_{f}$ Note that the operation of voltage sensing at the output is performed in parallel, or shunt, just as in ordinary voltmeter measurements (in the lab we always measure voltage in parallel, never in series!). However, the operation of voltage summing at the input is performed in series, which is how we connect together different voltage sources when we want to add or subtract their voltages-never connect different voltage sources in parallel!

To be able to focus on the effect of negative feedback upon $a, r_{i}$, and $r_{o}$ alone, irrespective of the surrounding circuitry's details, we deliberately assume the absence of any loading from both ports of the amplifier (the presence of loading encountered in practical circuits will be taken up in the next section). Thus, to prevent loading at the amplifier's input port, assume the $v_{i}$ and $b v_{o}$ sources have zero series resistances so we can write $v_{\varepsilon}=v_{i}-v_{f}$ (had these resistances been different from zero, we would have had voltage division there). Likewise, to prevent loading at the amplifier's output port, assume this port is left open circuited, and the feedback-network's presents infinite resistance to said port so we can write $v_{o}=a v_{\varepsilon}$ (had this not been the case,
image_name:(a)
description:The circuit is a series-shunt voltage amplifier configuration. It includes a feedback network to stabilize the gain and improve linearity. The voltage sources vi and bvo have zero series resistances to prevent input loading. The output is open-circuited to avoid loading effects.

(a)
image_name:(a)
description:The circuit is a series-shunt voltage amplifier with a feedback network to stabilize gain and improve linearity. Voltage sources vi and AocVi have zero series resistances to prevent input loading. The output is open-circuited to avoid loading effects.

(b)

FIGURE 7.12 The series-shunt configuration or voltage amplifier: (a) error amplifier (top) and idealized feedback network (bottom); (b) equivalent circuit.
image_name:(a)
description:The circuit is a series-shunt voltage amplifier with a feedback network to stabilize gain and improve linearity. Voltage sources vi and AocVi have zero series resistances to prevent input loading. The output is open-circuited to avoid loading effects.
image_name:(b)
description:The circuit is a series-shunt voltage amplifier with a feedback network to stabilize gain and improve linearity. Voltage sources Vi and AocVi have zero series resistances to prevent input loading. The output is open-circuited to avoid loading effects.

FIGURE 7.13 (a) Test circuit to find the closed-loop parameters $A=v_{0} / v_{i}$ and $R_{i}$ for the series-shunt configuration. (b) Test circuit to find $R_{o}$.
we would have had voltage division at the output port as well). With reference to Fig. 7.13a, we have, by inspection, $v_{o}=a v_{\varepsilon}=a\left(v_{i}-v_{f}\right)=a\left(v_{i}-b v_{o}\right)$. Collecting yields the familiar result

$$
\begin{equation*}
A_{o c}=\frac{v_{o}}{v_{i}}=\frac{1}{b} \frac{1}{1+1 / L} \tag{7.28}
\end{equation*}
$$

where $L=a b$. As we know, negative feedback stabilizes gain by making $A_{o c} \rightarrow 1 / b$ in the limit $L \rightarrow \infty$.

To find the effect upon $r_{i}$, apply a test voltage $v_{i}$ as in Fig. 7.13a, find the ensuing current $i_{i}$, and obtain the closed-loop input resistance as the ratio $R_{i}=v_{i} / i_{i}$. Thus, Ohm's law gives $i_{i}=v_{\varepsilon} / r_{i}$. But Eq. (7.10) predicts $v_{\varepsilon}=v_{i} /(1+L)$, so

$$
\begin{equation*}
R_{i}=\frac{v_{i}}{i_{i}}=r_{i}(1+L) \tag{7.29}
\end{equation*}
$$

indicating that negative feedback takes the input resistance $r_{i}$, which in a welldesigned voltage amplifier is high to begin with, and multiplies it by $(1+L)$ to make it even higher. This is quite desirable in voltage-input amplifiers as it helps reduce input loading dramatically. Physically, we justify as follows. In the absence of any feedback we would have $v_{f}=0$, so the entire test voltage $v_{i}$ would appear across $r_{i}$ to give $i_{i}=v_{i} / r_{i}$.However, with feedback in place, the voltage across $r_{i}$ is reduced to $v_{\varepsilon}$, which is $(1+L)$ times as small as $v_{i}$, by Eq. (7.10). This lowers $i_{i}$ by a factor of $(1+L)$, effectively raising $r_{i}$ by $(1+L)$. In the ideal limit $L \rightarrow \infty$ we get $i_{i} \rightarrow 0$ and thus $R_{i} \rightarrow \infty$, indicating that the input port of an amplifier of the series-input type, with sufficient loop gain, tends to act as an open circuit.

Next, set $v_{i}=0$ and subject the output port to a test current $i_{o}$, as in Fig. 7.13b. Then, find the ensuing voltage $v_{o}$ and obtain the closed-loop output resistance as $R_{o}=v_{o} / i_{o}$. By KVL and Ohm's law,

$$
v_{o}=a v_{\varepsilon}+r_{o} i_{o}=a\left(-v_{f}\right)+r_{o} i_{o}=-a b v_{o}+r_{o} i_{o}
$$

Collecting and simplifying gives

$$
\begin{equation*}
R_{o}=\frac{v_{o}}{i_{o}}=\frac{r_{o}}{1+L} \tag{7.30}
\end{equation*}
$$

indicating that negative feedback takes the output resistance $r_{o}$, which in a welldesigned voltage amplifier is low to begin with, and divides it by $(1+L)$ to make it even lower. This is highly desirable in voltage-output amplifiers as it helps reduce output loading dramatically. Physically, we justify as follows. In the absence of feedback $(b=0)$ the circuit of Fig. $7.13 b$ would give $a v_{\varepsilon}=0$ and thus $v_{o}=r_{o} i_{o}$. However, with feedback in place, the amplifier, in its attempt to drive $v_{\varepsilon}$ close to zero, adjusts its dependent source so that $v_{o}\left(=v_{f} / b=-v_{\varepsilon} / b\right)$ becomes $(1+L)$ times as small, effectively lowering $r_{o}$ by $(1+L)$. In the ideal limit $L \rightarrow \infty$ we get $v_{o} \rightarrow 0$ and thus $R_{o} \rightarrow 0$, indicating that in the absence of any input signal, the output port of an amplifier of the output-shunt type, with sufficient loop gain, tends to act as a short circuit.

In light of the above results, it is apparent that the series-shunt configuration of Fig. 7.12 $a$ admits the voltage-amplifier equivalent of Fig. 7.12b, with the closed-loop parameters $A, R_{i}$, and $R_{o}$ as given in Eqs. (7.28) through (7.30). Note the use of upper-case letters to distinguish these parameters from their open-loop counterparts $a, r_{i v}$ and $r_{o}$.

An op amp with $a=10^{5} \mathrm{~V} / \mathrm{V}, r_{i}=1 \mathrm{M} \Omega$, and $r_{o}=100 \Omega$ is operated in the seriesshunt mode with $b=0.01 \mathrm{~V} / \mathrm{V}$. Estimate $A_{o c}, R_{i j}$, and $R_{o}$, and comment.

#### Solution

We have $L=10^{5} \times 0.01=10^{3}$. Thus, $A_{o c} \cong 100\left(1-1 / 10^{3}\right)=99.9 \mathrm{~V} / \mathrm{V}$, $R_{i}=10^{6}\left(1+10^{3}\right) \cong 10^{9} \Omega=1 \mathrm{G} \Omega$, and $R_{o}=100 /\left(1+10^{3}\right) \cong 0.1 \Omega$. Compared with the resistances surrounding an op amp, which are typically in the $\mathrm{k} \Omega$-range, $R_{i}$ effectively appears as an open circuit and $R_{o}$ as a short circuit.

### The Shunt-Series Configuration

We now turn our attention to the application of negative feedback around a current amplifier, the dual of the voltage amplifier. As shown in Fig. 7.14a, the amplifier's output port is modeled with a Norton equivalent consisting of the dependent source $a i_{\varepsilon}$ and the parallel output resistance $r_{o}$. The input port, assumed to play a purely passive role, is modeled with the input resistance $r_{i}$. The role of the feedback network is to sense the output current $i_{o}$ and produce a scaled version of it, or $i_{f}=b i_{o}$, such that $i_{f}$ is then summed to the input $i_{i}$ to generate the error signal $i_{\varepsilon}=i_{i}-i_{f}$ The operation of current sensing at the output port is performed in series, just as in laboratory current measurements, where we break the circuit to insert the ammeter in series (recall that currents are always measured in series, voltages always in parallel!). However, the operation of current summing at the input is performed in parallel, or shunt, as this is how we connect together different current sources when we want to add or subtract their currents-never connect different current sources in series!
image_name:(a)
description:
[
name: Ii, type: CurrentSource, value: Ii, ports: {Np: X1, Nn: X2}
name: ri, type: Resistor, value: ri, ports: {N1: X1, N2: X2}
name: aiε, type: VoltageControlledVoltageSource, ports: {Np: X3, Nn: X4}
name: ro, type: Resistor, value: ro, ports: {N1: X3, N2: X4}
name: biO, type: VoltageControlledCurrentSource, ports: {Np: X1, Nn: X2}
]
extrainfo:The circuit represents a shunt-series configuration or current amplifier with an error amplifier and idealized feedback network. The current sources are connected in parallel for current summing, while the current sensing is performed in series at the output.

image_name:(b) Equivalent circuit
description:
[
name: i_i, type: CurrentSource, value: i_i, ports: {Np: X1, Nn: X2}
name: R_i, type: Resistor, value: R_i, ports: {N1: X2, N2: X1}
name: A_sci_i, type: CurrentControlledCurrentSource, value: A_sci_i, ports: {Np: X3, Nn: X2}
name: R_o, type: Resistor, value: R_o, ports: {N1: X3, N2: X4}
name: i_o, type: CurrentSource, value: i_o, ports: {Np: X4, Nn: X3}
]
extrainfo:The circuit diagram represents a shunt-series configuration or current amplifier. It includes an error amplifier and an idealized feedback network. The current summing at the input is performed in parallel, whereas the current sensing at the output is in series. The feedback is negative, affecting the open-loop parameters a, ri, and ro.

(b)

FIGURE 7.14 The shunt-series configuration or current amplifier: (a) error amplifier (top) and idealized feedback network (bottom). (b) Equivalent circuit.

To be able to focus on the effect of negative feedback upon the open-loop parameters $a, r_{i}$, and $r_{o}$ alone, irrespective of the surrounding circuitry's details, we again deliberately assume the absence of any loading from both ports of the amplifier (the presence of loading encountered in practical circuits will be taken up in the next section). Thus, to prevent loading at the amplifier's input port, assume the $i_{i}$ and $b i_{o}$ sources have infinite parallel resistance so we can write $i_{\varepsilon}=i_{i}-i_{f}$ (had these sources had non-infinite resistances, we would have had current division at the input port). Likewise, to prevent loading at the amplifier's output port, assume this port is short circuited, and the feedback-network's presents zero resistance to said port so we can simply write $i_{o}=a i_{\varepsilon}$ (had this not been the case, we would have had current division at the amplifier's output port as well). With reference to Fig. 7.14a, we have, by inspection, $i_{o}=a i_{\varepsilon}=a\left(i_{i}-i_{f}\right)=a\left(i_{i}-b i_{o}\right)$. Collecting yields the familiar result

$$
\begin{equation*}
A_{s c}=\frac{i_{o}}{i_{i}}=\frac{1}{b} \frac{1}{1+1 / L} \tag{7.31}
\end{equation*}
$$

where $L=a b$. As we know, negative feedback stabilizes gain by making $A_{s c} \rightarrow 1 / b$ in the limit $L \rightarrow \infty$.

To find the effect upon $r_{i}$, apply a test current $i_{i}$ as in Fig. 7.15a, find the ensuing voltage $v_{i}$, and obtain the closed-loop input resistance as $R_{i}=v_{i} / i_{i}$. Thus, Ohm's law gives $v_{i}=r_{i} i_{\varepsilon}$. But Eq. (7.10) predicts $i_{\varepsilon}=i_{i} /(1+L)$, so

$$
\begin{equation*}
R_{i}=\frac{v_{i}}{i_{i}}=\frac{r_{i}}{1+L} \tag{7.32}
\end{equation*}
$$

indicating that negative feedback takes the input resistance $r_{i}$, which in a welldesigned current amplifier is usually low to begin with, and divides it by $(1+L)$ to make it even lower. This is highly desirable in current-input amplifiers, as it helps reduce input loading dramatically. Physically, we justify as follows. In the absence of any feedback, the entire test current $i_{i}$ would flow through $r_{i}$, giving $v_{i}=r_{i} i_{i}$. However, with feedback in place, the current through $r_{i}$ reduces to the error current
image_name:(a)
description:The circuit is a shunt-series feedback configuration designed to find closed-loop parameters such as A = vo/vi and Ri. It includes a current amplifier with feedback elements to adjust the input and output characteristics.
image_name:(b)
description:The circuit diagram (b) is used to find the output resistance R0 of a shunt-series feedback amplifier. It contains a voltage-controlled current source (aiε) and a current-controlled current source (biο) which are part of the feedback network. The test current i0 is applied at the output to determine R0.

FIGURE 7.15 (a) Test circuit to find the closed-loop parameters $A=v_{o} / v_{i}$ and $R_{i}$ for the shunt-series configuration. (b) Test circuit to find $R_{0}$.
$i_{\varepsilon}$, which is $(1+L)$ times as small as $i_{i}$, by Eq. (7.10). This reduces $v_{i}$ by a factor of $(1+L)$, effectively dividing $r_{i}$ by $(1+L)$. In the ideal limit $L \rightarrow \infty$ we get $v_{i} \rightarrow 0$ and $R_{i} \rightarrow 0$, indicating that the input port of an amplifier of the input-shunt type, with sufficient loop gain, tends to act as a short circuit.

Next, set $i_{i}=0$ and subject the output port to a test voltage $v_{o}$ as shown in Fig. 7.15b. Then, find the ensuing current $i_{o}$ and obtain the closed-loop output resistance as $R_{o}=v_{o} / i_{o}$. By KCL and Ohm's law,

$$
i_{o}=a i_{\varepsilon}+v_{o} / r_{o}=a\left(-i_{f}\right)+v_{o} / r_{o}=-a b i_{o}+v_{o} / r_{o}
$$

Collecting and simplifying gives

$$
\begin{equation*}
R_{o}=\frac{v_{o}}{i_{o}}=r_{o}(1+L) \tag{7.33}
\end{equation*}
$$

indicating that negative feedback takes the output resistance $r_{o}$, which in a welldesigned current amplifier is usually high to begin with, and multiplies it by $(1+L)$ to make it even higher. This is quite desirable in current-output amplifiers as it helps reduce output loading dramatically. Physically, we justify as follows. In the absence of any feedback we would have $i_{o}=v_{o} / r_{o}$. However, with feedback in place, the amplifier, in its attempt to drive $i_{\varepsilon}$ close to zero, adjusts its dependent source so that $i_{o}\left(=i_{f} / b=-i_{\varepsilon} / b\right)$ becomes $(1+L)$ times as small, effectively raising $r_{o}$ by $(1+L)$. In the ideal limit $L \rightarrow \infty$ we get $i_{o} \rightarrow 0$ and thus $R_{o} \rightarrow \infty$, indicating that in the absence of any input, the output port of an amplifier of the output-series type, with sufficient loop gain, tends to act as an open circuit.

In light of the above results, it is apparent that the shunt-series configuration of Fig. 7.14 $a$ admits the current-amplifier equivalent of Fig. 7.14b, with the closed-loop parameters $A_{s c}, R_{i}$, and $R_{o}$ as given in Eqs. (7.31) through (7.33). Note that what is good for a current amplifier ( $R_{i} \rightarrow 0$ and $R_{o} \rightarrow \infty$ ) is just the opposite of what is good for a voltage amplifier ( $R_{i} \rightarrow \infty$ and $R_{o} \rightarrow 0$ ). This is yet another manifestation of the duality principle.
image_name:(a)
description:
[
name: ri, type: Resistor, value: ri, ports: {N1: X1, N2: X2}
name: ro, type: Resistor, value: ro, ports: {N1: X4, N2: X3}
name: ii, type: CurrentSource, ports: {Np: X1, Nn: X2}
name: aie, type: VoltageControlledVoltageSource, value: aie, ports: {Np: X3, Nn: X4}
name: bio, type: VoltageControlledCurrentSource, value: bio, ports: {Np: X1, Nn: X2}
]
extrainfo:The circuit diagram (a) represents a shunt-shunt configuration or transresistance amplifier with negative feedback. It includes a current source at the input and a voltage output. The feedback network is designed to convert the output voltage back into a current for feedback.
image_name:(b)
description:
[
name: Ri, type: Resistor, value: Ri, ports: {N1: X1, N2: X2}
name: Aocii, type: VoltageControlledVoltageSource, ports: {Np: X5, Nn: X3}
name: Ro, type: Resistor, value: Ro, ports: {N1: X4, N2: X5}
name: ii, type: CurrentSource, ports: {Np: X1, Nn: X2}
]
extrainfo:The circuit in Figure 7.16(b) is a simplified equivalent circuit of a transresistance amplifier with feedback. The input is a current source ii connected between nodes X1 and X2, and the output is a voltage across nodes X4 and X3. The transresistance amplifier is represented by a voltage-controlled voltage source Aocii with a series resistance Ro.

FIGURE 7.16 The shunt-shunt configuration or transresistance amplifier: (a) error amplifier (top) and idealized feedback network (bottom). (b) Equivalent circuit.

### The Shunt-Shunt Configuration

Figure $7.16 a$ shows the application of negative feedback around a transresistance amplifier. The input signal is a current, so input current summing is done in shunt fashion, as in the case of the current amplifier of Fig. 7.14a. On the other hand, the output signal is a voltage, so the amplifier's output port is modeled with the Thévenin source $a i_{\varepsilon}$, and output voltage sensing is done in shunt fashion, as in the case of the voltage amplifier of Fig. 7.12a. The transresistance amplifier is thus of the shunt-shunt type.

To find the closed-loop gain $A_{o c}$ we write $v_{o}=a i_{\varepsilon}=a\left(i_{i}-i_{f}\right)=a\left(i_{i}-b v_{o}\right)$. Collecting yields the familiar result

$$
\begin{equation*}
A_{o c}=\frac{v_{o}}{i_{i}}=\frac{1}{b} \frac{1}{1+1 / L} \tag{7.34}
\end{equation*}
$$

where $L=a b$. To find the closed-loop resistances $R_{i}$ and $R_{o}$, we use the test-signal techniques already utilized above. Actually, since the input port is similar to that of the shunt-series configuration, and the output port is similar to that of the series-shunt configuration, we recycle the results developed in connection with Figs. 7.15a and 7.13b, and write

$$
\begin{equation*}
R_{i}=\frac{r_{i}}{1+L} \quad R_{o}=\frac{r_{o}}{1+L} \tag{7.35}
\end{equation*}
$$

In the limit $L \rightarrow \infty$ the shunt-shunt configuration gives $A_{o c} \rightarrow 1 / b, R_{i} \rightarrow 0$, and $R_{o} \rightarrow 0$.

### The Series-Series Configuration

Figure $7.17 a$ shows the application of negative feedback around a transconductance amplifier. The input signal is a voltage, so input voltage summing is done in series fashion, as in the case of the voltage amplifier of Fig. 7.12a. Conversely, the output signal is a current, so the amplifier's output port is modeled with the Norton source
image_name:(a)
description:
[
name: Vi, type: VoltageSource, ports: {Np: X2, Nn: X1}
name: ri, type: Resistor, value: ri, ports: {N1: X2, N2: X3}
name: avε, type: VoltageControlledVoltageSource, ports: {Np: X5, Nn: X4}
name: ro, type: Resistor, value: ro, ports: {N1: X5, N2: X4}
name: bio, type: VoltageControlledCurrentSource, ports: {Np: X3, Nn: X1}
]
extrainfo:The circuit is a series-series configuration transconductance amplifier with negative feedback. The input is a voltage (Vi) and the output is a current (io). The feedback network consists of a voltage-controlled current source and resistors.
image_name:(b)
description:
[
'name': 'Vi', 'type': 'VoltageSource', 'ports': {'Np': 'X2', 'Nn': 'X1'
'name': 'Ri', 'type': 'Resistor', 'value': 'Ri', 'ports': {'N1': 'X2', 'N2': 'X1'
'name': 'A_scVi', 'type': 'VoltageControlledVoltageSource', 'ports': {'Np': 'X3', 'Nn': 'X4'
'name': 'Ro', 'type': 'Resistor', 'value': 'Ro', 'ports': {'N1': 'X4', 'N2': 'X3'
]
extrainfo:The circuit represents a series-series configuration of a transconductance amplifier with feedback. The input voltage is applied across nodes X1 and X2, and the output current is sensed across Ro.

FIGURE 7.17 The series-series configuration or transconductance amplifier: (a) error amplifier (top) and idealized feedback network (bottom). (b) Equivalent circuit.
$a v_{\varepsilon}$, and output current sensing is done in series fashion, as in the case of the current amplifier of Fig. 7.14a. The transconductance amplifier is thus of the series-series type, the dual type of the shunt-shunt amplifier.

To find the closed-loop parameters we proceed in the usual fashion, obtaining

$$
\begin{gather*}
A_{s c}=\frac{i_{o}}{v_{i}}=\frac{1}{b} \frac{1}{1+1 / L}  \tag{7.36}\\
R_{i}=r_{i}(1+L) \quad R_{o}=r_{o}(1+L)
\end{gather*}
$$

where $L=a b$. In the limit $L \rightarrow \infty$, the series-series configuration gives $A_{s c} \rightarrow 1 / b$, $R_{i} \rightarrow \infty$, and $R_{o} \rightarrow \infty$.

### Summary

In light of the above results, we can state that the closed-loop gain $A$ of each of the four negative-feedback configurations can be expressed in the form

$$
\begin{equation*}
A=A_{\text {ideal }} \frac{1}{1+1 / L} \tag{7.38}
\end{equation*}
$$

where $A_{\text {ideal }}=1 / b$ is the closed-loop gain in the limit $L \rightarrow \infty, L=a b$ is the loop gain, $a$ is the open-loop gain, and $b$ is the feedback factor. Moreover, the closed-loop terminal resistances $R_{i / o}$ can be expressed in terms of the open-loop resistances $r_{i / o}$ as

$$
\begin{equation*}
R_{i / o}=r_{i / o}(1+L)^{ \pm 1} \tag{7.39}
\end{equation*}
$$

with +1 for the series cases, and -1 for shunt cases. Table 7.1 summarizes the four negative-feedback topologies, along with the terminal resistances in the idealized limit $L \rightarrow \infty$.

TABLE 7.1 The four feedback topologies, and their idealized closed-loop terminal resistances.

| $\boldsymbol{s}_{\boldsymbol{i}}$ | $\boldsymbol{s}_{\boldsymbol{o}}$ | Name | $\boldsymbol{a}$ | $\boldsymbol{b}$ | Topology | $\boldsymbol{R}_{\boldsymbol{i} \text { (ideal) }}$ | $\boldsymbol{R}_{\boldsymbol{o} \text { (ideal) }}$ |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| $v_{i}$ | $v_{o}$ | Voltage amp | V/V | V/V | Series-shunt | $\infty$ | 0 |
| $i_{i}$ | $i_{o}$ | Current amp | A/A | A/A | Shunt-series | 0 | $\infty$ |
| $i_{i}$ | $v_{o}$ | Transresistance amp | V/A | A/V | Shunt-shunt | 0 | 0 |
| $v_{i}$ | $i_{o}$ | Transconductance amp | A/V | V/A | Series-series | $\infty$ | $\infty$ |

### The Four Feedback Configurations Using Op Amps

Sometimes the operations of input summing and output sensing are not that obvious. So, to develop a quick feel, let us examine actual circuit examples using the op amp, the most popular building block designed for negative-feedback operation. Even though the op amp is, strictly speaking, a voltage-type amplifier (to stress this, we use the symbol $a_{v}$ to denote its voltage gain), it can be used in any of the four feedback topologies discussed above, giving further credence to the designation operational.

- Series-Shunt Configuration (Fig. 7.18a): we have already examined this configuration in connec-tion with Fig. 7.2. With sufficiently high loop gain, as is generally the case with op amp circuits, the input error voltage $v_{\varepsilon}$ will be
image_name:Series-Shunt Configuration (Fig. 7.18a)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: vf, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: vo, N2: vf}
name: av, type: OpAmp, value: av, ports: {InP: Vi, InN: vf, OutP: vo, OutN: GND}
name: LD, type: Other, ports: {N1: vo, N2: GND}
]
extrainfo:The circuit is a series-shunt feedback amplifier configuration. The input voltage source Vi provides the input signal. The operational amplifier with voltage gain av amplifies the input signal. The feedback network consists of resistors R1 and R2, which determine the feedback factor b.

(a) Series-shunt: $b=\frac{v_{f}}{v_{o}}=\frac{R_{1}}{R_{1}+R_{2}}$
image_name:FIGURE 7.18
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: av, type: OpAmp, value: av, ports: {InP: Vi, InN: vf, OutP: vo, OutN: GND}
name: LD, type: Diode, ports: {Na: vo, Nc: vf}
name: R, type: Resistor, value: R, ports: {N1: vf, N2: GND}
]
extrainfo:The circuit is a series-shunt feedback amplifier configuration. The input voltage source Vi provides the input signal. The operational amplifier with voltage gain av amplifies the input signal. The feedback network consists of resistors R1 and R2, which determine the feedback factor b. For series-shunt configuration, the feedback factor b is given by b = R1 / (R1 + R2).

(c) Series-series: $b=\frac{v_{f}}{i_{o}}=R$
image_name:Series-shunt feedback amplifier configuration
description:
[
name: i_i, type: CurrentSource, value: i_i, ports: {Np: GND, Nn: vf}
name: R, type: Resistor, value: R, ports: {N1: vf, N2: vo}
name: a_v, type: OpAmp, value: a_v, ports: {InP: GND, InN: vf, OutP: vo}
name: LD, type: Diode, ports: {Na: vo, Nc: GND}
]
extrainfo:The circuit is a series-shunt feedback amplifier configuration with a current source input. The feedback is provided through resistor R, and the output is connected to a diode LD. The feedback factor b is given by b = R1 / (R1 + R2) for the series-shunt configuration.

(b) Shunt-shunt: $b=\frac{i_{f}}{v_{o}}=-\frac{1}{R}$
image_name:Figure 7.18
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: X2, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: vf, N2: X2}
name: LD, type: Diode, ports: {Na: Out, Nc: X2}
name: av, type: OpAmp, value: av, ports: {InP: vf, InN: GND, OutP: Out}
name: ii, type: CurrentSource, value: ii, ports: {Np: vf, Nn: GND}
]
extrainfo:The circuit is a series-shunt feedback amplifier configuration with a current source input. The feedback is provided through resistor R2, and the output is connected to a diode LD. The feedback factor b is given by b = R1 / (R1 + R2) for the series-shunt configuration.

(d) Shunt-series: $b=\frac{i_{f}}{i_{o}}=-\frac{R_{1}}{R_{1}+R_{2}}$

FIGURE 7.18 Illustrating the four basic negative-feedback topologies using op amps.
vanishingly small, indicating a vanishingly small current through the op amp's internal resistance $r_{i}$. Consequently, for all practical purposes the op amp's input port appears as an open circuit to the feedback network. This allows us to apply the voltage divider rule and write

$$
\begin{equation*}
b=\frac{v_{f}}{v_{i}}=\frac{R_{1}}{R_{1}+R_{2}}=\frac{1}{1+R_{2} / R_{1}} \tag{7.40}
\end{equation*}
$$

In the ideal op-amp limit $a_{v} \rightarrow \infty$ this circuit gives $A_{o c}=v_{o} / v_{i} \rightarrow 1 / b=1+R_{2} / R_{1}$, $R_{i} \rightarrow \infty$, and $R_{o} \rightarrow 0$.

- Shunt-Shunt Configuration (Fig. 7.18b): the student will recall from basic op amp theory that in the ideal limit $a_{v} \rightarrow \infty$ the inverting-input node, also called a current-summing junction, acts as a virtual ground. The natural input signal is in this case a current, so the error signal is $i_{\varepsilon}=i_{i}-i_{\rho}$, as shown. Moreover, with the inverting-input node at 0 V , we have, by Ohm's law, $i_{f}=\left(0-v_{o}\right) / R$, so

$$
\begin{equation*}
b=\frac{i_{f}}{v_{o}}=-\frac{1}{R} \tag{7.41}
\end{equation*}
$$

In the ideal op-amp limit $a_{v} \rightarrow \infty$, this circuit gives $A_{o c}=v_{o} / i_{i} \rightarrow 1 / b=-R$. Moreover, the resistance seen by the input source is $R_{i} \rightarrow 0$, and that seen by the output load is $R_{o} \rightarrow 0$.

The shunt-shunt configuration forms the basis of the popular inverting voltage amplifier of Fig. 7.19a. Even though this is a voltage-in, voltage-out amplifier, from a feedback viewpoint it is a shunt-shunt configuration. This becomes more apparent if we perform a source transformation to convert from the voltage $v_{i}$ to the current $i_{i}=v_{i} / R_{1}$. Then, the closed-loop voltage gain is

$$
\begin{equation*}
A_{v}=\frac{v_{o}}{v_{i}}=\frac{v_{o}}{i_{i}} \times \frac{i_{i}}{v_{i}}=\left(-R_{2}\right) \times \frac{1}{R_{1}}=-\frac{R_{2}}{R_{1}} \tag{7.42}
\end{equation*}
$$

- Series-Series Configuration (Fig. 7.18c): the natural signals for this circuit are a voltage at the input and a current at the output. The task of the feedback network is to sense the output current $i_{o}$ in series, and convert it to the feedback voltage $v_{f}$ to be summed to the input $v_{i}$ in series. Amazingly, both operations are performed by means of a single resistance, $R$. As discussed earlier, the op amp's input port appears for all practical purposes as an open circuit to the feedback network. We can thus use Ohm's law and write $v_{f}=R i_{o}$, so

$$
\begin{equation*}
b=\frac{v_{f}}{i_{o}}=R \tag{7.43}
\end{equation*}
$$

image_name:FIGURE 7.19(a)
description:
[
name: vi, type: VoltageSource, value: vi, ports: {Np: Vi, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vi, N2: InN(av)}
name: R2, type: Resistor, value: R2, ports: {N1: InN(av), N2: vo}
name: av, type: OpAmp, value: av, ports: {InP: GND, InN: InN(av), Out: vo}
]
extrainfo:The circuit is an inverting voltage amplifier configured as a shunt-shunt amplifier. The feedback network senses the output current and converts it to a feedback voltage using a single resistor R.

FIGURE 7.19 The popular inverting voltage amplifier is actually a shunt-shunt amplifier, as demonstrated by the source transformation.

In the ideal op-amp limit $a_{v} \rightarrow \infty$, this circuit gives $A_{s c}=i_{o} / v_{i} \rightarrow 1 / b=1 / R$. Moreover, the resistance seen by the input source is $R_{i} \rightarrow \infty$, and that seen by the output load is $R_{o} \rightarrow \infty$.

- Shunt-Series Configuration (Fig. 7.18d): the natural signals for this circuit are a current at the input and a current at the output. Given that the inverting-input node is at 0 V , we can apply the current-divider rule and write

$$
-i_{f}=\frac{R_{1}}{R_{1}+R_{2}} i_{o}
$$

so

$$
\begin{equation*}
b=\frac{i_{f}}{i_{o}}=\frac{-R_{1}}{R_{1}+R_{2}}=\frac{-1}{1+R_{2} / R_{1}} \tag{7.44}
\end{equation*}
$$

In the ideal op-amp limit $a_{v} \rightarrow \infty$, this circuit gives $A_{s c}=i_{o} / i_{i} \rightarrow-\left(1+R_{2} / R_{1}\right)$. Moreover, the resistance seen by the input source is $R_{i} \rightarrow 0$, and that seen by the output load is $R_{o} \rightarrow \infty$.

## 7.4 PRACTICAL CONFIGURATIONS AND THE EFFECT OF LOADING

The feedback networks of Section 7.3 were deliberately assumed idealized so we could focus on the effects of negative feedback upon the amplifier's parameters $a$, $r_{i}$, and $r_{o}$ alone. In a practical circuit the feedback network introduces loading both at the amplifier's input and output. Moreover, the amplifier and the feedback network are sometimes interwoven with each other, making the separation between the two not always obvious. A negative-feedback circuit can always be analyzed in its entirety via standard techniques such as nodal or loop analysis. However, as circuit complexity increases, this approach soon becomes prohibitive.

Mercifully, suitable approximations can be made that allow us to separate the circuit into a basic amplifier incorporating the effects of loading, and a distinct feedback network. With this separation in hand, we can then apply Eqs. (7.38) and (7.39) to find the closed-loop parameters $A, R_{i}$, and $R_{o}$. These approximations exploit a priori the fact that with a sufficiently high loop gain $T$, a terminal resistance $R_{i / o}$ satisfies

$$
\begin{array}{ll}
\lim _{L \rightarrow \infty} R_{i / o}=\infty & \text { for the series case } \\
\lim _{L \rightarrow \infty} R_{i / o}=0 & \text { for the shunt case } \tag{7.45b}
\end{array}
$$

In words, the feedback network sees in effect an open circuit (OC) when looking into an amplifier's port where summing or sensing is done in series, and a short circuit (SC) when summing or sensing is done in shunt. These claims, and their usefulness, will become clearer as we proceed.

### Series-Shunt Circuits

In Fig. $7.18 a$ we have investigated the non-inverting op amp configuration as a classic example of a series-shunt circuit. We now re-examine it with an eye on the interaction between the error amplifier's internal resistances $r_{i}$ and $r_{o}$ and the external resistances $R_{1}$ and $R_{2}$ making up the feedback network. This interaction results in loading both at the amplifier's input and output. To be able to focus on loading by the feedback network alone, we continue to assume a driving source $v_{i}$ with zero series resistance, and an unloaded (open-circuited) output port, as shown in Fig. 7.20.
image_name:FIGURE 7.20
description:
[
name: Vi, type: VoltageSource, ports: {Np: Vi, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: vf, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: vf, N2: vo}
name: OpAmp, type: OpAmp, ports: {InP: Vi, InN: vf, OutP: vo}
]
extrainfo:The circuit is a non-inverting op-amp configuration with internal resistances ri and ro explicitly shown. It includes a feedback network formed by resistors R1 and R2. The input voltage source is Vi and there is an additional loading resistor Ro at the output.

FIGURE 7.20 The non-inverting op amp with its internal resistances $r_{i}$ and $r_{o}$ explicitly shown.

To investigate loading at the input port, note that the external resistance seen by this port would appear to be $R_{1} / /\left(R_{2}+r_{o}\right)$. But we know a priori that in feedback operation the system will present a very low resistance $\left(R_{o} \rightarrow 0\right)$ at the output node due to shunt-type sensing there. This swamps out the effect of $r_{o}$, causing the external resistance seen by the amplifier's input port to be in effect $R_{1} / / R_{2}$. This is depicted in the amplifier's equivalent of Fig. 7.21a, where $R_{2}$ is shown short-circuited (SC) to ground.

To investigate loading at the output port, note that the external resistance seen by this port would appear to be $R_{2}+\left(R_{1} / / r_{i}\right)$. But we know a priori that in feedback
image_name:(a)
description:
[
name: v_e, type: VoltageSource, value: v_e, ports: {Np: v_e, Nn: GND}
name: ri, type: Resistor, value: ri, ports: {N1: v_e, N2: GND}
name: OpAmp, type: OpAmp, ports: {InP: v_e, InN: v_f, OutP: v_o, OutN: GND}
name: a_vv_d, type: VoltageControlledVoltageSource, value: a_vv_d, ports: {Np: v_o, Nn: GND}
name: ro, type: Resistor, value: ro, ports: {N1: v_o, N2: v_1}
name: R1, type: Resistor, value: R1, ports: {N1: v_f, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: v_o, N2: OC}
name: r_o, type: Resistor, value: r_o, ports: {N1: v_1, N2: GND}
]
extrainfo:The circuit in diagram (a) represents an error amplifier configuration with a feedback network composed of resistors R1 and R2. The op-amp is configured with a voltage-controlled voltage source a_vv_d. The output of the op-amp is connected to the load through resistors ro and r_oa. The input voltage is applied at v_e, and the feedback voltage is taken from v_f. The circuit aims to minimize error voltage v_d by adjusting v_o.
image_name:(b)
description:
[
name: R1, type: Resistor, ports: {N1: vf, N2: OC}
name: R2, type: Resistor, ports: {N1: vf, N2: vo}
name: vo, type: VoltageSource, ports: {Np: vo, Nn: GND}
]
extrainfo:The circuit diagram (b) represents a feedback network with resistors R1 and R2. The node 'vf' serves as the feedback voltage node, while 'vo' is the output voltage node. The 'OC' node is open-circuited, and 'SC' indicates a short circuit to ground for the voltage source.

FIGURE 7.21 Decomposing the circuit of Fig. 7.20 into (a) the error amplifier and (b) the feedback network.
operation the system will present a very high resistance $\left(R_{i} \rightarrow \infty\right)$ at the input node due to series-type summing there. This stems from the fact that $v_{\varepsilon} \rightarrow 0$, making the current through $r_{i}$ truly negligible and thus swamping out the effect of $r_{i}$. For practical purposes, the amplifier's input port appears as an open circuit to the feedback network. This too is depicted in Fig. 7.21a, where the node common to $R_{1}$ and $R_{2}$ is shown as open-circuited (OC), indicating that the external resistance seen by the amplifier's output port is in effect $R_{2}+R_{1}$.

With the feedback path interrupted both at the output (via short circuiting) and at the input (via open circuiting), the circuit of Fig. $7.21 a$ represents the error amplifier in open-loop operation, but with loading by the external feedback network specifically taken into account at both ports. Next, we wish to find its openloop parameters, now denoted as $a\left(=v_{o} / v_{\varepsilon}\right), r_{i a}$ and $r_{o a}$. By the voltage divider rule we have

$$
v_{o}=\frac{R_{1}+R_{2}}{r_{o}+R_{1}+R_{2}} a_{v} v_{d}=\frac{R_{1}+R_{2}}{r_{o}+R_{1}+R_{2}} a_{v} \frac{r_{i}}{r_{i}+\left(R_{1} / / R_{2}\right)} v_{\varepsilon}
$$

so that

$$
\begin{equation*}
a=\frac{v_{o}}{v_{\varepsilon}}=\frac{r_{i}}{r_{i}+\left(R_{1} / / R_{2}\right)} a_{v} \frac{R_{1}+R_{2}}{r_{o}+R_{1}+R_{2}} \tag{7.46}
\end{equation*}
$$

Note that $a<a_{v}$ because of input and output loading. We also have, by inspection

$$
\begin{equation*}
r_{i a}=r_{i}+\left(R_{1} / / R_{2}\right) \quad r_{o a}=r_{o} / /\left(R_{2}+R_{1}\right) \tag{7.47}
\end{equation*}
$$

Next, we seek a representation for the feedback network that is separate from the basic amplifier. Referring back to Fig. 7.20 we observe that at the sensing side this network is driven by a voltage source $v_{o}$ expected to exhibit extremely low series resistance $R_{o}$, and that at the summing side it drives the amplifier's input port which, for practical purposes, appears as an open circuit (OC). The circuit for the calculation of $b$ is thus as in Fig. 7.21b, from which we readily find

$$
\begin{equation*}
b=\frac{v_{f}}{v_{o}}=\frac{R_{1}}{R_{1}+R_{2}}=\frac{1}{1+R_{2} / R_{1}} \tag{7.48}
\end{equation*}
$$

Finally, we apply Eq. (7.28) to find the unloaded gain $A_{o c}$, and Eqs. (7.29) and (7.30), but with $r_{i}$ and $r_{o}$ replaced by $r_{i a}$ and $r_{o a}$, to find the closed-loop terminal resistances $R_{i}$, and $R_{o}$. Once these three parameters are known, we can use them in the general case in which the feedback amplifier is driven by a signal source $v_{s i g}$ with nonzero series resistance $R_{s i g}$, and drives a noninfinite output load $R_{L}$. With reference to the circuit model of Fig. 7.22, the source-to-load gain $v_{o} / v_{\text {sig }}$, also called the loaded gain, is readily found as

$$
\begin{equation*}
\frac{v_{o}}{v_{s i g}}=\frac{R_{i}}{R_{s i g}+R_{i}} A_{o c} \frac{R_{L}}{R_{o}+R_{L}} \tag{7.49}
\end{equation*}
$$

image_name:FIGURE 7.22
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: Vi}
name: Ri, type: Resistor, value: Ri, ports: {N1: Vi, N2: GND}
name: AocVi, type: VoltageControlledVoltageSource, value: AocVi, ports: {Np: AocVi, Nn: GND}
name: Ro, type: Resistor, value: Ro, ports: {N1: AocVi, N2: Vo}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a closed-loop voltage amplifier model driven by a source Vsig and driving an external load RL. It includes a voltage-controlled voltage source AocVi representing the amplifier with input resistance Ri and output resistance Ro.

FIGURE 7.22 Modeling a closed-loop voltage amplifier driven by a source $v_{s i g}$ and driving an external load $R_{L}$.
(a) In the circuit of Fig. 7.20 let the op amp be a mediocre type with $a_{v}=$

#### EXAMPLE 7.9

$1000 \mathrm{~V} / \mathrm{V}, r_{i}=10 \mathrm{k} \Omega$, and $r_{o}=1.0 \mathrm{k} \Omega$. If $R_{1}=1.0 \mathrm{k} \Omega$ and $R_{2}=9.0 \mathrm{k} \Omega$, find $R_{i}, R_{o}$, and the unloaded gain $A_{o c}$.
(b) Find the source-to-load gain $A=v_{o} / v_{\text {sig }}$ if the feedback amplifier is driven by a signal source $v_{s i g}$ having a series resistance $R_{s i g}=20 \mathrm{k} \Omega$, and drives a load $R_{L}=2.0 \mathrm{k} \Omega$.

#### Solution

(a) Using Eqs. (7.46) through (7.48) we have

$$
\begin{aligned}
a & =\frac{10}{10+(1.0 / / 9.0)} 1000 \frac{1.0+9.0}{1.0+1.0+9.0}=0.917 \times 1000 \times 0.909 \\
& =833.3 \mathrm{~V} / \mathrm{V}(<1000 \mathrm{~V} / \mathrm{V}) \\
r_{i a} & =10+(1.0 / / 9.0)=10.9 \mathrm{k} \Omega \quad r_{o a}=1.0 / /(9.0+1.0)=0.909 \mathrm{k} \Omega \\
b & =\frac{1.0}{1.0+9.0}=\frac{1}{10} \mathrm{~V} / \mathrm{V}
\end{aligned}
$$

Thus, $L=a b=833.3 / 10=83.33$, so

$$
\begin{aligned}
& A_{o c}=\frac{10}{1+1 / 83.33}=9.881 \mathrm{~V} / \mathrm{V} \\
& R_{i}=10.9(1+83.33) \cong 920 \mathrm{k} \Omega \\
& R_{o}=\frac{909}{1+83.33} \cong 10.8 \Omega
\end{aligned}
$$

(b) By Eq. (7.49), the source-to-load gain is

$$
\begin{aligned}
\frac{v_{o}}{v_{s i g}} & =\frac{920}{20+920} 9.88 \frac{2000}{10.8+2000}=0.979 \times 9.881 \times 0.995 \\
& =9.618 \mathrm{~V} / \mathrm{V}\left(<A_{o c}\right)
\end{aligned}
$$

The line of reasoning developed for the above example can be generalized to the following Series-Shunt Procedure:

- To calculate loading at the input of the basic amplifier, short-circuit (SC) the sensing-side port of the feedback network.
- To calculate loading at the output of the basic amplifier, open-circuit (OC) the summing-side port of the feedback network.
- To find $b$, apply a voltage $v_{o}$ to the sensing-side port of the feedback network, find the open-circuit (OC) voltage $v_{f}$ at the summing-side port of the feedback network, and let $b=v_{f} / v_{o}$.
We shall illustrate the procedure with additional examples.
image_name:Figure 7.23 Series-shunt feedback triple
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: Q1, type: NPN, ports: {C: V2, B: vi, E: vf}
name: Q2, type: NPN, ports: {C: V3, B: V2, E: GND}
name: Q3, type: NPN, ports: {C: GND, B: V3, E: vo}
name: R1, type: Resistor, value: R1, ports: {N1: vf, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: vf, N2: Vo}
name: R3, type: Resistor, value: R3, ports: {N1: Vo, N2: GND}
name: R4, type: Resistor, value: R4, ports: {N1: V2, N2: GND}
name: R5, type: Resistor, value: R5, ports: {N1: V3, N2: GND}
]
extrainfo:The circuit is a series-shunt feedback amplifier. Q1 is a differential amplifier responding to the input voltage difference. Q2 provides additional voltage gain, and Q3 acts as an emitter follower to provide current gain. The feedback network consists of resistors R1 and R2, which sample the output voltage and feed it back to the input.

FIGURE 7.23 Series-shunt feedback triple.
In the feedback circuit of Fig. 7.23, $Q_{1}$ responds to the difference $v_{\varepsilon}=v_{i}-v_{f}$, so we have series-type summing. $Q_{2}$ is a CE stage designed to provide additional voltage gain and thus boost the system's loop gain $L . Q_{3}$ is an emitter follower designed to provide current gain at low output resistance. Finally, we note that $v_{o}$ is shunted to the feedback network consisting of $R_{1}$ and $R_{2}$, indicating shunt-type sensing. Functionally, this circuit is similar to the non-inverting op amp of Fig. 7.20. Applying the aforementioned SeriesShunt Procedure, we end up with the error amplifier and feedback network of Fig. 7.24.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: v1, B: Ve, E: X1}
name: Q2, type: NPN, ports: {C: Vc2, B: v1, E: GND}
name: Q3, type: NPN, ports: {C: Vo, B: Vc2, E: GND}
name: R1, type: Resistor, value: R1, ports: {N1: X1, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: OC, N2: Vo}
name: R3, type: Resistor, value: R3, ports: {N1: Vo, N2: GND}
name: R4, type: Resistor, value: R4, ports: {N1: v1, N2: GND}
name: R5, type: Resistor, value: R5, ports: {N1: Vc2, N2: GND}
name: Vε, type: VoltageSource, value: Vε, ports: {Np: Ve, Nn: GND}
]
extrainfo:The circuit is a feedback amplifier with three NPN transistors (Q1, Q2, Q3) and several resistors (R1, R2, R3, R4, R5). It includes a voltage source Vε and is configured to provide voltage gain and current gain, with feedback implemented through resistors R1 and R2. The output voltage Vo is fed back to the input through a feedback network.
image_name:(b)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: OC, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vf, N2: SC}
name: R3, type: Resistor, value: R3, ports: {N1: SC, N2: GND}
name: R4, type: Resistor, value: R4, ports: {N1: v1, N2: GND}
name: R5, type: Resistor, value: R5, ports: {N1: Vc2, N2: GND}
name: Vε, type: VoltageSource, value: Vε, ports: {Np: Ve, Nn: GND}
name: ve, type: VoltageSource, value: ve, ports: {Np: Ve, Nn: ria}
name: vo, type: VoltageSource, value: vo, ports: {Np: SC, Nn: GND}
name: ria, type: Resistor, value: ria, ports: {N1: Ve, N2: GND}
name: roa, type: Resistor, value: roa, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit in diagram (b) represents a feedback network with resistors R1 and R2 forming a voltage divider. The output voltage vo is fed back to the input via this network. The circuit in diagram (a) is an amplifier circuit with three NPN transistors providing voltage and current gain.

FIGURE 7.24 Decomposing the circuit of Fig. 7.23 into (a) the error amplifier and (b) the feedback network.

EXAMPLE 7.10 (a) In the circuit of Fig. 7.23 let $R_{1}=1.0 \mathrm{k} \Omega, R_{2}=3.0 \mathrm{k} \Omega$, and $R_{3}=R_{4}=R_{5}=$ $10 \mathrm{k} \Omega$. Moreover, let all BJTs have $g_{m}=1 /(25 \Omega), r_{\pi}=5 \mathrm{k} \Omega$, and $r_{o}=\infty$. Find $R_{i}, R_{o}$, and the unloaded gain $A_{o c}$.
(b) Verify your results via PSpice.

#### Solution

(a) For the BJTs we have $\beta_{0}=g_{m} r_{\pi}=5000 / 25=200$. Using Fig. 7.24a, we find, by inspection,

$$
\begin{aligned}
& r_{i a}=r_{\pi 1}+\left(\beta_{01}+1\right)\left(R_{1} / / R_{2}\right)=5+201(1 / / 3) \cong 156 \mathrm{k} \Omega \\
& r_{o a}=\frac{R_{5}+r_{\pi 3}}{\beta_{03}+1} / / R_{3} / /\left(R_{1}+R_{2}\right)=\frac{10+5}{201} / / 10 / /(1.0+3.0) \cong 73 \Omega
\end{aligned}
$$

To find the overall voltage gain $a$, examine one stage at a time. We note that $Q_{1}$ is a CE-ED stage, so we use the popular rule of thumb stating that the gain is the negative of the ratio of the total collector-node resistance to the total emitter-node resistance, or

$$
\frac{v_{c 1}}{v_{\varepsilon}}=-\frac{R_{4} / / r_{\pi 2}}{r_{e 1}+\left(R_{1} / / R_{2}\right)}=-\frac{10 / / 5}{0.025+(1.0 / / 3.0)}=-4.3 \mathrm{~V} / \mathrm{V}
$$

One can readily verify that the resistance $R_{b 3}$ seen looking into $Q_{3}$ 's base is such that $R_{b 3} \gg R_{5}$, so the gain provided by $Q_{2}$ is

$$
\frac{v_{c 2}}{v_{c 1}}=-g_{m 2}\left(R_{5} / / R_{b 3}\right) \cong-g_{m 2} R_{5}=-10 / 0.025=-400 \mathrm{~V} / \mathrm{V}
$$

We expect the gain of the voltage follower $Q_{3}$ to be very close to unity,

$$
\frac{v_{o}}{v_{c 2}} \cong 1 \mathrm{~V} / \mathrm{V}
$$

Combining the above results, we finally obtain

$$
a=\frac{v_{o}}{v_{\varepsilon}}=\frac{v_{c 1}}{v_{\varepsilon}} \times \frac{v_{c 2}}{v_{c 1}} \times \frac{v_{o}}{v_{c 2}} \cong(-4.3)(-400)(1)=1720 \mathrm{~V} / \mathrm{V}
$$

We also have, from Fig. 7.24b,

$$
b=\frac{v_{f}}{v_{o}}=\frac{R_{1}}{R_{1}+R_{2}}=\frac{1.0}{1.0+3.0}=\frac{1}{4} \mathrm{~V} / \mathrm{V}
$$

so the loop gain is $L=a b=1720 / 4=430$. Finally,

$$
\begin{aligned}
& A_{o c}=\frac{v_{o}}{v_{i}}=\frac{4}{1+1 / 430}=3.991 \mathrm{~V} / \mathrm{V} \\
& R_{i}=156 \times 10^{3}(1+430)=67 \mathrm{M} \Omega \quad R_{o}=\frac{73}{1+430}=0.17 \Omega
\end{aligned}
$$

Remark: Note that if $Q_{1}$ weren't part of the negative-feedback loop, the resistance seen looking into its emitter would be $r_{e 1}$, or $25 \Omega$ in our example, a rather low value. However, in feedback operation the situation changes dramatically. To get a feel, consider the case $v_{i}=1.0 \mathrm{~V}$. Then, the base current is $i_{b 1}=v_{i} / R_{i}=1 /(67 \mathrm{M} \Omega) \cong$ 15 nA , and the emitter current is $i_{e 1}=\left(\beta_{01}+1\right) i_{b 1}=201(15 \mathrm{nA}) \cong 3 \mu \mathrm{~A}$. On the other hand, the current through $R_{1}$ is $i_{1}=v_{f} / R_{1} \cong v_{i} / R_{1}=(1 \mathrm{~V}) /(1 \mathrm{k} \Omega)=1 \mathrm{~mA}$. Given that $3 \mu \mathrm{~A} \ll 1 \mathrm{~mA}$, there is no question that for all practical purposes $Q_{1}$ 's emitter appears as an open circuit (OC) to $R_{1}$ and $R_{2}$ !
(b) The PSpice circuit of Fig. 7.25 uses three VCCSs to model the BJTs in smallsignal operation, and it includes the $0-\mathrm{V}$ dummy source $V_{0}$ to sense the current out of $Q_{1}$ 's emitter. After directing PSpice to perform the dc analysis as well as the transfer function (. TF ) analysis, we get $A_{o c}=3.99 \mathrm{~V} / \mathrm{V}, R_{i}=65.13 \mathrm{M} \Omega$, and $R_{o}=0.1739 \Omega$. Moreover, the current through the test source $V_{0}$ for $v_{i}=$ 1.0 V is $3.086 \mu \mathrm{~A}$. All data are amazingly close to those calculated by hand!
image_name:FIGURE 7.25
description:The circuit is a multi-stage amplifier with voltage-controlled current sources (G1, G2, G3) and resistive loads (R1, R2, R3, R4, R5). The input voltage source vi is connected to the first stage, and the output is taken across R3. The circuit also includes a dummy voltage source V0 for sensing the current.

FIGURE 7.25 PSpice circuit to verify the series-shunt triple of Example 7.10.

EXAMPLE 7.11 Assuming $g_{m}=1 \mathrm{~mA} / \mathrm{V}$ and $r_{o}=50 \mathrm{k} \Omega$ for all FETs in the circuit of Fig. 7.26, along with $\chi_{5}=0.25$, find the unloaded gain $A_{o c}$ and the output resistance $R_{o}\left(R_{i}=\infty\right.$ because the input source is looking right into $M_{1}$ 's gate).
image_name:Figure 7.26
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: VSS}
name: M1, type: NMOS, ports: {S: P, D: X1, G: Vi}
name: M2, type: NMOS, ports: {S: P, D: X2, G: vo}
name: M3, type: PMOS, ports: {S: VDD, D: X2, G: X1}
name: M4, type: PMOS, ports: {S: VDD, D: X1, G: X1}
name: M5, type: NMOS, ports: {S: VDD, D: Vo, G: X2}
name: IS5, type: CurrentSource, value: IS5, ports: {Np: Vo, Nn: VSS}
]
extrainfo:The circuit is a series-shunt feedback amplifier with a dummy voltage source for current sensing. It includes a differential amplifier stage with M1 and M2, a current mirror load with M3 and M4, and a source follower with M5. The unloaded gain and output resistance are to be calculated.

FIGURE 7.26 Series-shunt circuit of Example 7.11.

#### Solution

This is a unity-gain non-inverting amplifier whose decomposition appears as in Fig. 7.27. The voltage gain of the first stage is $g_{m}\left(r_{o p} / / r_{o n}\right)=g_{m} r_{o} / 2$ and that of the $M_{5}$ source follower is $1 /\left(1+\chi_{5}\right)$, so we write

$$
a=\frac{v_{o}}{v_{\varepsilon}}=\frac{g_{m} r_{o} / 2}{1+\chi_{5}}=\frac{1 \times 50 / 2}{1+0.25}=20 \mathrm{~V} / \mathrm{V} \quad b=1.0 \mathrm{~V} / \mathrm{V} \quad L=20
$$

We also have $r_{o a}=1 /\left[g_{m 5}\left(1+\chi_{5}\right)\right]=1 / 1.25=800 \Omega$. Consequently,
image_name:(a)
description:
[
name: v_e, type: VoltageSource, ports: {Np: v_e, Nn: GND}
name: M1, type: NMOS, ports: {S: s1s2, D: X1, G: v_e}
name: M2, type: NMOS, ports: {S: s1s2, D: x2, G: GND}
name: M3, type: PMOS, ports: {S: GND, D: x2, G: x1}
name: M4, type: PMOS, ports: {S: GND, D: x1, G: x1}
name: M5, type: NMOS, ports: {S: vo, D: GND, G: x2}
]
extrainfo:The circuit is a multi-stage amplifier with NMOS and PMOS transistors. It includes a voltage source for input and output. The circuit is designed to provide amplification with feedback.
image_name:(b)
description:
[
name: Vo, type: VoltageSource, ports: {Np: vf, Nn: GND}
]
extrainfo:The circuit diagram (b) is a simplified representation focusing on the output voltage Vo and feedback voltage vf. It includes a single NMOS transistor M5, connected to the output node vo. The voltage source Vε is connected between node ve and ground, and another voltage source Vo is connected between node vf and SC.

FIGURE 7.27 Decomposing the circuit of Fig. 7.26 into (a) the error amplifier and (b) the feedback network.

As our last example, let us investigate the emitter follower of Fig. 7.28a. On a variety of occasions it has been said that a resistance in series with the emitter of a BJT or with the source of a FET introduces degeneration, and that, among other things, it stabilizes the dc bias point. We now wish to reexamine this issue from the viewpoint of negative feedback. The BJT responds to the signal $v_{\varepsilon}=v_{i}-v_{o}$, indicating
image_name:Figure 7.28 (a)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: RE, type: Resistor, value: RE, ports: {N1: vo, N2: GND}
name: NPN, type: NPN, ports: {C: GND, B: Vi, E: vo}
]
extrainfo:The circuit is an emitter follower configuration with negative feedback. It stabilizes the DC bias point using degeneration through the resistor RE. The NPN transistor is used as the main amplifying device.
image_name:Figure 7.28 (b)
description:
[
'name': 'Vi', 'type': 'VoltageSource', 'value': 'Vi', 'ports': {'Np': 'Vi', 'Nn': 'GND'
'name': 'rπ', 'type': 'Resistor', 'value': 'rπ', 'ports': {'N1': 'vi', 'N2': 'vf'
'name': 'ro', 'type': 'Resistor', 'value': 'ro', 'ports': {'N1': 'GND', 'N2': 'vo'
'name': 'gmve', 'type': 'VoltageControlledCurrentSource', 'ports': {'Np': 'GND', 'Nn': 'vo'
'name': 'RE', 'type': 'Resistor', 'value': 'RE', 'ports': {'N1': 'vo', 'N2': 'GND'
]
extrainfo:The circuit is an emitter follower with negative feedback. It uses a BJT and includes resistors for bias stabilization and feedback. The voltage source Vi provides the input signal. The current source gmve represents the transconductance of the transistor.

FIGURE 7.28 The emitter follower as a negative-feedback system: (a) ac equivalent and (b) small-signal representation.
image_name:(a)
description:
[
name: vε, type: VoltageSource, ports: {Np: GND, Nn: vπ}
name: rπ, type: Resistor, value: rπ, ports: {N1: vπ, N2: SC}
name: gmvπ, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: vo}
name: RE, type: Resistor, value: RE, ports: {N1: vo, N2: GND}
name: ro, type: Resistor, value: ro, ports: {N1: vo, N2: GND}
]
extrainfo:The circuit is an emitter follower with negative feedback. It uses a BJT and includes resistors for bias stabilization and feedback. The voltage source vε provides the input signal. The current source gmvπ represents the transconductance of the transistor.
image_name:(b)
description:
[
name: vo, type: VoltageSource, ports: {Np: vf, Nn: GND}
]
extrainfo:The diagram represents a small-signal model of an emitter follower with feedback. It includes a voltage source vo representing the output voltage and a feedback voltage vf. The circuit is simplified to show the feedback path.

FIGURE 7.29 Decomposing the feedback circuit of Fig. 7.28 into (a) the error amplifier and (b) the feedback network.
a series-shunt configuration with $b=1 \mathrm{~V} / \mathrm{V}$. To decompose the circuit into the error amplifier and the feedback network, refer to the small-signal equivalent of Fig. 7.28b.

Following the aforementioned Series-Shunt Procedure, we first ground node $v_{o}$ to find loading at the amplifier's input. This yields the left portion of the circuit of Fig. 7.29a. Next, we open-circuit node $v_{f}$ to find loading at the amplifier's output. This yields the right portion of the circuit of Fig. 7.29a. (It is certainly intriguing that the same node, namely, the emitter node, acts as a short or as an open circuit, depending on the viewpoint!) Finally, the feedback network appears as in Fig. 7.29b, giving $b=1 \mathrm{~V} / \mathrm{V}$.

EXAMPLE 7.12 In the emitter follower of Fig. 7.28a let $R_{E}=10 \mathrm{k} \Omega$. Moreover, let the BJT have $g_{m}=1 /(25 \Omega), r_{\pi}=5 \mathrm{k} \Omega$, and $r_{o}=100 \mathrm{k} \Omega$. Find $R_{i}, R_{o}$, and the unloaded gain $A_{o c}$. Comment on your findings.

#### Solution

With reference to Fig. 7.29a we have, by inspection,

$$
\begin{aligned}
& r_{i a}=r_{\pi}=5 \mathrm{k} \Omega \quad r_{o a}=R_{E} / / r_{o}=10 / / 100=9.09 \mathrm{k} \Omega \\
& a=\frac{v_{o}}{v_{\varepsilon}}=g_{m}\left(R_{E} / / r_{o}\right)=9.09 / 0.025 \cong 364 \mathrm{~V} / \mathrm{V}
\end{aligned}
$$

With reference to Fig. $7.29 b$ we have $b=v_{f} / v_{o}=1 \mathrm{~V} / \mathrm{V}$, so

$$
L=a \times 1=g_{m}\left(R_{E} / / r_{o}\right)=364
$$

Finally,

$$
\begin{aligned}
& A_{o c}=\frac{1}{1+1 /\left[g_{m}\left(R_{E} / / r_{o}\right)\right]}=\frac{1}{1+1 / 364}=0.997 \mathrm{~V} / \mathrm{V} \\
& R_{i}=r_{\pi}\left[1+g_{m}\left(R_{E} / / r_{o}\right)\right]=5(1+364)=1.83 \mathrm{M} \Omega \\
& R_{o}=\frac{R_{E} / / r_{o}}{1+g_{m}\left(R_{E} / / r_{o}\right)}=\frac{1}{g_{m}} / / R_{E} / / r_{o} \cong \frac{1}{g_{m}} \cong r_{e}=25 \Omega
\end{aligned}
$$

The interested student can, after suitable manipulations, compare the above expressions with their exact counterparts of Section 2.9. The minor differences (such as $\beta_{0}$ instead of $\beta_{0}+1$ ) stem from the fact that the method used here is based on Eqs. $7.45 a$ and $b$, and as such it is an approximation-though a fairly good one in this case, as confirmed by the numerical results.

Remark: It is interesting to note that a feedback circuit can in turn be part of another more complex feedback circuit: an example is the emitter follower subcircuit $\left(Q_{3}\right)$ of the series-shunt triple of Fig. 7.23.

### Shunt-Shunt Circuits

In Fig. 7.30 we re-examine the shunt-shunt op amp configuration of Fig. 7.18b, but with an eye on the interaction between the amplifier's internal resistances $r_{i}$ and $r_{o}$ and the external feedback network, in this case consisting of $R$. To be able to focus on loading by the feedback network alone, we continue to assume a driving source $i_{i}$ with infinite parallel resistance, and an unloaded (open-circuited) output port.

As we know, because of the high gain $a_{v}$, the differential input voltage $v_{d}$ is going to be vanishingly small, indicating that the inverting-input node will be kept at virtual-ground potential. Thus, to calculate loading at the amplifier's output port, we regard $R$ as if its left terminal were short-circuited (SC) to ground. To find loading at the input, we note that sensing at the output is of the shunt type, just as in the case of the series-shunt circuit of Fig. 7.20. Consequently, to calculate loading at the amplifier's input port, we regard $R$ as if its right terminal were short-circuited (SC) to ground. Both situations are depicted in Fig. 7.31a, which shows the error amplifier in open-loop operation, but with loading by the external feedback network specifically taken into account at both ports. Next, we wish to find its open-loop parameters, now denoted as $a\left(=v_{o} / i_{\varepsilon}\right), r_{i a}$ and $r_{o a}$. By the voltage divider rule and Ohm's law,

$$
v_{o}=\frac{R}{r_{o}+R} a_{v} v_{d}=\frac{R}{r_{o}+R} a_{v}\left(r_{i} / / R\right)\left(-i_{\varepsilon}\right)
$$

image_name:FIGURE 7.30
description:
[
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'vo', 'N2': vf'
'name': 'ri', 'type': 'Resistor', 'value': 'ri', 'ports': {'N1': 'vf', 'N2': 'GND'
'name': 'avd', 'type': 'VoltageControlledVoltageSource', 'value': 'avd', 'ports': {'Np': 'vd', 'Nn': 'GND'
'name': 'ii', 'type': 'CurrentSource', 'ports': {'Np': 'GND', 'Nn': 'Vf'
'name': 'OpAmp', 'type': 'OpAmp', 'ports': {'InP': 'GND', 'InN': 'vf', 'OutP': 'vo'
]
extrainfo:This circuit is a transresistance operational amplifier with internal resistances ri and ro. The voltage-controlled voltage source avd is part of the op-amp model.

FIGURE 7.30 The transresistance op amp with its internal resistances $r_{i}$ and $r_{0}$ explicitly shown.
image_name:(a)
description:
[
name: ie, type: CurrentSource, value: ie, ports: {Np: GND, Nn: Vf}
name: ri, type: Resistor, value: ri, ports: {N1: vf, N2: GND}
name: avvd, type: VoltageControlledVoltageSource, value: avvd, ports: {Np: avd, Nn: GND}
name: ro, type: Resistor, value: ro, ports: {N1: avd, N2: vo}
name: R, type: Resistor, value: R, ports: {N1: vo, N2: GND}
name: OpAmp, type: OpAmp, ports: {InP: GND, InN: vd, OutP: vo}
]
extrainfo:This circuit is a transresistance operational amplifier with internal resistances ri and ro. The voltage-controlled voltage source avd is part of the op-amp model.
image_name:(b)
description:
[
name: R, type: Resistor, value: R, ports: {N1: GND, N2: vo}
name: vo, type: VoltageSource, value: vo, ports: {Np: vo, Nn: GND}
]
extrainfo:This is a feedback network circuit consisting of a current source if, a resistor R, and a voltage source vo. The circuit is connected to ground at multiple points, forming a loop with the resistor and voltage source.

FIGURE 7.31 Decomposing the circuit of Fig. 7.30 into (a) basic amplifier and (b) feedback network.
so that

$$
\begin{equation*}
a=\frac{v_{o}}{i_{\varepsilon}}=-\left(r_{i} / / R\right) a_{v} \frac{R}{r_{o}+R} \tag{7.50}
\end{equation*}
$$

Note that $a$ now has the dimensions of V/A, and is negative. Moreover, by inspection, we have

$$
\begin{equation*}
r_{i a}=r_{i} / / R \quad r_{o a}=r_{o} / / R \tag{7.51}
\end{equation*}
$$

Next, we seek a representation for the feedback network that is separate from the basic amplifier. Referring back to Fig. 7.30, we observe that at the sensing side this network is driven by a voltage source $v_{o}$ expected to exhibit extremely small series resistance $R_{o}$, and that at the summing side it drives the amplifier's input port which, for practical purposes, appears as a short circuit (SC). The circuit for the calculation of $b$ is thus as in Fig. $7.31 b$, from which we readily find $i_{f}=\left(0-v_{o}\right) / R$, so

$$
\begin{equation*}
b=\frac{i_{f}}{v_{o}}=-\frac{1}{R} \tag{7.52}
\end{equation*}
$$

The dimensions of $b$ are $\mathrm{A} / \mathrm{V}$, the reciprocal of those of $a$. Moreover, $b$ is negative, just like $a$. Both properties are consistent with the fact that $L=a b$ must be dimensionless and positive. We can now apply Eq. (7.34) to find the unloaded gain $A_{o c}$, and Eq. (7.35), but with $r_{i}$ and $r_{o}$ replaced by $r_{i a}$ and $r_{o a}$, to find the closed-loop terminal resistances $R_{i}$, and $R_{o}$.

EXAMPLE 7.13 In the circuit of Fig. 7.30 let the op amp have $a_{v}=10^{5} \mathrm{~V} / \mathrm{V}, r_{i}=2 \mathrm{M} \Omega$, and $r_{o}=$ $100 \Omega$. If $R=1.0 \mathrm{M} \Omega$, find $R_{i}, R_{o}$, and the unloaded gain $A_{o c}$.

#### Solution

Using Eqs. (7.50) through (7.52) we have

$$
\begin{aligned}
& r_{i a}=(2 / / 1) \times 10^{6}=667 \mathrm{k} \Omega \quad r_{o a}=100 / / 10^{6}=100 \Omega \\
& a=-(2 / / 1) 10^{6} \times 10^{5} \frac{10^{6}}{100+10^{6}}=-6.66 \times 10^{10} \mathrm{~V} / \mathrm{A} \quad b=-10^{-6} \mathrm{~A} / \mathrm{V}
\end{aligned}
$$

$$
\begin{aligned}
L & =\left(-6.667 \times 10^{10}\right)\left(-10^{-6}\right)=66,667 \\
A_{o c} & =\frac{-10^{6}}{1+1 / 66,667} \cong-1.0 \mathrm{~V} / \mu \mathrm{A} \\
R_{i} & =\frac{667 \mathrm{k} \Omega}{66,667}=10 \Omega \\
R_{o} & =\frac{100 \Omega}{66,667}=1.5 \mathrm{~m} \Omega
\end{aligned}
$$

The line of reasoning developed for the above example can be generalized to the following Shunt-Shunt Procedure:

- To calculate loading at the input of the basic amplifier, short-circuit (SC) the sensing-side port of the feedback network.
- To calculate loading at the output of the basic amplifier, short-circuit (SC) the summing-side port of the feedback network.
- To find $b$, apply a voltage $v_{o}$ to the sensing-side port of the feedback network, find the short-circuit current $i_{f}$ flowing into the summing-side port of the feedback network, and let $b=i_{f} / v_{o}$.
We shall illustrate the procedure with additional examples.
The feedback circuit of Fig. 7.32 is similar to that of Fig. 7.23, except that the input source is now a current that has been moved to $Q_{1}$ 's emitter, while the base has been grounded. Thus, $Q_{1}$ is now operating in the CB mode. As we know, the resistance seen looking into its emitter is low to begin with, and we anticipate that feedback will make it even lower. Applying the aforementioned Shunt-Shunt Procedure, we end up with the basic amplifier and feedback network of Fig. 7.33.
image_name:FIGURE 7.32 Shunt-shunt feedback triple
description:
[
name: Q1, type: NPN, ports: {C: V2, B: GND, E: V1}
name: Q2, type: NPN, ports: {C: V3, B: V2, E: GND}
name: Q3, type: NPN, ports: {C: GND, B: V3, E: vo}
name: R1, type: Resistor, value: R1, ports: {N1: V1, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vo, N2: V1}
name: R3, type: Resistor, value: R3, ports: {N1: Vo, N2: GND}
name: R4, type: Resistor, value: R4, ports: {N1: V2, N2: GND}
name: R5, type: Resistor, value: R5, ports: {N1: V3, N2: GND}
name: Ii, type: CurrentSource, value: Ie, ports: {Np: GND, Nn: V1}
]
extrainfo:The circuit is a shunt-shunt feedback amplifier using three NPN transistors. Q1 operates in common-base mode, and feedback is applied to reduce the input resistance.

FIGURE 7.32 Shunt-shunt feedback triple.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: vc1, B: ve1, E: GND}
name: Q2, type: NPN, ports: {C: vc2, B: vc1, E: GND}
name: Q3, type: NPN, ports: {C: GND, B: vc2, E: vo}
name: R1, type: Resistor, value: R1, ports: {N1: ve1, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: ve1, N2: GND}
name: R22, type: Resistor, value: R22, ports: {N1: ve1, N2: GND}
name: R3, type: Resistor, value: R3, ports: {N1: vo, N2: GND}
name: R4, type: Resistor, value: R4, ports: {N1: vc1, N2: GND}
name: R5, type: Resistor, value: R5, ports: {N1: vc2, N2: GND}
name: Ie, type: CurrentSource, value: Ie, ports: {Np: GND, Nn: ve1}
]
extrainfo:The circuit is a shunt-shunt feedback amplifier using three NPN transistors. Q1 operates in common-base mode, and feedback is applied to reduce the input resistance. The circuit is decomposed into an error amplifier and a feedback network.
image_name:(b)
description:
[
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'vo, 'N2': 'GND'
'name': 'Vo', 'type': 'VoltageSource', 'value': 'Vo', 'ports': {'Np': 'Vo', 'Nn': 'GND'
]
extrainfo:The circuit is a shunt-shunt feedback amplifier using three NPN transistors. Q1 operates in common-base mode, and feedback is applied to reduce the input resistance. The circuit decomposed in (b) shows the feedback network with a resistor R2 and a voltage source Vo.

FIGURE 7.33 Decomposing the circuit of Fig. 7.32 into (a) the error amplifier and (b) the feedback network.

EXAMPLE 7.14 (a) Let the circuit of Fig. 7.32 have the same parameters of Example 7.10, namely, $R_{1}=1.0 \mathrm{k} \Omega, R_{2}=3.0 \mathrm{k} \Omega$, and $R_{3}=R_{4}=R_{5}=10 \mathrm{k} \Omega$. Moreover, let all BJTs have $g_{m}=1 /(25 \Omega), r_{\pi}=5 \mathrm{k} \Omega$, and $r_{o}=\infty$. Find $R_{i}, R_{o}$, and the unloaded gain $A_{o c}$.
(b) Compare with Example 7.10, and justify similarities as well as differences.

#### Solution

(a) Retracing similar steps as in Example 7.10 using the circuit of Fig. 7.33 we find

$$
\begin{aligned}
& r_{i a}=r_{e 1} / / R_{1} / / R_{2}=24.2 \Omega \quad r_{o a}=\frac{R_{5}+r_{\pi 3}}{\beta_{03}+1} / / R_{2} / / R_{3} \cong 72.3 \Omega \\
& \frac{v_{e 1}}{i_{\varepsilon}}=r_{i a}=24.2 \mathrm{~V} / \mathrm{A} \quad \frac{v_{c 1}}{v_{e 1}}=g_{m 1}\left(R_{4} / / r_{\pi 2}\right)=133 \mathrm{~V} / \mathrm{V} \\
& \frac{v_{c 2}}{v_{c 1}}=-g_{m 2}\left(R_{5} / / R_{b 3}\right)=-400 \mathrm{~V} / \mathrm{V} \quad \frac{v_{o}}{v_{c 2}} \cong 1 \mathrm{~V} / \mathrm{V} \\
& a=\frac{v_{o}}{i_{\varepsilon}}=\frac{v_{e 1}}{i_{\varepsilon}} \times \frac{v_{c 1}}{v_{e 1}} \times \frac{v_{c 2}}{v_{c 1}} \times \frac{v_{o}}{v_{c 2}} \cong(24.2)(133)(-400)(1)=-1.29 \times 10^{6} \mathrm{~V} / \mathrm{A} \\
& b=\frac{i_{f}}{v_{o}}=-\frac{1}{R_{2}}=-\frac{1}{3 \times 10^{3}} \mathrm{~A} / \mathrm{V} \quad L=a b=\frac{-1.29 \times 10^{6}}{-3 \times 10^{3}}=430 \\
& A_{o c}=\frac{v_{o}}{i_{i}}=\frac{-3 \times 10^{3}}{1+1 / 430}=-2.993 \mathrm{~V} / \mathrm{mA} \\
& R_{i}=\frac{24.2}{1+430}=0.056 \Omega \quad R_{o}=\frac{72.3}{1+430} \cong 0.168 \Omega
\end{aligned}
$$

(b) We immediately observe that even though $a$ and $b$ are quite different in the two examples, both in values and dimensions, their product $L=a b$ is the same (430). However, some of the closed-loop parameters have changed drastically because of the different feedback topology. In both cases, output sensing is of the shunt type, so $R_{o}$ is virtually unchanged. By contrast, $R_{i}$ changes from $67 \mathrm{M} \Omega$ in the input-series circuit of Example 7.10, to $0.056 \Omega$ in the inputshunt circuit of the present example-quite a change! Also, the closed-loop gain has changed in value, dimensions, and even polarity, as it should be.

As our last example, we turn to the ac circuit of Fig. $7.34 a$, representing the familiar feedback-bias scheme. As we know, this scheme offers a good dc biasing alternative for a transistor. By inspection we find that this circuit is a shunt-shunt type. We thus apply the aforementioned Shunt-Shunt Procedure to end up with the decompositions of Fig. 7.34b and $c$.
(a) In the shunt-shunt circuit of Fig. $7.34 a$ let $R_{B}=100 \mathrm{k} \Omega$ and $R_{C}=10 \mathrm{k} \Omega$.

EXAMPLE 7.15 Moreover, let the BJT have $g_{m}=1 /(25 \Omega), r_{\pi}=5 \mathrm{k} \Omega$, and $r_{o}=100 \mathrm{k} \Omega$. Find $R_{i}, R_{o}$, and the unloaded gain $A_{o c}$.
(b) Repeat if $R_{B}$ is lowered to $5.0 \mathrm{k} \Omega$. Comment.

#### Solution

(a) With reference to Figs. $7.34 b$ and $c$ we have, by inspection,

$$
r_{i a}=R_{B} / / r_{\pi}=100 / / 5=4.76 \mathrm{k} \Omega \quad r_{o a}=R_{C} / / R_{B} / / r_{o}=10 / / 100 / / 100=8.33 \mathrm{k} \Omega
$$

$$
\begin{aligned}
& \frac{v_{b}}{i_{\varepsilon}}=r_{i a}=4.76 \mathrm{~V} / \mathrm{mA} \quad \frac{v_{o}}{v_{b}}=-g_{m} r_{o a}=-\frac{8.333}{0.025}=-333 \mathrm{~V} / \mathrm{V} \\
& a=\frac{v_{o}}{i_{\varepsilon}}=\frac{v_{b}}{i_{\varepsilon}} \times \frac{v_{o}}{v_{b}}=-g_{m} r_{i a} r_{o a}=\left(4.76 \times 10^{3}\right)(-333)=-1.59 \times 10^{6} \mathrm{~V} / \mathrm{A}
\end{aligned}
$$

image_name:(a)
description:
[
name: RC, type: Resistor, value: RC, ports: {N1: GND, N2: Vo}
name: RB, type: Resistor, value: RB, ports: {N1: Vo, N2: v1}
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: NPN, type: NPN, ports: {C: Vo, B: V1, E: GND}
]
extrainfo:The circuit is a feedback-bias BJT configuration as a shunt-shunt circuit. The input current is 'ii', and the feedback current is 'if'. The output voltage is 'Vo'. The resistors RC, RB, and Ro are connected to form a parallel combination at node Vo.

image_name:(b)
description:
[
name: RC, type: Resistor, value: RC, ports: {N1: Vo, N2: GND}
name: RB, type: Resistor, value: RB, ports: {N1: Vb, N2: GND}
name: RB, type: Resistor, value: RB, ports: {N1: Vo, N2: GND}
name: NPN, type: NPN, ports: {C: Vo, B: Vb, E: GND}
name: ie, type: CurrentSource, value: ie, ports: {Np: GND, Nn: Vb}
]
extrainfo:The circuit is a feedback-bias BJT configuration as a shunt-shunt circuit. The input current is 'ii', and the feedback current is 'if'. The output voltage is 'Vo'. The resistors RC, RB, and Ro are connected to form a parallel combination at node Vo.
image_name:(c)
description:
[
name: RB, type: Resistor, value: RB, ports: {N1: Vo, N2: GND}
name: Vo, type: VoltageSource, value: Vo, ports: {Np: Vo, Nn: GND}
]
extrainfo:The circuit is a feedback network with a shunt-shunt configuration. The feedback current is 'if', and the output voltage is 'Vo'. The resistor RB is connected in series with the feedback network.

FIGURE 7.34 (a) The feedback-bias BJT configuration as a shunt-shunt circuit. (b) Error amplifier and (c) feedback network.

$$
\begin{aligned}
& b=\frac{i_{f}}{v_{o}}=-\frac{1}{R_{B}}=-\frac{1}{10^{5}} \mathrm{~A} / \mathrm{V} \quad L=a b=\frac{-1.59 \times 10^{6}}{-10^{5}}=15.9 \\
& A_{o c}=\frac{v_{o}}{i_{i}}=-\frac{10^{5}}{1+1 / 15.9}=-94 \mathrm{~V} / \mathrm{mA} \\
& R_{i}=\frac{4.76}{1+15.9} \cong 0.28 \mathrm{k} \Omega \quad R_{o}=\frac{8.33}{1+15.9} \cong 0.5 \mathrm{k} \Omega
\end{aligned}
$$

(b) With $R_{B}=5.0 \mathrm{k} \Omega$ we get $r_{i a}=2.5 \mathrm{k} \Omega, r_{o a}=3.23 \mathrm{k} \Omega, a=-3.23 \times 10^{5} \mathrm{~V} / \mathrm{A}$, and $b=-1 /\left(5 \times 10^{3}\right) \mathrm{A} / \mathrm{V}$. Consequently,

$$
L=65.5 \quad A_{o c}=-4.925 \mathrm{~V} / \mathrm{mA} \quad R_{i}=38.2 \Omega \quad R_{o}=49.2 \Omega
$$

Note the significant increase in the value of $L$, from 15.9 to 65.5 . Can you justify this intuitively?

### Series-Series Circuits

In Fig. 7.35 we re-examine the series-series op amp configuration of Fig. $7.18 c$, but with the usual eye on the interaction between the amplifier's internal resistances $r_{i}$ and $r_{o}$ and the external feedback network, in this case consisting of $R$. To be able to focus on loading by the feedback network alone, we continue to assume the absence of any external loading, meaning a driving source $v_{i}$ with zero series resistance, and a short-circuit output load (note that an unloaded output port is an open circuit for a voltage-output device, but a short circuit for a current-output type).

As already seen in connection with the circuit of Fig. 7.20, the op amp's input port appears as an open circuit to the feedback network, so to calculate loading at the amplifier's output we regard the wire to the left of $R$ as an open circuit (OC). To find loading at the input, we note that sensing at the output is of the series type, where we anticipate a high closed-loop resistance. Consequently, to calculate loading at the amplifier's input port, we regard $R$ as if its terminal facing the load was open-circuited (OC).
image_name:FIGURE 7.35
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: Vf, N2: GND}
name: OpAmp, type: OpAmp, value: OpAmp, ports: {InP: Vi, InN: Vf, OutP: Vf}
]
extrainfo:The circuit is a transconductance operational amplifier with internal resistances ri and ro. It features a feedback network with a series sensing output.

FIGURE 7.35 The transconductance op amp with its internal resistances $r_{i}$ and $r_{0}$ explicitly shown.
image_name:(a)
description:
[
name: Vε, type: VoltageSource, ports: {Np: Vε, Nn: GND}
name: rᵢ, type: Resistor, value: rᵢ, ports: {N1: Ve, N2: GND}
name: aᵥvₑ, type: VoltageControlledVoltageSource, ports: {Np: Vd, Nn: GND}
name: rₒ, type: Resistor, value: rₒ, ports: {N1: vd, N2: V2}
name: R, type: Resistor, value: R, ports: {N1: V1, N2: GND}
name: R, type: Resistor, value: R, ports: {N1: V2, N2: GND'}
]
extrainfo:The circuit is a transconductance operational amplifier with internal resistances ri and ro. It features a feedback network with a series sensing output. The diagram shows an error amplifier in open-loop operation with loading by an external feedback network.
image_name:(b)
description:
[
name: R, type: Resistor, value: R, ports: {N1: Vi, N2: GND}
name: io, type: CurrentSource, value: io, ports: {Np: GND, Nn: Vf}
]
extrainfo:The circuit diagram (b) represents a feedback network with a current source io flowing from node Vf to ground. It is part of a transconductance operational amplifier circuit with internal resistances and a feedback network.

FIGURE 7.36 Decomposing the circuit of Fig. 7.35 into (a) the error amplifier, and (b) the feedback network.

The two situations are depicted in Fig. 7.36a, which represents the error amplifier in open-loop operation, but with loading by the external feedback network specifically taken into account at both ports. Next, we wish to find its open-loop parameters, now denoted as $a, r_{i a}$ and $r_{o a}$. By Ohm's law and the voltage divider rule,

$$
i_{o}=\frac{a_{v} v_{d}}{r_{o}+R}=\frac{1}{r_{o}+R} a_{v} \frac{r_{i}}{r_{i}+R} v_{\varepsilon}
$$

so

$$
\begin{equation*}
a=\frac{i_{o}}{v_{\varepsilon}}=\frac{r_{i}}{r_{i}+R} a_{v} \frac{1}{r_{o}+R} \tag{7.53}
\end{equation*}
$$

Note that $a$ now has the dimensions of $\mathrm{A} / \mathrm{V}$. Moreover, the resistances seen by the input source $v_{\varepsilon}$ and by the short-circuit load are, respectively,

$$
\begin{equation*}
r_{i a}=r_{i}+R \quad r_{o a}=r_{o}+R \tag{7.54}
\end{equation*}
$$

Next, we seek a representation for the feedback network that is separate from the basic amplifier. Referring back to Fig. 7.35, we observe that at the sensing side $R$ is driven by a current source $i_{o}$ expected to exhibit extremely high parallel resistance $R_{o}$, and that at the summing side it drives the amplifier's input port which, for practical purposes, appears as an open circuit (OC). The circuit to calculate $b$ is thus as in Fig. 7.36b, from which we readily find $v_{f}=R i_{o}$, so

$$
\begin{equation*}
b=\frac{v_{f}}{i_{o}}=R \tag{7.55}
\end{equation*}
$$

The dimensions of $b$ are V/A, the reciprocal of those of $a$, as it must be in order to make $L$ dimensionless. As usual, we now apply Eq. (7.36) to find the unloaded gain $A_{s c}$, and Eq. (7.37), but with $r_{i}$ and $r_{o}$ replaced by $r_{i a}$ and $r_{o a}$, to find the closed-loop terminal resistances $R_{i}$ and $R_{o}$.

EXAMPLE 7.16 (a) In the circuit of Fig. 7.35 let the op amp have $a_{v}=10^{3} \mathrm{~V} / \mathrm{V}, r_{i}=100 \mathrm{k} \Omega$, and $r_{o}=1.0 \mathrm{k} \Omega$. If $R=10 \mathrm{k} \Omega$, find $R_{i}, R_{o}$, and the unloaded gain $A_{s c}$.
(b) If $v_{i}=5.0 \mathrm{~V}$, what is the short-circuit output current? If the short-circuit is replaced by a load that develops a $4.0-\mathrm{V}$ voltage drop, by how much will the output current change? Comment.

#### Solution

(a) Using Eqs. (7.53) through (7.55) we have

$$
\begin{aligned}
& a=\frac{100}{100+10} 10^{3} \frac{1}{(1+10) 10^{3}}=\frac{1}{12.1} \mathrm{~A} / \mathrm{V} \quad b=10^{4} \mathrm{~V} / \mathrm{A} \\
& L=\frac{10^{4}}{12.1}=826 \\
& r_{i a}=100+10=110 \mathrm{k} \Omega \quad r_{o a}=1+10=11 \mathrm{k} \Omega \\
& A_{s c}=\frac{1 / 10^{4}}{1+1 / 826}=99.88 \mu \mathrm{~A} / \mathrm{V} \quad R_{i}=110(1+826)=91 \mathrm{M} \Omega \\
& R_{o}=11(1+826)=9.1 \mathrm{M} \Omega
\end{aligned}
$$

(b) The short-circuit output current is $i_{o}=A_{s c} v_{i}=99.88 \times 5.0=499.4 \mu \mathrm{~A}$ (ideally, $500 \mu \mathrm{~A}$ ). Visualizing the output port via its Norton equivalent, we note that with a $4.0-\mathrm{V}$ load-voltage increase, the current will decrease by $(4.0 \mathrm{~V}) /(9.1 \mathrm{M} \Omega)=0.44 \mu \mathrm{~A}$, an insignificant amount. This, thanks to the high output resistance brought about by negative feedback!

The line of reasoning developed for the above example can be generalized to the following Series-Series Procedure:

- To calculate loading at the input of the basic amplifier, open-circuit (OC) the sensing-side port of the feedback network.
- To calculate loading at the output of the basic amplifier, open-circuit (OC) the summing-side port of the feedback network.
- To find $b$, apply a current $i_{o}$ to the sensing-side port of the feedback network, find the open-circuit voltage $v_{f}$ at the summing-side port of the feedback network, and let $b=v_{f} / i_{o}$.

Let us illustrate the procedure using the single BJT circuit of Fig. 7.37, here operated in the series-series mode to act as a voltage-to-current (V-I) converter. The circuit is similar to the CC of Fig. 7.28, except that the output is now the short-circuit collector current instead of the open-circuit emitter voltage. To decompose the feedback circuit into the basic error amplifier and the feedback network, refer to the small-signal equivalent of Fig. 7.37b, where we note that the current being sensed is not $i_{o}$ itself, but $i_{o} / \alpha_{0}$.
image_name:(a)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: RE, type: Resistor, value: RE, ports: {N1: X1, N2: GND}
name: NPN, type: NPN, ports: {C: GND, B: Vi, E: X1}
]
extrainfo:This circuit is a single-BJT voltage-to-current (V-I) converter operating in series-series feedback mode. It converts an input voltage to an output current by sensing the current through the feedback network. The circuit uses a BJT in common collector configuration with feedback provided by a resistor network.
image_name:(b)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: vi, N2: vf}
name: ro, type: Resistor, value: ro, ports: {N1: vf, N2: GND}
name: RE, type: Resistor, value: RE, ports: {N1: vf, N2: GND}
]
extrainfo:The circuit is a single-BJT voltage-to-current (V-I) converter operating in series-series feedback mode. It senses the current i_o/α_0 instead of i_o directly.

FIGURE 7.37 The single-BJT voltage-to-current (V-I) converter as a series-series feedback system. (a) Ac equivalent and (b) small-signal representation.

Following the aforementioned Series-Series Procedure, we open-circuit at the right-hand side of $R_{E}$ to find loading at the input, thus obtaining the left portion of the circuit of Fig. 7.38a. Likewise, we open-circuit at the left-hand side of $R_{E}$ to find loading at the output, thus obtaining the right portion of the circuit of Fig. 7.38a. Finally, we drive the feedback network $R_{E}$ with the current $i_{o} / a_{0}$ to find $v_{f}$
image_name:(a)
description:
[
name: vE, type: VoltageSource, value: vE, ports: {Np: VE, Nn: GND}
name: r_π, type: Resistor, value: r_π, ports: {N1: Ve, N2: V1}
name: RE, type: Resistor, value: RE, ports: {N1: V1, N2: GND}
name: g_mv_π, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: V2}
name: ro, type: Resistor, value: ro, ports: {N1: V2, N2: GND}
name: RE, type: Resistor, value: RE, ports: {N1: V2, N2: GND}
]
extrainfo:The circuit diagram (a) represents an error amplifier with a feedback network represented in diagram (b). The circuit is decomposed to find input and output loading. The BJT parameters are given as gm = 1/25 Ω, rπ = 5 kΩ, and ro = 100 kΩ. The resistor RE is 10 kΩ.
image_name:(b)
description:
[
name: i_o/α_0, type: CurrentSource, value: i_o/α_0, ports: {Np: GND, Nn: Vf}
name: RE, type: Resistor, value: RE, ports: {N1: vf, N2: GND}
]
extrainfo:The circuit diagram (b) represents a feedback network with a current source and a voltage source connected to a resistor RE, forming a feedback loop. The current source 'i_o/α_0' flows from ground to the node 'Vf', and the voltage source 'Vf' is connected from 'Vf' to 'OC'. The resistor RE connects the 'OC' node to ground.

FIGURE 7.38 Decomposing the circuit of Fig. 7.37 into (a) the error amplifier and (b) the feedback network.

In the V-I converter of Fig. $7.37 a$ let $R_{E}=10 \mathrm{k} \Omega$. Moreover, let the BJT have $g_{m}=1 /(25 \Omega), r_{\pi}=5 \mathrm{k} \Omega$, and $r_{o}=100 \mathrm{k} \Omega$. Find $R_{i}, R_{o}$, and the unloaded gain $A_{s c}$. Comment on your findings.

#### Solution

With reference to Fig. 7.38a we have, by inspection,

$$
\begin{aligned}
& r_{i a}=r_{\pi}+R_{E}=5+10=15 \mathrm{k} \Omega \quad r_{o a}=r_{o}+R_{E}=100+10=110 \mathrm{k} \Omega \\
& i_{o}=i_{R_{E}}=\frac{r_{o}}{R_{E}+r_{o}} g_{m} v_{\pi}=\frac{r_{o}}{R_{E}+r_{o}} g_{m} \frac{r_{\pi}}{r_{\pi}+R_{E}} v_{\varepsilon}
\end{aligned}
$$

so

$$
a=\frac{i_{o}}{v_{\varepsilon}}=\frac{r_{\pi}}{r_{\pi}+R_{E}} g_{m} \frac{r_{o}}{R_{E}+r_{o}}=\frac{5}{5+10} \times \frac{1}{25} \times \frac{100}{10+100}=\frac{1}{82.5} \mathrm{~A} / \mathrm{V}
$$

Moreover, with reference to Fig. $7.38 b$ we have $v_{f}=R_{E} i_{o} / \alpha_{0}$, so

$$
b=\frac{v_{f}}{i_{o}}=\frac{R_{E}}{\alpha_{0}}=\frac{10,000}{200 / 201}=10,050 \mathrm{~V} / \mathrm{A} \quad L=a b=\frac{10,050}{82.5}=122
$$

Finally,

$$
\begin{aligned}
& A_{s c}=\frac{i_{o}}{v_{i}}=\frac{1}{10,050} \frac{1}{1+1 / 122}=98.7 \mu \mathrm{~A} / \mathrm{V} \\
& R_{i}=15(1+122)=1.85 \mathrm{M} \Omega \quad R_{o}=110(1+122)=13.5 \mathrm{M} \Omega
\end{aligned}
$$

Remark: The student should compare the above (approximate) results with those provided by the exact expressions of Section 2.6, and verify that the differences are reasonably small. Even though the V-I converter of Fig. 7.37a is similar to the emitter follower of Fig. 7.28 and uses the same component values, the loop gains are quite different ( $L=364$ for the emitter follower, $L=122$ for the V-I converter). On the other hand, the series-shunt circuit of Example 7.10 and its shuntshunt counterpart of Example 7.14 have the same value of $L(430)$. It must be said that $L$ generally depends on the feedback topology being used, even if the sourceless circuits are the same. This issue will be taken up again in the next section.

### Shunt-Series Circuits

In Fig. 7.39 we re-examine the shunt-series op amp configuration of Fig. $7.18 d$, but using the full-blown op amp model. Again, we assume the absence of any external loading, meaning zero parallel resistance for the input current source, and a short circuit as the load. With shunt summing, the op amp's input port appears to the feedback network as a short circuit (SC), while with series sensing, the op amp's output port appears to the feedback network as an open circuit (OC). Consequently, we end up with the situation
image_name:FIGURE 7.39
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'X1', 'N2': 'GND'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'X1', 'N2': 'Vf'
'name': 'ri', 'type': 'Resistor', 'value': 'ri', 'ports': {'N1': 'Vf', 'N2': 'GND'
'name': 'ro', 'type': 'Resistor', 'value': 'ro', 'ports': {'N1': 'a_vd', 'N2': 'GND'
'name': 'OpAmp', 'type': 'OpAmp', 'value': 'a_vd', 'ports': {'InP': 'Vf', 'InN': 'GND', 'OutP': 'a_vd', 'OutN': 'GND'
'name': 'ii', 'type': 'CurrentSource', 'ports': {'Np': 'Vf', 'Nn': 'GND'
]
extrainfo:The circuit is a shunt-series op-amp configuration used as a current amplifier. It includes internal resistances ri and ro, with feedback resistors R1 and R2. The input current source ii is connected to the feedback network, and the output is taken across Ro.

FIGURE 7.39 The op amp as a current amplifier with its internal resistances $r_{i}$ and $r_{0}$ explicitly shown.
image_name:(a)
description:
[
name: ig, type: CurrentSource, ports: {Np: GND, Nn: Vf}
name: R2, type: Resistor, value: R2, ports: {N1: Vf, N2: V1}
name: R1, type: Resistor, value: R1, ports: {N1: V1, N2: GND}
name: ro, type: Resistor, value: ro, ports: {N1: a_vd, N2: GND}
name: OpAmp, type: OpAmp, ports: {InP: GND, InN: vf, OutP: a_vd, OutN: GND}
name: R2, type: Resistor, value: R2, ports: {N1: V2, N2: gnd}
name: R1, type: Resistor, value: R1, ports: {N1: V2, N2: GND}
]
extrainfo:The circuit is a shunt-series op-amp configuration used as a current amplifier. It includes internal resistances ri and ro, with feedback resistors R1 and R2. The input current source ii is connected to the feedback network, and the output is taken across Ro.
image_name:(b)
description:
[
name: R2, type: Resistor, ports: {N1: GND, N2: OC}
name: R1, type: Resistor, ports: {N1: OC, N2: GND}
name: io, type: CurrentSource, ports: {Np: GND, Nn: OC}
]
extrainfo:The circuit is a feedback network for a current amplifier configuration. It consists of resistors R1 and R2 and a current source io. The network provides a path for feedback current if, influencing the operation of the amplifier circuit by connecting node SC to OC and then to GND.

FIGURE 7.40 Decomposing the circuit of Fig. 7.39 into (a) the error amplifier and (b) the feedback network.
of Fig. 7.40a, showing the error amplifier in open-loop operation, but with loading by the feedback network specifically taken into account at both ports. Next, we wish to find its open-loop parameters, now denoted as $a, r_{i a}$ and $r_{o a}$. By inspection

$$
\begin{equation*}
r_{i a}=r_{i} / /\left(R_{2}+R_{1}\right) \quad r_{o a}=r_{o}+\left(R_{2} / / R_{1}\right) \tag{7.56}
\end{equation*}
$$

Moreover,

$$
i_{o}=\frac{a_{v} v_{d}}{r_{o a}}=\frac{1}{r_{o a}} a_{v} r_{i a}\left(-i_{\varepsilon}\right)
$$

so that

$$
\begin{equation*}
a=\frac{i_{o}}{i_{\varepsilon}}=-\frac{r_{i a}}{r_{o a}} a_{v} \tag{7.57}
\end{equation*}
$$

Note that $a$ now has the dimensions of $\mathrm{A} / \mathrm{A}$, and it is negative.
Next, we seek a representation for the feedback network that is separate from the basic amplifier. Referring back to Fig. 7.39 we observe that at the sensing side the feedback network is driven by a current source $i_{o}$ expected to exhibit extremely high parallel resistance $R_{o}$, whereas at the summing side it drives the amplifier's input port which, for practical purposes, appears as a short circuit (SC). The circuit for the calculation of $b$ is thus as in Fig. 7.40b. Using the current divider rule, we have

$$
\begin{equation*}
b=\frac{i_{f}}{i_{o}}=-\frac{R_{1}}{R_{1}+R_{2}}=-\frac{1}{1+R_{2} / R_{1}} \tag{7.58}
\end{equation*}
$$

Note that $b$ is negative and is in A/A, just like $a$. As usual, we now apply Eq. (7.31) to find the unloaded gain $A_{s c}$, and Eqs. (7.32) and (7.33), but with $r_{i}$ and $r_{o}$ replaced by $r_{i a}$ and $r_{o a}$, to find the closed-loop terminal resistances $R_{i}$, and $R_{o}$. Moreover, the general case in which a feedback current amplifier is driven by a signal source $i_{s i g}$ with noninfinite
image_name:Figure 7.41
description:
[
name: isig, type: CurrentSource, value: isig, ports: {Np: X1, Nn: X2}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: X1, N2: X2}
name: Ri, type: Resistor, value: Ri, ports: {N1: X2, N2: X1}
name: Ascvi, type: VoltageControlledCurrentSource, value: Ascvi, ports: {Np: X3, Nn: X4}
name: Ro, type: Resistor, value: Ro, ports: {N1: X3, N2: X4}
name: RL, type: Resistor, value: RL, ports: {N1: X4, N2: X3}
]
extrainfo:The circuit is a closed-loop current amplifier with feedback, driven by a current source isig and driving a load RL. It consists of a voltage-controlled current source Ascvi, input resistance Ri, output resistance Ro, and source resistance Rsig.

FIGURE 7.41 Modeling a closed-loop current amplifier driving a load $R_{L}$ and driven by a source having output resistance $R_{\text {sig }}$.
parallel resistance $R_{s i g}$ and drives a nonzero output load $R_{L}$, is readily investigated with reference to the circuit model of Fig. 7.41. Its source-to-load current gain is

$$
\begin{equation*}
\frac{i_{o}}{i_{s i g}}=\frac{R_{s i g}}{R_{s i g}+R_{i}} A_{s c} \frac{R_{o}}{R_{o}+R_{L}} \tag{7.59}
\end{equation*}
$$

EXAMPLE 7.18 (a) In the circuit of Fig. 7.39 let the op amp have $a_{v}=10^{3} \mathrm{~V} / \mathrm{V}, r_{i}=100 \mathrm{k} \Omega$, and $r_{o}=100 \Omega$. If $R_{1}=1.0 \mathrm{k} \Omega$ and $R_{2}=9.0 \mathrm{k} \Omega$, find $R_{i}, R_{o}$, and the unloaded gain $A_{s c}$.
(b) Find the signal-to-load gain $i_{o} / i_{s i g}$ if the feedback amplifier is driven by a signal source $i_{\text {sig }}$ having a parallel resistance $R_{s i g}=1.0 \mathrm{k} \Omega$, and drives a load $R_{L}=1.0 \mathrm{k} \Omega$.

#### Solution

(a) Using Eqs. (7.56) through (7.58) we have

$$
\begin{aligned}
& r_{i a}=100 / /(9.0+1.0)=9.09 \mathrm{k} \Omega \quad r_{o a}=0.1+(9.0 / / 1.0)=1.0 \mathrm{k} \Omega \\
& a=-\frac{9.09}{1.0} 10^{3}=-9,090 \mathrm{~A} / \mathrm{A} \\
& b=-\frac{1}{1+9 / 1}=-0.1 \mathrm{~A} / \mathrm{A} \\
& L=a b=909 \\
& A_{s c} \cong-10\left(1-\frac{1}{909}\right)=-9.989 \mathrm{~A} / \mathrm{A} \\
& R_{i}=\frac{9100}{1+909}=10 \Omega \\
& R_{o}=1(1+909)=910 \mathrm{k} \Omega
\end{aligned}
$$

(b) Refer to the equivalent representation of Fig. 7.41, where we note that we have current division both at the input and at the output. The signal-to-load gain is readily found as

$$
\frac{i_{o}}{i_{s i g}}=\frac{1.0}{1.0+0.010}(-9.989) \frac{910}{910+2.0}=-9.868 \mathrm{~A} / \mathrm{A}
$$

The line of reasoning developed for the above example can be generalized to the following Shunt-Series Procedure:

- To calculate loading at the input of the basic amplifier, open-circuit (OC) the sensing-side port of the feedback network.
- To calculate loading at the output of the basic amplifier, short-circuit (SC) the summing-side port of the feedback network.
- To find $b$, apply a current $i_{o}$ to the sensing-side port of the feedback network, find the short-circuit current $i_{f}$ through the summing-side port of the feedback network, and let $b=i_{f} / i_{o}$.
image_name:Figure 7.42
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: V3, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: V1, N2: V3}
name: R3, type: Resistor, value: R3, ports: {N1: GND, N2: V2}
name: Q1, type: NPN, ports: {C: V2, B: V1, E: GND}
name: Q2, type: NPN, ports: {C: GND, B: V2, E: V3}
name: ii, type: CurrentSource, value: ii, ports: {Np: V1, Nn: GND}
]
extrainfo:The circuit is a shunt-series feedback pair, also known as a current amplifier pair. It consists of two NPN transistors (Q1 and Q2) and several resistors. The feedback network is connected between nodes V1, V2, and V3. The input current source ii provides current to the amplifier, and the output is taken across the resistor Ro.

FIGURE 7.42 Shunt-series feedback pair.

Let us illustrate the procedure using the shunt-series pair of Fig. 7.42, also referred to as a current amplifier pair. Applying the aforementioned Shunt-Series Procedure, we end up with the basic amplifier and feedback network of Fig. 7.43.
image_name:(a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: OC, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: X1, N2: vb1}
name: R3, type: Resistor, value: R3, ports: {N1: vc1, N2: GND}
name: Q1, type: NPN, ports: {C: vc1, B: vb1, E: GND}
name: Q2, type: NPN, ports: {C: ve2, B: vc1, E: GND}
name: ie, type: CurrentSource, ports: {Np: x1, Nn: vb1}
name: R1, type: Resistor, value: R1, ports: {N1: ve2, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: ve2, N2: GND}
]
extrainfo:The circuit diagram (a) consists of a shunt-series feedback pair with a current amplifier. It includes two NPN transistors (Q1 and Q2) and several resistors (R1, R2, R3). The input current source ie provides current to the amplifier. The feedback network is connected between nodes X1 and OC. The output is taken across the resistor Ro.
image_name:(b)
description:
[
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'OC', 'N2': 'GND'
'name': 'io, 'type': 'CurrentSource', 'ports': {'Np': 'GND', 'Nn': 'OC'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'OC', 'N2': 'GND'
]
extrainfo:The circuit diagram (b) shows a simplified feedback network with resistors R1 and R2 connected between nodes OC and SC, and a current source io flowing into node OC. The transistors Q1 and Q2 in diagram (a) are part of an amplifier configuration with feedback.

FIGURE 7.43 Decomposing the circuit of Fig. 7.42 into (a) the error amplifier and (b) the feedback network.

EXAMPLE 7.19 (a) In the shunt-series pair of Fig. 7.42 let $R_{1}=1.0 \mathrm{k} \Omega, R_{2}=3.0 \mathrm{k} \Omega$, and $R_{3}=10 \mathrm{k} \Omega$. Moreover, let the BJTs have $g_{m}=1 /(25 \Omega), r_{\pi}=4.0 \mathrm{k} \Omega$, and $r_{o}=50 \mathrm{k} \Omega$. Find $R_{i}, R_{o}$, and the unloaded gain $A_{s c}$.
(b) Verify your results via PSpice.

#### Solution

(a) We have $\beta_{0}=g_{m} r_{\pi}=4 / 0.025=160$. With reference to Fig. 7.43 we have, by inspection,

$$
\begin{aligned}
& r_{i a}=\left(R_{2}+R_{1}\right) / / r_{\pi 1}=(3.0+1.0) / / 4=2.0 \mathrm{k} \Omega \\
& r_{o a}=\frac{\left(r_{o 1} / / R_{3}\right)+r_{\pi 2}}{\beta_{02}+1}+\left(R_{2} / / R_{1}\right) \cong \frac{(50 / / 10)+4}{161}+(3.0 / / 1.0)=0.827 \mathrm{k} \Omega \\
& \frac{v_{b 1}}{i_{\varepsilon}}=r_{i a}=2.0 \mathrm{k} \Omega \\
& \frac{v_{c 1}}{v_{b 1}}=-g_{m 1}\left\{R_{3} / / r_{o 1} / /\left[r_{\pi 2}+\left(\beta_{02}+1\right)\left(R_{1} / / R_{2}\right)\right]\right\} \\
& =-\frac{10 / / 50 / /[4+161(1.0 / / 3.0)]}{0.025}=-312 \mathrm{~V} / \mathrm{V} \\
& \frac{v_{e 2}}{v_{c 1}}=\frac{1}{1+\frac{\left(R_{3} / / r_{o 2}\right)+r_{\pi 2}}{\left(\beta_{02}+1\right)\left(R_{1} / / R_{2}\right)}}=\frac{1}{1+\frac{10 / / 50+4}{161(1.0 / / 3.0)}}=0.907 \mathrm{~V} / \mathrm{V} \\
& \frac{i_{o}}{V_{e 2}}=\frac{1}{R_{1} / / R_{2}}=\frac{1}{1.0 / / 3.0}=\frac{1}{0.75 \mathrm{k} \Omega} \\
& a=\frac{i_{o}}{i_{\varepsilon}}=\frac{v_{b 1}}{i_{\varepsilon}} \times \frac{v_{c 1}}{v_{b 1}} \times \frac{v_{e 2}}{v_{c 1}} \times \frac{i_{o}}{v_{e 2}}=\frac{(2)(-312)(0.907)}{0.75}=-755 \mathrm{~A} / \mathrm{A} \\
& b=-\frac{1.0}{1.0+3.0}=-\frac{1}{4} \mathrm{~A} / \mathrm{A} \quad L=a b=(-755)(-0.25)=189
\end{aligned}
$$

Finally, the closed-loop parameters are

$$
\begin{aligned}
& A_{s c}=\frac{i_{o}}{i_{i}} \cong \frac{-4}{1+1 / 189}=-3.979 \mathrm{~A} / \mathrm{A} \\
& R_{i}=\frac{2000}{1+189} \cong 10.5 \Omega \\
& R_{o}=0.827(1+189)=157 \mathrm{k} \Omega
\end{aligned}
$$

(b) The PSpice circuit, shown in Fig. 7.44, includes the $0-\mathrm{V}$ dummy source $V_{L}$ to measure the short-circuit load current. After directing PSpice to perform the transfer function (.TF) analysis we get $A_{s c}=-3.980 \mathrm{~A} / \mathrm{A}, R_{i}=9.877 \Omega$ and $R_{o}=167.4 \mathrm{k} \Omega$, all in fair agreement with our calculations above.
image_name:FIGURE 7.44
description:
[
name: ii, type: CurrentSource, value: ii, ports: {Np: V1, Nn: GND}
name: r_pi1, type: Resistor, value: 4 kΩ, ports: {N1: V1, N2: GND}
name: R3, type: Resistor, value: 10 kΩ, ports: {N1: V2, N2: V4}
name: r_o1, type: Resistor, value: 50 kΩ, ports: {N1: V2, N2: GND}
name: r_pi2, type: Resistor, value: 4 kΩ, ports: {N1: V2, N2: V5}
name: R2, type: Resistor, value: 3.0 kΩ, ports: {N1: V2, N2: V3}
name: R1, type: Resistor, value: 1.0 kΩ, ports: {N1: V3, N2: GND}
name: r_o2, type: Resistor, value: 50 kΩ, ports: {N1: V5, N2: GND}
name: G1, type: VoltageControlledCurrentSource, ports: {Np: V1, Nn: V2}
name: G2, type: VoltageControlledCurrentSource, ports: {Np: V4, Nn: V5}
name: VL, type: VoltageSource, value: 0 Vdc, ports: {Np: V4, Nn: V3}
]
extrainfo:The circuit is a PSpice model for verifying a specific example, including current sources, voltage-controlled current sources, and resistors. It uses a dummy voltage source for measuring short-circuit load current.

FIGURE 7.44 PSpice circuit to verify Example 7.19.
GND

If an even higher output resistance is desired, the load can be moved to the collector side, which usually presents a much higher ac resistance than the emitter. This results in the alternative of Fig. 7.45a. Note that the load is now outside the feedback loop; however, the B-E port of $Q_{2}$ is still inside the loop, so the current being regulated is still $Q_{2}$ 's emitter current $i_{e 2}$. This current is related to the load current as $i_{e 2}=i_{o} / \alpha_{0}$. Moreover, as depicted in Fig. 7.45b, negative feedback in effect places in series with $Q_{2}$ 's emitter a resistance equal to that found in connection with Fig. 7.42, namely, $r_{o a}(1+L)$.
image_name:(a)
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'V3', 'N2': 'GND'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'V1', 'N2': 'V3'
'name': 'R3', 'type': 'Resistor', 'value': 'R3', 'ports': {'N1': 'V2', 'N2': 'GND'
'name': 'Q1', 'type': 'NPN', 'ports': {'C': 'V2', 'B': 'V1', 'E': 'GND'
'name': 'Q2', 'type': 'NPN', 'ports': {'C': 'GND', 'B': 'V2', 'E': 'V3'
'name': 'ii', 'type': 'CurrentSource', 'ports': {'Np': 'GND', 'Nn': 'V1'
]
extrainfo:The circuit is a shunt-series feedback amplifier with the load in series with Q2's collector. The feedback is applied to the base of Q1, which controls the emitter current ie2 of Q2. The output current io is regulated and related to ie2 by the factor 1/alpha0.
image_name:(b)
description:
[
'name': 'Q2', 'type': 'NPN', 'ports': {'C': 'GND', 'B': 'GND', 'E': 'e1'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'e1', 'N2': 'GND'
]
extrainfo:The circuit diagram (b) is an equivalent circuit for finding the output current (io) and output resistance (Ro) with a feedback network. Transistor Q2 is used to regulate the current with a negative feedback loop involving a resistance roa(1+L). The diagram shows the relationship between the emitter current of Q2 and the load current.

FIGURE 7.45 (a) Shunt-series feedback pair with the load in series with $Q_{2}$ 's collector. (b) Equivalent circuit for finding $i_{0}$ and $R_{0}$.

EXAMPLE 7.20 Assuming the same parameters of Example 7.19, along with $r_{\mu}=\infty$, find the unloaded gain $i_{o} / i_{i}$ as well as $R_{o}$ for the circuit of Fig. 7.45a. Hence, verify via PSpice.

#### Solution

We now have $i_{o}=\alpha_{0}(-3.979) i_{i}$, or

$$
\begin{aligned}
& \frac{i_{o}}{i_{i}}=\frac{160}{161}(-3.979)=-3.954 \mathrm{~A} / \mathrm{A} \\
& R_{o} \cong r_{o 2}\left[1+g_{m 2}\left\{r_{\pi 2} / /\left[r_{o a}(1+L)\right]\right\}\right]=50 \times 10^{3} \times[1+(4 / / 157) / 0.025] \cong 7.8 \mathrm{M} \Omega
\end{aligned}
$$

To verify with PSpice we still use the circuit of Fig. 7.44, but with the currentsensing source $V_{L}$ now in series with the collector. This gives $i_{o} / i_{i}=-3.955 \mathrm{~A} / \mathrm{A}$, $R_{i}=9.877 \Omega$, and $R_{o}=7.5 \mathrm{M} \Omega$, again in good agreement with the calculations.

### Finding the Source-to-Load Gain Directly

As illustrated in Figs. 7.22 and 7.41, once we know $R_{i}, R_{o}$, and the unloaded gain $A_{o c}$ or $A_{s c}$, we can find the signal-to-source gain for the case of a non-ideal driving source and an arbitrary output load. However, the need often arises to find the signal-to-load gain directly, without having to go through the intermediate calculations of $R_{i}$ and $R_{o}$. This is achieved by including also the signal source resistance $R_{\text {sig }}$ and the load resistance $R_{L}$ in the circuit of the basic amplifier when calculating its open-loop gain $a$. Then, the source-to-load gain is simply $A=a /(1+a b)$. We shall demonstrate for the cases of voltage and current amplifiers, but the technique is applicable also to the other two amplifier types.

#### EXAMPLE 7.21

Use direct calculation to find the signal-to-load gain $A=v_{o} / v_{\text {sig }}$ of Example 7.9b, for which $a_{v}=1000 \mathrm{~V} / \mathrm{V}, r_{i}=10 \mathrm{k} \Omega, r_{o}=1.0 \mathrm{k} \Omega, R_{1}=1.0 \mathrm{k} \Omega, R_{2}=9.0 \mathrm{k} \Omega$, $R_{s i g}=20 \mathrm{k} \Omega$, and $R_{L}=2.0 \mathrm{k} \Omega$.
image_name:FIGURE 7.46
description:
[
name: Ve, type: VoltageSource, value: Ve, ports: {Np: Ve, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Ve, N2: V1}
name: ri, type: Resistor, value: ri, ports: {N1: V1, N2: vf}
name: R1, type: Resistor, value: R1, ports: {N1: Vf, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vf, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
name: OpAmp, type: OpAmp, ports: {InP: V1, InN: GND, OutP: Vo}
name: R1, type: Resistor, value: R1, ports: {N1: OC, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: vo, N2: OC}
]
extrainfo:The circuit is a voltage amplifier with external loading resistors Rsig and RL. It includes an operational amplifier with gain av and internal resistances ri and ro, configured for voltage amplification.

FIGURE $\mathbf{7 . 4 6}$ Modifying the basic voltage amplifier of
Fig. 7.21a to account for external loading due to $R_{\text {sig }}$ and $R_{L}$.

#### Solution

Redraw the circuit of Fig. 7.21a, but with $R_{s i g}$ and $R_{L}$ also included. This results in the circuit of Fig. 7.46, where we note that $R_{s i g}$ appears in series and $R_{L}$ in shunt, in accordance with the present topology type. Thus, Eq. (7.46) changes to

$$
\begin{aligned}
& a=\frac{v_{o}}{v_{\varepsilon}}=\frac{r_{i}}{R_{s i g}+r_{i}+\left(R_{1} / / R_{2}\right)} a_{v} \frac{\left(R_{1}+R_{2}\right) / / R_{L}}{r_{o}+\left[\left(R_{1}+R_{2}\right) / / R_{L}\right]} \\
& \text { or } \\
& \begin{aligned}
a & =\frac{10}{20+10+(1.0 / / 9.0)} 1000 \frac{(1.0+9.0) / / 2.0}{1+[(1.0+9.0) / 2.0]} \\
& =0.324 \times 1000 \times 0.625=202 \mathrm{~V} / \mathrm{V}
\end{aligned}
\end{aligned}
$$

By Eq. (7.48) we still have $b=0.1 \mathrm{~V} / \mathrm{V}$, so $L=202 \times 0.1=20.2$ and

$$
\frac{v_{o}}{v_{s i g}}=\frac{1 / b}{1+1 / L}=\frac{10}{1+1 / 20.2}=9.528 \mathrm{~V} / \mathrm{V}
$$

in reasonable agreement with the result of Example 7.9b.

Use direct calculation to find the signal-to-load gain $A=i_{o} / i_{s i g}$ of the circuit of
EXAMPLE 7.22 Example 7.18b.

#### Solution

Redraw the circuit of Fig. 7.40a, but with $R_{s i g}$ and $R_{L}$ also included. The result is shown in Fig. 7.47, where we note that $R_{s i g}$ appears in shunt and $R_{L}$ in series, in accordance with the present feedback topology. Thus, Eq. (7.57) changes to

$$
a=\frac{i_{o}}{i_{\varepsilon}}=-\frac{R_{s i g} / / r_{i} / /\left(R_{1}+R_{2}\right)}{r_{o}+R_{L}+\left(R_{1} / / R_{2}\right)} a_{v}=-\frac{1.0 / / 100 / /(1.0+9.0)}{1.0+2.0+(1.0 / / 9.0)} 10^{3}=-231 \mathrm{~A} / \mathrm{A}
$$

With $b$ still given as in Eq. (7.58), or $b=-0.1 \mathrm{~A} / \mathrm{A}$, we get

$$
\frac{i_{o}}{i_{s i g}}=\frac{a}{1+a b}=\frac{-231}{1+(-231)(-0.1)}=-9.585 \mathrm{~A} / \mathrm{A}
$$

in reasonable agreement with the result of Example 7.18b.
image_name:FIGURE 7.47
description:
[
name: Rsig, type: Resistor, value: Rsig, ports: {N1: -Vd, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: -Vd, N2: X1}
name: R1, type: Resistor, value: R1, ports: {N1: X1, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: X2, N2: vo1}
name: ie, type: CurrentSource, value: ie, ports: {Np: -Vd, Nn: GND}
name: Av Vd, type: OpAmp, value: Av Vd, ports: {InP: -Vd, InN: GND, OutP: X2, OutN: GND}
name: R2, type: Resistor, value: R2, ports: {N1: x2, N2: GND}
name: R1, type: Resistor, value: R1, ports: {N1: X2, N2: GND}
]
extrainfo:The circuit is a modified current amplifier with external loading due to Rsig and RL. It uses an op-amp with feedback to control the output current io.

FIGURE 7.47 Modifying the basic current amplifier of
Fig. 7.40a to account for external loading due to $R_{\text {sig }}$ and $R_{L}$.

### Identifying Feedback Type and Topology

The analytical tools developed so far can be applied to any feedback circuit provided feedback is itself negative. To assess feedback polarity, apply a stimulus $s_{i}$ at the input, follow its effect around the loop, and determine whether the returned signal $s_{f}$ opposes or reinforces $s_{i}$. Only if it opposes is feedback negative. The procedure is readily visualized via signal "bumps" as exemplified in Fig. 7.48.

In Fig. 7.48a we have frozen the ac input $v_{i}$ during a positive alternation, signified by a positive bump. This bump is amplified and inverted by $Q_{1}$ and then by $Q_{2}$, and is finally buffered by $Q_{4}$ back to the input port via the voltage divider $R_{2}-R_{1}$. With two inversions, the returned $v_{f}$ bump has the same polarity as the original $v_{i}$ bump. Since $Q_{1}$ responds to the difference $v_{i}-v_{f}$, it is apparent that $v_{f}$ tends to neutralize the effect of $v_{i}$, so feedback is negative. Had $R_{2}$ been returned to $Q_{1}$ 's base instead of the emitter, $v_{f}$ would have reinforced $v_{i}$, so feedback would have been positive.

In Fig. $7.48 b$ a positive current bump in $i_{i}$ is converted by $Q_{1}$ to a negative voltage bump at the collector, which is then buffered by $Q_{2}$ back to $Q_{1}$ 's base via $R_{2}$. With a negative bump at its right side, $R_{2}$ will sink current away from to $Q_{1}$ 's base. Since $Q_{1}$ responds to the difference $i_{i}-i_{f}$, it is apparent that $i_{f}$ tends to neutralize the effect of $i_{i}$, so feedback is negative. Had we inserted an additional inverting stage between $Q_{1}$ and $Q_{2}$ in the manner of Fig. 7.48a, the direction of $i_{f}$ would have been reversed, causing $i_{f}$ to reinforce $i_{i}$, so feedback would have been positive.

To identify the feedback topology we must determine the type of signal sensing at the output as well as the type of signal summing at the input. To identify the type of output sensing, proceed like this:

- To test for voltage sensing, set $v_{o} \rightarrow 0$ by short-circuiting the output port. Then, if the signal returned to the input port also drops to zero, sensing is of the shunt type.
- To test for current sensing, set $i_{o} \rightarrow 0$ by open-circuiting the output port. Then, if the signal returned to the input port also drops to zero, sensing is of the series type.

As an example, short-circuiting the output port in Fig. 7.48a yields $v_{f} \rightarrow 0$, confirming voltage feedback. Conversely, open-circuiting the output port in Fig. $7.48 b$ yields
image_name:(a)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: vi, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: GND, N2: vf}
name: R2, type: Resistor, value: R2, ports: {N1: vf, N2: vo}
name: R3, type: Resistor, value: R3, ports: {N1: vo, N2: GND}
name: R4, type: Resistor, value: R4, ports: {N1: v2, N2: GND}
name: R5, type: Resistor, value: R5, ports: {N1: v3, N2: GND}
name: Q1, type: NPN, ports: {C: v2, B: vi, E: vf}
name: Q2, type: NPN, ports: {C: v3, B: v2, E: GND}
name: Q3, type: NPN, ports: {C: GND, B: v3, E: vo}
]
extrainfo:The circuit diagram (a) is a feedback amplifier with three NPN transistors (Q1, Q2, Q3) and five resistors (R1, R2, R3, R4, R5). The input voltage source Vi is connected to the base of Q1, and the output is taken across R2. The circuit is designed for voltage feedback analysis.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: V2, B: V1, E: GND}
name: Q2, type: NPN, ports: {C: V2, B: X1, E: GND}
name: R1, type: Resistor, value: R1, ports: {N1: X1, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: X1, N2: V1}
name: R3, type: Resistor, value: R3, ports: {N1: V2, N2: GND}
name: i_i, type: CurrentSource, ports: {Np: GND, Nn: i_i}
]
extrainfo:The circuit diagram (b) features two NPN transistors Q1 and Q2, three resistors R1, R2, and R3, a voltage source Vi, and two current sources V1 and i_i. The circuit implements a feedback mechanism with current sensing and summing. The base of Q1 is connected to node V2, and its collector is connected to node V1. Q2's base is connected to node X1, and its collector is connected to node V2. The feedback current if flows into node V1.

FIGURE 7.48 Using voltage "bumps" to investigate signal propagation around the feedback loop of (a) the series-shunt triple and (b) the shunt-series pair studied above.
$i_{f} \rightarrow 0$, confirming current feedback. In general one would apply both tests, one to identify and the other to corroborate.

To identify the type of input summing, proceed as follows:

- To test for voltage summing, look for an input mesh comprising the series combination of the input voltage, the voltage controlling the amplifier, and the voltage fed back from that across the output load. If such a mesh can be found, then summing is of the series type. If this test fails, then test for current summing.
- To test for current summing, look for an input node comprising the shunt combination of the input current, the current controlling the amplifier, and the current fed back from that through the output load. If such a node can be found, then summing is of the shunt type. If this test fails, then test for voltage summing.
In Fig. $7.48 a$ we identify a mesh comprising the series combination of $v_{i}, v_{\varepsilon}$, and $v_{f}$, indicating series summing. In Fig. $7.48 b$ we identify a node comprising $i_{i}, i_{s}$, and $i_{f}$, indicating shunt summing. No such node is present in Fig. 7.48a, just as no mesh counterpart is present in Fig. 7.48b.

It also helps exercising intuition to anticipate the expected resistance level: a high resistance implies series type, and a low resistance implies shunt type. The student is urged to apply the sensing and summing tests to all circuits investigated so far. With enough practice, you will soon be able to identify a topology by mere inspection!

## 7.5 RETURN-RATIO ANALYSIS

There is no doubt that the loop gain plays a central role in a negative-feedback system. Since it gives a measure of how close circuit behavior comes to ideal, the designer often needs to come up with a quick estimate for this gain to see whether the circuit under development meets the design specifications or needs improvement. Two-port techniques require that we find $a$ and $b$ separately via suitable circuit manipulations and approximations, and then estimate the loop gain as $L=a b$ (as seen in the previous section, both $a$ and $b$ vary with the feedback topology in use). Unlike two-port methods, direct methods are based on the idea of injecting a stimulus into the feedback loop and then observing the system's response to find the overall loop characteristics (as such, they are topology independent). As we inject a stimulus we must be careful ( $a$ ) not to upset the existing dc bias conditions and (b) not to alter the local loading conditions. Two techniques are available for the direct estimation of the feedback loop characteristics. The first method, discussed in the present section, is suited to hand calculations on circuit schematics involving dependent sources. The second method, discussed in the next section, is suited to test and measurement environments such as lab measurements or transistor-level computer simulations.

### The Return Ratio of a Dependent Source

Given a dependent source inside a single-loop feedback circuit, we find its return ratio as follows:

- Set the external driving source $s_{i}$ to zero, that is, replace $s_{i}$ with a short circuit if it is a voltage source, or with an open circuit if it is a current source.
image_name:(a)
description:The circuit diagram (a) shows a feedback loop with a voltage-controlled voltage source (Vr) and a test voltage source (Vt). The feedback loop is designed to analyze the return ratio of the dependent voltage source.
image_name:(b)
description:The circuit diagram (b) demonstrates a feedback loop with a current-controlled current source and a test current source. The dependent source is short-circuited as per the method for finding the return ratio.

FIGURE 7.49 Finding the return ratio $T$ of a dependent source of the (a) voltage type and (b) current type.

- Break the feedback loop right downstream of the dependent source, and leave this source open-circuited if it is of the voltage type, or short-circuited it if it is of the current type.
- If the dependent source is of the voltage type, drive the circuit downstream with a test voltage $v_{t}$ having the same polarity as the dependent source (see Fig. 7.49a). Hence, find the open-circuit voltage $v_{r}$ returned by the dependent source, and obtain the source's return ratio, denoted as $T$, as

$$
\begin{equation*}
T=-\frac{v_{r}}{v_{t}} \tag{7.60a}
\end{equation*}
$$

- If the dependent source is of the current type, drive the circuit downstream with a test current $i_{t}$ having the same direction as the dependent source (see Fig. 7.49b). Hence, find the short-circuit current $i_{r}$ returned by the dependent source, and obtain the source's return ratio as

$$
\begin{equation*}
T=-\frac{i_{r}}{i_{t}} \tag{7.60b}
\end{equation*}
$$

### Comparing $T$ and $L$

Intuitively, it would seem that $T$ is the same as $L$ (in fact, it is common practice to refer also to $T$ as the loop gain, further adding to the confusion.) Though they may coincide in some some cases, $T$ and $L$ are generally different (when necessary to distinguish between the two, we shall refer to $T$ as the return-ratio loop gain, and to $L$ as the two-port loop gain). To understand the difference, recall that $L$ as defined in Eq. (7.6) is predicated on two premises, namely,

- Forward signal transmission occurs exclusively through the amplifier (in Fig. 7.1 we signify this by representing the amplifier with an arrowhead in the forward direction)
- Reverse signal transmission occurs exclusively through the feedback network (in Fig. 7.1 we signify this by representing the feedback network with an arrowhead in the reverse direction)

When this is the case, the amplifier and feedback network are said to be unilateral. However, most real-life feedback networks are bilateral. Add to this the fact that in the two-port approach we use short-circuit (SC) and open-circuit (OC) approximations to expedite the calculation of $a$ and $b$, and we have additional reasons for possible differences between $T$ and $L$. At this juncture it must be stressed that the calculation of $T$ does not predicate any premises and thus yields exact results.

We can better appreciate the similarities and differences between $T$ and $L$ by examining the manner in which each intervenes in the expression for the closed-loop gain $A$. Let the gain of the dependent source in question be denoted as $k$ (for instance, $k=a_{v}$ for an op amp, $k=\beta_{0}$ for a BJT, $k=g_{m}$ for a FET or a BJT, $k=z$ for a CFA). As we know, the closed-loop gain $A$ is related to the loop gain $L$ as

$$
\begin{equation*}
A=\frac{s_{o}}{s_{i}}=\frac{A_{\text {ideal }}}{1+1 / L} \tag{7.61}
\end{equation*}
$$

where

$$
\begin{equation*}
A_{\text {ideal }}=\lim _{k \rightarrow \infty} \frac{s_{o}}{s_{i}} \tag{7.62}
\end{equation*}
$$

is the value of $A$ in the idealized limit of the dependent source having infinite gain. We visualize Eq. (7.61) via the familiar block diagram of Fig. 7.50a, which has been derived from Fig. 7.1 by letting $b \rightarrow 1 / A_{\text {ideal }}$ and $a \rightarrow a b / b=L / b=L A_{\text {ideal }}$. As we know, a signal starting at the error amplifier's input and going around the loop clockwise undergoes an overall amplification of $\left(L A_{\text {ideal }}\right) \times\left(1 / A_{\text {ideal }}\right) \times(-1)$, or $-L$.

By contrast, the dependence of the closed-loop gain $A$ upon the return ratio $T$ takes on the form ${ }^{1,4}$

$$
\begin{equation*}
A=\frac{s_{o}}{s_{i}}=\frac{A_{\text {ideal }}}{1+1 / T}+\frac{a_{\mathrm{ft}}}{1+T} \tag{7.63}
\end{equation*}
$$

image_name:(a)
description:The block diagram labeled (a) represents a feedback control system illustrating the role of loop gain, denoted as \( L \).

Main Components:
1. **Summing Junction (\( \Sigma \))**:
- Positioned at the input, this block combines the input signal \( s_i \) and the feedback signal.
- It has two inputs: the input signal \( s_i \) (positive) and the feedback signal (negative).

2. **Amplifier \( LA_{\text{ideal}} \)**:
- This block represents the loop gain \( L \) multiplied by the ideal amplifier gain \( A_{\text{ideal}} \).
- It amplifies the error signal from the summing junction.

3. **Amplifier \( 1/A_{\text{ideal}} \)**:
- Represents the inverse of the ideal amplifier gain.
- It attenuates the output signal, providing the feedback path.

Flow of Information or Control:
- The input signal \( s_i \) enters the summing junction, where it is combined with the feedback signal.
- The resulting error signal is amplified by the \( LA_{\text{ideal}} \) block.
- The amplified signal is output as \( s_o \), which is also fed back through the \( 1/A_{\text{ideal}} \) block.
- The feedback signal is then fed back into the summing junction to complete the loop.

Labels, Annotations, and Key Indicators:
- **\( s_i \)**: Input signal.
- **\( s_o \)**: Output signal.
- **\( LA_{\text{ideal}} \)**: Loop gain with ideal amplification.
- **\( 1/A_{\text{ideal}} \)**: Inverse of the ideal amplifier gain, part of the feedback path.

Overall System Function:
The primary function of this system is to illustrate the concept of loop gain \( L \) in a feedback control system. The loop gain determines the extent to which the feedback affects the overall gain of the system. The arrangement allows for the stabilization and control of the output signal \( s_o \) by adjusting the feedback based on the loop gain \( L \). This configuration is crucial for maintaining desired performance characteristics in various control systems.
image_name:(b)
description:The block diagram labeled (b) represents a system that illustrates the roles of the return ratio \( T \) in a feedback control system. This diagram is a more generalized form compared to diagram (a) and includes additional components to show the impact of feedthrough gain.

Main Components:
1. **Summing Junction (Σ):**
- Located at the input, it combines the input signal \( s_i \) with the feedback signal. It has both positive and negative inputs.
- Another summing junction is present at the output to combine signals.

2. **Amplifiers:**
- **\( TA_{\text{ideal}} \):** This block represents the ideal transfer function of the system affected by the return ratio \( T \).
- **\( 1/A_{\text{ideal}} \):** This block represents the inverse of the ideal amplifier gain, used in the feedback path.
- **\( a_{\text{ft}} \):** This block represents the feedthrough gain, which accounts for forward transmission around the dependent source.

3. **Feedback Loop:**
- The feedback loop takes the output \( s_o \) and feeds it back through the \( 1/A_{\text{ideal}} \) block to the summing junction at the input.

Flow of Information or Control:
- The input signal \( s_i \) enters the system and is combined with the feedback signal at the first summing junction.
- The combined signal is then amplified by the \( TA_{\text{ideal}} \) block.
- Simultaneously, the feedthrough gain \( a_{\text{ft}} \) affects the signal and contributes to the final output at the second summing junction.
- The output \( s_o \) is partially fed back into the system through the \( 1/A_{\text{ideal}} \) block, completing the feedback loop.

Labels, Annotations, and Key Indicators:
- The blocks are labeled with their respective functions: \( TA_{\text{ideal}} \), \( 1/A_{\text{ideal}} \), and \( a_{\text{ft}} \).
- The summing junctions are marked with plus and minus signs indicating the addition and subtraction of signals.

Overall System Function:
The primary function of this system is to demonstrate how the return ratio \( T \) and feedthrough gain \( a_{\text{ft}} \) affect the closed-loop gain of the system. The arrangement of blocks and the flow of signals illustrate the balance between amplification and feedback, showing how the system can maintain stability and control over its output through these parameters. The feedthrough gain provides an additional path for signal transmission, which is accounted for in the overall system dynamics.

FIGURE 7.50 Block diagrams illustrating the roles of (a) the loop gain $L$, and (b) the return ratio $T$.
where

$$
\begin{equation*}
a_{\mathrm{ft}}=\lim _{k \rightarrow 0} \frac{s_{o}}{s_{i}} \tag{7.64}
\end{equation*}
$$

is the feedthrough gain, that is, the gain with the dependent source set to zero. This gain stems from forward transmission around the dependent source. We visualize Eq. (7.63) via the block diagram of Fig. 7.50b, which is a generalization of that of Fig. $7.50 a$ because it includes also the feedthrough path shown at the top.

Compared to two-port analysis, return-ratio analysis is more insightful as it splits $A$ into two separate components, both stemming from forward transmission, but one through the error amplifier and the other through the feedback network. Two-port analysis, on the other hand, attempts at making the entire feedback system conform to the simpler diagram of Fig. 7.50a, this being the reason why it gives only approximate results compared to the exact results of the return-ratio method. ${ }^{1,4} \mathrm{It}$ is apparent from Eq. (7.63) that if the condition

$$
\begin{equation*}
\left|a_{\mathrm{ft}}\right| \ll\left|T A_{\text {ideal }}\right| \tag{7.65}
\end{equation*}
$$

is met, the feedthrough component of $A$ in Eq. (7.63) can be ignored, implying that Eq. (7.63) becomes formally identical to Eq. (7.61). Even so, $T$ and $L$ may still differ from each other due to the approximations at the basis of $L$. As such, $T$ and $L$ tend to provide different values for $A$, though this difference may be very small for large $T$ and $L$.

As an alternative viewpoint, we can regard the signal component $a_{\mathrm{ft}} s_{i}$ that manages to creep to the output as a form of output noise. Reflected to the input, this noise gets divided by the gain $T A_{\text {ideal }}$, thus resulting in the equivalent input noise component $s_{n i}=a_{\mathrm{ft}} s_{i} /\left(T A_{\text {ideal }}\right)$. It is clear that as long as Eq. (7.65) is met, then $\left|s_{n i}\right| \ll\left|s_{i}\right|$, so the fact that the feedback network is not unilateral is of little consequence in this case.

### Return-Ratio Calculation Examples

The above concepts are best illustrated via practical examples. Let us start with the familiar op amp circuit of Fig. 7.51, now shown in a more general setting that includes loading both at the input $\left(R_{s i g}\right)$ and at the output $\left(R_{L}\right)$. To find $T$, suppress $v_{s i g}$ by grounding it, break the loop right at the source $a_{v} v_{d}$ and leave the latter open-circuited, inject a test source $v_{t}$, positive at the top, into the circuit downstream, and calculate the return voltage $v_{r}$. With reference to Fig. $7.52 a$, we start out at the left and work our way toward the right via repeated application of the voltage divider rule to obtain

$$
v_{r}=a_{v} v_{d}=a_{v} \frac{-r_{i}}{R_{s i g}+r_{i}} \times \frac{\left(R_{s i g}+r_{i}\right) / / R_{1}}{\left[\left(R_{s i g}+r_{i}\right) / / R_{1}\right]+R_{2}} \times \frac{\left\{\left[\left(R_{s i g}+r_{i}\right) / / R_{1}\right]+R_{2}\right\} / / R_{L}}{\left(\left\{\left[\left(R_{s i g}+r_{i}\right) / / R_{1}\right]+R_{2}\right\} / / / R_{L}\right)+r_{o}} v_{t}
$$

After minor algebra we get

$$
\begin{equation*}
T=-\frac{v_{r}}{v_{t}}=a_{v} \times \frac{1}{1+\frac{R_{s i g}}{r_{i}}} \times \frac{1}{1+\frac{R_{2}}{\left(R_{s i g}+r_{i}\right) / / R_{1}}} \times \frac{1}{1+\frac{r_{o}}{\left\{\left[\left(R_{s i g}+r_{i}\right) / / R_{1}\right]+R_{2}\right\} / / R_{L}}} \tag{7.66}
\end{equation*}
$$

image_name:FIGURE 7.51
description:
[
name: Vsig, type: VoltageSource, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: V1}
name: Ri, type: Resistor, value: Ri, ports: {N1: V1, N2: GND}
name: R1, type: Resistor, value: R1, ports: {N1: V2, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: V2, N2: Vo}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
name: AvVd, type: VoltageControlledVoltageSource, ports: {Np: Vo, Nn: GND}
name: Ro, type: Resistor, value: Ro, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a non-inverting operational amplifier with input and output loading. It includes a voltage source Vsig, input resistors Rsig and Ri, feedback resistors R1 and R2, load resistor RL, and a voltage-controlled voltage source AvVd representing the op-amp.

FIGURE 7.51 Non-inverting op amp with input and output loading.

To find $a_{\mathrm{ft}}$, let $a_{v} \rightarrow 0$, so that the dependent-source side of $r_{o}$ goes to 0 V , or ground. This gives us the situation of Fig. 7.52b. Starting out at the right, and applying the voltage divider rule twice, we get

$$
v_{o}=\frac{r_{o} / / R_{L}}{R_{2}+\left(r_{o} / / R_{L}\right)} \times \frac{R_{1} / /\left[R_{2}+\left(r_{o} / / R_{L}\right)\right]}{R_{s i g}+r_{i}+\left\{R_{1} / /\left[R_{2}+\left(r_{o} / / R_{L}\right)\right]\right\}} v_{s i g}
$$

or

$$
\begin{equation*}
a_{\mathrm{ft}}=\lim _{a_{\imath} \rightarrow 0} \frac{v_{o}}{v_{s i g}}=\frac{1}{1+\frac{R_{2}}{r_{o} / / R_{L}}} \times \frac{1}{1+\frac{R_{s i g}+r_{i}}{R_{1} / /\left[R_{2}+\left(r_{o} / / R_{L}\right)\right]}} \tag{7.67}
\end{equation*}
$$

image_name:(a)
description:
[
name: Rsig, type: Resistor, value: Rsig, ports: {N1: vx, N2: GND}
name: ri, type: Resistor, value: ri, ports: {N1: vx, N2: vf}
name: ro, type: Resistor, value: ro, ports: {N1: vo, N2: vt}
name: RL, type: Resistor, value: RL, ports: {N1: vo, N2: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vf, N2: GND}
name: vt, type: VoltageSource, value: vt, ports: {Np: vx, Nn: GND}
name: a_vd, type: VoltageControlledVoltageSource, value: a_vd, ports: {Np: vd, Nn: GND}
]
extrainfo:The circuit is an op-amp configuration with feedback, consisting of resistors and dependent sources. It is used to analyze the return ratio and forward transmission in the op-amp circuit. The circuit includes a voltage-controlled voltage source and a test voltage source for analysis.

(a)
image_name:(b)
description:
[
name: Vsig, type: VoltageSource, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: X1}
name: ri, type: Resistor, value: ri, ports: {N1: X1, N2: X2}
name: R1, type: Resistor, value: R1, ports: {N1: X2, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: X2, N2: vo}
name: ro, type: Resistor, value: ro, ports: {N1: vo, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: vo, N2: GND}
]
extrainfo:The circuit is an op-amp configuration with feedback, used to analyze the return ratio and forward transmission. It includes a voltage-controlled voltage source and a test voltage source for analysis. The resistors are connected in a series-parallel configuration to achieve the desired feedback and transmission characteristics.

FIGURE 7.52 Modifying the circuit of Fig. 7.51 to find (a) its return ratio $T$, and (b) the forward transmission $a_{\mathrm{ft}}$ around the dependent source.

Use return-ratio analysis to find the signal-to-load gain $A=v_{o} / v_{\text {sig }}$ of the (mediocre) op amp circuit of Example 7.21, for which $a_{v}=1000 \mathrm{~V} / \mathrm{V}, r_{i}=10 \mathrm{k} \Omega, r_{o}=$ $1.0 \mathrm{k} \Omega, R_{1}=1.0 \mathrm{k} \Omega, R_{2}=9.0 \mathrm{k} \Omega, R_{s i g}=20 \mathrm{k} \Omega$, and $R_{L}=2.0 \mathrm{k} \Omega$. Compare with Example 7.21 and comment.

#### Solution

Using Eqs. (7.66) and (7.67), we get
and

$$
\begin{aligned}
T= & 10^{3} \times \frac{1}{1+\frac{20}{10}} \times \frac{1}{1+\frac{9.0}{(20+10) / / 1.0}} \\
& \times \frac{1}{1+\frac{1.0}{\{[(20+10) / / 1.0]+9.0\} / / 2.0}}=10^{3} \times \frac{1}{3} \times \frac{1}{10.3} \times \frac{1}{1.6}=20.2
\end{aligned}
$$

$$
\begin{aligned}
a_{\mathrm{ft}} & =\frac{1}{1+\frac{9.0}{1.0 / / 2.0}} \times \frac{1}{1+\frac{20+10}{1.0 / /[9.0+(1.0 / / 2.0)]}} \\
& =\frac{1}{14.5} \times \frac{1}{34.1}=2.02 \times 10^{-3} \mathrm{~V} / \mathrm{V}
\end{aligned}
$$

Also, we know from basic op amp theory that in the limit $a_{v} \rightarrow \infty$ we have $A_{\text {ideal }}=$ $1+R_{2} / R_{2}=1+9.0 / 1.0=10 \mathrm{~V} / \mathrm{V}$, so Eq. (7.63) gives

$$
A=\frac{10}{1+1 / 20.2}+\frac{2.02 \times 10^{-3}}{1+20.2}=9.528+0.000095 \cong 9.528 \mathrm{~V} / \mathrm{V}
$$

The value of $T$ found here matches the value of $L$ of Example 7.21, so the effect of feedthrough is truly negligible in this example. Indeed, the numerical decomposition of $A$ reveals that the term due to $a_{\mathrm{ft}}$ accounts for only $0.001 \%$ of the overall gain $A$. Alternatively, the fact that $T A_{\text {ideal }}=20.2 \times 10=202 \mathrm{~V} / \mathrm{V}$ and $a_{\mathrm{ft}}=$ $2.02 \times 100^{-3}$ indicates that Eq. (7.65) is met abundantly.

Remark \#1: Looking at the circuit of Fig. $7.52 b$ we observe that if the op amp had $r_{o}=0$, then none of $v_{s i g}$ would be transmitted to $v_{o}$, so we would have $a_{\mathrm{ft}}=0$, as also confirmed by Eq. (7.67). The feedback network would be unilateral in this case.

Remark \#2: To gain additional insight, consider the limiting case $a_{v} \rightarrow 0$, which by Eq. (7.19) occurs for $f \rightarrow \infty$. With $a_{v} \rightarrow 0$ the loop is interrupted, giving $L=$ $T=0$. Then, Eq. (7.61) predicts $A=0$ and thus $v_{o}=A v_{s i g}=0$. On the other hand, Eq. (7.63) predicts $v_{o}=a_{\mathrm{ft}} v_{s i g}=\left(2.02 \times 10^{-3}\right) v_{s i g} \neq 0$. As we know, the latter is correct whereas the former is not.

Next, let us re-examine the feedback-bias BJT circuit of Fig. 7.53, but using return-ratio analysis.

To find $T$, refer to the ac equivalent of Fig. 7.54a, where the loop has been broken right at the upper terminal of the dependent source, which must be short-circuited in
image_name:FIGURE 7.53
description:
[
name: RC, type: Resistor, value: RC, ports: {N1: vo, N2: GND}
name: RB, type: Resistor, value: RB, ports: {N1: VI, N2: vo}
name: ii, type: CurrentSource, value: ii, ports: {Np: GND, Nn: VI}
name: Q1, type: NPN, ports: {C: vo, B: VI, E: GND}
]
extrainfo:This circuit is a feedback-bias BJT configuration with an NPN transistor. It includes a resistor RC connected to the collector, a resistor RB connected to the base, and a current source ii providing input current.

FIGURE 7.53 The feedback-
bias BJT configuration.
order to provide a path for its current to flow. Next, subject the rest of the circuit to a test source $i_{t}$ flowing downward like the dependent source. Using the voltage divider rule and Ohm's law we get

$$
i_{r}=g_{m} v_{\pi}=g_{m} \frac{r_{\pi}}{r_{\pi}+R_{B}} v_{o}=g_{m} \frac{r_{\pi}}{r_{\pi}+R_{B}}\left[\left(R_{B}+r_{\pi}\right) / / R_{C} / / r_{o}\right]\left(-i_{t}\right)
$$

Letting $g_{m} v_{\pi} \rightarrow \beta_{0}$ we obtain, after minor manipulation,

$$
\begin{equation*}
T=-\frac{i_{r}}{i_{t}}=\frac{\beta_{0}}{1+\frac{R_{B}+r_{\pi}}{R_{C} / / r_{o}}} \tag{7.68}
\end{equation*}
$$

(Note that $T<\beta_{0}$.) To find $a_{\mathrm{ff}}$, suppress the dependent source to obtain the situation of Fig. 7.54b. Using the voltage divider rule and Ohm's law, we get

$$
\begin{equation*}
a_{\mathrm{ft}}=\lim _{g_{m} \rightarrow 0} \frac{v_{o}}{i_{i}}=\frac{r_{o} / / R_{C}}{R_{B}+\left(r_{o} / / R_{C}\right)} \times\left\{r_{\pi} / /\left[R_{B}+\left(r_{o} / / R_{C}\right)\right]\right\} \tag{7.69}
\end{equation*}
$$

image_name:(a)
description:
[
name: rπ, type: Resistor, value: rπ, ports: {N1: Vπ, N2: GND}
name: RB, type: Resistor, value: RB, ports: {N1: Vπ, N2: Vo}
name: gmvπ, type: VoltageControlledCurrentSource, ports: {Np: Vo, Nn: GND}
name: ro, type: Resistor, value: ro, ports: {N1: Vo, N2: GND}
name: RC, type: Resistor, value: RC, ports: {N1: Vo, N2: GND}
name: iT, type: CurrentSource, ports: {Np: Vo, Nn: GND}
]
extrainfo:The circuit diagram (a) is an AC model of a feedback-bias BJT circuit. It includes resistors rπ, RB, ro, and RC, a voltage-controlled current source gmvπ, and current sources iT and iI. The circuit is used to analyze parameters T and aft.
image_name:(b)
description:
[
name: rπ, type: Resistor, value: rπ, ports: {N1: X1, N2: GND}
name: RB, type: Resistor, value: RB, ports: {N1: X1, N2: Vo}
name: ro, type: Resistor, value: ro, ports: {N1: Vo, N2: GND}
name: RC, type: Resistor, value: RC, ports: {N1: Vo, N2: GND}
name: ii, type: CurrentSource, ports: {Np: X1, Nn: GND}
]
extrainfo:This is an AC model of a feedback-bias BJT circuit used to analyze the feedback transconductance (a_ft). It includes resistors, a voltage source, and controlled sources.

FIGURE 7.54 Ac models of the circuit of Fig. 7.53 to find (a) $T$ and (b) $a_{\mathrm{ft}}$.

EXAMPLE 7.24 Find $T, a_{\mathrm{ft}}$, and $A$ for the feedback-bias BJT circuit of Example 7.15. Compare with the results found there, and comment.

#### Solution

(a) Using the component values given in Example $7.15 a$ we get $A_{\text {ideal }}=-R_{B}=$ $-100 \mathrm{~V} / \mathrm{mA}$,

$$
\begin{aligned}
T & =\frac{200}{1+\frac{100+5}{10 / / 100}}=15.9 \\
a_{\mathrm{ft}} & =\frac{100 / / 10}{100+(100 / / 10)} \times\{5 / /[100+(100 / / 10)]\}=0.4 \mathrm{~V} / \mathrm{mA} \\
A & =\frac{-100}{1+1 / 15.9}+\frac{0.40}{1+15.9}=-94.08+0.024=-94.1 \mathrm{~V} / \mathrm{mA}
\end{aligned}
$$

In Example $7.15 a$ we found $L=15.9$ and $A=-94.0 \mathrm{~V} / \mathrm{mA}$. In this case $T$ and $L$ coincide, and feedthrough accounts for only $0.025 \%$ of $A$, a truly negligible amount.
(b) Lowering $R_{B}$ from $100 \mathrm{k} \Omega$ to $5.0 \mathrm{k} \Omega$ gives

$$
\begin{aligned}
& A_{\text {ideal }}=-5.0 \mathrm{~V} / \mathrm{mA} \quad T=95.2 \\
& a_{\mathrm{ft}}=2.4 \mathrm{~V} / \mathrm{mA} \quad A=-4.948+0.025=-4.923 \mathrm{~V} / \mathrm{mA}
\end{aligned}
$$

In Example $7.15 b$ we found $L=65.5$ and $A=-4.925 \mathrm{~V} / \mathrm{mA}$. Even though the values of $A$ are still very close, $T$ and $L$ differ appreciably, and feedthrough has increased from $0.025 \%$ to about $0.5 \%$ of $A$. Note that the value of $A$ obtained via $T$ is exact, whereas that obtained via $L$ is only approximate.

Next, consider the generalized BJT circuit of Fig. 7.55a, shown with the external driving source already suppressed. Depending on where we apply the input and where we obtain the output, different topologies can be realized with just this one circuit! Thus, applying a voltage to the base or a current to the emitter we have, respectively, series or shunt summing. Using as output the emitter voltage or the collector current we have, respectively, shunt or series sensing. Yet, $T$ is an intrinsic characteristic of the circuit that must be invariant irrespective of the topology in use. On the contrary, both $L$ and $a_{\mathrm{ft}}$ will generally vary with the topology. To find $T$, break the loop right downstream of the controlled source, short-circuit the latter, and then subject the circuit downstream to the test source $i_{t}$ as in Fig. 7.55b. Using the voltage divider rule and Ohm's law we get

$$
i_{r}=g_{m} v_{\pi}=g_{m} \frac{r_{\pi}}{R_{B}+r_{\pi}}\left(-v_{e}\right)=g_{m} \frac{r_{\pi}}{R_{B}+r_{\pi}}\left[\left(R_{B}+r_{\pi}\right) / / R_{E} / / r_{o}\right]\left(-i_{t}\right)
$$

Letting $g_{m} v_{\pi} \rightarrow \beta_{0}$, we obtain, after minor manipulation,

$$
\begin{equation*}
T=-\frac{i_{r}}{i_{t}}=\frac{\beta_{0}}{1+\frac{R_{B}+r_{\pi}}{R_{E} / r_{o}}} \tag{7.70}
\end{equation*}
$$

image_name:(a)
description:
[
name: RB, type: Resistor, value: RB, ports: {N1: GND, N2: X1}
name: RE, type: Resistor, value: RE, ports: {N1: Ve, N2: GND}
name: Q1, type: NPN, ports: {C: GND, B: x1, E: Ve'}
]
extrainfo:The circuit diagram (a) represents a generalized BJT AC circuit with resistors RB and RE, and an NPN transistor X1. The small-signal model (b) includes a voltage-controlled current source gmvπ, resistors rπ and ro, and a current source it.
image_name:(b)
description:
[
name: RB, type: Resistor, value: RB, ports: {N1: GND, N2: X1}
name: rπ, type: Resistor, value: rπ, ports: {N1: X1, N2: ve}
name: gmVπ, type: VoltageControlledCurrentSource, value: gmVπ, ports: {Np: ve, Nn: ve}
name: ro, type: Resistor, value: ro, ports: {N1: ve, N2: ve}
name: RE, type: Resistor, value: RE, ports: {N1: ve, N2: GND}
name: it, type: CurrentSource, value: it, ports: {Np: GND, Nn: ve}
]
extrainfo:The circuit diagram (b) is a small-signal model of a BJT to find the transfer function T. It uses a voltage-controlled current source to model the transconductance, and includes resistors to represent the base resistance (rπ), output resistance (ro), and emitter resistance (RE). The circuit is grounded at multiple points and uses the current source to model the transistor's behavior.

FIGURE 7.55 (a) A generalized BJT ac circuit, and (b) its small-signal model to find $T$.
(Note that $T<\beta_{0}$.) Interestingly enough, there is a formal similarity with Eq. (7.68), provided we let $R_{C} \rightarrow R_{E}$. Can you explain why?
(a) In the generalized ac circuit of Fig. 7.55a, let $R_{B}=0$ and $R_{E}=10 \mathrm{k} \Omega$. Moreover, let the BJT have $g_{m}=1 /(25 \Omega), r_{\pi}=5 \mathrm{k} \Omega$, and $r_{o}=100 \mathrm{k} \Omega$, as in previous examples. Find $T$.
(b) Repeat, but with $R_{B}=30 \mathrm{k} \Omega$.
(c) Under what conditions is $T$ maximized, and what is its value in this example?

#### Solution

(a) Applying Eq. (7.70) we get

$$
T=\frac{200}{1+\frac{5}{10 / / 100}}=129
$$

(b) Changing $R_{B}$ from zero to $30 \mathrm{k} \Omega$ lowers the return ratio to $T=41$.
(c) Equation (7.70) indicates that $T$ is maximized when $R_{B}=0$ and $R_{E}=\infty$, implying the use of an ideal current sink to provide emitter bias for the CB transistor. Then, $T_{\max }=\beta_{0} /\left(1+r_{\pi} / r_{o}\right)=190.5$.
(a) Using the value of $T$ calculated in Example 7.25a, find the gain $A$ for the case in which the generalized BJT circuit of Fig. $7.55 a$ is operated in the seriesshunt mode as in Example 7.12, with the output being the emitter voltage. Compare and comment.
(b) Find the gain $A$ if the generalized BJT circuit of Fig. $7.55 a$ is operated in the series-series mode as in Example 7.17, with the output being now the collector current. Compare and comment.

#### Solution

From Example $7.25 a$ we know that $T=129$ regardless of the feedback topology.
(a) For series-shunt operation, refer to Fig. 7.56. To find $A_{\text {ideal }}$, let $g_{m} \rightarrow \infty$ in Fig. 7.56a. In this limit the dependent source will require a vanishingly small control voltage $v_{\pi}$ to sustain a finite output $v_{0}$. So, both the voltage across and
image_name:(a)
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: RB, type: Resistor, value: RB, ports: {N1: Vsig, N2: vπ+v0}
name: rπ, type: Resistor, value: rπ, ports: {N1: vπ+v0, N2: GND}
name: gmVπ, type: VoltageControlledCurrentSource, value: gmVπ, ports: {Np: v0, Nn: GND}
name: ro, type: Resistor, value: ro, ports: {N1: v0, N2: GND}
name: RE, type: Resistor, value: RE, ports: {N1: v0, N2: GND}
]
extrainfo:The circuit represents an AC model for a BJT in series-shunt operation. The dependent source gmVπ represents the transconductance of the BJT, and the resistors rπ, ro, and RE model the intrinsic resistances. The input signal is provided by Vsig, and the output is represented as Vo.
image_name:(b)
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: RB, type: Resistor, value: RB, ports: {N1: Vsig, N2: V1}
name: rπ, type: Resistor, value: rπ, ports: {N1: V1, N2: V0}
name: ro, type: Resistor, value: ro, ports: {N1: Vo, N2: GND}
name: RE, type: Resistor, value: RE, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit diagram (b) is a BJT model in series-series feedback configuration. It includes a voltage source Vsig, resistors RB, rπ, ro, and RE, and a voltage-controlled current source gmVπ. The output is taken across ro and RE, with V1 connected to the node between RB and rπ.

FIGURE 7.56 (a) Ac model for the BJT of Fig. 7.55a in series-shunt operation.
(b) Circuit to find $a_{\mathrm{ft}}$.
the current through $r_{\pi}$ will approach zero, giving, for $R_{B}=0, v_{o}=v_{b}=v_{s i g}$, or $A_{\text {ideal }}=v_{o} / v_{s i g}=1 \mathrm{~V} / \mathrm{V}$. To find $a_{\mathrm{ft}}$, suppress the BJT's dependent source by replacing it with an open circuit. This results in the situation of Fig. 7.56b, where we have, by the voltage divider rule,

$$
a_{\mathrm{ft}}=\lim _{g_{m} \rightarrow 0} \frac{v_{o}}{v_{s i g}}=\frac{R_{E} / / r_{o}}{R_{B}+r_{\pi}+\left(R_{E} / / r_{o}\right)}=\frac{1}{1+\frac{R_{B}+r_{\pi}}{R_{E} / / r_{o}}}=\frac{1}{1+\frac{0+5}{10 / / 100}}=\frac{1}{1.55}
$$

Using Eq. (7.63) we finally get

$$
A=\frac{1}{1+1 / 129}+\frac{1 / 1.55}{1+129}=0.992+0.005=0.997 \mathrm{~V} / \mathrm{V}
$$

This result matches exactly that of Example 7.12. To test for the accuracy of both methods, recall from Section 2.9 that the exact gain for $R_{B}=0$ is

$$
A_{\text {exact }}=\frac{1}{1+\frac{r_{\pi}}{\left(\beta_{0}+1\right)\left(R_{E} / / r_{o}\right)}}=\frac{1}{1+\frac{5}{201(10 / / 100)}}=0.997 \mathrm{~V} / \mathrm{V}
$$

Viewing the above expression as $A_{\text {exact }}=1 /\left(1+1 / L_{\text {exact }}\right)$, we readily find

$$
L_{\text {exact }}=\frac{\left(\beta_{0}+1\right)\left(R_{E} / / r_{o}\right)}{r_{\pi}}=\frac{201(10 / / 100)}{5}=365.5
$$

which is in excellent agreement with $L=364$ of Example 7.12. Thus, whether we use Eq. (7.61) with $L=364$ (as we did in Example 7.12), or we use Eq. (7.63) with $T=129$ and $a_{\mathrm{ft}}=1 / 1.55$ (as we are doing presently), we obtain consistent results for $A$.
(b) For series-series operation refer to Fig. 7.57. As we know, negative feedback regulates the emitter current $i_{e}$. The output current $i_{o}$ is outside the feedback loop, but it is related to the former as $i_{o}=\alpha_{0} i_{e}$. Given that $i_{e}=v_{e} / R_{E}$, we can recycle the value of $v_{e} / v_{s i g}$ found in part (a) and write

$$
\frac{i_{o}}{v_{s i g}}=\frac{i_{o}}{i_{e}} \times \frac{i_{e}}{v_{e}} \times \frac{v_{e}}{v_{s i g}}=\alpha_{0} \times \frac{1}{R_{E}} \times A=\frac{200}{201} \times \frac{1}{10^{4}} \times 0.997=99.2 \mu \mathrm{~A} / \mathrm{V}
$$

Comparing the gain of $98.7 \mu \mathrm{~A} / \mathrm{V}$ of Example 7.17 against the exact gain of $99.2 \mu \mathrm{~A}$ found here we conclude that the discrepancy stems from the approximations at the basis of the circuits of Fig. 7.38.
image_name:FIGURE 7.57
description:
[
name: Vsig, type: VoltageSource, ports: {Np: Vsig, Nn: GND}
name: RB, type: Resistor, value: RB, ports: {N1: Vsig, N2: X1}
name: rπ, type: Resistor, value: rπ, ports: {N1: X1, N2: ve}
name: gmvπ, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: ve}
name: RE, type: Resistor, value: RE, ports: {N1: ve, N2: GND}
name: ro, type: Resistor, value: ro, ports: {N1: GND, N2: ve}
]
extrainfo:The circuit represents an AC model for a BJT in series-series operation. It includes a voltage source Vsig, resistors RB, rπ, RE, and ro, and a voltage-controlled current source gmvπ. The output current io flows towards the ground.

FIGURE 7.57 Ac model for the BJT of Fig. 7.55a in series-series operation.

Remark: As mentioned, $L$ generally varies with the feedback topology, even though the sourceless circuit is the same. However, $T$ remains invariant.

We conclude our list of examples with the circuit of Fig. 7.58a, which uses a CMOS inverter to implement an inverting amplifier with ideal voltage gain $A_{v}=v_{o} / v_{i}=$ $-R_{2} / R_{1}$. As we know, this is a shunt-shunt configuration, so to prepare the circuit for two-port analysis we perform the input source transformation of Fig. 7.58b. To find $A_{v}$, we first find the transresistance gain $A=v_{o} / i_{i}$, then we let

$$
\begin{equation*}
A_{v}=\frac{v_{o}}{v_{i}}=\frac{v_{o}}{i_{i}} \times \frac{i_{i}}{v_{i}}=\frac{A}{R_{1}} \tag{7.71}
\end{equation*}
$$

As we know, the two FETs of a CMOS inverter reinforce each other in providing transconductance, acting like a single equivalent FET with equivalent parameters

$$
g_{m}=g_{m n}+g_{m p} \quad r_{o}=r_{o n} / / r_{o p}
$$

image_name:FIGURE 7.58 (a)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: C, type: Capacitor, value: C, ports: {Np: Vi, Nn: RC}
name: R1, type: Resistor, value: R1, ports: {N1: RC, N2: In(-1)}
name: R2, type: Resistor, value: R2, ports: {N1: In(-1), N2: Vo}
name: CMOS, type: OpAmp, ports: {InP: GND, InN: In(-), OutP: Vo, OutN: GND}
]
extrainfo:The circuit is a CMOS inverter used as an inverting amplifier. The voltage source Vi is connected to a capacitor C, followed by resistors R1 and R2, forming a feedback loop with the CMOS op-amp. The op-amp is powered by VDD and grounded.

amplifier. (b) Its shunt-shunt ac equivalent.
image_name:(a)
description:
[
name: i_i, type: CurrentSource, ports: {Np: v_g, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: v_g, N2: v_g}
name: R2, type: Resistor, value: R2, ports: {N1: v_g, N2: v_o}
name: g_m v_g, type: VoltageControlledCurrentSource, ports: {Np: v_o, Nn: GND}
name: r_o, type: Resistor, value: r_o, ports: {N1: v_o, N2: GND}
]
extrainfo:The circuit is a small-signal equivalent of a CMOS inverter used as an inverting amplifier. It includes resistors R1 and R2, a voltage-controlled current source g_m*v_g, and a resistor r_o. The current source i_i is connected to the input node and ground.
image_name:(b)
description:
[
name: i_e, type: CurrentSource, value: i_e, ports: {Np: GND, Nn: vg}
name: R1, type: Resistor, value: R1, ports: {N1: Vg, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vg, N2: GND}
name: i_f, type: CurrentSource, value: i_f, ports: {Np: GND, Nn: vo}
name: g_m v_g, type: VoltageControlledCurrentSource, ports: {Np: Vo, Nn: GND}
name: r_o, type: Resistor, value: r_o, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a small-signal equivalent of a CMOS inverter used as an inverting amplifier. It includes resistors R1 and R2, a voltage-controlled current source representing the transconductance g_m, and resistors modeling the output resistance r_o. The current sources i_e and i_f represent small-signal currents.

FIGURE 7.59 (a) Small-signal equivalent of the circuit of Fig. 7.58. (b) Circuit to find $a$ and $b$.

This is shown in the small-signal equivalent of Fig. 7.59a. This circuit is simple enough that we can find its exact gain $A$ directly. We will also find $A$ via loop-gain analysis and via return-ratio analysis, so we can compare the three methods and get a better feel for similarities and differences.

#### Exercise 7.2

Use node analysis to prove that the circuit of Fig. 7.59a gives

$$
\begin{equation*}
A=\frac{v_{o}}{i_{i}}=-R_{2} \frac{1}{1+\frac{\left(1+R_{2} / R_{1}\right)\left(1+R_{2} / r_{o}\right)}{g_{m} R_{2}-1}} \tag{7.72}
\end{equation*}
$$

so that, expressing as $A=\left(-R_{2}\right) /\left(1+1 / L_{\text {exact }}\right)$ we get, after minor manipulation,

$$
\begin{equation*}
L_{\text {exact }}=\frac{g_{m}\left(R_{2} / / r_{o}\right)-1 /\left(1+R_{2} / r_{o}\right)}{1+R_{2} / R_{1}} \tag{7.73}
\end{equation*}
$$

Next, estimate $L$ via two-port analysis. With reference to Fig. $7.59 b$ we readily find

$$
\begin{gather*}
a=\frac{v_{o}}{i_{\varepsilon}}=-g_{m}\left(R_{1} / / R_{2}\right) \times\left(R_{2} / / / r_{o}\right) \quad b=\lim _{i_{s} \rightarrow 0} \frac{i_{f}}{v_{o}}=-\frac{1}{R_{2}} \\
L=a b=\frac{g_{m}\left(R_{2} / / r_{o}\right)}{1+R_{2} / R_{1}} \tag{7.74}
\end{gather*}
$$

Note that the two-port approximation gives, for this circuit, $L>L_{\text {exact }}$. The difference between the two depends on the ratio $R_{2} / r_{o}$ : the higher this ratio, the smaller the difference.

Finally, we turn to Fig. 7.60 $a$ and $b$ to calculate $T$ and $a_{\mathrm{ft}}$, respectively. The results are easily found to be

$$
\begin{equation*}
T=-\frac{i_{r}}{i_{t}}=\frac{g_{m} r_{o}}{1+\left(R_{2}+r_{o}\right) / R_{1}} \quad a_{\mathrm{ft}}=\lim _{g_{m} \rightarrow 0} \frac{v_{o}}{i_{i}}=\frac{r_{o}}{1+\left(R_{2}+r_{o}\right) / R_{1}} \tag{7.75}
\end{equation*}
$$

image_name:(a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vg, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vg, N2: Vo}
name: g_mv_g, type: VoltageControlledCurrentSource, value: g_mv_g, ports: {Np: vo, Nn: GND}
name: i_t, type: CurrentSource, value: i_t, ports: {Np: Vo, Nn: GND}
name: r_o, type: Resistor, value: r_o, ports: {N1: Vo, N2: Vd}
]
extrainfo:The circuit diagram (a) is used to calculate the transfer function T and involves a voltage-controlled current source, resistors R1 and R2, and current sources i_t and i_i. The circuit is configured for unity voltage-gain operation. The analysis involves finding Av = vo/vi using exact, two-port, and return-ratio methods.
image_name:(b)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: X1, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: X1, N2: Vo}
name: r_o, type: Resistor, value: r_o, ports: {N1: Vo, N2: GND}
name: i_i, type: CurrentSource, ports: {Np: GND, Nn: x1}
]
extrainfo:The circuit (b) is a small-signal model for analyzing the parameter a_ft. It consists of a current source i_i, resistors R1 and R2, and a resistor r_o connected to the output Vo.

FIGURE 7.60 Small-signal circuits to find (a) $T$ and (b) $a_{\mathrm{ft}}$ for the circuit of Fig. 7.58.
(a) In the circuit of Fig. $7.58 a$ let $g_{m}=2 \mathrm{~mA} / \mathrm{V}$ and $r_{o}=50 \mathrm{k} \Omega$. Assuming the circuit has been configured for unity voltage-gain operation using $R_{1}=R_{2}=$ $100 \mathrm{k} \Omega$, find $A_{v}=v_{o} / v_{i}$ via exact analysis, via two-port analysis, and via return-ratio analysis. Compare the three cases, and comment.
(b) Repeat, but for the case $R_{1}=R_{2}=10 \mathrm{k} \Omega$. Compare with part (a), and comment.

#### Solution

(a) We have $A_{v(\text { (ideal })}=-100 / 100=-1 \mathrm{~V} / \mathrm{V}$. Applying Eqs. (7.71) through (7.73) we get

$$
\begin{aligned}
& L_{\mathrm{exact}}=\frac{2(100 / / 50)-1 /(1+100 / 50)}{1+100 / 100}=33.33-0.17=33.17 \\
& A_{v}=\frac{-100 / 100}{1+1 / 33.17}=-0.9707 \mathrm{~V} / \mathrm{V}
\end{aligned}
$$

Applying Eqs. (7.74) and (7.61) gives

$$
L=2 \frac{100 / / 50}{1+100 / 100}=33.33 \quad A_{v}=\frac{-100 / 100}{1+1 / 33.3}=-0.9709 \mathrm{~V} / \mathrm{V}
$$

Applying Eq. (7.75) we find

$$
T=\frac{2 \times 50}{1+(100+50) / 100}=40.0 \quad a_{\mathrm{ft}}=\frac{50}{1+(100+50) / 100}=20 \mathrm{~V} / \mathrm{A}
$$

so Eq. (7.63) gives

$$
A_{v}=\frac{1}{100}\left(\frac{-100}{1+1 / 40}+\frac{20}{1+40}\right)=\frac{1}{100}(-97.56+0.49)=-0.9707 \mathrm{~V} / \mathrm{V}
$$

As mentioned, two-port analysis for this circuit slightly overestimates the value of $L$ compared to the exact value, but in this case the effect upon $A_{v}$ is negligible. Note also that $T>L$ as $a_{\mathrm{ft}}$ and $A_{v(\text { ideal })}$ have opposite polarities. Forward transmission through the feedback network accounts for about $0.5 \%$ of $A_{v}$.
(b) Recalculating with $R_{1}=R_{2}=10 \mathrm{k} \Omega$ we have $A_{v(\text { (ideal })}=-10 / 10=-1 \mathrm{~V} / \mathrm{V}$ and

$$
\begin{array}{ll}
L_{\text {exact }}=7.917 & A_{v}=-0.8879 \mathrm{~V} / \mathrm{V} \\
L=8.333 & A_{v}=-0.8929 \mathrm{~V} / \mathrm{V} \\
T=14.29 & a_{\mathrm{ft}}=7.14 \mathrm{~V} / \mathrm{A} \quad A_{v}=-0.9346+0.047=-0.8879 \mathrm{~V} / \mathrm{V}
\end{array}
$$

Again, the gain via the return-ratio matches the exact gain. Lowering $R_{1}$ and $R_{2}$ simultaneously by an order of magnitude leaves $A_{v(\text { (ideal })}$ unchanged but alters the loading as well as the forward transmission conditions appreciably. Indeed, $T$ is now almost twice as large as $L$ and forward transmission through the feedback network now accounts for $5 \%$ of $A_{v}$.

### The Feedback Factor $\boldsymbol{\beta}$

By analogy with the two-port loop gain $L$, which takes on the form of a product $L=$ $a b$, it is convenient to express also the return-ratio loop gain $T$ as a product,

$$
\begin{equation*}
T=a \beta \tag{7.76}
\end{equation*}
$$

where $\beta$, the counterpart of $b$, shall be called the return-ratio feedback factor (this, to distinguish it from $b$, which shall be called the two-portfeedback factor). The derivation of $\beta$ is similar to that of $T$ of Eq. (7.60), except that the return signal is now the signal controlling the dependent source (alternatively, we can find $T$ and then let $\beta=$ $T / a$ ). Just as $T$ and $L$ are generally different, so are $\beta$ and $b$, though they may coincide in particular cases. Let us illustrate via the noninverting op amp of Fig. 7.20, repeated for convenience in Fig. 7.61a. With reference to Fig. 7.61b, we readily find $\beta$ using the voltage divider twice. So, we write

$$
\beta=-\frac{v_{d}}{v_{t}}=\frac{1}{1+\frac{R_{2}}{r_{i} / / R_{1}}} \times \frac{1}{1+\frac{r_{o}}{r_{i} / / R_{1}+R_{2}}} \quad a=a_{v}
$$

image_name:Fig. 7.61a
description:
[
name: Vi, type: VoltageSource, ports: {Np: vi, Nn: GND}
name: ri, type: Resistor, value: ri, ports: {N1: vi, N2: X1}
name: R1, type: Resistor, value: R1, ports: {N1: X1, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: X1, N2: vo}
name: avvd, type: VoltageControlledVoltageSource, ports: {Np: avvd, Nn: GND2}
name: ro, type: Resistor, value: ro, ports: {N1: avvd, N2: vo}
]
extrainfo:This is a noninverting amplifier circuit with a voltage-controlled voltage source representing the op-amp with gain avvd. The input voltage source Vi provides the input signal vi, and the resistors R1 and R2 form a feedback network. The resistor ri represents the input resistance of the op-amp, and ro represents the output resistance.
image_name:Fig. 7.61b
description:
[
name: Vt, type: VoltageSource, value: vt, ports: {Np: Vt, Nn: GND}
name: ro, type: Resistor, value: ro, ports: {N1: Vt, N2: X1}
name: R2, type: Resistor, value: X1, ports: {N1: X1, N2: -Vd}
name: R1, type: Resistor, value: R1, ports: {N1: -Vd, N2: GND}
name: ri, type: Resistor, value: ri, ports: {N1: -Vd, N2: GND}
]
extrainfo:The circuit is used to find the feedback factor β in a noninverting amplifier configuration. It includes a voltage source Vt, resistors ro, R2, R1, and ri, and a voltage-controlled voltage source represented by vd.

FIGURE 7.61 (a) Noninverting amplifier and (b) circuit to find $\beta$. $\left(a_{\mathrm{v}}=1000 \mathrm{~V} / \mathrm{V}, r_{i}=10 \mathrm{k} \Omega, r_{o}=1.0 \mathrm{k} \Omega, R_{1}=1.0 \mathrm{k} \Omega\right.$, and $R_{2}=9.0 \mathrm{k} \Omega$.)

On the other hand, according to Eqs. (7.48) and (7.46), we have, respectively,

$$
b=\frac{1}{1+R_{2} / R_{1}} \quad a=\frac{r_{i}}{r_{i}+\left(R_{1} / / R_{2}\right)} a_{v} \frac{R_{1}+R_{2}}{r_{o}+R_{1}+R_{2}}
$$

Plugging in the component values of Fig. 7.61 we get

$$
L=a b=833.3 \times \frac{1}{10}=83.33 \quad T=a \beta=1000 \times \frac{1}{12}=83.33
$$

We now make the following generalizations:

- Two-port analysis makes the feedback factor $b$ depend exclusively on the feedback network such that $b=1 / A_{\text {ideal }}(=1 / 10$ in the above example). Loading by the feedback network is absorbed by the amplifier, causing gain to drop from $a_{v}=1000$ to $a=833.3$ in the example.
- Return-ratio analysis leaves the amplifier gain unchanged at $a_{v}$ ( $=1000$ in the example). Loading by amplifier is absorbed by the feedback network, causing the feedback factor to drop from $b=1 / 10$ to $\beta=1 / 12$ in the example. Consequently, $A_{\text {ideal }} \neq 1 / \beta$ (to avoid confusion, always calculate $A_{\text {ideal }}$ in the limit $k \rightarrow \infty$, or $a_{v} \rightarrow \infty$ in the case of an op amp circuit).
- In this particular case we have $T=L$, though in general $T$ and $L$ differ. As mentioned, even when $T$ and $L$ are equal, they contribute differently to $A$ as per Eqs (7.61) and (7.63).
As we embark upon the study of stability, in Section 7.7, we shall use returnratio analysis because it shifts loading to $\beta$ and it makes easier to investigate stability graphically, starting with the Bode plot of the gain $a$.

## 7.6 BLACKMAN'S IMPEDANCE FORMULA AND INJECTION METHODS

The return ratio is a powerful tool also for the calculation of the closed-loop resistance $R$ between any pair of nodes of a negative-feedback circuit - not just the nodes of the input and output ports. Such a resistance is given by Blackman's impedance formula ${ }^{5}$

$$
\begin{equation*}
R=r_{0} \frac{1+T_{\mathrm{sc}}}{1+T_{\mathrm{oc}}} \tag{7.77}
\end{equation*}
$$

where

$$
\begin{equation*}
r_{0}=\lim _{k \rightarrow 0} R \tag{7.78}
\end{equation*}
$$

is the resistance between the given node pair with the dependent source set to zero, and $T_{\mathrm{sc}}$ and $T_{\mathrm{oc}}$ are the return ratios of the same source with the two nodes shortcircuited and open-circuited, respectively. Blackman's formula holds regardless of the feedback topology in use. Oftentimes either $T_{\mathrm{sc}}$ or $T_{\mathrm{oc}}$ is zero, indicating that negative feedback will either raise $r_{0}$ by $\left(1+T_{\mathrm{sc}}\right.$ ) (this is the case of a series topology), or lower $r_{0}$ by ( $1+T_{\mathrm{oc}}$ ) (shunt topology).

EXAMPLE 7.28 Consider the feedback-bias shunt-shunt circuit of Fig. 7.62, which has already been the focus of our attention in Examples 7.15 and 7.24. Assuming the parameter values of Example $7.15 b\left(R_{B}=5.0 \mathrm{k} \Omega, R_{C}=10 \mathrm{k} \Omega, g_{m}=1 /(25 \Omega), r_{\pi}=\right.$ $5 \mathrm{k} \Omega$, and $r_{o}=100 \mathrm{k} \Omega$ ), use Blackman's impedance formula to find (a) $R_{i}$ and (b) $R_{o}$. Compare with the example and comment.
image_name:Figure 7.62
description:
[
name: RC, type: Resistor, value: RC, ports: {N1: V0, N2: GND}
name: RB, type: Resistor, value: RB, ports: {N1: X1, N2: V0}
name: NPN, type: NPN, ports: {C: Vo, B: X1, E: GND}
name: ii, type: CurrentSource, value: ii, ports: {Np: GND, Nn: ii}
]
extrainfo:This is a feedback-bias BJT circuit with a shunt-shunt topology. It includes resistors RC, RB, Ri, Ro, an NPN transistor, and a current source ii. The circuit is used to analyze input and output resistances using Blackman's impedance formula.

FIGURE $\mathbf{7 . 6 2}$ Feedback-bias BJT circuit of Example 7.28.

#### Solution

To find $r_{i 0}$ and $r_{o 0}$, we let $g_{m} \rightarrow 0$ while suppressing the input source $i_{i}$ and leaving the output port open-circuited. This yields the situation of Fig. 7.63a. To find the return ratios we use Fig. 7.63b.
(a) By inspection,

$$
r_{i 0}=r_{\pi} / /\left[R_{B}+\left(r_{o} / / R_{C}\right)\right]=5 / /[5+(100 / / 10)]=3.69 \mathrm{k} \Omega
$$

Short-circuiting the input port in Fig. 7.63b yields $v_{\pi}=0$, and thus $i_{r}=0$, so $T_{\mathrm{sc}}=0$. Leaving the input port open-circuited results in the same situation of Example 7.24b, so we recycle the result obtained there and write $T_{\text {oc }}=95.2$. Consequently,

$$
R_{i}=r_{i 0} \frac{1+T_{\mathrm{sc}}}{1+T_{\mathrm{oc}}}=3.69 \frac{1+0}{1+95.2}=38.4 \Omega
$$

image_name:(a)
description:
[
name: RB, type: Resistor, value: RB, ports: {N1: V1, N2: V2}
name: rπ, type: Resistor, value: rπ, ports: {N1: V1, N2: GND}
name: ro, type: Resistor, value: ro, ports: {N1: V2, N2: GND}
name: RC, type: Resistor, value: RC, ports: {N1: V2, N2: GND}
]
extrainfo:The circuit in diagram (a) is an AC model for analyzing input and output resistances. It includes resistors RB, rπ, ro, and RC connected in a network to determine r_i0 and r_o0.
image_name:(b)
description:
[
name: RB, type: Resistor, value: RB, ports: {N1: V1, N2: V2}
name: rπ, type: Resistor, value: rπ, ports: {N1: V1, N2: GND}
name: ro, type: Resistor, value: ro, ports: {N1: V2, N2: GND}
name: RC, type: Resistor, value: RC, ports: {N1: V2, N2: GND}
name: gmvπ, type: VoltageControlledCurrentSource, value: gmvπ, ports: {Np: V2, Nn: GND}
name: it, type: CurrentSource, value: it, ports: {Np: V2, Nn: GND}
]
extrainfo:The circuit is an AC model for analyzing return ratios with resistors and controlled sources. It includes a voltage-controlled current source and a current source connected to ground.

FIGURE 7.63 Ac models of the circuit of Fig. 7.62 for finding (a) $r_{i 0}$ and $r_{00}$, and (b) the return ratios.
(b) Referring again to Fig. 7.63a, we have, by inspection,

$$
r_{o 0}=R_{C} / / r_{o} / /\left(R_{B}+r_{\pi}\right)=4.76 \mathrm{k} \Omega
$$

Short-circuiting the output port in Fig. 7.63b gives again $v_{\pi}=0$, and thus $T_{\mathrm{sc}}=0$. Likewise, leaving it open-circuited gives again $T_{\mathrm{oc}}=95.2$. Consequently,

$$
R_{o}=r_{o 0} \frac{1+T_{s c}}{1+T_{o c}}=4.76 \frac{1+0}{1+95.2}=49.5 \Omega
$$

The values of $38.2 \Omega$ and $49.2 \Omega$ found in Example $7.15 b$ are fairly close to the present (exact) ones.

The Wilson current mirror, shown in ac form in Fig. 7.64a, is a shunt-series feedback circuit based on $Q_{3}$. This is better understood via the small-signal equivalent of Fig. 7.64b, where we note that diode-connected $Q_{2}$ senses $Q_{3}$ 's emitter current, and current mirror $Q_{1}$ replicates this current with a feedback factor of unity and then sinks it from the input summing node. We wish to use Blackman's impedance formula in connection with the dependent source modeling $Q_{1}$ to find expressions for (a) $R_{i}$ and (b) $R_{o}$.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: X1, B: X2, E: GND}
name: Q2, type: NPN, ports: {C: X2, B: X2, E: GND}
name: Q3, type: NPN, ports: {C: GND, B: X1, E: X2}
name: i_i, type: CurrentSource, ports: {Np: GND, Nn: X1}
]
extrainfo:The circuit diagram (a) is a shunt-series feedback circuit based on Q3, using a Wilson current mirror configuration with Q1, Q2, and Q3. This configuration senses Q3's emitter current and mirrors it using Q1 and Q2. The feedback factor is unity, providing current sinking from the input summing node.
image_name:(b)
description:
[
'name': 'i_i', 'type': 'CurrentSource', 'ports': {'Np': 'GND', 'Nn': 'X2'
'name': 'r_π', 'type': 'Resistor', 'value': 'r_π', 'ports': {'N1': 'X2', 'N2': 'X1'
'name': 'β_0i_1', 'type': 'CurrentControlledCurrentSource', 'ports': {'Np': 'GND', 'Nn': 'X1'
'name': 'i2', 'type': 'CurrentControlledCurrentSource', 'ports': {'Np': 'X2', 'Nn': 'GND'
'name': '1/g_m', 'type': 'Resistor', 'value': '1/g_m', 'ports': {'N1': 'X1', 'N2': 'GND'
'name': 'r_o', 'type': 'Resistor', 'value': 'r_o', 'ports': {'N1': 'X1', 'N2': 'GND'
]
extrainfo:The circuit is a small-signal equivalent of a shunt-series feedback circuit. It uses a Wilson current mirror configuration with transistors Q1, Q2, and Q3. The feedback is provided by a current mirror with a feedback factor of unity.

FIGURE 7.64 (a) The Wilson current mirror, and (b) its small-signal equivalent.

#### Solution

To find $r_{i 0}$ and $r_{00}$, we suppress the input source $i_{i}$ and set the dependent source modeling $Q_{1}$ to zero. This yields the situation of Fig. 7.65a. By inspection,

$$
r_{i 0}=r_{\pi}+\left(\beta_{0}+1\right)\left(\frac{1}{g_{m}} / / r_{o}\right) \cong 2 \pi_{\pi} \quad r_{o 0}=r_{o}+\frac{1}{g_{m}} \cong r_{o}
$$

To find the return ratios, refer to Fig. 7.65b.
(a) With the input terminal open circuited as in Fig. 7.65b we have $i_{r}=1 i_{2} \cong\left(\beta_{0}\right.$ $+1) i_{1}=-\left(\beta_{0}+1\right) i_{t}$, where we have ignored $r_{o}$ because it is in parallel with $1 / g_{m}$, and $r_{o} \gg 1 / g_{m}$. Consequently, $T_{\mathrm{oc}}=-i_{r} / i_{t}=\left(\beta_{0}+1\right)$. Shorting the
image_name:(a)
description:
[
'name': 'r_π', 'type': 'Resistor', 'value': 'r_π', 'ports': {'N1': 'LOAD1', 'N2': 'X1'
'name': 'β_0i', 'type': 'VoltageControlledCurrentSource', 'ports': {'Np': 'X2', 'Nn': 'X1'
'name': '1/g_m', 'type': 'Resistor', 'value': '1/g_m', 'ports': {'N1': 'X1', 'N2': 'GND'
'name': 'r_o', 'type': 'Resistor', 'value': 'r_o', 'ports': {'N1': 'X2', 'N2': 'GND'
]
extrainfo:The circuit is used to analyze the return ratios with open and short circuit conditions at the input terminal. It includes a voltage-controlled current source and several resistors to model the behavior of a transistor.
image_name:(b)
description:
[
name: r_π, type: Resistor, value: r_π, ports: {N1: LOAD1, N2: X1}
name: β_0i, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: X1}
name: r_o, type: Resistor, value: r_o, ports: {N1: X1, N2: GND}
name: 1/g_m, type: Resistor, value: 1/g_m, ports: {N1: X1, N2: GND}
name: i_t, type: CurrentSource, ports: {Np: LOAD1, Nn: GND}
name: 1i_2, type: VoltageControlledCurrentSource, ports: {Np: LOAD2, Nn: GND}
]
extrainfo:The circuit diagram (b) is used to find the return ratios with the input terminal open-circuited and the output terminal shorted to ground. The current source i_t is used to simulate the input current, and the voltage-controlled current source β_0i represents the transistor's behavior. The resistors r_π, r_o, and 1/g_m model the transistor's internal resistances.

FIGURE 7.65 Modifying the circuit of Fig. $7.64 b$ to find (a) $r_{i 0}$ and $r_{00}$, and (b) to find the return ratios.
input terminal to ground will cause $i_{t}$ to flow through this short, giving $i_{1}=$ $i_{2}=0$. So, $i_{r}=0$ and $T_{\mathrm{sc}}=0$. Then,

$$
R_{i}=r_{i 0} \frac{1+T_{\mathrm{sc}}}{1+T_{\mathrm{oc}}}=2 r_{\pi} \frac{1+0}{1+\beta_{0}+1} \cong \frac{2}{g_{m}}
$$

(b) With the output terminal shorted to ground as in Fig. $7.65 b$ we can recycle the result of ( $a$ ) and write $T_{\mathrm{sc}}=\left(\beta_{0}+1\right)$. Open-circuiting the output terminal will cause the current $\beta_{0} i_{1}$ to flow through $r_{o}$, yielding $i_{r}=1 i_{2}=i_{1}=-i_{t}$. So, $T_{\text {oc }}=-i_{r} / i_{t}=1$, and

$$
R_{o}=r_{o 0} \frac{1+T_{\mathrm{sc}}}{1+T_{\mathrm{oc}}} \cong r_{o} \frac{1+\beta_{0}+1}{1+1}=r_{o} \frac{\beta_{0}+2}{2} \cong \frac{\beta_{0}}{2} r_{o}
$$

Both results coincide with those derived in Section 4.8. It is interesting to note that in part (b) both $T_{\mathrm{oc}}$ and $T_{\mathrm{sc}}$ are different from zero. Moreover, $T_{\mathrm{sc}}$ in part (b) is the same as $T_{\mathrm{oc}}$ in part (a).

### Finding T via Successive Voltage and Current Injections

When dealing with a feedback circuit in physical form in the lab, or in transistorlevel schematic form in the course of computer simulation, we do not have access to any internal dependent sources, so we need alternative techniques for finding $T$. An elegant technique, devised by R. D. Middlebrook, is the successive voltage and current injection technique ${ }^{6}$ depicted in Fig. 7.66. Its steps are as follows.

- First, set all external signal sources to zero so as to put the circuit in its dormant state.
- Break the feedback loop and insert a series test source $v_{t}$ as shown in Fig. 7.66a. The perturbation introduced by $v_{t}$ will cause a signal $v_{f}$ to propagate in the forward direction, in turn causing the feedback system to respond with a return signal $v_{r}$. Measure the voltage ratio

$$
\begin{equation*}
T_{v}=-\frac{v_{r}}{v_{f}} \tag{7.79a}
\end{equation*}
$$

image_name:(a)
description:The circuit diagram (a) illustrates a feedback system with a voltage test source vt inserted in series. The perturbation introduced by vt causes a forward signal vf and a return signal vr. The voltage ratio Tv is measured as -vr/vf.
image_name:(b)
description:The circuit diagram (b) illustrates the current injection method. A current source 'it' is placed in series with the feedback loop to measure the current ratio. The perturbation introduced by 'it' causes a forward signal 'if' and a return signal 'ir'. The current ratio is measured as T_i = -ir/if.

FIGURE 7.66 Illustrating the (a) voltage injection and (b) current injection method.

- Remove the test source $v_{t}$ and apply between the same set of wires a shunt test source $i_{t}$ as shown in Fig. 7.66b. The perturbation introduced by $i_{t}$ will cause a signal $i_{f}$ to propagate in the forward direction, in turn causing the feedback system to respond with a return signal $i_{r}$. Measure the current ratio

$$
\begin{equation*}
T_{i}=-\frac{i_{r}}{i_{f}} \tag{7.79b}
\end{equation*}
$$

- It has been proved ${ }^{6}$ that the loop's return ratio $T$ is such that

$$
\begin{equation*}
\frac{1}{1+T}=\frac{1}{1+T_{v}}+\frac{1}{1+T_{i}} \tag{7.80}
\end{equation*}
$$

Solving for $T$ we get

$$
\begin{equation*}
T=\frac{T_{v} T_{i}-1}{T_{v}+T_{i}+2} \tag{7.81}
\end{equation*}
$$

It should be noted that $T$ is independent of the particular point of the loop at which the two injections are made.
Depending on the point of signal injection, the ac signals $v_{t}$ and $i_{t}$ may need to be kept suitably small to prevent the circuit from behaving nonlinearly. Note that both test setups preserve the existing dc biasing conditions as well as the existing loading conditions. An actual example will better illustrate.

Shown in Fig. 7.67 is the feedback-bias BJT that we have already investigated in Examples 7.15 and 7.24. Lacking any input signal source, the circuit is already in its ac dormant state. Assuming the BJT has $I_{s}=2 \mathrm{fA}, \beta_{F}=200$, and $V_{A}=100 \mathrm{~V}$, use PSpice to find the return ratio of this circuit, compare with Example 7.24, and comment.
image_name:Figure 7.67
description:
[
name: RB, type: Resistor, value: 5 kΩ, ports: {N1: X, N2: Y}
name: RC, type: Resistor, value: 10 kΩ, ports: {N1: X1, N2: VCC}
name: VCC, type: VoltageSource, value: 10.8 V, ports: {Np: VCC, Nn: GND}
name: Q, type: NPN, ports: {C: X1, B: Y, E: GND}
]
extrainfo:This is a feedback-bias BJT configuration with feedback signal flow in a counterclockwise direction. The circuit is in its AC dormant state with no input signal source.

FIGURE 7.67 The feedback-bias BJT configuration.

#### Solution

In this circuit rendition feedback signal flow is counterclockwise, and there are three points where we can apply our double injection, namely, $X, Y$, and $Z$. In the laboratory one would choose a point where signal levels are the highest and therefore easier to measure, especially in the presence of noise. In the PSpice circuits of Fig. 7.68 we have arbitrarily chosen point $Y$, but the procedure can readily be repeated for the other two. (Note that the current injection circuit requires the use of two $0-\mathrm{V}$ dummy sources $V_{1}$ and $V_{2}$ to sense the currents $i_{r}$ and $i_{f}$ ) The results of the simulation are as follows:

| At point $X:$ | $T_{v}=179.8$ | $T_{i}=201.1$ | $T=94.4$ |
| :--- | :--- | :--- | :--- |
| At point $Y:$ | $T_{v}=353.4$ | $T_{i}=129.4$ | $T=94.3$ |
| At point $Z:$ | $T_{v}=1983$ | $T_{i}=99.26$ | $T=94.4$ |

It is interesting that $T_{v}$ and $T_{i}$ change with the point of injection whereas $T$ is invariant (within roundoff errors). Also, $T$ agrees well with the value found in Example $7.24 b$ via hand calculations.
image_name:FIGURE 7.68 (a)
description:
[
name: RB, type: Resistor, value: 5kΩ, ports: {N1: X1, vr: vr}
name: RC, type: Resistor, value: 10kΩ, ports: {N1: VCC, N2: X1}
name: VCC, type: VoltageSource, value: 10.8V, ports: {Np: VCC, Nn: GND}
name: Q1, type: NPN, ports: {C: X1, B: vf, E: GND}
name: vt, type: VoltageSource, value: 1mVac, ports: {Np: vf, Nn: vr}
]
extrainfo:The circuit is a feedback-bias configuration with a voltage injection at the base of an NPN transistor. The biasing is provided by a voltage source VCC and resistors RB and RC. The voltage source vr injects a small AC voltage into the base of the transistor.
image_name:FIGURE 7.68 (b)
description:
[
name: RB, type: Resistor, value: 5kΩ, ports: {N1: X2, N2: V1}
name: RC, type: Resistor, value: 10kΩ, ports: {N1: VCC, N2: X2}
name: VCC, type: VoltageSource, value: 10.8V, ports: {Np: VCC, Nn: GND}
name: V1, type: VoltageSource, value: 0, ports: {Np: V1, Nn: X1}
name: V2, type: VoltageSource, value: 0, ports: {Np: X1, Nn: vb1}
name: it, type: CurrentSource, value: 1nAac, ports: {Np: GND, Nn: X1}
name: X1, type: NPN, ports: {C: X2, B: vb1, E: GND}
]
extrainfo:The circuit is a feedback-bias configuration with two NPN transistors. It includes a voltage source of 1mVac and a current source of 1nAac. The feedback is provided through resistors RB and RC connected to a common VCC supply of 10.8V. The transistors share the same collector and base nodes, with their emitters grounded.

FIGURE 7.68 Applying (a) voltage and (b) current injection to the feedback-bias circuit of Fig. 7.67.
image_name:FIGURE 7.69
description:The system block diagram, labeled as FIGURE 7.69, represents a feedback loop system with impedances $Z_{f}$ and $Z_{r}$. The diagram is structured in a rectangular loop indicating a feedback mechanism.

Main Components:
1. **Impedance $Z_{f}$:** This component is positioned in the forward path of the loop. It represents the impedance seen when looking in the forward direction.
2. **Impedance $Z_{r}$:** This component is positioned in the return path of the loop. It represents the impedance seen when looking in the return direction.

Flow of Information or Control:
- The diagram shows a signal entering from the left side, traveling through the forward impedance $Z_{f}$, and then looping back through the return impedance $Z_{r}$.
- The arrows indicate the direction of signal flow, with the signal moving clockwise through the loop.
- The feedback loop is explicitly labeled, indicating that part of the signal is fed back from the output to the input to control the system's behavior.

Labels, Annotations, and Key Indicators:
- The diagram includes labels for the impedances $Z_{f}$ and $Z_{r}$, which are critical for understanding the system's signal flow and feedback characteristics.
- The feedback loop is clearly labeled, emphasizing its role in the system.

Overall System Function:
The primary function of the system is to manage signal flow through a feedback loop, where the forward and return impedances play a crucial role in determining the system's behavior. The feedback mechanism allows for control and stability of the system by adjusting how much of the output signal is fed back into the input. This configuration is common in electronic circuits where maintaining specific signal characteristics is necessary.

FIGURE 7.69 The impedances $Z_{f}$ and $Z_{r}$ seen
looking in the forward and the return directions.

### Single-Injection Approximations

According to Eq. (7.80), the terms $\left(1+T_{v}\right)$ and $\left(1+T_{i}\right)$ combine like resistances in parallel. If one happens to be much larger than the other, the smaller will prevail and we can estimate $T$ more quickly by limiting ourselves to just one signal injection, namely, the one that results in the much smaller return ratio. For instance, had we anticipated the condition $T_{v} \gg T_{i}$ at point $Z$ in the circuit of Fig. 7.67, we could have skipped the voltage injection to approximate $T \cong T_{i} \cong 99$, for an error of less than $5 \%$. The choice of where to break the feedback loop is facilitated by the fact that $T_{v}$ and $T_{i}$ are constrained as ${ }^{6}$

$$
\begin{equation*}
\frac{1+T_{v}}{1+T_{i}}=\frac{Z_{r}}{Z_{f}} \tag{7.82}
\end{equation*}
$$

where $Z_{f}$ and $Z_{r}$ are the impedances seen looking in the forward and in the return directions from the point of signal injection, as depicted in Fig. 7.69. For instance, if we select point $Z$ in Fig. 7.67, then $Z_{r}$ is the impedance seen looking into the collector, which is much higher than the impedance $Z_{f}$ seen looking toward the node common to $R_{C}$ and $R_{B}$. Consequently, Eq. (7.82) predicts $\left(1+T_{v}\right) \gg\left(1+T_{i}\right)$, as we already know from Example 7.30.

Using the 741 macro-model available in PSpice's library, find $T$ for the case in which the 741 is configured to function as an inverting amplifier with a gain of $-100 \mathrm{~V} / \mathrm{V}$ by means of two resistances $R_{1}=1.0 \mathrm{k} \Omega$ and $R_{2}=100 \mathrm{k} \Omega$. Pick a point where only one injection is sufficient.

#### Solution

After setting the input source to zero to put the circuit in its dormant state, we end up with the situation of Fig. 7.70. The point of injection has been chosen right at the op amp's inverting input, where $Z_{f}\left(=r_{i}\right)$ is in the $\mathrm{M} \Omega$ range, while $Z_{r}\left[=R_{1} / /\right.$ $\left.\left(R_{2}+r_{o}\right)\right]$ is less than $1 \mathrm{k} \Omega$. With a disparity on the order of three orders of magnitude it is hardly worth performing the current-injection test, so we limit ourselves to a mere voltage test, as shown. The simulation yields

$$
T_{v}=1970
$$

The student can verify that a current-injection test at the same node would yield $T_{i}=1.983 \times 10^{6}\left(\gg T_{v}\right)$, thus validating the approximation $T \cong T_{v}$.
image_name:FIGURE 7.70 Circuit of Example 7.31
description:
[
name: μA741, type: OpAmp, value: μA741, ports: {InP: GND, InN: Vf, OutP: Out, OutN: GND, Vdd: VCC, -Vdd: VEE}
name: R1, type: Resistor, value: 1.0 kΩ, ports: {N1: Vr, N2: GND}
name: R2, type: Resistor, value: 100 kΩ, ports: {N1: Out, N2: Vr}
name: Vt, type: VoltageSource, value: 1 mVac, ports: {Np: Vf, Nn: Vr}
]
extrainfo:The circuit is a feedback amplifier using a μA741 operational amplifier. The op-amp is powered by ±10V supplies (VCC and VEE). The input voltage source Vf is 1 mVac. R1 and R2 form a voltage divider providing feedback to the inverting input of the op-amp.

FIGURE 7.70 Circuit of Example 7.31, where only voltage injection suffices.

## 7.7 STABILITY IN NEGATIVE-FEEDBACK CIRCUITS

For all its benefits, negative feedback poses the potential risk of oscillation. Because of this, negative feedback was met with skepticism when first proposed by Harold Black, in 1928. However, once this risk became better understood and suitable cures were developed to tame unwanted oscillations, negative feedback established itself as the cornerstone of electronics and control we know today. To develop a basic feel for stability (or lack thereof), let us assume negligible feedthrough, so both the amplifier and the feedback network can be regarded as unilateral as in Fig. 7.71. Moreover, we take the viewpoint of the IC designer, whose concern is to ensure that the amplifier is stable when operated with purely resistive feedback networks. With this type of feedback, the feedback factor $\beta$ is frequency independent and its phase angle is thus zero. (If the feedback network contains reactive elements such as capacitors, then $\beta$ too will be frequency dependent and the responsibility for ensuring stability is now shifted to the user. ${ }^{7}$ )

Let us start out by expressing the closed-loop gain in the more insightful form

$$
\begin{equation*}
A(j f)=\frac{S_{o}}{S_{i}}=A_{\text {ideal }} \times D(j f) \tag{7.83}
\end{equation*}
$$

where $A_{\text {ideal }}=\lim _{a \rightarrow \infty} A$, and the quantity

$$
\begin{equation*}
D(j f)=\frac{1}{1+1 / T(j f)} \tag{7.84}
\end{equation*}
$$

image_name:FIGURE 7.71
description:The system block diagram, referred to as FIGURE 7.71, represents a negative-feedback system featuring a unilateral amplifier and a feedback network with a frequency-independent feedback factor \( \beta \).

1. **Main Components:**
- **Input Signal \( S_i \):** The starting point of the system where the input signal is applied.
- **Summer (\( \Sigma \)):** This block combines the input signal \( S_i \) with the feedback signal \( S_f \). It outputs the error signal \( S_\varepsilon \), which is the difference between \( S_i \) and \( S_f \).
- **Amplifier \( a(jf) \):** This block amplifies the error signal \( S_\varepsilon \) and is characterized by a frequency-dependent gain \( a(jf) \).
- **Output Signal \( S_o \):** The result of the amplified signal, which is the output of the system.
- **Feedback Network \( \beta \):** This block takes a portion of the output signal \( S_o \) and feeds it back to the summer as the feedback signal \( S_f \). The feedback factor \( \beta \) is constant and frequency-independent.

2. **Flow of Information or Control:**
- The input signal \( S_i \) enters the summer \( \Sigma \) where it is combined with the feedback signal \( S_f \) to produce the error signal \( S_\varepsilon \).
- The error signal \( S_\varepsilon \) is then amplified by the amplifier \( a(jf) \) to produce the output signal \( S_o \).
- A portion of \( S_o \) is fed back through the feedback network with a gain \( \beta \), creating the feedback signal \( S_f \).
- This feedback signal \( S_f \) is subtracted from the input signal \( S_i \) at the summer, completing the feedback loop.

3. **Labels, Annotations, and Key Indicators:**
- The diagram includes labels for each signal and component, such as \( S_i \), \( S_o \), \( S_\varepsilon \), \( S_f \), \( a(jf) \), and \( \beta \).
- The positive and negative signs at the summer indicate the subtraction of \( S_f \) from \( S_i \).

4. **Overall System Function:**
- The primary function of this system is to maintain stability and control the output by using negative feedback. The feedback loop helps in minimizing the error signal \( S_\varepsilon \) by adjusting the output based on the feedback signal \( S_f \). The frequency-independent feedback factor \( \beta \) ensures that the feedback does not vary with frequency, simplifying stability analysis and design considerations.

FIGURE 7.71 Negative-feedback system with unilateral amplifier and feedback network, and a frequency independent feedback factor $\beta$.
is called the discrepancy function because it gives a measure of the deviation of $A(j f)$ from $A_{\text {ideal }}$. Moreover, $T(j f)=\beta a(j f)$ is the familiar loop gain. As a signal $S_{\varepsilon}$ propagates around the loop and returns to the summer $\Sigma$ as $S_{f}$, it experiences a frequency-dependent phase shift, which we shall denote as ph $T(j f)$. If this shift reaches $-180^{\circ}$, then feedback turns from negative to positive. Denoting the frequency at which this happens as $f_{-180^{\circ}}$, it follows that $T\left(j f_{-180^{\circ}}\right)$ is a real, negative number such as $-0.5,-1,-2$, etc. We have three possibilities:

- $\left|T\left(j f_{-180^{\circ}}\right)\right|<1$. Even though feedback is positive at $f_{-180^{\circ}}, S_{\varepsilon}$ gets attenuated each time it goes around the loop, so if we set $S_{i} \rightarrow 0$, any signal present in the loop will eventually decay to zero, and the system is said to be stable.
- $T\left(j f_{-180^{\circ}}\right) \rightarrow-1$. By Eq. (7.84) we have $D\left(j f_{-180^{\circ}}\right) \rightarrow \infty$ and so $A\left(j f_{-180^{0}}\right) \rightarrow \infty$, indicating that the system can sustain an output signal $S_{o} \neq 0$ with a vanishingly small input $S_{i} \rightarrow 0$. Once a signal component $S_{\varepsilon}\left(j f_{-180^{\circ}}\right)$ is initiated in the circuit (for instance by electronic noise, which is always present in one form or another), this component will emerge from the feedback network as $S_{f}\left(j f_{-180^{0}}\right)=-S_{\varepsilon}\left(j f_{-180^{\circ}}\right)$, and then undergo one more inversion at the summer $\Sigma$ to reappear at the amplifier's input as the original signal $S_{\varepsilon}\left(j f_{-180^{\circ}}\right)$ itself! A circuit's ability to sustain a signal at $f_{-180^{\circ}}$ qualifies it as an oscillator, and such the circuit is regarded as unstable.
- $\left|T\left(j f_{-180}\right)\right|>1$. Suppose we change $T\left(j f_{-180^{\circ}}\right)$ from -1 to a more negative value, say, -1.1 . This implies a $10 \%$ increase in magnitude each time a signal goes around the loop, thus resulting in oscillations of growing magnitude. The oscillations will grow until some inherent circuit nonlinearity, such as op amp saturation, will limit $T$ to -1 exactly and thus sustain steady oscillation. Though this mechanism can be exploited on purpose to design oscillators, when it comes to amplifiers, buffers, V-I and I-V converters, voltage and current sources, and active filters, oscillations must be avoided by all means. As we shall see, unwanted oscillations are tamed via suitable techniques generally referred to as frequency compensation.

Suppose the circuit of Fig. 7.71 is unstable and such that its own internal noise
EXAMPLE 7.32 has initiated a growing oscillation at 1 MHz . If amplitude increases by $10 \%$ from one oscillation cycle to the next, find the number of cycles as well as the amount of time it takes for the oscillation to grow from 1 nV to 1 V .

#### Solution

After going around the loop once, the amplitude will be $(1 \mathrm{nV}) \times 1.1$; after going around twice, it will be $(1 \mathrm{nV}) \times 1.1^{2}$, and so forth. Imposing $(1 \mathrm{nV}) \times 1.1^{n}=1 \mathrm{~V}$ and solving, we get $n \cong 217$. Since one period of oscillation is $1 / 10^{6}=1 \mu \mathrm{~s}$, the signal takes about $217 \times(1 \mu \mathrm{~s})=217 \mu \mathrm{~s}$ to grow from 1 nV to 1 V .

### Graphical Visualization of the Loop Gain $\boldsymbol{T}$

Given the impact of the loop gain $T$ upon the stability of a circuit, we seek a quick way to visualize the frequency plots of the magnitude $|T(j f)|$ and the phase angle ph $T(j f)$. By definition,

$$
|T|_{\mathrm{dB}}=20 \log |T|=20 \log |a \beta|=20 \log \left|\frac{a}{1 / \beta}\right|=20 \log |a|-20 \log \left|\frac{1}{\beta}\right|
$$

that is,

$$
\begin{equation*}
|T(j f)|_{\mathrm{dB}}=|a(j f)|_{\mathrm{dB}}-\left|\frac{1}{\beta}\right|_{\mathrm{dB}} \tag{7.85a}
\end{equation*}
$$

Similarly, $\operatorname{ph} T(j f)=\operatorname{ph} a(j f)-\operatorname{ph} \beta$. So long as $\beta$ is frequency independent we have $\operatorname{ph} \beta=0$, so

$$
\begin{equation*}
\operatorname{ph} T(j f)=\operatorname{ph} a(j f) \tag{7.85b}
\end{equation*}
$$

Based on these relationships, we proceed as follows:

- On the decibel plot of $|a(j f)|$, draw the decibel plot of the noise gain $1 / \beta$ as depicted in Fig. 7.72a, top. Since $\beta$ is assumed to be frequency independent and
image_name:(a)
description:The graph labeled "(a)" in Figure 7.72 illustrates two main plots related to the analysis of open-loop gain and phase characteristics of a system.

1. **Type of Graph and Function:**
- The top plot is a Bode plot showing the magnitude of the open-loop gain \(|a(jf)|\) in decibels (dB) versus frequency \(f\).
- The bottom plot is a phase plot showing the phase of \(a(jf)\) in degrees versus frequency \(f\).

2. **Axes Labels and Units:**
- **Top Plot:**
- Vertical axis: "Open-loop gain \(a\) (dB)".
- Horizontal axis: Frequency \(f\), likely in a logarithmic scale.
- **Bottom Plot:**
- Vertical axis: "ph \(a\)" in degrees, ranging from 0° to -180°.
- Horizontal axis: Frequency \(f\), consistent with the top plot.

3. **Overall Behavior and Trends:**
- **Magnitude Plot:**
- The open-loop gain \(|a(jf)|\) starts at a high value \(a_0\) and decreases with increasing frequency.
- A horizontal line represents the noise gain \(1/\beta\), which is constant across frequencies.
- The crossover frequency \(f_x\) is marked where the open-loop gain intersects the \(1/\beta\) line.
- **Phase Plot:**
- The phase starts near 0° and decreases, approaching -180° as frequency increases.

4. **Key Features and Technical Details:**
- **Magnitude Plot:**
- The initial gain level is \(T_0\).
- The crossover frequency \(f_x\) is a critical point where the gain equals \(1/\beta\).
- The phase margin \(\phi_m\) is indicated at the crossover frequency.
- **Phase Plot:**
- The phase margin \(\phi_m\) is shown as the difference between the phase at \(f_x\) and -180°.

5. **Annotations and Specific Data Points:**
- The crossover frequency \(f_x\) is marked on both plots as a vertical line.
- The phase margin \(\phi_m\) is annotated on the phase plot to highlight stability considerations.
- The point where the gain plot intersects the \(1/\beta\) line is annotated as \(|T|\).
image_name:(b)
description:The graph labeled "(b)" is a Bode plot, which consists of two subplots: one for magnitude and one for phase. This type of graph is commonly used to analyze the frequency response of a system.

1. **Magnitude Plot (Top):**
- **Axes:**
- **Vertical Axis:** Represents the loop gain \(|T(jf)|\) in decibels (dB).
- **Horizontal Axis:** Represents frequency \(f\), typically in hertz (Hz).
- **Scale:** The frequency axis is likely logarithmic, which is standard for Bode plots.
- **Behavior:**
- The plot starts at a high gain level \(T_0\) and shows a downward trend as frequency increases, indicating a decrease in gain.
- The curve crosses the 0 dB line at the crossover frequency \(f_x\).
- **Key Features:**
- The crossover frequency \(f_x\) is marked where the gain crosses 0 dB.
- The initial gain level \(T_0\) is indicated at the low-frequency end.

2. **Phase Plot (Bottom):**
- **Axes:**
- **Vertical Axis:** Represents the phase \(\operatorname{ph} T\) in degrees.
- **Horizontal Axis:** Represents frequency \(f\), consistent with the magnitude plot.
- **Behavior:**
- The phase starts at 0° and decreases as frequency increases, eventually approaching -180°.
- **Key Features:**
- The phase margin \(\phi_m\) is indicated, which is the difference between the phase at the crossover frequency and -180°.
- The phase curve shows a typical slope that flattens out as it approaches -180°.

Overall, this Bode plot provides insights into the stability and frequency response characteristics of the system, highlighting important parameters like the crossover frequency and phase margin.

FIGURE 7.72 Visualizing the loop gain $|T(j f)|$, the crossover frequency $f_{x}$, and the phase margin $\phi_{m}$.
$0<\beta \leq 1$, the $1 / \beta$ curve will be a horizontal line positioned somewhere above the $0-\mathrm{dB}$ axis (or right on the $0-\mathrm{dB}$ axis if $\beta=1$ ).

- Visualize the plot of $|T(j f)|$ as the difference between the plot of $|a(j f)|$ and the $1 / \beta$ curve. Equivalently, visualize the plot of $|T(j f)|$ as the plot of $|a(j f)|$, but with the $1 / \beta$ curve as its new $0-\mathrm{dB}$ axis, as depicted in Fig. $7.72 b$, top.
- The plot of $|T(j f)|$ starts out at the typically high dc value $T_{0}=\beta a_{0}$, and then it rolls off with frequency with the same profile as $|a(j f)|$.
- The frequency at which the $1 / \beta$ curve intersects the $|a(j f)|$ curve is aptly called the crossover frequency $f_{x}$. At this frequency we have $\left|T\left(j f_{x}\right)\right|=0 \mathrm{~dB}$, or $\left|T\left(j f_{x}\right)\right|=1 \mathrm{~V} / \mathrm{V}$, so we can write $T\left(j f_{x}\right)=1 \exp \left(j \phi_{x}\right)$, where $\phi_{x}=\operatorname{ph} a\left(j f_{x}\right)$, as depicted in Fig. 7.72a (bottom).
- For $f>f_{x}$ the decibel value of $|T(j f)|$ becomes negative, indicating loop signal attenuation. For $|T(j f)| \ll 1$ we can approximate Eq. (7.84) as $|D(j f)| \cong$ $|1 /(1 / T)|=|T(j f)|$.

### The Phase Margin $\boldsymbol{\phi}_{\boldsymbol{m}}$

In light of the discussion at the beginning of this section, we want the crossover to occur well before the dreaded condition $T=1 e^{j\left(-180^{\circ}\right)}=-1$ occurs, which is the recipe for oscillation. The degree of stability of a circuit is quantified via the phase margin, defined as $\phi_{m}=\phi_{x}-\left(-180^{\circ}\right)$, that is,

$$
\begin{equation*}
\phi_{m}=180+\phi_{x} \tag{7.86}
\end{equation*}
$$

This margin is depicted in Fig. $7.72 b$ (bottom). As we move along, we shall be interested in the value of the discrepancy function at $f_{x}$. Letting $T\left(j f_{x}\right)=1 \exp \left(j \phi_{x}\right)=$ $1 \exp \left[j\left(\phi_{m}-180^{\circ}\right)\right]=-1 \exp \left(j \phi_{m}\right)$ in Eq. (7.84), we get

$$
\begin{aligned}
\left|D\left(j f_{x}\right)\right| & =\left|\frac{1}{1+1 /\left(-1 e^{j \phi_{m}}\right)}\right|=\left|\frac{1}{1-e^{-j \phi_{m}}}\right|=\left|\frac{1}{1-\left(\cos \phi_{m}-j \sin \phi_{m}\right)}\right| \\
& =\frac{1}{\sqrt{\left(1-\cos \phi_{m}\right)^{2}+\left(\sin \phi_{m}\right)^{2}}}
\end{aligned}
$$

where Euler's formula has been used. Expanding and using the identity $\cos ^{2} \phi_{m}+$ $\sin ^{2} \phi_{m}=1$ gives

$$
\begin{equation*}
\left|D\left(j f_{x}\right)\right|=\frac{1}{\sqrt{2\left(1-\cos \phi_{m}\right)}} \tag{7.87}
\end{equation*}
$$

### An Illustrative Example

Let us illustrate the above concepts using the feedback circuit of Fig. 7.73 as a vehicle. The circuit utilizes a three-stage amplifier consisting of a pair of transconductance stages with dc gains $a_{10}=G_{m 1} R_{1}=10^{3} \mathrm{~V} / \mathrm{V}$ and $a_{20}=G_{m 2} R_{2}=10^{3} \mathrm{~V} / \mathrm{V}$, followed by a unity-gain buffer, so $a_{0}=a_{10} a_{20}=10^{6} \mathrm{~V} / \mathrm{V}$. The pole frequencies of
image_name:FIGURE 7.73
description:The circuit is a three-stage amplifier with feedback, consisting of two transconductance stages followed by a unity-gain buffer. The feedback is controlled by a voltage-controlled voltage source Eβ. The circuit is designed to investigate the behavior of a three-pole operational amplifier under different feedback conditions.

FIGURE 7.73 PSpice circuit to investigate a three-pole op amp under different amounts of feedback.
the three stages are $f_{1}=1 /\left(2 \pi R_{1} C_{1}\right)=1 \mathrm{kHz}, f_{2}=1 /\left(2 \pi R_{2} C_{2}\right)=100 \mathrm{kHz}$, and $f_{3}=1 /\left(2 \pi R_{3} C_{3}\right)=10 \mathrm{MHz}$, so the open-loop gain is

$$
\begin{equation*}
a(j f)=\frac{10^{6}}{\left(1+j f / 10^{3}\right)\left(1+j f / 10^{5}\right)\left(1+j f / 10^{7}\right)} \tag{7.88}
\end{equation*}
$$

Magnitude and phase are calculated as

$$
\begin{gather*}
|a(j f)|=\frac{10^{6}}{\sqrt{\left[1+\left(f / 10^{3}\right)^{2}\right] \times\left[1+\left(f / 10^{5}\right)^{2}\right] \times\left[1+\left(f / 10^{7}\right)^{2}\right]}}  \tag{7.89a}\\
\text { ph } a(j f)=-\left[\tan ^{-1}\left(f / 10^{3}\right)+\tan ^{-1}\left(f / 10^{5}\right)+\tan ^{-1}\left(f / 10^{7}\right)\right] \tag{7.89b}
\end{gather*}
$$

and are plotted via PSpice, as depicted in Fig. 7.74a (magnitude is in dB , as marked at the left, and phase in degrees, as marked at the right).
image_name:(a)
description:The graph in Fig. 7.74a is a Bode plot, which consists of two separate plots: one for magnitude and another for phase. The x-axis represents frequency in Hertz (Hz) on a logarithmic scale, ranging from 10 Hz to 10^8 Hz. The left y-axis indicates the gain \( |a| \) in decibels (dB), ranging from -60 dB to 120 dB. The right y-axis marks the phase of \( a \) in degrees, ranging from -270° to 0°.

Magnitude Plot:
- The magnitude plot shows a decreasing trend as frequency increases. It starts at a high gain of around 100 dB at low frequencies (10 Hz) and progressively decreases.
- Key frequencies are marked as \( f_1 \), \( f_2 \), and \( f_3 \), which correspond to the corner frequencies where the slope of the magnitude plot changes.
- The magnitude decreases with a slope of approximately -20 dB/decade initially, steepening to -40 dB/decade, and finally to -60 dB/decade as frequency increases past each corner frequency.

Phase Plot:
- The phase plot shows a cumulative phase shift starting from 0° at low frequencies and decreasing to -270° at high frequencies.
- At each corner frequency \( f_1 \), \( f_2 \), and \( f_3 \), there is a noticeable change in the phase slope, contributing to the total phase shift.
- The phase reaches -180° at a frequency marked as \( f_{180°} \), indicating a significant phase shift point.

Key Features:
- The Bode plot illustrates the characteristic behavior of a system with three widely spaced poles.
- The magnitude and phase plots are consistent with the mathematical expressions provided, showing the effect of each pole on the system's response.
- The graph helps visualize how the gain and phase of the error amplifier change with frequency, which is crucial for understanding stability and performance in control systems.
image_name:(b)
description:The graph in Fig. 7.74b is a linearized Bode plot, showing both magnitude and phase of the transfer function for an error amplifier. The x-axis represents frequency in hertz (Hz) on a logarithmic scale, ranging from 10^1 to 10^8 Hz. The left y-axis indicates the gain \( a \) in decibels (dB), while the right y-axis shows the phase of \( a \) in degrees.

Type of Graph and Function:
- **Graph Type:** Bode plot (magnitude and phase).
- **Function:** Represents the frequency response of an error amplifier.

Axes Labels and Units:
- **X-Axis:** Frequency \( f \) in Hertz (Hz), logarithmic scale.
- **Left Y-Axis:** Gain \( a \) in decibels (dB).
- **Right Y-Axis:** Phase of \( a \) in degrees.

Overall Behavior and Trends:
- **Magnitude Plot:** The gain starts at 120 dB at low frequencies and decreases linearly in segments with different slopes as frequency increases.
- From \( f_1 \) to \( f_2 \), the slope is \(-20\) dB/decade.
- From \( f_2 \) to \( f_{180^\circ} \), the slope is \(-40\) dB/decade.
- Beyond \( f_{180^\circ} \), the slope is \(-60\) dB/decade.
- **Phase Plot:** The phase starts at 0° and decreases linearly as frequency increases.
- At \( f_1 \), the phase is \(-45\)°.
- At \( f_2 \), the phase is \(-135\)°.
- At \( f_{180^\circ} \), the phase reaches \(-180\)°.
- At \( f_3 \), the phase is \(-270\)°.

Key Features and Technical Details:
- **Cutoff Frequencies:**
- \( f_1 \), \( f_2 \), and \( f_3 \) are marked as significant frequencies where the slope changes.
- **Phase Shifts:**
- \( -45\)° at \( f_1 \), \(-90\)° at \( f_2 \), \(-135\)° at \( f_{180^\circ} \), and \(-270\)° at \( f_3 \).

Annotations and Specific Data Points:
- Annotations on the plot indicate the slope of the magnitude plot and significant phase angles at key frequencies.

FIGURE $\mathbf{7 . 7 4}$ (a) Frequency plots of magnitude $|a|$ and phase $\Varangle a$ for the error amplifier of Fig. 7.73.
(b) Linearized magnitude plot associating phase with slope.

If the roots are widely spaced apart as in the present example, we can combine magnitude and phase in the more concise and visually intuitive form of Fig. 7.74b. Specifically, we draw a linearized magnitude plot using segments with progressively steeper slopes, and we mark significant phase values using the correspondence

$$
\begin{equation*}
\text { Phase }\left(\text { in }^{\circ}\right) \leftrightarrow 4.5 \times \text { Slope }(\text { in } \mathrm{dB} / \mathrm{dec}) \tag{7.90}
\end{equation*}
$$

Thus, from dc to $f_{1}$ we draw a segment with a slope of $0 \mathrm{~dB} / \mathrm{dec}$, for which Eq. (7.90) implies a phase of $0^{\circ}$. From $f_{1}$ to $f_{2}$ we draw a segment with a slope of $-20 \mathrm{~dB} / \mathrm{dec}$, implying a phase of $4.5 \times(-20)$, or $-90^{\circ}$. Right at $f_{1}$ the slope is $-10 \mathrm{~dB} / \mathrm{dec}$, so the corresponding phase is $4.5 \times(-10)$, or $-45^{\circ}$. Likewise, the segment from $f_{2}$ to $f_{3}$ has a slope of $-40 \mathrm{~dB} / \mathrm{dec}$, which implies a phase of $-180^{\circ}$. The phase at $f_{2}$ is $-135^{\circ}$. Past $f_{3}$ slope approaches $-60 \mathrm{~dB} / \mathrm{dec}$ and phase approaches $-270^{\circ}$.

We now wish to investigate the closed-loop response under increasing amounts of feedback, which we implement by varying the feedback factor $\beta$. We have the following significant cases:

- Starting out with $\beta=10^{-5}$, we observe that if we draw the $1 / \beta$ line $\left(1 / \beta=10^{5}=\right.$ 100 dB ) in Fig. $7.74 b$, it will intersect the gain curve at $f_{x} \cong 10 \mathrm{kHz}$, where $\phi_{x} \cong$ $-90^{\circ}$. Consequently, $\phi_{m} \cong 180^{\circ}-90^{\circ}=90^{\circ}$. Figure 7.75 shows that the closedloop gain starts out as $A_{0}=(1 / \beta) /\left(1+1 / T_{0}\right)=10^{5} /(1+1 / 10)=90,909 \mathrm{~V} / \mathrm{V}$ (about $10 \%$ lower than $A_{\text {ideal }}=100,000 \mathrm{~V} / \mathrm{V}$ because of low $T_{0}$ ), and it exhibits a dominant pole frequency of $f_{x}$. Shown in Fig. 7.76a is the response to an input step of $\beta \mathrm{V}(=10 \mu \mathrm{~V})$. This is an approximately exponential transient, so once the input is stepped back to zero, $v_{o}(t)$ will decay in approximately exponential fashion, indicating a stable circuit.
image_name:Figure 7.75
description:The graph in Figure 7.75 is a Bode plot depicting the gain versus frequency response of a circuit with varying feedback levels. The plot is presented on a logarithmic scale for both axes, with the x-axis representing frequency in hertz (Hz) ranging from \(10^2\) to \(10^7\) Hz, and the y-axis representing gain in volts per volt (V/V) ranging from \(10^1\) to \(10^6\).

The graph includes several plots for different values of \(1/\beta\), each associated with a specific phase margin \(\phi_m\). These are:

- \(1/\beta = 10^5\) with \(\phi_m \approx 90^\circ\)
- \(1/\beta = 10^4\) with \(\phi_m \approx 45^\circ\)
- \(1/\beta = 10^3\) with \(\phi_m \approx 17.5^\circ\)
- \(1/\beta = 98.02\) with \(\phi_m = 0^\circ\)

The plot shows that as \(\beta\) increases (or \(1/\beta\) decreases), the crossover frequency shifts to higher frequencies, resulting in greater phase shifts and reduced phase margin. This causes increased peaking and potential instability in the system.

For \(1/\beta = 10^5\), the gain is relatively flat across the frequency range, indicating a stable system with a high phase margin. As \(1/\beta\) decreases, the plots exhibit more pronounced peaks and dips, particularly noticeable at higher frequencies, indicating increased ringing and potential instability.

The graph highlights the trade-off between stability and bandwidth in feedback systems, illustrating how different feedback levels impact the gain and phase characteristics of the circuit.

FIGURE 7.75 Closed-loop responses of the circuit of Fig. 7.73 for different amounts of feedback. Raising $\beta$ lowers the $1 / \beta$ curve, shifting the crossover frequency towards regions of greater phase shift and thus lower phase margin. This, in turn, increases the amount of peaking as well as ringing (see Fig. 7.76).
image_name:(a)
description:### Type of Graph and Function:
The graph labeled (a) is a time-domain waveform representing the step response of a feedback system.

Axes Labels and Units:
- **X-axis:** Time in microseconds (µs), ranging from 0 to 40 µs.
- **Y-axis:** Voltage in volts (V), ranging from 0 to 1 V.

Overall Behavior and Trends:
The waveform shows a gradual rise in voltage from 0 V to 1 V over a period of 40 µs. This behavior indicates a stable response with no overshoot or oscillation, suggesting a high phase margin and a stable closed-loop system.

Key Features and Technical Details:
- The curve starts at 0 V and increases steadily to reach 1 V by approximately 40 µs.
- The system exhibits a smooth and monotonic rise, characteristic of an overdamped response.
- The feedback factor β is set to $10^{-5}$, indicating minimal feedback.

Annotations and Specific Data Points:
- The graph is annotated with β = $10^{-5}$, denoting the feedback level.
- There are no visible peaks, oscillations, or ringing, which implies a stable system with a large phase margin.

Overall, the graph illustrates a stable feedback system with a low feedback factor, resulting in a smooth and gradual step response without any peaking or oscillation.
image_name:(b)
description:The graph labeled (b) is a time-domain waveform illustrating the step response of a circuit for a feedback factor \( \beta = 10^{-4} \). The horizontal axis represents time in microseconds (\( \mu s \)), ranging from 0 to 40 \( \mu s \). The vertical axis represents voltage in volts (V), ranging from 0 V to 1 V.

Overall Behavior and Trends:
- The waveform begins at 0 V and quickly rises, reaching a peak slightly above 1 V at around 5 \( \mu s \), indicating an overshoot.
- After the peak, the waveform exhibits a slight oscillation before settling to a steady state at approximately 1 V.
- This behavior reflects a typical underdamped response, characterized by an initial overshoot followed by damped oscillations as it approaches equilibrium.

Key Features and Technical Details:
- The peak voltage is slightly above 1 V, indicating the presence of overshoot due to the feedback factor.
- The oscillations following the peak are indicative of ringing, which is common in systems with reduced phase margins.
- The settling time, or the time taken to reach and remain within a certain percentage of the final value, is around 20 \( \mu s \).

Annotations and Specific Data Points:
- The feedback factor \( \beta = 10^{-4} \) is annotated on the graph, highlighting the specific condition under which this response is observed.
- The response indicates a phase margin that allows for some overshoot and ringing, reflecting the trade-off between stability and bandwidth in feedback systems.
image_name:(c)
description:The graph labeled (c) is a time-domain waveform illustrating the step response of a feedback circuit with a feedback factor \( \beta = 10^{-3} \). The x-axis represents time in microseconds (\( \mu s \)), ranging from 0 to 40 \( \mu s \). The y-axis represents voltage in volts, ranging from 0 to 2 V.

**Overall Behavior and Trends:**
- The waveform shows an underdamped response with noticeable oscillations. Initially, the voltage rises rapidly from 0 V, surpassing the 1 V mark, indicating overshoot.
- The waveform exhibits decaying oscillations, with the amplitude of the oscillations decreasing over time, suggesting the system is settling towards a steady state.

**Key Features and Technical Details:**
- The initial peak exceeds 1 V, indicating a significant overshoot due to the feedback level.
- The oscillations have a decaying nature, which points to a damping effect in the system.
- This behavior is typical when the system's poles are complex conjugates with a real part that is relatively small compared to the imaginary part, indicating limited damping.

**Annotations and Specific Data Points:**
- The plot is part of a series showing responses for different \( \beta \) values, illustrating how increasing feedback affects system dynamics by increasing overshoot and oscillations.
- The pole-zero plot adjacent to the waveform shows the poles \( p_1 \), \( p_2 \), and \( p_3 \) moving closer to the imaginary axis, indicating reduced stability and increased oscillatory behavior as feedback increases.
image_name:(d)
description:The graph labeled (d) is a time-domain waveform depicting the step response of a feedback system. The x-axis represents time in microseconds (μs), ranging from 0 to 5 μs, while the y-axis represents voltage in volts (V), ranging from 0 V to 2 V. The graph is linear in scale.

**Overall Behavior and Trends:**
The waveform shows a periodic oscillation with a constant amplitude, indicating a sustained oscillatory response over the observed time period. This behavior suggests that the system is at the brink of instability, characterized by a phase margin of 0 degrees.

**Key Features and Technical Details:**
- The system exhibits a constant amplitude oscillation, indicating a lack of damping.
- The feedback factor is given as β = 1.02 × 10⁻², which corresponds to a phase margin (φₘ) of 0 degrees. This implies that the system is marginally stable.

**Annotations and Specific Data Points:**
- The oscillation period is consistent throughout the graph, suggesting a stable frequency of oscillation.
- The poles in the accompanying pole-zero diagram are positioned on the imaginary axis, further confirming the marginal stability of the system.

This graph illustrates the critical point where increasing feedback leads to a loss of stability, resulting in sustained oscillations without decay.
image_name:(e)
description:The graph labeled (e) in the image is a time-domain waveform illustrating the step response of a feedback circuit for a specific feedback factor, \( \beta = 2 \times 10^{-2} \). The x-axis represents time in microseconds (\( \mu s \)), ranging from 0 to 5 \( \mu s \), while the y-axis shows voltage in nanovolts (nV), ranging from -200 nV to 200 nV.

**Overall Behavior and Trends:**
The waveform exhibits oscillatory behavior, indicating a response with significant ringing. The oscillations are periodic and decrease slightly in amplitude over time, suggesting a lightly damped system. This behavior is characteristic of a feedback system with a low phase margin, where the system is close to instability.

**Key Features and Technical Details:**
- The waveform starts at 0 V and quickly begins to oscillate.
- The amplitude of the oscillations is approximately 200 nV at the peak and -200 nV at the trough.
- The frequency of oscillation appears to be consistent throughout the displayed time period.
- The pole-zero plot accompanying the waveform shows three poles, \( p_1, p_2, \) and \( p_3 \), with \( p_1 \) and \( p_2 \) being complex conjugates, indicating the oscillatory nature of the response.

**Annotations and Specific Data Points:**
- The feedback factor \( \beta = 2 \times 10^{-2} \) is annotated on the graph.
- The response shows a phase margin close to zero, as indicated by the pole locations, suggesting a system on the verge of instability.

FIGURE 7.76 Step responses and pole locations of the circuit of Fig. 7.73 for increasing values of $\beta$.

- Raising $\beta$ to $10^{-4}$ lowers the $1 / \beta$ line to 80 dB in Fig. $7.74 b$, giving $f_{x} \cong 100 \mathrm{kHz}$ and $\phi_{x} \cong-135^{\circ}$, so $\phi_{m} \cong 180^{\circ}-135^{\circ}=45^{\circ}$. The closed-loop gain now exhibits a bit of peaking just before $f_{x}$, after which it rolls off with frequency as $|a(j f)|$. By Eq. (7.87) we have $\left|D\left(j f_{x}\right)\right|=1 / \sqrt{2\left(1-\cos 45^{\circ}\right)}=1.307$, so

Eq. (7.83) predicts $\left|A\left(j f_{x}\right)\right|=10^{4} \times 1.307=13,070 \mathrm{~V} / \mathrm{V}$, which is $30.7 \%$ higher than $A_{\text {ideal }}$. Recall from systems theory that peaking in the frequency domain is accompanied by ringing in the time domain. This is confirmed by Fig. 7.76b, showing the transient response to an input step of $\beta \mathrm{V}(=0.1 \mathrm{mV})$. Once we step the input back to zero, $v_{o}(t)$ will decay to zero, albeit with a bit of ringing. We conclude that a circuit with $\phi_{m}=45^{\circ}$ is still a stable circuit, though its (moderate) amount of peaking and ringing may be undesirable in certain applications.

- For $\beta=10^{-3}$ the $1 / \beta$ line is lowered further to 60 dB in Fig. $7.74 b$, so $f_{x}$ is now the geometric mean of 100 kHz and 1 MHz , or $f_{x} \cong \sqrt{10^{5} \times 10^{6}}=$ 316 kHz , and $\phi_{x}$ is the arithmetic mean of $-145^{\circ}$ and $-180^{\circ}$, or $\phi_{x} \cong$ $-162.5^{\circ}$, so $\phi_{m} \cong 180^{\circ}-162.5^{\circ}=17.5^{\circ}$. With a reduced phase margin, both peaking and ringing are more pronounced. In fact we now have $\left|D\left(j f_{x}\right)\right|=$ $1 / \sqrt{2\left(1-\cos 17.5^{\circ}\right)}=3.29$, so Eq. (7.83) predicts $\left|A\left(j f_{x}\right)\right| \cong 1,000 \times 3.29=$ $3,290 \mathrm{~V} / \mathrm{V}$, or almost $3.3 \times A_{\text {ideal }}!$ Figure $7.76 c$ shows the response to an input step of $\beta \mathrm{V}(=1 \mathrm{mV})$. Once we step the input back to zero, $v_{o}(t)$ will decay with quite a bit of ringing. We conclude that a circuit with $\phi_{m}=17.5^{\circ}$, though still stable, is likely to be unacceptable in most applications because of excessive peaking and/or ringing.
- Cursor measurements on the PSpice plots of Fig. 7.74a give $f_{-180^{\circ}}=1.006 \mathrm{MHz}$, where $\left|a\left(j f_{-180^{\circ}}\right)\right|=98.02 \mathrm{~V} / \mathrm{V}$, so if we let $\beta=1 / 98.02=1.02 \times 10^{-2}$, we get $f_{x}=1.006 \mathrm{MHz}$ and $\phi_{x}=-180^{\circ}$, or $\phi_{m}=0^{\circ}$. Consequently, $\left|D\left(j f_{x}\right)\right| \rightarrow \infty$, indicating oscillatory bevavior. This is confirmed by the response to a $10-\mathrm{mV}$ input step of Fig. 7.76d.
- Raising $\beta$ to $2 \times 10^{-2}$ lowers the $1 / \beta$ curve further, pushing $f_{x}$ into a region of additional phase shift and thus $\phi_{m}<0^{\circ}$. All it takes now is internal noise to trigger a growing oscillation. Using an input step of just 1 nV to simulate noise, we obtain the response of Fig. 7.76e.

It is instructive to visualize circuit behavior also in terms of its poles in the complex plane. Letting $j f \rightarrow s /(2 \pi)$ in Eq. (7.88), substituting into Eq. (7.84) and then into Eq. (7.83), gives

$$
A(s)=\frac{10^{6}}{\beta 10^{6}+\left(1+\frac{S}{2 \pi 10^{3}}\right)\left(1+\frac{S}{2 \pi 10^{5}}\right)\left(1+\frac{S}{2 \pi 10^{7}}\right)}
$$

The roots of the denominator are the poles of $A(s)$. Using a scientific calculator or similar, we find the poles tabulated in Table 7.2. These data are best visualized in the $s$-plane as shown (not to scale) on the right side of Fig. 7.76. Starting out with no feedback $(\beta=0)$ and gradually increasing $\beta$ brings the two lowest poles closer together, until they become coincident and then split apart to become complex conjugate and move toward the imaginary axis (see the shaded root locus). Once on the imaginary axis, they result in sustained oscillation, and once they spill into the right half of the complex plane, they result in a growing oscillation.

Looking at Fig. 7.75, we observe that if we can tolerate the amounts of peaking and ringing that come with, say, $\phi_{m}=45^{\circ}$, then we must restrict operation to

TABLE 7.2 Poles of the closed-loop gain of the circuit of Fig. 7.73.

| $\boldsymbol{\beta}$ | $\boldsymbol{p}_{\mathbf{1}}\left(\mathbf{s}^{-1}\right)$ | $\boldsymbol{p}_{\mathbf{2}}\left(\mathbf{s}^{-1}\right)$ | $\boldsymbol{p}_{\mathbf{3}}\left(\mathbf{s}^{-1}\right)$ |
| :---: | :---: | :---: | :---: |
| 0 | $2 \pi(-1.0 \mathrm{k})$ | $2 \pi(-100 \mathrm{k})$ | $2 \pi(-10 \mathrm{M})$ |
| $10^{-5}$ | $2 \pi(-12.4 \mathrm{k})$ | $2 \pi(-88.5 \mathrm{k})$ | $2 \pi(-10 \mathrm{M})$ |
| $10^{-4}$ | $2 \pi(-50 \mathrm{k}+j 87.2 \mathrm{k})$ | $2 \pi(-50 \mathrm{k}-j 87.2 \mathrm{k})$ | $2 \pi(-10 \mathrm{M})$ |
| $10^{-3}$ | $2 \pi(-45.4 \mathrm{k}+j 313 \mathrm{k})$ | $2 \pi(-45.4 \mathrm{k}-j 313 \mathrm{k})$ | $2 \pi(-10.01 \mathrm{M})$ |
| $1.02 \times 10^{-2}$ | $2 \pi(0+1.0 \mathrm{M})$ | $2 \pi(0-1.0 \mathrm{M})$ | $2 \pi(-10.1 \mathrm{M})$ |
| $2 \times 10^{-2}$ | $2 \pi(46.7 \mathrm{k}+1.34 \mathrm{M})$ | $2 \pi(46.7 \mathrm{k}-1.34 \mathrm{M})$ | $2 \pi(-10.19 \mathrm{M})$ |

$1 / \beta \geq 10^{4} \mathrm{~V} / \mathrm{V}$. What if we want to operate the amplifier with lower closed-loop gains, such as $1 / \beta=50 \mathrm{~V} / \mathrm{V}$, or $1 / \beta=2 \mathrm{~V} / \mathrm{V}$ ? As is, the circuit will simply oscillate for these values of $\beta$ ! Mercifully, some clever frequency-compensation techniques have been developed that allow us to stabilize an amplifier for virtually any closedloop gain we wish, including what by now we recognize as the most difficult configuration to stabilize, namely, the voltage follower, for which $\beta=1$.

EXAMPLE 7.33 (a) What is the minimum allowable noise gain $1 / \beta$ if we want to operate the amplifier of Fig. 7.73 with a phase margin of $60^{\circ}$ ?
(b) Find $\left|D\left(f f_{x}\right)\right|$ and comment.
(c) Verify with PSpice.

#### Solution

(a) By Eq. (7.86) we have $\phi_{x}=\phi_{m}-180^{\circ}=60^{\circ}-180^{\circ}=-120^{\circ}$. Figure $7.74 a$ indicates that $f_{-120^{\circ}}$ occurs a bit below 100 kHz . Start out with the initial estimate $f_{-120^{\circ}}=50 \mathrm{kHz}$ and iterate using Eq. (7.89b) until you settle at $f_{-120^{\circ}}=$ 59.2 kHz . Next, use Eq. $(7.89 a)$ to find $\mid a\left(j f_{-120^{\circ}} \mid \cong 14,534 \mathrm{~V} / \mathrm{V}\right.$. This is the minimum value of $1 / \beta$ for $\phi_{m} \geq 60^{\circ}$ with this particular amplifier.
(b) Proceeding in the usual manner we get

$$
\left|D\left(j f_{x}\right)\right| \cong \frac{1}{\sqrt{2\left(1-\cos 60^{\circ}\right)}}=1
$$

Since $T_{0}=10^{6} / 14,534=68.8$, we also have $D_{0}=1 /(1+1 / 68.8)=0.986$, indicating a very small amount of peaking.
(c) Using the circuit of Fig. 7.73 with $\beta=1 / 14,534=68.8 \times 10^{-6} \mathrm{~V} / \mathrm{V}$ we get the plots of Fig. 7.77. It is fair to say that, aside for a slight amount of peaking and ringing, which is acceptable in many applications, the condition $\phi_{m}=60^{\circ}$ is almost as good as $\phi_{m}=90^{\circ}$ in terms of stability, yet it expands the range of possible closed-loop gains by decreasing the lower limit of acceptable values for $1 / \beta$ from $100,000 \mathrm{~V} / \mathrm{V}$ to $14,534 \mathrm{~V} / \mathrm{V}$, or by almost 17 dB .
image_name:(a)
description:The graph labeled (a) is a Bode plot, specifically depicting the frequency response of a system with a phase margin of \( \phi_{m}=60^{\circ} \).

Axes Labels and Units:
- **X-Axis:** Frequency \( f \) in Hertz (Hz), ranging from \( 10^2 \) to \( 10^7 \) Hz, on a logarithmic scale.
- **Y-Axis:** Gain \( \text{V/V} \), also on a logarithmic scale, ranging from \( 10^0 \) to \( 10^5 \).

Overall Behavior and Trends:
- The gain remains relatively constant at approximately \( 10^4 \) from \( 10^2 \) to about \( 10^5 \) Hz.
- Beyond \( 10^5 \) Hz, the gain begins to decrease, indicating a roll-off.
- The plot exhibits a slight peaking just before the roll-off begins, which is characteristic of systems with a phase margin of \( 60^{\circ} \).

Key Features and Technical Details:
- There is a noticeable peak in the gain just before the frequency reaches \( 10^5 \) Hz, which is typical for a phase margin of \( 60^{\circ} \).
- The gain starts to drop off significantly after this peak, indicating the cutoff frequency or the bandwidth limit of the system.

Annotations and Specific Data Points:
- Important markers on the frequency axis are at \( 10^3 \), \( 10^4 \), \( 10^5 \), and \( 10^6 \) Hz, which help in identifying the range over which the system maintains its gain and where it starts to decline.
- The gain peaking and subsequent roll-off are indicative of the system's stability characteristics and are relevant for assessing the range of acceptable closed-loop gains.
image_name:(b)
description:The graph labeled as "(b)" represents the step response of a system with a phase margin of \( \phi_{m} = 60^{\circ} \). This is a time-domain waveform.

1. **Axes Labels and Units:**
- The horizontal axis represents time in microseconds (\( \mu s \)). The scale is linear, ranging from 0 to 50 \( \mu s \).
- The vertical axis represents the output voltage \( v_o \) in volts (V). The scale is linear, ranging from 0 to 1.2 V.

2. **Overall Behavior and Trends:**
- The graph shows a rapid rise in voltage from 0 V, indicating the system's response to a step input.
- There is a noticeable overshoot where the voltage exceeds the final steady-state value.
- After the overshoot, the voltage exhibits slight oscillations (ringing) before settling at a steady-state value slightly below the peak.

3. **Key Features and Technical Details:**
- The peak of the overshoot occurs around 10 \( \mu s \), where the voltage reaches approximately 1.1 V.
- The waveform stabilizes around 1 V, indicating the steady-state output voltage.
- The presence of ringing is indicative of a typical underdamped response, which is consistent with a phase margin of 60 degrees.

4. **Annotations and Specific Data Points:**
- The initial rise and overshoot are key features, with the overshoot percentage being a critical parameter for assessing system performance.
- The system's response time and settling time can be inferred from the graph, though specific numerical values for these are not directly marked.

FIGURE 7.77 (a) Frequency and (b) step responses for the special case $\phi_{m}=60^{\circ}$.

### Peaking and Ringing as Functions of the Phase Margin $\boldsymbol{\phi}_{\boldsymbol{m}}$

Figure 7.78 depicts peaking and ringing by the circuit of Fig. 7.73 as functions of the phase margin $\phi_{m}$. These characteristics are quantified in terms of the gain peaking $G P$ and the overshoot $O S$, defined as

$$
\begin{equation*}
G P=20 \log _{10}\left|A_{p}-A_{0}\right| \quad O S(\%)=100 \frac{V_{p}-V_{\infty}}{V_{\infty}} \tag{7.91}
\end{equation*}
$$

Peaking occurs for $\phi_{m}$ less than about $65^{\circ}$, and ringing for $\phi_{m}$ less than about $75^{\circ}$.
image_name:Closed-loop gain A
description:The graph in Figure 7.78 illustrates the behavior of a closed-loop gain as a function of frequency, highlighting the concepts of peaking and ringing in relation to the phase margin \( \phi_{m} \). The graph is divided into two main sections: peaking and ringing, each with its own subplots.

Peaking (Figure 7.78a)
- **Type of Graph:** The upper left plot is a frequency response graph, showing the closed-loop gain \( A \) as a function of frequency.
- **Axes Labels and Units:**
- **X-axis:** Frequency (units not specified, typically hertz in similar contexts).
- **Y-axis:** Closed-loop gain \( A \), likely in decibels (dB).
- **Overall Behavior and Trends:**
- The gain starts at a baseline level \( A_0 \) and increases to a peak \( A_p \), indicating gain peaking.
- After reaching the peak, the gain decreases sharply.
- **Key Features and Technical Details:**
- **Gain Peaking (GP):** Defined as \( 20 \log_{10}|A_p - A_0| \), shown as the vertical distance between \( A_p \) and \( A_0 \).
- Peaking is significant for \( \phi_{m} \) less than about \( 65^{\circ} \).

Ringing (Figure 7.78b)
- **Type of Graph:** The upper right plot is a time-domain response showing the step response of the closed-loop system.
- **Axes Labels and Units:**
- **X-axis:** Time (units not specified, typically seconds or milliseconds).
- **Y-axis:** Closed-loop step response (likely in volts).
- **Overall Behavior and Trends:**
- The response shows an initial overshoot \( V_p \) above the final value \( V_\infty \), followed by oscillations that gradually settle.
- **Key Features and Technical Details:**
- **Overshoot (OS):** Defined as \( 100 \frac{V_p - V_\infty}{V_\infty} \), shown as the vertical distance between \( V_p \) and \( V_\infty \).
- Ringing is significant for \( \phi_{m} \) less than about \( 75^{\circ} \).

Additional Graphs
- **Gain Peaking vs. Phase Margin (Lower Left):**
- **X-axis:** Phase margin \( \phi_{m} \) in degrees.
- **Y-axis:** Gain peaking \( GP \) in decibels (dB).
- **Behavior:** A decreasing trend showing that gain peaking reduces as the phase margin increases.

- **Overshoot vs. Phase Margin (Lower Right):**
- **X-axis:** Phase margin \( \phi_{m} \) in degrees.
- **Y-axis:** Overshoot \( OS \) in percentage (%).
- **Behavior:** A decreasing trend indicating that overshoot diminishes as the phase margin increases.

These graphs collectively illustrate how the phase margin \( \phi_{m} \) affects the stability and performance of a closed-loop system, with specific emphasis on gain peaking and overshoot characteristics.
image_name:Closed-loop step response
description:The graph titled "Closed-loop step response" is a time-domain waveform illustrating the behavior of a system's response to a step input.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph showing the closed-loop step response of a system.

2. **Axes Labels and Units:**
- The horizontal axis represents time, although specific units are not labeled.
- The vertical axis represents the response amplitude, with reference levels indicated as \( V_p \) (peak amplitude) and \( V_\infty \) (steady-state amplitude).

3. **Overall Behavior and Trends:**
- The graph shows an initial rise in response, peaking at \( V_p \), followed by oscillations that gradually settle down to a steady-state level \( V_\infty \).
- The waveform exhibits overshoot and ringing, characteristic of underdamped systems.

4. **Key Features and Technical Details:**
- The overshoot \( OS \) is defined as the percentage by which the peak \( V_p \) exceeds the steady-state value \( V_\infty \).
- The waveform demonstrates typical underdamped behavior, with oscillations decreasing in amplitude over time.
- No specific numerical values for time or amplitude are given, but the qualitative behavior is clearly depicted.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for \( V_p \) and \( V_\infty \), indicating the peak and steady-state values.
- The overshoot \( OS \) is visually represented as the vertical difference between \( V_p \) and \( V_\infty \).
image_name:(a)
description:The graph labeled "(a)" is a plot of gain peaking (GP) as a function of phase margin (\(\phi_m\)).

Type of Graph and Function
This is a two-dimensional line graph representing the relationship between gain peaking and phase margin in a closed-loop system.

Axes Labels and Units
- **X-axis:** Phase margin \(\phi_m\) in degrees (°), ranging from 0° to 90°.
- **Y-axis:** Gain peaking \(GP\) in decibels (dB), ranging from 0 dB to 28 dB.

Overall Behavior and Trends
The graph shows a clear decreasing trend. As the phase margin \(\phi_m\) increases from 0° to 90°, the gain peaking \(GP\) decreases. This indicates that higher phase margins result in lower gain peaking.

Key Features and Technical Details
- At low phase margins (close to 0°), the gain peaking is high, reaching up to approximately 28 dB.
- As the phase margin increases, the gain peaking decreases sharply at first and then more gradually.
- Around a phase margin of 65°, the gain peaking falls below 5 dB, indicating reduced peaking.
- The graph approaches 0 dB gain peaking as the phase margin nears 90°.

Annotations and Specific Data Points
- The graph is marked with gridlines, aiding in the estimation of specific values.
- No specific data points or annotations are highlighted on the curve itself, but the trend is clear and continuous across the range of phase margins.
image_name:(b)
description:The graph labeled (b) is a plot depicting the relationship between overshoot (OS) in percentage and phase margin (φₘ) in degrees. This graph is a line plot where the x-axis represents the phase margin φₘ, ranging from 0° to 90°, and the y-axis represents the overshoot OS in percentage, ranging from 0% to 100%.

Type of Graph and Function:
This is a line graph showing how the overshoot in a control system's step response varies as a function of the phase margin.

Axes Labels and Units:
- **X-axis:** Phase margin φₘ in degrees (°), with a range from 0 to 90.
- **Y-axis:** Overshoot OS in percentage (%), with a range from 0 to 100.
- The graph uses a linear scale for both axes.

Overall Behavior and Trends:
The graph exhibits a decreasing trend, where the overshoot percentage diminishes as the phase margin increases. Initially, at lower phase margins, the overshoot is high, nearing 100%. As the phase margin increases, the overshoot decreases steadily.

Key Features and Technical Details:
- The curve starts at a high overshoot value near 100% when the phase margin is close to 0°.
- The overshoot decreases sharply as the phase margin increases from 0° to about 20°.
- Beyond 20°, the overshoot continues to decrease but at a slower rate.
- At a phase margin of around 75°, the overshoot approaches zero, indicating minimal ringing and peaking.

Annotations and Specific Data Points:
- The graph clearly shows that a phase margin of less than 75° is associated with noticeable overshoot, which aligns with the context provided that ringing occurs for phase margins below this threshold.
- No specific data points are annotated, but the overall trend is clear and consistent with theoretical expectations of control system behavior.

FIGURE 7.78 (a) Peaking and (b) ringing as functions of the phase margin $\phi_{m}$.

### Using PSpice to Plot $\boldsymbol{T}$ and to Measure $\boldsymbol{\phi}_{\boldsymbol{m}}$

The signal injection technique of Section 7.6 constitutes a powerful tool for the investigation of stability, especially when complex frequency responses need to be plotted and examined. The PSpice circuit of Fig. 7.79a uses the 741 macro-model, along with the voltage injection technique discussed in connection with Fig. 7.70, to generate the plots of $|T(j f)|$ and $\mathrm{ph} T(j f)$ for the case of a capacitively loaded 741 voltage buffer. The plots, shown in Fig. 7.79b, are obtained, respectively, as

$$
\begin{equation*}
|T(j f)|=\left|-\frac{V_{r}}{V_{f}}\right| \quad \text { ph } T(j f)=\operatorname{ph}\left(-\frac{V_{r}}{V_{f}}\right) \tag{7.92}
\end{equation*}
$$

Using the cursor facility of PSpice we find $f_{x}=864 \mathrm{kHz}$ and $\mathrm{ph} T\left(j f_{x}\right)=-124^{\circ}$, so $\phi_{m}=180-124=56^{\circ}$. Rerunning the simulation for the unloaded case ( $C_{L}=0$ and $\left.R_{L}=\infty\right)$ gives $f_{x}=888 \mathrm{kHz}$ and $\phi_{m}=62.8^{\circ}$, indicating that the present load erodes $\phi_{m}$ by $6.8^{\circ}$ (this is due to the high-frequency pole formed by $C_{L}$ with the output resistance $r_{o}$ of the op $\mathrm{amp}^{7}$ ).
image_name:(a)
description:
[
name: μA741, type: OpAmp, value: μA741, ports: {InP: GND, InN: Vf, OutP: Vr, OutN: GND, Vdd: VCC, -Vdd: VEE}
name: RL, type: Resistor, value: 2kΩ, ports: {N1: GND, N2: Vr}
name: CL, type: Capacitor, value: 0.5nF, ports: {Np: Vr, Nn: GND}
name: Vf, type: VoltageSource, value: 1mVac, ports: {Np: Vf, Nn: Vr}
]
extrainfo:The circuit is a voltage buffer using a μA741 operational amplifier with feedback. It includes a load resistor (RL) and a load capacitor (CL) connected at the output. The op-amp is powered by VCC = 10V and VEE = -10V. A small AC voltage (1mVac) is injected at the input.

(a)
image_name:Figure 7.79
description:The graph in Figure 7.79 is a Bode plot, which is used to analyze the frequency response of a system. It consists of two plots: one showing the loop gain \( T \) in decibels (dB) and the other showing the phase of \( T \) in degrees.

Axes Labels and Units:
- **X-axis:** Frequency \( f \) in hertz (Hz), ranging from 1 Hz to 10 million Hz (10^7 Hz) on a logarithmic scale.
- **Left Y-axis:** Loop gain \( T \) in decibels (dB), ranging from -40 dB to 100 dB.
- **Right Y-axis:** Phase of \( T \) in degrees, ranging from -150° to 0°.

Overall Behavior and Trends:
- **Loop Gain \( T \):**
- Starts high at around 100 dB at 1 Hz.
- Decreases steadily with increasing frequency, showing a downward slope.
- The slope becomes steeper after approximately 10^3 Hz.
- Continues to decrease until it reaches below 0 dB around 10^6 Hz.

- **Phase of \( T \):**
- Begins near 0° at low frequencies.
- Decreases gradually, showing a downward slope.
- The phase becomes more negative, reaching approximately -150° at around 10^7 Hz.

Key Features and Technical Details:
- **Cutoff Frequency:** The point where the gain drops to 0 dB is a critical frequency, indicating the bandwidth limit of the system.
- **Phase Margin:** The phase margin can be inferred from the phase plot where the gain crosses 0 dB. This is crucial for determining the stability of the system.

Annotations and Specific Data Points:
- The plot is annotated with the labels \( T \) for the gain plot and \( \angle T \) for the phase plot.
- The gridlines help in identifying key frequency points and corresponding gain and phase values.

(b)

FIGURE 7.79 Using the voltage injection technique to find the phase margin of a capacitively loaded 741 voltage buffer.

## 7.8 DOMINANT-POLE COMPENSATION

If a negative-feedback system fails to meet the desired degree of stability, its loop gain $T(j f)$ must be altered in such a way as to raise the phase margin $\phi_{m}$ to an acceptable value. Altering $T(j f)$ to stabilize a circuit is referred to as frequency compensation. Since $T(j f)=a(j f) \beta(j f)$, we can alter $T(j f)$ by altering $a(j f)$, or $\beta(j f)$, or both. Here we take the viewpoint of the IC designer, who strives to ensure a given $\phi_{m}$ for the hardest-to-compensate configuration with frequency-independent feedback, namely, the voltage-follower, for which $\beta=1 \mathrm{~V} / \mathrm{V}$. In this particular case we have

$$
\begin{equation*}
T(j f)=a(j f) \beta=a(j f) \times 1=a(j f) \tag{7.93}
\end{equation*}
$$

that is, $T(j f)$ coincides with $a(j f)$. If the op amp utilizes frequency-dependent feedback, then it may be necessary for the user to take additional measures ${ }^{7}$ to stabilize it (see also the end-of-chapter problems).

A popular compensation technique involves lowering the first pole frequency $f_{1}$ to a new value $f_{D}$ such that the compensated response is dominated by this lone pole all the way up to the crossover frequency $f_{x}$, which, for $\beta=1 \mathrm{~V} / \mathrm{V}$, coincides with the already-familiar transition frequency $f_{t}$. The phase shift at $f_{x}$ is then $\phi_{x}=-90^{\circ}+$ $\phi_{x(\mathrm{HOR})}$, where $-90^{\circ}$ is the phase shift due to $f_{D}$, and $\phi_{x(\mathrm{HOR})}$ is the combined phase shift due to the higher-order roots (poles and possibly zeros) at $f_{x}$. (For instance, the loaded 741 op amp of Fig. 7.79 has $\phi_{x(\mathrm{HOR})}=90^{\circ}+\phi_{x}=90^{\circ}-124^{\circ}=-34^{\circ}$.) The phase margin after compensation is $\phi_{m}=180^{\circ}+\phi_{x}=180^{\circ}-90^{\circ}+\phi_{x(\mathrm{HOR})}$, that is,

$$
\begin{equation*}
\phi_{m}=90^{\circ}+\phi_{x(\mathrm{HOR})} \tag{7.94}
\end{equation*}
$$

By making $f_{D}$ sufficiently low, we can keep $\phi_{x(\mathrm{HOR})}$ as small as needed. For instance, for $\phi_{m} \geq 60^{\circ}$ we need to ensure $\phi_{x(\text { HOR })} \geq-30^{\circ}$. An obvious drawback of dominantpole compensation is a drastic gain reduction above $f_{D}$, but this is the price we must pay for the sake of stability. Though there are other, more sophisticated techniques ${ }^{7}$ that preserve gain over a wider portion of the frequency spectrum, here we limit ourselves to the dominant-pole types. Two popular techniques for shifting $f_{1}$ to $f_{D}\left(\ll f_{1}\right)$ are the shunt-capacitance technique and the Miller-compensation technique.

### Shunt-Capacitance Compensation

A simple technique for lowering a pole frequency $f_{1}$ is to deliberately increase the capacitance of the node responsible for $f_{1}$ itself. In the case of the 3-pole amplifier example of the previous section we simply add a shunt capacitance $C_{\text {shunt }}$ in parallel with $C_{1}$ to lower its pole frequency from $f_{1}=1 /\left(2 \pi R_{1} C_{1}\right)$ to

$$
\begin{equation*}
f_{D}=\frac{1}{2 \pi R_{1}\left(C_{1}+C_{\text {shunt }}\right)} \tag{7.95}
\end{equation*}
$$

To visualize the required location of $f_{D}$, refer to the linearized plot of Fig. 7.80 and proceed as follows:

- Identify the frequency $f_{x}$ at which the phase of $a(j f)$ is $\phi_{x}=\phi_{m}-180^{\circ}$, where $\phi_{m}$ is the desired phase margin (e.g. $45^{\circ}, 60^{\circ}$, etc.) This is going to be the transition frequency $f_{t}$ after compensation. (We can read out $\phi_{x}$ from the phase plot of $a(j f)$, if available, or from slope readings on the magnitude plot of $a(\mathrm{ff})$, in the manner illustrated in Fig. 7.74b.)
- Starting at $f_{x}$ on the $0-\mathrm{dB}$ axis of the decibel plot of $|a(j f)|$, draw a line with a slope of $-20 \mathrm{~dB} / \mathrm{dec}$ till it intersects the $a_{0}$ curve. The corresponding frequency is going to be $f_{D}$. Exploiting the constancy of the gain-bandwidth product, we write $a_{0} \times f_{D}=1 \times f_{x}$, which allows us to calculate the new pole location as

$$
\begin{equation*}
f_{D}=\frac{f_{x}}{a_{0}} \tag{7.96}
\end{equation*}
$$

image_name:FIGURE 7.80
description:The graph in FIGURE 7.80 is a Bode plot illustrating the open-loop gain \( a(jf) \) of a system with respect to frequency \( f \). The vertical axis represents the open-loop gain \( a \) in decibels (dB), while the horizontal axis represents the frequency \( f \), typically in hertz (Hz). The plot is logarithmic on the frequency axis.

Overall Behavior and Trends:
- The plot begins with a horizontal line at a gain level of \( a_0 \) dB, indicating a constant gain over a range of frequencies.
- At frequency \( f_1 \), the gain starts to decrease linearly with a slope of \(-20 \) dB/decade, reflecting a first-order roll-off typical of a single-pole system.
- The slope continues until it reaches frequency \( f_x \), where further poles cause the slope to steepen.
- The shaded curve indicates the gain before compensation, which begins to drop before \( f_1 \) and at a steeper rate.

Key Features and Technical Details:
- **\( f_D \):** The dominant pole frequency is marked where the initial constant gain line intersects the line with \(-20 \) dB/decade slope. This is calculated as \( f_D = \frac{f_x}{a_0} \).
- **\( f_1, f_2, f_3 \):** These are critical frequencies where significant changes in slope occur due to additional poles. \( f_2 \) and \( f_3 \) are marked with vertical dashed lines.
- **\( \phi_x = \phi_m - 180^\circ \):** This annotation indicates the phase margin at frequency \( f_x \), which is a crucial parameter for stability analysis.

Annotations and Specific Data Points:
- The phase margin \( \phi_x \) is annotated at the frequency \( f_x \), providing a reference for the stability of the system.
- The shaded area shows the gain before compensation, emphasizing the impact of shunt-capacitance compensation in improving system performance.

This graphical method effectively illustrates how the dominant pole \( f_D \) is located and highlights the impact of compensation techniques on the system's gain behavior.

FIGURE 7.80 Graphical method for locating the dominant pole $f_{D}$ for the case of shuntcapacitance compensation (the shaded curve shows gain before compensation).

If the first two poles are widely spaced, and any higher-order root frequencies (such as $f_{3}$ in our example) are sufficiently high, a graphically and computationally convenient starting point is $\phi_{x}=-135^{\circ}$, for then $f_{x}=f_{2}$, giving $f_{D}=f_{2} / a_{0}$. The corresponding phase margin is only $45^{\circ}$, but we can always lower $f_{D}$ further to increase $\phi_{m}$, for instance to $60^{\circ}$, which Example 7.33 has demonstrated to be often adequate.

EXAMPLE 7.34 (a) Find the capacitance $C_{\text {shunt }}$ that will stabilize the amplifier of Fig. 7.72 for $\phi_{m}=45^{\circ}$ when used with $\beta=1$. Verify with PSpice.
(b) To what value must we increase $C_{\text {shunt }}$ if we want to achieve $\phi_{m}=60^{\circ}$ ?

#### Solution

(a) Letting $f_{x}=f_{2}=100 \mathrm{kHz}$ and $a_{0}=10^{6} \mathrm{~V} / \mathrm{V}$ in Eq. (7.96) gives $f_{D}=10^{5} / 10^{6}=$ 0.1 Hz. By Eq. (7.95),

$$
C_{\text {shunt }}=\frac{1}{2 \pi R_{1} f_{D}}-C_{1}=\frac{1}{2 \pi 10^{7} \times 0.1}-15.9 \times 10^{-12}=159.1 \mathrm{nF}
$$

Using the PSpice circuit of Fig. 7.81 we get the curves of Fig. 7.82, which show unequivocally the large amount of gain that needs to be sacrificed for the sake of shunt-capacitance stabilization. But it is better to have a stable circuit with sacrificed gain than an unstable one!
image_name:FIGURE 7.81
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: Gm1, type: VoltageControlledCurrentSource, value: 100 μA/V, ports: {Np: Gm1, Nn: GND}
name: R1, type: Resistor, value: 10 MΩ, ports: {N1: Vi, N2: GND}
name: C1, type: Capacitor, value: 15.92 pF, ports: {Np: V1, Nn: GND}
name: Cshunt, type: Capacitor, value: 159.1 nF, ports: {Np: V1, Nn: GND}
name: Gm2, type: VoltageControlledCurrentSource, value: 10 mA/V, ports: {Np: V1, Nn: GND}
name: R2, type: Resistor, value: 100 kΩ, ports: {N1: V2, N2: GND}
name: C2, type: Capacitor, value: 15.92 pF, ports: {Np: V2, Nn: GND}
name: E3, type: VoltageControlledVoltageSource, value: 1 V/V, ports: {Np: V2, Nn: GND}
name: R3, type: Resistor, value: 1.0 kΩ, ports: {N1: V2, N2: Vo}
name: C3, type: Capacitor, value: 15.92 pF, ports: {Np: Vo, Nn: GND}
]
extrainfo:This is a three-pole amplifier circuit with shunt-capacitance compensation. It includes two voltage-controlled current sources (Gm1 and Gm2) and a voltage-controlled voltage source (E3). The circuit is designed to stabilize the amplifier with shunt capacitance, sacrificing gain for stability.

FIGURE 7.81 Three-pole amplifier with shunt-capacitance compensation.
(b) For $\phi_{m}=60^{\circ}$ the crossover must be placed at the frequency $f_{x}$ where $\phi_{x}=$ $\phi_{m}-180^{\circ}=60^{\circ}-180^{\circ}=-120^{\circ}$. Example 7.33 indicated that $f_{x}=$ 59.2 kHz , so Eq. (7.96) gives $f_{D}=0.0592 \mathrm{~Hz}$, and Eq. (7.95) gives $C_{\text {shunt }} \cong$ 269 nF . Re-running PSpice with $C_{\text {shunt }}=269 \mathrm{nF}$ and using the cursor facility, we measure $f_{x}=59.4 \mathrm{kHz}$ and $\phi_{x}=-118^{\circ}$, in fairly good agreement with the predicted values.
image_name:FIGURE 7.82
description:The graph in FIGURE 7.82 consists of two Bode plots, showing both the magnitude and phase response of an open-loop gain with shunt capacitance compensation.

1. **Type of Graph and Function:**
- The graph is a Bode plot, which includes two separate plots: one for magnitude (gain) and another for phase.

2. **Axes Labels and Units:**
- **Magnitude Plot:**
- **Y-Axis:** Open-loop gain \( a \) in decibels (dB), ranging from -20 dB to 120 dB.
- **X-Axis:** Frequency \( f \) in Hertz (Hz), presented on a logarithmic scale from 0.01 Hz to 1 MHz.
- **Phase Plot:**
- **Y-Axis:** Phase of \( a \) in degrees, ranging from -180° to 0°.
- **X-Axis:** Frequency \( f \) in Hertz (Hz), also on a logarithmic scale from 0.01 Hz to 1 MHz.

3. **Overall Behavior and Trends:**
- **Magnitude Plot:**
- The gain starts high at low frequencies (around 120 dB) and decreases linearly on the logarithmic scale, indicating a typical roll-off characteristic of a low-pass filter.
- The gain crosses 0 dB near the frequency of 100 kHz.
- **Phase Plot:**
- The phase starts near 0° at low frequencies and decreases, approaching -180° as the frequency increases.
- There is a noticeable phase shift occurring around the 100 kHz mark.

4. **Key Features and Technical Details:**
- The crossover frequency \( f_x \) where the gain is 0 dB occurs around 100 kHz.
- The phase margin is indicated by the phase angle at the crossover frequency, which is approximately -120° as noted in the context.
- The shaded curves in both plots represent the response before compensation (when \( C_{\text{shunt}} = 0 \)), showing a higher gain and less phase shift at higher frequencies compared to the compensated response.

5. **Annotations and Specific Data Points:**
- The plots include gridlines that help in identifying specific frequencies and gain/phase values.
- The compensated response (solid line) shows improved stability with reduced gain and a more gradual phase shift as compared to the shaded pre-compensation response.

FIGURE 7.82 Magnitude and phase plots with shuntcapacitance compensation for $\phi_{m}=45^{\circ}$. The shaded curves show the response before compensation ( $C_{\text {shunt }}=0$ ).

### Miller Compensation

The low value required of $f_{D}$ for dominant-pole compensation results in a relatively large $C_{\text {shunt }}$. This may not necessarily be a problem if $C_{\text {shunt }}$ is a discrete capacitor external to the op amp. However, in integrated circuits it is desirable to fabricate the compensation circuitry directly on chip, and capacitors higher than a few tens of picofarads would take up too much chip area. A clever way around this limitation is to start out with a small enough capacitance $C_{f}$ that can be fabricated on chip, and then use the Miller effect to make it appear as large as needed for frequency compensation. We shall see that two additional benefits accrue from this scheme, namely, pole splitting as well as higher slew rates.
image_name:FIGURE 7.83
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: Gm1Vi, type: VoltageControlledCurrentSource, ports: {Np: Vi, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vi1, N2: V1}
name: C1, type: Capacitor, value: C1, ports: {Np: V1, Nn: GND}
name: Cf, type: Capacitor, value: Cf, ports: {Np: V1, Nn: Vo}
name: Gm2, type: VoltageControlledCurrentSource, ports: {Np: Vo, Nn: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vo, N2: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: Vo, Nn: GND}
]
extrainfo:The circuit is a two-pole amplifier with Miller compensation. It uses the Miller effect to increase apparent capacitance for frequency compensation, achieving pole splitting and higher slew rates.

FIGURE 7.83 Two-pole amplifier with Miller compensation.

In order to focus on the essentials of Miller compensation, let us first investigate the two-pole amplifier of Fig. 7.83, which, in the absence of $C_{f}$, exhibits the pole frequencies

$$
\begin{equation*}
f_{1}=\frac{1}{2 \pi R_{1} C_{1}} \quad f_{2}=\frac{1}{2 \pi R_{2} C_{2}} \tag{7.97}
\end{equation*}
$$

With $C_{f}$ present, the circuit resembles that of Fig. 6.21 (one is readily obtained from the other via a mere source transformation at the input). Adapting Eqs. (6.45) and (6.46) to the present circuit, we find that the presence of $C_{f}$ results in a new polefrequency pair

$$
\begin{gathered}
f_{1(\mathrm{new})}=\frac{1 / 2 \pi}{R_{1}\left[C_{1}+C_{f}\left(1+G_{m 2} R_{2}+R_{2} / R_{1}\right)\right]+R_{2} C_{2}} \\
f_{2(\mathrm{new})}=\frac{1 / 2 \pi}{R_{1} R_{2}\left(C_{1} C_{f}+C_{1} C_{2}+C_{f} C_{2}\right) 2 \pi f_{1(\mathrm{new})}}
\end{gathered}
$$

Anticipating $f_{1 \text { (new) }} \ll f_{1}$, we recognize that the denominator of $f_{1 \text { (new) }}$ must be dominated by the term $R_{1} C_{f} G_{m 2} R_{2}$, so we simplify as $f_{1 \text { (new) }} \cong 1 /\left(2 \pi R_{1} C_{f} G_{m 2} R_{2}\right)=$ $1 /\left(2 \pi R_{1} C_{1} G_{m 2} R_{2} C_{f} / C_{1}\right)$. Using Eq. (7.97), along with straightforward algebra, we express the new pole pair in the more insightful form

$$
\begin{equation*}
f_{1(\mathrm{new})} \cong \frac{f_{1}}{\left(G_{m 2} R_{2} C_{f}\right) / C_{1}} \quad f_{2(\text { (new })} \cong \frac{\left(G_{m 2} R_{2} C_{f}\right) f_{2}}{C_{1}+C_{f}\left(1+C_{1} / C_{2}\right)} \tag{7.98}
\end{equation*}
$$

Since $f_{1}$ is divided by $G_{m 2} R_{2} C_{f}$ whereas $f_{2}$ is multiplied by the same term, we conclude that increasing $C_{f}$ moves the first pole down in frequency and the second pole up in frequency, a phenomenon aptly called pole splitting. Depicted in Fig. 7.84, pole splitting is highly beneficial because it pushes the second pole and its phase lag up in frequency, making the placement of the dominant pole less stringent compared to shunt-capacitance compensation.

Recall from Eq. (6.43) that the presence of $C_{f}$ results also in the creation of a right-half-plane (RHP) zero at $s=G_{m 2} / C_{f}$. Noting that the dc gain in Fig. 7.83 is $a_{0}=\left(-G_{m 1} R_{1}\right) \times\left(-G_{m 2} R_{2}\right)$, we summarize by stating that with Miller compensation gain takes on the form

$$
\begin{equation*}
a(j f)=a_{0} \frac{1-j f / f_{0}}{\left(1+j f / f_{1 \text { (new) })}\right)\left(1+j f / f_{2(\text { new })}\right)} \tag{7.99}
\end{equation*}
$$

image_name:FIGURE 7.84
description:The graph in FIGURE 7.84 is a Bode plot that illustrates the open-loop gain \(a\) of a two-pole amplifier with respect to frequency \(f\). The vertical axis represents the open-loop gain \(a\) in decibels (dB), while the horizontal axis represents the frequency \(f\) in unspecified units, typically hertz (Hz) for such plots. The graph uses a logarithmic scale for the frequency axis, which is common in Bode plots to cover a wide range of frequencies.

Overall Behavior and Trends:
The graph shows two curves: a shaded curve representing the gain before compensation and a solid black curve representing the gain after Miller compensation. The initial gain level at low frequencies is denoted as \(a_0\).

- **Before Compensation (Shaded Curve):**
- The gain is flat at \(a_0\) until the first pole at frequency \(f_1\), after which it begins to decrease at a certain slope.
- The slope changes further at another frequency \(f_2\), indicating a second pole.

- **After Compensation (Solid Black Curve):**
- The gain is initially flat at \(a_0\) until the new first pole at \(f_{1(\text{new})}\), where it starts decreasing.
- The slope of the gain reduction is steeper after \(f_{2(\text{new})}\), reflecting the effect of pole splitting.
- The gain continues to decrease past the frequency \(f_0\), where the right-half-plane zero is introduced due to the Miller compensation.

Key Features and Technical Details:
- **Critical Frequencies:**
- \(f_{1(\text{new})}\): The new first pole frequency after compensation.
- \(f_1\): The original first pole frequency before compensation.
- \(f_2\): The original second pole frequency before compensation.
- \(f_{2(\text{new})}\): The new second pole frequency after compensation.
- \(f_0\): The frequency where the RHP zero is introduced.

- **Gain Levels:**
- The initial gain level \(a_0\) is the DC gain of the amplifier before any frequency-dependent effects take place.

Annotations and Specific Data Points:
- The graph includes annotations for \(f_{1(\text{new})}\), \(f_1\), \(f_2\), \(f_{2(\text{new})}\), and \(f_0\), marking the key frequencies where the behavior of the gain changes.
- The transition points and slopes are indicative of the pole and zero effects on the amplifier's frequency response, with Miller compensation causing the poles to split and introducing a zero that affects the high-frequency behavior.

FIGURE $\mathbf{7 . 8 4}$ Miller compensation and pole splitting for the two-pole amplifier of Fig. 7.83 (the shaded curve shows the gain before compensation).
where

$$
\begin{gather*}
a_{0}=G_{m 1} R_{1} G_{m 2} R_{2} \quad f_{0}=\frac{G_{m 2}}{2 \pi C_{f}}  \tag{7.100}\\
f_{1 \text { (new) }} \cong \frac{1 / 2 \pi}{R_{1}\left[C_{1}+C_{f}\left(1+G_{m 2} R_{2}+R_{2} / R_{1}\right)\right]+R_{2} C_{2}} \cong \frac{1}{2 \pi R_{1} G_{m 2} R_{2} C_{f}}  \tag{7.101}\\
f_{2(\text { new })} \cong \frac{G_{m 2} / 2 \pi}{C_{1}+C_{2}\left(1+C_{1} / C_{f}\right)}
\end{gather*}
$$

Also, the gain-bandwidth product after compensation is GBP $=a_{0} \times f_{1 \text { (new) }}$. Combining Eqs. (7.100) and (7.101), we readily find

$$
\begin{equation*}
\mathrm{GBP} \cong \frac{G_{m 1}}{2 \pi C_{f}} \tag{7.103}
\end{equation*}
$$

Magnitude and phase are readily found as

$$
\begin{gather*}
|a(j f)|=a_{0} \sqrt{\frac{1+\left(f / f_{0}\right)^{2}}{\left[1+\left(f / f_{1 \text { (new })}\right)^{2}\right]\left[1+\left(f / f_{2 \text { (new) }}\right)^{2}\right]}}  \tag{7.104a}\\
\operatorname{ph} a(j f)=-\tan ^{-1}\left(f / f_{0}\right)-\tan ^{-1}\left(f / f_{1 \text { (new })}\right)-\tan ^{-1}\left(f / f_{2 \text { (new) }}\right) \tag{7.104b}
\end{gather*}
$$

Remark: Note that a RHP zero contributes phase lag, just like a pole in the left half plane! (As we shall see, this can be an issue in two-stage CMOS op amps.)

Pole splitting is readily visualized via PSpice. The circuit of Fig 7.85 utilizes only the first two stages of our three-pole working example to show how
image_name:FIGURE 7.85
description:
[
name: vi, type: VoltageSource, value: vi, ports: {Np: Vi, Nn: GND}
name: Gm1, type: VoltageControlledCurrentSource, value: 100 μA/V, ports: {Np: Vi, Nn: GND}
name: R1, type: Resistor, value: 10 MΩ, ports: {N1: V1, N2: GND}
name: C1, type: Capacitor, value: 15.92 pF, ports: {Np: V1, Nn: GND}
name: Cf, type: Capacitor, value: Cf, ports: {Np: V1, Nn: Vo}
name: Gm2, type: VoltageControlledCurrentSource, value: 10 mA/V, ports: {Np: V1, Nn: GND}
name: R2, type: Resistor, value: 100 kΩ, ports: {N1: Vo, N2: GND}
name: C2, type: Capacitor, value: 15.92 pF, ports: {Np: Vo, Nn: GND}
]
extrainfo:The circuit is a two-stage amplifier demonstrating pole splitting. The voltage source 'vi' provides input to a voltage-controlled current source 'Gm1' with a transconductance of 100 μA/V. The first stage includes a resistor 'R1' and capacitor 'C1', forming a high-pass filter. The second stage consists of another voltage-controlled current source 'Gm2' with a transconductance of 10 mA/V, a feedback capacitor 'Cf', and a parallel RC network 'R2' and 'C2'. The circuit illustrates how increasing 'Cf' causes the poles to split apart, affecting the phase shift.

FIGURE 7.85 Using the first two stages of the amplifier of Fig. 7.81
to investigate pole splitting.
increasing $C_{f}$ causes the poles to split apart from their initial values $f_{1}=1 \mathrm{kHz}$ and $f_{2}=100 \mathrm{kHz}$ (see Fig. 7.86). The phase plot indicates that the maximum phase shift before compensation is $-180^{\circ}$ (with each pole contributing a maximum of $-90^{\circ}$ ), but after compensation it becomes $-270^{\circ}$ because of the additional $-90^{\circ}$ phase lag due to the RHP zero.
image_name:FIGURE 7.86
description:The graph in FIGURE 7.86 consists of two Bode plots: the top plot shows the open-loop gain \( a \) in decibels (dB) versus frequency in hertz (Hz), while the bottom plot displays the phase of \( a \) in degrees versus frequency in hertz (Hz). Both plots use a logarithmic scale for the frequency axis, ranging from 0.01 Hz to 10 GHz.

Top Plot: Open-Loop Gain
- **Axes:**
- **Y-axis:** Open-loop gain \( a \) in decibels (dB), ranging from -120 dB to 120 dB.
- **X-axis:** Frequency \( f \) in hertz (Hz), logarithmic scale from 0.01 Hz to 10 GHz.
- **Behavior:**
- The gain decreases with increasing frequency.
- Multiple curves are shown, indicating different values of feedback capacitance \( C_f \).
- The gray curve represents the response before compensation (\( C_f = 0 \)), while the black curves show the response with increasing \( C_f \).
- As \( C_f \) increases, the gain decreases more gradually at lower frequencies, indicating pole splitting.

Bottom Plot: Phase
- **Axes:**
- **Y-axis:** Phase of \( a \) in degrees, ranging from 0° to -270°.
- **X-axis:** Frequency \( f \) in hertz (Hz), logarithmic scale from 0.01 Hz to 10 GHz.
- **Behavior:**
- The phase decreases with increasing frequency.
- Multiple curves are shown, similar to the gain plot, representing different values of \( C_f \).
- The gray curve shows the phase response before compensation (\( C_f = 0 \)), and the black curves illustrate the effect of increasing \( C_f \).
- As \( C_f \) increases, the phase shift extends further negative, reaching up to -270° due to the right-half-plane (RHP) zero.

Key Features and Observations:
- **Pole Splitting:** As \( C_f \) increases, the poles split, lowering the initial pole frequency \( f_1 \) from 1 kHz to as low as 1 Hz, as indicated by the changing curves.
- **Phase Shift:** The maximum phase shift increases from -180° before compensation to -270° after compensation, due to the additional -90° phase lag introduced by the RHP zero.
- **Trend:** Increasing \( C_f \) causes both gain and phase curves to flatten, indicating a more stable system with extended bandwidth at the cost of reduced high-frequency gain.

FIGURE 7.86 Pole splitting as a function of $C_{f}$ for the two-stage amplifier of Fig. 7.85. The values used are $C_{f}=0.143 \mathrm{pF}, 1.59 \mathrm{pF}$, and 15.9 pF , which lower $f_{1}$ from 1 kHz to $f_{1 \text { (new) }}=100 \mathrm{~Hz}, 10 \mathrm{~Hz}$, and 1 Hz , respectively. The gray curves show the response before compensation ( $C_{f}=0$ ).

EXAMPLE 7.35 (a) Estimate the pole and zero frequencies of the two-stage amplifier of Fig. 7.85 if $C_{f}=5 \mathrm{pF}$.
(b) Estimate $C_{f}$ for a phase margin of $60^{\circ}$.
(c) Verify part (b) with PSpice and comment.

#### Solution

(a) By Eq. (7.100) we have $f_{0}=10^{-2} /\left(2 \pi \times 5 \times 10^{-12}\right)=318 \mathrm{MHz}$. Moreover, using $G_{m 2} R_{2}=10^{3}$, we calculate Eq. (7.98) as

$$
\begin{aligned}
f_{1(\text { new })} & \cong \frac{10^{3}}{10^{3} \times 5 / 15.92}=3.18 \mathrm{~Hz} \\
f_{2(\text { new })} & \cong \frac{10^{3} \times 5 \times 10^{5}}{16.92+5(1+15.92 / 15.92)}=18.6 \mathrm{MHz}
\end{aligned}
$$

It is apparent that the first pole has moved down from 1 kHz to 3.18 Hz , whereas the second pole has moved $u p$ from 100 kHz to 18.6 MHz . Moreover, $f_{0} \gg f_{2 \text { (new) }}$.
(b) By Eq. (7.94) the combined phase shift at $f_{x}$ due to $f_{2(\text { new) }}$ and $f_{0}$ must be $\phi_{x(\mathrm{HOR})}=\phi_{m}-90^{\circ}=60^{\circ}-90^{\circ}=-30^{\circ}$. Since in this particular example $f_{0}$ is so high, we can ignore its phase contribution at $f_{x}$ and impose $-30^{\circ}=$ $-\tan ^{-1}\left[f_{x} / f_{2 \text { (new) }}\right]$, which gives $f_{x}=\left(\tan 30^{\circ}\right) \times f_{2 \text { (new) }}=0.577 \times f_{2 \text { (new) }}$. Exploiting the constancy of the gain-bandwidth product we write

$$
a_{0} \times f_{1(\text { new })}=1 \times f_{x}=0.577 \times f_{2 \text { (new) }}
$$

Using Eqs. (7.102) and (7.103) we express this as

$$
\frac{G_{m 1}}{2 \pi C_{f}}=0.577 \times \frac{G_{m 2} / 2 \pi}{C_{1}+C_{2}\left(1+C_{1} / C_{f}\right)}
$$

Substituting the given values of $G_{m 1}, G_{m 2}, C_{1}$, and $C_{2}$, and solving for $C_{f}$ finally gives $C_{f}=2.388$ pF. Plugging into Eqs. (7.101) and (7.102) we get $f_{1 \text { (new) }}=$ 6.66 Hz and $f_{2 \text { (new) }}=11.54 \mathrm{MHz}$, so $f_{x}=0.577 \times 11.54=6.66 \mathrm{MHz}$.
(c) Running the PSpice circuit of Fig. 7.85 with $C_{f}=2.388 \mathrm{pF}$ gives $f_{x} \cong$ 5.9 MHz and $\phi_{m} \cong 62^{\circ}$. Considering all the approximations made, the calculated values are in reasonable agreement with PSpice.

Turning to the full-blown three-pole amplifier of Fig. 7.81 we observe that the phase lag due to $f_{3}$ will erode the phase margin calculated for the two-pole version of Fig. 7.85, so $C_{f}$ will have to be increased slightly if the same phase margin is to be retained. In particular, we use PSpice to find empirically that with $C_{f}=4.7 \mathrm{pF}$ the three-pole amplifier of Fig. 7.81 exhibits $f_{x} \cong 3.2 \mathrm{MHz}$ and $\phi_{m} \cong 62^{\circ}$.

### Shunt-Capacitance and Miller Compensation Comparison

We wish to compare the shunt-capacitance and the Miller compensation schemes for the case of the three-pole amplifier operated with $\beta=1$ and $\phi_{m} \cong 60^{\circ}$. Running the PSpice circuit of Fig. 7.87, first with $C_{\text {shunt }}=269 \mathrm{nF}$ (and $C_{f}=0$ ), and then with $C_{f}=4.7 \mathrm{pF}$ (and $C_{\text {shunt }}=0$ ), we obtain the closed-loop frequency and step responses of Fig. 7.88. It is apparent that the Miller scheme results in much faster dynamics, thanks to the pole splitting effect, which pushes the second pole toward higher frequencies, thus relaxing the constraints on the dominant pole location. Also, the
image_name:FIGURE 7.87
description:
[
name: vi, type: VoltageSource, ports: {Np: Vi, Nn: GND}
name: 100μA/V, type: VoltageControlledCurrentSource, value: 100μA/V, ports: {Np: Vi, Nn: Vo}
name: R1, type: Resistor, value: 10MΩ, ports: {N1: V1, N2: GND}
name: C1, type: Capacitor, value: 15.92pF, ports: {Np: V1, Nn: GND}
name: Cshunt, type: Capacitor, value: 269nF, ports: {Np: V1, Nn: GND}
name: Gm2, type: VoltageControlledCurrentSource, value: 10mA/V, ports: {Np: V1, Nn: GND}
name: Cf, type: Capacitor, value: 4.7pF, ports: {Np: V1, Nn: V2}
name: R2, type: Resistor, value: 100kΩ, ports: {N1: V2, N2: GND}
name: C2, type: Capacitor, value: 15.92pF, ports: {Np: V2, Nn: GND}
name: E3, type: VoltageControlledVoltageSource, value: 1V/V, ports: {Np: V2, Nn: GND}
name: R3, type: Resistor, value: 1.0kΩ, ports: {N1: V2, N2: Vo}
name: C3, type: Capacitor, value: 15.92pF, ports: {Np: Vo, Nn: GND}
]
extrainfo:The circuit compares the shunt-capacitance and Miller compensation schemes. It includes a voltage source, resistors, capacitors, a voltage-controlled current source, and a voltage-controlled voltage source. The Miller scheme allows for smaller compensation capacitors, beneficial for on-chip fabrication.

FIGURE 7.87 PSpice circuit to compare the shunt-capacitance and the Miller compensation schemes for the case $\beta=1$ and $\phi_{m} \cong 60^{\circ}$.

Miller-multiplication effect allows for $C_{f}$ to be much smaller than $C_{\text {shunt }}$ so it can be fabricated on chip. Finally, not immediately apparent from the amplifier model used above, is the fact that the slew rate SR is likely to be much higher with the Miller compensation scheme as the much smaller $C_{f}$ can get charged/discharged much more rapidly.
image_name:(a)
description:The graph labeled (a) is a Bode plot illustrating the closed-loop gain of a unity-gain amplifier as a function of frequency. The x-axis represents the frequency \( f \) in hertz (Hz) on a logarithmic scale, ranging from \( 10^3 \) to \( 10^7 \) Hz. The y-axis shows the closed-loop gain in decibels (dB), ranging from -5 dB to 0 dB.

Two curves are depicted: one for the Shunt compensation scheme and another for the Miller compensation scheme. Both curves start at 0 dB gain at low frequencies. The Shunt compensation curve begins to roll off around \( 10^5 \) Hz and drops sharply beyond this frequency. In contrast, the Miller compensation curve maintains a flat response until a higher frequency, indicating a wider bandwidth compared to the Shunt scheme.

Key features include the point where the Shunt curve begins to decline significantly, marking its cutoff frequency, and the Miller curve maintaining stability over a broader frequency range. This illustrates the Miller compensation's effectiveness in extending the bandwidth of the amplifier.
image_name:(b)
description:The graph labeled as "(b)" is a time-domain waveform representing the step response of a unity-gain amplifier. The x-axis is labeled "Time" and is measured in microseconds (µs), ranging from 0 to 15 µs. The y-axis is labeled "v_o" (output voltage) and is measured in volts (V), ranging from 0 to 1.2 V.

The graph shows two response curves: one for the Shunt compensation scheme and another for the Miller compensation scheme.

- **Shunt Compensation Curve:** This curve shows a slower rise time, indicating a gradual increase in output voltage as time progresses. It starts from 0 V and rises to approximately 1 V, reaching its peak around 10 µs before slightly settling.

- **Miller Compensation Curve:** This curve exhibits a faster response with a quicker rise time compared to the Shunt compensation. It starts from 0 V and rapidly approaches its steady-state value of around 1 V, reaching it in approximately 5 µs. There is a noticeable overshoot at the beginning, where the voltage briefly exceeds 1.2 V before settling back down.

The overall behavior indicates that the Miller compensation scheme allows for a faster response time with some initial overshoot, whereas the Shunt compensation scheme provides a slower, more gradual response without overshoot. This reflects the theoretical understanding that the Miller compensation can charge and discharge more rapidly due to its smaller capacitance.

FIGURE 7.88 (a) Frequency and (b) step responses for the unity-gain amplifier of Fig. 7.87.

## 7.9 FREQUENCY COMPENSATION OF MONOLITHIC OP AMPS

We are now ready to apply the techniques of the previous section to the compensation of the monolithic op amp representatives of Chapter 5, namely, the 741 bipolar op amp and the CMOS op amps of the two-stage and the folded-cascode types. Historically, the 741 was the first op amp to incorporate frequency compensation on chip, in the mid 1960s, a feature that contributed to making the 741 one of the most popular ICs ever. MOS analog technology reached commercial maturity later,
and the first significant articles on CMOS op amp frequency compensation started to appear only in the early 1980s.

### Frequency Compensation of the $\mathbf{7 4 1} \mathbf{0 p}$ Amp

With two dozen transistors, an uncompensated 741 op amp exhibits a multitude of pole and zero frequencies, including complex-conjugate pole pairs, ${ }^{1}$ whose cumulative phase lag far exceeds $-180^{\circ}$. As depicted in the 741 schematic of Fig. 5.1, the 741 is Miller compensated via the capacitance $C_{c}=30 \mathrm{pF}$ across the intermediate stage consisting of the CC-CE pair $Q_{16} Q_{17}$. After compensation, the roots undergo a drastic rearrangement in the complex plane, ${ }^{1}$ such that their combined phase lag is pushed sufficiently above the transition frequency $f_{t}(\cong 1 \mathrm{MHz}$ ). To estimate the dominant pole frequency, refer to the ac equivalent of Fig. 5.11, repeated for convenience in Fig. 7.89 along with the Miller capacitance $C_{c}$. (In anticipation of the dominant role played by $C_{c}$, the much smaller stray capacitances of the nodes at either side of $C_{c}$ have been omitted for simplicity.) This circuit is similar to that of Fig. 7.83, provided we let $C_{f}=C_{c}=30 \mathrm{pF}, R_{1}=R_{o 1} / / R_{i 2}=6.12 / / 4.63=2.64 \mathrm{M} \Omega$, and $R_{2}=R_{o 2} / / R_{i 3}=81.3 / / 9330=80.6 \mathrm{k} \Omega$. Adapting Eq. (7.101) and retaining only the dominant denominator term, we estimate the $-3-\mathrm{dB}$ frequency $f_{b}$ as

$$
\begin{equation*}
f_{b} \cong \frac{1 / 2 \pi}{R_{1} C_{c}\left(1+G_{m 2} R_{2}\right)}=\frac{1 / 2 \pi}{2.64 \times 10^{6} \times 30 \times 10^{-12}(1+80.6 / 0.161)}=4 \mathrm{~Hz} \tag{7.105}
\end{equation*}
$$

Considering all the approximations made, this is close enough to data-sheet value of 5 Hz .
A simulation with the 741 macro-model available in PSpice's library gives, for the case of $\pm 10-\mathrm{V}$ power supplies, $a_{0}=199,220 \mathrm{~V} / \mathrm{V}, f_{b}=5.0 \mathrm{~Hz}, f_{t}=888 \mathrm{kHz}$, and $\operatorname{ph} a\left(f_{t}\right)=-117.2^{\circ}$, so $\phi_{m}=62.8^{\circ}$. As we know from Chapter $6, C_{c}$ also sets the slew rate at a nominal value of $0.5 \mathrm{~V} / \mu \mathrm{s}$. The Miller effect boosts the apparent value of $C_{c}$ by $1+80.6 / 0.161=501.6$, making it appear as an equivalent capacitance of $501.6 \times 30 \mathrm{pF}=150 \mathrm{nF}$ ! Were we to use shunt-capacitance compensation, such a large value could not be fabricated on chip and it would also result in a much lower slew rate.
image_name:FIGURE 7.89 Ac equivalent of the 741 op amp for the estimation of the dominant pole f_{D}
description:
[
name: Rid, type: Resistor, value: 2.19 MΩ, ports: {N1: Vid+, N2: Vid-}
name: Gm1Vid, type: VoltageControlledCurrentSource, ports: {Np: V2, Nn: V1}
name: Ro1, type: Resistor, value: 6.12 MΩ, ports: {N1: V2, N2: V1}
name: Ri2, type: Resistor, value: 4.63 MΩ, ports: {N1: V2, N2: V1}
name: Cc, type: Capacitor, value: 30 pF, ports: {Np: V2, Nn: V3}
name: Gm2V12, type: VoltageControlledCurrentSource, ports: {Np: V3, Nn: V1}
name: Ro2, type: Resistor, value: 81.3 kΩ, ports: {N1: V3, N2: V1}
name: Ri3, type: Resistor, value: 9.33 MΩ, ports: {N1: V3, N2: V1}
name: 1V23, type: VoltageControlledVoltageSource, ports: {Np: X1, Nn: Vo-}
name: Ro, type: Resistor, value: 47 Ω, ports: {N1: X1, N2: Vo+}
]
extrainfo:This AC equivalent circuit diagram represents the 741 operational amplifier for estimating the dominant pole frequency (f_D). It includes resistors, capacitors, and controlled sources to model the amplifier behavior. The Miller effect is considered with a compensation capacitor Cc to manage the slew rate and stability.

FIGURE 7.89 Ac equivalent of the 741 op amp for the estimation of the dominant pole $f_{D}$.

### Frequency Compensation of the Two-Stage CMOS Op Amp

We wish to investigate the frequency compensation of the two-stage CMOS op amp of Fig. 7.90, assuming a $1-\mathrm{pF}$ load. We assume the process parameters of Section 6.12, which are based on $L_{\text {drawn }}=1 \mu \mathrm{~m}$ and are listed in the following PSpice models:

```
.model Mn NMOS(Level=1 Tox=20n Uo=600 Vto=0.7 Lambda=0.1
+ Ld=0.15u Gamma=0.6 phi=0.75 Cj=166u Mj=0.5 Cjsw=0.127n
+ Mjsw=0.33 Pb=0.909 Cgso=0.259n Cgdo=0.259n)
.model Mp PMOS(Level=1 Tox=20n Uo=250 Vto=-0.7 Lambda=0.05
+ Ld=0.2u Gamma=0.5 phi=0.7 Cj=396u Mj=0.5 Cjsw=0.366n
+ Mjsw=0.33 Pb=0.955 Cgso=0.345n Cgdo=0.345n)
```

Following the procedure of Section 6.12, we specify the individual transistor dimensions $A_{s}, P_{s}, A_{d}$, and $P_{d}$ so as to reflect the device geometries of Fig. 7.90. Here, the Ws have been calculated on the basis of $V_{O V}=0.25 \mathrm{~V}$ for all FETs as well as the effective channel lengths $L_{n}=L_{\text {drawn }}-2 L_{\text {ovn }}=1-2 \times 0.15=0.7 \mu \mathrm{~m}$ and $L_{p}=L_{\text {drawn }}-2 L_{\text {ovp }}=$ $1-2 \times 0.2=0.6 \mu \mathrm{~m}$. The outcome is the following PSpice netlist

```
* source CKT_of_Fig_7.90
V_VDD DD 0 2.5V
V_VSS 0 SS 2.5V
I_IREF GP SS DC 100uA
V_Vi IN O DC OVdc AC 1Vac
M_M1 GN O SP SP Mp L=1u W=22u As=66p Ps=28u Ad=66p
+ Pd=28u
M_M2 V1 IN SP SP Mp L=1u W=22u As=66p Ps=28u Ad=66p
+ Pd=28u
M_M3 GN GN SS SS Mn L=1u W=12u As=30p Ps=17u Ad=30p
+
Pd=17u
M_M4 V1 GN SS SS Mn L=1u W=12u As=30p Ps=17u Ad=30p
+ Pd=17u
M_M5 VO V1 SS SS Mn L=1u W=22U As=55p Ps=27u Ad=55p
+
M_M6 VO GP DD DD Mp L=1u W=44u As=132p Ps=50u Ad=132p
+ Pd=50u
M_M7 SP GP DD DD Mp L=1u W=44u As=132p Ps=50u Ad=132p
+ Pd=50u
M_M8 GP GP DD DD Mp L=1u W=44u As=132p Ps=50u Ad=132p
+ Pd=50u
C_CL VO O 5pF
C_Cc V1 VO {Ccvar}
.INC "CKT_of_Fig_7.90-SCHEMATIC1.par"
```

image_name:FIGURE 7.90
description:
[
name: M8, type: PMOS, ports: {S: VDD, D: x1, G: x1}
name: M7, type: PMOS, ports: {S: VDD, D: x2, G: x1}
name: M6, type: PMOS, ports: {S: VDD, D: Vo, G: x1}
name: M1, type: PMOS, ports: {S: x2, D: x3, G: 0}
name: M2, type: PMOS, ports: {S: x2, D: V1, G: Vi}
name: M3, type: NMOS, ports: {S: VSS, D: x3, G: x3}
name: M4, type: NMOS, ports: {S: VSS, D: V1, G: x3}
name: M5, type: NMOS, ports: {S: VSS, D: Vo, G: v1}
name: I_REF, type: CurrentSource, value: 100uA, ports: {Np: x1, Nn: VSS}
name: V_DD, type: VoltageSource, value: 2.5V, ports: {Np: VDD, Nn: 0}
name: V_SS, type: VoltageSource, value: -2.5V, ports: {Np: VSS, Nn: 0}
name: V_i, type: VoltageSource, ports: {Np: Vi, Nn: 0}
name: C_L, type: Capacitor, value: 1.0pF, ports: {Np: Vo, Nn: 0}
name: C_c, type: Capacitor, value: Cvar, ports: {Np: V1, Nn: Vo}
]
extrainfo:The circuit is a two-stage CMOS operational amplifier using conventional Miller compensation. It includes PMOS and NMOS transistors, current and voltage sources, and capacitors for frequency response analysis. The small-signal (.TF) analysis yields specific low-frequency parameters, and the AC analysis provides additional frequency response data.

FIGURE 7.90 PSpice circuit to plot the frequency response a two-stage CMOS op amp using conventional Miller compensation.

The small-signal (.TF) analysis yields the following low-frequency parameter values:

$$
\begin{gathered}
a_{0}=4245 \mathrm{~V} / \mathrm{V} \quad g_{m 1}=0.425 \mathrm{~mA} / \mathrm{V} \quad r_{o 2} / / r_{o 4}=143.3 \mathrm{k} \Omega \\
g_{m 5}=0.9344 \mathrm{~mA} / \mathrm{V} \quad r_{o 5} / / r_{o 6}=74.59 \mathrm{k} \Omega
\end{gathered}
$$

The ac analysis gives the open-loop responses of Fig. 7.91. Using the cursor facility of PSpice on the uncompensated curves ( $C_{c}=0$ ), we find that gain crosses the $0-\mathrm{dB}$ axis at $f_{x} \cong 366 \mathrm{MHz}$, where $\phi_{x} \cong-184^{\circ}$, indicating an amplifier in dire need of frequency compensation.

The logical candidate for dominant-pole compensation is the CS stage $M_{5}$, where we can take advantage of the Miller effect to multiply a small compensation capacitance $C_{c}$ placed between its gate and drain terminals for the purpose of establishing a dominant pole at a suitably low frequency. To investigate further, refer to the ac equivalent of Fig. 7.92, where

$$
\begin{equation*}
R_{1}=r_{o 2} / / r_{o 4} \quad R_{2}=r_{o 5} / / / r_{o 6} \tag{7.106}
\end{equation*}
$$

and $C_{1}$ and $C_{2}$ are the net capacitances associated with the gate and drain terminals of $M_{5}$,

$$
\begin{equation*}
C_{1}=C_{g d 2}+C_{d b 2}+C_{g d 4}+C_{d b 4}+C_{g 55} \quad C_{2}=C_{d b 5}+C_{d b 6}+C_{g d 6}+C_{L} \tag{7.107}
\end{equation*}
$$

(Usually the load capacitance $C_{L}$ dominates all the output-node parasitic capacitances, so we approximate $C_{2} \cong C_{L}$ and ignore $C_{1}$ compared to $C_{2}$.) Moreover, the feedback capacitance is

$$
\begin{equation*}
C_{f}=C_{c}+C_{g d 5} \tag{7.108}
\end{equation*}
$$

image_name:FIGURE 7.91
description:The graph in FIGURE 7.91 consists of two Bode plots, which represent the open-loop gain and phase response of an operational amplifier as a function of frequency. The plots illustrate the effects of different compensation capacitances \( C_c \) on the amplifier's frequency response.

Upper Plot: Open-Loop Gain
- **Type of Graph**: Bode plot for open-loop gain.
- **Axes Labels and Units**:
- **Y-axis**: Open-loop gain \( a \) in decibels (dB).
- **X-axis**: Frequency \( f \) in hertz (Hz), displayed on a logarithmic scale ranging from \( 10^3 \) to \( 10^{11} \) Hz.
- **Overall Behavior and Trends**:
- The gain starts high (around 80 dB) at low frequencies and decreases with increasing frequency.
- The uncompensated response (\( C_c = 0 \)) shows a steeper decline in gain as frequency increases.
- As \( C_c \) increases from 0.1 pF to 10 pF, the gain curve flattens, indicating improved stability and bandwidth.
- **Key Features and Technical Details**:
- The curves show different slopes, with larger \( C_c \) values resulting in more gradual slopes.
- The crossover frequency, where the gain drops to 0 dB, shifts to higher frequencies with increasing \( C_c \).

Lower Plot: Phase Response
- **Type of Graph**: Bode plot for phase.
- **Axes Labels and Units**:
- **Y-axis**: Phase of \( a \) in degrees.
- **X-axis**: Frequency \( f \) in hertz (Hz), also on a logarithmic scale ranging from \( 10^3 \) to \( 10^{11} \) Hz.
- **Overall Behavior and Trends**:
- The phase starts near 0° at low frequencies and decreases, approaching -360° at high frequencies.
- The phase response for \( C_c = 0 \) shows a rapid decline, whereas higher \( C_c \) values slow the phase drop.
- **Key Features and Technical Details**:
- The phase margin, indicating stability, improves with increasing \( C_c \), as the curves bend more towards -90° in the vicinity of the crossover frequency.
- The phase crossover point, where the phase reaches -180°, shifts to higher frequencies with larger \( C_c \).

Annotations and Specific Data Points
- The graph includes annotations indicating the values of \( C_c \) for each curve, specifically at 0 pF, 0.1 pF, 1 pF, and 10 pF. These annotations help identify how the compensation capacitance affects the amplifier's frequency response.

FIGURE 7.91 Magnitude and phase plots for the op amp of Fig. 7.90. The dark curves show the uncompensated ( $C_{c}=0$ ) response. The shaded curves indicate that conventional Miller compensation fails to convincingly bend the phase curves toward $-90^{\circ}$ in the vicinity of crossover.
(Usually $C_{c} \gg C_{g d 5}$, so we approximate $C_{f} \cong C_{c}$.) Ignoring the stray capacitance $C_{i}$, we observe that this circuit is similar to that of Fig. 7.83, so we adapt the formulas developed there (after dropping the subscripts "new" to simplify the notation), and state that in the presence of $C_{c}$, gain takes on the form

$$
\begin{equation*}
a(j f)=a_{0} \frac{1-j f / f_{0}}{\left(1+j f / f_{1}\right)\left(1+j f / f_{2}\right)} \tag{7.109}
\end{equation*}
$$

image_name:FIGURE 7.92
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: Ci, type: Capacitor, value: Ci, ports: {Np: Vi, Nn: V1}
name: g_m1Vi, type: VoltageControlledCurrentSource, ports: {Np: V1, Nn: GND}
name: R1, type: Resistor, value: (ro2//ro4), ports: {N1: V1, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: V1, Nn: GND}
name: Cf, type: Capacitor, value: Cf, ports: {Np: V1, Nn: Vo}
name: g_m5V1, type: VoltageControlledCurrentSource, ports: {Np: Vo, Nn: GND}
name: R2, type: Resistor, value: (ro5//ro6), ports: {N1: Vo, N2: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: Vo, Nn: GND}
]
extrainfo:The circuit is an approximate AC equivalent of a two-stage CMOS amplifier, consisting of a voltage source, capacitors, resistors, and voltage-controlled current sources. It includes feedback capacitance Cf and forward capacitance C1, with resistors R1 and R2 representing parallel resistances. The circuit is used to analyze frequency response and gain characteristics.

FIGURE 7.92 Approximate ac equivalent of the two-stage CMOS amplifier of Fig. 7.90.
where

$$
\begin{gather*}
a_{0}=g_{m 1} R_{1} g_{m 5} R_{2}  \tag{7.110}\\
f_{1} \cong \frac{1 / 2 \pi}{R_{1}\left[C_{1}+C_{f}\left(1+g_{m 5} R_{2}+R_{2} / R_{1}\right)\right]+R_{2} C_{2}} \cong \frac{1}{2 \pi R_{1} g_{m 5} R_{2} C_{f}} \cong \frac{1}{2 \pi R_{1} g_{m 5} R_{2} C_{c}}  \tag{7.111}\\
f_{2} \cong \frac{g_{m 5} / 2 \pi}{C_{1}+C_{2}\left(1+C_{1} / C_{f}\right)} \cong \frac{g_{m 5}}{2 \pi C_{2}} \cong \frac{g_{m 5}}{2 \pi C_{L}}  \tag{7.112}\\
f_{0}=\frac{g_{m 5}}{2 \pi C_{f}} \cong \frac{g_{m 5}}{2 \pi C_{c}} \tag{7.113}
\end{gather*}
$$

Moreover, the gain-bandwidth product over the frequency region dominated by $f_{1}$ is GBP $=a_{0} \times f_{1}$, or

$$
\begin{equation*}
\mathrm{GBP}=\frac{g_{m 1}}{2 \pi C_{f}} \cong \frac{g_{m 1}}{2 \pi C_{c}} \tag{7.114}
\end{equation*}
$$

(Beside confirming the pole pair and RHP zero, the plots of Fig. 7.91 reveal the existence of an additional RHP zero in the $10-\mathrm{GHz}$ range, stemming from forward transmission from $V_{i}$ to $V_{1}$ via the parasitics of the input stage. However, given its high frequency, its impact on the phase margin will be negligible and it shall be ignored. Moreover, the first stage introduces an additional pole-zero pair spaced an octave apart, as per Fig. 6.29b. This too will be ignored for the sake of simplicity.)

Equations (7.111) through (7.113) indicate that increasing $C_{c}$ will downshift both $f_{1}$ and $f_{0}$ by about the same amount, while leaving $f_{2}$ approximately unchanged. In fact, for $C_{c}=C_{L}(=1 \mathrm{pF}), f_{0}$ overlaps $f_{2}$, and for $C_{c}=10 C_{L}(=10 \mathrm{pF}), f_{0}$ is a decade below $f_{2}$ (this is confirmed also by the magnitude plots of Fig. 7.91). We make the important observation that regardless of the value of $C_{c}, f_{1}$ and $f_{0}$ are generally not separated widely enough to prevent the phase lag of the RHP zero from eroding the phase margin. This inherent limitation of MOSFETs stems from their notoriously low $g_{m} \mathrm{~s}\left(g_{m 5}\right.$ in the present case, as evidenced by the fact that the separation $f_{0} / f_{1}$ is proportional to $g_{m 5}^{2}$ ). Were it possible to raise $g_{m 5}$ by, say, a decade without altering the capacitances, the GBP would remain unchanged, while both $f_{0}$ and $f_{2}$ would move up and away from $f_{x}$ by a decade, raising the phase margin significantly (see Problem 7.64).
(a) Estimate the phase margin of the amplifier of Fig. 7.90 for the special case $C_{c}=C_{L}(=1 \mathrm{pF})$.
(b) Comment on your results.

#### Solution

(a) Equations (7.111) through (7.113) give $f_{1}=1 /\left(2 \pi \times 143.3 \times 10^{3} \times 0.9344 \times\right.$ $\left.10^{-3} \times 74.59 \times 10^{3} \times 1 \times 10^{-12}\right)=15.9 \mathrm{kHz}$ and $f_{0}=f_{2}=0.9344 \times$ $10^{-3} /\left(2 \pi \times 1 \times 10^{-12}\right)=149 \mathrm{MHz}$, so the gain is

$$
a(j f)=\frac{4245\left[1-j f /\left(149 \times 10^{6}\right)\right]}{\left[1+j f /\left(15.9 \times 10^{3}\right)\right] \times\left[1+j f /\left(149 \times 10^{6}\right)\right]}
$$

We easily find that the magnitude

$$
\begin{aligned}
|a(j f)| & =4245 \sqrt{\frac{1+f^{2} /\left(149 \times 10^{6}\right)^{2}}{\left[1+f^{2} /\left(15.9 \times 10^{3}\right)^{2}\right]\left[1+f^{2} /\left(149 \times 10^{6}\right)^{2}\right]}} \\
& =\frac{4245}{\sqrt{1+f^{2} /\left(15.9 \times 10^{3}\right)^{2}}}
\end{aligned}
$$

drops to $1 \mathrm{~V} / \mathrm{V}$ at $f_{x}=67.5 \mathrm{MHz}$, where

$$
\begin{aligned}
\phi_{x} & =-\tan ^{-1} \frac{67.5 \times 10^{6}}{15.9 \times 10^{3}}-\tan ^{-1} \frac{67.5 \times 10^{6}}{149 \times 10^{6}}-\tan ^{-1} \frac{67.5 \times 10^{6}}{149 \times 10^{6}} \\
& \cong-90^{\circ}-24.4^{\circ}-24.4^{\circ} \cong-139^{\circ}
\end{aligned}
$$

Consequently, $\phi_{m}=180-139=41^{\circ}$, which is generally not sufficiently high. (PSpice gives $f_{x}=63.5 \mathrm{MHz}, \phi_{x}=-141.6^{\circ}$, and $\phi_{m}=38.4^{\circ}$, in reasonable agreement with the calculations.)
(b) For $C_{c}=C_{L}$ the RHP zero and the second pole cancel each other from the magnitude expression, leaving only the dominant pole (this is confirmed by the magnitude curve corresponding to $C_{c}=1 \mathrm{pF}$ in Fig. 7.91). However, their individual phase lags, far from canceling out, reinforce each other!

To figure ways around the effect of low $g_{m 5}$, we need to take a closer look at the physical basis of the zero frequency $f_{0}$. With reference to Fig. 7.92 , we decompose the current through $C_{f}$ into a forward component $I_{f w}(j f)=V_{1} /\left(1 / j 2 \pi f C_{c}\right)$ and a reverse component $I_{r v}(j f)=V_{o} /\left(1 / j 2 \pi f C_{c}\right)$, or

$$
\begin{equation*}
I_{f w}(j f)=j 2 \pi f C_{c} V_{1} \quad I_{r v}(j f)=j 2 \pi f C_{c} V_{o} \tag{7.115}
\end{equation*}
$$

We make the following observations:

- $I_{r v}(j f)$ is responsible for making $C_{c}$ appear magnified by the Miller multiplier when reflected to the input node $V_{1}$. As such, $I_{r v}(j f)$ is desirable because it establishes the dominant pole.
- $I_{f w}(j f)$ is responsible for creating the RHP transmission zero at the output node $V_{o}$. As such, it is undesirable because the presence of this zero erodes the phase margin and halts the gain roll-off that is needed to stabilize the circuit. Recall from Section 6.3 that $f_{0}$ is the frequency at which the condition $\left|I_{f_{v}}\left(j f_{0}\right)\right|=g_{m 5} V_{1}$ is met, which causes $V_{o}$ to drop to zero (hence the name). Rewriting as $\left|j 2 \pi f_{0} C_{f} V_{1}\right|=$ $g_{m 5} V_{1}$ gives the familiar result $f_{0}=g_{m s} /\left(2 \pi C_{f}\right)$. For $f>f_{0}$ we have $\left|I_{f w}(j f)\right|>$ $g_{m 5} V_{1}$, indicating a polarity reversal of $V_{o}$ that turns feedback from negative to positive. This is not necessarily a problem if $f_{0} \gg f_{x}$, which is usually the case with bipolar amplifiers. However, in MOS amplifiers $f_{0}$ tends to be much lower due to the aforementioned low $g_{m}$ of FETs.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: S1, D: VDD, G: Vo}
name: M5, type: NMOS, ports: {S: VSS, D: Vo, G: V1}
name: I_S, type: CurrentSource, value: I_S, ports: {Np: s1, Nn: VSS}
]
extrainfo:The circuit diagram (a) shows a configuration to eliminate the RHP zero using a voltage buffer. The NMOS M_CD acts as a buffer, transmitting the current I_rv to node V1. The NMOS M5 is connected to the output node Vo, providing the necessary feedback.
image_name:(b)
description:
[
'name': 'M5', 'type': 'NMOS', 'ports': {'S': 'VSS', 'D': 'Vo', 'G': 'V1'
'name': 'MCG', 'type': 'PMOS', 'ports': {'S': 's1', 'D': 'v1', 'G': '0'
'name': 'ID', 'type': 'CurrentSource', 'value': 'ID', 'ports': {'Np': 'V1', 'Nn': 'VSS'
'name': 'I_S', 'type': 'CurrentSource', 'value': 'I_S', 'ports': {'Np': 'VDD', 'Nn': 's1'
'name': 'CC', 'type': 'Capacitor', 'value': 'CC', 'ports': {'Np': 'S1', 'Nn': 'Vo'
]
extrainfo:The circuit diagram (b) shows a configuration using NMOS and PMOS transistors with voltage and current sources. The NMOS transistor M1 is used for amplification, while M5 acts as a load. The PMOS transistor MCG provides feedback. The current sources IS and ID supply biasing currents, and the capacitor CC stabilizes the circuit. The circuit is designed to eliminate or relocate the right-half-plane zero.
image_name:(c)
description:
[
name: M5, type: NMOS, ports: {S: VSS, D: Vo, G: V1}
name: C_C, type: Capacitor, value: C_C, ports: {Np: Vo, Nn: RC}
name: R_C, type: Resistor, value: R_C, ports: {N1: RC, N2: V1}
]
extrainfo:The circuit diagram (c) shows a configuration to relocate the RHP zero using a series resistance R_C. It includes a capacitor C_C connected between the output Vo and the node RC, which is also connected to the gate of NMOS M5 through the resistor R_C.

FIGURE 7.93 The RHP zero can be eliminated via (a) a voltage buffer or (b) a current buffer, or it can be relocated via (c) a suitable series resistance $R_{c}$.

The best way to cope with the undesirable RHP zero is to eliminate it altogether or at least to shift it to a less harmful location. Figure 7.93 shows three different techniques for achieving this goal.

- The scheme ${ }^{8}$ of Fig. 7.93a exploits the unilateral nature of a CD voltage buffer to transmit $I_{r v}$ to node $V_{1}$ while diverting $I_{f w}$ to $V_{D D}$ and thus preventing it from reaching node $V_{o}$, where it would create the RHP zero (see Problem 7.69). A drawback of this scheme is a reduction in the OVS, as $v_{O(\min )}$ is raised from $V_{S S}+V_{O V S}$ to $V_{S S}+V\left(I_{S}\right)_{\min }+V_{G S(C D)}$, where $V\left(I_{S}\right)_{\text {min }}$ is the minimum allowable voltage drop across the $I_{S}$ current sink, and $V_{G S(C D)}$ is the gate-source voltage drop of the CD buffer.
- The scheme ${ }^{9}$ of Fig. $7.93 b$ uses a CG current buffer to transmit $I_{r v}$ to node $V_{1}$ while inhibiting the formation of $I_{f w}$ because of the high resistance seen looking into the buffer's drain (see Problem 7.70). A drawback of this scheme is that $I_{S}$ and $I_{D}$ must be closely matched to avoid creating an intolerable offset error (see Ref. [10] for an ingenious way around this).
- The scheme ${ }^{11}$ of Fig. $7.93 c$ utilizes a series resistance $R_{c}$ to curb $I_{f w}$ at high frequencies. At low frequencies, where $R_{c} \ll\left|1 /\left(j 2 \pi f C_{c}\right)\right|, C_{c}$ still dominates, giving $I_{r v}(j f) \cong j 2 \pi f C_{c} V_{o}$ to sustain the dominant pole $f_{1}$. But at high frequencies, the presence of $R_{c}$ changes the location of the transmission zero because we now have $I_{f w}(s)=V_{1} /\left(R_{c}+1 / s C_{c}\right)$. $V_{o}$ will drop to zero at the complex frequency $s_{0}$ such that $I_{f w}\left(s_{0}\right)=g_{m 5} V_{1}$, or

$$
\frac{V_{1}}{R_{c}+1 /\left(s_{0} C_{c}\right)}=g_{m 5} V_{1}
$$

Solving for $s_{0}$, we get the $s$-plane zero

$$
s_{0}=\frac{1}{\left(1 / g_{m 5}-R_{c}\right) C_{c}}
$$

As a consequence, the zero frequency in the numerator of Eq. (7.109) takes on the modified form

$$
\begin{equation*}
f_{0(\text { new })}=\frac{1}{2 \pi\left(1 / g_{m 5}-R_{c}\right) C_{c}} \tag{7.116}
\end{equation*}
$$

We observe that the presence of $R_{c}$ reduces the denominator (at least so long as $\left.R_{c}<1 / g_{m 5}\right)$, in turn raising $f_{0(\text { new })}$ and pushing its phase lag above and away from the crossover frequency $f_{x}$. Making $R_{c}=1 / g_{m 5}$ pushes $f_{0(\text { new })}$ to infinity and reduces the numerator of Eq. (7.109) to unity. Raising $R_{c}$ further $\left(R_{c}>1 / g_{m 5}\right)$ changes the polarity of $f_{0(\text { new })}$ in the numerator of Eq. (7.109), thus resulting in a left-half-plane (LHP) zero. As we know, this is highly desirable because it produces phase lead (as opposed to the phase lag of a RHP zero). The resistance $R_{c}$ is usually the channel of a MOSFET biased in the ohmic region (see Problem 7.71 for a popular circuit realization of $R_{c}$ ).
(a) Find $R_{c}$ and $C_{c}$ to compensate the two-stage op amp of Fig. 7.90 for $\phi_{m}=$ $75^{\circ}$ with $f_{0}=\infty$. Hence, estimate the open-loop gain $a(j f)$, the gain-bandwidth product GBP, and the slew rate SR.
(b) Compare with PSpice, and comment.
(c) Assuming $\beta=1$, plot the closed-loop frequency response as well as the transient response to a pulse alternating between -100 mV and +100 mV . Is the pulse response slew-rate limited?

#### Solution

(a) The pole frequency due to $C_{L}$ is still $f_{2}=g_{m 5} /\left(2 \pi C_{L}\right) \cong 149 \mathrm{MHz}$. For $\phi_{m}=$ $75^{\circ}$ we need $\phi_{x}=75-180=-105^{\circ}$. With $-90^{\circ}$ coming from the dominant pole frequency $f_{1}$, the cumulative phase contribution by $f_{2}$ and higher-order root frequencies must be $90-105=-15^{\circ}$. Ignoring the higher-order roots, we require that $-15^{\circ} \cong-\tan ^{-1}\left(f_{x} / f_{2}\right)$, or

$$
f_{x} \cong f_{2} \times \tan 15^{\circ}=149 \times 0.268=39.8 \mathrm{MHz}
$$

The required dominant pole frequency is

$$
f_{1}=\frac{f_{x}}{a_{0}}=\frac{39.8 \times 10^{6}}{4245}=9.39 \mathrm{kHz}
$$

so Eq. (7.111) gives

$$
\begin{aligned}
C_{c} & \cong \frac{1}{2 \pi R_{1} g_{m 5} R_{2} f_{1}} \\
& =\frac{1}{2 \pi \times 143.3 \times 10^{3} \times 0.9344 \times 10^{-3} \times 74.59 \times 10^{3} \times 9.39 \times 10^{3}} \\
& \cong 1.70 \mathrm{pF}
\end{aligned}
$$

Finally, to move the zero frequency to infinity we need

$$
R_{c}=1 / g_{m 5}=1 /\left(0.9344 \times 10^{-3}\right)=1.07 \mathrm{k} \Omega
$$

image_name:Figure 7.94
description:
[
name: M8, type: PMOS, ports: {S: VDD, D: X1, G: X1}
name: M7, type: PMOS, ports: {S: VDD, D: X2, G: X1}
name: M6, type: PMOS, ports: {S: VDD, D: Vo, G: X1}
name: M1, type: PMOS, ports: {S: X2, D: X3, G: GND}
name: M2, type: PMOS, ports: {S: X2, D: V1, G: Vi}
name: M3, type: NMOS, ports: {S: VSS, D: X3, G: X3}
name: M4, type: NMOS, ports: {S: VSS, D: Vo, G: X3}
name: M5, type: NMOS, ports: {S: VSS, D: Vo, G: V1}
name: IREF, type: CurrentSource, value: 100μA, ports: {Np: X1, Nn: GND}
name: Vi, type: VoltageSource, ports: {Np: Vi, Nn: GND}
name: Rc, type: Resistor, value: 1.07kΩ, ports: {N1: V1, N2: Rc}
name: Cc, type: Capacitor, value: 1.7pF, ports: {Np: Rc, Nn: Vo}
name: CL, type: Capacitor, value: 1.0pF, ports: {Np: Vo, Nn: GND}
]
extrainfo:This is a frequency-compensated operational amplifier circuit. It uses PMOS and NMOS transistors in a differential amplifier configuration. The compensation is achieved using a resistor Rc and a capacitor Cc to stabilize the frequency response. The circuit is powered by a positive supply VDD and a negative supply VSS. The output node is Vo, and the input is Vi.

FIGURE 7.94 Frequency compensation for op amp of Example 7.37.
Ignoring higher-order roots, the gain after compensation is approximately

$$
a(j f) \cong \frac{4245}{\left[1+j f /\left(9.39 \times 10^{3}\right)\right] \times\left[1+j f /\left(149 \times 10^{6}\right)\right]}
$$

We also have $\mathrm{GBP} \cong f_{x}=39.8 \mathrm{MHz}$ and $\mathrm{SR}=I_{D 7} / C_{c}=(100 \mu \mathrm{~A}) /(1.70 \mathrm{pF}) \cong$ $59 \mathrm{~V} / \mu \mathrm{s}$.
(b) Using the PSpice circuit of Fig. 7.94, we obtain the plots of Fig. 7.95. Compared to Fig. 7.91, the phase curve at crossover is now far more convincingly bent
image_name:FIGURE 7.95
description:The graph in FIGURE 7.95 consists of two plots: a magnitude plot and a phase plot, both related to the open-loop gain of an operational amplifier.

Magnitude Plot
- **Type of Graph:** Bode plot for open-loop gain.
- **Axes Labels and Units:**
- **X-Axis:** Frequency \( f \) in Hertz (Hz), ranging from \( 10^3 \) to \( 10^{11} \) Hz on a logarithmic scale.
- **Y-Axis:** Open-loop gain \( a \) in decibels (dB), ranging from -60 dB to 80 dB.
- **Overall Behavior and Trends:**
- The plot shows two curves representing different conditions: \( C_c = 1.7 \) pF (black curve) and \( C_c \approx 0 \) (gray curve).
- Both curves start at a high gain and decrease as frequency increases, indicating a typical low-pass filter behavior.
- The curve with \( C_c = 1.7 \) pF shows a steeper decline compared to the curve with \( C_c \approx 0 \).
- **Key Features and Technical Details:**
- The gain crosses 0 dB at different frequencies for the two conditions, reflecting the effect of the compensation capacitance \( C_c \).

Phase Plot
- **Type of Graph:** Bode plot for phase shift.
- **Axes Labels and Units:**
- **X-Axis:** Frequency \( f \) in Hertz (Hz), same as the magnitude plot.
- **Y-Axis:** Phase of \( a \) in degrees, ranging from -360° to 0°.
- **Overall Behavior and Trends:**
- The phase plot also shows two curves for the same conditions: \( C_c = 1.7 \) pF (black curve) and \( C_c \approx 0 \) (gray curve).
- Both curves start near 0° and decrease with frequency, crossing -90° and further declining.
- The phase shift is more pronounced for the \( C_c = 1.7 \) pF condition, indicating greater phase lag.
- **Key Features and Technical Details:**
- The phase at crossover frequency \( f_x = 35.2 \) MHz for \( C_c = 1.7 \) pF is approximately -107.2°, leading to a phase margin \( \phi_m \) of 72.8°.

Annotations and Specific Data Points:
- The plots are annotated with arrows indicating the conditions for \( C_c = 1.7 \) pF and \( C_c \approx 0 \).
- The critical crossover frequency and phase margin are key points of interest, particularly in assessing stability and performance of the op amp circuit.

FIGURE 7.95 Magnitude and phase plots for the op amp of Fig. 7.94.
toward $-90^{\circ}$. In fact, using PSpice's cursor facility, we find $f_{x}=35.2 \mathrm{MHz}$, where $\phi_{x}=-107.2^{\circ}$, and, hence, $\phi_{m}=180-107.2=72.8^{\circ}$. These data are in fair agreement with the hand calculations, which are based on the assumption that all internal stray capacitances are negligible compared to $C_{c}$ and $C_{L}$.
(c) To achieve $\beta=1$ in Fig. 7.94 , lift $M_{1}$ 's gate off ground and tie it to node $V_{o}$. This yields the closed-loop responses of Fig 7.96. Note the absence of slewrate limiting in Fig. 7.96b.
image_name:(a)
description:The graph is a Bode plot representing the closed-loop gain in decibels (dB) versus frequency in hertz (Hz). The x-axis is labeled "Frequency f (Hz)" and is on a logarithmic scale ranging from \(10^6\) Hz to \(10^9\) Hz. The y-axis is labeled "Closed-loop gain (dB)" and ranges from -40 dB to 0 dB.

Overall Behavior and Trends
- **Initial Plateau:** The gain starts at 0 dB, indicating unity gain at low frequencies.
- **Roll-off:** As the frequency increases beyond \(10^7\) Hz, the gain begins to decrease, indicating a typical low-pass filter behavior.
- **Steep Decline:** The graph shows a steep decline in gain after \(10^8\) Hz, suggesting a significant reduction in gain at higher frequencies.

Key Features and Technical Details
- **Cutoff Frequency:** The transition from the flat region to the declining region occurs around \(10^8\) Hz, indicating the cutoff frequency where the gain starts to drop significantly.
- **Slope:** The slope of the decline is consistent with a standard roll-off, likely around -20 dB/decade, typical for a single-pole low-pass filter.

Annotations and Specific Data Points
- There are no specific annotations or markers on the graph, but the logarithmic scale and gridlines provide clear reference points for estimating the gain at various frequencies.

image_name:(b)
description:1. **Type of Graph and Function:**
- The graph is a time-domain waveform, specifically showing a pulse response of a CMOS operational amplifier configured for negative-feedback operation.

2. **Axes Labels and Units:**
- The horizontal axis represents **Time** in nanoseconds (ns).
- The vertical axis represents **Output Voltage, \( v_o \)** in millivolts (mV).
- The scale for both axes is linear.

3. **Overall Behavior and Trends:**
- The waveform exhibits a pulse shape with a distinct rise and fall.
- Starting at -100 mV, the output quickly rises to approximately 100 mV, indicating a sharp increase.
- The waveform maintains a high level around 100 mV for a period before dropping back down to -100 mV.
- The transitions between high and low levels are relatively sharp, suggesting a fast response time.

4. **Key Features and Technical Details:**
- The initial rise occurs almost immediately at the start of the time axis, indicating a rapid response.
- The pulse width, or the duration for which the output remains high, is approximately from 10 ns to 100 ns.
- There is a slight overshoot observed at the beginning of the rise, which then stabilizes.
- The fall back to -100 mV is also steep, occurring around 100 ns.

5. **Annotations and Specific Data Points:**
- There are no specific annotations or markers on the graph.
- The gridlines provide clear reference points for estimating the timing and voltage levels of the pulse response.

This graph effectively demonstrates the pulse response characteristics of the CMOS op amp, highlighting its fast switching capability and the stability of its output during the pulse duration.

(b)

FIGURE 7.96 (a) Frequency (b) pulse responses of the CMOS op amp of Fig. 7.94 configured for negative-feedback operation with $\beta=1$.

If $C_{L}$ is doubled in the circuit of Example 7.37, find $R_{c}$ so as to retain the same phase margin without increasing $C_{c}$. What is the expression for $a(j f)$ after compensation? Verify with PSpice and comment.

#### Solution

Doubling $C_{L}$ will halve $f_{2}$ to 74.5 MHz , bringing it an octave closer to $f_{x}$, where it will erode $\phi_{m}$. Its phase at $f_{x}$ is $-\tan ^{-1}\left(f_{x} / f_{2}\right)=-\tan ^{-1}(39.8 / 74.5)=-28.1^{\circ}$, which exceeds the original $-15^{\circ}$ by $-28.1-(-15)=-13.1^{\circ}$. To retain the original $\phi_{m}$, we must neutralize this excess phase lag with the phase lead of a LHP zero. Its frequency $-f_{0 \text { (new) }}$ must be such that $+13.1^{\circ}=\tan ^{-1}\left[f_{x} /\left(-f_{0(\text { new })}\right)\right]=$ $\tan ^{-1}\left[39.8 /\left(-f_{0 \text { (new) }}\right)\right]$, which gives $-f_{0 \text { (new) }} \cong 171 \mathrm{MHz}$. Using Eq. (7.116)

$$
-171 \times 10^{6}=\frac{1}{2 \pi\left(1070-R_{c}\right) \times 1.7 \times 10^{-12}}
$$

gives $R_{c}=1.617 \mathrm{k} \Omega$. After compensation the gain is

$$
a(j f) \cong \frac{4245\left[1+j f /\left(171 \times 10^{6}\right)\right]}{\left[1+j f /\left(9.39 \times 10^{3}\right)\right] \times\left[1+j f /\left(74.5 \times 10^{6}\right)\right]}
$$

(note the + sign in the numerator, indicative of a LHP zero!). Re-running the PSpice circuit of Fig. 7.94, but with $C_{L}=2 \mathrm{pF}$ and $R_{c}=1.617 \mathrm{k} \Omega$ we find $f_{x}=35.2 \mathrm{MHz}$, where $\phi_{x}=-107.2^{\circ}$, and, hence, $\phi_{m}=180-107.2=72.8^{\circ}$. These data are again in fair agreement with the hand calculations, which are based on the assumption that all internal stray capacitances are negligible compared to $C_{c}$ and $C_{L}$.

### Frequency Compensation of the Folded-Cascode CMOS Op Amp

Figure 7.97 shows the ac model of the folded-cascode op amp, along with the most relevant capacitances intervening in its frequency response. Each capacitance is the result of lumping together all parasitic capacitances associated with the corresponding node (the output node includes also the external load capacitance). According to the OCTC procedure of Section 6.7, the $-3-\mathrm{dB}$ frequency is

$$
\begin{equation*}
f_{b} \cong \frac{1 / 2 \pi}{R_{1} C_{1}+R_{2} C_{2}+\cdots+R_{5} C_{5}+R_{o}\left(C_{6}+C_{c}\right)} \tag{7.117}
\end{equation*}
$$

where $R_{1}$ through $R_{5}$ are the open-circuit equivalent resistances seen by $C_{1}$ through $C_{5}$, and $R_{o}$ is the op amp's output resistance. By Eq. (5.69), this resistance is

$$
\begin{equation*}
R_{o} \cong\left[\left(g_{m 6}+g_{m b 6}\right) r_{o 6} r_{o 8}\right] / /\left[\left(g_{m 4}+g_{m b 4}\right) r_{o 4}\left(r_{o 2} / / r_{o 10}\right)\right] \tag{7.118}
\end{equation*}
$$

The resistances $R_{1}$ through $R_{5}$ are all source resistances, on the order of $1 /\left(g_{m}+g_{m b}\right)$. As such they are much smaller than $R_{o}$, and even though the time constants $R_{1} C_{1}$ through $R_{5} C_{5}$ are likely to differ from one another, they all tend to be negligible compared to that associated with $R_{o}$, so we approximate

$$
\begin{equation*}
f_{b} \cong \frac{1}{2 \pi R_{o}\left(C_{6}+C_{c}\right)} \tag{7.119}
\end{equation*}
$$

According to Eq. (7.94), the phase margin can be expressed as $\phi_{m}=90^{\circ}+\phi_{x(\mathrm{HOR})}$, where $\phi_{x(\mathrm{HOR})}$ is the combined phase shift due to all higher-order roots. Consequently,
image_name:FIGURE 7.97
description:
[
name: M1, type: PMOS, ports: {S: s1s2, D: s1s3d9, G: Vid/2}
name: M2, type: PMOS, ports: {S: s1s2, D: d2s4d10, G: -Vid/2}
name: M3, type: NMOS, ports: {S: d1s3d9, D: X2, G: GND}
name: M4, type: NMOS, ports: {S: d2s4d10, D:  V2, G: GND}
name: M5, type: PMOS, ports: {S: x1, D: x2, G: x2}
name: M6, type: PMOS, ports: {S: d8s6, D: Vo, G: x2}
name: M7, type: PMOS, ports: {S: GND, D: x1, G: x1}
name: M8, type: PMOS, ports: {S: x1, D: d856, G: x1}
name: M9, type: NMOS, ports: {S: GND, D: d1s3d9, G: GND}
name: M10, type: NMOS, ports: {S: GND, D: d2s4d10, G: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: d2s4d10, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: d1s3d9, Nn: GND}
name: C3, type: Capacitor, value: C3, ports: {Np: x2, Nn: GND}
name: C4, type: Capacitor, value: C4, ports: {Np: x1, Nn: GND}
name: C5, type: Capacitor, value: C5, ports: {Np: d856, Nn: GND}
name: C6, type: Capacitor, value: C6, ports: {Np: Vo, Nn: GND}
name: Cc, type: Capacitor, value: Cc, ports: {Np: Vo, Nn: GND}
name: Vid/2, type: VoltageSource, ports: {Np: Vid/2, Nn: GND}
name: -Vid/2, type: VoltageSource, ports: {Np: -Vid/2, Nn: GND}
]
extrainfo:This is a folded-cascode operational amplifier circuit. It features differential inputs and uses PMOS and NMOS transistors to achieve high gain and wide bandwidth. Capacitors C1 to C6 and Cc are used for frequency compensation and stability. The circuit is designed to optimize phase margin and gain.

FIGURE 7.97 Ac model of the folded-cascode op amp.
image_name:FIGURE 7.98 PSpice circuit to plot the gain of a folded-cascode CMOS op amp
description:
[
name: M1, type: PMOS, ports: {S: P, D: X4, G: Vi}
name: M2, type: PMOS, ports: {S: P, D: x5, G: GND}
name: M3, type: NMOS, ports: {S: x4, D: x2, G: x3}
name: M4, type: NMOS, ports: {S: x5, D: Vo, G: x3}
name: M5, type: PMOS, ports: {S: x1, D: VDD, G: x1}
name: M6, type: PMOS, ports: {S: x7, D: Vo, G: x2}
name: M7, type: PMOS, ports: {S: VDD, D: x1, G: x1}
name: M8, type: PMOS, ports: {S: VDD, D: x7, G: x1}
name: M9, type: NMOS, ports: {S: VSS, D: x4, G: x6}
name: M10, type: NMOS, ports: {S: VSS, D: x5, G: x6}
name: IREF, type: CurrentSource, value: 100uA, ports: {Np: VDD, Nn: p}
name: Vi, type: VoltageSource, ports: {Np: Vi, Nn: GND}
name: Cc, type: Capacitor, value: Cvar, ports: {Np: Vo, Nn: GND}
]
extrainfo:This circuit is a folded-cascode CMOS operational amplifier designed for high gain and wide bandwidth. It uses PMOS and NMOS transistors in a differential pair configuration. The capacitors are used for frequency compensation to optimize the phase margin and gain. The supply voltages are VDD (2.5V) and VSS (-2.5V).

FIGURE 7.98 PSpice circuit to plot the gain of a folded-cascode CMOS op amp with a variable load $C_{c}$.
in order to compensate the folded-cascode op amp for a given $\phi_{m}$, we simply add enough capacitance to the output node to lower $f_{b}$ until the condition $\phi_{x(\mathrm{HOR})}=\phi_{m}-$ $90^{\circ}$ is met. The gain-bandwidth product after compensation is GBP $=a_{0} \times f_{b}$, where $a_{0}=g_{m 1} R_{o}, g_{m 1}$ being the transconductance of the transistors of the SC pair. Using Eq. (7.119), we get

$$
\begin{equation*}
\mathrm{GBP} \cong \frac{g_{m 1}}{2 \pi\left(C_{6}+C_{c}\right)} \tag{7.120}
\end{equation*}
$$

Let us illustrate the above concepts using the PSpice circuit of Fig. 7.98 as a practical example. We assume the same process parameters as the two-stage op amp of Fig. 7.90, which are based on $L_{\text {drawn }}=1 \mu \mathrm{~m}$ with effective channel lengths $L_{n}=0.7 \mu \mathrm{~m}$ and $L_{p}=0.6 \mu \mathrm{~m}$. Moreover, the $W \mathrm{~s}$ have been calculated on the basis of $V_{O V}=0.25 \mathrm{~V}$ for all FETs. The outcome is the following netlist:

```
* source CKT_of_Fig_7.98
V_VDD DD 0 2.5V
V_VSS 0 SS 2.5V
I_I1 DD S12 DC 100uA
V_V1 G90 SS 0.95V
V_V2 G34 G90 0.25V
M_M1 D9 IN S12 S12 Mp L=1u W=22u As=66p Ps=28u Ad=66p
+ Pd=28u
M_M2 {lo 0 S12 S12 Mp L=1u W=22u As=66p Ps=28u Ad=66p
```

| M_M3 | G56 G34 D9 SS Mn L=1u W=16U As=40p Ps=21u As=40p |
| :---: | :---: |
| + | $\mathrm{Ps}=21 \mathrm{u}$ |
| M_M4 | OUT G34 D10 SS Mn L=1u W=16U As=40p Ps=21u As=40p |
| + | Ps $=21 u$ |
| M_M5 | G56 G56 G78 DD Mp L=1u W=33u As=99p Ps=39u Ad=99p |
| + | Pd=39u |
| M_M6 | OUT G56 S6 DD Mp L=1u W=33u As=99p Ps=39u Ad=99p |
| $+$ | Pd=39u |
| M_M7 | G78 G78 DD DD Mp L=1u W=33u As=99p Ps=39u Ad=99p |
| $+$ | $\mathrm{Pd}=39 \mathrm{u}$ |
| M_M8 | S6 G78 DD DD Mp L=1u W=33u As=99p Ps=39u Ad=99p |
| $+$ | Pd=39u |
| M_M9 | D9 G90 SS SS Mn L=1u W=27U As=68p Ps=33u Ad=68p |
| $+$ | Pd=33u |
| M_M10 | D10 G90 SS SS Mn L=1u W=27.02U As=68p Ps=33u Ad=68p |
| $+$ | Pd=33u |
| C_Cc | V1 VO \{Ccvar\} |
| . INC | _of_Fig_9.11-SCHEMATIC1.par" |

The small-signal ( .TF) analysis gives the following low-frequency parameter values

$$
\begin{equation*}
a_{0}=2679 \mathrm{~V} / \mathrm{V} \quad R_{o}=6.391 \mathrm{M} \Omega \quad g_{m 1}=419 \mu \mathrm{~A} / \mathrm{V} \tag{7.121a}
\end{equation*}
$$

The ac analysis gives the open-loop responses of Fig. 7.99. Using PSpice's cursor facility, we find that the uncompensated response, corresponding to $C_{c}=0$, has

$$
\begin{equation*}
f_{b}=425 \mathrm{kHz} \quad f_{x}=749.5 \mathrm{MHz} \quad \phi_{x}=-131.5^{\circ} \quad \phi_{m}=48.5^{\circ} \tag{7.121b}
\end{equation*}
$$

image_name:FIGURE 7.99
description:The graph in FIGURE 7.99 is a Bode plot showing the open-loop gain (in decibels) versus frequency (in hertz) for an operational amplifier with different values of compensation capacitance, \( C_c \). The x-axis represents frequency on a logarithmic scale ranging from \( 10^4 \) Hz to \( 10^{10} \) Hz, and the y-axis represents the open-loop gain in decibels, ranging from -60 dB to 80 dB.

Overall Behavior and Trends:
- The plot shows three curves, each corresponding to a different value of \( C_c \): 0 pF, 0.2 pF, and 1.0 pF.
- All curves start at a high gain level and decrease as frequency increases, which is typical for a Bode magnitude plot.
- As the compensation capacitance \( C_c \) increases, the bandwidth decreases, shown by the leftward shift of the curves.

Key Features and Technical Details:
- The curve for \( C_c = 0 \) pF has the widest bandwidth, maintaining a higher gain over a broader range of frequencies.
- The curve for \( C_c = 1.0 \) pF shows the most significant reduction in bandwidth, indicating a trade-off between stability (phase margin) and bandwidth.
- The gain crossover frequency, where the gain is 0 dB, shifts to lower frequencies as \( C_c \) increases.

Annotations and Specific Data Points:
- The graph is annotated with arrows indicating the curves for \( C_c = 0 \) pF, 0.2 pF, and 1.0 pF.
- The uncompensated response (\( C_c = 0 \)) corresponds to a higher bandwidth, while the compensated responses show reduced bandwidth but improved phase margin, as explained in the context.

image_name:FIGURE 7.99
description:The graph in FIGURE 7.99 is a Bode plot, showing the phase response of an operational amplifier (op amp) for different values of compensation capacitance \( C_c \). The x-axis represents frequency \( f \) in hertz (Hz), plotted on a logarithmic scale ranging from \( 10^4 \) to \( 10^{10} \) Hz. The y-axis represents the phase of the amplifier's output, measured in degrees, with markings at 0°, -90°, and -180°.

Overall Behavior and Trends:
- The phase response curves downward as frequency increases, indicating a phase lag typical of op amp circuits.
- As the frequency increases, the phase shifts from near 0° to below -90° and approaches -180° at very high frequencies.

Key Features and Technical Details:
- Three distinct curves are shown, each corresponding to a different value of the compensation capacitance \( C_c \): 0 pF, 0.2 pF, and 1.0 pF.
- The curve for \( C_c = 0 \) pF (uncompensated) exhibits the highest bandwidth, maintaining a phase closer to 0° over a broader frequency range before dropping sharply.
- The curve for \( C_c = 0.2 \) pF shows a moderate reduction in bandwidth, with a phase shift occurring at lower frequencies compared to the uncompensated case.
- The \( C_c = 1.0 \) pF curve presents the most significant reduction in bandwidth, with an earlier and more gradual phase shift, indicating improved phase margin.

Annotations and Specific Data Points:
- Arrows on the graph indicate the specific curves for \( C_c = 0 \) pF, 0.2 pF, and 1.0 pF, helping to differentiate the effects of increasing compensation capacitance.
- The annotations highlight the trade-off between stability (phase margin) and bandwidth: as \( C_c \) increases, the phase margin improves at the cost of reduced bandwidth.

This Bode plot effectively illustrates how increasing the compensation capacitance \( C_c \) in an op amp circuit affects the phase response, providing a visual representation of the trade-off between phase margin and bandwidth.

FIGURE 7.99 Magnitude and phase plots for the op amp of Fig. 7.98 for different values of $C_{c}$.

To increase $\phi_{m}$ we deliberately add capacitance to the output node and obtain the curves shown for the cases $C_{c}=0.2 \mathrm{pF}$ and 1 pF . As expected, the price for more phase margin is bandwidth reduction.

EXAMPLE 7.39 (a) Using the above cursor data, estimate the output-node parasitic capacitance $C_{6}$.
(b) Find $C_{c}$ for $\phi_{m}=75^{\circ}$ using the fact that the cursor gives, for the uncompensated response, $f_{-105^{\circ}}=186 \mathrm{MHz}$. What are the ensuing bandwidth $f_{b}$ and GBP? Check with PSpice and comment.

#### Solution

(a) For $C_{c}=0$ we use Eq. (7.119) to impose

$$
425 \times 10^{3}=\frac{1}{2 \pi \times 6.391 \times 10^{6} \times\left(C_{6}+0\right)}
$$

This gives $C_{6}=58.6 \mathrm{fF}$.
(b) Adapting Eq. (7.96) to the present case we write $f_{b}=f_{-105^{\circ}} / a_{0}=186 \times$ $10^{6} / 2679 \cong 69.4 \mathrm{kHz}$. Using again Eq. (7.119),

$$
69.4 \times 10^{3}=\frac{1}{2 \pi \times 6.391 \times 10^{6} \times\left(58.6 \times 10^{-15}+C_{c}\right)}
$$

which gives $C_{c}=300 \mathrm{fF}$ and $\mathrm{GBP}=186 \mathrm{MHz}$. Rerunning PSpice with $C_{c}=0.3 \mathrm{pF}$ we get $f_{b}=69.3 \mathrm{kHz}, \mathrm{GBP}=f_{x}=173 \mathrm{MHz}, \phi_{x}=-108^{\circ}$, and $\phi_{m}=72^{\circ}$, all in reasonable agreement with the calculated values.

### Comparing the Two-Stage and Folded-Cascode Op Amps

The two topologies exhibit similarities as well as differences:

- Both topologies exhibit a dominant pole frequency of the type

$$
f_{b} \propto \frac{1}{2 \pi R M C_{c}}
$$

where $R$ is a suitable resistance, and $M$ is a large multiplier that helps establish a suitably low $f_{b}$ with a compensation capacitance $C_{c}$ that can easily be fabricated on chip. In the two-stage topology it is $C_{c}$ that gets multiplied by $M$ by the Miller effect, whereas in the cascode topology it is $R$ that gets multiplied by $M$ because of cascoding.

- Increasing $C_{c}$ in the two-stage topology has a destabilizing effect because it lowers the RHP zero frequency, thus eroding the phase margin.
- Increasing $C_{c}$ in the cascode topology has a stabilizing effect because it lowers the first pole, thus pushing the phase margin closer to $90^{\circ}$. This makes cascode op amps particularly suited to driving arbitrary capacitive loads as in switchedcapacitor filters.

## 7.10 NOISE

Any disturbance that tends to obscure a signal of interest is generally referred to as noise. A familiar example is hum ("hmmm") in a poorly designed audio system. This noise is injected into the circuit from the outside (in this case from the utility power). Another example is the hiss ("shhh") produced by a low quality audio amplifier and best evidenced when we turn the volume all the way up with no audio input. This is an example of intrinsic noise, so called because it is generated internally by the components (resistors, diodes, and transistors) making up the circuit (conversely, noise injected from the outside is called extrinsic noise). Though we can virtually eliminate extrinsic noise via proper design, layout, and shielding, intrinsic noise is always present in a circuit. It can be reduced via proper component and circuit topology selection, and filtering, but it can never be eliminated entirely.

The most common example of intrinsic noise is resistor noise, which is the result of thermal agitation of the charge carriers (electrons in ordinary resistors and $n$-type materials, holes in $p$-type materials), and is present even if the resistor is sitting in the drawer. Though the voltage across an unconnected resistor averages to zero, its instantaneous value is constantly fluctuating about zero as depicted in Fig. 7.100.

### Basic Noise Properties

Denoting a noise voltage as $e_{n}(t)$ and a noise current as $i_{n}(t)$, we are interested in their root-mean-square (rms) values $E_{n}$ and $I_{n}$ over a time interval $t_{1}$ to $t_{2}$, respectively defined as

$$
\begin{equation*}
E_{n}=\sqrt{\frac{1}{t_{2}-t_{1}} \int_{t_{1}}^{t_{2}} e_{n}^{2}(t) d t} \quad I_{n}=\sqrt{\frac{1}{t_{2}-t_{1}} \int_{t_{1}}^{t_{2}} i_{n}^{2}(t) d t} \tag{7.122}
\end{equation*}
$$

Their physical meanings are that if we play $e_{n}(t)$ across or $i_{n}(t)$ through a resistor $R$, the power dissipated by $R$ is $E_{n}^{2} / R$ or $R I_{n}^{2}$. Alternatively, we say that $E_{n}^{2}$ and $I_{n}^{2}$ represent the power dissipated by $e_{n}(t)$ and $i_{n}(t)$ in a 1- $\Omega$ resistance. Though $e_{n}(t)$ and $i_{n}(t)$ cannot be integrated analytically because they are random variables, $E_{n}$ and $I_{n}$ are easily measured with a true rms multimeter.
image_name:FIGURE 7.100 Oscilloscope display of (suitably magnified) resistor noise.
description:The graph in FIGURE 7.100 is an oscilloscope display depicting resistor noise, specifically a time-domain waveform. The x-axis is labeled 'Time,' while the y-axis is labeled 'Amplitude.' Both axes appear to use a linear scale, although specific units are not provided.

Overall Behavior and Trends:
The waveform exhibits a random pattern characteristic of noise, with no discernible periodicity or regular oscillations. The amplitude fluctuates around a central baseline, showing both positive and negative excursions. The waveform is dense with peaks and troughs, indicating a high level of noise activity over time.

Key Features and Technical Details:
- **Peaks and Valleys:** There are numerous peaks and valleys throughout the waveform, with no single peak dominating the display. The amplitude appears to vary randomly, as expected for noise.
- **Zero Crossings:** The waveform frequently crosses the zero line, consistent with noise signals that have a mean value around zero.

Annotations and Specific Data Points:
There are no specific annotations, markers, or reference lines provided on the graph. The display is typical of a noise signal observed across a resistor, likely magnified to emphasize the noise characteristics.

### Interpretation:
This oscilloscope display illustrates the random nature of resistor noise, which is a common consideration in noise analysis. The graph effectively demonstrates the unpredictable variations in amplitude over time, which are integral to understanding and measuring noise in electrical circuits.

FIGURE 7.100 Oscilloscope display of (suitably magnified) resistor noise.

In the course of noise analysis we often deal with noise voltages in series or noise currents in parallel, so we are interested in the rms value of the combined noise. For the case of a pair of noise voltages $e_{n 1}(t)$ and $e_{n 2}(t)$ in series, the overall rms value is

$$
E_{n}^{2}=\frac{1}{t_{2}-t_{1}} \int_{t_{1}}^{t_{2}}\left[e_{n 1}(t)+e_{n 2}(t)\right]^{2} d t=E_{n 1}^{2}+\frac{2}{t_{2}-t_{1}} \int_{t_{1}}^{t_{2}} e_{n 1}(t) \times e_{n 2}(t) d t+E_{n 2}^{2}
$$

having expanded the quadratic term and then used Eq. (7.122) twice. In most cases of interest $e_{n 1}(t)$ and $e_{n 2}(t)$ are uncorrelated, so their product averages to zero, giving $E_{n}^{2}=E_{n 1}^{2}+E_{n 2}^{2}$. We readily generalize this result to the case of $N$ uncorrelated noise voltages in series or $N$ uncorrelated noise currents in parallel by stating that they combine in rms fashion as

$$
\begin{equation*}
E_{n}=\sqrt{E_{n 1}^{2}+E_{n 2}^{2} \cdots+E_{n N}^{2}} \quad I_{n}=\sqrt{I_{n 1}^{2}+I_{n 2}^{2} \cdots+I_{n N}^{2}} \tag{7.123}
\end{equation*}
$$

### Noise Spectra

The physical meaning of the rms value of noise is similar to the rms value of an ac signal, except that the power of a sinusoid is concentrated at just one frequency whereas noise power is usually spread all over the frequency spectrum. The frequency distribution of noise power is specified via the noise power densities $e_{n}^{2}(f)$ and $i_{n}^{2}(f)$, each representing the average noise power over a $1-\mathrm{Hz}$ bandwidth as a function of frequency $f$. We use the power densities to calculate analytically the rms values over an arbitrary frequency interval $f_{L}$ to $f_{H}$ as

$$
\begin{equation*}
E_{n}=\sqrt{\int_{f_{L}}^{f_{n}} e_{n}^{2}(f) d f} \quad I_{n}=\sqrt{\int_{f_{L}}^{f_{n}} i_{n}^{2}(f) d f} \tag{7.124}
\end{equation*}
$$

Since $E_{n}$ is in V and $f$ in Hz , it follows that $e_{n}^{2}(f)$ is in $\mathrm{V}^{2} / \mathrm{Hz}$; similarly, $i_{n}^{2}(f)$ is in $\mathrm{A}^{2} / \mathrm{Hz}$.
As an example, the power densities of integrated-circuit (IC) noise take on the analytical forms

$$
\begin{equation*}
e_{n}^{2}(f)=e_{n w}^{2}\left(\frac{f_{c e}}{f}+1\right) \quad i_{n}^{2}(f)=i_{n w}^{2}\left(\frac{f_{c i}}{f}+1\right) \tag{7.125}
\end{equation*}
$$

so substituting into Eq. (7.124) and integrating we obtain

$$
\begin{equation*}
E_{n}=e_{n v} \sqrt{f_{c e} \ln \left(\frac{f_{H}}{f_{L}}\right)+f_{H}-f_{L}} \quad I_{n}=i_{n v} \sqrt{f_{c i} \ln \left(\frac{f_{H}}{f_{L}}\right)+f_{H}-f_{L}} \tag{7.126}
\end{equation*}
$$

Data sheets usually show the square roots of the noise power densities, or $e_{n}(f)$ and $i_{n}(f)$. Called, if improperly, the noise voltage and the noise current for short (beware that their units are $\mathrm{nV} / \sqrt{\mathrm{Hz}}$ and $\mathrm{pA} / \sqrt{\mathrm{Hz}}$, not nV and pA ), they are plotted in Fig. 7.101. We make the following observations:

- For $f \gg f_{c e}$ we have $e_{n} \rightarrow e_{n w}$, and for $f \gg f_{c i}$ we have $i_{n} \rightarrow i_{n w}$, indicating highfrequency asymptotes that are constant with frequency. This type of noise is
image_name:(a)
description:The graph labeled (a) in Figure 7.101 is a plot of noise voltage spectral density versus frequency. This is a Bode plot, which is commonly used to represent the frequency response of a system.

1. **Axes Labels and Units:**
- The vertical axis represents the noise voltage $e_n(f)$ in units of nV/√Hz, and it is plotted on a logarithmic scale marked as "dec".
- The horizontal axis represents frequency in hertz (Hz), also on a logarithmic scale marked as "dec".

2. **Overall Behavior and Trends:**
- The graph shows two distinct regions based on frequency:
- For low frequencies (\(f \ll f_{ce}\)), the noise voltage spectral density decreases with a slope of -0.5 dec/dec. This indicates a 1/f noise characteristic, where the noise power is inversely proportional to frequency.
- For high frequencies (\(f \gg f_{ce}\)), the noise voltage approaches a constant value, \(e_{nw}\), indicating white noise behavior where the noise spectral density is flat across frequencies.

3. **Key Features and Technical Details:**
- The cutoff frequency, \(f_{ce}\), marks the transition between the 1/f noise region and the white noise region.
- The asymptotic behavior at high frequencies is constant, representing the white noise floor \(e_{nw}\).

4. **Annotations and Specific Data Points:**
- The slope of -0.5 dec/dec for the low-frequency region is explicitly annotated on the graph.
- The transition point, \(f_{ce}\), and the constant white noise level, \(e_{nw}\), are marked on the plot, though specific numerical values are not provided in the image.
image_name:(b)
description:The graph labeled "(b)" is a plot of noise current spectral density, denoted as $i_n(f)$, versus frequency in Hertz (Hz). The vertical axis represents noise current in picoamperes per square root Hertz (pA/√Hz), and the horizontal axis represents frequency in a logarithmic scale (decades).

Overall Behavior and Trends
- **Low-Frequency Behavior:**
- For frequencies much less than the cutoff frequency $f_{ci}$, the noise current spectral density follows a trend proportional to $1/f$. This is indicated by the slope of -0.5 dec/dec, representing a decrease in noise current as frequency decreases. This behavior suggests a dominance of flicker noise (or 1/f noise) at low frequencies.

- **High-Frequency Behavior:**
- For frequencies much greater than $f_{ci}$, the noise current spectral density approaches a constant value, denoted as $i_{nw}$. This indicates the presence of white noise, where the noise power is uniformly distributed across frequencies.

Key Features and Technical Details
- **Cutoff Frequency ($f_{ci}$):**
- The graph shows a transition around the cutoff frequency $f_{ci}$, where the slope changes from -0.5 dec/dec to a flat line, indicating a shift from flicker noise to white noise.

- **White Noise Floor ($i_{nw}$):**
- At high frequencies, the noise current levels off at $i_{nw}$, which is the white noise floor. This represents the constant spectral density characteristic of white noise.

Annotations and Specific Data Points
- The graph is annotated with the slope of -0.5 dec/dec for the low-frequency region and the horizontal line at $i_{nw}$ for the high-frequency region. There is a vertical reference line at $f_{ci}$, marking the transition between the two noise behaviors.

FIGURE 7.101 Typical spectral densities of integrated circuit noise: (a) noise voltage and (b) noise current.
called white noise by analogy with white light, which contains all frequency components, and $e_{n w}$ and $i_{n w}$ are aptly called white-noise floors.

- For $f \ll f_{c e}$ we have, by Eq. (7.125), $e_{n}^{2}(f) \propto 1 / f$, and for $f \ll f_{c i}$ we have $i_{n}^{2}(f) \propto 1 / f$, indicating low-frequency asymptotes with slopes of $-1 \mathrm{dec} / \mathrm{dec}$. (By contrast, the plots of the square roots of Fig. 7.101 exhibit slopes of $-0.5 \mathrm{dec} / \mathrm{dec}$ ). Noise with a power density inversely proportional to frequency $f$ is aptly called $1 / f$ noise.
- The frequencies $f_{c e}$ and $f_{c i}$, representing the borderlines between $1 / f$ noise and white noise are called the corner frequencies by analogy with filters. As a practical example, the data sheets of the popular 741 op amp give

$$
\begin{equation*}
e_{n w}=20 \mathrm{nV} / \sqrt{\mathrm{Hz}} \quad f_{c e}=200 \mathrm{~Hz} \quad i_{n w}=0.5 \mathrm{pA} / \sqrt{\mathrm{Hz}} \quad f_{c i}=2 \mathrm{kHz} \tag{7.127}
\end{equation*}
$$

(a) Find $E_{n}$ for the 741 op amp over the audio range ( 20 Hz to 20 kHz ).
(b) Repeat, but for the wide-band range of 0.1 Hz to 1 MHz , compare with (a), and comment.

#### Solution

(a) Using Eq. (7.126),

$$
\begin{aligned}
E_{n} & =20 \times 10^{-9} \sqrt{200 \ln \left(\frac{20 \times 10^{3}}{20}\right)+20 \times 10^{3}-20} \\
& \cong 20 \times 10^{-9} \sqrt{1,382+20 \times 10^{3}}=2.92 \mu \mathrm{~V} \mathrm{rms}
\end{aligned}
$$

(b) Likewise,

$$
\begin{aligned}
E_{n} & =20 \times 10^{-9} \sqrt{200 \ln \left(\frac{10^{6}}{0.1}\right)+10^{6}-0.1} \\
& \cong 20 \times 10^{-9} \sqrt{3,224+10^{6}}=20.0 \mu \mathrm{~V} \mathrm{rms}
\end{aligned}
$$

Increasing the bandwidth increases both the $1 / f$ noise and the white noise contributions. However, due to its logarithmic dependence, the $1 / f$ noise contribution increases less noticeably than the white noise contribution, which increases with the square root of the bandwidth.

It is apparent that the lower the noise floor the lower the white noise contribution, and the lower the corner frequency the lower the $1 / f$ noise contribution. A circuit's noise performance strongly depends also on the frequency limits $f_{L}$ and $f_{H}$. Specifically, the $1 / f$ noise contribution is affected by the $\operatorname{ratiof}_{H} / f_{L}$, and the white noise contribution by the difference $f_{H}-f_{L}$. In general $f_{L}$ is taken as the reciprocal of the time interval over which noise is observed or measured (for instance, for an observation time of 10 s we let $f_{L}=1 / 10=0.1 \mathrm{~Hz}$ ). Shortly we shall discuss how the circuit's frequency characteristics establish the value of $f_{H}$. To avoid unnecessary noise, the user may deliberately apply filtering techniques to lower the value of $f_{H}$ to the minimum required by the application at hand (for instance, band-limiting an audio amplifier to 20 kHz will eliminate any noise contribution above that frequency).

### Noise Types

Noise stems from a number of different physical mechanisms. Following are the types of noise most commonly found in electronic devices:

- Thermal noise. As mentioned, this form of noise stems from thermal agitation of the charge carriers in conductors. It is white, and its power density is proportional to absolute temperature T. Also called Johnson noise for John B. Johnson who first investigated it in 1928, it is present in all resistors, whether intentional resistors or parasitic resistors like the bulk resistance of a pn junction, the base-region resistance of a BJT, or the channel resistance of a FET. We model an actual resistor with a noiseless resistance $R$ in series with a noise voltage $e_{n}$, as depicted in Fig. 7.102a. Or, we can perform a source transformation and use a noiseless resistance $R$ in parallel with a noise current $i_{n r}=e_{n r} / R$, as in Fig. 7.102b. The power densities are given by ${ }^{1}$

$$
\begin{equation*}
e_{n r}^{2}=4 k T R \quad i_{n r}^{2}=\frac{4 k T}{R} \tag{7.128}
\end{equation*}
$$

where $k=1.38 \times 10^{-23} \mathrm{~J} / \mathrm{K}$ is Boltzmann's constant. For instance, at room temperature a $1-\mathrm{k} \Omega$ resistor has $e_{n r}=\sqrt{4 \times 1.38 \times 10^{-23} \times 300 \times 10^{3}} \cong 4 \mathrm{nV} / \sqrt{\mathrm{Hz}}$ and $i_{n r}=4 \times 10^{-9} / 10^{3}=4 \mathrm{pA} / \sqrt{\mathrm{Hz}}$. The rms voltage over a 1-MHz bandwidth is $E_{n}=4 \times 10^{-9} \times \sqrt{10^{6}}=4 \mu \mathrm{~V}$ rms.
image_name:(a)
description:
[
name: enr, type: VoltageSource, value: enr, ports: {Np: n1, Nn: n2}
name: R, type: Resistor, value: R, ports: {N1: n2, N2: n3}
]
extrainfo:The circuit diagram (a) represents a resistor noise model consisting of a noiseless resistance R and a series noise voltage source enr.
image_name:(b)
description:
[
name: R, type: Resistor, value: R, ports: {N1: GND, N2: Vout}
name: inr, type: CurrentSource, value: inr, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit diagram (b) represents a resistor noise model with a parallel noise current source 'inr'. The resistor 'R' is connected between the ground and output node 'Vout', with the noise current source 'inr' in parallel.

FIGURE 7.102 Resistor noise models, consisting of a noiseless resistance $R$ and (a) a series noise voltage $e_{n r}$ or (b) a parallel noise current $i_{n r}$.

- Shot Noise. As charge carriers flow across a potential barrier such as that of a $p n$ junction, they produce a current $i(t)$ that is constantly fluctuating around its average value $I$ because of the discrete nature of charge. The power density of these fluctuations is proportional to $I$ according to ${ }^{1}$

$$
\begin{equation*}
i_{n}^{2}=2 q I \tag{7.129}
\end{equation*}
$$

where $q=1.602 \times 10^{-19} \mathrm{C}$ is the electron charge.

- Flicker Noise. Also known as contact noise, this form of noise has various origins, depending on the device type. In transistors it is generally due to traps that capture and release charge carriers randomly as they flow to produce current. The ensuing fluctuations exhibit a power density of the type ${ }^{1}$

$$
\begin{equation*}
i_{n}^{2}=\frac{K I^{a}}{f^{b}} \tag{7.130}
\end{equation*}
$$

where $K$ is a device constant called the flicker coefficient, $I$ is the average current, and $a$ and $b$ are additional device constants with $0.5<a<2$ and $b \cong 1$. Since its power density is (approximately) inversely proportional to frequency $f$, flicker noise is also called $1 / f$ noise. Another name is pink noise, by analogy with pink light, whose power is denser at low frequencies.

- Other Forms of Noise. Another form of low-frequency noise is burst noise, so called because of its appearance when observed on the oscilloscope. Also called popcorn noise because of the sound it produces when played through a loudspeaker, it manifests itself in the presence of heavy metal-ion contaminants, such as gold doping ${ }^{1}$ (we will ignore this form of noise here). Another form of noise is breakdown noise, so called because produced by pn junctions when operated in breakdown.

### Noise Models of Semiconductor Devices

We now wish to develop noise models for semiconductor devices using noiseless devices but equipped with suitable external noise sources, in the manner already seen for the resistor.

- Diode Noise Model. To account for its shot and flicker noise, we model an actual diode with a noiseless $p n$ junction but having a parallel noise current $i_{n d}$ as depicted in Table 7.3. Also shown is a series noise voltage $e_{n r}$ modeling the thermal noise of the diode's bulk resistance $r_{S}$ (see Chapter 1$)$. The power densities of these sources are, respectively, ${ }^{1}$

$$
\begin{equation*}
i_{n d}^{2}=2 q I_{D}+\frac{K I_{D}^{a}}{f} \tag{7.131a}
\end{equation*}
$$

$$
\begin{equation*}
e_{n r}^{2}=4 k T_{S} \tag{7.131b}
\end{equation*}
$$

TABLE 7.3 Noise models and noise power densities for semiconductor devices (the devices in the models are assumed noiseless and noise is accounted for by suitable noise sources, as shown).
COADI
image_name:LOAD1
description:
[
name: enr, type: VoltageSource, ports: {Np: LOAD1, Nn: X1}
name: D, type: Diode, ports: {Na: X1, Nc: GND}
name: ind, type: CurrentSource, ports: {Np: X1, Nn: GND}
]
extrainfo:The circuit consists of a voltage source 'enr', a diode 'D', and a current source 'ind'. The voltage source is connected to node 'LOAD1' and node 'X1'. The diode anode is connected to node 'X1' and cathode to ground. The current source flows from node 'X1' to ground.

LOAD2

$$
\begin{aligned}
& e_{n r}^{2}=4 k T r_{S} \\
& i_{n d}^{2}=2 q I_{D}+\frac{K I_{D}^{a}}{f}
\end{aligned}
$$

$$
\begin{aligned}
& e_{n b}^{2}=4 k T\left(r_{b}+\frac{1}{2 g_{m}}\right) \\
& i_{n b}^{2}=2 q\left(I_{B}+\frac{K I_{B}^{a}}{f}+\frac{I_{C}}{\left|\beta_{0}(j f)\right|^{2}}\right) \\
& i_{n d}^{2}=\frac{K I_{d}^{a}}{f}+4 k T \frac{2}{3} g_{m} \\
& e_{n g}^{2}=\frac{K}{W L C_{o x} f}+4 k T \frac{2}{3} \frac{1}{g_{m}}
\end{aligned}
$$

LOADI
image_name:BJT Noise Model
description:The circuit includes an NMOS transistor, an inductor, and a voltage source. The NMOS transistor M1 is connected with its source and drain at the node labeled LOAD2. The gate of M1 is connected to node P1. The inductor is connected between two points labeled LOAD2. The voltage source eng is connected from the node eng to LOAD2.

- BJT Noise Model. A forward-biased BJT with base current $I_{B}$ and collector current $I_{C}$ exhibits shot-noise power densities of $2 q I_{B}$ at the base and $2 q I_{C}$ at the collector. Dividing $2 q I_{C}$ by $g_{m}^{2}, g_{m}=I_{C} / V_{T}=q I_{C} / k T$, reflects it to the base, where it is added to $4 k T r_{b}$, the thermal noise due to the base's bulk resistance $r_{b}$ (see Chapter 2). The result is the overall base power density ${ }^{1}$

$$
\begin{equation*}
e_{n b}^{2}=4 k T\left(r_{b}+\frac{1}{2 g_{m}}\right) \tag{7.132a}
\end{equation*}
$$

Likewise, dividing $2 q I_{C}$ by $\left|\beta_{0}(j f)\right|^{2}$ reflects it to the base, where it is added to the base's shot noise as well as to the base's flicker noise, to give the overall base power density ${ }^{1}$

$$
\begin{equation*}
i_{n b}^{2}=2 q\left(I_{B}+\frac{K I_{B}^{a}}{f}+\frac{I_{C}}{\left|\beta_{0}(j f)\right|^{2}}\right) \tag{7.132b}
\end{equation*}
$$

where $K$ and $a$ are process-related parameters. The BJT's noise model and relative power densities are summarized in Table 7.3. By Eq. (7.132a), a BJT

produces the same amount of voltage noise as a resistance $R_{e q}=r_{b}+1 /\left(2 g_{m}\right)$. For instance, a BJT with $r_{b}=250 \Omega$ operating at $I_{C}=0.1 \mathrm{~mA}$ has $R_{e q}=250+$ $(26 / 0.1) / 2=380 \Omega$, giving $e_{n b} \cong 2.5 \mathrm{nV} / \sqrt{\mathrm{Hz}}$.

- MOSFET Noise Models. The noise characteristics of a saturated MOSFET are dominated by two noise types: (a) flicker noise, due to the dangling bonds in the channel near the interface with the oxide, which act as traps, randomly capturing and releasing charge carriers as they flow from source to drain; (b) thermal noise, due to the channel's resistance. The noise power density of the drain current is given by ${ }^{1}$

$$
\begin{equation*}
i_{n d}^{2}=\frac{K_{d} I_{D}^{a}}{f}+4 k T \frac{2}{3} g_{m} \tag{7.133a}
\end{equation*}
$$

where $K_{d}$ and $a$ are suitable parameters. Alternatively, we reflect the drain noise to the gate as $e_{n g}^{2}=i_{n d}^{2} / g_{m}^{2}$. The result is expressed in the insightful form ${ }^{1}$

$$
\begin{equation*}
e_{n g}^{2}=\frac{K}{W L C_{o x} f}+4 k T \frac{2}{3} \frac{1}{g_{m}} \tag{7.133b}
\end{equation*}
$$

where $K$ is a process-related constant on the order of $10^{-24} \mathrm{~V}^{2} \mathrm{~F}$. The two MOSFET noise models and relative power densities are summarized in Table 7.3. Flicker noise is inversely proportional to the area $W \times L$, so the IC designer has the option of specifying large-area MOSFETs to keep flicker noise below a prescribed level. Also, $K$ tends to be lower in $p$ MOSFETs than in $n$ MOSFETs as holes are less likely to get trapped than electrons. This is another reason why $p$-channel input stages are preferable. By Eq. (7.133), a MOSFET produces the same amount of voltage noise as a resistance $R_{e q}=2 /\left(3 g_{m}\right)$. For instance, a FET with $g_{m}=1 \mathrm{~mA} / \mathrm{V}$ has $R_{e q}=667 \Omega$, giving $e_{n g} \cong 3.3 \mathrm{nV} / \sqrt{\mathrm{Hz}}$.

### Noise Dynamics

An integrated circuit such as an amplifier consists of a variety of devices, both active and passive, each contributing noise to the output, so finding the individual contributions may be an arduous task. Mercifully, the noise characteristics of the entire circuit can be modeled with just a pair of input noise sources as depicted in Fig. 7.103a. The source $e_{n}$ models the short-circuit input noise because shortcircuiting the input port forces $i_{n}$ to flow through $e_{n}$, so $i_{n}$ has no effect on the output noise, which is thus due exclusively to $e_{n}$. Conversely, the source $i_{n}$ models the opencircuit input noise because open-circuiting the input port eliminates the effect of $e_{n}$ and noise is now due exclusively to $i_{n}$ flowing through the circuit's input impedance.

Once we embed an amplifier in a circuit, we are interested in its total rms output noise $E_{n o}$ for the case of a voltage-output type, or in $I_{n o}$ for a current-output type (by total we mean over the frequency interval $f_{L}<f<\infty$ ). To this end, we first combine the effects of $e_{n}$ and $i_{n}$ into a single equivalent input source $e_{n i}(f)$ for a voltage-input type, or $i_{n i}(f)$ for a current-input type. Next, we multiply this input source by the
image_name:(a)
description:The diagram labeled "(a)" represents the noise model of an amplifier system. It consists of the following main components:

1. **Input Noise Sources:**
- **Voltage Noise Source (e<sub>n</sub>):** This is depicted as a voltage source symbol, representing the inherent voltage noise present at the input of the amplifier.
- **Current Noise Source (i<sub>n</sub>):** This is shown as a current source symbol, representing the inherent current noise at the input.

2. **Noiseless Amplifier:**
- This block is labeled "Noiseless amplifier," indicating that it amplifies the input signal without adding any additional noise of its own.

3. **Connections:**
- The input side is connected to both the voltage and current noise sources, which are in parallel. These noise sources are then fed into the noiseless amplifier.
- The output of the noiseless amplifier provides the amplified signal, which is free from additional noise introduced by the amplifier itself.

**Flow of Information:**
- The signal flow starts at the input, where the noise sources (e<sub>n</sub> and i<sub>n</sub>) are combined and fed into the noiseless amplifier.
- The amplifier processes the combined noise input and outputs an amplified signal.

**Overall System Function:**
- The primary function of this system is to model the noise behavior of an amplifier. By representing the input noise sources and assuming a noiseless amplification process, the diagram helps in analyzing how input noise affects the overall output of the amplifier system. This model is crucial for understanding and calculating the total noise performance of an amplifier in a circuit.
image_name:The circuit diagram (b) represents a noise model of an amplifier where the total input noise voltage eni(f) is amplified by the noise gain |An(jf)| to produce the output noise voltage eno(f).

FIGURE 7.103 (a) Noise model of an amplifier. (b) Circuit for the calculation of the output noise voltage $e_{n o}$ of a voltage amplifier with total input noise voltage $e_{n i}$ and noise gain $A_{n}$.
circuit's noise gain to obtain the output noise. For example, in the case of the voltagetype amplifier exemplified in Fig. $7.103 b$ we write $e_{n o}(f)=\left|A_{n}(j f)\right| e_{n i}(f)$, where $A_{n}(j f)$ is the noise gain, in V/V. Finally, we adapt Eq. (7.124) to find the total rms output noise above some prescribed frequency $f_{L}$ as

$$
\begin{equation*}
E_{n o}=\sqrt{\int_{f_{L}}^{\infty}\left|A_{n}(j f)\right|^{2} e_{n i}^{2}(f) d f} \tag{7.134}
\end{equation*}
$$

Most noise gains of interest are dominated by a single pole, or

$$
\begin{equation*}
A_{n}(j f)=\frac{A_{n 0}}{1+j f / f_{B}} \tag{7.135}
\end{equation*}
$$

where $A_{n 0}$ is the dc gain and $f_{B}$ is the $-3-\mathrm{dB}$ frequency. We are interested in two special cases, namely, the case of white input noise and the case of $1 / f$ input noise.

- White-Noise Equivalent Bandwidth (NEB). Assuming $e_{n i}(f)=e_{n i v}$, we combine Eqs. (7.134) and (7.135) and obtain (see Problem 7.74)
$E_{n o}=A_{n 0} e_{n i w} \sqrt{\int_{f_{L}}^{\infty} \frac{d f}{1+\left(f / f_{B}\right)^{2}}}=A_{n 0} e_{n i w} \sqrt{f_{B}\left(\tan ^{-1} \infty-\tan ^{-1} \frac{f_{L}}{f_{B}}\right)}=A_{n 0} e_{n i w} \sqrt{\text { NEB }}$
where

$$
\begin{equation*}
\mathrm{NEB}=f_{B}\left(\frac{\pi}{2}-\tan ^{-1} \frac{f_{L}}{f_{B}}\right) \tag{7.136}
\end{equation*}
$$

is the white-noise equivalent bandwidth. Situations of practical interest are such that $f_{L} \ll f_{B}$, indicating that we can approximate $\tan ^{-1}\left(f_{L} / f_{B}\right) \cong f_{L} / f_{B}$ in Eq. (7.136). Consequently,

$$
\begin{equation*}
\mathrm{NEB} \cong 1.57 f_{B}-f_{L} \tag{7.137}
\end{equation*}
$$

We observe that if $\left|A_{n}(\mathrm{jf})\right|$ rolled off sharply (brick-wall type) at $f_{B}$, then $f_{H}$ would coincide with $f_{B}$ itself. However, because the rolloff is gradual (1st order), the noise above $f_{B}$ provides an additional contribution of $57 \%$.

- Brick-Wall Equivalent for Flicker Noise. Assuming $e_{n i}^{2}(f)=K I / f$, we again combine Eqs. (7.134) and (7.135) and obtain (see Problem 7.74)

$$
E_{n o}=A_{n 0} \sqrt{\int_{f_{L}}^{\infty} \frac{K I d f}{f\left[1+\left(f / f_{B}\right)^{2}\right]}}=A_{n 0} \sqrt{K I \ln \frac{f_{B} \sqrt{1+\left(f_{L} / f_{B}\right)^{2}}}{f_{L}}}=A_{n 0} \sqrt{K I \ln \frac{f_{H}}{f_{L}}}
$$

where

$$
\begin{equation*}
f_{H}=f_{B} \sqrt{1+\left(f_{L} / f_{B}\right)^{2}} \tag{7.138}
\end{equation*}
$$

In words, passing above- $f_{L}$-flicker-noise through a 1 st-order low-pass filter with $-3-\mathrm{dB}$ of $f_{B}$ is equivalent to passing it through a brick-wall filter with a cutoff frequency of $f_{H}$ as given above. Situations of practical interest are such that $f_{L} \ll f_{B}$, so we approximate the above expression as

$$
\begin{equation*}
f_{H} \cong f_{B} \tag{7.139}
\end{equation*}
$$

(a) A $p n$ junction with $r_{S} \cong 0, K=5 \times 10^{-17} \mathrm{~A}$, and $a=1$ is forward-biased at $I_{D}$ $=100 \mu \mathrm{~A}$ by means of a noiseless current source. Find the rms noise voltage $E_{n}$ across its terminals from 0.1 Hz to 1 MHz .
(b) Find a capacitance $C$ that, when placed across its terminals, will limit $E_{n}$ to $1.0 \mu \mathrm{~V} \mathrm{rms}$.

#### Solution

(a) By Eq. $(7.131 a)$ we have

$$
\begin{aligned}
i_{n d}^{2} & =2 \times 1.602 \times 10^{-19} \times 100 \times 10^{-6}+\frac{5 \times 10^{-17} \times 100 \times 10^{-6}}{f} \\
& =(5.66 \mathrm{pA})^{2}\left(\frac{156}{f}+1\right)
\end{aligned}
$$

The noise voltage across the junction is $e_{n d}=r_{d} i_{n d}$, where $=r_{d}=26 / 0.1=$ $260 \Omega$, so

$$
e_{n d}^{2}=\left(260 \times 5.66 \times 10^{-12}\right)^{2}\left(\frac{156}{f}+1\right)=(1.472 \mathrm{nV})^{2}\left(\frac{156}{f}+1\right)
$$

Using Eq. (7.126) we get

$$
E_{n} \cong(1.472 \mathrm{nV}) \sqrt{156 \ln \left(\frac{10^{6}}{0.1}\right)+10^{6}} \cong(1.472 \mathrm{nV}) \sqrt{10^{6}}=1.47 \mu \mathrm{~V} \mathrm{rms}
$$

indicating that flicker noise is negligible in this case.
(b) Placing a capacitor $C$ in parallel with the junction establishes a pole frequency at $f_{B}=1 /\left(2 \pi r_{d} C\right)$. Since flicker noise is negligible, we impose

$$
(1.472 \mathrm{nV}) \sqrt{1.57 f_{B}}=1.0 \mu \mathrm{~V}
$$

to obtain $f_{B}=294 \mathrm{kHz}$. Finally, $C=1 /\left(2 \pi r_{d} f_{B}\right)=1 /(2 \pi \times 260 \times 294 \times$ $\left.10^{3}\right) \cong 2.1 \mathrm{nF}$.

### An Op Amp Circuit Example

The op amp circuit of Fig. 7.104a is a classic benchmark for noise calculations. No input signals are shown, so whatever emerges from the output is just noise. (The circuit is fairly general in that, depending on where we apply the input or inputs, it could be an inverting amplifier, a noninverting amplifier, a summing or a difference amplifier, a buffer, an I-V converter, and so forth.) We wish to find the total output noise $E_{n o}$ assuming an op amp with a constant GBP product of $f_{t}$ and the spectral densities of Eq. 7.126. To this end we redraw the circuit as in Fig. 7.104b, showing all noise sources explicitly. Since the op amp is a differential-input device, both noise currents $i_{n n}$ and $i_{n p}$ must be shown (however, the individual noise voltages are lumped together into a single source $e_{n}$ in series with just one of the inputs). Additionally, we must show the noise of each resistor (we use either the series or the parallel model, depending on which one makes the calculations easier). Next, we combine the effects of all sources into a single input source $e_{n i}$ as shown in Fig. 7.104c. Finally, we apply Eq. (7.134) to find $E_{n o}$.

The feedback factor is $\beta=R_{1} /\left(R_{1}+R_{2}\right)$, so $A_{n 0}=1 / \beta$ and $f_{B}=\beta f_{i}$, or

$$
\begin{equation*}
A_{n 0}=1+\frac{R_{2}}{R_{1}} \quad f_{B}=\frac{f_{t}}{1+R_{2} / R_{1}} \tag{7.140}
\end{equation*}
$$

To find the contributions to $e_{n i}$ by $e_{3}, e_{n}$, and $i_{n p}$, we observe that $R_{3}$ and $i_{n p}$ produce the noise voltage $R_{3} i_{n p}$, so their power densities combine as

$$
e_{3}^{2}+e_{n}^{2}+R_{3}^{2} i_{n p}^{2}=4 k T R_{3}+e_{n}^{2}+R_{3}^{2} i_{n p}^{2}
$$

where Eq. (7.128) has been used. To find the contributions to $e_{n i}$ by $i_{1}, i_{2}$, and $i_{n n}$, set $e_{3}, e_{n}$, and $i_{n p}$ to zero. This forces the inverting node to virtual ground, causing
image_name:(a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: GND, N2: InN(A1)}
name: R2, type: Resistor, value: R2, ports: {N1: InN(A1), N2: Eno}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Eno, OutN: GND}
name: R3, type: Resistor, value: R3, ports: {N1: InP(A1), N2: GND}
]
extrainfo:The circuit diagram (a) represents a generalized resistive-type operational amplifier circuit with noise sources. It includes resistors (R1, R2, R3), an operational amplifier (A1), and various noise sources (current and voltage). The resistors are connected to the inverting and non-inverting inputs of the op-amp, with noise contributions analyzed through different configurations.
image_name:(b)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: GND, N2: InN(A1)}
name: R2, type: Resistor, value: R2, ports: {N1: InN(A1), N2: Eno}
name: R3, type: Resistor, value: R3, ports: {N1: x2, N2: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Eno}
name: i1, type: CurrentSource, value: i1, ports: {Np: GND, Nn: InN(A1)}
name: i2, type: CurrentSource, value: i2, ports: {Np: InN(A1), Nn: Eno}
name: inn, type: CurrentSource, value: inn, ports: {Np: GND, Nn: InN(A1)}
name: inp, type: CurrentSource, value: inp, ports: {Np: GND, Nn: InP(A1)}
name: en, type: VoltageSource, value: en, ports: {Np: X1, Nn: InP(A1)}
name: e3, type: VoltageSource, value: e3, ports: {Np: X1, Nn: X2}
]
extrainfo:The circuit in diagram (b) is a noise analysis model of a resistive-type op-amp circuit. It includes various noise sources such as current and voltage sources, which are used to model the noise contributions from different parts of the circuit. The op-amp A1 is configured with resistors R1, R2, and R3, and noise sources are connected to both the inverting and non-inverting inputs. The output node is labeled as Eno. This model helps in analyzing the impact of noise on the overall circuit performance.
image_name:(c)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: GND, N2: InN(A1)}
name: R2, type: Resistor, value: R2, ports: {N1: InN(A1), N2: Eno}
name: R3, type: Resistor, value: R3, ports: {N1: X1, N2: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Eno, OutN: '}
name: eni, type: VoltageSource, value: eni, ports: {Np: InP(A1), Nn: X1'}
]
extrainfo:The circuit diagram (c) shows a resistive-type op-amp circuit with noise voltage sources. The op-amp A1 is configured with resistors R1, R2, and R3, and a noise voltage source eni connected to the non-inverting input. The output is labeled as Eno.

FIGURE 7.104 (a) Generalized resistive-type op amp circuit. (b) Redrawing the circuit with all noise sources explicitly shown. (c) Noise model after all sources have been combined into a single noise voltage $e_{n}$.
$i_{1}, i_{2}$, and $i_{n n}$ to flow through $R_{2}$ and thus yield the power density $R_{2}^{2}\left(i_{1}^{2}+i_{2}^{2}+i_{n n}^{2}\right)$ at the output. To find its contribution to $e_{n i}$, we must reflect the output power density to the noninverting input by dividing it by $A_{n 0}^{2}$. So, the contributions by $i_{1}, i_{2}$, and $i_{n n}$ are

$$
\begin{aligned}
\frac{R_{2}^{2}\left(i_{1}^{2}+i_{2}^{2}+i_{n n}^{2}\right)}{A_{n 0}^{2}} & =\frac{R_{2}^{2}\left(i_{1}^{2}+i_{2}^{2}+i_{n n}^{2}\right)}{\left(1+R_{2} / R_{1}\right)^{2}}=\left(R_{1} / / R_{2}\right)^{2}\left(i_{1}^{2}+i_{2}^{2}+i_{n n}^{2}\right) \\
& =4 k T\left(R_{1} / / R_{2}\right)+\left(R_{1} / / R_{2}\right)^{2} i_{n n}^{2}
\end{aligned}
$$

where Eq. (7.128) has been used again. Combining all contributions gives the total input power density

$$
\begin{equation*}
e_{n i}^{2}=4 k T\left[R_{3}+\left(R_{1} / / R_{2}\right)\right]+e_{n}^{2}+R_{3}^{2} i_{n p}^{2}+\left(R_{1} / / R_{2}\right)^{2} i_{n n}^{2} \tag{7.141}
\end{equation*}
$$

Finally, we substitute into Eq. (7.134) and write

$$
\begin{equation*}
E_{n o}=\sqrt{E_{r}^{2}+E_{n}^{2}+E_{n p}^{2}+E_{n n}^{2}} \tag{7.142}
\end{equation*}
$$

where $E_{r}, E_{n}, E_{n p}$ and $E_{n n}$ represent, respectively, the noise contributions by the resistances, $e_{n}, i_{n p}$, and $i_{n n}$. Applying Eq. (7.126) with $\mathrm{NEB}_{\text {white }}=1.57 f_{B}$ and $\mathrm{NEB}_{\text {flicker }} \cong f_{B}$, and ignoring $f_{L}$ compared to $1.57 f_{B}$, gives

$$
\begin{align*}
E_{r} & \cong A_{n 0} \sqrt{4 k T\left[R_{3}+\left(R_{1} / / R_{2}\right)\right] \times 1.57 f_{B}}  \tag{7.143a}\\
E_{n} & \cong A_{n 0} e_{n w} \sqrt{f_{c e} \ln \frac{f_{B}}{f_{L}}+1.57 f_{B}}  \tag{7.143b}\\
E_{n p} & \cong A_{n 0} R_{3} i_{n p w} \sqrt{f_{c i p} \ln \frac{f_{B}}{f_{L}}+1.57 f_{B}}  \tag{7.143c}\\
E_{n n} & \cong A_{n 0}\left(R_{1} / / R_{2}\right) i_{n n w} \sqrt{f_{c i n} \ln \frac{f_{B}}{f_{L}}+1.57 f_{B}} \tag{7.143d}
\end{align*}
$$

The above derivations for voltage-type amplifiers are easily generalized to other amplifier types such as current, transresistance, and transconductance amplifiers (see the end-of-chapter problems).
(a) If the circuit of Fig. 7.104 uses a 741 op amp with $R_{1}=20 \mathrm{k} \Omega, R_{2}=180 \mathrm{k} \Omega$, and $R_{3}=18 \mathrm{k} \Omega$, find the rms output noise above 0.1 Hz . Compare the different noise components and comment.
(b) What happens if all resistances are simultaneously scaled to one-tenth of their original value? How would you scale the resistances in order to minimize output noise? What would the minimum be?

#### Solution

(a) We have $A_{n 0}=1+180 / 20=10 \mathrm{~V} / \mathrm{V}$ and $f_{B}=10^{6} / 10=10^{5} \mathrm{~Hz}$. Using Eq. (7.143) with the data of Eq. (7.127), and then substituting into Eq. (7.142), we find

$$
\begin{aligned}
& E_{r}= 10 \sqrt{4 \times 1.38 \times 10^{-23} \times 300 \times(18+18) 10^{3} \times 1.57 \times 10^{5}} \\
&= 96.7 \mu \mathrm{~V} \mathrm{rms} \\
& E_{n}= 10 \times 20 \times 10^{-9} \sqrt{200 \times \ln \frac{10^{5}}{0.1}+1.57 \times 10^{5}}=79.9 \mu \mathrm{~V} \mathrm{rms} \\
& E_{n p}= E_{n n}=10 \times 18 \times 10^{3} \times 0.5 \\
& \quad \times 10^{-12} \sqrt{2 \times 10^{3} \times \ln \frac{10^{5}}{0.1}+1.57 \times 10^{5}}=38.7 \mu \mathrm{~V} \mathrm{rms} \\
& \\
& E_{n o}= \sqrt{96.7^{2}+79.9^{2}+2 \times 38.7^{2}} \cong 137 \mu \mathrm{~V} \mathrm{rms}
\end{aligned}
$$

It is apparent that resistor noise dominates in this circuit, followed by op amp voltage noise, in turn followed by op amp current noise.
(b) Reducing all resistances to $1 / 10$ of their original values leaves $A_{n 0}, f_{B}$, and $E_{n}$ unchanged while reducing both $E_{n p}$ and $E_{n n}$ to $1 / 10$, or to $3.87 \mu \mathrm{~V} \mathrm{rms}$, which is negligible compared to $E_{n}$. However, because of the square-root dependence, $E_{r}$ is reduced only to $1 / \sqrt{10}$, or to $96.7 / \sqrt{10}=30.6 \mu \mathrm{~V} \mathrm{rms}$, giving $E_{n o} \cong \sqrt{30.6^{2}+79.9^{2}} \cong 85 \mu \mathrm{~V} \mathrm{rms}$. We can minimize noise by scaling all resistances further, until the condition $E_{r} \ll E_{n}$ is met, at which point $E_{n o} \cong$ $E_{n} \cong 80 \mu \mathrm{~V} \mathrm{rms}$. Of course, the price for smaller resistances is an increase in power dissipation.

High-gain amplifiers such as op amps and voltage comparators utilize a differential pair as the input stage. Since its noise adds directly to the useful input signals, its noise performance is usually critical (by contrast, a subsequent stage tends to be less critical because its noise, reflected to the input, gets divided by the gains of the preceding stages, as discussed in Section 7.2). It is therefore appropriate that we investigate the noise performance of differential pairs in detail.

### Noise in CMOS Differential Stages

We wish to model the noise characteristics of a CMOS differential stage with a single input source $e_{n}$ as in Fig. 7.105a, given the individual noise sources of Fig. 7.105b. To find $e_{n}$, we first calculate the short-circuit noise current $i_{n o}$ at the output, then we divide it by the circuit's transconductance $g_{m}$ to reflect it to the input and thus get $e_{n}=i_{n o} / g_{m}$. We use the superposition principle to find the power density contribution by each FET acting alone and then we add up all contributions to obtain $i_{n o}^{2}$.

By inspection, the contributions to $i_{n o}^{2}$ by $M_{1}$ and $M_{2}$ are, respectively, $g_{m 1}^{2} e_{n 1}^{2}$ and $g_{m 2}^{2} e_{n 2}^{2}$ (note that polarity inversion by one of the inputs is inconsequential because of the randomness of noise). Next, we find the contributions by $M_{3}$ and $M_{4}$ by setting
image_name:(a)
description:
[
name: M1, type: PMOS, ports: {S: X1, D: X2, G: V1}
name: M2, type: PMOS, ports: {S: X1, D: d2d4, G: GND}
name: M3, type: NMOS, ports: {S: VSS, D: X2, G: X2}
name: M4, type: NMOS, ports: {S: VSS, D: d2d4, G: X2}
name: M5, type: PMOS, ports: {S: VDD, D: X1, G: VG5}
name: en, type: VoltageSource, value: en, ports: {Np: V1, Nn: GND}
]
extrainfo:The circuit is an active-loaded CMOS differential stage with PMOS transistors M1, M2, an d M5, and NMOS transistors M3 and M4. It includes voltage sources V1 and en. The circuit is used to analyze noise contributions from individual transistors.
image_name:(b)
description:
[
name: M1, type: PMOS, ports: {S: X1, D: X2, G: V1}
name: M2, type: PMOS, ports: {S: X1, D: GND, G: V2}
name: M3, type: NMOS, ports: {S: GND, D: x2, G: V3}
name: M4, type: NMOS, ports: {S: GND, D: GND, G: v4}
name: M5, type: PMOS, ports: {S: GND, D: X1, G: v5}
name: V1, type: VoltageSource, value: V1, ports: {Np: GND, Nn: X2}
name: V2, type: VoltageSource, value: V2, ports: {Np: v2, Nn: GND}
name: V3, type: VoltageSource, value: V3, ports: {v5: GND, Nn: GND}
]
extrainfo:The circuit represents a noise model of an active-loaded CMOS differential stage. It includes contributions from individual FETs to the output noise current. The circuit uses superposition to analyze noise contributions, where M3 and M4 are connected in series with noise sources referenced to AC ground.

FIGURE 7.105 (a) Noise model of an active-loaded CMOS differential stage (all FETs in the model are assumed noiseless). (b) Noise circuit to find the individual FET contribution to the output noise current $i_{n o}$.
$e_{n 1}=e_{n 2}=e_{n 5}=0$. These conditions place $M_{3}$ 's gate at ac ground, so $M_{3}$ does not contribute noise directly. Rather, it contributes indirectly via $M_{4}$ because $e_{n 3}$ appears in series with $e_{n 4}$ and $e_{n 3}$ is referenced to ac ground. Consequently, $M_{4}$ contributes to $i_{n o}^{2}$ the power density $g_{m 4}^{2}\left(e_{n 3}^{2}+e_{n 4}^{2}\right)$. Finally, we observe that $e_{n 5}$ appears as a common-mode signal, so in a well-designed differential pair its contribution tends to be negligible compared to the others because the common-mode gain is usually very small. Summarizing, we have

$$
\begin{aligned}
i_{n o}^{2} & =g_{m 1}^{2} e_{n 1}^{2}+g_{m 2}^{2} e_{n 2}^{2}+g_{m 4}^{2}\left(e_{n 3}^{2}+e_{n 4}^{2}\right)=g_{m p}^{2}\left(e_{n p}^{2}+e_{n p}^{2}\right)+g_{m n}^{2}\left(e_{n n}^{2}+e_{n n}^{2}\right) \\
& =2\left(g_{m p}^{2} e_{n p}^{2}+g_{m n}^{2} e_{n n}^{2}\right)
\end{aligned}
$$

where the subscripts have been changed to $p$ and $n$ to identify $p$-channel and $n$-channel parameters. Dividing $i_{n o}^{2}$ by $g_{m p}^{2}$ reflects it to the input, giving

$$
e_{n}^{2}=2\left(e_{n p}^{2}+\frac{g_{m n}^{2}}{g_{m p}^{2}} e_{n n}^{2}\right)
$$

Combining with Eq. (7.133b) we obtain the more explicit expression

$$
e_{n}^{2}=2\left[\frac{K_{p}}{W_{p} L_{p} C_{o x} f}+4 k T_{\frac{2}{3}} \frac{1}{g_{m p}}+\frac{g_{m n}^{2}}{g_{m p}^{2}}\left(\frac{K_{n}}{W_{n} L_{n} C_{o x} f}+4 k T \frac{2}{3} \frac{1}{g_{m n}}\right)\right]
$$

where $K_{p}$ and $K_{n}$ are the flicker-noise coefficients of the $p$-type and $n$-type FETs. Regrouping terms and using $g_{m n}^{2} / g_{m p}^{2}=\left(2 k_{n} I_{D n}\right) /\left(2 k_{p} I_{D p}\right)=k_{n} / k_{p}=\left(\mu_{n} W_{n} / L_{n}\right) /\left(\mu_{p} W_{p} / L_{p}\right)$, we put the above expression in the more insightful form

$$
\begin{equation*}
e_{n}^{2}=e_{n(\text { thermal) }}^{2}+e_{n(\text { ficker })}^{2} \tag{7.144}
\end{equation*}
$$

where the term

$$
\begin{equation*}
e_{n \text { (thermal) }}^{2}=\frac{16}{3} k T \frac{1}{g_{m p}}\left(1+\frac{g_{m n}}{g_{m p}}\right) \tag{7.145}
\end{equation*}
$$

represents the thermal component of $e_{n}^{2}$, and the term

$$
\begin{equation*}
e_{n \text { (ficker) }}^{2}=\frac{2 K_{p}}{W_{p} L_{p} C_{o x} f}\left(1+\frac{K_{n}}{K_{p}} \frac{\mu_{n}}{\mu_{p}} \frac{L_{p}^{2}}{L_{n}^{2}}\right) \tag{7.146}
\end{equation*}
$$

represents the flicker component. We make the following observations:

- The term $(16 / 3) k T / g_{m p}$ in Eq. (7.145) represents the thermal noise of the differential pair acting alone.
- The presence of the active load augments this noise by the ratio $g_{m n} / g_{m p}$. For instance, if $g_{m n} / g_{m p}=1$, the presence of the load doubles the power density of the differential pair.
- Designing for $g_{m p} \gg g_{m n}$ will minimize the effect of the load, making $e_{n \text { (thermal })}^{2}$ approach the thermal noise of only the differential pair.
- If desirable, we can reduce the differential-pair noise by designing for a suitably large $g_{m p}$.
- The term $2 K_{p} /\left(W_{p} L_{p} C_{o x} f\right)$ in Eq. (7.146) represents the flicker noise of the differential pair alone.
- The presence of the active load augments this noise by the ratio $\left(K_{n} \mu_{n} L_{p}^{2}\right) /\left(K_{p} \mu_{p} L_{n}^{2}\right)$. (Interestingly, this augmentation depends only on the channel lengths, regardless of the channel widths.)
- Designing for $K_{p} \mu_{p} L_{n}^{2} \gg K_{n} \mu_{n} L_{p}^{2}$ will minimize the effect of the load, in turn making $e_{n \text { (ficker })}^{2}$ approach the flicker noise of only the differential pair.
- If desirable, we can reduce the differential-pair noise by designing for a suitably large area $W_{p} L_{p}$.

### Noise in Bipolar Differential Pairs

We wish to find an expression for the sources modeling the noise characteristics of the bipolar differential pair of Fig. 7.106 $a$. To find the short-circuit noise $e_{n}$, refer to the circuit of Fig. 7.106b, whose inputs have been grounded to blank out the noise currents and leave active only the noise voltages. Assuming $r_{o} \gg R_{C}$, the voltage noise gain is $g_{m} R_{C}$, so we write, by inspection,

$$
e_{n o}^{2}=g_{m 1}^{2} R_{C}^{2} e_{n 1}^{2}+g_{m 2}^{2} R_{C}^{2} e_{n 2}^{2}+e_{r 1}^{2}+e_{r 2}^{2}=2\left[g_{m}^{2} R_{C}^{2} e_{n 1}^{2}+4 k T R_{C}\right]
$$

having ignored the source $e_{n 3}$ because of the high CMRR of this circuit. Reflecting $e_{n o}^{2}$ to the input gives

$$
e_{n}^{2}=\frac{e_{n o}^{2}}{g_{m}^{2} R_{C}^{2}}=2\left[e_{n 1}^{2}+\frac{4 k T}{g_{m}^{2} R_{C}}\right]
$$

Substituting the expression of Eq. (7.132a) for $e_{n 1}^{2}$ we get, after minor algebra,

$$
e_{n}^{2}=2\left[4 k T\left(r_{b}+\frac{1}{2 g_{m}}+\frac{1}{\left(g_{m} R_{C}\right) g_{m}}\right)\right]
$$

image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: Voutn, B: Vin, E: P}
name: Q2, type: NPN, ports: {C: Voutp, B: Vip, E: P}
name: Q3, type: NPN, ports: {C: P, B: Vb3, E: VEE}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Voutn}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Voutp}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: VEE, type: VoltageSource, value: VEE, ports: {Np: GND, Nn: VEE}
name: en, type: VoltageSource, value: en, ports: {Np: Vi2, Nn: Vip}
name: inn, type: CurrentSource, value: inn, ports: {Np: Vin, Nn: GND}
name: inp, type: CurrentSource, value: inp, ports: {Np: Vip, Nn: GND}
]
extrainfo:The circuit diagram (a) represents a resistive-loaded bipolar differential pair with transistors Q1, Q2, and Q3. It is designed to have high CMRR, which allows ignoring certain noise sources. The differential pair is powered by VCC and VEE, with outputs at Voutn and Voutp. Noise sources are modeled with en, inn, and inp.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: eno+, B: V1, E: P}
name: Q2, type: NPN, ports: {C: eno-, B: V2, E: P}
name: Q3, type: NPN, ports: {C: P, B: en3, E: GND}
name: RC, type: Resistor, value: RC, ports: {N1: x1, N2: x2}
name: RC, type: Resistor, value: RC, ports: {N1: x1, N2: x3}
name: en1, type: VoltageSource, value: en1, ports: {Np: V1, Nn: GND}
name: er1, type: VoltageSource, value: er1, ports: {Np: x2, Nn: eno+}
name: er2, type: VoltageSource, value: er2, ports: {Np: x3, Nn: eno-}
name: en3, type: VoltageSource, value: en3, ports: {Np: en3, Nn: GND}
name: en2, type: VoltageSource, value: en1, ports: {Np: V2, Nn: GND}
]
extrainfo:The circuit is a noise model of a resistive-loaded bipolar differential pair. It is designed to analyze noise sources in the circuit, specifically focusing on devices Q1, Q2, and Q3. The circuit accounts for noise voltages and currents at various nodes and is used to understand the noise behavior in differential amplifiers.
image_name:(c)
description:
[
name: Q1, type: NPN, ports: {C: Voutn, B: V1, E: P}
name: Q2, type: NPN, ports: {C: Voutp, B: V2, E: P}
name: Q3, type: NPN, ports: {C: P, B: V3, E: GND}
name: RC, type: Resistor, value: RC, ports: {N1: Voutn, N2: GND}
name: RC, type: Resistor, value: RC, ports: {N1: Voutp, N2: GND}
name: en3, type: VoltageSource, value: en3, ports: {Np: V3, Nn: GND}
name: in1, type: CurrentSource, value: in1, ports: {Np: V1, Nn: GND}
name: in2, type: CurrentSource, value: in2, ports: {Np: V2, Nn: GND}
name: ir1, type: CurrentSource, value: ir1, ports: {Np: Voutn, Nn: GND}
name: ir2, type: CurrentSource, value: ir2, ports: {Np: Voutp, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with three NPN transistors (Q1, Q2, Q3) and resistive loads (RC). It includes noise voltage sources (en3) and current sources (in1, in2, ir1, ir2) to model various noise and signal contributions.

FIGURE 7.106 (a) Noise model of a resistive-loaded bipolar differential pair (the transistors and resistors in the model are assumed noiseless). Noise circuits to find (a) $e_{n}$ and (b) $i_{n n}$ and $i_{n p}$.

But a well-designed differential amplifier has $g_{m} R_{C} \gg 2$, so the above expression reduces to

$$
\begin{equation*}
e_{n}^{2} \cong 2 \times 4 k T\left(r_{b}+\frac{1}{2 g_{m}}\right)=2 e_{n b}^{2} \tag{7.147}
\end{equation*}
$$

It is apparent that the noise of the resistive load tends to play an insignificant role, though this is not necessarily true in the case of an active load (see Problem 7.85).

To find the open-circuit noise currents $i_{n n}$ and $i_{n p}$, refer to the circuit of Fig. 7.106c, whose inputs have been left floating to blank out the effect of the noise voltages and enable only that of the noise currents. We find $i_{n n}$ by reflecting $i_{r 1}$ to $Q_{1}$ 's base and then combining it with $i_{n 1}$. Since the current noise gain is $\left|\beta_{0}(j f)\right|$, we get

$$
i_{n n}^{2}=i_{n 1}^{2}+\frac{i_{r 1}^{2}}{\left|\beta_{0}(j f)\right|^{2}}=i_{n 1}^{2}+\frac{4 k T / R_{C}}{\left|\beta_{0}(j f)\right|^{2}}
$$

Substituting the expression of Eq. (7.132b) for $i_{n 1}^{2}$ we get

$$
\begin{equation*}
i_{n n}^{2}=2 q\left(I_{B}+\frac{K I_{B}^{a}}{f}+\frac{I_{C}}{\left|\beta_{0}(j f)\right|^{2}}\right)+\frac{4 k T / R_{C}}{\left|\beta_{0}(j f)\right|^{2}}=2 q\left(I_{B}+\frac{K I_{B}^{a}}{f}+\frac{I_{C}+2 V_{T} / R_{C}}{\left|\beta_{0}(j f)\right|^{2}}\right) \cong i_{n b}^{2} \tag{7.148}
\end{equation*}
$$

having exploited the fact that in a well-designed differential circuit the condition $R_{C} I_{C} \gg 2 V_{T}$ holds. It is apparent that the noise of a resistive load plays an insignificant role also in the case of current noise. By symmetry, similar considerations hold for $i_{n p}$, so we summarize by writing

$$
\begin{equation*}
i_{n p}^{2}=i_{n n}^{2} \cong 2 q\left(I_{B}+\frac{K I_{B}^{a}}{f}+\frac{I_{C}}{\left|\beta_{0}(j f)\right|^{2}}\right) \tag{7.149}
\end{equation*}
$$

This completes the noise analysis of the bipolar pair.

### SPICE Simulation of Noise

Used judiciously, SPICE is a powerful tool for noise analysis. As an example, let us use PSpice to verify the pn junction calculations of Example 7.41. SPICE calculates diode noise as

$$
\begin{equation*}
i_{n d}^{2}(f)=\mathrm{KF} \frac{I_{D}^{\mathrm{AF}}}{f}+2 q I_{D} \tag{7.150}
\end{equation*}
$$

where KF is the flicker noise coefficient and AF the exponent. These parameters must be specified in the device's .model statement, as exemplified for the following homebrew diode called Dnoise

```
.model Dnoise D(Is=2fA n=1 KF=5E-17 AF=1)
```

To obtain the noise plots we must direct SPICE to perform the ac analysis with the noise analysis enabled. Noise analysis requires that we specify the Output Vol tage and the I/V Source. For the example of Fig. 7.107a these are, respectively, V (vD) and ID. After running PSpice we specify the trace V(ONOISE) to display $e_{n d}$, and the trace SQRT ( $\mathrm{S}(\mathrm{V}(\mathrm{ONOISE}) * \mathrm{~V}(\mathrm{ONOISE}))$ ) to display $E_{n}$.

The results of the simulation, shown in Fig. 7.107b, confirm that the value of $E_{n}$ strongly depends on our choice of $f_{H}$. For $f_{H}=1 \mathrm{MHz}$ PSpice gives $E_{n}=1.466 \mu \mathrm{~V}$ rms , in excellent agreement with hand calculations. Placing a $2.1-\mathrm{nF}$ capacitance in parallel with the diode filters out high-frequency noise, causing $E_{n}$ to settle asymptotically to $1.0 \mu \mathrm{~V} \mathrm{rms}$, as desired.
image_name:(a)
description:
[
name: ID, type: CurrentSource, value: 0.1 mA, ports: {Np: 0, Nn: vD}
name: Dnoise, type: Diode, ports: {Na: vD, Nc: 0}
name: C, type: Capacitor, value: 2.1 nF, ports: {Np: vD, Nn: 0}
]
extrainfo:The circuit consists of a current source providing 0.1 mA to a diode and a capacitor in parallel, filtering high-frequency noise. The node vD is the voltage across the diode and capacitor.
image_name:(b)
description:The graph in Figure 7.107b is a frequency plot that displays the noise voltage characteristics of the circuit described in Example 7.41. It includes two main plots: the noise voltage $e_{n d}(t o p)$ and the root mean square (rms) voltage $E_{n}$.

1. **Type of Graph and Function:**
- The graph is a frequency response plot, likely a Bode plot, showing how the noise voltage varies with frequency.

2. **Axes Labels and Units:**
- The horizontal axis represents frequency, likely in hertz (Hz), although the exact units are not specified in the context.
- The vertical axis represents voltage, with the top plot showing the noise voltage $e_{n d}$ and the bottom plot showing the rms voltage $E_{n}$, both likely in microvolts (μV).

3. **Overall Behavior and Trends:**
- The top plot, $e_{n d}(t o p)$, shows how the noise voltage behaves across different frequencies. It likely displays variations indicating the presence of noise at certain frequency ranges.
- The bottom plot, $E_{n}$, shows the rms voltage behavior. It indicates that the rms voltage decreases as frequency increases, especially when a capacitance is added.

4. **Key Features and Technical Details:**
- The simulation results show that for $f_{H} = 1 \, \text{MHz}$, the rms voltage $E_{n}$ is $1.466 \, \mu \text{V}$, which matches hand calculations.
- When a $2.1 \, \text{nF}$ capacitance is added in parallel with the diode, the high-frequency noise is filtered out, causing $E_{n}$ to settle asymptotically to $1.0 \, \mu \text{V}$.

5. **Annotations and Specific Data Points:**
- The graph may have annotations or markers indicating key frequencies or voltage levels, such as the $1.0 \, \mu \text{V}$ rms voltage level after filtering.
- These annotations help to highlight the effectiveness of the capacitance in reducing noise levels at higher frequencies.

(a)
image_name:(b)
description:The graph consists of two plots that illustrate the noise characteristics of a diode as a function of frequency.

1. **Top Plot: Noise Voltage vs. Frequency**
- **Type of Graph:** This is a log-log plot showing the noise voltage per square root of the frequency ($e_{nd}$) in nanovolts per square root hertz (nV/√Hz) on the y-axis against frequency in hertz (Hz) on the x-axis.
- **Axes Labels and Units:**
- Y-axis: Noise voltage ($e_{nd}$) in nV/√Hz, logarithmic scale.
- X-axis: Frequency ($f$) in Hz, logarithmic scale.
- **Overall Behavior and Trends:**
- The noise voltage starts high at lower frequencies and decreases as the frequency increases, indicating a reduction in noise with increased frequency.
- After reaching a minimum, the noise voltage levels off, showing a consistent noise level over a range of higher frequencies.
- **Key Features and Technical Details:**
- The curve initially decreases steeply and then flattens, indicating that most of the noise reduction occurs at lower frequencies.
- There is a slight rise in noise at very high frequencies beyond $10^6$ Hz.
- **Annotations and Specific Data Points:**
- The plot is annotated with $e_{nd}$ to indicate the noise voltage curve.

2. **Bottom Plot: RMS Voltage vs. Frequency**
- **Type of Graph:** This is another log-log plot showing the root mean square (RMS) voltage ($E_{n}$) in microvolts (µV) on the y-axis against frequency in hertz (Hz) on the x-axis.
- **Axes Labels and Units:**
- Y-axis: RMS voltage ($E_{n}$) in µV, logarithmic scale.
- X-axis: Frequency ($f$) in Hz, logarithmic scale.
- **Overall Behavior and Trends:**
- The RMS voltage starts low at very low frequencies, increases slightly, and then shows a significant rise at higher frequencies, particularly beyond $10^5$ Hz.
- **Key Features and Technical Details:**
- The curve shows a noticeable increase in RMS voltage as frequency increases, indicating the effect of high-frequency noise on the RMS value.
- The RMS voltage appears to settle asymptotically towards 1.0 µV at higher frequencies, as indicated by the context.
- **Annotations and Specific Data Points:**
- The plot is annotated with $E_{n}$ to indicate the RMS voltage curve.

These plots together demonstrate the effectiveness of adding capacitance in parallel with the diode to filter out high-frequency noise, as evidenced by the behavior of both the noise voltage and RMS voltage across the frequency spectrum.

(b)

FIGURE 7.107 (a) PSpice circuit to plot the noise characteristics of the diode of Example 7.41. (b) Frequency plots of the noise voltage $e_{n d}(t o p)$ and the rms voltage $E_{n}$ (bottom).
