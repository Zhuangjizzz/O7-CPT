# 5. Feedback Amplifiers

Feedback is a topic of paramount importance in analog design. It is a key concept that enables us to construct almost ideal analog circuits from the poorly controlled and very nonideal transistors readily available to us. By doing so, it facilitates the division of complex systems into smaller subblocks that may be designed independently.

## 5.1 IDEAL MODEL OF NEGATIVE FEEDBACK

We begin by considering the simplified model of a very general negative feedback system in Fig. 5.1. Its analysis finds overlap in introductory control theory and is applicable to a wide variety of systems, including analog integrated circuits. Later in this chapter, we refine our analysis making it progressively better suited to the circuits of most interest to us.

### 5.1.1 Basic Definitions

The linear time-invariant negative feedback system in Fig. 5.1 includes an amplifier, $A$, and some feedback circuitry whose gain is $\beta$. Also labelled in Fig. 5.1 are the input signal, $u$, the output signal, y, the feedback signal, v, and the difference signal,

$$
\begin{equation*}
\mathrm{x}=\mathrm{u}-\mathrm{v} \tag{5.1}
\end{equation*}
$$

Physically, each of these signals may be small-signal node voltages or branch currents. ${ }^{1}$
image_name:Fig. 5.1
description:The diagram, Fig. 5.1, represents an ideal model of a linear time-invariant negative feedback system. The system consists of the following main components:

1. **Amplifier (A):** This block is responsible for amplifying the input signal. It takes the difference signal, \( x \), as its input and produces an amplified output.

2. **Feedback Circuitry (β):** This block represents the feedback path of the system. It takes a portion of the output signal, \( y \), and feeds it back to the input to form the feedback signal, \( v \). The gain of this feedback path is denoted as \( \beta \).

3. **Summing Junction:** This is where the input signal, \( u \), and the feedback signal, \( v \), are combined. The summing junction calculates the difference between these two signals, resulting in the difference signal, \( x = u - v \).

The flow of information in the system is as follows:
- The input signal, \( u \), enters the system and is combined with the feedback signal, \( v \), at the summing junction to produce the difference signal, \( x \).
- The difference signal, \( x \), is then amplified by the amplifier (A) to produce the output signal, \( y \).
- A portion of the output signal, \( y \), is fed back through the feedback circuitry (β) to generate the feedback signal, \( v \).

The key indicators and annotations in the diagram include the labels \( u \), \( x \), \( y \), and \( v \), which represent the input, difference, output, and feedback signals, respectively. The loop gain of the system is defined as \( L = A \beta \).

Overall, the primary function of this system is to maintain stability and control by adjusting the output based on the feedback. The negative feedback loop helps in reducing errors and improving the performance of the amplifier by comparing the output with the input and minimizing the difference.

1. In some cases, it may be difficult to identify precisely which circuit variables correspond to the signals in Fig. 5.1. The model is applied to a few practical examples in Section 5.4.

Clearly,

$$
\begin{equation*}
v=A \beta x \equiv L x \tag{5.2}
\end{equation*}
$$

where we have defined the open-loop gain, or simply "loop gain,"

$$
\begin{equation*}
L \equiv A \beta \tag{5.3}
\end{equation*}
$$

Since $x=u-v$ in Fig. 5.1, they must all have the same units. Hence, the loop gain $L$ is always dimensionless.
If we consider the entire feedback system as a unified single-input single-output block, its input-output relationship is derived as follows:

$$
\begin{gather*}
x=u-L x \Rightarrow x=\frac{u}{1+L}  \tag{5.4}\\
y=A x=\frac{A}{1+L} u=\frac{A}{1+A \beta} u \tag{5.5}
\end{gather*}
$$

The "closed-loop" gain follows from (5.5),

$$
\begin{equation*}
A_{C L} \equiv \frac{y}{u}=\frac{A}{1+A \beta}=\frac{A}{1+L} \tag{5.6}
\end{equation*}
$$

and is not to be confused with the loop gain in (5.3).

### 5.1.2 Gain Sensitivity

The gain of amplifier A depends upon the small-signal parameters of its constituent transistors (i.e., their transconductances, $g_{m}$, and output resistances, $r_{d s}$ ). These in turn are subject to large variations over temperature and from one sample of the circuit to another. Fortunately, the value of the closed-loop gain, $\mathrm{A}_{\mathrm{CL}}$, is largely immune to these variations so long as the loop-gain, L , is much larger than unity.

To quantify this, consider the effect of a change in the amplifier gain from $A$ to $A+\Delta A$ while keeping the value of $\beta$ constant. The resulting change in closed-loop gain is

$$
\begin{align*}
\Delta A_{C L} & =\frac{A+\Delta A}{1+(A+\Delta A) \beta}-\frac{A}{1+A \beta} \\
& =\frac{(A+\Delta A)(1+A \beta)-A[1+(A+\Delta A) \beta]}{[1+(A+\Delta A) \beta](1+A \beta)}  \tag{5.7}\\
& =\frac{\Delta A}{(1+L)^{2}+\Delta A \beta}
\end{align*}
$$

Hence, if $L » 1$, large changes in the amplifier gain, $\Delta A$, result in very little change in $A_{C L}$. In other words, negative feedback enables high accuracy in the gain of the overall amplifier, even when there are large variations in the transistor parameters of the transistors providing the gain.

#### EXAMPLE 5.1

Consider the negative feedback system pictured in Fig. 5.1 where the amplifier inputs and outputs are voltages, so that both $A$ and $\beta$ are dimensionless. If the amplifier gain is 80 dB and $\beta=0.2$, what is the resulting closed-loop gain, $A_{C L}$ ? If $A$ decreases by an order magnitude, what is the resulting change in $A_{C L}$ ?

#### Solution

A gain of 80 dB corresponds to a value of $\mathrm{A}=10^{4}$. Plugging this value into (5.6) results in a closed-loop gain of

$$
\mathrm{A}_{\mathrm{CL}}=\frac{10^{4}}{1+0.2 \cdot 10^{4}}=4.9975
$$

If the gain decreases by an order of magnitude to $60 \mathrm{~dB}\left(\mathrm{~A}=10^{3}\right)$ the closed-loop gain becomes

$$
\mathrm{A}_{\mathrm{CL}}=\frac{10^{3}}{1+0.2 \cdot 10^{3}}=4.9751
$$

representing a change of less than $0.5 \%$.

Key Point: When L>>1, the closed-loop system has an overall gain inversely proportional to the gain of the feedback circuit and highly insensitive to the gain of the amplifier, A.

The insensitivity of $A_{C L}$ to changes in $A$ is also evident if one rewrites (5.6) substituting $\mathrm{A}=\mathrm{L} / \beta$.

$$
\begin{equation*}
A_{C L}=\frac{1}{\beta} \cdot \frac{L}{(1+\mathrm{L})} \tag{5.8}
\end{equation*}
$$

The closed loop gain is equal to a constant, the "desired gain" $1 / \beta$, multiplied by an error term that is close to unity as long as $L$ » 1 . In the limit of very large loop gain, the closed loop gain approaches the desired gain.

$$
\begin{equation*}
A_{C L} \cong \frac{A}{L}=\frac{1}{\beta} \tag{5.9}
\end{equation*}
$$

Hence, to obtain high accuracy in the closed-loop gain it is necessary to have high accuracy in the gain of the feedback circuit.

#### EXAMPLE 5.2

Repeat Example 5.1, but this time consider a change in $\beta$ from 0.2 to 0.21 while A remains constant at 80 dB .

#### Solution

With $\beta=0.21$, the closed-loop gain becomes

$$
\mathrm{A}_{\mathrm{CL}}=\frac{10^{4}}{1+0.21 \cdot 10^{4}}=4.7596
$$

This is approximately $5 \%$ lower than the result obtained in Example 5.1 for $\beta=0.2$, a percentage change commensurate with the change in $\beta$.

### 5.1.3 Bandwidth

The amplifier gain A is frequency-dependent, generally decreasing in magnitude at higher frequencies, as depicted in Fig. 5.2. However, as long as the loop gain remains much greater than unity (i.e. $A(\omega)$ » $1 / \beta$ ) the closed-loop gain will remain approximately $\quad \mathrm{A}_{\mathrm{CL}} \cong 1 / \beta$. At very high frequency, eventually $A(\omega) \ll(1 / \beta) \Rightarrow L$ « 1 and (5.6) simplifies to $A_{C L} \cong A(\omega)$. A very rough estimate of the bandwidth of the closed-loop amplifier is therefore provided by the transition between these zones; that is, the frequency at which $|A(\omega)|=(1 / \beta)$, or

Key Point: A rough estimate of the bandwidth of a feedback amplifier is given by the frequency where $|L(\omega)|=1$, which is much higher than the bandwidth of $\mathrm{A}(\omega)$.
equivalently where $|L(\omega)|=1$. It is clear from Fig. 5.2 that this closed-loop bandwidth will generally be much higher than the bandwidth of $A(\omega)$.

The sketch in Fig. 6.2, is predicated on the assumption that $\beta$ remains constant over the entire frequency range under consideration. Hence, to realize a closed-loop amplifier with high bandwidth, it is necessary for the feedback network to have high bandwidth, but not the amplifier, A .

### 5.1.4 Linearity

The model in Fig. 5.1 is completely linear and, hence, is only valid so long as the transistors in the amplifier, A, are exposed to small voltage and current signals. Fortunately, by applying negative feedback with large loop gain, the signal that appears at the amplifier input, $x$, is a strongly attenuated version of the input to the overall system, $u$. With $\mathrm{L} » 1$, (5.4) becomes

$$
\begin{equation*}
x \cong \frac{u}{L} \tag{5.10}
\end{equation*}
$$

This means that even when large signals are present at $u$, the amplifier $A$ is exposed to only very small voltage and current signals at its input, and can therefore operate linearly. The feedback circuit, however, must operate linearly even when exposed to large signals. Its input is the amplifier output y which is A times greater than x .

Key Point: With feedback, an amplifier is exposed to signals that are approximately L times smaller than would be the case without feedback, making it much more linear.
image_name:Fig. 5.2 Bandwidth of a closed-loop amplifier
description:The graph in Figure 5.2 is a Bode plot representing the bandwidth of a closed-loop amplifier. The x-axis is labeled with the symbol \( \omega \), representing angular frequency, while the y-axis represents gain. The gain is plotted on a logarithmic scale, with significant markers indicating key gain levels.

The graph shows two main curves: \( A(\omega) \) and \( A_{CL}(\omega) \). \( A(\omega) \) represents the open-loop gain, which starts at a high level and decreases with increasing frequency. It follows a negative slope, indicating a reduction in gain as frequency increases.

\( A_{CL}(\omega) \), the closed-loop gain, is depicted as a horizontal line at the level \( 1/\beta \). This indicates that the closed-loop gain remains constant over a wide range of frequencies, showcasing the effect of feedback in stabilizing the gain.

Key points on the graph include:
- At low frequencies, \( A(\omega) \) is much greater than \( 1/\beta \), leading to \( A_{CL} \approx 1/\beta \).
- At high frequencies, \( A(\omega) \) is much less than \( 1/\beta \), causing \( A_{CL} \approx A(\omega) \).
- A critical frequency is marked where \( A(\omega) = 1/\beta \), indicating where the loop gain \( L(\omega) = 1 \).

The plot effectively illustrates how negative feedback maintains a stable and accurate gain \( A_{CL} = 1/\beta \) across a broad frequency range, provided the conditions for feedback are met, as discussed in the context. The annotations highlight the transitions and conditions under which the amplifier operates linearly and effectively.

Fig. 5.2 Bandwidth of a closed-loop amplifer.

### 5.1.5 Summary

The preceding subsections show that amplifiers with an accurate gain of $\mathrm{A}_{\mathrm{CL}}=1 / \beta$, high bandwidth, and high linearity may be realized by using negative feedback as long as:

1) the feedback circuit has an accurately controlled gain, $\beta$, high bandwidth, and high linearity
2) the loop gain $L=A \beta$ is large
3) the feedback loop is stable

The conditions on the feedback circuit (\#1) are most easily satisfied by constructing it out of passive components and/or transistors acting as simple switches, thus avoiding the variability, parasitic poles, and inherent nonlinearity of circuits with transistors in the active mode. Often, the gain is dependent only on the ratios of passive component values, which in integrated circuits are more accurate than their absolute values. Condition $\# 2$ is satisfied by designing an amplifier with large gain, $A » 1 / \beta$. However, this is virtually the only specification on the amplifier since feedback greatly relaxes the requirements on its accuracy, bandwidth, and linearity.

Condition \#3, concerning stability of the loop, is the topic of the next subsection.

## 5.2 DYNAMIC RESPONSE OF FEEDBACK AMPLIFIERS

The reader may have already made use of feedback amplifiers without explicitly considering their stability. However, such methods can fail to predict critical circuit behavior.

#### EXAMPLE 5.3

The noninverting amplifier in Fig. 5.3(a) is often analyzed assuming the opamp's differential input is zero. Hence, the negative amplifier terminal voltage is $\mathrm{v}_{-}=\mathrm{v}_{\mathrm{in}}$. Further assuming the amplifier has infinite input impedance, the output voltage may be related to the input by a nodal equation at $\mathbf{v}_{\text {_ }}$.

$$
\begin{gather*}
v_{\text {in }}\left(\frac{1}{R_{1}}+\frac{1}{R_{2}}\right)-\frac{v_{\text {out }}}{R_{2}}=0  \tag{5.11}\\
\Rightarrow \frac{v_{\text {out }}}{v_{\text {in }}}=1+\frac{R_{2}}{R_{1}}
\end{gather*}
$$

This result is accurate, as anyone who has tested such an amplifier in the lab may attest.
image_name:(a)
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Vin, InN: V-, OutP: Vout}
name: R1, type: Resistor, value: R1, ports: {N1: V-, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: V-, N2: Vout}
]
extrainfo:This circuit is a noninverting amplifier configuration. The gain is determined by the resistors R1 and R2.
image_name:(b)
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: V+, InN: Vin, vin: Vout}
name: R1, type: Resistor, value: R1, ports: {N1: V+, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vout, N2: V+}
]
extrainfo:The circuit is a non-inverting amplifier with the op-amp input terminals reversed, making it unstable. This configuration leads to a large output voltage due to the positive feedback loop.

