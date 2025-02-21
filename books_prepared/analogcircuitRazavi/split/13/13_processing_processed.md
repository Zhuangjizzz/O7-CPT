# Feedback

Feedback is an integral part of our lives. Try touching your fingertips together with your eyes closed; you may not succeed the first time because you have broken a feedback loop that ordinarily "regulates" your motions. The regulatory role of feedback manifests itself in biological, mechanical, and electronic systems, allowing precise realization of "functions." For example, an amplifier targeting a precise gain of 2.00 is designed much more easily with feedback than without.

This chapter deals with the fundamentals of (negative) feedback and its application to electronic circuits. The outline is shown below.

General Considerations

- Elements of Feedback Systems
- Loop Gain
- Properties of Negative Feedback

Amplifiers and Sense/Return
Methods
- Types of Amplifiers
- Amplifier Models
- Sense/Return Methods
- Polarity of Feedback

## 12.1 GENERAL CONSIDERATIONS

As soon as he reaches the age of 18 , John eagerly obtains his driver's license, buys a used car, and begins to drive. Upon his parents' stern advice, John continues to observe the speed limit while noting that every other car on the highway drives faster. He then reasons that the speed limit is more of a "recommendation" and exceeding it by a small amount would not be harmful. Over the ensuing months, John gradually raises his speed so as to catch up with the rest of the drivers on the road, only to see flashing lights in his rear-view mirror one day. He pulls over to the shoulder of the road, listens to the sermon given by the police officer, receives a speeding ticket, and, dreading his parents' reaction, drives home-now strictly adhering to the speed limit.
image_name:Figure 12.1 General feedback system
description:The diagram represents a general feedback system, showcasing the essential components and flow of information in a negative feedback loop.

1. **Main Components:**
- **Comparison Mechanism:** This is represented by a summing junction that takes two inputs: the reference input \( X \) and the feedback signal \( X_F \). The difference between these two signals is computed and sent forward.
- **Feedforward System (\( A_1 \)):** This is the primary system block that processes the input signal from the comparison mechanism. It is typically responsible for the main action or output generation in the system.
- **Sense Mechanism:** This component measures the output \( Y \) of the feedforward system and sends it to the feedback network.
- **Feedback Network (\( K \)):** This block processes the output signal \( Y \) to generate the feedback signal \( X_F \), which is fed back to the comparison mechanism.

2. **Flow of Information or Control:**
- The reference input \( X \) is fed into the comparison mechanism, where it is compared with the feedback signal \( X_F \). The resulting error signal is sent to the feedforward system \( A_1 \).
- The feedforward system processes this error signal and produces the output \( Y \).
- The output \( Y \) is sensed and sent to the feedback network.
- The feedback network processes \( Y \) to produce the feedback signal \( X_F \), which is then looped back to the comparison mechanism.

3. **Labels, Annotations, and Key Indicators:**
- The diagram is labeled with key components such as "Comparison Mechanism," "Feedforward System," "Sense Mechanism," and "Feedback Network."
- The signals are labeled as \( X \) (input), \( Y \) (output), and \( X_F \) (feedback signal).
- The feedback network is denoted by a gain \( K \), indicating the amplification or attenuation applied to the output signal before it is fed back.

4. **Overall System Function:**
- The primary function of this system is to regulate the output \( Y \) by using feedback to minimize the difference between the reference input \( X \) and the actual output. This is achieved through the negative feedback loop, where the feedback network modifies the output signal and feeds it back to the comparison mechanism to adjust the system's performance. This setup helps maintain stability and desired performance by correcting deviations from the set point.

Figure 12.1 General feedback system.

John's story exemplifies the "regulatory" or "corrective" role of negative feedback. Without the police officer's involvement, John would probably continue to drive increasingly faster, eventually becoming a menace on the road.

Shown in Fig. 12.1, a negative feedback system consists of four essential components. (1) The "feedforward" system: ${ }^{1}$ the main system, probably "wild" and poorly controlled. John, the gas pedal, and the car form the feedforward system, where the input is the amount of pressure that John applies to the gas pedal and the output is the speed of the car. (2) Output sense mechanism: a means of measuring the output. The police officer's radar serves this purpose here. (3) Feedback network: a network that generates a "feedback signal," $X_{F}$, from the sensed output. The police officer acts as the feedback network by reading the radar display, walking to John's car, and giving him a speeding ticket. The quantity $K=X_{F} / Y$ is called the "feedback factor." (4) Comparison or return mechanism: a means of subtracting the feedback signal from the input to obtain the "error," $E=X-X_{F}$. John makes this comparison himself, applying less pressure to the gas pedal-at least for a while.

The feedback in Fig. 12.1 is called "negative" because $X_{F}$ is subtracted from $X$. Positive feedback, too, finds application in circuits such as oscillators and digital latches. If $K=0$, i.e., no signal is fed back, then we obtain the "open-loop" system. If $K \neq 0$, we say the system operates in the "closed-loop" mode. As seen throughout this chapter, analysis of a feedback system requires expressing the closed-loop parameters in terms of the open-loop parameters. Note that the input port of the feedback network refers to that sensing the output of the forward system.

As our first step towards understanding the feedback system of Fig. 12.1, let us determine the closed-loop transfer function $Y / X$. Since $X_{F}=K Y$, the error produced by the subtractor is equal to $X-K Y$, which serves as the input of the forward system:

$$
\begin{equation*}
(X-K Y) A_{1}=Y \tag{12.1}
\end{equation*}
$$

That is,

$$
\begin{equation*}
\frac{Y}{X}=\frac{A_{1}}{1+K A_{1}} . \tag{12.2}
\end{equation*}
$$

This equation plays a central role in our treatment of feedback, revealing that negative feedback reduces the gain from $A_{1}$ (for the open-loop system) to $A_{1} /\left(1+K A_{1}\right)$.

[^11]The quantity $A_{1} /\left(1+K A_{1}\right)$ is called the "closed-loop gain." Why do we deliberately lower the gain of the circuit? As explained in Section 12.2, the benefits accruing from negative feedback very well justify this reduction of the gain.

Example 12.1

Analyze the noninverting amplifier of Fig. 12.2 from a feedback point of view.
image_name:Figure 12.2
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: X, InN: XF, OutP: Y, OutN:}
name: R1, type: Resistor, value: R1, ports: {N1: Y, N2: XF}
name: R2, type: Resistor, value: R2, ports: {N1: XF, N2: GND}
]
extrainfo:The circuit is a non-inverting amplifier using an op-amp with feedback resistors R1 and R2. The feedback network provides a feedback factor K = R2 / (R1 + R2). The closed-loop gain is given by A1 / (1 + K * A1).

Solution The op amp $A_{1}$ performs two functions: subtraction of $X$ and $X_{F}$ and amplification. The network $R_{1}$ and $R_{2}$ also performs two functions: sensing the output voltage and providing a feedback factor of $K=R_{2} /\left(R_{1}+R_{2}\right)$. Thus, Eq. (12.2) gives

$$
\begin{equation*}
\frac{Y}{X}=\frac{A_{1}}{1+\frac{R_{2}}{R_{1}+R_{2}} A_{1}} \tag{12.3}
\end{equation*}
$$

which is identical to the result obtained in Chapter 8.

Exercise $\quad$ Perform the above analysis if $R_{2}=\infty$.

It is instructive to compute the error, $E$, produced by the subtractor. Since $E=X-X_{F}$ and $X_{F}=K A_{1} E$,

$$
\begin{equation*}
E=\frac{X}{1+K A_{1}} \tag{12.4}
\end{equation*}
$$

suggesting that the difference between the feedback signal and the input diminishes as $K A_{1}$ increases. In other words, the feedback signal becomes a close "replica" of the input (Fig. 12.3). This observation leads to a great deal of insight into the operation of feedback systems.
image_name:Figure 12.3
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: X, InN: XF, OutP: Out(A1), OutN:}
name: R1, type: Resistor, value: R1, ports: {N1: Out(A1), N2: XF}
name: R2, type: Resistor, value: R2, ports: {N1: XF, N2: GND}
]
extrainfo:The circuit is a feedback amplifier where the output is fed back to the inverting input through resistor R1 and R2. The feedback signal X_F is a close replica of the input X when the gain is high.

Figure 12.3 Feedback signal as a good replica of the input.

Example
12.2 $\begin{aligned} & \text { Explain why in the circuit of Fig. 12.2, } Y / X \text { approaches } 1+R_{1} / R_{2} \text { as }\left[R_{2} /\left(R_{1}+R_{2}\right)\right] A_{1} \\ & \text { becomes much greater than unity. }\end{aligned}$ becomes much greater than unity.

Solution If $K A_{1}=\left[R_{2} /\left(R_{1}+R_{2}\right)\right] A_{1}$ is large, $X_{F}$ becomes almost identical to $X$, i.e., $X_{F} \approx X$. The voltage divider therefore requires that

$$
\begin{equation*}
Y \frac{R_{2}}{R_{1}+R_{2}} \approx X \tag{12.5}
\end{equation*}
$$

and hence

$$
\begin{equation*}
\frac{Y}{X} \approx 1+\frac{R_{1}}{R_{2}} \tag{12.6}
\end{equation*}
$$

Of course, Eq. (12.3) yields the same result if $\left[R_{2} /\left(R_{1}+R_{2}\right)\right] A_{1} \gg 1$.
Exercise $\quad$ Repeat the above example if $R_{2}=\infty$.

### 12.1.1 Loop Gain

In Fig. 12.1, the quantity $K A_{1}$, which is equal to product of the gain of the forward system and the feedback factor, determines many properties of the overall system. Called the "loop gain," $K A_{1}$ has an interesting interpretation. Let us set the input $X$ to zero and "break" the loop at an arbitrary point, e.g., as depicted in Fig. 12.4(a).
image_name:Fig. 12.4 (a)
description:The block diagram labeled (a) represents a feedback control system with the following components:

1. **Main Components:**
- **Summing Junction:** This is depicted as a circle with a plus and minus sign, indicating a subtractor. It takes two inputs: one from the ground (GND) and another from the feedback path, and outputs their difference.
- **Amplifier A1:** This block represents the forward gain of the system. It takes the output from the summing junction and amplifies it.
- **Feedback Path with Gain K:** The output of the amplifier A1 is fed back through a block labeled "K," which represents the feedback gain.

2. **Flow of Information or Control:**
- The input to the system is set to zero (grounded), and the control loop is broken at point M.
- The output from the amplifier A1 is directed to point N, and simultaneously, it is fed back through the feedback path.
- The feedback path includes a gain block "K," which sends the signal back to the summing junction. This creates a feedback loop that influences the input to the amplifier A1.

3. **Labels, Annotations, and Key Indicators:**
- Points M and N are labeled as key reference points for analyzing the system.
- The feedback loop is indicated by the path from N through K back to the summing junction.
- The input to the amplifier A1 is labeled as "In(A1)," and the output is labeled as "Out(K)."

4. **Overall System Function:**
- The primary function of this system is to model the feedback control loop, which is a common configuration in control systems to stabilize or control the behavior of the system. By breaking the loop at M, one can analyze the loop gain and understand how the feedback affects the overall system performance.
image_name:Fig. 12.4(b)
description:The system block diagram labeled "(b)" represents a feedback loop used to compute the loop gain in a control system. The diagram includes the following main components:

1. **Summing Junction**: This is depicted as a circle with a plus and minus sign. It combines the input signals, subtracting the feedback signal from the test signal \( V_{\text{test}} \). The output of this summing junction is fed into the amplifier \( A_1 \).

2. **Amplifier \( A_1 \)**: This block represents a forward gain stage. It takes the input from the summing junction and amplifies it. The output of \( A_1 \) is labeled \( V_N \), representing the node where the feedback loop is observed.

3. **Feedback Path**: The output \( V_N \) is fed back through a feedback network characterized by a gain \( K \). This feedback path is essential for determining the loop gain. The feedback signal is subtracted from the test signal at the summing junction.

4. **Test Signal Source**: \( V_{\text{test}} \) is applied as an input to the system to evaluate the loop gain. This is represented by a voltage source connected to the input of the feedback network.

**Flow of Information**:
- The test signal \( V_{\text{test}} \) is introduced into the system at the summing junction.
- The summing junction subtracts the feedback signal (amplified by \( K \)) from \( V_{\text{test}} \), and the resultant signal is passed to amplifier \( A_1 \).
- The output from \( A_1 \) is \( V_N \), which is then fed back through the feedback network with gain \( K \) to complete the loop.

**Labels and Annotations**:
- The diagram includes labels such as \( V_N \), \( V_{\text{test}} \), and \( GND \) for ground connections.
- The feedback path is labeled with gain \( K \), indicating its role in the feedback loop.

**Overall System Function**:
The primary function of this system is to determine the loop gain by introducing a test signal and observing the behavior of the feedback loop. The arrangement of the summing junction, amplifier, and feedback path allows for the analysis of how the system responds to changes in the loop, which is crucial for understanding the stability and performance of the control system. The loop gain is a key parameter in assessing the system's ability to maintain desired performance in the presence of disturbances or changes in input conditions.

Figure 12.4 Computation of the loop gain by (a) breaking the loop and (b) applying a test signal.
The resulting topology can be viewed as a system with an input $M$ and an output $N$. Now, as shown in Fig. 12.4(b), let us apply a test signal at $M$ and follow it through the feedback network, the subtractor, and the forward system to obtain the signal at $N .^{2}$ The input of $A_{1}$ is equal to $-K V_{\text {test }}$, yielding

$$
\begin{equation*}
V_{N}=-K V_{\text {test }} A_{1} \tag{12.7}
\end{equation*}
$$

and hence

$$
\begin{equation*}
K A_{1}=-\frac{V_{N}}{V_{\text {test }}} \tag{12.8}
\end{equation*}
$$

In other words, if a signal "goes around the loop," it experiences a gain equal to $-K A_{1}$; hence the term "loop gain." It is important not to confuse the closed-loop gain, $A_{1} /\left(1+K A_{1}\right)$, with the loop gain, $K A_{1}$.

[^12]Example Compute the loop gain of the feedback system of Fig. 12.1 by breaking the loop at the 12.3 input of $A_{1}$.

Solution Illustrated in Fig. 12.5 is the system with the test signal applied to the input of $A_{1}$. The output of the feedback network is equal to $K A_{1} V_{\text {test }}$, yielding

$$
\begin{equation*}
V_{N}=-K A_{1} V_{\text {test }} \tag{12.9}
\end{equation*}
$$

and hence the same result as in Eq. (12.8).
image_name:Figure 12.5
description:The system block diagram in Figure 12.5 represents a feedback control system with several key components and signal paths.

1. **Main Components**:
- **Subtractor**: This component is located at the beginning of the diagram. It takes two inputs, one from the ground and another from the feedback path, and outputs the difference. This output is labeled as \( V_N \).
- **Amplifier \( A_1 \)**: Positioned after the test voltage source \( V_{\text{test}} \), this block amplifies the input signal it receives.
- **Feedback Gain Block \( K \)**: This block represents the feedback gain applied to the output signal. It is connected in the feedback loop to control the system's response.
- **Test Voltage Source \( V_{\text{test}} \)**: This is used to apply a test signal to the system at point \( M \).

2. **Flow of Information or Control**:
- The system starts at the subtractor, which calculates the difference between the input and feedback signal, producing \( V_N \).
- \( V_N \) is then fed into the feedback path, going through the gain block \( K \), which scales the signal.
- After passing through \( K \), the signal moves towards the test voltage source \( V_{\text{test}} \) at point \( M \), where it is combined with the test signal.
- This combined signal is fed into the amplifier \( A_1 \), which amplifies it.
- The amplified output is then directed towards the output \( Y \), completing the signal path.
- The output \( Y \) is also fed back into the subtractor to form a closed feedback loop.

3. **Labels, Annotations, and Key Indicators**:
- The diagram includes labels such as \( V_N \), \( V_{\text{test}} \), \( A_1 \), \( K \), and \( Y \) to indicate the various signals and components.
- Ground symbols are used to denote reference points for voltage levels.

4. **Overall System Function**:
- The primary function of this system is to demonstrate a feedback control mechanism, where the output is fed back to the input to maintain control over the system's behavior. The loop gain is analyzed by breaking the loop at the input of the subtractor, allowing for the calculation of the feedback effect on the overall system performance. The test voltage \( V_{\text{test}} \) is used to probe the system's response and calculate the loop gain.

Figure 12.5
Exercise Compute the loop gain by breaking the loop at the input of the subtractor.

The reader may wonder if an ambiguity exists with respect to the direction of the signal flow in the loop gain test. For example, can we modify the topology of Fig. 12.4(b) as shown in Fig. 12.6? This would mean applying $V_{\text {test }}$ to the output of $A_{1}$ and expecting to observe a signal at its input and eventually at $N$. While possibly yielding a finite value, such a test does not represent the actual behavior of the circuit. In the feedback system, the signal flows from the input of $A_{1}$ to its output and from the input of the feedback network to its output.

Did you know?

Negative feedback is a common phenomenon in nature. When you enter a bright room, your brain commands your pupils to become smaller. If you listen to very loud music for several hours, you feel hard of hearing afterwards because your ear has adjusted your hearing threshold in response to the volume. And if you try writing with your eyes closed, your handwriting will not be good because the feedback loop monitoring your pen strokes is broken.
image_name:Figure 12.6 Incorrect method of applying test signal.
description:The diagram labeled 'Figure 12.6 Incorrect method of applying test signal' illustrates a feedback system with several key components and signal paths.

1. **Main Components:**
- **Summing Junction (+):** This is where the input signal 'X' and the feedback signal are combined. The summing junction outputs the difference between these signals.
- **Amplifier (A1):** This block receives the output from the summing junction. It amplifies the signal with a gain that is indicated as 'In(A1)'.
- **Feedback Path:** After amplification, the signal is fed back to the summing junction. This feedback is essential for controlling the system's behavior.
- **Test Voltage Source (Vtest):** Positioned at the output of the amplifier, this source is incorrectly placed for applying a test signal. It is connected to ground (GND) and introduces a test voltage 'Vtest' into the circuit.
- **Feedback Amplifier (K):** This component is part of the feedback loop, receiving the output from the amplifier 'A1' and feeding back a portion of the signal to the summing junction. It has a gain factor 'K'.
- **Output (Out(K)):** The output of the feedback amplifier 'K' is labeled as 'Out(k)', which is fed back to the summing junction.

2. **Flow of Information or Control:**
- The input signal 'X' enters the summing junction where it is combined with the feedback signal. The difference is sent to the amplifier 'A1'.
- The amplified signal is then split. One path leads to the test voltage source 'Vtest', and the other path leads to the feedback amplifier 'K'.
- The feedback amplifier processes the signal and sends it back to the summing junction, completing the feedback loop.

3. **Labels, Annotations, and Key Indicators:**
- 'In(A1)' indicates the input to the amplifier 'A1'.
- 'Vtest' is the test voltage applied at the output, which is incorrectly placed in this configuration.
- 'Out(k)' is the output from the feedback amplifier 'K'.
- 'VN' is a reference voltage connected to ground, labeled at the feedback amplifier.

4. **Overall System Function:**
- The primary function of this system is to control the output through negative feedback. However, the placement of the test voltage 'Vtest' at the amplifier's output is incorrect, as it disrupts the intended feedback loop. The system aims to stabilize the gain despite variations in the amplifier 'A1', but the test signal's incorrect application may lead to inaccurate results or instability.

Figure 12.6 Incorrect method of applying test signal.

## 12.2 PROPERTIES OF NEGATIVE FEEDBACK

### 12.2.1 Gain Desensitization

Suppose $A_{1}$ in Fig. 12.1 is an amplifier whose gain is poorly controlled. For example, a CS stage provides a voltage gain of $g_{m} R_{D}$ while both $g_{m}$ and $R_{D}$ vary with process and temperature; the gain thus may vary by as much as $\pm 20 \%$. Also, suppose we require a voltage gain of $4.00 .^{3}$ How can we achieve such precision? Equation (12.2) points to a potential solution: if $K A_{1} \gg 1$, we have

$$
\begin{equation*}
\frac{Y}{X} \approx \frac{1}{K} \tag{12.10}
\end{equation*}
$$

a quantity independent of $A_{1}$. From another perspective, Eq. (12.4) indicates that $K A_{1} \gg 1$ leads to a small error, forcing $X_{F}$ to be nearly equal to $X$ and hence $Y$ nearly equal to $X / K$. Thus, if $K$ can be defined precisely, then $A_{1}$ impacts $Y / X$ negligibly and a high precision in the gain is attained. The circuit of Fig. 12.2 exemplifies this concept very well. If $A_{1} R_{2} /\left(R_{1}+R_{2}\right) \gg 1$, then

$$
\begin{align*}
\frac{Y}{X} & \approx \frac{1}{K}  \tag{12.11}\\
& \approx 1+\frac{R_{1}}{R_{2}} \tag{12.12}
\end{align*}
$$

Why is $R_{1} / R_{2}$ more precisely defined than $g_{m} R_{D}$ is? If $R_{1}$ and $R_{2}$ are made of the same material and constructed identically, then the variation of their value with process and temperature does not affect their ratio. As an example, for a closed-loop gain of 4.00, we choose $R_{1}=3 R_{2}$ and implement $R_{1}$ as the series combination of three "unit" resistors equal to $R_{2}$. Illustrated in Fig. 12.7, the idea is to ensure that $R_{1}$ and $R_{2}$ "track" each other; if $R_{2}$ increases by $20 \%$, so does each unit in $R_{1}$ and hence the total value of $R_{1}$, still yielding a gain of $1+1.2 R_{1} /\left(1.2 R_{2}\right)=4$.
image_name:Figure 12.7
description:The image labeled as "Figure 12.7" illustrates a configuration of resistors designed for good matching in a circuit. The diagram shows a series of four rectangular resistor components. Three of these components are connected in series to form the resistor labeled as \( R_1 \), while a single resistor is labeled as \( R_2 \). Each resistor is depicted as a block with two connection points, indicating the flow of current through them.

**1. Identification of Components and Structure:**
- The structure consists of four resistors, each represented as a block with two terminals.
- Three resistors are connected in series to form \( R_1 \), while the fourth is \( R_2 \).

**2. Connections and Interactions:**
- The resistors forming \( R_1 \) are connected end-to-end, indicating a series connection. This configuration ensures that the total resistance of \( R_1 \) is three times that of a single unit resistor, which matches the description that \( R_1 = 3R_2 \).
- The current flows sequentially through the resistors in \( R_1 \) and separately through \( R_2 \).

**3. Labels, Annotations, and Key Features:**
- The diagram is annotated with labels \( R_1 \) and \( R_2 \) to indicate the grouping of resistors.
- The arrangement is designed to ensure that if the value of \( R_2 \) changes due to external factors like temperature, the value of \( R_1 \) will change proportionally, maintaining the desired ratio for stable circuit performance.

Figure 12.7 Construction of resistors for good matching.

The circuit of Fig. 12.2 is designed for a nominal gain of 4. (a) Determine the actual gain 12.4 if $A_{1}=1000$. (b) Determine the percentage change in the gain if $A_{1}$ drops to 500.

Solution For a nominal gain of 4 , Eq. (12.12) implies that $R_{1} / R_{2}=3$. (a) The actual gain is given by

$$
\begin{align*}
\frac{Y}{X} & =\frac{A_{1}}{1+K A_{1}}  \tag{12.13}\\
& =3.984 . \tag{12.14}
\end{align*}
$$

[^13]Note that the loop gain $K A_{1}=1000 / 4=250$. (b) If $A_{1}$ falls to 500 , then

$$
\begin{equation*}
\frac{Y}{X}=3.968 \tag{12.15}
\end{equation*}
$$

Thus, the closed-loop gain changes by only $(3.984 / 3.968) / 3.984=0.4 \%$ if $A_{1}$ drops by factor of 2 .

Exercise Determine the percentage change in the gain if $A_{1}$ falls to 200.

The above example reveals that the closed-loop gain of a feedback circuit becomes relatively independent of the open-loop gain so long as the loop gain, $K A_{1}$, remains sufficiently higher than unity. This property of negative feedback is called "gain desensitization."

We now see why we are willing to accept a reduction in the gain by a factor of $1+K A_{1}$. We begin with an amplifier having a high, but poorly-controlled gain and apply negative feedback around it so as to obtain a better-defined, but inevitably lower gain. This concept was also extensively employed in the op amp circuits described in Chapter 8.

The gain desensitization property of negative feedback means that any factor that influences the open-loop gain has less effect on the closed-loop gain. Thus far, we have blamed only process and temperature variations, but many other phenomena change the gain as well.

- As the signal frequency rises, $A_{1}$ may fall, but $A_{1} /\left(1+K A_{1}\right)$ remains relatively constant. We therefore expect that negative feedback increases the bandwidth (at the cost of gain).
- If the load resistance changes, $A_{1}$ may change; e.g., the gain of a CS stage depends on the load resistance. Negative feedback, on the other hand, makes the gain less sensitive to load variations.
- The signal amplitude affects $A_{1}$ because the forward amplifier suffers from nonlinearity. For example, the large-signal analysis of differential pairs in Chapter 10 reveals that the small-signal gain falls at large input amplitudes. With negative feedback, however, the variation of the open-loop gain due to nonlinearity manifests itself to a lesser extent in the closed-loop characteristics. That is, negative feedback improves the linearity.

We now study these properties in greater detail.

### 12.2.2 Bandwidth Extension

Let us consider a one-pole open-loop amplifier with a transfer function

$$
\begin{equation*}
A_{1}(s)=\frac{A_{0}}{1+\frac{s}{\omega_{0}}} \tag{12.16}
\end{equation*}
$$

Here, $A_{0}$ denotes the low-frequency gain and $\omega_{0}$ the -3 dB bandwidth. Noting from Eq. (12.2) that negative feedback lowers the low-frequency gain by a factor of $1+K A_{1}$, we wish to determine the resulting bandwidth improvement. The closed-loop transfer
function is obtained by substituting Eq. (12.16) for $A_{1}$ in Eq. (12.2):

$$
\begin{equation*}
\frac{Y}{X}=\frac{\frac{A_{0}}{1+\frac{s}{\omega_{0}}}}{1+K \frac{A_{0}}{1+\frac{s}{\omega_{0}}}} \tag{12.17}
\end{equation*}
$$

Multiplying the numerator and the denominator by $1+s / \omega_{0}$ gives

$$
\begin{align*}
\frac{Y}{X}(s) & =\frac{A_{0}}{1+K A_{0}+\frac{s}{\omega_{0}}}  \tag{12.18}\\
& =\frac{\frac{A_{0}}{1+K A_{0}}}{1+\frac{s}{\left(1+K A_{0}\right) \omega_{0}}} \tag{12.19}
\end{align*}
$$

In analogy with Eq. (12.16), we conclude that the closed-loop system now exhibits:

$$
\begin{align*}
\text { Closed-Loop Gain } & =\frac{A_{0}}{1+K A_{0}}  \tag{12.20}\\
\text { Closed-Loop Bandwidth } & =\left(1+K A_{0}\right) \omega_{0} \tag{12.21}
\end{align*}
$$

In other words, the gain and bandwidth are scaled by the same factor but in opposite directions, displaying a constant product.

Example Plot the closed-loop frequency response given by Eq. (12.19) for $K=0,0.1$, and 0.5 . 12.5 Assume $A_{0}=200$.

Solution For $K=0$, the feedback vanishes and $Y / X$ reduces to $A_{1}(s)$ as given by Eq. (12.16). For $K=0.1$, we have $1+K A_{0}=21$, noting that the gain decreases and the bandwidth increases by the same factor. Similarly, for $K=0.5,1+K A_{0}=101$, yielding a proportional reduction in gain and increase in bandwidth. The results are plotted in Fig. 12.8.
image_name:Figure 12.8
description:**Type of Graph and Function:**
The graph is a Bode plot representing the closed-loop frequency response of a system. It shows the magnitude response as a function of frequency for different feedback gain values, \( K \).

**Axes Labels and Units:**
- The vertical axis represents the gain, denoted as \( A_0 \), which is dimensionless.
- The horizontal axis represents frequency, denoted by \( \omega \), typically in radians per second.
- The scale appears to be linear for both axes.

**Overall Behavior and Trends:**
The plot shows three curves, each corresponding to different values of the feedback gain \( K \): 0, 0.1, and 0.5. For \( K = 0 \), the gain starts at \( A_0 \) and remains constant over a range of frequencies before decreasing sharply. For \( K = 0.1 \), the initial gain is lower, and the bandwidth is wider compared to \( K = 0 \). For \( K = 0.5 \), the initial gain is even lower, and the bandwidth is the widest among the three.

**Key Features and Technical Details:**
- The gain for \( K = 0 \) starts at the maximum value \( A_0 \) and decreases sharply after a certain frequency, indicating a narrow bandwidth.
- As \( K \) increases to 0.1 and 0.5, the initial gain decreases proportionally, but the bandwidth increases, showing a trade-off between gain and bandwidth.
- The plot demonstrates the effect of feedback on the system's frequency response, with higher \( K \) values reducing gain but increasing bandwidth.

**Annotations and Specific Data Points:**
- The curves are labeled with their respective \( K \) values: \( K = 0 \), \( K = 0.1 \), and \( K = 0.5 \).
- No specific numerical values for cutoff frequencies or other critical points are provided in the graph itself, but the trend of decreasing gain and increasing bandwidth with higher \( K \) is clear.

Figure 12.8

Exercise Repeat the above example for $K=1$.

Example Prove that the unity-gain bandwidth of the above system remains independent of $K$ if 12.6 $1+K A_{0} \gg 1$ and $K^{2} \ll 1$.

Solution The magnitude of Eq. (12.19) is equal to

$$
\begin{equation*}
\left|\frac{Y}{X}(j \omega)\right|=\frac{\frac{A_{0}}{1+K A_{0}}}{\sqrt{1+\frac{\omega^{2}}{\left(1+K A_{0}\right)^{2} \omega_{0}^{2}}}} \tag{12.22}
\end{equation*}
$$

Equating this result to unity and squaring both sides, we write

$$
\begin{equation*}
\left(\frac{A_{0}}{1+K A_{0}}\right)^{2}=1+\frac{\omega_{u}^{2}}{\left(1+K A_{0}\right)^{2} \omega_{0}^{2}} \tag{12.23}
\end{equation*}
$$

where $\omega_{u}$ denotes the unity-gain bandwidth. It follows that

$$
\begin{align*}
\omega_{u} & =\omega_{0} \sqrt{A_{0}^{2}-\left(1+K A_{0}\right)^{2}}  \tag{12.24}\\
& \approx \omega_{0} \sqrt{A_{0}^{2}-K^{2} A_{0}^{2}}  \tag{12.25}\\
& \approx \omega_{0} A_{0} \tag{12.26}
\end{align*}
$$

which is equal to the gain-bandwidth product of the open-loop system. Figure 12.9 depicts the results.
image_name:Figure 12.9
description:The graph depicted in Figure 12.9 is a Bode plot representing the frequency response of an open-loop system. The vertical axis is labeled in decibels (dB) and represents the gain, while the horizontal axis is labeled with angular frequency (ω) and is likely on a logarithmic scale.

Axes Labels and Units:
- **Vertical Axis:** Gain in dB
- **Horizontal Axis:** Frequency (ω), with significant points labeled as ω₀ and A₀ω₀.

Overall Behavior and Trends:
- The plot shows two curves indicating different gain responses.
- Both curves start at a high gain level, A₀, at low frequencies.
- At the frequency ω₀, marked by a vertical dashed line, the gain begins to decrease.
- The gain continues to decrease with frequency, reaching 0 dB at A₀ω₀.

Key Features and Technical Details:
- **Initial Gain Level:** Both curves start at A₀, indicating the initial gain level before the roll-off.
- **Cutoff Frequency:** The frequency ω₀ is a significant point where the gain starts to drop.
- **Unity-Gain Bandwidth:** The point where the gain reaches 0 dB is at A₀ω₀, indicating the unity-gain bandwidth.

Annotations and Specific Data Points:
- The graph highlights the transition from high gain to unity gain, showing the effect of frequency on the system's gain.
- The dashed line at ω₀ serves as a marker for the initial decrease in gain.

Figure 12.9

Exercise If $A_{0}=1000, \omega_{0}=2 \pi \times(10 \mathrm{MHz})$, and $K=0.5$, calculate the unity-gain bandwidth from Eqs. (12.24) and (12.26) and compare the results.

### 12.2.3 Modification of I/O Impedances

As mentioned above, negative feedback makes the closed-loop gain less sensitive to the load resistance. This effect fundamentally arises from the modification of the output impedance as a result of feedback. Feedback modifies the input impedance as well. We will formulate these effects carefully in the following sections, but it is instructive to study an example at this point.

Example
12.7

Figure 12.10 depicts a transistor-level realization of the feedback circuit shown in Fig. 12.2. Assume $\lambda=0$ and $R_{1}+R_{2} \gg R_{D}$ for simplicity. (a) Identify the four components of the feedback system. (b) Determine the open-loop and closed-loop voltage gain. (c) Determine the open-loop and closed-loop I/O impedances.
image_name:Figure 12.10
description:
[
name: M1, type: NMOS, ports: {S: Vin, D: Vout, G: g1}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: g1}
name: R2, type: Resistor, value: R2, ports: {N1: g1, N2: GND}
]
extrainfo:The circuit is a feedback amplifier with NMOS transistor M1 and resistors RD, R1, and R2. Vout is the output node, and Vin is the input node. R1 and R2 form a voltage divider feedback network.

