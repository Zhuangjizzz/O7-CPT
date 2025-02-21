# CHAPTER 8 Feedback

On a mild August morning in 1927, Harold Black was riding the ferry from New York to New Jersey, where he worked at Bell Laboratories. Black and many other researchers had been investigating the problem of nonlinearity in amplifiers used in long-distance telephone networks, seeking a practical solution. While reading the newspaper on the ferry, Black was suddenly struck by an idea and began to draw a diagram on the newspaper, which would later be used as the evidence in his patent application. The idea is known to us as the negative-feedback amplifier.

Feedback is a powerful technique that finds wide application in analog circuits. For example, negative feedback allows high-precision signal processing, and positive feedback makes it possible to build oscillators. In this chapter, we consider only negative feedback and use the term feedback to mean that.

We begin with a general view of feedback circuits, describing important benefits that result from feedback. Next, we study four feedback topologies and their properties. We then deal with difficulties in feedback circuit analysis and introduce the two-port technique, Bode's technique, and Blackman's theorem as possible solutions.

## 8.1 ■ General Considerations

Figure 8.1 shows a negative-feedback system, where $H(s)$ and $G(s)$ are called the feedforward and the feedback networks, respectively. Since the output of $G(s)$ is equal to $G(s) Y(s)$, the input to $H(s)$, called the feedback error, is given by $X(s)-G(s) Y(s)$. That is

$$
\begin{equation*}
Y(s)=H(s)[X(s)-G(s) Y(s)] \tag{8.1}
\end{equation*}
$$

Thus,

$$
\begin{equation*}
\frac{Y(s)}{X(s)}=\frac{H(s)}{1+G(s) H(s)} \tag{8.2}
\end{equation*}
$$

image_name:Figure 8.1 General feedback system
description:The block diagram in Figure 8.1 represents a general negative-feedback system. It consists of two main components: the feedforward network, denoted as \( H(s) \), and the feedback network, denoted as \( G(s) \).

1. **Main Components:**
- **\( H(s) \):** This block represents the open-loop transfer function, typically an amplifier in many systems. It processes the input signal and generates the output \( Y(s) \).
- **\( G(s) \):** This block represents the feedback network. It takes a fraction of the output \( Y(s) \) and feeds it back to the input.

2. **Flow of Information or Control:**
- The input signal \( X(s) \) enters the system and is combined with the feedback signal from \( G(s) \) at a summing junction. This combination is called the feedback error.
- The feedback error \( (X(s) - G(s)Y(s)) \) is then fed into the \( H(s) \) block.
- The output of \( H(s) \) is \( Y(s) \), which is the system's output.
- A portion of \( Y(s) \) is fed back through \( G(s) \) to form the feedback loop.

3. **Labels, Annotations, and Key Indicators:**
- The summing junction is labeled with a plus and minus sign, indicating the subtraction of the feedback signal from the input signal.
- The output of \( H(s) \) is labeled \( Y(s) \) and the input is labeled \( X(s) \).

4. **Overall System Function:**
- The primary function of this system is to control the output \( Y(s) \) by adjusting the influence of the feedback signal. The closed-loop transfer function of the system is given by \( \frac{H(s)}{1 + G(s)H(s)} \), which shows how the feedback affects the overall gain and stability of the system. The feedback helps to reduce errors, improve stability, and achieve desired performance characteristics in the output.

Figure 8.1 General feedback system.
image_name:Figure 8.1 General feedback system
description:The system block diagram labeled "Figure 8.1 General feedback system" represents a typical feedback control system. Here is a detailed description of the system:

1. **Main Components:**
- **Summing Junction (+/-):** This block is the initial point where the input signal is combined with the feedback signal. It generates an 'error' signal, which is the difference between the input and the feedback.
- **H(s) Block:** This represents the "open-loop" transfer function, typically an amplifier in the system. It processes the error signal to produce the system output.
- **G(s) Block:** This block is part of the feedback path and is generally a frequency-independent component. It processes a fraction of the output signal to be fed back into the system.

2. **Flow of Information or Control:**
- The input signal enters the system and is combined with the feedback signal at the summing junction, creating an error signal.
- The error signal is then passed to the H(s) block, which amplifies or processes it to produce the output Y(s).
- A portion of the output Y(s) is fed back into the system through the G(s) block, completing the feedback loop.
- This feedback loop is crucial for adjusting the system's performance by minimizing the error signal.

3. **Labels, Annotations, and Key Indicators:**
- The diagram is annotated with key terms such as "Error" at the summing junction, indicating the purpose of the block.
- The output is labeled as Y(s), and the feedback path is clearly shown with directional arrows, emphasizing the flow of signals.

4. **Overall System Function:**
- The primary function of this feedback system is to control the output Y(s) by adjusting the influence of the feedback signal. The closed-loop transfer function \( \frac{H(s)}{1 + G(s)H(s)} \) demonstrates how feedback affects the system's gain and stability. The feedback mechanism helps in reducing errors, improving stability, and achieving desired performance characteristics in the output.

Figure 8.2 Similarity between output of feedback network and input signal.

We call $H(s)$ the "open-loop" transfer function and $Y(s) / X(s)$ the "closed-loop" transfer function. In most cases of interest in this book, $H(s)$ represents an amplifier and $G(s)$ is a frequency-independent quantity. In other words, a fraction of the output signal is sensed and compared with the input, generating an error term. In a well-designed negative-feedback system, the error term is minimized, thereby making the output of $G(s)$ an accurate "copy" of the input and hence the output of the system a faithful (scaled) replica of the input (Fig. 8.2). We also say that the input of $H(s)$ is a "virtual ground" because the signal amplitude at this point is small. In subsequent developments, we replace $G(s)$ by a frequency-independent quantity $\beta$ and call it the "feedback factor."

It is instructive to identify four elements in the feedback system of Fig. 8.1: (1) the feedforward amplifier, (2) a means of sensing the output, (3) the feedback network, and (4) a means of generating the feedback error, i.e., a subtractor (or an adder). These elements exist in every feedback system, even though they may not be obvious in cases such as a simple common-source stage with resistive degeneration.

### 8.1.1 Properties of Feedback Circuits

Before proceeding to the analysis of feedback circuits, we study some simple examples to describe the benefits of negative feedback.

Gain Desensitization Consider the common-source stage shown in Fig. 8.3(a), where the voltage gain is equal to $g_{m 1} r_{O 1}$. A critical drawback of this circuit is the poor definition of the gain: both $g_{m 1}$ and $r_{O 1}$ vary with process and temperature. Now suppose the circuit is configured as in Fig. 8.3(b), where the gate bias of $M_{1}$ is set by means not shown here (Chapter 13). Let us calculate the overall voltage gain of the circuit at relatively low frequencies such that $C_{2}$ draws a negligible (small-signal) current from the output node, i.e., $V_{o u t} / V_{X}=-g_{m 1} r_{O 1}$ because the entire drain current flows through $r_{O 1}$. Since $\left(V_{\text {out }}-V_{X}\right) C_{2} s=\left(V_{X}-V_{\text {in }}\right) C_{1} s$, we have

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=-\frac{1}{\left(1+\frac{1}{g_{m 1} r_{O 1}}\right) \frac{C_{2}}{C_{1}}+\frac{1}{g_{m 1} r_{O 1}}} \tag{8.3}
\end{equation*}
$$

image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: Vout}
]
extrainfo:This is a simple common-source amplifier stage with an NMOS transistor (M1) and a current source (I1) as the load. The input is applied at the gate of M1, and the output is taken from the drain, which is connected to the current source I1.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: Vin}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: Vout}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: X}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Vout}
]
extrainfo:The circuit in (b) is a common-source amplifier with feedback, incorporating capacitors C1 and C2 to control the gain by the ratio of the capacitors. The current source I1 provides biasing.

Figure 8.3 (a) Simple common-source stage; (b) circuit of (a) with feedback.

If $g_{m 1} r_{O 1}$ is sufficiently large, the $1 /\left(g_{m 1} r_{O 1}\right)$ terms in the denominator can be neglected, yielding

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=-\frac{C_{1}}{C_{2}} \tag{8.4}
\end{equation*}
$$

Compared to $g_{m 1} r_{O 1}$, this gain can be controlled with much higher accuracy because it is given by the ratio of two capacitors. If $C_{1}$ and $C_{2}$ are made of the same material, then process and temperature variations do not change $C_{1} / C_{2}$.

The above example reveals that negative feedback provides gain "desensitization," i.e., the closed-loop gain is less sensitive to device parameters than the open-loop gain is. One may also say that negative feedback "stabilizes" the gain and hence "improves the stability." But this nomenclature may be confused with frequency stability (Chapter 10), which typically worsens as a result of negative feedback. Illustrated for a more general case in Fig. 8.4, gain desensitization can be quantified by writing

$$
\begin{align*}
\frac{Y}{X} & =\frac{A}{1+\beta A}  \tag{8.5}\\
& \approx \frac{1}{\beta}\left(1-\frac{1}{\beta A}\right) \tag{8.6}
\end{align*}
$$

where we have assumed that $\beta A \gg 1$. We note that the closed-loop gain is determined, to the first order by the feedback factor, $\beta$. More important, even if the open-loop gain, $A$, varies by a factor of, say, 2 , $Y / X$ varies by a small percentage because $1 /(\beta A) \ll 1$.
image_name:Figure 8.4 Simple feedback system
description:The block diagram labeled "Figure 8.4 Simple feedback system" illustrates a basic feedback control system. It consists of the following key components:

1. **Summing Junction (+/-):** This is the initial point where the input signal, X, is introduced. The summing junction adds the input signal X to the feedback signal (with a subtraction, indicated by the negative sign) to produce an error signal.

2. **Amplifier (A):** The error signal from the summing junction is fed into an amplifier with gain A. This block amplifies the error signal, and the output of this block is the amplified signal.

3. **Output (Y):** The amplified signal from the amplifier is taken as the system's output, Y.

4. **Feedback Path (β):** The output Y is fed back into the system through a feedback path that includes a block with a gain factor β. This feedback path takes a portion of the output signal and returns it to the summing junction, where it is subtracted from the input signal X.

**Flow of Information:**
- The input signal X enters the summing junction.
- The feedback signal, derived from the output Y and scaled by β, is subtracted from X at the summing junction.
- The resulting error signal is amplified by the amplifier with gain A.
- The amplified signal is the output Y, which is also fed back into the system through the feedback path.

**Overall System Function:**
This system is a classic example of a negative feedback loop, where the output is fed back into the input to minimize the error signal. The primary function of this system is to stabilize the output Y against variations in the open-loop gain A by adjusting the feedback factor β. This configuration helps maintain a consistent closed-loop gain, making Y/X less sensitive to changes in A, thereby improving system accuracy and stability.

Figure 8.4 Simple feedback system.
Called the "loop gain," the quantity $\beta A$ plays an important role in feedback systems. ${ }^{1}$ We see from (8.6) that the higher $\beta A$ is, the less sensitive $Y / X$ will be to variations in $A$. From another perspective, the accuracy of the closed-loop gain improves by maximizing $\beta A$. Note that as $\beta$ increases, the closedloop gain, $Y / X \approx 1 / \beta$, decreases, suggesting a trade-off between precision and the closed-loop gain. In other words, we begin with a high-gain amplifier and apply feedback to obtain a low, but less sensitive, closed-loop gain. Another conclusion here is that the output of the feedback network is equal to $\beta Y=$ $X \cdot \beta A /(1+\beta A)$, approaching $X$ as $\beta A$ becomes much greater than unity. This result agrees with the illustration in Fig. 8.2.

The calculation of the loop gain can proceed as follows. As illustrated in Fig. 8.5, we set the main input to (ac) zero, break the loop at some point, inject a test signal in the "right direction," follow the signal around the loop, and obtain the value that returns to the break point. The negative of the transfer function thus derived is the loop gain. Note that the loop gain is a dimensionless quantity. In Fig. 8.5, we have $V_{t} \beta(-1) A=V_{F}$ and hence $V_{F} / V_{t}=-\beta A$. Similarly, as depicted in Fig. 8.6, for the simple feedback circuit, we can write $V_{X}=V_{t} C_{2} /\left(C_{1}+C_{2}\right)$ and $^{2}$

$$
\begin{equation*}
V_{t} \frac{C_{2}}{C_{1}+C_{2}}\left(-g_{m 1} r_{O 1}\right)=V_{F} \tag{8.7}
\end{equation*}
$$

[^44]image_name:Figure 8.5 Computation of loop gain
description:The block diagram in Figure 8.5 illustrates the computation of loop gain in a feedback control system. The primary components of this system include:

1. **Summing Junction**: This is where the input signal and the feedback signal are combined. The input signal enters the summing junction with a positive sign, while the feedback signal is subtracted, indicating negative feedback.

2. **Amplifier (A)**: The output of the summing junction is fed into an amplifier block labeled 'A'. This block amplifies the input signal, and its gain is a crucial part of the loop gain calculation.

3. **Feedback Path**: The output of the amplifier is fed back to the input through a feedback path. This path includes a block labeled 'β', which represents the feedback factor. The feedback signal is taken from the output of this block and fed back into the summing junction.

4. **Voltage Indicators (V_t and V_F)**: The diagram includes two voltage indicators. 'V_t' is the test voltage applied at the input, and 'V_F' is the feedback voltage. These voltages are used to calculate the loop gain.

5. **Equation Annotation**: The diagram is annotated with the equation X(s) = 0, indicating that the system is being analyzed at a specific condition where the input is set to zero. This is typical in loop gain analysis to determine system stability.

**Flow of Information**:
- The input signal is introduced at the summing junction, where it is combined with the negative feedback signal.
- The resultant signal is then amplified by the amplifier 'A'.
- The amplified signal is split; one part goes to the output, and the other part is fed back through the feedback block 'β'.
- The feedback signal is then subtracted from the input at the summing junction, completing the feedback loop.

**Overall System Function**:
The primary function of this system is to compute the loop gain, which is a measure of how much the output of the system is fed back into the input. This loop gain is critical for analyzing the stability and performance of the feedback control system. The negative feedback helps in stabilizing the gain and reducing the effects of parameter variations in the amplifier.

Figure 8.5 Computation of loop gain.
image_name:Figure 8.6
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: X, Nn: X}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: X}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: d1}
name: M1, type: NMOS, ports: {S: GND, D: d1, G: X}
]
extrainfo:The circuit is a feedback loop designed to compute the loop gain. It includes capacitors C1 and C2, a current source I1, and an NMOS transistor M1. The voltage Vt is applied at the input, and the feedback voltage VF is taken across the NMOS.

Figure 8.6 Computation of loop gain in a simple feedback circuit.

That is

$$
\begin{equation*}
\frac{V_{F}}{V_{t}}=-\frac{C_{2}}{C_{1}+C_{2}} g_{m 1} r_{O 1} \tag{8.8}
\end{equation*}
$$

Note that the current drawn by $C_{2}$ from the output is neglected here. This issue will be addressed in Sec. 8.5.

#### Example 8.1

Determine the loop gain for the feedback common-gate stage shown in Fig. 8.7(a).
image_name:Figure 8.7(a)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: g1, Nn: GND}
name: M1, type: NMOS, ports: {S: s1, D: Vout, G: g1}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: Vout}
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
]
extrainfo:The circuit is a feedback common-gate stage with an NMOS transistor M1. The feedback voltage is taken across M1, and the loop gain is determined by the capacitors C1 and C2. The input voltage is applied at Vin, and the output is at Vout.

(a)
image_name:(a)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: VDD, Nn: g1}
name: C2, type: Capacitor, value: C2, ports: {Np: g1, Nn: GND}
name: g1, type: VoltageSource, value: g1, ports: {Np: g1, Nn: GND}
name: M1, type: NMOS, ports: {S: g1, D: Vout, G: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: Vout}
]
extrainfo:The circuit is a feedback common-gate stage with an NMOS transistor M1. The feedback voltage is taken across M1, and the loop gain is determined by the capacitors C1 and C2. The input voltage is applied at Vin, and the output is at Vout.

(b)
image_name:Figure 8.7(b)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: VDD, Nn: Vout}
name: C2, type: Capacitor, value: C2, ports: {Np: g1, Nn: GND}
name: M1, type: NMOS, ports: {S: g1, D: Vout, G: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: Vout}
name: g1, type: VoltageControlledCurrentSource, value: g1, ports: {Np: g1, Nn: GND}
]
extrainfo:The circuit is a feedback common-gate stage with an NMOS transistor M1. The feedback voltage is taken across M1, and the loop gain is determined by the capacitors C1 and C2. The input voltage is applied at Vin, and the output is at Vout.

(c)

Figure 8.7

#### Solution

In order to compute the loop gain, we must first set the main input to (ac) zero, arriving at the arrangement shown in Fig. 8.7(b). Redrawing the circuit as in Fig. 8.7(c), we recognize that this topology is identical to the CS stage of Fig. 8.3(b) with $V_{i n}=0$. The loop gain is therefore given by Eq. (8.8).

The important point here is that, when computing the loop gain, we no longer know where the main input and output terminals are. Thus, seemingly different circuit topologies may have the same loop gain.

We should emphasize that the desensitization of gain by feedback leads to many other properties of feedback systems. Our examination of Eq. (8.6) indicates that large variations in $A$ affect $Y / X$ negligibly if $\beta A$ is large. Such variations can arise from different sources: process, temperature, frequency, and loading. For example, if $A$ drops at high frequencies, $Y / X$ varies to a lesser extent, and the bandwidth is increased. Similarly, if $A$ decreases because the amplifier drives a heavy load, $Y / X$ is not affected much. These concepts become clearer below.

Terminal Impedance Modification As a second example, let us study the circuit shown in Fig. 8.8(a), where a capacitive voltage divider senses the output voltage of a common-gate stage, applying the result to the gate of current source $M_{2}$ and hence returning a signal to the input. ${ }^{3}$ Our objective is to compute the input resistance at relatively low frequencies with and without feedback. Neglecting channellength modulation and the current drawn by $C_{1}$, we break the feedback loop as shown in Fig. 8.8(b) and write

$$
\begin{equation*}
R_{i n, \text { open }}=\frac{1}{g_{m 1}+g_{m b 1}} \tag{8.9}
\end{equation*}
$$

image_name:(a)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: P}
name: C2, type: Capacitor, value: C2, ports: {Np: P, Nn: GND}
name: M1, type: NMOS, ports: {S: P, D: Vout, G: Vb}
name: M2, type: NMOS, ports: {S: GND, D: P, G: Vin}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: Rin, type: Resistor, value: Rin, ports: {N1: Vin, N2: GND}
]
extrainfo:The circuit is a common-gate amplifier with feedback, used to compute input resistance with and without feedback. It includes capacitors C1 and C2 for AC coupling and a resistor RD for load resistance. NMOS transistors M1 and M2 form the core of the amplifier.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: Vin, D: Vout, G: Vb}
name: M2, type: NMOS, ports: {S: GND, D: Vin, G: P}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: P}
name: C2, type: Capacitor, value: C2, ports: {Np: P, Nn: GND}
name: Rin, type: Resistor, value: Rin, ports: {N1: Vin, N2: GND}
name: VX, type: VoltageSource, value: VX, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is an open-loop configuration of a common-gate amplifier with feedback. It includes two NMOS transistors, capacitors for AC coupling, and a resistor for load. The input is applied at Vin, and the output is taken from Vout. The feedback is analyzed by breaking the loop and using a test voltage source VX.
image_name:(c)
description:
[
name: M1, type: NMOS, ports: {S: P, D: Vout, G: Vb}
name: M2, type: NMOS, ports: {S: GND, D: P, G: Vx}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: P}
name: C2, type: Capacitor, value: C2, ports: {Np: P, Nn: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: Rin, type: Resistor, value: Rin, ports: {N1: Vin, N2: P}
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Vx, Nn: GND}
]
extrainfo:The circuit is a common-gate amplifier with feedback. It includes two NMOS transistors, M1 and M2, with feedback applied via a voltage source Vx. Capacitors C1 and C2 are used for coupling and bypassing. The resistor RD is connected to VDD to provide a load for M1. The input resistance is analyzed with the feedback loop open and closed.

Figure 8.8 (a) Common-gate circuit with feedback; (b) open-loop circuit; (c) calculation of input resistance.
For the closed-loop circuit, as depicted in Fig. 8.8(c), we write $V_{\text {out }}=\left(g_{m 1}+g_{m b 1}\right) V_{X} R_{D}$ and

$$
\begin{align*}
V_{P} & =V_{\text {out }} \frac{C_{1}}{C_{1}+C_{2}}  \tag{8.10}\\
& =\left(g_{m 1}+g_{m b 1}\right) V_{X} R_{D} \frac{C_{1}}{C_{1}+C_{2}} \tag{8.11}
\end{align*}
$$

Thus, the small-signal drain current of $M_{2}$ equals $g_{m 2}\left(g_{m 1}+g_{m b 1}\right) V_{X} R_{D} C_{1} /\left(C_{1}+C_{2}\right)$. Adding this current to the drain current of $M_{1}$ with proper polarity yields $I_{X}$ :

$$
\begin{align*}
I_{X} & =\left(g_{m 1}+g_{m b 1}\right) V_{X}+g_{m 2}\left(g_{m 1}+g_{m b 1}\right) \frac{C_{1}}{C_{1}+C_{2}} R_{D} V_{X}  \tag{8.12}\\
& =\left(g_{m 1}+g_{m b 1}\right)\left(1+g_{m 2} R_{D} \frac{C_{1}}{C_{1}+C_{2}}\right) V_{X} \tag{8.13}
\end{align*}
$$

[^45]It follows that

$$
\begin{align*}
R_{\text {in,closed }} & =V_{X} / I_{X}  \tag{8.14}\\
& =\frac{1}{g_{m 1}+g_{m b 1}} \frac{1}{1+g_{m 2} R_{D} \frac{C_{1}}{C_{1}+C_{2}}} \tag{8.15}
\end{align*}
$$

We therefore conclude that this type of feedback reduces the input resistance by a factor of $1+$ $g_{m 2} R_{D} C_{1} /\left(C_{1}+C_{2}\right)$. The reader can prove that the quantity $g_{m 2} R_{D} C_{1} /\left(C_{1}+C_{2}\right)$ is the loop gain.

Let us now consider the circuit of Fig. 8.9(a) as an example of output impedance modification by feedback. Here $M_{1}, R_{S}$, and $R_{D}$ constitute a common-source stage and $C_{1}, C_{2}$, and $M_{2}$ sense the output voltage, ${ }^{4}$ returning a current equal to $\left[C_{1} /\left(C_{1}+C_{2}\right)\right] V_{\text {out }} g_{m 2}$ to the source of $M_{1}$. The reader can prove that the feedback is indeed negative. To compute the output resistance at relatively low frequencies, we set the input to zero [Fig. 8.9(b)] and write

$$
\begin{equation*}
I_{D 1}=V_{X} \frac{C_{1}}{C_{1}+C_{2}} g_{m 2} \frac{R_{S}}{R_{S}+\frac{1}{g_{m 1}+g_{m b 1}}} \tag{8.16}
\end{equation*}
$$

image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: s1d2, D: Vout, G: Vin}
name: M2, type: NMOS, ports: {S: GND, D: s1d2, G: Vout}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: RS, type: Resistor, value: RS, ports: {N1: s1d2, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: P}
name: C2, type: Capacitor, value: C2, ports: {Np: P, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a common-source stage with feedback, where M1 and M2 are NMOS transistors. M1 senses the input voltage Vin and M2 senses the output voltage Vout. Capacitors C1 and C2 form a feedback network. The output is taken at Vout.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: s1d2, D: Vout, G: Vin}
name: M2, type: NMOS, ports: {S: GND, D: s1d2, G: Vout}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: RS, type: Resistor, value: RS, ports: {N1: s1d2, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: s1d2}
name: C2, type: Capacitor, value: C2, ports: {Np: s1d2, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a common-source (CS) amplifier stage with feedback, used to sense output voltage and provide negative feedback. The feedback is implemented using capacitors C1 and C2, and transistors M1 and M2 form the main amplification stage.

(a)
image_name:Figure 8.9 (a)
description:
[
name: M1, type: NMOS, ports: {S: s1d2, D: Vx, G: Vin}
name: M2, type: NMOS, ports: {S: GND, D: s1d2, G: Vx}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vx}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: s1d2}
name: C1, type: Capacitor, value: C1, ports: {Np: Vx, Nn: P}
name: C2, type: Capacitor, value: C2, ports: {Np: P, Nn: GND}
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Vx, Nn: GND}
]
extrainfo:The circuit is a common-source (CS) amplifier stage with feedback. Transistors M1 and M2 form the main amplification stage. Capacitors C1 and C2 are used for negative feedback to sense output voltage. The circuit is designed to decrease the output resistance by implementing feedback.

(b)

Figure 8.9 (a) CS stage with feedback; (b) calculation of output resistance.
Since $I_{X}=V_{X} / R_{D}+I_{D 1}$, we have

$$
\begin{equation*}
\frac{V_{X}}{I_{X}}=\frac{R_{D}}{1+\frac{g_{m 2} R_{S}\left(g_{m 1}+g_{m b 1}\right) R_{D}}{\left(g_{m 1}+g_{m b 1}\right) R_{S}+1} \frac{C_{1}}{C_{1}+C_{2}}} \tag{8.17}
\end{equation*}
$$

Equation (8.17) implies that this type of feedback decreases the output resistance. The denominator of (8.17) is indeed equal to one plus the loop gain.

Bandwidth Modification. The next example illustrates the effect of negative feedback on the bandwidth. Suppose the feedforward amplifier has a one-pole transfer function:

$$
\begin{equation*}
A(s)=\frac{A_{0}}{1+\frac{s}{\omega_{0}}} \tag{8.18}
\end{equation*}
$$

[^46]where $A_{0}$ denotes the low-frequency gain and $\omega_{0}$ is the $3-\mathrm{dB}$ bandwidth. What is the transfer function of the closed-loop system? From (8.5), we have
\$\$

$$
\begin{align*}
\frac{Y}{X}(s) & =\frac{\frac{A_{0}}{1+\frac{s}{\omega_{0}}}}{1+\beta \frac{A_{0}}{1+\frac{s}{\omega_{0}}}}  \tag{8.19}\\
& =\frac{A_{0}}{1+\beta A_{0}+\frac{s}{\omega_{0}}}  \tag{8.20}\\
& =\frac{\frac{A_{0}}{1+\beta A_{0}}}{1+\frac{s}{\left(1+\beta A_{0}\right) \omega_{0}}} \tag{8.21}
\end{align*}
$$

\$\$

The numerator of (8.21) is simply the closed-loop gain at low frequencies-as predicted by (8.5)-and the denominator reveals a pole at $\left(1+\beta A_{0}\right) \omega_{0}$. Thus, the $3-\mathrm{dB}$ bandwidth has increased by a factor of $1+\beta A_{0}$, albeit at the cost of a proportional reduction in the gain (Fig. 8.10).
image_name:Figure 8.10 Bandwidth modification as a result of feedback
description:The graph in Figure 8.10 is a Bode plot illustrating the effect of feedback on the bandwidth of a system. It is composed of a magnitude plot showing the relationship between the gain |Y/X| and the frequency \( \omega \).

1. **Axes Labels and Units:**
- The horizontal axis represents frequency \( \omega \), likely in radians per second (rad/s), though the specific unit is not labeled.
- The vertical axis represents the magnitude of the gain |Y/X|, with reference levels indicated at \( A_0 \) and \( \frac{A_0}{1 + \beta A_0} \) which approximates \( \frac{1}{\beta} \).

2. **Overall Behavior and Trends:**
- The plot starts at a high gain level \( A_0 \) at low frequencies.
- As frequency increases, the gain decreases, exhibiting a slope that indicates a reduction in gain with increasing frequency.
- There is a distinct change in slope at two key frequency points: \( \omega_0 \) and \( (1 + \beta A_0) \omega_0 \).

3. **Key Features and Technical Details:**
- The initial gain level is \( A_0 \) at low frequencies, representing the open-loop gain.
- The gain decreases to \( \frac{A_0}{1 + \beta A_0} \) at higher frequencies, indicating the closed-loop gain.
- The bandwidth of the system is increased by a factor of \( 1 + \beta A_0 \), as shown by the extension from \( \omega_0 \) to \( (1 + \beta A_0) \omega_0 \).
- This increase in bandwidth comes with a proportional reduction in gain, demonstrating the trade-off between gain and bandwidth in feedback systems.

4. **Annotations and Specific Data Points:**
- The plot includes horizontal lines marking the gain levels \( A_0 \) and \( \frac{1}{\beta} \).
- Vertical dashed lines highlight the cutoff frequencies \( \omega_0 \) and \( (1 + \beta A_0) \omega_0 \), indicating the transition points for the bandwidth increase due to feedback.

This Bode plot effectively illustrates the concept that feedback can increase the bandwidth of a system while simultaneously reducing its gain, a principle fundamental to control systems and signal processing.

Figure 8.10 Bandwidth modification as a result of feedback.
The increase in the bandwidth fundamentally originates from the gain desensitization property of feedback. Recall from (8.6) that, if $A$ is large enough, the closed-loop gain remains approximately equal to $1 / \beta$ even if $A$ experiences substantial variations. In the example of Fig. $8.10, A$ varies with frequency rather than process or temperature, but negative feedback still suppresses the effect of this variation. Of course, at high frequencies, $A$ drops to such low levels that $\beta A$ becomes comparable with unity and the closed-loop gain falls below $1 / \beta$.

Equation (8.21) suggests that the "gain-bandwidth product" of a one-pole system is equal to $A_{0} \omega_{0}$ and does not change much with feedback, making the reader wonder how feedback improves the speed if a high gain is required. Suppose we need to amplify a 20-MHz square wave by a factor of 100 and maximum bandwidth, but we have only a single-pole amplifier with an open-loop gain of 100 and 3-dB bandwidth of 10 MHz . If the input is applied to the open-loop amplifier, the response appears as shown in Fig. 8.11(a), exhibiting a long risetime and falltime because the time constant is equal to $1 /\left(2 \pi f_{3-\mathrm{dB}}\right) \approx 16 \mathrm{~ns}$.

Now suppose we apply feedback to the amplifier such that the gain and bandwidth are modified to 10 and 100 MHz , respectively. Placing two of these amplifiers in a cascade [Fig. 8.11(b)], we obtain a much faster response with an overall gain of 100 . Of course, the cascade consumes twice as much power, but it would be quite difficult to achieve this performance with the original amplifier even if its power dissipation were doubled.

Nonlinearity Reduction An important property of negative feedback is the reduction of nonlinearity in analog circuits. A nonlinear characteristic is one that departs from a straight line, i.e., one whose slope varies (Fig. 8.12). A familiar example is the input-output characteristic of differential pairs. Note that
image_name:(a)
description:The diagram labeled as (a) illustrates the amplification of a 20-MHz square wave using a single amplifier. The main components of this system include:

1. **Amplifier Block**:
- **Type**: Single amplifier
- **3-dB Bandwidth (f₃₋dB)**: 10 MHz
- **Voltage Gain (Aᵥ)**: 100
- **Function**: Amplifies the input signal (Vᵢₙ) to produce an output signal (Vₒᵤₜ).

2. **Input and Output Signals**:
- **Input Signal (Vᵢₙ)**: A square wave with a frequency of 20 MHz.
- **Output Signal (Vₒᵤₜ)**: The amplified version of the input signal, showing a rise and fall time characteristic.

3. **Signal Flow and Characteristics**:
- The input signal (Vᵢₙ) is fed into the amplifier block.
- The output signal (Vₒᵤₜ) is generated after amplification, showing a significant rise time of approximately 16 nanoseconds (τ ≈ 16 ns).

4. **Overall System Function**:
- The primary function of this system is to amplify the 20-MHz square wave input using a single amplifier with a 10 MHz bandwidth and a gain of 100. However, due to the bandwidth limitation, the output signal exhibits a noticeable rise time, indicating slower response to the high-frequency input.
image_name:(b)
description:The graph labeled as (b) illustrates the input-output characteristics of a cascade of two 100-MHz feedback amplifiers when amplifying a 20-MHz square wave. This is a time-domain waveform where the horizontal axis represents time (t) and the vertical axis represents the output voltage (V_out). The input (V_in) is a square wave, and the output is also expected to be a square wave but with some distortion due to the amplifier's characteristics.

**Type of Graph and Function**:
This is a time-domain waveform graph showing the response of an amplifier to a square wave input.

**Axes Labels and Units**:
- The horizontal axis represents time (t), likely in nanoseconds (ns), although not explicitly labeled.
- The vertical axis represents the output voltage (V_out).

**Overall Behavior and Trends**:
- The graph shows a rapid rise and fall in the output voltage corresponding to the rising and falling edges of the input square wave.
- The rise and fall times are significantly reduced compared to a single amplifier setup, indicating faster response due to the cascaded amplifiers.

**Key Features and Technical Details**:
- The time constant (τ) for the rise and fall times is approximately 1.6 ns, indicating a very fast response time.
- Each amplifier in the cascade has a bandwidth of 100 MHz and a gain (A_v) of 10.
- The cascade effectively improves the speed of the output waveform compared to a single amplifier setup.

**Annotations and Specific Data Points**:
- The graph is annotated with τ ≈ 1.6 ns, highlighting the rapid transition times achieved by the cascade of amplifiers.
- The input is a square wave, and the output closely follows this shape but with improved rise and fall times due to the high bandwidth and gain of the cascade setup.

Figure 8.11 Amplification of a 20-MHz square wave by (a) a 10-MHz amplifier and (b) a cascade of two $100-\mathrm{MHz}$ feedback amplifiers.
image_name:Figure 8.12 (a)
description:The graph in Figure 8.12 (a) is a plot of the input-output characteristic of a nonlinear amplifier before applying feedback. It is a typical Cartesian graph with the horizontal axis labeled \( V_{in} \) representing the input voltage, and the vertical axis labeled \( V_{out} \) representing the output voltage. Both axes are likely in volts, though specific units are not provided.

Type of Graph and Function:
This is an input-output characteristic curve, which is commonly used to illustrate how the output of a system (in this case, an amplifier) responds to different levels of input. The curve is nonlinear, indicating a nonlinear relationship between input and output voltages.

Axes Labels and Units:
- **Horizontal Axis (\( V_{in} \))**: Represents input voltage.
- **Vertical Axis (\( V_{out} \))**: Represents output voltage.
- Units are not specified, but typically these would be in volts.

Overall Behavior and Trends:
The graph shows a nonlinear increase in output voltage as the input voltage increases. Initially, for small values of \( V_{in} \), the graph starts with a steep slope, indicating high gain (denoted as \( A_1 \)). As \( V_{in} \) increases, the slope of the curve decreases, indicating a reduction in gain, which is marked as \( A_2 \). This suggests that the amplifier is saturating, which is typical behavior for nonlinear amplifiers.

Key Features and Technical Details:
- **\( A_1 \) and \( A_2 \)**: These represent different gain levels at different regions of the input voltage. \( A_1 \) is the initial, higher gain, while \( A_2 \) is the reduced gain as the amplifier approaches saturation.
- The curve does not show any linear region, indicating that the amplifier is inherently nonlinear across the range of input voltages shown.

Annotations and Specific Data Points:
- The graph is annotated with \( A_1 \) and \( A_2 \), representing the different gain levels at different input voltage regions. These annotations help in understanding the gain variation due to the nonlinear nature of the amplifier.

This graph is crucial for understanding how the amplifier behaves without feedback, showing its inherent nonlinearity and gain variation across different input levels.
image_name:Figure 8.12 (b)
description:The graph labeled as Figure 8.12 (b) depicts the input-output characteristic of a nonlinear amplifier after applying feedback. This is a typical V-out versus V-in plot, where the x-axis represents the input voltage (V_in) and the y-axis represents the output voltage (V_out). Both axes use a linear scale.

**Type of Graph and Function:**
This is a characteristic curve graph showing the relationship between input and output voltages for a feedback amplifier. It illustrates how feedback affects the amplifier's linearity and gain.

**Axes Labels and Units:**
- **X-axis (V_in):** Input voltage (units not specified, but typically in volts).
- **Y-axis (V_out):** Output voltage (units not specified, but typically in volts).

**Overall Behavior and Trends:**
The graph shows a generally linear relationship between V_in and V_out, indicating improved linearity due to feedback. The slope of the curve is less steep compared to the open-loop configuration, suggesting a reduction in gain but an increase in linearity.

**Key Features and Technical Details:**
- The graph is linear over a wider range of input voltages compared to a nonlinear amplifier without feedback.
- The slope of the line is marked as 1/β, which represents the small-signal gain of the feedback amplifier. This indicates that the feedback reduces the open-loop gain, stabilizing it over a broader input range.

**Annotations and Specific Data Points:**
- The annotation 1/β highlights the reduced gain due to feedback, which is a key characteristic of closed-loop amplifiers. This gain is more consistent across different input levels compared to the varying gain in the open-loop configuration shown in Figure 8.12 (a).

Figure 8.12 Input-output characteristic of a nonlinear amplifier (a) before and (b) after applying feedback.
the slope can be viewed as the small-signal gain. We predict that, even though the gain of an open-loop amplifier varies from $A_{1}$ to $A_{2}$ in Fig. 8.12, a closed-loop feedback system incorporating such an amplifier exhibits less gain variation and hence a higher linearity. To quantify this effect, we note that the open-loop gain ratio between regions 1 and 2 in Fig. 8.12 is equal to

$$
\begin{equation*}
r_{\text {open }}=\frac{A_{2}}{A_{1}} \tag{8.22}
\end{equation*}
$$

