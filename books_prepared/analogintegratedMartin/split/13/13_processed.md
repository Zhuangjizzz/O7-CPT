# 13 Discrete-Time Signals

A basic understanding of discrete-time signal processing is essential in the design of most modern analog systems. For example, discrete-time signal processing is heavily used in the design and analysis of oversampling analog-todigital (A/D) and digital-to-analog (D/A) converters used in digital audio, wireless communication, and instrumentation applications. Also, a discrete-time filtering technique known as switched-capacitor filtering is a popular approach for realizing fully integrated analog filters. Switched-capacitor filters are in the class of analog filters since voltage levels in these filters remain continuous. In other words, switched-capacitor filters operate and are analyzed using discrete time-steps but involve no $\mathrm{A} / \mathrm{D}$ or $\mathrm{D} / \mathrm{A}$ converters; hence, they are quantized in time but not in amplitude. This chapter presents some basic concepts of discrete-time signals and filters.

## 13.1 OVERVIEW OF SOME SIGNAL SPECTRA

Consider the spectra of sampled and continuous-time signals in the block diagram systems shown in Fig. 13.1, where it is assumed that the continu-ous-time signal, $\mathrm{x}_{\mathrm{c}}(\mathrm{t})$, is band limited through the use of an anti-aliasing filter (not shown). DSP refers to Discrete-time signal processing, which may be accomplished using fully digital processing or discrete-time analog circuits such as switched-capacitor filters. Some example time signals and frequency spectra for this system are shown in Fig. 13.2. Here, $\mathbf{s}(\mathrm{t})$ is a periodic impulse train in time with a period of T , where T equals the inverse of the sampling frequency, $\mathrm{f}_{\mathrm{s}}$. Some relationships for the signals in

Key Point: Discrete-time signals may be processed either digitally, in which case they are quantized both in time and amplitude, or using discrete-time analog circuits such as switched-capacitor circuits, in which case the signal amplitude is continuously variable.

Figs. 13.1 and 13.2 are as follows:

1. $x_{s}(t)$ has the same frequency spectrum as $x_{c}(t)$, but the baseband spectrum repeats every $f_{s}$ (assuming that no aliasing occurs and hence, an anti-aliasing filter is needed).
2. $x(n)$ has the same frequency spectrum as $x_{s}(t)$, but the sampling frequency is normalized to 1 .
3. The frequency spectrum for $x_{s h}(t)$ equals that of $x_{s}(t)$ multiplied by a response of $(\sin x) / x($ in effect, multiplying $X_{s}(f)$ by this response helps to remove high-frequency images).
The remainder of this chapter confirms these spectral relationships and introduces other basic discrete-time concepts.

## 13.2 LAPLACE TRANSFORMS OF DISCRETE-TIME SIGNALS

Consider the sampled signal, $\mathbf{x}_{\mathrm{s}}(\mathrm{t})$, related to the continuous-time signal, $\mathrm{x}_{\mathrm{c}}(\mathrm{t})$, as shown in Fig. 13.3. The signal $\mathrm{x}_{\mathrm{s}}(\mathrm{t})$ is fictitious; it does not arise anywhere in a practical physical realization, such as the one depicted in Fig. 13.1(b). However, it is a useful tool to aid our understanding and modeling of practical discrete-time signals.
image_name:(a)
description:The system block diagram labeled as "(a)" represents a conceptual realization of performing digital signal processing (DSP) on analog signals. Here's a detailed breakdown of the diagram:

1. **Main Components:**
- **Multiplier (Mixer):** The signal \( x_c(t) \) is multiplied by a sampling signal \( s(t) \) to produce a sampled signal \( x_s(t) \).
- **Convert to Discrete-Time Sequence:** This block converts the sampled continuous-time signal \( x_s(t) \) into a discrete-time sequence \( x(n) = x_c(nT) \).
- **DSP (Digital Signal Processor):** This block processes the discrete-time sequence \( x(n) \) to produce a processed discrete-time output \( y(n) \).
- **Convert to Impulse Train:** Converts the processed discrete-time sequence \( y(n) \) back into a continuous-time impulse train \( y_s(t) \).
- **Hold:** This block holds the impulse train \( y_s(t) \) to produce a piecewise constant signal \( y_{sh}(t) \).
- **Analog Low-Pass Filter:** The final block smooths out the held signal \( y_{sh}(t) \) to reconstruct the continuous-time output signal \( y_c(t) \).

2. **Flow of Information or Control:**
- The continuous-time input signal \( x_c(t) \) is first sampled by multiplying it with \( s(t) \), resulting in \( x_s(t) \).
- \( x_s(t) \) is then converted into a discrete-time sequence \( x(n) \), which is fed into the DSP block.
- The DSP block outputs a processed sequence \( y(n) \), which is converted into an impulse train \( y_s(t) \).
- The impulse train \( y_s(t) \) is held to form \( y_{sh}(t) \), and finally, the low-pass filter outputs the continuous-time signal \( y_c(t) \).

3. **Labels, Annotations, and Key Indicators:**
- \( x_c(t) \): Continuous-time input signal.
- \( x_s(t) \): Sampled signal after multiplication.
- \( x(n) = x_c(nT) \): Discrete-time sequence.
- \( y(n) \): Output from DSP.
- \( y_s(t) \): Impulse train.
- \( y_{sh}(t) \): Held signal.
- \( y_c(t) \): Final continuous-time output signal.

4. **Overall System Function:**
- The primary function of this system is to perform digital signal processing on an analog input signal. The analog signal \( x_c(t) \) is sampled, converted to a discrete sequence, processed digitally, and then converted back to a continuous-time signal through a series of steps involving impulse train conversion, holding, and filtering. This arrangement allows for the manipulation and enhancement of signals in the digital domain before converting them back to analog form for practical applications.
image_name:(b)
description:The system block diagram labeled "(b)" illustrates a typical physical realization for performing digital signal processing (DSP) on analog signals. The process begins with an analog continuous-time signal \( x_c(t) \).

1. **Sample and Hold:** The first block is the "Sample and hold" circuit. This component samples the continuous-time signal \( x_c(t) \) at discrete intervals and holds each sample value for a certain period. The output of this block is \( x_{sh}(t) \), a sampled version of the input signal that maintains the sample value constant between sampling points.

2. **A/D Converter:** The output from the "Sample and hold" block is fed into an "A/D converter" (Analog-to-Digital Converter). This block converts the sampled analog signal \( x_{sh}(t) \) into a discrete-time digital sequence \( x(n) \). The digital sequence \( x(n) \) represents the sampled values of \( x_c(nT) \) at discrete time intervals \( nT \).

3. **DSP:** The digital sequence \( x(n) \) is then processed by the "DSP" block. This block performs various digital signal processing operations, such as filtering, modulation, or other transformations, to produce a new digital sequence \( y(n) \).

4. **D/A Converter with Hold:** The processed digital signal \( y(n) \) is passed to a "D/A converter with hold" (Digital-to-Analog Converter). This block converts the digital sequence back into an analog signal \( y_{sh}(t) \), applying a hold function to maintain the analog value between digital samples.

5. **Analog Low-Pass Filter:** Finally, the analog signal \( y_{sh}(t) \) is input into an "Analog low-pass filter." This block smooths the signal, removing high-frequency components introduced during the sampling and conversion processes, resulting in the continuous-time output signal \( y_c(t) \).

Overall, this system converts an analog input signal into a digital form for processing and then back into an analog signal, suitable for various applications in communication and signal processing systems.

Fig. 13.1 Performing DSP on ana log signals. (a) Conceptual realization, and (b) typical physical realization.
image_name:x_s(t)
description:The graph titled "x_s(t)" is a time-domain waveform representing a sampled version of an analog signal, \( x_c(t) \). The graph is a combination of a continuous-time signal and its sampled counterpart, depicted as a series of vertical lines at discrete time intervals, \( nT \), where \( T \) is the sampling period.

Type of Graph and Function:
- **Type:** Time-domain waveform
- **Function:** Represents sampled signal \( x_s(t) \) derived from the continuous-time signal \( x_c(t) \).

Axes Labels and Units:
- **Horizontal Axis (t):** Represents time. Units are typically in seconds, but specific units are not labeled.
- **Vertical Axis:** Represents amplitude, but specific units are not labeled.
- **Scale:** Linear scale for both axes.

Overall Behavior and Trends:
- The continuous-time signal \( x_c(t) \) is shown as a smooth, sinusoidal curve.
- The sampled signal \( x_s(t) \) is represented by a series of vertical lines (impulses) at discrete intervals \( nT \), where each impulse's height corresponds to the amplitude of the continuous signal at that specific time.
- As \( \tau \to 0 \), the area under each pulse equals the value of \( x_c(nT) \).

Key Features and Technical Details:
- The continuous signal is sinusoidal, indicating periodic behavior.
- The sampled signal \( x_s(t) \) captures the amplitude of \( x_c(t) \) at each sampling point, effectively discretizing the continuous waveform.
- The relationship \( x_s(nT) = \frac{x_c(nT)}{\tau} \) is highlighted, showing how the sampled values are scaled.

Annotations and Specific Data Points:
- Annotations indicate the relationship between \( x_s(t) \) and \( x_c(t) \) through the scaling factor \( \tau \).
- The graph emphasizes the conversion from a continuous-time to a discrete-time signal, a key aspect of digital signal processing.
image_name:x_c(t)
description:The graph titled "x_c(t)" represents a time-domain waveform and its corresponding frequency spectrum, focusing on the process of sampling and reconstruction of signals.

1. **Type of Graph and Function:**
- The left side of the diagram illustrates time-domain signals, including continuous-time signal \( x_c(t) \), sampled signal \( x_s(t) \), discrete signal \( x(n) \), and the zero-order hold reconstruction signal \( x_{sh}(t) \).
- The right side shows frequency-domain representations of these signals, illustrating their spectra.

2. **Axes Labels and Units:**
- **Time-Domain (Left):**
- The horizontal axis is labeled \( t \) for continuous time and \( n \) for discrete time.
- The vertical axis represents amplitude.
- **Frequency-Domain (Right):**
- The horizontal axis is labeled \( f \) or \( \omega \) for frequency.
- The vertical axis represents amplitude, with units of \( A \) or \( \frac{A}{T} \).

3. **Overall Behavior and Trends:**
- **Time-Domain:**
- \( x_c(t) \) is a continuous sinusoidal waveform.
- \( x_s(t) \) consists of impulse samples derived from \( x_c(t) \), scaled by \( \tau \).
- \( x(n) \) is a discrete representation of the sampled signal, showing values at discrete intervals.
- \( x_{sh}(t) \) is a stepwise approximation of \( x_c(t) \), representing zero-order hold reconstruction.
- **Frequency-Domain:**
- \( X_c(f) \) shows a single peak at \( f_0 \).
- \( X_s(f) \) and \( X(\omega) \) display periodic replicas of the spectrum at multiples of the sampling frequency \( f_s \).
- \( X_{sh}(f) \) shows a modified spectrum, indicating the effects of zero-order hold.

4. **Key Features and Technical Details:**
- **Time-Domain:**
- The continuous waveform \( x_c(t) \) is smoothly oscillating.
- The sampled signal \( x_s(t) \) is represented by vertical lines at regular intervals.
- The discrete signal \( x(n) \) is marked by dots at each sample point.
- The reconstruction \( x_{sh}(t) \) is a piecewise constant function.
- **Frequency-Domain:**
- The spectrum \( X_c(f) \) has a single peak at \( f_0 \).
- The spectra \( X_s(f) \) and \( X(\omega) \) exhibit aliasing, with peaks at \( f_s \) and its multiples.
- The spectrum \( X_{sh}(f) \) shows attenuation at higher frequencies due to the zero-order hold.

5. **Annotations and Specific Data Points:**
- The time-domain graphs are annotated with the functions \( \tau x_s(t) \) and \( x_{sh}(t) \) to indicate their respective processes.
- The frequency-domain graphs indicate specific frequencies such as \( f_0 \), \( f_s \), and \( 2f_s \), highlighting the effects of sampling and reconstruction on the signal's spectrum.
image_name:x(n)
description:The graph labeled "x(n)" is a time-domain waveform representing a discrete-time signal. The x-axis is labeled with integer values indicating discrete time steps (n = 0, 1, 2, 3, etc.), while the y-axis represents the amplitude of the signal. The waveform is depicted as a series of vertical lines with dots at the top, connected by a dashed line that suggests the underlying continuous-time signal from which this discrete signal is sampled.

Axes Labels and Units:
- **X-axis:** Discrete time steps (n)
- **Y-axis:** Amplitude (unitless, but typically normalized or scaled)

Overall Behavior and Trends:
The graph shows a sinusoidal pattern, indicating that the discrete signal is sampled from a continuous sinusoidal waveform. The amplitude of the signal varies periodically, suggesting that the original continuous signal is a sinusoidal function. The sampling points (dots) are aligned with the peaks and troughs of the dashed sinusoidal line, illustrating the sampled nature of the signal.