Fig. 5.3 (a) A noninverting amplifier. (b) A noninverting amplifier with the opamp input terminals reversed is unstable.

One might be tempted to apply the same analysis to the amplifier in Fig. 5.3(b). Doing so would yield the same result (5.11) since the only difference between the circuits is the polarity of the opamp inputs which was nowhere considered in the analysis above. However, assuming that the opamp's differential input is zero presumes stability of the feedback loop. The feedback loop in Fig. $5.3(b)$ is in fact unstable. In practice, the voltage at $\mathrm{v}_{\text {_ }}$ will increase above $\mathrm{v}_{\mathrm{in}}$, and the opamp's large gain will amplify the difference producing an output voltage $\mathrm{V}_{\text {out }}$ close to the amplifier's supply voltage.

Example 5.3 is an extreme case where the loop's feedback is positive instead of negative. However, instability can arise more subtly, when at high frequencies the amplifier introduces a phase shift that causes negative feedback to become positive. In this section, general methods are presented to check the stability of analog circuits with feedback. For stable circuits the same methods provide insight into important aspects of the closed-loop amplifier's frequency response.

### 5.2.1 Stability Criteria

The methods applied to study the stability of analog circuits with feedback differ somewhat from those employed in courses and texts on introductory control theory. Control theory is often concerned with the problem of stabilizing, by application of feedback, a system that is otherwise unstable. ${ }^{2}$ By contrast, we will apply feedback to amplifiers A that are already stable on their own. We use feedback to improve the amplifier's accuracy, bandwidth, and linearity, as described in Section 5.1. Unfortunately, if care is not taken, feedback can make the previously-stable amplifier go unstable, as in Example 5.3.

Stability can be tested by checking that all poles of the closed loop system,

$$
\begin{equation*}
\mathrm{A}_{\mathrm{CL}}(\mathrm{~s})=\frac{\mathrm{A}(\mathrm{~s})}{1+\mathrm{A}(\mathrm{~s}) \beta} \tag{5.12}
\end{equation*}
$$

are in the left-half plane. However, this method is not often used because obtaining A(s) with accuracy is difficult. Fortunately, stability can be checked with knowledge of the magnitude and phase of the frequency response $L(\omega)$, which are readily obtained by circuit simulation.

In all situations of interest to us, the amplifier's magnitude response is large at low frequencies, $|A(\omega)| \gg 1 / \beta$, and decreases at high frequencies. The same poles that cause the magnitude response to roll off also contribute negative phase shift at higher frequencies. Furthermore, in accordance with the discussion in Section we shall assume that the feedback circuit has a constant and well-controlled gain, $\beta \leq 1$. The open-loop magnitude response is, therefore, simply a scaled version of the amplifier's magnitude response,

$$
\begin{equation*}
|L(\omega)|=|A(\omega)| \beta \tag{5.13}
\end{equation*}
$$

and the open-loop phase response is equal to that of the amplifier,

$$
\begin{equation*}
\angle \mathrm{L}(\omega)=\angle \mathrm{A}(\omega)+\angle \beta=\angle \mathrm{A}(\omega)+0^{\circ}=\angle \mathrm{A}(\omega) \tag{5.14}
\end{equation*}
$$

The open-loop Bode plot sketched in Fig. 5.4(a) is typical of all the feedback circuits we will consider. Of particular interest is the frequency at which the open-loop magnitude response is unity,

$$
\begin{equation*}
\left|\mathrm{L}\left(\omega_{\mathrm{t}}\right)\right|=1 \tag{5.15}
\end{equation*}
$$

The solution of (5.15) is the loop's "unity-gain frequency", $\omega_{t}{ }^{3}$
2. The system to be stabilized is referred to as "the plant."
3. Barring any strange ripples in the loop's magnitude response (which should certainly be avoided by design) equation (5.15) has only one (positive) solution and $\omega_{\mathrm{t}}$ is unique.

An alternative graphical representation of the open-loop magnitude and phase response is shown in Fig. $5.4(b)$, which is a polar plot of $L(\omega)=A(\omega) \beta$ for all frequencies, $-\infty<\omega<\infty$. At low frequencies where $\mathrm{L}(\omega)$ has large magnitude and near-zero phase shift, the polar plot will be far from the origin along the positive real axis. As $\omega$ increases to large positive values, the plot spirals clockwise inwards to the origin. For negative values of $\omega$, the spiral is mirrored in the real axis, spiraling counterclockwise from the point at $L(0)$. Given a stable amplifier A, the closed-loop feedback system will also be stable if and only if this polar plot does not encircle the point $-1 .{ }^{4}$ Such will be the case so long as the polar plot intersects the unit circle below the real axis for positive frequencies, as is the case in Fig. 5.4.

By definition, the polar plot's intersection with the unit circle occurs at the loop's unity-gain frequency, $\omega_{\mathrm{t}}$. Hence, an equivalent stability criterion is

$$
\begin{equation*}
\angle \mathrm{L}\left(\omega_{\mathrm{t}}\right)>-180^{\circ} \tag{5.16}
\end{equation*}
$$

Key Point: The stability of a feedback amplifier may be checked by looking at a Bode plot of the loop gain, $\mathrm{L}(\omega)$; so long at the phase response is greater than -180 degres at the unity gain frequency, the feedback system is stable.

In summary, a feedback amplifier is stable so long as (5.16) is satisfied with $\omega_{\mathrm{t}}$ defied by (5.15). This criteria is written completely in terms of the open-loop magnitude and phase response. Hence, it can be checked simply by examining a Bode plot of $L(\omega)$. There is little need for the polar plots and they will henceforth be avoided. Furthermore, using the procedure in Section 5.4.1, the Bode plot may be readily obtained by computer simulation.
image_name:(a)
description:The graph labeled (a) is a Bode plot, which consists of two separate plots: one for the magnitude and one for the phase of the loop gain $L(\omega)$ as a function of frequency $\omega$. The magnitude plot is shown on the top, and the phase plot is on the bottom.

1. **Magnitude Plot:**
- **Axes Labels and Units:**
- The vertical axis represents the magnitude of the loop gain $|L(\omega)|$ in decibels (dB).
- The horizontal axis represents the frequency $\omega$, typically in a logarithmic scale, though specific units are not marked.
- **Overall Behavior and Trends:**
- The plot starts at a high magnitude at low frequencies and decreases as frequency increases.
- The magnitude crosses the 0 dB line at a particular frequency, denoted as $\omega_t$, which is the gain crossover frequency.

2. **Phase Plot:**
- **Axes Labels and Units:**
- The vertical axis represents the phase angle $\angle L(\omega)$ in degrees.
- The horizontal axis is the same as the magnitude plot, representing frequency $\omega$.
- **Overall Behavior and Trends:**
- The phase starts at 0 degrees at low frequencies and decreases as frequency increases.
- As the frequency approaches $\omega_t$, the phase angle approaches -180 degrees.
- The phase margin (PM) is indicated as the difference between the phase angle at $\omega_t$ and -180 degrees.

3. **Key Features and Technical Details:**
- The Bode plot is used to determine the stability of a feedback system by examining the gain and phase margins.
- The phase margin is a crucial indicator of stability, representing how far the phase is from reaching -180 degrees when the gain is 0 dB.

4. **Annotations and Specific Data Points:**
- The plot includes a dashed line at $\omega_t$, indicating the frequency where the magnitude is 0 dB.
- The phase margin is explicitly marked on the phase plot as the vertical distance between the phase at $\omega_t$ and the -180-degree line.
image_name:(b)
description:The graph labeled (b) is a polar plot depicting the loop gain \( L(\omega) \) for a feedback circuit as a function of frequency. This type of graph is used to visualize the stability of feedback systems, particularly in the context of control systems and amplifier design.

Axes and Units:
- **Axes:** The polar plot does not have traditional Cartesian axes. Instead, it uses a circular coordinate system where the radial distance from the origin represents the magnitude of \( L(\omega) \) and the angle represents the phase.
- **Units:** The magnitude is typically dimensionless, while the phase is measured in degrees.

Overall Behavior and Trends:
- The plot shows the trajectory of \( L(\omega) \) as the frequency \( \omega \) varies from negative to positive values.
- The trajectory begins on the positive real axis at \( L(0) \) for \( \omega < 0 \) and loops around the origin.
- As \( \omega \) increases, the path crosses the negative real axis and continues, indicating changes in phase and magnitude.

Key Features and Technical Details:
- The plot crosses the negative real axis at the point \(-1\), which is crucial for assessing stability.
- The phase margin (PM) is indicated as the angle between the negative real axis and the point where the trajectory crosses the unit circle.
- The loop gain \( L(\omega) \) for \( \omega > 0 \) is shown with a thicker line, suggesting a focus on positive frequencies.
- The trajectory does not encircle the point \(-1\), indicating stability of the feedback system.

Annotations and Specific Data Points:
- The plot is annotated with the point \( L(0) \) and the phase margin (PM).
- The dashed circle represents the unit circle, a reference for assessing gain and phase margins.

This polar plot is used in conjunction with the Bode plot shown in part (a) to provide a comprehensive view of the system's stability characteristics. The plot's shape and its relation to the point \(-1\) are crucial for determining whether the feedback system remains stable across the range of frequencies.

Fig. 5.4 The relationship between (a) a Bode plot and (b) a polar plot of $L(\omega)$ for a stable feedback circuit.

#### EXAMPLE 5.4

Sketch a polar plot of loop gain for the positive-feedback circuit in Fig. 5.3(b).

#### Solution

Since the feedback is positive, when cast into our negative feedback model of Fig. 5.1 the loop gain $L=A \beta$ is negative at low frequencies where the opamp gain is very high. Hence, the plot begins on the negative real axis with large magnitude. From there, the magnitude response of the loop will tend to zero at high frequencies, so the polar plot spirals into the origin, as shown in Fig. 5.5. Clearly, it must encircle the point -1 so the loop is unstable.

### 5.2.2 Phase Margin

As the name suggests, phase margin provides a quantitative measure of how close a given feedback system is to instability. However, phase margin also provides the designer with important information about the closed-loop response of a feedback amplifier.

Phase margin is defined for stable feedback systems as the additional phase shift that would be required at the unity-gain frequency to cause instability. The definition is illustrated graphically in Fig. 5.4. Analytically, phase margin is

$$
\begin{equation*}
\mathrm{PM} \equiv \angle \mathrm{~L}\left(\omega_{\mathrm{t}}\right)+180^{\circ} \tag{5.17}
\end{equation*}
$$

It is commonplace to establish some minimum phase margin as a basic specification in the design of a feedback amplifier. A typical misconception amongst students of analog design is that such specifications are intended to safeguard against instability in the presence of variations in circuit parameter values. However, we generally demand far more phase margin than is required simply to ensure the system is robustly stable. Rather, large phase margins of between $45^{\circ}$ and $90^{\circ}$ are typically required because systems with smaller phase margins will exhibit undesirable dynamic behavior.
image_name:Fig. 5.5 Polar plot of the loop gain for the case of positive feedback
description:The graph in question is a polar plot representing the loop gain of a feedback system in the context of positive feedback. The axes are not labeled with specific units, but the plot is centered around the complex plane with the real axis running horizontally and the imaginary axis running vertically.

The plot features a distinctive loop that encircles the point labeled as -1 on the real axis. This encirclement indicates instability in the feedback loop, as it suggests that the Nyquist criterion for stability is not met. The loop starts from a point where the loop gain, denoted as L(0), is less than zero at low frequencies, which is indicated by the label L(0) < 0 on the negative side of the real axis.

The graph exhibits a closed loop that spirals outward and then inward, crossing the real axis at several points. The encirclement of the -1 point is a critical feature, highlighting the system's instability under the given conditions of positive feedback.

There are no specific numerical values or additional annotations provided on the graph, but the dashed circle around the -1 point serves as a reference for evaluating the stability of the system. The behavior of the loop, particularly its encirclement of the -1 point, is indicative of a system that will likely exhibit undesirable dynamic behavior due to insufficient phase margin.

Fig. 5.5 Polar plot of the loop gain for the case of positive feedback. Since the L is large and negative at low frequencies, the plot must certainly encircle the point -1 and the loop is therefore unstable.

#### EXAMPLE 5.5

Find an expression for the closed-loop gain of a feedback amplifier at the unity gain frequency, $\omega_{\mathrm{t}}$. Assume the system has a phase margin $\theta$.

#### Solution

At the unity gain frequency, combining (5.15) and (5.17) reveals

$$
\begin{gather*}
\mathrm{L}\left(\omega_{\mathrm{t}}\right)=-\mathrm{e}^{\mathrm{j} \theta}  \tag{5.18}\\
\Rightarrow \mathrm{~A}\left(\omega_{\mathrm{t}}\right)=\frac{\mathrm{L}\left(\omega_{\mathrm{t}}\right)}{\beta}=-\frac{\mathrm{e}^{\mathrm{j} \theta}}{\beta} \tag{5.19}
\end{gather*}
$$

Substituting (5.18) and (5.19) into (5.6) yields,

$$
\begin{equation*}
A_{C L}\left(\omega_{t}\right)=\frac{-e^{j \theta} / \beta}{1-e^{j \theta}} \tag{5.20}
\end{equation*}
$$

Taking the absolute value and recognizing that $\left|1-\mathrm{e}^{\mathrm{j} \theta}\right|=\sqrt{2(1-\cos \theta)}$,

$$
\begin{equation*}
\left|A_{C L}\left(\omega_{t}\right)\right|=\frac{1}{\beta \sqrt{2(1-\cos \theta)}} \tag{5.21}
\end{equation*}
$$

Notice that for $\theta<60^{\circ},\left|A_{C L}\left(\omega_{t}\right)\right|>1 / \beta$. But, it has already been shown in (5.9) that the closed-loop gain of such an amplifier at low-frequencies is

$$
A_{C L} \cong 1 / \beta
$$

Hence, with a phase margin less than $60^{\circ}$, the closed-loop gain actually increases as one moves from low frequencies up to $\omega_{t}$ ! Of course, at even higher frequencies the gain eventually decreases and we have $A_{c L}(\omega) \cong A(\omega) \ll(1 / \beta)$.

