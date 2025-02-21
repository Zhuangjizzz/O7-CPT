# CHAPTER 10 Stability and Frequency Compensation

Negative feedback finds wide application in the processing of analog signals. As described in Chapter 8, feedback suppresses the effect of the variations of the open-loop characteristics. Feedback systems, however, suffer from potential instability; that is, they may oscillate.

In this chapter, we deal with the stability and frequency compensation of linear feedback systems to the extent necessary to understand the design issues of analog feedback circuits. Beginning with a review of stability criteria and the concept of phase margin, we study frequency compensation, introducing various techniques suited to different op amp topologies. We also analyze the impact of frequency compensation on the slew rate of two-stage op amps. The chapter ends with a study of Nyquist's stability criterion.

## 10.1 ■ General Considerations

Let us consider the negative-feedback system shown in Fig. 10.1(a), where $\beta$ is assumed constant. Writing the closed-loop transfer function as

$$
\begin{equation*}
\frac{Y}{X}(s)=\frac{H(s)}{1+\beta H(s)} \tag{10.1}
\end{equation*}
$$

we note that if $\beta H\left(s=j \omega_{1}\right)=-1$ at $\omega_{1} \neq 0$, then the closed-loop "gain" goes to infinity, and the circuit can amplify its own noise until it eventually begins to oscillate. In other words, if the loop gain at $\omega_{1}, \beta H\left(j \omega_{1}\right)$, is equal to -1 , then the circuit may oscillate at frequency $\omega_{1}$. This condition can be expressed as

$$
\begin{align*}
& \left|\beta H\left(j \omega_{1}\right)\right|=1  \tag{10.2}\\
& \angle \beta H\left(j \omega_{1}\right)=-180^{\circ} \tag{10.3}
\end{align*}
$$

image_name:(a)
description:The diagram labeled "(a)" represents a basic negative-feedback system.

1. **Main Components:**
- **Summing Junction (+):** This is where the input signal \(X(s)\) and the feedback signal are combined. The summing junction adds the input signal and subtracts the feedback signal.
- **Forward Path Transfer Function \(H(s)\):** This block represents the system or plant being controlled, which processes the signal from the summing junction and generates the output \(Y(s)\).
- **Feedback Path with Gain \(\beta\):** This block takes a portion of the output \(Y(s)\), scales it by the feedback factor \(\beta\), and feeds it back to the summing junction.

2. **Flow of Information or Control:**
- The input signal \(X(s)\) enters the summing junction.
- The summing junction computes the difference between \(X(s)\) and the feedback signal (scaled by \(\beta\)).
- The resulting signal is processed by the forward path \(H(s)\), producing the output \(Y(s)\).
- A portion of \(Y(s)\) is fed back through the feedback path, scaled by \(\beta\), and subtracted from the input at the summing junction.

3. **Labels, Annotations, and Key Indicators:**
- The input and output signals are labeled as \(X(s)\) and \(Y(s)\), respectively.
- The feedback gain is denoted as \(\beta\).
- The forward path transfer function is represented by \(H(s)\).

4. **Overall System Function:**
- This system is designed to regulate its output \(Y(s)\) based on the input \(X(s)\) and the feedback signal. By adjusting the feedback gain \(\beta\), the system can control the stability and response characteristics of the output. The negative feedback loop helps in maintaining desired system performance by reducing the error between the input and the feedback signal.
image_name:(b)
description:The system block diagram labeled (b) represents a basic negative-feedback system with a focus on phase shift around the loop at a specific frequency, \( \omega_{1} \). The main components of this diagram include:

1. **Summing Junction**: This is the point where the input signal \( X(s) \) and the feedback signal are combined. The summing junction has two inputs: the main input signal \( X(s) \) and the feedback signal, which is subtracted from the main signal.

2. **Transfer Function Block \( H(s) \)**: This block processes the signal from the summing junction. It represents the system's transfer function, which dictates how the input signal is transformed into the output signal \( Y(s) \).

3. **Feedback Path**: This path includes a feedback transfer function \( \beta \), which takes a portion of the output signal \( Y(s) \) and feeds it back to the summing junction. The feedback path introduces a phase shift of 180 degrees.

4. **Phase Shift Indicator**: The diagram highlights that there is an additional 180-degree phase shift introduced by the system itself, making the total phase shift around the loop 360 degrees at frequency \( \omega_{1} \).

**Flow of Information**:
- The input signal \( X(s) \) enters the summing junction where it is combined with the feedback signal.
- The resultant signal is then processed by the transfer function \( H(s) \), producing the output signal \( Y(s) \).
- A portion of \( Y(s) \) is fed back through the feedback path with a gain of \( \beta \) and a phase shift of 180 degrees.

**Overall System Function**:
The primary function of this system is to maintain stability and control the amplification of signals by ensuring the total phase shift around the feedback loop is 360 degrees. This is in line with Barkhausen's Criteria for oscillation, where the magnitude of the loop gain is 1, and the phase shift is -180 degrees, effectively making it 360 degrees when considering the negative feedback. This setup is crucial for understanding conditions under which the system may begin to oscillate at a particular frequency, \( \omega_{1} \).

Figure 10.1 (a) Basic negative-feedback system, and (b) phase shift around the loop at $\omega_{1}$.
which are called "Barkhausen's Criteria." Note that (1) these equations relate only to the loop gain (more precisely, the loop transmission) ${ }^{1}$ and are independent of where the input and output are located, and (2) the total phase shift around the loop at $\omega_{1}$ is $360^{\circ}$ because negative feedback itself introduces $180^{\circ}$ of phase shift [Fig. 10.1(b)]. The $360^{\circ}$ phase shift is necessary for oscillation since the feedback signal must add in phase to the original noise to allow oscillation buildup. By the same token, a loop gain of unity (or greater) is also required to enable growth of the oscillation amplitude. These oscillation requirements are studied further in Chapter 15. The key point here is that the loop transmission, which can often be found from the open-loop system, reveals the stability of the closed-loop system.

In summary, a negative-feedback system may oscillate at $\omega_{1}$ if (1) the phase shift around the loop at this frequency is so great that the feedback becomes positive and (2) the loop gain is still enough to allow signal buildup. Illustrated in Fig. 10.2(a), the situation can be viewed as excessive loop gain at the frequency at which the phase shift reaches $-180^{\circ}$ or, equivalently, excessive phase at the frequency at which the loop gain drops to unity. Thus, to avoid instability, we must minimize the total phase shift so that if $|\beta H|=1$, then $\angle \beta H$ is still more positive than $-180^{\circ}$ [Fig. 10.2(b)]. In this chapter, we assume that $\beta$ is less than or equal to unity and does not depend on the frequency.
image_name:10.2(a)
description:The graph labeled "10.2(a)" is a Bode plot illustrating the characteristics of an unstable system. It consists of two separate plots: one for the magnitude of the loop gain and another for the phase. Both plots use a logarithmic scale for frequency, denoted as \( \omega \).

1. **Magnitude Plot:**
- **Vertical Axis:** Represents \( 20\log|\beta H(\omega)| \), which is the gain of the system in decibels (dB).
- **Horizontal Axis:** Frequency \( \omega \) on a logarithmic scale.
- **Behavior:** The magnitude starts at a certain level and decreases as frequency increases. The gain crosses the 0 dB line at frequency \( \omega_1 \), indicating the gain crossover frequency.
- **Key Feature:** The gain at \( \omega_2 \) is still positive, indicating excessive gain at this frequency.

2. **Phase Plot:**
- **Vertical Axis:** Represents the phase angle \( \angle \beta H(\omega) \) in degrees.
- **Horizontal Axis:** Frequency \( \omega \) on a logarithmic scale.
- **Behavior:** The phase decreases and crosses the \(-180^{\circ}\) line, indicating the phase crossover frequency occurs at \( \omega_2 \).
- **Key Feature:** The phase is excessively negative at the frequency where the gain is still positive, contributing to instability.

3. **Annotations and Observations:**
- The plot is labeled "Unstable" due to the excessive gain and phase shift.
- Annotations indicate "Excessive Gain" and "Excessive Phase" at the respective frequencies, highlighting the instability issues.

Overall, this Bode plot demonstrates that the gain crossover occurs after the phase crossover, leading to instability, as the phase at unity gain is more negative than \(-180^{\circ}\).
image_name:10.2(b)
description:The graph labeled "10.2(b)" is a Bode plot depicting the loop transmission characteristics of a stable system. It consists of two plots: the magnitude plot at the top and the phase plot at the bottom, both plotted against frequency on a logarithmic scale.

1. **Magnitude Plot:**
- **Y-Axis:** Represents the magnitude of the loop gain, denoted as \(20\log|\beta H(\omega)|\), measured in decibels (dB).
- **X-Axis:** Represents frequency \(\omega\) on a logarithmic scale.
- **Behavior:** The magnitude starts at a positive value and decreases as frequency increases. It crosses the 0 dB line, indicating the gain crossover frequency.

2. **Phase Plot:**
- **Y-Axis:** Represents the phase of the loop gain, denoted as \(\angle \beta H(\omega)\), measured in degrees.
- **X-Axis:** Represents frequency \(\omega\) on a logarithmic scale.
- **Behavior:** The phase starts near 0 degrees and decreases, approaching but not reaching \(-180^{\circ}\). The phase remains more positive than \(-180^{\circ}\) at the gain crossover frequency, indicating stability.

3. **Overall Stability:**
- The gain crossover frequency occurs before the phase crosses \(-180^{\circ}\), maintaining a positive phase margin, which is crucial for stability.
- There are no annotations indicating excessive gain or phase, unlike in the unstable system plot (10.2(a)).

4. **Key Features:**
- The phase margin is the difference between the phase at the gain crossover frequency and \(-180^{\circ}\). This margin ensures that the system remains stable.
- The plot demonstrates a typical stable system where the phase does not reach \(-180^{\circ}\) at the point where the magnitude is 0 dB, thus preventing oscillations or instability.

Figure 10.2 Bode plots of loop transmission for (a) unstable and (b) stable systems.

The frequencies at which the magnitude and phase of the loop gain are equal to unity and $-180^{\circ}$, respectively, play a critical role in the stability and are called the "gain crossover frequency" and the "phase crossover frequency," respectively. In a stable system, the gain crossover must occur well before the phase crossover. For the sake of brevity, we denote the gain crossover by GX and the phase crossover by PX. It is helpful to note that the gain crossover frequency is the same as the unity-gain bandwidth of the loop transmission.

#### Example 10.1

Explain whether the system depicted in Fig. 10.2(a) becomes more or less stable if the feedback is weakened, i.e., if $\beta$ is reduced.

#### Solution

As illustrated in Fig. 10.3, a lower $\beta$ shifts the plot of $20 \log |\beta H(\omega)|$ down and the GX to the left. Since $\angle \beta H(\omega)$ does not change, the system becomes more stable. After all, if we apply no feedback around an op amp, the circuit has no tendency to oscillate. Thus, the worst-case stability corresponds to $\beta=1$, i.e, unity-gain feedback. For this reason, we often analyze the magnitude and phase plots for $\beta H=H$.
image_name:Figure 10.3
description:Figure 10.3 is a Bode plot, which consists of two graphs: one for magnitude and one for phase, both plotted against frequency on a logarithmic scale. The x-axis for both graphs is labeled as "log ω," representing the logarithm of angular frequency ω. The y-axis of the upper graph is labeled "20 log |βH(ω)|," which shows the magnitude of the transfer function in decibels (dB). The y-axis of the lower graph is labeled "∠βH(ω)," which represents the phase angle of the transfer function.

**Magnitude Plot:**
- The magnitude plot displays two curves. The black curve represents a higher β value, while the gray curve labeled "Lower β" represents a reduced β value.
- Both curves start at the same level but diverge as frequency increases. The black curve maintains a higher magnitude compared to the gray curve.
- The slope of the curves changes at certain frequencies, indicating the presence of poles or zeros.
- The gray curve is shifted downward, indicating a lower magnitude for the reduced β value across the frequency spectrum.

**Phase Plot:**
- The phase plot shows a single curve, which remains unchanged regardless of β value, consistent with the context that the phase angle of βH(ω) does not change.
- The phase angle decreases with increasing frequency, showing typical phase lag behavior as frequency increases.

**Key Features:**
- The point where the magnitude plot crosses 0 dB is critical for stability analysis, as it indicates the gain crossover frequency.
- The phase plot is crucial for determining phase margin, which affects system stability.
- The dashed vertical lines connect corresponding points on the magnitude and phase plots, highlighting specific frequencies where changes occur.

Overall, the plot illustrates how reducing β shifts the magnitude plot downward, potentially increasing system stability by moving the gain crossover frequency to the left, while the phase plot remains constant.

Before studying more specific cases, let us review a few basic rules for constructing Bode plots. A Bode plot illustrates the asymptotic behavior of the magnitude and phase of a complex function according to the magnitude of the poles and zeros. The following two rules are used. (1) The slope of the magnitude plot changes by $+20 \mathrm{~dB} / \mathrm{dec}$ at every zero frequency and by $-20 \mathrm{~dB} / \mathrm{dec}$ at every pole frequency. (2) For a pole (zero) frequency of $\omega_{m}$, the phase begins to fall (rise) at approximately $0.1 \omega_{m}$, experiences a change of $-45^{\circ}\left(+45^{\circ}\right)$ at $\omega_{m}$, and approaches a change of $-90^{\circ}\left(+90^{\circ}\right)$ at approximately $10 \omega_{m}$. The key point here is that the phase is much more significantly affected by high-frequency poles and zeros than the magnitude is.

It is also instructive to plot the location of the poles of a closed-loop system on a complex plane. Expressing each pole frequency as $s_{p}=j \omega_{p}+\sigma_{p}$ and noting that the impulse response of the system includes a term $\exp \left(j \omega_{p}+\sigma_{p}\right) t$, we observe that if $s_{p}$ falls in the right half plane (RHP), i.e., if $\sigma_{p}>0$, then the system oscillates because its time-domain response exhibits a growing exponential [Fig. 10.4(a)]. Even if $\sigma_{p}=0$, the system sustains oscillations [Fig. 10.4(b)]. Conversely, if the poles lie in the left half plane (LHP), all time-domain exponential terms decay to zero [Fig. 10.4(c)]. ${ }^{2}$ In practice, we plot the location of the poles as the loop gain varies, thereby revealing how close to oscillation the system may come. Such a plot is called a "root locus."

We now study a feedback system incorporating a one-pole forward amplifier. Assuming $H(s)=$ $A_{0} /\left(1+s / \omega_{0}\right)$, we have from $(10.1)$

$$
\begin{equation*}
\frac{Y}{X}(s)=\frac{\frac{A_{0}}{1+\beta A_{0}}}{1+\frac{s}{\omega_{0}\left(1+\beta A_{0}\right)}} \tag{10.4}
\end{equation*}
$$

image_name:(a) unstable with growing amplitude
description:The graph labeled "(a)" consists of two parts: a pole-zero plot on the left and a time-domain waveform on the right.

1. **Type of Graph and Function:**
- The left part is a pole-zero plot in the complex plane, often used in control theory and signal processing to analyze system stability.
- The right part is a time-domain waveform showing the system's response over time.

2. **Axes Labels and Units:**
- **Pole-Zero Plot:**
- The vertical axis is labeled \( j\omega \), representing the imaginary part of the complex frequency.
- The horizontal axis is labeled \( \sigma \), representing the real part of the complex frequency.
- **Time-Domain Waveform:**
- The horizontal axis is labeled \( t \), representing time.
- The amplitude is plotted on the vertical axis with no specific units mentioned.

3. **Overall Behavior and Trends:**
- **Pole-Zero Plot:**
- Two poles are symmetrically placed along the imaginary axis at \( +\omega_p \) and \( -\omega_p \), with a real component \( \sigma_p \) indicating positive feedback.
- **Time-Domain Waveform:**
- The waveform exhibits growing oscillations, indicating an unstable system. The amplitude of the oscillations increases exponentially over time, following an envelope described by \( e^{\sigma_p t} \).

4. **Key Features and Technical Details:**
- The poles on the plot indicate that the system is unstable due to their location in the right half of the complex plane (positive real part \( \sigma_p \)).
- The system's response in the time domain is characterized by increasing oscillations, suggesting that any disturbance will lead to unbounded growth in amplitude.

5. **Annotations and Specific Data Points:**
- The exponential growth of the oscillations is depicted with a dashed line labeled \( e^{\sigma_p t} \) on the time-domain waveform.
- No specific numerical values are provided for \( \sigma_p \) or \( \omega_p \), but their positive values are implied by the growth in amplitude.
image_name:(b) unstable with constant-amplitude oscillation
description:The graph labeled "(b)" is a time-domain waveform illustrating the behavior of a system with constant-amplitude oscillation. This plot is typically used to represent the response of a system where the poles are located on the imaginary axis of the complex plane, indicating marginal stability.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform showing oscillatory behavior.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as time \( t \), though specific units are not provided. It represents the progression of time.
- The vertical axis represents the amplitude of the oscillation, but specific units are not given.

3. **Overall Behavior and Trends:**
- The waveform displays a constant amplitude oscillation, indicating that the system is neither growing nor decaying in amplitude over time.
- The oscillation is sinusoidal, maintaining a consistent frequency throughout the time axis.

4. **Key Features and Technical Details:**
- The poles are located at \(+j\omega_p\) and \(-j\omega_p\) on the imaginary axis, indicating that there is no real part contributing to exponential growth or decay.
- The system is marginally stable, as the poles are precisely on the imaginary axis, which typically leads to sustained oscillations without damping or amplification.

5. **Annotations and Specific Data Points:**
- The diagram does not provide specific numerical values for frequency or amplitude, but the presence of poles on the imaginary axis is a critical feature indicating the nature of the oscillation.
- There are no additional annotations or markers indicating specific time points or amplitude levels.
image_name:(c)stable.
description:The graph labeled (c) in the image illustrates the time-domain response of a stable system based on the position of poles in the complex plane.

1. **Type of Graph and Function**:
- This is a time-domain waveform graph, showing the response of a system over time.
- It is associated with the root locus method, indicating system stability.

2. **Axes Labels and Units**:
- The left part of the graph is a pole-zero plot on the complex plane with the vertical axis labeled as \( j\omega \) (imaginary axis) and the horizontal axis labeled as \( \sigma \) (real axis).
- The right part of the graph is a time-domain plot with the horizontal axis labeled as \( t \) (time).

3. **Overall Behavior and Trends**:
- The poles are located on the left half of the complex plane, indicating a stable system.
- The time-domain response on the right shows a decaying oscillation, which suggests that the system is stable and the oscillations diminish over time.

4. **Key Features and Technical Details**:
- The poles are positioned symmetrically about the real axis, with a negative real part \( \sigma_p \), ensuring stability as they are located in the left half-plane.
- The oscillation in the time-domain response decays exponentially, as indicated by the envelope \( e^{\sigma_p t} \).
- The system's response starts with a higher amplitude and gradually decreases, eventually settling to zero.

5. **Annotations and Specific Data Points**:
- The graph indicates the exponential decay with dotted lines showing the envelope of the oscillations.
- The poles are marked with crosses on the complex plane, and the distance from the origin indicates the natural frequency \( \omega_p \).
- The annotations \( e^{\sigma_p t} \) highlight the decaying nature of the oscillations.

Figure 10.4 Time-domain response of a system versus the position of poles: (a) unstable with growing amplitude; (b) unstable with constant-amplitude oscillation; (c) stable.

In order to analyze the stability behavior, we plot $|\beta H(s=j \omega)|$ and $\angle \beta H(s=j \omega)$ (Fig. 10.5), observing that a single pole cannot contribute a phase shift greater than $90^{\circ}$ and the system is unconditionally stable for all nonnegative values of $\beta$. Note that $\angle \beta H$ is independent of $\beta$.
image_name:Figure 10.5 Bode plots of loop transmission for a one-pole system
description:Figure 10.5 consists of two Bode plots for a one-pole system, illustrating the magnitude and phase of the loop transmission function $\beta H(s=j\omega)$ as a function of frequency $\omega$. Both plots use a logarithmic scale for the frequency axis.

1. **Magnitude Plot (Top):**
- **Y-Axis:** The vertical axis represents the magnitude of the loop transmission in decibels (dB), denoted as $20\log|\beta H(\omega)|$.
- **X-Axis:** The horizontal axis represents frequency $\omega$ on a logarithmic scale.
- **Behavior:** The plot starts at a constant level of $20\log\beta A_0$ up to a certain cutoff frequency $\omega_0$. At $\omega_0$, the plot begins to slope downward, indicating a decrease in gain with increasing frequency.
- **Trend:** The slope beyond $\omega_0$ is characteristic of a one-pole system, showing a decrease in gain at a rate of -20 dB/decade.

2. **Phase Plot (Bottom):**
- **Y-Axis:** The vertical axis represents the phase angle of the loop transmission in degrees, denoted as $\angle \beta H(\omega)$.
- **X-Axis:** The horizontal axis represents frequency $\omega$ on a logarithmic scale.
- **Behavior:** The phase starts at 0 degrees and begins to decrease as frequency increases, passing through -45 degrees at frequency $\omega_0$ and approaching -90 degrees asymptotically.
- **Trend:** The phase plot shows the typical behavior of a single-pole system, where the phase shift is limited to -90 degrees.

3. **Key Features:**
- **Cutoff Frequency ($\omega_0$):** This is the frequency at which the magnitude plot begins to decline and the phase is at -45 degrees.
- **Slope:** The magnitude plot has a slope of -20 dB/decade after $\omega_0$, indicating the rate of gain reduction.
- **Phase Shift Limitation:** The phase shift does not exceed -90 degrees, which is typical for a one-pole system.

These plots together provide insight into the stability and frequency response characteristics of the system, with the one-pole nature ensuring a predictable and gradual phase shift and gain reduction beyond the cutoff frequency.

#### Example 10.2

Construct the root locus for a one-pole system.

#### Solution

Equation (10.4) implies that the closed-loop system has a pole $s_{p}=-\omega_{0}\left(1+\beta A_{0}\right)$, i.e., a real-valued pole in the left half plane that moves away from the origin as the loop gain increases (Fig. 10.6).
image_name:Figure 10.6
description:**Type of Graph and Function:**
The graph is a root locus plot for a one-pole system, illustrating the movement of poles in the s-plane as the loop gain of the system changes.

**Axes Labels and Units:**
- The horizontal axis is labeled \( \sigma \), representing the real part of the complex frequency \( s \).
- The vertical axis is labeled \( j\omega \), representing the imaginary part of the complex frequency \( s \).
- Units are not explicitly mentioned, but \( \sigma \) and \( j\omega \) are typically in radians per second.

**Overall Behavior and Trends:**
The graph shows a single trajectory along the real axis, moving from left to right as the parameter \( \beta \) changes. This indicates that the pole starts at a certain point on the real axis and moves towards the right as the loop gain increases.

**Key Features and Technical Details:**
- The starting point of the pole is marked as \( -\omega_0 \), indicating the initial position of the pole when the loop gain is zero.
- The trajectory moves along the real axis, suggesting a real-valued pole that shifts without any imaginary component.
- A cross (×) is marked at the point where \( \beta = 0 \), indicating the position of the pole when the feedback factor \( \beta \) is zero.
- The direction of movement is indicated by arrows pointing to the right along the real axis.

**Annotations and Specific Data Points:**
- The graph is annotated with arrows labeled \( \beta \), showing the direction of increasing loop gain.
- The point \( -\omega_0 \) is a critical value, representing the initial pole position in the left half of the s-plane.
- The graph emphasizes the movement of the pole away from the origin as the loop gain increases, reflecting the stability characteristics of a one-pole system.

## 10.2 ■ Multipole Systems

Our study of op amps in Chapter 9 indicates that such circuits generally contain multiple poles. In twostage op amps, for example, each gain stage introduces a "dominant" pole. It is therefore important to study a feedback system whose core amplifier exhibits more than one pole.

Let us consider a two-pole system first. For stability considerations, we plot $|\beta H|$ and $\angle \beta H$ as a function of the frequency. Shown in Fig. 10.7, the magnitude begins to drop at $20 \mathrm{~dB} / \mathrm{dec}$ at $\omega=\omega_{p 1}$ and at $40 \mathrm{~dB} / \mathrm{dec}$ at $\omega=\omega_{p 2}$. Also, the phase begins to change at $\omega=0.1 \omega_{p 1}$, reaches $-45^{\circ}$ at $\omega=\omega_{p 1}$ and $-90^{\circ}$ at $\omega=10 \omega_{p 1}$, begins to change again at $\omega=0.1 \omega_{p 2}$ (if $0.1 \omega_{p 2}>10 \omega_{p 1}$ ), reaches $-135^{\circ}$ at $\omega=\omega_{p 2}$, and asymptotically approaches $-180^{\circ}$. The system is therefore stable because $|\beta H|$ drops to below unity at a frequency where $\angle \beta H<-180^{\circ}$.
image_name:Figure 10.7 Bode plots of loop transmission for a two-pole system
description:The graph depicted is a Bode plot, which consists of two subplots: the magnitude plot and the phase plot, for a two-pole system. Both plots have a horizontal axis representing frequency \( \omega \) on a logarithmic scale.

**Magnitude Plot:**
- The vertical axis is labeled as \( 20 \log |\beta H(\omega)| \), representing the magnitude of the loop transmission in decibels (dB).
- The plot starts with a flat region, indicating a constant magnitude at low frequencies.
- At the first pole \( \omega_{p1} \), the magnitude begins to decrease at a rate of \(-20\) dB/decade.
- At the second pole \( \omega_{p2} \), the slope increases to \(-40\) dB/decade.
- A gain crossover point is marked where the magnitude crosses 0 dB, indicating the frequency at which the gain is unity.
- A gray line represents a scenario with weaker feedback (lower \( \beta \)), showing a reduced magnitude across frequencies and an earlier gain crossover point.

**Phase Plot:**
- The vertical axis represents the phase angle \( \angle \beta H(\omega) \) in degrees.
- Initially, the phase is 0° and begins to decrease as frequency increases.
- At \( \omega = 0.1 \omega_{p1} \), the phase starts changing, reaching \(-45^{\circ}\) at \( \omega_{p1} \) and \(-90^{\circ}\) at \( 10 \omega_{p1} \).
- The phase starts changing again at \( \omega = 0.1 \omega_{p2} \) (if \( 0.1 \omega_{p2} > 10 \omega_{p1} \)), reaching \(-135^{\circ}\) at \( \omega_{p2} \) and asymptotically approaches \(-180^{\circ}\).

**Key Features:**
- The system's stability is discussed in terms of the magnitude and phase plots. The system remains stable as long as the magnitude drops below unity (0 dB) before the phase reaches \(-180^{\circ}\).
- Weaker feedback (depicted by the gray line) results in a more stable system, as the gain crossover point occurs at a lower frequency, while the phase crossover point remains constant.

What happens if the feedback is made "weaker"? To reduce the amount of feedback, we decrease $\beta$, obtaining the gray magnitude plot in Fig. 10.7. As the feedback becomes weaker, the gain crossover point moves toward the origin while the phase crossover point remains constant, resulting in a more stable system. The stability is obtained at the cost of weaker feedback.

#### Example 10.3

Construct the root locus for a two-pole system.

#### Solution

Writing the open-loop transfer function as

$$
\begin{equation*}
H(s)=\frac{A_{0}}{\left(1+\frac{s}{\omega_{p 1}}\right)\left(1+\frac{s}{\omega_{p 2}}\right)} \tag{10.5}
\end{equation*}
$$

we have

$$
\begin{align*}
\frac{Y}{X}(s) & =\frac{A_{0}}{\left(1+\frac{s}{\omega_{p 1}}\right)\left(1+\frac{s}{\omega_{p 2}}\right)+\beta A_{0}}  \tag{10.6}\\
& =\frac{A_{0} \omega_{p 1} \omega_{p 2}}{s^{2}+\left(\omega_{p 1}+\omega_{p 2}\right) s+\left(1+\beta A_{0}\right) \omega_{p 1} \omega_{p 2}} \tag{10.7}
\end{align*}
$$

Thus, the closed-loop poles are given by

$$
\begin{equation*}
s_{1,2}=\frac{-\left(\omega_{p 1}+\omega_{p 2}\right) \pm \sqrt{\left(\omega_{p 1}+\omega_{p 2}\right)^{2}-4\left(1+\beta A_{0}\right) \omega_{p 1} \omega_{p 2}}}{2} \tag{10.8}
\end{equation*}
$$

As expected, for $\beta=0, s_{1,2}=-\omega_{p 1},-\omega_{p 2}$. As $\beta$ increases, the term under the square root drops, taking on a value of zero for

$$
\begin{equation*}
\beta_{1}=\frac{1}{A_{0}} \frac{\left(\omega_{p 1}-\omega_{p 2}\right)^{2}}{4 \omega_{p 1} \omega_{p 2}} \tag{10.9}
\end{equation*}
$$

As shown in Fig. 10.8, the poles begin at $-\omega_{p 1}$ and $-\omega_{p 2}$, move toward each other, coincide for $\beta=\beta_{1}$, and become complex for $\beta>\beta_{1}$. The closed-loop system does not become unstable because the poles do not reach the $j \omega$ axis.
image_name:Figure 10.8
description:**Type of Graph and Function:**
The graph is a root locus plot, which is used in control systems to analyze the paths of poles of the closed-loop transfer function as a system parameter (in this case, \( \beta \)) is varied.

**Axes Labels and Units:**
- The horizontal axis is labeled \( \sigma \), representing the real part of the pole locations.
- The vertical axis is labeled \( j\omega \), representing the imaginary part of the pole locations.
- The axes do not specify units, as they are typically dimensionless in root locus plots.

**Overall Behavior and Trends:**
- The plot shows the movement of poles as the parameter \( \beta \) changes.
- Initially, the poles are located at \(-\omega_{p1}\) and \(-\omega_{p2}\) on the real axis (\( \beta = 0 \)).
- As \( \beta \) increases, the poles move towards each other on the real axis.
- At \( \beta = \beta_1 \), the poles coincide at a single point on the real axis.
- For \( \beta > \beta_1 \), the poles become complex conjugates, moving off the real axis and into the complex plane.

**Key Features and Technical Details:**
- The initial pole locations are marked with crosses at \(-\omega_{p1}\) and \(-\omega_{p2}\).
- The transition point where the poles coincide is marked as \( \beta = \beta_1 \).
- The plot indicates that the poles do not cross into the right half of the complex plane, suggesting that the system remains stable as \( \beta \) increases.

**Annotations and Specific Data Points:**
- The plot is annotated with the values \( \beta = 0 \) at the starting pole locations and \( \beta = \beta_1 \) at the coincidence point.
- Arrows indicate the direction of pole movement as \( \beta \) increases, moving from the real axis into the complex plane.

The foregoing calculations point to the complexity of the algebra required to construct a root locus for higher-order systems. For this reason, many root locus techniques have been devised so as to minimize such computations.

We now study a three-pole system. Shown in Fig. 10.9(a) are the Bode plots of the magnitude and phase of the loop gain. The third pole gives rise to additional phase shift, possibly moving the phase crossover to frequencies lower than the gain crossover and leading to oscillation.

Since the third pole also decreases the magnitude of the loop gain at a greater rate, the reader may wonder why the gain crossover does not move as much as the phase crossover does. As mentioned before, the phase begins to change at approximately one-tenth of the pole frequency, whereas the magnitude begins to drop only near the pole frequency. For this reason, additional poles (and zeros) affect the phase to a much greater extent than they do the magnitude.
image_name:Figure 10.9 (a)
description:Figure 10.9 (a) presents Bode plots for a three-pole system's loop transmission. It consists of two separate plots: one for magnitude and one for phase, both plotted against frequency on a logarithmic scale.

1. **Magnitude Plot**:
- **Y-Axis**: The magnitude of the loop transmission, expressed in decibels as \(20\log|\beta H(\omega)|\).
- **X-Axis**: Frequency \(\omega\) is plotted on a logarithmic scale.
- **Behavior**: The magnitude plot shows a decreasing trend. It starts flat, indicating a constant gain at low frequencies, and then begins to slope downward at each pole frequency \(\omega_p1\), \(\omega_p2\), and \(\omega_p3\). This indicates a drop in gain at these frequencies, typical for a system with poles.
- **Key Features**: The plot has three distinct slopes, each becoming steeper as additional poles are encountered, reflecting the cumulative effect of the poles on the system's gain.

2. **Phase Plot**:
- **Y-Axis**: The phase of the loop transmission, \(\angle \beta H(\omega)\), measured in degrees.
- **X-Axis**: Frequency \(\omega\) is again plotted on a logarithmic scale.
- **Behavior**: The phase plot starts at 0 degrees and decreases as frequency increases. It shows a more pronounced drop at each pole frequency, with the phase decreasing in steps, reflecting the phase lag introduced by each pole.
- **Key Features**: Notable phase shifts occur at each pole frequency, with the phase moving from 0 to -90 degrees, then further to -180 degrees and beyond as frequency increases.

Overall, this Bode plot illustrates how the three-pole system affects both the magnitude and phase of the loop transmission, highlighting the stability and response characteristics of the system as frequency varies.
image_name:Figure 10.9 (b)
description:Figure 10.9(b) shows the closed-loop response of a three-pole system. The graph is divided into two main plots. The top plot is a Bode plot displaying the magnitude of the closed-loop gain, and the bottom plot shows the phase response.

1. **Type of Graph and Function**:
- The graph is a Bode plot, which is used to analyze the frequency response of a system.

2. **Axes Labels and Units**:
- The horizontal axis represents frequency (ω) on a logarithmic scale.
- The vertical axis of the top plot represents the magnitude of the gain, denoted as \(|Y/X(\omega)|\), also on a logarithmic scale.
- The vertical axis of the bottom plot represents the phase angle \(\angle \beta H(\omega)\) in degrees.

3. **Overall Behavior and Trends**:
- **Magnitude Plot**: The gain initially remains constant, then peaks at a certain frequency \(\omega_0\), indicating a resonance. After reaching this peak, the gain decreases sharply.
- **Phase Plot**: The phase starts near 0 degrees, decreases gradually, and approaches -180 degrees as the frequency increases.

4. **Key Features and Technical Details**:
- **Resonance Peak**: The magnitude plot shows a pronounced peak at the resonant frequency \(\omega_0\), which is a critical feature indicating potential instability if not properly managed.
- **Phase Crossover**: The phase plot crosses -180 degrees, a point of interest for stability analysis.
- The gain at low frequencies is approximately \(1/\beta\), indicating the system's behavior in the steady state.

5. **Annotations and Specific Data Points**:
- The frequency \(\omega_0\) is marked as the point of resonance in the magnitude plot.
- The phase plot includes reference lines at -90 degrees and -180 degrees to assist in identifying phase margins and stability conditions.

Figure 10.9 (a) Bode plots of loop transmission for a three-pole system and (b) closed-loop response.

As with a two-pole system, if the feedback factor in Fig. 10.9 decreases, the circuit becomes more stable because the gain crossover moves toward the origin while the phase crossover remains constant. For this reason, a feedback amplifier designed for a higher closed-loop gain tends to be more stable (why?).

It is important not to confuse the $\beta H$ plots with the closed-loop frequency response, $Y / X$. As an example, consider a system with the loop response shown in Fig. 10.9(b), where the gain and phase crossover frequencies coincide. The closed-loop response, $|Y / X|$, exhibits infinite gain at $\omega_{0}$, predicting oscillation at this frequency.

## 10.3 ■ Phase Margin

We have seen that to ensure stability, $|\beta H|$ must drop to unity before $\angle \beta H$ crosses $-180^{\circ}$. We may naturally ask: How far should PX be from GX? Let us first consider a "marginal" case where, as depicted in Fig. 10.10(a), GX is only slightly below PX; for example, at GX, the phase equals $-175^{\circ}$. How does the closed-loop system respond in this case? Noting that at GX, $\beta H\left(j \omega_{1}\right)=1 \times \exp \left(-j 175^{\circ}\right)$, we have for the closed-loop system

