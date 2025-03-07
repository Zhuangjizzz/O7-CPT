# 11. Noise in Integrated Circuits

## 11.1 Introduction

This chapter deals with the effects of electrical noise in integrated circuits. The noise phenomena considered here are caused by the small current and voltage fluctuations that are generated within the devices themselves, and we specifically exclude extraneous pickup of human-made signals that can also be a problem in high-gain circuits. The existence of noise is basically due to the fact that electrical charge is not continuous but is carried in discrete amounts equal to the electron charge, and thus noise is associated with fundamental processes in the integrated-circuit devices.

The study of noise is important because it represents a lower limit to the size of electrical signal that can be amplified by a circuit without significant deterioration in signal quality. Noise also results in an upper limit to the useful gain of an amplifier, because if the gain is increased without limit, the output stage of the circuit will eventually begin to limit (that is, a transistor will leave the active region) on the amplified noise from the input stages.

In this chapter the various sources of electronic noise are considered, and the equivalent circuits of common devices including noise generators are described. Methods of circuit analysis with noise generators as inputs are illustrated, and the noise analysis of complex circuits such as op amps is performed. Methods of computer analysis of noise are examined, and, finally, some common methods of specifying circuit noise performance are described.

## 11.2 Sources of Noise

### 11.2.1 Shot Noise ${ }^{1,2,3,4}$

Shot noise is always associated with a direct-current flow and is present in diodes, MOS transistors, and bipolar transistors. The origin of shot noise can be seen by considering the diode of Fig. 11.1 $a$ and the carrier concentrations in the device in the forward-bias region as shown in Fig. 11.1b. As explained in Chapter 1, an electric field $\mathscr{E}$ exists in the depletion region and a voltage $\left(\psi_{0}-V\right)$ exists between the $p$-type and the $n$-type regions, where $\psi_{0}$ is the built-in potential and $V$ is the forward bias on the diode. The forward current of the diode $I$ is composed of holes from the $p$ region and electrons from the $n$ region, which have sufficient energy to overcome the potential barrier at the junction. Once the carriers have crossed the junction, they diffuse away as minority carriers.

The passage of each carrier across the junction, which can be modeled as a random event, is dependent on the carrier having sufficient energy and a velocity directed toward the junction. Thus external current $I$, which appears to be a steady current, is, in fact, composed of
image_name:(a)
description:
[
name: D1, type: Diode, ports: {Na: V, Nc: GND}
]
extrainfo:The diagram shows a forward-biased pn junction diode with a voltage source V and current I flowing through the diode. The carrier concentration graph illustrates the depletion region and carrier distribution across the pn junction.
image_name:(b)
description:The graph in Figure 11.1 (b) depicts the carrier concentration in a forward-biased pn junction diode as a function of distance across the junction. The x-axis represents the distance across the junction, labeled as 'Distance,' and is divided into two regions: the p-type region on the left and the n-type region on the right. The y-axis represents 'Carrier concentration,' indicating the density of charge carriers in the diode.

The graph shows two main curves that represent the concentration of holes and electrons in the respective p and n regions. In the p-region, the hole concentration (labeled \( p_p \)) is initially high and remains relatively constant until it approaches the depletion region, where it sharply decreases. Conversely, the electron concentration (labeled \( n_p \)) in the p-region is low and increases slightly as it approaches the depletion region.

In the n-region, the electron concentration (labeled \( n_n \)) starts high and remains constant until it reaches the depletion region, where it sharply decreases. The hole concentration (labeled \( p_n \)) in the n-region is low and increases slightly as it approaches the depletion region.

The depletion region is marked by vertical dashed lines and is characterized by a significant drop in both hole and electron concentrations. This region is where the carrier concentrations from both sides converge and drop to minimal levels.

Overall, the graph illustrates the typical behavior of carrier concentrations in a forward-biased pn junction, showing high concentrations of majority carriers on either side of the junction and a significant reduction within the depletion region.

Figure 11.1 (a) Forward-biased pn junction diode. (b) Carrier concentrations in the diode (not to scale).
image_name:Figure 11.2
description:The graph in Figure 11.2 represents the diode current $I$ as a function of time $t$. The graph is a time-domain waveform, illustrating the behavior of current through a diode over a period.

**Axes Labels and Units:**
- The vertical axis is labeled as "Diode current $I$," though specific units are not provided in the image. It is assumed to be in amperes.
- The horizontal axis is labeled as time $t$, but again, specific units are not indicated. It is typically in seconds or milliseconds for such analyses.

**Overall Behavior and Trends:**
- The graph exhibits a fluctuating current around an average value, $I_D$, which is marked on the graph. This fluctuation is indicative of shot noise, a common phenomenon in diode currents.
- The current shows random and independent pulses, with variations around the average line. The fluctuations are generally small, suggesting a relatively stable average current with minor deviations.
- Towards the right end of the graph, the current stabilizes, and the fluctuations decrease, approaching the average current $I_D$ more closely.

**Key Features and Technical Details:**
- The average current $I_D$ is indicated with a dashed line, representing the mean value around which the current fluctuates.
- The fluctuations in the current are small and appear as a random noise pattern, reflecting the shot noise characteristics.
- There are no significant peaks or valleys, as the fluctuations are relatively minor compared to the average current level.

**Annotations and Specific Data Points:**
- The graph highlights the concept of shot noise with the average current $I_D$ being a reference point.
- No specific numerical values or additional annotations are provided beyond the indication of $I_D$.

This graph effectively illustrates the concept of shot noise in diode currents, showing how the actual current varies around a stable average value due to random fluctuations.

Figure 11.2 Diode current $I$ as a function of time (not to scale).
a large number of random independent current pulses. If the current is examined on a sensitive oscilloscope, the trace appears as in Fig. 11.2, where $I_{D}$ is the average current.

The fluctuation in $I$ is termed shot noise and is generally specified in terms of its meansquare variation about the average value. This is written as $\overline{i^{2}}$, where

$$
\begin{align*}
\overline{i^{2}} & =\overline{\left(I-I_{D}\right)^{2}} \\
& =\lim _{T \rightarrow \infty} \frac{1}{T} \int_{0}^{T}\left(I-I_{D}\right)^{2} d t \tag{11.1}
\end{align*}
$$

It can be shown that if a current $I$ is composed of a series of random independent pulses with average value $I_{D}$, then the resulting noise current has a mean-square value

$$
\begin{equation*}
\overline{i^{2}}=2 q I_{D} \Delta f \tag{11.2}
\end{equation*}
$$

where $q$ is the electronic charge $\left(1.6 \times 10^{-19} \mathrm{C}\right)$ and $\Delta f$ is the bandwidth in hertz. This equation shows that the noise current has a mean-square value that is directly proportional to the bandwidth $\Delta f$ (in hertz) of the measurement. Thus a noise-current spectral density $i^{2} / \Delta f$ (with units square amperes per hertz) can be defined that is constant as a function of frequency. Noise with such a spectrum is often called white noise. Since noise is a purely random signal, the instantaneous value of the waveform cannot be predicted at any time. The only information available for use in circuit calculations concerns the mean square value of the signal given by (11.2). Bandwidth $\Delta f$ in (11.2) is determined by the circuit in which the noise source is acting.

Equation 11.2 is valid until the frequency becomes comparable to $1 / \tau$, where $\tau$ is the carrier transit time through the depletion region. For most practical electronic devices, $\tau$ is extremely
image_name:Figure 11.3 Spectral density of shot noise in a diode with transit time
description:The graph in Figure 11.3 is a plot of the spectral density of shot noise in a diode as a function of frequency, labeled as \( f \). It is a linear plot with both axes on a linear scale.

1. **Axes Labels and Units:**
- The horizontal axis represents frequency \( f \), with specific points marked at \( 0.5/\tau \), \( 1/\tau \), and \( 1.5/\tau \). \( \tau \) is the carrier transit time through the depletion region.
- The vertical axis represents the noise current spectral density divided by the bandwidth \( \Delta f \), denoted as \( \frac{i^2}{\Delta f} \).

2. **Overall Behavior and Trends:**
- The graph starts at a high value on the vertical axis and initially decreases sharply as frequency increases.
- It then levels off to a more gradual decline as it approaches \( 1/\tau \).
- Beyond \( 1/\tau \), the curve displays a slight increase and then stabilizes, indicating a minor peak before leveling off.

3. **Key Features and Technical Details:**
- The initial value of the noise spectral density is marked as \( 2qI_D \), where \( q \) is the charge of an electron and \( I_D \) is the diode current.
- The curve shows a marked decrease in spectral density as the frequency approaches \( 1/\tau \), indicative of the transit time effect on the noise characteristics.
- The plot illustrates the frequency-dependent behavior of shot noise, which is significant for frequencies comparable to the inverse of the transit time.

4. **Annotations and Specific Data Points:**
- The graph includes horizontal dashed lines indicating the initial spectral density level of \( 2qI_D \).
- The frequency markers at \( 0.5/\tau \), \( 1/\tau \), and \( 1.5/\tau \) provide reference points for analyzing the behavior of the spectral density across different frequency ranges.

Figure 11.3 Spectral density of shot noise in a diode with transit time $\tau$ (not to scale).
small and (11.2) is accurate well into the gigahertz region. A sketch of noise-current spectral density versus frequency for a diode is shown in Fig. 11.3 assuming that the passage of each charge carrier across the depletion region produces a square pulse of current with width $\tau$.

#### EXAMPLE

Calculate the shot noise in a diode current of 1 mA in a bandwidth of 1 MHz . Using (11.2) we have

$$
\overline{i^{2}}=2 \times 1.6 \times 10^{-19} \times 10^{-3} \times 10^{6} \mathrm{~A}^{2}=3.2 \times 10^{-16} \mathrm{~A}^{2}
$$

and thus

$$
i=1.8 \times 10^{-8} \mathrm{~A} \mathrm{rms}
$$

- where $i$ represents the root-mean-square (rms) value of the noise current.

The effect of shot noise can be represented in the low-frequency, small-signal equivalent circuit of the diode by inclusion of a current generator shunting the diode, as shown in Fig. 11.4. Since this noise signal has random phase and is defined solely in terms of its meansquare value, it also has no polarity. Thus the arrow in the current source in Fig. 11.2 has no significance and is included only to identify the generator as a current source. This practice is followed in this chapter where we deal only with noise generators having random phase.

The noise-current signal produced by the shot noise mechanism has an amplitude that varies randomly with time and that can only be specified by a probability-density function. It can be shown that the amplitude distribution of shot noise is Gaussian and the probabilitydensity function $p(I)$ of the diode current is plotted versus current in Fig. 11.5 (not to scale). The probability that the diode current lies between values $I$ and $(I+d I)$ at any time is given by $p(I) d I$. If $\sigma$ is the standard deviation of the Gaussian distribution, then the diode current
image_name:Figure 11.4 Junction diode small-signal equivalent circuit with noise
description:
[
name: D1, type: Diode, ports: {Na: S1, Nc: S2}
name: rd, type: Resistor, value: kT/qID, ports: {N1: S2, N2: S1}
name: i^2, type: CurrentSource, value: 2qIDΔf, ports: {Np: S2, Nn: S1}
]
extrainfo:The circuit represents a small-signal equivalent model of a junction diode with noise, including shot noise as a current source.

Figure 11.4 Junction diode small-signal equivalent circuit with noise.
image_name:Figure 11.5
description:The graph in Figure 11.5 is a probability density function (PDF) for the diode current, denoted as \( I \). It is a bell-shaped curve, which is typical of a normal distribution, centered around the mean diode current \( I_D \).

1. **Type of Graph and Function:**
- This is a probability density function graph representing the distribution of diode current values.

2. **Axes Labels and Units:**
- The horizontal axis represents the diode current \( I \), though specific units are not given, it typically would be in amperes.
- The vertical axis represents the probability density function \( p(I) \), which is unitless.

3. **Overall Behavior and Trends:**
- The graph shows a symmetric distribution centered at \( I_D \), indicating that \( I_D \) is the most probable current value.
- The amplitude of the distribution decreases as the current moves away from \( I_D \), indicating that values further from \( I_D \) are less probable.

4. **Key Features and Technical Details:**
- The peak of the curve is at \( I_D \), which is the mean of the distribution.
- The spread of the curve suggests the variance \( \sigma^2 \) of the distribution, where the amplitude lies between the limits \( I_D \pm \sigma \) for 68 percent of the time, consistent with a normal distribution.

5. **Annotations and Specific Data Points:**
- There is a dashed vertical line at \( I_D \) marking the mean current value.
- The graph does not provide specific numerical values but illustrates the concept of noise in diode current as a probability distribution.

Figure 11.5 Probability density function for the diode current $I$ (not to scale).
amplitude lies between limits $I_{D} \pm \sigma$ for 68 percent of the time. By definition, variance $\sigma^{2}$ is the mean-square value of $\left(I-I_{D}\right)$ and thus, from (11.1),

$$
\sigma^{2}=\overline{i^{2}}
$$

and

$$
\begin{equation*}
\sigma=\sqrt{2 q I_{D} \Delta f} \tag{11.3}
\end{equation*}
$$

using (11.2). Note that, theoretically, the noise amplitude can have positive or negative values approaching infinity. However, the probability falls off very quickly as amplitude increases and an effective limit to the noise amplitude is $\pm 3 \sigma$. The noise signal is within these limits for 99.7 percent of the time. A brief description of the Gaussian distribution is given in Appendix A.3.1 in Chapter 3.

It is important to note that the distribution of noise in frequency as shown in Fig. 11.3 is due to the random nature of the hole and electron transitions across the $p n$ junction. Consider the situation if all the carriers made transitions with uniform time separation. Since each carrier has a charge of $1.6 \times 10^{-19} \mathrm{C}$, a 1-mA current would then consist of current pulses every $1.6 \times 10^{-16} \mathrm{~s}$. The Fourier analysis of such a waveform would give the spectrum of Fig. 11.6, which shows an average or dc value $I_{D}$ and harmonics at multiples of $1 / \Delta t$, where $\Delta t$ is the period of the waveform and equals $1.6 \times 10^{-16} \mathrm{~s}$. Thus the first harmonic is at $6 \times 10^{6} \mathrm{GHz}$, which is far beyond the useful frequency of the device. There would be no noise produced in the normal frequency range of operation.
image_name:Figure 11.6 Shot-noise spectrum assuming uniform emission of carriers.
description:The graph in Figure 11.6 is a spectrum plot representing the shot-noise spectrum assuming uniform emission of carriers. It is a frequency-domain plot, where the x-axis is labeled as 'f' and represents frequency in gigahertz (GHz) on a linear scale. The y-axis is labeled as 'Amplitude of Fourier component' and represents the amplitude of the Fourier components.

The graph shows discrete spikes at specific frequencies, indicating the presence of harmonics. The first spike is at 6 x 10^6 GHz, which corresponds to the first harmonic, and there is another spike at 12 x 10^6 GHz, representing the second harmonic. These spikes suggest that the waveform has significant frequency components at these harmonics.

Additionally, there is a dc component labeled as I_D, which is the average value of the waveform, showing a constant amplitude at zero frequency.

The overall behavior of the graph indicates that the primary frequency components are far beyond the useful frequency range for typical device operation, as mentioned in the context. There are no significant components in the normal frequency range, implying minimal noise production within that range.

Figure 11.6 Shot-noise spectrum assuming uniform emission of carriers.
image_name:(a)
description:
[
name: R, type: Resistor, value: R, ports: {N1: V1, N2: X}
name: v^2, type: VoltageSource, value: v^2, ports: {Np: X, Nn: V2}
]
extrainfo:The circuit diagram (a) consists of a resistor R and a voltage source v^2 connected in series between nodes V1 and V2.
image_name:(b)
description:
[
name: R, type: Resistor, value: R, ports: {N1: V1, N2: V2}
name: i^2, type: CurrentSource, value: i^2, ports: {Np: V1, Nn: V2}
]
extrainfo:The circuit diagram (b) consists of a resistor R and a current source i^2 connected in parallel between nodes V5 and V3.

Figure 11.7 Alternative representations of thermal noise.

### 11.2.2 Thermal Noise ${ }^{\mathbf{1 , 3 , 5}}$

Thermal noise is generated by a completely different mechanism from shot noise. In conventional resistors it is due to the random thermal motion of the electrons and is unaffected by the presence or absence of direct current, since typical electron drift velocities in a conductor are much less than electron thermal velocities. Since this source of noise is due to the thermal motion of electrons, we expect that it is related to absolute temperature $T$. In fact thermal noise is directly proportional to $T$ (unlike shot noise, which is independent of $T$ ) and, as $T$ approaches zero, thermal noise also approaches zero.

In a resistor $R$, thermal noise can be shown to be represented by a series voltage generator $\overline{v^{2}}$ as shown in Fig. 11.7a, or by a shunt current generator $\overline{i^{2}}$ as in Fig. 11.7b. These representations are equivalent and

$$
\begin{align*}
& \overline{v^{2}}=4 k T R \Delta f  \tag{11.4}\\
& \overline{i^{2}}=4 k T \frac{1}{R} \Delta f \tag{11.5}
\end{align*}
$$

where $k$ is Boltzmann's constant. At room temperature $4 k T=1.66 \times 10^{-20} \mathrm{~V}$-C. Equations 11.4 and 11.5 show that the noise spectral density is again independent of frequency and, for thermal noise, this is true up to $10^{13} \mathrm{~Hz}$. Thus thermal noise is another source of white noise. Note that the Norton equivalent of (11.5) can be derived from (11.4) as

$$
\begin{equation*}
\overline{i^{2}}=\frac{\overline{v^{2}}}{R^{2}} \tag{11.6}
\end{equation*}
$$

A useful number to remember for thermal noise is that at room temperature $\left(300^{\circ} \mathrm{K}\right)$, the thermal noise spectral density in a $1-\mathrm{k} \Omega$ resistor is $\overline{v^{2}} / \Delta f \simeq 16 \times 10^{-18} \mathrm{~V}^{2} / \mathrm{Hz}$. This can be written in rms form as $v \simeq 4 \mathrm{nV} / \sqrt{\mathrm{Hz}}$ where the form $\mathrm{nV} / \sqrt{\mathrm{Hz}}$ is used to emphasize that the rms noise voltage varies as the square root of the bandwidth. Another useful equivalence is that the thermal noise-current generator of a $1-\mathrm{k} \Omega$ resistor at room temperature is the same as that of $50 \mu \mathrm{~A}$ of direct current exhibiting shot noise.

Thermal noise as described above is a fundamental physical phenomenon and is present in any linear passive resistor. This includes conventional resistors and the radiation resistance of antennas, loudspeakers, and microphones. In the case of loudspeakers and microphones, the source of noise is the thermal motion of the air molecules. In the case of antennas, the source of noise is the black-body radiation of the object at which the antenna is directed. In all cases, (11.4) and (11.5) give the mean-square value of the noise.

The amplitude distribution of thermal noise is again Gaussian. Since both shot and thermal noise each have a flat frequency spectrum and a Gaussian amplitude distribution, they are indistinguishable once they are introduced into a circuit. The waveform of shot and thermal noise combined with a sinewave of equal power is shown in Fig. 11.21.

### 11.2.3 Flicker Noise ${ }^{6,7,8}$ (1/f Noise)

This is a type of noise found in all active devices, as well as in some discrete passive elements such as carbon resistors. The origins of flicker noise are varied, but it is caused mainly by traps associated with contamination and crystal defects. These traps capture and release carriers in a random fashion and the time constants associated with the process give rise to a noise signal with energy concentrated at low frequencies.

Flicker noise, which is always associated with a flow of direct current, displays a spectral density of the form

$$
\begin{equation*}
\overline{i^{2}}=K_{1} \frac{I^{a}}{f^{b}} \Delta f \tag{11.7}
\end{equation*}
$$

where

```
$\Delta f=$ small bandwidth at frequency $f$
$I=$ direct current
$K_{1}=$ constant for a particular device
$a=$ constant in the range 0.5 to 2
$b=$ constant of about unity
```

If $b=1$ in (11.7), the noise spectral density has a $1 / f$ frequency dependence (hence the alternative name $1 / f$ noise), as shown in Fig. 11.8. It is apparent that flicker noise is most significant at low frequencies, although in devices exhibiting high flicker noise levels, this noise source may dominate the device noise at frequencies well into the megahertz range.

It was noted above that flicker noise only exists in association with a direct current. Thus, in the case of carbon resistors, no flicker noise is present until a direct current is passed through the resistor (however, thermal noise always exists in the resistor and is unaffected by any direct current as long as the temperature remains constant). Consequently, carbon resistors can be used if required as external elements in low-noise, low-frequency integrated circuits as long as they carry no direct current. If the external resistors for such circuits must carry direct current, however, metal film resistors that have no flicker noise should be used.

In earlier sections of this chapter, we saw that shot and thermal noise signals have welldefined mean-square values that can be expressed in terms of current flow, resistance, and a
image_name:Figure 11.8 Flicker noise spectral density versus frequency
description:The graph labeled "Figure 11.8 Flicker noise spectral density versus frequency" is a log-log plot illustrating the relationship between flicker noise spectral density and frequency.

1. **Type of Graph and Function:**
- This is a log-log plot, commonly used to display power-law relationships such as flicker noise, which is inversely proportional to frequency.

2. **Axes Labels and Units:**
- The x-axis represents frequency \( f \) and is on a logarithmic scale.
- The y-axis represents the flicker noise spectral density \( \frac{\bar{i}^2}{\Delta f} \) and is also on a logarithmic scale.

3. **Overall Behavior and Trends:**
- The graph shows a straight line with a negative slope, indicating an inverse relationship between noise spectral density and frequency. This aligns with the characteristic \( \frac{1}{f} \) behavior of flicker noise, where noise decreases as frequency increases.

4. **Key Features and Technical Details:**
- The line follows a \( \frac{1}{f} \) trend, which is typical for flicker noise. This suggests that the noise power decreases with increasing frequency.
- There are no specific markers or annotations indicating cutoff frequencies or other key points, as the focus is on the general trend.

5. **Annotations and Specific Data Points:**
- The graph is annotated with the \( \frac{1}{f} \) label, emphasizing the inverse frequency relationship.
- No specific numerical values or markers are provided on the graph, indicating that the emphasis is on the qualitative behavior rather than specific quantitative data.

Figure 11.8 Flicker noise spectral density versus frequency.
number of well-known physical constants. By contrast, the mean-square value of a flicker noise signal as given by (11.7) contains an unknown constant $K_{1}$. This constant not only varies by orders of magnitude from one device type to the next, but it can also vary widely for different transistors or integrated circuits from the same process wafer. This is due to the dependence of flicker noise on contamination and crystal imperfections, which are factors that can vary randomly even on the same silicon wafer. However, experiments have shown that if a typical value of $K_{1}$ is determined from measurements on a number of devices from a given process, then this value can be used to predict average or typical flicker noise performance for integrated circuits from that process. ${ }^{9}$

The final characteristic of flicker noise that is of interest is its amplitude distribution, which is often non-Gaussian, as measurements have shown.

### 11.2.4 Burst Noise ${ }^{7}$ (Popcorn Noise)

This is another type of low-frequency noise found in some integrated circuits and discrete transistors. The source of this noise is not fully understood, although it has been shown to be related to the presence of heavy-metal ion contamination. Gold-doped devices show very high levels of burst noise.

Burst noise is so named because an oscilloscope trace of this type of noise shows bursts of noise on a number (two or more) of discrete levels, as illustrated in Fig. 11.9a. The repetition rate of the noise pulses is usually in the audio frequency range (a few kilohertz or less) and produces a popping sound when played through a loudspeaker. This has led to the name popcorn noise for this phenomenon.
image_name:(a)
description:The graph labeled (a) is a time-domain waveform depicting burst noise, also known as popcorn noise. The x-axis represents time (t), although no specific units are provided, while the y-axis represents noise amplitude, also without specific units. The graph is linear in scale for both axes.

The waveform exhibits distinct bursts of noise at discrete levels, which appear as rectangular pulses of varying duration. These pulses fluctuate between positive and negative amplitudes, creating a pattern that resembles a square wave with added noise. The noise amplitude remains relatively consistent within each burst, but the transitions between levels are characterized by abrupt changes, highlighting the burst nature of the noise.

The overall behavior of the graph shows periodic bursts of noise, which are typical of burst noise phenomena. The repetition rate of these noise pulses is likely within the audio frequency range, leading to the characteristic popping sound when played through a speaker. There are no specific annotations or numerical values provided on the graph, but the key feature is the distinct, discrete levels of noise amplitude and the abrupt transitions between them.
image_name:(b)
description:The graph in figure 11.9 (b) is a plot of burst noise spectral density versus frequency. It is presented on a logarithmic scale for both axes. The x-axis represents frequency \( f \) in hertz, while the y-axis represents the spectral density \( \overline{i^2} / \Delta f \) also on a logarithmic scale.