Key Point: It is not enough that an amplifier simply be reliably stable-it must also reliably have large phase margin. To avoid undesirable behavior in the frequency and step responses of the closed-loop amplifier, it is common to require phase margins of 45 to 90 degrees.

Example 5.5 reveals that the sketch of closed-loop frequency response in Fig. 5.2 is accurate only for phase margins greater than $60^{\circ}$. Systems with phase margins less than $60^{\circ}$, but still stable, have a closed loop-frequency response as in Fig. 5.6, where peaking is observed around the loop's unity gain frequency. Since we wish the gain of the closed-loop amplifier to be constant around $1 / \beta$, such peaking is undesirable and, as we shall see in later sections, is generally accompanied by overshoot in the amplifier's transient step response. Hence, it is not enough that an amplifier simply be reliably stable-it must also reliably have large phase margin.
image_name:Fig. 5.6
description:The graph depicted in Fig. 5.6 is a Bode plot illustrating the closed-loop frequency response of a feedback amplifier. The horizontal axis represents frequency (ω), and the vertical axis represents magnitude, |A(ω)|, on a logarithmic scale. The plot focuses on the behavior of the amplifier around its unity gain frequency.

**Axes Labels and Units:**
- Horizontal Axis (ω): Frequency, typically in radians per second (not explicitly labeled).
- Vertical Axis (|A(ω)|): Magnitude of the gain, typically in decibels (dB), although not explicitly stated here.

**Overall Behavior and Trends:**
- The graph shows a typical frequency response with a notable peak around the unity gain frequency, indicating a resonant behavior.
- The response starts with a flat region at low frequencies, where the gain is significantly greater than 1/β.
- As frequency increases, the magnitude decreases, passing through the unity gain frequency where |A(ω)| = 1/β.
- The peaking occurs just past this point, suggesting a phase margin less than 60 degrees, which is associated with potential instability or overshoot in the transient response.
- Beyond the peak, the gain continues to decrease.

**Key Features and Technical Details:**
- The graph highlights the unity gain frequency, marked by a vertical dashed line where |A(ω)| = 1/β.
- The peaking in the response is undesirable for maintaining a stable closed-loop gain around 1/β.
- The closed-loop gain |A_CL(ω)| is emphasized at the peak, indicating it exceeds the desired value, leading to potential overshoot.

**Annotations and Specific Data Points:**
- The plot includes annotations showing the relationship between the open-loop gain |A(ω)| and the closed-loop gain |A_CL(ω)|.
- The point where |A(ω)| = 1/β is critical, and the graph shows that beyond this frequency, the gain becomes insufficient to maintain stability without peaking.
- The closed-loop gain at the peak is noted as being greater than 1/β, which is undesirable for a stable system.

In summary, the Bode plot in Fig. 5.6 illustrates the frequency response of a feedback amplifier with a phase margin less than 60 degrees, highlighting the peaking around the unity gain frequency and the challenges in maintaining a stable closed-loop gain.

Fig. 5.6 The closed-loop frequency response of a feedback amplifier with a phase margin less than 60 degrees.

## 5.3 FIRST- AND SECOND-ORDER FEEDBACK SYSTEMS

Although the frequency response of a practical amplifier may involve many poles and zeros, it is often sufficient to model it with a simple first- or second-order transfer function. It is most important to accurately understand the amplifier's response at frequencies $\omega \lesssim \omega_{\mathrm{t}}$ which determines the amplifier's stability and in-band performance. Hence, any poles and zeros at frequencies $\omega \gg \omega_{\mathrm{t}}$ may be neglected. A typical situation is depicted in Fig. 5.7 where one pole is dominant. A simple first-order model is sufficient to predict the behavior of feedback amplifiers when the unity-gain frequency is well below the second- and higher-order pole- and zero-frequencies of the amplifier, $\omega_{\mathrm{t}} \ll \omega_{\mathrm{p} 2}, \omega_{\mathrm{p} 3},\left|\omega_{\mathrm{z} 1}\right|, \ldots$ The second-order model is preferred when $\omega_{\mathrm{t}}$ is closer to $\omega_{\mathrm{p} 2}, \omega_{\mathrm{p} 3}, \omega_{\mathrm{z} 1}, \ldots$ For cases where $\omega_{\mathrm{t}}$ is at a frequency higher than $\omega_{\mathrm{p} 2}, \omega_{\mathrm{p} 3}, \omega_{\mathrm{z} 1}, \ldots$, even the second-order model has insufficient accuracy. However, these cases will have very little phase margin and they are, therefore, of little practical interest. This section focuses on simple first- and second-order models providing insight into the behavior of practical feedback amplifiers, which often defy rigorous analytical treatment.

### 5.3.1 First-Order Feedback Systems

A simple first-order model for the transfer function of a dominant-pole feedback amplifier, $A L(s)$, with dc gain $L_{0}$ and dominant pole frequency $\omega_{\mathrm{p} 1}$ is given by

$$
\begin{equation*}
L(s)=\frac{L_{0}}{\left(1+\mathrm{s} / \omega_{\mathrm{p} 1}\right)} \tag{5.22}
\end{equation*}
$$

image_name:Fig. 5.7 Typical feedback amplifier open-loop frequency response and the corresponding first and second-order models.
description:The graph in Fig. 5.7 consists of two parts, representing the open-loop frequency response of a feedback amplifier and its corresponding first and second-order models.

### Top Graph: Magnitude Response
- **Type of Graph:** Bode plot (magnitude response).
- **Axes Labels and Units:**
- The vertical axis represents the magnitude of the transfer function, \(|L(\omega)|\), in decibels (dB).
- The horizontal axis is frequency, \(\omega\), in radians per second, plotted on a logarithmic scale.
- **Overall Behavior and Trends:**
- The graph starts with a flat response at low frequencies, indicating a constant magnitude.
- At the dominant pole frequency \(\omega_{p1}\), the magnitude begins to decrease linearly on a logarithmic scale, signifying a first-order roll-off.
- Additional poles and zeros (\(\omega_{p2}, \omega_{p3}, \omega_{z1}, \ldots\)) introduce further changes in slope, depicted by the dashed lines representing first- and second-order models.
- **Key Features and Technical Details:**
- The first-order model shows a single linear decrease after \(\omega_{p1}\).
- The second-order model introduces additional slope changes, reflecting the influence of higher-order poles and zeros.
- **Annotations and Specific Data Points:**
- The graph marks key frequencies such as \(\omega_{p1}, \omega_{p2}, \omega_{p3}, \omega_{z1}\), indicating transitions in the response.

### Bottom Graph: Phase Response
- **Type of Graph:** Bode plot (phase response).
- **Axes Labels and Units:**
- The vertical axis represents the phase angle, \(\angle L(\omega)\), in degrees.
- The horizontal axis is frequency, \(\omega\), in radians per second, plotted on a logarithmic scale.
- **Overall Behavior and Trends:**
- The phase starts near 0 degrees at low frequencies.
- As frequency increases past \(\omega_{p1}\), the phase begins to drop.
- The first-order model shows a phase shift approaching -90 degrees.
- The second-order model demonstrates a more complex phase shift, approaching -180 degrees as more poles and zeros are considered.
- **Key Features and Technical Details:**
- The first-order model maintains a simple phase transition, while the second-order model reflects the combined effects of multiple poles and zeros.
- **Annotations and Specific Data Points:**
- The graph includes reference lines at -90 degrees and -180 degrees to highlight the phase margin and stability considerations.

Fig. 5.7 Typical feedback amplifier open-loop frequency response and the corresponding firstand second-order models.

Since there is only one pole contributing phase shift, the phase response of a first-order system never drops below $-90^{\circ}$. L,

$$
\begin{equation*}
\angle \mathrm{L}(\omega)>-90^{\circ} \tag{5.23}
\end{equation*}
$$

Key Point: A first-order feedback amplifier is unconditionally stable with approximately 90 degrees phase margin.

Combining (5.23) with the stability criteria in (5.16) and the definition of phase margin in (5.17), it is clear that a first-order feedback system is stable with at least $90^{\circ}$ phase margin. It is evident from the Bode plot in Fig. 5.8(a) that for large dc open-loop gain, $L_{0}$, the phase margin will in fact be very close to $90^{\circ}$. Furthermore, it is impossible for the polar plot of $L(\omega)$ for a negative feedback system with only 1 pole to encircle the point -1 , Fig. $5.8(b)$. Hence, first-order feedback systems are stable with $90^{\circ}$ phase margin for any dc gain, or pole frequency. This is unlike sec-ond- and higher-order loops where phase margin critically depends upon the feedback factor, $\beta$, dc gain, and pole frequencies,

Recall the unity-gain frequency $\omega_{\mathrm{t}}$, is the frequency at which $\left|L\left(\omega_{\mathrm{t}}\right)\right|=1$. We then have the following approximation, assuming $\omega_{\mathrm{t}} \gg>\omega_{\mathrm{p} 1}$ :

$$
\begin{equation*}
\left|\mathrm{L}\left(\omega_{\mathrm{t}}\right)\right|=1 \cong \frac{\mathrm{~L}_{0}}{\omega_{\mathrm{t}} / \omega_{\mathrm{p} 1}} \tag{5.24}
\end{equation*}
$$

image_name:(a)
description:The graph labeled "(a)" is a Bode plot, which is used to represent the frequency response of a first-order feedback system. It consists of two subplots: one for the magnitude of the open-loop transfer function \( |L(\omega)| \) in decibels (dB), and the other for the phase \( \angle L(\omega) \) in degrees.

1. **Magnitude Plot:**
- **Y-Axis:** Represents the magnitude \( |L(\omega)| \) in dB.
- **X-Axis:** Represents the frequency \( \omega \) on a logarithmic scale.
- The plot starts at a high magnitude \( L_0 \) and decreases linearly with frequency, indicating a slope of -20 dB/decade after the pole frequency \( \omega_{p1} \).
- The magnitude crosses the 0 dB line at the unity-gain frequency \( \omega_{t} \).

2. **Phase Plot:**
- **Y-Axis:** Represents the phase \( \angle L(\omega) \) in degrees.
- **X-Axis:** Represents the frequency \( \omega \) on a logarithmic scale.
- The phase starts at 0° and gradually decreases, approaching -180° as frequency increases.
- The phase margin is indicated as being greater than 90°, which is a measure of the system's stability.

3. **Key Features:**
- The pole frequency \( \omega_{p1} \) is marked on both plots, showing where the slope begins to change in the magnitude plot and where the phase begins to drop significantly.
- The unity-gain frequency \( \omega_{t} \) is also marked, where the magnitude crosses 0 dB.
- The phase margin (PM) is highlighted, showing it is greater than 90°, indicating unconditional stability.

This Bode plot provides a clear visualization of how the gain and phase of the system change with frequency, illustrating the unconditional stability and sufficient phase margin of the first-order feedback system.
image_name:(b)
description:### Type of Graph and Function:
The graph labeled "(b)" is a polar plot representing the open-loop frequency response of a first-order feedback system. This type of graph is used to illustrate the stability and phase margin of control systems.

Axes Labels and Units:
The polar plot does not have conventional axes like Cartesian plots. Instead, it represents complex plane coordinates with real and imaginary components. The plot is centered around the origin, with the real axis extending horizontally and the imaginary axis vertically.

Overall Behavior and Trends:
The plot shows a loop starting from the point labeled \(L(0)\) on the positive real axis and looping around the origin. The trajectory of \(L(\omega)\) for \(\omega > 0\) is shown in black, while the trajectory for \(\omega < 0\) is shown in gray. The loop passes close to the point \(-1\) on the real axis, indicating the critical point for stability analysis.

Key Features and Technical Details:
- The loop does not encircle the \(-1\) point, suggesting unconditional stability.
- The trajectory indicates a phase margin greater than \(90^\circ\), which is a desirable condition for stability in feedback systems.
- The dashed circle around the origin represents a reference magnitude, typically used to evaluate the gain margin.

Annotations and Specific Data Points:
- The point \(L(0)\) is marked on the positive real axis, indicating the starting point of the frequency response.
- The critical point \(-1\) is marked on the real axis, serving as a reference for assessing stability.
- The phase margin (PM) is not explicitly labeled on the polar plot but is indicated to be greater than \(90^\circ\) based on the loop's position relative to the \(-1\) point.

Fig. 5.8 Graphical illustration of the unconditional stability and $90^{\circ}$ phase margin of first-order feedback systems: (a) Bode plot and (b) polar plot of open-loop frequency response, L( $\omega$ ).

Thus, we have the following important relationship for this first-order model:

$$
\begin{equation*}
\omega_{\mathrm{t}} \cong \mathrm{~L}_{0} \omega_{\mathrm{p} 1} \tag{5.25}
\end{equation*}
$$

Substituting (5.25) into (5.22) for the case in which $\omega \gg \omega_{\mathrm{pl}}$, we have at midband frequencies

$$
\begin{equation*}
\mathrm{L}(\mathrm{~s}) \cong \frac{\omega_{\mathrm{t}}}{\mathrm{~s}} \tag{5.26}
\end{equation*}
$$

The relationship (5.26) is a simplified first-order model that assumes infinite dc gain, and is therefore not accurate at low frequencies. However, it can be used to analyze the system at midband frequencies, $\omega_{\mathrm{p} 1}<<\omega<\omega_{\mathrm{t}}$, including estimating the closed-loop circuit's -3 dB frequency and settling time.

At midband frequencies, the transfer function of the closed-loop amplifier may be found by substituting (5.26) into (5.8), resulting in

$$
\begin{equation*}
A_{C L}(s) \cong \frac{1}{\beta} \frac{1}{\left(1+s / \omega_{t}\right)} \tag{5.27}
\end{equation*}
$$

As expected, the closed-loop amplifier has a closed-loop gain at low frequencies approximately equal to $1 / \beta$. The -3 dB frequency of the closed-loop amplifier is given by

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}} \cong \omega_{\mathrm{t}} \tag{5.28}
\end{equation*}
$$

Furthermore, from (5.27) we recognize that the closed-loop amplifier is a first-order system with a time-constant, $\tau$, given by