$$
\begin{align*}
\frac{Y}{X}\left(j \omega_{1}\right) & =\frac{H\left(j \omega_{1}\right)}{1+\beta H\left(j \omega_{1}\right)}  \tag{10.10}\\
& =\frac{\frac{1}{\beta} \exp \left(-j 175^{\circ}\right)}{1+\exp \left(-j 175^{\circ}\right)}  \tag{10.11}\\
& =\frac{1}{\beta} \cdot \frac{-0.9962-j 0.0872}{0.0038-j 0.0872} \tag{10.12}
\end{align*}
$$

image_name:|βH(ω)| and ∠βH(ω) (a)
description:The graph consists of two main parts labeled as (a) and (b), representing different scenarios of closed-loop frequency and time responses based on the margin between gain and phase crossover points.

Graph (a):
1. **Type of Graph and Function:**
- The top part is a Bode plot showing both magnitude \(|\beta H(\omega)|\) and phase \(\angle \beta H(\omega)\).
- The middle part is a frequency response curve for \(|Y/X(\omega)|\).
- The bottom part is a time-domain response \(y(t)\).

2. **Axes Labels and Units:**
- The horizontal axis for all parts represents frequency \(\omega\) for the top two plots and time \(t\) for the bottom plot.
- The vertical axis for the top plot shows magnitude \(|\beta H(\omega)|\) and phase \(\angle \beta H(\omega)\) in degrees.
- The vertical axis for the middle plot shows \(|Y/X(\omega)|\).
- The vertical axis for the bottom plot shows \(y(t)\).

3. **Overall Behavior and Trends:**
- In the Bode plot, the magnitude decreases with frequency, crossing the 0 dB line at the gain crossover frequency (GX).
- The phase plot shows a phase margin (PM) at the phase crossover frequency (PX).
- The frequency response \(|Y/X(\omega)|\) exhibits a sharp peak near \(\omega = \omega_1\), indicating resonance.
- The time response \(y(t)\) shows oscillations, indicating potential instability or ringing.

4. **Key Features and Technical Details:**
- The gain crossover (GX) and phase crossover (PX) points are marked with dotted lines.
- The phase margin (PM) is indicated, showing the difference between the phase at PX and \(-180^\circ\).
- The peak in \(|Y/X(\omega)|\) suggests a high sensitivity or amplification at certain frequencies.
- The oscillatory nature of \(y(t)\) suggests underdamping in the system.

Graph (b):
1. **Type of Graph and Function:**
- Similar to (a), with a Bode plot, frequency response, and time response.

2. **Axes Labels and Units:**
- Same as in (a).

3. **Overall Behavior and Trends:**
- The Bode plot shows a more stable configuration with less pronounced peaks.
- The frequency response \(|Y/X(\omega)|\) is flatter, indicating less resonance.
- The time response \(y(t)\) shows a smooth rise without oscillations, indicating stability.

4. **Key Features and Technical Details:**
- The phase margin is larger than in (a), suggesting a more stable system.
- The absence of peaks in \(|Y/X(\omega)|\) and the smooth time response \(y(t)\) indicate a well-damped system.
image_name:|Y/X|(ω) (a)
description:The graph labeled "|Y/X|(ω) (a)" is a frequency response plot, specifically a magnitude plot, often used in control systems and signal processing to analyze the behavior of a system in the frequency domain.

1. **Type of Graph and Function:**
- This is a Bode plot, focusing on the magnitude response of the closed-loop transfer function |Y/X| as a function of frequency ω.

2. **Axes Labels and Units:**
- The horizontal axis represents frequency (ω), typically in radians per second or hertz, though the specific unit is not labeled.
- The vertical axis represents the magnitude |Y/X|, which is dimensionless.

3. **Overall Behavior and Trends:**
- The plot shows a sharp peak in the magnitude response, indicating a resonant frequency where the system amplifies the input signal significantly.
- After the peak, the magnitude decreases, suggesting the system attenuates higher frequencies.
- At low frequencies, the magnitude starts near 1/β, as expected from the context.

4. **Key Features and Technical Details:**
- The sharp peak indicates a resonant frequency, which is where the system has maximum gain.
- The peak suggests a potential stability issue or sensitivity to noise at this frequency.
- The system's behavior is characterized by a high Q-factor at the resonant frequency, indicating sharp selectivity.

5. **Annotations and Specific Data Points:**
- The graph does not explicitly label specific frequencies or magnitude values, but the peak is visually prominent.
- The baseline is marked at 1/β, aligning with the theoretical analysis provided.

This graph provides insight into the system's frequency response, highlighting the resonant behavior and potential stability concerns due to the sharp peak in the magnitude response.
image_name:y(t) (a)
description:The graph labeled "y(t) (a)" is a time-domain waveform plot. The x-axis represents time, denoted as "t," and the y-axis represents the amplitude of the output, denoted as "y(t)." The scale of the axes is linear.

Overall Behavior and Trends:
The waveform exhibits oscillatory behavior, indicating the presence of periodic fluctuations in the output over time. The amplitude of these oscillations appears to decrease gradually, suggesting a damped oscillatory response.

Key Features and Technical Details:
- **Oscillations:** The waveform starts with high amplitude oscillations that gradually diminish over time.
- **Damping:** The amplitude reduction over time suggests a damped system, where the oscillations are not sustained indefinitely.

Annotations and Specific Data Points:
- The graph is part of a comparison between two scenarios, (a) and (b), where (a) shows a system with a small margin between gain and phase crossover points, leading to more pronounced oscillations in the time response.

This graph is used to illustrate the time-domain response of a closed-loop system with specific gain and phase characteristics, highlighting how a small margin can lead to significant oscillatory behavior.
image_name:|βH(ω)| and ∠βH(ω) (b)
description:The graphs presented are Bode plots and time response diagrams that illustrate the frequency and time response of a closed-loop system for two different conditions: (a) with a small margin between gain and phase crossover points, and (b) with a large margin.

Graph (a): Small Margin
1. **Type of Graph and Function:**
- The top graph is a Bode plot showing the magnitude \(|\beta H(\omega)|\) and phase \(\angle \beta H(\omega)\) of the system.
- The middle graph shows the frequency response \(|Y/X(\omega)|\).
- The bottom graph is a time-domain response \(y(t)\).

2. **Axes Labels and Units:**
- The horizontal axis for the Bode plot and frequency response is frequency \(\omega\).
- The vertical axis for magnitude is \(|\beta H(\omega)|\) and \(|Y/X(\omega)|\), with a reference level at 1.
- The phase is shown in degrees, with a reference line at \(-180^\circ\).
- The time response \(y(t)\) has time \(t\) on the horizontal axis.

3. **Overall Behavior and Trends:**
- The magnitude plot shows a crossover at point GX where \(|\beta H(\omega)| = 1\).
- The phase plot crosses \(-180^\circ\) at point PX, indicating a phase margin PM.
- The frequency response \(|Y/X(\omega)|\) exhibits a sharp peak, suggesting resonance.
- The time response \(y(t)\) shows oscillations, indicating a less stable system.

4. **Key Features and Technical Details:**
- The phase margin PM is small, indicating a close proximity between gain and phase crossover frequencies.
- The oscillations in \(y(t)\) suggest potential overshoot and ringing in the system.

5. **Annotations and Specific Data Points:**
- Points GX and PX are marked, indicating gain and phase crossover frequencies, respectively.
- The phase margin PM is highlighted as a critical stability indicator.

Graph (b): Large Margin
1. **Type of Graph and Function:**
- Similar structure to Graph (a), with a Bode plot, frequency response, and time response.

2. **Axes Labels and Units:**
- Identical to Graph (a).

3. **Overall Behavior and Trends:**
- The magnitude and phase plots show a larger separation between GX and PX.
- The frequency response \(|Y/X(\omega)|\) is more stable, without sharp peaks.
- The time response \(y(t)\) is smoother, indicating a more stable system.

4. **Key Features and Technical Details:**
- The phase margin PM is larger, indicating improved stability.
- The lack of oscillations in \(y(t)\) suggests minimal overshoot and faster settling.

5. **Annotations and Specific Data Points:**
- Points GX and PX are marked, with a larger phase margin PM compared to Graph (a).
image_name:|Y/X|(ω) (b)
description:The graph labeled "|Y/X|(ω) (b)" is a frequency response plot that shows the magnitude of the closed-loop transfer function |Y/X| as a function of frequency ω.

1. **Type of Graph and Function:**
- This is a Bode plot focusing on the magnitude response of a closed-loop system.

2. **Axes Labels and Units:**
- The horizontal axis represents frequency (ω), typically measured in radians per second (rad/s).
- The vertical axis represents the magnitude |Y/X| of the closed-loop transfer function, which is dimensionless.
- The scale appears to be linear, as no logarithmic markers are indicated.

3. **Overall Behavior and Trends:**
- The graph shows a relatively flat response over a range of frequencies, indicating stable gain across those frequencies.
- Towards higher frequencies, the magnitude begins to decrease, suggesting a roll-off.

4. **Key Features and Technical Details:**
- The flat region of the graph suggests a consistent gain level, which is typical for a stable closed-loop system with a large margin between gain and phase crossover points.
- The roll-off at higher frequencies indicates the system's bandwidth limit, where the gain starts to decrease.
- There are no sharp peaks, unlike in the "(a)" graph, which implies a lack of resonance at ω = ω₁.

5. **Annotations and Specific Data Points:**
- No specific numerical values or annotations are provided on the graph.
- The graph implies a system with a large phase margin (PM) and gain margin, contributing to the stable response shown.

Overall, the graph illustrates a stable system with a broad frequency response and a gradual decline in gain at higher frequencies, characteristic of a system with a large gain and phase margin.
image_name:y(t) (b)
description:The graph labeled "y(t) (b)" is a time-domain waveform representing the output response of a closed-loop system over time. The horizontal axis is labeled "t" and represents time, though the specific units are not provided. The vertical axis is labeled "y(t)" and represents the amplitude of the response.

Overall Behavior and Trends:
- The waveform in graph (b) shows a smooth, gradual rise to a steady state. This indicates a stable response without oscillations or overshoot, suggesting a system with adequate phase margin and damping.
- The response appears to reach a constant value, indicating that the system eventually reaches a steady state.

Key Features and Technical Details:
- There are no oscillations or peaks in the waveform, implying that the system does not exhibit resonance or instability.
- The graph suggests a critically damped or overdamped system behavior, as it lacks oscillatory characteristics.

Annotations and Specific Data Points:
- The graph lacks specific numerical annotations or markers, but the shape of the curve suggests a well-damped response typical of systems with a large phase margin.

In summary, the time-domain response labeled "y(t) (b)" shows a stable, non-oscillatory behavior, indicating a well-damped system that smoothly transitions to a steady state without overshoot or oscillations.

Figure 10.10 Closed-loop frequency and time response for (a) small and (b) large margin between gain and phase crossover points.
and hence

$$
\begin{align*}
\left|\frac{Y}{X}\left(j \omega_{1}\right)\right| & =\frac{1}{\beta} \cdot \frac{1}{0.0872}  \tag{10.13}\\
& \approx \frac{11.5}{\beta} \tag{10.14}
\end{align*}
$$

Since at low frequencies, $|Y / X| \approx 1 / \beta$, the closed-loop frequency response exhibits a sharp peak in the vicinity of $\omega=\omega_{1}$. In other words, the closed-loop system is near oscillation, and its step response, $y(t)$, exhibits a very underdamped behavior. This point also reveals that a second-order system may suffer from ringing although it is stable.

Now suppose, as shown in Fig. 10.10(b), GX precedes PX by a greater margin. Then, we expect a relatively "well-behaved" closed-loop response in both the frequency domain and the time domain. It is therefore plausible to conclude that the greater the spacing between GX and PX (while GX remains below PX ), the more stable the feedback system. Alternatively, the phase of $\beta H$ at the gain crossover frequency can serve as a measure of stability: the smaller $|\angle \beta H|$ at this point, the more stable the system.

This observation leads us to the concept of "phase margin" (PM), defined as PM $=180^{\circ}+\angle \beta H(\omega=$ $\omega_{1}$ ), where $\omega_{1}$ is the gain crossover frequency. We see that stability calls for a positive and large PM.

#### Example 10.4

A two-pole feedback system is designed such that $\left|\beta H\left(\omega_{p 2}\right)\right|=1$ and $\left|\omega_{p 1}\right| \ll\left|\omega_{p 2}\right|$ (Fig. 10.11). How much is the phase margin?
image_name:Figure 10.11
description:The graph in Figure 10.11 is a Bode plot, which consists of two separate plots: the magnitude plot and the phase plot, both plotted against frequency on a logarithmic scale.

1. **Magnitude Plot (Top):**
- **Y-Axis:** Represents the magnitude of the loop gain, given as \(20 \log |\beta H(\omega)|\), in decibels (dB).
- **X-Axis:** Represents frequency \(\omega\) on a logarithmic scale.
- **Behavior:** The plot starts at a constant magnitude level at low frequencies, indicating that the gain is flat until the first pole \(\omega_{p1}\) is reached. Beyond \(\omega_{p1}\), the slope of the plot decreases, indicating a reduction in gain. The slope becomes steeper after the second pole \(\omega_{p2}\), showing a further drop in gain.
- **Key Points:** The gain crossover frequency is at \(\omega_{p2}\), where the magnitude crosses 0 dB.

2. **Phase Plot (Bottom):**
- **Y-Axis:** Represents the phase angle \(\angle \beta H(\omega)\) in degrees.
- **X-Axis:** Same frequency scale as the magnitude plot, logarithmic.
- **Behavior:** The phase starts at 0 degrees at low frequencies and begins to decrease as frequency increases. At \(\omega_{p2}\), the phase angle reaches \(-135^\circ\). The phase continues to decrease towards \(-180^\circ\).
- **Key Features:** The phase margin (PM) is indicated, which is the difference between \(-180^\circ\) and the phase angle at the gain crossover frequency. In this case, the phase margin is \(45^\circ\), as the phase angle at \(\omega_{p2}\) is \(-135^\circ\).

#### Solution

Since $\angle \beta H$ reaches $-135^{\circ}$ at $\omega=\omega_{p 2}$, the phase margin is equal to $45^{\circ}$. The key point to remember is that, if the loop gain drops to unity at a frequency above the second pole, the phase margin is less than $45^{\circ}$. As explained below, since $\mathrm{PM}=45^{\circ}$ is typically inadequate, we say that the ultimate unity-gain bandwidth cannot exceed the second pole of the open-loop op amp if a well-behaved time response is desired.

The above example suggests that for a phase margin greater than $45^{\circ}$, the gain crossover frequency must lie between the first pole and the second (in the absence of zeros). That is, the unity-gain bandwidth cannot exceed the second pole frequency.

How much phase margin is adequate? It is instructive to examine the closed-loop frequency response for different phase margins [1]. For $\mathrm{PM}=45^{\circ}$, at the gain crossover frequency $\angle \beta H\left(\omega_{1}\right)=-135^{\circ}$ and $\left|\beta H\left(\omega_{1}\right)\right|=1$ (Fig. 10.12), yielding

$$
\begin{align*}
\frac{Y}{X} & =\frac{H\left(j \omega_{1}\right)}{1+1 \times \exp \left(-j 135^{\circ}\right)}  \tag{10.15}\\
& =\frac{H\left(j \omega_{1}\right)}{0.29-0.71 j} \tag{10.16}
\end{align*}
$$

image_name:Figure 10.12 Closed-loop frequency response for 45° phase margin
description:### Type of Graph and Function:
The graph is a Bode plot, which is commonly used in control systems to represent the frequency response of a system. It consists of two separate plots: one for the magnitude and one for the phase of the system's transfer function.

Axes Labels and Units:
- **Magnitude Plot:**
- Vertical Axis: $|\beta H(\omega)|$ (dimensionless), with a reference level at 1.
- Horizontal Axis: Frequency $\omega$ (radians per second).
- **Phase Plot:**
- Vertical Axis: $\angle \beta H(\omega)$ (degrees), with a reference level at 0°.
- Horizontal Axis: Frequency $\omega$ (radians per second).
- **Closed-loop Gain Plot:**
- Vertical Axis: $\left| \frac{Y}{X}(\omega) \right|$ (dimensionless), with reference levels at $\frac{1}{\beta}$ and $\frac{1.3}{\beta}$.
- Horizontal Axis: Frequency $\omega$ (radians per second).

Overall Behavior and Trends:
- **Magnitude Plot:**
- The plot shows a line crossing the unity gain level (1) at the gain crossover frequency $\omega_1$, indicated by the point marked 'GX'.
- **Phase Plot:**
- The phase angle line crosses at -135° at the same frequency $\omega_1$, indicating the phase margin of 45°.
- **Closed-loop Gain Plot:**
- The plot shows a peak at the frequency $\omega_1$, reaching approximately $\frac{1.3}{\beta}$, indicating a 30% peak in the frequency response.

Key Features and Technical Details:
- **Gain Crossover Frequency ($\omega_1$):**
- At this frequency, the magnitude of $|\beta H(\omega_1)|$ is 1, and the phase angle is -135°.
- The gain margin and phase margin are critical for assessing system stability.
- **Peak in Closed-loop Gain:**
- The peak at $\omega_1$ in the closed-loop gain plot indicates a resonance or overshoot, which is a common characteristic in systems with a phase margin of 45°.

Annotations and Specific Data Points:
- **Markers:**
- The gain crossover frequency is marked with 'GX'.
- **Dashed Lines:**
- Vertical dashed lines indicate the frequency $\omega_1$ across all plots.
- Horizontal dashed lines on the closed-loop gain plot indicate the levels $\frac{1}{\beta}$ and $\frac{1.3}{\beta}$, illustrating the peak response.

It follows that

$$
\begin{align*}
\left|\frac{Y}{X}\right| & =\frac{1}{\beta} \cdot \frac{1}{|0.29-0.71 j|}  \tag{10.17}\\
& \approx \frac{1.3}{\beta} \tag{10.18}
\end{align*}
$$

Consequently, the frequency response of the feedback system suffers from a $30 \%$ peak at $\omega=\omega_{1}$.
It can be shown that for $\mathrm{PM}=60^{\circ}, Y\left(j \omega_{1}\right) / X\left(j \omega_{1}\right)=1 / \beta$, suggesting a negligible frequency peaking. This typically means that the step response of the feedback system exhibits little ringing, providing a fast settling. For greater phase margins, the system is more stable, but the time response slows down (Fig. 10.13). Thus, $\mathrm{PM}=60^{\circ}$ is typically considered the optimum value.
image_name:Figure 10.13 (a)
description:The graph labeled "(a)" in Figure 10.13 depicts a time-domain waveform representing the closed-loop step response of a feedback system with a phase margin (PM) of 45 degrees.

1. **Type of Graph and Function:**
- This is a time-domain response graph illustrating the behavior of a system to a step input.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \( t \) and represents time. The units are not specified but are typically in seconds or milliseconds.
- The vertical axis is labeled \( y(t) \) and represents the output response of the system. The units are not specified but generally correspond to the system's output variable (e.g., voltage, position).

3. **Overall Behavior and Trends:**
- The graph shows an initial rapid rise in the output, followed by oscillations that gradually decrease in amplitude over time. This indicates that the system initially overshoots its final value and then exhibits ringing before settling.

4. **Key Features and Technical Details:**
- The waveform exhibits a clear overshoot and subsequent damped oscillations, characteristic of a system with a lower phase margin.
- The oscillations indicate that the system has a tendency to ring, which is typical for a phase margin of 45 degrees, suggesting less stability compared to higher phase margins.

5. **Annotations and Specific Data Points:**
- There are no specific numerical values or markers provided on the graph for peak amplitudes or time constants. The graph is primarily qualitative, emphasizing the oscillatory nature of the response at this phase margin.
image_name:Figure 10.13 (b)
description:The graph labeled "(b)" in Figure 10.13 is a time-domain waveform representing the closed-loop step response of a system with a phase margin (PM) of 60 degrees.

1. **Type of Graph and Function:**
- This is a time-domain response graph showing how the output \( y(t) \) of a feedback system responds to a step input over time \( t \).

2. **Axes Labels and Units:**
- The horizontal axis is labeled \( t \) and represents time. The units are not specified but are typically in seconds or milliseconds.
- The vertical axis is labeled \( y(t) \) and represents the system's output response amplitude.

3. **Overall Behavior and Trends:**
- The graph shows a smooth, monotonic rise from an initial value at \( t = 0 \) to a steady-state value. This indicates a stable system response with minimal overshoot and no oscillations.
- The curve starts with a steep slope, indicating a fast initial response, and then gradually levels off as it approaches the steady-state value.

4. **Key Features and Technical Details:**
- The absence of oscillations or ringing in the response suggests a well-damped system.
- The system reaches its steady-state value quickly, reflecting the optimal phase margin of 60 degrees, which balances stability and response speed.

5. **Annotations and Specific Data Points:**
- The graph is annotated with "PM = 60°" above it, indicating the phase margin value.
- There are no specific numerical values or reference lines marked on the graph, but the smooth curve implies a critically damped or slightly underdamped response.
image_name:Figure 10.13 (c)
description:The graph labeled (c) is a time-domain waveform representing the closed-loop step response of a system with a phase margin (PM) of 90 degrees.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform illustrating the step response of a feedback system.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as \( t \), representing time.
- The vertical axis is labeled as \( y(t) \), representing the system's output response.
- No specific units are provided, but the graph is likely in arbitrary units or normalized units typical for such analyses.

3. **Overall Behavior and Trends:**
- The graph shows a smooth, monotonic increase from the origin, indicating a stable step response.
- The response rises quickly at first and then gradually approaches a steady-state value without any overshoot or oscillations.
- This behavior suggests a highly stable system with a slow response time.

4. **Key Features and Technical Details:**
- The system with a 90-degree phase margin is characterized by a slow response, as indicated by the gradual rise to the steady state.
- There are no oscillations, peaks, or valleys, which is typical for a system with a high phase margin.
- The lack of overshoot and ringing signifies a strong damping effect.

5. **Annotations and Specific Data Points:**
- The graph is specifically annotated with \( \text{PM} = 90^{\circ} \) to indicate the phase margin.
- No other specific numerical values or markers are provided on the graph.

Figure 10.13 Closed-loop time response for $45^{\circ}, 60^{\circ}$, and $90^{\circ}$ phase margins.

The concept of phase margin is well suited to the design of circuits that process small signals. In practice, the large-signal step response of feedback amplifiers does not follow the illustration of Fig. 10.13. This is not only due to slewing but also because of the nonlinear behavior resulting from large excursions in the bias voltages and currents of the amplifier. Such excursions in fact cause the pole and zero frequencies to vary during the transient, leading to a complicated time response. Thus, for large-signal applications, time-domain simulations of the closed-loop system prove more relevant and useful than small-signal ac computations of the open-loop amplifier.

As an example of a feedback circuit exhibiting a reasonable phase margin but poor settling behavior, consider the unity-gain amplifier of Fig. 10.14, where the aspect ratio of all transistors is equal to $50 \mu \mathrm{~m} /$ $0.6 \mu \mathrm{~m}$. With the choice of the device dimensions, bias currents, and capacitor values shown here, SPICE yields a phase margin of approximately $65^{\circ}$ and a unity-gain frequency of 150 MHz . The large-signal step response, however, suffers from significant ringing.
image_name:Figure 10.14 Unity-gain buffer
description:
[
name: M1, type: NMOS, ports: {S: GND, D: P, G: Vin}
name: M2, type: NMOS, ports: {S: P, D: d2d95, G: d2d95}
name: M5, type: NMOS, ports: {S: d2d95, D: Vout, G: Vout}
name: M3, type: PMOS, ports: {S: VDD, D: X, G: X}
name: M4, type: PMOS, ports: {S: VDD, D: d2d95, G: X}
name: C1, type: Capacitor, value: 1.6 pF, ports: {Np: X, Nn: d2d95}
name: C2, type: Capacitor, value: 1 pF, ports: {Np: Vout, Nn: Vout_o}
name: Iss, type: CurrentSource, value: 0.5 mA, ports: {Np: P, Nn: GND}
name: I1, type: CurrentSource, value: 0.3 mA, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a unity-gain buffer with a feedback loop. It includes a folded-cascode topology with NMOS and PMOS transistors and is compensated by capacitors C1 and C2. The circuit achieves a phase margin of approximately 65° and a unity-gain frequency of 150 MHz but suffers from significant ringing in the large-signal step response.
image_name:Large-signal step response
description:### Large-Signal Step Response Graph Description

1. **Type of Graph and Function:**
- The graph is a time-domain waveform depicting the large-signal step response of a unity-gain amplifier circuit.

2. **Axes Labels and Units:**
- The x-axis represents time (t), though specific units are not labeled, it is typically in microseconds or nanoseconds for such circuits.
- The y-axis represents voltage, with two plots: \( V_{in} \) and \( V_{out} \). The units are likely in volts.
- The graph does not specify scales, but it is assumed to be linear.

3. **Overall Behavior and Trends:**
- The input voltage \( V_{in} \) is a step function, showing a sudden rise from a lower level to a higher steady-state level.
- The output voltage \( V_{out} \) initially follows the input but exhibits significant overshoot and ringing before settling.
- The waveform has a damped oscillatory behavior, indicating underdamped system dynamics.

4. **Key Features and Technical Details:**
- The output voltage \( V_{out} \) shows an initial peak (overshoot) that exceeds the steady-state value.
- Following the peak, there are several oscillations (ringing) before the waveform stabilizes.
- The amplitude of oscillations decreases over time, suggesting a damping effect.
- The significant ringing indicates a phase margin that, while reasonable, is not sufficient to avoid oscillations in the step response.

5. **Annotations and Specific Data Points:**
- The graph does not provide specific numerical values for the overshoot or the frequency of oscillation.
- No reference lines or markers are present, but the behavior is characteristic of a phase margin around 65°, as noted in the context.
- The unity-gain frequency is approximately 150 MHz, influencing the speed and settling behavior of the response.

## 10.4 ■ Basic Frequency Compensation

Typical op amp circuits contain many poles. In a folded-cascode topology, for example, both the folding node and the output node contribute poles. For this reason, op amps must usually be "compensated," that is, their open-loop transfer function must be modified such that the closed-loop circuit is stable and the time response is well behaved.

The need for compensation arises because $|\beta H|$ does not drop to unity well before $\angle \beta H$ reaches $-180^{\circ}$. We then postulate that stability can be achieved by (1) minimizing the overall phase shift, thus pushing the phase crossover out [Fig. 10.15(a)]; or (2) dropping the gain with frequency, thereby pushing the gain crossover in [Fig. 10.15(b)]. The first approach requires that we attempt to minimize the number of poles in the signal path by proper design. Since each additional stage contributes at least one pole, this means that the number of stages must be minimized, a remedy that yields low voltage gain and/or limited output swings (Chapter 9). The second approach, on the other hand, retains the low-frequency gain and the output swings, but it reduces the bandwidth by forcing the gain to fall at lower frequencies.
image_name:Figure 10.15(a)
description:The graph in Figure 10.15 consists of two plots, each representing different aspects of frequency response in an operational amplifier (op-amp) design.

1. **Type of Graph and Function:**
- The graph is a Bode plot, commonly used to analyze the frequency response of systems.

2. **Axes Labels and Units:**
- The upper plot has a vertical axis labeled as `20log|βH(ω)|`, which represents the magnitude of the loop gain in decibels (dB). The horizontal axis is labeled `log(ω)`, indicating a logarithmic scale of frequency.
- The lower plot has a vertical axis labeled as `∠βH(ω)`, denoting the phase angle of the loop gain in degrees. The horizontal axis is also `log(ω)`, maintaining the logarithmic frequency scale.

3. **Overall Behavior and Trends:**
- In the magnitude plot (upper), the gain starts at a constant level and then decreases with increasing frequency, following a typical low-pass filter characteristic.
- In the phase plot (lower), the phase starts near 0° and decreases, eventually approaching -180°, indicating phase lag as frequency increases.

4. **Key Features and Technical Details:**
- The magnitude plot shows a clear breakpoint where the gain begins to roll off, indicating the cutoff frequency.
- The phase plot shows a gradual decrease in phase, with a notable change in slope as the frequency increases.
- The modified design is represented by a lighter line in the phase plot, showing a less steep descent, which suggests improved phase margin.

5. **Annotations and Specific Data Points:**
- Dashed lines indicate critical frequencies where the magnitude crosses 0 dB and where the phase approaches -180°.
- The modified design annotation highlights the adjustment made to improve stability by altering the phase response.

This Bode plot illustrates the effect of frequency compensation techniques, such as moving poles and adjusting gain, to maintain stability and desired performance in op-amp circuits.

image_name:(b)
description:The graph in question is a Bode plot, which is used to analyze the frequency response of a system, particularly focusing on gain and phase shift. It consists of two main plots: the magnitude plot and the phase plot.

1. **Type of Graph and Function:**
- The graph is a Bode plot, showing both the magnitude and phase response of a system.

2. **Axes Labels and Units:**
- The magnitude plot is on the top, with the vertical axis labeled as \(20\log|\beta H(\omega)|\), indicating the gain in decibels (dB). The horizontal axis is labeled as \(\log(\omega)\), representing the logarithm of the frequency in radians per second.
- The phase plot is on the bottom, with the vertical axis labeled as \(\angle \beta H(\omega)\), indicating the phase angle in degrees. The horizontal axis is again \(\log(\omega)\).

3. **Overall Behavior and Trends:**
- In the magnitude plot, the graph starts at a high gain level and decreases in a piecewise linear fashion as frequency increases. The modified design is shown as a lighter line, indicating an adjustment that results in a more gradual decline in gain.
- In the phase plot, the phase starts at 0° and decreases towards -180° as frequency increases, with some fluctuations along the way.

4. **Key Features and Technical Details:**
- The magnitude plot shows two distinct slopes, indicating changes in the system's pole-zero configuration.
- Dashed vertical lines mark critical frequencies where the magnitude crosses 0 dB and where the phase approaches -180°.
- The modified design annotation highlights the adjustment made to improve stability by altering the phase response.

5. **Annotations and Specific Data Points:**
- The plot includes annotations for a 'Modified Design', which shows an improvement in phase margin by altering the gain crossover frequency.
- The dashed lines indicate critical points where the system's response changes significantly, aiding in the analysis of system stability and performance.

This Bode plot is used to illustrate the effect of frequency compensation techniques, such as moving poles and adjusting gain, to maintain stability and desired performance in operational amplifier circuits. The modifications aim to enhance the phase margin, thereby improving the overall stability of the system.

Figure 10.15 Frequency compensation by (a) moving PX out and (b) pushing GX in.

In practice, we first try to design an op amp so as to minimize the number of poles while meeting other requirements. Since the resulting circuit may still suffer from insufficient phase margin, we then compensate the op amp, i.e., modify the design so as to move the gain crossover toward the origin. These efforts proceed with the $\beta$ value chosen according to the final design requirements. For example, a closed-loop gain of 4 in some cases translates to $\beta \approx 0.25$ if the loop gain is large. ${ }^{3}$ In other words, we need not compensate the circuit for $\beta=1$ if the closed-loop gain is always higher.

Let us apply the above concepts to the telescopic-cascode op amp shown in Fig. 10.16, where a PMOS current mirror performs differential to single-ended conversion. We identify a number of poles in the signal paths: path 1 contains a high-frequency pole at the source of $M_{3}$, a mirror pole at node $A$, and another high-frequency pole at the source of $M_{7}$, whereas path 2 contains a high-frequency pole at the source of $M_{4}$. The two paths share a pole at the output.

It is instructive to estimate the relative position of these poles. Since the output resistance of the op amp is much higher than the small-signal resistances seen at the other nodes in the circuit, we expect

image_name:Figure 10.16 Telescopic op amp with single-ended output
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin+}
name: M2, type: NMOS, ports: {S: P, D: Y, G: Vin-}
name: M3, type: NMOS, ports: {S: X, D: A, G: Vb1}
name: M4, type: NMOS, ports: {S: Y, D: Vout, G: Vb1}
name: M5, type: PMOS, ports: {S: VDD, D: A, G: A}
name: M6, type: PMOS, ports: {S: VDD, D: N, G: A}
name: M7, type: PMOS, ports: {S: N, D: Vout, G: Vb2}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: VDD, Nn: P}
]
extrainfo:The circuit is a telescopic op amp with single-ended output. Path 1 contains high-frequency poles at the source of M3 and M7, and a mirror pole at node A. Path 2 contains a high-frequency pole at the source of M4. Both paths share a pole at the output. The dominant pole is at the output, impacting the open-loop 3-dB bandwidth.

that, even with a moderate load capacitance, the output pole, $\omega_{p, \text { out }}$, is the closest to the origin. Called the "dominant pole," $\omega_{p, \text { out }}$ usually sets the open-loop 3-dB bandwidth.

We also surmise that the first "nondominant pole," i.e., the closest pole to the origin after the dominant pole, arises at node $A$. This is because the total capacitance at this node, roughly equal to $C_{G S 5}+C_{G S 6}+$ $C_{D B 5}+2 C_{G D 6}+C_{D B 3}+C_{G D 3}$, is typically quite a lot larger than that at nodes $X, Y$, and $N$, and the small-signal resistance of $M_{5}$, approximately $1 / g_{m 5}$, is also relatively large.

Which node yields the next nondominant pole: $N$ or $X$ (and $Y$ )? Recall from Chapter 9 that, to obtain a low overdrive and consume a reasonable voltage headroom, the PMOS devices in the op amp are typically wider than the NMOS transistors. Comparing $M_{4}$ and $M_{7}$ and neglecting body effect, we note that since $g_{m}=2 I_{D} /\left|V_{G S}-V_{T H}\right|$, if the two transistors are designed to have the same overdrive, they also exhibit the same transconductance. However, from square-law characteristics, we have $W_{4} / W_{7}=\mu_{p} / \mu_{n}$, which is about $1 / 2$ to $1 / 3$. Thus, nodes $N$ and $X$ (or $Y$ ) see roughly equal small-signal resistances to ground, but node $N$ suffers from much more capacitance. It is therefore plausible to assume that node $N$ contributes the next nondominant pole. Figure 10.17 illustrates the results, denoting the capacitance at nodes $A, N$, and $X$ by $C_{A}, C_{N}$, and $C_{X}$, respectively. The poles at nodes $X$ and $Y$ are nearly equal, and their corresponding terms in the transfer functions of path 1 and path 2 can be factored out. Thus, they count as one pole rather than two.
image_name:Figure 10.17 Pole locations for the op amp of Fig. 10.16.
description:Figure 10.17 is a pole-zero plot for an operational amplifier, displaying the locations of poles in the complex frequency plane. The graph is a two-dimensional plot with the real axis (σ) on the horizontal and the imaginary axis (jω) on the vertical.

1. **Type of Graph and Function:**
- This is a pole-zero plot, typically used in control systems and signal processing to represent the locations of poles and zeros of a transfer function in the complex plane.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as σ, representing the real part of the complex frequency.
- The vertical axis is labeled as jω, representing the imaginary part of the complex frequency.
- Units are not explicitly provided, but they are typically in radians per second for frequency.

3. **Overall Behavior and Trends:**
- The graph shows several poles marked as crosses (×) along the real axis.
- These poles are arranged from left to right with increasing real values, suggesting increasing damping or decreasing frequency response as you move right.

4. **Key Features and Technical Details:**
- The poles are labeled with specific terms: \(-\frac{g_{m3}}{C_{X}}, -\frac{g_{m7}}{C_{N}}, -\frac{g_{m5}}{C_{A}},\) and \(-\frac{1}{R_{out}C_{L}}\).
- These terms represent the inverse of time constants associated with different nodes or stages in the amplifier, with \(g_{m}\) representing transconductance and \(C\) representing capacitance.
- The pole \(-\frac{1}{R_{out}C_{L}}\) is likely the dominant pole, as it is positioned farthest to the right, indicating a lower frequency response limit.