Key Features and Technical Details:
- **Periodicity:** The signal exhibits periodic behavior, matching the sinusoidal pattern of the underlying continuous signal.
- **Sampling Points:** The signal is sampled at discrete intervals, as indicated by the dots and vertical lines at each integer time step.

Annotations and Specific Data Points:
- **Discrete Time Steps:** The graph is annotated with time steps n = 0, 1, 2, 3, etc., showing the discrete nature of the signal.
- **Dashed Line:** Represents the continuous-time sinusoidal waveform from which the discrete signal is sampled.

This graph is part of a larger system demonstrating the process of digital signal processing (DSP) on analog signals, where the continuous analog signal is sampled to form a discrete signal for digital processing.
image_name:X_c(f)
description:The graph labeled "X_c(f)" depicts a frequency spectrum of the continuous-time signal \( x_c(t) \). This is a frequency-domain representation, where the horizontal axis represents frequency \( f \) in hertz, and the vertical axis represents amplitude, denoted as \( A \).

Type of Graph and Function:
This is a frequency spectrum graph, displaying the frequency components of a continuous-time signal.

Axes Labels and Units:
- **Horizontal Axis (Frequency \( f \))**: Measured in hertz (Hz).
- **Vertical Axis (Amplitude \( A \))**: Represents the amplitude of the frequency components.

Overall Behavior and Trends:
The graph shows a triangular-shaped peak centered at a fundamental frequency \( f_0 \). The spectrum is symmetrical around this frequency, indicating the presence of a single dominant frequency component in the signal. The amplitude of this component is \( A \).

Key Features and Technical Details:
- **Peak at \( f_0 \)**: There is a significant peak at the fundamental frequency \( f_0 \), representing the main frequency component of the signal.
- **Symmetry**: The spectrum is symmetrical, suggesting that the signal is composed primarily of this single frequency and its harmonics.
- **No Other Peaks**: There are no additional peaks shown in this spectrum, indicating a lack of other significant frequency components within the analyzed range.

Annotations and Specific Data Points:
- The peak is labeled with amplitude \( A \), emphasizing the strength of the signal at \( f_0 \).
- The graph does not show any specific numerical values for \( f_0 \) or \( A \), but these are critical for understanding the signal's characteristics.

This graph provides insight into the frequency content of the continuous-time signal \( x_c(t) \), highlighting its primary frequency component and amplitude without additional complexity from other frequencies.
image_name:X_s(f)
description:The graph labeled "X_s(f)" represents a frequency spectrum of a sampled signal. It is a line plot on a frequency domain, where the horizontal axis is labeled as 'f' for frequency, and the vertical axis is labeled as 'A/T', indicating amplitude over time.

Type of Graph and Function:
This is a frequency spectrum diagram, typically used to illustrate the frequency components of a signal after sampling.

Axes Labels and Units:
- **Horizontal Axis (f):** Represents frequency, potentially in hertz (Hz).
- **Vertical Axis (A/T):** Represents amplitude over time, indicating the strength of frequency components.

Overall Behavior and Trends:
The graph shows a series of triangular peaks, indicating the presence of distinct frequency components. The primary peak is centered at the base frequency \( f_0 \), with additional peaks occurring at multiples of the sampling frequency \( f_s \) and \( 2f_s \). This pattern suggests that the signal has been sampled, and these peaks represent the spectral replicas that occur due to the sampling process.

Key Features and Technical Details:
- **Primary Peak at \( f_0 \):** The main frequency component of the original signal.
- **Replicas at \( f_s \) and \( 2f_s \):** These additional peaks are typical in sampled signals, representing the aliasing effect where frequency components are mirrored around the sampling frequency.
- **Amplitude:** The amplitude of the peaks is scaled by \( A/T \), indicating the amplitude of the frequency components relative to the sampling period.

Annotations and Specific Data Points:
- **Markers at \( f_0, f_s, 2f_s \):** Indicate the locations of the significant frequency components and their replicas. These markers are critical for understanding the effects of sampling and potential aliasing in the signal processing context.

This graph is crucial for analyzing the effects of sampling on the frequency content of a signal, especially in digital signal processing applications. It highlights how original and aliased frequencies are distributed across the spectrum after sampling.
image_name:X(ω)
description:The graph labeled "X(ω)" is a frequency spectrum plot, typically used to represent the frequency content of a signal in the angular frequency domain. Here is a detailed description of the graph:

1. **Type of Graph and Function:**
- The graph is a frequency spectrum plot in the angular frequency domain, commonly used in signal processing to depict how signal energy is distributed across different frequencies.

2. **Axes Labels and Units:**
- The horizontal axis represents angular frequency (ω), measured in radians per second.
- The vertical axis represents amplitude, typically normalized or scaled by a factor \( \frac{A}{T} \), where \( A \) is the amplitude and \( T \) is the period.

3. **Overall Behavior and Trends:**
- The graph shows a series of triangular-shaped spectra centered around specific angular frequencies.
- The main lobe is centered at \( \frac{2\pi f_0}{f_s} \) and extends to \( 2\pi \), indicating the primary frequency content of the signal.
- Repeated spectra are visible at multiples of \( 2\pi \), such as \( 4\pi \), reflecting the periodic nature of the frequency spectrum due to sampling.

4. **Key Features and Technical Details:**
- The main spectral lobe is centered at \( \frac{2\pi f_0}{f_s} \), which is a scaled representation of the original frequency \( f_0 \) in terms of the sampling frequency \( f_s \).
- The amplitude of the spectral components is scaled by \( \frac{A}{T} \), indicating a normalization based on the signal's amplitude and period.
- The periodic repetition of the spectrum at intervals of \( 2\pi \) is a characteristic of the sampled signals, indicating aliasing effects.

5. **Annotations and Specific Data Points:**
- There are no specific annotations or markers, but critical points are the centers of the spectral lobes at \( \frac{2\pi f_0}{f_s} \), \( 2\pi \), and \( 4\pi \).
- The graph visually emphasizes how sampling replicates the frequency spectrum in the angular frequency domain, a key concept in digital signal processing.
image_name:x_sh(t)
description:The graph labeled "x_sh(t)" is a time-domain waveform representing a sample-and-hold signal. This type of graph typically illustrates how a continuous-time signal is converted into a discrete-time signal for digital processing.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph depicting a sample-and-hold process.

2. **Axes Labels and Units:**
- The horizontal axis represents time (t) and is likely in arbitrary units, as no specific unit is provided.
- The vertical axis represents the amplitude of the signal.

3. **Overall Behavior and Trends:**
- The graph shows a stepped waveform, where each step corresponds to a sample taken from the continuous signal. The original continuous signal is shown as a dashed line, while the sampled signal is represented by a piecewise constant function.
- The sampled signal holds a constant value between sampling points, creating a staircase-like appearance.

4. **Key Features and Technical Details:**
- Each step in the waveform represents the value of the continuous signal at discrete sampling intervals.
- The dashed line indicates the original continuous waveform, which the sample-and-hold circuit approximates.
- The amplitude of each step matches the value of the continuous signal at the corresponding sampling point.

5. **Annotations and Specific Data Points:**
- The graph does not have specific numerical annotations, but the visual representation clearly shows the approximation of the continuous signal by the sample-and-hold process.
- The waveform's stepped nature highlights the discrete nature of digital sampling compared to the smoothness of the original analog signal.
image_name:X_sh(f)
description:The graph labeled "X_sh(f)" is a frequency-domain representation of a sampled signal, specifically focusing on the aliasing effects present in the frequency spectrum.

1. **Type of Graph and Function:**
- This is a frequency-domain graph, likely a spectrum plot, illustrating the frequency components of a sampled signal after a zero-order hold operation.

2. **Axes Labels and Units:**
- The horizontal axis represents frequency \( f \), typically in hertz (Hz).
- The vertical axis represents amplitude, though it is not explicitly labeled with units.

3. **Overall Behavior and Trends:**
- The graph shows multiple peaks, indicating the presence of various frequency components.
- The main peak is centered at the fundamental frequency \( f_0 \), with additional mirrored peaks appearing at multiples of the sampling frequency \( f_s \) and \( 2f_s \).
- The amplitude of the peaks decreases as the frequency increases, showing the effect of the zero-order hold which introduces sinc-like attenuation in the frequency domain.

4. **Key Features and Technical Details:**
- The peak at \( f_0 \) represents the original signal frequency.
- Peaks at \( f_s \) and \( 2f_s \) are due to aliasing, a common artifact in sampled systems.
- The amplitude of the main peak is marked as \( A \), indicating the magnitude of the frequency component.
- The graph also shows the effect of the zero-order hold with lobes that appear around these frequencies, demonstrating the sinc function's impact on the frequency response.

5. **Annotations and Specific Data Points:**
- No specific numerical values are provided for the frequency points, but the presence of \( f_0 \), \( f_s \), and \( 2f_s \) is marked.
- The graph visually emphasizes the aliasing effect and the zero-order hold's impact by showing the spread of frequency components.

Fig. 13.2 Some time signals and frequency spectra.

Compared to $\mathrm{x}_{\mathrm{c}}(\mathrm{t}), \mathrm{x}_{\mathrm{s}}(\mathrm{t})$ has been scaled by $\tau$ such that the area under the pulse at nT equals the value of $x_{c}(n T)$. In other words, at $t=n T$, we have

$$
\begin{equation*}
\mathrm{x}_{\mathrm{s}}(\mathrm{nT})=\frac{\mathrm{x}_{\mathrm{c}}(\mathrm{nT})}{\tau} \tag{13.1}
\end{equation*}
$$

image_name:Fig. 13.3 Sampled and continuous-time signals
description:The graph in Fig. 13.3 illustrates both sampled and continuous-time signals. It is a time-domain waveform plot, showing the relationship between the continuous signal \( x_c(t) \) and the sampled signal \( \tau x_s(t) \).

1. **Axes Labels and Units:**
- The horizontal axis represents time \( t \), marked at intervals of \( T \), \( 2T \), \( 3T \), and so on, with a specific point at \( nT \). There are no specific units indicated, but time is generally considered in seconds or milliseconds in such contexts.
- The vertical axis is not explicitly labeled with units, but it represents the amplitude of the signals \( x_c(t) \) and \( \tau x_s(t) \).

2. **Overall Behavior and Trends:**
- The continuous-time signal \( x_c(t) \) is shown as a smooth, dashed curve that oscillates, indicating periodic behavior.
- The sampled signal \( \tau x_s(t) \) is depicted as a series of vertical bars or pulses that occur at each sampling interval \( nT \). The height of these pulses corresponds to the amplitude of \( x_c(t) \) at those specific sampling times, scaled by \( \tau \).

3. **Key Features and Technical Details:**
- The continuous curve \( x_c(t) \) represents the original signal before sampling.
- The vertical pulses \( \tau x_s(t) \) represent the sampled values of the continuous signal, showing how the continuous signal is captured at discrete intervals.
- The graph emphasizes the relationship between the continuous signal and its sampled version, indicating that the area under each pulse of \( \tau x_s(t) \) equals the value of \( x_c(nT) \).

4. **Annotations and Specific Data Points:**
- Annotations on the graph point out the continuous signal \( x_c(t) \), the sampled signal \( \tau x_s(t) \), and a single pulse at \( nT \) as \( \tau x_{sn}(t) \).
- The dotted line follows the continuous signal, marking the sampled points where vertical bars intersect the curve.

This graph effectively demonstrates the concept of sampling in signal processing, showing how a continuous signal is represented by discrete samples at regular intervals.

Fig. 13.3 Sampled and continuous-time signals.
such that the area under the pulse, $\tau \mathrm{x}_{\mathrm{s}}(\mathrm{nT})$, equals $\mathrm{x}_{\mathrm{c}}(\mathrm{nT})$. Thus, as $\tau \rightarrow 0$, the height of $\mathrm{x}_{\mathrm{s}}(t)$ at time $n T$ goes to $\infty$, and so we plot $\tau \mathrm{X}_{\mathrm{s}}(\mathrm{t})$ instead of $\mathrm{X}_{\mathrm{s}}(\mathrm{t})$.

We define $\vartheta(\mathrm{t})$ to be the step function given by

$$
\vartheta(t) \equiv \begin{cases}1 & (t \geq 0)  \tag{13.2}\\ 0 & (t<0)\end{cases}
$$

Then $x_{s}(t)$ can be represented as a linear combination of a series of pulses, $x_{s n}(t)$, where $x_{s n}(t)$ is zero everywhere except for a single pulse at nT . The single-pulse signal, $\mathrm{x}_{\mathrm{sn}}(\mathrm{t})$, can be written as

$$
\begin{equation*}
\mathrm{x}_{\mathrm{sn}}(\mathrm{t})=\frac{\mathrm{x}_{\mathrm{c}}(\mathrm{nT})}{\tau}[\vartheta(\mathrm{t}-\mathrm{nT})-\vartheta(\mathrm{t}-\mathrm{nT}-\tau)] \tag{13.3}
\end{equation*}
$$

so that we can now write $\mathrm{x}_{\mathrm{s}}(\mathrm{t})$ as

