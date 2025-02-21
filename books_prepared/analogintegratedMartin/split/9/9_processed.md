# 9. Noise and Linearity Analysis and Modelling

To develop good analog circuit design techniques, a basic understanding of noise sources and analysis is required. Another motivation to study noise analysis is to learn basic concepts of random signals for a proper understanding of oversampling converters. The purpose of this chapter is to present some fundamentals of noise analysis followed by an introduction to electronic noise sources and circuit analysis, and finally linearity.

It should be mentioned here that this chapter deals with inherent noise as opposed to interference noise. Interference noise is a result of unwanted interaction between the circuit and the outside world, or between different parts of the circuit itself. This type of noise may or may not appear as random signals. Examples are power supply noise on ground wires (such as a $60-\mathrm{Hz}$ hum) or electromagnetic interference between wires. Interference noise can be significantly reduced by careful circuit wiring or layout. In contrast, inherent noise refers to random noise signals that can be reduced but never eliminated since this noise is due to fundamental properties of the circuits. Some examples of inherent noise are thermal, shot, and flicker noise. Inherent noise is only moderately affected by circuit wiring or layout, such as using multiple base contacts to change the resistance value of the base of a transistor. However, inherent noise can be significantly reduced through proper circuit design, such as changing the circuit structure or increasing the power consumption.

The outline of this chapter is as follows: First, a time-domain analysis of noise signals (or other random signals) is presented. Here, basic concepts such as rms value, signal-to-noise ratio, and noise summation are presented. Next, a frequency-domain analysis of noise is presented. As with deterministic signals, analysis in the frequency domain results in more powerful analysis tools than does analysis that remains strictly in the time domain. Noise models for circuit elements are then presented, followed by noise analyses of some real circuits to give the reader some experience in such analysis. Finally, whereas noise imposes a lower limit on the range of signal amplitudes that can be meaningfully processed by a circuit, linearity often imposes the upper limit. The difference between them is a circuit's dynamic range. The chapter ends with introductions to linearity and dynamic range.

## 9.1 TIME-DOMAIN ANALYSIS

Since inherent noise signals are random in nature, we define here some basic tools to effectively deal with random signals. Specifically, in this section, we define the following terms in the time domain: rms value, SNR, dBm , and noise summation.

An example of a random noise signal in the time domain is shown in Fig. 9.1. Although this signal is a voltage it could just as easily be current noise or some other quantity. The signal appears to have an average value of zero. In

Key Point: This chapter focuses on noise inherent to the physical operation of electronic components, not noise from outside interferences. Such noise sources are generally zero-mean.
fact, throughout this chapter we will assume all noise sig nals have a mean value of zero, which simplifies many of the definitions and is also valid in most physical systems.
image_name:Fig. 9.1 Example of a voltage noise signal in the time domain.
description:**Type of Graph and Function:**\nThe graph is a time-domain waveform representing a voltage noise signal.\n\n**Axes Labels and Units:**\n- The horizontal axis is labeled as 'Time (s)' and represents time in seconds, ranging from 0 to 1 second.\n- The vertical axis is labeled as 'v_n(t) (V)' and represents voltage in volts, with a range from -0.5 V to 0.5 V.\n\n**Overall Behavior and Trends:**\nThe waveform exhibits a fluctuating pattern around a mean value of zero, which is typical for noise signals. The signal shows rapid oscillations with no discernible periodicity, indicating a random noise pattern. The amplitude of the noise appears to remain within the bounds of -0.5 V to 0.5 V throughout the observed period.\n\n**Key Features and Technical Details:**\n- The noise signal crosses the zero line multiple times, reflecting its zero-mean nature.\n- There are no distinct peaks or valleys that dominate the waveform; instead, it is characterized by continuous, irregular oscillations.\n- The amplitude variation remains consistent, with no significant spikes or dips beyond the observed range.\n\n**Annotations and Specific Data Points:**\n- The graph does not contain specific annotations, markers, or reference lines.\n- No numerical values for specific data points are provided, as the graph illustrates a general noise behavior rather than specific measurements.

Fig. 9.1 Example of a voltage noise signal in the time domain.

### 9.1.1 Root Mean Square (rms) Value

Consider a noise voltage, $\mathrm{v}_{\mathrm{n}}(\mathrm{t})$, such as that shown in Fig. 9.1, or a noise current, $\mathrm{i}_{\mathrm{n}}(\mathrm{t})$. The rms, or root mean square, voltage value is defined ${ }^{1}$ as

$$
\begin{equation*}
\mathrm{V}_{\mathrm{n}(\mathrm{rms})} \equiv\left[\frac{1}{\mathrm{~T}} \int_{0}^{T} \mathrm{~V}_{\mathrm{n}}^{2}(\mathrm{t}) \mathrm{dt}\right]^{1 / 2} \tag{9.1}
\end{equation*}
$$

where T is a suitable averaging time interval. Typically, a longer T gives a more accurate rms measurement. Similarly, the rms current value is defined as

$$
\begin{equation*}
\mathrm{I}_{\mathrm{n}(\mathrm{rms})} \equiv\left[\frac{1}{\mathrm{~T}} \int_{0}^{\mathrm{T}} \mathrm{i}_{\mathrm{n}}^{2}(\mathrm{t}) \mathrm{dt}\right]^{1 / 2} \tag{9.2}
\end{equation*}
$$

The benefit in knowing the rms value of a signal is that it indicates the normalized noise power of the signal. Specifically, if the random signal $\mathrm{v}_{\mathrm{n}}(\mathrm{t})$ is applied to a $1-\Omega$ resistor, the average power dissipated, $\mathrm{P}_{\text {diss }}$, in watts, equals the normalized noise power and is given by

$$
\begin{equation*}
\mathrm{P}_{\mathrm{diss}}=\frac{\mathrm{V}_{\mathrm{n}(\mathrm{~ms})}^{2}}{1 \Omega}=\mathrm{V}_{\mathrm{n}(\mathrm{~ms})}^{2} \tag{9.3}
\end{equation*}
$$

Key Point: Although the instantaneous value of a noise voltage or current cannot be determined by analysis, therms value obtained by time-averaging its square provides a normalized measure of the noise signal's power.

This relationship implies that the power dissipated by a resistor is the same whether a random signal or a dc level of $k$ volts (rms) is applied across it. For example, a noise signal with an rms value of 1 mV (rms) dissipates the same power across a resistor as a dc voltage of 1 mV .
Similarly, for a noise current, $\mathrm{i}_{n}(\mathrm{t})$, applied to a $1-\Omega$ resistor,

$$
\begin{equation*}
P_{\text {diss }}=I_{n(\mathrm{rms})}^{2} \times 1 \Omega=I_{n(\mathrm{~ms})}^{2} \tag{9.4}
\end{equation*}
$$

As a result, the square of the rms values, $V_{n(r m s)}^{2}$ and $I_{n(r m s)}^{2}$, are sometimes referred to as the normalized noise powers of these two signals.

[^5]
### 9.1.2 SNR

The signal-to-noise ratio (SNR) value (in dB ) of a signal node in a system is defined as

$$
\begin{equation*}
\mathrm{SNR} \equiv 10 \log \left[\frac{\text { signal power }}{\text { noise power }}\right] \mathrm{dB} \tag{9.5}
\end{equation*}
$$

Thus, assuming a node in a circuit consists of a signal, $\mathrm{v}_{\mathrm{x}}(\mathrm{t})$, that has a normalized signal power of $\mathrm{V}_{\mathrm{x}(\mathrm{ms})}^{2}$ and a normalized noise power of $\mathrm{V}_{\mathrm{n}(\mathrm{ms})}^{2}$, the SNR is given by

$$
\begin{equation*}
\mathrm{SNR}=10 \log \left[\frac{\mathrm{~V}_{\mathrm{x}(\mathrm{rms})}^{2}}{\mathrm{~V}_{\mathrm{n}(\mathrm{rms})}^{2}}\right]=20 \log \left[\frac{\mathrm{~V}_{\mathrm{x}(\mathrm{rms})}}{\mathrm{V}_{\mathrm{n}(\mathrm{~ms})}}\right] \mathrm{dB} \tag{9.6}
\end{equation*}
$$

Key Point: SNR is the ratio of signal power to noise power, both normalized to the same impedance and expressed in $d B$.

Clearly, when the mean-squared values of the noise and signal are the same, then $\mathrm{SNR}=0 \mathrm{~dB}$.

### 9.1.3 Units of dBm

Although dB units relate the relative ratio of two power levels, it is often useful to know a signal's power in dB on an absolute scale. One common measure is that of dBm , where all power levels are referenced by 1 mW . In other words, a 1-mW signal corresponds to 0 dBm , whereas a $1-\mu \mathrm{W}$ signal corresponds to -30 dBm . When voltage levels are measured, it is also common to reference the voltage level to the equivalent power dissipated if the voltage is applied across either a $50-\Omega$ or a $75-\Omega$ resistor.

Key Point: Units of dBm express an average power level on a logarithmic scale normalized to 1 mW , so that 1 mW is 0 dBm and 0.1 mW is -10 dBm. Rms voltages or currents are also sometimes expressed in dBm by assuming that they are applied to some agreed-upon reference load, usually either 50 or 75 Ohms.

#### EXAMPLE 9.1

Find the rms voltage of a $0-\mathrm{dBm}$ signal referenced to a $50-\Omega$ resistor. What is the level in dBm of a 2 -volt rms signal?

#### Solution

A $0-\mathrm{dBm}$ signal referenced to a $50-\Omega$ resistor implies that the rms voltage level equals

$$
\begin{equation*}
\mathrm{V}_{(\mathrm{rms})}=\sqrt{(50 \Omega) \times 1 \mathrm{~mW}}=0.2236 \mathrm{~V} \tag{9.7}
\end{equation*}
$$

Thus, a 2-volt rms signal corresponds to

$$
\begin{equation*}
20 \log \left(\frac{2.0}{0.2236}\right)=19 \mathrm{dBm} \tag{9.8}
\end{equation*}
$$

and would dissipate 80 mW across a $50-\Omega$ resistor.

Note that the measured voltage may never be physically applied across any $50-\Omega$ resistor. The measured voltage is referenced only to power levels that would occur if the voltage were applied to such a load. Similar results are obtained if the power is referenced to a $75-\Omega$ resistor.

### 9.1.4 Noise Summation

Consider the case of two noise sources added together, as shown in Fig. 9.2. If the rms values of each individual noise source are known, what can be said about the rms value of the combined signal? We answer this question as follows. Define $\mathrm{v}_{\mathrm{no}}(\mathrm{t})$ as

$$
\begin{equation*}
\mathrm{v}_{\mathrm{n} 0}(\mathrm{t})=\mathrm{v}_{\mathrm{n} 1}(\mathrm{t})+\mathrm{v}_{\mathrm{n} 2}(\mathrm{t}) \tag{9.9}
\end{equation*}
$$

where $\mathrm{v}_{\mathrm{n} 1}(\mathrm{t})$ and $\mathrm{V}_{\mathrm{n} 2}(\mathrm{t})$ are two noise sources with known rms values $\mathrm{V}_{\mathrm{n} 1(\mathrm{~ms})}$ and $\mathrm{V}_{\mathrm{n} 2(\mathrm{~ms})}$, respectively. Then we can write

$$
\begin{equation*}
\mathrm{V}_{\mathrm{no}(\mathrm{rms})}^{2}=\frac{1}{\mathrm{~T}} \int_{0}^{\mathrm{T}}\left[\mathrm{v}_{\mathrm{n} 1}(\mathrm{t})+\mathrm{V}_{\mathrm{n} 2}(\mathrm{t})\right]^{2} \mathrm{dt} \tag{9.10}
\end{equation*}
$$

which, when expanded, gives,

$$
\begin{equation*}
\mathrm{V}_{\mathrm{no}(\mathrm{rms})}^{2}=\mathrm{V}_{\mathrm{n} 1(\mathrm{rms})}^{2}+\mathrm{V}_{\mathrm{n} 2(\mathrm{rms})}^{2}+\frac{2}{\mathrm{~T}} \int_{0}^{\mathrm{T}} \mathrm{~V}_{\mathrm{n} 1}(\mathrm{t}) \mathrm{V}_{\mathrm{n} 2}(\mathrm{t}) \mathrm{dt} \tag{9.11}
\end{equation*}
$$

Note that the first two terms in the right-hand side of (9.11) are the individual mean-squared values of the noise sources. The last term shows the correlation between the two signal sources, $\mathrm{v}_{\mathrm{n} 1}(\mathrm{t})$ and $\mathrm{v}_{\mathrm{n} 2}(\mathrm{t})$. An alternate way to write (9.11) that better indicates the effects of signal correlation, is to define a correlation coefficient, C , as

$$
\begin{equation*}
\mathrm{C} \equiv \frac{\frac{1}{\mathrm{~T}} \int_{0}^{T} \mathrm{v}_{\mathrm{n} 1}(\mathrm{t}) \mathrm{V}_{\mathrm{n} 2}(\mathrm{t}) \mathrm{dt}}{\mathrm{~V}_{\mathrm{n} 1(\mathrm{rms})} \mathrm{V}_{\mathrm{n} 2(\mathrm{rms})}} \tag{9.12}
\end{equation*}
$$

With this definition, (9.11) can also be written as

$$
\begin{equation*}
V_{\mathrm{no}(\mathrm{~ms})}^{2}=\mathrm{V}_{\mathrm{n} 1(\mathrm{~ms})}^{2}+\mathrm{V}_{\mathrm{n} 2(\mathrm{rms})}^{2}+2 C V_{\mathrm{n} 1(\mathrm{rms})} \mathrm{V}_{\mathrm{n} 2(\mathrm{rms})} \tag{9.13}
\end{equation*}
$$

It can be shown that the correlation coefficient always satisfies the condition $-1 \leq C \leq 1$. Also, a value of $C= \pm 1$ implies the two signals are fully correlated, whereas $\mathrm{C}=0$ indicates the signals are uncorrelated. Values in between imply the signals are partially correlated. Fortunately, we have little reason to analyze partially correlated signals since different inherent noise sources are typically uncorrelated.

In the case of two uncorrelated signals, the mean-squared value of their sum is given by

$$
\begin{equation*}
V_{\mathrm{no}(\mathrm{rms})}^{2}=V_{\mathrm{n} 1(\mathrm{rms})}^{2}+V_{\mathrm{n} 2(\mathrm{rms})}^{2} \tag{9.14}
\end{equation*}
$$

Key Point: The power of independent (uncorrelated) noise sources superimpose linearly, which means their voltages and currents superimpose in a root-sum-ofsquares fashion. As a result, to lower overall noise, one must focus on the largest noise contributors.

This relationship indicates that two rms values add as though they were the magnitudes of vectors at right angles to each other (i.e., orthogonal) when signals are uncorrelated.

It is of interest to contrast this uncorrelated case with that for fully correlated signals. An example of two fully correlated (though deterministic) sources are two sinusoidal signals that have the same frequency and a phase of 0 or 180 degrees with each other. In this fully correlated case, the mean-squared value of their sum is given by
image_name:(a)
description:
[
name: Vn1(t), type: VoltageSource, value: Vn1(t), ports: {Np: Vno(t), Nn: X}
name: Vn2(t), type: VoltageSource, value: Vn2(t), ports: {Np: X, Nn: GND}
]
extrainfo:The circuit diagram shows two voltage sources Vn1(t) and Vn2(t) connected in series to produce an output voltage Vno(t). The positive terminal of Vn1(t) is connected to node N1, which is also connected to the positive terminal of Vn2(t), while their negative terminals are connected to ground.

image_name:(b)
description:
[
name: in1(t), type: CurrentSource, value: in1(t), ports: {Np: GND, Nn: ino(t)}
name: in2(t), type: CurrentSource, value: in2(t), ports: {Np: GND, Nn: ino(t)}
]
extrainfo:The circuit diagram shows two current sources in1(t) and in2(t) connected in parallel. The output current ino(t) is controlled by a switch that connects the node N1 to the ground.

Fig. 9.2 Combining two noise sources, (a) voltage, and (b) current.

$$
\begin{equation*}
V_{\mathrm{no}(\mathrm{rms})}^{2}=\left[\mathrm{V}_{\mathrm{n} 1(\mathrm{rms})} \pm \mathrm{V}_{\mathrm{n} 2(\mathrm{rms})}\right]^{2} \tag{9.15}
\end{equation*}
$$

where the sign is determined by whether the signals are in or out of phase with each other. Note that, in this case where the signals are fully correlated, the rms values add linearly (similar to the magnitudes of aligned vectors).

#### EXAMPLE 9.2

Given two uncorrelated noise sources that have $\mathrm{V}_{\mathrm{n} 1(\mathrm{~ms})}=10 \mu \mathrm{~V}$ and $\mathrm{V}_{\mathrm{n} 2(\mathrm{~ms})}=5 \mu \mathrm{~V}$, find their total output rms value when combined. If we are required to maintain the total rms value at $10 \mu \mathrm{~V}$, how much should $\mathrm{V}_{\mathrm{n1}(\mathrm{rms})}$ be reduced while $\mathrm{V}_{\mathrm{n} 2(\mathrm{~ms})}$ remains unchanged?

#### Solution

Using (9.14) results in

$$
\begin{equation*}
\mathrm{V}_{\mathrm{no}(\mathrm{mss})}^{2}=\left(10^{2}+5^{2}\right)=125(\mu \mathrm{~V})^{2} \tag{9.16}
\end{equation*}
$$

which results in $\mathrm{V}_{\text {no(rms) }}=11.2 \mu \mathrm{~V}$.
To maintain $\mathrm{V}_{\mathrm{no}(\mathrm{ms})}=10 \mu \mathrm{~V}$ and $\mathrm{V}_{\mathrm{n} 2(\mathrm{rms})}=5 \mu \mathrm{~V}$, we have

$$
\begin{equation*}
10^{2}=V_{\mathrm{n} 1(\mathrm{~ms})}^{2}+5^{2} \tag{9.17}
\end{equation*}
$$

which results in $\mathrm{V}_{\mathrm{n} 1(\mathrm{rms})}=8.7 \mu \mathrm{~V}$. Therefore, reducing $\mathrm{V}_{\mathrm{n1}(\mathrm{rms})}$ by 13 percent is equivalent to eliminating $\mathrm{V}_{\mathrm{n} 2 \text { (rms) }}$ altogether!

The above example has an important moral. To reduce overall noise, concentrate on large noise signals.

## 9.2 FREQUENCY-DOMAIN ANALYSIS

As with deterministic signals, frequency-domain techniques are useful for dealing with random signals such as noise. This section presents frequency-domain techniques for dealing with noise signals and other random signals. It should be noted that units of hertz ( Hz ) (rather than radians/second) are used throughout this chapter since, historically, such units have been commonly used in the measurement of continuous-time spectral densities.

### 9.2.1 Noise Spectral Density

Although periodic signals (such as a sinusoid) have power at distinct frequency locations, random signals have their power spread out over the frequency spectrum. For example, if the time-domain signal shown in Fig. 9.1 is applied to a spectrum analyzer, the resulting spectrum might look like that shown in Fig. 9.3(a). Note here that although the horizontal scale is the usual frequency axis, the vertical scale is in units of microvolts-squared/hertz. In other words, the vertical axis is a measure of the normalized noise power (mean-squared value) over a $1-\mathrm{Hz}$ bandwidth at each frequency point. For example, the measurement at 100 Hz in Fig. 9.3(a) indicates that the normalized power between 99.5 Hz and 100.5 Hz is $10(\mu \mathrm{~V})^{2}$.

Thus, we define the noise spectral density, $\mathrm{V}_{\mathrm{n}}^{2}(\mathrm{f})$, or in the case of current, $\mathrm{I}_{\mathrm{n}}^{2}(\mathrm{f})$, as the average normalized noise power over a 1-Hz bandwidth. The units of $V_{n}^{2}(\mathrm{f})$ are volts-squared/hertz, whereas those of $I_{n}^{2}(f)$ are ampssquared/hertz. Also, $\mathrm{V}_{\mathrm{n}}^{2}(\mathrm{f})$ is a positive real-valued function.

Key Point: The frequencydomain representation of a noise signal is its spectral density: the average normalized power that may be measured within a $1-\mathrm{Hz}$ bandwidth.

It should be emphasized here that the mean-squared value of a random noise signal at a single precise frequency is zer $o$. In other words, the mean-squared value of the signal shown in Fig. 9.3(a) measured at 100 Hz is directly proportional to the bandwidth of the bandpass filter used for the measurement. In a laboratory spectrum analyzer, the bandwidth of the bandpass filter is determined by the resolution-bandwidth control. Thus, as the resolution bandwidth goes to zero, the mean-squared value also becomes zero. ${ }^{2}$ Conversely, as the resolution bandwidth increases, so does the measured mean-squared value. In either case, the measured mean-squared value should be normalized to the value that would be obtained for a bandwidth of 1 Hz when the noise spectral density is stated in units of $\mathrm{V}^{2} /(\mathrm{Hz})$. For example, if the signal corresponding to Fig. 9.3(a) were measured at around 0.1 Hz using a resolution bandwidth of 1 mHz , the mean-squared value measured would be $1(\mu \mathrm{~V})^{2}$, which, when scaled to a $1-\mathrm{Hz}$ bandwidth, equals $1,000\left(\mu \mathrm{~V}^{2}\right) / \mathrm{Hz}$.

An intuitive explanation of how a random noise signal is measured using a spectrum analyzer is as follows. A random noise signal has a frequency that is continually changing through a broad continuum of frequencies. A spectrum analyzer is sensitive to only a narrow frequency range that is the passband of its filter, and it measures the meansquared value in that range. The filter of the spectrum analyzer reacts with a time constant approximately given by

$$
\begin{equation*}
\tau \approx \frac{1}{\pi \mathrm{~W}} \tag{9.18}
\end{equation*}
$$

where W is the bandwidth of the filter. For some of the time, the random signal has the same frequency as the spectrum analyzer's filter. Thus, the spectrum analyzer effectively measures what percentage of time the random signal is in the frequency range of its filter. The narrower the bandwidth of the filter, the less percentage of time the signal is within its frequency range, and therefore the smaller is the spectrum analyzer's output. However, if the signal is not a random signal wandering in and out of the frequency range of the spectrum analyzer's filter, but is a deterministic signal at the center frequency of the filter, then the spectrum analyzer's reading is independent of the filter's bandwidth.

It is often convenient to plot the square root of the noise spectral density when we deal with filtered noise. Taking a square root results in $\mathrm{V}_{\mathrm{n}}(\mathrm{f})$, as shown in Fig. $9.3(b)$. We will refer to $\mathrm{V}_{\mathrm{n}}(\mathrm{f})$ as the root spectral density which is expressed in units of volts/root-hertz (i.e., $\mathrm{V} / \sqrt{\mathrm{Hz}}$ ). In the case of current noise, the resulting units are amps/root-hertz. Note that the horizontal axis remains unchanged although there is a root-hertz factor in the vertical axis.
image_name:(a)
description:The graph labeled "(a)" is a plot of voltage spectral density in the frequency domain. It is a logarithmic plot that depicts the spectral density of a signal, specifically the mean-squared voltage spectral density, denoted as \( V_n^2(f) \).