For example, $r_{\text {open }}=0.9$ means that the gain falls by $10 \%$ from region 1 to region 2 . Assuming $A_{2}=$ $A_{1}-\Delta A$, we can write

$$
\begin{equation*}
r_{\text {open }}=1-\frac{\Delta A}{A_{1}} \tag{8.23}
\end{equation*}
$$

Let us place this amplifier in a negative-feedback loop. For the closed-loop gain ratio, we have

$$
\begin{align*}
r_{\text {closed }} & =\frac{\frac{A_{2}}{1+\beta A_{2}}}{\frac{A_{1}}{1+\beta A_{1}}}  \tag{8.24}\\
& =\frac{1+\frac{1}{\beta A_{1}}}{1+\frac{1}{\beta A_{2}}} \tag{8.25}
\end{align*}
$$

It follows that

$$
\begin{align*}
r_{\text {closed }} & \approx 1-\frac{\frac{1}{\beta A_{2}}-\frac{1}{\beta A_{1}}}{1+\frac{1}{\beta A_{2}}}  \tag{8.26}\\
& \approx 1-\frac{A_{1}-A_{2}}{1+\beta A_{2}} \frac{1}{A_{1}}  \tag{8.27}\\
& \approx 1-\frac{\Delta A}{1+\beta A_{2}} \frac{1}{A_{1}} \tag{8.28}
\end{align*}
$$

Comparison of (8.23) and (8.28) suggests that the gain ratio is much closer to 1 in the latter if the loop gain, $1+\beta A_{2}$, is large.

We study nonlinearity and its behavior in feedback systems more extensively in Chapter 14.

### 8.1.2 Types of Amplifiers

Most of the circuits studied thus far can be considered "voltage amplifiers" because they sense a voltage at the input and produce a voltage at the output. However, three other types of amplifiers can also be constructed such that they sense or produce currents. Shown in Fig. 8.13, the four configurations have quite different properties: (1) circuits sensing a voltage must exhibit a high input impedance (a voltmeter measures a voltage with minimal loading) whereas those sensing a current must provide a low input impedance (a current meter inserted in a wire must negligibly disturb the current); (2) circuits generating a voltage must exhibit a low output impedance (as a voltage source) while those generating a current must provide a high output impedance (as a current source). Note that the gains of transimpedance and transconductance ${ }^{5}$ amplifiers have a dimension of resistance and conductance, respectively. For example, a transimpedance amplifier may have a gain of $2 \mathrm{k} \Omega$, which means that it produces a $2-\mathrm{V}$ output in response to a $1-\mathrm{mA}$ input. Also, we use the sign conventions depicted in Fig. 8.13; for example, the transimpedance $R_{0}=V_{\text {out }} / I_{\text {in }}$ if $I_{\text {in }}$ flows into the amplifier.

Voltage Amp
image_name:Voltage Amp
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Vout, type: VoltageSource, value: Vout, ports: {Np: Vout, Nn: GND}
name: Inverter, type: Inverter, ports: {In: Vin, Out: Vout}
]
extrainfo:The circuit diagram represents a voltage amplifier with an inverter configuration. The input voltage source Vin is connected to the input of the inverter, and the output is taken from Vout. Both Vin and Vout are referenced to the ground.
image_name:Transimpedance Amp.
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Vout, type: VoltageSource, value: Vout, ports: {Np: Vout, Nn: GND}
name: Inverter, type: Inverter, ports: {In: Vin, Out: Vout}
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Vout, type: VoltageSource, value: Vout, ports: {Np: Vout, Nn: GND}
name: VoltageControlledVoltageSource, type: VoltageControlledVoltageSource, ports: {N1: Vin, N2: GND, N3: Vout, N4: GND}
]
extrainfo:The diagram represents a transimpedance amplifier configuration. It includes two sections: an inverter and a voltage-controlled voltage source, both connected between Vin and Vout, with GND as the common reference node. The inverter and voltage-controlled voltage source indicate a feedback mechanism to achieve transimpedance amplification.
image_name:Transconductance Amp.
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Vout, type: VoltageSource, value: Vout, ports: {Np: Vout, Nn: GND}
name: Inverter, type: Inverter, ports: {In: Vin, Out: Vout}
]
extrainfo:The circuit diagram represents a transconductance amplifier. It consists of an inverter connected between the input voltage source Vin and the output voltage source Vout. The circuit is grounded.
image_name:Current Amp.
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Vout, type: VoltageSource, value: Vout, ports: {Np: Vout, Nn: GND}
name: Inverter, type: Inverter, ports: {In: Vin, Out: Vout}
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Vout, type: VoltageSource, value: Vout, ports: {Np: Vout, Nn: GND}
name: VoltageControlledVoltageSource, type: VoltageControlledVoltageSource, ports: {N1: Vin, N2: GND, N3: Vout, N4: GND}
]
extrainfo:The circuit diagram represents a current amplifier configuration. The inverter is connected between Vin and Vout, and a voltage-controlled voltage source is also present, indicating a feedback mechanism for amplification.

(a)

Transimpedance Amp.
image_name:(a) Transimpedance Amp.
description:
[
name: Inv, type: Inverter, ports: {In: Iin, Out: Vout}
name: Vout, type: VoltageSource, value: Vout, ports: {Np: Vout, Nn: GND}
name: VoltageControlledVoltageSource, type: VoltageControlledVoltageSource, ports: {N1: Iin, N2: GND, N3: Vout, N4: GND}
]
extrainfo:The circuit diagram represents a transimpedance amplifier configuration. It includes an inverter and a voltage-controlled voltage source, indicating a feedback mechanism to convert input current (Iin) to output voltage (Vout).
image_name:(b) Transconductance Amp.
description:
[
name: Inv, type: Inverter, ports: {In: Iin, Out: Vout}
name: Vout, type: VoltageSource, value: Vout, ports: {Np: Vout, Nn: GND}
name: VoltageControlledVoltageSource, type: VoltageControlledVoltageSource, ports: {N1: Iin, N2: GND, N3: Vout, N4: GND}
]
extrainfo:The circuit diagram represents a transconductance amplifier configuration. It includes an inverter connected between the input current (Iin) and the output voltage (Vout), along with a voltage-controlled voltage source for amplification.

(b)

Transconductance Amp.
image_name:Transconductance Amp.
description:The transconductance amplifier diagram consists of two main components: a triangular amplifier symbol and a current source symbol.

1. **Main Components:**
- **Amplifier (Triangle Symbol):** This component is responsible for converting an input voltage (Vin) into an output current (Iout). The amplifier is connected to the voltage input on its left side and outputs a current on its right side.
- **Current Source Symbol:** Below the amplifier, there is a current source symbol that also indicates the conversion from input voltage to output current, reinforcing the transconductance function.

2. **Flow of Information or Control:**
- **Input Voltage (Vin):** The voltage input is applied to the left side of the amplifier. It is labeled with a positive and negative sign to indicate the polarity.
- **Output Current (Iout):** The output is a current that flows from the right side of the amplifier and the current source symbol. This current is the result of the voltage-to-current conversion process.

3. **Labels, Annotations, and Key Indicators:**
- The input is labeled as Vin, and the output is labeled as Iout, indicating the transformation from voltage input to current output.
- Ground symbols are present to indicate the common reference point for the circuit.

4. **Overall System Function:**
- The primary function of this transconductance amplifier is to convert an input voltage (Vin) into an output current (Iout). This is achieved through the amplifier, which processes the voltage input and outputs a proportional current. The inclusion of a current source symbol further emphasizes the current output nature of this amplifier configuration. The system is designed to effectively manage the conversion with clear input and output labeling and grounding for stability.
image_name:Current Amp.
description:
[
name: Iout, type: VoltageControlledCurrentSource, ports: {Np: Vin, Nn: Iout}
name: Iout, type: CurrentSource, ports: {Np: Vin, Nn: GND}
]
extrainfo:The circuit diagram represents a current amplifier configuration. It includes a voltage-controlled current source and a current source, both controlled by the input voltage Vin, to provide the output current Iout.

(c)

Current Amp.

image_name:Figure 8.13 Types of amplifiers along with their idealized models
description:The system block diagram titled "Figure 8.13 Types of amplifiers along with their idealized models" illustrates two types of amplifier configurations.

1. **Main Components:**
- The top part of the diagram depicts a simple amplifier block, represented as a triangle, with an input labeled \( I_{in} \) and an output labeled \( I_{out} \). This symbolizes a generic amplifier that takes an input current and produces an output current.
- The bottom part of the diagram shows a more detailed configuration with a current source symbol and grounding symbols. It includes an input \( I_{in} \) and an output \( I_{out} \), with the current source connected between the input and output paths.

2. **Flow of Information or Control:**
- In the top configuration, the input current \( I_{in} \) enters the amplifier block and is processed to produce the output current \( I_{out} \). The direction is straightforward from input to output.
- In the bottom configuration, the input current \( I_{in} \) is fed into the circuit, where it is combined with a current source to produce the output current \( I_{out} \). The grounding symbols indicate that the circuit is referenced to a common ground, ensuring stability and proper operation.

3. **Labels, Annotations, and Key Indicators:**
- The labels \( I_{in} \) and \( I_{out} \) are used in both parts of the diagram to indicate the input and output currents, respectively.
- The triangle symbol in the top configuration represents an amplifier, a common symbol in electronics to denote signal amplification.
- The current source symbol in the bottom configuration indicates that the output current is controlled by an internal or external current source mechanism.

4. **Overall System Function:**
- The primary function of these diagrams is to illustrate different amplifier configurations and their idealized models. The top configuration represents a basic amplifier model that amplifies input current to produce an output current. The bottom configuration shows a more complex setup where an input current is modified by a current source to achieve the desired output current. Both configurations highlight the role of amplifiers in controlling and modifying current flow in electronic circuits.
image_name:Current Amp.
description:
[
name: I_in, type: Diode, ports: {Na: Iin, Nc: GND}
name: I_out, type: Diode, ports: {Na: Vin, Nc: Iout}
name: Inverter, type: Inverter, ports: {In: Vin, Out: Iout}
name: CurrentSource, type: CurrentSource, ports: {Np: Vin, Nn: GND}
]
extrainfo:The circuit diagram represents a current amplifier configuration, utilizing a voltage-controlled current source and a current source to amplify the input current Iin to produce the output current Iout.

(d)

Figure 8.13 Types of amplifiers along with their idealized models.

[^47]image_name:(d)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit diagram represents a simple NMOS amplifier configuration. It uses an NMOS transistor M1 to amplify the input voltage Vin to produce the output voltage Vout. The resistor RD is used as a load resistor, and VDD is the supply voltage.

(a)
image_name:Figure 8.14(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: Vin, Nn: GND}
]
extrainfo:The circuit diagram represents a simple NMOS amplifier configuration. It uses an NMOS transistor M1 to amplify the input voltage Vin to produce the output voltage Vout. The resistor RD is used as a load resistor, and VDD is the supply voltage.

(b)
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: LOAD, type: Diode, ports: {Na: Vout, Nc: VDD}
]
extrainfo:The circuit diagram represents a common-gate NMOS amplifier configuration. The input voltage Vin is applied to the gate of the NMOS transistor M1. The output voltage Vout is taken from the drain, which is connected to a diode acting as a load.

(c)
image_name:(c)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Iout, G: Vin}
name: LOAD, type: Diode, ports: {Na: Iout, Nc: VDD}
]
extrainfo:The circuit diagram shows a common-gate NMOS amplifier configuration with a diode as the load. The input voltage Vin is applied to the gate of the NMOS transistor M1, and the output is taken from the drain, which is connected to the diode acting as a load.

(d)

Figure 8.14 Simple implementations of four types of amplifiers.

Figure 8.14 illustrates simple implementations of each amplifier. In Fig. 8.14(a), a common-source stage senses and produces Voltages, and in Fig. 8.14(b), a common-gate circuit serves as a transimpedance amplifier, converting the source current to a voltage at the drain. In Fig. 8.14(c), a common-source transistor operates as a transconductance amplifier (also called a $V / I$ converter), generating an output current in response to an input voltage, and in Fig. 8.14(d), a common-gate device senses and produces currents.

The circuits of Fig. 8.14 may not provide adequate performance in many applications. For example, the circuits of Figs. 8.14(a) and (b) suffer from a relatively high output impedance. Figure 8.15 depicts modifications that alter the output impedance or increase the gain.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1s2, G: Vin}
name: M2, type: NMOS, ports: {S: d1s2, D: Vout, G: d1s2}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: d1s2}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a transconductance amplifier with NMOS transistors M1 and M2. M1 is configured with its gate connected to Vin, and M2 is configured as a current mirror with its source connected to the drain of M1. The resistor RD is connected to VDD and the drain of M1. The output current is taken at Vout.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1g2, G: Vin}
name: M2, type: NMOS, ports: {S: d1g2, D: Vout, G: Vb}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: d1g2}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit diagram (b) is a modified amplifier with improved output impedance. It uses two NMOS transistors M1 and M2, a resistor RD, and a current source I1. The node d1g2 is a common node connecting the drain of M1, the source of M2, and one terminal of RD. The bias voltage Vb is applied to the gate of M2.
image_name:(c)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1s1, G: Vin}
name: M2, type: NMOS, ports: {S: d1s1, D: Vout, G: Vb}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: d1s1}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a transconductance amplifier with improved performance, featuring two NMOS transistors and a resistor to adjust output impedance and gain. The gain is defined as Gm = Iout / Vin.
image_name:(d)
description:
[
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: d1s1}
name: M1, type: NMOS, ports: {S: s1, D: d1s1, G: Vin}
name: M2, type: NMOS, ports: {S: d1s1, D: Vout, G: Vb}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vin, Nn: GND}
name: LOAD, type: CurrentSource, value: LOAD, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a modified amplifier with NMOS transistors M1 and M2. The load current source is connected at the output to improve performance. The gain is defined by the transconductance and output impedance.

Figure 8.15 Four types of amplifiers with improved performance.

#### Example 8.2

Calculate the gain of the transconductance amplifier shown in Fig. 8.15(c).

#### Solution

The gain in this case is defined as $G_{m}=I_{\text {out }} / V_{\text {in }}$. That is

$$
\begin{align*}
G_{m} & =\frac{V_{X}}{V_{\text {in }}} \cdot \frac{I_{\text {out }}}{V_{X}}  \tag{8.29}\\
& =-g_{m 1}\left(r_{O 1} \| R_{D}\right) \cdot g_{m 2} \tag{8.30}
\end{align*}
$$

While most familiar amplifiers are of the voltage-voltage type, the other three configurations do find usage. For example, transimpedance amplifiers are an integral part of optical fiber receivers because they must sense the current produced by a photodiode, eventually generating a voltage that can be processed by subsequent circuits.

#### Example 8.3

Reconstruct the models of Fig. 8.13 for nonideal amplifiers.

#### Solution

A nonideal voltage amplifier draws current from its input and exhibits a finite output impedance, as depicted in Fig. 8.16(a).
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Zin, type: Resistor, value: Zin, ports: {N1: Vin, N2: AvVin}
name: AvVin, type: VoltageControlledVoltageSource, value: AvVin, ports: {Np: AvVin, Nn: GND}
name: Zout, type: Resistor, value: Zout, ports: {N1: AvVin, N2: Vout}
]
extrainfo:The circuit diagram (a) represents a nonideal voltage amplifier with input impedance Zin and output impedance Zout. The voltage source AvVin models the voltage gain of the amplifier.
image_name:(b)
description:
[
name: Zin, type: Resistor, value: Zin, ports: {N1: Iin, N2: GND}
name: RoIin, type: VoltageControlledVoltageSource, ports: {Np: Iin, Nn: GND}
name: Zout, type: Resistor, value: Zout, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit diagram represents a nonideal transimpedance amplifier with finite input and output impedances. The input impedance Zin is in series with the input current Iin, and the output impedance Zout is in series with the output voltage Vout. The voltage-controlled voltage source RoIin provides the output voltage based on the input current.
image_name:(c)
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: Zin, type: Resistor, value: Zin, ports: {N1: Vin, N2: GmVin}
name: GmVin, type: VoltageControlledCurrentSource, value: GmVin, ports: {Np: GmVin, Nn: Iout}
name: Zout, type: Resistor, value: Zout, ports: {N1: Iout, N2: GND}
]
extrainfo:The circuit represents a nonideal transimpedance amplifier model with finite input and output impedances. It converts an input voltage to an output current.
image_name:(d)
description:
[
name: Iin, type: CurrentSource, ports: {Np: Vin, Nn: GND}
name: Zin, type: Resistor, value: Zin, ports: {N1: Vin, N2: GND}
name: AoIin, type: CurrentControlledCurrentSource, value: AoIin, ports: {Np: Vin, Nn: Vout}
name: Zout, type: Resistor, value: Zout, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit in diagram (d) represents a nonideal transimpedance amplifier with an input current source and a current-controlled current source. It includes input and output impedances.

Figure 8.16

A nonideal transimpedance amplifier may have finite input and output impedances [Fig. 8.16(b)]. Note that $Z_{\text {in }}$ is in parallel with the input port in Fig. 8.16(a) and in series with the input port in Fig. 8.16(b). This is to ensure a meaningful result in the ideal case: if $Z_{\text {in }}$ goes to infinity in the former or to zero in the latter, the models reduce to those of Fig. 8.13.

The reader is encouraged to justify the models shown in Figs. 8.16(c) and (d) for the other two amplifier types. We should mention that these amplifiers may also have internal feedback from their output to their input, e.g., due to $C_{G D}$, but we neglect that for now.

### 8.1.3 Sense and Return Mechanisms

Placing a circuit in a feedback loop requires sensing the output signal and returning (a fraction) of the result to the summing node at the input. With voltage or current quantities as input and output signals, we can identify four types of feedback: voltage-voltage, voltage-current, current-current, and currentvoltage, where the first entry in each case denotes the quantity sensed at the output and the second the type of signal returned to the input. ${ }^{6}$

It is instructive to review methods of sensing and summing voltages or currents. To sense a voltage, we place a voltmeter in parallel with the corresponding port [Fig. 8.17(a)], ideally introducing no loading.
image_name:(a)
description:
[
name: Vout, type: VoltageSource, value: Vout, ports: {Np: Vout, Nn: GND}
name: Voltmeter, type: Other, ports: {N1: Vout, N2: GND}
]
extrainfo:The diagram (a) shows a voltage sensing circuit using a voltmeter connected in parallel with the output voltage source Vout. This setup is used to sense the voltage without loading the circuit.
image_name:(b)
description:
[
name: Vout, type: VoltageSource, value: Vout, ports: {Np: Vout, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Iout, N2: GND}
]
extrainfo:The diagram shows a current sensing setup using a current meter in series with a load resistor RL. The current Iout flows through the load RL.
image_name:(c)
description:
[
name: V_out, type: VoltageSource, value: V_out, ports: {Np: I_out, Nn: GND}
name: R_L, type: Resistor, value: R_L, ports: {N1: I_out, N2: GND}
name: R_S, type: Resistor, value: R_S, ports: {N1: GND, N2: V_S}
name: V_S, type: VoltageSource, value: V_S, ports: {Np: V_S, Nn: GND}
]
extrainfo:The circuit diagram (c) shows a current sensing setup using a small resistor R_S to measure the current I_out flowing through the load resistor R_L. The voltage source V_S is used to detect the current by measuring the voltage drop across R_S.

Figure 8.17 Sensing (a) a voltage by a voltmeter; (b) a current by a current meter; (c) a current by a small resistor.

[^48]When used in a feedback system, this type of sensing is also called "shunt feedback" (regardless of the quantity returned to the input).

To sense a current, a current meter is inserted in series with the signal [Fig. 8.17(b)], ideally exhibiting zero series resistance. Thus, this type of sensing is also called "series feedback." In practice, a small resistor replaces the current meter [Fig. 8.17(c)], with the voltage drop across the resistor serving as a measure of the output current.

The addition of the feedback signal and the input signal can be performed in the voltage domain or current domain. To add two quantities, we place them in series if they are voltages and in parallel if they are currents (Fig. 8.18).
image_name:Figure 8.18 Addition of (a) voltages
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: VF}
name: VF, type: VoltageSource, value: VF, ports: {Np: VF, Nn: GND}
]
extrainfo:The circuit diagram represents the addition of two voltages, Vin and VF, connected in series.

(a)
image_name:(b)
description:
[
name: Iin, type: CurrentSource, value: Iin, ports: {Np: Vin, Nn: GND}
name: IF, type: CurrentSource, value: IF, ports: {Np: Vin, Nn: GND}
]
extrainfo:The circuit diagram represents the addition of two currents, Iin and IF, connected in parallel.

(b)

Figure 8.18 Addition of (a) voltages and (b) currents.

To visualize the methods of Figs. 8.17 and 8.18, we consider a number of practical implementations. A voltage can be sensed by a resistive (or capacitive) divider in parallel with the port [Fig. 8.19(a)] and a
image_name:(a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vout, N2: VF}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: Vin, Nn: GND}
name: IF, type: CurrentSource, value: IF, ports: {Np: Vin, Nn: GND}
]
extrainfo:The circuit diagram in figure (a) represents the addition of two currents, Iin and IF, connected in parallel. The output voltage Vout is taken across resistors R1 and R2. The diagram is part of a series illustrating methods for sensing and adding voltages and currents.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: VF, type: VoltageSource, ports: {Np: Vout, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vout, N2: GND}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: VF}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vin, Nn: GND}
]
extrainfo:The circuit diagram (b) shows a configuration for adding two voltages, Vin and VF, using NMOS transistors M1 and M2. The output voltage Vout is connected to resistors R1 and R2, and the current source I1 is used to inject current into the input node Vin.
image_name:(c)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: VF, type: VoltageSource, value: VF, ports: {Np: VF, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vout, N2: VF}
name: Iout, type: CurrentSource, value: Iout, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit diagram (c) represents a voltage addition circuit using an operational amplifier and feedback resistors R1 and R2. The input voltages Vin and VF are added, and the output is taken across R1.
image_name:(d)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vout, N2: VF}
name: M1, type: NMOS, ports: {S: Vin, D: VF, G: P}
name: M2, type: NMOS, ports: {S: Vin, D: VF, G: P}
name: I1, type: CurrentSource, value: I1, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit diagram represents a method for subtracting two voltages using a differential pair of NMOS transistors (M1 and M2). The current source I1 provides a bias current to the gates of the NMOS transistors. The resistors R1 and R2 form a voltage divider at the output node Vout. This configuration allows the subtraction of the voltages Vin and VF, with the resulting voltage difference influencing the output voltage Vout.
image_name:(e)
description:
[
name: M1, type: NMOS, ports: {S: VF, D: Vout, G: Vin}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vout, N2: G1}
]
extrainfo:The circuit diagram (e) represents a voltage subtraction using an NMOS transistor (M1) where the output voltage Vout is derived from the difference between Vin and VF. Resistors R1 and R2 are connected to the output to form a voltage divider.
image_name:(f)
description:
[
name: M1, type: NMOS, ports: {S: VF, D: Vout, G: Vin}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vout, N2: VF}
]
extrainfo:The circuit diagram (f) represents a voltage subtraction using an NMOS transistor. The NMOS transistor M1 is used to subtract the voltage VF from Vin, resulting in Vout. The resistors R1 and R2 form a voltage divider at the output.
image_name:(g)
description:
[
name: Iin, type: CurrentSource, value: Iin, ports: {Np: Iin, Nn: GND}
name: IF, type: CurrentSource, value: IF, ports: {Np: Iin, Nn: GND}
name: RF, type: Resistor, value: RF, ports: {N1: Iin, N2: OpAmpIn}
]
extrainfo:The circuit diagram represents the addition of two currents, Iin and IF, connected in parallel, feeding into an operational amplifier through a resistor RF.
image_name:(h)
description:
[
name: Iin, type: CurrentSource, value: Iin, ports: {Np: Vin, Nn: GND}
name: IF, type: CurrentSource, value: IF, ports: {Np: Vin, Nn: GND}
name: M3, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
]
extrainfo:The circuit diagram represents the addition of two currents, Iin and IF, connected in parallel. An NMOS transistor (M3) is used to control the output voltage (Vout) based on the input voltage (Vin).

Figure 8.19 Practical means of sensing and adding voltages and currents.
current by placing a small resistor in series with the wire and sensing the voltage across it [Figs. 8.19(b) and (c)]. To subtract two voltages, a differential pair can be used [Fig. 8.19(d)]. Alternatively, a single transistor can perform voltage subtraction as shown in Figs. 8.19(e) and (f) because $I_{D 1}$ is a function of $V_{i n}-V_{F}$. Subtraction of currents can be accomplished as depicted in Fig. 8.19(g) or (h). Note that for voltage subtraction, the input and feedback signals are applied to two distinct nodes, whereas for current subtraction, they are applied to a single node. This observation proves helpful in identifying the type of feedback.

While ideally having no influence on the operation of the open-loop amplifier itself, the feedback network in reality introduces loading effects that must be taken into account. This issue is discussed in Sec. 8.5.

## 8.2 ■ Feedback Topologies

In this section, we study four "canonical" topologies resulting from placing each of the four amplifier types in a negative-feedback loop. As depicted in Fig. 8.20, $X$ and $Y$ can be a current or a voltage quantity. The main amplifier is called the "feedforward" or simply the "forward" amplifier, around which we apply feedback to improve the performance.
image_name:Figure 8.20 Canonical feedback system
description:The diagram represents a canonical feedback system consisting of two main components: the Forward Amplifier and the Feedback Network.

1. **Main Components:**
- **Forward Amplifier (H(s))**: This block represents the primary amplifier in the system, responsible for amplifying the input signal. The function H(s) denotes the transfer function of the amplifier, illustrating its behavior in the frequency domain.
- **Feedback Network (G(s))**: This block is responsible for feeding a portion of the output signal back to the input. The transfer function G(s) characterizes how the feedback network processes the signal.

2. **Flow of Information or Control:**
- The input signal, denoted as X(s), enters the system and is first processed by a summing junction.
- At the summing junction, the feedback signal is subtracted from the input signal, creating an error signal that is then fed into the Forward Amplifier H(s).
- The amplified signal from H(s) is output as Y(s), which is the system's output.
- A portion of Y(s) is routed back through the Feedback Network G(s) to the summing junction, completing the feedback loop.

3. **Labels, Annotations, and Key Indicators:**
- The summing junction is marked with '+' and '−' signs to indicate the addition of the input signal and the subtraction of the feedback signal.
- The arrows indicate the direction of signal flow, showing a clear path from input to output and back through the feedback loop.

4. **Overall System Function:**
- The primary function of this feedback system is to improve the performance of the Forward Amplifier by using feedback to control its behavior. This can include stabilizing the gain, reducing distortion, and controlling bandwidth. The feedback loop helps adjust the system's response to changes in input or disturbances, making it a crucial component in achieving desired performance characteristics.

Figure 8.20 Canonical feedback system.

We should remark that some feedback circuits do not conform to the four canonical topologies. We return to this point later in the chapter, but the intuition gained from the analysis of these topologies proves essential to analog design. For example, we greatly benefit from the knowledge that one type of feedback lowers the output impedance while another raises it.

### 8.2.1 Voltage-Voltage Feedback

This topology senses the output voltage and returns the feedback signal as a voltage. ${ }^{7}$ Following the conceptual illustrations of Figs. 8.17 and 8.18, we note that the feedback network is connected in parallel with the output and in series with the input port (Fig. 8.21). An ideal feedback network in this case exhibits infinite input impedance and zero output impedance because it senses a voltage and generates a voltage. We can therefore write $V_{F}=\beta V_{\text {out }}, V_{e}=V_{\text {in }}-V_{F}, V_{\text {out }}=A_{0}\left(V_{\text {in }}-\beta V_{\text {out }}\right)$, and hence

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=\frac{A_{0}}{1+\beta A_{0}} \tag{8.31}
\end{equation*}
$$

We recognize that $\beta A_{0}$ is the loop gain and that the overall gain has dropped by $1+\beta A_{0}$. Note that here both $A_{0}$ and $\beta$ are dimensionless quantities.

As a simple example of voltage-voltage feedback, suppose we employ a differential voltage amplifier with single-ended output as the feedforward amplifier and a resistive divider as the feedback network

[^49]image_name:Figure 8.21 Voltage-voltage feedback
description:The system block diagram, labeled "Figure 8.21 Voltage-voltage feedback," illustrates a voltage-voltage feedback amplifier configuration.

1. **Main Components:**
- **Feedforward Amplifier (A₀):** This block is the primary amplifier in the system, which amplifies the input signal. It is characterized by a gain denoted as A₀.
- **Feedback Network (β):** A resistive divider network that samples the output voltage and provides a portion of it back to the input to form a feedback loop. The feedback factor is represented by β.

2. **Flow of Information or Control:**
- **Input (V_in):** The input voltage is fed into the system at the left side of the diagram.
- **Error Signal (V_e):** The difference between the input voltage (V_in) and the feedback voltage (V_F) is the error signal (V_e), which is input to the feedforward amplifier.
- **Output (V_out):** The amplified output is taken from the feedforward amplifier and is also the point from which feedback is derived.
- **Feedback Path:** The output voltage (V_out) is sampled by the feedback network, which reduces it by a factor of β and feeds it back to the input to form the feedback voltage (V_F).
- **Feedback Loop:** The feedback loop is closed by connecting the output of the feedback network back to the input, influencing the error signal and thus controlling the overall gain of the system.

3. **Labels, Annotations, and Key Indicators:**
- **Low R_out and High R_in:** These indicate that the system is designed to have a low output impedance and a high input impedance, which are desirable traits for voltage amplifiers.
- **A₀ and β:** These are key parameters in determining the system's gain and stability, with A₀ being the open-loop gain and β being the feedback factor.

4. **Overall System Function:**
- The primary function of this system is to provide stable voltage amplification with feedback control. The feedback reduces the overall gain by a factor of (1 + βA₀), enhancing stability and bandwidth while reducing distortion. The system is designed to maintain a low output impedance and high input impedance, making it suitable for driving loads and accepting signals from various sources.

Figure 8.21 Voltage-voltage feedback.
image_name:Figure 8.21 Voltage-voltage feedback
description:
[
name: A0, type: OpAmp, value: A0, ports: {InP: Vin, InN: X1, Out: Vout}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: X1}
name: R2, type: Resistor, value: R2, ports: {N1: X1, N2: GND}
name: VF, type: VoltageSource, value: VF, ports: {Np: X1, Nn: GND}
]
extrainfo:The circuit is a voltage-voltage feedback amplifier with an operational amplifier A0. It uses resistors R1 and R2 to form a feedback network that senses the output voltage. The feedback reduces the overall gain to enhance stability and bandwidth while reducing distortion.

(a)
image_name:(a)
description:
[
name: A0, type: OpAmp, value: A0, ports: {InP: Vin, InN: X1, OutP: Vout, OutN: '}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: X1}
name: R2, type: Resistor, value: R2, ports: {N1: X1, N2: GND'}
]
extrainfo:The circuit is a voltage-voltage feedback amplifier with an operational amplifier A0. It uses resistors R1 and R2 to form a feedback network that senses the output voltage. The feedback reduces the overall gain to enhance stability and bandwidth while reducing distortion. A current named I_in(A0) flows into the negative input of the operational amplifier.

(b)

Figure 8.22 (a) Amplifier with output sensed by a resistive divider; (b) voltage-voltage feedback amplifier.
image_name:Figure 8.23
description:The block diagram in Figure 8.23 represents a voltage-voltage feedback amplifier system. Here are the key components and their interactions:

1. **Main Components:**
- **Operational Amplifier (A0):** This is the central component of the system, amplifying the input signal. It has a gain represented by \( A_0 \) and receives the error voltage \( V_e \) as input.
- **Feedback Network (β):** This block senses the output voltage \( V_{out} \) and produces a feedback voltage \( V_F \), which is a fraction of the output. The feedback network is characterized by the feedback factor \( β \).
- **Output Load (R_L):** This resistor represents the load connected to the output of the amplifier.
- **Output Resistance (R_out):** This is the inherent resistance at the output of the operational amplifier.

2. **Flow of Information or Control:**
- The input voltage \( V_{in} \) is applied to the non-inverting terminal of the operational amplifier.
- The output voltage \( V_{out} \) is fed back through the feedback network \( β \) to produce \( V_F \), which is subtracted from the input voltage \( V_{in} \) to generate the error voltage \( V_e \).
- The error voltage \( V_e \) is then amplified by the operational amplifier \( A_0 \) to produce the amplified output.
- The output voltage \( V_{out} \) is sensed across the load \( R_L \).

3. **Labels, Annotations, and Key Indicators:**
- \( V_{in}^+ \) and \( V_{in}^- \) indicate the positive and negative input terminals of the amplifier.
- \( V_{out}^+ \) and \( V_{out}^- \) mark the positive and negative output terminals.
- The feedback voltage \( V_F \) is derived using the feedback factor \( β \).

4. **Overall System Function:**
- The primary function of this system is to provide stable amplification of the input voltage \( V_{in} \) with reduced distortion and improved bandwidth. The feedback loop, formed by the feedback network (β), reduces the effective gain of the amplifier, thereby enhancing stability and reducing output impedance. This feedback mechanism ensures that any deviation in the output voltage is corrected by adjusting the input to the amplifier, maintaining the desired performance characteristics.

Figure 8.23 Effect of voltage-voltage feedback on output resistance.
[Fig. 8.22(a)]. The divider senses the output voltage, producing a fraction thereof as the feedback signal $V_{F}$. Following the block diagram of Fig. 8.21, we place $V_{F}$ in series with the input of the amplifier to perform subtraction of voltages [Fig. 8.22(b)].

How does voltage-voltage feedback modify the input and output impedances? Let us first consider the output impedance. Recall that a negative-feedback system attempts to make the output an accurate (scaled) replica of the input. Now suppose, as shown in Fig. 8.23, we load the output by a resistor $R_{L}$, gradually decreasing its value. While in the open-loop configuration, the output would simply drop in proportion to $R_{L} /\left(R_{L}+R_{\text {out }}\right)$, in the feedback system, $V_{\text {out }}$ is maintained as a reasonable replica of $V_{\text {in }}$ even though $R_{L}$ decreases. That is, so long as the loop gain remains much greater than unity, $V_{\text {out }} / V_{\text {in }} \approx 1 / \beta$, regardless of the value of $R_{L}$. From another point of view, since the circuit stabilizes ("regulates") the output voltage amplitude despite load variations, it behaves as a voltage source, thus exhibiting a low output impedance. This property fundamentally originates from the gain desensitization provided by feedback.

In order to formally prove that voltage feedback lowers the output impedance, we consider the simple model in Fig. 8.24, where $R_{\text {out }}$ represents the output impedance of the feedforward amplifier. Setting the input to zero and applying a voltage at the output, we write $V_{F}=\beta V_{X}, V_{e}=-\beta V_{X}, V_{M}=-\beta A_{0} V_{X}$,
image_name:Figure 8.24
description:
[
name: A0, type: OpAmp, value: A0, ports: {InP: VF, InN: Ve, OutP: VM, OutN: '}
name: Rout, type: Resistor, value: Rout, ports: {N1: VM, N2: Vx}
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Vx, Nn: GND'}
]
extrainfo:The circuit illustrates a voltage-voltage feedback system where the output impedance is reduced by feedback. The feedback factor is represented by β, and the output impedance Rout is modified by the gain factor A0. The feedback voltage VF is derived from the output voltage Vx.

Figure 8.24 Calculation of output resistance of a voltage-voltage feedback circuit.
and hence $I_{X}=\left[V_{X}-\left(-\beta A_{0} V_{X}\right)\right] / R_{\text {out }}$ (if the current drawn by the feedback network is neglected). It follows that

$$
\begin{equation*}
\frac{V_{X}}{I_{X}}=\frac{R_{\text {out }}}{1+\beta A_{0}} \tag{8.32}
\end{equation*}
$$

Thus, the output impedance and the gain are lowered by the same factor. In the circuit of Fig. 8.22(b), for example, the output impedance is lowered by $1+A_{0} R_{2} /\left(R_{1}+R_{2}\right)$.

#### Example 8.4

The circuit shown in Fig. 8.25(a) is an implementation of the feedback configuration depicted in Fig. 8.22(b), but with the resistors replaced by capacitors. (The bias network of $M_{2}$ is not shown.) Calculate the closed-loop gain and output resistance of the amplifier at relatively low frequencies.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: p}
name: M3, type: PMOS, ports: {S: VDD, D: Vout, G: x1}
name: M4, type: PMOS, ports: {S: VDD, D: x1, G: x1}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: X}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: GND}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: p, Nn: GND}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: Vt, Nn: GND}
]
extrainfo:The circuit is a simple operational amplifier with a differential input and a single-ended output. It utilizes NMOS and PMOS transistors in a complementary configuration. Capacitors C1 and C2 are used for frequency compensation, and a current source Iss provides biasing. The power supply is connected to VDD, and the output is taken from Vout.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: p, D: Vout, G: Vin}
name: M2, type: NMOS, ports: {S: p, D: Vout, G: X1}
name: M3, type: PMOS, ports: {S: VDD, D: X1, G: X1}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: X1}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: X}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: GND}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: p, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: Vt, Nn: GND}
]
extrainfo:The circuit is a simple operational amplifier with NMOS and PMOS transistors. It uses capacitive feedback with C1 and C2 to control the frequency response. The circuit is powered by a VDD voltage source and has a current source Iss for biasing.
image_name:(c)
description:
[
name: M1, type: NMOS, ports: {S: p, D: x, G: Vin}
name: M2, type: NMOS, ports: {S: p, D: Vout, G: VF}
name: M3, type: PMOS, ports: {S: VDD, D: x1, G: x}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: x}
name: C1, type: Capacitor, value: C1, ports: {Np: Vt, Nn: x}
name: C2, type: Capacitor, value: C2, ports: {Np: x, Nn: GND}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: p, Nn: GND}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: Vt, Nn: GND}
]
extrainfo:The circuit in diagram (c) is a simple operational amplifier configuration with feedback capacitors C1 and C2. The NMOS transistors M1 and M2 form a differential pair, while PMOS transistors M3 and M4 act as a current mirror load. The circuit is powered by a voltage source VDD, and a current source Iss is used for biasing. The feedback network includes capacitors C1 and C2, which are connected to the voltage source Vt for loop gain calculation.