$$
\begin{equation*}
\mathrm{x}_{\mathrm{s}}(\mathrm{t})=\sum_{\mathrm{n}=-\infty}^{\infty} \mathrm{x}_{\mathrm{sn}}(\mathrm{t}) \tag{18.4}
\end{equation*}
$$

Note that these signals are defined for all time, so we can find the Laplace transform of $\mathrm{x}_{\mathrm{s}}(\mathrm{t})$ in terms of $\mathrm{x}_{\mathrm{c}}(\mathrm{t})$. Using the notation that $X_{s}(s)$ is the Laplace transform of $x_{s}(t)$, we find the Laplace transform $X_{s n}(s)$ for $x_{s n}(t)$ to be given by

$$
\begin{equation*}
\mathrm{X}_{\mathrm{sn}}(\mathrm{~s})=\frac{1}{\tau}\left(\frac{1-\mathrm{e}^{-\mathrm{s} \tau}}{\mathrm{~s}}\right) \mathrm{x}_{\mathrm{c}}(\mathrm{nT}) \mathrm{e}^{-\mathrm{snT}} \tag{13.5}
\end{equation*}
$$

Since $x_{s}(t)$ is merely a linear combination of $x_{s n}(t)$, we also have (for $\tau \neq 0$ )

$$
\begin{equation*}
X_{s}(s)=\frac{1}{\tau}\left(\frac{1-e^{-s t}}{s}\right) \sum_{n=-\infty}^{\infty} x_{c}(n T) e^{-s n T} \tag{13.6}
\end{equation*}
$$

Using the expansion $\mathrm{e}^{\mathrm{x}}=1+\mathrm{x}+\left(\mathrm{x}^{2} / 2\right.$ ! $)+\cdots$, when $\tau \rightarrow 0$, the term before the summation in (13.6) goes to unity. Therefore, in the limiting case as $\tau \rightarrow 0$, we have

$$
\begin{equation*}
X_{s}(s)=\sum_{n=-\infty}^{\infty} x_{c}(n T) e^{-s n T} \tag{13.7}
\end{equation*}
$$

### 13.2.1 Spectra of Discrete-Time Signals

The spectrum of the sampled signal, $x_{s}(t)$, can be found by replacing $s$ by $j \omega$ in (13.7). However, a more intuitive approach to find the spectrum of $x_{s}(t)$ is to recall that multiplication in the time domain is equivalent to convolution in the frequency domain. To use this fact, note that, for $\tau \rightarrow 0, \mathrm{x}_{\mathrm{s}}(\mathrm{t})$ can be written as the product

$$
\begin{equation*}
\mathrm{x}_{\mathrm{s}}(\mathrm{t})=\mathrm{x}_{\mathrm{c}}(\mathrm{t}) \mathrm{s}(\mathrm{t}) \tag{13.8}
\end{equation*}
$$

where $\mathrm{s}(\mathrm{t})$ is a periodic pulse train, or mathematically,

$$
\begin{equation*}
s(t)=\sum_{n=-\infty}^{\infty} \delta(t-n T) \tag{13.9}
\end{equation*}
$$

where $\delta(\mathrm{t})$ is the unit impulse function, also called the Dirac delta function. It is well known that the Fourier transform of a periodic impulse train is another periodic impulse train. Specifically, the spectrum of $s(t), S(j \omega)$, is given by

$$
\begin{equation*}
\mathrm{S}(\mathrm{j} \omega)=\frac{2 \pi}{\mathrm{~T}} \sum_{\mathrm{k}=-\infty}^{\infty} \delta\left(\omega-\mathrm{k} \frac{2 \pi}{\mathrm{~T}}\right) \tag{13.10}
\end{equation*}
$$

Now writing (13.8) in the frequency domain, we have

$$
\begin{equation*}
X_{s}(j \omega)=\frac{1}{2 \pi} X_{c}(j \omega) \otimes S(j \omega) \tag{13.11}
\end{equation*}
$$

where $\otimes$ denotes convolution. Finally, by performing this convolution either mathematically or graphically, the spectrum of $X_{s}(j \omega)$ is seen to be given by

$$
\begin{equation*}
X_{s}(j \omega)=\frac{1}{T} \sum_{k=-\infty}^{\infty} X_{c}\left(j \omega-\frac{j k 2 \pi}{T}\right) \tag{13.12}
\end{equation*}
$$

or, equivalently,

$$
\begin{equation*}
X_{s}(f)=\frac{1}{T} \sum_{k=-\infty}^{\infty} X_{c}\left(j 2 \pi f-j k 2 \pi f_{s}\right) \tag{13.13}
\end{equation*}
$$

Key Point: The spectrum of a sampled signal is a sum of shifted copies of the original continuous-time spectrum so that no aliasing occurs if the original waveform is bandlimited to one-half the sampling rate. The minimum sampling frequency required to avoid aliasing is called the Nyquist rate, and is equal to two times the signal bandwidth.

Equations (13.12) and (13.13) show that the spectrum of the sampled signal, $x_{s}(t)$, equals a sum of shifted spectra of $x_{c}(t)$, and therefore no aliasing occurs if $X_{c}(j \omega)$ is band limited to $f_{s} / 2$. The minimum sampling frequency required to avoid aliasing is called the Nyquist rate, and is equal to two times the signal bandwidth. The relation in (13.13) also confirms the example spectrum for $\mathrm{X}_{\mathrm{s}}(\mathrm{f})$, shown in Fig. 13.2. Each copy of the dirac-delta-sampled spectrum is identical: $X_{s}(f)=X_{s}\left(f \pm k f_{s}\right)$, where $k$ is an arbitrary integer as seen by substitution in (13.13). ${ }^{1}$

Finally, note that the signal $\mathbf{x}_{s}(t)$ cannot exist in practice when $\tau \rightarrow 0$ since an infinite amount of power would be required to create it. This is evident when one considers the integral of $X_{s}(f)$ over all frequencies.

## 13.3 z-TRANSFORM

For our purposes, the z-transform is merely a shorthand notation for (13.7). Specifically, defining

$$
\begin{equation*}
z \equiv e^{s T} \tag{13.14}
\end{equation*}
$$

we can write

$$
\begin{equation*}
X(z) \equiv \sum_{n=-\infty}^{\infty} x_{c}(n T) z^{-n} \tag{13.15}
\end{equation*}
$$

where $X(z)$ is called the $z$-transform of the samples $x_{c}(n T)$.
Two properties of the $\mathbf{z}$-transform that can be deduced from Laplace transform properties are as follows:

1. If $x(n) \leftrightarrow X(z)$, then $x(n-k) \leftrightarrow z^{-k} X(z)$
2. Convolution in the time domain is equivalent to multiplication in the frequency domain. Specifically, if $y(n)=h(n) \otimes x(n)$, where $\otimes$ denotes convolution, then $Y(z)=H(z) X(z)$. Similarly, multiplication in the time domain is equivalent to convolution in the frequency domain.

Note that $X(z)$ is not a function of the sampling rate but is related only to the numbers $x_{c}(n T)$, whereas $X_{s}(s)$ is the Laplace transform of the signal $x_{s}(t)$ as $\tau \rightarrow 0$. In other words, the signal $x(n)$ is simply a series of numbers that may (or may not) have been obtained by sampling a continuous-time signal. One way of thinking about this series of numbers as they relate to the samples of a possible continuous-time signal is that the original sample time, $T$, has been effectively normalized to one (i.e., $f_{s}^{\prime}=1 \mathrm{~Hz}$ ). Such a normalization of the sample time, $T$, in both time and frequency, justifies the spectral relation between $X_{s}(f)$ and $X(\omega)$ shown in Fig. 13.2. Specifically, the relationship between $X_{s}(f)$ and $X(\omega)$ is given by

$$
\begin{equation*}
\mathrm{X}_{\mathrm{s}}(\mathrm{f})=\mathrm{X}\left(\frac{2 \pi \mathrm{f}}{\mathrm{f}_{\mathrm{s}}}\right) \tag{13.16}
\end{equation*}
$$

or, equivalently, the following frequency scaling has been applied:

$$
\begin{equation*}
\omega=\frac{2 \pi f}{f_{s}} \tag{13.17}
\end{equation*}
$$

This normalization results in discrete-time signals having $\omega$ in units of radians/sample, whereas the original continuous-time signals have frequency units of cycles/second (hertz) or radians/second. For example, a continuous-time sinusoidal signal of 1 kHz when sampled at 4 kHz will change by $\pi / 2$ radians between each sample. Therefore, such a discrete-time signal is defined to have a frequency of $\pi / 2 \mathrm{rad} / \mathrm{sample}$. Other examples of discrete-time sinusoidal signals

Key Point: Discrete-time signal spectra are equal to the corresponding sampled signal spectra with the sample time normalized to 1 Hz . Hence, their spectra repeat every $2 \pi$.
are shown in Fig. 13.4. The spectra of discrete-time signals are always invariant under shifts of $2 \pi$ radians/sample. For example, a discrete-time signal that has a frequency of $\pi / 4 \mathrm{rad} / \mathrm{sample}$ is identical to that of $9 \pi / 4 \mathrm{rad} / \mathrm{sample}$. Thus, normally discrete-time signals are completely specified by considering their spectra only between $-\pi$ and $\pi \mathrm{rad} / \mathrm{sample}$. For a more detailed discussion of this topic, see [Proakis, 1992].

#### EXAMPLE 13.1

Consider the spectra of $X_{c}(f)$ and $X_{s}(f)$, shown in Fig. 13.2, where $f_{0}$ is 1 Hz and $f_{s}$ is 4 Hz . Compare the time and spectrum plots of $X_{s}(f)$ and $X_{s 2}(f)$, where $X_{s 2}(f)$ is sampled at 12 Hz . How do the spectra differ between the two sampling rates?

#### Solution

By sampling at 12 Hz , the spectrum of $\mathrm{X}_{\mathrm{c}}(\mathrm{f})$ repeats every 12 Hz , resulting in the signals shown in Fig. 13.5.
Note that, for $X(\omega), 4 \mathrm{~Hz}$ is normalized to $2 \pi \mathrm{rad} / \mathrm{sample}$, whereas for $X_{2}(\omega), 12 \mathrm{~Hz}$ is normalized to $2 \pi \mathrm{rad} / \mathrm{sample}$.
image_name:(a)
description:The graph labeled (a) is a discrete-time signal plot. It is a stem plot representing a sequence of discrete samples over time. The x-axis is labeled 'n', representing the sample number, and the y-axis is labeled 'x(n)', representing the amplitude of the signal at each sample.

In this specific plot, the frequency is denoted as 0 rad/sample, which corresponds to 0 cycles/sample. This indicates that the signal is a constant or DC signal, meaning it does not vary with time. The plot shows a series of vertical lines (stems) at each integer value of 'n', all maintaining the same amplitude, indicating a flat line with no oscillation.

The overall behavior of the graph is a straight line parallel to the x-axis, showing no periodicity or variation in amplitude across the samples. Since the frequency is zero, there are no peaks, valleys, or oscillations present in this signal. The key feature of this plot is its constancy, representing a signal with no frequency content.
image_name:(b)
description:The graph labeled (b) is a discrete-time sinusoidal signal plot. The x-axis represents the sample number \( n \) and the y-axis represents the amplitude \( x(n) \). The sinusoidal signal is sampled at \( \pi/8 \) radians per sample, which corresponds to \( 1/16 \) cycles per sample.

Type of Graph and Function:
This is a discrete-time plot of a sinusoidal waveform, showing the sampled points of the signal.

Axes Labels and Units:
- **X-axis:** Sample number \( n \)
- **Y-axis:** Amplitude \( x(n) \)
- The frequency is given as \( \pi/8 \) rad/sample, equivalent to \( 1/16 \) cycles/sample.

Overall Behavior and Trends:
The graph shows a sinusoidal waveform sampled at discrete intervals. The waveform starts at a positive amplitude and decreases to zero, then to negative values, and back to zero, repeating this pattern. The overall shape is consistent with a sinusoidal function.

Key Features and Technical Details:
- The signal is periodic, repeating every 16 samples, which corresponds to the frequency of the waveform.
- The peaks and valleys are not explicitly marked, but the signal oscillates between positive and negative amplitudes.
- There are zero crossings approximately halfway between the peaks and valleys.

Annotations and Specific Data Points:
- The frequency annotation indicates \( \pi/8 \) rad/sample, providing a clear understanding of the sampling rate and frequency of the sinusoid.

This graph illustrates the sampled nature of sinusoidal signals in discrete-time signal processing, emphasizing the periodicity and sampling frequency.
image_name:(c)
description:**Type of Graph and Function:**
The graph (c) is a discrete-time sinusoidal signal plot, showing samples of a sinusoidal waveform.

**Axes Labels and Units:**
- The horizontal axis is labeled as \( n \), representing discrete time samples.
- The vertical axis is labeled as \( x(n) \), representing the amplitude of the signal.
- The frequency of the signal is given as \( \pi/4 \) rad/sample, equivalent to 1/8 cycles/sample.