1. **Type of Graph and Function:**
- This is a logarithmic plot showing the spectral density of a voltage signal.

2. **Axes Labels and Units:**
- The horizontal axis represents frequency in hertz (Hz) and is logarithmically scaled, ranging from 0.1 Hz to 1,000 Hz.
- The vertical axis represents the spectral density in units of microvolts squared per hertz \((\mu V)^2/\text{Hz}\), also on a logarithmic scale, ranging from 1 to 1,000 \((\mu V)^2/\text{Hz}\).

3. **Overall Behavior and Trends:**
- The graph starts with a high spectral density at low frequencies, around 1,000 \((\mu V)^2/\text{Hz}\), and decreases as the frequency increases.
- The decrease is initially sharp, then gradually becomes more moderate, showing a downward trend throughout the frequency range.

4. **Key Features and Technical Details:**
- The spectral density decreases significantly from low to high frequencies, indicating that the noise power is more concentrated at lower frequencies.
- There are no specific peaks or valleys; the curve smoothly transitions from high to low values.

5. **Annotations and Specific Data Points:**
- The graph is annotated with the label "Spectral density" indicating the type of data represented.
- No specific numerical values or markers are highlighted on the curve, but the axes provide a clear logarithmic scale for both frequency and spectral density.
image_name:(b)
description:The graph labeled (b) is a plot of root spectral density, specifically showing the voltage spectral density in the frequency domain. This is a logarithmic plot with the frequency (Hz) on the horizontal axis and the root spectral density (V<sub>n</sub>(f)) on the vertical axis.

1. **Axes Labels and Units:**
- **Horizontal Axis:** Frequency in Hertz (Hz) is plotted on a logarithmic scale, ranging from 0.1 Hz to 1,000 Hz.
- **Vertical Axis:** Root spectral density in microvolts per root Hertz (µV/√Hz) is also on a logarithmic scale, ranging from 1.0 µV/√Hz to 31.6 µV/√Hz.

2. **Overall Behavior and Trends:**
- The graph shows a decreasing trend in root spectral density as frequency increases.
- The curve starts at a high value around 31.6 µV/√Hz at 0.1 Hz and decreases steadily.
- The decrease is not linear, exhibiting a smooth downward curve as frequency increases.

3. **Key Features and Technical Details:**
- The curve indicates that the root spectral density is higher at lower frequencies and decreases as the frequency increases.
- There is no sharp cutoff or inflection point, suggesting a gradual roll-off.

4. **Annotations and Specific Data Points:**
- The graph is labeled "Root spectral density" to distinguish it from the regular spectral density.
- No specific numerical annotations or markers are present beyond the axis labels.

This graph is useful for understanding how the root spectral density of a voltage signal varies with frequency, emphasizing the decrease in noise power per root Hertz as the frequency increases.

Fig. 9.3 Example of voltage spectral density (frequency domain), for (a) spectral density, and (b) root spectral density.

Since the spectral density measures the mean-squared value over a 1-Hz bandwidth, one can obtain the total mean-squared value by integrating the spectral density over the entire frequency spectrum. Thus, the rms value of a noise signal can also be obtained in the frequency domain using the following relationship:

$$
\begin{equation*}
V_{n(r m s)}^{2}=\int_{0}^{\infty} V_{n}^{2}(f) d f \tag{9.19}
\end{equation*}
$$

Key Point: The mean square value of a noise signal is the integral of its spectral density over all frequencies.
and similarly for current noise,

$$
\begin{equation*}
I_{n(r m s)}^{2}=\int_{0}^{\infty} I_{n}^{2}(f) d f \tag{9.20}
\end{equation*}
$$

More generally, the rms noise within a specified frequency range is obtained by integrating the noise spectral density over that frequency range. For example, the rms voltage noise over the frequency range $f_{1}<f<f_{2}$ is

$$
\begin{equation*}
\int_{f_{1}}^{f_{1}} V_{n}^{2}(f) d f \tag{9.21}
\end{equation*}
$$

Finally, $\mathrm{V}_{\mathrm{n}}^{2}(\mathrm{f})$ is rigorously defined as the Fourier transform of the autocorrelation function of the timedomain signal, $\mathrm{v}_{\mathrm{n}}(\mathrm{t})$. This relationship is known as the Wiener-Khinchin theorem. The relationship just shown defines a one-sided spectral density function since the noise is integrated only over positive frequencies as opposed to both negative and positive frequencies, again primarily for historical reasons. A two-sided definition results in the spectral density being divided by two since, for real-valued signals, the spectral density is the same for positive and negative frequencies, and the total mean-squared value obtained by integrating over both positive and negative frequencies remains unchanged.

#### EXAMPLE 9.3

What mean-squared value would be measured on the signal shown in Fig. 9.3 at 100 Hz when a resolution bandwidth of 30 Hz is used on a spectrum analyzer? Answer the same question for a $0.1-\mathrm{Hz}$ resolution bandwidth.

#### Solution

Since the portion of spectral density function is flat at about 100 Hz , the measured value should simply be proportional to the bandwidth. Since the noise spectral density is $10(\mu \mathrm{~V})^{2} / \mathrm{Hz}$ at 100 Hz , the output of a $30-\mathrm{Hz}$ filter is $30 \mathrm{~Hz} \times 10(\mu \mathrm{~V})^{2} / \mathrm{Hz}=300(\mu \mathrm{~V})^{2}$ (or an rms value of $\sqrt{300} \mu \mathrm{~V}$ ).

For a $0.1-\mathrm{Hz}$ bandwidth, the measured value would be 10 times smaller than for a $1-\mathrm{Hz}$ bandwidth, resulting in a value of $1(\mu \mathrm{~V})^{2}($ or an rms value of $1 \mu \mathrm{~V})$.

### 9.2.2 White Noise

One common type of noise is white noise. A noise signal is said to be white if its spectral density is constant over a given frequency. In other words, a white noise signal would have a flat spectral density, as shown in Fig. 9.4, where $\mathrm{V}_{\mathrm{n}}(\mathrm{f})$ is given by

$$
\begin{equation*}
V_{n}(f)=V_{n w} \tag{9.22}
\end{equation*}
$$

Key Point: White noise has a spectral density that is constant over all frequencies.
and $\mathrm{V}_{\mathrm{nw}}$ is a constant value.
Substituting (9.22) into (9.19) suggests that white noise has infinite power. However, this is not a problem in practice since a finite capacitance is always present to bandlimit the noise and make the integral in (9.19) converge.
image_name:Fig. 9.4
description:The graph depicted in Fig. 9.4 is a spectral density plot representing white noise. It is a type of Bode plot, displaying the root spectral density of the noise across a range of frequencies.

1. **Axes Labels and Units:**
- The horizontal axis represents frequency \( f \) in hertz (Hz) and is scaled logarithmically, with markers at 0.1, 1, 10, 100, and 1,000 Hz.
- The vertical axis represents the root spectral density \( V_n(f) \) in microvolts per square root hertz (\( \mu V/\sqrt{Hz} \)). The scale is linear with significant markers at 1.0, 3.2, and 10 \( \mu V/\sqrt{Hz} \).

2. **Overall Behavior and Trends:**
- The graph shows a constant value across all frequencies, indicating that the spectral density of the white noise does not change with frequency. This is characteristic of white noise, which has a flat spectral density.

3. **Key Features and Technical Details:**
- The plot is a straight horizontal line at \( V_{nw} = 3.2 \mu V/\sqrt{Hz} \), demonstrating the constant spectral density of white noise.
- There are no peaks, valleys, or variations, reinforcing the idea of infinite bandwidth for ideal white noise.

4. **Annotations and Specific Data Points:**
- The graph is annotated with the value \( V_n(f) = V_{nw} = 3.2 \mu V/\sqrt{Hz} \), emphasizing the constant nature of the noise's spectral density.

This graph effectively illustrates the concept of white noise having a uniform spectral density across different frequencies.

Fig. 9.4 An example of a white noise signal.

### 9.2.3 1/f, or Flicker, Noise

Another common noise shape is that of $1 /$ f, or flicker, noise. ${ }^{3}$ The spectral density, $\mathrm{V}_{\mathrm{n}}^{2}(\mathrm{f})$, of $1 / \mathrm{f}$ noise is approximated by

$$
\begin{equation*}
V_{n}^{2}(f)=\frac{k_{v}^{2}}{f} \tag{9.23}
\end{equation*}
$$

where $k_{v}$ is a constant. Thus, the spectral density is inversely proportional to frequency, and hence the term " $1 / \mathrm{f}$ noise." In terms of root spectral density, $1 / \mathrm{f}$ noise is given by

$$
\begin{equation*}
V_{n}(f)=\frac{k_{v}}{\sqrt{f}} \tag{9.24}
\end{equation*}
$$

Key Point: Flicker noise, or 1/f-noise, has a spectral density proportional to 1ff. Hence, itfalls offat -10 dB/decade.

Note that it is inversely proportional to $\sqrt{f}$ (rather than f ). An example of a signal having both $1 / \mathrm{f}$ and white noise is shown in Fig. 9.5. Note that the $1 / \mathrm{f}$ noise falls off at a rate of $-10 \mathrm{~dB} /$ decade since it is inversely proportional to $\sqrt{\mathrm{f}}$. The intersection of the $1 / \mathrm{f}$ and white noise curves is often referred to as the $1 /$ f noise corner. (It occurs at 10 Hz in Fig. 9.5.)
image_name:Fig. 9.5
description:The graph in Fig. 9.5 is a Bode plot illustrating the noise characteristics of a signal with both $1/f$ noise and white noise components.

1. **Type of Graph and Function**:
- This is a Bode plot showing the root spectral density of noise as a function of frequency.

2. **Axes Labels and Units**:
- The x-axis represents frequency ($f$) in Hertz (Hz), and it is plotted on a logarithmic scale, covering a range from 0.1 Hz to 1000 Hz.
- The y-axis represents the noise voltage spectral density $V_n(f)$ in microvolts per square root Hertz (µV/√Hz).

3. **Overall Behavior and Trends**:
- The graph shows two distinct regions: a decreasing trend and a constant trend.
- In the lower frequency range (0.1 Hz to 10 Hz), the graph exhibits a decreasing trend, indicating $1/f$ noise which falls off at a rate of -10 dB per decade.
- Beyond 10 Hz, the noise level becomes constant, indicating the dominance of white noise.

4. **Key Features and Technical Details**:
- The $1/f$ noise corner occurs at 10 Hz, where the characteristics of the noise transition from $1/f$ noise to white noise.
- The slope of the $1/f$ noise region is marked as -10 dB/decade, reflecting its inverse proportionality to the square root of frequency.
- The formula provided on the chart is $V_n^2(f) \approx \frac{(3.2 \times 10^{-6})^2}{f} + (1 \times 10^{-6})^2$, indicating the mathematical representation of the noise components.

5. **Annotations and Specific Data Points**:
- The graph is annotated with labels indicating the $1/f$ noise region and the white noise region.
- Specific points on the y-axis are marked at 10, 3.2, and 1 µV/√Hz, providing reference levels for the noise spectral density.
- The transition at 10 Hz is highlighted as the $1/f$ noise corner, a critical point where the noise characteristics change.

Fig. 9.5 A noise signal that has both $1 / f$ and white noise.

Substituting (9.23) into (9.21) gives the power of a $1 / f$ noise source over a finite frequency range $f_{1}<f<f_{2}$.

$$
\begin{equation*}
\int_{f_{1}}^{f_{1}} \frac{k_{v}^{2}}{f} d f=k_{v}^{2} \ln \left(\frac{f_{2}}{f_{1}}\right) \tag{9.25}
\end{equation*}
$$

Hence, the noise power in every decade range of frequencies is equal to $\mathrm{k}_{v}^{2} \ln (10) \cong 2.3 \mathrm{k}_{v}^{2}$. Integration of $1 / \mathrm{f}$ noise all the way down to dc yields infinite power, but in practical cases, finite and reasonable values are obtained even when the lower limit of integration is very low.

#### EXAMPLE 9.4

Find the rms noise voltage of a $1 / \mathrm{f}$ noise source with $\mathrm{k}_{v}^{2}=\left(50 \mathrm{nV}{ }^{2}\right)$ integrating over the frequency range 1 Hz to 100 MHz . What is its rms noise voltage if instead the lower limit of integration is decreased to 10 nHz ?

#### Solution

The range 1 Hz to 100 MHz encompasses 8 decades. Hence, the rms noise voltage over that range is $\sqrt{8 \cdot 2.3 \cdot \mathrm{k}_{v}^{2}}=0.215 \mu \mathrm{~V}$. Decreasing the lower frequency limit to 10 nHz increases the rms noise voltage to $\sqrt{16 \cdot 2.3 \cdot \mathrm{k}_{\mathrm{v}}^{2}}=0.303 \mu \mathrm{~V}$. Circuit noise at frequencies around 10 nHz will only be observed after a circuit has been in continuous operation for more than 1 year. In practice, over such a long time, temperature and aging effects will cause shifts in device performance that are virtually indistinguishable from the 1/f noise.

### 9.2.4 Filtered Noise

Consider the case of a noise signal, $\mathrm{V}_{\mathrm{ni}}(\mathrm{f})$, being filtered by the transfer function $\mathrm{A}(\mathrm{s})$, as shown in Fig. 9.6. Here, $\mathrm{A}(\mathrm{s})$ represents a linear transfer function as a result of some circuit amplification, filtering, or both. The following relationship between the input and output signals can be derived using the definition of the spectral density.

$$
\begin{equation*}
V_{n o}^{2}(f)=|A(j 2 \pi f)|^{2} V_{n i}^{2}(f) \tag{9.26}
\end{equation*}
$$

The term $2 \pi f$ arises here since, for physical frequencies, we replace $s$ with $j \omega=j 2 \pi f$. Note that the output spectral density is a function only of the magnitude of the transfer function, and not its phase. As a result of (9.26), the total output mean-squared value is given by

$$
\begin{equation*}
V_{\text {no }(\mathrm{rms})}^{2}=\int_{0}^{\infty}|\mathrm{A}(\mathrm{j} 2 \pi \mathrm{f})|^{2} V_{\mathrm{ni}}^{2}(\mathrm{f}) \mathrm{df} \tag{9.27}
\end{equation*}
$$

If we wish to work with root spectral densities, we can take the square root of both sides of (9.26) resulting in

$$
\begin{equation*}
V_{n o}(f)=|A(j 2 \pi f)| V_{n i}(f) \tag{9.28}
\end{equation*}
$$

image_name:Fig. 9.6
description:The system block diagram in Fig. 9.6 illustrates the application of a transfer function to a noise signal. It consists of the following main components:

1. **Input Noise Signal**: The input to the system is denoted as \( V_{ni}^2(f) \), representing the power spectral density of the input noise signal.

2. **Transfer Function Block**: The core component is a block labeled \( A(s) \), which represents the system's transfer function or filter. This block processes the input noise signal.

3. **Output Noise Signal**: The output from the transfer function block is denoted as \( V_{no}^2(f) \) and \( V_{no}(f) \). These represent the power spectral density and root spectral density of the output noise signal, respectively.

**Flow of Information**:
- The input noise signal \( V_{ni}^2(f) \) enters the transfer function block \( A(s) \).
- The transfer function modifies the input signal, shaping its spectral density according to its magnitude response.
- The output from the block is a transformed noise signal \( V_{no}^2(f) = |A(j2\pi f)|^2 V_{ni}^2(f) \) and \( V_{no}(f) = |A(j2\pi f)| V_{ni}(f) \), indicating how the noise is altered by the filter.

**Labels and Annotations**:
- The diagram clearly labels the input and output signals with their respective spectral density expressions.
- The transfer function \( A(s) \) is central to the diagram, emphasizing its role in shaping the noise signal.

**Overall System Function**:
The primary function of this system is to filter or shape the input noise signal's spectral density using a transfer function. The system demonstrates how the magnitude response of the transfer function affects the output noise signal. This is crucial in applications where noise characteristics need to be controlled or modified, such as in signal processing and communication systems.

Fig. 9.6 Applying a transfer function (i.e. filter) to a noise signal.
image_name:Fig. 9.7 Filtered uncorrelated noise sources contributing to total output noise.
description:The system block diagram titled "Fig. 9.7 Filtered uncorrelated noise sources contributing to total output noise" illustrates the process of filtering multiple uncorrelated noise sources and their contribution to the total output noise.

1. **Main Components:**
- **Uncorrelated Noise Sources:** Three different noise sources, labeled as \(V_{n1}(f)\), \(V_{n2}(f)\), and \(V_{n3}(f)\), serve as the inputs to the system. These represent distinct noise signals with different spectral characteristics.
- **Filters (Transfer Functions):** Each noise source is passed through a filter, represented by blocks labeled \(A_1(s)\), \(A_2(s)\), and \(A_3(s)\). These filters are characterized by their respective transfer functions, \(A_i(s)\), which modify the spectral density of the input noise signals.
- **Summing Junction:** The outputs of the filters are combined at a summing junction, which calculates the total output noise \(V_{no}(f)\).

2. **Flow of Information or Control:**
- Each noise source \(V_{ni}(f)\) is individually processed by its corresponding filter \(A_i(s)\), which adjusts the magnitude response of the noise signal.
- The filtered signals are then directed to a summing junction, where they are combined to form the total output noise \(V_{no}(f)\).
- The flow of information is linear, moving from the noise sources through the filters to the summing junction.

3. **Labels, Annotations, and Key Indicators:**
- The diagram includes mathematical expressions indicating the relationship between the input noise signals and the output noise. The total output noise \(V_{no}(f)\) is given by the equation:
\[
V_{no}(f) = \left( \sum_{i=1,2,3} |A_i(j2\pi f)|^2 V_{ni}^2(f) \right)^{1/2}
\]
- This equation highlights how the magnitude of each transfer function \(|A_i(j2\pi f)|\) affects the contribution of each noise source to the total output noise.

4. **Overall System Function:**
- The primary function of this system is to demonstrate how uncorrelated noise sources, when filtered through different transfer functions, contribute to the overall noise output. Each filter shapes the root spectral density of its respective noise source, and the summing junction aggregates these contributions to produce the total output noise. This process is essential in understanding how noise characteristics are controlled and manipulated in signal processing applications.

Fig. 9.7 Filtered uncorrelated noise sources contributing to total output noise.

Key Point: Passing a noise signal through a circuit shapes its root spectral density by the circuit's magnitude response.

Key Point: Uncorrelated noise signals remain uncorrelated, even when filtered by a circuit's magnitude response.

The relationship in (9.28) should make intuitive sense since it indicates that the transfer function simply shapes the root spectral density of the input noise signal. It is important to note here that the root spectral density is simply shaped by $|A(j 2 \pi f)|$, whereas the spectral density is shaped by $|\mathrm{A}(\mathrm{j} 2 \pi \mathrm{f})|^{2}$, as seen by $(9.26)$. Hence, we see the benefit in dealing with the root spectral density rather than the spectral density. Specifically, straightforward transfer function analysis is applied when using root spectral densities, whereas squared terms are required to deal with spectral densities.

It is also of interest to consider the case of multiple uncorrelated noise sources that are each filtered and summed together. For example, consider the system shown in Fig. 9.7 in which three filtered, uncorrelated noise sources combine to form the total output noise, $\mathrm{V}_{\text {no }}(\mathrm{f})$. In this case, one can show that if the input random signals are uncorrelated, the filter outputs are also uncorrelated. As a result, the output spectral density is given by

$$
\begin{equation*}
V_{n o}^{2}(f)=\sum_{i=1,2,3}\left|A_{i}(j 2 \pi f)\right|^{2} V_{n i}^{2}(f) \tag{9.29}
\end{equation*}
$$

#### EXAMPLE 9.5

Consider a noise signal, $\mathrm{V}_{\mathrm{ni}}(\mathrm{f})$, that has a white root spectral density of $20 \mathrm{nV} / \sqrt{\mathrm{Hz}}$, as shown in Fig. 9.8(a). Find the total noise rms value between dc and 100 kHz . What is the total noise rms value if it is filtered by the RC filter shown in Fig. 9.8(b), where it is assumed the RC filter is noise free?

#### Solution

For the noise mean-square value from dc to 100 kHz of $\mathrm{V}_{\mathrm{ni}}(\mathrm{f})$, we have

$$
\begin{equation*}
V_{n i(r m s)}^{2}=\int_{0}^{10^{5}} 20^{2} \mathrm{df}=4 \times 10^{7}(\mathrm{nV})^{2} \tag{9.30}
\end{equation*}
$$

resulting in an rms value of $\mathrm{V}_{\text {ni(rms) }}=6.3 \mu \mathrm{~V}$ rms . Note that, for this simple case, one could also obtain the rms value by multiplying $20 \mathrm{nV} / \sqrt{\mathrm{Hz}}$ by the square root of the frequency span, or $\sqrt{100 \mathrm{kHz}}$, resulting in $6.3 \mu \mathrm{~V} \mathrm{rms}$.

For the filtered signal, $\mathrm{V}_{\mathrm{no}}(\mathrm{f})$, we find that the RC filter has the frequency response shown in Fig. 9.8(c). Therefore, we can multiply the root spectral density of $\mathrm{V}_{\text {ni }}(\mathrm{f})$ with the frequency response, $|A(j 2 \pi f)|$, to obtain the root spectral density of $\mathrm{V}_{\text {no }}(\mathrm{f})$, as shown in Fig. 9.8(d). Mathematically, the output root spectral density is given by

$$
\begin{equation*}
V_{n o}(f)=\frac{20 \times 10^{-9}}{\sqrt{1+\left(\frac{\mathrm{f}}{\mathrm{f}_{0}}\right)^{2}}} \tag{9.31}
\end{equation*}
$$

image_name:(a)
description:The graph labeled (a) is a spectral density plot for $V_{ni}(f)$. It is a type of frequency-domain graph showing the root spectral density of the input voltage noise.

1. **Axes Labels and Units:**
- The vertical axis is labeled $V_{ni}(f)$ and is measured in nanovolts per square root hertz (nV/√Hz).
- The horizontal axis represents frequency ($f$) in hertz (Hz) and is shown on a logarithmic scale with markers at 1, 10, 100, 10³, and 10⁴ Hz.

2. **Overall Behavior and Trends:**
- The graph shows a constant value of 20 nV/√Hz across the entire frequency range from 1 Hz to 10⁴ Hz. This indicates that the input voltage noise spectral density is frequency-independent over this range, suggesting that the noise is white.

3. **Key Features and Technical Details:**
- The spectral density remains flat at 20 nV/√Hz, with no peaks, valleys, or inflection points throughout the observed frequency range.
- There are no annotations or specific data points marked on the graph, as the value is constant.

4. **Annotations and Specific Data Points:**
- There are no additional annotations or reference lines present in this graph. The constant level of 20 nV/√Hz is the key feature of this plot.
image_name:(b)
description:
[
name: R, type: Resistor, value: 1kΩ, ports: {N1: Vni(f), N2: Vno(f)}
name: C, type: Capacitor, value: 0.159μF, ports: {Np: Vno(f), Nn: GND}
]
extrainfo:This is an RC low-pass filter circuit, where the resistor R and capacitor C form a network to filter the input noise voltage Vni(f), resulting in an output noise voltage Vno(f). The cutoff frequency f0 is given by f0 = 1/(2πRC).
image_name:(c)
description:The graph labeled (c) is a Bode plot representing the frequency response of an RC filter.