Figure 8.25

#### Solution

At low frequencies, $C_{1}$ and $C_{2}$ draw a negligible current from the output node. To find the open-loop voltage gain, we break the feedback loop as shown in Fig. 8.25(b), grounding the top plate of $C_{1}$ to ensure zero voltage feedback. The open-loop gain is thus equal to $g_{m 1}\left(r_{O 2} \| r_{O 4}\right)$.

We must also compute the loop gain, $\beta A_{0}$. With the aid of Fig. 8.25(c), we have

$$
\begin{equation*}
V_{F}=-V_{t} \frac{C_{1}}{C_{1}+C_{2}} g_{m 1}\left(r_{O 2} \| r_{O 4}\right) \tag{8.33}
\end{equation*}
$$

That is

$$
\begin{equation*}
\beta A_{0}=\frac{C_{1}}{C_{1}+C_{2}} g_{m 1}\left(r_{O 2} \| r_{O 4}\right) \tag{8.34}
\end{equation*}
$$

and hence

$$
\begin{equation*}
A_{\text {closed }}=\frac{g_{m 1}\left(r_{O 2} \| r_{O 4}\right)}{1+\frac{C_{1}}{C_{1}+C_{2}} g_{m 1}\left(r_{O 2} \| r_{O 4}\right)} \tag{8.35}
\end{equation*}
$$

As expected, if $\beta A_{0} \gg 1$, then $A_{\text {closed }} \approx 1+C_{2} / C_{1}$.
The open-loop output resistance of the circuit is equal to $r_{O 2} \| r_{O 4}$ (Chapter 5). It follows that

$$
\begin{equation*}
R_{\text {out }, \text { closed }}=\frac{r_{O 2} \| r_{O 4}}{1+\frac{C_{1}}{C_{1}+C_{2}} g_{m 1}\left(r_{O 2} \| r_{O 4}\right)} \tag{8.36}
\end{equation*}
$$

It is interesting to note that if $\beta A_{0} \gg 1$, then

$$
\begin{equation*}
R_{\text {out }, \text { closed }} \approx\left(1+\frac{C_{2}}{C_{1}}\right) \frac{1}{g_{m 1}} \tag{8.37}
\end{equation*}
$$

In other words, even if the open-loop amplifier suffers from a high output resistance, the closed-loop output resistance is independent of $r_{O 2} \| r_{O 4}$, simply because the open-loop gain scales with $r_{O 2} \| r_{O 4}$ as well.

#### Example 8.5

Figure 8.26(a) shows an inverting amplifier using an op amp, and Fig. 8.26(b) illustrates a circuit implementation incorporating capacitors rather than resistors for the feedback network. Determine the loop gain and output impedance of the latter at low frequencies.
image_name:(a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: X1}
name: R2, type: Resistor, value: R2, ports: {N1: Vin, N2: X1}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: X1, OutP: Vout, OutN: ''}
]
extrainfo:The circuit diagram (a) is an inverting amplifier using an op-amp with resistors R1 and R2 forming the feedback network. The input voltage is Vin and the output voltage is Vout.
image_name:(b)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: X1}
name: R2, type: Resistor, value: R2, ports: {N1: Vin, N2: X1}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: X1}
name: C2, type: Capacitor, value: C2, ports: {Np: Vin, Nn: g1}
name: M1, type: NMOS, ports: {S: g1, D: Vout, G: Vb}
name: M2, type: NMOS, ports: {S: Is, D: g1, G: Vb}
name: M3, type: PMOS, ports: {S: VDD, D: X1, G: Vout}
name: M4, type: PMOS, ports: {S: VDD, D: X1, G: Vout}
name: A1, type: OpAmp, value: A1, ports: {InP: g1, InN: X1, OutP: Vout}
name: Is, type: CurrentSource, value: Is, ports: {Np: Is, Nn: GND}
]
extrainfo:The circuit in (b) is an inverting amplifier using capacitors for feedback. It includes an op-amp and a combination of NMOS and PMOS transistors. The gain is determined by the ratio of C2 to C1, and the topology affects the loop gain and output impedance.

Figure 8.26

#### Solution

With $V_{i n}$ set to zero, this circuit becomes indistinguishable from that in Fig. 8.25(a). Thus, the loop gain is given by (8.34) and the output impedance by (8.36).

The circuits in Figs. 8.25(a) and 8.26(b) appear similar, but provide different closed-loop gains, approximately $1+C_{2} / C_{1}$ and $-C_{2} / C_{1}$, respectively. Thus, for a gain of, say, $4, C_{2} / C_{1} \approx 3$ in the former and $C_{2} / C_{1} \approx 4$ in the latter. Which topology exhibits a higher loop gain in this case?

Voltage-voltage feedback also modifies the input impedance. Comparing the configurations in Fig. 8.27, we note that the input impedance of the feedforward amplifier sustains the entire input voltage in Fig. 8.27(a), but only a fraction of $V_{i n}$ in Fig. 8.27(b). As a result, the current drawn by $R_{i n}$ in the feedback topology is less than that in the open-loop system, suggesting that returning a voltage quantity to the input increases the input impedance.
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: Ve}
name: Rin, type: Resistor, value: Rin, ports: {N1: Ve, N2: AoVe}
name: AoVe, type: VoltageControlledVoltageSource, value: AoVe, ports: {Np: AoVe, Nn: Vout}
name: Rout, type: Resistor, value: Rout, ports: {N1: AoVe, N2: Vout}
]
extrainfo:The circuit uses a voltage-voltage feedback configuration to increase input impedance. The input voltage is applied across Rin, and the controlled source AoVe provides amplification. Rout is connected to the output, Vout.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Rin, type: Resistor, value: Rin, ports: {N1: Vip, N2: Ve}
name: Rout, type: Resistor, value: Rout, ports: {N1: Voutp, N2: Ve}
name: RL, type: Resistor, value: RL, ports: {N1: Voutp, N2: Voutn}
]
extrainfo:The circuit in diagram (b) is a voltage amplifier with feedback. The voltage feedback is taken from the output and fed back to the input through a factor β. This feedback increases the input impedance and reduces the output impedance. The circuit consists of an input voltage source Vin, an input resistor Rin, an output resistor Rout, and a load resistor RL. The feedback loop is used to control the gain and stability of the amplifier.

Figure 8.27 Effect of voltage-voltage feedback on input resistance.
The foregoing observation can be confirmed analytically with the aid of Fig. 8.28. Since $V_{e}=I_{X} R_{i n}$ and $V_{F}=\beta A_{0} I_{X} R_{i n}$, we have $V_{e}=V_{X}-V_{F}=V_{X}-\beta A_{0} I_{X} R_{i n}$. Thus, $I_{X} R_{i n}=V_{X}-\beta A_{0} I_{X} R_{i n}$, and

$$
\begin{equation*}
\frac{V_{X}}{I_{X}}=R_{i n}\left(1+\beta A_{0}\right) \tag{8.38}
\end{equation*}
$$

The input impedance therefore increases by the ubiquitous factor $1+\beta A_{0}$, bringing the circuit closer to an ideal voltage amplifier.
image_name:Figure 8.28
description:
[
name: Vx, type: VoltageSource, ports: {Np: Vx, Nn: GND}
name: Ix, type: CurrentSource, ports: {Np: X2, Nn: X1}
name: Rin, type: Resistor, value: Rin, ports: {N1: X1, N2: Ve}
name: A0, type: OpAmp, value: A0, ports: {InP: Ve, InN: VF, OutP: X3, OutN: X2}
]
extrainfo:The circuit is a voltage-voltage feedback configuration with an input impedance that increases by a factor of 1+βA0. It features a voltage source Vx, a current source Ix, a resistor Rin, and an operational amplifier A0. The feedback is controlled by the factor β.

Figure 8.28 Calculation of input impedance of a voltage-voltage feedback circuit.

#### Example 8.6

Figure 8.29(a) shows a common-gate topology placed in a voltage-voltage feedback configuration. Note that the summation of the feedback voltage and the input voltage is accomplished by applying the former to the gate and the latter to the source. ${ }^{8}$ Calculate the input resistance at low frequencies if channel-length modulation is negligible.

#### Solution

Breaking the loop as depicted in Fig. 8.29(b), we recognize that the open-loop input resistance is equal to ( $g_{m 1}+$ $\left.g_{m b 1}\right)^{-1}$. To find the loop gain, we set the input to zero and inject a test signal in to the loop [Fig. 8.29(c)], obtaining $V_{F} / V_{t}=-g_{m 1} R_{D} C_{1} /\left(C_{1}+C_{2}\right)$. The closed-loop input impedance is then equal to

$$
\begin{equation*}
R_{\text {in, }, \text { closed }}=\frac{1}{g_{m 1}+g_{m b 1}}\left(1+\frac{C_{1}}{C_{1}+C_{2}} g_{m 1} R_{D}\right) \tag{8.39}
\end{equation*}
$$

[^50]image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: Vin, D: Vout, G: P}
name: RD, type: Resistor, value: RD, ports: {N1: Vout, N2: VDD}
name: C1, type: Capacitor, value: C1, ports: {Np: P, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: P, Nn: GND}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: Vin, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a common-source amplifier with an NMOS transistor M1. The input is at node Vin, and the output is at node Vout. The circuit uses a current source ISS as a biasing element. Capacitors C1 and C2 are connected in parallel to node P, providing AC coupling. The resistor RD is connected between Vout and VDD, acting as a load resistor.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: Vin, D: Vout, G: P}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: C1, type: Capacitor, value: C1, ports: {Np: P, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: P, Nn: GND}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: Vin, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a common-source NMOS amplifier with capacitive feedback. The feedback is provided by capacitors C1 and C2, and the output is taken across RD. The current source ISS provides the biasing current for the NMOS transistor M1.
image_name:(c)
description:
[
name: M1, type: NMOS, ports: {S: Vin, D: VF, G: P}
name: RD, type: Resistor, value: RD, ports: {N1: VF, N2: VDD}
name: C1, type: Capacitor, value: C1, ports: {Np: P, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: P, Nn: GND}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: Vin, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit diagram (c) represents a test setup for measuring loop gain by injecting a test signal Vt. The NMOS transistor M1 is configured with a drain resistor RD and two capacitors C1 and C2 connected at the gate. The current source ISS provides biasing. The output is taken across the drain of M1, labeled as VF.

Figure 8.29

The increase in the input impedance can be explained as follows. Suppose the input voltage decreases by $\Delta V$, causing the output voltage to fall. As a result, the gate voltage of $M_{1}$ decreases, thereby lowering the gate-source voltage of $M_{1}$ and yielding a change in $V_{G S 1}$ that is less than $\Delta V$. This means that the drain current changes by an amount less than $\left(g_{m}+g_{m b}\right) \Delta V$. By contrast, if the gate of $M_{1}$ were connected to a constant potential, the gate-source voltage would change by $\Delta V$, resulting in a larger current change.

In summary, voltage-voltage feedback decreases the output impedance and increases the input impedance, thereby proving useful as a "buffer" stage that can be interposed between a high-impedance source and a low-impedance load.

### 8.2.2 Current-Voltage Feedback

In some circuits, it is desirable or simpler to sense the output current to perform feedback. The current is actually sensed by placing a (preferably small) resistor in series with the output and using the voltage drop across the resistor as the feedback information. This voltage may even serve as the return signal that is directly subtracted from the input.
image_name:Figure 8.30 Current-voltage feedback
description:The system block diagram titled "Figure 8.30 Current-voltage feedback" represents a current-voltage feedback system used to control the output of a feedforward amplifier. The main components of this system include a Feedforward Amplifier, a Feedback Network, and a Load Impedance (ZL).

1. **Main Components:**
- **Feedforward Amplifier (Gm):** This block is responsible for amplifying the input signal (Vin). It produces an output current (Iout) based on the input voltage (Ve), which is the error voltage.
- **Feedback Network:** This block senses the output current (Iout) and converts it into a feedback voltage (VF). The feedback network has a feedback factor denoted as RF, which has the dimension of resistance.
- **Load Impedance (ZL):** This represents the impedance that the output current is delivered to. It must be finite to ensure proper operation of the Gm stage.

2. **Flow of Information or Control:**
- The input voltage (Vin) is applied to the system, and the error voltage (Ve) is determined by subtracting the feedback voltage (VF) from Vin.
- The feedforward amplifier amplifies the error voltage (Ve) to produce the output current (Iout).
- The output current (Iout) is delivered to the load impedance (ZL), and a portion of this current is sensed by the feedback network.
- The feedback network converts the sensed current to a feedback voltage (VF), which is used to adjust the input to the feedforward amplifier, thereby forming a feedback loop.

3. **Labels, Annotations, and Key Indicators:**
- The diagram is annotated with key signals such as Vin, Ve, VF, and Iout.
- The feedback factor is labeled as RF, and the load impedance is labeled as ZL.
- The diagram indicates that both the input and output have low resistances (Low Rin and Low Rout).

4. **Overall System Function:**
- The primary function of this system is to regulate the output current delivered to the load impedance using a current-voltage feedback mechanism. By sensing the output current and feeding back a proportional voltage, the system can adjust the input to the feedforward amplifier, thereby maintaining stable operation and desired output characteristics. This setup is particularly useful for systems requiring precise control of output current despite variations in load conditions or input signals.

Figure 8.30 Current-voltage feedback.

Let us consider the general current-voltage feedback system illustrated in Fig. 8.30. ${ }^{9}$ Since the feedback network senses the output current and returns a voltage, its feedback factor, $\beta$, has the dimension of resistance and is denoted by $R_{F}$. It is important to note that a $G_{m}$ stage must be loaded ("terminated") by a finite impedance, $Z_{L}$, to ensure that it can deliver its output current. If $Z_{L}=\infty$, then an ideal $G_{m}$

[^51]stage would sustain an infinite output voltage. We write $V_{F}=R_{F} I_{\text {out }}, V_{e}=V_{\text {in }}-R_{F} I_{\text {out }}$, and hence $I_{\text {out }}=G_{m}\left(V_{\text {in }}-R_{F} I_{\text {out }}\right)$. It follows that
\$\$

$$
\begin{equation*}
\frac{I_{\text {out }}}{V_{\text {in }}}=\frac{G_{m}}{1+G_{m} R_{F}} \tag{8.40}
\end{equation*}
$$

\$\$

An ideal feedback network in this case exhibits zero input and output impedances.
It is instructive to confirm that $G_{m} R_{F}$ is indeed the loop gain. As shown in Fig. 8.31, we set the input voltage to zero and break the loop by disconnecting the feedback network from the output and replacing it with a short at the output (if the feedback network is ideal). We then inject the test signal $I_{t}$, producing $V_{F}=R_{F} I_{t}$, and hence $I_{\text {out }}=-G_{m} R_{F} I_{t}$. Thus, the loop gain is equal to $G_{m} R_{F}$ and the transconductance of the amplifier is reduced by $1+G_{m} R_{F}$ when feedback is applied.
image_name:Figure 8.31 Calculation of loop gain for current-voltage feedback
description:
[
name: Gm, type: VoltageControlledCurrentSource, ports: {Np: +, Nn: -}
name: RF, type: Resistor, value: RF, ports: {N1: +, N2: -}
name: ZL, type: Resistor, value: ZL, ports: {N1: Iout, N2: Short}
name: It, type: CurrentSource, value: It, ports: {Np: Short, Nn: -}
]
extrainfo:The circuit illustrates the calculation of loop gain for current-voltage feedback. The loop gain is given by Gm*RF. The feedback network is disconnected, and a test current It is injected to determine the loop gain.

Figure 8.31 Calculation of loop gain for current-voltage feedback.

Is it realistic to assume that the input impedance of the feedback network is zero? Why do we use a test current rather than a test voltage? Does the type of test source affect the loop gain calculations? These questions are addressed later in this chapter.

Sensing the current at the output of a feedback system increases the output impedance. This is because the system attempts to make the output current a faithful replica of the input signal (with a proportionality factor if the input is a voltage quantity). Consequently, the system delivers the same current waveform as the load varies, in essence approaching an ideal current source and hence exhibiting a high output impedance.
image_name:Figure 8.32 Calculation of output resistance of a current-voltage feedback amplifier
description:
[
name: Gm, type: VoltageControlledCurrentSource, value: Gm, ports: {Np: +, Nn: -}
name: Rout, type: Resistor, value: Rout, ports: {N1: +, N2: Vx}
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Vx, Nn: -}
name: VF, type: VoltageSource, value: VF, ports: {Np: VF, Nn: -}
name: RF, type: Resistor, value: RF, ports: {N1: VF, N2: Gm}
]
extrainfo:The circuit is a current-voltage feedback amplifier used to calculate the output resistance. It includes a voltage-controlled current source (Gm), resistors (Rout and RF), and voltage sources (Vx and VF). The feedback network produces a voltage VF proportional to IX, and the current generated by Gm equals -RF * IX * Gm.

Figure 8.32 Calculation of output resistance of a current-voltage feedback amplifier.

To prove the above result, we consider the current-voltage feedback topology shown in Fig. 8.32, where $R_{\text {out }}$ represents the finite output impedance of the feedforward amplifier. ${ }^{10}$ The feedback network produces a voltage $V_{F}$ proportional to $I_{X}: V_{F}=R_{F} I_{X}$, and the current generated by $G_{m}$ equals $-R_{F} I_{X} G_{m}$. As a

[^52]result, $-R_{F} I_{X} G_{m}=I_{X}-V_{X} / R_{\text {out }}$, yielding
\$\$

$$
\begin{equation*}
\frac{V_{X}}{I_{X}}=R_{\text {out }}\left(1+G_{m} R_{F}\right) \tag{8.41}
\end{equation*}
$$

\$\$

The output impedance therefore increases by a factor of $1+G_{m} R_{F}$.

#### Example 8.7

Rechargeable batteries must be charged by a constant current (rather than a constant voltage) to avoid damage. The battery charger must therefore generate a constant current from a golden reference, $V_{R E F}$. As shown in Fig. 8.33(a), we can insert a small resistor $r$ in the output current path, apply the voltage across $r$ to an amplifier $A_{1}$, and subtract the output of $A_{1}$ from $V_{R E F}$. Calculate the output current and impedance of this circuit, assuming $\left|Z_{L}\right| \ll r_{O}$ (the output resistance of $M_{1}$ ).
image_name:(a)
description:
[
name: VREF, type: VoltageSource, value: VREF, ports: {Np: VREF, Nn: GND}
name: A1, type: OpAmp, ports: {InP: VREF, InN: g1, OutP: d1, OutN: '}
name: M1, type: NMOS, ports: {S: GND, D: d1, G: g1}
name: ZL, type: Resistor, value: ZL, ports: {N1: x1, N2: d1}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: Vt, Nn: GND'}
]
extrainfo:The circuit diagram represents a constant current battery charger. The operational amplifier A1 is used to maintain the output current Iout by comparing the reference voltage VREF with the voltage across the resistor r. The NMOS transistor M1 is used to control the output current path. The circuit ensures that the rechargeable battery receives a constant current, which is crucial for safe and efficient charging.
image_name:(b)
description:
[
name: A1, type: OpAmp, ports: {InP: x1, InN: VF, OutP: g1, OutN: GND}
name: M1, type: NMOS, ports: {S: GND, D: d1, G: g1}
name: VREF, type: VoltageSource, ports: {Np: VREF, Nn: GND}
name: ZL, type: Resistor, ports: {N1: x1, N2: d1}
name: Vt, type: VoltageSource, ports: {Np: Vt, Nn: GND}
]
extrainfo:This circuit is designed for generating a constant current for a rechargeable battery. It uses an op-amp (A1) to maintain the current across a resistor (r) and an NMOS transistor (M1) to control the current flow. The output current is determined by the reference voltage (VREF) and the gain of the op-amp. The load impedance (ZL) is connected in series with the output.

Figure 8.33

#### Solution

With a high loop gain, the output voltage of $A_{1}$ is approximately equal to $V_{R E F}$, and hence $I_{\text {out }}=\left(V_{R E F} / A_{1}\right) / r$. Using the circuit of Fig. 8.33(b) to determine the loop gain, we have

$$
\begin{equation*}
\frac{V_{F}}{V_{t}} \approx-g_{m} r A_{1} \tag{8.42}
\end{equation*}
$$

Thus, the open-loop output impedance seen by $Z_{L}$ is multiplied by $1+g_{m} r A_{1}$, yielding

$$
\begin{equation*}
R_{\text {out }, \text { closed }}=\left(1+g_{m} r A_{1}\right)\left(r_{O}+r\right) \tag{8.43}
\end{equation*}
$$

We observe that $Z_{L}$ is now driven by a better current source.

As with voltage-voltage feedback, current-voltage feedback increases the input impedance by a factor equal to one plus the loop gain. As illustrated in Fig. 8.34, we have $I_{X} R_{\text {in }} G_{m}=I_{\text {out }}$. Thus, $V_{e}=$ $V_{X}-G_{m} R_{F} I_{X} R_{i n}$ and

$$
\begin{equation*}
\frac{V_{X}}{I_{X}}=R_{i n}\left(1+G_{m} R_{F}\right) \tag{8.44}
\end{equation*}
$$

The reader can show that the loop gain is indeed equal to $G_{m} R_{F}$.
In summary, current-voltage feedback increases both the input and the output impedances while decreasing the feedforward transconductance. As explained in Chapter 9, the high output impedance proves useful in high-gain op amps.
image_name:Figure 8.34
description:
[
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Vx+, Nn: Ve+}
name: Ve, type: VoltageSource, value: Ve, ports: {Np: Ve+, Nn: Ve-}
name: Rin, type: Resistor, value: Rin, ports: {N1: Ve-, N2: Gm+}
name: Gm, type: VoltageControlledCurrentSource, value: Gm, ports: {Np: Gm+, Nn: Gm-}
name: Vf, type: VoltageSource, value: Vf, ports: {Np: Vout, Nn: Rf+}
name: Rf, type: Resistor, value: Rf, ports: {N1: Rf+, N2: Rf-}
]
extrainfo:The circuit is a current-voltage feedback amplifier. The input current Ix flows through the voltage source Vx and resistor Rin, while the output current Iout is controlled by the voltage-controlled current source Gm. The feedback loop includes the voltage source Vf and resistor Rf.

Figure 8.34 Calculation of input resistance of a current-voltage feedback amplifier.

### 8.2.3 Voltage-Current Feedback

In this type of feedback, the output voltage is sensed and a proportional current is returned to the summing point at the input. ${ }^{11}$ Note that the feedforward path incorporates a transimpedance amplifier with gain $R_{0}$ and the feedback factor has a dimension of conductance.

A voltage-current feedback topology is shown in Fig. 8.35. Sensing a voltage and producing a current, the feedback network is characterized by a transconductance $g_{m F}$, ideally exhibiting infinite input and output impedances. Since $I_{F}=g_{m F} V_{\text {out }}$ and $I_{e}=I_{\text {in }}-I_{F}$, we have $V_{\text {out }}=R_{0} I_{e}=R_{0}\left(I_{\text {in }}-g_{m F} V_{\text {out }}\right)$. It follows that

$$
\begin{equation*}
\frac{V_{\text {out }}}{I_{\text {in }}}=\frac{R_{0}}{1+g_{m F} R_{0}} \tag{8.45}
\end{equation*}
$$

The reader can prove that $g_{m F} R_{0}$ is indeed the loop gain, concluding that this type of feedback lowers the transimpedance by a factor equal to one plus the loop gain.
image_name:Figure 8.35 Voltage-current feedback
description:The system block diagram labeled as "Figure 8.35 Voltage-current feedback" illustrates a feedback mechanism involving a feedforward amplifier and a feedback network. Here's a detailed breakdown:

1. **Main Components:**
- **Feedforward Amplifier:** This block is responsible for amplifying the error current \( I_e \) and has an output resistance labeled \( R_0 \). It receives an input current \( I_e \) and outputs a voltage \( V_{out} \).
- **Feedback Network:** This block processes the output voltage \( V_{out} \) to generate a feedback current \( I_F \). It is characterized by a transconductance \( g_{mF} \) and has high input and output resistances \( R_{in} \) and \( R_{out} \), respectively.

2. **Flow of Information or Control:**
- The input current \( I_{in} \) is split into two paths: one goes directly to the feedforward amplifier as \( I_e \), while the other is directed to the feedback network, resulting in the feedback current \( I_F \).
- The feedforward amplifier processes \( I_e \) and produces the output voltage \( V_{out} \).
- The feedback network senses \( V_{out} \), converts it into \( I_F \) using its transconductance \( g_{mF} \), and feeds it back to subtract from \( I_{in} \), effectively controlling \( I_e \).

3. **Labels, Annotations, and Key Indicators:**
- \( R_0 \): Represents the output resistance of the feedforward amplifier.
- \( g_{mF} \): Represents the transconductance of the feedback network.
- High \( R_{in} \) and High \( R_{out} \): Indicate high input and output resistances of the feedback network, ensuring minimal loading effects.

4. **Overall System Function:**
- The primary function of this system is to implement voltage-current feedback to control the transimpedance \( \frac{V_{out}}{I_{in}} \). By feeding back a portion of the output voltage as a current \( I_F \) to subtract from the input current \( I_{in} \), the system reduces the effective transimpedance. This feedback mechanism lowers the transimpedance by a factor of \( 1 + g_{mF} R_0 \), thus enhancing the stability and performance of the amplifier system.

Figure 8.35 Voltage-current feedback.

#### Example 8.8

Calculate the transimpedance, $V_{\text {out }} / I_{\text {in }}$, of the circuit shown in Fig. 8.36(a) at relatively low frequencies. Assume that $\lambda=0$. (The bias network of $M_{1}$ is not shown.)

#### Solution

In this circuit, the capacitive divider $C_{1}-C_{2}$ senses the output voltage, applying the result to the gate of $M_{1}$ and producing a current that is subtracted from $I_{i n}$. The open-loop transimpedance equals that of the core common-gate stage, $R_{D}$. The loop gain is obtained by setting $I_{i n}$ to zero and breaking the loop at the output [Fig. 8.36(b)]:

$$
\begin{equation*}
-V_{t} \frac{C_{1}}{C_{1}+C_{2}} g_{m 1} R_{D}=V_{F} \tag{8.46}
\end{equation*}
$$

[^53]image_name:(a)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: P}
name: C2, type: Capacitor, value: C2, ports: {Np: P, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: d1s2, G: P}
name: M2, type: NMOS, ports: {S: d1s2, D: Vout, G: Vb}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: d1s2, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:This circuit is a common-gate transimpedance amplifier with capacitive feedback. It uses a capacitive divider (C1, C2) to sense the output voltage and control the current through M1, which is subtracted from the input current Iin. The overall transimpedance is determined by the resistor RD and the capacitive feedback.
image_name:(b)
description:
[
name: M2, type: NMOS, ports: {S: d1s2, D: VDD, G: Vb}
name: M1, type: NMOS, ports: {S: GND, D: d1s2, G: P}
name: C1, type: Capacitor, value: C1, ports: {Np: Vt, Nn: P}
name: C2, type: Capacitor, value: C2, ports: {Np: P, Nn: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: VF}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: Vt, Nn: GND}
]
extrainfo:The circuit diagram (b) is a feedback network with a capacitive divider formed by C1 and C2, which senses the output voltage. The transimpedance is determined by the resistor RD and the loop gain is influenced by the capacitive divider and the transconductance of M1.

Figure 8.36
Thus, the overall transimpedance is equal to

$$
\begin{equation*}
R_{t o t}=\frac{R_{D}}{1+\frac{C_{1}}{C_{1}+C_{2}} g_{m 1} R_{D}} \tag{8.47}
\end{equation*}
$$

#### Example 8.9

We know from the previous example that

$$
\begin{equation*}
R_{i n}=\frac{1}{g_{m 2}} \frac{1}{1+\frac{C_{1}}{C_{1}+C_{2}} g_{m 1} R_{D}} \tag{8.48}
\end{equation*}
$$

A student repeats the analysis, but with the input driven by a voltage source, concluding that the loop gain is zero and the input impedance is not affected by the feedback loop. Explain the flaw in the student's argument.

#### Solution

Consider the arrangement shown in Fig. 8.37(a). We know that $R_{i n}$ is affected by the feedback because $M_{1}$ generates a current in response to $V_{i n}$. On the other hand, it appears from Fig. 8.37(b) that the loop gain is zero in this case. How do we reconcile these two views?
image_name:Figure 8.37(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Rin, type: Resistor, value: Rin, ports: {N1: Vin, N2: Vin}
name: M1, type: NMOS, ports: {S: GND, D: Vin, G: P}
name: M2, type: NMOS, ports: {S: Vin, D: Vout, G: Vb}
name: RD, type: Resistor, value: RD, ports: {N1: Vout, N2: VDD}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: Vb}
name: C2, type: Capacitor, value: C2, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a feedback amplifier with NMOS transistors M1 and M2. The input voltage Vin is applied across Rin. M1 is configured as a common source amplifier, and M2 is connected in a cascode configuration. The circuit has capacitive coupling through C1 and C2, and RD is connected to VDD. The output voltage is taken across Vout.

(a)
image_name:(a)
description:
[
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: VF}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: Vb}
name: C2, type: Capacitor, value: C2, ports: {Np: P, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: P, G: VF}
name: M2, type: NMOS, ports: {S: P, D: VF, G: Vb}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: Vt, Nn: GND}
]
extrainfo:The circuit is a feedback amplifier with NMOS transistors M1 and M2. M1 is configured as a common source amplifier, and M2 is connected in a cascode configuration. The circuit has capacitive coupling through C1 and C2, with RD connected to VDD. The output voltage is taken across Vout.

(b)

Figure 8.37
We must recall that returning current to the input assumes that the circuit is driven by a current source; i.e., our generic negative-feedback system requires that the returned quantity and the input have the same dimension. In other
words, the circuit of Fig. 8.37(a) does not map to our canonical feedback system because it returns a current but is driven by a voltage. We therefore cannot compute the loop gain by setting the input voltage to zero and breaking the loop. Of course, the input impedance is still given by Eq. (8.48). We will return to this circuit in Sec. 8.6.4 and apply Blackman's theorem to it.

Following our reasoning for the other two types of feedback studied above, we surmise that voltagecurrent feedback decreases both the input and the output impedances. As shown in Fig. 8.38(a) and noted in Example 8.3, the input resistance of $R_{0}$ appears in series with its input port. We write $I_{F}=I_{X}-V_{X} / R_{i n}$ and $\left(V_{X} / R_{i n}\right) R_{0} g_{m F}=I_{F}$. Thus,

$$
\begin{equation*}
\frac{V_{X}}{I_{X}}=\frac{R_{i n}}{1+g_{m F} R_{0}} \tag{8.49}
\end{equation*}
$$

image_name:(a)
description:
[
name: Ix, type: CurrentSource, ports: {Np: GND, Nn: Node1}
name: Rin, type: Resistor, value: Rin, ports: {N1: Node1, N2: Node2}
name: OpAmp, type: OpAmp, ports: {InP: Node2, InN: GND, OutP: Node3, OutN: GND}
name: R0, type: Resistor, value: R0, ports: {N1: Node3, N2: Vout}
name: gmF, type: VoltageControlledCurrentSource, ports: {Np: Node1, Nn: GND}
name: Vx, type: VoltageSource, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a voltage-current feedback amplifier with decreased input and output impedances. It uses a feedback loop involving a voltage-controlled current source (gmF) to achieve the desired impedance characteristics.
image_name:(b)
description:
[
name: Ix, type: CurrentSource, ports: {Np: GND, Nn: Node1}
name: Rin, type: Resistor, value: Rin, ports: {N1: Node1, N2: Node2}
name: R0, type: Resistor, value: R0, ports: {N1: Node2, N2: Node3}
name: gmF, type: VoltageControlledCurrentSource, value: gmF, ports: {Np: Node4, Nn: GND}
name: Vout, type: VoltageSource, value: Vout, ports: {Np: Node5, Nn: GND}
name: Rout, type: Resistor, value: Rout, ports: {N1: Node3, N2: Node6}
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Node6, Nn: GND}
]
extrainfo:The circuit in diagram (b) is a voltage-current feedback amplifier. It includes a voltage-controlled current source with transconductance gmF, and resistors Rin, R0, and Rout. The current source Ix is connected to ground. The output voltage Vx is measured across Rout with respect to ground.

Figure 8.38 Calculation of (a) input and (b) output impedance of a voltage-current feedback amplifier.
Similarly, from Fig. 8.38(b), we have $I_{F}=V_{X} g_{m F}, I_{e}=-I_{F}$, and $V_{M}=-R_{0} g_{m F} V_{X}$. Neglecting the input current of the feedback network, we write $I_{X}=\left(V_{X}-V_{M}\right) / R_{\text {out }}=\left(V_{X}+g_{m F} R_{0} V_{X}\right) / R_{\text {out }}$. That is

$$
\begin{equation*}
\frac{V_{X}}{I_{X}}=\frac{R_{\text {out }}}{1+g_{m F} R_{0}} \tag{8.50}
\end{equation*}
$$

#### Example 8.10

Calculate the input and output impedances of the circuit shown in Fig. 8.39(a). For simplicity, assume that $R_{F} \gg R_{D}$.
image_name:Fig. 8.39(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: g1}
name: RF, type: Resistor, value: RF, ports: {N1: g1, N2: Vout}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: GND, Nn: g1}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: g1, Nn: Vt}
]
extrainfo:The circuit in Fig. 8.39(a) features an NMOS transistor M1 with its source connected to ground and its drain connected to the output node Vout. A feedback resistor RF connects the gate of M1 to Vout. The circuit is powered by a voltage source VDD through a resistor RD connected to Vout. The input current source Iin is connected from ground to the gate of M1, and a voltage source Vt is connected across the feedback resistor RF in Fig. 8.39(b).
image_name:Fig. 8.39(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: VF, G: g1}
name: RF, type: Resistor, value: RF, ports: {N1: g1, N2: Vt}
name: RD, type: Resistor, value: RD, ports: {N1: VF, N2: VDD}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: Vt, Nn: g1}
]
extrainfo:The circuit in Fig. 8.39(b) includes an NMOS transistor M1, with its source connected to ground, drain connected to node VF, and gate connected to node g1. The resistor RF connects node g1 to node Vt, and the resistor RD connects node VF to the power supply VDD. The voltage source Vt is connected between nodes Vt and g1.

Figure 8.39

#### Solution

In this circuit, $R_{F}$ senses the output voltage and returns a current to the input. Breaking the loop as depicted in Fig. 8.39(b), we calculate the loop gain as $g_{m} R_{D}$. Thus, the open-loop input impedance, $R_{F}$, is divided by $1+g_{m} R_{D}$ :

$$
\begin{equation*}
R_{\text {in, closed }}=\frac{R_{F}}{1+g_{m} R_{D}} \tag{8.51}
\end{equation*}
$$

Similarly,

$$
\begin{align*}
R_{\text {out }, \text { closed }} & =\frac{R_{D}}{1+g_{m} R_{D}}  \tag{8.52}\\
& =\frac{1}{g_{m}} \| R_{D} \tag{8.53}
\end{align*}
$$

Note that $R_{\text {out,closed }}$ is in fact the parallel combination of a diode-connected transistor and $R_{D}$.
The reduction of the input impedance agrees with Miller's prediction: since the voltage gain from the gate of $M_{1}$ to its drain is approximately equal to $-g_{m} R_{D}$, the feedback resistor equivalently produces a grounded resistance at the input equal to $R_{F} /\left(1+g_{m} R_{D}\right)$.

