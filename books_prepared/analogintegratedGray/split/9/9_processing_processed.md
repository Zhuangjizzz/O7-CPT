# 9. Frequency Response and Stability of Feedback Amplifiers

## 9.1 Introduction

In Chapter 8, we considered the effects of negative feedback on circuit parameters such as gain and terminal impedance. We saw that application of negative feedback resulted in a number of performance improvements, such as reduced sensitivity of gain to active-device parameter changes and reduction of distortion due to circuit nonlinearities.

In this chapter, we see the effect of negative feedback on the frequency response of a circuit. The possibility of oscillation in feedback circuits is illustrated, and methods of overcoming these problems by compensation of the circuit are described. Finally, the effect of compensation on the large-signal high-frequency performance of feedback amplifiers is investigated.

Much of the analysis in this chapter is based on the ideal block diagram in Fig. 9.1. This block diagram includes the forward gain $a$ and feedback factor $f$, which are the parameters used in two-port analysis of feedback circuits in Chapter 8. The equations and results in this chapter could be expressed in terms of the parameters used in the return-ratio analysis in Chapter 8 by an appropriate change of variables, as shown in Appendix A9.1.

The equations and relationships in this chapter are general and can be applied to any feedback circuit. However, for simplicity we will often assume the feedback factor $f$ is a positive, unitless constant. One circuit that has such an $f$ is the series-shunt feedback circuit shown in Fig 8.24. In this circuit, the feedback network is a resistive voltage divider, so $f$ is a constant with $0 \leq f \leq 1$. The forward gain $a$ is a voltage gain that is positive at low frequencies. This circuit gives a noninverting closed-loop voltage gain.

## 9.2 Relation Between Gain and Bandwidth in Feedback Amplifiers

Chapter 8 showed that the performance improvements produced by negative feedback were obtained at the expense of a reduction in gain by a factor $(1+T)$, where $T$ is the loop gain. The performance specifications that were improved were also changed by the factor $(1+T)$.

In addition to the foregoing effects, negative feedback also tends to broadband the amplifier. Consider first a feedback circuit as shown in Fig. 9.1 with a simple basic amplifier whose gain function contains a single pole

$$
\begin{equation*}
a(s)=\frac{a_{0}}{1-\frac{s}{p_{1}}} \tag{9.1}
\end{equation*}
$$

image_name:Figure 9.1 Feedback circuit configuration
description:
[
name: a(s), type: OpAmp, value: a(s), ports: {InP: v_ϵ, InN: GND, Out: v_o}
name: f, type: Other, ports: {N1: v_o, N2: v_fb}
]
extrainfo:The circuit diagram is a feedback configuration with an operational amplifier labeled 'a(s)' and a feedback element 'f'. The input voltage 'v_i' is compared with the feedback voltage 'v_fb' to produce the error voltage 'v_ϵ', which is then amplified to produce the output voltage 'v_o'.

Figure 9.1 Feedback circuit configuration.
where $a_{0}$ is the low-frequency gain of the basic amplifier and $p_{1}$ is the basic-amplifier pole in radians per second. Assume that the feedback path is purely resistive and thus the feedback function $f$ is a positive constant. Since Fig. 9.1 is an ideal feedback arrangement, the overall gain is

$$
\begin{equation*}
A(s)=\frac{v_{o}}{v_{i}}=\frac{a(s)}{1+a(s) f} \tag{9.2}
\end{equation*}
$$

where the loop gain is $T(s)=a(s) f$. Substitution of (9.1) in (9.2) gives

$$
\begin{equation*}
A(s)=\frac{\frac{a_{0}}{1-\frac{s}{p_{1}}}}{1+\frac{a_{0} f}{1-\frac{s}{p_{1}}}}=\frac{a_{0}}{1-\frac{s}{p_{1}}+a_{0} f}=\frac{a_{0}}{1+a_{0} f} \frac{1}{1-\frac{s}{p_{1}} \frac{1}{1+a_{0} f}} \tag{9.3}
\end{equation*}
$$

From (9.3) the low-frequency gain $A_{0}$ is

$$
\begin{equation*}
A_{0}=\frac{a_{0}}{1+T_{0}} \tag{9.4}
\end{equation*}
$$

where

$$
\begin{equation*}
T_{0}=a_{0} f=\text { low-frequency loop gain } \tag{9.5}
\end{equation*}
$$

The $-3-\mathrm{dB}$ bandwidth of the feedback circuit (i.e., the new pole magnitude) is $\left(1+a_{o} f\right) \cdot\left|p_{1}\right|$ from (9.3). Thus the feedback has reduced the low-frequency gain by a factor $\left(1+T_{0}\right)$, which is consistent with the results of Chapter 8 , but it is now apparent that the $-3-\mathrm{dB}$ frequency of the circuit has been increased by the same quantity $\left(1+T_{0}\right)$. Note that the gain-bandwidth product is constant. These results are illustrated in the Bode plots of Fig. 9.2, where the magnitudes of
image_name:Figure 9.2
description:**Figure 9.2 Description:**

1. **Type of Graph and Function:**
- The graph is a Bode plot representing gain magnitude versus frequency for a basic amplifier and a feedback amplifier.

2. **Axes Labels and Units:**
- The vertical axis represents "Gain magnitude" in decibels (dB).
- The horizontal axis represents frequency on a logarithmic scale, denoted as \( \omega \) log scale.

3. **Overall Behavior and Trends:**
- The plot shows two curves: one for the basic amplifier and another for the feedback amplifier.
- The basic amplifier curve starts at a high gain level of \( 20 \log_{10} a_0 \) and decreases at a rate of \(-6 \text{ dB/octave}\) after the cutoff frequency \(|p_1|\).
- The feedback amplifier curve starts at a lower gain level of \( \frac{a_0}{1+T_0} \) and follows a similar decreasing trend.

4. **Key Features and Technical Details:**
- The cutoff frequency for the basic amplifier is marked at \(|p_1|\).
- For the feedback amplifier, the cutoff frequency is shifted to \((1+T_0)|p_1|\), indicating an increase in bandwidth.
- Both curves show a consistent slope of \(-6 \text{ dB/octave}\) beyond their respective cutoff frequencies.
- The gain-bandwidth product remains constant, as indicated by the parallel nature of the curves.

5. **Annotations and Specific Data Points:**
- The plot includes annotations at key points, such as \(20 \log_{10} a_0\), \(20 \log_{10} |a(j\omega)|\), and \(20 \log_{10} |A(j\omega)|\).
- The gain for the feedback amplifier is reduced by a factor of \((1+T_0)\), as shown by the horizontal shift of the curve.

Figure 9.2 Gain magnitude versus frequency for the basic amplifier and the feedback amplifier.
image_name:Figure 9.3
description:The graph in Figure 9.3 is a pole-zero plot on the complex plane, also known as the s-plane. This type of graph is used to illustrate the position of poles and zeros of a transfer function as parameters change, in this case, the loop gain $T_{0}$.

1. **Axes Labels and Units:**
- The horizontal axis is labeled \(\sigma\), representing the real part of the complex frequency.
- The vertical axis is labeled \(j\omega\), representing the imaginary part of the complex frequency.
- The axes are on a linear scale, typical for s-plane diagrams.

2. **Overall Behavior and Trends:**
- The plot shows the movement of a pole in response to changes in the loop gain $T_{0}$.
- Initially, when $T_{0} = 0$, the pole is located at \(p_1\) on the real axis.
- As $T_{0}$ increases, the pole moves leftward on the real axis to a new position \((1 + T_{0}) p_1\), indicating a shift in the pole's location due to feedback.

3. **Key Features and Technical Details:**
- The point \(p_1\) is marked with an 'X', indicating its position when $T_{0} = 0$.
- The new pole position for finite $T_{0}$ is marked with a square, showing the effect of feedback on pole location.
- The movement of the pole from \(p_1\) to \((1 + T_{0}) p_1\) is depicted with an arrow, indicating the direction of change.

4. **Annotations and Specific Data Points:**
- The diagram includes annotations indicating the pole position for finite $T_{0}$ and the initial position at $T_{0} = 0$.
- The arrow and annotations help visualize the effect of changing loop gain on the stability and dynamics of the system.

This plot is crucial for understanding how feedback affects system stability by altering pole positions, thus allowing designers to manipulate gain and bandwidth effectively.

Figure 9.3 Locus of the pole of the circuit of Fig. 9.1 as loop gain $T_{0}$ varies.
$a(j \omega)$ and $A(j \omega)$ are plotted versus frequency on log scales. It is apparent that the gain curves for any value of $T_{0}$ are contained in an envelope bounded by the curve of $|a(j \omega)|$.

Because the use of negative feedback allows the designer to trade gain for bandwidth, negative feedback is widely used as a method for designing broadband amplifiers. The gain reduction that occurs is made up by using additional gain stages, which in general are also feedback amplifiers.

Let us now examine the effect of the feedback on the pole of the overall transfer function $A(s)$. It is apparent from (9.3) that as the low-frequency loop gain $T_{0}$ is increased, the magnitude of the pole of $A(s)$ increases. This is illustrated in Fig. 9.3, which shows the locus of the pole of $A(s)$ in the $s$ plane as $T_{0}$ varies. The pole starts at $p_{1}$ for $T_{0}=0$ and moves out along the negative real axis as $T_{0}$ is made positive. Figure 9.3 is a simple root-locus diagram and will be discussed further in Section 9.5.

## 9.3 Instability and the Nyquist Criterion ${ }^{1}$

In the above simple example the basic amplifier was assumed to have a single-pole transfer function, and this situation is closely approximated in practice by internally compensated general-purpose op amps. However, many amplifiers have multipole transfer functions that cause deviations from the above results. The process of compensation overcomes these problems, as will be seen later.

Consider an amplifier with a three-pole transfer function

$$
\begin{equation*}
a(s)=\frac{a_{0}}{\left(1-\frac{s}{p_{1}}\right)\left(1-\frac{s}{p_{2}}\right)\left(1-\frac{s}{p_{3}}\right)} \tag{9.6}
\end{equation*}
$$

where $\left|p_{1}\right|,\left|p_{2}\right|$, and $\left|p_{3}\right|$ are the pole magnitudes in rad/s. The poles are shown in the $s$ plane in Fig. 9.4 and gain magnitude $|a(j \omega)|$ and phase $\mathrm{ph} a(j \omega)$ are plotted versus frequency in Fig. 9.5 assuming about a factor of 10 separation between the poles. Only asymptotes are
image_name:Figure 9.4 Poles of an amplifier in the s plane
description:The graph in Figure 9.4 is a pole-zero plot in the complex $s$ plane, which is commonly used in control systems and signal processing to represent the poles and zeros of a transfer function.

1. **Type of Graph and Function:**
- This is a pole plot in the $s$ plane, specifically showing the poles of an amplifier's transfer function.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as $\sigma$, representing the real part of the complex frequency.
- The vertical axis is labeled as $j\omega$, representing the imaginary part of the complex frequency.
- The axes are not scaled with specific units, but typically in such plots, the units would be in radians per second (rad/s).

3. **Overall Behavior and Trends:**
- The plot displays three poles, marked as $p_1$, $p_2$, and $p_3$. These are shown as 'X' marks along the real axis, indicating that they are real-valued poles.
- The poles are evenly spaced along the negative real axis, suggesting a sequential order of decreasing magnitude from $p_1$ to $p_3$.

4. **Key Features and Technical Details:**
- The poles are located on the negative real axis, which typically indicates a stable system since they are in the left half of the $s$ plane.
- The separation between the poles is approximately a factor of 10, which is a common design choice for ensuring adequate phase margin and stability.

5. **Annotations and Specific Data Points:**
- The poles are labeled directly on the plot as $p_1$, $p_2$, and $p_3$, but specific numerical values are not provided. The exact positions would determine the cutoff frequencies and stability characteristics of the system.

This plot provides a visual representation of the poles, which are crucial for understanding the frequency response and stability of the amplifier circuit described by the transfer function.

Figure 9.4 Poles of an amplifier in the $s$ plane.
image_name:(a)
description:The graph labeled as '(a)' is a Bode plot, which consists of two separate plots: a magnitude plot and a phase plot, both plotted against frequency on a logarithmic scale.

1. **Magnitude Plot (Top):**
- **Axes:**
- The vertical axis represents the magnitude of the transfer function in decibels (dB), denoted as \(|a(j\omega)|\) dB.
- The horizontal axis represents frequency \(\omega\) on a logarithmic scale.
- **Overall Behavior:**
- The magnitude plot starts at a value of \(20 \log_{10} a_0\) dB, indicating the initial gain level.
- The plot shows a decreasing trend with three distinct slopes at different frequency ranges, corresponding to the system's poles.
- **Key Features:**
- **First Pole (\(|p_1|\)):** Above this frequency, the slope is \(-6 \text{ dB/octave}\).
- **Second Pole (\(|p_2|\)):** Beyond this point, the slope increases to \(-12 \text{ dB/octave}\).
- **Third Pole (\(|p_3|\)):** The slope further steepens to \(-18 \text{ dB/octave}\).
- The plot includes markers for these pole frequencies, indicating the transition points where the slope changes.

2. **Phase Plot (Bottom):**
- **Axes:**
- The vertical axis represents the phase angle of the transfer function, denoted as \(\text{Ph } a(j\omega)\), in degrees.
- The horizontal axis is the same logarithmic frequency scale as the magnitude plot.
- **Overall Behavior:**
- The phase plot starts near 0 degrees and decreases as frequency increases.
- **Key Features:**
- The phase shift approaches \(-90^{\circ}\), \(-180^{\circ}\), and \(-270^{\circ}\) as the frequency crosses each respective pole \(|p_1|\), \(|p_2|\), and \(|p_3|\).
- The plot includes horizontal dashed lines at \(-45^{\circ}\), \(-90^{\circ}\), \(-135^{\circ}\), \(-180^{\circ}\), \(-225^{\circ}\), and \(-270^{\circ}\) to aid in visualizing the phase shifts.

This Bode plot provides a comprehensive view of the frequency response of a circuit with a three-pole transfer function, illustrating how both the gain and phase respond to changes in frequency.
image_name:(b)
description:The graph depicted in part (b) is a phase plot of a Bode plot, which is part of a frequency response analysis for a circuit with a three-pole transfer function. The plot is presented on a logarithmic scale for frequency, denoted as \( \omega \), on the horizontal axis, and the phase angle \( \text{Ph} \, a(j\omega) \) in degrees on the vertical axis.

Axes and Units:
- **Horizontal Axis:** Frequency \( \omega \) (logarithmic scale)
- **Vertical Axis:** Phase angle \( \text{Ph} \, a(j\omega) \) in degrees

Overall Behavior and Trends:
The phase plot shows a decreasing trend as frequency increases. Starting from 0 degrees at low frequencies, the phase angle decreases, reaching approximately -90 degrees after the first pole \( |p_1| \), -180 degrees after the second pole \( |p_2| \), and further decreasing towards -270 degrees after the third pole \( |p_3| \).

Key Features:
- **Phase Shift:**
- Begins at 0 degrees and decreases to -90 degrees after the first pole \( |p_1| \).
- Continues to -180 degrees after the second pole \( |p_2| \).
- Further decreases to -270 degrees after the third pole \( |p_3| \).
- **Annotations:**
- Vertical dashed lines mark the locations of the poles \( |p_1|, |p_2|, |p_3| \), indicating significant phase shifts at these frequencies.
- **Phase Margin:**
- The plot shows the phase reaching -180 degrees at the frequency \( \omega_{180} \), which is crucial for assessing stability.

This phase plot is essential for understanding how the phase of the amplifier circuit changes with frequency, providing insights into the stability and transient response of the system. The consistent decrease in phase at each pole reflects the cumulative effect of each pole on the system's phase response.

Figure 9.5 Gain and phase versus frequency for a circuit with a three-pole transfer function.
shown for the magnitude plot. At frequencies above the first pole magnitude $\left|p_{1}\right|$, the plot of $|a(j \omega)|$ falls at $6 \mathrm{~dB} /$ octave and $\mathrm{ph} a(j \omega)$ approaches $-90^{\circ}$. Above $\left|p_{2}\right|$ these become 12 $\mathrm{dB} /$ octave and $-180^{\circ}$, and above $\left|p_{3}\right|$ they become $18 \mathrm{~dB} /$ octave and $-270^{\circ}$. The frequency where $\mathrm{ph} a(j \omega)=-180^{\circ}$ has special significance and is marked $\omega_{180}$, and the value of $|a(j \omega)|$ at this frequency is $a_{180}$. If the three poles are fairly widely separated (by a factor of 10 or more), the phase shifts at frequencies $\left|p_{1}\right|,\left|p_{2}\right|$, and $\left|p_{3}\right|$ are approximately $-45^{\circ},-135^{\circ}$, and $-225^{\circ}$, respectively. This will now be assumed for simplicity. In addition, the gain magnitude will be assumed to follow the asymptotic curve and the effect of these assumptions in practical cases will be considered later.

Now consider this amplifier connected in a feedback loop as in Fig. 9.1 with $f$ a positive constant. Since $f$ is constant, the loop gain $T(j \omega)=a(j \omega) f$ will have the same variation with frequency as $a(j \omega)$. A plot of $a f(j \omega)=T(j \omega)$ in magnitude and phase on a polar plot (with $\omega$ as a parameter) can thus be drawn using the data of Fig. 9.5 and the magnitude of $f$. Such a plot for this example is shown in Fig. 9.6 (not to scale) and is called a Nyquist diagram. The variable on the curve is frequency and varies from $\omega=-\infty$ to $\omega=\infty$. For $\omega=0,|T(j \omega)|=T_{0}$ and ph $T(j \omega)=0$, and the curve meets the real axis with an intercept $T_{0}$. As $\omega$ increases, as Fig. 9.5 shows, $|a(j \omega)|$ decreases and ph $a(j \omega)$ becomes negative and thus the plot is in the fourth quadrant. As $\omega \rightarrow \infty$, ph $a(j \omega) \rightarrow-270^{\circ}$ and $|a(j \omega)| \rightarrow 0$. Consequently, the plot is asymptotic to the origin and is tangent to the imaginary axis. At the frequency $\omega_{180}$ the phase is $-180^{\circ}$ and the curve crosses the negative real axis. If $\left|a\left(j \omega_{180}\right) f\right|>1$ at this point, the Nyquist diagram will encircle the point $(-1,0)$ as shown, and this has particular significance, as will
image_name:Figure 9.6 Nyquist diagram
description:The graph in question is a Nyquist diagram, which is a polar plot representing the frequency response of a system. This particular diagram is labeled as Figure 9.6 and corresponds to the characteristic of another figure, 9.5.

1. **Type of Graph and Function:**
- This is a Nyquist diagram used to analyze the stability of a feedback amplifier by plotting the complex function $T(j\omega)$ where $\omega$ is the frequency.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as the real part (Re) and the vertical axis as the imaginary part (Im) of the complex function $T(j\omega)$. The units are not explicitly mentioned but are typically dimensionless in such plots.

3. **Overall Behavior and Trends:**
- The plot shows a loop-like trajectory that begins at the point corresponding to $\omega = 0$ on the positive real axis and extends into the complex plane.
- As $\omega$ increases positively, the curve moves counterclockwise, eventually encircling the point $(-1,0)$, which is crucial for stability analysis.
- For negative and increasing magnitudes of $\omega$, the curve continues the counterclockwise loop and approaches the origin asymptotically as $\omega \rightarrow \infty$.

4. **Key Features and Technical Details:**
- The curve crosses the negative real axis at a point labeled $\omega = \omega_{180}$, where the phase angle is $-180^\circ$.
- At this crossing, if $|a(j\omega_{180})f| > 1$, the Nyquist plot will encircle the point $(-1,0)$, indicating potential instability in the feedback amplifier.
- The diagram shows the curve being tangent to the imaginary axis as it approaches the origin.

5. **Annotations and Specific Data Points:**
- The diagram includes annotations such as $a_{180}f$ and $T_0$, which are specific points or parameters relevant to the system's feedback and stability analysis.
- The diagram also annotates the direction of increasing frequency with arrows, helping to understand the progression of the curve as frequency changes.

This Nyquist plot is used to apply the Nyquist criterion for determining the stability of the amplifier. If the plot encircles the point $(-1,0)$, it suggests that the feedback amplifier may be unstable, which is a critical aspect of control system design and analysis.

Figure 9.6 Nyquist diagram [polar plot of $T(j \omega)$ in magnitude and phase] corresponding to the characteristic of Fig. 9.5 (not to scale).
now become apparent. For the purposes of this treatment, the Nyquist criterion for stability of the amplifier can be stated as follows:
"Consider a feedback amplifier with a stable $T(s)$ (i.e., all poles of $T(s)$ are in the left half-plane). If the Nyquist plot of $T(j \omega)$ encircles the point $(-1,0)$, the feedback amplifier is unstable."

This criterion simply amounts to a mathematical test for poles of transfer function $A(s)$ in the right half-plane. If the Nyquist plot encircles the point $(-1,0)$, the amplifier has poles in the right half-plane and the circuit will oscillate. In fact the number of encirclements of the point $(-1,0)$ gives the number of right half-plane poles and in this example there are two. The significance of poles in the right half-plane can be seen by assuming that a circuit has a pair of complex poles at $\left(\sigma_{1} \pm j \omega_{1}\right)$ where $\sigma_{1}$ is positive. The transient response of the circuit then contains a term $K_{1} \exp \sigma_{1} t \sin \omega_{1} t$, which represents a growing sinusoid if $\sigma_{1}$ is positive. ( $K_{1}$ is a constant representing initial conditions.) This term is then present even if no further input is applied, and a circuit behaving in this way is said to be unstable or oscillatory.

The significance of the point $(-1,0)$ can be appreciated if the Nyquist diagram is assumed to pass through this point. Then at the frequency $\omega_{180}, T(j \omega)=a(j \omega) f=-1$ and $A(j \omega)=\infty$ using (9.2) in the frequency domain. The feedback amplifier is thus calculated to have a forward gain of infinity, and this indicates the onset of instability and oscillation. This situation corresponds to poles of $A(s)$ on the $j \omega$ axis in the $s$ plane. If $T_{0}$ is then increased by increasing $a_{0}$ or $f$, the Nyquist diagram expands linearly and then encircles $(-1,0)$. This corresponds to poles of $A(s)$ in the right half-plane, as shown in Fig. 9.7.

From the above criterion for stability, a simpler test can be derived that is useful in most common cases.
"If $|T(j \omega)|>1$ at the frequency where ph $T(j \omega)=-180^{\circ}$, then the amplifier is unstable." The validity of this criterion for the example considered here is apparent from inspection of Fig. 9.6 and application of the Nyquist criterion.

In order to examine the effect of feedback on the stability of an amplifier, consider the three-pole amplifier with gain function given by (9.6) to be placed in a negative-feedback loop with $f$ constant. The gain (in decibels) and phase of the amplifier are shown again in Fig. 9.8, and also plotted is the quantity $20 \log _{10} 1 / f$. The value of $20 \log _{10} 1 / f$ is approximately equal
image_name:Figure 9.7
description:The graph in Figure 9.7 is a Nyquist diagram represented in the complex plane, specifically the \(s\) plane. The horizontal axis is labeled \(\sigma\), representing the real part of the complex frequency, and the vertical axis is labeled \(j\omega\), representing the imaginary part. The graph features a closed contour that is symmetric about the real axis.

The Nyquist diagram illustrates the behavior of a system's frequency response and is used to assess stability. The diagram shows two different paths that the Nyquist plot can take, depending on the pole positions of the system.

1. **Path Passing Through (-1, 0):**
- The diagram indicates that the Nyquist plot passes through the point \((-1, 0)\) on the real axis when the poles are in a certain position. This scenario is often associated with a critical point for stability analysis.

2. **Path Encircling (-1, 0):**
- Alternatively, the diagram shows that the Nyquist plot can encircle the point \((-1, 0)\). This encirclement is significant in determining the stability of the system using the Nyquist criterion.

The diagram is essential for visualizing how the gain and phase of a system affect its stability, particularly in feedback control systems. The encirclement or passage through the critical point \((-1, 0)\) is crucial for applying the Nyquist stability criterion, which helps in determining whether the system is stable or unstable based on the number of encirclements of the point \((-1, 0)\).

Figure 9.7 Pole positions corresponding to different Nyquist diagrams.
image_name:Figure 9.8
description:The graph in Figure 9.8 is a Bode plot, which consists of two separate plots: one for the magnitude of the gain \(|a(j\omega)|\) and one for the phase \(\text{Ph} \, a(j\omega)\), both plotted against frequency \(\omega\) on a logarithmic scale.

Magnitude Plot:
- **Axes Labels and Units:**
- The vertical axis represents the magnitude of the gain in decibels (dB), labeled as \(|a(j\omega)| \, \text{dB}\).
- The horizontal axis represents frequency \(\omega\) on a logarithmic scale.

- **Overall Behavior and Trends:**
- The magnitude plot starts at a high gain level, then decreases as frequency increases.
- There is a noticeable drop in gain at certain frequencies, indicating poles at \(|p_1|, |p_2|, |p_3|\).

- **Key Features and Technical Details:**
- The curve intersects the line labeled \(20 \log_{10} \frac{1}{f} \approx 20 \log_{10} A_0\), indicating the gain crossover frequency where the loop gain is 0 dB.
- The distance \(x\) between the initial gain level \(20 \log_{10} a_0\) and the loop gain of 0 dB is marked.

Phase Plot:
- **Axes Labels and Units:**
- The vertical axis represents the phase of the gain in degrees, labeled as \(\text{Ph} \, a(j\omega)\).
- The horizontal axis is the same logarithmic frequency scale as the magnitude plot.

- **Overall Behavior and Trends:**
- The phase plot shows a decreasing trend, starting from 0° and moving downwards, crossing -45°, -90°, -135°, and reaching -180°.

- **Key Features and Technical Details:**
- A phase margin is indicated by the vertical distance between the phase curve and the -180° line at the frequency \(\omega_0\), where the gain crosses 0 dB.

Annotations and Specific Data Points:
- The graph is annotated with several critical frequencies \(\omega_0, |p_1|, |p_2|, |p_3|\), where significant changes in gain and phase occur.
- The phase margin is a critical parameter for determining system stability, indicating how far the phase is from -180° at the gain crossover frequency.

This Bode plot is essential for analyzing the stability and performance of feedback control systems, highlighting how the gain and phase margins affect the system's response.

Figure 9.8 Amplifier gain and phase versus frequency showing the phase margin.
to the low-frequency gain in decibels with feedback applied since

$$
\begin{equation*}
A_{0}=\frac{a_{0}}{1+a_{0} f} \tag{9.7}
\end{equation*}
$$

and thus

$$
\begin{equation*}
\frac{1}{f} \approx A_{0} \tag{9.8}
\end{equation*}
$$

if

$$
T_{0}=a_{0} f \gg 1
$$

Consider the vertical distance between the curve of $20 \log _{10}|a(j \omega)|$ and the line $20 \log _{10} 1 / f$ in Fig. 9.8. Since the vertical scale is in decibels this quantity is

$$
\begin{align*}
x & =20 \log _{10}|a(j \omega)|-20 \log _{10} 1 / f  \tag{9.9}\\
& =20 \log _{10}|a(j \omega) f| \\
& =20 \log _{10}|T(j \omega)| \tag{9.10}
\end{align*}
$$

Thus the distance $x$ is a direct measure in decibels of the loop-gain magnitude, $|T(j \omega)|$. The point where the curve of $20 \log _{10}|a(j \omega)|$ intersects the line $20 \log _{10} 1 / f$ is the point where the loop-gain magnitude $|T(j \omega)|$ is 0 dB or unity, and the curve of $|a(j \omega)|$ in decibels in Fig. 9.8 can thus be considered a curve of $|T(j \omega)|$ in decibels if the dotted line at $20 \log _{10} 1 / f$ is taken as the new zero axis.

The simple example of Section 9.1 showed that the gain curve versus frequency with feedback applied $\left(20 \log _{10}|A(j \omega)|\right)$ follows the $20 \log _{10} A_{0}$ line until it intersects the gain curve $20 \log _{10}|a(j \omega)|$. At higher frequencies the curve $20 \log _{10}|A(j \omega)|$ simply follows the curve of $20 \log _{10}|a(j \omega)|$ for the basic amplifier. The reason for this is now apparent in that at the higher frequencies the loop gain $|T(j \omega)| \rightarrow 0$ and the feedback then has no influence on the gain of the amplifier.

Figure 9.8 shows that the loop-gain magnitude $|T(j \omega)|$ is unity at frequency $\omega_{0}$. At this frequency the phase of $T(j \omega)$ has not reached $-180^{\circ}$ for the case shown, and using the modified Nyquist criterion stated above we conclude that this feedback loop is stable. Obviously $|T(j \omega)|<1$ at the frequency where $\mathrm{ph} T(j \omega)=-180^{\circ}$. If the polar Nyquist diagram is sketched for this example, it does not encircle the point $(-1,0)$.

As $|T(j \omega)|$ is made closer to unity at the frequency where ph $T(j \omega)=-180^{\circ}$, the amplifier has a smaller margin of stability, and this can be specified in two ways. The most common is the phase margin, which is defined as follows:

Phase margin $=180^{\circ}+(\mathrm{ph} T(j \omega)$ at frequency where $|T(j \omega)|=1)$. The phase margin is indicated in Fig. 9.8 and must be greater than $0^{\circ}$ for stability.

Another measure of stability is the gain margin. This is defined to be $1 /|T(j \omega)|$ in decibels at the frequency where ph $T(j \omega)=-180^{\circ}$, and this must be greater than 0 dB for stability.

The significance of the phase-margin magnitude is now explored. For the feedback amplifier considered in Section 9.1, where the basic amplifier has a single-pole response, the phase margin is obviously $90^{\circ}$ if the low-frequency loop gain is reasonably large. This is illustrated in Fig. 9.9 and results in a very stable amplifier. A typical lower allowable limit for the phase margin in practice is $45^{\circ}$, with a value of $60^{\circ}$ being more common.

Consider a feedback amplifier with a phase margin of $45^{\circ}$ and a feedback function $f$ that is real (and thus constant). Then

$$
\begin{equation*}
\text { ph } T\left(j \omega_{0}\right)=-135^{\circ} \tag{9.11}
\end{equation*}
$$

where $\omega_{0}$ is the frequency defined by

$$
\begin{equation*}
\left|T\left(j \omega_{0}\right)\right|=1 \tag{9.12}
\end{equation*}
$$