1. **Type of Graph and Function:**
- This is a Bode plot showing the magnitude of the frequency response of an RC filter.

2. **Axes Labels and Units:**
- The x-axis represents frequency (f) in hertz (Hz) on a logarithmic scale, ranging from 1 Hz to 10,000 Hz (10^4 Hz).
- The y-axis represents the magnitude of the frequency response |A(j2πf)| in decibels (dB).

3. **Overall Behavior and Trends:**
- The graph shows a flat response at 0 dB for low frequencies up to the cutoff frequency, indicating no attenuation in this range.
- Beyond the cutoff frequency, the magnitude decreases linearly, showing a downward slope.

4. **Key Features and Technical Details:**
- The cutoff frequency (f₀) is marked at 1,000 Hz (10^3 Hz), where the slope begins.
- The slope beyond the cutoff frequency is approximately -20 dB/decade, which is typical for a first-order RC low-pass filter.

5. **Annotations and Specific Data Points:**
- The graph is annotated with the transfer function A(s) = 1 / (1 + s/2πf₀), indicating the mathematical model of the frequency response.
- The 0 dB line is clearly marked, showing the reference level for the magnitude response.
image_name:(d)
description:The graph (d) is a plot of the spectral density of $V_{no}(f)$, the output noise voltage, as a function of frequency.

1. **Type of Graph and Function:**
- This is a frequency-domain plot showing the root spectral density of noise voltage.

2. **Axes Labels and Units:**
- The x-axis represents frequency (f) in hertz (Hz) and is plotted on a logarithmic scale, ranging from 1 Hz to 10,000 Hz.
- The y-axis represents the root spectral density of the noise voltage $V_{no}(f)$ in nanovolts per square root hertz (nV/√Hz).

3. **Overall Behavior and Trends:**
- The graph shows a flat region at low frequencies, indicating a constant spectral density of 20 nV/√Hz.
- As frequency increases beyond a certain point, the spectral density decreases, showing a downward trend.

4. **Key Features and Technical Details:**
- The flat region extends from the lowest frequency up to approximately 1,000 Hz (10^3 Hz), where the spectral density remains constant at 20 nV/√Hz.
- Beyond 1,000 Hz, the spectral density decreases, following the behavior of a single-pole low-pass filter characterized by the RC network described in the context.
- The decrease in spectral density is consistent with the transfer function $A(s) = \frac{1}{1 + s/2\pi f_0}$, where $f_0 = 1,000$ Hz is the cutoff frequency.

5. **Annotations and Specific Data Points:**
- The cutoff frequency is marked at 1,000 Hz, which is the point where the spectral density starts to decrease.
- The graph does not show any specific annotations or markers beyond the axes labels and the flat and sloped regions.

Fig. 9.8 (a) Spectral density for $\mathrm{V}_{\text {ni }}$ (f). (b) RC filter to shape noise. (c) RC filter frequency response. (d) Spectral density for $\mathrm{V}_{\text {no }}(\mathrm{f})$.
where $f_{0}=10^{3}$. Thus, the noise mean-squared value of $\mathrm{V}_{n o}(\mathrm{f})$ between dc and 100 kHz is given by

$$
\begin{align*}
V_{n o(\mathrm{~ms})}^{2} & =\int_{0}^{10^{5}} \frac{20^{2}}{1+\left(\frac{f}{f_{0}}\right)^{2}} d f=\left.20^{2} f_{0} \arctan \left(f / f_{0}\right)\right|_{0} ^{10^{5}}  \tag{9.32}\\
& =6.24 \times 10^{5}(\mathrm{nV})^{2}
\end{align*}
$$

which results in an rms value of $\mathrm{V}_{\text {no(rms) }}=0.79 \mu \mathrm{~V}$ rms. Note that the noise rms value of $\mathrm{V}_{\text {no }}(\mathrm{f})$ is almost $1 / 10$ that of $\mathrm{V}_{\mathrm{ni}}(\mathrm{f})$ since high-frequency noise above 1 kHz was filtered. The lesson here is that you should not design circuits for larger bandwidths than your signal requires, otherwise noise performance suffers.

### 9.2.5 Noise Bandwidth

We just saw that the spectral density function is determined by the noise power within each 1-Hz bandwidth. Thus, in theory, one could measure the spectral density function by filtering a noise signal with a brick-wall bandpass filter having a $1-\mathrm{Hz}$ bandwidth. The term brick wall implies here that the $1-\mathrm{Hz}$ bandwidth of the filter is passed with a gain of one, whereas all other frequencies are entirely eliminated. However, practical filters can only approach a brick-wall response as their complexity (i.e. filter order) is increased. Thus, for lower-order filters with a 1-Hz passband, more noise

Key Point: The noise bandwidth of a given filter is equal to the frequency span of a brick-wall filter that has the same rms output noise as the given filter has when white noise is applied to both filters, assuming the same peak gain for both filters.
power is passed than what is simply in a $1-\mathrm{Hz}$ bandwidth. To account for the fact that practical filters have more gradual stopband characteristics, the term noise bandwidth is defined. The noise bandwidth of a given filter is equal to the frequency span of a brick-wall filter that has the same rms output noise as the given filter has when white noise is applied to both filters, assuming the same peak gain for
image_name:(a)
description:1. **Type of Graph and Function:**
- The graph is a frequency response plot, specifically a Bode plot magnitude response for a first-order low-pass filter.

2. **Axes Labels and Units:**
- The vertical axis represents magnitude in decibels (dB).
- The horizontal axis represents frequency, labeled as \( f \), with units in terms of \( f_0 \), the cutoff frequency.
- The frequency scale is logarithmic, indicated by the spacing of \( f_0/100, f_0/10, f_0, \) and \( 10f_0 \).

3. **Overall Behavior and Trends:**
- The magnitude response begins at 0 dB for low frequencies (\( f < f_0 \)).
- At the cutoff frequency \( f_0 \), the response starts to decline.
- The slope of the decline is \(-20 \) dB/decade, indicating a first-order roll-off.

4. **Key Features and Technical Details:**
- The cutoff frequency \( f_0 \) is marked on the horizontal axis.
- The graph shows a typical first-order low-pass filter behavior, where the gain remains constant at 0 dB until the cutoff frequency, after which it decreases at a rate of \(-20 \) dB/decade.
- The equation for the transfer function \( A(s) = \frac{1}{1 + s/2\pi f_0} \) is provided, indicating the mathematical model of the filter.

5. **Annotations and Specific Data Points:**
- An annotation indicates the slope of \(-20 \) dB/decade beyond the cutoff frequency.
- The plot is labeled as Fig. 9.9(a), distinguishing it from other diagrams.
image_name:(b)
description:The graph labeled as (b) represents the magnitude response of a brick-wall filter. This is a type of idealized filter response characterized by a perfectly flat passband and an abrupt transition to the stopband.

1. **Type of Graph and Function:**
- The graph is a frequency response plot, showing the magnitude of the filter's response in decibels (dB) against frequency.

2. **Axes Labels and Units:**
- The vertical axis represents magnitude in decibels (dB).
- The horizontal axis represents frequency, marked in terms of the normalized frequency $f_0$.
- Frequency points are marked at $f_0/100$, $f_0/10$, $f_0$, and a special point $f_x = \pi/2 \cdot f_0$.

3. **Overall Behavior and Trends:**
- The graph shows a flat response at 0 dB from the start until the cutoff frequency $f_0$.
- Beyond $f_0$, the response drops sharply to -20 dB, indicating a rapid transition to the stopband.

4. **Key Features and Technical Details:**
- The passband is perfectly flat with a gain of 0 dB up to the cutoff frequency $f_0$.
- The transition from passband to stopband is abrupt, characteristic of the idealized "brick-wall" filter.
- The stopband begins immediately after $f_0$, with the magnitude dropping to -20 dB.
- The point $f_x = \pi/2 \cdot f_0$ is an annotation marking a specific frequency related to the filter's characteristics.

5. **Annotations and Specific Data Points:**
- The graph includes annotations highlighting the frequency points and the sharp drop at the cutoff frequency $f_0$.
- There is no gradual slope like in the first-order response; instead, it is a clear step function from the passband to the stopband.

Fig. 9.9 (a) A first-order, low-pass response, and (b) a brick-wall filter that has the same peak gain and area as the first-order response.
both filters. In other words, given a filter response with peak gain $\mathrm{A}_{0}$, the noise bandwidth is the width of a rectangular filter that has the same area and peak gain, $\mathrm{A}_{0}$, as the original filter.

For example, consider a first-order, low-pass response with a 3-dB bandwidth of $\mathrm{f}_{0}$, as shown in Fig. 9.9(a). Such a response would occur from the RC filter shown in Fig. $9.8(b)$ with $f_{0}=(1 / 2 \pi R C)$. The transfer function of $A(s)$ is given by

$$
\begin{equation*}
A(s)=\frac{1}{1+\frac{s}{2 \pi f_{0}}} \tag{9.33}
\end{equation*}
$$

This results in the magnitude response of $A(s)$ being equal to

$$
\begin{equation*}
|\mathrm{A}(\mathrm{j} 2 \pi \mathrm{f})|=\left(\frac{1}{1+\left(\frac{\mathrm{f}}{\mathrm{f}_{0}}\right)^{2}}\right)^{1 / 2} \tag{9.34}
\end{equation*}
$$

An input signal, $\mathrm{V}_{\mathrm{ni}}(\mathrm{f})$, is a white noise source given by

$$
\begin{equation*}
V_{n i}(f)=V_{n w} \tag{9.35}
\end{equation*}
$$

where $V_{n w}$ is a constant. The total output noise rms value of $V_{n o}(f)$ is equal to

$$
\begin{equation*}
V_{\mathrm{no}(\mathrm{rms})}^{2}=\int_{0}^{\infty} \frac{\mathrm{V}_{\mathrm{nw}}^{2}}{1+\left(\frac{f}{f_{0}}\right)^{2}} \mathrm{df}=\left.\mathrm{V}_{\mathrm{nw}}^{2} \mathrm{f}_{0} \arctan \left(\frac{\mathrm{f}}{\mathrm{f}_{0}}\right)\right|_{0} ^{\infty}=\frac{\mathrm{V}_{\mathrm{nw}}^{2} \pi f_{0}}{2} \tag{9.36}
\end{equation*}
$$

If this same input signal, $\mathrm{V}_{\mathrm{ni}}(\mathrm{f})$, is applied to the filter shown in Fig. $9.9(b)$, then the total output noise rms value equals,

$$
\begin{equation*}
V_{\text {brick(rms) }}^{2}=\int_{0}^{f_{x}} V_{n w}^{2} d f=V_{n w}^{2} f_{x} \tag{9.37}
\end{equation*}
$$

Finally, equating the two output noise rms values, $\mathrm{V}_{\text {no(rms) }}=\mathrm{V}_{\text {brick(rms) }}$, results in

$$
\begin{equation*}
\mathrm{f}_{\mathrm{x}}=\frac{\pi \mathrm{f}_{0}}{2} \tag{9.38}
\end{equation*}
$$

Thus, the noise bandwidth of a first-order, low-pass filter with a 3-dB bandwidth of $f_{0}$ equals $\pi\left(f_{0} / 2\right)$. Note that, for the common case in which a firstorder circuit is realized by a capacitor, C , and the resistance seen by that capacitor, $\mathrm{R}_{\text {eq }}$, then

$$
\begin{equation*}
\mathrm{f}_{0}=\frac{1}{2 \pi \mathrm{R}_{\mathrm{eq}} \mathrm{C}} \tag{9.39}
\end{equation*}
$$

and the noise bandwidth is given by

$$
\begin{equation*}
f_{x}=\frac{1}{4 R_{e q} C} \tag{9.40}
\end{equation*}
$$

The advantage of knowing the noise bandwidth of a filter is that, when white noise is applied to the filter input, the total output noise mean-squared value is easily calculated by multiplying the spectral density by the noise bandwidth. Specifically, in the first-order case just described, the total output noise mean-squared value, $V_{\text {no(rms) }}^{2}$, is equal to

$$
\begin{equation*}
V_{\mathrm{no}(\mathrm{~ms})}^{2}=\mathrm{V}_{\mathrm{nw}}^{2} \mathrm{f}_{\mathrm{x}}=\mathrm{V}_{\mathrm{nw}}^{2}\left(\frac{\pi}{2}\right) \mathrm{f}_{0} \tag{9.41}
\end{equation*}
$$

Similar results for noise-bandwidth relationships can be obtained for higher-order and bandpass filters.

### 9.2.6 Piecewise Integration of Noise

Although simulation and computer techniques can analyze circuits or systems quite precisely (depending on their modeling accuracy), it is often convenient to make approximations that are useful in the early design stages. Such approximations are particularly useful in noise analysis, where large inaccuracies occur naturally due to such things as unknown parasitic effects and incomplete noise models. One such approximation is the estimation of total noise by integrating over frequency with the assumption that piecewise-linear Bode diagrams are exact. With such an approximation, integration formulas become much simpler when one needs only to integrate under linear functions and add together the resulting portions. The following example demonstrates this approach.

#### EXAMPLE 9.6

Consider an input noise signal, $\mathrm{V}_{\mathrm{ni}}(\mathrm{f})$, being applied to the amplifier $\mathrm{A}(\mathrm{s})$, as shown in Fig. 9.10. Find the output noise rms value of $\mathrm{V}_{\mathrm{n}}$ considering only frequencies above 1 Hz .

#### Solution

As shown, the output root spectral density, $\mathrm{V}_{\text {no }}(\mathrm{f})$, is determined by the addition of the Bode diagrams for $\mathrm{V}_{\mathrm{ni}}(\mathrm{f}$ ) and $A(s)$. To perform piecewise integration of $V_{n o}(f)$, the frequency range is broken into four regions, $N_{1}$ through $\mathrm{N}_{4}$, as shown.

For the region $\mathrm{N}_{1}$, the total mean-square noise is given by

$$
\begin{equation*}
N_{1}^{2}=\int_{1}^{100} \frac{200^{2}}{f} \mathrm{df}=\left.200^{2} \ln (f)\right|_{1} ^{100}=1.84 \times 10^{5}(\mathrm{nV})^{2} \tag{9.42}
\end{equation*}
$$

In the region $\mathrm{N}_{2}$, we have

$$
\begin{equation*}
\mathrm{N}_{2}^{2}=\int_{100}^{10^{3}} 20^{2} \mathrm{df}=\left.20^{2} \mathrm{f}\right|_{100} ^{10^{3}}=3.6 \times 10^{5}(\mathrm{nV})^{2} \tag{9.43}
\end{equation*}
$$

image_name:A(s)
description:The system block diagram titled "A(s)" represents an amplifier system that processes an input noise signal \( V_{ni}(f) \) to produce an output noise signal \( V_{no}(f) \). The diagram is organized into three main components: the input noise spectrum, the amplifier gain, and the output noise spectrum, each plotted against frequency.

1. **Main Components:**
- **Input Noise Spectrum (\( V_{ni}(f) \))**: The top graph displays the root spectral density of the input noise in \( \text{nV}/\sqrt{\text{Hz}} \) over a frequency range from 1 Hz to 10 MHz. The noise decreases from 200 \( \text{nV}/\sqrt{\text{Hz}} \) at low frequencies to 20 \( \text{nV}/\sqrt{\text{Hz}} \) and remains constant up to 10 kHz.
- **Amplifier Gain (|A(j2\pi f)|)**: The middle graph shows the frequency response of the amplifier in decibels (dB). The gain is flat at 0 dB up to 1 kHz, increases to 20 dB between 1 kHz and 10 kHz, and remains constant before decreasing again.
- **Output Noise Spectrum (\( V_{no}(f) \))**: The bottom graph illustrates the root spectral density of the output noise. It shows a similar pattern to the input noise but is modified by the amplifier's gain characteristics.

2. **Flow of Information or Control:**
- The input noise \( V_{ni}(f) \) is fed into the amplifier block \( A(s) \), which modifies the noise based on its frequency response characteristics.
- The output noise \( V_{no}(f) \) is the result of this amplification process, reflecting the changes imposed by the gain across different frequency ranges.

3. **Labels, Annotations, and Key Indicators:**
- The frequency axis is logarithmically scaled from 1 Hz to 10 MHz.
- The regions \( N_1, N_2, N_3, \) and \( N_4 \) are marked on the frequency axis, corresponding to different noise characteristics and amplifier responses.
- A dotted line labeled "1/f curve" on the output noise graph indicates the expected noise behavior beyond the amplifier's bandwidth.

4. **Overall System Function:**
- The system functions as a noise amplifier, where the input noise is modified by the amplifier's frequency response. The amplifier selectively boosts or attenuates the noise at different frequencies, resulting in an output noise spectrum that reflects these modifications. The regions \( N_1, N_2, N_3, \) and \( N_4 \) highlight how the noise characteristics change across different frequency bands, with the amplifier's gain playing a crucial role in shaping the output noise profile.
image_name:V_{ni}(f)
description:The graph labeled "V_{ni}(f)" is a plot of the input noise voltage spectral density against frequency. This is a Bode plot, which is commonly used to represent the frequency response of systems.

1. **Axes Labels and Units:**
- The x-axis represents frequency in Hertz (Hz) and is plotted on a logarithmic scale, ranging from 1 Hz to 10^7 Hz.
- The y-axis represents the noise voltage spectral density in nanovolts per square root Hertz (nV/√Hz), also on a logarithmic scale, ranging from 2 nV/√Hz to 200 nV/√Hz.

2. **Overall Behavior and Trends:**
- The plot begins at a high value of 200 nV/√Hz at 1 Hz and shows a decreasing trend until it reaches a plateau.
- From 1 Hz to approximately 100 Hz, the spectral density decreases sharply.
- Between 100 Hz and 10^3 Hz, the plot shows a flat region indicating a constant spectral density.
- Beyond this region, the spectral density remains constant until about 10^4 Hz.

3. **Key Features and Technical Details:**
- The initial sharp decline is consistent with a 1/f noise characteristic, which is typical in low-frequency regions.
- The flat regions indicate areas where the noise voltage is independent of frequency, suggesting white noise characteristics.
- There are no marked peaks or valleys beyond the initial decline.

4. **Annotations and Specific Data Points:**
- The graph is divided into regions labeled N1, N2, N3, and N4, which correspond to different noise characteristics as described in the context.
- The transition between regions is smooth, with no abrupt changes in the slope of the curve.

This plot is used to understand how the input noise voltage varies across different frequency ranges, which is crucial for analyzing the performance of amplifiers and other electronic systems. The characteristics observed here are typical for analyzing the noise behavior in electronic circuits, especially in the context of amplifier design and evaluation.
image_name:|A(j2\pi f)|
description:The provided graph is a Bode plot, which is used to analyze the frequency response of a system. It consists of three main plots:

1. **Top Plot - Input Noise Voltage Density (Vni(f))**:
- **Type**: Logarithmic plot.
- **Axes**:
- X-axis: Frequency in Hertz (Hz), on a logarithmic scale ranging from 1 Hz to 10^7 Hz.
- Y-axis: Input noise voltage density \( V_{ni}(f) \) in nanovolts per square root Hertz \( \frac{nV}{\sqrt{Hz}} \).
- **Behavior**: The plot starts at 200 nV/√Hz at 1 Hz, decreasing sharply to 20 nV/√Hz at 100 Hz, and remains constant from 100 Hz to 10^7 Hz.

2. **Middle Plot - Magnitude of Transfer Function |A(j2πf)|**:
- **Type**: Logarithmic plot.
- **Axes**:
- X-axis: Frequency in Hertz (Hz), on a logarithmic scale ranging from 1 Hz to 10^7 Hz.
- Y-axis: Magnitude in decibels (dB).
- **Behavior**: The magnitude is constant at 0 dB from 1 Hz to 100 Hz, increases linearly to 20 dB at 10^3 Hz, remains constant at 20 dB until 10^4 Hz, and then decreases back to 0 dB at 10^6 Hz.

3. **Bottom Plot - Output Noise Voltage Density (Vno(f))**:
- **Type**: Logarithmic plot.
- **Axes**:
- X-axis: Frequency in Hertz (Hz), on a logarithmic scale ranging from 1 Hz to 10^7 Hz.
- Y-axis: Output noise voltage density \( V_{no}(f) \) in nanovolts per square root Hertz \( \frac{nV}{\sqrt{Hz}} \).
- **Behavior**: The output noise starts at 200 nV/√Hz at 1 Hz, decreases to a minimum at 100 Hz, ramps up to a peak at 10^4 Hz, and then decreases again.
- **Annotations**: A dotted line representing a \( 1/f \) curve is present, indicating the expected trend without amplification.

4. **Regions (N1, N2, N3, N4)**:
- These regions are marked on the bottom plot:
- **N1**: 1 Hz to 100 Hz, showing a decrease in noise.
- **N2**: 100 Hz to 10^3 Hz, where noise remains low.
- **N3**: 10^3 Hz to 10^4 Hz, where noise increases.
- **N4**: 10^4 Hz to 10^7 Hz, where noise decreases.

This Bode plot effectively illustrates how the system's input noise is affected by the frequency response of the amplifier, highlighting the regions where noise is minimized and the effects of the amplifier's gain on the output noise.
image_name:V_{no}(f)
description:The graph titled "V_{no}(f)" is a plot representing the output noise spectral density as a function of frequency. It is part of a set of graphs analyzing the behavior of an amplifier system, specifically illustrating how input noise is transformed by the amplifier.

1. **Type of Graph and Function:**
- The graph is a Bode plot, which is typically used to represent frequency response in terms of magnitude.

2. **Axes Labels and Units:**
- The horizontal axis represents frequency in Hertz (Hz) and is plotted on a logarithmic scale, ranging from 1 Hz to 10 million Hz (10^7 Hz).
- The vertical axis represents the noise spectral density, V_{no}(f), in nanovolts per square root Hertz (nV/√Hz), also on a logarithmic scale.

3. **Overall Behavior and Trends:**
- The graph can be divided into four regions: N1, N2, N3, and N4.
- In region N1 (1 Hz to 100 Hz), the noise spectral density decreases sharply from 200 nV/√Hz to around 20 nV/√Hz.
- In region N2 (100 Hz to 1000 Hz), the noise spectral density remains constant at approximately 20 nV/√Hz.
- In region N3 (1000 Hz to 10^4 Hz), the noise spectral density increases back to 200 nV/√Hz.
- In region N4 (10^4 Hz to 10^7 Hz), the noise spectral density decreases again, following a 1/f curve, indicating a typical high-frequency roll-off.

4. **Key Features and Technical Details:**
- Region N1 shows a steep decline in noise, which is typical of low-frequency noise reduction.
- Region N2 is flat, indicating a stable noise floor.
- Region N3 shows an increase in noise, possibly due to gain peaking or resonance within the amplifier.
- Region N4 follows a 1/f curve, a common characteristic in electronic noise behavior at high frequencies.