5. **Annotations and Specific Data Points:**
- The poles are critical points that define the frequency response and stability of the amplifier.
- No specific numerical values are given, but the labels provide insight into the relative contributions of various components to the system's dynamics.

With the position of the poles roughly determined, we can construct the magnitude and phase plots for $\beta H$, using $\beta=1$ for the worst case. Shown in Fig. 10.18, such characteristics indicate that the mirror pole typically limits the phase margin because its phase contribution occurs at lower frequencies than that of other nondominant poles.
image_name:Figure 10.18 Bode plots of loop transmission for op amp of Fig. 10.16
description:The graph in Figure 10.18 is a Bode plot that illustrates the loop transmission characteristics for the operational amplifier circuit depicted in Figure 10.16. The Bode plot consists of two parts: the magnitude plot and the phase plot, both plotted against frequency on a logarithmic scale.

1. **Magnitude Plot (Top):**
- **Y-axis:** The vertical axis represents the magnitude of the loop transmission, expressed as \(20\log|\beta H(\omega)|\), in decibels (dB).
- **X-axis:** The horizontal axis represents frequency \(\omega\) on a logarithmic scale.
- **Overall Behavior:** The magnitude plot starts at a high level and decreases in a piecewise linear fashion as frequency increases. This indicates a reduction in gain with increasing frequency.
- **Key Features:**
- Several pole frequencies are marked with vertical dashed lines: \(\omega_{p,\text{out}}\), \(\omega_{p,A}\), \(\omega_{p,N}\), and \(\omega_{p,X}\). Each pole contributes to a slope change in the magnitude plot.
- The slope of the plot changes at each pole, typically decreasing by 20 dB/decade per pole.

2. **Phase Plot (Bottom):**
- **Y-axis:** The vertical axis represents the phase of the loop transmission, \(\angle \beta H(\omega)\), in degrees.
- **X-axis:** The horizontal axis is the same logarithmic frequency scale as the magnitude plot.
- **Overall Behavior:** The phase plot shows a downward trend, indicating a phase shift that becomes more negative with increasing frequency.
- **Key Features:**
- The phase decreases through significant thresholds at \(-180^\circ\), \(-270^\circ\), and approaches \(-360^\circ\), implying multiple poles contributing to phase lag.

This Bode plot highlights the impact of various poles on the loop transmission, with particular attention to how these poles affect both the gain and phase margin. The mirror pole, as mentioned in the context, typically limits the phase margin by contributing a phase shift at lower frequencies.

Recall from Chapter 6 that differential pairs using active current mirrors exhibit a left-half-plane zero located at twice the mirror pole frequency. The circuit of Fig. 10.16 contains such a zero as well. Located at $2 \omega_{p, A}$, the zero impacts both the magnitude and phase characteristics. The analysis is left to the reader.

Compensation Procedure How should we compensate the telescopic-cascode op amp? Recall that our ultimate goal is to ensure a loop gain sufficiently less than unity at the phase crossover frequency. Let us assume that the number and location of the nondominant poles and hence the phase plot at frequencies higher than roughly $10 \omega_{p, \text { out }}$, remain constant. We begin with the original response shown in Fig. 10.19, which has a negative phase margin. We must force the loop gain to drop such that the gain crossover point moves toward the origin. To accomplish this, we simply lower the frequency of the dominant pole, $\omega_{p 1}$, by increasing the load capacitance. The key point is that the phase contribution of the dominant pole in the vicinity of the gain or phase crossover point is close to $90^{\circ}$ and relatively independent of the location of the pole. That is, as illustrated in Fig. 10.19, translating the dominant pole toward the origin affects the magnitude plot, but not the critical part of the phase plot. If $\omega_{p 1}$ is lowered sufficiently, the PM reaches an acceptable value, but at the cost of bandwidth.
image_name:Figure 10.19 Translating the dominant pole toward the origin.
description:The graph in Figure 10.19 is a Bode plot, which consists of two separate plots: a magnitude plot and a phase plot. Both plots share a common horizontal axis representing frequency, denoted as \( \log(\omega) \), where \( \omega \) is the angular frequency.

Magnitude Plot:
- **Vertical Axis:** The magnitude plot's vertical axis is labeled as \( 20\log|\beta H(\omega)| \), which represents the gain in decibels (dB).
- **Behavior:** The plot shows a typical low-pass filter response. Initially, the magnitude is constant at 0 dB, indicating a flat response at low frequencies. As frequency increases, the magnitude begins to decline, indicating a reduction in gain.
- **Dominant Pole:** The frequency \( \omega_{p1} \) is marked, indicating the location of the dominant pole. The original response is shown in a thicker line, and a translated response (with the dominant pole shifted toward the origin) is depicted in a lighter line, illustrating the effect of moving the pole.

Phase Plot:
- **Vertical Axis:** The phase plot's vertical axis is labeled as \( \angle \beta H(\omega) \), representing the phase shift in degrees.
- **Behavior:** The phase starts at 0 degrees and decreases as frequency increases. A significant phase shift occurs around the dominant pole \( \omega_{p1} \), eventually approaching \(-180^{\circ}\).
- **Phase Margin (PM):** The phase margin is annotated, with areas marked \( PM > 0 \) and \( PM < 0 \). This indicates the stability of the system, with a positive phase margin suggesting stability and a negative phase margin indicating potential instability.

Key Features:
- **Annotations:** The graph includes annotations indicating the original response and the effects of translating the dominant pole. The critical frequencies and phase margins are highlighted, providing insight into the system's stability and performance.
- **Critical Values:** The plot emphasizes the importance of the dominant pole \( \omega_{p1} \) in affecting both the magnitude and phase characteristics, particularly in determining the phase margin and system stability.

In order to determine how much the dominant pole must be shifted down as well as arrive at an important conclusion, let us assume that (1) the second nondominant pole ( $\omega_{p, N}$ ) in Fig. 10.16 is much higher than the mirror pole so that the phase shift at $\omega=\omega_{p, A}$ is equal to $-135^{\circ}$, and (2) a phase
margin of $45^{\circ}$ (which is usually inadequate) is necessary. To compensate the circuit, we begin from $\angle \beta H(\omega)=-180^{\circ}+\mathrm{PM}=-135^{\circ}$ and identify the corresponding gain crossover frequency, in this case, $\omega_{p, A}$ (Fig. 10.20). Since the dominant pole must drop the gain to unity at $\omega_{p, A}$ with a slope of $20 \mathrm{~dB} / \mathrm{dec}$, we draw a straight line from $\omega_{p, A}$ toward the origin with such a slope, thus obtaining the new magnitude of the dominant pole, $\omega_{p, \text { out }}^{\prime}$. Therefore, the load capacitance must be increased by a factor of $\omega_{p, \text { out }} / \omega_{p, \text { out }}^{\prime}$.
image_name:Figure 10.20 Translating the dominant pole toward the origin for $45^{\circ}$ phase margin.
description:The graph in Figure 10.20 consists of two plots, both on logarithmic scales for frequency (ω) on the x-axis. The top plot is a magnitude plot, with the y-axis labeled as "20log|βH(ω)|" in decibels (dB). The bottom plot is a phase plot, with the y-axis labeled as "∠βH(ω)" in degrees.

Top Plot: Magnitude
- **Type of Graph:** Bode magnitude plot.
- **Axes:**
- **X-axis:** Frequency (ω) on a logarithmic scale.
- **Y-axis:** Magnitude in decibels (20log|βH(ω)|).
- **Overall Behavior and Trends:**
- The plot starts at a high gain level, remains flat until it reaches a frequency labeled as ω_{p,out}.
- Beyond ω_{p,out}, the gain begins to decrease with a slope of -20 dB/decade, indicating the presence of a dominant pole.
- The decrease continues until it intersects with a frequency labeled ω_{p,A}, where the magnitude reaches 0 dB, indicating the unity-gain crossover frequency.
- **Key Features and Technical Details:**
- The line with a -20 dB/dec slope is highlighted, showing the effect of the dominant pole.
- Critical frequencies are marked: ω_{p,out} and ω_{p,A}.

Bottom Plot: Phase
- **Type of Graph:** Bode phase plot.
- **Axes:**
- **X-axis:** Frequency (ω) on a logarithmic scale.
- **Y-axis:** Phase in degrees (∠βH(ω)).
- **Overall Behavior and Trends:**
- The phase starts at 0 degrees and decreases as frequency increases.
- A significant phase drop is observed, reaching approximately -135 degrees.
- **Key Features and Technical Details:**
- The phase plot shows a decrease in phase angle, typical of a system with poles affecting the phase margin.
- The phase margin at the unity-gain frequency is implied to be 45 degrees, as indicated by the context of the figure.

Annotations and Specific Data Points:
- The magnitude plot includes a reference line indicating the slope of -20 dB/decade.
- Frequencies ω_{p,out} and ω_{p,A} are explicitly marked, providing reference points for the dominant and unity-gain crossover frequencies respectively.

From the new magnitude plot, we note that the unity-gain bandwidth of the compensated (open-loop) op amp is equal to the frequency of the first nondominant pole (of course with a phase margin of $45^{\circ}$ ). This is a fundamental result, indicating that to achieve a wide bandwidth in a feedback system employing a multipole op amp, the first nondominant pole must be as far as possible. For this reason, the mirror pole proves undesirable.

We should also mention that although $\omega_{p, \text { out }}=\left(R_{\text {out }} C_{L}\right)^{-1}$, increasing $R_{\text {out }}$ does not compensate the op amp. As shown in Fig. 10.21, a higher $R_{\text {out }}$ results in a greater low-frequency loop gain, only affecting the low-frequency portion of the characteristics. Also, moving one of the nondominant poles toward the origin does not improve the phase margin. (Why?)
image_name:Figure 10.21 Bode plots of loop gain for higher output resistance
description:The graph in Figure 10.21 is a Bode plot, which consists of two separate plots: one for magnitude and one for phase. This type of graph is used to analyze the frequency response of a system, in this case, the loop gain of an operational amplifier with higher output resistance.

1. **Magnitude Plot (Top Graph):**
- **Y-Axis:** The magnitude is represented as \(20\log|\beta H(\omega)|\), measured in decibels (dB).
- **X-Axis:** The frequency \(\omega\) is plotted on a logarithmic scale.
- **Behavior:** The plot starts with a flat region indicating a constant gain at low frequencies. As frequency increases, the plot shows a downward slope, indicating a decrease in gain. The slope becomes steeper after the frequency \(\omega_{p,\text{out}}\), which is marked on the plot.
- **Key Feature:** The increase in output resistance \(R_{\text{out}}\) is shown to increase the low-frequency gain, depicted by a shift upwards in the flat region of the plot.

2. **Phase Plot (Bottom Graph):**
- **Y-Axis:** The phase is represented as \(\angle\beta H(\omega)\), measured in degrees.
- **X-Axis:** The frequency \(\omega\) is also plotted on a logarithmic scale.
- **Behavior:** The phase starts at 0 degrees and decreases as frequency increases. It approaches -180 degrees at higher frequencies.
- **Key Feature:** There is a noticeable phase drop around \(\omega_{p,\text{out}}\), which corresponds to the frequency where the magnitude plot begins to slope downward. This indicates a phase shift that accompanies the gain reduction.

Overall, the Bode plot illustrates how increasing the output resistance affects the loop gain, particularly by increasing the low-frequency gain and altering the phase response at higher frequencies. The plot emphasizes the importance of considering both magnitude and phase when analyzing frequency response for stability and performance in operational amplifiers.

In summary, frequency compensation moves the dominant pole of the open-loop amplifier to sufficiently low values so that the unity-gain bandwidth is well below the phase crossover frequency. Also, the compensated bandwidth cannot exceed the first nondominant pole frequency since a phase margin of greater than $45^{\circ}$ is typically required.

#### Example 10.5

An op amp is compensated to have a phase margin of $60^{\circ}$ with unity-gain feedback. By what factor can the compensation be relaxed if the circuit is to operate with a feedback factor of $\beta<1$ [Fig. 10.22(a)]?
image_name:(a)
description:
[
name: OpAmp1, type: OpAmp, ports: {InP: Vin, InN: Vout, OutP: Vout}
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'Vout', 'N2': 'X'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'X', 'N2': 'GND'
'name': 'OpAmp1', 'type': 'OpAmp', 'ports': {'InP': 'Vin', 'InN': 'X', 'OutP': 'Vout'
]
extrainfo:The circuit is an operational amplifier with feedback, where the feedback factor is less than 1. It includes two resistors R1 and R2 forming a voltage divider that provides feedback to the inverting input of the op-amp. This configuration allows the adjustment of the phase margin and gain.
image_name:(b)
description:**Type of Graph and Function:**
The graph in Figure 10.22(b) is a Bode plot, which consists of two separate plots: the magnitude plot (upper graph) and the phase plot (lower graph). The Bode plot is used to represent the frequency response of a system.

**Axes Labels and Units:**
- **Magnitude Plot:**
- Vertical Axis: "20log|βH(ω)|" in decibels (dB).
- Horizontal Axis: "log ω" representing the logarithm of frequency in radians per second.
- **Phase Plot:**
- Vertical Axis: "∠βH(ω)" in degrees.
- Horizontal Axis: "log ω" representing the logarithm of frequency in radians per second.

**Overall Behavior and Trends:**
- **Magnitude Plot:**
- The uncompensated response is shown as a solid line, initially flat at "20logA₀" and then sloping downwards at a rate of -20 dB/decade after a certain frequency.
- A dashed line indicates the compensated response starting from the point labeled "C" and sloping downwards, intersecting the vertical lines at "log ωₚ₁'" and "log ωₚ₁".
- The compensated response shows a shift downwards by "20log(βA₀)" due to the feedback factor β.
- **Phase Plot:**
- The phase response starts at 0 degrees and decreases, crossing -120 degrees at a specific frequency. This indicates the frequency at which the phase margin is determined.

**Key Features and Technical Details:**
- **Magnitude Plot:**
- Point "C" represents the starting point of the compensated response.
- Point "D" is the intersection of the compensated response with the vertical line at "log ωₚ₁'".
- The frequency "log ωₚ₁" is where the original dominant pole was located, and "log ωₚ₁'" is the new location after compensation.
- **Phase Plot:**
- The phase crosses -120 degrees, which is critical for determining stability margins.

**Annotations and Specific Data Points:**
- The plot includes reference lines for the uncompensated and compensated responses.
- The key frequencies "log ωₚ₁'", "log ωₚ₁", and the phase crossing at -120 degrees are marked, indicating critical points for analysis of the system's stability and response to feedback.

#### Solution

As illustrated in Fig. 10.22(b), the original compensation identifies the frequency at which $\angle \beta H=-120^{\circ}$, draws a line from this frequency at a slope of $20 \mathrm{~dB} / \mathrm{dec}$ toward the vertical axis, and hence moves the dominant pole from $\omega_{p 1}$ to $\omega_{p 1}^{\prime}$. With a feedback factor of $\beta$, the uncompensated magnitude response is shifted down by $-20 \log \beta$, requiring a dominant pole at $\omega_{p 1}^{\prime \prime}$. To obtain this value, we equate the slope of the line $C D$ to $20 \mathrm{~dB} / \mathrm{dec}$ :

$$
\begin{equation*}
\frac{-20 \log \beta}{\log \omega_{p 1}^{\prime \prime}-\log \omega_{p 1}^{\prime}}=20 \tag{10.19}
\end{equation*}
$$

and hence $\omega_{p 1}^{\prime \prime}=\omega_{p 1}^{\prime} / \beta$. That is, the compensation capacitor can be reduced by approximately a factor of $1 / \beta$. This, of course, does not mean that the new feedback circuit settles faster; the weaker feedback translates to a proportionally smaller extension of the bandwidth. In fact, we can write the closed-loop - $3-\mathrm{dB}$ bandwidths as $\left(1+A_{0}\right) \omega_{p 1}^{\prime} \approx A_{0} \omega_{p 1}^{\prime}$ for the original op amp and $\left(1+\beta A_{0}\right) \omega_{p 1}^{\prime \prime} \approx \beta A_{0} \omega_{p 1}^{\prime \prime} \approx A_{0} \omega_{p 1}^{\prime}$ for the newly-compensated counterpart, concluding that the closed-loop speed remains roughly the same.

A related question that we address in Problem 10.23 is the following: If an op amp is compensated to have $\mathrm{PM}=60^{\circ}$ with unity-gain feedback, by how much does its PM increase if the feedback factor is reduced to $\beta<1$ ?

Now consider the fully differential telescopic cascode depicted in Fig. 10.23. In addition to achieving various useful properties of differential operation, this topology avoids the mirror pole, thereby exhibiting stable behavior for a greater bandwidth. In fact, we can identify one dominant pole at each output node and only one nondominant pole arising from node $X$ (or $Y$ ). This suggests that fully differential telescopiccascode circuits are stable and do not need compensation.

But how about the pole at node $N$ (or $K$ ) in Fig. 10.23? Considering one of the PMOS cascodes as shown in Fig. 10.24(a), we may think that the capacitance at node $N, C_{N}=C_{G S 5}+C_{S B 5}+C_{G D 7}+C_{D B 7}$, shunts the output resistance of $M_{7}$ at high frequencies, thereby dropping the output impedance of the cascode. To quantify this effect, we first determine $Z_{\text {out }}$ in Fig. 10.24(a):

$$
\begin{equation*}
Z_{\text {out }}=\left(1+g_{m 5} r_{O 5}\right) Z_{N}+r_{O 5} \tag{10.20}
\end{equation*}
$$

image_name:Figure 10.23 Fully differential telescopic op amp
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: Vip}
name: M2, type: NMOS, ports: {S: P, D: Y, G: Vin}
name: M3, type: NMOS, ports: {S: X, D: Vout, G: Vb1}
name: M4, type: NMOS, ports: {S: Y, D: Vout, G: Vb1}
name: M5, type: PMOS, ports: {S: N, D: Vout, G: Vb2}
name: M6, type: PMOS, ports: {S: K, D: Vout, G: Vb2}
name: M7, type: PMOS, ports: {S: VDD, D: N, G: Vb3}
name: M8, type: PMOS, ports: {S: VDD, K: Vout, G: Vb3}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: P, Nn: GND}
]
extrainfo:This is a fully differential telescopic operational amplifier. It uses a pair of NMOS transistors (M1, M2) for the differential input stage, followed by NMOS cascode transistors (M3, M4) to increase the output impedance. The PMOS transistors (M5, M6, M7, M8) form the active load and provide the differential output. The circuit is biased by a constant current source Iss.

image_name:Figure 10.24 Effect of device capacitance at internal node of a cascode current source(a)
description:
[
name: M7, type: PMOS, ports: {S: VDD, D: N, G: Vb3}
name: M5, type: PMOS, ports: {S: N, D: d5, G: Vb2}
name: CN, type: Capacitor, value: CN, ports: {Np: N, Nn: GND}
name:CL, type:Capacitor, value:CL, ports:{Np:d5, Nn:GND}
]
extrainfo:This circuit diagram depicts the effect of device capacitance at the internal node of a cascode current source. The PMOS transistors M7 and M5 are configured in a cascode arrangement to improve output impedance. The capacitor CN is connected at the internal node N, which impacts the frequency response of the circuit. Zout represents the output impedance of the configuration.

image_name:Figure 10.24(b)
description:
[
name: M7, type: PMOS, ports: {S: VDD, D: N, G: Vb3}
name: M5, type: PMOS, ports: {S: N, D: d5, G: Vb2}
name: CN, type: Capacitor, value: CN, ports: {Np: N, Nn: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: d5, Nn: GND}
]
extrainfo:This circuit diagram depicts a cascode current source with PMOS transistors M7 and M5. The capacitor CN at node N affects the frequency response, and Zout represents the output impedance. The circuit is designed to improve output impedance by using a cascode configuration.

Figure 10.24 Effect of device capacitance at internal node of a cascode current source.
where body effect is neglected and $Z_{N}=r_{O 7} \|\left(C_{N} s\right)^{-1}$. Assuming the first term is much greater than the second, we have

$$
\begin{equation*}
Z_{\text {out }} \approx\left(1+g_{m 5} r_{O 5}\right) \frac{r_{O 7}}{r_{O 7} C_{N} s+1} \tag{10.21}
\end{equation*}
$$

Now, as illustrated in Fig. 10.24(b), we take the output load capacitance into account:

$$
\begin{align*}
Z_{\text {out }} \| \frac{1}{C_{L} s} & =\frac{\left(1+g_{m 5} r_{O 5}\right) \frac{r_{O 7}}{r_{O 7} C_{N} s+1} \cdot \frac{1}{C_{L} s}}{\left(1+g_{m 5} r_{O 5}\right) \frac{r_{O 7}}{r_{O 7} C_{N} s+1}+\frac{1}{C_{L} s}}  \tag{10.22}\\
& =\frac{\left(1+g_{m 5} r_{O 5}\right) r_{O 7}}{\left[\left(1+g_{m 5} r_{O 5}\right) r_{O 7} C_{L}+r_{O 7} C_{N}\right] s+1} \tag{10.23}
\end{align*}
$$

Thus, the parallel combination of $Z_{\text {out }}$ and the load capacitance still contains a single pole corresponding to a time constant $\left(1+g_{m 5} r_{O 5}\right) r_{O 7} C_{L}+r_{O 7} C_{N}$. Note that $\left(1+g_{m 5} r_{O 5}\right) r_{O 7} C_{L}$ is simply due to the lowfrequency output resistance of the cascode. In other words, the overall time constant equals the "output" time constant plus $r_{O 7} C_{N}$. The key point in this calculation is that the pole in the PMOS cascode (at node $N$ ) is merged with the output pole, thus creating no additional pole. It merely lowers the dominant pole
by a slight amount. For this reason, we loosely say that the signal does not "see" the pole in the cascode current sources. ${ }^{4}$

Comparison of the circuits shown in Figs. 10.16 and 10.23 now reveals that the fully differential configuration avoids both the mirror pole and the pole at node $N$. With the approximation made in (10.23), the circuit of Fig. 10.23 contains only one nondominant pole located at relatively high frequencies owing to the high transconductance of the NMOS transistors. This is a remarkable advantage of fully differential cascode op amps.

We have thus far observed that nondominant poles give rise to instability, requiring frequency compensation. Is it possible to cancel one or more of these poles by introducing zeros in the transfer function? For example, following the analysis of Fig. 6.41, we surmise that if a low-gain but fast path is placed in parallel with the main amplifier, a zero is created that can be positioned atop the first nondominant pole. However, cancellation of a pole by a zero in the presence of mismatches leads to long settling components in the step response of the closed-loop circuit. This effect is studied in Problem 10.19.

## 10.5 Compensation of Two-Stage Op Amps

Our study of op amps in Chapter 9 indicates that two-stage topologies may prove inevitable if the output voltage swing must be maximized. This is especially true in today's low-voltage op amps. Thus, the stability and compensation of such op amps is of interest.

Consider the circuit shown in Fig. 10.25. We identify three poles: a pole at $X$ (or $Y$ ), another at $E$ (or $F$ ), and a third at $A$ (or $B$ ). From our foregoing discussions, we know that the pole at $X$ lies at relatively high frequencies. But how about the other two? Since node $E$ exhibits a high small-signal resistance, even the capacitances of $M_{3}, M_{5}$, and $M_{9}$ can create a pole relatively close to the origin. At node $A$, the small-signal resistance is lower, but $C_{L}$ may be large. Consequently, we say that the circuit contains two dominant poles.
image_name:Figure 10.25 Two-stage op amp
description:This circuit is a two-stage operational amplifier. The first stage consists of a differential amplifier formed by M1 and M2, with active loads M3 and M4. The second stage is a common-source amplifier with M9 and M10 as active loads. The circuit includes compensation capacitors CL to stabilize the amplifier and improve the frequency response. There are two dominant poles at nodes E and A due to the high small-signal resistance and large load capacitance.

Figure 10.25 Two-stage op amp.
From these observations, we can construct the magnitude and phase plots shown in Fig. 10.26. Here, $\omega_{p, E}$ is assumed more dominant, but the relative positions of $\omega_{p, E}$ and $\omega_{p, A}$ depend on the design and the load capacitance. Note that, since the poles at $E$ and $A$ are relatively close to the origin, the phase

image_name:Figure 10.26 Bode plots of loop gain of two-stage op amp.
description:The graph in Figure 10.26 is a Bode plot representing the loop gain of a two-stage operational amplifier. It consists of two parts: the magnitude plot (top) and the phase plot (bottom), both plotted against frequency on a logarithmic scale.

Magnitude Plot:
- **Y-Axis:** The magnitude of the loop gain, expressed in decibels (dB) as \(20\log|\beta H(\omega)|\).
- **X-Axis:** Frequency \(\omega\), presented on a logarithmic scale.
- **Behavior:** The magnitude starts at a high level and remains flat over low frequencies, indicating a constant gain. As frequency increases, the magnitude begins to roll off, first at \(\omega_{p,E}\), followed by \(\omega_{p,A}\), and then \(\omega_{p,X}\). This roll-off indicates the effect of the dominant poles at these frequencies.
- **Key Features:**
- **\(\omega_{p,E}\):** The first pole, causing the initial decrease in magnitude.
- **\(\omega_{p,A}\):** The second pole, contributing to further attenuation.
- **\(\omega_{p,X}\):** A third pole, leading to a steeper decline in gain.

Phase Plot:
- **Y-Axis:** Phase shift of the loop gain, shown in degrees.
- **X-Axis:** Frequency \(\omega\), also on a logarithmic scale.
- **Behavior:** The phase starts near 0 degrees and decreases as frequency increases. It approaches \(-180^{\circ}\) before the third pole, indicating a significant phase shift due to the poles at \(\omega_{p,E}\) and \(\omega_{p,A}\). The phase continues to drop towards \(-270^{\circ}\) as the frequency reaches \(\omega_{p,X}\).
- **Key Features:**
- The phase margin is suggested to be close to zero before the third pole, emphasizing the need for frequency compensation.

Annotations:
- Dotted vertical lines mark the pole frequencies \(\omega_{p,E}\), \(\omega_{p,A}\), and \(\omega_{p,X}\).
- Horizontal dashed lines in the phase plot at \(-180^{\circ}\) and \(-270^{\circ}\) provide reference points for phase shifts.

Overall, the Bode plots illustrate the impact of the dominant poles on the loop gain and phase of the two-stage op amp, highlighting the need for careful frequency compensation to ensure stability.

approaches $-180^{\circ}$ well below the third pole. In other words, the phase margin may be close to zero even before the third pole contributes significant phase shift.

Let us now investigate the frequency compensation of two-stage op amps. In Fig. 10.26, one of the dominant poles must be moved toward the origin so as to place the gain crossover well below the phase crossover. However, recall from Sec. 10.4 that the unity-gain bandwidth after compensation cannot exceed the frequency of the second pole of the open-loop system for $\mathrm{PM}>45^{\circ}$. Thus, if in Fig. 10.26 the magnitude of $\omega_{p, E}$ is to be reduced, the available bandwidth is limited to approximately $\omega_{p, A}$, a low value. Furthermore, the very small magnitude of the new dominant pole translates to a large compensation capacitor.

Fortunately, a more efficient method of compensation can be applied to the circuit of Fig. 10.25. To arrive at this method, we note that, as illustrated in Fig. 10.27(a), the first stage exhibits a high output impedance, $R_{\text {out1 }}$, and the second stage provides a moderate gain, $A_{v 2}$, thereby creating a suitable environment for Miller multiplication of capacitors. Shown in Fig. 10.27(b), the idea is to create a large capacitance at node $E$, equal to $\left(1+A_{v 2}\right) C_{C}$, moving the corresponding pole to $R_{\text {out } 1}^{-1}\left[C_{E}+\left(1+A_{v 2}\right) C_{C}\right]^{-1}$, where $C_{E}$ denotes the capacitance at node $E$ before $C_{C}$ is added. As a result, a low-frequency pole can be established with a moderate capacitor value, saving considerable chip area. This technique is called "Miller compensation."
image_name:Figure 10.27 Miller compensation of a two-stage op amp.(a)
description:The system block diagram labeled "(a)" illustrates a basic two-stage operational amplifier configuration. The main components of this diagram are two amplifier stages. The first stage is denoted by $A_{v1}$, and the second stage is denoted by $A_{v2}$. These amplifiers are represented by triangular symbols, which are standard notations for amplifiers in circuit diagrams.

1. **Main Components:**
- **Amplifier $A_{v1}$:** This is the first stage of amplification, receiving the input signal and providing an amplified output to the next stage.
- **Amplifier $A_{v2}$:** This is the second stage of amplification, further amplifying the signal received from $A_{v1}$.

2. **Flow of Information or Control:**
- The signal flows from left to right, starting at the input of $A_{v1}$, where it is amplified and passed to node $E$.
- From node $E$, the signal continues to $A_{v2}$, where it undergoes further amplification before reaching the output labeled as $A$.
- There is a feedback path indicated by $R_{out1}$, which suggests feedback from the output of $A_{v1}$ back to its input or a related node, affecting the gain or stability of the amplifier.

3. **Labels, Annotations, and Key Indicators:**
- **$E$:** This is an intermediate node between the two amplifier stages.
- **$R_{out1}$:** This label indicates a feedback resistance or output resistance associated with the first stage, which plays a role in the feedback mechanism or output impedance.

4. **Overall System Function:**
- The primary function of this system is to amplify an input signal through two stages of amplification. The feedback mechanism via $R_{out1}$ helps in controlling the gain or enhancing the stability of the amplifier. This basic configuration sets the stage for further enhancements, such as Miller compensation, to improve performance by managing frequency response and stability.
image_name:Figure 10.27 Miller compensation of a two-stage op amp.(b)
description:The diagram labeled "(b)" illustrates a two-stage operational amplifier (op-amp) configuration employing Miller compensation. The key components in this system include two amplifiers and a compensation capacitor, denoted as $C_C$.

1. **Main Components:**
- **First Amplifier ($A_{v1}$):** This is the initial stage of the op-amp, receiving the input signal and providing an amplified output to the next stage.
- **Second Amplifier ($A_{v2}$):** This stage further amplifies the signal received from the first amplifier.
- **Compensation Capacitor ($C_C$):** Connected between the output of the second amplifier and the input of the first amplifier, it plays a crucial role in frequency compensation by affecting the pole locations in the amplifier's frequency response.

2. **Flow of Information or Control:**
- The signal flow begins at the input of the first amplifier $A_{v1}$, which amplifies the input signal and passes it to node $E$.
- From node $E$, the signal is fed into the second amplifier $A_{v2}$, which further amplifies the signal and outputs it to the final output node $A$.
- The compensation capacitor $C_C$ provides a feedback path from the output of $A_{v2}$ back to the input of the first amplifier $A_{v1}$, thereby influencing the frequency response and stability of the op-amp.

3. **Labels, Annotations, and Key Indicators:**
- The node labeled $E$ is a critical point in the circuit where the output of the first amplifier and the input of the second amplifier meet.
- The presence of $C_C$ indicates the implementation of Miller compensation, which is intended to shift the poles and stabilize the amplifier.

4. **Overall System Function:**
- The primary function of this system is to provide a stable, amplified output of an input signal through a two-stage amplification process. The addition of the compensation capacitor $C_C$ is crucial for achieving Miller compensation, which effectively increases the apparent capacitance at node $E$ and shifts the pole locations, thereby improving the stability and bandwidth of the op-amp. This arrangement reduces the necessary size of the compensation capacitor, saving space and resources in integrated circuit design.

In addition to lowering the required capacitor value, Miller compensation entails a very important property: it moves the output pole away from the origin. Illustrated in Fig. 10.28, this effect is called "pole splitting." To understand the underlying principle, we simplify the output stage of Fig. 10.25 as in Fig. 10.29 , where $R_{S}$ denotes the output resistance of the first stage and $R_{L}=r_{O 9} \| r_{O 11}$. From our
image_name:Figure 10.28 Pole splitting as a result of Miller compensation.
description:The graph in Figure 10.28 illustrates the concept of pole splitting as a result of Miller compensation in a two-stage operational amplifier. This is represented using a pole-zero plot, which is a common way to visualize the locations of poles and zeros in the complex plane.

1. **Type of Graph and Function**:
- The graph is a pole-zero plot, showing the effects of compensation on the pole locations in the s-plane (complex frequency plane).

2. **Axes Labels and Units**:
- The horizontal axis is labeled \( \sigma \) (real part of the complex frequency), and the vertical axis is labeled \( j\omega \) (imaginary part of the complex frequency).
- The axes are not explicitly marked with units, as they represent normalized frequency components.

3. **Overall Behavior and Trends**:
- Before compensation, the poles are located closer together along the \( \sigma \) axis, indicating a potential for instability or reduced phase margin in the amplifier.
- After compensation, the poles are split further apart along the \( \sigma \) axis, which increases the stability of the system by moving one of the poles to a lower frequency (closer to the origin) and the other to a higher frequency (further from the origin).

4. **Key Features and Technical Details**:
- The graph shows two poles before compensation, both positioned on the negative real axis, indicating a stable but potentially sluggish system.
- After compensation, the poles are split, with one pole moving towards the origin (lower frequency) and the other moving further to the left (higher frequency), enhancing the phase margin and stability of the amplifier.

5. **Annotations and Specific Data Points**:
- The graph uses arrows to indicate the direction of pole movement due to compensation.
- The labels "Before Compensation" and "After Compensation" clearly indicate the effect of Miller compensation on the pole positions.

This pole splitting is beneficial in amplifier design as it allows for a wider bandwidth and improved stability by effectively managing the locations of the poles in the frequency response.

image_name:Figure 10.29 (a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: g9}
name: CE, type: Capacitor, value: CE, ports: {Np: VDD, Nn: g9}
name: CC, type: Capacitor, value: CC, ports: {Np: g9, Nn: Vout}
name: M9, type: PMOS, ports: {S: VDD, D: Vout, G: g9}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a simplified two-stage op-amp with Miller compensation. It includes a PMOS transistor M9, resistors RS and RL, capacitors CE, CC, and CL, and a voltage source Vin. The compensation is achieved through the capacitor CC, which creates pole splitting to improve bandwidth and stability.

image_name:(b)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: Vout}
name: CE, type: Capacitor, value: CE, ports: {Np: VDD, Nn: Vout}
name: M9, type: PMOS, ports: {S: VDD, D: Vout, G: Vout}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a simplified two-stage op-amp with Miller compensation, featuring a PMOS transistor M9, resistors RS and RL, capacitors CE, CC, and CL, and a voltage source Vin. The compensation is achieved through the capacitor CC, which creates pole splitting to improve bandwidth and stability.

Figure 10.29 (a) Simplified circuit of a two-stage op amp, and (b) a rough model at high frequencies.
analysis in Chapter 6, we note that this compensated circuit contains two poles:

$$
\begin{align*}
& \omega_{p 1}^{\prime} \approx \frac{1}{R_{S}\left[\left(1+g_{m 9} R_{L}\right)\left(C_{C}+C_{G D 9}\right)+C_{E}\right]+R_{L}\left(C_{C}+C_{G D 9}+C_{L}\right)}  \tag{10.24}\\
& \omega_{p 2}^{\prime} \approx \frac{R_{S}\left[\left(1+g_{m 9} R_{L}\right)\left(C_{C}+C_{G D 9}\right)+C_{E}\right]+R_{L}\left(C_{C}+C_{G D 9}+C_{L}\right)}{\left.R_{S} R_{L}\left[\left(C_{C}+C_{G D 9}\right) C_{E}+\left(C_{C}+C_{G D 9}\right) C_{L}+C_{E} C_{L}\right)\right]} \tag{10.25}
\end{align*}
$$

These expressions are based on the assumption that $\left|\omega_{p 1}^{\prime}\right| \ll\left|\omega_{p 2}^{\prime}\right|$. Before compensation, however, $\omega_{p 1}$ and $\omega_{p 2}$ are of the same order of magnitude. For $C_{C}=0$ and relatively large $C_{L}$, we may approximate the magnitude of the output pole as $\omega_{p 2} \approx 1 /\left(R_{L} C_{L}\right)$.