**Overall Behavior and Trends:**
The graph displays a sinusoidal pattern, with peaks and troughs following a consistent wave-like pattern. The signal oscillates symmetrically around the horizontal axis, indicating a zero mean value. The discrete nature of the signal is evident from the individual sample points plotted on the waveform.

**Key Features and Technical Details:**
- The wave completes one full cycle every 8 samples, as indicated by the frequency of 1/8 cycles/sample.
- The signal has a periodic nature, with clear peaks and troughs visible at regular intervals.
- The dashed line represents the continuous-time equivalent of the sampled signal, showing the underlying sinusoidal waveform.

**Annotations and Specific Data Points:**
- The graph includes dashed lines to illustrate the continuous waveform that the discrete samples represent.
- Key points such as maxima and minima occur at regular intervals, aligning with the periodicity of the sinusoidal signal.
image_name:(d)
description:Graph (d) is a discrete-time sinusoidal signal plot. The horizontal axis represents the sample index \( n \), while the vertical axis represents the amplitude \( x(n) \). The graph is labeled with a frequency of \( \pi/2 \) rad/sample, which corresponds to \( 1/4 \) cycles per sample. This indicates that the signal completes a full cycle every 4 samples.

The plot shows a series of impulses (vertical lines) at regular intervals, specifically at every fourth sample (e.g., at \( n = 1, 5, 9, 13, \) etc.). The amplitude of the signal is consistent across these samples, suggesting a constant magnitude.

The overall behavior of the graph is periodic, with a clear repetition every 4 samples, consistent with the given frequency. There are no annotations or additional markers on this plot, and it lacks any visible gridlines or numerical values aside from the axis labels and frequency information. This graph likely serves to illustrate the concept of a discrete-time sinusoidal signal at a specific frequency.

Fig. 13.4 Some discrete-time sinusoidal signals.
image_name:x_2(n)
description:The graph labeled "x_2(n)" is a discrete-time sinusoidal signal representation. It is part of a larger diagram that compares time and frequency domains for different sampling rates, focusing on downsampling and upsampling processes.

Type of Graph and Function:
This is a time-domain waveform graph, showing discrete-time samples of a sinusoidal signal. It is accompanied by its frequency domain representation, illustrating the effects of downsampling.

Axes Labels and Units:
- **Time Domain (left side):**
- The horizontal axis is labeled "n" representing discrete time samples.
- The vertical axis represents the amplitude of the signal, though specific units are not provided.

- **Frequency Domain (right side):**
- The horizontal axis is labeled "f" (frequency) and "ω" (angular frequency), showing frequency in Hertz (Hz) and angular frequency in radians per second (π units).
- The vertical axis represents the amplitude of the frequency components.

Overall Behavior and Trends:
- **Time Domain:**
- The signal "x_2(n)" is shown as discrete vertical lines, indicating sampled values of a sinusoidal waveform. The waveform is periodic, with visible oscillations.
- The graph suggests a regular pattern in the sampling, with samples taken at specific intervals.

- **Frequency Domain:**
- The frequency representation "X_2(f), X_2(ω)" shows multiple spikes at different frequencies, indicating the presence of harmonics or aliased components due to downsampling.
- Peaks are visible at 1 Hz, 12 Hz, and 24 Hz, corresponding to angular frequencies π, 2π, and 4π radians per second.

Key Features and Technical Details:
- The time-domain signal indicates a periodic sinusoidal waveform sampled at regular intervals.
- The frequency domain spikes suggest the presence of aliased components, a common occurrence in downsampled signals.

Annotations and Specific Data Points:
- No specific numerical values or annotations are provided for individual samples or frequency components aside from the labeled frequencies.
- The graph does not include gridlines or additional markers, focusing primarily on illustrating the concept of discrete-time sampling and its frequency implications.
image_name:x_c(t)
description:The graph labeled "x_c(t)" is part of a composite diagram illustrating discrete-time sinusoidal signals and their corresponding frequency spectra.

1. **Type of Graph and Function**:
- The graph is a time-domain representation of a continuous-time signal, showing how discrete samples approximate the continuous waveform.

2. **Axes Labels and Units**:
- The horizontal axis represents time \( t \), with specific sample points marked (e.g., 0.25, 0.5).
- The vertical axis represents amplitude, but no specific units are given.
- The graph is linear, with no gridlines or specific numerical values aside from sample points.

3. **Overall Behavior and Trends**:
- The graph shows a sinusoidal waveform with discrete samples marked along the curve. The waveform appears periodic, with a smooth sinusoidal shape.
- Discrete samples are depicted as vertical lines intersecting the sinusoidal curve at specific points, indicating the sampled values.

4. **Key Features and Technical Details**:
- The sinusoidal waveform is smoothly oscillating, with peaks and valleys corresponding to the maxima and minima of the sine wave.
- The discrete samples do not cover every point of the continuous wave, highlighting the concept of sampling.

5. **Annotations and Specific Data Points**:
- The graph includes labels such as \( x_c(t) \), \( \tau x_{s2}(t) \), indicating different representations or transformations of the signal.
- Specific points on the time axis are labeled (e.g., 0.25, 0.5), which may correspond to specific sampling instances or periods.

Overall, the graph serves to illustrate the concept of sampling a continuous-time sinusoidal signal and how these samples represent the original waveform in discrete-time signal processing.
image_name:X_s(f), X(ω)
description:The image contains two sets of diagrams, each with time-domain and frequency-domain representations, illustrating concepts of discrete-time signal processing involving downsampling and upsampling.

Top Row:
1. **Time-Domain Representation:**
- **Signal:** Labeled as \( x_2(n) \), it is a discrete-time signal with samples shown as vertical lines.
- **Continuous-Time Representation:** Labeled as \( x_c(t) \), depicted with a dashed line representing the underlying continuous signal.
- **Upsampled Signal:** Labeled as \( \tau x_{s2}(t) \), showing an increased number of samples compared to \( x_2(n) \).
- **Axis:** The horizontal axis is time \( t \) (n), with marked intervals at 0.25 and 0.5.

2. **Frequency-Domain Representation:**
- **Fourier Transform:** Labeled as \( X_s(f), X(\omega) \), showing a series of triangular shapes at frequencies 1 Hz (0.5\( \pi \)), 4 Hz (2\( \pi \)), and 8 Hz (4\( \pi \)).
- **Axis:** The horizontal axis is frequency \( f \) (\( \omega \)), indicating the periodic nature of the signal in frequency.

Bottom Row:
1. **Time-Domain Representation:**
- **Signal:** Labeled as \( x(n) \), a discrete-time signal with more samples than \( x_2(n) \).
- **Continuous-Time Representation:** Labeled as \( x_c(t) \), again shown with a dashed line.
- **Downsampled Signal:** Labeled as \( \tau x_s(t) \), indicating fewer samples compared to \( x(n) \).
- **Axis:** The horizontal axis is time \( t \) (n), with marked intervals extending to 0.5.

2. **Frequency-Domain Representation:**
- **Fourier Transform:** Labeled as \( X_{s2}(f), X_2(\omega) \), with triangular patterns at 1 Hz (\( \pi/6 \)), 12 Hz (2\( \pi \)), and 24 Hz (4\( \pi \)).
- **Axis:** The horizontal axis is frequency \( f \) (\( \omega \)), showing higher frequency components than the top diagram.

Key Features:
- The diagrams emphasize the relationships between time and frequency domains in the context of sampling.
- The top set illustrates upsampling, while the bottom set shows downsampling.
- Frequency components are periodic, with distinct peaks at specified frequencies, demonstrating aliasing and signal representation concepts in discrete-time processing.
image_name:X_s2(f), X_2(ω)
description:The diagram consists of two parts, each showing a time-domain representation and a frequency-domain representation of discrete-time signals.

Upper Part:
- **Time-Domain Representation:**
- The signal is represented by discrete vertical lines at intervals, labeled as \( x_2(n) \). The continuous curve \( x_c(t) \) represents the continuous-time version of the signal. The dashed line \( \tau x_{s2}(t) \) indicates a sampled version of the signal.
- The discrete points are positioned at specific time intervals marked as 0.25 and 0.5, with numerical indices (1) and (2).

- **Frequency-Domain Representation:**
- The spectrum is labeled as \( X_s(f), X(\omega) \), showing triangular patterns at specific frequencies.
- Peaks occur at 1 Hz (0.5\( \pi \)), 4 Hz (2\( \pi \)), and 8 Hz (4\( \pi \)).
- This indicates a periodic repetition in the frequency domain.

Lower Part:
- **Time-Domain Representation:**
- This part shows a denser set of discrete vertical lines labeled as \( x(n) \), with a continuous curve \( x_c(t) \) and a dashed line \( \tau x_s(t) \) representing another sampled version.
- The points are marked at intervals 0.25 and 0.5, with numerical indices (3) and (6).

- **Frequency-Domain Representation:**
- The spectrum, labeled as \( X_{s2}(f), X_2(\omega) \), shows narrower triangular shapes.
- Peaks are located at 1 Hz (\( \pi/6 \)), 12 Hz (2\( \pi \)), and 24 Hz (4\( \pi \)).
- This suggests a different sampling rate or process compared to the upper part.

General Observations:
- The graph illustrates the concepts of sampling in both time and frequency domains, highlighting how different sampling rates affect the frequency spectrum.
- The absence of gridlines or numerical annotations beyond frequency labels suggests a focus on conceptual understanding rather than precise measurements.

Fig. 13.5 Comparing time and frequency of two sampling rates.

## 13.4 DOWNSAMPLING AND UPSAMPLING

Two important operations in discrete-time signal processing are downsampling and upsampling. Downsampling is used to reduce the sample rate, and hence the amount of information that must be processed and/or stored, hopefully without information loss. Upsampling is used to increase the sample rate. Although noninteger downsampling and upsampling rates can be achieved, here we consider only the case in which $L$ is an integer value.

Downsampling is achieved by keeping every Lth sample and discarding the others. As Fig. 13.6 shows, the result of downsampling is to expand the original spectra by L. Thus, to avoid digital aliasing, the spectrum of the original signal must be band limited to $\pi / \mathrm{L}$ before downsampling is done. In other words, the signal must be sampled $L$ times above its minimum sampling

Key Point: To avoid aliasing when downsampling by a factor L, the original signal must be sampled at L times the Nyquist rate.
rate so that no information is lost during downsampling.

Upsampling is accomplished by inserting $L-1$ zero values between each pair of consecutive samples, as shown in Fig. 13.7. In this case, one can show that the spectrum of the resulting upsampled signal is identical to that of the original signal but with a renormalization along the frequency axis. Specifically, when a signal is upsampled by $L$, the frequency axis is scaled by $L$ such that $2 \pi$ now occurs where $L 2 \pi$ occurred in the original signal and $L$ identical copies of the original spectrum are now squeezed within the range 0 to $2 \pi$. This operation

Key Point: Upsampling by $L$ results in a renormalization along the frequency axis so that $L$ copies of the original signal spectrum are now squeezed in the range 0 to $2 \pi$.
is useful when one wishes to increase the effective sampling rate of a signal, particularly if postfiltering is then applied.

Follow the next two examples carefully-they help explain the spectral changes due to downsampling and upsampling.

#### EXAMPLE 13.2

The signal $\mathrm{x}_{2}(n)$ in Example 13.1 is to be downsampled by $L=3$. Find the new spectrum, $X_{3}(\omega)$, when every third sample is kept and the others are discarded. In other words, if the original series of numbers is $\mathrm{x}_{1}, \mathrm{x}_{2}, \mathrm{x}_{3}, \mathrm{x}_{4}, \ldots$, the new series is $\mathrm{x}_{1}, \mathrm{x}_{4}, \mathrm{x}_{7}, \mathrm{x}_{10}, \ldots$
image_name:(a)
description:The system block diagram labeled "(a)" illustrates the process of downsampling by a factor of 4, shown both in the time domain and frequency domain.

1. **Main Components:**
- **Input Signal:** The time domain representation on the left shows a discrete signal with samples at regular intervals. This is depicted as a sinusoidal waveform with discrete sample points.
- **Downsampling Block:** A block labeled with a downward arrow and "L=4" indicates the downsampling operation. This block reduces the sampling rate by keeping every fourth sample and discarding the others.
- **Output Signal:** The resulting downsampled signal is shown on the right in the time domain, with fewer sample points. The waveform is now reconstructed with a larger interval between samples, reflecting the downsampling by a factor of 4.

2. **Flow of Information:**
- The input signal flows into the downsampling block, where it undergoes the reduction in sampling rate. The output from the block is the downsampled signal.
- The arrows indicate the direction of signal flow from input to output.

3. **Labels and Annotations:**
- The time domain is labeled with "n" for discrete time indices.
- "L = 4" indicates the downsampling factor.
- The frequency domain is labeled with "ω" representing angular frequency.

4. **Frequency Domain Representation:**
- Below the time domain diagrams, the corresponding frequency domain representations are shown.
- The original spectrum on the left shows two peaks at specific frequencies. After downsampling, the spectrum on the right shows the effect of aliasing, with repeated frequency components appearing due to the reduced sampling rate.