**Overall Behavior and Trends:**
The graph shows a characteristic low-pass filter behavior. At lower frequencies, the spectral density remains relatively constant, indicating that the noise power is independent of frequency. As the frequency increases, the spectral density starts to decrease, following a slope that approximates \( 1/f^2 \). This behavior suggests that the noise power diminishes at higher frequencies.

**Key Features and Technical Details:**
- The graph has a distinct cutoff frequency, labeled as \( f_c \), where the transition from a flat response to a declining response begins. This cutoff frequency is a critical point where the noise spectral density starts to roll off.
- Beyond the cutoff frequency \( f_c \), the spectral density decreases sharply, following a \( 1/f^2 \) slope, which is typical for burst noise exhibiting a Lorentzian spectrum.
- The graph is marked with a dashed line indicating the asymptotic behavior of the spectral density as it follows the \( 1/f^2 \) trend.

**Annotations and Specific Data Points:**
- The cutoff frequency \( f_c \) is explicitly marked on the graph.
- There are no specific numerical values provided for the cutoff frequency or the levels of spectral density, but the graph clearly illustrates the general trend and behavior of burst noise in relation to frequency.

Figure 11.9 (a) Typical burst noise waveform. (b) Burst noise spectral density versus frequency.
image_name:Figure 11.9 (b)
description:**Type of Graph and Function:**
The graph is a log-log plot illustrating the spectral density of burst noise as a function of frequency. It is a representation of how the noise power varies with frequency, specifically showing the behavior of burst noise in electronic devices.

**Axes Labels and Units:**
- The horizontal axis represents frequency \( f \) on a logarithmic scale.
- The vertical axis represents the normalized spectral density \( \overline{i^2} / \Delta f \) also on a logarithmic scale.

**Overall Behavior and Trends:**
The graph shows a general trend where the spectral density decreases with increasing frequency. Initially, the curve decreases steeply, representing a high level of spectral density at lower frequencies. As the frequency increases, the curve exhibits a series of humps, labeled as "Burst noise humps," indicating regions where the spectral density temporarily increases before continuing its downward trend. Beyond these humps, the curve asymptotically approaches a \( 1/f^2 \) behavior, indicating a significant reduction in spectral density at high frequencies.

**Key Features and Technical Details:**
- The curve starts at a high value on the vertical axis, indicating a high spectral density at low frequencies.
- The "Burst noise humps" suggest regions of increased noise activity, possibly due to specific burst noise events.
- The asymptotic behavior of the curve at high frequencies follows the \( 1/f^2 \) trend, which is characteristic of certain types of noise, such as flicker noise.

**Annotations and Specific Data Points:**
- The graph includes annotations indicating the presence of "Burst noise humps."
- There is a note of the asymptotic \( \propto 1/f^2 \) behavior at the right end of the graph, emphasizing the decrease in spectral density with increasing frequency.

Figure 11.10 Spectral density of combined multiple burst noise sources and flicker noise.

The spectral density of burst noise can be shown to be of the form

$$
\begin{equation*}
\overline{i^{2}}=K_{2} \frac{I^{c}}{1+\left(\frac{f}{f_{c}}\right)^{2}} \Delta f \tag{11.8}
\end{equation*}
$$

where
$K_{2}=$ constant for a particular device
$I=$ direct current
$c=$ constant in the range 0.5 to 2
$f_{c}=$ particular frequency for a given noise process
This spectrum is plotted in Fig. $11.9 b$ and illustrates the typical hump that is characteristic of burst noise. At higher frequencies the noise spectrum falls as $1 / f^{2}$.

Burst noise processes often occur with multiple time constants, and this gives rise to multiple humps in the spectrum. Also, flicker noise is invariably present as well so that the composite low-frequency noise spectrum often appears as in Fig. 11.10. As with flicker noise, factor $K_{2}$ for burst noise varies considerably and must be determined experimentally. The amplitude distribution of the noise is also non-Gaussian.

### 11.2.5 Avalanche Noise ${ }^{10}$

This is a form of noise produced by Zener or avalanche breakdown in a pn junction. In avalanche breakdown, holes and electrons in the depletion region of a reverse-biased pn junction acquire sufficient energy to create hole-electron pairs by colliding with silicon atoms. This process is cumulative, resulting in the production of a random series of large noise spikes. The noise is always associated with a direct-current flow, and the noise produced is much greater than shot noise in the same current, as given by (11.2). This is because a single carrier can start an avalanching process that results in the production of a current burst containing many carriers moving together. The total noise is the sum of a number of random bursts of this type.

The most common situation where avalanche noise is a problem occurs when Zener diodes are used in the circuit. These devices display avalanche noise and are generally avoided in low-noise circuits. If Zener diodes are present, the noise representation of Fig. 11.11 can be used, where the noise is represented by a series voltage generator $v^{2}$. The dc voltage $V_{z}$ is the breakdown voltage of the diode, and the series resistance $R$ is typically 10 to $100 \Omega$. The
image_name:Figure 11.11
description:The circuit represents an equivalent model of a Zener diode including noise. The Zener diode is connected between nodes S2 and S1. A series resistor R and voltage sources V1, V2, and V3 are included, representing the breakdown voltage and noise.

magnitude of $\overline{v^{2}}$ is difficult to predict as it depends on the device structure and the uniformity of the silicon crystal, but a typical measured value is $\overline{v^{2}} / \Delta f \simeq 10^{-14} \mathrm{~V}^{2} / \mathrm{Hz}$ at a dc Zener current of 0.5 mA . Note that this is equivalent to the thermal noise voltage in a $600-\mathrm{k} \Omega$ resistor and completely overwhelms thermal noise in $R$. The spectral density of the noise is approximately flat, but the amplitude distribution is generally non-Gaussian.

## 11.3 Noise Models of Integrated-Circuit Components

In the above sections, the various physical sources of noise in electronic circuits were described. In this section, these sources of noise are brought together to form the small-signal equivalent circuits including noise for diodes and for bipolar and MOS transistors.

### 11.3.1 Junction Diode

The equivalent circuit for a forward-biased junction diode was considered briefly in the consideration of shot noise. The basic equivalent circuit of Fig. 11.4 can be made complete by adding series resistance $r_{s}$ as shown in Fig. 11.12. Since $r_{s}$ is a physical resistor due to the resistivity of the silicon, it exhibits thermal noise. Experimentally it has been found that any flicker noise present can be represented by a current generator in shunt with $r_{d}$, and can be
image_name:Figure 11.12 Complete diode small-signal equivalent circuit with noise sources
description:The circuit is a small-signal equivalent model of a forward-biased junction diode including noise sources. It consists of a diode, series resistance, and noise sources represented by a voltage source and a current source. The series resistance models the thermal noise, while the current source models the shot noise and flicker noise.

Figure 11.12 Complete diode small-signal equivalent circuit with noise sources.
conveniently combined with the shot-noise generator as indicated by (11.10) to give

$$
\begin{align*}
& \overline{v_{s}^{2}}=4 k T r_{s} \Delta f  \tag{11.9}\\
& \overline{i^{2}}=2 q I_{D} \Delta f+K \frac{I_{D}^{a}}{f} \Delta f \tag{11.10}
\end{align*}
$$

### 11.3.2 Bipolar Transistor ${ }^{11}$

In a bipolar transistor in the forward-active region, minority carriers diffuse and drift across the base region to be collected at the collector-base junction. Minority carriers entering the collector-base depletion region are accelerated by the field existing there and swept across this region to the collector. The time of arrival at the collector-base junction of the diffusing (or drifting) carriers can be modeled as a random process, and thus the transistor collector current consists of a series of random current pulses. Consequently, collector current $I_{C}$ shows full shot noise as given by (11.2), and this is represented by a shot noise current generator $\bar{i}_{c}^{2}$ from collector to emitter as shown in the equivalent circuit of Fig. 11.13.

Base current $I_{B}$ in a transistor is due to recombination in the base and base-emitter depletion regions and also to carrier injection from the base into the emitter. All of these are independent random processes, and thus $I_{B}$ also shows full shot noise. This is represented by shot noise current generator $\overline{i_{b}^{2}}$ in Fig. 11.13.

Transistor base resistor $r_{b}$ is a physical resistor and thus has thermal noise. Collector series resistor $r_{c}$ also shows thermal noise, but since this is in series with the high-impedance collector node, this noise is negligible and is usually not included in the model. Note that resistors $r_{\pi}$ and $r_{o}$ in the model are fictitious resistors that are used for modeling purposes only, and they do not exhibit thermal noise.

Flicker noise and burst noise in a bipolar transistor have been found experimentally to be represented by current generators across the internal base-emitter junction. These are conveniently combined with the shot noise generator in $\overline{i_{b}^{2}}$. Avalanche noise in bipolar transistors is found to be negligible if $V_{C E}$ is kept at least 5 V below the breakdown voltage $B V_{C E O}$, and this source of noise will be neglected in subsequent calculations.

The full small-signal equivalent circuit including noise for the bipolar transistor is shown in Fig. 11.13. Since they arise from separate, independent physical mechanisms, all the noise sources are independent of each other and have mean-square values:

$$
\begin{align*}
& \overline{v_{b}^{2}}=4 k T r_{b} \Delta f  \tag{11.11}\\
& \overline{i_{c}^{2}}=2 q I_{C} \Delta f \tag{11.12}
\end{align*}
$$

$$
\begin{equation*}
\overline{i_{b}^{2}}=\underbrace{2 q I_{B} \Delta f}_{\text {Shot noise }}+\underbrace{K_{1} \frac{I_{B}^{a}}{f} \Delta f}_{\text {Flicker noise }}+K_{2} \frac{I_{B}^{c}}{\underbrace{1+\left(\frac{f}{f_{c}}\right)^{2}}_{\text {Burst noise }}} \Delta f \tag{11.13}
\end{equation*}
$$

image_name:Figure 11.13
description:
[
name: rb, type: Resistor, value: rb, ports: {N1: B, N2: "X1"}
name: v^2_b, type: VoltageSource, value: v^2_b, ports: {Np: "B", Nn: X1}
name: i^2_b, type: CurrentSource, value: i^2_b, ports: {Np: B, Nn: E}
name: rπ, type: Resistor, value: rπ, ports: {N1: "B", N2: E}
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: "B", Nn: E}
name: g_mv1, type: VoltageControlledCurrentSource, value: g_mv1, ports: {Np: E, Nn: "C"}
name: Cμ, type: Capacitor, value: Cμ, ports: {Np: "B", Nn: "C"}
name: ro, type: Resistor, value: ro, ports: {N1: "C", N2: E}
name: i^2_c, type: CurrentSource, value: i^2_c, ports: {Np: "C", Nn: E}
name: Ccs, type: Capacitor, value: Ccs, ports: {Np: "C", Nn: GND}
name: rc, type: Resistor, value: rc, ports: {N1: "C", N2: C'}
]
extrainfo:This is a small-signal equivalent circuit of a bipolar transistor with noise sources. It includes resistors, capacitors, voltage and current sources, and a voltage-controlled current source. The circuit models various noise components such as base and collector current noise.

image_name:Figure 11.14
description:The graph in Figure 11.14 is a log-log plot representing the spectral density of the base-current noise generator in a bipolar transistor. The x-axis represents frequency \( f \) in a logarithmic scale, while the y-axis represents the noise current spectral density \( \frac{\bar{i}_b^2}{\Delta f} \) also in a logarithmic scale.

Overall Behavior and Trends:
- The graph displays two main regions: a high-frequency region where the spectral density is constant and a low-frequency region where the spectral density decreases with increasing frequency.
- At lower frequencies, the plot follows a \( \frac{1}{f} \) trend, indicating flicker noise, also known as 1/f noise. This is represented by the line \( K_1 \frac{I_B^a}{f} \).
- At higher frequencies, the spectral density becomes constant, indicating shot noise, and is represented by the line \( 2qI_B \).
- The two regions meet at a frequency \( f_a \), which is marked on the graph.

Key Features and Technical Details:
- The flicker noise region has a negative slope due to its inverse relationship with frequency.
- The shot noise region is horizontal, indicating a constant spectral density.
- The intersection point at \( f_a \) is a critical frequency where the transition from flicker noise to shot noise occurs.

Annotations and Specific Data Points:
- The graph includes annotations such as \( K_1 \frac{I_B^a}{f} \) and \( 2qI_B \), which denote the mathematical expressions for flicker noise and shot noise, respectively.
- The frequency \( f_a \) is specifically marked with a vertical dashed line, illustrating the transition point between the two noise behaviors.

Figure 11.14 Spectral density of the base-current noise generator in a bipolar transistor.

This equivalent circuit is valid for both $n p n$ and $p n p$ transistors. For $p n p$ devices, the magnitudes of $I_{B}$ and $I_{C}$ are used in the above equations.

The base-current noise spectrum can be plotted using (11.13), and this has been done in Fig. 11.14, where burst noise has been neglected for simplicity. The shot noise and flicker noise asymptotes meet at a frequency $f_{a}$, which is called the flicker noise corner frequency. In some transistors using careful processing, $f_{a}$ can be as low as 100 Hz . In other transistors, $f_{a}$ can be as high as 10 MHz .

### 11.3.3 MOS Transistor ${ }^{12}$

The structure of MOS transistors was described in Chapter 1. We showed there that the resistive channel under the gate is modulated by the gate-source voltage so that the drain current is controlled by the gate-source voltage. Since the channel material is resistive, it exhibits thermal noise, which is a major source of noise in MOS transistors. This noise source can be represented by a noise-current generator $\overline{i_{d}^{2}}$ from drain to source in the small-signal equivalent circuit of Fig. 11.15.

Another source of noise in MOS transistors is flicker noise. Because MOS transistors conduct current near the surface of the silicon where surface states act as traps that capture and release current carriers, their flicker noise component can be large. Flicker noise in the MOS transistor is also found experimentally to be represented by a drain-source current
image_name:Figure 11.15
description:
[
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: G, Nn: D}
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: G, Nn: S}
name: ig, type: CurrentSource, value: ig, ports: {Np: G, Nn: S}
name: gmvi, type: VoltageControlledCurrentSource, value: gmvi, ports: {Np: G, Nn: D}
name: ro, type: Resistor, value: ro, ports: {N1: D, N2: S}
name: id, type: CurrentSource, value: id, ports: {Np: D, Nn: S}
]
extrainfo:The circuit represents a small-signal equivalent model of a MOSFET with noise sources. It includes capacitive coupling between gate and drain (Cgd), gate and source (Cgs), and various noise sources represented by current generators.

Figure 11.15
MOSFET small-signal equivalent circuit with noise sources.
generator, and the flicker and thermal noise can be lumped into one noise generator $\overline{i_{d}^{2}}$ in Fig. 11.15 with

$$
\begin{equation*}
\overline{i_{d}^{2}}=\underbrace{4 k T\left(\frac{2}{3} g_{m}\right) \Delta f}_{\text {Thermal noise }}+\underbrace{K \frac{I_{D}^{a}}{f} \Delta f}_{\text {Flicker noise }} \tag{11.14}
\end{equation*}
$$

where
$I_{D}=$ drain bias current
$K=$ constant for a given device
$a=$ constant between 0.5 and 2
$g_{m}=$ device transconductance at the operating point
This equation is valid for long-channel devices. For channel lengths less than $1 \mu \mathrm{~m}$, thermal noise 2 to 5 times larger than given by the first term in (11.14) has been measured. ${ }^{13}$ This increase in thermal noise may be attributed to hot electrons in short-channel devices.

Another source of noise in the MOS transistor is shot noise generated by the gate leakage current. This noise can be represented by $\overline{i_{g}^{2}}$ in Fig. 11.15, with

$$
\begin{equation*}
\overline{i_{g}^{2}}=2 q I_{G} \Delta f \tag{11.15}
\end{equation*}
$$

This noise current is usually very small since the dc gate current $I_{G}$ is typically less than $10^{-15}$ A. The noise terms in (11.14) and (11.15) are all independent of each other.

There is one other component of noise that is usually insignificant at low frequencies but important in very high-frequency MOS circuits, such as radio-frequency amplifiers, for example. At an arbitrary point in the channel, the gate-to-channel voltage has a random component due to fluctuations along the channel caused by thermal noise. These voltage variations generate a noisy ac gate current $i_{g}$ due to the capacitance between the gate and channel. The mean-squared value of this gate current for a long-channel device in the active region is

$$
\begin{equation*}
\overline{i_{g}^{2}}=\frac{16}{15} k T \omega^{2} C_{g s}^{2} \Delta f \tag{11.16}
\end{equation*}
$$

where $C_{g s}=(2 / 3) C_{o x} W L$. The gate-current noise in (11.16) is correlated with the thermalnoise term in (11.14) because both noise currents stem from thermal fluctuations in the channel. The magnitude of the correlation between these currents is $0.39 .{ }^{12}$ For channel lengths less than $1 \mu \mathrm{~m}$, this component of gate-current noise may be larger than given by (11.16) if thermal noise associated with the channel increases due to hot electrons as noted above. ${ }^{14}$ The total gate-current noise is the sum of the terms in (11.15) and (11.16).

### 11.3.4 Resistors

Monolithic and thin-film resistors display thermal noise as given by (11.4) and (11.5), and the circuit representation of this is shown in Fig. 11.7. As mentioned in Section 11.2.3, discrete carbon resistors also display flicker noise, and this should be considered if such resistors are used as external components to the integrated circuit.

### 11.3.5 Capacitors and Inductors

Capacitors are common elements in integrated circuits, either as unwanted parasitics or as elements introduced for a specific purpose. Inductors are sometimes realized on the silicon die in integrated high-frequency communication circuits. There are no sources of noise in
ideal capacitors or inductors. In practice, real components have parasitic resistance that does display noise as given by the thermal noise formulas of (11.4) and (11.5). In the case of integrated-circuit capacitors, the parasitic resistance usually consists of a small value in series with the capacitor. Parasitic resistance in inductors can be modeled by either series or shunt elements.

## 11.4 Circuit Noise Calculations ${ }^{15,16}$

The device equivalent circuits including noise that were derived in Section 11.3 can be used for the calculation of circuit noise performance. First, however, methods of circuit calculation with noise generators as sources must be established, and attention is now given to this problem.

Consider a noise current source with mean-square value

$$
\begin{equation*}
\overline{i^{2}}=S(f) \Delta f \tag{11.17}
\end{equation*}
$$

where $S(f)$ is the noise spectral density. The value of $S(f)$ is plotted versus frequency in Fig. 11.16 $a$ for an arbitrary noise generator. In a small bandwidth $\Delta f$, the mean-square value of the noise current is given by (11.17), and the rms values can be written as

$$
\begin{equation*}
i=\sqrt{S(f) \Delta f} \tag{11.18}
\end{equation*}
$$

The noise current in bandwidth $\Delta f$ can be represented approximately ${ }^{15}$ by a sinusoidal current generator with rms value $i$ as shown in Fig. 11.16b. If the noise current in bandwidth $\Delta f$ is now applied as an input signal to a circuit, its effect can be calculated by substituting the sinusoidal generator and performing circuit analysis in the usual fashion. When the circuit response to the sinusoid is calculated, the mean-square value of the output sinusoid gives the mean-square value of the output noise in bandwidth $\Delta f$. Thus network noise calculations reduce to familiar sinusoidal circuit-analysis calculations. The only difference occurs when multiple noise sources are applied, as is usually the case in practical circuits. Each noise source is then represented by a separate sinusoidal generator, and the output contribution of each one is separately calculated. The total output noise in bandwidth $\Delta f$ is calculated as a mean-square value by adding the individual mean-square contributions from each output sinusoid. This
image_name:(a)
description:The graph labeled (a) is a representation of noise in a frequency domain. It is a plot of the noise spectral density, denoted as \( S(f) \), against frequency \( f \).

1. **Type of Graph and Function:**
- This is a frequency domain graph, likely a spectral density plot, depicting how noise power is distributed across frequencies.

2. **Axes Labels and Units:**
- The horizontal axis represents frequency \( f \), though the specific unit is not provided (commonly in Hertz).
- The vertical axis represents the spectral density \( S(f) \), which is often measured in units like V²/Hz or A²/Hz.

3. **Overall Behavior and Trends:**
- The graph shows a generally flat or slightly undulating line, indicating a relatively constant noise spectral density across the frequency range shown.
- There is a specific bandwidth \( \Delta f \) highlighted, suggesting a focus on this particular frequency range for analysis.

4. **Key Features and Technical Details:**
- The bandwidth \( \Delta f \) is marked with vertical dashed lines, indicating the range of frequencies being considered for the noise calculation.
- The graph suggests calculating the total noise power within this bandwidth.

5. **Annotations and Specific Data Points:**
- The lower part of the diagram (b) shows an amplitude representation, where the amplitude \( i \) is calculated as \( i = \sqrt{S(f) \Delta f} \), indicating the root mean square (rms) value of the noise over the specified bandwidth.
- This rms value is represented by a horizontal dashed line extending from the spectral density graph to the amplitude axis, showing the equivalent sinusoidal amplitude for the noise in the bandwidth \( \Delta f \).
image_name:(b)
description:The graph labeled (b) is a representation of noise in a bandwidth \( \Delta f \) by an equivalent sinusoid with the same RMS value.

1. **Type of Graph and Function:**
- The graph is a frequency-domain representation depicting the concept of noise power spectral density and its equivalent sinusoidal representation.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \( f \), representing frequency.
- The vertical axis is labeled "Amplitude," indicating the amplitude of the equivalent sinusoid.

3. **Overall Behavior and Trends:**
- The graph shows a vertical line indicating the amplitude of the equivalent sinusoid, which is derived from the noise power spectral density over the bandwidth \( \Delta f \).
- The amplitude is consistent across the small frequency band \( \Delta f \).

4. **Key Features and Technical Details:**
- The amplitude of the sinusoid is given by \( i = \sqrt{S(f) \Delta f} \), where \( S(f) \) is the power spectral density at frequency \( f \).
- This representation is used to equate the noise in a specified bandwidth to a sinusoidal signal with an equivalent RMS value.

5. **Annotations and Specific Data Points:**
- The graph includes a dashed line connecting the power spectral density plot (from part (a) above) to the amplitude axis of the sinusoid in part (b).
- The bandwidth \( \Delta f \) is marked with a horizontal double-arrow line, indicating the range of frequencies considered.

This graphical representation is used to simplify the analysis of noise by converting it into an equivalent sinusoidal form, which can be more easily handled in circuit analysis.

Figure 11.16 Representation of noise in a bandwidth $\Delta f$ by an equivalent sinusoid with the same rms value.
image_name:Figure 11.17
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: S4, N2: S3}
name: R2, type: Resistor, value: R2, ports: {N1: S2, N2: S1}
name: S1, type: VoltageSource, value: 1/2 V2, ports: {Np: S1, Nn: GND}
name: S2, type: Resistor, value: R2, ports: {N1: S2, N2: S3}
name: S3, type: VoltageSource, value: 1/2 V1, ports: {Np: S3, Nn: S2}
name: S4, type: Switch, ports: {N1: S4, N2: S3}
]
extrainfo:The circuit represents the calculation of total noise voltage produced by two resistors in series, with independent noise sources modeled as voltage sources.

Figure 11.17Circuit for the calculation of the total noise $\overline{v_{T}^{2}}$ produced by two resistors in series.
depends, however, on the original noise sources being independent, as will be shown below. This requirement is usually satisfied if the equivalent noise circuits derived in previous sections are used, as all the noise sources except the induced gate noise in (11.16) arise from separate mechanisms and are thus independent.

For example, consider two resistors $R_{1}$ and $R_{2}$ connected in series as shown in Fig. 11.17. Resistors $R_{1}$ and $R_{2}$ have respective noise generators

$$
\begin{align*}
& \overline{v_{1}^{2}}=4 k T R_{1} \Delta f  \tag{11.19a}\\
& \overline{v_{2}^{2}}=4 k T R_{2} \Delta f \tag{11.19b}
\end{align*}
$$

In order to calculate the mean-square noise voltage $\overline{v_{T}^{2}}$ produced by the two resistors in series, let $v_{T}(t)$ be the instantaneous value of the total noise voltage and $v_{1}(t)$ and $v_{2}(t)$ the instantaneous values of the individual generators. Then