To compare the magnitudes of $\omega_{p 2}^{\prime}$ before and after compensation, we consider a typical case: $C_{C}+$ $C_{G D 9} \gg C_{E}$, reducing (10.25) to $\omega_{p 2}^{\prime} \approx g_{m 9} /\left(C_{E}+C_{L}\right)$. Noting that typically $C_{E} \ll C_{L}$, we conclude that Miller compensation increases the magnitude of the output pole by roughly a factor of $g_{m 9} R_{L}$, a relatively large value. Intuitively, this is because at high frequencies, $C_{C}$ provides a low impedance between the gate and drain of $M_{9}$, reducing the resistance seen by $C_{L}$ from $R_{L}$ to roughly $R_{S}\left\|g_{m 9}^{-1}\right\| R_{L} \approx$ $g_{m 9}^{-1}\left[\right.$ Fig. 10.29(b)]. From another perspective, $C_{C}$ provides feedback around the second stage by sensing the output voltage; as a result, the output resistance falls and the second pole moves to higher frequencies. ${ }^{5}$

In summary, Miller compensation moves the interstage pole toward the origin and the output pole away from the origin, allowing a much greater bandwidth than that obtained by merely connecting the compensation capacitor from one node to ground. In practice, the choice of the compensation capacitor for proper phase margin requires some iteration because both poles move. The following example gives a rough estimate.

#### Example 10.6

The two-stage op amp of Fig. 10.25 incorporates Miller compensation to reach a phase margin of $45^{\circ}$. Estimate the compensation capacitor value.

[^72]
#### Solution

After frequency compensation, the dominant pole moves down to approximately $\left(g_{m 9} R_{L} C_{C} R_{S}\right)^{-1}$, where $R_{S}$ denotes the output resistance of the first stage, and the second pole moves up to roughly $g_{m 9} / C_{L}$. For a phase margin of $45^{\circ}$, the loop gain must drop to unity at the second pole. With a low-frequency loop gain of $\beta g_{m 1} R_{S} g_{m 9} R_{L}$, we consider the postcompensation plot in Fig. 10.30 (on linear axes) and write

$$
\begin{equation*}
|\beta H(\omega)| \approx \frac{\beta g_{m 1} R_{S} g_{m 9} R_{L}}{\sqrt{1+\omega^{2} / \omega_{p 1}^{, 2}}} \tag{10.26}
\end{equation*}
$$

where the effect of $\omega_{p 2}^{\prime}$ on the magnitude is neglected. At $\omega=\omega_{p 2}^{\prime}$, the second term under the square root dominates, and

$$
\begin{equation*}
\frac{\beta g_{m 1} R_{S} g_{m 9} R_{L}}{\omega_{p 2}^{\prime} / \omega_{p 1}^{\prime}}=1 \tag{10.27}
\end{equation*}
$$

image_name:Figure 10.30
description:The graph depicted in Figure 10.30 is a Bode plot, specifically representing the magnitude of a transfer function in relation to frequency. The x-axis is labeled with the angular frequency symbol \( \omega \), and the y-axis denotes the magnitude \( |\beta H(\omega)| \). The y-axis is scaled to show the magnitude in terms of \( \beta g_{m1} R_{S} g_{m2} R_{L} \), where \( g_{m1} \) and \( g_{m2} \) are transconductances, \( R_{S} \) is the source resistance, and \( R_{L} \) is the load resistance.

Overall Behavior and Trends:
The graph starts at a high magnitude level of \( \beta g_{m1} R_{S} g_{m2} R_{L} \) at low frequencies. As the frequency increases, the magnitude remains constant until it reaches the first pole frequency \( \omega_{p1}^{\prime} \). Beyond \( \omega_{p1}^{\prime} \), the magnitude begins to decrease, following a downward slope.

Key Features and Technical Details:
- The magnitude starts at a normalized value of \( \beta g_{m1} R_{S} g_{m2} R_{L} \) and remains constant until \( \omega_{p1}^{\prime} \).
- At \( \omega_{p1}^{\prime} \), the slope changes, indicating the influence of the first pole. The graph shows a typical roll-off behavior.
- The magnitude at the point \( \omega_{p1}^{\prime} \) is marked as 1, indicating a significant point where the behavior starts to change.
- As the frequency approaches \( \omega_{p2}^{\prime} \), the decrease in magnitude continues, suggesting a further reduction in gain.

Annotations and Specific Data Points:
- The graph includes annotations at the frequencies \( \omega_{p1}^{\prime} \) and \( \omega_{p2}^{\prime} \), which are critical points where the magnitude response changes notably.
- The horizontal line at the magnitude level of 1 serves as a reference point, highlighting where the magnitude equals unity.

This Bode plot effectively illustrates how the magnitude of the transfer function is affected by the pole frequencies, demonstrating a typical low-pass filter response with decreasing gain as frequency increases beyond the pole frequencies.

Substituting for the pole frequencies and assuming that $\beta=1$, we obtain

$$
\begin{equation*}
C_{C}=\frac{g_{m 1}}{g_{m 9}} C_{L} \tag{10.28}
\end{equation*}
$$

Note that $g_{m 1}$ and $g_{m 9}$ are the transconductances of the two stages. The reader can prove that, if the effect of $\omega_{p 2}^{\prime}$ is included, then $C_{C}=\left[g_{m 1} /\left(\sqrt{2} g_{m 9}\right)\right] C_{L}$. Of course, $C_{C}$ must generally be greater than this value so as to establish a higher phase margin, but this estimate serves as a reasonable starting point in the design.

This result assumes that $\beta=1$; in practice, most op amps are configured for a closed-loop gain of 2 or higher, thus requiring a smaller $C_{C}$.

Our study of stability and compensation has thus far neglected the effect of zeros of the transfer function. While in cascode topologies, the zeros are far from the origin, in two-stage op amps incorporating Miller compensation, a nearby zero appears in the circuit. Recall from Chapter 6 that the circuit of Fig. 10.29 contains a right-half-plane zero at $\omega_{z}=g_{m 9} /\left(C_{C}+C_{G D 9}\right)$. This is because $C_{C}+C_{G D 9}$ forms a "feedforward" signal path from the input to the output. What is the effect of such a zero? The numerator of the transfer function reads $\left(1-s / \omega_{z}\right)$, yielding a phase of $-\tan ^{-1}\left(\omega / \omega_{z}\right)$, a negative value because $\omega_{z}$ is positive. In other words, as with poles in the left half plane, a zero in the right half plane contributes additional negative phase shift, thus moving the phase crossover toward the origin. Furthermore, from Bode approximations, the zero slows down the drop of the magnitude, thereby pushing the gain crossover away from the origin. As a result, the stability degrades considerably.

To better understand the foregoing discussion, let us construct the Bode plots for a third-order system containing a dominant pole $\omega_{p 1}$, two nondominant poles $\omega_{p 2}$ and $\omega_{p 3}$, and a zero in the right half plane $\omega_{z}$. For two-stage op amps, typically $\left|\omega_{p 1}\right|<\left|\omega_{z}\right|<\left|\omega_{p 2}\right|$. As shown in Fig. 10.31, the zero introduces significant phase shift while preventing the gain from falling sufficiently.
image_name:Figure 10.31 Effect of right-half-plane zero
description:The graph in Figure 10.31 is a Bode plot, which consists of two plots: one for magnitude and one for phase, both plotted against frequency on a logarithmic scale.

Magnitude Plot:
- **Type:** Logarithmic plot of magnitude.
- **Y-Axis:** Represents the magnitude in decibels (dB), specifically \(20\log|\beta H(\omega)|\).
- **X-Axis:** Represents frequency \(\omega\) on a logarithmic scale.
- **Behavior:**
- The plot starts at a constant level, indicating a flat gain at low frequencies.
- As the frequency increases, the first pole \(\omega_{p1}\) causes the magnitude to begin decreasing at a rate of -20 dB/decade.
- The presence of the zero \(\omega_{z}\) temporarily flattens the slope, reducing the rate of decrease.
- After the zero, the second pole \(\omega_{p2}\) and third pole \(\omega_{p3}\) cause further decreases in the magnitude, each contributing an additional -20 dB/decade, resulting in a steeper slope.

Phase Plot:
- **Type:** Logarithmic plot of phase.
- **Y-Axis:** Represents the phase in degrees.
- **X-Axis:** Represents frequency \(\omega\) on a logarithmic scale.
- **Behavior:**
- The phase starts at 0 degrees and begins to decrease as frequency increases.
- The first pole \(\omega_{p1}\) causes the phase to drop towards -90 degrees.
- The right-half-plane zero \(\omega_{z}\) introduces a positive phase shift, which is atypical as it causes the phase to initially increase slightly before continuing to decrease.
- The subsequent poles \(\omega_{p2}\) and \(\omega_{p3}\) cause further phase decreases, moving the phase closer to -270 degrees.

Key Features:
- The graph clearly illustrates the effect of a right-half-plane zero, which notably alters the phase response and reduces the rate of magnitude decrease temporarily.
- Critical points like \(\omega_{p1}\), \(\omega_{z}\), \(\omega_{p2}\), and \(\omega_{p3}\) are marked, showing their impact on the system's frequency response.

#### Example 10.7

Noting that the Miller compensation in Fig. 10.29(a) yields $\omega_{p 2} \approx g_{m 9} / C_{L}$ and $\omega_{z} \approx g_{m 9} / C_{C}$, a student decides to choose $C_{C}=C_{L}$, aiming to cancel the second pole by the zero. Explain what happens.

#### Solution

Recall that the zero is located in the right half plane and the poles in the left half plane. The compensated loop transmission can therefore be expressed as

$$
\begin{equation*}
\beta H(s)=\frac{\beta A_{0}\left(1-\frac{s}{\omega_{z}}\right)}{\left(1+\frac{s}{\omega_{p 1}}\right)\left(1+\frac{s}{\omega_{p 2}}\right)} \tag{10.29}
\end{equation*}
$$

We recognize that the zero does not cancel the pole and still affects $|\beta H|$ and $\angle \beta H$.

The right-half-plane zero in two-stage CMOS op amps, given by $g_{m} /\left(C_{C}+C_{G D}\right)$, is a serious issue because $g_{m}$ is relatively small and $C_{C}$ is chosen large enough to position the dominant pole properly. Various techniques for eliminating or moving the zero have been invented. Illustrated in Fig. 10.32, places a resistor in series with the compensation capacitor, thereby modifying the zero frequency. The output stage now exhibits three poles, but for moderate values of $R_{z}$, the third pole is located at high frequencies and the first two poles are close to the values calculated with $R_{z}=0$. Moreover, it can be
image_name:Figure 10.32 Addition of $R_{z}$ to move the right-half-plane zero.
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: g9}
name: CE, type: Capacitor, value: CE, ports: {Np: VDD, Nn: g9}
name: M9, type: PMOS, ports: {S: VDD, D: Vout, G: g9}
name: RZ, type: Resistor, value: Rz, ports: {N1: g9, N2: r_c}
name: CC, type: Capacitor, value: CC, ports: {Np: r_c, Nn: Vout}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit diagram 'Figure 10.32' includes a PMOS transistor M9 with a compensation capacitor CC and a resistor RZ added to move the zero frequency. The output stage exhibits three poles with the addition of RZ.

shown (Problem 10.8) that the zero frequency is given by

$$
\begin{equation*}
\omega_{z} \approx \frac{1}{C_{C}\left(g_{m 9}^{-1}-R_{z}\right)} \tag{10.30}
\end{equation*}
$$

Thus, if $R_{z} \geq g_{m 9}^{-1}$, then $\omega_{z} \leq 0$. While $R_{z}=g_{m 9}^{-1}$ seems a natural choice, in practice we may even move the zero well into the left half plane so as to cancel the first nondominant pole. This occurs if

$$
\begin{equation*}
\frac{1}{C_{C}\left(g_{m 9}^{-1}-R_{z}\right)}=\frac{-g_{m 9}}{C_{L}+C_{E}} \tag{10.31}
\end{equation*}
$$

that is

$$
\begin{align*}
R_{z} & =\frac{C_{L}+C_{E}+C_{C}}{g_{m 9} C_{C}}  \tag{10.32}\\
& \approx \frac{C_{L}+C_{C}}{g_{m 9} C_{C}} \tag{10.33}
\end{align*}
$$

because $C_{E}$ is typically much less than $C_{L}+C_{C}$.
The possibility of canceling the nondominant pole makes this technique attractive, but in reality two important drawbacks must be considered. First, it is difficult to guarantee the relationship given by (10.33), especially if $C_{L}$ is unknown or variable. Mismatch between the pole and zero frequencies leads to the "doublet problem" (Problem 10.19). For example, as explained in Chapter 13, the load capacitance seen by an op amp may vary from one part of the period to another in switched-capacitor circuits, necessitating a corresponding change in $R_{z}$ and complicating the design. The second drawback relates to the actual implementation of $R_{z}$. Typically realized by a MOS transistor in the triode region (Fig. 10.33), $R_{z}$ changes substantially as output voltage excursions are coupled through $C_{C}$ to node $X$, thereby degrading the large-signal settling response.
image_name:Figure 10.33 Effect of large output swings on $R_{z}$.
description:The circuit diagram shows a configuration where the load capacitance and the resistor Rz are connected to an op amp. The PMOS transistors M9 and M0 are used to adjust the resistance Rz. The circuit is designed to maintain Rz equal to (1+CL/CC)/gm9 despite variations. The output voltage is labeled as Vout.

Generating $V_{b}$ in Fig. 10.33 is not straightforward because $R_{Z}$ must remain equal to $\left(1+C_{L} / C_{C}\right) / g_{m 9}$ despite process and temperature variations. A common approach is illustrated in Fig. 10.34 [2], where diode-connected devices $M_{13}$ and $M_{14}$ are placed in series. If $I_{1}$ is chosen with respect to $I_{D 9}$ such that $V_{G S 13}=V_{G S 9}$, then $V_{G S 15}=V_{G S 14}$. Since $g_{m 14}=\mu_{p} C_{o x}(W / L)_{14}\left(V_{G S 14}-V_{T H 14}\right)$ and $R_{o n 15}=$ $\left[\mu_{p} C_{o x}(W / L)_{15}\left(V_{G S 15}-V_{T H 15}\right)\right]^{-1}$, we have $R_{o n 15}=g_{m 14}^{-1}(W / L)_{14} /(W / L)_{15}$. For pole-zero cancellation to occur,

$$
\begin{equation*}
g_{m 14}^{-1} \frac{(W / L)_{14}}{(W / L)_{15}}=g_{m 9}^{-1}\left(1+\frac{C_{L}}{C_{C}}\right) \tag{10.34}
\end{equation*}
$$

image_name:Figure 10.34 Generation of Vb for proper temperature and process tracking.
description:
[
name: M13, type: PMOS, ports: {S: VDD, D: d13g13s14, G: d13g13s14}
name: M14, type: PMOS, ports: {S: d13g13s14, D: Vb, G: Vb}
name: M9, type: PMOS, ports: {S: VDD, D: Vout, G: g9}
name: M15, type: PMOS, ports: {S: g9, D: d15, G: Vb2}
name: M11, type: NMOS, ports: {S: GND, D: Vb2, G: Vout}
name: I1, type: CurrentSource, ports: {Np: Vb, Nn: GND}
name: CE, type: Capacitor, value: CE, ports: {Np: VDD, Nn: g9}
name: CC, type: Capacitor, value: CC, ports: {Np: d15, Nn: Vout}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is designed for generating a bias voltage Vb for proper temperature and process tracking. It involves PMOS and NMOS transistors, capacitors, a resistor, and a current source. The design ensures pole-zero cancellation and stability in the circuit.

and hence

$$
\begin{equation*}
(W / L)_{15}=\sqrt{(W / L)_{14}(W / L)_{9}} \sqrt{\frac{I_{D 9}}{I_{D 14}}} \frac{C_{C}}{C_{C}+C_{L}} \tag{10.35}
\end{equation*}
$$

If $C_{L}$ is constant, (10.35) can be established with reasonable accuracy because it contains only the ratio of quantities.

Another method of guaranteeing Eq. (10.33) is to use a simple resistor for $R_{Z}$ and define $g_{m 9}$ with respect to a resistor that closely matches $R_{Z}$ [3]. Depicted in Fig. 10.35, this technique incorporates $M_{b 1}-M_{b 4}$ along with $R_{S}$ to generate $I_{b} \propto R_{S}^{-2}$. (This circuit is studied in detail in Chapter 12.) Thus, $g_{m 9} \propto \sqrt{I_{D 9}} \propto \sqrt{I_{D 11}} \propto R_{S}^{-1}$. Proper ratioing of $R_{Z}$ and $R_{S}$ therefore ensures that (10.33) is valid even with temperature and process variations.
image_name:Figure 10.35
description:
[
name: Mb3, type: PMOS, ports: {S: VDD, D: X, G: Y}
name: Mb4, type: PMOS, ports: {S: sb4, D: Y, G: Y}
name: M9, type: PMOS, ports: {S: VDD, D: Vout, G: g9}
name: Mb1, type: NMOS, ports: {S: GND, D: X, G: X}
name: Mb2, type: NMOS, ports: {S: GND, D: X, G: Y}
name: M11, type: NMOS, ports: {S: GND, D: Vout, G: X}
name: RS, type: Resistor, value: RS, ports: {N1: VDD, N2: sb4}
name: CE, type: Capacitor, value: CE, ports: {Np: VDD, Nn: g9}
name: CC, type: Capacitor, value: CC, ports: {Np: r_c, Nn: Vout}
name: RZ, type: Resistor, value: RZ, ports: {N1: g9, N2: r_c}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is designed to define the transconductance g_{m9} with respect to the resistor RS. It incorporates PMOS transistors Mb3, Mb4, M9 and NMOS transistors Mb1, Mb2, M11, along with resistors RS, RZ, and capacitors CE, CC, CL. The circuit aims to ensure g_{m9} is proportional to the inverse of RS, even considering temperature and process variations.

Figure 10.35 Method of defining $g_{m 9}$ with respect to $R_{S}$.

The principal drawback of the two methods described above is that they assume square-law characteristics for all of the transistors. As described in Chapter 17, short-channel MOSFETs may substantially deviate from the square-law regime, creating errors in the foregoing calculations. In particular, transistor $M_{9}$ is typically a short-channel device because it appears in the signal path and its raw speed is critical.

An attribute of two-stage op amps that makes them inferior to "one-stage" op amps is the susceptibility to the load capacitance. Since Miller compensation establishes the dominant pole at the output of the first stage, a higher load capacitance presented to the second stage moves the second pole toward the origin, degrading the phase margin. By contrast, in one-stage op amps, a higher load capacitance brings the dominant pole closer to the origin, improving the phase margin (albeit making the feedback system more overdamped). Illustrated in Fig. 10.36 is the step response of a unity-gain feedback amplifier employing a one-stage or a two-stage op amp, suggesting that the response approaches an oscillatory behavior if the load capacitance seen by the two-stage op amp increases.
image_name:Figure 10.36 Effect of increased load capacitance on step response of one- and two-stage op amps.
description:The graph in Figure 10.36 illustrates the step response of a unity-gain feedback amplifier using both one-stage and two-stage operational amplifiers (op amps). The graph is divided into two sections, each representing a different configuration of op amp.

Type of Graph and Function:
The graph is a time-domain waveform depicting the step response of the amplifier circuits. It shows how the output voltage \( V_{out} \) changes over time \( t \) in response to a step input \( V_{in} \).

Axes Labels and Units:
- **X-axis:** Represents time \( t \), though units are not explicitly labeled, it is typically in seconds or milliseconds in such contexts.
- **Y-axis:** Represents the output voltage \( V_{out} \), indicating the response level, but specific voltage units are not provided.

Overall Behavior and Trends:
- **One-Stage Op Amp (Left Graph):** The response shows a smooth rise to the final value without overshoot. The solid line represents the response with a standard load capacitance \( C_L \), while the dashed line shows the response with a larger load capacitance. The larger capacitance results in a slower rise time, indicating a more overdamped system.
- **Two-Stage Op Amp (Right Graph):** This response exhibits oscillatory behavior, especially with larger load capacitance \( C_L \). The solid line is the response with standard \( C_L \), showing some overshoot and ringing. The dashed line, representing a larger \( C_L \), shows increased oscillations and longer settling time, approaching instability.

Key Features and Technical Details:
- **One-Stage Op Amp:** The response is stable and non-oscillatory, with larger load capacitance increasing the damping and reducing the speed of response.
- **Two-Stage Op Amp:** The response becomes more oscillatory with increased load capacitance, indicating a reduction in phase margin and potential instability.

Annotations and Specific Data Points:
- The graphs are annotated with labels indicating the effect of a 'Larger \( C_L \),' highlighting the changes in the response due to increased load capacitance.

This graph effectively demonstrates how increased load capacitance affects the stability and speed of response in one-stage versus two-stage op amps, with the former becoming more overdamped and the latter more prone to oscillations.

## 10.6 ■ Slewing in Two-Stage Op Amps

It is instructive to study the slewing characteristics of two-stage op amps. Before delving into the details, let us consider the simple circuit shown in Fig. 10.37(a), where $I_{i n}$ is a current step given by $I_{S S} u(t)$ and $C_{F}$ has a zero initial condition. If $A$ is large, node $X$ is a virtual ground and the voltage across $C_{F}$ is approximately equal to $V_{o u t}$. Receiving a constant current equal to $I_{S S}, C_{F}$ generates an output voltage given by

$$
\begin{equation*}
V_{\text {out }}(t) \approx \frac{I_{S S}}{C_{F}} t \tag{10.36}
\end{equation*}
$$

image_name:(a)
description:
[
name: CF, type: Capacitor, value: CF, ports: {Np: X, Nn: Vout}
name: A, type: OpAmp, value: -A, ports: {InP: X, Out: Vout}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: X, Nn: GND}
]
extrainfo:The circuit is a simple integrator with an op-amp, capacitor CF, and current source Iin. Node X is a virtual ground due to the high gain of the op-amp.
image_name:(b)
description:
[
name: CF, type: Capacitor, value: CF, ports: {Np: X, Nn: Vout}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: X, Nn: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: Vout}
name: Mout, type: NMOS, ports: {S: GND, D: Vout, G: X}
name: ro, type: Resistor, value: ro, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit in Fig. 10.37(b) is an implementation of an integrator with a current input Iin, using an op-amp, capacitor CF, and NMOS transistor Mout. The output voltage Vout is determined by the integration of the input current over time, with the NMOS transistor providing additional current control. The output waveform during slewing is shown in Fig. 10.37(c), illustrating the linear increase of Vout over time.
image_name:(c)
description:The graph in Figure 10.37(c) is a time-domain waveform illustrating the output voltage \( V_{out}(t) \) of a circuit during the slewing phase.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph showing the relationship between output voltage and time.

2. **Axes Labels and Units:**
- The horizontal axis represents time \( t \).
- The vertical axis represents the output voltage \( V_{out}(t) \).
- No specific units are given, but time is typically in seconds and voltage in volts.

3. **Overall Behavior and Trends:**
- The graph shows a linear increase in the output voltage over time.
- Initially, the voltage starts from a negative value \( \frac{-I_{SS}}{g_m + r_O^{-1}} \) and increases linearly, indicating a constant rate of change.

4. **Key Features and Technical Details:**
- The slope of the line is given by \( \frac{I_{SS}}{C_F(1 + \frac{1}{g_m r_O})} \), which represents the rate of change of the output voltage.
- The graph starts from a negative voltage value, indicating an initial condition influenced by the circuit parameters.
- The linear region of the graph represents the slewing behavior, where the output voltage changes at a constant rate determined by the input current and circuit capacitance.

5. **Annotations and Specific Data Points:**
- The graph includes a dashed line indicating the slope of the linear region, emphasizing the relationship between the current \( I_{SS} \), the capacitance \( C_F \), and the transconductance \( g_m \) and output resistance \( r_O \).
- The initial voltage point \( \frac{-I_{SS}}{g_m + r_O^{-1}} \) is a critical value that highlights the starting condition of the waveform.

Figure 10.37 (a) Simplified circuit for slew study, (b) realization of (a), and (c) output waveform during slewing.
We now consider the implementation depicted in Fig. $10.37(\mathrm{~b})^{6}$ and write $V_{\text {out }} / r_{O}+g_{m} V_{X}+I_{\text {in }}=I_{1}$ and $C_{F} d\left(V_{\text {out }}-V_{X}\right) / d t=I_{i n}$. Substituting for $V_{X}$ from the former equation in the latter, we have

$$
\begin{equation*}
C_{F}\left(1+\frac{1}{g_{m} r_{O}}\right) \frac{d V_{\text {out }}}{d t}=I_{\text {in }}-\frac{C_{F}}{g_{m}} \frac{d I_{\text {in }}}{d t} \tag{10.37}
\end{equation*}
$$

We consider the terms on the right-hand side as two inputs and apply superposition, obtaining

$$
\begin{equation*}
V_{\text {out }}(t)=\frac{I_{S S}}{C_{F}\left(1+\frac{1}{g_{m} r_{O}}\right)} t u(t)-\frac{I_{S S}}{g_{m}+\frac{1}{r_{O}}} u(t) \tag{10.38}
\end{equation*}
$$

(This voltage, of course, rides on top of a bias value.) As illustrated in Fig. 10.37(c), $V_{\text {out }}$ initially jumps to $-I_{S S} /\left(g_{m}+r_{O}^{-1}\right)$ and subsequently ramps up with a slope equal to $I_{S S} /\left[C_{F}\left(1+g_{m}^{-1} r_{O}^{-1}\right)\right]$. It is interesting to note that (1) at $t=0^{+}, C_{F}$ acts as a short circuit, allowing $I_{i n}$ to flow through $\left(1 / g_{m}\right) \| r_{O}$ and creating a downward step at the output; (2) the slope of the ramp suggests an equivalent capacitance of $C_{F}\left(1+g_{m}^{-1} r_{O}^{-1}\right)$, revealing the Miller effect of $C_{F}$ at the output; and (3) Eq. (10.38) does not depend on $I_{1}$ because this current simply serves as the bias current of $M_{\text {out }}$. We approximate the output voltage as $V_{\text {out }}(t) \approx\left(I_{S S} / C_{F}\right) t u(t)$.

Let us return to a two-stage op amp and suppose that in Fig. 10.38(a), $V_{i n}$ experiences a large positive step at $t=0$, turning off $M_{2}, M_{4}$, and $M_{3}$. The circuit can then be simplified to that in Fig. 10.38(b), revealing that $C_{C}$ is charged by a constant current $I_{S S}$ if parasitic capacitances at node $X$ are negligible. Recognizing that the gain of the output stage makes node $X$ a virtual ground, we write $V_{\text {out }}(t) \approx$ $\left(I_{S S} t / C_{C}\right) u(t)$. Thus, the positive slew rate ${ }^{7}$ equals $I_{S S} / C_{C}$. Note that during slewing, $M_{5}$ must provide two currents: $I_{S S}$ and $I_{1}$. If $M_{5}$ is not wide enough to sustain $I_{S S}+I_{1}$ in saturation, then $V_{X}$ drops significantly, possibly driving $M_{1}$ into the triode region.
image_name:(a)
description:The diagram labeled (a) represents a simple two-stage operational amplifier (op-amp) circuit. This op-amp consists of the following main components:

1. **Input Differential Pair**: Transistors M1 and M2 form the input differential pair, which receives the input voltage $V_{in}$. This pair is biased by a constant current source $I_{SS}$ connected to the ground ($GND$).

2. **Current Mirrors**: Transistors M3 and M4 act as a current mirror, which replicates the current through M1 to M4. This configuration helps in converting the differential input signal into a single-ended output.

3. **Second Gain Stage**: Transistor M5 acts as the second gain stage, which is connected to the supply voltage $V_{DD}$. This stage provides additional amplification to the signal processed by the input stage.

4. **Compensation Capacitor (C_C)**: The capacitor $C_C$ is connected between the output of the first stage (node X) and the output of the second stage ($V_{out}$). This capacitor is crucial for frequency compensation, ensuring stability of the op-amp by controlling the bandwidth and phase margin.

5. **Output Stage**: The output voltage is taken across $V_{out}$, which is connected to another current source $I_1$ to ground. This stage provides the final amplified output.

**Flow of Information**:
- The input voltage $V_{in}$ is applied to the gate of M1.
- The differential pair (M1, M2) converts the input voltage difference into a current difference, which is mirrored by M3 and M4.
- The current through M4 is fed into the gate of M5, amplifying the signal further.
- The compensation capacitor $C_C$ helps stabilize the op-amp by providing a feedback path from the output to the node X.

**Overall System Function**:
This op-amp is designed to amplify the input signal applied at $V_{in}$, providing a larger output signal at $V_{out}$. The use of a differential pair allows the op-amp to reject common-mode signals, enhancing the precision of amplification. The compensation capacitor ensures the stability of the op-amp across a range of frequencies, making it suitable for a variety of analog signal processing applications.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin}
name: M5, type: PMOS, ports: {S: VDD, D: Vout, G: X}
name: Cc, type: Capacitor, value: Cc, ports: {Np: X, Nn: Vout}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: P, Nn: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a simplified two-stage operational amplifier during positive slewing. M1 is an NMOS transistor connected to the input, and M5 is a PMOS transistor providing current to the output. The capacitor Cc is used for compensation between node X and Vout. Current sources Iss and I1 are used for biasing and output current, respectively.
image_name:(c)
description:
[
name: M3, type: PMOS, ports: {S: VDD, D: X, G: Vb}
name: M5, type: PMOS, ports: {S: VDD, D: Vout, G: X}
name: CC, type: Capacitor, value: CC, ports: {Np: X, Nn: Vout}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit diagram represents a simplified two-stage op-amp during negative slewing. The current ISS flows into node x, which is also connected to the drain of M3 and the source of M5. The capacitor CC is connected between node x and Vout. The current source I1 is connected from Vout to ground. M3 and M5 are PMOS transistors with their sources connected to VDD.

Figure 10.38 (a) Simple two-stage op amp, (b) simplified circuit during positive slewing, and (c) simplified circuit during negative slewing.

For the negative slew rate, we simplify the circuit as shown in Fig. 10.38(c). Here $I_{1}$ must support both $I_{S S}$ and $I_{D 5}$. For example, if $I_{1}=I_{S S}$, then $V_{X}$ rises so as to turn off $M_{5}$. If $I_{1}<I_{S S}$, then $M_{3}$ enters the triode region and the slew rate is given by $I_{D 3} / C_{C}$.

#### Example 10.8

Op amps typically drive a heavy load capacitance. Repeat the slew rate analysis if the circuit of Fig. 10.37(b) sees a load capacitance of $C_{L}$. For simplicity, neglect channel-length modulation.

#### Solution

We consider two cases: $I_{i n}$ flows into or out of node $X$. With $\lambda=0$, the steady-state gain from $V_{X}$ to $V_{\text {out }}$ is infinite, forcing $X$ to be a virtual ground node. In the first case [Fig. 10.39(a)], $I_{i n}=I_{S S u}(t)$ flows through $C_{F}$, generating a ramp voltage across it. Since $V_{X}$ is constant, the voltage at the right terminal of $C_{F}, V_{\text {out }}$, must fall at a rate of $I_{S S} / C_{F}$. This also means that $C_{L}$ is discharged at the same rate, requiring that the transistor draw three currents: $I_{1}, I_{S S}$, and $C_{L} d V_{\text {out }} / d t=\left(C_{L} / C_{F}\right) I_{S S}$. Thus, so long as $M_{\text {out }}$ remains in saturation, the output slew rate is approximately equal to $I_{S S} / C_{F}$.
image_name:(a)
description:
[
name: CF, type: Capacitor, value: CF, ports: {Np: Vout, Nn: X}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
name: Mout, type: NMOS, ports: {S: GND, D: Vout, G: X}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: Vout}
name: Issu(t), type: CurrentSource, value: Issu(t), ports: {Np: VDD, Nn: X}
]
extrainfo:The circuit is a current-controlled ramp generator. The NMOS transistor Mout controls the discharge of the capacitors CF and CL. The output voltage Vout changes at a rate determined by the current Issu(t) and the capacitance CF.
image_name:(b)
description:
[
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: Vout}
name: CF, type: Capacitor, value: CF, ports: {Np: Vout, Nn: X}
name: Mout, type: NMOS, ports: {S: GND, D: Vout, G: X}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
name: Issu(t), type: CurrentSource, value: Issu(t), ports: {Np: X, Nn: GND}
]
extrainfo:The circuit is a configuration involving a current source I1, capacitors CF and CL, and an NMOS transistor Mout. It is designed to control the output voltage Vout, with node X acting as a virtual ground. The current Issu(t) flows into node X, and the NMOS transistor Mout helps regulate the discharge of CL.
image_name:(c)
description:
[
name: I_SS, type: CurrentSource, value: I_SS, ports: {Np: X, Nn: GND}
name: C_F, type: Capacitor, value: C_F, ports: {Np: Vout, Nn: X}
name: C_L, type: Capacitor, value: C_L, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is designed to control the output slew rate by adjusting the current through the NMOS transistor M_out. The current source I_1 is adjusted by subtracting I_SS, affecting the voltage across the capacitors C_F and C_L, which in turn controls the rate of change of Vout.

Now, let us study the second case [Fig. 10.39(b)]. If $X$ is a virtual ground, $V_{\text {out }}$ must rise at a rate of $I_{S S} / C_{F}$, and $C_{L}$ must also receive a current of $C_{L} d V_{\text {out }} / d t=\left(C_{L} / C_{F}\right) I_{S S}$. We observe that, if $I_{1}>I_{S S}\left(C_{L} / C_{F}\right)+I_{S S}$, then $M_{\text {out }}$ remains on, $V_{X}$ varies little, and the output slew rate is equal to $I_{S S} / C_{F}$. On the other hand, if $I_{1}<$ $\left(1+C_{L} / C_{F}\right) I_{S S}, M_{\text {out }}$ turns off, the difference between $I_{1}$ and $I_{S S}$ charges $C_{L}$ [Fig. 10.39(c)], and the slew rate is given by $\left(I_{1}-I_{S S}\right) / C_{L}$, a low value.

Two-Stage Class-AB Op Amps The two-stage class-AB op amp studied in Chapter 9 can incorporate Miller compensation as well. Recall, however, that the current mirrors in the signal path contribute an additional pole, degrading the phase margin. For this reason, two-stage class-AB op amps are typically slower than their class-A counterparts.

We wish to compute the slew rate of two-stage class-AB op amps. Let us redraw the circuit of Fig. 10.39(b) for this op amp topology (Fig. 10.40). In this case, too, the slew rate is equal to ( $\left.I_{1}-I_{S S}\right) / C_{L}$ if $M_{\text {out }}$ turns off, but, by virtue of class-AB operation, $I_{1}$ itself can be quite large. The current mirror action yields $I_{1}=\left(W_{p 1} / W_{p 2}\right) \alpha I_{i n}$ and hence a slew rate of $\left[\alpha\left(W_{p 1} / W_{p 2}\right)-1\right] I_{S S} / C_{L}$.
image_name:Figure 10.40 Simplified class-AB op amp
description:
[
name: Mp2, type: PMOS, ports: {S: VDD, D: Y, G: Y}
name: Mp1, type: PMOS, ports: {S: VDD, D: Vout, G: Y}
name: Mout, type: NMOS, ports: {S: GND, D: Vout, G: X}
name: CF, type: Capacitor, value: CF, ports: {Np: Vout, Nn: X}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
name: αIin, type: CurrentSource, value: αIin, ports: {Np: Y, Nn: GND}
]
extrainfo:The diagram represents a simplified class-AB operational amplifier. The circuit features a PMOS current mirror formed by Mp2 and Mp1, and an NMOS output stage Mout. The capacitors CF and CL provide frequency compensation and load capacitance, respectively. The current sources αIin and I1 are used for biasing and setting the operating point of the amplifier.

## 10.7 ■ Other Compensation Techniques

The difficulty in compensating two-stage CMOS op amps arises from the feedforward path formed by the compensation capacitor [Fig. 10.41(a)]. If $C_{C}$ could conduct current from the output node to node $X$ but not vice versa, then the zero would move to a very high frequency. As shown in Fig. 10.41(b), this can be accomplished by inserting a source follower in series with the capacitor. Since the gate-source capacitance of $M_{2}$ is typically much less than $C_{C}$, we expect the right-half-plane zero to occur at high frequencies. Assuming that $\gamma=\lambda=0$ for the source follower, neglecting some of the device capacitances, and simplifying the circuit as shown in Fig. 10.42, we can write $-g_{m 1} V_{1}=V_{\text {out }}\left(R_{L}^{-1}+C_{L} s\right)$, and hence

$$
\begin{equation*}
V_{1}=\frac{-V_{\text {out }}}{g_{m 1} R_{L}}\left(1+R_{L} C_{L} s\right) \tag{10.39}
\end{equation*}
$$

image_name:Figure 10.41 (a)
description:
[
name: A0, type: OpAmp, value: A0, ports: {InP: Vip, InN: Vin, Out: X}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: X}
name: CC, type: Capacitor, value: CC, ports: {Np: X, Nn: Vout}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: Vout}
]
extrainfo:Figure 10.41 (a) shows a two-stage op-amp with a right-half-plane zero due to the compensation capacitor CC. The op-amp is followed by an NMOS transistor M1, which is used for output buffering. The circuit is powered by a current source I1 connected to VDD, with the output taken at Vout.
image_name:Figure 10.41 (b)
description:
[
name: A0, type: OpAmp, value: A0, ports: {InP: Vip, InN: Vin, Out: X}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: X}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: Vout}
name: CC, type: Capacitor, value: CC, ports: {Np: X, Nn: S2}
name: M2, type: NMOS, ports: {S: s2, D: VDD, G: Vout}
name: I2, type: CurrentSource, value: I2, ports: {Np: S2, Nn: GND}
]
extrainfo:The circuit is a two-stage op amp with a source follower added to remove the right-half-plane zero due to CC. M2 acts as a source follower, and I2 is used to bias M2. The circuit operates with VDD as the power supply and GND as the ground reference.

