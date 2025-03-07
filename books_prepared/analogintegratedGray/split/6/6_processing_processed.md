# 6. Operational Amplifiers with Single-Ended Outputs

In the previous three chapters, the most important circuit building blocks utilized in analog integrated circuits (ICs) have been studied. Most analog ICs consist primarily of these basic circuits connected in such a way as to perform the desired function. Although the variety of standard and special-purpose custom ICs is almost limitless, a few standard circuits stand out as perhaps having the widest application in systems of various kinds. These include operational amplifiers, voltage regulators, and analog-to-digital (A/D) and digital-to-analog (D/A) converters. In this chapter, we will consider monolithic operational amplifiers (op amps) with single-ended outputs, both as an example of the utilization of the previously described circuit building blocks and as an introduction to the design and application of this important class of analog circuit. Op amps with fully differential outputs are considered in Chapter 12, and voltage-regulator circuits are considered in Chapter 8 . The design of A/D and D/A converters is not covered, but it involves application of the circuit techniques described throughout the book.

An ideal op amp with a single-ended output has a differential input, infinite voltage gain, infinite input resistance, and zero output resistance. A conceptual schematic diagram is shown in Fig. 6.1. While actual op amps do not have these ideal characteristics, their performance is usually sufficiently good that the circuit behavior closely approximates that of an ideal op amp in most applications.

In op-amp design, bipolar transistors offer many advantages over their CMOS counterparts, such as higher transconductance for a given current, higher gain $\left(g_{m} r_{o}\right)$, higher speed, lower input-referred offset voltage and lower input-referred noise voltage. (The topic of noise is considered in Chapter 11.) As a result, op amps made from bipolar transistors offer the best performance in many cases, including for example dc-coupled, low-offset, low-drift applications. For these reasons, bipolar op amps became commercially significant first and still usually offer superior analog performance. However, CMOS technologies have become dominant in building the digital portions of signal-processing systems because CMOS digital circuits are smaller and dissipate less power than their bipolar counterparts. Since these systems often operate on signals that originate in analog form, analog circuits such as op amps are required to interface to the digital CMOS circuits. To reduce system cost and increase portability, analog and digital circuits are now often integrated together, providing a strong economic incentive to use CMOS op amps.

In this chapter, we first explore several applications of op amps to illustrate their versatility in analog circuit and system design. CMOS op amps are considered next. Then a generalpurpose bipolar monolithic op amp, the NE5234, is analyzed, and the ways in which the performance of the circuit deviates from ideality are described. Design considerations for improving the various aspects of monolithic op-amp low-frequency performance are described. The high-frequency and transient response of op amps are covered in Chapters 7 and 9.

image_name:Figure 6.1 Ideal operational amplifier
description:
[
name: A0, type: OpAmp, value: A0, ports: {InP: Vip, InN: Vin, OutP: Vo, OutN: GND}
]
extrainfo:The diagram represents an ideal operational amplifier with infinite gain (a → ∞). The input is differential with Vip and Vin, and the output is Vo. The op-amp is grounded at the negative output terminal.

Figure 6.1 Ideal operational amplifier.

## 6.1 Applications of Operational Amplifiers

### 6.1.1 Basic Feedback Concepts

Virtually all op-amp applications rely on the principles of feedback. The topic of feedback amplifiers is covered in detail in Chapter 8; we now consider a few basic concepts necessary for an understanding of op-amp circuits. A generalized feedback amplifier is shown in Fig. 6.2. The block labeled $a$ is called the forward or basic amplifier, and the block labeled $f$ is called the feedback network. The gain of the basic amplifier when the feedback network is not present is called the open-loop gain, $a$, of the amplifier. The function of the feedback network is to sense the output signal $S_{o}$ and develop a feedback signal $S_{f b}$, which is equal to $f S_{o}$, where $f$ is usually less than unity. This feedback signal is subtracted from the input signal $S_{i}$, and the difference $S_{\epsilon}$ is applied to the basic amplifier. The gain of the system when the feedback network is present is called the closed-loop gain. For the basic amplifier we have

$$
\begin{equation*}
S_{o}=a S_{\epsilon}=a\left(S_{i}-S_{f b}\right)=a\left(S_{i}-f S_{o}\right) \tag{6.1}
\end{equation*}
$$

and thus

$$
\begin{equation*}
\frac{S_{o}}{S_{i}}=\frac{a}{1+a f}=\frac{1}{f}\left(\frac{a f}{1+a f}\right)=\frac{1}{f}\left(\frac{T}{1+T}\right) \tag{6.2}
\end{equation*}
$$

where $T=a f$ is called the loop gain. When $T$ becomes large compared to unity, the closed-loop gain becomes

$$
\begin{equation*}
\lim _{T \rightarrow \infty} \frac{S_{o}}{S_{i}}=\frac{1}{f} \tag{6.3}
\end{equation*}
$$

image_name:Figure 6.2 A conceptual feedback amplifier
description:The system block diagram, labeled as "Figure 6.2 A conceptual feedback amplifier," represents a feedback amplifier system. It consists of the following main components and flow of information:

1. **Main Components:**
- **Amplifier Block (a):** This block represents the main amplifier with an open-loop gain denoted by 'a'. It amplifies the input error signal \( S_\epsilon \) to produce the output signal \( S_o \).
- **Feedback Network (f):** This block represents the feedback network with a feedback factor 'f'. It processes the output signal \( S_o \) and generates the feedback signal \( S_{fb} \).
- **Summing Junction:** A summing junction is used to compute the error signal \( S_\epsilon \) by subtracting the feedback signal \( S_{fb} \) from the input signal \( S_i \).

2. **Flow of Information or Control:**
- The input signal \( S_i \) enters the system and is directed to the summing junction.
- The summing junction calculates the error signal \( S_\epsilon = S_i - S_{fb} \).
- The error signal \( S_\epsilon \) is then fed into the amplifier block 'a', which amplifies it to produce the output signal \( S_o \).
- The output signal \( S_o \) is split; one path leads to the final output, while the other is fed back into the feedback network 'f'.
- The feedback network processes \( S_o \) to generate the feedback signal \( S_{fb} = f \times S_o \), which is looped back to the summing junction.

3. **Labels, Annotations, and Key Indicators:**
- The diagram includes labels for each signal and block, such as \( S_i \) for input, \( S_o \) for output, \( S_\epsilon \) for error signal, and \( S_{fb} \) for feedback signal.
- The gain of the amplifier is denoted by 'a', and the feedback factor is represented by 'f'.

4. **Overall System Function:**
- The primary function of this feedback amplifier system is to regulate the gain and stability of the amplifier output. By using feedback, the system can achieve a closed-loop gain that is largely independent of the open-loop gain 'a', especially when the loop gain \( T = a \times f \) is much greater than 1. This configuration allows the system to maintain a stable and precise gain of \( 1/f \), making it robust against variations in the amplifier's open-loop characteristics. This is a fundamental concept in operational amplifier design and application.

Figure 6.2 A conceptual feedback amplifier.

Since the feedback network is composed of passive components, the value of $f$ can be set to an arbitrary degree of accuracy and will establish the gain at a value of $1 / f$ if $T \gg 1$, independent of any variations in the open-loop gain $a$. This independence of closed-loop performance from the parameters of the active amplifier is the primary factor motivating the wide use of op amps as active elements in analog circuits.

For the circuit shown in Fig. 6.2, the feedback signal tends to reduce the magnitude of $S_{\epsilon}$ below that of the open-loop case (for which $f=0$ ) when $a$ and $f$ have the same sign. This case is called negative feedback and is the case of practical interest in this chapter.

With this brief introduction to feedback concepts, we proceed to a consideration of several examples of useful op-amp configurations. Because these example circuits are simple, direct analysis with Kirchoff's laws is easier than attempting to consider them as feedback amplifiers. In Chapter 8, more complicated feedback configurations are considered in which the use of feedback concepts as an analytical tool is more useful than in these examples.

### 6.1.2 Inverting Amplifier

The inverting amplifier connection is shown in Fig. 6.3a. ${ }^{1,2,3}$ We assume that the op-amp input resistance is infinite, and that the output resistance is zero as shown in Fig. 6.1. From KCL at node $X$,

$$
\begin{equation*}
\frac{V_{s}-V_{i}}{R_{1}}+\frac{V_{o}-V_{i}}{R_{2}}=0 \tag{6.4}
\end{equation*}
$$

Since $R_{2}$ is connected between the amplifier output and the inverting input, the feedback is negative. Therefore, $V_{i}$ would be driven to zero with infinite open-loop gain. On the other hand, with finite open-loop gain $a$,

$$
\begin{equation*}
V_{i}=\frac{-V_{o}}{a} \tag{6.5}
\end{equation*}
$$

image_name:(a)
description:
[
name: VS, type: VoltageSource, value: VS, ports: {Np: VS, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: VS, N2: X}
name: R2, type: Resistor, value: R2, ports: {N1: X, N2: Vo}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: X, OutP: Vo}
]
extrainfo:The circuit is an inverting amplifier configuration. The voltage source VS is connected to resistor R1, leading to node X, which is the inverting input of the op-amp A0. Resistor R2 provides negative feedback from the output Vo back to the inverting input. The non-inverting input of the op-amp is connected to ground. The output voltage Vo is inverted with respect to the input voltage.
image_name:(b)
description:
[
name: VS, type: VoltageSource, value: VS, ports: {Np: Vs, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vx, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vx, N2: Vo}
name: A0, type: OpAmp, value: A0, ports: {InP: Vs, InN: Vx, Out: Vo}
]
extrainfo:This circuit is a non-inverting amplifier configuration. The input voltage is applied to the non-inverting terminal of the op-amp.
image_name:(c)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: A0, type: OpAmp, value: A0, ports: {InP: Vs, InN: Vo, OutP: Vo}
]
extrainfo:The circuit diagram (c) represents a voltage follower configuration where the output voltage Vo follows the input voltage Vs. The op-amp A0 is configured to provide a unity gain buffer.

Figure 6.3 (a) Inverting amplifier configuration. (b) Noninverting amplifier configuration. (c) Voltagefollower configuration.

Substituting (6.5) into (6.4) and rearranging gives

$$
\begin{equation*}
\frac{V_{o}}{V_{s}}=-\frac{R_{2}}{R_{1}}\left[\frac{1}{1+\frac{1}{a}\left(1+\frac{R_{2}}{R_{1}}\right)}\right] \tag{6.6}
\end{equation*}
$$

If the gain of the op amp is large enough that

$$
\begin{equation*}
a\left(\frac{R_{1}}{R_{1}+R_{2}}\right) \gg 1 \tag{6.7}
\end{equation*}
$$

then the closed-loop gain is

$$
\begin{equation*}
\frac{V_{o}}{V_{s}} \simeq-\frac{R_{2}}{R_{1}} \tag{6.8}
\end{equation*}
$$

When the inequality in (6.7) holds, (6.8) shows that the closed-loop gain depends primarily on the external passive components $R_{1}$ and $R_{2}$. Since these components can be selected with arbitrary accuracy, a high degree of precision can be obtained in closed-loop performance independent of variations in the active device (op-amp) parameters. For example, if the opamp gain were to change from $5 \times 10^{4}$ to $10^{5}$, this 100 percent increase in gain would have almost no observable effect on closed-loop performance provided that (6.7) is valid.

#### EXAMPLE

Calculate the gain of the circuit Fig. 6.3a, for $a=10^{4}$ and $a=10^{5}$, and $R_{1}=1 \mathrm{k} \Omega, R_{2}=$ $10 \mathrm{k} \Omega$.

From (6.6) with $a=10^{4}$,

$$
\begin{equation*}
A=\frac{V_{o}}{V_{s}}=-10\left(\frac{1}{1+\frac{11}{10^{4}}}\right)=-9.9890 \tag{6.9a}
\end{equation*}
$$

From (6.6) with $a=10^{5}$,

$$
\begin{equation*}
A=\frac{V_{o}}{V_{s}}=-10\left(\frac{1}{1+\frac{11}{10^{5}}}\right)=-9.99890 \tag{6.9b}
\end{equation*}
$$

The large gain of op amps allows the approximate analysis of circuits like that of Fig. 6.3a to be performed by the use of summing-point constraints. ${ }^{1}$ If the op amp is connected in a negative-feedback circuit, and if the gain of the op amp is very large, then for a finite value of output voltage the input voltage must approach zero since

$$
\begin{equation*}
V_{i}=-\frac{V_{o}}{a} \tag{6.10}
\end{equation*}
$$

Thus one can analyze such circuits approximately by assuming a priori that the op-amp input voltage is driven to zero. An implicit assumption in doing so is that the feedback is negative, and that the circuit has a stable operating point at which (6.10) is valid.

The assumption that $V_{i}=0$ is called a summing-point constraint. A second constraint is that no current can flow into the op-amp input terminals, since no voltage exists across the input resistance of the op amp if $V_{i}=0$. This summing-point approach allows an intuitive understanding of the operation of the inverting amplifier configuration of Fig. 6.3a. Since the
inverting input terminal is forced to ground potential, the resistor $R_{1}$ serves to convert the voltage $V_{s}$ to an input current of value $V_{s} / R_{1}$. This current cannot flow in the input terminal of an ideal op amp; therefore, it flows through $R_{2}$, producing a voltage drop of $V_{s} R_{2} / R_{1}$. Because the op-amp input terminal operates at ground potential, the input resistance of the overall circuit as seen by $V_{s}$ is equal to $R_{1}$. Since the inverting input of the amplifier is forced to ground potential by the negative feedback, it is sometimes called a virtual ground.

### 6.1.3 Noninverting Amplifier

The noninverting amplifier is shown in Fig. 6.3b. ${ }^{1,2,3}$ Using Fig. 6.1, assume that no current flows into the inverting op-amp input terminal. If the open-loop gain is $a, V_{i}=V_{o} / a$ and

$$
\begin{equation*}
V_{x}=V_{o}\left(\frac{R_{1}}{R_{1}+R_{2}}\right)=V_{s}-\frac{V_{o}}{a} \tag{6.11}
\end{equation*}
$$

Rearranging (6.11) gives

$$
\begin{equation*}
\frac{V_{o}}{V_{s}}=\left(1+\frac{R_{2}}{R_{1}}\right) \frac{\frac{a R_{1}}{R_{1}+R_{2}}}{1+\frac{a R_{1}}{R_{1}+R_{2}}} \simeq\left(1+\frac{R_{2}}{R_{1}}\right) \tag{6.12}
\end{equation*}
$$

The approximation in (6.12) is valid to the extent that $a R_{1} /\left(R_{1}+R_{2}\right) \gg 1$.
In contrast to the inverting case, this circuit displays a very high input resistance as seen by $V_{s}$ because of the type of feedback used. (See Chapter 8.) Also unlike the inverting case, the noninverting connection causes the common-mode input voltage of the op amp to be equal to $V_{s}$. An important variation of this connection is the voltage follower, in which $R_{1} \rightarrow \infty$ and $R_{2}=0$. This circuit is shown in Fig. 6.3c, and its gain is close to unity if $a \gg 1$.

### 6.1.4 Differential Amplifier

The differential amplifier is used to amplify the difference between two voltages. The circuit is shown in Fig. 6.4. ${ }^{1,2}$ For this circuit, $I_{i 1}=0$ and thus resistors $R_{1}$ and $R_{2}$ form a voltage
image_name:Figure 6.4 Differential amplifier configuration
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
name: V2, type: VoltageSource, value: V2, ports: {Np: V2, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: V1, N2: Vx}
name: R1, type: Resistor, value: R1, ports: {N1: V2, N2: Vy}
name: R2, type: Resistor, value: R2, ports: {N1: Vy, N2: Vo}
name: R2, type: Resistor, value: R2, ports: {N1: Vx, N2: GND}
name: A0, type: OpAmp, value: A0, ports: {InP: Vx, InN: Vy, OutP: Vo}
]
extrainfo:The circuit is a differential amplifier configuration. It amplifies the difference between two input voltages V1 and V2. The output voltage Vo is determined by the relationship between the resistors R1 and R2 and the input voltages.

Figure 6.4 Differential amplifier configuration.
divider. Voltage $V_{x}$ is then given by

$$
\begin{equation*}
V_{x}=V_{1}\left(\frac{R_{2}}{R_{1}+R_{2}}\right) \tag{6.13}
\end{equation*}
$$

The current $I_{1}$ is

$$
\begin{equation*}
I_{1}=\left(\frac{V_{2}-V_{y}}{R_{1}}\right)=I_{2} \tag{6.14}
\end{equation*}
$$

The output voltage is given by

$$
\begin{equation*}
V_{o}=V_{y}-I_{2} R_{2} \tag{6.15}
\end{equation*}
$$

If the open-loop gain is infinite, the summing-point constraint that $V_{i}=0$ is valid and forces $V_{y}=V_{x}$. Substituting $V_{y}=V_{x}$, (6.13), and (6.14) into (6.15) and rearranging gives

$$
\begin{equation*}
V_{o}=\frac{R_{2}}{R_{1}}\left(V_{1}-V_{2}\right) \tag{6.16}
\end{equation*}
$$

The circuit thus amplifies the difference voltage ( $V_{1}-V_{2}$ ).
Differential amplifiers are often required to detect and amplify small differences between two sizable voltages. For example, a typical application is the measurement of the difference voltage between the two arms of a Wheatstone bridge. As in the case of the noninverting amplifier, the op amp of Fig. 6.4 experiences a common-mode input that is almost equal to the common-mode voltage ( $V_{1}+V_{2}$ )/2 applied to the input terminals when $R_{2} \gg R_{1}$.

### 6.1.5 Nonlinear Analog Operations

By including nonlinear elements in the feedback network, op amps can be used to perform nonlinear operations on one or more analog signals. The logarithmic amplifier, shown in Fig. 6.5, is an example of such an application. Log amplifiers find wide application in instrumentation systems where signals of very large dynamic range must be sensed and recorded. The operation of this circuit can again be understood by application of the summing-point constraints. Because the input voltage of the op amp must be zero, the resistor $R$ serves to convert the input voltage $V_{s}$ into a current. This same current must then flow into the collector of the transistor. Thus the circuit forces the collector current of the transistor to be proportional to the input voltage. Furthermore, the transistor operates in the forward-active region because $V_{C B} \simeq 0$. Since the base-emitter voltage of a bipolar transistor in the forward-active region is logarithmically related to the collector current, and since the output voltage is just the emitter-base voltage of the transistor, a logarithmic transfer characteristic is produced. In terms of equations,

$$
\begin{equation*}
I_{1}=\frac{V_{s}}{R}=I_{c}=I_{S}\left[\exp \left(\frac{V_{b e}}{V_{T}}\right)-1\right] \simeq I_{S} \exp \left(\frac{V_{b e}}{V_{T}}\right) \tag{6.17}
\end{equation*}
$$

image_name:Figure 6.5 Logarithmic amplifier configuration
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: Vs, N2: InN(A0)}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: InN(A0), Out: Vo}
name: NMOS, type: NMOS, ports: {S: V0, D: InN(A0), G: GND}
]
extrainfo:The circuit is a logarithmic amplifier configuration using an op-amp and an NMOS transistor. The input voltage Vs is converted into a logarithmic output voltage Vo. The op-amp A0 is configured with negative feedback through the NMOS transistor, which helps achieve the logarithmic characteristic. The resistor R is connected in series with the input voltage source.

Figure 6.5 Logarithmic amplifier configuration.
and

$$
\begin{equation*}
V_{o}=-V_{b e} \tag{6.18}
\end{equation*}
$$

Thus

$$
\begin{equation*}
V_{o}=-V_{T} \ln \left(\frac{V_{s}}{I_{S} R}\right) \tag{6.19}
\end{equation*}
$$

The log amplifier is only one example of a wide variety of op-amp applications in which a nonlinear feedback element is used to develop a nonlinear transfer characteristic. For example, two log amplifiers can be used to develop the logarithm of two different signals. These voltages can be summed, and then the exponential function of the result can be developed using an inverting amplifier connection with $R_{1}$ replaced with a diode. The result is an analog multiplier. Other nonlinear operations such as limiting, rectification, peak detection, squaring, square rooting, raising to a power, and division can be performed in conceptually similar ways.

### 6.1.6 Integrator, Differentiator

The integrator and differentiator circuits, shown in Fig. 6.6, are examples of using op amps with reactive elements in the feedback network to realize a desired frequency response or timedomain response. ${ }^{1,2}$ In the case of the integrator, the resistor $R$ is used to develop a current $I_{1}$ that is proportional to the input voltage. This current flows into the capacitor $C$, whose voltage is proportional to the integral of the current $I_{1}$ with respect to time. Since the output voltage is equal to the negative of the capacitor voltage, the output is proportional to the integral of the input voltage with respect to time. In terms of equations,

$$
\begin{equation*}
I_{1}=\frac{V_{s}}{R}=I_{2} \tag{6.20}
\end{equation*}
$$

and

$$
\begin{equation*}
V_{o}=-\frac{1}{C} \int_{0}^{t} I_{2} d \tau+V_{o}(0) \tag{6.21}
\end{equation*}
$$

Combining (6.20) and (6.21) yields

$$
\begin{equation*}
V_{o}(t)=-\frac{1}{R C} \int_{0}^{t} V_{s}(\tau) d \tau+V_{o}(0) \tag{6.22}
\end{equation*}
$$

The performance limitations of real op amps limit the range of $V_{o}$ and the rate of change of $V_{o}$ for which this relationship is maintained.

In the case of the differentiator, the capacitor $C$ is connected between $V_{s}$ and the inverting op-amp input. The current through the capacitor is proportional to the time derivative of the
image_name:(a)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: Vs, N2: InN(A0)}
name: C, type: Capacitor, value: C, ports: {Np: InN(A0), Nn: Vo}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: InN(A0), OutP: Vo}
]
extrainfo:This is an integrator circuit configuration (a) where the input voltage Vs is integrated over time to produce the output voltage Vo. The current I1 flows through the resistor R, and the current I2 flows through the capacitor C.
image_name:(b)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: C, type: Capacitor, value: C, ports: {Np: Vs, Nn: InN(A0)}
name: R, type: Resistor, value: R, ports: {N1: InN(A0), N2: Vo}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: InN(A0), Out: Vo}
]
extrainfo:The circuit is a differentiator configuration. The capacitor C is connected between the input voltage source Vs and the inverting input of the op-amp A0. The feedback resistor R is connected between the inverting input and the output Vo of the op-amp.

Figure 6.6 (a) Integrator configuration. (b) Differentiator configuration.
voltage across it, which is equal to the input voltage. This current flows through the feedback resistor $R$, producing a voltage at the output proportional to the capacitor current, which is proportional to the time rate of change of the input voltage. In terms of equations,

$$
\begin{gather*}
I_{1}=C \frac{d V_{s}}{d t}=I_{2}  \tag{6.23}\\
V_{o}=-R I_{2}=-R C \frac{d V_{s}}{d t} \tag{6.24}
\end{gather*}
$$

### 6.1.7 Internal Amplifiers

The performance objectives for op amps to be used within a monolithic analog subsystem are often quite different from those of general-purpose op amps that use external feedback elements. In a monolithic analog subsystem, only a few of the amplifiers must drive a signal off-chip where the capacitive and resistive loads are significant and variable. These amplifiers will be termed output buffers, and the amplifiers whose outputs do not go off chip will be termed internal amplifiers. Perhaps the most important difference is that the load an internal amplifier has to drive is well defined and is often purely capacitive with a value of a few picofarads. In contrast, stand-alone general-purpose amplifiers usually must be designed to achieve a certain level of performance that is independent of changes in capacitive loads up to several hundred picofarads and resistive loads down to $2 \mathrm{k} \Omega$ or less.

#### 6.1.7.1 Switched-Capacitor Amplifier

In MOS technologies, capacitors instead of resistors are often used as passive elements in feedback amplifiers in part because capacitors are often the best available passive components. Also, capacitors can store charge proportional to analog signals of interest, and MOS transistors can act as switches to connect to the capacitors without offset and with little leakage, allowing the discrete-time signal processing of analog quantities. The topic of MOS switched-capacitor amplifiers is one important application of internal amplifiers. Here, we introduce the application to help explain the construction of MOS op amps.

Figure 6.7 shows the schematic of an inverting amplifier with capacitive feedback in contrast to the resistive feedback shown in Fig. 6.3a. If the op amp is ideal, the gain from a change in the input $\Delta V_{s}$ to a change in the output $\Delta V_{o}$ is still given by the ratio of the impedance of the feedback element $C_{2}$ to the impedance of the input element $C_{1}$, or

$$
\begin{equation*}
\frac{\Delta V_{o}}{\Delta V_{s}}=-\frac{\frac{1}{\omega C_{2}}}{\frac{1}{\omega C_{1}}}=-\frac{C_{1}}{C_{2}} \tag{6.25}
\end{equation*}
$$

Unlike the case when resistors are used as passive elements, however, this circuit does not provide dc bias for the inverting op-amp input because the impedances of both capacitors are
image_name:Figure 6.7
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vs, Nn: InN(A0)}
name: C2, type: Capacitor, value: C2, ports: {Np: InN(A0), Nn: Vo}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: InN(A0), OutP: Vo, OutN: GND}
]
extrainfo:The circuit is an inverting amplifier configuration with capacitive feedback. It lacks DC bias for the inverting op-amp input due to the capacitive elements.

Figure 6.7 Inverting amplifier configuration with capacitive feedback without dc bias for the inverting
op-amp input.
infinite at dc. To overcome this problem, switches controlled by a two-phase nonoverlapping clock are used to control the operation of the above circuit. The resulting circuit is known as a switched-capacitor amplifier.

Figure $6.8 a$ shows the schematic of a switched-capacitor amplifier. Each switch in the schematic is controlled by one of two clock phases $\phi_{1}$ and $\phi_{2}$, and the timing diagram is shown
image_name:(a)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: S1, type: Switch, ports: {N1: Vs, N2: X1}
name: S2, type: Switch, ports: {N1: X1, N2: GND}
name: S3, type: Switch, ports: {N1: GND, N2: InN(A0)}
name: S4, type: Switch, ports: {N1: GND, N2: X2}
name: S5, type: Switch, ports: {N1: X2, N2: Vo}
name: C1, type: Capacitor, value: C1, ports: {Np: X1, Nn: InN(A0)}
name: C2, type: Capacitor, value: C2, ports: {Np: InN(A0), Nn: X2}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: InN(A0), OutP: Vo}
]
extrainfo:The circuit is a switched-capacitor amplifier with two-phase nonoverlapping clock signals \(\phi_1\) and \(\phi_2\). The switches are controlled by these clock phases, ensuring only one set of switches is closed at a time. The amplifier uses capacitive feedback with no DC bias at the inverting input of the op-amp. The timing diagram for the clock signals is shown in the schematic, illustrating the nonoverlapping nature of \(\phi_1\) and \(\phi_2\).
image_name:(b)
description:The graph in Figure 6.8(b) is a timing diagram representing two non-overlapping clock signals, \( \phi_1 \) and \( \phi_2 \), used to control switches in a switched-capacitor amplifier circuit. This type of graph is a time-domain waveform.

1. **Axes Labels and Units:**
- The horizontal axis represents time (\( t \)), though no specific units are provided. The axis is linear, showing the progression of time.
- The vertical axis represents the logic level of the clock signals, typically high or low (often interpreted as 1 or 0 in digital systems).

2. **Overall Behavior and Trends:**
- Both \( \phi_1 \) and \( \phi_2 \) are periodic waveforms, indicating a repeating cycle of high and low states.
- \( \phi_1 \) and \( \phi_2 \) are non-overlapping, meaning they do not go high at the same time. When one is high, the other is low, ensuring that switches controlled by these signals do not close simultaneously.

3. **Key Features and Technical Details:**
- Both clock signals have a duty cycle that shows equal high and low periods, but the exact timing intervals are not specified.
- The non-overlapping nature is crucial to the operation of the switched-capacitor amplifier, preventing short circuits or unwanted paths in the circuit.

4. **Annotations and Specific Data Points:**
- No specific numerical data points or annotations are provided on the timing diagram.
- The diagram effectively illustrates the alternating nature of the two-phase clock system, which is essential for the function of the switched-capacitor circuit.
image_name:(c)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vs, Nn: InN(A0)}
name: C2, type: Capacitor, value: C2, ports: {Np: InN(A0), Nn: GND}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: InN(A0)}
]
extrainfo:The circuit is a switched-capacitor amplifier during phase φ1, with capacitors C1 and C2, and an op-amp A0. The input voltage source Vs is connected through C1 to the inverting input of the op-amp. C2 is connected between the inverting input and ground.
image_name:(d)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: GND, Nn: InN(A0)}
name: C2, type: Capacitor, value: C2, ports: {Np: InN(A0), Nn: Vo}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: InN(A0), OutP: Vo}
]
extrainfo:The circuit is a switched-capacitor amplifier with capacitive feedback, controlled by two non-overlapping clock phases, phi1 and phi2. During phi1, switches S1, S3, and S4 are closed, connecting the input voltage Vs to the capacitor C1 and setting the initial conditions. During phi2, switches S2 and S5 are closed, transferring charge to the output through the op-amp A0, resulting in an amplified output voltage Vo.

Figure 6.8 (a) Schematic of a switched-capacitor amplifier with ideal switches. (b) Timing diagram of clock signals. (c) Connections during $\phi_{1}$. (d) Connections during $\phi_{2}$.
in Fig. 6.8b. We will assume that each switch is closed when its controlling clock signal is high, and open when its clock signal is low. Since $\phi_{1}$ and $\phi_{2}$ are never both high at the same time, the switches controlled by one clock phase are never closed at the same time as the switches controlled by the other clock phase. Because of this property, the clock signals in Fig. 6.8b are known as nonoverlapping. For example, the left side of $C_{1}$ is connected to the input $V_{s}$ through switch $S_{1}$ when $\phi_{1}$ is high and to ground through switch $S_{2}$ when $\phi_{2}$ is high, but this node is never simultaneously connected to both the input and ground.

To simplify the description of the operation of switched-capacitor circuits, they are often redrawn twice, once for each nonoverlapping clock phase. Figures $6.8 c$ and $6.8 d$ show the connections when $\phi_{1}$ is high (during $\phi_{1}$ ) and when $\phi_{2}$ is high (during $\phi_{2}$ ), respectively. Switches that are closed are assumed to be short circuits, and switches that are open are assumed to be open circuits.

To find the output for a given input, an analysis based on charge conservation is used. After switch $S_{3}$ opens, the charge on the plates of the capacitors that connect to the op-amp input node is conserved until this switch closes again. This property stems partly from the fact that the passive elements connected to the op-amp input node are capacitors, which conduct zero dc current. Also, if the op amp is constructed with an MOS differential input pair, the op-amp input is connected to the gate of one transistor in the differential pair, and the gate conducts zero dc current. Finally, if we assume that switch $S_{3}$ conducts zero current when it is open, the charge stored cannot leak away while $S_{3}$ is open.

Since both sides of $C_{2}$ are grounded in Fig. 6.8c, the charge stored on the plates of the capacitors that connect to the the op-amp input node during $\phi_{1}$ is

$$
\begin{equation*}
Q_{1}=\left(0-V_{s}\right) C_{1}+(0) C_{2}=\left(0-V_{s}\right) C_{1} \tag{6.26}
\end{equation*}
$$

Because the input voltage is sampled or stored onto capacitor $C_{1}$ during $\phi_{1}$, this phase is known as the input sample phase. If the op amp is ideal, the voltage $V_{i}$ from the inverting op-amp input to ground is driven to zero by negative feedback during $\phi_{2}$. Therefore, the charge stored during $\phi_{2}$ is

$$
\begin{equation*}
Q_{2}=(0) C_{1}+\left(0-V_{o}\right) C_{2}=\left(0-V_{o}\right) C_{2} \tag{6.27}
\end{equation*}
$$

Because the sampled charge appears on $C_{1}$ during $\phi_{1}$ and on $C_{2}$ during $\phi_{2}, \phi_{2}$ is known as the charge-transfer phase. By charge conservation, $Q_{2}=Q_{1}$; therefore,

$$
\begin{equation*}
\frac{V_{o}}{V_{s}}=\frac{C_{1}}{C_{2}} \tag{6.28}
\end{equation*}
$$

In (6.28), $V_{s}$ represents the input voltage at the end of $\phi_{1}$, and $V_{o}$ represents the output voltage at the end of $\phi_{2}$. The shape of the output voltage waveform is not predicted by (6.28) and depends on the rates at which the capacitors are charged and discharged. In practice, these rates depend on the bandwidth of the op amp and the resistances of the closed switches. The result in (6.28) is valid as long as the op amp is ideal, the input $V_{s}$ is dc, and the intervals over which $\phi_{1}$ and $\phi_{2}$ are high are long enough to completely charge and discharge the associated capacitors. The ratio of $V_{o} / V_{s}$ in (6.28) is positive because if $V_{s}>0$ during $\phi_{1}$, the voltage applied between the left side of $C_{1}$ and ground decreases from a positive value to zero during $\phi_{2}$. Therefore, this negative change in the applied voltage during $\phi_{2}$ is multiplied by a negative closed-loop amplifier gain, giving a positive ratio in (6.28).

MOS technologies are well suited to building switched-capacitor circuits for two key reasons. First, the dc current that flows into the input terminals of MOS op amps is zero as long as the inputs are connected only to the gates of MOS transistors. In contrast, bipolar op amps have nonzero dc input currents that stem from finite $\beta_{F}$ in bipolar transistors. Second, the switches in Fig. 6.8 can be implemented without offset by using MOS transistors, as shown
image_name:(a)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: M1, type: NMOS, ports: {S: X1, D: Vs, G: phi1}
name: M2, type: NMOS, ports: {S: X1, D: GND, G: phi2}
name: C1, type: Capacitor, value: C1, ports: {Np: X1, Nn: InN(A0)}
name: M3, type: NMOS, ports: {S: GND, D: InN(A0), G: phi1}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: InN(A0), OutP: Vo}
name: C2, type: Capacitor, value: C2, ports: {Np: InN(A0), Nn: d4d5}
name: M4, type: NMOS, ports: {S: GND, D: d4d5, G: phi1}
name: M5, type: NMOS, ports: {S: Vo, D: d4d5, G: phi2}
name: Cp, type: Capacitor, value: Cp, ports: {Np: InN(A0), Nn: GND}
]
extrainfo:This is a switched-capacitor amplifier circuit using n-channel MOS transistors as switches. The clock waveforms phi1 and phi2 control the switching of the MOS transistors. The circuit is designed to sample and amplify the input voltage Vs.
image_name:(b)
description:The graph labeled "(b)" depicts two time-domain waveforms representing clock signals \( \phi_1 \) and \( \phi_2 \). The x-axis is labeled as time \( t \), while the y-axis represents the voltage levels of the clock signals. The voltage levels are indicated by \( V_{DD} \) and \( -V_{SS} \), suggesting that the signals alternate between these two values.

1. **Type of Graph and Function**:
- The graph is a time-domain waveform plot, depicting the behavior of clock signals over time.

2. **Axes Labels and Units**:
- The x-axis is time \( t \), though specific units are not provided, it typically represents time in seconds or milliseconds.
- The y-axis represents voltage levels, with specific reference levels \( V_{DD} \) and \( -V_{SS} \).

3. **Overall Behavior and Trends**:
- Both \( \phi_1 \) and \( \phi_2 \) waveforms are square waves, alternating between \( V_{DD} \) and \( -V_{SS} \).
- The waveforms appear periodic, suggesting a regular switching pattern typical for clock signals.

4. **Key Features and Technical Details**:
- The waveforms exhibit a consistent duty cycle, implying equal time spent at each voltage level.
- There are no visible annotations or markers indicating specific timings or frequency values.

5. **Annotations and Specific Data Points**:
- The graph does not provide specific numerical values for \( V_{DD} \) or \( -V_{SS} \), nor does it specify the period of the waveforms.
- The signals are depicted in separate plots but are likely synchronized in some manner, as is typical in switched-capacitor circuits.

Overall, the graph illustrates the typical square waveforms used to control switches in a switched-capacitor circuit, as part of the clock signal generation necessary for the operation of the circuit shown in the schematic above (Fig. 6.9a).

Figure 6.9 (a) Schematic of a switched-capacitor amplifier with $n$-channel MOS transistors used as switches. (b) Clock waveforms with labeled voltages.
in Fig. 6.9a. The arrows indicating the source terminals of $M_{1}-M_{5}$ are arbitrarily chosen in the sense that the source and drain terminals are interchangeable. (Since the source is the source of electrons in $n$-channel transistors, the source-to-ground voltage is lower than the drain-to-ground voltage.) Assume that the clock voltages alternate between $-V_{S S}$ and $V_{D D}$ as shown in Fig. 6.9b. Also assume that all node voltages are no lower than $-V_{S S}$ and no higher than $V_{D D}$. Finally, assume that the transistor threshold voltages are positive. Under these conditions, each transistor turns off when its gate is low. Furthermore, each transistor turns on when its gate is high as long as its source operates at least a threshold below $V_{D D}$. If $V_{s}$ is a dc signal, all drain currents approach zero as the capacitors become charged. As the drain currents approach zero, the MOS transistors that are on operate in the triode region, where the drain-source voltage is zero when the drain current is zero. Therefore, the input voltage $V_{s}$ is sampled onto $C_{1}$ with zero offset inserted by the MOS transistors operating as switches. This property of MOS transistors is important in the implementation of switched-capacitor circuits. In contrast, bipolar transistors operating as switches do not give zero collector-emitter voltage with zero collector current.

The switched-capacitor amplifier shown in Fig. $6.9 a$ is important in practice mainly because the gain of this circuit has little dependence on the various parasitic capacitances that are present on all the nodes in the circuit. These undesired capacitances stem in part from the drain-body and source-body junction capacitances of each transistor. Also, the op-amp input capacitance contributes to the parasitic capacitance on the op-amp input node. Furthermore,
as described in Section 2.10.2, the bottom plates of capacitors $C_{1}$ and $C_{2}$ exhibit at least some capacitance to the underlying layer, which is the substrate or a well diffusion. Since the gain of the circuit is determined by charge conservation at the op-amp input node, the presence of parasitic capacitance from any node except the op-amp input to any node with a constant voltage to ground makes no difference to the accuracy of the circuit. (Such parasitics do reduce the maximum clock rate, however.) On the other hand, parasitic capacitance on the op-amp input node does affect the accuracy of the circuit gain, but the error is inversely proportional to the op-amp gain, as we will now show.

Let $C_{P}$ represent the total parasitic capacitance from the op-amp input to all nodes with constant voltage to ground. If the op-amp gain is $a$, the voltage from the inverting op-amp input to ground during $\phi_{2}$ is given by (6.10). Therefore, with finite op-amp gain, $C_{1}$ and $C_{P}$ are not completely discharged during $\phi_{2}$. Under these conditions, the charge stored on the op-amp input node during $\phi_{2}$ becomes