Figure 12.10
Solution
(a) In analogy with Fig. 12.10, we surmise that the forward system (the main amplifier) consists of $M_{1}$ and $R_{D}$, i.e., a common-gate stage. Resistors $R_{1}$ and $R_{2}$ serve as both the sense mechanism and the feedback network, returning a signal equal to $V_{\text {out }} R_{2} /\left(R_{1}+R_{2}\right)$ to the subtractor. Transistor $M_{1}$ itself operates as the subtractor because the smallsignal drain current is proportional to the difference between the gate and source voltages:

$$
\begin{equation*}
i_{D}=g_{m}\left(v_{G}-v_{S}\right) \tag{12.27}
\end{equation*}
$$

(b) The forward system provides a voltage gain equal to

$$
\begin{equation*}
A_{0} \approx g_{m} R_{D} \tag{12.28}
\end{equation*}
$$

because $R_{1}+R_{2}$ is large enough that its loading on $R_{D}$ can be neglected. The closed-loop voltage gain is thus given by

$$
\begin{align*}
\frac{v_{\text {out }}}{v_{\text {in }}} & =\frac{A_{0}}{1+K A_{0}}  \tag{12.29}\\
& =\frac{g_{m} R_{D}}{1+\frac{R_{2}}{R_{1}+R_{2}} g_{m} R_{D}} \tag{12.30}
\end{align*}
$$

We should note that the overall gain of this stage can also be obtained by simply solving the circuit's equations-as if we know nothing about feedback. However, the use of feedback concepts both provides a great deal of insight and simplifies the task as circuits become more complex.
(c) The open-loop I/O impedances are those of the CG stage:

$$
\begin{align*}
R_{i n, \text { open }} & =\frac{1}{g_{m}}  \tag{12.31}\\
R_{\text {out }, \text { open }} & =R_{D} \tag{12.32}
\end{align*}
$$

At this point, we do not know how to obtain the closed-loop I/O impedances in terms of the open-loop parameters. We therefore simply solve the circuit. From Fig. 12.11(a), we recognize that $R_{D}$ carries a current approximately equal to $i_{X}$ because $R_{1}+R_{2}$ is assumed large. The drain voltage of $M_{1}$ is thus given by $i_{X} R_{D}$,
leading to a gate voltage equal to $+i_{X} R_{D} R_{2} /\left(R_{1}+R_{2}\right)$. Transistor $M_{1}$ generates a drain current proportional to $v_{G S}$ :

$$
\begin{align*}
i_{D} & =g_{m} v_{G S}  \tag{12.33}\\
& =g_{m}\left(\frac{+i_{X} R_{D} R_{2}}{R_{1}+R_{2}}-v_{X}\right) \tag{12.34}
\end{align*}
$$

Since $i_{D}=-i_{X}$, Eq. (12.34) yields

$$
\begin{equation*}
\frac{v_{X}}{i_{X}}=\frac{1}{g_{m}}\left(1+\frac{R_{2}}{R_{1}+R_{2}} g_{m} R_{D}\right) . \tag{12.35}
\end{equation*}
$$

That is, the input resistance increases from $1 / g_{m}$ by a factor equal to $1+$ $g_{m} R_{D} R_{2} /\left(R_{1}+R_{2}\right)$, the same factor by which the gain decreases.
image_name:Figure 12.11 (a)
description:
[
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: d1}
name: R1, type: Resistor, value: R1, ports: {N1: g1, N2: d1}
name: R2, type: Resistor, value: R2, ports: {N1: g1, N2: GND}
name: M1, type: NMOS, ports: {S: Vx, D: d1, G: g1}
name: Vx, type: VoltageSource, value: vx, ports: {Np: Vx, Nn: GND}
]
extrainfo:The circuit is a common-source NMOS amplifier with resistive load RD and a voltage divider bias network R1 and R2. The input voltage is Vx and the output is taken from the drain of M1.

image_name:Figure 12.11(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vx, G: g1}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vx}
name: R1, type: Resistor, value: R1, ports: {N1: g1, N2: Vx}
name: R2, type: Resistor, value: R2, ports: {N1: g1, N2: GND}
name: Vx, type: VoltageSource, value: vx, ports: {Np: Vx, Nn: GND}
]
extrainfo:The circuit is a common-source NMOS amplifier with a resistive load RD and a voltage divider bias network consisting of R1 and R2. The input voltage is Vx, and the output is taken from the drain of M1. The circuit also includes a voltage-controlled current source g1.

To determine the output resistance, we write from Fig. 12.11(b),

$$
\begin{equation*}
v_{G S}=\frac{R_{2}}{R_{1}+R_{2}} v_{X} \tag{12.36}
\end{equation*}
$$

and hence

$$
\begin{align*}
i_{D} & =g_{m} v_{G S}  \tag{12.37}\\
& =g_{m} \frac{R_{2}}{R_{1}+R_{2}} v_{X} \tag{12.38}
\end{align*}
$$

Noting that, if $R_{1}+R_{2} \gg R_{D}$, then $i_{X} \approx i_{D}+v_{X} / R_{D}$, we obtain

$$
\begin{equation*}
i_{X} \approx g_{m} \frac{R_{2}}{R_{1}+R_{2}} v_{X}+\frac{v_{X}}{R_{D}} . \tag{12.39}
\end{equation*}
$$

It follows that

$$
\begin{equation*}
\frac{v_{X}}{i_{X}}=\frac{R_{D}}{1+\frac{R_{2}}{R_{1}+R_{2}} g_{m} R_{D}} \tag{12.40}
\end{equation*}
$$

The output resistance thus decreases by the "universal" factor $1+g_{m} R_{D} R_{2} /\left(R_{1}+R_{2}\right)$.

The above computation of I/O impedances can be greatly simplified if feedback concepts are employed. As exemplified by Eqs. (12.35) and (12.40), the factor $1+K A_{0}=1+g_{m} R_{D} R_{2} /\left(R_{1}+R_{2}\right)$ plays a central role here. Our treatment of feedback circuits in this chapter will provide the foundation for this point.

Exercise In some applications, the input and output impedances of an amplifier must both be equal to $50 \Omega$. What relationship guarantees that the input and output impedances of the above circuit are equal?

The reader may raise several questions at this point. Do the input impedance and the output impedance always scale down and up, respectively? Is the modification of I/O impedances by feedback desirable? We consider one example here to illustrate a point and defer more rigorous answers to subsequent sections.
$\begin{array}{cl}\text { Example } & \begin{array}{l}\text { The common-gate stage of Fig. } 12.10 \text { must drive a load resistance } \\ \text { does the gain change (a) without feedback, (b) with feedback? }\end{array}\end{array}$ does the gain change (a) without feedback, (b) with feedback?

Solution (a) Without feedback [Fig. 12.12(a)], the CG gain is equal to $g_{m}\left(R_{D} \| R_{L}\right)=g_{m} R_{D} / 3$. That is, the gain drops by factor of three.
image_name:Figure 12.12
description:
[
name: M1, type: NMOS, ports: {S: Vin, D: Vout, G: Vb}
name: RD, type: Resistor, value: RD, ports: {N1: Vout, N2: VDD}
name: RL, type: Resistor, value: RD/2, ports: {N1: Vout, N2: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:This is a common-gate amplifier circuit with an NMOS transistor M1. The circuit is powered by a voltage source VDD and includes load resistors RD and RL. The output voltage Vout is taken across RL.

(b) With feedback, we use Eq. (12.30) but recognize that the open-loop gain has fallen to $g_{m} R_{D} / 3$ :

$$
\begin{align*}
\frac{v_{\text {out }}}{v_{\text {in }}} & =\frac{g_{m} R_{D} / 3}{1+\frac{R_{2}}{R_{1}+R_{2}} g_{m} R_{D} / 3}  \tag{12.41}\\
& =\frac{g_{m} R_{D}}{3+\frac{R_{2}}{R_{1}+R_{2}} g_{m} R_{D}} \tag{12.42}
\end{align*}
$$

For example, if $g_{m} R_{D} R_{2} /\left(R_{1}+R_{2}\right)=10$, then this result differs from the "unloaded" gain expression in Eq. (12.30) by about $18 \%$. Feedback therefore desensitizes the gain to load variations.

Exercise $\quad$ Repeat the above example for $R_{L}=R_{D}$.
image_name:Figure 12.13 (a)
description:**Type of Graph and Function:**
Figure 12.13 (a) shows a nonlinear open-loop characteristic of an amplifier. It is a plot of the output signal \( y \) versus the input signal \( x \).

**Axes Labels and Units:**
- **X-axis:** Represents the input signal \( x \).
- **Y-axis:** Represents the output signal \( y \).

**Overall Behavior and Trends:**
The graph depicts a nonlinear relationship between the input and output signals. It starts at the origin and curves upwards, indicating that the gain changes with different input levels. The curve is concave down, showing diminishing returns in output as input increases.

**Key Features and Technical Details:**
- The slope of the curve at different points represents the small-signal gain of the amplifier.
- At \( x_1 \), the gain is denoted as \( A_1 \), and at \( x_2 \), the gain is \( A_2 \).
- The curve indicates a decrease in gain as the input level increases from \( x_1 \) to \( x_2 \).

**Annotations and Specific Data Points:**
- Dotted lines are used to mark the points \( x_1 \) and \( x_2 \) on the x-axis and their corresponding output levels on the y-axis.
- The gains \( A_1 \) and \( A_2 \) are shown as the slopes of the tangent lines at \( x_1 \) and \( x_2 \), respectively.

This graph illustrates the nonlinearity in the amplifier's response, which can be improved by introducing feedback, as suggested by the context and the accompanying figure (b).
image_name:Figure 12.13 (b)
description:Figure 12.13(b) illustrates the improvement in linearity of an amplifier due to feedback. The graph is a plot of input \(x\) versus output \(y\), showing two characteristics: open-loop and closed-loop.

1. **Type of Graph and Function:**
- The graph is a characteristic curve showing the relationship between input and output of an amplifier.
- It demonstrates how feedback affects the linearity of the amplifier's response.

2. **Axes Labels and Units:**
- The horizontal axis represents the input \(x\), while the vertical axis represents the output \(y\).
- No specific units are given, indicating a general characteristic analysis.

3. **Overall Behavior and Trends:**
- The open-loop characteristic (shown in a lighter curve) is nonlinear, with a decreasing slope as \(x\) increases, indicating decreasing gain.
- The closed-loop characteristic (shown in a darker curve) is more linear, with a reduced slope compared to the open-loop, indicating a more consistent gain across the input range.

4. **Key Features and Technical Details:**
- The open-loop gain at point \(x_1\) is \(A_1\) and at \(x_2\) is \(A_2\), showing variability in gain.
- The closed-loop gain is reduced to \(\frac{A_1}{1 + KA_1}\) at \(x_1\) and \(\frac{A_2}{1 + KA_2}\) at \(x_2\), where \(K\) is the feedback factor. This reduction in gain variability illustrates the stabilizing effect of feedback.

5. **Annotations and Specific Data Points:**
- The graph is annotated with gain values for both open-loop and closed-loop conditions at specific input points \(x_1\) and \(x_2\).
- The labels clearly indicate the improvement in linearity and the effect of feedback on the gain values.

Figure 12.13 (a) Nonlinear open-loop characteristic of an amplifier, (b) improvement in linearity due to feedback.

### 12.2.4 Linearity Improvement

Consider a system having the input/output characteristic shown in Fig. 12.13(a). The nonlinearity observed here can also be viewed as the variation of the slope of the characteristic, i.e., the small-signal gain. For example, this system exhibits a gain of $A_{1}$ near $x=x_{1}$ and $A_{2}$ near $x=x_{2}$. If placed in a negative-feedback loop, the system provides a more uniform gain for different signal levels and, therefore, operates more linearly. In fact, as illustrated in Fig. 12.13(b) for the closed-loop system, we can write

$$
\text { Gain at } \begin{align*}
x_{1} & =\frac{A_{1}}{1+K A_{1}}  \tag{12.43}\\
& \approx \frac{1}{K}\left(1-\frac{1}{K A_{1}}\right) \tag{12.44}
\end{align*}
$$

where it is assumed $K A_{1} \gg 1$. Similarly,

$$
\text { Gain at } \begin{align*}
x_{2} & =\frac{A_{2}}{1+K A_{2}}  \tag{12.45}\\
& \approx \frac{1}{K}\left(1-\frac{1}{K A_{2}}\right) \tag{12.46}
\end{align*}
$$

Thus, so long as $K A_{1}$ and $K A_{2}$ are large, the variation of the closed-loop gain with the signal level remains much less than that of the open-loop gain.

All of the above attributes of negative feedback can also be considered a result of the minimal error property illustrated in Fig. 12.3. For example, if at different signal levels, the forward amplifier's gain varies,

Amplifier driving a speaker (a) without, and (b) with feedback.
the feedback still ensures the feedback signal is a close replica of the input, and so is the output.

## 12.3 TYPES OF AMPLIFIERS

The amplifiers studied thus far in this book sense and produce voltages. While less intuitive, other types of amplifiers also exist, i.e., those that sense and/or produce currents. Figure 12.14 depicts the four possible combinations along with their input and output impedances in the ideal case. For example, a circuit sensing a current must display a low input impedance to resemble a current meter. Similarly, a circuit generating an output current must achieve a high output impedance to approximate a current source. The reader is encouraged to confirm the other cases as well. The distinction among the four types of amplifiers becomes important in the analysis of feedback circuits. Note that the "current-voltage" and "voltagecurrent" amplifiers of Figs. 12.14(b) and (c) are commonly known as "transimpedance" and "transconductance" amplifiers, respectively.
image_name:Figure 12.14 (a)
description:The circuit diagram (a) represents a voltage amplifier with infinite input impedance and zero output impedance. The voltage source Vin is connected to the input of the operational amplifier A0, and the output is taken at Vout. The configuration ensures that the amplifier does not load the preceding stage and provides an ideal voltage gain.
image_name:Figure 12.14 (b)
description:The circuit in diagram (b) represents a transimpedance amplifier. It features a voltage-controlled voltage source (R0) and a current source (Iin) with zero input resistance and output resistance. The input is connected to node X, and the output is at Vout.
image_name:Figure 12.14(c)
description:The circuit in diagram (c) represents a transconductance amplifier. It converts an input voltage (Vin) to an output current (Iout). The input impedance is infinite, and the output impedance is zero.
image_name:Figure 12.14(d)
description:The circuit represents a current amplifier with an input current source (Iin) and an operational amplifier (AI) providing an output current (Iout). The circuit is designed with an infinite output impedance (Rout = ∞) and zero input impedance (Rin = 0).

Figure 12.14 (a) Voltage, (b) transimpedance, (c) transconductance, and (d) current amplifiers.

### 12.3.1 Simple Amplifier Models

For our studies later in this chapter, it is beneficial to develop simple models for the four amplifier types. Depicted in Fig. 12.15 are the models for the ideal case. The voltage amplifier in Fig. 12.15(a) provides an infinite input impedance so that it can sense voltages as an ideal voltmeter, i.e., without loading the preceding stage. Also, the circuit exhibits a
image_name:Figure 12.15(a)
description:This circuit diagram represents a voltage amplifier with a voltage-controlled voltage source A0. The input voltage is Vin, and the output voltage is Vout. The amplifier has an infinite input impedance and is grounded at the negative terminal.
image_name:Figure 12.15(b)
description:The circuit is a transimpedance amplifier where the input current (iin) is converted to an output voltage (Vout) by the transimpedance gain R0.
image_name:Figure 12.15(c)
description:This is a transconductance amplifier circuit where the input voltage 'Vin' controls the output current 'i_out'. The transconductance is represented by 'Gm'. The load is connected to the output current 'i_out'.
image_name:Figure 12.15(d)
description:The circuit diagram (d) represents a current amplifier model where the output current (i_out) is controlled by the input current (i_in). The current-controlled current source A1 amplifies the input current i_in to produce the output current i_out. The load is connected to the output current path.

Figure 12.15 Ideal models for (a) voltage, (b) transimpedance, (c) transconductance, and (d) current amplifiers.
image_name:Figure 12.16 (a)
description:The circuit diagram represents a voltage amplifier model. The input voltage Vin is applied across the resistor Rin, and the amplified output voltage A0*Vin is generated across the op-amp A0, with the output Vout across the resistor Rout.

image_name:Figure 12.16(b)
description:The circuit diagram represents an incorrect voltage amplifier model. The input voltage Vin is applied across the resistor Rin, and a voltage-controlled current source Gmv_in is used. The output is taken across the resistor Rout.


image_name:Figure 12.16 (c)
description:The circuit diagram represents a realistic model of a current amplifier. The input current i_in flows through the resistor Rin, and the voltage-controlled voltage source R0i_in is used. The output is taken across the resistor Rout.

image_name:Figure 12.16(d)
description:The circuit diagram represents a realistic model of a current amplifier. The input current i_in flows through the resistor Rin, and the current-controlled current source A is used. The output is taken across the resistor Rout.

Figure 12.16 (a) Realistic model of voltage amplifier, (b) incorrect voltage amplifier model, (c) realistic model of transimpedance amplifier, (d) incorrect model of transimpedance amplifier, (e) realistic model of transconductance amplifier, (f) realistic model of current amplifier.
zero output impedance so as to serve as an ideal voltage source, i.e., deliver $v_{\text {out }}=A_{0} v_{\text {in }}$ regardless of the load impedance.

The transimpedance amplifier in Fig. 12.15(b) has a zero input impedance so that it can measure currents as an ideal current meter. Similar to the voltage amplifier, the output impedance is also zero if the circuit operates as an ideal voltage source. Note that the "transimpedance gain" of this amplifier, $R_{0}=v_{\text {out }} / i_{\text {in }}$, has a dimension of resistance. For example, a transimpedance gain of $2 \mathrm{k} \Omega$ means a 1-mA change in the input current leads to a 2-V change at the output.

The I/O impedances of the topologies in Figs. 12.15(c) and (d) follow similar observations. It is worth noting that the amplifier of Fig. 12.15(c) has a "transconductance gain," $G_{m}=i_{\text {out }} / v_{\text {in }}$, with a dimension of transconductance.

In reality, the ideal models in Fig. 12.15 may not be accurate. In particular, the I/O impedances may not be negligibly large or small. Figure 12.16 shows more realistic models of the four amplifier types. Illustrated in Fig. 12.16(a), the voltage amplifier model contains an input resistance in parallel with the input port and an output resistance in series with the output port. These choices are unique and become clearer if we attempt other combinations. For example, if we envision the model as shown in Fig. 12.16(b), then the input and output impedances remain equal to infinity and zero, respectively, regardless of the values of $R_{\text {in }}$ and $R_{\text {out }}$. (Why?) Thus, the topology of Fig. 12.16(a) serves as the only possible model representing finite I/O impedances.

Figure 12.16(c) depicts a nonideal transimpedance amplifier. Here, the input resistance appears in series with the input. Again, if we attempt a model such as that in Fig. 12.16(d), the input resistance is zero. The other two amplifier models in Figs. 12.16(e) and (f) follow similar concepts.

### 12.3.2 Examples of Amplifier Types

It is instructive to study examples of the above four types. Figure 12.17(a) shows a cascade of a CS stage and a source follower as a "voltage amplifier." The circuit indeed provides a high input impedance (similar to a voltmeter) and a low output impedance (similar to a voltage source). Figure 12.17(b) depicts a cascade of a CG stage and a source follower as a transimpedance amplifier. Such a circuit displays low input and output impedances to serve as a "current sensor" and a "voltage generator." Figure 12.17(c) illustrates a single
image_name:Figure 12.17(a)
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: d1g2, G: Vin}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: d1g2}
name: M2, type: NMOS, ports: {S: d1g2, D: Vout, G: Vout}
name: VDD, type: VoltageSource, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a voltage amplifier with a cascade of a common-source stage and a source follower. It provides high input impedance and low output impedance.
image_name:Figure 12.17(b)
description:
[
name: M1, type: NMOS, ports: {S: s1, D: d1g2, G: Vb}
name: M2, type: NMOS, ports: {S:Vout, D: VDD, G: d1g2}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: d1g2}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: GND, Nn: s1}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a transimpedance amplifier with low input and output impedances, serving as a current sensor and voltage generator. The small-signal output resistance is 1/gm2, and the input resistance is 1/gm1.
image_name:Figure 12.17(c)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: LOAD, G: Vin}
]
extrainfo:The circuit in diagram (c) is a transconductance amplifier using a single NMOS transistor M1. It converts an input voltage (Vin) to an output current (Iout), with high input and output impedances. The output resistance is labeled as ro.
image_name:Figure 12.17(d)
description:
[
name: M1, type: NMOS, ports: {S: s1, D: LOAD, G: Vb}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: GND, Nn: s1}
]
extrainfo:The circuit is a common-gate current amplifier providing low input impedance and high output impedance. It uses an NMOS transistor M1 with a bias voltage Vb and an input current source Iin.

Figure 12.17 Examples of (a) voltage, (b) transimpedance, (c) transconductance, and (d) current amplifiers.

MOSFET as a transconductance amplifier. With high input and output impedances, the circuit efficiently senses voltages and generates currents. Finally, Fig. 12.17(d) shows a common-gate transistor as a current amplifier. Such a circuit must provide a low input impedance and a high output impedance.

Let us also determine the small-signal "gain" of each circuit in Fig. 12.17, assuming $\lambda=0$ for simplicity. The voltage gain, $A_{0}$, of the cascade in Fig. 12.17(a) is equal to $-g_{m} R_{D}$ if $\lambda=0 .{ }^{4}$ The gain of the circuit in Fig. 12.17(b) is defined as $v_{\text {out }} / i_{\text {in }}$, called the "transimpedance gain," and denoted by $R_{T}$. In this case, $i_{i n}$ flows through $M_{1}$ and $R_{D}$, generating a voltage equal to $i_{i n} R_{D}$ at both the drain of $M_{1}$ and the source of $M_{2}$. That is, $v_{\text {out }}=i_{\text {in }} R_{D}$ and hence $R_{T}=R_{D}$.

For the circuit in Fig. 12.17(c), the gain is defined as $i_{\text {out }} / v_{\text {in }}$, called the "transconductance gain," and denoted by $G_{m}$. In this example, $G_{m}=g_{m}$. For the current amplifier in Fig. 12.17(d), the current gain, $A_{I}$, is equal to unity because the input current simply flows to the output.

Example With a current gain of unity, the topology of Fig. 12.17(d) appears hardly better than a 12.9 piece of wire. What is the advantage of this circuit?

Solution The important property of this circuit lies in its input impedance. Suppose the current source serving as the input suffers from a large parasitic capacitance, $C_{p}$. If applied directly to a resistor $R_{D}$ [Fig. 12.18(a)], the current would be wasted

[^14]image_name:Fig. 12.18(a)
description:
[
name: I_in, type: CurrentSource, value: I_in, ports: {Np: GND, Nn: Vout}
name: C_P, type: Capacitor, value: C_P, ports: {Np: Vout, Nn: GND}
name: R_D, type: Resistor, value: R_D, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit consists of a current source, capacitor, and resistor all connected in parallel between the Vout node and ground.

image_name:Fig. 12.18(b)
description:
[
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: M1, type: NMOS, ports: {S: S1, D: Vout, G: Vb}
name: CP, type: Capacitor, value: CP, ports: {Np: S1, Nn: GND}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: GND, Nn: s1}
name: I1, type: CurrentSource, value: I1, ports: {Np: S1, Nn: GND}
]
extrainfo:The circuit includes a resistor RD connected from VDD to Vout, an NMOS transistor M1 with the source connected to node S1, the drain to Vout, and the gate to Vb. A capacitor CP and two current sources Iin and I1 are connected in parallel between node S1 and ground.

through $C_{p}$ at high frequencies, exhibiting a -3 dB bandwidth of only $\left(R_{D} C_{p}\right)^{-1}$. On the other hand, the use of a CG stage [Fig. 12.18(b)] moves the input pole to $g_{m} / C_{p}$, a much higher frequency.

Exercise Determine the transfer function $V_{\text {out }} / I_{\text {in }}$ for each of the above circuits.

## 12.4 SENSE AND RETURN TECHNIQUES

Recall from Section 12.1 that a feedback system includes means of sensing the output and "returning" the feedback signal to the input. In this section, we study such means so as to recognize them easily in a complex feedback circuit.

How do we measure the voltage across a port? We place a voltmeter in parallel with the port, and require that the voltmeter have a high input impedance so that it does not disturb the circuit [Fig. 12.19(a)]. By the same token, a feedback circuit sensing an output voltage must appear in parallel with the output and, ideally, exhibit an infinite impedance [Fig. 12.19(b)]. Shown in Fig. 12.19(c) is an example in which the resistive divider consisting of $R_{1}$ and $R_{2}$ senses the output voltage and generates the feedback signal, $v_{F}$. To approach the ideal case, $R_{1}+R_{2}$ must be very large so that $A_{1}$ does not "feel" the effect of the resistive divider.

How do we measure the current flowing through a wire? We break the wire and place a current meter in series with the wire [Fig. 12.20(a)]. The current meter in fact consists of a small resistor, so that it does not disturb the circuit, and a voltmeter that measures
image_name:Fig. 12.19(a)
description:The circuit is a feedback system with an operational amplifier A1. The output voltage Vout is sensed by a feedback network consisting of resistors R1 and R2, generating a feedback voltage VF. The input voltage is Vin.
image_name:(b)
description:The diagram labeled (b) represents a system with two main components: a Feedforward System and a Feedback Network, both of which are crucial for controlling and stabilizing the output voltage, \( V_{out} \).

Main Components:
1. **Feedforward System:**
- This block is responsible for processing the input signal and directly affecting the output, \( V_{out} \). It is designed to enhance the performance by anticipating changes and making adjustments to maintain the desired output.

2. **Feedback Network:**
- This block senses the output voltage and generates a feedback signal. The feedback is used to compare the actual output with the desired output, allowing for corrections to be made. This network ensures stability and accuracy by adjusting the system based on the feedback received.

Flow of Information or Control:
- **Signal Flow:**
- The input signal is processed by the Feedforward System, which influences the output, \( V_{out} \).
- The Feedback Network senses the \( V_{out} \) and sends a feedback signal back to the system.
- **Feedback Loop:**
- The feedback loop is crucial for stabilizing the system. It allows the system to self-correct by comparing the output with the desired value and making necessary adjustments.

Labels, Annotations, and Key Indicators:
- The diagram includes labels for the Feedforward System and Feedback Network.
- \( V_{out} \) is the primary output voltage that is being controlled and stabilized.
- The feedback path is indicated, showing its return to the system to influence control actions.

Overall System Function:
- The primary function of this system is to maintain a stable and accurate output voltage \( V_{out} \) by using both feedforward and feedback techniques. The feedforward system anticipates changes and adjusts accordingly, while the feedback network ensures stability by correcting any deviations from the desired output. Together, these components work to provide a robust and reliable control system for voltage regulation.
image_name:Fig. 12.19(c)
description:
[
name: A1, type: OpAmp, ports: {InP: Vin, InN: VF, OutP: Vout, OutN:}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: VF}
name: R2, type: Resistor, value: R2, ports: {N1: VF, N2: GND}
]
extrainfo:The circuit is a feedback network with an operational amplifier A1, sensing the output voltage Vout and generating a feedback signal VF through resistors R1 and R2.

Figure 12.19 (a) Sensing a voltage by a voltmeter, (b) sensing the output voltage by the feedback network, (d) example of implementation.
image_name:Figure 12.20(a)
description:The circuit (a) is a current sensing network using a current meter in series with a load resistor RL. The operational amplifier A1 and NMOS M1 form a feedback system that controls the voltage VF across RS to regulate the output current Iout.
image_name:Figure 12.20(b)
description:The circuit diagram (b) shows a voltmeter sensing the output voltage across a resistor RL with an internal resistance r. The operational amplifier A1 is used in a feedback configuration to control the NMOS transistor M1, which regulates the output current Iout. The feedback signal VF is generated across resistor RS.
image_name:Figure 12.20(c)
description:The system block diagram labeled (c) illustrates a feedback control system for sensing output current. This diagram consists of two main components: a Feedforward System and a Feedback Network.

1. **Main Components:**
- **Feedforward System:** This block is responsible for processing the input signal to produce an output current, denoted as \( I_{out} \). It serves as the primary path for the signal to reach the load.
- **Feedback Network:** This block is connected in parallel with the Feedforward System. It senses the output current and provides a feedback signal to ensure the system operates correctly.

2. **Flow of Information or Control:**
- The output current \( I_{out} \) flows from the Feedforward System towards the load.
- The Feedback Network senses a portion of this output current and generates a feedback signal that is fed back into the system to adjust the output as needed.
- The feedback loop is crucial for maintaining stability and accuracy in the system's output.

3. **Labels, Annotations, and Key Indicators:**
- The diagram includes arrows indicating the direction of current flow.
- The output current \( I_{out} \) is clearly labeled, providing a reference for understanding the flow of the signal through the system.

4. **Overall System Function:**
- The primary function of this system is to accurately control and stabilize the output current \( I_{out} \) delivered to a load. The Feedforward System generates the initial output, while the Feedback Network ensures that any deviations from the desired output are corrected. This arrangement allows for precise control of the output current, enhancing the system's performance and reliability.
image_name:Figure 12.20(d)
description:The circuit is a feedback network with an operational amplifier A1, sensing the output voltage at the load and generating a feedback signal VF through the resistors r and RS. The NMOS transistor M1 is used to control the current flowing through the load.

Figure 12.20 (a) Sensing a current by a current meter, (b) actual realization of current meter, (c) sensing the output current by the feedback network, (d) example of implementation.
the voltage drop across the resistor [Fig. 12.20(b)]. Thus, a feedback circuit sensing an output current must appear in series with the output and, ideally, exhibit a zero impedance [Fig. 12.20(c)]. Depicted in Fig. 12.20(d) is an implementation of this concept. A resistor placed in series with the source of $M_{1}$ senses the output current, generating a proportional feedback voltage, $V_{F}$. Ideally, $R_{S}$ is so small ( $\ll 1 / g_{m 1}$ ) that the operation of $M_{1}$ remains unaffected.

To return a voltage or current to the input, we must employ a mechanism for adding or subtracting such quantities. ${ }^{5}$ To add two voltage sources, we place them in series [Fig. 12.21(a)]. Thus, a feedback network returning a voltage must appear in series with the input signal [Fig. 12.21(b)], so that

$$
\begin{equation*}
v_{e}=v_{i n}-v_{F} \tag{12.47}
\end{equation*}
$$

For example, as shown in Fig. 12.21(c), a differential pair can subtract the feedback voltage from the input. Alternatively, as mentioned in Example 12.7, a single transistor can operate as a voltage subtractor [Fig. 12.21(d)].

To add two current sources, we place them in parallel [Fig. 12.22(a)]. Thus, a feedback network returning a current must appear in parallel with the input signal, Fig. 12.22(b), so that

$$
\begin{equation*}
i_{e}=i_{i n}-i_{F} \tag{12.48}
\end{equation*}
$$

For example, a transistor can return a current to the input [Fig. 12.22(c)]. So can a resistor if it is large enough to approximate a current source [Fig. 12.22(d)].

[^15]image_name:Figure 12.21(a)
description:The circuit adds two voltage sources V1 and V2 in series, with nodes labeled X1, X2, and X3.
image_name:Figure 12.21(b)
description:The system block diagram labeled as "(b)" illustrates a feedback control system with two main components: a Feedforward System and a Feedback Network.

1. **Main Components:**
- **Feedforward System:** This block processes the input signal directly and contributes to the overall system output.
- **Feedback Network:** This block takes a portion of the output and feeds it back to the input, creating a closed-loop system.

2. **Flow of Information or Control:**
- The input voltage \(v_{in}\) enters the system and is split into two paths. One path goes directly into the Feedforward System, while the other path is involved in the feedback loop.
- The output of the Feedforward System is denoted as \(v_{e}\), which is compared with the feedback voltage \(v_{F}\) to generate an error signal.
- The Feedback Network takes the output voltage \(v_{F}\) and feeds it back to the input, where it is subtracted from \(v_{in}\) to produce the error signal at node \(x_3\).

3. **Labels, Annotations, and Key Indicators:**
- The diagram shows key nodes \(x_1\), \(x_2\), and \(x_3\), where \(x_3\) is the node where the input and feedback signals are combined.
- The feedback voltage \(v_{F}\) is shown being subtracted from the input at node \(x_3\).

4. **Overall System Function:**
- The primary function of this system is to maintain control over the output by adjusting the input signal based on the feedback received. This setup allows for error correction, where any deviation in the output can be corrected by the feedback mechanism. The combination of feedforward and feedback paths ensures that the system can respond dynamically to changes in input or external disturbances, enhancing stability and performance.
image_name:Figure 12.21(c)
description:The circuit diagram (c) illustrates a differential pair using NMOS transistors M1 and M2 with a diode S1S2, acting as a voltage subtractor. The input voltage Vin is applied to the gate of M1, and the feedback voltage VF is applied to the gate of M2. The diode is connected to the common source node of M1 and M2, providing a path to ground.
image_name:Figure 12.21(d)
description:The circuit diagram (d) shows a single NMOS transistor used as a voltage subtractor. The input voltage is applied to the gate of the NMOS, and the output is taken from the drain, which connects to the load.