5. **Annotations and Specific Data Points:**
- The graph includes a dotted line in region N4, representing the 1/f curve.
- The regions N1, N2, N3, and N4 are clearly marked on the graph, indicating the frequency ranges and behavior of the noise spectral density within those ranges.
- The graph is part of a larger analysis that includes the input noise spectral density and the amplifier's frequency response, which are plotted in separate graphs above the main graph of interest.

Fig. 9.10 Root spectral densities and amplifier curve example. $\mathrm{V}_{\text {no }}(\mathrm{f})$ is the output noise that results from applying an input signal with noise $\mathrm{V}_{\mathrm{ni}}(\mathrm{f})$ to the amplifier $\mathrm{A}(\mathrm{s})$.

Region $\mathrm{N}_{3}$ ramps up rather than down, resulting in

$$
\begin{equation*}
\mathrm{N}_{3}^{2}=\int_{10^{0^{2}}}^{10^{4}} \frac{20^{2} \mathrm{f}^{2}}{\left(10^{3}\right)^{2}} \mathrm{df}=\left(\frac{20}{10^{3}}\right)^{2}\left[\left.\frac{1}{3} \mathrm{f}^{3}\right|_{10^{3}} ^{10^{4}}\right]=1.33 \times 10^{8}(\mathrm{nV})^{2} \tag{9.44}
\end{equation*}
$$

Finally, for region $\mathrm{N}_{4}$, we can use the noise bandwidth result of a first-order, low-pass response and simply remove the noise portion resulting from under $10^{4} \mathrm{~Hz}$. Specifically, we have

$$
\begin{align*}
\mathrm{N}_{4}^{2} & =\int_{10^{4}}^{\infty} \frac{200^{2}}{1+\left(\frac{\mathrm{f}}{10^{5}}\right)^{2}} \mathrm{df}=\int_{0}^{\infty} \frac{200^{2}}{1+\left(\frac{\mathrm{f}}{10^{5}}\right)^{2}} \mathrm{df}-\int_{0}^{10^{4}} 200^{2} \mathrm{df}  \tag{9.45}\\
& =200^{2}\left(\frac{\pi}{2}\right) 10^{5}-\left(200^{2}\right)\left(10^{4}\right)=5.88 \times 10^{9}(\mathrm{nV})^{2}
\end{align*}
$$

Thus, the total output noise can be estimated to be

$$
\begin{equation*}
\mathrm{V}_{\mathrm{no}(\mathrm{rms})}=\left(\mathrm{N}_{1}^{2}+\mathrm{N}_{2}^{2}+\mathrm{N}_{3}^{2}+\mathrm{N}_{4}^{2}\right)^{1 / 2}=77.5 \mu \mathrm{~V} \mathrm{rms} \tag{9.46}
\end{equation*}
$$

An interesting point to note here is that in the preceding example, $\mathrm{N}_{4}=76.7 \mu \mathrm{~V}$ rms is quite close to the total noise value of $77.5 \mu \mathrm{~V} \mathrm{rms}$. Thus, in practice, there is little need to find the noise contributions in the regions $N_{1}, N_{2}$, and $N_{3}$. Such an observation leads us to the 1/f noise tangent principle.

### 9.2.7 1/f Noise Tangent Principle

The $1 / f$ noise tangent principle is as follows: To determine the frequency region or regions that contribute the dominant noise, lower a 1/f noise line until it touches the spectral density curve-the total noise can be approximated by the noise in the vicinity of the 1/f line [Kennedy, 1988; Franco, 2002]. For example, lowering a $1 / \mathrm{f}$ line toward the root spectral density of $V_{n o}(\mathrm{f})$ in Fig. 9.10 indicates that the noise around $10^{5}$ dominates. The reason this simple rule works is that a curve proportional to $1 / \mathrm{x}$ results in equal

Key Point: To determine the frequency region or regions that contribute the dominant noise, lower a 1/f noise line until it touches the spectral density curve. The total noise can be approximated by the noise in the vicinity of the 1/fline.
power over each decade of frequency. Therefore, by lowering this constant power/frequency curve, the largest power contribution will touch it first. However, because the integration of $1 / x$ approaches infinity if either the upper bound is infinity or the lower bound is zero, one must be careful in cases where the spectral density curve runs parallel to a $1 / \mathrm{f}$ tangent line for an appreciable frequency span. For example, consider once again Fig. 9.10, where the region $\mathrm{N}_{1}$ runs parallel to the $1 / \mathrm{f}$ tangent line. However, in this example, region $\mathrm{N}_{1}$ does not contribute much noise since the noise was only integrated above 1 Hz . If a much lower frequency bound is used, this region can also contribute appreciable noise power.

## 9.3 NOISE MODELS FOR CIRCUIT ELEMENTS

There are three main fundamental noise mechanisms: thermal, shot, and flicker. In this section, we discuss noise models for popular circuit elements where all three mechanisms occur. However, first we briefly describe these noise phenomena.

Thermal noise is due to the thermal excitation of charge carriers in a conductor. This noise has a white spectral density and is proportional to absolute temperature. It is not dependent on bias conditions (dc bias current) and it occurs in all resistors (including semiconductors) above absolute zero temperature. Thus, thermal noise places fundamental limits on the dynamic range achievable in electronic circuits. It should be mentioned here that thermal noise is also referred to as Johnson or Nyquist noise since it was first observed by J. B. Johnson [Johnson, 1928] and analyzed using the second law of thermodynamics by H. Nyquist [Nyquist, 1928].

Shot noise was first studied by W. Schottky using vacuum-tube diodes [Schottky, 1918], but shot noise also occurs in pn junctions. This noise occurs because the dc bias current is not continuous and smooth but instead is a result of pulses of current caused by the flow of individual carriers. As such, shot noise is dependent on the dc bias current. It can also be modelled as a white noise source. Shot noise is also typically larger than thermal noise and is sometimes used to create white noise generators.

Flicker noise is the least understood of the three noise phenomena. It is found in all active devices as well as in carbon resistors, ${ }^{4}$ but it occurs only when a dc current is flowing. Flicker noise usually arises due to traps in the semiconductor, where carriers that would normally constitute dc current flow are held for some time period and then released. Flicker noise is also commonly referred to as $1 / \mathrm{f}$ noise since it is well modelled as having a $1 / \mathrm{f}^{\alpha}$ spectral density, where $\alpha$ is between 0.8 and 1.3. Although both bipolar and MOSFET transistors have flicker noise, it is a significant noise source in MOS transistors, whereas it can often be ignored in bipolar transistors.

### 9.3.1 Resistors

The major source of noise in resistors is thermal noise. As just discussed, it appears as white noise and can be modelled as a voltage source, $\mathrm{V}_{\mathrm{R}}(\mathrm{f})$, in series with a noiseless resistor. With such an approach, the spectral density function, $V_{R}^{2}(f)$, is found to be given by

$$
\begin{equation*}
V_{R}^{2}(f)=4 k T R \tag{9.47}
\end{equation*}
$$

where k is Boltzmann's constant $\left(1.38 \times 10^{-23} \mathrm{JK}^{-1}\right)$, T is the temperature in Kelvins, and R is the resistance value.
Alternatively, (9.47) may be rewritten noting that a $1-\mathrm{k} \Omega$ resistor exhibits a root spectral density of $4.06 \mathrm{nV} / \sqrt{\mathrm{Hz}}$ in thermal noise at room temperature $\left(300^{\circ} \mathrm{K}\right)$. Since the root spectral density is proportional to the square root of the resistance, we can also write

$$
\begin{equation*}
V_{R}(f)=\sqrt{\frac{R}{1 k}} \times 4.06 \mathrm{nV} / \sqrt{\mathrm{Hz}} \quad \text { for } 27^{\circ} \mathrm{C} \tag{9.48}
\end{equation*}
$$

Key Point: Resistors exhibit thermal noise modeled either by a voltage source in series with the resistor having a white noise spectral density 4 kTR , or a Norton equivalent current source having a white noise spectral density 4kT/R.

Note that, to reduce the thermal noise voltage due to resistors, one must either lower the temperature or use lower resistance values. The fact that lower resistance values cause less thermal noise becomes much more apparent when we look at $\mathrm{kT} / \mathrm{C}$ noise in capacitors later in this section.

An alternate model can be derived by finding the Norton equivalent circuit. Specifically, the series voltage noise source, $\mathrm{V}_{\mathrm{R}}(\mathrm{f})$, can be replaced with a parallel current noise source, $\mathrm{I}_{\mathrm{R}}(\mathrm{f})$, given by

$$
\begin{equation*}
I_{R}^{2}(f)=\frac{V_{R}^{2}(f)}{R^{2}}=\frac{4 k T}{R} \tag{9.49}
\end{equation*}
$$

Both resistor models are summarized in Fig. 9.11.

### 9.3.2 Diodes

Key Point: Diodes exhibit shot noise modeled by a current source having a white noise spectral density $2 \mathrm{ql}_{\mathrm{D}}$.

Shot noise is typically the dominant noise in diodes and can be modelled with a current source in parallel with the small-signal resistance of the diode, as Fig. 9.11 shows. The spectral density function of the current source is found to be given by

$$
\begin{equation*}
\mathrm{I}_{\mathrm{d}}^{2}(\mathrm{f})=2 \mathrm{q} \mathrm{I}_{\mathrm{D}} \tag{9.50}
\end{equation*}
$$

$$
\begin{equation*}
r_{d}=\frac{k T}{q I_{D}} \tag{9.51}
\end{equation*}
$$

The Thévenin equivalent circuit can also be used, as shown in Fig. 9.11. Note that the small-signal resistance, $r_{d}$, is used for small-signal modelling and is not a physical resistor; hence, $r_{d}$ does not contribute any thermal noise.

### 9.3.3 Bipolar Transistors

The noise in bipolar transistors is due to the shot noise of both the collector and base currents, the flicker noise of the base current, and the thermal noise of the base resistance. A common practice is to combine all these noise sources into two equivalent noise sources at the base of the transistor, as shown in Fig. 9.11. Here, the equivalent input voltage noise, $\mathrm{V}_{\mathrm{i}}(\mathrm{f})$, is given by

$$
\begin{equation*}
\mathrm{V}_{\mathrm{i}}^{2}(\mathrm{f})=4 \mathrm{kT}\left(\mathrm{r}_{\mathrm{b}}+\frac{1}{2 \mathrm{~g}_{\mathrm{m}}}\right) \tag{9.52}
\end{equation*}
$$

where the $r_{b}$ term is due to the thermal noise of the base resistance and the $g_{m}$ term is due to collector-current shot noise referred back to the input. The equivalent input current noise, $I_{i}(f)$, equals

$$
\begin{equation*}
I_{i}^{2}(f)=2 q\left(I_{B}+\frac{K I_{B}}{f}+\frac{I_{C}}{|\beta(f)|^{2}}\right) \tag{9.53}
\end{equation*}
$$

Key Point: Bipolar transistor noise is typically dominated by the thermal noise of the series base resistance, and shot noise in the basecurrent junction.
where the $2 q I_{B}$ term is a result of base-current shot noise, the $K I_{B} / f$ term models $1 / \mathrm{f}$ noise ( K is a constant dependent on device properties), and the $\mathrm{I}_{\mathrm{C}}$ term is the input-referred collector-current shot noise (often ignored).

The noise of $r_{b}$ typically dominates in $V_{i}(f)$, and the base-current shot noise often dominates in the input-current noise, $I_{i}^{2}(\mathrm{f})$. Thus, the equivalent voltage and current noise are not derived from the same noise sources. As a result, it is common practice to assume that the input voltage and current noise sources in a bipolar transistor are uncorrelated. ${ }^{5}$

### 9.3.4 MOSFETS

The dominant noise sources for active MOSFET transistors are flicker and thermal noise, as shown in Fig. 9.11. The flicker noise is modelled as a voltage source in series with the gate of value

$$
\begin{equation*}
V_{g}^{2}(f)=\frac{K}{W L C_{o x} f} \tag{9.54}
\end{equation*}
$$

Key Point: At low frequencies, l/f noise is dominant in MOSFET circuits. It is minimized by using large gate areas and p-channel transistors wherever possible.
where the constant K is dependent on device characteristics and can vary widely for different devices in the same process. The variables $W, L$, and $C_{o x}$ represent the transistor's width, length, and gate capacitance per unit area, respectively. The 1/f no ise is inversely proportional to the tran sistor area, WL, so larger devices have less $1 / \mathrm{f}$ noise. In MOSFET circuits, $1 / \mathrm{f}$ noise is extremely important because it typically dominates at low frequencies unless switching-circuit techniques are used to reduce its effect. Typically, the $1 / \mathrm{f}$ noise constant K is

[^7]smaller for p -channel transistors than their n -channel counterparts since their majority carriers (holes) are less likely to be trapped, so it is desirable to use p -channel transistors when $1 / \mathrm{f}$ noise is to be reduced.

The derivation of the thermal noise term is straightforward and is due to the resistive channel of a MOS transistor in the active region. If the transistor was in triode, the thermal noise current in the drain due to the channel resistance would simply be given by $I_{d}^{2}(f)=(4 k T) / r_{d s}$, where $r_{d s}$ is the channel resistance. However, when the transistor is in the active region, the channel cannot be considered homogeneous, and thus, the total noise is found by integrating over small portions of the channel. Such an integration results in the noise current in the drain given by

$$
\begin{equation*}
\mathrm{I}_{\mathrm{d}}^{2}(\mathrm{f})=4 \mathrm{k} T \gamma \mathrm{~g}_{\mathrm{m}} \tag{9.55}
\end{equation*}
$$

For the case $\mathrm{V}_{\mathrm{DS}}=\mathrm{V}_{\mathrm{GS}}-\mathrm{V}_{\mathrm{T}}$ and assuming a long channel device, $\gamma=2 / 3$. However, for short gate-length devices much higher values of $\gamma$ may be observed. Note that the white noise parameter $\gamma$ is different from the body-effect parameter $\gamma$.

Often, noise analyses are done just by including this noise source between the transistor drain and source. Sometimes, however, analysis may be simplified if it is replaced by an equivalent input noise source. To find the equivalent noise voltage that would cause this drain current,

Key Point: MOSFET thermal noise is simply that of a resistor with value $\mathrm{r}_{\mathrm{ds}}$ when in triode. In active mode, thermal noise is modeled by a white current noise source between drain and source with spectral density $8 \mathrm{k} \mathrm{Tg}_{\mathrm{m}} / 3$, for a long channel device, and somewhat higher for short-channel devices.
we note that the drain current is equal to the gate voltage times the transconductance of the device, or, mathematically, $\mathrm{I}_{\mathrm{d}}(\mathrm{f})=\mathrm{g}_{\mathrm{m}} \mathrm{V}_{\mathrm{i}}(\mathrm{f})$. Thus, dividing (9.55) by $\mathrm{g}_{\mathrm{m}}^{2}$ results in the simplified MOSFET model, also shown in Fig. 9.11, where there is now only one voltage noise source. However, one should be aware that this simplified model assumes the gate current is zero. Although this assumption is valid at low and moderate frequencies, an appreciable amount of current would flow through the gate-source capacitance, $\mathrm{C}_{\mathrm{gs}}$, at higher frequencies. In summary, although most noise analysis can be performed using the simplified model, if in doubt, one should use the model with the thermal noise placed as a current source in parallel with the drain-source channel.

Although gate leakage can introduce an additional source of noise, no gate leakage noise terms have been included in this noise model since the gate leakage is generally so small that its noise contribution is rarely significant.

#### EXAMPLE 9.7

A large MOS transistor consists of ten individual transistors connected in parallel. Considering 1/f noise only, what is the equivalent input voltage noise spectral density for the ten transistors compared to that of a single transistor?

#### Solution

From (9.54), the $1 / \mathrm{f}$ noise can be modelled as a current source going from the drain to the source with a noise spectral density of

$$
\begin{equation*}
I_{d}^{2}(f)=\frac{K g_{m}^{2}}{W L C_{o x} f} \tag{9.56}
\end{equation*}
$$

where $\mathrm{g}_{\mathrm{m}}$ is the transconductance of a single transistor. When ten transistors are connected in parallel, the draincurrent noise spectral density is ten times larger, so we have

$$
\begin{equation*}
\mathrm{I}_{\mathrm{d}=10}^{2}(\mathrm{f})=\frac{10 \mathrm{Kg}_{\mathrm{m}}^{2}}{\mathrm{WLC}_{\mathrm{ox}} \mathrm{f}} \tag{9.57}
\end{equation*}
$$

image_name:(a)
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: Vno^2(f), OutP: 'Vno^2(f)}
]
extrainfo:The circuit diagram (a) shows an op-amp with a noise model. The noise voltage Vn(f) is ignored, assuming Vno^2 = 0, but the actual noise voltage is Vno^2 = Vn^2. The op-amp has a negative input connected to InN and a positive input connected to GND, with the output labeled as Vno^2(f).
image_name:(b)
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Vno^2(f)}
name: R, type: Resistor, value: R, ports: {N1: Vno^2(f), N2: InN(A1)}
]
extrainfo:The circuit diagram (b) shows an op-amp with a feedback resistor R connected between the output and the inverting input. The non-inverting input is grounded. The noise voltage at the output is calculated by considering both the voltage noise Vn and the current noise In- flowing through the resistor R. The actual output noise voltage is given by Vno^2 = Vn^2 + (In- * R)^2. The diagram illustrates the importance of considering both voltage and current noise sources in op-amp circuits.
image_name:(c)
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: Vno^2(f), OutP: Vno^2(f), OutN: GND}
name: R, type: Resistor, value: R, ports: {N1: InP(A1), N2: GND}
]
extrainfo:The circuit diagram (c) is an op-amp configuration with a resistor connected to the non-inverting input. The noise voltage at the output is given by V_no^2 = V_n^2 + (I_n+R)^2, considering the noise current I_n+ flowing through the resistor.

Fig. 9.12 Opamp circuits showing the need for three noise sources in an opamp noise model. Assume the resistance, $R$, is noiseless. Also, notation is simplified from $V_{n}(f)$ to $V_{n}$, and so on.

When this noise is referred back to the input of the equivalent transistor, we have

$$
\begin{equation*}
V_{i=10}^{2}(f)=\frac{10 K_{m}^{2}}{W L C_{o x} f_{m=10}^{2}}=\frac{K}{10 W_{o x} f} \tag{9.58}
\end{equation*}
$$

since the transconductance of ten transistors in parallel, $\mathrm{g}_{\mathrm{m}=10}$, is equal to $10 \mathrm{~g}_{\mathrm{m}}$. Thus, the drain current noise spectral density of the equivalent transistor is ten times larger, but the input voltage noise spectral density is ten times smaller. This result is expected because the input voltage noise source due to $1 / \mathrm{f}$ noise is inversely proportional to the equivalent transistor area, which in this case is 10 WL .

### 9.3.5 Opamps

Noise in opamps is modelled using three uncorrelated input-referred noise sources, as shown in Fig. 9.11. With an opamp that has a MOSFET input stage, the current noises can often be ignored at low frequencies since their values are small. However, for bipolar input stages, all three noise sources are typically required, as shown in Fig. 9.12. In Fig. $9.12(a)$, if $\mathrm{V}_{\mathrm{n}}(\mathrm{f})$ is not included in the model, a unity-gain buffer with no resistors indicates that the circuit output is noiseless. In fact, the voltage noise source, $\mathrm{V}_{\mathrm{n}}(\mathrm{f})$, dominates. If $\mathrm{I}_{\mathrm{n}-}(\mathrm{f})$ is not included in an opamp model, the circuit shown in Fig. 9.12(b) indicates that the output noise voltage equals $\mathrm{V}_{\mathrm{n}}(\mathrm{f})$. Here, the current noise may dominate if the resistance, R, is large. A similar conclusion can be drawn with $I_{n+}(f)$, as shown in Fig. 9.12(c).

### 9.3.6 Capacitors and Inductors

Capacitors and inductors do not generate any noise. However, they do accumulate noise generated by other noise sources. Here, we will see that the capacitor noise mean-squared voltage equals $\mathrm{kT} / \mathrm{C}$ when it is connected to an arbitrary resistor value.

Consider a capacitance, C, in parallel with a resistor of arbitrary size, R, as shown in Fig. 9.13(a). The equivalent circuit for noise analysis is shown in Fig. 9.13(b). To determine the total noise mean-squared value across the capacitor, we note that $\mathrm{V}_{\mathrm{n} 0}(\mathrm{f})$ is simply a first-order, low-pass, filtered signal with $\mathrm{V}_{\mathrm{R}}(\mathrm{f})$ as the input. Therefore, we recognize that the noise bandwidth is given by $(\pi / 2) \mathrm{f}_{0}$ as in $(9.41)$, and since the input has a white spectral density, the total output mean-squared value is calculated as

$$
\begin{align*}
& V_{\text {no(rms) }}^{2}=V_{\mathrm{R}}^{2}(\mathrm{f})\left(\frac{\pi}{2}\right) \mathrm{f}_{0}=(4 \mathrm{kTR})\left(\frac{\pi}{2}\right)\left(\frac{1}{2 \pi \mathrm{RC}}\right)  \tag{9.59}\\
& V_{\mathrm{no}(\mathrm{~ms})}^{2}=\frac{\mathrm{kT}}{\mathrm{C}}
\end{align*}
$$

image_name:(a)
description:
[
name: R, type: Resistor, value: R, ports: {N1: rc, N2: GND}
name: C, type: Capacitor, value: C, ports: {Np: rc, Nn: GND}
]
extrainfo:The circuit consists of a resistor R and a capacitor C connected in parallel, both connected to ground.

image_name:(b)
description:
[
name: R, type: Resistor, value: R, ports: {N1: Vno(f), N2: X}
name: C, type: Capacitor, value: C, ports: {Np: Vno(f), Nn: GND}
name: V_R(f), type: VoltageSource, value: √4kTR, ports: {Np: X, Nn: GND}
]
extrainfo:The circuit consists of a resistor R and a capacitor C connected in parallel, both connected to ground. The voltage source V_R(f) represents thermal noise voltage across the resistor.

Fig. 9.13 (a) Capacitor, C, in parallel with a resistor, and (b) equivalent noise model circuit.

In other words, the rms voltage value across a capacitor is equal to $\sqrt{\mathrm{kT} / \mathrm{C}}$, whenever a simple passive resistance of any value is connected across it. Such a result is due to fact that small resistances have less noise spectral density but result in a wide bandwidth, compared to large resistances, which have reduced bandwidth but larger noise spectral density.

Finally, it should be stated that this noise property for capacitors gives a

Key Point: In a circuit comprising only capacitors and resistors (including triode MOSFETs) but no active devices, the squared rms noise on each capacitor is $\mathrm{kT} / \mathrm{C}$.
fundamental limit on the minimum noise level across a capacitor connected to passive components. ${ }^{6}$ Thus, to lower the noise level either the temperature must be lowered, or the capacitance value must be increased in which case a constant bandwidth is maintained by decreasing resistance.

#### EXAMPLE 9.8

At a room temperature of $300^{\circ} \mathrm{K}$, what capacitor size is needed to achieve a $96-\mathrm{dB}$ dynamic range in an analog circuit with maximum signal levels of 1 V rms?

#### Solution