$$
\begin{equation*}
Q_{2}=\left(-\frac{V_{o}}{a}\right) C_{1}+\left(-\frac{V_{o}}{a}\right) C_{P}+\left(-\frac{V_{o}}{a}-V_{o}\right) C_{2} \tag{6.29}
\end{equation*}
$$

When the op-amp gain becomes infinite, (6.29) collapses to (6.27), as expected. Setting $Q_{2}$ in (6.29) equal to $Q_{1}$ in (6.26) by charge conservation gives

$$
\begin{equation*}
\frac{V_{o}}{V_{s}}=\frac{C_{1}}{C_{2}}\left[\frac{1}{1+\frac{1}{a}\left(\frac{C_{1}+C_{2}+C_{P}}{C_{2}}\right)}\right] \tag{6.30}
\end{equation*}
$$

This closed-loop gain can be written as

$$
\begin{equation*}
\frac{V_{o}}{V_{s}}=\frac{C_{1}}{C_{2}}(1-\epsilon) \tag{6.31}
\end{equation*}
$$

where $\epsilon$ is a gain error given by

$$
\begin{equation*}
\epsilon=\frac{1}{1+a\left(\frac{C_{2}}{C_{1}+C_{2}+C_{P}}\right)} \tag{6.32}
\end{equation*}
$$

As $a \rightarrow \infty, \epsilon \rightarrow 0$, and the gain of the switched-capacitor amplifier approaches $C_{1} / C_{2}$ as predicted in (6.28). As a result, the circuit gain is said to be parasitic insensitive to an extent that depends on the op-amp gain.

One important parameter of the switched-capacitor amplifier shown in Fig. $6.9 a$ is the minimum clock period. This period is divided into two main parts, one for each clock phase. The duration of $\phi_{2}$ must be long enough for the op-amp output to reach and stay within a given level of accuracy. This time is defined as the op-amp settling time and depends on the switch resistances, the circuit capacitances, and the op-amp properties. The settling time is usually determined by SPICE simulations. Such simulations should be run for both clock phases because the op-amp output voltage during $\phi_{1}$ is not well controlled in practice. If the op amp is ideal, this output voltage is zero. With nonzero offset voltage, however, the output voltage will be driven to a nonzero value during $\phi_{1}$ that depends on both the offset voltage and the op-amp gain. If the op-amp gain is large, the offset can easily be large enough to force the output voltage to clip near one of the supplies. The output voltage at the end of $\phi_{1}$ can be thought of as an initial condition for the circuit during $\phi_{2}$. If the initial condition and the desired final output at the end of $\phi_{2}$ happen to have far different values, the time required for the output to reach a given level of accuracy during $\phi_{2}$ can be increased. Furthermore, nonzero offset can increase the time required for the op-amp output voltage to reach a constant level during $\phi_{1}$. Although the circuit output voltage defined in (6.30) only appears during $\phi_{2}$, failure
to reach a constant output voltage during $\phi_{1}$ causes the initial condition defined above to vary, depending on the value of $V_{o}$ at the end of the preceding $\phi_{2}$. As a result of this memory effect, the circuit can behave as a filter (which is possibly nonlinear), weighting together the results of more than one previous input sample to determine any given output. The key point is that an increase in the minimum duration of either phase requires an increase in the minimum clock period. This effect should be included in simulation by intentionally simulating with nonzero offset voltages.

One way to reduce the effect of nonzero offset voltage on the minimum clock period is to include a reset switch at the op-amp output. If the op amp has a single-ended output as shown in Fig. 6.9a, such a switch can be connected between the op-amp output and a bias point between the two supplies. On the other hand, if the op amp has differential outputs as described in Chapter 12, such a reset switch can be connected between the two op-amp outputs. In either case, the reset switch would be turned on during $\phi_{1}$ and off during $\phi_{2}$. The main value of such a reset switch is that it can reduce both the maximum output voltage produced by a nonzero offset voltage during $\phi_{1}$ and the time required to reach this value, in turn reducing the effect of nonzero offset on the minimum durations of both phases.

The accuracy of the switched-capacitor amplifier shown in Fig. $6.9 a$ is limited by several other factors that we will now consider briefly. First, even with an ideal op amp, the gain depends on the ratio of capacitors $C_{1} / C_{2}$, which is not controlled perfectly in practice because of random-mismatch effects. Second, op-amp offset limits the minimum signal that can be distinguished from the offset in the switched-capacitor amplifier. As shown in Section 3.5.6, the input-referred offset of CMOS differential pairs is usually worse than for bipolar differential pairs. This property extends to op amps and stems partly from the reduced transconductance-to-current ratio of MOS transistors compared to their bipolar counterparts and partly from the threshold mismatch term, which appears only in the MOS case. Third, the charge-conservation equation and accuracy of the switched-capacitor amplifier are affected by the charge stored under the gates of some of the MOS transistors acting as switches in Fig. 6.9a. For example, some of the charge stored under the gate of transistor $M_{3}$ in Fig. $6.9 a$ is injected onto the op-amp input node after $M_{3}$ is turned off. Techniques to overcome these limitations are often used in practice but are not considered here.

#### 6.1.7.2 Switched-Capacitor Integrator

Another application of an internal op amp, a switched-capacitor integrator, is illustrated in its simplest form in Fig. 6.10a. This circuit is widely utilized as the basic element of monolithic switched-capacitor filters for two main reasons. First, the frequency response of the integrator is insensitive to the various parasitic capacitances that are present on all nodes in the circuit. ${ }^{4,5}$ Second, using switched-capacitor integrators as the basic elements, the synthesis of desired filter frequency responses is relatively straightforward. In this section, we will analyze the frequency response of the switched-capacitor integrator.

The integrator consists of an op amp, a sampling capacitor $C_{S}$, an integrating capacitor $C_{I}$, and four MOS transistor switches. The load capacitance shown represents the sampling capacitor of the following integrator, plus any parasitic capacitances that may be present. Typical values for the sampling, integrating, and load capacitances are labeled in Fig. 6.10a.

Figure $6.10 b$ shows the timing diagram of two nonoverlapping clock signals, $\phi_{1}$ and $\phi_{2}$, that control the operation of the circuit as well as typical input and output waveforms. During the interval when clock phase $\phi_{1}$ is high, transistors $M_{1}$ and $M_{3}$ operate in the triode region and serve to charge the sampling capacitor to a voltage that is equal to the input voltage. Subsequently, clock signal $\phi_{1}$ falls. Then clock signal $\phi_{2}$ rises, causing transistors $M_{2}$ and $M_{4}$ to turn on and the sampling capacitor to be connected between the inverting op-amp input, which is sometimes called the summing node, and ground. If the op amp is ideal, the resulting
image_name:(a)
description:The circuit is a switched-capacitor integrator. It uses NMOS transistors M1 and M3 to charge the sampling capacitor CS during the first clock phase (phi1), and NMOS transistors M2 and M4 to transfer the charge during the second clock phase (phi2). The op-amp A0 integrates the voltage across CI, and the output is taken across CL.
image_name:(b)
description:The graph in figure 6.10(b) is a timing diagram depicting the operation of a switched-capacitor integrator circuit. The diagram consists of three primary waveforms plotted against time on the x-axis.

1. **Type of Graph and Function:**
This is a timing diagram representing digital clock signals and their effect on the output voltage of a switched-capacitor integrator circuit.

2. **Axes Labels and Units:**
- The x-axis represents time, labeled in terms of discrete time intervals: \(nT\), \((n + \frac{1}{2})T\), and \((n + 1)T\).
- The y-axis is divided into three sections, each representing different signals:
- \(\phi_1\) and \(\phi_2\) are digital clock signals.
- \(V_o\) is the output voltage.
- \(V_s\) is the sampled input voltage.

3. **Overall Behavior and Trends:**
- **Clock Signals (\(\phi_1\) and \(\phi_2\)):**
- \(\phi_1\) is high during the first half of the clock period and low during the second half.
- \(\phi_2\) is the inverse of \(\phi_1\), low during the first half and high during the second half.
- **Output Voltage (\(V_o\)):**
- The output voltage \(V_o\) shows discrete steps, increasing at the end of each clock cycle. The change in \(V_o\) is given by the equation \(V_o[n+1] = V_o[n] + \frac{C_S}{C_I}V_s[n]\).
- **Sampled Input Voltage (\(V_s\)):**
- The input voltage \(V_s\) is sampled and held constant during each clock cycle, showing a step-like increase corresponding to the sampled values.

4. **Key Features and Technical Details:**
- The clock signals \(\phi_1\) and \(\phi_2\) are non-overlapping, which is crucial for the proper operation of the switched-capacitor circuit.
- The output voltage \(V_o\) changes at discrete intervals, determined by the sampling of \(V_s\) and the ratio of the capacitors \(C_S\) and \(C_I\).
- The timing diagram illustrates the integration process as \(V_o\) accumulates the effect of the input signal \(V_s\) over time.

5. **Annotations and Specific Data Points:**
- The diagram includes annotations for the timing intervals and the relationship between \(V_o[n+1]\), \(V_o[n]\), and \(V_s[n]\).
- Key times are marked by vertical dashed lines, indicating the transition points in the clock signals and corresponding changes in \(V_o\) and \(V_s\).

image_name:Figure 6.10 (a)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: R, type: Resistor, value: 1/fCs, ports: {N1: Vs, N2: InN(A0)}
name: CI, type: Capacitor, value: CI, ports: {Np: InN(A0), Nn: Vo}
name: Ao, type: OpAmp, value: Ao, ports: {InP: GND, InN: InN(A0), Out: Vo}
]
extrainfo:This is a switched-capacitor integrator circuit. The circuit integrates the input voltage Vs over time and produces an output voltage Vo. The timing diagram illustrates the integration process, showing how Vo accumulates the effect of Vs. The op-amp Ao stabilizes the summing-node voltage to ground after transients. The resistor R is defined by the equation R = 1/(fCs), where f is the frequency and Cs is the capacitance.

Figure 6.10 (a) Schematic of a
switched-capacitor integrator.
(b) Timing diagram. (c) Continuoustime equivalent circuit for input frequencies much less than the clock frequency.
change in the summing-node voltage causes the op-amp output to move so that the summingnode voltage is driven back to ground. After the transient has gone to completion, the voltage across $C_{S}$ is driven to zero.

To find the relationship between the input and output, a charge-conservation analysis is used. After transistor $M_{1}$ opens in Fig. 6.10a, the charge on the plates of the capacitors connected to node Top and the inverting op-amp input is conserved until $M_{1}$ closes again. Define time points $[n]$ and $[n+1 / 2]$ as the time indexes at which $\phi_{1}$ and $\phi_{2}$ first fall in Fig. $6.10 b$, respectively. Point $[n+1]$ is defined as the next time index at which $\phi_{1}$ falls. The points $[n]$ and $[n+1]$ are separated by one clock period $T$. If the switches and the op amp are
ideal, the charge stored at time index $[n]$ is

$$
\begin{equation*}
Q[n]=\left(0-V_{s}[n]\right) C_{S}+\left(0-V_{o}[n]\right) C_{I} \tag{6.33}
\end{equation*}
$$

Under the same conditions, the charge stored at time index $[n+1 / 2]$ is

$$
\begin{equation*}
Q[n+1 / 2]=(0) C_{S}+\left(0-V_{o}[n+1 / 2]\right) C_{I} \tag{6.34}
\end{equation*}
$$

From charge conservation, $Q[n+1 / 2]=Q[n]$. Also, the charge stored on $C_{I}$ is constant during $\phi_{1}$ under these conditions; therefore, $V_{o}[n+1]=V_{o}[n+1 / 2]$. Combining these relations gives

$$
\begin{equation*}
V_{o}[n+1]=V_{o}[n]+\left(\frac{C_{S}}{C_{I}}\right) V_{s}[n] \tag{6.35}
\end{equation*}
$$

Thus, one complete clock cycle results in a change in the integrator output voltage that is proportional to the value of the input voltage and to the capacitor ratio.

Equation 6.35 can be used to find the frequency response of the integrator by using the fact that the operation of delaying a signal by one clock period $T$ in the time domain corresponds to multiplication by the factor $e^{-j \omega T}$ in the frequency domain. Thus

$$
\begin{equation*}
V_{o}(j \omega)=V_{o}(j \omega) e^{-j \omega T}+\left(\frac{C_{S}}{C_{I}}\right) V_{s}(j \omega) e^{-j \omega T} \tag{6.36}
\end{equation*}
$$

Therefore, the integrator frequency response is

$$
\begin{equation*}
\frac{V_{o}}{V_{s}}(j \omega)=-\frac{C_{S}}{C_{I}}\left(\frac{1}{1-e^{j \omega T}}\right)=\frac{C_{S}}{C_{I}}\left(\frac{2 j}{e^{j \omega T / 2}-e^{-j \omega T / 2}}\right)\left(\frac{e^{-j \omega T / 2}}{2 j}\right) \tag{6.37}
\end{equation*}
$$

Using the identity

$$
\begin{equation*}
\sin x=\frac{1}{2 j}\left(e^{j x}-e^{-j x}\right) \tag{6.38}
\end{equation*}
$$

in (6.37) with $x=\omega T / 2$ we find

$$
\begin{equation*}
\frac{V_{o}}{V_{s}}(j \omega)=\frac{C_{S}}{C_{I}}\left(\frac{\omega T / 2}{\sin \omega T / 2}\right)\left(\frac{e^{-j \omega T / 2}}{2 j \omega T / 2}\right)=\frac{1}{\frac{j \omega}{\omega_{o}}}\left(\frac{\omega T / 2}{\sin \omega T / 2} e^{-j \omega T / 2}\right) \tag{6.39}
\end{equation*}
$$

where

$$
\begin{equation*}
\omega_{o}=\frac{C_{S}}{T C_{I}}=\frac{f C_{S}}{C_{I}}=\frac{1}{\tau} \tag{6.40}
\end{equation*}
$$

where $\tau$ is the time constant of the integrator. Here $f$ is the clock frequency, equal to $1 / T$. For input frequencies that are much less than the clock frequency, the quantity $\omega T$ is much less than unity, and the right-most term in parentheses in (6.39) reduces to unity. The remaining term is simply the frequency response of an analog integrator, as desired. In practical designs, the excess phase and magnitude error contributed by the term in parentheses in (6.39) must often be taken into account. From a conceptual standpoint, however, the circuit can be thought of as providing an analog integration of the signal. Note that the time constant of the integrator is the same as would occur if the sampling capacitor and switches were replaced by a continuousvalue resistor of value $\left(1 / f C_{S}\right)$. This equivalence is illustrated in Fig. 6.10c.

A key advantage of a switched-capacitor integrator compared to its continuous-time counterpart is that the time constant of the switched-capacitor integrator can be much better controlled in practice. The time constant of a continuous-time integrator depends on the product of a resistance and a capacitance as in (6.22). In monolithic technologies, resistance and
capacitance values do not track each other. Therefore, the time constant of a continuous-time integrator is not well controlled over variations in process, supply, and temperature in general. However, the time constant of a switched-capacitor integrator is determined by the ratio of two capacitor values and the clock frequency, as in (6.40). If the two capacitors have the same properties, the ratio is well controlled even when the absolute values are poorly controlled. Since the clock frequency can be precisely determined by a crystal-controlled clock generator, the time constant of a switched-capacitor integrator can be well controlled in monolithic technologies.

A key requirement for the op amps in Figs. $6.9 a$ and $6.10 a$ is that dc currents at the input terminals must be extremely small to minimize the loss of charge over the time when the above analyses assumed that charge was conserved. Therefore, switched-capacitor amplifiers and integrators are ideally suited to the use of op amps with MOS transistors in the input stage.

## 6.2 Deviations from Ideality in Real Operational Amplifiers

Real op amps deviate from ideal behavior in significant ways. The main effects of these deviations are to limit the frequency range of the signals that can be accurately amplified, to place a lower limit on the magnitude of dc signals that can be detected, and to place an upper limit on the magnitudes of the impedance of the passive elements that can be used in the feedback network with the amplifier. This section summarizes the most important deviations from ideality and their effects in applications.

### 6.2.1 Input Bias Current

An input stage for a bipolar transistor op amp is shown in Fig. 6.11. Here $Q_{1}$ and $Q_{2}$ are the input transistors of the amplifier. The base currents of $Q_{1}$ and $Q_{2}$ flow into the amplifier input terminals, and the input bias current is defined as the average of the two input currents:

$$
\begin{equation*}
I_{\mathrm{BIAS}}=\frac{I_{B 1}+I_{B 2}}{2} \tag{6.41}
\end{equation*}
$$

Nonzero bias current violates the assumption made in summing-point analysis that the current into the input terminals is zero. Typical magnitudes for the bias current are 10 to 100 nA
image_name:Figure 6.11 Typical op-amp input stage
description:
[
name: Q1, type: NPN, ports: {C: InP(A0), B: Vin, E: e1e2}
name: Q2, type: NPN, ports: {C: InN(A0), B: Vip, E: e1e2}
name: RC1, type: Resistor, value: RC1, ports: {N1: InP(A0), N2: VCC}
name: RC2, type: Resistor, value: RC2, ports: {N1: InN(A0), N2: VCC}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: e1e2, Nn: GND}
name: A0, type: OpAmp, value: A0, ports: {InP: InP(A0), InN: InN(A0), OutP: Vout}
]
extrainfo:The circuit is a typical op-amp input stage with bipolar NPN transistors as the input devices. It includes biasing resistors RC1 and RC2 and a current source IEE. The circuit is powered by VCC and VEE.

Figure 6.11 Typical op-amp input stage.
for bipolar input devices and less than 0.001 pA for MOS input devices. In dc inverting and noninverting amplifiers, this bias current can cause undesired voltage drops in the resistors forming the feedback network, with the result that a residual dc voltage appears at the output when the amplifier is ideal in all other ways and the external input voltage is zero. In integrator circuits, the input bias current is indistinguishable from the current being integrated and causes the output voltage to change at a constant rate even when $V_{s}$ is zero. To the extent that the currents are equal in the two input leads, however, their effects can be canceled in some applications by including a balancing resistor in series with one of the input leads so that the same resistance is seen looking away from each op-amp input. For example, the differential amplifier of Fig. 6.4 produces zero output with $V_{1}=V_{2}=0$ if identical currents flow in both op-amp input leads. In practice, however, the two input currents are not exactly equal because of random mismatches, causing nonzero output in Fig. 6.4 when $V_{1}=V_{2}=0$.

### 6.2.2 Input Offset Current

For the emitter-coupled pair shown in Fig. 6.11, the two input bias currents will be equal only if the two transistors have equal betas. Geometrically identical devices on the same IC die typically display beta mismatches that are described by a normal distribution with a standard deviation of a few percent of the mean value. Since this mismatch in the two currents varies randomly from circuit to circuit, it cannot be compensated by a fixed resistor. This aspect of op-amp performance is characterized by the input offset current, defined as

$$
\begin{equation*}
I_{O S}=I_{B 1}-I_{B 2} \tag{6.42}
\end{equation*}
$$

Consider the differential amplifier in Fig. 6.4. Repeating the analysis in Section 6.1.4 for that circuit with nonzero $I_{O S}$ and $V_{1}=V_{2}=0$ gives a dc output voltage of

$$
\begin{equation*}
V_{O}=\left(I_{B 2}-I_{B 1}\right) R_{2}=-I_{O S} R_{2} \tag{6.43}
\end{equation*}
$$

If $I_{O S}=0$, then $V_{O}=0$ here. This equation shows that the error in the dc output voltage is proportional to both the input offset current and the feedback resistance under these conditions. The key point is that the size of the feedback resistance is limited by the maximum offset current that can arise and by the allowed error in the dc output voltage in practice. See Problem 6.6.

### 6.2.3 Input Offset Voltage

As described in Chapter 3, mismatches result in nonzero input offset voltage in amplifiers. The input offset voltage is the differential input voltage that must be applied to drive the output to zero. For untrimmed monolithic op amps, this offset is typically 0.1 to 2 mV for bipolar input devices and 1 to 20 mV for MOS input devices. This offset can be nulled with an external potentiometer in the case of stand-alone op amps; however, the variation of offset with temperature (called drift) does not necessarily go to zero when the input offset is nulled. In dc amplifier applications, the offset and drift place a lower limit on the magnitude of the dc voltage that can be accurately amplified. In some sampled-data applications such as switchedcapacitor filters, the input offset voltage of the op amp is sampled and stored on the capacitors every clock cycle. Thus the input offset is effectively canceled and is not a critical parameter. This same principle is used in chopper-stabilized op amps.

### 6.2.4 Common-Mode Input Range

The common-mode input range is the range of dc common-mode input voltages for which an op amp behaves normally with its key parameters, including offset voltage and input bias current,
within specifications. Many years ago, op amps were usually designed to use large equal-andopposite power-supply voltages. For example, the 741 op amp, described in previous editions of this book, often operated with supply voltages of $\pm 15 \mathrm{~V}$, with a corresponding common-mode input range of about $\pm 13 \mathrm{~V}$. In contrast, modern op amps often operate between ground and one positive power-supply voltage of 3 V or less. If the common-mode input range were limited to be 2 V above ground and 2 V below the positive supply in this case, the input stage in such op amps would not operate properly for any common-mode input voltage. Although reducing the gap between the common-mode input range and the supplies overcomes this problem, the inverting amplifier configuration shown in Fig. $6.3 a$ cannot be used without modification when the op amp operates from a single nonzero supply voltage unless the common-mode input range is extended to include ground. In practice, including both power-supply voltages in the common-mode input range is often important. For example, in the noninverting amplifier and voltage follower shown in Fig. 6.3b and Fig. 6.3c, respectively, the op-amp common-mode input voltage is approximately equal to $V_{s}$. Extending the common-mode input range to include both supplies avoids an unnecessary limit to op-amp performance in these configurations. Section 6.8 describes an example op amp with this property, which is called a rail-to-rail common-mode input range.

### 6.2.5 Common-Mode Rejection Ratio (CMRR)

If an op amp has a differential input and a single-ended output, its small-signal output voltage can be described in terms of its differential and common-mode input voltages ( $v_{i d}$ and $v_{i c}$ ) by the following equation

$$
\begin{equation*}
v_{o}=A_{d m} v_{i d}+A_{c m} v_{i c} \tag{6.44}
\end{equation*}
$$

where $A_{d m}$ is the differential-mode gain and $A_{c m}$ is the common-mode gain. As defined in (3.187), the common-mode rejection ratio of the op amp is

$$
\begin{equation*}
\mathrm{CMRR}=\left|\frac{A_{d m}}{A_{c m}}\right| \tag{6.45}
\end{equation*}
$$

From an applications standpoint, the CMRR can be regarded as the change in input offset voltage that results from a unit change in common-mode input voltage. For example, assume that we apply zero common-mode input voltage to the amplifier and then apply just enough differential voltage to the input to drive the output voltage to zero. The dc voltage we have applied is just the input offset voltage $V_{O S}$. If we keep the applied differential voltage constant and increase the common-mode input voltage by an amount $\Delta V_{i c}$, the output voltage will change, by an amount

$$
\begin{equation*}
v_{o}=\Delta V_{o}=A_{c m} \Delta V_{i c}=A_{c m} v_{i c} \tag{6.46}
\end{equation*}
$$

To drive the output voltage back to zero, we will have to change the differential input voltage by an amount

$$
\begin{equation*}
v_{i d}=\Delta V_{i d}=\frac{\Delta V_{o}}{A_{d m}}=\frac{A_{c m} \Delta V_{i c}}{A_{d m}} \tag{6.47}
\end{equation*}
$$

Thus we can regard the effect of finite CMRR as causing a change in the input offset voltage whenever the common-mode input voltage is changed. Using (6.45) and (6.47), we obtain

$$
\begin{equation*}
\mathrm{CMRR}=\left|\frac{A_{d m}}{A_{c m}}\right|=\left(\left.\frac{\Delta V_{i d}}{\Delta V_{i c}}\right|_{V_{o}=0}\right)^{-1}=\left(\frac{\Delta V_{O S}}{\Delta V_{i c}}\right)^{-1} \simeq\left(\left.\frac{\partial V_{O S}}{\partial V_{i c}}\right|_{V_{o}=0}\right)^{-1} \tag{6.48}
\end{equation*}
$$

In circuits such as the differential amplifier of Fig. 6.11, an offset voltage is produced that is a function of the common-mode signal input, producing a voltage at the output that is indistinguishable from the desired signal. For a common-mode rejection ratio of $10^{4}$ (or $80 \mathrm{~dB}),(6.48)$ shows that a $10-\mathrm{V}$ common-mode signal produces a $1-\mathrm{mV}$ change in the input offset voltage.

### 6.2.6 Power-Supply Rejection Ratio (PSRR)

In (6.44), we assumed that the power-supply voltages are constant so that the op-amp output voltage depends only on the differential and common-mode input voltages provided to the op amp. In practice, however, the power-supply voltages are not exactly constant, and variations in the power-supply voltages contribute to the op-amp output. Figure 6.12 shows a block diagram of an op amp with varying power-supply voltages. The small-signal variation on the positive and negative power supplies is $v_{d d}$ and $v_{s s}$, respectively. If $v_{i c}=0$ is assumed for simplicity, the resulting small-signal op-amp output voltage is

$$
\begin{equation*}
v_{o}=A_{d m} v_{i d}+A^{+} v_{d d}+A^{-} v_{s s} \tag{6.49}
\end{equation*}
$$

where $A^{+}$and $A^{-}$are the small-signal gains from the positive and negative power-supplies to the output, respectively. Since op amps should be sensitive to changes in their differentialmode input voltage but insensitive to changes in their supply voltages, this equation is rewritten below in a form that simplifies comparison of these gains:

$$
\begin{align*}
v_{o} & =A_{d m}\left(v_{i d}+\frac{A^{+}}{A_{d m}} v_{d d}+\frac{A^{-}}{A_{d m}} v_{s s}\right)  \tag{6.50}\\
& =A_{d m}\left(v_{i d}+\frac{v_{d d}}{\mathrm{PSRR}^{+}}+\frac{v_{s s}}{\mathrm{PSRR}^{-}}\right)
\end{align*}
$$

where

$$
\begin{equation*}
\mathrm{PSRR}^{+}=\frac{A_{d m}}{A^{+}} \quad \text { and } \quad \mathrm{PSRR}^{-}=\frac{A_{d m}}{A^{-}} \tag{6.51}
\end{equation*}
$$

Figure 6.13 shows one way to interpret (6.50), where the diagram in Fig. 6.12 is redrawn using an op amp with constant power supplies. To set the output in Fig. 6.13 equal to that in Fig. 6.12, the power-supply variations from Fig. 6.12 are included as equivalent differential inputs
image_name:Figure 6.13
description:The block diagram in Figure 6.13 represents an operational amplifier (op-amp) with power supply variations modeled as differential inputs. The primary components and flow of the system are as follows:

1. **Main Components:**
- **Operational Amplifier (Op-Amp):** Denoted as \( A_0 \), it is the central component of the diagram, responsible for amplifying the input signals.
- **Input Voltage Sources:** There are two input voltage sources, \( v_{ic} \) and \( v_{id} \). The input common-mode voltage \( v_{ic} \) is connected to both the non-inverting and inverting inputs of the op-amp, while the differential input voltage \( v_{id} \) is split equally (\( \frac{v_{id}}{2} \)) between the inputs.
- **Power Supplies:** The op-amp is powered by two supply voltages, \( V_{DD} \) and \( V_{SS} \), with variations represented by \( v_{dd} \) and \( v_{ss} \) respectively.

2. **Flow of Information or Control:**
- The input signals \( v_{ic} \) and \( v_{id} \) are applied to the op-amp inputs. The common-mode voltage \( v_{ic} \) is applied directly, while the differential voltage \( v_{id} \) is split between the inverting and non-inverting inputs.
- The op-amp amplifies the differential input signal, and the output voltage \( v_o \) is generated at the output terminal.
- The power supply variations \( v_{dd} \) and \( v_{ss} \) are modeled as equivalent differential inputs, affecting the op-amp's operation.

3. **Labels, Annotations, and Key Indicators:**
- The inputs are labeled as "InP(A_0)" for the non-inverting input and "InN(A_0)" for the inverting input.
- The output voltage is labeled as \( v_o \), with a reference to ground (GND).
- Power supply voltages are labeled \( V_{DD} \) and \( V_{SS} \) with their variations \( v_{dd} \) and \( v_{ss} \).

4. **Overall System Function:**
- The diagram illustrates how power supply variations can be modeled as differential inputs in an op-amp circuit. The goal is to analyze and maximize the Power Supply Rejection Ratio (PSRR) by considering these variations, thereby minimizing their impact on the op-amp's output. This setup helps in understanding the influence of power supply fluctuations on the op-amp's performance and ensuring stable operation by effectively rejecting these variations.

Figure 6.12 Block diagram of an op amp with varying power- supply voltages.
image_name:Figure 6.13
description:The block diagram in Figure 6.13 represents an operational amplifier (op-amp) circuit designed to model the influence of power supply variations as differential inputs. This setup is used to analyze and optimize the Power Supply Rejection Ratio (PSRR), thereby minimizing the impact of these variations on the op-amp's output.

1. **Main Components:**
- **Differential Input Voltage Source (V_id):** The input voltage is represented as a differential signal, \( V_{id} \), split into two equal parts \( \frac{V_{id}}{2} \) at the positive and negative input terminals.
- **Power Supply Rejection Blocks (PSRR+ and PSRR-):** These blocks model the rejection of power supply variations from the positive \( V_{dd} \) and negative \( V_{ss} \) supply voltages. The PSRR+ and PSRR- blocks indicate the op-amp's ability to reject power supply noise.
- **Summing Nodes (x1):** These nodes combine the input differential voltage and the effects of power supply variations.
- **Operational Amplifier (A_0):** The core amplifier block with gain \( A_0 \), which amplifies the differential input signal while ideally rejecting power supply noise.

2. **Flow of Information or Control:**
- The differential input voltage \( V_{id} \) is divided and fed into the summing nodes.
- The power supply variations \( \frac{V_{dd}}{\text{PSRR+}} \) and \( \frac{V_{ss}}{\text{PSRR-}} \) are also fed into the summing nodes, where they are algebraically combined with the differential input voltage.
- The summed input is then fed into the operational amplifier \( A_0 \), which amplifies the signal and ideally rejects the power supply noise.
- The output voltage \( V_o \) is taken from the output of the op-amp, reflecting the amplified input signal with minimized power supply noise effects.

3. **Labels, Annotations, and Key Indicators:**
- \( V_{id} \), \( V_{dd} \), and \( V_{ss} \) are labeled to indicate input and supply voltages.
- PSRR+ and PSRR- are annotated to show the power supply rejection ratios for the positive and negative supplies.
- \( A_0 \) denotes the gain of the op-amp.
- Ground (GND) is indicated for reference.

4. **Overall System Function:**
- The primary function of this system is to amplify the differential input signal \( V_{id} \) while minimizing the impact of variations in the power supply voltages \( V_{dd} \) and \( V_{ss} \). By modeling the power supply variations as differential inputs, the system aims to maximize the PSRR, ensuring stable and accurate op-amp performance even in the presence of power supply fluctuations.

Figure 6.13 Block diagram of an op amp with supply variations modeled in the input differential loop and with $v_{i c}=0$.
in Fig. 6.13. Equation 6.50 and Fig. 6.13 show that the power-supply rejection ratios should be maximized to minimize the undesired contributions to the op-amp output voltage. In practice, the power-supply rejection ratios are functions of frequency and often decrease for increasing frequency.

Power-supply rejection ratio has become an increasingly important parameter in MOS amplifier design as the level of integration increases. With small-scale integration, few transistors could be integrated on one integrated circuit. Therefore, analog and digital functions were isolated from each other on separate chips, avoiding some coupling from the digital circuits to the analog supplies. Also, such separation provides an opportunity to filter interference generated by the digital circuits at the printed-circuit-board level with external capacitors connected in parallel with the supplies. With large-scale integration, however, many transistors can be integrated on one integrated circuit. Integrating analog and digital functions on the same chip reduces cost but increases the coupling from the digital circuits to the analog supplies. In principle, monolithic filter capacitors can be used to reduce the resulting supply variations; however, the required areas of such capacitors are large in practice. For example, if the oxide thickness is $100 \AA$, the capacitance per unit area is $3.45 \mathrm{fF} / \mu \mathrm{m}^{2}$. For a capacitor of $0.01 \mu \mathrm{~F}$ (a commonly used value to filter supplies on printed-circuit boards), the required area is $1.7 \mathrm{~mm}^{2}$. Since many integrated circuits occupy areas less than $100 \mathrm{~mm}^{2}$, this single capacitor would account for a significant fraction of the cost of many integrated circuits.

To reduce the cost, instead of concentrating only on reducing supply variations through filtering, another option is to build circuits with low sensitivities to power-supply variations. The use of fully differential circuit techniques has emerged as an important tool in this effort. Fully differential circuits represent all signals of interest as differences between two corresponding quantities such as voltages or currents. If two identical signal paths are used to determine corresponding quantities, and if the coupling from supply variations to one quantity is the same as to the other quantity, the difference can be independent of the supply variations and the coupling in principle. In practice, mismatches cause differences in the two signal paths, and the coupling may not be identical, causing imperfect cancellation. Also, if the powersupply noise is large enough, nonlinearity may result and limit the extent of the cancellation. Although the op amps considered in this chapter have differential inputs, they are not fully differential because their outputs are single-ended. Fully differential op amps are considered in Chapter 12.

### 6.2.7 Input Resistance

In bipolar transistor input stages, the input resistance is typically in the $100 \mathrm{k} \Omega$ to $1 \mathrm{M} \Omega$ range. Usually, however, the voltage gain is large enough that this input resistance has little effect on circuit performance in closed-loop feedback configurations.

Op amps whose inputs are connected to the gates of MOS transistors have essentially infinite input resistance in principle. In practice, however, MOS-transistor gates connected through package pins to the outside world must be protected against damage by static electricity. This protection is typically achieved by connecting back-biased clamping diodes from $V_{D D}$ and $V_{S S}$ to the gate, and thus the effective input leakage currents are determined by junction leakage and are of the order of picoamps. However, protection is required only at the inputs and outputs of integrated circuits. In internal applications, where op-amp inputs are not connected to the external pins of an integrated circuit, protection is not required and op amps with MOS transistor gates as inputs do realize ultra-high input resistance.

### 6.2.8 Output Resistance

General-purpose bipolar op amps usually use a buffer as an output stage, which typically produces an output resistance on the order of $40 \Omega$ to $100 \Omega$. On the other hand, in MOS technologies, internal op amps usually do not have to drive resistive loads. Therefore, internal MOS op amps usually do not use a buffer output stage, and the resulting output resistance can be much larger than in the bipolar case. In both cases, however, the output resistance does not strongly affect the closed-loop performance except as it affects stability under large capacitive loading, and in the case of power op amps that must drive a small load resistance.

### 6.2.9 Frequency Response

Because of the capacitances associated with devices in the op amp, the voltage gain decreases at high frequencies. This fall-off must usually be controlled by the addition of extra capacitance, called compensation capacitance, to ensure that the circuit does not oscillate when connected in a feedback loop. (See Chapter 9.) This aspect of op-amp behavior is characterized by the unity-gain bandwidth, which is the frequency at which the magnitude of the open-loop voltage gain is equal to unity. For general-purpose amplifiers, this frequency is typically in the 1 to 100 MHz range. This topic is considered in detail in Chapters 7 and 9.

A second aspect of op-amp high-frequency behavior is a limitation of the rate at which the output voltage can change under large-signal conditions. This limitation stems from the limited current available within the circuit to charge the compensation capacitor. This maximum rate, called the slew rate, is described more extensively in Chapter 9.

### 6.2.10 Operational-Amplifier Equivalent Circuit

The effect of some of these deviations from ideality on the low-frequency performance of an op amp in a particular application can be calculated using the equivalent circuit shown in Fig. 6.14. (This model does not include the effects of finite PSRR or CMRR.) Here, the two current sources labeled $I_{\text {BIAS }}$ represent the average value of dc current flowing into the input terminals. The polarity of these current sources shown in Fig. 6.14 applies for an $n p n$ transistor input stage. The current source labeled $I_{O S}$ represents the difference between the currents flowing into the amplifier terminals. For example, if a particular circuit displayed a current of $1.5 \mu \mathrm{~A}$ flowing into the noninverting input terminal and a current of $1 \mu \mathrm{~A}$ flowing into the inverting input terminal, then the value of $I_{\text {BIAS }}$ in Fig. 6.14 would be $1.25 \mu \mathrm{~A}$, and the value of $I_{O S}$ would be $0.5 \mu \mathrm{~A}$.
image_name:Figure 6.14
description:
[
name: IBIAS, type: CurrentSource, ports: {Np: Vip, Nn: GND}
name: IBIAS, type: CurrentSource, ports: {Np: Vin, Nn: GND}
name: IOS/2, type: CurrentSource, ports: {Np: Vip, Nn: Vin}
name: VOS, type: VoltageSource, ports: {Np: Vip, Nn: Vip}
name: Ri, type: Resistor, value: Ri, ports: {N1: Vip, N2: Vin}
name: a(jω)vi, type: VoltageControlledVoltageSource, ports: {Np: x3, Nn: GND}
name: Ro, type: Resistor, value: Ro, ports: {N1: x3, N2: Vout}
]
extrainfo:The circuit is an equivalent model of an operational amplifier, including input offset voltage and current, input and output resistance, and voltage gain.

Figure 6.14 Equivalent circuit for the operational amplifier including input offset voltage and current, input and output resistance, and voltage gain.

## 6.3 Basic Two-Stage MOS Operational Amplifiers

Figure 6.15 shows a schematic of a basic two-stage CMOS op amp. ${ }^{6,7,8}$ A differential input stage drives an active load followed by a second gain stage. An output stage is usually not used but may be added for driving heavy loads off-chip. This circuit configuration provides good common-mode range, output swing, voltage gain, and CMRR in a simple circuit that can be compensated with a single capacitor. The circuit is redrawn in Fig. 6.16, where the ideal current sources are replaced with transistor current mirrors. In this section, we will analyze the various performance parameters of this CMOS op-amp circuit.
image_name:Figure 6.15
description:The circuit is a two-stage CMOS operational amplifier with a differential input stage (M1, M2), a current mirror load (M3, M4), and an output stage (M5). It is powered by VDD and -VSS, with a compensation capacitor CC connected between the intermediate node and the output node.
Figure 6.15 Basic two-stage CMOS operational amplifier.
image_name:Figure 6.16
description:
[
name: M8, type: PMOS, ports: {S: VDD, D: x1, G: x1}
name: M5, type: PMOS, ports: {S: VDD, D: s1s2d5, G: x1}
name: M7, type: PMOS, ports: {S: VDD, D: Vo, G: x1}
name: M1, type: PMOS, ports: {S: s1s2d5, D: x2, G: Vip}
name: M2, type: PMOS, ports: {S: s1s2d5, D: d2d4g6, G: Vin}
name: M3, type: NMOS, ports: {S: -VSS, D: x2, G: x2}
name: M4, type: NMOS, ports: {S: -VSS, D: x2, G: d2d4g6}
name: M6, type: NMOS, ports: {S: -VSS, D: Vo, G: d2d4g6}
name: IBIAS, type: CurrentSource, ports: {Np: VDD, Nn: -VSS}
name: Cc, type: Capacitor, value: Cc, ports: {Np: d2d4g6, Nn: Vo}
]
extrainfo:The circuit is a two-stage CMOS operational amplifier with a differential input stage (M1, M2), a current mirror load (M3, M4), and an output stage (M5). It is powered by VDD and -VSS, with a compensation capacitor CC connected between the intermediate node and the output node.