Figure 12.21 (a) Addition of two voltages, (b) addition of feedback and input voltages, (c) differential pair as a voltage subtractor, (d) single transistor as a voltage subtractor.
image_name:Figure 12.22 (a)
description:The circuit diagram shows two current sources, i1 and i2, connected in parallel between nodes X2 and X1. This configuration results in the addition of the currents from i1 and i2 at the node X2, with the combined current flowing towards node X1.

image_name:Figure 12.22 (b)
description:The diagram labeled "Figure 12.22 (b)" illustrates a system with both feedforward and feedback components designed to manage and process electrical currents.

Main Components:
1. **Current Source (i_in):**
- Provides an input current to the system.

2. **Feedforward System:**
- Receives a portion of the input current labeled as `i_e` after a split at node `X2`.
- Processes this current to achieve a certain desired output or effect without waiting for feedback.

3. **Feedback Network:**
- Receives a feedback current labeled as `i_F` from node `X1`.
- This network is responsible for adjusting the system's operation based on the output, maintaining stability or improving performance.

Flow of Information or Control:
- The input current `i_in` enters the system and splits at node `X1`.
- A portion of this current, `i_F`, is directed to the Feedback Network.
- The remaining current continues to node `X2`, where it becomes `i_e` and enters the Feedforward System.
- The Feedback Network processes `i_F` and provides necessary feedback to adjust the system's behavior, typically by influencing the input or the feedforward path.

Labels, Annotations, and Key Indicators:
- **Nodes `X1` and `X2`:** Indicate points where the current splits or is directed to different parts of the system.
- **Currents `i_e` and `i_F`:** Label the specific currents entering the Feedforward System and Feedback Network, respectively.

Overall System Function:
The primary function of this system is to manage the input current `i_in` through a combination of feedforward processing and feedback correction. The feedforward component processes the current to achieve a desired output directly, while the feedback network ensures the system remains stable and performs optimally by adjusting the input or processing path based on the feedback current `i_F`. This combination allows for improved control and precision in current management.

image_name:Figure 12.22(d)
description:
[
name: Iin, type: CurrentSource, value: Iin, ports: {Np: GND, Nn:In(Ao)}
name: RF, type: Resistor, value: RF, ports: {N1: In(Ao), N2: LOAD}
name: A0, type: OpAmp, value: A0, ports: {InP: In, InN: GND, OutP: Out}
]
extrainfo:This circuit is a non-inverting amplifier with feedback. The input current 'i_in' is fed into the op-amp 'A0'. The feedback current 'i_F' flows through the resistor 'RF', stabilizing the system by adjusting the input path. The output is connected to a load.

Figure 12.22 (a) Addition of two currents, (b) addition of feedback current and input current, (c) circuit realization, (d) another realization.

Example 12.10

Determine the types of sensed and returned signals in the circuit of Fig. 12.23.
image_name:Figure 12.23
description:
[
name: M1, type: NMOS, ports: {S: S1S2, D: d1g3d3, G: Vin}
name: M2, type: NMOS, ports: {S: S1S2, D: Vout, G: VF}
name: M3, type: PMOS, ports: {S: VDD, D: d1g3d3, G: d1g3d3}
name: M4, type: PMOS, ports: {S: VDD, D: d1g3d3, G: d1g3d3}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: VF}
name: R2, type: Resistor, value: R2, ports: {N1: VF, N2: GND}
name: I_SS, type: CurrentSource, value: I_SS, ports: {Np: S1S2, Nn: GND}
]
extrainfo:The circuit is a non-inverting amplifier using a differential pair with an active load as the op-amp. The resistive divider senses the output voltage and provides feedback.

Figure 12.23

Solution This circuit is an implementation of the noninverting amplifier shown in Fig. 12.2. Here, the differential pair with the active load plays the role of an op amp. The resistive divider senses the output voltage and serves as the feedback network, producing $v_{F}=\left[R_{2} /\left(R_{1}+R_{2}\right)\right] v_{\text {but }}$. Also, $M_{1}$ and $M_{2}$ operate as both part of the op amp (the forward system) and a voltage subtractor. The amplifier therefore combines the topologies in Figs. 12.19(c) and 12.21(c).

Exercise $\quad$ Repeat the above example if $R_{2}=\infty$.
image_name:Fig. 12.24
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1g2, G: g1}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: d1g2}
name: MF, type: NMOS, ports: {S: GND, D: g1, G: Vout}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: d1g2}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: Vout}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: GND, Nn: g1}
]
extrainfo:The circuit is a differential pair with an active load acting as an op-amp. The feedback network is a resistive divider sensing the output voltage. The feedback factor is influenced by the transconductance of MF.

Solution Transistor $M_{F}$ both senses the output voltage and returns a current to the input. The feedback factor is thus given by

$$
\begin{equation*}
K=\frac{i_{F}}{v_{\text {out }}}=g_{m F} \tag{12.49}
\end{equation*}
$$

where $g_{m F}$ denotes the transconductance of $M_{F}$.

Exercise Calculate the feedback factor if $M_{F}$ is degenerated by a resistor of value $R_{S}$.

Let us summarize the properties of the "ideal" feedback network. As illustrated in Fig. 12.25(a), we expect such a network to exhibit an infinite input impedance if sensing a voltage and a zero input impedance if sensing a current. Moreover, the network must provide a zero output impedance if returning a voltage and an infinite output impedance if returning a current.

## 12.5 POLARITY OF FEEDBACK

While the block diagram of a feedback system, e.g., Fig. 12.1, readily reveals the polarity of feedback, an actual circuit implementation may not. The procedure of determining this polarity involves three steps: (a) assume the input signal goes up (or down); (b) follow the change through the forward amplifier and the feedback network; (c) determine whether the returned quantity opposes or enhances the original "effect" produced by the input change. A simpler procedure is as follows: (a) set the input to zero; (b) break the loop; (c) apply a test signal, $V_{\text {test }}$, travel around the loop, examine the returned signal, $V_{\text {ret }}$, and determine the polarity of $V_{\text {ret }} / V_{\text {test }}$.
image_name:Fig. 12.25(a)
description:Main Components:
1. **Amplifier (A₀):**
- This block represents an ideal amplifier with a gain of A₀. It is responsible for amplifying the input signal.
- There are two instances of this amplifier in the system.

2. **Feedback Network (K):**
- This is a feedback block with a gain of K. It is used to control the feedback loop in the system.
- The feedback network takes the output from the amplifier and feeds a portion of it back into the system.

3. **Input and Output Ports:**
- **V_in:** The input voltage signal to the system.
- **V_out:** The output voltage from the amplifier.
- **I_out:** The output current from the amplifier.

Flow of Information or Control:
- The input voltage signal **V_in** is fed into the amplifier A₀.
- The amplified output voltage **V_out** is produced by the amplifier.
- **V_out** is then fed into the feedback network K, which processes the signal and feeds it back into the system.
- The feedback loop is closed by feeding the processed signal back to the input of the amplifier, thereby influencing the input signal processing.
- The output current **I_out** is another output of the amplifier, indicating that the system can handle both voltage and current outputs.

Labels, Annotations, and Key Indicators:
- **A₀:** Indicates the gain of the amplifier.
- **K:** Represents the gain of the feedback network.
- Arrows indicate the direction of signal flow, showing the path from input to output and through the feedback loop.

Overall System Function:
The system is designed to amplify an input voltage signal while employing a feedback loop to control and stabilize the output. The feedback network ensures that any changes in the output are fed back into the system to maintain a desired level of amplification and stability. This configuration is typical in control systems where feedback is used to enhance performance and reduce errors in signal processing.
image_name:Fig. 12.25(b)
description:The block diagram labeled "(b)" represents the output impedance of an ideal feedback network for producing voltage and current quantities. The system comprises several key components:

1. **Input Source (V_in):**
- The input voltage source, denoted as \( V_{in} \), is applied to the system.

2. **Summing Junction:**
- The input voltage \( V_{in} \) is fed into a summing junction, which combines it with a feedback signal \( V_F \). The summing junction outputs the difference between \( V_{in} \) and \( V_F \).

3. **Forward Amplifier (A_0):**
- The output of the summing junction is fed into a forward amplifier \( A_0 \), which amplifies the difference signal.

4. **Feedback Path:**
- The output of the forward amplifier is connected to a feedback network. This network includes a current source and a feedback amplifier (K).
- The feedback amplifier \( K \) receives its input from the output of the forward amplifier and contributes to the feedback signal \( V_F \).

5. **Current Source and Ground Connection:**
- The feedback path includes a current source connected to ground, which influences the feedback current \( I_F \).

6. **Output Impedance Control:**
- The output impedance is controlled by the feedback network, which adjusts \( I_{out} \) based on the feedback loop.

7. **Output:**
- The system's output is represented by the current \( I_{out} \), which is influenced by the feedback and the forward amplification.

**Flow of Information:**
- The input voltage \( V_{in} \) is processed through the summing junction, where it is combined with the feedback voltage \( V_F \). The resultant signal is amplified by the forward amplifier \( A_0 \).
- The amplified signal is then used to generate a feedback current \( I_F \) through the feedback network, which includes a current source and feedback amplifier \( K \).
- The feedback loop ensures that the output current \( I_{out} \) is controlled, maintaining the desired output impedance characteristics.

**Overall System Function:**
- The primary function of this system is to control the output impedance through feedback mechanisms. The feedback network adjusts the output current based on the input voltage and the feedback signal, ensuring stable and precise output characteristics.

Figure 12.25 (a) Input impedance of ideal feedback networks for sensing voltage and current quantities, (b) output impedance of ideal feedback networks for producing voltage and current quantities.

Example Determine the polarity of feedback in the circuit of Fig. 12.26. <br> 12.12

image_name:Figure 12.26
description:
[
name: M1, type: NMOS, ports: {S: s1s2, D:d1d3g3 , G: Vin}
name: M2, type: NMOS, ports: {S: s1s2, D: Vout, G: X}
name: M3, type: PMOS, ports: {S: VDD, D: d1d3g3, G: d1d3g3}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: d1d3g3}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: X}
name: R2, type: Resistor, value: R2, ports: {N1: X, N2: GND}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: s1s2, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with NMOS and PMOS transistors. It uses a current source for biasing and feedback resistors for stability.


Solution If $V_{\text {in }}$ goes up, $I_{D 1}$ tends to increase and $I_{D 2}$ tends to decrease. As a result, $V_{o u t}$ and hence $V_{X}$ tend to rise. The rise in $V_{X}$ tends to increase $I_{D 2}$ and decrease $I_{D 1}$, counteracting the effect of the change in $V_{i n}$. The feedback is therefore negative. The reader is encouraged to apply the second procedure.

Exercise $\quad$ Suppose the top terminal of $R_{1}$ is tied to the drain of $M_{1}$ rather than the the drain of $M_{2}$. Determine the polarity of feedback.
image_name:Figure 12.27
description:
[
name: M1, type: NMOS, ports: {S: X, D: A, G: Vin}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: A}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: A}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: Vout}
name: RF1, type: Resistor, value: RF1, ports: {N1: Vout, N2: X}
name: RF2, type: Resistor, value: RF2, ports: {N1: X, N2: GND}
]
extrainfo:The circuit is designed to determine the polarity of feedback. It includes two NMOS transistors (M1 and M2), where M1 is controlled by the input voltage Vin, and M2 is part of the feedback loop. The resistors RD1 and RD2 are connected to the power supply VDD, and resistors RF1 and RF2 form a feedback network connected to the output Vout. The feedback is negative, as an increase in Vin results in a decrease in ID1 and an increase in ID2, opposing the change in Vin.

Figure 12.27

Solution If $V_{\text {in }}$ goes up, $I_{D 1}$ tends to increase. Thus, $V_{A}$ falls, $V_{o u t}$ rises, and so does $V_{X}$. The rise in $V_{X}$ tends to reduce $I_{D 1}$ (why?), thereby opposing the effect produced by $V_{i n}$. The feedback is therefore negative.

Exercise Repeat the above example if $M_{2}$ is converted to a CG stage, i.e., its source is tied to node $A$ and its gate to a bias voltage.
image_name:Fig. 12.28
description:
[
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: Vout}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: X}
name: M2, type: NMOS, ports: {S: GND, D: X, G: Vout}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: GND, Nn:X}
]
extrainfo:The circuit consists of two NMOS transistors M1 and M2, a resistor RD1 connected to VDD, and a current source Iin. The feedback in the circuit is positive, as an increase in input current Iin leads to an increase in VX, which further increases ID1 and decreases Vout.

Figure 12.28

Solution If $I_{\text {in }}$ goes up, $V_{X}$ tends to rise (why?), thus raising $I_{D 1}$. As a result, $V_{\text {out }}$ falls and $I_{D 2}$ decreases, allowing $V_{X}$ to rise (why?). Since the returned signal enhances the effect produced by $I_{i n}$, the polarity of feedback is positive.

Exercise Repeat the above example if $M_{2}$ is a PMOS device (still operating as a CS stage). What happens if $R_{D} \rightarrow \infty$ ? Is this result expected?

Did you know?

While we focus on negative feedback in this book, positive feedback also finds its own applications. Suppose, for example, that a new ice cream store adopts a unique recipe and begins to attract many customers. If the store now adds one more scoop to each ice cream for free, then it will draw even more customers. That is, the store owner is providing a feedback signal that enhances the customer response (positive feedback). On the other hand, if the owner is greedy and reduces the size of the ice cream, then the store loses customers (negative feedback).

## 12.6 FEEDBACK TOPOLOGIES

Our study of different types of amplifiers in Section 12.3 and sense and return mechanisms in Section 12.4 suggests that four feedback topologies can be constructed. Each topology includes one of four types of amplifiers as its forward system. The feedback network must, of course, sense and return quantities compatible with those produced and sensed by the forward system, respectively. For example, a voltage amplifier requires that the feedback network sense and return voltages, whereas a transimpedance amplifier must employ a feedback network that senses a voltage and returns a current. In this section, we study each topology and compute the closed-loop characteristics such as gain and I/O impedances with the assumption that the feedback network is ideal (Fig. 12.25).

### 12.6.1 Voltage-Voltage Feedback

Illustrated in Fig. 12.29(a), this topology incorporates a voltage amplifier, requiring that the feedback network sense the output voltage and return a voltage to the subtractor. Recall from Section 12.4 that such a feedback network appears in parallel with the output and in series with the input, ${ }^{6}$ ideally exhibiting an infinite input impedance and a zero output impedance.
image_name:Figure 12.29
description:The circuit is a voltage-voltage feedback topology with an ideal feedback network. It includes two operational amplifiers, A0 and K, where A0 amplifies the voltage difference between nodes X3 and X2, and K provides feedback from the output node X3 to the input node X2. The input is at node X1, and the output is at node X3. The feedback network ideally has infinite input impedance and zero output impedance.

Figure 12.29 Voltage-voltage feedback.

We first calculate the closed-loop gain. Since

$$
\begin{align*}
V_{1} & =V_{\text {in }}-V_{F}  \tag{12.50}\\
V_{\text {out }} & =A_{0} V_{1}  \tag{12.51}\\
V_{F} & =K V_{\text {out }}, \tag{12.52}
\end{align*}
$$

we have

$$
\begin{equation*}
V_{\text {out }}=A_{0}\left(V_{\text {in }}-K V_{\text {out }}\right) \tag{12.53}
\end{equation*}
$$

and hence

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=\frac{A_{0}}{1+K A_{0}} \tag{12.54}
\end{equation*}
$$

an expected result.

Determine the closed-loop gain of the circuit shown in Fig. 12.30, assuming $R_{1}+R_{2}$ is very large.
image_name:Figure 12.30
description:
[
name: M1, type: NMOS, ports: {S: S1S2, D: d1d3g3, G: Vin}
name: M2, type: NMOS, ports: {S: S1S2, D: Vout, G: VF}
name: M3, type: PMOS, ports: {S: VDD, D: d1d3g3, G: d1d3g3}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: d1d3g3}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: VF}
name: R2, type: Resistor, value: R2, ports: {N1: VF, N2: GND}
name: I_SS, type: CurrentSource, value: I_SS, ports: {Np: S1S2, Nn: GND}
]
extrainfo:The circuit employs a differential amplifier topology with NMOS and PMOS transistors, and includes negative voltage-voltage feedback. The resistive network senses Vout, feeding back a voltage to the gate of M2. The configuration is known as series-shunt feedback.

Figure 12.30
${ }^{6}$ For this reason, this type of feedback is also called the "series-shunt" topology, where the first term refers to the return mechanism at the input and the second term to the sense mechanism at the output.
| Solution As evident from Examples 12.10 and 12.12, this topology indeed employs negative voltage-voltage feedback: the resistive network senses $V_{\text {out }}$ with a high impedance (because $R_{1}+R_{2}$ is very large), returning a voltage to the gate of $M_{2}$. As mentioned in Example $12.10, M_{1}$ and $M_{2}$ serve as the input stage of the forward system and as a subtractor.

Noting that $A_{0}$ is the gain of the circuit consisting of $M_{1}-M_{4}$, we write from Chapter 10

$$
\begin{equation*}
A_{0}=g_{m N}\left(r_{O N} \| r_{O P}\right) \tag{12.55}
\end{equation*}
$$

where the subscripts $N$ and $P$ refer to NMOS and PMOS devices, respectively. ${ }^{7}$ With $K=R_{2} /\left(R_{1}+R_{2}\right)$, we obtain

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=\frac{g_{m N}\left(r_{O N} \| r_{O P}\right)}{1+\frac{R_{2}}{R_{1}+R_{2}} g_{m N}\left(r_{O N} \| r_{O P}\right)} \tag{12.56}
\end{equation*}
$$

As expected, if the loop gain remains much greater than unity, then the closed-loop gain is approximately equal to $1 / K=1+R_{1} / R_{2}$.

Exercise If $g_{m N}=1 /(100 \Omega), r_{O N}=5 \mathrm{k} \Omega$, and $r_{O P}=2 \mathrm{k} \Omega$, determine the required value of $R_{2} /\left(R_{1}+R_{2}\right)$ for a closed loop gain of 4 . Compare the result with the nominal value of $\left(R_{2}+R_{1}\right) / R_{2}=4$.
image_name:Figure 12.31 Calculation of input impedance
description:The system block diagram titled "Figure 12.31 Calculation of input impedance" illustrates a feedback amplifier system with several key components:

1. **Main Components:**
- **Voltage Source (V_in):** This is the input voltage source, grounded at one end, providing the input signal to the system.
- **Summing Junction (+):** This block combines the input voltage \( V_{in} \) with the feedback voltage \( V_F \). The input voltage \( V_{in} \) is applied to the positive terminal, and the feedback voltage \( V_F \) is applied to the negative terminal, resulting in the effective input voltage \( V'_{in} \).
- **Feedforward System Block:**
- **Amplifier (A_0):** An operational amplifier with finite input resistance \( R_{in} \). It amplifies the input current \( I_{in} \) and produces an output \( Out(A_0) \).
- **Input Resistance (R_{in}):** Connected to ground, it models the finite input impedance of the amplifier.
- **Feedback Network (K):** This block takes a portion of the output and feeds it back to the summing junction as \( V_F \).

2. **Flow of Information or Control:**
- The input voltage \( V_{in} \) is applied to the summing junction, where it is combined with the feedback voltage \( V_F \) to produce \( V'_{in} \).
- The resulting voltage \( V'_{in} \) is converted to a current \( I_{in} \) through the input resistance \( R_{in} \), and this current flows into the amplifier \( A_0 \).
- The amplifier \( A_0 \) processes this current and produces an output \( Out(A_0) \).
- A portion of this output is fed back through the feedback network \( K \) to the summing junction.

3. **Labels, Annotations, and Key Indicators:**
- The diagram includes labels such as \( V_{in} \), \( I_{in} \), \( R_{in} \), \( A_0 \), \( Out(A_0) \), and \( V_F \) to indicate the various voltages, currents, and components within the system.
- Ground symbols are present to indicate reference points for the voltages.

4. **Overall System Function:**
- The primary function of this system is to amplify the input signal \( V_{in} \) while incorporating feedback to control the overall gain and input impedance. The feedback network adjusts the effective input voltage \( V'_{in} \) by subtracting a portion of the output, thus stabilizing the system and maintaining the desired gain and impedance characteristics.

Figure 12.31 Calculation of input impedance.
In order to analyze the effect of feedback on the I/O impedances, we assume the forward system is a nonideal voltage amplifier (i.e., it exhibits finite I/O impedances) while the feedback network remains ideal. Depicted in Fig. 12.31 is the overall topology including a finite input resistance for the forward amplifier. Without feedback, of course, the entire input signal would appear across $R_{i n}$, producing an input current of $V_{i n} / R_{i n}{ }^{8}$ With feedback, on the other hand, the voltage developed at the input of $A_{0}$ is equal to $V_{i n}-V_{F}$ and also equal to $I_{i n} R_{i n}$. Thus,

$$
\begin{align*}
I_{i n} R_{i n} & =V_{i n}-V_{F}  \tag{12.57}\\
& =V_{i n}-\left(I_{i n} R_{i n}\right) A_{0} K \tag{12.58}
\end{align*}
$$

[^16]It follows that

$$
\begin{equation*}
\frac{V_{i n}}{I_{i n}}=R_{i n}\left(1+K A_{0}\right) \tag{12.59}
\end{equation*}
$$

Interestingly, negative feedback around a voltage amplifier raises the input impedance by the universal factor of one plus the loop gain. This impedance modification brings the circuit closer to an ideal voltage amplifier.

Example Determine the input impedance of the stage shown in Fig. 12.32(a) if $R_{1}+R_{2}$ is very 12.16 large.
image_name:Fig. 12.32(a)
description:
[
name: M1, type: NMOS, ports: {S:Vin, D: Vout, G: VF}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: VF}
name: R2, type: Resistor, value: R2, ports: {N1: VF, N2: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a common-source NMOS amplifier with resistive feedback. The feedback network consists of resistors R1 and R2, providing negative feedback to stabilize the gain and increase input impedance. The output is taken at Vout.

image_name:Fig. 12.32(b)
description:
[
name: M1, type: NMOS, ports: {S: Vin, D: Vout, G: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: X}
name: R2, type: Resistor, value: R2, ports: {N1: X, N2: GND}
]
extrainfo:The circuit is a common-source NMOS amplifier with resistive feedback. The feedback network consists of resistors R1 and R2, providing negative feedback to stabilize the gain and increase input impedance. The output is taken at Vout.

Solution We first open the loop to calculate $R_{\text {in }}$ in Eq. (12.59). To open the loop, we break the gate of $M_{1}$ from the feedback signal and tie it to ground [Fig. 12.32(b)]:

$$
\begin{equation*}
R_{i n}=\frac{1}{g_{m}} \tag{12.60}
\end{equation*}
$$

The closed-loop input impedance is therefore given by

$$
\begin{equation*}
\frac{V_{i n}}{I_{i n}}=\frac{1}{g_{m}}\left(1+\frac{R_{2}}{R_{1}+R_{2}} g_{m} R_{D}\right) \tag{12.61}
\end{equation*}
$$

Exercise What happens if $R_{2} \rightarrow \infty$ ? Is this result expected?

The effect of feedback on the output impedance can be studied with the aid of the diagram shown in Fig. 12.33, where the forward amplifier exhibits an output impedance of $R_{\text {out }}$. Expressing the error signal at the input of $A_{0}$ as $-V_{F}=-K V_{X}$, we write the output voltage of $A_{0}$ as $-K A_{0} V_{X}$ and hence

$$
\begin{equation*}
I_{X}=\frac{V_{X}-\left(-K A_{0} V_{X}\right)}{R_{\text {out }}} \tag{12.62}
\end{equation*}
$$

where the current drawn by the feedback network is neglected. Thus,

$$
\begin{equation*}
\frac{V_{X}}{I_{X}}=\frac{R_{\text {out }}}{1+K A_{0}} \tag{12.63}
\end{equation*}
$$

image_name:Figure 12.33
description:The circuit is a feedforward system with an operational amplifier A0, a resistor Rout, and a feedback element K. The voltage source Vx is connected to the output node Vx, which is also connected to the feedback element K.

Figure 12.33 Calculation of output impedance.
revealing that negative feedback lowers the output impedance if the topology senses the output voltage. The circuit is now a better voltage amplifier-as predicted by our gain desensitization analysis in Section 12.2.

Example $\quad$ Calculate the output impedance of the circuit shown in Fig. 12.34 if $R_{1}+R_{2}$ is very large.
image_name:Figure 12.34
description:
[
name: M1, type: NMOS, ports: {S: s1s2, D: d1d3g3, G: GND}
name: M2, type: NMOS, ports: {S: s1s2, D: Vx, G: VF}
name: M3, type: PMOS, ports: {S: VDD, D: d1d3g3, G: d1d3g3}
name: M4, type: PMOS, ports: {S: VDD, D: Vx, G: d1d3g3}
name: R1, type: Resistor, value: R1, ports: {N1: Vx, N2: VF}
name: R2, type: Resistor, value: R2, ports: {N1: VF, N2: GND}
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Vx, Nn: GND}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: s1s2, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with a current source biasing. M1 and M2 form the differential pair, while M3 and M4 act as active loads. The resistors R1 and R2 provide feedback, and the voltage source Vx is used for testing output impedance.

Figure 12.34

Solution Recall from Example 12.15 that the open-loop output impedance is equal to $r_{O N} \| r_{O P}$ and $K A_{0}=\left[R_{2} /\left(R_{1}+R_{2}\right)\right] g_{m N}\left(r_{O N} \| r_{O P}\right)$. Thus, the closed-loop output impedance, $R_{\text {out,closed }}$, is given by

$$
\begin{equation*}
R_{\text {out }, \text { closed }}=\frac{r_{O N} \| r_{O P}}{1+\frac{R_{2}}{R_{1}+R_{2}} g_{m N}\left(r_{O N} \| r_{O P}\right)} \tag{12.64}
\end{equation*}
$$

If the loop gain is much greater than unity,

$$
\begin{equation*}
R_{\text {out }, \text { closed }} \approx\left(1+\frac{R_{1}}{R_{2}}\right) \frac{1}{g_{m N}} \tag{12.65}
\end{equation*}
$$

a value independent of $r_{O N}$ and $r_{O P}$. In other words, while the open-loop amplifier suffers from a high output impedance, the application of negative feedback lowers $R_{\text {out }}$ to a multiple of $1 / g_{m N}$.

Exercise What happens if $R_{2} \rightarrow \infty$ ? Can you prove this result by direct analysis of the circuit?

In summary, voltage-voltage feedback lowers the gain and the output impedance by $1+K A_{0}$ and raises the input impedance by the same factor.

### 12.6.2 Voltage-Current Feedback

Depicted in Fig. 12.35, this topology employs a transimpedance amplifier as the forward system, requiring that the feedback network sense the output voltage and return a current to the subtractor. In our terminology, the first term in "voltage-current feedback" refers to the quantity sensed at the output, and the second, to the quantity returned to the input. (This terminology is not standard.) Also, recall from Section 12.4 that such a feedback network must appear in parallel with the output and with the input, ${ }^{9}$ ideally providing both an infinite input impedance and an infinite output impedance (why?). Note that the feedback factor in this case has a dimension of conductance because $K=I_{F} / V_{\text {out }}$.
image_name:Figure 12.35 Voltage-current feedback
description:The circuit implements a voltage-current feedback mechanism where the current at the output is sensed and fed back to the input. The feedback factor K is characterized by the conductance (I_F / V_out). The closed-loop gain is derived as V_out / I_in = R_0 / (1 + K * R_0).

Figure 12.35 Voltage-current feedback.
We first compute the closed-loop gain, expecting to obtain a familiar result. Since $I_{e}=I_{\text {in }}-I_{F}$ and $V_{\text {out }}=I_{e} R_{0}$, we have

$$
\begin{align*}
V_{\text {out }} & =\left(I_{\text {in }}-I_{F}\right) R_{0}  \tag{12.66}\\
& =\left(I_{\text {in }}-K V_{\text {out }}\right) R_{0}, \tag{12.67}
\end{align*}
$$

and hence

$$
\begin{equation*}
\frac{V_{\text {out }}}{I_{\text {in }}}=\frac{R_{0}}{1+K R_{0}} . \tag{12.68}
\end{equation*}
$$

For the circuit shown in Fig. 12.36(a), assume $\lambda=0$ and $R_{F}$ is very large and (a) prove that 12.18 the feedback is negative; (b) calculate the open-loop gain; (c) calculate the closed-loop
gain.

[^17]Solution (a) If $I_{\text {in }}$ increases, $I_{D 1}$ decreases and $V_{X}$ rises. As a result, $V_{\text {out }}$ falls, thereby reducing $I_{R F}$. Since the currents injected by $I_{i n}$ and $R_{F}$ into the input node change in opposite directions, the feedback is negative.
(b) To calculate the open-loop gain, we consider the forward amplifier without the feedback network, exploiting the assumption that $R_{F}$ is very large [Fig. 12.36(b)].
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: S1, D: X, G: Vb}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: X}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: X}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: Vout}
name: RF, type: Resistor, value: RF, ports: {N1: S1, N2: Vout}
name: iin, type: CurrentSource, value: iin, ports: {Np: GND, Nn: s1}
]
extrainfo:The circuit is a transimpedance amplifier with negative feedback. The feedback is provided through RF, and the amplifier consists of two NMOS transistors M1 and M2. RD1 and RD2 are the load resistors. The input current iin is converted to an output voltage Vout.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: S1, D: X, G: Vb}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: X}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: X}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: Vout}
name: iin, type: CurrentSource, value: iin, ports: {Np: GND, Nn: s1}
]
extrainfo:The circuit (b) is an open-loop amplifier configuration. M1 and M2 are NMOS transistors, RD1 and RD2 are the load resistors, and RF is the feedback resistor. The input current source SI is connected to the source of M1 and the feedback resistor RF. The circuit is designed to analyze the open-loop gain by considering the forward amplifier without the feedback network.
image_name:(c)
description:
[
name: M1, type: NMOS, ports: {S: s1, D: LOAD, G: Vb}
name: RF, type: Resistor, value: RF, ports: {N1: s1, N2: Vout}
]
extrainfo:The circuit is a transimpedance amplifier with feedback. The feedback resistor RF connects the output to the input current source SI. The NMOS transistors M1 and M2 form the amplification stages, with M1's gate controlled by a bias voltage Vb and M2's gate connected to the node X. The resistors RD1 and RD2 are load resistors connected to the supply voltage VDD.

Figure 12.36
The transimpedance gain is given by the gain from $I_{\text {in }}$ to $V_{X}$ (i.e., $R_{D 1}$ ) multiplied by that from $V_{X}$ to $V_{\text {out }}$ (i.e., $-g_{m 2} R_{D 2}$ ):

$$
\begin{equation*}
R_{0}=R_{D 1}\left(-g_{m 2} R_{D 2}\right) \tag{12.69}
\end{equation*}
$$

Note that this result assumes $R_{F} \gg R_{D 2}$ so that the gain of the second stage remains equal to $-g_{m 2} R_{D 2}$.
(c) To obtain the closed-loop gain, we first note that the current returned by $R_{F}$ to the input is approximately equal to $V_{\text {out }} / R_{F}$ if $R_{F}$ is very large. To prove this, we consider a section of the circuit as in Fig. 12.36(c) and write

$$
\begin{equation*}
I_{R F}=\frac{V_{\text {out }}}{R_{F}+\frac{1}{g_{m 1}}} \tag{12.70}
\end{equation*}
$$

Thus, if $R_{F} \gg 1 / g_{m 1}$, the returned current is approximately equal to $V_{\text {out }} / R_{F}$. (We say " $R_{F}$ operates as a current source.") That is, $K=-1 / R_{F}$, where the negative sign arises from the direction of the current drawn by $R_{F}$ from the input node with respect to that in Fig. 12.35. Forming $1+K R_{0}$, we express the closed-loop gain as

$$
\begin{equation*}
\left.\frac{V_{\text {out }}}{I_{\text {in }}}\right|_{\text {closed }}=\frac{-g_{m 2} R_{D 1} R_{D 2}}{1+\frac{g_{m 2} R_{D 1} R_{D 2}}{R_{F}}} \tag{12.71}
\end{equation*}
$$

which reduces to $-R_{F}$ if $g_{m 2} R_{D 1} R_{D 2} \gg R_{F}$.
It is interesting to note that the assumption that $R_{F}$ is very large translates to two conditions in this example: $R_{F} \gg R_{D 2}$ and $R_{F} \gg 1 / g_{m 1}$. The former arises from the output network calculations and the latter from the input network calculations. What happens if one or both of these assumptions are not valid? We deal with this (relatively common) situation in Section 12.7.