The value of noise that can be tolerated here is 96 dB down from 1 V rms , which is

$$
\begin{equation*}
V_{n(\mathrm{rms})}=\frac{1 \mathrm{~V}}{10^{96 / 20}}=15.8 \mu \mathrm{~V} \mathrm{rms} \tag{9.60}
\end{equation*}
$$

Using (9.59), we have

$$
\begin{equation*}
\mathrm{C}=\frac{\mathrm{kT}}{\mathrm{~V}_{\mathrm{n}(\mathrm{~ms})}^{2}}=16.6 \mathrm{pF} \tag{9.61}
\end{equation*}
$$

Thus, the minimum capacitor size that can be used (without oversampling) is 16.6 pF . The use of this minimum capacitor size determines the maximum resistance size allowed to achieve a given time constant.

Finally, it should be mentioned that the equivalent noise current mean-squared value in an inductor of value L connected only to resistors is given by (see Problem 9.19)

$$
\begin{equation*}
I_{\mathrm{no}(\mathrm{~ms})}^{2}=\frac{\mathrm{kT}}{\mathrm{~L}} \tag{9.62}
\end{equation*}
$$

### 9.3.7 Sampled Signal Noise

In many cases, one should obtain a sampled value of an analog voltage. For example, switched-capacitor circuits make extensive use of sampling, and sample-and-hold circuits are commonly used in analog-to-digital and digital-to-analog conversion.

Key Point: Sampling an analog voltage on a capacitor captures both the signal component and noise with a mean-square value of $\mathrm{kT} / \mathrm{C}$, assuming a purely passive sampling network.

Consider a basic sample-and-hold circuit, as shown in Fig. 9.14. When $\phi_{\mathrm{clk}}$ drops, the transistor turns off and, in an ideal noiseless world, the input voltage signal at that instance would be held on capacitance C. However, when thermal noise is present, the resistance when the transistor is switched on causes voltage noise on the capacitor with an rms value of $\sqrt{\mathrm{kT} / C}$. Thus, when the switch is turned off, the noise as well as the desired signal is held on C. As a result, a fundamental limit occurs for sampled signals using a capaci-
tance C -an rms noise voltage of $\sqrt{\mathrm{kT} / \mathrm{C}}$. The sampled noise may be higher than this limit if the sample-andhold circuit includes active components, such as an opamp.

The sampled noise voltage does not depend on the sampling rate and is independent from sample to sample. This fact suggests a method to reduce the noise level of a signal measurement. Specifically, in the case where $\mathrm{v}_{\text {in }}$ is a dc (or low-frequency) signal, taking only one sample results in a noise voltage of $\sqrt{\mathrm{kT}} / \mathrm{C}$. However, if many samples are taken (say, 1,000 ) and all samples are averaged, the averaged value will have a reduced noise level. The reason this technique improves the measurement accuracy is that, when individual sampled values are summed together, their signal values add linearly, whereas their noise values (being uncorrelated) add as the root of the sum of squares. This technique is known as oversampling and will be discussed at length with respect to oversampling converters in Chapter 18.

### 9.3.8 Input-Referred Noise

Key Point: The input-referred noise of a circuit, if applied to the input of a noiseless copy of the circuit, results in the exact same output noise as when all of the circuit's noise sources were present. It is found by dividing the observed output noise by the gain of the circuit.

In general, the noise voltage at a particular node, or noise current in a particular branch, will be a superposition of multiple filtered uncorrelated noise sources, as illustrated in Fig. 9.7. In order to quantify the impact of all these noise sources upon SNR, it is useful to know the total input-referred noise of the circuit.

The input-referred noise of a circuit, if applied to the input of a noiseless copy of the circuit, results in the exact same output noise as when all of the circuit's noise sources were present. It is found by dividing the observed output noise by the gain of the circuit. A method to determine input referred noise by analysis or simulation is illustrated in Fig. 9.15. The output noise of the circuit $\mathrm{v}_{\text {on(rms) }}$ is first determined, then divided by the circuit's mid-band gain to arrive at a rms input-referred noise quantity. If the input source is best modeled as a voltage source, it makes sense to use an input-referred noise voltage defined in terms of the circuit's mid-band small signal voltage gain,

$$
\begin{equation*}
v_{i n(r m s)}=v_{o n(r m s)} / A \tag{9.63}
\end{equation*}
$$

Fig. 9.14 A sample-and-hold circuit.
image_name:Fig. 9.14 A sample-and-hold circuit
description:
[
name: M1, type: NMOS, ports: {S: Vin, D: Vout, G: clk}
name: C, type: Capacitor, value: C, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a sample-and-hold circuit. The NMOS transistor M1 is controlled by a clock signal 'clk'. The capacitor C is connected between the output node Vout and ground.

Voltage Amplifier
image_name:Voltage Amplifier
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: Zs, type: Resistor, value: Zs, ports: {N1: Vs, N2: In(A)}
name: A, type: OpAmp, value: A, ports: {InP: In(A) ,OutP: Out(A)}
name: RL, type: Resistor, value: RL, ports: {N1: Out(A), N2: GND}
]
extrainfo:The circuit is a voltage amplifier circuit with a noisy operational amplifier. The input voltage source Vs is connected through a resistor Zs to the input of the op-amp A. The output of the op-amp is connected to a load resistor RL.

GND
OR
image_name:Voltage Amplifier Circuit(Noiseless)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: Zs, type: Resistor, value: Zs, ports: {N1: Vs, N2: X}
name: A, type: OpAmp, value: A, ports: {InP: In(A), InN: GND, OutP: Out(A), OutN: GND}
name: ZL, type: Resistor, value: ZL, ports: {N1: Out(A), N2: GND}
]
extrainfo:The circuit is a voltage amplifier circuit with a noiseless operational amplifier. The input voltage source Vs is connected through a resistor Zs to the input of the op-amp A. The output of the op-amp is connected to a load resistor ZL.

$\mathrm{V}_{\mathrm{in}(\mathrm{ms})}=\mathrm{V}_{\mathrm{on}(\mathrm{rms})} / \mathrm{A}$
$\mathrm{SNR}=20 \log \left[\frac{\mathrm{~V}_{\mathrm{s}(\mathrm{rms})}}{\mathrm{V}_{\mathrm{in}(\mathrm{rms})}}\right]$

Transimpedance Amplifier
image_name:Transimpedance Amplifier (Noisy)
description:
[
name: Zs, type: Resistor, value: Zs, ports: {N1: In(Z), N2: GND}
name: ZL, type: Resistor, value: ZL, ports: {N1: Out(Z), N2: GND}
name: Z, type: OpAmp, value: Z, ports: {InP: In(Z), InN: GND, OutP: Out(Z)}
name: is, type: CurrentSource, value: is, ports: {Np: In(Z), Nn: GND}
]
extrainfo:The circuit is a transimpedance amplifier with a noisy operational amplifier. It converts input current to output voltage. The input current source i_s is connected through a resistor Z_s to the input of the op-amp Z. The output of the op-amp is connected to a load resistor Z_L. The SNR is calculated using the formula: SNR = 20 log [i_s(rms) / i_in(rms)]. The input-referred noise current is given by i_in(rms) = v_on(rms) / Z.
image_name:Transimpedance Amplifier (Noiseless)
description:
[
name: Zs, type: Resistor, value: Zs, ports: {N1: In(Z), N2: GND}
name: ZL, type: Resistor, value: ZL, ports: {N1: Out(Z), N2: GND}
name: Z, type: OpAmp, value: Z, ports: {InP: In(Z), InN: GND, OutP: Out(Z)}
name: is, type: CurrentSource, value: is, ports: {Np: In(Z), Nn: GND}
]
extrainfo:The circuit is a transimpedance amplifier that converts input current to output voltage. The input current source is connected through a resistor Zs to the input of the op-amp Z. The output of the op-amp is connected to a load resistor ZL. The diagram includes equations for input-referred noise and SNR.

$$
\mathrm{SNR}=20 \log \left[\frac{\mathrm{i}_{\mathrm{s}(\mathrm{rms})}}{\mathrm{i}_{\mathrm{in}(\mathrm{~ms})}}\right]
$$

Fig. 9.15 Determination of input-referred noise.
Alternatively, if the input source is best modeled as a Norton-equivalent current source, the input-referred noise current may be a more relevant quantity, obtained from the circuit's mid-band transimpedance gain,

$$
\begin{equation*}
i_{i n(\mathrm{rms})}=v_{\mathrm{on}(\mathrm{rms})} / Z \tag{9.64}
\end{equation*}
$$

In general, the output noise depends upon the source and load impedances connected to the circuit, $\mathbf{Z}_{\mathrm{s}}$ and $Z_{L}$ in Fig. 9.15, so noise analysis should always be performed with those impedances in place. However, when it is known that $Z_{s}$ is much smaller than the circuit's input impedance (i.e., a voltage input) then the noise analysis can be performed with $Z_{s}=0$ (short-circuit) with good accuracy. For example, this is typically the case for an opamp. Similarly, if $\mathbf{Z}_{\mathrm{s}}$ is much larger than the circuit input impedance (i.e., current input) then the noise analysis can be performed with an open-circuit input.

#### EXAMPLE 9.9

Two voltage amplifiers (each having very large input impedance and small output impedance) are available: one with a gain of $3 \mathrm{~V} / \mathrm{V}$ and $3 \mu \mathrm{~V}_{\mathrm{rms}}$ noise observed at the output; the other with a gain of $8 \mathrm{~V} / \mathrm{V}$ and $6 \mu \mathrm{~V}_{\mathrm{rms}}$ noise observed at its output. What is the input-referred noise of each amplifier? If the two amplifiers are to be placed in series to realize a gain of $24 \mathrm{~V} / \mathrm{V}$, in what order should they be placed in order to obtain the best noise performance? What is the resulting input-referred noise of the overall system?
image_name:(a)
description:The circuit diagram (a) shows two amplifiers in series with gains of 3 V/V and 8 V/V respectively, resulting in an overall gain of 24 V/V. The input-referred noise for the first amplifier is 1 μV_rms and for the second amplifier is 0.75 μV_rms. The total output noise is 24.7 μV_rms.
image_name:(b)
description:The circuit in diagram (b) consists of two op-amps connected in series. The first op-amp has a gain of 8 V/V with an input-referred noise of 0.75 µV_rms. The second op-amp has a gain of 3 V/V with an input-referred noise of 1 µV_rms. The overall configuration results in a total output noise of 18.2 µV_rms. The op-amp with a gain of 24 V/V is connected after this series configuration, resulting in an output noise of 0.76 µV_rms.
image_name:(b) converted
description:The circuit diagram illustrates two configurations for cascading amplifiers to achieve a total gain of 24 V/V. Configuration (a) places the amplifier with a gain of 3 V/V first, followed by the amplifier with a gain of 8 V/V, resulting in a total output noise of 24.7 µVrms. Configuration (b) reverses the order, placing the 8 V/V amplifier first, resulting in a total output noise of 18.2 µVrms. The input-referred noise for the 3 V/V amplifier is 1 µVrms, and for the 8 V/V amplifier is 0.75 µVrms. The best noise performance is achieved by placing the 8 V/V amplifier first.

Fig. 9.16 Computing the input-referred noise of Example 9.9.

#### Solution

The first amplifier has an input referred noise of $3 \mu \mathrm{~V} / 3=1 \mu \mathrm{~V}_{\mathrm{rms}}$ and the second has an input-referred noise of $6 \mu \mathrm{~V} / 8=0.75 \mu \mathrm{~V}_{\mathrm{rms}}$. First consider placing the amplifier with a gain of $3 \mathrm{~V} / \mathrm{V}$ first, as illustrated in Fig. $9.16(a)$. In this case, the total output noise is given by

$$
\begin{gathered}
\mathrm{V}_{\mathrm{on}(\mathrm{rms})}^{2}=(1 \mu \mathrm{~V})^{2}(3 \cdot 8)^{2}+(0.75 \mu \mathrm{~V})^{2} 8^{2}=0.61 \cdot 10^{-9} \mathrm{~V}^{2} \\
\mathrm{~V}_{\mathrm{on}(\mathrm{rms})}=24.7 \mu \mathrm{~V}_{\mathrm{rms}}
\end{gathered}
$$

The alternative arrangement is depicted in Fig. 9.16(b), and results in an output noise of

$$
\begin{gathered}
\mathrm{V}_{\mathrm{on}(\mathrm{rms})}^{2}=(0.75 \mu \mathrm{~V})^{2}(8 \cdot 3)^{2}+(1 \mu \mathrm{~V})^{2} 3^{2}=0.33 \cdot 10^{-9} \mathrm{~V}^{2} \\
\mathrm{~V}_{\mathrm{on}(\mathrm{~ms})}=18.2 \mu \mathrm{~V}_{\mathrm{rms}}
\end{gathered}
$$

Clearly, the second situation is preferable. The total input referred noise in this case is

$$
\mathrm{v}_{\mathrm{in}(\mathrm{rms})}=18.2 \mu \mathrm{~V}_{\mathrm{rms}} /(3 \cdot 8)=0.76 \mu \mathrm{~V}_{\mathrm{rms}}
$$

Notice that the total input referred noise is almost identical to that of the first amplifier alone. This result could also have been obtained by input-referring the noise contribution of each amplifier directly from Fig. 9.16(b).

$$
v_{\text {in(rms) }}=\sqrt{(0.75 \mu \mathrm{~V})^{2}+\frac{(1 \mu \mathrm{~V})^{2}}{8^{2}}}=0.76 \mu \mathrm{~V}_{\mathrm{rms}}
$$

The larger gain in the first stage renders the noise from the second stage negligible. This illustrates why, for example, the first stage is the dominant noise contributor in a two-stage opamp. In general, when very low-amplitude signals must be processed with high fidelity, it is desirable to use an initial low-noise and high-gain pre-amplifier. Doing so ensures the noise performance of subsequent stages is not critical.

The noise spectral density at the output of the circuit is generally the sum of noise contributed by the circuit itself, $\mathrm{v}_{\mathrm{a}}(\mathrm{f})$, as well as thermal noise from the real part of the source impedance filtered by the circuit, $4 \mathrm{kTR}_{\mathrm{s}}|\mathrm{A}(\mathrm{f})|^{2}$. These quantities may be input referred as illustrated in Fig. 9.17 for a voltage amplifier where

$$
\begin{equation*}
\mathrm{vail}_{\mathrm{a}}^{2}(\mathrm{f})=\frac{\mathrm{va}_{\mathrm{a}(\mathrm{f}}^{2}(\mathrm{f})}{|\mathrm{A}(\mathrm{f})|^{2}} \tag{9.65}
\end{equation*}
$$

image_name:Fig. 9.17
description:
[
name: Rs, type: Resistor, value: Rs, ports: {N1: In(A(f)), N2: GND}
name: A(f), type: OpAmp, value: A(f), ports: {InP: In(A(f)), OutP: Out(A(f))}
name: ZL, type: Resistor, value: ZL, ports: {N1: Out(A(f)), N2: GND}
]
extrainfo:The circuit diagram illustrates the separation of noise contributed by the source resistance and circuit noise. The input-referred noise is shown as an equivalent noiseless circuit with additional noise sources representing thermal noise and circuit noise.

Fig. 9.17 Separating noise contributed by the source resistance and circuit noise.
Note that the input-referred noise $\mathrm{v}_{\text {in(rms) }}$ in (9.63) is not obtained by integrating the input-referred noise spectrum over some bandwidth. The rms input-referred noise divides the rms output noise by the mid-band gain only so that it can be used to determine SNR assuming the input signal is confined to the circuit's mid-band region.

In radio-frequency applications, the signal input is narrowband and filters can be used to eliminate all out-of-band noise. In this case, a mea-

Key Point: The noise performance of a circuit at a particular frequency is usually reported as its input-referred noise spectrum, equal to the circuit's output noise spectrum divided by its magnitude response, or equivalently by its noise figure.
sure of noise spectral density at a particular frequency, also called the spot noise, is useful. A common noise metric in this case is the noise factor, $\mathrm{F}(\mathrm{f})$, given by the ratio of the total noise to the noise that would arise if only the source resistance were noisy, at a particular frequency.

$$
\begin{equation*}
F(f)=\frac{v_{n_{0}}^{2}(f)}{4 k R_{s}|A(f)|^{2}} \tag{9.66}
\end{equation*}
$$

This quantity may be related to the input referred noise of the amplifier alone, $\mathrm{v}_{\mathrm{ai}}^{2}(\mathrm{f})$.

$$
\begin{equation*}
F(f)=\frac{4 k T R_{s}+v_{a i}^{2}(f)}{4 k T R_{s}}=1+\frac{v_{a i}^{2}(f)}{4 k T R_{s}} \tag{9.67}
\end{equation*}
$$

Expressed in decibels, the noise factor becomes the noise figure of the circuit,

$$
\begin{equation*}
N F(f)=10 \log _{10}[F(f)] d B \tag{9.68}
\end{equation*}
$$

## 9.4 NOISE ANALYSIS EXAMPLES

In this section, a variety of circuits are analyzed from a noise perspective. Although some useful design techniques for reducing noise are presented, the main purpose of this section is to give the reader some experience in analyzing circuits from a noise perspective.

### 9.4.1 Opamp Example

Consider an inverting amplifier and its equivalent noise model, as shown in Fig. 9.18. Here, $\mathrm{V}_{\mathrm{n}}(\mathrm{f}), \mathrm{I}_{\mathrm{n}-}(\mathrm{f})$, and $\mathrm{I}_{\mathrm{n+}}(\mathrm{f})$ represent the opamp's equivalent input noise, and the remaining noise sources are resistor thermal noise sources. Note that current noise sources are used in the models for $R_{1}$ and $R_{f}$, whereas a voltage noise source is used for $\mathrm{R}_{2}$. As we will see, these choices of noise sources simplify the circuit analysis.

First, using superposition and assuming all noise sources are uncorrelated, consider the output noise voltage, $V_{n o 1}^{2}(f)$, due only to $I_{n 1}, I_{n f}$, and $I_{n-}$. These three noise currents add together, and their total current sum is fed into the parallel combination of $C_{f}$ and $R_{f}$. Note that no current passes through $R_{1}$ since the voltage across it is zero due to the virtual ground at the negative opamp terminal (assuming a high-gain opamp). Thus, the output noise mean-squared value due to these three noise currents is given by

$$
\begin{equation*}
V_{n 01}^{2}(f)=\left[I_{n 1}^{2}(f)+I_{n f}^{2}(f)+I_{n-}^{2}(f)\right]\left|\frac{R_{f}}{1+j 2 \pi f R_{f} C_{f}}\right|^{2} \tag{9.69}
\end{equation*}
$$

image_name:(a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vi, N2: InN(A1)}
name: R2, type: Resistor, value: R2, ports: {N1: InP(A1), N2: GND}
name: Rf, type: Resistor, value: Rf, ports: {N1: InN(A1), N2: Vo}
name: Cf, type: Capacitor, value: Cf, ports: {N1: InN(A1), N2: Vo}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Vo}
]
extrainfo:The circuit diagram (a) represents a low-pass filter with an operational amplifier (A1) in an inverting configuration. The resistors R1 and R2 are connected to the input and ground, respectively, while Rf and Cf form a parallel feedback network connected to the output Vo. The input voltage Vi is applied to R1. The op-amp's negative terminal is virtually grounded. The circuit is designed to filter out high-frequency noise, with a 3-dB cutoff frequency determined by Rf and Cf. The equivalent noise model in diagram (b) includes noise current sources (In1, In-, Inf) and voltage sources (Vn2, Vn) to represent the noise contributions in the circuit.
image_name:(b)
description:The circuit diagram (b) represents an equivalent noise model for a low-pass filter with an op-amp. It includes noise current sources (In1, In-, In+, Inf) and voltage noise sources (Vn2, Vn) affecting the output voltage Vno(f). The noise is shaped by the feedback network consisting of Rf and Cf, forming a low-pass filter.

Fig. 9.18 (a) Low-pass filter, and (b) equivalent noise model.

This equation indicates that this part of the output noise value equals the sum of the noise currents multiplied by $R_{f}^{2}$. This noise portion is then shaped by a low-pass filter with a 3-dB frequency equal to $f_{0}=1 /\left(2 \pi R_{f} C_{f}\right)$ Following an analysis similar to that in Section 9.3.6, the total integrated mean squared output noise voltage due to Rf alone may be shown to be simply $k T / C_{f}$. Including the noise of $R_{1}$ increases the result to $\left(1+R_{f} / R_{1}\right) k T / C_{f}$ and including opamp noise increases it further. Hence, $\mathrm{kT} / \mathrm{C}_{\mathrm{f}}$ is a lower limit on the noise of opamps with capacitive feedback.

Using superposition further, the output mean-squared value, $\mathrm{V}_{\mathrm{n} 02}^{2}(\mathrm{f})$, due to the three noise sources at the positive opamp terminal can be found as follows: By converting $I_{n+}$ to a voltage source (by multiplying it by $R_{2}$ ), we see that the three noise voltages are summed and are applied to the positive opamp terminal. Since the gain from the positive opamp terminal to the output signal is easily found, the output noise mean-squared value due to these three noise sources is given by

$$
\begin{equation*}
V_{n o 2}^{2}(f)=\left[I_{n+1}^{2}(f) R_{2}^{2}+V_{n 2}^{2}(f)+V_{n}^{2}(f)\right]\left|1+\frac{R_{f} / R_{1}}{1+j 2 \pi f C_{f} R_{f}}\right|^{2} \tag{9.70}
\end{equation*}
$$

This equation indicates that this part of the output noise mean-squared value equals the sum of the noise voltages, and this noise portion is then shaped by the shown transfer function. For this transfer function, if $R_{f} \ll R_{1}$, then its gain approximately equals unity for all frequencies. Thus, for an ideal opamp, the noise would exist up to infinite frequency, resulting in an infinite amount of mean-squared volts. However, for practical circuits, the gain drops off above the unity-gain frequency of the opamp, and thus the noise is effectively low-pass filtered. In the case where $R_{f} \gg>R_{1}$, the low-frequency gain is roughly $R_{f} / R_{l}$, and its 3-dB frequency is the same as in the case of the noise sources at the negative opamp terminal (i.e., $f_{0}=1 /\left(2 \pi R_{f} C_{f}\right)$ ). However, in this case, the gain only decreases to unity and then remains at that level. Treating the Bode plot as exact and noting that, above $f_{0}$, the gain drops off at $-20 d B /$ decade, this transfer function reaches unity around $f_{1}=\left(R_{f} / R_{1}\right) f_{0}$. Thus, one should also include the opamp's positive input noise (with a gain of one) integrated over the region between $f_{1}$ and the unitygain frequency of the opamp.

Finally, the total output noise mean-squared value is simply the sum

$$
\begin{equation*}
V_{n o}^{2}(f)=V_{n o 1}^{2}(f)+V_{\mathrm{nO2}}^{2}(f) \tag{9.71}
\end{equation*}
$$

or, if rms values are found,

$$
\begin{equation*}
V_{\mathrm{no}(\mathrm{rms})}^{2}=V_{\mathrm{nol}(\mathrm{rms})}^{2}+V_{\mathrm{nO2}(\mathrm{rms})}^{2} \tag{9.72}
\end{equation*}
$$