5. **Overall System Function:**
- The primary function of this system is to reduce the sampling rate of a discrete-time signal by a factor of 4. This involves retaining every fourth sample and discarding the others, which affects both the time domain representation and introduces aliasing in the frequency domain. The diagram effectively illustrates the changes in both domains due to downsampling.
image_name:(b)
description:The graph labeled (b) is a frequency domain representation of a signal that has been downsampled. This is a spectral diagram showing the effect of downsampling by a factor of 4 on the signal's spectrum.

1. **Type of Graph and Function:**
- This is a frequency domain graph, representing the spectrum of a signal after downsampling.

2. **Axes Labels and Units:**
- The horizontal axis is labeled with the angular frequency $\omega$, measured in radians per second. Key points are marked at $0$, $\frac{4\pi}{6}$, and $2\pi$.
- The vertical axis represents the amplitude of the frequency components, but it is not labeled with specific units.

3. **Overall Behavior and Trends:**
- The spectrum is characterized by a periodic triangular shape. There are repeating peaks and valleys across the frequency range.
- The peaks occur at multiples of $\frac{4\pi}{6}$, indicating the periodicity introduced by the downsampling process.

4. **Key Features and Technical Details:**
- The spectrum shows a mirrored triangular pattern about the vertical axis, suggesting symmetrical frequency components.
- The first peak is centered at $\omega = 0$, and subsequent peaks appear at intervals of $\frac{4\pi}{6}$.
- The shape of the spectrum suggests aliasing effects due to the downsampling, which typically introduces periodic replication of the original spectrum.

5. **Annotations and Specific Data Points:**
- The graph does not include numerical values for the amplitude, but the key frequency points are clearly marked, providing a reference for interpreting the spectral replication due to downsampling.

Fig. 13.6 Downsampling by 4: (a) time domain, and (b) frequency domain.
image_name:(a)
description:The system block diagram labeled "(a)" illustrates the process of upsampling by a factor of 4. It consists of two main sections: the time domain representation and the frequency domain representation.

Main Components:
1. **Time Domain Representation:**
- **Input Signal (Left Graph):** This graph shows a discrete-time signal with samples at intervals of 1. The waveform is depicted with a dashed line to indicate its continuous nature, and the discrete samples are shown as vertical lines at specific points (0, 1, 2, etc.).
- **Upsampling Block:** This is represented by a block with an upward arrow labeled "L" with "L = 4". This block is responsible for increasing the sample rate by inserting zeros between the original samples.
- **Output Signal (Right Graph):** The output of the upsampling block is shown with samples now spaced at intervals of 4, reflecting the increased sample rate.

2. **Frequency Domain Representation:**
- **Input Spectrum (Left Graph):** The spectrum of the original signal is shown with a triangular waveform, indicating the frequency content before upsampling. The key frequency point is marked at \( \frac{4\pi}{6} \).
- **Output Spectrum (Right Graph):** After upsampling, the spectrum shows periodic replication, with the main components now appearing at intervals of \( \frac{\pi}{6} \), \( \pi \), and \( 2\pi \). This illustrates the effect of upsampling on the frequency domain, where the spectral components are repeated due to the insertion of zeros.

Flow of Information or Control:
- **Signal Flow:** The discrete-time signal flows from the input graph through the upsampling block, where the sample rate is increased, and then to the output graph, showing the effect in the time domain.
- **Frequency Transformation:** The frequency domain transformation is shown separately, indicating how the spectrum changes as a result of upsampling.

Labels, Annotations, and Key Indicators:
- The upsampling factor is clearly labeled as "L = 4."
- Frequency points are marked on the frequency domain graphs to indicate the spectral replication.

Overall System Function:
The primary function of this system is to increase the sample rate of a discrete-time signal by a factor of 4. This is achieved by inserting zeros between samples in the time domain and results in a replicated spectrum in the frequency domain. The diagram effectively demonstrates both the time domain and frequency domain effects of the upsampling process.
image_name:(b)
description:The graph labeled "(b)" is a frequency domain representation of a signal after upsampling by a factor of 4. This type of graph is typically used to show how the frequency content of a signal is affected by the upsampling process.

1. **Type of Graph and Function:**
- This is a frequency domain graph, specifically a spectral plot showing the effects of upsampling.

2. **Axes Labels and Units:**
- The horizontal axis is labeled with the angular frequency \( \omega \) and measures in radians per second. Key frequencies are marked at \( \frac{\pi}{6} \), \( \pi \), and \( 2\pi \).
- The vertical axis represents amplitude, but specific numerical values are not provided.

3. **Overall Behavior and Trends:**
- The graph shows periodic replication of the original spectrum due to the upsampling process. There are repeated triangular shapes that extend along the frequency axis.
- The triangular spectral shapes indicate that the original frequency content is being replicated at intervals determined by the upsampling factor.

4. **Key Features and Technical Details:**
- Peaks of the triangular shapes are aligned at multiples of \( \frac{\pi}{6} \), which corresponds to the upsampling factor of 4.
- The graph suggests that the upsampling introduces additional spectral components, resulting in a denser frequency spectrum.

5. **Annotations and Specific Data Points:**
- While numerical amplitude values are not given, the key frequency points are clearly marked, allowing for analysis of spectral replication and potential aliasing effects.

Fig. 13.7 Upsampling by 4: (a) time domain, and (b) frequency domain.

#### Solution

Clearly the solution here is that the new sequence is equivalent to $x(n)$ in Example 13.1, and thus its spectrum is simply $X_{3}(\omega)=X(\omega)$.

Note that no information was lost in this example because the initial images of the signal $x_{2}(n)$ were far enough apart. However, if the downsampling operation results in the spectra overlapping one another, then an aliasing phenomenon occurs that is similar to that which occurs when sampling an analog signal lower than the Nyquist rate. In fact, it can be shown that, to avoid any aliasing during downsampling by the factor $L$, the original signal should be band limited to $\pi / \mathrm{L}$.

#### EXAMPLE 13.3

As an example of upsampling of the signal $x(n)$ in Example 13.1, find the new spectrum, $X_{4}(\omega)$, if two zeros are inserted between each sample (i.e., if we upsample by $L=3$ ). In other words, if the original series of numbers was $\mathrm{x}(\mathrm{n})=\mathrm{x}_{1}, \mathrm{x}_{2}, \mathrm{x}_{3}, \ldots$ and had a spectrum $X(\omega)$, then the new series of numbers is now $x_{4}(n)=\left(x_{1}, 0,0, x_{2}, 0,0, x_{3}, \ldots\right)$ and has a spectrum $X_{4}(\omega)$.

#### Solution

Perhaps the simplest way to conceptualize the insertion of these extra 0 samples in a series is to look at $X_{s 4}(\mathrm{f})$ in time and frequency when we let $f_{s 4}=12 \mathrm{~Hz}$. Recall that $x_{s 4}(t)$ is defined for all time, where it is zero between its impulses, and the Laplace transform is used to observe its frequency response. With such a sampling frequency, we note that $x_{s 4}(t)$ is equal to the signal $x_{s}(t)$, and thus $X_{s 4}(f)=X_{s}(f)$. To find $X_{4}(\omega)$, recall that it is simply a frequency normalization of $X_{s 4}(f)$, where the sampling frequency is normalized to $2 \pi$. In other words, the series $\mathbf{x}(\mathrm{n})$ is simply a normalization of the time between impulses to 1 . However, by inserting extra zeros between samples, the normalization is effectively being done for a time period smaller than that between nonzero impulses. Thus, the images remain the same while the normalization along the frequency axis is different.

In this example, since two zeros are inserted, the effective sampling rate might be thought of as 12 Hz , but now the images at 4 Hz and 8 Hz remain in contrast to $\mathrm{X}_{2}(\omega)$ in Example 13.1. The resulting signals are shown in Fig. 13.8.

Finally, note that if signal processing is used on the samples $x_{4}(n)$ to eliminate the two images at $(2 \pi) / 3$ and $(4 \pi) / 3$, then the resulting signal will equal $\mathrm{x}_{2}(\mathrm{n})$. In other words, as long as an analog signal is originally sampled higher than the Nyquist rate, we can use upsampling and digital-signal processing to derive signals that are the same as if the analog signal were sampled at a much higher rate.
image_name:Fig. 13.8
description:The graph in Fig. 13.8 consists of two main components: a time-domain representation and a frequency-domain spectrum of a discrete-time signal that has been upsampled by a factor of 3.

Time-Domain Representation:
- **Type of Graph:** The top part of the graph is a time-domain waveform.
- **Axes Labels and Units:**
- **Horizontal Axis (Time):** Labeled as 't (seconds)' with discrete points marked as 'n'. Specific time markers are at 0.25 and 0.5 seconds, corresponding to sample numbers 3 and 6.
- **Vertical Axis:** Represents signal amplitude, though units are not specified.
- **Overall Behavior and Trends:**
- The signal $x_c(t)$ is shown as a continuous line with a sinusoidal shape.
- Discrete samples of $x_4(n)$ are shown as vertical lines at specific time intervals, indicating sampled values of the continuous signal.
- The sampled signal maintains the general shape of the continuous signal but only at discrete intervals.
- **Key Features and Technical Details:**
- The sampled points are equally spaced, indicating uniform sampling.
- The relationship between the sampled signal $x_4(n)$ and the continuous signal $x_c(t)$ is highlighted with annotations.

Frequency-Domain Spectrum:
- **Type of Graph:** The bottom part of the graph is a frequency-domain spectrum.
- **Axes Labels and Units:**
- **Horizontal Axis (Frequency):** Labeled as 'f' and 'ω', with frequency values marked in both hertz and radians per second.
- **Vertical Axis:** Represents the amplitude of the frequency components, labeled as $X_{s4}(f), X_4(ω)$.
- **Overall Behavior and Trends:**
- The spectrum shows repeated triangular peaks at intervals of 3 Hz, starting at 1 Hz and continuing at 4 Hz, 8 Hz, 12 Hz, and 16 Hz.
- The peaks represent the frequency components of the upsampled signal.
- **Key Features and Technical Details:**
- The spectrum indicates aliasing, with images at $(2\pi)/3$ and $(4\pi)/3$ as noted in the context.
- The frequency axis is marked with both linear frequency (Hz) and angular frequency (radians), showing the conversion between the two.

Annotations and Specific Data Points:
- The graph includes annotations indicating the relationship between sampled and continuous signals, as well as the positions of key frequency components in the spectrum.
- The context notes that signal processing can remove images at $(2\pi)/3$ and $(4\pi)/3$, which would result in the signal matching $x_2(n)$.

This graph illustrates the effects of upsampling on both the time-domain and frequency-domain representations of a discrete-time signal.

Fig. 13.8 Spectrum of a discrete-time signal upsampled by 3.

## 13.5 DISCRETE-TIME FILTERS

Thus far, we have seen the relationship between continuous-time and discrete-time signals in the time and frequency domain. However, often one wishes to perform filtering on a discrete-time signal to produce another discrete-time signal. In other words, an input series of numbers is applied to a discrete-time filter to create an output series of numbers. This filtering of discrete-time signals is most easily visualized with the shorthand notation of z-transforms.

Consider the system shown in Fig. 13.9, where the output signal is defined to be the impulse response, $h(\mathrm{n})$, when the input, $u(n)$, is an impulse (i.e., 1 for $\mathrm{n}=0$ and 0 otherwise). The transfer function of the filter is said to be given by $\mathrm{H}(\mathrm{z})$, which is the $z$-transform of the impulse response, $h(n)$.

### 13.5.1 Frequency Response of Discrete-Time Filters

The transfer functions for discrete-time filters appear similar to those for continuous-time filters; practical integrated circuit discrete-time transfer functions are represented by rational transfer functions except that, instead of polynomials in s , polynomials in $\mathbf{z}$ are obtained. For example, the transfer function of a low-pass, continuoustime filter, $\mathrm{H}_{\mathrm{c}}(\mathrm{s})$, might appear as

$$
\begin{equation*}
H_{c}(s)=\frac{4}{s^{2}+2 s+4} \tag{13.18}
\end{equation*}
$$

The poles for this filter are determined by finding the roots of the denominator polynomial, which are $-1.0 \pm 1.7321 \mathrm{j}$ for this example. This continuous-time filter is also defined to have two zeros at $\infty$ since the
image_name:Fig. 13.9 Discrete-time filter system
description:The system block diagram labeled "Fig. 13.9 Discrete-time filter system" consists of a single block representing a discrete-time filter with a transfer function denoted as \( H(z) \). This block is the central component of the system and is responsible for processing input signals.

1. **Main Components:**
- **Filter Block \( H(z) \):** This is the primary component of the system, representing the transfer function of the discrete-time filter. It processes the input signal \( u(n) \) to produce the output signal \( y(n) \).

2. **Flow of Information:**
- The input signal \( u(n) \) enters the system from the left and is fed into the filter block \( H(z) \).
- The processed output signal \( y(n) \) exits the system from the right of the filter block.
- The flow of information is unidirectional, from the input to the output through the filter block.