$$
\begin{equation*}
\tau=\frac{1}{\omega_{-3 \mathrm{~dB}}}=\frac{1}{\omega_{t}} \tag{5.29}
\end{equation*}
$$

The settling-time performance of integrated amplifiers is often an important design parameter. For example, in switched-capacitor circuits, the charge from one or more capacitors must be mostly transferred to a feedback capacitor within about half a clock period. This charge transfer is closely related to the opamp's step response. As a result, the settling time is defined to be the time it takes for an opamp to reach a specified percentage of its final value when a step input is applied.

Recall that the step response of any first-order circuit is given by

$$
\begin{equation*}
\mathrm{V}_{\text {out }}(\mathrm{t})=\mathrm{V}_{\text {step }}\left(1-\mathrm{e}^{-\mathrm{t} / \tau}\right) \tag{5.30}
\end{equation*}
$$

Here, $\mathrm{V}_{\text {step }}$ is the size of the voltage step. With this exponential relationship, the time required for the first-order closed-loop circuit to settle with a specified accuracy can be found. For example, if $1 \%$ accuracy is required, then one must allow $\mathrm{e}^{-\mathrm{t} / \tau}$ to reach 0.01 , which is achieved at a time of $\mathrm{t}=4.6 \tau$. For settling to within $0.1 \%$ accuracy, the settling time needed becomes approximately $7 \tau$. Also, note that just after the step input, the slope of the output will be at its maximum, given by

$$
\begin{equation*}
\left.\frac{d}{d t} v_{\text {out }}(t)\right|_{t=0}=\frac{V_{\text {step }}}{\tau} \tag{5.31}
\end{equation*}
$$

Key Point: The closed-loop bandwidth of a feedback amplifier is $\omega_{\mathrm{t}}$, independent of the amplifier's 3-dB bandwidth, $\omega_{\mathrm{p} 1}$. The settling time is $1 / \omega_{\mathrm{t}}$

Since a real amplifier will have a finite current available to charge the parasitic capacitances at $\mathrm{v}_{\text {out }}$, in many practical cases for large steps $\mathrm{V}_{\text {step }}$ the amplifier will be unable to change the output voltage at the rate predicted by (5.31). In such a case, the amplifier is no longer behaving linearly and the model's predictions break down.

#### EXAMPLE 5.6

One phase of a switched-capacitor circuit is shown in Fig. 5.9, where the input signal can be modelled as a voltage step and $0.1 \%$ accuracy is needed in $0.1 \mu \mathrm{~s}$. Assuming linear settling, find the required unity-gain frequency in terms of the capacitance values, $C_{1}$ and $C_{2}$. For $C_{2}=10 C_{1}$, what is the necessary unity-gain frequency of the opamp? What unity-gain frequency is needed in the case $\mathrm{C}_{2}=0.2 \mathrm{C}_{1}$ ?

#### Solution

We first note that a capacitive feedback network is used rather than a resistive one. A difficulty with this network in a nonswitched circuit is that no bias current can flow into the negative opamp input terminal. However, in a switched circuit using a CMOS opamp, the shown configuration occurs only for a short time and does not cause any problems. Second, assume the opamp has a dominant pole response with unity gain frequency $\omega_{\mathrm{ta}}$ (different from the unity gain frequency of $L(s)$, defined as $\omega_{t}$ ) and large dc gain. Hence, its frequency response at midband

Fig. 5.9 (a) One phase of $a$ switched-capacitor circuit. (b) Open-loop feedback circuit illustrating L(s)
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: InN}
name: C2, type: Capacitor, value: C2, ports: {Np: InN, Nn: Vout}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN, OutP: Vout}
]
extrainfo:The circuit is a switched-capacitor circuit phase with a capacitive feedback network and an operational amplifier. The input voltage Vin is coupled through C1, and C2 provides feedback from the output to the inverting input of the op-amp.

image_name:(b)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: Out(A1), Nn: Vout}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: vin, OutP: Out(A1)}
]
extrainfo:The circuit is a switched-capacitor phase with a capacitive feedback network and an operational amplifier. The input voltage Vin is coupled through C1, and C2 provides feedback from the output to the inverting input of the op-amp. The open-loop response L(s) is approximated by (s/ωta)(C2/(C1+C2)).

frequencies is well approximated by $s / \omega_{\mathrm{ta}}$. The open-loop response, $L(s)$, is given by this opamp response driving the capacitive feedback network, as shown in Fig. 5.9(b).

$$
\begin{equation*}
L(s) \cong\left(\frac{s}{\omega_{\mathrm{ta}}}\right)\left(\frac{\mathrm{C}_{2}}{\mathrm{C}_{1}+\mathrm{C}_{2}}\right) \tag{5.32}
\end{equation*}
$$

The unity gain frequency of $L(s)$ is found by substituting (5.32) into (5.15) and solving for $\omega_{\mathrm{t}}=\omega_{\mathrm{ta}} \mathrm{C}_{2} /\left(\mathrm{C}_{1}+\mathrm{C}_{2}\right)$. For $7 \tau$ settling within $0.1 \mu \mathrm{~s}$, we see that $\tau$ must be less than 14.2 ns . Since $\tau=1 / \omega_{\mathrm{t}}$,

$$
\begin{equation*}
\omega_{\mathrm{ta}} \geq\left(\frac{\mathrm{C}_{1}+\mathrm{C}_{2}}{\mathrm{C}_{2}}\right)\left(\frac{1}{14.2 \mathrm{~ns}}\right) \tag{5.33}
\end{equation*}
$$

For the case in which $\mathrm{C}_{2}=10 \mathrm{C}_{1}$, a unity-gain frequency of $2 \pi \cdot 12.3 \mathrm{MHz}$ is needed, whereas in the case of $\mathrm{C}_{2}=0.2 \mathrm{C}_{1}$, $\omega_{\mathrm{ta}}$ should be larger than $2 \pi \cdot 66.8 \mathrm{MHz}$.

The unconditional stability, predictable bandwidth, and predictable settling time of first-order systems are strong incentives to ensure feedback circuits have a dominant pole and, therefore, may be approximated by the single-pole model in (5.22).

### 5.3.2 Second-Order Feedback Systems

Although first-order feedback amplifiers exhibit several desirable characteristics, practical feedback amplifiers generally have more than one pole. Recall that the main objective in the design of the amplifier $A$ is that it must have large low-frequency gain. Unfortunately, the maximum gain achievable with a single transistor, given by its intrinsic gain $A_{i}=g_{m} r_{d s}$, is usually insufficient. Hence, multiple transistors must be combined resulting in a more complex circuit with several nodes and, inevitably, multiple poles.

A general second-order feedback loop transfer function is,

$$
\begin{equation*}
\mathrm{L}(\mathrm{~s})=\frac{\mathrm{L}_{0}}{\left(1+\mathrm{s} / \omega_{\mathrm{p} 1}\right)\left(1+\mathrm{s} / \omega_{\mathrm{eq}}\right)} \tag{5.34}
\end{equation*}
$$

It is assumed that $\omega_{\text {eq }}>\omega_{\mathrm{p} 1}$. It is clear from the Bode plot of (5.34) in Fig. 5.7 that it will be unconditionally stable since a phase shift of $-180^{\circ}$ is never attained. However, the phase margin may approach $0^{\circ}$ depending on $L_{0}, \omega_{p}$, and $\omega_{\text {eq }}$.

At frequencies much greater than the dominant pole frequency, $\omega \gg \omega_{\mathrm{p} 1}$, we see that $1+j \omega / \omega_{\mathrm{p} 1} \cong j \omega / \omega_{\mathrm{p} 1}$, and so (5.34) can be accurately approximated by

$$
\begin{equation*}
\mathrm{L}(\mathrm{~s}) \cong \frac{\omega_{\mathrm{t}}}{\mathrm{~s}\left(1+\mathrm{s} / \omega_{\mathrm{eq}}\right)} \tag{5.35}
\end{equation*}
$$

Key Point: All-pole sec-ond-order feedback systems are unconditionally stable with a phase margin of between 90 and 0 degrees.

Note that this approximation result is especially valid at the unity-gain frequency of the loop $\omega_{\mathrm{t}}$ (which we are presently interested in) which is almost certainly much greater than $\omega_{\mathrm{p} 1}$ as long as $\mathrm{L}_{0}$ » 1 .

Since $L(s)=\beta A(s)$ where $\beta$ is a scalar constant, it is clear that the poles are contributed by the forward amplifier, $\mathrm{A}(\mathrm{s})$. Using (5.34) we can define $\mathrm{A}_{0}=\mathrm{L}_{0} / \beta$ which is the dc gain of $\mathrm{A}(\mathrm{s})$ and $\omega_{\mathrm{ta}}=\mathrm{A}_{0} \omega_{\mathrm{p} 1}$ as the approximate unity-gain frequency of $\mathrm{A}(\mathrm{s})$ under a dominant pole approximation. Hence, at frequencies around $\omega_{\mathrm{t}}$, the loop gain, $L(\mathrm{~s})$, is given by

$$
\begin{equation*}
L(s)=\beta A(s)=\frac{\beta \omega_{\mathrm{ta}}}{s\left(1+s / \omega_{\mathrm{eq}}\right)} \tag{5.36}
\end{equation*}
$$

The unity-gain frequency, $\omega_{\mathrm{t}}$, can now be found by setting the magnitude of (5.36) equal to unity after substituting $\mathrm{s}=\mathrm{j} \omega_{\mathrm{t}}$. Once this is done and the equation is rearranged, one can write,

$$
\begin{equation*}
\beta \frac{\omega_{\mathrm{ta}}}{\omega_{\mathrm{eq}}}=\frac{\omega_{\mathrm{t}}}{\omega_{\mathrm{eq}}} \sqrt{1+\left(\frac{\omega_{\mathrm{t}}}{\omega_{\mathrm{eq}}}\right)^{2}} \tag{5.37}
\end{equation*}
$$

For the dominant pole special case in which the unity-gain frequency is much less than the equivalent nondominant pole frequency (i.e., $\omega_{\mathrm{t}}$ « $\omega_{\text {eq }}$ ), (5.37) may be simplified to

$$
\begin{equation*}
\omega_{\mathrm{ta}}=\frac{\omega_{\mathrm{t}}}{\beta} \sqrt{1+\left(\frac{\omega_{\mathrm{t}}}{\omega_{\mathrm{eq}}}\right)^{2}} \cong \frac{\omega_{\mathrm{t}}}{\beta} \tag{5.38}
\end{equation*}
$$

From (5.36), the phase shift, $\angle \mathrm{L}(\omega)$, is found.

$$
\begin{equation*}
\angle \mathrm{L}(\omega)=-90^{\circ}-\tan ^{-1}\left(\omega / \omega_{\mathrm{eq}}\right) \tag{5.39}
\end{equation*}
$$

This equation implies that at the unity-gain frequency, $\omega=\omega_{\mathrm{t}}$, we have

$$
\begin{equation*}
\mathrm{PM}=\angle \mathrm{L}\left(\omega_{\mathrm{t}}\right)-\left(-180^{\circ}\right)=90^{\circ}-\tan ^{-1}\left(\omega_{\mathrm{t}} / \omega_{\mathrm{eq}}\right) \tag{5.40}
\end{equation*}
$$

and, therefore,

Key Point: The process of designing or modifying a feedback amplifier to have some targeted phase margin is called compensation.

$$
\begin{align*}
\omega_{\mathrm{t}} / \omega_{\mathrm{eq}} & =\tan \left(90^{\circ}-\mathrm{PM}\right)  \tag{5.41}\\
\Rightarrow \omega_{\mathrm{t}} & =\tan \left(90^{\circ}-\mathrm{PM}\right) \omega_{\mathrm{eq}}
\end{align*}
$$

Equation (5.41) gives the required $\omega_{\mathrm{t}} / \omega_{\text {eq }}$ for a specified phase margin. The process of designing or modifying a feedback amplifier to have the ratio $\omega_{\mathrm{t}} / \omega_{\text {eq }}$ required by (5.41) for some targeted phase margin is called compensation.

#### EXAMPLE 5.7

A closed-loop amplifier is to have a $75^{\circ}$ phase margin for $\beta=1$. What is the required unity-gain frequency $f_{t}$ if $f_{\text {eq }}=\omega_{\text {eq }} /(2 \pi)=50 \mathrm{MHz}$ ? What is the required $f_{\mathrm{ta}}$ ?

#### Solution

Using (5.40), we have $\omega_{\mathrm{t}}=0.268 \omega_{\text {eq }}$, which implies that the loop-gain unity-gain frequency is given by $f_{t}=\omega_{t} / 2 \pi=13.4 \mathrm{MHz}$. Using (5.38), we also have, for $\beta=1$, $\omega_{\mathrm{ta}}=\omega_{\mathrm{t}} \sqrt{1+0.268^{2}}=1.035 \omega_{\mathrm{t}}$, which implies that $\mathrm{f}_{\mathrm{ta}}=\omega_{\mathrm{ta}} / 2 \pi=13.9 \mathrm{MHz}$.

The closed-loop response of a second-order feedback amplifier may be found by substituting (5.34) into (5.8) and rearranging.

$$
\begin{equation*}
\mathrm{A}_{\mathrm{CL}}(\mathrm{~s})=\frac{\mathrm{A}_{\mathrm{CL} 0}}{1+\frac{\mathrm{s}\left(1 / \omega_{\mathrm{p} 1}+1 / \omega_{\mathrm{eq}}\right)}{1+\mathrm{L}_{0}}+\frac{\mathrm{s}^{2}}{\left(1+\mathrm{L}_{0}\right)\left(\omega_{\mathrm{p} 1} \omega_{\mathrm{eq}}\right)}} \tag{5.42}
\end{equation*}
$$

where

$$
\begin{equation*}
A_{C L 0} \equiv \frac{\mathrm{~L}_{0} / \beta}{1+\mathrm{L}_{0}} \cong \frac{1}{\beta} \tag{5.43}
\end{equation*}
$$

Table 5.1 The relation ship betw een $\mathrm{PM}, \omega_{\mathrm{t}} / \omega_{\text {eq }}, Q$ fact or, and percentage overshoot