#### EXAMPLE 9.10

Estimate the total output noise rms value for a $10-\mathrm{kHz}$ low-pass filter, as shown in Fig. 9.18, when $\mathrm{C}_{\mathrm{f}}=160 \mathrm{pF}$, $R_{f}=100 \mathrm{k}, R_{1}=10 \mathrm{k}$, and $\mathrm{R}_{2}=9.1 \mathrm{k}$. Also, find the SNR for an input signal equal to 100 mV rms . Assume that the noise voltage of the opamp is given by $\mathrm{V}_{\mathrm{n}}(\mathrm{f})=20 \mathrm{nV} / \sqrt{\mathrm{Hz}}$, both its noise currents are $\mathrm{I}_{\mathrm{n}}(\mathrm{f})=0.6 \mathrm{pA} / \sqrt{\mathrm{Hz}}$, and that its unity-gain frequency equals 5 MHz .

#### Solution

Assuming the device is at room temperature, the resistor noise sources are equal to

$$
\begin{align*}
\mathrm{I}_{\mathrm{nf}} & =0.406 \mathrm{pA} / \sqrt{\mathrm{Hz}}  \tag{9.73}\\
\mathrm{I}_{\mathrm{n} 1} & =1.28 \mathrm{pA} / \sqrt{\mathrm{Hz}}  \tag{9.74}\\
\mathrm{~V}_{\mathrm{n} 2} & =12.2 \mathrm{nV} / \sqrt{\mathrm{Hz}} \tag{9.75}
\end{align*}
$$

The low-frequency value of $V_{\text {no1 }}^{2}(f)$ is found by letting $f=0$ in (9.69).

$$
\begin{align*}
\mathrm{V}_{\mathrm{n} 01}^{2}(0) & =\left[\mathrm{I}_{\mathrm{n} 1}^{2}(0)+\mathrm{I}_{\mathrm{n} \mathrm{n}}^{2}(0)+\mathrm{I}_{\mathrm{n}-}^{2}(0)\right] \mathrm{R}_{\mathrm{f}}^{2} \\
& =\left(0.406^{2}+1.28^{2}+0.6^{2}\right)\left(1 \times 10^{-12}\right)^{2}(100 \mathrm{k})^{2}  \tag{9.76}\\
& =(147 \mathrm{nV} / \sqrt{\mathrm{Hz}})^{2}
\end{align*}
$$

Since (9.69) also indicates that this noise is low-pass filtered, the rms output noise value due to these three sources can be found using the concept of a noise equivalent bandwidth. Specifically, we multiply the spectral density by $\left(\pi f_{0}\right) / 2$, where $f_{0}=1 /\left(2 \pi R_{f} C_{f}\right)$. Thus,

$$
\begin{align*}
\mathrm{V}_{\mathrm{no1}(\mathrm{rms})}^{2} & =(147 \mathrm{nV} / \sqrt{\mathrm{Hz}})^{2} \times \frac{1}{4(100 \mathrm{k} \Omega)(160 \mathrm{pF})}  \tag{9.77}\\
& =(18.4 \mu \mathrm{~V})^{2}
\end{align*}
$$

To estimate the output noise due to the sources at the positive opamp terminal, we find $\mathrm{V}_{\text {no2 }}^{2}(0)$ to be given by

$$
\begin{align*}
V_{n o 2}^{2}(0) & =\left[I_{n+}^{2}(f) R_{2}^{2}+V_{n 2}^{2}(f)+V_{n}^{2}(f)\right]\left(1+R_{f} / R_{1}\right)^{2} \\
& =(24.1 \mathrm{nV} / \sqrt{\mathrm{Hz}})^{2} \times 11^{2}  \tag{9.78}\\
& =(265 \mathrm{nV} / \sqrt{\mathrm{Hz}})^{2}
\end{align*}
$$

This noise is also low-pass filtered at $f_{0}$ until $f_{1}=\left(R_{t} / R_{1}\right) f_{0}$, where the noise gain reaches unity and it remains until $f_{t}=5 \mathrm{MHz}$ (i.e, the unity-gain frequency of the opamp). Thus, breaking this noise into two portions, and using (9.40) to calculate the first portion, we have

$$
\begin{align*}
V_{\text {no2(rms) }}^{2} & =\left(265 \times 10^{-9}\right)^{2}\left(\frac{1}{4 R_{f} C_{f}}\right)+\left(24.1 \times 10^{-9}\right)^{2}\left(\frac{\pi}{2}\right)\left(f_{t}-f_{1}\right)  \tag{9.79}\\
& =(74.6 \mu \mathrm{~V})^{2}
\end{align*}
$$

Thus, the total output noise is estimated to be

$$
\begin{equation*}
V_{\mathrm{no}(\mathrm{rms})}=\sqrt{V_{\mathrm{nO} 1(\mathrm{rms})}^{2}+\mathrm{V}_{\mathrm{nO}(\mathrm{rms})}^{2}}=77 \mu \mathrm{Vms} \tag{9.80}
\end{equation*}
$$

It should be noted here that the major source of noise at low frequencies is due to the opamp's voltage noise, $\mathrm{V}_{\mathrm{n}}(\mathrm{f})$.
To obtain the SNR for this circuit with a $100-\mathrm{mV}$ rms input level, one can find the output signal meansquared value and relate that to the output noise value. Alternatively, one can find the equivalent input noise value
image_name:Fig. 9.19 A bipolar common-emitter amplifier
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: X3}
name: R_C, type: Resistor, value: R_C, ports: {N1: VCC, N2: Vout}
name: C_C, type: Capacitor, value: C_C, ports: {Np: Vout, Nn: GND}
name: Vi^2, type: VoltageSource, value: Vi^2, ports: {Np: X3, Nn: X2}
name: Ii^2, type: CurrentSource, value: Ii^2, ports: {Np: X2, Nn: GND}
name: IB, type: CurrentSource, value: IB, ports: {Np: X1, Nn: GND}
name: Q1, type: NPN, ports: {C: Vout, B: X2, E: X1}
]
extrainfo:This circuit is a bipolar common-emitter amplifier. The input voltage source Vi is connected through a resistor RS to the base of the NPN transistor Q1. The collector of Q1 is connected to VCC through the resistor RC, and the emitter is connected to ground through a current source IB. The output is taken from the collector of Q1. The capacitor CC is used for AC coupling at the output.

Fig. 9.19 A bipolar common-emitter amplifier.
by dividing the output noise value by the circuit's gain and then relate the input signal and noise mean-squared values. Taking the first approach results in an output signal level of 1 V rms, which gives an SNR of

$$
\begin{equation*}
\mathrm{SNR}=20 \log \left(\frac{1 \mathrm{~V}}{77 \mu \mathrm{~V}}\right)=82 \mathrm{~dB} \tag{9.81}
\end{equation*}
$$

Note here that using a lower-speed opamp would have reduced the total output noise, as would choosing an opamp with a lower noise voltage. Also note that $R_{2}$ contributes to the output noise through both its thermal noise and the noise current of the opamp's positive input. Since its only purpose is to improve the dc offset performance, $R_{2}$ should be eliminated in a low-noise circuit (assuming dc offset can be tolerated).

### 9.4.2 Bipolar Common-Emitter Example

In this example, we consider a bipolar common-emitter amplifier, as shown in Fig. 9.19. Here, we wish to find the optimum bias current to minimize the equivalent input noise of this amplifier (i.e., maximize the signal-to-noise ratio of the amplifier).

We should state that it is assumed here that the collector-current shot noise dominates in the input voltage noise source and the base-current shot noise dominates in the input current noise source. Therefore, the input voltage noise due to the transistor alone is given by

$$
\begin{equation*}
V_{i}^{2}(f)=2 \mathrm{kT} / \mathrm{g}_{\mathrm{m}} \tag{9.82}
\end{equation*}
$$

and the input current noise due to the transistor alone is given by

$$
\begin{equation*}
\mathrm{I}_{\mathrm{i}}^{2}(\mathrm{f})=2 \mathrm{q} \mathrm{I}_{\mathrm{B}} \tag{9.83}
\end{equation*}
$$

These assumptions are reasonable since usually $1 / \mathrm{f}$ noise is not important for bipolar transistors, and the collector shot noise is usually not a major component of the input current noise source for wideband examples. Also, although the base resistance has temporarily been ignored, it will be taken into account shortly by simply modifying the size of the source resistance.

The first step is to replace the input current noise source by an input voltage noise source. First, note that the gain from the base to the collector (ignoring the transistor output impedance, $r_{o}$ ) is equal to $g_{m} R_{C}$, and the impedance looking into the base is $r_{\pi}$. Therefore, the output noise due to $I_{i}^{2}(f)$ is given by

$$
\begin{equation*}
V_{\mathrm{oi}}^{2}(\mathrm{f})=\mathrm{I}_{\mathrm{i}}^{2}(\mathrm{f})\left[\left(\mathrm{R}_{\mathrm{S}} \| \mathrm{r}_{\pi}\right) \mathrm{g}_{\mathrm{m}} \mathrm{R}_{\mathrm{C}}\right]^{2} \tag{9.84}
\end{equation*}
$$

Now the gain from the input voltage noise source to the output is given by

$$
\begin{equation*}
A_{V}=\frac{V_{o}}{V_{i}}=\frac{r_{\pi}}{r_{\pi}+R_{S}} g_{m} R_{C} \tag{9.85}
\end{equation*}
$$

To represent the output noise due to the input current source by an equivalent input voltage source, we have

$$
\begin{equation*}
V_{\text {ieq }}^{2}(f)=\frac{V_{o i}^{2}(f)}{A_{V}^{2}}=\left(\frac{\frac{r_{\pi} R_{S}}{\left(r_{\pi}+R_{S}\right)} g_{m} R_{C}}{\frac{r_{\pi}}{\left(r_{\pi}+R_{S}\right)} g_{m} R_{C}}\right)^{2} I_{i}^{2}(f)=I_{i}^{2}(f) R_{S}^{2} \tag{9.86}
\end{equation*}
$$

We can now replace all noise sources by a single voltage noise source, which includes the noise due to the input voltage noise source and the input current noise source of the transistor, as well as the noise of the source resistor. We have

$$
\begin{equation*}
V_{i=\text { total }}^{2}(f)=V_{i}^{2}(f)+V_{\text {ieq }}^{2}(f)+4 k T R_{S} \tag{9.87}
\end{equation*}
$$

The first two terms represent the noise of the transistor and the third term represents the noise of the source resistance. Using (9.82), (9.83), and (9.86), we have

$$
\begin{equation*}
\mathrm{V}_{\mathrm{i}=\text { total }}^{2}(\mathrm{f})=\frac{2 \mathrm{kT}}{\mathrm{~g}_{\mathrm{m}}}+2 \mathrm{q} \mathrm{I}_{\mathrm{B}} \mathrm{R}_{\mathrm{S}}^{2}+4 \mathrm{kTR} \mathrm{R}_{\mathrm{S}} \tag{9.88}
\end{equation*}
$$

Substituting $g_{m}=q I_{C} /(k T)$ and $I_{B}=I_{C} / \beta$, we find

$$
\begin{equation*}
\mathrm{V}_{\mathrm{i}=\text { total }}^{2}(\mathrm{f})=\frac{2(\mathrm{kT})^{2}}{q \mathrm{I}_{\mathrm{C}}}+\frac{2 \mathrm{qI}_{\mathrm{C}} \mathrm{R}_{\mathrm{S}}^{2}}{\beta}+4 \mathrm{kTR} \mathrm{R}_{\mathrm{S}} \tag{9.89}
\end{equation*}
$$

The noise of the transistor base resistor can now be included by replacing $R_{S}$ with $R_{S}+r_{b}$ to obtain

$$
\begin{equation*}
\mathrm{V}_{\mathrm{i}=\text { total }}^{2}(\mathrm{f})=\frac{2(\mathrm{kT})^{2}}{q \mathrm{I}_{\mathrm{c}}}+\frac{2 \mathrm{qI}_{\mathrm{C}}\left(\mathrm{R}_{\mathrm{S}}+\mathrm{r}_{\mathrm{b}}\right)^{2}}{\beta}+4 \mathrm{kT}\left(\mathrm{R}_{\mathrm{S}}+\mathrm{r}_{\mathrm{b}}\right) \tag{9.90}
\end{equation*}
$$

Alternatively, (9.90) can be expressed in terms of $\mathrm{g}_{\mathrm{m}}=\mathrm{qI}_{\mathrm{c}} /(\mathrm{kT})$ as in [Buchwald, 1995]

$$
\begin{equation*}
V_{i=1 \text { total }}^{2}(f)=4 k T\left[R_{s}+r_{b}+\frac{1}{2 g_{m}}+\frac{g_{m}\left(R_{s}+r_{b}\right)^{2}}{2 \beta}\right] \tag{9.91}
\end{equation*}
$$

These two equations are good approximations for most applications of bipolar common-emitter amplifiers. Notice in (9.90), the first term models the transistor base-current shot noise and decreases with increased bias current. However, the second term (which models the transistor collector shot noise) increases with increasing collector bias current. Finally, the terms modelling the noise of the source resistor and the transistor base resistor are independent of the transistor bias current. To find the optimum bias current, we differentiate (9.90) with respect to $\mathrm{I}_{C}$ and set the result to zero. This yields the rather simple result of

$$
\begin{equation*}
I_{c, \text { opt }}=\frac{k T}{q} \frac{\sqrt{\beta}}{R_{S}+r_{b}} \tag{9.92}
\end{equation*}
$$

or, equivalently,

$$
\begin{equation*}
g_{m, \text { opt }}=\frac{\sqrt{\beta}}{R_{S}+r_{b}} \tag{9.93}
\end{equation*}
$$

#### EXAMPLE 9.11

Consider the common-emitter amplifier shown in Fig. 9.19, where $\mathrm{R}_{\mathrm{C}}=10 \mathrm{k} \Omega, \mathrm{C}_{\mathrm{C}}=1 \mathrm{pF}, \mathrm{R}_{\mathrm{s}}=500 \Omega$, $\beta=100$, and the base resistance is given by $r_{b}=300 \Omega$. At room temperature, (i.e., $300{ }^{\circ} \mathrm{K}$ ), find the optimum bias current and the total equivalent input noise.

#### Solution

Using (9.92), we find

$$
\begin{equation*}
\mathrm{I}_{\mathrm{C}=\mathrm{opt}}=0.026 \times \frac{\sqrt{100}}{500+300}=0.325 \mathrm{~mA} \tag{9.94}
\end{equation*}
$$

implying that

$$
\begin{equation*}
\mathrm{g}_{\mathrm{m}}=\frac{\mathrm{I}_{\mathrm{C}}}{\mathrm{~V}_{\mathrm{T}}}=12.5 \mathrm{~mA} / \mathrm{V} \tag{9.95}
\end{equation*}
$$

To find the output noise spectral density, we now use (9.91) to find

$$
\begin{equation*}
\mathrm{V}_{\mathrm{i}=\text { total }}^{2}(\mathrm{f})=4 \mathrm{kT}(500+300+40+40)=1.46 \times 10^{-17} \mathrm{~V}^{2} / \mathrm{Hz} \tag{9.96}
\end{equation*}
$$

Notice that the noise due to the source resistance dominates, even though the source resistance is moderately small. Even for no source resistance, the thermal noise due to the base resistance would still dominate. Thus, for a very low source resistance, the major way to improve the noise is to minimize the base resistance by using larger transistors (or to combine a number of parallel transistors).

Assuming the RC time constant at the collector dominates the frequency response, the noise bandwidth of the amplifier is given by

$$
\begin{equation*}
f_{x}=\frac{1}{4 R_{c} C_{c}}=25 \mathrm{MHz} \tag{9.97}
\end{equation*}
$$

resulting in the total input-referred voltage noise given by

$$
\begin{equation*}
V_{\text {ni(rms) }}=\left[f_{x} \mathrm{~V}_{i=\text { total }}^{2}(f)\right]^{1 / 2}=19.1 \mu \mathrm{~V} \tag{9.98}
\end{equation*}
$$

### 9.4.3 CMOS Differential Pair Example

In this example, we look at the input circuitry of a traditional two-stage CMOS opamp, as shown in Fig. 9.20. As illustrated in Example 9.9, as long as the input stage of a two-stage opamp has some significant gain, it will dominate the overall noise performance of the opamp. Note that each of the transistors have been modelled using an equivalent voltage noise source, as presented in Fig. 9.11. Voltage noise sources are used here since we will be addressing the low-frequency noise performance of this stage. It should be mentioned here that in the following derivations, we have assumed matching between transistor pair $Q_{1}$ and $Q_{2}$ as well as in pair $Q_{3}$ and $Q_{4}$.

We start by finding the gains from each noise source to the output node, $V_{n 0}$. The gains from $V_{n 1}$ and $V_{n 2}$ are the same as the gains from the input signals, resulting in

$$
\begin{equation*}
\left|\frac{V_{\mathrm{no}}}{V_{n 1}}\right|=\left|\frac{V_{n 0}}{V_{n 2}}\right|=g_{m 1} R_{\circ} \tag{9.99}
\end{equation*}
$$

where $R_{0}$ is the output impedance seen at $V_{n}$.
image_name:Fig. 9.20 A CMOS input stage for a traditional opamp with MOSFET noise sources shown.
description:The circuit is a CMOS input stage for a traditional opamp with MOSFET noise sources. It includes matched transistor pairs Q1/Q2 and Q3/Q4. Q5 serves as a current source connected to VDD. The output node is Vno.

Fig. 9.20 A CMOS input stage for a traditional opamp with MOSFET noise sources shown.

Next, for $\mathrm{V}_{\mathrm{n} 3}$, notice that the current through this voltage source must be zero because one side is connected to the gate of $Q_{3}$ only. Therefore, assuming all other sources are zero, the drain current is unaffected by $\mathrm{V}_{\mathrm{n} 3}$. This implies that the gate voltage of $\mathrm{Q}_{3}$ is also unaffected by $\mathrm{V}_{\mathrm{n} 3}$. Therefore, in the small-signal model, $\mathrm{V}_{\mathrm{n} 3}$ is equal to $\mathrm{V}_{\mathrm{gs} 4}$, and the gain from $\mathrm{V}_{\mathrm{n} 3}$ to the output is the same as the gain from $\mathrm{V}_{\mathrm{n} 4}$ to the output. Thus, we have

$$
\begin{equation*}
\left|\frac{V_{\mathrm{no}}}{V_{n 3}}\right|=\left|\frac{V_{n 0}}{V_{n 4}}\right|=g_{m 3} R_{0} \tag{9.100}
\end{equation*}
$$

Finally, the noise gain from $\mathrm{V}_{\mathrm{n} 5}$ to the output can be found by noting that it modulates the bias current and the fact that, due to the symmetry in the circuit, the drain of $Q_{2}$ will track that of $Q_{1}$. As a result, the last gain factor is given by

$$
\begin{equation*}
\left|\frac{V_{\mathrm{no}}}{V_{\mathrm{n} 5}}\right|=\frac{g_{\mathrm{m} 5}}{2 \mathrm{~g}_{\mathrm{m} 3}} \tag{9.101}
\end{equation*}
$$

Since this last gain factor is relatively small compared to the others, it will be ignored from here on.
Using the gain factors just shown, the output noise value is seen to be given by

$$
\begin{equation*}
V_{n o}^{2}(f)=2\left(g_{m 1} R_{o}\right)^{2} V_{n 1}^{2}(f)+2\left(g_{m 3} R_{o}\right)^{2} V_{n 3}^{2}(f) \tag{9.102}
\end{equation*}
$$

This output noise value can be related back to an equivalent input noise value, $\mathrm{V}_{\text {neq }}(\mathrm{f})$, by dividing it by the gain, $g_{m 1} R_{0}$, which results in

$$
\begin{equation*}
V_{\text {neq }}^{2}(f)=2 V_{n 1}^{2}(f)+2 V_{n 3}^{2}(f)\left(\frac{g_{m 3}}{g_{m 1}}\right)^{2} \tag{9.103}
\end{equation*}
$$

Thus, for the white noise portion of $\mathrm{V}_{n 1}(\mathrm{f})$ and $\mathrm{V}_{n 3}(\mathrm{f})$, we make the substitution

$$
\begin{equation*}
\mathrm{V}_{\mathrm{ni}}^{2}(\mathrm{f})=4 \mathrm{kT} \gamma\left(\frac{1}{\mathrm{~g}_{\mathrm{m}}}\right) \tag{9.104}
\end{equation*}
$$

resulting in

$$
\begin{equation*}
\mathrm{V}_{\mathrm{neq}}^{2}(\mathrm{f})=2 \cdot 4 \mathrm{kT} \gamma\left(\frac{1}{\mathrm{~g}_{\mathrm{m} 1}}\right)+2 \cdot 4 \mathrm{kT} \gamma\left(\frac{\mathrm{~g}_{\mathrm{m} 3}}{\mathrm{~g}_{\mathrm{m} 1}}\right)^{2}\left(\frac{1}{\mathrm{~g}_{\mathrm{m} 3}}\right) \tag{9.105}
\end{equation*}
$$

Key Point: To minimize thermal noise in a CMOS differential amplifier, the input pair transconductance should be maximized. For a fixed drain current, that implies operation in weak inversion or even subthreshold.

We see here that the noise contribution of both pairs of transistors is inversely proportional to the transconductance of $\mathrm{g}_{\mathrm{m} 1}$. In other wor ds , $\mathrm{g}_{\mathrm{m} 1}$ should be made as large as possible to minimize thermal noise . Also, $g_{m 3}$ should be made small to reduce its thermal noise contribution. For a fixed bias current, $\mathrm{I}_{\mathrm{D} 5}$, this suggests making $\mathrm{V}_{\mathrm{eff,1}}$ small and $\mathrm{V}_{\text {eff,3 }}$ large. Increasing $\mathrm{V}_{\text {eff, } 3}$ also reduces the output signal swing available, which may adversely effect the maximum SNR achievable in this circuit. However, the signal swing at the output of the first stage in a two-stage opamp is usually relatively small anyway.
Next, we consider the effects of $1 / \mathrm{f}$, or flicker, noise, which normally greatly dominates at low frequencies. First, make the following substitution into (9.103),

$$
\begin{equation*}
g_{m i}=\sqrt{2 \mu_{i} C_{o x}\left(\frac{W}{L}\right)_{i} I_{D i}} \tag{9.106}
\end{equation*}
$$

resulting in

$$
\begin{equation*}
V_{n i}^{2}(f)=2 V_{n 1}^{2}(f)+2 V_{n 3}^{2}(f)\left[\frac{(W / L)_{3} \mu_{n}}{(W / L)_{1} \mu_{p}}\right] \tag{9.107}
\end{equation*}
$$

Now, letting each of the noise sources have a spectral density given by

$$
\begin{equation*}
V_{n i}^{2}(f)=\frac{K_{i}}{W_{i} L_{i} C_{o x} f} \tag{9.108}
\end{equation*}
$$

we have [Bertails, 1979]