Figure 10.41 (a) Two-stage op amp with right-half-plane zero due to $C_{C}$; (b) addition of a source follower to remove the zero.
image_name:Figure 10.42 Simplified equivalent circuit of Fig. 10.41(b).
description:The circuit is a two-stage op amp with a source follower added to remove the right-half-plane zero due to CC. M2 acts as a source follower, and I2 is used to bias M2. The circuit operates with VDD as the power supply and GND as the ground reference.

We also have

$$
\begin{equation*}
\frac{V_{\text {out }}-V_{1}}{\frac{1}{g_{m 2}}+\frac{1}{C_{C} s}}+I_{\text {in }}=\frac{V_{1}}{R_{S}} \tag{10.40}
\end{equation*}
$$

Substituting for $V_{1}$ from (10.39) yields

$$
\begin{equation*}
\frac{V_{\text {out }}}{I_{\text {in }}}=\frac{-g_{m 1} R_{L} R_{S}\left(g_{m 2}+C_{C} s\right)}{R_{L} C_{L} C_{C}\left(1+g_{m 2} R_{S}\right) s^{2}+\left[\left(1+g_{m 1} g_{m 2} R_{L} R_{S}\right) C_{C}+g_{m 2} R_{L} C_{L}\right] s+g_{m 2}} \tag{10.41}
\end{equation*}
$$

Thus, the circuit contains a zero in the left half plane, which can be chosen to cancel one of the poles. The zero can also be derived as illustrated in Fig. 6.18.

We can also compute the magnitudes of the two poles, assuming that they are widely separated. Since typically $1+g_{m 2} R_{S} \gg 1$ and $\left(1+g_{m 1} g_{m 2} R_{L} R_{S}\right) C_{C} \gg g_{m 2} R_{L} C_{L}$, we have

$$
\begin{align*}
\omega_{p 1} & \approx \frac{g_{m 2}}{g_{m 1} g_{m 2} R_{L} R_{S} C_{C}}  \tag{10.42}\\
& \approx \frac{1}{g_{m 1} R_{L} R_{S} C_{C}} \tag{10.43}
\end{align*}
$$

and

$$
\begin{align*}
\omega_{p 2} & \approx \frac{g_{m 1} g_{m 2} R_{L} R_{S} C_{C}}{R_{L} C_{L} C_{C} g_{m 2} R_{S}}  \tag{10.44}\\
& \approx \frac{g_{m 1}}{C_{L}} \tag{10.45}
\end{align*}
$$

Thus, the new values of $\omega_{p 1}$ and $\omega_{p 2}$ are similar to those obtained by simple Miller approximation. For example, the output pole has moved from $\left(R_{L} C_{L}\right)^{-1}$ to $g_{m 1} / C_{L}$.

The primary issue in the circuit of Fig. 10.41(b) is that the source follower limits the lower end of the output voltage to $V_{G S 2}+V_{I 2}$, where $V_{I 2}$ is the voltage required across $I_{2}$. For this reason, it is desirable to utilize the compensation capacitor to isolate the dc levels in the active feedback stage from that at the output. Such a topology is depicted in Fig. 10.43, where $C_{C}$ and the common-gate stage $M_{2}$ convert the output voltage swing to a current, returning the result to the gate of $M_{1}$ [4]. If $V_{1}$ changes by $\Delta V$ and $V_{\text {out }}$ by $A_{v} \Delta V$, then the current through the capacitor is nearly equal to $A_{v} \Delta V C_{C} s$ because $1 / g_{m 2}$ can be relatively small. Thus, a change $\Delta V$ at the gate of $M_{1}$ creates a current change of $A_{v} \Delta V C_{C} s$, providing a capacitor multiplication factor equal to $A_{v}$.

Assuming that $\lambda=\gamma=0$ for the common-gate stage, we redraw the circuit of Fig. 10.43 in Fig. 10.44, where we have

$$
\begin{equation*}
V_{\text {out }}+\frac{g_{m 2} V_{2}}{C_{C} s}=-V_{2} \tag{10.46}
\end{equation*}
$$

image_name:Figure 10.43 Compensation technique using a common-gate stage.
description:The circuit is a two-stage amplifier with compensation using a common-gate stage. The first stage is an operational amplifier with a feedback resistor RS. The second stage includes a PMOS and NMOS transistor, providing a compensation technique. The compensation capacitor CC connects between the output and intermediate node g1d2. Current sources I1, I2, and I3 provide biasing for the circuit.

image_name:Figure 10.44 Simplified equivalent circuit of Fig. 10.43.
description:The circuit is a two-stage amplifier with a common-gate stage for compensation. It includes an operational amplifier with a feedback resistor RS, and a PMOS and NMOS transistor for compensation. A compensation capacitor CC connects the output and intermediate node g1. Biasing is provided by current sources I1, I2, and I3.

and hence

$$
\begin{equation*}
V_{2}=-V_{\text {out }} \frac{C_{C} s}{C_{C} s+g_{m 2}} \tag{10.47}
\end{equation*}
$$

Also,

$$
\begin{equation*}
g_{m 1} V_{1}+V_{\text {out }}\left(\frac{1}{R_{L}}+C_{L} s\right)=g_{m 2} V_{2} \tag{10.48}
\end{equation*}
$$

and $I_{i n}=V_{1} / R_{S}+g_{m 2} V_{2}$. Solving these equations, we obtain

$$
\begin{equation*}
\frac{V_{\text {out }}}{I_{\text {in }}}=\frac{-g_{m 1} R_{S} R_{L}\left(g_{m 2}+C_{C} s\right)}{R_{L} C_{L} C_{C} S^{2}+\left[\left(1+g_{m 1} R_{S}\right) g_{m 2} R_{L} C_{C}+C_{C}+g_{m 2} R_{L} C_{L}\right] s+g_{m 2}} \tag{10.49}
\end{equation*}
$$

As with the circuit of Fig. 10.41(b), this topology contains a zero in the left half plane. Using similar approximations, we compute the poles as

$$
\begin{align*}
& \omega_{p 1} \approx \frac{1}{g_{m 1} R_{L} R_{S} C_{C}}  \tag{10.50}\\
& \omega_{p 2} \approx \frac{g_{m 2} R_{s} g_{m 1}}{C_{L}} \tag{10.51}
\end{align*}
$$

Interestingly, the second pole has considerably risen in magnitude - by a factor of $g_{m 2} R_{S}$ with respect to that of the circuit of Fig. 10.41. This is because at very high frequencies, the feedback loop consisting of $M_{2}$ and $R_{S}$ in Fig. 10.43 lowers the output resistance by the same factor. Of course, if the capacitance at the gate of $M_{1}$ is taken into account, pole splitting is less pronounced. Nevertheless, this technique can potentially provide a high bandwidth in two-stage op amps.

The op amp of Fig. 10.43 entails important slewing issues. For positive slewing at the output, the simplified circuit of Fig. 10.45(a) suggests that $M_{2}$ and hence $I_{1}$ must support $I_{S S}$, requiring that $I_{1} \geq$ $I_{S S}+I_{D 1}$. If $I_{1}$ is less, then $V_{P}$ drops, turning $M_{1}$ off, and if $I_{1}<I_{S S}, M_{0}$ and its tail current source must enter the triode region, yielding a slew rate equal to $I_{1} / C_{C}$.
image_name:(a)
description:
[
name: M0, type: NMOS, ports: {S: GND, D: P, G: s0}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: P}
name: M2, type: PMOS, ports: {S: VDD, D: X, G: Vb}
name: M00, type: PMOS, ports: {S: VDD, D: P, G: Vin}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: Vout}
name: I2, type: CurrentSource, value: I2, ports: {Np: P, Nn: GND}
name: I3, type: CurrentSource, value: I3, ports: {Np: VDD, Nn: X}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: s0, Nn: GND}
name: CC, type: Capacitor, value: CC, ports: {Np: X, Nn: Vout}
]
extrainfo:The circuit represents a simplified two-stage operational amplifier during positive slewing. It includes NMOS and PMOS transistors, current sources, and a capacitor for compensation. The nodes are labeled according to their function within the circuit, with VDD as the power supply and GND as the ground. The current sources I1, I2, and I3 are equal in value, supporting the slewing operation.
image_name:(b)
description:
[
name: M0, type: PMOS, ports: {S: VDD, D: P, G: Vin}
name: M2, type: PMOS, ports: {S: VDD, D: X, G: Vb}
name: M1, type: NMOS, ports: {S: GND, D: P, G: X}
name: M00, type: PMOS, ports: {S: VDD, D: P, G: Vin}
name: Cc, type: Capacitor, value: Cc, ports: {Np: X, Nn: Vout}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: X}
name: I2, type: CurrentSource, value: I2, ports: {Np: P, Nn: GND}
name: I3, type: CurrentSource, value: I3, ports: {Np: VDD, Nn: X}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: VDD, Nn: P}
]
extrainfo:The circuit diagram represents a two-stage operational amplifier during negative slewing. The current sources I1, I2, and I3 are equal, i.e., I3 = I2 = I1. The PMOS transistors M0, M2, and M00 are configured with their sources connected to VDD, while the NMOS transistor M1 has its source connected to GND. The capacitor Cc is connected between nodes X and Vout.

Figure 10.45 Circuit of Fig. 10.43 during (a) positive and (b) negative slewing.
For negative slewing, $I_{2}$ must support both $I_{S S}$ and $I_{D 2}$ [Fig. 10.45(b)]. As $I_{S S}$ flows into node $P, V_{P}$ tends to rise, increasing $I_{D 1}$. Thus, $M_{1}$ absorbs the current produced by $I_{3}$ through $C_{C}$, turning off $M_{2}$ and opposing the increase in $V_{P}$. We can therefore consider $P$ a virtual ground node. This means that,
for equal positive and negative slew rates, $I_{3}$ (and hence $I_{2}$ ) must be as large as $I_{S S}$, raising the power dissipation.

Op amps using a cascode topology as their first stage can incorporate a variant of the technique illustrated in Fig. 10.43. Shown in Fig. 10.46(a), this approach places the compensation capacitor between the source of the cascode devices and the output nodes. Using the simplified model of Fig. 10.46(b) and the method of Fig. 6.18, the reader can prove that the zero appears at $\left(g_{m 4} R_{e q}\right)\left(g_{m 9} / C_{C}\right)$, a much greater magnitude than $g_{m 9} / C_{C}$. If other capacitances are neglected, it can also be proved that the dominant pole is located at approximately $\left(R_{e q} g_{m 9} R_{L} C_{C}\right)^{-1}$, as if $C_{C}$ were connected to the gate of $M_{9}$ rather the source of $M_{4}$. The first nondominant pole is given by $g_{m 4} g_{m 9} R_{e q} / C_{L}$, an effect similar to that described by Eq. (10.51). In reality, the capacitance at $X$ may create a significant pole because the resistance seen at this node is quite large. The analysis of the slew rate is left as an exercise for the reader. (One can also insert a resistor in series with each $C_{C}$ to move the zero frequency.)

It is possible to combine two compensation techniques. As shown in Fig. 10.46(a), both $C_{C}$ and $C_{C}^{\prime}$ provide greater flexibility in the design.
image_name:Figure 10.46 (a)
description:The circuit in Figure 10.46 (a) is an alternative method of compensating two-stage operational amplifiers, using both CC and CC' for greater design flexibility. The circuit includes a combination of NMOS and PMOS transistors, capacitors for compensation and load, and current sources for biasing. The compensation capacitors CC and CC' are used to manage stability and frequency response. The circuit aims to improve the slew rate and stability of the op-amp stages.
image_name:(b)
description:
[
name: M4, type: NMOS, ports: {S: s4, D: X, G: GND}
name: M9, type: PMOS, ports: {S: GND, D: Vout, G: X}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
name: Cc, type: Capacitor, value: Cc, ports: {Np: s4, Nn: Vout}
name: Req, type: Resistor, value: Req, ports: {N1: X, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: GND, Nn: s4}
]
extrainfo:This circuit is a simplified equivalent of a two-stage op-amp compensation method. It includes NMOS and PMOS transistors, capacitors for compensation, resistors, and current sources. The circuit aims to stabilize and control the frequency response of the op-amp.

Figure 10.46 (a) Alternative method of compensating two-stage op amps; (b) simplified equivalent circuit of (a).

## 10.8 - Nyquist's Stability Criterion ${ }^{8}$

### 10.8.1 Motivation

Our analysis of stability in negative-feedback systems has drawn upon Bode's view of the loop transmission, namely, the magnitude and phase plots as a function of frequency, but only for $s=j \omega$. To understand the shortcomings of this approach. let us consider the loop transmission plots shown in Fig. 10.47, where $\beta=1$ and $|H|$ is equal to 3 at the phase crossover frequency, $\omega_{0}$. Our previous studies suggest that such a feedback system is unstable because it has a negative phase margin. However, if we write the closed-loop transfer function as $Y / X=H(s) /[1+H(s)]$ and assume that $s=j \omega_{0}$, then we have

$$
\begin{align*}
\frac{Y}{X}\left(j \omega_{0}\right) & =\frac{-3}{1-3}  \tag{10.52}\\
& =\frac{3}{2} \tag{10.53}
\end{align*}
$$

image_name:Figure 10.47 Unstable system Bode plots
description:The graph in Figure 10.47 is a Bode plot, which consists of two separate plots: a magnitude plot and a phase plot, both against frequency on a logarithmic scale.

1. **Magnitude Plot (Top):**
- **Axes:** The vertical axis represents the magnitude of the transfer function |H(ω)| in logarithmic scale, while the horizontal axis represents the frequency (ω) also in logarithmic scale.
- **Behavior:** The magnitude starts at a constant level of 3 (in dB) at low frequencies. As the frequency increases, the magnitude remains constant until it reaches the phase crossover frequency, ω₀, at which the magnitude is still 3. Beyond ω₀, the magnitude begins to decrease, indicating a roll-off. This decrease continues past another frequency, ωᵤ, where the magnitude is below 1.

2. **Phase Plot (Bottom):**
- **Axes:** The vertical axis represents the phase angle θ in degrees, while the horizontal axis is the same logarithmic frequency scale as the magnitude plot.
- **Behavior:** The phase starts at 0 degrees and remains constant over a range of frequencies. As frequency increases towards ω₀, the phase begins to drop, reaching -180 degrees. This indicates a phase crossover point at ω₀, where the phase margin is negative. The phase continues to decrease beyond ω₀, showing further phase lag.

3. **Key Features:**
- **Phase Crossover Frequency (ω₀):** At this frequency, the magnitude is 3, and the phase is -180 degrees, indicating a critical point where the system may become unstable.
- **Unity Gain Frequency (ωᵤ):** This is the frequency where the magnitude crosses 1, and the phase is less than -180 degrees, reinforcing the system's instability at this point.

4. **Annotations:**
- The plot includes dashed lines at the magnitude of 3 and 1, marking critical gain levels. Vertical dashed lines indicate ω₀ and ωᵤ, highlighting key frequencies where significant changes in magnitude and phase occur.

Overall, the Bode plot illustrates an unstable feedback system due to the negative phase margin at the phase crossover frequency, ω₀, and further instability at the unity gain frequency, ωᵤ.

Since the closed-loop gain is less than infinity at $\omega_{0}$, the circuit cannot oscillate at this frequency. In fact, for no value of $s=j \omega$ in Fig. 10.47 can we find the condition $Y / X=\infty$. For example, at $\omega_{u}$, we have $Y / X=\exp (j \theta) /[1+\exp (j \theta)]<\infty$ if $\theta \neq x \times 180^{\circ}$.

Should we conclude that this system does not oscillate?! This difficulty arises because Bode plots confine $s$ to imaginary values, i.e., they predict the behavior with only simple sinusoids. Indeed, this study shows that no simple sinusoid can circulate around the loop indefinitely. This, however, does not preclude other unstable waveforms. For example, suppose $s$ is equal to $\sigma_{1}+j \omega_{1}$ with $\sigma_{1}>0$, representing a growing sinusoid. It is possible that in the system of Fig. 10.47, $H\left(s=\sigma_{1}+j \omega_{1}\right)=-1$; that is, $Y / X$ goes to infinity for a growing sinusoid, allowing such a waveform to survive. Whether or not $s=\sigma_{1}+j \omega_{1}$ exists is predicted by Nyquist's theorem but not by Bode plots.

We can exploit Nyquist's stability analysis, for it provides greater insight and, more important, tackles complex circuits more clearly. For a loop transmission $\beta H(s)$, this analysis predicts how many zeros $1+\beta H(s)$ has in the right half plane (RHP) or on the $j \omega$ axis. If it has none, then the closed-loop system is stable.

Nyquist's method, however, is less intuitive and demands additional background in complex number theory. The reader should study this section patiently. We remind the reader that the poles and zeros of a transfer function can be shown on the complex $s$ plane (Fig. 10.48).
image_name:Figure 10.48
description:Figure 10.48 displays a complex s-plane diagram, which is used to represent the poles and zeros of a transfer function. The axes are labeled with \( \sigma \) for the real part (horizontal axis) and \( j\omega \) for the imaginary part (vertical axis). This setup is typical for analyzing system stability in control theory.

In the diagram:
- **Poles** are represented by 'X' marks. There are three poles visible:
- One pole is located on the negative real axis.
- Two poles are located in the left half of the plane, indicating a stable system as none are in the right half.
- **Zeros** are represented by 'O' marks. There are three zeros visible:
- One zero is on the real axis.
- Two zeros are in the right half of the plane.

The presence of poles and zeros in specific regions of the s-plane is crucial for determining the stability and response characteristics of a system. In this case, the system appears to be stable since all poles are in the left half of the s-plane, indicating no right half-plane poles which would suggest instability. The zeros do not affect stability directly but influence the system's frequency response and transient behavior.

### 10.8.2 Basic Concepts

Bode's approach to stability analysis plots the magnitude and phase of the loop gain versus frequency in Cartesian coordinates. We can also plot these two parameters in polar coordinates, in which every point is defined by an angle, $\theta$, and a radius, $r$, rather than by $x$ and $y$ [Fig. 10.49(a)]. As the frequency varies, so do $\angle H$ and $|H|$, creating a "contour" in these coordinates [Fig. 10.49(b)]. The horizontal and vertical axes in Fig. 10.49(a) also carry a meaning: the projections of the vector on the two are expressed as
image_name:Figure 10.49 (a)
description:Figure 10.49 (a) is a polar plot representing a single value of the function $H(s)$ in terms of its magnitude and phase. In this type of graph, each point is defined by a radius, $r$, which corresponds to the magnitude $|H|$, and an angle, $\theta$, which corresponds to the phase $\angle H$. Unlike Cartesian coordinates, which use $x$ and $y$ axes, polar coordinates use the radial distance from the origin and the angle from a reference direction.

**Axes Labels and Units:**
- The radial axis represents the magnitude $|H|$ of the function.
- The angular axis represents the phase $\angle H$.
- The units are not explicitly provided, but typically, magnitude is unitless or in decibels (dB), and phase is in degrees or radians.

**Overall Behavior and Trends:**
- The graph shows a single vector from the origin, indicating one specific value of $H(s)$.
- As the frequency changes, this single point would trace a path, forming a contour as illustrated in Figure 10.49(b).

**Key Features and Technical Details:**
- The vector's projection on the horizontal axis represents the real part of $H$, $|H| \cos(\angle H)$.
- The projection on the vertical axis represents the imaginary part, $|H| \sin(\angle H)$.
- These projections can be used to convert polar coordinates to Cartesian coordinates, denoted as $\operatorname{Re}\{H\}$ and $\operatorname{Im}\{H\}$.

**Annotations and Specific Data Points:**
- There are no specific numerical values given for the magnitude or phase in this description.
- The graph's purpose is to visualize the relationship between magnitude and phase at a particular frequency, emphasizing the polar representation of complex numbers.
image_name:Figure 10.49 (b)
description:The graph in Figure 10.49(b) is a Nyquist plot, which represents the contour of $H(s)$ as the frequency varies. This type of graph is used to analyze the stability of control systems and is plotted in polar coordinates, where each point is defined by an angle $\theta$ and a radius $r$.

Axes Labels and Units:
- **Horizontal Axis:** Represents the real part of the function, denoted as $\operatorname{Re}\{H\}$.
- **Vertical Axis:** Represents the imaginary part of the function, denoted as $\operatorname{Im}\{H\}$.
- The scales on both axes are typically linear, and the units depend on the specific system being analyzed.

Overall Behavior and Trends:
- The graph shows a contour that represents how the loop gain $H(s)$ changes as the frequency varies.
- The contour typically starts from a point on the real axis at lower frequencies and moves in a path that may encircle or approach the critical point (-1,0) in the complex plane.
- The shape of the contour can vary significantly depending on the system parameters, showing characteristics like loops or spirals.

Key Features and Technical Details:
- Important features include the encirclement of the critical point, which is related to the stability of the system.
- The contour may have loops or crossings, indicating resonant frequencies or phase shifts.
- The distance from the origin at any point represents the magnitude of $H(s)$ at that frequency.
- The angle from the positive real axis represents the phase angle $\angle H$.

Annotations and Specific Data Points:
- The graph may include annotations such as arrows indicating the direction of increasing frequency.
- Critical points like the -1 point may be marked to assess stability using the Nyquist criterion.
- Specific frequency values or gain levels might be annotated along the contour, though not visible in the description provided.

Figure 10.49 (a) One value of $H(s)$ shown in polar coordinates, and (b) contour of $H(s)$ as the frequency varies.
$|H| \cos (\angle H)$ and $|H| \sin (\angle H)$, respectively, with the former being the real part of $H$ and the latter, the imaginary part. We thus denote the two axes by $\operatorname{Re}\{H\}$ and $\operatorname{Im}\{H\}$, respectively. We call the polar plot of $H(s)$ the " $H$ contour." We initially assume that $s=j \omega$, but later allow it to become complex.

As an example, let us plot $H(s)=A_{0} /\left(1+s / \omega_{p}\right)$ in polar coordinates if $s$ is replaced with $j \omega$ and $\omega$ varies from 0 to $+\infty$. The phase, $-\tan ^{-1}\left(\omega / \omega_{p}\right)$, begins at zero and approaches $-90^{\circ}$ while the magnitude, $A_{0} / \sqrt{1+\omega^{2} / \omega_{p}^{2}}$, varies from $A_{0}$ to zero. Figure 10.50 sketches both the Bode plots and the polar plot, highlighting the corresponding points at $\omega=0(M)$ and $\omega=\infty(N)$. The reader may wonder how we know that the polar plot is a semicircle. It is possible to prove this by calculating $\operatorname{Im}\{H\}$ and $\operatorname{Re}\{H\}$, but, as seen later, we do not have any interest in the actual shape. The beauty of Nyquist's method is that it primarily considers $\omega=0$ and $\omega= \pm \infty$, avoiding the need for lengthy algebra.

image_name:Bode plot magnitude
description:The image contains three plots related to the function \( H(s) \) as \( s = j\omega \) varies from zero to infinity. These plots include two Bode plots and one polar plot.

1. **Bode Plot - Magnitude**:
- **Type of Graph**: Bode plot showing the magnitude of the transfer function \( |H(\omega)| \).
- **Axes Labels and Units**:
- The vertical axis represents the magnitude \( |H(\omega)| \), starting from a value \( A_0 \) and decreasing to 0.
- The horizontal axis represents the frequency \( \omega \), ranging from 0 to infinity.
- **Overall Behavior and Trends**:
- The plot starts at the point \( (A_0, M) \) for \( \omega = 0 \) and decreases monotonically towards the point \( (0, N) \) as \( \omega \) approaches infinity.
- **Key Features and Technical Details**:
- The plot shows a smooth, continuous decrease in magnitude, indicating a low-pass filter characteristic.

2. **Bode Plot - Phase**:
- **Type of Graph**: Bode plot showing the phase angle \( \angle H(\omega) \).
- **Axes Labels and Units**:
- The vertical axis represents the phase angle \( \angle H(\omega) \) in degrees, starting from 0 and approaching \(-90^\circ\).
- The horizontal axis represents the frequency \( \omega \), ranging from 0 to infinity.
- **Overall Behavior and Trends**:
- The phase angle starts at 0 degrees at \( \omega = 0 \) and decreases towards \(-90^\circ\) as \( \omega \) approaches infinity.
- **Key Features and Technical Details**:
- The plot indicates a phase shift characteristic of a first-order system.

3. **Polar Plot**:
- **Type of Graph**: Polar plot of the transfer function \( H(s) \).
- **Axes Labels and Units**:
- The vertical axis represents the imaginary part \( \operatorname{Im}\{H\} \).
- The horizontal axis represents the real part \( \operatorname{Re}\{H\} \).
- **Overall Behavior and Trends**:
- The polar plot forms a semicircle starting from point \( (A_0, 0) \) at \( \omega = 0 \) and ending at the origin \( (0, N) \) as \( \omega \) approaches infinity.
- **Key Features and Technical Details**:
- The contour travels below the horizontal axis, reflecting the negative phase angle, and approaches the origin at an angle of \(-90^\circ\). This semicircular shape is typical for systems with a simple pole at the origin.

Figure 10.50 Bode and polar plots of $H$ as $s=j \omega$ goes from zero to infinity.
This simple example readily demonstrates various decisions that we must make while plotting the $H$ contour: (1) the contour begins at $\left(A_{0}, 0\right)$ for $\omega=0$ and travels to the left because it must eventually reach the origin for $\omega=\infty$; (2) the contour falls below the horizontal axis because $\angle H$ is negative; and (3) the contour approaches the origin at an angle of $-90^{\circ}$.

Since calculating $|H|$ and $\angle H$ is generally cumbersome, we wish to construct polar plots by considering only the poles and zeros of the transfer function. To understand the objective, consider the complex $s$ plane for the above example, where the pole is real and equal to $-\omega_{p}$ (Fig. 10.51). As $\omega$ goes from 0 to $+\infty$, we begin at the origin and travel upward on the $j \omega$ axis. ${ }^{9}$ Can we construct the polar plot of $H$ by examining what happens in the $s$ plane?

Let us first see whether $\angle H$ can be directly computed in the $s$ plane. To this end, we consider one value for $s$ and denote it by $s_{1}=\sigma_{1}+j \omega_{1}$, a complex value. Shown in Fig. 10.52 for a one-pole system,

image_name:Figure 10.51 The $s$ plane with one pole.
description:The graph in Figure 10.51 is a representation of the $s$ plane, which is commonly used in control systems and signal processing to analyze complex functions. This particular graph illustrates a one-pole system. The axes are labeled with $\sigma$ on the horizontal axis, representing the real part of the complex frequency, and $j\omega$ on the vertical axis, representing the imaginary part.

The graph features a pole located at $-\omega_{p}$ on the $\sigma$ axis, shown as a cross (×). This indicates that the system has a single real pole at this position. The pole is a critical point in determining the behavior of the system's transfer function $H(s)$.

A dotted line extends from the pole at $-\omega_{p}$ to a point on the positive $j\omega$ axis, representing a specific complex frequency $s_1 = \sigma_1 + j\omega_1$. This line suggests the calculation of the phase angle $\angle H(s_1)$, which is the angle between the real axis and the line connecting the pole to the point on the $j\omega$ axis.

An arrow on the $j\omega$ axis indicates the direction of increasing frequency, suggesting that as $\omega$ increases from 0 to $+\infty$, the system's response can be tracked along the imaginary axis. This is typical in analyzing how the system behaves at various frequencies, particularly in the context of frequency response analysis.

Overall, the graph provides a visual representation of the pole's influence on the phase of the transfer function $H(s)$, indicating how the phase shift is affected by the position of the pole in the $s$ plane.

image_name:Figure 10.52 Phase shift produced by a pole at frequency $s_{1}$.
description:The graph in Figure 10.52 is a representation of the $s$ plane, which is used in control theory and signal processing to analyze the behavior of systems in the frequency domain. The $s$ plane is a complex plane with the real part ($\sigma$) on the horizontal axis and the imaginary part ($j\omega$) on the vertical axis.

Axes Labels and Units:
- **Horizontal Axis ($\sigma$):** Represents the real part of the complex frequency, typically in radians per second.
- **Vertical Axis ($j\omega$):** Represents the imaginary part of the complex frequency, also in radians per second.

Overall Behavior and Trends:
- The graph illustrates the position of a single pole in the $s$ plane, marked by an 'X' at $-\omega_p$ on the real axis.
- A point $s_1$ is shown in the first quadrant, indicating a specific frequency point with real part $\sigma_1$ and imaginary part $j\omega_1$.
- A dashed line connects the pole $-\omega_p$ to the point $s_1$, forming an angle $\theta$ with the negative real axis. This angle represents the phase angle of the transfer function $H(s)$ at $s_1$.

Key Features and Technical Details:
- The pole at $-\omega_p$ is a crucial element, affecting the system's stability and frequency response.
- The angle $\theta$ is calculated as $-\tan^{-1} \frac{\omega_1}{\sigma_1 + \omega_p}$, representing the phase shift introduced by the pole at the frequency $s_1$.
- The distance along the real axis from the origin to $s_1$ is $\sigma_1$, and the total distance from the pole at $-\omega_p$ to $s_1$ is $\sigma_1 + \omega_p$.

Annotations and Specific Data Points:
- The graph includes a reference line from the pole to the point $s_1$, emphasizing the geometric interpretation of the phase shift.
- The angle $\theta$ is annotated on the graph, illustrating the phase influence of the pole.

This graph is essential for understanding how poles in the $s$ plane influence the phase of a system's transfer function, particularly in frequency response analysis.

the $s$ plane can yield a value for $\angle H\left(s=s_{1}\right)$. Since

$$
\begin{align*}
H\left(s_{1}\right) & =\frac{A_{0}}{1+\frac{\sigma_{1}+j \omega_{1}}{\omega_{p}}}  \tag{10.54}\\
& =\frac{A_{0} \omega_{p}}{\sigma_{1}+\omega_{p}+j \omega_{1}} \tag{10.55}
\end{align*}
$$

we have

$$
\begin{equation*}
\angle H\left(s_{1}\right)=-\tan ^{-1} \frac{\omega_{1}}{\sigma_{1}+\omega_{p}} \tag{10.56}
\end{equation*}
$$

Thus, the angle $\theta$ in Fig. 10.52 is equal to $-\angle H\left(s_{1}\right)$. That is, to determine $\angle H\left(s_{1}\right)$ in the $s$ plane, we draw a vector from the pole to $s_{1}$, measure the angle of this vector with respect to the positive $\sigma$ axis, and multiply the result by -1 . For the phase contributed by a zero, the procedure is the same, except that the result is not multiplied by -1 . If $H$ contains multiple poles and zeros, then their phase contributions simply add algebraically.

It is possible to calculate $|H|$ from the $s$ plane as well, ${ }^{10}$ but, fortunately, the exact knowledge of $|H|$ is not necessary in Nyquist's approach.

### 10.8.3 Construction of Polar Plots

In this section, we study examples of plotting $H(s)$ in polar coordinates so as to prepare ourselves for Nyquist's stability criterion.

General First-Order System Suppose $H(s)=A_{0}\left(1+s / \omega_{z}\right) /\left(1+s / \omega_{p}\right)$ and $\omega_{p}>\omega_{z}$. We first plot $H$ for $s=j \omega$ as $\omega$ varies from 0 to $+\infty$. At $\omega=0,|H(s)|=A_{0}$. Also, as shown in Fig. 10.53(a), the vectors going from the pole and the zero to $s=0$ contribute equal and opposite angles, yielding

image_name:(a)
description:The graph labeled as "(a)" in Figure 10.53 is a polar plot representing the phase shifts contributed by a pole and a zero at the origin in the s-plane. This plot is part of a study on the Nyquist stability criterion for a general first-order system described by the transfer function \( H(s) = A_{0}\frac{1+s/\omega_{z}}{1+s/\omega_{p}} \) where \( \omega_{p} > \omega_{z} \).

1. **Type of Graph and Function:**
- The graph is a polar plot depicting the contributions of poles and zeros to the phase of the transfer function \( H(s) \) at \( s = 0 \).

2. **Axes Labels and Units:**
- The horizontal axis represents the real part of \( s \) (\( \sigma \)) and the vertical axis represents the imaginary part (\( j\omega \)).
- Units are in terms of frequency, typically radians per second.

3. **Overall Behavior and Trends:**
- At \( s = 0 \), the vectors from the pole at \( -\omega_{p} \) and the zero at \( -\omega_{z} \) point towards the origin.
- These vectors contribute equal and opposite phase angles to \( H(s) \), resulting in a net phase angle of zero at \( s = 0 \).

4. **Key Features and Technical Details:**
- The pole is located at \( -\omega_{p} \) on the real axis, and the zero is located at \( -\omega_{z} \).
- The system's gain at \( s = 0 \) is \( |H(0)| = A_{0} \).
- The equal and opposite phase contributions from the pole and zero ensure that the initial phase angle \( \angle H(0) \) is zero.

5. **Annotations and Specific Data Points:**
- The graph includes markers for the pole and zero locations, represented by an 'X' and an 'O', respectively.
- The vectors are drawn from these points to the origin, indicating the direction of phase contribution.
image_name:(b)
description:The graph labeled (b) represents a polar plot of the transfer function $H(s)$ for a general first-order system, specifically at the point $s = j\omega_1$. The axes are marked as $\sigma$ (real part) and $j\omega$ (imaginary part) in the complex plane, with the zero and pole locations indicated on the real axis as $-\omega_z$ and $-\omega_p$, respectively.

Type of Graph and Function:
This is a polar plot showing the phase relationship between the zero and pole at a specific frequency in the complex plane.