| PM <br> (Phase margin) | $\omega_{\mathbf{t}} / \omega_{\text {eq }}$ | Q factor | Percentage <br> overshoot for a <br> step input |
| :---: | :---: | :---: | :---: |
| $55^{\circ}$ | 0.700 | 0.925 | $13.3 \%$ |
| $60^{\circ}$ | 0.580 | 0.817 | $8.7 \%$ |
| $65^{\circ}$ | 0.470 | 0.717 | $4.7 \%$ |
| $70^{\circ}$ | 0.360 | 0.622 | $1.4 \%$ |
| $75^{\circ}$ | 0.270 | 0.527 | $0.008 \%$ |
| $80^{\circ}$ | 0.175 | 0.421 | - |
| $85^{\circ}$ | 0.087 | 0.296 | - |

Thus, the closed-loop response is also second-order. The general equation for a second-order all-pole transfer function is

$$
\begin{equation*}
H(s)=\frac{K \omega_{0}^{2}}{s^{2}+\left(\frac{\omega_{0}}{Q}\right) s+\omega_{0}^{2}}=\frac{K}{1+\frac{s}{\omega_{0} Q}+\frac{s^{2}}{\omega_{0}^{2}}} \tag{5.44}
\end{equation*}
$$

Recall from the preceding chapter that $\omega_{0}$ is called the resonant frequency and parameter Q is called the Q factor ${ }^{5}$ [Sedra, 1991]. If $\mathrm{Q}=\sqrt{1 / 2} \cong 0.707$, then the magnitude response will have a -3 -dB frequency equal to $\omega_{0}$. Lower Q -factors $(\mathrm{Q}<\sqrt{1 / 2}$ ) result in lower bandwidth whereas higher Q -factors $(\mathrm{Q}>\sqrt{1 / 2}$ ) result in peaking in the frequency response. Furthermore, recall that if $Q \leq 0.5$ both poles of $A_{C L}(s)$ are real and there is no overshoot in the feedback amplifier's step response. In the case where $Q>0.5$, the percentage overshoot of the step response is given by

$$
\begin{equation*}
\% \text { overshoot }=100 e^{\frac{-\pi}{\sqrt{4 Q^{2}-1}}} \tag{5.45}
\end{equation*}
$$

Equating (5.42) with (5.44) and solving for $\omega_{0}$ and Q results in

$$
\begin{equation*}
\omega_{0}=\sqrt[t]{\left(1+\mathrm{L}_{0}\right)\left(\omega_{\mathrm{p} 1} \omega_{\mathrm{eq}}\right)} \cong \sqrt{\omega_{i} \omega_{\mathrm{eq}}} \tag{5.46}
\end{equation*}
$$

and

$$
\begin{equation*}
Q=\frac{\sqrt{\left(1+\mathrm{L}_{0}\right) / \omega_{\mathrm{p} 1} \omega_{\mathrm{eq}}}}{1 / \omega_{\mathrm{p} 1}+1 / \omega_{\mathrm{eq}}} \cong \sqrt{\frac{\mathrm{~L}_{0} \omega_{\mathrm{p} 1}}{\omega_{\mathrm{eq}}}}=\sqrt{\frac{\beta \omega_{\mathrm{ta}}}{\omega_{\mathrm{eq}}}} \tag{5.47}
\end{equation*}
$$

where the approximation on $Q$ is valid since $L_{0}>>1$ and $\omega_{\mathrm{p} 1}<<\omega_{\mathrm{eq}}$.
It is now possible to relate a specified phase margin to the Q factor of the resulting closed-loop amplifier. Equation (5.41) can be used to find $\omega_{\mathrm{t}} / \omega_{\mathrm{eq}}$. This result can be substituted into (5.37) to find $\beta\left(\omega_{\mathrm{ta}} / \omega_{\mathrm{eq}}\right)$, which can then be substituted into (5.47) to find the equivalent Q factor. Finally, (5.45) can be used to find the corresponding percentage overshoot for a step input. This procedure gives us the information in Table 5.1.

Table 5.1 leads to some interesting observations. First, a frequency response with $Q \cong \sqrt{1 / 2}$ roughly corresponds to a phase margin of $65^{\circ}$. Therefore, a common specification is to design for a phase margin of at least $65^{\circ}$ in the presence of both process and temperature changes as this ensures no peaking in the closed-loop amplifier's frequency response. If one wants to ensure that there is no overshoot for a step input, then the phase margin should be at least $75^{\circ}$, again, given both process and temperature variations. Hence, a nominal phase margin of $80^{\circ}$ to $85^{\circ}$ is often targeted to account for these variations.
5. The Q factor is $1 / 2$ times the inverse of the damping factor. The damping factor is an alternative method of indicating the pole locations in second-order transfer functions.

Finally, it is worth mentioning that when an amplifier is designed for use with many different feedback networks, the worst-case phase margin occurs for the maximum value of $\beta$ which corresponds to the smallest closedloop gain. Thus, the amplifier is designed to have sufficient phase margin for the maximum value of $\beta$. It is then guaranteed to have even greater phase margin for all other $\beta$, although in these cases it will be sub-optimally compensated and will be slower than necessary.

### 5.3.3 Higher-Order Feedback Systems

High-gain amplifiers will often include more than two poles, and perhaps some zeroes. A general transfer function for such an amplifier is

$$
\begin{equation*}
A(s)=A_{0} \frac{\left(1+\frac{s}{\omega_{\mathrm{z} 1}}\right)\left(1+\frac{\mathrm{s}}{\omega_{\mathrm{z} 2}}\right) \ldots\left(1+\frac{\mathrm{s}}{\omega_{\mathrm{zm}}}\right)}{\left(1+\frac{\mathrm{s}}{\omega_{\mathrm{p} 1}}\right)\left(1+\frac{\mathrm{s}}{\omega_{\mathrm{p} 2}}\right) \ldots\left(1+\frac{\mathrm{s}}{\omega_{\mathrm{pn}}}\right)} \tag{5.48}
\end{equation*}
$$

Feedback systems based on such amplifiers are not necessarily stable since, at some frequency, they may attain a phase shift beyond $180^{\circ}$.

It is important to accurately model the open-loop transfer function at frequencies up to and around the loop's unity-gain frequency, $\omega_{\mathrm{t}}$. This can be done with the first-order model (5.22) only when the second and higherorder poles and all zeros are at frequencies much higher than $\omega_{\mathrm{t}}$,

$$
\begin{equation*}
\omega_{\mathrm{t}} « \omega_{\mathrm{p} 2}, \ldots, \omega_{\mathrm{pn}},\left|\omega_{\mathrm{z} 1}\right|, \ldots,\left|\omega_{\mathrm{zm}}\right| \tag{5.49}
\end{equation*}
$$

Even when it is possible to design an amplifier that satisfies (5.49), doing so is often overly-conservative resulting in significant over-design and a sub-optimal circuit. Instead, by accounting for all poles and zeros the specified phase margin can be achieved with a higher unity-gain frequency, $\omega_{\mathrm{t}}$, which as we saw in Section 5.1.3 will result in a higher closed-loop bandwidth.

Key Point: Higher-order feedback amplifiers may be modeled using a second-order transfer function so long at they are not approaching instability. The second pole is chosen as the frequency at which a phase response of -135 degrees is attained.

When all poles and zeros are on the real axis, they can be modelled reasonably well by just two poles. Specifically, we include in our model the first dominant-pole frequency, $\omega_{\mathrm{pl}}$, and a second pole frequency that models all higher-frequency poles and zeros, $\omega_{\text {eq }}$. Given a set of real-axis poles, $\omega_{\mathrm{pi}}$, and zeros, $\omega_{\mathrm{zi}}$, a good choice for $\omega_{\mathrm{eq}}$ is given by

$$
\begin{equation*}
\frac{1}{\omega_{\text {eq }}} \cong \sum_{i=2}^{n} \frac{1}{\omega_{p i}}-\sum_{i=1}^{m} \frac{1}{\omega_{z i}} \tag{5.50}
\end{equation*}
$$

It should be noted here that the approximation in (5.50) is different than that given in [Sedra, 1991] since we are mostly interested in the phase shifts due to higher-frequency poles and zeros, rather than the attenuation. In practice, $\omega_{\text {eq }}$ is found from simulation as the frequency at which the open-loop transfer function, $L(s)$, has a $-135^{\circ}$ phase shift $\left(-90^{\circ}\right.$ due to the dominant pole and another $-45^{\circ}$ due to the combined effect of higher-frequency poles and zeros).

## 5.4 COMMON FEEDBACK AMPLIFIERS

We will now apply our general analysis of feedback systems to small-signal circuits. In order to do so, we must cast the circuit of interest into the model of Fig. 5.1. Unfortunately, this is often easier said than done. There may be ambiguity in identifying whether the inputs and/or outputs of a particular circuit are voltages or currents. Furthermore, the forward amplifier, $A$, and feedback network, $\beta$, are difficult to discern. Some components in a circuit are simultaneously involved in both the forward amplifier and the feedback network.

In particular, it is difficult to find A . For example, consider the inverting amplifier configuration in Fig. 5.10 where the opamp has a finite output impedance, $Z_{0}$. It is tempting to conclude that $A$ is simply the voltage gain of the opamp, but this is not the case. Equation (5.5) and Fig. 5.1 show that when $A=0$ the closed-loop amplifier output must be zero. However, even if the gain of the opamp were zero, a finite voltage would appear at $v_{\text {out }}$ due to division of the source voltage, $v_{s}$, by impedances in the feedback network $\left(Z_{1}\right.$ and $\left.Z_{2}\right)$ and at the output node ( $Z_{0}$ and $Z_{L}$ ). In fact, an accurate analysis for A is quite complex even in this every-day example. It depends not only on the opamp but also the feedback components $Z_{1}$ and $Z_{2}$, and the load, $Z_{L}$. Computer simulation is of little help since it is not obvious exactly what circuit must be simulated to find $A$, the forward gain without feedback.

On the other hand, the value of $\beta$ is usually relatively obvious if one remembers that the circuit's desired gain is simply $1 / \beta$. For example, the gain we expect from the inverting opamp configuration above is well-known to be $-\left(Z_{2} / Z_{1}\right)$. Hence, we may assume that $\beta=-\left(Z_{1} / Z_{2}\right)$. More generally, the value of $\beta$ is the inverse of the closed-loop gain we expect under ideal conditions of very large loop gain. In opamp circuits, this gain will result from analyzing the circuit assuming infinite opamp gain. Although this choice of $\beta$ does not necessarily identify the gain between any two particular voltages and/or currents in the circuit, this need not trouble us-it clearly is in keeping with our immediate goal of casting the circuit into the ideal feedback model, and more importantly allows us to find the properties of a feedback circuit that are of most interest to us such as gain error, bandwidth, phase margin, and settling time.

Whereas there may be some ambiguity in defining $A$, the loop gain $L$ is unique. This is satisfying since stability of the loop depends only on $L(s)$, and physically a feedback circuit will be either stable of unstable, regardless of how we choose to analyze it.

If $L$ is known and $\beta$ is taken by definition to be the reciprocal of the desired closed-loop gain, rather than trying to perform a rigorous analysis for $A$ we can infer it from $A=L / \beta$. Therefore, our analysis of feedback circuits will be based on a knowledge of $\beta$, ours either by design or by inspection of a relatively simply circuit, and from a knowledge of $L$ which can be estimated using a systematic procedure described in Section 5.4.1.

Generalizing the expression for closed-loop gain in (5.8), the closed-loop frequency response of a feedback circuit can be expressed without reference to $A(\mathrm{~s})$.

$$
\begin{equation*}
A_{C L}(s)=\frac{1}{\beta} \cdot \frac{L(s)}{1+L(s)} \tag{5.51}
\end{equation*}
$$

In (5.51) the term $L(s) /(1+L(s))$ is the closed-loop amplifier gain normalized to the desired gain, $1 / \beta$. Many circuit attributes of interest to us may be thought of in terms of this normalized frequency response which depends only upon $L(\mathrm{~s})$. For example, the bandwidth, the poles and the zeros of the closed-loop amplifier are those of $\mathrm{L}(\mathrm{s}) /(1+\mathrm{L}(\mathrm{s}))$. The gain error at dc, defined as the fractional error between the desired gain, $1 / \beta$, and the actual gain, $\mathrm{A}_{\mathrm{CL} 0}=\mathrm{A}_{\mathrm{CL}}(0)$, is simply

$$
\begin{equation*}
\text { Gain error }=1-\frac{\mathrm{A}_{\mathrm{CL} 0}}{1 / \beta}=1-\frac{\mathrm{L}_{0}}{1+\mathrm{L}_{0}} \tag{5.52}
\end{equation*}
$$

Key Point: Feedback systems may be analyzed in terms of their desired gain, $\beta$, and loop gain, $L(\omega)$, from which the closed-loop amplifier's gain, bandwidth, phase margin, and frequency response may all be inferred.
which will clearly assume a value very close to zero so long as the loop gain at dc, $L_{0}=L(0)$, is large.
image_name:Fig. 5.10 An inverting opamp configuration.
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: Z1, type: Resistor, value: Z1, ports: {N1: Vs, N2: InN(A1)}
name: Z2, type: Resistor, value: Z2, ports: {N1: InN(A1), N2: Vout}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Vout, OutN: GND}
name: ZL, type: Resistor, value: ZL, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is an inverting op-amp configuration with feedback resistors Z1 and Z2 setting the gain. The load resistor ZL is connected at the output Vout.

Fig. 5.10 An inverting opamp configuration.

### 5.4.1 Obtaining the Loop Gain, L(s)

To find the loop gain of a feedback circuit, we break the loop, insert a test signal (either voltage or current) and see what signal the loop returns to the other side of the break. The procedure is illustrated in Fig. 5.11. Specifically, for any (small-signal) feedback circuit,

1. Set any independent sources in the circuit equal to zero, including the input source. Zeroing a voltage source means replacing it will a short circuit. (A short circuit is an ideal voltage source of 0 V.) Zeroing a current source means replacing it with an open circuit. (An open circuit is an ideal current source with a value of 0 A .)
2. Break the loop. Find the impedance at the break point, $Z_{t}$, and terminate the loop with this impedance as shown in Fig. 5.11.
3. Insert a test signal (either voltage, $\mathrm{v}_{\mathrm{t}}$, or current, $\mathrm{i}_{\mathrm{t}}$ ) into the loop at the break and find the returned signal: either the voltage across $Z_{t}, v_{r}$, or the current through $Z_{t}, i_{r}$. The loop gain is then