An important application of amplifiers with low input impedance is in fiber optic receivers, where light received through a fiber is converted to a current by a reverse-biased photodiode. This current is typically converted to a voltage for further amplification and processing. Shown in Fig. 8.40(a), such conversion can be accomplished by a simple resistor, but at the cost of bandwidth because the diode suffers from a relatively large junction capacitance. For this reason, the feedback topology of Fig. 8.40(b) is usually employed, where $R_{1}$ is placed around the voltage amplifier $A$ to form a "transimpedance amplifier" (TIA). The input impedance is $R_{1} /(1+A)$ and the output voltage is approximately $-R_{1} I_{D 1}$. The bandwidth thus increases from $1 /\left(2 \pi R_{1} C_{D 1}\right)$ to $(1+A) /\left(2 \pi R_{1} C_{D 1}\right)$ if $A$ itself is a wideband amplifier.
image_name:(a)
description:
[
name: D1, type: Diode, ports: {Na: ID, Nc: GND}
name: CD1, type: Capacitor, value: CD1, ports: {Np: Vout, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit represents a simple photodiode detection system using a resistor (R1) to convert the diode current (ID) to a voltage (Vout). The diode D1 is connected to the ground, and the capacitor CD1 is used for filtering. The output voltage is taken across the resistor R1.
image_name:(b)
description:
[
name: D1, type: Diode, ports: {Na: ID, Nc: GND}
name: CD1, type: Capacitor, value: CD1, ports: {Np: ID, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: ID, N2: Vout}
name: A, type: OpAmp, ports: {InP: GND, InN: ID, OutP: Vout, OutN: GND}
]
extrainfo:The circuit is a transimpedance amplifier used to convert current from a photodiode into a voltage output. The diode D1 is connected to ground, and the amplifier A is configured with feedback resistor R1.

Figure 8.40 Detection of current produced by a photodiode by (a) resistor $R_{1}$ and (b) a transimpedance amplifier.

### 8.2.4 Current-Current Feedback

Figure 8.41 illustrates this type of feedback. ${ }^{12}$ Here, the feedforward amplifier is characterized by a current gain, $A_{I}$, and the feedback network by a current ratio, $\beta$. In a fashion similar to the previous derivations, the reader can easily prove that the closed-loop current gain is equal to $A_{I} /\left(1+\beta A_{I}\right)$, the input impedance is divided by $1+\beta A_{I}$ and the output impedance is multiplied by $1+\beta A_{I}$.

[^54]image_name:Figure 8.41 Current-current feedback
description:The diagram labeled "Figure 8.41 Current-current feedback" illustrates a system employing current-current feedback. The primary components of this system include a feedforward amplifier characterized by a current gain, denoted as \( A_I \), and a feedback network characterized by a current ratio, \( \beta \).

**Main Components:**
1. **Feedforward Amplifier:** This block is responsible for amplifying the input current \( I_{in} \). The amplifier has a current gain \( A_I \), and it outputs a current \( I_{out} \).
2. **Feedback Network:** This block receives a portion of the output current \( I_{out} \) and feeds back a current \( I_F \) to the input of the system. The feedback network is defined by a current ratio \( \beta \).
3. **Load Impedance \( Z_L \):** The output current \( I_{out} \) is delivered to a load with impedance \( Z_L \).

**Flow of Information or Control:**
- The input current \( I_{in} \) is fed into the system.
- The feedforward amplifier takes this input current and amplifies it, resulting in an output current \( I_{out} \).
- A portion of \( I_{out} \) is fed back through the feedback network as \( I_F \), which influences the input to the feedforward amplifier.
- The feedback loop is characterized by the current ratio \( \beta \), which determines how much of the output current is fed back.

**Labels, Annotations, and Key Indicators:**
- \( I_e \) denotes the current entering the feedforward amplifier.
- The feedback network is indicated to have high output impedance \( R_{out} \) and low input impedance \( R_{in} \).
- The feedback factor \( \beta \) is crucial for determining the feedback current \( I_F \).

**Overall System Function:**
The primary function of this system is to provide current amplification with a feedback mechanism that stabilizes and controls the gain. The closed-loop current gain of the system is given by \( A_I / (1 + \beta A_I) \), showing that the feedback reduces the overall gain but increases stability. The input impedance is lowered, and the output impedance is increased by the factor \( 1 + \beta A_I \), which is beneficial for certain applications requiring current control and stability.

Figure 8.41 Current-current feedback.
image_name:Figure 8.42
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: g1}
name: M2, type: NMOS, ports: {S: X, D: Y, G: g1}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: RF, type: Resistor, value: RF, ports: {N1: g1, N2: Y}
name: RS, type: Resistor, value: RS, ports: {N1: Y, N2: GND}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: g1, Nn: GND}
]
extrainfo:The circuit implements a current-current feedback mechanism with NMOS transistors M1 and M2. Resistor RF provides feedback from the output node Y to the gate of M1. Resistor RS monitors the output current. The circuit is designed to stabilize and control the current gain.

Figure 8.42

Figure 8.42 illustrates an example of current-current feedback. Here, since the source and drain currents of $M_{2}$ are equal (at low frequencies), resistor $R_{S}$ is inserted in the source network to monitor the output current. Resistor $R_{F}$ plays the same role as in Fig. 8.39.

### 8.3 Effect of Feedback on Noise

反馈并不能提高电路的噪声性能！

Feedback does not improve the noise performance of circuits. Let us first consider the simple case illustrated in Fig. 8.43(a), where the open-loop voltage amplifier $A_{1}$ is characterized by only an inputreferred noise voltage and the feedback network is noiseless. We have $\left(V_{\text {in }}-\beta V_{\text {out }}+V_{n}\right) A_{1}=V_{\text {out }}$, and hence

$$
\begin{equation*}
V_{\text {out }}=\left(V_{\text {in }}+V_{n}\right) \frac{A_{1}}{1+\beta A_{1}} \tag{8.54}
\end{equation*}
$$

image_name:(a)
description:The block diagram labeled as (a) illustrates a feedback system around a noisy circuit. The main components in this system include:

1. **Input Signal ($V_{in}$):** This is the initial signal that is fed into the system.

2. **Summing Junction:** The input signal $V_{in}$ is combined with the feedback signal. This junction also adds an input-referred noise voltage $V_n$ to the input signal.

3. **Noise Source ($V_n$):** This represents the noise voltage that is added to the input signal.

4. **Amplifier ($A_1$):** After the summing junction, the combined signal is fed into an amplifier $A_1$. The amplifier boosts the signal and any noise present.

5. **Output ($V_{out}$):** The amplified signal is present at the output of the amplifier.

6. **Feedback Network ($\beta$):** A portion of the output signal $V_{out}$ is fed back through the feedback network characterized by a factor $\beta$. This feedback network is assumed to be noiseless in this context.

Flow of Information:
- The input signal $V_{in}$ and noise voltage $V_n$ are summed at the summing junction. The output of this summing junction is then fed to the amplifier $A_1$.
- The amplifier $A_1$ processes this signal, and the output $V_{out}$ is obtained.
- Part of the output $V_{out}$ is fed back through the feedback network with a feedback factor $\beta$ to the summing junction, creating a feedback loop.

Overall System Function:
- The primary function of this system is to amplify the input signal while accounting for the noise introduced at the input. The feedback loop, characterized by the factor $\beta$, helps in controlling the gain and stability of the system. However, as analyzed, the input-referred noise remains the same, indicating that the feedback does not improve the noise performance of the circuit when the feedback network is noiseless.
image_name:(b)
description:The system block diagram labeled (b) represents a feedback amplifier circuit. The main components of the diagram include:

1. **Input Signal ($V_{in}$):** This is the initial voltage signal input to the system.

2. **Noise Source ($V_{n}$):** A noise voltage is introduced in series with the input signal. This noise is considered input-referred, meaning it appears at the input of the amplifier.

3. **Summing Junction:** The input signal $V_{in}$ and the noise $V_{n}$ are summed together. This results in a combined signal that is fed into the amplifier.

4. **Amplifier ($A_{1}$):** The combined signal from the summing junction is fed into the amplifier block $A_{1}$. The amplifier boosts the signal strength according to its gain.

5. **Feedback Network ($\beta$):** The output of the amplifier $V_{out}$ is fed back into the system through a feedback network characterized by the factor $\beta$. This feedback signal is subtracted from the input noise signal at the summing junction.

6. **Output Voltage ($V_{out}$):** The final output of the system is taken from the output of the amplifier.

Flow of Information:
- The input voltage $V_{in}$ and noise voltage $V_{n}$ are summed at the summing junction.
- The resulting signal is amplified by the amplifier $A_{1}$, producing the output voltage $V_{out}$.
- A portion of this output is fed back through the feedback network ($\beta$) to the summing junction, where it is subtracted from the noise voltage $V_{n}$.

Labels and Annotations:
- The diagram labels the input and output voltages, the noise voltage, the amplifier, and the feedback network.

Overall System Function:
The primary function of this system is to amplify the input signal while maintaining a feedback loop. The feedback helps control the gain of the amplifier and can stabilize the system. However, the noise introduced at the input remains unaffected by the feedback network, as the feedback network is assumed to be noiseless. The analysis shows that the input-referred noise voltage remains the same, demonstrating that feedback does not improve noise performance in this configuration.

Figure 8.43 Feedback around a noisy circuit.

Thus, the circuit can be simplified as shown in Fig. 8.43(b), revealing that the input-referred noise of the overall circuit is still equal to $V_{n}$. This analysis can be extended to all four feedback topologies to prove that the input-referred noise voltage and current remain the same if the feedback network introduces no noise. In practice, the feedback network itself may contain resistors or transistors, degrading the overall noise performance.

It is important to note that in Fig. 8.43(a), the output of interest is the same as the quantity sensed by the feedback network. This need not always be the case. For example, in the circuit of Fig. 8.44, the output is provided at the drain of $M_{1}$ whereas the feedback network senses the voltage at the source of $M_{1}$. In such cases, the input-referred noise of the closed-loop circuit may not be equal to that of the open-loop circuit even if the feedback network is noiseless. As an example, let us consider the topology of Fig. 8.44 and, for simplicity, take only the noise of $R_{D}, V_{n, R D}$, into account. The reader can prove that the closed-loop voltage gain is equal to $-A_{1} g_{m} R_{D} /\left[1+\left(1+A_{1}\right) g_{m} R_{S}\right]$ if $\lambda=\gamma=0$, and hence the input-referred noise voltage due to $R_{D}$ is

$$
\begin{equation*}
\left|V_{n, i n, \text { closed }}\right|=\frac{\left|V_{n, R D}\right|}{A_{1} R_{D}}\left[\frac{1}{g_{m}}+\left(1+A_{1}\right) R_{S}\right] \tag{8.55}
\end{equation*}
$$

image_name:Figure 8.44
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Vin, InN: InN(A1), OutP: Vout, OutN: '}
name: M1, type: NMOS, ports: {S: InN(A1), D: Vout, G: Vout}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: RS, type: Resistor, value: RS, ports: {N1: InN(A1), N2: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND'}
]
extrainfo:This is a feedback amplifier circuit with an op-amp (A1) and an NMOS transistor (M1). The feedback is sensing the source voltage of M1. The circuit includes resistors RD and RS, and a voltage source VDD. The op-amp is configured with a negative feedback loop.

Figure 8.44 Noisy circuit with feedback sensing the source voltage.

For the open-loop circuit, on the other hand, the input-referred noise is

$$
\begin{equation*}
\left|V_{n, \text { in }, \text { open }}\right|=\frac{\left|V_{n, R D}\right|}{A_{1} R_{D}}\left[\frac{1}{g_{m}}+R_{S}\right] \tag{8.56}
\end{equation*}
$$

Interestingly, as $A_{1} \rightarrow \infty,\left|V_{n, \text { in, closed }}\right| \rightarrow\left|V_{n, R D}\right| R_{S} / R_{D}$ whereas $\left|V_{n, \text { in }, \text { open }}\right| \rightarrow 0$.
8.4 - Feedback Analysis Difficulties

Our study of feedback systems has made some simplifying assumptions that may not hold in all circuits. In this section, we point out five difficulties that arise in the analysis of feedback circuits, and in subsequent sections, we deal with some of them.

The analysis approach described previously proceeds as follows: (a) break the loop and obtain the open-loop gain and input and output impedances, (b) determine the loop gain, $\beta A_{0}$, and hence the closed-
loop parameters from their open-loop counterparts, and (c) use the loop gain to study properties such as open-loop gain and input and output impedances, (b) determine the loop gain, $\beta A_{0}$, and hence the closed-
loop parameters from their open-loop counterparts, and (c) use the loop gain to study properties such as stability (Chapter 10), etc. However, this approach faces issues in some circuits.

The first difficulty relates to breaking the loop and stems from the "loading" effects imposed by the feedback network upon the feedforward amplifier. For example, in the noninverting amplifier of Fig. 8.45(a) and its simple implementation shown in Fig. 8.45(b), the feedback branch consisting of $R_{1}$
and $R_{2}$ may draw a significant signal current from the op amp, reducing its open-loop gain. Figure 8.45(c) Fig. 8.45(a) and its simple implementation shown in Fig. 8.45(b), the feedback branch consisting of $R_{1}$
and $R_{2}$ may draw a significant signal current from the op amp, reducing its open-loop gain. Figure 8.45(c) depicts another case, in which the open-loop gain of the forward CS stage falls if $R_{F}$ is not very large. In both cases, this "output" loading results from the nonideal input impedance of the feedback network.

实际上，反馈网络往往会包含电阻或者电容，这会降低整体的噪声性能
image_name:Figure 8.45(a)
description:
[

]
extrainfo:The diagram is too complex to analyze without a device list. It seems to depict a noninverting amplifier as part of a larger circuit.
image_name:Figure 8.45(b)
description:
[

]
extrainfo:The circuit diagram is too complex to analyze without a device list. It appears to be a differential pair implementation of a noninverting amplifier, possibly involving transistors and feedback resistors. The feedback network might be affecting the open-loop gain due to nonideal input impedance.
image_name:Figure 8.45(c)
description:
[

]
extrainfo:The circuit diagram is too complex to analyze without a device list. It involves a feedback network that affects the open-loop gain of the forward CS stage.
image_name:Figure 8.45(d)
description:
[

]
extrainfo:The circuit diagram is complex and the device list is not provided. The diagram appears to show a two-stage amplifier implementation, with feedback resistors R1 and R2 sensing the output voltage and returning a voltage to the source of M1. The feedback network may affect the open-loop gain due to its nonideal input impedance.

image_name:(a)
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Vin, InN: VF, OutP: Vout}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: VF}
name: R2, type: Resistor, value: R2, ports: {N1: VF, N2: GND}
name: M1, type: NMOS, ports: {S: GND, D: d1g2, G: Vin}
name: M2, type: NMOS, ports: {S: d1g2, D: Vout, G: VF}
name: M3, type: PMOS, ports: {S: VDD, D: d1g2, G: Vout}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: Vout}
name: IS, type: CurrentSource, value: IS, ports: {Np: d1g2, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: GND}
name: RF, type: Resistor, value: RF, ports: {N1: d1g2, N2: Vout}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: d1g2}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: Vout}
]
extrainfo:The circuit is a two-stage amplifier with feedback resistors R1 and R2 sensing the output voltage and returning a voltage to the source of M1. The feedback network affects the open-loop gain due to its nonideal input impedance. The amplifier uses NMOS and PMOS transistors and includes a current source IS for biasing.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: VF, D: d1g2, G: Vin}
name: M2, type: NMOS, ports: {S: d1g2, D: Vout, G: Vout}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: Vout1}
name: R2, type: Resistor, value: R2, ports: {N1: Vout1, N2: VF}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: d1g2}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: Vout}
]
extrainfo:The circuit diagram is a two-stage amplifier with a feedback network. The feedback resistors R1 and R2 sense the output voltage and return a voltage to the source of M1. The NMOS transistors M1 and M2 form a cascade that amplifies the input signal Vin. The resistors RD1 and RD2 are connected to the power supply VDD, providing load resistance for the NMOS transistors. The feedback network affects the open-loop gain by degenerating M1.
image_name:(c)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: g1}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: g1}
name: RF, type: Resistor, value: RF, ports: {N1: g1, N2: Vout}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
]
extrainfo:The circuit diagram shows a common-source amplifier with feedback. The amplifier uses a feedback resistor RF and a source resistor RS to control the gain. The NMOS transistor M1 is used as the amplifying device. The feedback network affects the open-loop gain of the amplifier.
image_name:(d)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1g2, G: Vin}
name: M2, type: NMOS, ports: {S: d1g2, D: Vout, G: Vout}
name: M3, type: PMOS, ports: {S: VDD, D: d1g2, G: Vout}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: d1g2}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: VF}
name: R2, type: Resistor, value: R2, ports: {N1: VF, N2: GND}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: d1g2}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: Vout}
name: I1S, type: CurrentSource, ports: {Np: d1g2, Nn: GND}
]
extrainfo:The diagram shows a two-stage amplifier with feedback affecting the open-loop gain. It includes feedback resistors R1 and R2, sensing the output voltage Vout and returning a voltage to the source of M1. The feedback network's nonideal input impedance affects the open-loop gain.

Figure 8.45 (a) Noninverting amplifier, (b) implementation using a differential pair, (c) implementation using a CS stage, and (d) implementation using a two-stage amplifier.

As another example, consider the arrangement shown in Fig. 8.45(d), where $R_{1}$ and $R_{2}$ sense $V_{\text {out }}$ and return a voltage to the source of $M_{1}$. Since the output impedance of the feedback network may not be sufficiently small, we surmise that $M_{1}$ is degenerated appreciably even as far as the open-loop forward amplifier is concerned. This circuit exemplifies "input loading" due to the nonideal output impedance of the feedback network.

The important question that we must address with regard to loading is, how do we break the loop while properly including output and input loading effects?

#### Example 8.11

Can the loop be broken at the gate of $M_{2}$ in Fig. 8.45(d) without concern for loading effects?

#### Solution

As illustrated in Fig. 8.46, such an attempt provides the loop gain while avoiding loading issues. However, we are also interested in the open-loop gain and the open-loop input and output impedances, which cannot be obtained from this configuration. We must therefore develop a methodical approach to constructing the open-loop system such that the loading effects are included.

The second difficulty is that some circuits cannot be clearly decomposed into a forward amplifier and a feedback network. In the two-stage network of Fig. 8.47, it is unclear whether $R_{D 2}$ belongs to the
image_name:Figure 8.46
description:
[
name: M1, type: NMOS, ports: {S: GND, D: VF, G: s1}
name: M2, type: NMOS, ports: {S: GND, D: VDD, G: VF}
name: RD1, type: Resistor, value: RD1, ports: {N1: VF, N2: VDD}
name: RD2, type: Resistor, value: RD2, ports: {N1: d2, N2: VDD}
name: R1, type: Resistor, value: R1, ports: {N1: s1, N2: d2}
name: R2, type: Resistor, value: R2, ports: {N1: s1, N2: GND}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: VF, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a two-stage amplifier with NMOS transistors M1 and M2. M1 is connected to a feedback network through resistor RD1. The circuit is powered by a VDD voltage source. The input is applied at node s1 and the output is taken from node d2.

Figure 8.46
image_name:Figure 8.46
description:
[
name: M1, type: NMOS, ports: {S: s1, D: d1s2, G: Vin}
name: M2, type: PMOS, ports: {S: VDD, D: d1s2, G: d1s2}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: d1s2}
name: RD2, type: Resistor, value: RD2, ports: {N1: Vout, N2: GND}
name: RS, type: Resistor, value: RS, ports: {N1: s1, N2: GND}
name: RF, type: Resistor, value: RF, ports: {N1: s1, N2: Vout}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a two-stage amplifier with NMOS transistor M1 and PMOS transistor M2. M1 is connected to a feedback network through resistor RD1. The circuit is powered by a VDD voltage source. The input is applied at node Vin and the output is taken from node Vout. The feedback network consists of resistor RF.

Figure 8.47 Feedback circuit without a clearly-distinguishable feedback network.
feedforward amplifier or the feedback network. We might choose the former case, reasoning that $M_{2}$ needs a load so as to operate as a voltage amplifier, but such a choice seems arbitrary.

The third difficulty in feedback analysis is that some circuits do not readily map to the four canonical topologies studied in the previous sections. For example, a simple degenerated common-source stage does contain feedback because the source resistance measures the drain current, converts it to voltage, and subtracts the result from the input [Fig. 8.48(a)]. However, it is not immediately clear which feedback topology represents this arrangement because the sensed quantity, $I_{D 1}$, is different from the output of interest, $V_{\text {out }}$ [Fig. 8.48(b)].
image_name:(a)
description:
[
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: RS, type: Resistor, value: RS, ports: {N1: S1, N2: GND}
name: M1, type: NMOS, ports: {S: S1, D: Vout, G: Vin}
name: ID1, type: Diode, ports: {Na: S1, Nc: GND}
]
extrainfo:This circuit is a common-source amplifier with degeneration using an NMOS transistor M1. The source is connected to a resistor RS and a diode ID1, providing feedback. The output is taken from the drain and is connected to RD, which is tied to VDD. The input is applied at the gate of M1.
image_name:(b)
description:The block diagram labeled (b) represents a common-source (CS) amplifier stage with feedback. This CS stage consists of several key components:

1. **Main Components:**
- **Transistor (M1):** This is an N-channel MOSFET, which serves as the main amplifying component. It receives an input voltage \( V_{in} \) at its gate.
- **Drain Resistor (R_D):** Connected to the drain of the transistor and to the supply voltage \( V_{DD} \). It helps set the gain and load the transistor.
- **Source Resistor (R_S):** Connected to the source of the transistor and ground. It introduces negative feedback by converting the drain current \( I_{D1} \) into a voltage \( S_1 \) that is subtracted from the input.
- **Output Voltage (V_{out}):** Taken from the drain of the transistor, representing the amplified signal.

2. **Flow of Information or Control:**
- The input signal \( V_{in} \) is applied to the gate of the MOSFET \( M_1 \). The MOSFET amplifies this signal, and the amplified output \( V_{out} \) is taken across \( R_D \).
- The drain current \( I_{D1} \) flows through \( R_S \), creating a voltage drop \( S_1 \). This voltage drop acts as a feedback mechanism, effectively reducing the gate-source voltage and hence the gain of the amplifier.

3. **Labels, Annotations, and Key Indicators:**
- The diagram indicates the direction of current flow \( I_{D1} \) and the position of the output voltage \( V_{out} \).
- \( V_{DD} \) is the supply voltage, providing power to the circuit.

4. **Overall System Function:**
- The primary function of this system is to amplify the input signal \( V_{in} \) while incorporating negative feedback through \( R_S \) to stabilize the gain and improve linearity. The feedback is achieved by sensing the drain current \( I_{D1} \) and converting it to a voltage across \( R_S \), which is subtracted from the input signal, effectively controlling the gain of the amplifier.

(a)
image_name:Figure 8.48 (b)
description:The block diagram in Figure 8.48 (b) represents a feedback amplifier system. This system is designed to amplify an input signal \( V_{in} \) while incorporating feedback to control the gain and improve linearity.

1. **Main Components:**
- **Input Source \( V_{in} \):** This is where the signal to be amplified is introduced into the system.
- **Summing Junction:** The input signal \( V_{in} \) is combined with a feedback signal at this point. The summing junction is depicted with a circle containing a plus and minus sign, indicating the subtraction of the feedback signal from the input.
- **Forward Circuit:** This block represents the main amplifier stage that processes the input signal. The output of this block is the amplified signal \( V_{out} \).
- **Feedback Path (\( \beta \)):** This component represents the feedback network that samples the output and returns a portion of it back to the input. The feedback factor is denoted by \( \beta \).
- **Output \( V_{out} \):** The final output of the system, which is the amplified version of the input signal.
- **Drain Current \( I_{D1} \):** This is a representation of the current flowing through the forward circuit, which is part of the feedback mechanism.

2. **Flow of Information or Control:**
- The input signal \( V_{in} \) is fed into the summing junction.
- At the summing junction, the feedback signal (derived from the output \( V_{out} \) through the feedback path \( \beta \)) is subtracted from the input signal.
- The resulting signal is then passed to the forward circuit block, which amplifies it.
- The output from the forward circuit is \( V_{out} \), which is directed to the output terminal.
- A portion of \( V_{out} \) is fed back through the feedback path \( \beta \) to the summing junction, completing the feedback loop.

3. **Labels, Annotations, and Key Indicators:**
- The diagram is labeled with key indicators such as \( V_{in} \), \( V_{out} \), and \( I_{D1} \) to show the flow of signals.
- The feedback factor is denoted by \( \beta \), indicating the proportion of the output signal that is fed back to the input.

4. **Overall System Function:**
- The primary function of this system is to amplify the input signal \( V_{in} \) while incorporating negative feedback to stabilize the gain and enhance linearity. The feedback loop, represented by \( \beta \), helps in controlling the gain by adjusting the input signal based on the output, thereby maintaining a stable and linear amplification process.

(b)

Figure 8.48 (a) CS stage and (b) block diagram showing the output and sense ports.
The fourth difficulty is that the general feedback system analyzed thus far assumes unilateral stages, i.e., signal propagation in only one direction around the loop. In practice, however, the loop may contain bilateral circuits, allowing signals to flow from the output toward the input through a path other than the
image_name:Figure 8.49
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1g2, G: g1}
name: M2, type: NMOS, ports: {S: Vout, D: VDD, G: d1g2}
name: RD, type: Resistor, value: RD, ports: {N1: d1g2, N2: VDD}
name: CGS2, type: Capacitor, value: CGS2, ports: {Np: d1g2, Nn: g2}
name: RF, type: Resistor, value: RF, ports: {N1: g1, N2: Vout}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: g1, Nn: GND}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit contains two NMOS transistors, M1 and M2, with feedback mechanisms provided by RF and CGS2. M1 is configured with its source connected to ground, while M2's source is connected to the output node Vout. The resistor RD is connected between the drain of M1 and VDD, and the capacitor CGS2 is connected between the gate of M2 and the node d1g2. The current source Iin provides input current at node g1, and ISS is connected between Vout and ground. The circuit demonstrates multiloop feedback with both resistive and capacitive elements.

Figure 8.49 Example of circuit with more than one feedback mechanism.
nominal feedback path. In Fig. 8.47, for example, the signal leaks from the drain of $M_{2}$ to its gate through $C_{G D 2}$ at high frequencies.

The fifth difficulty arises in circuits containing multiple feedback mechanisms (loosely called "multiloop" circuits). In the topology of Fig. 8.49, for example, $R_{F}$ provides feedback around the circuit, and $C_{G S 2}$ around $M_{2}$. We can also say that the source follower itself contains degeneration and hence feedback. We must then ask, which loop should be broken and what exactly do we mean by "loop gain" in this case? Table 8.1 summarizes the five issues described here.

Table 8.1 Feedback analysis difficulties.
image_name:Loading
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: G}
name: R2, type: Resistor, value: R2, ports: {N1: VDD, N2: D}
name: R3, type: Resistor, value: R3, ports: {N1: VDD, N2: Vout}
name: M1, type: NMOS, ports: {S: GND, D: D, G: G}
]
extrainfo:The circuit labeled 'Loading' consists of an NMOS transistor M1 with source connected to ground, drain connected to node D, and gate connected to node G. R1 connects Vin to the gate of M1. R2 connects the drain of M1 to VDD. R3 connects VDD to Vout.
image_name:Ambiguous Decomposition
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1, G: Vin}
name: M2, type: PMOS, ports: {S: VDD, D: d1, G: Vout}
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: Vin}
name: R2, type: Resistor, value: R2, ports: {N1: d1, N2: GND}
name: R3, type: Resistor, value: R3, ports: {N1: d1, N2: Vout}
name: R4, type: Resistor, value: R4, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a multiloop feedback configuration with NMOS and PMOS transistors, resistors, and feedback loops. It demonstrates ambiguous decomposition in feedback analysis.
image_name:Noncanonical Topologies
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: Vout}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: R2, type: Resistor, value: R2, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit represents a noncanonical topology with feedback mechanisms involving an NMOS transistor and resistors. The input is applied at Vin, and the output is taken from Vout.
image_name:Nonunilateral Loop
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: d1}
name: R2, type: Resistor, value: R2, ports: {N1: d2, N2: d3}
name: R3, type: Resistor, value: R3, ports: {N1: d3, N2: Vout}
name: R0, type: Resistor, value: R0, ports: {N1: s1, N2: s3}
name: M1, type: NMOS, ports: {S: GND, D: d1, G: Vin}
name: M2, type: NMOS, ports: {S: GND, D: d2, G: d1}
name: M3, type: NMOS, ports: {S: GND, D: d3, G: d2}
]
extrainfo:The circuit diagram represents a nonunilateral loop topology with three NMOS transistors connected in series, each driving the next stage. The feedback loop is formed using the resistor R0, connecting the source of the first NMOS to the source of the third NMOS.
image_name:Multiple Feedback Mechanisms
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: d1}
name: R2, type: Resistor, value: R2, ports: {N1: s1d2, N2: GND}
name: R3, type: Resistor, value: R3, ports: {N1: s2, N2: Vin}
name: M1, type: NMOS, ports: {S: s1d2, D: d1, G: Vin}
name: M2, type: PMOS, ports: {S: VDD, D: s2, G: d1}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: Vout}
]
extrainfo:The circuit contains multiple feedback mechanisms using resistors and transistors. R1 and M2 create a feedback loop around the PMOS transistor. The NMOS transistor M1 provides another feedback path. I1 is a current source connected from VDD to Vout.

In this chapter, we introduce three methods of feedback circuit analysis. Outlined in Table 8.2, the first employs two-port models to analyze the four canonical topologies while including loading effects.

Table 8.2 Three methods of feedback analysis.

| Two-Port Method | Bode's Method | Middlebrook's Method |
| :---: | :---: | :---: |
| - Computes open-loop and closed-loop quantities and the loop gain. <br> - Includes loading effects. <br> - Neglects feedforward through feedback network. <br> - Can be applied recursively to multiple feedback mechanisms. <br> - Does not apply to noncanonical topologies. | - Computes closed-loop quantities without breaking the loop. <br> - Applies to any topology. <br> - Provides loop gain only if one feedback mechanism is present. | - Computes closed-loop quantities without breaking the loop. <br> - Applies to any topology. <br> - Provides loop gain only if local and global loops are distinguishable. <br> - Reveals effect of reverse loop gain in nonunilateral loops. |

This method proves more efficient than direct analysis of the circuit (with no knowledge of feedback) if the loop is assumed unilateral, i.e., the forward propagation of the input signal through the feedback network is neglected, and so is the backward propagation of the signal through the forward amplifier. The other two methods do not attempt to break the loop and yield the closed-loop quantities exactly but with lengthier algebra.

## 8.5 ■ Effect of Loading

The problem of loading manifests itself when we need to break the feedback loop so as to identify the open-loop system, e.g., calculate the open-loop gain and the input and output impedances. To arrive at the proper procedure for including the feedback network terminal impedances, we first review models of two-port networks.

### 8.5.1 Two-Port Network Models

The simplified amplifier and feedback network models employed in the previous sections may not suffice in general. We must therefore resort to accurate two-port models. For example, the feedback network placed around the feedforward amplifier can be considered a two-port circuit sensing and producing voltages or currents. Recall from basic circuit theory that a two-port linear (and time-invariant) network can be represented by any of the four models shown in Fig. 8.50. The "Z model" in Fig. 8.50(a) consists of input and output impedances in series with current-dependent voltage sources, whereas the "Y model" in Fig. 8.50(b) comprises input and output admittances in parallel with voltage-dependent current sources. The "hybrid models" of Figs. 8.50(c) and (d) incorporate a combination of impedances and admittances and voltage sources and current sources. Each model is described by two equations. For the Z model, we have

$$
\begin{align*}
& V_{1}=Z_{11} I_{1}+Z_{12} I_{2}  \tag{8.57}\\
& V_{2}=Z_{21} I_{1}+Z_{22} I_{2} \tag{8.58}
\end{align*}
$$

Each Z parameter has a dimension of impedance and is obtained by leaving one port open, e.g., $Z_{11}=$ $V_{1} / I_{1}$ when $I_{2}=0$. Similarly, for the Y model,

$$
\begin{align*}
& I_{1}=Y_{11} V_{1}+Y_{12} V_{2}  \tag{8.59}\\
& I_{2}=Y_{21} V_{1}+Y_{22} V_{2} \tag{8.60}
\end{align*}
$$

image_name:(a)
description:
[
name: Z11, type: Resistor, value: Z11, ports: {N1: ViP, N2: X1}
name: Z12, type: Resistor, value: Z12, ports: {N1: X1, N2: Vin}
name: Z21, type: Resistor, value: Z21, ports: {N1: X1, N2: V2n}
name: Z22, type: Resistor, value: Z22, ports: {N1: V2n, N2: V2P}
name: Y11, type: Resistor, value: Y11, ports: {N1: ViP, N2: Vin}
name: Y12, type: Resistor, value: Y12, ports: {N1: V2P, N2: V2n}
name: Y21, type: CurrentSource, value: Y21, ports: {Np: V2P, Nn: V2n}
name: Y22, type: Resistor, value: Y22, ports: {N1: V2P, N2: V2n}
name: H11, type: Resistor, value: H11, ports: {N1: ViP, N2: X1}
name: H12, type: VoltageSource, value: H12, ports: {Np: X1, Nn: Vin}
name: H21, type: CurrentSource, value: H21, ports: {Np: X1, Nn: V2n}
name: H22, type: Resistor, value: H22, ports: {N1: V2n, N2: V2P}
name: G11, type: Resistor, value: G11, ports: {N1: ViP, N2: Vin}
name: G12, type: CurrentSource, value: G12, ports: {Np: ViP, Nn: Vin}
name: G21, type: VoltageSource, value: G21, ports: {Np: V2P, Nn: V2n}
name: G22, type: Resistor, value: G22, ports: {N1: V2P, N2: V2n}
]
extrainfo:The diagram shows different linear two-port network models, including Z, Y, H, and G parameters. Each model is represented with specific components and sources to describe the relationships between voltages and currents at the ports.
image_name:(b)
description:
[
name: Y11, type: CurrentSource, ports: {Np: Vin, Nn: V1}
name: Y12, type: CurrentSource, ports: {Np: V2, Nn: V2p}
name: Y21, type: CurrentSource, ports: {Np: Vin, Nn: V2n}
name: Y22, type: Resistor, value: Y22, ports: {N1: V2, N2: V2n}
]
extrainfo:The circuit diagram (b) represents a two-port network using the Y-parameter model. It includes current sources Y11, Y12, Y21, and a resistor Y22. The nodes are labeled as Vin, V1, V2, V2p, and V2n, indicating input, output, and intermediate connections.
image_name:(c)
description:
[
name: H11, type: Resistor, value: H11, ports: {N1: Vin, N2: X1}
name: H12, type: VoltageSource, value: H12, ports: {Np: X1, Nn: V1}
name: H21, type: CurrentSource, ports: {Np: V1, Nn: V2n}
name: H22, type: Resistor, value: H22, ports: {N1: V2n, N2: V2p}
]
extrainfo:This circuit represents the H-parameter model of a linear two-port network. It includes a resistor (H11), a voltage source (H12), a current source (H21), and another resistor (H22). The model is used to describe the relationship between input and output voltages and currents in terms of hybrid parameters.
image_name:(d)
description:
[
name: G11, type: CurrentSource, ports: {Np: Vin, Nn: Vip}
name: G12, type: CurrentControlledVoltageSource, value: G12, ports: {Np: Vin, Nn: X1}
name: G21, type: VoltageControlledCurrentSource, value: G21, ports: {Np: X1, Nn: V2n}
name: G22, type: Resistor, value: G22, ports: {N1: V2n, N2: V2p}
]
extrainfo:This is a G-parameter model of a two-port network, where G11 is a current source, G12 is a current-controlled voltage source, G21 is a voltage-controlled current source, and G22 is a resistor.

Figure 8.50 Linear two-port network models.
where each Y parameter is calculated by shorting one port, e.g., $Y_{11}=I_{1} / V_{1}$ when $V_{2}=0$. For the H model,

$$
\begin{align*}
& V_{1}=H_{11} I_{1}+H_{12} V_{2}  \tag{8.61}\\
& I_{2}=H_{21} I_{1}+H_{22} V_{2} \tag{8.62}
\end{align*}
$$

and for the G model,

$$
\begin{align*}
I_{1} & =G_{11} V_{1}+G_{12} I_{2}  \tag{8.63}\\
V_{2} & =G_{21} V_{1}+G_{22} I_{2} \tag{8.64}
\end{align*}
$$

Note that, for example, $Y_{11}$ may not be equal to the inverse of $Z_{11}$ because the two are obtained under different conditions: the output is shorted for the former but left open for the latter.

It is instructive to compare the general two-port models with the simplified amplifier representations that we have used in the previous sections. For example, let us consider the voltage amplifier model in Example 8.3 vis-à-vis the Z model. We observe that (1) absent in the former, $Z_{12} I_{2}$ represents the amplifier's internal feedback, e.g., due to $C_{G D}$; (2) if $Z_{12}$ is zero, then $Z_{11}$ is equal to $Z_{i n}$, the input impedance calculated with the output left open; and (3) $Z_{22}$ is not necessarily equal to $Z_{\text {out }}$ : the former is computed with the input port left open and the latter with the input shorted.

The most important drawback of the Z model for our purposes is that its output generator, $Z_{21} I_{1}$, is controlled by the input current rather than the input voltage. For a MOS circuit with the input applied to the gate, this model becomes meaningless if the input capacitance is neglected. The H model entails the same difficulty.

Do any of the two-port models agree with our intuitive picture of voltage amplifiers? Yes, the G model is close. If the internal feedback, $G_{12} I_{2}$, is neglected, then $G_{11}\left(=I_{1} / V_{1}\right.$ with $\left.I_{2}=0\right)$ represents the inverse of the input impedance, and $G_{22}\left(=V_{2} / I_{2}\right.$ with $\left.V_{1}=0\right)$ the output impedance. The reader can try this exercise for the other three types of amplifiers.

### 8.5.2 Loading in Voltage-Voltage Feedback

As mentioned before, the Z and H models fail to represent voltage amplifiers if the input current is very small—as in a simple CS stage. We therefore choose the G model here. ${ }^{13}$ The complete equivalent circuit is shown in Fig. 8.51(a), where the forward and feedback network parameters are denoted by upper-case and lower-case letters, respectively. Since the input port of the feedback network is connected to the output port of the forward amplifier, $g_{11}$ and $g_{12} I_{\text {in }}$ are tied to $V_{\text {out }}$.