$$
\begin{equation*}
V_{n i}^{2}(f)=\frac{2}{C_{o x} f}\left[\frac{K_{1}}{W_{1} L_{1}}+\left(\frac{\mu_{n}}{\mu_{p}}\right)\left(\frac{K_{3} L_{1}}{W_{1} L_{3}^{2}}\right)\right] \tag{9.109}
\end{equation*}
$$

Recall that the first term in (9.109) is due to the p -channel input transistors, $\mathrm{Q}_{1}$ and $\mathrm{Q}_{2}$, and the second term is due to the n -channel loads, $\mathrm{Q}_{3}$ and $\mathrm{Q}_{4}$. We note some points for $1 / \mathrm{f}$ noise here:

1. For $L_{1}=L_{3}$, the noise of the n -channel loads dominate since $\mu_{n}>\mu_{p}$ and typically n -channel transistors have larger 1/f noise than p-channel transistors (i.e., $\mathrm{K}_{3}>\mathrm{K}_{1}$ ).
2. Taking $L_{3}$ longer greatly helps due to the inverse squared relationship in the second term of (9.109). This limits the signal swings somewhat, but it may be a reasonable trade-off where low noise is important.
3. The input noise is independent of $\mathrm{W}_{3}$, and therefore we can make it large if large signal swing is desired at the output (although this will increase the thermal noise of $Q_{3}$ and $Q_{4}$ ).
4. Taking $\mathrm{W}_{1}$ wider also helps to minimize $1 / \mathrm{f}$ noise. (Doing so reduces thermal noise, as well.)
5. Taking $L_{1}$ longer increases the noise because the second term in (9.109) is dominant. Specifically, this decreases the input-referred noise of the p-channel input transistors, which are not the dominant noise sources, while increasing the input-referred noise of the n -channel load transistors, which are the dominant noise sources.

Finally, we can integrate (9.109) from $f_{1}$ to $f_{2}$ to find the equivalent input noise value given by

$$
\begin{equation*}
\mathrm{V}_{\mathrm{ni}(\mathrm{rms})}^{2}=\frac{2}{\mathrm{C}_{\mathrm{ox}}}\left[\frac{\mathrm{~K}_{1}}{\mathrm{~W}_{1} \mathrm{~L}_{1}}+\left(\frac{\mu_{\mathrm{n}}}{\mu_{\mathrm{p}}}\right)\left(\frac{\mathrm{K}_{3} \mathrm{~L}_{1}}{\mathrm{~W}_{1} \mathrm{~L}_{3}^{2}}\right)\right] \ln \left(\frac{\mathrm{f}_{2}}{\mathrm{f}_{1}}\right) \tag{9.110}
\end{equation*}
$$

### 9.4.4 Fiber-Optic Transimpedance Amplifier Example

The most popular means of detecting light from a fiber-optic cable is to use a transimpedance amplifier, as shown in Fig. 9.21. The light from the fiber cable hits a photodetector, such as a reverse-biased diode. The light produces electron hole carriers in the depletion region of the reverse-biased diode, causing current to flow through the resistor, and therefore the output of the amplifier becomes positive. A popular choice for the first stage of the amplifier is to use a common-source amplifier with a resistor load. In low-noise applications, an active load would be too noisy. Assuming a CMOS transistor is used, ${ }^{7}$ the preamp can be modelled as shown in Fig. 9.22. The photodetector is modelled as an input current source along with a parasitic capacitance, $\mathrm{C}_{\text {in }}$. Also shown in Fig. 9.22 are the two major noise sources, namely the thermal current noise at the drain of $Q_{1}$ and the thermal noise from the feedback resistor, $R_{F}$. The $1 / f$ noise of the transistor is ignored because it is assumed that the circuit is high speed, such that thermal noise dominates. The second (and perhaps subsequent) stage is modelled by an amplifier that has a gain of $\mathrm{A}_{2}$. The noise due to this second stage is also ignored since the noise sources in the second stage are not amplified by the gain of the first stage.

A simplified small-signal model of this preamplifier, used for noise analysis, is shown in Fig. 9.23. The only parasitic capacitance considered in the transistor model is $\mathrm{C}_{\mathrm{gs}}$, since the gain of the first stage is only moderate,
image_name:Fig. 9.21 A fiber-optic transresistance preamp.
description:The circuit is a fiber-optic transresistance preamplifier. It consists of a photodiode converting optical signals to electrical, connected to an operational amplifier in a feedback configuration with a feedback resistor RF.

Fig. 9.21 A fiber-optic transresistance preamp.
image_name:Fig. 9.22 A fiber-optic transresistance preamp.
description:
[
name: Iin, type: CurrentSource, value: Iin, ports: {Np: P, Nn: GND}
name: Cin, type: Capacitor, value: Cin, ports: {Np: P, Nn: GND}
name: Q1, type: NMOS, ports: {S: GND, D: In(A2), G: P}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: In(A2)}
name: I_R^2, type: CurrentSource, value: 4KT/R, ports: {Np: P, Nn: Vout}
name: RF, type: Resistor, value: RF, ports: {N1: Vout, N2: P}
name: A2, type: OpAmp, value: A2, ports: {InP: In(A2), Out: Vout}
name: I_D^2, type: CurrentSource, value: 4KT(2/3)gm, ports: {Np: In(A2), Nn: GND}
]
extrainfo:The circuit is a fiber-optic transresistance preamplifier that converts optical signals to electrical signals using a photodiode and an operational amplifier in a feedback configuration. It includes a feedback resistor RF and is used for noise analysis in fiber-optic applications.

Fig. 9.22 A simplified model for a CMOS fiber-optic preamp.
7. Fiber-optic preamps have also been realized using JFET transistors as well, but since their thermal noise model is identical to the noise model of the CMOS transistor, the analysis would be almost unchanged.
image_name:Fig. 9.23 A simplified small-signal model used for noise analysis
description:
[
name: i_in, type: CurrentSource, value: i_in, ports: {Np: Vg, Nn: GND}
name: C_in, type: Capacitor, value: C_in, ports: {Np: Vg, Nn: GND}
name: C_gs, type: Capacitor, value: C_gs, ports: {Np: Vg, Nn: GND}
name: R_D, type: Resistor, value: R_D, ports: {N1: VDD, N2: Vd}
name: R_F, type: Resistor, value: R_F, ports: {N1: Vg, N2: Vout}
name: A2, type: OpAmp, value: A2, ports: {InP: Vd, Out: Vout}
name: I_D^2, type: CurrentSource, value: 4KT(2/3)gm, ports: {Np: Vd, Nn: GND}
name: I_R^2, type: CurrentSource, value: 4KT/R, ports: {Np: Vg, Nn: Vout}
name: gmvg, type: VoltageControlledCurrentSource, ports: {N1: Vd, N2: GND}
]
extrainfo:The circuit is a simplified small-signal model used for noise analysis in a CMOS fiber-optic preamp. It includes a feedback configuration with a photodiode and an operational amplifier, focusing on analyzing noise contributions from various components.

Fig. 9.23 A simplified small-signal model used for noise analysis.
due to the resistor load, and therefore we can assume that $\mathrm{C}_{\mathrm{gd}}$ and $\mathrm{C}_{\mathrm{db}}$ can be ignored. The transfer function from $\mathrm{i}_{\mathrm{in}}$ to the output is found by using nodal analysis to be

$$
\begin{equation*}
\frac{V_{\text {out }}(s)}{I_{\text {in }}(s)}=R_{F}\left(\frac{A_{V}}{1+A_{V}}\right) \frac{1}{1+s\left(\frac{R_{F} C_{T}}{1+A_{V}}\right)} \tag{9.111}
\end{equation*}
$$

where $A_{V}=A_{1} A_{2}$ is the total voltage gain of the preamp and $C_{T}=C_{g s}+C_{i n}$. It is also found that this is the same transfer function from $I_{R}^{2}$ to the output. Thus, the noise current source $I_{R}^{2}$ can be replaced by an input current noise source having a spectral density of $4 k T / R_{F}$. In a typical design, one would choose $R_{F}$ as large as possible to limit this noise. However, this choice is constrained by the bandwidth requirements of passing the signal frequencies. From (9.111), we have the $-3-\mathrm{dB}$ frequency of the amplifier, given by

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}}=\frac{1+\mathrm{A}_{\mathrm{V}}}{\mathrm{R}_{\mathrm{F}} \mathrm{C}_{\mathrm{T}}} \tag{9.112}
\end{equation*}
$$

For a given amplifier gain and detector capacitance, $R_{F}$ is chosen using (9.112) to place the $-3-\mathrm{dB}$ frequency as small as possible without substantially attenuating the signals. This makes the dominant node for determining stability the input node. The bandwidth of the second amplifier must be substantially greater than that of the input node to guarantee stability. Unfortunately, this constraint greatly amplifies the thermal noise due to input transistor $\mathrm{Q}_{1}$, as we will see next.

The gain from the noise source $I_{D}^{2}$ to the output is found by using nodal analysis to be

$$
\begin{equation*}
\frac{V_{\text {out }}(s)}{I_{D}(s)}=\frac{1}{g_{m}} \frac{A_{V}}{1+A_{V}} \frac{1+s R_{F} C_{T}}{1+s\left[\frac{R_{F} C_{T}}{\left(1+A_{V}\right)}\right]} \tag{9.113}
\end{equation*}
$$

At low frequencies, this gain is approximately given by $1 / g_{m}$, whereas at high frequencies it is as much as $1+A_{V}$ times greater. Thus, the high-frequency output noise due to $Q_{1}$ is much greater than the low-frequency noise due to $\mathrm{Q}_{1}$. Furthermore, the only bandwidth limitation of this noise at high frequencies is due to the finite bandwidth of the second amplifier, $\mathrm{A}_{2}$. From the discussion on compensation in Chapter 5, we know the second pole frequency of the amplifier must be almost four times greater than the closed-loop -3-dB frequency when lead compensation is not used. ${ }^{8}$

Continuing, in order to refer the noise due to $Q_{1}$ back to the input, we use (9.111) and (9.113) to obtain

$$
\begin{equation*}
I_{i D}^{2}(f)=I_{D}^{2}(f)\left|\frac{V_{\text {out }}(j \omega)}{I_{D}(j w)}\right|^{2}\left|\frac{I_{i n}(j \omega)}{V_{\text {out }}(j w)}\right|^{2}=I_{D}^{2}(f) \frac{1+\omega^{2}\left(R_{F} C_{T}\right)^{2}}{\left(g_{m} R_{F}\right)^{2}} \tag{9.114}
\end{equation*}
$$

We use

$$
\begin{equation*}
I_{D}^{2}(f)=4 k T \gamma g_{m} \tag{9.115}
\end{equation*}
$$

and we add to this the input noise source that models the noise of the feedback resistor to obtain the total inputreferred noise, given by

$$
\begin{equation*}
I_{i}^{2}(f)=\frac{4 k T}{R_{F}}+4 k T \gamma \frac{1+\omega^{2}\left(R_{F} C_{T}\right)^{2}}{g_{m} R_{F}^{2}} \tag{9.116}
\end{equation*}
$$

Notice that the second term starts to quickly increase at a frequency of

$$
\begin{equation*}
\omega_{z}=\frac{1}{R_{F} C_{T}}=\frac{\omega_{-3 \mathrm{~dB}}}{1+A_{V}} \tag{9.117}
\end{equation*}
$$

which is a relatively low frequency.
Continuing, normally $\gamma /\left(g_{m} R_{F}\right) \ll 1$, and we have

$$
\begin{align*}
I_{i}^{2}(f) & =\frac{4 k T}{R_{F}}\left(1+\frac{\gamma}{g_{m} R_{F}}\right)+4 k T \gamma \frac{\omega^{2} C_{T}^{2}}{g_{m}} \\
& \cong \frac{4 k T}{R_{F}}+4 k T \gamma \frac{\omega^{2} C_{T}^{2}}{g_{m}} \tag{9.118}
\end{align*}
$$

Using the facts that

$$
\begin{equation*}
g_{m}=\mu_{n} C_{o x} \frac{W}{L} V_{\text {eff }} \tag{9.119}
\end{equation*}
$$

and that

$$
\begin{equation*}
\mathrm{C}_{\mathrm{gs}}=\frac{2}{3} \mathrm{C}_{\mathrm{ox}} \mathrm{WL} \tag{9.120}
\end{equation*}
$$

we can write (9.118) as

$$
\begin{equation*}
I_{i}^{2}(f) \cong \frac{4 k T}{R_{F}}+\frac{16}{9} k T \frac{L^{2}}{\mu_{n} V_{\text {eff }}} \omega^{2} \frac{\left(C_{g s}+C_{i n}\right)^{2}}{C_{g s}} \tag{9.121}
\end{equation*}
$$

Normally, $\mathrm{V}_{\text {eff }}$ is taken as large as possible given power-supply-voltage and power-dissipation constraints. The only parameter left for the designer to choose is the width of the input transistor and, therefore, $\mathrm{C}_{\mathrm{gs}}$. It can be shown (by differentiating the second term of (9.121) with respect to $\mathrm{C}_{g \mathrm{~g}}$ and then setting the result to zero) that the second term of $(9.121)$ is minimized by the choice $C_{g s}=C_{i n}$, in which case we have

$$
\begin{equation*}
\mathrm{I}_{\mathrm{i}}^{2}(\mathrm{f}) \cong 4 \mathrm{kT}\left(\frac{1}{\mathrm{R}_{F}}+\frac{4}{9} \frac{\mathrm{~L}^{2}}{\mu_{\mathrm{n}} \mathrm{~V}_{\mathrm{eff}}} \omega^{2} \mathrm{C}_{\mathrm{in}}\right) \tag{9.122}
\end{equation*}
$$

## 9.5 DYNAMIC RANGE PERFORMANCE

Analog circuits generally have many different performance criteria that must be met so that overall system performance meets specifications. Whereas noise limits the value of the smallest useful signals, linearity limits the value of the largest useful signals that can occur in the circuit. Thus, we find that linearity and noise together determine
the useful dynamic range of a circuit. It should be noted here that the dynamic range of integrated analog circuits is often a crucial measure since its value is often low and can seriously impair system performance.

### 9.5.1 Total Harmonic Distortion (THD)

If a sinusoidal waveform is applied to a linear time-invariant system, it is well known that the output will also be a sinusoidal waveform at the same frequency, but possibly with different magnitude and phase values. However, if the same input is applied to a nonlinear system, the output signal will have frequency components at harmonics of the input waveform, including the fundamental (or first) harmonic. For example, if a 1-MHz sinusoidal input signal is used, the output signal will have power at the fundamental, 1 MHz , as well as at the harmonic frequencies, 2 MHz , $3 \mathrm{MHz}, 4 \mathrm{MHz}$, and so on.

Specifically, consider a nonlinear system ${ }^{9}$ with an input signal, $\mathrm{v}_{\mathrm{in}}(\mathrm{t})$, and an output signal, $\mathrm{v}_{\mathrm{o}}(\mathrm{t})$. The output signal can be written as a Taylor series expansion of the input signal:

$$
\begin{equation*}
v_{0}(t)=a_{1} v_{i n}(t)+a_{2} v_{i n}^{2}(t)+a_{3} v_{\text {in }}^{3}(t)+a_{4} v_{i n}^{4}(t)+\cdots \tag{9.123}
\end{equation*}
$$

Here, the linear term is $a_{1}$, whereas $a_{2}, a_{3}$, and $a_{4}$ characterize the second-, third-, and fourth-order distortion terms, respectively. In fully differential circuits, all even terms (i.e., $a_{2}$ and $a_{4}$ ) are small, so typically $a_{3}$ dominates and we approximate $\mathrm{V}_{\mathrm{o}}(\mathrm{t})$ as

$$
\begin{equation*}
v_{0}(t) \cong a_{1} v_{i n}(t)+a_{3} v_{i n}^{3}(t) \tag{9.124}
\end{equation*}
$$

If $v_{i n}(t)$ is a sinusoidal signal given by

$$
\begin{equation*}
\mathrm{v}_{\mathrm{in}}(\mathrm{t})=\mathrm{A} \cos (\omega \mathrm{t}) \tag{9.125}
\end{equation*}
$$

the output signal can be shown to be approximated by

$$
\begin{equation*}
v_{0}(t) \cong a_{1} A \cos (\omega t)+\frac{a_{3}}{4} A^{3}[3 \cos (\omega t)+\cos (3 \omega t)] \tag{9.126}
\end{equation*}
$$

where we see a fundamental term and a third-harmonic term. Defining $H_{D 1}$ and $H_{D 3}$ to be the amplitudes of the fundamental and third-harmonic terms, respectively, we can write

$$
\begin{equation*}
\mathrm{v}_{\mathrm{o}}(\mathrm{t}) \equiv \mathrm{H}_{\mathrm{D} 1} \cos (\omega \mathrm{t})+\mathrm{H}_{\mathrm{D} 3} \cos (3 \omega \mathrm{t}) \tag{9.127}
\end{equation*}
$$

Since, typically, (3/4) $a_{3} A^{3} \ll a_{1} A$, one usually approximates the linear component of the output signal as

$$
\begin{equation*}
\mathrm{H}_{\mathrm{D} 1}=\mathrm{a}_{1} \mathrm{~A} \tag{9.128}
\end{equation*}
$$

and the third-harmonic term as

$$
\begin{equation*}
H_{D 3}=\frac{a_{3}}{4} A^{3} \tag{9.129}
\end{equation*}
$$

Finally, we see that the third-order distortion term results in power at the third harmonic frequency and the ratio of $H_{D 3} / H_{D 1}$ is defined as the third-order harmonic distortion ratio, given by

$$
\begin{equation*}
\mathrm{HD}_{3} \equiv \frac{\mathrm{H}_{\mathrm{D} 3}}{\mathrm{H}_{\mathrm{D} 1}}=\left(\frac{\mathrm{a}_{3}}{\mathrm{a}_{1}}\right)\left(\frac{\mathrm{A}^{2}}{4}\right) \tag{9.130}
\end{equation*}
$$

The total harmonic distortion (THD) of a signal is defined to be the ratio of the total power of all second and higher harmonic components to the power of the fundamental for that signal. In units of dB , THD is found using
9. We assume here that the nonlinear system is memoryless and time invariant. Unfortunately, circuits are not memoryless, and a Volterra series should be used; however, this assumption simplifies the analysis and usually results in good approximations for distortion figures.
the following relation:

$$
\begin{equation*}
\mathrm{THD}=10 \log \left(\frac{\mathrm{H}_{\mathrm{D} 2}^{2}+\mathrm{H}_{\mathrm{D} 3}^{2}+\mathrm{H}_{\mathrm{D} 4}^{2}+\cdots}{\mathrm{H}_{\mathrm{D} 1}^{2}}\right) \tag{9.131}
\end{equation*}
$$

Sometimes THD is presented as a percentage value. In this case,

$$
\begin{equation*}
\mathrm{THD}=\frac{\sqrt{\mathrm{H}_{\mathrm{D} 2}^{2}+\mathrm{H}_{\mathrm{D} 3}^{2}+\mathrm{H}_{\mathrm{D} 4}^{2}+\cdots}}{\mathrm{H}_{\mathrm{D} 1}} \times 100 \% \tag{9.132}
\end{equation*}
$$

For example, a 0.1 -percent THD value implies that the amplitude of the fundamental is 1,000 times larger than the amplitude of the harmonic components. This 0.1 -percent THD value is equivalent to a value of -60 dB THD. It should also be noted that the THD value is almost always a function of the amplitude of the input (or output) signal level, and thus the corresponding signal amplitude must also be reported. Also, for practical reasons, typically the power of only the first few harmonics (say, the first 5) are included since the distortion components usually fall off quickly for higher harmonics.

The total harmonic distortion of a circuit deteriorates as the applied signal amplitudes are increased. This is intuitive since we regularly employ linear circuit models for the analysis of small signals. For example, in the case of a fully-differential circuit where the dominant distortion is $\mathrm{H}_{\mathrm{D}_{3}}$, the total harmonic distortion is approximately equal to $\mathrm{HD}_{3}$, which in (9.130) is shown to be proportional the input amplitude squared, $\mathrm{A}^{2}$.

One difficulty with the use of THD in reporting circuit performance is that often the harmonic components fall outside of the circuit's usable bandwidth, and thus the THD value is falsely improved. For example, if a 21-MHz low-pass filter is being tested, then a $5-\mathrm{MHz}$ input signal results in the $10-\mathrm{MHz}, 15-\mathrm{MHz}$, and $20-\mathrm{MHz}$ components falling within the passband, whereas higher distortion components will be attenuated by the filter. However, circuit linearity is often worse when higher input signal frequencies are applied due to nonlinear capacitances or, worse, nonlinear signal

Key Point: Total harmonic distortion (THD) measures the ratio of fundamental signal power to that of all harmonics. A THD measurement is straightforward to perform only when the fundamental signal frequency is well below the circuit's upper passband limit.
cancellation. Thus, it is useful to measure circuit linearity with input signals near the upper edge of the passband. Unfortunately, if a $20-\mathrm{MHz}$ input signal is applied to the example low-pass filter, the second and higher harmonic components lie in the stopband and the THD value will indicate much better linearity than would occur for a practical application. Moreover, the testing of a narrowband filter always has this THD measurement difficulty since the use of an input frequency in the passband will result in harmonics that will certainly be attenuated by the filter's stopband. In summary, a THD measurement is straightforward to perform but does not work well in the important test of high-frequency signals near the upper passband limit of the circuit. Fortunately, as we will see next, one can use intermodulation tests to measure circuit linearity near the upper passband edge.

#### EXAMPLE 9.12

Calculate the THD value of a signal in which the fundamental component is at 1 MHz and has a power level of -10 dBm , and the only significant harmonics are the first three above the fundamental. These harmonics, at $2 \mathrm{MHz}, 3 \mathrm{MHz}$, and 4 MHz , are measured to have power levels of $-53 \mathrm{dBm},-50 \mathrm{dBm}$, and -56 dBm , respectively.

#### Solution

Recalling that 0 dBm refers to a $1-\mathrm{mW}$ signal, then the power of the fundamental component is $100 \mu \mathrm{~W}$, whereas the power of the first three harmonics are $5 \mathrm{nW}, 10 \mathrm{nW}$, and 2.5 nW , respectively. Thus, the total power of the harmonics is equal to

$$
\begin{equation*}
P_{\text {harm }}=5+10+2.5=17.5 \mathrm{nW} \tag{9.133}
\end{equation*}
$$

As a result, the THD is calculated to be

$$
\begin{equation*}
\mathrm{THD}=10 \log \left(\frac{17.5 \mathrm{nW}}{100 \mu \mathrm{~W}}\right)=-37.6 \mathrm{~dB} \tag{9.134}
\end{equation*}
$$

### 9.5.2 Third-Order Intercept Point (IP3)

Here, we introduce the concept of the third-order intercept point (IP3) as a measure for the third-order distortion component [Carson, 1990]. Unfortunately, as just noted, distortion terms for a single sinusoidal input often lie outside of a circuit's bandwidth, and thus we resort to an intermodulation test to move the distortion term back near the frequency of the input signals. We focus here on third-order distortion since, for fully differential circuits, the even-order distortion components are ideally zero and, thus, third-order distortion typically dominates. However, in cases where second-order distortion dominates, a similar concept is also possible and is referred to as the sec-ond-order intercept point (IP2).