What is the closed-loop gain if $R_{D 1} \rightarrow \infty$ ? How can this result be interpreted? (Hint: the infinite open-loop gain creates a virtual ground node at the source of $M_{1}$.)
image_name:Figure 12.37
description:
[
name: Ix, type: CurrentSource, ports: {Np: GND, Nn: Vx}
name: Rin, type: Resistor, value: Rin, ports: {N1: Vx, N2: In(R0)}
name: R0, type: OpAmp, value: R0, ports: {InP: In(R0), InN: GND, Out: Out(R0)}
name: K, type: Other, ports: {N1: Out(R0), N2: In(R0)}
]
extrainfo:The circuit models a transimpedance amplifier with input current Ix and output voltage at Out(R0). The feedback network includes a block labeled K, indicating additional processing or feedback control.

Figure 12.37 Calculation of input impedance.

We now proceed to determine the closed-loop I/O impedances. Modeling the forward system as an ideal transimpedance amplifier but with a finite input impedance $R_{\text {in }}$ (Section 12.3), we construct the test circuit shown in Fig. 12.37. Since the current flowing through $R_{\text {in }}$ is equal to $V_{X} / R_{\text {in }}$ (why?), the forward amplifier produces an output voltage equal to $\left(V_{X} / R_{\text {in }}\right) R_{0}$ and hence

$$
\begin{equation*}
I_{F}=K \frac{V_{X}}{R_{i n}} R_{0} \tag{12.72}
\end{equation*}
$$

Writing a KCL at the input node thus yields

$$
\begin{equation*}
I_{X}-K \frac{V_{X}}{R_{i n}} R_{0}=\frac{V_{X}}{R_{i n}} \tag{12.73}
\end{equation*}
$$

and hence

$$
\begin{equation*}
\frac{V_{X}}{I_{X}}=\frac{R_{i n}}{1+K R_{0}} \tag{12.74}
\end{equation*}
$$

That is, a feedback loop returning current to the input lowers the input impedance by a factor of one plus the loop gain, bringing the circuit closer to an ideal "current sensor."

| Example <br> 12.19 | Determine the closed-loop input impedance of the circuit studied in Example 12.18. |
| :--- | :--- |
| Solution | The open-loop amplifier shown in Fig. 12.36(b) exhibits an input impedance $R_{\text {in }}=1 / g_{m 1}$ <br> because $R_{F}$ is assumed to be very large. With $1+K R_{0}$ from the denominator of <br> Eq. (12.71), we obtain |
| $\qquad R_{\text {in, closed }}=\frac{1}{g_{m 1}} \cdot \frac{1}{1+\frac{g_{m 2} R_{D 1} R_{D 2}}{R_{F}}}$. |  |

Exercise Explain what happens if $R_{D 1} \rightarrow \infty$ and why.

From our study of voltage-voltage feedback in Section 12.6.1, we postulate that voltage-current feedback too lowers the output impedance because a feedback loop "regulating" the output voltage tends to stabilize it despite load impedance variations. Drawing the circuit as shown in Fig. 12.38, where the input current source is set to zero and $R_{\text {out }}$ models the open-loop output resistance, we observe that the feedback network produces a current of $I_{F}=K V_{X}$. Upon flowing through the forward amplifier, this current translates
image_name:Figure 12.38
description:The circuit diagram depicts a voltage-current feedback system used to lower the output impedance. The feedback network generates a current (IF) proportional to the voltage (Vx), which is fed back through the forward amplifier (R0). The equation for the output impedance is given by Rout/(1+KR0). The circuit stabilizes the output voltage despite load impedance variations.

Figure 12.38 Calculation of output impedance.
to $V_{A}=-K V_{X} R_{0}$ and hence

$$
\begin{align*}
I_{X} & =\frac{V_{X}-V_{A}}{R_{\text {out }}}  \tag{12.76}\\
& =\frac{V_{X}+K V_{X} R_{0}}{R_{\text {out }}} \tag{12.77}
\end{align*}
$$

where the current drawn by the feedback network is neglected. Thus,

$$
\begin{equation*}
\frac{V_{X}}{I_{X}}=\frac{R_{\text {out }}}{1+K R_{0}} \tag{12.78}
\end{equation*}
$$

an expected result.

Example Calculate the closed-loop output impedance of the circuit studied in Example 12.18.
12.20

Solution From the open-loop circuit in Fig. 12.36(b), we have $R_{\text {out }} \approx R_{D 2}$ because $R_{F}$ is assumed very large. Writing $1+K R_{0}$ from the denominator of Eq. (12.71) gives

$$
\begin{equation*}
R_{\text {out }, \text { closed }}=\frac{R_{D 2}}{1+\frac{g_{m 2} R_{D 1} R_{D 2}}{R_{F}}} \tag{12.79}
\end{equation*}
$$

Exercise Explain what happens if $R_{D 1} \rightarrow \infty$ and why.

### 12.6.3 Current-Voltage Feedback

Shown in Fig. 12.39(a), this topology incorporates a transconductance amplifier, requiring that the feedback network sense the output current and return a voltage to the subtractor. Again, in our terminology, the first term in "current-voltage feedback" refers to the
image_name:Figure 12.39
description:The system block diagram in Figure 12.39 illustrates a current-voltage feedback topology, which is centered around a transconductance amplifier labeled as **Gm**. This topology is designed to sense an output current and feed back a voltage to a subtractor, forming a feedback loop.

Main Components:
1. **Transconductance Amplifier (Gm):** This block is responsible for converting the input voltage difference into an output current (**I_out**). It receives input from two points, labeled **V1+** and **V1-**.
2. **Feedback Network (K):** This block processes the feedback voltage (**V_F**) and returns it to the subtractor input. It is connected in a loop with the transconductance amplifier.

Flow of Information or Control:
- The input voltage (**Vin**) is applied, and the transconductance amplifier (**Gm**) converts the voltage difference between **V1+** and **V1-** into an output current (**I_out**).
- The output current (**I_out**) is sensed at point **X2** and is part of the feedback loop.
- The feedback network (**K**) receives the feedback voltage (**V_F**) generated from the output current and processes it to be fed back into the amplifier.
- The feedback voltage is applied to the subtractor, influencing the input to the transconductance amplifier, thereby controlling the output current.

Labels, Annotations, and Key Indicators:
- **Vin1, Vin2:** These are input voltages applied to the system.
- **X1, X2, X3:** These points indicate connections and interaction points within the feedback loop.
- **V1+, V1-:** Differential input terminals for the transconductance amplifier.
- **V_F:** Feedback voltage that is processed by block **K**.

Overall System Function:
The primary function of this system is to achieve current-voltage feedback, where the output current is sensed and converted back into a controlling voltage. This feedback mechanism helps regulate the operation of the transconductance amplifier by adjusting the input voltage difference based on the output current, maintaining stability and desired performance in the circuit.

Figure 12.39 Current-voltage feedback.

[^0]:    ${ }^{10}$ The Early effect and channel-length modulation are neglected here.

[^1]:    ${ }^{11}$ Recall that we denote frequency-domain quantities with upper-case letters.

[^2]:    ${ }^{12}$ As explained in more advanced courses, this zero does become problematic in the internal circuitry of op amps.

[^3]:    ${ }^{13}$ The large discrepancy between $\left|\omega_{p, \text { out }}\right|$ and $\left|\omega_{p 2}\right|$ results from an effect called "pole splitting" and is studied in more advanced courses.

[^4]:    ${ }^{14}$ In calculation of the input impedance, the output impedance of the preceding stage (denoted by $R_{S}$ ) is excluded.

[^5]:    ${ }^{15}$ One exception is encountered in radio-frequency circuits (e.g., cellphones), where the input capacitance becomes undesirable.

[^6]:    ${ }^{16}$ In reality, the junction capacitances $C_{S B}$ and $C_{D B}$ sustain different reverse bias voltages and are therefore not quite equal.

[^7]:    ${ }^{17}$ If the follower output resistance is greater than $R_{S}$, then it is better to omit the follower!

[^8]:    ${ }^{18}$ The voltage division between $R_{S}$ and $r_{\pi 1}$ lowers the gain slightly in the bipolar circuit.

[^9]:    *This section can be skipped in a first reading.

[^10]:    ${ }^{19}$ With this estimate of the gain, we can express the Miller effect of $R_{F}$ at the output as $R_{F} /\left(1-A_{v 2}^{-1}\right) \approx 8.7 \mathrm{k} \Omega$, place this resistance in parallel with $R_{L 2}$, and write $A_{v 2}=-g_{m 2}\left(R_{D 2} \| 8.7 \mathrm{k} \Omega\right)=-5.98$. But we continue without this iteration for simplicity. ${ }^{20}$ If not, then the circuit must be solved using a complete small-signal equivalent.

[^11]:    ${ }^{1}$ Also called the "forward" system.

[^12]:    ${ }^{2}$ We use voltage quantities in this example, but other quantities work as well.

[^13]:    ${ }^{3}$ Some analog-to-digital converters (ADCs) require very precise voltage gains. For example, a 10-bit ADC may call for a gain of 2.000 .

[^14]:    ${ }^{4}$ Recall from Chapter 7 that the gain of the source follower is equal to unity in this case.

[^15]:    ${ }^{5}$ Of course, only quantities having the same dimension can be added or subtracted. That is, a voltage cannot be added to a current.

[^16]:    ${ }^{7}$ We observe that $R_{1}+R_{2}$ must be much greater than $r_{O N} \| r_{O P}$ for this to hold. This serves as the definition of $R_{1}+R_{2}$ being "very large."
${ }^{8}$ Note that $V_{\text {in }}$ and $R_{\text {in }}$ carry equal currents because the feedback network must appear in series with the input [Fig. 12.21(a)].

[^17]:    ${ }^{9}$ For this reason, this type is also called "shunt-shunt" feedback.

quantity sensed at the output, and the second, to the quantity returned to the input. Recall from Section 12.4 that such a feedback network must appear in series with the output and with the input, ${ }^{10}$ ideally exhibiting zero input and output impedances. Note that the feedback factor in this case has a dimension of resistance because $K=V_{F} / I_{\text {out }}$.

Let us first confirm that the closed-loop gain is equal to the open-loop gain divided by one plus the loop gain. Since the forward system produces a current equal to $I_{\text {out }}=G_{m}\left(V_{\text {in }}-V_{F}\right)$ and since $V_{F}=K I_{\text {out }}$, we have

$$
\begin{equation*}
I_{\text {out }}=G_{m}\left(V_{\text {in }}-K I_{\text {out }}\right) \tag{12.80}
\end{equation*}
$$

and hence

$$
\begin{equation*}
\frac{I_{\text {out }}}{V_{\text {in }}}=\frac{G_{m}}{1+K G_{m}} \tag{12.81}
\end{equation*}
$$

image_name:Figure 12.40(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: Vin}
name: RM, type: Resistor, value: RM, ports: {N1: VF, N2: GND}
name: A0, type: OpAmp, value: A0, ports: {InP: Vin, InN: VF, OutP: d1, OutN: GND}
name: M5, type: PMOS, ports: {S: VDD, D: X, G: Y}
name: M6, type: PMOS, ports: {S: VDD, D: Y, G: X}
name: M3, type: NMOS, ports: {S: GND, D: s3s4, G: Vin}
name: M4, type: NMOS, ports: {S: s3s4, D: GND, G: VF}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: s3s4, Nn: GND}
]
extrainfo:The circuit is designed to deliver a well-defined current to a laser diode. It uses a feedback loop with an op-amp to control the current through the laser by monitoring the voltage across a series resistor RM. The transconductance of M1 is controlled by the op-amp, which adjusts the gate voltage of the NMOS transistors M3 and M4 to maintain the desired current level.
image_name:Figure 12.40(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: VDD}
name: RM, type: Resistor, value: RM, ports: {N1: VF, N2: GND}
name: Ao, type: OpAmp, value: Ao, ports: {InP: Vin, InN: VF, Out: d1}
name: M5, type: PMOS, ports: {S: VDD, D: X, G: Y}
name: M6, type: PMOS, ports: {S: VDD, D: Y, G: X}
name: M3, type: NMOS, ports: {S: s3s4, D: Vin, G: GND}
name: M4, type: NMOS, ports: {S: s3s4, D: VF, G: GND}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: GND, Nn: s3s4}
]
extrainfo:The circuit in Figure 12.40(b) is designed to deliver a well-defined current to a laser diode. It uses an op-amp to control the transconductance of M1 by monitoring the current through a resistor RM. The op-amp adjusts the gate voltage of M1 to maintain the desired current. The circuit also includes PMOS transistors M5 and M6, and NMOS transistors M3 and M4, along with a current source ISS to stabilize the operation.
image_name:Figure 12.40(c)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: Y}
name: M3, type: NMOS, ports: {S: GND, D: X, G: Vin}
name: M4, type: NMOS, ports: {S: X, D: Y, G: Vin}
name: M5, type: PMOS, ports: {S: VDD, D: X, G: Y}
name: M6, type: PMOS, ports: {S: VDD, D: Y, G: X}
name: A0, type: OpAmp, ports: {InP: Vin, InN: VF, Out: Y}
name: RM, type: Resistor, value: RM, ports: {N1: VF, N2: GND}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: GND, Nn: X}
]
extrainfo:The circuit is designed to deliver a well-defined current to a laser diode by controlling the transconductance of M1 through feedback. The op-amp provides high gain to stabilize the output current, I_out. The circuit uses a feedback loop involving a resistor RM to monitor the current and adjust the input to the op-amp accordingly.
image_name:Figure 12.40(d)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Iout, G: X}
name: RM, type: Resistor, value: RM, ports: {N1: VF, N2: GND}
name: A0, type: OpAmp, value: A0, ports: {InP: Vin, InN: VF, Out: X}
name: M3, type: NMOS, ports: {S: GND, D: S3S4, G: Vin}
name: M4, type: NMOS, ports: {S: S3S4, D: GND, G: VF}
name: M5, type: PMOS, ports: {S: VDD, D: X, G: S3S4}
name: M6, type: PMOS, ports: {S: VDD, D: Y, G: S3S4}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: S3S4, Nn: GND}
]
extrainfo:The circuit is a current mirror with feedback control using an op-amp to stabilize the current through a laser diode. The op-amp senses the voltage across RM and adjusts the gate voltage of M1 to control Iout.
image_name:Figure 12.40(e)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Iout, G: Vin}
name: RM, type: Resistor, value: RM, ports: {N1: VF, N2: GND}
name: Ao, type: OpAmp, value: Ao, ports: {InP: Vin, InN: VF, Out: G1}
name: M3, type: NMOS, ports: {S: GND, D: S3S4, G: Vin}
name: M4, type: NMOS, ports: {S: S3S4, D: VF, G: Vin}
name: M5, type: PMOS, ports: {S: VDD, D: X, G: Y}
name: M6, type: PMOS, ports: {S: VDD, D: Y, G: X}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: S3S4, Nn: GND}
]
extrainfo:The circuit in Fig. 12.40(e) is a current control system for a laser diode. It uses an operational amplifier to monitor and control the current through the laser diode by adjusting the voltage across a resistor (RM). The PMOS and NMOS transistors form a feedback loop to stabilize the current output.



[^0]Solution If the gain of the op amp is very high, the difference between $V_{i n}$ and $V_{F}$ is very small. Thus, $R_{M}$ sustains a voltage equal to $V_{i n}$ and hence

$$
\begin{equation*}
I_{\text {out }} \approx \frac{V_{\text {in }}}{R_{M}} \tag{12.82}
\end{equation*}
$$

We now determine the open-loop gain of the transistor-level implementation in Fig. 12.40(c). The forward amplifier can be identified as shown in Fig. 12.40(d), where the gate of $M_{4}$ is grounded because the feedback signal (voltage) is set to zero. Since $I_{\text {out }}=-g_{m 1} V_{X}($ why? $)$ and $V_{X}=-g_{m 3}\left(r_{O 3} \| r_{O 5}\right) V_{\text {in }}$, we have

$$
\begin{equation*}
G_{m}=g_{m 1} g_{m 3}\left(r_{O 3} \| r_{O 5}\right) \tag{12.83}
\end{equation*}
$$

The feedback factor $K=V_{F} / I_{\text {out }}=R_{M}$. Thus,

$$
\begin{equation*}
\left.\frac{I_{\text {out }}}{V_{\text {in }}}\right|_{\text {closed }}=\frac{g_{m 1} g_{m 3}\left(r_{O 3} \| r_{O 5}\right)}{1+g_{m 1} g_{m 3}\left(r_{O 3} \| r_{O 5}\right) R_{M}} \tag{12.84}
\end{equation*}
$$

Note that if the loop gain is much greater than unity, then

$$
\begin{equation*}
\left.\frac{I_{\text {out }}}{V_{\text {in }}}\right|_{\text {closed }} \approx \frac{1}{R_{M}} \tag{12.85}
\end{equation*}
$$

We must now answer two questions. First, why is the drain of $M_{1}$ shorted to ground in the open-loop test? The simple answer is that, if this drain is left open, then $I_{\text {out }}=0$ ! But, more fundamentally, we can observe a duality between this case and that of voltage outputs, e.g., in Fig. 12.36. If driving no load, the output port of a voltage amplifier is left open. Similarly, if driving no load, the output port of a circuit delivering a current must be shorted to ground.

Second, why is the active-load amplifier in Fig. 12.40(c) drawn with the diodeconnected device on the right? This is to ensure negative feedback. For example, if $V_{\text {in }}$ goes up, $V_{X}$ goes down (why?), $M_{1}$ provides a greater current, and the voltage drop across $R_{M}$ rises, thereby steering a larger fraction of $I_{S S}$ to $M_{4}$ and opposing the effect of the change in $V_{\text {in }}$. Alternatively, the circuit can be drawn as shown in Fig. 12.40(e).

Exercise Suppose $V_{\text {in }}$ is a sinusoid with a peak amplitude of 100 mV . Plot $V_{F}$ and the current through the laser as a function of time if $R_{M}=10 \Omega$ and $G_{m}=1 /(0.5 \Omega)$. Is the voltage at the gate of $M_{1}$ necessarily a sinusoid?

From our analysis of other feedback topologies in Sections 12.6 .1 and 12.6.2, we postulate that current-voltage feedback increases the input impedance by a factor of $1+K G_{m}$. In fact, the test circuit shown in Fig. 12.41(a) is similar to that in Fig. 12.31-except that the forward system is denoted by $G_{m}$ rather than $A_{0}$. Thus, Eq. (12.59) can be rewritten as

$$
\begin{equation*}
\frac{V_{i n}}{I_{i n}}=R_{i n}\left(1+K G_{m}\right) \tag{12.86}
\end{equation*}
$$

The output impedance is calculated using the test circuit of Fig. 12.41(b). Note that, in contrast to the cases in Figs. 12.33 and 12.38, the test voltage source is inserted in series with the output port of the forward amplifier and the input port of the feedback network. The voltage developed at port $A$ is equal to $-K I_{X}$ and the current drawn by the $G_{m}$ stage
image_name:Figure 12.41(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Rin, type: Resistor, value: Rin, ports: {N1: Iin, N2: GND}
name: Gm, type: OpAmp, value: Gm, ports: {InP: Iin, InN: VF, OutP: Out, OutN:}
name: K, type: Other, ports: {N1: VF, N2: Out}
name: Rout, type: Resistor, value: Rout, ports: {N1: Vx, N2: X3}
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Vx, Nn: GND}
name: A, type: Other, ports: {N1: X1, N2: X2}
]
extrainfo:The circuit diagram (a) is used to calculate input impedance, involving a voltage source Vin, a resistor Rin, and an operational amplifier Gm with feedback K. It forms a feedback loop with the output connected back to the input through K. The diagram (b) is used to calculate output impedance, involving a voltage source Vx, a resistor Rout, and an operational amplifier Gm with feedback K. The nodes X1, X2, and X3 are used to interconnect the components.
image_name:Figure 12.41(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: X1, Nn: GND}
name: Rin, type: Resistor, value: Rin, ports: {N1: X1, N2: X2}
name: Gm, type: OpAmp, value: Gm, ports: {InP: X2, InN: X3, OutP: X1}
name: K, type: Other, ports: {N1: X2, N2: X3}
name: Rout, type: Resistor, value: Rout, ports: {N1: X3, N2: Vx}
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Vx, Nn: GND}
name: A, type: Other, ports: {N1: X1, N2: X2}
]
extrainfo:The circuit in diagram (b) is used to calculate the output impedance. It includes an op-amp Gm, resistors Rin and Rout, and voltage sources Vin and Vx. The feedback network K is connected between nodes X2 and X3. The test voltage source Vx is in series with the output port of the forward amplifier and the input port of the feedback network.

Figure 12.41 Calculation of (a) input and (b) output impedances.
equal to $-K G_{m} I_{X}$. Since the current flowing through $R_{\text {out }}$ is given by $V_{X} / R_{\text {out }}$, a KCL at the output node yields

$$
\begin{equation*}
I_{X}=\frac{V_{X}}{R_{\text {out }}}-K G_{m} I_{X} \tag{12.87}
\end{equation*}
$$

and hence

$$
\begin{equation*}
\frac{V_{X}}{I_{X}}=R_{\text {out }}\left(1+K G_{m}\right) \tag{12.88}
\end{equation*}
$$

Interestingly, a negative feedback loop sensing the output current raises the output impedance, bringing the circuit closer to an ideal current generator. As in other cases studied thus far, this occurs because negative feedback tends to regulate the output quantity that it senses.

Example An alternative approach to regulating the current delivered to a laser diode is shown in
12.22 Fig. 12.42(a). As in the circuit of Fig. 12.40(b), the very small resistor $R_{M}$ monitors the current, generating a proportional voltage and feeding it back to the subtracting device, $M_{1}$. Determine the closed-loop gain and I/O impedances of the circuit.
image_name:Figure 12.42(a)
description:
[
name: M1, type: NMOS, ports: {S: Vin, D: X, G: VF}
name: M2, type: NMOS, ports: {S: Y, D: VDD, G: X}
name: RD, type: Resistor, value: RD, ports: {N1: X, N2: VDD}
name: RM, type: Resistor, value: RM, ports: {N1: VF, N2: GND}
]
extrainfo:The circuit is a current regulator for a laser diode using NMOS transistors in a feedback configuration. The current through the laser is monitored by a small resistor RM, and the feedback is used to stabilize the current.

image_name:Figure 12.42(b)
description:
[
name: RD, type: Resistor, ports: {N1: X, N2: VDD}
name: M1, type: NMOS, ports: {S: Vin, D: X, G: GND}
name: M2, type: NMOS, ports: {S: GND, D: VDD, G: X}
]
extrainfo:The circuit is a current regulator for a laser diode using NMOS transistors in a feedback configuration. The current through the laser is monitored by a small resistor RM, and the feedback is used to stabilize the current.

Solution Since $R_{M}$ is very small, the open-loop circuit reduces to that shown in Fig. 12.42(b), where the gain can be expressed as

$$
\begin{align*}
G_{m} & =\frac{V_{X}}{V_{\text {in }}} \cdot \frac{I_{\text {out }}}{V_{X}}  \tag{12.89}\\
& =g_{m 1} R_{D} \cdot g_{m 2} \tag{12.90}
\end{align*}
$$

The input impedance is equal to $1 / g_{m 1}$ and the output impedance equal to $1 / g_{m 2}{ }^{12}$ The feedback factor is equal to $R_{M}$, yielding

$$
\begin{equation*}
\left.\frac{I_{\text {out }}}{V_{\text {in }}}\right|_{\text {closed }}=\frac{g_{m 1} g_{m 2} R_{D}}{1+g_{m 1} g_{m 2} R_{D} R_{M}} \tag{12.91}
\end{equation*}
$$

which reduces to $1 / R_{M}$ if the loop gain is much greater than unity. The input impedance rises by a factor of $1+G_{m} R_{M}$ :

$$
\begin{equation*}
R_{\text {in,closed }}=\frac{1}{g_{m 1}}\left(1+g_{m 1} g_{m 2} R_{D} R_{M}\right) \tag{12.92}
\end{equation*}
$$

and so does the output impedance (i.e., that seen by the laser):

$$
\begin{equation*}
R_{\text {out }, \text { closed }}=\frac{1}{g_{m 2}}\left(1+g_{m 1} g_{m 2} R_{D} R_{M}\right) \tag{12.93}
\end{equation*}
$$

Exercise If an input impedance of $500 \Omega$ and an output impedance of $5 \mathrm{k} \Omega$ are desired, determine the required values of $g_{m 1}$ and $g_{m 2}$. Assume $R_{D}=1 \mathrm{k} \Omega$ and $R_{M}=100 \Omega$.

Example A student attempts to calculate the output impedance of the current-voltage feedback
12.23
topology with the aid of circuit depicted in Fig. 12.43. Explain why this topology is an incorrect representation of the actual circuit.
image_name:Figure 12.43
description:The circuit includes a feedback network with a block labeled K, indicating a feedback path between the output and input. The output current Ix is sensed and fed back to influence the input of the system. The circuit topology suggests a current-voltage feedback configuration.


Solution If sensing the output current, the feedback network must remain in series with the output port of the forward amplifier, and so must the test voltage source. In other words, the output current of the forward system must be equal to both the input current of the feedback network and the current drawn by $V_{X}$ [as in Fig. 12.41(b)]. In the arrangement of Fig. 12.43, however, these principles are violated because $V_{X}$ is placed in parallel with the output. ${ }^{13}$

Exercise Apply the above (incorrect) test to the circuit of Fig. 12.42 and examine the results.

[^1]image_name:Figure 12.45
description:
[
name: Ix, type: CurrentSource, value: Ix, ports: {Np: GND, Nn: Vx}
name: Rin, type: Resistor, value: Rin, ports: {N1: Vx, N2: In(AI)}
name: AI, type: OpAmp, value: AI, ports: {InP: In(AI), InN: GND, OutP: Out(AI)}
name: K, type: Other, ports: {N1: Out(AI), N2: Vx}
]
extrainfo:The circuit diagram shows a feedback system with a current source Ix, a voltage source Vx, a resistor Rin, an operational amplifier AI, and a feedback component K. The current Ix flows into the node Vx, which is connected to the input of the op-amp AI through Rin. The output of AI is connected to the feedback component K, which feeds back to the node Vx.

Figure 12.45 Calculation of input impedance.

For the output impedance, we utilize the test circuit shown in Fig. 12.46, where the input is left open and $V_{X}$ is inserted in series with the output port. Since $I_{F}=K I_{X}$, the forward amplifier produces an output current equal to $-K A_{I} I_{X}$. Noting that $R_{\text {out }}$ carries a current of $V_{X} / R_{\text {out }}$ and writing a KCL at the output node, we have

$$
\begin{equation*}
I_{X}=\frac{V_{X}}{R_{\text {out }}}-K A_{I} I_{X} \tag{12.100}
\end{equation*}
$$

It follows that

$$
\begin{equation*}
\frac{V_{X}}{I_{X}}=R_{\text {out }}\left(1+K A_{I}\right) . \tag{12.101}
\end{equation*}
$$

image_name:Figure 12.46
description:The system block diagram, labeled as Figure 12.46, illustrates the calculation of output impedance in a feedback-controlled circuit. The main components in this diagram include:

1. **Transconductance Amplifier (Gm):** This block is responsible for converting an input voltage to an output current. It is labeled as \( G_m \) and is connected to a resistor \( R_{\text{out}} \).

2. **Feedback Amplifier (K):** This block provides a feedback control mechanism by taking a portion of the output current \( I_X \) and feeding it back as \( I_F \). The feedback amplifier scales the current by a factor \( K \).

3. **Resistor (Rout):** The resistor \( R_{\text{out}} \) is connected in series with the output port and is used to determine the output impedance.

4. **Output Voltage Source (Vx):** The circuit produces an output voltage \( V_X \), which is influenced by the output current \( I_X \) flowing through \( R_{\text{out}} \).

**Flow of Information or Control:**
- The input voltage is applied to the transconductance amplifier \( G_m \), which generates an output current \( I_X \).
- This current flows through the resistor \( R_{\text{out}} \) to produce the output voltage \( V_X \).
- A portion of \( I_X \) is fed back through the feedback amplifier \( K \), which generates the feedback current \( I_F = K I_X \).
- The feedback current \( I_F \) is subtracted from the input at node \( X_4 \), creating a negative feedback loop.

**Labels, Annotations, and Key Indicators:**
- The nodes are labeled as \( X_1, X_2, X_3, \) and \( X_4 \) to indicate points of interest in the circuit.
- The current \( I_X \) and feedback current \( I_F \) are clearly marked to show the direction of current flow.

**Overall System Function:**
The primary function of this system is to regulate the output current delivered to a load, such as a laser diode, by using negative feedback. The feedback mechanism ensures stability and accuracy in the output current by adjusting it based on the feedback signal. The output impedance is calculated as \( R_{\text{out}}(1 + KA_I) \), indicating how the feedback influences the impedance seen by the load.

Figure 12.46 Calculation of output impedance.

Consider the circuit shown in Fig. 12.47(a), where the output current delivered to a
laser diode is regulated by negative feedback. Prove that the feedback is negative and compute the closed-loop gain and I/O impedances if $R_{M}$ is very small and $R_{F}$ very large.
image_name:Figure 12.47(a)
description:
[
name: M1, type: NMOS, ports: {S: S1, D: X, G: Vb}
name: M2, type: PMOS, ports: {S: VDD, D: d2, G: X}
name: RD, type: Resistor, value: RD, ports: {N1: X, N2: VDD}
name: RF, type: Resistor, value: RF, ports: {N1: S1, N2: P}
name: RM, type: Resistor, value: RM, ports: {N1: P, N2: GND}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: GND, Nn: S1}
]
extrainfo:The circuit is a feedback system regulating the output current to a laser diode using NMOS and PMOS transistors. Negative feedback is provided through RF, influencing the source voltage of M1 and the gate voltage of M2.
image_name:Figure 12.47(b)
description:
[
name: M1, type: NMOS, ports: {S: S1, D: X, G: Vb}
name: M2, type: PMOS, ports: {S: VDD, D: d2, G: X}
name: RD, type: Resistor, value: RD, ports: {N1: X, N2: VDD}
name: RF, type: Resistor, value: RF, ports: {N1: S1, N2: GND}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: S1, Nn: GND}
name: Laser, type: Other, ports: {N1: GND, N2: s1}
]
extrainfo:The circuit is a feedback system regulating the output current to a laser diode using NMOS and PMOS transistors. Negative feedback is provided through RF, influencing the source voltage of M1 and the gate voltage of M2.


Solution $\quad$ Suppose $I_{i n}$ increases. Then, the source voltage of $M_{1}$ tends to rise, and so does its drain voltage (why?). As a result, the overdrive of $M_{2}$ decreases, $I_{\text {out }}$ and hence $V_{P}$ fall, and $I_{F}$ increases, thereby lowering the source voltage of $M_{1}$. Since the feedback signal, $I_{F}$, opposes the effect produced by $I_{i n}$, the feedback is negative.

We must now analyze the open-loop system. Since $R_{M}$ is very small, we assume $V_{P}$ remains near zero, arriving at the open-loop circuit depicted in Fig. 12.47(b). The assumption that $R_{F}$ is very large $\left(\gg 1 / g_{m 1}\right)$ indicates that almost all of $I_{i n}$ flows through $M_{1}$ and $R_{D}$, thus generating $V_{X}=I_{i n} R_{D}$ and hence

$$
\begin{align*}
I_{\text {out }} & =-g_{m 2} V_{X}  \tag{12.102}\\
& =-g_{m 2} R_{D} I_{i n} . \tag{12.103}
\end{align*}
$$

That is,

$$
\begin{equation*}
A_{I}=-g_{m 2} R_{D} \tag{12.104}
\end{equation*}
$$

The input impedance is approximately equal to $1 / g_{m 1}$ and the output impedance is equal to $\mathrm{r}_{\mathrm{O} 2}$.

To obtain the closed-loop parameters, we must compute the feedback factor, $I_{F} / I_{\text {out }}$. Recall from Example 12.18 that the current returned by $R_{F}$ can be approximated as $-V_{P} / R_{F}$ if $R_{F} \gg 1 / g_{m 1}$. We also note that $V_{P}=I_{o u t} R_{M}$, concluding that

$$
\begin{align*}
K & =\frac{I_{F}}{I_{\text {out }}}  \tag{12.105}\\
& =\frac{-V_{P}}{R_{F}} \cdot \frac{1}{I_{\text {out }}}  \tag{12.106}\\
& =-\frac{R_{M}}{R_{F}} \tag{12.107}
\end{align*}
$$

The closed-loop parameters are therefore given by:

$$
\begin{align*}
A_{I, \text { closed }} & =\frac{-g_{m 2} R_{D}}{1+g_{m 2} R_{D} \frac{R_{M}}{R_{F}}}  \tag{12.108}\\
R_{\text {in, closed }} & =\frac{1}{g_{m 1}} \cdot \frac{1}{1+g_{m 2} R_{D} \frac{R_{M}}{R_{F}}}  \tag{12.109}\\
R_{\text {out }, \text { closed }} & =r_{02}\left(1+g_{m 2} R_{D} \frac{R_{M}}{R_{F}}\right) . \tag{12.110}
\end{align*}
$$