$$
\begin{equation*}
L=-\frac{v_{r}}{v_{t}} \text { (voltage test signals) or }-\frac{i_{r}}{i_{t}} \text { (current test signals). } \tag{5.53}
\end{equation*}
$$

image_name:Fig. 5.11
description:The circuit is used to determine the loop gain L by breaking the loop and inserting a test signal. The loop gain is calculated as L = -Vr/Vt or -Ir/It. The diagram shows a series of blocks, each containing a resistor, capacitor, and a voltage-controlled voltage source, connected in a loop with a test impedance Zt and test voltage Vt.

Fig. 5.11 Determining the loop gain, L, by breaking the loop.

The key step is 2 . Although the loop may be broken anywhere, it is convenient to do so right at an ideal voltage or current source so that the terminating impedance plays no role in the result, and hence may be omitted. Alternatively, one may chose a point in the loop where the terminating impedance is easily found.

The loop gain obtained in this manner is actually an approximation since it neglects the possibility of signals circulating in the opposite direction around the loop. The approximation is accurate so long as the gain

Key Point: The loop gain, $\mathrm{L}(\omega)$, may be estimated by zeroing the input, breaking the loop, and injecting a test signal. This is an accurate approximation in the typical case where high forward gain around the loop is being traded for increased bandwidth, accuracy, etc.
around the loop in the forward direction (clockwise in Fig. 5.11) is much greater than the gain in the opposite direction (counterclockwise in Fig. 5.11). This will generally be the case in the circuits of present interest to us where feedback is used to trade high gain for other desirable properties, as described in Section 5.1.

#### EXAMPLE 5.8

Find the loop gain, $L(s)$, and closed-loop gain, $A_{C L}(s)$, of the inverting opamp configuration shown in Fig. 5.10 where the load impedance, $Z_{L}$, is infinite. Assume the opamp has a voltage gain $A_{v}$, and an infinite input impedance.

#### Solution

The small-signal equivalent representation of the circuit is shown in Fig. 5.12(a). To this circuit, we apply the procedure for determining the loop gain.

1. The input source is zeroed by setting $\mathrm{v}_{\mathrm{s}}$ to ground.
2. The loop is broken at the opamp input terminals. This point is chosen because the input impedance there is infinite, so finding $Z_{t}$ is trivial.
3. The test signal $v_{t}$ is injected into the new circuit, Fig. $5.12(b)$. The returned voltage is determined by nodal analysis,

$$
v_{r}=-A_{v}(s) \frac{Z_{1}}{Z_{1}+Z_{2}+Z_{0}} v_{t}
$$

Hence, the loop gain is

$$
L(s)=-\frac{v_{r}}{v_{t}}=A_{v}(s) \frac{Z_{1}}{Z_{1}+Z_{2}+Z_{0}}
$$

The normalized closed-loop gain is

$$
\frac{L(s)}{1+L(s)}=\frac{A_{v}(s) Z_{1}}{A_{v}(s) Z_{1}+Z_{1}+Z_{2}+Z_{o}}
$$

The desired gain of this circuit is $1 / \beta=-\left(Z_{2} / Z_{1}\right)$, so the closed loop gain is given by (5.51),

$$
A_{\mathrm{CL}}(\mathrm{~s})=-\frac{Z_{2}}{Z_{1}} \cdot \frac{A_{v}(s) Z_{1}}{A_{v}(s) Z_{1}+Z_{1}+Z_{2}+Z_{o}}
$$

As long as $A_{v}$ » $\left(Z_{1}+Z_{2}+Z_{0}\right) / Z_{1}$, the closed-loop gain will approximately equal the desired gain. The same result may be obtained by direct nodal analysis of the circuit in Fig. 5.12(a) without breaking the loop.
(a)
image_name:Fig. 5.12 (b)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: Z1, type: Resistor, value: Z1, ports: {N1: Vs, N2: -Vi}
name: Z2, type: Resistor, value: Z2, ports: {N1: -Vi, N2: Vout}
name: Opamp, type: OpAmp, value: Av(s), ports: {InP: GND, InN: -Vi, OutP: Vout}
name: Zo, type: Resistor, value: Zo, ports: {N1: Vout, N2: GND}
]
extrainfo:This circuit represents a small-signal model of an inverting op-amp configuration with a feedback loop. The loop is broken at the indicated point for analysis of the loop gain.

(b)
image_name:Fig. 5.12 (b)
description:
[
name: Vs, type: VoltageSource, value: 0, ports: {Np: GND, Nn: Vs}
name: Z1, type: Resistor, value: Z1, ports: {N1: Vr, N2: GND}
name: Z2, type: Resistor, value: Z2, ports: {N1: Vr, N2: Vout}
name: Av(s)Vi, type: VoltageControlledVoltageSource, ports: {Np: Vout, Nn: GND}
name: Zo, type: Resistor, value: Zo, ports: {N1: Av(s)*Vi, N2: Vout}
]
extrainfo:This circuit represents a configuration for determining the loop gain L = -vr/vt of a small-signal model. It includes a feedback loop broken at a specific point for analysis. The voltage source Vs is set to 0, indicating a test condition for loop gain measurement.

Fig. 5.12 (a) Small-signal model of an inverting opamp configuration. (b) Circuit for determining the loop gain, $L=-v_{r} / v_{t}$.

#### EXAMPLE 5.9

Find the loop gain of the differential pair feedback circuit shown in Fig. 5.13(a).

#### Solution

We are considering only the small-signal response of the circuit, so we first take the circuit's small-signal equivalent, shown in Fig. 5.13(b) where it is naturally assumed that $Q_{1,2}$ and $Q_{3,4}$ are matched device pairs. A simplified small-signal model of the differential pair with active load is adopted; for complete details the reader is referred to Chapter 3.

The circuit for determining the loop gain is shown in Fig. 5.13(c).

1. The input source is zeroed by setting $\mathrm{v}_{\mathrm{in}}$ to ground.
2. The loop is broken at the gate of $M 2$. This point is chosen because the terminating impedance, $Z_{t}$, is simply the input capacitance to the differential pair. In the circuit of Fig. 5.13( $c$ ), this terminating capacitance is placed in parallel with the (much larger) $\mathrm{C}_{\mathrm{L}}$, so any inaccuracy in accounting for all the parasitic components of the input capacitance will have little effect on the subsequent analysis.
3. A test source, $\mathrm{v}_{\mathrm{t}}$, is introduced at the break point. The circuit of Fig. $5.13(c)$ must now be analyzed to find $\mathrm{L}=-\left(\mathrm{v}_{\mathrm{r}} / \mathrm{v}_{\mathrm{t}}\right)$. The analysis at dc follows.
image_name:(a)
description:The circuit diagram (a) represents a unity-gain feedback circuit with two NMOS transistors (Q1 and Q2) and three PMOS transistors (Q3, Q4, and Q5). The circuit is configured to provide negative feedback with the output voltage 'Vout' being fed back to the gates of the PMOS transistors. The capacitor 'CL' is the load capacitance at the output, and 'Cgs,1/2' and 'Cgs,5' are gate-source capacitances. The circuit includes voltage-controlled current sources and several resistive and capacitive elements to stabilize the feedback loop.
image_name:(b)
description:The circuit diagram represents a small-signal equivalent model for a unity-gain feedback circuit. It includes capacitors, resistors, and a voltage-controlled current source. The node 'Vgs,5' is connected to the gate-source voltage of a transistor, while 'Vout' is the output node. The diagram is used to analyze the loop gain of the circuit.
image_name:(c)
description:The circuit is a small-signal model used to analyze the loop gain L = -vr/vt. It includes MOSFET devices and capacitors to model parasitic effects in the feedback loop.

Fig. 5.13 (a) A unity-gain feedback circuit. (b) Its small-signal equivalent. (c) The small-signal circuit for finding the loop gain, $L=-v_{r} / v_{t}$.

Since the impedance looking into the gate of $Q_{5}$ is infinite at dc, the small-signal gate voltage is

$$
\mathrm{v}_{\mathrm{g}, 5}=-\mathrm{g}_{\mathrm{m}, 1} \mathrm{v}_{\mathrm{t}}\left(\mathrm{r}_{\mathrm{ds}, 1}| | \mathrm{r}_{\mathrm{ds}, 3}\right)
$$

The returned voltage is then given by a voltage division,

$$
v_{r}=v_{g, 5}\left(\frac{g_{m, 5}}{g_{m, 5}+1 / r_{d s, 5}+g_{m b, 5}}\right)=-\left[\frac{g_{m, 1}\left(r_{d s, 1}| | r_{d s, 3}\right) g_{m, 5}}{g_{m, 5}+1 / r_{d s, 5}+g_{m b, 5}}\right] v_{t}
$$

Hence, the loop gain at dc is

$$
\mathrm{L}=\frac{\mathrm{g}_{\mathrm{m}, 1}\left(\mathrm{r}_{\mathrm{ds}, 1}| | \mathrm{r}_{\mathrm{ds}, 3}\right) \mathrm{g}_{\mathrm{m}, 5}}{\mathrm{~g}_{\mathrm{m}, 5}+1 / \mathrm{r}_{\mathrm{ds}, 5}+\mathrm{g}_{\mathrm{mb}, 5}}
$$

The high-frequency analysis is left as an exercise for the reader, where it may be useful to refer to the commonsource amplifier high-frequency analysis presented in Chapter 4.

This approach is also very useful because it can be applied to computer circuit simulations to find the loop gain with great accuracy. However, the preceding steps must only be applied to the small-signal equivalent circuit. In a transistor circuit, the dc biasing connections must not be broken, otherwise some of the circuit's small-signal parameters will be completely altered. This may be achieved in simulation using a very large ideal inductance, as shown in Fig. 5.14. The large inductance is a short at dc thus preserving the dc biasing but is effectively an opencircuit at any frequencies of interest. A test small signal may then be introduced via a large coupling capacitor.

### 5.4.2 Noninverting Amplifier

A classic example of a feedback amplifier is the generalized noninverting opamp shown in Fig. 5.15. The operational amplifier is assumed to have a frequency-dependent voltage gain, $\mathrm{A}_{\mathrm{v}}(\mathrm{s})$, and complex input and output impedances given by $Z_{i}(\mathrm{~s})$ and $Z_{o}(s)$, respectively. A complete circuit model is shown in Fig. 5.16. Note that the
image_name:Fig. 5.14
description:The circuit in Fig. 5.14 breaks the loop using a large ideal inductance and introduces a test signal via a large coupling capacitor to determine the small-signal loop gain in simulation without disturbing the circuit's DC biasing.

Fig. 5.14 Breaking the loop using a large ideal inductance and introducing a test signal via a large coupling capacitor to determine the small-signal loop gain in simulation without disturbing the circuit's dc biasing.

Fig. 5.15 A generalized noninverting feedback operational amplifier configuration.
image_name:Fig. 5.15 A generalized noninverting feedback operational amplifier configuration.
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: Zs, type: Resistor, value: Zs, ports: {N1: Vs, N2: InP(Av)}
name: Z1, type: Resistor, value: Z1, ports: {N1: InN(Av), N2: GND}
name: Z2, type: Resistor, value: Z2, ports: {N1: InN(Av), N2: Vout}
name: ZL, type: Resistor, value: ZL, ports: {N1: Vout, N2: GND}
name: Av, type: OpAmp, value: Av, ports: {InP: InP(Av), InN: InN(Av), OutP: Vout}
]
extrainfo:The circuit is a noninverting feedback operational amplifier configuration with feedback components Z1 and Z2. The input is applied through Vs and Zs, and the output is taken across ZL.

image_name:Fig. 5.16 Small-signal model of a noninverting feedback amplifier
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: Zs, type: Resistor, value: Zs, ports: {N1: Vs, N2: InP(Av)}
name: Zi, type: Resistor, value: Zi, ports: {N1: InP(Av), N2: InN(Av)}
name: Z1, type: Resistor, value: Z1, ports: {N1: InN(Av), N2: GND}
name: Z2, type: Resistor, value: Z2, ports: {N1: InN(Av), N2: Vout}
name: ZL, type: Resistor, value: ZL, ports: {N1: Vout, N2: GND}
name: Zo, type: Resistor, value: Zo, ports: {N1: Av(s)Vi, N2: Vout}
name: Av(s)*Vi, type: VoltageControlVotageSource, value: Av(s)*Vi, ports: {N1: Av(s)*Vi, N2: GND}
]
extrainfo:The circuit is a small-signal model of a noninverting feedback amplifier. It uses an operational amplifier with feedback components Z1 and Z2. The input signal is applied through a voltage source Vs and resistor Zs, and the output is taken across the load resistor ZL. The opamp has a small-signal open-circuit gain Av(s)Vi and is configured with input and feedback resistors Zi and Zo.

Fig. 5.16 Small-signal model of a noninverting feedback amplifier.
gain $A_{v}$ is the (small-signal) open-circuit gain of the opamp and is therefore not equal to the forward-path gain $A$ of the feedback amplifier which must include all loading.

#### EXAMPLE 5.10

An opamp specification indicates an input capacitance of 0.5 pF , an output resistance of $500 \Omega$, a dc gain of 80 dB , and a unity-gain frequency of 100 MHz . The specification also indicates that the opamp has a phase response of -105 degrees at the unity-gain frequency of $A_{v}(s)$. Find the opamp model components: $Z_{i}, Z_{o}$, and $A_{v}(s)$.

#### Solution

The input and output impedances are directly given in the specification.

$$
\begin{gathered}
Z_{i}(s)=\frac{1}{\left(5 \cdot 10^{-13}\right) s} \Omega \\
Z_{0}(s)=500 \Omega
\end{gathered}
$$

For the gain, we adopt a second-order model similar to (5.34).

$$
\begin{equation*}
A_{v}(s)=\frac{A_{v 0}}{\left(1+s / \omega_{\mathrm{p} 1}\right)\left(1+s / \omega_{e q}\right)} \tag{5.54}
\end{equation*}
$$