It is possible to solve this circuit exactly, but we simplify the analysis by neglecting two quantities: the amplifier's internal feedback, $G_{12} V_{\text {out }}$, and the "forward" propagation of the input signal through the feedback network, $g_{12} I_{i n}$. In other words, the loop is "unilateralized." Figure 8.51(b) depicts the resulting circuit with our intuitive amplifier notations ( $Z_{i n}, Z_{\text {out }}, A_{0}$ ) added to indicate equivalencies. Let us first directly compute the closed-loop voltage gain. Recognizing that $g_{11}$ is an admittance and $g_{22}$ an impedance, we write a KVL around the input network and a KCL at the output node:

$$
\begin{array}{r}
V_{\text {in }}=V_{e}+g_{22} \frac{V_{e}}{Z_{\text {in }}}+g_{21} V_{\text {out }} \\
g_{11} V_{\text {out }}+\frac{V_{\text {out }}-A_{0} V_{e}}{Z_{\text {out }}}=0 \tag{8.66}
\end{array}
$$

[^55]image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: G11, type: Resistor, value: G11, ports: {N1: Vip, N2: X1}
name: G22, type: Resistor, value: G22, ports: {N1: X2, N2: Voutp}
name: g22, type: Resistor, value: g22, ports: {N1: X1, N2: X2}
name: Ao, type: VoltageControlledVoltageSource, value: Ao, ports: {Np: Vout, Nn: Voutn}
name: G12Vout, type: CurrentControlledCurrentSource, ports: {Np: Vip, Nn: X1}
name: G21Ve, type: CurrentControlledCurrentSource, ports: {Np: X1, Nn: X2}
name: g21Vout, type: CurrentControlledCurrentSource, ports: {Np: Vin, Nn: X2}
name: g12Iin, type: CurrentControlledCurrentSource, ports: {Np: Vin, Nn: Voutn}
name: ZinG21Ve, type: VoltageControlledVoltageSource, ports: {Np: X1, Nn: Voutn}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: Vip, Nn: Vin}
]
extrainfo:The circuit diagram represents a voltage-voltage feedback configuration with a feedback network modeled by a G model. It includes a voltage source Vin, resistors G11 and G22, and multiple controlled sources. The configuration aims to analyze the closed-loop voltage gain with feedback.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: G11, type: Resistor, value: G11, ports: {N1: Vip, N2: X1}
name: G12, type: CurrentControlledVoltageSource, value: G12Vout, ports: {Np: Vip, Nn: X1}
name: G21, type: VoltageControlledVoltageSource, value: G21Ve, ports: {Np: X1, Nn: X2}
name: G22, type: Resistor, value: G22, ports: {N1: X2, N2: Voutp}
name: g22, type: Resistor, value: g22, ports: {N1: Vin, N2: X1}
name: g21, type: VoltageControlledVoltageSource, value: g21Vout, ports: {Np: X1, Nn: Vin}
name: g12, type: CurrentControlledCurrentSource, value: g12Iin, ports: {Np: Vin, Nn: Vinn}
name: Zin, type: Resistor, value: Zin, ports: {N1: Vip, N2: X1}
name: Ao, type: VoltageControlledVoltageSource, value: AoVe, ports: {Np: Voutp, Nn: Voutn}
]
extrainfo:The circuit diagram represents a voltage-voltage feedback system with a G model feedback network. It simplifies the feedback network to analyze closed-loop voltage gain. The circuit includes various controlled sources and resistors to model the feedback and input-output relationships.

Figure 8.51 Voltage-voltage feedback circuit with (a) feedback network represented by a G model and (b) a simplified G model.

Finding $V_{e}$ from the latter equation and substituting the result in the former, we have

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=\frac{A_{0}}{\left(1+\frac{g_{22}}{Z_{\text {in }}}\right)\left(1+g_{11} Z_{\text {out }}\right)+g_{21} A_{0}} \tag{8.67}
\end{equation*}
$$

It is desirable to express the closed-loop gain in the familiar form, $A_{v, \text { open }} /\left(1+\beta A_{v, \text { open }}\right)$. To this end, we divide the numerator and the denominator by $\left(1+g_{22} / Z_{\text {in }}\right)\left(1+g_{11} Z_{\text {out }}\right)$ :

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=\frac{\frac{A_{0}}{\left(1+\frac{g_{22}}{Z_{\text {in }}}\right)\left(1+g_{11} Z_{\text {out }}\right)}}{1+g_{21} \frac{A_{0}}{\left(1+\frac{g_{22}}{Z_{\text {in }}}\right)\left(1+g_{11} Z_{\text {out }}\right)}} \tag{8.68}
\end{equation*}
$$

We can thus write

$$
\begin{align*}
A_{v, \text { open }} & =\frac{A_{0}}{\left(1+\frac{g_{22}}{Z_{\text {in }}}\right)\left(1+g_{11} Z_{\text {out }}\right)}  \tag{8.69}\\
\beta & =g_{21} \tag{8.70}
\end{align*}
$$

Let us now interpret these results. The equivalent open-loop gain contains a factor $A_{0}$, i.e., the original amplifier's voltage gain (before immersion in feedback). But this gain is attenuated by two factors, namely, $1+g_{22} / Z_{\text {in }}$ and $1+g_{11} Z_{\text {out }}$. Interestingly, we can write $1+g_{22} / Z_{\text {in }}=\left(Z_{\text {in }}+g_{22}\right) / Z_{\text {in }}$, concluding that $A_{0}$ is multiplied by $Z_{i n} /\left(Z_{i n}+g_{22}\right)$, which reminds us of a voltage divider. Similarly, $1+g_{11} Z_{\text {out }}=\left(g_{11}^{-1}+Z_{\text {out }}\right) / g_{11}^{-1}$, whose inverse points to another voltage divider. The loaded forward amplifier now emerges as shown in Fig. 8.52. Note that this model excludes the two generators $G_{12} V_{\text {out }}$ and $g_{12} I_{i n}$, which are generally not negligible.
image_name:Figure 8.52
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin+, Nn: GND}
name: Ve, type: VoltageSource, value: Ve, ports: {Np: "Vin", Nn: Vin+}
name: Zin, type: Resistor, value: Zin, ports: {N1: "Vin", N2: X2}
name: A0Ve, type: VoltageSource, value: A0Ve, ports: {Np: X1, Nn: X2}
name: Zout, type: Resistor, value: Zout, ports: {N1: X1, N2: Vout}
name: g11, type: CurrentSource, value: g11, ports: {Np: Vout, Nn: GND}
name: g22, type: CurrentSource, value: g22, ports: {Np: X2, Nn: GND}
]
extrainfo:The circuit is a voltage-voltage feedback amplifier with input and output impedances represented by Zin and Zout. The amplifier is loaded with a feedback network, excluding the generators G12 Vout and g12 Iin, for simplification.

Figure 8.52 Proper method of including loading in a voltage-voltage feedback circuit.
The reader may wonder why we go to the trouble of finding the open-loop parameters while the closed-loop circuit in Fig. 8.51(a) can be solved exactly. The key principle here is that the rules depicted in Fig. 8.52 afford us a quick and intuitive understanding of the circuit that would not be possible from the direct analysis of Fig. 8.51(a). Specifically, we recognize that the finite input and output impedances of the feedback network reduce the output voltage and the voltage seen by the input of the main amplifier, respectively.

It is important to note that $g_{11}$ and $g_{22}$ in Fig. 8.50 are computed as follows:

$$
\begin{align*}
& g_{11}=\left.\frac{I_{1}}{V_{1}}\right|_{I 2=0}  \tag{8.71}\\
& g_{22}=\left.\frac{V_{2}}{I_{2}}\right|_{V 1=0} \tag{8.72}
\end{align*}
$$

Thus, as illustrated in Fig. 8.53, $g_{11}$ is obtained by leaving the output of the feedback network open whereas $g_{22}$ is calculated by shorting the input of the feedback network.
image_name:Figure 8.53
description:The system block diagram depicted in Figure 8.53 represents a voltage-voltage feedback loop with proper loading. The main components of this system include:

1. **Summing Junction (+/-):** This is where the input voltage $V_{in}$ enters the system. The summing junction combines $V_{in}$ with the feedback signal coming from the feedback network.

2. **Main Amplifier ($A_0$):** The amplifier receives the signal from the summing junction and amplifies it. The output of the amplifier is $V_{out}$.

3. **Feedback Network:** There are two identical blocks labeled with the gain factor $\beta$. These blocks are part of the feedback path that takes a portion of the output $V_{out}$ and feeds it back to the input. The feedback network is responsible for stabilizing the system and controlling the gain.

4. **Feedback Paths ($g_{22}$ and $g_{11}^{-1}$):**
- $g_{22}$ indicates the path where the output of the feedback network is open. This path is connected back to the summing junction.
- $g_{11}^{-1}$ indicates the path where the input of the feedback network is shorted, providing another feedback loop.

**Flow of Information:**
- The input signal $V_{in}$ is combined with the feedback signal at the summing junction. The resulting signal is amplified by the main amplifier $A_0$.
- The amplified output $V_{out}$ is split into two paths that pass through identical feedback blocks with gain $\beta$.
- One feedback path is connected back to the summing junction through $g_{22}$, and the other is through $g_{11}^{-1}$, completing the feedback loop.

**Overall System Function:**
The primary function of this system is to provide a controlled amplification of the input signal $V_{in}$ to produce the output $V_{out}$. The feedback network ensures stability and adjusts the gain to maintain the desired performance. By opening and shorting specific paths, the system can measure and adjust parameters like $g_{11}$ and $g_{22$, which are critical for determining the input and output impedances and the loop gain of the system.

Figure 8.53 Conceptual view of opening a voltage-voltage feedback loop with proper loading.

Another important result of the foregoing analysis is that the loop gain, i.e., the second term in the denominator of (8.68), is simply equal to the loaded open-loop gain multiplied by $g_{21}$. Thus, a separate calculation of the loop gain is not necessary. Also, the open-loop input and output impedances obtained from Fig. 8.52 are scaled by $1+g_{21} A_{v, \text { open }}$ to yield the closed-loop values. Again, we must bear in mind that this loop gain neglects the effect of $G_{12} V_{\text {out }}$ and $g_{12} I_{i n}$.

#### Example 8.12

For the circuit shown in Fig. 8.54(a), calculate the open-loop and closed-loop gains assuming $\lambda=\gamma=0$.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: Vin}
name: M2, type: PMOS, ports: {S: VDD, D: X, G: Vout}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: X}
name: RD2, type: Resistor, value: RD2, ports: {N1: Vout, N2: GND}
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: SI}
name: RF, type: Resistor, value: RF, ports: {N1: SI, N2: Vout}
name: SI, type: Switch, ports: {N1: SI, N2: M1}
]
extrainfo:The circuit in Fig. 8.54(a) is a two-stage amplifier with negative feedback provided by the resistors RF and RS. Transistor M1 is configured as a common-source amplifier, and transistor M2 as a common-gate amplifier. The feedback network senses the output voltage and returns a fraction to the source of M1, ensuring negative feedback.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: S1, D: X, G: Vin}
name: M2, type: PMOS, ports: {S: VDD, D: X, G: Y}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: X}
name: RS, type: Resistor, value: RS, ports: {N1: S1, N2: GND}
name: RF, type: Resistor, value: RF, ports: {N1: S1, N2: X}
name: RD2, type: Resistor, value: RD2, ports: {N1: Y, N2: GND}
]
extrainfo:The circuit in Fig. 8.54(b) is a common-source amplifier with feedback. The feedback network consists of resistors RS and RF, which return a fraction of the output voltage to the source of M1. The circuit uses two stages, with M1 being an NMOS transistor and M2 being a PMOS transistor, and it operates with a supply voltage VDD. The feedback is negative, stabilizing the gain.

Figure 8.54

#### Solution

The circuit consists of two common-source stages, with $R_{F}$ and $R_{S}$ sensing the output voltage and returning a fraction thereof to the source of $M_{1}$. This transistor subtracts the returned voltage from $V_{i n}$. The reader can prove that the feedback is indeed negative. Following the procedure illustrated in Fig. 8.53, we identify $R_{F}$ and $R_{S}$ as the feedback network and construct the open-loop circuit as shown in Fig. 8.54(b). Note that the loading effect in the input network is obtained by shorting the right terminal of $R_{F}$ to ground and that in the output by leaving the left terminal of $R_{F}$ open. Neglecting channel-length modulation and body effect for simplicity, we observe that $M_{1}$ is degenerated by the feedback network and

$$
\begin{equation*}
A_{v, \text { open }}=\frac{V_{Y}}{V_{\text {in }}}=\frac{-R_{D 1}}{R_{F} \| R_{S}+1 / g_{m 1}}\left\{-g_{m 2}\left[R_{D 2} \|\left(R_{F}+R_{S}\right)\right]\right\} \tag{8.73}
\end{equation*}
$$

To compute the closed-loop gain, we first find the loop gain as $g_{21} A_{v, \text { open }}$. Recall from (8.64) that $g_{21}=V_{2} / V_{1}$ with $I_{2}=0$. For the voltage divider consisting of $R_{F}$ and $R_{S}, g_{21}=R_{S} /\left(R_{F}+R_{S}\right)$. The closed-loop gain is simply equal to $A_{v, \text { closed }}=A_{v, \text { open }} /\left(1+g_{21} A_{v, \text { open }}\right)$.

Can we include $R_{D 2}$ in the feedback network rather than in the forward amplifier? Yes, we can ascribe a finite $r_{O}$ to $M_{2}$ and proceed while considering $R_{D 2}, R_{F}$, and $R_{S}$ as the feedback network. The result is slightly different from that obtained above.

The above analysis neglects the forward amplifier's internal feedback (e.g., due to $C_{G D 2}$ ) and the propagation of the input signal from the source of $M_{1}$ and through $R_{F}$ to the output. (Transistor $M_{1}$ also operates as a source follower in this case.)

#### Example 8.13

A student eager to understand the approximations leading to the circuit in Fig. 8.51(b) decides to use an H model for the forward amplifier and obtain an exact solution. Perform this analysis and explain the results.

#### Solution

Illustrated in Fig. 8.55, this representation is attractive as it allows a simple series connection of voltages and impedances at the input and a parallel connection at the output. Writing a KVL and a KCL gives

$$
\begin{array}{r}
V_{\text {in }}=I_{\text {in }} H_{11}+H_{12} V_{\text {out }}+I_{\text {in }} g_{22}+g_{21} V_{\text {out }} \\
H_{22} V_{\text {out }}+H_{21} I_{\text {in }}+g_{11} V_{\text {out }}+g_{12} I_{\text {in }}=0 \tag{8.75}
\end{array}
$$

image_name:Figure 8.55
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: "Vin"}
name: H11, type: Resistor, value: H11, ports: {N1: "Vin", N2: X1}
name: H12, type: CurrentControlledVoltageSource, value: H12, ports: {Np: X1, Nn: X2}
name: H21, type: VoltageControlledCurrentSource, value: H21, ports: {Np: VoutP, Nn: VoutN}
name: H22, type: Resistor, value: H22, ports: {N1: VoutP, N2: VoutN}
name: g22, type: Resistor, value: g22, ports: {N1: X2, N2: X3}
name: g21, type: VoltageControlledCurrentSource, value: g21, ports: {Np: VoutP, Nn: Vin}
name: g12, type: CurrentControlledVoltageSource, value: g12, ports: {Np: Vin, Nn: "Vin"}
name: g11, type: Resistor, value: g11, ports: {N1: VoutP, N2: VoutN'}
]
extrainfo:The circuit is a hybrid-pi model with voltage and current sources controlled by other voltages and currents. It features series and parallel connections of impedances and sources, providing a representation for analyzing input and output relationships in terms of voltages and currents.

Figure 8.55

Finding $I_{i n}$ from the latter and replacing it in the former, we have

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=\frac{-\frac{H_{21}+g_{12}}{\left(H_{22}+g_{11}\right)\left(H_{11}+g_{22}\right)}}{1-\left(H_{12}+g_{21}\right) \frac{H_{21}+g_{12}}{\left(H_{22}+g_{11}\right)\left(H_{11}+g_{22}\right)}} \tag{8.76}
\end{equation*}
$$

We can thus define

$$
\begin{align*}
A_{v, \text { open }} & =-\frac{H_{21}+g_{12}}{\left(H_{22}+g_{11}\right)\left(H_{11}+g_{22}\right)}  \tag{8.77}\\
\beta & =H_{12}+g_{21} \tag{8.78}
\end{align*}
$$

If we assume that $g_{12} \ll H_{21}$ and $H_{12} \ll g_{21}$, then

$$
\begin{align*}
A_{v, \text { open }} & =\frac{-H_{21}}{\left(H_{22}+g_{11}\right)\left(H_{11}+g_{22}\right)}  \tag{8.79}\\
\beta & =g_{21} \tag{8.80}
\end{align*}
$$

and the attenuation factors $H_{22}+g_{11}$ and $H_{11}+g_{22}$ can be interpreted in the same manner as those in Eq. (8.69). This approach therefore explicitly reveals the simplifying approximations, namely, $g_{12} \ll H_{21}$ and $H_{12} \ll g_{21}$. Unfortunately, however, for a MOS gate input, $H_{21}$ (the "current gain") approaches infinity, making the model difficult to use.

### 8.5.3 Loading in Current-Voltage Feedback

In this case, the feedback network appears in series with the output so as to sense the current. We represent the forward amplifier and the feedback network by Y and Z models, respectively (Fig. 8.56), neglecting the generators $Y_{12} V_{\text {out }}$ and $z_{12} I_{\text {in }}$. We wish to compute the closed-loop gain, $I_{\text {out }} / V_{\text {in }}$, and therefrom determine how the open-loop parameters can be obtained in the presence of loading. Noting that $I_{i n}=Y_{11} V_{e}$ and $I_{2}=I_{i n}$, we write two KVLs:

$$
\begin{align*}
V_{\text {in }} & =V_{e}+Y_{11} V_{e} z_{22}+z_{21} I_{\text {out }}  \tag{8.81}\\
-I_{\text {out }} z_{11} & =\frac{I_{\text {out }}-Y_{21} V_{e}}{Y_{22}} \tag{8.82}
\end{align*}
$$

image_name:Figure 8.56 Current-voltage feedback circuit with loading
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Y11, type: Resistor, value: Y11, ports: {N1: Vip, N2: x1}
name: Y22, type: Resistor, value: Y22, ports: {N1: x1, N2: x2}
name: Z22, type: Resistor, value: Z22, ports: {N1: x1, N2: x2}
name: Z11, type: Resistor, value: Z11, ports: {N1: x1, N2: x2}
name: Y21Ve, type: VoltageControlledCurrentSource, value: Y21Ve, ports: {Np: Vip, Nn: x1}
name: Z21, type: VoltageSource, value: Z21, ports: {Np: x2, Nn: Vin}
]
extrainfo:The circuit is a current-voltage feedback circuit with loading. It includes a voltage source Vin, resistors Y11, Y22, Z22, Z11, a voltage-controlled current source Y21Ve, and a voltage source Z21. The nodes are labeled as Vin, Vip, Ve, x1, x2, and Iout. The circuit is designed to analyze the closed-loop gain Iout/Vin in the presence of loading.

Figure 8.56 Current-voltage feedback circuit with loading.

Finding $V_{e}$ from the latter and substituting in the former, we have

$$
\begin{equation*}
\frac{I_{\text {out }}}{V_{\text {in }}}=\frac{\frac{Y_{21}}{\left(1+z_{22} Y_{11}\right)\left(1+z_{11} Y_{22}\right)}}{1+z_{21} \frac{Y_{21}}{\left(1+z_{22} Y_{11}\right)\left(1+z_{11} Y_{22}\right)}} \tag{8.83}
\end{equation*}
$$

We can thus visualize the open-loop gain and the feedback factor as

$$
\begin{align*}
G_{m, \text { open }} & =\frac{Y_{21}}{\left(1+z_{22} Y_{11}\right)\left(1+z_{11} Y_{22}\right)}  \tag{8.84}\\
\beta & =z_{21} \tag{8.85}
\end{align*}
$$

Note that $Y_{21}$ is in fact the transconductance gain, $G_{m}$, of the original amplifier. The two attenuation factors $\left(1+z_{22} Y_{11}\right)^{-1}$ and $\left(1+z_{11} Y_{22}\right)^{-1}$ respectively correspond to voltage division at the input and current division at the output, allowing us to construct the loaded open-loop forward amplifier as shown in Fig. 8.57. Since $z_{22}=V_{2} / I_{2}$ with $I_{1}=0$ and $z_{11}=V_{1} / I_{1}$ with $I_{2}=0$, we arrive at the conceptual picture depicted in Fig. 8.58 for properly breaking the feedback. Note that the loop gain is equal to $z_{21} G_{m, \text { open }}$.
image_name:Figure 8.57
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vip, Nn: Vin}
name: Y11, type: Resistor, value: Y11, ports: {N1: Vip, N2: Ve}
name: Z22, type: Resistor, value: Z22, ports: {N1: Vin, N2: X1}
name: GmVe, type: VoltageControlledCurrentSource, ports: {Np: X1, Nn: X2}
name: Y22, type: Resistor, value: Y22, ports: {N1: X1, N2: X2}
name: Z11, type: Resistor, value: Z11, ports: {N1: X1, N2: X2}
]
extrainfo:The circuit is a current-voltage feedback circuit with a voltage source Vin, resistors Y11, Z22, Y22, Z11, and a voltage-controlled current source GmVe. The feedback is properly loaded with resistors.

Figure 8.57 Current-voltage feedback circuit with proper loading of feedback network.
image_name:Figure 8.57
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Gm, type: VoltageControlledCurrentSource, value: Gm, ports: {Np: GmOut, Nn: GND}
name: Z22, type: Other, value: Z22, ports: {N1: Vin, N2: GmOut}
name: Z11, type: Resistor, value: Z11, ports: {N1: GmOut, N2: GND}
]
extrainfo:The circuit is a current-voltage feedback circuit with a voltage source Vin, resistors Z22, Z11, and a voltage-controlled current source GmVe. The feedback network is properly loaded with resistors.

Figure 8.58 Conceptual view of opening the loop in current-voltage feedback.

#### Example 8.14

A PMOS current source delivers a current to a load, e.g., the rechargeable battery in a cell phone [Fig. 8.59(a)]. We wish to make this current less PVT-dependent by means of negative feedback. As shown in Fig. 8.59(b), we convert the output current to voltage by a small series resistor, $r_{M}$, compare this voltage with a reference by means of an amplifier, and return the result to the gate of $M_{1}$. Determine the output current and the impedance seen by the load.
image_name:(a)
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: d1, G: Vb}
name: A1, type: OpAmp, value: A1, ports: {InP: s1, InN: Vb, OutP: s1, OutN: '}
name: rM, type: Resistor, value: rM, ports: {N1: d1, N2: GND'}
]
extrainfo:The circuit in diagram (a) is a PMOS current source with feedback to stabilize the output current. The PMOS transistor M1 is controlled by a feedback loop including an op-amp A1 and a resistor rM. The output current Iout is drawn from the drain of M1 and flows through the load to ground. The feedback loop aims to make the output current less dependent on process, voltage, and temperature variations.
image_name:(b)
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: X, G: S1}
name: A1, type: OpAmp, ports: {InP: X, InN: Y, OutP: S1}
name: rM, type: Resistor, value: rM, ports: {N1: Y, N2: GND}
]
extrainfo:The circuit implements a PMOS current source with negative feedback to stabilize the output current. The feedback network consists of a resistor rM, and the amplifier A1 compares the voltage across rM with a reference voltage Vb.
image_name:(c)
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: d1, G: InP(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: Vb, InN: InP(A1), OutP: InP(A1)}
name: rM, type: Resistor, value: rM, ports: {N1: InP(A1), N2: GND}
]
extrainfo:The circuit in Figure 8.59(c) is a PMOS current source with negative feedback implemented through an op-amp and a feedback resistor rM. The output current Iout is stabilized by the feedback loop, which compares the voltage across rM with a reference voltage Vb.
image_name:(d)
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: d1, G: InP(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: Vb, InN: X1, OutP: InP(A1)}
name: rM, type: Resistor, value: rM, ports: {N1: X1, N2: GND}
]
extrainfo:The circuit is a PMOS current source with negative feedback to stabilize the output current. The feedback network consists of a resistor rM, converting the output current to a voltage for comparison with a reference voltage Vb using an op-amp A1. The goal is to make the output current less dependent on process, voltage, and temperature variations.

Figure 8.59

#### Solution

We view $V_{b}$ as the input voltage and recognize that $r_{M}$ sustains a voltage approximately equal to $V_{b}$ if the loop gain is high. That is, $I_{\text {out }} \approx V_{b} / r_{M}$. But let us analyze this arrangement more accurately. Redrawing the circuit as in Fig. 8.59(c), we identify $A_{1}$ and $M_{1}$ as the forward transconductance amplifier and $r_{M}$ as the feedback network. The procedure depicted in Fig. 8.58 leads to the open-loop topology of Fig. 8.59(d), and hence

$$
\begin{align*}
G_{m, \text { open }} & =\frac{I_{\text {out }}}{V_{b}}  \tag{8.86}\\
& \approx A_{1} g_{m} \tag{8.87}
\end{align*}
$$

where the current flowing through $r_{O}$ is neglected. The feedback factor $\beta=z_{21}=r_{M}$. Thus, the closed-loop output current is given by

$$
\begin{equation*}
I_{\text {out }}=\frac{A_{1} g_{m}}{1+A_{1} g_{m} r_{M}} V_{b} \tag{8.88}
\end{equation*}
$$

In the open-loop configuration, the load sees an impedance of $r_{O}+r_{M}$. Since feedback regulates the output current, the impedance seen by the load rises by a factor of $1+A_{1} g_{m} r_{M}$, reaching $Z_{\text {out }}=\left(1+A_{1} g_{m} r_{M}\right)\left(r_{O}+r_{M}\right)$.

A critical point emerging from this example is that the output impedance of a current-voltage feedback topology must be obtained by breaking the output current path and measuring the impedance between the resulting two nodes [e.g., $X$ and $Y$ in Fig. 8.59(b)]. In the above calculations, the "impedance seen by the load" is in fact computed by replacing the load with a voltage source and measuring the current through it.

### 8.5.4 Loading in Voltage-Current Feedback

In this configuration, the forward (transimpedance) amplifier generates an output voltage in response to the input current and can thus be represented by a Z model. Sensing the output voltage and returning a proportional current, the feedback network lends itself to a Y model. The equivalent circuit is shown in Fig. 8.60, where the effect of $Z_{12}$ and $y_{12}$ is neglected. As in previous cases, we compute the closed-loop
image_name:Figure 8.60
description:
[
name: Iin, type: CurrentSource, value: Iin, ports: {Np: X1, Nn: X2}
name: Z11, type: Resistor, value: Z11, ports: {N1: X1, N2: X3}
name: Z21, type: VoltageControlledVoltageSource, ports: {Np: X3, Nn: VoutP}
name: Z22, type: Resistor, value: Z22, ports: {N1: VoutP, N2: Vout}
name: Y22, type: Resistor, value: Y22, ports: {N1: X1, N2: X4}
name: Y21, type: CurrentControlledCurrentSource, ports: {Np: X4, Nn: X2}
name: Y11, type: Resistor, value: Y11, ports: {N1: X4, N2: Vout}
]
extrainfo:The circuit is a voltage-current feedback configuration with loading. It consists of a transimpedance amplifier that generates an output voltage in response to the input current. The feedback network senses the output voltage and returns a proportional current. The effect of Z12 and y12 is neglected in the analysis.

Figure 8.60 Voltage-current feedback circuit with loading.
gain, $V_{\text {out }} / I_{\text {in }}$, by writing two equations:

$$
\begin{array}{r}
I_{\text {in }}=I_{e}+I_{e} Z_{11} y_{22}+y_{21} V_{\text {out }} \\
y_{11} V_{\text {out }}+\frac{V_{\text {out }}-Z_{21} I_{e}}{Z_{22}}=0 \tag{8.90}
\end{array}
$$

Eliminating $I_{e}$, we obtain

$$
\begin{equation*}
\frac{V_{\text {out }}}{I_{\text {in }}}=\frac{\frac{Z_{21}}{\left(1+y_{22} Z_{11}\right)\left(1+y_{11} Z_{22}\right)}}{1+y_{21} \frac{Z_{21}}{\left(1+y_{22} Z_{11}\right)\left(1+y_{11} Z_{22}\right)}} \tag{8.91}
\end{equation*}
$$

Thus, the equivalent open-loop gain and feedback factor are given by

$$
\begin{align*}
R_{0, \text { open }} & =\frac{Z_{21}}{\left(1+y_{22} Z_{11}\right)\left(1+y_{11} Z_{22}\right)}  \tag{8.92}\\
\beta & =y_{21} \tag{8.93}
\end{align*}
$$

Interpreting the attenuation factors in $R_{0, \text { open }}$ as current division at the input and voltage division at the output, we arrive at the conceptual view in Fig. 8.61. The loop gain is given by $y_{21} R_{0, \text { open }}$.
image_name:Figure 8.61
description:The block diagram in Figure 8.61 represents a conceptual view of opening the loop in a voltage-current feedback system. This diagram is focused on illustrating the feedback mechanism and how it affects the open-loop gain.

1. **Main Components:**
- **Current Source (I_in):** This is the input current source that feeds into the system.
- **Summing Junction (+/-):** This block combines the input current with the feedback current. It has a positive and a negative input, indicating subtraction of the feedback signal from the input.
- **Feedback Blocks (β):** These blocks represent the feedback factor β, which is used to control the amount of feedback current affecting the system.
- **Inverse Admittance Blocks (Y_22⁻¹ and Y_11⁻¹):** These blocks represent the inverse admittance, which is used to model the impedance seen by the feedback network.
- **Amplifier (R_0,open):** This block represents the open-loop amplifier with a gain of R_0,open, which is the equivalent open-loop gain of the system.
- **Output (V_out):** This is the output voltage of the system, which is the result of the amplified input signal after feedback correction.

2. **Flow of Information or Control:**
- The input current (I_in) enters the summing junction, where it is combined with the feedback current.
- The feedback current is derived from the output voltage (V_out) and is processed through the feedback blocks (β) and inverse admittance blocks (Y_22⁻¹ and Y_11⁻¹).
- The combined signal at the summing junction is then fed into the amplifier (R_0,open), which amplifies the signal and produces the output voltage (V_out).
- The output voltage (V_out) is used to generate the feedback signal, closing the loop.

3. **Labels, Annotations, and Key Indicators:**
- The diagram is labeled with key parameters such as β, Y_22⁻¹, Y_11⁻¹, and R_0,open, which are critical for understanding the gain and feedback characteristics of the system.
- The direction of current flow and the feedback loop is clearly indicated.

4. **Overall System Function:**
- The primary function of this system is to demonstrate how feedback can be used to control the gain and stability of an amplifier. By opening the loop, the diagram illustrates the role of feedback in modifying the effective gain through current and voltage division, as represented by the feedback and admittance blocks. The system aims to stabilize the output by adjusting the input based on the feedback received, thus achieving a desired output response.

Figure 8.61 Conceptual view of opening the loop in voltage-current feedback.

#### Example 8.15

Figure 8.62(a) shows a transimpedance amplifier topology commonly used in optical communication systems. Determine the circuit's gain and input and output impedances if $\lambda=0$.
image_name:Figure 8.62(a)
description:
[
name: A1, type: OpAmp, ports: {InP: GND, InN: GND, OutP: Vout, OutN: GND}
name: RF, type: Resistor, value: RF, ports: {N1: Vout, N2: g1}
name: Iin, type: CurrentSource, ports: {Np: g1, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: g1}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a transimpedance amplifier topology used in optical communication systems. It uses an op-amp with feedback resistor RF and an NMOS transistor M1 to convert input current (Iin) into an output voltage (Vout). The resistor RD is connected to VDD, providing the necessary biasing for the NMOS transistor.
image_name:Figure 8.62(b)
description:
[
name: RF, type: Resistor, value: RF, ports: {N1: Vout, N2: g1}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: g1, OutP: Vout, OutN: GND}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: g1, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: g1, G: Vout}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
]
extrainfo:The circuit is a transimpedance amplifier topology used in optical communication systems. It converts input current to output voltage using a feedback resistor RF and an NMOS transistor M1. The open-loop gain is determined by the feedback network and the transconductance of M1.

Figure 8.62

#### Solution

We can view the feedback resistor, $R_{F}$, as a network that senses the output voltage, converts it to current, and returns the result to the input. Following Figure 8.61, we construct the loaded open-loop amplifier as shown in Fig. 8.62(b), and express the open-loop gain as

$$
\begin{equation*}
R_{0, \text { open }}=-R_{F} g_{m}\left(R_{F} \| R_{D}\right) \tag{8.94}
\end{equation*}
$$

The feedback factor, $y_{21}\left(=I_{2} / V_{1}\right.$ with $\left.V_{2}=0\right)$ is equal to $-1 / R_{F}$. It follows that the closed-loop gain is equal to

$$
\begin{equation*}
\frac{V_{\text {out }}}{I_{\text {in }}}=\frac{-R_{F} g_{m}\left(R_{F} \| R_{D}\right)}{1+g_{m}\left(R_{F} \| R_{D}\right)} \tag{8.95}
\end{equation*}
$$

which, if $g_{m}\left(R_{F} \| R_{D}\right) \gg 1$, reduces to $-R_{F}$, an expected result (why?). The closed-loop input impedance is

$$
\begin{equation*}
R_{i n}=\frac{R_{F}}{1+g_{m}\left(R_{F} \| R_{D}\right)} \tag{8.96}
\end{equation*}
$$

which is approximately equal to $\left(1+R_{F} / R_{D}\right)\left(1 / g_{m}\right)$ if the above condition holds. Similarly, the closed-loop output impedance is given by

$$
\begin{equation*}
R_{\text {out }}=\frac{R_{F} \| R_{D}}{1+g_{m}\left(R_{F} \| R_{D}\right)} \tag{8.97}
\end{equation*}
$$

which amounts to $1 / g_{m}$ if $g_{m}\left(R_{F} \| R_{D}\right) \gg 1$. Note that if $\lambda>0$, we can simply replace $R_{D}$ with $R_{D} \| r_{O}$ in all of the foregoing equations.

This transconductance amplifier is simple enough that we can solve it directly, and the reader is encouraged to do so. But we can readily identify two inconsistencies. First, breaking the loop at the gate of $M_{1}$ yields a loop gain of $g_{m} R_{D}$ rather than $g_{m}\left(R_{D} \| R_{F}\right)$. Second, the closed-loop output impedance [with $I_{i n}$ set to zero in Fig. 8.62(a)] is simply equal to $R_{D} \|\left(1 / g_{m}\right)=R_{D} /\left(1+g_{m} R_{D}\right)$. The value derived above can be expressed as $R_{D} /\left(1+g_{m} R_{D}+R_{D} / R_{F}\right)$, revealing the extra term $R_{D} / R_{F}$. These errors arise from the approximate nature of the model.

#### Example 8.16

Calculate the voltage gain of the circuit shown in Fig. 8.63(a).

#### Solution

What type of feedback is used in this circuit? Resistor $R_{F}$ senses the output voltage and returns a proportional current to node $X$. Thus, the feedback can be considered as the voltage-current type. However, in the general representation of Fig. 8.60(a), the input signal is a current quantity, whereas in this example, it is a voltage quantity. For this reason, we replace $V_{i n}$ and $R_{S}$ by a Norton equivalent [Fig. 8.63(b)] and view $R_{S}$ as the input resistance of the main amplifier. Opening the loop according to Fig. 8.61 and neglecting channel-length modulation, we write the open-loop gain
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: RF, type: Resistor, value: RF, ports: {N1: X, N2: Vout}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: X}
]
extrainfo:The circuit is a feedback amplifier with a voltage input Vin, and the output is taken across RD and RF. The NMOS transistor M1 is used for amplification, and the feedback network consists of resistors RS and RF.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: GND}
name: RF, type: Resistor, value: RF, ports: {N1: Vout, N2: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: GND}
name: IN, type: CurrentSource, value: IN, ports: {Np: GND, Nn: GND}
]
extrainfo:The circuit represents a feedback amplifier with NMOS transistor M1. The input is a current source IN, and the output is taken across RD. The feedback network consists of RS and RF.
image_name:(c)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: RF, type: Resistor, value: RF, ports: {N1: X, N2: Vout}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: X}
name: IN, type: CurrentSource, value: IN, ports: {Np: GND, Nn: X}
name: gI, type: VoltageControlledCurrentSource, value: gI, ports: {Np: X, Nn: GND}
]
extrainfo:The circuit in figure (c) is a feedback amplifier with a voltage-controlled current source (gI) and an NMOS transistor (M1). The feedback network is formed by resistors RF and RD. The input is a voltage source Vin, and the output is taken across Vout. The current source IN is connected to ground and node X.

Figure 8.63
from Fig. 8.63(c) as

$$
\begin{align*}
R_{0, \text { open }} & =\left.\frac{V_{\text {out }}}{I_{N}}\right|_{\text {open }}  \tag{8.98}\\
& =-\left(R_{S} \| R_{F}\right) g_{m}\left(R_{F} \| R_{D}\right) \tag{8.99}
\end{align*}
$$

where $I_{N}=V_{\text {in }} / R_{S}$. We also calculate the loop gain as $y_{21} R_{0, \text { open }}$. Thus, the circuit of Fig. 8.63(a) exhibits a voltage gain of

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=\frac{1}{R_{S}} \cdot \frac{-\left(R_{S} \| R_{F}\right) g_{m}\left(R_{F} \| R_{D}\right)}{1+g_{m}\left(R_{F} \| R_{D}\right) R_{S} /\left(R_{S}+R_{F}\right)} \tag{8.100}
\end{equation*}
$$