Axes Labels and Units:
- **Horizontal Axis ($\sigma$):** Represents the real part of the complex frequency $s$.
- **Vertical Axis ($j\omega$):** Represents the imaginary part of the complex frequency $s$.
- Units are in terms of frequency, though not explicitly labeled in standard units.

Overall Behavior and Trends:
- The plot shows vectors originating from the zero and the pole extending to the point $s = j\omega_1$.
- The angle $\theta_z$ contributed by the zero is greater than the angle $\theta_p$ contributed by the pole, indicating a net positive phase shift at this frequency.

Key Features and Technical Details:
- **Zero Location ($-\omega_z$):** The point on the real axis from which the zero vector originates.
- **Pole Location ($-\omega_p$):** The point on the real axis from which the pole vector originates.
- **Phase Angles:** $\theta_z$ and $\theta_p$ are the angles from the zero and pole to the point $s = j\omega_1$, showing the phase contribution of each.

Annotations and Specific Data Points:
- The vectors and angles are annotated to show the phase relationship at $s = j\omega_1$, with $\theta_z > \theta_p$.
- This plot is a part of a sequence illustrating how the phase of $H(s)$ changes as the frequency varies from $0$ to $+\infty$.
image_name:(c)
description:The graph labeled "(c)" is a polar plot illustrating the contour of the transfer function $H(s)$ as the complex frequency $s$ moves from $0$ to $j\omega_1$. This is part of an analysis for a general first-order system with a transfer function $H(s) = A_0 (1 + s/\omega_z) / (1 + s/\omega_p)$, where $\omega_p > \omega_z$.

1. **Type of Graph and Function**: This is a polar plot, which is used to depict the magnitude and phase of a complex function as the frequency varies.

2. **Axes Labels and Units**: The horizontal axis represents the real part of $H(s)$, denoted as $\text{Re}\{H\}$, and the vertical axis represents the imaginary part, denoted as $\text{Im}\{H\}$. There are no units specified, as this is a normalized plot.

3. **Overall Behavior and Trends**: The plot shows the path of the complex function $H(s)$ from $s = 0$ to $s = j\omega_1$. The path starts at the point $A_0$ on the real axis and extends upwards in a curved trajectory. The curve indicates a change in both magnitude and phase of $H(s)$ as $\omega$ increases from $0$ to $\omega_1$.

4. **Key Features and Technical Details**:
- The curve represents the vector sum of contributions from a zero and a pole.
- At $s = 0$, the angle $\theta_z$ contributed by the zero and $\theta_p$ by the pole are equal and opposite, resulting in an initial angle of $0$.
- As $s$ moves to $j\omega_1$, the angle $\theta_z$ becomes greater than $\theta_p$, indicating a net phase shift.
- The magnitude $|H(j\omega)|$ is shown as increasing from $A_0$.
- The angle $\theta_z - \theta_p$ is depicted, highlighting the phase difference.

5. **Annotations and Specific Data Points**: The graph is annotated with the initial point $A_0$ and the direction of the contour as $s$ moves from $0$ to $j\omega_1$. The angles $\theta_z$ and $\theta_p$ are marked to indicate their contributions to the phase shift.
image_name:(d)
description:The graph labeled (d) in Figure 10.53 is a polar plot representing the phase shifts contributed by a pole and a zero at infinity for the transfer function $H(s) = A_{0}(1+s/\omega_{z})/(1+s/\omega_{p})$. The plot is shown in the complex plane with the horizontal axis labeled as $\sigma$ (real part) and the vertical axis labeled as $j\omega$ (imaginary part). The point $s = j\infty$ is depicted as the endpoint of a vector originating from the origin.

In this graph, the angles $\theta_{p}$ and $\theta_{z}$ are illustrated with dashed lines, representing the angles from the pole and the zero to the point $s = j\infty$. The zero is located at $-\omega_{z}$, and the pole is located at $-\omega_{p}$ on the real axis. The angle $\theta_{z}$ is greater than $\theta_{p}$, indicating a larger phase shift contribution from the zero compared to the pole as $s$ approaches $j\infty$. This results in a net positive phase shift as the frequency increases towards infinity.

Overall, the graph illustrates the behavior of the transfer function $H(s)$ in the frequency domain, showing how the phase shifts evolve as the frequency moves towards infinity. This polar plot is crucial for understanding the stability characteristics of the system when applying Nyquist's stability criterion.
image_name:(e)
description:The graph labeled (e) is a polar plot of the transfer function $H(s)$ for a general first-order system, where $H(s) = A_{0}(1 + s/\omega_z) / (1 + s/\omega_p)$ and $\omega_p > \omega_z$. This plot is used to visualize the contour of $H(s)$ as the frequency $\omega$ varies from 0 to $+\infty$.

1. **Type of Graph and Function:**
- This is a Nyquist plot, which is a polar plot used in control theory to assess the stability of a system.

2. **Axes Labels and Units:**
- The horizontal axis represents the real part of $H(s)$, denoted as $\text{Re}\{H\}$.
- The vertical axis represents the imaginary part of $H(s)$, denoted as $\text{Im}\{H\}$.
- Units are not explicitly labeled but are typically dimensionless in such plots.

3. **Overall Behavior and Trends:**
- The plot starts at $s = 0$ with a real value of $A_0$ on the real axis.
- As $s$ moves towards $j\infty$, the contour follows a semicircular path above the real axis.
- The contour returns to the real axis at $s = +j\infty$ with a value of $A_0 \omega_p / \omega_z$.

4. **Key Features and Technical Details:**
- The plot indicates a phase shift as the frequency increases from 0 to $+\infty$.
- The contour is a semicircle, indicating a change in phase from 0 to $\pi$ radians.
- No specific numerical values are annotated on this plot.

5. **Annotations and Specific Data Points:**
- The start point on the real axis is marked as $A_0$.
- The endpoint on the real axis is marked as $A_0 \omega_p / \omega_z$.
- The path of the contour is marked with arrows indicating the direction from $s = 0$ to $s = +j\infty$.

This plot is crucial in analyzing the stability of a control system using Nyquist's stability criterion, as it visually represents the frequency response of the system.
image_name:(f)
description:The graph labeled (f) is a Bode plot, which is used to represent the frequency response of the system described by the transfer function \( H(s) = A_{0}\left(1+s / \omega_{z}\right) /\left(1+s / \omega_{p}\right) \). This plot consists of two separate plots: the magnitude plot and the phase plot.

1. **Magnitude Plot:**
- **Type:** Logarithmic scale.
- **Axes:** The horizontal axis represents the frequency \( \omega \) in a logarithmic scale, while the vertical axis represents the magnitude \( |H(\omega)| \) in decibels (dB).
- **Behavior:** The magnitude starts at \( A_0 \) when \( \omega = 0 \). As the frequency increases, there is a noticeable rise in magnitude around the zero frequency \( \omega_z \), and it continues to increase until reaching a plateau or leveling off beyond the pole frequency \( \omega_p \).
- **Key Features:** The transition points at \( \omega_z \) and \( \omega_p \) are marked with dashed vertical lines, indicating significant changes in the slope of the magnitude curve.

2. **Phase Plot:**
- **Type:** Linear scale.
- **Axes:** The horizontal axis represents the frequency \( \omega \) in a logarithmic scale, while the vertical axis shows the phase \( \angle H(\omega) \) in degrees.
- **Behavior:** The phase plot starts at 0 degrees at \( \omega = 0 \). As frequency increases, the phase increases, reaches a peak, and then returns towards zero as it approaches higher frequencies.
- **Key Features:** The phase shift is most significant between \( \omega_z \) and \( \omega_p \), where the curve shows a peak, indicating the maximum phase contribution of the zero and pole.

Overall, this Bode plot illustrates the frequency response of a first-order system, showing how the magnitude and phase of the system's output vary with frequency. The plot highlights the impact of the zero and pole on the system's behavior across different frequencies, providing insights into the system's stability and performance.
image_name:(g)
description:The graph labeled (g) is a Nyquist plot for the transfer function \( H(s) = A_{0}\left(1+s / \omega_{z}\right) /\left(1+s / \omega_{p}\right) \), where \( \omega_{p} > \omega_{z} \). This plot is used to analyze the stability of the system by mapping the frequency response of the system in the complex plane as \( s = j\omega \) varies from \( 0 \) to \( +j\infty \) and from \( 0 \) to \(-j\infty \).

1. Type of Graph and Function:
This is a Nyquist diagram, which represents the frequency response of a system in the complex plane.

2. Axes Labels and Units:
- **Real Axis (Re{H}):** Represents the real part of the frequency response.
- **Imaginary Axis (Im{H}):** Represents the imaginary part of the frequency response.
- No specific units are labeled, as this is a dimensionless plot.

3. Overall Behavior and Trends:
- The plot forms a closed loop in the complex plane.
- As \( \omega \) increases from 0 to \(+\infty\), the plot starts at \( A_0 \) on the real axis, moves counterclockwise, and completes a loop.
- The contour is symmetric about the real axis, indicating that the system is stable if the loop does not encircle the critical point (-1,0).

4. Key Features and Technical Details:
- **Starting Point:** \( A_0 \) on the real axis.
- **Ending Point:** The loop returns to \( A_0 \) on the real axis.
- **Critical Points:** The loop passes through key points determined by \( \omega_z \) and \( \omega_p \).
- **Symmetry:** The plot is symmetric about the real axis, a typical feature of systems with conjugate poles and zeros.

5. Annotations and Specific Data Points:
- The arrows indicate the direction of increasing frequency \( \omega \).
- The loop crosses the real axis at \( A_0 \) and \( A_0 \omega_p / \omega_z \), showing the gain at these frequencies.
- No explicit annotations for specific frequencies, but the symmetry and shape provide insights into system stability.

This Nyquist plot helps in assessing the stability of the control system by visually inspecting the encirclement of the critical point (-1,0) in the complex plane.

Figure 10.53 (a) Phase shifts contributed by a pole and a zero at $s=0$, (b) phase shifts at $s=j \omega_{1}$, (c) contour of $H$ as $s$ goes from zero to $j \omega_{1}$, (d) phase shifts as $s \rightarrow j \infty$, (e) correct contour of $H$, (f) corresponding Bode plots, and ( g ) complete $H$ contour.
$\angle H(0)=0$. Now, if $s$ rises to $j \omega_{1}$ [Fig. 10.53(b)], the angle contributed by the zero, $\theta_{z}$, is greater than that contributed by the pole, $\theta_{p}$. That is, $\angle H=\theta_{z}-\theta_{p}$ remains positive. We have thus far constructed the $H$ contour shown in Fig. 10.53(c). The reader may wonder whether $\left|H\left(j \omega_{1}\right)\right|$ is greater or less than $A_{0}$, but we do not concern ourselves at this point.

What happens as $s$ goes toward $+j \infty$ ? As depicted in Fig. 10.53(d), the angles arising from the zero and the pole approach $90^{\circ}$, producing a net value of 0 for $\angle H$. The magnitude of $H$, on the other hand, approaches $A_{0} \omega_{p} / \omega_{z}>A_{0}$. This means that the $H$ contour returns to the $\sigma$ axis, but at a more positive real value. Our guess in Fig. 10.53(c) is therefore not quite correct and must be revised to that in Fig. 10.53(e). For completeness, we also show the Bode plots in Fig. 10.53(f).

It is necessary to repeat this procedure as $s=j \omega$ goes from 0 to $-j \infty$. Since the $s$ plane contents are always symmetric with respect to the $\sigma$ axis for a physical system (due to conjugate symmetry of the poles and zeros), the polar plot is also symmetric, emerging as shown in Fig. 10.53(g).

What if $\omega_{p}<\omega_{z}$ ? As shown in Fig. 10.54(a), the net angle is now negative as $s$ travels upward on the $j \omega$ axis. Moreover, since $|H(j \omega=0)|=A_{0}$ and $|H(j \omega=+j \infty)|=A_{0} \omega_{p} / \omega_{z}<A_{0}$, the $H$ contour begins from $A_{0}$ on the real axis, rotates downward, and shrinks in magnitude [Fig. 10.54(b)]. For $s=0$ to $-j \infty$, this plot is reflected around the real axis in a manner similar to that in Fig. 10.53(g). The Bode plots are also constructed in Fig. 10.54(c) to highlight the correspondences.

We have mostly confined the $s$ values in $H(s)$ to the $j \omega$ axis. In general, however, $s$ can travel on an arbitrary path (contour) in the $s$ plane, assuming complex, real, or imaginary values. It is therefore beneficial to consider the behavior of the foregoing first-order system in such a case. For example, suppose $s$ travels clockwise on a closed contour in the right half plane [Fig. 10.55(a)]. How does $H(s)=A_{0}\left(1+s / \omega_{z}\right) /\left(1+s / \omega_{p}\right)$ behave if $\omega_{p}>\omega_{z}$ ? At point $M, s$ is real and equal to $\sigma_{M}$, yielding
image_name:(a)
description:The diagram labeled (a) is a Nyquist plot illustrating the trajectory of a complex variable \( s \) in the \( s \)-plane. The plot is set in the context of analyzing the behavior of a transfer function \( H(s) = A_{0}\left(1+s / \omega_{z}\right) /\left(1+s / \omega_{p}\right) \) when \( \omega_{p} > \omega_{z} \).

1. **Type of Graph and Function**:
- This is a Nyquist plot, which is typically used to assess the stability of a control system by plotting the frequency response of a system's open-loop transfer function.

2. **Axes Labels and Units**:
- The horizontal axis represents the real part of \( s \) (\( \sigma \)), while the vertical axis represents the imaginary part (\( j\omega \)).
- The plot does not explicitly label units, but the axes are standard for a Nyquist plot.

3. **Overall Behavior and Trends**:
- The contour in the \( s \)-plane moves from \( s = j\omega_1 \) upwards, indicating a path through the imaginary axis.
- The contour excludes the pole at \( -\omega_{p} \) and the zero at \( -\omega_{z} \), as indicated by the open circle and cross on the real axis.

4. **Key Features and Technical Details**:
- The plot shows the trajectory moving clockwise, which is typical in a Nyquist plot to indicate increasing frequency.
- The contour avoids the pole and zero, which is crucial for maintaining system stability.
- The diagram suggests a focus on the right half-plane, relevant for stability analysis when \( \omega_{p} > \omega_{z} \).

5. **Annotations and Specific Data Points**:
- The point \( s = j\omega_1 \) is marked, indicating a specific frequency point on the imaginary axis.
- The diagram does not provide specific numerical values for \( \omega_{p} \) and \( \omega_{z} \), but these are critical in the context of the transfer function's behavior.

Overall, this Nyquist plot is used to visualize how the system's transfer function \( H(s) \) behaves as \( s \) traverses a contour in the \( s \)-plane, specifically avoiding the pole and zero, which is significant in analyzing the stability of control systems.
image_name:(b)
description:The graph labeled (b) is a Nyquist diagram that represents the contour of the transfer function \( H(s) = A_{0}\left(1+s / \omega_{z}\right) /\left(1+s / \omega_{p}\right) \) in the complex plane. The axes are labeled as \( \text{Re}\{H\} \) and \( \text{Im}\{H\} \), representing the real and imaginary parts of the transfer function, respectively.

Axes Labels and Units:
- **Horizontal Axis (\( \text{Re}\{H\} \))**: Represents the real part of the transfer function.
- **Vertical Axis (\( \text{Im}\{H\} \))**: Represents the imaginary part of the transfer function.

Overall Behavior and Trends:
- The graph shows a semicircular path in the complex plane.
- The contour starts at \( s = 0 \) on the real axis at a value of \( A_0 \), moves towards \( s = +j\infty \) along a semicircular path, and returns back to the real axis.
- The path indicates that as \( s \) travels along the contour, the transfer function \( H(s) \) follows this semicircular trajectory.

Key Features and Technical Details:
- **Starting Point (\( s = 0 \))**: The contour begins at \( A_0 \) on the real axis.
- **End Point (\( s = +j\infty \))**: The contour returns to the real axis at the same point \( A_0 \).
- **Semicircular Path**: The contour is symmetric about the real axis and passes through the point \( \omega_p/\omega_z \) on the real axis.

Annotations and Specific Data Points:
- The contour is marked with arrows indicating the direction of traversal, starting from \( s = 0 \) to \( s = +j\infty \) and back.
- The graph does not show any specific numerical values or additional annotations apart from the path and direction.
image_name:(c)
description:The graph labeled (c) consists of two separate plots: a magnitude plot and a phase plot of a transfer function \( H(s) \). Both plots are functions of frequency \( \omega \).

1. **Magnitude Plot (|H(ω)|):**
- **Type of Graph:** Bode magnitude plot.
- **Axes Labels and Units:**
- The horizontal axis represents frequency \( \omega \), typically in radians per second.
- The vertical axis represents the magnitude \( |H(\omega)| \), which is dimensionless.
- **Overall Behavior and Trends:**
- The plot starts at a constant magnitude \( A_0 \) at low frequencies.
- There is a noticeable drop in magnitude at two specific frequencies: \( \omega_p \) and \( \omega_z \).
- After \( \omega_z \), the magnitude levels off at a lower value.
- **Key Features and Technical Details:**
- The transitions at \( \omega_p \) and \( \omega_z \) are marked by vertical dashed lines, indicating critical frequencies where the behavior of the system changes.
- The magnitude decreases between \( \omega_p \) and \( \omega_z \), indicating a frequency-dependent attenuation.

2. **Phase Plot (∠H(ω))**
- **Type of Graph:** Bode phase plot.
- **Axes Labels and Units:**
- The horizontal axis represents frequency \( \omega \).
- The vertical axis represents the phase angle \( \angle H(\omega) \), typically in degrees or radians.
- **Overall Behavior and Trends:**
- The phase starts at zero and decreases, reaching a minimum between \( \omega_p \) and \( \omega_z \).
- After \( \omega_z \), the phase gradually returns towards zero.
- **Key Features and Technical Details:**
- The phase plot is a smooth curve with a dip, indicating phase lag introduced by the system.
- The critical frequencies \( \omega_p \) and \( \omega_z \) are marked with vertical dashed lines, corresponding to the points where the phase shift is more pronounced.

Overall, the graph (c) illustrates the frequency response of a system with a transfer function \( H(s) \), highlighting how the magnitude and phase shift as frequency changes, particularly around the pole \( \omega_p \) and zero \( \omega_z \).

Figure 10.54 System with $\omega_{p}<\omega_{z}$, (b) contour of $H$, and (c) corresponding Bode plots.
image_name:(a)
description:The graph labeled "(a)" is a contour plot in the complex frequency domain, representing the contour of a transfer function \( H(s) \). The axes are labeled \( \sigma \) (real part) on the horizontal axis and \( j\omega \) (imaginary part) on the vertical axis. The plot features a closed loop contour that excludes specific points, namely the pole at \( -\omega_p \) and the zero at \( -\omega_z \), which are marked on the horizontal axis.

The contour is depicted as a loop starting from a point \( M \) on the real axis at \( \sigma_M \), moving upwards and looping around, and then returning to a point \( N \) on the real axis at \( \sigma_N \). The direction of the contour is indicated by arrows, showing a counter-clockwise path.

Key features of this graph include the avoidance of the pole and zero, illustrating how the contour in the \( s \)-plane is constructed to bypass these critical points. The contour path is significant in complex analysis and control theory, often used to evaluate integrals or to apply the Argument Principle or Nyquist criterion in system stability analysis.

The graph serves as a foundational representation for further analysis of the system's behavior, particularly in understanding how the transfer function \( H(s) \) behaves as the complex frequency \( s \) varies around these critical points.
image_name:(b)
description:The graph labeled (b) is a polar plot representing possible trajectories for the transfer function \( H(s) \). The plot is part of a set of diagrams analyzing the behavior of a dynamic system characterized by its transfer function.

1. **Type of Graph and Function:**
- This is a polar plot, which is used to represent the complex values of the transfer function \( H(s) \) as the frequency changes.

2. **Axes Labels and Units:**
- The horizontal axis represents the real part of \( H(s) \), denoted as \( \text{Re}(H) \).
- The vertical axis represents the imaginary part of \( H(s) \), denoted as \( \text{Im}(H) \).
- There are no specific units marked on the axes, as this is a dimensionless representation of the complex plane.

3. **Overall Behavior and Trends:**
- The plot shows a starting point labeled \( M \) on the real axis, from which possible trajectories emanate.
- The trajectories are indicated by dashed lines and question marks, suggesting uncertainty in the path direction.
- The plot does not show a closed contour, indicating that it is illustrating potential paths rather than a specific response.

4. **Key Features and Technical Details:**
- The point \( M \) represents a specific real value of \( H \) from which the trajectory departs.
- The dashed lines imply possible directions of movement in the complex plane but do not specify a definitive path.
- The lack of a closed loop suggests exploration of potential behavior rather than a definitive contour.

5. **Annotations and Specific Data Points:**
- The graph includes a question mark near the dashed lines, indicating ambiguity or multiple possibilities in the trajectory's continuation.
- No specific numerical values are provided, as the plot is more conceptual, focusing on potential movement directions rather than exact data points.
image_name:(c)
description:The graph labeled (c) in Figure 10.55 is a contour plot of the transfer function \( H(s) \) in the complex plane, specifically illustrating the trajectory or contour of \( H \) as the complex frequency \( s \) varies. The axes are labeled as \( \text{Re}\{H\} \) for the real part and \( \text{Im}\{H\} \) for the imaginary part of the transfer function.

1. **Type of Graph and Function:**
- This is a polar plot or contour plot of the transfer function \( H(s) \) in the complex plane.

2. **Axes Labels and Units:**
- The horizontal axis represents the real part of \( H \), labeled as \( \text{Re}\{H\} \).
- The vertical axis represents the imaginary part of \( H \), labeled as \( \text{Im}\{H\} \).
- There are no specific units marked on the axes as it is a dimensionless plot of complex numbers.

3. **Overall Behavior and Trends:**
- The contour forms a closed loop, indicating the trajectory of \( H(s) \) as \( s \) traverses a specific path in the complex plane.
- The loop suggests that the system's response varies in both magnitude and phase as frequency changes.

4. **Key Features and Technical Details:**
- The contour starts at point \( M \) and ends at point \( N \), indicating the starting and ending points of the path traced by \( H(s) \).
- The direction of the contour is indicated by arrows, showing the progression from \( M \) to \( N \).
- The contour does not cross the origin, suggesting that the system does not have a zero at the origin in this configuration.

5. **Annotations and Specific Data Points:**
- Points \( M \) and \( N \) are marked on the contour, representing specific values of \( s \) where the trajectory is analyzed.
- The contour's shape and direction provide insight into the phase shift and gain changes of the system as \( s \) moves in the complex plane.

This graph is useful for understanding how the transfer function \( H(s) \) behaves over a range of frequencies, particularly in terms of phase and magnitude changes.
image_name:(d)
description:The graph labeled "(d)" is a Nyquist plot, which represents the frequency response of a system by plotting the imaginary part of the transfer function \( H(s) \) against its real part. This specific plot is used to analyze the stability and behavior of the system described by the transfer function \( H(s) = A_{0}\left(1+\sigma_{M} / \omega_{z}\right) /\left(1+\sigma_{M} / \omega_{p}\right) \).

Axes Labels and Units:
- **Horizontal Axis (Re\{H\}):** Represents the real part of the transfer function \( H(s) \).
- **Vertical Axis (Im\{H\}):** Represents the imaginary part of the transfer function \( H(s) \).
- Both axes are dimensionless as they represent normalized values of the transfer function.

Overall Behavior and Trends:
- The Nyquist plot in graph (d) shows a closed contour that encircles the origin in a clockwise direction.
- The contour begins and ends on the real axis, indicating a full cycle of frequency response from low to high frequencies.
- The plot suggests that for this specific configuration, the zero contributes more phase than the pole, leading to a net positive angle as frequency increases.

Key Features and Technical Details:
- **Critical Points:** The contour passes through points labeled \( M \) and \( N \) on the real axis, indicating significant points in the frequency response.
- **Encirclement:** The contour encircles the origin, which is a critical aspect for assessing system stability using Nyquist criteria.
- **Direction of Encirclement:** The clockwise direction of the contour is important for determining the stability margins.
- **Phase Contribution:** The configuration \( -\omega_{z} < -\omega_{p} \) implies that the zero is more dominant than the pole in phase contribution.

Annotations and Specific Data Points:
- The contour is annotated with arrows indicating the direction of the plot.
- Points \( M \) and \( N \) are marked on the real axis, representing specific values of the transfer function at certain frequencies.
- The contour shape and encirclement provide insights into the system’s stability and phase characteristics.

Figure 10.55 (a) $s$ contour excluding pole and zero, (b) possible trajectories for $H$, (c) actual $H$ contour, and (d) $H$ contour if $-\omega_{z}<-\omega_{p}$.
$H(s)=A_{0}\left(1+\sigma_{M} / \omega_{z}\right) /\left(1+\sigma_{M} / \omega_{p}\right)$, a real point in the polar plot of $H$ [Fig. 10.55(b)]. As $s$ departs from $M$, the net angle becomes more positive because the zero contributes more phase than the pole does, but we do not know whether the $H$ contour rises to the left or to the right. We therefore continue the $s$ contour to point $N$, noting that the angle returns to zero and $H(s)=A_{0}\left(1+\sigma_{N} / \omega_{z}\right) /\left(1+\sigma_{N} / \omega_{p}\right)$, which is greater than $H\left(s=\sigma_{M}\right)$ if $\omega_{p}>\omega_{z}$. Thus, the $H$ contour must rise to the right, i.e., rotate clockwise. Figure 10.55(c) depicts the complete plot as $s$ traverses clockwise the contour in the $s$ plane from $M$ to $N$ and from $N$ back to $M$. For the case of $\omega_{p}<\omega_{z}, H$ rotates counterclockwise [Fig. 10.55(d)] because $H\left(\sigma_{N}\right)<H\left(\sigma_{M}\right)$. The reader is encouraged to repeat this analysis for $H(s)=A_{0} /\left(1+s / \omega_{p}\right)$.

Let us consider another $s$ contour that encloses the pole and the zero of the transfer function. As illustrated in Fig. 10.56(a), we begin at point $M$ and observe a net angle of zero and $H\left(\sigma_{M}\right)=A_{0}(1+$ $\left.\sigma_{M} / \omega_{z}\right) /\left(1+\sigma_{M} / \omega_{p}\right)$. Since $\sigma_{M}$ is more negative than $-\omega_{z}$ and $-\omega_{p}, H\left(\sigma_{M}\right)>0$, yielding a point on
the real axis for the polar plot of $H$ [Fig. 10.56(b)]. As we travel clockwise on the $s$ contour, say to point $s_{1}$, the net angle becomes positive (why?), eventually returning to zero as we reach point $N$. Since $\sigma_{N}$ is less negative than $-\omega_{z}$ and $-\omega_{p}, H\left(\sigma_{N}\right)>0$. The reader can prove that $H\left(\sigma_{N}\right)>H\left(\sigma_{M}\right)$. If we now continue on the $s$ contour from $N$ toward $M$, the polar plot of $H$ becomes negative and returns to zero. It is important to note that the $H$ contour does not enclose the origin. We say that $H$ does not "encircle" the origin. The $s$ contours in both Figs. 10.55(a) and 10.56(a) lead to $H$ contours that do not encircle the origin. The significance of this point becomes clear later.
image_name:Figure 10.56 (a)
description:Figure 10.56 (a) is a Nyquist diagram representing the contour of a complex function $H(s)$ in the complex plane. The graph consists of two main axes: the real axis (labeled $\sigma$) and the imaginary axis (labeled $j\omega$). The plot is centered around the origin, and the contour is drawn in a closed loop.

1. **Type of Graph and Function:**
- The graph is a Nyquist plot, which is typically used in control systems to assess the stability of a system by plotting the frequency response of a transfer function.

2. **Axes Labels and Units:**
- The horizontal axis is the real part of the complex frequency, denoted as $\sigma$.
- The vertical axis is the imaginary part, denoted as $j\omega$.
- Units are not explicitly provided, as this is a normalized frequency response.

3. **Overall Behavior and Trends:**
- The contour starts at point $M$, moves towards $s_1$, and then proceeds to point $N$. It forms a loop around the origin but does not enclose it.
- The path indicates a trajectory that initially moves through negative real values and circles back to positive real values without encircling the origin.

4. **Key Features and Technical Details:**
- Points $M$ and $N$ are marked on the real axis, with $M$ located at $\sigma_M$ and $N$ at $\sigma_N$.
- The contour passes through a pole at $-\omega_p$ and a zero at $-\omega_z$.
- The contour does not enclose the origin, indicating that the function $H(s)$ does not encircle the origin.

5. **Annotations and Specific Data Points:**
- The path is annotated with arrows indicating the direction of the contour from $M$ to $N$.
- Critical points such as $s_1$, $-\omega_p$ (pole), and $-\omega_z$ (zero) are highlighted.
- The contour's trajectory suggests a change in phase but maintains a consistent gain level that does not lead to encirclement of the origin, which is significant for stability analysis.
image_name:Figure 10.56 (b)
description:**Type of Graph and Function:**
Figure 10.56 (b) is a Nyquist plot, which is used in control systems to represent the frequency response of a system. This plot typically maps the complex plane with the real part of the transfer function on the x-axis and the imaginary part on the y-axis.

**Axes Labels and Units:**
- The x-axis is labeled as \( \text{Re}\{H\} \), representing the real part of the transfer function \( H(s) \).
- The y-axis is labeled as \( \text{Im}\{H\} \), representing the imaginary part of the transfer function \( H(s) \).
- There are no specific units provided for the axes, as they represent complex numbers.

**Overall Behavior and Trends:**
The Nyquist plot in Figure 10.56 (b) shows a closed loop that does not encircle the origin. The curve starts at point \( M \), moves counterclockwise, and returns to point \( N \). The path indicates that the system's frequency response does not lead to instability, as it does not encircle the critical point (-1,0) in the Nyquist plot.

**Key Features and Technical Details:**
- The plot is symmetric with respect to the real axis, indicating a conjugate symmetry typical for systems with real coefficients.
- The movement from \( M \) to \( N \) suggests a change in phase from negative to positive, consistent with the behavior of a stable system.
- The lack of encirclement of the origin is significant as it implies that the system is stable according to the Nyquist stability criterion.

**Annotations and Specific Data Points:**
- Points \( M \) and \( N \) are marked on the plot, indicating specific points on the contour.
- The line does not cross the real axis at the origin, confirming that there is no encirclement.
- The plot is smooth without any sharp turns or discontinuities, suggesting a continuous and stable frequency response.

Figure 10.56 (a) $s$ contour enclosing pole and zero, and (b) $H$ contour.

What happens if the first-order system has no zero? As shown in Fig. 10.57(a), $\angle H$ is equal to $-180^{\circ}$ at point $M$, reaching $-90^{\circ}$ at $s_{1}$ and zero at $N$. Also, $H\left(\sigma_{M}\right)=A_{0} /\left(1+\sigma_{M} / \omega_{p}\right)<0$ and $H\left(\sigma_{N}\right)>0$ [Fig. 10.57(b)]. We thus observe that $H(s)$ encircles the origin in this case, and that the encirclement is in the counterclockwise direction. Similarly, if the system has only one zero and no pole, a clockwise $s$ contour containing the zero maps to an $H$ contour that encircles the origin in the clockwise direction [Fig. 10.57(c)]. We hereafter assume that the $s$ contours are symmetric around the $\sigma$ axis, obtaining polar plots that are symmetric around the real axis.
image_name:(a)
description:Figure 10.57(a) illustrates a contour plot on the complex plane for a system with one pole. The plot is labeled with axes \( \sigma \) (real part) and \( j\omega \) (imaginary part), which is typical for a Nyquist diagram. The contour is a closed loop that begins and ends at point \( M \), passing through point \( N \). The path of the contour is indicated by arrows, showing a clockwise direction around the complex plane.

The contour encloses a pole located at \( -\omega_p \) on the real axis, which is marked with an 'x'. The contour starts at \( M \), moves upwards, loops around, and returns to \( M \) after passing through \( N \). The path is symmetric around the real axis, reflecting the system's response as the frequency varies.

This plot represents the behavior of the transfer function \( H(s) \) as the contour in the \( s \)-plane encircles the pole. The contour in the \( s \)-plane maps to a corresponding contour in the \( H \)-plane, as shown in the subsequent figures (Fig. 10.57(b) and (c)), which indicate how the contour around the pole affects the system's stability and response characteristics. The critical points \( M \) and \( N \) on the contour correspond to specific values of \( H(s) \) that are relevant for analyzing the system's stability and frequency response characteristics.
image_name:(b)
description:The graph in Figure 10.57(b) is a Nyquist plot, which is a graphical representation used in control systems to determine the stability of a system. This plot maps the contour of the system's transfer function $H(s)$ in the complex plane.

1. **Type of Graph and Function:**
- This is a Nyquist plot representing the contour of the transfer function $H(s)$ as the complex frequency $s$ traverses a specified path in the $s$-plane.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as \( \text{Re}\{H\} \), representing the real part of the transfer function.
- The vertical axis is labeled as \( \text{Im}\{H\} \), representing the imaginary part of the transfer function.
- Units are typically dimensionless as they represent the gain and phase of the system.

3. **Overall Behavior and Trends:**
- The plot shows a closed contour that encircles the origin. The contour begins at point $M$ and proceeds to point $N$ in a counterclockwise direction, indicating that the phase of $H(s)$ becomes more positive as $s$ moves along its path.
- The shape of the contour suggests that the system's response includes both a zero and a pole, affecting the encirclement direction and the shape of the plot.

4. **Key Features and Technical Details:**
- The contour passes through specific points labeled as $H(\sigma_M)$ and $H(\sigma_N)$, indicating the real parts of the transfer function at specific frequencies.
- The loop encircles the origin once in the counterclockwise direction, which is significant for stability analysis, as it indicates the presence of poles in the right half of the $s$-plane.

5. **Annotations and Specific Data Points:**
- Points $M$ and $N$ are annotated on the plot, marking critical locations where the phase of $H(s)$ changes significantly.
- The plot does not show specific numerical values, but the encirclement and direction provide qualitative insights into the system's stability characteristics.
image_name:(c)
description:The graph labeled as (c) in Figure 10.57 is a Nyquist plot, which is used to represent the frequency response of a system in the complex plane. This particular plot is for a system with one zero and no pole.

1. **Type of Graph and Function:**
- This is a Nyquist plot, which visualizes the complex frequency response of a system.

2. **Axes Labels and Units:**
- The horizontal axis represents the real part of the transfer function $H(s)$, labeled as Re\{H\}.
- The vertical axis represents the imaginary part of the transfer function $H(s)$, labeled as Im\{H\}.
- There are no specific units provided for the axes, as they are dimensionless in Nyquist plots.

3. **Overall Behavior and Trends:**
- The Nyquist plot shows a closed contour that encircles the origin once in the clockwise direction.
- The contour begins at point $M$ and traverses through point $N$, indicating the path of the frequency response as the frequency varies.
- The contour is symmetric around the real axis, reflecting the symmetric nature of the $s$ contour around the $
abla$ axis.

4. **Key Features and Technical Details:**
- The plot indicates a clockwise encirclement of the origin, which is consistent with the system having one zero.
- The system's stability can be inferred from the number of encirclements and their direction, although specific stability conclusions require additional context about the open-loop poles and zeros.
- Key points such as $H(\sigma_M)$, $H(\sigma_N)$, and $H(s_1)$ are marked on the plot, representing significant points on the contour.

5. **Annotations and Specific Data Points:**
- The annotations $M$ and $N$ help identify the starting and ending points of the contour on the Nyquist plot.
- The plot does not provide specific numerical values for gains or phase angles, as it is a qualitative representation of the system's response.

Overall, this Nyquist plot illustrates the behavior of a system with one zero, showing how the frequency response encircles the origin in a manner that is typical for such systems.

Figure 10.57 (a) System with one pole, (b) $H$ contour, and (c) $s$ and $H$ contours if system has only one zero.