A dc gain of 80 dB implies $\mathrm{A}_{\mathrm{v} 0}=10^{4}$. Since the unity-gain frequency, $\omega_{\mathrm{ta}}$, satisfies $\omega_{\mathrm{p} 1}$ 《 $\omega_{\mathrm{ta}}$ « $\omega_{\mathrm{p} 2}$, the dominant pole frequency is

$$
\begin{equation*}
\omega_{\mathrm{p} 1}=\frac{\omega_{\mathrm{ta}}}{\mathrm{~A}_{\mathrm{v} 0}}=2 \pi \frac{10^{8}}{10^{4}}=2 \pi \cdot\left(10^{4} \mathrm{~Hz}\right) \tag{5.55}
\end{equation*}
$$

To find the non-dominant pole frequency, we assume the dominant pole contributes $-90^{\circ}$ phase shift at $\omega_{\mathrm{ta}}$, and hence,

$$
\begin{equation*}
\tan ^{-1}\left(\frac{\omega_{\mathrm{ta}}}{\omega_{\mathrm{eq}}}\right)=15^{\circ} \Rightarrow \frac{\omega_{\mathrm{ta}}}{\omega_{\mathrm{eq}}}=0.270 \Rightarrow \omega_{\mathrm{eq}}=\frac{\omega_{\mathrm{ta}}}{0.270}=2 \pi \cdot\left(3.70 \cdot 10^{8} \mathrm{~Hz}\right) \tag{5.56}
\end{equation*}
$$

It is well known that the gain of the noninverting amplifier under ideal conditions of infinite opamp gain is

$$
\begin{align*}
& \frac{1}{\beta}=\frac{Z_{1}+Z_{2}}{Z_{1}}  \tag{5.57}\\
& \Rightarrow \beta=\frac{Z_{1}}{Z_{1}+Z_{2}}
\end{align*}
$$

In order to determine the loop gain, we must analyze the circuit in Fig. 5.17. The loop is broken at the output of the controlled-source $A_{v}$, which models the opamp voltage gain. Since the termination impedance, $Z_{t}$, is inserted across an ideal voltage source, its value will have no effect on the analysis. The redrawn schematic at the bottom of Fig. 5.17 clearly shows

$$
\begin{gather*}
v_{r}=A_{v}(s) v_{i}=-A_{v}(s) \frac{Z_{i}}{Z_{o}}\left[\frac{Z_{L}| | Z_{o}}{Z_{L}| | Z_{o}+Z_{2}+Z_{1}| |\left(Z_{s}+Z_{i}\right)}\right]\left[\frac{Z_{1}}{Z_{s}+Z_{i}+Z_{1}}\right] v_{t} \\
L(s)=A_{v}(s) \frac{Z_{i}}{Z_{o}}\left[\frac{Z_{L}| | Z_{o}}{Z_{L}| | Z_{o}+Z_{2}+Z_{1}| |\left(Z_{s}+Z_{i}\right)}\right]\left[\frac{Z_{1}}{Z_{s}+Z_{i}+Z_{1}}\right] \tag{5.58}
\end{gather*}
$$

A bode plot of $\mathrm{L}(\mathrm{s})$ gives the phase margin. Substituting (5.57) and (5.58) into (5.51) and (5.52) will give the closedloop frequency response and gain error. If the simplifying assumptions $Z_{i} \gg Z_{1}, Z_{s}$ and $Z_{o}$ « $Z_{L}, Z_{2}$ are made (i.e., the opamp has relatively high input impedance and low output impedance) (5.58) reduces to a simple result.

$$
\begin{equation*}
\mathrm{L}(\mathrm{~s}) \approx \mathrm{A}_{\mathrm{v}}(\mathrm{~s}) \frac{\mathrm{Z}_{1}}{\mathrm{Z}_{1}+\mathrm{Z}_{2}}=\mathrm{A}_{\mathrm{v}}(\mathrm{~s}) \beta \tag{5.59}
\end{equation*}
$$

image_name:Fig. 5.17
description:
[
name: Zs, type: Resistor, value: Zs, ports: {N1: GND, N2: X}
name: Zi, type: Resistor, value: Zi, ports: {N1: X, N2: Y}
name: Z1, type: Resistor, value: Z1, ports: {N1: Y, N2: GND}
name: Z2, type: Resistor, value: Z2, ports: {N1: Y, N2: Vout}
name: Zt, type: Resistor, value: Zt, ports: {N1: Vr(Av(s)*Vi), N2: GND}
name: Zo, type: Resistor, value: Zo, ports: {N1: Vt, N2: Vout}
name: ZL, type: Resistor, value: ZL, ports: {N1: Vout, N2: GND}
name: Av(s)*Vi, type: VoltageControlledVoltageSource, ports: {Np: Vr, Nn: GND}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: Vt, Nn: GND}
]
extrainfo:The circuit diagram represents equivalent circuits for finding the loop gain, L(s), of a voltage feedback amplifier. It includes various resistive components and voltage sources to model the feedback and input/output impedances.

Fig. 5.17 Equivalent circuits for finding the loop gain, $L(s)$, of a voltage feedback amplifier.

#### EXAMPLE 5.11

The opamp from Example 5.10 is to be used to drive a load of $Z_{L}=200 \Omega$ in a unity-gain configuration, as shown in Fig. 5.18. Find the dc gain error, phase margin, and bandwidth.

#### Solution

A unity-gain opamp configuration is a special case of the noninverting operational amplifier where $\mathbf{Z}_{1}=\infty$ and $Z_{2}=0$. Substituting these and $Z_{s}=0$ into (5.58), and assuming $Z_{L} \ll Z_{i}$,

$$
\begin{equation*}
L(s)=A_{v}(s)\left(\frac{Z_{L}}{Z_{L}+Z_{o}}\right) \tag{5.60}
\end{equation*}
$$

Since the desired gain is $1 / \beta=1$, the closed loop gain is

$$
\begin{equation*}
A_{C L}(s)=\frac{L(s)}{1+L(s)}=\frac{A_{v}(s) Z_{L}}{A_{v}(s) Z_{L}+Z_{L}+Z_{0}} \tag{5.61}
\end{equation*}
$$

A numerical result for the gain error is obtained using the parameter values for the opamp at dc,

$$
\begin{equation*}
1-\frac{\mathrm{L}_{0}}{1+\mathrm{L}_{0}}=1-\frac{\mathrm{A}_{\mathrm{v} 0} \mathrm{Z}_{\mathrm{L}}}{\mathrm{~A}_{\mathrm{v} 0} \mathrm{Z}_{\mathrm{L}}+\mathrm{Z}_{\mathrm{L}}+\mathrm{Z}_{\mathrm{o}}}=1-\frac{10^{4} 200}{10^{4} 200+200+500}=0.0003 \tag{5.62}
\end{equation*}
$$

indicating a gain error of 0.03\%.
Substituting (5.54) into equation (5.60) gives the loop gain,

$$
\begin{equation*}
L(s)=\frac{A_{v 0}}{\left(1+\frac{s}{\omega_{\mathrm{p} 1}}\right)\left(1+\frac{s}{\omega_{\mathrm{eq}}}\right)}\left(\frac{Z_{\mathrm{L}}}{Z_{\mathrm{L}}+Z_{\mathrm{o}}}\right) \tag{5.63}
\end{equation*}
$$

A bode plot of (5.63) indicates a phase margin of $85.6^{\circ}$.
Finally, the bandwidth may be found by solving for the -3 dB frequency of (5.61). To simplify the analysis, notice that the phase margin is close to $90^{\circ}$ so the equivalent second pole $\omega_{\text {eq }}$ is playing only a small role at frequencies around the closed-loop bandwidth. Hence, a first-order approximation may be used for the opamp, $\mathrm{A}_{\mathrm{v}}(\mathrm{s}) \cong \omega_{\mathrm{ta}} / \mathrm{s}$. Substituting this into (5.61) results in

$$
\begin{equation*}
\mathrm{A}_{\mathrm{CL}}(\mathrm{~s}) \cong \frac{1}{1+\left(\frac{Z_{\mathrm{L}}+Z_{\mathrm{o}}}{\mathrm{Z}_{\mathrm{L}}}\right) \frac{\mathrm{s}}{\omega_{\mathrm{ta}}}} \tag{5.64}
\end{equation*}
$$

from which it straightforwardly follows that the $3-\mathrm{dB}$ bandwidth is approximately $\left(\omega_{t a} Z_{L}\right) /\left(Z_{L}+Z_{o}\right)$ which in this case equals $2 \pi \cdot 2.86 \mathrm{MHz}$.
image_name:Fig. 5.18 Unity-gain opamp configuration
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: Vs, InN: Vout, OutP: Vout}
name: ZL, type: Resistor, value: ZL, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a unity-gain opamp configuration with a feedback loop. The opamp is connected in a voltage follower configuration, where the output is directly connected to the inverting input, ensuring unity gain. The load resistor ZL is connected to the output and ground.

Fig. 5.18 Unity-gain opamp configuration.

In Example 5.11, an amplifier with an output impedance of $500 \Omega$ is used to drive a load of only $200 \Omega$, which one might think would cause a reduction in the amplifier's gain. However, a result very close to the desired gain of unity is obtained. The voltage division between the opamp's output impedance and load, $Z_{L} /\left(Z_{L}+Z_{0}\right)$, does indeed show up as a term in (5.60) that reduces the open-loop gain, $L$. But, so long as the opamp has large voltage gain, $A_{v}$, the open-loop gain $L$ remains much larger than unity and the circuit continues to work as an ideal voltage buffer with a closed-loop gain $\mathrm{A}_{\mathrm{CL}} \cong 1$.

#### EXAMPLE 5.12

What is the output impedance of the closed-loop amplifier in Example 5.11?

#### Solution

If the load of the closed-loop amplifier, $Z_{\mathrm{L}}$, were equal to its output impedance, $Z_{\text {out }}$ in Fig. 5.18, the closed-loop amplifier gain would be exactly one-half the value obtained with $Z_{L}=\infty$. In this case, the closed-loop gain with $Z_{L}=\infty$ is almost precisely unity. Hence, we can substitute $Z_{L}=Z_{\text {out }}$ and $A_{C L}=1 / 2$ into (5.61) and solve for $\mathrm{Z}_{\text {out }}$.

$$
\frac{1}{2}=\frac{A_{v} Z_{\text {out }}}{A_{v} Z_{\text {out }}+Z_{\text {out }}+Z_{o}} \Rightarrow Z_{\text {out }}=Z_{o} \cdot \frac{1}{A_{v}-1}
$$

Substituting in dc values from Example 5.10, $Z_{o}=500 \Omega$ and $A_{v}=A_{v 0}=10^{4}$, gives a dc closed-loop output impedance of

$$
\mathrm{Z}_{\text {out }}=\frac{(500 \Omega)}{\left(10^{4}-1\right)} \cong 0.05 \Omega
$$

#### Key Point: Another

important feature of feedback for CMOS integrated circuits is that it reduces the output-impedance of an amplifier by a factor approximately equal to the loop gain. tive opamp terminal. This has the effect of increasing the amplifier's input impedance; the feedback ensures the opamp input terminals are exposed to only very small differential voltages, $\mathrm{v}_{\mathrm{i}}$, so clearly very little input current is required. However, this is not a particularly exciting property since MOSFET gates provide relatively high input impedance even without feedback. However, we shall see in the next section that current feedback can be used to realize very low input impedances, which can be very useful when designing a CMOS circuit to amplify current signals.
6. For example, a common-source amplifier has an output impedance that depends on its small-signal $r_{d s}$ in active mode, which is in turn inversely proportional to its drain current. Hence, to decrease the output impedance, the drain current must increase.

In general, feedback in integrated circuits provides an effective reduction in the output impedance of an amplifier. Specifically, the output impedance of the amplifier, including the loading of the feedback network, is reduced by a factor approximately equal to the loop gain, L. This is an important feature of feedback, particularly in CMOS integrated circuits where low output impedance would otherwise require high power dissipation. ${ }^{6}$

Noninverting amplifiers are said to employ voltage feedback because the signal being subtracted from the source is a voltage-in this case, the voltage at the nega-

### 5.4.3 Transimpedance (Inverting) Amplifiers

The inverting opamp configuration shown in Fig. 5.10 may actually be thought of as a transimpedance amplifier. It is redrawn in Fig. 5.19 with a Norton-equivalent source. Transimpedance amplifiers employ current feedback: the branch current through $Z_{f}$ is subtracted from current coming from the source. We shall see that this results in a low input impedance, $Z_{i}$, which is useful when the input is a current. Hence, transimpedance amplifiers are useful when there is a high source impedance, $Z_{s}$. For example, they are used as amplifiers following sensors such as microphones and photodetectors.

The desired gain of the transimpedance amplifier, $1 / \beta$, is the gain $v_{\text {out }} / \mathrm{i}_{\mathrm{s}}$ obtained under conditions of very high loop gain. Consider the case where the voltage gain of the amplifier, $A_{v}=v_{\text {out }} / v_{i}$, is very large as shown in Fig. 5.20. Assuming the loop is stable $v_{\text {out }}$ remains finite, so $v_{i} \cong 0$. It follows that all of the current $i_{s}$ must flow through $Z_{f}$ and the output voltage is $v_{\text {out }} \cong-Z_{i} i_{s}$. Hence, the desired gain for the transimpedance amplifier is

$$
\begin{equation*}
\frac{1}{\beta}=-Z_{f} \tag{5.65}
\end{equation*}
$$

Notice that the circuit has a current input and voltage output, so its gain is expressed in ohms.
The loop gain is obtained, as usual, by breaking the loop and injecting a test source. Note that once the source $\mathrm{i}_{\mathrm{s}}$ is zeroed, the transimpedance amplifier in Fig. 5.19 is topologically identical to the noninverting feedback amplifier with sources zeroed in Fig. 5.17. Hence, the loop gain is the found by making the following substitutions into (5.58):