Note that if $g_{m 2} R_{D} R_{M} / R_{F} \gg 1$, then the closed-loop gain is simply given by $-R_{F} / R_{M}$.
Noting that $\left.R_{\text {out }}\right|_{\text {closed }}$ is the impedance seen by the laser in the closed-loop circuit, construct a Norton equivalent for the entire circuit that drives the laser.
image_name:Figure 12.48 Output impedance falls by 1+ loop gain
description:The diagram consists of four different configurations, illustrating the effect of feedback on input and output impedances in various amplifier setups. Each configuration highlights a specific relationship between the amplifier, feedback, and load.

1. **Top Left Configuration: Output Impedance Falls by 1 + Loop Gain**
- **Components:**
- An amplifier block labeled \(A_0\) with an output \(V_{out}\).
- A feedback element labeled \(K\) connected to a load.
- **Flow of Information:**
- The output \(V_{out}\) of the amplifier \(A_0\) is fed back through the feedback element \(K\) to the load.
- The feedback reduces the output impedance by a factor of \(1 + \text{loop gain}\).
- **Function:**
- This setup decreases the output impedance, improving the ability to drive the load.

2. **Top Right Configuration: Output Impedance Rises by 1 + Loop Gain**
- **Components:**
- An amplifier block labeled \(A_I\) with an output current \(I_{out}\).
- A feedback element labeled \(K\) connected to a load.
- **Flow of Information:**
- The output current \(I_{out}\) from the amplifier \(A_I\) is fed back through the feedback element \(K\).
- The feedback increases the output impedance by a factor of \(1 + \text{loop gain}\).
- **Function:**
- This configuration increases the output impedance, which may be useful in current source applications.

3. **Bottom Left Configuration: Input Impedance Rises by 1 + Loop Gain**
- **Components:**
- An input voltage \(V_{in}\) is fed into a summing junction.
- An amplifier block labeled \(A_0\) and a feedback element \(K\) connected to a load.
- **Flow of Information:**
- The input voltage \(V_{in}\) is compared with a feedback signal \(X_2\) in the summing junction.
- The feedback increases the input impedance by a factor of \(1 + \text{loop gain}\).
- **Function:**
- This setup is beneficial for applications requiring high input impedance.

4. **Bottom Right Configuration: Input Impedance Falls by 1 + Loop Gain**
- **Components:**
- An input current \(I_{in}\) source connected to ground.
- An amplifier block labeled \(A_I\) and a feedback element \(K\) connected to a load.
- **Flow of Information:**
- The input current \(I_{in}\) is fed into the system, with feedback \(I_F\) affecting the input impedance.
- The feedback decreases the input impedance by a factor of \(1 + \text{loop gain}\).
- **Function:**
- This configuration is useful for applications requiring low input impedance.

Overall, the diagram demonstrates how feedback can be used to manipulate the input and output impedances of amplifier systems, either increasing or decreasing them depending on the configuration and application needs.
image_name:Figure 12.48 Output impedance rises by 1+ loop gain
description:The system block diagram titled "Output impedance rises by 1+ loop gain" illustrates the effect of feedback on both input and output impedances in a feedback amplifier system. The diagram consists of four separate parts, each demonstrating different scenarios of impedance changes due to feedback.

Top Left Block:
- **Components:**
- Amplifier labeled as \(A_0\).
- Feedback network labeled as \(K\).
- Load connected to the output.
- **Flow of Information:**
- The output voltage \(V_{out}\) from \(A_0\) is fed back through the network \(K\) to the input.
- **Function:**
- Demonstrates that the output impedance falls by a factor of \(1 + \text{loop gain}\).

Top Right Block:
- **Components:**
- Amplifier labeled as \(A_I\).
- Feedback network labeled as \(K\).
- Load connected to the output.
- **Flow of Information:**
- The output current \(I_{out}\) is fed back through the network \(K\).
- **Function:**
- Illustrates that the output impedance rises by a factor of \(1 + \text{loop gain}\).

Bottom Left Block:
- **Components:**
- Summing junction combining input \(V_{in}\) and feedback signal \(X_2\).
- Amplifier labeled as \(A_0\).
- Feedback network labeled as \(K\).
- Load connected to the output.
- **Flow of Information:**
- The input voltage \(V_{in}\) is modified by the feedback signal \(X_2\) before being amplified.
- **Function:**
- Shows that the input impedance rises by a factor of \(1 + \text{loop gain}\).

Bottom Right Block:
- **Components:**
- Amplifier labeled as \(A_I\).
- Feedback network labeled as \(K\).
- Load connected to the output.
- Current input source \(I_{in}\).
- **Flow of Information:**
- The input current \(I_{in}\) is influenced by feedback current \(I_F\).
- **Function:**
- Indicates that the input impedance falls by a factor of \(1 + \text{loop gain}\).

Overall System Function:
The diagram collectively illustrates how feedback affects the input and output impedances in different configurations of amplifier systems. It highlights that feedback can either increase or decrease impedance depending on the specific configuration and type of feedback loop employed.
image_name:Figure 12.48 Input impedance rises by 1+ loop gain
description:The system block diagram titled "Input impedance rises by 1+ loop gain" illustrates the effect of feedback on input and output impedances in a circuit. It consists of four separate configurations, each demonstrating different feedback effects on impedance.

1. **Top Left Configuration:**
- **Components:**
- An amplifier block labeled \(A_0\) is connected to a feedback amplifier labeled \(K\).
- A load is connected to the output of the feedback amplifier.
- **Function:**
- The output impedance decreases by a factor of \(1 + \text{loop gain}\).
- This configuration shows how feedback can reduce output impedance, enhancing the ability to drive loads.

2. **Top Right Configuration:**
- **Components:**
- An amplifier block labeled \(A_I\) with a feedback amplifier labeled \(K\).
- A load is connected to the output of the feedback amplifier.
- **Function:**
- The output impedance increases by a factor of \(1 + \text{loop gain}\).
- This setup demonstrates how feedback can increase output impedance, which might be used for specific applications requiring high output impedance.

3. **Bottom Left Configuration:**
- **Components:**
- An input summing junction with inputs \(V_{in}\), \(X_1\), and \(X_2\).
- Amplifier block \(A_0\) and feedback amplifier \(K\) with a load.
- **Function:**
- The input impedance increases by a factor of \(1 + \text{loop gain}\).
- This illustrates how feedback can enhance input impedance, potentially reducing loading effects on the source.

4. **Bottom Right Configuration:**
- **Components:**
- An amplifier block \(A_I\) with a feedback amplifier \(K\), connected to a load.
- An input current source \(I_{in}\) and feedback current \(I_F\) with ground reference.
- **Function:**
- The input impedance decreases by a factor of \(1 + \text{loop gain}\).
- This configuration shows how feedback can reduce input impedance, which might be beneficial in certain low-impedance applications.

Overall, the diagram effectively demonstrates the impact of feedback on both input and output impedances, highlighting how different feedback configurations can be used to tailor impedance characteristics for specific circuit requirements.
image_name:Figure 12.48 Input impedance falls by 1+ loop gain
description:The system block diagram illustrates the effect of feedback on input and output impedances in a circuit, with a focus on how these impedances change with the loop gain.

Main Components:
1. **Amplifiers (A0 and AI):**
- These are the primary amplifying elements in the circuits, denoted as blocks labeled A0 and AI.
- They serve to amplify the input signals, with A0 associated with voltage amplification and AI with current amplification.

2. **Feedback Amplifier (K):**
- This block, marked as K, is responsible for providing feedback to the system.
- It influences the overall loop gain and subsequently affects the input and output impedances.

3. **Load:**
- Represented by the term "LOAD," indicating where the output is delivered or where the input is received.

4. **Input and Output Nodes (Vout, Iout, Vin, X):**
- These nodes indicate where the input is applied and where the output is taken.

Flow of Information or Control:
- **Top Left Diagram:**
- The signal flows from the amplifier A0 to the output node Vout. The feedback loop through amplifier K reduces the output impedance by a factor of 1 plus the loop gain.

- **Top Right Diagram:**
- The signal flows from the amplifier AI to the output node X. The feedback through amplifier K increases the output impedance by a factor of 1 plus the loop gain.

- **Bottom Left Diagram:**
- The input signal Vin is applied to a summing junction, which feeds into amplifier A0. The feedback loop through amplifier K increases the input impedance by a factor of 1 plus the loop gain.

- **Bottom Right Diagram:**
- The input current Iin flows into the node X and through amplifier AI. The feedback loop through amplifier K reduces the input impedance by a factor of 1 plus the loop gain.

Labels, Annotations, and Key Indicators:
- **Loop Gain Effect:**
- Each diagram is annotated to indicate whether the impedance (input or output) is rising or falling due to the loop gain.

Overall System Function:
The primary function of the system is to demonstrate how feedback can modify the input and output impedances of amplifiers. By introducing a feedback loop through amplifier K, the circuit can either increase or decrease these impedances depending on the configuration, thus affecting the performance and stability of the system in practical applications. The diagrams collectively show the versatility of feedback in controlling impedance characteristics in electronic circuits.

Figure 12.48 Effect of feedback on input and output impedances.

The effect of feedback on the input and output impedances of the forward amplifier is summarized in Fig. 12.48.

## 12.7 EFFECT OF NONIDEAL I/O IMPEDANCES

Our study of feedback topologies in Section 12.6 has been based on idealized models for the feedback network, always assuming that the I/O impedances of this network are very large or very small depending on the type of feedback. In practice, however, the finite I/O impedances of the feedback network may considerably alter the performance of the circuit, thereby necessitating analysis techniques to account for these effects. In such cases, we say the feedback network "loads" the forward amplifier and the "loading effects" must be determined.

Before delving into the analysis, it is instructive to understand the difficulty in the context of an example.

Example 12.25

Suppose in the circuit of Example 12.7, $R_{1}+R_{2}$ is not much greater than $R_{D}$. How should we analyze the circuit?

Solution In Example 12.7, we constructed the open-loop circuit by simply neglecting the effect of $R_{1}+R_{2}$. Here, on the other hand, $R_{1}+R_{2}$ tends to reduce the open-loop gain because it appears in parallel with $R_{D}$. We therefore surmise that the open-loop circuit must be configured as shown in Fig. 12.49, with the open-loop gain given by

$$
\begin{equation*}
A_{O}=g_{m 1}\left[R_{D} \|\left(R_{1}+R_{2}\right)\right] \tag{12.111}
\end{equation*}
$$

and the output impedance

$$
\begin{equation*}
R_{\text {out }, \text { open }}=R_{D} \|\left(R_{1}+R_{2}\right) \tag{12.112}
\end{equation*}
$$

image_name:Figure 12.49
description:
[
name: M1, type: NMOS, ports: {S: Vin, D: Vout, G: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: X}
name: R2, type: Resistor, value: R2, ports: {N1: X, N2: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a common-source NMOS amplifier with feedback resistors R1 and R2. The output is taken across the drain of the NMOS transistor M1. The resistors R1 and R2 form a voltage divider that provides feedback to stabilize the gain.
Other forward and feedback parameters are identical to those calculated in Example 12.7. Thus,

$$
\begin{align*}
A_{v, \text { closed }} & =\frac{g_{m 1}\left[R_{D} \|\left(R_{1}+R_{2}\right)\right]}{1+\frac{R_{2}}{R_{1}+R_{2}} g_{m 1}\left[R_{D} \|\left(R_{1}+R_{2}\right)\right]}  \tag{12.113}\\
R_{\text {in,closed }} & =\frac{1}{g_{m 1}}\left\{1+\frac{R_{2}}{R_{1}+R_{2}} g_{m 1}\left[R_{D} \|\left(R_{1}+R_{2}\right)\right]\right\}  \tag{12.114}\\
R_{\text {out,closed }} & =\frac{R_{D} \|\left(R_{1}+R_{2}\right)}{1+\frac{R_{2}}{R_{1}+R_{2}} g_{m 1}\left[R_{D} \|\left(R_{1}+R_{2}\right)\right]} \tag{12.115}
\end{align*}
$$

Exercise Repeat the above example if $R_{D}$ is replaced with an ideal current source.

The above example easily lends itself to intuitive inspection. But many other circuits do not. To gain more confidence in our analysis and deal with more complex circuits, we must develop a systematic approach.

### 12.7.1 Inclusion of I/O Effects

We present a methodology here that allows the analysis of the four feedback topologies even if the I/O impedances of the forward amplifier or the feedback network depart from their ideal values. The methodology is based on a formal proof that is somewhat beyond the scope of this book and can be found in [1].

Our methodology proceeds in six steps:

1. Identify the forward amplifier.
2. Identify the feedback network.
3. Break the feedback network according to the rules described below.
4. Calculate the open-loop parameters.
5. Determine the feedback factor according to the rules described below.
6. Calculate the closed-loop parameters.

Rules for Breaking the Feedback Network The third step is carried out by "duplicating" the feedback network at both the input and the output of the overall system.
image_name:Figure 12.50
description:The system block diagram in Figure 12.50 illustrates a feedback loop methodology for analyzing a control system.

Main Components:
1. **Summing Junction (+/-):**
- This is where the input signal (X) and feedback signal are combined. The feedback signal is subtracted from the input signal.

2. **Forward Amplifier (A1):**
- Labeled as A1, this block represents the main amplifier in the system, responsible for amplifying the input signal after it has been processed by the summing junction.

3. **Feedback Network:**
- Composed of two blocks, K1 and K2, which are amplifiers or transfer functions representing parts of the feedback network.
- **K1 (Return Duplicate):** Positioned after the summing junction, it processes the output of the summing junction and feeds it back into the input.
- **K2 (Sense Duplicate):** Positioned to sense the output of A1 and feed a portion of it back into the summing junction.

Flow of Information or Control:
- The input signal X is fed into the summing junction, where it is combined with the feedback signal. The result is then passed to the forward amplifier A1.
- The output of A1 is the system output Y, which is also fed into the feedback network.
- In the feedback network, the output is processed by K2 (Sense Duplicate) and a portion is fed back to the input through K1 (Return Duplicate).

Labels, Annotations, and Key Indicators:
- **In (A1):** Indicates the input to the forward amplifier.
- **Out (K1) and Out (K2):** Indicate the outputs of the respective feedback components.
- The diagram uses arrows to indicate the direction of signal flow, and question marks suggest areas where connections or configurations might vary or need to be determined.

Overall System Function:
The primary function of this system is to control the output Y by adjusting the feedback network. By breaking the feedback loop and analyzing it with duplicates, the system can be better understood and optimized. The methodology ensures that both the input and output of the forward amplifier are correctly loaded, which is essential for accurate performance analysis and control optimization. This setup allows for the calculation of open-loop and closed-loop parameters, crucial for determining system stability and performance.

Figure 12.50 Method of breaking the feedback loop.

Illustrated in Fig. 12.50, the idea is to "load" both the input and the output of the forward amplifier by proper copies of the feedback network. The copy tied to the output is called the "sense duplicate" and that connected to the input, the "return duplicate." We must also decide what to do with the output port of the former and the input port of the latter, i.e., whether to short or open these ports. This is accomplished through the use of the "termination" rules depicted in Fig. 12.51. For example, for voltage-voltage feedback [Fig. 12.51(a)], the output port of the sense replica is left open while the input of the return duplicate is shorted. Similarly, for voltage-current feedback [Fig. 12.51(b)], both the output port of the sense duplicate and the input port of the return duplicate are shorted.

The formal proof of these concepts is given in [1] but it is helpful to remember these rules based on the following intuitive (but not quite rigorous) observations. In an ideal situation, a feedback network sensing an output voltage is driven by a zero impedance, namely, the output impedance of the forward amplifier. Thus, the input port of the return duplicate is shorted. Moreover, a feedback network returning a voltage to the input ideally sees an infinite impedance, namely, the input impedance of the forward amplifier. Thus, the output port of the sense duplicate is left open. Similar observations apply to the other three cases.
image_name:Figure 12.51 (a)
description:The diagram labeled "(a)" illustrates a voltage-voltage feedback system consisting of several key components and connections:

1. **Main Components:**
- **Summing Junction (+/-):** This is where the input voltage \( V_{in} \) is applied. It compares the input voltage with the feedback voltage.
- **Amplifier \( A_0 \):** This block represents the forward amplifier with a gain \( A_0 \). It amplifies the input signal from the summing junction to produce the output voltage \( V_{out} \).
- **Feedback Network (K):** The feedback path includes an amplifier with gain \( K \). This network samples the output voltage and feeds a portion back to the summing junction.

2. **Flow of Information or Control:**
- The input voltage \( V_{in} \) is fed into the positive terminal of the summing junction.
- The feedback voltage from the output is fed back into the negative terminal of the summing junction through the feedback network \( K \).
- The amplified signal from \( A_0 \) is the output voltage \( V_{out} \), which is also the point where the feedback is taken.

3. **Labels, Annotations, and Key Indicators:**
- The summing junction is annotated with \( V_{in} \) and the feedback path is labeled \( Out(K) \), indicating the point where the feedback network outputs its signal.
- The amplifier \( A_0 \) has its input labeled as \( In(A_0) \) and its output as \( V_{out} \).
- The feedback network is labeled \( K \) with its output connected to ground when open, indicating the condition for proper termination.

4. **Overall System Function:**
- The primary function of this system is to maintain a stable output voltage \( V_{out} \) by using negative feedback. The feedback network samples the output and adjusts the input signal at the summing junction to minimize the difference between \( V_{in} \) and the feedback voltage. This configuration helps stabilize the gain and bandwidth of the amplifier \( A_0 \), ensuring consistent performance in the presence of variations in input or load conditions.
image_name:Figure 12.51 (b)
description:**Main Components:**
1. **Current Source (I_in):** Provides the input current to the system.
2. **Summing Junction (X_1):** Combines the input current with feedback current (I_F).
3. **Amplifier (R_0):** Amplifies the combined current from the summing junction to produce the output voltage (V_out).
4. **Feedback Network (K):** Two feedback paths with amplifiers labeled 'K' that process the feedback current.

**Flow of Information or Control:**
- The input current (I_in) enters the system at the current source and flows to the summing junction (X_1).
- At the summing junction, the input current is combined with the feedback current (I_F) from the feedback network.
- The combined current is then fed into the amplifier (R_0), which processes the current to produce an output voltage (V_out).
- The output voltage (V_out) is then fed back into the system through the feedback network.
- The feedback network consists of two amplifiers labeled 'K'. These amplifiers process the feedback current (I_F) which is grounded, indicating that the feedback loop is closed through the ground.

**Labels, Annotations, and Key Indicators:**
- **I_in:** Input current.
- **I_F:** Feedback current.
- **V_out:** Output voltage.
- **GND:** Ground symbol indicating where certain parts of the system are grounded.
- **K:** Amplifiers in the feedback network.

**Overall System Function:**
The system in diagram (b) is a voltage-current feedback system. It takes an input current and combines it with feedback current at the summing junction. This combined current is then amplified to produce an output voltage. The feedback network, consisting of amplifiers, processes the feedback current to influence the input current, thereby creating a feedback loop that helps stabilize or control the output voltage. The grounding in the feedback network indicates a specific configuration for proper functioning of the feedback mechanism.
image_name:Figure 12.51 (c)
description:The diagram labeled (c) illustrates a current-current feedback system. Here's a detailed description of the system block diagram:

1. **Main Components:**
- **Current Source (I_in):** This is the input current source labeled as \( I_{in} \) which provides the input current to the system.
- **Amplifier (A_I):** The block labeled \( A_I \) represents the main amplifier in the system. It processes the input current and produces an output current \( I_{out} \).
- **Feedback Network (K):** Two blocks labeled \( K \) are part of the feedback network. These are used to sense and return the current in the feedback loop.

2. **Flow of Information or Control:**
- The input current \( I_{in} \) enters the system and is fed into the amplifier \( A_I \).
- The amplifier \( A_I \) processes this current and produces an output current \( I_{out} \).
- The output current \( I_{out} \) is then fed back to the input through the feedback network.
- The feedback network consists of two paths: one path senses the output current \( I_{out} \) and the other path returns a feedback current \( I_F \) to the input.
- The sense duplicate in the feedback network is left open, which means it does not load the output, while the return duplicate is grounded, ensuring proper feedback.

3. **Labels, Annotations, and Key Indicators:**
- The input and output ports are labeled \( In(A_I) \) and \( Out(A_I) \) respectively.
- The feedback current is labeled \( I_F \).
- The grounding symbols indicate where the circuit is connected to the ground.

4. **Overall System Function:**
- The primary function of this system is to control and stabilize the current output by using a feedback mechanism. The feedback network ensures that any changes in the output current are sensed and corrected by adjusting the input current, maintaining a stable output.
- The open and grounded states of the feedback network components are crucial for achieving the desired feedback characteristics, ensuring that the system operates efficiently without unwanted loading or interference.
image_name:Figure 12.51 (d)
description:### System Block Diagram (d): Current-Voltage Feedback

1. **Main Components:**
- **Input Summing Node:** Combines the input voltage \( V_{in} \) with a feedback signal. This is the point where the input signal and feedback are compared.
- **Transconductance Amplifier (\( G_m \)):** Converts the input voltage difference into an output current \( I_{out} \). It is labeled as \( G_m \) and is a key part of the current-to-voltage feedback system.
- **Feedback Amplifiers (\( K \)):** Two identical amplifiers labeled \( K \) are used in the feedback network. These amplifiers have their outputs open, indicating that they are used to sense the current and provide feedback.

2. **Flow of Information or Control:**
- The input voltage \( V_{in} \) is applied to the positive terminal of the summing node, while the feedback signal is applied to the negative terminal.
- The difference between \( V_{in} \) and the feedback signal is fed into the transconductance amplifier \( G_m \), which converts this voltage difference into a current \( I_{out} \).
- The output current \( I_{out} \) is then used to generate a feedback signal through the feedback amplifiers \( K \), which are configured to sense the output current.
- The feedback loop is closed by feeding the sensed signal back into the summing node.

3. **Labels, Annotations, and Key Indicators:**
- \( V_{in} \) is labeled at the input.
- \( I_{out} \) is labeled at the output of the transconductance amplifier.
- The feedback amplifiers \( K \) have their outputs labeled as "Open," indicating that they are not directly contributing to the output but are part of the sensing mechanism.
- The input and output of the transconductance amplifier are labeled \( In(G_m) \) and \( Out(G_m) \) respectively.

4. **Overall System Function:**
- The system primarily functions as a current-to-voltage feedback loop. The transconductance amplifier \( G_m \) plays a crucial role by converting the input voltage difference into an output current, which is then fed back into the system to control the input summing node. The open configuration of the feedback amplifiers \( K \) ensures that they only sense the current without loading the system. This setup allows for precise control of the output current based on the input voltage, maintaining stability and accuracy in the feedback loop.

Figure 12.51 Proper termination of duplicates in (a) voltage-voltage, (b) voltagecurrent, (c) current-current, and (d) current-voltage feedback.

Solution We identify the forward system as $M_{1}$ and $R_{D}$, and the feedback network as $R_{1}$ and $R_{2}$. We construct the open-loop circuit according to Fig. 12.51(a), as shown in Fig. 12.53(b). Note that the feedback network appears twice. The sense duplicate output port is left open and the input port of the return duplicate is shorted. The open-loop parameters of this topology were computed in Example 12.25.

To determine the feedback factor, we follow the rule in Fig. 12.52(a) to form the circuit shown in Fig. 12.53(c), arriving at

$$
\begin{align*}
K & =\frac{V_{2}}{V_{1}}  \tag{12.116}\\
& =\frac{R_{2}}{R_{1}+R_{2}} . \tag{12.117}
\end{align*}
$$

It follows that

$$
\begin{equation*}
K A_{0}=\frac{R_{2}}{R_{1}+R_{2}} g_{m 1}\left[R_{D} \|\left(R_{1}+R_{2}\right)\right] \tag{12.118}
\end{equation*}
$$

and hence

$$
\begin{align*}
A_{v, \text { closed }} & =\frac{g_{m 1}\left[R_{D} \|\left(R_{1}+R_{2}\right)\right]}{1+\frac{R_{2}}{R_{1}+R_{2}} g_{m 1}\left[R_{D} \|\left(R_{1}+R_{2}\right)\right]}  \tag{12.119}\\
R_{\text {in,closed }} & =\frac{1}{g_{m 1}}\left\{1+\frac{R_{2}}{R_{1}+R_{2}} g_{m 1}\left[R_{D} \|\left(R_{1}+R_{2}\right)\right]\right\}  \tag{12.120}\\
R_{\text {out }, \text { closed }} & =\frac{R_{D} \|\left(R_{1}+R_{2}\right)}{1+\frac{R_{2}}{R_{1}+R_{2}} g_{m 1}\left[R_{D} \|\left(R_{1}+R_{2}\right)\right]} \tag{12.121}
\end{align*}
$$

Obtained through our general methodology, these results agree with those found by inspection in Example 12.25.

Exercise Repeat the above analysis if $R_{D}$ is replaced with an ideal current source.

Analyze the circuit of Fig. 12.54(a) if $R_{1}+R_{2}$ is not much greater than $r_{O P} \| r_{O N}$.
image_name:Figure 12.54 (a)
description:
[
name: M1, type: NMOS, ports: {S: s1s2, D: X, G: Vin}
name: M2, type: NMOS, ports: {S: s1s2, D: Vout, G: X}
name: M3, type: PMOS, ports: {S: VDD, D: X, G: X}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: X}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: g2}
name: R2, type: Resistor, value: R2, ports: {N1: g2, N2: GND}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: s1s2, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with NMOS and PMOS transistors. M1 and M2 form the differential pair, while M3 and M4 act as active loads. The current source Iss provides biasing. Vout is the output node connected through resistors R1 and R2 to ground.

image_name:Figure 12.54 (b)
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin}
name: M2, type: NMOS, ports: {S: P, D: Vout, G: g2}
name: M3, type: PMOS, ports: {S: VDD, D: X, G: X}
name: M4, type: PMOS, ports: {S: VDD, D: Vout, G: X}
name: R1, type: Resistor, value: R1, ports: {N1: g2, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: g2, N2: GND}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: P, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: Open}
name: R2, type: Resistor, value: R2, ports: {N1: open, N2: GND}
]
extrainfo:The circuit is a differential amplifier with NMOS and PMOS transistors. M1 and M2 form the differential pair, while M3 and M4 act as active loads. The current source Iss provides biasing. Vout is the output node connected through resistors R1 and R2 to ground. The loop is broken for feedback analysis.
Solution Here, $M_{1}-M_{4}$ constitute the forward amplifier, and $R_{1}$ and $R_{2}$ the feedback network. The loop is broken in a manner similar to that in Example 12.26 because the type of feedback is the same [Fig. 12.54(b)]. The open-loop parameters are therefore given by

$$
\begin{align*}
A_{0} & =g_{m N}\left[r_{O N}\left\|r_{O P}\right\|\left(R_{1}+R_{2}\right)\right]  \tag{12.122}\\
R_{\text {in,open }} & =\infty  \tag{12.123}\\
R_{\text {out,open }} & =r_{O N}\left\|r_{O P}\right\|\left(R_{1}+R_{2}\right) . \tag{12.124}
\end{align*}
$$

The test circuit for calculation of the feedback factor is identical to that in Fig. 12.53(c), yielding

$$
\begin{equation*}
K=\frac{R_{2}}{R_{1}+R_{2}} \tag{12.125}
\end{equation*}
$$

It follows that

$$
\begin{align*}
\left.\frac{V_{\text {out }}}{V_{\text {in }}}\right|_{\text {closed }} & =\frac{g_{m N}\left[r_{O N}\left\|r_{O P}\right\|\left(R_{1}+R_{2}\right)\right]}{1+\frac{R_{2}}{R_{1}+R_{2}} g_{m N}\left[r_{O N}\left\|r_{O P}\right\|\left(R_{1}+R_{2}\right)\right]}  \tag{12.126}\\
R_{\text {in }, \text { closed }} & =\infty  \tag{12.127}\\
R_{\text {out }, \text { closed }} & =\frac{r_{O N}\left\|r_{O P}\right\|\left(R_{1}+R_{2}\right)}{1+\frac{R_{2}}{R_{1}+R_{2}} g_{m N}\left[r_{O N}\left\|r_{O P}\right\|\left(R_{1}+R_{2}\right)\right]} \tag{12.128}
\end{align*}
$$

Exercise Repeat the above example if a load resistor of $R_{L}$ is tied between the output of the circuit and ground.

Example
12.28 Analyze the circuit of Fig. 12.55(a).
image_name:Fig. 12.55(a)
description:
[
name: M1, type: NMOS, ports: {S: s1, D: d1g2, G: Vin}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: d1g2}
name: RD1, type: Resistor, value: RD1, ports: {N1: d1g2, N2: VDD}
name: RD2, type: Resistor, value: RD2, ports: {N1: Vout, N2: VDD}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: s1}
name: R2, type: Resistor, value: R2, ports: {N1: s1, N2: GND}
]
extrainfo:The circuit is a feedback amplifier with transistors M1 and M2, and resistors RD1, RD2, R1, and R2. It uses a switch S1 for grounding. The feedback network returns a voltage to the source of M1.
image_name:Fig. 12.55(b)
description:
[
name: M1, type: NMOS, ports: {S: s1, D: X, G: Vin}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: X}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: X}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: Vout}
name: R1, type: Resistor, value: R1, ports: {N1: s1, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: s1, N2: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: s1}
name: R2, type: Resistor, value: R2, ports: {N1: s1, N2: GND}
]
extrainfo:The circuit is an amplifier with a feedback network consisting of resistors R1 and R2. M1 and M2 are NMOS transistors forming the core of the amplifier. RD1 and RD2 are load resistors connected to VDD. The feedback network is connected between the output and the source of M1.

Figure 12.55

We identify the forward system as $M_{1}, R_{D 1}, M_{2}$, and $R_{D 2}$. The feedback network consists of $R_{1}$ and $R_{2}$ and returns a voltage to the source of the subtracting transistor, $M_{1}$. In a manner similar to the above two examples, the open-loop circuit is constructed as shown in Fig. 12.55(b). Note that $M_{1}$ is now degenerated by $R_{1} \| R_{2}$. Writing $A_{0}=\left(V_{X} / V_{\text {in }}\right)\left(V_{\text {out }} / V_{X}\right)$, we have

$$
\begin{align*}
A_{0} & =\frac{-R_{D 1}}{\frac{1}{g_{m}}+R_{1} \| R_{2}} \cdot\left\{-g_{m 2}\left[R_{D 2} \|\left(R_{1}+R_{2}\right)\right]\right\}  \tag{12.129}\\
R_{\text {in,open }} & =\infty  \tag{12.130}\\
R_{\text {out }, \text { open }} & =R_{D 2} \|\left(R_{1}+R_{2}\right) . \tag{12.131}
\end{align*}
$$

As in the above example, the feedback factor is equal to $R_{2} /\left(R_{1}+R_{2}\right)$, yielding

$$
\begin{align*}
\left.\frac{V_{\text {out }}}{V_{\text {in }}}\right|_{\text {closed }} & =\frac{A_{0}}{1+\frac{R_{2}}{R_{1}+R_{2}} A_{0}}  \tag{12.132}\\
R_{\text {in }, \text { closed }} & =\infty  \tag{12.133}\\
R_{\text {out }, \text { closed }} & =\frac{R_{D 2} \|\left(R_{1}+R_{2}\right)}{1+\frac{R_{2}}{R_{1}+R_{2}} A_{0}} \tag{12.134}
\end{align*}
$$

where $A_{0}$ is given by Eq. (12.129).

Exercise Repeat the above example if $M_{2}$ is degenerated by a resistor of value $R_{S}$.

Analyze the circuit of Fig. 12.56(a), assuming that $R_{F}$ is not very large.
image_name:Fig. 12.56(a)
description:The circuit diagram is complex and involves feedback topology with a forward amplifier formed by M1, RD1, M2, and RD2, and a feedback network consisting of RF. The loop is opened for analysis, and the output port of the sense duplicate is shorted. The circuit is analyzed as a voltage-current feedback topology.

As a voltage-current feedback topology, this circuit must be handled according to the rules in Figs. 12.51(b) and 12.52(b). The forward amplifier is formed by $M_{1}, R_{D 1}, M_{2}$, and $R_{D 2}$. The feedback network simply consists of $R_{F}$. The loop is opened as shown in Fig. 12.56(b), where, from Fig. 12.51(b), the output port of the sense duplicate is shorted. Since $I_{i n}$ splits between $R_{F}$ and $M_{1}$, we have

$$
\begin{equation*}
V_{X}=I_{i n} \frac{R_{F} R_{D 1}}{R_{F}+\frac{1}{g_{m 1}}} \tag{12.135}
\end{equation*}
$$

Noting that $R_{0}=V_{\text {out }} / I_{\text {in }}=\left(V_{X} / I_{\text {in }}\right)\left(V_{\text {out }} / V_{X}\right)$, we write

$$
\begin{equation*}
R_{0}=\frac{R_{F} R_{D 1}}{R_{F}+\frac{1}{g_{m 1}}} \cdot\left[-g_{m 2}\left(R_{D 2} \| R_{F}\right)\right] \tag{12.136}
\end{equation*}
$$

The open-loop input and output impedances are respectively given by

$$
\begin{align*}
R_{\text {in,open }} & =\frac{1}{g_{m 1}} \| R_{F}  \tag{12.137}\\
R_{\text {out }, \text { open }} & =R_{D 2} \| R_{F} \tag{12.138}
\end{align*}
$$