Now $\left|T\left(j \omega_{0}\right)\right|=\left|a\left(j \omega_{0}\right) f\right|=1$ implies that

$$
\begin{equation*}
\left|a\left(j \omega_{0}\right)\right|=\frac{1}{f} \tag{9.13}
\end{equation*}
$$

assuming that $f$ is positive real.
image_name:Figure 9.9
description:The graph in Figure 9.9 is a Bode plot, which consists of two separate plots: one for gain (magnitude) and one for phase, both plotted against frequency on a logarithmic scale.

1. **Type of Graph and Function**:
- The top plot represents the magnitude of the gain, \(|a(j\omega)|\), in decibels (dB).
- The bottom plot represents the phase of the gain, \(\text{Ph}\,a(j\omega)\), in degrees.
- Both plots are functions of frequency, \(\omega\), presented on a logarithmic scale.

2. **Axes Labels and Units**:
- The horizontal axis for both plots represents frequency (\(\omega\)) on a logarithmic scale.
- The vertical axis of the top plot is labeled \(|a(j\omega)|\) in dB, indicating the magnitude of the gain.
- The vertical axis of the bottom plot is labeled \(\text{Ph}\,a(j\omega)\), indicating the phase shift in degrees.

3. **Overall Behavior and Trends**:
- In the magnitude plot, the gain starts at a high level and decreases at a rate of \(-6\,\text{dB/octave}\) after a certain frequency, indicating a single-pole roll-off.
- In the phase plot, the phase starts near \(-45^\circ\) and decreases towards \(-180^\circ\) as the frequency increases.

4. **Key Features and Technical Details**:
- The initial gain level is marked as \(20 \log_{10} A_0\), where \(A_0\) is the low-frequency gain.
- The point where the loop gain equals 0 dB is marked on the magnitude plot, indicating the crossover frequency.
- The phase margin is approximately \(90^\circ\), as indicated on the phase plot. This is the difference between the phase at the crossover frequency and \(-180^\circ\).

5. **Annotations and Specific Data Points**:
- The magnitude plot includes annotations for \(T_0\) and the loop gain.
- The phase plot highlights the phase margin with a reference line at \(-135^\circ\), showing the phase shift at the crossover frequency.

This Bode plot provides insight into the stability and frequency response of a single-pole basic amplifier, emphasizing the phase margin and gain characteristics across frequencies.

Figure 9.9 Gain and phase versus frequency for a single-pole basic amplifier showing the phase margin for a low-frequency loop gain $T_{0}$.

The overall gain is

$$
\begin{equation*}
A(j \omega)=\frac{a(j \omega)}{1+T(j \omega)} \tag{9.14}
\end{equation*}
$$

Substitution of (9.11) and (9.12) in (9.14) gives

$$
A\left(j \omega_{0}\right)=\frac{a\left(j \omega_{0}\right)}{1+e^{-j 135^{\circ}}}=\frac{a\left(j \omega_{0}\right)}{1-0.7-0.7 j}=\frac{a\left(j \omega_{0}\right)}{0.3-0.7 j}
$$

and thus

$$
\begin{equation*}
\left|A\left(j \omega_{0}\right)\right|=\frac{\left|a\left(j \omega_{0}\right)\right|}{0.76}=\frac{1.3}{f} \tag{9.15}
\end{equation*}
$$

using (9.13).
The frequency $\omega_{0}$, where $\left|T\left(j \omega_{0}\right)\right|=1$, is the nominal $-3-\mathrm{dB}$ point for a single-pole basic amplifier, but in this case there is $2.4 \mathrm{~dB}(1.3 \times)$ of peaking above the low-frequency gain of $1 / f$.

Consider a phase margin of $60^{\circ}$. At the frequency $\omega_{0}$ in this case

$$
\begin{equation*}
\operatorname{ph} T\left(j \omega_{0}\right)=-120^{\circ} \tag{9.16}
\end{equation*}
$$

and

$$
\begin{equation*}
\left|T\left(j \omega_{0}\right)\right|=1 \tag{9.17}
\end{equation*}
$$

Following a similar analysis we obtain

$$
\left|A\left(j \omega_{0}\right)\right|=\frac{1}{f}
$$

In this case there is no peaking at $\omega=\omega_{0}$, but there has also been no gain reduction at this frequency.

Finally, the case where the phase margin is $90^{\circ}$ can be similarly calculated. In this case

$$
\begin{equation*}
\operatorname{ph} T\left(j \omega_{0}\right)=-90^{\circ} \tag{9.18}
\end{equation*}
$$

and

$$
\begin{equation*}
\left|T\left(j \omega_{0}\right)\right|=1 \tag{9.19}
\end{equation*}
$$

A similar analysis gives

$$
\begin{equation*}
\left|A\left(j \omega_{0}\right)\right|=\frac{0.7}{f} \tag{9.20}
\end{equation*}
$$

As expected in this case, the gain at frequency $\omega_{0}$ is 3 dB below the midband value.
These results are illustrated in Fig. 9.10, where the normalized overall gain versus frequency is shown for various phase margins. The plots are drawn assuming the response is dominated by the first two poles of the transfer function, except for the case of the $90^{\circ}$ phase margin, which has one pole only. As the phase margin diminishes, the gain peak becomes larger until the gain approaches infinity and oscillation occurs for phase margin $=0^{\circ}$. The gain peak usually occurs close to the frequency where $|T(j \omega)|=1$, but for a phase margin of $60^{\circ}$ there is 0.2 dB of peaking just below this frequency. Note that after the peak, the gain curves approach an asymptote of $-12 \mathrm{~dB} /$ octave for phase margins other than $90^{\circ}$. This is because the open-loop gain falls at -12 dB /octave due to the presence of two poles in the transfer function.

The simple tests for stability of a feedback amplifier (i.e., positive phase and gain margins) can only be applied when the phase and gain margins are uniquely defined. The phase margin is uniquely defined if there is only one frequency at which the magnitude of the loop gain equals one. Similarly, the gain margin is uniquely defined if there is only one frequency at which the phase of the loop gain equals $-180^{\circ}$. In most feedback circuits, these margins are uniquely defined. However, if either of these margins is not uniquely defined, then stability should be checked using a Nyquist diagram and the Nyquist criterion.
image_name:Figure 9.10
description:**Type of Graph and Function:**
The graph is a Bode plot, specifically showing the relative gain in decibels (dB) versus the normalized frequency for feedback amplifiers. It illustrates how the gain changes with frequency for different phase margins.

**Axes Labels and Units:**
- The vertical axis represents the "Relative gain" measured in decibels (dB). It ranges from -15 dB to 10 dB, with grid lines marked at intervals of 5 dB.
- The horizontal axis represents "Relative frequency," which is normalized and spans from approximately 0.1 to 10. The scale is logarithmic, as indicated by the spacing of the frequency markers.

**Overall Behavior and Trends:**
The graph shows several curves, each corresponding to a different phase margin (30°, 45°, 60°, 90°). The curves demonstrate how the gain varies with frequency:
- At low frequencies (below the unity gain frequency, marked as 1 on the horizontal axis), the gain remains relatively constant.
- As frequency increases towards the unity gain frequency, the gain starts to peak, particularly noticeable in the curves with smaller phase margins.
- Beyond the unity gain frequency, the gain decreases, with the slope dependent on the phase margin. The slopes are marked as -6 dB/octave and -12 dB/octave.

**Key Features and Technical Details:**
- The phase margin is annotated for each curve at its respective peak or inflection point.
- The gain for the 30° phase margin curve peaks higher and decreases more steeply compared to the others, indicating less stability.
- The 90° phase margin curve shows the least peaking and a gentler slope, suggesting higher stability.

**Annotations and Specific Data Points:**
- The phase margins are clearly labeled on the graph for each curve.
- The slopes of the curves beyond the unity gain frequency are marked as -6 dB/octave and -12 dB/octave, indicating the rate of gain decrease with frequency.
- The unity gain frequency is indicated by the point where the relative frequency is 1 on the horizontal axis.

Figure 9.10 Normalized overall gain for feedback amplifiers versus normalized frequency for various phase margins. Frequency is normalized to the frequency where the loop gain is unity.

The loop gain $T=a f$ can be examined to determine the stability of a feedback circuit, as explained in this section. Alternatively these measures of stability can be applied to the return ratio $\mathscr{R}$, as explained in Appendix A9.1. Techniques for simulating $\mathscr{R}^{2-5}$ and $T=a f^{4}$ using SPICE have been developed, based on methods for measuring loop transmission. ${ }^{6,7}$ These techniques measure the loop transmission at the closed-loop dc operating point. An advantage of SPICE simulation of the loop transmission is that parasitics that might have an important effect are included. For example, parasitic capacitance at the op-amp input introduces frequency dependence in the feedback network in Fig. 8.24, which may degrade the phase margin.

## 9.4 Compensation

### 9.4.1 Theory of Compensation

Consider again the amplifier whose gain and phase is shown in Fig. 9.8. For the feedback circuit in which this was assumed to be connected, the forward gain was $A_{0}$, as shown in Fig. 9.8 , and the phase margin was positive. Thus the circuit was stable. It is apparent, however, that if the amount of feedback is increased by making $f$ larger (and thus $A_{0}$ smaller), oscillation will eventually occur. This is shown in Fig. 9.11, where $f_{1}$ is chosen to give a zero phase margin and the corresponding overall gain is $A_{1} \simeq 1 / f_{1}$. If the feedback is increased to $f_{2}$ (and $A_{2} \simeq 1 / f_{2}$ is the overall gain), the phase margin is negative and the circuit will oscillate. Thus if this amplifier is to be used in a feedback loop with loop gain larger than $a_{0} f_{1}$, efforts
image_name:Figure 9.11
description:Figure 9.11 is a Bode plot that consists of two graphs: the magnitude plot and the phase plot, both plotted against frequency on a logarithmic scale.

Magnitude Plot:
- **Y-Axis:** Represents the magnitude of the gain \(|a(j\omega)|\) in decibels (dB).
- **X-Axis:** Represents the frequency \(\omega\) on a logarithmic scale.
- **Behavior:** The plot starts at a high gain level, indicated as \(20 \log_{10} a_0\), and decreases with increasing frequency.
- **Key Points:** There are markers at frequencies \(|p_1|\), \(|p_2|\), and \(|p_3|\), indicating pole frequencies where the slope of the magnitude plot changes.
- **Annotations:** Two specific gain levels are noted: \(20 \log_{10} \frac{1}{f_1} \approx 20 \log_{10} A_1\) and \(20 \log_{10} \frac{1}{f_2} \approx 20 \log_{10} A_2\), corresponding to feedback factors \(f_1\) and \(f_2\).

Phase Plot:
- **Y-Axis:** Represents the phase \(Ph \, a(j\omega)\) in degrees.
- **X-Axis:** Represents the frequency \(\omega\) on a logarithmic scale.
- **Behavior:** The phase starts around \(-45^\circ\) and decreases, passing through \(-90^\circ\), \(-135^\circ\), \(-180^\circ\), and reaching \(-270^\circ\) as frequency increases.
- **Key Points:** The phase plot is smooth and continuously decreasing, with significant phase shifts occurring around the pole frequencies \(|p_1|\), \(|p_2|\), and \(|p_3|\).

Overall Description:
This Bode plot illustrates the gain and phase characteristics of a three-pole amplifier. The magnitude plot shows a typical roll-off with increasing frequency, while the phase plot indicates a continuous phase lag. Feedback factors \(f_1\) and \(f_2\) are critical for determining phase margin and stability, with \(f_1\) giving a zero phase margin and \(f_2\) resulting in a negative phase margin, leading to oscillations.

Figure 9.11 Gain and phase versus frequency for a three-pole basic amplifier. Feedback factor $f_{1}$ gives a zero phase margin and factor $f_{2}$ gives a negative phase margin.
must be made to increase the phase margin. This process is known as compensation. Note that without compensation, the forward gain of the feedback amplifier cannot be made less than $A_{1} \simeq 1 / f_{1}$ because of the oscillation problem.

The simplest and most common method of compensation is to reduce the bandwidth of the amplifier (often called narrowbanding). That is, a dominant pole is deliberately introduced into the amplifier to force the phase shift to be less than $-180^{\circ}$ when the loop gain is unity. This involves a direct sacrifice of the frequency capability of the amplifier.

If $f$ is constant, the most difficult case to compensate is $f=1$, which is a unity-gain feedback configuration. In this case the loop-gain curve is identical to the gain curve of the basic amplifier. Consider this situation and assume that the basic amplifier has the same characteristic as in Fig. 9.11. To compensate the amplifier, we introduce a new dominant pole with magnitude $\left|p_{D}\right|$, as shown in Fig. 9.12, and assume that this does not affect the original amplifier poles with magnitudes $\left|p_{1}\right|,\left|p_{2}\right|$, and $\left|p_{3}\right|$. This is often not the case but is assumed here for purposes of illustration.

The introduction of the dominant pole with magnitude $\left|p_{D}\right|$ into the amplifier gain function causes the gain magnitude to decrease at $6 \mathrm{~dB} /$ octave until frequency $\left|p_{1}\right|$ is reached, and over this region the amplifier phase shift asymptotes to $-90^{\circ}$. If frequency $\left|p_{D}\right|$ is chosen so that the gain $|a(j \omega)|$ is unity at frequency $\left|p_{1}\right|$ as shown, then the loop gain is also unity at frequency $\left|p_{1}\right|$ for the assumed case of unity feedback with $f=1$. The phase margin in this case is then $45^{\circ}$, which means that the amplifier is stable. The original amplifier would have been unstable in such a feedback connection.
image_name:Figure 9.12
description:The graph in Figure 9.12 is a Bode plot, which consists of two separate plots: a gain (magnitude) plot and a phase plot, both against frequency on a logarithmic scale.

1. **Type of Graph and Function:**
- The graph is a Bode plot used to analyze the frequency response of a three-pole basic amplifier.

2. **Axes Labels and Units:**
- The horizontal axis represents frequency (ω) on a logarithmic scale.
- The vertical axis of the top plot represents gain, denoted as |a(jω)|, in decibels (dB).
- The vertical axis of the bottom plot represents phase, denoted as Ph a(jω), in degrees.

3. **Overall Behavior and Trends:**
- **Gain Plot:**
- The original gain curve starts at a high level and decreases at a rate of -6 dB/octave until it reaches |p₁|. Beyond |p₁|, it continues to decrease at -12 dB/octave.
- The gain curve after compensation starts similarly but has a lower slope of -6 dB/octave throughout, intersecting the original gain curve at |p₁|.
- **Phase Plot:**
- The original phase begins near 0° and decreases, asymptotically approaching -270°.
- The phase after compensation starts similarly but asymptotically approaches -180°.

4. **Key Features and Technical Details:**
- The gain curve shows three poles at frequencies |p₁|, |p₂|, and |p₃|, with the introduction of a negative real pole at |p_D| for compensation.
- The gain after compensation achieves unity at |p₁|.
- The phase margin after compensation is indicated as 45°, ensuring stability.

5. **Annotations and Specific Data Points:**
- The gain curve after compensation is labeled and shown with a dashed line.
- The phase after compensation is also labeled with a dashed line.
- The phase margin of 45° is explicitly marked on the phase plot.
- Vertical dashed lines mark the pole frequencies |p_D|, |p₁|, |p₂|, and |p₃|.

Figure 9.12 Gain and phase versus frequency for a three-pole basic amplifier. Compensation for unity-gain feedback operation $(f=1)$ is achieved by introduction of a negative real pole with magnitude $\left|p_{D}\right|$.

The price that has been paid for achieving stability in this case is that with the feedback removed, the basic amplifier has a unity-gain bandwidth of only $\left|p_{1}\right|$, which is much less than before. Also, with feedback applied, the loop gain now begins to decrease at a frequency $\left|p_{D}\right|$, and all the benefits of feedback diminish as the loop gain decreases. For example, in Chapter 8 it was shown that shunt feedback at the input or output of an amplifier reduces the basic terminal impedance by $[1+T(j \omega)]$. Since $T(j \omega)$ is frequency dependent, the terminal impedance of a shunt-feedback amplifier will begin to rise when $|T(j \omega)|$ begins to decrease. Thus the high-frequency terminal impedance will appear inductive, as in the case of $z_{0}$ for an emitter follower, which was calculated in Chapter 7. (See Problem 9.8.)

#### EXAMPLE

Calculate the dominant-pole magnitude required to give unity-gain compensation of the 702 op amp with a phase margin of $45^{\circ}$. The low-frequency gain is $a_{0}=3600$ and the circuit has poles at $-\left(p_{1} / 2 \pi\right)=1 \mathrm{MHz},-\left(p_{2} / 2 \pi\right)=4 \mathrm{MHz}$, and $-\left(p_{3} / 2 \pi\right)=40 \mathrm{MHz}$.

In this example, the second pole $p_{2}$ is sufficiently close to $p_{1}$ to produce significant phase shift at the amplifier $-3-\mathrm{dB}$ frequency. The approach to this problem will be to use the approximate results developed above to obtain an initial estimate of the required dominant-pole magnitude and then to empirically adjust this estimate to obtain the required results.

The results of Fig. 9.12 indicate that a dominant pole with magnitude $\left|p_{D}\right|$ should be introduced so that gain $a_{0}=3600$ is reduced to unity at $\left|p_{1} / 2 \pi\right|=1 \mathrm{MHz}$ with a $6-\mathrm{dB} /$ octave decrease as a function of frequency. The product $|a| \omega$ is constant where the slope of the gain-magnitude plot is -6 dB /octave; therefore

$$
\left|\frac{p_{D}}{2 \pi}\right|=\frac{1}{a_{0}}\left|\frac{p_{1}}{2 \pi}\right|=\frac{10^{6}}{3600} \mathrm{~Hz}=278 \mathrm{~Hz}
$$

This would give a transfer function

$$
\begin{equation*}
a(j \omega)=\frac{3600}{\left(1+\frac{j \omega}{\left|p_{D}\right|}\right)\left(1+\frac{j \omega}{\left|p_{1}\right|}\right)\left(1+\frac{j \omega}{\left|p_{2}\right|}\right)\left(1+\frac{j \omega}{\left|p_{3}\right|}\right)} \tag{9.21}
\end{equation*}
$$

where the pole magnitudes are in radians per second. Equation 9.21 gives a unity-gain frequency [where $|a(j \omega)|=1$ ] of 780 kHz . This is slightly below the design value of 1 MHz because the actual gain curve is 3 dB below the asymptote at the break frequency $\left|p_{1}\right|$. At 780 kHz the phase shift obtained from (9.21) is $-139^{\circ}$ instead of the desired $-135^{\circ}$ and this includes a contribution of $-11^{\circ}$ from pole $p_{2}$. Although this result is close enough for most purposes, a phase margin of precisely $45^{\circ}$ can be achieved by empirically reducing $\left|p_{D}\right|$ until (9.21) gives a phase shift of $-135^{\circ}$ at the unity gain frequency. This occurs for $\left|p_{D} / 2 \pi\right|=$ 260 Hz , which gives a unity-gain frequency of 730 kHz .

Consider now the performance of the amplifier whose characteristic is shown in Fig. 9.12 (with dominant pole magnitude $\left|p_{D}\right|$ ) when used in a feedback loop with $f<1$ (i.e., overall gain $A_{0}>1$ ). This case is shown in Fig. 9.13. The loop gain now falls to unity at frequency $\omega_{x}$ and the phase margin of the circuit is now approximately $90^{\circ}$. The $-3-\mathrm{dB}$ bandwidth of the feedback circuit is $\omega_{x}$. The circuit now has more compensation than is needed, and, in fact, bandwidth is being wasted. Thus, although it is convenient to compensate an amplifier for unity gain and then use it unchanged for other applications (as is done in many op amps), this procedure is quite wasteful of bandwidth. Fixed-gain amplifiers that are designed for applications where maximum bandwidth is required are usually compensated for a specified phase margin (typically $45^{\circ}$ to $60^{\circ}$ ) at the required gain value. However, op amps are
image_name:Figure 9.13
description:The graph in Figure 9.13 is a Bode plot, which is used to represent the gain and phase of an amplifier as a function of frequency. It consists of two separate plots: the upper plot shows the magnitude of the gain in decibels (dB) and the lower plot shows the phase angle in degrees.

1. **Type of Graph and Function:**
- This is a Bode plot, commonly used in control systems and signal processing to analyze the frequency response of a system.

2. **Axes Labels and Units:**
- The horizontal axis (common to both plots) represents frequency \( \omega \) on a logarithmic scale.
- The vertical axis of the upper plot represents the magnitude of the gain \(|a(j\omega)|\) in decibels (dB).
- The vertical axis of the lower plot represents the phase angle \( \text{Ph} \, a(j\omega) \) in degrees.

3. **Overall Behavior and Trends:**
- **Gain Plot:** The gain starts at a high value of \(20 \log_{10} a_0\) and decreases at a rate of \(-6 \text{ dB/octave}\) initially, indicating a single-pole roll-off. It then transitions to a steeper slope of \(-12 \text{ dB/octave}\), suggesting the presence of an additional pole.
- **Phase Plot:** The phase begins at 0 degrees and decreases, passing through critical points such as \(-45^{\circ}\), \(-90^{\circ}\), \(-135^{\circ}\), and approaches \(-180^{\circ}\) as frequency increases.

4. **Key Features and Technical Details:**
- **Loop Gain:** The plot indicates the loop gain, with a specific point marked where the loop gain is 0 dB.
- **Phase Margin:** The phase margin is shown as the difference between the phase angle and \(-180^{\circ}\) at the frequency where the gain crosses 0 dB. In this graph, it is indicated to be \(45^{\circ}\).
- **Critical Frequencies:** The frequency \( \omega_x \) is marked, corresponding to the unity gain crossover frequency where the gain is 0 dB.
- **Roll-off Rates:** The transition from \(-6 \text{ dB/octave}\) to \(-12 \text{ dB/octave}\) is clearly depicted, indicating the change in system dynamics.

5. **Annotations and Specific Data Points:**
- Annotations include the loop gain values and the specific phase margin. The plot also shows the gain at \( \omega_x \) and the corresponding phase shift.
- Specific markers such as \( |P_1| \) and \( |P_D| \) are indicated, which represent certain gain and phase characteristics at particular frequencies.

Figure 9.13 Gain and phase versus frequency for an amplifier compensated for use in a feedback loop with $f=1$ and a phase margin of $45^{\circ}$. The phase margin is shown for operation in a feedback loop with $f<1$.
general-purpose circuits that are used with differing feedback networks with $f$ values ranging from 0 to 1 . Optimum bandwidth is achieved in such circuits if the compensation is tailored to the gain value required, and this approach gives much higher bandwidths for high gain values, as seen in Fig. 9.14. This figure shows compensation of the amplifier characteristic of Fig. 9.11 for operation in a feedback circuit with forward gain $A_{0}$. A dominant pole is added with magnitude $\left|p_{D}^{\prime}\right|$ to give a phase margin of $45^{\circ}$. Frequency $\left|p_{D}^{\prime}\right|$ is obviously $\gg\left|p_{D}\right|$, and the $-3-\mathrm{dB}$ bandwidth of the feedback amplifier is nominally $\left|p_{1}\right|$, at which frequency the loop gain is 0 dB (disregarding peaking). The $-3-\mathrm{dB}$ frequency from Fig. 9.13 would be only $\omega_{x}=\left|p_{1}\right| / A_{0}$ if unity-gain compensation had been used. Obviously, since $A_{0}$ can be large, the improvement in bandwidth is significant.

In the compensation schemes discussed above, an additional dominant pole was assumed to be added to the amplifier, and the original amplifier poles were assumed to be unaffected by this procedure. In terms of circuit bandwidth, a much more efficient way to compensate the amplifier is to add capacitance to the circuit in such a way that the original amplifier dominant pole magnitude $\left|p_{1}\right|$ is reduced so that it performs the compensation function. This technique requires access to the internal nodes of the amplifier, and knowledge of the nodes in the circuit where added capacitance will reduce frequency $\left|p_{1}\right|$.

Consider the effect of compensating for unity-gain operation the amplifier characteristic of Fig. 9.11 in this way. Again assume that higher frequency poles $p_{2}$ and $p_{3}$ are unaffected by this procedure. In fact, depending on the method of compensation, these poles are usually moved up or down in magnitude by the compensation. This point will be taken up later.
image_name:Figure 9.14
description:The graph in Figure 9.14 is a Bode plot, which consists of two separate plots: one for gain and one for phase, both plotted against frequency on a logarithmic scale.