We now study a first-order system that has both a zero and a pole while the $s$ contour encircles only the pole. We note from Fig. 10.58(a) that the polar plot of $H(s)$ assumes a positive value at $M$, as it did in Fig. 10.56(b). As $s$ begins from point $M$ and traverses the contour clockwise, $\angle H$ becomes more positive, reaching $180^{\circ}$ at point $N$ [Fig. 10.58(b)]. (It is helpful as a crosscheck to show that $H\left(\sigma_{N}\right)<0$.) Thus, the $H$ contour encircles the origin counterclockwise in a manner similar to that in Fig. 10.57(b). The reader can repeat this exercise with an $s$ contour enclosing only the zero and prove that the plot of $H(s)$ encircles the origin clockwise.
image_name:(a)
description:The graph labeled "(a)" is a contour plot in the complex plane, specifically illustrating an $s$ contour that encloses a pole. This is a typical representation used in control systems and signal processing to analyze the behavior of transfer functions in the complex frequency domain.

1. **Type of Graph and Function:**
- The graph is a contour plot in the complex $s$-plane, often used in the context of Nyquist plots or root locus diagrams.

2. **Axes Labels and Units:**
- The horizontal axis is labeled $\sigma$, representing the real part of the complex frequency $s$.
- The vertical axis is labeled $j\omega$, representing the imaginary part of the complex frequency $s$.
- There are no specific units provided, as this is a conceptual representation.

3. **Overall Behavior and Trends:**
- The contour starts at point $M$ and moves clockwise around a pole located at $-\omega_p$ on the real axis.
- The contour passes through significant points $M$ and $N$, indicating critical changes in the behavior of the function $H(s)$.
- The path of the contour is a closed loop, indicating that it completely encloses the pole at $-\omega_p$.

4. **Key Features and Technical Details:**
- The point $M$ is marked on the left side of the contour, and point $N$ is on the right.
- The contour crosses the real axis twice, at $\sigma_M$ and $-\omega_z$, suggesting these are points of interest, possibly related to zero locations.
- The contour's clockwise traversal indicates the presence of a pole within the loop.

5. **Annotations and Specific Data Points:**
- The pole at $-\omega_p$ is marked with an "X" on the real axis.
- A zero is indicated at $-\omega_z$, marked with an open circle on the real axis.
- The direction of traversal is indicated by arrows, showing a clockwise path around the pole.
image_name:(b)
description:The graph in Fig. 10.58(b) is a Nyquist diagram representing the contour of the complex function $H(s)$ as $s$ traverses a specific path in the complex plane. This type of graph is typically used to analyze the stability of control systems.

**Axes Labels and Units:**
- The horizontal axis represents the real part of $H(s)$, labeled as Re\{H\}.
- The vertical axis represents the imaginary part of $H(s)$, labeled as Im\{H\}.
- There are no units specified for these axes as they represent complex quantities.

**Overall Behavior and Trends:**
- The contour begins at point $M$ and moves in a counterclockwise direction, encircling the origin.
- The path shows a loop that starts from point $M$, moves upward, and then curves around to point $N$.
- After reaching point $N$, the contour continues to encircle back to point $M$, forming a closed loop.

**Key Features and Technical Details:**
- The contour encircles the origin once in a counterclockwise manner, indicating that the system potentially has a pole in the right half-plane, which is crucial for stability analysis.
- The contour's shape is influenced by the poles and zeros of the system, particularly the interaction between $\omega_p$ and $\omega_z$ as seen in the related $s$-plane plot (Fig. 10.58(a)).
- The encirclement of the origin is a key feature in determining the number of poles in the right half-plane using the Nyquist stability criterion.

**Annotations and Specific Data Points:**
- Points $M$ and $N$ are marked on the contour, indicating significant phases in the traversal of $s$.
- The point $H(\sigma_N)$ is indicated, which is relevant for verifying the condition $H(\sigma_N)<0$ as a crosscheck for the contour’s direction and encirclement behavior.

This Nyquist plot is crucial for understanding the behavior of the system as it provides insight into the stability and response characteristics through the contour’s interaction with the origin in the complex plane.

Figure 10.58 (a) $s$ contour enclosing only one pole, and (b) $H$ contour.
Second-Order System Consider $H(s)=A_{0}\left[\left(1+s / \omega_{p 1}\right)\left(1+s / \omega_{p 2}\right)\right]^{-1}$ and assume that $s$ travels upward on the $j \omega$ axis [Fig. 10.59(a)]. We recognize that $|H(s)|$ begins at $A_{0}$ and falls as $s \rightarrow+j \infty$. Also, $\angle H(s)$ begins at 0 and becomes more negative, reaching $-90^{\circ}$ and, asymptotically, $-180^{\circ}$. As depicted in Fig. 10.59(b), the $H$ contour begins at $A_{0}$, rotates clockwise, crosses the $j \omega$ axis when
image_name:(a)
description:The graph labeled (a) in the context is a Nyquist plot, which represents the frequency response of a two-pole system in the complex plane.

1. **Type of Graph and Function:**
- This is a Nyquist plot, used to analyze the stability of a control system by plotting the frequency response of the transfer function $H(s)$.

2. **Axes Labels and Units:**
- The horizontal axis is labeled $\sigma$, representing the real part of the complex frequency $s$.
- The vertical axis is labeled $j\omega$, representing the imaginary part of the complex frequency $s$.

3. **Overall Behavior and Trends:**
- The plot begins at $s = 0$, corresponding to the gain $A_0$ at low frequencies.
- As $s$ travels upwards along the $j\omega$ axis, the magnitude of $H(s)$ decreases, representing the system's gain decreasing at higher frequencies.
- The phase of $H(s)$ starts at 0 degrees and becomes more negative, moving towards -90 degrees and asymptotically to -180 degrees.

4. **Key Features and Technical Details:**
- Two poles are marked on the real axis at $-\omega_{p1}$ and $-\omega_{p2}$, indicating the natural frequencies of the system.
- As the contour moves upwards, the plot shows a clockwise rotation, indicating a phase lag.
- The contour crosses the $j\omega$ axis when the phase angle of $H(s)$ is -90 degrees.

5. **Annotations and Specific Data Points:**
- The contour starts at $A_0$ on the real axis and eventually returns to the origin, completing a loop in the complex plane.
- The contour is symmetric about the real axis, reflecting the behavior of the system for $s = 0$ to $-j\infty$.

This Nyquist plot effectively illustrates the stability characteristics of the two-pole system by showing how the system's gain and phase shift vary with frequency.
image_name:(b)
description:The graph in Fig. 10.59(b) represents the Nyquist plot of a two-pole system transfer function \(H(s)\). The plot is a polar graph depicting the complex plane where the real part \(\text{Re}\{H\}\) is on the horizontal axis and the imaginary part \(\text{Im}\{H\}\) is on the vertical axis.

1. **Type of Graph and Function:**
- This is a Nyquist diagram, which is used to analyze the stability and frequency response of control systems.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \(\text{Re}\{H\}\) (Real part of \(H\)).
- The vertical axis is labeled \(\text{Im}\{H\}\) (Imaginary part of \(H\)).
- There are no specific units indicated, as Nyquist plots are typically dimensionless.

3. **Overall Behavior and Trends:**
- The plot begins at a point on the real axis at \(A_0\) when \(s=0\).
- As \(s\) moves upward along the \(j\omega\) axis from \(0\) to \(+j\infty\), the contour rotates clockwise.
- The plot crosses the imaginary axis at the point where the phase angle \(\angle H(s) = -90^\circ\).
- The contour continues into the third quadrant and returns to the origin, completing a full loop.

4. **Key Features and Technical Details:**
- The initial point at \(A_0\) represents the magnitude of the transfer function at \(s=0\).
- The phase angle begins at \(0^\circ\) and becomes more negative, approaching \(-180^\circ\) asymptotically.
- The crossing of the imaginary axis at \(-90^\circ\) is a critical point indicating a phase shift.

5. **Annotations and Specific Data Points:**
- The direction of the contour is indicated by arrows, showing a clockwise rotation.
- The contour is symmetric about the real axis, reflecting behavior for \(s=0\) to \(-j\infty\).
image_name:(c)
description:The graph labeled (c) in Figure 10.59 is a contour plot on the complex plane. It represents the path of the complex variable \( s \) as it traverses a contour that encloses both poles of a two-pole system. The axes are labeled \( \sigma \) (real part) on the horizontal axis and \( j\omega \) (imaginary part) on the vertical axis.

Type of Graph and Function:
This is a Nyquist contour plot used in control system analysis to evaluate the stability of a system by enclosing the poles in the \( s \)-plane.

Axes Labels and Units:
- **Horizontal Axis (\( \sigma \))**: Represents the real part of the complex frequency \( s \).
- **Vertical Axis (\( j\omega \))**: Represents the imaginary part of the complex frequency \( s \).

Overall Behavior and Trends:
- The contour starts at point \( M \) on the negative real axis, encircles the poles located at \( -\omega_{p1} \) and \( -\omega_{p2} \), and ends at point \( N \) on the positive real axis.
- The path is a closed loop that moves in a clockwise direction, indicating the traversal of the contour in the \( s \)-plane.

Key Features and Technical Details:
- **Poles**: The contour encloses two poles located at \( -\omega_{p1} \) and \( -\omega_{p2} \) on the negative real axis.
- **Contour Path**: The path includes segments labeled \( s_1, s_2, \) and \( s_3 \), which are intermediate points on the contour.
- **Direction**: The contour moves clockwise, which is typical for enclosing poles in the Nyquist plot.
- **Critical Points**: The contour crosses the real axis at points \( M \) and \( N \).

Annotations and Specific Data Points:
- The contour is annotated with several points \( s_1, s_2, \) and \( s_3 \), indicating specific locations on the path.
- The direction of traversal is indicated by arrows along the contour, emphasizing the clockwise movement.

This contour plot is fundamental in assessing the stability of a feedback control system by analyzing how the contour in the \( s \)-plane maps into the \( H(s) \)-plane, as shown in the subsequent plot (d). The behavior of the contour in this plot is critical for understanding the system's response to changes in frequency.
image_name:(d)
description:The graph in Fig. 10.59(d) is a Nyquist plot representing the contour of the transfer function \( H(s) \) as the complex variable \( s \) travels along a specific path in the complex plane. This is a crucial tool in control systems and stability analysis.

1. **Type of Graph and Function:**
- The graph is a Nyquist plot, which is used to assess the stability of a control system by mapping the contour of \( H(s) \) as \( s \) encircles the poles of the system.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as \( \text{Re}\{H\} \) (real part of \( H(s) \)).
- The vertical axis is labeled as \( \text{Im}\{H\} \) (imaginary part of \( H(s) \)).
- No specific units are provided, as the Nyquist plot is typically dimensionless.

3. **Overall Behavior and Trends:**
- The plot begins at the point \( H(\sigma_M) \) on the real axis and traces a loop in the complex plane.
- It moves through the points \( H(s_1) \), \( H(s_2) \), and \( H(s_3) \), indicating the system's response at these critical points.
- The contour loops back to the starting point, reflecting the behavior of the system as \( s \) travels around the poles.

4. **Key Features and Technical Details:**
- The contour encloses the origin, which is crucial for determining the system's stability.
- The plot crosses the real axis between points \( M \) and \( N \), indicating critical phase angles where \( \angle H(s) = -180^\circ \).
- The path reflects the clockwise encirclement of the poles, aligning with the Nyquist stability criterion.

5. **Annotations and Specific Data Points:**
- Points \( H(s_1) \), \( H(s_2) \), and \( H(s_3) \) are marked, showing significant values along the contour.
- The arrows on the contour indicate the direction of traversal, which is essential for interpreting the Nyquist plot correctly.
- The plot is symmetric about the real axis, highlighting the reflection property of the Nyquist plot when considering both positive and negative frequencies.

Figure 10.59 (a) Two-pole system, (b) $H$ contour as $s$ travels up on the $j \omega$ axis, (c) $s$ contour chosen to enclose both poles, and (d) corresponding $H$ contour.
$\angle H=-90^{\circ}$, enters the third quadrant, and eventually returns to the origin at a $180^{\circ}$ angle. For $s=0$ to $-j \infty$, this plot is reflected around the real axis.

What if the contour of $s$ encloses both poles? From Fig. 10.59(c), we note that $\angle H=-360^{\circ}$ at $M$ and $H\left(\sigma_{M}\right)>0$. As we travel clockwise on the $s$ contour to some point $s_{1}$, the angle becomes less negative, e.g., equal to $-320^{\circ}=+40^{\circ}$. Thus, the $H$ contour rotates counterclockwise [Fig. 10.59(d)]. At some point, $s_{2}$, the net angle is around $-270^{\circ}=+90^{\circ}$, and at some other point, $s_{3}$, we have $\angle H\left(s_{3}\right)=-180^{\circ}$. As $s$ approaches point $N, H(s)$ reaches a real, positive value. The other symmetric half is shown in gray for clarity. We observe that the polar plot encircles the origin twice in the counterclockwise direction if the $s$ contour encircles two poles in the clockwise direction.

### 10.8.4 Cauchy's Principle

From the foregoing studies, we postulate that, if the $s$ contour encircles $P$ poles and $Z$ zeros of $H(s)$ in the clockwise direction, then the polar plot of $H(s)$ encircles the origin $Z-P$ times in the same direction. This is known as "Cauchy's Principle of Argument." For example, if the $s$ contour encircles clockwise three zeros and no poles, then the $H$ contour encircles the origin $3-0=3$ times clockwise. As seen earlier, the $H$ contour is constructed primarily from the angles contributed by the poles and zeros, with little need for the exact knowledge of $|H|$.

We have thus far assumed that we know the locations of the poles and zeros of a transfer function and we construct the polar plot to see how many times it encircles the origin. One can embark on a different task: suppose we know that an $s$ contour contains $P$ poles but do not know the number of zeros within the contour. If we still manage to draw the polar plot of the transfer function and find that it encircles the origin clockwise $N$ times, we can conclude that the number of zeros within the $s$ contour is equal to $Z=N+P$. This is the key to Nyquist's stability theorem.

### 10.8.5 Nyquist's Method

Having studied the foregoing concepts patiently, the reader is now ready to learn Nyquist's stability analysis. A negative-feedback system whose closed-loop transfer function is given by

$$
\begin{equation*}
\frac{Y}{X}(s)=\frac{H(s)}{1+\beta H(s)} \tag{10.57}
\end{equation*}
$$

becomes unstable if it has any poles on the $j \omega$ axis or in the right half plane, both of which we call herein the "critical region." In other words, if $1+\beta H(s)$ has any zeros in this critical region, then the system is unstable.

How do we determine whether $1+\beta H(s)$ has any zeros in the critical region? Let us construct an $s$ contour containing this region (Fig. 10.60). From Cauchy's principle, we know that the polar plot of
image_name:Figure 10.60 Critical region in the s plane
description:The graph consists of two parts: a contour in the $s$-plane on the left and a corresponding polar plot on the right.

Left Side: $s$-Plane Contour
- **Type of Graph:** This is a contour plot in the $s$-plane.
- **Axes Labels and Units:**
- The horizontal axis is labeled $\sigma$ (real part of $s$).
- The vertical axis is labeled $j\omega$ (imaginary part of $s$).
- **Overall Behavior and Trends:**
- The contour encloses a region labeled as the "Critical Region."
- The contour is a closed loop that begins and ends on the $j\omega$ axis, indicating the path of $s$ as it traverses the critical region.
- **Key Features:**
- The contour loops around the critical region, which is essential for determining the stability of the system.

Right Side: Polar Plot
- **Type of Graph:** This is a polar plot of the function $1 + \beta H(s)$.
- **Axes Labels and Units:**
- The horizontal axis is labeled Re\{1 + $\beta H(s)$\} (real part).
- The vertical axis is labeled Im\{1 + $\beta H(s)$\} (imaginary part).
- **Overall Behavior and Trends:**
- The plot is a closed loop, indicating the path traced by $1 + \beta H(s)$ as $s$ traverses the contour in the $s$-plane.
- The plot does not appear to encircle the origin, which is crucial for stability analysis.
- **Key Features and Technical Details:**
- The direction of traversal is indicated by arrows, showing a clockwise direction.
- The number of encirclements of the origin by this plot will determine the stability of the system according to the Nyquist criterion.

Annotations and Specific Data Points:
- The critical region and the direction of traversal are annotated on both plots, providing guidance on how to interpret the system's stability based on the Nyquist criterion.

Figure 10.60 Critical region in the $s$ plane and the corresponding $H$ contour.
$1+\beta H(s)$ encircles the origin $Z-P$ times, where $Z$ and $P$ respectively denote the number of zeros and poles that $1+\beta H(s)$ contains within the $s$ contour. We thus proceed as follows: (1) independently determine $P$, (2) draw the polar plot of $1+\beta H(s)$ as $s$ traverses the contour shown in Fig. 10.60, (3) determine the number of times, $N$, that $1+\beta H(s)$ encircles the origin clockwise, and (4) find $P+N$ as the number of zeros that $1+\beta H(s)$ has in the critical region.

We must recognize a point that simplifies our task. The poles of $1+\beta H(s)$ are in fact the same as the poles of $H(s)$. If the open-loop system is stable (as is the case in most of our circuits), then $H(s)$ has no poles in the critical region and $N=Z$. Unless otherwise stated, we assume this to be true.

Before studying examples of the above procedure, we make one change that leads us to Nyquist's theorem: if the polar plot of $1+\beta H(s)$ encircles the origin, then the polar plot of $\beta H(s)$ encircles the point $(-1,0)$ (Fig. 10.61) because the latter is obtained by shifting the former to the left by one unit. Nyquist's theorem articulates this result as for a closed-loop system, $H(s) /[1+\beta H(s)]$, to be stable, the polar plot of $\beta H(s)$ must not encircle the point $(-1,0)$ clockwise as $s$ traverses a contour around the critical region clockwise.
image_name:Figure 10.61 Polar Plot of 1+βH(s)
description:The image contains two polar plots side by side, illustrating the Nyquist theorem.

1. **Type of Graph and Function:**
- These are polar plots, commonly used in control systems to analyze the stability of a system.
- The left plot represents $1+\beta H(s)$, and the right plot represents $\beta H(s)$.

2. **Axes Labels and Units:**
- Both plots have axes labeled as 'Re' (Real) on the horizontal axis and 'Im' (Imaginary) on the vertical axis.
- There are no specific units marked, as is typical for polar plots.

3. **Overall Behavior and Trends:**
- The polar plot of $1+\beta H(s)$ on the left shows a loop that encircles the origin (0,0) in a counter-clockwise direction.
- The polar plot of $\beta H(s)$ on the right is shifted to the left by one unit, such that it encircles the point (-1,0) in a similar counter-clockwise manner.

4. **Key Features and Technical Details:**
- The encirclement of the origin by the $1+\beta H(s)$ plot indicates potential instability in the closed-loop system unless specific conditions are met.
- The $\beta H(s)$ plot's encirclement of (-1,0) is crucial for applying Nyquist's criterion for stability.
- Both plots have a similar shape, indicating that the transformation from $1+\beta H(s)$ to $\beta H(s)$ is a simple horizontal shift.

5. **Annotations and Specific Data Points:**
- The origin (0,0) and the point (-1,0) are marked on the respective plots, highlighting the key reference points for stability analysis.
- Arrows on the plots indicate the direction of traversal, which is counter-clockwise in both cases.

Figure 10.61 Polar plots of $1+\beta H(s)$ and $\beta H(s)$.
In applying Nyquist's theorem, we must choose the $s$ contour so as to minimize the mathematical labor. One possibility is depicted in Fig. 10.62: we begin at the origin, travel on the $j \omega$ axis to $+j \infty$, go around the RHP on a very large radius, continue to $j \omega=-j \infty$, and return to the origin on the $j \omega$ axis. The reader may wonder what exactly happens now that the contour does not enclose the $j \omega$ axis. If $1+\beta H(s)$ has any zeros on this axis, then the polar plot of $\beta H(s)$ goes through the point $(-1,0)$ rather than encircle it. [Recall from Bode plots that $1+\beta H\left(j \omega_{1}\right)=0$ translates to $\left|\beta H\left(j \omega_{1}\right)\right|=1$ and $\angle H\left(j \omega_{1}\right)=180^{\circ}$.] Since the $s$ contour is symmetric around the $\sigma$ axis, we construct the $\beta H$ contour only as $s$ goes from the origin to $M$ and $N$, and simply reflect the result around the real axis to complete the task.
image_name:Figure 10.62 Simple contour enclosing the $j \omega$ axis and RHP.
description:Figure 10.62 is a Nyquist plot representing the contour of the function \( \beta H(s) \) as it encloses the \( j\omega \) axis and the right half plane (RHP). The graph is plotted on a complex plane with the horizontal axis labeled as \( \sigma \) (real part) and the vertical axis labeled as \( j\omega \) (imaginary part).

1. Type of Graph and Function:
- **Type:** Nyquist plot.
- **Function:** Represents \( \beta H(s) \), where \( H(s) \) is a transfer function.

2. Axes Labels and Units:
- **Horizontal Axis (\( \sigma \)):** Represents the real part of the complex function.
- **Vertical Axis (\( j\omega \)):** Represents the imaginary part of the complex function.
- **Scale:** Linear.
3. Overall Behavior and Trends:
- The contour starts at point \( M \) on the positive imaginary axis, moves clockwise, and passes through point \( N \) on the positive real axis.
- It then curves back towards the negative imaginary axis, creating a loop that is symmetric around the real axis.
4. Key Features and Technical Details:
- **Symmetry:** The contour is symmetric around the real axis, indicating that the Nyquist plot reflects the real part of the function.
- **Direction:** The arrow indicates the direction of increasing frequency, moving from point \( M \) to \( N \) and back.
- **Encirclement:** The contour does not encircle the point \((-1, 0)\), which is crucial for determining stability in control systems.
5. Annotations and Specific Data Points:
- **Points \( M \) and \( N \):** These are significant points on the plot, marking the transition of the contour from the imaginary to the real axis.
- **Reflection:** The lower part of the contour is a reflection of the upper part across the real axis, completing the Nyquist plot for the entire frequency range.

This Nyquist plot is used to assess the stability of a closed-loop system by examining whether the contour encloses the point \((-1, 0)\) on the complex plane, which it does not in this case, indicating a potential stability condition for the given system.

#### Example 10.9

Study the closed-loop stability if $H(s)=A_{0} /\left(1+s / \omega_{p 1}\right)$.

#### Solution

For the $s$ contour shown in Fig. 10.63(a), $\beta H(s)$ begins at $\beta A_{0}$ for $s=0$. As $s=j \omega$ moves upward, the phase becomes more negative. At $+j \infty$, the phase goes to $-90^{\circ}$ and the magnitude drops to zero, i.e., the polar plot reaches the origin at an angle of $-90^{\circ}$ [Fig. 10.63(b)]. What happens as $s$ enters the right half plane? Traveling in the RHP at a very long radius, $s$ keeps $\beta H(s)$ at zero. That is, the entire RHP contour from $M$ to $N$ maps to the origin. We reflect this polar plot around the real axis to obtain the complete $\beta H$ contour. Since the contour does not encircle $(-1,0)$, the closed-loop system is always stable.
image_name:Figure 10.63 (a)
description:The graph in Figure 10.63 (a) is a Nyquist plot, commonly used in control systems to assess the stability of a system by mapping the frequency response of a transfer function. This specific plot shows the contour of $s$ for a one-pole system.

1. **Type of Graph and Function:**
- The graph is a Nyquist plot, depicting the frequency response of a one-pole system.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as $\sigma$, representing the real part of the complex frequency $s$.
- The vertical axis is labeled as $j\omega$, representing the imaginary part of the complex frequency $s$.
- The plot is in the complex plane, and specific units are not provided, but it typically involves normalized frequency components.

3. **Overall Behavior and Trends:**
- The contour begins on the real axis at a point $-\omega_p$, where $\omega_p$ indicates a pole location on the negative real axis.
- The contour moves upwards along the imaginary axis, indicating increasing frequency.
- It loops around, forming a semicircular path in the right half-plane (RHP), and returns to the real axis.
- The plot reflects symmetry about the real axis, indicating the behavior of the system for negative frequencies.

4. **Key Features and Technical Details:**
- The contour is marked with points $M$ and $N$, which typically denote critical frequency points or transitions in the system's response.
- The contour does not encircle the point $(-1,0)$, which is crucial for assessing stability. Since there is no encirclement, the system is stable.
- The plot emphasizes the system's response in the RHP, showing that the response remains on the real axis as it extends to infinity.

5. **Annotations and Specific Data Points:**
- The pole location is marked with a cross on the negative real axis at $-\omega_p$.
- The arrows on the contour indicate the direction of increasing frequency, moving from low to high frequencies.
- The reflection of the contour around the real axis is shown in a lighter shade, illustrating the complete Nyquist contour for both positive and negative frequencies.

image_name:(b)
description:The graph in question is a Nyquist plot, which is used to assess the stability of a control system by mapping the frequency response of an open-loop transfer function.

**Axes Labels and Units:**
- The horizontal axis represents the real part of the function \( \beta H(s) \) and is labeled as \( \text{Re}\{\beta H(s)\} \).
- The vertical axis represents the imaginary part of the function \( \beta H(s) \) and is labeled as \( \text{Im}\{\beta H(s)\} \).

**Overall Behavior and Trends:**
- The Nyquist plot shows a closed-loop trajectory starting from the point \( \beta A_0 \) on the real axis when \( s = 0 \), indicating the initial gain of the system.
- As the frequency increases (indicated by the contour moving in the direction of the arrows), the plot loops around in a counter-clockwise manner.
- The contour approaches the origin as \( s \) approaches \( +j\infty \), showing that the magnitude decreases to zero.

**Key Features and Technical Details:**
- The plot does not encircle the critical point \((-1, 0)\), which implies that the closed-loop system is stable.
- The phase shift introduced by the poles causes the plot to move through the complex plane, eventually reaching a phase angle of \(-180^\circ\) at \( s = +j\infty \).
- The contour's shape is influenced by the two poles of the system, which contribute to the negative phase as frequency increases.

**Annotations and Specific Data Points:**
- The plot is annotated with arrows indicating the direction of increasing frequency, starting from \( s = 0 \) and moving towards \( s = +j\infty \).
- The point \( \beta A_0 \) on the real axis is marked, representing the initial condition at \( s = 0 \).

This Nyquist plot effectively illustrates the stability characteristics of the given system by showing how the frequency response behaves across the complex plane. The lack of encirclement of the critical point confirms the stability of the closed-loop system.

Figure 10.63 (a) $s$ contour for a one-pole system, and (b) $\beta H$ contour.

#### Example 10.10

Study the closed-loop stability if $H(s)=A_{0} /\left[\left(1+s / \omega_{p 1}\right)\left(1+s / \omega_{p 2}\right)\right]$.

#### Solution

At $s=0, \beta H(s)=\beta A_{0}$. As $s=j \omega$ moves upward, the two poles contribute negative phase (Fig. 10.64). At $s=+j \infty$, the phase goes to $-180^{\circ}$ and the magnitude falls to zero, i.e., the polar plot reaches the origin at an angle of $180^{\circ}$. The $\beta H$ contour remains at the origin as $s$ traverses the RHP at a very long radius from $M$ to $N$. Since the contour does not encircle $(-1,0)$, the closed-loop system is stable for any value of the feedback factor, $\beta$. The reader is encouraged to repeat this exercise for increasingly larger values of $\omega_{p 2}$.
image_name:(a)
description:The graph in figure (a) is a Nyquist plot representing the frequency response of a two-pole system in the complex plane. The axes are labeled with \( j\omega \) for the imaginary axis and \( \sigma \) for the real axis.

Type of Graph and Function
This is a Nyquist diagram used to analyze the stability of a control system by plotting the complex values of the open-loop transfer function \( \beta H(s) \) as a function of frequency \( \omega \).

Axes Labels and Units
- **Imaginary Axis (Vertical):** \( j\omega \)
- **Real Axis (Horizontal):** \( \sigma \)
- The plot does not explicitly show units, but it is understood that \( \omega \) is in radians per second and \( \sigma \) is dimensionless.

Overall Behavior and Trends
- The plot starts at a point on the real axis corresponding to the gain \( \beta A_0 \) at low frequencies.
- As frequency increases, the plot traces a clockwise loop.
- The contour begins at point \( M \) and moves towards \( N \), eventually reaching the origin.
- At high frequencies (\( s = +j\infty \)), the plot approaches the origin with a phase angle of \( -180^{\circ} \).

Key Features and Technical Details
- The plot crosses the real axis at two points, corresponding to the poles \( -\omega_{p1} \) and \( -\omega_{p2} \).
- The contour does not encircle the point \((-1,0)\), indicating that the closed-loop system is stable for any value of the feedback factor \( \beta \).
- The shape of the plot is influenced by the pole locations and the feedback factor.

Annotations and Specific Data Points
- Points \( M \) and \( N \) are marked on the plot to indicate significant parts of the contour.
- The plot does not explicitly show numerical values, but the general path and encirclement properties are clear.
- The dashed lines indicate the direction of the contour as it approaches the poles \( -\omega_{p1} \) and \( -\omega_{p2} \).

This Nyquist plot effectively demonstrates the stability characteristics of the system by showing that the contour does not encircle the critical point \((-1,0)\), thus confirming stability across different feedback values.

image_name:Figure 10.65(a)
description:The graph in Figure 10.65(a) is a Nyquist plot, which is used to analyze the stability of a control system. The plot represents the complex plane with the real part of \( \beta H(s) \) on the horizontal axis and the imaginary part on the vertical axis.

1. **Type of Graph and Function:**
- This is a Nyquist plot, a polar plot that shows the frequency response of a system.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as \( \text{Re}\{\beta H(s)\} \) and the vertical axis as \( \text{Im}\{\beta H(s)\} \). There are no specific units provided, as these are dimensionless quantities representing the real and imaginary parts of the system's transfer function.

3. **Overall Behavior and Trends:**
- The plot starts at a point on the positive real axis, labeled \( \beta A_0 \), and traces a path that rotates clockwise. It forms a loop that crosses the real axis and approaches the origin at \( s = +j \infty \).
- The contour does not encircle the critical point \((-1,0)\), indicating stability for the system.

4. **Key Features and Technical Details:**
- The plot shows a looped path, indicative of a phase shift as the system's frequency response is plotted.
- The direction of the contour is marked with arrows, showing the movement from \( s = 0 \) to \( s = +j \infty \).
- The loop does not cross the critical point, confirming that the system remains stable.

5. **Annotations and Specific Data Points:**
- The point \( \beta A_0 \) is marked on the real axis, indicating the starting magnitude of the function.
- Arrows indicate the direction of the contour, providing insight into how the frequency response evolves as the frequency increases.

This Nyquist plot provides a clear visual representation of the system's stability characteristics, showing that the contour avoids encircling the critical point, which is crucial for confirming stability in feedback systems.

Figure $10.64 s$ plane and $\beta H$ contours for a two-pole system.

#### Example 10.11

Study the closed-loop stability if $H(s)=A_{0} /\left[\left(1+s / \omega_{p 1}\right)\left(1+s / \omega_{p 2}\right)\left(1+s / \omega_{p 3}\right)\right]$.

#### Solution

The polar plot of $\beta H(s)$ begins at $\beta A_{0}$ and rotates clockwise, reaching an angle of $-270^{\circ}=+90^{\circ}$ and a magnitude of zero at $s=+j \infty$ [Fig. 10.65(a)]. The reflection of this half around the real axis completes the plot, revealing that the $\beta H$ contour can encircle $(-1,0)$ depending on the location of the intersection point, $Q$. At this point, $\angle \beta H=-180^{\circ}$, i.e., $\tan ^{-1}\left(\omega_{Q} / \omega_{p 1}\right)+\tan ^{-1}\left(\omega_{Q} / \omega_{p 2}\right)+\tan ^{-1}\left(\omega_{Q} / \omega_{p 3}\right)=180^{\circ}$. With the pole values known, one can compute $\omega_{Q}$ and hence $\left|\beta H\left(s=j \omega_{Q}\right)\right|$ so as to determine whether point $Q$ is to the right or to the left of $(-1,0)$. The corresponding calculation on Bode plots is illustrated in Fig. 10.65(b).

What happens to the $\beta H$ contour in Fig. 10.65(a) if different values of $\beta$ are chosen? Since the radius at every point on the plot is proportional to $\beta$, the contour contracts as $\beta$ decreases and expands as $\beta$ increases. Illustrated in Fig. 10.65(c), this trend confirms that a higher feedback factor can make a three-pole system unstable.
image_name:(a)
description:The diagram labeled as Figure 10.65(a) illustrates the $s$ and $H$ contours for a three-pole system. This Nyquist plot is a graphical representation used to analyze the stability of the system in the frequency domain.

1. **Main Components:**
- The plot features a contour that represents the complex function $\beta H(s)$, where $H(s)$ is the system's transfer function and $\beta$ is the feedback factor.
- The contour is plotted in the complex plane with the real part $\text{Re}\{\beta H(s)\}$ on the x-axis and the imaginary part $\text{Im}\{\beta H(s)\}$ on the y-axis.

2. **Flow of Information or Control:**
- The contour starts at the origin when $s = 0$ and proceeds to $s = +j\infty$, looping around the point $Q$, which represents the critical point $(-1,0)$ in the complex plane.
- The direction of the contour is indicated by arrows, showing the progression of $\beta H(s)$ as the frequency $\omega$ changes.

3. **Labels, Annotations, and Key Indicators:**
- The diagram includes key points labeled $M$ and $N$ on the contour.
- The point $Q$ is highlighted as a reference for determining stability, specifically how the contour encircles the point $(-1,0)$.
- The contour's shape and encirclement behavior are critical for assessing the system's stability according to the Nyquist stability criterion.

4. **Overall System Function:**
- The primary function of this diagram is to evaluate the stability of the three-pole system by examining how the contour encircles the point $(-1,0)$.
- The encirclement count is used to determine if the system is stable or unstable, where zero or an even number of encirclements suggest stability, and an odd number indicates potential instability.
- Adjusting the feedback factor $\beta$ affects the contour's radius, influencing the stability analysis as shown in the related diagrams.
image_name:(b)
description:The graph in Figure 10.65(b) is a Bode plot, which consists of two parts: a magnitude plot and a phase plot.

1. **Magnitude Plot:**
- **Axes Labels and Units:** The vertical axis represents the magnitude of the transfer function $|\beta H(\omega)|$ and is typically measured in decibels (dB), though specific units are not labeled here. The horizontal axis represents the frequency $\omega$, which is usually in radians per second or hertz.
- **Overall Behavior and Trends:** The magnitude plot shows a decreasing trend as frequency increases. It starts at a higher magnitude at low frequencies and declines through three marked frequency points $\omega_p1$, $\omega_p2$, and $\omega_p3$.
- **Key Features and Technical Details:** There are three vertical dashed lines indicating the pole frequencies $\omega_p1$, $\omega_p2$, and $\omega_p3$. The plot suggests a roll-off characteristic typical of a three-pole system.

2. **Phase Plot:**
- **Axes Labels and Units:** The vertical axis represents the phase angle of $\beta H(\omega)$, measured in degrees, ranging from 0° to -270°. The horizontal axis is the same frequency axis as the magnitude plot.
- **Overall Behavior and Trends:** The phase plot shows a downward trend, indicating a phase lag that increases with frequency. It passes through critical phase angles of -90°, -180°, and approaches -270°.
- **Key Features and Technical Details:** A specific point is marked as 'Point Q' on the phase plot, which likely corresponds to a critical phase or gain crossover frequency where the system's stability is assessed. This point is crucial for determining the stability of the system, particularly in relation to the Nyquist criterion.

3. **Annotations and Specific Data Points:**
- **Critical Values:** The intersection of the phase plot with the -180° line is significant for assessing stability margins. The question mark near the magnitude plot suggests uncertainty or a condition to be checked, possibly whether the gain is less than or equal to 1 at a specific frequency.