Figure 6.16 More detailed schematic diagram of a typical two-stage CMOS operational amplifier.

### 6.3.1 Input Resistance, Output Resistance, and Open-Circuit Voltage Gain

The first stage in Fig. 6.16 consists of a $p$-channel differential pair $M_{1}-M_{2}$ with an $n$-channel current mirror load $M_{3}-M_{4}$ and a $p$-channel tail current source $M_{5}$. The second stage consists of an $n$-channel common-source amplifier $M_{6}$ with a $p$-channel current-source load $M_{7}$. Because the op-amp inputs are connected to the gates of MOS transistors, the input resistance is essentially infinite when the op amp is used in internal applications, which do not require the protection diodes described in Section 6.2.7. For the same reason, the input resistance of the second stage of the op amp is also essentially infinite.

The output resistance is the resistance looking back into the second stage with the op-amp inputs connected to small-signal ground:

$$
\begin{equation*}
R_{o}=r_{o 6} \| r_{o 7} \tag{6.52}
\end{equation*}
$$

Although this output resistance is almost always much larger than in general-purpose bipolar op amps, low output resistance is usually not required when driving purely capacitive loads.

Since the input resistance of the second stage is essentially infinite, the voltage gain of the amplifier in Fig. 6.16 can be found by considering the two stages separately. The first stage is precisely the same configuration as that considered in Section 4.3.5. The small-signal voltage gain is

$$
\begin{equation*}
A_{v 1}=\frac{v_{o 1}}{v_{i}}=G_{m 1} R_{o 1} \tag{6.53}
\end{equation*}
$$

where $G_{m 1}$ and $R_{o 1}$ are the transconductance and output resistance of the first stage, respectively. From (4.143) and (4.149),

$$
\begin{equation*}
A_{\nu 1}=g_{m 1}\left(r_{o 2} \| r_{o 4}\right) \tag{6.54}
\end{equation*}
$$

Similarly, the second-stage voltage gain is

$$
\begin{equation*}
A_{\nu 2}=-g_{m 6} R_{o} \tag{6.55}
\end{equation*}
$$

where $R_{o}$ is given in (6.52). As a result, the overall gain of the amplifier is

$$
\begin{equation*}
A_{v}=A_{v 1} A_{v 2}=-g_{m 1}\left(r_{o 2} \| r_{o 4}\right) g_{m 6}\left(r_{o 6} \| r_{o 7}\right) \tag{6.56}
\end{equation*}
$$

This equation shows that the overall gain is related to the quantity $\left(g_{m} r_{o}\right)^{2}$. Recall from (3.27) that

$$
\begin{equation*}
g_{m} r_{o}=\frac{2 V_{A}}{V_{o v}} \tag{6.57}
\end{equation*}
$$

Therefore, the overall voltage gain is a strong function of the Early voltage (which is proportional to the effective channel length) and the overdrive (which is set by the bias conditions).

#### EXAMPLE

Calculate the gain of the op amp in Fig. 6.16 assuming that it uses the $0.8-\mu \mathrm{m}$ process technology described in Table 2.3. Also, assume that $L_{\text {eff }}=0.8 \mu \mathrm{~m}$ and $\left|V_{o v}\right|=\left|V_{G S}-V_{t}\right|=0.2 \mathrm{~V}$ for all devices.

Let $I_{D 2}, I_{D 4}, I_{D 6}$, and $I_{D 7}$ represent the bias currents flowing into the drains of $M_{2}, M_{4}$, $M_{6}$, and $M_{7}$, respectively. Since $I_{D 4}=-I_{D 2}$ and $I_{D 7}=-I_{D 6}$, (6.56) shows that

$$
\begin{align*}
A_{v} & =-g_{m 1}\left(\frac{\frac{\left|V_{A 2}\right|}{\left|I_{D 2}\right|} \frac{V_{A 4}}{\left|I_{D 2}\right|}}{\frac{\left|V_{A 2}\right|}{\left|I_{D 2}\right|}+\frac{V_{A 4}}{\left|I_{D 2}\right|}}\right) g_{m 6}\left(\frac{\frac{V_{A 6}}{I_{D 6}} \frac{\left|V_{A 7}\right|}{I_{D 6}}}{\frac{V_{A 6}}{I_{D 6}}+\frac{\left|V_{A 7}\right|}{I_{D 6}}}\right)  \tag{6.58}\\
& =-\frac{g_{m 1}}{\left|I_{D 2}\right|} \frac{g_{m 6}}{I_{D 6}}\left(\frac{\left|V_{A 2}\right| V_{A 4}}{\left|V_{A 2}\right|+V_{A 4}}\right)\left(\frac{V_{A 6}\left|V_{A 7}\right|}{V_{A 6}+\left|V_{A 7}\right|}\right)
\end{align*}
$$

where the absolute-value function has been used so that each quantity in (6.58) is positive. From (1.181),

$$
\begin{equation*}
A_{v}=-\frac{2}{\left|V_{o v 1}\right|} \frac{2}{V_{o v 6}}\left(\frac{\left|V_{A 2}\right| V_{A 4}}{\left|V_{A 2}\right|+V_{A 4}}\right)\left(\frac{V_{A 6}\left|V_{A 7}\right|}{V_{A 6}+\left|V_{A 7}\right|}\right) \tag{6.59}
\end{equation*}
$$

because $I_{D 1}=I_{D 2}$ with zero differential input. From (1.163),

$$
\begin{equation*}
V_{A}=L_{\mathrm{eff}}\left(\frac{d X_{d}}{d V_{D S}}\right)^{-1} \tag{6.60}
\end{equation*}
$$

Substituting (6.60) into (6.59) with the given data and $d X_{d} / d V_{D S}$ from Table 2.3 gives

$$
A_{v}=-\frac{2}{0.2} \frac{2}{0.2}\left(\frac{\frac{0.8}{0.04} \times \frac{0.8}{0.08}}{\frac{0.8}{0.04}+\frac{0.8}{0.08}}\right)^{2} \simeq-4400
$$

The overall gain can be increased by either increasing the channel lengths of the devices to increase the Early voltages or by reducing the bias current to reduce the overdrives.

### 6.3.2 Output Swing

The output swing is defined to be the range of output voltages $V_{o}=V_{O}+v_{o}$ for which all transistors operate in the active region so that the gain calculated in (6.56) is approximately
constant. From inspection of Fig. 6.16, $M_{6}$ operates in the triode region if the output voltage is less than $V_{o v 6}-V_{S S}$. Similarly, $M_{7}$ operates in the triode region if the output voltage is more than $V_{D D}-\left|V_{o v 7}\right|$. Therefore, the output swing is

$$
\begin{equation*}
V_{o v 6}-V_{S S} \leq V_{o} \leq V_{D D}-\left|V_{o v 7}\right| \tag{6.61}
\end{equation*}
$$

This inequality shows that the op amp can provide high gain while its output voltage swings within one overdrive of each supply. Beyond these limits, one of the output transistors enters the triode region, where the overall gain of the amplifier would be greatly diminished. As a result, the output swing can be increased by reducing the overdrives of the output transistors.

### 6.3.3 Input Offset Voltage

In Sections 3.5.6 and 6.2.3, the input offset voltage of a differential amplifier was defined as the differential input voltage for which the differential output voltage is zero. Because the op amp in Fig. 6.16 has a single-ended output, this definition must be modified here. Referring to the voltage between the output node and ground as the output voltage, the most straightforward modification is to define the input offset voltage of the op amp as the differential input voltage for which the op-amp output voltage is zero. This definition is reasonable if $V_{D D}=V_{S S}$ because setting the output voltage to zero maximizes the allowed variation in the output voltage before one transistor operates in the triode region provided that $V_{o v 6}=\left|V_{o v 7}\right|$. If $V_{D D} \neq V_{S S}$, however, the output voltage should be set midway between the supply voltages to maximize the output swing. Therefore, we will define the input offset voltage of op amps with differential inputs and single-ended outputs as the differential input voltage for which the dc output voltage is midway between the supplies.

The offset voltage of an op amp is composed of two components: the systematic offset and the random offset. The former results from the design of the circuit and is present even when all the matched devices in the circuit are identical. The latter results from mismatches in supposedly identical pairs of devices.

Systematic Offset Voltage. In bipolar technologies, the gain of each stage in an op amp can be quite high (on the order of 500) because the $g_{m} r_{o}$ product is usually greater than 1000 . As a result, the input-referred offset voltage of a bipolar op amp usually depends mainly on the design of the first stage. In MOS technologies, however, the $g_{m} r_{o}$ product is usually between about 20 and 100 , reducing the gain per stage and sometimes causing the offset of the second stage to play an important role in determining the op-amp offset voltage.

To study the systematic offset, Fig. 6.17 shows the op amp of Fig. 6.16 split into two separate stages. If the inputs of the first stage are grounded, and if the matching is perfect, then the dc drain-source voltage of $M_{4}$ must be equal to the dc drain-source voltage of $M_{3}$. This result stems from the observation that if $V_{D S 3}=V_{D S 4}$, then $V_{D S 1}=V_{D S 2}$ and $I_{D 1}=I_{D 2}=I_{D 5} / 2$. Therefore, with $V_{D S 3}=V_{D S 4}, I_{D 3}=I_{D 4}=-I_{D 5} / 2$. As a result, $V_{D S 3}$ must be equal to $V_{D S 4}$ because this operating point is the only point for which the current flowing out of the drain of $M_{2}$ is equal to the current flowing into the drain of $M_{4}$. For example, increasing the drainsource voltage of $M_{4}$ would increase the current flowing into the drain of $M_{4}$ but decrease the current flowing out of the drain of $M_{2}$ because of the effects of channel-length modulation. Therefore, the dc drain-source voltages of $M_{3}$ and $M_{4}$ must be equal under these conditions.

On the other hand, the value of the gate-source voltage of $M_{6}$ required to set the amplifier output voltage midway between the supplies may differ from the dc output voltage of the first stage. If the first stage gain is 50 , for example, each $50-\mathrm{mV}$ difference in these voltages results in 1 mV of input-referred systematic offset. Ignoring channel-length modulation in $M_{5}$ and $M_{7}$, the current in these transistors is independent of their drain-source voltages if they operate
image_name:Figure 6.17
description::This is a two-stage amplifier circuit. The first stage consists of a differential amplifier formed by M1, M2, M3, and M4. The second stage is a common-source amplifier using M6 and M7. The circuit is designed to set the amplifier output voltage midway between the supplies by adjusting the gate-source voltage of M6.

Figure 6.17 Two-stage amplifier with first and second stages disconnected to show the effect of interstage coupling on inputreferred offset voltage.
in the active region. To set the output voltage midway between the supplies, the gate-source voltage of $M_{6}$ should be chosen so that the drain current of $M_{6}$ is equal to the drain current of $M_{7}$ while both transistors operate in the active region. When the input of the second stage is connected to the output of the first stage, $V_{G S 6}=V_{D S 4}$. With perfect matching and zero input voltages, $V_{D S 4}=V_{D S 3}=V_{G S 3}$ and $V_{t 3}=V_{t 4}=V_{t 6}$. Therefore,

$$
\begin{equation*}
V_{o v 3}=V_{o v 4}=V_{o v 6} \tag{6.62}
\end{equation*}
$$

is required. Substituting (1.166) into (6.62) gives

$$
\begin{equation*}
\frac{I_{D 3}}{(W / L)_{3}}=\frac{I_{D 4}}{(W / L)_{4}}=\frac{I_{D 6}}{(W / L)_{6}} \tag{6.63}
\end{equation*}
$$

In other words, requiring that the transistors have equal overdrives is equivalent to requiring that they have equal drain-current-to-W/L ratios (or current densities). Since $I_{D 3}=I_{D 4}=\left|I_{D 5}\right| / 2$ and $I_{D 6}=\left|I_{D 7}\right|$,

$$
\begin{equation*}
\frac{\left|I_{D 5}\right|}{2(W / L)_{3}}=\frac{\left|I_{D 5}\right|}{2(W / L)_{4}}=\frac{\left|I_{D 7}\right|}{(W / L)_{6}} \tag{6.64}
\end{equation*}
$$

Since $M_{5}$ and $M_{7}$ have equal gate-source voltages,

$$
\begin{equation*}
\frac{I_{D 5}}{I_{D 7}}=\frac{(W / L)_{5}}{(W / L)_{7}} \tag{6.65}
\end{equation*}
$$

Substituting (6.65) into (6.64) gives

$$
\begin{equation*}
\frac{(W / L)_{3}}{(W / L)_{6}}=\frac{(W / L)_{4}}{(W / L)_{6}}=\frac{1}{2} \frac{(W / L)_{5}}{(W / L)_{7}} \tag{6.66}
\end{equation*}
$$

With the aspect ratios chosen to satisfy (6.66), $M_{3}, M_{4}$, and $M_{6}$ operate with equal current densities. In the active region, the current density of a device depends not only on its gate-source voltage, but also on its drain-source voltage to some extent. Since the gate-source voltages and current densities of $M_{3}, M_{4}$, and $M_{6}$ are equal, the drain-source voltages of these transistors
must also be equal. Therefore, the dc output voltage under these conditions is

$$
\begin{equation*}
V_{O}=V_{D S 6}-V_{S S}=V_{D S 3}-V_{S S}=V_{G S 3}-V_{S S}=V_{t 3}+V_{o v 3}-V_{S S} \tag{6.67}
\end{equation*}
$$

To find the systematic offset voltage at the op-amp output, the output voltage in (6.67) should be subtracted from a voltage midway between the supplies. To refer the systematic offset voltage to the op-amp input, this difference should be divided by the op-amp gain. The result is

$$
\begin{equation*}
V_{O S(s y s)}=\frac{\frac{V_{D D}-V_{S S}}{2}-\left(V_{t 3}+V_{o v 3}-V_{S S}\right)}{A_{v}} \tag{6.68}
\end{equation*}
$$

where $A_{v}$ is the op-amp gain given in (6.56). In most cases, the dc output voltage will not be midway between the supplies because $V_{G S 3}=V_{t 3}+V_{o v 3} \neq\left(V_{D D}+V_{S S}\right) / 2$. Therefore, the systematic offset is usually nonzero. Although the systematic offset voltage is nonzero in general, the choice of aspect ratios as given in (6.66) can result in an operating point that is insensitive to process variations, as explained next.

Equation 2.35 shows that the effective channel length of a MOS transistor differs from its drawn length by offset terms caused by the side diffusion of the source and drain $\left(L_{d}\right)$ and the depletion region width around the drain $\left(X_{d}\right)$. Similarly, the effective width of a MOS transistor differs from the drawn width by an offset term $d W$ caused by the bird's-beak effect in the oxide described in Section 2.9.1. To keep the ratio in (6.66) constant in the presence of process-induced variations in $L_{d}, X_{d}$, and $d W$, the drawn channel lengths and widths of the ratioed transistors can each be chosen to be identical. In this case, the ratio in (6.66) can be set equal to any rational number $J / K$ by connecting $J$ identical devices called $n$-channel units in parallel to form $M_{3}$ and $M_{4}$ while $K n$-channel units in parallel form $M_{6}$. Then if $M_{5}$ is constructed of $2 J$ identical devices called $p$-channel units, $M_{7}$ should be constructed from $K p$-channel units. In practice for matched devices, the channel lengths are almost never ratioed directly because the use of small channel lengths for high-speed operation would result in a large sensitivity to process variations. On the other hand, the channel widths of matched devices are sometimes ratioed directly when the width is large enough to make the resulting sensitivity to process variations insignificant.

A key point of this analysis is that the use of identical channel lengths for $M_{3}, M_{4}$, and $M_{6}$ conflicts with a combination of other requirements. First, for stability reasons described in Chapter $9, M_{6}$ should have a large transconductance and thus a short channel length. Second, for low noise and random input offset voltage, $M_{3}$ and $M_{4}$ should have a small transconductance and therefore a long channel length. Noise is considered in Chapter 11, and random input offset voltage is considered next.

Random Input Offset Voltage. As described in Section 3.5.6, source-coupled pairs generally display a higher random offset than their bipolar counterparts. Ignoring the contribution of the second stage in the op amp to the input-referred random offset, a straightforward analysis for the offset voltage of the circuit of Fig. 6.16, which is analogous to the analysis leading to (3.248), gives

$$
\begin{align*}
V_{O S} \simeq & \Delta V_{t(1-2)}+\Delta V_{t(3-4)}\left(\frac{g_{m 3}}{g_{m 1}}\right) \\
& +\frac{V_{o v(1-2)}}{2}\left[\frac{\Delta\left(\frac{W}{L}\right)_{(3-4)}}{\left(\frac{W}{L}\right)_{(3-4)}}-\frac{\Delta\left(\frac{W}{L}\right)_{(1-2)}}{\left(\frac{W}{L}\right)_{(1-2)}}\right] \tag{6.69}
\end{align*}
$$

The first term represents the threshold mismatch of the input transistors. The second is the threshold mismatch of the current-mirror-load devices and is minimized by choosing the $W / L$ ratio of the load devices so that their transconductance is small compared to that of the input transistors. For this reason, selecting a longer channel length for $M_{3}$ and $M_{4}$ than for $M_{1}$ and $M_{2}$ reduces the random input offset voltage. The third term represents the effects of $W / L$ mismatches in the input transistors and loads and is minimized by operating the input transistors at low values of overdrive, typically on the order of 50 to 200 mV .

### 6.3.4 Common-Mode Rejection Ratio

For the op amp in Fig. 6.16, (6.45) gives

$$
\begin{equation*}
\mathrm{CMRR}=\left|\frac{A_{d m}}{A_{c m}}\right|=\left|\frac{\frac{v_{o}}{v_{o 1}} \frac{v_{o 1}}{v_{i d}}}{\frac{v_{o}}{v_{o 1}} \frac{v_{o 1}}{v_{i c}}}\right|=\mathrm{CMRR}_{1} \tag{6.70}
\end{equation*}
$$

where $\mathrm{CMRR}_{1}$ is the common-mode rejection ratio of the first stage. The second stage does not contribute to the common-mode rejection ratio of the op amp because the second stage has a single-ended input and a single-ended output. In (4.182) and (4.183), the common-mode rejection ratio of a stage with a differential pair and a current-mirror load was calculated assuming perfect matching. Applying (4.183) here gives

$$
\begin{equation*}
\text { CMRR } \simeq\left(2 g_{m(d p)} r_{\mathrm{tail}}\right) g_{m(m i r)}\left(r_{o(d p)} \| r_{o(m i r)}\right) \tag{6.71}
\end{equation*}
$$

where $g_{m(d p)}$ and $r_{o(d p)}$ are the transconductance and output resistance of $M_{1}$ and $M_{2}, g_{m(m i r)}$ and $r_{o(m i r)}$ are the transconductance and output resistance of $M_{3}$ and $M_{4}$, and $r_{\text {tail }}$ is the output resistance of $M_{5}$. By a process similar to the derivation of (6.59), this equation can be simplified to give