To obtain the feedback factor, we follow the rule in Fig. 12.52(b) and construct the test circuit shown in Fig. 12.56(c), obtaining

$$
\begin{align*}
K & =\frac{I_{2}}{V_{1}}  \tag{12.139}\\
& =-\frac{1}{R_{F}} \tag{12.140}
\end{align*}
$$

Note that both $R_{0}$ and $K$ are negative here, yielding a positive loop gain and hence confirming that the feedback is negative. The closed-loop parameters are thus expressed as

$$
\begin{align*}
\left.\frac{V_{\text {out }}}{I_{\text {in }}}\right|_{\text {closed }} & =\frac{R_{0}}{1-\frac{R_{0}}{R_{F}}}  \tag{12.141}\\
R_{\text {in }, \text { closed }} & =\frac{\frac{1}{g_{m 1}} \| R_{F}}{1-\frac{R_{0}}{R_{F}}}  \tag{12.142}\\
R_{\text {out }, \text { closed }} & =\frac{R_{D 2} \| R_{F}}{1-\frac{R_{0}}{R_{F}}} \tag{12.143}
\end{align*}
$$

where $R_{0}$ is given by Eq. (12.136).

Exercise Repeat the above example if $R_{D 2}$ is replaced with an ideal current source.

Example
12.30

Analyze the circuit of Fig. 12.57(a), assuming $R_{M}$ is not small, $r_{O 1}<\infty$, and the laser diode has an impedance of $R_{L}$.
image_name:Figure 12.57 (a)
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: d1, G: X}
name: M5, type: PMOS, ports: {S: VDD, D: X, G: Y}
name: M6, type: PMOS, ports: {S: VDD, D: Y, G: Y}
name: M3, type: NMOS, ports: {S: s3s4, D: X, G: Vin}
name: M4, type: NMOS, ports: {S: s3s4, D: Y, G: g4}
name: ISS, type: CurrentSource, value: I_ss, ports: {Np: s3s4, Nn: GND}
name: RM, type: Resistor, value: RM, ports: {N1: g4, N2: GND}
]
extrainfo:The circuit employs a combination of PMOS and NMOS transistors to control a laser diode. The PMOS transistors (M1, M5, M6) are connected to the VDD, while the NMOS transistors (M3, M4) are connected to the ground. A current source (S354) provides biasing current to the NMOS transistors. The laser diode is connected in series with a resistor (RM) to ground.

image_name:Figure 12.57 (b)
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: d1, G: X}
name: M5, type: PMOS, ports: {S: VDD, D: X, G: Y}
name: M6, type: PMOS, ports: {S: VDD, D: Y, G: Y}
name: M3, type: NMOS, ports: {S: s3s4, D: X, G: Vin}
name: M4, type: NMOS, ports: {S: s3s4, D: Y, G: g4}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: s3s4, Nn: GND}
name: rO1, type: Resistor, value: rO1, ports: {N1: d1, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: d1, N2: k}
name: RM, type: Resistor, value: RM, ports: {N1: k, N2: GND}
name: RM, type: Resistor, value: RM, ports: {N1: g4, N2: GND}
]
extrainfo:The circuit employs a combination of PMOS and NMOS transistors to control a laser diode. The PMOS transistors (M1, M5, M6) are connected to VDD, while the NMOS transistors (M3, M4) are connected to ground. A current source (ISS) provides biasing current to the NMOS transistors. The laser diode is connected in series with a resistor (RM) to ground. The forward amplifier is formed by M1 and M3-M6, and the feedback network consists of RM.

image_name:Figure 12.57(c)
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: d1, G: X}
name: M5, type: PMOS, ports: {S: VDD, D: X, G: Y}
name: M6, type: PMOS, ports: {S: VDD, D: Y, G: Y}
name: M3, type: NMOS, ports: {S: s3s4, D: X, G: Vin}
name: M4, type: NMOS, ports: {S: s3s4, D: Y, G: g4}
name: I_SS, type: CurrentSource, ports: {Np: s3s4, Nn: GND}
name: R_M, type: Resistor, value: R_M, ports: {N1: g4, N2: GND}
name: r_o1, type: Resistor, value: r_o1, ports: {N1: d1, N2: GND}
name: V_x, type: VoltageSource, value: V_x, ports: {Np: d1, Nn: K}
name: R_M, type: Resistor, value: R_M, ports: {N1: k, N2: GND}
]
extrainfo:The circuit employs PMOS and NMOS transistors to control a laser diode. The PMOS transistors (M1, M5, M6) connect to VDD, and the NMOS transistors (M3, M4) connect to ground. A current source (ISS) provides biasing to the NMOS transistors. The laser diode is in series with a resistor (RM) to ground. The forward amplifier is formed by M1 and M3-M6, with RM as the feedback network.

Solution
This circuit employs current-voltage feedback and must be opened according to the rules shown in Figs. 12.51(d) and 12.52(d). The forward amplifier is formed by $M_{1}$ and $M_{3}-M_{6}$, and the feedback network consists of $R_{M}$. Depicted in Fig. 12.52(d), the openloop circuit contains two instances of the feedback network, with the output port of the sense duplicate and the input port of the return duplicate left open. The open-loop gain $G_{m}=I_{\text {out }} / V_{\text {in }}=\left(V_{X} / V_{\text {in }}\right)\left(I_{\text {out }} / V_{X}\right)$, and

$$
\begin{equation*}
\frac{V_{X}}{V_{i n}}=-g_{m 3}\left(r_{O 3} \| r_{O 5}\right) \tag{12.144}
\end{equation*}
$$

To calculate $I_{\text {out }} / V_{X}$, we note that the current produced by $M_{1}$ is divided between $r_{O 1}$ and $R_{L}+R_{M}$ :

$$
\begin{equation*}
I_{\text {out }}=-\frac{r_{O 1}}{r_{O 1}+R_{L}+R_{M}} g_{m 1} V_{X} \tag{12.145}
\end{equation*}
$$

where the negative sign arises because $I_{\text {out }}$ flows out of the transistor. The open-loop gain is therefore equal to

$$
\begin{equation*}
G_{m}=\frac{g_{m 3}\left(r_{O 3} \| r_{O 5}\right) g_{m 1} r_{O 1}}{r_{O 1}+R_{L}+R_{M}} \tag{12.146}
\end{equation*}
$$

The output impedance is measured by replacing $R_{L}$ with a test voltage source and measuring the small-signal current [Fig. 12.57(c)]. The top and bottom terminals
of $V_{X}$ respectively see an impedance of $r_{O 1}$ and $R_{M}$ to ac ground; thus,

$$
\begin{align*}
R_{\text {in,open }} & =\frac{V_{X}}{I_{X}}  \tag{12.147}\\
& =r_{O 1}+R_{M} . \tag{12.148}
\end{align*}
$$

The feedback factor is computed according to the rule in Fig. 12.52(d):

$$
\begin{align*}
K & =\frac{V_{2}}{I_{1}}  \tag{12.149}\\
& =R_{M} . \tag{12.150}
\end{align*}
$$

Forming $K G_{m}$, we express the closed-loop parameters as

$$
\begin{align*}
\left.\frac{I_{\text {out }}}{V_{\text {in }}}\right|_{\text {closed }} & =\frac{G_{m}}{1+R_{M} G_{m}}  \tag{12.151}\\
R_{\text {in }, \text { closed }} & =\infty  \tag{12.152}\\
R_{\text {out }, \text { closed }} & =\left(r_{O 1}+R_{M}\right)\left(1+R_{M} G_{m}\right) \tag{12.153}
\end{align*}
$$

where $G_{m}$ is given by Eq. (12.146).
Construct the Norton equivalent of the entire circuit that drives the laser.

Example Analyze the circuit of Fig. 12.58(a), assuming $R_{M}$ is not small, and the laser diode exhibits 12.31 an impedance of $R_{L}$.
image_name:Figure 12.58(a)
description:
[
name: M1, type: NMOS, ports: {S: Vin, D: VF, G: X}
name: M2, type: NMOS, ports: {S: Iout, D: VDD, G: X}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: RM, type: Resistor, value: RM, ports: {N1: VF, N2: GND}
]
extrainfo:The circuit is a feedback amplifier driving a laser diode. M1 and M2 are NMOS transistors, RD and RM are resistors, and S2 is a switch. The circuit senses voltage at node X and delivers current to the laser.

image_name:Figure 12.58 (b)
description:
[
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: RM, type: Resistor, value: RM, ports: {N1: G1, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Iout, N2: K}
name: M1, type: NMOS, ports: {S: Vin, D: X, G: Vf}
name: M2, type: NMOS, ports: {S: Iout, D: VDD, G: X}
name: RM, type: Resistor, value: RM, ports: {N1: k, N2: GND}
]
extrainfo:The circuit is a feedback amplifier driving a laser diode. M1 and M2 are NMOS transistors, RD and RM are resistors, and S2 is a switch. The circuit senses voltage at node X and delivers current to the laser.

image_name:Figure 12.58 (c)
description:
[
name: M1, type: NMOS, ports: {S: Vin, D: X, G: g1}
name: M2, type: NMOS, ports: {S: S2, D: VDD, G: X}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: RM, type: Resistor, value: RM, ports: {N1: g1, N2: GND}
name: Vx, type: VoltageSource, value: Vx, ports: {Np: S2, Nn: k}
name: RM, type: Resistor, value: RM, ports: {N1: k, N2: GND}
]
extrainfo:The circuit is a feedback amplifier driving a laser diode. It consists of NMOS transistors M1 and M2, with RD and RM as resistors. S2 is a voltage source. The circuit senses voltage at node X and delivers current to the laser.

Solution
The forward amplifier consisting of $M_{1}, R_{D}$, and $M_{2}$ senses a voltage and delivers a current to the load, and resistor $R_{M}$ plays the role of the feedback network. In a manner similar to Example 12.30, we open the loop as shown in Fig. 12.58(b), where $G_{m}=I_{\text {out }} / V_{\text {in }}=\left(V_{X} / V_{\text {in }}\right)\left(I_{\text {out }} / V_{X}\right)$. As a common-gate stage, $M_{1}$ and $R_{D}$ yield
$V_{X} / V_{\text {in }}=g_{m 1} R_{D}$. To determine $I_{\text {out }}$, we first view $M_{2}$ as a source follower and calculate the voltage gain $V_{A} / V_{X}$ from Chapter 7:

$$
\begin{equation*}
\frac{V_{A}}{V_{X}}=\frac{R_{L}+R_{M}}{R_{L}+R_{M}+\frac{1}{g_{m 2}}} \tag{12.154}
\end{equation*}
$$

Thus,

$$
\begin{align*}
I_{\text {out }} & =\frac{V_{A}}{R_{L}+R_{M}}  \tag{12.155}\\
& =\frac{V_{X}}{R_{L}+R_{M}+\frac{1}{g_{m 2}}} \tag{12.156}
\end{align*}
$$

yielding the open-loop gain as

$$
\begin{equation*}
G_{m}=\frac{g_{m 1} R_{D}}{R_{L}+R_{M}+\frac{1}{g_{m 2}}} \tag{12.157}
\end{equation*}
$$

The open-loop input impedance is equal to $1 / g_{m 1}$. For the open-loop output impedance, we replace $R_{L}$ with a test voltage source [Fig. 12.58(c)], obtaining

$$
\begin{equation*}
\frac{V_{X}}{I_{X}}=\frac{1}{g_{m 2}}+R_{M} \tag{12.158}
\end{equation*}
$$

The feedback factor remains identical to that in Example 12.30, leading to the following expressions for the closed-loop parameters:

$$
\begin{align*}
\left.\frac{I_{\text {out }}}{V_{\text {in }}}\right|_{\text {closed }} & =\frac{G_{m}}{1+R_{M} G_{m}}  \tag{12.159}\\
R_{\text {in, closed }} & =\frac{1}{g_{m 1}}\left(1+R_{M} G_{m}\right)  \tag{12.160}\\
R_{\text {out }, \text { closed }} & =\left(\frac{1}{g_{m 2}}+R_{M}\right)\left(1+R_{M} G_{m}\right) \tag{12.161}
\end{align*}
$$

where $G_{m}$ is given by Eq. (12.157).

Exercise Repeat the above example if a resistor of value of $R_{1}$ is tied between the source of $M_{2}$ and ground.

Analyze the circuit of Fig. 12.59(a), assuming $R_{F}$ is not large, $R_{M}$ is not small, and the 12.32 laser diode is modeled by a resistance $R_{L}$. Also, assume $r_{O 2}<\infty$.

Solution As a current-current feedback topology, the amplifier must be analyzed according to the rules illustrated in Figs. 12.51(c) and 12.52(c). The forward system consists of $M_{1}$, $R_{D}$, and $M_{2}$, and the feedback network includes $R_{M}$ and $R_{F}$. The loop is opened as depicted in Fig. 12.59(b), where the output port of the sense duplicate is shorted because the feedback network returns a current to the input. Given by $\left(V_{X} / I_{\text {in }}\right)\left(I_{\text {out }} / V_{X}\right)$,
image_name:Fig. 12.59(a)
description:
[
name: M1, type: NMOS, ports: {S: S1, D: X, G: Vb}
name: M2, type: PMOS, ports: {S: VDD, D: d2, G: X}
name: RD, type: Resistor, value: RD, ports: {N1: X, N2: VDD}
name: RF, type: Resistor, value: RF, ports: {N1: S1, N2: P}
name: RM, type: Resistor, value: RM, ports: {N1: P, N2: GND}
name: Iin, type: CurrentSource, ports: {Np: GND, Nn: S1}
]
extrainfo:The circuit is a feedback amplifier with a current input Iin and a feedback network consisting of RF and RM. The output is taken across RL and rO2. M1 and M2 form the core amplifier with RD providing load resistance. The bias voltage Vb is applied to the gate of M1.
image_name:Fig. 12.59(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: Vb}
name: M2, type: PMOS, ports: {S: VDD, D: X, G: Vb}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: RF, type: Resistor, value: RF, ports: {N1: S1, N2: K1}
name: RM, type: Resistor, value: RM, ports: {N1: K1, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Iout, N2: GND}
name: rO2, type: Resistor, value: rO2, ports: {N1: Iout, N2: K2}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: S1, Nn: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: X, Nn: GND}
]
extrainfo:The circuit is a feedback amplifier with NMOS M1 and PMOS M2 transistors. The feedback network includes resistors RF and RM, and the forward path includes M1, M2, and RD. The current source Iin provides input current at node S1, and the output is taken at node Iout. The circuit implements a current-current feedback topology.
image_name:Fig. 12.59(c)
description:
[
name: RF, type: Resistor, value: RF, ports: {N1: I2, N2: X}
name: RM, type: Resistor, value: RM, ports: {N1: X, N2: GND}
name: I1, type: CurrentSource, ports: {Np: X, Nn: GND}
]
extrainfo:The circuit diagram (c) depicts a feedback network with resistors RF and RM connected to a current source I1. The node X serves as a junction for the feedback network and is grounded through RM. The current source I1 injects current into node X, with the other terminal connected to ground.

the open-loop gain is computed as

$$
\begin{equation*}
A_{I, \text { open }}=\frac{\left(R_{F}+R_{M}\right) R_{D}}{R_{F}+R_{M}+\frac{1}{g_{m 1}}} \cdot \frac{-g_{m 2} r_{O 2}}{r_{O 2}+R_{L}+R_{M} \| R_{F}} \tag{12.162}
\end{equation*}
$$

where the two fractions account for the division of $I_{i n}$ between $R_{F}+R_{M}$ and $M_{1}$, and the division of $I_{D 2}$ between $r_{O 2}$ and $R_{L}+R_{M} \| R_{F}$.

The open-loop I/O impedances are expressed as

$$
\begin{align*}
R_{\text {in,open }} & =\frac{1}{g_{m 1}} \|\left(R_{F}+R_{M}\right)  \tag{12.163}\\
R_{\text {out,open }} & =r_{O 2}+R_{F} \| R_{M} \tag{12.164}
\end{align*}
$$

with the latter obtained in a manner similar to that depicted in Fig. 12.57(c).
To determine the feedback factor, we apply the rule of Fig. 12.52(c) as shown in Fig. 12.59(c), thereby obtaining

$$
\begin{align*}
K & =\frac{I_{2}}{I_{1}}  \tag{12.165}\\
& =-\frac{R_{M}}{R_{M}+R_{F}} \tag{12.166}
\end{align*}
$$

The closed-loop parameters are thus given by

$$
\begin{align*}
A_{I, \text { closed }} & =\frac{A_{I, \text { open }}}{1-\frac{R_{M}}{R_{M}+R_{F}} A_{I, \text { open }}}  \tag{12.167}\\
R_{\text {in }, \text { closed }} & =\frac{\frac{1}{g_{m 1}} \|\left(R_{F}+R_{M}\right)}{1-\frac{R_{M}}{R_{M}+R_{F}} A_{I, \text { open }}}  \tag{12.168}\\
R_{\text {out }, \text { closed }} & =\left(r_{O 2}+R_{F} \| R_{M}\right)\left(1-\frac{R_{M}}{R_{M}+R_{F}} A_{I, \text { open }}\right) \tag{12.169}
\end{align*}
$$

where $A_{I, \text { open }}$ is expressed by Eq. (12.162).

Exercise Construct the Norton equivalent of the entire circuit that drives the laser.

Example
12.33

Figure 12.60(a) depicts a circuit similar to that in Fig. 12.59(a), but the output of interest here is $V_{\text {out }}$. Analyze the amplifier and study the differences between the two.
image_name:Figure 12.60(a)
description:
[
name: M1, type: NMOS, ports: {S: S1, D: d1g2, G: Vb}
name: M2, type: PMOS, ports: {S: VDD, D: Vout, G: d1g2}
name: RD, type: Resistor, value: RD, ports: {N1: d1g2, N2: VDD}
name: RF, type: Resistor, value: RF, ports: {N1: s1, N2: Vout}
name: RM, type: Resistor, value: RM, ports: {N1: Vout, N2: GND}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: GND, Nn: s1}
]
extrainfo:The circuit is a feedback amplifier with voltage-current feedback. M1 is an NMOS transistor, and M2 is a PMOS transistor. The input current source Iin drives the circuit, and the output is taken at Vout. The resistors RF and RM form part of the feedback network. The bias voltage Vb controls the gate of M1.
image_name:Figure 12.60(b)
description:
[
name: M1, type: NMOS, ports: {S: s1, D: d1g2, G: Vb}
name: M2, type: PMOS, ports: {S: VDD, D: Vout, G: d1g2}
name: RD, type: Resistor, value: RD, ports: {N1: d1g2, N2: VDD}
name: RF, type: Resistor, value: RF, ports: {N1: s1, N2: GND}
name: RF, type: Resistor, value: RF, ports: {N1: Vout, N2: GND}
name: RM, type: Resistor, value: RM, ports: {N1: Vout, N2: GND}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: GND, Nn: s1}
]
extrainfo:The circuit is a feedback amplifier with voltage-current feedback. M1 is an NMOS transistor controlled by the bias voltage Vb, and M2 is a PMOS transistor. The input current source Iin drives the circuit, and the output is taken at Vout. The resistors RF and RM form part of the feedback network. RM is part of the forward amplifier, and M2 cannot generate an output voltage without RM.

image_name:Figure 12.60(c)
description:
[
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: d1g2}
name: RF, type: Resistor, value: RF, ports: {N1: s1, N2: GND}
name: RF, type: Resistor, value: RF, ports: {N1: Vx, N2: GND}
name: RM, type: Resistor, value: RM, ports: {N1: Vx, N2: GND}
name: M1, type: NMOS, ports: {S: s1, D: d1g2, G: Vb}
name: M2, type: PMOS, ports: {S: VDD, D: Vx, G: d1g2}
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Vx, Nn: GND}
]
extrainfo:The circuit is a feedback amplifier with voltage-current feedback. M1 is an NMOS transistor controlled by the bias voltage Vb, and M2 is a PMOS transistor. The input current source Iin drives the circuit, and the output is taken at Vout. The resistors RF and RM form part of the feedback network. RM is part of the forward amplifier, and M2 cannot generate an output voltage without RM. The circuit incorporates voltage-current feedback, and RD is connected to the node dig2.

Solution

The circuit incorporates voltage-current feedback. In contrast to the previous case, $R_{M}$ now belongs to the forward amplifier rather than the feedback network. After all, $M_{2}$ would not be able to generate an output voltage without $R_{M}$. In fact, this circuit resembles the configuration of Fig. 12.56(a), except that the common-source stage employs a PMOS device.

Opening the loop with the aid of the rules in Fig. 12.51(b), we arrive at the topology in Fig. 12.60(b). Note that the return duplicate in this case $\left(R_{F}\right)$ differs from that in Fig. 12.59(b) $\left(R_{F}+R_{M}\right)$. The open-loop gain is then equal to

$$
\begin{align*}
R_{O} & =\frac{V_{\text {out }}}{I_{\text {in }}}  \tag{12.170}\\
& =\frac{R_{F} R_{D}}{R_{F}+\frac{1}{g_{m 1}}}\left[-g_{m 2}\left(R_{F} \| R_{M}\right)\right] \tag{12.171}
\end{align*}
$$

and the open-loop input impedance is given by

$$
\begin{equation*}
R_{\text {in,open }}=\frac{1}{g_{m 1}} \| R_{F} \tag{12.172}
\end{equation*}
$$

The output impedance is computed as illustrated in Fig. 12.60(c):

$$
\begin{align*}
R_{\text {out }, \text { open }} & =\frac{V_{X}}{I_{X}}  \tag{12.173}\\
& =R_{F} \| R_{M} \tag{12.174}
\end{align*}
$$

If $r_{O 2}<\infty$, then it simply appears in parallel with $R_{F}$ and $R_{M}$ in both Eqs. (12.171) and (12.174).

The feedback factor also differs from that in Example 12.32 and is determined with the aid of Fig. 12.52(b):

$$
\begin{align*}
K & =\frac{I_{2}}{V_{1}}  \tag{12.175}\\
& =-\frac{1}{R_{F}} \tag{12.176}
\end{align*}
$$

yielding the following expressions for the closed-loop parameters:

$$
\begin{align*}
\left.\frac{V_{\text {out }}}{I_{\text {in }}}\right|_{\text {closed }} & =\frac{R_{O}}{1-\frac{R_{O}}{R_{F}}}  \tag{12.177}\\
R_{\text {in }, \text { closed }} & =\frac{\frac{1}{g_{m 1}} \| R_{F}}{1-\frac{R_{O}}{R_{F}}}  \tag{12.178}\\
R_{\text {out }, \text { closed }} & =\frac{R_{F} \| R_{M}}{1-\frac{R_{O}}{R_{F}}} . \tag{12.179}
\end{align*}
$$

In contrast to Example 12.32 , the output impedance in this case decreases by $1-R_{O} / R_{F}$ even though the circuit topology remains unchanged. This is because the output impedance is measured very differently in the two cases.

Exercise Repeat the above example if $M_{2}$ is degenerated by a resistor of value $R_{S}$.

## 12.8 STABILITY IN FEEDBACK SYSTEMS

Our studies in this chapter have thus far revealed many important benefits of negative feedback. Unfortunately, if designed poorly, negative-feedback amplifiers may behave "badly" or even oscillate. We say the system is marginally stable or simply unstable. In this section, we reexamine our understanding of feedback so as to define the meaning of "behaving badly" and determine the sources of instability.
### 12.8.1 Review of Bode's Rules

In our review of Bode's rules in Chapter 11, we noted that the slope of the magnitude of a transfer function decreases (increases) by $20 \mathrm{~dB} / \mathrm{dec}$ as the frequency passes a pole (zero). We now review Bode's rule for plotting the phase of the transfer function:

The phase of a transfer function begins to decrease (increase) at one-tenth of the pole (zero) frequency, incurs a change of $-45^{\circ}\left(+45^{\circ}\right)$ at the pole (zero) frequency, and experiences a total change of nearly $-90^{\circ}\left(+90^{\circ}\right)$ at ten times the pole (zero) frequency. ${ }^{14}$

Since the phase begins to change at one-tenth of a pole or zero frequency, even poles or zeros that seem far may affect it significantly-a point of contrast to the behavior of the magnitude.

Example
12.34

Figure 12.61(a) depicts the magnitude response of an amplifier. Using Bode's rule, plot the phase response. ${ }^{15}$

Solution Plotted in Fig. 12.61(b), the phase begins to fall at $0.1 \omega_{p 1}$, reaches $-45^{\circ}$ at $\omega_{p 1}$ and $-90^{\circ}$ at $10 \omega_{p 1}$, begins to rise at $0.1 \omega_{z}$, reaches $-45^{\circ}$ at $\omega_{z}$ and approximately zero at $10 \omega_{z}$, and finally begins to fall at $0.1 \omega_{p 2}$, reaching $-45^{\circ}$ at $\omega_{p 2}$ and $-90^{\circ}$ at $10 \omega_{p 2}$. In this example, we have assumed that the pole and zero frequencies are so wide apart that $10 \omega_{p 1}<0.1 \omega_{z}$ and $10 \omega_{z}<0.1 \omega_{p 2}$. In practice, this may not hold, requiring more detailed calculations.
image_name:Fig. 12.61 (a)
description:The graph in question is a Bode magnitude plot, which is a type of graph used to display the frequency response of a system. The horizontal axis represents the angular frequency (denoted as \(\omega\)) on a logarithmic scale, while the vertical axis represents the magnitude of the system's transfer function, expressed in decibels (20\(\log|H|\)).

Axes Labels and Units:
- **Horizontal Axis:** \(\omega\) (log scale)
- **Vertical Axis:** 20\(\log|H|\) (in decibels)

Overall Behavior and Trends:
- The plot begins with a flat region, indicating a constant gain at low frequencies.
- At \(\omega_{p1}\), the magnitude starts to decrease, indicating the presence of a pole. This results in a downward slope, suggesting a reduction in gain.
- At \(\omega_{z}\), the slope levels off, indicating a zero that compensates for the pole's effect, maintaining a constant gain over a range of frequencies.
- The magnitude decreases again at \(\omega_{p2}\), indicating another pole, which further reduces the gain.

Key Features and Technical Details:
- **\(\omega_{p1}\):** First pole frequency where the magnitude begins to decrease.
- **\(\omega_{z}\):** Zero frequency where the magnitude levels off.
- **\(\omega_{p2}\):** Second pole frequency where the magnitude decreases again.
- The slope changes are typical of a system with poles and zeros, indicating changes in the system's gain characteristics at these frequencies.

Annotations and Specific Data Points:
- The plot is annotated with dashed lines at \(\omega_{p1}\), \(\omega_{z}\), and \(\omega_{p2}\) to highlight the critical frequencies where the behavior of the system changes.
- The graph shows typical Bode plot behavior with distinct regions of gain reduction associated with poles and zeros, useful for analyzing the stability and performance of amplifiers in feedback loops.
image_name:Fig. 12.61 (b)
description:The graph in Figure 12.61(b) is a Bode plot depicting the phase response of an amplifier. The horizontal axis represents frequency \( \omega \) on a logarithmic scale, while the vertical axis shows the phase angle \( \angle H \) in degrees.

Overall Behavior and Trends:
- The phase response starts at 0 degrees and initially decreases, showing a downward trend.
- It reaches a minimum phase angle of approximately -90 degrees.
- The phase then increases back towards 0 degrees, forming a wave-like pattern.
- This pattern repeats, indicating oscillatory behavior in the phase response.

Key Features and Technical Details:
- The graph includes dashed horizontal lines at -45 degrees and -90 degrees, marking significant phase angles.
- The phase response exhibits a smooth transition between these angles, characteristic of systems with multiple poles and zeros.
- The overall shape suggests the presence of two poles and possibly a zero between them, causing the phase to dip to -90 degrees and then rise back.

Annotations and Specific Data Points:
- Dashed lines are used to highlight critical phase angles, which are essential for analyzing the stability of amplifiers in feedback loops.
- The wave-like pattern indicates changes in phase due to different frequencies affecting the system's gain characteristics.

(b)

Figure 12.61

Exercise Repeat the above example if $\omega_{p 1}$ falls between $\omega_{z}$ and $\omega_{p 2}$.

Amplifiers having multiple poles may become unstable if placed in a negative-feedback loop. The following example serves as our first step toward understanding this phenomenon.

[^2]Example Construct the magnitude and phase response of an amplifier having (a) one pole, 12.35 (b) two poles, or (c) three poles.

Solution Figures 12.62(a)-(c) show the response for the three cases. The phase shift between the input and the output asymptotically approaches $-90^{\circ},-180^{\circ}$, and $-270^{\circ}$ in one-pole, two-pole, and three-pole systems, respectively. An important observation here is that the three-pole system introduces a phase shift of $-180^{\circ}$ at a finite frequency $\omega_{1}$, reversing the sign of an input sinusoid at this frequency [Fig. 12.62(d)]. For example, a 1-GHz sinusoid is shifted (delayed) by 0.5 ns .
image_name:Fig. 12.61 (a)
description:The graph labeled "(a)" is a Bode plot consisting of two subplots: one for magnitude and one for phase. Both plots use a logarithmic scale on the x-axis, which represents frequency (ω).

1. **Magnitude Plot**:
- **Y-Axis**: The magnitude is expressed in decibels (dB), specifically as \(20 \log |H|\).
- **X-Axis**: The frequency \(ω\) is presented on a logarithmic scale.
- **Behavior**: The magnitude starts at 0 dB and begins to decrease at the corner frequency \(ω_{p1}\), indicated by a dotted vertical line.
- **Trend**: The slope of the line beyond \(ω_{p1}\) is negative, indicating a reduction in gain with increasing frequency.

2. **Phase Plot**:
- **Y-Axis**: The phase is measured in degrees, \(\angle H\), ranging from 0° to -90°.
- **X-Axis**: Frequency \(ω\) is again on a logarithmic scale.
- **Behavior**: The phase starts at 0° and begins to decrease as the frequency increases, approaching -90° asymptotically.
- **Key Feature**: The phase shift occurs gradually, indicating a first-order system response typical of a single-pole system.

Overall, this graph illustrates the frequency response of a one-pole system, showing how both the magnitude and phase shift with increasing frequency. The magnitude decreases at a rate of -20 dB/decade beyond \(ω_{p1}\), and the phase shift asymptotically approaches -90°.
image_name:Fig. 12.61 (b)
description:The graph labeled "(b)" is a Bode plot, which consists of two separate plots: one for the magnitude and one for the phase of a transfer function.

1. **Magnitude Plot:**
- **Type of Graph:** Logarithmic scale Bode plot for magnitude.
- **Axes Labels and Units:**
- **Y-axis:** 20log|H| (decibels, dB)
- **X-axis:** Frequency (ω) in a logarithmic scale, typically in radians per second or Hertz.
- **Overall Behavior and Trends:**
- The plot starts at 0 dB and remains flat until it reaches the first corner frequency, ωp1. After ωp1, the slope of the magnitude plot decreases, indicating a reduction in gain.
- At the second corner frequency, ωp2, the slope further decreases, reflecting additional attenuation.
- **Key Features and Technical Details:**
- Two corner frequencies, ωp1 and ωp2, are marked with vertical dashed lines.
- The slope changes at each corner frequency, typical of a two-pole system.

2. **Phase Plot:**
- **Type of Graph:** Logarithmic scale Bode plot for phase.
- **Axes Labels and Units:**
- **Y-axis:** Phase angle (degrees)
- **X-axis:** Frequency (ω) in a logarithmic scale.
- **Overall Behavior and Trends:**
- The phase starts at 0 degrees and begins to decrease as frequency increases.
- It asymptotically approaches -180 degrees as the frequency continues to rise.
- **Key Features and Technical Details:**
- The phase shift at ωp1 begins to decrease from 0 degrees toward -90 degrees, and the transition continues past ωp2, eventually approaching -180 degrees.
- This behavior is characteristic of a two-pole system, where each pole contributes a phase shift of -90 degrees.

The graph effectively illustrates the behavior of a two-pole system, showing both the attenuation in magnitude and the phase shift that occurs as the frequency increases beyond the corner frequencies ωp1 and ωp2.
image_name:Fig. 12.61 (c)
description:The graph labeled (c) is a Bode plot, which consists of two separate plots: a magnitude plot and a phase plot. Both plots are drawn with frequency (ω) on the horizontal axis, presented in a logarithmic scale.

Magnitude Plot:
- **Vertical Axis:** The magnitude is given in decibels (dB) as \(20\log|H|\).
- **Horizontal Axis:** Frequency \(\omega\) in a logarithmic scale.
- **Overall Behavior:** The magnitude plot starts at 0 dB and shows a decreasing trend. It features three distinct breakpoints at frequencies \(\omega_{p1}, \omega_{p2},\) and \(\omega_{p3}\), indicating the presence of three poles. Each pole contributes to a steeper slope in the plot.

Phase Plot:
- **Vertical Axis:** Phase angle \(\angle H\) in degrees.
- **Horizontal Axis:** Frequency \(\omega\) in a logarithmic scale.
- **Overall Behavior:** The phase plot starts at 0° and decreases as frequency increases, showing a total phase shift that asymptotically approaches -270°. This behavior indicates the cumulative effect of the three poles, each contributing a -90° phase shift.
- **Key Features:** At a specific frequency \(\omega_1\), the phase shift reaches -180°, which is significant as it reverses the sign of an input sinusoid at this frequency.