Overall, this Bode plot is used to analyze the frequency response of a three-pole system, with particular attention to points that might affect system stability, such as the gain and phase margins at the marked frequencies.
image_name:(c)
description:The system block diagram labeled "(c)" in Figure 10.65 illustrates the contour plot of the product \( \beta H(s) \) for different values of the feedback factor \( \beta \) in a three-pole system. The diagram is a graphical representation showing how the contour changes as \( \beta \) varies.

1. **Main Components:**
- The diagram features a contour plot of the complex function \( \beta H(s) \), where \( H(s) \) represents the system's transfer function and \( \beta \) is the feedback factor.
- Axes are labeled as \( \text{Re}\{\beta H(s)\} \) and \( \text{Im}\{\beta H(s)\} \), denoting the real and imaginary components, respectively.

2. **Flow of Information or Control:**
- The contour represents the locus of \( \beta H(s) \) in the complex plane as the frequency varies from zero to infinity.
- The contour's shape changes with different values of \( \beta \), indicating how feedback affects system stability.

3. **Labels, Annotations, and Key Indicators:**
- The diagram shows two contours: one for a smaller \( \beta \) and another for a larger \( \beta \).
- The contour for a larger \( \beta \) is depicted as expanding outward, while the smaller \( \beta \) contour is more contracted.
- Arrows indicate the direction of increasing frequency along the contour.

4. **Overall System Function:**
- The primary function of this diagram is to illustrate the effect of the feedback factor \( \beta \) on the stability of a three-pole system.
- As \( \beta \) increases, the contour expands, potentially leading to instability if it encircles the critical point \((-1,0)\). This emphasizes the significance of feedback in controlling system behavior and stability.

Figure 10.65 (a) $s$ and $H$ contours for three-pole system, (b) corresponding Bode plots, and (c) $H$ contour for different values of $\beta$.

In some cases, it may not be straightforward to determine how many times the $\beta H$ contour encircles $(-1,0)$ clockwise. The general procedure for counting the number of encirclements is as follows: (1) draw a straight line from $(-1,0)$ to infinity in any direction, (2) count the number of times the contour crosses this line in clockwise and counterclockwise directions, and (3) subtract the latter from the former.

### 10.8.6 Systems with Poles at Origin

Some open-loop systems contain one or more poles at the origin. For example, the integrator shown in Fig. 10.66 has the following transfer function:

$$
\begin{equation*}
H(s)=\frac{-1}{R_{1} C_{1} s} \tag{10.58}
\end{equation*}
$$

image_name:Figure 10.66 Integrator
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: InN(Ao)}
name: C1, type: Capacitor, value: C1, ports: {Np: InN(A0), Nn: Vout}
name: Ao, type: OpAmp, value: Ao, ports: {InP: GND, InN: InN(Ao), OutP: Vout}
]
extrainfo:The circuit is an integrator configuration using an operational amplifier, a resistor R1, and a capacitor C1. The input voltage Vin is fed through R1 to the inverting input of the op-amp Ao, and the feedback loop is closed by C1 connected from the output Vout to the inverting input InN.

if the op amp is ideal. When such systems are placed in a negative-feedback loop, their Nyquist stability analysis must choose a slightly different $s$ contour. We begin with a one-pole system as depicted in Fig. 10.67(a) and seek a contour that does not go through the origin so as to avoid an infinite value for $\beta H(s)$. Rather than begin at $(0,0)$, we travel on an infinitesimally small circle around it given by $\epsilon \exp (j \phi)$ until we reach the $j \omega$ axis and then move upward. The key point here is that $\epsilon$ is very small, simplifying the calculations.
image_name:(a)
description:The graph labeled "(a)" is a representation of the $s$-plane contour used in Nyquist stability analysis for a one-pole system. This contour is specifically chosen to avoid passing through the origin, thereby preventing an infinite value for the transfer function $\beta H(s)$.

1. **Type of Graph and Function:**
- This is a complex plane graph (also known as the $s$-plane) used in control theory for stability analysis.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as $\sigma$, representing the real part of the complex frequency $s$.
- The vertical axis is labeled as $j\omega$, representing the imaginary part of the complex frequency $s$.

3. **Overall Behavior and Trends:**
- The contour begins at a point slightly offset from the origin, represented by an infinitesimal circle with radius $\epsilon$. This ensures the path does not pass through the pole at the origin.
- The contour then moves upward along the imaginary axis ($j\omega$ direction), indicating traversal through increasing imaginary frequencies.

4. **Key Features and Technical Details:**
- The pole is marked at the origin of the $s$-plane, which is a critical point in the system.
- The contour is represented by $\epsilon e^{j\phi}$, where $\phi$ is the angle parameter, indicating a small circular path around the pole.
- This approach allows the analysis to proceed without encountering infinite values in the transfer function.

5. **Annotations and Specific Data Points:**
- The contour is annotated with $\epsilon e^{j\phi}$, indicating the path taken around the pole.
- The pole at the origin is explicitly marked, emphasizing its significance in the stability analysis.

Overall, this diagram illustrates the careful choice of contour in the $s$-plane to facilitate Nyquist stability analysis while avoiding singularities at the pole.
image_name:(b)
description:The graph labeled (b) is a Nyquist diagram, which is commonly used in control theory to assess the stability of a system. This specific diagram illustrates the contour of $\beta H(s)$ as $s$ traverses a modified path around a pole at the origin.

1. **Type of Graph and Function:**
- This is a Nyquist plot of the open-loop transfer function $\beta H(s)$.

2. **Axes Labels and Units:**
- The horizontal axis represents the real part of $\beta H(s)$, labeled as \(\text{Re}\{\beta H(s)\}\).
- The vertical axis represents the imaginary part of $\beta H(s)$, labeled as \(\text{Im}\{\beta H(s)\}\).
- No specific units are indicated, as this is a dimensionless representation.

3. **Overall Behavior and Trends:**
- The plot shows a semicircular path starting from a point on the positive real axis at $s = \epsilon$.
- As $s$ moves in a circular path around the origin, the contour of $\beta H(s)$ also moves in a semicircular arc from the positive real axis to the negative imaginary axis.
- The semicircular path reflects the phase change of $\beta H(s)$ as $s$ traverses the circle from $0$ to $90^\circ$.

4. **Key Features and Technical Details:**
- The contour begins at a point on the positive real axis, specifically at \(\beta \frac{A_0}{\epsilon}\), which is very large due to the small value of $\epsilon$.
- As $s$ moves around the circle, the phase of $\beta H(s)$ changes, causing the contour to move counterclockwise in the complex plane.
- The contour approaches the negative imaginary axis as $s$ reaches $90^\circ$.

5. **Annotations and Specific Data Points:**
- The starting point of the contour is marked as $s = \epsilon$ on the positive real axis.
- The contour is depicted as a dashed line, indicating the path of $\beta H(s)$ as $s$ moves along the circle.
- The point $\beta H(\epsilon e^{j90^\circ})$ is labeled on the negative imaginary axis, showing the endpoint of the semicircular path.

This Nyquist plot is crucial for analyzing the stability of the system by observing how the contour encircles the critical point, which in this case is the origin.

Figure 10.67 (a) $s$ plane contour bypassing pole at origin, and (b) corresponding $\beta H$ contour.

If $H(s)=A_{0} / s$ and we choose $s=\epsilon \exp (j \phi)$, then $\beta H(s)=\beta\left(A_{0} / \epsilon\right) \exp (-j \phi)$. At $\phi=0, s=\epsilon$, and $\beta H$ is real and very large [Fig. 10.67(b)]. As $s$ traverses the circle, $\phi$ rotates toward $+90^{\circ}$ and $\beta\left(A_{0} / \epsilon\right) \exp (-j \phi)$ remains at a very large radius, approaching $-90^{\circ}$. This behavior is indicated by a dashed curve in Fig. 10.67(b) to emphasize the large radius. Now, $s$ travels upward on the $j \omega$ axis, still retaining a phase of $-90^{\circ}$ (due to the pole at the origin), while $|\beta H|$ falls, i.e., $\beta H$ goes toward the origin at an angle of $-90^{\circ}$ and remains at $(0,0)$ as $s$ enters the RHP (not shown in the $s$ plane). The other half of the contour is obtained if $s$ begins from the RHP (not shown), arrives at $-j \infty$, travels toward the origin on the $j \omega$ axis, and traverses the circle $\epsilon \exp (j \phi)$ from $\phi=-90^{\circ}$ to $\phi=0$. Note that the polar plot of $\beta H$ does not encircle $(-1,0)$.

#### Example 10.12

Analyze the closed-loop stability of $H(s)=A_{0}\left(1+s / \omega_{z}\right) / s$. The zero can be created, for example, by inserting a resistor in series with $C_{1}$ in Fig. 10.66.

#### Solution

With $s=\epsilon \exp (j \phi)$ in Fig. 10.68(a), $\beta H(s) \approx \beta\left(A_{0} / \epsilon\right) \exp (-j \phi)$ because $\epsilon$ is small. Shown in Fig. 10.68(b) is the $\beta H$ contour. Even at $\phi=90^{\circ}$, the zero contributes negligible phase because the circle's radius is very small. As we travel upward on the $j \omega$ axis, the zero begins to add positive phase, and $\beta H(s)=\beta A_{0}\left(1+s / \omega_{z}\right) / s$ approaches a real value equal to $\beta A_{0} / \omega_{z}$ at $s=+j \infty$. In contrast to the case illustrated in Fig. 10.67, this contour is deflected away from the origin by the zero.
image_name:Figure 10.68 (a)
description:The diagram labeled "(a)" is a complex plane plot, likely a Nyquist diagram, used to analyze the stability of a feedback system. The axes are labeled \(\sigma\) (real part) and \(j\omega\) (imaginary part), representing the real and imaginary components of the complex frequency \(s\).

1. **Type of Graph and Function:**
- This is a Nyquist plot, which is typically used to assess the stability of control systems in the frequency domain.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \(\sigma\), representing the real part of the complex frequency.
- The vertical axis is labeled \(j\omega\), representing the imaginary part.
- Units are not specified, as this is a theoretical plot for analysis.

3. **Overall Behavior and Trends:**
- The plot shows a contour that begins at the origin and extends vertically upward along the imaginary axis.
- As the contour moves upward, it curves back towards the real axis, indicating a phase shift.

4. **Key Features and Technical Details:**
- The contour starts at a point labeled with an open circle at the origin, indicating the start of the frequency response.
- A significant feature is the angle \(\epsilon e^{j\phi}\), which suggests the contour is parameterized by a small perturbation \(\epsilon\) and phase angle \(\phi\).
- The contour crosses the imaginary axis, reflecting a phase shift as \(\phi\) increases.
- The contour's behavior suggests the presence of a pole at the origin and its deflection indicates the influence of a zero.

5. **Annotations and Specific Data Points:**
- The plot includes an annotated path showing the direction of increasing frequency.
- Specific markers or annotations are not provided for numerical values, but the contour’s trajectory indicates key phase changes in the system response.

This diagram provides insights into the phase and gain characteristics of the system, crucial for determining its stability using Nyquist criteria.
image_name:Figure 10.68 (b)
description:The graph labeled as (b) is a Nyquist diagram, which is used to analyze the stability of control systems. This specific diagram represents the complex plane with the real part of the function \( \beta H(s) \) on the x-axis (Re{\( \beta H(s) \)}) and the imaginary part on the y-axis (Im{\( \beta H(s) \)}).

Axes Labels and Units:
- **X-axis (Real):** Re{\( \beta H(s) \)}, representing the real part of the function.
- **Y-axis (Imaginary):** Im{\( \beta H(s) \)}, representing the imaginary part.

Overall Behavior and Trends:
- The contour starts from the point \( s = \epsilon \) on the real axis, moving in a clockwise direction.
- The path deflects away from the origin due to the presence of a zero, which affects the phase of the function.
- As the contour travels upward along the imaginary axis, \( \beta H(s) \) begins to add positive phase.
- At \( s = +j\infty \), the function approaches a real value of \( \beta A_{0} / \omega_{z} \).

Key Features and Technical Details:
- The contour initially is close to the real axis, indicating a large magnitude at \( s = \epsilon \).
- There is a noticeable deflection from the origin, consistent with the effect of the zero in the function.
- The contour passes through the point \( \beta A_{0} / \omega_{z} \) on the real axis, which is a critical value as \( s \) approaches infinity.
- The phase shift is significant as \( \phi \) increases, leading to a rotation in the contour.

Annotations and Specific Data Points:
- The diagram includes annotations such as \( \beta H(e^{j90^\circ}) \) and \( s = +j\infty \), indicating key points in the contour's path.
- The path is marked with arrows showing the direction of traversal, emphasizing the clockwise movement.

This Nyquist plot is essential for assessing the stability of the system by examining how the contour encircles the origin, which is indicative of system stability according to the Nyquist stability criterion.

#### Example 10.13

A negative-feedback loop employs two ideal integrators, i.e., $H(s)=A_{0} / s^{2}$. Study the closed-loop stability of the system.

#### Solution

We begin with $s=\epsilon \exp (j \phi), \phi=0$, and hence $\beta H=\beta A_{0} / \epsilon^{2}$ (Fig. 10.69). As $\phi$ goes to $+45^{\circ}$ (point $N$ ), $\beta H(s)=\beta\left(A_{0} / \epsilon^{2}\right) \exp (-2 j \phi)$ rotates by $-90^{\circ}$, still at a very large radius. For $\phi=+90^{\circ}$ (point $\left.P\right), \beta H(s)$ returns to the real axis. Now, as $s=+j \omega$ travels upward, the angle remains unchanged, but the magnitude, $\beta|H(j \omega)|=\beta A_{0} / \omega^{2}$, falls. That is, $\beta H$ continues on the real axis toward the origin, passing through $(-1,0)$ at $\omega=\sqrt{\beta A_{0}}$. The closed-loop system therefore contains two poles on the $j \omega$ axis because it crosses $(-1,0)$ twice. After all, we can write $H(s) /[1+\beta H(s)]=A_{0} /\left(s^{2}+\beta A_{0}\right)$, observing two imaginary poles at $\pm j \sqrt{\beta A_{0}}$. Thus, a two-pole system can oscillate if it has two poles at the origin.
image_name:Figure 10.69 (a)
description:The graph labeled "(a)" is a pole-zero plot typically used in control systems and signal processing to depict the position of poles and zeros in the complex plane. This particular plot illustrates the behavior of the transfer function \(H(s)\) with a zero added to one of the integrators.

1. **Type of Graph and Function:**
- This is a pole-zero plot in the complex plane, showing the trajectory of the function \(H(s)\) as it relates to stability and oscillation.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \(\sigma\) (real part), and the vertical axis is labeled \(j\omega\) (imaginary part).
- The plot does not specify units, as it is typically dimensionless in such diagrams.

3. **Overall Behavior and Trends:**
- The plot shows a trajectory beginning at the origin, indicating two poles at the origin (marked by a cross).
- The path moves upward along the imaginary axis to a point labeled \(Q\) at \(\omega = \sqrt{\beta A_0}\), indicating a critical frequency where the system behavior changes.
- The trajectory then curves around and crosses the real axis at point \(P\), marked \((-1,0)\), which is significant for stability analysis.

4. **Key Features and Technical Details:**
- The presence of two poles at the origin suggests potential oscillatory behavior.
- The crossing at \((-1,0)\) implies a critical point for stability, as it relates to the Nyquist criterion.
- The path continues, indicating the influence of the added zero, which alters the phase and magnitude of the system response.
- Points \(M\), \(N\), and \(Q\) are labeled along the trajectory, indicating specific values and changes in the system's response.

5. **Annotations and Specific Data Points:**
- The plot includes annotations such as \(\beta H(s)\) and values like \(\frac{A_0}{\epsilon^2}\), which are important for understanding the gain and phase characteristics of the system.
- The trajectory's path is depicted with arrows, showing the direction of movement and the influence of the added zero on the system's behavior.

This plot provides a visual representation of how adding a zero affects the system's poles and zeros, influencing its stability and response characteristics.
image_name:Figure 10.69 (b)
description:The graph labeled as (b) is a Nyquist plot, which is used to analyze the frequency response of a control system. This plot represents the complex function \( \beta H(s) \) as \( s \) varies along the imaginary axis, specifically for the system described by \( H(s) = A_0(1+s/\omega_z)/s^2 \).

Axes Labels and Units:
- **Horizontal Axis (Real Part)**: Represents the real part of \( \beta H(s) \).
- **Vertical Axis (Imaginary Part)**: Represents the imaginary part of \( \beta H(s) \).
- Units are not explicitly given, but they are typically dimensionless in a Nyquist plot.

Overall Behavior and Trends:
- The plot starts at the point \( M \) on the positive real axis, where \( s = \epsilon \) and \( \beta H \approx \frac{\beta A_0}{\epsilon^2} \).
- As \( s \) moves along the imaginary axis (\( s = j\omega \)), the plot traces a path that moves towards the left, crossing the negative real axis at point \( P \) which corresponds to \( (-1, 0) \).
- The plot continues in a circular path, looping around and returning towards the starting point \( M \), completing a loop around the origin.

Key Features and Technical Details:
- **Point \( P \)**: The plot crosses the negative real axis at \( (-1, 0) \), indicating a critical point where the system's phase is at a specific value.
- **Point \( Q \)**: Located on the imaginary axis, corresponds to \( \omega = \sqrt{\beta A_0} \), representing the frequency where significant phase contribution begins.
- The plot does not encircle the origin, indicating specific stability characteristics related to the closed-loop system.

Annotations and Specific Data Points:
- The plot is annotated with points \( P, Q, M, \) and \( N \), marking important transitions and behaviors as \( s \) traverses the Nyquist path.
- The system is described as having two poles at the origin, which is crucial in understanding its oscillatory behavior and stability.

This Nyquist plot provides insight into the stability and frequency response of the system, especially in understanding how the addition of a zero affects the phase and gain characteristics.

#### Example 10.14

Repeat the previous example if a zero is added to one of the integrators, i.e., $H(s)=A_{0}\left(1+s / \omega_{z}\right) / s^{2}$.

#### Solution

With $s=\epsilon \exp (j \phi)$ and $\phi=0$, we have $\beta H \approx \beta A_{0} / \epsilon^{2}$. The behavior of $\beta H$ is similar to that in the previous example up to point $P$ (Fig. 10.70). As $s=+j \omega$ travels upward, the zero begins to contribute appreciable phase and $|\beta H(j \omega)|=\beta A_{0} \sqrt{1+\omega^{2} / \omega_{z}^{2}} / \omega^{2}$ continues to fall. As $s \rightarrow+j \infty, \angle \beta H$ approaches $-90^{\circ}$, suggesting that the $\beta H$ contour must reach the origin at an angle of $-90^{\circ}$. As shown in Fig. 10.70, the zero ensures that $\beta H$ does not cross or encircle $(-1,0)$, stabilizing the closed-loop system.
image_name:Figure 10.70 (a)
description:The graph labeled as (a) in Figure 10.70 is a Nyquist plot, which is used to analyze the stability of control systems by mapping the frequency response of a system. This particular Nyquist plot represents the function \( \beta H(s) \) over a range of frequencies.

**Axes Labels and Units:**
- The horizontal axis represents the real part of \( \beta H(s) \), denoted as \( \sigma \).
- The vertical axis represents the imaginary part of \( \beta H(s) \), denoted as \( j\omega \).
- There are no specific units given, as this is a dimensionless plot.

**Overall Behavior and Trends:**
- The contour starts at a point on the negative real axis and loops around, moving upward and then downward, before returning to cross the real axis again.
- As \( s = +j\omega \) travels upward, the contour begins to contribute more phase, and the magnitude \( |\beta H(j\omega)| \) decreases.
- The contour does not encircle the critical point \((-1, 0)\), indicating stability in the closed-loop system.

**Key Features and Technical Details:**
- The contour begins at point \( P \) on the negative real axis and moves towards the origin.
- It passes through points \( N \) and \( M \), with \( M \) being on the positive real axis.
- The contour approaches the origin at an angle of \(-90^\circ\) as \( s \rightarrow +j\infty \).
- The zero in the system ensures the contour does not cross or encircle \((-1, 0)\).

**Annotations and Specific Data Points:**
- The plot includes specific markers for points \( P \), \( N \), and \( M \), which are significant in analyzing the system's response.
- The point \( Q \) is marked on the imaginary axis, denoting a specific frequency \( \omega = \sqrt{\beta A_0} \).
- The contour is annotated with the term \( \epsilon e^{j\phi} \), indicating a phase shift or rotation in the response.

This Nyquist plot is crucial for understanding the closed-loop stability and behavior of the system, particularly in relation to phase-locked loops and oscillations at certain frequencies.
image_name:Figure 10.70 (b)
description:The graph labeled "(b)" is a Nyquist plot, which is used to analyze the stability of a control system by depicting the frequency response of the open-loop transfer function \( \beta H(s) \).

1. **Axes Labels and Units:**
- The horizontal axis represents the real part of \( \beta H(s) \), while the vertical axis represents the imaginary part of \( \beta H(s) \). There are no specific units indicated as this is a complex plane representation.

2. **Overall Behavior and Trends:**
- The plot shows a contour starting from point \( P \) and moving in a clockwise direction. The contour loops around the origin, indicating how the gain and phase of the system change with frequency.
- As \( s \) approaches infinity, the contour approaches the origin at an angle of \(-90^\circ\).

3. **Key Features and Technical Details:**
- The contour does not cross or encircle the critical point \((-1, 0)\), which is crucial for determining system stability. This behavior indicates that the closed-loop system remains stable.
- The plot features a loop that extends from point \( M \) to \( N \) and back, indicating changes in the phase and magnitude of the transfer function.
- The contour is influenced by a zero, ensuring that the plot behaves in a stable manner without crossing the critical point.

4. **Annotations and Specific Data Points:**
- The point \( P \) is marked on the negative real axis as \(-\frac{\beta A_0}{\epsilon^2}\), while point \( M \) is marked on the positive real axis as \(\frac{A_0}{\epsilon^2}\).
- The point \((-1, 0)\) is highlighted as a reference for stability analysis.
- The path from \( P \) to \( M \) and \( N \) is shown with directional arrows, indicating the progression of the contour as frequency increases.

The foregoing example sheds light on a common paradox that the Bode plots of the two-integrator system conjure up, especially in the context of phase-locked loops (Chapter 16). As shown in Fig. 10.71, it appears that the above closed-loop system is capable of oscillation at a frequency $\omega_{1}$, at which $|\beta H|$ is greater than unity and $\angle \beta H=-180^{\circ}$. But we observe from the Nyquist plot in Fig. 10.70 or from $\beta H\left(j \omega_{1}\right)=-\beta A_{0}\left(1+j \omega_{1} / \omega_{z}\right) / \omega_{1}^{2}$ that, owing to the zero, the phase of $\beta H$ never reaches exactly $180^{\circ}$. That is, at point $P$ in Fig. 10.70, the infinitesimal phase contributed by the zero causes $|\angle \beta H|$ to be less than $180^{\circ}$. Similarly, even though the approximate Bode plots of Fig. 10.71 suggest a phase of $180^{\circ}$ for $\omega_{1} \ll \omega_{z}$, in reality this amount of phase occurs only at $\omega=0$. The story, however, does not end here. The next section provides a more fundamental understanding.
image_name:Figure 10.71 Bode plots of a system with two poles at origin and one zero.
description:The graph in Figure 10.71 consists of two Bode plots for a system with two poles at the origin and one zero. The top plot illustrates the magnitude response, while the bottom plot shows the phase response, both plotted against the logarithm of frequency (log ω).

**Magnitude Plot:**
- **Axes:** The vertical axis represents the magnitude in decibels (dB) as \(20\log|\beta H(\omega)|\), and the horizontal axis is the logarithmic frequency scale (log ω).
- **Behavior:** The magnitude plot starts with a slope of -40 dB/decade, indicating the presence of two poles at the origin. At a certain frequency \(\omega_1\), the slope changes to -20 dB/decade due to the presence of a zero. This slope change is marked by a dashed vertical line at \(\omega_1\).
- **Key Features:** The plot shows two distinct slopes before and after \(\omega_1\), with the transition occurring at the zero frequency \(\omega_z\).

**Phase Plot:**
- **Axes:** The vertical axis represents phase in degrees as \(\angle \beta H(\omega)\), and the horizontal axis is the logarithmic frequency scale (log ω).
- **Behavior:** The phase starts at 0 degrees and decreases to -90 degrees at \(\omega_1\), then further approaches -180 degrees as frequency increases, influenced by the zero.
- **Key Features:** The phase does not reach exactly -180 degrees, highlighting the effect of the zero. The transition points are indicated by dashed vertical lines at \(\omega_1\).

**Overall Trends:**
- The system exhibits a decrease in magnitude and phase as frequency increases, typical of systems with poles at the origin and zeros affecting the slope and phase shift.
- The presence of the zero modifies the slope and phase trajectory, preventing the phase from reaching -180 degrees exactly, as noted in the context.

### 10.8.7 Systems with Multiple $180^{\circ}$ Crossings

Consider a system whose loop transmission has three poles and two zeros as shown in Fig. 10.72(a). Illustrated in Fig. 10.72(b), the Bode plots reveal that the phase crosses $-180^{\circ}$ twice while the gain remains higher than unity. Is this system stable when placed in a negative-feedback loop?

image_name:(a)
description:The system block diagram labeled as "(a)" represents a system with three poles and two zeros. The main components of this system are depicted on a complex plane, where the horizontal axis represents the real part (Re) and the vertical axis represents the imaginary part (Im) of the function \( \beta H(s) \). The diagram includes:

1. **Poles and Zeros:**
- **Zeros (\( \omega_{z1} \) and \( \omega_{z2} \))**: These are represented by open circles on the real axis.
- **Poles (\( \omega_{p1} \), \( \omega_{p2} \), and \( \omega_{p3} \))**: These are represented by crosses on the real axis.

2. **Nyquist Path:**
- The Nyquist path is illustrated with a contour that starts at point A on the real axis and moves counterclockwise.
- The path includes segments labeled A, B, C, and D, indicating different sections of the contour.

3. **Flow of Information or Control:**
- The diagram suggests the system's response to frequency variations by showing how the function \( \beta H(s) \) behaves in the complex plane.
- The contour path indicates potential encirclements of the critical point, which is crucial for determining system stability.

4. **Overall System Function:**
- The primary function of this diagram is to analyze the stability of the system when placed in a negative-feedback loop.
- The presence of three poles and two zeros affects the system's phase and gain, which is further analyzed using Bode plots. The system's stability is evaluated based on the number of encirclements around the critical point in the Nyquist plot.

This diagram is part of a broader analysis involving Bode plots to understand how the phase crosses \(-180^{\circ}\) and the implications for system stability in feedback loops.

image_name:(b) Bode plots
description:The graph in question is a Bode plot, which consists of two plots: a magnitude plot and a phase plot. This type of graph is used to analyze the frequency response of a system.

1. **Type of Graph and Function:**
- This is a Bode plot, displaying both the magnitude and phase of a system's transfer function \( \beta H(\omega) \).

2. **Axes Labels and Units:**
- The magnitude plot (top) has the vertical axis labeled as \( 20\log|\beta H(\omega)| \), representing the gain in decibels (dB).
- The phase plot (bottom) has the vertical axis labeled as \( \angle H(\omega) \), representing the phase angle in degrees.
- Both plots share a horizontal axis labeled as \( \log \omega \), indicating a logarithmic scale for frequency.

3. **Overall Behavior and Trends:**
- **Magnitude Plot:** The magnitude decreases in a step-like fashion, indicating a system with multiple poles and zeros. The decline in magnitude is typical for systems with poles reducing gain as frequency increases.
- **Phase Plot:** The phase starts near 0 degrees, dips below -180 degrees, and then rises again, suggesting a complex phase behavior due to the interaction of poles and zeros.

4. **Key Features and Technical Details:**
- **Magnitude Plot:**
- The plot shows three distinct slopes corresponding to three poles \( \omega_{p1}, \omega_{p2}, \omega_{p3} \) and two zeros \( \omega_{z1}, \omega_{z2} \).
- Each pole contributes a -20 dB/decade slope, while each zero contributes a +20 dB/decade slope.
- **Phase Plot:**
- The phase crosses the -180 degrees line between points B and C, which is crucial for stability analysis.
- Points A, B, C, and D mark significant changes in the phase angle, correlating with the frequency locations of poles and zeros.

5. **Annotations and Specific Data Points:**
- The magnitude plot is annotated with vertical dashed lines at the frequencies of poles and zeros, \( \omega_{p1}, \omega_{p2}, \omega_{p3}, \omega_{z1}, \omega_{z2} \).
- The phase plot includes points A, B, C, and D, which are key in understanding the phase shift behavior and its impact on system stability.

This Bode plot is essential for understanding the frequency response and stability of the system, particularly in determining how the system behaves at critical frequencies and how it might respond under feedback conditions.

image_name:(c)
description:The graph labeled "(c)" is a Nyquist plot, which is used to assess the stability of a control system by plotting the complex values of the open-loop transfer function as frequency varies.

1. **Type of Graph and Function:**
- This is a Nyquist plot representing the frequency response of a system with three poles and two zeros.

2. **Axes Labels and Units:**
- The horizontal axis represents the real part of the transfer function, \( \text{Re}\{\beta H(s)\} \).
- The vertical axis represents the imaginary part of the transfer function, \( \text{Im}\{\beta H(s)\} \).
- The plot is in the complex plane, and no specific units are provided.

3. **Overall Behavior and Trends:**
- The plot shows a closed loop starting and ending at the far right side of the real axis.
- It loops around the origin, indicating how the phase and gain change with frequency.
- The path crosses the real axis at multiple points, indicating potential phase shifts.

4. **Key Features and Technical Details:**
- The plot starts from the point labeled \( A \) on the right and moves counterclockwise.
- It loops around a point, possibly indicating a critical point for stability analysis.
- The curve crosses the real axis twice, suggesting potential multiple crossings of the \(-180^{\circ}\) phase angle.

5. **Annotations and Specific Data Points:**
- Points \( A, B, C, \) and \( D \) are marked, indicating significant points in the plot.
- The direction of the curve is indicated with arrows, showing the path of the frequency response as it loops around the critical point.

This Nyquist plot is essential for determining the stability of a system when placed in a negative-feedback loop. The multiple crossings of the real axis are critical in assessing the stability margins and potential for oscillations.

image_name:(d) Nyquist plot
description:The graph depicted is a Nyquist plot, which is a polar plot of the frequency response of a control system. It is used to assess the stability of a feedback system by plotting the complex function \( \beta H(s) \) as a function of frequency.

Axes Labels and Units:
- **Horizontal Axis (Real Part):** Labeled as \( \text{Re}\{\beta H(s)\} \), representing the real part of the frequency response.
- **Vertical Axis (Imaginary Part):** Labeled as \( \text{Im}\{\beta H(s)\} \), representing the imaginary part of the frequency response.
- The axes are typically unitless in a Nyquist plot, as they represent scaled values of the system's transfer function.

Overall Behavior and Trends:
- The plot features a looped path in the complex plane, starting from point \( A \) and moving through points \( B, C, \) and \( D \), indicating the trajectory of the frequency response as frequency increases.
- The path crosses the real axis multiple times, which is crucial for determining the stability margins.
- Arrows on the plot indicate the direction of increasing frequency, moving from low to high frequencies.

Key Features and Technical Details:
- **Critical Point:** The plot is centered around the critical point \((-1, 0)\), which is significant for stability analysis.
- **Points of Interest:**
- **Point A:** Represents the starting or ending point of the Nyquist path.
- **Point B:** Indicates a crossing of the real axis.
- **Point C:** Another crossing point, possibly indicating a change in the direction of the loop.
- **Point D:** Marks a significant feature in the loop.
- **Infinity Points:** The plot extends towards infinity in the imaginary direction, indicating the behavior as frequency approaches infinity.

Annotations and Specific Data Points:
- The plot is annotated with specific points \( P \) and \( Q \), which may represent specific frequencies or phase conditions.
- The contour includes a dashed line from \( P \) to \( Q \), suggesting a reference or transition line.
- The arrows along the path indicate the direction of increasing frequency, helping to visualize the system's response over the frequency range.

This Nyquist plot is instrumental in determining the stability of the system when placed in a negative-feedback loop. The multiple crossings of the real axis and the loop around the critical point \((-1, 0)\) are key in assessing the stability margins and the potential for oscillations.

image_name:Figure 10.72 (e)
description:Figure 10.72 (e) is a Nyquist plot, which is used to analyze the stability of a feedback system by illustrating the frequency response of the open-loop transfer function, \( \beta H(s) \).

Axes Labels and Units:
- **Horizontal Axis (Re{\( \beta H(s) \)}):** Represents the real part of the open-loop transfer function.
- **Vertical Axis (Im{\( \beta H(s) \)}):** Represents the imaginary part of the open-loop transfer function.

Overall Behavior and Trends:
- The plot features a complex trajectory that begins at point \( A \) on the positive real axis and extends towards infinity in the imaginary direction.
- As it progresses, the curve loops back, crossing the real axis at point \( B \) and creating a closed loop with notable points \( C \) and \( D \).
- The curve approaches the origin from the direction of \( s = +j\infty \), indicating high-frequency behavior.

Key Features and Technical Details:
- **Point \( B \):** Marks a crossing on the real axis, significant for determining stability margins.
- **Points \( C \) and \( D \):** Indicate regions of phase change and are critical for analyzing phase margin.
- The plot passes near the critical point \((-1, 0)\), which is crucial for determining the stability of the closed-loop system.
- The trajectory's direction is counterclockwise, which is typical for systems with negative feedback.

Annotations and Specific Data Points:
- The Nyquist plot provides insight into gain and phase margins by illustrating the contour's proximity to the critical point \((-1, 0)\).
- The plot highlights the importance of ensuring the contour does not encircle the critical point in the clockwise direction, which would indicate potential instability.

This Nyquist plot is essential for visualizing the stability characteristics of the system, particularly in feedback control design, where ensuring the system does not become unstable is critical.

Figure 10.72 (a) System with three poles and two zeros, (b) Bode plots, (c) $\beta H$ contour, (d) case where $C$ is to the left of $(-1,0)$, and (e) case where $C$ is to the right of $(-1,0)$.

In the absence of the zeros, the $\beta H$ contour crosses $-180^{\circ}$ and approaches the origin at an angle of $-270^{\circ}$ [Fig. 10.65(a)]. We now construct the Nyquist plot as follows. As we begin from the origin in Fig. 10.72(a) and travel up on the $j \omega$ axis, the phase starts at zero and the $\beta H$ contour at point $A$ in Fig. 10.72(c). Due to the higher number of poles, $\angle \beta H$ becomes negative, reaching $-180^{\circ}$ (point $B$ ) for some value of $j \omega$. As $\omega$ increases further, $\angle \beta H$ becomes more negative, but, due to the contribution of the zeros, it deflects, forcing the $\beta H$ contour to return to the real axis (point $C$ ). The phase then becomes more positive and, for $\omega \rightarrow \infty$, approaches $-90^{\circ}$ (point $D$ ). Drawing the other symmetric half, we distinguish between two cases.

1. Point $C$ is to the left of $(-1,0)$ [Fig. 10.72(d)]; if we draw a line from $(-1,0)$ to infinity, it crosses the contour twice (at $P$ and $Q$ ), but the contour has opposite directions at these two points. The
closed-loop system therefore has no poles in the RHP. Since both $B$ and $C$ are to the right of $(-1,0)$, this case corresponds to the Bode plots of Fig. 10.72(b).
2. Point $(-1,0)$ lies between $C$ and $B$ [Fig. 10.72(e)]. In this case, the system is unstable.

We summarize the above results as follows. If $\angle \beta H$ crosses $180^{\circ}$ an even (odd) number of times while $|\beta H|>1$, then the system is stable (unstable).