Gain Plot:
- **Axes:**
- The vertical axis represents gain in decibels (dB), noted as \( |a(j\omega)| \) dB.
- The horizontal axis represents frequency \( \omega \) on a logarithmic scale.
- **Behavior and Trends:**
- The gain plot shows two curves: the original gain curve and the gain curve after compensation.
- The original gain curve decreases at a rate of \(-6 \text{ dB/octave}\) initially, then \(-12 \text{ dB/octave}\), and finally \(-18 \text{ dB/octave}\) as frequency increases past \(|p_1|\), \(|p_2|\), and \(|p_3|\) respectively.
- The compensated gain curve starts at a higher level and maintains a \(-6 \text{ dB/octave}\) slope until \(|p_D'|\), after which it follows the original curve's slope changes.
- **Key Features:**
- The loop gain is marked as the difference between the initial gain level \(20 \log_{10} a_0\) and \(20 \log_{10} \frac{1}{f} \approx 20 \log_{10} A_0\).
- Important frequency markers are \(|p_D'|\), \(|p_1|\), \(|p_2|\), and \(|p_3|\), indicating pole locations.

Phase Plot:
- **Axes:**
- The vertical axis represents phase in degrees, noted as \( \text{Ph} \, a(j\omega) \).
- The horizontal axis is the same frequency \( \omega \) as the gain plot.
- **Behavior and Trends:**
- The phase plot shows two curves: the original phase curve and the phase curve after compensation.
- The original phase decreases, crossing critical phase angles like \(-45^\circ\), \(-90^\circ\), \(-135^\circ\), \(-180^\circ\), etc.
- The phase after compensation is adjusted to provide a phase margin of \(45^\circ\), leading to a phase shift that is less steep than the original.
- **Key Features:**
- The phase margin of \(45^\circ\) is highlighted, showing the improvement in stability due to compensation.

Annotations and Specific Data Points:
- The graph includes annotations indicating the slopes of the gain curves and the phase margin.
- Vertical dashed lines mark the frequencies \(|p_D'|\), \(|p_1|\), \(|p_2|\), and \(|p_3|\), which are critical points for both gain and phase adjustments.

Figure 9.14 Gain and phase versus frequency for an amplifier compensated for use in a feedback loop with $f<1$ and a phase margin of $45^{\circ}$. Compensation is achieved by adding a new pole $p_{D}^{\prime}$ to the amplifier.

Compensation of the amplifier by reducing $\left|p_{1}\right|$ is shown in Fig. 9.15. For a $45^{\circ}$-phase margin in a unity-gain feedback configuration, dominant pole magnitude $\left|p_{1}^{\prime}\right|$ must cause the gain to fall to unity at frequency $\left|p_{2}\right|$ (the second pole magnitude). Thus the nominal bandwidth in a unity-gain configuration is $\left|p_{2}\right|$, and the loop gain is unity at this frequency. This result can be contrasted with a bandwidth of $\left|p_{1}\right|$, as shown in Fig. 9.12 for compensation achieved by adding another pole with magnitude $\left|p_{D}\right|$ to the amplifier. In practical amplifiers, frequency $\left|p_{2}\right|$ is often 5 or 10 times frequency $\left|p_{1}\right|$ and substantial improvements in bandwidth are thus achieved.

The results of this section illustrate why the basic amplifier of a feedback circuit is usually designed with as few stages as possible. Each stage of gain inevitably adds more poles to the transfer function, complicating the compensation problem, particularly if a wide bandwidth is required.

### 9.4.2 Methods of Compensation

In order to compensate a circuit by the common method of narrowbanding described above, it is necessary to add capacitance to create a dominant pole with the desired magnitude. One method of achieving this is shown in Fig. 9.16, which is a schematic of the first two stages of a simple amplifier. A large capacitor $C$ is connected between the collectors of the input stage. The output stage, which is assumed relatively broadband, is not shown. A differential half-circuit of Fig. 9.16 is shown in Fig. 9.17, and it should be noted that the compensation
image_name:Figure 9.15
description:The graph in Figure 9.15 is a Bode plot, which consists of two subplots: a gain plot and a phase plot, both plotted against frequency on a logarithmic scale.

**Gain Plot:**
- **Axes:** The vertical axis represents the magnitude of the gain \(|a(j\omega)|\) in decibels (dB), and the horizontal axis represents the frequency \(\omega\) on a logarithmic scale.
- **Behavior:** The original gain curve starts at a high gain level and decreases with slopes of \(-6\, \text{dB/octave}\), \(-12\, \text{dB/octave}\), and \(-18\, \text{dB/octave}\) as the frequency increases. The compensated gain curve, which is shown as a dashed line, follows a \(-6\, \text{dB/octave}\) slope from the start, indicating a reduction in the dominant pole's magnitude.
- **Key Features:** The plot shows significant points labeled \(|p'_1|\), \(|p_1|\), \(|p_2|\), and \(|p_3|\), which are critical frequencies where the slope changes occur.

**Phase Plot:**
- **Axes:** The vertical axis represents the phase \(\text{Ph } a(j\omega)\) in degrees, while the horizontal axis is the same logarithmic frequency scale as the gain plot.
- **Behavior:** The original phase curve decreases with frequency, showing a typical phase lag. The compensated phase curve, shown as a dashed line, indicates a phase shift designed to improve stability.
- **Key Features:** The phase margin is marked at \(45^{\circ}\), showing the difference between the phase of the compensated system and \(-180^{\circ}\) at the gain crossover frequency. The phase after compensation is less negative, indicating improved stability.

**Annotations:**
- The graph includes annotations of the gain and phase curves before and after compensation, highlighting the effects of introducing a large capacitor to reduce the dominant pole's magnitude. This compensation aims to achieve a phase margin of \(45^{\circ}\), ensuring stability when the amplifier is used in a feedback loop.
Figure 9.15 Gain and phase versus frequency for an amplifier compensated for use in a feedback loop with $f=1$ and a phase margin of $45^{\circ}$. Compensation is achieved by reducing the magnitude $\left|p_{1}\right|$ of the dominant pole of the original amplifier.

image_name:Compensation of an amplifier by introduction of a large capacitor $C$.
description:
[
name: Q1, type: NPN, ports: {C: c1b3, B: vin, E: e1e2}
name: Q2, type: NPN, ports: {C: c2b4, B: Vip, E: e1e2}
name: Q3, type: NPN, ports: {C: Vcc, B: c1b3, E: e3e4}
name: Q4, type: NPN, ports: {C: Vout, B: c2b4, E: e3e4}
name: RL1, type: Resistor, value: RL1, ports: {N1: VCC, N2: c1b3}
name: RL2, type: Resistor, value: RL2, ports: {N1: VCC, N2: Vout}
name: C, type: Capacitor, value: C, ports: {Np: c1b3, Nn: c2b4}
name: VEE, type: VoltageSource, value: VEE, ports: {Np: e1e2, Nn: GND}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with compensation achieved by introducing a large capacitor C. It uses NPN transistors Q1, Q2, Q3, and Q4. The compensation reduces the magnitude of the dominant pole to achieve stability with a phase margin of 45 degrees. The resistors RL1 and RL2 are connected to the VCC rail, and the circuit is powered by VCC and VEE voltage sources.
Figure 9.16 Compensation of an amplifier by introduction of a large capacitor $C$.
capacitor is doubled in the half-circuit. The major contributions to the dominant pole of a circuit of this type (if $R_{S}$ is not large) come from the input capacitance of $Q_{4}$ and Miller capacitance associated with $Q_{4}$. Thus the compensation as shown will reduce the magnitude of the dominant pole of the original amplifier so that it performs the required compensation function. Almost certainly, however, the higher frequency poles of the amplifier will also be changed by the addition of $C$. In practice, the best method of approaching the compensation
image_name:Figure 9.17 Differential half-circuit of Fig. 9.16
description:
[
name: Vs, type: VoltageSource, ports: {Np: Vs, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vs, N2: Q2_B}
name: Q2, type: NPN, ports: {C: c2b4, B: Q2_B, E: GND}
name: RL1, type: Resistor, value: RL1, ports: {N1: c2b4, N2: GND}
name: 2C, type: Capacitor, value: 2C, ports: {Np: c2b4, Nn: GND}
name: Q4, type: NPN, ports: {C: Vo, B: c2b4, E: GND}
name: RL2, type: Resistor, value: RL2, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a differential amplifier with compensation. It includes two NPN transistors (Q2 and Q4) and uses capacitive compensation (C2b4) to manage pole positions. The output is taken across RL2.

Figure 9.17 Differential half-circuit of Fig. 9.16.
design is to use computer simulation to determine the original pole positions. A first estimate of $C$ is made on the assumption that the higher frequency poles do not change in magnitude and a new computer simulation is made with $C$ included to check this assumption. Another estimate of $C$ is then made on the basis of the new simulation, and this process usually converges after several iterations.

The magnitude of the dominant pole of Fig. 9.17 can be estimated using zero-value time constant analysis. However, if the value of $C$ required is very large, this capacitor will dominate and a good estimate of the dominant pole can be made by considering $C$ only and ignoring other circuit capacitance. In that case the dominant-pole magnitude is

$$
\begin{equation*}
\left|p_{D}\right|=\frac{1}{2 C R} \tag{9.22}
\end{equation*}
$$

where

$$
\begin{equation*}
R=R_{L 1} \| R_{i 4} \tag{9.23}
\end{equation*}
$$

and

$$
\begin{equation*}
R_{i 4}=r_{b 4}+r_{\pi 4} \tag{9.24}
\end{equation*}
$$

One disadvantage of the above method of compensation is that the value of $C$ required is quite large (typically $>1000 \mathrm{pF}$ ) and cannot be realized on a monolithic chip.

Many general-purpose op amps have unity-gain compensation included on the monolithic chip and require no further compensation from the user. (The sacrifice in bandwidth caused by this technique when using gain other than unity was described earlier.) In order to realize an internally compensated monolithic op amp, compensation must be achieved using capacitance less than about 50 pF . This can be achieved using Miller multiplication of the capacitance as in the 741 op amp , which uses a 30 pF compensation capacitor and was analyzed in previous editions of this book.

As well as allowing use of a small capacitor that can be integrated on the monolithic chip, this type of compensation has another significant advantage. This is due to the phenomenon of pole splitting, ${ }^{8}$ in which the dominant pole moves to a lower frequency while the next pole moves to a higher frequency. The splitting of the two low-frequency poles in practical op amps is often a rather complex process involving other higher frequency poles and zeros as well. However, the process involved can be illustrated with the two-stage op-amp model in Fig. 9.18. The input is from from a current $i_{s}$, which stems from the transconductance of the first stage times the op-amp differential input voltage. Resistors $R_{1}$ and $R_{2}$ represent the total shunt resistances at the output of the first and second stages, including transistor input and output resistances. Similarly, $C_{1}$ and $C_{2}$ represent the total shunt capacitances at the same places. Capacitor $C$ represents transistor collector-base capacitance of the amplifying transistor in the second stage plus the compensation capacitance.
image_name:Figure 9.18 Small-signal equivalent circuit of a single transistor stage
description:
[
name: is, type: CurrentSource, value: is, ports: {Np: V1, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: V1, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: V1, Nn: GND}
name: C, type: Capacitor, value: C, ports: {Np: V1, Nn: Vo}
name: gmv1, type: VoltageControlledCurrentSource, value: gmv1, ports: {Np: Vo, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: Vo, Nn: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit represents a small-signal equivalent of a single transistor stage with feedback. The feedback capacitor C includes compensation capacitance.

Figure 9.18 Small-signal equivalent circuit of a single transistor stage. Feedback capacitor $C$ includes compensation capacitance.

For the circuit of Fig. 9.18,

$$
\begin{gather*}
-i_{s}=\frac{v_{1}}{R_{1}}+v_{1} C_{1} s+\left(v_{1}-v_{o}\right) C s  \tag{9.25}\\
g_{m} v_{1}+\frac{v_{o}}{R_{2}}+v_{o} C_{2} s+\left(v_{o}-v_{1}\right) C s=0 \tag{9.26}
\end{gather*}
$$

From (9.25) and (9.26)

$$
\begin{equation*}
\frac{v_{o}}{i_{s}}=\frac{\left(g_{m}-C s\right) R_{2} R_{1}}{1+s\left[\left(C_{2}+C\right) R_{2}+\left(C_{1}+C\right) R_{1}+g_{m} R_{2} R_{1} C\right]+s^{2} R_{2} R_{1}\left(C_{2} C_{1}+C C_{2}+C C_{1}\right)} \tag{9.27}
\end{equation*}
$$

The circuit transfer function has a positive real zero at

$$
\begin{equation*}
z=\frac{g_{m}}{C} \tag{9.27a}
\end{equation*}
$$

which usually has such a large magnitude in bipolar circuits that it can be neglected. This is often not the case in MOS circuits because of their lower $g_{m}$. This point is taken up later.

The circuit has a two-pole transfer function. If $p_{1}$ and $p_{2}$ are the poles of the circuit, then the denominator of (9.27) can be written

$$
\begin{align*}
D(s) & =\left(1-\frac{s}{p_{1}}\right)\left(1-\frac{s}{p_{2}}\right)  \tag{9.28}\\
& =1-s\left(\frac{1}{p_{1}}+\frac{1}{p_{2}}\right)+\frac{s^{2}}{p_{1} p_{2}} \tag{9.29}
\end{align*}
$$

and thus

$$
\begin{equation*}
D(s) \simeq 1-\frac{s}{p_{1}}+\frac{s^{2}}{p_{1} p_{2}} \tag{9.30}
\end{equation*}
$$

if the poles are real and widely separated, which is usually true. Note that $p_{1}$ is assumed to be the dominant pole.

If the coefficients in (9.27) and (9.30) are equated then

$$
\begin{equation*}
p_{1}=-\frac{1}{\left(C_{2}+C\right) R_{2}+\left(C_{1}+C\right) R_{1}+g_{m} R_{2} R_{1} C} \tag{9.31}
\end{equation*}
$$

and this can be approximated by

$$
\begin{equation*}
p_{1} \simeq-\frac{1}{g_{m} R_{2} R_{1} C} \tag{9.32}
\end{equation*}
$$

since the Miller effect due to $C$ will be dominant if $C$ is large and $g_{m} R_{1}, g_{m} R_{2} \gg 1$. Equation 9.31 is the same result for the dominant pole as is obtained using zero-value time constant analysis.

The nondominant pole $p_{2}$ can now be estimated by equating coefficients of $s^{2}$ in (9.27) and (9.30) and using (9.32).

$$
\begin{equation*}
p_{2} \simeq-\frac{g_{m} C}{C_{2} C_{1}+C\left(C_{2}+C_{1}\right)} \tag{9.33}
\end{equation*}
$$

Equation 9.32 indicates that the dominant-pole magnitude $\left|p_{1}\right|$ decreases as $C$ increases, whereas (9.33) shows that $\left|p_{2}\right|$ increases as $C$ increases. Thus, increasing $C$ causes the poles to split apart. The dominant pole moves to a lower frequency because increasing $C$ increases the time constant associated with the output node of the first stage in Fig. 9.18. The reason the nondominant pole moves to a higher frequency is explained below.

Equation 9.33 can be interpreted physically by associating $p_{2}$ with the output node in Fig. 9.18. Then

$$
\begin{equation*}
p_{2}=-\frac{1}{R_{o} C_{T}} \tag{9.33a}
\end{equation*}
$$

where $R_{o}$ is the output resistance including negative feedback around the second stage through $C$, and $C_{T}$ is the total capacitance from the output node to ground. The output resistance is

$$
\begin{equation*}
R_{o}=\frac{R_{2}}{1+T} \tag{9.33b}
\end{equation*}
$$

where $R_{2}$ is the open-loop output resistance, and $T$ is the loop gain around the second stage through capacitor $C$, which is the open-loop gain, $g_{m} R_{2}$, times the feedback factor, $f$. Therefore,

$$
\begin{equation*}
R_{o}=\frac{R_{2}}{1+g_{m} R_{2} f} \simeq \frac{1}{g_{m} f} \tag{9.33c}
\end{equation*}
$$

assuming that $T=g_{m} R_{2} f \gg 1$. Since $p_{2}$ is a high frequency, we will find $f$ at high frequency $\omega$, where $1 / \omega C_{1} \ll R_{1}$. Then the feedback around the second stage is controlled by a capacitive voltage divider and

$$
\begin{equation*}
f \simeq \frac{C}{C+C_{1}} \tag{9.33d}
\end{equation*}
$$

Thus,

$$
\begin{equation*}
R_{o} \simeq \frac{C+C_{1}}{g_{m} C} \tag{9.33e}
\end{equation*}
$$

The total capacitance from the output node to ground is $C_{2}$ in parallel with the series combination of $C$ and $C_{1}$ :

$$
\begin{equation*}
C_{T}=C_{2}+\frac{C C_{1}}{C+C_{1}}=\frac{C C_{2}+C_{1} C_{2}+C C_{1}}{C+C_{1}} \tag{9.33f}
\end{equation*}
$$

Substituting (9.33e) and (9.33f) into (9.33a) gives (9.33).
Equations 9.33 d and 9.33 f show that increasing $C$ increases the feedback factor but has little effect on the total capacitance in shunt with the output node because $C$ is in series with $C_{1}$. As a result, increasing $C$ reduces the output resistance and increases the frequency of the nondominant pole. In the limit as $C \rightarrow \infty$, the feedback factor approaches unity, and $p_{2} \rightarrow-g_{m} /\left(C_{2}+C_{1}\right)$. In practice, however, (9.33d) shows that the feedback factor is less than unity, which limits the increase in the magnitude of the nondominant pole frequency.
image_name:Figure 9.19
description:The graph in Figure 9.19 is a pole-zero plot presented in the complex plane, specifically the s-plane, where the horizontal axis is labeled as \( \sigma \) (real part) and the vertical axis is labeled as \( j\omega \) (imaginary part). This type of graph is used to analyze the stability and frequency response of a circuit as a parameter \( C \) is varied.

Axes Labels and Units:
- **Horizontal Axis (\( \sigma \))**: Represents the real part of the poles, indicating stability with negative values.
- **Vertical Axis (\( j\omega \))**: Represents the imaginary part of the poles, showing oscillatory behavior.

Overall Behavior and Trends:
- As \( C \) increases from zero, the poles of the circuit move along the real axis. Initially, the poles are located at specific positions determined by the values \(-1/(R_2C_2)\) and \(-1/(R_1C_1)\).
- The poles split and move towards different asymptotic positions as \( C \) becomes very large, indicating changes in the circuit's frequency response.

Key Features and Technical Details:
- **Initial Pole Positions**:
- \(-1/(R_2C_2)\): Initial position of one pole when \( C = 0 \).
- \(-1/(R_1C_1)\): Initial position of the other pole when \( C = 0 \).
- **Asymptotic Pole Positions**: As \( C \rightarrow \infty \), the poles approach the positions:
- \(-g_mC/(C_2C_1 + C(C_2 + C_1))\): Reflects the influence of increasing \( C \).
- \(-1/(g_mR_1R_2C)\): Shows the change in pole position with large \( C \).
- **Pole Splitting**: A key event where the poles diverge from their initial positions, indicating a change in the system's dynamics.

Annotations and Specific Data Points:
- The plot includes annotations such as "Poles split," highlighting the point where the poles begin to separate.
- Specific markers (e.g., squares and crosses) denote the initial and asymptotic positions of the poles.

This graph visually demonstrates how the poles of the circuit shift as the capacitance \( C \) is increased, providing insights into the stability and frequency behavior of the system.

Figure 9.19 Locus of the poles of the circuit of Fig. 9.18 as $C$ is increased from zero, for the case $-1 /\left(R_{1} C_{1}\right)>-1 /\left(R_{2} C_{2}\right)$.

On the other hand, with $C=0$, the poles of the circuit of Fig. 9.18 are

$$
\begin{align*}
& p_{1}=-\frac{1}{R_{1} C_{1}}  \tag{9.34a}\\
& p_{2}=-\frac{1}{R_{2} C_{2}} \tag{9.34b}
\end{align*}
$$

Thus as $C$ increases from zero, the locus of the poles of the circuit of Fig. 9.18 is as shown in Fig. 9.19.

Another explanation of pole splitting is as follows. The circuit in Fig. 9.18 has two poles. The compensation capacitor across the second stage provides feedback and causes the second stage to act like an integrator. The two poles split apart as $C$ increases. One pole moves to a low frequency (toward dc), and the other moves to a high frequency (toward $-\infty$ ) to approximate an ideal integrator, which has only one pole at dc.

The previous calculations have shown how compensation of an amplifier by addition of a large Miller capacitance to a single transistor stage causes the nondominant pole to move to a much higher frequency. For the sake of comparison, consider compensating the circuit in Fig. 9.18 without adding capacitance to $C$ by making $C_{1}$ large enough to produce a dominant pole. Then the pole can be calculated from (9.31) as $p_{1} \simeq-1 / R_{1} C_{1}$. The nondominant pole can be estimated by equating coefficients of $s^{2}$ in (9.27) and (9.30) and using this value of $p_{1}$. This gives $p_{2} \simeq-1 / R_{2}\left(C_{2}+C\right)$. This value of $p_{2}$ is approximately the same as that given by (9.34b), which is for $C=0$ and is before pole splitting occurs. Thus, creation of a dominant pole in the circuit of Fig. 9.18 by making $C_{1}$ large will result in a second pole magnitude $\left|p_{2}\right|$ that is much smaller than that obtained if the dominant pole is created by increasing $C$. As a consequence, the realizable bandwidth of the circuit when compensated in this way is much smaller than that obtained with Miller-effect compensation. Also, without using the Miller effect, the required compensation capacitor often would be too large to be included on a monolithic chip. The same general conclusions are true in the more complex situation that exists in many practical op amps.

The results derived in this section are useful in further illuminating the considerations of Section 7.3.3. In that section, it was stated that in a common-source cascade, the existence of drain-gate capacitance tends to cause pole splitting and to produce a dominant-pole situation. If the equivalent circuit of Fig. 9.18 is taken as a representative section of a cascade of commonsource stages ( $C_{2}$ is the input capacitance of the following stage) and capacitor $C$ is taken as $C_{g d}$, the calculations of this section show that the presence of $C_{g d}$ does, in fact, tend to produce a dominant-pole situation because of the pole splitting that occurs. Thus, the zero-value time constant approach gives a good estimate of $\omega_{-3 \mathrm{~dB}}$ in such circuits.

The theory of compensation that was developed in this chapter was illustrated with some bipolar-transistor circuit examples. The theory applies in general to any active circuit, but the unique device parameters of MOSFETs cause some of the approximations that were made in
the preceding analyses to become invalid. The special aspects of MOS amplifier compensation are now considered.

### 9.4.3 Two-Stage MOS Amplifier Compensation

The basic two-stage CMOS op amp topology shown in Fig. 6.16 is essentially identical to its bipolar counterpart. As a consequence, the equivalent circuit of Fig. 9.18 can be used to represent the second stage with its compensation capacitance. The poles of the circuit are again given by (9.32) and (9.33) and the zero by (9.27a). In the case of the MOS transistor, however, the value of $g_{m}$ is typically an order of magnitude lower than for a bipolar transistor, and the break frequency caused by the right half-plane zero in (9.27) may actually fall below the nominal unity-gain frequency of the amplifier. The effect of this is shown in Fig. 9.20. At the frequency $|z|$ the gain characteristic of the amplifier flattens out because of the contribution to the gain of +6 dB /octave from the zero. In the same region the phase is made $90^{\circ}$ more negative by the positive real zero. As a consequence, the amplifier will have negative phase margin and be unstable when the influence of the next most dominant pole is felt. In effect, the zero halts the gain roll-off intended to stabilize the amplifier and simultaneously pushes the phase in the negative direction. Note also from (9.33) that the low $g_{m}$ of the MOSFET will tend to reduce the value of $\left|p_{2}\right|$ relative to a bipolar amplifier.

Another way to view this problem is to note from Fig. 9.18 that at high frequencies, feedforward through $C$ tends to overwhelm the normal gain path via $g_{m}$ of the second stage
image_name:Figure 9.20 Typical gain and phase of the CMOS op amp of Fig. 6.16.
description:The graph in Figure 9.20 is a Bode plot illustrating the typical gain and phase response of a CMOS operational amplifier as described in the context. The plot consists of two separate graphs: the top one represents the magnitude (gain) in decibels (dB), and the bottom one shows the phase in degrees. Both graphs are plotted against frequency, which is represented on the horizontal axis using a logarithmic scale, denoted by \( \omega \) (log scale).

Magnitude Plot (Top Graph):
- **Vertical Axis**: Represents the magnitude of the gain \( \left| \frac{V_o}{V_i}(j\omega) \right| \) in decibels (dB).
- **Horizontal Axis**: Frequency \( \omega \) on a logarithmic scale.
- **Behavior**:
- The gain starts at a high value and decreases at a rate of \(-6 \text{ dB/octave}\) after the first pole \( |p_1| \).
- At the frequency \( |z| = \frac{g_m}{C} \), there is a noticeable flattening, indicating the presence of a zero that halts the gain roll-off.
- The gain resumes its decline past the second pole \( |p_2| \).
- **Key Points**:
- \( |p_1| \) and \( |p_2| \) are marked as the first and second pole frequencies, respectively.
- \( |z| = \frac{g_m}{C} \) is marked as the zero frequency.

Phase Plot (Bottom Graph):
- **Vertical Axis**: Represents the phase of the gain \( \text{ph} \left( \frac{V_o}{V_i}(j\omega) \right) \) in degrees.
- **Horizontal Axis**: Frequency \( \omega \) on a logarithmic scale.
- **Behavior**:
- The phase starts near 0° and decreases, reaching approximately \(-45°\) at \( |p_1| \).
- The phase continues to decrease beyond the zero \( |z| \), passing through \(-90°\) and \(-135°\) and approaching \(-180°\) after \( |p_2| \).
- **Key Points**:
- The phase plot shows the typical phase lag associated with poles and the phase lead introduced by the zero.

This Bode plot effectively demonstrates the frequency response of a CMOS op amp, highlighting the effects of poles and zeros on both gain and phase.

Figure 9.20 Typical gain and phase of the CMOS op amp of Fig. 6.16.
if $g_{m}$ is small. The feedforward path does not have the $180^{\circ}$ phase shift of the normal gain stage, and thus the gain path loses an inverting stage. Any feedback applied around the overall amplifier will then be positive instead of negative feedback, resulting in oscillation. At very high frequencies, $C$ acts like a short circuit, diode-connecting the second stage, which then simply presents a resistive load of $1 / g_{m}$ to the first stage, again showing the loss of $180^{\circ}$ of phase shift.

The right half-plane (RHP) zero is caused by the interaction of current from the $g_{m}$ generator and the frequency-dependent current that flows forward from the input node to the output node through $C$. The current through $C$ in Fig. 9.18 is

$$
\begin{equation*}
i_{c}=s C\left(v_{o}-v_{1}\right) \tag{9.35}
\end{equation*}
$$

This current can be broken into two parts: a feedback current $i_{f b}=s C v_{o}$ that flows from the output back toward the input and a feedforward current $i_{f f}=s C v_{1}$ that flows forward from the input toward the output. This feedforward current is related to $v_{1}$. The current $g_{m} v_{1}$ from the controlled source flows out of the output node and is also related to $v_{1}$. Subtracting these two currents gives the total current at the output node that is related to $v_{1}$ :

$$
\begin{equation*}
i_{v_{1}}=\left(g_{m}-s C\right) v_{1} \tag{9.36}
\end{equation*}
$$

A zero exists in the transfer function where this current equals zero, at $z=g_{m} / C$.
Three techniques have been used to eliminate the effect of the RHP zero. One approach is to put a source follower in series with the compensation capacitor, ${ }^{9}$ as shown in Fig. 9.21a. The source follower blocks feedforward current through $C$ from reaching the output node and therefore eliminates the zero. This will be shown by analyzing Fig. 9.18 with $C$ replaced by the model in Fig. 9.21b. Here the source follower is modeled as an ideal voltage buffer. Equation 9.25 still holds because the same elements are connected to the input node and the voltage across $C$ remains $v_{o}-v_{1}$. However, summing currents at the output node gives a different equation than (9.26) because no current flows through $C$ to the output node due to the buffer. The new equation is

$$
\begin{equation*}
g_{m} v_{1}+\frac{v_{o}}{R_{2}}+s C_{2} v_{o}=0 \tag{9.37}
\end{equation*}
$$

Combining this equation with (9.25) gives

$$
\begin{equation*}
\frac{v_{o}}{i_{s}}=\frac{g_{m} R_{1} R_{2}}{1+s\left[R_{1}\left(C_{1}+C\right)+R_{2} C_{2}+g_{m} R_{2} R_{1} C\right]+s^{2} R_{1} R_{2} C_{2}\left(C_{1}+C\right)} \tag{9.38}
\end{equation*}
$$

image_name:(a)
description:
[
name: C, type: Capacitor, value: C, ports: {Np: v1, Nn: s1}
name: M1, type: NMOS, ports: {S: s1, D: VDD, G: vo}
name: ID, type: CurrentSource, value: ID, ports: {Np: s1, Nn: VSS}
]
extrainfo:Figure 9.21(a) shows a compensation capacitor C in series with a source follower using an NMOS transistor M1. The circuit includes a voltage source S1 providing VDD and a current source ID with VSS as the negative terminal.
image_name:(b)
description:
[
name: C, type: Capacitor, value: C, ports: {Np: v1, Nn: vo}
name: OpAmp, type: OpAmp, value: X1, ports: {InP: v1, InN: GND, OutP: vo}
]
extrainfo:The circuit diagram (b) shows a capacitor C connected between input v1 and output vo, with an op-amp (X1) configured as a buffer (unity gain amplifier). This configuration isolates the capacitor from the load, preventing any current from flowing through the capacitor to the output node.

Figure 9.21 (a) Compensation capacitor $C$ in Fig. 9.18 is replaced by $C$ in series with a source follower. (b) A simple model for the capacitor and source follower.

The zero has been eliminated. Assuming $g_{m} R_{1}, g_{m} R_{2} \gg 1$ and $C$ is large, the same steps that led from (9.27) to (9.32) and (9.33) give

$$
\begin{align*}
& p_{1} \approx-\frac{1}{g_{m} R_{2} R_{1} C}  \tag{9.39a}\\
& p_{2} \approx-\frac{g_{m} C}{\left(C_{1}+C\right) C_{2}} \approx-\frac{g_{m}}{C_{2}} \tag{9.39b}
\end{align*}
$$

The dominant pole $p_{1}$ is unchanged, and $p_{2}$ is about the same as before if $C_{2} \gg C_{1}$. This approach eliminates the zero, but the follower requires extra devices and bias current. Also, the source follower has a nonzero dc voltage between its input and output. This voltage will affect the output voltage swing since the source-follower transistor must remain in the active region to maintain the desired feedback through $C$.

A second approach to eliminate the RHP zero is to block the feedforward current through $C$ using a common-gate transistor, ${ }^{10}$ as illustrated in Fig. 9.22a. This figure shows a two-stage op amp , with the addition of two current sources of value $I_{2}$ and transistor $M_{11}$. The compensation capacitor is connected from the op-amp output to the source of $M_{11}$. Here, common-gate $M_{11}$ allows capacitor current to flow from the output back toward the input of the second stage. However, the impedance looking into the drain of $M_{11}$ is very large. Therefore, feedforward current through $C$ is very small. If the feedforward current is zero, the RHP zero is eliminated. A simplified small-signal model for the common-gate stage and compensation capacitor is shown in Fig. 9.22b. Here common-gate $M_{11}$ is modeled as an ideal current buffer. Replacing $C$ in Fig. 9.18 with the model in Fig. $9.22 b$ yields

$$
\begin{gather*}
-i_{s}=\frac{v_{1}}{R_{1}}+v_{1} C_{1} s-v_{o} C s  \tag{9.40a}\\
g_{m} v_{1}+\frac{v_{o}}{R_{2}}+v_{o} C s+v_{o} C_{2} s=0 \tag{9.40b}
\end{gather*}
$$

image_name:(a)
description: differential pair formed by PMOS transistors M0 and M1, with NMOS transistors M2 and M3 forming the current mirror load. The output stage consists of PMOS transistor M11 and NMOS transistor M6. Current sources I1, I2, and I3 provide biasing for the circuit.
image_name:(b)
description:The circuit is a two-stage CMOS operational amplifier with a common-gate PMOS transistor M11 connected to a compensation capacitor C. The amplifier is biased with three current sources I1, I2, and I3. The input stage consists of PMOS transistors M0 and M1, and the output stage includes NMOS transistors M6 and a compensation capacitor C connected to the output node Vo.

(b)

Figure 9.22 (a) A two-stage CMOS op amp with common-gate $M_{11}$ connected to compensation capacitor $C$. (b) Simple small-signal model for $M_{11}$ and $C$.

Combining these equations gives

$$
\begin{equation*}
\frac{v_{o}}{i_{s}}=\frac{g_{m} R_{1} R_{2}}{1+s\left[R_{1} C_{1}+R_{2}\left(C+C_{2}\right)+g_{m} R_{1} R_{2} C\right]+s^{2} R_{1} R_{2} C_{1}\left(C_{2}+C\right)} \tag{9.41}
\end{equation*}
$$

The zero has been eliminated. Again assuming $g_{m} R_{1}, g_{m} R_{2} \gg 1$ and $C$ is large, the poles are

$$
\begin{align*}
& p_{1} \approx-\frac{1}{g_{m} R_{2} R_{1} C}  \tag{9.42a}\\
& p_{2} \approx-\frac{g_{m}}{C+C_{2}} \cdot \frac{C}{C_{1}} \tag{9.42b}
\end{align*}
$$

The dominant pole is the same as before. However, the nondominant pole $p_{2}$ is different. This $p_{2}$ is at a higher frequency than in the two previous approaches because $C \gg C_{1}$ when $C$ and $C_{2}$ are comparable. (In this section, we assume that the two-stage MOS op amp in Fig. 9.18 drives a load capacitor $C_{2}$ that is much larger than parasitic capacitance $C_{1}$; therefore $C_{2} \gg C_{1}$.) Therefore, a smaller compensation capacitor $C$ can be used here for a given load capacitance $C_{2}$, when compared to the previous approaches. The increase in $\left|p_{2}\right|$ arises because the input node is not connected to, and therefore is not loaded by, the compensation capacitor. An advantage of this scheme is that it provides better high-frequency negative-power-supply rejection than Miller compensation. (Power-supply rejection was introduced in Section 6.3.6.) With Miller compensation, $C$ is connected from the gate to drain of $M_{6}$, and it shorts the gate and drain at high frequencies. Assuming $V_{g s 6}$ is approximately constant, high-frequency variations on the negative supply are coupled directly to the op-amp output. Connecting $C$ to common-gate $M_{11}$ eliminates this coupling path. Drawbacks of this approach are that extra devices and dc current are needed to implement the scheme in Fig. 9.22a. Also, if there is a mismatch between the $I_{2}$ current sources, the difference current must flow in the input stage, which disrupts the balance in the input stage and affects the input-offset voltage of the op amp.

When the first stage of the op amp uses a cascode transistor, the compensation capacitor can be connected to the source of the cascode device as shown in Fig. 9.23. ${ }^{11}$ This connection reduces the feedforward current through $C$, when compared to connecting $C$ to node $(8)$, if the
image_name:Figure 9.23
description:The circuit is a two-stage CMOS op amp with a cascoded current-mirror load in the input stage. The compensation capacitor C is connected to the cascode node Y. The input stage uses a cascode transistor configuration to improve gain and bandwidth. The compensation technique reduces the feedforward current through C, enhancing stability.
Figure 9.23 A two-stage CMOS op amp with a cascoded current-mirror load in the input stage, and with the compensation capacitor $C$ connected to the cascode node.

image_name:(a)
description:
[
name: is, type: CurrentSource, value: is, ports: {Np: VI, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: VI, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: VI, Nn: GND}
name: RZ, type: Resistor, value: RZ, ports: {N1: VI, N2: X1}
name: C, type: Capacitor, value: C, ports: {Np: X1, Nn: VO}
name: gmV1, type: CurrentSource, ports: {Np: VO, Nn: GND}
name: R2, type: Resistor, value: R2, ports: {N1: VO, N2: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: VO, Nn: GND}
]
extrainfo:The circuit is a two-stage CMOS op amp with a cascoded current-mirror load in the input stage, using a compensation technique to enhance stability by reducing feedforward current through the capacitor C.
image_name:(b)
description:The graph in Figure 9.24(b) is a pole-zero diagram plotted on the complex s-plane, which is used to illustrate the behavior of a system's transfer function as the nulling resistor $R_{Z}$ varies.

1. **Type of Graph and Function:**
- This is a pole-zero diagram, a common tool in control theory and signal processing to analyze the stability and frequency response of systems.

2. **Axes Labels and Units:**
- The horizontal axis represents the real part of the complex frequency, denoted as $\sigma$.
- The vertical axis represents the imaginary part of the complex frequency, denoted as $j\omega$.
- There are no specific units marked, as it is a conceptual representation.

3. **Overall Behavior and Trends:**
- The diagram shows how the transmission zero moves in the s-plane as the value of $R_{Z}$ increases.
- Starting from the rightmost zero at $R_{Z} = 0$, the zero moves along a curved path towards the left as $R_{Z}$ increases.
- The path is indicated by an arrow, suggesting the direction of movement with increasing $R_{Z}$.

4. **Key Features and Technical Details:**
- The zero starts at the real axis when $R_{Z} = 0$ and moves leftward.
- There is a marked point where $R_{Z} > \frac{1}{g_m}$, indicating a critical value of $R_{Z}$ that affects the system's dynamics.
- The movement of the zero can significantly affect the stability and frequency response of the op-amp circuit by modifying the phase and gain margins.

5. **Annotations and Specific Data Points:**
- The diagram includes annotations such as $R_{Z} = 0$ and $R_{Z} > \frac{1}{g_m}$ to highlight significant positions of the zero.
- The path of the zero is marked with a dashed curve and directional arrows, illustrating the trajectory as $R_{Z}$ increases.

This diagram is essential for understanding how varying the nulling resistor $R_{Z}$ in the compensation stage affects the transmission zero, which in turn influences the stability and performance of the op-amp circuit.

Figure 9.24 (a) Small-signal equivalent circuit of a compensation stage with nulling resistor. (b) Pole-zero diagram showing movement of the transmission zero for various values of $R_{Z}$.
voltage swing at the source of the cascode device is smaller than the swing at its drain. This approach eliminates the feedforward path, and therefore the zero, if the voltage swing at the source of the cascode device is zero. An advantage of this approach is that it avoids the extra devices, bias current, and mismatch problems in Fig. 9.22a.

A third way to deal with the RHP zero is to insert a resistor in series with the compensation capacitor, as shown in Fig. 9.24a. ${ }^{12,13}$ Rather than eliminate the feedforward current, the resistor modifies this current and allows the zero to be moved to infinity. If the zero moves to infinity, the total forward current at the output node that is related to $v_{1}$ must go to zero when $\omega \rightarrow \infty$. When $\omega \rightarrow \infty$, capacitor $C$ is a short circuit and therefore the feedforward current is only due to $R_{Z}$ :

$$
\begin{equation*}
i_{f f}(\omega \rightarrow \infty)=-\frac{v_{1}}{R_{Z}} \tag{9.43}
\end{equation*}
$$

When this current is added to the current from the $g_{m}$ source, the total current at the output node that is related to $v_{1}$ is

$$
\begin{equation*}
i_{v_{1}}=\left(g_{m}-\frac{1}{R_{Z}}\right) v_{1} \tag{9.44}
\end{equation*}
$$

when $\omega \rightarrow \infty$. If $R_{Z}=1 / g_{m}$, this term vanishes, and the zero is at infinity.
The complete transfer function can be found by carrying out an analysis similar to that performed for Fig. 9.18, which gives

$$
\begin{equation*}
\frac{v_{o}}{i_{s}}=\frac{g_{m} R_{1} R_{2}\left[1-s C\left(\frac{1}{g_{m}}-R_{Z}\right)\right]}{1+b s+c s^{2}+d s^{3}} \tag{9.45}
\end{equation*}
$$

where

$$
\begin{align*}
& b=R_{2}\left(C_{2}+C\right)+R_{1}\left(C_{1}+C\right)+R_{Z} C+g_{m} R_{1} R_{2} C  \tag{9.46a}\\
& c=R_{1} R_{2}\left(C_{1} C_{2}+C C_{1}+C C_{2}\right)+R_{Z} C\left(R_{1} C_{1}+R_{2} C_{2}\right)  \tag{9.46b}\\
& d=R_{1} R_{2} R_{Z} C_{1} C_{2} C \tag{9.46c}
\end{align*}
$$

Again assuming $g_{m} R_{1}, g_{m} R_{2} \gg 1$ and $C$ is large, the poles can be approximated by

$$
\begin{align*}
& p_{1} \approx-\frac{1}{g_{m} R_{2} R_{1} C}  \tag{9.47a}\\
& p_{2} \approx-\frac{g_{m} C}{C_{1} C_{2}+C\left(C_{1}+C_{2}\right)} \approx-\frac{g_{m}}{C_{1}+C_{2}}  \tag{9.47b}\\
& p_{3} \approx-\frac{1}{R_{Z} C_{1}} \tag{9.47c}
\end{align*}
$$

The first two poles, $p_{1}$ and $p_{2}$, are the same as for the original circuit in Fig. 9.18. The third pole is at a very high frequency with $\left|p_{3}\right| \gg\left|p_{2}\right|$ because typically $C_{1} \ll C_{2}$ (since $C_{1}$ is a small parasitic capacitor and $C_{2}$ is the load capacitor) and $R_{Z}$ will be about equal to $1 / g_{m}$ if the zero is moved to a high frequency [from (9.44)]. This circuit has three poles because there are three independent capacitors. In contrast, Fig. 9.18 has three capacitors that form a loop, so only two of the capacitor voltages are independent. Thus there are only two poles associated with that circuit.

The zero of (9.45) is

$$
\begin{equation*}
z=\frac{1}{\left(\frac{1}{g_{m}}-R_{Z}\right) C} \tag{9.48}
\end{equation*}
$$

This zero moves to infinity when $R_{Z}$ equals $1 / g_{m}$. Making the resistor greater than $1 / g_{m}$ moves the zero into the left half-plane, which can be used to provide positive phase shift at high frequencies and improve the phase margin of a feedback circuit that uses this op amp. ${ }^{13}$ The movement of the zero for increasing $R_{Z}$ is shown in Fig. 9.24b.

Figure 9.25 shows a Miller-compensated op amp using a resistor $R_{Z}$ in series with the compensation capacitor. In practice, resistor $R_{Z}$ is usually implemented using a MOS transistor
image_name:Figure 9.25
description:The circuit is a two-stage CMOS op amp with Miller compensation using a resistor RZ in series with the compensation capacitor CL. It features a differential input stage (M1, M2, M3, M4) and a gain stage (M5, M6). The output is taken at node Vo. The circuit is powered by VDD and VSS.

Figure 9.25 A two-stage CMOS op amp.
biased in the triode region. From (1.152), a MOS transistor operating in the triode region behaves like a linear resistor if $V_{d s} \ll 2\left(V_{G S}-V_{t}\right)$. The on-resistance $R_{Z}$ of the triode device can be made to track $1 / g_{m}$ of common-source transistor $M_{6}$ if the two transistors are identical and have the same $V_{G S}-V_{t}$. When this MOS transistor is placed to the left of the compensation capacitor as shown in Fig. 9.25 , its source voltage is set by $V_{g s 6}$, which is approximately constant. Therefore, $V_{G S}$ of the triode transistor can be set by connecting its gate to a dc bias voltage, which can be generated using replica biasing. ${ }^{13}$ (See Problem 9.23.)

Another way to shift the zero location that can be used in multistage op amps will be presented in Section 9.4.5.

In all the compensation approaches described so far, the dominant pole is set by compensation capacitor $C$ and is independent of the load capacitor $C_{2}$. However, the second pole is a function of $C_{2}$. If the op amp will be used in different applications with a range of load capacitors, the compensation capacitor should be selected to give an acceptable phase margin for the largest $C_{2}$. Then the phase margin will increase as the load capacitor decreases because $\left|p_{2}\right|$ is inversely proportional to $C_{2}$.

#### EXAMPLE

Compensate the two-stage CMOS op amp from the example in Section 6.3.5 (Fig. 6.16) to achieve a phase margin of $45^{\circ}$ or larger when driving a load capacitance of 5 pF , assuming the op amp is connected in unity-gain feedback.

With the op amp in unity-gain feedback, $f=1$ and the loop gain $T=a f=a$ (or, equivalently, $A_{\infty}=1$ and the return ratio $\mathscr{R}=a$ ). Therefore, the phase and gain margins can be determined from Bode plots of $|a|$ and $\mathrm{ph}(a)$.

The two-stage op amp and a simplified model for this op amp are shown in Fig. 9.25. In the model, all capacitances that connect to node $\otimes$ are lumped into $C_{1}$, and all capacitances that connect to the output node are lumped into $C_{2}$. If we apply an input voltage $v_{i}$ in Fig. 9.26, a current $i_{1}=g_{m 1} v_{i}$ is generated. This $i_{1}$ drives a circuit that is the same as the circuit that $i_{s}$ drives in Fig. 9.18. Therefore, the equations for the two poles and one zero for the circuit in Fig. 9.18 apply here with $i_{s}=g_{m 1} v_{i}, g_{m}=g_{m 6}, R_{1}=r_{o 2} \| r_{o 4}$, and $R_{2}=r_{o 6} \| r_{o 7}$.

We will use Miller compensation with a series resistance to eliminate the zero. To achieve a $45^{\circ}$ phase margin, the compensation capacitor $C$ should be chosen so that $\left|p_{2}\right|$ equals the unity-gain frequency (assuming the zero has been eliminated and $\left|p_{3}\right| \gg\left|p_{2}\right|$ ). Since the gain roll-off from $\left|p_{1}\right|$ to $\left|p_{2}\right|$ is $-6 \mathrm{~dB} /$ octave, $|a(j \omega)| \cdot \omega$ is constant from $\left|p_{1}\right|$ to $\left|p_{2}\right|$. Therefore,

$$
\begin{equation*}
a_{o} \cdot\left|p_{1}\right|=1 \cdot\left|p_{2}\right| \tag{9.49}
\end{equation*}
$$

where

$$
\begin{equation*}
a_{o}=g_{m 1}\left(r_{o 2} \| r_{o 4}\right) g_{m 6}\left(r_{o 6} \| r_{o 7}\right)=g_{m 1} R_{1} g_{m 6} R_{2} \tag{9.50}
\end{equation*}
$$

image_name:Figure 9.26
description:
[
name: Cin, type: Capacitor, value: Cin, ports: {Np: Vi, Nn: vx}
name: gm1vi, type: VoltageControlledCurrentSource, ports: {Np: vx, Nn: GND}
name: R1, type: Resistor, value: ro2||ro4, ports: {N1: vx, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: vx, Nn: GND}
name: Rz, type: Resistor, value: Rz, ports: {N1: vx, N2: x1}
name: C, type: Capacitor, value: C, ports: {Np: x1, Nn: vo}
name: gm6vx, type: VoltageControlledCurrentSource, ports: {Np: vo, Nn: GND}
name: R2, type: Resistor, value: ro6||ro7, ports: {N1: vo, N2: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: vo, Nn: GND}
]
extrainfo:The circuit is a small-signal model of an operational amplifier. It includes voltage-controlled current sources representing transconductance amplifiers and passive components that form part of the feedback and compensation network. The input is at node Vi, and the output is at node Vo. The circuit is designed to analyze the frequency response and gain characteristics of the op amp.

Figure 9.26 A small-signal model for the op amp in Fig. 9.25.
is the dc gain of the op amp. Substitution of (9.47) and (9.50) into (9.49) gives

$$
g_{m 1} R_{1} g_{m 6} R_{2} \cdot \frac{1}{g_{m 6} R_{2} R_{1} C}=1 \cdot \frac{g_{m 6}}{C_{1}+C_{2}}
$$

or

$$
\begin{equation*}
\frac{g_{m 1}}{C}=\frac{g_{m 6}}{C_{1}+C_{2}} \tag{9.51}
\end{equation*}
$$

The capacitance $C_{2}$ at the output is dominated by the $5-\mathrm{pF}$ load capacitance, and the internal parasitic capacitance $C_{1}$ is much smaller than 5 pF (SPICE simulation gives $C_{1} \approx 120 \mathrm{fF}$ ). Therefore $C_{1}+C_{2} \approx 5 \mathrm{pF}$. From the example in Section 6.3.5, we find

$$
g_{m 1}=k_{p}^{\prime}(W / L)_{1}\left|V_{o v 1}\right|=\left(64.7 \mu \mathrm{~A} / \mathrm{V}^{2}\right)(77)(0.2 \mathrm{~V})=1 \mathrm{~mA} / \mathrm{V}
$$

and

$$
g_{m 6}=k_{n}^{\prime}(W / L)_{6}\left(V_{o v 6}\right)=\left(194 \mu \mathrm{~A} / \mathrm{V}^{2}\right)(16)(0.5 \mathrm{~V})=1.55 \mathrm{~mA} / \mathrm{V}
$$

Substituting these values into (9.51) and rearranging gives

$$
C=\frac{g_{m 1}}{g_{m 6}}\left(C_{1}+C_{2}\right) \approx \frac{1 \mathrm{~mA} / \mathrm{V}}{1.55 \mathrm{~mA} / \mathrm{V}}(5 \mathrm{pF})=3.2 \mathrm{pF}
$$

To eliminate the zero due to feedforward through $C$, a resistor $R_{Z}$ of value $1 / g_{m 6}=645 \Omega$ can be connected in series with the compensation capacitor $C$. (In practice, this resistance should be implemented with an NMOS transistor that is a copy of $M_{6}$ biased in the triode region, so that $R_{Z}=1 / g_{m 6}$. See Problem 9.23.)

SPICE simulations (using models based on Table 2.4) of the op amp before and after compensation give the magnitude and phase plots shown in Fig. 9.27. Before compensation, the amplifier is unstable and has a phase margin of $-6^{\circ}$. After compensation with $R_{Z}=645 \Omega$ and $C=3.2 \mathrm{pF}$ the phase margin improves to $41^{\circ}$ with a unity-gain frequency of 35 MHz , and the gain margin is 15 dB . This phase margin is less than the desired $45^{\circ}$. The simulated value of $g_{m 6}$ is $1.32 \mathrm{~mA} / \mathrm{V}$ and differs somewhat from the calculated $g_{m 6}$, because the formulas used to calculate $g_{m}$ are based on square-law equations that are only approximately correct. Changing $R_{Z}$ to $1 / g_{m 6}($ SPICE $)=758 \Omega$ gives a phase margin of $46^{\circ}$ with a unity-gain frequency of 35 MHz , and the gain margin is 22 dB . Without $R_{Z}$, the phase margin is $14^{\circ}$, so eliminating the right-half-plane zero significantly improves the phase margin.

Two earlier assumptions can be checked from SPICE simulations. First, $C_{1} \approx 120 \mathrm{fF}$ from SPICE and $C_{2} \approx 5 \mathrm{pF}$; therefore, the assumption that $C_{1} \ll C_{2}$ is valid. Also, $\left|p_{3}\right| \gg\left|p_{2}\right|$ follows from $\left|p_{3}\right| \approx 1 /\left(R_{Z} C_{1}\right)=g_{m 6} / C_{1},\left|p_{2}\right| \approx g_{m 6} / C_{2}$, and $C_{1} \ll C_{2}$.

### 9.4.4 Compensation of Single-Stage CMOS Op Amps

Single-stage op amps, such as the telescopic cascode or folded cascode, have only one gain stage; therefore Miller compensation is not possible. These op amps have high open-loop output resistance and are typically used in switched-capacitor circuits, where the load is purely capacitive. Therefore, the dominant pole is associated with the output node, and the load capacitor provides the compensation.

A simplified, fully differential, telescopic-cascode op amp is shown in Fig. 9.28a. The simplifications here are that ideal current sources replace biasing transistors and all capacitances have been lumped into the load capacitors $C_{L}$ and the parasitic capacitors $C_{p}$ at the cascode nodes. The differential-mode (DM) voltage gain can be found by analyzing the half-circuit shown in Fig. 9.28b. Since there are two independent capacitors, the DM gain has two poles.
image_name:(a)
description:The graph in Figure 9.27(a) is a Bode plot, which consists of two parts: the magnitude plot and the phase plot of the operational amplifier (op-amp) gain before and after compensation.

**Magnitude Plot:**
- **Axes:**
- The x-axis represents frequency in Hertz (Hz), ranging from 100 Hz to 1 GHz. The scale is logarithmic.
- The y-axis represents the magnitude of the gain (|a|), ranging from 0.01 to 10,000 on a logarithmic scale.
- **Behavior and Trends:**
- Before compensation (C=0), the gain starts at a high value around 10,000 at low frequencies and decreases steadily as frequency increases, crossing the unity gain (|a|=1) around 100 MHz.
- After compensation, the gain starts at the same initial value but decreases more gradually, crossing the unity gain at a lower frequency, around 10 MHz.
- **Key Features:**
- The compensation shifts the -3 dB point to a lower frequency, indicating increased stability and bandwidth.

**Phase Plot:**
- **Axes:**
- The x-axis is the same as the magnitude plot, representing frequency in Hertz (Hz) on a logarithmic scale.
- The y-axis represents phase in degrees, ranging from 0° to -270°.
- **Behavior and Trends:**
- Before compensation, the phase starts at 0° and decreases, reaching approximately -180° around 100 MHz.
- After compensation, the phase decreases more gradually, reaching -180° at a lower frequency, around 10 MHz.
- **Key Features:**
- The phase margin is improved after compensation, indicating enhanced stability.

**Annotations and Specific Data Points:**
- The plots are annotated with labels 'Before comp. (C=0)' and 'After comp.', showing the effects of compensation on both magnitude and phase.
- The dashed line at |a|=1 in the magnitude plot and at -180° in the phase plot serve as reference lines for unity gain and phase shift, respectively.
image_name:(b)
description:The graph labeled (b) is a Bode plot displaying the phase response of an operational amplifier (op-amp) gain both before and after compensation. The x-axis represents frequency in Hertz (Hz), ranging from 100 Hz to 1 GHz, on a logarithmic scale. The y-axis represents the phase shift in degrees, ranging from 0° to -270°.

Overall Behavior and Trends:
- **Before Compensation:** The phase starts at 0° and begins to decrease around 10 kHz. It reaches approximately -90° at around 1 MHz, and continues to decrease, approaching -180° near 100 MHz. The phase further decreases towards -270° as the frequency approaches 1 GHz.
- **After Compensation:** The phase response also starts at 0° but begins to decrease at a lower frequency compared to the uncompensated case. It reaches -90° at a lower frequency, around 100 kHz, and approaches -180° near 10 MHz. The compensated phase response stabilizes more quickly than the uncompensated one.

Key Features and Technical Details:
- The compensation shifts the phase response to stabilize it earlier in the frequency range, which is indicated by a more gradual slope compared to the uncompensated case.
- The phase margin is improved with compensation, as seen by the earlier stabilization of the phase angle.

Annotations and Specific Data Points:
- The graph includes annotations for 'Before comp. (C = 0)' and 'After comp.' to distinguish between the two responses.
- A dashed horizontal line is present at -180°, indicating the critical phase shift where stability is often evaluated in control systems and feedback loops.

(b)

Figure 9.27 Plots of the simulated (a) magnitude and (b) phase of the op-amp gain before and after compensation ( $C=3.2 \mathrm{pF}, R_{Z}=645 \Omega$ ) for the op amp in Fig. 9.25.

An exact analysis, ignoring body effect, gives a DM gain of

$$
\begin{equation*}
\frac{v_{o d}}{v_{i d}}=-\frac{g_{m 1} r_{o 1}\left(g_{m 1 A} r_{o 1 A}+1\right)}{1+s\left(r_{o 1 A} C_{L}+r_{o 1} C_{p}+r_{o 1} C_{L}+g_{m 1 A} r_{o 1 A} r_{o 1} C_{L}\right)+s^{2} r_{o 1} r_{o 1 A} C_{p} C_{L}} \tag{9.52}
\end{equation*}
$$

If $g_{m} r_{o} \gg 1,(9.52)$ simplifies to

$$
\begin{equation*}
\frac{v_{o d}}{v_{i d}}=-\frac{g_{m 1} r_{o 1} g_{m 1 A} r_{o 1 A}}{1+s g_{m 1 A} r_{o 1 A} r_{o 1} C_{L}+s^{2} r_{o 1} r_{o 1 A} C_{p} C_{L}} \tag{9.53}
\end{equation*}
$$

The gain has two poles and no zeros. Assuming widely spaced real poles, the poles can be approximated using (9.29) and (9.30):

$$
\begin{align*}
& p_{1} \approx-\frac{1}{g_{m 1 A} r_{o 1 A} r_{o 1} C_{L}} \approx-\frac{1}{R_{o} C_{L}}  \tag{9.54a}\\
& p_{2} \approx-\frac{g_{m 1 A}}{C_{p}} \tag{9.54b}
\end{align*}
$$

image_name:(a)
description:
[
name: M1A, type: NMOS, ports: {S: d1S1A, D: Vout+, G: VBB}
name: M1, type: NMOS, ports: {S: S1S2, D: d1S1A, G: in+}
name: M2A, type: NMOS, ports: {S: d2S2A, D: Vout-, G: VBB}
name: M2, type: NMOS, ports: {S: S1S2, D: d2S2A, G: in-}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout+, Nn: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout-, Nn: GND}
name: Cp, type: Capacitor, value: Cp, ports: {Np: d1S1A, Nn: GND}
name: Cp, type: Capacitor, value: Cp, ports: {Np: d2S2A, Nn: GND}
name: I, type: CurrentSource, value: I, ports: {Np: VDD, Nn: Vout+}
name: I, type: CurrentSource, value: I, ports: {Np: VDD, Nn: Vout-}
name: 2I, type: CurrentSource, value: 2I, ports: {Np: S1S2, Nn: VSS}
]
extrainfo:The circuit is a simplified CMOS telescopic-cascode operational amplifier. It consists of two differential pairs with NMOS transistors M1A, M1 and M2A, M2. The circuit uses capacitors CL and Cp for load and compensation, respectively. The current sources I and 2I provide biasing and operation currents. The op-amp is designed to amplify the differential input signals in+ and in-.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1s1A, G: Vid/2}
name: M1A, type: NMOS, ports: {S: d1s1A, D: Vod/2, G: VBB}
name: CL, type: Capacitor, value: CL, ports: {Np: Vod/2, Nn: GND}
name: Cp, type: Capacitor, value: Cp, ports: {Np: d1s1A, Nn: GND}
]
extrainfo:The circuit diagram is a differential-mode half-circuit of a CMOS telescopic-cascode op amp. It includes NMOS transistors M1 and M1A, and capacitors CL and Cp. The circuit is biased with a voltage VBB and has an input Vid/2. The output is taken across CL.
Figure 9.28 (a) Simplified CMOS telescopic-cascode op amp. (b) The differential-mode half-circuit.
where $R_{o}$ is the output resistance of the DM half-circuit and $R_{o} \approx g_{m 1 A} r_{o 1 A} r_{o 1}$. Alternatively, these poles can be estimated using time-constant analysis as shown in Chapter 7. The dominant pole is set by the zero-value time constant for $C_{L}$, which is computed with $C_{p}$ open and equals $R_{O} C_{L}$. The nondominant pole can be approximated using the short-circuit time constant for $C_{p}$, which is computed with $C_{L}$ shorted. When $C_{L}$ is shorted, the resistance seen by $C_{p}$ is the resistance looking into the source of $M_{1 A}$, which is $1 / g_{m 1 A}$ (ignoring body effect). Typically, $\left|p_{1}\right| \ll\left|p_{2}\right|$ because $R_{o} \gg 1 / g_{m 1 A}$ and $C_{L} \gg C_{p}$. If the phase margin is not large enough for a given feedback application, additional capacitance can be added at the output node to increase $C_{L}$, which decreases $\left|p_{1}\right|$ without affecting $p_{2}$ and therefore increases the phase margin.

Capacitance $C_{p}$ consists of $C_{g s 1 A}$ plus smaller capacitances such as $C_{d b 1}$ and $C_{s b 1 A}$. Assuming $C_{p} \approx C_{g s 1 A}$, then $\left|p_{2}\right| \approx g_{m 1 A} / C_{p} \approx g_{m 1 A} / C_{g s 1 A} \approx \omega_{T}$ of $M_{1 A}$. Thus, the frequency at which the magnitude of the op-amp gain equals one, which is called the unity-gain bandwidth, can be very high with this op amp.

A simplified, fully differential, folded-cascode op amp is shown in Fig. 9.29a. As above, the simplifications are that ideal current sources replace biasing transistors and all capacitances have been lumped into the load capacitors $C_{L}$ and the parasitic capacitors $C_{p}^{\prime}$ at the cascode nodes. With these simplifications, the DM voltage gain can be found by analyzing the halfcircuit shown in Fig. 9.29b. This circuit is identical to Fig. 9.28b except that the cascode device is $p$-channel rather than $n$-channel and $C_{p}^{\prime}$ replaces $C_{p}$. Therefore, the gain is identical to (9.52)
image_name:Figure 9.29 (a)
description:This is a simplified CMOS folded-cascode operational amplifier with differential inputs and outputs. The circuit includes NMOS and PMOS transistors, load capacitors CL, and parasitic capacitors C'p at the cascode nodes. Current sources provide biasing currents.
image_name:Figure 9.29 (b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1s1A, G: vid/2}
name: M1A, type: PMOS, ports: {S: d1s1A, D: vod/2, G: GND}
name: "Cp", type: Capacitor, value: "Cp", ports: {Np: d1s1A, Nn: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: vod/2, Nn: GND}
]
extrainfo:The circuit is a differential-mode half-circuit of a CMOS folded-cascode op amp, focusing on the left half with NMOS and PMOS transistors and capacitors C'p and CL.

with $C_{p}$ replaced by $C_{p}^{\prime}$. Hence the dominant pole has the same form as (9.54a)

$$
\begin{equation*}
p_{1} \approx-\frac{1}{g_{m 1 A} r_{o 1 A} r_{o 1} C_{L}} \approx-\frac{1}{R_{o} C_{L}} \tag{9.55a}
\end{equation*}
$$

The second pole is associated with $C_{p}^{\prime}$ and is approximately given by

$$
\begin{equation*}
p_{2} \approx-\frac{g_{m 1 A}}{C_{p}^{\prime}} \tag{9.55b}
\end{equation*}
$$

Equations 9.55 b and 9.54 b look similar, but $\left|p_{2}\right|$ for the folded-cascode op amp will usually be smaller than $\left|p_{2}\right|$ for the telescopic-cascode op amp. The reason is that, while the transconductances of the cascode devices in the two circuits are often comparable, $C_{p}^{\prime}$ will be significantly larger than $C_{p}$. One cause of the higher capacitance is that more devices are connected to the node associated with $C_{p}^{\prime}$ in the folded-cascode op amp than are connected to the node associated with $C_{p}$ in the telescopic cascode. (Recall that the output of each ideal current source in Fig. 9.29a is the drain of a transistor.) Also, $W / L$ of the $p$-channel cascode transistor $M_{1 A}$ in Fig. $9.29 b$ must be larger than $W / L$ of the $n$-channel cascode device in Fig. $9.28 b$ to make their transconductances comparable. The larger $W / L$ will cause $C_{p}^{\prime}$ to be larger than $C_{p}$. The smaller $\left|p_{2}\right|$ for the folded cascode leads to a smaller unity-gain bandwidth, if the two op amps are compensated to give the same phase margin in a given feedback application.

The circuits in Figs. 9.28 and 9.29 are fully differential. These op amps can be converted to single-ended op amps by replacing a pair of matched current sources with a current mirror. In Fig. 9.28a, the two $I$ current sources would be replaced with a $p$-channel current mirror. In

Fig. $9.29 a$, the two $I_{2}$ current sources would be replaced with a $n$-channel current mirror. As shown in Section 7.3.5, a current mirror introduces a closely spaced pole-zero pair, in addition to the poles $p_{1}$ and $p_{2}$ in (9.54) and (9.55).

Active cascodes can be used to increase the low-frequency gain of an op amp, as shown in Fig. 6.30a. There are four active cascodes in Fig. 6.30a; each consists of a cascode transistor $\left(M_{1 A}-M_{4 A}\right)$ and an auxiliary amplifier $\left(A_{1}\right.$ or $\left.A_{2}\right)$ in a feedback loop. When such an op amp is placed in feedback, multiple feedback loops are present. There are four local feedback loops associated with the active cascodes in the op amp and one global feedback loop that consists of the op amp and a feedback network around the op amp. All these feedback loops must be stable to avoid oscillation. The stability of each local feedback loop can be determined from its loop gain or return ratio. Since the auxiliary amplifiers in these loops are op amps, each auxiliary amplifier can be compensated using the techniques described in this chapter to ensure stability of these local loops. Then the global feedback loop can be compensated to guarantee its stability.

### 9.4.5 Nested Miller Compensation

Many feedback circuits require an op amp with a high voltage gain. While cascoding is commonly used to increase the gain in op amps with a total supply voltage of 5 V or more, cascoding becomes increasingly difficult as the power-supply voltage is reduced. (See Chapter 4.) To overcome this problem, simple gain stages without cascoding can be cascaded to achieve high gain. When three or more voltage-gain stages must be cascaded to achieve the desired gain, the op amp will have three or more poles, and frequency compensation becomes complicated. Nested Miller compensation can be used with more than two gain stages. ${ }^{14,15}$ This compensation scheme involves repeated, nested application of Miller compensation. An example of nested Miller compensation applied to three cascaded gain stages is shown in Fig. $9.30 a$. Two noninverting gain stages are followed by an inverting gain stage. Each voltage-gain stage is assumed to have a high-output resistance and therefore is labeled as a $g_{m}$ block. The sign of the dc voltage gain of each stage is given by the sign of the transconductance. Two Miller compensation capacitors are used: $C_{m 1}$, which is placed around the last gain stage, and $C_{m 2}$, which is connected across the last two gain stages. Because the dc gain of the second stage is positive and the dc gain of the third stage is negative, both capacitors are in negative feedback loops.

A simplified circuit schematic is shown in Fig. 9.30b. Each noninverting gain stage is composed of a differential pair with a current-source load. The inverting gain stage consists of a common-source amplifier with a current-source load. A simplified small-signal model is shown in Fig. 9.30c. The main simplification here is that all capacitances associated with the gain stages are modeled by $C_{0}, C_{1}$, and $C_{2}$.

Without the compensation capacitors, this amplifier has three real poles that are not widely spaced if the $R_{i} C_{i}$ time constants are comparable. When $C_{m 1}$ is added, the two poles associated with the output nodes of the second and third stages split apart along the real axis due to the Miller compensation, but the pole associated with output of the first stage does not change. From a design standpoint, the goal of this pole splitting is to cause one pole to dominate the frequency response of the second and third stages together. Assume at first that this goal is met. Then adding $C_{m 2}$ across the second and third stages is similar to adding $C_{m 1}$ across the third stage. Pole splitting occurs again, and the pole associated with the output node of the first stage becomes dominant because the Miller-multiplied $C_{m 2}$ loads this node. Meanwhile, the pole associated with the output of the second stage moves to higher frequency because of negative feedback through $C_{m 2}$. The polarity of this feedback does not become positive at any frequency where the gain around the loop is at least unity because the frequency response of of the second and third stages is dominated by one pole.
image_name:(a)
description:The block diagram labeled as Figure 9.30 (a) represents a three-stage operational amplifier (op amp) with nested Miller compensation. The main components of this system include three amplifier stages and two compensation capacitors.

1. **Main Components:**
- **Amplifiers:** There are three amplifiers in series denoted by their transconductance values: \( +g_{m0} \), \( +g_{m1} \), and \( -g_{m2} \). These amplifiers are responsible for amplifying the input signal \( V_{in} \) and processing it through the stages.
- **Compensation Capacitors:** Two capacitors, \( C_{m1} \) and \( C_{m2} \), are used for Miller compensation to stabilize the op amp and control the frequency response.

2. **Flow of Information or Control:**
- The input signal \( V_{in} \) is fed into the first amplifier with a transconductance of \( +g_{m0} \). The output of this stage is \( V_{o1} \).
- The signal then flows to the second amplifier \( +g_{m1} \), producing an output \( V_{o2} \).
- The third stage is an inverting amplifier \( -g_{m2} \), which outputs \( V_o \).
- The capacitor \( C_{m2} \) provides feedback from the output \( V_o \) to the first stage, introducing a dominant pole that stabilizes the op amp.
- The capacitor \( C_{m1} \) connects the output \( V_o \) of the third stage back to the second stage output \( V_{o2} \), further contributing to the compensation.

3. **Labels, Annotations, and Key Indicators:**
- Each amplifier block is labeled with its corresponding transconductance value \( g_{m0} \), \( g_{m1} \), and \( g_{m2} \).
- The capacitors \( C_{m1} \) and \( C_{m2} \) are clearly marked, indicating their role in the feedback and compensation network.
- The input and output nodes are labeled as \( V_{in} \) and \( V_o \), respectively.

4. **Overall System Function:**
- This block diagram illustrates a three-stage op amp designed to achieve high gain and stability through nested Miller compensation. The arrangement of amplifiers and feedback capacitors ensures that the frequency response is dominated by a single pole, improving stability. The feedback through \( C_{m2} \) and \( C_{m1} \) helps to manage the pole-zero placement, crucial for maintaining the desired performance of the op amp across different frequencies.
image_name:(b)
description:The circuit is a three-stage op amp with nested Miller compensation. It includes NMOS transistors M0 to M4, current sources I1 to I3, and capacitors Cm1 and Cm2 for compensation. The op amp stages are connected to provide negative feedback and stabilize the output. The circuit is designed to control the pole and zero locations for improved frequency response.
image_name:(c)
description:he circuit represents a three-stage operational amplifier with nested Miller compensation. It employs capacitors Cm1 and Cm2 for frequency compensation, shifting poles and introducing zeros for stability. The stages are connected through resistors and capacitors, with a voltage source providing input. The op-amps are configured with positive and negative gain stages to achieve the desired frequency response.

Figure 9.30 (a) Block diagram for a three-stage op amp with nested Miller compensation. (b) A simplified schematic for such an op amp in CMOS. (c) A small-signal model.

In practice, the exact movement of the poles is complicated by the nondominant pole in the feedback loop though $C_{m 2}$. Also, zeros are introduced by feedforward through $C_{m 1}$ and $C_{m 2}$. The pole and zero locations can be found from an exact analysis of the small-signal circuit. The analysis can be carried out by summing currents at the outputs of the $g_{m}$ generators, then manipulating the resulting three equations. These steps are not conceptually difficult but are not shown here. The exact transfer function from the output of the current generator in the input stage, $i_{s}=g_{m 0} v_{\mathrm{in}}$, to the output voltage $v_{o}$ is

$$
\begin{align*}
\frac{v_{o}}{i_{s}} & =-\frac{N(s)}{D(s)}  \tag{9.56}\\
& =-\frac{R_{0} g_{m 1} R_{1} g_{m 2} R_{2}-\left(g_{m 1} R_{1} C_{m 1}+C_{m 2}\right) R_{0} R_{2} s-R_{0} R_{1} R_{2} C_{m 2}\left(C_{1}+C_{m 1}\right) s^{2}}{1+a_{1} s+a_{2} s^{2}+a_{3} s^{3}}
\end{align*}
$$

where

$$
\begin{align*}
a_{1}= & K+R_{0}\left(C_{m 2}+C_{0}\right)+g_{m 1} R_{1} g_{m 2} R_{2} R_{0} C_{m 2}  \tag{9.57a}\\
a_{2}= & R_{1} R_{2}\left(C_{2}+C_{m 1}+C_{m 2}\right)\left(C_{1}+C_{m 1}\right)-R_{1} R_{2} C_{m 1}^{2}+R_{0}\left(C_{m 2}+C_{0}\right) K \\
& -g_{m 1} R_{1} C_{m 1} C_{m 2} R_{0} R_{2}-R_{0} R_{2} C_{m 2}^{2}  \tag{9.57b}\\
a_{3}= & R_{0} R_{1} R_{2}\left[\left(C_{2} C_{m 2}+C_{0} C_{2}+C_{0} C_{m 2}\right)\left(C_{1}+C_{m 1}\right)+C_{1} C_{m 1} C_{m 2}\right. \\
& \left.+C_{0} C_{1} C_{m 1}\right] \tag{9.57c}
\end{align*}
$$

with

$$
\begin{equation*}
K=R_{2}\left(C_{2}+C_{m 1}+C_{m 2}\right)+R_{1}\left(C_{1}+C_{m 1}\right)+R_{1} C_{m 1} g_{m 2} R_{2} \tag{9.57d}
\end{equation*}
$$

Equation 9.56 is the transfer function from $i_{s}$ to $v_{o}$. The transfer function of the voltage gain from $v_{\text {in }}$ to $v_{o}$ is found by multiplying (9.56) by $g_{m 0}$ (since $i_{s}=g_{m 0} v_{\text {in }}$ ); therefore, the voltage gain and (9.56) have the same poles and zeros. The transfer function in (9.56) has two zeros and three poles. Let us first examine the poles. The expressions for the $a_{i}$ coefficients are complicated and involve many terms. Therefore assumptions are needed to simplify the equations. If $g_{m 1} R_{1} g_{m 2} R_{2} \gg 1$, which is usually true, then

$$
\begin{equation*}
a_{1} \approx g_{m 1} R_{1} g_{m 2} R_{2} R_{0} C_{m 2} \tag{9.58}
\end{equation*}
$$

Assuming there is a dominant pole $p_{1}$, then

$$
\begin{equation*}
p_{1} \approx-\frac{1}{a_{1}}=-\frac{1}{g_{m 1} R_{1} g_{m 2} R_{2} R_{0} C_{m 2}} \tag{9.59}
\end{equation*}
$$

Another way to arrive at this estimate of $p_{1}$ is to apply the Miller effect to $C_{m 2}$. The effective Miller capacitor is about $C_{m 2}$ times the negative of the gain across $C_{m 2}$, which is $g_{m 1} R_{1} g_{m 2} R_{2}$. This capacitor appears in parallel with $R_{0}$, giving a time constant of $\left(g_{m 1} R_{1} g_{m 2} R_{2}\right) R_{0} C_{m 2}$.

The other poles $p_{2}$ and $p_{3}$ could be found by factoring the third-order denominator in (9.56), which can be done using a computer but is difficult by hand. However, these poles can be estimated from a quadratic equation under certain conditions. If there is a dominant pole $p_{1}$, then $\left|p_{2}\right|,\left|p_{3}\right| \gg\left|p_{1}\right|$. At high frequencies, where $|s| \gg\left|p_{1}\right| \approx 1 / a_{1}$, we have $\left|a_{1} s\right| \gg 1$, so the denominator in (9.56) can be approximated by dropping the constant " 1 " to give

$$
\begin{equation*}
D(s) \approx a_{1} s+a_{2} s^{2}+a_{3} s^{3}=a_{1} s\left(1+\frac{a_{2}}{a_{1}} s+\frac{a_{3}}{a_{1}} s^{2}\right) \tag{9.60}
\end{equation*}
$$

This equation gives three poles. One pole is at dc, which models the effect of the dominant pole $p_{1}$ for frequencies well above $\left|p_{1}\right|$. Poles $p_{2}$ and $p_{3}$ are the other roots of (9.60). They can be found by concentrating on the quadratic term in parenthesis in (9.60), which is

$$
\begin{equation*}
D^{\prime}(s)=\frac{D(s)}{a_{1} s} \approx 1+\frac{a_{2}}{a_{1}} s+\frac{a_{3}}{a_{1}} s^{2} \approx\left(1-\frac{s}{p_{2}}\right)\left(1-\frac{s}{p_{3}}\right) \tag{9.61}
\end{equation*}
$$

Assuming that $R_{0}, R_{1}, R_{2} \gg\left|1 /\left(g_{m 2}-g_{m 1}\right)\right|$ and $C_{o}$ is small compared to the other capacitors, (9.57b) and ( 9.57 c ) simplify to

$$
\begin{align*}
& a_{2} \approx R_{0} R_{1} R_{2}\left(g_{m 2}-g_{m 1}\right) C_{m 1} C_{m 2}  \tag{9.62}\\
& a_{3} \approx R_{0} R_{1} R_{2}\left(C_{1} C_{2} C_{m 2}+C_{2} C_{m 1} C_{m 2}+C_{1} C_{m 1} C_{m 2}\right) \tag{9.63}
\end{align*}
$$

Using (9.58), (9.62), and (9.63), the coefficients in $D^{\prime}(s)$ are

$$
\begin{align*}
& \frac{a_{2}}{a_{1}} \approx \frac{g_{m 2}-g_{m 1}}{g_{m 1} g_{m 2}} C_{m 1}  \tag{9.64}\\
& \frac{a_{3}}{a_{1}} \approx \frac{C_{1} C_{2}+C_{m 1} C_{1}+C_{2} C_{m 1}}{g_{m 1} g_{m 2}} \tag{9.65}
\end{align*}
$$

To ensure that the high-frequency poles are in the left half-plane (LHP), $a_{2} / a_{1}$ must be positive (see Appendix A9.2). Therefore, $g_{m 2}$ must be larger than $g_{m 1}$. Poles $p_{2}$ and $p_{3}$ can be real or complex, and in general the quadratic formula must be used to solve for these poles. However, if these poles are real and widely spaced and if $C_{m 1} \gg C_{1}, C_{2}$, then approximate expressions can be found. If $\left|p_{2}\right| \ll\left|p_{3}\right|$, then $-1 / p_{2}$ is approximately equal to the coefficient of $s$ in $D^{\prime}(s)$, so

$$
\begin{equation*}
p_{2} \approx-\frac{a_{1}}{a_{2}}=-\frac{g_{m 1} g_{m 2}}{\left(g_{m 2}-g_{m 1}\right) C_{m 1}} \tag{9.66a}
\end{equation*}
$$

Also $1 /\left(p_{2} p_{3}\right)$ is equal to the coefficient of $s^{2}$ in $D^{\prime}(s)$, so

$$
\begin{align*}
p_{3} \approx \frac{a_{1}}{a_{3}} \frac{1}{p_{2}} & =-\frac{g_{m 1} g_{m 2}}{C_{1} C_{2}+C_{m 1} C_{1}+C_{2} C_{m 1}} \cdot \frac{\left(g_{m 2}-g_{m 1}\right) C_{m 1}}{g_{m 1} g_{m 2}}  \tag{9.66b}\\
& =-\frac{\left(g_{m 2}-g_{m 1}\right) C_{m 1}}{C_{1} C_{2}+C_{m 1}\left(C_{1}+C_{2}\right)} \approx-\frac{g_{m 2}-g_{m 1}}{C_{1}+C_{2}}
\end{align*}
$$

The final approximation here follows if $C_{m 1}$ is large. Equations 9.66 a and 9.66 b are accurate if $\left|p_{2}\right| \ll\left|p_{3}\right|$. Substituting (9.66a) and (9.66b) into this inequality produces an equivalent condition

$$
\begin{equation*}
\left|p_{2}\right| \approx \frac{g_{m 1} g_{m 2}}{\left(g_{m 2}-g_{m 1}\right) C_{m 1}} \ll \frac{\left(g_{m 2}-g_{m 1}\right) C_{m 1}}{C_{1} C_{2}+C_{m 1}\left(C_{1}+C_{2}\right)} \approx\left|p_{3}\right| \tag{9.67}
\end{equation*}
$$

If this condition is not satisfied, $p_{2}$ and $p_{3}$ are either complex conjugates or real but closely spaced. $C_{m 1}$ can always be chosen large enough to satisfy the inequality in (9.67). While it is possible to make the high-frequency poles real and widely separated, higher unity-gain bandwidth may be achievable when $p_{2}$ and $p_{3}$ are not real and widely separated. ${ }^{16}$

In the simplified equations 9.66 a and 9.66 b , poles $p_{2}$ and $p_{3}$ are dependent on $C_{m 1}$ but not on $C_{m 2}$. In contrast, dominant pole $p_{1}$ is inversely proportional to $C_{m 2}$ and is independent of $C_{m 1}$. The poles can be positioned to approximate a two-pole op amp by making $\left|p_{1}\right| \ll$ $\left|p_{2}\right| \ll\left|p_{3}\right|$ and positioning $\left|p_{3}\right|$ well beyond the unity-gain frequency of the op amp.

The zero locations can be found by factoring the second-order numerator $N(s)$ in (9.56). The coefficients of $s$ and $s^{2}$ in the numerator are negative and the constant term is positive. As a result, the zeros are real. One is positive and the other is negative, as is shown in Appendix A9.2.

The zeros will be found using some simplifying assumptions. First, the numerator of (9.56) can be rewritten as

$$
\begin{equation*}
N(s)=R_{0} g_{m 1} R_{1} g_{m 2} R_{2}\left[1-s\left(\frac{C_{m 1}}{g_{m 2}}+\frac{C_{m 2}}{g_{m 1} R_{1} g_{m 2}}\right)-s^{2} \frac{C_{m 2}\left(C_{1}+C_{m 1}\right)}{g_{m 1} g_{m 2}}\right] \tag{9.68}
\end{equation*}
$$

Assuming that $C_{m 1} \gg C_{1}$ and $C_{m 1} \gg C_{m 2} /\left(g_{m 1} R_{1}\right)$, then

$$
\begin{equation*}
N(s) \approx R_{0} g_{m 1} R_{1} g_{m 2} R_{2}\left[1-s \frac{C_{m 1}}{g_{m 2}}-s^{2} \frac{C_{m 2} C_{m 1}}{g_{m 1} g_{m 2}}\right] \tag{9.69}
\end{equation*}
$$

The zeros are the roots of $N(s)=0$. Using the quadratic formula and (9.69), the zeros are

$$
\begin{equation*}
z_{1,2}=-\frac{g_{m 1}}{2 C_{m 2}} \pm \sqrt{\left(\frac{g_{m 1}}{2 C_{m 2}}\right)^{2}+\frac{g_{m 1} g_{m 2}}{C_{m 1} C_{m 2}}}=-\frac{g_{m 1}}{2 C_{m 2}}\left(1 \pm \sqrt{1+\frac{4 g_{m 2} C_{m 2}}{g_{m 1} C_{m 1}}}\right) \tag{9.70}
\end{equation*}
$$

Taking the positive square root in the right-most formula in (9.70) yields a value that is larger than one. Adding this value to 1 gives a positive value for the term in parentheses; subtracting this value from 1 gives a negative quantity with a smaller magnitude than the sum. Therefore, one zero is in the LHP and has a magnitude greater than $g_{m 1} /\left(2 C_{m 2}\right)$. The other zero is in the RHP and has a smaller magnitude than the LHP zero. As a result, the effect of the RHP zero is felt at a lower frequency than the LHP zero.

The magnitude of one or both zeros can be comparable to $\left|p_{2}\right|$. Because the RHP zero is at a lower frequency than the LHP zero, the RHP zero can cause significant negative phase shift for frequencies at or below $\left|p_{2}\right|$, which would degrade the phase margin of a feedback loop. This undesired negative phase shift would not occur if the transfer function did not have zeros. Unfortunately, the three techniques considered in Section 9.4.3 to eliminate a RHP zero have important limitations in a low-supply application. First, the zeros could be eliminated by adding a source-follower buffer between the op-amp output and the right-hand side of capacitors $C_{m 1}$ and $C_{m 2}$ (as in Fig. 9.21), thereby eliminating the feedforward paths through the capacitors. However, the source follower has a nonzero dc voltage between its input and output. This voltage may limit the op-amp output swing to an unacceptably low value in a low-power-supply application. Second, cascode stages could be used to eliminate the zeros, as shown in Fig. 9.23. However, the requirement that all transistors in the cascode stage operate in the active region may limit the minimum supply voltage. Finally, a series zero-canceling resistance (as in Fig. 9.24a) implemented with a transistor may require a large gate voltage that exceeds the power supply.

The NE5234 op amp uses nested Miller-effect compensation. Figure 9.31 repeats the simplified ac schematic of the high-frequency gain path of the NE5234 shown in Fig. 7.36. Here, the common-mode input voltage is assumed to be low enough that $Q_{1}$ and $Q_{2}$ in Fig. 6.36 are off. Also, the dc load current is assumed to be $I_{L}=1 \mathrm{~mA}$ as in the calculations in Chapter 6. Therefore, $Q_{75}$ in Fig. 6.39 conducts a nearly constant current and is omitted in Fig. 9.31 along with the circuits that control it for simplicity. In practice, these transistors are important under other bias conditions. Also, note that the transconductance of the output stage depends on the bias point assumed. The key point here is that this op amp uses three nested compensation loops: through $C_{22}, C_{25}$, and $C_{65}$. The loop through $C_{25}$ includes series resistor $R_{25}=1.3 \mathrm{k} \Omega$ to reduce the effects of the zero introduced through $C_{25}$ and increase the phase margin. ${ }^{17}$ This structure has one more level of nesting than shown in Fig. 9.30. The extra level is introduced through $C_{65}$ in the third stage, and its purpose is explained next.

Chapter 6 pointed out that the output transistors $Q_{74}$ and $Q_{75}$ in Fig. 6.39 are driven by emitter followers to increase the current gain of the output stage and reduce its load on the second stage. Because the integrated-circuit process is optimized to build much higher quality $n p n$ transistors than pnp transistors, $\beta_{p n p}<\beta_{n p n}$ in practice. To provide adequate current gain when $Q_{74}$ controls the output as shown in Fig. 9.31, two emitter followers $Q_{64} Q_{65}$ drive $Q_{74}$. In contrast, Fig. 6.39 shows that only one emitter follower $Q_{68}$ is used to drive $Q_{75}$. Furthermore, $Q_{64}$ and $Q_{65}$ use opposite polarity transistors to avoid introducing a large dc level shift that would increase the minimum required power-supply voltage.
image_name:Figure 9.31
description:The circuit diagram represents the high-frequency gain path of the NE5234 op amp. It features multiple NPN transistors arranged in a complex configuration to achieve desired amplification and frequency response characteristics. The circuit utilizes emitter followers (Q64, Q65) to drive Q74, providing unity gain and minimizing frequency response limitations. Various resistors and capacitors are used for biasing and frequency compensation. The output is taken across RL, and the load current is denoted as IL.
Figure 9.31 An ac schematic of the high-frequency gain path of the NE5234 op amp assuming that the common-mode input voltage is low enough that $Q_{1}$ and $Q_{2}$ in Fig. 6.36 are off and assuming that $Q_{75}$ in Fig. 6.39 conducts a constant current and can be ignored along with the elements that drive it.

Ideally, these emitter followers give unity gain and do not limit the frequency response of the third stage. In practice, however, they introduce extra poles that contribute unwanted phase shift at high frequency that reduces the phase margin when the op amp is connected in a feedback loop. This problem is especially severe in driving $Q_{74}$ because two emitter followers are used instead of one and because the output transistor and one of the emitter followers are $p n p$ transistors, which have much lower $f_{T}$ than $n p n$ transistors operating at the same bias currents. If Miller compensation were not applied through $C_{65}$, the presence of the extra poles in the output stage due to the emitter followers would introduce extra undesired phase shift near the unity-gain frequency of the op amp and significantly reduce the phase margin. To overcome this problem, the extra level of Miller-effect compensation through $C_{65}$ is introduced. It forces one pole to be dominant in the output stage when feedback is applied through $C_{25}$. The minimum required value of $C_{65}$ must be able to cope with all possible bias currents in the output stage. From a stability standpoint, the worst case is when the bias current and transconductance of $Q_{74}$ are maximum because the op-amp bandwidth is increased in this case, which increases the importance of poles introduced by the emitter followers. In practice, $C_{65}$ is chosen from simulations to be $10 \mathrm{pF} .{ }^{17}$ The corresponding capacitor on the npn side of the output stage is $C_{68}$ in Fig. 6.39, and this capacitor is only 1 pF . In practice, $C_{68} \ll C_{65}$ because the $n p n$ side uses only one emitter follower and because the transistors on this side are both npn transistors.
image_name:Figure 9.32 Gain and phase versus frequency for the NE5234 op amp from SPICE
description:The graph in Figure 9.32 is a Bode plot displaying the gain and phase versus frequency for the NE5234 operational amplifier as analyzed using SPICE simulation.

1. **Type of Graph and Function:**
- The graph is a Bode plot, which consists of two separate plots: one for magnitude (gain) and one for phase, both plotted against frequency.

2. **Axes Labels and Units:**
- The horizontal axis is labeled "Frequency (Hz)" and uses a logarithmic scale ranging from 10 Hz to 10 MHz.
- The vertical axis for the gain plot (top) is labeled "|Loop Gain| (dB)" ranging from -40 dB to 100 dB.
- The vertical axis for the phase plot (bottom) is labeled "∠ Loop Gain" with units in degrees, ranging from -225° to 0°.

3. **Overall Behavior and Trends:**
- **Gain Plot:** The gain starts at a high value near 100 dB at low frequencies and decreases linearly on a logarithmic scale, following a slope of -6 dB/octave. The gain crosses 0 dB at approximately 2.7 MHz.
- **Phase Plot:** The phase starts near 0° at low frequencies, decreases steadily, and approaches -180° as the frequency increases. The phase margin is noted at 43°.

4. **Key Features and Technical Details:**
- **Gain Plot:**
- The gain decreases with a consistent slope of -6 dB/octave, indicative of a single pole system.
- The unity gain frequency, where the gain crosses 0 dB, is at 2.7 MHz.
- **Phase Plot:**
- The phase response shows a decreasing trend, with a phase margin of 43° at the unity gain frequency, indicating the stability of the op-amp.

5. **Annotations and Specific Data Points:**
- The gain plot is annotated with the slope "-6 dB/octave" and the unity gain frequency "2.7 MHz."
- The phase plot includes an annotation for the phase margin, "Phase Margin = 43°," which is a critical parameter for stability analysis.

This Bode plot highlights the frequency response characteristics of the NE5234 op-amp, showing its gain and phase behavior over a wide frequency range, and provides key insights into its stability and performance limits.

Figure 9.32 Gain and phase versus frequency for the NE5234 op amp from SPICE.

The presence of an extra level of Miller compensation reduces the bandwidth of the output stage to make one pole dominant. Although it allows a simple compensation scheme for the op amp, it also limits the high-frequency performance of the op amp with compensation.

As shown in Chapter 7, the frequency response of the NE5234 is dominated by the Miller multiplied $C_{22}$. With unity-gain feedback as in Fig. 6.3c, the resulting gain and phase plots for the NE5234 are shown in Fig. 9.32. These plots were generated using SPICE with transistor parameters as shown in Fig. 2.32 except $\beta_{F}=40$ and $V_{A}=30 \mathrm{~V}$ for $n p n$ transistors and $\beta_{F}=10$ and $V_{A}=20 \mathrm{~V}$ for pnp transistors. The bias conditions are the same as assumed in Chapter 6. The resulting unity-gain frequency is 2.7 MHz , and the phase margin is 43 degrees. Return ratio simulations give the same results.

Fig. 9.33a shows another technique for eliminating a RHP zero that can be used with cascaded stages in a low-supply application. ${ }^{16,18}$ Two gain stages and one Miller compensation capacitor are shown. A transconductance stage, $g_{m f}$, is included. It provides a feedforward path that can be used to move the zero to infinity. The small-signal circuit is shown in Fig. 9.33b. To allow a simple explanation of this circuit, initially assume that $C_{1}=C_{2}=0$. The circuit has one pole due to $C_{m}$ and one zero due to the feedforward current through $C_{m}$. If the zero moves to infinity, the total forward current must go to zero when $\omega \rightarrow \infty$. Also, if the zero moves to
image_name:(a)
description:The block diagram labeled (a) represents a two-stage operational amplifier (op-amp) with Miller compensation and a feedforward transconductor. Here's a detailed breakdown of the diagram:

1. **Main Components:**
- **Amplifiers:**
- The first stage is represented by a transconductance amplifier with a gain denoted as \(+g_{m1}\). This stage takes the input voltage \(v_1\) and produces an output current proportional to \(v_1\).
- The second stage is another transconductance amplifier with a gain of \(-g_{m2}\), which processes the voltage \(v_2\) from the first stage and outputs a current that contributes to the final output voltage \(v_o\).
- A feedforward transconductance stage \(-g_{mf}\) is included, providing a direct path from the input to the output, bypassing the second stage.
- **Capacitor:**
- A Miller compensation capacitor \(C_m\) is connected between the output of the first stage \(v_2\) and the output \(v_o\).

2. **Flow of Information or Control:**
- The input voltage \(v_1\) is fed into the first transconductance stage \(+g_{m1}\), producing an intermediate voltage \(v_2\).
- The intermediate voltage \(v_2\) is then processed by the second transconductance stage \(-g_{m2}\), generating the output voltage \(v_o\).
- The feedforward transconductance stage \(-g_{mf}\) directly takes the input voltage \(v_1\) and contributes to the output voltage \(v_o\), providing a feedforward path.
- The Miller compensation capacitor \(C_m\) introduces a feedback loop from \(v_2\) to \(v_o\), stabilizing the amplifier and affecting its frequency response.

3. **Labels, Annotations, and Key Indicators:**
- The diagram is annotated with voltage nodes \(v_1\), \(v_2\), and \(v_o\), indicating the flow of signals through the stages.
- The transconductance gains \(+g_{m1}\), \(-g_{m2}\), and \(-g_{mf}\) are marked, highlighting the amplification and feedforward characteristics of each stage.
- The capacitor \(C_m\) is labeled, emphasizing its role in compensation.

4. **Overall System Function:**
- The primary function of this system is to amplify an input signal \(v_1\) through two stages of transconductance amplification, with the aid of Miller compensation for stability and improved frequency response.
- The inclusion of the feedforward transconductance stage \(-g_{mf}\) allows for the movement of the zero to infinity, which can improve the phase margin and overall stability of the op-amp by reducing the effect of the second stage at high frequencies.
- The arrangement of these components ensures a balanced trade-off between bandwidth, gain, and stability, making it suitable for high-performance analog applications.
image_name:(b)
description:
[
name: g_m1*v1, type: VoltageControlledCurrentSource, value: g_m1*v1, ports: {Np: GND, Nn: v2}
name: g_m2*v2, type: VoltageControlledCurrentSource, value: g_m2*v2, ports: {Np: v2, Nn: vo}
name: g_mf*v1, type: VoltageControlledCurrentSource, value: g_mf*v1, ports: {Np: v1, Nn: vo}
name: C_m, type: Capacitor, value: C_m, ports: {Np: v2, Nn: vo}
name: R_1, type: Resistor, value: R_1, ports: {N1: v2, N2: GND}
name: C_1, type: Capacitor, value: C_1, ports: {Np: v2, Nn: GND}
name: R_2, type: Resistor, value: R_2, ports: {N1: vo, N2: GND}
name: C_2, type: Capacitor, value: C_2, ports: {Np: vo, Nn: GND}
]
extrainfo:The circuit is a two-stage operational amplifier with Miller compensation and a feedforward transconductance stage. It includes capacitors C_m, C_1, and C_2, resistors R_1 and R_2, and voltage-controlled current sources g_m1, g_m2, and g_mf. The feedforward transconductance stage can move the zero to infinity, affecting the transfer function of the amplifier.
Figure 9.33 (a) Block diagram of a two-stage op amp with Miller compensation and a feedforward transconductor. (b) A small-signal model.
infinity, the output voltage will go to zero as $\omega \rightarrow \infty$ due to the pole in the transfer function. When $\omega \rightarrow \infty$, capacitor $C_{m}$ becomes a short circuit, so $v_{2}=0$ when $\omega \rightarrow \infty$. Therefore at infinite frequency, the current $g_{m 1} v_{1}$ from the $g_{m 1}$ source flows through $C_{m}$. Adding this feedforward current to the current $g_{m f} v_{1}$ from the $g_{m f}$ generator gives the total current at the output node that is related to $v_{1}$

$$
\begin{equation*}
i_{f f}(\omega \rightarrow \infty)=\left(-g_{m 1}+g_{m f}\right) v_{1} \tag{9.71}
\end{equation*}
$$

If $g_{m f}=g_{m 1}$, this current equals zero, which means the zero is at infinity.
An exact analysis of the circuit in Fig. 9.33 gives a transfer function

$$
\begin{align*}
& \frac{v_{o}}{v_{1}}=  \tag{9.72}\\
& \frac{-g_{m 1} R_{1} g_{m 2} R_{2}-g_{m f} R_{2}-s R_{1} R_{2}\left[g_{m f}\left(C_{1}+C_{m}\right)-g_{m 1} C_{m}\right]}{1+s\left[g_{m 2} R_{1} R_{2} C_{m}+R_{2}\left(C_{2}+C_{m}\right)+R_{1}\left(C_{1}+C_{m}\right)\right]+s^{2} R_{1} R_{2}\left(C_{1} C_{2}+C_{1} C_{m}+C_{2} C_{m}\right)}
\end{align*}
$$

The zero can be moved to infinity by choosing $g_{m f}$ so that the coefficient of $s$ in the numerator is zero, which occurs when

$$
\begin{equation*}
g_{m f}=g_{m 1} \frac{C_{m}}{C_{1}+C_{m}}=\frac{g_{m 1}}{1+\frac{C_{1}}{C_{m}}} \tag{9.73}
\end{equation*}
$$

This value of $g_{m f}$ depends on the ratio of an internal parasitic capacitance $C_{1}$, which is not well controlled, and compensation capacitor $C_{m}$. Using $g_{m f}=g_{m 1}$ moves the zero into the LHP to about $-g_{m 2} / C_{1}$; the magnitude of this zero is usually above the unity-gain frequency of the op amp. If the $g_{m 1}$ stage has a differential input, the $-g_{m f}$ stage can be realized using a replica of the $g_{m 1}$ stage with the inputs reversed to change the sign of the transconductance.

This zero-cancellation scheme can be used repeatedly in a three-stage op amp to eliminate the zeros, as shown in Fig. 9.34a. A small-signal model is shown in Fig. 9.34b. Analysis of
image_name:(a)
description:The system block diagram labeled as (a) represents a three-stage operational amplifier (op-amp) with nested Miller compensation and two feedforward transconductors. Here’s a detailed breakdown of the components and their interactions:

1. **Main Components:**
- **Transconductance Amplifiers (g):**
- **+gm0:** This is the first stage amplifier, which receives the input voltage \(v_{in}\) and outputs \(v_1\).
- **+gm1:** The second stage amplifier takes \(v_1\) as input and outputs \(v_2\).
- **+gm2:** The third stage amplifier receives \(v_2\) and outputs the final voltage \(v_o\).
- **Feedforward Transconductors (g_mf):**
- **-gmf1:** Connected in parallel with the second stage, it provides a feedforward path from \(v_1\) to \(v_o\), reversing the transconductance sign.
- **-gmf0:** Connected from the input \(v_{in}\) to the output \(v_o\), providing another feedforward path.
- **Capacitors (C):**
- **Cm2:** Connected between the output of the first stage \(v_1\) and the output \(v_o\), providing Miller compensation.
- **Cm1:** Connected between the output of the second stage \(v_2\) and the output \(v_o\), also providing Miller compensation.

2. **Flow of Information or Control:**
- The input voltage \(v_{in}\) is amplified by the first stage (+gm0) to produce \(v_1\).
- \(v_1\) is then amplified by the second stage (+gm1) to produce \(v_2\).
- \(v_2\) is further amplified by the third stage (+gm2) to produce the output voltage \(v_o\).
- The feedforward transconductors (-gmf1 and -gmf0) provide direct paths from earlier stages or input to the output, effectively bypassing intermediate stages to improve frequency response and stability.
- The capacitors Cm1 and Cm2 provide feedback paths that stabilize the amplifier by compensating for phase shifts introduced by the amplifiers.

3. **Labels, Annotations, and Key Indicators:**
- The diagram clearly labels each transconductance amplifier and feedforward transconductor with their respective symbols and polarities (positive or negative).
- The connections between the stages are annotated with voltage nodes (\(v_1, v_2, v_o\)).
- The capacitors Cm1 and Cm2 are labeled to indicate their role in the compensation mechanism.

4. **Overall System Function:**
- The primary function of this system is to provide a high-gain amplification of an input signal while maintaining stability across a wide frequency range. The nested Miller compensation, along with the feedforward paths, helps in canceling out unwanted zeros, thus enhancing the op-amp's performance by improving its bandwidth and phase margin. This configuration is particularly useful in applications requiring precise amplification and fast response times.
image_name:(b)
description:
[
name: Cm2, type: Capacitor, value: Cm2, ports: {Np: v1, Nn: v0}
name: Cm1, type: Capacitor, value: Cm1, ports: {Np: v2, Nn: vo}
equation*
v_{o
v_{i n
R_{2
0
1
2
2
1+b_{1
2
2
3
3
9.74
equation*
1
3
1
3
align*
1
1
m f 1
0
2
m 2
9.75a
2
2
m f 1
0
1
2
1
m 1
m 2
9.75b
3
3
9.75c
align*
align*
0
m 0
m 1
m 2
0
1
m f 0
m 0
m f 1
0
9.76a
1
m 0
m 1
m f 1
0
1
m 1
m 0
m f 0
0
m 2
m f 0
1
1
m 1
m f 0
0
0
m 0
m f 1
0
1
1
9.76b
2
m 0
m f 0
0
1
1
m 1
m 2
m f 0
0
1
1
m 1
0
9.76c
align*
2
m f 0
m f
0
1
m f 0
m 0
m f 1
m 1
0
1
2
m f 1
m 1
m f 0
m 0
1
1
m 1
1
m 2
2
0
m 2
m 2
1
1
1
1
2
2
2
3
1
3
1
3
\circ
k
0
1
m f 0
m f 1
m f 0
m 0
m f 1
m 1
0
1
m 1
m 2
m f 0
m f 1
i
m f 0
m f 1
2
3
3
1
1
1
1
1
2
3
m f 1
2
1
m 1
2
2
m f 1
0
1
2
m 1
m 2
2
m f 1
m 1
2
m 2
0
1
2
m 1
m 2
align*
2
b_{1
b_{2
g_{m 1
C_{m 1
9.77a
3
b_{1
b_{3
1
p_{2
g_{m 2
C_{2
9.77b
align*
2
3
3
2
equation*
m 1
g_{m 1
g_{m 2
2
9.78
equation*
m 1
2
pF
m 1
m 2
m 1
m 2
m 1
pF
pF
2
\circ
1
2
equation*
0
1
2
9.79
equation*
equation*
0
m 0
0
m 1
1
m 2
2
9.80
equation*
g_{m 0
C_{m 2
g_{m 1
C_{m 1
m 0
m 1
m 2
m 1
pF
0
m 0
0
m 1
1
m 2
2
g_{m 1
3
0.2
k
3
~dB
m 0
m 1
m 2
m 1
m 0
m f 1
m f 0
~mA
V
m 2
m 1
~mA
V
1
kHz
2
MHz
3
MHz
1,2
MHz
GHz
m 1
pF
m 2
pF

1,19
0
equation*
a_{0
\left(1-\frac{s
p_{1
3
9.81
equation*
0
1
equation*
a(s)
1+a(s) f
9.82
equation*
equation*
\frac{a_{0
\left(1-\frac{s
p_{1
3
1+\frac{a_{0
\left(1-\frac{s
p_{1
3
a_{0
\left(1-\frac{s
p_{1
3
0
9.83
equation*
0
0
equation*
s
p_{1
3
0
9.84
equation*
s
p_{1
3
0
s
p_{1
-T_{0
T_{0
or
T_{0
j 60^{\circ
or
T_{0
-j 60^{\circ
align*
1
1
T_{0
2
1
T_{0
j 60^{\circ
9.85
3
1
T_{0
-j 60^{\circ
align*
equation*
a_{0
1+T_{0
1
\left(1-\frac{s
s_{1
s
s_{2
s
s_{3
9.86
equation*
0
0
1
0
\circ
0
0
2
Re
2
Re
T_{0
j 60^{\circ
T_{0
\circ
0
0
0
0
0
equation*
0
1
\circ
1
9.87
equation*
1
0
\sigma t
0
0
equation*
a_{0
\left(1+\frac{j \omega
\left|p_{1
3
T_{0
\left(1+j \frac{\omega
\left|p_{1
3
9.88
equation*
10
dB/octave
180
180
Ph
180
180
180
180
dB/octave
180
\circ
\circ
\omega_{180
\left|p_{1
equation*
180
1
9.89
equation*
equation*
180
0
9.90
equation*
180
equation*
180
T_{0
\left|1+j \frac{\omega_{180
\left|p_{1
3
T_{0
8
9.91
equation*
180
0
0
equation*
0
1+a_{1
2
2
1+b_{1
2
2
9.92
equation*
equation*
0
N_{a
D_{a
9.93
equation*
equation*
0
1+c_{1
2
2
1+d_{1
2
2
9.94
equation*
equation*
0
N_{f
D_{f
9.95
equation*
0
0
equation*
a(s)
1+a(s) f(s)
9.96
equation*
equation*
a_{0
a
f
D_{f
a
0
a
f
9.97
equation*
equation*
0
0
0
9.98
equation*
equation*
f
a
0
a
f
9.99
equation*
0
0
equation*
a
f
9.100
equation*
0
0
f
a
0
N_{a
D_{a
N_{f
D_{f
0
N_{a
D_{a
N_{f
D_{f
equation*
0
\left(1-\frac{s
z_{a 1
s
z_{a 2
s
z_{f 1
s
z_{f 2
\left(1-\frac{s
p_{a 1
s
p_{a 2
s
p_{f 1
s
p_{f 2
9.101
equation*
gathered
a 1
a 2
are zeros of
f 1
f 2
are zeros of
a 1
a 2
are poles of
f 1
f 2
are poles of
gathered
align*
0
\left(-p_{a 1
a 2
f 1
f 2
\left(-z_{a 1
a 2
f 1
f
\left(s-z_{a 1
a 2
f 1
f 2
\left(s-p_{a 1
a 2
f 1
f 2
9.102
align*
a 1
a 2
equation*
0
\left|p_{a 1
a 2
f 1
f 2
\left|z_{a 1
a 2
f 1
f 2
\left(s-z_{a 1
a 2
f 1
f 2
\left(s-p_{a 1
a 2
f 1
f 2
9.103
equation*
align*
a 1
a 2
s-z_{f 1
s-z_{f 2
a 1
a 2
f 1
f 2
9.104
align*
equation*
0
\left|p_{a 1
a 2
f 1
f 2
\left|z_{a 1
a 2
f 1
f 2
\left|s-z_{a 1
a 2
f 1
f 2
\left|s-p_{a 1
a 2
f 1
f 2
9.105
equation*
aligned
Y
1
\circ
Y
1
\circ
aligned
1
aligned
Z
1
\circ
Z
1
\circ
Z
2
\circ
Z
3
\circ
Z
4
\circ
aligned
1
2
3
1
4
a i
a i
a i
1
2
3
4
3
1
3
1
4
4
1
2

20
p
z
p
z
p
z
p
z
equation*
a
\sum[\text { poles of
zeros of
N_{p
z
9.106
equation*
0
0
equation*
100
\left(1-\frac{s
p_{1
s
p_{2
s
p_{3
9.107
equation*
aligned
1
6
rad
s
2
6
rad
s
3
6
rad
s
aligned
6
rad
s
6
6
6
rad
s
1
2
3
1
2
i
equation*
1
\sigma_{i
1
\sigma_{i
1
\sigma_{i
9.108
equation*
i
i
\circ
\circ
a
a
(-1-2-4)-0
3
\circ
i
equation*
0
1 \times 2 \times 4
0.45 \times 0.55 \times 2.55
9.109
equation*
array
rlr
1
2
3
1
2
3
array
at the point being considered
0
1
2
\circ
equation*
0
1 \times 2 \times 4
4.1 \times 4.5 \times 5.7
9.110
equation*
1
2
3
at this point on the locus
0
0
0
0
a_{0
1+T_{0
T_{0
a_{0
\circ
0
1 \times 2 \times 4
1.52 \times 1.55 \times 2.93
0
3
0
1 \times 2 \times 4
1 \times 3 \times 4
0
0
1 \times 2 \times 4
2 \times 4 \times 5
0
0
equation*
T_{0
\left(1+\frac{j \omega
10^{6
j \omega
2 \times 10^{6
j \omega
4 \times 10^{6
9.111
equation*
\circ
6
rad
s
6
rad
s
6
equation*
T_{0
11.6
9.112
equation*
0
6
rad
s
0
0
0
0
0
0
equation*
M(s)
G(s)+x H(s)
9.113
equation*
1
2
1
2
equation*
i
p_{1
2
2
9.114
equation*
\circ
i
0
0
\circ
equation*
0
\left|p_{1
2
\left|s-p_{1
2
9.115
equation*
1
1
2
i
2
\circ
1
2
2
2
0
1
\left|p_{1
2
2
\left|p_{2
2
2
equation*
0
1
2
\left|p_{2
\left|p_{1
9.116
equation*
0
1
0
\circ
1
0
2
F
F
equation*
i_{i
i_{2
R_{E
R_{F
E
1+R_{F
F
1+\frac{R_{E
F
R_{E
F
F
9.117
equation*
equation*
z
1
R_{F
F
9.118
equation*
equation*
p
R_{E
F
R_{E
1
R_{F
F
9.119
equation*
E
F
E
E
F
E
name: Q1, type: NPN, ports: {C: c1b21, B: b1, E: GND}
name: Q2, type: NPN, ports: {C: c2, B: c1b2, E: e2}
name: i_s, type: CurrentSource, value: i_s, ports: {Np: GND, Nn: b1}
name: R_F, type: Resistor, value: R_F, ports: {N1: b1, N2: e2}
name: C_F, type: Capacitor, value: C_F, ports: {Np: b1, Nn: e2}
name: R_L1, type: Resistor, value: R_L1, ports: {N1: c1b2, N2: GND}
name: R_E, type: Resistor, value: R_E, ports: {N1: e2, N2: GND}
name: Z_L, type: Resistor, value: Z_L, ports: {N1: c2, N2: GND}
name: RE, type: Resistor, value: RE, ports: {Np: e2, Nn: GND}
]
extrainfo:The circuit is a feedback amplifier with a feedback capacitor CF. It includes transistors Q1 and Q2, resistors RF, RL1, RE, and ZL, and a current source is. The feedback network is formed by RF and CF.
Figure 9.41 Shunt-series feedback amplifier including a feedback capacitor $C_{F}$.

image_name:Figure 9.42
description:
[
name: Q1, type: NPN, ports: {C: c1b2, B: b1, E: GND}
name: Q2, type: NPN, ports: {C: c2, B: c1b2, E: e2}
name: RF, type: Resistor, value: RF, ports: {N1: b1, N2: x1}
name: CF, type: Capacitor, value: CF, ports: {Np: b1, Nn: x1}
name: RE, type: Resistor, value: RE, ports: {N1: x1, N2: GND}
name: RL1, type: Resistor, value: RL1, ports: {N1: c1b2, N2: GND}
name: ZL, type: Resistor, value: ZL, ports: {N1: c2, N2: GND}
name: is, type: CurrentSource, value: is, ports: {Np: b1, Nn: GND}
name: CF, type: Capacitor, value: CF, ports: {Np: e2, Nn: GND}
name: RF, type: Resistor, value: RF, ports: {N1: e2, N2: GND}
name:RE,type:Resistor,value:RE,ports:{N1:e2,N2:GND}
]
extrainfo:The circuit is a feedback amplifier with a feedback capacitor CF. It includes transistors Q1 and Q2, resistors RF, RL1, RE, and ZL, and a current source is. The feedback network is formed by RF and CF.
Figure 9.42 Basic amplifier including feedback loading for the circuit of Fig. 9.41.

image_name:Figure 9.43
description:
[
name: CF, type: Capacitor, value: CF, ports: {Np: GND, Nn: Vo}
name: RF, type: Resistor, value: RF, ports: {N1: GND, N2: Vo}
name: RE, type: Resistor, value: RE, ports: {N1: Vo, N2: GND}
name: i2, type: CurrentSource, value: i2, ports: {Np: GND, Nn: Vo}
]
extrainfo:The circuit is a feedback network with a feedback capacitor CF and resistor RF. It includes two current sources i1 and i2, and a resistor RE. The feedback is applied at node Vo.
Figure 9.43 Circuit for the calculation of feedback function $f$ for the amplifier of Fig. 9.41.
given by (9.119) is usually much larger than the zero magnitude. This will be assumed and the effects of the pole will be neglected, but if $\left(R_{E}+R_{F}\right) / R_{E}$ becomes comparable to unity, the pole will be important and must be included.

The basic amplifier of Fig. 9.42 has two significant poles contributed by $Q_{1}$ and $Q_{2}$. Although higher magnitude poles exist, these do not have a dominant influence and will be neglected. The effects of this assumption will be investigated later. The loop gain of the circuit of Fig. 9.41 thus contains two forward-path poles and a feedback zero, giving rise to the root locus of Fig. 9.44. For purposes of illustration, the two poles are assumed to be $p_{1}=$ $-10 \times 10^{6} \mathrm{rad} / \mathrm{s}$ and $p_{2}=-20 \times 10^{6} \mathrm{rad} / \mathrm{s}$ and the zero is $z=-50 \times 10^{6} \mathrm{rad} / \mathrm{s}$. For convenience in the calculations, the numbers will be normalized to $10^{6} \mathrm{rad} / \mathrm{s}$.

Assume now that the loop gain of the circuit of Fig. 9.41 can be varied without changing the parameters of the basic amplifier of Fig. 9.42. Then a root locus can be plotted as the loop gain changes, and using rules 1 and 2 indicates that the root locus exists on the axis between $p_{1}$ and $p_{2}$, and to the left of $z$. The root locus must thus break away from the axis between $p_{1}$ and $p_{2}$ at $\sigma_{1}$ as shown, and return again at $\sigma_{2}$. One branch then extends to the right along the axis to end at the zero while the other branch heads toward infinity on the left. Using rule 6 gives

$$
\begin{equation*}
\frac{1}{\sigma_{1}+10}+\frac{1}{\sigma_{1}+20}=\frac{1}{\sigma_{1}+50} \tag{9.120}
\end{equation*}
$$

Solution of (9.120) for $\sigma_{1}$ gives

$$
\sigma_{1}=-84.6 \quad \text { or } \quad-15.4
$$

image_name:Figure 9.44
description:The graph depicted is a root locus plot, which is used to analyze the stability of a control system by showing the paths of the poles of the closed-loop transfer function as system parameters are varied. This particular graph is for a system where the basic amplifier contributes two poles to the transfer function \( T(s) \) and the feedback circuit contributes one zero.

Axes Labels and Units:
- **Horizontal Axis (\( \sigma \)):** Represents the real part of the complex frequency \( s \), scaled by \( 10^6 \) rad/sec.
- **Vertical Axis (\( j\omega \)):** Represents the imaginary part of the complex frequency \( s \).

Overall Behavior and Trends:
- The root locus consists of two branches. One branch starts at the pole \( p_1 \) at \( -10 \) and the other at pole \( p_2 \) at \( -20 \). These branches break away from the real axis at \( \sigma_1 = -15.4 \), forming a circular path centered around the zero \( z \) at \( -50 \).
- The branches then return to the real axis at \( \sigma_2 = -84.6 \) and extend further. One branch goes towards infinity on the left, while the other ends at the zero \( z \).

Key Features and Technical Details:
- **Breakaway Point:** \( \sigma_1 = -15.4 \)
- **Return Point:** \( \sigma_2 = -84.6 \)
- **Zero Location:** \( z = -50 \)
- **Pole Locations:** \( p_1 = -10 \), \( p_2 = -20 \)
- The circular portion of the locus is indicative of the complex conjugate pole pairs in the system.

Annotations and Specific Data Points:
- The graph shows markers for the poles (\( \times \)) and the zero (\( \circ \)).
- The circular path is symmetric about the real axis, illustrating the symmetrical nature of the root locus with respect to the real axis.

This root locus plot is a valuable tool for understanding how the system's stability changes with variations in system parameters, particularly in the context of feedback control systems.

Figure 9.44 Root locus for the circuit of Fig. 9.41 assuming the basic amplifier contributes two poles to $T(s)$ and the feedback circuit contributes one zero.

Obviously $\sigma_{1}=-15.4$ and the other value is $\sigma_{2}=-84.6$. Note that these points are equidistant from the zero, and, in fact, it can be shown that in this example the portion of the locus that is off the real axis is a circle centered on the zero. An aspect of the root-locus diagrams that is a useful aid in sketching the loci is apparent from Fig. 9.39 and Fig. 9.44. The locus tends to bend toward zeros as if attracted and tends to bend away from poles as if repelled.

The effectiveness of the feedback zero in compensating the amplifier is apparent from Fig. 9.44. If we assume that the amplifier has poles $p_{1}$ and $p_{2}$ and there is no feedback zero, then when feedback is applied the amplifier poles will split out and move parallel to the $j \omega$ axis. For practical values of loop gain $T_{0}$, this would result in "high $Q$ " poles near the $j \omega$ axis, which would give rise to an excessively peaked response. In practice, oscillation can occur because higher magnitude poles do exist and these would tend to give a locus of the kind of Fig. 9.39, where the remote poles cause the locus to bend and enter the right half-plane. (Note that this behavior is consistent with the alternative approach of considering a diminished phase margin to be causing a peaked response and eventual instability.) The inclusion of the feedback zero, however, bends the locus away from the $j \omega$ axis and allows the designer to position the poles in any desired region.

An important point that should be stressed is that the root locus of Fig. 9.44 gives the poles of the feedback amplifier. The zero in that figure is a zero of loop gain $T(s)$ and thus must be included in the root locus. However, the zero is contributed by the feedback network and is not a zero of the overall feedback amplifier. As pointed out in Section 9.5.2, the zeros of the overall feedback amplifier are the zeros of basic amplifier $a(s)$ and the poles of feedback network $f(s)$. Thus the transfer function of the overall feedback amplifier in this case has two poles and no zeros, as shown in Fig. 9.45, and the poles are assumed placed at $45^{\circ}$ to the axis by appropriate choice of $z$. Since the feedback zero affects the root locus but does not appear as a zero of the overall amplifier, it has been called a phantom zero.

On the other hand, if the zero $z$ were contributed by the basic amplifier, the situation would be different. For the same zero, the root locus would be identical but the transfer function of the overall feedback amplifier would then include the zero as shown in Fig. 9.46. This zero would then have a significant effect on the amplifier characteristics. This point is made simply to illustrate the difference between forward path and feedback-path zeros. There is no practical way to introduce a useful forward-path zero in this situation.

Before leaving this subject, we mention the effect of higher magnitude poles on the root locus of Fig. 9.44, and this is illustrated in Fig. 9.47. A remote pole $p_{3}$ will cause the locus to
image_name:Figure 9.45
description:Figure 9.45 presents two pole-zero plots on the complex s-plane, which is a graphical representation used in control theory and signal processing to analyze the poles and zeros of a transfer function.

1. **Type of Graph and Function:**
- This is a pole-zero plot on the complex s-plane.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as \( \sigma \) (real axis), and the vertical axis is labeled as \( j\omega \) (imaginary axis).
- There are no specific units provided, as this is a dimensionless representation.

3. **Overall Behavior and Trends:**
- The plots show poles (represented by crosses) and zeros (represented by circles) on the complex plane.
- The top plot shows two poles symmetrically placed along lines at a 45-degree angle to the real axis.
- The bottom plot is similar but includes an additional zero on the real axis.

4. **Key Features and Technical Details:**
- In the top plot, two poles are located symmetrically around the origin, indicating a system that may have oscillatory behavior due to complex conjugate poles.
- The bottom plot introduces a zero on the real axis, which can affect the system's frequency response by introducing a notch or altering the phase.
- Both plots have dashed lines indicating the angle of the poles, marked as 45 degrees from the real axis.

5. **Annotations and Specific Data Points:**
- There is a clear indication of the angle (45 degrees) for the lines along which the poles are placed.
- The zero is labeled as \( z \) in the bottom plot, indicating its presence and potential impact on the system dynamics.

These plots are crucial for understanding the stability and frequency response of the feedback amplifier system described in the context. The presence of poles and zeros can significantly impact the system's behavior, including stability and transient response characteristics.
image_name:Figure 9.46
description:The graph in Figure 9.46 is a pole-zero plot on the complex s-plane, which is commonly used in control systems and signal processing to represent the poles and zeros of a transfer function. This plot consists of two diagrams, each illustrating different configurations of poles and zeros.

Type of Graph and Function:
- **Type:** Pole-zero plot
- **Function:** Represents the poles and zeros of a transfer function of a feedback amplifier.

Axes Labels and Units:
- **Horizontal Axis (σ):** Real part of the complex frequency (no specific units)
- **Vertical Axis (jω):** Imaginary part of the complex frequency (no specific units)
- The plot is in the complex s-plane, typically used in Laplace transforms.

Overall Behavior and Trends:
- **Top Diagram:**
- Features two poles marked with 'x' on the left half of the s-plane.
- The poles are symmetrically placed about the real axis, forming a 45-degree angle with it.
- The lines connecting these poles to the origin indicate potential root locus paths.
- **Bottom Diagram:**
- Similar to the top diagram but includes an additional zero marked with 'o' on the real axis.
- The zero is positioned to the left of the origin, influencing the root locus paths.

Key Features and Technical Details:
- **Poles:**
- Two poles are present in both diagrams, symmetrically placed, indicating a potentially oscillatory system.
- The angle of 45 degrees suggests a balanced contribution from both real and imaginary components.
- **Zero (Bottom Diagram):**
- The zero is placed on the real axis, which can significantly alter the system's response by affecting the root locus.

Annotations and Specific Data Points:
- **45° Angle:**
- The angle is explicitly annotated, indicating the symmetrical nature of the pole placement.
- **Zero Marker (z):**
- Annotated with 'z' to denote its position and impact on the transfer function's behavior.

This plot illustrates how the introduction of a zero can modify the root locus and, consequently, the dynamic response of the feedback amplifier system. The presence of the zero in the bottom diagram highlights its role in altering the feedback characteristics of the amplifier.

Figure 9.45 Poles of the transfer function of the feedback amplifier of Fig. 9.41. The transfer function contains no zeros.

Figure 9.46 Poles and zeros of the transfer function of the feedback amplifier of Fig. 9.41 if the zero is assumed contributed by the basic amplifier.
image_name:Figure 9.47
description:The graph in Figure 9.47 is a root locus plot, which is a graphical representation used in control systems to analyze the locations of poles of a transfer function as a system parameter (usually gain) is varied. The plot is set in the complex s-plane, with the horizontal axis labeled as \( \sigma \) (real part) and the vertical axis labeled as \( j\omega \) (imaginary part).

Axes and Units:
- **Horizontal Axis (\( \sigma \)):** Represents the real part of the complex poles.
- **Vertical Axis (\( j\omega \)):** Represents the imaginary part of the complex poles.

Overall Behavior and Trends:
- The root locus starts at the poles of the open-loop transfer function, indicated by crosses (\( \times \)) on the real axis.
- There are three poles labeled \( p_1, p_2, \) and \( p_3 \) on the real axis.
- The locus shows a branch that moves off the real axis and curves into the complex plane, indicating an increase in the imaginary component of the poles as the gain is increased. This is typical of systems that exhibit oscillatory behavior.

Key Features and Technical Details:
- **Poles:** \( p_1 \), \( p_2 \), and \( p_3 \) are marked on the real axis.
- **Zero:** A zero, marked by a circle (\( \circ \)), is positioned between \( p_2 \) and \( p_3 \) on the real axis.
- The branch that curves into the complex plane suggests that as the system gain is increased, the poles move into the right half of the s-plane, potentially leading to instability if they cross the imaginary axis.

Annotations and Specific Data Points:
- The plot indicates the direction of pole movement with arrows along the locus paths.
- The presence of the zero influences the path of the root locus, altering the feedback characteristics of the amplifier system as described in the context.

This root locus plot provides insights into how the dynamic response and stability of the feedback amplifier system can be modified by adjusting the gain and considering the effects of additional poles and zeros.

Figure 9.47 Root locus of the circuit of Fig. 9.41 when an additional pole of the basic amplifier is included. (Not to scale.)
deviate from the original as shown and produce poles with a larger imaginary part than expected. The third pole, which is on the real axis, may also be significant in the final amplifier. Acceptable performance can usually be obtained by modifying the value of $z$ from that calculated above.

Finally, the results derived in this chapter explain the function of capacitors $C_{P}$ and $C_{F}$ in the circuit of the MC 1553 series-series triple of Fig. 8.21a, which was described in Chapter 8. Capacitor $C_{P}$ causes pole splitting to occur in stage $Q_{2}$ and produces a dominant pole in the basic amplifier, which aids in the compensation. However, as described above, a large value
of $C_{P}$ will cause significant loss of bandwidth in the amplifier, and so a feedback zero is introduced via $C_{F}$, which further aids in the compensation by moving the root locus away from the $j \omega$ axis. The final design is a combination of two methods of compensation in an attempt to find an optimum solution.

## 9.6 Slew Rate ${ }^{8}$

The previous sections of this chapter have been concerned with the small-signal behavior of feedback amplifiers at high frequencies. However, the behavior of feedback circuits with large input signals (either step inputs or sinusoidal signals) is also of interest, and the effect of frequency compensation on the large-signal, high-frequency performance of feedback amplifiers is now considered.

### 9.6.1 Origin of Slew-Rate Limitations

A common test of the high-frequency, large-signal performance of an amplifier is to apply a step input voltage as shown in Fig. 9.48. This figure shows an op amp in a unity-gain feedback configuration and will be used for purposes of illustration in this development. Assuming the op amp is powered from a single supply between 3 V and ground, the input here is chosen to step from 0.5 V to 2.5 V so that the circuit operates linearly well before and well after the step. Suppose initially that the circuit has a single-pole transfer function given by

$$
\begin{equation*}
\frac{V_{o}}{V_{i}}(s)=\frac{A}{1+s \tau} \tag{9.121}
\end{equation*}
$$

where

$$
\begin{equation*}
\tau=\frac{1}{2 \pi f_{o}} \tag{9.122}
\end{equation*}
$$

and $f_{o}$ is the $-3-\mathrm{dB}$ frequency. Since the circuit is connected as a voltage follower, the lowfrequency gain $A$ will be close to unity. If we assume that this is so, the response of the circuit to this step input $\left[V_{i}(s)=2 / s\right]$ is given by

$$
\begin{equation*}
V_{o}(s)=\frac{1}{1+s \tau} \frac{2}{s} \tag{9.123}
\end{equation*}
$$

using (9.121). Equation 9.123 can be factored to the form

$$
\begin{equation*}
V_{o}(s)=\frac{2}{s}-\frac{2}{s+\frac{1}{\tau}} \tag{9.124}
\end{equation*}
$$

From (9.124)

$$
\begin{equation*}
V_{o}(t)=2\left(1-e^{-t / \tau}\right) \tag{9.125}
\end{equation*}
$$

image_name:Figure 9.48 (a)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: Ao, type: OpAmp, value: Ao, ports: {InP: Vi, InN: Vo, OutP: Vo}
]
extrainfo:The circuit is a basic op-amp configuration with feedback. The input voltage Vi is applied, and the output Vo is fed back to the inverting input of the op-amp.
image_name:Figure 9.48 (b)
description:The graph in Figure 9.48 (b) is a time-domain waveform representing the input voltage $V_i$ over time $t$. The x-axis is labeled as time $t$ and is typically measured in seconds, though specific units are not indicated in the diagram. The y-axis represents the input voltage $V_i$ in volts (V).

Overall Behavior and Trends:
The graph shows a step input function where the voltage $V_i$ initially holds a constant value of +0.5 V. At a certain point in time, the voltage abruptly increases to +2.5 V, forming a step change. This indicates a sudden change in the input voltage applied to the circuit.

Key Features and Technical Details:
- **Initial Voltage Level:** The graph starts at +0.5 V, indicating the initial steady-state voltage before the step occurs.
- **Step Change:** The voltage steps up from +0.5 V to +2.5 V. This step change is crucial for testing the slew-rate performance of the circuit.
- **Time of Step:** The exact time at which the step occurs is not specified, but it is represented as a vertical line on the graph, indicating an instantaneous change.

Annotations and Specific Data Points:
- The initial voltage level is marked at +0.5 V.
- The final voltage level after the step is marked at +2.5 V.

This waveform is used to test the response of the circuit, particularly its ability to handle rapid changes in input voltage, which is essential for evaluating the slew-rate performance of the operational amplifier in the circuit depicted in Figure 9.48 (a).

Figure 9.48 (a) Circuit and (b) input for testing slew-rate performance.
image_name:(a)
description:The graph labeled (a) is a time-domain waveform representing the output voltage response \( V_o(t) \) of an operational amplifier to a step input. The x-axis is labeled \( t \) in microseconds (\( \mu s \)), indicating time, while the y-axis is labeled \( V_o(V) \), indicating output voltage in volts.

Type of Graph and Function:
This is a time-domain waveform graph depicting the transient response of an op-amp to a step input.

Axes Labels and Units:
- **X-axis:** Time in microseconds (\( \mu s \)), ranging from 0 to 0.5 \( \mu s \).
- **Y-axis:** Output voltage \( V_o \) in volts, ranging from 0 to 2.5 V.

Overall Behavior and Trends:
The graph shows an exponential rise in the output voltage from 0 V towards 2.5 V. The curve starts at the origin (0,0) and rapidly rises, reaching approximately 90% of its final value around 0.14 \( \mu s \). After this point, the curve flattens out, indicating that the output voltage is approaching its steady-state value of 2.5 V.

Key Features and Technical Details:
- **Initial Voltage:** The response begins at 0 V.
- **Final Voltage:** The output stabilizes at approximately 2.5 V.
- **Rise Time:** The output reaches 90% of its final value in about 0.14 \( \mu s \), showcasing the op-amp's slew-rate performance.
- **Exponential Rise:** The graph exhibits an exponential increase typical of an op-amp's response to a step input.

Annotations and Specific Data Points:
- The graph highlights the rapid rise in voltage, which is critical for evaluating the op-amp's ability to handle quick changes in input, relevant for slew-rate testing.
image_name:(b)
description:The graph labeled (b) is a time-domain waveform illustrating the output voltage \( V_o(t) \) of an operational amplifier in response to a step input voltage. The horizontal axis represents time \( t \) in microseconds (\( \mu s \)), while the vertical axis represents the output voltage \( V_o \) in volts (V).

Axes Labels and Units:
- **Horizontal Axis (x-axis):** Time \( t \) in microseconds (\( \mu s \)).
- **Vertical Axis (y-axis):** Output Voltage \( V_o \) in volts (V).

Overall Behavior and Trends:
The waveform exhibits a linear increase in voltage from an initial level of approximately +0.5 V to a final level of +2.5 V. This linear rise occurs over a time span of about 3 microseconds, indicating a constant slew rate during this period. After reaching 2.5 V, the voltage levels off and remains constant, showing that the output has stabilized at the final voltage level.

Key Features and Technical Details:
- **Initial Voltage Level:** Approximately +0.5 V.
- **Final Voltage Level:** +2.5 V.
- **Rise Time:** Approximately 3 microseconds to reach the final voltage level.
- **Slew Rate:** The graph represents a constant slew rate, as indicated by the linear rise in voltage over time.
- **Stabilization:** After reaching the final level, the output voltage remains constant, indicating the system's ability to handle the input change effectively.

Annotations and Specific Data Points:
- The initial and final voltage levels are marked, with the final level indicated by a dashed line at +2.5 V.
- The graph demonstrates the operational amplifier's response to a 2 V step input, testing its slew-rate performance.

Figure 9.49 Response of the circuit of Fig. 9.48 when a $2-\mathrm{V}$ step input is applied. (a) Response predicted by (9.125) for the NE5234 op amp.

The predicted response from (9.125) is shown in Fig. 9.49a using data for the NE5234 op amp with $f_{o} \simeq 2.7 \mathrm{MHz}$. This shows an exponential rise of $V_{o}(t)$ by 2 V and the output reaches 90 percent of its final value in about $0.14 \mu \mathrm{~s}$.

A typical output for the NE5234 op amp in such a test is shown in Fig. 9.49b and exhibits a completely different response. The output voltage is a slow ramp of almost constant slope and takes about $2.6 \mu \mathrm{~s}$ to reach 90 percent of its final value. Obviously the small-signal linear analysis is inadequate for predicting the circuit behavior under these conditions. The response shown in Fig. 9.49b is typical of op-amp performance with a large input step voltage applied. The rate of change of output voltage $d V_{o} / d t$ in the region of constant slope is called the slew rate and is usually specified in $\mathrm{V} / \mu \mathrm{s}$.

The reason for the discrepancy between predicted and observed behavior noted above can be appreciated by examining the circuit of Fig. $9.48 a$ and considering the responses in Fig. 9.49. At $t=0$, the input voltage steps up by +2 V , but the output voltage cannot respond instantaneously and is initially unchanged. Thus the op-amp differential input is $V_{i d}=2 \mathrm{~V}$, which drives the input stage completely out of its linear range of operation. This can be seen by considering a two-stage op amp; simplified schematics for a bipolar and CMOS op amp for use in this analysis are shown in Fig. $9.50 a$ and $b$. The Miller compensation capacitor $C$ connects around the high-gain second stage and causes this stage to act as an integrator. The current from the input stage, which charges the compensation capacitor, is $I_{x}$. The large-signal transfer characteristic from the op-amp differential input voltage $V_{i d}$ to $I_{x}$ is that of a differential pair, which is shown in Fig. 9.50c. From Fig. 9.50c, the maximum current available to charge $C$ is $2 I_{1}$, which is the tail current in the input stage. For a bipolar differential pair, $\left|I_{x}\right| \approx 2 I_{1}$
image_name:(a)
description:
[
name: Q1, type: PNP, ports: {C: x1, B: Vin, E: e1e2}
name: Q2, type: PNP, ports: {C: x2, B: Vip, E: e1e2}
name: Q3, type: NPN, ports: {C: x1, B: x1, E: -VEE}
name: Q4, type: NPN, ports: {C: x2, B: x1, E: -VEE}
name: C, type: Capacitor, value: C, ports: {Np: x2, Nn: Vo}
name: -Av, type: OpAmp, value: -Av, ports: {InP: x2, InN: Vo, OutP: Vo}
]
extrainfo:The circuit is a two-stage bipolar operational amplifier used for slew rate calculations. It consists of a differential pair at the input (Q1, Q2) with a tail current source (2I1), and a second stage with transistors Q3 and Q4. The output is connected to an op-amp with a capacitive load C for integration.
image_name:(b)
description:
[
name: M1, type: PMOS, ports: {S: s1s2, D: x1, G: Vin}
name: M2, type: PMOS, ports: {S: s1s2, D: x2, G: Vip}
name: M3, type: NMOS, ports: {S: -VSS, D: x1, G: x1}
name: M4, type: NMOS, ports: {S: -VSS, D: x2, G: x1}
name: Av, type: OpAmp, value: -Av, ports: {In: x2, Out: Vo}
name: C, type: Capacitor, value: C, ports: {Np: Vo, Nn: x2}
]
extrainfo:The circuit is a two-stage MOS operational amplifier used for slew rate calculations. It includes a PMOS differential pair (M1, M2) and an NMOS current mirror (M3, M4). The current source 2I1 provides biasing current, and the output is connected to an op-amp with a feedback capacitor C for integration.

image_name:(c)
description:The graph depicted is a large signal transfer characteristic for the input stages of a two-stage operational amplifier, specifically for the MOS differential pair. It is a plot of the output current \( I_x \) versus the differential input voltage \( V_{id} \).

Axes Labels and Units:
- **Horizontal Axis (\( V_{id} \))**: Represents the differential input voltage. Units are likely in volts, though not explicitly labeled.
- **Vertical Axis (\( I_x \))**: Represents the output current. Units are likely in amperes, though not explicitly labeled.

Overall Behavior and Trends:
- The graph exhibits an S-shaped curve, indicating a nonlinear relationship between \( I_x \) and \( V_{id} \).
- As \( V_{id} \) increases from negative to positive values, \( I_x \) transitions from \(-2I_1\) to \(2I_1\).
- The graph shows saturation behavior at both ends, where the current \( I_x \) levels off at \( \pm 2I_1 \).

Key Features and Technical Details:
- The curve is symmetric around the origin, reflecting the balanced nature of the differential pair.
- Key points include the saturation levels at \( I_x = 2I_1 \) and \( I_x = -2I_1 \).
- The linear region of the graph is centered around \( V_{id} = 0 \), where the slope is steepest, indicating high sensitivity to input voltage changes.
- The inflection points occur approximately at \( V_{id} = \pm V_{IL} \), where the curve transitions from linear to saturation.

Annotations and Specific Data Points:
- The graph is annotated with the current levels \( 2I_1 \) and \( -2I_1 \) on the vertical axis.
- The voltage levels \( \pm V_{IL} \) are marked on the horizontal axis, indicating the transition points between the linear and saturated regions.
Figure 9.50 Simplified
schematics of a two-stage
(a) bipolar and (b) MOS op amp for slew rate calculations and (c) approximate large signal transfer characteristic for the input stages in (a) and (b). For the bipolar differential pair, $V_{I L} \approx 3 V_{T}$. For the MOS differential pair, $V_{I L} \approx \sqrt{2}\left|V_{o v 1}\right|$.
if $\left|V_{i d}\right|>3 V_{T}$. For a MOS differential pair, $\left|I_{x}\right| \approx 2 I_{1}$ if $\left|V_{i d}\right|>\sqrt{2}\left|V_{o V 1}\right|$. (See Chapter 3.) Thus, when $V_{i d}=2 \mathrm{~V}$ as described above, the input stage limits and $I_{x} \approx 2 I_{1}$ (assuming that $\sqrt{2}\left|V_{o v 1}\right|<2 \mathrm{~V}$ for the MOS circuit). The circuit thus operates nonlinearly, and linear analysis fails to predict the behavior. If the input stage did act linearly, the input voltage change of 2 V would produce a very large current $I_{x}$ to charge the compensation capacitor. The fact that this current is limited to the fairly small value of $2 I_{1}$ is the reason for the slew rate being much less than a linear analysis would predict.

Consider a large input voltage applied to the circuits of Fig. 9.50 so that $I_{x}=2 I_{1}$. Then the second stage acts as an integrator with an input current $2 I_{1}$, and the output voltage $V_{o}$ can be written as

$$
\begin{equation*}
V_{o}=\frac{1}{C} \int 2 I_{1} d t \tag{9.126}
\end{equation*}
$$

and thus

$$
\begin{equation*}
\frac{d V_{o}}{d t}=\frac{2 I_{1}}{C} \tag{9.127}
\end{equation*}
$$

Equation 9.127 predicts a constant rate of change of $V_{o}$ during the slewing period, which is in agreement with the experimental observation.

The above calculation of slew rate was performed on the circuits of Fig. 9.50, which have no overall feedback. Since the input stage produces a constant output current that is independent of its input during the slewing period, the presence of a feedback connection to the input does not affect the circuit operation during this time. Thus, the slew rate of the amplifier is the same whether feedback is applied or not.

The NE5234 op amp does not quite fit the model shown in Fig. 9.50a because the output of its first stage is differential. Figure 9.51 shows a model that assumes the op-amp common-mode input voltage is low enough that $Q_{1}, Q_{2}$, and $Q_{5}-Q_{7}$ in Fig. 6.36 are off. In practice, the input step in Fig. $9.48 a$ changes the op-amp common-mode input voltage. Although this change affects the biasing of the input stage in the NE5234, it has little effect on the currents that limit the slew rate because the total current that biases the two differential pairs $Q_{1-} Q_{4}$ in Fig. 6.36
image_name:Figure 9.51 Simplified schematic of the NE5234 op amp
description::This circuit is a simplified schematic of the NE5234 op amp. It features a differential input stage with transistors Q3 and Q4, and a current mirror formed by Q9 and Q10. The circuit is biased with multiple constant current sources. Capacitors C21 and C22 are used for frequency compensation. The output is taken from the operational amplifier.

Figure 9.51 Simplified schematic of the NE5234 op amp.
is constant. Therefore, the change in the op-amp common-mode input voltage is ignored here. The three current sources at the top of Fig. 9.51 model the dc currents set by transistors $Q_{11}$, $Q_{13}$, and $Q_{14}$ in Fig. 6.36 and are assumed constant here. When $V_{i d}=0, I_{C 3}=I_{C 4}=-3 \mu \mathrm{~A}$, ignoring base currents (as is done throughout this analysis for simplicity). The negative signs here stem from the convention that defines transistor collector current as positive when it flows into the collector. To simplify the following description, let $I_{3}=-I_{C 3}$ and $I_{4}=-I_{C 4}$. Then with $V_{i d}=0, I_{3}=I_{4}=3 \mu \mathrm{~A}, I_{C 9}=I_{C 10}=6 \mu \mathrm{~A}$, and capacitor currents $I_{21}=I_{22}=0$, as shown in Fig. 9.51 and calculated in Chapter 6. Immediately after the step input in Fig. 9.48, $Q_{4}$ turns off, $I_{3}=6 \mu \mathrm{~A}$ and $I_{4}=0$. Note that the changes in $I_{3}$ and $I_{4}$ are differential in the sense that one increases and the other decreases while their average value is constant. So we will ignore the common-mode feedback circuit that controls the average voltage to ground at the first-stage outputs and assume the voltage from node Bias ${ }_{\mathrm{CM}}$ to ground ( $V_{\text {biascm }}$ ) is constant.

First, we calculate $I_{C 9}$ immediately after the input step using the assumption that $V_{\text {biascm }}$ is constant by setting $V_{R 9}+V_{b e 9}$ before and after the step equal to each other.

$$
\begin{equation*}
(3 \mu \mathrm{~A}+6 \mu \mathrm{~A}) 22 \mathrm{k} \Omega+V_{T} \ln \left(\frac{6 \mu \mathrm{~A}}{I_{S 9}}\right)=\left(6 \mu \mathrm{~A}+I_{C 9}\right) 22 \mathrm{k} \Omega+V_{T} \ln \left(\frac{I_{C 9}}{I_{S 9}}\right) \tag{9.128a}
\end{equation*}
$$

Simplifying this equation gives

$$
\begin{equation*}
0=\left(I_{C 9}-3 \mu \mathrm{~A}\right) 22 \mathrm{k} \Omega+V_{T} \ln \left(\frac{I_{C 9}}{6 \mu \mathrm{~A}}\right) \tag{9.128b}
\end{equation*}
$$

Solving this equation by trial and error gives $I_{C 9}=3.6 \mu \mathrm{~A}$. Then from KCL at node 9 , $I_{21}=6 \mu \mathrm{~A}-I_{C 9}=2.4 \mu \mathrm{~A}$. As a result, $d V_{9} / d t=2.4 \mu \mathrm{~A} / 5.2 \mathrm{pF}=0.46 \mathrm{~V} / \mu \mathrm{s}$, where $V_{9}$ is the voltage from node 9 to ground.

Next, we calculate $I_{C 10}$ immediately after the input step in a similar manner.

$$
\begin{equation*}
(3 \mu \mathrm{~A}+6 \mu \mathrm{~A}) 22 \mathrm{k} \Omega+V_{T} \ln \left(\frac{6 \mu \mathrm{~A}}{I_{S 10}}\right)=\left(I_{C 10}\right) 22 \mathrm{k} \Omega+V_{T} \ln \left(\frac{I_{C 10}}{I_{S 10}}\right) \tag{9.128c}
\end{equation*}
$$

Simplifying this equation gives

$$
\begin{equation*}
0=\left(I_{C 10}-9 \mu \mathrm{~A}\right) 22 \mathrm{k} \Omega+V_{T} \ln \left(\frac{I_{C 10}}{6 \mu \mathrm{~A}}\right) \tag{9.128d}
\end{equation*}
$$

Solving this equation by trial and error gives $I_{C 9}=8.6 \mu \mathrm{~A}$. Then from KCL at node 10 , $I_{22}=I_{C 10}-6 \mu \mathrm{~A}=2.6 \mu \mathrm{~A}$. Therefore, the voltage across $C_{22}$ increases at a rate of $d\left(V_{o}-\right.$ $\left.V_{10}\right) / d t=2.6 \mu \mathrm{~A} / 5.5 \mathrm{pF}=0.47 \mathrm{~V} / \mu \mathrm{s}$, where $V_{10}$ is the voltage from node 10 to ground. In Fig. 9.51, the amplifier that represents the second and third stages in the NE5234 has negative feedback connected around it through capacitor $C_{22}$. Assuming that the gain of this amplifier is large and that it operates linearly, $V_{o}$ is driven so that $V_{10} \simeq V_{9}$. Therefore, the slew rate of the NE5234 is

$$
\begin{equation*}
d V_{o} / d t=d V_{9} / d t+d\left(V_{o}-V_{10}\right) / d t=(0.46+0.47) \mathrm{V} / \mu \mathrm{s}=0.93 \mathrm{~V} / \mu \mathrm{s} \tag{9.128e}
\end{equation*}
$$

In contrast, the plot in Fig. $9.49 b$ shows that the simulated slew rate is about $0.68 \mathrm{~V} / \mu \mathrm{s}$, and the difference stems partly from ignoring base currents in the calculations above.

### 9.6.2 Methods of Improving Slew-Rate in Two-Stage Op Amps

In order to examine methods of slew-rate improvement, a more general analysis is required. This can be performed using the circuit of Fig. 9.52, which is a general representation of an op amp circuit. The input stage has a small-signal transconductance $g_{m I}$ and, with a large input voltage, can deliver a maximum current $I_{x m}$ to the next stage. The compensation is shown
image_name:Figure 9.52 Generalized representation of an op amp for slew-rate calculations
description:The circuit is a two-stage operational amplifier with a compensation capacitor C connected between the output of the first stage and the output of the second stage. The first stage is a voltage-controlled current source with transconductance gml, and the second stage provides a large voltage gain. The slew rate is determined by the maximum current Ix flowing through the capacitor C.

Figure 9.52 Generalized representation of an op amp for slew-rate calculations.
as the Miller effect using the capacitor $C$, since this representation describes most two-stage integrated-circuit op amps.

From Fig. 9.52 and using (9.127), we can calculate the slew rate for a large input voltage as

$$
\begin{equation*}
\frac{d V_{o}}{d t}=\frac{I_{x m}}{C} \tag{9.129}
\end{equation*}
$$

Consider now small-signal operation. For the input stage, the small-signal transconductance is

$$
\begin{equation*}
\frac{\Delta I_{x}}{\Delta V_{i}}=g_{m I} \tag{9.130}
\end{equation*}
$$

For the second stage (which acts as an integrator) the transfer function at high frequencies is

$$
\begin{equation*}
\frac{\Delta V_{o}}{\Delta I_{x}}=\frac{1}{s C} \tag{9.131a}
\end{equation*}
$$

and in the frequency domain

$$
\begin{equation*}
\frac{\Delta V_{o}}{\Delta I_{x}}(j \omega)=\frac{1}{j \omega C} \tag{9.131b}
\end{equation*}
$$

Combining (9.130) and (9.131b) gives

$$
\begin{equation*}
\frac{\Delta V_{o}}{\Delta V_{i}}(j \omega)=\frac{g_{m I}}{j \omega C} \tag{9.131c}
\end{equation*}
$$

In our previous consideration of compensation, it was shown that the small-signal, open-loop voltage gain $\left(\Delta V_{o} / \Delta V_{i}\right)(j \omega)$ must fall to unity at or before a frequency equal to the magnitude of the second most dominant pole $\left(\omega_{2}\right)$. If we assume, for ease of calculation, that the circuit is compensated for unity-gain operation with $45^{\circ}$ phase margin as shown in Fig. 9.15, the gain $\left(\Delta V_{o} / \Delta V_{i}\right)(j \omega)$ as given by $(9.131 \mathrm{c})$ must fall to unity at frequency $\omega_{2}$. (Compensation capacitor $C$ must be chosen to ensure that this occurs.) Thus from (9.131c)

$$
1=\frac{g_{m I}}{\omega_{2} C}
$$

and thus

$$
\begin{equation*}
\frac{1}{C}=\frac{\omega_{2}}{g_{m I}} \tag{9.132}
\end{equation*}
$$

Note that (9.132) was derived on the basis of a small-signal argument. This result can now be substituted in the large-signal equation (9.129) to give

$$
\begin{equation*}
\text { Slew rate }=\frac{d V_{o}}{d t}=\frac{I_{x m}}{g_{m I}} \omega_{2} \tag{9.133}
\end{equation*}
$$

Equation 9.133 allows consideration of the effect of circuit parameters on slew rate, and it is apparent that, for a given $\omega_{2}$, the ratio $I_{x m} / g_{m l}$ must be increased if slew rate is to be increased.

### 9.6.3 Improving Slew-Rate in Bipolar Op Amps

The analysis of the previous section can be applied to a bipolar op amp that uses Miller compensation. In the case of the op amp in Fig. 9.50a, we have $I_{x m}=2 I_{1}, g_{m I}=q I_{1} / k T$, and substitution in (9.133) gives

$$
\begin{equation*}
\text { Slew rate }=2 \frac{k T}{q} \omega_{2} \tag{9.134}
\end{equation*}
$$

Since both $I_{x m}$ and $g_{m I}$ are proportional to bias current $I_{1}$, the influence of $I_{1}$ cancels in the equation and slew rate is independent of $I_{1}$ for a given $\omega_{2}$. However, increasing $\omega_{2}$ will increase the slew rate, and this course is followed in most high-slew-rate circuits. The limit here is set by the frequency characteristics of the transistors in the IC process, and further improvements depend on circuit modifications as described below.

The above calculation has shown that varying the input-stage bias current of a two-stage bipolar op amp does not change the circuit slew rate. However, (9.133) indicates that for a given $I_{x m}$, slew rate can be increased by reducing the input-stage transconductance. One way this can be achieved is by including emitter-degeneration resistors to reduce $g_{m I}$ as shown in Fig. 9.53. The small-signal transconductance of this input stage can be shown to be

$$
\begin{equation*}
g_{m I}=\frac{\Delta I_{x}}{\Delta V_{i d}}=g_{m 1} \frac{1}{1+g_{m 1} R_{E}} \tag{9.135}
\end{equation*}
$$

where

$$
\begin{equation*}
g_{m 1}=\frac{q I_{1}}{k T} \tag{9.136}
\end{equation*}
$$

The value of $I_{x m}$ is still $2 I_{1}$. Substituting (9.135) in (9.133) gives

$$
\begin{equation*}
\text { Slew rate }=\frac{2 k T}{q} \omega_{2}\left(1+g_{m 1} R_{E}\right) \tag{9.137}
\end{equation*}
$$

image_name:Figure 9.53
description:
[
name: Q1, type: PNP, ports: {C: x1, B: Vin, E: e1}
name: Q2, type: PNP, ports: {C: Vo, B: x2, E: e2}
name: Q3, type: NPN, ports: {C: x1, B: x1, E: -VEE}
name: Q4, type: NPN, ports: {C: Vo, B: x1, E: -VEE}
name: RE1, type: Resistor, value: RE, ports: {N1: e1, N2: x2}
name: RE2, type: Resistor, value: RE, ports: {N1: e2, N2: x2}
name: 2I1, type: CurrentSource, value: 2I1, ports: {Np: VCC, Nn: x2}
]
extrainfo:The circuit is a differential amplifier with emitter degeneration resistors RE to improve slew rate. The current source 2I1 provides biasing for the input stage. The PNP transistors Q1 and Q2 form the differential pair, while the NPN transistors Q3 and Q4 act as active loads.

Figure 9.53 Inclusion of emitter resistors in the input stage in Fig. 9.50a to improve slew rate.

Thus the slew rate is increased by the factor $\left[1+\left(g_{m 1} R_{E}\right)\right]$ over the value given by (9.134). The fundamental reason for this is that, for a given bias current $I_{1}$, reducing $g_{m I}$ reduces the compensation capacitor $C$ required, as shown by (9.132).

The practical limit to this technique is due to the fact that the emitter resistors of Fig. 9.53 have a dc voltage across them, and mismatches in the resistor values give rise to an input dc offset voltage. The use of large-area resistors can give resistors whose values match to within 0.2 percent ( 1 part in 500). If the maximum contribution to input offset voltage allowed from the resistors is 1 mV , then these numbers indicate that the maximum voltage drop allowed is

$$
\begin{equation*}
\left.I_{1} R_{E}\right|_{\max }=500 \mathrm{mV} \tag{9.138}
\end{equation*}
$$

Thus

$$
\begin{equation*}
\left.g_{m 1} R_{E}\right|_{\max }=\left.\frac{q}{k T} I_{1} R_{E}\right|_{\max }=\frac{500}{26}=20 \tag{9.139}
\end{equation*}
$$

Using (9.139) in (9.137) shows that given these data, the maximum possible improvement in slew rate by use of emitter resistors is a factor of 21 times.

Finally, in this description of methods of slew-rate improvement, we mention the Class $A B$ input stage described by Hearn. ${ }^{21}$ In this technique, the small-signal transconductance of the input stage is left essentially unchanged, but the limit $I_{x m}$ on the maximum current available for charging the compensation capacitor is greatly increased. This is done by providing alternative paths in the input stage that become operative for large inputs and deliver large charging currents to the compensation point. This has resulted in slew rates of the order of $30 \mathrm{~V} / \mu \mathrm{s}$ in bipolar op amps , and, as in the previous cases, the limitation is an increase in input offset voltage.

### 9.6.4 Improving Slew-Rate in MOS Op Amps

A two-stage Miller-compensated MOS op amp is shown in Fig. 9.50b, and its slew rate is given by (9.127). From the analysis in Section 9.6.2, (9.133) shows that the slew rate can be increased by increasing $\omega_{2}$. On the other hand, if $\omega_{2}$ is fixed, increasing the ratio $I_{x m} / g_{m I}$ improves the slew rate. Using (1.180), (9.133) can be rewritten as

$$
\begin{equation*}
\text { Slew rate }=\frac{I_{x m}}{g_{m I}} \omega_{2}=\frac{2 I_{1}}{\sqrt{2 k^{\prime}(W / L)_{1} I_{1}}} \omega_{2}=\sqrt{\frac{2 I_{1}}{k^{\prime}(W / L)_{1}}} \omega_{2} \tag{9.140}
\end{equation*}
$$

This equation shows that the slew rate increases if $(W / L)_{1}$ decreases with $I_{1}$ constant. In this case, $g_{m I}=g_{m 1}$ decreases. From (9.132), a smaller compensation capacitor can then be used; therefore, the slew rate in (9.127) increases because $I_{1}$ is unchanged. Equation 9.140 also shows that the slew rate can be increased by increasing $I_{1}$. Assume that $I_{1}$ increases by a factor $x$ where $x>1$. Then the ratio $I_{x m} / g_{m I}$ increases by the factor $\sqrt{x}$ because $g_{m 1}$ is proportional to $\sqrt{I_{1}}$. From (9.132), the compensation capacitor must be increased by the factor $\sqrt{x}$ if $\omega_{2}$ is fixed. With these changes, the slew rate in (9.127) becomes

$$
\begin{equation*}
\frac{d V_{o}}{d t}=\frac{2 x I_{1}}{C \sqrt{x}}=\frac{2 I_{1} \sqrt{x}}{C} \tag{9.141}
\end{equation*}
$$

Since $x>1$, the slew rate is increased.
Alternatively, the ratio $I_{x m} / g_{m I}$ of the input stage can be increased by adding degeneration resistors $R_{S}$ in series with the sources of $M_{1}$ and $M_{2}$ to give

$$
\begin{equation*}
g_{m I}=\frac{g_{m 1}}{1+\left(g_{m 1}+g_{m b 1}\right) R_{S}} \tag{9.142}
\end{equation*}
$$

For fixed $I_{1}$, increasing $R_{S}$ decreases $g_{m I}$ and increases $I_{x m} / g_{m I}$, which increases the slew rate.

These approaches increase the slew rate but have some drawbacks. First, decreasing $g_{m I}$ of the input stage while keeping its bias current constant will usually lower the dc gain of the first stage and hence reduce the dc gain of the entire op amp. Also, increasing $I_{1}$ or reducing $(W / L)_{1}$ tends to increase the input-offset voltage of the op amp, as can be seen from (3.248). Finally, if source-degeneration resistors are added, mismatch between these resistors degrades the input-offset voltage.

For single-stage MOS op amps, such as the telescopic-cascode and folded-cascode op amps , the slew rate is set by the maximum output current divided by the capacitance that loads the output. The maximum output current is equal to the tail current in these op amps.

#### EXAMPLE

Find the output slew rate for the cascode op amp shown in Fig. 9.54.
Assuming the op amp has a large positive differential input voltage applied, $M_{2}$ is cutoff and $I_{\text {TAIL }}$ flows through $M_{1}$. Therefore the drain current in $M_{2 A}$ is zero, and the drain current in $M_{3}$ is $I_{d 3}=-I_{\text {TAIL }}$. The current mirror $M_{3}-M_{4}$ forces $I_{d 3}=I_{d 4}$. It follows that $I_{d 4 A}=$ $I_{d 4}=-I_{\text {TAIL }}$. The current flowing into the load capacitor $C_{L}$ is

$$
I_{o}=-I_{d 2 A}-I_{d 4 A}=-0-\left(-I_{\mathrm{TAIL}}\right)=I_{\mathrm{TAIL}}
$$

Therefore the positive output slew rate is

$$
\begin{equation*}
\frac{d V_{o}}{d t}=\frac{I_{o}}{C_{L}}=\frac{I_{\mathrm{TAIL}}}{C_{L}} \tag{9.143}
\end{equation*}
$$

Application of a large negative input forces $M_{1}$ into cutoff so $I_{\text {TAIL }}$ must flow through $M_{2}$. Therefore, $I_{d 4 A}=I_{d 4}=I_{d 3}=0$ and $I_{d 2 A}=I_{d 2}=I_{\text {TAIL }}$. The current $I_{o}$ flowing through $C_{L}$ is

$$
I_{o}=-I_{d 2 A}-I_{d 4 A}=-I_{\mathrm{TAIL}}-0=-I_{\mathrm{TAIL}}
$$

- Hence, the negative slew rate is the opposite of the value in (9.143), $-I_{\text {TAIL }} / C_{L}$.
image_name:Figure 9.54 A CMOS telescopic-cascode op amp.
description:The circuit is a CMOS telescopic-cascode operational amplifier. It uses NMOS and PMOS transistors in a cascode configuration. The output is taken across a capacitive load CL, and the current source ITAIL provides biasing. The amplifier is designed for high gain and wide bandwidth, suitable for high-speed applications.
Figure 9.54 A CMOS

telescopic-cascode op amp.
image_name:Figure 9.55
description:
[
name: CS, type: Capacitor, value: CS, ports: {Np: GND, Nn: In(Ao)}
name: Cip, type: Capacitor, value: Cip, ports: {Np: In(Ao), Nn: Ip(A0)}
name: CI, type: Capacitor, value: CI, ports: {Np: Vo, Nn: In(Ao)}
name: CL, type: Capacitor, value: CL, ports: {Np: Vo, Nn: GND}
name: Ao, type: OpAmp, value: Ao, ports: {InP: In(Ao), InN: In(Ao), OutP: Vo, OutN: Vo}
]
extrainfo:The circuit is a switched-capacitor integrator using an operational amplifier. It includes capacitors CS, Cip, CI, and CL, with the op-amp Ao providing amplification. The circuit is designed for integration during a specific clock phase (phi_2), assuming ideal MOS switches. It is suitable for use in applications with capacitive loads and feedback.
Figure 9.55 An op amp with capacitive load and feedback. This is the switchedcapacitor integrator of Fig. 6.10 $a$ during $\phi_{2}$, assuming ideal MOS switches.

CMOS op amps are often used without an output stage when the output loading is purely capacitive, as is the case in switched-capacitor circuits. Avoiding an output stage saves power and is possible because low-output resistance is not needed to drive a capacitive load. An example of such a circuit is the switched-capacitor integrator shown in Fig. 6.10a. This circuit is redrawn in Fig. 9.55 when clock phase $\phi_{2}$ is high and $\phi_{1}$ is low, assuming that MOS transistors $M_{1}-M_{4}$ behave like ideal switches. The additional capacitor $C_{i p}$ here models the total parasitic capacitance at the op-amp input and includes the input capacitance of the op amp. A question that arises is: "For the feedback circuit in Fig. 9.55, what value of output load capacitance should be used to compute the slew rate for a single-stage op amp?" When the op amp is slewing, its behavior is nonlinear. Therefore the feedback is not effective and the virtual ground at the negative op-amp input is lost. With the feedback loop broken, the total capacitance seen from the output to ground is

$$
\begin{equation*}
C_{L}+C_{I} \|\left(C_{S}+C_{i p}\right) \tag{9.144}
\end{equation*}
$$

This is the capacitance seen looking from the op-amp output node to ground, with the connection to the op-amp inverting input replaced with an open circuit. The effective output load capacitance in (9.144) is the same as the output load found when the feedback loop is broken to find the return ratio.

For the CMOS op amps considered so far in this section, the slew rate is proportional to a bias current in the op amp. A CMOS op amp with a Class AB input stage can give a slew rate that is not limited by a dc bias current in the op amp. An example ${ }^{22,23}$ is shown in Fig. 9.56. The input voltage is applied between the gates of $M_{1}, M_{2}$ and $M_{3}, M_{4}$. Transistors $M_{1}$ and $M_{4}$ act simply as unity-gain source followers to transfer the input voltage to the gates of $M_{6}$ and $M_{7}$. Diodeconnected transistors $M_{5}$ and $M_{8}$ act as level shifts, which, together with bias current sources $I_{1}$, set the quiescent Class AB current in $M_{2}, M_{3}, M_{6}$, and $M_{7}$. The currents in $M_{3}$ and $M_{7}$ are delivered to the output via cascode current mirrors $M_{9}, M_{10}, M_{13}, M_{14}$ and $M_{11}, M_{12}, M_{15}, M_{16}$. Bias currents can be determined by assuming that the input voltage $V_{i}=0$, giving

$$
\begin{equation*}
V_{G S 1}+\left|V_{G S 5}\right|=\left|V_{G S 6}\right|+V_{G S 3} \tag{9.145}
\end{equation*}
$$

Assuming that (1.157) is valid we have

$$
\begin{equation*}
V_{t n}+\sqrt{2 \frac{I_{1}}{k_{n}^{\prime}}\left(\frac{L}{W}\right)_{1}}+\left|V_{t p}\right|+\sqrt{2 \frac{I_{1}}{k_{p}^{\prime}}\left(\frac{L}{W}\right)_{5}}=\left|V_{t p}\right|+\sqrt{2 \frac{I_{B}}{k_{P}^{\prime}}\left(\frac{L}{W}\right)_{6}}+V_{t n}+\sqrt{2 \frac{I_{B}}{k_{n}^{\prime}}\left(\frac{L}{W}\right)_{3}} \tag{9.146}
\end{equation*}
$$

where $I_{B}=\left|I_{D 6}\right|=I_{D 3}=I_{D 2}=\left|I_{D 7}\right|$ is the bias current and subscripts $n$ and $p$ indicate NMOS and PMOS, respectively. The two sides of the input stage are assumed symmetrical. From (9.146) we have

$$
\begin{equation*}
\sqrt{I_{B}}\left[\sqrt{\frac{2}{k_{p}^{\prime}}\left(\frac{L}{W}\right)_{6}}+\sqrt{\frac{2}{k_{n}^{\prime}}\left(\frac{L}{W}\right)_{3}}\right]=\sqrt{I_{1}}\left[\sqrt{\frac{2}{k_{p}^{\prime}}\left(\frac{L}{W}\right)_{5}}+\sqrt{\frac{2}{k_{n}^{\prime}}\left(\frac{L}{W}\right)_{1}}\right] \tag{9.147}
\end{equation*}
$$

Equation 9.147 is the design equation for the input-stage bias current $I_{B}$.

image_name:Figure 9.56 CMOS amplifier with a Class AB input stage.
description:The circuit is a CMOS amplifier with a Class AB input stage. It uses cascode current mirrors with unity current gain. The bias currents in M9-M16 equal I_B. The input stage is designed for symmetrical operation.Figure 9.56 CMOS amplifier with a Class AB input stage.

Assuming that the cascode current mirrors in Fig. 9.56 have unity current gain, the bias currents in $M_{9}-M_{16}$ all equal $I_{B}$. To analyze this circuit, we will connect a voltage $V_{i}$ to the noninverting op-amp input and ground the inverting op-amp input. If a positive $V_{i}$ is applied, the magnitude of the currents in $M_{3}$ and $M_{6}$ increase, while the magnitude of the currents in $M_{2}$ and $M_{7}$ decrease. When mirrored to the output, these changes drive $I_{o}$ and $V_{o}$ positive. To calculate the small-signal gain, we neglect body effect. We can consider $M_{6}$ to act as source degeneration for $M_{3}$. The resistance looking into the source of $M_{6}$ is $1 / g_{m 6}$, thus

$$
\begin{equation*}
i_{d 3}=\frac{g_{m 3}}{1+\frac{g_{m 3}}{g_{m 6}}} v_{i} \tag{9.148}
\end{equation*}
$$

Similarly, $M_{2}$ acts as source degeneration for $M_{7}$, so

$$
\begin{equation*}
i_{d 7}=\frac{g_{m 7}}{1+\frac{g_{m 7}}{g_{m 2}}} v_{i}=\frac{g_{m 2}}{1+\frac{g_{m 2}}{g_{m 7}}} v_{i} \tag{9.149}
\end{equation*}
$$

where the right-most expression is found by rearranging. Thus, the transconductance of the amplifier is

$$
\begin{equation*}
G_{m}=\left.\frac{i_{o}}{v_{i}}\right|_{v_{o}=0}=\frac{i_{d 3}+i_{d 7}}{v_{i}}=\frac{2 g_{m 3}}{1+\frac{g_{m 3}}{g_{m 6}}} \tag{9.150}
\end{equation*}
$$

using $g_{m 2}=g_{m 3}$ and $g_{m 6}=g_{m 7}$. If $g_{m 3}=g_{m 6}$, then $G_{m}=g_{m 3}$.

The output resistance of this op amp is just the output resistance of the cascodes in parallel and is

$$
\begin{equation*}
R_{o} \approx\left(r_{o 14} g_{m 14} r_{o 13}\right) \|\left(r_{o 15} g_{m 15} r_{o 16}\right) \tag{9.151}
\end{equation*}
$$

Finally, the small-signal voltage gain is

$$
\begin{equation*}
A_{v}=G_{m} R_{o} \tag{9.152}
\end{equation*}
$$

The small-signal analysis above showed that a small positive $V_{i}$ causes a positive $I_{o}$. If $V_{i}$ continues to increase beyond the small-signal linear range of the input stage, $M_{2}$ and $M_{7}$ will be cut off, while $M_{3}$ and $M_{6}$ will be driven to larger values of $\left|V_{g s}\right|$. The currents in $M_{3}$ and $M_{6}$ can increase to quite large values, which gives a correspondingly large positive $I_{o}$. For large negative values of $V_{i}, M_{3}$ and $M_{6}$ turn off, $M_{2}$ and $M_{7}$ conduct large currents, and $I_{o}$ becomes large negative. Thus this circuit is capable of supplying large positive and negative currents to a load capacitance, and the magnitude of these output currents can be much larger than the bias current $I_{B}$ in the input stage. Therefore, this op amp does not display slew-rate limiting in the usual sense.

One disadvantage of this structure is that about half the transistors turn completely off during slewing. As a result, the time required to turn these transistors back on can be an important limitation to the high-frequency performance. To overcome this problem, the op amp can be designed so that the minimum drain currents are set to a nonzero value. ${ }^{24}$

### 9.6.5 Effect of Slew-Rate Limitations on Large-Signal Sinusoidal Performance

The slew-rate limitations described above can also affect the performance of the circuit when handling large sinusoidal signals at higher frequencies. Consider the circuit of Fig. 9.48 with a large sinusoidal signal applied as shown in Fig. 9.57a. Since the circuit is connected as a voltage follower, the output voltage $V_{o}$ will be forced to follow the $V_{i}$ waveform. The maximum value of $d V_{i} / d t$ occurs as the waveform crosses the axis, and if $V_{i}$ is given by

$$
\begin{equation*}
V_{i}=\hat{V}_{i} \sin \omega t \tag{9.153}
\end{equation*}
$$

then

$$
\frac{d V_{i}}{d t}=\omega \hat{V}_{i} \cos \omega t
$$

and

$$
\begin{equation*}
\left.\frac{d V_{i}}{d t}\right|_{\max }=\omega \hat{V}_{i} \tag{9.154}
\end{equation*}
$$

As long as the value of $d V_{i} /\left.d t\right|_{\max }$ given by (9.154) is less than the slew-rate limit, the output voltage will closely follow the input. However, if the product $\omega \hat{V}_{i}$ is greater than the slew-rate limit, the output voltage will be unable to follow the input, and waveform distortion of the kind shown in Fig. $9.57 b$ will result. If a sine wave with $\hat{V}_{i}$ equal to the supply voltage is applied to the amplifier, slew limiting will eventually occur as the sine-wave frequency is increased. The frequency at which this occurs is called the full-power bandwidth of the circuit. (In practice, a value of $\hat{V}_{i}$ slightly less than the supply voltage is used to avoid clipping distortion of the type described in Chapter 5.)
image_name:(a)
description:The graph labeled (a) is a time-domain waveform of a large sinusoidal input voltage applied to a circuit. The x-axis represents time \(t\), and the y-axis represents the input voltage \(V_i\). The graph is plotted in a linear scale.

**Type of Graph and Function:**
The graph is a sinusoidal waveform, representing a large input voltage applied over time.

**Axes Labels and Units:**
- **X-axis:** Time \(t\) (units not specified, typically seconds or milliseconds in such contexts).
- **Y-axis:** Input Voltage \(V_i\) (units not specified, typically volts).

**Overall Behavior and Trends:**
The waveform shows a typical sinusoidal behavior, starting from zero, reaching a peak at \(\hat{V}_i\), descending back to zero, and then going to a negative peak before returning to zero. The waveform is symmetric, indicating a consistent periodicity.

**Key Features and Technical Details:**
- The maximum voltage \(\hat{V}_i\) is marked as the peak of the waveform.
- The slope of the waveform at the steepest point is marked as \(\left| \frac{dV_i}{dt} \right|_{max}\), indicating the maximum rate of change of voltage, which is critical for understanding slew rate limitations.

**Annotations and Specific Data Points:**
- The peak voltage \(\hat{V}_i\) is annotated, showing the maximum amplitude of the input voltage.
- The maximum rate of change \(\left| \frac{dV_i}{dt} \right|_{max}\) is indicated by a tangent line at the steepest point of the waveform, illustrating the slew rate constraint that limits how fast the voltage can change.

This graph is used to illustrate the input conditions leading to slew rate limiting, which is further analyzed in the context of the amplifier's performance and bandwidth capabilities.
image_name:(b)
description:**Type of Graph and Function:**
The graph in Figure 9.57 (b) is a time-domain waveform plot, comparing the ideal and actual output voltage waveforms of an amplifier subject to slew rate limitations.

**Axes Labels and Units:**
- The horizontal axis represents time (t), though the specific units are not labeled, it is typically in seconds or microseconds for such waveforms.
- The vertical axis represents the output voltage (V_o), without specific units labeled, but typically in volts.

**Overall Behavior and Trends:**
- The dashed line represents the ideal sine wave output that the amplifier should produce if there were no slew rate limitations.
- The solid line shows the actual waveform, which deviates from the ideal sine wave due to the amplifier's slew rate limitation.
- The actual waveform shows a noticeable distortion, particularly in the rising and falling edges, where it cannot follow the rapid changes of the ideal sine wave.

**Key Features and Technical Details:**
- The distortion is most apparent at the points where the sine wave has the steepest slope, indicating the slew rate limitation.
- The maximum rate of change of the output voltage is less than that of the input sine wave, causing the actual waveform to lag behind the ideal waveform.
- This results in a rounding of the peaks and a delay in the zero crossings compared to the ideal sine wave.

**Annotations and Specific Data Points:**
- The graph includes annotations indicating the 'Actual waveform' and the 'Sine wave,' showing the difference between the ideal and real output.
- No specific numerical data points are provided on the graph, but the context implies that the slew rate is a key parameter affecting the waveform behavior.

Figure 9.57 (a) Large sinusoidal input voltage applied to the circuit of Fig. 9.48. (b) Output voltage resulting from input (a) showing slew limiting.

EXAMPLE
Calculate the full-power bandwidth of the NE5234. Use $\hat{V}_{i}=1$ V. From (9.154) put

$$
\omega \hat{V}_{i}=\text { slew rate }
$$

Using the slew rate of $0.68 \mathrm{~V} / \mathrm{\mu s}$ found in simulation gives

$$
\omega=\frac{0.68 \mathrm{~V} / \mu \mathrm{s}}{1 \mathrm{~V}}=680 \times 10^{3} \mathrm{rad} / \mathrm{s}
$$

Thus

$$
f=110 \mathrm{kHz}
$$

This means that a NE5234 op amp with a sinusoidal output of 1 V amplitude will begin to show slew-limiting distortion if the frequency exceeds 110 kHz .

## APPENDIX

### A.9.1 ANALYSIS IN TERMS OF RETURN-RATIO PARAMETERS

Much of the analysis in this chapter is based on the ideal block diagram in Fig. 9.1. This block diagram includes the forward gain $a$ and feedback $f$, which are the parameters used in two-port analysis of feedback circuits in Chapter 8. The resulting closed-loop gain expression is

$$
\begin{equation*}
A=\frac{a}{1+T}=\frac{a}{1+a f} \tag{9.155}
\end{equation*}
$$

The block diagram from return-ratio analysis in Fig. 8.42 is the same as Fig. 9.1 if $a$ is replaced by $b, f$ is replaced by $1 / A_{\infty}$, and the direct feedforward $d$ is negligible. (The contribution of feedforward through the feedback network to $a$ is also neglected in the analysis in Sections 9.2-9.5, since feedforward introduces one or more zeros into $a(s)$, but only oneand two-pole $a(s)$ are considered in these sections. Neglecting the feedforward in $a$ or the direct feedthrough $d$ is reasonable if its effect is negligible at and below the frequency where the magnitude of the loop transmission falls to 1.) The corresponding equations from return-ratio analysis are

$$
\begin{equation*}
A=\frac{b}{1+\mathscr{R}}+\frac{d}{1+\mathscr{R}} \approx \frac{b}{1+\mathscr{R}}=\frac{b}{1+\frac{b}{A_{\infty}}} \tag{9.156}
\end{equation*}
$$

For the circuit in Fig. 8.24, $0 \leq 1 / A_{\infty} \leq 1$, and $b$ is positive at low frequencies. Therefore, the equations, graphs, and relationships in Sections $9.2-9.5$ can be expressed in terms of the return-ratio variables by making the following substitutions:

$$
\begin{align*}
& a \rightarrow b  \tag{9.157a}\\
& f \rightarrow 1 / A_{\infty}  \tag{9.157b}\\
& T \rightarrow \mathscr{R}  \tag{9.157c}\\
& a f \rightarrow b / A_{\infty} \tag{9.157d}
\end{align*}
$$

The return ratio can be used to check stability of an amplifier with a single feedback loop because $A_{\infty}$ and $d$ are stable transfer functions associated with passive networks, and $\mathscr{R}(s)$ is stable because it is the signal transfer around a loop that consists of one gain stage or a cascade of stable gain stages. Therefore the zeros of $1+\mathscr{R}(s)$, which are poles of the closed-loop gain $A$, determine the stability of the feedback circuit. ${ }^{25}$ From the Nyquist stability criterion, these zeros are in the left half-plane if a polar plot of $\mathscr{R}(j \omega)$ does not encircle the point $(-1,0)$. In most cases, this stability condition is equivalent to having a positive phase margin. The phase margin is measured at the frequency where $|\Re(j \omega)|=1$.

Since the equations for two-port and return-ratio analyses are not identical, $T(s)$ and $\mathscr{R}(s)$ may be different for a given circuit. ${ }^{26}$ In general, the phase margins using $T$ and $\mathscr{R}$ may differ, but both will have the same sign and therefore will agree on the stability of the feedback circuit.

### A.9.2 ROOTS OF A QUADRATIC EQUATION

A second-order polynomial often appears in the denominator or numerator of a transfer function, and the zeros of this polynomial are the poles or zeros of the transfer function. In this appendix, the relationships between the zeros of a quadratic and its coefficients are explored for a few specific cases of interest. Also, the conditions under which a dominant root exists are derived.

Consider the roots of the quadratic equation

$$
\begin{equation*}
a s^{2}+b s+c=0 \tag{9.158}
\end{equation*}
$$

The two roots of this equation, $r_{1}$ and $r_{2}$, are given by the quadratic formula:

$$
\begin{equation*}
r_{1,2}=\frac{-b \pm \sqrt{b^{2}-4 a c}}{2 a} \tag{9.159}
\end{equation*}
$$

where it is understood that the square root of a positive quantity is positive. Factoring $b$ out of the square root and rearranging gives

$$
\begin{align*}
r_{1,2} & =-\frac{b}{2 a}\left(1 \pm \sqrt{1-\frac{4 a c}{b^{2}}}\right)  \tag{9.160a}\\
& =-\frac{b}{2 a}(1 \pm \sqrt{D}) \tag{9.160b}
\end{align*}
$$

The quantity under the square root in (9.160a) has been replaced by $D$ in (9.160b), where

$$
\begin{equation*}
D=1-\frac{4 a c}{b^{2}} \tag{9.161}
\end{equation*}
$$

Now, consider the locations of the roots if coefficients $a, b$, and $c$ all have the same sign. In this case, both roots are in the left half-plane (LHP), as will be shown next. First, note that if all the coefficients have the same sign, then

$$
\begin{equation*}
\frac{b}{2 a}>0 \tag{9.162}
\end{equation*}
$$

and

$$
\begin{equation*}
\frac{4 a c}{b^{2}}>0 \tag{9.163}
\end{equation*}
$$

Let us divide (9.163) into two different regions. First, if

$$
\begin{equation*}
0<\frac{4 a c}{b^{2}} \leq 1 \tag{9.164}
\end{equation*}
$$

then $D$ will be positive and less than one. Therefore, $\sqrt{D}<1$, so $1+\sqrt{D}$ and $1-\sqrt{D}$ are both positive. As a result, the roots are both negative and real, because $-b / 2 a<0$.

Now, consider the other region for (9.163), which is

$$
\begin{equation*}
\frac{4 a c}{b^{2}}>1 \tag{9.165}
\end{equation*}
$$

In this case, $D<0$; therefore $\sqrt{D}$ is imaginary. The roots are complex conjugates with a real part of $-b / 2 a$, which is negative. So the roots are again in the LHP. Therefore, when coefficients $a, b$, and $c$ all have the same sign, both roots are in the LHP.

Next, consider the locations of the roots if coefficients $a$ and $b$ have the same sign and $c$ has a different sign. In this case, one real root is in the right half-plane (RHP) and the other is in the LHP. To prove this, first note from (9.161) that $D>1$ here because $4 a c / b^{2}<0$. Therefore both roots are real and $\sqrt{D}>1$, so

$$
\begin{equation*}
1+\sqrt{D}>0 \tag{9.166a}
\end{equation*}
$$

and

$$
\begin{equation*}
1-\sqrt{D}<0 \tag{9.166b}
\end{equation*}
$$

Substituting into (9.160), one root will be positive and the other negative (the sign of $-b / 2 a$ is negative here).

Finally, let us consider the conditions under which LHP roots are real and widely spaced. From (9.160), real LHP roots are widely spaced if

$$
\begin{equation*}
-\frac{b}{2 a}(1+\sqrt{D}) \ll-\frac{b}{2 a}(1-\sqrt{D}) \tag{9.167}
\end{equation*}
$$

or

$$
\begin{equation*}
1+\sqrt{D} \gg 1-\sqrt{D} \tag{9.168}
\end{equation*}
$$

Substituting the expression for $D$ in (9.161) into (9.168) and simplifying leads to an equivalent condition for widely spaced roots, which is

$$
\begin{equation*}
\frac{4 a c}{b^{2}} \ll 1 \tag{9.169}
\end{equation*}
$$

Under this condition, one root is

$$
\begin{equation*}
r_{2}=-\frac{b}{2 a}(1+\sqrt{D}) \approx-\frac{b}{2 a}(1+1)=-\frac{b}{a} \tag{9.170a}
\end{equation*}
$$

The other root is

$$
\begin{align*}
r_{1} & =-\frac{b}{2 a}(1-\sqrt{D}) \\
& =-\frac{b}{2 a}\left(1-\sqrt{1-\frac{4 a c}{b^{2}}}\right)  \tag{9.170b}\\
& \approx-\frac{b}{2 a}\left(1-\left(1-\frac{4 a c}{2 b^{2}}\right)\right) \\
& =-\frac{c}{b}
\end{align*}
$$

where the approximation

$$
\begin{equation*}
\sqrt{1-x} \approx 1-\frac{x}{2} \quad \text { for } \quad|x| \ll 1 \tag{9.171}
\end{equation*}
$$

has been used. Here, $\left|r_{1}\right| \ll\left|r_{2}\right|$ because $\left|r_{1}\right| \approx c / b \ll b / a \approx\left|r_{2}\right|$ (which follows from $\left.4 a c / b^{2} \ll 1\right)$. If these roots are poles, $r_{1}$ corresponds to the dominant pole, and $r_{2}$ gives the nondominant pole. Equations 9.170a and 9.170 b are in agreement with (9.30) through (9.33).

Table 9.1 summarizes the location of the roots of (9.158) for the cases considered in this appendix. When both roots are in the LHP, the roots are both real if (9.164) is satisfied. These roots are widely spaced if (9.169) is satisfied.

Table 9.1

| Sign of Coefficient Values in (9.158) |  | Roots |  |
| :---: | :---: | :---: | :--- |
| $a$ | $b$ | $c$ |  |
| + | + | + | Both in LHP |
| - | - | - | Both in LHP |
| + | + | - | One in LHP, one in RHP |
| - | - | + | One in LHP, one in RHP |

## REFERENCES

1. K. Ogata. Modern Control Engineering, 2nd Edition. Prentice-Hall, Englewood Cliffs, NJ, 1990.
2. P. W. Tuinenga. SPICE: A Guide to Circuit Simulation and Analysis using PSPICE, 3rd Edition. Prentice-Hall, Englewood Cliffs, NJ, 1995.
3. G. W. Roberts and A. S. Sedra. SPICE, 2nd Edition. Oxford Press, New York, 1997.
4. P. J. Hurst. "Exact Simulation of Feedback Circuit Parameters," IEEE Trans. on Circuits and Systems, Vol. CAS-38, No. 11, pp. 1382-1389, November 1991.
5. P. J. Hurst and S.H. Lewis. "Determination of Stability Using Return Ratios in Balanced Fully Differential Feedback Circuits," IEEE Trans. on Circuits and Systems II, pp. 805-817, December 1995.
6. S. Rosenstark. Feedback Amplifier Principles, MacMillan, New York, 1986.
7. R. D. Middlebrook. "Measurement of Loop Gain in Feedback Systems," Int. J. Electronics, Vol. 38, No. 4, pp. 485-512, 1975.
8. J. E. Solomon. "The Monolithic Op Amp: A Tutorial Study," IEEE J. Solid-State Circuits, Vol. SC-9, pp. 314-332, December 1974.

Figure 9.65 Circuit for Problem 9.45.
9.46 Consider a two-stage CMOS op amp modeled by the equivalent circuit in Fig. 9.18, where $i_{s}=g_{m} v_{i d}$ and $v_{i d}$ is the differential op-amp input. Let $g_{m}=19.7 \mathrm{~mA} / \mathrm{V}, R_{1}=R_{2}=6.67 \mathrm{k} \Omega$, and $C_{1}=$ $C_{2}=C=2 \mathrm{pF}$. Calculate and sketch the root locus when feedback is applied as $f$ varies from 0 to 1 . Calculate the real component of $s$ for which the poles become complex. Is the amplifier unconditionally stable? If yes, calculate the pole positions for unity-gain feedback. If no, find the loop gain required to cause instability.
9. Y. P. Tsividis and P.R. Gray. "An Integrated NMOS Operational Amplifier with Internal Compensation," IEEE J. Solid-State Circuits, Vol. SC-11, pp. 748-753, December 1976.
10. B. K. Ahuja. "An Improved Frequency Compensation Technique for CMOS Operational Amplifiers," IEEE J. Solid-State Circuits, Vol. SC-18, pp. 629-633, December 1983.
11. D. B. Ribner and M. A. Copeland. "Design Techniques for Cascoded CMOS Op Amps with Improved PSRR and Common-Mode Input Range," IEEE J. Solid-State Circuits, pp. 919-925, December 1984.
12. D. Senderowicz, D. A. Hodges, and P. R. Gray. "A High-Performance NMOS Operational Amplifier," IEEE J. Solid-State Circuits, Vol. SC-13, pp. 760-768, December 1978.
13. W. C. Black, D. J. Allstot, and R. A. Reed. "A High Performance Low Power CMOS Channel Filter," IEEE J. Solid-State Circuits, Vol. SC-15, pp. 929-938, December 1980.
14. E. M. Cherry. "A New Result in Negative Feedback Theory and Its Application to Audio Power Amplifiers," Int. J. Circuit Theory, Vol. 6, pp. 265288, July 1978.
15. J. H. Huijsing and D. Linebarger. "LowVoltage Operational Amplifier with Rail-to-Rail Input and Output Ranges," IEEE J. Solid-State Circuits, Vol. 20, pp. 1144-1150. December 1985.
16. R. G. H. Eschauzier and J. H. Huijsing. Frequency Compensation Techniques for Low-Power Operational Amplifiers. Kluwer, Dordrecht, The Netherlands, 1995.
17. M. J. Fonderie and J. H. Huijsing. Design of Low-Voltage Bipolar Operational Amplifiers. Kluwer Academic Publishers, Boston, 1993.
18. F. You, H. K. Embabi, and E. SanchezSinencio. "A Multistage Amplifier Topology with Nested Gm-C Compensation," IEEE J. SolidState Circuits, Vol. 32, pp. 2000-2011, December 1997.
19. P. E. Gray and C. L. Searle. Electronic Principles: Physics, Models, and Circuits. Wiley, New York, 1969.
20. J. D'Azzo and C. Houpis. Linear Control System Analysis and Design: Conventional and Modern. McGraw-Hill, New York, 1975.
21. W. E. Hearn. "Fast Slewing Monolithic Operational Amplifier," IEEE J. Solid-State Circuits, Vol. SC-6, pp. 20-24, February 1971.
22. P. W. Li, M. J. Chin, P. R. Gray, and R. Castello. "A Ratio-Independent Algorithmic Analog-to-Digital Conversion Technique," IEEE J. Solid-State Circuits, Vol. SC-19, pp. 828-836, December 1984.
23. E. Seevinck and R. Wassenaar. "A Versatile CMOS Linear Transconductor/Square-Law Function Circuit," IEEE J. Solid-State Circuits, Vol. SC-22, pp. 366-377, June 1987.
24. F.N.L. O. Eynde, P.F. M. Ampe, L. Verdeyen, and W. M. C. Sansen. "A CMOS Large-Swing LowDistortion Three-Stage Class AB Power Amplifier," IEEE J. Solid-State Circuits, Vol. SC-25, pp. 265-273, February 1990.
25. H. W. Bode. Network Analysis and Feedback Amplifier Design. Van Nostrand, New York, 1945.
26. P. J. Hurst. "A Comparison of Two Approaches to Feedback Circuit Analysis," IEEE Trans. on Education, Vol. 35, No. 3, pp. 253-261, August 1992.