Annotations and Specific Data Points:
- The plot highlights the critical points \(\omega_{p1}, \omega_{p2},\) and \(\omega_{p3}\) where the slope changes, and \(\omega_1\) where the phase shift is -180°.
- The magnitude plot's slope increases negatively at each pole, indicating the system's increasing attenuation at higher frequencies.
- The phase plot's asymptotic behavior is marked by horizontal dashed lines at -90°, -180°, and -270° to show the phase shift levels reached as frequency increases.
image_name:Fig. 12.61 (d)
description:The diagram labeled "(d)" represents a simplified block diagram of a three-pole system. The main component in this system is a block labeled "Three-Pole System," which is depicted as a rectangular box. This block is responsible for processing an input sinusoidal signal at a specific frequency, denoted as \( \omega_1 \), and producing an output signal.

**Main Components:**
- **Three-Pole System Block:** This is the central processing unit of the diagram. It represents a system with three poles, which affects the phase and magnitude of the input signal.

**Flow of Information or Control:**
- **Input Signal:** The input sinusoidal signal, represented by a wavy line, enters the Three-Pole System block from the left.
- **Output Signal:** After processing by the Three-Pole System, the output signal exits the block on the right, also represented by a wavy line.

**Labels, Annotations, and Key Indicators:**
- **\( \omega_1 \):** This label indicates the frequency at which the input signal is applied. The diagram suggests that the three-pole system introduces a phase shift of \(-180^{\circ}\) at this frequency, effectively reversing the sign of the input sinusoid.

**Overall System Function:**
The primary function of this system is to introduce specific phase shifts to the input signal as it passes through the three-pole system. At the frequency \( \omega_1 \), the system introduces a \(-180^{\circ}\) phase shift, which is significant as it reverses the sign of the sinusoidal input. This characteristic is crucial for applications requiring precise phase manipulation, such as in feedback control systems or signal processing applications.

Figure 12.62

Exercise

Repeat the above analysis for a three-pole system if $\omega_{p 1}=\omega_{p 2}$.

### 12.8.2 Problem of Instability

Suppose an amplifier having a transfer function $H(s)$ is placed in a negative feedback loop (Fig. 12.63). As with the cases studied in Section 12.1, we write the closed-loop transfer function as

$$
\begin{equation*}
\frac{Y}{X}(s)=\frac{H(s)}{1+K H(s)} \tag{12.180}
\end{equation*}
$$

image_name:Figure 12.63
description:The block diagram in Figure 12.63 represents a negative feedback system, which is a common configuration in control systems and signal processing. The main components of this system include:

1. **Summing Junction (+):** This is where the input signal, denoted as \( X \), is combined with the feedback signal. The summing junction has two inputs: the main input \( X \) (positive) and the feedback signal (negative).

2. **Transfer Function Block \( H(s) \):** This block represents the system or amplifier with a transfer function \( H(s) \). It processes the signal from the summing junction and outputs it as \( Y \).

3. **Feedback Path with Gain \( K \):** The output \( Y \) is fed back through a path that includes a gain block \( K \). This gain is a constant and is used to control the amount of feedback.

**Flow of Information:**
- The input signal \( X \) is fed into the positive terminal of the summing junction.
- The output from the summing junction is the input to the \( H(s) \) block.
- The signal processed by \( H(s) \) is the output \( Y \), which is also the output of the overall system.
- \( Y \) is fed back through the gain \( K \), and this feedback signal is subtracted from the input \( X \) at the summing junction, creating a negative feedback loop.

**Annotations and Labels:**
- The input to \( H(s) \) is labeled as \( \text{In}(H(s)) \), and the output as \( \text{Out}(H(s)) \).
- The feedback path output is labeled as \( \text{Out}(K) \).

**Overall System Function:**
The primary function of this system is to stabilize and control the output \( Y \) of the transfer function \( H(s) \) by using negative feedback. The feedback loop helps to reduce the sensitivity of the system to parameter variations and can improve its stability and bandwidth. The closed-loop transfer function is given by \( \frac{Y}{X}(s) = \frac{H(s)}{1 + K H(s)} \), indicating how the feedback affects the overall system behavior.

Figure 12.63 Negative feedback system.
where $K H(s)$ is sometimes called the "loop transmission" rather than the loop gain to emphasize its frequency dependence. Recall from Chapter 11 that for a sinusoidal input, $x(t)=A \cos \omega t$, we simply make the substitution $s=j \omega$ in the above transfer function. We assume the feedback factor, $K$, exhibits no frequency dependence. (For example, it is equal to the ratio of two resistors.)

An interesting question that arises here is, what happens if at a certain input frequency $\omega_{1}$, the loop transmission, $K H\left(j \omega_{1}\right)$, becomes equal to -1 ? Then, the closed-loop system provides an infinite gain (even though the open-loop amplifier does not). To understand the consequences of infinite gain, we recognize that even an infinitesimally small input at $\omega_{1}$ leads to a finite output component at this frequency. For example, the devices comprising the subtractor generate electronic "noise" containing all frequencies. A small noise component at $\omega_{1}$ therefore experiences a very high gain and emerges as a large sinusoid at the output. We say the system oscillates at $\omega_{1}{ }^{16}$

It is also possible to understand the above oscillation phenomenon intuitively. Recall from Example 12.35 that a three-pole system introducing a phase shift of $-180^{\circ}$ reverses the sign of the input signal. Now, if $H(s)$ in Fig. 12.63 contains three poles such that $\angle H=-180^{\circ}$ at $\omega_{1}$, then the feedback becomes positive at this frequency, thereby producing a feedback signal that enhances the input. Circulating around the loop, the signal may thus continue to grow in amplitude. In practice, the final amplitude remains bounded by the supply voltage or other "saturation" mechanisms in the circuit.

For analysis purposes, we express the condition $K H\left(j \omega_{1}\right)=-1$ in a different form. Viewing $K H$ as a complex quantity, we recognize that this condition is equivalent to