3. **Labels, Annotations, and Key Indicators:**
- The input is labeled as \( u(n) \), and the output is labeled as \( y(n) \), indicating their roles as the input and output signals, respectively.
- The filter block is labeled \( H(z) \), indicating its function as a discrete-time filter characterized by the transfer function \( H(z) \).

4. **Overall System Function:**
- The primary function of this system is to filter the input signal \( u(n) \) using the transfer function \( H(z) \), resulting in the output signal \( y(n) \). This setup is typical for digital signal processing applications where specific frequency components of the input signal are modified or extracted by the filter.

(Discrete-time filter)
( $y(n)$ equals $h(n)$ if $u(n)$ is an impulse)
Fig. 13.9 Discrete-time filter system.
image_name:(a)
description:The graph labeled as "(a)" is a pole-zero plot on the s-plane, which is used to represent the poles of a continuous-time transfer function \( H_c(s) \). This type of graph is essential in analyzing the stability and frequency response of a system.

1. **Type of Graph and Function:**
- This is a pole-zero plot on the s-plane, commonly used in control systems and signal processing to analyze continuous-time systems.

2. **Axes Labels and Units:**
- The horizontal axis represents the real part of the complex frequency \( s \), and the vertical axis represents the imaginary part, denoted as \( j\omega \).
- No specific units are provided on the axes, as this is a general representation of the complex plane.

3. **Overall Behavior and Trends:**
- The graph shows two poles marked by crosses (\( \times \)) on the imaginary axis. This indicates that the system has oscillatory behavior without damping, as the poles are purely imaginary.
- The poles are symmetrically placed about the origin, suggesting a balanced frequency response.

4. **Key Features and Technical Details:**
- The poles are located on the imaginary axis, which implies that the system is marginally stable and will exhibit sustained oscillations at the frequency corresponding to the imaginary part of the pole location.
- The high frequency is indicated by \( j\omega = \infty \) at the top of the imaginary axis, and DC (direct current) is indicated by \( j\omega = 0 \) at the origin.

5. **Annotations and Specific Data Points:**
- There are no specific numerical values or additional annotations provided, but the concept of high frequency and DC is clearly marked on the graph.

This pole-zero plot is fundamental for understanding the frequency response characteristics of a continuous-time system and predicting its behavior in response to various inputs.
image_name:(b)
description:The graph labeled (b) is a pole-zero plot on the z-plane, which is used to analyze digital filters in discrete-time systems. This plot is crucial for understanding the stability and frequency response of the system.

Type of Graph and Function:
- The graph is a pole-zero plot on the z-plane.
- It represents the frequency response of a discrete-time system.

Axes Labels and Units:
- The horizontal axis is the real axis of the z-plane, ranging from -1 to 1.
- The vertical axis is the imaginary axis of the z-plane, ranging from -j to j.
- The plot is represented on a unit circle, which is a common approach in z-plane analysis, where the radius equals 1.

Overall Behavior and Trends:
- The graph shows the unit circle, which is significant in evaluating the stability and frequency response of the filter.
- The frequency response is evaluated by examining the positions of poles and zeros in relation to the unit circle.

Key Features and Technical Details:
- The unit circle is marked with specific frequency points:
- ω = 0 at (1, 0)
- ω = π/2 at (0, j)
- ω = π at (-1, 0)
- ω = 3π/2 at (0, -j)
- ω = 2π at (1, 0) again, completing the circle.
- There are two poles marked on the plot, which are crucial for determining the system's behavior.
- The poles are located near the unit circle, indicating potential resonance frequencies or stability considerations.

Annotations and Specific Data Points:
- The plot includes annotations for key frequency points around the unit circle.
- The positions of poles are marked with 'X', which are critical in analyzing the system's stability and response.
- The circle and axes are bolded to emphasize the unit circle's importance in the analysis.

This pole-zero plot provides insight into the system's stability and frequency characteristics by examining the location of poles and zeros in relation to the unit circle on the z-plane.

Fig. 13.10 Transfer function response. (a) Continuous-time, and (b) discrete-time.
denominator polynomial is two orders higher than the numerator polynomial. To find the frequency response of $H_{c}(s)$, it is evaluated along the $j \omega$ axis by substituting $s=j \omega$. The poles and zeros are plotted on the $s$-plane in Fig. 13.10(a), and the magnitude and phase response $\mathrm{H}_{\mathrm{c}}(\mathrm{j} \omega)$ can be found in terms of the magnitude and phase of vectors from all poles (and finite zeros) to the point $s=j \omega$ along the frequency-axis.

$$
\begin{gather*}
\left.\mid \mathrm{H}_{\mathrm{c}} \mathrm{j} \omega\right) \left\lvert\,=\frac{4}{|\mathrm{j} \omega+1.0+1.7321 \mathrm{j}||\mathrm{j} \omega+1.0-1.7321 \mathrm{j}|}\right.  \tag{13.19}\\
\angle \mathrm{H}_{\mathrm{c}}(\mathrm{j} \omega)=-\angle(\mathrm{j} \omega+1.0+1.7321 \mathrm{j})-\angle(\mathrm{j} \omega+1.0-1.7321 \mathrm{j}) \tag{13.20}
\end{gather*}
$$

An example of a discrete-time, low-pass transfer function is given by the following equation:

$$
\begin{equation*}
H(z)=\frac{0.05}{z^{2}-1.6 z+0.65} \tag{13.21}
\end{equation*}
$$

Key Point: The frequency response of a discrete-time filter $H(z)$ is found by evaluating its magnitude and phase on the unit circle, or graphically by considering the magnitude and phase of vectors connecting its poles and zeros to points around the unit circle.

The poles of $H(z)$ occur at $0.8 \pm 0.1 \mathrm{j}$ in the $z$-plane, and two zeros are again at $\infty$. To find the frequency response of $\mathrm{H}(\mathrm{z})$, we evaluate it around the unit circle contour $\mathbf{Z}=\mathrm{e}^{\mathrm{j} \omega}$ as shown in Fig. 13.10(b), instead of going along the vertical $\mathrm{j} \omega$ axis as in the s-plane. Note that substituting $z=\mathrm{e}^{\mathrm{j} \omega}$ in the z domain transfer function, $H(z)$, is simply a result of substituting $s=j \omega$ into (13.14), where T has been normalized to 1, as discussed in Section 13.3. The discrete-time frequency response can be found graphically by considering the magnitude and phase of vectors from each pole and zero of $\mathrm{H}(\mathrm{z})$ as shown in Fig. $13.10(b)$ to the corresponding frequency on the unit circle $z=e^{j \omega}$.

Poles or zeros occurring at $z=0$ do not affect the magnitude response $\mathrm{H}(\mathrm{z})$ since a vector from the origin to the unit circle always has a length of unity. However, they do affect the phase response.

In discrete time, $\mathrm{H}(\mathrm{z}=1)$ corresponds to the frequency response at