$$
\begin{equation*}
v_{T}(t)=v_{1}(t)+v_{2}(t) \tag{11.20}
\end{equation*}
$$

and thus

$$
\begin{align*}
\overline{v_{T}(t)^{2}} & =\overline{\left[v_{1}(t)+v_{2}(t)\right]^{2}} \\
& =\overline{v_{1}(t)^{2}}+\overline{v_{2}(t)^{2}}+\overline{2 v_{1}(t) v_{2}(t)} \tag{11.21}
\end{align*}
$$

Now, since noise generators $v_{1}(t)$ and $v_{2}(t)$ arise from separate resistors, they must be independent. Thus the average value of their product $\overline{v_{1}(t) v_{2}(t)}$ will be zero and (11.21) becomes

$$
\begin{equation*}
\overline{v_{T}^{2}}=\overline{v_{1}^{2}}+\overline{v_{2}^{2}} \tag{11.22}
\end{equation*}
$$

Thus the mean-square value of the sum of a number of independent noise generators is the sum of the individual mean-square values. Substituting (11.19a) and (11.19b) in (11.22) gives

$$
\begin{equation*}
\overline{v_{T}^{2}}=4 k T\left(R_{1}+R_{2}\right) \Delta f \tag{11.23}
\end{equation*}
$$

Equation 11.23 is just the value that would be predicted for thermal noise in a resistor $\left(R_{1}+R_{2}\right)$ using (11.4), and thus the results are consistent. These results are also consistent with the representation of the noise generators by independent sinusoids as described earlier. It is easily shown that when two or more such generators are connected in series, the mean-square value of the total voltage is equal to the sum of the individual mean-square values.

In the above calculation, two noise voltage sources were considered connected in series. It can be similarly shown that an analogous result is true for independent noise current sources connected in parallel. The mean-square value of the combination is the sum of the individual mean-square values. This result was assumed in the modeling of Section 11.3 where, for example, three independent noise-current generators (shot, flicker, and burst) were combined into a single base-emitter noise source for a bipolar transistor.

### 11.4.1 Bipolar Transistor Noise Performance

As an example of the manipulation of noise generators in circuit calculations, consider the noise performance of the simple transistor stage with the ac schematic shown in Fig. 11.18a. The small-signal equivalent circuit including noise is shown in Fig. 11.18b. (It should be pointed out that, for noise calculations, the equivalent circuit analyzed must be the actual circuit configuration used. That is, Fig. $11.18 a$ cannot be used as a half-circuit representation of a differential pair for the purposes of noise calculation because noise sources in each half of a differential pair affect the total output noise.)

In the equivalent circuit of Fig. 11.18b, the external input signal $v_{i}$ has been ignored so that output signal $v_{o}$ is due to noise generators only. $C_{\mu}$ is assumed small and is neglected. Output resistance $r_{o}$ is also neglected. The transistor noise generators are as described previously and in addition

$$
\begin{align*}
& \overline{v_{s}^{2}}=4 k T R_{S} \Delta f  \tag{11.24}\\
& \overline{i_{l}^{2}}=4 k T \frac{1}{R_{L}} \Delta f \tag{11.25}
\end{align*}
$$

The total output noise can be calculated by considering each noise source in turn and performing the calculation as if each noise source were a sinusoid with rms value equal to that of the noise source being considered. Consider first the noise generator $v_{s}$ due to $R_{S}$. Then

$$
\begin{equation*}
v_{1}=\frac{Z}{Z+r_{b}+R_{S}} v_{s} \tag{11.26}
\end{equation*}
$$

image_name:(a)
description:
[
name: vi, type: VoltageSource, value: vi, ports: {Np: Vi, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vi, N2: b0}
name: B0, type: NPN, ports: {C: Vo, B: b0, E: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a simple transistor amplifier with a voltage source vi connected through a resistor RS to the base of an NPN transistor B0. The collector of B0 is connected to the output node Vo, and the emitter is grounded. A load resistor RL is connected between Vo and ground.
image_name:(b)
description:The circuit is a small-signal equivalent model of a transistor amplifier with noise sources. It includes a voltage source Vi, resistors RS, rπ, and RL, a capacitor Cπ, a voltage-controlled current source gmV1, and current sources ib, ic, and il. The transistor B0 is modeled as an NPN with connections to nodes bo, Vo, and GND.

(b)

Figure 11.18 (a) Simple transistor amplifier ac schematic. (b) Small-signal equivalent circuit with noise sources.
where

$$
\begin{equation*}
Z=r_{\pi} \| \frac{1}{j \omega C_{\pi}} \tag{11.27}
\end{equation*}
$$

The output noise voltage due to $v_{s}$ is

$$
\begin{equation*}
v_{o 1}=-g_{m} R_{L} v_{1} \tag{11.28}
\end{equation*}
$$

Use of (11.26) in (11.28) gives

$$
\begin{equation*}
v_{o 1}=-g_{m} R_{L} \frac{Z}{Z+r_{b}+R_{S}} v_{s} \tag{11.29}
\end{equation*}
$$

The phase information contained in (11.29) is irrelevant because the noise signal has random phase and the only quantity of interest is the mean-square value of the output voltage produced by $v_{s}$. From (11.29) this is

$$
\begin{equation*}
\overline{v_{o 1}^{2}}=g_{m}^{2} R_{L}^{2} \frac{|Z|^{2}}{\left|Z+r_{b}+R_{S}\right|^{2}} \overline{v_{s}^{2}} \tag{11.30}
\end{equation*}
$$

By similar calculations it is readily shown that the noise voltage produced at the output by $\overline{v_{b}^{2}}$ and $\overline{i_{b}^{2}}$ is

$$
\begin{align*}
& \overline{v_{o 2}^{2}}=g_{m}^{2} R_{L}^{2} \frac{|Z|^{2}}{\left|Z+r_{b}+R_{S}\right|^{2}} \overline{v_{b}^{2}}  \tag{11.31}\\
& \overline{v_{o 3}^{2}}=g_{m}^{2} R_{L}^{2} \frac{\left(R_{S}+r_{b}\right)^{2}|Z|^{2}}{\left|Z+r_{b}+R_{S}\right|^{2}} i_{b}^{2} \tag{11.32}
\end{align*}
$$

Noise at the output due to $\overline{i_{l}^{2}}$ and $\overline{i_{c}^{2}}$ is

$$
\begin{align*}
& \overline{v_{o 4}^{2}}=\overline{i_{l}^{2}} R_{L}^{2}  \tag{11.33}\\
& \overline{v_{o 5}^{2}}=\overline{i_{c}^{2}} R_{L}^{2} \tag{11.34}
\end{align*}
$$

Since all five noise generators are independent, the total output noise is

$$
\begin{align*}
\overline{v_{o}^{2}}= & \sum_{n=1}^{5} \overline{v_{o n}^{2}}  \tag{11.35}\\
= & g_{m}^{2} R_{L}^{2} \frac{|Z|^{2}}{\left|Z+r_{b}+R_{S}\right|^{2}}\left[\overline{v_{s}^{2}}+\overline{v_{b}^{2}}+\left(R_{S}+r_{b}\right)^{2} \overline{i_{b}^{2}}\right]  \tag{11.36}\\
& \left.+R_{L}^{2} \overline{\left(\overline{i_{l}^{2}}\right.}+\overline{i_{c}^{2}}\right)
\end{align*}
$$

Substituting expressions for the noise generators we obtain

$$
\begin{align*}
\frac{\overline{v_{o}^{2}}}{\Delta f}= & g_{m}^{2} R_{L}^{2} \frac{|Z|^{2}}{\left|Z+r_{b}+R_{S}\right|^{2}}\left[4 k T\left(R_{S}+r_{b}\right)+\left(R_{S}+r_{b}\right)^{2} 2 q I_{B}\right] \\
& +R_{L}^{2}\left(4 k T \frac{1}{R_{L}}+2 q I_{C}\right) \tag{11.37}
\end{align*}
$$

image_name:Figure 11.19
description:The graph in Figure 11.19 is a plot of noise voltage spectral density, denoted as \( S_o(f) = \frac{\overline{v_o^2}}{\Delta f} \), versus frequency \( f \) in megahertz (MHz). The vertical axis represents the noise spectral density in units of \( \text{V}^2/\text{Hz} \), while the horizontal axis represents frequency in MHz.

The graph is plotted on a linear scale with marked gridlines for both axes. The vertical axis ranges from \( 5 \times 10^{-16} \) to \( 5 \times 10^{-15} \) \( \text{V}^2/\text{Hz} \), and the horizontal axis ranges from 0 to 250 MHz.

The overall behavior of the graph shows a decreasing trend in noise spectral density with increasing frequency. Starting at approximately \( 5 \times 10^{-15} \text{ V}^2/\text{Hz} \) at low frequencies, the spectral density decreases steadily. At a frequency of \( f_1 = 23.3 \) MHz, a notable point is marked where the curve begins to drop more sharply. The spectral density continues to decrease, reaching around \( 0.88 \times 10^{-15} \text{ V}^2/\text{Hz} \) at higher frequencies beyond 200 MHz.

Key features include the initial flat region at lower frequencies, the marked frequency \( f_1 \), and the subsequent decline in spectral density. The graph does not exhibit any oscillations or periodic behavior, indicating a simple low-pass filter-like characteristic where higher frequencies are attenuated more significantly.

Figure 11.19 Noise voltage spectrum at the output of the circuit of Fig. 11.18.
where flicker noise has been assumed small and neglected. Substituting for $Z$ from (11.27) in (11.37) we find

$$
\begin{align*}
\frac{\overline{v_{o}^{2}}}{\Delta f}= & g_{m}^{2} R_{L}^{2} \frac{r_{\pi}^{2}}{\left(r_{\pi}+R_{S}+r_{b}\right)^{2}} \frac{1}{1+\left(\frac{f}{f_{1}}\right)^{2}}\left[4 k T\left(R_{S}+r_{b}\right)+\left(R_{S}+r_{b}\right)^{2} 2 q I_{B}\right] \\
& +R_{L}^{2}\left(4 k T \frac{1}{R_{L}}+2 q I_{C}\right) \tag{11.38}
\end{align*}
$$

where

$$
\begin{equation*}
f_{1}=\frac{1}{2 \pi\left[r_{\pi} \|\left(R_{S}+r_{b}\right)\right] C_{\pi}} \tag{11.39}
\end{equation*}
$$

The output noise-voltage spectral density represented by (11.38) has a frequencydependent part and a constant part. The frequency dependence arises because the gain of the stage begins to fall above frequency $f_{1}$, and noise due to generators $\overline{v_{s}^{2}}, \overline{v_{b}^{2}}$, and $\overline{i_{b}^{2}}$, which appears amplified in the output, also begins to fall. The constant term in (11.38) is due to noise generators $\overline{i_{l}^{2}}$ and $\overline{i_{c}^{2}}$. Note that this noise contribution would also be frequency dependent if the effect of $C_{\mu}$ had not been neglected. The noise-voltage spectral density represented by (11.38) has the form shown in Fig. 11.19.

#### EXAMPLE

In order to give an appreciation of the numbers involved, specific values will now be assigned to the parameters of (11.38), and the various terms in the equation will be evaluated. Assume that

$$
\begin{array}{lrr}
I_{C}=100 \mu \mathrm{~A} & \beta=100 & r_{b}=200 \Omega \\
R_{S}=500 \Omega & C_{\pi}=10 \mathrm{pF} & \\
R_{L}=5 \mathrm{k} \Omega & &
\end{array}
$$

Substituting these values in (11.38) and using $4 k T=1.66 \times 10^{-20} \mathrm{~V}$-C gives

$$
\begin{align*}
\frac{\overline{v_{o}^{2}}}{\Delta f} & =\left[5.82 \times 10^{-18} \frac{1}{1+\left(\frac{f}{f_{1}}\right)^{2}}(700+9.4)+1.66 \times 10^{-20}(5000+48,080)\right] \mathrm{V}^{2} / \mathrm{Hz} \\
& =\left[\frac{4.13 \times 10^{-15}}{1+\left(\frac{f}{f_{1}}\right)^{2}}+0.88 \times 10^{-15}\right] \mathrm{V}^{2} / \mathrm{Hz} \tag{11.40}
\end{align*}
$$

Equation 11.39 gives

$$
\begin{equation*}
f_{1}=23.3 \mathrm{MHz} \tag{11.41}
\end{equation*}
$$

Equation 11.40 shows the output noise-voltage spectral density is $5.0 \times 10^{-15} \mathrm{~V}^{2} / \mathrm{Hz}$ at low frequencies, and it approaches $0.88 \times 10^{-15} \mathrm{~V}^{2} / \mathrm{Hz}$ at high frequencies. The major contributor to the output noise in this case is the source resistance $R_{S}$, followed by the base resistance of the transistor. The noise spectrum given by (11.40) is plotted in Fig. 11.19.

#### EXAMPLE

Suppose the amplifier in the above example is followed by later stages that limit the bandwidth to a sharp cutoff at 1 MHz . Since the noise spectrum as shown in Fig. 11.19 does not begin to fall significantly until $f_{1}=23.3 \mathrm{MHz}$, the noise spectrum may be assumed constant at $5.0 \times 10^{-15} \mathrm{~V}^{2} / \mathrm{Hz}$ over the bandwidth 0 to 1 MHz . Thus the total noise voltage at the output of the circuit of Fig. 11.18a in a 1-MHz bandwidth is

$$
\overline{v_{o T}^{2}}=5.0 \times 10^{-15} \times 10^{6} \mathrm{~V}^{2}=5.0 \times 10^{-9} \mathrm{~V}^{2}
$$

and thus

$$
\begin{equation*}
v_{o T}=71 \mu \mathrm{~V} \mathrm{rms} \tag{11.42}
\end{equation*}
$$

Now suppose that the amplifier of Fig. $11.18 a$ is not followed by later stages that limit the bandwidth but is fed directly to a wideband detector (this could be an oscilloscope or a voltmeter). In order to find the total output noise voltage in this case, the contribution from each frequency increment $\Delta f$ must be summed at the output. This reduces to integration across the bandwidth of the detector of the noise-voltage spectral-density curve of Fig. 11.19. For example, if the detector had a 0 to $50-\mathrm{MHz}$ bandwidth with a sharp cutoff, then the total output noise would be

$$
\begin{align*}
\overline{v_{o T}^{2}} & =\sum_{f=0}^{50 \times 10^{6}} S_{o}(f) \Delta f \\
& =\int_{0}^{50 \times 10^{6}} S_{o}(f) d f \tag{11.43}
\end{align*}
$$

where

$$
\begin{equation*}
S_{o}(f)=\frac{\overline{v_{o}^{2}}}{\Delta f} \tag{11.44}
\end{equation*}
$$

is the noise spectral density defined by (11.40). In practice, the exact evaluation of such integrals is often difficult and approximate methods are often used. Note that if the integration of (11.43) is done graphically, the noise spectral density versus frequency must be plotted on linear scales.

### 11.4.2 Equivalent Input Noise and the Minimum Detectable Signal

In the previous section, the output noise produced by the circuit of Fig. 11.18 was calculated. The significance of the noise performance of a circuit is, however, the limitation it places on the smallest input signals the circuit can handle before the noise degrades the quality of the output signal. For this reason, the noise performance is usually expressed in terms of an equivalent input noise signal, which gives the same output noise as the circuit under consideration. In this way, the equivalent input noise can be compared directly with incoming signals and the effect of the noise on those signals is easily determined. For this purpose, the circuit of Fig. 11.18 can be represented as shown in Fig. 11.20, where $\overline{v_{i N}^{2}}$ is an input noise-voltage generator that produces the same output noise as all of the original noise generators. All other sources of noise in Fig. 11.20 are considered removed. Using the same equivalent circuit as in Fig. $11.18 b$, we obtain, for the output noise from Fig. 11.20,

$$
\begin{equation*}
\overline{v_{o}^{2}}=g_{m}^{2} R_{L}^{2} \frac{|Z|^{2}}{\left|Z+r_{b}+R_{S}\right|^{2}} \overline{v_{i N}^{2}} \tag{11.45}
\end{equation*}
$$

If this noise expression is equated to $\overline{v_{o}^{2}}$ from (11.37), the equivalent input noise voltage for the circuit can be calculated as

$$
\begin{align*}
\frac{\overline{v_{i N}^{2}}}{\Delta f} & 4 k T\left(R_{S}+r_{b}\right)+\left(R_{S}+r_{b}\right)^{2} 2 q I_{B} \\
& +\frac{1}{g_{m}^{2} R_{L}^{2}} \frac{\left|Z+r_{b}+R_{S}\right|^{2}}{|Z|^{2}} R_{L}^{2}\left(4 k T \frac{1}{R_{L}}+2 q I_{C}\right) \tag{11.46}
\end{align*}
$$

Note that the noise-voltage spectral density given by (11.46) rises at high frequencies because of the variation of $|Z|$ with frequency. This is due to the fact that as the gain of the device falls with frequency, output noise generators $\overline{i_{c}^{2}}$ and $\overline{i_{l}^{2}}$ have a larger effect when referred back to the input.
image_name:Figure 11.20
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: X1, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
name: v^2iN, type: VoltageSource, value: v^2iN, ports: {Np: bo, Nn: X1}
name: Bo, type: NPN, ports: {C: Vo, B: bo, E: GND}
]
extrainfo:The circuit represents a noise performance model with an equivalent input noise voltage source. It includes a noiseless NPN transistor and resistors RS and RL connected to ground, with the output voltage taken across RL.

Figure 11.20 Representation of circuit noise performance by an equivalent input noise voltage.

#### EXAMPLE

Calculate the total input noise voltage $\overline{v_{i N T}^{2}}$ for the circuit of Fig. 11.18 in a bandwidth of 0 to 1 MHz .

This could be calculated using (11.46), derived above. Alternatively, since the total output noise voltage $v_{o T}^{2}$ has already been calculated, this can be used to calculate $\overline{v_{i N T}^{2}}$ (in a $1-\mathrm{MHz}$ bandwidth) by dividing by the circuit voltage gain squared. If $A_{v}$ is the low-frequency, small-signal voltage gain of Fig. 11.18, then

$$
A_{v}=\frac{r_{\pi}}{r_{b}+r_{\pi}+R_{S}} g_{m} R_{L}
$$

Use of the previously specified data for this circuit gives

$$
A_{v}=\frac{26,000}{200+26,000+500} \frac{5000}{260}=18.7
$$

image_name:Since the noise spectrum is flat up to 1 MHz, the low-frequency gain can be used to calculate
description:The image contains a text statement that reads: "Since the noise spectrum is flat up to 1 MHz, the low-frequency gain can be used to calculate." This phrase is underlined, indicating its importance or relevance to the surrounding context. The statement suggests that because the noise spectrum remains constant up to 1 MHz, the low-frequency gain of the circuit can be utilized in calculations, likely related to noise voltage or signal processing in the given context.
$\overline{v_{i N T}^{2}}$ as

$$
\overline{v_{i N T}^{2}}=\frac{\overline{v_{o T}^{2}}}{A_{v}^{2}}=\frac{5 \times 10^{-9}}{18.7^{2}} \mathrm{~V}^{2}=14.3 \times 10^{-12} \mathrm{~V}^{2}
$$

Thus we have

$$
v_{i N T}=3.78 \mu \mathrm{~V} \mathrm{rms}
$$

The above example shows that in a bandwidth of 0 to 1 MHz , the noise in the circuit appears to come from a $3.78-\mu \mathrm{V}$ rms noise-voltage source in series with the input. This noise voltage can be used to estimate the smallest signal that the circuit can effectively amplify, sometimes called the minimum detectable signal (MDS). This depends strongly on the nature of the signal and the application. If no special filtering or coding techniques are used, the MDS
image_name:Figure 11.21
description:The graph in Figure 11.21 is a time-domain waveform display, likely captured on an oscilloscope. The vertical axis represents voltage in microvolts (µV), with markings at intervals of 200 µV, ranging from -400 µV to 400 µV. The horizontal axis denotes time, although specific time units or divisions are not labeled, suggesting a qualitative rather than quantitative analysis of time.

The waveform exhibits a periodic oscillation, resembling a sine wave with noticeable amplitude variations. The amplitude of the waveform appears to peak at approximately 400 µV and trough at around -400 µV, indicating a total peak-to-peak voltage of about 800 µV.

The waveform is characterized by a consistent periodicity, demonstrating regular oscillations without significant distortion or asymmetry. The amplitude of the waveform is consistent with the described input noise voltage of 3.78 µV rms, as the waveform's envelope seems to illustrate the amplified noise signal.

Overall, the graph provides a visual representation of the circuit's output when subjected to a 3.78 µV rms sine wave input, highlighting the noise characteristics and the circuit's ability to handle signals within the specified bandwidth of 0 to 1 MHz.

Figure 11.21 Output voltage waveform of the circuit of Fig. 11.18 with a $3.78-\mu \mathrm{V} \mathrm{rms}$ sinewave applied at the input. The circuit bandwidth is limited to 1 MHz , which gives an equivalent input noise voltage of $3.78 \mu \mathrm{~V} \mathrm{rms}$.
can be taken as equal to the equivalent input noise voltage in the passband of the amplifier. Thus, in this case

$$
\mathrm{MDS}=3.78 \mu \mathrm{~V} \mathrm{rms}
$$

If a sinewave of magnitude $3.78 \mu \mathrm{~V}$ rms were applied to this circuit, and the output in a 1-MHz bandwidth examined on an oscilloscope, the sine wave would be barely detectable in the noise, as shown in Fig. 11.21. The noise waveform in this figure is typical of that produced by shot and thermal noise.

## 11.5 Equivalent Input Noise Generators ${ }^{17}$

In the previous section, the equivalent input noise voltage for a particular configuration was calculated. This gave rise to an expression for an equivalent input noise-voltage generator that was dependent on the source resistance $R_{S}$, as well as the transistor parameters. This method is now extended to a more general and more useful representation in which the noise performance of any two-port network is represented by two equivalent input noise generators. The situation is shown in Fig. 11.22, where a two-port network containing noise generators is represented by the same network with internal noise sources removed (the noiseless network) and with a noise voltage $\overline{v_{i}^{2}}$ and current generator $\overline{i_{i}^{2}}$ connected at the input. It can be shown that this representation is valid for any source impedance, provided that correlation between the two noise generators is considered. That is, the two noise generators are not independent in general because they are both dependent on the same set of original noise sources.

The inclusion of correlation in the noise representation results in a considerable increase in the complexity of the calculations, and if correlation is important, it is often easier to return to the original network with internal noise sources to perform the calculations. However, in a larger number of practical circuits, the correlation is small and may be neglected. In addition, if either equivalent input generator $\overline{v_{i}^{2}}$ or $\overline{i_{i}^{2}}$ dominates, the correlation may be neglected in any case. The use of this method of representation is then extremely useful, as will become apparent.

The need for both an equivalent input noise voltage generator and an equivalent input noise current generator to represent the noise performance of the circuit for any source resistance can be appreciated as follows. Consider the extreme case of source resistance $R_{S}$ equal to zero or infinity. If $R_{S}=0, \overline{i_{i}^{2}}$ in Fig. 11.22 is shorted out, and since the original circuit will still show output noise in general, we need an equivalent input noise voltage $\overline{v_{i}^{2}}$ to represent this behavior. Similarly, if $R_{S} \rightarrow \infty, \overline{v_{i}^{2}}$ in Fig. 11.22 cannot produce output noise and $\overline{\bar{i}_{i}^{2}}$ represents the noise performance of the original noisy network. For finite values of $R_{S}$, both $\overline{v_{i}^{2}}$ and $\overline{i_{i}^{2}}$ contribute to the equivalent input noise of the circuit.
image_name:Figure 11.22
description:The circuit diagram represents the equivalent input noise model of a noisy network. It uses a resistor RS, a voltage source vi^2, and a current source ii^2 to model the noise behavior. The noiseless network is connected to the output of this equivalent model.

Figure 11.22 Representation of noise in a two-port network by equivalent input voltage and current generators.

The values of the equivalent input generators of Fig. 11.22 are readily determined. This is done by first short-circuiting the input of both circuits and equating the output noise in each case to calculate $\overline{v_{i}^{2}}$. The value of $\overline{i_{i}^{2}}$ is found by open-circuiting the input of each circuit and equating the output noise in each case. This will now be done for the bipolar transistor and the MOS transistor.

### 11.5.1 Bipolar Transistor Noise Generators

The equivalent input noise generators for a bipolar transistor can be calculated from the equivalent circuit of Fig. 11.23a. The output noise is calculated with a short-circuited load, and $C_{\mu}$ is neglected. This will be justified later. The circuit of Fig. $11.23 a$ is to be equivalent to that of Fig. $11.23 b$ in that each circuit should give the same output noise for any source impedance.

The value of $\overline{v_{i}^{2}}$ can be calculated by short-circuiting the input of each circuit and equating the output noise $i_{o}$. We use rms noise quantities in the calculations, but make no attempt to preserve the signs of the noise quantities as the noise generators are all independent and have random phase. The polarity of the noise generators does not affect the answer. Short-circuiting the inputs of both circuits in Fig. 11.23, assuming that $r_{b}$ is small $\left(\ll r_{\pi}\right)$ and equating $i_{o}$, we obtain

$$
\begin{equation*}
g_{m} v_{b}+i_{c}=g_{m} v_{i} \tag{11.47}
\end{equation*}
$$

which gives

$$
\begin{equation*}
v_{i}=v_{b}+\frac{i_{c}}{g_{m}} \tag{11.48}
\end{equation*}
$$

Since $r_{b}$ is small, the effect of $\overline{i_{b}^{2}}$ is neglected in this calculation.
image_name:(a)
description:
[
name: rb, type: Resistor, value: rb, ports: {N1: X2, N2: X3}
name: v̅^2b, type: VoltageSource, value: v̅^2b, ports: {Np: X3, Nn: V1}
name: i^2b, type: CurrentSource, value: i^2b, ports: {Np: V1, Nn: X1}
name: rπ, type: Resistor, value: rπ, ports: {N1: V1, N2: X1}
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: V1, Nn: X1}
name: gₘv₁, type: VoltageControlledCurrentSource, value: gₘv₁, ports: {Np: X1, Nn: X1}
name: ro, type: Resistor, value: ro, ports: {N1: X1, N2: X1}
name: i̅c, type: CurrentSource, value: i̅c, ports: {Np: X1, Nn: X1}
]
extrainfo:This is a small-signal equivalent circuit of a bipolar transistor with noise generators. The circuit includes resistors, capacitors, voltage, and current sources to model the noise performance. The nodes are labeled X1, X2, X3, and V1, representing different connection points in the circuit.
image_name:(b)
description:The circuit represents the noise performance equivalent of a bipolar transistor small-signal model. It includes voltage and current noise sources, resistors, and capacitors modeling the transistor's behavior.