Consider an intermodulation test, where the input signal consists of two equally sized sinusoidal signals and is written as

$$
\begin{equation*}
v_{i n}(t)=A \cos \left(\omega_{1} t\right)+A \cos \left(\omega_{2} t\right) \tag{9.135}
\end{equation*}
$$

Presuming the input-output relationship of (9.123), the output signal can be shown to be approximated by

$$
\begin{align*}
v_{0}(t) \cong & \left(a_{1} A+\frac{9 a_{3}}{4} A^{3}\right)\left[\cos \left(\omega_{1} t\right)+\cos \left(\omega_{2} t\right)\right] \\
& +\frac{a_{3}}{4} A^{3}\left[\cos \left(3 \omega_{1} t\right)+\cos \left(3 \omega_{2} t\right)\right]  \tag{9.136}\\
& +\frac{3 a_{3}}{4} A^{3}\left[\cos \left(2 \omega_{1} t+\omega_{2} t\right)+\cos \left(2 \omega_{2} t+\omega_{1} t\right)\right] \\
& +\frac{3 a_{3}}{4} A^{3}\left[\cos \left(\omega_{1} t-\Delta \omega t\right)+\cos \left(\omega_{2} t+\Delta \omega t\right)\right]
\end{align*}
$$

where $\Delta \omega$ is defined to be the difference between the input frequencies (i.e., $\Delta \omega \equiv \omega_{2}-\omega$ ) which we assume to be small. Here, we see that the first line of (9.136) is the fundamental components, the second line shows the levels at three times the fundamentals, the third line also describes distortion at nearly three times the fundamentals, and the fourth line describes the distortion levels at two new frequencies that are close to the input frequencies (slightly below $\omega_{1}$ and slightly above $\omega_{2}$ ). As a result, for a narrowband or low-pass circuit, these two new distortion components (due to third-order distortion) fall in the passband and can be used to predict the third-order distortion term.

Using the same notation as in the harmonic distortion case, we have the intermodulation distortion levels given by

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D} 1}=\mathrm{a}_{1} \mathrm{~A} \tag{9.137}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D} 3}=\frac{3 \mathrm{a}_{3}}{4} \mathrm{~A}^{3} \tag{9.138}
\end{equation*}
$$

The ratio of these two is the third-order intermodulation value, given by

$$
\begin{equation*}
I D_{3}=\frac{I_{D 3}}{I_{D 1}}=\left(\frac{a_{3}}{a_{1}}\right)\left(\frac{3 A^{2}}{4}\right) \tag{9.139}
\end{equation*}
$$

[^0]:    1. A practical lower limit of 10 's of $\mu \mathrm{A}$ is usually established for $I_{d}$ since smaller currents can result in too much noise on the resulting bias voltages.
[^1]:    2. Also, if on-chip resistors, such as well or diffusion resistors, are used, this effect will be somewhat offset by their positive tempera-ture-coefficient dependency.
[^2]:    3. It is here assumed the reader is familiar with the basics of bipolar transistors. If needed, the reader may refer to Section 8.1.1 for this background.
[^3]:    H. Banba, H. Shiga, A. Umezawa, T. Miyaba, T. Tanzawa, S. Atsumi, and K. Sakui. "A CMOS Bandgap Reference Circuit with Sub-1-V Operation," IEEE Journal of Solid-State Circuits, Vol. 34, no. 5, pp. 670-674, May 1999.
P. Brokaw. "A Simple Three-Terminal IC Bandgap Reference," IEEE Journal of Solid-State Circuits, Vol. SC-9, pp. 388-393, December 1974.
J. Brugler. "Silicon Transistor Biasing for Linear Collector Current Temperature Dependence," IEEE Journal of Solid-State Circuits, Vol. SC-2, pp. 57-58, June 1967.

[^4]:    1. In many bipolar processes, pnp transistors are only available as lateral devices.
[^5]:    1. For those more rigorously inclined, we assume throughout this chapter that random signals are ergodic, implying their ensemble averages can be approximated by their time averages.
[^6]:    4. Carbon resistors are not used in integrated-circuit design but are available as discrete elements.
[^7]:    5. An exception to this is high-frequency designs in which the collector shot noise becomes more important because, at high frequencies, $\beta$ becomes small. In this case, the input current noise source is partially correlated with the input voltage noise source. If neither noise source dominates, then the correct analysis is more difficult and beyond the scope of this text. Fortunately, this case is not often encountered in practice.

image_name:Fig. 9.24
description:The graph in Fig. 9.24 is a plot illustrating the third-order intercept point (IP3) in terms of input and output power levels, measured in dBm. The x-axis represents the input level A in dBm, while the y-axis shows the output power level, also in dBm.

The graph features two main lines: one representing the fundamental signal (ID1) and another representing the third-order intermodulation product (ID3). The fundamental signal line (ID1) has a slope of 1, indicating a linear relationship between input and output power levels. In contrast, the third-order intermodulation product line (ID3) has a slope of 3, indicating a cubic relationship.

The plot shows how the output power level of the fundamental rises linearly with increasing input level, while the intermodulation product rises more steeply, due to its cubic nature. As input power increases, both lines eventually compress, deviating from their initial linear and cubic paths.

Key points on the graph include the input third-order intercept point (IIP3) and the output third-order intercept point (OIP3). These points are where the extrapolated linear and cubic lines would intersect if they continued without compression. However, in practice, these points cannot be measured directly because the fundamental and intermodulation products compress at high power levels, preventing the lines from reaching the intercept points.

Annotations on the graph highlight these intercept points and the slopes of the lines. The third-order intercept point is marked, emphasizing its theoretical nature due to the compression effects. The graph serves to illustrate the concept of third-order intercept points in RF and communication systems, where linearity and intermodulation distortion are significant considerations.

Fig. 9.24 Graphical illustration of the third-order intercept-point. $\mathrm{IIP}_{3}$ and $\mathrm{OIP}_{3}$ are the input and output third-order intercept points, respectively. They cannot be measured directly due to compression of the fundamental and intermodulation products at high-power levels.

From (9.137) and (9.138), note that, as the amplitude of the input signal, A , is increased, the level of the fundamental rises linearly, whereas the $I_{D 3}$ rises in a cubic fashion. For example, if $A$ is increased by 1 dB , then $I_{D 1}$ also increases by 1 dB while $\mathrm{I}_{\mathrm{D} 3}$ increases by 3 dB . Thus, when the fundamental and intermodulation levels are plotted in a dB scale against the signal amplitude, A , the two curves are linear, but with different slopes, as shown in Fig. 9.24. The third-order intercept point is defined to be the intersection of these two lines. Note, however, that as the signal amplitude rises, the linear relationships of $I_{D 1}$ and $I_{D 3}$ are no longer obeyed due to the large amount of nonlinearities violating some of our original assumptions. For example, in (9.136), we ignored the cubic A term in estimating the fundamental level, $\mathrm{I}_{\mathrm{D} 1}$. Also, other distortion terms that were ignored now become important. As a result, it is impossible to directly measure the third-order intercept point, and thus it must be extrapolated from the measured data. The third-order intercept point results in two values- $\mathrm{IIP}_{3}$ and $\mathrm{OIP}_{3}$, which are related to the input and output levels, respectively. If the linear gain term, $a_{1}$, is unity (or, equivalently, 0 dB ), then $I I P_{3}=$ OIP $_{3}$. However, if $\mathrm{a}_{1}$ is not unity, one must be careful to state which of the two intercept points is being reported.

Knowledge of the third-order intercept point is quite useful in determining what signal level should be chosen to achieve a desired intermodulation ratio, $\mathrm{ID}_{3}$. Specifically, we see from (9.139) that $\mathrm{ID}_{3}$ improves by 2 dB for every 1 dB of signal level decrease (since it is related to $A^{2}$ ) and that $\mathrm{OIP}_{3}$ is defined to be the $I_{D 1}$ point where $\mathrm{ID}_{3}=0 \mathrm{~dB}$. Thus, we have the simple relationship (all in decibels)

$$
\begin{equation*}
\mathrm{OIP}_{3}=\mathrm{I}_{\mathrm{D} 1}-\frac{\mathrm{ID}_{3}}{2} \tag{9.140}
\end{equation*}
$$

image_name:Fig. 9.25 Graphical illustration of spurious-free dynamic range (SFDR)
description:The graph is a linear plot illustrating the concept of spurious-free dynamic range (SFDR) in the context of intermodulation distortion. The x-axis represents the input level (A) in dBm, while the y-axis represents output power also in dBm.

The graph features two main lines:

1. **Fundamental Output Line:** This line starts from a point labeled \( I_{D1} \) and extends linearly upwards with a slope of 1, representing the fundamental signal's output power as the input power increases.

2. **Third-Order Intermodulation Product Line:** This line begins at \( I_{D3} \) and has a steeper slope of 3, indicating how the third-order intermodulation products increase more rapidly with input power compared to the fundamental.

**Key Points and Features:**
- **OIP3 (Output Third-Order Intercept Point):** This is where the extrapolated fundamental output line and the third-order intermodulation product line intersect. It is labeled on the y-axis.
- **IIP3 (Input Third-Order Intercept Point):** This is the corresponding point on the x-axis where the input level would theoretically result in the fundamental and third-order products being equal.
- **SFDR (Spurious-Free Dynamic Range):** This is the range between the noise floor (\( N_0 \)) and the point where the third-order intermodulation products become significant, denoted by \( I^*_{D1} \) and \( I^*_{D3} \).
- **Noise Floor (\( N_0 \)):** This horizontal line indicates the minimum detectable signal level, below which signals are obscured by noise.

The graph visually demonstrates how the SFDR is determined by the distance between the noise floor and the point where the third-order intermodulation products intersect with the noise floor. This range is critical for ensuring that the output signal remains free from significant intermodulation distortion.

Fig. 9.25 Graphical illustration of spurious-free dynamic range (SFDR).

#### EXAMPLE 9.13

If $\mathrm{OIP}_{3}=20 \mathrm{dBm}$, what output-signal level should be used such that the third-order intermodulation products are 60 dB below the fundamental?

#### Solution

Using (9.140) with $\mathrm{ID}_{3}=-60 \mathrm{~dB}$, we have

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D} 1}=\mathrm{OIP}_{3}+\frac{\mathrm{ID}_{3}}{2}=-10 \mathrm{dBm} \tag{9.141}
\end{equation*}
$$

Thus, an output level of -10 dBm should be used.

### 9.5.3 Spurious-Free Dynamic Range (SFDR)

Spurious-free dynamic range (SFDR) is defined to be the signal-to-noise ratio when the power of the distortion equals the noise power. In an intermodulation test, the third order intermodulation products are the dominant distortion. In Fig. 9.25, the circuit's total output noise power is shown along the vertical axis as $\mathrm{N}_{0}$. If a low enough signal level is used, $\mathrm{I}_{\mathrm{D} 3}$ will be well below the noise floor. However, since $\mathrm{I}_{\mathrm{D} 3}$ rises 3 dB for every 1 dB of signallevel increase, there will soon be a point where $I_{D_{3}}$ is equal to the noise power. As the figure shows, SFDR is defined to be the output SNR ratio when $\mathrm{I}_{\mathrm{D} 3}$ is equal to $\mathrm{N}_{0}$. Alternatively, one can measure SFDR using the inputsignal levels as the difference between the level that results in $I_{D 3}=N_{o}$ and the level $A_{N o}$ that results in a fundamental output level equal to $\mathrm{N}_{0}$.

To find a formula relating SFDR, $\mathrm{OIP}_{3}$, and $\mathrm{N}_{0}$ (all in dB units), we first note that

$$
\begin{equation*}
\mathrm{SFDR}=\mathrm{I}_{\mathrm{D} 1}^{*}-\mathrm{N}_{\mathrm{o}}=\mathrm{I}_{\mathrm{D} 1}^{*}-\mathrm{I}_{\mathrm{D} 3}^{*} \tag{9.142}
\end{equation*}
$$

where $I_{D 1}^{*}$ and $I_{D 3}^{*}$ refer to the output and distortion levels when $I_{D 3}=N_{0}$, as shown in Fig. 9.25. Since the units are assumed to be in dB , we also have, from (9.139),

$$
\begin{equation*}
\mathrm{ID}_{3}=\mathrm{I}_{\mathrm{D} 3}-\mathrm{I}_{\mathrm{D} 1} \tag{9.143}
\end{equation*}
$$

Using (9.140), we have

$$
\begin{equation*}
\mathrm{OIP}_{3}=\mathrm{I}_{\mathrm{D} 1}^{*}-\frac{\left(\mathrm{N}_{\mathrm{o}}-\mathrm{I}_{\mathrm{D} 1}^{*}\right)}{2} \tag{9.144}
\end{equation*}
$$

and substituting in $\mathrm{I}_{\mathrm{D} 1}^{*}=\mathrm{SFDR}+\mathrm{N}_{\circ}$ from (9.142) and rearranging, we have

$$
\begin{equation*}
\mathrm{SFDR}=\frac{2}{3}\left(\mathrm{OIP}_{3}-\mathrm{N}_{\mathrm{o}}\right) \tag{9.145}
\end{equation*}
$$

#### EXAMPLE 9.14

At an input-signal level of 0 dBm , an intermodulation ratio of -40 dB was measured in a circuit with a gain of 2 dB. Calculate the value of the input and output third-order intercept points. What input-signal level should be applied if one wants an intermodulation ratio of -45 dB ? If the noise power at the output is measured to be -50 dBm , what is the expected SFDR, and what output-signal level does it correspond to?

#### Solution

With an input level of 0 dBm and a gain of 2 dB , the output level is $\mathrm{I}_{\mathrm{D} 1}=2 \mathrm{dBm}$ with a measured value of $I D_{3}=-40 \mathrm{~dB}$. Using (9.140), we have

$$
\begin{equation*}
\mathrm{OIP}_{3}=\mathrm{I}_{\mathrm{D} 1}-\frac{\mathrm{ID}_{3}}{2}=22 \mathrm{dBm} \tag{9.146}
\end{equation*}
$$

whereas the $\mathrm{IIP}_{3}$ is 2 dB lower (i.e., $\operatorname{IIP}_{3}=20 \mathrm{dBm}$ ).
For signal levels corresponding to an intermodulation of $\mathrm{ID}_{3}=45 \mathrm{~dB}$, we have

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D} 1}=\mathrm{OIP}_{3}+\frac{\mathrm{ID}_{3}}{2}=22-\frac{45}{2}=-0.5 \mathrm{dBm} \tag{9.147}
\end{equation*}
$$

However, this value is the level of the output signal, so the input signal should be 2 dB lower or, equivalently, the input-signal level should be at -2.5 dBm . Note that this result could have been obtained more directly by noting that a $5-\mathrm{dB}$ improvement in distortion was desired, implying that the signal level should be decreased by $(5 \mathrm{~dB}) / 2$.

Finally, we use (9.145) to find

$$
\begin{equation*}
\mathrm{SFDR}=\frac{2}{3}(22+50)=48 \mathrm{~dB} \tag{9.148}
\end{equation*}
$$

from which the output level is given by

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D}_{1}}^{*}=\mathrm{SFDR}+\mathrm{N}_{\mathrm{o}}=-2 \mathrm{dBm} \tag{9.149}
\end{equation*}
$$

Thus, when the output level is at -2 dBm , the third-order intermodulation power equals the noise power. If the output level is increased, the distortion products will increase and limit the dynamic-range performance. However, if the output level is decreased, the distortion products will be buried below the noise floor, and the noise will limit dynamic-range performance. Therefore, optimum dynamic-range performance is obtained at an output level of -2 dBm . However, note that the dynamic-range performance is actually 3 dB below the SFDR value since the dynamic range is based on the ratio of the signal power to the distortion plus the noise power (which are both equal at this point).

### 9.5.4 Signal-to-Noise and Distortion Ratio (SNDR)

The signal-to-noise and distortion ratio (SNDR) of a signal is defined as the ratio of the signal power to the total power in all noise and distortion components. Usually measured with a single-tone input, the signal power is the amplitude of the fundamental, and the distortion includes all harmonics.

$$
\begin{equation*}
\text { SNDR }=10 \log \left(\frac{V_{f}^{2}}{N_{0}+V_{h 2}^{2}+V_{h 3}^{2}+V_{h 4}^{2}+\cdots}\right) \tag{9.150}
\end{equation*}
$$

Unlike SFDR, SNDR is a function of signal amplitude. For small signal power levels, the harmonics are negligible relative to the noise, and the SNDR is well approximated by the $\mathrm{SNR}, \mathrm{SNDR} \cong 10 \log \left(\mathrm{~V}_{\mathrm{f}}^{2} / \mathrm{N}_{\mathrm{o}}\right)$. In this circumstance, assuming the noise power remains constant as the signal power varies, we see an increasing SNDR with increasing signal power. By contrast, at high signal power levels the harmonic distortion terms dominate the denominator of (9.150), at which point SNDR is approximately equal to $1 /$ THD, SNDR $\cong 10 \log \left(V_{f}^{2} / V_{h 2}^{2}+V_{h 3}^{2}+V_{h 4}^{2}+\cdots\right)$. Since harmonic power levels increase faster than the fundamental power, SNDR decreases at high signal powers. Hence, SNDR varies with signal amplitude as shown in Fig. 9.26. SNDR is maximized at a particular input amplitude. The maximal value SNDR $_{\text {max }}$ is, like SFDR, a useful metric for quantifying the dynamic range of a circuit.
image_name:Fig. 9.26
description:The graph in Fig. 9.26 is a plot illustrating the variation of Signal-to-Noise and Distortion Ratio (SNDR) with signal amplitude (A) in an analog circuit. The graph is a line plot with the vertical axis labeled as 'SNDR (dB)' indicating the Signal-to-Noise and Distortion Ratio measured in decibels, and the horizontal axis labeled as 'A', representing the signal amplitude without specific units provided.

The graph shows a curve that rises sharply from the left, reaches a peak, and then gradually declines to the right. This behavior indicates that SNDR increases with signal amplitude up to a certain point, beyond which it begins to decrease. The peak of the curve represents the maximum SNDR (SNDR_max), which is marked with a dashed horizontal line indicating the highest value of SNDR achievable at an optimal signal amplitude.

The graph is divided into two regions along the horizontal axis: 'Noise-limited' and 'Distortion-limited'. In the noise-limited region, at lower amplitudes, the SNDR increases as the signal amplitude increases, suggesting that noise is the dominant factor limiting performance. In the distortion-limited region, at higher amplitudes, the SNDR decreases with increasing amplitude, indicating that distortion becomes the dominant limiting factor.

This graph effectively demonstrates that there is an optimal signal amplitude where SNDR is maximized, balancing between noise and distortion in the system.

Fig. 9.26 Variation of SNDR with signal amplitude in an analog circuit.

## 9.6 KEY POINTS

- This chapter focuses on noise inherent to the physical operation of electronic components, not noise from outside interferences. Such noise sources are generally zero-mean. [p. 363]
- Although the instantaneous value of a noise voltage or current cannot be determined by analysis, the rms value obtained by time-averaging its square provides a normalized measure of the noise signal's power. [p. 364]
- $\quad$ SNR is the ratio of signal power to noise power, both normalized to the same impedance and expressed in dB . [p. 365]
- Units of dBm express an average power level on a logarithmic scale normalized to 1 mW , so that 1 mW is 0 dBm and 0.1 mW is 10 dBm . Rms voltages or currents are also sometimes expressed in dBm by assuming that they are applied to some agreed-upon reference load, usually either 50 or 75 Ohms. [p. 365]
- The power of independent (uncorrelated) noise sources superimpose linearly, which means their voltages and currents superimpose in a root-sum-of-squares fashion. As a result, to lower overall noise, one must focus on the largest noise contributors. [p. 366]
- The mean square value of a noise signal is the integral of its spectral density over all frequencies. [p. 369]
- The frequency-domain representation of a noise signal is its spectral density: the average normalized power that may be measured within a 1-Hz bandwidth. [p. 368]
- White noise has a spectral density that is constant over all frequencies. [p. 369]
- Flicker noise, or 1/f-noise, has a spectral density proportional to 1/f. Hence, it falls off at $-10 \mathrm{~dB} /$ decade. [p. 370]
- Uncorrelated noise signals remain uncorrelated, even when filtered by a circuit's magnitude response. [p. 372]
- Passing a noise signal through a circuit shapes its root spectral density by the circuit's magnitude response. [p. 372]
- The noise bandwidth of a given filter is equal to the frequency span of a brick-wall filter that has the same rms output noise as the given filter has when white noise is applied to both filters, assuming the same peak gain for both filters. [p. 373]
- The noise bandwidth of a first-order lowpass filter is $\pi / 2$ times the filter's -3 dB bandwidth. [p. 375]
- To determine the frequency region or regions that contribute the dominant noise, lower a $1 / \mathrm{f}$ noise line until it touches the spectral density curve. The total noise can be approximated by the noise in the vicinity of the 1/f line. [p. 377]
- Resistors exhibit thermal noise modeled either by a voltage source in series with the resistor having a white noise spectral density 4 kTR , or a Norton equivalent current source having a white noise spectral density $4 \mathrm{kT} / \mathrm{R}$. [p. 378]
- Diodes exhibit shot noise modeled by a current source having a white noise spectral density $2 \mathrm{ql}_{\mathrm{D}}$. [p. 378]
- At low frequencies, $1 / \mathrm{f}$ noise is dominant in MOSFET circuits. It is minimized by using large gate areas and pchannel transistors wherever possible. [p. 380]
- Bipolar transistor noise is typically dominated by the thermal noise of the series base resistance, and shot noise in the base-current junction. [p. 380]
- MOSFET thermal noise is simply that of a resistor with value $r_{d s}$ when in triode. In active mode, thermal noise is modeled by a white current noise source between drain and source with spectral density $8 \mathrm{k} \mathrm{Tg}_{\mathrm{m}} / 3$, for a long channel device, and somewhat higher for short-channel devices. [p. 381]
- In a circuit comprising only capacitors and resistors (including triode MOSFETs) but no active devices, the squared rms noise on each capacitor is $\mathrm{kT} / \mathrm{C}$. [p. 383]
- The input-referred noise of a circuit, if applied to the input of a noiseless copy of the circuit, results in the exact same output noise as when all of the circuit's noise sources were present. It is found by dividing the observed output noise by the gain of the circuit. [p. 384]
- The input-referred noise of a circuit, if applied to the input of a noiseless copy of the circuit, results in the exact same output noise as when all of the circuit's noise sources were present. It is found by dividing the observed output noise by the gain of the circuit. [p. 384]
- Sampling an analog voltage on a capacitor captures both the signal component and noise with a mean-square value of $\mathrm{kT} / \mathrm{C}$, assuming a purely passive sampling network. [p. 384]
- The noise performance of a circuit at a particular frequency is usually reported as its input-referred noise spectrum, equal to the circuit's output noise spectrum divided by its magnitude response, or equivalently by its noise figure. [p. 387]
- To minimize thermal noise in a CMOS differential amplifier, the input pair transconductance should be maximized. For a fixed drain current, that implies operation in weak inversion or even subthreshold. [p. 394]