$$
\begin{equation*}
\mathrm{CMRR} \simeq\left|\frac{2}{V_{o v(d p)}} \frac{2}{V_{o v(m i r)}}\left(\frac{V_{A(d p p} V_{A(m i r)}}{\left|V_{A(d p)}\right|+\left|V_{A(m i r)}\right|}\right)\right| \tag{6.72}
\end{equation*}
$$

where $V_{o v(d p)}$ and $V_{A(d p)}$ are the overdrive and Early voltage of the differential pair, and $V_{o v(\text { mir })}$ and $V_{A(m i r)}$ are the overdrive and Early voltage of the mirror. Equation 6.72 shows that the common-mode rejection ratio of the op amp can be increased by reducing the overdrive voltages.

Another way to increase the common-mode rejection ratio is to replace the simple current mirror $M_{5}$ and $M_{8}$ with one of the high-output-resistance current mirrors considered in Chapter 4. Unfortunately, such a replacement would also worsen the common-mode input range.

### 6.3.5 Common-Mode Input Range

The common-mode input range of the op amp in Fig. 6.16 is the range of dc common-mode input voltages for which all transistors in the first stage operate in the active region. To operate in the active region, the gate-drain voltages of $n$-channel transistors must be less than their thresholds so that their channels do not exist at their drains. Similarly, $p$-channel transistors operate in the active region only if their gate-drain voltages are more than their thresholds, again so that their channels do not exist at their drains. With a pure common-mode input $V_{I C}$ applied to the inputs of the op amp in Fig. 6.16,

$$
\begin{equation*}
V_{D S 4}=V_{D S 3}=V_{G S 3}=V_{t 3}+V_{o v 3} \tag{6.73}
\end{equation*}
$$

The gate-drain voltage of $M_{1}$ and $M_{2}$ is

$$
\begin{equation*}
V_{G D 1}=V_{G D 2}=V_{I C}-V_{t 3}-V_{o v 3}+V_{S S} \tag{6.74}
\end{equation*}
$$

When $V_{I C}$ is reduced to the point at which $V_{G D 1}=V_{G D 2}=V_{t 1}=V_{t 2}, M_{1}$ and $M_{2}$ operate at the edge between the the triode and active regions. This point defines the lower end of the common-mode range, which is

$$
\begin{equation*}
V_{I C}>V_{t 1}+V_{t 3}+V_{o v 3}-V_{S S} \tag{6.75}
\end{equation*}
$$

If $V_{I C}$ is too high, however, $M_{5}$ operates in the triode region. The drain-source voltage of $M_{5}$ is

$$
\begin{equation*}
V_{D S 5}=V_{I C}-V_{G S 1}-V_{D D}=V_{I C}-V_{t 1}-V_{o v 1}-V_{D D} \tag{6.76}
\end{equation*}
$$

From the standpoint of drain-source voltages, $n$-channel transistors operate in the active region only if their drain-source voltage is more than their overdrive. On the other hand, $p$-channel transistors operate in the active region only if their drain-source voltage is less than their overdrive. Therefore, the upper end of the common-mode input range is

$$
\begin{equation*}
V_{I C}<V_{t 1}+V_{o v 1}+V_{o v 5}+V_{D D} \tag{6.77}
\end{equation*}
$$

Since $M_{1}$ and $M_{5}$ are $p$-channel transistors, their overdrives are negative; that is, their gate-source voltages must be less than their thresholds for the channel to exist at the source. Furthermore, if $M_{1}$ is an enhancement-mode device, its threshold is negative because it is p-type. Under this assumption, the common-mode range limits in (6.75) and (6.77) can be rewritten as

$$
\begin{equation*}
V_{t 3}-\left|V_{t 1}\right|+V_{o v 3}-V_{S S}<V_{I C}<V_{D D}-\left|V_{t 1}\right|-\left|V_{o v 1}\right|-\left|V_{o v 5}\right| \tag{6.78}
\end{equation*}
$$

This inequality shows that the magnitudes of the overdrive terms should be minimized to maximize the common-mode range. Also, the body effect on the input transistors can be used to increase the range. If the bodies of $M_{1}$ and $M_{2}$ are connected to $V_{D D}$ as implied in Fig. 6.16, the source-body voltage of these transistors is low when $V_{I C}$ is high. Therefore, the upper limit in (6.78) can be found approximately by using the zero-bias value of $V_{t 1}$. On the other hand, when $V_{I C}$ decreases, the source-body voltage of $M_{1}$ and $M_{2}$ becomes more negative, widening the depletion region around the source and making the threshold voltage of these transistors more negative. Therefore, the body effect can be used to include the negative supply in the common-mode range.

#### EXAMPLE

For the two-stage CMOS op amp in Fig. 6.16, choose the device sizes to give a dc voltage gain greater than 5000 and a peak output swing of at least 1 V . Use the $0.4 \mu \mathrm{~m}$ CMOS model parameters in Table 2.4. Use bias currents of $\left|I_{D 1}\right|=\left|I_{D 2}\right|=100 \mu \mathrm{~A}$, and $I_{D 6}=400 \mu \mathrm{~A}$. Assume $V_{D D}=V_{S S}=1.65 \mathrm{~V} \pm 0.15 \mathrm{~V}$. Assume perfect matching and that all transistors operate in the active (or saturation) region with dc voltages $V_{I C}=0$ (where $V_{I C}$ is the commonmode input voltage), $V_{I}=0$ and $V_{O} \simeq 0$. Ignore the body effect.

To simplify the design, a drawn channel length $L=1 \mu \mathrm{~m}$ will be used for all transistors. This selection avoids short-channel effects that degrade output resistance and cause transistor operation to deviate from the square-law equations.

Since the peak output swing should be 1 V and the magnitude of each supply is at least $1.5 \mathrm{~V},(6.61)$ shows that

$$
V_{o v 6}=\left|V_{o v 7}\right| \leq 0.5 \mathrm{~V}
$$

To maximize the transition frequency $f_{T}$ of each device subject to this constraint, we will choose $V_{o v 6}=\left|V_{o v 7}\right|=0.5 \mathrm{~V}$. Using (1.157) with $\left|I_{D 7}\right|=I_{D 6}=400 \mu \mathrm{~A}$ gives

$$
\left(\frac{W}{L}\right)_{7}=\frac{2\left|I_{D 7}\right|}{k_{p}^{\prime}\left(V_{o v 7}\right)^{2}}=\frac{2(400)}{64.7(-0.5)^{2}} \simeq 50
$$

and

$$
\left(\frac{W}{L}\right)_{6}=\frac{2 I_{D 6}}{k_{n}^{\prime}\left(V_{o v 6}\right)^{2}}=\frac{2(400)}{194(0.5)^{2}} \simeq 16
$$

Since $V_{o v 5}=V_{o v 7}$ by KVL and $I_{D 1}+I_{D 2}=I_{D 7} / 2$,

$$
\left(\frac{W}{L}\right)_{5}=\frac{1}{2}\left(\frac{W}{L}\right)_{7} \simeq 25
$$

From (6.66),

$$
\left(\frac{W}{L}\right)_{3}=\left(\frac{W}{L}\right)_{4}=\frac{1}{2} \frac{(W / L)_{5}}{(W / L)_{7}}(W / L)_{6} \simeq \frac{1}{2}\left(\frac{25}{50}\right) 16=4
$$

Since the common-mode input range should include $V_{I C}=0$, the allowed overdrives on $M_{1}$ and $M_{2}$ are limited by (6.77), and rearranging this equation with $V_{I C}=0$ and $V_{D D}=1.5 \mathrm{~V}$ gives

$$
V_{o v 1}>V_{I C}-V_{t 1}-V_{o v 5}-V_{D D}=0-(-0.8 \mathrm{~V})-(-0.5 \mathrm{~V})-1.5 \mathrm{~V}=-0.2 \mathrm{~V}
$$

Therefore,

$$
\left(\frac{W}{L}\right)_{1}=\left(\frac{W}{L}\right)_{2}>\frac{2\left|I_{D 1}\right|}{k_{p}^{\prime}\left(V_{o v 1}\right)^{2}}=\frac{2(100)}{64.7(-0.2)^{2}} \simeq 77
$$

From (6.59) and (6.60) with $L_{\text {eff }} \simeq L_{\mathrm{drwn}}-2 L_{d}$, and using data from Table 2.4,

$$
\begin{array}{r}
A_{v}=-\frac{2}{\left|V_{o v 1}\right|} \frac{2}{V_{o v 6}}\left(\frac{\left|V_{A 2}\right| V_{A 4}}{\left|V_{A 2}\right|+V_{A 4}}\right)\left(\frac{V_{A 6}\left|V_{A 7}\right|}{V_{A 6}+\left|V_{A 7}\right|}\right) \\
=-\frac{2}{0.2} \frac{2}{0.5}\left(\frac{\frac{0.82}{0.04} \times \frac{0.82}{0.02}}{\frac{0.82}{0.04}+\frac{0.82}{0.02}}\right)^{2} \simeq-7500
\end{array}
$$

This calculation assumes that $d X_{d} / d V_{D S}$ and $L_{\text {eff }}$ are constant for each type of transistor, allowing us to use constant Early voltages. In practice, however, $d X_{d} / d V_{D S}$ and $L_{\text {eff }}$ both depend on the operating point, and accurate values of the Early voltages are rarely available to circuit designers when channel lengths are less than about $1.5 \mu \mathrm{~m}$. As a result, circuit simulations are an important part of the design process. SPICE simulation of the op amp under the conditions described above gives a gain of about 6200, which shows that the hand calculations are accurate within about 20 percent.

### 6.3.6 Power-Supply Rejection Ratio (PSRR)

To calculate the PSRR from the $V_{d d}$ supply for the op amp in Fig. 6.16, we will divide the smallsignal gain $A^{+}=v_{o} / v_{d d}$ into the gain from the input. For this calculation, assume that the $V_{s s}$ supply voltage is constant and that both op-amp inputs in Fig. 6.16 are connected to small-signal grounds. The current in $M_{8}$ is equal to $I_{\text {BIAS. }}$. If this current is constant, the gate-source voltage of $M_{8}$ must be constant because $M_{8}$ is diode connected. Therefore, $v_{g s 8}=v_{g s 5}=v_{g s 7}=0$, and the $g_{m}$ generators in $M_{5}$ and $M_{7}$ are inactive. As a result, if $r_{o 5}=r_{\text {tail }} \rightarrow \infty$ and $r_{07} \rightarrow \infty$, $v_{o} / v_{d d}=0$. To find the gain with finite $r_{\text {tail }}$ and $r_{o 7}$, consider the small-signal diagrams shown in Fig. 6.18, where the $g_{m}$ generators for $M_{5}$ and $M_{7}$ are omitted because they are inactive. In Fig. $6.18 a$, the output is defined as $v_{o a}$, and the $v_{d d}$ supply variation is set equal to zero at the point where $r_{\text {tail }}$ is connected. In Fig. 6.18b, the output is defined as $v_{o b}$, and the $v_{d d}$ supply variation is set equal to zero at the point where $r_{o 7}$ is connected. We will find $v_{o a}$ and $v_{o b}$ separately and use superposition to find the total gain $v_{o} / v_{d d}=\left(v_{o a}+v_{o b}\right) / v_{d d}$.

In Fig. $6.18 a$, the first stage experiences no variation, and $v_{g 6}=0$. Therefore, $g_{m 6}$ is inactive, and the output stage appears as a simple voltage divider to the supply variation. Since the dc drain current in $M_{6}$ is equal and opposite to that in $M_{7}$,

$$
\begin{equation*}
\frac{v_{o a}}{v_{d d}}=\frac{r_{o 6}}{r_{o 6}+r_{o 7}}=\frac{\frac{V_{A 6}}{I_{D 6}}}{\frac{V_{A 6}}{I_{D 6}}+\frac{\left|V_{A 7}\right|}{I_{D 6}}}=\frac{V_{A 6}}{V_{A 6}+\left|V_{A 7}\right|} \tag{6.79}
\end{equation*}
$$

In Fig. 6.18b,

$$
\begin{equation*}
\frac{v_{o b}}{v_{d d}}=\frac{v_{g s 6}}{v_{d d}} \frac{v_{o b}}{v_{g s 6}} \tag{6.80}
\end{equation*}
$$

where the first term on the right side represents the gain of the first stage, and the second term represents the gain of the second stage. The $v_{d d}$ input to the first stage in Fig. $6.18 b$ is applied between the top of $r_{\text {tail }}$ and ground while the gates of $M_{1}$ and $M_{2}$ are grounded. This situation is equivalent to grounding the top of $r_{\text {tail }}$ and applying a voltage of $-v_{d d}$ between the gates of $M_{1}$ and $M_{2}$ and ground. In other words, the $v_{d d}$ input in Fig. $6.18 b$ appears as a common-mode
image_name:(a)
description:
[
name: M1, type: PMOS, ports: {S: s1s2, D: x1, G: GND}
name: M2, type: PMOS, ports: {S: s1s2, D: d2d4g6, G: GND}
name: M3, type: NMOS, ports: {S: GND, D: x1, G: x1}
name: M4, type: NMOS, ports: {S: GND, D: d2d4g6, G: x1}
name: M6, type: NMOS, ports: {S: GND, D: voa, G: d2d4g6}
name: r_tail, type: Resistor, value: r_tail, ports: {N1: s1s2, N2: GND}
name: r_o7, type: Resistor, value: r_o7, ports: {N1: Vdd, N2: Voa}
]
extrainfo:The circuit is a two-stage operational amplifier. The first stage consists of a differential pair (M1 and M2) with NMOS current mirrors (M3 and M4). The second stage is a common-source amplifier with NMOS transistor M6. Resistors r_tail and r_o7 are used for biasing and load, respectively. The output is taken at Voa.
image_name:(b)
description:
[
name: M1, type: PMOS, ports: {S: s1s2, D: x1, G: GND}
name: M2, type: PMOS, ports: {S: s1s2, D: d2d4g6, G: GND}
name: M3, type: NMOS, ports: {S: GND, D: x1, G: x1}
name: M4, type: NMOS, ports: {S: GND, D: d2d4g6, G: d2d4g6}
name: M6, type: NMOS, ports: {S: GND, D: GND, G: d2d4g6}
name: rtail, type: Resistor, value: rtail, ports: {N1: s1s2, N2: GND}
name: ro7, type: Resistor, value: ro7, ports: {N1: Vdd, N2: GND}
]
extrainfo:This is a small-signal model of a two-stage operational amplifier focusing on coupling from Vdd to the output through the first stage. The circuit includes PMOS transistors M1 and M2, NMOS transistors M3, M4, and M6, and resistors rtail and ro7. The input is applied between the top of rtail and ground, with gates of M1 and M2 grounded, simulating a common-mode input.
Figure 6.18 Small-signal diagrams of the two-stage op amp used to calculate the coupling from $v_{d d}$ to the output $(a)$ through the second stage and $(b)$ through the first stage.
input $v_{i c}=-v_{d d}$ to the first stage. Therefore, the gain of the first stage can be expressed as

$$
\begin{equation*}
\frac{v_{g s 6}}{v_{d d}}=-\frac{v_{g s 6}}{v_{i c}}=-G_{m}[\mathrm{~cm}] R_{o 1} \tag{6.81}
\end{equation*}
$$

where $G_{m}[\mathrm{~cm}]$ is the common-mode transconductance of the first stage and $R_{o 1}$ is the output resistance of the first stage. Substituting (4.149), (4.166), (4.173), and (4.179) into (6.81) gives

$$
\begin{equation*}
\frac{v_{g s 6}}{v_{d d}} \simeq \frac{g_{m(d p)}\left(r_{o(d p)} \| r_{o(m i r)}\right)}{1+2 g_{m(d p)} r_{\text {tail }}}\left(\frac{1}{1+g_{m(m i r)} r_{o(d p)}}+\frac{1}{1+g_{m(m i r)} r_{o(m i r)}}\right) \tag{6.82}
\end{equation*}
$$

If $2 g_{m(d p)} r_{\text {tail }} \gg 1, g_{m(m i r)} r_{o(d p)} \gg 1$, and $g_{m(m i r)} r_{o(m i r)} \gg 1$,

$$
\begin{equation*}
\frac{v_{g s 6}}{v_{d d}} \simeq \frac{r_{o(d p)} \| r_{o(m i r)}}{2 r_{\text {tail }} g_{m(m i r)}\left(r_{o(d p)} \| r_{o(m i r)}\right)}=\frac{1}{2 g_{m(m i r)} r_{\text {tail }}} \tag{6.83}
\end{equation*}
$$

Substituting (6.83), (6.55), and (6.52) into (6.80) gives

$$
\begin{equation*}
\frac{v_{o b}}{v_{d d}} \simeq-\frac{g_{m 6}\left(r_{o 6} \| r_{o 7}\right)}{2 g_{m(\operatorname{mir})} r_{\text {tail }}} \tag{6.84}
\end{equation*}
$$

If $V_{o v 3}=V_{o v 6}$ as in (6.62) to control the systematic offset, $g_{m 6} / g_{m(m i r)}=I_{D 6} / I_{D 3}$. Since the dc drain current in $M_{6}$ is equal and opposite to that in $M_{7}$,

$$
\begin{align*}
\frac{v_{o b}}{v_{d d}} \simeq-\frac{I_{D 6}}{2 I_{D 3}}\left(\frac{\frac{V_{A 6}}{I_{D 6}} \frac{\left|V_{A 7}\right|}{I_{D 6}}}{\frac{V_{A 6}}{I_{D 6}}+\frac{\left|V_{A 7}\right|}{I_{D 6}}}\right) \frac{\left|I_{D 5}\right|}{\left|V_{A 5}\right|} & =-\frac{\left|I_{D 5}\right|}{2 I_{D 3}}\left(\frac{V_{A 6}}{V_{A 6}+\left|V_{A 7}\right|}\right) \frac{\left|V_{A 7}\right|}{\left|V_{A 5}\right|}  \tag{6.85}\\
& =-\frac{V_{A 6}}{V_{A 6}+V_{A 7}}
\end{align*}
$$

because $V_{A 5}=V_{A 7}$ and $\left|I_{D 5}\right|=2 I_{D 3}$. Combining (6.79) and (6.85) gives

$$
\begin{equation*}
A^{+}=\frac{v_{o}}{v_{d d}}=\frac{v_{o a}+v_{o b}}{v_{d d}} \simeq 0 \tag{6.86}
\end{equation*}
$$

Therefore, from (6.51), PSRR $^{+} \rightarrow \infty$ for low frequencies with perfect matching because the coupling from $v_{d d}$ to the output through the first stage cancels that through the second stage. In practice, mismatch can increase the common-mode transconductance of the first stage as shown at the end of Section 4.3.5.3, disrupting this cancellation and decreasing the low-frequency PSRR ${ }^{+}$.

To calculate the PSRR from the $V_{s s}$ supply for the op amp in Fig. 6.16, we will calculate the small-signal gain $A^{-}=v_{o} / v_{s s}$ and then normalize to the gain from the input. For this calculation, assume that the $V_{d d}$ supply voltage is constant and that both op-amp inputs in Fig. 6.16 are connected to small-signal grounds. Under these conditions, $M_{1}$ and $M_{2}$ act as common-gate amplifiers, attempting to keep the bias current in $M_{3}$ and $M_{4}$ constant. If the drain current of $M_{3}$ is constant, the gate-source voltage of $M_{3}$ must be constant because $M_{3}$ is diode connected. Therefore, $v_{g s 3}=0$. Since $v_{d s 3}=v_{g s 3}$, and since $v_{d s 4}=v_{d s 3}$ under these conditions, $v_{d s 4}=v_{g s 6}=0$. Therefore, $g_{m 6}$ is inactive, and the output stage appears as a simple voltage divider to the supply variation. Since the drain current in $M_{6}$ is equal and opposite to that in $M_{7}$,

$$
\begin{equation*}
A^{-}=\frac{v_{o}}{v_{s s}}=\frac{r_{o 7}}{r_{o 6}+r_{o 7}}=\frac{\frac{\left|V_{A 7}\right|}{I_{D 6}}}{\frac{V_{A 6}}{I_{D 6}}+\frac{\left|V_{A 7}\right|}{I_{D 6}}}=\frac{\left|V_{A 7}\right|}{V_{A 6}+\left|V_{A 7}\right|} \tag{6.87}
\end{equation*}
$$

Substituting (6.59) and (6.87) into (6.51) gives

$$
\begin{equation*}
\operatorname{PSRR}^{-}=\frac{A_{d m}}{A^{-}}=\frac{\frac{v_{o}}{v_{i d}}}{\frac{v_{o}}{v_{s s}}}=-\frac{2}{\left|V_{o v 1}\right|} \frac{2}{V_{o v 6}}\left(\frac{\left|V_{A 2}\right| V_{A 4}}{\left|V_{A 2}\right|+V_{A 4}}\right) V_{A 6} \tag{6.88}
\end{equation*}
$$

This equation gives the low-frequency supply rejection from the negative supply. This rejection worsens as frequency increases. The topic of frequency response is covered in detail in Chapters 7 and 9 , but the essence of this behavior can be understood without a complete frequency-response analysis. As the applied frequency increases, the impedance of the compensation capacitor $C_{C}$ in Fig. 6.16 decreases, effectively shorting the gate of $M_{6}$ to its drain for high-frequency ac signals. If the gate-source voltage on $M_{6}$ is constant, the variation on the negative supply is fed directly to the output at high frequencies. Therefore, $A^{-} \simeq 1$ at frequencies high enough to short circuit $C_{C}$, assuming that $C_{C} \gg C_{L}$, where $C_{L}$ is the load capacitance of the op amp connected between the op-amp output and ground. The same phenomenon causes the gains $A_{d m}$ and $A^{+}$to decrease as frequency increases, so that the PSRR ${ }^{+}$ remains relatively constant with increasing frequency. Since $A^{-}$increases to unity as $A_{d m}$ decreases, however, $\mathrm{PSRR}^{-}$decreases and reaches unity at the frequency where $\left|A_{d m}\right|=1$.

Power-Supply Rejection and Supply Capacitance. Another important contribution to nonzero gain between the power supplies and the op-amp output is termed supply capacitance. ${ }^{9,10}$ This phenomenon manifests itself as a capacitive coupling between one or both of the power supplies and the op-amp input leads when the op amp is connected with capacitive feedback $C_{I}$ as shown in Fig. 6.19. For simplicity, assume that the op-amp open-loop gain is infinite. If the supply-coupling capacitance is $C_{\text {sup }}$, the gain from $C_{\text {sup }}$ to the op-amp output is $-C_{\text {sup }} / C_{I}$. Figure 6.19 shows two possible sources of supply capacitance, which are the gate-drain and gate-source capacitance of $M_{1}$. Four important ways in which supply capacitance can occur are described below.
image_name:Figure 6.19
description:The circuit is a two-stage MOS amplifier with capacitive feedback. It includes PMOS and NMOS transistors configured to provide amplification with capacitive feedback through C_I. The circuit also features supply capacitance from the gate-drain and gate-source capacitance of M1. The gain from the supply coupling capacitance to the op-amp output is given by -C_sup / C_I. The circuit is designed to analyze the dependence of the output voltage on the tail current.

Figure 6.19 Supply capacitance in a two-stage MOS amplifier with capacitive feedback.
image_name:(a)
description:
[
name: M0, type: PMOS, ports: {S: d0, D: GND, G: GND}
name: I_TAIL, type: CurrentSource, value: I_TAIL, ports: {Np: VDD, Nn: d0}
name: i_tail, type: CurrentSource, value: i_tail, ports: {Np: VDD, Nn: d0}
]
extrainfo:The circuit is a source follower configuration with PMOS M0 providing amplification. The tail current sources (I_TAIL and i_tail) are connected to the drain of M0. The output voltage is influenced by the tail current and the supply voltage VDD.
image_name:(b)
description:
[
name: i_tail, type: CurrentSource, value: i_tail, ports: {Np: GND, Nn: Vs}
name: r_o, type: Resistor, value: r_o, ports: {N1: VS, N2: GND}
]
extrainfo:The circuit diagram (b) is a small-signal model analyzing the dependence of the output voltage vs on the tail current i_tail. It includes a current source and a resistor connected to the ground, with the node VS representing the voltage across both components.

Figure 6.20 (a) Source follower and (b) small-signal diagram to calculate the dependence of $v_{s}$ on $i_{\text {tail }}$.

1. If the drain current of $M_{3}$ is constant, a variation on $V_{s s}$ causes the voltage from the drain of $M_{1}$ to ground to vary to hold the gate-source voltage of $M_{3}$ constant. This variation couples to the summing node through the gate-drain capacitance of $M_{1}$; that is, the supply capacitance $C_{\text {sup }}=C_{g d 1}$. This problem is usually overcome by the use of cascode transistors in series with the drains of the input transistors.
2. A variation on $V_{d d}$ or $V_{s s}$ causes the current flowing in the tail current source to vary. To understand the effect of this bias-current variation, consider Fig. 6.20a, which shows a $p$-channel source follower whose biasing current source $I_{\text {tail }}=I_{\text {TAIL }}+i_{\text {tail }}$ is not constant. The source follower models the behavior of $M_{1}$ in Fig. 6.19 from the standpoint of variation in $I_{\text {tail }}$ for two reasons. First, the voltage from the gate of $M_{1}$ to ground is held to smallsignal ground by negative feedback. Second, MOS transistors that operate in the active region are controlled mainly by their gate-source voltages. For simplicity, ignore the body effect because it is not needed to demonstrate the problem here. The small-signal diagram of the source follower is shown in Fig. 6.20b. From KCL at the source,

$$
\begin{equation*}
i_{\mathrm{tail}}=g_{m} v_{s}+\frac{v_{s}}{r_{o}} \tag{6.89}
\end{equation*}
$$

Rearranging this equation gives

$$
\begin{equation*}
v_{s}=\frac{i_{\text {tail }} r_{o}}{1+g_{m} r_{o}} \simeq \frac{i_{\text {tail }}}{g_{m}} \tag{6.90}
\end{equation*}
$$

Therefore, nonzero $i_{\text {tail }}$ arising from supply variations causes nonzero $v_{s}$ in the source follower. Similarly, in Fig. 6.19, the voltage from the source of $M_{1}$ to ground varies with $I_{\text {tail }}$, and this variation couples to the summing node through the gate-source capacitance of $M_{1}$; that is, the supply capacitance $C_{\text {sup }}=C_{g s 1}$. A supply-independent bias reference is usually used to overcome this problem.
3. If the substrate terminal of the input transistors is connected to a supply or a supply-related voltage, then the substrate bias changes as the supply voltage changes. In turn, substrate bias variation changes the threshold through the body effect, which changes the gate-source voltage. Again, this mechanism can be studied with the help of a source follower, as shown in Fig. 6.21a. Here $I_{\text {TAIL }}$ is assumed to be constant, but $V_{d d}=V_{D D}+v_{d d}$ is assumed to vary. The small-signal diagram is shown in Fig. 6.21b. From KCL at the source,

$$
\begin{equation*}
g_{m b} v_{d d}=g_{m} v_{s}+g_{m b} v_{s}+\frac{v_{s}}{r_{o}} \tag{6.91}
\end{equation*}
$$

image_name:(a)
description:
[
name: M0, type: PMOS, ports: {S: Vs+vs, D: GND, G: GND}
name: ITAIL, type: CurrentSource, ports: {Np: VDD+vdd, Nn: Vs+vs}
]
extrainfo:The circuit is a source follower configuration with a PMOS transistor and a constant current source. The small-signal model shows the dependence of the source voltage on the drain-source voltage through the body effect.
image_name:(b)
description:
[
name: gmvgs, type: CurrentSource, ports: {Np: GND, Nn: Vs}
name: gmbvsb, type: CurrentSource, ports: {Np: Vs, Nn: GND}
name: ro, type: Resistor, value: ro, ports: {N1: Vs, N2: GND}
]
extrainfo:The circuit is a small-signal model of a source follower, illustrating the dependence of the source voltage on variations in the supply voltage through the body effect.
Figure 6.21 (a) Source follower and (b) small-signal diagram to calculate the dependence of $v_{s}$ on $v_{d d}$ through the body effect.

Rearranging this equation gives

$$
\begin{equation*}
v_{s}=\frac{g_{m b} r_{o}}{1+\left(g_{m}+g_{m b}\right) r_{o}} v_{d d} \simeq \frac{g_{m b}}{g_{m}+g_{m b}} v_{d d} \tag{6.92}
\end{equation*}
$$

Therefore, nonzero $v_{d d}$ in the source follower in Fig. 6.21 causes nonzero $v_{s}$. Similarly, in Fig. 6.19, the voltage from the source of $M_{1}$ to ground varies with $V_{d d}$, and this variation couples to the summing node through the gate-source capacitance of $M_{1}$; that is, the supply capacitance $C_{\text {sup }}=C_{g s 1}$.

A solution to this problem is to place the input transistors in a well and connect the well to the sources of the input transistors to eliminate the body effect. This solution has two potential disadvantages. First, it disallows the use of the body effect on the input devices to increase the common-mode input range of the op amp, as described in Section 6.3.5. Second, this solution dictates the polarity of the input transistors in a given process. For example, in a $p$-well process, the input devices must be $n$-channel devices to place them in a $p$ well. This requirement might conflict with the polarity of the input transistors that would be chosen for other reasons. For example, $p$-channel input transistors would be used to minimize the input-referred flicker noise. (See Chapter 11.)
4. Interconnect crossovers in the op-amp and system layout can produce undesired capacitive coupling between the supplies and the summing node. In this case, the supply capacitance is a parasitic or undesired capacitance. This problem is usually overcome with careful layout. In particular, one important layout technique is to shield the op-amp inputs with metal lines connected to ground.

The result of supply capacitance can be quite poor power-supply rejection in switchedcapacitor filters and other sampled-data analog circuits that use capacitive feedback. In addition to the solutions to this problem mentioned above, another solution is to use fully differential op amps , which have two outputs. The output voltage of interest is the voltage difference between these outputs. Fully differential op amps, which are considered in Chapter 12, overcome the supply capacitance problem to the extent that the coupling from a given supply to one output is the same as to the other output.

### 6.3.7 Effect of Overdrive Voltages

The overdrive of a MOS transistor can be reduced by reducing the ratio of its drain current to its $W / L$. Reducing the overdrive voltages in the op amp in Fig. 6.16 improves the op-amp
performance by increasing the voltage gain as shown by (6.59), increasing the swing as shown by (6.61), reducing the input offset voltage as shown by (6.69), increasing the CMRR as shown by (6.72), increasing the common-mode range as shown by (6.78), and increasing the power-supply rejection ratio as shown by (6.88). These observations are valid provided that the transistors in the op amp operate in strong inversion. Also, increasing the channel lengths increases the corresponding Early voltages as shown by (1.163), and thereby increases the opamp gain, common-mode rejection ratio, and power-supply rejection ratio as shown by (6.59), (6.72), and (6.88). Unfortunately, the transition frequency of MOS transistors is proportional to the overdrive and inversely proportional to the square of the channel length from (1.209). Therefore, reducing overdrives and increasing the channel lengths degrades the frequency response of the transistors and in turn the amplifier. Thus we find a fundamental trade-off between the frequency response and the other measures of performance in CMOS op-amp design.

### 6.3.8 Layout Considerations

A basic objective in op-amp design is to minimize the mismatch between the two signal paths in the input differential pair so that common-mode input signals are rejected to the greatest possible extent. Mismatch affects the performance of the differential pair not only at dc, where it causes nonzero offset voltage, but also at high frequencies where it reduces the common-mode and power-supply rejection ratios.

Figure $6.22 a$ shows a possible layout of a differential pair. Five nodes are labeled: two gates, two drains, and one source. Connections to each region are omitted for simplicity. The
image_name:(a)
description:The image shows a simplified layout of a differential pair with mirror symmetry, typically used in integrated circuit design to achieve high common-mode rejection. The layout consists of five distinct regions labeled as follows:

1. **D1 (Drain 1):** This region represents the drain of the first transistor in the differential pair.
2. **G1 (Gate 1):** This area corresponds to the gate of the first transistor. It is placed adjacent to the drain and source regions.
3. **S (Source):** This central region is the common source shared by both transistors. The source regions of the two transistors are merged into a single diffusion area to save space and minimize parasitic capacitance.
4. **G2 (Gate 2):** This is the gate of the second transistor, symmetrically placed on the opposite side of the source.
5. **D2 (Drain 2):** This represents the drain of the second transistor, mirroring the layout of the first transistor.

The layout is designed to achieve symmetry, which is crucial for minimizing mismatches that affect performance. The symmetrical arrangement helps in achieving balanced electrical characteristics, which is essential for rejecting common-mode signals effectively. However, the description notes that while this layout conserves area and reduces undesired capacitance, it may not be optimal for matching due to its sensitivity to process variations and other factors.

image_name:(b)
description:The diagram shows a symmetrical differential-pair layout with two capacitors (CP1 and CP2) connected to the drains (D1 and D2) of the transistors. The sources of the transistors are merged into one diffusion region (S). This layout is designed to save area and minimize undesired capacitance.

Figure 6.22 Differential-pair layouts
with mirror symmetry.
sources of the two transistors are connected to each other by merging the two sources together into one diffusion region. Although such a layout saves area and minimizes undesired capacitance connected to the sources, this layout is not optimum from the standpoint of matching in part because it is sensitive to alignment shifts between masks that define various layers in an integrated circuit. The key problem is that the layout in Fig. $6.22 a$ uses only mirror symmetry in the sense that each transistor is a mirror image of the other. For example, suppose that two additional grounded segments of metal are added to the layout to produce the layout shown in Fig. 6.22b. In exactly these locations, the parasitic capacitance $C_{P 1}$ from $D_{1}$ to ground is equal to the parasitic capacitance $C_{P 2}$ from $D_{2}$ to ground. However, if the mask that defines the metal shifts to the right compared to the mask that defines the diffusion, $C_{P 1}$ increases but $C_{P 2}$ decreases, creating mismatch. In practice, balancing the parasitics in a way that is insensitive to alignment shifts is most important in amplifiers that have both differential inputs and differential outputs. Such amplifiers are considered in Chapter 12.

Figure 6.23 shows layouts that overcome these problems. In Fig. 6.23a-b, the transistors are drawn using translational symmetry; that is, each transistor is a copy of the other without rotation. Another option is shown in Fig. 6.23c, where each transistor has been split into two pieces. To maintain the same width/length ratio as in the previous drawings, the width of each transistor in Fig. 6.23c has been reduced by a factor of two. This structure has both translational and mirror symmetry. Structures with translational symmetry are insensitive to alignment shifts.

One limitation of these layouts is that they are sensitive to process gradients perpendicular to the line of symmetry. For example, in Fig. 6.23c, suppose the oxide thickness increases from
image_name:Figure 6.23 (a)
description:The diagram in Figure 6.23 (a) illustrates differential-pair layouts with translational symmetry. It shows two transistors with gates labeled G1 and G2, sources labeled S, and drains labeled D1 and D2. The width (W) and length (L) dimensions are indicated, maintaining symmetry in the layout. This layout is designed to be insensitive to alignment shifts due to its symmetry but may be sensitive to process gradients perpendicular to the line of symmetry.

image_name:(b)
description:
[
name: G1, type: Other, ports: {N1: S, N2: D1, N3: G1}
name: G2, type: Other, ports: {N1: S, N2: D2, N3: G2}
]
extrainfo:The circuit diagram (c) shows a symmetric layout for a differential pair with two transistors. Each transistor has a gate (G1 or G2), source (S), and drain (D1 or D2). The layout is designed with translational symmetry to reduce sensitivity to alignment shifts. The width (W) is divided equally across the transistors, and the length (L) is consistent, maintaining symmetry.

Figure 6.23 Differential-pair layouts with translational symmetry.
image_name:(c)
description:
[
name: M1, type: NMOS, ports: {S: S, D: D1, G: G1}
name: M2, type: NMOS, ports: {S: S, D: D2, G: G2}
name: M3, type: NMOS, ports: {S: S, D: D2, G: G2}
name: M4, type: NMOS, ports: {S: S, D: D1, G: G1}
]
extrainfo:The circuit is a differential pair with a symmetric layout, designed to reduce sensitivity to alignment shifts. It uses translational symmetry and common-centroid structure to alleviate process-related gradients.

image_name:Figure 6.24
description:
[
name: M1, type: NMOS, ports: {S: S, D: D1, G: G1}
name: M2, type: NMOS, ports: {S: S, D: D2, G: G1}
name: M3, type: NMOS, ports: {S: S, D: D2, G: G2}
name: M4, type: NMOS, ports: {S: S, D: D1, G: G2}
]
extrainfo:The circuit diagram shows a common-centroid layout for a differential pair with four NMOS transistors, M1, M2, M3, and M4. The layout is symmetric to minimize process-related variations, with gates G1 and G2 controlling the respective pairs of transistors. This design helps reduce mismatches due to process gradients across the chip.

Figure 6.24 Common-centroid structure for the MOS differential pair.
left to right. Then the gate stripes connected to $G_{1}$ have thinner oxide than those connected to $G_{2}$, causing the transistors to have unequal thresholds and unequal transconductance parameters. The effects of process-related gradients across the die can be partially alleviated by use of common-centroid geometries. Figure 6.24 shows a common-centroid layout of the differential pair. Each side of the differential pair is split into two components that are cross connected in the layout. In a geometric sense, the centroid of both composite devices lies at center of the structure. Because any gradient can be decomposed into horizontal and vertical components, this layout overcomes the effect of linear process gradients in any direction.

Figure 6.24 also shows two layers of metal used to cross connect the devices. One layer of metal is drawn with solid lines. The other is drawn with dashed lines. The two layers connect at intersections only where dots are drawn. The interconnect drawn here is shift insensitive and balanced in the sense that any signal line that crosses a node on one side of the differential pair also crosses the corresponding node on the other side. This balance helps to keep undesired signals in common-mode form so they can be rejected by the differential pair. Finally, the only line that crosses the metal connected to the two input gates is the metal line to the sources of the differential pair. This characteristic is important because such crossings create a small parasitic capacitance between the two layers that cross, and can allow undesired signals to couple to the op-amp inputs. Since op amps are designed to have high gain, op-amp inputs are
the most sensitive nodes in analog integrated circuits. Therefore, if any signal line is allowed to cross one gate, it should also cross the other to balance the parasitic capacitances. Since the parasitics may not be perfectly matched in practice, however, avoiding crossings is better than balancing them. In Fig. 6.24, the gates are allowed to cross the source of the differential pair because the transistors themselves already provide a large capacitance between each gate and the source in the form of the gate-source capacitance of each transistor.

A disadvantage of common-centroid layouts is also apparent in Fig. 6.24. That is, the need to cross-connect the devices increases the separation between matched devices and may worsen matching in cases where linear process gradients are not the main limitation. Therefore, the value of a common-centroid layout must be determined on a case-by-case basis.

## 6.4 Two-Stage MOS Operational Amplifiers with Cascodes

The basic two-stage op amp described above is widely used with many variations that optimize certain aspects of the performance. In this section, we consider an important variation on the basic circuit to increase the voltage gain.

The voltage gain that is available from the basic circuit shown in Fig. 6.16 may be inadequate in a given application to achieve the required accuracy in the closed-loop gain. For example, suppose the basic op amp uses transistors with $g_{m} r_{o}=20$ and is connected in the voltage-follower configuration shown in Fig. 6.3c. The op-amp gain is given in (6.56) and is less than $\left(g_{m} r_{o}\right)^{2}$ in practice. For simplicity, assume that the op-amp gain is about $\left(g_{m} r_{o}\right)^{2}$, or 400 in this case. The closed-loop gain is given by (6.12) and is approximately unity because $R_{2}=0$ in the follower configuration. The error in this approximation is one part in the op-amp gain or at least 0.25 percent. In precision applications, this error may be too large to meet the given specifications, requiring an increase in the op-amp gain.

One approach to increasing the op-amp gain is to add another common-source gain stage to the op amp so that the overall gain is approximately $\left(g_{m} r_{o}\right)^{3}$ instead of $\left(g_{m} r_{o}\right)^{2}$. An important problem with this approach, however, stems from the fact that op amps are intended to be used in negative-feedback configurations. In practice, op-amp frequency response is not constant. If the op amp introduces an additional phase shift of $180^{\circ}$ at some frequency, the negative feedback that was intended becomes positive feedback at that frequency, and the op amp may be unstable. The topics of frequency response and stability are covered in detail in Chapters 7 and 9 , respectively. The key point here is that if an op amp is unstable in a given feedback configuration, it does not act as an amplifier but as a latch or oscillator. To avoid this problem, op amps are usually designed with no more than two gain stages because each stage contains a node for which the impedance to ground is high and as a result contributes a significant pole to the op-amp transfer function. Since the phase shift from one pole approaches $-90^{\circ}$ asymptotically, an op amp with no more than two poles cannot provide the $180^{\circ}$ phase shift that is required to convert negative feedback into positive feedback.

To increase the voltage gain without adding another common-source gain stage, commongate transistors can be added. Together with a common-source transistor, a common-gate transistor forms a cascode that increases the output resistance and gain of the stage while contributing a less significant pole to the amplifier transfer function than would be contributed by another common-source stage. Figure 6.25 illustrates the use of cascodes to increase the voltage gain of a two-stage amplifier. Here, a series connection of two transistors, one in the common-source connection and one in the common-gate connection, replace each common-source transistor in the first stage. Therefore, $M_{1}$ and $M_{1 A}$ in Fig. 6.25 replace $M_{1}$ in Fig. 6.16. Similarly, $M_{2}$ and $M_{2 A}$ in Fig. 6.25 replace $M_{2}$ in Fig. 6.16. Transistor $M_{9}$ and current source $I_{C}$ have also been added to bias the gates of $M_{1 A}$ and $M_{2 A}$. In practice, the
image_name:Figure 6.25
description:The circuit is a two-stage amplifier with cascoded first stage to increase output impedance. M1 and M2 are NMOS transistors in the differential pair, with M1A and M2A as cascode devices. M9 is a PMOS transistor used for biasing.

Figure 6.25 Two-stage amplifier with cascoded first stage.
$W / L$ of $M_{9}$ is chosen so that $M_{1}$ and $M_{2}$ are operated barely in the active region. The effect of these replacements is to increase the unloaded output impedance of the differential pair by a factor that is approximately equal to $g_{m} r_{o}$ of the cascode device.

If the current mirror $M_{3}-M_{4}$ were not also cascoded, however, the output resistance of the first stage including the current-mirror load would be limited by the mirror. To overcome this limitation, a cascode current mirror shown in Fig. 4.9 is used instead. As a result, the stage gain and output resistance including the load are increased by approximately a factor $g_{m} r_{o}$. In this circuit, $M_{10}$ and $M_{11}$ are included to level shift the output of the first stage down by $V_{G S 10}$ so that the second stage input is driven by a signal whose dc level is $V_{G S 3}$ above $-V_{S S}$. If the aspect ratios are chosen to satisfy (6.66), and if each common-gate transistor is identical to its common-source counterpart, the systematic offset voltage with this level shift is given by (6.68), where the op-amp gain here is on the order of $\left(g_{m} r_{o}\right)^{3}$ instead of $\left(g_{m} r_{o}\right)^{2}$ in Fig. 6.16. One disadvantage of this circuit is a substantial reduction in the common-mode input range. (See Problem 6.16.) To overcome this problem, cascoding could be added instead to the second stage. In that case, however, the output swing of the op amp would be degraded by the cascodes.

## 6.5 MOS Telescopic-Cascode Operational Amplifiers

As mentioned in the previous section, cascode configurations may be used to increase the voltage gain of CMOS transistor amplifier stages. In many applications, the stage gain can be increased enough so that a single common-source-common-gate stage can provide enough voltage gain to meet the accuracy requirements. The first stage of Fig. 6.25 is sometimes used by itself as an op amp and provides a gain comparable to the gain of the two-stage op-amp in Fig. 6.16. This structure has been called a telescopic-cascode op amp ${ }^{11}$ because the cascodes are connected between the power supplies in series with the transistors in the differential pair,
resulting in a structure in which the transistors in each branch are connected along a straight line like the lenses of a refracting telescope. The main potential advantage of telescopic cascode op amps is that they can be designed so that the signal variations are entirely handled by the fastest-polarity transistors in a given process. Such designs use fully differential configurations and are considered in Chapter 12.

In addition to the poor common-mode input range calculated in Problem 6.16, another disadvantage of the telescopic-cascode configuration is that the output swing is small. For example, ignore $M_{6}, M_{7}, M_{10}, M_{11}$, and $C_{C}$ in Fig. 6.25 and define the dc op-amp output voltage as the voltage $V_{O 1}$ from the drains of $M_{2 A}$ and $M_{4 A}$ to ground. For simplicity, assume that all transistors are enhancement mode with identical overdrive magnitudes. To calculate the output swing, first consider the cascode current mirror by itself. If $V_{S S}=0$, the minimum output voltage for which $M_{4}$ and $M_{4 A}$ operate in the active region would be given by (4.59). With nonzero $V_{S S}$, this condition becomes

$$
\begin{equation*}
V_{O 1(\min )}=-V_{S S}+V_{t n}+2 V_{o v} \tag{6.93}
\end{equation*}
$$

The presence of a threshold term in this equation is an important limitation because it causes a substantial reduction in the allowed output swing. Fortunately, this limitation can be overcome by using one of the high-swing cascode current mirrors shown in Figs. 4.11 and 4.12, which would eliminate the threshold term from (6.93) and give

$$
\begin{equation*}
V_{O 1(\min )}=-V_{S S}+2 V_{o v} \tag{6.94}
\end{equation*}
$$

With this change, we can see that to achieve a gain comparable to $\left(g_{m} r_{o}\right)^{2}$ in one stage, the swing is limited at best to two overdrives away from the supply. In contrast, the basic twostage op amp in Fig. 6.16 gives about the same gain but allows the output to swing within one overdrive of each supply, as shown by (6.61).

To find the maximum output voltage swing of the telescopic-cascode op amp, consider the cascoded differential pair shown in Fig. 6.25. Assume that the common-mode input from the gates of $M_{1}$ and $M_{2}$ to ground is $V_{I C}$. The voltage from the source of $M_{1}$ and $M_{2}$ to ground is

$$
\begin{equation*}
V_{S}=V_{I C}+\left|V_{t p}\right|+\left|V_{o v}\right| \tag{6.95}
\end{equation*}
$$

To operate $M_{5}$ in the active region, its source-drain voltage should be at least $\left|V_{o v}\right|$. Therefore,

$$
\begin{equation*}
V_{D D}-V_{S} \geq\left|V_{o v}\right| \tag{6.96}
\end{equation*}
$$

Substituting (6.95) into (6.96) and rearranging gives

$$
\begin{equation*}
V_{I C} \leq V_{D D}-\left|V_{t p}\right|-2\left|V_{o v}\right| \tag{6.97}
\end{equation*}
$$

If we assume that $M_{9}$ and $I_{C}$ are chosen to operate $M_{1}$ and $M_{2}$ at the edge of the active region, the maximum output voltage for which $M_{2}$ and $M_{2 A}$ operate in the active region is

$$
\begin{equation*}
V_{O 1(\max )}=V_{S}-2\left|V_{o v}\right| \tag{6.98}
\end{equation*}
$$

Substituting (6.95) into (6.98) gives

$$
\begin{equation*}
V_{O 1(\max )}=V_{I C}+\left|V_{t p}\right|-\left|V_{o v}\right| \tag{6.99}
\end{equation*}
$$

This equation shows another limitation of the telescopic-cascode op amp from the standpoint of output swing; that is, the maximum output voltage depends on the common-mode input. However, this limitation as well as the limitation on the common-mode input range calculated in Problem 6.16 can be overcome in switched-capacitor circuits. Such circuits allow the op-amp common-mode input voltage to be set to a level that is independent of all other common-mode voltages on the same integrated circuit. This property holds because the only coupling of signals
to the op-amp inputs is through capacitors, which conduct zero dc current even with a nonzero dc voltage drop. Assuming that the op-amp inputs are biased to the maximum common-mode input voltage for which $M_{5}$ operates in the active region, the maximum output voltage can be found by substituting the maximum $V_{I C}$ from (6.97) into (6.99), which gives

$$
\begin{equation*}
V_{O 1(\max )}=V_{D D}-3\left|V_{o v}\right| \tag{6.100}
\end{equation*}
$$

This equation shows that the maximum output voltage of a telescopic op amp that consists of the first stage of Fig. 6.25 with optimum common-mode input biasing is three overdrives less than the positive supply. This result stems from the observation that three transistors ( $M_{5}$, $M_{2}$, and $M_{2 A}$ ) are connected between $V_{D D}$ and the output. In contrast, (6.94) shows that the minimum output swing is limited by two overdrives.

To determine the minimum required supply voltage difference, we will subtract (6.94) from (6.100), which gives

$$
\begin{equation*}
V_{O 1(\max )}-V_{O 1(\min )}=V_{D D}-\left(-V_{S S}\right)-5\left|V_{o v}\right| \tag{6.101}
\end{equation*}
$$

assuming that the magnitudes of all the overdrives are all equal. Rearranging this equation gives

$$
\begin{equation*}
V_{D D}-\left(-V_{S S}\right)=V_{O 1(\max )}-V_{O 1(\min )}+5\left|V_{o v}\right| \tag{6.102}
\end{equation*}
$$

This equation shows that the minimum difference between the supply voltages in a telescopic cascode op amp must be at least equal to the peak-to-peak output signal swing plus five overdrive voltages to operate all transistors in the active region. For example, with a peak-topeak output swing of 1 V and $\left|V_{o v}\right|=100 \mathrm{mV}$ for each transistor, the minimum difference between the supply voltages is 1.5 V .

In practice, this calculation has two main limitations. First, if transistors are deliberately biased at the edge of the active region, a small change in the process, supply, or temperature may cause one or more transistors to operate in the triode region, reducing the output resistance and gain of the op amp. To avoid this problem, transistors in practical op amps are usually biased so that the magnitude of the drain-source voltage of each transistor is more than the corresponding overdrive by a margin of typically at least one hundred millivolts. The margin allowed for each transistor directly adds to the minimum required supply voltage difference. Second, this calculation determines the supply requirements only for transistors between the output node and each supply, and other branches may require a larger supply difference than given in (6.102). For example, consider the path from one supply to the other through $M_{5}$, $M_{1}, M_{1 A}, M_{3 A}$, and $M_{3}$ in Fig. 6.25. Ignore the body effect for simplicity. Since $M_{3 A}$ and $M_{3}$ are diode connected, the drain-source voltage of each is $V_{t}+V_{o v}$. Furthermore, if the $W / L$ of $M_{3 A}$ is reduced by a factor of four to build the high-swing cascode current mirror shown in Fig. 4.11, the voltage drop from the drain of $M_{3 A}$ to the source of $M_{3}$ is $2 V_{t}+3 V_{o v}$. If the other three transistors in this path are biased so that $\left|V_{D S}\right|=\left|V_{o v}\right|$, the required supply difference for all the transistors in this path to operate in the active region is $2 V_{t}+6\left|V_{o v}\right|$. This requirement exceeds the requirement given in (6.102) if $2 V_{t}+\left|V_{o v}\right|$ is more than the peak-to-peak output swing. However, this result does not pose a fundamental limitation to the minimum required power-supply voltage because low-threshold devices are sometimes available.

The minimum supply voltage difference in (6.102) includes five overdrive terms. In contrast, the corresponding equation for the op amp in Fig. 6.16 would include only two overdrive terms, one for $M_{6}$ and the other for $M_{7}$. The presence of the three extra overdrive terms increases the minimum required supply difference or reduces the allowed overdrives for a given supply difference. The extra three overdrive terms in (6.102) stem from the two cascode devices and the tail current source. The overdrives from the cascodes should be viewed as the
cost of using cascodes; however, the overdrive of the tail current source can be eliminated from the minimum required supply difference using the circuit described in the next section.

## 6.6 MOS Folded-Cascode Operational Amplifiers

Figure 6.26 shows two cascode circuits where $V_{D D}=0$ for simplicity. In Fig. $6.26 a$, both $M_{1}$ and $M_{1 A}$ are $p$-channel devices. In Fig. $6.26 b, M_{1}$ is still a $p$-channel device but $M_{1 A}$ is now an $n$-channel device. In both cases, however, $M_{1}$ is connected in a common-source configuration, and $M_{1 A}$ is connected in a common-gate configuration. Small-signal variations in the drain current of $M_{1}$ are conducted primarily through $M_{1 A}$ in both cases because $I_{\text {BIAS }}$ is a constant current source. Therefore, both circuits are examples of cascodes. The cascode in Fig. 6.26b is said to be folded in the sense that it reverses the direction of the signal flow back toward ground. This reversal has two main advantages when used with a differential pair. First, it increases the output swing. Second, it increases the common-mode input range.

Figure 6.27 shows a simplified schematic of a circuit that applies the folded-cascode structure to both sides of a differential pair. As in Fig. 6.26b, $M_{1}$ and $M_{1 A}$ form one cascode structure in Fig. 6.27. Also, $M_{2}$ and $M_{2 A}$ form another. The current mirror converts the differential signal into a single-ended output by sending variations in the drain current of $M_{1 A}$ to the output. The resulting op amp is called a folded-cascode op amp. ${ }^{7,12}$ A complete schematic is shown in Fig. 6.28. Bias is realized by making the currents in current sources $M_{11}$ and $M_{12}$ larger than $\left|I_{D 5}\right| / 2$. Thus

$$
\begin{equation*}
I_{D 1 A}=I_{D 2 A}=I_{D 11}-\frac{\left|I_{D 5}\right|}{2}=I_{D 12}-\frac{\left|I_{D 5}\right|}{2}=I_{\mathrm{BIAS}}-\frac{I_{\mathrm{TAIL}}}{2} \tag{6.103}
\end{equation*}
$$

Compared to the other op-amp configurations we have considered, the folded-cascode configuration improves the common-mode input range. The upper end of the range is the same as in the basic two-stage op amp and the telescopic cascode op amp. On the other hand, the lower end of the range can be reduced significantly compared to both of the other configurations if $V_{\text {BIAS2 }}$ is adjusted so that $M_{11}$ and $M_{12}$ operate at the edge of the active region. Under this condition, the bias voltage from the drain of $M_{1}$ to $-V_{S S}$ is $V_{o v 11}$, which can be much less than in the other configurations. See (6.75), (6.77), and Problem 6.18.
image_name:Figure 6.26 (a)
description:
[
name: M1, type: PMOS, ports: {S: GND, D: d1s1A, G: -(VI+vi)}
name: M1A, type: PMOS, ports: {S: d1s1A, D: -(VO+vo), G: VBIAS}
name: R, type: Resistor, value: R, ports: {N1: -(VO+vo), N2: -Vo}
]
extrainfo:This is a standard cascode configuration circuit with PMOS transistors M1 and M1A. The circuit amplifies the input voltage VI+vi and outputs at VO+vo. The resistor R is connected between the output and the negative voltage node -Vo. The bias voltage VBIAS is applied to the gate of M1A. The current source IBIAS provides biasing current from node d1s1A to -VSS.
image_name:Figure 6.26 (b)
description:
[
name: M1, type: PMOS, ports: {S: GND, D: d1s1A, G: -(Vi+vi)}
name: R, type: Resistor, value: R, ports: {N1: GND, N2: -(Vo+vo)}
name: VBias, type: VoltageSource, value: VBias, ports: {Np: Vb, Nn: GND}
name: M1A, type: PMOS, ports: {S: d1s1A, D: -(Vo+vo), G: Vb}
name: IBias, type: CurrentSource, value: IBias, ports: {Np: d1s1A, Nn: -VSS}
]
extrainfo:The circuit diagram is a folded-cascode configuration. It uses a PMOS transistor (M1) for the input stage and another PMOS (M1A) for the cascode stage. The output is taken across a resistor R connected to the drain of M1. A bias voltage VBias is applied to the gate of M1A. The circuit is powered by a voltage source VI+vi and a bias current source IBias.

Figure 6.26 (a) Standard cascode configuration. (b) Folded-cascode configuration.
image_name:Figure 6.27
description:The circuit is a folded-cascode op-amp configuration. It features a PMOS input stage with M1 and M2, and NMOS cascode transistors M1A and M2A. The op-amp is powered by a current source I_TAIL and bias current sources I_BIAS. The output is taken across a capacitor CL connected to the output node vo.

Figure 6.27 Simplified schematic of a folded-cascode op amp.
image_name:Figure 6.28
description:The circuit is a folded-cascode op-amp configuration with a PMOS input stage (M1, M2) and NMOS cascode transistors (M1A, M2A). It includes a PMOS current mirror (M3, M4) and biasing transistors (M5, M11, M12). The output is taken across a capacitor CL connected to the output node vo.

Figure 6.28 More detailed schematic of a folded-cascode op amp.

To calculate the output swing, first consider the $p$-type cascode current mirror by itself. Since $M_{3}$ and $M_{3 A}$ are diode connected, the voltage from $V_{D D}$ to the gate of $M_{4 A}$ is $2\left|V_{t p}\right|+$ $2\left|V_{o v}\right|$. Therefore, the source-drain voltage of $M_{4}$ is $\left|V_{t p}\right|+\left|V_{o v}\right|$, and the maximum output for which both $M_{4}$ and $M_{4 A}$ operate in the active region is

$$
\begin{equation*}
V_{\text {OUT }(\max )}=V_{D D}-\left|V_{t p}\right|-2\left|V_{o v}\right| \tag{6.104}
\end{equation*}
$$

This equation is analogous to (6.93) where an $n$-type cascode current mirror limits the minimum output swing of the telescopic op amp. The threshold term in this equation can be eliminated by using a $p$-type version of one of the high-swing cascode current mirrors shown in Figs. 4.11 and 4.12. The result is

$$
\begin{equation*}
V_{\text {OUT }(\max )}=V_{D D}-2\left|V_{o v}\right| \tag{6.105}
\end{equation*}
$$

To find the minimum output voltage, assume that $V_{\text {BIAS2 }}$ is adjusted so that $M_{12}$ operates at the edge of the active region. Then the drain-source voltage of $M_{12}$ is $V_{o v}$ and the minimum output voltage for which both $M_{2 A}$ and $M_{12}$ operate in the active region is

$$
\begin{equation*}
V_{\mathrm{OUT}(\min )}=-V_{S S}+2 V_{o v} \tag{6.106}
\end{equation*}
$$

Therefore, a folded-cascode op amp can provide nearly constant voltage gain while its output swings within two overdrives of each supply. In contrast, the output of a telescopic-cascode op amp can swing within two overdrives of one supply and three overdrives of the other while providing nearly constant gain.

The small-signal voltage gain of this circuit at low frequencies is

$$
\begin{equation*}
A_{v}=G_{m} R_{o} \tag{6.107}
\end{equation*}
$$

where $G_{m}$ is the transconductance and $R_{o}$ is the output resistance. When all the transistors operate in the active region, the range of typical gain magnitudes is from several hundred to several thousand. Because of the action of the current mirror $M_{3}-M_{4}$, variation in the drain current of $M_{1}$ and $M_{2}$ contribute constructively to the transconductance. Therefore,

$$
\begin{equation*}
G_{m}=g_{m 1}=g_{m 2} \tag{6.108}
\end{equation*}
$$

To find $R_{o}$, both inputs are connected to ac ground. Although the input voltages do not move in this case, the sources of $M_{1}-M_{2}$ do not operate at ac ground. However, connecting this node to small-signal ground as shown in Fig. $6.29 a$ causes little change in $R_{o}$ because of the action of the current mirror $M_{3}-M_{4}$, as explained next.

Let $i_{d 1}$ and $i_{d 2}$ represent the small-signal drain currents of $M_{1}$ and $M_{2}$ respectively. Also, let $\Delta i_{d 1}$ and $\Delta i_{d 2}$ represent the corresponding changes in $i_{d 1}$ and $i_{d 2}$ caused by connecting the sources of $M_{1}-M_{2}$ to a small-signal ground as shown in Fig. 6.29a. If $r_{o} \rightarrow \infty, \Delta i_{d 1}=\Delta i_{d 2}$ because this connection introduces equal changes in the gate-source voltages of $M_{1}$ and $M_{2}$. Then $\Delta i_{d 1}$ flows in the source of $M_{1 A}$, where it is mirrored to the output with a gain of unity if $r_{o} \rightarrow \infty$ in $M_{3}-M_{4}$. Therefore, KCL at the output shows that $\Delta i_{d 1}$ and $\Delta i_{d 2}$ cancel, causing no change to the output current $i_{x}$ or the output resistance $R_{o}$. As a result, $R_{o}$ can be found, assuming that the sources of $M_{1}-M_{2}$ operate at ac ground. In practice, $r_{o}$ in all the transistors is finite, and $R_{o}$ is altered slightly by connecting this point to ac ground for two reasons. First, $\Delta i_{d 1}$ and $\Delta i_{d 2}$ are not exactly equal with finite $r_{o}$ because $v_{d s 1}$ and $v_{d s 2}$ are not exactly equal. Differences between $v_{d s 1}$ and $v_{d s 2}$ stem from finite $r_{o}$ in $M_{1 A}$ and $M_{2 A}$ because $M_{3}$ and $M_{3 A}$ are diode connected but their counterparts $M_{4}$ and $M_{4 A}$ are not diode connected. Second, the small-signal current gain of the current mirror is not exactly unity with finite $r_{o}$ because $v_{d s 3}$ and $v_{d s 4}$ are not exactly equal. However, the change in the output resistance introduced by these considerations is usually negligible. (These effects are related to the explanation of
image_name:(a)
description:The circuit is a differential pair with a current mirror load. M3 and M3A are diode connected, providing a small Thevenin resistance to the gates of M4 and M4A. The sources of M1 and M2 are connected to AC ground, ensuring constant drain current. The circuit is used to calculate the output resistance with a test voltage source applied to the output.
image_name:(b)
description:
[
name: M2, type: PMOS, ports: {S: GND, D: d2d12, G: GND}
name: M4, type: PMOS, ports: {S: GND, D: d4s4A, G: GND}
name: M4A, type: PMOS, ports: {S: d4s4A, D: Vx, G: GND}
name: M2A, type: NMOS, ports: {S: d2d12, D: Vx, G: GND}
name: M12, type: NMOS, ports: {S: GND, D: d2d12, G: GND}
]
extrainfo:The circuit is a simplified test setup for calculating the output resistance. PMOS transistors M4 and M4A are connected in a cascode configuration, with M4A acting as a diode-connected load. NMOS transistors M2A and M12 are used as current sinks. The test voltage source Vx is applied to the output node to measure the output resistance.
Figure 6.29 (a) Test voltage source applied to the output to calculate the output resistance. (b) Simplified circuit.
how a current-mirror load increases the common-mode rejection ratio of a differential pair presented in Section 4.3.5.3.)

With the sources of $M_{1}-M_{2}$ connected to ac ground, the drain current of $M_{1}$ is constant. Furthermore, the Thevenin equivalent resistances presented to the gates of $M_{4}$ and $M_{4 A}$ are small because $M_{3}$ and $M_{3 A}$ are diode connected. So little error is introduced by assuming that the gates of $M_{4}$ and $M_{4 A}$ are connected to small-signal ground. Therefore, the calculation of $R_{o}$ can be carried out using the circuit of Fig. 6.29b. By inspection,

$$
\begin{equation*}
R_{O}=\left(\left.R_{\text {out }}\right|_{M 2 A}\right) \|\left(\left.R_{\text {out }}\right|_{M 4 A}\right) \tag{6.109}
\end{equation*}
$$

The output resistance of transistor current sources with nonzero source resistance was considered in Chapter 4. The result is the same as for a common-source amplifier with source degeneration. The incremental resistance in the source of $M_{2 A}$ is the $r_{o}$ of $M_{2}$ in parallel with the $r_{o}$ of $M_{12}$ while the incremental resistance in the source of $M_{4 A}$ is the $r_{o}$ of $M_{4}$. From (3.107),

$$
\begin{align*}
\left.R_{\text {out }}\right|_{M 2 A} & =\left(r_{o 2} \| r_{o 12}\right)+r_{o 2 A}\left[1+\left(g_{m 2 A}+g_{m b 2 A}\right)\left(r_{o 2} \| r_{o 12}\right)\right]  \tag{6.110}\\
& \simeq\left[g_{m 2 A}\left(r_{o 2} \| r_{o 12}\right)\right] r_{o 2 A}
\end{align*}
$$

and

$$
\begin{align*}
\left.R_{\mathrm{out}}\right|_{M 4 A} & =r_{o 4}+r_{o 4 A}\left[1+\left(g_{m 4 A}+g_{m b 4 A}\right)\left(r_{o 4}\right)\right]  \tag{6.111}\\
& \simeq\left(g_{m 4 A} r_{o 4}\right) r_{o 4 A}
\end{align*}
$$

An important advantage of this circuit is that the load capacitance $C_{L}$ performs the compensation function (see Chapter 9). Thus no additional capacitance (such as $C_{C}$ in previous circuits) need be added to keep the amplifier from oscillating when connected in a feedback
loop. Furthermore, in the basic two-stage op amp, $C_{C}$ feeds the variation from one power supply forward to the op-amp output at high frequencies, as described in Section 6.3.6. This feedforward does not occur in one-stage op amps such as the folded-cascode and telescopiccascode structures, improving their high-frequency power-supply rejection ratios from the $V_{s s}$ supply.

## 6.7 MOS Active-Cascode Operational Amplifiers

One way to increase the gain of the folded-cascode op amp without cascading additional stages is to add another layer of cascodes. See Problem 6.21. Although this approach gives a gain on the order of $\left(g_{m} r_{o}\right)^{3}$, it reduces the output swing by at least another overdrive in each direction. This reduction becomes increasingly important as the difference between the power-supply voltages is reduced in scaled technologies. To increase the op-amp gain without reducing the output swing, the active-cascode technique described in Chapter 3 can be used. ${ }^{13}$

Figure 6.30a shows the schematic of a folded-cascode op amp with active cascodes. The gates of each of the four cascode transistors $M_{1 A}, M_{2 A}, M_{3 A}$, and $M_{4 A}$ are no longer connected to a constant bias source but instead to the output of an amplifier. These auxiliary amplifiers are themselves connected in negative feedback loops to increase the resistance looking into the drain of each cascode transistor. As shown by (3.133), the active-cascode configuration increases the output resistance by increasing the effective transconductance of the cascode transistor by $(a+1)$, where $a$ is the voltage gain of the auxiliary amplifier. Let the gains of the auxiliary amplifiers driving $M_{3 A}$ and $M_{4 A}$ be $A_{1}$. Applying (3.133) to (6.111) to find the
image_name:(a)
description:The circuit is a folded-cascode operational amplifier with active-cascode gain-enhancement auxiliary amplifiers. It uses two op-amps (A1 and A2) for gain enhancement, increasing the output resistance and improving performance. The circuit has bias voltages labeled as VBIAS1, VBIAS2, VBIAS3, and VBIAS4. The output is taken from the drain of M4A and is connected to a load capacitor CL. The power supply voltages are VDD and VSS.

Figure 6.30 (a) Folded-cascode op amp with active-cascode gain-enhancement auxiliary amplifiers.
output resistance looking into the drain of $M_{4 A}$ gives

$$
\begin{align*}
\left.R_{\text {out }}\right|_{M 4 A} & =r_{o 4}+r_{o 4 A}\left\{1+\left[g_{m 4 A}\left(A_{1}+1\right)+g_{m b 4 A}\right]\left(r_{o 4}\right)\right\}  \tag{6.112}\\
& \simeq\left(A_{1}+1\right)\left(g_{m 4 A} r_{o 4}\right) r_{o 4 A}
\end{align*}
$$

Let the gains of the auxiliary amplifiers driving $M_{1 A}$ and $M_{2 A}$ be $A_{2}$. Applying (3.133) to (6.110) to find the output resistance looking into the drain of $M_{2 A}$ gives

$$
\begin{align*}
\left.R_{\text {out }}\right|_{M 2 A} & =\left(r_{o 2} \| r_{o 12}\right)+r_{o 2 A}\left\{1+\left[g_{m 2 A}\left(A_{2}+1\right)+g_{m b 2 A}\right]\left(r_{o 2} \| r_{o 12}\right)\right\}  \tag{6.113}\\
& \simeq\left(A_{2}+1\right)\left[g_{m 2 A}\left(r_{o 2} \| r_{o 12}\right)\right] r_{o 2 A}
\end{align*}
$$

To find the overall op-amp gain, (6.112) and (6.113) can be substituted into (6.109) and the result in (6.107). This analysis shows that the gain enhancement in the folded-cascode op amp does not rely on the use of auxiliary amplifiers driving the gates of $M_{1 A}$ and $M_{3 A}$. However, these auxiliary amplifiers are included in Fig. 6.30a because they reduce the systematic offset of the folded-cascode op amp. Also, using identical auxiliary amplifiers to drive the gates of both $M_{1 A}$ and $M_{2 A}$ balances the two signal paths until the differential signal is converted into single-ended form by the current mirror.

In Fig. 6.30a, the auxiliary amplifiers with gain $A_{1}$ drive the gates of $M_{3 A}$ and $M_{4 A}$ so that the voltages from the drains of $M_{3}$ and $M_{4}$ to ground are approximately equal to $V_{\text {BIAS2 }}$. For simplicity, assume that the overdrive voltages for all $p$ - and $n$-channel transistors operating in the active region are $V_{\text {ovp }}$ and $V_{\text {ovn }}$, respectively. Also assume that all $n$-channel transistors have positive thresholds and all $p$-channel transistors have negative thresholds. To maximize the positive output swing of the folded-cascode amplifier, the voltage drop from $V_{D D}$ to $V_{\text {BIAS2 }}$ is chosen to be about $\left|V_{\text {ovp }}\right|$. Therefore, the $A_{1}$ amplifiers must operate with a high common-mode input voltage. If these amplifiers use a $p$-channel differential input pair, the maximum common-mode input voltage would be no more than $V_{D D}-\left|V_{t p}\right|-2\left|V_{o v p}\right|$. To overcome this limitation, the $A_{1}$ amplifiers use an $n$-channel differential pair $M_{21}$ and $M_{22}$ as shown in Fig. 6.30b. In operation, the dc voltage from $V_{D D}$ to the output of the $A_{1}$ amplifiers is about $\left|V_{t p}\right|+2\left|V_{\text {ovp }}\right|$ so that the source-drain voltages of $M_{3}$ and $M_{4}$ are $\left|V_{o v p}\right|$. Therefore, the gate-drain voltage of $M_{22}$ is approximately $\left|V_{t p}\right|+\left|V_{o v p}\right|$, and $M_{22}$ operates in the active region only if its threshold (with the body effect) is greater than this value.

A similar argument can be made to explain the use of $p$-channel differential pairs in the auxiliary amplifiers with gain $A_{2}$. The schematic is shown in Fig. 6.30c, and the common-mode inputs are close to $V_{S S}$ in this case.

Figure $6.30 d$ shows a circuit that produces the bias voltages needed in Fig. 6.30a-c. The voltage from $V_{D D}$ to $V_{\text {BIAS1 }}$ is $\left|V_{t p}\right|+\left|V_{o v p}\right|$, and the voltage from $V_{\text {BIAS4 }}$ to $V_{S S}$ is $V_{t n}+V_{o v n}$. Transistor $M_{105}$ forces $M_{106}$ to operate in the triode region, and the voltage from $V_{D D}$ to $V_{\text {BIAS2 }}$ is at least $\left|V_{\text {ovp }}\right|$ if

$$
\begin{equation*}
\left(\frac{W}{L}\right)_{106} \leq \frac{1}{3}\left(\frac{W}{L}\right)_{105} \tag{6.114}
\end{equation*}
$$

ignoring body effect as in (4.73). Similarly, the voltage from $V_{\text {BIAS3 }}$ to $V_{S S}$ is at least $V_{\text {ovn }}$ if

$$
\begin{equation*}
\left(\frac{W}{L}\right)_{114} \leq \frac{1}{3}\left(\frac{W}{L}\right)_{113} \tag{6.115}
\end{equation*}
$$

One potential problem with the structure shown in Fig. 6.30a is instability in the feedback loops around the auxiliary amplifiers. To avoid instability, a compensation capacitor can be placed from each auxiliary-amplifier output to a small-signal ground. Since the $A_{1}$ amplifiers are used to improve the performance of a $p$-channel current mirror, where signals are referenced to $V_{D D}$, compensation capacitors for the $A_{1}$ amplifiers $C_{C 1}$ are connected to $V_{D D}$. Similarly,
image_name:Figure 6.30 (b)
description:
[
name: M23, type: PMOS, ports: {S: VDD, D: X1, G: X1}
name: M24, type: PMOS, ports: {S: VDD, D: O, G: X1}
name: M21, type: NMOS, ports: {S: X2, D: X1, G: P}
name: M22, type: NMOS, ports: {S: x2, D: O, G: N}
name: M25, type: NMOS, ports: {S: -VSS, D: X2, G: VBIAS4}
]
extrainfo:The circuit in Figure 6.30 (b) is an auxiliary amplifier with gain A1, designed to improve the performance of a p-channel current mirror. The PMOS transistors (M23 and M24) are used at the top, connected to VDD, while NMOS transistors (M21, M22, and M25) form the lower part connected to VSS. The compensation capacitors for stability are connected to VDD.
image_name:Figure 6.30 (c)
description:
[
name: M31, type: PMOS, ports: {S: x1, D: x2, G: P}
name: M32, type: PMOS, ports: {S: x1, D: d32d34, G: N}
name: M35, type: PMOS, ports: {S: VDD, D: x1, G: VBIAS1}
name: M33, type: NMOS, ports: {S: -Vss, D: x2, G: x2}
name: M34, type: NMOS, ports: {S: -Vss, D: d32d34, G: x2}
]
extrainfo:The circuit is an auxiliary amplifier with gain A2, using PMOS and NMOS transistors to form differential pairs. The PMOS transistors are connected to VDD and the NMOS transistors to VSS. Biasing is provided by VBIAS1.
image_name:Figure 6.30 (d)
description:The circuit in Figure 6.30 (d) is a bias circuit with multiple PMOS and NMOS transistors connected to provide biasing voltages VBIAS1, VBIAS2, VBIAS3, and VBIAS4. The circuit also includes a current source IBIAS connected between VDD and one of the PMOS transistors. The circuit is designed to establish proper operating points for other parts of the system using these bias voltages.

Figure 6.30 (b) Auxiliary amplifier with gain $A_{1}$. (c) Auxiliary amplifier with gain $A_{2}$. (d) Bias circuit.
compensation capacitors for the $A_{2}$ amplifiers $C_{C 2}$ are connected to $V_{S S}$. The need for such capacitors stems from the observation that the capacitance looking into the gates of $M_{1 A}, M_{2 A}$, $M_{3 A}$, and $M_{4 A}$ can be quite small because the gate-source capacitances of these transistors are bootstrapped. This expression means that the source of each of these transistors follows its gate when the corresponding drain current is constant. If the gate-source voltages are exactly constant, zero ac current flows into the gate-source capacitances, and the capacitances looking into the gates of the cascode transistors are independent of their gate-source capacitances. In practice, the gate-source voltages are not exactly constant because of variations in the drain currents caused by variations in the differential input voltage of the folded-cascode op amp, but the bootstrapping effect is significant. As a result, the load capacitances of the auxiliary amplifiers are dominated by parasitics that may vary considerably over variations in processing unless a capacitor is added at the output of each auxiliary amplifier. The issue of stability in feedback amplifiers is considered in detail in Chapter 9.

## 6.8 Bipolar Operational Amplifiers

A basic topology for the input stage of bipolar-transistor op amps is shown in Fig. 6.31a. As in the case of the basic MOS op amp, the input stage consists of a differential pair, a tail current source, and a current-mirror load. The common-mode input range of op amps with this input
stage is the range of dc common-mode input voltages for which all transistors in Fig. 6.31a operate in the forward-active region. Assume that a pure common-mode voltage $V_{I C}$ is applied from the op-amp inputs to ground. Also, assume that $Q_{1}$ is identical to $Q_{2}$, and $Q_{3}$ is identical to $Q_{4}$. Then the collector-emitter voltage of $Q_{5}$ is

$$
\begin{equation*}
V_{C E 5}=V_{I C}-V_{B E 1}-V_{C C} \tag{6.116}
\end{equation*}
$$

This equation shows that increasing $V_{I C}$ increases $V_{C E 5}$. Since $Q_{5}$ is a pnp transistor, it operates in the active region when $V_{C E 5}<V_{C E 5(\text { sat) }}$. Therefore, (6.116) can be rearranged to give the following upper limit for the common-mode input range

$$
\begin{equation*}
V_{I C}<V_{C C}+V_{B E 1}+V_{C E 5(\mathrm{sat})} \tag{6.117}
\end{equation*}
$$

For example, if $V_{B E 1}=-0.7 \mathrm{~V}$ and $V_{C E 5(\mathrm{sat})}=-0.1 \mathrm{~V}, V_{I C}<V_{C C}-0.8 \mathrm{~V}$ is required to operate $Q_{5}$ in the forward-active region.

To find the lower limit for the common-mode range, ignore base currents for simplicity. Then with a pure common-mode input,

$$
\begin{equation*}
V_{C E 4}=V_{C E 3}=V_{B E 3} \tag{6.118}
\end{equation*}
$$

As a result, the collector-emitter voltages of $Q_{1}$ and $Q_{2}$ are

$$
\begin{equation*}
V_{C E 1}=V_{C E 2}=-V_{E E}+V_{B E 3}-\left(V_{I C}-V_{B E 1}\right) \tag{6.119}
\end{equation*}
$$

Because $Q_{1}$ and $Q_{2}$ are pnp transistors, they operate in the forward-active region when $V_{C E 1}<$ $V_{C E 1 \text { (sat) }}$ and $V_{C E 2}<V_{C E 2(\mathrm{sat})}$. Therefore, the lower end of the common-mode range is

$$
\begin{equation*}
V_{I C}>-V_{E E}+V_{B E 3}+V_{B E 1}-V_{C E 1(\mathrm{sat})} \tag{6.120}
\end{equation*}
$$

For example, if $V_{B E 3}=0.7 \mathrm{~V}, V_{B E 1}=-0.7 \mathrm{~V}$, and $V_{C E 5(\mathrm{sat})}=-0.1 \mathrm{~V}, V_{I C}>-V_{E E}+$ 0.1 V is required to operate $Q_{1}$ and $Q_{2}$ in the forward-active region.

This inequality shows that the common-mode input range of the op amp in Fig. 6.31a almost includes $-V_{E E}$. A simple way to see this result is to let $V_{I C}=-V_{E E}$ in Fig. 6.31a. Then the collector-base voltages of $Q_{1}$ and $Q_{2}$ are

$$
\begin{equation*}
V_{C B 1}=V_{C B 2}=V_{B E 3} \tag{6.121}
\end{equation*}
$$

image_name:Figure 6.31 (a)
description:
[
name: Q1, type: PNP, ports: {C: X1, B: Vin-, E: e1e2c5}
name: Q2, type: PNP, ports: {C: c2c4, B: Vin+, E: e1e2c5}
name: Q3, type: NPN, ports: {C: X1, B: X1, E: -VEE}
name: Q4, type: NPN, ports: {C: c2c4, B: X1, E: -VEE}
name: Q5, type: PNP, ports: {C: e1e2c5, B: Bias1, E: Vcc}
]
extrainfo:The circuit is an input stage of a basic bipolar operational amplifier with a differential pair (Q1 and Q2) and current mirrors (Q3, Q4, and Q5). The common-mode input range includes -VEE.

image_name:(b)
description:
[
name: Q1, type: PNP, ports: {C: c1, B: Vin-, E: e1e2c5}
name: Q2, type: PNP, ports: {C: c2, B: Vin+, E: e1e2c5}
name: Q3, type: NPN, ports: {C: X1, B: X1, E: -VEE}
name: Q4, type: NPN, ports: {C: c2c4, B: X1, E: -VEE}
name: Q5, type: PNP, ports: {C: e1e2c5, B: Bias1, E: Vcc}
name: R1, type: Resistor, ports: {N1: c1, N2:-VEE}
name: R2, type: Resistor, ports: {N1: c2, N2:-VEE}
]
extrainfo:The circuit is an input stage of a basic bipolar operational amplifier. It features a differential pair (Q1 and Q2) with resistive loads (R1 and R2) to include -VEE in the input common-mode range. Q5 acts as a current mirror for biasing.

Figure 6.31 (a) Input stage in a basic bipolar operational amplifier. (b) Input stage with resistive loads to include $-V_{E E}$ in the input common-mode range. Assume $R_{1}=R_{2}$.

Since $Q_{3}$ is diode connected and conducts current from its collector to its emitter, $V_{B E 3}$ is big enough to forward bias the base-emitter junction of $Q_{3}$. Therefore, $V_{B E 3}$ is also big enough to forward bias the collector-base junctions of $Q_{1}$ and $Q_{2}$, pushing these transistors into saturation.

To extend the common-mode input range to include $-V_{E E}$ (which is important in singlesupply applications with $V_{E E}=0$ ), the $V_{B E 3}$ term in (6.120) and (6.121) can be reduced by replacing the $Q_{3}-Q_{4}$ current mirror by resistive loads, ${ }^{14}$ as shown in Fig. 6.31b. The voltage drops across the resistors $V_{R 1}$ and $V_{R 2}$ are chosen to be too small to forward bias the collectorbase junctions of $Q_{1}$ and $Q_{2}$ when $V_{I C}=-V_{E E}$. In practice, these drops are usually set to about 200 mV with a pure common-mode input so that the common-mode input range extends a few hundred millivolts below $-V_{E E}$. One example in which this property is useful is in the inverting amplifier configuration shown in Fig. 6.3a when $V_{E E}=0$. Since the configuration is inverting, $V_{S}<0$ causes $V_{o}>0$, and single-supply op amps can have high gain with positive outputs and $V_{C C}>0$. However, if the op amp has zero offset and its gain $a$ is finite, (6.5) shows that $V_{i}<0$ when $V_{o}>0$. As a result, the op-amp common-mode input voltage is negative, requiring that the common-mode input range extend below ground to handle this case.

The main drawback of the circuit in Fig. $6.31 b$ is that its gain is low. ${ }^{15}$ If the matching is perfect and $V_{R 1}=V_{R 2}=0.2 \mathrm{~V}$,

$$
\begin{equation*}
\frac{v_{o d}}{v_{i d}}=g_{m 1} R_{1}=\frac{I_{\mathrm{BIAS}}}{2 V_{T}} R_{1}=\frac{V_{R 1}}{V_{T}}=\frac{0.2}{0.026} \simeq 7.7 \tag{6.122}
\end{equation*}
$$

To increase the gain, the input stage can use the folded-cascode structure shown in Fig. 6.32. Transistors $Q_{3}$ and $Q_{4}$ are connected in a common-base configuration. Combined with the input differential pair, this circuit forms a folded-cascode amplifier. The gain is

$$
\begin{equation*}
\frac{v_{o d}}{v_{i d}}=g_{m 1} \rho_{1} R_{o 1} \tag{6.123}
\end{equation*}
$$

image_name:Figure 6.32 Folded-cascode input stage
description:The circuit is a folded-cascode input stage amplifier with a differential input pair (Q1, Q2) and a folded-cascode configuration using Q3 and Q4. The PMOS transistors Q5, Q6, and Q7 provide current biasing. The resistors R3, R4, R5, R6, and R7 are used for biasing and load purposes. The circuit aims to increase gain by utilizing the folded-cascode structure, which provides high output resistance and increased voltage gain.

Figure 6.32 Folded-cascode input stage.
where $\rho_{1}$ represents the fraction of the small-signal collector current in $Q_{1}$ that flows into the emitter of $Q_{3}$ and $R_{o 1}$ represents the output resistance of this stage. To find $\rho_{1}$, the smallsignal resistance looking into the emitter of $Q_{3}$ is needed. Since $Q_{3}$ operates as a common-base amplifier, this resistance can be found using (3.53) and is approximately equal to $r_{e 3}$, ignoring the last term in (3.53) for simplicity. Then

$$
\begin{equation*}
\rho_{1} \simeq \frac{R_{3}}{R_{3}+r_{e 3}} \tag{6.124}
\end{equation*}
$$

Assume that $\mathrm{Bias}_{1}$ and $\mathrm{Bias}_{\mathrm{CM}}$ are adjusted so that $Q_{6}, Q_{7}, Q_{9}$, and $Q_{10}$ operate in the forward-active region. Then the output resistance of the stage is

$$
\begin{equation*}
R_{o 1}=R_{\text {up } 1} \| R_{\text {down } 1} \tag{6.125}
\end{equation*}
$$

where

$$
\begin{equation*}
R_{\mathrm{up} 1} \simeq r_{o 6}\left(1+g_{m 6} R_{6}\right) \tag{6.126}
\end{equation*}
$$

and

$$
\begin{equation*}
R_{\text {down } 1} \simeq r_{o 3}\left(1+g_{m 3} R_{3}\right) \tag{6.127}
\end{equation*}
$$

assuming $g_{m 6} R_{6} \ll \beta_{p n p}, g_{m 3} R_{3} \ll \beta_{n p n}$, and the resistance looking back into the collector of $Q_{1}$ is much greater than $R_{3}$. Although the folded-cascode circuit in Fig. 6.32 increases the stage gain significantly and allows proper operation for common-mode inputs slightly below $-V_{E E}$, it does not allow operation with common-mode inputs up to $V_{C C}$ as shown by (6.117).

To extend the common-mode input range to $V_{C C}$, an $n p n$ differential pair can be added, as shown in Fig. 6.33. ${ }^{16}$ Assume that the dc voltage drops on $R_{5}-R_{10}$ are 200 mV each. Then
image_name:Figure 6.33 Rail-to-rail folded-cascode input stage
description:This circuit is a rail-to-rail folded-cascode input stage that extends the common-mode input range to VCC by using both NPN and PNP differential pairs. The PNP differential pair operates for common-mode inputs slightly below ground to about 1V below VCC, while the NPN differential pair operates for inputs slightly above VCC to about 1V above ground. The resistors R5 to R10 have a DC voltage drop of 200mV each.

Figure 6.33 Rail-to-rail folded-cascode input stage.
the pnp differential pair operates normally for common-mode inputs slightly below ground to about 1 V below $V_{C C}$. Similarly, the $n p n$ differential pair operates normally for commonmode inputs slightly above $V_{C C}$ to about 1 V above ground. Therefore, if $V_{C C}<2 \mathrm{~V}$, neither differential pair operates normally when $V_{I C}=V_{C C} / 2$ because both $Q_{5}$ and $Q_{8}$ operate in saturation under these conditions. On the other hand, if $V_{C C} \geq 2 \mathrm{~V}$, at least one of the two differential pairs operates normally for any common-mode input voltage from just below $-V_{E E}$ to just above $V_{C C}$. In other words, the stage has a rail-to-rail common-mode input range for $V_{C C} \geq 2 \mathrm{~V}$.

However, an important disadvantage of this input stage is that its small-signal transconductance is not constant. The stage transconductance is the sum of the transconductances from both differential pairs. In the center of the common-mode range, both differential pairs operate normally, and the stage transconductance is high. On the other hand, when the common-mode input voltage is within about 1 V of either supply, the tail current source in one of the differential pairs saturates, reducing that current as well as the transconductances of that differential pair and the input stage. This variation in the stage transconductance causes variation in the open-loop gain and frequency response of the op amp, compromising its performance when it is designed to be stable in a closed-loop configuration. (The topic of stability is covered in Chapter 9.) This disadvantage is overcome in the NE5234 op amp, which is described below. ${ }^{17,18}$ This stand-alone op amp is widely used, and its popularity stems from the fact that it can operate with $V_{E E}=0$ and $V_{C C}$ as low as 2 V , giving constant input transconductance over a common-mode input range slightly beyond the power-supply voltages (or rails) and almost a rail-to-rail output swing.

### 6.8.1 The dc Analysis of the NE5234 Operational Amplifier

Bias Circuit. Figure 6.34 shows the schematic of the NE5234 bias circuit. On the bottom of the circuit, $Q_{49}, Q_{60}$, and $R_{60}$ form a Widlar current mirror. Instead of diode connecting $Q_{49}$, the bases of $Q_{49}$ and $Q_{60}$ are driven by a unity-gain buffer formed by $Q_{50} Q_{53}$ to follow the collector of $Q_{49}$. This buffer is used as a beta helper as in Fig. 4.6 to reduce the base-current error in the $Q_{49}-Q_{60}$ current mirror. In Fig. 4.6, the buffer is simply an npn emitter follower. As a result, $V_{C E 1}=V_{B E 1}+V_{B E 2}=2 V_{B E(\text { on })}$ there. In contrast, if $Q_{1}$ were diode connected, $V_{C E 1}$ would equal $V_{B E(\text { on })}$. Increasing $V_{C E 1}$ increases the minimum value of $V_{C C}$ needed to operate the transistors that implement $I_{\mathrm{IN}}$ in the forward-active region. To reduce the required $V_{C C}$, the corresponding buffer in Fig. 6.34 is a complementary emitter follower, which means that it consists of a pnp emitter follower $\left(Q_{50}-Q_{51}\right)$ and an $n p n$ follower $\left(Q_{52}-Q_{53}\right)$. If $V_{B E 51}=-V_{B E 52}, V_{C E 49}=V_{B E 49}=V_{B E(\mathrm{on})}$, which is reduced by about 0.7 V in practice compared to a conventional beta helper through the use of the complementary follower. Similarly, $Q_{54-} Q_{57}$ in Fig. 6.34 act as a complementary follower to drive the bases of $Q_{47}$ and $Q_{58}$. Also, $Q_{48}$ and $Q_{59}$ serve as common-base stages or cascodes, reducing the dependence of the currents in $Q_{47}$ and $Q_{60}$ on $V_{C C}$.

To concentrate on the core of the bias circuit, Fig. 6.35 shows a simplified bias circuit in which the beta helpers, cascodes, and associated elements are removed. This simplification shows that the core circuit is a self-biased current source using the thermal voltage, as in Fig. 4.41. In that circuit, corresponding transistors are matched except that the emitter area of $Q_{2}$ is twice that of $Q_{1}$. Similar conditions hold in Figs. 6.34 and 6.35, where the emitter area of $Q_{60}$ is twice that of $Q_{49}$. As a result, the collector currents of the transistors in Fig. 6.35 can be found assuming $\beta_{F} \rightarrow \infty$ and $V_{A} \rightarrow \infty$ using (4.237)

$$
\begin{equation*}
\left|I_{C 47}\right|=I_{C 49}=\left|I_{C 58}\right|=I_{C 60}=\frac{V_{T}}{R_{60}} \ln 2=\frac{0.026 \mathrm{~V}}{3 \mathrm{k} \Omega} \ln 2=6 \mu \mathrm{~A} \tag{6.128}
\end{equation*}
$$

image_name:Figure 6.34 Schematic of the NE5234 bias circuit
description::The circuit is a bias circuit for the NE5234. It uses a series of NPN transistors and resistors to establish bias currents. The transistors are arranged in a way to provide proportional to absolute temperature (PTAT) currents. Capacitors C49 and C58 are used for stability.

Figure 6.34 Schematic of the NE5234 bias circuit.
image_name:Figure 6.34
description:The circuit is a bias circuit for the NE5234, using NPN transistors and resistors to establish PTAT currents. It produces DC voltages at nodes Bias1 and Bias5 for scaled copies of 6 µA currents.

Figure 6.35 Simplified schematic of the NE5234 bias circuit.

If $R_{60}$ is constant, these currents are proportional to absolute temperature (PTAT). Although $\beta_{F}$ and $V_{A}$ are finite in practice, this equation also gives the corresponding currents in Fig. 6.34 because that circuit uses the beta helpers and cascodes mentioned above. The bias circuit produces dc voltages at two nodes, Bias ${ }_{1}$ and Bias5, that are used to establish scaled copies of the $6 \mu \mathrm{~A}$ current in $p n p$ and $n p n$ transistors in the op amp, respectively. Since these
scaled currents are also PTAT, the transconductances of transistors conducting these currents are independent of temperature.

Resistor $R_{57}$ in Fig. 6.34 prevents the transistors in the bias circuit from conducting zero current when the power supply is applied. ${ }^{18}$ Without $R_{57}$, the transistors could conduct zero current because the voltage from node Bias 1 to ground could be close to $V_{C C}$. However, with $R_{57}, Q_{55}$ pulls Bias 1 low enough to start the flow of nonzero current. In steady state, nonzero current in $R_{57}$ increases the collector current in $Q_{56}$ but has little overall effect on the operation of the bias circuit.

Input Stage. Figure 6.36 shows a simplified schematic of the NE5234 input stage. This circuit uses a folded-cascode structure with complementary input pairs to give rail-to-rail commonmode input range as in Fig. 6.33; however, the input-stage transconductance in Fig. 6.36 does not depend on the common-mode input voltage.

Node Bias 1 comes from the bias circuit in Fig. 6.34, and $Q_{58}$ and $R_{58}$ there plus $Q_{11}$ and $R_{11}$ in Fig. 6.36 form a current mirror with degeneration. From (4.36) and (6.128),

$$
\begin{equation*}
\left|I_{C 11}\right|=\frac{R_{58}}{R_{11}}\left|I_{C 58}\right|=\left(\frac{33 \mathrm{k} \Omega}{33 \mathrm{k} \Omega}\right) 6 \mu \mathrm{~A}=6 \mu \mathrm{~A} \tag{6.129}
\end{equation*}
$$

Similarly, $\left|I_{C 12}\right|=3 \mu \mathrm{~A}$, and $\left|I_{C 13}\right|=\left|I_{C 14}\right|=6 \mu \mathrm{~A}$. Ignoring base currents for simplicity, the $3 \mu \mathrm{~A}$ from $Q_{12}$ flows in $Q_{8}$ and $R_{8}$, setting the voltage from the base of $Q_{5}$ to ground to

$$
\begin{equation*}
V_{B 5}=\left|I_{C 12}\right| R_{8}+V_{B E 8(\mathrm{on})} \simeq 3 \mu \mathrm{~A}(33 \mathrm{k} \Omega)+0.7 \mathrm{~V}=0.8 \mathrm{~V} \tag{6.130}
\end{equation*}
$$

Assume that the op-amp inputs are driven by a pure common-mode voltage $V_{I C}$. Transistors $Q_{3}$ and $Q_{4}$ together can be viewed as forming one half of a differential pair with $Q_{5}$ forming the other half of this pair. This differential pair is unbalanced because $Q_{3}$ and $Q_{4}$ together have a larger emitter area (and saturation current) than $Q_{5}$ by itself, causing a nonzero offset voltage. Ignore this offset for simplicity. Then if $V_{I C} \ll 0.8 \mathrm{~V}$, the $6 \mu \mathrm{~A}$ current from $Q_{11}$ flows in the pnp input pair $Q_{3}-Q_{4}$, and $Q_{5}-Q_{7}$ plus $Q_{1-} Q_{2}$ are off. On the other hand, if $V_{I C} \gg 0.8 \mathrm{~V}$, the pnp pair is off and the $6 \mu \mathrm{~A}$ current from $Q_{11}$ flows in $Q_{5}$, where it is copied by the $Q_{7}-Q_{6}$ current mirror to activate the $n p n$ input pair $Q_{1-} Q_{2}$.
image_name:Figure 6.36 Simplified schematic of the NE5234 input stage
description:The circuit is a simplified schematic of the NE5234 input stage. It features a dual differential amplifier configuration with both NPN and PNP transistors. The input stage is designed to maintain a constant transconductance, set by the current from Q11. The transition region around 0.8V allows both input pairs Q1-Q2 and Q3-Q4 to be active. The resistors are used to set biasing conditions and stabilize the circuit.

Figure 6.36 Simplified schematic of the NE5234 input stage.

In both extreme cases, the transconductance of the input stage is constant because it is set by the $6 \mu \mathrm{~A}$ current. In the transition region around 0.8 V , both input pairs $Q_{1}-Q_{2}$ and $Q_{3}-Q_{4}$ are active. The width of this region is about $\pm 3 V_{T}$ or $\pm 78 \mathrm{mV}$. In this region, some of the $6 \mu \mathrm{~A}$ from $Q_{11}$ flows in $Q_{3}-Q_{4}$, and the rest flows in $Q_{5}$, where it ultimately biases $Q_{1}-Q_{2}$ through $Q_{6}$. Therefore, the sum of the collector currents in $Q_{1}-Q_{4}$ is a constant of $6 \mu \mathrm{~A}$ ignoring base currents, base-width modulation, and mismatch. Since the transconductance of each input pair is proportional to its bias current, and since the total input-stage transconductance is the sum of the transconductances of both input pairs, the input-stage transconductance does not depend on $V_{I C}$. ${ }^{17}$

To obtain high gain in the first stage, transistors $Q_{9}, Q_{10}, Q_{13}$, and $Q_{14}$ must operate in the forward-active region so that the output resistance of the stage is high. Since Bias ${ }_{1}$ is set so that $\left|I_{C 13}\right|=\left|I_{C 14}\right|=6 \mu \mathrm{~A}$, Bias ${ }_{\mathrm{CM}}$ should be adjusted so that $I_{C 9}$ and $I_{C 10}$ also equal $6 \mu \mathrm{~A}$. However, if the currents in $Q_{9}$ and $Q_{10}$ are simply adjusted to this constant value, the common-mode output voltage at nodes 9 and 10 would be sensitive to small changes in transistors $Q_{9}, Q_{10}, Q_{13}$, and $Q_{14}$. For example, suppose that $Q_{9}$ and $Q_{10}$ conduct $6 \mu \mathrm{~A}$ as expected but $Q_{13}$ and $Q_{14}$ conduct $6.1 \mu \mathrm{~A}$ each because of a slight increase in their emitter areas. Then the common-mode output voltage would rise until KCL is satisfied at nodes 9 and 10, forcing transistors $Q_{13}$ and $Q_{14}$ to operate at the edge of saturation to reduce their currents to $6 \mu \mathrm{~A}$. Similarly, if $Q_{9}$ and $Q_{10}$ pull slightly more current than pushed by $Q_{13}$ and $Q_{14}$, the common-mode output output voltage would fall until KCL is satisfied. The key point is that the common-mode output voltage of the input stage is not well controlled by the circuit in Fig. 6.36. This problem is overcome in the second stage of the amplifier, which adjusts $\mathrm{Bias}_{\mathrm{CM}}$ to set the common-mode output voltage of the first stage so that $Q_{9}, Q_{10}, Q_{13}$, and $Q_{14}$ operate in the forward-active region.

Second Stage. Figure 6.37 shows a schematic of the NE5234 second stage. Nodes 9 and 10 are the outputs of the first stage and the inputs of the second stage. Capacitors $C_{21}$ and $C_{22}$ are used for frequency compensation; that is, they control the frequency response so that the op amp is stable when connected in a negative feedback loop. The topic of compensation is covered in Chapter 9. Capacitor $C_{22}$ is connected to the op-amp output, which is generated in the output stage. Both capacitors are ignored here. Emitter followers $Q_{21}$ and $Q_{22}$ reduce the loading of the second stage on the first. Ignore $Q_{23}$ and $Q_{24}$ at first because they are normally off. Transistors $Q_{25}-Q_{28}$ form a differential pair in which each side of the pair is split into two transistors. This differential pair amplifies the differential output of the first stage $v_{o d 1}$. Splitting the pair allows it to produce two outputs that are in phase with respect to each other, one at node 25 and the other at node 26 , as required by the output stage.

From a dc standpoint, (4.36) and (6.128) can be applied to find

$$
\begin{equation*}
\left|I_{C 15}\right|=\frac{R_{58}}{R_{15}}\left|I_{C 58}\right|=\left(\frac{33 \mathrm{k} \Omega}{66 \mathrm{k} \Omega}\right) 6 \mu \mathrm{~A}=3 \mu \mathrm{~A} \tag{6.131}
\end{equation*}
$$

Similarly, $\left|I_{C 16}\right|=\left|I_{C 19}\right|=4 \mu \mathrm{~A},\left|I_{C 17}\right|=\left|I_{C 18}\right|=21 \mu \mathrm{~A}$, and $\left|I_{C 20}\right|=6.6 \mu \mathrm{~A}$. For simplicity, assume that $\left|I_{C 16}\right|$ and $\left|I_{C 19}\right|$ set $V_{E B 21}=V_{E B 22}=0.7 \mathrm{~V}$. Ignoring base currents, $\left|I_{C 15}\right|$ flows in Schottky diode $D_{1}$. The voltage across the diode is

$$
\begin{equation*}
V_{D 1}=V_{T} \ln \frac{\left|I_{C 15}\right|}{I_{S(D 1)}} \tag{6.132}
\end{equation*}
$$

where $I_{S(D 1)}$ is the saturation current of $D_{1}$. Assume $I_{S(D 1)}=6 \times 10^{-13} \mathrm{~A}$. Then

$$
\begin{equation*}
V_{D 1}=0.026 \ln \left(\frac{3 \times 10^{-6}}{6 \times 10^{-13}}\right) \mathrm{V}=0.4 \mathrm{~V} \tag{6.133}
\end{equation*}
$$

image_name:Figure 6.37 Schematic of the NE5234 second stage
description:The circuit shown in Figure 6.37 is the second stage of the NE5234 operational amplifier. It includes a Widlar current mirror formed by transistors Q29 and Q30 along with resistor R29. The circuit is designed to amplify signals with high precision. Schottky diode D1 is used in the circuit to prevent saturation of the transistors. Capacitors C21 and C22 are used for frequency compensation. The circuit operates between power supply rails VCC and -VEE, with various bias voltages (Bias1, Bias2, Bias3, BiasCM) for proper transistor operation.

Figure 6.37 Schematic of the NE5234 second stage. Node Out is the output of the third stage (shown in Fig. 6.39).

Resistor $R_{29}$ along with transistors $Q_{29} Q_{30}$ form a Widlar current mirror. If $\beta_{F} \rightarrow \infty$, (4.190) gives

$$
\begin{equation*}
V_{T} \ln \frac{I_{C 30}}{I_{S 30}}-V_{T} \ln \frac{I_{C 29}}{I_{S 29}}-I_{C 29} R_{29}=0 \tag{6.134}
\end{equation*}
$$

In the NE5234 op amp, $I_{S 29} / I_{S 30}=7$ and

$$
\begin{equation*}
V_{T} \ln \frac{7 I_{C 30}}{I_{C 29}}=I_{C 29} R_{29} \tag{6.135}
\end{equation*}
$$

Since $I_{C 30}=\left|I_{C 20}\right|=6.6 \mu \mathrm{~A}$, a trial-and-error solution of this equation gives $I_{C 29}=42 \mu \mathrm{~A}$. Therefore, the current available for $Q_{25}-Q_{28}$ is $I_{C 29}-I_{D 1}=39 \mu \mathrm{~A}$. Let $V_{9}$ and $V_{10}$ represent the voltages from nodes 9 and 10 to ground, respectively, and assume $V_{9}=V_{10}$. Then $I_{C 25}=I_{C 26}=I_{C 27}=I_{C 28}=39 / 4 \mu \mathrm{~A} \simeq 10 \mu \mathrm{~A}$. For simplicity, assume that these currents set $V_{B E 25}=V_{B E 26}=V_{B E 27}=V_{B E 28}=0.7 \mathrm{~V}$.

Let $V_{\text {cmout } 1}$ represent the common-mode output voltage of the first stage, including both dc and ac components. It is the average of the voltages from nodes 9 and 10 to ground:

$$
\begin{equation*}
V_{\text {cmout } 1}=\frac{1}{2}\left(V_{9}+V_{10}\right) \tag{6.136}
\end{equation*}
$$

Similarly, let $V_{\text {biascm }}$ represent the voltage from node Bias ${ }_{\mathrm{Cm}}$ to ground. Elements in the first and second stages work together to set both of these voltages, as explained below.

Consider the first stage, where $V_{\text {biascm }}$ is an input and $V_{\text {cmout } 1}$ is an output. The relationship between these voltages here is controlled by the common-emitter amplifiers with degeneration ( $Q_{9}$ and $Q_{10}$ ) and active loads ( $Q_{13}$ and $Q_{14}$ ). Let $v_{\text {biascm }}, v_{9}$, and $v_{10}$ represent the changes in the voltages from nodes $\mathrm{Bias}_{\mathrm{CM}}, 9$, and 10 to ground, respectively. Let the small-signal gain $v_{9} / v_{\text {biascm }}$ equal $A$. Then $A=v_{10} / v_{\text {biascm }}$ from symmetry. In other words, $A$ is the commonmode gain from $B^{-295}{ }_{\mathrm{CM}}$ to the first-stage output. The polarity of $A$ is negative because pulling up on $\mathrm{Bias}_{\mathrm{CM}}$ increases the collector currents in $Q_{9}$ and $Q_{10}$, reducing the common-mode output voltage. The magnitude of $A$ is large, but its magnitude is not calculated here because it is not important to a first-order analysis that finds the operating point. For simplicity, assume $A \rightarrow-\infty$ when $Q_{9}, Q_{10}, Q_{13}$, and $Q_{14}$ operate in the forward-active region.

Assume the op-amp common-mode input voltage $V_{I C}$ is much less than the 0.8 V threshold given in (6.130). Then $Q_{1}$ and $Q_{2}$ are off. Since $\left|I_{C 13}\right|=\left|I_{C 14}\right|=6 \mu \mathrm{~A}$, the dc voltages across $R_{13}$ and $R_{14}$ are

$$
\begin{equation*}
V_{R 13}=V_{R 14}=6 \mu \mathrm{~A}(33 \mathrm{k} \Omega)=0.2 \mathrm{~V} \tag{6.137}
\end{equation*}
$$

If $V_{C E 13(\mathrm{sat})}=V_{C E 14(\mathrm{sat})}=-0.1 \mathrm{~V}, Q_{13}$ and $Q_{14}$ operate in the forward-active region if $V_{\text {cmout } 1}<V_{C C}-0.3 \mathrm{~V}$.

To satisfy KCL at nodes 9 and $10, Q_{9}$ and $Q_{10}$ must adapt to pull the same current pushed by $Q_{13}$ and $Q_{14}$, which is $6 \mu \mathrm{~A}$ under nominal conditions. Assume that this current sets $V_{B E 9}=$ $V_{B E 10}=0.7 \mathrm{~V}$. Also, since $V_{I C} \ll 0.8 \mathrm{~V}$ is assumed, $\left|I_{C 3}\right|=\left|I_{C 4}\right|=\left|I_{C 11}\right| / 2=3 \mu \mathrm{~A}$, and the dc currents in $R_{9}$ and $R_{10}$ are

$$
\begin{equation*}
I_{R 9}=I_{R 10}=I_{C 9}+\left|I_{C 3}\right|=I_{C 10}+\left|I_{C 4}\right|=9 \mu \mathrm{~A} \tag{6.138}
\end{equation*}
$$

As a result, the dc voltages across these resistors are

$$
\begin{equation*}
V_{R 9}=V_{R 10}=9 \mu \mathrm{~A}(22 \mathrm{k} \Omega)=0.2 \mathrm{~V} \tag{6.139}
\end{equation*}
$$

Assume $V_{C E 9(\text { sat })}=V_{C E 10(\text { sat })}=0.1 \mathrm{~V}$. Then $Q_{9}$ and $Q_{10}$ operate in the forward active region if $V_{\text {cmout } 1}>0.3 \mathrm{~V}$ and $V_{\text {biascm }}$ is

$$
\begin{equation*}
V_{\text {biascm }}=V_{R 9}+V_{B E 9}=V_{R 10}+V_{B E 10}=0.9 \mathrm{~V} \tag{6.140}
\end{equation*}
$$

This behavior is summarized in Fig. 6.38, which shows two plots of $V_{\text {cmout } 1}$ versus $V_{\text {biascm }}$. One plot is labeled Amplifier Characteristic. For $V_{\text {biascm }}<0.9 \mathrm{~V}$, it shows that $V_{\text {cmout } 1}$ is constant at $V_{C C}-0.3 \mathrm{~V}$ because $Q_{13}$ and $Q_{14}$ saturate. For $V_{\text {biascm }}>0.9 \mathrm{~V}$, this plot shows that $V_{\text {cmout } 1}$ is constant at 0.3 V because $Q_{9}$ and $Q_{10}$ saturate. For $V_{\text {biascm }}=0.9 \mathrm{~V}, V_{\text {cmout }}$ falls from $V_{C C}-0.3 \mathrm{~V}$ to 0.3 V because $A \rightarrow-\infty$ is assumed above.
image_name:Figure 6.38
description:The graph in Figure 6.38 is a plot of \( V_{\text{cmout} 1} \) versus \( V_{\text{biascm}} \), illustrating the characteristics of an amplifier and its feedback. The graph is a typical linear plot with both axes labeled in volts (V).

Axes:
- **Y-axis (Vertical):** Represents \( V_{\text{cmout} 1} \), the common-mode output voltage from stage 1. The scale is linear, and the axis is labeled with values such as \( V_{CC} - 0.3 \) V, 0.5 V, and 0.3 V.
- **X-axis (Horizontal):** Represents \( V_{\text{biascm}} \), the bias common-mode voltage. The scale is linear, with a critical point at 0.9 V.

Graph Characteristics:
1. **Amplifier Characteristic:**
- For \( V_{\text{biascm}} < 0.9 \) V, \( V_{\text{cmout} 1} \) remains constant at \( V_{CC} - 0.3 \) V. This is due to the saturation of transistors \( Q_{13} \) and \( Q_{14} \).
- For \( V_{\text{biascm}} > 0.9 \) V, \( V_{\text{cmout} 1} \) is constant at 0.3 V, indicating saturation of transistors \( Q_{9} \) and \( Q_{10} \).
- At \( V_{\text{biascm}} = 0.9 \) V, \( V_{\text{cmout} 1} \) transitions sharply from \( V_{CC} - 0.3 \) V to 0.3 V.
- The slope of the amplifier characteristic is indicated as \( A \rightarrow -\infty \), suggesting an infinite gain at the transition point.

2. **Feedback Characteristic:**
- The feedback characteristic is represented by a line with a slope of 1, described by the equation \( V_{\text{biascm}} = V_{\text{cmout} 1} + 0.4 \) V.
Key Features:
- **Operating Point:**
- The operating point is marked at the intersection of the amplifier and feedback characteristics, specifically at \( V_{\text{biascm}} = 0.9 \) V, and \( V_{\text{cmout} 1} = 0.5 \) V.

Annotations:
- The plot includes annotations for the amplifier characteristic, feedback characteristic, slope, and operating point, aiding in the understanding of the graph's behavior and critical transitions.

Figure 6.38 Plots of $V_{\text {cmout } 1}$ versus $V_{\text {biascm }}$. The amplifier characteristic comes from stage 1 , and the feedback characteristic comes from stage 2.

Now consider the second stage, where $V_{\text {cmout } 1}$ is an input and $V_{\text {biascm }}$ is an output. Assume that the first-stage common-mode output voltage increases by $v_{\text {cmout } 1}$. Then the voltages from the emitters of $Q_{21}$ and $Q_{22}$ to ground also increase by approximately $v_{\text {cmout }}$ because these transistors act as emitter followers. These changes cause the voltage from the collector of $Q_{29}$ to ground to rise by approximately $v_{\text {cmout } 1}$ because the base-emitter voltages of $Q_{25} Q_{28}$ are almost constant. This result stems from the fact that the combination of $Q_{25-} Q_{26}$ on the one hand and $Q_{27}-Q_{28}$ on the other hand forms a differential pair. Since the input to this differential pair is a pure common-mode signal under the conditions given above, the collector currents of the individual transistors are approximately constant assuming that the tail current source $Q_{29}$ has high output resistance. Furthermore, from a dc standpoint, the emitter followers $Q_{21}$ and $Q_{22}$ level shift $V_{9}$ and $V_{10}$ up by 0.7 V , and the split differential pair $Q_{25-} Q_{28}$ level shifts the emitter follower outputs back down by the same amount. Then because the voltage across Schottky diode $D_{1}$ is constant as shown by (6.133), the voltage from Bias ${ }_{\mathrm{CM}}$ to ground is the first-stage common-mode output voltage shifted up by 0.4 V . Since the collector voltage of $Q_{29}$ rises by $v_{\text {cmout }}$ in this example, the voltage from Bias ${ }_{\mathrm{CM}}$ to ground also rises by the same amount. As a result, the voltage from node $\mathrm{Bias}_{\mathrm{CM}}$ to ground is

$$
\begin{equation*}
V_{\text {biascm }}=V_{\text {cmout } 1}+0.4 \mathrm{~V} \tag{6.141}
\end{equation*}
$$

This equation is plotted in Fig. 6.38. It is labeled as the Feedback Characteristic because the role of the second stage is to sense, level shift, and feed the first-stage common-mode output voltage back to the first stage to control the common-mode operating point. This loop is an example of negative feedback because increasing $V_{\text {cmout } 1}$ increases $V_{\text {biascm }}$, which then reduces $V_{\text {cmout } 1}$ through the action of the common-mode amplifiers with gain $A$ in the first stage described above. Although this negative feedback loop operates on the first-stage common-mode output voltage, it does not operate on the first-stage differential output. For example, suppose that $V_{9}$ increases incrementally and $V_{10}$ decreases by the same amount. Then the voltage from node 29 to ground is constant because $Q_{25}$ and $Q_{26}$ pull up while $Q_{27}$ and $Q_{28}$ pull down with equal strength. As a result, $V_{\text {biascm }}$ is constant, and the loop is inactive. Therefore, the loop under consideration is called a common-mode feedback loop. The topic of common-mode feedback is covered in detail in Chapter 12.

Figure 6.38 presents a graphical analysis to explain how the bias point is set here. Two variables, $V_{\text {biascm }}$ and $V_{\text {cmout } 1}$, are central to this analysis. These variables are related to each other in two ways, by the amplifier and feedback characteristics described above. Since both characteristics must be satisfied, the circuits operate at their intersection, where the average value of $V_{\text {biascm }}=0.9 \mathrm{~V}$ and the average value of $V_{\text {cmout } 1}=0.5 \mathrm{~V}$. In principle, finite $A$ and $V_{E B 21}=V_{E B 22} \neq V_{B E 25}=V_{B E 26}=V_{B E 27}=V_{B E 28}$ alter the operating point slightly, but $Q_{9}, Q_{10}, Q_{13}$, and $Q_{14}$ still operate in the forward-active region for a wide range of process, supply, and temperature conditions in practice.

Output Stage. In many op amps, the output stage uses transistors operating in a commoncollector configuration to drive the output node. For example, the 741 op amp uses the circuit shown in Fig. 5.20. Transistors $Q_{14}$ and $Q_{20}$ there operate as emitter followers, giving the output stage low output resistance, as desired. These transistors are biased by $Q_{13 A}, Q_{18}$, and $Q_{19}$ to operate in a Class AB mode, giving high-power efficiency and low-crossover distortion. However, the output swing available with this structure is low. Equations 5.80 and 5.81 show that the output can swing from about 1.4 V above the low supply $\left(-V_{E E}\right)$ to about 0.8 V below the high supply $\left(V_{C C}\right)$. This limitation was not a major concern when the supply voltages were $\pm 15 \mathrm{~V}$. However, it would mean that the output could not swing at all with $V_{C C}=2 \mathrm{~V}$ and $V_{E E}=0$.

To overcome this limitation, the NE5234 op amp does not use transistors in a commoncollector configuration to drive its output. Figure 6.39 shows a schematic of the NE5234 output
image_name:Figure 6.39 Schematic of the NE5234 output stage
description:The NE5234 output stage uses common-emitter transistors Q74 and Q75 to drive the output. The circuit is designed to reduce output resistance through negative feedback. Nodes 25 and 26 are the inputs to this stage. Capacitors C25 and C26 along with resistors R25 and R26 are used for frequency compensation. The output is connected to a load represented by IL.

Figure 6.39 Schematic of the NE5234 output stage.
stage. Nodes 25 and 26 are the inputs of this stage and outputs of the second stage. Capacitors $C_{25}$ and $C_{26}$ along with resistors $R_{25}$ and $R_{26}$ are for frequency compensation and are ignored here. The output is driven by common-emitter transistors $Q_{74}$ and $Q_{75}$. Although the resulting output resistance of the stage is high, the output resistance is reduced dramatically by negative feedback around the op amp. Negative feedback is covered in Chapter 8. The main reason to use such an output stage is that it can drive the output node to within $V_{C E 75(\text { sat })}$ or about 0.1 V of the low supply and to within $\left|V_{C E 74(\text { sat })}\right|$ or about 0.1 V of the high supply. In other words, this output stage gives almost rail-to-rail output swing.

A design goal is for $Q_{74}$ to be able to push up to 10 mA into a load connected to the output. Similarly, $Q_{75}$ should be able to pull the same current out of the load. ${ }^{18}$ The bias currents of $Q_{25}$ and $Q_{26}$ in Fig. 6.37 are about $10 \mu \mathrm{~A}$ each. To limit the current required to flow into or out of nodes 25 and 26 to this amount, the output stage should provide a current gain of at least 1000. To meet this requirement when $Q_{75}$ pulls current from the load, emitter follower $Q_{68}$ is used. The current gain from node 26 to the output is approximately $\beta_{F 68} \beta_{F 75}=\beta_{F(n p n)}^{2}$, which is greater than 1000 because the minimum value of $\beta_{F(n p n)}$ is about 40 in this process. On the other hand, when $Q_{74}$ pushes current into the load, the current gain might be less than 1000 if $Q_{74}$ were driven by only a pnp emitter follower because the minimum value of $\beta_{F(p n p)}$ is about 10 in this process. To overcome this problem, the buffer that drives the base of $Q_{74}$ consists of a complementary emitter follower $Q_{64} Q_{65}$, giving a current gain from node 25 to the output of approximately $\beta_{F 64} \beta_{F 65} \beta_{F 74}=\beta_{F(p n p)}^{2} \beta_{F(n p n)}$.

Nodes Bias ${ }_{1}$ and Bias5 in Fig. 6.39 come from the bias circuit in Fig. 6.34. From a dc standpoint, (4.36) and (6.128) can be applied to find

$$
\begin{equation*}
\left|I_{C 61}\right|=\frac{R_{58}}{R_{61}}\left|I_{C 58}\right|=\frac{33 \mathrm{k} \Omega}{33 \mathrm{k} \Omega} 6 \mu \mathrm{~A}=6 \mu \mathrm{~A} \tag{6.142}
\end{equation*}
$$

Transistors $Q_{62}$ and $Q_{63}$ along with $R_{62}$ and $R_{63}$ form a current mirror with emitter degeneration. Transistor $Q_{67}$ is normally off and is ignored at first. Applying (4.136) and (6.128) gives $I_{C 63}=\left(R_{62} / R_{63}\right) 6 \mu \mathrm{~A}=70 \mu \mathrm{~A}$. However, this equation assumes that the voltage drop on $R_{62}$ is equal to that on $R_{63}$ because the difference in the base-emitter voltages of $Q_{62}$ and $Q_{63}$ is negligible. With the currents calculated above, the difference in the base-emitter voltages is $V_{T} \ln \left(I_{C 62} / I_{C 63}\right)=64 \mathrm{mV}$ assuming $Q_{62}$ and $Q_{63}$ are identical. Since the voltage drop on $R_{62}$ is $6 \mu \mathrm{~A}(14 \mathrm{k} \Omega)=84 \mathrm{mV}, V_{B E 62}-V_{B E 63}$ is not negligible here. From KVL with $\beta_{F} \rightarrow \infty$,

$$
\begin{equation*}
I_{C 62} R_{62}-I_{C 63} R_{63}=V_{B E 63}-V_{B E 62}=V_{T} \ln \left(I_{C 63} / I_{C 62}\right) \tag{6.143}
\end{equation*}
$$

A trial-and-error solution of this equation gives $I_{C 63}=33 \mu \mathrm{~A}$. Ignoring base currents, $I_{C 64}=I_{C 63}=33 \mu \mathrm{~A}$. The current in $R_{65}$ is $I_{R 65}=V_{E B 74} / R_{65}$, which equals $\left|I_{C 65}\right|$ ignoring base currents. In practice, $V_{E B 74}$ depends on $\left|I_{C 74}\right|$. A case in which $\left|I_{C 74}\right|$ is large ( $>1 \mathrm{~mA}$ ) is considered below. In this case, $V_{E B 74}$ is also large. For example, let $V_{E B 74}=0.75 \mathrm{~V}$. Therefore,
image_name:Figure 6.40 Schematic of the bias circuit for the output stage
description:This is a bias circuit for the output stage, using multiple NPN transistors and resistors to set bias voltages and currents. The circuit is powered by VCC and grounded at VEE = 0. It includes several bias points labeled Bias1, Bias2, Bias3, and Bias5, as well as a base voltage point Pbase and Nbase. The resistors are used to set the bias currents through various branches of the circuit.

Figure 6.40 Schematic of the bias circuit for the output stage.
$\left|I_{C 65}\right|=I_{R 65}=100 \mu \mathrm{~A}$. Since the base-emitter voltage of $Q_{69}$ is equal to that of $Q_{49}$ in Fig. 6.34, $I_{C 69}=I_{C 49}=6 \mu \mathrm{~A}$. Ignoring base currents, $I_{C 68}=I_{C 69}=6 \mu \mathrm{~A}$. However, nonzero base currents often have a significant effect in the output stage, especially on $I_{C 64}$, $\left|I_{C 65}\right|$, and $I_{C 68}$, which are recalculated below after $\left|I_{C 74}\right|$ and $I_{C 75}$ are found. Transistors $Q_{70}$, $Q_{72}$, and $Q_{73}$ are normally off and ignored at first.

The dc currents in the other transistors in the output stage are set by the bias circuit for the output stage, which is shown in Fig. 6.40. Nodes Pbase and Nbase are outputs of the output stage and inputs to this bias circuit. Node Bias $_{2}$ is an output that becomes an input to the second stage in Fig. 6.37 and is ignored at first. Node $\mathrm{Bias}_{3}$ comes from the second stage. Since $V_{B E 31}=V_{B E 30}, I_{C 31}=I_{C 30}=6.6 \mu \mathrm{~A}$. This current is mirrored through $Q_{32}-Q_{33}$ and then $Q_{34-} Q_{35}$ so that $I_{C 35}=6.6 \mu \mathrm{~A}$ ignoring base currents and base-width modulation. Applying (4.136) and (6.128) gives $\left|I_{C 44}\right|=6 \mu \mathrm{~A}$. Similarly, $\left|I_{C 36}\right|=\left(R_{58} / R_{36}\right) 6 \mu \mathrm{~A}=14 \mu \mathrm{~A}$. Then $I_{C 37}=I_{C 38}=\left|I_{C 36}\right|-I_{C 35}=7.4 \mu \mathrm{~A}$. Node Bias5 comes from the bias circuit in Fig. 6.34. Since $V_{B E 41}=V_{B E 49}$, and since $I_{S 41} / I_{S 49}=3$ in the NE5234 op amp, $I_{C 41}=3 I_{C 49}=18 \mu \mathrm{~A}$.

To focus on the interaction between the circuits of Figs. 6.39 and 6.40, Fig. 6.41 shows a simplified schematic of the NE5234 output stage with its bias circuit. For simplicity here, the transistors that are normally off are omitted, and the bias currents calculated above are set by current sources. As in many output stages, this stage operates in a Class AB mode. However, the basic relationship between the collector currents of the two output transistors differs here compared to that in many op amps, as explained below.

In op amps with common-collector output drivers, the classical Class AB biasing technique sets the product of the collector currents of the two output transistors to a constant. For example,
image_name:Figure 6.41 Simplified schematic of the NE5234 output stage with its bias circuit
description:This circuit is a simplified schematic of the NE5234 output stage with its bias circuit. It operates in Class AB mode, with the bias currents set by current sources. The transistors are organized to provide the necessary output drive, with current sources ensuring the correct biasing.

Figure 6.41 Simplified schematic of the NE5234 output stage with its bias circuit.
in the $741 \mathrm{op} \mathrm{amp}, Q_{14}$ and $Q_{20}$ in Fig. 5.20 are the output transistors. These transistors are biased by $Q_{18}$ and $Q_{19}$ through a KVL loop, as shown in (5.82). Manipulating this equation gives

$$
\begin{equation*}
I_{C 14}\left|I_{C 20}\right|=I_{C 18} I_{C 19}\left(\frac{I_{S 14}\left|I_{S 20}\right|}{I_{S 18} I_{S 19}}\right)=\mathrm{constant} \tag{6.144}
\end{equation*}
$$

As a result, neither $I_{C 14}$ nor $\left|I_{C 20}\right|$ goes to zero in principle even when the other is large. However, in practice, the KVL loop includes terms omitted from (5.82) for simplicity. For example, voltage drops appear on nonzero resistances in the base and emitter regions of the driving transistor. These extra drops increase the $\left|V_{B E}\right|$ of the driving transistor as the magnitude of the load current increases, turning the inactive transistor off at some point. As a result, the time required to turn this transistor back on increases the delay in driving the output in the other direction, worsening crossover distortion. ${ }^{19}$

To overcome this problem, the output transistors in the NE5234 op amp are biased so that neither turns off even for extreme signal swings. ${ }^{19,20}$ The circuit compares the collector currents of the two output transistors and controls the smaller current through negative feedback when the driving current is large. The collector currents can be sensed by placing elements in series with the collectors or emitters of the output transistors; however, the voltage drops across such elements would not be zero and would reduce the output swing. To maximize the output swing, the collector currents are sensed through the base-emitter voltages of the output transistors. These voltages are manipulated and sent to differential pair $Q_{45}-Q_{46}$ for comparison. This differential pair operates on the voltages from the bases of these transistors to ground, $V_{B 45}$ and $V_{B 46}$. For $V_{B 46}$,

$$
\begin{equation*}
V_{B 46}=V_{B E 75}=V_{T} \ln \frac{I_{C 75}}{I_{S 75}} \tag{6.145}
\end{equation*}
$$

In other words, the natural log function maps the collector current of $Q_{75}$ to its base-emitter voltage, which equals $V_{B 46}$ by KVL.

For $V_{B 45}$, the emitter-base voltage of $Q_{74}$ is converted into the collector current of $Q_{43}$ and then back into a voltage across $Q_{42}$ and $R_{42}$. From KVL,

$$
\begin{equation*}
V_{B 45}=V_{B E 42}+\left|I_{C 43}\right| R_{42} \tag{6.146}
\end{equation*}
$$

where

$$
\begin{equation*}
\left|I_{C 43}\right|=\frac{V_{E B 74}-V_{E B 43}}{R_{43}} \tag{6.147}
\end{equation*}
$$

Since $R_{42}=R_{43}$, substituting (6.147) into (6.146) gives

$$
\begin{equation*}
V_{B 45}=V_{B E 42}+V_{E B 74}-V_{E B 43}=V_{E B 74}+V_{T} \ln \left(\frac{\left|I_{S 43}\right|}{I_{S 42}}\right)=V_{T} \ln \frac{\left|I_{C 74}\right|}{I_{S 75}} \tag{6.148}
\end{equation*}
$$

where $I_{S 75}=\left|I_{S 74}\right| I_{S 42} /\left|I_{S 43}\right|$ is assumed. This equation shows that $V_{B 45}$ is equal to the baseemitter voltage of a transistor equivalent to $Q_{75}$ whose collector current equals $\left|I_{C 74}\right|$. This conversion allows $\left|I_{C 74}\right|$ to be compared to $I_{C 75}$ by $Q_{45}-Q_{46}$ in a way that is not sensitive to differences in the saturation currents of pnp and npn transistors.

If $\left|V_{B 45}-V_{B 46}\right|>3 V_{T}$, the transistor in the $Q_{45} Q_{46}$ pair with the higher base voltage turns off. Under this condition, the voltage from the emitters of these transistors to ground is controlled by the output transistor that conducts the least current. This voltage becomes the input to one side of differential pair $Q_{39}-Q_{40}$. The other input is a constant voltage set by $I_{R E F}=$ $\left|I_{C 36}\right|-I_{C 35}$ flowing in diode-connected transistors $Q_{37}$ and $Q_{38}$. Transistors $Q_{39} Q_{40}$ form the core of a differential amplifier, and this amplifier operates in a negative feedback
loop. For example, assume that $Q_{75}$ conducts a large current to pull the op-amp output low. Then the loop controls the collector current of $Q_{74}$. If the voltage from the base of $Q_{40}$ rises for some reason, $I_{C 40}$ is increased and $I_{C 39}$ is reduced. As a result, the voltage from node 25 to ground increases, which increases the voltage from node Pbase to ground because $Q_{64}$ and $Q_{65}$ are emitter followers. This change reduces $V_{B 45}$ because common-emitter amplifier $Q_{43}$ provides inverting gain at low frequencies. Finally, reducing $V_{B 45}$ reduces the voltage from the base of $Q_{40}$ to ground because $V_{E B 45}$ is almost constant. In other words, the loop responds to a change in the voltage at the base of $Q_{40}$ by driving this voltage in the opposite direction of the original change. Similar reasoning applies if $Q_{74}$ conducts a large current to pull the opamp output high. Therefore, the loop has negative gain, which means that it is a negative feedback loop, as stated above. Negative feedback is covered in Chapter 8. The key point here is that if the magnitude of the gain around this loop is high enough, the loop drives the voltage from the base of $Q_{40}$ to ground to equal the voltage from the base of $Q_{39}$ to ground. This result can be viewed as an example of the summing-point constraints used to analyze ideal op-amp circuits such as those in Fig. 6.3.

When $Q_{45}$ and $Q_{46}$ are both on, the relationship between the collector currents of $Q_{74}$ and $Q_{75}$ is determined by the interaction of one KCL equation and two KVL equations in Fig. 6.41. First, from KCL

$$
\begin{equation*}
\left|I_{C 45}\right|+\left|I_{C 46}\right|=\left|I_{C 44}\right| \tag{6.149}
\end{equation*}
$$

Also, from KVL,

$$
\begin{equation*}
V_{B E 75}+V_{E B 46}-V_{E B 45}-V_{B 45}=0 \tag{6.150}
\end{equation*}
$$

Finally, from KVL,

$$
\begin{equation*}
V_{B E 75}+V_{E B 46}-V_{B E 40}-I_{R 40} R_{40}+I_{R 39} R_{39}+V_{B E 39}-V_{B E 37}-V_{E B 38}=0 \tag{6.151}
\end{equation*}
$$

where $I_{R 39}$ and $I_{R 40}$ are the currents in $R_{39}$ and $R_{40}$, respectively. Since the voltage from the base of $Q_{40}$ is driven to equal the voltage from the base of $Q_{39}$ by negative feedback,

$$
\begin{equation*}
V_{B E 40}+I_{R 40} R_{40}=V_{B E 39}+I_{R 39} R_{39} \tag{6.152}
\end{equation*}
$$

and (6.151) reduces to

$$
\begin{equation*}
V_{B E 75}+V_{E B 46}-V_{B E 37}-V_{E B 38}=0 \tag{6.153}
\end{equation*}
$$

Substituting (1.82) for each term in this equation gives

$$
\begin{equation*}
V_{T} \ln \frac{I_{C 75}}{I_{S 75}}+V_{T} \ln \frac{\left|I_{C 46}\right|}{\left|I_{S 46}\right|}-V_{T} \ln \frac{I_{C 37}}{I_{S 37}}-V_{T} \ln \frac{\left|I_{C 38}\right|}{\left|I_{S 38}\right|}=0 \tag{6.154}
\end{equation*}
$$

Ignoring base currents, $I_{C 37}=\left|I_{C 38}\right|=I_{R E F}=\left|I_{C 36}\right|-I_{C 35}$. Therefore,

$$
\begin{equation*}
\left(\frac{I_{C 75}}{I_{R E F}}\right) \frac{I_{S 37}}{I_{S 75}}=\left(\frac{I_{R E F}}{\left|I_{C 46}\right|}\right) \frac{\left|I_{S 466}\right|}{\left|I_{S 38}\right|} \tag{6.155}
\end{equation*}
$$

Also, substituting (1.82) for the first three terms in (6.150) and (6.148) for the last term gives

$$
\begin{equation*}
V_{T} \ln \frac{I_{C 75}}{I_{S 75}}+V_{T} \ln \frac{\left|I_{C 46}\right|}{\left|I_{S 46}\right|}-V_{T} \ln \frac{\left|I_{C 45}\right|}{\left|I_{S 45}\right|}-V_{T} \ln \frac{\left|I_{C 74}\right|}{I_{S 75}}=0 \tag{6.156}
\end{equation*}
$$

Assuming $Q_{45}$ and $Q_{46}$ are identical, this equation becomes

$$
\begin{equation*}
\frac{I_{C 75}}{\left|I_{C 74}\right|}=\frac{\left|I_{C 45}\right|}{\left|I_{C 46}\right|} \tag{6.157}
\end{equation*}
$$

Substituting (6.149) into (6.157) gives

$$
\begin{equation*}
\frac{I_{C 75}}{\left|I_{C 74}\right|}=\frac{\left|I_{C 44}\right|-\left|I_{C 46}\right|}{\left|I_{C 46}\right|} \tag{6.158}
\end{equation*}
$$

Solving for $\left|I_{C 46}\right|$ gives

$$
\begin{equation*}
\left|I_{C 46}\right|=\frac{\left|I_{C 44}\right|\left|I_{C 74}\right|}{I_{C 75}+\left|I_{C 74}\right|} \tag{6.159}
\end{equation*}
$$

Substituting this equation into (6.155) gives

$$
\begin{equation*}
\frac{I_{C 75}\left|I_{C 74}\right|}{I_{C 75}+\left|I_{C 74}\right|}=\frac{\left(I_{R E F}\right)^{2}}{\left|I_{C 44}\right|} \frac{I_{S 75}}{I_{S 37}} \frac{\left|I_{S 46}\right|}{\left|I_{S 38}\right|} \tag{6.160}
\end{equation*}
$$

In the NE5234 op amp, $I_{R E F}=7.4 \mu \mathrm{~A}$ and $\left|I_{C 44}\right|=6 \mu \mathrm{~A}$ as calculated above. Also, $I_{S 75} / I_{S 37}=10$ and $\left|I_{S 46}\right| /\left|I_{S 38}\right|=2$. When the load current $I_{L}=0,(6.160)$ gives

$$
\begin{equation*}
I_{C 75}=\left|I_{C 74}\right|=2 \frac{(7.4 \mu \mathrm{~A})^{2}}{6 \mu \mathrm{~A}} 20=360 \mu \mathrm{~A} \tag{6.161}
\end{equation*}
$$

When $I_{L}$ is big and negative, it flows in $Q_{75}$, and $V_{B E 75}$ is big enough to turn off $Q_{46}$. Therefore, the negative feedback loop in Fig. 6.41 sets the collector current in $Q_{74}$. To find $\left|I_{C 74}\right|$, the limit of (6.160) with $I_{C 75} \rightarrow \infty$ gives

$$
\begin{equation*}
\lim _{I_{C 75} \rightarrow \infty}\left(\frac{I_{C 75}\left|I_{C 74}\right|}{I_{C 75}+I_{C 74}}\right)=\left|I_{C 74}\right|=\frac{\left(I_{R E F}\right)^{2}}{\left|I_{C 44}\right|} \frac{I_{S 75}}{I_{S 37}} \frac{\left|I_{S 46}\right|}{\left|I_{S 38}\right|}=\frac{(7.4 \mu \mathrm{~A})^{2}}{6 \mu \mathrm{~A}} 20=180 \mu \mathrm{~A} \tag{6.162}
\end{equation*}
$$

Similarly, when $I_{L}$ is big and positive, it comes from $Q_{74}$, and $Q_{45}$ turns off. Then

$$
\begin{equation*}
\lim _{\mid I_{C 74 \mid} \rightarrow \infty}\left(\frac{I_{C 75}\left|I_{C 74}\right|}{I_{C 75}+I_{C 74}}\right)=I_{C 75}=\frac{\left(I_{R E F}\right)^{2}}{\left|I_{C 44}\right|} \frac{I_{S 75}}{I_{S 37}} \frac{\left|I_{S 46}\right|}{\left|I_{S 38}\right|}=180 \mu \mathrm{~A} \tag{6.163}
\end{equation*}
$$

These equations give the currents flowing in the inactive output transistor when the other transistor drives a load current large enough to turn either $Q_{45}$ or $Q_{46}$ off. These currents are half the bias current that flows in both output transistors when the load current is zero.

The output either sources or sinks current, depending on the output voltage and load. As a result, the properties of the output stage are dependent on the particular value of output voltage and current. For example, assume that the load current $I_{L}=1 \mathrm{~mA}$ and that this current flows out of the output terminal. Further assume that the load resistance is $2 \mathrm{k} \Omega$. From KCL at the output,

$$
\begin{equation*}
\left|I_{C 74}\right|=I_{C 75}+I_{L}=I_{C 75}+1 \mathrm{~mA} \tag{6.164}
\end{equation*}
$$

Substituting this equation into (6.160) and solving for $I_{C 75}$ in the NE5234 op amp gives $I_{C 75}=210 \mu \mathrm{~A}$. Therefore, $\left|I_{C 74}\right|=1.2 \mathrm{~mA}$. If the load current increases to $1.1 \mathrm{~mA}, I_{C 75}$ decreases by only a few $\mu \mathrm{A}$ and is still about $210 \mu \mathrm{~A}$ while $\left|I_{C 74}\right|$ becomes about 1.3 mA . In other words, the current in $Q_{75}$ is almost constant under these conditions because its current is regulated by the loop described above.

Now that the collector currents of $Q_{74}$ and $Q_{75}$ have been calculated, we are able to calculate the collector currents in $Q_{42}, Q_{43}, Q_{45}$, and $Q_{46}$. Ignoring base currents, KVL across the emitter-base junctions of $Q_{43}$ and $Q_{74}$ gives

$$
\begin{equation*}
\left|I_{C 43}\right| R_{43}=V_{T} \ln \frac{\left|I_{C 74}\right|}{\left|I_{C 43}\right|} \frac{\left|I_{S 43}\right|}{\left|I_{S 74}\right|} \tag{6.165}
\end{equation*}
$$

The ratio of the emitter area of $Q_{43}$ to that of $Q_{74}$ is $3 / 32$. Therefore,

$$
\begin{equation*}
\left|I_{C 43}\right|(1.3 \mathrm{k} \Omega)=V_{T} \ln \frac{1200 \mu \mathrm{~A}}{\left|I_{C 43}\right|} \frac{3}{32} \tag{6.166}
\end{equation*}
$$

Solving this equation by trial and error as in a Widlar current mirror gives $\left|I_{C 43}\right|=28 \mu \mathrm{~A}$. As a result, $I_{C 42}=28 \mu \mathrm{~A}$, and the differential input voltage to the $Q_{45}-Q_{46}$ differential pair is

$$
\begin{align*}
V_{B 45}-V_{B 46} & =V_{B E 42}+I_{C 42} R_{42}-V_{B E 75} \\
& =V_{T} \ln \frac{I_{C 42}}{I_{C 75}} \frac{I_{S 75}}{I_{S 42}}+I_{C 42} R_{42} \\
& =(26 \mathrm{mV}) \ln \left(\frac{28}{210} \cdot \frac{10}{1}\right)+(28 \mu \mathrm{~A})(1.3 \mathrm{k} \Omega)=44 \mathrm{mV} \tag{6.167}
\end{align*}
$$

because the ratio of the emitter area of $Q_{75}$ to that of $Q_{42}$ is 10 . From (3.147) and (3.148) with $\alpha_{F}=1$,

$$
\begin{equation*}
\left|I_{C 45}\right|=\frac{\left|I_{C 44}\right|}{1+\exp \frac{V_{B 45}-V_{B 46}}{V_{T}}}=\frac{6 \mu \mathrm{~A}}{1+\exp \frac{44}{26}}=0.93 \mu \mathrm{~A} \tag{6.168}
\end{equation*}
$$

and

$$
\begin{equation*}
\left|I_{C 46}\right|=\frac{\left|I_{C 44}\right|}{1+\exp \frac{V_{B 46}-V_{B 45}}{V_{T}}}=\frac{6 \mu \mathrm{~A}}{1+\exp \frac{-44}{26}}=5.1 \mu \mathrm{~A} \tag{6.169}
\end{equation*}
$$

where $\left|I_{C 46}\right|>\left|I_{C 45}\right|$ because $V_{B 45}>V_{B 46}$.
Finally, with $\left|I_{C 74}\right|=1.2 \mathrm{~mA}$ and $I_{C 75}=210 \mu \mathrm{~A}$, we will recalculate the collector currents of $Q_{64}, Q_{65}$, and $Q_{68}$, taking nonzero base currents into account. Assume $\beta_{F(n p n)}=40$ and $\beta_{F(p n p)}=10$. Then $\left|I_{B 74}\right|=1.2 \mathrm{~mA} / 10=120 \mu \mathrm{~A}$. Therefore,

$$
\begin{equation*}
\left|I_{C 65}\right|=\left(\frac{\beta_{F(p n p)}}{\beta_{F(p n p)}+1}\right)\left(I_{R 65}+\left|I_{B 74}\right|\right)=\left(\frac{10}{11}\right)(100+120) \mu \mathrm{A}=200 \mu \mathrm{~A} \tag{6.170}
\end{equation*}
$$

This equation ignores the base current in $Q_{66}$, which is reasonable because the emitter area of $Q_{66}$ is 32 times smaller than that of $Q_{74}$. Therefore, $\left|I_{B 65}\right|=20 \mu \mathrm{~A}$ and

$$
\begin{equation*}
I_{C 64}=\left(\frac{\beta_{F(n p n)}}{\beta_{F(n p n)}+1}\right)\left(I_{C 63}-\left|I_{B 65}\right|\right)=\left(\frac{40}{41}\right)(33-20) \mu \mathrm{A} \simeq 13 \mu \mathrm{~A} \tag{6.171}
\end{equation*}
$$

Similarly, $I_{B 75}=210 \mu \mathrm{~A} / 40=5.3 \mu \mathrm{~A}$ and

$$
\begin{equation*}
I_{C 68}=\left(\frac{\beta_{F(n p n)}}{\beta_{F(n p n)}+1}\right)\left(I_{C 69}+I_{B 75}\right)=\left(\frac{40}{41}\right)(6+5.3) \mu \mathrm{A} \simeq 11 \mu \mathrm{~A} \tag{6.172}
\end{equation*}
$$

ignoring the base current in $Q_{71}$, which is ten times smaller than $Q_{75}$.
Figure 6.42 shows the relative emitter areas of the transistors in the NE5234 op amp, the dc collector currents calculated above, and the dc collector currents predicted by SPICE simulations under the conditions described above. The calculated collector currents of $Q_{55}$

| Trans. | Rel. <br> Area | $\begin{gathered} I_{C}(\mu \mathrm{~A}) \\ \text { (Calc.) } \end{gathered}$ | $I_{C}(\mu \mathrm{~A})$ <br> (Sim.) | Trans. | Rel. <br> Area | $I_{C}(\mu \mathrm{~A})$ (Calc.) | $I_{C}(\mu \mathrm{~A})$ (Sim.) |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| $Q_{1}$ | 2 | 0 | 0 | $Q_{37}$ | 1 | 7.4 | 7.29 |
| $Q_{1 d}$ | 4 | 0 | 0 | $Q_{38}$ | 1 | -7.4 | -6.79 |
| $Q_{2}$ | 2 | 0 | 0 | $Q_{39}$ | 1 | 9.0 | 8.33 |
| $Q_{2 d}$ | 4 | 0 | 0 | $Q_{40}$ | 1 | 9.0 | 8.48 |
| $Q_{3}$ | 2 | $-3.0$ | -2.65 | $Q_{41}$ | 3 | 18 | 17.2 |
| $Q_{3 d}$ | 4 | 0 | 0 | $Q_{42}$ | 1 | 28 | 27.3 |
| $Q_{4}$ | 2 | $-3.0$ | -2.63 | $Q_{43}$ | 3 | -28 | -27.9 |
| $Q_{4 d}$ | 4 | 0 | 0 | $Q_{44}$ | 1 | -6.0 | -5.79 |
| $Q_{5}$ | 1 | 0 | 0 | $Q_{45}$ | 2 | -0.93 | -0.939 |
| $Q_{6}$ | 1 | 0 | 0 | $Q_{46}$ | 2 | -5.1 | -4.15 |
| $Q_{7}$ | 1 | 0 | 0 | $Q_{47}$ | 1 | -6.0 | -5.76 |
| $Q_{8}$ | 1 | 3.0 | 3.06 | $Q_{48}$ | 1 | -6.0 | -5.25 |
| $Q_{9}$ | 2 | 6.0 | 6.16 | $Q_{49}$ | 1 | 6.0 | 5.74 |
| $Q_{10}$ | 2 | 6.0 | 6.17 | $Q_{50}$ | 1 | -6.0 | -5.80 |
| $Q_{11}$ | 1 | $-6.0$ | -5.81 | $Q_{51}$ | 1 | -6.0 | $-5.01$ |
| $Q_{12}$ | 1 | -3.0 | -3.14 | $Q_{52}$ | 1 | 6.0 | 6.73 |
| $Q_{13}$ | 1 | -6.0 | -5.84 | $Q_{53}$ | 1 | 6.0 | 5.74 |
| $Q_{14}$ | 1 | -6.0 | -5.84 | $Q_{54}$ | 1 | -6.0 | -5.76 |
| $Q_{15}$ | 1 | -3.0 | -3.13 | $Q_{55}$ | 1 | -6.0 | -15.9 |
| $Q_{16}$ | 1 | -4.0 | -4.01 | $Q_{56}$ | 1 | 6.0 | 5.01 |
| $Q_{17}$ | 1 | -21 | -17.6 | $Q_{57}$ | 1 | 6.0 | 5.85 |
| $Q_{18}$ | 1 | -21 | -17.7 | $Q_{58}$ | 1 | -6.0 | -5.76 |
| $Q_{19}$ | 1 | -4.0 | -4.01 | $Q_{59}$ | 1 | 6.0 | 5.64 |
| $Q_{20}$ | 1 | -6.6 | $-6.35$ | $Q_{60}$ | 2 | 6.0 | 5.78 |
| $Q_{21}$ | 1 | -4.0 | -3.25 | $Q_{61}$ | 1 | -6.0 | -5.83 |
| $Q_{22}$ | 1 | -4.0 | -3.38 | $Q_{62}$ | 1 | 6.0 | 5.08 |
| $Q_{23}$ | 1 | 0 | 0 | $Q_{63}$ | 1 | 33 | 25.3 |
| $Q_{24}$ | 1 | 0 | 0 | $Q_{64}$ | 1 | 13 | 5.04 |
| $Q_{25}$ | 1 | 10 | 9.13 | $Q_{65}$ | 8 | -200 | -216 |
| $Q_{26}$ | 1 | 10 | 8.94 | $Q_{66}$ | 1 | -37 | -43.2 |
| $Q_{27}$ | 1 | 10 | 6.19 | $Q_{67}$ | 1 | 0 | 0 |
| $Q_{28}$ | 1 | 10 | 6.19 | $Q_{68}$ | 1 | 11 | 12.0 |
| $Q_{29}$ | 7 | 42 | 34.0 | $Q_{69}$ | 1 | 6.0 | 5.75 |
| $Q_{30}$ | 1 | 6.6 | 5.23 | $Q_{70}$ | 1 | 0 | 0 |
| $Q_{31}$ | 1 | 6.6 | 5.50 | $Q_{71}$ | 1 | 21 | 25.9 |
| $Q_{32}$ | 1 | $-6.6$ | -4.59 | $Q_{72}$ | 3 | 0 | 0 |
| $Q_{33}$ | 1 | $-6.6$ | -4.81 | $Q_{73}$ | 1 | 0 | 0 |
| $Q_{34}$ | 1 | 6.6 | 4.58 | $Q_{74}$ | 32 | -1200 | -1260 |
| $Q_{35}$ | 1 | 6.6 | 4.70 | $Q_{75}$ | 10 | 210 | 264 |
| $Q_{36}$ | 1 | $-14$ | $-12.4$ |  |  |  |  |

Figure 6.42 Relative emitter areas, calculated collector currents, and simulated collector currents of transistors in the NE5234 op amp with $V_{I C} \ll 0.8 \mathrm{~V}$ and $I_{L}=1 \mathrm{~mA}$.
and $Q_{64}$ have large errors. Transistor $Q_{55}$ is an emitter follower that drives the node Bias ${ }_{1}$ in Fig. 6.34. The calculation of $I_{C 55}$ ignores the base currents in all the transistors with bases connected to Bias. This calculation is not repeated here because it makes little difference to the parameters calculated in this book. Similarly, $Q_{64}$ is an emitter follower that drives emitter follower $Q_{65}$ in Fig. 6.39. The error in $I_{C 64}$ stems from the calculation of $I_{C 62}$. Ignoring base currents, $I_{C 62}$ is estimated as $6 \mu \mathrm{~A}$, and $(6.143)$ is solved by trial and error to estimate $I_{C 63}$ as
$33 \mu \mathrm{~A}$. However, the combined base current of $Q_{62}$ and $Q_{63}$ is then $(39 \mu \mathrm{~A}) / \beta_{F(n p n)}$, which is about $1 \mu \mathrm{~A}$ with $\beta_{F(n p n)}=40$. As a result, $I_{C 62}$ is about $5 \mu \mathrm{~A}$ instead of $6 \mu \mathrm{~A}$. When $I_{C 63}$ is recalculated by trial and error from (6.143) with the new value of $I_{C 62}$, the result is $I_{C 63}=24 \mu \mathrm{~A}$. Although the change from $33 \mu \mathrm{~A}$ to $24 \mu \mathrm{~A}$ does not seem large, the collector current of $Q_{64}$ is significantly reduced by this change because it is determined by the difference between two currents. From KCL,

$$
\begin{equation*}
I_{C 64}=\left(\frac{\beta_{F(n p n)}}{\beta_{F(n p n)}+1}\right)\left(I_{C 63}-\left|I_{B 65}\right|\right)=\left(\frac{40}{41}\right)\left(24-\frac{200}{10}\right) \mu \mathrm{A} \simeq 4 \mu \mathrm{~A} \tag{6.173}
\end{equation*}
$$

instead of $13 \mu \mathrm{~A}$ as calculated in (6.171).
Of course, improved estimates of $I_{C 55}$ and $I_{C 64}$ could have been calculated in the first place by including base currents in the original calculations. However, that approach would have added a significant level of complexity to those calculations. In practice, the first level of analysis usually makes broad simplifying assumptions. For example, base currents are normally ignored in dc analysis. Then the results are compared to SPICE simulations, and the comparison may lead to some further calculations including previously ignored parameters, exactly as done here. This approach has the advantage of simplicity. Simplifying analysis is important in practice because design is the inverse of analysis. Simplifying assumptions allow designers to improve designs by quickly repeating analysis under modified conditions. This approach allows designers to focus on parameters that limit performance at every step in the design process.

### 6.8.2 Transistors that Are Normally Off ${ }^{18}$

Consider Fig. 6.36, and assume that the common-mode input voltage is set at a level at which $Q_{1}, Q_{2}$, and $Q_{6}$ operate in the forward-active region. If the differential op-amp input voltage increases, the collector current of $Q_{2}$ increases and that of $Q_{1}$ decreases. Therefore, the voltage from node 2 to ground falls and the voltage from node 1 to ground rises. The key point is that when $Q_{1}$ and $Q_{2}$ operate in the forward-active region, they introduce $180^{\circ}$ of phase shift from their bases to their collectors. Now assume that the common-mode input voltage is raised above $V_{C C}$ by more than a few hundred millivolts so that $Q_{1}$ and $Q_{2}$ saturate. Under this condition, the collector-base junctions of these transistors become forward biased, keeping the collector-base voltages approximately constant. Therefore, increasing the differential op-amp input voltage increases the voltage from node 2 to ground and decreases the voltage from node 1 to ground. In other words, operating the transistors in saturation eliminates the $180^{\circ}$ of phase shift normally introduced. Reversing the polarity of the gain through the input transistors reverses the polarity of the op-amp gain, converting negative feedback to positive feedback and potentially causing instability. A similar problem happens when the common-mode input voltage is lowered below $-V_{E E}$ until $Q_{3}$ and $Q_{4}$ saturate.

This problem occurs at common-mode input voltages beyond the common-mode range. In principle, this problem can be avoided by specifying that the op amp must not operate with common-mode input voltages that saturate any of the input transistors. However, preventing the polarity reversal through circuit design extends the applications in which the op amp can be used.

Figure 6.43 shows a schematic of part of the NE5234 input stage with transistors $Q_{1 d}, Q_{2 d}$, $Q_{3 d}$, and $Q_{4 d}$, which were omitted from Fig. 6.36 for simplicity. The base-emitter junctions of these transistors are short circuited; therefore, each of these transistors operates as a diode between its collector and base. When $Q_{1}$ and $Q_{2}$ saturate, their collector-base junctions become forward biased. The base of $Q_{1 d}$ is connected to the base of $Q_{1}$. The base of $Q_{2 d}$ is connected to the base of $Q_{2}$. The collectors of $Q_{1 d}$ and $Q_{2 d}$ are connected to the collectors of $Q_{2}$ and $Q_{1}$, respectively. Therefore, with perfect matching and a pure common-mode input voltage,
image_name:Figure 6.43
description:The circuit is a partial schematic of the NE5234 input stage with diodes in both differential pairs. It uses transistors and resistors to manage biasing and signal processing, with matched transistor pairs and specific area ratios to prevent polarity reversal.

Figure 6.43 Partial schematic of the NE5234 input stage with diodes in both differential pairs.
Transistors $Q_{9}, Q_{10}, Q_{13}$, and $Q_{14}$ and their degeneration resistors have been omitted for simplicity.
$V_{B C 1}=V_{B C 1 d}=V_{B C 2}=V_{B C 2 d}$, and the collector-base junctions of these four transistors are equally biased. To prevent the polarity reversal described above, $Q_{1 d}$ and $Q_{2 d}$ have larger areas than $Q_{1}$ and $Q_{2}$. (In the NE5234 op amp, the area ratio is 2.) Then when the collector-base junctions become forward biased, the collector-base junctions of $Q_{1 d}$ and $Q_{2 d}$ conduct more current than those of $Q_{1}$ and $Q_{2}$. Therefore, changes in the noninverting op-amp input voltage exert more influence on node 1 than on node 2 , and changes in the inverting op-amp input voltage exert more influence on node 2 than on node 1 . As a result, when the differential op-amp input voltage increases, the voltage from node 1 to ground rises, and the voltage from node 2 to ground falls, as in normal operation. Similar statements apply to the pnp differential pair. This circuit allows the common-mode input voltage to range from about 700 mV above $V_{C C}$ to about 700 mV below $-V_{E E}$. In the top and bottom few hundred millivolts of this range, transistors in the input stage operate in saturation, and some op-amp specifications are not met. However, the polarity of the op-amp gain is not reversed in this range. Beyond this range, damage to transistors $Q_{1 d}, Q_{2 d}, Q_{3 d}$, and $Q_{4 d}$ could occur. Resistors in series with each op-amp input can be added to avoid damage by limiting the current that flows in the diodes when they turn on. ${ }^{14}$

Transistors $Q_{23}$ and $Q_{24}$ in Fig. 6.37 are normally off. Their bases are connected to node $\mathrm{Bias}_{2}$, which is an output of the bias circuit in Fig. 6.40. The voltage from Bias ${ }_{2}$ to ground is $V_{E B 38} \simeq 0.7 \mathrm{~V}$. Therefore, if the voltage from node 9 to ground or node 10 to ground rises to about 1.4 V when a large differential voltage is provided to the op-amp inputs, $Q_{23}$ or $Q_{24}$ turn on to prevent further increases in these voltages. This limitation is important to avoid saturating $Q_{16}$ and $Q_{19}$, reducing the delay required to properly handle a sudden reduction in the magnitude of the differential op-amp input voltage.

Transistors $Q_{67}$ and $Q_{70}$ in Fig. 6.39 are normally off. These transistors turn on to limit $\left|I_{L}\right|$ to prevent destruction of $Q_{74}$ and $Q_{75}$. For example, if $Q_{67}$ is off, its base-emitter voltage is

$$
\begin{equation*}
V_{B E 67}=\left|I_{C 66}\right| R_{67}-I_{C 63} R_{63} \tag{6.174}
\end{equation*}
$$

Transistor $Q_{67}$ turns on when $V_{B E 67}=V_{B E(\mathrm{on})}$. Rearranging (6.174) with this condition gives

$$
\begin{equation*}
\left|I_{C 66}\right|=\frac{V_{B E(\mathrm{on})}}{R_{67}}+I_{C 63}\left(\frac{R_{63}}{R_{67}}\right)=\frac{0.7 \mathrm{~V}}{1.5 \mathrm{k} \Omega}+33 \mu \mathrm{~A}\left(\frac{1.2 \mathrm{k} \Omega}{1.5 \mathrm{k} \Omega}\right)=490 \mu \mathrm{~A} \tag{6.175}
\end{equation*}
$$

Since the emitter area of $Q_{74}$ is thirty-two times larger than that of $Q_{66}, Q_{67}$ turns on when

$$
\begin{equation*}
\left|I_{C 74}\right|=32(490 \mu \mathrm{~A})=16 \mathrm{~mA} \tag{6.176}
\end{equation*}
$$

Once $Q_{67}$ turns on, it raises the voltage across $R_{63}$, decreasing $I_{C 63}$. This change reduces the ability of $Q_{63}$ to pull down on the base of $Q_{65}$, which then limits the ability of $Q_{65}$ to pull down on the base of $Q_{74}$. As a result, the maximum $\left|I_{C 74}\right|$ is limited to about 16 mA .

Similar reasoning applies to limiting the current in $Q_{75}$. The current is sensed by $Q_{71}$. When $I_{C 71}$ is large enough, $Q_{70}$ turns on and pulls down on the emitter of $Q_{18}$ in Fig. 6.37. This change reduces $\left|I_{C 18}\right|$, limiting the current that it can provide to pull up on node 26, thereby limiting $I_{C 75}$. See Problem 6.25.

Transistors $Q_{72}$ and $Q_{73}$ in Fig. 6.39 are normally off. Their purpose is to limit the extent to which $Q_{74}$ and $Q_{75}$ can saturate. ${ }^{21}$ This limitation is important because allowing either output transistor to thoroughly saturate fills its base region with minority carriers and increases the delay required to drive the output in the other direction, worsening crossover distortion.

If $Q_{74}$ begins to saturate, its collector-base junction becomes forward biased. As a result, the collector-base junction of $Q_{72}$ also becomes forward biased. Since the voltage from node 25 to ground is level shifted down about 0.7 V by $Q_{64}$ and up about the same amount by $Q_{65}$, $V_{E B 72} \simeq 0$. Therefore, $Q_{72}$ operates in the reverse-active mode when $Q_{74}$ begins to saturate. In this mode, the current in $Q_{72}$ flows into its collector, out its emitter, and into node 25. This current raises the voltage from node 25 to ground, which reduces the output voltage and the extent to which $Q_{74}$ saturates. Similarly, when $Q_{75}$ begins to saturate, its base-collector junction becomes forward biased, which forward biases the base-collector junction of $Q_{73}$. This transistor then operates in the reverse-active region, pulling current out of node 26 to reduce the voltage from node 26 to ground and limit the extent of the saturation in $Q_{75}$.

### 6.8.3 Small-Signal Analysis of the NE5234 Operational Amplifier

Our next objective is to determine the small-signal properties of the amplifier. We will break the circuit up into its three stages-the input stage, second stage, and output stage-and analyze each. In this section, we will assume that $\beta_{0(n p n)}=40, \beta_{0(p n p)}=10, V_{A(n p n)}=30 \mathrm{~V}$, and $V_{A(p n p)}=20 \mathrm{~V}$ unless otherwise stated. These numbers are estimates of the minimum values that occur in practice.

Input Stage. The input stage of the NE5234 op amp is a fully differential circuit with two emitter-coupled pairs, and the input resistance depends on which pair or pairs are conducting. Assume that $V_{I C} \ll 0.8 \mathrm{~V}$. Then the $n p n$ pair $Q_{1-} Q_{2}$ is off, and $Q_{11}$ biases the pnp pair $Q_{3}-Q_{4}$. Figure 6.44 shows the differential-mode half circuit under this condition. The load resistance is $R_{\text {in2 }} / 2$, which is half the input resistance of the second stage. Since the emitter of $Q_{3}$ operates at a small-signal ground, the input resistance of the differential-mode half circuit is $r_{\pi 3}$, as shown in Fig. 3.56. From (3.195), the differential input resistance is

$$
\begin{equation*}
R_{i d}=2 r_{\pi 3} \tag{6.177}
\end{equation*}
$$

Since $\left|I_{C 11}\right|=6 \mu \mathrm{~A},\left|I_{C 3}\right|=\left|I_{C 4}\right|=3 \mu \mathrm{~A}$, and

$$
\begin{equation*}
R_{i d}=2\left(\frac{\beta_{0(p n p)}}{g_{m 3}}\right)=2\left(\frac{\beta_{0(p n p)}}{\left|I_{C 3}\right|}\right) V_{T}=2\left(\frac{10}{3 \mu \mathrm{~A}}\right) 26 \mathrm{mV}=170 \mathrm{k} \Omega \tag{6.178}
\end{equation*}
$$

image_name:Figure 6.44
description:
[
name: Q3, type: PNP, ports: {C: GND, B: Vb, E: c3e9}
name: Q13, type: PNP, ports: {C: e13, B: GND, E: GND}
name: Q9, type: NPN, ports: {C: 9, B: 3, E: GND}
name: R13, type: Resistor, value: 33kΩ, ports: {N1: e13, N2: GND}
name: R9, type: Resistor, value: 22kΩ, ports: {N1: 3, N2: GND}
]
extrainfo:The circuit is a differential-mode half circuit of the input stage with a differential-mode input. Q9 and Q13 operate as common-base amplifiers. The differential input resistance is calculated as 170 kΩ.

Figure 6.44 Differential-mode half circuit of the input stage with $V_{I C} \ll 0.8 \mathrm{~V}$.

With a pure differential-mode input, the bases of $Q_{9}$ and $Q_{13}$ also operate as small-signal grounds, as shown in Fig. 6.44. As a result, $Q_{9}$ and $Q_{13}$ are common-base amplifiers. From the term in brackets in (3.61), the output resistance looking up into the collector of $Q_{13}$ is

$$
\begin{equation*}
R_{\mathrm{up} 1}=\frac{r_{o 13}+R_{13}\left(1+\frac{g_{m 13} r_{o 13}\left(\beta_{0(p n p)}+1\right)}{\beta_{0(p n p)}}\right)}{1+\frac{g_{m 13} R_{13}}{g_{m 13} r_{\pi 13}}} \simeq \frac{r_{o 13}\left(1+g_{m 13} R_{13} \frac{\beta_{0(p n p)}+1}{\beta_{0(p n p)}}\right)}{1+\frac{g_{m 13} R_{13}}{\beta_{0(p n p)}}} \tag{6.179}
\end{equation*}
$$

because $R_{13} \ll r_{o 13}$. Then,

$$
\begin{equation*}
R_{\mathrm{up} 1}=\frac{\frac{20 \mathrm{~V}}{6 \mu \mathrm{~A}}\left[1+\left(\frac{6 \mu \mathrm{~A}}{26 \mathrm{mV}}\right) 33 \mathrm{k} \Omega\left(\frac{11}{10}\right)\right]}{1+\frac{\left(\frac{6 \mu \mathrm{~A}}{26 \mathrm{mV}}\right) 33 \mathrm{k} \Omega}{10}}=18 \mathrm{M} \Omega \tag{6.180}
\end{equation*}
$$

Similarly, if the resistance looking back into the collector of $Q_{3}$ is much greater than $R_{9}$, the output resistance looking down into the collector of $Q_{9}$ is

$$
\begin{equation*}
R_{\mathrm{down} 1} \simeq \frac{r_{o 9}\left(1+g_{m 9} R_{9} \frac{\beta_{0(n p n)}+1}{\beta_{0(n p n)}}\right)}{1+\frac{g_{m 9} R_{9}}{\beta_{0(n p n)}}} \simeq \frac{r_{o 9}\left(1+g_{m 9} R_{9}\right)}{1+\frac{g_{m 9} R_{9}}{\beta_{0(n p n)}}} \tag{6.181}
\end{equation*}
$$

because $R_{9} \ll r_{o 9}$ and $\beta_{0(n p n)}+1 \simeq \beta_{0(n p n)}$. Then,

$$
\begin{equation*}
R_{\mathrm{down} 1} \simeq \frac{\frac{30 \mathrm{~V}}{6 \mu \mathrm{~A}}\left[1+\left(\frac{6 \mu \mathrm{~A}}{26 \mathrm{mV}}\right) 22 \mathrm{k} \Omega\right]}{1+\frac{\left(\frac{6 \mu \mathrm{~A}}{26 \mathrm{mV}}\right) 22 \mathrm{k} \Omega}{40}}=27 \mathrm{M} \Omega \tag{6.182}
\end{equation*}
$$

Therefore, the output resistance of the first stage is

$$
\begin{equation*}
R_{o 1}=R_{\mathrm{up} 1}\left\|R_{\mathrm{down} 1}=18 \mathrm{M} \Omega\right\| 27 \mathrm{M} \Omega=11 \mathrm{M} \Omega \tag{6.183}
\end{equation*}
$$

The transconductance of the input stage is

$$
\begin{equation*}
G_{m 1}=g_{m 3} \rho_{3} \tag{6.184}
\end{equation*}
$$

where $g_{m 3}$ is the transconductance of $Q_{3}$ and $\rho_{3}$ represents the fraction of the small-signal collector current in $Q_{3}$ that flows into the emitter of $Q_{9}$. As in (6.124),

$$
\begin{equation*}
\rho_{3} \simeq \frac{R_{9}}{R_{9}+r_{e 9}}=\frac{R_{9}}{R_{9}+\left(\frac{\beta_{0(n p n)}}{\beta_{0(n p n)}+1}\right) \frac{V_{T}}{I_{C 9}}}=\frac{22 \mathrm{k} \Omega}{22 \mathrm{k} \Omega+\left(\frac{40}{41}\right) \frac{26 \mathrm{mV}}{6 \mu \mathrm{~A}}}=0.84 \tag{6.185}
\end{equation*}
$$

Therefore,

$$
\begin{equation*}
G_{m 1}=\left(\frac{\left|I_{C 3}\right|}{V_{T}}\right) \rho_{3}=\left(\frac{3 \mu \mathrm{~A}}{26 \mathrm{mV}}\right) 0.84=97 \frac{\mu \mathrm{~A}}{\mathrm{~V}} \tag{6.186}
\end{equation*}
$$

As pointed out in Section 6.8.1, the transconductance of the input stage does not depend on the common-mode input voltage.

Second Stage. Since nodes 9 and 10 move equally but in opposite directions with a pure differential input, the emitters of $Q_{25}-Q_{28}$ operate at a small-signal ground. Therefore, the resistance looking in the second stage (Fig. 6.37) is

$$
\begin{equation*}
R_{i 2}=2\left[r_{\pi 21}+\left(\beta_{0(p n p)}+1\right)\left(r_{\pi 25} \| r_{\pi 26}\right)\right] \tag{6.187}
\end{equation*}
$$

assuming the resistance looking into the collector of $Q_{16}$ is much bigger than $r_{\pi 25} \| r_{\pi 26}$. Since $r_{\pi 25}=r_{\pi 26}=\beta_{0(n p n)} / g_{m 25}$,

$$
\begin{align*}
R_{i 2} & =2\left[\frac{\beta_{0(p n p)}}{g_{m 21}}+\frac{\beta_{0(p n p)}+1}{2}\left(\frac{\beta_{0(n p n)}}{g_{m 25}}\right)\right] \\
& =2\left[\frac{10(26 \mathrm{mV})}{4 \mu \mathrm{~A}}+\frac{11}{2}\left(\frac{40(26 \mathrm{mV})}{10 \mu \mathrm{~A}}\right)\right]=1.3 \mathrm{M} \Omega \tag{6.188}
\end{align*}
$$

To find the stage output resistance, we first calculate the resistance looking up into the collector of $Q_{17}$ or $Q_{18}$, which is $R_{\text {up } 2}$. Since these transistors can be viewed as operating as common-base amplifiers, the term in brackets in (3.61) can be used to give

$$
\begin{equation*}
R_{\mathrm{up} 2}=\frac{r_{o 17}+R_{17}\left(1+\frac{g_{m 17} r_{017}\left(\beta_{0(p n p)}+1\right)}{\beta_{0(p n p)}}\right)}{1+\frac{g_{m 17} R_{17}}{g_{m 17} r_{\pi 17}}} \simeq \frac{r_{o 17}\left(1+g_{m 17} R_{17} \frac{\beta_{0(p n p)}+1}{\beta_{0(p n p)}}\right)}{1+\frac{g_{m 17} R_{17}}{\beta_{0(p n p)}}} \tag{6.189}
\end{equation*}
$$

because $R_{17} \ll r_{o 17}$. Then,

$$
\begin{equation*}
R_{\mathrm{up} 2}=\frac{\frac{20 \mathrm{~V}}{21 \mu \mathrm{~A}}\left[1+\left(\frac{21 \mu \mathrm{~A}}{26 \mathrm{mV}}\right) 9.3 \mathrm{k} \Omega\left(\frac{11}{10}\right)\right]}{1+\frac{\left(\frac{21 \mu \mathrm{~A}}{26 \mathrm{mV}}\right) 9.3 \mathrm{k} \Omega}{10}}=5.0 \mathrm{M} \Omega \tag{6.190}
\end{equation*}
$$

Now looking down into the collector of $Q_{25}$ or $Q_{26}$, we see

$$
\begin{equation*}
R_{\text {down } 2}=r_{o 25}\left(1+g_{m 25} R_{E 25}\right) \tag{6.191}
\end{equation*}
$$

where $R_{E 25}$ is the small-signal resistance looking away from the emitter of $Q_{25}$. Assuming that the resistance looking into the collector of $Q_{29}$ is high enough to be ignored, $R_{E 25}$ is the resistance looking into the emitters of $Q_{26} Q_{28}$. Since the collectors of $Q_{27}$ and $Q_{28}$ are connected to a small-signal ground ( $V_{C C}$ ), the resistance looking into each of their emitters is just $r_{e 27}=r_{e 28}$ from (3.53) with $R_{C}=0$. However, for $Q_{26}$, the calculation is more complicated than for $Q_{27}$ or $Q_{28}$ because the resistance connected to the collector of $Q_{26}$ can be large. Let $R_{\text {in3(26) }}$ represent the input resistance of the third stage at node 26 . Then from (3.53),

$$
\begin{equation*}
R_{E 25}=\left[r_{e 26}+\left(\frac{\beta_{0(n p n)}}{\beta_{0(n p n)}+1}\right) \frac{\left(R_{\text {up } 2} \| R_{\text {in3(26) }}\right)}{g_{m 26} r_{o 26}}\right]\left\|r_{e 27}\right\| r_{e 28} \tag{6.192}
\end{equation*}
$$

If $R_{\text {in3(26) }} /\left(g_{m 26} r_{o 26}\right) \ll r_{e 26}$, which turns out to be true with the small value of $\beta_{0(n p n)}$ assumed here, then

$$
\begin{align*}
R_{E 25} & \simeq\left(\frac{\beta_{0(n p n)}}{\beta_{0(n p n)}+1}\right)\left[\frac{1}{g_{m 26}}\left\|\frac{1}{g_{m 27}}\right\| \frac{1}{g_{m 28}}\right] \\
& =\left(\frac{40}{41}\right)\left[\frac{26 \mathrm{mV}}{10 \mu \mathrm{~A}}\left\|\frac{26 \mathrm{mV}}{10 \mu \mathrm{~A}}\right\| \frac{26 \mathrm{mV}}{10 \mu \mathrm{~A}}\right]=0.85 \mathrm{k} \Omega \tag{6.193}
\end{align*}
$$

Substituting this result into (6.191) gives

$$
\begin{equation*}
R_{\text {down } 2}=\frac{30 \mathrm{~V}}{10 \mu \mathrm{~A}}\left[1+\left(\frac{10 \mu \mathrm{~A}}{26 \mathrm{mV}}\right) 0.85 \mathrm{k} \Omega\right]=4.0 \mathrm{M} \Omega \tag{6.194}
\end{equation*}
$$

As a result, the output resistance of the second stage looking back into node 25 is

$$
\begin{equation*}
R_{o 2}=R_{\mathrm{up} 2}\left\|R_{\mathrm{down} 2}=5.0 \mathrm{M} \Omega\right\| 4.0 \mathrm{M} \Omega=2.2 \mathrm{M} \Omega \tag{6.195}
\end{equation*}
$$

Let $R_{\text {in3(25) }}$ represent the input resistance of the third stage at node 25 . If $R_{\text {in3(25) }} \simeq R_{\text {in3(26) }}$, then (6.195) also gives the output resistance of the second stage looking back into node 26.

Figure 6.45 shows a small-signal model of the second stage for finding its transconductance. The resistors labeled $R_{\text {up } 2}$ represent the small-signal resistance looking into the collector of $Q_{17}$ or $Q_{18}$ in Fig. 6.37. As shown in (6.190), these resistances are $5 \mathrm{M} \Omega$ each. The resistances labeled $R_{\mathrm{in} 3(25)}$ and $R_{\mathrm{in} 3(26)}$ are the input resistances of the third stage from nodes 25 and 26 , respectively. Let $v_{9}, v_{10}$, and $v_{25}$ represent the small-signal voltages to ground from nodes 9,10 , and 25 , respectively. The emitters of $Q_{25}-Q_{28}$ are floating in Fig. 6.45 because $Q_{29}$ in Fig. 6.37 operates as a current source with an output resistance that is much higher than the resistances looking into the emitters of $Q_{25}-Q_{28}$. Let $a_{v 21}$ and $a_{v 22}$ represent the small-signal
image_name:Figure 6.45
description:The circuit is a small-signal model of the second stage to find its transconductance. It includes resistors Rup2 and Rin3, NPN transistors Q25-Q28, and voltage sources av21v9 and av22v10. The emitters of Q25-Q28 are floating due to a high output resistance of a current source not shown in the diagram.

Figure 6.45 Small-signal model of second stage to find its transconductance.
gains of emitter followers $Q_{21}$ and $Q_{22}$ in Fig. 6.37, respectively. Each emitter follower drives a load of $R_{L}=r_{\pi 25}\left\|r_{\pi 26}=r_{\pi 27}\right\| r_{\pi 28}=r_{\pi 25} / 2$. From (3.69) with $R_{S}=0$,

$$
\begin{align*}
& a_{v 21}=a_{v 22}=\frac{1}{1+\frac{r_{\pi 21}}{\left(\beta_{0(p n p)}+1\right)\left[\left(r_{\pi 25} / 2\right) \| r_{o 21}\right]}} \\
& =\frac{1}{1+\frac{\frac{10(26 \mathrm{mV})}{4 \mu \mathrm{~A}}}{(11)\left[\left(\frac{40(26 \mathrm{mV})}{2(10 \mu \mathrm{~A})}\right) \|\left(\frac{20 \mathrm{~V}}{4 \mu \mathrm{~A}}\right)\right]}}=0.90 \tag{6.196}
\end{align*}
$$

The transconductance of the second stage is

$$
\begin{equation*}
G_{m 2}=\left.\frac{i_{o}}{v_{9}-v_{10}}\right|_{v_{25}=0} \tag{6.197}
\end{equation*}
$$

Because the common-mode output voltage of the first stage is set to a constant as shown in Fig. $6.38, v_{9}=v_{o d 1} / 2$ and $v_{10}=-v_{o d 1} / 2$, where $v_{o d 1}$ is the small-signal differential output voltage of the first stage. For simplicity in finding the stage transconductance, assume that $v_{10}=0$. This change introduces a nonzero common-mode input voltage to the second stage. However, this common-mode input causes a negligible change in $G_{m 2}$ because the tail current source $Q_{29}$ has high output resistance. Setting $v_{10}=0$ also halves the differential input voltage to the second stage. However, since the small-signal model is linear, halving the input voltage halves $i_{o}$ but does not change $G_{m 2}$. As a result,

$$
\begin{equation*}
G_{m 2}=\left.\frac{i_{o}}{v_{9}}\right|_{v_{25}=0} \tag{6.198}
\end{equation*}
$$

Since the circuit is linear from a small-signal standpoint, superposition can be used to find $i_{o}$. Figure 6.46 shows the circuit configuration to find the first component of $i_{o}$. The bases of $Q_{25}$ and $Q_{26}$ are driven separately, and the base of $Q_{26}$ is connected to a small-signal ground here. The resistances connected to node 25 are removed because zero small-signal current flows in them. To find $i_{o 1}, Q_{25}$ is viewed as a common-emitter amplifier with degeneration. The small-signal resistance looking away from the emitter of $Q_{25}$ is $R_{E 25}=0.85 \mathrm{k} \Omega$ as shown in (6.193). From (3.93),

$$
\begin{equation*}
i_{o 1}=\frac{g_{m 25}}{1+g_{m 25} R_{E 25}} a_{v 21} v_{9} \tag{6.199}
\end{equation*}
$$

Figure 6.47 shows the circuit configuration to find the second component of $i_{o}$. Here the base of $Q_{25}$ is connected to small-signal ground. To find $i_{c 26}, Q_{26}$ is viewed as another

image_name:Figure 6.47
description:The circuit is a small-signal model for analyzing the second component of the output current io. It is a common-emitter amplifier with degeneration using multiple NPN transistors. The small-signal resistance looking away from the emitter of Q25 is RE25 = 0.85 kΩ. The small-signal resistance looking away from the emitter of Q26 is given by RE26 = r_e25 || r_e27 || r_e28 = r_e25 / 3 = 0.85 kΩ.

Figure 6.47 Small-signal model to find the second component of $i_{o}$.
common-emitter amplifier with degeneration. The small-signal resistance looking away from the emitter of $Q_{26}$ is

$$
\begin{equation*}
R_{E 26}=r_{e 25}\left\|r_{e 27}\right\| r_{e 28}=r_{e 25} / 3=0.85 \mathrm{k} \Omega \tag{6.200}
\end{equation*}
$$

From (3.99), the small-signal resistance looking down into the collector of $Q_{26}$ is

$$
\begin{equation*}
R_{C 26}=r_{o 26}\left(1+g_{m 26} R_{E 26}\right)=\frac{30 \mathrm{~V}}{10 \mu \mathrm{~A}}\left[1+\left(\frac{10 \mu \mathrm{~A}}{26 \mathrm{mV}}\right) 0.85 \mathrm{k} \Omega\right]=4.0 \mathrm{M} \Omega \tag{6.201}
\end{equation*}
$$

To find the small-signal collector current in $Q_{26}$, (3.93) can be used along with a fraction to account for the current divider at the collector of $Q_{26}$ :

$$
\begin{equation*}
i_{c 26} \simeq \frac{g_{m 26}}{1+g_{m 26} R_{E 26}} a_{v 21} v_{9}\left(\frac{R_{C 26}}{R_{C 26}+R_{\mathrm{up} 2}| | R_{\mathrm{in} 3(26)}}\right) \simeq \frac{g_{m 26}}{1+g_{m 26} R_{E 26}} a_{v 21} v_{9} \tag{6.202}
\end{equation*}
$$

where $R_{\text {in3(26) }} \ll R_{C 26}$ is assumed in the last approximation. Since $\beta_{0(n p n)} r_{o 26} \gg R_{E 26}$ and $g_{m 26} r_{o 26} \gg 1$, this equation ignores the terms involving $r_{o}$ in (3.92). Also, the $1 / \beta_{0}$ term there is ignored here as well as in the rest of the calculation of $G_{m 2}$ for simplicity.

Since $Q_{25}, Q_{27}$, and $Q_{28}$ are identical and their bases and collectors are all connected to small-signal grounds, $i_{c 26}$ splits into three equal parts. Therefore, ignoring base currents, $i_{o 2}$ is

$$
\begin{equation*}
i_{o 2} \simeq-i_{c 26} / 3 \tag{6.203}
\end{equation*}
$$

Since $i_{o}=i_{o 1}+i_{o 2}$,

$$
\begin{align*}
G_{m 2} & \simeq a_{v 21}\left(\frac{g_{m 25}}{1+g_{m 25} R_{E 25}}-\frac{g_{m 26}}{3\left(1+g_{m 26} R_{E 26}\right)}\right) \\
& =0.9\left\{\frac{\frac{10 \mu \mathrm{~A}}{26 \mathrm{mV}}}{1+\left(\frac{10 \mu \mathrm{~A}}{26 \mathrm{mV}}\right) 0.85 \mathrm{k} \Omega}-\frac{\frac{10 \mu \mathrm{~A}}{26 \mathrm{mV}}}{3\left[1+\left(\frac{10 \mu \mathrm{~A}}{26 \mathrm{mV}}\right) 0.85 \mathrm{k} \Omega\right]}\right\} \\
& \simeq 170 \frac{\mu \mathrm{~A}}{\mathrm{~V}} \tag{6.204}
\end{align*}
$$

This transconductance is calculated to the output at node 25 , but it also applies to the output at node 26 as long as $R_{\mathrm{in3(25)}} \simeq R_{\mathrm{in3} 3(26)}$. When $\left|I_{C 74}\right| \gg I_{C 75}$ or $\left|I_{C 74}\right| \ll I_{C 75}$, feedback biasing in the output stage doubles this transconductance for the path that drives the output, as described below.

Output Stage. In Section 6.8.1, we assumed that $I_{L}=1 \mathrm{~mA}$. In this case, the bias circuit for the output stage regulates the collector current in $Q_{75}$ to be almost constant. Since $Q_{75}$ is driven by emitter follower $Q_{68}$, the base current for $Q_{68}$ must be approximately constant
image_name:Fig. 6.48
description:The circuit is a differential amplifier with two stages. The first stage is formed by transistors Q25 and Q26, and the second stage is formed by Q27 and Q28. The biasing of the circuit is achieved using resistors R_up2 and voltage sources av21 and av22. The output is taken from nodes 25 and 26, with feedback control via transistors Q39 and Q40.The diagram represents the small-signal model of the interaction between the second stage and the differential pair in a differential amplifier circuit. It focuses on the control of the output stage by the differential pair Q39-Q40. The outputs are taken from nodes 25 and 26, which drive the bases of transistors in the subsequent stage.
$Q_{39}-Q_{40}$ in the bias circuit for the third stage when $I_{C 75}$ is almost constant.
under this condition. To explain this result, consider Fig. 6.48, which shows a small-signal model of the key part of the second stage plus differential pair $Q_{39-} Q_{40}$ from the bias circuit that controls the output stage. The outputs of this model are nodes 25 and 26 , which drive the bases of $Q_{64}$ and $Q_{68}$ in Fig. 6.39.

First consider the second stage. The two outputs are driven by matched circuits in the second stage, and the loading placed on these two nodes in the third stage is almost identical. Therefore, the small-signal currents drawn into nodes 25 and 26 from the second stage are almost identical and labeled as $i$ in Fig. 6.48.

Now consider differential pair $Q_{39}-Q_{40}$. This pair forms the input of a differential amplifier that operates in a negative feedback loop and keeps $I_{C 75}$ almost constant when $\left|I_{C 74}\right| \gg$ $I_{C 75}$, as described in Section 6.8.1. The base of $Q_{39}$ is connected to a small-signal ground in Fig. 6.48 because the collector currents of $Q_{37}$ and $Q_{38}$ in Fig. 6.40 are constant. On the other hand, the base of $Q_{40}$ is driven by $v_{b 40}$, which is the small-signal voltage from the base of $Q_{40}$ to ground. Since $Q_{75}$ is driven by $Q_{68}$, keeping $I_{C 75}$ constant means that the small-signal base current of $Q_{68}, i_{b 68}$, is approximately zero. Therefore, $Q_{40}$ must inject a small-signal current of $i$ into node 26 under these conditions, as shown in Fig. 6.48. Since the total current in the differential pair is constant, $Q_{39}$ pulls the same current $i$ out of node 25 . This result doubles the small-signal base current of $Q_{64}, i_{b 64}$, to $2 i$, effectively doubling $G_{m 2}$ to node 25 and setting $G_{m 2}$ to node 26 to approximately zero when $\left|I_{C 74}\right| \gg I_{C 75}$. Therefore, in the analysis of the output stage below, we will focus on the path from node 25 to the output. In the opposite case (when $\left|I_{C 74}\right| \ll I_{C 75}$ ), the path from node 26 to the output is dominant. When $\left|I_{C 74}\right| \simeq I_{C 75}$, both paths must be considered.

Ignoring the resistance looking down into the collector of $Q_{39}$, the input resistance of the third stage (Fig. 6.39) at node 25 is

$$
\begin{equation*}
R_{i 3(25)}=r_{\pi 64}+\left(\beta_{0(n p n)}+1\right) R_{E 64} \tag{6.205}
\end{equation*}
$$

In this equation, $R_{E 64}$ is the incremental resistance from the emitter of $Q_{64}$ to small-signal ground, which is

$$
\begin{equation*}
R_{E 64}=\left[r_{o 63}\left(1+g_{m 63} R_{63}\right)\right]| |\left[r_{\pi 65}+\left(\beta_{0(p n p)}+1\right) R_{E 65}\right] \tag{6.206}
\end{equation*}
$$

Similarly, $R_{E 65}$ is the incremental resistance from the emitter of $Q_{65}$ to small-signal ground. Ignoring the resistance looking into the base of $Q_{43}$ in Fig. 6.40, $R_{E 65}$ is

$$
\begin{equation*}
R_{E 65}=R_{65}\left\|r_{\pi 66}| | r_{\pi 74}=R_{65}| | \frac{\beta_{0(p n p)} V_{T}}{\left|I_{C 66}\right|}\right\| \frac{\beta_{0(p n p)} V_{T}}{\left|I_{C 74}\right|} \tag{6.207}
\end{equation*}
$$

Since the emitter area of $Q_{74}$ is thirty-two times larger than that of $Q_{66}$,

$$
\begin{equation*}
\left|I_{C 66}\right|=\left|I_{C 74}\right| / 32=1200 \mu \mathrm{~A} / 32=37 \mu \mathrm{~A} \tag{6.208}
\end{equation*}
$$

So

$$
\begin{equation*}
R_{E 65}=7.5 \mathrm{k} \Omega\left\|\frac{10(26 \mathrm{mV})}{37 \mu \mathrm{~A}}\right\| \frac{10(26 \mathrm{mV})}{1200 \mu \mathrm{~A}}=200 \Omega \tag{6.209}
\end{equation*}
$$

Then

$$
\begin{equation*}
R_{E 64}=\left[\frac{30 \mathrm{~V}}{33 \mu \mathrm{~A}}\left(1+\frac{33 \mu \mathrm{~A}}{26 \mathrm{mV}} 1.2 \mathrm{k} \Omega\right)\right] \|\left[\frac{10(26 \mathrm{mV})}{200 \mu \mathrm{~A}}+(11) 200 \Omega\right]=3.5 \mathrm{k} \Omega \tag{6.210}
\end{equation*}
$$

Finally, from (6.205) with $I_{C 64}=4 \mu \mathrm{~A}$ as calculated in (6.173),

$$
\begin{equation*}
R_{i 3(25)}=\frac{40(26 \mathrm{mV})}{4 \mu \mathrm{~A}}+(41) 3.5 \mathrm{k} \Omega=404 \mathrm{k} \Omega \tag{6.211}
\end{equation*}
$$

The output resistance of the stage is

$$
\begin{equation*}
R_{o 3}=r_{o 74}\left\|r_{o 75}=\frac{20 \mathrm{~V}}{1200 \mu \mathrm{~A}}\right\| \frac{30 \mathrm{~V}}{210 \mu \mathrm{~A}}=15 \mathrm{k} \Omega \tag{6.212}
\end{equation*}
$$

The transconductance of the stage is

$$
\begin{equation*}
G_{m 3}=a_{v 64} a_{v 65} g_{m 74} \tag{6.213}
\end{equation*}
$$

where $a_{v 64}$, and $a_{v 65}$ are the gains of emitter followers $Q_{64}$ and $Q_{65}$, respectively.
Since $r_{o 64} \gg R_{E 64},(3.69)$ gives

$$
\begin{equation*}
a_{v 64}=\frac{1}{1+\frac{r_{\pi 64}}{\left(\beta_{0(n p n)}+1\right) R_{E 64}}}=\frac{1}{1+\frac{40(26 \mathrm{mV})}{41(3.5 \mathrm{k} \Omega)}}=0.36 \tag{6.214}
\end{equation*}
$$

Since $r_{065} \gg R_{E 65},(3.69)$ gives

Therefore,

$$
\begin{equation*}
G_{m 3}=0.36(0.63)\left(\frac{1200 \mu \mathrm{~A}}{26 \mathrm{mV}}\right)=\frac{1}{96 \Omega} \tag{6.216}
\end{equation*}
$$

Overall Gain. The voltage gain of the input stage when loaded by the second stage is

$$
\begin{equation*}
a_{v 1}=G_{m 1}\left(R_{o 1} \| \frac{R_{i 2}}{2}\right)=97 \frac{\mu \mathrm{~A}}{\mathrm{~V}}\left(11 \mathrm{M} \Omega \| \frac{1.3 \mathrm{M} \Omega}{2}\right)=60 \tag{6.217}
\end{equation*}
$$

The voltage gain of the second stage when loaded by the third stage is

$$
\begin{equation*}
a_{v 2}=2 G_{m 2}\left(R_{o 2} \| R_{i 3(25)}\right)=2 \times 170 \frac{\mu \mathrm{~A}}{\mathrm{~V}}(2.2 \mathrm{M} \Omega \| 404 \mathrm{k} \Omega)=120 \tag{6.218}
\end{equation*}
$$

In this equation, $G_{m 2}$ is multiplied by two because of the effect of feedback biasing explained above. The voltage gain of the third stage when loaded by a $2 \mathrm{k} \Omega$ resistor conducting a current of 1 mA is

$$
\begin{equation*}
a_{v 3}=G_{m 3}\left(R_{o 3} \| R_{L}\right)=\frac{1}{96 \Omega}(15 \mathrm{k} \Omega \| 2 \mathrm{k} \Omega)=18 \tag{6.219}
\end{equation*}
$$

Therefore, the overall gain of the NE5234 op amp is

$$
\begin{equation*}
a_{v}=a_{v 1} a_{v 2} a_{v 3}=130,000 \tag{6.220}
\end{equation*}
$$

This gain is an estimate of the minimum gain of the op amp because the load is usually larger than $2 \mathrm{k} \Omega$ and because the values of Early voltages and betas used are the minimum values expected to occur when building many op amps. In practice, the gain is usually much higher than this value. See Problem 6.28.

### 6.8.4 Calculation of the Input Offset Voltage and Current of the NE5234

Two important aspects of the performance of op amps are the input offset voltage and current. Since the offsets are indistinguishable from the dc component in the signal of interest, these deviations from ideality limit the ability of the circuit to amplify small dc signals accurately. Furthermore, calculation of these parameters is fundamentally different from calculation of other parameters such as voltage gain. Offset voltage and current are random parameters with mean values that are usually near zero. These offsets arise from randomly occurring mismatches between pairs of matched elements in the input stage of the circuit, and are best described by a probability distribution with (ideally) zero mean and some standard deviation. The parameters of interest from the designer's standpoint are the standard deviations of the offset voltage and current distributions, which determine the limits that can be placed on the offset voltage and current of production units being tested while maintaining an acceptable yield. From the user's standpoint, the details of the distribution are of little significance except as they affect the specified maximum offset voltage chosen by the designer. The information available to the designer at the design stage is the distribution of mismatches in resistor values, transistor saturation currents, and transistor betas. Given these distributions, the task is to design an input stage with the minimum offset while meeting the other circuit requirements. We will calculate the offset voltage and current of the NE5234 op amp under the assumption that the various device mismatches are described by normal or Gaussian distributions.

In this analysis, we will assume that the voltage and current gains of the input stage are large enough that other stages have negligible effect on the input offset voltage and current of the op amp. Provided that the mismatches are small enough that they only slightly perturb the currents in the circuit, we can simplify the problem by considering each device pair independently. Figure 6.49 shows a simplified schematic of the input stage of the NE5234. This figure assumes that the common-mode input voltage to the op amp is low enough that $Q_{3}$ and $Q_{4}$ are active but $Q_{1}$ and $Q_{2}$ are off. The collector currents of $Q_{3}$ and $Q_{4}$ are modeled here by current sources $\left|I_{C 3}\right|$ and $\left|I_{C 4}\right|$. The first problem is to determine the difference between $\left|I_{C 3}\right|$ and $\left|I_{C 4}\right|$ required to set $I_{C 9}-I_{C 10}=0$ in the presence of mismatches between $Q_{9}$ and $Q_{10}$ as well as between $R_{9}$ and $R_{10}$.

From KVL,

$$
\begin{equation*}
V_{B}=V_{T} \ln \left(\frac{I_{C 9}}{I_{S 9}}\right)+\left(\frac{I_{C 9}}{\alpha_{F 9}}+\left|I_{C 3}\right|\right) R_{9} \tag{6.221}
\end{equation*}
$$

image_name:Figure 6.49
description:
[
name: IC3, type: CurrentSource, value: IC3, ports: {Np: Vcc, Nn: 3}
name: IC4, type: CurrentSource, value: IC4, ports: {Np: Vcc, Nn: 4}
name: Q9, type: NPN, ports: {C: Vcc, B: VB, E: 3}
name: Q10, type: NPN, ports: {C: Vcc, B: VB, E: 4}
name: R9, type: Resistor, value: 22kΩ, ports: {N1: 3, N2: VB}
name: R10, type: Resistor, value: 22kΩ, ports: {N1: 4, N2: VB}
name: VB, type: VoltageSource, ports: {Np: VB, Nn: -VEE}
]
extrainfo:The circuit is a differential amplifier input stage with current sources IC3 and IC4. It includes two NPN transistors Q9 and Q10 with resistors R9 and R10 connected to the emitters. The goal is to balance the currents IC9 and IC10.

Figure 6.49 A model of the NE5234 input stage for finding $\left|I_{C 3}\right|-\left|I_{C 4}\right|$ to set $I_{C 9}-I_{C 10}=0$.
and

$$
\begin{equation*}
V_{B}=V_{T} \ln \left(\frac{I_{C 10}}{I_{S 10}}\right)+\left(\frac{I_{C 10}}{\alpha_{F 10}}+\left|I_{C 4}\right|\right) R_{10} \tag{6.222}
\end{equation*}
$$

Subtracting these equations gives

$$
\begin{equation*}
0=V_{T} \ln \left(\frac{I_{C 9}}{I_{C 10}}\right)-V_{T} \ln \left(\frac{I_{S 9}}{I_{S 10}}\right)+\frac{I_{C 9}}{\alpha_{F 9}} R_{9}-\frac{I_{C 10}}{\alpha_{F 10}} R_{10}+\left|I_{C 3}\right| R_{9}-\left|I_{C 4}\right| R_{10} \tag{6.223}
\end{equation*}
$$

To simplify the first two terms on the right side of this equation, use standard definitions of average and mismatch quantities as in Section A.4.1.1: $I_{C 9,10}=\left(I_{C 9}+I_{C 10}\right) / 2$, $\Delta I_{C 9,10}=I_{C 9}-I_{C 10}, I_{S 9,10}=\left(I_{S 9}+I_{S 10}\right) / 2$, and $\Delta I_{S 9,10}=I_{S 9}-I_{S 10}$. Also, assume that $\Delta I_{C 9,10} / 2 I_{C 9,10} \ll 1, \Delta I_{S 9,10} / 2 I_{S 9,10} \ll 1$, and $\ln (1+x) \simeq x$ for $x \ll 1$. Then

$$
\begin{equation*}
V_{T} \ln \left(\frac{I_{C 9}}{I_{C 10}}\right)-V_{T} \ln \left(\frac{I_{S 9}}{I_{S 10}}\right) \simeq V_{T}\left(\frac{\Delta I_{C 9,10}}{I_{C 9,10}}-\frac{\Delta I_{S 9,10}}{I_{S 9,10}}\right) \tag{6.224}
\end{equation*}
$$

With corresponding definitions and assumptions for other parameters, the next two terms in (6.223) become

$$
\begin{equation*}
\frac{I_{C 9}}{\alpha_{F 9}} R_{9}-\frac{I_{C 10}}{\alpha_{F 10}} R_{10} \simeq \frac{I_{C 9,10} R_{9,10}}{\alpha_{F 9,10}}\left(\frac{\Delta I_{C 9,10}}{I_{C 9,10}}+\frac{\Delta R_{9,10}}{R_{9,10}}-\frac{\Delta \alpha_{F 9,10}}{\alpha_{F 9,10}}\right) \tag{6.225}
\end{equation*}
$$

Similarly, the last two terms in (6.223) become

$$
\begin{equation*}
\left|I_{C 3}\right| R_{9}-\left|I_{C 4}\right| R_{10} \simeq\left|I_{C 3,4}\right| R_{9,10}\left(\frac{\Delta\left|I_{C 3,4}\right|}{\left|I_{C 3,4}\right|}+\frac{\Delta R_{9,10}}{R_{9,10}}\right) \tag{6.226}
\end{equation*}
$$

Substituting (6.224), (6.225), and (6.226) into (6.223) and finding $\Delta\left|I_{C 3,4}\right| /\left|I_{C 3,4}\right|$ needed to set $\Delta I_{C 9,10} / I_{C 9,10}=0$ gives

$$
\begin{equation*}
\frac{\Delta\left|I_{C 3,4}\right|}{\left|I_{C 3,4}\right|} \simeq \frac{1}{g_{m 3,4} R_{9,10}} \frac{\Delta I_{S 9,10}}{I_{S 9,10}}-\left(1+\frac{g_{m 9,10}}{\alpha_{F 9,10} g_{m 3,4}}\right) \frac{\Delta R_{9,10}}{R_{9,10}}+\frac{g_{m 9,10}}{\alpha_{F 9,10} g_{m 3,4}} \frac{\Delta \alpha_{F 9,10}}{\alpha_{F 9,10}} \tag{6.227}
\end{equation*}
$$

Now consider Fig. 6.50, which shows a slightly more complicated model of the NE5234 input stage. This figure includes $\left|I_{C 13}\right|$ and $\left|I_{C 14}\right|$ to model the currents produced by $Q_{13}, Q_{14}$, $R_{13}$, and $R_{14}$. These elements form the outputs of a pair of current mirrors, and the effect of
image_name:Figure 6.50
description:
[
name: IC3, type: CurrentSource, value: IC3, ports: {Np: Vcc, Nn: 3}
name: IC4, type: CurrentSource, value: IC4, ports: {Np: Vcc, Nn: 4}
name: IC13, type: CurrentSource, value: IC13, ports: {Np: Vcc, Nn: 9}
name: IC14, type: CurrentSource, value: IC14, ports: {Np: Vcc, Nn: 10}
name: Q9, type: NPN, ports: {C: 9, B: VB, E: 3}
name: Q10, type: NPN, ports: {C: 10, B: VB, E: 4}
name: R9, type: Resistor, value: 22kΩ, ports: {N1: 3, N2: gnd}
name: R10, type: Resistor, value: 22kΩ, ports: {N1: 4, N2: gnd}
name: VB, type: VoltageSource, value: VB, ports: {Np: VB, Nn: gnd}
]
extrainfo:The circuit is a model of the NE5234 input stage, designed to balance the collector currents IC3 and IC4 with IC13 and IC14 through transistors Q9 and Q10. Resistors R9 and R10 provide biasing, and the voltage source VB sets the base voltage for Q9 and Q10.

Figure 6.50 A model of the NE5234 input stage for finding $\left|I_{C 3}\right|-\left|I_{C 4}\right|$ to set $I_{C 9}-I_{C 10}=\left|I_{C 13}\right|-\left|I_{C 14}\right|$.
mismatch in these elements is considered in Section A.4.1.1. From (4.296),

$$
\begin{align*}
& \frac{\Delta\left|I_{C 13,14}\right|}{\left|I_{C 13,14}\right|} \simeq\left(\frac{1}{1+\frac{g_{m 13,14} R_{13,14}}{\alpha_{F 13,14}}}\right) \frac{\Delta\left|I_{S 13,14}\right|}{\left|I_{S 13,14}\right|}  \tag{6.228}\\
&+\frac{\frac{g_{m 13,14} R_{13,14}}{\alpha_{F 13,14}}}{1+\frac{g_{m 13,14} R_{13,14}}{\alpha_{F 13,14}}}\left(-\frac{\Delta R_{13,14}}{R_{13,14}}+\frac{\Delta \alpha_{F 13,14}}{\alpha_{F 13,14}}\right)
\end{align*}
$$

To include these mismatches in the stage offsets, we substitute (6.224), (6.225), and (6.226) into (6.223) and find $\Delta\left|I_{C 3,4}\right| /\left|I_{C 3,4}\right|$ needed to set $\Delta I_{C 9,10} / I_{C 9,10}=\Delta\left|I_{C 13,14}\right| /\left|I_{C 13,14}\right|$, which causes the differential output voltage of the stage to be zero and gives

$$
\begin{align*}
\frac{\Delta\left|I_{C 3,4}\right|}{\left|I_{C 3,4}\right|} \simeq & \frac{1}{g_{m 3,4} R_{9,10}} \frac{\Delta I_{S 9,10}}{I_{S 9,10}}-\left(1+\frac{g_{m 9,10}}{\alpha_{F 9,10} g_{m 3,4}}\right) \frac{\Delta R_{9,10}}{R_{9,10}}+\frac{g_{m 9,10}}{\alpha_{F 9,10} g_{m 3,4}} \frac{\Delta \alpha_{F 9,10}}{\alpha_{F 9,10}} \\
& -\left(\frac{1+\frac{g_{m 9,10} R_{9,10}}{\alpha_{F 9,10}}}{g_{m 3,4} R_{9,10}}\right)\left(\frac{\frac{g_{m 13,14} R_{13,14}}{\alpha_{F 13,14}}}{1+\frac{g_{m 13,14} R_{13,14}}{\alpha_{F 13,14}}}\right)\left(-\frac{\Delta R_{13,14}}{R_{13,14}}+\frac{\Delta \alpha_{F 13,14}}{\alpha_{F 13,14}}\right) \\
& -\left(\frac{1+\frac{g_{m 9,10} R_{9,10}}{\alpha_{F 9,10}}}{g_{m 3,4} R_{9,10}}\right)\left(\frac{1}{1+\frac{g_{m 13,14} R_{13,14}}{\alpha_{F 13,14}}}\right) \frac{\Delta\left|I_{S 13,14}\right|}{\left|I_{S 13,14}\right|} \tag{6.229}
\end{align*}
$$

Now the problem is to refer $\Delta\left|I_{C 3,4}\right| /\left|I_{C 3,4}\right|$ to the input of the op amp. Fig. 6.51 shows a model of the input stage used to find the input offset voltage. From KVL,

$$
\begin{equation*}
V_{4}-V_{3}=V_{E B 3}-V_{E B 4}=V_{T} \ln \left(\frac{\left|I_{S 4}\right|}{\left|I_{S 3}\right|} \frac{\left|I_{C 3}\right|}{\left|I_{C 4}\right|}\right) \tag{6.230}
\end{equation*}
$$

image_name:Figure 6.51
description:
[
name: Q3, type: PNP, ports: {C: 3, B: V3, E: e3e4}
name: Q4, type: PNP, ports: {C: 4, B: V4, E: e3e4}
name: V3, type: VoltageSource, value: V3, ports: {Np: V3, Nn: GND}
name: V4, type: VoltageSource, value: V4, ports: {Np: V4, Nn: GND}
name: IC11, type: CurrentSource, value: IC11, ports: {Np: VCC, Nn: e3e4}
]
extrainfo:The circuit is a differential pair with PNP transistors Q3 and Q4. The emitters of Q3 and Q4 are connected together and biased by the current source IC11. The bases of Q3 and Q4 are connected to voltage sources V3 and V4, respectively. The collectors of Q3 and Q4 are connected to nodes 3 and 4, respectively.

Figure 6.51 A model of the NE5234 input stage for finding $V_{O S}$ when the commonmode input voltage is low enough that $Q_{1}$ and $Q_{2}$ are off.

Using standard definitions of average and mismatch quantities and similar assumptions to those made to simplify (6.223) gives

$$
\begin{equation*}
V_{4}-V_{3} \simeq V_{T}\left(-\frac{\Delta\left|I_{S 3,4}\right|}{\left|I_{S 3,4}\right|}+\frac{\Delta\left|I_{C 3,4}\right|}{\left|I_{C 3,4}\right|}\right) \tag{6.231}
\end{equation*}
$$

Then the input offset voltage, $V_{O S}$, is the differential input voltage, $V_{4}-V_{3}$, for which the differential output voltage of the stage is zero. This condition is satisfied when $\Delta\left|I_{C 3,4}\right| /\left|I_{C 3,4}\right|$ is given by (6.229). Substituting (6.229) into (6.231) with $g_{m 3,4}=3 \mu \mathrm{~A} / 26 \mathrm{mV}, g_{m 9,10}=$ $g_{m 13,14}=6 \mu \mathrm{~A} / 26 \mathrm{mV}, R_{9,10}=22 \mathrm{k} \Omega, R_{13,14}=33 \mathrm{k} \Omega, \alpha_{F 9,10}=40 / 41$, and $\alpha_{F 13,14}=$ 10/11 gives

$$
\begin{align*}
V_{O S} \simeq & V_{T}\left[-\left(\frac{\Delta\left|I_{S 3,4}\right|}{\left|I_{S 3,4}\right|}\right)+0.39\left(\frac{\Delta I_{S 9,10}}{I_{S 9,10}}\right)-3.1\left(\frac{\Delta R_{9,10}}{R_{9,10}}\right)+2.1\left(\frac{\Delta \alpha_{F 9,10}}{\alpha_{F 9,10}}\right)\right. \\
& \left.-2.2\left(-\frac{\Delta R_{13,14}}{R_{13,14}}+\frac{\Delta \alpha_{F 13,14}}{\alpha_{F 13,14}}\right)-0.26\left(\frac{\Delta\left|I_{S 13,14}\right|}{\left|I_{S 13,14}\right|}\right)\right] \tag{6.232}
\end{align*}
$$

For a given set of mismatches, this expression gives the input offset voltage. However, the information of interest to the designer is the distribution of observed offset voltages over a large number of samples, and the information available is the distribution of the mismatch factors. If each of the quantities

$$
\frac{\Delta\left|I_{S 3,4}\right|}{\left|I_{S 3,4}\right|} \quad \frac{\Delta I_{S 9,10}}{I_{S 9,10}} \quad \frac{\Delta R_{9,10}}{R_{9,10}} \quad \frac{\Delta \alpha_{F 9,10}}{\alpha_{F 9,10}} \quad \frac{\Delta R_{13,14}}{R_{13,14}} \quad \frac{\Delta \alpha_{F 13,14}}{\alpha_{F 13,14}} \quad \frac{\Delta\left|I_{S 13,14}\right|}{\left|I_{S 13,14}\right|}
$$

are regarded as independent random variables with normal distributions, the standard deviation of the sum is given by

$$
\begin{equation*}
\sigma_{\mathrm{sum}}=\sqrt{\sum_{n} \sigma_{n}^{2}} \tag{6.233}
\end{equation*}
$$

as described in Appendix A3.1. Thus the standard deviation of the distribution for $V_{O S}$ is calculated by taking the square root of the sum of the squares of the individual contributions.

Assuming that the standard deviation of resistor matching is 1 percent, that of $I_{S}$ matching is 5 percent, and that of beta matching is 10 percent, we obtain

$$
\begin{align*}
\frac{\sigma_{V_{O S}}}{V_{T}} & =\sqrt{(0.050)^{2}+(0.020)^{2}+(0.031)^{2}+(0.0050)^{2}+(0.022)^{2}+(0.020)^{2}+(0.013)^{2}} \\
\sigma_{V_{O S}} & =V_{T}(0.070)=1.8 \mathrm{mV} \tag{6.234}
\end{align*}
$$

image_name:Figure 6.52
description:
[
name: Q3, type: PNP, ports: {C: e3e4, B: b3, E: 3}
name: Q4, type: PNP, ports: {C: e3e4, B: b4, E: 4}
name: I_B3, type: CurrentSource, value: I_B3, ports: {Np: b3, Nn: GND}
name: I_B4, type: CurrentSource, value: I_B4, ports: {Np: b4, Nn: GND}
name: I_C11, type: CurrentSource, value: I_C11, ports: {Np: VCC, Nn: e324}
]
extrainfo:This circuit represents the input stage of the NE5234 with Q3 and Q4 as PNP transistors. The current sources I_B3 and I_B4 provide biasing for the bases of Q3 and Q4, respectively. I_C11 is a current source connected to the common collector node e324. The emitters of Q3 and Q4 are connected to nodes 3 and 4, respectively.

Figure 6.52 A model of the NE5234 input stage for finding $I_{O S}$ when the commonmode input voltage is low enough that $Q_{1}$ and $Q_{2}$ are off.

The largest single offset contribution is thus the saturation current mismatch of the input devices $Q_{3}$ and $Q_{4}$. If the offset voltage has a standard deviation of 1.8 mV , then the fraction, $Y$, of all devices fabricated that will have an offset voltage of less than the NE5234 specification of 5 mV can be found using (3.285) and is

$$
\begin{equation*}
Y=\int_{-5}^{5} \frac{1}{1.8 \sqrt{2 \pi}} \exp \left[-\frac{x^{2}}{2(1.8)^{2}}\right] d x \tag{6.235}
\end{equation*}
$$

Evaluating this integral with the aid of Fig. 3.71 gives $Y=0.995$. Thus a 0.5 percent yield loss will be suffered from offset voltage variations with the $5-\mathrm{mV}$ offset specification.

Figure 6.52 shows a model of the input stage used to find the input offset current. The difference of the magnitudes of the base currents is

$$
\begin{align*}
\left|I_{B 4}\right|-\left|I_{B 3}\right| & =\frac{\left|I_{C 4}\right|}{\beta_{F 4}}-\frac{\left|I_{C 3}\right|}{\beta_{F 3}}=\frac{\left|I_{C 3,4}\right|}{\beta_{F 3,4}}\left(\frac{1-\frac{\Delta\left|I_{C 3,4}\right|}{2\left|I_{C 3,4}\right|}}{1-\frac{\Delta \beta_{F 3,4}}{2 \beta_{F 3,4}}}-\frac{1+\frac{\Delta\left|I_{C 3,4}\right|}{2\left|I_{C 3,4}\right|}}{1+\frac{\Delta \beta_{F 3,4}}{2 \beta_{F 3,4}}}\right) \\
& \simeq\left|I_{B 3,4}\right|\left(\frac{\Delta \beta_{F 3,4}}{\beta_{F 3,4}}-\frac{\Delta\left|I_{C 3,4}\right|}{\left|I_{C 3,4}\right|}\right) \tag{6.236}
\end{align*}
$$

Then the input offset current, $I_{O S}$, is the differential input current, $\left|I_{B 4}\right|-\left|I_{B 3}\right|$, for which the differential output voltage of the stage is zero. This condition is satisfied when $\Delta\left|I_{C 3,4}\right| /\left|I_{C 3,4}\right|$ is given by (6.229). Substituting (6.229) into (6.236) with the same parameter values as in (6.232) gives

$$
\begin{align*}
I_{O S} \simeq & \left|I_{B 3,4}\right|\left[\left(\frac{\Delta \beta_{F 3,4}}{\beta_{F 3,4}}\right)-0.39\left(\frac{\Delta I_{S 9,10}}{I_{S 9,10}}\right)+3.1\left(\frac{\Delta R_{9,10}}{R_{9,10}}\right)-2.1\left(\frac{\Delta \alpha_{F 9,10}}{\alpha_{F 9,10}}\right)\right. \\
& \left.+2.2\left(-\frac{\Delta R_{13,14}}{R_{13,14}}+\frac{\Delta \alpha_{F 13,14}}{\alpha_{F 13,14}}\right)+0.26\left(\frac{\Delta\left|I_{S 13,14}\right|}{\left|I_{S 13,14}\right|}\right)\right] \tag{6.237}
\end{align*}
$$

Under the same conditions used to calculate $\sigma_{V_{O S}}$, we obtain

$$
\begin{align*}
\frac{\sigma_{I O S}}{\left|I_{B 3,4}\right|} & =\sqrt{(0.10)^{2}+(0.020)^{2}+(0.031)^{2}+(0.0050)^{2}+(0.022)^{2}+(0.020)^{2}+(0.013)^{2}} \\
\sigma_{I O S} & =\frac{3 \mu \mathrm{~A}}{10}(0.11)=33 \mathrm{nA} \tag{6.238}
\end{align*}
$$

and is dominated by the beta mismatch between $Q_{3}$ and $Q_{4}$.