Figure 11.23 (a) Bipolar transistor small-signal equivalent circuit with noise generators. (b) Representation of the noise performance of $(a)$ by equivalent input generators.

Using the fact that $v_{b}$ and $i_{c}$ are independent, we obtain, from (11.48),

$$
\begin{equation*}
\overline{v_{i}^{2}}=\overline{v_{b}^{2}}+\frac{\overline{i_{c}^{2}}}{g_{m}^{2}} \tag{11.49}
\end{equation*}
$$

Substituting in (11.49) for $\overline{v_{b}^{2}}$ and $\overline{i_{c}^{2}}$ from (11.11) and (11.12) gives

$$
\overline{v_{i}^{2}}=4 k \operatorname{Tr}_{b} \Delta f+\frac{2 q I_{C} \Delta f}{g_{m}^{2}}
$$

and thus

$$
\begin{equation*}
\frac{\overline{v_{i}^{2}}}{\Delta f}=4 k T\left(r_{b}+\frac{1}{2 g_{m}}\right) \tag{11.50}
\end{equation*}
$$

The equivalent input noise-voltage spectral density of a bipolar transistor thus appears to come from a resistor $R_{\text {eq }}$ such that

$$
\begin{equation*}
\frac{\overline{v_{i}^{2}}}{\Delta f}=4 k T R_{\mathrm{eq}} \tag{11.51}
\end{equation*}
$$

where

$$
\begin{equation*}
R_{\mathrm{eq}}=r_{b}+\frac{1}{2 g_{m}} \tag{11.52}
\end{equation*}
$$

and this is called the equivalent input noise resistance. Of this fictitious resistance, portion $r_{b}$ is, in fact, a physical resistor in series with the input, whereas portion $1 / 2 g_{m}$ represents the effect of collector current shot noise referred back to the input. Equations 11.50 and 11.52 are extremely useful approximations, although the assumption that $r_{b} \ll r_{\pi}$ may not be valid at high collector bias currents, and the calculation should be repeated without restrictions in those circumstances.

Equation 11.50 allows easy comparison of the relative importance of noise from $r_{b}$ and $I_{C}$ in contributing to $\overline{v_{i}^{2}}$. For example, if $I_{C}=1 \mu \mathrm{~A}$, then $1 / 2 g_{m}=13 \mathrm{k} \Omega$ and this will dominate typical $r_{b}$ values of about $100 \Omega$. Alternately, if $I_{C}=10 \mathrm{~mA}$, then $1 / 2 g_{m}=1.3 \Omega$ and noise from $r_{b}$ will totally dominate $\overline{v_{i}^{2}}$. Since $\overline{v_{i}^{2}}$ is the important noise generator for low source impedance (since $\overline{i_{i}^{2}}$ then tends to be shorted), it is apparent that good noise performance from a low source impedance requires minimization of $R_{\mathrm{eq}}$. This is achieved by designing the transistor to have a low $r_{b}$ and running the device at a large collector bias current to reduce $1 / 2 g_{m}$. Finally, it should be noted from (11.50) that the equivalent input noise-voltage spectral density of a bipolar transistor is independent of frequency.

In order to calculate the equivalent input noise current generator $\overline{i_{i}^{2}}$, the inputs of both circuits in Fig. 11.23 are open-circuited and output noise currents $i_{o}$ are equated. Using rms noise quantities, we obtain

$$
\begin{equation*}
\beta(j \omega) i_{i}=i_{c}+\beta(j \omega) i_{b} \tag{11.53}
\end{equation*}
$$

which gives

$$
\begin{equation*}
i_{i}=i_{b}+\frac{i_{c}}{\beta(j \omega)} \tag{11.54}
\end{equation*}
$$

Since $i_{b}$ and $i_{c}$ are independent generators, we obtain, from (11.54),

$$
\begin{equation*}
\overline{i_{i}^{2}}=\overline{i_{b}^{2}}+\frac{\overline{i_{c}^{2}}}{|\beta(j \omega)|^{2}} \tag{11.55}
\end{equation*}
$$

where

$$
\begin{equation*}
\beta(j \omega)=\frac{\beta_{0}}{1+j \frac{\omega}{\omega_{\beta}}} \tag{11.56}
\end{equation*}
$$

and $\beta_{0}$ is the low-frequency, small-signal current gain. [See (1.122) and (1.126)].
Substituting in (11.55) for $\overline{i_{b}^{2}}$ and $\overline{i_{c}^{2}}$ from (11.13) and (11.12) gives

$$
\begin{equation*}
\frac{\overline{i_{i}^{2}}}{\Delta f}=2 q\left[I_{B}+K_{1}^{\prime} \frac{I_{B}^{a}}{f}+\frac{I_{C}}{|\beta(j \omega)|^{2}}\right] \tag{11.57}
\end{equation*}
$$

where

$$
\begin{equation*}
K_{1}^{\prime}=\frac{K_{1}}{2 q} \tag{11.57a}
\end{equation*}
$$

and the burst noise term has been omitted for simplicity. The last term in parentheses in (11.57) is due to collector current noise referred to the input. At low frequencies this becomes $I_{C} / \beta_{0}^{2}$ and is negligible compared with $I_{B}$ for typical $\beta_{0}$ values. When this is true, $\overline{i_{i}^{2}}$ and $\overline{v_{i}^{2}}$ do not contain common noise sources and are totally independent. At high frequencies, however, the last term in (11.57) increases and can become dominant, and correlation between $\overline{v_{i}^{2}}$ and $\overline{i_{i}^{2}}$ may then be important since both contain a contribution from $\overline{i_{c}^{2}}$.

The equivalent input noise current spectral density given by (11.57) appears to come from a current $I_{\text {eq }}$ showing full shot noise, such that

$$
\begin{equation*}
\frac{\overline{i_{i}^{2}}}{\Delta f}=2 q I_{\mathrm{eq}} \tag{11.58}
\end{equation*}
$$

where

$$
\begin{equation*}
I_{\mathrm{eq}}=I_{B}+K_{1}^{\prime} \frac{I_{B}^{a}}{f}+\frac{I_{C}}{|\beta(j \omega)|^{2}} \tag{11.59}
\end{equation*}
$$

and this is called the equivalent input shot noise current. This is a fictitious current composed of the base current of the device plus a term representing flicker noise and one representing collector-current noise transformed to the input. It is apparent from (11.59) that $I_{\text {eq }}$ is minimized by utilizing low bias currents in the transistor, and also using high- $\beta$ transistors. Since $\overline{i_{i}^{2}}$ is the dominant equivalent input noise generator in circuits where the transistor is fed from a high source impedance, low bias currents and high $\beta$ are obviously required for good noise performance under these conditions. Note that the requirement for low bias currents to minimize $\overline{i_{i}^{2}}$ conflicts with the requirement for high bias current to minimize $\overline{v_{i}^{2}}$.

Spectral density $\overline{i_{i}^{2}} / \Delta f$ of the equivalent input noise current generator can be plotted as a function of frequency using (11.57). This is shown in Fig. 11.24 for typical transistor parameters. In this case, the spectral density is frequency dependent at both low and high frequencies, the low-frequency rise being due to flicker noise and the high-frequency rise being due to collector-current noise referred to the input. This input-referred noise rises at high frequencies because the transistor current gain begins to fall, and this is the reason for degradation in transistor noise performance observed at high frequencies.

Frequency $f_{b}$ in Fig. 11.24 is the point where the high-frequency noise asymptote intersects the midband asymptote. This can be calculated from (11.57) as follows:

$$
\begin{equation*}
\beta(j f)=\frac{\beta_{0}}{1+j \frac{f}{f_{T}} \beta_{0}} \tag{11.60}
\end{equation*}
$$

image_name:Figure 11.24
description:The graph in Figure 11.24 is a plot of the equivalent input noise current spectral density of a bipolar transistor. The y-axis represents the noise current spectral density \( \frac{\overline{i_i^2}}{\Delta f} \) in units of \( A^2/Hz \), and the x-axis represents frequency \( f \) in hertz (Hz), on a logarithmic scale.

Overall Behavior and Trends:
- **Low-Frequency Region:** At low frequencies, the graph shows a decreasing trend, characterized by a \( \frac{1}{f} \) flicker noise behavior. This is evident from the initial downward slope on the left side of the graph.
- **Midband Region:** As the frequency increases, the graph reaches a minimum point, indicating the midband region where the noise is relatively constant and at its lowest level.
- **High-Frequency Region:** Beyond this midband region, the graph begins to rise again, showing an \( f^2 \) behavior, which corresponds to the increase in noise due to the fall in transistor current gain at high frequencies.

Key Features and Technical Details:
- **Intersection Points:** The graph includes two significant intersection points:
- \( f_a \), where the flicker noise \( \frac{1}{f} \) intersects the midband noise level.
- \( f_b = 50 \) MHz, where the high-frequency \( f^2 \) noise intersects the midband level.
- **Annotations:** The graph is annotated with the noise behaviors \( \frac{1}{f} \) and \( f^2 \) to indicate the regions of flicker noise and high-frequency noise, respectively.

Annotations and Specific Data Points:
- The noise level is marked at approximately \( 3 \times 10^{-23} \), \( 3 \times 10^{-24} \), and \( 3 \times 10^{-25} \) \( A^2/Hz \) on the y-axis.
- The frequency \( f \) is marked at intervals from \( 10^1 \) to \( 10^{10} \) Hz, showing a wide range of frequencies on the logarithmic scale.

This graph effectively illustrates the behavior of noise in a bipolar transistor across different frequency ranges, highlighting the transition from flicker noise to midband noise, and then to high-frequency noise.

Figure 11.24 Equivalent input noise current spectral density of a bipolar transistor with $I_{C}=100 \mu \mathrm{~A}, \beta_{0}=\beta_{F}=100, f_{T}=500 \mathrm{MHz}$. Typical flicker noise is included.
where $\beta_{0}$ is the low-frequency, small-signal current gain. Thus the collector current noise term in (11.57) is

$$
\begin{equation*}
2 q \frac{I_{C}}{|\beta(j f)|^{2}}=2 q \frac{I_{C}}{\beta_{0}^{2}}\left(1+\frac{f^{2}}{f_{T}^{2}} \beta_{0}^{2}\right) \simeq 2 q I_{C} \frac{f^{2}}{f_{T}^{2}} \tag{11.61}
\end{equation*}
$$

at high frequencies. Equation 11.61 shows that the equivalent input noise current spectrum rises as $f^{2}$ at high frequencies. Frequency $f_{b}$ can be calculated by equating (11.61) to the midband noise, which is $2 q\left[I_{B}+\left(I_{C} / \beta_{0}^{2}\right)\right]$. For typical values of $\beta_{0}$, this is approximately $2 q I_{B}$, and equating this quantity to (11.61) we obtain

$$
2 q I_{B}=2 q I_{C} \frac{f_{b}^{2}}{f_{T}^{2}}
$$

and thus

$$
\begin{equation*}
f_{b}=f_{T} \sqrt{\frac{I_{B}}{I_{C}}} \tag{11.62}
\end{equation*}
$$

The large-signal (or dc) current gain is defined as

$$
\begin{equation*}
\beta_{F}=\frac{I_{C}}{I_{B}} \tag{11.63}
\end{equation*}
$$

and thus (11.62) becomes

$$
\begin{equation*}
f_{b}=\frac{f_{T}}{\sqrt{\beta_{F}}} \tag{11.64}
\end{equation*}
$$

Using the data given in Fig. 11.24, we obtain $f_{b}=50 \mathrm{MHz}$ for that example.
Once the above input noise generators have been calculated, the transistor noise performance with any source impedance is readily calculated. For example, consider the simple circuit of Fig. $11.25 a$ with a source resistance $R_{S}$. The noise performance of this circuit can be
image_name:Fig. 11.25a
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: X}
name: i^2_l, type: CurrentSource, value: i^2_l, ports: {Np: bo, Nn: GND}
name: B0, type: NPN, ports: {C: co, B: bo, E: eo}
name: RL, type: Resistor, value: RL, ports: {N1: co, N2: GND}
name: v^2s, type: VoltageSource, value: v^2s, ports: {Np: X1, Nn: X}
name: v^2i, type: VoltageSource, value: v^2i, ports: {Np: bo, Nn: X1}
]
extrainfo:The circuit represents a simple transistor amplifier with an input noise voltage source and a load resistor. The noise performance is analyzed by considering equivalent noise voltage and current sources.
image_name:Fig. 11.25b
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: x}
name: B0, type: NPN, ports: {C: co, B: bo, E: eo}
name: RL, type: Resistor, value: RL, ports: {N1: co, N2: GND}
name: v^2iN, type: VoltageSource, value: v^2iN, ports: {Np: bo, Nn: x}
]
extrainfo:The circuit represents a noise model with a single equivalent input noise voltage generator. The NPN transistor is connected with its collector to node co, base to node bo, and emitter to node eo, which is grounded. A current source i̅i injects current into node bo.

Figure 11.25 Representation of circuit noise by a single equivalent input noise voltage generator. (a) Original circuit. (b) Equivalent representation.
represented by the total equivalent noise voltage $\overline{v_{i N}^{2}}$ in series with the input of the circuit as shown in Fig. 11.25b. Neglecting noise in $R_{L}$ (this will be discussed later), and equating the total noise voltage at the base of the transistor in Figs. $11.25 a$ and $11.25 b$, we obtain

$$
v_{i N}=v_{s}+v_{i}+i_{i} R_{S}
$$

If correlation between $v_{i}$ and $i_{i}$ is neglected this equation gives

$$
\begin{equation*}
\overline{v_{i N}^{2}}=\overline{v_{s}^{2}}+\overline{v_{i}^{2}}+\overline{i_{i}^{2}} R_{S}^{2} \tag{11.65}
\end{equation*}
$$

Using (11.50) and (11.57) in (11.65) and neglecting flicker noise, we find

$$
\begin{equation*}
\frac{\overline{v_{i N}^{2}}}{\Delta f}=4 k T R_{S}+4 k T\left(r_{b}+\frac{1}{2 g_{m}}\right)+R_{S}^{2} 2 q\left[I_{B}+\frac{I_{C}}{|\beta(j f)|^{2}}\right] \tag{11.66}
\end{equation*}
$$

Equation 11.66 is similar to (11.46) if $r_{b}$ is small, as has been assumed.

#### EXAMPLE

Using data from the example in Section 11.4.1, calculate the total input noise voltage for the circuit of Fig. 11.25a in a bandwidth 0 to 1 MHz neglecting flicker noise and using (11.66). At low frequencies, (11.66) becomes

$$
\begin{aligned}
\overline{\frac{v_{i N}^{2}}{\Delta f}} & =4 k T\left(R_{S}+r_{b}+\frac{1}{2 g_{m}}\right)+R_{S}^{2} 2 q I_{B} \\
& =\left[1.66 \times 10^{-20}(500+200+130)+500^{2} \times 3.2 \times 10^{-19} \times 10^{-6}\right] \mathrm{V}^{2} / \mathrm{Hz} \\
& =(13.8+0.08) \times 10^{-18} \mathrm{~V}^{2} / \mathrm{Hz} \\
& =13.9 \times 10^{-18} \mathrm{~V}^{2} / \mathrm{Hz}
\end{aligned}
$$

The total input noise in a 1-MHz bandwidth is

$$
\begin{aligned}
\overline{v_{i N T}^{2}} & =13.9 \times 10^{-18} \times 10^{6} \mathrm{~V}^{2} \\
& =13.9 \times 10^{-12} \mathrm{~V}^{2}
\end{aligned}
$$

and thus

$$
v_{i N T}=3.73 \mu \mathrm{~V} \mathrm{rms}
$$

This is almost identical to the answer obtained in Section 11.4.1. However, the method described above has the advantage that once the equivalent input generators are known for any particular device, the answer can be written down almost by inspection and requires much less labor.

Also, the relative contributions of the various noise generators are more easily seen. In this case, for example, the equivalent input noise current is obviously a negligible factor.

### 11.5.2 MOS Transistor Noise Generators

The equivalent input noise generators for a MOS field-effect transistor (MOSFET) can be calculated from the equivalent circuit of Fig. 11.26a. This circuit is to be made equivalent to that of Fig. 11.26b. The output noise in each case is calculated with a short-circuit load and $C_{g d}$ is neglected.

If the input of each circuit in Fig. 11.26 is short-circuited and resulting output noise currents $i_{o}$ are equated, we obtain

$$
i_{d}=g_{m} v_{i}
$$

and thus

$$
\begin{equation*}
\overline{v_{i}^{2}}=\frac{\overline{i_{d}^{2}}}{g_{m}^{2}} \tag{11.67}
\end{equation*}
$$

Substituting $\overline{i_{d}^{2}}$ from (11.14) in (11.67) gives

$$
\begin{equation*}
\frac{\overline{v_{i}^{2}}}{\Delta f}=4 k T \frac{2}{3} \frac{1}{g_{m}}+K \frac{I_{D}^{a}}{g_{m}^{2} f} \tag{11.68a}
\end{equation*}
$$

The equivalent input noise resistance $R_{\text {eq }}$ of the MOS transistor is defined as

$$
\frac{\overline{v_{i}^{2}}}{\Delta f}=4 k T R_{\mathrm{eq}}
$$

where

$$
\begin{equation*}
R_{\mathrm{eq}}=\frac{2}{3} \frac{1}{g_{m}}+K^{\prime} \frac{I_{D}^{a}}{g_{m}^{2} f} \tag{11.68b}
\end{equation*}
$$

image_name:(a)
description:
[
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: G(Vg), Nn: D}
name: gmVg, type: CurrentControlledCurrentSource, ports: {Np: D, Nn: D}
name: rd, type: Resistor, value: rd, ports: {N1: D, N2: D}
name: i^2vg, type: CurrentSource, ports: {Np: D, Nn: D}
name: i²g, type: CurrentSource, ports: {Np: G, Nn: D}
]
extrainfo:The circuit diagram (a) represents a MOSFET small-signal equivalent circuit with noise generators. It includes a gate-source capacitance (Cgs), a current-controlled current source (gmVg), and a drain resistor (rd). The diagram shows noise current sources i̅g² and i̅d², as well as an input noise voltage source v̅i².
image_name:(b)
description:
[
name: v_i^2, type: VoltageSource, value: v_i^2, ports: {Np: G, Nn: Vg}
name: i_i^2, type: CurrentSource, value: i_i^2, ports: {Np: D, Nn: Vg}
name: C_gs, type: Capacitor, value: C_gs, ports: {Np: Vg, Nn: D}
name: g_m v_g, type: CurrentSource, value: g_m v_g, ports: {Np: D, Nn: D}
name: r_d, type: Resistor, value: r_d, ports: {N1: D, N2: D}
]
extrainfo:The diagram represents a simplified small-signal equivalent circuit of a MOSFET with noise sources, illustrating the input-referred noise components.
Figure 11.26 (a) MOSFET small-signal equivalent circuit with noise generators. (b) Representation of (a) by two input noise generators.
image_name:Figure 11.27 Typical equivalent input noise voltage spectral density for a MOSFET
description:The graph presented is a log-log plot representing the equivalent input noise voltage spectral density for a MOSFET. The x-axis is labeled 'f' and represents frequency in hertz (Hz), spanning from 10 Hz to 10^8 Hz. The y-axis is labeled with the spectral density formula \( \frac{\overline{v_i^2}}{\Delta f} \) and is measured in \( V^2/Hz \), ranging from 10^{-18} to 10^{-14}.

**Type of Graph and Function:**
The graph is a spectral density plot, typically used to display how power (or variance) is distributed over frequency.

**Axes Labels and Units:**
- **X-axis:** Frequency (f) in hertz (Hz), logarithmic scale from 10 to 10^8.
- **Y-axis:** Noise voltage spectral density \( \frac{\overline{v_i^2}}{\Delta f} \) in \( V^2/Hz \), logarithmic scale from 10^{-18} to 10^{-14}.

**Overall Behavior and Trends:**
The graph shows a decreasing trend of noise voltage spectral density with increasing frequency. At lower frequencies, the noise follows a \( \frac{1}{f} \) behavior, indicating flicker noise dominance. As frequency increases beyond the flicker noise region, the spectral density levels off, indicating a transition to a region dominated by white noise.

**Key Features and Technical Details:**
- **Flicker Noise Region:** At lower frequencies (up to approximately 10^4 Hz), the noise follows a \( \frac{1}{f} \) slope, characteristic of flicker noise.
- **Transition to White Noise:** Beyond approximately 10^5 Hz, the graph shows a flattening trend, indicating the dominance of white noise.
- **Intersection and Asymptotic Behavior:** The intersection between the flicker noise line and the white noise level occurs around 10^5 Hz.

**Annotations and Specific Data Points:**
- A dashed line represents the \( \frac{1}{f} \) slope, indicating the flicker noise region.
- Horizontal dashed line indicates the white noise level at higher frequencies.

This graph effectively illustrates the transition from flicker noise to white noise as frequency increases, which is typical in MOSFET noise analysis.

Figure 11.27 Typical equivalent input noise voltage spectral density for a MOSFET.
and

$$
K^{\prime}=\frac{K}{4 k T}
$$

At frequencies above the flicker noise region, $R_{\mathrm{eq}}=(2 / 3)\left(1 / g_{m}\right)$. For $g_{m}=1 \mathrm{~mA} / \mathrm{V}$, this gives $R_{\mathrm{eq}}=667 \Omega$, which is significantly higher than for a bipolar transistor at a comparable bias current (about 1 mA ). The equivalent input noise-voltage spectral density for a typical MOS transistor is plotted versus frequency in Fig. 11.27. Unlike the bipolar transistor, the equivalent input noise-voltage generator for a MOS transistor contains flicker noise, and it is not uncommon for the flicker noise to extend well into the megahertz region.

In MOS field-effect transistors, the presence of electron energy states at the $\mathrm{Si}^{-} \mathrm{SiO}_{2}$ interface tends to result in an input-referred flicker noise component that is larger than the thermal noise component for frequencies below 1 to 10 kHz for most bias conditions and device geometries. Thus, an accurate representation of the input-referred flicker noise component in MOS transistors is important for the optimization of the noise performance of MOS analog circuits.