Interestingly, if $R_{F}$ is replaced by a capacitor, this analysis does not yield a zero in the transfer function because we have neglected the reverse transmission of the feedback network (from the output of the feedback network to its input). The input and output impedances of the circuit are also interesting to calculate. This is left as an exercise for the reader. The reader is also encouraged to apply this solution to the circuit of Fig. 8.3(b).

### 8.5.5 Loading in Current-Current Feedback

The forward amplifier in this case generates an output current in response to the input current and can be represented by an H model, and so can the feedback network. Shown in Fig. 8.64 is the equivalent circuit with the $H_{12}$ and $h_{12}$ generators neglected. We write

$$
\begin{align*}
I_{\text {in }} & =I_{e} H_{11} h_{22}+h_{21} I_{\text {out }}+I_{e}  \tag{8.101}\\
I_{\text {out }} & =-I_{\text {out }} h_{11} H_{22}+H_{21} I_{e} \tag{8.102}
\end{align*}
$$

image_name:Figure 8.64 Equivalent circuit for current-current feedback.
description:
[
name: Iin, type: CurrentSource, value: Iin, ports: {Np: X1, Nn: X2}
name: H11, type: Resistor, value: H11, ports: {N1: X1, N2: X3}
name: H22, type: Resistor, value: H22, ports: {N1: X4, N2: X5}
name: h22, type: Resistor, value: h22, ports: {N1: X1, N2: X6}
name: h11, type: Resistor, value: h11, ports: {N1: X7, N2: X1}
name: H21, type: VoltageControlledVoltageSource, value: H21, ports: {Np: X3, Nn: X5}
name: h21, type: CurrentControlledCurrentSource, value: h21, ports: {Np: X6, Nn: X7}
]
extrainfo:The circuit represents a current-current feedback system using an H model. The input current Iin is fed into the system, and the output current Iout is generated. The feedback network and the forward amplifier are described with resistors and controlled sources, implementing the feedback equations provided in the context.

Figure 8.64 Equivalent circuit for current-current feedback.
and hence

$$
\begin{equation*}
\frac{I_{\text {out }}}{I_{\text {in }}}=\frac{\frac{H_{21}}{\left(1+h_{22} H_{11}\right)\left(1+h_{11} H_{22}\right)}}{1+h_{21} \frac{H_{21}}{\left(1+h_{22} H_{11}\right)\left(1+h_{11} H_{22}\right)}} \tag{8.103}
\end{equation*}
$$

As in previous topologies, we define the equivalent open-loop current gain and the feedback factor as

$$
\begin{align*}
A_{I, \text { open }} & =\frac{H_{21}}{\left(1+h_{22} H_{11}\right)\left(1+h_{11} H_{22}\right)}  \tag{8.104}\\
\beta & =h_{21} \tag{8.105}
\end{align*}
$$

The conceptual view of the broken loop is depicted in Fig. 8.65, and the loop gain is equal to $h_{21} A_{I, \text { open }}$.
image_name:Figure 8.65
description:The block diagram in Figure 8.65 illustrates a conceptual view of a current-current feedback system. The main components of this system include:

1. **Current Source ($I_{in}$):** This is the input current source that initiates the signal flow into the system.

2. **Summing Junction (+/-):** The input current and a feedback current are combined at this point. The summing junction calculates the difference between the input current and the feedback current.

3. **Amplifier ($A_I$):** This block represents the open-loop current gain of the system. It amplifies the difference current from the summing junction to produce an output current ($I_{out}$).

4. **Feedback Network:**
- **Feedback Factor ($\beta$):** There are two blocks labeled with $\beta$, representing the feedback factor. These blocks are part of the feedback loop that returns a portion of the output current back to the input.
- **Impedances ($h_{22}^{-1}$ and $h_{11}$):** These are elements of the feedback loop. $h_{22}^{-1}$ is connected in series with the feedback path, while $h_{11}$ is connected in parallel, influencing the feedback current.

5. **Feedback Path:** The output current ($I_{out}$) is fed back to the input through the feedback network. The feedback current is modified by the feedback factor and the impedances in the network.

**Flow of Information:**
- The input current ($I_{in}$) enters the summing junction, where it is combined with the feedback current. The resulting current is then amplified by the open-loop amplifier ($A_I$) to produce the output current ($I_{out}$).
- The output current is fed back to the input through the feedback network, which adjusts the feedback current based on the feedback factor ($\beta$) and the impedances ($h_{22}^{-1}$ and $h_{11}$).

**Overall System Function:**
- The primary function of this system is to regulate the output current ($I_{out}$) by using a current-current feedback mechanism. The feedback loop aims to stabilize the system and maintain a desired output current by adjusting the feedback current based on changes in the output.

Figure 8.65 Conceptual view of loading in current-current feedback.

#### Example 8.17

Calculate the open-loop and closed-loop gains of the circuit shown in Fig. 8.66(a). Assume that $\lambda=\gamma=0$.
image_name:(a)
description:
[
name: Iin, type: CurrentSource, ports: {Np: Vin, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: X, G: Vin}
name: M2, type: NMOS, ports: {S: X, D: Vout, G: X}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: RF, type: Resistor, value: RF, ports: {N1: Vin, N2: Y}
name: RS, type: Resistor, value: RS, ports: {N1: Y, N2: GND}
]
extrainfo:The circuit implements a current-current feedback mechanism to stabilize and regulate the output current (Iout). The feedback loop involves sensing the output current through resistors RF and RS, and feeding back a portion to the input via M1.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: G1}
name: M2, type: NMOS, ports: {S: X, D: Iout, G: G1}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: RF, type: Resistor, value: RF, ports: {N1: G1, N2: Z}
name: RS, type: Resistor, value: RS, ports: {N1: Z, N2: Y}
name: Iin, type: CurrentSource, ports: {Np: G1, Nn: GND}
]
extrainfo:The circuit diagram (b) shows a current-current feedback circuit with NMOS transistors M1 and M2. The resistors RF and RS are used for feedback and sensing. The current source Iin provides input current to the circuit. The output current is labeled as Iout.

Figure 8.66

#### Solution

In this circuit, $R_{S}$ and $R_{F}$ sense the output current and return a fraction thereof to the input. Breaking the loop according to Fig. 8.65, we arrive at the circuit in Fig. 8.66(b), where we have

$$
\begin{equation*}
A_{I, \text { open }}=-\left(R_{F}+R_{S}\right) g_{m 1} R_{D} \frac{1}{R_{S} \| R_{F}+1 / g_{m 2}} \tag{8.106}
\end{equation*}
$$

The loop gain is given by $h_{21} A_{I, \text { open }}$, where, from (8.62), $h_{21}=I_{2} / I_{1}$ with $V_{2}=0$. For the feedback network consisting of $R_{S}$ and $R_{F}$, we have $h_{21}=-R_{S} /\left(R_{S}+R_{F}\right)$. The closed-loop gain equals $A_{I, \text { open }} /\left(1+h_{21} A_{I, \text { open }}\right)$.

### 8.5.6 Summary of Loading Effects

The results of our study of loading are summarized in Fig. 8.67. The analysis is carried out in three steps: (1) open the loop with proper loading and calculate the open-loop gain, $A_{O L}$, and the open-loop input and output impedances; (2) determine the feedback ratio, $\beta$, and hence the loop gain, $\beta A_{O L}$; and (3) calculate the closed-loop gain and input and output impedances by scaling the open-loop values by a factor of $1+\beta A_{O L}$. Note that in the equations defining $\beta$, the subscripts 1 and 2 refer to the input and output ports of the feedback network, respectively.

In this chapter, we have described two methods of obtaining the loop gain: (1) by breaking the loop at an arbitrary point, as shown in Fig. 8.5, and (2) by calculating $A_{O L}$ and $\beta$, as illustrated in Fig. 8.67. The two methods may yield slightly different results due to the issues outlined in Table 8.1.
image_name:(a)
description:The diagram labeled "(a)" illustrates a negative feedback amplifier system. The primary components include:

1. **Input Source**: The input voltage, denoted as \( V_{in} \), enters the system.

2. **Summing Junction**: The input signal \( V_{in} \) is applied to a summing junction. This junction subtracts the feedback signal from \( \beta \) and outputs the error signal \( X_1 \).

3. **Amplifier**: The error signal \( X_1 \) is fed into an amplifier with a gain of \( A_0 \). The amplifier increases the magnitude of the error signal and produces an output voltage \( V_{out} \).

4. **Feedback Network**: The output voltage \( V_{out} \) is sent through a feedback network characterized by a feedback factor \( \beta \). This network scales the output and feeds a portion back to the summing junction.

5. **Feedback Factor**: The feedback factor \( \beta \) is defined as the ratio \( \beta = \frac{V_2}{V_1} \) under the condition that the output loop current \( I_2 = 0 \), indicating that the feedback network is voltage-based.

**Flow of Information**:
- The input voltage \( V_{in} \) is adjusted by the summing junction based on the feedback signal, resulting in the error signal \( X_1 \).
- The error signal is amplified by the amplifier \( A_0 \), producing the output \( V_{out} \).
- The output is partially fed back through the feedback network to the summing junction, completing the loop.

**Overall System Function**:
The primary function of this system is to maintain a stable output \( V_{out} \) by adjusting the input based on the feedback signal. The feedback mechanism ensures that the output is controlled and stabilized by continuously comparing it with the input and adjusting accordingly. This negative feedback configuration enhances the system's stability and accuracy.
image_name:(b)
description:The diagram labeled as (b) illustrates a feedback system involving a transconductance amplifier, denoted as \( G_m \). Here's a detailed breakdown of its components and operation:

1. **Main Components:**
- **Summing Junction:** Located at the input, it combines the input voltage \( V_{in} \) with feedback signals. It has a positive and negative input, indicating differential input processing.
- **Transconductance Amplifier (\( G_m \)):** Converts the input voltage difference into an output current \( I_{out} \). This amplifier is the central element of the system, providing the gain required for the operation.
- **Feedback Network (\( \beta \)):** Connected from the output back to the summing junction. It senses the output current and feeds back a portion of it to the input.

2. **Flow of Information or Control:**
- **Input Signal (\( V_{in} \)):** Enters the system at the summing junction.
- **Feedback Loop:** The feedback network picks up a portion of the output current \( I_{out} \) and sends it back to the summing junction. This feedback is negative, as indicated by the subtraction at the summing junction.
- **Output Signal (\( I_{out} \)):** The transconductance amplifier outputs a current based on the input voltage difference.

3. **Labels, Annotations, and Key Indicators:**
- **\( \beta = \frac{V_2}{I_1} \bigg|_{I_2=0} \):** This equation defines the feedback factor \( \beta \), indicating the ratio of the feedback voltage \( V_2 \) to the input current \( I_1 \), with the condition that output current \( I_2 \) is zero.
- The system is grounded at multiple points, indicating a common reference potential.

4. **Overall System Function:**
- The primary function of this system is to regulate the output current \( I_{out} \) in response to the input voltage \( V_{in} \), using a feedback mechanism to stabilize the operation. The feedback network ensures that the output remains proportional to the input, as defined by the transconductance \( G_m \) and the feedback factor \( \beta \). This setup is typical in applications requiring precise control of current output based on voltage inputs, such as in analog signal processing or control systems.
image_name:(c)
description:The block diagram labeled "(c)" represents a feedback system featuring a transresistance amplifier configuration. Here is a detailed breakdown:

1. **Main Components:**
- **Current Source (I_in):** The input to the system is a current source, denoted as \(I_{in}\).
- **Summing Junction:** The input current \(I_{in}\) is fed into a summing junction, which combines the input signal with feedback from the system.
- **Transresistance Amplifier (R_0):** This block converts the input current to an output voltage. It is represented by \(R_0\) and is the main amplification component of the system.
- **Feedback Network (β):** The feedback network is connected from the output of the amplifier back to the summing junction, providing a portion of the output signal back to the input to control the system behavior.

2. **Flow of Information or Control:**
- The input current \(I_{in}\) enters the system at the summing junction.
- The summing junction outputs a signal that is the difference between \(I_{in}\) and the feedback current.
- This signal is then amplified by the transresistance amplifier \(R_0\), producing an output voltage \(V_{out}\).
- A portion of \(V_{out}\) is fed back through the feedback network \(β\) to the summing junction, completing the feedback loop.

3. **Labels, Annotations, and Key Indicators:**
- The feedback factor \(β\) is defined as \(\beta = \frac{I_2}{V_1}\) with the condition \(V_2 = 0\), indicating how the feedback network is characterized in terms of output current to input voltage.

4. **Overall System Function:**
- The primary function of this system is to convert an input current \(I_{in}\) to an output voltage \(V_{out}\) with transresistance amplification, while the feedback network stabilizes and controls the gain and bandwidth of the system. The feedback mechanism ensures that the system can maintain stability and desired performance characteristics by adjusting the input signal based on the output.
image_name:(d)
description:The system block diagram labeled "(d)" illustrates a feedback circuit with a current amplifier configuration. Here's a detailed description:

1. **Main Components:**
- **Current Source (I_in):** The input to the system is a current source labeled \( I_{in} \).
- **Summing Junction:** This is where the input current \( I_{in} \) is combined with the feedback current. It has two inputs, one positive and one negative, indicating the subtraction of the feedback current from the input current.
- **Current Amplifier (A_I):** This block amplifies the input current. The output of this amplifier is denoted as \( I_{out} \).
- **Feedback Network (β):** This block samples the output current \( I_{out} \) and feeds a portion of it back to the summing junction. The feedback factor is defined as \( \beta = \frac{I_2}{I_1} \) with \( V_2 = 0 \), indicating that the feedback is based on current and not voltage.

2. **Flow of Information or Control:**
- The input current \( I_{in} \) enters the summing junction, where it is combined with the feedback current.
- The resulting current is then fed into the current amplifier \( A_I \), which produces an output current \( I_{out} \).
- A portion of \( I_{out} \) is fed back through the feedback network (β) to the summing junction to be subtracted from the input current, forming a feedback loop.

3. **Labels, Annotations, and Key Indicators:**
- The feedback factor \( \beta \) is defined as \( \beta = \frac{I_2}{I_1} \) with the condition \( V_2 = 0 \), emphasizing that the feedback is purely current-based.

4. **Overall System Function:**
- This system functions as a current feedback amplifier. The purpose of the feedback loop is to stabilize the gain and improve the performance of the amplifier by continuously adjusting the input current based on the output current. The feedback mechanism ensures that the output current is proportional to the input current, controlled by the feedback factor \( \beta \). This type of configuration is typically used in applications requiring precise current amplification with feedback control.

Figure 8.67 Summary of loading effects.

## 8.6 ■ Bode's Analysis of Feedback Circuits

Bode's approach provides a rigorous solution for a circuit's closed-loop parameters (whether it includes feedback or not), but it does not tell us much about the loop gain in the presence of multiple feedback mechanisms. The analysis presented in this section was originally described by Bode in his 1945 classic textbook Network Analysis and Feedback Network Design. Since this approach is somewhat less intuitive, we encourage the reader to be patient and read this section in several sittings.

### 8.6.1 Observations

Before delving into Bode's analysis, we should make two simple, yet new observations with regard to circuit equations.

First, consider the general circuit shown in Fig. 8.68(a), where one transistor is explicitly shown in its ideal form. We know from our small-signal gain and transfer function analyses in previous chapters that $V_{\text {out }}$ can eventually be expressed as $A_{v} V_{\text {in }}$ or $H(s) V_{\text {in }}$. But, what happens if we denote the dependent current source by $I_{1}$ and do not make the substitution $I_{1}=g_{m} V_{1}$ yet? Then, $V_{\text {out }}$ is obtained as a function
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: X1, Nn: GND}
name: gmV1, type: VoltageControlledCurrentSource, ports: {Np: Vout, Nn: X1}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X1}
name: I1, type: VoltageControlledCurrentSource, ports: {Np: X1, Nn: Vout}
name: ro, type: Resistor, value: ro, ports: {N1: Vout, N2: X1}
name: RD, type: Resistor, value: RD, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit contains a dependent current source 'gmV1' controlled by voltage 'V1'. The output voltage 'Vout' is influenced by both the input voltage 'Vin' and the current source 'I1'. The resistors 'RS', 'ro', and 'RD' provide biasing and load to the circuit.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: X1, Nn: GND}
name: gmV1, type: VoltageControlledCurrentSource, value: gmV1, ports: {Np: X1, Nn: Vout}
name: RS, type: Resistor, value: RS, ports: {N1: X1, N2: GND}
name: RD, type: Resistor, value: RD, ports: {N1: Vout, N2: X1}
name: r0, type: Resistor, value: r0, ports: {N1: Vout, N2: X1}
]
extrainfo:The circuit is a degenerated common-source amplifier with a dependent current source gmV1, resistors RS and RD, and an additional resistor r0. The output voltage Vout is influenced by the input voltage Vin and the current source.
image_name:(c)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
name: gmV1, type: VoltageControlledCurrentSource, value: gmV1, ports: {Np: V1, Nn: GND}
]
extrainfo:The circuit diagram (c) contains a voltage source Vin, a voltage source V1, and a voltage-controlled current source gmV1. The circuit is simplified and encapsulated in a box, indicating a modular or abstract representation of the circuit.

Figure 8.68 (a) Circuit containing a dependent source, (b) circuit example, and (c) $V_{1}$ as a signal of interest.
of both $V_{\text {in }}$ and $I_{1}$ :

$$
\begin{equation*}
V_{\text {out }}=A V_{\text {in }}+B I_{1} \tag{8.107}
\end{equation*}
$$

As an example, in the degenerated common-source stage of Fig. 8.68(b), we note that the current flowing upward through $R_{D}$ (and downward through $R_{S}$ ) is equal to $-V_{\text {out }} / R_{D}$, and hence the voltage drop across $r_{O}$ is given by $\left(-V_{\text {out }} / R_{D}-I_{1}\right) r_{O}$. A KVL around the output network thus yields

$$
\begin{equation*}
V_{\text {out }}=\left(-\frac{V_{\text {out }}}{R_{D}}-I_{1}\right) r_{O}-\frac{V_{\text {out }}}{R_{D}} R_{S} \tag{8.108}
\end{equation*}
$$

and

$$
\begin{equation*}
V_{\text {out }}=\frac{-r_{O}}{1+\frac{r_{O}+R_{S}}{R_{D}}} I_{1} \tag{8.109}
\end{equation*}
$$

In this case, $A=0$ and $B=-r_{O} R_{D} /\left(R_{D}+r_{O}+R_{S}\right)$.
Second, let us return to the general circuit in Fig. 8.68(a) and consider $V_{1}$ as the signal of interest, i.e., we wish to compute $V_{1}$ as a function of $V_{i n}$ in the form of $A_{v} V_{i n}$ or $H(s) V_{i n}$. This is always possible by pretending that $V_{1}$ is the "output," as conceptually illustrated in Fig. 8.68(c). In a manner similar to Eq. (8.107), $V_{1}$ can be written as

$$
\begin{equation*}
V_{1}=C V_{i n}+D I_{1} \tag{8.110}
\end{equation*}
$$

if we temporarily forget that $I_{1}=g_{m} V_{1}$. In Fig. 8.68(b), for example, we express the current though $R_{S}$ (and $\left.R_{D}\right)$ as $\left(V_{i n}-V_{1}\right) R_{S}$, subtract this current from $I_{1}$, and let the result flow through $r_{O}$. A KVL around the output network gives

$$
\begin{equation*}
V_{i n}-V_{1}-\left(I_{1}-\frac{V_{i n}-V_{1}}{R_{S}}\right) r_{O}=-\frac{V_{i n}-V_{1}}{R_{S}} R_{D} \tag{8.111}
\end{equation*}
$$

and hence

$$
\begin{equation*}
V_{1}=V_{i n}-\frac{r_{O} R_{S}}{R_{D}+r_{O}+R_{S}} I_{1} \tag{8.112}
\end{equation*}
$$

That is, $C=1$ and $D=-r_{O} R_{S} /\left(R_{D}+r_{O}+R_{S}\right)$.

In summary, in a given circuit containing at least one transistor (whether there is feedback or not), we can eventually reach two equations that express $V_{\text {out }}$ and $V_{1}$ in terms of $V_{\text {in }}$ and $I_{1}$. To obtain $V_{\text {out }} / V_{\text {in }}$, we solve the two equations while applying the knowledge that $I_{1}$ is in fact equal to $g_{m} V_{1}$.

The foregoing developments and, in particular, Eqs. (8.107) and (8.110) appear unnecessarily tedious. After all, we can directly solve the circuit in Fig. 8.68(b) with less algebra. However, the interpretation of the coefficients $A, B, C$, and $D$ affords a simple and elegant approach to feedback analysis.

### 8.6.2 Interpretation of Coefficients

We now focus on Eqs. (8.107) and (8.110) and ask whether the $A-D$ coefficients can be directly calculated for a given circuit. We begin with $A$ :

$$
\begin{equation*}
A=\frac{V_{\text {out }}}{V_{\text {in }}} \text { with } I_{1}=0 \tag{8.113}
\end{equation*}
$$

This result implies that $A$ is obtained as the voltage gain of the circuit if the dependent current source is set to zero, which can be readily accomplished by "disabling" the transistor, i.e., by forcing the transistor's $g_{m}$ to zero. We can consider $V_{\text {out }}$ in this case as the "feedthrough" of the input signal (in the absence of the ideal transistor) [Fig. 8.69(a)]. In the CS example, $V_{\text {out }}=0$ if $I_{1}=0$ because no current flows through $R_{S}, r_{O}$, and $R_{D}$. That is, $A=0$.
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: Vout, Nn: X1}
name: I1, type: CurrentSource, value: I1, ports: {Np: X1, Nn: Vout}
name: RS, type: Resistor, value: RS, ports: {N1: X1, N2: GND}
name: rO, type: Resistor, value: rO, ports: {N1: X1, N2: Vout}
name: RD, type: Resistor, value: RD, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit diagram (a) represents a basic setup for calculating the voltage gain A by setting the dependent current source to zero, effectively disabling the transistor. The output voltage Vout is the result of the input signal feedthrough in the absence of the transistor.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: Vout, Nn: X1}
name: I1, type: CurrentSource, value: I1, ports: {Np: X1, Nn: Vout}
name: RS, type: Resistor, value: RS, ports: {N1: X1, N2: GND}
name: r_o, type: Resistor, value: r_o, ports: {N1: X1, N2: Vout}
name: RD, type: Resistor, value: RD, ports: {N1: Vout, N2: GND}
]
extrainfo:This circuit diagram (b) represents a setup for calculating the B coefficient, where the input voltage is set to zero. The current source I1 is considered as an independent source to determine the output voltage Vout.
image_name:(c)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: X1, Nn: X2}
name: I1, type: CurrentSource, value: I1, ports: {Np: X1, Nn: X2}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X2}
name: ro, type: Resistor, value: ro, ports: {N1: X1, N2: X3}
name: RD, type: Resistor, value: RD, ports: {N1: X3, N2: Vout}
]
extrainfo:The circuit setup in diagram (c) is used to calculate the coefficient C, where Vout is determined with Vin set to zero. This involves analyzing the effect of the current source I1 in the presence of resistors RS, ro, and RD.
image_name:(d)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: X1, Nn: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: X1, Nn: X2}
name: RS, type: Resistor, value: RS, ports: {N1: X2, N2: GND}
name: ro, type: Resistor, value: ro, ports: {N1: X1, N2: Vout}
name: RD, type: Resistor, value: RD, ports: {N1: Vout, N2: GND}
]
extrainfo:This circuit is used to analyze the coefficient D, where the output voltage Vout is influenced by the current source I1 and the resistors ro and RD, with the input voltage Vin set to zero.

Figure 8.69 Setups for the calculation of (a) $A$, (b) $B$, (c) $C$, and (d) $D$.

As for the $B$ coefficient in (8.107), we have

$$
\begin{equation*}
B=\frac{V_{\text {out }}}{I_{1}} \text { with } V_{\text {in }}=0 \tag{8.114}
\end{equation*}
$$

That is, we set the input to zero and compute $V_{\text {out }}$ as a result of $I_{1}$ [Fig. 8.69(b)], pretending that $I_{1}$ is an independent source. ${ }^{14}$ In the CS example,

$$
\begin{equation*}
\left(-\frac{V_{\text {out }}}{R_{D}}-I_{1}\right) r_{O}-\frac{V_{\text {out }}}{R_{D}} R_{S}=V_{\text {out }} \tag{8.115}
\end{equation*}
$$

[^56]and hence
\$\$

$$
\begin{equation*}
V_{\text {out }}=\frac{-r_{O} R_{D}}{R_{D}+r_{O}+R_{S}} I_{1} \tag{8.116}
\end{equation*}
$$

\$\$

Thus, $B=-r_{O} R_{D} /\left(R_{D}+r_{O}+R_{S}\right)$.
The $C$ coefficient in (8.110) is interpreted as

$$
\begin{equation*}
C=\frac{V_{1}}{V_{i n}} \text { with } I_{1}=0 \tag{8.117}
\end{equation*}
$$

i.e., the transfer function from the input to $V_{1}$ with the transistor's $g_{m}$ set to zero [Fig. 8.69(c)]. In the CS circuit, no current flows through $R_{S}$ under this condition, yielding $V_{1}=V_{i n}$ and $C=1$.

Finally, the $D$ coefficient is obtained as

$$
\begin{equation*}
D=\frac{V_{1}}{I_{1}} \text { with } V_{i n}=0 \tag{8.118}
\end{equation*}
$$

which, as illustrated in Fig. 8.69(d), represents the transfer function from $I_{1}$ to $V_{1}$ with the input at zero. In the CS stage, the current flowing through $R_{S}$ (and $R_{D}$ ) under this condition is equal to $-V_{1} / R_{S}$, producing a voltage drop of $\left(-V_{1} / R_{S}-I_{1}\right) r_{O}$ across $r_{O}$. A KVL around the output network yields

$$
\begin{equation*}
-V_{1}-\left(\frac{V_{1}}{R_{S}}+I_{1}\right) r_{O}=\frac{V_{1}}{R_{S}} R_{D} \tag{8.119}
\end{equation*}
$$

We therefore have

$$
\begin{equation*}
V_{1}=-\frac{r_{O} R_{S}}{R_{D}+r_{O}+R_{S}} I_{1} \tag{8.120}
\end{equation*}
$$

and hence $D=-r_{O} R_{S} /\left(R_{D}+r_{O}+R_{S}\right)$.
In summary, the $A-D$ coefficients are computed as shown in Fig. 8.70: (1) we disable the transistor by setting its $g_{m}$ to zero and obtain $A$ and $C$ as the feedthroughs from $V_{i n}$ to $V_{\text {out }}$ and to $V_{1}$, respectively, and (2) we set the input to zero and calculate $B$ and $D$ as the gain from $I_{1}$ to $V_{\text {out }}$ and to $V_{1}$, respectively. From another perspective, the former step finds the responses to $V_{i n}$ with $g_{m}=0$, and the latter, to $I_{1}$ with $V_{i n}=0$. We can even say that the circuit is excited each time by one input, either $V_{i n}$ or $I_{1}$, and generates two outputs of interest, $V_{\text {out }}$ and $V_{1}$. The reader may still not see the reason for these derivations, but patience is a virtue!
image_name:(a)
description:
[
name: V_in, type: VoltageSource, value: V_in, ports: {Np: Vin, Nn: GND}
name: I_1, type: CurrentSource, value: I_1, ports: {Np: V1, Nn: Vout}
]
extrainfo:The circuit diagram (a) shows a voltage source V_in and a current source I_1. The gain from V_in to V_out is labeled as A = V_out/V_in, and the gain from V_in to V1 is labeled as C = V1/V_in.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: V1, Nn: Vout}
]
extrainfo:The circuit diagram (b) shows the computation of coefficients B and D, where B = Vout/I1 and D = V1/I1. The input voltage source Vin is set to zero, and the current source I1 is active. The circuit generates two outputs of interest, Vout and V1, in response to the input current I1.

Figure 8.70 Summary of computations for $A-D$.

#### Example 8.18

Compute the $A-D$ coefficients for the circuit shown in Fig. 8.71(a).
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: g1}
name: RF, type: Resistor, value: RF, ports: {N1: g1, N2: Vout}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: g1}
name: V1, type: VoltageSource, value: V1, ports: {Np: g1, Nn: GND}
]
extrainfo:The circuit computes coefficients A and C. A = Vout/Vin and C = V1/Vin with Vin as the input voltage source and I1 set to zero. The NMOS transistor M1 is used to control the output voltage Vout.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: x1}
name: RF, type: Resistor, value: RF, ports: {N1: x1, N2: Vout}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: V1, type: VoltageSource, value: V1, ports: {Np: x1, Nn: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit diagram (b) computes coefficients B and D, where B = Vout/I1 and D = V1/I1. Vin is set to zero, and the current source I1 is active. The outputs of interest are Vout and V1 in response to I1.
image_name:(c)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X1}
name: RF, type: Resistor, value: RF, ports: {N1: X1, N2: Vout}
name: RD, type: Resistor, value: RD, ports: {N1: Vout, N2: VDD}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: X1}
name: I1, type: CurrentSource, value: I1, ports: {Np: V1, Nn: GND}
]
extrainfo:The circuit diagram (c) shows the computation of coefficients B and D, where B = Vout/I1 and D = V1/I1. The input voltage source Vin is set to zero, and the current source I1 is active. The circuit generates two outputs of interest, Vout and V1, in response to the input current I1.

Figure 8.71

#### Solution

Following the procedures illustrated in Fig. 8.70, we first set $I_{1}$ (i.e., $g_{m}$ ) to zero and determine the feedthrough components $V_{\text {out }} / V_{\text {in }}$ and $V_{1} / V_{\text {in }}$. From Fig. 8.71(b), we have

$$
\begin{align*}
A & =\frac{V_{\text {out }}}{V_{\text {in }}}  \tag{8.121}\\
& =\frac{R_{D}}{R_{D}+R_{S}+R_{F}} \tag{8.122}
\end{align*}
$$

and

$$
\begin{align*}
C & =\frac{V_{1}}{V_{i n}}  \tag{8.123}\\
& =\frac{R_{F}+R_{D}}{R_{D}+R_{S}+R_{F}} \tag{8.124}
\end{align*}
$$

Next, we set $V_{\text {in }}$ to zero and calculate the transfer functions from $I_{1}$ to $V_{\text {out }}$ and to $V_{1}$ [Fig. 8.71(c)]:

$$
\begin{align*}
B & =\frac{V_{\text {out }}}{I_{1}}  \tag{8.125}\\
& =-R_{D} \|\left(R_{S}+R_{F}\right)  \tag{8.126}\\
& =-\frac{R_{D}\left(R_{S}+R_{F}\right)}{R_{D}+R_{S}+R_{F}} \tag{8.127}
\end{align*}
$$

and

$$
\begin{align*}
D & =\frac{V_{1}}{I_{1}}  \tag{8.128}\\
& =\frac{R_{S}}{R_{S}+R_{F}} \frac{V_{\text {out }}}{I_{1}}  \tag{8.129}\\
& =-\frac{R_{S} R_{D}}{R_{D}+R_{S}+R_{F}} \tag{8.130}
\end{align*}
$$

For our subsequent studies, we must refresh our memory about loop gain calculations.

Example 8.19
Determine the exact loop gain for the circuit of Fig. 8.71(a).

#### Solution

We prefer to break the loop at a port that does not entail loading effects. Let us do so at the gate of $M_{1}$, as depicted in Fig. 8.72(a). Applying a test voltage, $V_{t}$, and calculating the feedback voltage, $V_{F}$, we have

$$
\begin{align*}
\text { Loop Gain } & =-\frac{V_{F}}{V_{t}}  \tag{8.131}\\
& =g_{m}\left[R_{D} \|\left(R_{S}+R_{F}\right)\right] \frac{R_{S}}{R_{S}+R_{F}}  \tag{8.132}\\
& =\frac{g_{m} R_{S} R_{D}}{R_{D}+R_{S}+R_{F}} \tag{8.133}
\end{align*}
$$

Note that the loop gain and the $D$ coefficient in (8.130) differ by only a factor of $-g_{m}$. We return to this point below.
image_name:(a)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: VF}
name: RF, type: Resistor, value: RF, ports: {N1: VF, N2: Vout}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: Vt, Nn: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: Vout, Nn: GND}
name: gm V1, type: VoltageControlledCurrentSource, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit includes a voltage-controlled current source representing a transconductance amplifier with gain gm. The loop gain is calculated using the resistors RS, RF, and RD.

(a)
image_name:Figure 8.72(b)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: VF}
name: RF, type: Resistor, value: RF, ports: {N1: VF, N2: X}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: It, type: CurrentSource, value: It, ports: {Np: X, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is used to measure the loop gain by injecting a test current It at node X and measuring the feedback voltage VF. The loop gain is calculated using the resistors RS, RF, and RD. The voltage-controlled current source represents a transconductance amplifier with gain gm.

(b)

Figure 8.72
Alternatively, we can break the loop at the top terminal of the dependent current source. Illustrated in Fig. 8.72(b), the idea is to draw a test current, $I_{t}$, from node $X$ and measure the resulting feedback voltage, $V_{F}$, recognizing that the ratio $-V_{F} / I_{t}$ must be multiplied by $g_{m}$ to arrive at the loop gain:

$$
\begin{equation*}
V_{F}=-I_{t}\left[R_{D} \|\left(R_{S}+R_{F}\right)\right] \frac{R_{S}}{R_{S}+R_{F}} \tag{8.134}
\end{equation*}
$$

and thus

$$
\begin{align*}
\text { Loop Gain } & =-\frac{g_{m} V_{F}}{I_{t}}  \tag{8.135}\\
& =\frac{g_{m} R_{S} R_{D}}{R_{D}+R_{S}+R_{F}} \tag{8.136}
\end{align*}
$$

We see a similarity between the calculation of $D$ in Fig. 8.69(d) and the calculation of the loop gain in Fig. 8.72(b). In both cases, we set the input to zero, apply $I_{1}$ or $I_{t}$, and measure the controlling voltage, $V_{1}$. We therefore surmise that $D$ and the loop gain may be related. We will keep the reader in suspense for now.

### 8.6.3 Bode's Analysis

We have seen in the previous section that the $A-D$ coefficients can be computed relatively easily. We now express $V_{\text {out }} / V_{\text {in }}$ in terms of these coefficients. Since

$$
\begin{align*}
V_{\text {out }} & =A V_{\text {in }}+B I_{1}  \tag{8.137}\\
V_{1} & =C V_{\text {in }}+D I_{1} \tag{8.138}
\end{align*}
$$

and, in the actual circuit, $I_{1}=g_{m} V_{1}$, we have

$$
\begin{equation*}
V_{1}=\frac{C}{1-g_{m} D} V_{i n} \tag{8.139}
\end{equation*}
$$

The closed-loop gain is therefore equal to

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=A+\frac{g_{m} B C}{1-g_{m} D} \tag{8.140}
\end{equation*}
$$

As expected, the first term represents the input-output feedthrough, manifesting itself when $g_{m}=0$. We can also write

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=\frac{A+g_{m}(B C-A D)}{1-g_{m} D} \tag{8.141}
\end{equation*}
$$

In contrast to direct analysis of the closed-loop circuit, Bode's method decomposes the computation into several simpler steps. While our formulation has assumed a dependent current source, the results are applicable to dependent voltage sources as well. Let us solve some circuits using Bode's approach.

#### Example 8.20

Determine the voltage gain of the degenerated CS stage shown in Fig. 8.69.

#### Solution

Utilizing the results obtained for Fig. 8.69 and noting that $A=0$ and $C=1$, we have

$$
\begin{align*}
\frac{V_{\text {out }}}{V_{\text {in }}} & =\frac{g_{m} \frac{-r_{O} R_{D}}{R_{D}+r_{O}+R_{S}}}{1+g_{m} \frac{r_{O} R_{S}}{R_{D}+r_{O}+R_{S}}}  \tag{8.142}\\
& =\frac{-g_{m} r_{O} R_{D}}{R_{D}+r_{O}+\left(1+g_{m} r_{O}\right) R_{S}} \tag{8.143}
\end{align*}
$$

The reader is encouraged to repeat this analysis in the presence of body effect.

#### Example 8.21

Determine the voltage gain of the feedback amplifier shown in Fig. 8.71(a) without breaking the loop.

#### Solution

With the aid of the results obtained in Example 8.18, we obtain

$$
\begin{align*}
\frac{V_{\text {out }}}{V_{\text {in }}} & =\frac{R_{D}}{R_{D}+R_{S}+R_{F}}+\frac{-g_{m} \frac{R_{D}\left(R_{S}+R_{F}\right)\left(R_{F}+R_{D}\right)}{\left(R_{D}+R_{S}+R_{F}\right)^{2}}}{1+\frac{g_{m} R_{S} R_{D}}{R_{D}+R_{S}+R_{F}}}  \tag{8.144}\\
& =\frac{R_{D}}{R_{D}+R_{S}+R_{F}}+\frac{-g_{m} R_{D}\left(R_{S}+R_{F}\right)\left(R_{F}+R_{D}\right)}{\left(R_{D}+R_{S}+R_{F}+g_{m} R_{S} R_{D}\right)\left(R_{D}+R_{S}+R_{F}\right)} \tag{8.145}
\end{align*}
$$

Note that this result is exact, with the first term representing the circuit's direct feedthrough in the absence of transistor action $\left(g_{m}=0\right)$.

Under what condition does the above loop gain reduce to the familiar, ideal form $-R_{F} / R_{S}$ ? We may surmise that $R_{D}$ must be small enough not to "feel" the loading effect of $R_{F}$. But the condition $R_{D} \ll R_{F}$ does not yield a voltage gain of $-R_{F} / R_{S}$. After all, this ideal value also presumes a high open-loop gain. Thus, we need two conditions, namely, $R_{D} \ll R_{F}$ and $g_{m} R_{D} \gg 1$ for the above result to reduce to $-R_{F} / R_{S}$.

Let us make a useful observation. If $A=0$, Eq. (8.140) yields $V_{\text {out }} / V_{\text {in }}=g_{m} B C /\left(1-g_{m} D\right)$, a result resembling the generic feedback equation $A_{0} /\left(1+\beta A_{0}\right)$. We therefore loosely call $g_{m} B C$ the "open-loop" gain.

Return Ratio and Loop Gain As mentioned in Example 8.19, the quantity $D\left(=V_{1} / I_{1}\right.$ with $\left.V_{\text {in }}=0\right)$ and the loop gain appear to be related. In fact, the closed-loop gain expression in Eq. (8.141) may suggest that $1-g_{m} D=1+$ loop gain, and hence loop gain $=-g_{m} D$. This is not a coincidence: in both cases, we set the main input to zero, break the loop by replacing the dependent source with an independent source, and compute the returned quantity.

In his original treatment of feedback, Bode introduces the term "return ratio" (RR) to refer to $-g_{m} D$ and ascribes it to a given dependent source in the circuit [1]. Thus, the return ratio, obtained by injecting a voltage in place of $V_{G S}$ or a current in place of $I_{D}$, appears to be the same as the true loop gain ${ }^{15}$ even if the loop cannot be completely broken. In fact, the return ratio is equal to the loop gain if the circuit contains only one feedback mechanism and the loop traverses the transistor of interest. We elaborate on this point later.

#### Example 8.22

Determine the voltage gain of the source follower shown in Fig. 8.73(a) using Bode's method. Assume that $\lambda=\gamma=0$.
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vout, N2: GND}
name: M1, type: NMOS, ports: {S: Vout, D: VDD, G: Vin}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a source follower configuration with an NMOS transistor. The output voltage is taken across the resistor RS connected to ground. The gate of the NMOS is driven by the input voltage Vin, and the drain is connected to VDD.