$$
\begin{align*}
\mid K H\left(j \omega_{1} \mid\right. & =1  \tag{12.181}\\
\angle K H\left(j \omega_{1}\right) & =-180^{\circ} \tag{12.182}
\end{align*}
$$

the latter confirming our above intuitive perspective. In fact, Eq. (12.182) guarantees positive feedback (sufficient delay) and Eq. (12.181) ensures sufficient loop gain for the circulating signal to grow. Called "Barkhausen's criteria" for oscillation, Eqs. (12.181) and (12.182) prove extremely useful in the study of stability.

Example Explain why a two-pole system cannot oscillate. ${ }^{17}$ <br> 12.36

Solution As evident from the Bode plots in Fig. 12.62(b), the phase shift produced by such a system reaches $-180^{\circ}$ only at $\omega=\infty$, where $|H| \rightarrow 0$. In other words, at no frequency are both Eqs. (12.181) and (12.182) satisfied.

Exercise What happens if one of the poles is at the origin?

[^3]image_name:Fig. 12.64 (a)
description:The system block diagram labeled as "(a)" depicts a feedback control system designed to process an input signal at frequency \( \omega_1 \). The main components of the system include:

1. **Input Signal:** An oscillatory input at frequency \( \omega_1 \) is introduced into the system.

2. **Summing Junction:** The input signal is fed into a summing junction, which has two inputs: the main input signal (positive) and a feedback signal (negative). The output of this summing junction is labeled as point \( B \).

3. **Transfer Function Block \( H(s) \):** The output from the summing junction \( B \) is passed through a block with a transfer function \( H(s) \). This block processes the signal and outputs it to the next stage.

4. **Feedback Path:** The output of the \( H(s) \) block is fed back into the system through a feedback path that includes an amplifier with gain \( K \). This feedback path takes the processed signal and returns it to the summing junction as a negative feedback signal labeled \( A \).

5. **Output:** The processed signal is also directed to the output of the system, labeled as \( \text{Out}(H(s)) \), indicating the system's response to the input signal.

**Flow of Information:**
- The input signal at frequency \( \omega_1 \) is combined with the feedback signal at the summing junction.
- The combined signal is processed by the transfer function \( H(s) \), which affects the amplitude and phase of the signal.
- The output of \( H(s) \) is directed both to the system's output and back through the feedback loop, where it is amplified by \( K \) and fed back into the summing junction.

**Overall System Function:**
The primary function of this system is to produce an output signal that is a stable response to the input at \( \omega_1 \). The feedback loop, which introduces a phase shift and gain adjustment, is crucial for maintaining stability. The system aims to control the signal such that the conditions for oscillation are not met, thereby ensuring stable operation without sustained oscillations.
image_name:Fig. 12.64 (b)
description:The system block diagram labeled "(b)" represents a feedback control system designed to illustrate oscillatory behavior. The key components of this system include:

1. **Summing Junction (+/-):** This component receives two inputs. The first input is a sinusoidal signal at frequency \( \omega_1 \). The second input is a feedback signal from the output of the amplifier \( K \), which is subtracted from the input.

2. **Forward Path Transfer Function \( H(s) \):** The output from the summing junction is fed into a block labeled \( H(s) \), which represents the system's transfer function. This block processes the signal and outputs it to the next stage.

3. **Feedback Loop:** The output of the \( H(s) \) block is directed back to the input of the amplifier \( K \). This feedback loop is crucial for determining the system's stability and potential for oscillation.

4. **Amplifier \( K \):** The feedback signal is amplified by a factor \( K \) before being fed back into the summing junction. This amplification can affect the overall gain of the system and contribute to the conditions necessary for oscillation.

**Flow of Information:**
- The initial input signal at frequency \( \omega_1 \) enters the summing junction.
- The summing junction outputs the difference between the input signal and the feedback signal (after amplification).
- This difference is processed by the \( H(s) \) block, which modifies the signal according to its transfer function.
- The processed signal is then fed back to the amplifier \( K \), completing the feedback loop.

**Labels and Annotations:**
- The diagram is labeled with nodes \( A \) and \( B \) to indicate key points in the signal path.
- The output of the system is marked as \( \text{Out}(H(s)) \), representing the point after the transfer function block where the processed signal is available.

**Overall System Function:**
This system is designed to study the conditions under which a feedback system may become oscillatory. The interaction between the phase shift introduced by \( H(s) \) and the gain provided by \( K \) determines whether the system will oscillate. Specifically, the system may become unstable if the phase shift reaches \(-180^\circ\) at a frequency \( \omega_1 \) with a loop gain of unity, as suggested by the context. This diagram helps visualize how feedback can lead to oscillation under certain conditions.
image_name:Fig. 12.64 (c)
description:The system block diagram labeled "(c)" illustrates a negative feedback loop designed to enhance a signal at a specific frequency, \( \omega_1 \). The diagram consists of several key components:

1. **Input Signal (\( \omega_1 \))**: The system begins with an input sinusoidal signal at frequency \( \omega_1 \).

2. **Summing Junction**: The input signal is fed into a summing junction labeled with a plus (+) and minus (-) sign, indicating that it combines signals through addition and subtraction. The input signal enters the positive terminal.

3. **Feedback Path**: From the output of the summing junction, the signal proceeds to a block labeled \( H(s) \), which represents a transfer function or filter. This block processes the signal and outputs it to a node labeled as "Out(H(s))".

4. **Amplifier (\( K \))**: The processed signal from \( H(s) \) is then fed into an amplifier labeled \( K \). This amplifier boosts the signal's strength, which is crucial for maintaining the loop gain.

5. **Negative Feedback Loop**: The amplified signal is fed back into the summing junction at the negative terminal. This creates a negative feedback loop, which is essential for controlling the stability and behavior of the system.

6. **Output**: The output from the \( H(s) \) block is also the system’s final output, showing the result of the feedback process.

**Flow of Information**: The signal flow begins at the input signal \( \omega_1 \), moves through the summing junction, and is processed by the \( H(s) \) block. It is then amplified by \( K \) and fed back into the summing junction, completing the feedback loop. This loop is designed to enhance the signal at node B, as indicated in the context.

**Overall System Function**: The primary function of this system is to stabilize and enhance the signal at a specific frequency \( \omega_1 \) by using negative feedback. The phase shift and gain conditions are adjusted through the feedback loop to achieve the desired signal enhancement at node B, as described in the context. This setup is crucial for maintaining stability and preventing unwanted oscillations in the system.

Figure 12.64 Evolution of oscillatory system with time: (a) a component at $\omega_{1}$ is sensed at input, (b) the component returns to subtractor with a $180^{\circ}$ phase shift, (c) the subtractor enhances the signal at node $B$.

In summary, a negative feedback system may become unstable if the forward amplifier introduces a phase shift of $-180^{\circ}$ at a finite frequency, $\omega_{1}$, and the loop transmission $|K H|$ is equal to unity at that frequency. These conditions become intuitive in the time domain as well. Suppose, as shown in Fig. 12.64(a), we apply a small sinusoid at $\omega_{1}$ to the system and follow it around the loop as time progresses. The sinusoid incurs a sign reversal as it emerges at the output of the forward amplifier [Fig. 12.64(b)]. Assumed frequencyindependent, the feedback factor simply scales the result by a factor of $K$, producing an inverted replica of the input at node $A$ if $\left|K H\left(j \omega_{1}\right)\right|=1$. This signal is now subtracted from the input, generating a sinusoid at node $B$ with twice the amplitude [Fig. 12.64(c)]. The signal level thus continues to grow after each trip around the loop. On the other hand, if $\left|K H\left(j \omega_{1}\right)\right|<1$, then the output cannot grow indefinitely.

A three-pole feedback system exhibits the frequency response depicted in Fig. 12.65.
image_name:Figure 12.65
description:The graph in Figure 12.65 is a Bode plot, which consists of two separate plots: the magnitude plot and the phase plot, both plotted against frequency on a logarithmic scale.

Magnitude Plot:
- **Axes:**
- The vertical axis represents the magnitude of the loop gain $|KH|$ in decibels (dB), specifically $20\log|KH|$.
- The horizontal axis represents the frequency $\omega$ in radians per second, shown on a logarithmic scale.
- **Behavior:**
- The plot starts at a certain gain level and exhibits a downward slope as frequency increases.
- There are three distinct poles marked as $\omega_{p1}$, $\omega_{p2}$, and $\omega_{p3}$, where the slope of the plot changes.
- The gain decreases more steeply after each pole, indicating that each pole contributes to a further reduction in gain.
- A significant point $\omega_1$ is marked, where the gain is greater than 0 dB, indicating that the loop gain at this frequency is greater than unity.

Phase Plot:
- **Axes:**
- The vertical axis represents the phase angle $\angle H$ in degrees.
- The horizontal axis, like the magnitude plot, represents the frequency $\omega$ on a logarithmic scale.
- **Behavior:**
- The phase plot starts at 0 degrees and decreases, showing a phase lag as frequency increases.
- The plot crosses key phase angles at -90°, -180°, and approaches -270°.
- The phase lag increases at each pole, corresponding to the frequencies $\omega_{p1}$, $\omega_{p2}$, and $\omega_{p3}$.
- At $\omega_1$, the phase is notably below -180°, indicating a phase margin that could lead to instability if the gain is sufficient.

Key Features and Annotations:
- The plot is annotated with vertical dashed lines at the pole frequencies $\omega_{p1}$, $\omega_{p2}$, $\omega_{p3}$, and the frequency $\omega_1$.
- The gain at $\omega_1$ being greater than 0 dB suggests that the system can oscillate if the phase margin is inadequate.
- The combined effect of the poles results in a rapid phase drop, which is critical in determining the stability of the feedback system.

Figure 12.65

Solution Yes, it does. The loop gain at $\omega_{1}$ is greater than unity, but we note from the analysis in Fig. 12.64 that indefinite signal growth still occurs, in fact more rapidly. After each trip around the loop, a sinusoid at $\omega_{1}$ experiences a gain of $|K H|>1$ and returns with opposite phase to the subtractor.

Exercise Suppose $\omega_{p 1}$ is halved in value. Does the system still oscillate?


### 12.8.3 Stability Condition

Our foregoing investigation indicates that if $\left|K H\left(j \omega_{1}\right)\right| \geq 1$ and $\angle H\left(j \omega_{1}\right)=-180^{\circ}$, then the negative feedback system oscillates. Thus, to avoid instability, we must ensure that these two conditions do not occur at the same frequency.

Figure 12.66 depicts two scenarios wherein the two conditions do not coincide. Are both of these systems stable? In Fig. 12.66(a), the loop gain at $\omega_{1}$ exceeds unity ( 0 dB ), still leading to oscillation. In Fig. 12.66(b), on the other hand, the system cannot oscillate at $\omega_{1}$ (due to insufficient phase shift) or $\omega_{2}$ (because of inadequate loop gain).

The frequencies at which the loop gain falls to unity or the phase shift reaches $-180^{\circ}$ play such a critical role as to deserve specific names. The former is called the "gain crossover frequency" $\left(\omega_{G X}\right)$ and the latter, the "phase crossover frequency" $\left(\omega_{P X}\right)$. In Fig. 12.66(b), for example, $\omega_{G X}=\omega_{1}$ and $\omega_{P X}=\omega_{2}$. The key point emerging from the two above scenarios is that stability requires that

$$
\begin{equation*}
\omega_{G X}<\omega_{P X} \tag{12.183}
\end{equation*}
$$

image_name:Fig. 12.66 (b)
description:The graph in Fig. 12.66(b) is a Bode plot, which consists of two separate plots: one for gain and one for phase, both plotted against frequency (ω).

1. **Type of Graph and Function**:
- The graph is a Bode plot, commonly used in control systems and signal processing to represent the frequency response of a system.

2. **Axes Labels and Units**:
- The top plot represents the magnitude of the loop gain, labeled as `20log|KH|`, which is in decibels (dB).
- The bottom plot represents the phase angle of the loop gain, labeled as `∠KH`, with the phase shift in degrees.
- The horizontal axis for both plots is frequency (ω), typically in radians per second (rad/s).

3. **Overall Behavior and Trends**:
- In the magnitude plot, the gain decreases linearly with increasing frequency, indicating a typical roll-off characteristic of a low-pass filter.
- In the phase plot, the phase decreases, crossing the critical phase of `-180°` at a certain frequency.

4. **Key Features and Technical Details**:
- **Gain Crossover Frequency (ω₁)**: This is the frequency where the gain plot crosses the 0 dB line, denoted as ω₁.
- **Phase Crossover Frequency (ω₂)**: This is the frequency where the phase plot crosses the `-180°` line, denoted as ω₂.
- The stability condition requires that ω₁ (gain crossover frequency) is less than ω₂ (phase crossover frequency), ensuring that the phase does not reach `-180°` before the gain drops to unity.

5. **Annotations and Specific Data Points**:
- Vertical dashed lines are drawn from the crossover points on the gain and phase plots to the frequency axis, clearly marking ω₁ and ω₂.
- These crossover frequencies are critical for determining the stability of the system when negative feedback is applied.

In summary, this Bode plot illustrates a system where the gain falls to unity before the phase shift reaches `-180°`, satisfying the stability criterion for negative-feedback systems.

(b)

Figure 12.66 Systems with phase reaching $-180^{\circ}$ (a) before and (b) after the loop gain reaches unity.

In summary, to guarantee stability in negative-feedback systems, we must ensure that the loop gain falls to unity before the phase shift reaches $-180^{\circ}$ so that Barkhausen's criteria do not hold at the same frequency.

We wish to apply negative feedback with $K=1$ around the three-stage amplifier shown in Fig. 12.67(a). Neglecting other capacitances and assuming identical stages, plot the frequency response of the circuit and determine the condition for stability. Assume $\lambda=0$.

Solution The circuit exhibits a low-frequency gain of $\left(g_{m} R_{D}\right)^{3}$ and three coincident poles given by $\left(R_{D} C_{1}\right)^{-1}$. Thus, as depicted in Fig. 12.67(b), $|H|$ begins to fall at a rate of $60 \mathrm{~dB} / \mathrm{dec}$ at $\omega_{p}=\left(R_{D} C_{1}\right)^{-1}$. The phase begins to change at one-tenth of this frequency, ${ }^{18}$ reaches $-135^{\circ}$ at $\omega_{p}$, and approaches $-270^{\circ}$ at $10 \omega_{p}$.
image_name:Fig. 12.67 (a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1g2, G: Vin}
name: M2, type: NMOS, ports: {S: GND, D: d2g3, G: d1g2}
name: M3, type: NMOS, ports: {S: GND, D: Vout, G: d2g3}
name: RD1, type: Resistor, value: RD, ports: {N1: VDD, N2: d1g2}
name: RD2, type: Resistor, value: RD, ports: {N1: VDD, N2: d2g3}
name: RD3, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: C1a, type: Capacitor, value: C1, ports: {Np: d1g2, Nn: GND}
name: C1b, type: Capacitor, value: C1, ports: {Np: d2g3, Nn: GND}
name: C1c, type: Capacitor, value: C1, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a three-stage NMOS amplifier with each stage consisting of an NMOS transistor, a resistor (RD), and a capacitor (C1). The gain is determined by the product of the transconductance (gm) and the drain resistor (RD) raised to the power of three. The circuit exhibits three coincident poles at frequency (RD*C1)^-1, leading to a gain roll-off of 60 dB/decade.
image_name:Fig. 12.67 (b)
description:The graph in Figure 12.67(b) is a Bode plot, which consists of two separate plots: a magnitude plot and a phase plot. Both plots are presented on a logarithmic frequency scale on the x-axis, denoted as \( \omega \) (angular frequency), and the scale is logarithmic in nature.

Magnitude Plot:
- **Y-Axis (Magnitude):** The y-axis represents the magnitude of the transfer function \( |H| \), measured in decibels (dB). The plot starts at a high gain of \( 20 \log |H| = (g_m R_D)^3 \).
- **Behavior:** The plot shows a flat response initially, indicating a constant gain at low frequencies. As the frequency increases, the plot begins to fall off at a rate of \(-60 \text{ dB/decade}\) starting at the pole frequency \( \omega_p = (R_D C_1)^{-1} \). This indicates the presence of three coincident poles.

Phase Plot:
- **Y-Axis (Phase):** The y-axis represents the phase angle \( \angle H \), measured in degrees.
- **Behavior:** The phase begins to change at one-tenth of the pole frequency \( \omega_p \). At the pole frequency \( \omega_p \), the phase reaches \(-135^\circ\). As the frequency continues to increase, the phase approaches \(-270^\circ\) at ten times the pole frequency \( 10 \omega_p \).

Key Features:
- The magnitude plot and phase plot are aligned on the same frequency axis, allowing for easy correlation between gain and phase changes.
- The slope of \(-60 \text{ dB/decade}\) in the magnitude plot is typical for a system with three coincident poles.
- The phase plot shows a smooth transition from 0 to \(-270^\circ\), illustrating the phase lag introduced by the poles.

This Bode plot is used to analyze the stability and frequency response of the amplifier circuit, as described in the context. The key takeaway is the identification of the pole frequency \( \omega_p \) and the behavior of the system as frequency increases, which is crucial for stability analysis in a unity-feedback system.
image_name:Fig. 12.67 (c)
description:The graph in part (c) consists of two plots: a magnitude plot and a phase plot, both of which are Bode plots representing the frequency response of an amplifier.

1. **Magnitude Plot (Top Graph):**
- **Type:** Bode magnitude plot.
- **Axes:**
- **Y-axis:** 20log|H| (dB), representing the gain in decibels.
- **X-axis:** Frequency (ω) on a logarithmic scale.
- **Behavior:**
- The gain starts at a high value, approximately \( (g_m R_D)^3 \) dB.
- It exhibits a flat response initially, indicating constant gain.
- At the frequency \( \omega = \frac{1}{R_D C_1} \), the gain begins to decrease at a rate of -60 dB/decade, indicating the presence of three coincident poles.
- **Key Features:**
- A point \( P \) is marked on the curve, corresponding to a specific frequency \( \omega_{PX} \) on the phase plot.
- \(|H_P|\) is the gain at this point, and it must be less than 1 for stability.

2. **Phase Plot (Bottom Graph):**
- **Type:** Bode phase plot.
- **Axes:**
- **Y-axis:** Phase angle of \( H \) (degrees).
- **X-axis:** Frequency (ω) on a logarithmic scale.
- **Behavior:**
- The phase starts at 0 degrees and begins to decrease before \( \omega = \frac{1}{R_D C_1} \).
- At \( \omega = \frac{1}{R_D C_1} \), the phase is approximately -135 degrees.
- The phase continues to decrease and approaches -270 degrees as the frequency reaches \(10 \omega_{p}\).
- **Key Features:**
- The phase crossover frequency \( \omega_{PX} \) is marked, where the phase crosses -180 degrees.
- This frequency is crucial for determining the stability of the system, as it corresponds to the point \( P \) on the magnitude plot.

Figure 12.67

To guarantee that a unity-feedback system incorporating this amplifier remains stable, we must ensure that $|K H|(=|H|)$ falls below unity at the phase crossover frequency. Illustrated in Fig. 12.67(c), the procedure entails identifying $\omega_{P X}$ on the phase response, finding the corresponding point, $P$, on the gain response, and requiring that $\left|H_{P}\right|<1$.

[^4]We now repeat the procedure analytically. The amplifier transfer function is given by the product of those of the three stages: ${ }^{19}$

$$
\begin{equation*}
H(s)=\frac{\left(g_{m} R_{D}\right)^{3}}{\left(1+\frac{s}{\omega_{p}}\right)^{3}} \tag{12.184}
\end{equation*}
$$

where $\omega_{p}=\left(R_{D} C_{1}\right)^{-1}$. The phase of the transfer function can be expressed as ${ }^{20}$

$$
\begin{equation*}
\angle H(j \omega)=-3 \tan ^{-1} \frac{\omega}{\omega_{p}} \tag{12.185}
\end{equation*}
$$

where the factor 3 accounts for the three coincident poles. The phase crossover occurs if $\tan ^{-1}\left(\omega / \omega_{p}\right)=60^{\circ}$ and hence

$$
\begin{equation*}
\omega_{P X}=\sqrt{3} \omega_{p} \tag{12.186}
\end{equation*}
$$

The magnitude must remain less than unity at this frequency:

$$
\begin{equation*}
\frac{\left(g_{m} R_{D}\right)^{3}}{\left[\sqrt{1+\left(\frac{\omega_{P X}}{\omega_{p}}\right)^{2}}\right]^{3}}<1 \tag{12.187}
\end{equation*}
$$

It follows that

$$
\begin{equation*}
g_{m} R_{D}<2 \tag{12.188}
\end{equation*}
$$

If the low-frequency gain of each stage exceeds 2 , then a feedback loop around this amplifier with $K=1$ becomes unstable.

Exercise Repeat the above example if the last stage incorporates a load resistance equal to $2 R_{D}$.

Example A common-source stage is placed in a unity-gain feedback loop as shown in Fig. 12.68.
12.39 Explain why this circuit does not oscillate.
image_name:Figure 12.68
description:
[
name: M1, type: NMOS, ports: {S: GND, D: g1d1, G: g1d1}
name: RD, type: Resistor, value: RD, ports: {N1: g1d1, N2: VDD}
name: C1, type: Capacitor, value: C1, ports: {Np: g1d1, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a common-source amplifier with a feedback loop. It contains an NMOS transistor M1 with a resistor RD and a capacitor C1 connected to the drain. The gate and drain are connected together to form a feedback loop. The circuit is powered by a voltage source VDD.

Figure 12.68

Solution Since the circuit contains only one pole, the phase shift cannot reach $180^{\circ}$ at any frequency. The circuit is thus stable.

Exercise What happens if $R_{D} \rightarrow \infty$ and $\lambda \rightarrow 0$ ?

[^5]Example Repeat Example 12.38 if the target value of $K$ is $1 / 2$, i.e., the feedback is weaker.
12.40

Solution We plot $|K H|=0.5|H|$ and $\angle K H=\angle H$ as shown in Fig. 12.69(a). Note the $|K H|$ plot is simply shifted down by 6 dB on a logarithmic scale. Starting from the phase crossover frequency, we determine the corresponding point, $P$, on $|K H|$ and require that $0.5\left|H_{P}\right|<1$. Recognizing that Eqs. (12.185) and (12.186) still hold, we write

$$
\begin{equation*}
\frac{0.5\left(g_{m} R_{D}\right)^{3}}{\left[\sqrt{1+\left(\frac{\omega_{P X}}{\omega_{p}}\right)^{2}}\right]^{3}}<1 \tag{12.189}
\end{equation*}
$$

That is,

$$
\begin{equation*}
\left(g_{m} R_{D}\right)^{3}<\frac{2^{3}}{0.5} \tag{12.190}
\end{equation*}
$$

Thus, the weaker feedback permits a greater open-loop gain.
image_name:Figure 12.69
description:The graph in Figure 12.69 is a Bode plot, which consists of two subplots: one for magnitude and one for phase, both plotted against frequency on a logarithmic scale.

Magnitude Plot:
- **Vertical Axis:** The magnitude is given in decibels (dB) as \(20 \log |KH|\).
- **Horizontal Axis:** Frequency \(\omega\) is plotted on a logarithmic scale.
- **Behavior:** The plot shows a high gain at low frequencies, represented by a horizontal line at \((g_m R_D)^3\). This indicates a strong open-loop gain. As frequency increases, the gain decreases, shown by a downward sloping line.
- **Key Features:**
- The magnitude at point \(P\) is marked, showing where \(|HP|\) is less than \((g_m R_D)^3\) and greater than \(0.5(g_m R_D)^3\).
- The frequency \(\omega_{PX}\) is indicated, marking the transition point where the slope changes.
- A critical frequency is labeled as \(\frac{1}{R_D C_1}\), which is likely a breakpoint in the system's response.

Phase Plot:
- **Vertical Axis:** The phase angle \(\angle H\) is shown in degrees, ranging from 0° to -180°.
- **Horizontal Axis:** Frequency \(\omega\) is also plotted on a logarithmic scale.
- **Behavior:** The phase plot starts at 0° and decreases as frequency increases, eventually reaching -180°.
- **Key Features:**
- The phase shift at \(\omega_{PX}\) is marked, indicating a significant change in the system's response.

Annotations and Specific Data Points:
- The plot includes annotations for significant points such as \(P\) and \(\omega_{PX}\), providing visual markers for critical transitions in the system's behavior.
- The graph highlights the importance of maintaining the frequency \(\omega_{GX}\) below \(\omega_{PX}\) to avoid oscillation, as discussed in the surrounding context.

Figure 12.69

Repeat the above example if the third stage incorporates a load resistor of value $2 R_{D}$.

### 12.8.4 Phase Margin

Our study of instability in negative-feedback systems reveals that $\omega_{G X}$ must remain below $\omega_{P X}$ to avoid oscillation. But by how much? We surmise that if $\omega_{G X}<\omega_{P X}$ but the difference between the two is small, then the feedback system displays an almost-oscillatory response. Shown in Fig. 12.70 are three cases illustrating this point. In Fig. 12.70(a), Barkhausen's criteria are met and the system produces oscillation in response to an input step. In Fig. 12.70(b), $\omega_{G X}<\omega_{P X}$, but the step response "rings" for a long time because the system is "marginally" stable and behaves "badly." We therefore postulate that a
image_name:Fig. 12.70 (a)
description:The graph in Fig. 12.70(a) represents a Bode plot, which is used to analyze the frequency response of a system. The plot consists of two parts: the magnitude plot and the phase plot, both plotted against frequency.

1. **Type of Graph and Function**:
- The graph is a Bode plot, which includes both a magnitude plot (top) and a phase plot (bottom).

2. **Axes Labels and Units**:
- The horizontal axis represents frequency, denoted by \( \omega \), typically in radians per second.
- The vertical axis of the magnitude plot is labeled \( 20\log|KH| \) and is measured in decibels (dB).
- The vertical axis of the phase plot is labeled \( \angle KH \) and is measured in degrees.

3. **Overall Behavior and Trends**:
- The magnitude plot shows a downward slope, indicating a decrease in gain as frequency increases.
- The phase plot also shows a downward trend, crossing the -180° line.
- At the gain crossover frequency \( \omega_{G X} \), the magnitude is 0 dB.
- At the phase crossover frequency \( \omega_{P X} \), the phase is -180°.

4. **Key Features and Technical Details**:
- In this graph, the gain crossover frequency \( \omega_{G X} \) coincides with the phase crossover frequency \( \omega_{P X} \).
- This coincidence satisfies Barkhausen's criteria for oscillation, which means the system will oscillate in response to an input step.
- The phase at \( \omega_{G X} \) is exactly -180°, which is critical for meeting the oscillation condition.

5. **Annotations and Specific Data Points**:
- The graph includes dotted lines that connect the crossover points to the axes, highlighting the coincidence of \( \omega_{G X} \) and \( \omega_{P X} \).
- There are no specific numerical values given for \( \omega_{G X} \) and \( \omega_{P X} \), but their coincidence is the key feature of this plot.

This configuration illustrates a system that meets the criteria for oscillation, leading to an oscillatory response when subjected to a step input.
image_name:Fig. 12.70 (b)
description:The system block diagram labeled (b) illustrates a feedback control system where the gain crossover frequency (ω_GX) is slightly below the phase crossover frequency (ω_PX), leading to a marginally stable system with noticeable ringing in response to a step input.

1. **Main Components:**
- **Summing Junction (+):** This block receives an input signal and subtracts the feedback signal from it, producing the error signal.
- **Transfer Function Block (H(s)):** This block processes the error signal. It is responsible for the system's dynamic behavior and modifies the frequency response.
- **Amplifier (K):** Amplifies the output of the transfer function block. This block represents the system's gain and is crucial in determining stability.
- **Feedback Loop:** The output from the amplifier is fed back into the summing junction, completing the loop.

2. **Flow of Information or Control:**
- The input signal enters the summing junction where the feedback signal is subtracted, resulting in the error signal.
- The error signal is processed by the transfer function block (H(s)), which alters its frequency characteristics.
- The output of H(s) is then amplified by the gain block (K), increasing the signal's magnitude.
- This amplified signal is the system's output and is also fed back into the summing junction as the feedback signal, forming a closed loop.

3. **Labels, Annotations, and Key Indicators:**
- The graph above the block diagram shows the Bode plot with gain and phase margins. The gain crossover frequency (ω_GX) is indicated, where the magnitude of KH equals 0 dB.
- The phase crossover frequency (ω_PX) is also indicated, where the phase angle of KH reaches -180 degrees.
- The proximity of ω_GX to ω_PX suggests a marginal stability, leading to a ringing effect in the system's step response.

4. **Overall System Function:**
- The primary function of this system is to maintain stability while amplifying the input signal through feedback control. However, due to the close proximity of the gain and phase crossover frequencies, the system is only marginally stable, resulting in oscillatory behavior or ringing in response to a step input. This configuration highlights the importance of maintaining adequate phase margin to ensure a well-behaved system response.
image_name:Fig. 12.70 (c)
description:The graph in Fig. 12.70(c) is a Bode plot, which is a graphical representation of a linear, time-invariant system transfer function. It consists of two plots: the magnitude plot and the phase plot.

1. **Type of Graph and Function:**
- This is a Bode plot, used to analyze the frequency response of a system.

2. **Axes Labels and Units:**
- The horizontal axis in both plots represents frequency, denoted as \( \omega \), typically in radians per second.
- The vertical axis of the upper plot represents the magnitude of the transfer function \( |KH| \) in decibels (dB), shown as \( 20 \log |KH| \).
- The vertical axis of the lower plot represents the phase angle of the transfer function \( \angle KH \) in degrees.

3. **Overall Behavior and Trends:**
- The magnitude plot shows a decreasing trend, indicating a low-pass filter characteristic where gain decreases with increasing frequency.
- The phase plot starts above \(-180^{\circ}\) and shows a decreasing trend as frequency increases.

4. **Key Features and Technical Details:**
- The gain crossover frequency \( \omega_{GX} \) is marked where the magnitude plot crosses 0 dB.
- The phase crossover frequency \( \omega_{PX} \) is marked where the phase plot crosses \(-180^{\circ}\).
- In this case, \( \omega_{GX} \) is significantly lower than \( \omega_{PX} \), indicating a stable system with a good phase margin.
- At \( \omega_{GX} \), the phase angle \( \angle KH \) is significantly more positive than \(-180^{\circ}\), contributing to system stability.

5. **Annotations and Specific Data Points:**
- The plot includes dotted lines to visually connect the crossover frequencies with their respective axes.
- The system diagram below the Bode plot illustrates the feedback loop with block components labeled \( H(s) \) and \( K \), showing input and output signals, emphasizing the system's stable behavior due to the margin between crossover frequencies.

This Bode plot illustrates a system where the gain crossover is well below the phase crossover, providing a stable response due to the phase margin, as indicated by the more positive phase angle at \( \omega_{GX} \).

(c)

Figure 12.70 Systems with (a) coincident gain and phase crossovers, (b) gain crossover slightly below phase crossover, (c) gain crossover well below phase crossover.
well-behaved system is obtained only if a sufficient "margin" is allowed between $\omega_{G X}$ and $\omega_{P X}$ [Fig. 12.70(c)]. Note that in this case, $\angle K H$ at $\omega_{G X}$ remains significantly more positive than $-180^{\circ}$.

A measure commonly used to quantify the stability of feedback systems is the "phase margin" (PM). As exemplified by the cases in Fig. 12.70, the more stable a system is, the greater is the difference between $\angle H\left(\omega_{G X}\right)$ and $-180^{\circ}$. Indeed, this difference is called the phase margin:

$$
\begin{equation*}
\text { Phase Margin }=\angle H\left(\omega_{G X}\right)+180^{\circ} . \tag{12.191}
\end{equation*}
$$

Example
12.41

Figure 12.71 plots the frequency response of a multipole amplifier. The magnitude drops to unity at the second pole frequency. Determine the phase margin of a feedback system employing this amplifier with $K=1$.
image_name:Figure 12.71
description:**Type of Graph and Function:**
The graph in Figure 12.71 is a Bode plot, which is used to represent the frequency response of a system. It consists of two separate plots: one for magnitude and one for phase.

**Axes Labels and Units:**
- The horizontal axis for both plots represents frequency (ω) on a logarithmic scale.
- The vertical axis of the top plot represents the magnitude in decibels (20log|H|).
- The vertical axis of the bottom plot represents the phase angle in degrees (∠H).

**Overall Behavior and Trends:**
- **Magnitude Plot:**
- The magnitude plot starts at a certain level and remains constant until it reaches the first pole frequency (ω_p1), after which it begins to decrease.
- The slope of the magnitude plot becomes steeper after the second pole frequency (ω_p2), indicating a more rapid decrease.
- The magnitude drops to unity (0 dB) at the second pole frequency.
- **Phase Plot:**
- The phase plot starts from 0° and gradually decreases.
- At the second pole frequency, the phase reaches approximately -135°.

**Key Features and Technical Details:**
- **Magnitude Plot:**
- The magnitude is constant initially and begins to decrease at ω_p1, indicating the presence of a pole.
- There is a further decrease in slope at ω_p2, marking the second pole.
- **Phase Plot:**
- The phase shift is gradual, with a notable point at -135° at the second pole frequency.
- This value is crucial for determining the phase margin.

**Annotations and Specific Data Points:**
- The magnitude plot shows markers at ω_p1 and ω_p2, indicating the pole frequencies.
- The phase plot highlights the point where the phase reaches -135°, which is used to calculate the phase margin.

In conclusion, the Bode plot illustrates the frequency response of a multi-pole amplifier, with the phase reaching -135° at the second pole frequency, leading to a phase margin of 45° when K=1.

Figure 12.71

Solution The plot suggests that the phase reaches $-135^{\circ}$ at the second pole frequency (i.e., the poles are far apart). Thus, the phase margin is equal to $45^{\circ}$.

Exercise Is the phase margin greater or less than $45^{\circ}$ if $K=0.5$ ?

How much phase margin is necessary? For a well-behaved response, we typically require a phase margin of $60^{\circ}$. Thus, the above example is not considered an acceptable design. In other words, the gain crossover must fall below the second pole.

### 12.8.5 Frequency Compensation

It is possible that after the design of an amplifier is completed, the phase margin proves inadequate. How is the circuit modified to improve the stability? For example, how do we make the three-stage amplifier of Example 12.38 stable if $K=1$ and $g_{m} R_{D}>2$ ? The solution is to make two of the poles unequal in magnitude. Called "frequency compensation," this task can be accomplished by shifting $\omega_{G X}$ toward the origin (without changing $\omega_{P X}$ ). In other words, if $|K H|$ is forced to drop to unity at a lower frequency, then the phase margin increases [Fig. 12.72(a)].

How can $\omega_{G X}$ be shifted toward the origin? We recognize that if the dominant pole is translated to lower frequencies, so is $\omega_{G X}$. Figure 12.72(b) illustrates an example where the first pole is shifted from $\omega_{p 1}$ to $\omega_{p 1}^{\prime}$, but other poles are constant. As a result, $\omega_{G X}$ decreases in magnitude.

What happens to the phase after compensation? As shown in Fig. 12.72(b), the lowfrequency section of $\angle K H$ changes because $\omega_{p 1}$ is moved to $\omega_{P 1}^{\prime}$, but the critical section near $\omega_{G X}$ does not. Consequently, the phase margin increases.
image_name:Figure 12.72 (a)
description:**Type of Graph and Function:**
The graph is a Bode plot, which is used to analyze the frequency response of a system. It consists of two plots: the magnitude plot (top) and the phase plot (bottom).

**Axes Labels and Units:**
- The horizontal axis in both plots represents frequency (ω), displayed on a logarithmic scale.
- The vertical axis of the magnitude plot is labeled as \(20 \log |KH|\), indicating the gain in decibels (dB).
- The vertical axis of the phase plot is labeled as \(\angle KH\), representing the phase angle in degrees.

**Overall Behavior and Trends:**
- **Magnitude Plot (Figure 12.72a):**
- The original design shows a slope decreasing from left to right, indicating a reduction in gain as frequency increases.
- The compensated design shifts the curve downward, starting at a lower frequency \(\omega'_{GX}\) compared to the original \(\omega_{GX}\).
- Both designs intersect at the same point on the frequency axis, indicating a change in gain behavior.

- **Phase Plot (Figure 12.72b):**
- The original design phase curve decreases more sharply at the start, indicating a phase drop at lower frequencies.
- The compensated design shows a more gradual phase decrease, indicating improved phase margin.

**Key Features and Technical Details:**
- **Magnitude Plot:**
- Key frequencies are marked: \(\omega'_{GX}, \omega_{GX}, \omega_{PX}\).
- The compensated design shows a decrease in gain at \(\omega'_{GX}\), highlighting the effect of compensation.

- **Phase Plot:**
- Key frequencies \(\omega_{p1}, \omega'_{p1}, \omega_{PX}\) are indicated.
- The phase margin is improved in the compensated design, as shown by the less steep curve.

**Annotations and Specific Data Points:**
- The compensated and original designs are clearly labeled on both plots.
- Specific frequencies where changes occur are marked with dashed lines, indicating critical points of interest.
image_name:Figure 12.72 (b)
description:Figure 12.72(b) depicts a Bode plot, which includes both magnitude and phase plots for a system's frequency response. The horizontal axis represents the frequency \( \omega \) on a logarithmic scale. The vertical axis of the top plot shows \( 20 \log |KH| \), indicating the gain in decibels, while the bottom plot shows the phase \( \angle KH \) in degrees.

Magnitude Plot:
- **Original Design**: The original design is shown in a lighter line. It begins with a flat response at low frequencies, indicating a constant gain. As frequency increases, the plot shows a gradual decline starting at the first pole \( \omega_{p1} \), and this decline steepens past this point.
- **Compensated Design**: The compensated design, represented by a darker line, shows a shift in the location of the first pole from \( \omega_{p1} \) to \( \omega_{p1}' \), which is at a lower frequency. This results in a more gradual decline in gain with frequency, indicating improved stability and a reduction in bandwidth.

Phase Plot:
- **Original Design**: The phase plot of the original design shows a gradual decrease in phase, dropping significantly as frequency increases past \( \omega_{p1} \).
- **Compensated Design**: The compensated design shows a change in the phase profile at low frequencies due to the shift of the first pole to \( \omega_{p1}' \). The phase plot exhibits a slower decrease compared to the original design, especially near the critical frequency \( \omega_{GX} \), leading to an increased phase margin.

Key Features:
- **Critical Frequencies**: The graph highlights critical frequencies such as \( \omega_{p1} \), \( \omega_{p1}' \), \( \omega_{GX} \), and \( \omega_{PX} \).
- **Phase Margin**: The increase in phase margin is a significant result of the compensation, indicating improved stability.

The overall effect of the compensation is a more stable system with increased phase margin and slightly reduced bandwidth, as the first pole is shifted to a lower frequency, causing changes in both the magnitude and phase plots.

Figure 12.72 (a) Concept of frequency compensation, (b) effect on phase profile.

Example 12.42

The amplifier shown in Fig. 12.73(a) employs a cascode stage and a CS stage. Assuming that the pole at node $B$ is dominant, sketch the frequency response and explain how the circuit can be "compensated."
image_name:Fig. 12.73 (a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: A, G: Vin}
name: M2, type: NMOS, ports: {S: A, D: B, G: Vb1}
name: M3, type: PMOS, ports: {S: VDD, D: B, G: Vb2}
name: M4, type: PMOS, ports: {S: s3d4, D: VDD, G: Vb3}
name: M5, type: PMOS, ports: {S: VDD, D: X, G: B}
name: M6, type: NMOS, ports: {S: GND, D: X, G: Vb4}
name: Ccomp, type: Capacitor, value: Ccomp, ports: {Np: B, Nn: GND}
]
extrainfo:The circuit is a multi-stage amplifier with a cascode configuration. It includes both NMOS and PMOS transistors and a compensation capacitor. The circuit is designed for frequency compensation, affecting the phase and magnitude of the frequency response.
image_name:Fig. 12.73 (b)
description:The graph in Figure 12.73(b) is a Bode plot, which consists of two parts: a magnitude plot and a phase plot. This type of graph is commonly used in control systems and signal processing to analyze the frequency response of a system.

1. **Magnitude Plot:**
- **Axes:** The vertical axis represents the magnitude of the gain in decibels (dB), specifically noted as \(20\log|KH|\). The horizontal axis represents frequency \(\omega\) on a logarithmic scale.
- **Overall Behavior:** The magnitude plot starts at a high gain level, remains constant over a range of frequencies, and then begins to roll off at higher frequencies. This indicates a flat response in the passband followed by a decrease in gain as frequency increases.
- **Key Features:** The plot shows three distinct breakpoints labeled \(\omega_{p,B}\), \(\omega_{p,out}\), and \(\omega_{p,A}\). These correspond to the poles of the system, with \(\omega_{p,B}\) being the dominant pole, and \(\omega_{p,A}\) being further out.

2. **Phase Plot:**
- **Axes:** The vertical axis shows the phase shift in degrees, marked at intervals of \(-90^\circ\), \(-180^\circ\), and \(-270^\circ\). The horizontal axis is the same logarithmic frequency scale as the magnitude plot.
- **Overall Behavior:** The phase plot begins at 0°, remains constant over the initial frequency range, and then drops in steps as frequency increases. This indicates phase lag introduced by the poles.
- **Key Features:** The phase decreases in discrete steps corresponding to the frequencies of the poles \(\omega_{p,B}\), \(\omega_{p,out}\), and \(\omega_{p,A}\). Each pole contributes additional phase lag, resulting in the step-like appearance of the phase plot.

Overall, the Bode plot illustrates how the system's gain and phase shift vary across different frequencies, highlighting the effects of the poles on the system's stability and performance. The dominant pole at \(\omega_{p,B}\) plays a significant role in shaping the frequency response, particularly in the low-frequency range.

image_name:Figure 12.73(c)
description:The graph depicted is a Bode plot, which is used to illustrate the frequency response of a system. It consists of a magnitude plot, showing how the gain of the system varies with frequency.

1. **Axes Labels and Units:**
- The horizontal axis represents frequency \( \omega \) on a logarithmic scale, indicating how the system responds over a wide range of frequencies.
- The vertical axis is labeled as \( 20 \log |KH| \), representing the gain in decibels (dB).

2. **Overall Behavior and Trends:**
- The plot starts with a flat region at low frequencies, indicating constant gain.
- As frequency increases, the plot exhibits a step-like decrease in gain, which is characteristic of the influence of poles on the system.
- The gain decreases progressively as the frequency passes through each pole, showing a downward slope.

3. **Key Features and Technical Details:**
- Several poles are marked on the frequency axis: \( \omega'_{p,B} \), \( \omega_{p,B} \), \( \omega_{p,out} \), and \( \omega_{p,A} \).
- Each pole contributes to a reduction in gain, with the most significant drop occurring at \( \omega_{p,B} \), indicating its dominance in shaping the low-frequency response.
- The plot transitions from a flat response to a sloped decline, with each pole adding a -20 dB/decade slope.

4. **Annotations and Specific Data Points:**
- Vertical dashed lines mark the positions of each pole, providing visual reference points for where the gain begins to decrease.
- The plot emphasizes the impact of the dominant pole \( \omega_{p,B} \) on the overall frequency response, which is crucial for understanding the system's stability and performance.

image_name:Figure 12.73
description:### Type of Graph and Function:
The graph is a phase response plot, typically part of a Bode plot, which shows the phase shift of a system as a function of frequency. The frequency axis is on a logarithmic scale, denoted by \( \omega \) (omega).

Axes Labels and Units:
- **Horizontal Axis:** Represents frequency \( \omega \) on a logarithmic scale.
- **Vertical Axis:** Represents phase shift in degrees, ranging from 0° to -270°.

Overall Behavior and Trends:
The phase plot begins at 0° and exhibits a series of downward steps. Each step represents a phase shift of approximately -90°, consistent with the introduction of poles in the system. The graph shows three distinct steps, indicating the presence of three poles, each contributing a -90° phase shift.

Key Features and Technical Details:
- **Initial Phase:** Starts at 0°.
- **Phase Shifts:**
- The first step drops the phase to approximately -90°.
- The second step drops the phase to approximately -180°.
- The third step drops the phase to approximately -270°.
- **Dashed Lines:** Horizontal dashed lines mark the -90°, -180°, and -270° phase levels, providing visual reference points for the phase shifts.

Annotations and Specific Data Points:
- The plot emphasizes the impact of each pole on the phase response, crucial for understanding the system's stability and performance. The specific frequencies at which these phase shifts occur are not labeled, but they correspond to the positions of the poles as discussed in the context.

(c)

Figure 12.73

Solution Recall from Chapter 11 that the cascode stage exhibits one pole arising from node $A$ and another from node $B$, with the latter falling much closer to the origin. We can express these poles respectively as

$$
\begin{align*}
\omega_{p, A} & \approx \frac{g_{m 2}}{C_{A}}  \tag{12.192}\\
\omega_{p, B} & \approx \frac{1}{\left[\left(g_{m 2} r_{O 2} r_{O 1}\right) \|\left(g_{m 3} r_{O 3} r_{O 4}\right)\right] C_{B}} \tag{12.193}
\end{align*}
$$

where $C_{A}$ and $C_{B}$ denote the total capacitance seen at each node to ground. The third pole is associated with the output node:

$$
\begin{equation*}
\omega_{p, \text { out }}=\frac{1}{\left(r_{O 5} \| r_{O 6}\right) C_{\text {out }}} \tag{12.194}
\end{equation*}
$$

where $C_{\text {out }}$ represents the total capacitance at the output node. We assume $\omega_{P, B}<$ $\omega_{P, \text { out }}<\omega_{P, A}$. The frequency response of the amplifier is plotted in Fig. 12.73(b).

To compensate the circuit for use in a feedback system, we can add capacitance to node $B$ so as to reduce $\omega_{p, B}$. If $C_{c o m p}$ is sufficiently large, the gain crossover occurs well below the phase crossover, providing adequate phase margin [Fig. 12.73(c)]. An important observation here is that frequency compensation inevitably degrades the speed because the dominant pole is reduced in magnitude.

Exercise Repeat the above example if $M_{2}$ and $M_{3}$ are omitted, i.e., the first stage is a simple CS amplifier.

We now formalize the procedure for frequency compensation. Given the frequency response of an amplifier and the desired phase margin, we begin from the phase response and determine the frequency, $\omega_{P M}$, at which $\angle H=-180^{\circ}+$ PM (Fig. 12.74). We then mark $\omega_{P M}$ on the magnitude response and draw a line having a slope of $20 \mathrm{~dB} / \mathrm{dec}$ toward the vertical axis. The point at which this line intercepts the original magnitude response represents the new position of the dominant pole, $\omega_{p 1}^{\prime}$. By design, the compensated amplifier now exhibits a gain crossover at $\omega_{P M}$.
image_name:Figure 12.74
description:The graph in Figure 12.74 is a Bode plot, which consists of two subplots: the magnitude plot and the phase plot. Both plots use a logarithmic scale on the x-axis, representing frequency \( \omega \) in radians per second.

Magnitude Plot:
- **Y-axis:** The magnitude is expressed in decibels (dB), specifically as \( 20 \log |KH| \).
- **X-axis:** Frequency \( \omega \) is on a logarithmic scale.
- **Behavior:** The magnitude plot starts at a constant level and then begins to decrease at a rate of \(-20 \text{ dB/decade}\) after the frequency \( \omega_{p1} \). This slope is indicated by a line drawn on the plot.
- **Key Points:**
- \( \omega_{p1} \): The original dominant pole frequency where the slope begins to change.
- \( \omega_{p1}' \): The new position of the dominant pole after compensation.
- \( \omega_{PM} \): The frequency at which the phase margin is achieved. This point is marked on the magnitude plot.

Phase Plot:
- **Y-axis:** The phase angle \( \angle KH \) in degrees.
- **X-axis:** Frequency \( \omega \) on a logarithmic scale, similar to the magnitude plot.
- **Behavior:** The phase plot shows a decreasing trend, reaching \(-180^\circ + \text{PM}\) at \( \omega_{PM} \).
- **Annotations:**
- A horizontal line at \(-180^\circ + \text{PM}\) is drawn to indicate the desired phase margin.
- The intersection of this line with the phase curve helps determine \( \omega_{PM} \), which is then used on the magnitude plot to adjust the dominant pole position.

Overall, this Bode plot illustrates the systematic method for frequency compensation by adjusting the position of the dominant pole to achieve a specific phase margin.

Figure 12.74 Systematic method for frequency compensation.

| Example |
| :---: |
| 12.43 |

A multipole amplifier exhibits the frequency response plotted in Fig. 12.75(a). Assuming the poles are far apart, compensate the amplifier for a phase margin of $45^{\circ}$ with $K=1$.
image_name:Figure 12.74
description:The graph in Figure 12.74 is a Bode plot, consisting of two parts: a magnitude plot and a phase plot, both plotted against frequency on a logarithmic scale.

1. **Magnitude Plot (Top):**
- **Axes:** The vertical axis represents the magnitude in decibels (dB), specifically \(20 \log |H|\), while the horizontal axis represents the frequency \(\omega\) on a logarithmic scale.
- **Behavior:** The plot starts at a constant magnitude of 0 dB, indicating no gain or loss at low frequencies. As the frequency increases, the plot shows a decline with a slope of approximately \(-20 \text{ dB/decade}\) after the first pole \(\omega_{p1}\). This slope continues until the second pole \(\omega_{p2}\), where the slope becomes steeper.
- **Key Features:**
- The dominant pole is initially at \(\omega_{p1}\) but is adjusted to \(\omega_{p1}'\) to achieve the desired phase margin.
- The line between \(\omega_{p1}\) and \(\omega_{p2}\) is highlighted, indicating the region of interest for frequency compensation.

2. **Phase Plot (Bottom):**
- **Axes:** The vertical axis represents the phase angle in degrees, and the horizontal axis is the same logarithmic frequency scale as the magnitude plot.
- **Behavior:** The phase starts at 0 degrees and decreases as frequency increases. It reaches \(-135^{\circ}\) at the frequency \(\omega_{p2}\), which is significant for determining the phase margin.
- **Key Features:**
- The point where the phase reaches \(-135^{\circ}\) is marked, indicating the critical frequency \(\omega_{PM}\).

Overall, this Bode plot illustrates the adjustment of the dominant pole position to achieve a specific phase margin, demonstrating the systematic method for frequency compensation in a multipole amplifier.
image_name:Figure 12.75
description:The graph in Figure 12.75 is a Bode plot, which consists of two separate plots: a magnitude plot and a phase plot, both against frequency on a logarithmic scale.

Magnitude Plot:
- **Axes:**
- The vertical axis represents the magnitude of the transfer function, denoted as \(20 \log |H|\), measured in decibels (dB).
- The horizontal axis represents frequency \(\omega\) on a logarithmic scale.
- **Behavior and Trends:**
- The plot starts with a flat line at 0 dB, indicating no attenuation at low frequencies.
- As frequency increases, the magnitude begins to decrease at a slope of \(-20 \text{ dB/decade}\) starting from \(\omega_{p1}\).
- There is a noticeable change in slope at \(\omega_{p2}\), where the slope increases to \(-40 \text{ dB/decade}\), indicating the presence of additional poles.
- **Key Features:**
- \(\omega_{p1}\) and \(\omega_{p2}\) are marked as critical frequencies where the slope changes.
- A new line with a slope of \(-20 \text{ dB/decade}\) is drawn from \(\omega_{p2}\) back towards the vertical axis, indicating the concept of compensating the dominant pole to \(\omega_{p1}'\).

Phase Plot:
- **Axes:**
- The vertical axis represents the phase angle \(\angle H\) in degrees.
- The horizontal axis is the same log scale of frequency \(\omega\) as the magnitude plot.
- **Behavior and Trends:**
- The phase starts at 0 degrees at low frequencies.
- As frequency increases, the phase begins to decrease, reaching \(-135^{\circ}\) at \(\omega_{p2}\).
- **Key Features:**
- \(\omega_{p2}\) is identified as the frequency where the phase reaches \(-135^{\circ}\), which is critical for determining the phase margin.

Annotations and Specific Data Points:
- The plot illustrates the systematic method for frequency compensation by adjusting the position of the dominant pole to achieve a specific phase margin, in this case, 45 degrees.
- The diagram includes dashed vertical lines at \(\omega_{p1}\), \(\omega_{p1}'\), and \(\omega_{p2}\) to mark these significant frequencies.

Figure 12.75
Solution Since the phase reaches $-135^{\circ}$ at $\omega=\omega_{p 2}$, in this example $\omega_{P M}=\omega_{p 2}$. We thus draw a line with a slope of $-20 \mathrm{~dB} / \mathrm{dec}$ from $\omega_{p 2}$ toward the vertical axis. The dominant pole must therefore be translated to $\omega_{p 1}^{\prime}$. Since this phase margin is generally inadequate, in practice, $\omega_{P M}<\omega_{p 2}$.

Exercise Repeat the above example for $K=0.5$ and compare the results.

Did you know?

It is interesting to know how one capacitor changed the fate of a product forever. A generalpurpose, innovative op amp (LM101) introduced by Robert Widlar at National Semiconductor in 1967 employed Miller compensation but with an external 30 pF capacitor. Evidently, the compensation capacitor was left off-chip to provide greater flexibility for the user. In 1968, David Fullagar at Fairchild Semiconductor introduced another op amp very similar to the LM101, except that the compensation capacitor was integrated on the chip. This was the 741 op amp, which quickly became popular and has served the electronics industry for nearly half a century.

The reader may wonder why the line originating at $\omega_{P M}$ must rise at a slope of $20 \mathrm{~dB} / \mathrm{dec}$ (rather than 40 or $60 \mathrm{~dB} / \mathrm{dec}$ ) toward the vertical axis. Recall from Examples 12.41 and 12.43 that, for adequate phase margin, the gain crossover must occur below the second pole. Thus, the magnitude response of the compensated amplifier does not "see" the second pole as it approaches $\omega_{G X}$; i.e., the magnitude response has a slope of only $-20 \mathrm{~dB} / \mathrm{dec}$.

### 12.8.6 Miller Compensation

In Example 12.42, we noted that a capacitor can be tied from node $B$ to ground to compensate the amplifier. The required value of this capacitor may be quite large, necessitating a large area on an integrated circuit. But recall from Miller's theorem in Chapter 11 that the apparent value of a capacitor increases if the device is connected between the input and output of an inverting amplifier. We also observe that the two-stage amplifier of Fig. 12.73(a) can employ Miller multiplication because the second stage provides some voltage gain. Illustrated in Fig. 12.76, the idea
image_name:Fig. 12.76(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: A, G: Vin}
name: M2, type: NMOS, ports: {S: A, D: B, G: Vb1}
name: M3, type: PMOS, ports: {S: VDD, D: B, G: Vb2}
name: M4, type: PMOS, ports: {S: VDD, D: s3d4, G: Vb3}
name: M5, type: PMOS, ports: {S: VDD, D: X, G: s3d4}
name: M6, type: NMOS, ports: {S: X, D: GND, G: Vb4}
name: Cc, type: Capacitor, value: Cc, ports: {Np: B, Nn: X}
name: Ceq, type: Capacitor, value: Ceq, ports: {Np: B, Nn: GND}
]
extrainfo:The circuit employs Miller compensation with a capacitor Cc connected between the input and output of the second stage, effectively creating an equivalent grounded capacitance Ceq at node B. This reduces the required value of Cc by utilizing the voltage gain of the second stage.
image_name:Figure 12.76(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: A, G: Vin}
name: M2, type: NMOS, ports: {S: A, D: B, G: Vb1}
name: M3, type: PMOS, ports: {S: VDD, D: B, G: Vb2}
name: M4, type: PMOS, ports: {S: VDD, D: s3d4, G: Vb3}
name: M5, type: PMOS, ports: {S: VDD, D: X, G: s3d4}
name: M6, type: NMOS, ports: {S: GND, D: X, G: Vb4}
name: Cc, type: Capacitor, value: Cc, ports: {Np: B, Nn: X}
name: Ceq, type: Capacitor, value: Ceq, ports: {Np: B, Nn: GND}
]
extrainfo:The circuit is a two-stage amplifier with Miller compensation applied. The compensation capacitor Cc is placed between the input and output of the second stage, creating an equivalent capacitance Ceq at node B. This reduces the required value of Cc by a factor related to the gain of the second stage.

Figure 12.76 Example of Miller compensation.
is to introduce the compensation capacitor between the input and output of the second stage, thereby creating an equivalent grounded capacitance at $B$ given by

$$
\begin{align*}
C_{e q} & =\left(1-A_{v}\right) C_{c}  \tag{12.195}\\
& =\left[1+g_{m 5}\left(r_{O 5} \| r_{O 6}\right)\right] C_{c} . \tag{12.196}
\end{align*}
$$

Called "Miller compensation," this technique reduces the required value of $C_{c}$ by a factor of $1+g_{m 5}\left(r_{O 5} \| r_{O 6}\right)$.

Miller compensation entails a number of interesting side effects. For example, it shifts not only the dominant pole but also the output pole. Such phenomena are studied in more advanced texts, e.g., [1].

## 12.9 CHAPTER SUMMARY

- Negative feedback can be used to regulate the behavior of systems that are otherwise "untamed" and poorly controlled.
- A negative feedback system consists of four components: forward system, output sense mechanism, feedback network, and input comparison mechanism.
- The loop gain of a feedback system can, in principle, be obtained by breaking the loop, injecting a test signal, and calculating the gain as the signal goes around the loop. The loop gain determines many properties of feedback systems, e.g., gain, frequency response, and I/O impedances.
- The loop gain and closed-loop gain should not be confused with each other. The latter refers to the overall gain from the main input to the main output while the feedback loop is closed.
- If the loop gain is much greater than unity, the closed-loop gain becomes approximately equal to the inverse of the feedback factor.
- Making the closed-loop gain relatively independent of the open-loop gain, negative feedback provides many useful properties: it reduces the sensitivity of the gain to component variations, load variations, frequency variations, and signal level variations.
- Amplifiers can generally be viewed as one of four types with voltage or current inputs and outputs. In the ideal case, the input impedance of a circuit is infinite if it senses a voltage or zero if it senses a current. Also, the output impedance of an ideal circuit is zero if it generates a voltage or infinite if it generates a current.
- Voltage quantities are sensed in parallel and current quantities in series. Voltage quantities are summed in series and current quantities in parallel.
- Depending on the type of the forward amplifier, four feedback topologies can be constructed. The closed-loop gain of each is equal to the open-loop gain divided by one plus the loop gain.
- A negative-feedback loop sensing and regulating the output voltage lowers the output impedance by a factor of one plus the loop gain, making the circuit a better voltage source.
- A negative-feedback loop sensing and regulating the output current raises the output impedance by a factor of one plus the loop gain, making the circuit a better current source.
- A negative-feedback loop returning a voltage to the input raises the input impedance by one plus the loop gain, making the circuit a better voltage sensor.
- A negative-feedback loop returning a current to the input lowers the input impedance by one plus the loop gain, making the circuit a better current sensor.
- If the feedback network departs from its ideal model, then it "loads" the forward amplifier characteristics. In this case, a methodical method must be followed that included the effect of finite I/O impedances.
- A high-frequency signal traveling through a forward amplifier experiences significant phase shift. With several poles, it is possible that the phase shift reaches $180^{\circ}$.
- A negative-feedback loop that introduces a large phase shift may become a positivefeedback loop at some frequency and begin to oscillate if the loop gain at that frequency is unity or higher.
- To avoid oscillation, the gain crossover frequency must fall below the phase crossover frequency.
- Phase margin is defined as $180^{\circ}$ minus the phase of the loop transmission at the gain crossover frequency.
- To ensure a well-behaved time and frequeny response, a negative-feedback system must realize sufficient phase margin, e.g., $60^{\circ}$.
- If a feedback circuit suffers from insufficient phase margin, then it must be "frequencycompensated." The most common method is to lower the dominant pole so as to reduce the gain crossover frequency (without changing the phase profile). This typically requires adding a large capacitor from the dominant pole node to ground.
- To lower the dominant pole, one can exploit Miller multiplication of capacitors.