The physical mechanisms giving rise to $1 / f$ noise in MOS transistors have received extensive study. ${ }^{18}$ The exact dependence of the magnitude of the input-referred flicker noise on transistor bias conditions and device geometry is dependent on the details of the process that is used to fabricate the device. In most cases, the magnitude of the input-referred flicker noise component is approximately independent of bias current and voltage and is inversely proportional to the active gate area of the transistor. The latter occurs because as the transistor is made larger, a larger number of surface states are present under the gate, so that an averaging effect occurs that reduces the overall noise. It is also observed that the input-referred flicker noise is an inverse function of the gate-oxide capacitance per unit area. This is physically reasonable since the surface states can be thought of as a time-varying component of the surfacestate charge $Q_{s s}$. From (1.139) this produces a time-varying component in the threshold voltage that is inversely proportional to $C_{o x}$. For a MOS transistor, then, the equivalent input-referred voltage noise can often be written as

$$
\begin{equation*}
\frac{\overline{v_{i}^{2}}}{\Delta f}=4 k T \frac{2}{3} \frac{1}{g_{m}}+\frac{K_{f}}{W L C_{o x} f} \tag{11.69}
\end{equation*}
$$

A typical value for $K_{f}$ is $3 \times 10^{-24} \mathrm{~V}^{2}-\mathrm{F}$, or $3 \times 10^{-12} \mathrm{~V}^{2}-\mathrm{pF}$.

The equivalent input noise-current generator $i_{i}^{2}$ for the MOSFET can be calculated by open-circuiting the input of each circuit in Fig. 11.26 and equating the output noise. This gives

$$
i_{i} \frac{g_{m}}{j \omega C_{g s}}=i_{g} \frac{g_{m}}{j \omega C_{g s}}+i_{d}
$$

and thus

$$
\begin{equation*}
i_{i}=i_{g}+\frac{j \omega C_{g s}}{g_{m}} i_{d} \tag{11.70}
\end{equation*}
$$

Since $i_{g}$ and $i_{d}$ represent independent generators, (11.70) can be written as

$$
\begin{equation*}
\overline{i_{i}^{2}}=\overline{i_{g}^{2}}+\frac{\omega^{2} C_{g s}^{2}}{g_{m}^{2}} \overline{i_{d}^{2}} \tag{11.71}
\end{equation*}
$$

Ignoring (11.16) and substituting (11.14) and (11.15) in (11.17) gives

$$
\begin{equation*}
\frac{\overline{i_{i}^{2}}}{\Delta f}=2 q I_{G}+\frac{\omega^{2} C_{g s}^{2}}{g_{m}^{2}}\left(4 k T \frac{2}{3} g_{m}+K \frac{I_{D}^{a}}{f}\right) \tag{11.72}
\end{equation*}
$$

In (11.72) the ac current gain of the MOS transistor can be identified as

$$
\begin{equation*}
A_{I}=\frac{g_{m}}{\omega C_{g s}} \tag{11.73}
\end{equation*}
$$

and thus the noise generators at the output are divided by $A_{I}^{2}$ when referred back to the input. At low frequencies the input noise-current generator is determined by the gate leakage current $I_{G}$, which is very small ( $10^{-15}$ A or less). For this reason, MOS transistors have noise performance that is much superior to bipolar transistors when the driving source impedance is large. Under these circumstances the input noise-current generator is dominant and is much smaller for a MOS transistor than for a bipolar transistor. It should be emphasized, however, that the input noise-voltage generator of a bipolar transistor in (11.50) is typically smaller than that of a MOS transistor in (11.68a) because the bipolar transistor has a larger $g_{m}$ for a given bias current. Thus for low source impedances, a bipolar transistor often has noise performance superior to that of a MOS transistor.

## 11.6 Effect of Feedback on Noise Performance

The representation of circuit noise performance with two equivalent input noise generators is extremely useful in the consideration of the effect of feedback on noise performance. This will be illustrated by considering first the effect of ideal feedback on the noise performance of an amplifier. Practical aspects of feedback and noise performance will then be considered.

### 11.6.1 Effect of Ideal Feedback on Noise Performance

In Fig. 11.28a a series-shunt feedback amplifier is shown where the feedback network is ideal in that the signal feedback to the input is a pure voltage source and the feedback network is unilateral. Noise in the basic amplifier is represented by equivalent input generators $\overline{v_{i a}^{2}}$ and $\overline{i_{i a}^{2}}$. The noise performance of the overall circuit is represented by equivalent input generators $\overline{v_{i}^{2}}$ and $\overline{i_{i}^{2}}$ as shown in Fig. 11.28b. The value of $\overline{v_{i}^{2}}$ can be found by short-circuiting the input of each circuit and equating the output signal. However, since the output of the feedback network has a zero impedance, the current generators in each circuit are then short-circuited and the
image_name:(a)
description:The circuit is a series-shunt feedback amplifier with noise generators represented by v_ia^2 and i_ia^2. The feedback voltage source fv_o is connected in parallel with the output of the op-amp.
image_name:(b)
description:Equivalent representation of a series-shunt feedback amplifier with noise generators, showing two input noise generators.

Figure 11.28 (a) Series-shunt feedback amplifier with noise generators. (b) Equivalent representation of (a) with two input noise generators.
two circuits are identical only if

$$
\begin{equation*}
\overline{v_{i}^{2}}=\overline{v_{i a}^{2}} \tag{11.74}
\end{equation*}
$$

If the input terminals of each circuit are open-circuited, both voltage generators have a floating terminal and thus no effect on the circuit, and for equal output it is necessary that

$$
\begin{equation*}
\overline{i_{i}^{2}}=\overline{i_{i a}^{2}} \tag{11.75}
\end{equation*}
$$

Thus, for the case of ideal feedback, the equivalent input noise generators can be moved unchanged outside the feedback loop and the feedback has no effect on the circuit noise performance. Since the feedback reduces the circuit gain, the output noise is reduced by the feedback, but desired signals are reduced by the same amount and the signal-to-noise ratio will be unchanged. The above result is easily shown for all four possible feedback configurations described in Chapter 8.

### 11.6.2 Effect of Practical Feedback on Noise Performance

The idealized series-shunt feedback circuit considered in the previous section is usually realized in practice as shown in Fig. 11.29a. The feedback circuit is a resistive divider consisting of $R_{E}$ and $R_{F}$. If the noise of the basic amplifier is represented by equivalent input noise generators $\overline{i_{i a}^{2}}$ and $\overline{v_{i a}^{2}}$ and the thermal noise generators in $R_{F}$ and $R_{E}$ are included, the circuit is as shown in Fig. 11.29b. The noise performance of the circuit is to be represented by two equivalent input generators $\overline{v_{i}^{2}}$ and $\overline{i_{i}^{2}}$, as shown in Fig. 11.29c.

In order to calculate $\overline{v_{i}^{2}}$, consider the inputs of the circuits of Fig. $11.29 b$ and $11.29 c$ short-circuited, and equate the output noise. It is readily shown that

$$
\begin{equation*}
v_{i}=v_{i a}+i_{i a} R+\frac{R_{F}}{R_{F}+R_{E}} v_{e}+\frac{R_{E}}{R_{F}+R_{E}} v_{f} \tag{11.76}
\end{equation*}
$$

where

$$
\begin{equation*}
R=R_{F} \| R_{E} \tag{11.77}
\end{equation*}
$$

Assuming that all noise sources in (11.76) are independent, we have

$$
\begin{equation*}
\overline{v_{i}^{2}}=\overline{v_{i a}^{2}}+\overline{i_{i a}^{2}} R^{2}+4 k T R \Delta f \tag{11.78}
\end{equation*}
$$

image_name:(a)
description:The circuit is a series-shunt feedback amplifier with an operational amplifier 'a'. It includes a feedback resistor RF and an emitter resistor RE, forming a voltage divider feedback network. The input is connected to the positive terminal of the op-amp, and the negative terminal is grounded. The output is taken from the op-amp's output terminal.
image_name:(b)
description:The circuit represents a series-shunt feedback configuration with noise sources. It includes an operational amplifier with feedback resistors RE and RF. Noise voltage sources v_ia, v_f, and v_e, and noise current sources i_ia and i_i are included to model the input noise.
image_name:(c)
description:The circuit is a series-shunt feedback amplifier with noise sources included. It uses an operational amplifier with resistors RE and RF to provide feedback and stabilize the gain. The noise sources are modeled as voltage and current sources at the input.

Figure 11.29 (a) Series-shunt feedback circuit. (b) Series-shunt feedback circuit including noise generators. (c) Equivalent representation of (b) with two input noise generators.
where the following substitutions have been made:

$$
\begin{align*}
& \overline{v_{e}^{2}}=4 k T R_{E} \Delta f  \tag{11.79}\\
& \overline{v_{f}^{2}}=4 k T R_{F} \Delta f \tag{11.80}
\end{align*}
$$

Equation 11.78 shows that in this practical case, the equivalent input noise voltage of the overall amplifier contains the input noise voltage of the basic amplifier plus two other terms. The second term in (11.78) is usually negligible, but the third term represents thermal noise in $R=R_{E} \| R_{F}$ and is often significant.

The equivalent input noise current $\overline{i_{i}^{2}}$ is calculated by open-circuiting both inputs and equating output noise. It is apparent that

$$
\begin{equation*}
\overline{i_{i}^{2}} \simeq \overline{i_{i a}^{2}} \tag{11.81}
\end{equation*}
$$

since noise in the feedback resistors is no longer amplified, but appears only in shunt with the output. Thus the equivalent input noise current is unaffected by the application of feedback. The above results are true in general for series feedback at the input. For single-stage series feedback, the above equations are valid with $R_{F} \rightarrow \infty$ and $R=R_{E}$.

If the basic amplifier in Fig. 8.29 is an op amp, the calculation is slightly modified. This is due to the fact (shown in Section 11.8 and Fig. 11.39) that an op amp must be considered a three-port device for noise representation. However, if the circuit of Fig. 11.39 is used as the basic amplifier in the above calculation, expressions very similar to (11.78) and (11.81) are obtained.

Consider now the case of shunt feedback at the input, and as an example consider the shunt-shunt feedback circuit of Fig. 11.30a. This is shown in Fig. 11.30b with noise sources
image_name:Fig. 11.30a
description:The circuit is a shunt-shunt feedback amplifier with an op-amp and resistor RF providing feedback from the output to the input.
image_name:Fig. 11.30b
description:The circuit is a shunt-shunt feedback amplifier with an op-amp and a feedback resistor RF. The output voltage vo is equal to a multiplied by v1.
image_name:Fig. 11.30c
description:The circuit is a feedback amplifier using an op-amp with a gain of 'a' and a feedback resistor RF. The output voltage vo is equal to av1.

Figure 11.30 (a) Shunt-shunt feedback circuit. (b) Shunt-shunt feedback circuit including noise generators. (c) Equivalent representation of (b) with two input noise generators.
$v_{i a}^{2}$ and $i_{i a}^{2}$ of the basic amplifier, and noise source $i_{f}^{2}$ due to $R_{F}$. These noise sources are referred back to the input to give $\overline{v_{i}^{2}}$ and $\overline{i_{i}^{2}}$ as shown in Fig. 11.30c.

Open-circuiting the inputs of Fig. $11.30 b$ and $11.30 c$, and equating output noise, we calculate

$$
\begin{equation*}
i_{i}=i_{i a}+\frac{v_{i a}}{R_{F}}+i_{f} \tag{11.82}
\end{equation*}
$$

Assuming that all noise sources in (11.82) are independent, we find

Thus the equivalent input noise current with shunt feedback applied consists of the input noise current of the basic amplifier together with a term representing thermal noise in the feedback resistor. The second term in (11.83) is usually negligible. These results are true in general for shunt feedback at the input. A general rule for calculating the equivalent input noise contribution due to thermal noise in the feedback resistors is to follow the two-port methods described in Chapter 8 for calculating feedback-circuit loading on the basic amplifier. Once the shunt or series resistors representing feedback loading at the input have been determined, these same resistors may be used to calculate the thermal noise contribution at the input due to the feedback resistors.

If the inputs of the circuits of Fig. $11.30 b$ and $11.30 c$ are short-circuited, and the output noise is equated, it follows that

$$
\begin{equation*}
\overline{v_{i}^{2}} \simeq \overline{v_{i a}^{2}} \tag{11.84}
\end{equation*}
$$

Equations 11.83 and 11.84 are true in general for shunt feedback at the input. They apply directly when the basic amplifier of Fig. 11.30 is an op amp, since one input terminal of the basic amplifier is grounded and the op amp becomes a two-port device.

The above results allow justification of some assumptions made earlier. For example, in the calculation of the equivalent input noise generators for a bipolar transistor in Section 11.5.1, collector-base capacitance $C_{\mu}$ was ignored. This capacitance represents single-stage shunt feedback and thus does not significantly affect the equivalent input noise generators of a transistor, even if the Miller effect is dominant. Note that there is no thermal noise contribution from the capacitor as there was from $R_{F}$ in Fig. 11.30. Also, the second term in (11.83) becomes $\overline{v_{i a}^{2}} /\left|Z_{F}\right|^{2}$ where $Z_{F}$ is the impedance of $C_{\mu}$. Since $\left|Z_{F}\right|$ is quite large at all frequencies of interest, this term is negligible.

#### EXAMPLE

As an example of calculations involving noise in feedback amplifiers, consider the wideband current-feedback pair whose ac schematic is shown in Fig. 11.31. The circuit is fed from a current source and the frequency response $\left|\left(i_{o} / i_{i}\right)(j \omega)\right|$ is flat with frequency to 100 MHz , where it falls rapidly. We calculate the minimum input signal $i_{s}$ required for an output signal-to-noise ratio greater than 20 dB . Data are as follows: $\beta_{1}=\beta_{2}=100, f_{T 1}=300 \mathrm{MHz}, I_{C 1}=$ $0.5 \mathrm{~mA}, I_{C 2}=1 \mathrm{~mA}, f_{T 2}=500 \mathrm{MHz}, r_{b 1}=r_{b 2}=100 \Omega$. Flicker noise is neglected.

The methods developed above allow the equivalent input noise generators for this circuit to be written down by inspection. A preliminary check shows that the noise due to the 20-k $\Omega$ interstage resistor and the base current noise of $Q_{2}$ are negligible. Using the rule stated in Section 11.2.2, we find that the $20-\mathrm{k} \Omega$ resistor contributes an equivalent noise current of $2.5 \mu \mathrm{~A}$. The base current of $Q_{2}$ is $10 \mu \mathrm{~A}$. Both of these can be neglected when compared to the $500 \mu \mathrm{~A}$ collector current of $Q_{1}$. Thus the input noise generators of the whole circuit are those of $Q_{1}$ moved outside the feedback loop, together with the noise contributed by the feedback resistors.

Using the methods of Chapter 8, we can derive the basic amplifier including feedback loading and noise sources for the circuit of Fig. 11.31 as shown in Fig. 11.32. The equivalent input noise-current generator for the overall circuit can be calculated from Fig. 11.32 or by using (11.83) with $R_{F}=5.5 \mathrm{k} \Omega$. Since the circuit is assumed to be driven from a current
image_name:Figure 11.31
description:
[
name: Q1, type: NPN, ports: {C: c1b2, B: b1, E: GND}
name: Q2, type: NPN, ports: {C: c2, B: c1b2, E: e2}
name: R1, type: Resistor, value: 5kΩ, ports: {N1: b1, N2: e2}
name: R2, type: Resistor, value: 20kΩ, ports: {N1: c1b2, N2: GND}
name: R3, type: Resistor, value: 500Ω, ports: {N1: e2, N2: GND}
name: Is, type: CurrentSource, ports: {Np: b1, Nn: GND}
]
extrainfo:The circuit is a current feedback pair with two NPN transistors Q1 and Q2. It uses feedback resistors R1, R2, and R3 to control the operation. The input current source Is drives the circuit, and the output current is taken from the collector of Q2.
Figure 11.31 An ac schematic of a current feedback pair.
image_name:Figure 11.31
description:
[
name: i_f^2, type: CurrentSource, value: i_f^2, ports: {Np: GND, Nn: V1}
name: v^2_ia, type: VoltageSource, value:  v^2_ia, ports: {Np: V1, Nn: b1}
name: 5.5 kΩ, type: Resistor, value: 5.5 kΩ, ports: {N1: V1, N2: GND}
name: i^2_ia, type: CurrentSource, value: i^2_ia, ports: {Np: b1, Nn: GND}
name: Q1, type: NPN, ports: {C: c1b2, B: b1, E: GND}
name: 20 kΩ, type: Resistor, value: 20 kΩ, ports: {N1: c1b2, N2: GND}
name: Q2, type: NPN, ports: {C: i_o, B: c1b2, E: e2}
name: 5 kΩ || 500 Ω, type: Resistor, value: 5 kΩ || 500 Ω, ports: {N1: e2, N2: GND}
]
extrainfo:The circuit is a current feedback pair with two NPN transistors Q1 and Q2. It uses feedback resistors R1, R2, and R3 to control the operation. The input current source Is drives the circuit, and the output current is taken from the collector of Q2.

Figure 11.32 Basic amplifier for the circuit of Fig. 11.31 including feedback loading and noise sources.
source, the equivalent input noise voltage is not important. From (11.83)

$$
\begin{equation*}
\overline{i_{i}^{2}}=\overline{i_{i a}^{2}}+\frac{\overline{v_{i a}^{2}}}{(5500)^{2}}+4 k T \frac{1}{5500} \Delta f \tag{11.85}
\end{equation*}
$$

Using (11.57) and neglecting flicker noise, we have for $\overline{i_{i a}^{2}}$

$$
\overline{i_{i a}^{2}}=2 q\left(I_{B}+\frac{I_{C}}{|\beta(j f)|^{2}}\right) \Delta f
$$

and thus

$$
\begin{equation*}
\frac{\overline{i_{i a}^{2}}}{\Delta f}=2 q\left(5+\frac{500}{|\beta|^{2}}\right) \times 10^{-6} \mathrm{~A}^{2} / \mathrm{Hz} \tag{11.86}
\end{equation*}
$$

Substitution of (11.86) in (11.85) gives

$$
\begin{equation*}
\frac{\overline{i_{i}^{2}}}{\Delta f}=2 q\left(5+\frac{500}{|\beta|^{2}}\right) \times 10^{-6}+\frac{\overline{v_{i a}^{2}}}{(5500)^{2} \Delta f}+2 q(9.1) \times 10^{-6} \tag{11.87}
\end{equation*}
$$

where the noise in the $5.5-\mathrm{k} \Omega$ resistor has been expressed in terms of the equivalent noise current of $9.1 \mu \mathrm{~A}$.

Use of (11.50) gives

$$
\frac{\overline{v_{i a}^{2}}}{\Delta f}=4 k T\left(r_{b 1}+\frac{1}{2 g_{m}}\right)=4 k T(126)
$$

Division of this equation by $(5500)^{2}$ gives

$$
\begin{align*}
\frac{\overline{v_{i a}^{2}}}{(5500)^{2} \Delta f} & =4 k T \frac{1}{240,000}  \tag{11.88}\\
& =2 q(0.2) \times 10^{-6} \tag{11.89}
\end{align*}
$$

Thus the term involving $\overline{v_{i a}^{2}}$ in (11.87) is seen to be equivalent to thermal noise in a $240-\mathrm{k} \Omega$ resistor using (11.88), and this can be expressed as noise in $0.2 \mu \mathrm{~A}$ of equivalent noise current, as shown in (11.89). This term is negligible in this example, as is usually the case.

Combining all these terms we can express (11.87) as

$$
\begin{align*}
\frac{\overline{i_{i}^{2}}}{\Delta f} & =2 q\left(5+\frac{500}{|\beta|^{2}}+0.2+9.1\right) \times 10^{-6} \mathrm{~A}^{2} / \mathrm{Hz} \\
& =2 q\left(14.3+\frac{500}{|\beta|^{2}}\right) \times 10^{-6} \mathrm{~A}^{2} / \mathrm{Hz} \tag{11.90}
\end{align*}
$$

Equation 11.90 shows that the equivalent input noise-current spectral density rises at high frequencies (as $|\beta|$ falls) as expected for a transistor. In a single transistor without feedback, the equivalent input noise current also rises with frequency, but because the transistor gain falls with frequency, the output noise spectrum of a transistor without feedback always falls as frequency rises (see Section 11.4.1). However, in this case, the negative feedback holds the gain constant with frequency, and thus the output noise spectrum of this circuit will rise as frequency increases, until the amplifier band edge is reached. This is illustrated in Fig. 11.33, where the input noise-current spectrum, the amplifier frequency response squared, and the output noise-current spectrum (product of the first two) are shown. The current gain of the circuit is $A_{I} \simeq 11$.
image_name:(a)
description:The graph labeled (a) is a plot of the equivalent input noise spectrum. It is a log-log plot with the x-axis representing frequency \( f \) in hertz (Hz) and the y-axis representing the noise spectral density \( \frac{\overline{i_{i}^{2}}}{\Delta f} \) in \( A^2/Hz \). The frequency scale is logarithmic, ranging from \( 10^3 \) Hz to \( 10^9 \) Hz, and the noise spectral density also follows a logarithmic scale, ranging from \( 10^{-24} \) to \( 10^{-22} \) \( A^2/Hz \).

Overall Behavior and Trends:
- **Low-Frequency Region:** The noise spectrum is relatively flat and constant at approximately \( 10^{-23} \) \( A^2/Hz \) up to around \( 10^8 \) Hz.
- **High-Frequency Region:** Beyond \( 10^8 \) Hz, the noise spectrum begins to rise sharply, indicating an increase in noise with frequency.

Key Features and Technical Details:
- **Constant Region:** The flat region suggests that the input noise is stable across a wide range of lower frequencies.
- **Rising Edge:** The sharp increase in the noise spectrum at high frequencies suggests a significant change in behavior, likely due to the amplifier's frequency response approaching its band edge.
- **Numerical Annotation:** At \( 10^8 \) Hz, the noise spectral density is annotated with a value of \( 4.6 \times 10^{-24} \) \( A^2/Hz \), indicating a reference point for the rising trend.

Annotations and Specific Data Points:
- The graph includes a dashed line marking the frequency \( 10^8 \) Hz, which aligns with the point where the noise spectrum starts to rise.
- The annotation \( 4.6 \times 10^{-24} \) \( A^2/Hz \) provides a specific value for the noise level at this critical frequency point.
image_name:(b)
description:The graph labeled "(b)" in Figure 11.33 represents the frequency response squared of an amplifier circuit. This is a Bode plot, which typically shows the magnitude of a system's frequency response. In this specific graph, the vertical axis is labeled \(|A_I|^2\), representing the square of the current gain magnitude, and is plotted on a logarithmic scale with values ranging from 10 to 1000. The horizontal axis is labeled \(f\) in Hertz (Hz), also using a logarithmic scale, spanning from \(10^3\) Hz to \(10^9\) Hz.

**Overall Behavior and Trends:**
- The graph shows a flat response, indicating that the squared magnitude of the current gain \(|A_I|^2\) is constant across the frequency range shown.
- The value of \(|A_I|^2\) is marked as 121, suggesting that the gain remains constant at this level until a certain frequency point.

**Key Features and Technical Details:**
- The constant value of 121 indicates that the current gain squared is stable across the frequency spectrum depicted in the graph.
- There are no peaks, valleys, or inflection points within the frequency range presented, emphasizing the stability and consistency of the gain.
- The graph does not show any cutoff frequency or bandwidth limitations within the plotted range, implying that the gain is maintained throughout.

**Annotations and Specific Data Points:**
- The graph is straightforward with a single marked value of 121, which is the squared gain value maintained across the frequency range.
- The graph does not include additional annotations or markers beyond the constant gain value.

This plot demonstrates the behavior of the amplifier's frequency response squared, reinforcing the concept that the gain remains constant with frequency due to negative feedback, as described in the context.
image_name:(c)
description:The graph labeled (c) is a plot of the output noise spectrum of a circuit. It is a frequency-domain graph showing the spectral density of the output noise current, \( \frac{\overline{i_{o}^{2}}}{\Delta f} \), on the vertical axis, measured in \( \text{A}^2/\text{Hz} \), versus frequency \( f \) on the horizontal axis, measured in hertz (Hz). The horizontal axis is logarithmically scaled, ranging from \( 10^3 \) Hz to \( 10^9 \) Hz, while the vertical axis is also logarithmically scaled, ranging from \( 10^{-22} \) to \( 10^{-20} \) \( \text{A}^2/\text{Hz} \).