(a)
image_name:Figure 8.73(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: gmV1, type: VoltageControlledCurrentSource, ports: {Np: V1, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a small-signal model with a voltage-controlled current source gmV1. The input voltage is Vin, and the output voltage is Vout. The resistor RS is connected to ground, and the voltage across it is Vout. The current source gmV1 is controlled by the voltage V1.

(b)

Figure 8.73

#### Solution

Figure 8.73(b) depicts the small-signal model. To compute the $A$ and $C$ coefficients, Fig. 8.70 suggests setting $g_{m}$ to zero, which results in

$$
\begin{align*}
A & =\frac{V_{\text {out }}}{V_{\text {in }}}=0  \tag{8.146}\\
C & =\frac{V_{1}}{V_{\text {in }}}=1 \tag{8.147}
\end{align*}
$$

For the $B$ and and $D$ coefficients, we set $V_{i n}$ to zero and apply a current source $I_{1}$ in lieu of $g_{m} V_{1}$ :

$$
\begin{align*}
& B=\frac{V_{\text {out }}}{I_{1}}=R_{S}  \tag{8.148}\\
& D=\frac{V_{1}}{I_{1}}=-R_{S} \tag{8.149}
\end{align*}
$$

[^57]From (8.140) or (8.141), we have

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=\frac{g_{m} R_{S}}{1+g_{m} R_{S}} \tag{8.150}
\end{equation*}
$$

The return ratio associated with the dependent source is equal to $-g_{m} D=g_{m} R_{S}$.
A peculiar result occurs here if $R_{S}$ approaches an ideal current source: the return ratio, $g_{m} R_{S}$, goes to infinity, and so does $B$. Since (8.140) was obtained by dividing by $B$ and $D$, in general it may give an incorrect value if $B$ or $D$ is infinite. In the case of the source follower, however, (8.140) produces a correct result.

#### Example 8.23

Figure 8.74(a) shows a circuit in which one transistor, $M_{1}$, resides outside the feedback loop. Using Bode's method, compute $V_{\text {out }} / V_{\text {in }}$.
image_name:Figure 8.74(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: V1}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
]
extrainfo:The circuit is a feedback amplifier with NMOS transistors M1 and M2. M1 is outside the feedback loop, and M2 is inside. The input is applied to the gate of M2, and the output is taken from the drain of M1. The source of M1 is grounded, and the drain is connected to Vout. The resistor RD is connected between VDD and Vout, while RS is connected between Vin and ground.

Figure 8.74

#### Solution

We first obtain $A$ and $C$ by setting $g_{m 1}$ to zero:

$$
\begin{align*}
& A=\frac{V_{\text {out }}}{V_{\text {in }}}=0  \tag{8.151}\\
& C=\frac{V_{1}}{V_{\text {in }}}=\frac{g_{m 2} R_{S}}{1+g_{m 2} R_{S}} \tag{8.152}
\end{align*}
$$

Next, we set $V_{i n}$ to zero and apply $I_{1}$ in lieu of $M_{1}$ :

$$
\begin{align*}
& B=\frac{V_{\text {out }}}{I_{1}}=-R_{D}  \tag{8.153}\\
& D=\frac{V_{1}}{I_{1}}=0 \tag{8.154}
\end{align*}
$$

As expected, the return ratio for $M_{1}$ is zero. We thus have

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=g_{m 1}\left(-R_{D} \frac{g_{m 2} R_{S}}{1+g_{m 2} R_{S}}\right) \tag{8.155}
\end{equation*}
$$

Alternatively, the gain can be obtained by treating $M_{2}$ as the dependent source of interest. The return ratio for $M_{2}$ is the same as that found for the source follower in the above example. Even though the circuit contains one feedback mechanism, the two return rations are unequal because the feedback loop does not traverse $M_{1}$.

#### Example 8.24

Calculate the closed-loop gain of the circuit shown in Fig. 8.75(a). Assume that $\lambda=\gamma=0$.
image_name:Fig. 8.75(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: V1}
name: M2, type: NMOS, ports: {S: GND, D: d1, G: Vin}
name: RD, type: Resistor, value: RD, ports: {N1: d1, N2: VDD}
name: RS, type: Resistor, value: RS, ports: {N1: Vout, N2: GND}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: Vin, Nn: GND}
]
extrainfo:The circuit is a common-source amplifier with NMOS transistors M1 and M2. M1 is used as an active load, and M2 is the amplifying device. The input current source Iin drives the gate of M2, and the output is taken across RS.
image_name:Fig. 8.75(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: V1}
name: M2, type: NMOS, ports: {S: GND, D: d2, G: Vout}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: d2}
name: RS, type: Resistor, value: RS, ports: {N1: Vout, N2: GND}
name: Iin, type: CurrentSource, ports: {Np: GND, Nn: Vout}
name: I1, type: CurrentSource, ports: {Np: V1, Nn: Vout}
]
extrainfo:The circuit is a common-source amplifier with NMOS transistors M1 and M2. M1 is driven by a voltage source V1, and M2 is configured as a current mirror with RD. I1 is an additional current source connected between V1 and Vout. The output is taken across RS.

Figure 8.75

#### Solution

We calculate the $A-D$ coefficients with the aid of the conceptual diagram in Fig. 8.70. We can select either transistor as the device of interest. Setting $g_{m 1}$ to zero, we obtain

$$
\begin{align*}
A & =\frac{V_{\text {out }}}{I_{\text {in }}} \text { with } g_{m 1}=0  \tag{8.156}\\
& =R_{S} \tag{8.157}
\end{align*}
$$

because, in the absence of $M_{1}, I_{i n}$ simply flows through $R_{S}$, producing a feedthrough component at the output. For $C$, we note that $V_{1}=I_{i n} R_{S}\left(-g_{m 2} R_{D}\right)-I_{i n} R_{S}$, and hence

$$
\begin{align*}
C & =\frac{V_{1}}{I_{i n}} \text { with } g_{m 1}=0  \tag{8.158}\\
& =-\left(1+g_{m 2} R_{D}\right) R_{S} \tag{8.159}
\end{align*}
$$

We now set $I_{i n}$ to zero and inject an independent current source in place of $M_{1}$, as shown in Fig. 8.75(b). Since $V_{\text {out }}=I_{1} R_{S}$,

$$
\begin{align*}
B & =\frac{V_{\text {out }}}{I_{1}} \text { with } I_{\text {in }}=0  \tag{8.160}\\
& =R_{S} \tag{8.161}
\end{align*}
$$

Also, $V_{1}=I_{1} R_{S}\left(-g_{m 2} R_{D}\right)-I_{1} R_{S}=-I_{1} R_{S}\left(1+g_{m 2} R_{D}\right)$ and

$$
\begin{align*}
D & =\frac{V_{1}}{I_{1}} \text { with } I_{i n}=0  \tag{8.162}\\
& =-R_{S}\left(1+g_{m 2} R_{D}\right) \tag{8.163}
\end{align*}
$$

Equation (8.140) thus gives

$$
\begin{align*}
\frac{V_{\text {out }}}{I_{\text {in }}} & =A+\frac{g_{m 1} B C}{1-g_{m 1} D}  \tag{8.164}\\
& =R_{S}-\frac{g_{m 1}\left(1+g_{m 2} R_{D}\right) R_{S}^{2}}{1+g_{m 1} R_{S}\left(1+g_{m 2} R_{D}\right)}  \tag{8.165}\\
& =\frac{R_{S}}{1+g_{m 1} R_{S}\left(1+g_{m 2} R_{D}\right)} \tag{8.166}
\end{align*}
$$

The reader is encouraged to repeat the derivation with $M_{2}$ as the dependent source of interest.

### 8.6.4 Blackman's Impedance Theorem

Continuing our effort to compute the closed-loop parameters of a feedback system without breaking the loop, we now study Blackman's theorem, which determines the impedance seen at any port of a general circuit. This theorem can be proved using Bode's approach.

Consider the general circuit depicted in Fig. 8.76(a), where the impedance between nodes $P$ and $Q$ is of interest. As in Bode's analysis, we have explicitly shown one of the transistors by its ideal model, the voltage-dependent current source $I_{1}$. Let us pretend that $I_{i n}$ is the input signal and $V_{i n}$ the output signal so that we can utilize Bode's results:

$$
\begin{align*}
V_{i n} & =A I_{i n}+B I_{1}  \tag{8.167}\\
V_{1} & =C I_{i n}+D I_{1} \tag{8.168}
\end{align*}
$$

It follows that

$$
\begin{equation*}
Z_{i n}=\frac{V_{i n}}{I_{i n}}=A+\frac{g_{m} B C}{1-g_{m} D} \tag{8.169}
\end{equation*}
$$

image_name:(a)
description:
[
name: Iin, type: CurrentSource, value: Iin, ports: {Np: P, Nn: Q}
name: Vin, type: VoltageSource, value: Vin, ports: {Np: P, Nn: Q}
name: V1, type: VoltageSource, value: V1, ports: {Np: P, Nn: Q}
name: I1, type: CurrentSource, value: I1, ports: {Np: P, Nn: Q}
]
extrainfo:The circuit is arranged for calculating a port impedance. The input current source Iin and the voltage source Vin are connected in parallel between nodes P and Q. The voltage source V1 and current source I1 are also connected in parallel between nodes P and Q.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: P, Nn: Q}
name: V1, type: VoltageSource, value: V1, ports: {Np: P, Nn: Q}
name: I1, type: CurrentSource, value: I1, ports: {Np: Q, Nn: P}
]
extrainfo:The circuit diagram (b) is used for calculating the open-circuit transconductance T_oc. The voltage source V1 and the current source I1 are connected across nodes P and Q, with V1 in parallel with I1.
image_name:(c)
description:
[
name: Iin, type: CurrentSource, ports: {Np: P, Nn: Q}
name: Vin, type: VoltageSource, value: Vin, ports: {Np: P, Nn: Q}
name: V1, type: VoltageSource, value: V1, ports: {Np: P, Nn: Q}
name: I1, type: CurrentSource, ports: {Np: P, Nn: Q}
]
extrainfo:The circuit diagram (c) shows a short between nodes P and Q. This configuration is used for calculating the short-circuit transmittance Tsc.

Figure 8.76 (a) Arrangement for calculating a port impedance, (b) calculation of $T_{o c}$, and (c) calculation of $T_{s c}$.
where $g_{m}$ denotes the transconductance of the transistor modeled by $I_{1}$ in Fig. 8.76(a). We now manipulate this result in three steps so as to obtain a more intuitive expression. First, we recognize from (8.168) that, if $I_{i n}=0$, then $V_{1} / I_{1}=D$. We call $-g_{m} D$ the "open-circuit loop gain" (because the port of interest is left open) and denote it by $T_{o c}$ [Fig. 8.76(b)]. Second, we note from (8.167) that, if $V_{i n}=0$, then $I_{i n}=(-B / A) I_{1}$, and hence, from (8.168),

$$
\begin{equation*}
\frac{V_{1}}{I_{1}}=\frac{A D-B C}{A} \tag{8.170}
\end{equation*}
$$

We call $-g_{m}$ times this quantity the "short-circuit" loop gain (because $V_{i n}=0$ ) and denote it by $T_{s c}$ [Fig. 8.76(c)]. Note that the circuit topology changes in these two cases. Both $T_{o c}$ and $T_{s c}$ can be viewed as return ratios associated with $I_{1}$ for the two circuit topologies. In summary,

$$
\begin{align*}
T_{o c} & =-\left.g_{m} \frac{V_{1}}{I_{1}}\right|_{I i n=0}  \tag{8.171}\\
T_{s c} & =-\left.g_{m} \frac{V_{1}}{I_{1}}\right|_{V i n=0} \tag{8.172}
\end{align*}
$$

In the third step, we use $T_{o c}$ and $T_{s c}$ to rewrite Eq. (8.169) as

$$
\begin{align*}
Z_{i n}=\frac{V_{i n}}{I_{i n}} & =\frac{A-g_{m}(B C-A D)}{1-g_{m} D}  \tag{8.173}\\
& =A \frac{1+T_{s c}}{1+T_{o c}} \tag{8.174}
\end{align*}
$$

Originally derived by Blackman [2], this result lends itself to a great deal of intuition if we recall that $A=V_{i n} / I_{i n}$ with $I_{1}=0$, i.e., when the transistor under consideration is disabled. We roughly view $A$ as the "open-loop" impedance because it is obtained without the transistor in the feedback loop. In addition, we observe that (1) if $\left|T_{s c}\right| \ll 1$, then $Z_{i n} \approx A /\left(1+T_{o c}\right)$; that is, the open-loop impedance is divided by $1+T_{o c}$; and (2) if $\left|T_{o c}\right| \ll 1$, then $Z_{i n} \approx A\left(1+T_{s c}\right)$; i.e., the open-loop impedance is multiplied by $1+T_{s c}$. Reminiscent of closed-loop input and output impedances derived in previous sections, these two cases nonetheless reveal that, in general, the closed-loop impedance cannot be expressed as $Z_{\text {in }}$ multiplied or divided by ( $1+$ the loop gain $)$.

#### Example 8.25

Determine the output impedance of a degenerated CS stage [Fig. 8.77(a)]. Assume that $\gamma=0$.
image_name:Figure 8.77(a)
description:
[
name: M1, type: NMOS, ports: {S: s1, D: LOAD, G: GND}
name: Rout, type: Resistor, value: Rout, ports: {N1: LOAD, N2: ro}
name: ro, type: Resistor, value: ro, ports: {N1: ro, N2: s1}
name: Rs, type: Resistor, value: Rs, ports: {N1: s1, N2: GND}
]
extrainfo:The circuit is a degenerated common-source stage with an NMOS transistor M1. The output is taken across the resistor Rout.

(a)
image_name:(a)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: x1, Nn: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: x1, Nn: x2}
name: Rs, type: Resistor, value: Rs, ports: {N1: x2, N2: GND}
name: ro, type: Resistor, value: ro, ports: {N1: x1, N2: x3}
]
extrainfo:The circuit is a simple series circuit with a voltage source V1, a current source I1, and resistors Rs and ro. The current I1 flows from node x1 to x2, and the voltage V1 is applied between node x1 and ground.

(b)
image_name:(b)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: x1, Nn: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: x1, Nn: GND}
name: Rs, type: Resistor, value: Rs, ports: {N1: x1, N2: GND}
name: ro, type: Resistor, value: ro, ports: {N1: x1, N2: GND}
]
extrainfo:The circuit is a simple series circuit with a voltage source V1, a current source I1, and resistors Rs and ro. The current I1 flows from node x1 to ground, and the voltage V1 is applied between node x1 and ground.

(c)

Figure 8.77

#### Solution

We must compute three quantities. First, with the transistor disabled,

$$
\begin{equation*}
A=r_{O}+R_{S} \tag{8.175}
\end{equation*}
$$

Second, with the port of interest left open [Fig. 8.77(b)], we have

$$
\begin{align*}
T_{o c} & =-g_{m} \frac{V_{1}}{I_{1}}  \tag{8.176}\\
& =0 \tag{8.177}
\end{align*}
$$

because no current flows through $R_{S}$. Third, with the port of interest shorted [Fig. 8.77(c)], we obtain

$$
\begin{align*}
T_{s c} & =-g_{m} \frac{V_{1}}{I_{1}}  \tag{8.178}\\
& =+g_{m}\left(R_{S} \| r_{O}\right) \tag{8.179}
\end{align*}
$$

It follows from Eq. (8.174) that

$$
\begin{align*}
Z_{\text {out }} & =\left(r_{O}+R_{S}\right)\left[1+g_{m}\left(R_{S} \| r_{O}\right)\right]  \tag{8.180}\\
& =\left(1+g_{m} r_{O}\right) R_{S}+r_{O} \tag{8.181}
\end{align*}
$$

The reader is encouraged to repeat the analysis while including body effect.

#### Example 8.26

Compute the output impedance of the circuit shown in Fig. 8.78(a). Assume that $\gamma=0$.
image_name:(a)
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: s1, OutP: s1, OutN: '}
name: M1, type: NMOS, ports: {S: s1, D: LOAD, G: s1}
name: RS, type: Resistor, value: RS, ports: {N1: s1, N2: GND'}
]
extrainfo:The circuit is a feedback amplifier with an NMOS transistor controlled by the output of an op-amp. The source and gate of the NMOS are connected to the same node, creating a source follower configuration. The output is taken at the drain of the NMOS, labeled as 'LOAD'. The op-amp senses the voltage at the source of M1.
image_name:(b)
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: S1, OutP: LOAD, OutN: GND}
name: M1, type: NMOS, ports: {S: S1, D: LOAD, G: GND}
name: RS, type: Resistor, value: RS, ports: {N1: S1, N2: GND}
name: Rout, type: Resistor, value: Rout, ports: {N1: LOAD, N2: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: LOAD, Nn: S1}
name: ro, type: Resistor, value: ro, ports: {N1: LOAD, N2: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: LOAD, Nn: S1}
]
extrainfo:The circuit includes an OpAmp A1 with feedback, an NMOS transistor M1, and a combination of resistors and current/voltage sources to form a load. The output is taken across the load.
image_name:(c)
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: s1, OutP: GND, OutN: '}
name: M1, type: NMOS, ports: {S: GND, D: s1, G: GND}
name: RS, type: Resistor, value: RS, ports: {N1: s1, N2: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: s1, Nn: GND}
name: ro, type: Resistor, value: ro, ports: {N1: s1, N2: GND'}
]
extrainfo:The circuit in diagram (c) includes an OpAmp A1 with its non-inverting input connected to ground and inverting input connected to node s1. NMOS M1 has its source and gate connected to ground, and its drain connected to node s1. A resistor RS and a resistor ro are both connected between node s1 and ground. A current source I1 is also connected from node s1 to ground.

Figure 8.78

#### Solution

The difficulty with this circuit is that it does not map into one of the four canonical topologies: amplifier $A_{1}$ senses the voltage at the source of $M_{1}$ whereas the output is taken at the drain. Fortunately, Blackman's theorem is impervious to such departures. Again, we proceed in three steps. With the transistor disabled,

$$
\begin{equation*}
A=r_{O}+R_{S} \tag{8.182}
\end{equation*}
$$

If the output is left open [Fig. 8.78(b)], no current flows through $R_{S}$, and hence $T_{o c}=0$. With the output shorted [Fig. 8.78(c)],

$$
\begin{equation*}
T_{s c}=g_{m}\left(R_{S} \| r_{O}\right) A_{1} \tag{8.183}
\end{equation*}
$$

Thus,

$$
\begin{align*}
Z_{\text {out }} & =\left(r_{O}+R_{S}\right)\left[1+g_{m}\left(R_{S} \| r_{O}\right) A_{1}\right]  \tag{8.184}\\
& =r_{O}+R_{S}+g_{m} r_{O} R_{S} A_{1}  \tag{8.185}\\
& =\left(1+g_{m} r_{O}\right) A_{1} R_{S}+r_{O} \tag{8.186}
\end{align*}
$$

To the first order, the factor $1+g_{m} r_{O}$ is "boosted" by another factor of $A_{1}$.

#### Example 8.27

Determine the output impedance of the source follower shown in Fig. 8.79(a). Assume that $\lambda=\gamma=0$.
image_name:Fig. 8.79(a)
description:
[
name: M1, type: NMOS, ports: {S: Vout, D: VDD, G: Vin}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a source follower configuration with an NMOS transistor M1 and a current source I1. The input voltage Vin controls the gate of M1, and the output is taken from the source terminal at Vout. The circuit is powered by VDD.

(a)
image_name:Fig. 8.79(a)
description:
[
name: M1, type: NMOS, ports: {S: Vout, D: VDD, G: Vin}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a source follower configuration with an NMOS transistor M1 and a current source I1. The input voltage Vin controls the gate of M1, and the output is taken from the source terminal at Vout. The circuit is powered by VDD.

(b)
image_name:Fig. 8.79(b)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: X1, Nn: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: X1, Nn: GND}
]
extrainfo:The circuit contains a voltage source V1 and a current source I1 connected in parallel. The node X1 is the common node connecting both sources, and the circuit is grounded.

(c)

Figure 8.79

#### Solution

With $g_{m}=0$, the output impedance, and hence $A$, are infinity. The two loop gains are obtained from Figs. 8.79(b) and (c) as $T_{s c}=0$ and $T_{o c}=\infty$, respectively. These difficulties arise because the proof of Blackman's theorem divides by $A$, tacitly assuming that $A<\infty$. One can avoid this situation by placing a resistor in parallel with the port of interest and letting it approach infinity in the end result. This is left as an exercise for the reader.

#### Example 8.28

Using Blackman's theorem, determine the input impedance of the circuit shown in Fig. 8.37(a). Assume that $\lambda=$ $\gamma=0$.

#### Solution

We set $g_{m 2}$ to zero to compute $A$, observing that $A=\infty$ ! Since the derivation of Blackman's expression relies on dividing by $A$, we know that $A=\infty$ may invalidate the result. This is one drawback of Blackman's approach. The situation becomes even more interesting if we attempt to compute $T_{o c}$. As depicted in Fig. 8.80, we apply an independent small-signal circuit source $I_{1}$ and seek $V_{1}$. The voltage at the gate of $M_{1}$ is equal to $-I_{1} R_{D} C_{1} /\left(C_{1}+C_{2}\right)$, yielding a drain current of $-g_{m 1} I_{1} R_{D} C_{1} /\left(C_{1}+C_{2}\right)$. This current must be equal to $I_{1}$, and hence

$$
\begin{equation*}
\left(1+g_{m 1} R_{D} \frac{C_{1}}{C_{1}+C_{2}}\right) I_{1}=0 \tag{8.187}
\end{equation*}
$$

This relation cannot hold because $g_{m 1} R_{D} C_{1} /\left(C_{1}+C_{2}\right)$ is not necessarily zero and $I_{1}$ itself is an external stimulus and nonzero. This nonsensical result arises because two ideal current sources, namely, $I_{1}$ and $M_{1}$, are placed in series. Similarly, $V_{1}$ cannot be calculated because the drain voltage of $M_{1}$ is not defined.
image_name:Figure 8.80
description:
[
name: RD, type: Resistor, value: RD, ports: {N1: X1, N2: VDD}
name: C1, type: Capacitor, value: C1, ports: {Np: X1, Nn: P}
name: C2, type: Capacitor, value: C2, ports: {Np: P, Nn: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: X1, Nn: D1}
name: M1, type: NMOS, ports: {S: GND, D: D1, G: P}
]
extrainfo:The circuit includes an NMOS transistor M1 with its source connected to ground, drain connected to node D1, and gate connected to node P. A current source I1 is connected between nodes X1 and D1. Capacitors C1 and C2 are connected to nodes X1, P, and ground. A resistor RD is connected between nodes X1 and VDD.

Figure 8.80

#### Example 8.29

A student wrestling with the above example decides to attach a resistance from the drain of $M_{1}$ to ground and let its value go to infinity in the final result. Does this rescue Blackman's theorem?

#### Solution

As shown in Fig. 8.81, $A=R_{T}$. Moreover, we can now compute $T_{o c}$ by writing a KCL at the drain of $M_{1}$ :

$$
\begin{equation*}
-g_{m 1} I_{1} R_{D} \frac{C_{1}}{C_{1}+C_{2}}-\frac{V_{1}}{R_{T}}=I_{1} \tag{8.188}
\end{equation*}
$$

and hence

$$
\begin{equation*}
T_{o c}=-g_{m 2} \frac{V_{1}}{I_{1}}=g_{m 2}\left(1+g_{m 1} R_{D} \frac{C_{1}}{C_{1}+C_{2}}\right) R_{T} \tag{8.189}
\end{equation*}
$$

image_name:Figure 8.81
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: x1, Nn: P}
name: C2, type: Capacitor, value: C2, ports: {Np: P, Nn: p}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: x1}
name: RT, type: Resistor, value: RT, ports: {N1: d1, N2: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: P, Nn: d}
name: I1, type: CurrentSource, value: I1, ports: {Np: x1, Nn: d}
name: M1, type: NMOS, ports: {S: GND, D: d, G: P}
]
extrainfo:The circuit contains an NMOS transistor M1 with its source connected to ground, drain to node d, and gate to node P. Capacitors C1 and C2 are connected between nodes x1 and P, and P and p, respectively. Resistors RD and RT are connected to nodes VDD and x1, and d1 and ground, respectively. Voltage source V1 is connected between nodes P and d, and current source I1 is connected between nodes x1 and d.

Figure 8.81

This result suggests that $T_{o c} \rightarrow \infty$ as $R_{T} \rightarrow \infty$. Since $T_{s c}=0$ (why?), we have

$$
\begin{align*}
R_{\text {in }} & =A \frac{1+T_{s c}}{1+T_{o c}}  \tag{8.190}\\
& =R_{T} \frac{1}{1+g_{m 2}\left(1+g_{m 1} R_{D} \frac{C_{1}}{C_{1}+C_{2}}\right) R_{T}} \tag{8.191}
\end{align*}
$$

If $R_{T} \rightarrow \infty, R_{i n}$ approaches $1 / g_{m 2}$ divided by the loop gain.
It is peculiar that the return ratio of $M_{2}$ is not equal to that of $M_{1}$ even though the circuit appears to have only one feedback mechanism. But looks can be deceiving: $M_{2}$ is degenerated by $R_{T}$, experiencing local feedback. We can say $M_{2}$ sees infinite degeneration if $R_{T}=\infty$, and hence has an infinite return ratio.

#### Example 8.30

Using Blackman's theorem, determine $R_{i n}$ in Fig. 8.82(a). Assume that $\gamma=0$.
image_name:Fig. 8.82(a)
description:
[
name: M1, type: NMOS, ports: {S: s1, D: d1, G: Vb}
name: RD, type: Resistor, value: RD, ports: {N1: d1, N2: VDD}
name: ro, type: Resistor, value: ro, ports: {N1: d1, N2: s1}
name: Rin, type: Resistor, value: Rin, ports: {N1: s1, N2: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a common-source amplifier with an NMOS transistor M1. It uses resistors RD and ro for load and degeneration, and Rin represents the input resistance.

(a)
image_name:Figure 8.82(b)
description:
[
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: X1}
name: ro, type: Resistor, value: ro, ports: {N1: X1, N2: X2}
name: I1, type: CurrentSource, value: I1, ports: {Np: X1, Nn: X2}
name: V1, type: VoltageSource, value: V1, ports: {Np: X2, Nn: GND}
]
extrainfo:The circuit is a simplified model of a common-source amplifier with resistive load and current source biasing, analyzing open-circuit conditions.

(b)

Figure 8.82

#### Solution

With $g_{m}=0$, we have $A=R_{D}+r_{O}$. If the input port is shorted, no feedback is present and $T_{s c}=0$. With the input port open [Fig. 8.82(b)], we observe that no current flows through $R_{D}, I_{1}$ generates a voltage of $-I_{1} r_{O}$ across $r_{O}$, and $V_{1}=-I_{1} r_{O}$. That is, $T_{o c}=g_{m} r_{O}$. It follows that

$$
\begin{equation*}
R_{i n}=\frac{R_{D}+r_{O}}{1+g_{m} r_{O}} \tag{8.192}
\end{equation*}
$$

as expected.

It is interesting to note that $T_{o c}>0$ even though the feedback through $r_{O}$ is positive. This occurs because the circuit contains two feedback mechanisms, one through $r_{O}$ and another due to degeneration of $M_{1}$ by an infinite source resistance. In such a case, the sign of $T_{o c}$ does not reveal the polarity of feedback. This point becomes clearer in the next example.

#### Example 8.31

Determine the return ratios of $M_{1}$ and $M_{2}$ in Fig. 8.83(a), assuming $\lambda=\gamma=0$.
image_name:Figure 8.83(a)
description:
[
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: d1g1}
name: RS, type: Resistor, value: RS, ports: {N1: Vout, N2: GND}
name: M1, type: NMOS, ports: {S: Vout, D: d1g1, G: Vin}
name: M2, type: NMOS, ports: {S: d1g1, D: VDD, G: Vout}
]
extrainfo:The circuit is a common source amplifier with NMOS transistors M1 and M2. The resistor RS provides source degeneration, and RD is the load resistor. M2 provides positive feedback to the source of M1.

(a)
image_name:(b)
description:
[
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: g2}
name: RS, type: Resistor, value: RS, ports: {N1: S2, N2: GND}
name: M2, type: NMOS, ports: {S: S2, D: VDD, G: g2}
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: g2, Nn: S2}
]
extrainfo:The circuit is a common source amplifier with NMOS transistor M2. The resistor RS provides source degeneration, and RD is the load resistor. M2 provides positive feedback to the source. A current source I1 is connected between nodes g2 and S2, and a voltage source V1 is connected to the ground.

(b)
image_name:Figure 8.83
description:
[
name: RD, type: Resistor, value: RD, ports: {N1: d1, N2: VDD}
name: RS, type: Resistor, value: RS, ports: {N1: s1, N2: GND}
name: M1, type: NMOS, ports: {S: s1, D: d1, G: s1}
name: I2, type: CurrentSource, value: I2, ports: {Np: s1, Nn: VDD}
]
extrainfo:The circuit is a common source amplifier with NMOS transistor M1. The resistor RS provides source degeneration, and RD is the load resistor. A current source I2 is connected between nodes s1 and VDD.

(c)

Figure 8.83

#### Solution

In this circuit, $R_{S}$ degenerates both $M_{1}$ and $M_{2}$, and $M_{2}$ returns a voltage to the source of $M_{1}$ with positive feedback. Injecting a current as shown in Fig. 8.83(b), we note that $R_{S}$ carries a current of $-V_{1} / R_{S}$, leading to $I_{D 2}=-I_{1}-V_{1} / R_{S}$, and hence $V_{G S 2}=\left(-I_{1}-V_{1} / R_{S}\right) / g_{m 2}$. Adding the voltage drops across $R_{D}$ and $R_{S}$ to $V_{G S 2}$, we have

$$
\begin{equation*}
I_{1} R_{D}-\frac{I_{1}}{g_{m 2}}-\frac{V_{1}}{g_{m 2} R_{S}}-V_{1}=0 \tag{8.193}
\end{equation*}
$$

and

$$
\begin{align*}
R R_{1} & =-g_{m 1} \frac{V_{1}}{I_{1}}  \tag{8.194}\\
& =\frac{1-g_{m 2} R_{D}}{1+g_{m 2} R_{S}} g_{m 1} R_{S} \tag{8.195}
\end{align*}
$$

For $R R_{2}$, the arrangement in Fig. 8.83(c) yields $I_{D 1}=-I_{2} R_{S} /\left(R_{S}+1 / g_{m 1}\right)=-I_{2} g_{m 1} R_{S} /\left(1+g_{m 1} R_{S}\right)$. Adding the voltage drops across $R_{D}$ and $R_{S}$ to $V_{2}$, we obtain

$$
\begin{equation*}
-\frac{I_{2} g_{m 1} R_{S}}{1+g_{m 1} R_{S}} R_{D}+V_{2}+I_{2} \frac{1 / g_{m 1}}{R_{S}+1 / g_{m 1}} R_{S}=0 \tag{8.196}
\end{equation*}
$$

It follows that

$$
\begin{equation*}
R R_{2}=\frac{1-g_{m 1} R_{D}}{1+g_{m 1} R_{S}} g_{m 2} R_{S} \tag{8.197}
\end{equation*}
$$

The return ratios are unequal and can assume positive or negative values independently.

## 8.7 ■ Middlebrook's Method

Middlebrook exploits the "Dissection Theorem" to derive the closed-loop transfer function without breaking the loop and while revealing the effect of backward (reverse) propagation in non-unilateral loops [5, 6]. This theorem states that any transfer function, $H(s)$, can be dissected into a product of the form

$$
\begin{equation*}
H(s)=H_{\infty} \frac{1+\frac{1}{T_{2}}}{1+\frac{1}{T_{1}}} \tag{8.198}
\end{equation*}
$$

where $H_{\text {infty }}, T_{1}$, and $T_{2}$ are simpler transfer functions corresponding to special cases, e.g., with some signal in the loop forced to zero. These quantities are computed as follows. As shown in Fig. 8.84, we insert a voltage source, $V_{t}$, in series with a branch of the circuit and inject a current, $I_{t}$, to either side of $V_{t}$. We now have four new quantities, namely, $V_{1}, V_{2}, I_{1}$, and $I_{2}$. (Note the polarity of $V_{1}$.) The key point here is that the loop is not broken, and hence loading effects are immaterial. The "ideal" transfer function, $H_{\infty}$, is obtained as follows:

$$
\begin{equation*}
H_{\infty}(s)=\left.\frac{V_{\text {out }}}{V_{\text {in }}}\right|_{V 1=0, I 1=0} \tag{8.199}
\end{equation*}
$$

image_name:Figure 8.84
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Vt, type: VoltageControlledVoltageSource, value: Vt, ports: {Np: Node1, Nn: Node2}
name: It, type: CurrentSource, value: It, ports: {Np: Node2, Nn: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: GND, Nn: Node1}
name: V2, type: VoltageSource, value: V2, ports: {Np: Node3, Nn: GND}
]
extrainfo:The circuit illustrates Middlebrook's method for measuring transfer functions. It includes a voltage source Vin, a voltage-controlled voltage source Vt, a current source It, and two other voltage sources V1 and V2. The method involves setting V1 and I1 to zero to obtain the ideal transfer function H∞.

Figure 8.84 Illustration of Middlebrook's method.
i.e., we choose $V_{t}$ and $I_{t}$ such that $V_{1}$ and $I_{1}$ are forced to zero. The other two transfer functions are more involved. Middlebrook shows that

$$
\begin{equation*}
\frac{1}{T_{1}}=\frac{1}{T_{i}}+\frac{1}{T_{v}}+\frac{1}{T_{i}^{\prime} T_{v}^{\prime}} \tag{8.200}
\end{equation*}
$$

where $V_{i n}=0$ and

$$
\begin{align*}
T_{i} & =\left.\frac{I_{1}}{I_{2}}\right|_{V 1=0} \quad \text { (Short-circuit forward current loop gain) }  \tag{8.201}\\
T_{v} & =\left.\frac{V_{1}}{V_{2}}\right|_{I 1=0} \quad \text { (Open-circuit forward voltage loop gain) }  \tag{8.202}\\
\frac{1}{T_{i}^{\prime}} & =\left.\frac{I_{2}}{I_{1}}\right|_{V 2=0} \quad \text { (Short-circuit reverse current loop gain) }  \tag{8.203}\\
\frac{1}{T_{v}^{\prime}} & =\left.\frac{V_{2}}{V_{1}}\right|_{I 2=0} \quad \text { (Open-circuit reverse voltage loop gain) } \tag{8.204}
\end{align*}
$$

The computation of $T_{2}$ is similar, except that it requires $V_{\text {out }}$ (rather than $V_{i n}$ ) to be forced to zero. We observe that Middlebrook's approach is generally more laborious than Bode's method.

Middlebrook's formulation provides insight regarding the forward (usually desirable) and reverse (usually undesirable) signal propagation around a nonunilateral loop. With no reverse propagation, we have $1 / T_{i}^{\prime}=1 / T_{v}^{\prime}=0$ and $T_{1}=T_{i} \| T_{v}$, e.g., the parallel combination of the two forward loop gains. Middlebrook denotes this quantity by $T_{f w d}$. In a similar fashion, we can define the total reverse loop gain as $T_{\text {rev }}=\left(1 / T_{i}^{\prime}\right) \|\left(1 / T_{v}^{\prime}\right)$ and manipulate Eq. (8.200) to reach