Key Point: In discrete-time, the point $z=1$ corresponds both to dc and to signals at the sampling frequency. The frequency response is periodic, and for rational transfer functions with real-valued coefficients exhibits conjugate symmetry around dc. Hence, discrete-time frequency responses need only be plotted from dc to half the sample rate, $\pi$.
both dc (i.e., $\omega=0$ ) and at $\omega=2 \pi$. Also, the time normalization of setting T to unity implies that $\omega=2 \pi$ is equivalent to the samplingrate speed (i.e., $f=f_{s}$ ) for $X_{s}(f)$. In addition, note that the frequency response of a filter need be plotted only for $0 \leq \omega \leq \pi$ (i.e., $0 \leq \omega \leq f_{s} / 2$ ) since, for filters with real coefficients, the poles and zeros always occur in complex-conjugate pairs (or on the real axis), so the magnitude response of the filter is equal to that for $\pi \leq \omega \leq 2 \pi$ (the filter's phase is antisymmetric). Going around the circle again gives the same result as the first time, implying that the frequency response repeats every $2 \pi$.

Before we leave this section, a word of caution is in order. To simplify notation, the same variables, $f$ and $\omega$, are used in both the continuous-time and discrete-time domains in Fig. 13.10. However, these variables are not equal in the two domains, and care should be taken not to confuse values from the two domains. The continuous-time domain is used here for illustrative reasons only since the reader should already be quite familiar with transfer function analysis in the s -domain. In summary, the unit circle, $\mathrm{e}^{\mathrm{j} \omega}$, is used to determine the frequency response of a system that has its input and output as a series of numbers, whereas the $\mathrm{j} \omega$-axis is used for a system that has continuous-time inputs and outputs. However, $\omega$ is different for the two domains.

#### EXAMPLE 13.4

Assuming a sample rate of $f_{s}=100 \mathrm{kHz}$, find the magnitude of the transfer function in (13.21) for 0 Hz , $100 \mathrm{~Hz}, 1 \mathrm{kHz}, 10 \mathrm{kHz}, 50 \mathrm{kHz}, 90 \mathrm{kHz}$, and 100 kHz .

#### Solution

To find the magnitude of $\mathrm{H}(\mathrm{z})$ at these frequencies, first we find their equivalent $\mathbf{z}$-domain locations by normalizing $f_{s}$ to $2 \pi$. Next, we find the gain of $H(z)$ by putting these $z$-domain values into (13.21) and finding the magnitude of the resulting complex value. Table 13.1 summarizes the results.

Note that the gain of $\mathrm{H}(\mathrm{z})$ is the same at both 0 Hz and 100 kHz , as expected, since their z-plane locations are the same. Also, the gain is the same at both 10 kHz and 90 kHz since their z-plane locations are complex conjugates of each other. Finally, note that the minimum gain for this transfer function occurs at $\mathbf{z}=-1$, or equivalently, $\mathrm{f}_{\mathrm{s}} / 2=50 \mathrm{kHz}$.

#### EXAMPLE 13.5

Consider a first-order $\mathrm{H}(\mathrm{z})$ having its zero at $\infty$ and its pole on the real axis, where $0<\mathrm{a}<1$. Mathematically, the transfer function is represented by $H(z)=b /(z-a)$. Find the value of $\omega$, where the magnitude of $H(z)$ is $3 d B$ lower than its dc value. What is the $3-\mathrm{dB}$ value of $\omega$ for a real pole at 0.8 ? What fraction of the sampling rate, $\mathrm{f}_{\mathrm{s}}$, does it correspond to?

Table 13.1 Finding the gain of $\mathrm{H}(\mathrm{z})$ at some example frequencies.

|  | $\mathbf{z - p l a n e}$ locations |  |  |
| :---: | :--- | :---: | :--- |
| Frequency <br> $(\mathbf{k H z})$ | $\mathbf{e}^{\mathrm{j} \omega}$ | $\mathbf{z}=\mathbf{x}+\mathbf{j} \mathbf{y}$ |  |
| 0 | $\mathrm{e}^{\mathrm{j} 0}$ | $1.0+\mathrm{j} 0.0$ | 1.0 |
| 0.1 | $\mathrm{e}^{\mathrm{j} 0.002 \pi}$ | $0.9999803+\mathrm{z} 0.00628314$ | 0.9997 |
| 1 | $\mathrm{e}^{\mathrm{j} 0.02 i}$ | $0.9980267+\mathrm{j} 0.06279052$ | 0.968 |
| 10 | $\mathrm{e}^{\mathrm{j} 0.2 \pi}$ | $0.809+\mathrm{j} 0.5878$ | 0.149 |
| 50 | $\mathrm{e}^{\mathrm{j} \pi}$ | $-1.0+\mathrm{j} 0.0$ | 0.0154 |
| 90 | $\mathrm{e}^{\mathrm{j} 1.8 \pi}$ | $0.809-\mathrm{j} 0.5878$ | 0.149 |
| 100 | $\mathrm{e}^{\mathrm{j} 2 \pi}$ | $1.0+\mathrm{j} 0.0$ | 1.0 |

image_name:Fig. 13.11 Pole-zero plot
description:This is a pole-zero plot on the complex z-plane, which is used to analyze the 3-dB frequency of a first-order discrete-time filter. The graph is centered on the origin and depicts a unit circle, which is a common feature in such plots. The real axis is labeled from -1 to 1, and the imaginary axis is labeled from -j to j.

Axes Labels and Units:
- **Horizontal Axis (Real Axis):** Ranges from -1 to 1.
- **Vertical Axis (Imaginary Axis):** Ranges from -j to j.
- The plot is in the complex plane, typically used to represent poles and zeros of a transfer function.

Overall Behavior and Trends:
- The unit circle is shown, which is crucial in determining the stability and frequency response of the filter.
- The pole is marked at a point on the real axis, denoted by \( a \).
- Vectors \( I_1 \) and \( I_2 \) are depicted, representing distances related to the pole and the point \( e^{j\omega} \) on the unit circle.

Key Features and Technical Details:
- The vector \( I_1 \) is defined as \( (1-a) \), which represents the distance from the pole to the point 1 on the real axis.
- The vector \( I_2 \) is defined as \( |e^{j\omega} - a| \) and is equivalent to \( \sqrt{2}(1-a) \), representing the distance from the pole to the point on the unit circle.
- The plot is used to determine when the magnitude of the denominator of \( H(z) \) becomes \( \sqrt{2} \) times larger than its dc value, which is a method to find the 3-dB frequency.

Annotations and Specific Data Points:
- The unit circle and vectors \( I_1 \) and \( I_2 \) are annotated, providing a visual reference for the mathematical relationships.
- The point \( e^{j\omega} \) is indicated on the unit circle, and its relation to the pole is a key aspect of analyzing the filter's characteristics.

Fig. 13.11 Pole-zero plot used to determine the 3-dB frequency of a first-order, discrete-time filter.

#### Solution

Consider the pole-zero plot shown in Fig. 13.11, where the zero is not shown since it is at $\infty$. Since the zero is at $\infty$, we need be concerned only with the magnitude of the denominator of $H(z)$ and when it becomes $\sqrt{2}$ larger than its dc value. The magnitude of the denominator of $\mathrm{H}(\mathrm{z})$ for $\mathrm{Z}=1$ (i.e., dc) is shown as the vector $\mathrm{I}_{1}$ in Fig. 13.11. This vector changes in size as $z$ goes around the unit circle and is shown as $I_{2}$ when it becomes $\sqrt{2}$ larger than $I_{1}$. Thus we can write

$$
\begin{equation*}
\mathrm{I}_{2}=\left|\mathrm{e}^{\mathrm{j} \omega}-\mathrm{a}\right| \equiv \sqrt{2}(1-\mathrm{a}) \tag{13.22}
\end{equation*}
$$

Writing $\mathrm{e}^{\mathrm{j} \omega}=\cos (\omega)+\mathrm{j} \sin (\omega)$, we have

$$
\begin{gather*}
|(\cos (\omega)-a)+j \sin (\omega)|^{2}=2(1-a)^{2}  \tag{13.23}\\
\cos ^{2}(\omega)-(2 a) \cos (\omega)+a^{2}+\sin ^{2}(\omega)=2(1-a)^{2}  \tag{13.24}\\
1-(2 a) \cos (\omega)+a^{2}=2\left(1-2 a+a^{2}\right) \tag{13.25}
\end{gather*}
$$

which is rearranged to give the final result.

$$
\begin{equation*}
\omega=\cos ^{-1}\left(2-\frac{\mathrm{a}}{2}-\frac{1}{2 \mathrm{a}}\right) \tag{13.26}
\end{equation*}
$$

For $\mathrm{a}=0.8, \omega=0.2241 \mathrm{rad}$, or 12.84 degrees. Such a location on the unit circle corresponds to $0.2241 /(2 \pi)$ times $\mathrm{f}_{\mathrm{s}}$ or, equivalently, $\mathrm{f}_{\mathrm{s}} / 28.04$.

### 13.5.2 Stability of Discrete-Time Filters

To realize rational polynomials in $\mathbf{z}$, discrete-time filters use delay elements (i.e., $z^{-1}$ building blocks) much the same way that analog filters can be formed using integrators (i.e., $\mathrm{s}^{-1}$ building blocks). The result is that finite difference equations represent discrete-time filters rather than the differential equations used to describe continuoustime filters.

Consider the signal flow graph block diagram of a first-order, discrete-time filter shown in Fig. 13.12. A finite difference equation describing this block diagram can be written as

$$
\begin{equation*}
y(n+1)=b x(n)+a y(n) \tag{13.27}
\end{equation*}
$$

image_name:Fig. 13.12
description:The system block diagram in Fig. 13.12 represents a first-order, discrete-time filter. It consists of the following main components:

1. **Input Signal Block (x(n))**: This is where the input signal, denoted as x(n), enters the system.

2. **Gain Block (b)**: The input signal is multiplied by a gain factor b. This is represented by an arrow leading from x(n) to a summing junction.

3. **Summing Junction**: This component adds two incoming signals. One is the scaled input signal bx(n), and the other is the feedback signal from the output, scaled by a factor a.

4. **Feedback Loop**: The output of the system, y(n), is fed back into the summing junction through a gain block with factor a. This forms a feedback loop that influences the next output y(n+1).

5. **Delay Block (z^{-1})**: After the summing junction, the signal passes through a delay block, represented by z^{-1}, which delays the signal by one time step. This delayed signal becomes the output y(n).

6. **Output Signal Block (y(n))**: The delayed signal is the output of the system, denoted as y(n).

Flow of Information:
- The input signal x(n) is multiplied by the gain b and added to the feedback signal ay(n) at the summing junction.
- The resulting signal, y(n+1), is then passed through the delay block z^{-1), producing the output y(n).
- The output y(n) is fed back into the system with a gain of a, completing the feedback loop.

Overall System Function:
The primary function of this system is to filter the input signal x(n) using a discrete-time first-order filter. The feedback loop and delay block are crucial for determining the filter's characteristics, such as its pole location in the z-domain, which is given by the transfer function H(z) = b / (z - a). This setup allows the system to continuously update its output based on both the current input and the previous output, providing a smooth filtering effect.

Fig. 13.12 A first-order, discrete-time filter.

In the Z -domain, this equation is written as

$$
\begin{equation*}
z \mathrm{y}(\mathrm{z})=\mathrm{bX}(\mathrm{z})+\mathrm{a} \mathrm{Y}(\mathrm{z}) \tag{13.28}
\end{equation*}
$$

where the z -domain property of delayed signals is used. We define the transfer function of this system to be $\mathrm{H}(\mathrm{z})$ given by

$$
\begin{equation*}
H(z) \equiv \frac{Y(z)}{X(z)}=\frac{b}{z-a} \tag{13.29}
\end{equation*}
$$

which has a pole on the real axis at $\mathbf{z}=\mathrm{a}$.
To test for stability, we let the input, $\mathbf{x}(\mathrm{n})$, be an impulse signal (i.e., 1 for $\mathrm{n}=0$ and 0 otherwise), which gives the following output signal, according to (13.27),

$$
y(0)=k
$$

where k is some arbitrary initial state value for y .

$$
\begin{gathered}
y(1)=b+a k \\
y(2)=a b+a^{2} k \\
y(3)=a^{2} b+a^{3} k \\
y(4)=a^{3} b+a^{4} k
\end{gathered}
$$

More concisely, the response, $h(n)$, is given by

$$
h(n)=\left\{\begin{array}{cc}
k & (n<1)  \tag{13.30}\\
\left(a^{n-1} b+a^{n} k\right) & (n \geq 1)
\end{array}\right.
$$

Clearly, this response remains bounded only when $|\mathrm{a}| \leq 1$ for this first-order filter and is unbounded otherwise.
Although this stability result is shown only for first-order systems, in general, an arbitrary, linear, time-invariant, discrete-time filter, $H(z)$, is stable if and only if all its poles are located within the unit circle. In other words, if $\mathbf{z}_{\mathrm{pi}}$ are the poles, then $\left|z_{\mathrm{pi}}\right|<1$ for all i . Locating some poles on the unit circle is similar to poles being on the imaginary $\mathrm{j} \omega$-axis for continuous-time systems. For example, in the preceding firstorder example, if $\mathrm{a}=1$, the pole is at $\mathbf{z}=1$, and the system is marginally stable (in

Key Point: A discretetime filter is stable if and only if all its poles are located within the unit circle.
fact, it is a discrete-time integrator). If we let $\mathrm{a}=-1$, the pole is at $\mathbf{z}=-1$, and one can show that the system oscillates at $f_{s} / 2$, as expected.

### 13.5.3 IIR and FIR Filters

Key Point: An infinite impulse response (IIR) filter has an impulse response that remains nonzero forever. A finite impulse response (FIR) filter has an impulse response that is finite in duration, eventually becoming preciselyzero.

Infinite impulse $r$ esponse (IIR) filters are discrete-time filters that, when excited by an impulse, have nonzero outputs indefinitely, assuming infinite precision arithmetic. ${ }^{2}$ For example, the filter given in (13.29) is an IIR filter (for a not equal to zero) since, although its impulse response decays towards zero (as all stable filters should), it remains nonzero forever, seen by letting $\mathrm{n} \rightarrow \infty$ in (13.30).

Finite impulse response (FIR) filters are discrete-time filters that, when excited by an impulse, their outputs go precisely to zero (and remain zero) after a finite value of $n$. As an example of an FIR filter, consider the following filter:

$$
\begin{equation*}
y(n)=\frac{1}{3}[x(n)+x(n-1)+x(n-2)] \tag{13.31}
\end{equation*}
$$

The transfer function for this filter, $H(z)$, is

$$
\begin{equation*}
H(z)=\frac{1}{3} \sum_{i=0}^{2} z^{-i} \tag{13.32}
\end{equation*}
$$

This filter is essentially a running average filter since its output is equal to the average value of its input over the last three samples. Applying an impulse signal to this filter results in an output that is nonzero for only three samples and, therefore, this is an FIR filter. Note that this FIR filter has poles, but they all occur at $\mathbf{z}=0$.

Some advantages of FIR filters are that stability is never an issue (they are always stable) and exact linear phase filters can be realized (a topic beyond the scope of this chapter). However, for many specifications, an IIR filter can meet the same specifications as an FIR filter, but with a much lower order, particularly in narrowband filters in which the poles of an IIR filter are placed close to the unit circle (i.e., has a slowly decaying impulse response).

### 13.5.4 Bilinear Transform

One method for obtaining a discrete-time transfer functions that meets a set of specifications is to use a bilinear transform to convert the specifications into a set of fictitious continuous-time filter specifications, design a filter in continuous-time to meet those specifications, and then convert the resulting filter back to discrete-time, again using a bilinear transform. Assuming that $\mathrm{H}_{\mathrm{c}}(\mathrm{s})$ is a continuous-time transfer function (where s is the complex variable equal to $\left.\sigma_{s}+j \Omega\right)$, the bilinear transform is defined to be given by ${ }^{3}$

$$
\begin{equation*}
s=\frac{z-1}{z+1} \tag{13.33}
\end{equation*}
$$

The inverse transformation is given by

$$
\begin{equation*}
\mathrm{z}=\frac{1+\mathrm{s}}{1-\mathrm{s}} \tag{13.34}
\end{equation*}
$$

[^0]A couple of points of interest about this bilinear transform are that the z-plane locations of 1 and -1 (i.e., dc and $f_{s} / 2$ ) are mapped to s-plane locations of 0 and $\infty$, respectively. However, with a little analysis, we will see that this bilinear transformation also maps the unit circle, $z=\mathrm{e}^{\mathrm{j} \omega}$, in the z-plane to the entire $\mathrm{j} \Omega$-axis in the s-plane. To see this mapping, we substitute $\mathrm{Z}=\mathrm{e}^{\mathrm{j} \omega}$ into (13.33),

$$
\begin{align*}
s & =\frac{e^{j \omega}-1}{e^{j \omega}+1}=\frac{e^{j(\omega / 2)}\left(e^{j(\omega / 2)}-e^{-j(\omega / 2)}\right)}{e^{j(\omega / 2)}\left(e^{j(\omega / 2)}+e^{-j(\omega / 2)}\right)}  \tag{13.35}\\
& =\frac{2 j \sin (\omega / 2)}{2 \cos (\omega / 2)}=j \tan (\omega / 2)
\end{align*}
$$

Thus, we see that points on the unit circle in the z-plane are mapped to locations on the j $\Omega$-axis in the s-plane, and we have

$$
\begin{equation*}
\Omega=\tan (\omega / 2) \tag{13.36}
\end{equation*}
$$

As a check, note that the z-plane locations of 1 and -1 , which correspond to $\omega$ equal to 0 and $\pi$, respectively, map to $\Omega$ equal to 0 and $\infty$.

One way to use this transform is to design a continuous-time transfer function, $\mathrm{H}_{\mathrm{c}}(\mathrm{s})$, and choose the discrete-time transfer function, $\mathrm{H}(\mathrm{z})$, such that

$$
\begin{equation*}
H(z) \equiv H_{c}[(z-1) /(z+1)] \tag{13.37}
\end{equation*}
$$

With such an arrangement, one can show that,

$$
\begin{equation*}
\mathrm{H}\left(\mathrm{e}^{\mathrm{j} \omega}\right)=\mathrm{H}_{\mathrm{c}}[\mathrm{j} \tan (\omega / 2)] \tag{13.38}
\end{equation*}
$$

and so the response of $\mathrm{H}(\mathrm{z})$ is shown to be equal to the response of $\mathrm{H}_{\mathrm{c}}(\mathrm{s})$, except with a frequency warping according to (13.36). Note that the order of $\mathrm{H}(\mathrm{z})$ equals that of $\mathrm{H}_{\mathrm{c}}(\mathrm{s})$ since, according to (13.37), each s term is replaced by another first-order function.

Key Point: The bilinear transform provides a mapping betweendiscreteand continuous-time transfer functions whereby $z=-1$ maps to infinite frequency and $z=1$ maps to dc.

#### EXAMPLE 13.7

Using the bilinear transform, find a first-order $H(z)$ that has a $3-d B$ frequency at $f_{s} / 20$, a zero at -1 , and a dc gain of 1 .

#### Solution

Using (13.36), the frequency value, $\mathrm{f}_{\mathrm{s}} / 20$, or equivalently, $\omega=(2 \pi) / 20=0.314159$ is mapped to $\Omega=0.1584 \mathrm{rad} / \mathrm{s}$. Thus, $\mathrm{H}_{\mathrm{c}}(\mathrm{s})$ should have a $3-\mathrm{dB}$ frequency value of $0.1584 \mathrm{rad} / \mathrm{s}$. Such a $3-\mathrm{dB}$ frequency value is obtained by having a s-plane zero equal to $\infty$ and a pole equal to -0.1584 . Transforming these continuous-time pole and zero back into the $\mathbf{z}$-plane using (13.34) results in a $\mathbf{Z}$-plane zero at -1 and a pole at 0.7265 . Therefore, $H(z)$ appears as

$$
H(z)=\frac{k(z+1)}{z-0.7265}
$$

The constant $k$ can be determined by setting the dc gain to 1 , or equivalently, $|H(1)|=1$, which results in $\mathrm{k}=0.1368$.

## 13.6 SAMPLE-AND-HOLD RESPONSE

In this section, we look at the frequency response that occurs when we change a discrete-time signal back into an analog signal with the use of a sample-and-hold circuit. Note that here we plot a frequency response for all frequencies (as opposed to only up to $f_{s} / 2$ ) since the output signal is a continuous-time signal rather than a discrete-time one.

A sample-and-hold signal, $\mathrm{x}_{\mathrm{sh}}(\mathrm{t})$, is related to its sampled signal by the mathematical relationship

$$
\begin{equation*}
\mathrm{x}_{\mathrm{sh}}(\mathrm{t})=\sum_{n=-\infty}^{\infty} \mathrm{x}_{\mathrm{c}}(\mathrm{nT})[\vartheta(\mathrm{t}-\mathrm{nT})-\vartheta(\mathrm{t}-\mathrm{nT}-\mathrm{T})] \tag{13.39}
\end{equation*}
$$

Note that, once again, $\mathrm{x}_{\mathrm{sh}}(\mathrm{t})$ is well defined for all time, and thus the Laplace transform can be found to be equal to

$$
\begin{align*}
X_{s h}(s) & =\frac{1-e^{-s T}}{s} \sum_{n=-\infty}^{\infty} x_{c}(n T) e^{-s n T}  \tag{13.40}\\
& =\frac{1-e^{s T}}{s} X_{s}(s)
\end{align*}
$$

This result implies that the hold transfer function, $\mathrm{H}_{\mathrm{sh}}(\mathrm{s})$, is equal to

$$
\begin{equation*}
\mathrm{H}_{\mathrm{sh}}(\mathrm{~s})=\frac{1-\mathrm{e}^{-\mathrm{sT}}}{\mathrm{~s}} \tag{13.41}
\end{equation*}
$$

It should be mentioned here that this transfer function is usually referred to as the sample-and-hold response although, in fact, it only accounts for the hold portion.

The spectrum for $H_{s h}(s)$ is found by substituting $s=j \omega$ into (13.41), resulting in

$$
\begin{equation*}
H_{s h}(j \omega)=\frac{1-e^{-j \omega T}}{j \omega}=T \times e^{-j \omega T / 2} \times \frac{\sin (\omega T / 2)}{(\omega T / 2)} \tag{13.42}
\end{equation*}
$$

image_name:Fig. 13.13 Sample-and-hold response
description:The graph labeled "Fig. 13.13 Sample-and-hold response" depicts a frequency response function, specifically illustrating the magnitude of the sample-and-hold response, also known as the sinc response.

1. **Type of Graph and Function:**
- This is a frequency response graph showing the magnitude of the sample-and-hold function, often referred to as the sinc function.

2. **Axes Labels and Units:**
- The x-axis represents frequency \( f \), marked in terms of multiples of the sampling frequency \( f_s \), such as \(-3f_s, -2f_s, -f_s, 0, f_s, 2f_s, 3f_s\).
- The y-axis represents the magnitude of the response \(|H_{sh}(j\omega)|\).

3. **Overall Behavior and Trends:**
- The graph displays a central peak at \( f = 0 \), indicating the maximum magnitude of the response.
- As the frequency moves away from zero, the magnitude decreases, showing a characteristic sinc function shape with diminishing oscillations.
- The response exhibits periodic nulls at multiples of the sampling frequency \( \pm f_s, \pm 2f_s, \pm 3f_s \), where the magnitude reaches zero.

4. **Key Features and Technical Details:**
- The central peak at \( f = 0 \) represents the maximum value of the sinc function.
- The graph shows symmetrical behavior around \( f = 0 \), with decreasing amplitude oscillations as frequency increases.
- The zero crossings at \( \pm f_s, \pm 2f_s, \pm 3f_s \) are significant points where the response nulls out.

5. **Annotations and Specific Data Points:**
- The graph is marked with specific frequency points \( -3f_s, -2f_s, -f_s, 0, f_s, 2f_s, 3f_s \) on the x-axis, highlighting the periodic nature of the sinc response.
- There are no additional annotations or numerical values provided beyond these labeled points.

Fig. 13.13 Sample-and-hold response (also called the sinc response).
The magnitude of this response is given by

$$
\left|\mathrm{H}_{\mathrm{sh}}(\mathrm{j} \omega)\right|=\mathrm{T} \frac{|\sin (\omega \mathrm{~T} / 2)|}{|\omega \mathrm{T} / 2|}
$$

or

$$
\begin{equation*}
\left|\mathrm{H}_{\mathrm{sh}}(\mathrm{f})\right|=\mathrm{T} \frac{\left|\sin \left(\pi \mathrm{f} / \mathrm{f}_{\mathrm{s}}\right)\right|}{\left|(\pi \mathrm{f}) / \mathrm{f}_{\mathrm{s}}\right|} \tag{13.43}
\end{equation*}
$$

and is often referred to as the $(\sin \mathbf{x}) / \mathrm{x}$ or sinc response. This magnitude response is illustrated in Fig. 13.13.
Multiplying this sinc response by $\mathrm{X}_{\mathrm{s}}(\mathrm{f})$ in Fig. 13.2 confirms the spectral relationship for $\mathrm{X}_{\text {sh }}(\mathrm{f})$. It should be noted here that this frequency shaping of a sample and hold occurs only for a continuous-time signal. Specifically, although the sample and hold before the A/D converter shown in Fig. 13.1(b) would result in $\mathrm{x}_{\mathrm{sh}}(\mathrm{t})$ having smaller images at higher frequencies (due to the sinc response), the images of $x(n)$ are all of the same height (i.e., they are not multiplied by the sinc response) since it is a discrete-time signal. This is because, when converted to a discrete-time signal, the smaller images located at and above $f_{s}$ are aliased in a manner that pre-

Key Point: The frequencyresponse of a sample-and-held signal is that of the original discrete-time sequence, repeated every $f_{s}$, and then shaped by a sinc frequency response.
cisely reconstructs the original spectrum, so long as it was sampled above the Nyquist rate. In other words, a sample and hold before an A/D converter simply allows the converter to have a constant input value during one conversion and does not aid in any anti-aliasing requirement.

#### EXAMPLE 13.8

Consider the discrete-time signal processing system shown in Fig. 13.1(b), where a sample (and clock rate) of 50 kHz is used and the digital filter has the response

$$
H(z)=\frac{0.2}{z-0.8}
$$

For a $10-\mathrm{kHz}$ input sinusoidal signal of 1 V rms , find the magnitude of the output signal, $\mathrm{y}_{\mathrm{sn}}(\mathrm{t})$, at 10 kHz , and at the images 40 kHz and 60 kHz . Assume the quantization effects of the $\mathrm{A} / \mathrm{D}$ and $\mathrm{D} / \mathrm{A}$ converters are so small that they can be ignored. Also assume the converters complement each other such that a 1-V dc signal into the $\mathrm{A} / \mathrm{D}$ converter results in a $1-\mathrm{V}$ dc signal from the $\mathrm{D} / \mathrm{A}$ converter if the converters are directly connected together.

#### Solution

First, the magnitude of $\mathrm{H}(\mathrm{z})$ is found for a $10-\mathrm{kHz}$ signal when the sampling rate is 50 kHz by noting that

$$
\begin{aligned}
\mathrm{e}^{\mathrm{j}(2 \pi \times 10 \mathrm{kHz} / 50 \mathrm{kHz})} & =\mathrm{e}^{\mathrm{j} 0.4 \pi}=\cos (0.4 \pi)+\mathrm{j} \sin (0.4 \pi) \\
& =0.309017+\mathrm{j} 0.951057
\end{aligned}
$$

and therefore the gain of $\mathrm{H}(\mathrm{z})$ for a $10-\mathrm{kHz}$ signal is found to be given by

$$
\left|\mathrm{H}\left(\mathrm{e}^{\mathrm{j} 0.4 \pi}\right)\right|=\frac{0.2}{|(0.309017-0.8)+\mathrm{j} 0.951057|}=0.186864
$$

To determine the magnitude of $\mathrm{y}_{\mathrm{sh}}(\mathrm{t})$ at various frequencies, we need only multiply the filter's gain by the sinc response shown in Fig. 13.13. Specifically, the magnitude of the sample-and-hold response for a $10-\mathrm{kHz}$ signal when using a $50-\mathrm{kHz}$ clock is equal to

$$
\left|\mathrm{H}_{\mathrm{sh}}(10 \mathrm{kHz})\right|=\mathrm{T} \frac{\sin (\pi 10 / 50)}{(\pi 10 / 50)}=0.9355 \mathrm{~T}
$$

and therefore the magnitude of $\mathrm{y}_{\mathrm{sh}}(\mathrm{t})$ at 10 kHz is equal to $0.18686 \times 0.9355=175 \mathrm{mV}_{\mathrm{rms}}$ (note that the T term cancels with a similar T term due to the creation of a discrete-time signal-see (13.13) in Section 13.2). Similarly, the magnitude of $\mathrm{H}_{\mathrm{sh}}(\mathrm{f})$ at 40 kHz and 60 kHz is 0.2399 and 0.1559 , respectively, resulting in the magnitude of $\mathrm{y}_{\mathrm{sh}}(\mathrm{t})$ at 40 kHz and 60 kHz to be 43.7 and $29.1 \mathrm{mV}_{\mathrm{rms}}$, respectively.

## 13.7 KEY POINTS

- Discrete-time signals may be processed either digitally, in which case they are quantized both in time and amplitude, or using discrete-time analog circuits such as switched-capacitor circuits, in which case the signal amplitude is continuously variable. [p. 537]
- The spectrum of a sampled signal is a sum of shifted copies of the original continuous-time spectrum so that no aliasing occurs if the original waveform is bandlimited to one-half the sampling rate. The minimum sampling frequency required to avoid aliasing is called the Nyquist rate, and is equal to two times the signal bandwidth. [p. 540]
- Discrete-time signal spectra are equal to the corresponding sampled signal spectra with the sample time normalized to 1 Hz . Hence, their spectra repeat every $2 \pi$. [p. 541]
- To avoid aliasing when downsampling by a factor L , the original signal must be sampled at L times the Nyquist rate. [p. 543]
- Upsampling by L results in a renormalization along the frequency axis so that L copies of the original signal spectrum are now squeezed in the range 0 to $2 \pi$. [p. 543]
- The frequency response of a discrete-time filter $\mathrm{H}(\mathrm{z})$ is found by evaluating its magnitude and phase on the unit circle, or graphically by considering the magnitude and phase of vectors connecting its poles and zeros to points around the unit circle. [p. 546]
- In discrete-time, the point $\mathrm{z}=1$ corresponds both to dc and to signals at the sampling frequency. The frequency response is periodic, and for rational transfer functions with real-valued coefficients exhibits conjugate symmetry around dc. Hence, discrete-time frequency responses need only be plotted from dc to half the sample rate, p. [p. 546]
- A discrete-time filter is stable if and only if all its poles are located within the unit circle. [p. 549]
- An infinite impulse response (IIR) filter has an impulse response that remains nonzero forever. A finite impulse response (FIR) filter has an impulse response that is finite in duration, eventually becoming precisely zero. [p. 550]
- The bilinear transform provides a mapping between discrete- and continuous-time transfer functions whereby $\mathrm{z}=-1$ maps to infinite frequency and $\mathrm{z}=1$ maps to dc. [p. 551]
- Using the bilinear transform, discrete-time transfer functions can be designed by mapping the specifications to fictitious continuous-time equivalents and finding a suitable $\mathrm{H}_{\mathrm{c}}(\mathrm{s})$. The inverse mapping $\mathrm{H}(\mathrm{z})=\mathrm{H}_{\mathrm{c}}((\mathrm{z}-1) /(\mathrm{z}+1))$ results in the desired discrete-time transfer function. [p. 551]
- The frequency-response of a sample-and-held signal is that of the original discrete-time sequence, repeated every $f_{s}$, and then shaped by a sinc frequency response. [p. 553]