**Overall Behavior and Trends:**
- The graph shows that the output noise spectrum is relatively constant at lower frequencies, maintaining a value close to \( 5.6 \times 10^{-22} \) \( \text{A}^2/\text{Hz} \) up to a certain point.
- As the frequency approaches \( 10^8 \) Hz, there is a noticeable rise in the noise spectrum, indicating an increase in noise with frequency.

**Key Features and Technical Details:**
- The graph remains flat until it nears the cutoff frequency around \( 10^8 \) Hz, where the noise spectrum begins to rise sharply.
- This behavior is consistent with the description that the output noise spectrum increases with frequency until the amplifier band edge is reached.
- The significant rise in noise at higher frequencies suggests the influence of the amplifier's frequency response on the output noise.

**Annotations and Specific Data Points:**
- A horizontal dashed line is shown at \( 5.6 \times 10^{-22} \) \( \text{A}^2/\text{Hz} \), indicating the level of the noise spectrum in the lower frequency range.
- A vertical dashed line at \( 10^8 \) Hz marks the frequency where the noise begins to rise sharply, which is a critical point in understanding the behavior of the output noise.

Figure 11.33 Noise performance of the circuit of Fig. 11.32. (a) Equivalent input noise spectrum. (b) Frequency response squared.
(c) Output noise spectrum.

The total output noise from the circuit $\overline{i_{o T}^{2}}$ is obtained by integrating the output noise spectral density, which is

$$
\begin{equation*}
\frac{\overline{i_{o}^{2}}}{\Delta f}=A_{I}^{2} \frac{\overline{i_{i}^{2}}}{\Delta f} \tag{11.91}
\end{equation*}
$$

Thus

$$
\begin{align*}
\overline{i_{o T}^{2}} & =\int_{0}^{B} A_{I}^{2} \frac{\overline{i_{i}^{2}}}{\Delta f} d f \\
& =A_{I}^{2} \int_{0}^{B} 2 q\left(14.3+\frac{500}{|\beta(j f)|^{2}}\right) \times 10^{-6} d f \tag{11.92}
\end{align*}
$$

where (11.90) has been used and $A_{I}^{2}$ is assumed constant up to $B=10^{8} \mathrm{~Hz}$ as specified earlier. The current gain is

$$
\begin{equation*}
\beta(j f)=\frac{\beta_{0}}{1+j \frac{\beta_{0} f}{f_{T 1}}} \tag{11.93}
\end{equation*}
$$

and

$$
\begin{equation*}
\frac{1}{|\beta(j f)|^{2}}=\frac{1}{\beta_{0}^{2}}\left(1+\frac{\beta_{0}^{2} f^{2}}{f_{T 1}^{2}}\right) \tag{11.94}
\end{equation*}
$$

Substitution of (11.94) in (11.92) gives

$$
\begin{align*}
\overline{i_{o T}^{2}} & =A_{I}^{2} 2 q \times 10^{-6} \int_{0}^{B}\left[14.3+\frac{500}{\beta_{0}^{2}}\left(1+\frac{\beta_{0}^{2} f^{2}}{f_{T 1}^{2}}\right)\right] d f  \tag{11.95}\\
& =A_{I}^{2} 2 q \times 10^{-6}\left[14.3 f+\frac{500}{\beta_{0}^{2}} f+\frac{500}{f_{T 1}^{2}} \frac{f^{3}}{3}\right]_{0}^{B} \tag{11.96}
\end{align*}
$$

Using $\beta_{0}=100$ and $B=100 \mathrm{MHz}=f_{T 1} / 3$ gives

$$
\begin{align*}
& \overline{i_{o T}^{2}}=A_{I}^{2} \times 2 q \times 10^{-6}(14.3 B+18.6 B)  \tag{11.97}\\
& \overline{i_{o T}^{2}}=A_{I}^{2} \times 1.05 \times 10^{-15} \mathrm{~A}^{2} \tag{11.98}
\end{align*}
$$

The equivalent input noise current is

$$
\overline{i_{i T}^{2}}=\frac{\overline{i_{o T}^{2}}}{\overline{A_{I}^{2}}}=1.05 \times 10^{-15} \mathrm{~A}^{2}
$$

and from this

$$
\begin{equation*}
i_{i T}=32.4 \mathrm{nArms} \tag{11.99}
\end{equation*}
$$

Thus the equivalent input noise current is 32.4 nA rms and (11.97) shows that the frequencydependent part of the equivalent input noise is dominant. For a $20-\mathrm{dB}$ signal-to-noise ratio, input signal current $i_{s}$ must be greater than $0.32 \mu \mathrm{~A}$ rms.

## 11.7 Noise Performance of Other Transistor Configurations

Transistor configurations other than the common-emitter and common-source stages considered so far are often used in integrated-circuit design. The noise performance of other important configurations will now be considered. To avoid repetition, the discussion will be directed toward bipolar devices only. However, all the results carry over directly to FET circuits.

### 11.7.1 Common-Base Stage Noise Performance

The common-base stage is sometimes used as a low-input-impedance current amplifier. A common-base stage is shown in Fig. $11.34 a$ and the small-signal equivalent circuit is shown in Fig. $11.34 b$ together with the equivalent input noise generators derived for a common-emitter stage. Since these noise generators represent the noise performance of the transistor in any connection, Fig. $11.34 b$ is a valid representation of common-base noise performance. In Fig. $11.34 c$ the noise performance of the common-base stage is represented in the standard fashion with equivalent input noise generators $\overline{v_{i B}^{2}}$ and $\overline{i_{i B}^{2}}$. These can be related to the common-emitter input generators by alternately short circuiting and open circuiting the circuits of Fig. 11.34b and $11.34 c$ and equating output noise. It then follows that

$$
\begin{align*}
& \overline{i_{i B}^{2}}=\overline{i_{i}^{2}}  \tag{11.100}\\
& \overline{v_{i B}^{2}}=\overline{v_{i}^{2}} \tag{11.101}
\end{align*}
$$

image_name:(a)
description:The diagram (a) represents a common-base transistor configuration with an NPN transistor labeled B0. The collector is connected to node C, the base is connected to node B, and the emitter is connected to node E. This configuration is used to analyze noise performance in integrated circuits.
image_name:(b)
description:The diagram represents a common-base transistor configuration with noise analysis, including equivalent input noise generators.
image_name:(c)
description:The circuit diagram represents a common-base equivalent circuit with input noise generators. It includes noise sources modeled as voltage and current sources. The diagram illustrates the equivalence of input noise in common-emitter and common-base transistor configurations.

Figure 11.34 (a) Common-base transistor configuration. (b) Common-base equivalent circuit with noise generators. (c) Common-base equivalent circuit with input noise generators.

Thus the equivalent input noise generators of common-emitter and common-base connections are the same and the noise performance of the two configurations is identical, even though their input impedances differ greatly.

Although the noise performances of common-emitter and common-base stages are nominally identical (for the same device parameters), there is one characteristic of the common-base stage that makes it generally unsuitable for use as a low-noise input stage. This is due to the fact that its current gain $\alpha \simeq 1$, and thus any noise current at the output of the common-base stage is referred directly back to the input without reduction. Thus a $10-\mathrm{k} \Omega$ load resistor that has an equivalent noise current of $5 \mu \mathrm{~A}$ produces this amount of equivalent noise current at the input. In many circuits this would be the dominant source of input current noise. The equivalent input noise currents of following stages are also referred back unchanged to the input of the common-base stage. This problem can be overcome in discrete common-base circuits by use
image_name:Figure 11.35 Emitter-follower circuit
description:
[
name: B0, type: NPN, ports: {C: GND, B: Vi, E: Vo}
name: ZL, type: Resistor, value: ZL, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is an emitter-follower configuration with a single NPN transistor B0 and a load resistor ZL connected to the emitter. The input voltage is applied at the base, and the output is taken from the emitter. The collector is connected to the ground.

Figure 11.35 Emitter-follower circuit.
of a transformer that gives current gain at the output of the common-base stage. This option is not available in integrated-circuit design unless resort is made to external components.

### 11.7.2 Emitter-Follower Noise Performance

Consider the emitter follower shown in Fig. 11.35. The noise performance of this circuit can be calculated using the results of previous sections. The circuit can be viewed as a series-feedback stage and the equivalent input noise generators of the transistor can be moved unchanged back to the input of the complete circuit. Thus, if noise in $z_{L}$ is neglected, the emitter follower has the same equivalent input noise generators as the common-emitter and common-base stages. However, since the emitter follower has unity voltage gain, the equivalent input noise voltage of the following stage is transformed unchanged to the input, thus degrading the noise performance of the circuit. Noise due to $z_{L}$ must also be included, but since the follower output is taken at the emitter, which is a low impedance point, the noise due to $z_{L}$ is greatly attenuated compared with its effect on a series-feedback stage.

### 11.7.3 Differential-Pair Noise Performance

The differential pair is the basic building block of linear integrated circuits and, as such, its noise performance is of considerable importance. A bipolar differential pair is shown in Fig. $11.36 a$, and the base of each device is generally independently accessible, as shown. Thus this circuit cannot in general be represented as a two-port, and its noise performance cannot be represented in the usual fashion by two input noise generators. However, the techniques developed previously can be used to derive an equivalent noise representation of the circuit that employs two noise generators at each input. This is illustrated in Fig. 11.36b, and a simpler version of this circuit, which employs only three noise generators, is shown in Fig. 11.36c.

The noise representation of Fig. $11.36 b$ can be derived by considering noise due to each device separately. Consider first noise in $Q_{1}$, which can be represented by input noise generators $\overline{v_{i}^{2}}$ and $\overline{i_{i}^{2}}$ as shown in Fig. 11.37a. These noise generators are those for a single transistor as given by (11.50) and (11.57). Transistor $Q_{2}$ is initially assumed noiseless and the impedance seen looking in its emitter is $z_{E 2}$. Note that $z_{E 2}$ will be a function of the impedance connected from the base of $Q_{2}$ to ground. As described in previous sections, the noise generators of Fig. $11.37 a$ can be moved unchanged to the input of the circuit (independent of $z_{E 2}$ ) as shown in Fig. 11.37b. This representation can then be used to calculate the output noise produced by $Q_{1}$ in the differential pair for any impedances connected from the base of $Q_{1}$ and $Q_{2}$ to ground.

Now consider noise due to $Q_{2}$. In similar fashion this can be represented by noise generators $\overline{v_{i}^{2}}$ and $\overline{i_{i}^{2}}$, as shown in Fig. 11.37c. In this case $Q_{1}$ is assumed noiseless and $z_{E 1}$ is the
impedance seen looking in at the emitter of $Q_{1}$. If $Q_{1}$ and $Q_{2}$ are identical, the equivalent input noise generators of Fig. $11.37 b$ and $11.37 c$ are identical. However, since they are produced by different transistors, the noise generators of Fig. $11.37 b$ and $11.37 c$ are independent. The total noise performance of the differential pair including noise due to both $Q_{1}$ and $Q_{2}$ can thus be represented as shown in Fig. 11.36b, and this representation is valid for any source resistance connected to either input terminal. Noise generators $\overline{v_{i}^{2}}$ and $\overline{i_{i}^{2}}$ are basically those due to each transistor alone. If noise due to $R_{L}$ or following stages is significant, it should be referred back symmetrically to the appropriate input. In practice, current source $I_{E E}$ will also contain noise, and this can be included in the representation. However, if the circuit is perfectly balanced, the current-source noise represents a common-mode signal and will produce no differential output.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: Vop, B: Vip, E: e1,e2}
name: Q2, type: NPN, ports: {C: Vpp, B: Vin, E: e1,e2}
name: RL1, type: Resistor, value: RL, ports: {N1: VCC, N2: Vop}
name: RL2, type: Resistor, value: RL, ports: {N1: VCC, N2: Vpp}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: e1,e2, Nn: VEE}
]
extrainfo:The circuit is a differential pair with two NPN transistors Q1 and Q2, sharing a common emitter current source IEE. The resistors RL are connected to the collectors of the transistors and VCC. The differential inputs are Vip and Vin, with outputs at Vop and Vpp.

image_name:(a) Differential-pair circuit
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Vip, type: VoltageSource, value: Vip, ports: {Np: Vip, Nn: GND}
name: i2i, type: CurrentSource, value: i2i, ports: {Np: GND, Nn: b1}
name: i2i, type: CurrentSource, value: i2i, ports: {Np: GND, Nn: b2}
name: Q1, type: NPN, ports: {C: Vop, B: b1, E: ee2}
name: Q2, type: NPN, ports: {C: Vpp, B: b2, E: ee2}
name: RL, type: Resistor, value: RL, ports: {N1: VCC, N2: Vop}
name: RL, type: Resistor, value: RL, ports: {N1: VCC, N2: Vpp}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: ee2, Nn: GND}
]
extrainfo:The circuit is a differential pair with two NPN transistors (Q1 and Q2) sharing a common emitter current source (IEE). The resistors (RL) are connected to the collectors of the transistors and VCC. The differential inputs are Vip and Vin, with outputs at Vop and Vpp.

Figure 11.36
(a) Differential-pair circuit.
(b) Complete differential pair noise representation.
image_name:Figure 11.36 (b)
description:
[
name: Q1, type: NPN, ports: {C: Vu, B: Vip, E: ee2}
name: Q2, type: NPN, ports: {C: Vw, B: Vin, E: ee2}
name: RL1, type: Resistor, value: RL, ports: {N1: Vu, N2: VCC}
name: RL2, type: Resistor, value: RL, ports: {N1: Vw, N2: VCC}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: VEE, type: VoltageSource, value: VEE, ports: {Np: ee2, Nn: GND}
name: IEE, type: CurrentSource, value: IEE, ports: {Np: ee2, Nn: GND}
]
extrainfo:The circuit is a differential pair with two NPN transistors (Q1 and Q2) sharing a common emitter current source (IEE). The resistors (RL) are connected to the collectors of the transistors and VCC. The differential inputs are Vip and Vin, with outputs at Vop and Vw.

Figure 11.36 (c) Simplified
(c)
noise representation.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: a, B: x1, E: e1}
name: RL, type: Resistor, value: RL, ports: {N1: a, N2: GND}
name: Z_E2, type: Resistor, value: Z_E2, ports: {N1: e1, N2: GND}
name: I_i, type: CurrentSource, value: I_i, ports: {Np: x1, Nn: e1}
name: V_i, type: VoltageSource, value: V_i, ports: {Np: Vin, Nn: x1}
]
extrainfo:The circuit is an AC schematic of a differential pair including noise due to Q1 only. It shows the input voltage source V_i connected to the base of Q1, with a current source I_i modeling noise. The collector of Q1 is connected to RL and the emitter to Z_E2, both leading to ground.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: c1, B: x1, E: e1}
name: RL, type: Resistor, value: RL, ports: {N1: c1, N2: GND}
name: Z_E2, type: Resistor, value: Z_E2, ports: {N1: e1, N2: GND}
name: i_i^2, type: CurrentSource, value: i_i^2, ports: {Np: x1, Nn: GND}
name: v_i^2, type: VoltageSource, value: v_i^2, ports: {Np: vin, Nn: x1}
]
extrainfo:The circuit diagram (b) represents an AC schematic of a differential pair with noise due to Q1 referred to the input. Q1 is an NPN transistor with its collector connected to RL and GND, base connected to vin through v_i^2, and emitter connected to Z_E2 and GND. The current source i_i^2 is connected between x1 and GND.
image_name:(c)
description:
[
name: Q2, type: NPN, ports: {C: c2, B: b2, E: e2}
name: RL, type: Resistor, value: RL, ports: {N1: c2, N2: GND}
name: Z_E1, type: Resistor, value: Z_E1, ports: {N1: e2, N2: GND}
name: i_i, type: CurrentSource, value: i_i, ports: {Np: e2, Nn: GND}
]
extrainfo:This is an AC schematic of a differential pair including noise due to Q2 only. The circuit includes an NPN transistor Q2, a load resistor RL connected to the collector of Q2, and a resistor Z_E1 connected to the emitter. The current source i_i is connected to the emitter and ground. The input is labeled as Vin.

Figure 11.37 (a) ac schematic of a differential pair including noise due to $Q_{1}$ only. (b) ac schematic of a differential pair with noise due to $Q_{1}$ referred to the input. (c) ac schematic of a differential pair including noise due to $Q_{2}$ only.

The noise representation of Fig. $11.36 b$ can be simplified somewhat if the common-mode rejection of the circuit is high. In this case, one of the noise-voltage generators can be moved to the other side of the circuit, as shown in Fig. 11.36c. This can be justified if equal noisevoltage generators are added in series with each input and these generators are chosen such that the noise voltage at the base of $Q_{2}$ is canceled. This leaves two independent noise-voltage generators in series with the base of $Q_{1}$, and these can be represented as a single noise-voltage generator of value $\overline{2 v_{i}^{2}}$. Thus for the circuit of Fig. $11.36 c$ we can write

$$
\begin{gather*}
\overline{v_{d p}^{2}}=2 \overline{v_{i}^{2}}  \tag{11.102}\\
\overline{i_{d p}^{2}}=\overline{i_{i}^{2}} \tag{11.103}
\end{gather*}
$$

where $\overline{v_{d p}^{2}}$ and $\overline{i_{d p}^{2}}$ are the equivalent input noise generators of the differential pair.
The differential pair is often operated with the base of $Q_{2}$ grounded, and in this case the noise-current generator at the base of $Q_{2}$ is short circuited. The noise performance of the circuit is then represented by the two noise generators connected to the base of $Q_{1}$ in Fig. 11.36c. In this case the equivalent input noise-current generator of the differential pair is simply that due to one transistor alone, whereas the equivalent input noise-voltage generator has a meansquare value twice that of either transistor. Thus from a low source impedance, a differential pair has an equivalent input noise voltage 3 dB higher than a common-emitter stage with the same collector current as the devices in the pair.

## 11.8 Noise in Operational Amplifiers

Integrated-circuit amplifiers designed for low-noise operation generally use a simple commonemitter or common-source differential-pair input stage with resistive loads. Since the input stage has both current and voltage gain, the noise of following stages is generally not significant, and the resistive loads make only a small noise contribution. The noise analysis of such circuits is quite straightforward using the techniques described in this chapter. However, circuits of this type (the 725 op amp is an example) are inefficient in terms of optimizing important op amp parameters such as gain and bandwidth. To improve the gain, active loads can be used as in the first stage of the NE5234 op amp. However, by their very nature, active loads amplify their own internal noise and cause considerable degradation of circuit noise performance. To illustrate these points and show the compromises involved in the design of general-purpose circuits, an approximate noise analysis of the NE5234 will now be made. ${ }^{19}$

A simplified schematic of the input stage of the NE5234 is shown in Fig. 11.38a. The common-mode input voltage, $V_{I C}$, is assumed to be low enough that the npn input pair $Q_{1}-Q_{2}$ in Fig. 6.36 is off and can be ignored here. The differential output current is $i_{o}$. Components $Q_{13}$ and $R_{13}$ of the active load generate noise and contribute to the output noise at $i_{o}$. Since transistor $Q_{9}$ presents a high impedance to the active load, the noise due to the active load can be calculated from the isolated portion of the circuit shown in Fig. 11.38b. Noise due to $Q_{13}$ and $R_{13}$ is represented by equivalent input noise generators $\overline{v_{i 13}^{2}}$ and $\overline{i_{i 13}^{2}}$. The impedance looking back into the Bias ${ }_{1}$ output of the bias circuit is small and ignored. Therefore, $\overline{\dot{i}_{i 13}^{2}}$ may be neglected. Also, noise generated in the bias circuit may be ignored because it couples into $Q_{13}$ and $Q_{14}$ equally and does not affect the differential output current $i_{o}$ with perfect matching. Start with (11.78). Using (11.50) for $\overline{v_{i a}^{2}}$ and neglecting the $\overline{i_{i a}^{2}}$ term as well as flicker
image_name:(a)
description:
[
name: R11, type: Resistor, value: 33kΩ, ports: {N1: VCC, N2: e11}
name: R13, type: Resistor, value: 33kΩ, ports: {N1: VCC, N2: e13}
name: R14, type: Resistor, value: 33kΩ, ports: {N1: VCC, N2: e14}
name: R9, type: Resistor, value: 22kΩ, ports: {N1: c3e9, N2: GND}
name: R10, type: Resistor, value: 22kΩ, ports: {N1: c4e10, N2: GND}
name: Q11, type: PNP, ports: {C: e11, B: Bias1, E: c3e9}
name: Q13, type: PNP, ports: {C: e13, B: Bias1, E: 9}
name: Q14, type: PNP, ports: {C: e14, B: Bias1, E: 10}
name: Q3, type: PNP, ports: {C: c3e9, B: Vin, E: e3e11}
name: Q4, type: PNP, ports: {C: c4e10, B: Vip, E: e4e10}
name: Q9, type: NPN, ports: {C: 9, B: c3e9, E: GND}
name: Q10, type: NPN, ports: {C: 10, B: c4e10, E: GND}
]
extrainfo:This circuit is the input stage of the NE5234 operational amplifier. It uses a differential pair with Q3 and Q4, and current mirrors with Q9 and Q10 for biasing. The resistors R11, R13, and R14 provide biasing from VCC, while R9 and R10 are connected to ground. Transistors Q13 and Q14 serve as part of the current mirror configuration, and Q11 is part of the biasing network.
image_name:(b)
description:
[
name: Q3, type: PNP, ports: {C: c3eq, B: Vin, E: e3eq}
name: Q4, type: PNP, ports: {C: c4e10, B: Vip, E: e4e10}
name: Q9, type: NPN, ports: {C: 9, B: c3eq, E: GND}
name: Q10, type: NPN, ports: {C: 10, B: c4e10, E: GND}
name: Q11, type: PNP, ports: {C: e11, B: Bias1, E: GND}
name: Q13, type: PNP, ports: {C: e13, B: Bias1, E: 9}
name: Q14, type: PNP, ports: {C: e14, B: Bias1, E: 10}
name: R11, type: Resistor, value: 33kΩ, ports: {N1: VCC, N2: e11}
name: R13, type: Resistor, value: 33kΩ, ports: {N1: VCC, N2: e13}
name: R14, type: Resistor, value: 33kΩ, ports: {N1: VCC, N2: e14}
name: R9, type: Resistor, value: 22kΩ, ports: {N1: c3eq, N2: GND}
name: R10, type: Resistor, value: 22kΩ, ports: {N1: c4e10, N2: GND}
]
extrainfo:The circuit represents a simplified schematic of the NE5234 op amp input stage. It includes differential input pairs formed by Q3, Q4, Q9, and Q10, with additional current mirrors for biasing. The resistors R11, R13, and R14 are connected to VCC, while R9 and R10 are connected to ground. The noise analysis focuses on Q13 and the associated resistor R13 in the context of noise evaluation.

Figure 11.38 (a) Simplified schematic of the NE5234 op amp input stage with $V_{I C} \ll 0.8 \mathrm{~V}$. (b) ac schematic (including noise) of $Q_{13}$ and $R_{13}$.
noise gives

$$
\begin{equation*}
\overline{\frac{v_{i 13}^{2}}{\Delta f}}=4 k T\left(r_{b 13}+\frac{1}{2 g_{m 13}}+R_{13}\right) \tag{11.104}
\end{equation*}
$$

This noise generator can be evaluated as follows. The dc collector current in $Q_{13}$ is approximately $6 \mu \mathrm{~A}$, giving $1 / 2 g_{m 13}=2.17 \mathrm{k} \Omega$. Also, $R_{13}=33 \mathrm{k} \Omega$, and a typical value of $r_{b}$ for pnp transistors is $200 \Omega$. Thus (11.104) becomes

$$
\begin{equation*}
\overline{\frac{v_{i 13}^{2}}{\Delta f}}=4 k T(35,000) \tag{11.105}
\end{equation*}
$$

This noise generator produces a noise output $i_{o A}$ where

$$
\begin{equation*}
i_{o A} \simeq \frac{1}{\frac{1}{g_{m 13}}+R_{13}} v_{i 13} \simeq \frac{v_{i 13}}{37,000} \tag{11.106}
\end{equation*}
$$

Using (11.105) in (11.106) gives

$$
\begin{equation*}
\frac{\overline{i_{O A}^{2}}}{\Delta f}=4 k T \frac{35,000}{37,000^{2}} \tag{11.107}
\end{equation*}
$$

A similar analysis done to find $\overline{v_{i 9}^{2}}$, the noise due to $Q_{9}$ and $R_{9}$ in series with the base of $Q_{9}$, gives

$$
\begin{equation*}
\frac{\overline{v_{i 9}^{2}}}{\Delta f}=4 k T\left(r_{b 9}+\frac{1}{2 g_{m 9}}+R_{9}\right) \tag{11.108}
\end{equation*}
$$