- replace $Z_{1}$ with $Z_{f}$
- replace $Z_{2}$ with $Z_{s}$
- replace $Z_{s}$ with 0
image_name:Fig. 5.19 A generalized transimpedance amplifier.
description:
[
name: Is, type: CurrentSource, ports: {Np: -Vi, Nn: GND}
name: Zs, type: Resistor, value: Zs, ports: {N1: -Vi, N2: GND}
name: Zf, type: Resistor, value: Zf, ports: {N1: OutP, N2: -Vi}
name: ZL, type: Resistor, value: ZL, ports: {N1: Vout, N2: GND}
name: OpAmp, type: OpAmp, ports: {InP: GND, InN: Vi, OutP: Vout}
]
extrainfo:The circuit is a generalized transimpedance amplifier with a feedback resistor Zf. It converts the input current Is into an output voltage Vout. The op-amp has a high gain, and the loop gain is significant.

Fig. 5.20 A generalized transimpedance amplifier.
image_name:Fig. 5.20 A transimpedance amplifier with a very high voltage-gain amplifier
description:
[
name: Is, type: CurrentSource, value: Is, ports: {Np: -Vi, Nn: GND}
name: Zs, type: Resistor, value: Zs, ports: {N1: -Vi, N2: GND}
name: Zf, type: Resistor, value: Zf, ports: {N1: OutP, N2: -Vi}
name: ZL, type: Resistor, value: ZL, ports: {N1: Vout, N2: GND}
name: OpAmp, type: OpAmp, ports: {InP: GND, InN: -Vi, OutP: Vout}
]
extrainfo:The circuit is a generalized transimpedance amplifier with a feedback resistor Zf. It converts the input current Is into an output voltage Vout. The op-amp has a high gain, and the loop gain is significant.

Fig. 5.20 A transimpedance amplifier with a very high voltage-gain amplifier, $A_{v} \rightarrow \infty$ and hence very high loop gain, L.

The results are summarized below where, as before, $Z_{i}$ and $Z_{o}$ are the input and output impedances of the opamp respectively.

$$
\begin{equation*}
L(s)=A_{v}(s) \frac{Z_{i}}{Z_{o}}\left[\frac{Z_{L}| | Z_{o}}{Z_{L}| | Z_{o}+Z_{f}+Z_{s}| | Z_{i}}\right]\left[\frac{Z_{s}}{Z_{i}+Z_{s}}\right] \tag{5.66}
\end{equation*}
$$

If it is assumed that $Z_{i} \gg Z_{s}$ and $Z_{o}$ 《 $Z_{L}, Z_{f}$, then (5.66) simplifies considerably.

$$
\begin{equation*}
L(s) \approx A_{v}(s) \frac{Z_{s}}{Z_{f}+Z_{s}} \tag{5.67}
\end{equation*}
$$

Notice that (5.67) is identical to (5.59) for the noninverting amplifier with $Z_{s}=Z_{1}$ and $Z_{f}=Z_{2}$. This is satisfying since the undriven circuits look nearly identical for the noninverting and transimpedance feedback amplifiers (with the exception of an additional impedance at the positive amplifier terminal in the noninverting schematics of Fig. 5.15, Fig. 5.16, and Fig. 5.17).

#### EXAMPLE 5.13

In the inverting feedback amplifier of Fig. 5.9, adopt a first-order model for the opamp, as in Fig. 5.21 where the input has been zeroed. Show that the system is 1 st order and find the closed-loop pole.

#### Solution

The open-loop gain of the circuit in Fig. 5.21 may be obtained by breaking the loop at the opamp input terminals and injecting a test signal.

$$
\begin{aligned}
v_{r} & =-g_{m} v_{t}\left[R_{0} \|\left(\frac{1}{s C_{1}}+\frac{1}{s C_{2}}\right)\right] \cdot \frac{C_{2}}{C_{1}+C_{2}} \\
& \Rightarrow L(s)=-\frac{v_{r}}{v_{t}}=\frac{g_{m} R_{0} C_{2}}{C_{1}+C_{2}+s C_{1} C_{2} R_{0}}
\end{aligned}
$$

The poles of the closed-loop amplifier are given by the solutions of $1+\mathrm{L}(\mathrm{s})=0$.

$$
\begin{align*}
& 1+\frac{g_{m} R_{0} C_{2}}{C_{1}+C_{2}+s C_{1} C_{2} R_{0}}=0 \\
& \Rightarrow s=-\frac{\left(g_{m} R_{0} C_{2}+C_{1}+C_{2}\right)}{C_{1} C_{2} R_{0}} \tag{5.68}
\end{align*}
$$

Fig. 5.21 Noninverting capacitive feedback amplifier with simple opamp model and zero input.
image_name:Fig. 5.21 Noninverting capacitive feedback amplifier with simple opamp model and zero input
description:This is a noninverting capacitive feedback amplifier with a simple opamp model. The circuit has a stable pole on the negative real axis. The system is first-order, and the pole frequency is approximately gm/C1 when gm*R0 >> 1 and C2 >> C1.

Hence, it is a first-order system with the stable pole on the negative real axis at $-\left(g_{m} R_{0} C_{2}+C_{1}+C_{2}\right) /\left(C_{1} C_{2} R_{0}\right)$. If one assumes $g_{m} R_{0}$ » 1 and $C_{2}$ » $C_{1}$, we have a pole frequency of $g_{m} / C_{1}$.

Note the circuit poles can also be found by performing a direct nodal analysis of Fig. 5.21 with the loop closed (i.e., $\mathrm{V}_{\mathrm{r}}=\mathrm{v}_{\mathrm{t}}$ ) and solving the resulting system of equations for s . The node equation at the negative opamp input terminal is

$$
\begin{equation*}
-\mathrm{sC}_{1} \mathrm{v}_{\mathrm{t}}-\mathrm{sC}_{2}\left(\mathrm{v}_{\mathrm{t}}+\mathrm{v}_{\mathrm{y}}\right)=0 \Rightarrow \mathrm{v}_{\mathrm{t}}=-\frac{\mathrm{C}_{2}}{\mathrm{C}_{1}+\mathrm{C}_{2}} \mathrm{v}_{\mathrm{y}} \tag{5.69}
\end{equation*}
$$

The node equation at $v_{y}$ is

$$
\begin{equation*}
s C_{2}\left(v_{y}+v_{t}\right)-g_{m} v_{t}+\frac{v_{y}}{R_{o}}=0 \tag{5.70}
\end{equation*}
$$

Substituting (5.69) into (5.70) and rearranging gives the same unique pole as in (5.68).

#### EXAMPLE 5.14

In Fig. 5.22 a transimpedance amplifier is realized by replacing the opamp of Fig. 5.19 with a cascade of three common-source amplifiers. Find the loop gain, closed-loop gain, and input resistance, all at dc.

#### Solution

Assuming the transistors are in saturation, the small-signal equivalent circuit is shown in Fig. 5.23(a). Breaking the loop immediately after the current source, $\mathrm{g}_{\mathrm{m}} \mathrm{v}_{\mathrm{gs}}$, makes the analysis insensitive to the choice of the termination impedance, $Z_{t}$. Setting $i_{s}=0$, introducing the test source $i_{t}$, and rearranging the schematic results in Fig. 5.23(b) from which the loop gain is derived.

$$
L(0)=-\frac{i_{r}}{i_{t}}=g_{m, 1} r_{d s, 1} g_{m, 2} r_{d s, 2} g_{m, 3}\left(\frac{r_{d s, 3}}{r_{d s, 3}+R_{f}+R_{s}}\right) R_{s}
$$

The desired gain is given by (5.65). In this case

$$
1 / \beta=-R_{f}
$$

image_name:Fig. 5.22
description:
[
name: is, type: CurrentSource, ports: {Np: P, Nn: GND}
name: Rs, type: Resistor, value: Rs, ports: {N1: P, N2: GND}
name: Rf, type: Resistor, value: Rf, ports: {N1: P, N2: Vout}
name: Q1, type: PMOS, ports: {S: GND, D: d1g2, G: P}
name: Q2, type: PMOS, ports: {S: GND, D: d2g3, G: d1g2}
name: Q3, type: PMOS, ports: {S: GND, D: Vout, G: d2g3}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a transimpedance amplifier using three PMOS common-source stages with feedback resistor Rf. Current sources labeled as LOAD1, LOAD2, and LOAD3 provide biasing currents Ibias_1, Ibias_2, and Ibias_3 to the PMOS transistors, respectively. The input current is is, and the output voltage is taken across CL.

Fig. 5.22 A transimpedance amplifier based on NMOS common-source stages.

Hence, the dc closed-loop gain is

$$
\begin{equation*}
A_{C L}(0)=\frac{1}{\beta} \cdot \frac{L(0)}{1+L(0)}=-R_{f} \cdot\left(\frac{g_{m, 1} r_{d s, 1} g_{m, 2} r_{d s, 2} g_{m, 3} r_{d s, 3} R_{s}}{g_{m, 1} r_{d s, 1} g_{m, 2} r_{d s, 2} g_{m, 3} r_{d s, 3} R_{s}+r_{d s, 3}+R_{f}+R_{s}}\right) \tag{5.71}
\end{equation*}
$$

which very closely approaches the desired $-R_{f}$ so long as each transistor's intrinsic gain $g_{m} r_{d s}$ is significant and $R_{s}$ is not too small.

The input resistance is given by the value of $R_{s}$ for which $A_{C L}(0)=-R_{f} / 2$. Assuming $g_{m, 1} r_{d s, 1} g_{m, 2} r_{d s, 2} g_{m, 3} r_{d s, 3}$ " 1 in (5.71), the result is

$$
\begin{equation*}
R_{i n} \cong \frac{r_{d s, 3}+R_{f}}{g_{m, 1} r_{d s, 1} g_{m, 2} r_{d s, 2} g_{m, 3} r_{d s, 3}} \tag{5.72}
\end{equation*}
$$

For example, if $R_{f}=250 \Omega \ll r_{d s, 3}$ and $g_{m} r_{d s}=10$, then $R_{i n} \cong 0.25 \Omega$. Finally, note that the circuit is a third-order feedback system so there must be a dominant pole to ensure stability with phase margin, likely at the output node.

The input resistance of the transimpedance amplifier can be very small, even if the value of the feedback impedance, $Z_{\mathrm{f}}$, is large to provide high transimpedance gain. This is because the output of the amplifier draws additional current from the input through $\mathbf{Z}_{\mathrm{f}}$. In general, increasing the loop gain reduces the input impedance proportionately.

Key Point: If current feedback is used, the input-impedance of the closed-loop amplifier is reduced compared to that of the amplifier without feedback by a factor approximately equal to the loop gain.

A low input impedance is desirable when the amplifier is driven by a current signal source. But, since any linear source may be modeled by its Thevenin/Norton equivalents, what distinguishes a voltage signal source from a current signal source? In order to observe a current signal, one wishes to have an input impedance lower than the source impedance. Hence, when the source impedance is high it is sensible to consider the input a current signal, and a low input impedance ensures little of the available source current, $\mathrm{i}_{\mathrm{s}}$, is lost in $\mathrm{Z}_{\mathrm{s}}$. However, when the source impedance is low, it is easier to consider the input a voltage signal and provide a higher input impedance.
image_name:(a)
description:The circuit diagram (a) represents a small-signal model of a transimpedance amplifier. It includes multiple voltage-controlled current sources and resistors connected to a common node P, with feedback resistor Rf connecting node P to Vout. The loop is broken at Vout for analysis of loop gain.
image_name:(b)
description:This is a small-signal model of a transimpedance amplifier with feedback. The circuit is designed to convert input current to output voltage. The loop is broken at the output to determine the loop gain.

Fig. 5.23 (a) Small-signal model of the transimpedance amplifier of Fig. 5.22. (b) Loop broken and test signal introduced to determine the loop gain, L(s).

## 5.5 SUMMARY OF KEY POINTS

- When $L \gg 1$, the closed-loop system has an overall gain inversely proportional to the gain of the feedback circuit and highly insensitive to the gain of the amplifier, A. [p. 206]
- A rough estimate of the bandwidth of a feedback amplifier is given by the frequency where $\mathrm{IL}(\omega) \mid=1$, which is much higher than the bandwidth of $A(\omega)$. [p. 207]
- With feedback, an amplifier is exposed to signals that are approximately L times smaller than would be the case without feedback, making it much more linear. [p. 207]
- The stability of a feedback amplifier may be checked by looking at a Bode plot of the loop gain, $L(\omega)$; so long at the phase response is greater than -180 degres at the unity gain frequency, the feedback system is stable. [p. 210]
- It is not enough that an amplifier simply be reliably stable-it must also reliably have large phase margin. To avoid undesirable behavior in the frequency and step responses of the closed-loop amplifier, it is common to require phase margins of 45 to 90 degrees. [p. 212]
- A first-order feedback amplifier is unconditionally stable with approximately 90 degrees phase margin. [p. 214]
- The closed-loop bandwidth of a feedback amplifier is $\omega_{\mathrm{t}}$, independent of the amplifier's 3-dB bandwidth, $\omega_{\mathrm{p} 1}$. The settling time is $1 / \omega_{\mathrm{t}}$. [p. 216]
- All-pole second-order feedback systems are unconditionally stable with a phase margin of between 90 and 0 degrees. [p. 217]
- The process of designing or modifying a feedback amplifier to have some targeted phase margin is called compensation. [p. 218]
- Higher-order feedback amplifiers may be modeled using a second-order transfer function so long at they are not approaching instability. The second pole is chosen as the frequency at which a phase response of -135 degrees is attained. [p. 220]
- Feedback systems may be analyzed in terms of their desired gain, $\beta$, and loop gain, $L(\omega)$, from which the closed-loop amplifier's gain, bandwidth, phase margin, and frequency response may all be inferred. [p. 221]
- The loop gain, $L(\omega)$, may be estimated by zeroing the input, breaking the loop, and injecting a test signal. This is an accurate approximation in the typical case where high forward gain around the loop is being traded for increased bandwidth, accuracy, etc. [p. 223]
- Another important feature of feedback for CMOS integrated circuits is that it reduces the output-impedance of an amplifier by a factor approximately equal to the loop gain. [p. 230]
- If current feedback is used, the input-impedance of the closed-loop amplifier is reduced compared to that of the amplifier without feedback by a factor approximately equal to the loop gain. [p. 234]