$$
\begin{equation*}
T_{1}=\frac{T_{f w d}}{1+T_{r e v}} \tag{8.205}
\end{equation*}
$$

The interesting observation here is that the equivalent loop gain is degraded if the reverse loop gain, $T_{r e v}$, becomes comparable to unity-even if it remains much less than $T_{f w d}$. Middlebrook, however, recognizes that this interpretation is valid only if (a) $V_{t}$ and $I_{t}$ are injected such that $V_{1}$ and $I_{1}$ are the "error" signal, a vague definition, and (b) $V_{t}$ and $I_{t}$ are injected inside the major loop and outside any minor loops, again a vague condition. For example, a degenerated CS stage with $\lambda>0$ eludes both of these conditions.

## 8.8 - Loop Gain Calculation Issues

### 8.8.1 Preliminary Concepts

The loop gain plays a central role in feedback systems, as evidenced by the universal factor $1+\beta A$ in the closed-loop expressions of gain, bandwidth, input and output impedances, and nonlinearity. In addition, if the poles and zeros in the loop are considered, then the loop gain [called the "loop transmission," $T(s)$, in this case] reveals the circuit's stability properties. For these reasons, we must often determine the loop gain even if we are not interested in the open-loop parameters of the circuit.

According to the procedure illustrated in Fig. 8.5, the loop gain calculation should be straightforward: we set the input to zero, break the loop at some point, apply a test signal, follow this signal around the loop (in the proper direction), and obtain the returned signal. However, in some cases, the situation is more complex, eliciting two questions: (1) Can we break the loop at any arbitrary point? (2) Should the test signal be a voltage or a current? We remind the reader that in such a test, the actual input and output disappear; i.e., the loop gain does not depend on where the main input and output ports are.

For example, consider the two-stage amplifier shown in Fig. 8.85(a), where the resistive divider consisting of $R_{1}$ and $R_{2}$ senses the output voltage and returns a fraction thereof to the source of $M_{1}$. As illustrated in Fig. 8.85(b), we set $V_{i n}$ to zero, break the loop at node $X$, apply a test signal to the right terminal of $R_{1}$, and measure the resulting $V_{F}{ }^{16}$ But is this test setup correct? First, we note that in Fig. 8.85(a), $R_{1}$ draws an ac current from $R_{D 2}$, but in Fig. 8.85(b), it does not. That is, the gain associated with the second common-source stage has been altered. Second, why did we decide to apply a test voltage? Can we apply a test current and measure a returned current?

To address the first issue, we surmise that it is best to break the loop at the gate of a MOSFET. We can break the loop at the gate of $M_{2}$ [Fig. 8.85(c)] and thus not alter the gain associated with the first stage-at least at low frequencies. The reader is encouraged to derive the loop gain using Figs. 8.85(b) and (c) and show that they are not equal.

What if we must include $C_{G S}$ of $M_{2}$ [Fig. 8.86(a)]? Then, we break the loop after $C_{G S 2}$ [Fig. 8.86(b)] to ensure that the load seen by $M_{1}$ remains unchanged. But is it always possible to break the loop at the

[^58]image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1, G: Vin}
name: M2, type: NMOS, ports: {S: d1, D: Vout, G: d1}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: d1}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: Vout}
name: R1, type: Resistor, value: R1, ports: {N1: X(Vout), N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vin, N2: GND}
name: S1, type: VoltageSource, value: S1, ports: {Np: Vin, Nn: X(Vout)}
]
extrainfo:The circuit is a two-stage feedback amplifier with NMOS transistors. It includes a feedback loop broken at the gate of M2 to analyze the loop gain. The circuit aims to maintain the load seen by M1 unchanged by breaking the loop after CGS2.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: VF, G: d1g2}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: VF}
name: RD1, type: Resistor, value: RD1, ports: {N1: VF, N2: VDD}
name: RD2, type: Resistor, value: RD2, ports: {N1: Vout, N2: VDD}
name: R1, type: Resistor, value: R1, ports: {N1: d1g2, N2: d2}
name: R2, type: Resistor, value: R2, ports: {N1: d1g2, N2: GND}
name: S1, type: VoltageSource, value: S1, ports: {Np: d1g2, Nn: GND}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: d2, Nn: GND}
]
extrainfo:This is a two-stage amplifier circuit with feedback, where the loop is broken at the gate of M2. The circuit includes resistors RD1 and RD2 connected to VDD, and a voltage source Vt is connected to the gate of M2. The NMOS transistors M1 and M2 are configured to amplify the input signal. The feedback is applied at the gate of M2 to stabilize the gain.
image_name:(c)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: VF, G: d1}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: Vt}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: VF}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: Vout}
name: R1, type: Resistor, value: R1, ports: {N1: d2, N2: Vt}
name: R2, type: Resistor, value: R2, ports: {N1: S1, N2: GND}
name: S1, type: VoltageSource, value: S1, ports: {Np: S1, Nn: GND}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: Vt, Nn: d2}
]
extrainfo:This is a two-stage feedback amplifier with a loop broken at the gate of M2. The circuit includes two NMOS transistors, M1 and M2, with feedback provided through resistors and a voltage source Vt. The output is taken at the drain of M2.

Figure 8.85 (a) Two-stage feedback amplifier, (b) breaking the loop at the left terminal of $R_{1}$, and (c) breaking the loop at the gate of $M_{2}$.
image_name:Figure 8.85 (a)
description:
[
name: M1, type: NMOS, ports: {S: Vin, D: d1, G: d1g}
name: M2, type: NMOS, ports: {S: d1, D: Vout, G: d2}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: d1}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: Vout}
name: R1, type: Resistor, value: R1, ports: {N1: X, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vin, N2: GND}
name: CGS2, type: Capacitor, value: CGS2, ports: {Np: d1g, Nn: GND}
name: S1, type: Switch, ports: {N1: Vin, N2: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: Vt, Nn: d2}
]
extrainfo:This is a two-stage feedback amplifier with a loop broken at the gate of M2. The circuit includes two NMOS transistors, M1 and M2, with feedback provided through resistors and a voltage source Vt. The output is taken at the drain of M2.
image_name:Figure 8.85 (b)
description:
[
name: M1, type: NMOS, ports: {S: S1, D: d1, G: VF}
name: M2, type: NMOS, ports: {S: d2, D: d1, G: Vt}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: d1}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: d1}
name: R1, type: Resistor, value: R1, ports: {N1: d2, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: S1, N2: GND}
name: CGS2, type: Capacitor, value: CGS2, ports: {Np: d2, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: Vt, Nn: d2}
]
extrainfo:This circuit diagram represents a two-stage feedback amplifier with a loop broken at the gate of M2. The circuit includes key components such as two NMOS transistors (M1 and M2), resistors, and a capacitor. The feedback is provided through resistors and a test voltage source Vt. The output is taken at the drain of M2.

Figure 8.86 (a) Two-stage amplifier including $C_{G S 2}$, and (b) breaking the loop at the gate of $M_{2}$.
gate of a MOSFET? Yes, indeed. For the feedback to be negative, the signal must be sensed by at least one gate in the loop because only the common-source topology inverts signals.

Let us now turn our attention to the second issue, namely, the type of the test signal. In the foregoing study, we naturally chose a test voltage, $V_{t}$, because we replaced the controlling voltage of a MOSFET with an independent source. Under what condition can we apply a test current? In Fig. 8.85(a), for example, we can break the loop at the drain of $M_{2}$, inject a current $I_{t}$, and measure the current returned by $M_{2}$ [Fig. 8.87(a)]. The reader can prove that $I_{F} / I_{t}$ in this case is the same as $V_{F} / V_{t}$ in Fig. 8.85(c).

But what exactly should we do with the drain node of $M_{2}$ in Fig. 8.87(a)? If tied to ac ground, this node does not experience the voltage excursions present in the closed-loop circuit—an issue when $r_{O 2}$ is taken into account. We can merge $r_{O 2}$ with $R_{D 2}$ in this case, but not if $M_{2}$ is degenerated. Thus, in general, we cannot inject $I_{t}$ without altering some aspects of the circuit.

Not all hope is lost yet. Suppose we replace the controlled current source of $M_{2}$ with an independent current source, $I_{t}$, and compute the returned $V_{G S}$ as $V_{F}$ [Fig. 8.87(b)]. Since in the original circuit, the dependent source and $V_{G S 2}$ were related by a factor of $g_{m 2}$, we can now write the loop gain as $\left(-V_{F} / I_{t}\right) \times g_{m 2}$. This approach is feasible even if $M_{2}$ is degenerated. We recognize that this result is the same as the return ratio of $M_{2}$.

At low frequencies, the loop gain can be computed with the aid of the following observation. Since the circuit incorporates negative feedback, the loop must traverse the gate of a transistor (only the CS stage
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1, G: x2}
name: M2, type: NMOS, ports: {S: GND, D: xv, G: d1}
name: R1, type: Resistor, value: R1, ports: {N1: x2, N2: s1}
name: R2, type: Resistor, value: R2, ports: {N1: s1, N2: GND}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: d1}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: xv}
name: IF, type: CurrentSource, value: IF, ports: {Np: d1, Nn: GND}
name: It, type: CurrentSource, value: It, ports: {Np: xv, Nn: GND}
]
extrainfo:The circuit in Figure 8.87 (a) shows a two-stage amplifier with NMOS transistors M1 and M2. The feedback loop is broken at the drain of M2, allowing for the analysis of loop gain. The circuit uses resistors RD1 and RD2 for load, and R1 and R2 for biasing. A current source IF is connected to the drain of M2, and another current source It is connected to the node xv. The circuit is powered by VDD.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: s1, D: d1, G: x1}
name: RD1, type: Resistor, value: RD1, ports: {N1: d1, N2: VDD}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: x1}
name: R1, type: Resistor, value: R1, ports: {N1: x1, N2: s1}
name: R2, type: Resistor, value: R2, ports: {N1: s1, N2: GND}
name: It, type: CurrentSource, ports: {Np: x1, Nn: GND}
name: VF, type: VoltageSource, ports: {Np: x1, Nn: s1}
]
extrainfo:The circuit diagram (b) shows a feedback loop broken at the dependent source of M2, replaced with an independent voltage source VF and a current source It. The NMOS transistor M1 is connected with its source to node s1, drain to node d1, and gate to node x1. The resistors RD1 and RD2 are connected to VDD, while R1 and R2 provide biasing between nodes x1 and s1.

Figure 8.87 (a) Breaking the loop at the drain of $M_{2}$, and (b) replacing dependent source of $M_{2}$ with an independent source.
inverts). ${ }^{17}$ We can therefore break the loop at this gate without the need for including loading effects. Of course, this method applies only if the loop has only one feedback mechanism.

In summary, the "best" place to break a feedback loop is (a) the gate-source of a MOSFET if voltage injection is desired, or (b) the dependent current source of a MOSFET if current injection is desired (provided that the returned quantity is $V_{G S}$ of the MOSFET). Of course, these two methods are related because they differ by only a factor of $g_{m}$.

Unfortunately, the foregoing techniques face difficulties in some cases. For example, suppose we include $C_{G D 2}$ in Fig. 8.85(a). We inject a test voltage or current as before, but the issue is that $C_{G D 2}$ does not allow a "clean" break. As shown in Fig. 8.88, even though we provide the gate-source voltage by the independent source, $V_{t}, C_{G D 2}$ still creates "local" feedback from the drain of $M_{2}$ to its gate, raising the question of whether the loop gain should be obtained by nulling all feedback mechanisms. We should also mention that the method of current and voltage injection proposed by Middlebrook in [3] applies only if the loop is unilateral.
image_name:Figure 8.88
description:
[
name: M1, type: NMOS, ports: {S: GND, D: VF, G: S1}
name: R1, type: Resistor, value: R1, ports: {N1: S1, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: S1, N2: GND}
name: RD1, type: Resistor, value: RD1, ports: {N1: VF, N2: VDD}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: X1}
name: CGD2, type: Capacitor, value: CGD2, ports: {Np: VF, Nn: X1}
name: S1, type: VoltageSource, value: S1, ports: {Np: S1, Nn: GND}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: Vt, Nn: GND}
name: gm2Vt, type: VoltageControlledCurrentSource, value: gm2Vt, ports: {Np: X1, Nn: GND}
]
extrainfo:The circuit is a two-stage amplifier with feedback. It includes an NMOS transistor M1, resistors RD1 and RD2 for load, and a feedback capacitor CGD2. The voltage sources S1 and Vt provide biasing, while the voltage-controlled current source gm2Vt models the transconductance of the second stage.

Figure 8.88 Two-stage amplifier
including $C_{D 2}$.

### 8.8.2 Difficulties with Return Ratio

Bode's method enables us to compute the closed-loop transfer function in terms of four simpler transfer functions-without the need for breaking the loop. But we are also interested in the loop gain as it

[^59]image_name:(a)
description:
[
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: g2}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: d2}
name: R1, type: Resistor, value: R1, ports: {N1: d2, N2: X1}
name: R2, type: Resistor, value: R2, ports: {N1: X1, N2: GND}
name: M1, type: NMOS, ports: {S: GND, D: d2, G: X1}
name: M2, type: NMOS, ports: {S: GND, D: d2, G: g2}
name: I1, type: CurrentSource, value: I1, ports: {Np: V1, Nn: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
]
extrainfo:The circuit is a two-stage amplifier with NMOS transistors M1 and M2. RD1 and RD2 are the load resistors. V1 and I1 provide biasing. The feedback loop includes M2 and affects the overall gain and stability.
image_name:(b)
description:
[
name: RD1, type: Resistor, value: RD1, ports: {N1: d1, N2: VDD}
name: RD2, type: Resistor, value: RD2, ports: {N1: d1, N2: X1}
name: R2, type: Resistor, value: R2, ports: {N1: s1, N2: GND}
name: R1, type: Resistor, value: R1, ports: {N1: s1, N2: X1}
name: M2, type: NMOS, ports: {S: GND, D: d2, G: g2}
name: M1, type: NMOS, ports: {S: s1, D: d1, G: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: X1, Nn: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: X1, Nn: GND}
]
extrainfo:The circuit is a two-stage amplifier with NMOS transistors M1 and M2. It includes resistive loads RD1 and RD2, and uses a voltage source V1 and a current source I1 for biasing. The circuit is powered by VDD.

Figure 8.89 Equivalent circuits for the calculation of the return ratios for (a) $M_{1}$, and (b) $M_{2}$.
determines the consequences of applying feedback to a given circuit, e.g., the increase in the bandwidth, the reduction in the nonlinearity, and the stability behavior.

We may view the return ratio associated with a given dependent source as the loop gain, but circuits containing more than one feedback mechanism may exhibit different return ratios for different sources. As an example, we consider again the two-stage amplifier shown in Fig. 8.85(a), recognizing that $R_{1}$ and $R_{2}$ provide both "global" feedback and "local" feedback (by degenerating $M_{1}$ ). With the aid of the equivalent circuits shown in Fig. 8.89, the reader can show that the return ratios for $M_{1}$ and $M_{2}$ are respectively given by

$$
\begin{equation*}
\text { Return Ratio }_{M 1}=\frac{g_{m 1} R_{2}\left(R_{1}+R_{D 2}+g_{m 2} R_{D 2} R_{D 1}\right)}{R_{1}+R_{2}+R_{D 2}} \tag{8.206}
\end{equation*}
$$

and

$$
\begin{equation*}
\text { Return Ratio }_{M 2}=\frac{g_{m 1} g_{m 2} R_{2} R_{D 1} R_{D 2}}{\left(1+g_{m 1} R_{2}\right)\left(R_{1}+R_{D 2}\right)+R_{2}} \tag{8.207}
\end{equation*}
$$

If, as in our standard loop gain calculations, we break the loop at the gate of $M_{2}$, we obtain a value equal to the return ratio for $M_{2}$. It is unclear which return ratio should be considered the loop gain.

Why are the two return ratios different here? This is because disabling $M_{1}$ (by making $I_{1}$ an independent source) removes both feedback mechanisms whereas disabling $M_{2}$ still retains the degeneration experienced by $M_{1}$.

Another method of loop gain calculation is to inject a signal without breaking the loop, as shown in Fig. 8.90, and write $Y / W=1 /\left(1+\beta A_{0}\right)$, and hence

$$
\begin{equation*}
\text { Loop Gain }=\left(\frac{Y}{W}\right)^{-1}-1 \tag{8.208}
\end{equation*}
$$

image_name:Figure 8.90
description:The diagram in Figure 8.90 represents a feedback loop system used for calculating loop gain by injecting a signal without breaking the loop. The main components of the system include:

1. **Summing Junctions (Adders):** There are two summing junctions in the diagram. The first summing junction is located at the input, where it combines the input signal with the feedback signal. The second summing junction is located at the output, where the injected signal \( W \) is combined with the output signal \( Y \).

2. **Amplifier (\( A_0 \)):** The amplifier block \( A_0 \) is placed between the two summing junctions. It amplifies the input signal from the first summing junction before sending it to the second summing junction.

3. **Feedback Path (\( \beta \)):** The feedback loop is created by the feedback block \( \beta \), which takes a portion of the output signal \( Y \) and feeds it back to the input summing junction. This feedback path is responsible for controlling the overall gain of the system.

**Flow of Information or Control:**
- The input signal is initially combined with the feedback signal at the first summing junction.
- The combined signal is then amplified by the amplifier \( A_0 \).
- The amplified signal is sent to the second summing junction, where it is combined with the injected signal \( W \) to produce the output signal \( Y \).
- A portion of the output signal \( Y \) is fed back through the feedback block \( \beta \) to the first summing junction, completing the feedback loop.

**Labels, Annotations, and Key Indicators:**
- \( W \) represents the injected signal point.
- \( Y \) denotes the output signal.
- \( A_0 \) and \( \beta \) are key parameters indicating the amplifier gain and feedback factor, respectively.

**Overall System Function:**
The primary function of this system is to calculate the loop gain by injecting a signal \( W \) without breaking the loop. This approach allows for analyzing the stability and performance of the feedback system, particularly in non-unilateral circuits where different injection points might yield different loop gains. The feedback loop, consisting of the amplifier and feedback block, regulates the system's gain and stability.

Figure 8.90 Another method of loop gain calculation.
image_name:(a)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: g1}
name: RF, type: Resistor, value: RF, ports: {N1: x1, N2: g1}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Y}
name: M1, type: NMOS, ports: {S: GND, D: Y, G: g1}
]
extrainfo:The circuit is used to calculate loop gain by injecting a signal W in the feedback loop. The feedback loop includes an amplifier and a feedback block. The node g1 is the gate of the NMOS M1, and the node Y is the drain, connected to resistor RD and VDD. The source of M1 is connected to ground.
image_name:(b)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: X2}
name: RF, type: Resistor, value: RF, ports: {N1: X2, N2: d1}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Y}
name: M1, type: NMOS, ports: {S: GND, D: Y, G: d1}
name: W, type: VoltageControlledVoltageSource, value: W, ports: {Np: d1, Nn: X2}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit diagram shows a feedback loop with an NMOS transistor and resistors RS, RF, and RD. The loop gain is analyzed by injecting a signal W at different points. The NMOS transistor M1 is used to control the feedback loop, and the circuit is powered by a voltage source VDD.

Figure 8.91 Different injection points in a nonunilateral circuit.

But this method tacitly assumes a unilateral loop, yielding different loop gains for different injection points if the loop is not unilateral. For example, the circuit of Fig. 8.71(a) can be excited as shown in Figs. 8.91(a) or (b), producing different values for $(Y / W)^{-1}-1$.

The exact calculation of the loop gain for non-unilateral or multiloop circuits is beyond the scope of this book.

## 8.9 ■ Alternative Interpretations of Bode's Method

Bode's results can be manipulated to produce other forms that offer new insights.
Asymptotic Gain Form Let us return to $V_{\text {out }} / V_{\text {in }}=A+g_{m} B C /\left(1-g_{m} D\right)$ and note that $V_{\text {out }} / V_{\text {in }}=A$ if $g_{m}=0$ (the dependent source is disabled) and $V_{\text {out }} / V_{\text {in }}=A-B C / D$ if $g_{m} \rightarrow \infty$ (the dependent source is very "strong"). We denote these values of $V_{\text {out }} / V_{\text {in }}$ by $H_{0}$ and $H_{\infty}$, respectively, and $-g_{m} D$ by $T$. It is helpful to consider $H_{0}$ as the direct feedthrough and $H_{\infty}$ as the "ideal" gain, i.e., if the dependent source were infinitely strong (or the loop gain were infinite). It follows that

$$
\begin{align*}
\frac{V_{\text {out }}}{V_{\text {in }}} & =H_{0}+\frac{g_{m} B C}{1+T}  \tag{8.209}\\
& =H_{0} \frac{1+T}{1+T}+\frac{g_{m} B C}{1+T}  \tag{8.210}\\
& =\frac{H_{0}}{1+T}+\frac{T\left(H_{0}+g_{m} B C / T\right)}{1+T} \tag{8.211}
\end{align*}
$$

Since $H_{0}+g_{m} B C / T=A-g_{m} B C /\left(g_{m} D\right)=A-B C / D=H_{\infty}$, we have

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=H_{\infty} \frac{T}{1+T}+H_{0} \frac{1}{1+T} \tag{8.212}
\end{equation*}
$$

Called the "asymptotic gain equation" [4], this form reveals that the gain consists of an ideal value multiplied by $T /(1+T)$ and a direct feedthrough multiplied by $1 /(1+T)$. The calculations are somewhat simpler here if we recognize from $V_{1}=C V_{i n}+D I_{1}$ and $I_{1}=g_{m} V_{1}$ that $V_{1}=C V_{i n} /\left(1-g_{m} D\right) \rightarrow 0$ if $g_{m} \rightarrow \infty$ (provided that $V_{i n}<\infty$ ). This is similar to how a virtual ground is created if the loop gain is large.

#### Example 8.32

Calculate the voltage gain of the circuit shown in Fig. 8.92(a) using the asymptotic gain method. Assume that $\lambda=\gamma=0$.
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: X}
name: R2, type: Resistor, value: R2, ports: {N1: X, N2: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vout, N2: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
]
extrainfo:The circuit is a multi-stage amplifier using NMOS transistors and resistors. It features two NMOS transistors, M1 and M2, connected in a specific configuration to amplify the input voltage Vin to produce Vout. The circuit operates with a power supply voltage VDD and has resistors R1, R2, RS, and RD to control current and voltage levels within the circuit.
image_name:(b)
description:The system block diagram labeled as "(b)" represents an electrical circuit designed to analyze voltage gain using the asymptotic gain model. Here is a detailed description:

1. **Main Components:**
- **Voltage Source (Vin):** The input voltage source, denoted as \( V_{in} \), is where the input signal is applied.
- **Resistor \( R_1 \):** Connected in series with the input voltage source, \( R_1 \) is a resistor that affects the input impedance and the voltage division in the circuit.
- **Operational Amplifier (Op-Amp):** The central component is an operational amplifier with an infinite open-loop gain (\( A_0 = -\infty \)). The op-amp receives the input from \( R_1 \) and provides the main amplification in the circuit.
- **Feedback Resistor \( R_2 \):** This resistor is connected from the output of the op-amp back to its input, forming a feedback loop that stabilizes the gain and sets the closed-loop gain of the system.

2. **Flow of Information or Control:**
- The input voltage \( V_{in} \) is applied across \( R_1 \), which then feeds into the non-inverting input of the operational amplifier (indicated by the positive input sign).
- The op-amp amplifies the input signal, and the output voltage \( V_{out} \) is taken from the output of the op-amp.
- A feedback loop is established by connecting \( R_2 \) from the output back to the inverting input (indicated by the negative input sign) of the op-amp. This feedback loop controls the overall gain of the amplifier.

3. **Labels, Annotations, and Key Indicators:**
- The diagram indicates the feedback mechanism with \( X_1 \) as the node where feedback is applied, helping in understanding the control over gain.
- The op-amp's infinite gain \( A_0 = -\infty \) suggests that it operates in a virtual ground configuration, ensuring that the voltage difference between its inputs is minimized.

4. **Overall System Function:**
- The primary function of this system is to amplify the input voltage \( V_{in} \) using the operational amplifier with a defined gain set by the resistors \( R_1 \) and \( R_2 \). The feedback loop plays a crucial role in stabilizing the system and setting the desired gain. The infinite gain of the op-amp implies that the system can achieve a very high closed-loop gain, constrained only by the feedback network.
image_name:(c)
description:The system block diagram labeled "(c)" consists of a series of components designed to model or simulate a particular electronic circuit's behavior, particularly focusing on voltage gain.

1. **Main Components:**
- **Input Voltage Source (Vin):** The system starts with an input voltage source labeled \(V_{in}\).
- **Resistor (R1):** This is connected in series with the input source and serves as the first component in the signal path.
- **First Amplifier Block:** The signal from \(V_{in}\) passes through \(R_1\) and enters the first amplifier block. This amplifier is labeled with a gain of \(-g_{m1}R_D\), indicating it is an inverting amplifier with a gain proportional to the transconductance \(g_{m1}\) and the drain resistance \(R_D\).
- **Second Amplifier Block:** After the first amplifier, the signal is fed into a second amplifier block, which has a gain of \(+1\). This block acts as a buffer, maintaining the signal level without further amplification or attenuation.
- **Resistor (R2):** Connected in the feedback loop, \(R_2\) provides negative feedback by connecting the output back to the input of the first amplifier.
- **Output Voltage (Vout):** The final output voltage \(V_{out}\) is taken from the output of the second amplifier.

2. **Flow of Information or Control:**
- The signal flow starts from the input voltage \(V_{in}\), passes through \(R_1\), and enters the first amplifier block.
- The amplified signal, with an inversion due to the negative gain of \(-g_{m1}R_D\), is then passed to the second amplifier.
- The second amplifier, with a gain of \(+1\), outputs the signal as \(V_{out}\).
- A feedback loop is established from \(V_{out}\) through \(R_2\) back to the input of the first amplifier, stabilizing the circuit and controlling the gain.

3. **Labels, Annotations, and Key Indicators:**
- The amplifiers are labeled with their respective gains, \(-g_{m1}R_D\) and \(+1\), indicating their roles in signal inversion and buffering.
- \(R_1\) and \(R_2\) are critical in defining the input path and feedback loop.

4. **Overall System Function:**
- The primary function of this system is to provide a controlled voltage gain from \(V_{in}\) to \(V_{out}\) with inversion and buffering. The feedback loop through \(R_2\) ensures stability and precise gain control. This configuration is typical in operational amplifier circuits used for signal conditioning and processing applications.

Figure 8.92

#### Solution

Suppose $M_{1}$ is the dependent source of interest. If $g_{m 1}=0$, then $V_{i n}$ propagates through $R_{1}$ and $R_{2}$ and sees an impedance of $\left(1 / g_{m 2}\right) \| R_{S}$ at the source of $M_{2}$. Thus,

$$
\begin{equation*}
H_{0}=\frac{\left(1 / g_{m 2}\right) \| R_{S}}{\left(1 / g_{m 2}\right) \| R_{S}+R_{1}+R_{2}} \tag{8.213}
\end{equation*}
$$

If $g_{m 1}=\infty$, then $V_{G S 1}=0$ (like a virtual ground), yielding a current of $V_{i n} / R_{1}$ through $R_{1}$ and $R_{2}$. That is

$$
\begin{equation*}
H_{\infty}=-\frac{R_{2}}{R_{1}} \tag{8.214}
\end{equation*}
$$

an expected result because $M_{1}$ and $M_{2}$ operate as an op amp with an infinite open-loop gain [Fig. 8.92(b)]. To determine the return ratio for $M_{1}$, we set $V_{i n}$ to zero, replace $M_{1}$ 's dependent source with an independent source, $I_{1}$, and express $V_{X}$ as $-I_{1} R_{D}$. Since $M_{2}$ sees a load resistance of $R_{S} \|\left(R_{1}+R_{2}\right)$, we have $V_{\text {out }}=-I_{1} R_{D}\left[R_{S} \|\left(R_{1}+\right.\right.$ $\left.\left.R_{2}\right)\right] /\left[1 / g_{m 2}+R_{S} \|\left(R_{1}+R_{2}\right)\right]$. The gate voltage of $M_{1}$ is equal to $V_{\text {out }} R_{1} /\left(R_{1}+R_{2}\right)$, leading to

$$
\begin{equation*}
T_{1}=g_{m 1} R_{D} \frac{g_{m 2}\left[R_{S} \|\left(R_{1}+R_{2}\right)\right]}{1+g_{m 2}\left[R_{S} \|\left(R_{1}+R_{2}\right)\right]} \frac{R_{1}}{R_{1}+R_{2}} \tag{8.215}
\end{equation*}
$$

We must now substitute for $H_{\infty}, T$, and $H_{0}$ in Eq. (8.212) to obtain the closed-loop gain—a laborious task left for the reader. This example suggests that the direct analysis of the circuit (without knowledge of feedback) may in fact be simpler in some cases, as is true for this circuit.

It is instructive to repeat the foregoing calculations if $M_{2}$ is the dependent source of interest. For $g_{m 2}=0, V_{\text {in }}$ is simply divided according to

$$
\begin{equation*}
H_{0}=\frac{R_{S}}{R_{S}+R_{1}+R_{2}} \tag{8.216}
\end{equation*}
$$

For $g_{m 2}=\infty$, we have $V_{G S 2}=0, V_{X}=V_{\text {out }}$, and hence a current of $-V_{\text {out }} / R_{D}$ flowing through $M_{1}$. It follows that $V_{G S 1}=-V_{\text {out }} /\left(g_{m 1} R_{D}\right)$ and $\left[V_{\text {in }}+V_{\text {out }} /\left(g_{m 1} R_{D}\right)\right] / R_{1}=\left[-V_{\text {out }} /\left(g_{m 1} R_{D}\right)-V_{\text {out }}\right] / R_{2}$. We therefore have

$$
\begin{equation*}
H_{\infty}=\frac{-g_{m 1} R_{2} R_{D}}{R_{1}+R_{2}+g_{m 1} R_{1} R_{D}} \tag{8.217}
\end{equation*}
$$

This result is also expected if we consider $M_{2}$ an ideal unity-gain buffer (due to its infinite $g_{m}$ ) and redraw the circuit as shown in Fig. 8.92(c).

The return ratio for $M_{2}$ can be found as

$$
\begin{equation*}
T_{2}=\frac{g_{m 2} R_{S}\left(g_{m 1} R_{1} R_{D}+R_{1}+R_{2}\right)}{R_{S}+R_{1}+R_{2}} \tag{8.218}
\end{equation*}
$$

Again, these values must be substituted in (8.212) to compute the closed-loop gain.

Double-Null Method Blackman's impedance theorem raises an interesting question: Can we write the transfer function of a circuit in a form similar to $A\left(1+T_{s c}\right) /\left(1+T_{o c}\right)$ ? In other words, can we generalize the result to a case in which $I_{i n}$ is replaced by an arbitrary input and $V_{i n}$ by an arbitrary output? To understand the rationale for this question, let us observe that (1) $T_{o c}$ is the return ratio with $I_{i n}=0$, i.e., $T_{o c}$ denotes the RR with the input set to zero in Fig. 8.76(a); and (2) $T_{s c}$ is the RR with $V_{i n}=0$, i.e., $T_{s c}$ represents the return ratio with the output forced to zero. Figure 8.93 conceptually illustrates the setups for these two measurements, with one "nulling" the input and the other, the output. We make a slight change in our notation and postulate that the transfer function of a given circuit can be written as

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=A \frac{1+T_{\text {out }, 0}}{1+T_{\text {in }, 0}} \tag{8.219}
\end{equation*}
$$

where $A=V_{\text {out }} / V_{\text {in }}$ with the dependent source set to zero, and $T_{\text {out }, 0}$ and $T_{\text {in }, 0}$ respectively denote the return ratios for $V_{\text {out }}=0$ and $V_{\text {in }}=0$.
image_name:(a)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: VDD, Nn: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: GND}
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
]
extrainfo:The diagram illustrates two configurations for calculating return ratios Tin,0 and Tout,0. In configuration (a), the input is shorted for Tin,0 calculation. In configuration (b), Vout is set to 0 for Tout,0 calculation.
image_name:(b)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: Vin, Nn: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: GND, Nn: Vout}
]
extrainfo:The circuit illustrates the concept of return ratios T_out,0 with V_out set to zero. It includes a voltage source V1 and a current source I1.

Figure 8.93 Conceptual illustration of $T_{\text {in }, 0}$ and $T_{\text {out }, 0}$.
The proof of (8.219) is similar to that of Blackman's theorem. Beginning from

$$
\begin{align*}
V_{\text {out }} & =A V_{\text {in }}+B I_{1}  \tag{8.220}\\
V_{1} & =C V_{\text {in }}+D I_{1} \tag{8.221}
\end{align*}
$$

we recognize that, if $V_{\text {in }}=0$, then $V_{1} / I_{1}=D$, and hence $T_{i n, 0}=-g_{m} D$. On the other hand, if $V_{\text {out }}=0$, then $V_{\text {in }}=(-B / A) I_{1}$, and hence $V_{1} / I_{1}=(A D-B C) / A$, i.e., $T_{\text {out }, 0}=-g_{m}(A D-B C) / A$. Combining these results indeed yields (8.219). Note that division by $A$ in these calculations assumes that $A \neq 0$, a critical point revisited below.

Equation (8.219) offers interesting insights. The quantity $T_{\text {out }, 0}$ reveals that, even though $V_{\text {in }}$ and $I_{1}$ are chosen so as to drive $V_{\text {out }}$ to zero, there is still an "internal" feedback loop emanating from $I_{1}$ and producing a finite value for $V_{1}$. The generic system of Fig. 8.1, on the other hand, does not lend itself to this perspective because its feedback network, $G(s)$, directly senses the output. The following example illustrates this point.

Example 8.33
Determine $V_{\text {out }} / V_{\text {in }}$ in Fig. 8.94(a), assuming $\lambda=\gamma=0$. Note that the feedback network does not sense the main output here.

#### Solution

If $M_{1}$ is the dependent source of interest and $g_{m 1}=0$, then the voltage at the source of $M_{2}$ is equal to $V_{i n}\left(R_{S} \| g_{m 2}^{-1}\right) /$ $\left(R_{S} \| g_{m 2}^{-1}+R_{1}+R_{2}\right)$, yielding

$$
\begin{equation*}
A=g_{m 2} R_{D 2} \frac{R_{S} \| g_{m 2}^{-1}}{R_{S} \| g_{m 2}^{-1}+R_{1}+R_{2}} \tag{8.222}
\end{equation*}
$$

image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1, G: g1}
name: M2, type: NMOS, ports: {S: s2, D: Vout, G: d1}
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: g1}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: d1}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: Vout}
name: R2, type: Resistor, value: R2, ports: {N1: g1, N2: s2}
name: RS, type: Resistor, value: RS, ports: {N1: s2, N2: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: g2, Nn: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: g2, Nn: X1}
]
extrainfo:The circuit consists of a two-stage amplifier with NMOS transistors M1 and M2. Resistors R1, R2, RD1, RD2, and RS are used for biasing and load. The input is applied at Vin, and the output is taken from Vout. The circuit is powered by VDD.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: x1, G: Vin}
name: M2, type: NMOS, ports: {S: x1, D: d2, G: g2}
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: x1}
name: RD1, type: Resistor, value: RD1, ports: {N1: d2, N2: VDD}
name: RD2, type: Resistor, value: RD2, ports: {N1: d2, N2: 0}
name: R2, type: Resistor, value: R2, ports: {N1: x1, N2: GND}
name: RS, type: Resistor, value: RS, ports: {N1: x1, N2: GND}
name: S2, type: Resistor, value: S2, ports: {N1: x1, N2: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: GND, Nn: x1}
name: V1, type: VoltageSource, value: V1, ports: {Np: x1, Nn: GND}
]
extrainfo:The circuit is a feedback network with NMOS transistors M1 and M2. It includes resistors R1, RD1, RD2, R2, RS, and S2, as well as a current source I1 and a voltage source V1. The feedback network does not sense the main output.

Figure 8.94

To obtain $T_{\text {out }, 0}$, we choose $V_{\text {in }}$ and $I_{1}$ so as to produce $V_{\text {out }}=0$, and hence $V_{G S 2}=0$ and $I_{D 2}=0$ [Fig. 8.94(b)]. The source voltage of $M_{2}$ is therefore equal to $-I_{1} R_{D 1}$ and also equal to $V_{i n} R_{S} /\left(R_{1}+R_{2}+R_{S}\right)$. Similarly, $V_{1}=V_{i n}\left(R_{2}+R_{S}\right) /\left(R_{1}+R_{2}+R_{S}\right)$ and

$$
\begin{align*}
T_{\text {out }, 0} & =-g_{m 1} \frac{V_{1}}{I_{1}}  \tag{8.223}\\
& =g_{m 1} R_{D 1} \frac{R_{2}+R_{S}}{R_{S}} \tag{8.224}
\end{align*}
$$

The nonzero $T_{\text {out }, 0}$ implies that $I_{1}$ still controls $V_{1}$ through an internal loop even though $V_{\text {out }}=0$. The loop gain with $V_{i n}=0$ is given by Eq. (8.215).

What if $M_{2}$ is the dependent source of interest? Then, for $g_{m 2}=0$, we have $V_{\text {out }}=0$, and hence $A=0$. Equation (8.219) thus fails to hold because its derivation has assumed that $A \neq 0$. This shortcoming of the double-null method manifests itself in many CMOS circuits, even in a simple degenerated common-source stage.