The dc collector current in $Q_{9}$ is approximately $6 \mu \mathrm{~A}$, giving $1 / 2 g_{m 9}=2.17 \mathrm{k} \Omega$. Also, $R_{9}=$ $22 \mathrm{k} \Omega$, and a typical value of $r_{b}$ for $n p n$ transistors is $400 \Omega$. Thus (11.108) becomes

$$
\begin{equation*}
\frac{\overline{v_{i 9}^{2}}}{\Delta f}=4 k T(25,000) \tag{11.109}
\end{equation*}
$$

This noise generator produces a noise output $i_{o B}$ where

$$
\begin{equation*}
i_{o B} \simeq \frac{1}{\frac{1}{g_{m 9}}+R_{9}} v_{i 9} \simeq \frac{v_{i 9}}{26,000} \tag{11.110}
\end{equation*}
$$

Using (11.109) in (11.110) gives

$$
\begin{equation*}
\frac{\overline{i_{o B}^{2}}}{\Delta f}=4 k T \frac{25,000}{26,000^{2}} \tag{11.111}
\end{equation*}
$$

The total mean-square noise current in the output at node 9 due to the active loads is $\overline{i_{o A}^{2}}+\overline{i_{o B}^{2}}$. Components $Q_{14}, R_{14}, Q_{10}$, and $R_{10}$ generate an equal mean-square noise current in the output at node 10. Although Fig. 11.38a shows that the deterministic current $i_{o}$ flows out of node 9 and into node 10, the polarities of the noise currents are not known, and the mean-square noise contributions add because the noise sources are uncorrelated with each other. Therefore, the total mean-square output current density stemming from the active loads attached to both nodes 9 and 10 is

$$
\begin{equation*}
\frac{\overline{i_{o A B}^{2}}}{\Delta f}=2\left(\frac{\overline{i_{o A}^{2}}}{\Delta f}+\frac{\overline{i_{o B}^{2}}}{\Delta f}\right) \tag{11.112}
\end{equation*}
$$

This result can be referred back to the input of the complete circuit of Fig. 11.38a in the standard manner. Consider the contribution to the equivalent input noise voltage. A voltage applied at the input of the full circuit of Fig. 11.38a gives

$$
\frac{i_{o}}{v_{i d}}=G_{m 1}
$$

where $G_{m 1}=97 \mu \mathrm{~A} / \mathrm{V}$ from (6.186). Therefore,

$$
\begin{equation*}
\overline{i_{o}^{2}}=G_{m 1}^{2} \overline{v_{i d}^{2}} \tag{11.113}
\end{equation*}
$$

Equating output noise current in (11.112) and (11.113), we obtain an equivalent input noise voltage due to the active loads as

$$
\begin{equation*}
\frac{\overline{v_{i A B}^{2}}}{\Delta f}=4 k T\left[2\left(\frac{35,000}{37,000^{2}}+\frac{25,000}{26,000^{2}}\right)\right]\left(\frac{1}{97 \times 10^{-6}}\right)^{2}=4 k T(13,000) \tag{11.114}
\end{equation*}
$$

Thus the active load causes a contribution of $13 \mathrm{k} \Omega$ to the equivalent input noise resistance of the NE5234 op amp. Finally, the results of Section 11.7.3 show that the equivalent input noise voltage squared of the differential pair $Q_{3}-Q_{4}$ is just the sum of the values from each half of the circuit. This gives an input noise-voltage contribution due to $Q_{3}-Q_{4}$ of

$$
\begin{equation*}
\frac{\overline{v_{i C}^{2}}}{\Delta f}=4 k T\left(\frac{1}{2 g_{m 3}}+\frac{1}{2 g_{m 4}}+r_{b 3}+r_{b 4}\right) \tag{11.115}
\end{equation*}
$$

Assuming a collector bias current of $3 \mu \mathrm{~A}$ for each device, and $r_{b}=200 \Omega$ in (11.115), we calculate

$$
\begin{equation*}
\frac{\overline{v_{i C}^{2}}}{\Delta f}=4 k T(9,000) \tag{11.116}
\end{equation*}
$$

image_name:Figure 11.39 Complete op amp noise representation
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vip, Nn: Ip(A0)}
name: Ii, type: CurrentSource, value: Ii, ports: {Np: Ip(A0), Nn: GND}
name: A0, type: OpAmp, value: A0, ports: {InP: Ip(A0), InN: In(A0), OutP: Vo, OutN: GND}
]
extrainfo:The circuit diagram represents a complete op amp noise model with a voltage source 'Vi' at the positive input and a current source 'Ii' connected to ground. The op amp 'A0' amplifies the input signal with its output at 'Vo'.

Figure 11.39 Complete op amp noise representation.

For the total input noise voltage of the NE5234, combining (11.114) and (11.116) gives

$$
\begin{equation*}
\frac{\overline{v_{i}^{2}}}{\Delta f}=\frac{\overline{v_{i A B}^{2}}}{\Delta f}+\frac{\overline{v_{i C}^{2}}}{\Delta f}=4 k T(22,000) \tag{11.117}
\end{equation*}
$$

Thus the input noise voltage of the NE5234 is represented by an equivalent input noise resistance of $22 \mathrm{k} \Omega$. This is a large value and is close to the measured and computer-calculated result. Note that the active load is the main contributor to the noise. The magnitude of the noise voltage can be appreciated by noting that if this op amp is fed from a $1-\mathrm{k} \Omega$ source resistance for example, the circuit adds twenty-two times as much noise power as is contributed by the source resistance itself.

The calculations above concerned the equivalent input noise voltage of the NE5234. A similar calculation performed to determine the equivalent input noise current shows that it is dominated by the base current of the input device. The current gain of the input differential pair is sufficient to ensure that following stage noise, including noise in the active loads, gives a negligible contribution to input current noise. Since the circuit is differential, the complete noise representation consists of the equivalent input noise voltage calculated above plus two equivalent input noise-current generators as shown in Fig. 11.39. This follows from the discussion of differential-pair noise performance in Section 11.7.3. The equivalent input noise-current generators are (neglecting flicker noise)

$$
\frac{\overline{i_{i}^{2}}}{\Delta f} \simeq 2 q I_{B}
$$

where $I_{B}$ is the base current of $Q_{1}$ or $Q_{2}$ in Fig. 11.38a. With $\beta_{F(p n p)}=10$,

$$
\begin{equation*}
\frac{\overline{i_{i}^{2}}}{\Delta f} \simeq 2 q\left(0.3 \times 10^{-6}\right) \tag{11.118}
\end{equation*}
$$

Increasing $\beta_{F}$ reduces the input mean-square current noise. When $V_{I C} \gg 0.8 \mathrm{~V}$, the input stage of the NE5234 turns off $Q_{3}{ }^{-} Q_{4}$ and turns on $Q_{1-} Q_{2}$ with the same collector bias currents as assumed above. Therefore, the input mean-square current density depends on $V_{I C}$ unless $\beta_{F(n p n)}=\beta_{F(p n p)}$.

Consider the case of the CMOS input stage shown in Fig. 11.40. If the noise in each MOS transistor is represented as shown by its equivalent input noise voltage generator, the equivalent input noise voltage of the circuit $\frac{1}{v_{\mathrm{eq} T}^{2}}$ can be calculated by equating the output current noise
image_name:(a)
description:
[
name: M1, type: PMOS, ports: {S: X2, D: X1, G: GND}
name: M2, type: PMOS, ports: {S: X2, D: C2C4, G: GND}
name: M3, type: NMOS, ports: {S: -VSS, D: X1, G: X1}
name: M4, type: NMOS, ports: {S: -VSS, D: C2C4, G: X1}
name: VDD, type: VoltageSource, ports: {Np: VDD, Nn: X2}
]
extrainfo:The circuit is a CMOS input stage with noise contributions from each MOS transistor represented by equivalent input noise voltage generators. The circuit includes two PMOS transistors (M1, M2) connected to a common power supply node (X2) and two NMOS transistors (M3, M4) connected to a common ground (-VSS). The equivalent input noise voltage is calculated by combining the noise contributions of each transistor.
image_name:(b)
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: c1b3b4, G: GND}
name: M2, type: PMOS, ports: {S: VDD, D: GND, G: c2c4}
name: M3, type: NMOS, ports: {S: -VSS, D: c1b3b4, G: c1b3b4}
name: M4, type: NMOS, ports: {S: -VSS, D: c2c4, G: c1b3b4}
name: VDD, type: CurrentSource, value: VDD, ports: {Np: VDD, Nn: c1b3b4}
]
extrainfo:This circuit is a CMOS input stage with noise contributions. It includes PMOS transistors M1 and M2, and NMOS transistors M3 and M4. The circuit is powered by a current source VDD. The input noise is represented by equivalent input noise voltage sources.

Figure 11.40 (a) CMOS input stage device noise contributions. (b) Equivalent input noise representation.
$\overline{i_{o}^{2}}$ for the circuits in Fig. 11.40a and Fig. 11.40b giving

$$
\begin{equation*}
\overline{v_{\mathrm{eq} T}^{2}}=\overline{v_{\mathrm{eq} 1}^{2}}+\overline{v_{\mathrm{eq} 2}^{2}}+\left(\frac{g_{m 3}}{g_{m 1}}\right)^{2}\left(\overline{v_{\mathrm{eq} 3}^{2}}+\overline{v_{\mathrm{eq} 4}^{2}}\right) \tag{11.119}
\end{equation*}
$$

where it has been assumed that $g_{m 1}=g_{m 2}$ and that $g_{m 3}=g_{m 4}$. Thus, the input transistors contribute to the input noise directly while the contribution of the loads is reduced by the square of the ratio of their transconductance to that of the input transistors. The significance of this in the design can be further appreciated by considering the input-referred $1 / f$ noise and the input-referred thermal noise separately.

The dependence of the $1 / f$ portion of the device equivalent input noise-voltage spectrum on device geometry and bias conditions was considered earlier. Considerable discrepancy exists in the published data on $1 / f$ noise, indicating that it arises from a mechanism that is strongly affected by details of device fabrication. The most widely accepted model for $1 / f$ noise is that, for a given device, the gate-referred equivalent mean-square voltage noise is approximately independent of bias conditions in saturation and is inversely proportional to the gate capacitance of the device. The following analytical results are based on this model, but it should be emphasized that the actual dependence must be verified for each process technology and device type. Thus we let

$$
\begin{equation*}
\overline{v_{\mathrm{eq}}^{2}}=\frac{K_{f} \Delta f}{C_{o x} W L f} \tag{11.120}
\end{equation*}
$$

where the parameter $K_{f}$ is the flicker-noise coefficient. Utilizing this assumption, and using (11.119), we obtain for the equivalent input $1 / f$ noise generator for the circuit of Fig. 11.40a

$$
\begin{equation*}
\overline{v_{1 / f}^{2}}=\frac{2 K_{p}}{f W_{1} L_{1} C_{o x}}\left(1+\frac{K_{n} \mu_{n} L_{1}^{2}}{K_{p} \mu_{p} L_{3}^{2}}\right) \Delta f \tag{11.121}
\end{equation*}
$$

where $K_{n}$ and $K_{p}$ are the flicker noise coefficients for the $n$-channel and $p$-channel devices, respectively. Depending on processing details, these may be comparable or different by a factor of two or more. Note that the first term in (11.121) is the equivalent input noise of the input transistors alone, and the term in parentheses is the increase in noise over and above this value due to the loads. The second term shows that the load contribution can be made small by simply making the channel lengths of the loads longer than those of the input transistors by a factor of about two or more. The input transistors can then be made wide enough to achieve the desired performance. It is interesting to note that changing the width of the channel in the loads does not effect the $1 / f$ noise performance.

The thermal noise performance of the circuit of Fig. 11.40a can be calculated as follows. As discussed in Section 11.5.2, the input-referred thermal noise of a MOS transistor is given by

$$
\begin{equation*}
\overline{v_{\mathrm{eq}}^{2}}=4 k T\left(\frac{2}{3 g_{m}}\right) \Delta f \tag{11.122}
\end{equation*}
$$

Utilizing the same approach as for the flicker noise, we obtain for the equivalent input thermal noise of the circuit of Fig. 11.40a

$$
\begin{equation*}
\overline{v_{\mathrm{Th}}^{2}}=4 k T \frac{4}{3 \sqrt{2 \mu_{p} C_{o x}(W / L)_{1} I_{D}}}\left(1+\sqrt{\frac{\mu_{n}(W / L)_{3}}{\mu_{p}(W / L)_{1}}}\right) \Delta f \tag{11.123}
\end{equation*}
$$

where $I_{D}$ is the bias current in each device. Again, the first term represents the thermal noise from the input transistors and the term in parentheses represents the fractional increase in noise due to the loads. The term in parentheses will be small if the $W / L$ ratios are chosen so that the
transconductance of the input devices is much larger than that of the loads. If this condition is satisfied, then the input noise is simply determined by the transconductance of the input transistors.

## 11.9 Noise Bandwidth

In the noise analysis performed thus far, the circuits considered were generally assumed to have simple gain-frequency characteristics with abrupt band edges as shown in Fig. 11.33b. The calculation of total circuit noise then reduced to an integration of the noise spectral density across this band. In practice, many circuits do not have such ideal gain-frequency characteristics, and the calculation of total circuit noise can be much more complex in those cases. However, if the equivalent input noise spectral density of a circuit is constant and independent of frequency (i.e., if the noise is white), we can simplify the calculations using the concept of noise bandwidth described below.

Consider an amplifier as shown in Fig. 11.41, and assume it is fed from a low source impedance so that the equivalent input noise voltage $\overline{v_{i}^{2}}$ determines the noise performance. Assume initially that the spectral density $\overline{v_{i}^{2}} / \Delta f=S_{i}(f)=S_{i 0}$ of the input noise voltage is flat as shown in Fig. 11.42a. Further assume that the magnitude squared of the voltage gain $\left|A_{v}(\mathrm{jf})\right|^{2}$ of the circuit is as shown in Fig. 11.42b. The output noise-voltage spectral density $S_{o}(f)=\overline{v_{o}^{2}} / \Delta f$ is the product of the input noise-voltage spectral density and the square of the voltage gain and is shown in Fig. 11.42c. The total output noise voltage is obtained by summing the contribution from $S_{o}(f)$ in each frequency increment $\Delta f$ between zero and infinity to give

$$
\begin{align*}
\overline{v_{o T}^{2}} & =\sum_{f=0}^{\infty} S_{o}(f) \Delta f=\int_{0}^{\infty} S_{o}(f) d f=\int_{0}^{\infty}\left|A_{v}(j f)^{2}\right| S_{i 0} d f \\
& =S_{i 0} \int_{0}^{\infty}\left|A_{v}(j f)\right|^{2} d f \tag{11.124}
\end{align*}
$$

The evaluation of the integral of (11.124) is often difficult except for very simple transfer functions. However, if the problem is transformed into a normalized form, the integrals of common circuit functions can be evaluated and tabulated for use in noise calculations. For this purpose, consider a transfer function as shown in Fig. 11.43 with the same low-frequency value $A_{v 0}$ as the original circuit but with an abrupt band edge at a frequency $f_{N}$. Frequency $f_{N}$ is chosen to give the same total output noise voltage as the original circuit when the same input noise voltage is applied. Thus

$$
\begin{equation*}
\overline{v_{o T}^{2}}=S_{i 0} A_{v 0}^{2} f_{N} \tag{11.125}
\end{equation*}
$$

If (11.124) and (11.125) are equated, we obtain

$$
\begin{equation*}
f_{N}=\frac{1}{A_{v 0}^{2}} \int_{0}^{\infty}\left|A_{v}(j f)\right|^{2} d f \tag{11.126}
\end{equation*}
$$

image_name:Figure 11.41 Circuit with equivalent input noise voltage generator
description:
[
name: vi/2, type: VoltageSource, ports: {Np: Vin, Nn: GND}
]
extrainfo:The circuit in Figure 11.41 includes an equivalent input noise voltage generator represented by a voltage source labeled vi/2. The output is connected to vo, with positive and negative terminals indicated.

Figure 11.41 Circuit with equivalent input noise voltage generator.
image_name:(a)
description:The graph labeled (a) represents the equivalent input noise-voltage spectral density. It is a plot of $S_i(f)$, which is defined as the noise spectral density, against frequency $f$. The vertical axis is labeled $S_i(f) = \frac{\overline{v_i^2}}{\Delta f}$ and is measured in units of $V^2/Hz$, while the horizontal axis represents frequency $f$ on a logarithmic scale.

This graph is a horizontal line indicating a constant spectral density $S_{i0}$ across all frequencies. The line suggests that the noise power per unit bandwidth is uniform over the frequency range shown. There are no peaks, valleys, or other features; the line remains flat, implying no frequency dependency in the spectral density within the range of interest.
image_name:(b)
description:The graph labeled (b) is a Bode plot representing the squared magnitude of the circuit's transfer function. It is plotted on a logarithmic scale on both axes. The horizontal axis represents frequency (f) in a logarithmic scale, while the vertical axis represents the squared magnitude of the transfer function |A_v(jf)|^2, also in a logarithmic scale.

Overall Behavior and Trends:
- The graph starts with a flat region, indicating a constant squared magnitude at low frequencies. This region is characterized by a high and constant value, represented by A_v0^2, which is the squared gain of the circuit.
- As the frequency increases, the graph shows a downward slope starting at a certain cutoff frequency, labeled f_1. This indicates a decrease in the squared magnitude of the transfer function, suggesting a roll-off behavior typical of a low-pass filter.

Key Features and Technical Details:
- **Flat Region:** The initial flat section of the graph indicates that the circuit maintains a constant gain up to the cutoff frequency f_1.
- **Cutoff Frequency (f_1):** This is the frequency at which the graph begins to slope downwards, marking the transition from the passband to the stopband.
- **Slope:** Beyond f_1, the graph exhibits a roll-off, which is typical for filters, indicating a reduction in gain as frequency increases.

Annotations and Specific Data Points:
- The graph is annotated with A_v0^2, representing the squared gain in the passband.
- The cutoff frequency f_1 is marked with a vertical dashed line, highlighting the transition point where the gain begins to decrease.

This Bode plot (b) effectively illustrates the frequency response of the circuit, showing how it attenuates signals beyond a certain frequency, characteristic of a low-pass filter behavior.
image_name:(c)
description:The graph labeled (c) is a plot of the output noise-voltage spectral density, denoted as \( S_o(f) \), against frequency \( f \). This is a log-log plot, with both axes on a logarithmic scale.

1. **Axes Labels and Units:**
- The vertical axis represents the spectral density \( S_o(f) = \frac{\overline{v_o^2}}{\Delta f} \), measured in \( \text{V}^2/\text{Hz} \).
- The horizontal axis represents frequency \( f \), with a logarithmic scale.

2. **Overall Behavior and Trends:**
- The graph shows a flat region at lower frequencies, indicating a constant noise spectral density.
- As the frequency increases, there is a noticeable roll-off starting at a critical frequency \( f_1 \), where the spectral density begins to decrease.
- The curve exhibits a slope after \( f_1 \), suggesting a reduction in noise spectral density with increasing frequency.

3. **Key Features and Technical Details:**
- The flat portion of the curve at low frequencies represents the maximum output noise spectral density, characterized by \( A_v^2 S_{i0} \), where \( A_v^2 \) is the squared magnitude of the transfer function at low frequencies and \( S_{i0} \) is the input noise spectral density.
- The roll-off point \( f_1 \) is marked by a vertical dashed line, indicating the frequency at which the spectral density begins to decline.
- The slope beyond \( f_1 \) indicates the rate at which the output noise spectral density decreases.

4. **Annotations and Specific Data Points:**
- The graph includes annotations such as \( A_v^2 S_{i0} \) and \( f_1 \), which are critical to understanding the behavior of the output noise spectral density.
- These annotations help identify the key transition points and values in the graph, providing insight into the circuit's noise performance across different frequencies.

Figure 11.42 Assumed parameters for the circuit of Fig. 11.41. (a) Equivalent input noise-voltage spectral density. (b) Circuit transfer function squared. (c) Output noise-voltage spectral density.
image_name:Figure 11.43
description:The graph depicted in Figure 11.43 is a plot of the squared magnitude of a transfer function, \(|A_v(jf)|^2\), versus frequency \(f\). This is a frequency response graph commonly used in analyzing the behavior of circuits in the frequency domain.

Axes Labels and Units:
- The **horizontal axis** represents frequency \(f\), typically measured in hertz (Hz).
- The **vertical axis** represents the squared magnitude of the transfer function, \(|A_v(jf)|^2\).

Overall Behavior and Trends:
- The graph is characterized by a flat, constant region followed by a sharp drop to zero. This indicates a passband with constant gain followed by a cutoff frequency where the gain drops to zero.
- The flat region extends from the origin to the cutoff frequency \(f_N\), where the squared magnitude is constant at a value of \(A_v^2\).

Key Features and Technical Details:
- The **passband** is represented by the horizontal line where the gain is \(A_v^2\), indicating that within this range of frequencies, the circuit has a uniform response.
- The **cutoff frequency** is marked at \(f_N\), where the transfer function magnitude abruptly drops to zero, indicating the end of the passband.
- There are no peaks, valleys, or oscillations in this graph, signifying a simple low-pass filter characteristic.

Annotations and Specific Data Points:
- The graph is annotated with \(A_v^2\) at the height of the passband, highlighting the constant gain level.
- The cutoff frequency \(f_N\) is labeled on the frequency axis, marking the boundary between the passband and the stopband.

This graph effectively illustrates a simple filter with a flat response up to a certain frequency, beyond which the response drops to zero, typical of an idealized low-pass filter behavior in frequency domain analysis.

Figure 11.43 Transfer function of a circuit giving the same output noise as a circuit with a transfer function as specified in Fig. 11.42b.
where $f_{N}$ is the equivalent noise bandwidth of the circuit. Although derived for the case of a voltage transfer function, this result can be used for any type of transfer function. Note that the integration of (11.126) can be performed numerically if measured data for the circuit transfer function is available.

Once the noise bandwidth is evaluated using (11.126), the total output noise of the circuit is readily calculated using (11.125). The advantage of the form of (11.126) is that the circuit gain is normalized to its low-frequency value and thus the calculation of $f_{N}$ concerns only the frequency response of the circuit. This can be done in a general way so that whole classes of circuits are covered by one calculation. For example, consider an amplifier with a single-pole frequency response given by

$$
\begin{equation*}
A_{\nu}(j f)=\frac{A_{v 0}}{1+j \frac{f}{f_{1}}} \tag{11.127}
\end{equation*}
$$

where $f_{1}$ is the $-3-\mathrm{dB}$ frequency. The noise bandwidth of this circuit can be calculated from (11.126) as

$$
\begin{equation*}
f_{N}=\int_{0}^{\infty} \frac{d f}{1+\left(\frac{f}{f_{1}}\right)^{2}}=\frac{\pi}{2} f_{1}=1.57 f_{1} \tag{11.128}
\end{equation*}
$$

This gives the noise bandwidth of any single-pole circuit and shows that it is larger than the $-3-\mathrm{dB}$ bandwidth by a factor of 1.57 . Thus a circuit with the transfer function of (11.127) produces noise as if it had an abrupt band edge at a frequency $1.57 f_{1}$.

As the steepness of the transfer function fall-off with frequency becomes greater, the noise bandwidth approaches the $-3-\mathrm{dB}$ bandwidth. For example, a two-pole transfer function with complex poles at $45^{\circ}$ to the negative real axis has a noise bandwidth only 11 percent greater than the $-3-\mathrm{dB}$ bandwidth.

#### EXAMPLE

As an example of noise bandwidth calculations, suppose a NE5234 op amp is used in a feedback configuration with a low-frequency gain of $A_{\nu 0}=100$ and it is desired to calculate the total output noise $v_{O T}$ from the circuit with a zero source impedance and neglecting flicker noise. If the unity-gain bandwidth of the op amp is 2.7 MHz , then the transfer function in a gain of 100 configuration will have a -3-dB frequency of 27 kHz with a single-pole response. From (11.128) the noise bandwidth is

$$
\begin{equation*}
f_{N}=1.57 \times 27 \mathrm{kHz}=42 \mathrm{kHz} \tag{11.129}
\end{equation*}
$$

Assuming that the circuit is fed from a zero source impedance, and using the previously calculated value of $22 \mathrm{k} \Omega$ as the equivalent input noise resistance, we can calculate the lowfrequency input noise voltage spectral density of the NE5234 as

$$
\begin{equation*}
S_{i 0}=\frac{\overline{v_{i}^{2}}}{\Delta f}=4 k T(22,000)=3.7 \times 10^{-16} \mathrm{~V}^{2} / \mathrm{Hz} \tag{11.130}
\end{equation*}
$$

Using $A_{v 0}=100$ together with substitution of (11.129) and (11.130) in (11.125) gives, for the total output noise voltage,

$$
\overline{v_{o T}^{2}}=3.7 \times 10^{-16} \times(100)^{2} \times 42 \times 10^{3} \mathrm{~V}^{2}=1.6 \times 10^{-7} \mathrm{~V}^{2}
$$

- $\quad$ and thus $v_{O T}=390 \mu \mathrm{~V}$ rms.

The calculations of noise bandwidth considered above were based on the assumption of a flat input noise spectrum. This is often true in practice and the concept of noise bandwidth is useful in those cases, but there are also many examples where the input noise spectrum varies
with frequency. In these cases, the total output noise voltage is given by

$$
\begin{align*}
\overline{v_{o T}^{2}} & =\int_{0}^{\infty} S_{o}(f) d f  \tag{11.131}\\
& =\int_{0}^{\infty}\left|A_{v}(j f)\right|^{2} S_{i}(f) d f \tag{11.132}
\end{align*}
$$

where $A_{v}(j f)$ is the voltage gain of the circuit and $S_{i}(f)$ is the input noise-voltage spectral density. If the circuit has a voltage gain $A_{v S}$ at the frequency of the applied input signal, then the total equivalent input noise voltage becomes

$$
\begin{align*}
\overline{v_{i T}^{2}} & =\frac{1}{A_{v S}^{2}} \int_{0}^{\infty}\left|A_{v}(j f)\right|^{2} S_{i}(f) d f  \tag{11.133}\\
& =\int_{0}^{\infty}\left|\frac{A_{v}(j f)}{A_{v S}}\right|^{2} S_{i}(f) d f \tag{11.134}
\end{align*}
$$

Equation 11.134 shows that, in general, the total equivalent input noise voltage of a circuit is obtained by integrating the product of the input noise-voltage spectrum and the normalized voltage gain function.

One last topic that should be mentioned in this section is the problem that occurs in calculating the flicker noise in direct-coupled amplifiers. Consider an amplifier with an input noise spectral density as shown in Fig. 11.44a and a voltage gain that extends down to dc and up to $f_{1}=10 \mathrm{kHz}$ with an abrupt cutoff, as shown in Fig. 11.44b. Then, using (11.134), we
image_name:(a)
description:1. **Type of Graph and Function:**
- The graph is a plot of the input noise-voltage spectral density, denoted as \( S_i(f) \), against frequency, \( f \). This is typically known as a noise spectral density plot.

2. **Axes Labels and Units:**
- The x-axis represents frequency \( f \) in hertz (Hz), ranging from 10 Hz to 10 kHz.
- The y-axis represents the noise spectral density \( S_i(f) \) in \( \text{V}^2/\text{Hz} \), with a logarithmic scale ranging from \( 10^{-17} \) to \( 10^{-14} \) \( \text{V}^2/\text{Hz} \).

3. **Overall Behavior and Trends:**
- The graph exhibits a decreasing trend, starting at a higher noise spectral density at lower frequencies and gradually decreasing as the frequency increases.
- The curve shows a characteristic \( 1/f \) noise behavior, which is common in electronic noise spectra.

4. **Key Features and Technical Details:**
- The plot starts at a noise spectral density slightly above \( 10^{-14} \) \( \text{V}^2/\text{Hz} \) at around 10 Hz and decreases towards \( 10^{-16} \) \( \text{V}^2/\text{Hz} \) as it approaches 1 kHz.
- Beyond 1 kHz, the spectral density levels off and remains constant at \( 10^{-16} \) \( \text{V}^2/\text{Hz} \) up to 10 kHz.
- A dashed line indicates the \( 1/f \) slope, emphasizing the initial decline in noise density.

5. **Annotations and Specific Data Points:**
- The graph is annotated with a \( 1/f \) label, indicating the inverse relationship between frequency and noise density in the initial part of the spectrum.
- The transition from a decreasing trend to a flat response occurs around 1 kHz, marking a significant change in the behavior of the noise spectral density.

(a)
image_name:(b) Circuit transfer function squared
description:The graph is a Bode plot representing the squared magnitude of the circuit transfer function, \(|A(jf)|^2\), as a function of frequency \(f\) in hertz (Hz). The x-axis is logarithmically scaled, spanning frequencies from 10 Hz to 10 kHz, while the y-axis represents the squared magnitude of the transfer function on a linear scale, ranging from 1 to 100.

**Overall Behavior and Trends:**
- The graph shows a flat response at a magnitude of 100 for frequencies between 10 Hz and 10 kHz. This indicates that the transfer function maintains a constant gain of 100 squared over this frequency range.
- At 10 kHz, there is a sharp transition where the squared magnitude drops to 1, indicating a significant decrease in gain beyond this frequency.

**Key Features and Technical Details:**
- The graph features a plateau at \(|A(jf)|^2 = 100\) from 10 Hz to 10 kHz, suggesting a wide bandwidth where the circuit maintains a consistent gain.
- The sharp drop at 10 kHz marks the cutoff frequency, beyond which the gain decreases rapidly.

**Annotations and Specific Data Points:**
- The plot does not include additional annotations or markers, but the critical points are the constant magnitude of 100 up to 10 kHz and the drop to 1 at 10 kHz.

(b)

Figure 11.44 (a) Input noise-voltage spectral density for a circuit. (b) Circuit transfer function squared.
can calculate the total equivalent input noise voltage as

$$
\begin{align*}
\overline{v_{i T}^{2}} & =\int_{0}^{f_{1}} S_{i}(f) d f \\
& =\int_{0}^{f_{1}}\left(1+\frac{1000}{f}\right) \times 10^{-16} d f \\
& =10^{-16}[f+1000 \ln f]_{0}^{f_{1}} \tag{11.135}
\end{align*}
$$

Evaluating (11.135) produces a problem since $\overline{v_{i T}^{2}}$ is infinite when a lower limit of zero is used on the integration. This suggests infinite power in the $1 / f$ noise signal. In practice, measurements of $1 / f$ noise spectra show a continued $1 / f$ dependence to as low a frequency as is measured (cycles per day or less). This problem can be resolved only by noting that $1 / f$ noise eventually becomes indistinguishable from thermal drift and that the lower limit of the integration must be specified by the period of observation. For example, taking a lower limit to the integration of $f_{2}=1$ cycle/day, we have $f_{2}=1.16 \times 10^{-5} \mathrm{~Hz}$. Changing the limit in (11.135) we find

$$
\begin{align*}
\overline{v_{i T}^{2}} & =10^{-16}[f+1000 \ln f]_{f_{2}}^{f_{1}} \\
& =10^{-16}\left[\left(f_{1}-f_{2}\right)+1000 \ln \frac{f_{1}}{f_{2}}\right] \tag{11.136}
\end{align*}
$$

Using $f_{1}=10 \mathrm{kHz}$ and $f_{2}=1.16 \times 10^{-5} \mathrm{~Hz}$ in (11.136) gives

$$
\begin{aligned}
\overline{v_{i T}^{2}} & =10^{-16}(10,000+20,600) \\
& =3.06 \times 10^{-12} \mathrm{~V}^{2}
\end{aligned}
$$

and thus

$$
v_{i T}=1.75 \mu \mathrm{~V} \mathrm{rms}
$$

If the lower limit of integration is changed to 1 cycle/year $=3.2 \times 10^{-8} \mathrm{~Hz}$, then (11.136) becomes

$$
\begin{aligned}
\overline{v_{i T}^{2}} & =10^{-16}(10,000+26,500) \\
& =3.65 \times 10^{-12} \mathrm{~V}^{2}
\end{aligned}
$$

and thus

$$
v_{i T}=1.9 \mu \mathrm{~V} \mathrm{rms}
$$

The noise voltage changes very slowly as $f_{2}$ is reduced further because of the $\ln$ function in (11.136).

### 11.10 Noise Figure and Noise Temperature

### 11.10.1 Noise Figure

The most general method of specifying the noise performance of circuits is by specifying input noise generators as described above. However, a number of specialized methods of specifying noise performance have been developed that are convenient in particular situations. Two of these methods are now described.
image_name:Figure 11.45 Signal and noise power at the input and output of a circuit.
description:The diagram labeled "Figure 11.45 Signal and noise power at the input and output of a circuit" illustrates a simple block representation of a circuit's noise performance. It contains the following components and flow of information:

1. **Main Components:**
- **Circuit Block:** This is the central component of the diagram, representing the entire circuit whose noise performance is being analyzed.

2. **Flow of Information or Control:**
- **Input Signals:** On the left side of the circuit block, there are two input signals labeled \( S_i \) and \( N_i \). Here, \( S_i \) represents the signal power at the input, and \( N_i \) represents the noise power at the input.
- **Output Signals:** On the right side of the circuit block, there are two output signals labeled \( S_o \) and \( N_o \). \( S_o \) denotes the signal power at the output, and \( N_o \) denotes the noise power at the output.
- The diagram indicates that both signal and noise power are processed by the circuit, with inputs entering from the left and outputs exiting from the right.

3. **Labels, Annotations, and Key Indicators:**
- The labels \( S_i, N_i, S_o, N_o \) clearly indicate the respective signal and noise power levels at the input and output of the circuit.

4. **Overall System Function:**
- The primary function of the system depicted in this diagram is to illustrate the transformation of signal and noise power as they pass through the circuit. This transformation is crucial for understanding the circuit's noise figure, which is a measure of how much noise the circuit adds to the signal as it processes it. The diagram serves to conceptualize how input signal and noise are altered by the circuit, resulting in specific output signal and noise levels, thereby providing insight into the circuit's noise performance.

Figure 11.45 Signal and noise power at the input and output of a circuit.

The noise figure $(F)$ is a commonly used method of specifying the noise performance of a circuit or a device. Its disadvantage is that it is limited to situations where the source impedance is resistive, and this precludes its use in many applications where noise performance is important. However, it is widely used as a measure of noise performance in communication systems where the source impedance is often resistive.

The definition of the noise figure of a circuit is

$$
\begin{equation*}
F=\frac{\text { input } S / N \text { ratio }}{\text { output } S / N \text { ratio }} \tag{11.137}
\end{equation*}
$$

and $F$ is usually expressed in decibels. The utility of the noise-figure concept is apparent from the definition, as it gives a direct measure of the signal-to-noise $(S / N)$ ratio degradation that is caused by the circuit. For example, if the $S / N$ ratio at the input to a circuit is 50 dB , and the circuit noise figure is 5 dB , then the $S / N$ ratio at the output of the circuit is 45 dB .

Consider a circuit as shown in Fig. 11.45, where $S$ represents signal power and $N$ represents noise power. The input noise power $N_{i}$ is always taken as the noise in the source resistance. The output noise power $N_{o}$ is the total output noise including the circuit contribution and noise transmitted from the source resistance. From (11.137) the noise figure is

$$
\begin{equation*}
F=\frac{S_{i}}{N_{i}} \frac{N_{o}}{S_{o}} \tag{11.138}
\end{equation*}
$$

For an ideal noiseless amplifier, all output noise comes from the source resistance at the input, and thus if $G$ is the circuit power gain, then the output signal $S_{o}$ and the output noise $N_{o}$ are given by

$$
\begin{align*}
& S_{o}=G S_{i}  \tag{11.139}\\
& N_{o}=G N_{i} \tag{11.140}
\end{align*}
$$

Substituting (11.139) and (11.140) in (11.138) gives $F=1$ or 0 dB in this case.
A useful alternative definition of $F$ may be derived from (11.138) as follows:

$$
\begin{equation*}
F=\frac{S_{i}}{N_{i}} \frac{N_{o}}{S_{o}}=\frac{N_{o}}{G N_{i}} \tag{11.141}
\end{equation*}
$$

Equation 11.141 can be written as

$$
\begin{equation*}
F=\frac{\text { total output noise }}{\text { that part of the output noise due to the source resistance }} \tag{11.142}
\end{equation*}
$$

Note that since $F$ is specified by a power ratio, the value in decibels is given by $10 \log _{10}$ (numerical ratio).

The calculations of the previous sections have shown that the noise parameters of most circuits vary with frequency, and thus the bandwidth must be specified when the noise figure of a circuit is calculated. The noise figure is often specified for a small bandwidth $\Delta f$ at a frequency $f$ where $\Delta f \ll f$. This is called the spot noise figure and applies to tuned amplifiers and also to broadband amplifiers that may be followed by frequency-selective circuits. For broadband amplifiers whose output is utilized over a wide bandwidth, an average noise figure is often
image_name:Figure 11.46 Equivalent input noise representation for the calculation of noise figure.
description:
[
name: isignal, type: CurrentSource, value: isignal, ports: {Np: Vi, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vi, N2: GND}
name: zi, type: Resistor, value: zi, ports: {N1: Vx, N2: GND}
name: Gvx, type: VoltageControlledVoltageSource, value: Gvx, ports: {Np: Vo, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is designed for calculating the noise figure using an equivalent input noise representation. It includes a current source for signal input, resistors for impedance, and a voltage-controlled voltage source for output voltage control.

Figure 11.46 Equivalent input noise representation for the calculation of noise figure.
specified. This requires calculation of the total output noise over the frequency band of interest using the methods described in previous sections.

In many cases, the most convenient way to calculate noise figure is to return to the original equivalent circuit of the device with its basic noise generators to perform the calculation. However, some insight into the effect of circuit parameters on the noise figure can be obtained by using the equivalent input noise generator representation of Fig. 11.46. In this figure, a circuit with input impedance $z_{i}$ and voltage gain $G=v_{o} / v_{x}$ is fed from a source resistance $R_{S}$ and drives a load $R_{L}$. The source resistance shows thermal noise $\overline{i_{s}^{2}}$, and the noise of the circuit itself is represented by $\overline{i_{i}^{2}}$ and $\overline{v_{i}^{2}}$, assumed uncorrelated. The noise at the input terminals due to $\overline{v_{i}^{2}}$ and $\overline{i_{i}^{2}}$ is

$$
v_{x A}=v_{i} \frac{z_{i}}{z_{i}+R_{S}}+i_{i} \frac{R_{S} z_{i}}{R_{S}+z_{i}}
$$

and thus

$$
\begin{equation*}
\overline{v_{x A}^{2}}=\overline{v_{i}^{2}} \frac{\left|z_{i}\right|^{2}}{\left|z_{i}+R_{S}\right|^{2}}+\overline{i_{i}^{2}} \frac{\left|R_{S} z_{i}\right|^{2}}{\left|R_{S}+z_{i}\right|^{2}} \tag{11.143}
\end{equation*}
$$

The noise power in $R_{L}$ produced by $\overline{v_{i}^{2}}$ and $\overline{i_{i}^{2}}$ is

$$
\begin{equation*}
N_{o A}=\frac{|G|^{2}}{R_{L}} \overline{v_{x A}^{2}}=\frac{|G|^{2}}{R_{L}}\left(\overline{v_{i}^{2}} \frac{\left|z_{i}\right|^{2}}{\left|z_{i}+R_{S}\right|^{2}}+\overline{i_{i}^{2}} \frac{\left|R_{S} z_{i}\right|^{2}}{\left|R_{S}+z_{i}\right|^{2}}\right) \tag{11.144}
\end{equation*}
$$

The noise power in $R_{L}$ produced by source resistance noise generator $\overline{i_{s}^{2}}$ is

$$
\begin{equation*}
N_{o B}=\frac{|G|^{2}}{R_{L}} \frac{\left|R_{S} z_{i}\right|^{2}}{\left|R_{S}+z_{i}\right|^{2}} \overline{i_{s}^{2}} \tag{11.145}
\end{equation*}
$$

The noise in the source resistance in a narrow bandwidth $\Delta f$ is

$$
\begin{equation*}
\overline{i_{s}^{2}}=4 k T \frac{1}{R_{S}} \Delta f \tag{11.146}
\end{equation*}
$$

Substituting (11.146) in (11.145) gives

$$
\begin{equation*}
N_{o B}=\frac{|G|^{2}}{R_{L}} \frac{\left|R_{S} z_{i}\right|^{2}}{\left|R_{S}+z_{i}\right|^{2}} 4 k T \frac{1}{R_{S}} \Delta f \tag{11.147}
\end{equation*}
$$

Using the definition of noise figure in (11.142) and substituting from (11.147) and (11.144), we find

$$
\begin{align*}
F & =\frac{N_{o A}+N_{o B}}{N_{o B}} \\
& =1+\frac{N_{o A}}{N_{o B}}  \tag{11.148}\\
& =1+\frac{\overline{v_{i}^{2}}}{4 k T R_{S} \Delta f}+\frac{\overline{i_{i}^{2}}}{4 k T \frac{1}{R_{S}} \Delta f} \tag{11.149}
\end{align*}
$$

Equation 11.149 gives the circuit spot noise figure assuming negligible correlation between $\overline{v_{i}^{2}}$ and $\overline{i_{i}^{2}}$. Note that $F$ is independent of all circuit parameters $\left(G, z_{i}, R_{L}\right)$ except the source resistance $R_{S}$ and the equivalent input noise generators.

It is apparent from (11.149) that $F$ has a minimum as $R_{S}$ varies. For very low values of $R_{S}$, the $\overline{v_{i}^{2}}$ generator is dominant, whereas for large $R_{S}$ the $\overline{i_{i}^{2}}$ generator is most important. By differentiating (11.149) with respect to $R_{S}$, we can calculate the value of $R_{S}$ giving minimum $F$ :

$$
\begin{equation*}
R_{S(\mathrm{opt})}^{2}=\frac{\overline{v_{i}^{2}}}{\overline{\overline{i_{i}^{2}}}} \tag{11.150}
\end{equation*}
$$

This result is true in general, even if correlation is significant. A graph of $F$ in decibels versus $R_{S}$ is shown in Fig. 11.47.

The existence of a minimum in $F$ as $R_{S}$ is varied is one reason for the widespread use of transformers at the input of low-noise tuned amplifiers. This technique allows the source impedance to be transformed to the value that simultaneously gives the lowest noise figure and causes minimal loss in the circuit.

For example, consider the noise figure of a bipolar transistor at low-to-moderate frequencies, where both flicker noise and high-frequency effects are neglected. From (11.50) and (11.57),

$$
\begin{aligned}
& \overline{v_{i}^{2}}=4 k T\left(r_{b}+\frac{1}{2 g_{m}}\right) \Delta f \\
& \overline{i_{i}^{2}}=2 q I_{B} \Delta f=2 q \frac{I_{C}}{\beta_{F}} \Delta f
\end{aligned}
$$

image_name:Figure 11.47
description:The graph in Figure 11.47 is a plot showing the variation of the noise figure, denoted as **F**, with respect to the source resistance, denoted as **R_S**. This graph is a typical U-shaped curve plotted on a logarithmic scale for the x-axis, representing **R_S**, and a linear scale for the y-axis, representing the noise figure **F** in decibels (dB).

Axes Labels and Units:
- **X-axis (Horizontal):** Represents the source resistance **R_S**, plotted on a logarithmic scale. The axis is labeled as **R_S (log scale)**.
- **Y-axis (Vertical):** Represents the noise figure **F** in decibels (dB).

Overall Behavior and Trends:
The graph exhibits a U-shaped curve indicating that the noise figure **F** decreases to a minimum value at an optimal source resistance, denoted as **R_S(opt)**, and then increases again as the source resistance continues to change. The decrease and increase in the noise figure occur at a rate of 10 dB per decade, as indicated by the annotations on the graph.

Key Features and Technical Details:
- **Minimum Point:** The graph reaches its minimum noise figure at **R_S(opt)**, where the noise figure is optimal.
- **Slope:** The slopes on either side of the minimum point are symmetrical, each with a slope of 10 dB/decade.
- **Annotations:** The graph is annotated with the slope values of 10 dB/decade on both the left and right sides of the curve, highlighting the rate at which the noise figure changes with the source resistance.

Annotations and Specific Data Points:
- **R_S(opt):** A vertical dashed line indicates the position of the optimal source resistance where the noise figure is at its minimum.
- **Symmetry:** The graph is symmetrical around **R_S(opt)**, emphasizing the optimal point for the noise figure.

This graph is crucial for understanding how the noise figure of a bipolar transistor varies with source resistance and helps in designing circuits to achieve minimal noise figure by selecting the appropriate source resistance.

Figure 11.47 Variation in noise figure $F$ with source resistance $R_{S}$.

Substitution of these values in (11.150) gives

$$
\begin{equation*}
R_{S(\mathrm{opt})}=\frac{\sqrt{\beta_{F}}}{g_{m}} \sqrt{1+2 g_{m} r_{b}} \tag{11.151}
\end{equation*}
$$

At this value of $R_{S}$, the noise figure is given by (11.149) as

$$
\begin{equation*}
F_{\mathrm{opt}} \simeq 1+\frac{1}{\sqrt{\beta_{F}}} \sqrt{1+2 g_{m} r_{b}} \tag{11.152}
\end{equation*}
$$

At a collector current of $I_{C}=1 \mathrm{~mA}$, and with $\beta_{F}=100$ and $r_{b}=50 \Omega$, (11.151) gives $R_{S(\mathrm{opt})}=572 \Omega$ and $F_{\text {opt }}=1.22$. In decibels the value is $10 \log _{10} 1.22=0.9 \mathrm{~dB}$. Note that $F_{\text {opt }}$ decreases as $\beta_{F}$ increases and as $r_{b}$ and $g_{m}$ decrease. However, increasing $\beta_{F}$ and decreasing $g_{m}$ result in an increasing value of $R_{S(\mathrm{opt})}$, and this may prove difficult to realize in practice.

As another example, consider the MOSFET at low frequencies. Neglecting flicker noise, we can calculate the equivalent input generators from Section 11.5.2 as

$$
\begin{align*}
& \overline{v_{i}^{2}} \simeq 4 k T \frac{2}{3} \frac{1}{g_{m}} \Delta f  \tag{11.153}\\
& \overline{i_{i}^{2}} \simeq 0 \tag{11.154}
\end{align*}
$$

Using these values in (11.149) and (11.150), we find that $R_{S(\mathrm{opt})} \rightarrow \infty$ and $F_{\mathrm{opt}} \rightarrow 0 \mathrm{~dB}$. Thus the MOS transistor has excellent noise performance from a high source resistance. However, if the source resistance is low (kilohms or less) and transformers cannot be used, the noise figure for the MOS transistor may be worse than for a bipolar transistor. For source resistances of the order of megohms or higher, the MOS transistor usually has significantly lower noise figure than a bipolar transistor.

### 11.10.2 Noise Temperature

Noise temperature is an alternative noise representation and is closely related to noise figure. The noise temperature $T_{n}$ of a circuit is defined as the temperature at which the source resistance $R_{S}$ must be held so that the noise output from the circuit due to $R_{S}$ equals the noise output due to the circuit itself. If these conditions are applied to the circuit of Fig. 11.46, the output noise $N_{O A}$ due to the circuit itself is unchanged but the output noise due to the source resistance becomes

$$
\begin{equation*}
N_{o B}^{\prime}=\frac{|G|^{2}}{R_{L}} \frac{\left|R_{S} z_{i}\right|^{2}}{\left|R_{S}+z_{i}\right|^{2}} 4 k T_{n} \frac{1}{R_{S}} \Delta f \tag{11.155}
\end{equation*}
$$

Substituting for $N_{o B}$ from (11.147) in (11.155), we obtain

$$
\begin{equation*}
N_{o B}^{\prime}=N_{o B} \frac{T_{n}}{T} \tag{11.156}
\end{equation*}
$$

where $T$ is the circuit temperature at which the noise performance is specified (usually taken as $290^{\circ} \mathrm{K}$ ). Substituting (11.156) in (11.148) gives

$$
\begin{equation*}
\frac{T_{n}}{T}=(F-1) \tag{11.157}
\end{equation*}
$$

where $F$ is specified as a ratio and is not in decibels.
Thus noise temperature and noise figure are directly related. The main application of noise temperature provides a convenient expanded measure of noise performance near $F=1$ for very-low-noise amplifiers. A noise figure of $F=2(3 \mathrm{~dB})$ corresponds to $T_{n}=290^{\circ} \mathrm{K}$ and $F=1.1(0.4 \mathrm{~dB})$ corresponds to $T_{n}=29^{\circ} \mathrm{K}$.
